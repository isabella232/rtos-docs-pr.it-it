---
title: Capitolo 2 - Considerazioni sulla classe di dispositivi USBX
description: La classe RNDIS del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come dispositivo ethernet. Questa classe è basata sull'implementazione proprietaria di Microsoft ed è specifica per Windows piattaforme.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2a28196c8f0e29ad94ef9f2d65b143459bf0214f48c345e6bb0d4ea71d520dfd
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802625"
---
# <a name="chapter-2---usbx-device-class-considerations"></a>Capitolo 2 - Considerazioni sulla classe di dispositivi USBX

## <a name="usb-device-rndis-class"></a>Classe RNDIS del dispositivo USB

La classe RNDIS del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come dispositivo ethernet. Questa classe è basata sull'implementazione proprietaria di Microsoft ed è specifica per Windows piattaforme.

Un framework di dispositivo conforme a RNDIS deve essere dichiarato dallo stack di dispositivi. Di seguito è riportato un esempio.

```C
unsigned char device_framework_full_speed[] = {
    /* VID: 0x04b4
    PID: 0x1127
    */

    /* Device Descriptor */
    0x12, /* bLength */
    0x01, /* bDescriptorType */
    0x10, 0x01, /* bcdUSB */
    0x02, /* bDeviceClass - CDC */
    0x00, /* bDeviceSubClass */
    0x00, /* bDeviceProtocol */
    0x40, /* bMaxPacketSize0 */
    0xb4, 0x04, /* idVendor */
    0x27, 0x11, /* idProduct */
    0x00, 0x01, /* bcdDevice */
    0x01, /* iManufacturer */
    0x02, /* iProduct */
    0x03, /* iSerialNumber */
    0x01, /* bNumConfigurations */

    /* Configuration Descriptor */
    0x09, /* bLength */
    0x02, /* bDescriptorType */
    0x38, 0x00, /* wTotalLength */
    0x02, /* bNumInterfaces */
    0x01, /* bConfigurationValue */
    0x00, /* iConfiguration */
    0x40, /* bmAttributes - Self-powered */
    0x00, /* bMaxPower */

    /* Interface Association Descriptor */
    0x08, /* bLength */
    0x0b, /* bDescriptorType */
    0x00, /* bFirstInterface */
    0x02, /* bInterfaceCount */
    0x02, /* bFunctionClass - CDC - Communication */
    0xff, /* bFunctionSubClass - Vendor Defined – In this case, RNDIS */
    0x00, /* bFunctionProtocol - No class specific protocol required */
    0x00, /* iFunction */

    /* Interface Descriptor */
    0x09, /* bLength */
    0x04, /* bDescriptorType */
    0x00, /* bInterfaceNumber */
    0x00, /* bAlternateSetting */
    0x01, /* bNumEndpoints */
    0x02, /* bInterfaceClass - CDC - Communication */
    0xff, /* bInterfaceSubClass - Vendor Defined – In this case, RNDIS */
    0x00, /* bInterfaceProtocol - No class specific protocol required */
    0x00, /* iInterface */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x83, /* bEndpointAddress */
    0x03, /* bmAttributes - Interrupt */
    0x08, 0x00, /* wMaxPacketSize */
    0xff, /* bInterval */

    /* Interface Descriptor */
    0x09, /* bLength */
    0x04, /* bDescriptorType */
    0x01, /* bInterfaceNumber */
    0x00, /* bAlternateSetting */
    0x02, /* bNumEndpoints */
    0x0a, /* bInterfaceClass - CDC - Data */
    0x00, /* bInterfaceSubClass - Should be 0x00 */
    0x00, /* bInterfaceProtocol - No class specific protocol required */
    0x00, /* iInterface */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x02, /* bEndpointAddress */
    0x02, /* bmAttributes - Bulk */
    0x40, 0x00, /* wMaxPacketSize */
    0x00, /* bInterval */

    /* Endpoint Descriptor */
    0x07, /* bLength */
    0x05, /* bDescriptorType */
    0x81, /* bEndpointAddress */
    0x02, /* bmAttributes - Bulk */
    0x40, 0x00, /* wMaxPacketSize */
    0x00, /* bInterval */
};
```

La classe RNDIS usa un approccio descrittore di dispositivo molto simile a CDC-ACM e CDC-ECM e richiede anche un descrittore IAD. Vedere la classe CDC-ACM per la definizione e i requisiti per il descrittore del dispositivo.

L'attivazione della classe RNDIS è la seguente.

```C
/* Set the parameters for callback when insertion/extraction of a CDC device. Set to NULL.*/

parameter.ux_slave_class_rndis_instance_activate = UX_NULL;
parameter.ux_slave_class_rndis_instance_deactivate = UX_NULL;

/* Define a local NODE ID. */

parameter.ux_slave_class_rndis_parameter_local_node_id[0] = 0x00;
parameter.ux_slave_class_rndis_parameter_local_node_id[1] = 0x1e;
parameter.ux_slave_class_rndis_parameter_local_node_id[2] = 0x58;
parameter.ux_slave_class_rndis_parameter_local_node_id[3] = 0x41;
parameter.ux_slave_class_rndis_parameter_local_node_id[4] = 0xb8;
parameter.ux_slave_class_rndis_parameter_local_node_id[5] = 0x78;

/* Define a remote NODE ID. */

parameter.ux_slave_class_rndis_parameter_remote_node_id[0] = 0x00;
parameter.ux_slave_class_rndis_parameter_remote_node_id[1] = 0x1e;
parameter.ux_slave_class_rndis_parameter_remote_node_id[2] = 0x58;
parameter.ux_slave_class_rndis_parameter_remote_node_id[3] = 0x41;
parameter.ux_slave_class_rndis_parameter_remote_node_id[4] = 0xb8;
parameter.ux_slave_class_rndis_parameter_remote_node_id[5] = 0x79;

/* Set extra parameters used by the RNDIS query command with certain OIDs. */

parameter.ux_slave_class_rndis_parameter_vendor_id = 0x04b4 ;
parameter.ux_slave_class_rndis_parameter_driver_version = 0x1127;
ux_utility_memory_copy(parameter.ux_slave_class_rndis_parameter_vendor_description,
    "ELOGIC RNDIS", 12);

/* Initialize the device rndis class. This class owns both interfaces. */
status = ux_device_stack_class_register(_ux_system_slave_class_rndis_name,
    ux_device_class_rndis_entry, 1,0, &parameter);
```

Come per CDC-ECM, la classe RNDIS richiede 2 nodi, uno locale e uno remoto, ma non è necessario disporre di un descrittore di stringa che descrive il nodo remoto.

Tuttavia, a causa del meccanismo di messaggistica proprietario di Microsoft, sono necessari alcuni parametri aggiuntivi. Prima di tutto è necessario passare l'ID fornitore. Analogamente, la versione del driver di RNDIS. È necessario specificare anche una stringa del fornitore.

La classe RNDIS dispone di API incorporate per il trasferimento dei dati in entrambi i modi, ma sono nascoste all'applicazione perché l'applicazione utente comunicherà con il dispositivo USB Ethernet tramite NetX.

La classe USBX RNDIS è strettamente associata Azure RTOS stack di rete NetX. Un'applicazione che usa la classe RNDIS NetX e USBX attiverà lo stack di rete NetX nel modo consueto, ma deve anche attivare lo stack di rete USB come indicato di seguito.

```C
/* Initialize the NetX system. */

nx_system_initialize();

/* Perform the initialization of the network driver. This will initialize the USBX network layer.*/
ux_network_driver_init();
```

Lo stack di rete USB deve essere attivato una sola volta e non è specifico di RNDIS, ma è richiesto da qualsiasi classe USB che richiede servizi NetX.

La classe RNDIS non verrà riconosciuta dagli host MAC OS e Linux perché è specifica per i sistemi operativi Microsoft. Nelle piattaforme Windows un file inf deve essere presente nell'host che corrisponde al descrittore del dispositivo. Microsoft fornisce un modello per la classe RNDIS ed è disponibile nella directory usbx_windows_host_files. Per una versione più recente Windows usare il file RNDIS_Template.inf. Questo file deve essere modificato per riflettere il PID/VID usato dal dispositivo. Il PID/VID sarà specifico per il cliente finale quando l'azienda e il prodotto vengono registrati con USB-IF. Nel file inf i campi da modificare si trovano qui.

```Inf
[DeviceList]
%DeviceName%=DriverInstall, USB\\VID_xxxx&PID_yyyy&MI_00

[DeviceList.NTamd64]
%DeviceName%=DriverInstall, USB\\VID_xxxx&PID_yyyy&MI_00
```

Nel framework di dispositivo del dispositivo RNDIS, il PID/VID viene archiviato nel descrittore del dispositivo (vedere il descrittore del dispositivo dichiarato in precedenza)

Quando un sistema host USB individua il dispositivo RNDIS USB, monta un'interfaccia di rete e il dispositivo può essere usato con lo stack di protocolli di rete. Per informazioni di riferimento, vedere il sistema operativo host.

## <a name="usb-device-dfu-class"></a>Classe DFU del dispositivo USB

La classe DFU del dispositivo USB consente a un sistema host USB di aggiornare il firmware del dispositivo in base a un'applicazione host. La classe DFU è una classe standard USB-IF.

La classe USBX DFU è relativamente semplice. Il descrittore del dispositivo non richiede altro che un endpoint di controllo. Nella maggior parte dei casi, questa classe verrà incorporata in un dispositivo usb composito. Il dispositivo può essere qualsiasi elemento, ad esempio un dispositivo di archiviazione o un dispositivo comm e l'interfaccia DFU aggiunta può informare l'host che il dispositivo può avere il firmware aggiornato in tempo reale.

La classe DFU funziona in 3 passaggi. Prima il dispositivo viene montato normalmente usando la classe esportata. Un'applicazione nell'host (Windows o Linux) eserciterà la classe DFU e invierà una richiesta per reimpostare il dispositivo in modalità DFU. Il dispositivo scompare dal bus per un breve periodo di tempo (sufficiente perché l'host e il dispositivo rilevino una sequenza RESET) e al riavvio il dispositivo sarà esclusivamente in modalità DFU, in attesa che l'applicazione host invii un aggiornamento del firmware. Al termine dell'aggiornamento del firmware, l'applicazione host reimposta il dispositivo e al momento della nuova enumerazione il dispositivo ripristina il normale funzionamento con il nuovo firmware.

Un framework di dispositivi DFU sarà simile al seguente.

```C
UCHAR device_framework_full_speed[] = {

    /* Device descriptor */
    0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x40,
    0x99, 0x99, 0x00, 0x00, 0x00, 0x00, 0x01, 0x02,
    0x03, 0x01,

    /* Configuration descriptor */
    0x09, 0x02, 0x1b, 0x00, 0x01, 0x01, 0x00, 0xc0,
    0x32,

    /* Interface descriptor for DFU. */
    0x09, 0x04, 0x00, 0x00, 0x00, 0xFE, 0x01, 0x01, 0x00,

    /* Functional descriptor for DFU. */
    0x09, 0x21, 0x0f, 0xE8, 0x03, 0x40, 0x00, 0x00,
    0x01,

};
```

In questo esempio il descrittore DFU non è associato ad altre classi. Ha un descrittore di interfaccia semplice e nessun altro endpoint collegato. È disponibile un descrittore funzionale che descrive le specifiche delle funzionalità DFU del dispositivo.

La descrizione delle funzionalità DFU è la seguente.

| Nome             | Offset  | Dimensione | tipo      | Descrizione |
|------------------|----------|------|-----------|------------|
| bmAttributes  | 2     | 1   | Campo di bit | Bit 3: il dispositivo eseguirà una sequenza di collegamento del bus quando riceve una DFU_DETACH richiesta. L'host non deve emettere una reimpostazione USB. (bitWillDetach) 0 = no 1 = sì Bit 2: il dispositivo è in grado di comunicare tramite USB dopo la fase di manifestazione. (bitManifestationTolerant) 0 = no, deve vedere bus reset 1 = yes Bit 1: upload capable (bitCanUpload) 0 = no 1 = yes Bit 0: download capable (bitCanDnload) 0 = no 1 = yes  |
| wDetachTimeOut  | 3      | 2  | d'acquisto    | Tempo, in millisecondi, che il dispositivo attenderà dopo la ricezione della DFU_DETACH richiesta. Se questo tempo è trascorso senza una reimpostazione USB, il dispositivo terminerà la fase di riconfigurazione e tornerà al normale funzionamento. Rappresenta il tempo massimo di attesa del dispositivo (a seconda dei timer e così via). USBX imposta questo valore su 1000 ms.  |
| wTransferSize  | 5      | 2  | d'acquisto    | Numero massimo di byte che il dispositivo può accettare per ogni operazione di \- scrittura del controllo. USBX imposta questo valore su 64 byte. |

La dichiarazione della classe DFU è la seguente:

```C
/* Store the DFU parameters. */

dfu_parameter.ux_slave_class_dfu_parameter_instance_activate =
    tx_demo_thread_dfu_activate;

dfu_parameter.ux_slave_class_dfu_parameter_instance_deactivate =
    tx_demo_thread_dfu_deactivate;

dfu_parameter.ux_slave_class_dfu_parameter_read =
    tx_demo_thread_dfu_read;

dfu_parameter.ux_slave_class_dfu_parameter_write =
    tx_demo_thread_dfu_write;

dfu_parameter.ux_slave_class_dfu_parameter_get_status =
    tx_demo_thread_dfu_get_status;

dfu_parameter.ux_slave_class_dfu_parameter_notify =
    tx_demo_thread_dfu_notify;

dfu_parameter.ux_slave_class_dfu_parameter_framework =
    device_framework_dfu;

dfu_parameter.ux_slave_class_dfu_parameter_framework_length =
    DEVICE_FRAMEWORK_LENGTH_DFU;

/* Initialize the device dfu class. The class is connected with interface
1 on configuration 1. */
status = ux_device_stack_class_register(_ux_system_slave_class_dfu_name,
    ux_device_class_dfu_entry, 1, 0,
    (VOID *)&dfu_parameter);

if (status!=UX_SUCCESS) return;
```

La classe DFU deve funzionare con un'applicazione firmware del dispositivo specifica per la destinazione. Definisce quindi diversi blocchi di lettura e scrittura del firmware e per ottenere lo stato dall'applicazione di aggiornamento del firmware. La classe DFU include anche una funzione di callback notify per informare l'applicazione quando si verifica un inizio e una fine del trasferimento del firmware.

Di seguito è riportata la descrizione di un tipico flusso di applicazioni DFU.

![Flusso dell'applicazione DFU](./media/usbx-device-stack-supplemental/dfu-application-flow.png)

La sfida principale della classe DFU è ottenere l'applicazione giusta nell'host per eseguire il download del firmware. Non è disponibile alcuna applicazione fornita da Microsoft o USB-IF. Alcuni shareware esistono e funzionano ragionevolmente bene in Linux e in misura minore Windows.

In Linux è possibile usare dfu-utils per trovare qui: Molte informazioni sulle dfu utils sono disponibili anche [https://wiki.openmoko.org/wiki/Dfu-util](https://wiki.openmoko.org/wiki/Dfu-util) in questo collegamento: [https://www.libusb.org/wiki/windows_backend](https://www.libusb.org/wiki/windows_backend)

L'implementazione Linux di DFU esegue correttamente la sequenza di reimpostazione tra l'host e il dispositivo e pertanto il dispositivo non deve eseguire questa operazione. Linux può accettare che *bitWillDetach* di bmAttributes sia 0. Windows sul lato opposto è necessario che il dispositivo eseere la reimpostazione.

In Windows, il registro USB deve essere in grado di associare il dispositivo USB al relativo PID/VID e alla libreria USB che verrà a sua volta usata dall'applicazione DFU. Questa operazione può essere eseguita facilmente con l'utilità gratuita Zadig, disponibile qui: [https://sourceforge.net/projects/libwdi/files/zadig/](https://sourceforge.net/projects/libwdi/files/zadig/) .

Eseguendo Zadig per la prima volta verrà visualizzata questa schermata:

![Esecuzione di Zadig per la prima volta](./media/usbx-device-stack-supplemental/zadig.png)

Nell'elenco dei dispositivi individuare il dispositivo e associarlo al driver libusb windows. In questo modo il PID/VID del dispositivo verrà associato alla Windows USB usata dalle utilità DFU.

Per usare il comando DFU, è sufficiente decomprimere le utilità dfu compresse in una directory, verificando che anche la dll libusb sia presente nella stessa directory. Le utilità DFU devono essere eseguite da una casella DOS nella riga di comando.

Per prima cosa, digitare **il comando dfu-util –l** per determinare se il dispositivo è elencato. In caso contrario, eseguire Zadig per assicurarsi che il dispositivo sia elencato e associato alla libreria USB. Verrà visualizzata una schermata come segue:

```Command-line
C:\usb specs\DFU\dfu-util-0.6&gt;dfu-util -l dfu-util 0.6

Copyright 2005-2008 Weston Schmidt, Harald Welte and OpenMoko Inc.
Copyright 2010-2012 Tormod Volden and Stefan Schmidt
This program is Free Software and has ABSOLUTELY NO WARRANTY
Found Runtime: [0a5c:21bc] devnum=0, cfg=1, intf=3, alt=0, name="UNDEFINED"
```

Il passaggio successivo consiste nel preparare il file da scaricare. La classe USBX DFU non esegue alcuna verifica su questo file ed è indipendente dal formato interno. Questo file del firmware è molto specifico per la destinazione, ma non per DFU né per USBX.

È quindi possibile indicare a dfu-util di inviare il file digitando il comando seguente:

```Command-line
dfu-util –R –t 64 -D file_to_download.hex
```

Dfu-util dovrebbe visualizzare il processo di download dei file fino a quando il firmware non è stato scaricato completamente.

## <a name="usb-device-pima-class-ptp-responder"></a>Classe USB Device PIMA (PTP Responder)

La classe PIMA del dispositivo USB consente a un sistema host USB (Iniziatore) di connettersi a un

Dispositivo PIMA (Resonder) per trasferire file multimediali. La classe USBX Pima è conforme alla classe USB-IF PIMA 15740 nota anche come classe PTP (per Picture Transfer Protocol).

La classe PIMA sul lato dispositivo USBX supporta le operazioni seguenti.

| Codice dell'operazione                                    | Valore | Descrizione                       |
|---------------------------------------------------|---------|-----------------------------------------------------|
| UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO    | 0x1001  | Ottenere le operazioni e gli eventi supportati dal dispositivo                                                         |
| UX_DEVICE_CLASS_PIMA_OC_OPEN_SESSION        | 0x1002  | Aprire una sessione tra l'host e il dispositivo                                                            |
| UX_DEVICE_CLASS_PIMA_OC_CLOSE_SESSION       | 0x1003  | Chiudere una sessione tra l'host e il dispositivo                                                           |
| UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_IDS    | 0x1004  | Restituisce l'ID di archiviazione per il dispositivo. USBX PIMA usa un solo ID di archiviazione |
| UX_DEVICE_CLASS_PIMA_OC_GET_STORAGE_INFO   | 0x1005  | Restituire informazioni sull'oggetto di archiviazione, ad esempio capacità massima e spazio disponibile                           |
| UX_DEVICE_CLASS_PIMA_OC_GET_NUM_OBJECTS    | 0x1006  | Restituisce il numero di oggetti contenuti nel dispositivo di archiviazione                                              |
| UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_HANDLES | 0x1007  | Restituisce una matrice di handle degli oggetti nel dispositivo di archiviazione                                           |
| UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT_INFO    | 0x1008  | Restituisce informazioni su un oggetto, ad esempio il nome dell'oggetto, la data di creazione, la data di modifica |
| UX_DEVICE_CLASS_PIMA_OC_GET_OBJECT          | 0x1009  | Restituire i dati relativi a un oggetto specifico                                                         |
| UX_DEVICE_CLASS_PIMA_OC_GET_THUMB           | 0x100A  | Inviare l'anteprima, se disponibile, su un oggetto                                                           |
| UX_DEVICE_CLASS_PIMA_OC_DELETE_OBJECT       | 0x100B  | Eliminare un oggetto nel supporto                                                                             |
| UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT_INFO   | 0x100C  | Inviare al dispositivo informazioni su un oggetto per la creazione nel supporto                              |
| UX_DEVICE_CLASS_PIMA_OC_SEND_OBJECT         | 0x100D  | Inviare i dati per un oggetto al dispositivo                                                                     |
| UX_DEVICE_CLASS_PIMA_OC_FORMAT_STORE        | 0x100F  | Pulire il supporto del dispositivo                                                                                    |
| UX_DEVICE_CLASS_PIMA_OC_RESET_DEVICE        | 0x0110  | Reimpostare il dispositivo di destinazione                                                                                   |

| Codice operazione                                         | Valore | Descrizione |
|--------------------------------------------------------|-------|-----------------------------------------|
| UX_DEVICE_CLASS_PIMA_EC_CANCEL_TRANSACTION       | 0x4001  | Annulla la transazione corrente                                                 |
| UX_DEVICE_CLASS_PIMA_EC_OBJECT_ADDED             | 0x4002  | Un oggetto è stato aggiunto al supporto del dispositivo e può essere recuperato dall'host. |
| UX_DEVICE_CLASS_PIMA_EC_OBJECT_REMOVED           | 0x4003  | Un oggetto è stato eliminato dal supporto del dispositivo                                |
| UX_DEVICE_CLASS_PIMA_EC_STORE_ADDED              | 0x4004  | È stato aggiunto un supporto al dispositivo                                            |
| UX_DEVICE_CLASS_PIMA_EC_STORE_REMOVED            | 0x4005  | Un supporto è stato eliminato dal dispositivo                                        |
| UX_DEVICE_CLASS_PIMA_EC_DEVICE_PROP_CHANGED     | 0x4006  | Le proprietà del dispositivo sono state modificate                                                  |
| UX_DEVICE_CLASS_PIMA_EC_OBJECT_INFO_CHANGED     | 0x4007  | Le informazioni sull'oggetto sono state modificate                                               |
| UX_DEVICE_CLASS_PIMA_EC_DEVICE_INFO_CHANGE      | 0x4008  | Un dispositivo è stato modificato                                                            |
| UX_DEVICE_CLASS_PIMA_EC_REQUEST_OBJECT_TRANSFER | 0x4009  | Il dispositivo richiede il trasferimento di un oggetto dall'host                     |
| UX_DEVICE_CLASS_PIMA_EC_STORE_FULL               | 0x400A  | Il dispositivo segnala che il supporto è pieno                                                |
| UX_DEVICE_CLASS_PIMA_EC_DEVICE_RESET             | 0x400B  | Il dispositivo segnala che è stato reimpostato                                                     |
| UX_DEVICE_CLASS_PIMA_EC_STORAGE_INFO_CHANGED    | 0x400C  | Archiviazione le informazioni sul dispositivo sono state modificate                                   |
| UX_DEVICE_CLASS_PIMA_EC_CAPTURE_COMPLETE         | 0x400D  | Acquisizione completata                                                            |

La classe di dispositivo USBX PIMA usa un thread TX per restare in ascolto dei comandi PIMA dall'host.

Un comando PIMA è costituito da un blocco di comandi, un blocco di dati e una fase di stato.

La funzione ux_device_class_pima_thread invia una richiesta nello stack per ricevere un comando PIMA dal lato host. Il comando PIMA viene decodificato e verificato per il contenuto. Se il blocco di comandi è valido, viene diramato al gestore comandi appropriato.

La maggior parte dei comandi PIMA può essere eseguita solo quando una sessione è stata aperta dall'host. L'unica eccezione è il comando **UX_DEVICE_CLASS_PIMA_OC_GET_DEVICE_INFO**. Con l'implementazione di USBX PIMA, è possibile aprire una sola sessione tra un iniziatore e un risponditore in qualsiasi momento. Tutte le transazioni all'interno della singola sessione sono bloccanti e nessuna nuova transazione può iniziare prima del completamento della precedente.

Le transazioni PIMA sono costituite da 3 fasi, una fase di comando, una fase dati facoltativa e una fase di risposta. Se è presente una fase dati, può essere solo in una direzione.

L'iniziatore determina sempre il flusso delle operazioni PIMA, ma il risponditore può avviare di nuovo gli eventi all'iniziatore per informare le modifiche dello stato che si sono verificate durante una sessione.

Il diagramma seguente illustra il trasferimento di un oggetto dati tra l'host e la classe di dispositivo PIMA.

![Transazioni PIMA](./media/usbx-device-stack-supplemental/pima-transactions.png)

## <a name="initialization-of-the-pima-device-class"></a>Inizializzazione della classe di dispositivo PIMA

La classe di dispositivo PIMA richiede alcuni parametri forniti dall'applicazione durante l'inizializzazione.

I parametri seguenti descrivono le informazioni sul dispositivo e sull'archiviazione.

- `ux_device_class_pima_manufacturer`
- `ux_device_class_pima_model`
- `ux_device_class_pima_device_version`
- `ux_device_class_pima_serial_number`
- `ux_device_class_pima_storage_id`
- `ux_device_class_pima_storage_type`
- `ux_device_class_pima_storage_file_system_type`
- `ux_device_class_pima_storage_access_capability`
- `ux_device_class_pima_storage_max_capacity_low`
- `ux_device_class_pima_storage_max_capacity_high`
- `ux_device_class_pima_storage_free_space_low`
- `ux_device_class_pima_storage_free_space_high`
- `ux_device_class_pima_storage_free_space_image`
- `ux_device_class_pima_storage_description`
- `ux_device_class_pima_storage_volume_label`

La classe PIMA richiede anche la registrazione del callback nell'applicazione per informare l'applicazione di determinati eventi o recuperare/archiviare dati da/verso i supporti locali. I callback sono i seguenti.

- `ux_device_class_pima_object_number_get`
- `ux_device_class_pima_object_handles_get`
- `ux_device_class_pima_object_info_get`
- `ux_device_class_pima_object_data_get`
- `ux_device_class_pima_object_info_send`
- `ux_device_class_pima_object_data_send`
- `ux_device_class_pima_object_delete`

Nell'esempio seguente viene illustrato come inizializzare il lato client di PIMA. Questo esempio usa Pictbridge come client per PIMA.

```C
/* Initialize the first XML object valid in the pictbridge instance.

Initialize the handle, type and file name.

The storage handle and the object handle have a fixed value of 1 in our implementation. */

object_info = pictbridge -> ux_pictbridge_object_client;

object_info -> ux_device_class_pima_object_format = UX_DEVICE_CLASS_PIMA_OFC_SCRIPT;
object_info -> ux_device_class_pima_object_storage_id = 1;
object_info -> ux_device_class_pima_object_handle_id = 2;

ux_utility_string_to_unicode(_ux_pictbridge_ddiscovery_name,
    object_info -> ux_device_class_pima_object_filename);

/* Initialize the head and tail of the notification round robin buffers.
   At first, the head and tail are pointing to the beginning of the array.
*/

pictbridge -> ux_pictbridge_event_array_head =
    pictbridge -> ux_pictbridge_event_array;

pictbridge -> ux_pictbridge_event_array_tail =
    pictbridge -> ux_pictbridge_event_array;

pictbridge -> ux_pictbridge_event_array_end =
    pictbridge -> ux_pictbridge_event_array +
    UX_PICTBRIDGE_MAX_EVENT_NUMBER;

/* Initialialize the pima device parameter. */
pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_manufacturer =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_model =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_serial_number =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_id = 1;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_type =
    UX_DEVICE_CLASS_PIMA_STC_FIXED_RAM;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_file_system_type =
    UX_DEVICE_CLASS_PIMA_FSTC_GENERIC_FLAT;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_access_capability =
    UX_DEVICE_CLASS_PIMA_AC_READ_WRITE;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_max_capacity_low =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_storage_size;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_max_capacity_high = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_low =
    pictbridge -> ux_pictbridge_dpslocal.ux_pictbridge_devinfo_storage_size;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_high = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_free_space_image = 0;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_description =
    _ux_pictbridge_volume_description;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_storage_volume_label =
    _ux_pictbridge_volume_label;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_number_get =
    ux_pictbridge_dpsclient_object_number_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_handles_get =
    ux_pictbridge_dpsclient_object_handles_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_info_get =
    ux_pictbridge_dpsclient_object_info_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_data_get =
    ux_pictbridge_dpsclient_object_data_get;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_info_send =
    ux_pictbridge_dpsclient_object_info_send;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_data_send =
    ux_pictbridge_dpsclient_object_data_send;

pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_object_delete =
    ux_pictbridge_dpsclient_object_delete;

/* Store the instance owner. */
pictbridge -> ux_pictbridge_pima_parameter.ux_device_class_pima_parameter_application =
    (VOID *) pictbridge;

/* Initialize the device pima class. The class is connected with interface 0 */

status = ux_device_stack_class_register(_ux_system_slave_class_pima_name,
    ux_device_class_pima_entry, 1, 0, (VOID *)&pictbridge -> ux_pictbridge_pima_parameter);

/* Check status. */
if (status != UX_SUCCESS)
```

## <a name="ux_device_class_pima_object_add"></a>ux_device_class_pima_object_add

Aggiunta di un oggetto e invio dell'evento all'host

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_pima_object_add(
    UX_SLAVE_CLASS_PIMA *pima, 
    ULONG object_handle);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando la classe PIMA deve aggiungere un oggetto e informare l'host.

### <a name="parameters"></a>Parametri

- **pima:** puntatore all'istanza della classe pima
- **object_handle**: handle dell'oggetto.

### <a name="example"></a>Esempio

```C
/* Send the notification to the host that an object has been added. */

status = ux_device_class_pima_object_add(pima, UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST);
```

## <a name="ux_device_class_pima_object_number_get"></a>ux_device_class_pima_object_number_get

Recupero del numero di oggetto dall'applicazione

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_pima_object_number_get(
    UX_SLAVE_CLASS_PIMA *pima, 
    ULONG *object_number);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando la classe PIMA deve recuperare il numero di oggetti nel sistema locale e inviarlo all'host.

### <a name="parameters"></a>Parametri

- **pima:** puntatore all'istanza della classe pima
- **object_number**: indirizzo del numero di oggetti da restituire

### <a name="example"></a>Esempio

```C
UINT ux_pictbridge_dpsclient_object_number_get(UX_SLAVE_CLASS_PIMA *pima, ULONG *number_objects)
{
    /* We force the number of objects to be 1 only here. This will be the XML scripts. */
    *number_objects = 1;
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_handles_get"></a>ux_device_class_pima_object_handles_get

Restituire la matrice di handle di oggetto

### <a name="prototype"></a>Prototipo

```C
UINT **ux_device_class_pima_object_handles_get**(
    UX_SLAVE_CLASS_PIMA_STRUCT *pima,
    ULONG object_handles_format_code,
    ULONG object_handles_association,
    ULONG *object_handles_array,
    ULONG object_handles_max_number);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando la classe PIMA deve recuperare la matrice di handle di oggetto nel sistema locale e inviarla nuovamente all'host.

### <a name="parameters"></a>Parametri

- **pima:** puntatore all'istanza della classe pima.
- **object_handles_format_code:** formattare il codice per gli handle
- **object_handles_association:** codice di associazione di oggetti
- **object_handle_array**: Indirizzo in cui archiviare gli handle
- **object_handles_max_number:** numero massimo di handle nella matrice

### <a name="example"></a>Esempio

```C
UINT ux_pictbridge_dpsclient_object_handles_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handles_format_code,
    ULONG object_handles_association,
    ULONG *object_handles_array,
    ULONG object_handles_max_number)
{

    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *) pima -> ux_device_class_pima_application;

    /* Set the pima pointer to the pictbridge instance. */
    pictbridge -> ux_pictbridge_pima = (VOID *) pima;

    /* We say we have one object but the caller might specify different format code and associations. */
    object_info = pictbridge -> ux_pictbridge_object_client;

    /* Insert in the array the number of found handles so far: 0. */
    ux_utility_long_put((UCHAR *)object_handles_array, 0);

    /* Check the type demanded. */

    if (object_handles_format_code == 0 || object_handles_format_code ==
        0xFFFFFFFF || object_info -> ux_device_class_pima_object_format ==
        object_handles_format_code)
    {
        /* Insert in the array the number of found handles. This handle is for the client XML script. */
        ux_utility_long_put((UCHAR *)object_handles_array, 1);

        /* Adjust the array to point after the number of elements. */
        object_handles_array++;

        /* We have a candicate. Store the handle. */
        ux_utility_long_put((UCHAR *)object_handles_array, object_info ->
            ux_device_class_pima_object_handle_id);
    }

    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_info_get"></a>ux_device_class_pima_object_info_get

Restituire le informazioni sull'oggetto

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_pima_object_info_get(
    struct UX_SLAVE_CLASS_PIMA_STRUCT *pima,
    ULONG object_handle, 
    UX_SLAVE_CLASS_PIMA_OBJECT **object);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando la classe PIMA deve recuperare la matrice di handle di oggetto nel sistema locale e inviarla nuovamente all'host.

### <a name="parameters"></a>Parametri

- **pima:** puntatore all'istanza della classe pima.
- **object_handles**: Handle dell'oggetto
- **object**: indirizzo del puntatore all'oggetto

### <a name="example"></a>Esempio

```C
UINT ux_pictbridge_dpsclient_object_info_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, UX_SLAVE_CLASS_PIMA_OBJECT **object)
{
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Check the object handle. If this is handle 1 or 2 , we need to return the XML script object.
       If the handle is not 1 or 2, this is a JPEG picture or other object to be printed. */
    if ((object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE) ||
        (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST)) {

        /* Check what XML object is requested. It is either a request script or a response. */
        if (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE)
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge -> ux_pictbridge_object_host;
        else
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_client;
    } else
        /* Get the object info from the job info structure. */
        object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
            ux_pictbridge_jobinfo.ux_pictbridge_jobinfo_object;
    /* Return the pointer to this object. */
    *object = object_info;

    /* We are done. */
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_data_get"></a>ux_device_class_pima_object_data_get

Restituire i dati dell'oggetto

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_pima_object_info_get(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length_requested,
    ULONG *object_actual_length);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando la classe PIMA deve recuperare i dati dell'oggetto nel sistema locale e inviarli all'host.

### <a name="parameters"></a>Parametri

- **pima:** puntatore all'istanza della classe pima.
- **object_handle**: Handle dell'oggetto
- **object_buffer:** indirizzo del buffer di oggetti
- **object_length_requested:** lunghezza dei dati dell'oggetto richiesta dal client all'applicazione
- **object_actual_length:** lunghezza dei dati dell'oggetto restituita dall'applicazione

### <a name="example"></a>Esempio

```C
UINT ux_pictbridge_dpsclient_object_data_get(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, UCHAR *object_buffer, ULONG object_offset,
    ULONG object_length_requested, ULONG *object_actual_length)
{

    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    UCHAR *pima_object_buffer;
    ULONG actual_length;
    UINT status;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Check the object handle. If this is handle 1 or 2 , we need to return the XML script object.
       If the handle is not 1 or 2, this is a JPEG picture or other object to be printed. */
    if ((object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE) ||
        (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_CLIENT_REQUEST))
    {
        /* Check what XML object is requested. It is either a request script or a response. */
        if (object_handle == UX_PICTBRIDGE_OBJECT_HANDLE_HOST_RESPONSE)
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_host;
        else
            object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
                ux_pictbridge_object_client;

       /* Is this the corrent handle ? */
       if (object_info -> ux_device_class_pima_object_handle_id == object_handle)
       {
           /* Get the pointer to the object buffer. */
           pima_object_buffer = object_info -> ux_device_class_pima_object_buffer;

           /* Copy the demanded object data portion. */
           ux_utility_memory_copy(object_buffer, pima_object_buffer +
               object_offset, object_length_requested);

           /* Update the length requested. for a demo, we do not do any checking. */
           *object_actual_length = object_length_requested;

           /* What cycle are we in ? */
           if (pictbridge -> ux_pictbridge_host_client_state_machine &
               UX_PICTBRIDGE_STATE_MACHINE_HOST_REQUEST)
            {
                /* Check if we are blocking for a client request. */
                if (pictbridge -> ux_pictbridge_host_client_state_machine &
                    UX_PICTBRIDGE_STATE_MACHINE_CLIENT_REQUEST_PENDING)

                    /* Yes we are pending, send an event to release the pending request. */
                    ux_utility_event_flags_set(&pictbridge ->
                        ux_pictbridge_event_flags_group,
                        UX_PICTBRIDGE_EVENT_FLAG_STATE_MACHINE_READY, TX_OR);

               /* Since we are in host request, this indicates we are done with the cycle. */
               pictbridge -> ux_pictbridge_host_client_state_machine =
                   UX_PICTBRIDGE_STATE_MACHINE_IDLE;

            }

            /* We have copied the requested data. Return OK. */
            return(UX_SUCCESS);

        }
    }
    else
    {

        /* Get the object info from the job info structure. */
        object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
            ux_pictbridge_jobinfo.ux_pictbridge_jobinfo_object;

        /* Obtain the data from the application jobinfo callback. */
        status = pictbridge -> ux_pictbridge_jobinfo.
            ux_pictbridge_jobinfo_object_data_read(pictbridge, object_buffer, object_offset,
            object_length_requested, &actual_length);

        /* Save the length returned. */
        *object_actual_length = actual_length;

        /* Return the application status. */
        return(status);

    }

    /* Could not find the handle. */

    return(UX_DEVICE_CLASS_PIMA_RC_INVALID_OBJECT_HANDLE);
}
```

## <a name="ux_device_class_pima_object_info_send"></a>ux_device_class_pima_object_info_send

L'host invia le informazioni sull'oggetto

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_pima_object_info_send(
    UX_SLAVE_CLASS_PIMA *pima,
    UX_SLAVE_CLASS_PIMA_OBJECT *object, 
    ULONG *object_handle);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando la classe PIMA deve ricevere le informazioni sull'oggetto nel sistema locale per l'archiviazione futura.

### <a name="parameters"></a>Parametri

- **pima:** puntatore all'istanza della classe pima
- **object**: puntatore all'oggetto
- **object_handle**: Handle dell'oggetto

### <a name="example"></a>Esempio

```C
UINT ux_pictbridge_dpsclient_object_info_send(UX_SLAVE_CLASS_PIMA *pima,
    UX_SLAVE_CLASS_PIMA_OBJECT *object, ULONG *object_handle)
{
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info; UCHAR
    string_discovery_name[UX_PICTBRIDGE_MAX_FILE_NAME_SIZE];

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* We only have one object. */
    object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
        ux_pictbridge_object_host;

    /* Copy the demanded object info set. */
    ux_utility_memory_copy(object_info, object,
        UX_SLAVE_CLASS_PIMA_OBJECT_DATA_LENGTH);

    /* Store the object handle. In Pictbridge we only receive XML scripts so the handle is hardwired to 1. */
    object_info -> ux_device_class_pima_object_handle_id = 1;
    *object_handle = 1;

    /* Check state machine. If we are in discovery pending mode, check file name of this object. */
    if (pictbridge -> ux_pictbridge_discovery_state ==
        UX_PICTBRIDGE_DPSCLIENT_DISCOVERY_PENDING)
    {
        /* We are in the discovery mode. Check for file name. It must match
           HDISCVRY.DPS in Unicode mode. */

        /* Check if this is a script. */
        if (object_info -> ux_device_class_pima_object_format ==
            UX_DEVICE_CLASS_PIMA_OFC_SCRIPT)
        {

            /* Yes this is a script. We need to search for the HDISCVRY.DPS file name. Get the file name in a ascii format. */
            ux_utility_unicode_to_string(object_info ->
                ux_device_class_pima_object_filename,
                string_discovery_name);

            /* Now, compare it to the HDISCVRY.DPS file name. Check length first. */
            if (ux_utility_string_length_get(_ux_pictbridge_hdiscovery_name)
                == ux_utility_string_length_get(string_discovery_name))
            {

                /* So far, the length of name of the files are the same. Compare names now. */
                if(ux_utility_memory_compare(_ux_pictbridge_hdiscovery_name,
                    string_discovery_name,
                    ux_utility_string_length_get(string_discovery_name)) == UX_SUCCESS)
                {
                    /* We are done with discovery of the printer. We can now send notifications when the camera wants to print an object. */
                    pictbridge -> ux_pictbridge_discovery_state =
                        UX_PICTBRIDGE_DPSCLIENT_DISCOVERY_COMPLETE;

                    /* Set an event flag if the application is listening. */
                    ux_utility_event_flags_set(&pictbridge ->
                        ux_pictbridge_event_flags_group,
                        UX_PICTBRIDGE_EVENT_FLAG_DISCOVERY, TX_OR);

                    /* There is no object during th discovery cycle. */
                    return(UX_SUCCESS);
                }
            }
        }
    }
    /* What cycle are we in ? */
    if (pictbridge -> ux_pictbridge_host_client_state_machine ==
        UX_PICTBRIDGE_STATE_MACHINE_IDLE)

        /* Since we are in idle state, we must have received a request from the host. */
        pictbridge -> ux_pictbridge_host_client_state_machine =
            UX_PICTBRIDGE_STATE_MACHINE_HOST_REQUEST;

    /* We have copied the requested data. Return OK. */
    return(UX_SUCCESS);
}
```

## <a name="ux_device_class_pima_object_data_send"></a>ux_device_class_pima_object_data_send

L'host invia i dati dell'oggetto

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_pima_object_data_send(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle, 
    ULONG phase, 
    UCHAR *object_buffer,
    ULONG object_offset, 
    ULONG object_length);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando la classe PIMA deve ricevere i dati dell'oggetto nel sistema locale per l'archiviazione.

### <a name="parameters"></a>Parametri

- **pima:** puntatore all'istanza della classe pima
- **object_handle**: Handle dell'oggetto
- **fase:** fase del trasferimento (attiva o completa)
- **object_buffer:** indirizzo del buffer di oggetti
- **object_offset**: Indirizzo dei dati
- **object_length:** lunghezza dei dati degli oggetti inviati dall'applicazione

### <a name="example"></a>Esempio

```C
UINT ux_pictbridge_dpsclient_object_data_send(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle,
    ULONG phase,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length)
{
    UINT status;
    UX_PICTBRIDGE *pictbridge;
    UX_SLAVE_CLASS_PIMA_OBJECT *object_info;
    ULONG event_flag;
    UCHAR *pima_object_buffer;

    /* Get the pointer to the Pictbridge instance. */
    pictbridge = (UX_PICTBRIDGE *)pima -> ux_device_class_pima_application;

    /* Get the pointer to the pima object. */
    object_info = (UX_SLAVE_CLASS_PIMA_OBJECT *) pictbridge ->
        ux_pictbridge_object_host;

    /* Is this the corrent handle ? */
    if (object_info -> ux_device_class_pima_object_handle_id == object_handle)
    {
        /* Get the pointer to the object buffer. */
        pima_object_buffer = object_info ->
            ux_device_class_pima_object_buffer;

        /* Check the phase. We should wait for the object to be completed and the response sent back before parsing the object. */
        if (phase == UX_DEVICE_CLASS_PIMA_OBJECT_TRANSFER_PHASE_ACTIVE)
        {
            /* Copy the demanded object data portion. */
            ux_utility_memory_copy(pima_object_buffer + object_offset,
                object_buffer, object_length);

            /* Save the length of this object. */
            object_info -> ux_device_class_pima_object_length = object_length;

            /* We are not done yet. */
            return(UX_SUCCESS);
        }
        else
        {
            /* Completion of transfer. We are done. */
            return(UX_SUCCESS);
        }
    }
}
```

## <a name="ux_device_class_pima_object_delete"></a>ux_device_class_pima_object_delete

Eliminare un oggetto locale

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_pima_object_delete(
    UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando la classe PIMA deve eliminare un oggetto nell'archiviazione locale.

### <a name="parameters"></a>Parametri

- **pima:** puntatore all'istanza della classe pima
- **object_handle**: Handle dell'oggetto

### <a name="example"></a>Esempio

```C
UINT ux_pictbridge_dpsclient_object_delete(UX_SLAVE_CLASS_PIMA *pima,
    ULONG object_handle)
{
    /* Delete the object pointer by the handle. */

}
```

## <a name="usb-device-audio-class"></a>Classe audio del dispositivo USB

La classe Audio del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come dispositivo audio. Questa classe è basata sullo standard USB e sullo standard USB Audio Class 1.0 o 2.0.

Un framework di dispositivo conforme all'audio USB deve essere dichiarato dallo stack di dispositivi. Di seguito è riportato un esempio di altoparlante Audio 2.0:

```C
unsigned char device_framework_high_speed[] = {

    /* --- Device Descriptor 18 bytes
    0x00 bDeviceClass: Refer to interface
    0x00 bDeviceSubclass: Refer to interface
    0x00 bDeviceProtocol: Refer to interface

    idVendor & idProduct - https://www.linux-usb.org/usb.ids
    */

    /* 0 bLength, bDescriptorType */ 18, 0x01,
    /* 2 bcdUSB : 0x200 (2.00) */ 0x00, 0x02,
    /* 4 bDeviceClass : 0x00 (see interface) */ 0x00,
    /* 5 bDeviceSubClass : 0x00 (see interface) */ 0x00,
    /* 6 bDeviceProtocol : 0x00 (see interface) */ 0x00,
    /* 7 bMaxPacketSize0 */ 0x08,
    /* 8 idVendor, idProduct */ 0x84, 0x84, 0x03, 0x00,
    /* 12 bcdDevice */ 0x00, 0x02,
    /* 14 iManufacturer, iProduct, iSerialNumber */ 0, 0, 0,
    /* 17 bNumConfigurations */ 1,
    /* ---------------- Device Qualifier Descriptor */
    /* 0 bLength, bDescriptorType */ 10, 0x06,
    /* 2 bcdUSB : 0x200 (2.00) */ 0x00,0x02,
    /* 4 bDeviceClass : 0x00 (see interface) */ 0x00,
    /* 5 bDeviceSubClass : 0x00 (see interface) */ 0x00,
    /* 6 bDeviceProtocol : 0x00 (see interface) */ 0x00,
    /* 7 bMaxPacketSize0 */ 8,
    /* 8 bNumConfigurations */ 1,
    /* 9 bReserved */ 0,
    /* --- Configuration Descriptor (9+8+73+55=145, 0x91) */
    /* 0 bLength, bDescriptorType */ 9, 0x02,
    /* 2 wTotalLength */ 145, 0,
    /* 4 bNumInterfaces, bConfigurationValue */ 2, 1,
    /* 6 iConfiguration */ 0,
    /* 7 bmAttributes, bMaxPower */ 0x80, 50,
    /* ----------- Interface Association Descriptor */
    /* 0 bLength, bDescriptorType */ 8, 0x0B,
    /* 2 bFirstInterface, bInterfaceCount */ 0, 2,
    /* 4 bFunctionClass : 0x01 (Audio) */ 0x01,
    /* 5 bFunctionSubClass : 0x00 (UNDEFINED) */ 0x00,
    /* 6 bFunctionProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 7 iFunction */ 0,
    /* --- Interface Descriptor #0: Control (9+64=73) */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 0, 0,
    /* 4 bNumEndpoints */ 0,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioControl) */ 0x01,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* --- Audio 2.0 AC Interface Header Descriptor (9+8+17+18+12=64, 0x40) */
    /* 0 bLength */ 9,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x01,
    /* 3 bcdADC */ 0x00, 0x02,
    /* 5 bCategory : 0x08 (IO Box) */ 0x08,
    /* 6 wTotalLength */ 64, 0,
    /* 8 bmControls */ 0x00,
    /* -------- Audio 2.0 AC Clock Source Descriptor */
    /* 0 bLength */ 8,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x0A,
    /* 3 bClockID */ 0x10,
    /* 4 bmAttributes : 0x05 (Sync|InternalFixedClk) */ 0x05,
    /* 5 bmControls : 0x01 (FreqReadOnly) */ 0x01,
    /* 6 bAssocTerminal, iClockSource */ 0x00, 0,
    /* ------ Audio 2.0 AC Input Terminal Descriptor */
    /* 0 bLength */ 17,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x02, /* 3 bTerminalID */ 0x04,
    /* 4 wTerminalType : 0x0101 (USB Streaming) */ 0x01, 0x01,
    /* 6 bAssocTerminal, bCSourceID */ 0x00, 0x10,
    /* 8 bNrChannels */ 2,
    /* 9 bmChannelConfig */ 0x00, 0x00, 0x00, 0x00,
    /* 13 iChannelNames, bmControls, iTerminal */ 0, 0x00, 0x00, 0,
    /* -------- Audio 2.0 AC Feature Unit Descriptor */
    /* 0 bLength */ 18,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x06,
    /* 3 bUnitID, bSourceID */ 0x05, 0x04,
    /* 5 bmaControls(0) : 0x0F (VolumeRW|MuteRW) */ 0x0F, 0x00, 0x00, 0x00,
    /* 9 bmaControls(1) : 0x00000000 */ 0x00, 0x00, 0x00, 0x00,
    /* 13 bmaControls(1) : 0x00000000 */ 0x00, 0x00, 0x00, 0x00,
    /* . iFeature */ 0,
    /* ----- Audio 2.0 AC Output Terminal Descriptor */
    /* 0 bLength */ 12,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x03, /* 3 bTerminalID */ 0x06,
    /* 4 wTerminalType : 0x0301 (Speaker) */ 0x01, 0x03,
    /* 6 bAssocTerminal, bSourceID, bCSourceID */ 0x00, 0x05, 0x10,
    /* 9 bmControls, iTerminal */ 0x00, 0x00, 0,
    /* --- Interface Descriptor #1: Stream OUT (9+9+16+6+7+8=55) */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 1, 0,
    /* 4 bNumEndpoints */ 0,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioStream) */ 0x02,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* ----------------------- Interface Descriptor */
    /* 0 bLength, bDescriptorType */ 9, 0x04,
    /* 2 bInterfaceNumber, bAlternateSetting */ 1, 1,
    /* 4 bNumEndpoints */ 1,
    /* 5 bInterfaceClass : 0x01 (Audio) */ 0x01,
    /* 6 bInterfaceSubClass : 0x01 (AudioStream) */ 0x02,
    /* 7 bInterfaceProtocol : 0x20 (VERSION_02_00) */ 0x20,
    /* 8 iInterface */ 0,
    /* ----------- Audio 2.0 AS Interface Descriptor */
    /* 0 bLength */ 16,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x01,
    /* 3 bTerminalLink, bmControls */ 0x04, 0x00,
    /* 5 bFormatType : 0x01 (FORMAT_TYPE_I) */ 0x01,
    /* 6 bmFormats : 0x000000001 (PCM) */ 0x01, 0x00, 0x00, 0x00, /* 10 bNrChannels */ 2,
    /* 11 bmChannelConfig */ 0x00, 0x00, 0x00, 0x00,
    /* 15 iChannelNames */ 0, /* --------- Audio 2.0 AS Format Type Descriptor */
    /* 0 bLength */ 6,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x24, 0x02,
    /* 3 bFormatType : 0x01 (FORMAT_TYPE_I) */ 0x01,
    /* 4 bSubslotSize, bBitResolution */ 2, 16,
    /* ------------------------- Endpoint Descriptor */
    /* 0 bLength, bDescriptorType */ 7, 0x05,
    /* 2 bEndpointAddress */ 0x02,
    /* 3 bmAttributes : 0x0D (Sync|ISO) */ 0x0D,
    /* 4 wMaxPacketSize : 0x0100 (256) */ 0x00, 0x01,
    /* 6 bInterval : 0x04 (1ms) */ 4,
    /* - Audio 2.0 AS ISO Audio Data Endpoint Descriptor */
    /* 0 bLength */ 8,
    /* 1 bDescriptorType, bDescriptorSubtype */ 0x25, 0x01,
    /* 3 bmAttributes, bmControls */ 0x00, 0x00,
    /* 5 bLockDelayUnits, wLockDelay */ 0x00, 0x00, 0x00,
};
```

La classe Audio usa un framework di dispositivo composito per raggruppare le interfacce (controllo e streaming). Di conseguenza, è necessario fare attenzione quando si definisce il descrittore del dispositivo. USBX si basa sul descrittore IAD per sapere internamente come associare le interfacce. Il descrittore IAD deve essere dichiarato prima delle interfacce (un'interfaccia AudioControl seguita da una o più interfacce AudioStreaming) e contenere la prima interfaccia della classe Audio (l'interfaccia AudioControl) e il numero di interfacce collegate.

Il funzionamento della classe audio dipende dal fatto che il dispositivo invii o riceva audio, ma entrambi i casi usano un FIFO per l'archiviazione dei buffer dei frame audio: se il dispositivo invia audio all'host, l'applicazione aggiunge buffer di frame audio al FIFO che vengono successivamente inviati all'host da USBX. se il dispositivo riceve l'audio dall'host, USBX aggiunge i buffer dei frame audio ricevuti dall'host al FIFO che vengono letti successivamente dall'applicazione. Ogni flusso audio ha un proprio FIFO e ogni buffer di frame audio è costituito da più campioni.

L'inizializzazione della classe Audio prevede le parti seguenti.

1. La classe audio prevede i parametri di streaming seguenti:

   ```C
   /* Set the parameters for Audio streams. */
   /* Set the application-defined callback that is invoked when the
      host requests a change to the alternate setting. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_callbacks
       .ux_device_class_audio_stream_change = demo_audio_read_change;

   /* Set the application-defined callback that is invoked whenever
      a USB packet (audio frame) is sent to or received from the host. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_callbacks
       .ux_device_class_audio_stream_frame_done = demo_audio_read_done;

   /* Set the number of audio frame buffers in the FIFO. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_max_frame _buffer_nb = UX_DEMO_FRAME_BUFFER_NB;

   /* Set the maximum size of each audio frame buffer in the FIFO. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_max_frame _buffer_size = UX_DEMO_MAX_FRAME_SIZE;

   /* Set the internally-defined audio processing thread entry pointer. If the application wishes to receive audio from the host
      (which is the case in this example), ux_device_class_audio_read_thread_entry should be used;
      if the application wishes to send data to the host, ux_device_class_audio_write_thread_entry should be used. */
   audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_entry = ux_device_class_audio_read_thread_entry;
   ```

2. La classe audio prevede i parametri della funzione seguenti.

   ```C
   /* Set the parameters for Audio device. */

   /* Set the number of streams. */
   audio_parameter.ux_device_class_audio_parameter_streams_nb = 1;

   /* Set the pointer to the first audio stream parameter.
      Note that we initialized this parameter in the previous section.
      Also note that for more than one streams, this should be an array. */
   audio_parameter.ux_device_class_audio_parameter_streams = audio_stream_parameter;

   /* Set the application-defined callback that is invoked when the audio class
      is activated i.e. device is connected to host. */
   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_slave_class_audio_instance_activate = demo_audio_instance_activate;

   /* Set the application-defined callback that is invoked when the audio class
      is deactivated i.e. device is disconnected from host. */

   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_slave_class_audio_instance_deactivate = demo_audio_instance_deactivate;

   /* Set the application-defined callback that is invoked when the stack receives a control request from the host.
      See below for more details.
   */
   audio_parameter.ux_device_class_audio_parameter_callbacks
       .ux_device_class_audio_control_process = demo_audio20_request_process;

   /* Initialize the device Audio class. This class owns interfaces starting with 0. */
   status = ux_device_stack_class_register(_ux_system_slave_class_audio_name,
       ux_device_class_audio_entry, 1, 0, &audio_parameter);
   if(status!=UX_SUCCESS)
       return;
   ```

   Il callback della richiesta di controllo definito dall'applicazione (***ux_device_class_audio_control_process***; impostato nell'esempio precedente) viene richiamato quando lo stack riceve una richiesta di controllo dall'host. Se la richiesta viene accettata e gestita (confermata o bloccata), il callback deve restituire l'esito positivo, in caso contrario dovrebbe essere restituito un errore.

   Il processo di richiesta di controllo specifico della classe è definito come callback definito dall'applicazione perché le richieste di controllo sono molto diverse tra le versioni audio USB e gran parte del processo di richiesta è correlata al framework del dispositivo. L'applicazione deve gestire correttamente le richieste per rendere il dispositivo funzionante.

   Poiché per un dispositivo audio, il volume, l'audio e la frequenza di campionamento sono richieste di controllo comuni, nelle sezioni successive vengono introdotti callback semplici e definiti internamente per versioni audio USB diverse per l'uso da parte delle applicazioni. Per altri **dettagli, vedere*** ux_device_class_audio10_control_process _ e _ *_ux_device_class_audio_control_request_** .

Nel framework del dispositivo audio, il PID/VID viene archiviato nel descrittore del dispositivo (vedere il descrittore del dispositivo dichiarato in precedenza).

Quando un sistema host USB individua il dispositivo audio USB e monta la classe audio, il dispositivo può essere usato con qualsiasi lettore audio o registratore (a seconda del framework). Per informazioni di riferimento, vedere il sistema operativo host.

Le API della classe Audio sono definite di seguito.

## <a name="ux_device_class_audio_read_thread_entry"></a>ux_device_class_audio_read_thread_entry

Voce di thread per la lettura dei dati per la funzione Audio.

### <a name="prototype"></a>Prototipo

```C
VOID ux_device_class_audio_read_thread_entry(ULONG audio_stream);
```

### <a name="description"></a>Descrizione

Questa funzione viene passata al parametro di inizializzazione del flusso audio se si desidera leggere l'audio dall'host. Internamente, viene creato un thread con questa funzione come funzione di ingresso. il thread stesso legge i dati audio tramite l'endpoint OUT isochronous nella funzione Audio.

### <a name="parameters"></a>Parametri

- **audio_stream:** puntatore all'istanza del flusso audio.

### <a name="example"></a>Esempio

```C
/* Set parameter to initialize a stream for reading. */
audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_entry
     = ux_device_class_audio_read_thread_entry;
```

## <a name="ux_device_class_audio_write_thread_entry"></a>ux_device_class_audio_write_thread_entry

Immissione di thread per la scrittura di dati per la funzione Audio

### <a name="prototype"></a>Prototipo

```C
VOID ux_device_class_audio_write_thread_entry(ULONG audio_stream);
```

### <a name="description"></a>Descrizione

Questa funzione viene passata al parametro di inizializzazione del flusso audio se si desidera scrivere audio nell'host. Internamente, viene creato un thread con questa funzione come funzione di ingresso. il thread stesso scrive dati audio tramite l'endpoint ISOchronous IN nella funzione Audio.

### <a name="parameters"></a>Parametri

- **audio_stream:** puntatore all'istanza del flusso audio.

### <a name="example"></a>Esempio

```C
/* Set parameter to initialize as stream for writing. */
audio_stream_parameter[0].ux_device_class_audio_stream_parameter_thread_en
    try = ux_device_class_audio_write_thread_entry;
```

## <a name="ux_device_class_audio_stream_get"></a>ux_device_class_audio_stream_get

Ottenere un'istanza di flusso specifica per la funzione Audio

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_stream_get(
    UX_DEVICE_CLASS_AUDIO *audio,
    ULONG stream_index, 
    UX_DEVICE_CLASS_AUDIO_STREAM **stream);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata per ottenere un'istanza di flusso della classe audio.

### <a name="parameters"></a>Parametri

- **audio:** puntatore all'istanza audio
- **stream_index:** Indice dell'istanza di flusso in base a 0
- **stream:** puntatore al buffer per archiviare il puntatore dell'istanza del flusso audio

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita
- **UX_ERROR** (0xFF) Errore dalla funzione

### <a name="example"></a>Esempio

```C
/* Get audio stream instance. */
status = ux_device_class_audio_stream_get(audio, 0, &stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_reception_start"></a>ux_device_class_audio_reception_start

Avviare la ricezione dei dati audio per il flusso audio

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_reception_start(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata per avviare la lettura dei dati audio nei flussi audio.

### <a name="parameters"></a>Parametri

- **stream:** puntatore all'istanza del flusso audio.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'interfaccia non è disponibile.
- **UX_BUFFER_OVERFLOW** (0x5d) il buffer FIFO è pieno.
- **UX_ERROR** (0xFF) Errore dalla funzione

### <a name="example"></a>Esempio

```C
/* Start stream data reception. */
status = ux_device_class_audio_reception_start(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read8"></a>ux_device_class_audio_sample_read8

Leggere un esempio a 8 bit dal flusso audio

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_sample_read8(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    UCHAR *buffer);
```

### <a name="description"></a>Descrizione

Questa funzione legge i dati di esempio audio a 8 bit dal flusso specificato.

In particolare, legge i dati di esempio dal buffer dei frame audio corrente nel FILE FIFO. Durante la lettura dell'ultimo esempio in un frame audio, il frame verrà liberato automaticamente in modo che possa essere usato per accettare più dati dall'host.

### <a name="parameters"></a>Parametri

- **stream:** puntatore all'istanza del flusso audio.
- **buffer**: puntatore al buffer per salvare il byte di esempio.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'interfaccia non è disponibile.
- **UX_BUFFER_OVERFLOW** (0x5d) il buffer FIFO è Null.
- **UX_ERROR** (0xFF) Errore dalla funzione

### <a name="example"></a>Esempio

```C
/* Read a byte in audio FIFO. */

status = ux_device_class_audio_sample_read8(stream, &sample_byte);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read16"></a>ux_device_class_audio_sample_read16

Leggere un esempio a 16 bit dal flusso audio

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_sample_read16(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    USHORT *buffer);
```

### <a name="description"></a>Descrizione

Questa funzione legge i dati di esempio audio a 16 bit dal flusso specificato.

In particolare, legge i dati di esempio dal buffer dei frame audio corrente nel FILE FIFO. Durante la lettura dell'ultimo esempio in un frame audio, il frame verrà liberato automaticamente in modo che possa essere usato per accettare più dati dall'host.

### <a name="parameters"></a>Parametri

- **stream:** puntatore all'istanza del flusso audio.
- **buffer**: puntatore al buffer per salvare l'esempio a 16 bit.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'interfaccia non è disponibile.
- **UX_BUFFER_OVERFLOW** (0x5d) il buffer FIFO è Null.
- **UX_ERROR** (0xFF) Errore dalla funzione

### <a name="example"></a>Esempio

```C
/* Read a 16-bit sample in audio FIFO. */

status = ux_device_class_audio_sample_read16(stream, &sample_word);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read24"></a>ux_device_class_audio_sample_read24

Leggere un esempio a 24 bit dal flusso audio

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_sample_read24(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG *buffer);
```

### <a name="description"></a>Descrizione

Questa funzione legge i dati di esempio audio a 24 bit dal flusso specificato.

In particolare, legge i dati di esempio dal buffer dei frame audio corrente nel FILE FIFO. Durante la lettura dell'ultimo esempio in un frame audio, il frame verrà liberato automaticamente in modo che possa essere usato per accettare più dati dall'host.

### <a name="parameters"></a>Parametri

- **stream:** puntatore all'istanza del flusso audio.
- **buffer**: puntatore al buffer per salvare l'esempio a 3 byte.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'interfaccia non è disponibile.
- **UX_BUFFER_OVERFLOW** (0x5d) il buffer FIFO è Null.
- **UX_ERROR** (0xFF) Errore dalla funzione

### <a name="example"></a>Esempio

```C
/* Read 3 bytes to in audio FIFO. */

status = ux_device_class_audio_sample_read24(stream, &sample_bytes);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_sample_read32"></a>ux_device_class_audio_sample_read32

Leggere un esempio a 32 bit dal flusso audio

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_sample_read32(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG *buffer);
```

### <a name="description"></a>Descrizione

Questa funzione legge i dati di esempio audio a 32 bit dal flusso specificato.

In particolare, legge i dati di esempio dal buffer dei frame audio corrente nel FILE FIFO. Durante la lettura dell'ultimo esempio in un frame audio, il frame verrà liberato automaticamente in modo che possa essere usato per accettare più dati dall'host.

### <a name="parameters"></a>Parametri

- **stream:** puntatore all'istanza del flusso audio.
- **buffer**: puntatore al buffer per salvare i dati a 4 byte.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'interfaccia non è disponibile.
- **UX_BUFFER_OVERFLOW** (0x5d) il buffer FIFO è Null.
- **UX_ERROR** (0xFF) Errore dalla funzione

### <a name="example"></a>Esempio

```C
/* Read 4 bytes in audio FIFO. */

status = ux_device_class_audio_sample_read32(stream, &sample_bytes);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_read_frame_get"></a>ux_device_class_audio_read_frame_get

Ottenere l'accesso al frame audio nel flusso audio

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_read_frame_get(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR **frame_data, 
    ULONG *frame_length);
```

### <a name="description"></a>Descrizione

Questa funzione restituisce il primo buffer di frame audio e la relativa lunghezza nel FIFO del flusso specificato. Al termine dell'elaborazione dei dati da parte dell'applicazione, ux_device_class_audio_read_frame_free usare per liberare il buffer dei frame nel FILE FIFO.

### <a name="parameters"></a>Parametri

- **stream:** puntatore all'istanza del flusso audio.
- **frame_data:** puntatore al puntatore ai dati in cui restituire il puntatore ai dati.
- **frame_length:** puntatore al buffer per salvare la lunghezza del frame in numero di byte.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'interfaccia non è disponibile.
- **UX_BUFFER_OVERFLOW** (0x5d) il buffer FIFO è Null.
- **UX_ERROR** (0xFF) Errore dalla funzione

### <a name="example"></a>Esempio

```C
/* Get frame access. */

status = ux_device_class_audio_read_frame_get(stream, &frame, &frame_length);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_read_frame_free"></a>ux_device_class_audio_read_frame_free

Liberare un buffer di frame audio nel flusso audio

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_read_frame_free(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a>Descrizione

Questa funzione libera il buffer dei frame audio nella parte anteriore del FIFO del flusso specificato in modo che possa ricevere dati dall'host.

### <a name="parameters"></a>Parametri

- **stream:** puntatore all'istanza del flusso audio.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'interfaccia non è disponibile.
- **UX_BUFFER_OVERFLOW** (0x5d) il buffer FIFO è Null.
- **UX_ERROR** (0xFF) Errore dalla funzione

### <a name="example"></a>Esempio

```C
/* Refree a frame buffer in FIFO. */

status = ux_device_class_audio_read_frame_free(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_transmission_start"></a>ux_device_class_audio_transmission_start

Avviare la trasmissione di dati audio per il flusso audio

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_transmission_start(UX_DEVICE_CLASS_AUDIO_STREAM *stream);
```

### <a name="description"></a>Descrizione

Questa funzione viene usata per iniziare a inviare dati audio scritti al FIFO nella classe audio.

### <a name="parameters"></a>Parametri

- **stream:** puntatore all'istanza del flusso audio.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'interfaccia non è disponibile.
- **UX_BUFFER_OVERFLOW** (0x5d) il buffer FIFO è Null.
- **UX_ERROR** (0xFF) Errore dalla funzione

### <a name="example"></a>Esempio

```C
/* Start stream data transmission. */

status = ux_device_class_audio_transmission_start(stream);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_frame_write"></a>ux_device_class_audio_frame_write

Scrivere un fotogramma audio nel flusso audio

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_frame_write(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR *frame,
    ULONG frame_length);
```

### <a name="description"></a>Descrizione

Questa funzione scrive un frame nel FIFO del flusso audio. I dati del frame vengono copiati nel buffer disponibile in FIFO in modo che possano essere inviati all'host.

### <a name="parameters"></a>Parametri

- **stream:** puntatore all'istanza del flusso audio.
- **frame:** puntatore ai dati del frame.
- **frame_length** Lunghezza del frame in numero di byte.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'interfaccia non è disponibile.
- **UX_BUFFER_OVERFLOW** (0x5d) il buffer FIFO è pieno.
- **UX_ERROR** (0xFF) Errore dalla funzione

### <a name="example"></a>Esempio

```C
/* Get frame access. */

status = ux_device_class_audio_frame_write(stream, frame, frame_length);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio_write_frame_get"></a>ux_device_class_audio_write_frame_get

Ottenere l'accesso al frame audio nel flusso audio

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_write_frame_get(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream,
    UCHAR **frame_data, 
    ULONG *frame_length);
```

### <a name="description"></a>Descrizione

Questa funzione recupera l'indirizzo dell'ultimo buffer di frame audio del FILE FIFO. recupera anche la lunghezza del buffer dei fotogrammi audio. Dopo che l'applicazione ha riempito il buffer dei frame audio con i dati ***desiderati,*** è necessario ux_device_class_audio_write_frame_commit per aggiungere o eseguire il commit del buffer dei frame nel file FIFO.

### <a name="parameters"></a>Parametri

- **stream:** puntatore all'istanza del flusso audio.
- **frame_data:** puntatore al puntatore ai dati del frame in cui restituire il puntatore ai dati del frame.
- **frame_length** Puntatore al buffer per salvare la lunghezza del frame in numero di byte .

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'interfaccia non è disponibile.
- **UX_BUFFER_OVERFLOW** buffer FIFO (0x5d) è pieno.
- **UX_ERROR** (0xFF) dalla funzione

### <a name="example"></a>Esempio

```C
/* Get frame access. */

status = ux_device_class_audio_write_frame_get(stream, &frame, &frame_length);

if(status != UX_SUCCESS)
     return;
```

## <a name="ux_device_class_audio_write_frame_commit"></a>ux_device_class_audio_write_frame_commit

Eseguire il commit di un buffer di frame audio nel flusso audio.

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio_write_frame_commit(
    UX_DEVICE_CLASS_AUDIO_STREAM *stream, 
    ULONG length);
```

### <a name="description"></a>Descrizione

Questa funzione aggiunge/esegue il commit dell'ultimo buffer di frame audio nel file FIFO in modo che il buffer sia pronto per essere trasferito all'host. Si noti che l'ultimo buffer dei fotogrammi audio deve essere stato compilato tramite ux_device_class_write_frame_get.

### <a name="parameters"></a>Parametri

- **stream:** puntatore all'istanza del flusso audio.
- **length:** numero di byte pronti nel buffer.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) L'interfaccia non è disponibile.
- **UX_BUFFER_OVERFLOW** buffer FIFO (0x5d) è fssull.
- **UX_ERROR** (0xFF) dalla funzione

### <a name="example"></a>Esempio

```C
/* Commit a frame after fill values in buffer. */

status = ux_device_class_audio_write_frame_commit(stream, 192);

if(status != UX_SUCCESS)
    return;
```

## <a name="ux_device_class_audio10_control_process"></a>ux_device_class_audio10_control_process

Elaborare le richieste di controllo usb audio 1.0

### <a name="prototype"></a>Prototipo

```C
UINT ux_device_class_audio10_control_process(
    UX_DEVICE_CLASS_AUDIO *audio,
    UX_SLAVE_TRANSFER *transfer_request,
    UX_DEVICE_CLASS_AUDIO10_CONTROL_GROUP *group);
```

### <a name="description"></a>Descrizione

Questa funzione gestisce le richieste di base inviate dall'host nell'endpoint di controllo con un tipo specifico di audio USB 1.0.

Le funzionalità audio 1.0 delle richieste di volume e disattivazione audio vengono elaborate nella funzione . Durante l'elaborazione delle richieste, i dati predefiniti passati dall'ultimo parametro (gruppo) vengono usati per rispondere alle richieste e archiviare le modifiche del controllo.

### <a name="parameters"></a>Parametri

- **audio:** puntatore all'istanza audio.
- **transfer:** puntatore all'istanza della richiesta di trasferimento.
- **group:** gruppo di dati per il processo di richiesta.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_ERROR** (0xFF) dalla funzione

### <a name="example"></a>Esempio

```C
/* Initialize audio 1.0 control values. */

audio_control[0].ux_device_class_audio10_control_fu_id = 2;
audio_control[0].ux_device_class_audio10_control_mute[0] = 0;
audio_control[0].ux_device_class_audio10_control_volume[0] = 0;
audio_control[1].ux_device_class_audio10_control_fu_id = 5;
audio_control[1].ux_device_class_audio10_control_mute[0] = 0;
audio_control[1].ux_device_class_audio10_control_volume[0] = 0;

/* Handle request and update control values.
Note here only mute and volume for master channel is supported.
*/

status = ux_device_class_audio10_control_process(audio, transfer, &group);
if (status == UX_SUCCESS)
{
    /* Request handled, check changes */
    switch(audio_control[0].ux_device_class_audio10_control_changed)
    {
        case UX_DEVICE_CLASS_AUDIO10_CONTROL_MUTE_CHANGED:
        case UX_DEVICE_CLASS_AUDIO10_CONTROL_VOLUME_CHANGED:
        default: break;
    }
}
```

## <a name="ux_device_class_audio20_control_process"></a>ux_device_class_audio20_control_process

Elaborare le richieste di controllo usb audio 1.0

### <a name="prototype"></a>Prototipo
```C
UINT ux_device_class_audio20_control_process(
    UX_DEVICE_CLASS_AUDIO *audio,
    UX_SLAVE_TRANSFER *transfer_request,
    UX_DEVICE_CLASS_AUDIO20_CONTROL_GROUP *group);
```

### <a name="description"></a>Descrizione

Questa funzione gestisce le richieste di base inviate dall'host nell'endpoint di controllo con un tipo specifico di audio USB 2.0.

Frequenza di campionamento audio 2.0 (si presuppone una singola frequenza fissa), le funzionalità delle richieste di volume e disattivazione audio vengono elaborate nella funzione . Durante l'elaborazione delle richieste, i dati predefiniti passati dall'ultimo parametro (gruppo) vengono usati per rispondere alle richieste e archiviare le modifiche del controllo.

### <a name="parameters"></a>Parametri

- **audio:** puntatore all'istanza audio.
- **transfer:** puntatore all'istanza della richiesta di trasferimento.
- **group:** gruppo di dati per il processo di richiesta.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_ERROR** (0xFF) dalla funzione

### <a name="example"></a>Esempio

```C
/* Initialize audio 2.0 control values. */

audio_control[0].ux_device_class_audio20_control_cs_id = 0x10;
audio_control[0].ux_device_class_audio20_control_sampling_frequency = 48000;
audio_control[0].ux_device_class_audio20_control_fu_id = 2;
audio_control[0].ux_device_class_audio20_control_mute[0] = 0;
audio_control[0].ux_device_class_audio20_control_volume_min[0] = 0;
audio_control[0].ux_device_class_audio20_control_volume_max[0] = 100;
audio_control[0].ux_device_class_audio20_control_volume[0] = 50;
audio_control[1].ux_device_class_audio20_control_cs_id = 0x10;
audio_control[1].ux_device_class_audio20_control_sampling_frequency = 48000;
audio_control[1].ux_device_class_audio20_control_fu_id = 5;
audio_control[1].ux_device_class_audio20_control_mute[0] = 0;
audio_control[1].ux_device_class_audio20_control_volume_min[0] = 0;
audio_control[1].ux_device_class_audio20_control_volume_max[0] = 100;
audio_control[1].ux_device_class_audio20_control_volume[0] = 50;

/* Handle request and update control values.
Note here only mute and volume for master channel is supported.
*/

status = ux_device_class_audio20_control_process(audio, transfer, &group);
if (status == UX_SUCCESS)
{
    /* Request handled, check changes */
    switch(audio_control[0].ux_device_class_audio20_control_changed)
    {
        case UX_DEVICE_CLASS_AUDIO20_CONTROL_MUTE_CHANGED:
        case UX_DEVICE_CLASS_AUDIO20_CONTROL_VOLUME_CHANGED:
        default: break;
    }
}
```
