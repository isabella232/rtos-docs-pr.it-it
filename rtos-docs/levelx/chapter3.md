---
title: Azure RTOS LevelX NAND
description: La memoria flash NAD viene in genere usata all'interno di LevelX per l'archiviazione di dati di grandi dimensioni, tipica dei file system.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 950a4f260d032ebe032aca79ac99cc8217915a3b21b230be9475d82b267da18c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790582"
---
# <a name="chapter-3---azure-rtos-levelx-nand-support"></a>Capitolo 3 - Supporto Azure RTOS LevelX NAND

La memoria flash NAD viene in genere usata per l'archiviazione di dati di grandi dimensioni, tipica dei file system. La memoria NAD è costituita da *blocchi*. All'interno di ogni blocco NAND è disponibile una serie di *pagine*. I blocchi NAND sono cancellabili, ovvero tutte le pagine all'interno del blocco NAND vengono cancellate (impostate su tutte). Ogni pagina di blocco NAND ha un set di byte di riserva che vengono utilizzati da Azure RTOS LevelX per la gestione della prenotazione, la gestione dei blocchi non validi e il rilevamento degli errori.  Le pagine in blocchi NAD sono disponibili in diverse dimensioni. Le dimensioni di pagina più comuni sono: 

| **Dimensioni pagina** | **Byte di riserva** |
| ------------- | --------------- |
| 256           | 8               |
| 512           | 16              |
| 2048          | 64              |

La memoria NAD è diversa dalla memoria NOR perché non esiste alcun accesso diretto, ad esempio la memoria NAD non può essere letta direttamente dal processore come la memoria NOR. La memoria NAD può essere scritta solo dopo una cancellazione per un numero limitato di volte. Anche in questo caso, questo comportamento è diverso dalla memoria NOR che può essere scritta un numero illimitato di volte, a seconda che la richiesta di scrittura eserciti la cancellazione dei bit impostati. Infine, i byte di riserva associati a ogni pagina sono univoci per la memoria flash NAD. Le configurazioni tipiche dei byte di riserva sono illustrate nella tabella seguente.

| **Byte di riserva** | **Numeri di byte** | **Configuration**     |
| ------------------------- | -------------- | --------------------- |
| 8                         | Byte 0-2:     | Byte ECC             |
|                           | Byte 3,4,6,7: | Mapping dei settori LevelX |
|                           | Byte 5:        | Flag di blocco non valido        |
| 16                        | Byte 0-3,6-7: | Byte ECC             |
|                           | Byte 8-11:    | Mapping dei settori LevelX |
|                           | Byte 12-15:   | Non utilizzato                |
|                           | Byte 5:        | Flag di blocco non valido        |
| 64                        | Byte 0:        | Flag di blocco non valido        |
|                           | Byte da 2 a 5:     | Mapping dei settori LevelX |
|                           | Byte 6-39:    | Non utilizzato                |
|                           | Byte 40-63:   | Byte ECC             |

LevelX utilizza 4 dei byte di riserva di ogni pagina NAD per tenere traccia del settore logico mappato alla pagina NAD fisica. Questi 4 byte vengono usati per implementare un intero senza segno a 32 bit con un formato proprietario LevelX. Il bit superiore del campo a 32 bit (bit 31) viene usato per indicare che il mapping tra settori logici e pagine è valido. Se questo bit è 0, le informazioni in questa pagina non sono più valide. Il bit successivo, ovvero il bit 30, viene usato per indicare che questa pagina sta diventando obsoleta e che è in corso la scrittura di un nuovo settore. Il bit 29 viene usato per indicare quando la scrittura della voce di mapping è stata completata. Se il bit 29 è 0, la scrittura della voce di mapping è stata completata. Se è impostato il bit 29, la voce di mapping è in corso di scrittura. I bit 30 e 29 vengono usati per il ripristino da una potenziale interruzione dell'alimentazione durante l'aggiornamento di una nuova pagina flash. Infine, i 29 bit inferiori (28-0) contengono il numero di settore logico per la pagina.

**Voce di mapping LevelX**

| Bit(s) | Significato |
| ------ | ------- |
| 31     | Flag valido. Se impostato e il settore logico non è tutti quelli indicano che il mapping è valido |
| 30     | Flag obsoleto. Quando è chiaro, questo mapping è obsoleto o sta per diventare obsoleto. |
| 29     | La scrittura della voce di mapping è completa quando questo bit è 0 |
| 0-28   | Settore logico mappato a questa pagina fisica, quando non tutti. |

LevelX usa anche la prima pagina di ogni blocco NAD per il conteggio di cancellazione dei blocchi, nonché l'elenco di pagine mappate quando il blocco è pieno. Il formato della prima pagina di un blocco NAD in LevelX è illustrato di seguito:

| Formato pagina 0 del blocco LevelX |
|:--------------------------:|
| [Conteggio cancellazione blocchi]        |
| [Page 1 Sector Mapping]    |
| ...                        |
| [Page "n" Sector Mapping]  |
| [0xF0F0F0F0]               |

> [!NOTE]
> Le informazioni di mapping della pagina vengono scritte solo quando il blocco è pieno, ad esempio tutte le pagine del blocco sono state scritte. Ciò consente una ricerca più rapida delle pagine gratuite e del mapping dei settori logici in fase di esecuzione.

## <a name="nand-bad-block-support"></a>Supporto dei blocchi non erati NAND

È anche più probabile che la memoria NAD abbia blocchi non erati rispetto alla memoria NOR. Ciò è dovuto in gran parte al fatto che i produttori DI NAD possono aumentare la produzione consentendo blocchi non dannosi e richiedendo al software di risolvere tali blocchi non dannosi. LevelX gestisce la gestione dei blocchi non valido NAD semplicemente mappando i blocchi non valido.

LevelX fornisce anche API per codici ECC (Hamming Error Correction Code) a 256 byte che il driver LevelX sottostante può usare per calcolare nuovi codici ECC o per eseguire la correzione degli errori a 1 bit durante la lettura della pagina all'interno di ogni sezione di 256 byte della pagina.

## <a name="nand-driver-requirements"></a>Requisiti del driver NAND

LevelX richiede un driver flash NAD sottostante specifico della parte flash sottostante e dell'implementazione hardware. Il driver viene specificato in LevelX durante l'inizializzazione tramite l'API ***lx_nand_flash_open***. Il prototipo del driver LevelX è il seguente.

```c
INT nand_driver_initialize(LX_NAND_FLASH *instance);
```

Il *parametro* dell'istanza specifica il blocco di controllo LevelX NAND. La funzione di inizializzazione del driver è responsabile della configurazione di tutti gli altri servizi a livello di driver per l'istanza LevelX associata. I servizi necessari per ogni istanza NAD LevelX sono visualizzati nell'elenco seguente.

- Lettura pagina
- Pagina di scrittura
- Cancellazione blocchi
- Block Erased Verify
- Verifica cancellazione pagina
- Ottenere lo stato del blocco
- Blocca set di stato
- Blocca byte aggiuntivi get
- Blocca byte aggiuntivi impostati
- Gestore degli errori di sistema

## <a name="driver-initialization"></a>Inizializzazione del driver

Questi servizi vengono configurati tramite l'impostazione di puntatori a funzione **nell'istanza LX_NAND_FLASH** all'interno della funzione di inizializzazione del driver. La funzione di inizializzazione del driver specifica anche il numero totale di blocchi, pagine per blocco, byte per pagina e un'area RAM sufficientemente grande da leggere una pagina in memoria. È probabile che la funzione di inizializzazione del driver esegua anche altri compiti di inizializzazione specifici del dispositivo e/o **dell'implementazione prima** di restituire LX_SUCCESS .

## <a name="driver-read-page"></a>Pagina di lettura del driver

Il servizio "pagina di lettura" del driver NAND LevelX è responsabile della lettura di una pagina specifica in un blocco specifico del flash NAND. Tutta la logica di controllo e correzione degli errori è responsabilità del servizio driver. Se ha esito positivo, il driver NAND LevelX restituisce **LX_SUCCESS**. In caso contrario, il driver NAND LevelX restituisce **LX_ERROR**. Di seguito è riportato il prototipo del servizio "pagina di lettura" del driver NAND LevelX.

```c
INT nand_driver_read_page(
    ULONG block,
    ULONG page,
    ULONG *destination, 
    ULONG words);
```

Dove *block* e *page* identificano la  pagina da leggere e *la destinazione* e le parole specificano dove posizionare il contenuto della pagina e il numero di parole a 32 bit da leggere.

## <a name="driver-write-page"></a>Pagina di scrittura del driver

Il servizio "write page" del driver NAND LevelX è responsabile della scrittura di una pagina specifica nel blocco specificato del flash NAND. Tutto il controllo degli errori e il calcolo ECC è responsabilità del servizio driver. Se ha esito positivo, il driver NAND LevelX restituisce **LX_SUCCESS**. In caso contrario, il driver NAND LevelX restituisce **LX_ERROR**. Il prototipo del servizio "write page" del driver NAND LevelX è illustrato di seguito.

```c
INT nand_driver_write_page(
    ULONG block, 
    ULONG page,
    ULONG *source, 
    ULONG words);
```

Dove *block* e *page* identificano la pagina da scrivere e *l'origine* e *le* parole che specificano l'origine della scrittura e il numero di parole a 32 bit da scrivere.

> [!NOTE]
> LevelX si basa sul driver per il rilevamento degli errori di basso livello durante la scrittura nella pagina flash, che in genere comporta la lettura della pagina e il confronto con il buffer di scrittura per assicurarsi che la scrittura sia riuscita.

## <a name="driver-block-erase"></a>Cancellazione blocchi driver

Il servizio "cancellazione blocchi" del driver NAND LevelX è responsabile della cancellazione del blocco specificato del flash NAND. Se ha esito positivo, il driver NAND LevelX restituisce **LX_SUCCESS**. In caso contrario, il driver NAND LevelX restituisce **LX_ERROR**. Il prototipo del servizio "cancellazione blocchi" del driver NAND LevelX è il seguente.

```c
INT nand_driver_block_erase(ULONG block,  
    ULONG erase_count);
```

Where *block* identifica il blocco da cancellare. Il parametro *erase_count* viene fornito a scopo diagnostico. Ad esempio, il driver potrebbe voler avvisare un'altra parte del software dell'applicazione quando il numero di cancellazioni supera una soglia specifica.

> [!NOTE]
> LevelX si basa sul driver per il rilevamento degli errori di basso livello quando il blocco viene cancellato, che in genere comporta la verifica che tutte le pagine del blocco siano tutte uno.

## <a name="driver-block-erased-verify"></a>Verifica del blocco del driver cancellato

Il servizio di verifica della cancellazione del blocco del driver NAND LevelX è responsabile della verifica della cancellazione del blocco specificato del flash NAND. Se viene cancellato, il driver NAND LevelX **restituisce** LX_SUCCESS . Se il blocco non viene cancellato, il driver NAND LevelX restituisce **LX_ERROR**. Il prototipo del servizio levelx NAND driver "block erased verify" è:

```c
INT nand_driver_block_erased_verify(ULONG block);
```

Where *block* specifica quale blocco verificare che sia stato cancellato.

> [!NOTE]
> LevelX si basa sul driver per esaminare tutte le pagine e tutti i byte di ogni pagina, inclusi i byte di dati e di riserva, per assicurarsi che siano cancellati (contengono tutti).

## <a name="driver-page-erased-verify"></a>Verifica della cancellazione della pagina del driver

Il servizio "page erased verify" del driver NAND LevelX è responsabile della verifica della cancellazione della pagina specificata del blocco specificato del flash NAND. Se viene cancellato, il driver NAND LevelX **restituisce** LX_SUCCESS . Se la pagina non viene cancellata, il driver NAND LevelX restituisce **LX_ERROR**. Il prototipo del servizio "page erased verify" del driver NAND LevelX è:

```c
INT nand_driver_page_erased_verify(
    ULONG block,  
    ULONG page);
```
Where *block* specifica quale blocco e *quale pagina* specifica la pagina per verificare che sia cancellata.

> [!NOTE]
> LevelX si basa sul driver per esaminare tutti i byte della pagina specificata, inclusi i byte di riserva e di dati, per assicurarsi che siano cancellati (contengono tutti quelli).

## <a name="driver-block-status-get"></a>Ottenere lo stato del blocco driver

Il servizio "block status get" del driver NAND LevelX è responsabile del recupero del flag di blocco non valido del blocco specificato del flash NAND. Se ha esito positivo, il driver NAND LevelX restituisce **LX_SUCCESS**. Se non ha esito positivo, il driver NAND LevelX restituisce **LX_ERROR**. Il prototipo del servizio "block status get" del driver NAND LevelX è: illustrato di seguito.

```c
INT nand_driver_block_status_get(
    ULONG block,  
    UCHAR *bad_block_byte);
```

Where *block* specifica quale blocco *e* bad_block_byte specifica la destinazione per il flag di blocco non valido.

## <a name="driver-block-status-set"></a>Driver Block Status Set

Il servizio "block status set" del driver NAND LevelX è responsabile dell'impostazione del flag di blocco non valido del blocco specificato del flash NAND. Se ha esito positivo, il driver NAND LevelX restituisce **LX_SUCCESS**. Se non ha esito positivo, il driver NAND LevelX restituisce **LX_ERROR**. Il prototipo del servizio "block status set" del driver NAND LevelX è:

```c
INT nand_driver_block_status_set(
    ULONG block,
    UCHAR bad_block_byte);
```

Where *block* specifica quale blocco *e* bad_block_byte specifica il valore del flag di blocco non valido.

## <a name="driver-block-extra-bytes-get"></a>Byte aggiuntivi del blocco driver get

Il servizio "block extra bytes get" del driver NAND LevelX è responsabile del recupero di byte aggiuntivi associati a una pagina specifica di un blocco specifico del flash NAND. Se ha esito positivo, il driver NAND LevelX restituisce **LX_SUCCESS**. Se non ha esito positivo, il driver NAND LevelX restituisce **LX_ERROR**. Il prototipo del servizio "block extra bytes get" del driver NAND LevelX è:

```c
INT nand_driver_block_extra_bytes_get(
    ULONG block,  
    ULONG page, 
    UCHAR *destination, 
    UINT size);
```

Where *block* specifica quale blocco, *page* specifica la pagina specifica e *la destinazione* specifica la destinazione per i byte aggiuntivi. La dimensione *del* parametro specifica il numero di byte aggiuntivi da ottenere.

## <a name="driver-block-extra-bytes-set"></a>Set di byte aggiuntivi del blocco driver

Il servizio "block extra bytes set" del driver NAND LevelX è responsabile dell'impostazione di byte aggiuntivi in una pagina specifica di un blocco specifico del flash NAND. Se ha esito positivo, il driver NAND LevelX restituisce **LX_SUCCESS**. Se non ha esito positivo, il driver NAND LevelX restituisce **LX_ERROR**. Il prototipo del servizio "block extra bytes set" del driver NAND LevelX è:

```c
INT nand_driver_block_extra_bytes_set(
    ULONG block,  
    ULONG page, 
    UCHAR *source, 
    UINT size);
```

Where *block* specifica quale blocco, *page* specifica la pagina specifica e *source* specifica l'origine dei byte aggiuntivi. La dimensione *del* parametro specifica il numero di byte aggiuntivi da impostare.

## <a name="driver-system-error"></a>Errore di sistema del driver

Il servizio "Gestore errori di sistema" del driver NAND LevelX è responsabile della gestione degli errori di sistema rilevati da LevelX. L'elaborazione in questa routine dipende dall'applicazione. Se ha esito positivo, il driver NAND LevelX restituisce **LX_SUCCESS**. Se non ha esito positivo, il driver NAND LevelX restituisce **LX_ERROR**. Il prototipo del servizio "errore di sistema" del driver NAND LevelX è:

```c
INT nand_driver_system_error(
    UINT error_code,  
    ULONG block, 
    ULONG page);
```

Where *block* specifica il blocco e *page* specifica la pagina specifica in cui si è verificato l'errore *error_code* errore.

## <a name="nand-simulated-driver"></a>Driver simulato NAND

LevelX fornisce un driver flash NAND simulato che usa semplicemente la RAM per simulare il funzionamento di una parte flash NAND. Per impostazione predefinita, il driver simulato NAND fornisce 8 blocchi flash NAND con 16 pagine per blocco e 2048 byte per pagina.

La funzione di inizializzazione del driver flash NAND simulato è ***lx_nand_flash_simulator_initialize** _ e viene definita in _*_lx_nand_flash_simulator.c_**. Questo driver fornisce anche un buon modello per la scrittura di driver flash NAND specifici.

## <a name="nand-filex-integration"></a>Integrazione fileX NAND

Come accennato in precedenza, LevelX non si basa su FileX per il funzionamento. Tutte le API LevelX possono essere chiamate direttamente dal software dell'applicazione per archiviare/recuperare dati non elaborati nei settori logici forniti da LevelX. LevelX supporta tuttavia anche FileX.

Il file ***fx_nand_flash_simulated_driver.c*** contiene un driver FileX di esempio da usare con la simulazione flash NAND. Un aspetto interessante di questo driver è che combina settori logici a 512 byte in genere usati da FileX in richieste di lettura/scrittura a settore logico singolo al simulatore LevelX usando pagine a 2048 byte. Ciò comporta un uso più efficiente della memoria flash NAND. Il driver FileX flash NAND per LevelX rappresenta un buon punto di partenza per la scrittura di driver FileX personalizzati.  
  
> [!NOTE]
> Il formato flash NAND FileX deve avere dimensioni di un blocco completo di settori inferiori a quelle fornite dal flash NAND. Ciò consente di garantire prestazioni ottimali durante l'elaborazione del livello di usura. Di seguito sono riportate altre tecniche per migliorare le prestazioni di scrittura nell'algoritmo di livellamento dell'usura LevelX.

1. Assicurarsi che tutte le operazioni di scrittura siano esattamente di dimensioni di uno o più cluster e che inizino in base ai limiti esatti del cluster.
1. Preallocare i cluster prima di eseguire operazioni di scrittura di file di grandi dimensioni tramite la ***fx_file_allocate*** fileX di API.
1. Assicurarsi che il driver FileX sia abilitato per ricevere informazioni sul settore di rilascio e che le richieste inviate al driver per rilasciare i settori siano gestite nel driver chiamando ***lx_nor_flash_sector_release***.
1. L'uso ***periodico lx_nand_flash_defragment*** per liberare il maggior numero possibile di blocchi NAND e quindi migliorare le prestazioni di scrittura.
1. Usare l'API ***lx_nand_flash_extended_cache_enable*** per fornire una cache RAM di varie risorse di blocco NAD per ottenere prestazioni più veloci.
