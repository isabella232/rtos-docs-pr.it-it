---
title: 'Capitolo 2: Installazione Azure RTOS stack host USBX'
description: Informazioni su come installare lo stack di host USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 77df2c4e4bf4ef38403fe78eb98f18820de4325aadb941fc69275e4c77754212
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790964"
---
# <a name="chapter-2---azure-rtos-usbx-host-stack-installation"></a>Capitolo 2: Installazione Azure RTOS stack host USBX

## <a name="host-considerations"></a>Considerazioni sull'host

### <a name="computer-type"></a>Tipo computer

Lo sviluppo incorporato viene in genere eseguito Windows computer host PC o Unix. Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.

### <a name="download-interfaces"></a>Interfacce di download

In genere, il download di destinazione viene eseguito tramite un'interfaccia seriale RS-232, anche se le interfacce parallele, USB ed Ethernet stanno diventando sempre più popolari. Per le opzioni disponibili, vedere la documentazione dello strumento di sviluppo.

### <a name="debugging-tools"></a>Strumenti di debug

Il debug viene eseguito in genere tramite lo stesso collegamento del download dell'immagine del programma. Sono disponibili diversi debugger, che vanno da piccoli programmi di monitoraggio in esecuzione nella destinazione fino agli strumenti BDM (Background Debug Monitor) e In-Circuit Emulator (ICE). Lo strumento ICE offre il debug più affidabile dell'hardware di destinazione effettivo.

### <a name="required-hard-disk-space"></a>Spazio richiesto su disco rigido

Il codice sorgente per USBX viene fornito in formato ASCII e richiede circa 500 KByte di spazio sul disco rigido del computer host.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

USBX richiede da 24 kByte a 64 KByte di memoria di sola lettura (ROM) nella destinazione in modalità host. La quantità di memoria necessaria dipende dal tipo di controller usato e dalle classi USB collegate a USBX. Per le strutture di dati globali USBX e il pool di memoria sono necessari altri 32 KB di memoria ad accesso casuale (RAM) della destinazione. Questo pool di memoria può essere regolato anche in base al numero previsto di dispositivi su USB e al tipo di controller USB. Il lato dispositivo USBX richiede circa 10-12 K di ROM a seconda del tipo di controller del dispositivo. L'utilizzo della memoria RAM dipende dal tipo di classe emulata dal dispositivo.

USBX si basa anche su semafori ThreadX, mutex e thread per la protezione di più thread, la sospensione di I/O e l'elaborazione periodica per il monitoraggio della topologia del bus USB.

### <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTOS USBX può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/usbx/> .

Di seguito è riportato un elenco di diversi file importanti nel repository:

- ***ux_api.h:*** questo file di intestazione C contiene tutti gli equilibrazioni di sistema, le strutture di dati e i prototipi di servizio.
- ***ux_port.h:*** questo file di intestazione C contiene tutte le strutture e le definizioni di dati specifiche dello strumento di sviluppo.
- ***ux.lib:*** versione binaria della libreria USBX C. Viene distribuito con il pacchetto standard.
- ***demo_usbx.c:*** file C contenente una semplice demo USBX

Tutti i nomi file sono in lettere minuscole. Questa convenzione di denominazione semplifica la conversione dei comandi in piattaforme di sviluppo Unix.

## <a name="usbx-installation"></a>Installazione di USBX

USBX viene installato clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository USBX nel PC:

```powershell
    git clone https://github.com/azure-rtos/usbx
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante di download nella GitHub pagina principale.

Le istruzioni per la creazione della libreria USBX sono disponibili anche nella pagina iniziale del repository online.

Le istruzioni generali seguenti si applicano praticamente a qualsiasi installazione:

1. Usare la stessa directory in cui in precedenza è stato installato ThreadX nel disco rigido host. Tutti i nomi USBX sono univoci e non interferiranno con l'installazione precedente di USBX.
2. Aggiungere una chiamata a ***ux_system_initialize** _ all'inizio di _ *_tx_application_define_.* * Qui vengono inizializzate le risorse USBX.
3. Aggiungere una chiamata a ***ux_host_stack_initialize*.**
4. Aggiungere una o più chiamate per inizializzare la porta USBX richiesta.
5. Aggiungere una o più chiamate per inizializzare i controller host disponibili nel sistema.
6. Potrebbe essere necessario modificare il file tx_low_level_initialize.c per aggiungere l'inizializzazione hardware di basso livello e il routing del vettore di interrupt. Questa operazione è specifica della piattaforma hardware e non verrà illustrata qui.
7. Compilare il codice sorgente dell'applicazione e collegarsi alle librerie di runtime USBX e ThreadX (Possono essere necessari anche FileX e/o Netx se la classe di archiviazione USB e/o le classi di rete USB devono essere compilate in), ux.a (o ux.lib) e tx.a (o tx.lib). L'oggetto risultante può essere scaricato nella destinazione ed eseguito.

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la compilazione della libreria USBX. Tutte le opzioni si trovano nel ***file ux_user.h.***

L'elenco seguente illustra in dettaglio ogni opzione di configurazione.


- **UX_PERIODIC_RATE:** questo valore rappresenta il numero di tick al secondo per una piattaforma hardware specifica. Il valore predefinito è 1000, che indica un tick per millisecondo.
- **UX_MAX_CLASS_DRIVER:** questo valore è il numero massimo di classi che possono essere caricate da USBX. Questo valore rappresenta il contenitore di classi e non il numero di istanze di una classe. Ad esempio, se una particolare implementazione di USBX richiede la classe hub, la classe della stampante e la classe di archiviazione, il valore UX_MAX_CLASS_DRIVER può essere impostato su 3 indipendentemente dal numero di dispositivi che appartengono a queste classi.
- **UX_MAX_HCD**: questo valore rappresenta il numero di controller host diversi disponibili nel sistema. Per il supporto usb 1.1, questo valore sarà principalmente 1. Per il supporto USB 2.0, questo valore può essere maggiore di 1. Questo valore rappresenta il numero di controller host simultanei in esecuzione contemporaneamente. Se, ad esempio, sono in esecuzione due istanze di OHCI o un ehci e un controller OHCI in esecuzione, il UX_MAX_HCD deve essere impostato su 2. 
- **UX_MAX_DEVICES:** questo valore rappresenta il numero massimo di dispositivi che possono essere collegati all'USB. In genere, il numero massimo teorico in una singola porta USB è 127 dispositivi. Questo valore può essere ridimensionato per risparmiare memoria. Si noti che questo valore rappresenta il numero totale di dispositivi indipendentemente dal numero di bus USB nel sistema.
- **UX_MAX_ED**: questo valore rappresenta il numero massimo di ED nel pool di controller. Questo numero viene assegnato a un solo controller. Se sono presenti più istanze di controller, questo valore viene usato da ogni singolo controller.
- **UX_MAX_TD e UX_MAX_ISO_TD:** questo valore rappresenta il numero massimo di TD regolari e isocroni nel pool di controller. Questo numero viene assegnato a un solo controller. Se sono presenti più istanze di controller, questo valore viene usato da ogni singolo controller.
- **UX_THREAD_STACK_SIZE:** questo valore è la dimensione dello stack in byte per i thread USBX. Può essere in genere di 1024 byte o 2048 byte a seconda del processore usato e del controller host.
- **UX_HOST_ENUM_THREAD_STACK_SIZE:** questo valore è la dimensione dello stack del thread di enumerazione dell'host USB. Se questo simbolo non è impostato, le dimensioni dello stack dei thread di enumerazione host USBX vengono impostate **su UX_THREAD_STACK_SIZE**. 
- **UX_HOST_HCD_THREAD_STACK_SIZE:** questo valore è la dimensione dello stack del thread HCD dell'host USB. Se questo simbolo non è impostato, la dimensione dello stack di thread HCD dell'host USBX viene impostata **su UX_THREAD_STACK_SIZE**.
- **UX_THREAD_PRIORITY_ENUM:** valore di priorità ThreadX per i thread di enumerazione USBX che monitora la topologia del bus.
- **UX_THREAD_PRIORITY_CLASS:** valore di priorità ThreadX per i thread USBX standard.
- **UX_THREAD_PRIORITY_KEYBOARD:** valore di priorità ThreadX per la classe di tastiera USBX HID.
- **UX_THREAD_PRIORITY_HCD:** valore di priorità ThreadX per il thread del controller host.
- **UX_NO_TIME_SLICE**: questo valore definisce effettivamente l'intervallo di tempo che verrà usato per i thread. Ad esempio, se è definito su 0, la porta di destinazione ThreadX non usa gli intervallo di tempo.
- **UX_MAX_HOST_LUN:** questo valore rappresenta il numero massimo di unità logiche SCSI rappresentate nel driver della classe di archiviazione host.
- **UX_HOST_CLASS_STORAGE_INCLUDE_LEGACY_PROTOCOL_SUPPORT:** se definito, questo valore include il codice per gestire i dispositivi di archiviazione che usano il protocollo CB o CBI ,ad esempio i dischi floppy. È disattivata per impostazione predefinita perché questi protocolli sono obsoleti, sostituiti dal protocollo BOT (Bulk Only Transport), che viene utilizzato praticamente da tutti i dispositivi di archiviazione moderni.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE:** se definito, questo valore fa in modo che ux_host_class_hid_keyboard_key_get segnalare solo le modifiche dei tasti, ad esempio le combinazioni di tasti e le versioni dei tasti. Per impostazione predefinita, segnala solo quando una chiave non è disponibile.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_KEY_DOWN_ONLY**: usato solo se **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** è definito. Se definito, fa in modo ux_host_class_hid_keyboard_key_get segnala solo le modifiche ai tasti premuti o in basso; Le modifiche alla chiave rilasciate o rilasciate non vengono segnalate.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_LOCK_KEYS**: usato solo se **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** è definito. Se definito, fa in modo ux_host_class_hid_keyboard_key_get segnalare le modifiche alla chiave di blocco (CapsLock/NumLock/ScrollLock).
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_MODIFIER_KEYS**: usato solo se **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** è definito. Se definito, fa in modo ux_host_class_hid_keyboard_key_get segnalare le modifiche apportate al tasto di modifica (CTRL/ALT/MAIUSC/GUI).
- **UX_HOST_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES**: se definito, questo valore rappresenta il numero di pacchetti nella classe host CDC-ECM. Il valore predefinito è 16.

## <a name="source-code-tree"></a>Albero del codice sorgente

I file USBX vengono forniti in diverse directory.

![Albero del codice sorgente](media/usbx-host-stack/source-code-tree.png)

Per rendere i file riconoscibili in base ai nomi, è stata adottata la convenzione seguente:

| Nome suffisso file | Descrizione file                          |
| ---------------- | ----------------------------------------- |
| ux_host_stack    | File di base dello stack host usbx                |
| ux_host_class    | File delle classi dello stack host usbx             |
| ux_hcd           | File del driver del controller dello stack host usbx   |
| ux_device_stack  | File di base dello stack di dispositivi usbx              |
| ux_device_class  | File delle classi dello stack di dispositivi usbx           |
| ux_dcd           | File del driver del controller dello stack di dispositivi usbx |
| ux_otg           | File correlati al driver del controller usbx otg  |
| ux_pictbridge    | File usbx pictbridge                     |
| ux_utility       | Funzioni di utilità usbx                    |
| demo_usbx        | file dimostrativi per USBX              |

## <a name="initialization-of-usbx-resources"></a>Inizializzazione delle risorse USBX

USBX ha un proprio gestore di memoria. La memoria deve essere allocata a USBX prima dell'inizializzazione del lato host o dispositivo di USBX. Gestione memoria USBX può supportare sistemi in cui la memoria può essere memorizzata nella cache.

La funzione seguente inizializza le risorse di memoria USBX con 128 KB di memoria normale e nessun pool separato per la memoria cache sicura:

```c
/* Initialize USBX Memory */

ux_system_initialize(memory_pointer,(128*1024),UX_NULL,0);
```

Il prototipo per il ux_system_initialize è il seguente.

```c
UINT ux_system_initialize( 
    VOID *regular_memory_pool_start,
    ULONG regular_memory_size,
    VOID *cache_safe_memory_pool_start,
    ULONG cache_safe_memory_size);
```

### <a name="input-parameters"></a>Parametri di input:

- **regular_memory_pool_start** Inizio del normale pool di memoria.
- **regular_memory_size** Dimensioni del normale pool di memoria.
- **cache_safe_memory_pool_start** Inizio del pool di memoria cache sicura.
- **cache_safe_memory_size** Dimensioni del pool di memoria sicura della cache.    |

Non tutti i sistemi richiedono la definizione di memoria cache sicura. In un sistema di questo tipo, i valori passati durante l'inizializzazione per il puntatore di memoria verranno impostati su UX_NULL e la dimensione del pool su 0. USBX userà quindi il normale pool di memoria al posto del pool sicuro per la cache.

In un sistema in cui la memoria normale non è sicura per la cache e un controller richiede l'esecuzione della memoria DMA (ad esempio OHCI, controller EHCI tra gli altri), è necessario definire un pool di memoria in una zona sicura della cache.

## <a name="uninitialization-of-usbx-resources"></a>Annullamento dell'inizializzazione delle risorse USBX

USBX può essere terminato rilasciando le relative risorse. Prima di terminare usbx, tutte le classi e le risorse del controller devono essere terminate correttamente. La funzione seguente annulla l'inizializzazione delle risorse di memoria USBX:

```c
/* Unitialize USBX Resources */

ux_system_uninitialize();
```

Il prototipo per il ux_system_initialize è il seguente.

```c
UINT ux_system_uninitialize(VOID);
```

## <a name="definition-of-usb-host-controllers"></a>Definizione di controller host USB

È necessario definire almeno un controller host USB per il funzionamento di USBX in modalità host. Il file di inizializzazione dell'applicazione deve contenere questa definizione. La riga seguente esegue la definizione di un controller host generico.

```c
ux_host_stack_hcd_register("ux_hcd_controller",
        ux_hcd_controller_initialize, 0xd0000, 0x0a);
```

Il ux_host_stack_hcd_register ha il prototipo seguente.

```c
UINT ux_host_stack_hcd_register(
    UCHAR *hcd_name,
    UINT (*hcd_initialize_function)(struct UX_HCD_STRUCT *),
    ULONG hcd_param1, ULONG hcd_param2);
```

La ux_host_stack_hcd_register ha i parametri seguenti.

- **hcd_name**: stringa del nome del controller
- **hcd_initialize_function**: funzione di inizializzazione del controller
- **hcd_param1**: in genere il valore di I/O o la memoria usata dal controller
- **hcd_param2:** in genere l'IRQ usato dal controller

Nell'esempio precedente:

- "ux_hcd_controller" è il nome del controller
- "ux_hcd_controller_initialize" è la routine di inizializzazione per il controller host
- 0xd0000 è l'indirizzo in cui i registri del controller host sono visibili in memoria
- e 0x0a è l'IRQ usato dal controller host.

Di seguito è riportato un esempio dell'inizializzazione di USBX in modalità host con un controller host e diverse classi.

```c
UINT status;

/* Initialize USBX. */
ux_system_initialize(memory_ptr, (128*1024),0,0);

/* The code below is required for installing the USBX host stack. */
status = ux_host_stack_initialize(UX_NULL);

/* If status equals UX_SUCCESS, host stack has been initialized. */

/* Register all the host classes for this USBX implementation. */
status = ux_host_class_register("ux_host_class_hub", ux_host_class_hub_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_storage", ux_host_class_storage_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_printer", ux_host_class_printer_entry);

/* If status equals UX_SUCCESS, host class has been registered. */
status = ux_host_class_register("ux_host_class_audio", ux_host_class_audio_entry);

/* If status equals UX_SUCCESS, host class has been registered. */

/* Register all the USB host controllers available in this system. */ 
status = ux_host_stack_hcd_register("ux_hcd_controller", ux_hcd_controller_initialize, 0x300000, 0x0a);

/* If status equals UX_SUCCESS, USB host controllers have been registered. */
```

## <a name="definition-of-host-classes"></a>Definizione di classi host

È necessario definire una o più classi host con USBX. Una classe USB è necessaria per l'unità di un dispositivo USB dopo che lo stack USB ha configurato il dispositivo USB. Una classe USB è specifica del dispositivo. Potrebbe essere necessaria una o più classi per la gestione di un dispositivo USB a seconda del numero di interfacce contenute nei descrittori di dispositivo USB.

Questo è un esempio della registrazione della classe HUB.

```c
status = ux_host_stack_class_register("ux_host_class_hub", ux_host_class_hub_entry);
```

La funzione ux_host_class_register ha il prototipo seguente.

```c
UINT ux_host_stack_class_register(
    UCHAR *class_name, 
    UINT (*class_entry_address) (struct UX_HOST_CLASS_COMMAND_STRUCT *));
```

- **class_name** è il nome della classe
- **class_entry_address** è il punto di ingresso della classe

Nell'esempio dell'inizializzazione della classe HUB:

- "ux_host_class_hub" è il nome della classe hub
- ux_host_class_hub_entry è il punto di ingresso della classe HUB.

## <a name="troubleshooting"></a>Risoluzione dei problemi

USBX viene fornito con un file dimostrativo e un ambiente di simulazione. È sempre una buona idea fare in modo che la piattaforma dimostrativa sia in esecuzione per prima, nell'hardware di destinazione o in una piattaforma dimostrativa specifica.

Se il sistema dimostrativo non funziona, provare a eseguire le operazioni seguenti per limitare il problema.

## <a name="usbx-version-id"></a>ID versione USBX

La versione corrente di USBX è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione. Il programmatore può ottenere la versione USBX dall'esame del file *** ux_port.h** _. Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software applicativo può ottenere la versione USBX esaminando la stringa globale *_ _ux_version_id_* _, definita in _*_ux_port.h_**.
