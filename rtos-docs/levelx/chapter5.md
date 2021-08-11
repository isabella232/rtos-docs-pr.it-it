---
title: Capitolo 5 - Supporto Azure RTOS LevelX NOR
description: LA memoria flash NOR è costituita da blocchi in genere divisibile uniformemente per 512 byte. Azure RTOS LevelX divide ogni blocco flash NOR in settori logici a 512 byte.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d5d06fa66f0cae29eeb2a89560704b2ef510597e44a565499bf672a75555f208
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790565"
---
# <a name="chapter-5---azure-rtos-levelx-nor-support"></a>Capitolo 5 - Supporto Azure RTOS LevelX NOR

LA memoria flash NOR è costituita *da blocchi* in genere divisibile uniformemente per 512 byte. Non esiste alcun concetto di pagina flash *nella* memoria flash NOR. Inoltre, non sono presenti byte *di* riserva nella memoria flash NOR, quindi Azure RTOS LevelX deve usare la memoria flash NOR stessa per tutte le informazioni di gestione. L'accesso in lettura diretto è possibile nella memoria flash NOR. L'accesso in scrittura richiede in genere una sequenza speciale di operazioni. La memoria flash NOR può essere scritta più volte, a meno che i bit vengano cancellati. I bit nella memoria flash NOR possono essere impostati una sola volta, tramite l'operazione di cancellazione del blocco.

LevelX divide ogni blocco flash NOR in settori logici *a* 512 byte. LevelX usa inoltre i primi settori "n" di ogni blocco flash NOR per archiviare le informazioni di gestione. Il formato delle informazioni di gestione della memoria flash LevelX NOR è:

**Formato del blocco LevelX NOR**

| Byte Offset  | Contenuto                     |
| ------------ | ---------------------------- |
| 0            | [Conteggio cancellazione blocchi]          |
| 4            | [Settore minimo mappato]      |
| 8            | [Maximum Mapped Sector]      |
| 12           | [Free Sector Bit Map]        |
| m            | [Voce di mapping settore 0]     |
|              | …                            |
| m+4*(n-1)    | [Voce di mapping "n" settore]   |
|              | …                            |
| s            | [Contenuto settore 0]          |
|              | …                            |
| s+512*(n-1) | [Settore "n" Contenuto]         |

Il conteggio delle cancellazioni dei *blocchi a* 32 bit contiene il numero di volte in cui il blocco è stato cancellato. L'obiettivo principale di LevelX è mantenere il conteggio delle cancellazioni di tutti i blocchi relativamente vicino per evitare che un blocco si disassoci prematuramente. I campi Minimum *Mapped Sector* e *Maximum Mapped Sector* a 32 bit vengono scritti solo quando è stato eseguito il mapping e la scrittura di tutti i settori logici nel blocco. Questi campi sono utili per l'ottimizzazione dell'operazione di lettura del settore. La *voce Free Sector Bit Map è* una mappa di bit in cui ogni bit impostato corrisponde a un settore non mappato nel blocco . Questo campo viene usato per rendere più efficiente la ricerca di settori gratuiti. Si tratta di un campo a lunghezza variabile che richiede una parola per ogni 32 settori nel blocco . La *matrice Sector Mapping Entry* contiene informazioni di mapping per ogni settore nel blocco . Ogni voce ha il formato seguente:

**Voce di mapping dei settori**

| Bit | Significato  |
| ------ | -------- |
| 31     | Flag valido. Se impostato e settore logico non tutti indicano che il mapping è valido |
| 30     | Flag obsoleto. Quando è chiaro, questo mapping è obsoleto o sta per diventare obsoleto. |
| 29     | La scrittura della voce di mapping è completa quando questo bit è 0 |
| 0-28   | Settore logico mappato a questo settore fisico, quando non tutti. |

Il bit superiore del campo a 32 bit (bit 31) viene usato per indicare che il mapping del settore logico è valido. Se questo bit è 0, le informazioni contenute in questa voce (e il contenuto del settore corrispondente) non sono più valide. Il bit successivo, il bit 30, viene usato per indicare che questo settore sta diventando obsoleto e che è in corso la scrittura di un nuovo settore. Il bit 29 viene usato per indicare quando la scrittura della voce di mapping è stata completata. Se il bit 29 è 0, la scrittura della voce di mapping è stata completata. Se è impostato il bit 29, la voce di mapping è in fase di scrittura. I bit 30 e 29 vengono usati per il ripristino da una potenziale interruzione dell'alimentazione durante l'aggiornamento di un nuovo mapping di settore. Infine, i 29 bit inferiori (28-0) contengono il numero di settore logico per il settore. Se non è stato eseguito il mapping di un settore, verranno impostati tutti i bit, ad esempio il valore sarà 0xFFFFFFFF.

## <a name="nor-driver-requirements"></a>Requisiti del driver NOR

LevelX richiede un driver flash NOR sottostante specifico della parte flash sottostante e dell'implementazione hardware. Il driver viene specificato in LevelX durante l'inizializzazione tramite l'API ***lx_nor_flash_open***. Il prototipo del driver LevelX è:

```c
INT nor_driver_initialize(LX_NOR_FLASH *instance);
```

Il parametro "*instance*" specifica il blocco di controllo LevelX NOR. La funzione di inizializzazione del driver è responsabile della configurazione di tutti gli altri servizi a livello di driver per l'istanza LevelX associata. I servizi necessari per ogni istanza di LevelX NOR sono:

- Settore di lettura
- Settore di scrittura
- Cancellazione blocchi
- Block Erased Verify
- Gestore degli errori di sistema

## <a name="driver-initialization"></a>Inizializzazione del driver

Questi servizi vengono configurazione tramite l'impostazione di puntatori a funzione **nell'istanza LX_NOR_FLASH** all'interno della funzione di inizializzazione del driver. La funzione di inizializzazione del driver è anche responsabile di:

1. Specifica dell'indirizzo di base della memoria flash.
1. Specifica del numero totale di blocchi e del numero di parole per blocco.
1. Buffer RAM per la lettura di un settore di memoria flash (512 byte) e allineato per l'accesso ULONG.

È probabile che la funzione di inizializzazione del driver esegua anche ulteriori compiti di inizializzazione specifici del dispositivo e/o **dell'implementazione prima** di restituire LX_SUCCESS .

## <a name="driver-read-sector"></a>Settore di lettura driver

Il servizio "settore di lettura" del driver LevelX NOR è responsabile della lettura di un settore specifico in un blocco specifico della memoria flash NOR. Tutta la logica di controllo e correzione degli errori è responsabilità del servizio driver. Se ha esito positivo, il driver LevelX NOR **restituisce LX_SUCCESS**. In caso contrario, il driver LevelX NOR *restituisce LX_ERROR*. Il prototipo del servizio "settore di lettura" del driver LevelX NOR è:

```c
INT nor_driver_read_sector(
    ULONG *flash_address,
    ULONG *destination, 
    ULONG words);
```

Dove "*flash_address*" specifica l'indirizzo di un settore logico all'interno di un blocco flash NOR di memoria e "*destinazione*" e *"* parole " specificano dove posizionare il contenuto del settore e il numero di parole a 32 bit da leggere.

## <a name="driver-write-sector"></a>Settore di scrittura driver

Il servizio "settore di scrittura" del driver LevelX NOR è responsabile della scrittura di un settore specifico in un blocco della memoria flash NOR. Tutto il controllo degli errori è responsabilità del servizio driver. Se ha esito positivo, il driver LevelX NOR **restituisce LX_SUCCESS**. In caso contrario, il driver LevelX NOR **restituisce LX_ERROR**. Il prototipo del servizio "settore di scrittura" del driver LevelX NOR è:

```c
INT nor_driver_write_sector(
    ULONG *flash_address,
    ULONG *source, 
    ULONG words);
```

Dove "*flash_address*" specifica l'indirizzo di un settore logico all'interno di un blocco flash NOR di memoria e "*source*" e "*words*" specificano l'origine della scrittura e il numero di parole a 32 bit da scrivere.

> [!NOTE]
> LevelX si basa sul driver per verificare che il settore di scrittura sia riuscito. Questa operazione viene in genere eseguita leggendo il valore programmato per assicurarsi che corrisponda al valore richiesto da scrivere.

## <a name="driver-block-erase"></a>Cancellazione del blocco di driver

Il servizio di cancellazione dei blocchi del driver LevelX NOR è responsabile della cancellazione del blocco specificato della memoria flash NOR. Se ha esito positivo, il driver LevelX NOR **restituisce LX_SUCCESS**. In caso contrario, il driver LevelX NOR **restituisce LX_ERROR**. Il prototipo del servizio di cancellazione a blocchi del driver LevelX NOR è:

```c
INT nor_driver_block_erase(ULONG block,  
    ULONG erase_count);
```

Dove "*block*" identifica il blocco NOR da cancellare. Il parametro "*erase_count*" viene fornito a scopo diagnostico. Ad esempio, il driver potrebbe voler avvisare un'altra parte del software dell'applicazione quando il numero di cancellazioni supera una soglia specifica.

> [!NOTE]
> LevelX si basa sul driver per esaminare tutti i byte del blocco per assicurarsi che siano cancellati (contengono tutti quelli).

## <a name="driver-block-erased-verify"></a>Verifica della cancellazione del blocco di driver

Il servizio "Verifica cancellazione blocchi" del driver LevelX NOR è responsabile della verifica che il blocco specificato della memoria flash NOR sia stato cancellato. Se viene cancellato, il driver LevelX NOR restituisce **LX_SUCCESS**. Se il blocco non viene cancellato, il driver LevelX NOR restituisce **LX_ERROR**. Il prototipo del servizio di verifica della cancellazione dei blocchi del driver LevelX NOR è:

```c
INT nor_driver_block_erased_verify(ULONG block);
```

Dove "*block*" specifica il blocco per verificare che sia stato cancellato.

> [!NOTE]
> LevelX si basa sul driver per esaminare tutti i byte dell'oggetto specificato per assicurarsi che siano cancellati (contengono tutti quelli).

## <a name="driver-system-error"></a>Errore di sistema del driver

Il servizio "Gestore errori di sistema" del driver LevelX NOR è responsabile dell'impostazione della gestione degli errori di sistema rilevati da LevelX. L'elaborazione in questa routine dipende dall'applicazione. Se ha esito positivo, il driver LevelX NOR restituisce **LX_SUCCESS**. Se l'operazione non riesce, il driver LevelX NOR **restituisce LX_ERROR**. Il prototipo del servizio "errore di sistema" del driver LevelX NOR è:

```c
INT nor_driver_system_error(UINT error_code);
```

Dove "*error_code*" rappresenta l'errore che si è verificato.

## <a name="nor-simulated-driver"></a>DRIVER SIMULATO NOR

LevelX fornisce un driver flash NOR simulato che usa semplicemente ram per simulare il funzionamento di una parte flash NOR. Per impostazione predefinita, il driver simulato NOR fornisce 8 blocchi flash NOR con settori da 16 512 byte per blocco.

La funzione di inizializzazione del driver flash NOR simulato è ***lx_nor_flash_simulator_initialize** _ ed è definita in _*_lx_nor_flash_simulator.c_**. Questo driver fornisce anche un buon modello per la scrittura di driver flash NOR specifici.

## <a name="nor-filex-integration"></a>Integrazione di NOR FileX

Come accennato in precedenza, LevelX non si basa su FileX per il funzionamento. Tutte le API LevelX possono essere chiamate direttamente dal software dell'applicazione per archiviare/recuperare i dati non elaborati nei settori logici forniti da LevelX. LevelX supporta tuttavia anche FileX.

Il file ***fx_nor_flash_simulated_driver.c*** contiene un driver FileX di esempio da usare con la simulazione flash NOR. Il driver Nor Flash FileX per LevelX rappresenta un buon punto di partenza per la scrittura di driver FileX personalizzati.

> [!NOTE]
> Il formato flash NOR FileX deve avere dimensioni di blocco complete dei settori inferiori a quelle fornite dalla memoria flash NOR. Ciò consente di garantire prestazioni ottimali durante l'elaborazione del livello di usura. Altre tecniche per migliorare le prestazioni di scrittura nell'algoritmo di livellamento dell'usura LevelX includono:
> 1. Assicurarsi che tutte le operazioni di scrittura siano esattamente di uno o più cluster di dimensioni e che inizino in corrispondenza dei limiti esatti del cluster.
> 2. Preallocare i cluster prima di eseguire operazioni di scrittura di file di grandi dimensioni tramite fileX ***fx_file_allocate*** di API.
> 3.  L'uso ***periodico lx_nor_flash_defragment*** per liberare il maggior numero possibile di blocchi NOR e quindi migliorare le prestazioni di scrittura.
> 4. Verificare che il driver FileX sia abilitato per ricevere informazioni sui settori di rilascio e che le richieste inviate al driver per rilasciare i settori siano gestite nel driver chiamando ***lx_nor_flash_sector_release***.
