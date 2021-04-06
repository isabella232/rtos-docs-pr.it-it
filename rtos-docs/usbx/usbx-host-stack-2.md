---
title: Capitolo 2-installazione dello stack host di Azure RTO USBX
description: Informazioni su come installare lo stack host USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 4c33f95b8ac268c557fd947a1303ec3af315a37e
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377085"
---
# <a name="chapter-2---azure-rtos-usbx-host-stack-installation"></a>Capitolo 2-installazione dello stack host di Azure RTO USBX

## <a name="host-considerations"></a>Considerazioni sull'host

### <a name="computer-type"></a>Tipo computer

Lo sviluppo incorporato viene in genere eseguito nei computer host Windows o UNIX. Dopo che l'applicazione è stata compilata, collegata e posizionata nell'host, viene scaricata nell'hardware di destinazione per l'esecuzione.

### <a name="download-interfaces"></a>Interfacce di download

Il download di destinazione viene in genere eseguito tramite un'interfaccia seriale RS-232, sebbene le interfacce parallele, USB e Ethernet stiano diventando più diffuse. Per le opzioni disponibili, vedere la documentazione dello strumento di sviluppo.

### <a name="debugging-tools"></a>Strumenti di debug

Il debug viene eseguito in genere sullo stesso collegamento del download dell'immagine del programma. Sono disponibili diversi debugger, a partire da piccoli programmi di monitoraggio in esecuzione nella destinazione tramite il monitoraggio di debug in background (BDM) e gli strumenti di In-Circuit Emulator (ICE). Lo strumento ICE fornisce il debug più affidabile dell'hardware di destinazione effettivo.

### <a name="required-hard-disk-space"></a>Spazio su disco rigido richiesto

Il codice sorgente per USBX viene fornito in formato ASCII e richiede circa 500 KB di spazio sul disco rigido del computer host.

## <a name="target-considerations"></a>Considerazioni sulla destinazione

USBX richiede tra 24 KByte e 64 Kbyte di memoria di sola lettura (ROM) nella destinazione in modalità host. La quantità di memoria richiesta dipende dal tipo di controller usato e dalle classi USB collegate a USBX. Sono necessari altri 32 KByte della memoria ad accesso casuale (RAM) della destinazione per le strutture di dati globali USBX e il pool di memoria. È anche possibile modificare questo pool di memoria in base al numero previsto di dispositivi sul dispositivo USB e al tipo di controller USB. Il lato dispositivo USBX richiede circa 10-12 K di ROM a seconda del tipo di controller del dispositivo. L'utilizzo della memoria RAM dipende dal tipo di classe emulata dal dispositivo.

USBX si basa anche su semafori, mutex e thread ThreadX per la protezione di più thread e la sospensione di I/O e l'elaborazione periodica per il monitoraggio della topologia del bus USB.

### <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTO USBX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo <https://github.com/azure-rtos/usbx/> .

Di seguito è riportato un elenco di diversi file importanti nel repository:

- ***ux_api. h***: questo file di intestazione C contiene tutti gli equivalenti di sistema, le strutture di dati e i prototipi di servizio.
- ***ux_port. h***: questo file di intestazione C contiene tutte le definizioni e le strutture dei dati specifici dello strumento di sviluppo.
- ***UX. lib***: è la versione binaria della libreria C di USBX. Viene distribuito con il pacchetto standard.
- ***demo_usbx. c***: il file c contenente una demo USBX semplice

Tutti i nomi di file sono in lettere minuscole. Questa convenzione di denominazione rende più semplice convertire i comandi in piattaforme di sviluppo Unix.

## <a name="usbx-installation"></a>Installazione di USBX

USBX viene installato clonando il repository GitHub nel computer locale. Di seguito è riportata la sintassi tipica per la creazione di un clone del repository USBX nel PC:

```powershell
    git clone https://github.com/azure-rtos/usbx
```

In alternativa, è possibile scaricare una copia del repository usando il pulsante Download nella pagina principale di GitHub.

Sono inoltre disponibili istruzioni per la compilazione della libreria USBX nella pagina iniziale del repository online.

Le istruzioni generali riportate di seguito si applicano praticamente a qualsiasi installazione:

1. Usare la stessa directory in cui è stato precedentemente installato ThreadX nel disco rigido host. Tutti i nomi di USBX sono univoci e non interferiscono con l'installazione precedente di USBX.
2. Aggiungere una chiamata a ***ux_system_initialize** _ a o quasi all'inizio di _ *_tx_application_define_.* * Qui vengono inizializzate le risorse USBX.
3. Aggiungere una chiamata a ***ux_host_stack_initialize *.**
4. Aggiungere una o più chiamate per inizializzare il USBX richiesto.
5. Aggiungere una o più chiamate per inizializzare i controller host disponibili nel sistema.
6. Potrebbe essere necessario modificare il file tx_low_level_initialize. c per aggiungere l'inizializzazione hardware di basso livello e il routing vettoriale di interrupt. Questa operazione è specifica della piattaforma hardware e non verrà discussa qui.
7. Compilare il codice sorgente dell'applicazione e il collegamento con le librerie di runtime USBX e ThreadX (FileX e/o NETX potrebbero essere necessari anche se la classe di archiviazione USB e/o le classi di rete USB devono essere compilate in), UX. a (o UX. lib) e TX. a (o TX. lib). Il risultante può essere scaricato nella destinazione ed eseguito.

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la compilazione della libreria USBX. Tutte le opzioni si trovano in ***ux_user. h***.

Nell'elenco seguente vengono illustrate tutte le opzioni di configurazione.


- **UX_PERIODIC_RATE**: questo valore rappresenta il numero di cicli al secondo per una piattaforma hardware specifica. Il valore predefinito è 1000, che indica un segno di cicli per millisecondo.
- **UX_MAX_CLASS_DRIVER**: questo valore è il numero massimo di classi che possono essere caricate da USBX. Questo valore rappresenta il contenitore della classe e non il numero di istanze di una classe. Ad esempio, se una particolare implementazione di USBX necessita della classe Hub, della classe Printer e della classe di archiviazione, il valore di UX_MAX_CLASS_DRIVER può essere impostato su 3 indipendentemente dal numero di dispositivi che appartengono a tali classi.
- **UX_MAX_HCD**: questo valore rappresenta il numero di controller host diversi disponibili nel sistema. Per il supporto USB 1,1, questo valore sarà per lo più 1. Per il supporto USB 2,0, questo valore può essere maggiore di 1. Questo valore rappresenta il numero di controller host simultanei in esecuzione nello stesso momento. Se ad esempio sono presenti due istanze di OHCI in esecuzione o un EHCI e un controller OHCI in esecuzione, il UX_MAX_HCD deve essere impostato su 2. 
- **UX_MAX_DEVICES**: questo valore rappresenta il numero massimo di dispositivi che possono essere collegati al dispositivo USB. Normalmente, il numero massimo teorico su un singolo USB è 127 dispositivi. Per ridurre la memoria, questo valore può essere ridotto. Si noti che questo valore rappresenta il numero totale di dispositivi indipendentemente dal numero di bus USB nel sistema.
- **UX_MAX_ED**: questo valore rappresenta il numero massimo di EDS nel pool di controller. Questo numero viene assegnato solo a un controller. Se sono presenti più istanze di controller, questo valore viene usato da ogni singolo controller.
- **UX_MAX_TD e UX_MAX_ISO_TD**: questo valore rappresenta il numero massimo di TDS regolari e isocroni nel pool di controller. Questo numero viene assegnato solo a un controller. Se sono presenti più istanze di controller, questo valore viene usato da ogni singolo controller.
- **UX_THREAD_STACK_SIZE**: questo valore corrisponde alla dimensione dello stack in byte per i thread USBX. Può essere in genere 1024 byte o 2048 byte a seconda del processore usato e del controller host.
- **UX_HOST_ENUM_THREAD_STACK_SIZE**: questo valore corrisponde alla dimensione dello stack del thread di enumerazione host USB. Se il simbolo non è impostato, le dimensioni dello stack del thread di enumerazione dell'host USBX vengono impostate su **UX_THREAD_STACK_SIZE**. 
- **UX_HOST_HCD_THREAD_STACK_SIZE**: questo valore corrisponde alla dimensione dello stack del thread HCD dell'host USB. Se il simbolo non è impostato, le dimensioni dello stack dei thread HCD dell'host USBX sono impostate su **UX_THREAD_STACK_SIZE**.
- **UX_THREAD_PRIORITY_ENUM**: valore di priorità threadX per i thread di enumerazione USBX che monitora la topologia del bus.
- **UX_THREAD_PRIORITY_CLASS**: valore di priorità threadX per i thread USBX standard.
- **UX_THREAD_PRIORITY_KEYBOARD**: valore di priorità threadX per la classe della tastiera USBX HID.
- **UX_THREAD_PRIORITY_HCD**: valore di priorità threadX per il thread del controller host.
- **UX_NO_TIME_SLICE**: questo valore definisce effettivamente l'intervallo di tempo che verrà usato per i thread. Se, ad esempio, viene definito su 0, la porta di destinazione ThreadX non utilizza intervalli di tempo.
- **UX_MAX_HOST_LUN**: questo valore rappresenta il numero massimo di unità logiche SCSI rappresentate nel driver della classe di archiviazione host.
- **UX_HOST_CLASS_STORAGE_INCLUDE_LEGACY_PROTOCOL_SUPPORT**: se definito, questo valore include il codice per gestire i dispositivi di archiviazione che usano il protocollo CB o CBI, ad esempio i dischi floppy. È disattivata per impostazione predefinita perché questi protocolli sono obsoleti, sostituiti dal trasporto Bulk Only (il protocollo BOT, che praticamente tutti i dispositivi di archiviazione moderni usano).
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE**: se definito, questo valore causa ux_host_class_hid_keyboard_key_get solo le modifiche apportate alle chiavi, le pressioni di tasto e le versioni di chiave. Per impostazione predefinita, viene segnalato solo quando un tasto è inattivo.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_KEY_DOWN_ONLY**: utilizzato solo se viene definito **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** . Se definito, fa in modo che ux_host_class_hid_keyboard_key_get solo le modifiche alla pressione del tasto. le modifiche apportate/rilasciate della chiave non vengono segnalate.
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_LOCK_KEYS**: utilizzato solo se viene definito **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** . Se definito, causa ux_host_class_hid_keyboard_key_get le modifiche alla chiave di blocco (CapsLock/NumLock/ScrollLock).
- **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE_REPORT_MODIFIER_KEYS**: utilizzato solo se viene definito **UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE** . Se definito, fa sì che ux_host_class_hid_keyboard_key_get le modifiche del tasto di modifica (Ctrl/Alt/Shift/GUI).
- **UX_HOST_CLASS_CDC_ECM_NX_PKPOOL_ENTRIES**: se definito, questo valore rappresenta il numero di pacchetti nella classe host CDC-ECM. Il valore predefinito è 16.

## <a name="source-code-tree"></a>Albero del codice sorgente

I file USBX sono disponibili in più directory.

![Albero del codice sorgente](media/usbx-host-stack/source-code-tree.png)

Per rendere i file riconoscibili con i rispettivi nomi, è stata adottata la convenzione seguente:

| Nome suffisso file | Descrizione file                          |
| ---------------- | ----------------------------------------- |
| ux_host_stack    | USBX file core dello stack host                |
| ux_host_class    | file delle classi dello stack host USBX             |
| ux_hcd           | file driver del controller dello stack host USBX   |
| ux_device_stack  | file principali dello stack di dispositivi USBX              |
| ux_device_class  | file delle classi dello stack del dispositivo USBX           |
| ux_dcd           | file driver del controller dello stack del dispositivo USBX |
| ux_otg           | file correlati driver del controller USBX OTG  |
| ux_pictbridge    | file PictBridge USBX                     |
| ux_utility       | funzioni di utilità USBX                    |
| demo_usbx        | file dimostrativi per USBX              |

## <a name="initialization-of-usbx-resources"></a>Inizializzazione delle risorse di USBX

USBX dispone di un proprio gestore della memoria. La memoria deve essere allocata a USBX prima che il lato host o dispositivo di USBX venga inizializzato. Il gestore della memoria USBX può supportare i sistemi in cui è possibile memorizzare nella cache la memoria.

La funzione seguente inizializza le risorse di memoria USBX con 128 KB di memoria normale e nessun pool separato per la memoria sicura della cache:

```c
/* Initialize USBX Memory */

ux_system_initialize(memory_pointer,(128*1024),UX_NULL,0);
```

Il prototipo per la ux_system_initialize è il seguente.

```c
UINT ux_system_initialize( 
    VOID *regular_memory_pool_start,
    ULONG regular_memory_size,
    VOID *cache_safe_memory_pool_start,
    ULONG cache_safe_memory_size);
```

### <a name="input-parameters"></a>Parametri di input:

- **regular_memory_pool_start** Inizio del pool di memoria normale.
- **regular_memory_size** Dimensioni del pool di memoria normale.
- **cache_safe_memory_pool_start** Inizio del pool di memoria sicuro della cache.
- **cache_safe_memory_size** Dimensioni del pool di memoria sicuro della cache.    |

Non tutti i sistemi richiedono la definizione di memoria protetta dalla cache. In tale sistema, i valori passati durante l'inizializzazione per il puntatore di memoria verranno impostati su UX_NULL e le dimensioni del pool su 0. USBX utilizzerà quindi il normale pool di memoria anziché il pool di sicurezza della cache.

In un sistema in cui la memoria normale non è protetta dalla cache e un controller richiede l'esecuzione di memoria DMA (come OHCI, controller EHCI tra gli altri) è necessario definire un pool di memoria in un'area di sicurezza della cache.

## <a name="uninitialization-of-usbx-resources"></a>Inizializzazione delle risorse di USBX

USBX può essere terminato rilasciando le risorse. Prima di terminare il USBX, tutte le classi e le risorse del controller devono essere terminate correttamente. La funzione seguente consente di uninizializzare le risorse di memoria USBX:

```c
/* Unitialize USBX Resources */

ux_system_uninitialize();
```

Il prototipo per la ux_system_initialize è il seguente.

```c
UINT ux_system_uninitialize(VOID);
```

## <a name="definition-of-usb-host-controllers"></a>Definizione dei controller host USB

È necessario definire almeno un controller host USB per il funzionamento di USBX in modalità host. Il file di inizializzazione dell'applicazione deve contenere questa definizione. La riga seguente esegue la definizione di un controller host generico.

```c
ux_host_stack_hcd_register("ux_hcd_controller",
        ux_hcd_controller_initialize, 0xd0000, 0x0a);
```

Il ux_host_stack_hcd_register presenta il seguente prototipo.

```c
UINT ux_host_stack_hcd_register(
    UCHAR *hcd_name,
    UINT (*hcd_initialize_function)(struct UX_HCD_STRUCT *),
    ULONG hcd_param1, ULONG hcd_param2);
```

La funzione ux_host_stack_hcd_register presenta i parametri seguenti:

- **hcd_name**: stringa del nome del controller
- **hcd_initialize_function**: funzione di inizializzazione del controller
- **hcd_param1**: in genere il valore io o la memoria usata dal controller
- **hcd_param2**: in genere l'IRQ usato dal controller

Nell'esempio precedente:

- "ux_hcd_controller" è il nome del controller
- "ux_hcd_controller_initialize" è la routine di inizializzazione per il controller host
- 0xD0000 è l'indirizzo in cui i registri del controller host sono visibili in memoria
- e 0x0A è l'IRQ usato dal controller host.

Di seguito è riportato un esempio di inizializzazione di USBX in modalità host con un controller host e diverse classi.

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

## <a name="definition-of-host-classes"></a>Definizione delle classi host

È necessario definire una o più classi host con USBX. Una classe USB è necessaria per guidare un dispositivo USB dopo che lo stack USB ha configurato il dispositivo USB. Una classe USB è specifica del dispositivo. Una o più classi potrebbero essere necessarie per guidare un dispositivo USB a seconda del numero di interfacce contenute nei descrittori di dispositivo USB.

Questo è un esempio di registrazione della classe HUB.

```c
status = ux_host_stack_class_register("ux_host_class_hub", ux_host_class_hub_entry);
```

Il prototipo della funzione ux_host_class_register è il seguente.

```c
UINT ux_host_stack_class_register(
    UCHAR *class_name, 
    UINT (*class_entry_address) (struct UX_HOST_CLASS_COMMAND_STRUCT *));
```

- **class_name** è il nome della classe
- **class_entry_address** è il punto di ingresso della classe

Nell'esempio di inizializzazione della classe HUB:

- "ux_host_class_hub" è il nome della classe Hub
- ux_host_class_hub_entry è il punto di ingresso della classe HUB.

## <a name="troubleshooting"></a>Risoluzione dei problemi

USBX viene fornito con un file dimostrativo e un ambiente di simulazione. È sempre consigliabile ottenere prima di tutto la piattaforma dimostrativa, sia nell'hardware di destinazione che in una piattaforma dimostrativa specifica.

Se il sistema dimostrativo non funziona, provare a eseguire le operazioni seguenti per restringere il problema.

## <a name="usbx-version-id"></a>ID versione USBX

La versione corrente di USBX è disponibile sia per l'utente che per il software dell'applicazione in fase di esecuzione. Il programmatore può ottenere la versione di USBX dall'esame del file ***ux_port. h** _. Inoltre, questo file contiene anche una cronologia delle versioni della porta corrispondente. Il software applicativo può ottenere la versione di USBX esaminando la stringa globale _ *_ _ux_version_id_* _, definita in _ *_ux_port. h_* *.
