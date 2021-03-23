---
title: Capitolo 2-installazione e uso di Azure RTO FileX
description: Questo capitolo contiene un'introduzione ad Azure RTO FileX e una descrizione di condizioni di installazione, procedure e uso, incluse le seguenti
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6703b10d8e0895984bb92d74d5dff809dca1a7f8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821413"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-filex"></a>Capitolo 2-installazione e uso di Azure RTO FileX

Questo capitolo contiene un'introduzione ad Azure RTO FileX e una descrizione delle condizioni di installazione, delle procedure e dell'uso. 

## <a name="host-considerations"></a>Considerazioni sull'host

### <a name="computer-type"></a>Tipo computer

Lo sviluppo incorporato viene in genere eseguito nei computer host Windows o Linux (Unix). Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.

### <a name="download-interfaces"></a>Interfacce di download

Il download di destinazione viene in genere eseguito dal debugger dello strumento di sviluppo. Dopo il download, il debugger è responsabile di fornire il controllo di esecuzione di destinazione (go, Halt, breakpoint e così via), nonché di accedere ai registri della memoria e del processore.

### <a name="debugging-tools"></a>Strumenti di debug

La maggior parte dei debugger dello strumento di sviluppo comunica con l'hardware di destinazione tramite connessioni di debug (OCD) on-chip come JTAG (IEEE 1149,1) e la modalità di debug in background (BDM). I debugger comunicano anche con l'hardware di destinazione tramite connessioni di In-Circuit emulazione (ICE). Le connessioni OCD e ICE forniscono soluzioni affidabili con intrusione minima sul software residente di destinazione.

### <a name="required-hard-disk-space"></a>Spazio su disco rigido richiesto

Il codice sorgente per FileX viene fornito in formato ASCII e richiede circa 500 KB di spazio sul disco rigido del computer host

## <a name="target-considerations"></a>Considerazioni sulla destinazione

FileX richiede tra 6 Kbyte e 30 Kbyte di memoria Read-Only (ROM) nella destinazione. Per le strutture di dati globali FileX sono necessari altri 100 byte della memoria ad accesso casuale (RAM) della destinazione. Ogni supporto aperto richiede anche 1,5 Kbyte di RAM per il blocco di controllo oltre alla RAM per l'archiviazione dei dati per un settore (in genere 512 byte).

Per il corretto funzionamento del timestamp di data/ora, FileX si basa sulle funzionalità del timer di ThreadX. Questa operazione viene implementata creando un timer specifico di FileX durante l'inizializzazione di FileX. FileX si basa anche su semafori ThreadX per la protezione di più thread e la sospensione di I/O.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTO FileX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/filex/> .

Di seguito è riportato un elenco di diversi file importanti nel repository:

- ***fx_api. h*** : questo file di intestazione C contiene tutti gli equivalenti di sistema, le strutture di dati e i prototipi di servizio.
- ***fx_port. h*** : questo file di intestazione C contiene tutte le definizioni e le strutture dei dati specifici dello strumento di sviluppo.
- ***demo_filex. c*** : questo file c contiene una piccola applicazione demo.
- ***FX. a (o FX. lib)*** : questa è la versione binaria della libreria FILEX C. Viene distribuito con il pacchetto standard.

> [!IMPORTANT]
> *Tutti i nomi di file sono in lettere minuscole. Questa convenzione di denominazione rende più semplice convertire i comandi in piattaforme di sviluppo Linux (Unix).*

## <a name="filex-installation"></a>Installazione di FileX

FileX viene installato clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository FileX nel PC:

```c
    git clone https://github.com/azure-rtos/filex
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante Download nella pagina principale di GitHub.

Sono inoltre disponibili istruzioni per la compilazione della libreria FileX nella pagina iniziale del repository online.

> [!IMPORTANT]
> Il software applicativo deve accedere al file di libreria FileX (in genere ***FX. a** _ o _*_FX. lib_*_) _and i file di inclusione C **fx_api. h** e **fx_port. h**. Questa operazione può essere eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nell'area di sviluppo dell'applicazione.

## <a name="using-filex"></a>Uso di FileX

L'uso di FileX è facile. In pratica, il codice dell'applicazione deve includere ***fx_api. h** _ durante la compilazione e il collegamento con la libreria di runtime FILEX _*_FX. a_*_ (o _*_FX. lib_*_). Naturalmente, sono necessari anche i file ThreadX, vale a dire _*_tx_api. h_*_ e _*_TX. a_*_ (o _*_TX. lib_*_) _, *.

> [!IMPORTANT]
> Quando si usa FileX in modalità autonoma (è necessario definire **FX_STANDALONE_ENABLE** ), i file e le librerie threadX non sono necessari.

Supponendo che si stia già usando ThreadX, per compilare un'applicazione FileX sono necessari quattro passaggi:

1. Includere il file ***fx_api. h*** in tutti i file dell'applicazione che utilizzano i servizi o le strutture di dati FILEX.
1. Inizializzare il sistema FileX chiamando ***fx_system_initialize** _ dalla funzione _ *_tx_application_define_** o da un thread dell'applicazione.

    > [!IMPORTANT]
    > Quando si usa FileX in modalità autonoma, è necessario chiamare direttamente ***fx_system_initialize*** dal codice dell'applicazione.

1. Aggiungere una o più chiamate a ***fx_media_open*** per configurare il supporto FILEX. Questa chiamata deve essere eseguita dal contesto di un thread dell'applicazione.

    > [!IMPORTANT]
    > *Tenere presente che la chiamata **fx_media_open** richiede una quantità di RAM sufficiente per archiviare i dati per un settore.*

1. Compilare l'origine e il collegamento dell'applicazione con le librerie di runtime FileX e ThreadX, ***FX. a** _ (o _*_FX. lib_*_) e _*_TX. a_*_ (o _ *_TX. lib_* *). L'immagine risultante può essere scaricata nella destinazione ed eseguita.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta FileX viene fornita con un'applicazione dimostrativa. È sempre consigliabile che il sistema dimostrativo venga eseguito per primo, sia nell'hardware di destinazione che in un ambiente dimostrativo specifico.

Se il sistema dimostrativo non funziona, provare a eseguire le operazioni seguenti per restringere il problema:

1. Determinare la quantità della dimostrazione in esecuzione.
1. Aumentare le dimensioni dello stack (questo aspetto è più importante nel codice dell'applicazione effettivo rispetto a quello per la dimostrazione).
1. Verificare che sia disponibile una quantità di RAM sufficiente per le dimensioni del disco RAM predefinite 32KBytes. Il sistema di base funzionerà su una quantità di RAM molto inferiore; Tuttavia, quando si usa un disco RAM, si verificano problemi se la memoria è insufficiente.
1. Ignorare temporaneamente le modifiche recenti per verificare se il problema scompare o è stato modificato. Tali informazioni dovrebbero risultare utili per i tecnici del supporto tecnico Microsoft. Seguire le procedure descritte in "Customer Support Center" per inviare le informazioni raccolte dalle procedure per la risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Quando si compilano la libreria FileX e l'applicazione tramite FileX, sono disponibili diverse opzioni di configurazione. Le opzioni seguenti possono essere definite nell'origine dell'applicazione, nella riga di comando o nel file di inclusione ***fx_user. h*** .

> [!IMPORTANT]
> *Le opzioni definite in **fx_user. h** vengono applicate solo se l'applicazione e la libreria threadX sono compilate con **_FX_INCLUDE_USER_DEFINE_FILE_* _ defined._ quando si usa FILEX in modalità autonoma (*** è necessario definire FX_STANDALONE_ENABLE *), non sono necessarie le librerie e i file threadX.

Il seguente elenco descrive in dettaglio ogni opzione di configurazione:

|Definire|Significato|
|----------    |-----------|
|FX_MAX_LAST_NAME_LEN        |Questo valore definisce la lunghezza massima del nome file, che include il nome del percorso completo. Per impostazione predefinita, tale valore è 256.|
|FX_DONT_UPDATE_OPEN_FILES    |Definito, FileX non aggiorna i file già aperti.|
|FX_MEDIA_DISABLE_SEARCH_CACHE    |Definito, l'ottimizzazione della cache di ricerca file è disabilitata.|
|FX_MEDIA_DISABLE_SEARCH_CACHE    |Definito, l'ottimizzazione della cache di ricerca file è disabilitata.|
|FX_DISABLE_DIRECT_DATA_READ_CACHE_FILL |Definito, l'aggiornamento del settore di lettura diretta della cache è disabilitato.|
|FX_MEDIA_STATISTICS_DISABLE |Definito, la raccolta di statistiche multimediali è disabilitata.|
|FX_SINGLE_OPEN_LEGACY |Definita, è abilitata la logica di apertura singola legacy per lo stesso file.|
|FX_RENAME_PATH_INHERIT    |Definito, la ridenominazione eredita le informazioni sul percorso.|
|FX_DISABLE_ERROR_CHECKING    |Rimuove l'API di base per il controllo degli errori di FileX e produce prestazioni migliori (fino al 30%) e dimensioni del codice inferiori.|
|FX_MAX_LONG_NAME_LEN    |Specifica la dimensione massima del nome file per FileX. Il valore predefinito è 256, ma è possibile eseguirne l'override con una riga di comando definita. I valori validi sono compresi tra 13 e 256.|
|FX_MAX_SECTOR_CACHE|Specifica il numero massimo di settori logici che possono essere memorizzati nella cache da FileX. Il numero effettivo di settori che è possibile memorizzare nella cache è inferiore a questa costante e al numero di settori che è possibile inserire nella quantità di memoria fornita in fx_media_open. Il valore predefinito è 256. Tutti i valori devono essere una potenza di 2.|
|FX_FAT_MAP_SIZE    |Specifica il numero di settori che possono essere rappresentati nella mappa di aggiornamento FAT. Il valore predefinito è 256, ma è possibile eseguirne l'override con una riga di comando definita. I valori più grandi consentono di ridurre gli aggiornamenti non necessari dei settori FAT secondari.|
|FX_MAX_FAT_CACHE    |Specifica il numero di voci nella cache FAT interna. Il valore predefinito è 16, ma è possibile eseguirne l'override con una riga di comando definita. Tutti i valori devono essere una potenza di 2.|
|FX_FAULT_TOLERANT    |Quando viene definito, FileX passa immediatamente le richieste di scrittura di tutti i settori di sistema (avvio, FAT e settori di directory) al driver del supporto. Ciò può ridurre le prestazioni, ma consente di limitare il danneggiamento ai cluster persi. Si noti che l'abilitazione di questa funzionalità non abilita automaticamente il modulo a tolleranza di errore FileX, che è abilitato definendo|
|FX_FAULT_TOLERANT_DATA    |Quando viene definito, FileX passa immediatamente tutte le richieste di scrittura dei dati dei file al driver del supporto. Ciò può ridurre le prestazioni, ma consente di limitare i dati dei file persi. Si noti che l'abilitazione di questa funzionalità non abilita automaticamente il modulo a tolleranza di errore FileX, che viene abilitato definendo ***FX_ENABLE_FAULT_TOLERANT***|
|FX_NO_LOCAL_PATH|Rimuove la logica del percorso locale da FileX, ottenendo dimensioni del codice minori.|
|FX_NO_TIMER|Elimina la configurazione del timer ThreadX per aggiornare la data e l'ora di sistema FileX. Questa operazione comporta l'inserimento di data e ora predefinite in tutte le operazioni sui file.|
|FX_UPDATE_RATE_IN_SECONDS    |Specifica la frequenza di regolazione dell'ora di sistema in FileX. Per impostazione predefinita, il valore è 10, che specifica che l'ora di sistema FileX viene aggiornata ogni 10 secondi.|
|FX_ENABLE_EXFAT| Quando è definito, la logica per la gestione di exFAT file system è abilitata in FileX. Per impostazione predefinita, questo simbolo non è definito.| 
|FX_UPDATE_RATE_IN_TICKS| Specifica la stessa frequenza del ***FX_UPDATE_RATE_IN_SECONDS*** (vedere sopra), ad eccezione dei termini della frequenza del timer threadX sottostante. Il valore predefinito è 1000, che presuppone una frequenza del timer ThreadX 10 ms e un intervallo di 10 secondi.|
|FX_SINGLE_THREAD|Elimina la logica di protezione ThreadX dall'origine FileX. Deve essere usato se FileX viene usato solo da un thread o se FileX è usato senza ThreadX.|
|FX_DRIVER_USE_64BIT_LBA|Quando definito, Abilita gli indirizzi del settore a 64 bit utilizzati nel driver di I/O. Per impostazione predefinita, questa opzione non è definita.|
|FX_ENABLE_FAULT_TOLERANT| Quando definito, Abilita il modulo a tolleranza di errore FileX. L'abilitazione della tolleranza di errore definisce automaticamente il simbolo ***FX_FAULT_TOLERANT** _ e _ *_FX_FAULT_TOLERANT_DATA_* *. Per impostazione predefinita, questa opzione non è definita.|
|FX_FAULT_TOLERANT_BOOT_INDEX|Definisce l'offset dei byte nel settore di avvio in cui il cluster per il log a tolleranza di errore è. Per impostazione predefinita, questo valore è 116. Questo campo accetta 4 byte. Vengono scelti i byte da 116 a 119 perché sono contrassegnati come riservati dalla specifica FAT 12/16/32/exFAT.|
|FX_FAULT_TOLERANT_MINIMAL_CLUSTER|Questo simbolo è deprecato. Non è più usato dalla tolleranza di errore FileX.|
|FX_STANDALONE_ENABLE|Definito, Abilita l'uso di FileX in modalità autonoma (senza Azure RTO). Per impostazione predefinita, questo simbolo non è definito.|

> [!IMPORTANT]
> Quando **FX_STANDALONE_ENABLE** è definito, la logica del percorso locale e l'installazione del timer threadX sono disabilitati.

## <a name="filex-version-id"></a>ID versione FileX

La versione corrente di FileX è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione. Il programmatore può ottenere la versione di FileX dall'esame del file **fx_port. h** . Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software applicativo può ottenere la versione di FileX esaminando la stringa globale **_ _fx_version_id_**.
