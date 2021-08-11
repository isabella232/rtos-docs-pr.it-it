---
title: Capitolo 3 - Componenti funzionali di Azure RTOS FileX
description: Questo capitolo contiene una descrizione delle prestazioni elevate Azure RTOS fileX incorporato file system dal punto di vista funzionale
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: bb2e1d7f10d71ed01a040cea63e9e469855525d89dd6318f3147c61ed166ee4c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783035"
---
# <a name="chapter-3---functional-components-of-azure-rtos-filex"></a>Capitolo 3 - Componenti funzionali di Azure RTOS FileX

Questo capitolo contiene una descrizione delle prestazioni elevate Azure RTOS fileX incorporato file system dal punto di vista funzionale.

## <a name="media-description"></a>Descrizione supporto

FileX è un'estensione incorporata a file system prestazioni elevate conforme al formato FILE SYSTEM FAT. FileX visualizza il supporto fisico come matrice di settori logici. La modalità di mapping di questi settori al supporto fisico sottostante è determinata dal driver di I/O connesso al supporto FileX durante la ***fx_media_open*** chiamata.

### <a name="fat121632-logical-sectors"></a>Settori logici FAT12/16/32

L'organizzazione esatta dei settori logici dei supporti è determinata dal contenuto del record di avvio del supporto fisico. Il layout generale dei settori logici dei supporti è illustrato nella figura 1.

I settori logici FileX iniziano dal settore logico 1, che punta al primo settore riservato del supporto. I settori riservati sono facoltativi, ma quando sono in uso contengono in genere informazioni di sistema, ad esempio il codice di avvio.

### <a name="fat121632-media-boot-record"></a>Record di avvio del supporto FAT12/16/32

L'offset di settore esatto delle altre aree nella visualizzazione dei settori logici del supporto deriva dal contenuto del *record di avvio multimediale*. La posizione del record di avvio si trova in genere nel settore 0. Tuttavia, se i supporti hanno *settori* nascosti, l'offset per il settore di avvio deve essere conto di essi (si trovano immediatamente PRIMA del settore di avvio). La tabella 1 elenca i componenti dei record di avvio del supporto e i componenti sono descritti nei paragrafi.

- **Istruzione di salto** Il *campo dell'istruzione* di salto è un campo a tre byte che rappresenta un'istruzione del computer Intel x86 per un salto del processore. Si tratta di un campo legacy nella maggior parte delle situazioni.

  ![Visualizzazione settore logico filex multimediale](./media/user-guide/filex-media-logical-sector-view.png)

  **FIGURA 1. Visualizzazione settore logico filex multimediale**

- **Nome OEM** Il *campo Nome OEM* è riservato ai produttori per inserire il nome o il nome del dispositivo.
- **Byte per settore** Il *campo byte per* settore nel record di avvio del supporto definisce il numero di byte presenti in ogni settore, ovvero l'elemento fondamentale del supporto.
- **Settori per cluster** Il *campo settori per cluster* nel record di avvio dei supporti definisce il numero di settori assegnati a un cluster. Il cluster è l'elemento di allocazione fondamentale in un cluster compatibile con FAT file system. Tutte le informazioni sui file e le sottodirectory vengono allocate dai cluster disponibili del supporto, come determinato dalla tabella fat (File Allocation Table).

    **TABELLA 1. Record di avvio dei supporti FileX**
    
    |Offset  |Campo  |Numero di byte|
    |----------|-----------|------------|
    |0x00|Istruzione di salto (e9,xx,xx o eb,xx,90)|3|
    |0x03|Nome OEM|8|
    |0x0B|Byte per settore|2|
    |0x0d|Settori per cluster|1|
    |0x0E|Numero di settori riservati|2|
    |0x10|Numero di fat|1|
    |0x11|Dimensioni della directory radice|2|
    |0x13|Numero di settori FAT-12 &amp; FAT-16|2|
    |0x15|Tipo supporto|1|
    |0x16|Numero di settori per FAT|2|
    |0x18|Settori per traccia|2|
    |0x1A|Numero di teste|2|
    |0x1C|Numero di settori nascosti|4|
    |0x20|Number of Sectors - FAT-32|4|
    |0x24|Settori per FAT (FAT-32)|4|
    |0x2C|Cluster di directory radice|4|
    |0x3E|Codice di avvio del sistema|448
    |0x1FE|0x55AA|2|

- **Settori riservati** Il *campo dei settori* riservati nel record di avvio del supporto definisce il numero di settori riservati tra il record di avvio e il primo settore dell'area FAT. Questa voce è zero nella maggior parte dei casi.
- **Numero di fat** Il *numero di voci FAT* nel record di avvio del supporto definisce il numero di faT nel supporto. In un supporto deve essere sempre presente almeno un file FAT. I fat aggiuntivi sono semplicemente copie duplicate del fat primario (primo) e vengono in genere usati dal software di diagnostica o di ripristino.
- **Dimensioni directory radice** La *voce relativa alle dimensioni* della directory radice nel record di avvio del supporto definisce il numero fisso di voci nella directory radice del supporto. Questo campo non è applicabile alle sottodirectory e alla directory radice FAT-32 perché entrambi sono allocati dai cluster dei supporti.
- **Number of Sectors FAT-12 & FAT-16** Il *campo del numero di* settori nel record di avvio dei supporti contiene il numero totale di settori nel supporto. Se questo campo è zero, il numero totale di settori è contenuto nel campo numero di settori *FAT-32* che si trova in un secondo momento nel record di avvio.
- **Tipo di supporto** Il *campo tipo di* supporto viene usato per identificare il tipo di supporto presente nel driver di dispositivo. Si tratta di un campo legacy.
- **Settori per FAT** I *settori per FAT* contenuti nel record di avvio dei supporti contengono il numero di settori associati a ogni FAT nell'area FAT. Il numero di settori FAT deve essere sufficientemente grande da essere in grado di contenere il numero massimo possibile di cluster che possono essere allocati nei supporti.
- **Settori per traccia** Il *campo settori per traccia* nel record di avvio del supporto definisce il numero di settori per traccia. Ciò è in genere pertinente solo ai supporti effettivi di tipo disco. I dispositivi FLASH non usano questo mapping.
- **Numero di testine** Il *campo numero di testine* nel record di avvio multimediale definisce il numero di testine nel supporto. Questo è in genere pertinente solo ai supporti effettivi di tipo disco. I dispositivi FLASH non usano questo mapping.
- **Settori nascosti** Il *campo settori* nascosti nel record di avvio multimediale definisce il numero di settori prima del record di avvio. Questo campo viene mantenuto nel blocco **FX_MEDIA** controllo e deve essere preso in considerazione nei driver di I/O FileX in tutte le richieste di lettura e scrittura effettuate da FileX.
- **Numero di settori FAT-32** Il *campo del numero di* settori nel record di avvio multimediale è valido solo se il campo *numero* di settori a due byte è zero. In tal caso, questo campo a quattro byte contiene il numero di settori nei supporti.
- **Settori per FAT (FAT-32)** Il *campo settori per FAT (FAT-32)* è valido solo in formato FAT-32 e contiene il numero di settori allocati per ogni FAT del supporto.
- **Cluster di directory radice** Il *campo del cluster della directory* radice è valido solo in formato FAT-32 e contiene il numero di cluster iniziale della directory radice.
- **Codice di avvio del sistema** Il *campo del codice di* avvio del sistema è un'area in cui archiviare una piccola parte del codice di avvio. Nella maggior parte dei dispositivi attualmente si tratta di un campo legacy.
- **Firma 0x55AA** Il *campo della* firma è un modello di dati usato per identificare il record di avvio. Se questo campo non è presente, il record di avvio non è valido.

### <a name="exfat"></a>exFAT

La dimensione massima del file in FAT32 è di 4 GB, che limita l'ampia adozione di file multimediali ad alta definizione. Per impostazione predefinita, FAT32 supporta supporti di archiviazione fino a 32 GB. Con l'aumento della capacità flash e della scheda SD, FAT32 diventa meno efficiente nella gestione di volumi di grandi dimensioni. exFAT è progettato per superare queste limitazioni. exFAT supporta dimensioni di file fino a un exabyte (EB), ovvero circa un miliardo di GB. Un'altra differenza significativa tra exFAT e FAT32 è che exFAT usa la bitmap per gestire lo spazio disponibile nel volume, rendendo exFAT più efficiente nel trovare spazio disponibile durante la scrittura dei dati nel file. Per i file archiviati in cluster contigui, exFAT elimina il percorso lungo la catena FAT per trovare tutti i cluster, rendendolo più efficiente quando si accede a file di grandi dimensioni. ExFAT è necessario per l'archiviazione flash e le schede SD di dimensioni superiori a 32 GB.

### <a name="exfat-logical-sectors"></a>Settori logici exFAT

Il layout generale dei settori logici dei supporti in exFAT è illustrato nella figura 2. In exFAT il blocco di avvio e l'area FAT appartengono all'area di sistema. Il resto dei cluster è Area utente. Sebbene non sia obbligatorio, lo standard exFAT consiglia che la bitmap di allocazione si trova all'inizio dell'area utente, seguita dalla tabella up case e dalla directory radice.

### <a name="exfat-media-boot-record"></a>Record di avvio dei supporti exFAT

Il contenuto del record di avvio multimediale in exFAT è diverso da quello in FAT12/16/32. Sono elencati nella tabella 2. Per evitare confusione, l'area tra 0x0B e 0x40, che contiene vari parametri multimediali in FAT12/16/32 è contrassegnata come *Riservata* in exFAT. Questa area riservata deve essere programmata con zeri, evitando di interpretazione errata del record di avvio multimediale.

![Settori logici exFAT](./media/user-guide/exfat-logical-sectors.png)

**FIGURA 2. Settori logici exFAT**

- **Istruzione Jump** Il *campo dell'istruzione* jump è un campo a tre byte che rappresenta un'istruzione del computer Intel x86 per un salto del processore. Si tratta di un campo legacy nella maggior parte dei casi.

    **TABELLA 2. Record di avvio dei supporti exFAT**

    |Offset  |Campo  |Numero di byte|
    |----------|-----------|------------|
    |0x00|Istruzione Jump|3|
    |0x03|Nome file system|8|
    |0x0B|Riservato|53|
    |0x40|Offset partizione|8|
    |0x48|Lunghezza volume|8|
    |0x50|FAT Offset|4|
    |0x54|Lunghezza FAT|4|
    |0x58|Offset dell'heap del cluster|4|
    |0x5C|Conteggio cluster|4|
    |0x60|Primo cluster della directory radice|4|
    |0x64|Numero di serie del volume|4|
    |0x68|Revisione del file system|2|
    |0x6A|Flag di volume|2|
    |0x6C|Byte per spostamento di settore|1|
    |0x6D|Spostamento settore per cluster|1|
    |0x6E|Numero di domande frequenti|1|
    |0x6F|Selezione unità|1|
    |0x70|Percentuale in uso|7|
    |0x71|Riservato|1|
    |0x78|Codice di avvio|390|
    |0x1FE|Firma di avvio|2|

- **Nome file system** Per exFAT *il file system* nome deve essere "EXFAT" seguito da tre spazi vuoti finali.
- **Riservato** Il contenuto del *campo riservato* deve essere zero. Questa area si sovrappone ai record di avvio in FAT12/16/32. Rendendo questa area zero si evita che i file system interpretino in modo errato questo volume.
- **Offset partizione** Il *campo offset* partizione indica l'inizio di questa partizione.
- **Lunghezza volume** Il *campo volume length* (Lunghezza volume) definisce le dimensioni, in numero di settori, di questa partizione.
- **Offset FAT** Il *campo offset FAT* definisce il numero di settore iniziale, relativo all'inizio di questa partizione, della tabella FAT per questa partizione.
- **Lunghezza FAT** Il *campo lunghezza* FAT definisce le dimensioni della tabella FAT, in numero di settori.
- **Offset dell'heap del cluster** Il *campo dell'offset dell'heap* del cluster definisce il numero di settore iniziale, relativo all'inizio della partizione, dell'heap del cluster. L'heap del cluster è l'area in cui vengono archiviate le informazioni sulle directory e i dati del file.
- **Conteggio cluster** Il *campo cluster count* (Conteggio cluster) definisce il numero di cluster di questa partizione.
- **Primo cluster della directory radice** Il *primo cluster del* campo della directory radice definisce il percorso iniziale della directory radice, che è consigliabile usare subito dopo la bitmap di allocazione e la tabella up-case.
- **Numero di serie del volume** Il *campo numero di serie* del volume definisce il numero di serie per questa partizione.
- **Revisione del file system** Il *file system di revisione* definisce la versione principale e secondaria di exFAT.
- **Flag di volume** Il *campo flag del* volume contiene flag che indicano lo stato del volume.
- **Byte per spostamento di settore** Il *campo bytes per sector shift* definisce il numero di byte per settore, in log2(n), dove n è il numero di byte per settore. Ad esempio, nella scheda SD le dimensioni del settore sono di 512 byte. Questo campo deve quindi essere 9 (log2(512) = 9).
- **Spostamento settori per cluster** Il *campo settori per turno del cluster* definisce il numero di settori in un cluster, in log2(n) dove n è il numero di settori per cluster.
- **Numero di domande frequenti** Il *campo Number of FATs (Numero di* tabelle FAT) definisce il numero di tabelle FAT in questa partizione. Per exFAT, è consigliabile che il valore sia 1, per una tabella FAT.
- **Selezione unità** Il *campo di selezione* del driver definisce il numero di unità INT 13h esteso.
- **Percentuale in uso** Il *campo percentuale in* uso definisce la percentuale di allocazione dei cluster nell'heap del cluster. I valori validi sono compresi tra 0 e 100 inclusi.
- **Riservato** Questo campo è riservato per un uso futuro.
- **Codice di avvio** Il *campo del codice* di avvio è un'area in cui archiviare una piccola parte del codice di avvio. Nella maggior parte dei dispositivi attualmente si tratta di un campo legacy.
- **Firma 0x55AA** Il *campo della firma* di avvio è un modello di dati usato per identificare il record di avvio. Se questo campo non è presente, il record di avvio non è valido.

### <a name="file-allocation-table-fat"></a>Tabella di allocazione file (FAT)

La *tabella di allocazione file (FAT)* viene avviata dopo i settori riservati nei supporti. L'area FAT è fondamentalmente una matrice di voci a 12 bit, 16 o 32 bit che determinano se tale cluster è allocato o parte di una catena di cluster che comprende una sottodirectory o un file. Le dimensioni di ogni voce FAT sono determinate dal numero di cluster che devono essere rappresentati. Se il numero di cluster (derivati dai settori totali divisi per i settori per cluster) è minore o uguale a 4.086, vengono usate voci FAT a 12 bit. Se il numero totale di cluster è maggiore di 4.086 e minore di 65.525, vengono usate voci FAT a 16 bit. In caso contrario, se il numero totale di cluster è maggiore o uguale a 65.525, vengono usati FAT a 32 bit o exFAT.

Per FAT12/16/32, la tabella FAT non solo mantiene la catena di cluster, ma fornisce anche informazioni sull'allocazione del cluster: se un cluster è disponibile o meno. In exFAT, le informazioni sull'allocazione del cluster vengono gestite da una voce di directory bitmap di allocazione. Ogni partizione ha una propria bitmap di allocazione. Le dimensioni della bitmap sono sufficientemente grandi da coprire tutti i cluster disponibili. Se un cluster è disponibile per l'allocazione, il bit corrispondente nella bitmap di allocazione viene impostato su 0. In caso contrario, il bit è impostato su 1. Per un file che occupa cluster consecutivi, exFAT non richiede una catena FAT per tenere traccia di tutti i cluster. Tuttavia, per un file che non occupa cluster consecutivi, è comunque necessario mantenere una catena FAT.

### <a name="fat-entry-contents"></a>Contenuto delle voci FAT

Le prime due voci della tabella FAT non vengono usate e in genere includono il contenuto seguente.

|Voce FAT |FAT a 12 bit|FAT a 16 bit|FAT a 32 bit| exFAT|
|----------|-----------|------------|-------|------|
|Voce 0|0x0F0|0x00F0|0x000000F0|0xF8FFFFFF|
|Voce 1|0xFFF|0xFFFF|0x0FFFFFFF|0xffffffff|

Il numero di voce FAT 2 rappresenta il primo cluster nell'area dati del supporto. Il contenuto di ogni voce del cluster determina se è gratuita o parte di un elenco collegato di cluster allocati per un file o una sottodirectory. Se la voce del cluster contiene un'altra voce del cluster valida, il cluster viene allocato e il relativo valore punta al cluster successivo allocato nella catena di cluster.

Le possibili voci del cluster sono definite come indicato di seguito.

|Significato|FAT a 12 bit|FAT a 16 bit|FAT a 32 bit| exFAT|
|----------|-----------|------------|-------|------|
|Cluster gratuito|0x000|0x0000|0x00000000|0x00000000|
|Non utilizzate|0x001|0x0001|0x00000001|0x00000001|
|Riservato|0xFF0-FF6|0xFFF0-FFF6|0x0FFFFFF0-6|Da ClusterCounter +2 a 0xFFFFFFF6|
|Cluster non erto|0xFF7|0xFFF7|0x0FFFFFF7|0xFFFFFFF7|
|Riservato| - | - | - | 0xFFFFFFF8-E|
|Ultimo cluster| 0xFF8-FFF| 0xFFF8-FFFF| 0x0FFFFFF8-F| 0xffffffff|
|Collegamento al cluster| 0x002-0xFEF| 0x0002-FFEF| 0x2-0x0FFFFFEF | 0x2 - ClusterCount + 1|

L'ultimo cluster in una catena allocata di cluster contiene il valore Ultimo cluster (definito in precedenza). Il primo numero di cluster si trova nella voce di directory del file o della sottodirectory.

### <a name="internal-logical-cache"></a>Cache logica interna

FileX gestisce una cache *del settore logico usata* più di recente per ogni supporto aperto. La dimensione massima della cache del settore logico è definita dalla costante **FX_MAX_SECTOR_CACHE** e si trova in **_fx_api.h_**. Si tratta del primo fattore che determina le dimensioni della cache del settore logico interno.

L'altro fattore che determina le dimensioni della cache del settore logico è la quantità di memoria fornita alla chiamata *** fx_media_open** _dall'applicazione. La memoria deve essere sufficiente per almeno un settore logico. Se sono necessari più di _ *FX_MAX_SECTOR_CACHE** settori logici, la costante deve essere modificata in **_fx_api.h_** e deve essere ricompilata l'intera libreria FileX.

> [!IMPORTANT]
> *Ogni supporto aperto in FileX può avere dimensioni della cache diverse a seconda della memoria fornita durante la chiamata aperta.*

### <a name="write-protect"></a>Protezione da scrittura

FileX offre al driver dell'applicazione la possibilità di impostare dinamicamente la protezione da scrittura sul supporto. Se è necessaria la protezione da scrittura, il driver imposta FX_TRUE campo *fx_media_driver_write_protect* nella struttura FX_MEDIA associata. Se impostata, tutti i tentativi dell'applicazione di modificare i supporti vengono rifiutati e i tentativi di aprire i file per la scrittura. Il driver può anche disabilitare la protezione da scrittura deselezionando questo campo.

### <a name="free-sector-update"></a>Aggiornamento del settore gratuito

FileX fornisce un meccanismo per informare il driver dell'applicazione quando i settori non sono più in uso. Ciò è particolarmente utile per i gestori di memoria FLASH che gestiscono tutti i settori logici usati da FileX.

Se è necessaria la notifica dei settori liberi, il driver dell'applicazione imposta FX_TRUE campo *fx_media_driver_free_sector_update* campo nella struttura FX_MEDIA di lavoro associata. Questa assegnazione viene in genere eseguita durante l'inizializzazione del driver.

Se si imposta questo campo, FileX esegue FX_DRIVER_RELEASE_SECTORS **chiamata** del driver che indica quando uno o più settori consecutivi diventano gratuiti.

### <a name="media-control-block-fx_media"></a>Blocco di controllo multimediale FX_MEDIA

Le caratteristiche di ogni supporto aperto in FileX sono contenute nel blocco di controllo dei supporti. Questa struttura è definita nel file ***fx_api.h***.

Il blocco di controllo multimediale può trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione.

L'individuazione del blocco di controllo in altre aree richiede un po' più di attenzione, proprio come tutta la memoria allocata dinamicamente. Se un blocco di controllo viene allocato all'interno di una funzione C, la memoria associata fa parte dello stack del thread chiamante.

> [!WARNING]
>*In generale, evitare di usare l'archiviazione locale per i blocchi di controllo perché dopo la funzione viene restituito tutto lo spazio dello stack delle variabili locali, indipendentemente dal fatto che sia ancora in uso.*

## <a name="fat121632-directory-description"></a>**Descrizione della directory FAT12/16/32**

FileX supporta sia i formati di nome 8.3 che Windows LFN (Long File Name). Oltre al nome, ogni voce di directory contiene gli attributi della voce, l'ora e la data dell'ultima modifica, l'indice del cluster iniziale e le dimensioni in byte della voce. La tabella 3 mostra il contenuto e le dimensioni di una voce di directory FileX 8.3.

- **Nome directory**

    FileX supporta nomi di file di dimensioni comprese tra 1 e 255 caratteri. I nomi di file standard di otto caratteri sono rappresentati in una singola voce di directory nel supporto. Vengono lasciati giustificati nel campo del nome della directory e sono riempiti in spazi vuoti. Inoltre, i caratteri ASCII che costituiscono il nome vengono sempre in maiuscolo.

    I nomi di file lunghi (LFN) sono rappresentati da voci di directory consecutive, in ordine inverso, seguite immediatamente da un nome di file standard 8.3. Il nome 8.3 creato contiene tutte le informazioni significative sulla directory associate al nome. La tabella 4 mostra il contenuto delle voci di directory usate per contenere le informazioni sul nome file lungo e la tabella 5 mostra un esempio di LFN di 39 caratteri che richiede un totale di quattro voci di directory.

> [!IMPORTANT]
> *La costante **FX_MAX_LONG_NAME_LEN**, definita in **fx_api.h**, contiene la lunghezza massima supportata da FileX.*

- **Estensione del nome file della directory**

    Per i nomi di file standard 8.3, FileX supporta anche l'estensione facoltativa di tre caratteri del nome *file della directory*. Proprio come il nome del file di otto caratteri, le estensioni dei nomi di file vengono giustificate a sinistra nel campo dell'estensione del nome file della directory, riempite vuote e sempre in maiuscolo.

    **TABELLA 3. Voce di directory FileX 8.3**

    |Offset|Campo|Numero di byte|
    |------------|-----------|------------|
    |0x00|Nome voce directory|8|
    |0x08|Estensione directory|3|
    |0x0B|Attributi|1|
    |0x0C|NT (introdotto dal formato di nome file lungo ed è riservato per NT [sempre 0])|1|
    |0x0d|Ora creazione in millisecondi ( introdotta dal formato del nome file lungo e rappresenta il numero di millisecondi di creazione del file).|1|
    |0x0E|Ora creazione in ore minuti (introdotta dal formato di nome file lungo e rappresenta l'ora e il &amp; minuto in cui è stato creato il file)|2|
    |0x10|Data creazione (introdotta dal formato di nome file lungo e rappresenta la data di creazione del file).|2|
    |0x12|Data ultimo accesso (introdotta dal formato di nome file lungo e rappresenta la data dell'ultimo accesso al file).|2|
    |0x14|Avvio del cluster (solo FAT-32 a 16 bit superiore)|2|
    |0x16|Ora modifica|2|
    |0x18|Data ultima modifica|2|
    |0x1A|Cluster iniziale (16 bit inferiori FAT-32 o FAT-12 o FAT-16)|2|
    |0x1C|Dimensioni file|4|


- **Attributi di directory**

    La voce di campo *dell'attributo di directory* a un byte contiene una serie di bit che specificano varie proprietà della voce di directory. Le definizioni degli attributi della directory sono le seguenti:

    |Bit di attributo|Significato|
    |------------|-----------|
    |0x01|La voce è di sola lettura.|
    |0x02|La voce è nascosta.|
    |0x04|Entry è una voce di sistema.|
    |0x08|Entry è un'etichetta di volume|
    |0x10|La voce è una directory.|
    |0x20|La voce è stata modificata.|

    Poiché tutti i bit di attributo si escludono a vicenda, possono essere impostati più bit di attributo alla volta.

- **Tempo directory**

    Il campo *dell'ora della directory a due* byte contiene le ore, i minuti e i secondi dell'ultima modifica apportata alla voce di directory specificata. I bit da 15 a 11 contengono le ore, i bit da 10 a 5 contengono i minuti e i bit da 4 a 0 contengono i mezzo secondi. I secondi effettivi vengono divisi per due prima di essere scritti in questo campo.

- **Data directory**

    Il campo della *data della directory* a due byte contiene l'anno (offset dal 1980), il mese e il giorno dell'ultima modifica apportata alla voce di directory specificata. I bit da 15 a 9 contengono l'offset dell'anno, i bit da 8 a 5 contengono l'offset del mese e i bit da 4 a 0 contengono il giorno.

- **Cluster di avvio della directory**

    Questo campo occupa 2 byte per FAT-12 e FAT-16. Per FAT-32 questo campo occupa 4 byte. Questo campo contiene il primo numero di cluster allocato alla voce (sottodirectory o file).

    > [!NOTE]
    > *Si noti che FileX crea nuovi file senza un cluster iniziale (campo iniziale del cluster uguale a zero) per consentire agli utenti di allocare facoltativamente un numero contiguo di cluster per un file appena creato. *

- **Dimensioni file directory**

    Il campo delle dimensioni *del file di* *directory* a quattro byte contiene il numero di byte nel file. Se la voce è effettivamente una sottodirectory, il campo delle dimensioni è zero.

### <a name="long-file-name-directory"></a>Directory nome file lungo

- **Ordinale**

    Campo ordinale a *un* byte che specifica il numero della voce LFN. Poiché le voci LFN sono posizionate in ordine inverso, i valori ordinali delle voci di directory LFN che comprendono un singolo LFN diminuiscono di uno. Inoltre, il valore ordinale dell'LFN direttamente prima del nome file 8.3 deve essere uno.

    **TABELLA 4. Voce di directory nome file lungo**

    | Offset | Campo | Numero di byte |
    |------------|-----------|------------|
    | 0x00 | Campo ordinale | 1 |
    | 0x01 | Carattere Unicode 1 | 2 |
    | 0x03 | Carattere Unicode 2 | 2 |
    | 0x05 | Carattere Unicode 3 | 2 |
    | 0x07 | Carattere Unicode 4 | 2 |
    | 0x09 | Carattere Unicode 5 | 2 |
    | 0x0B | Attributi LFN | 1 |
    | 0x0C | Tipo LFN (riservato sempre 0) | 1 |
    | 0x0d | LFN Checksum | 1 |
    | 0x0E | Carattere Unicode 6 | 2 | 
    | 0x10 | Carattere Unicode 7 | 2 |
    | 0x12 | Carattere Unicode 8 | 2 |
    | 0x14 | Carattere Unicode 9 | 2 |
    | 0x16 | Carattere Unicode 10 | 2 |
    | 0x18 | Carattere Unicode 11 | 2 |
    | 0x1A | Cluster LFN (sempre inutilizzato 0) | 2 |
    | 0x1C | Carattere Unicode 12 | 2 |
    | 0x1E | Carattere Unicode 13 | 2 |

- **Carattere Unicode**

    I campi carattere Unicode a *due* byte sono progettati per supportare caratteri di molte lingue diverse. I caratteri ASCII standard sono rappresentati con il carattere ASCII archiviato nel primo byte del carattere Unicode seguito da uno spazio.

- **Attributi LFN**

    Il campo Attributi *LFN a* un byte contiene attributi che identificano la voce di directory come voce di directory LFN. Questa operazione viene eseguita impostando tutti gli attributi di sola lettura, di sistema, nascosti e del volume.

- **Tipo LFN**

    Il campo *Tipo LFN a* un byte è riservato ed è sempre 0.

- **LFN Checksum**

    Il campo *Checksum LFN* a un byte rappresenta un checksum degli 11 caratteri del nome file MSDOS 8.3 associato. Questo checksum viene archiviato in ogni voce LFN per garantire che la voce LFN corrisponda al nome file 8.3 appropriato.

- **LFN Cluster**

    Il campo cluster *LFN a due* byte non è usato e è sempre 0.

    **TABELLA 5. Voci di directory che comprendono un LFN di 39 caratteri**

    |Voce|Significato|
    |------------|-----------|
    |1|Voce di directory LFN 3|
    |2|Voce di directory LFN 2|
    |3|Voce di directory LFN 1|
    |4|8.3 Voce di directory (ttttt~n.xx)|

### <a name="exfat-directory-description"></a>Descrizione della directory exFAT

exFAT file system la voce di directory e il nome del file in modo diverso. La voce di directory contiene gli attributi della voce, vari timestamp relativi alla creazione, alla modifica e all'accesso della voce. Altre informazioni, ad esempio le dimensioni del file e il cluster iniziale, vengono archiviate nella voce della directory dell'estensione di flusso che segue immediatamente la voce di directory primaria. exFAT supporta solo il formato di nome LFN (Long File Name). che viene archiviato in File Name Directory Entry (Voce directory nome file) segue immediatamente la voce di directory dell'estensione di flusso, come illustrato nella tabella 2.

### <a name="exfat-file-directory-entry"></a>Voce della directory dei file exFAT

Una descrizione della voce della directory dei file exFAT e del relativo contenuto è inclusa nella tabella e nei paragrafi seguenti.

- **Tipo voce**

    Il campo tipo di voce indica il tipo di questa voce. Per Voce directory file, questo campo deve essere 0x85.

- **Conteggio voci secondarie**

    Il *campo secondary entry count* (Conteggio voci secondarie) indica il numero di voci secondarie immediatamente dopo questa voce primaria. Le voci secondarie associate alla voce della directory file includono una voce di directory dell'estensione di flusso e una o più voci di directory dei nomi file.

    **TABELLA 6. Voce della directory dei file exFAT**

    |Offset|Campo|Numero di byte|
    |----|-----------|-|
    |0x00|Tipo voce|1|
    |0x01|Voce secondaria|1|
    |0x02|Checksum|2|
    |0x04|Attributi file|2|
    |0x06|Riservato 1|2|
    |0x08|Timestamp creazione|4|
    |0x0C|Timestamp dell'ultima modifica|4|
    |0x10|Timestamp ultimo accesso|4|
    |0x14|Incremento di 10 ms|1|
    |0x15|Incremento dell'ultima modifica di 10 ms|1|
    |0x16|Creare un offset UTC|1|
    |0x17|Offset UTC ultima modifica|1|
    |0x18|Offset UTC ultimo accesso|1|
    |0x19|Riservato 2|7|

- **Checksum**

    Il *campo checksum* contiene il valore del checksum su tutte le voci nel set di voci di directory (la voce della directory file e le relative voci secondarie).

- **Attributi file**

    La voce di campo attributi a un byte contiene una serie di bit che specificano varie proprietà della voce di directory. La definizione della maggior parte dei bit di attributi è identica a FAT 16/12/32. Le definizioni degli attributi della directory sono le seguenti:

    |Bit di attributo|Significato|
    |------------|-----------|
    |0x01| La voce è di sola lettura|
    |0x02|La voce è nascosta|
    |0x04|La voce è una voce di sistema|
    |0x08|La voce è riservata|
    |0x10|La voce è una directory|
    |0x20|La voce è stata modificata|
    |Tutti gli altri bit|Riservato|

- **Reserved1**

    Questo campo deve essere zero.

- **Timestamp creazione**

    Il *campo crea timestamp,* combinando le informazioni del campo create *10ms Increment,* descrive la data e l'ora locali in cui è stato creato il file o la directory.

- **Timestamp dell'ultima modifica**

    Il *campo timestamp* dell'ultima modifica, che combina le informazioni del campo dell'incremento dell'ultima modifica di *10* ms, descrive la data e l'ora dell'ultima modifica del file o della directory. Vedere le note seguenti sui timestamp.

- **Timestamp ultimo accesso**

    Il *campo timestamp dell'ultimo* accesso descrive la data e l'ora dell'ultimo accesso al file o alla directory. Vedere le note seguenti sui timestamp.

- **Incremento di 10 ms**

    Il *campo create 10ms increment,* che combina le informazioni del campo *create timestamp,* descrive la data e l'ora locali in cui è stato creato il file o la directory. Vedere le note seguenti sui timestamp.

- **Incremento dell'ultima modifica di 10 ms**

    Il *campo dell'incremento* dell'ultima modifica  di 10 ms, che combina le informazioni del campo timestamp dell'ultima modifica, descrive la data e l'ora dell'ultima modifica del file o della directory. Vedere le note seguenti sui timestamp.

- **Creare un offset UTC**

    Il *campo create UTC offset (Crea offset UTC)* descrive la differenza tra l'ora locale e l'ora UTC, quando è stato creato il file o la directory. Vedere le note seguenti sui timestamp.

- **Offset UTC ultima modifica**

    *L'ultimo campo di offset UTC* modificato descrive la differenza tra l'ora locale e l'ora UTC, quando è stata modificata l'ultima modifica del file o della directory. Vedere le note seguenti sui timestamp.

- **Offset UTC ultimo accesso**

    Il *campo dell'ultimo offset UTC* a cui si è eseguito l'accesso descrive la differenza tra l'ora locale e l'ora UTC, quando è stato eseguito l'ultimo accesso al file o alla directory. Vedere le note seguenti sui timestamp.

- **Riservato2**

    Questo campo deve essere zero.

### <a name="notes-on-timestamps"></a>Note sui timestamp

- **Voce timestamp** I campi timestamp vengono interpretati come segue:

- **Campi di incremento di 10 ms** Il valore nel campo 10ms increment fornisce una granularità più fine al valore timestamp. I valori validi sono compresi tra 0 (0 ms) e 199 (1990 ms).

     ![Campi di incremento di 10 ms](./media/user-guide/10ms-increment-fields.png)

- **Campo offset UTC**

     ![Campo offset UTC](./media/user-guide/utc-offset-field.png)

- **Valore di scostamento**

    Intero con segno a 7 bit che rappresenta l'offset dall'ora UTC, in incrementi di 15 minuti.

- **Valido**

    Indica se il valore nel campo offset è valido o meno. 0 indica che il valore nel campo del valore di offset non è valido. 1 indica che il valore è valido.

### <a name="stream-extension-directory-entry"></a>Voce della directory dell'estensione di flusso

Nella tabella seguente è inclusa una descrizione della voce della directory dell'estensione di flusso e del relativo contenuto.

**TABELLA 7. Voce della directory dell'estensione di flusso**

|Offset|Campo| Numero di byte|
|------------|-----------|-------|
|0x00|Tipo voce|1|
|0x01|Flags|1|
|0x02|Riservato 1|1|
|0x03|Lunghezza del nome|1|
|0x04|Hash dei nomi|2|
|0x06|Riservato 2|2|
|0x08|Lunghezza dei dati valida|8|
|0x10|Riservato 3|4|
|0x14|Primo cluster|4|
|0x18|Lunghezza dei dati|8|

- **Tipo voce**

    Il *campo tipo* di voce indica il tipo di questa voce. Per l'estensione di streaming Directory Entry, questo campo deve essere 0xC0.

- **Flag**

    Questo campo contiene una serie di bit che specificano varie proprietà:
    
    |Flag Bit|Significato    |
    |-----------------|-----------|
    |0x01            |Questo campo indica se è possibile o meno l'allocazione dei cluster. Questo campo deve essere 1.|
    |0x02            |Questo campo indica se i cluster associati sono contigui. Il valore 0 indica che la voce FAT è valida e FileX deve seguire la catena FAT. Il valore 1 indica che la voce FAT non è valida e che i cluster sono contigui.|
    |Tutti gli altri bit    |Riservato.|

- **Riservato 1**

    Questo campo deve essere 0.

- **Lunghezza del nome**

    Il *campo name length* (Lunghezza nome) contiene la lunghezza della stringa Unicode contenuta collettivamente nelle voci della directory dei nomi file. Le voci della directory dei nomi di file seguono immediatamente questa voce di directory dell'estensione di flusso.

- **Hash dei nomi**

    Il *campo hash* del nome è una voce a 2 byte contenente il valore hash del nome di file con distinzione tra maiuscole e minuscole. Il valore hash consente una ricerca più rapida dei nomi di file/directory: se i valori hash non corrispondono, il nome file associato a questa voce non corrisponde.

- **Riservato 2**

    Questo campo deve essere 0.

- **Lunghezza dei dati valida**

    Il *campo valid data length* (Lunghezza dati valida) indica la quantità di dati validi nel file.

- **Riservato 3**

    Questo file deve essere 0.

- **Primo cluster**

    Il *primo campo del cluster* contiene l'indice del primo cluster del flusso di dati.

- **Lunghezza dei dati**

    Il *campo della* lunghezza dei dati contiene il numero totale di byte nei cluster allocati. Questo valore può essere maggiore di *Valid Data Length*, poiché exFAT consente la preallocazione dei cluster di dati.

### <a name="root-directory"></a>Directory radice

Nei formati FAT 12 e 16 bit, la *directory* radice si trova immediatamente dopo tutti i settori FAT nei supporti e può essere individuata esaminando ***fx_media_root_sector_start** _ in un blocco di controllo _ *FX_MEDIA** aperto. Le dimensioni della directory radice, in termini di numero di voci di directory (ogni 32 byte), sono determinate dalla voce corrispondente nel record di avvio del supporto.

La directory radice in FAT-32 ed exFAT può trovarsi in qualsiasi punto dei cluster disponibili. La posizione e le dimensioni sono determinate dal record di avvio all'apertura del supporto. Dopo l'apertura del supporto, ***il fx_media_root_sector_start*** può essere usato per trovare il cluster iniziale della directory radice FAT-32 o exFAT.

### <a name="subdirectories"></a>Sottodirectory

In un sistema FAT è presente un numero qualsiasi di sottodirectory. Il nome della sottodirectory risiede in una voce di directory esattamente come un nome di file. Tuttavia, la specifica dell'attributo di directory (0x10) è impostata per indicare che la voce è una sottodirectory e le dimensioni del file sono sempre pari a zero.
La figura 3 illustra l'aspetto di una tipica struttura di sottodirectory per una nuova sottodirectory singlecluster denominata ***SAMPLE. DIR** _ con un file denominato _*_FILE.TXT_**.
Nella maggior parte dei casi, le sottodirectory sono molto simili alle voci di file. Il primo campo del cluster punta al primo cluster di un elenco collegato di cluster. Quando viene creata una sottodirectory, le prime due voci di directory contengono le directory predefinite, in questo caso la directory "." e la directory "..". La directory "." punta alla sottodirectory stessa, mentre la directory ".." punta alla directory precedente o padre.

### <a name="global-default-path"></a>Percorso predefinito globale

FileX fornisce un percorso predefinito globale per il supporto. Il percorso predefinito viene usato in qualsiasi file o servizio directory che non specifica in modo esplicito un percorso completo.

Inizialmente, la directory predefinita globale è impostata sulla directory radice del supporto. Questa operazione può essere modificata dall'applicazione chiamando ***fx_directory_default_set***.

Il percorso predefinito corrente per il supporto può essere esaminato chiamando ***fx_directory_default_get** _. Questa routine fornisce un puntatore di stringa alla stringa di percorso predefinita gestita all'interno del blocco di controllo _ *FX_MEDIA**.

### <a name="local-default-path"></a>Percorso predefinito locale

FileX fornisce anche un percorso predefinito specifico del thread che consente a thread diversi di avere percorsi univoci senza conflitti. La **FX_LOCAL_PATH** viene fornita dall'applicazione durante le chiamate **_a fx_directory_local_path_set_ _ e *_*_fx_directory_local_path_restore_** per modificare il percorso locale per il thread chiamante.

Se è presente un percorso locale, il percorso locale ha la precedenza sul percorso multimediale predefinito globale. Se il percorso locale non è stato specificato o se viene cancellato con il ***servizio fx_directory_local_path_clear,*** il percorso predefinito globale del supporto viene usato di nuovo.

## <a name="file-description"></a>Descrizione file

FileX supporta nomi di file standard di 8.3 caratteri e lunghi con estensioni di tre caratteri. Oltre al nome ASCII, ogni voce di file contiene gli attributi della voce, l'ora e la data dell'ultima modifica, l'indice cluster iniziale e le dimensioni in byte della voce.

### <a name="file-allocation"></a>Allocazione di file

FileX supporta lo schema di allocazione cluster standard del formato FAT. FileX supporta anche l'allocazione pre-cluster di cluster contigui. A tale scopo, ogni file FileX viene creato senza cluster allocati. I cluster vengono allocati in richieste di scrittura successive ***o*** in fx_file_allocate per preallocare cluster contigui.

La figura 4, "FileX FAT-16 File Example", mostra un file denominatoFILE.TXTcon due cluster sequenziali allocati ***a*** partire dal cluster 101, una dimensione di 26 e l'alfabeto come dati nel primo cluster di dati del file numero 101.

### <a name="file-access"></a>Accesso ai file

Un file FileX può essere aperto più volte contemporaneamente per l'accesso in lettura. Tuttavia, un file può essere aperto una sola volta per la scrittura. Le informazioni utilizzate per supportare l'accesso ai file sono contenute nel ***blocco FX_FILE*** di controllo file.

> [!NOTE]
> *Si noti che il driver multimediale può impostare dinamicamente la protezione in scrittura. In questo caso, tutte le richieste di scrittura vengono rifiutate e i tentativi di aprire un file per la scrittura.*

### <a name="file-layout-in-exfat"></a>Layout dei file in exFAT

La progettazione di exFAT non richiede la manutenzione della catena FAT per un file se i dati vengono archiviati in cluster. Il bit *NoFATChain* nella voce della directory dell'estensione del flusso indica se la catena FAT deve essere usata o meno durante la lettura dei dati dal file. Se la *proprietà NoFATChain* è impostata, FileX legge in sequenza dal cluster indicato nel campo *First Cluster* (Primo cluster) nella voce della directory dell'estensione stream.

D'altra parte, se *NoFATChain* è chiaro, FileX seguirà la catena FAT per attraversare l'intero file, in modo simile alla catena FAT in FAT12/16/32.

La figura 3 mostra due file di esempio, uno non richiede una catena FAT e l'altro richiede una catena FAT.

## <a name="system-information"></a>Informazioni di sistema

Le informazioni sul sistema FileX consistono nel tenere traccia delle istanze dei supporti aperti e nel mantenere l'ora e la data di sistema globali.

![File con cluster contigui e file che richiedono il collegamento FAT](./media/user-guide/system-information.png)

**FIGURA 3. File con cluster contigui e file che richiedono il collegamento FAT**

Per impostazione predefinita, la data e l'ora di sistema sono impostate sulla data dell'ultima versione di FileX. Per avere una data e un'ora di sistema accurate, l'applicazione deve chiamare ***fx_system_time_set** _ e _ *_fx_system_date_set_** durante l'inizializzazione.

### <a name="system-date"></a>Data di sistema

La data del sistema FileX viene mantenuta nella variabile ***_fx_system_date*** globale. I bit da 15 a 9 contengono l'offset dell'anno dal 1980, i bit da 8 a 5 contengono l'offset del mese e i bit da 4 a 0 contengono il giorno. |

### <a name="system-time"></a>Ora di sistema

L'ora di sistema FileX viene mantenuta nella variabile ***_fx_system_time*** globale. I bit da 15 a 11 contengono le ore, i bit da 10 a 5 contengono i minuti e i bit da 4 a 0 contengono i mezzo secondi.

### <a name="periodic-time-update"></a>Aggiornamento periodico dell'ora

Durante l'inizializzazione del sistema, FileX crea un timer dell'applicazione ThreadX per aggiornare periodicamente la data e l'ora di sistema. Frequenza con cui la data e l'ora di sistema vengono aggiornate in base a due costanti utilizzate dalla ***_fx_system_initialize*** funzione .

Le costanti **FX_UPDATE_RATE_IN_SECONDS** e **FX_UPDATE_RATE_IN_TICKS** rappresentano lo stesso periodo di tempo. La costante **FX_UPDATE_RATE_IN_TICKS** è il numero di tick del timer ThreadX che rappresenta il numero di secondi specificato dalla costante **FX_UPDATE_RATE_IN_SECONDS**. La **FX_UPDATE_RATE_IN_SECONDS** costante specifica il numero di secondi tra ogni aggiornamento dell'ora FileX. Di conseguenza, il tempo FileX interno aumenta a intervalli **di FX_UPDATE_RATE_IN_SECONDS**. Queste costanti possono essere fornite durante la compilazione di fx_system_initialize _, oppure lo sviluppatore può modificare le impostazioni predefinite presenti nel file ***_*_fx_port.h_** della versione FileX.

Il timer FileX periodico viene usato solo per aggiornare la data e l'ora di sistema globale, che viene usata esclusivamente per il timestamp dei file. Se il timestamp non è necessario, è sufficiente definire FX_NO_TIMER durante la compilazione **_di fx_system_initialize.c_** per eliminare la creazione del timer periodico FileX. 

![Esempio di file FileX FAT-16](./media/user-guide/fat-16-file-example.png)

**FIGURA 4. Esempio di file FileX FAT-16**
