---
title: Capitolo 2 - Installazione e uso di Azure RTOS FileX
description: "Questo capitolo contiene un'introduzione Azure RTOS FileX e una descrizione delle condizioni di installazione, delle procedure e dell'uso, tra cui:"
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2f064fc65ef8445ea33590f23d5a040ed8b07c6c651ea4cf5c4aaef4b6c4fa7b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783850"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-filex"></a>Capitolo 2 - Installazione e uso di Azure RTOS FileX

Questo capitolo contiene un'introduzione Azure RTOS FileX e una descrizione delle condizioni di installazione, delle procedure e dell'uso. 

## <a name="host-considerations"></a>Considerazioni sull'host

### <a name="computer-type"></a>Tipo computer

Lo sviluppo incorporato viene in genere eseguito Windows computer host Linux (Unix). Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.

### <a name="download-interfaces"></a>Scaricare le interfacce

In genere il download di destinazione viene eseguito dall'interno del debugger dello strumento di sviluppo. Dopo il download, il debugger è responsabile del controllo dell'esecuzione di destinazione (go, halt, breakpoint e così via), nonché dell'accesso ai registri di memoria e del processore.

### <a name="debugging-tools"></a>Strumenti di debug

La maggior parte dei debugger degli strumenti di sviluppo comunica con l'hardware di destinazione tramite connessioni OCD (On-Chip Debug), ad esempio JTAG (IEEE 1149.1) e modalità di debug in background (BDM). I debugger comunicano anche con l'hardware di destinazione tramite In-Circuit di emulazione (ICE). Entrambe le connessioni OCD e ICE offrono soluzioni affidabili con intrusioni minime sul software residente di destinazione.

### <a name="required-hard-disk-space"></a>Spazio su disco rigido richiesto

Il codice sorgente per FileX viene fornito in formato ASCII e richiede circa 500 KByte di spazio sul disco rigido del computer host

## <a name="target-considerations"></a>Considerazioni sulla destinazione

FileX richiede da 6 kByte a 30 KByte di memoria Read-Only memoria (ROM) nella destinazione. Per le strutture di dati globali FileX sono necessari altri 100 byte della memoria ad accesso casuale (RAM) della destinazione. Ogni supporto aperto richiede anche 1,5 KByte di RAM per il blocco di controllo oltre alla RAM per l'archiviazione dei dati per un settore (in genere 512 byte).

Per il corretto funzionamento del timestamp di data/ora, FileX si basa sulle funzionalità del timer ThreadX. Questa operazione viene implementata creando un timer specifico di FileX durante l'inizializzazione di FileX. FileX si basa anche sui semafori ThreadX per la protezione di più thread e la sospensione di I/O.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS FileX può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/filex/> .

Di seguito è riportato un elenco di diversi file importanti nel repository:

- ***fx_api.h:*** questo file di intestazione C contiene tutti gli elementi di sistema, le strutture dei dati e i prototipi di servizio.
- ***fx_port.h:*** questo file di intestazione C contiene tutte le definizioni e le strutture di dati specifiche dello strumento di sviluppo.
- ***demo_filex.c:*** questo file C contiene una piccola applicazione demo.
- ***fx.a (o fx.lib):*** versione binaria della libreria FileX C. Viene distribuito con il pacchetto standard.

> [!IMPORTANT]
> *Tutti i nomi di file sono in lettere minuscole. Questa convenzione di denominazione semplifica la conversione dei comandi in piattaforme di sviluppo Linux (Unix).*

## <a name="filex-installation"></a>Installazione di FileX

FileX viene installato clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository FileX nel PC:

```c
    git clone https://github.com/azure-rtos/filex
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante di download nella GitHub principale.

Le istruzioni per la compilazione della libreria FileX sono disponibili anche nella prima pagina del repository online.

> [!IMPORTANT]
> Il software dell'applicazione deve accedere al file di libreria FileX (in genere denominato* in genere ***fx.a** _ o _*_fx.lib_*_ _and ) nei file di inclusione C **fx_api.h** e **fx_port.h**. Questa operazione viene eseguita impostando il percorso appropriato per gli strumenti di sviluppo o copiando questi file nell'area di sviluppo dell'applicazione.

## <a name="using-filex"></a>Uso di FileX

L'uso di FileX è semplice. In pratica, il codice dell'applicazione deve includere ***fx_api.h** _ durante la compilazione e il collegamento con la libreria di runtime FileX _*_fx.a_*_ (o _*_fx.lib_*_). Naturalmente, sono necessari anche i file _*_ThreadX, ovvero tx_api.h_*_ e _*_tx.a_*_ _*_(o tx.lib_*_)_,*.

> [!IMPORTANT]
> Quando si usa FileX in modalità **autonoma (FX_STANDALONE_ENABLE** deve essere definito), i file/librerie ThreadX non sono necessari.

Supponendo che si sta già usando ThreadX, sono necessari quattro passaggi per compilare un'applicazione FileX:

1. Includere il ***file fx_api.h*** in tutti i file dell'applicazione che usano servizi FileX o strutture di dati.
1. Inizializzare il sistema FileX chiamando ***fx_system_initialize** _ dalla funzione _ *_tx_application_define_** o da un thread dell'applicazione.

    > [!IMPORTANT]
    > Quando si usa FileX in modalità ***autonoma,*** fx_system_initialize deve essere chiamato direttamente dal codice dell'applicazione.

1. Aggiungere una o più chiamate a ***fx_media_open*** configurare il supporto FileX. Questa chiamata deve essere effettuata dal contesto di un thread dell'applicazione.

    > [!IMPORTANT]
    > *Tenere presente che **la fx_media_open** richiede una quantità di RAM sufficiente per archiviare i dati per un settore.*

1. Compilare l'origine dell'applicazione e collegarsi alle librerie di runtime FileX e ThreadX, ***fx.a** _ _*_(o fx.lib_*_) e _*_tx.a_*_ (o _*_tx.lib_**). L'immagine risultante può essere scaricata nella destinazione ed eseguita.

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ogni porta FileX viene recapitata con un'applicazione dimostrativa. È sempre buona idea che il sistema dimostrativo sia in esecuzione per primo, ovvero nell'hardware di destinazione o in un ambiente dimostrativo specifico.

Se il sistema dimostrativo non funziona, provare a eseguire le operazioni seguenti per restringere il problema:

1. Determinare la parte della dimostrazione in esecuzione.
1. Aumentare le dimensioni dello stack (questo aspetto è più importante nel codice dell'applicazione effettivo rispetto alla dimostrazione).
1. Assicurarsi che la RAM sia sufficiente per le dimensioni predefinite del disco ram di 32 KB. Il sistema di base funzionerà su una quantità molto minore di RAM; Tuttavia, poiché viene usata una quantità maggiore del disco RAM, si verificano problemi se la memoria non è sufficiente.
1. Ignorare temporaneamente le modifiche recenti per verificare se il problema scompare o cambia. Tali informazioni dovrebbero risultare utili per i tecnici del supporto Tecnico Microsoft. Seguire le procedure descritte in "Customer Support Center" per inviare le informazioni raccolte dai passaggi per la risoluzione dei problemi.

## <a name="configuration-options"></a>Opzioni di configurazione

Quando si compila la libreria FileX e l'applicazione usando FileX, sono disponibili diverse opzioni di configurazione. Le opzioni seguenti possono essere definite nell'origine dell'applicazione, nella riga di comando o nel file ***di inclusione fx_user.h.***

> [!IMPORTANT]
> Le opzioni definite *in **fx_user.h** vengono applicate solo se l'applicazione e la libreria ThreadX vengono compilate con **_FX_INCLUDE_USER_DEFINE_FILE_*_ defined._ Quando*** si usa FileX in modalità autonoma (è necessario definire FX_STANDALONE_ENABLE * ), i file/librerie ThreadX non sono necessari.

L'elenco seguente descrive in dettaglio ogni opzione di configurazione:

|Definire|Significato|
|----------    |-----------|
|FX_MAX_LAST_NAME_LEN        |Questo valore definisce la lunghezza massima del nome file, che include il nome del percorso completo. Per impostazione predefinita, tale valore è 256.|
|FX_DONT_UPDATE_OPEN_FILES    |Definito, FileX non aggiorna i file già aperti.|
|FX_MEDIA_DISABLE_SEARCH_CACHE    |Definito, l'ottimizzazione della cache di ricerca file è disabilitata.|
|FX_MEDIA_DISABLE_SEARCH_CACHE    |Definito, l'ottimizzazione della cache di ricerca file è disabilitata.|
|FX_DISABLE_DIRECT_DATA_READ_CACHE_FILL |Definito, l'aggiornamento del settore di lettura diretta della cache è disabilitato.|
|FX_MEDIA_STATISTICS_DISABLE |Definito, la raccolta di statistiche multimediali è disabilitata.|
|FX_SINGLE_OPEN_LEGACY |È abilitata la logica di apertura singola legacy per lo stesso file.|
|FX_RENAME_PATH_INHERIT    |Definito, la ridenominazione eredita le informazioni sul percorso.|
|FX_DISABLE_ERROR_CHECKING    |Rimuove l'API di controllo degli errori FileX di base e comporta prestazioni migliorate (fino al 30%) e dimensioni del codice inferiori.|
|FX_MAX_LONG_NAME_LEN    |Specifica le dimensioni massime del nome file per FileX. Il valore predefinito è 256, ma può essere sostituito con una definizione della riga di comando. I valori validi sono compresi tra 13 e 256.|
|FX_MAX_SECTOR_CACHE|Specifica il numero massimo di settori logici che possono essere memorizzati nella cache da FileX. Il numero effettivo di settori che è possibile memorizzare nella cache è minore di questa costante e il numero di settori che possono rientrare nella quantità di memoria fornita fx_media_open. Il valore predefinito è 256. Tutti i valori devono avere una potenza di 2.|
|FX_FAT_MAP_SIZE    |Specifica il numero di settori che possono essere rappresentati nella mappa di aggiornamento FAT. Il valore predefinito è 256, ma può essere sostituito con una definizione della riga di comando. Valori più grandi consentono di ridurre gli aggiornamenti non necessari dei settori FAT secondari.|
|FX_MAX_FAT_CACHE    |Specifica il numero di voci nella cache FAT interna. Il valore predefinito è 16, ma può essere sostituito con una definizione della riga di comando. Tutti i valori devono essere una potenza di 2.|
|FX_FAULT_TOLERANT    |Se definito, FileX passa immediatamente le richieste di scrittura di tutti i settori di sistema (settori di avvio, FAT e directory) al driver del supporto. Questo riduce potenzialmente le prestazioni, ma consente di limitare il danneggiamento ai cluster persi. Si noti che l'abilitazione di questa funzionalità non abilita automaticamente il modulo a tolleranza di errore FileX, che viene abilitato definendo|
|FX_FAULT_TOLERANT_DATA    |Se definito, FileX passa immediatamente tutte le richieste di scrittura dei dati dei file al driver del supporto. Questo riduce potenzialmente le prestazioni, ma consente di limitare la perdita dei dati dei file. Si noti che l'abilitazione di questa funzionalità non abilita automaticamente il modulo a tolleranza di errore FileX, che viene abilitato ***definendo*** FX_ENABLE_FAULT_TOLERANT|
|FX_NO_LOCAL_PATH|Rimuove la logica del percorso locale da FileX, con conseguente dimensione del codice inferiore.|
|FX_NO_TIMER|Elimina la configurazione del timer ThreadX per aggiornare l'ora e la data del sistema FileX. In questo modo, l'ora e la data predefinite vengono inserite in tutte le operazioni sui file.|
|FX_UPDATE_RATE_IN_SECONDS    |Specifica la frequenza con cui viene regolata l'ora di sistema in FileX. Per impostazione predefinita, il valore è 10, che specifica che l'ora del sistema FileX viene aggiornata ogni 10 secondi.|
|FX_ENABLE_EXFAT| Quando è definito, la logica per la gestione dei file system exFAT è abilitata in FileX. Per impostazione predefinita, questo simbolo non è definito.| 
|FX_UPDATE_RATE_IN_TICKS| Specifica la stessa frequenza ***di*** FX_UPDATE_RATE_IN_SECONDS (vedere sopra), ad eccezione della frequenza del timer ThreadX sottostante. Il valore predefinito è 1000, che presuppone una frequenza di timer ThreadX di 10 ms e un intervallo di 10 secondi.|
|FX_SINGLE_THREAD|Elimina la logica di protezione ThreadX dall'origine FileX. Deve essere usato se FileX viene usato solo da un thread o se FileX viene usato senza ThreadX.|
|FX_DRIVER_USE_64BIT_LBA|Se definito, abilita gli indirizzi di settore a 64 bit usati nel driver di I/O. Per impostazione predefinita, questa opzione non è definita.|
|FX_ENABLE_FAULT_TOLERANT| Se definito, abilita il modulo a tolleranza di errore FileX. L'abilitazione della tolleranza di errore definisce **automaticamente il simbolo * FX_FAULT_TOLERANT** _ e _*_FX_FAULT_TOLERANT_DATA_**. Per impostazione predefinita, questa opzione non è definita.|
|FX_FAULT_TOLERANT_BOOT_INDEX|Definisce l'offset dei byte nel settore di avvio in cui si trova il cluster per il log a tolleranza di errore. Per impostazione predefinita, questo valore è 116. Questo campo accetta 4 byte. I byte da 116 a 119 vengono scelti perché sono contrassegnati come riservati dalla specifica FAT 32/16/32/exFAT.|
|FX_FAULT_TOLERANT_MINIMAL_CLUSTER|Questo simbolo è deprecato. Non viene più usato dalla tolleranza di errore FileX.|
|FX_STANDALONE_ENABLE|Definito, consente l'uso di FileX in modalità autonoma (senza Azure RTOS). Per impostazione predefinita, questo simbolo non è definito.|

> [!IMPORTANT]
> Quando **FX_STANDALONE_ENABLE** definita, la logica del percorso locale e la configurazione del timer ThreadX sono disabilitate.

## <a name="filex-version-id"></a>ID versione FileX

La versione corrente di FileX è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione. Il programmatore può ottenere la versione FileX dall'esame del file **fx_port.h.** Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software applicativo può ottenere la versione di FileX esaminando la stringa **globale _ _fx_version_id_**.
