---
title: Capitolo 2-installazione dello stack di dispositivi USBX di Azure RTO
description: Informazioni su come installare lo stack di dispositivi USBX di Azure RTO, nonché le considerazioni importanti sull'host che è necessario considerare prima di installare.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: dd58f77130fa252be9163bd70c29f7deee400d30
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106549777"
---
# <a name="chapter-2---azure-rtos-usbx-device-stack-installation"></a>Capitolo 2-installazione dello stack di dispositivi USBX di Azure RTO

## <a name="host-considerations"></a>Considerazioni sull'host

### <a name="computer-type"></a>Tipo computer

Lo sviluppo incorporato viene in genere eseguito nei computer host Windows o UNIX. Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.

### <a name="download-interfaces"></a>Interfacce di download

Il download di destinazione viene in genere eseguito tramite un'interfaccia seriale RS-232, sebbene le interfacce parallele, USB e Ethernet stiano diventando più diffuse. Per le opzioni disponibili, vedere la documentazione dello strumento di sviluppo.

### <a name="debugging-tools"></a>Strumenti di debug

Il debug viene eseguito in genere sullo stesso collegamento del download dell'immagine del programma. Sono disponibili diversi debugger, a partire da piccoli programmi di monitoraggio in esecuzione nella destinazione tramite il monitoraggio di debug in background (BDM) e gli strumenti di In-Circuit Emulator (ICE). Lo strumento ICE fornisce il debug più affidabile dell'hardware di destinazione effettivo.

### <a name="required-hard-disk-space"></a>Spazio su disco rigido richiesto

Il codice sorgente per USBX viene fornito in formato ASCII e richiede circa 500 KB di spazio sul disco rigido del computer host.

### <a name="target-considerations"></a>Considerazioni sulla destinazione

USBX richiede tra 24 KByte e 64 Kbyte di memoria di sola lettura (ROM) nella destinazione in modalità host. La quantità di memoria richiesta dipende dal tipo di controller usato e dalle classi USB collegate a USBX. Sono necessari altri 32 KByte della memoria ad accesso casuale (RAM) della destinazione per le strutture di dati globali USBX e il pool di memoria. È anche possibile modificare questo pool di memoria in base al numero previsto di dispositivi sul dispositivo USB e al tipo di controller USB. Il lato dispositivo USBX richiede circa 10-12 K di ROM a seconda del tipo di controller del dispositivo. L'utilizzo della memoria RAM dipende dal tipo di classe emulata dal dispositivo.

USBX si basa anche su semafori, mutex e thread ThreadX per la protezione di più thread e la sospensione di I/O e l'elaborazione periodica per il monitoraggio della topologia del bus USB.

### <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTO USBX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/usbx/> .

Di seguito è riportato un elenco di diversi file importanti nel repository.

* ***ux_api. h***: questo file di intestazione C contiene tutti gli equivalenti di sistema, le strutture di dati e i prototipi di servizio.
* ***ux_port. h***: questo file di intestazione C contiene tutte le definizioni e le strutture dei dati specifici dello strumento di sviluppo.
* ***UX. lib***: è la versione binaria della libreria C di USBX. Viene distribuito con il pacchetto standard.
* ***demo_usbx. c***: il file c contenente una demo USBX semplice

Tutti i nomi di file sono in lettere minuscole. Questa convenzione di denominazione rende più semplice convertire i comandi in piattaforme di sviluppo Unix.

## <a name="usbx-installation"></a>Installazione di USBX

USBX viene installato clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository USBX nel PC:

```c
    git clone https://github.com/azure-rtos/usbx
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante Download nella pagina principale di GitHub.

Sono inoltre disponibili istruzioni per la compilazione della libreria USBX nella pagina iniziale del repository online.

Le istruzioni generali riportate di seguito si applicano praticamente a qualsiasi installazione:

1. Usare la stessa directory in cui è stato precedentemente installato ThreadX nel disco rigido host. Tutti i nomi di USBX sono univoci e non interferiscono con l'installazione precedente di USBX.
1. Aggiungere una chiamata a ***ux_system_initialize** _ all'inizio di _ *_tx_application_define_* *. Questa è la posizione in cui vengono inizializzate le risorse di USBX.
1. Aggiungere una chiamata a ***ux_device_stack_initialize *.**
1. Aggiungere una o più chiamate per inizializzare le classi USBX obbligatorie (classi host e/o dispositivi)
1. Aggiungere una o più chiamate per inizializzare il controller del dispositivo disponibile nel sistema.
1. Potrebbe essere necessario modificare il file tx_low_level_initialize. c per aggiungere l'inizializzazione hardware di basso livello e il routing vettoriale di interrupt. Questo è specifico per la piattaforma hardware e non verrà discusso qui. |
1. Compilare il codice sorgente dell'applicazione e il collegamento con le librerie di runtime USBX e ThreadX (FileX e/o NETX potrebbero essere necessari anche se la classe di archiviazione USB e/o le classi di rete USB devono essere compilate in), UX. a (o UX. lib) e TX. a (o TX. lib). Il risultato può essere scaricato nella destinazione ed eseguito.

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la compilazione della libreria USBX. Tutte le opzioni si trovano in ***ux_user. h***.

Nell'elenco seguente vengono illustrate tutte le opzioni di configurazione.

| Opzione di configurazione &nbsp; | Descrizione |
| --- | --- |
| **UX_PERIODIC_RATE** | Questo valore rappresenta il numero di cicli al secondo per una piattaforma hardware specifica. Il valore predefinito è 1000 che indica 1 segno di cicli per millisecondo. |
| **UX_THREAD_STACK_SIZE** | Questo valore corrisponde alla dimensione dello stack in byte per i thread USBX. Può essere in genere 1024 byte o 2048 byte a seconda del processore usato e del controller host. |
| **UX_THREAD_PRIORITY_ENUM** | Si tratta del valore di priorità ThreadX per i thread di enumerazione USBX che monitora la topologia del bus. |
| **UX_THREAD_PRIORITY_CLASS** | Si tratta del valore di priorità ThreadX per i thread USBX standard. |
| **UX_THREAD_PRIORITY_KEYBOARD** | Si tratta del valore di priorità ThreadX per la classe della tastiera USBX HID. |
| **UX_THREAD_PRIORITY_DCD** | Si tratta del valore di priorità ThreadX per il thread del controller del dispositivo. |
| **UX_NO_TIME_SLICE** | Questo valore definisce effettivamente l'intervallo di tempo che verrà usato per i thread. Se, ad esempio, viene definito su 0, la porta di destinazione ThreadX non utilizza intervalli di tempo. |
| **UX_MAX_SLAVE_CLASS_DRIVER** | Questo è il numero massimo di classi USBX che possono essere registrate tramite ux_device_stack_class_register. |
| **UX_MAX_SLAVE_LUN** | Questo valore rappresenta il numero corrente di unità logiche SCSI rappresentate nel driver della classe di archiviazione del dispositivo. |
| **UX_SLAVE_CLASS_STORAGE_INCLUDE_MMC** | Se definito, la classe di archiviazione gestirà i comandi Multimedia (MMC), ovvero DVD-ROM. |
| **UX_DEVICE_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES** | Questo valore rappresenta il numero di pacchetti NetX nel pool di pacchetti della classe CDC-ECM. Il valore predefinito è 16. |
| **UX_SLAVE_REQUEST_CONTROL_MAX_LENGTH** | Questo valore rappresenta il numero massimo di byte ricevuti su un endpoint di controllo nello stack del dispositivo. Il valore predefinito è 256 byte, ma può essere ridotto in ambienti di vincoli di memoria. |
| **UX_DEVICE_CLASS_HID_EVENT_BUFFER_LENGTH** | Questo valore rappresenta la lunghezza massima in byte di un report nascosto. |
| **UX_DEVICE_CLASS_HID_MAX_EVENTS_QUEUE** | Questo valore rappresenta il numero massimo di report HID che possono essere accodati in una sola volta. |
| **UX_SLAVE_REQUEST_DATA_MAX_LENGTH** | Questo valore rappresenta il numero massimo di byte ricevuti in un endpoint bulk nello stack del dispositivo. Il valore predefinito è 4096 byte, ma può essere ridotto in ambienti di vincoli di memoria. |

## <a name="source-code-tree"></a>Albero del codice sorgente

I file USBX sono disponibili in più directory.

![Albero del codice sorgente](media/usbx-device-stack/source-code-tree.png)

Per rendere i file riconoscibili con i rispettivi nomi, è stata adottata la convenzione seguente:

| Nome suffisso file  | Descrizione file                          |
| ----------------- | ----------------------------------------- |
| ux_host_stack   | USBX file core dello stack host                |
| ux_host_class   | file delle classi dello stack host USBX             |
| ux_hcd           | file driver del controller dello stack host USBX   |
| ux_device_stack | file principali dello stack di dispositivi USBX              |
| ux_device_class | file delle classi dello stack del dispositivo USBX           |
| ux_dcd           | file driver del controller dello stack del dispositivo USBX |
| ux_otg           | file correlati driver del controller USBX OTG  |
| ux_pictbridge    | file PictBridge USBX                     |
| ux_utility       | funzioni di utilità USBX                    |
| demo_usbx        | file dimostrativi per USBX              |

## <a name="initialization-of-usbx-resources"></a>Inizializzazione delle risorse di USBX

USBX dispone di un proprio gestore della memoria. La memoria deve essere allocata a USBX prima che il lato host o dispositivo di USBX venga inizializzato. Il gestore della memoria USBX può supportare i sistemi in cui è possibile memorizzare nella cache la memoria.

La funzione seguente inizializza le risorse di memoria USBX con 128 K di memoria normale e nessun pool separato per la memoria sicura della cache:

```c
/* Initialize USBX Memory */
ux_system_initialize(memory_pointer,(128*1024),UX_NULL,0);
```

Il prototipo per la ux_system_initialize è il seguente:

```c
UINT ux_system_initialize(VOID *regular_memory_pool_start,
        ULONG regular_memory_size,
        VOID *cache_safe_memory_pool_start,
        ULONG cache_safe_memory_size);
```

Parametri di input:

| Parametro                          | Descrizione                             |
| ---------------------------------- | --------------------------------------- |
| VOID * regular_memory_pool_start    | Inizio del pool di memoria normale    |
| Regular_memory_size ULONG          | Dimensioni del pool di memoria normale         |
| VOID * cache_safe_memory_pool_start | Inizio del pool di memoria sicuro della cache |
| Cache_safe_memory_size ULONG       | Dimensioni del pool di memoria sicuro della cache      |

Non tutti i sistemi richiedono la definizione di memoria protetta dalla cache. In tale sistema, i valori passati durante l'inizializzazione per il puntatore di memoria verranno impostati su UX_NULL e le dimensioni del pool su 0. USBX utilizzerà quindi il normale pool di memoria anziché il pool di sicurezza della cache.

In un sistema in cui la memoria normale non è protetta dalla cache e un controller richiede per eseguire la memoria DMA è necessario definire un pool di memoria in un'area di sicurezza della cache.

## <a name="uninitialization-of-usbx-resources"></a>Inizializzazione delle risorse di USBX

USBX può essere terminato rilasciando le risorse. Prima di terminare il USBX, tutte le classi e le risorse del controller devono essere terminate correttamente. La funzione seguente consente di uninizializzare le risorse di memoria USBX:

```c
/* Unitialize USBX Resources */

ux_system_uninitialize();
```

Il prototipo per la ux_system_initialize è il seguente:

```c
UINT ux_system_uninitialize(VOID);
```

## <a name="definition-of-usb-device-controller"></a>Definizione del controller del dispositivo USB

Per il funzionamento in modalità dispositivo è possibile definire un solo controller di dispositivo USB in qualsiasi momento. Il file di inizializzazione dell'applicazione deve contenere questa definizione. La riga seguente esegue la definizione di un controller USB generico:

```c
ux_dcd_controller_initialize(0x7BB00000, 0, 0xB7A00000);
```

L'inizializzazione del dispositivo USB presenta il seguente prototipo:

```c
UINT ux_dcd_controller_initialize(ULONG dcd_io,
    ULONG dcd_irq, ULONG dcd_vbus_address);
```

con i parametri seguenti:

| Pararmeter               | Descrizione                      |
| ------------------------ | -------------------------------- |
| Dcd_io ULONG            | Indirizzo dell'IO del controller     |
| Dcd_irq ULONG           | Interrupt utilizzato dal controller |
| Dcd_vbus_address ULONG | Indirizzo del GPIO VBUS         |

L'esempio seguente è l'inizializzazione di USBX in modalità dispositivo con la classe del dispositivo di archiviazione e un controller generico:

```c
/* Initialize USBX Memory */

ux_system_initialize(memory_pointer,(128*1024), 0, 0);

/* The code below is required for installing the device portion of USBX */
status = ux_device_stack_initialize(&device_framework_high_speed,
    DEVICE_FRAMEWORK_LENGTH_HIGH_SPEED, &device_framework_full_speed,
    DEVICE_FRAMEWORK_LENGTH_FULL_SPEED, &string_framework,
    STRING_FRAMEWORK_LENGTH, &language_id_framework,
    LANGUAGE_ID_FRAMEWORK_LENGTH, UX_NULL);

/* If status equals UX_SUCCESS, installation was successful. */

/* Store the number of LUN in this device storage instance: single LUN. */
storage_parameter.ux_slave_class_storage_parameter_number_lun = 1;

/* Initialize the storage class parameters for reading/writing to the Flash Disk. */
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_last_lba = 0x1e6bfe;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_block_length = 512;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_type = 0;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_removable_flag = 0x80;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_read = tx_demo_thread_flash_media_read;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_write = tx_demo_thread_flash_media_write;
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_status = tx_demo_thread_flash_media_status;

/* Initialize the device storage class. The class is connected with interface 0 */
status = ux_device_stack_class_register(ux_system_slave_class_storage_name ux_device_class_storage_entry,
    ux_device_class_storage_thread,0, (VOID *)&storage_parameter);

/* Register the device controllers available in this system */
status = ux_dcd_controller_initialize(0x7BB00000, 0, 0xB7A00000);

/* If status equals UX_SUCCESS, registration was successful. */
```

## <a name="troubleshooting"></a>Risoluzione dei problemi

USBX viene fornito con un file dimostrativo e un ambiente di simulazione. È sempre consigliabile ottenere prima di tutto la piattaforma dimostrativa, sia nell'hardware di destinazione che in una piattaforma dimostrativa specifica.

## <a name="usbx-version-id"></a>ID versione USBX

La versione corrente di USBX è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione. Il programmatore può ottenere la versione di USBX dall'esame del file ***ux_port. h** _. Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software applicativo può ottenere la versione di USBX esaminando la stringa globale _ *_ _ux_version_id_* _, definita in _ *_ux_port. h_* *.
