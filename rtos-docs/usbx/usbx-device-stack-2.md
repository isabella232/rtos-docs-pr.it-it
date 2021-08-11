---
title: Capitolo 2 - Azure RTOS'installazione dello stack di dispositivi USBX
description: Informazioni su come installare lo stack Azure RTOS dispositivo USBX, oltre alle importanti considerazioni sull'host da tenere in considerazione prima di installare.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: abe3e43e090890a5e51700fc2f587c59619fcdad5b71681fd4071c614dab5ce6
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791406"
---
# <a name="chapter-2---azure-rtos-usbx-device-stack-installation"></a>Capitolo 2 - Azure RTOS'installazione dello stack di dispositivi USBX

## <a name="host-considerations"></a>Considerazioni sull'host

### <a name="computer-type"></a>Tipo computer

Lo sviluppo incorporato viene in genere eseguito Windows computer host PC o Unix. Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.

### <a name="download-interfaces"></a>Scaricare le interfacce

In genere il download di destinazione viene eseguito tramite un'interfaccia seriale RS-232, anche se le interfacce parallele, USB ed Ethernet stanno diventando sempre più popolari. Per le opzioni disponibili, vedere la documentazione dello strumento di sviluppo.

### <a name="debugging-tools"></a>Strumenti di debug

Il debug viene in genere eseguito sullo stesso collegamento del download dell'immagine del programma. Esistono diversi debugger, che vanno da piccoli programmi di monitoraggio in esecuzione nella destinazione tramite gli strumenti BDM (Background Debug Monitor) e In-Circuit Emulator (ICE). Lo strumento ICE offre il debug più affidabile dell'hardware di destinazione effettivo.

### <a name="required-hard-disk-space"></a>Spazio su disco rigido richiesto

Il codice sorgente per USBX viene fornito in formato ASCII e richiede circa 500 KByte di spazio sul disco rigido del computer host.

### <a name="target-considerations"></a>Considerazioni sulla destinazione

USBX richiede da 24 KByte a 64 KByte di memoria di sola lettura (ROM) sulla destinazione in modalità host. La quantità di memoria necessaria dipende dal tipo di controller usato e dalle classi USB collegate a USBX. Altri 32 KByte della memoria ad accesso casuale (RAM) della destinazione sono necessari per le strutture di dati globali USBX e il pool di memoria. Questo pool di memoria può anche essere regolato a seconda del numero previsto di dispositivi nell'USB e del tipo di controller USB. Il lato del dispositivo USBX richiede circa 10-12 K di ROM a seconda del tipo di controller del dispositivo. L'utilizzo della memoria RAM dipende dal tipo di classe emulata dal dispositivo.

USBX si basa anche su semafori ThreadX, mutex e thread per la protezione di più thread, la sospensione di I/O e l'elaborazione periodica per il monitoraggio della topologia del bus USB.

### <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS USBX può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/usbx/> .

Di seguito è riportato un elenco di diversi file importanti nel repository.

* ***ux_api.h:*** questo file di intestazione C contiene tutti gli elementi di sistema, le strutture dei dati e i prototipi di servizio.
* ***ux_port.h:*** questo file di intestazione C contiene tutte le definizioni e le strutture di dati specifiche dello strumento di sviluppo.
* ***ux.lib:*** versione binaria della libreria USBX C. Viene distribuito con il pacchetto standard.
* ***demo_usbx.c:*** file C contenente una semplice demo USBX

Tutti i nomi file sono in lettere minuscole. Questa convenzione di denominazione semplifica la conversione dei comandi in piattaforme di sviluppo Unix.

## <a name="usbx-installation"></a>Installazione di USBX

USBX viene installato clonando GitHub repository nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository USBX nel PC:

```c
    git clone https://github.com/azure-rtos/usbx
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante di download nella GitHub principale.

Le istruzioni per la compilazione della libreria USBX sono disponibili anche nella prima pagina del repository online.

Le istruzioni generali seguenti si applicano praticamente a qualsiasi installazione:

1. Usare la stessa directory in cui in precedenza è stato installato ThreadX nel disco rigido host. Tutti i nomi USBX sono univoci e non interferiranno con l'installazione precedente di USBX.
1. Aggiungere una chiamata a ***ux_system_initialize** _ all'inizio di __*_ tx_application_define **. Qui vengono inizializzate le risorse USBX.
1. Aggiungere una chiamata a ***ux_device_stack_initialize*.**
1. Aggiungere una o più chiamate per inizializzare le classi USBX necessarie (classi host e/o dispositivi)
1. Aggiungere una o più chiamate per inizializzare il controller di dispositivo disponibile nel sistema.
1. Potrebbe essere necessario modificare il file tx_low_level_initialize.c per aggiungere l'inizializzazione hardware di basso livello e il routing del vettore di interrupt. Questo è specifico della piattaforma hardware e non verrà illustrato qui.|
1. Compilare il codice sorgente dell'applicazione e collegarsi alle librerie di runtime USBX e ThreadX (possono essere necessari anche FileX e/o Netx se la classe di archiviazione USB e/o le classi di rete USB devono essere compilate in), ux.a (o ux.lib) e tx.a (o tx.lib). L'oggetto risultante può essere scaricato nella destinazione ed eseguito.

## <a name="configuration-options"></a>Opzioni di configurazione

Esistono diverse opzioni di configurazione per la compilazione della libreria USBX. Tutte le opzioni si trovano nel ***file ux_user.h.***

L'elenco seguente illustra in dettaglio ogni opzione di configurazione.

| Opzione di &nbsp; configurazione | Descrizione |
| --- | --- |
| **UX_PERIODIC_RATE** | Questo valore rappresenta il numero di tick al secondo per una piattaforma hardware specifica. Il valore predefinito è 1000 che indica 1 tick al millisecondo. |
| **UX_THREAD_STACK_SIZE** | Questo valore è la dimensione dello stack in byte per i thread USBX. In genere può essere di 1024 byte o 2048 byte a seconda del processore usato e del controller host. |
| **UX_THREAD_PRIORITY_ENUM** | Si tratta del valore di priorità ThreadX per i thread di enumerazione USBX che monitora la topologia del bus. |
| **UX_THREAD_PRIORITY_CLASS** | Si tratta del valore di priorità ThreadX per i thread USBX standard. |
| **UX_THREAD_PRIORITY_KEYBOARD** | Si tratta del valore di priorità ThreadX per la classe di tastiera HID USBX. |
| **UX_THREAD_PRIORITY_DCD** | Si tratta del valore di priorità ThreadX per il thread del controller del dispositivo. |
| **UX_NO_TIME_SLICE** | Questo valore definisce effettivamente l'intervallo di tempo che verrà usato per i thread. Se, ad esempio, è stato definito su 0, la porta di destinazione ThreadX non usa gli intervallo di tempo. |
| **UX_MAX_SLAVE_CLASS_DRIVER** | Si tratta del numero massimo di classi USBX che possono essere registrate tramite ux_device_stack_class_register. |
| **UX_MAX_SLAVE_LUN** | Questo valore rappresenta il numero corrente di unità logiche SCSI rappresentate nel driver della classe di archiviazione del dispositivo. |
| **UX_SLAVE_CLASS_STORAGE_INCLUDE_MMC** | Se definita, la classe di archiviazione gestirà i comandi multi-media (MMC), ovvero DVD-ROM. |
| **UX_DEVICE_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES** | Questo valore rappresenta il numero di pacchetti NetX nel pool di pacchetti della classe CDC-ECM. Il valore predefinito è 16. |
| **UX_SLAVE_REQUEST_CONTROL_MAX_LENGTH** | Questo valore rappresenta il numero massimo di byte ricevuti in un endpoint di controllo nello stack del dispositivo. Il valore predefinito è 256 byte, ma può essere ridotto negli ambienti con vincoli di memoria. |
| **UX_DEVICE_CLASS_HID_EVENT_BUFFER_LENGTH** | Questo valore rappresenta la lunghezza massima in byte di un report HID. |
| **UX_DEVICE_CLASS_HID_MAX_EVENTS_QUEUE** | Questo valore rappresenta il numero massimo di report HID che possono essere accodati contemporaneamente. |
| **UX_SLAVE_REQUEST_DATA_MAX_LENGTH** | Questo valore rappresenta il numero massimo di byte ricevuti in un endpoint bulk nello stack di dispositivi. Il valore predefinito è 4096 byte, ma può essere ridotto negli ambienti con vincoli di memoria. |

## <a name="source-code-tree"></a>Albero del codice sorgente

I file USBX vengono forniti in diverse directory.

![Albero del codice sorgente](media/usbx-device-stack/source-code-tree.png)

Per rendere i file riconoscibili in base ai nomi, è stata adottata la convenzione seguente:

| Nome suffisso file  | Descrizione file                          |
| ----------------- | ----------------------------------------- |
| ux_host_stack   | File di base dello stack di host usbx                |
| ux_host_class   | File di classi dello stack host usbx             |
| ux_hcd           | File del driver del controller dello stack di host usbx   |
| ux_device_stack | File di base dello stack di dispositivi usbx              |
| ux_device_class | File di classi dello stack di dispositivi usbx           |
| ux_dcd           | File del driver del controller dello stack di dispositivi usbx |
| ux_otg           | File correlati al driver del controller usbx otg  |
| ux_pictbridge    | File usbx pictbridge                     |
| ux_utility       | Funzioni dell'utilità usbx                    |
| demo_usbx        | file dimostrativi per USBX              |

## <a name="initialization-of-usbx-resources"></a>Inizializzazione delle risorse USBX

USBX ha un proprio gestore di memoria. La memoria deve essere allocata a USBX prima dell'inizializzazione del lato host o dispositivo di USBX. Gestione memoria USBX può supportare sistemi in cui la memoria può essere memorizzata nella cache.

La funzione seguente inizializza le risorse di memoria USBX con 128 K di memoria normale e nessun pool separato per la memoria sicura della cache:

```c
/* Initialize USBX Memory */
ux_system_initialize(memory_pointer,(128*1024),UX_NULL,0);
```

Il prototipo per il ux_system_initialize è il seguente:

```c
UINT ux_system_initialize(VOID *regular_memory_pool_start,
        ULONG regular_memory_size,
        VOID *cache_safe_memory_pool_start,
        ULONG cache_safe_memory_size);
```

Parametri di input:

| Parametro                          | Descrizione                             |
| ---------------------------------- | --------------------------------------- |
| VOID *regular_memory_pool_start    | Inizio del pool di memoria normale    |
| ULONG regular_memory_size          | Dimensioni del pool di memoria normale         |
| VOID *cache_safe_memory_pool_start | Inizio del pool di memoria sicura della cache |
| ULONG cache_safe_memory_size       | Dimensioni del pool di memoria sicura della cache      |

Non tutti i sistemi richiedono la definizione di memoria sicura della cache. In un sistema di questo tipo, i valori passati durante l'inizializzazione per il puntatore alla memoria verranno impostati su UX_NULL e le dimensioni del pool su 0. USBX userà quindi il pool di memoria normale al posto del pool sicuro della cache.

In un sistema in cui la memoria normale non è sicura per la cache e un controller richiede l'esecuzione della memoria DMA, è necessario definire un pool di memoria in una zona sicura della cache.

## <a name="uninitialization-of-usbx-resources"></a>Annullamento dell'inizializzazione delle risorse USBX

USBX può essere terminato rilasciando le relative risorse. Prima di terminare usbx, tutte le classi e le risorse del controller devono essere terminate correttamente. La funzione seguente annulla l'inizializzazione delle risorse di memoria USBX:

```c
/* Unitialize USBX Resources */

ux_system_uninitialize();
```

Il prototipo per il ux_system_initialize è il seguente:

```c
UINT ux_system_uninitialize(VOID);
```

## <a name="definition-of-usb-device-controller"></a>Definizione del controller di dispositivo USB

È possibile definire un solo controller di dispositivo USB in qualsiasi momento per operare in modalità dispositivo. Il file di inizializzazione dell'applicazione deve contenere questa definizione. La riga seguente esegue la definizione di un controller USB generico:

```c
ux_dcd_controller_initialize(0x7BB00000, 0, 0xB7A00000);
```

L'inizializzazione del dispositivo USB ha il prototipo seguente:

```c
UINT ux_dcd_controller_initialize(ULONG dcd_io,
    ULONG dcd_irq, ULONG dcd_vbus_address);
```

con i parametri seguenti:

| Pararmeter               | Descrizione                      |
| ------------------------ | -------------------------------- |
| ULONG dcd_io            | Indirizzo dell'I/O del controller     |
| ULONG dcd_irq           | Interrupt usato dal controller |
| ULONG dcd_vbus_address | Indirizzo dell'oggetto GPIO VBUS         |

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

USBX viene fornito con un file dimostrativo e un ambiente di simulazione. È sempre buona idea che la piattaforma dimostrativa sia in esecuzione per prima, sia nell'hardware di destinazione che in una piattaforma dimostrativa specifica.

## <a name="usbx-version-id"></a>ID versione USBX

La versione corrente di USBX è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione. Il programmatore può ottenere la versione USBX dall'esame del file *** ux_port.h** _. Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software dell'applicazione può ottenere la versione USBX esaminando la stringa globale *_ __ ux_version_id_* _, definita in _*_ux_port.h_**.
