---
title: Supporto per NAND LevelX di Azure RTO
description: La memoria flash NAND viene comunemente utilizzata all'interno di LevelX per l'archiviazione di dati di grandi dimensioni, che è tipica dei file System.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3286e4ea7f16b28ff55fc95a87a1e0c313ec4240
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822172"
---
# <a name="chapter-3---azure-rtos-levelx-nand-support"></a>Capitolo 3-supporto per NAND LevelX di Azure RTO

La memoria flash NAND viene in genere utilizzata per l'archiviazione di dati di grandi dimensioni, che è tipica dei file System. La memoria NAND è costituita da *blocchi*. All'interno di ogni blocco NAND è presente una serie di *pagine*. I blocchi NAND sono cancellabili, il che significa che tutte le pagine all'interno del blocco NAND vengono cancellate (impostate su tutte). Ogni pagina di blocco NAND ha un set di *byte di riserva* usati da Azure RTO LevelX per la contabilità, la gestione dei blocchi non corretti e il rilevamento degli errori. Le pagine di blocco NAND sono disponibili in un'ampia gamma di dimensioni. Le dimensioni di pagina più comuni sono: 

| **Dimensioni pagina** | **Byte di riserva** |
| ------------- | --------------- |
| 256           | 8               |
| 512           | 16              |
| 2048          | 64              |

La memoria NAND è diversa dalla memoria e non è presente alcun accesso diretto, ovvero non è possibile leggere la memoria NAND direttamente dal processore, ad esempio o memoria. La memoria NAND può essere scritta solo dopo una cancellazione di un numero limitato di volte. Anche in questo caso, questo comportamento è diverso da quello della memoria che può essere scritto per un numero illimitato di volte, purché la richiesta di scrittura stia cancellando i bit impostati. Infine, i byte di riserva associati a ogni pagina sono univoci per NAND Flash. Le configurazioni tipiche dei byte di riserva sono illustrate nella tabella seguente.

| **Byte di riserva** | **Numeri di byte** | **Configuration**     |
| ------------------------- | -------------- | --------------------- |
| 8                         | Byte 0-2:     | Byte ECC             |
|                           | Byte 3, 4, 6, 7: | Mapping del settore LevelX |
|                           | Byte 5:        | Flag di blocco non valido        |
| 16                        | Byte 0-3, 6-7: | Byte ECC             |
|                           | Byte 8-11:    | Mapping del settore LevelX |
|                           | Byte 12-15:   | Non utilizzato                |
|                           | Byte 5:        | Flag di blocco non valido        |
| 64                        | Byte 0:        | Flag di blocco non valido        |
|                           | Byte 2-5:     | Mapping del settore LevelX |
|                           | Byte 6-39:    | Non utilizzato                |
|                           | Byte 40-63:   | Byte ECC             |

LevelX utilizza 4 dei byte di riserva di ogni pagina NAND per tenere traccia del settore logico mappato alla pagina NAND fisica. Questi 4 byte vengono usati per implementare un Unsigned Integer a 32 bit con un formato proprietario di LevelX. Il bit superiore del campo a 32 bit (bit 31) viene utilizzato per indicare che il mapping da settore a pagina logico è valido. Se il bit è 0, le informazioni in questa pagina non sono più valide. Il bit successivo, bit 30, viene usato per indicare che questa pagina è in corso di diventare obsoleta ed è in corso la scrittura di un nuovo settore. Il bit 29 viene utilizzato per indicare il completamento della scrittura della voce di mapping. Se il bit 29 è 0, la scrittura della voce di mapping è stata completata. Se è impostato il bit 29, è in corso la scrittura della voce di mapping. I bit 30 e 29 vengono usati per il ripristino da una potenziale perdita di energia durante l'aggiornamento di una nuova pagina Flash. Infine, i 29 bit inferiori (28-0) contengono il numero di settore logico per la pagina.

**Voce di mapping di LevelX**

| Bit/i | Significato |
| ------ | ------- |
| 31     | Flag valido. Quando l'impostazione e il settore logico non sono tutti quelli indicati, il mapping è valido |
| 30     | Flag obsoleto. Se chiaro, questo mapping è obsoleto o sta per diventare obsoleto. |
| 29     | La scrittura della voce di mapping è completa quando questo bit è 0 |
| 0-28   | Settore logico mappato a questa pagina fisica, quando non tutti. |

LevelX utilizza inoltre la prima pagina di ogni blocco NAND per il conteggio delle cancellazioni dei blocchi, nonché l'elenco delle pagine mappate quando il blocco è pieno. Il formato della prima pagina di un blocco NAND in LevelX è illustrato di seguito:

| Formato della pagina 0 del blocco LevelX |
|:--------------------------:|
| [Conteggio blocchi cancellati]        |
| [Mapping di settore di pagina 1]    |
| ...                        |
| [Mapping del settore di pagina "n"]  |
| [0xF0F0F0F0]               |

> [!NOTE]
> Le informazioni sul mapping della pagina vengono scritte solo quando il blocco è pieno, ovvero tutte le pagine del blocco sono state scritte in. In questo modo è possibile cercare più velocemente le pagine gratuite e il mapping dei settori logici in fase di esecuzione.

## <a name="nand-bad-block-support"></a>Supporto del blocco non valido NAND

È inoltre più probabile che la memoria NAND disponga di blocchi danneggiati e non di memoria. Questa operazione è in gran parte dovuta al fatto che i produttori di NAND possono aumentare il rendimento consentendo blocchi danneggiati e richiedendo il software per aggirare tali blocchi danneggiati. LevelX gestisce la gestione dei blocchi non validi di NAND semplicemente eseguendo il mapping intorno a blocchi danneggiati.

LevelX fornisce anche API per i codici di correzione degli errori di Hamming a 256 byte per il driver LevelX sottostante da utilizzare per il calcolo di nuovi codici ECC o per la correzione di errori a 1 bit nella lettura della pagina all'interno di ogni sezione 256 byte della pagina.

## <a name="nand-driver-requirements"></a>Requisiti del driver NAND

LevelX richiede un driver Flash NAND sottostante specifico per l'implementazione dell'hardware e della parte Flash sottostante. Il driver viene specificato per LevelX durante l'inizializzazione tramite l'API ***lx_nand_flash_open***. Il prototipo del driver LevelX è il seguente.

```c
INT nand_driver_initialize(LX_NAND_FLASH *instance);
```

Il parametro *instance* specifica il blocco di controllo NAND LevelX. La funzione di inizializzazione driver è responsabile della configurazione di tutti gli altri servizi a livello di driver per l'istanza di LevelX associata. I servizi richiesti per ogni istanza di LevelX NAND sono visualizzati nell'elenco seguente.

- Leggi pagina
- Scrivi pagina
- Cancella blocco
- Verifica cancellazione blocco
- Verifica cancellazione pagina
- Ottieni stato blocco
- Imposta stato blocco
- Blocca i byte aggiuntivi Get
- Blocca i byte aggiuntivi impostati
- Gestore errori di sistema

## <a name="driver-initialization"></a>Inizializzazione driver

Questi servizi vengono impostati tramite l'impostazione di puntatori a funzione nell'istanza **LX_NAND_FLASH** all'interno della funzione di inizializzazione del driver. La funzione di inizializzazione del driver specifica anche il numero totale di blocchi, pagine per blocco, byte per pagina e un'area RAM sufficientemente grande da leggere una pagina in memoria. La funzione di inizializzazione dei driver esegue probabilmente anche ulteriori attività di inizializzazione specifiche del dispositivo e/o dell'implementazione prima di restituire **LX_SUCCESS**.

## <a name="driver-read-page"></a>Pagina lettura driver

Il servizio "lettura pagina" del driver NAND LevelX è responsabile della lettura di una pagina specifica in un blocco specifico del flash NAND. Tutte le verifiche degli errori e la logica di correzione sono responsabilità del servizio driver. In caso di esito positivo, il driver LevelX NAND restituisce **LX_SUCCESS**. Se l'operazione non riesce, il driver LevelX NAND restituisce **LX_ERROR**. Il prototipo del servizio "lettura pagina" del driver NAND LevelX è riportato di seguito.

```c
INT nand_driver_read_page(
    ULONG block,
    ULONG page,
    ULONG *destination, 
    ULONG words);
```

Dove *blocco* e *pagina* identificano la pagina da leggere e la *destinazione* e le *parole* specificano dove inserire il contenuto della pagina e il numero di parole a 32 bit da leggere.

## <a name="driver-write-page"></a>Pagina scrittura driver

Il servizio "scrittura pagina" del driver NAND LevelX è responsabile della scrittura di una pagina specifica nel blocco specificato del flash NAND. Il controllo degli errori e il calcolo ECC sono la responsabilità del servizio driver. In caso di esito positivo, il driver LevelX NAND restituisce **LX_SUCCESS**. Se l'operazione non riesce, il driver LevelX NAND restituisce **LX_ERROR**. Il prototipo del servizio "scrittura pagina" del driver NAND LevelX è illustrato di seguito.

```c
INT nand_driver_write_page(
    ULONG block, 
    ULONG page,
    ULONG *source, 
    ULONG words);
```

Dove *blocco* e *pagina* identificano la pagina da scrivere e l' *origine* e le *parole* specificano l'origine della scrittura e il numero di parole a 32 bit da scrivere.

> [!NOTE]
> LevelX si basa sul driver per il rilevamento degli errori di basso livello durante la scrittura nella pagina Flash, che in genere comporta la lettura della pagina e il confronto con il buffer di scrittura per garantire la corretta scrittura.

## <a name="driver-block-erase"></a>Cancellazione blocco driver

Il servizio "blocco Erase" del driver NAND LevelX è responsabile della cancellazione del blocco specificato del flash NAND. In caso di esito positivo, il driver LevelX NAND restituisce **LX_SUCCESS**. Se l'operazione non riesce, il driver LevelX NAND restituisce **LX_ERROR**. Il prototipo del servizio "blocco Erase" del driver NAND LevelX è il seguente.

```c
INT nand_driver_block_erase(ULONG block,  
    ULONG erase_count);
```

Dove *Block* identifica il blocco da cancellare. Il parametro *erase_count* viene fornito a scopo diagnostico. Ad esempio, il driver potrebbe voler avvisare un'altra parte del software applicativo quando il numero di cancellazioni supera una soglia specifica.

> [!NOTE]
> LevelX si basa sul driver per il rilevamento degli errori di basso livello quando il blocco viene cancellato, che in genere comporta la verifica che tutte le pagine del blocco siano tutte quelle.

## <a name="driver-block-erased-verify"></a>Verifica cancellazione blocco driver

Il servizio "Block eraseed Verify" del driver NAND LevelX è responsabile della verifica della cancellazione del blocco specificato del flash NAND. Se viene cancellato, il driver LevelX NAND restituisce **LX_SUCCESS**. Se il blocco non viene cancellato, il driver LevelX NAND restituisce **LX_ERROR**. Il prototipo del servizio "Block eraseed Verify" del driver NAND LevelX è:

```c
INT nand_driver_block_erased_verify(ULONG block);
```

Where *Block* specifica quale blocco verificare che venga cancellato.

> [!NOTE]
> LevelX si basa sul driver per esaminare tutte le pagine e tutti i byte di ogni pagina, inclusi i byte di riserva e di dati, per assicurarsi che vengano cancellati (contenere tutti).

## <a name="driver-page-erased-verify"></a>Verifica cancellazione pagina driver

Il servizio del driver NAND LevelX "pagina di verifica cancellata" è responsabile della verifica della cancellazione della pagina specificata del blocco specificato del flash NAND. Se viene cancellato, il driver LevelX NAND restituisce **LX_SUCCESS**. Se la pagina non viene cancellata, il driver LevelX NAND restituisce **LX_ERROR**. Il prototipo del servizio del driver NAND LevelX "pagina di verifica cancellata" è:

```c
INT nand_driver_page_erased_verify(
    ULONG block,  
    ULONG page);
```
Where *Block* specifica il blocco e la *pagina* che specificano la pagina per verificare che venga cancellata.

> [!NOTE]
> LevelX si basa sul driver per esaminare tutti i byte della pagina specificata, inclusi i byte di riserva e di dati, per assicurarsi che vengano cancellati (contenere tutti i byte).

## <a name="driver-block-status-get"></a>Stato blocco driver Get

Il servizio "stato blocco Get" del driver NAND LevelX è responsabile del recupero del flag di blocco errato del blocco specificato del flash NAND. Se l'operazione ha esito positivo, il driver LevelX NAND restituisce **LX_SUCCESS**. Se l'operazione ha esito negativo, il driver LevelX NAND restituisce **LX_ERROR**. Il prototipo del servizio "blocco stato Get" del driver NAND LevelX è: illustrato di seguito.

```c
INT nand_driver_block_status_get(
    ULONG block,  
    UCHAR *bad_block_byte);
```

Where *Block* specifica quale blocco e *bad_block_byte* specifica la destinazione per il flag di blocco errato.

## <a name="driver-block-status-set"></a>Set di Stati del blocco driver

Il servizio "set status Block" del driver NAND LevelX è responsabile dell'impostazione del flag di blocco errato del blocco specificato del flash NAND. Se l'operazione ha esito positivo, il driver LevelX NAND restituisce **LX_SUCCESS**. Se l'operazione ha esito negativo, il driver LevelX NAND restituisce **LX_ERROR**. Il prototipo del servizio "Block status set" del driver NAND LevelX è:

```c
INT nand_driver_block_status_set(
    ULONG block,
    UCHAR bad_block_byte);
```

Where *Block* specifica quale blocco e *bad_block_byte* specifica il valore del flag di blocco errato.

## <a name="driver-block-extra-bytes-get"></a>Blocco driver aggiuntivo Byte Get

Il servizio "blocca byte aggiuntivi Get" del driver NAND LevelX è responsabile del recupero di byte aggiuntivi associati a una pagina specifica di un blocco specifico del flash NAND. Se l'operazione ha esito positivo, il driver LevelX NAND restituisce **LX_SUCCESS**. Se l'operazione ha esito negativo, il driver LevelX NAND restituisce **LX_ERROR**. Il prototipo del servizio "blocca byte aggiuntivi Get" del driver NAND LevelX è:

```c
INT nand_driver_block_extra_bytes_get(
    ULONG block,  
    ULONG page, 
    UCHAR *destination, 
    UINT size);
```

Where *Block* specifica il blocco, la *pagina* specifica la pagina specifica e la *destinazione* specifica la destinazione per i byte aggiuntivi. La *dimensione* del parametro specifica il numero di byte aggiuntivi da ottenere.

## <a name="driver-block-extra-bytes-set"></a>Set di byte aggiuntivi del blocco driver

Il servizio LevelX NAND driver "Block extra bytes set" è responsabile dell'impostazione di byte aggiuntivi in una pagina specifica di un blocco specifico del flash NAND. Se l'operazione ha esito positivo, il driver LevelX NAND restituisce **LX_SUCCESS**. Se l'operazione ha esito negativo, il driver LevelX NAND restituisce **LX_ERROR**. Il prototipo del servizio "blocco di byte aggiuntivi di LevelX" del driver NAND è:

```c
INT nand_driver_block_extra_bytes_set(
    ULONG block,  
    ULONG page, 
    UCHAR *source, 
    UINT size);
```

Dove *Block* specifica il blocco, la *pagina* specifica la pagina e l' *origine* specifici che specificano l'origine dei byte aggiuntivi. Le *dimensioni* del parametro specificano il numero di byte aggiuntivi da impostare.

## <a name="driver-system-error"></a>Errore di sistema del driver

Il servizio "gestore errori di sistema" del driver LevelX NAND è responsabile dell'impostazione degli errori di sistema di gestione rilevati da LevelX. L'elaborazione in questa routine dipende dall'applicazione. Se l'operazione ha esito positivo, il driver LevelX NAND restituisce **LX_SUCCESS**. Se l'operazione ha esito negativo, il driver LevelX NAND restituisce **LX_ERROR**. Il prototipo del servizio "errore di sistema" del driver NAND LevelX è:

```c
INT nand_driver_system_error(
    UINT error_code,  
    ULONG block, 
    ULONG page);
```

Dove *Block* specifica il blocco e la *pagina* specifica la pagina specifica in cui si è verificato l'errore rappresentato da *error_code* .

## <a name="nand-simulated-driver"></a>Driver simulato NAND

LevelX fornisce un driver Flash NAND simulato che usa semplicemente RAM per simulare il funzionamento di una parte Flash NAND. Per impostazione predefinita, il driver simulato NAND fornisce 8 blocchi flash NAND con 16 pagine per blocco e 2048 byte per pagina.

La funzione di inizializzazione del driver Flash NAND simulato è ***lx_nand_flash_simulator_initialize** _ ed è definita in _ *_lx_nand_flash_simulator. c_* *. Questo driver fornisce anche un modello valido per la scrittura di driver Flash NAND specifici.

## <a name="nand-filex-integration"></a>Integrazione di FileX NAND

Come indicato in precedenza, LevelX non si basa su FileX per Operation. Tutte le API di LevelX possono essere chiamate direttamente dal software dell'applicazione per archiviare o recuperare dati non elaborati nei settori logici forniti da LevelX. Tuttavia, LevelX supporta anche FileX.

Il file ***fx_nand_flash_simulated_driver. c*** contiene un driver FILEX di esempio da usare con la simulazione Flash NAND. Un aspetto interessante di questo driver è che combina settori logici a 512 byte usati in genere da FileX in singole richieste di lettura/scrittura nel settore logico per il simulatore LevelX usando pagine a 2048 byte. Questo comporta un uso più efficiente della memoria flash NAND. Il driver FileX NAND Flash per LevelX fornisce un valido punto di partenza per la scrittura di driver FileX personalizzati.  
  
> [!NOTE]
> Il formato Flash NAND di FileX deve essere costituito da una dimensione blocco completo dei settori minori rispetto a quelle fornite da NAND Flash. Ciò consente di garantire prestazioni ottimali durante l'elaborazione del livello di usura. Le tecniche aggiuntive per migliorare le prestazioni di scrittura nell'algoritmo di livellamento dell'uso di LevelX includono quanto segue.

1. Verificare che tutte le Scritture siano esattamente di uno o più cluster e che inizino con i limiti esatti del cluster.
1. Pre-allocare i cluster prima di eseguire operazioni di scrittura di file di grandi dimensioni tramite la classe FileX ***fx_file_allocate*** di API.
1. Verificare che il driver FileX sia abilitato per ricevere le informazioni sul settore di rilascio e le richieste effettuate al driver per rilasciare i settori vengono gestite nel driver chiamando ***lx_nor_flash_sector_release***.
1. Uso periodico di ***lx_nand_flash_defragment*** per liberare il maggior numero possibile di blocchi NAND e migliorare quindi le prestazioni di scrittura.
1. Usare l'API ***lx_nand_flash_extended_cache_enable*** per fornire una cache RAM di varie risorse del blocco NAND per ottenere prestazioni più veloci.
