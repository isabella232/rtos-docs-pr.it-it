---
title: Capitolo 5-Azure RTO LevelX e supporto
description: La memoria flash è costituita da blocchi generalmente divisibile in modo uniforme per 512 byte. Azure RTO LevelX divide ogni blocco Flash in settori logici a 512 byte.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3a0c73c2b45c32bf3f1ef56de684fa83c334b59e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822163"
---
# <a name="chapter-5---azure-rtos-levelx-nor-support"></a>Capitolo 5-Azure RTO LevelX e supporto

La memoria flash è costituita da *blocchi* generalmente divisibile in modo uniforme per 512 byte. Non è previsto alcun concetto di *pagina* Flash in memoria o memoria flash. Inoltre, non sono presenti byte di *riserva* nella memoria flash, di conseguenza Azure RTO LevelX deve usare la memoria di memoria flash per tutte le informazioni di gestione. L'accesso in lettura diretto è possibile in o memoria flash. L'accesso in scrittura richiede in genere una sequenza speciale di operazioni. La memoria flash può essere scritta più volte, a condizione che i bit vengano cancellati. I bit in o la memoria flash possono essere impostati solo una volta, tramite l'operazione di cancellazione del blocco.

LevelX divide ogni blocco Flash in *settori* logici a 512 byte. Inoltre, LevelX usa i primi "n" settori di ogni blocco Flash per archiviare le informazioni di gestione. Il formato di LevelX o le informazioni di gestione della memoria flash sono:

**LevelX e formato di blocco**

| Offset byte  | Contenuto                     |
| ------------ | ---------------------------- |
| 0            | [Conteggio blocchi cancellati]          |
| 4            | [Settore minimo mappato]      |
| 8            | [Settore con mapping massimo]      |
| 12           | [Mappa di bit per settore gratuito]        |
| m            | [Voce di mapping settore 0]     |
|              | …                            |
| m + 4 * (n-1)    | [Voce di mapping settore "n"]   |
|              | …                            |
| s            | [Contenuto settore 0]          |
|              | …                            |
| s + 512 * (n-1) | [Contenuto settore "n"]         |

Il *conteggio di cancellazione dei blocchi* a 32 bit contiene il numero di volte in cui il blocco è stato cancellato. L'obiettivo principale di LevelX consiste nel limitare il numero di cancelli di tutti i blocchi relativamente vicini per evitare che un blocco venga esaurito in modo anomalo. Il *settore con mapping minimo* a 32 bit e i campi di *settore con mapping massimo* vengono scritti solo quando tutti i settori logici del blocco sono stati mappati e scritti in. Questi campi sono utili per l'ottimizzazione dell'operazione di lettura del settore. La voce della *mappa di bit del settore gratuito* è una mappa di bit in cui ogni bit del set corrisponde a un settore non mappato nel blocco. Questo campo viene usato per rendere più efficiente la ricerca nel settore gratuito. Si tratta di un campo a lunghezza variabile che richiede una parola per ogni settore 32 nel blocco. La matrice di *voci di mapping del settore* contiene informazioni di mapping per ogni settore nel blocco. Ogni voce ha il formato seguente:

**Voce mapping settore**

| Bit/i | Significato  |
| ------ | -------- |
| 31     | Flag valido. Quando l'impostazione e il settore logico non sono tutti quelli indicati, il mapping è valido |
| 30     | Flag obsoleto. Se chiaro, questo mapping è obsoleto o sta per diventare obsoleto. |
| 29     | La scrittura della voce di mapping è completa quando questo bit è 0 |
| 0-28   | Settore logico mappato a questo settore fisico, quando non tutti gli altri. |

Il bit superiore del campo a 32 bit (bit 31) viene utilizzato per indicare che il mapping del settore logico è valido. Se il bit è 0, le informazioni in questa voce (e il relativo contenuto del settore) non sono più valide. Il successivo bit bit 30 viene usato per indicare che questo settore è in corso di diventare obsoleto ed è in corso la scrittura di un nuovo settore. Il bit 29 viene utilizzato per indicare il completamento della scrittura della voce di mapping. Se il bit 29 è 0, la scrittura della voce di mapping è stata completata. Se è impostato il bit 29, è in corso la scrittura della voce di mapping. I bit 30 e 29 vengono usati per il ripristino da una potenziale perdita di energia durante l'aggiornamento di un nuovo mapping di settore. Infine, i 29 bit inferiori (28-0) contengono il numero di settore logico per il settore. Se non è stato eseguito il mapping di un settore, verranno impostati tutti i bit, vale a dire il valore 0xFFFFFFFF.

## <a name="nor-driver-requirements"></a>E requisiti dei driver

LevelX richiede un driver sottostante o flash specifico per l'implementazione dell'hardware e della parte Flash sottostante. Il driver viene specificato per LevelX durante l'inizializzazione tramite l'API ***lx_nor_flash_open***. Il prototipo del driver LevelX è:

```c
INT nor_driver_initialize(LX_NOR_FLASH *instance);
```

Il parametro "*instance*" specifica il LevelX e il blocco di controllo. La funzione di inizializzazione driver è responsabile della configurazione di tutti gli altri servizi a livello di driver per l'istanza di LevelX associata. I servizi richiesti per ogni LevelX o istanza sono:

- Leggi settore
- Settore di scrittura
- Cancella blocco
- Verifica cancellazione blocco
- Gestore errori di sistema

## <a name="driver-initialization"></a>Inizializzazione driver

Questi servizi vengono impostati tramite l'impostazione di puntatori a funzione nell'istanza **LX_NOR_FLASH** all'interno della funzione di inizializzazione del driver. La funzione di inizializzazione del driver è responsabile anche di:

1. Specificare l'indirizzo di base del flash.
1. Specifica del numero totale di blocchi e del numero di parole per blocco.
1. Buffer RAM per la lettura di un settore di Flash (512 byte) e allineato per l'accesso ULONG.

La funzione di inizializzazione dei driver esegue probabilmente anche ulteriori attività di inizializzazione specifiche del dispositivo e/o dell'implementazione prima di restituire **LX_SUCCESS**.

## <a name="driver-read-sector"></a>Settore di lettura driver

Il servizio LevelX e il driver "Read Sector" è responsabile della lettura di un settore specifico in un blocco specifico di o Flash. Tutte le verifiche degli errori e la logica di correzione sono responsabilità del servizio driver. In caso di esito positivo, il LevelX o il driver restituisce **LX_SUCCESS**. In caso di esito negativo, il LevelX o il driver restituisce *LX_ERROR*. Il prototipo del servizio LevelX e del driver "Read Sector" è:

```c
INT nor_driver_read_sector(
    ULONG *flash_address,
    ULONG *destination, 
    ULONG words);
```

Dove "*flash_address*" specifica l'indirizzo di un settore logico all'interno di un blocco di memoria, di memoria e di "*destinazione*" e "*parole*", che specificano la posizione in cui inserire il contenuto del settore e il numero di parole a 32 bit da leggere.

## <a name="driver-write-sector"></a>Settore scrittura driver

Il servizio LevelX e il driver "Write Sector" è responsabile della scrittura di un settore specifico in un blocco di o Flash. Il controllo degli errori è responsabilità del servizio driver. In caso di esito positivo, il LevelX o il driver restituisce **LX_SUCCESS**. In caso di esito negativo, il LevelX o il driver restituisce **LX_ERROR**. Il prototipo del servizio LevelX e del driver "scrittura settore" è:

```c
INT nor_driver_write_sector(
    ULONG *flash_address,
    ULONG *source, 
    ULONG words);
```

Dove "*flash_address*" specifica l'indirizzo di un settore logico all'interno di un blocco di memoria o di un blocco Flash e "*source*" e "*Words*" specificano l'origine della scrittura e il numero di parole a 32 bit da scrivere.

> [!NOTE]
> LevelX si basa sul driver per verificare che il settore di scrittura abbia avuto esito positivo. Questa operazione viene in genere eseguita leggendo indietro il valore programmato per assicurarsi che corrisponda al valore richiesto da scrivere.

## <a name="driver-block-erase"></a>Cancellazione blocco driver

Il servizio LevelX e il driver "block erase" è responsabile della cancellazione del blocco specificato di o del flash. In caso di esito positivo, il LevelX o il driver restituisce **LX_SUCCESS**. In caso di esito negativo, il LevelX o il driver restituisce **LX_ERROR**. Il prototipo del servizio LevelX e del driver "block erase" è:

```c
INT nor_driver_block_erase(ULONG block,  
    ULONG erase_count);
```

Dove "*Block*" identifica i blocchi da cancellare. Il parametro "*erase_count*" viene fornito a scopo diagnostico. Ad esempio, il driver potrebbe voler avvisare un'altra parte del software applicativo quando il numero di cancellazioni supera una soglia specifica.

> [!NOTE]
> LevelX si basa sul driver per esaminare tutti i byte del blocco per assicurarsi che vengano cancellati (contenere tutti).

## <a name="driver-block-erased-verify"></a>Verifica cancellazione blocco driver

Il servizio LevelX e il driver "Block Cancellated Verify" è responsabile della verifica della cancellazione del blocco specificato di o del flash. Se viene cancellato, il LevelX o il driver restituisce **LX_SUCCESS**. Se il blocco non viene cancellato, il LevelX o il driver restituisce **LX_ERROR**. Il prototipo del servizio LevelX e del driver "blocca la verifica cancellata" è:

```c
INT nor_driver_block_erased_verify(ULONG block);
```

Dove "*Block*" specifica quale blocco verificare che venga cancellato.

> [!NOTE]
> LevelX si basa sul driver per esaminare tutti i byte dell'oggetto specificato per assicurarsi che vengano cancellati (contenere tutti).

## <a name="driver-system-error"></a>Errore di sistema del driver

Il servizio "gestore errori di sistema" di LevelX e driver è responsabile dell'impostazione degli errori di sistema di gestione rilevati da LevelX. L'elaborazione in questa routine dipende dall'applicazione. Se l'operazione ha esito positivo, il LevelX o il driver restituisce **LX_SUCCESS**. Se l'operazione ha esito negativo, LevelX e il driver restituiscono **LX_ERROR**. Il prototipo del servizio LevelX o del driver "errore di sistema" è:

```c
INT nor_driver_system_error(UINT error_code);
```

Dove "*error_code*" rappresenta l'errore che si è verificato.

## <a name="nor-simulated-driver"></a>O driver simulato

LevelX fornisce un driver simulato o Flash che usa semplicemente la RAM per simulare il funzionamento di una parte o di una parte Flash. Per impostazione predefinita, il driver non simulato non fornisce 8 né blocchi flash con settori a 16 512 byte per blocco.

La funzione di inizializzazione del driver simulato e Flash è ***lx_nor_flash_simulator_initialize** _ ed è definita in _ *_lx_nor_flash_simulator. c_* *. Questo driver fornisce anche un modello valido per la scrittura di driver specifici o Flash.

## <a name="nor-filex-integration"></a>NÉ integrazione con FileX

Come indicato in precedenza, LevelX non si basa su FileX per Operation. Tutte le API di LevelX possono essere chiamate direttamente dal software dell'applicazione per archiviare o recuperare dati non elaborati nei settori logici forniti da LevelX. Tuttavia, LevelX supporta anche FileX.

Il file ***fx_nor_flash_simulated_driver. c*** contiene un driver FILEX di esempio da usare con la simulazione di o Flash. Il driver FileX o Flash per LevelX fornisce un valido punto di partenza per la scrittura di driver FileX personalizzati.

> [!NOTE]
> Il formato FileX o Flash deve essere una dimensione di blocco completo dei settori minori di e non fornisce Flash. Ciò consente di garantire prestazioni ottimali durante l'elaborazione del livello di usura. Altre tecniche per migliorare le prestazioni di scrittura nell'algoritmo di livellamento dell'uso di LevelX includono:
> 1. Verificare che tutte le Scritture siano esattamente di uno o più cluster e che inizino con i limiti esatti del cluster.
> 2. Pre-allocare i cluster prima di eseguire operazioni di scrittura di file di grandi dimensioni tramite la classe FileX ***fx_file_allocate*** di API.
> 3.  Uso periodico di ***lx_nor_flash_defragment*** per liberare il maggior numero possibile di blocchi e, di conseguenza, migliorare le prestazioni di scrittura.
> 4. Verificare che il driver FileX sia abilitato per ricevere le informazioni sul settore di rilascio e le richieste effettuate al driver per rilasciare i settori vengono gestite nel driver chiamando ***lx_nor_flash_sector_release***.
