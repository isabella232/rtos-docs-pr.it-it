---
title: Capitolo 3-componenti funzionali di Azure RTO FileX
description: Questo capitolo contiene una descrizione del file system di Azure RTO FileX embedded a prestazioni elevate dal punto di vista funzionale
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1e1e1a1dbd844d811c7ee3122113f28162639fb4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821437"
---
# <a name="chapter-3---functional-components-of-azure-rtos-filex"></a>Capitolo 3-componenti funzionali di Azure RTO FileX

Questo capitolo contiene una descrizione del file system di Azure RTO FileX embedded a prestazioni elevate dal punto di vista funzionale.

## <a name="media-description"></a>Descrizione supporti

FileX è un file system incorporato a prestazioni elevate conforme al formato di file system FAT. FileX Visualizza i supporti fisici come una matrice di settori logici. Il modo in cui viene eseguito il mapping di questi settori al supporto fisico sottostante è determinato dal driver di I/O connesso al supporto FileX durante la chiamata ***fx_media_open*** .

### <a name="fat121632-logical-sectors"></a>Settori logici FAT12/16/32

L'esatta organizzazione dei settori logici del supporto è determinata dal contenuto del record di avvio dei supporti fisici. Il layout generale dei settori logici del supporto è illustrato nella figura 1.

I settori logici FileX iniziano dal settore logico 1, che punta al primo settore riservato del supporto. I settori riservati sono facoltativi, ma quando vengono usati in genere contengono informazioni di sistema, ad esempio il codice di avvio.

### <a name="fat121632-media-boot-record"></a>Record di avvio multimediale FAT12/16/32

L'offset esatto del settore delle altre aree nella visualizzazione del settore logico del supporto deriva dal contenuto del *record di avvio multimediale*. Il percorso del record di avvio è in genere il settore 0. Tuttavia, se il supporto ha *settori nascosti*, è necessario che l'offset al settore di avvio li tenga conto (si trovano immediatamente prima del settore di avvio). Nella tabella 1 sono elencati i componenti dei record di avvio dei supporti e i componenti sono descritti nei paragrafi.

- **Istruzione di salto** Il campo *Jump istruzione* è un campo a tre byte che rappresenta un'istruzione Intel x86 computer per un salto del processore. Si tratta di un campo Legacy nella maggior parte dei casi.

  ![Visualizzazione settore logico multimediale FileX](./media/user-guide/filex-media-logical-sector-view.png)

  **FIGURA 1. Visualizzazione settore logico multimediale FileX**

- **Nome OEM** Il campo *nome OEM* è riservato ai produttori per inserire il nome o un nome per il dispositivo.
- **Byte per settore** Il campo *byte per settore* nel record di avvio multimediale definisce il numero di byte in ogni settore, ovvero l'elemento fondamentale del supporto.
- **Settori per cluster** Il campo *settori per cluster* nel record di avvio multimediale definisce il numero di settori assegnati a un cluster. Il cluster è l'elemento di allocazione fondamentale in un file system compatibile con FAT. Tutte le informazioni sui file e le sottodirectory vengono allocate dai cluster disponibili del supporto come determinato dalla tabella di allocazione file (FAT).

    **TABELLA 1. Record di avvio multimediale FileX**
    |Offset  |Campo  |Numero di byte|
    |----------|-----------|------------|
    |0x00|Istruzione Jump (E9, XX, XX o EB, XX, 90)|3|
    |0x03|Nome OEM|8|
    |0x0B|Byte per settore|2|
    |0x0D|Settori per cluster|1|
    |0x0E|Numero di settori riservati|2|
    |0x10|Numero di grassi|1|
    |0x11|Dimensioni della directory radice|2|
    |0x13|Numero di settori FAT-12 &amp; FAT-16|2|
    |0x15|Tipo supporto|1|
    |0x16|Numero di settori per FAT|2|
    |0x18|Settori per traccia|2|
    |0x1A|Numero di intestazioni|2|
    |0x1C|Numero di settori nascosti|4|
    |0x20|Numero di settori-FAT-32|4|
    |0x24|Settori per grasso (FAT-32)|4|
    |0x2C|Cluster di directory radice|4|
    |0x3E|Codice di avvio del sistema|448
    |0x1FE|0x55AA|2|

- **Settori riservati** Il campo *settori riservati* nel record di avvio multimediale definisce il numero di settori riservati tra il record di avvio e il primo settore dell'area FAT. Questa voce è zero nella maggior parte dei casi.
- **Numero di grassi** La voce relativa al *numero di grassi* nel record di avvio multimediale definisce il numero di grassi nei supporti. In un supporto deve essere sempre presente almeno un FAT. I grassi aggiuntivi sono semplicemente copie duplicate del database primario (primo) e vengono in genere utilizzate dal software di diagnostica o di ripristino.
- **Dimensioni directory radice** La voce della *dimensione della directory radice* nel record di avvio multimediale definisce il numero fisso di voci nella directory radice del supporto. Questo campo non è applicabile alle sottodirectory e alla directory radice FAT-32 perché sono entrambe allocate dai cluster dei supporti.
- **Numero di settori FAT-12 & FAT-16** Il campo *numero di settori* nel record di avvio multimediale contiene il numero totale di settori nel supporto. Se questo campo è pari a zero, il numero totale di settori è contenuto nel campo *numero di settori FAT-32* che si trova in un secondo momento nel record di avvio.
- **Tipo di supporto** Il campo *Media Type* viene usato per identificare il tipo di supporto presente nel driver di dispositivo. Si tratta di un campo legacy.
- **Settori per FAT** I *settori per ogni Fat* archiviato nel record di avvio multimediale contengono il numero di settori associati a ogni Fat nell'area FAT. Il numero di settori FAT deve essere sufficientemente grande da tenere conto del numero massimo possibile di cluster che possono essere allocati nei supporti.
- **Settori per traccia** Il campo *settori per traccia* nel record di avvio multimediale definisce il numero di settori per traccia. Questo è in genere pertinente solo per i supporti di tipo disco effettivi. I dispositivi FLASH non usano questo mapping.
- **Numero di intestazioni** Il campo *numero di intestazioni* nel record di avvio multimediale definisce il numero di intestazioni nei supporti. Questo è in genere pertinente solo per i supporti di tipo disco effettivi. I dispositivi FLASH non usano questo mapping.
- **Settori nascosti** Il campo *settori nascosti* nel record di avvio multimediale definisce il numero di settori prima del record di avvio. Questo campo viene mantenuto nel blocco di controllo **FX_MEDIA** e deve essere considerato in FILEX i/O Drivers in tutte le richieste di lettura e scrittura effettuate da FILEX.
- **Numero di settori FAT-32** Il campo *numero di settori* nel record di avvio multimediale è valido solo se il campo *numero di settori* a due byte è pari a zero. In tal caso, questo campo a quattro byte contiene il numero di settori nel supporto.
- **Settori per grasso (FAT-32)** Il campo *settori per grasso (FAT-32)* è valido solo nel formato fat-32 e contiene il numero di settori allocati per ogni FAT del supporto.
- **Cluster di directory radice** Il campo *cluster directory radice* è valido solo nel formato FAT-32 e contiene il numero di cluster iniziale della directory radice.
- **Codice di avvio del sistema** Il campo del *codice di avvio del sistema* è un'area in cui archiviare una piccola parte del codice di avvio. Attualmente, nella maggior parte dei dispositivi, si tratta di un campo legacy.
- **0X55AA firma** Il campo della *firma* è un modello di dati usato per identificare il record di avvio. Se questo campo non è presente, il record di avvio non è valido.

### <a name="exfat"></a>exFAT

Le dimensioni massime del file in FAT32 sono 4GB, che limitano l'adozione ampia di file multimediali ad alta definizione. Per impostazione predefinita, FAT32 supporta supporti di archiviazione fino a 32 GB. Con un aumento della capacità di memoria flash e SD, FAT32 diventa meno efficiente nella gestione di volumi di grandi dimensioni. exFAT è progettato per superare queste limitazioni. exFAT supporta le dimensioni dei file fino a un exabyte (EB), che è approssimativamente di 1 miliardo GB. Un'altra differenza significativa tra exFAT e FAT32 è che exFAT USA bitmap per gestire lo spazio disponibile nel volume, rendendo exFAT più efficiente per trovare lo spazio disponibile durante la scrittura dei dati nel file. Per i file archiviati in cluster contigui, exFAT Elimina la discesa della catena FAT per trovare tutti i cluster, rendendola più efficiente quando si accede a file di grandi dimensioni. exFAT è necessario per l'archiviazione flash e le schede SD maggiori di 32 GB.

### <a name="exfat-logical-sectors"></a>Settori logici exFAT

Il layout generale dei settori logici del supporto in exFAT è illustrato nella figura 2. In exFAT il blocco di avvio e l'area FAT appartengono all'area del sistema. Il resto dei cluster è area utente. Sebbene non sia obbligatorio, exFAT standard suggerisce che la bitmap di allocazione si trovi all'inizio dell'area utente, seguita dalla tabella del case e dalla directory radice.

### <a name="exfat-media-boot-record"></a>Record di avvio multimediale exFAT

Il contenuto del record di avvio multimediale in exFAT è diverso da quello di FAT12/16/32. Sono elencate nella tabella 2. Per evitare confusione, l'area tra 0x0B e 0x40, che contiene vari parametri multimediali in FAT12/16/32 è contrassegnata come *riservata* in exFAT. Questa area riservata deve essere programmata con zeri, evitando di interpretare erroneamente il record di avvio multimediale.

![Settori logici exFAT](./media/user-guide/exfat-logical-sectors.png)

**FIGURA 2. Settori logici exFAT**

- **Istruzione di salto** Il campo *Jump istruzione* è un campo a tre byte che rappresenta un'istruzione Intel x86 computer per un salto del processore. Si tratta di un campo Legacy nella maggior parte dei casi.

    **TABELLA 2. Record di avvio multimediale exFAT**

    |Offset  |Campo  |Numero di byte|
    |----------|-----------|------------|
    |0x00|Istruzione di salto|3|
    |0x03|Nome del file System|8|
    |0x0B|Riservato|53|
    |0x40|Offset partizione|8|
    |0x48|Lunghezza del volume|8|
    |0x50|Offset FAT|4|
    |0x54|Lunghezza FAT|4|
    |0x58|Offset heap cluster|4|
    |0x5C|Conteggio cluster|4|
    |0x60|Primo cluster di directory radice|4|
    |0x64|Numero di serie del volume|4|
    |0x68|Revisione del file System|2|
    |0x6A|Flag del volume|2|
    |0x6C|Byte per settore MAIUSC|1|
    |0x6D|Spostamento settore per cluster|1|
    |0x6E|Numero di grassi|1|
    |0x6F|Selezione unità|1|
    |0x70|Percentuale in uso|7|
    |0x71|Riservato|1|
    |0x78|Codice di avvio|390|
    |0x1FE|Firma di avvio|2|

- **Nome del file System** Per exFAT il campo *nome file System* deve essere "exFAT" seguito da tre spazi vuoti finali.
- **Riservato** Il contenuto del campo *riservato* deve essere zero. Questa area si sovrappone ai record di avvio in FAT12/16/32. Questa area zero evita che i file System vengano interpretati in modo errato da questo volume.
- **Offset partizione** Il campo *offset partizione* indica l'inizio di questa partizione.
- **Lunghezza del volume** Il campo *lunghezza del volume* definisce la dimensione, in numero di settori, di questa partizione.
- **Offset Fat** Il campo *offset Fat* definisce il numero di settore iniziale, relativo all'inizio di questa partizione, della tabella FAT per questa partizione.
- **Lunghezza Fat** Il campo *lunghezza Fat* definisce la dimensione della tabella FAT, in numero di settori.
- **Offset heap cluster** Il campo *offset heap cluster* definisce il numero di settore iniziale, relativo all'inizio della partizione, dell'heap del cluster. Heap del cluster è l'area in cui vengono archiviate le informazioni sulle directory e i dati del file.
- **Conteggio cluster** Il campo *conteggio cluster* definisce il numero di cluster di questa partizione.
- **Primo cluster di directory radice** Il *primo cluster del campo directory radice* definisce la posizione iniziale della directory radice, che è consigliabile subito dopo la bitmap di allocazione e la tabella del case.
- **Numero di serie del volume** Il campo numero di serie del *volume* definisce il numero di serie per la partizione.
- **Revisione del file System** Il campo *file System Revisione* definisce la versione principale e secondaria di exFAT.
- **Flag del volume** Il campo *flag del volume* contiene flag che indicano lo stato del volume.
- **Byte per settore MAIUSC** Il campo di *spostamento byte per settore* definisce il numero di byte per settore, in log2 (n), dove n è il numero di byte per settore. Ad esempio, nella scheda SD, le dimensioni del settore sono pari a 512 byte. Pertanto questo campo sarà 9 (log2 (512) = 9).
- **Settori per spostamento del cluster** Il campo *settori per spostamento cluster* definisce il numero di settori in un cluster, in log2 (n), dove n è il numero di settori per cluster.
- **Numero di grassi** Il campo *numero di grassi* definisce il numero di tabelle FAT in questa partizione. Per exFAT, è consigliabile usare il valore 1 per una tabella FAT.
- **Selezione unità** Il campo *Seleziona driver* definisce il numero di unità Int 13h esteso.
- **Percentuale in uso** Il campo percentuale *in uso consente* di definire la percentuale dei cluster nell'heap del cluster da allocare. I valori validi sono compresi tra 0 e 100, inclusi.
- **Riservato** Questo campo è riservato per un utilizzo futuro.
- **Codice di avvio** Il campo del *codice di avvio* è un'area in cui archiviare una piccola parte del codice di avvio. Attualmente, nella maggior parte dei dispositivi, si tratta di un campo legacy.
- **0X55AA firma** Il campo della *firma di avvio* è un modello di dati usato per identificare il record di avvio. Se questo campo non è presente, il record di avvio non è valido.

### <a name="file-allocation-table-fat"></a>Tabella di allocazione file (FAT)

La *tabella di allocazione file (FAT)* viene avviata dopo i settori riservati nel supporto. L'area FAT è essenzialmente una matrice di voci a 12 bit, a 16 bit o a 32 bit che determinano se il cluster è allocato o parte di una catena di cluster che comprende una sottodirectory o un file. La dimensione di ogni voce FAT è determinata dal numero di cluster che devono essere rappresentati. Se il numero di cluster (derivato dai settori totali divisi per i settori per cluster) è minore o uguale a 4.086, vengono usate voci FAT a 12 bit. Se il numero totale di cluster è maggiore di 4.086 e minore di 65.525, vengono utilizzate le voci FAT a 16 bit. In caso contrario, se il numero totale di cluster è maggiore o uguale a 65.525, vengono utilizzati FAT o exFAT a 32 bit.

Per FAT12/16/32, la tabella FAT non solo gestisce la catena del cluster, ma fornisce anche informazioni sull'allocazione del cluster: indipendentemente dal fatto che sia disponibile o meno un cluster. In exFAT, le informazioni sull'allocazione del cluster vengono gestite da una voce di directory bitmap di allocazione. Ogni partizione dispone di una propria bitmap di allocazione. La dimensione della bitmap è sufficientemente grande da coprire tutti i cluster disponibili. Se è disponibile un cluster per l'allocazione, il bit corrispondente nella bitmap di allocazione viene impostato su 0. In caso contrario, il bit viene impostato su 1. Per un file che occupa cluster consecutivi, exFAT non richiede una catena FAT per tenere traccia di tutti i cluster. Tuttavia, per un file che non occupa i cluster consecutivi, è ancora necessario mantenere una catena FAT.

### <a name="fat-entry-contents"></a>Contenuto voce FAT

Le prime due voci della tabella FAT non vengono utilizzate e in genere presentano il contenuto seguente.

|Voce FAT |FAT a 12 bit|FAT a 16 bit|FAT 32 bit| exFAT|
|----------|-----------|------------|-------|------|
|Voce 0|0x0F0|0x00F0|0x000000F0|0xF8FFFFFF|
|Voce 1|0xFFF|0xFFFF|0x0FFFFFFF|0xFFFFFFFF|

La voce FAT numero 2 rappresenta il primo cluster nell'area dati del supporto. Il contenuto di ogni voce del cluster determina se è gratuito o parte di un elenco collegato di cluster allocati per un file o una sottodirectory. Se la voce del cluster contiene un'altra voce del cluster valida, il cluster viene allocato e il relativo valore punta al cluster successivo allocato nella catena del cluster.

Le possibili voci del cluster sono definite come segue.
|Significato|FAT a 12 bit|FAT a 16 bit|FAT 32 bit| exFAT|
|----------|-----------|------------|-------|------|
|Cluster gratuito|0x000|0x0000|0x00000000|0x00000000|
|Non utilizzate|0x001|0x0001|0x00000001|0x00000001|
|Riservato|0xFF0-FF6|0xFFF0-FFF6|0x0FFFFFF0-6|Da ClusterCounter + 2 a 0xFFFFFFF6|
|Cluster non valido|0xFF7|0xFFF7|0x0FFFFFF7|0xFFFFFFF7|
|Riservato| - | - | - | 0xFFFFFFF8-E|
|Ultimo cluster| 0xFF8-FFF| 0xFFF8-FFFF| 0x0FFFFFF8-F| 0xFFFFFFFF|
|Collegamento del cluster| 0x002-0xFEF| 0x0002-FFEF| 0x2-0x0FFFFFEF | 0x2-Clustercount-+ 1|

L'ultimo cluster in una catena allocata di cluster contiene l'ultimo valore del cluster (definito in precedenza). Il primo numero di cluster si trova nella voce della directory di file o sottodirectory.

### <a name="internal-logical-cache"></a>Cache logica interna

FileX gestisce una cache del settore logico *utilizzata più di recente* per ogni supporto aperto. La dimensione massima della cache del settore logico è definita dalla costante **FX_MAX_SECTOR_CACHE** e si trova in **_fx_api. h_**. Si tratta del primo fattore che determina le dimensioni della cache interna del settore logico.

L'altro fattore che determina le dimensioni della cache del settore logico è la quantità di memoria fornita alla chiamata ***fx_media_open** _ da parte dell'applicazione. È necessario disporre di memoria sufficiente per almeno un settore logico. Se sono necessari più di _ *FX_MAX_SECTOR_CACHE** settori logici, è necessario modificare la costante in **_fx_api. h_** ed è necessario ricompilare l'intera libreria FILEX.

> [!IMPORTANT]
> *Ogni supporto aperto in FileX può avere dimensioni della cache diverse a seconda della memoria fornita durante la chiamata aperta.*

### <a name="write-protect"></a>Proteggi scrittura

FileX fornisce al driver dell'applicazione la possibilità di impostare dinamicamente la protezione delle scritture sui supporti. Se è richiesta la protezione in scrittura, il driver imposta su FX_TRUE campo *fx_media_driver_write_protect* nella struttura FX_MEDIA associata. Se impostato, tutti i tentativi eseguiti dall'applicazione per modificare i supporti vengono rifiutati e i tentativi di aprire i file per la scrittura. Il driver può inoltre disabilitare la protezione da scrittura deselezionando questo campo.

### <a name="free-sector-update"></a>Aggiornamento del settore gratuito

FileX fornisce un meccanismo per informare il driver dell'applicazione quando i settori non sono più in uso. Questa operazione è particolarmente utile per i gestori di memoria FLASH che gestiscono tutti i settori logici utilizzati da FileX.

Se è necessaria la notifica dei settori gratuiti, il driver dell'applicazione imposta su FX_TRUE il campo *fx_media_driver_free_sector_update* nella struttura FX_MEDIA associata. Questa assegnazione viene in genere eseguita durante l'inizializzazione del driver.

Impostando questo campo, FileX esegue una chiamata al driver **FX_DRIVER_RELEASE_SECTORS** che indica quando uno o più settori consecutivi diventano disponibili.

### <a name="media-control-block-fx_media"></a>FX_MEDIA blocco di controllo multimediale

Le caratteristiche di ogni supporto aperto in FileX sono contenute nel blocco di controllo multimediale. Questa struttura viene definita nel file ***fx_api. h***.

Il blocco di controllo multimediale può trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendolo al di fuori dell'ambito di qualsiasi funzione.

Per individuare il blocco di controllo in altre aree, è necessario prestare maggiore attenzione, come per tutta la memoria allocata in modo dinamico. Se un blocco di controllo viene allocato all'interno di una funzione C, la memoria associata è parte dello stack del thread chiamante.

> [!WARNING]
>*In generale, evitare di usare l'archiviazione locale per i blocchi di controllo perché, dopo la restituzione della funzione, viene rilasciato tutto lo spazio dello stack della variabile locale, indipendentemente dal fatto che sia ancora in uso.*

## <a name="fat121632-directory-description"></a>**Descrizione Directory FAT12/16/32**

FileX supporta entrambi i formati di nome 8,3 e Windows Long File Name (LFN). Oltre al nome, ogni voce di directory contiene gli attributi della voce, l'ora e la data dell'Ultima modifica, l'indice del cluster iniziale e la dimensione in byte della voce. La tabella 3 Mostra il contenuto e le dimensioni di una voce di directory FileX 8,3.

- **Nome directory**

    FileX supporta i nomi di file con dimensioni comprese tra 1 e 255 caratteri. I nomi di file di otto caratteri standard sono rappresentati in una singola voce di directory sul supporto. Vengono mantenuti giustificati nel campo nome directory e sono riempiti di spazio vuoto. Inoltre, i caratteri ASCII che includono il nome sono sempre in maiuscolo.

    I nomi di file lunghi (LFNs) sono rappresentati da voci di directory consecutive, in ordine inverso, seguite immediatamente da un nome di file standard 8,3. Il nome 8,3 creato contiene tutte le informazioni di directory significative associate al nome. La tabella 4 Mostra il contenuto delle voci di directory usate per conservare le informazioni sul nome file lungo e la tabella 5 Mostra un esempio di LFN di 39 caratteri che richiede un totale di quattro voci di directory.

> [!IMPORTANT]
> *La costante **FX_MAX_LONG_NAME_LEN**, definita in **fx_api. h**, contiene la lunghezza massima supportata da FILEX.*

- **Estensione nome file directory**

    Per i nomi di file 8,3 standard, FileX supporta anche l'estensione facoltativa del nome file della *directory* a tre caratteri. Analogamente al nome del file di otto caratteri, le estensioni del nome file vengono mantenuti giustificate nel campo di estensione del nome file della directory, spazio vuoto e sempre maiuscolo.

    **TABELLA 3. Voce della directory FileX 8,3**

    |Offset|Campo|Numero di byte|
    |------------|-----------|------------|
    |0x00|Nome voce di directory|8|
    |0x08|Estensione directory|3|
    |0x0B|Attributi|1|
    |0x0C|NT (introdotto dal formato del nome di file lungo ed è riservato per NT [always 0])|1|
    |0x0D|Tempo di creazione in millisecondi (introdotto dal formato del nome di file lungo e rappresenta il numero di millisecondi durante la creazione del file.)|1|
    |0x0E|Tempo in minuti creato &amp; (introdotto dal formato del nome di file lungo e rappresenta l'ora e il minuto in cui è stato creato il file)|2|
    |0x10|Data di creazione (introdotta dal formato del nome di file lungo e rappresenta la data di creazione del file.)|2|
    |0x12|Data dell'ultimo accesso (introdotta dal formato del nome di file lungo e rappresenta la data dell'ultimo accesso al file).|2|
    |0x14|Avvio del cluster (solo 16 bit superiori-32)|2|
    |0x16|Ora modifica|2|
    |0x18|Data ultima modifica|2|
    |0x1A|Avvio del cluster (inferiore a 16 bit FAT-32 o FAT-12 o FAT-16)|2|
    |0x1C|Dimensioni file|4|


- **Attributi di directory**

    La voce di campo dell' *attributo della directory* a un byte contiene una serie di bit che specificano varie proprietà della voce di directory. Le definizioni degli attributi di directory sono le seguenti:

    |Bit attributo|Significato|
    |------------|-----------|
    |0x01|La voce è di sola lettura.|
    |0x02|La voce è nascosta.|
    |0x04|La voce è una voce di sistema.|
    |0x08|Entry è un'etichetta di volume|
    |0x10|La voce è una directory.|
    |0x20|La voce è stata modificata.|

    Poiché tutti i bit di attributo si escludono a vicenda, è possibile che siano impostati più bit di attributo alla volta.

- **Ora directory**

    Il campo relativo all' *ora della directory* a due byte contiene le ore, i minuti e i secondi dell'Ultima modifica apportata alla voce di directory specificata. I bit da 15 a 11 contengono le ore, i bit 10, sebbene 5 contengano i minuti e i bit 4, sebbene 0 contengano i secondi. I secondi effettivi sono divisi per due prima di essere scritti in questo campo.

- **Data Directory**

    Il campo della *Data della directory* a due byte contiene l'anno (offset da 1980), il mese e il giorno dell'Ultima modifica apportata alla voce di directory specificata. I bit da 15 a 9 contengono l'offset dell'anno, i bit da 8 a 5 contengono l'offset del mese e i bit da 4 a 0 contengono il giorno.

- **Cluster di avvio directory**

    Questo campo occupa 2 byte per FAT-12 e FAT-16. Per FAT-32 questo campo occupa 4 byte. Questo campo contiene il primo numero di cluster allocato alla voce (sottodirectory o file).

    > [!NOTE]
    > * Si noti che FileX crea nuovi file senza un cluster iniziale (inizio campo cluster uguale a zero) per consentire agli utenti di allocare facoltativamente un numero contiguo di cluster per un file appena creato. *

- **Dimensioni del file di directory**

    Il campo *dimensioni file* di *directory* a quattro byte contiene il numero di byte nel file. Se la voce è effettivamente una sottodirectory, il campo dimensione è zero.

### <a name="long-file-name-directory"></a>Directory nome file lungo

- **Ordinale**

    Campo *ordinale* a un byte che specifica il numero della voce LFN. Poiché le voci LFN sono posizionate in ordine inverso, i valori ordinali delle voci di directory LFN che includono un singolo LFN diminuiscono di uno. Inoltre, il valore ordinale di LFN direttamente prima del nome del file 8,3 deve essere uno.

    **TABELLA 4. Voce directory nome file lungo**

    |Offset|Campo|Numero di byte|
    |------------|-----------|------------|
    0x00|Campo ordinale|1|
    0x01|Carattere Unicode 1|2|
    0x03|Carattere Unicode 2|2|
    0x05|Carattere Unicode 3|2|
    0x07|Carattere Unicode 4|2|
    0x09|Carattere Unicode 5|2|
    0x0B|Attributi LFN|1|
    0x0C|Tipo LFN (riservato sempre 0)|1|
    0x0D|Checksum LFN|1|
    0x0E|Carattere Unicode 6|2|
    0x10|Carattere Unicode 7|2|
    0x12|Carattere Unicode 8|2|
    0x14|Carattere Unicode 9|2|
    0x16|Carattere Unicode 10|2|
    0x18|Carattere Unicode 11|2|
    0x1A|Cluster LFN (non usato sempre 0)|2|
    0x1C|Carattere Unicode 12|2|
    0x1E|Carattere Unicode |13|2|

- **Carattere Unicode**

    I campi *carattere Unicode* a due byte sono progettati per supportare i caratteri di molti linguaggi diversi. I caratteri ASCII standard sono rappresentati con il carattere ASCII archiviato nel primo byte del carattere Unicode seguito da uno spazio.

- **Attributi LFN**

    Il campo *attributi LFN* a un byte contiene gli attributi che identificano la voce di directory come voce di directory LFN. Questa operazione viene eseguita con gli attributi di sola lettura, di sistema, nascosti e di volume impostati.

- **Tipo LFN**

    Il campo di *tipo LFN* a un byte è riservato ed è sempre 0.

- **Checksum LFN**

    Il campo di *checksum LFN* a un byte rappresenta un checksum dei 11 caratteri del nome file MSDOS 8,3 associato. Questo checksum viene archiviato in ogni voce LFN per garantire che la voce LFN corrisponda al nome file 8,3 appropriato.

- **Cluster LFN**

    Il campo del *cluster LFN* a due byte non è usato ed è sempre 0.

    **TABELLA 5. Voci di directory contenenti un LFN di 39 caratteri**

    |Voce|Significato|
    |------------|-----------|
    |1|Voce di directory LFN 3|
    |2|Voce di directory 2 LFN|
    |3|Voce di directory 1 di LFN|
    |4|8,3 voce di directory (ttttt ~ n. XX)|

### <a name="exfat-directory-description"></a>Descrizione Directory exFAT

exFAT file system archivia le voci di directory e il nome file in modo diverso. La voce di directory contiene gli attributi della voce, diversi timestamp in cui la voce è stata creata, modificata e accessibile. Altre informazioni, ad esempio le dimensioni del file e il cluster iniziale, vengono archiviate nella voce della directory dell'estensione del flusso che segue immediatamente la voce della directory primaria. exFAT supporta solo il formato del nome di file lungo (LFN). il file viene archiviato nella voce della directory del nome file immediatamente dopo la voce della directory dell'estensione di flusso, come illustrato nella tabella 2.

### <a name="exfat-file-directory-entry"></a>Voce directory file exFAT

Una descrizione della voce della directory di file exFAT e del relativo contenuto è inclusa nella tabella e nei paragrafi seguenti.

- **Tipo voce**

    Il campo tipo di voce indica il tipo di questa voce. Per la voce della directory di file, questo campo deve essere 0x85.

- **Conteggio voci secondarie**

    Il campo *conteggio voci secondarie* indica il numero di voci secondarie che segue immediatamente questa voce primaria. Le voci secondarie associate alla voce della directory di file includono una voce di directory dell'estensione del flusso e una o più voci di directory del nome file.

    **TABELLA 6. Voce directory file exFAT**

    |Offset|Campo|Numero di byte|
    |----|-----------|-|
    |0x00|Tipo voce|1|
    |0x01|Voce secondaria|1|
    |0x02|Checksum|2|
    |0x04|Attributi file|2|
    |0x06|Riservato 1|2|
    |0x08|Timestamp creazione|4|
    |0x0C|Timestamp Ultima modifica|4|
    |0x10|Timestamp ultimo accesso|4|
    |0x14|Crea incremento 10 ms|1|
    |0x15|Incremento 10 ms Ultima modifica|1|
    |0x16|Crea offset UTC|1|
    |0x17|Offset UTC Ultima modifica|1|
    |0x18|Offset UTC ultimo accesso|1|
    |0x19|Riservato 2|7|

- **Checksum**

    Il campo *checksum* contiene il valore del checksum su tutte le voci nel set di voci di directory (la voce della directory di file e le relative voci secondarie).

- **Attributi file**

    La voce di campo attributi a un byte contiene una serie di bit che specificano varie proprietà della voce di directory. La definizione della maggior parte degli attributi BITS è identica alla 12/16/32 FAT. Le definizioni degli attributi di directory sono le seguenti:

    |Bit attributo|Significato|
    |------------|-----------|
    |0x01| La voce è di sola lettura|
    |0x02|Voce nascosta|
    |0x04|La voce è una voce di sistema|
    |0x08|La voce è riservata|
    |0x10|La voce è una directory|
    |0x20|La voce è stata modificata|
    |Tutti gli altri bit|Riservato|

- **Reserved1**

    Questo campo deve essere zero.

- **Timestamp creazione**

    Il campo *Crea timestamp* , combinando le informazioni dal campo *create 10 ms Increment* , descrive la data e l'ora locali in cui è stato creato il file o la directory.

- **Timestamp Ultima modifica**

    *Ultimo campo timestamp modificato* , combinando le informazioni dal campo dell'ultimo *incremento 10 ms modificato* , descrivere la data e l'ora dell'Ultima modifica apportata al file o alla directory. Vedere le note sotto sui timestamp.

- **Timestamp ultimo accesso**

    Il campo *timestamp ultimo accesso* descrive la data e l'ora dell'ultimo accesso al file o alla directory. Vedere le note sotto sui timestamp.

- **Crea incremento 10 ms**

    Il campo *create 10 ms Increment* , combinando le informazioni dal campo *create timestamp* , descrive la data e l'ora locali in cui è stato creato il file o la directory. Vedere le note sotto sui timestamp.

- **Incremento 10 ms Ultima modifica**

    Ultimo campo di *incremento 10 ms modificato* , che combina le informazioni dal campo *timestamp dell'Ultima modifica* , descrive la data e l'ora dell'Ultima modifica del file o della directory. Vedere le note sotto sui timestamp.

- **Crea offset UTC**

    Il campo *crea offset UTC* descrive la differenza tra l'ora locale e l'ora UTC, al momento della creazione del file o della directory. Vedere le note sotto sui timestamp.

- **Offset UTC Ultima modifica**

    Il campo *Last offset UTC modificato* descrive la differenza tra l'ora locale e l'ora UTC, al momento dell'Ultima modifica del file o della directory. Vedere le note sotto sui timestamp.

- **Offset UTC ultimo accesso**

    Il campo *offset UTC ultimo accesso* descrive la differenza tra l'ora locale e l'ora UTC, quando è stato eseguito l'ultimo accesso al file o alla directory. Vedere le note sotto sui timestamp.

- **Reserved2**

    Questo campo deve essere zero.

### <a name="notes-on-timestamps"></a>Note sui timestamp

- **Voce timestamp** I campi timestamp vengono interpretati nel modo seguente:

- **campi di incremento 10 ms** Il valore nel campo incremento 10 MS fornisce una maggiore granularità al valore timestamp. I valori validi sono compresi tra 0 (0ms) e 199 (1990ms).

     ![Campi di incremento 10 ms](./media/user-guide/10ms-increment-fields.png)

- **Campo offset UTC**

     ![Campo offset UTC](./media/user-guide/utc-offset-field.png)

- **Valore di scostamento**

    l'intero con segno a 7 bit rappresenta l'offset rispetto all'ora UTC, con incrementi di 15 minuti.

- **Valido**

    Indica se il valore nel campo offset è valido. 0 indica che il valore nel campo del valore di offset non è valido. 1 indica che il valore è valido.

### <a name="stream-extension-directory-entry"></a>Voce di directory dell'estensione di flusso

La tabella seguente include una descrizione della voce di directory dell'estensione del flusso e del relativo contenuto.

**TABELLA 7. Voce di directory dell'estensione di flusso**

|Offset|Campo| Numero di byte|
|------------|-----------|-------|
|0x00|Tipo voce|1|
|0x01|Flags|1|
|0x02|Riservato 1|1|
|0x03|Lunghezza del nome|1|
|0x04|Hash del nome|2|
|0x06|Riservato 2|2|
|0x08|Lunghezza dati valida|8|
|0x10|Riservato 3|4|
|0x14|Primo cluster|4|
|0x18|Lunghezza dei dati|8|

- **Tipo voce**

    Il campo *tipo di voce* indica il tipo di questa voce. Per la voce della directory dell'estensione di flusso, questo campo deve essere 0xC0.

- **Flag**

    Questo campo contiene una serie di bit che specificano varie proprietà:
    |Bit del flag|Significato    |
    |-----------------|-----------|
    |0x01            |Questo campo indica se l'allocazione dei cluster è possibile o meno. Questo campo deve essere 1.|
    |0x02            |Questo campo indica se i cluster associati sono o meno contigui. Un valore 0 indica che la voce FAT è valida e che FileX deve seguire la catena FAT. Il valore 1 indica che la voce FAT non è valida e i cluster sono contigui.|
    |Tutti gli altri bit    |Riservato.|

- **Riservato 1**

    Questo campo deve essere 0.

- **Lunghezza del nome**

    Il campo *lunghezza nome* contiene la lunghezza della stringa Unicode nelle voci di directory del nome file che contengono collettivamente. Le voci di directory del nome file seguono immediatamente questa voce di directory dell'estensione del flusso.

- **Hash del nome**

    Il campo *hash del nome* è una voce a 2 byte, che contiene il valore hash del nome del file con maiuscole/minuscole. Il valore hash consente la ricerca più veloce dei nomi di file/directory: se i valori hash non corrispondono, il nome file associato a questa voce non corrisponde.

- **Riservato 2**

    Questo campo deve essere 0.

- **Lunghezza dati valida**

    Il campo *lunghezza dati valido* indica la quantità di dati validi nel file.

- **Riservato 3**

    Il file archiviato dovrebbe essere 0.

- **Primo cluster**

    Il *primo campo cluster* contiene l'indice del primo cluster del flusso di dati.

- **Lunghezza dei dati**

    Il campo *lunghezza dati* contiene il numero totale di byte nei cluster allocati. Questo valore può essere maggiore della *lunghezza dei dati valida*, perché exFAT consente la preallocazione dei cluster di dati.

### <a name="root-directory"></a>Directory radice

Nei formati FAT 12 e 16 bit la *directory radice* si trova immediatamente dopo tutti i settori FAT del supporto e può essere individuata esaminando la ***fx_media_root_sector_start** _ in un blocco di controllo opened *FX_MEDIA**. La dimensione della directory radice, in termini di numero di voci di directory (ogni 32 byte), è determinata dalla voce corrispondente nel record di avvio del supporto.

La directory radice in FAT-32 e exFAT può trovarsi in qualsiasi punto dei cluster disponibili. La posizione e le dimensioni vengono determinate dal record di avvio quando viene aperto il supporto. Dopo l'apertura del supporto, è possibile usare il campo ***fx_media_root_sector_start*** per trovare il cluster iniziale della directory radice FAT-32 o exFAT.

### <a name="subdirectories"></a>Sottodirectory

Un sistema FAT è costituito da un numero qualsiasi di sottodirectory. Il nome della sottodirectory si trova in una voce di directory come un nome di file. Tuttavia, la specifica dell'attributo di directory (0x10) è impostata per indicare che la voce è una sottodirectory e le dimensioni del file sono sempre zero.
Nella figura 3 viene illustrata l'aspetto di una tipica struttura di sottodirectory per una nuova sottodirectory singlecluster denominata ***Sample. DIR** _ con un file denominato _ *_FILE.TXT_* *.
Nella maggior parte dei casi, le sottodirectory sono molto simili alle voci di file. Il primo campo del cluster punta al primo cluster di un elenco collegato di cluster. Quando viene creata una sottodirectory, le prime due voci di directory contengono le directory predefinite, ovvero la directory "." e la directory "..". La directory "." fa riferimento alla sottodirectory stessa, mentre la directory ".." punta alla directory precedente o padre.

### <a name="global-default-path"></a>Percorso predefinito globale

FileX fornisce un percorso predefinito globale per il supporto. Il percorso predefinito viene usato in qualsiasi file o servizio directory che non specifichi in modo esplicito un percorso completo.

Inizialmente, la directory predefinita globale è impostata sulla directory radice del supporto. Questo può essere modificato dall'applicazione chiamando ***fx_directory_default_set***.

Il percorso predefinito corrente per il supporto può essere esaminato chiamando ***fx_directory_default_get** _. Questa routine fornisce un puntatore di stringa alla stringa di percorso predefinita mantenuta all'interno del blocco di controllo _ *FX_MEDIA**.

### <a name="local-default-path"></a>Percorso predefinito locale

FileX fornisce anche un percorso predefinito specifico del thread che consente a thread diversi di avere percorsi univoci senza conflitti. La struttura **FX_LOCAL_PATH** viene fornita dall'applicazione durante le chiamate a **_fx_directory_local_path_set_*_ e _*_fx_directory_local_path_restore_** per modificare il percorso locale per il thread chiamante.

Se è presente un percorso locale, il percorso locale ha la precedenza sul percorso del supporto predefinito globale. Se il percorso locale non è configurato o viene cancellato con il servizio ***fx_directory_local_path_clear*** , il percorso predefinito globale del supporto viene usato ancora una volta.

## <a name="file-description"></a>Descrizione file

FileX supporta il carattere 8,3 standard e i nomi di file lunghi con estensioni di tre caratteri. Oltre al nome ASCII, ogni voce di file contiene gli attributi della voce, l'ora e la data dell'Ultima modifica, l'indice del cluster iniziale e la dimensione in byte della voce.

### <a name="file-allocation"></a>Allocazione file

FileX supporta lo schema di allocazione cluster standard del formato FAT. Inoltre, FileX supporta l'allocazione pre-cluster di cluster contigui. Per risolvere questo problema, ogni file FileX viene creato senza cluster allocati. I cluster vengono allocati nelle richieste di scrittura successive o in ***fx_file_allocate*** richieste di pre-allocare i cluster contigui.

Nella figura 4, "esempio di file FAT-16 FileX", viene visualizzato un file denominato ***FILE.TXT*** con due cluster sequenziali allocati a partire dal cluster 101, una dimensione di 26 e l'alfabeto come dati nel primo cluster di dati del File numero 101.

### <a name="file-access"></a>Accesso ai file

Un file FileX può essere aperto più volte contemporaneamente per l'accesso in lettura. Tuttavia, un file può essere aperto solo una volta per la scrittura. Le informazioni usate per supportare l'accesso ai file sono contenute nel blocco di controllo file ***FX_FILE*** .

> [!NOTE]
> *Si noti che il driver multimediale può impostare in modo dinamico la protezione delle Scritture. In questo caso tutte le richieste di scrittura vengono rifiutate, nonché i tentativi di aprire un file per la scrittura.*

### <a name="file-layout-in-exfat"></a>Layout di file in exFAT

La progettazione di exFAT non richiede la conservazione della catena FAT per un file se i dati vengono archiviati in cluster contagiosi. Il bit *NoFATChain* nella voce della directory dell'estensione del flusso indica se utilizzare o meno la catena grassa durante la lettura dei dati dal file. Se *NoFATChain* è impostato, FILEX legge in sequenza dal cluster indicato nel primo campo del *cluster* nella voce della directory dell'estensione di flusso.

D'altra parte, se il *NoFATChain* è chiaro, FILEX seguirà la catena FAT per attraversare l'intero file, in modo analogo alla catena FAT in FAT12/16/32.

Nella figura 3 vengono illustrati due file di esempio, uno non richiede una catena FAT e l'altro richiede una catena FAT.

## <a name="system-information"></a>Informazioni di sistema

Le informazioni sul sistema FileX sono tenuti a tenere traccia delle istanze di supporti aperti e di mantenere la data e l'ora di sistema globali.

![File con cluster contigui rispetto al file che richiede un collegamento FAT](./media/user-guide/system-information.png)

**FIGURA 3. File con cluster contigui rispetto al file che richiede un collegamento FAT**

Per impostazione predefinita, la data e l'ora di sistema sono impostate sulla data dell'ultima versione di FileX. Per avere una data e un'ora di sistema accurate, l'applicazione deve chiamare ***fx_system_time_set** _ e _ *_fx_system_date_set_** durante l'inizializzazione.

### <a name="system-date"></a>Data di sistema

La data di sistema FileX viene mantenuta nella variabile ***_fx_system_date*** globale. I bit da 15 a 9 contengono l'offset dell'anno da 1980, i bit da 8 a 5 contengono l'offset del mese e i bit da 4 a 0 contengono il giorno. |

### <a name="system-time"></a>Ora di sistema

L'ora di sistema FileX viene mantenuta nella variabile ***_fx_system_time*** globale. I bit da 15 a 11 contengono le ore, i bit 10, sebbene 5 contengano i minuti e i bit 4, sebbene 0 contengano i secondi.

### <a name="periodic-time-update"></a>Aggiornamento periodico

Durante l'inizializzazione del sistema, FileX crea un timer dell'applicazione ThreadX per aggiornare periodicamente la data e l'ora di sistema. Frequenza con cui l'aggiornamento di data e ora di sistema è determinato da due costanti utilizzate dalla funzione ***_fx_system_initialize*** .

Le costanti **FX_UPDATE_RATE_IN_SECONDS** e **FX_UPDATE_RATE_IN_TICKS** rappresentano lo stesso periodo di tempo. La costante **FX_UPDATE_RATE_IN_TICKS** è il numero di cicli del timer threadX che rappresenta il numero di secondi specificato dalla costante **FX_UPDATE_RATE_IN_SECONDS**. La costante **FX_UPDATE_RATE_IN_SECONDS** specifica il numero di secondi tra ogni aggiornamento del tempo di filex. Il tempo di FileX interno viene pertanto incrementato a intervalli di **FX_UPDATE_RATE_IN_SECONDS**. Queste costanti possono essere fornite durante la compilazione di **_fx_system_initialize_*_ oppure lo sviluppatore può modificare i valori predefiniti trovati nel file _*_fx_port. h_** della versione FILEX.

Il timer FileX periodico viene usato solo per l'aggiornamento della data e dell'ora di sistema globale, usato esclusivamente per il timestamp del file. Se il timestamp non è necessario, è sufficiente definire **FX_NO_TIMER** durante la compilazione di **_fx_system_initialize. c_** per eliminare la creazione del timer periodico FILEX.

![Esempio di file FAT-16 FileX](./media/user-guide/fat-16-file-example.png)

**FIGURA 4. Esempio di file FAT-16 FileX**
