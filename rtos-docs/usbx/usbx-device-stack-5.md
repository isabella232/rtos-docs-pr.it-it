---
title: Capitolo 5-considerazioni sulle classi di dispositivi USBX
description: Informazioni sulle considerazioni sulle classi di dispositivi USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 84f215ad990a2fe185a08f3876276528787ef8bc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822445"
---
# <a name="chapter-5---usbx-device-class-considerations"></a>Capitolo 5-considerazioni sulle classi di dispositivi USBX

## <a name="device-class-registration"></a>Registrazione classe dispositivo

Ogni classe di dispositivo segue lo stesso principio per la registrazione. Una struttura che contiene parametri di classe specifici viene passata alla funzione di inizializzazione della classe.

```c
/* Set the parameters for callback when insertion/extraction of a HID device. */

hid_parameter.ux_slave_class_hid_instance_activate = tx_demo_hid_instance_activate;

hid_parameter.ux_slave_class_hid_instance_deactivate = tx_demo_hid_instance_deactivate;

/* Initialize the hid class parameters for the device. */
hid_parameter.ux_device_class_hid_parameter_report_address = hid_device_report;

hid_parameter.ux_device_class_hid_parameter_report_length = HID_DEVICE_REPORT_LENGTH;

hid_parameter.ux_device_class_hid_parameter_report_id = UX_TRUE;
hid_parameter.ux_device_class_hid_parameter_callback = demo_thread_hid_callback;

/* Initialize the device hid class. The class is connected with interface 0 */

status = ux_device_stack_class_register(_ux_system_slave_class_hid_name,
    ux_device_class_hid_entry,1,0, (VOID *)&hid_parameter);
```

Ogni classe può registrare, facoltativamente, una funzione di callback quando viene attivata un'istanza della classe. Il callback viene quindi chiamato dallo stack del dispositivo per informare l'applicazione che è stata creata un'istanza.

L'applicazione avrebbe nel corpo le 2 funzioni per l'attivazione e la disattivazione, come illustrato nell'esempio seguente.

```c
VOID tx_demo_hid_instance_activate(VOID *hid_instance)
{
    /* Save the HID instance. */
    hid_slave = (UX_SLAVE_CLASS_HID *) hid_instance;
}

VOID tx_demo_hid_instance_deactivate(VOID *hid_instance)
{
    /* Reset the HID instance. */
    hid_slave = UX_NULL;
}
```

Non è consigliabile eseguire alcuna operazione all'interno di queste funzioni, ma per memorizzare l'istanza della classe e sincronizzarla con il resto dell'applicazione.

## <a name="usb-device-storage-class"></a>Classe di archiviazione dispositivo USB

La classe di archiviazione dispositivo USB consente a un dispositivo di archiviazione incorporato nel sistema di essere reso visibile a un host USB.

La classe di archiviazione del dispositivo USB non fornisce una soluzione di archiviazione. Accetta e interpreta semplicemente le richieste SCSI provenienti dall'host. Quando una di queste richieste è un comando Read o Write, richiama una chiamata predefinita a un gestore di dispositivi di archiviazione reale, ad esempio un driver di dispositivo ATA o un driver di dispositivo flash.

Quando si inizializza la classe di archiviazione del dispositivo, viene assegnata una struttura del puntatore alla classe che contiene tutte le informazioni necessarie. Di seguito è illustrato un esempio.

```c
/* Initialize the storage class parameters to customize vendor strings. */

storage_parameter.ux_slave_class_storage_parameter_vendor_id
    = demo_ux_system_slave_class_storage_vendor_id;

storage_parameter.ux_slave_class_storage_parameter_product_id
    = demo_ux_system_slave_class_storage_product_id;

storage_parameter.ux_slave_class_storage_parameter_product_rev
    = demo_ux_system_slave_class_storage_product_rev;

storage_parameter.ux_slave_class_storage_parameter_product_serial
    = demo_ux_system_slave_class_storage_product_serial;

/* Store the number of LUN in this device storage instance: single LUN. */
storage_parameter.ux_slave_class_storage_parameter_number_lun = 1;

/* Initialize the storage class parameters for reading/writing to the Flash Disk. */

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_last_lba = 0x1e6bfe;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_block_length = 512;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_type = 0;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_removable_flag = 0x80;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_read_only_flag
    = UX_FALSE;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_read
    = tx_demo_thread_flash_media_read;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_write
    = tx_demo_thread_flash_media_write;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_status
    = tx_demo_thread_flash_media_status;

/* Initialize the device storage class. The class is connected with interface 0 */
status = ux_device_stack_class_register(_ux_system_slave_class_storage_name,
    ux_device_class_storage_entry, ux_device_class_storage_thread, 0, (VOID *)&storage_parameter);
```

In questo esempio, le stringhe di archiviazione del driver vengono personalizzate assegnando puntatori di stringa al parametro corrispondente. Se uno dei puntatore di stringa viene lasciato UX_NULL, viene utilizzata la stringa di Azure RTO predefinita.

In questo esempio viene fornito l'ultimo indirizzo del blocco o l'LBA dell'unità, nonché le dimensioni del settore logico. LBA è il numero di settori disponibili nel supporto – 1. La lunghezza del blocco è impostata su 512 nei supporti di archiviazione normali. Può essere impostato su 2048 per le unità ottiche.

L'applicazione deve passare tre puntatori a funzione di callback per consentire alla classe di archiviazione di leggere, scrivere e ottenere lo stato del supporto.

Nell'esempio riportato di seguito vengono illustrati i prototipi per le funzioni di lettura e scrittura.

```c
UINT media_read( 
    VOID *storage,  
    ULONG lun,  
    UCHAR *data_pointer,
    ULONG number_blocks,  
    ULONG lba,  
    ULONG *media_status);

UINT media_write( 
    VOID *storage,  
    ULONG lun,  
    UCHAR *data_pointer,
    ULONG number_blocks,  
    ULONG lba,  
    ULONG *media_status);
```

Dove:

- l' *archiviazione* è l'istanza della classe di archiviazione.
- *lun* è il lun a cui viene indirizzato il comando.
- *data_pointer* è l'indirizzo del buffer da utilizzare per la lettura o la scrittura.
- *number_blocks* è il numero di settori di lettura/scrittura.
- *LBA* è l'indirizzo di settore da leggere.
- *media_status* deve essere compilato esattamente come il valore restituito del callback dello stato dei supporti.

Il valore restituito può contenere il valore UX_SUCCESS o UX_ERROR che indica un'operazione riuscita o non riuscita. Queste operazioni non devono restituire altri codici di errore. Se si verifica un errore in qualsiasi operazione, la classe di archiviazione richiama la funzione di richiamata dello stato.

Questa funzione presenta il seguente prototipo.

```c
ULONG media_status( 
    VOID *storage,  
    ULONG lun,  
    ULONG media_id,  
    ULONG *media_status);
```

Il parametro chiamante media_id non è attualmente in uso e deve essere sempre 0. In futuro può essere usato per distinguere più dispositivi di archiviazione o dispositivi di archiviazione con più LUN SCSI. Questa versione della classe di archiviazione non supporta più istanze della classe di archiviazione o dei dispositivi di archiviazione con più LUN SCSI.

Il valore restituito è un codice di errore SCSI che può avere il formato seguente.

- **Bits 0-7** Sense_key
- **Bits 8-15** Codice di rilevamento aggiuntivo
- **Bits 16-23** Qualificatore del codice di rilevamento aggiuntivo

La tabella seguente fornisce le combinazioni possibili/ASC/ASCQ.

| Chiave Sense | ASC | ASCQ | Descrizione                                       |
| --------- | --- | ---- | ------------------------------------------------- |
| 00        | 00  | 00   | NESSUN SIGNIFICATO                                          |
| 01        | 17  | 01   | DATI RIPRISTINATI CON TENTATIVI                       |
| 01        | 18  | 00   | DATI RIPRISTINATI CON ECC                           |
| 02        | 04  | 01   | L'UNITÀ LOGICA NON È PRONTA PER ESSERE PRONTA          |
| 02        | 04  | 02   | UNITÀ LOGICA NON PRONTA-INIZIALIZZAZIONE RICHIESTA |
| 02        | 04  | 04   | UNITÀ LOGICA NON PRONTA-FORMATO IN CORSO       |
| 02        | 04  | FF   | UNITÀ LOGICA NON PRONTA-IL DISPOSITIVO È OCCUPATO          |
| 02        | 06  | 00   | NON SONO STATE TROVATE POSIZIONI DI RIFERIMENTO                       |
| 02        | 08  | 00   | ERRORE DI COMUNICAZIONE UNITÀ LOGICA                |
| 02        | 08  | 01   | TIMEOUT COMUNICAZIONE UNITÀ LOGICA               |
| 02        | 08  | 80   | SOVRACCARICO DELLE COMUNICAZIONI TRA UNITÀ LOGICHE                |
| 02        | 3A  | 00   | MEDIA NON PRESENTE                                |
| 02        | 54  | 00   | ERRORE DELL'INTERFACCIA DI SISTEMA DA USB A HOST              |
| 02        | 80  | 00   | RISORSE INSUFFICIENTI                            |
| 02        | FF  | FF   | ERRORE SCONOSCIUTO                                     |
| 03        | 02  | 00   | NESSUNA RICERCA COMPLETATA                                  |
| 03        | 03  | 00   | ERRORE DI SCRITTURA                                       |
| 03        | 10  | 00   | ERRORE CRC ID                                      |
| 03        | 11  | 00   | ERRORE DI LETTURA NON RECUPERATO                            |
| 03        | 12  | 00   | CONTRASSEGNO INDIRIZZO NON TROVATO PER IL CAMPO ID               |
| 03        | 13  | 00   | CONTRASSEGNO INDIRIZZO NON TROVATO PER IL CAMPO DATI             |
| 03        | 14  | 00   | ENTITÀ REGISTRATA NON TROVATA                         |
| 03        | 30  | 01   | NON È POSSIBILE LEGGERE IL FORMATO MEDIO-SCONOSCIUTO               |
| 03        | 31  | 01   | COMANDO FORMAT NON RIUSCITO                             |
| 04        | 40  | NN   | ERRORE DI DIAGNOSTICA SUL COMPONENTE NN (80H-FFH)      |
| 05        | 1A  | 00   | ERRORE DI LUNGHEZZA DELL'ELENCO DI PARAMETRI                       |
| 05        | 20  | 00   | CODICE OPERAZIONE COMANDO NON VALIDO                    |
| 05        | 21  | 00   | INDIRIZZO BLOCCO LOGICO NON COMPRESO NELL'INTERVALLO                |
| 05        | 24  | 00   | CAMPO NON VALIDO NEL PACCHETTO DI COMANDI                   |
| 05        | 25  | 00   | UNITÀ LOGICA NON SUPPORTATA                        |
| 05        | 26  | 00   | CAMPO NON VALIDO NELL'ELENCO DI PARAMETRI                   |
| 05        | 26  | 01   | PARAMETRO NON SUPPORTATO                           |
| 05        | 26  | 02   | VALORE PARAMETRO NON VALIDO                           |
| 05        | 39  | 00   | SALVATAGGIO DEI PARAMETRI NON SUPPORTATO                     |
| 06        | 28  | 00   | TRANSIZIONE NON PRONTA PER LA PREPARAZIONE: I SUPPORTI SONO STATI MODIFICATI     |
| 06        | 29  | 00   | RIPRISTINO DELL'ACCENSIONE O DELLA REIMPOSTAZIONE DEL DISPOSITIVO BUS       |
| 06        | 2F  | 00   | COMANDI CANCELLATI DA UN ALTRO INIZIATORE             |
| 07        | 27  | 00   | SCRIVI SUPPORTO PROTETTO                             |
| 0B        | 4E  | 00   | TENTATIVO DI COMANDO SOVRAPPOSTO                      |

Sono disponibili altri due callback facoltativi che l'applicazione può implementare; uno è per rispondere a un comando **GET_STATUS_NOTIFICATION** e l'altro per rispondere al comando **SYNCHRONIZE_CACHE** .

Se l'applicazione desidera gestire il comando GET_STATUS_NOTIFICATION dall'host, deve implementare un callback con il prototipo seguente.

```c
UINT ux_slave_class_storage_media_notification( 
    VOID *storage,  
    ULONG lun,
    ULONG media_id,  
    ULONG notification_class,
    UCHAR **media_notification,  
    ULONG *media_notification_length);
```

Dove:

- l' *archiviazione* è l'istanza della classe di archiviazione.
- *media_id* non è attualmente in uso. notification_class specifica la classe di notifica.
- *media_notification* deve essere impostato dall'applicazione sul buffer contenente la risposta per la notifica.
- *media_notification_length* necessario impostare l'applicazione in modo che contenga la lunghezza del buffer di risposta.

Il valore restituito indica se il comando ha avuto esito positivo o meno, **UX_SUCCESS** o **UX_ERROR**.

Se l'applicazione non implementa questo callback, al momento della ricezione del comando di **GET_STATUS_NOTIFICATION** , USBX informerà l'host che il comando non è implementato.

Il **SYNCHRONIZE_CACHE** comando deve essere gestito se l'applicazione utilizza una cache per le Scritture dall'host. Un host può inviare questo comando se sa che il dispositivo di archiviazione sta per essere disconnesso, ad esempio in Windows, se si fa clic con il pulsante destro del mouse sull'icona di un'unità flash sulla barra degli strumenti e si seleziona "Rimuovi \[ nome dispositivo \] di archiviazione", Windows emetterà il comando **SYNCHRONIZE_CACHE** al dispositivo.

Se l'applicazione desidera gestire il comando **GET_STATUS_NOTIFICATION** dall'host, deve implementare un callback con il prototipo seguente.

```c
UINT ux_slave_class_storage_media_flush(
    VOID *storage, 
    ULONG lun,
    ULONG number_blocks, 
    ULONG lba, 
    ULONG *media_status);
```

Dove:

- l' *archiviazione* è l'istanza della classe di archiviazione.
- il parametro *lun* specifica il lun a cui viene indirizzato il comando.
- *number_blocks* specifica il numero di blocchi da sincronizzare.
- *LBA* è l'indirizzo di settore del primo blocco da sincronizzare.
- *media_status* deve essere compilato esattamente come il valore restituito del callback dello stato dei supporti.

Il valore restituito indica se il comando ha avuto esito positivo o meno, **UX_SUCCESS** o **UX_ERROR**.

### <a name="multiple-scsi-lun"></a>LUN multiplo SCSI

La classe di archiviazione del dispositivo USBX supporta più lun. È pertanto possibile creare un dispositivo di archiviazione che funga da CD-ROM e da un disco flash nello stesso momento. In tal caso, l'inizializzazione è leggermente diversa. Di seguito è riportato un esempio per un disco flash e un CD-ROM:

```c
/* Store the number of LUN in this device storage instance. */
storage_parameter.ux_slave_class_storage_parameter_number_lun = 2;

/* Initialize the storage class parameters for reading/writing to the Flash Disk. */
storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_last_lba = 0x7bbff;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_block_length = 512;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_type = 0;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_removable_flag = 0x80;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_read = tx_demo_thread_flash_media_read;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_write = tx_demo_thread_flash_media_write;

storage_parameter.ux_slave_class_storage_parameter_lun[0].ux_slave_class_storage_media_status = tx_demo_thread_flash_media_status;

/* Initialize the storage class LUN parameters for reading/writing to the CD-ROM. */

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_last_lba = 0x04caaf;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_block_length = 2048;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_type = 5;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_removable_flag = 0x80;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_read = tx_demo_thread_cdrom_media_read;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_write = tx_demo_thread_cdrom_media_write;

storage_parameter.ux_slave_class_storage_parameter_lun[1].ux_slave_class_storage_media_status = tx_demo_thread_cdrom_media_status;

/* Initialize the device storage class for a Flash disk and CD-ROM. The class is connected with interface 0 */ status = ux_device_stack_class_register(_ux_system_slave_class_storage_name,ux_device_class_storage_entry,
    ux_device_class_storage_thread,0, (VOID *) &storage_parameter);
```

## <a name="usb-device-cdc-acm-class"></a>Classe dispositivo USB CDC-ACM

La classe CDC-ACM del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come un dispositivo seriale. Questa classe è basata sullo standard USB ed è un subset dello standard CDC.

Un Framework di dispositivi conformi a CDC-ACM deve essere dichiarato dallo stack del dispositivo. Un esempio è disponibile qui di seguito.

```c
unsigned char device_framework_full_speed[] = {

    /*
    Device descriptor 18 bytes
    0x02 bDeviceClass: CDC class code
    0x00 bDeviceSubclass: CDC class sub code 0x00 bDeviceProtocol: CDC Device protocol
    idVendor & idProduct - https://www.linux-usb.org/usb.ids
    */

    0x12, 0x01, 0x10, 0x01,
    0xEF, 0x02, 0x01, 0x08,
    0x84, 0x84, 0x00, 0x00,
    0x00, 0x01, 0x01, 0x02,
    0x03, 0x01,

    /* Configuration 1 descriptor 9 bytes */
    0x09, 0x02, 0x4b, 0x00, 0x02, 0x01, 0x00,0x40, 0x00,

    /* Interface association descriptor. 8 bytes. */
    0x08, 0x0b, 0x00,
    0x02, 0x02, 0x02, 0x00, 0x00,

    /* Communication Class Interface Descriptor Requirement. 9 bytes. */
    0x09, 0x04, 0x00, 0x00,0x01,0x02, 0x02, 0x01, 0x00,

    /* Header Functional Descriptor 5 bytes */
    0x05, 0x24, 0x00,0x10, 0x01,

    /* ACM Functional Descriptor 4 bytes */
    0x04, 0x24, 0x02,0x0f,

    /* Union Functional Descriptor 5 bytes */
    0x05, 0x24, 0x06, 0x00,

    /* Master interface */
    0x01, /* Slave interface */

    /* Call Management Functional Descriptor 5 bytes */
    0x05, 0x24, 0x01,0x03, 0x01, /* Data interface */

    /* Endpoint 1 descriptor 7 bytes */
    0x07, 0x05, 0x83, 0x03,0x08, 0x00, 0xFF,

    /* Data Class Interface Descriptor Requirement 9 bytes */
    0x09, 0x04, 0x01, 0x00, 0x02,0x0A, 0x00, 0x00, 0x00,

    /* First alternate setting Endpoint 1 descriptor 7 bytes*/
    0x07, 0x05, 0x02,0x02,0x40, 0x00,0x00,

    /* Endpoint 2 descriptor 7 bytes */
    0x07, 0x05, 0x81,0x02,0x40, 0x00, 0x00,

};
```

La classe CDC-ACM usa un Framework per dispositivi composito per raggruppare le interfacce (controllo e dati). È necessario prestare attenzione quando si definisce il descrittore del dispositivo. USBX si basa sul descrittore IAD per comprendere internamente come associare le interfacce. Il descrittore IAD deve essere dichiarato prima delle interfacce e contenere la prima interfaccia della classe CDC-ACM e il numero di interfacce associate.

La classe CDC-ACM usa anche un descrittore di funzionalità di Unione che esegue la stessa funzione del descrittore IAD più recente. Sebbene sia necessario dichiarare un descrittore funzionale Unione per motivi cronologici e la compatibilità con il lato host, questo non viene usato da USBX.

L'inizializzazione della classe CDC-ACM prevede i parametri seguenti.

```c
/* Set the parameters for callback when insertion/extraction of a CDC device. */

parameter.ux_slave_class_cdc_acm_instance_activate = tx_demo_cdc_instance_activate;

parameter.ux_slave_class_cdc_acm_instance_deactivate = tx_demo_cdc_instance_deactivate;

parameter.ux_slave_class_cdc_acm_parameter_change = tx_demo_cdc_instance_parameter_change;

/* Initialize the device cdc class. This class owns both interfaces starting with 0. */
status = ux_device_stack_class_register(_ux_system_slave_class_cdc_acm_name,ux_device_class_cdc_acm_entry,
    1,0, &parameter);
```

I 2 parametri definiti sono puntatori di callback nelle applicazioni utente che verranno chiamate quando lo stack attiva o disattiva questa classe.

Il terzo parametro definito è un puntatore di callback all'applicazione utente che verrà chiamato in caso di modifica del parametro della riga o del codice di riga. Ad esempio, quando è presente una richiesta da host per modificare lo stato di DTR su **true**, viene richiamato il callback, nell'applicazione utente it è possibile controllare gli Stati della riga tramite la funzione IOCTL per l'host Kow è pronto per la comunicazione.

CDC-ACM si basa su uno standard USB-IF e viene riconosciuto automaticamente dai sistemi operativi MACOs e Linux. Nelle piattaforme Windows questa classe richiede un file inf per la versione di Windows precedente alla 10. Windows 10 non richiede alcun file inf. Viene fornito un modello per la classe CDC-ACM, che è possibile trovare nella directory ***usbx_windows_host_files*** . Per la versione più recente di Windows, è necessario utilizzare il file CDC_ACM_Template_Win7_64bit. inf (ad eccezione di Win10). Questo file deve essere modificato in modo da riflettere il PID/VID usato dal dispositivo. Il PID/VID sarà specifico per il cliente finale quando la società e il prodotto vengono registrati con il dispositivo USB-IF. Nel file inf i campi da modificare si trovano qui.

```INF
[DeviceList]
%DESCRIPTION%=DriverInstall, USB\VID_8484&PID_0000

[DeviceList.NTamd64]
%DESCRIPTION%=DriverInstall, USB\VID_8484&PID_0000
```

Nel Framework del dispositivo del dispositivo CDC-ACM, il PID/VID viene archiviato nel descrittore del dispositivo (vedere il descrittore del dispositivo dichiarato in precedenza).

Quando un sistema host USB individua il dispositivo USB CDC-ACM, viene montata una classe seriale e il dispositivo può essere usato con qualsiasi programma terminale seriale. Per informazioni di riferimento, vedere il sistema operativo host.

Le funzioni API della classe CDC-ACM sono definite di seguito.

### <a name="ux_device_class_cdc_acm_ioctl"></a>ux_device_class_cdc_acm_ioctl

Eseguire IOCTL sull'interfaccia CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm, 
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve eseguire varie chiamate ioctl all'interfaccia di CDC ACM

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe CDC.
- **ioctl_function**: funzione IOCTL da eseguire.
- **Parameter**: puntatore a un parametro specifico della chiamata IOCTL.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) questa operazione è stata completata.
- Errore di **UX_ERROR** (0xFF) dalla funzione

### <a name="example"></a>Esempio

```c
/* Start cdc acm callback transmission. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START, &callback);

if(status != UX_SUCCESS)
    return;
```

### <a name="ioctl-functions"></a>Funzioni IOCTL:

| Funzione                                        | Valore |
| ----------------------------------------------- | - |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING    | 1 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING    | 2 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE     | 3 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE         | 4 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE     | 5 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START | 6 |
| UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP  | 7 |

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_set_line_coding"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING

Eseguire la codifica a linee del set IOCTL sull'interfaccia CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM*cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve impostare i parametri di codifica della riga.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe CDC.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING
- **parametro**: puntatore a una struttura di parametri di linea:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER_STRUCT
{
    ULONG ux_slave_class_cdc_acm_parameter_baudrate;
    UCHAR ux_slave_class_cdc_acm_parameter_stop_bit;
    UCHAR ux_slave_class_cdc_acm_parameter_parity;
    UCHAR ux_slave_class_cdc_acm_parameter_data_bit;
} UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER;
```

### <a name="return-value"></a>Valore restituito

**UX_SUCCESS** (0x00) questa operazione è stata completata.

### <a name="example"></a>Esempio

```c
/* Change the line coding values. */

line_coding.ux_slave_class_cdc_acm_line_coding_dter = 9600;
line_coding.ux_slave_class_cdc_acm_line_coding_stop_bit =
    UX_HOST_CLASS_CDC_ACM_LINE_CODING_STOP_BIT_15;

line_coding.ux_slave_class_cdc_acm_line_coding_parity =
    UX_HOST_CLASS_CDC_ACM_LINE_CODING_PARITY_EVEN;

line_coding.ux_slave_class_cdc_acm_line_coding_data_bits = 5;

status = _ux_slave_class_cdc_acm_ioctl(cdc_acm,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING, &line_coding);

if (status != UX_SUCCESS)
    break;
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_get_line_coding"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING

Eseguire IOCTL per ottenere la codifica della riga sull'interfaccia CDC-ACM

### <a name="prototype"></a>Prototipo

```c
device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve ottenere i parametri di codifica della riga.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe CDC.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_ LINE_CODING
- **parametro**: puntatore a una struttura di parametri di linea:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER_STRUCT
{
    ULONG ux_slave_class_cdc_acm_parameter_baudrate;
    UCHAR ux_slave_class_cdc_acm_parameter_stop_bit;
    UCHAR ux_slave_class_cdc_acm_parameter_parity;
    UCHAR ux_slave_class_cdc_acm_parameter_data_bit;
} UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER;
```

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) questa operazione è stata completata.

### <a name="example"></a>Esempio

```c
/* This is to retrieve BAUD rate. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING, &line_coding);

/* Any error ? */
if (status == UX_SUCCESS)
{
    /* Decode BAUD rate. */
    switch (line_coding.ux_slave_class_cdc_acm_parameter_baudrate)
    {
        case 1200 :
            status = tx_demo_thread_slave_cdc_acm_response("1200", 4);
            break;
        case 2400 :
            status = tx_demo_thread_slave_cdc_acm_response("2400", 4);
            break;
        case 4800 :
            status = tx_demo_thread_slave_cdc_acm_response("4800", 4);
            break;
        case 9600 :
            status = tx_demo_thread_slave_cdc_acm_response("9600", 4);
            break;
        case 115200 :
            status = tx_demo_thread_slave_cdc_acm_response("115200", 6);
            break;
    }
}
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_get_line_state"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE

Eseguire IOCTL ottenere lo stato della riga sull'interfaccia CDC-ACM

## <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM*cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve ottenere i parametri dello stato della riga.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe CDC.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE
- **parametro**: puntatore a una struttura di parametri di linea:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER_STRUCT
{
    UCHAR ux_slave_class_cdc_acm_parameter_rts;
    UCHAR ux_slave_class_cdc_acm_parameter_dtr;
} UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER;
```

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) questa operazione è stata completata.

### <a name="example"></a>Esempio

```c
/* This is to retrieve RTS state. */
status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE, &line_state);

/* Any error ? */
if (status == UX_SUCCESS)
{
/* Check state. */
    if (line_state.ux_slave_class_cdc_acm_parameter_rts == UX_TRUE)
        /* State is ON. */
        status = tx_demo_thread_slave_cdc_acm_response("RTS ON", 6);
    else
        /* State is OFF. */
        status = tx_demo_thread_slave_cdc_acm_response("RTS OFF", 7);
}
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_set_line_state"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE

Eseguire lo stato della linea di set IOCTL sull'interfaccia CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve ottenere i parametri dello stato della riga

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe CDC.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE
- **parametro**: puntatore a una struttura di parametri di linea:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER_STRUCT
{
    UCHAR ux_slave_class_cdc_acm_parameter_rts;
    UCHAR ux_slave_class_cdc_acm_parameter_dtr;
} UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER;
```

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) questa operazione è stata completata.

### <a name="example"></a>Esempio

```c
/* This is to set RTS state. */

line_state.ux_slave_class_cdc_acm_parameter_rts = UX_TRUE;
status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE, &line_state);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_abort_pipe"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE

Eseguire la PIPE di interruzione IOCTL nell'interfaccia CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve interrompere una pipe. Ad esempio, per interrompere una scrittura in corso, UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT deve essere passata come parametro.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe CDC.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE
- **parametro**: direzione pipe:

```c
UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT 1

UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_RCV 2
```

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) questa operazione è stata completata.
- La direzione della pipe **UX_ENDPOINT_HANDLE_UNKNOWN** (0X53) non è valida.

### <a name="example"></a>Esempio

```c
/* This is to abort the Xmit pipe. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE,
    UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_transmission_start"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START

Eseguire l'avvio della trasmissione IOCTL sull'interfaccia CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione vuole usare la trasmissione con callback.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe CDC.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START
- **parametro**: puntatore alla struttura del parametro di trasmissione iniziale:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_CALLBACK_PARAMETER_STRUCT
{
    UINT (*ux_device_class_cdc_acm_parameter_write_callback)(struct UX_SLAVE_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, ULONG length);
    UINT (*ux_device_class_cdc_acm_parameter_read_callback)(struct UX_SLAVE_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, UCHAR *data_pointer, ULONG length);
} UX_SLAVE_CLASS_CDC_ACM_CALLBACK_PARAMETER;
```

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) questa operazione è stata completata.
- Trasmissione **UX_ERROR** (0xFF) già avviata.
- **UX_MEMORY_INSUFFICIENT** (0X12) un'allocazione di memoria non riuscita.

### <a name="example"></a>Esempio

```c
/* Set the callback parameter. */

callback.ux_device_class_cdc_acm_parameter_write_callback
    = tx_demo_thread_slave_write_callback;

callback.ux_device_class_cdc_acm_parameter_read_callback
    = tx_demo_thread_slave_read_callback;

/* Program the start of transmission. */
status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START, &callback);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_transmission_stop"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP

Eseguire l'arresto della trasmissione IOCTL sull'interfaccia CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_ioctl( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione desidera interrompere l'utilizzo della trasmissione con callback.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe CDC.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSI ON_STOP
- **parametro**: non usato

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) questa operazione è stata completata.
- **UX_ERROR** (0Xff) nessuna trasmissione in corso.

### <a name="example"></a>Esempio

```c
/* Program the stop of transmission. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP, UX_NULL);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_read"></a>ux_device_class_cdc_acm_read

Lettura dalla pipe CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_read( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length,  
    ULONG *actual_length);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve leggere dalla pipe di dati OUT (dall'host, IN dal dispositivo). Si tratta di un blocco.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe CDC.
- **buffer**: indirizzo del buffer in cui verranno archiviati i dati.
- **requested_length**: lunghezza massima prevista.
- **actual_length**: lunghezza restituita nel buffer.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) questa operazione è stata completata.
- Lo stato del dispositivo **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) non è più configurato.
- **UX_TRANSFER_NO_ANSWER** (0X22) nessuna risposta dal dispositivo. Il dispositivo è stato probabilmente disconnesso mentre il trasferimento era in sospeso.

### <a name="example"></a>Esempio

```c
/* Read from the CDC class. */

status = ux_device_class_cdc_acm_read(cdc, buffer, UX_DEMO_BUFFER_SIZE, &actual_length);

if(status != UX_SUCCESS) return;
```

### <a name="ux_device_class_cdc_acm_write"></a>ux_device_class_cdc_acm_write

Scrivere in una pipe CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_write( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length,  
    ULONG *actual_length);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve scrivere nella pipe di dati (IN dall'host, dal dispositivo). Si tratta di un blocco.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe CDC.
- **buffer**: indirizzo del buffer in cui vengono archiviati i dati.
- **requested_length**: lunghezza del buffer da scrivere.
- **actual_length**: lunghezza restituita nel buffer dopo l'esecuzione della scrittura.

### <a name="return-value"></a>Valore restituito
- **UX_SUCCESS** (0x00) questa operazione è stata completata.
- Lo stato del dispositivo **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) non è più configurato.
- **UX_TRANSFER_NO_ANSWER** (0X22) nessuna risposta dal dispositivo. Il dispositivo è stato probabilmente disconnesso mentre il trasferimento era in sospeso.

### <a name="example"></a>Esempio

```c
/* Write to the CDC class bulk in pipe. */

status = ux_device_class_cdc_acm_write(cdc, buffer, UX_DEMO_BUFFER_SIZE, &actual_length);

if(status != UX_SUCCESS)
    return;
```

### <a name="ux_device_class_cdc_acm_write_with_callback"></a>ux_device_class_cdc_acm_write_with_callback

Scrittura in una pipe CDC-ACM con callback

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_write_with_callback( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve scrivere nella pipe di dati (IN dall'host, dal dispositivo). Questa funzione non è bloccata e il completamento verrà eseguito tramite un set di callback in UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe CDC.
- **buffer**: indirizzo del buffer in cui vengono archiviati i dati.
- **requested_length**: lunghezza del buffer da scrivere.
- **actual_length**: lunghezza restituita nel buffer dopo l'esecuzione della scrittura

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) questa operazione è stata completata.
- Lo stato del dispositivo **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) non è più configurato.
- **UX_TRANSFER_NO_ANSWER** (0X22) nessuna risposta dal dispositivo. Il dispositivo è stato probabilmente disconnesso mentre il trasferimento era in sospeso.

### <a name="example"></a>Esempio

```c
/* Write to the CDC class bulk in pipe non blocking mode. */
status = ux_device_class_cdc_acm_write_with_callback(cdc, buffer, UX_DEMO_BUFFER_SIZE);

if(status != UX_SUCCESS)
    return;
```

### <a name="usb-device-cdc-ecm-class"></a>Classe dispositivo USB CDC-ECM

La classe CDC-ECM del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come dispositivo Ethernet. Questa classe è basata sullo standard USB ed è un subset dello standard CDC.

Un Framework di dispositivi conformi a CDC-ACM deve essere dichiarato dallo stack del dispositivo. Un esempio è disponibile qui di seguito.

```c
unsigned char device_framework_full_speed[] = {

    /* Device descriptor 18 bytes
    0x02 bDeviceClass: CDC_ECM class code
    0x06 bDeviceSubclass: CDC_ECM class sub code
    0x00 bDeviceProtocol: CDC_ECM Device protocol
    idVendor & idProduct - https://www.linux-usb.org/usb.ids
    0x3939 idVendor: Azure RTOS test.
    */
    
    0x12, 0x01, 0x10, 0x01,
    0x02, 0x00, 0x00, 0x08,
    0x39, 0x39, 0x08, 0x08, 0x00, 0x01, 0x01, 0x02, 03,0x01,
    
    /* Configuration 1 descriptor 9 bytes. */
    0x09, 0x02, 0x58, 0x00,0x02, 0x01, 0x00,0x40, 0x00,
    
    /* Interface association descriptor. 8 bytes. */
    
    0x08, 0x0b, 0x00, 0x02, 0x02, 0x06, 0x00, 0x00,
    
    /* Communication Class Interface Descriptor Requirement 9 bytes */
    0x09, 0x04, 0x00, 0x00,0x01,0x02, 0x06, 0x00, 0x00,
    
    /* Header Functional Descriptor 5 bytes */
    0x05, 0x24, 0x00, 0x10, 0x01,
    
    /* ECM Functional Descriptor 13 bytes */
    0x0D, 0x24, 0x0F, 0x04,0x00, 0x00, 0x00, 0x00, 0xEA, 0x05, 0x00,
    0x00,0x00,
    
    /* Union Functional Descriptor 5 bytes */
    0x05, 0x24, 0x06, 0x00,0x01,
    
    /* Endpoint descriptor (Interrupt) */
    0x07, 0x05, 0x83, 0x03, 0x08, 0x00, 0x08,
    
    /* Data Class Interface Descriptor Alternate Setting 0, 0 endpoints. 9 bytes */
    0x09, 0x04, 0x01, 0x00, 0x00, 0x0A, 0x00, 0x00, 0x00,
    
    /* Data Class Interface Descriptor Alternate Setting 1, 2 endpoints. 9 bytes */
    0x09, 0x04, 0x01, 0x01, 0x02, 0x0A, 0x00, 0x00,0x00,
    
    /* First alternate setting Endpoint 1 descriptor 7 bytes */
    0x07, 0x05, 0x02, 0x02, 0x40, 0x00, 0x00,
    
    /* Endpoint 2 descriptor 7 bytes */
    0x07, 0x05, 0x81, 0x02, 0x40, 0x00,0x00

};
```

La classe CDC-ECM usa un approccio del descrittore di dispositivo molto simile a CDC-ACM e richiede anche un descrittore IAD. Vedere la classe CDC-ACM per la definizione.

Oltre al normale Framework per dispositivi, CDC-ECM richiede descrittori di stringa speciali. Di seguito è illustrato un esempio.

```c
unsigned char string_framework[] = {
    /* Manufacturer string descriptor: Index 1 - "Azure RTOS" */
    0x09, 0x04, 0x01, 0x0c,
    0x45, 0x78, 0x70, 0x72, 0x65, 0x73, 0x20, 0x4c,
    0x6f, 0x67, 0x69, 0x63,
    
    /* Product string descriptor: Index 2 - "EL CDCECM Device" */
    0x09, 0x04, 0x02, 0x10,
    0x45, 0x4c, 0x20, 0x43, 0x44, 0x43, 0x45, 0x43,
    0x4d, 0x20, 0x44, 0x65, 0x76, 0x69, 0x63, 0x64,
    
    /* Serial Number string descriptor: Index 3 - "0001" */
    0x09, 0x04, 0x03, 0x04,
    0x30, 0x30, 0x30, 0x31,
    
    /* MAC Address string descriptor: Index 4 - "001E5841B879" */
    0x09, 0x04, 0x04, 0x0C,
    0x30, 0x30, 0x31, 0x45, 0x35, 0x38,
    0x34, 0x31, 0x42, 0x38, 0x37, 0x39

};
```

Il descrittore della stringa dell'indirizzo MAC viene usato dalla classe CDC-ECM per rispondere alle query host per l'indirizzo MAC a cui il dispositivo risponde al protocollo TCP/IP. Può essere impostata sulla scelta del dispositivo, ma deve essere definita qui.

L'inizializzazione della classe CDC-ECM è la seguente.

```c
/* Set the parameters for callback when insertion/extraction of a CDC device. Set to NULL.*/
cdc_ecm_parameter.ux_slave_class_cdc_ecm_instance_activate = UX_NULL;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_instance_deactivate = UX_NULL;

/* Define a NODE ID. */
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[0] = 0x00;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[1] = 0x1e;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[2] = 0x58;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[3] = 0x41;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[4] = 0xb8;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_local_node_id[5] = 0x78;

/* Define a remote NODE ID. */
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[0] = 0x00;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[1] = 0x1e;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[2] = 0x58;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[3] = 0x41;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[4] = 0xb8;
cdc_ecm_parameter.ux_slave_class_cdc_ecm_parameter_remote_node_id[5] = 0x79;

/* Initialize the device cdc_ecm class. */
status = ux_device_stack_class_register(_ux_system_slave_class_cdc_ecm_name,
    ux_device_class_cdc_ecm_entry, 1,0,&cdc_ecm_parameter);
```

L'inizializzazione di questa classe prevede lo stesso callback di funzione per l'attivazione e la disattivazione, anche se in questo caso viene impostato su NULL in modo che non venga eseguito alcun callback.

I parametri successivi sono per la definizione degli ID del nodo. 2 nodi sono necessari per CDC-ECM, un nodo locale e un nodo remoto. Il nodo locale specifica l'indirizzo MAC del dispositivo, mentre il nodo remoto specifica l'indirizzo MAC dell'host. Il nodo remoto deve essere uguale a quello dichiarato nel descrittore di stringa del Framework del dispositivo.

La classe CDC-ECM include API incorporate per il trasferimento dei dati in entrambe le direzioni, ma nascoste all'applicazione perché l'applicazione utente comunicherà con il dispositivo Ethernet USB tramite NetX.

La classe USBX CDC-ECM è strettamente legata allo stack di rete NetX di Azure RTO. Un'applicazione che usa sia NetX che la classe CDC-ECM USBX attiverà lo stack di rete NetX nel modo consueto, ma in aggiunta deve attivare lo stack di rete USB come indicato di seguito.

```c
/* Initialize the NetX system. */
nx_system_initialize();

/* Perform the initialization of the network driver. This will initialize the USBX network layer.*/
ux_network_driver_init();
```

Lo stack di rete USB deve essere attivato solo una volta e non è specifico di CDCECM, ma è richiesto da qualsiasi classe USB che richiede i servizi di NetX.

La classe CDC-ECM verrà riconosciuta dagli host MAC OS e Linux. Non è tuttavia disponibile alcun driver fornito da Microsoft Windows per riconoscere CDC-ECM in modo nativo. Per le piattaforme Windows sono presenti prodotti commerciali che forniscono il proprio file con estensione inf. Questo file deve essere modificato nello stesso modo in cui si trova il modello CDC-ACM inf per corrispondere al PID/VID del dispositivo di rete USB.

## <a name="usb-device-hid-class"></a>Classe dispositivo HID USB

La classe HID del dispositivo USB consente a un sistema host USB di connettersi a un dispositivo HID con funzionalità client HID specifiche.

La classe del dispositivo HID USBX è relativamente semplice rispetto al lato host. È strettamente legata al comportamento del dispositivo e del relativo descrittore HID.

Per tutti i client HID è necessario innanzitutto definire un Framework per dispositivi HID come riportato di seguito.

```c
UCHAR device_framework_full_speed[] = {
    /* Device descriptor */
    0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x08,
    0x81, 0x0A, 0x01, 0x01, 0x00, 0x00, 0x00, 0x00,
    0x00, 0x01,

    /* Configuration descriptor */
    0x09, 0x02, 0x22, 0x00, 0x01, 0x01, 0x00, 0xc0, 0x32,

    /* Interface descriptor */
    0x09, 0x04, 0x00, 0x00, 0x01, 0x03, 0x00, 0x00, 0x00,

    /* HID descriptor */
    0x09, 0x21, 0x10, 0x01, 0x21, 0x01, 0x22, 0x3f, 0x00,

    /* Endpoint descriptor (Interrupt) */
    0x07, 0x05, 0x81, 0x03, 0x08, 0x00, 0x08

};
```

Il Framework HID contiene un descrittore di interfaccia che descrive la classe HID e la sottoclasse del dispositivo HID. L'interfaccia HID può essere una classe autonoma o una parte di un dispositivo composito.

Attualmente la classe HID USBX non supporta più ID report, perché la maggior parte delle applicazioni richiede un solo ID (ID zero). Se più ID report sono una funzionalità a cui si è interessati, contattare Microsoft.

L'inizializzazione della classe HID è la seguente, usando una tastiera USB come esempio.

```c
/* Initialize the hid class parameters for a keyboard. */
hid_parameter.ux_device_class_hid_parameter_report_address = hid_keyboard_report;
hid_parameter.ux_device_class_hid_parameter_report_length = HID_KEYBOARD_REPORT_LENGTH;
hid_parameter.ux_device_class_hid_parameter_callback = tx_demo_thread_hid_callback;
hid_parameter.ux_device_class_hid_parameter_report_id = 0;

/* Initialize the device hid class. The class is connected with interface 0 */

status = ux_device_stack_class_register(_ux_system_slave_class_hid_name,
    ux_device_class_hid_entry, 1,0,(VOID *)&hid_parameter);
if (status!=UX_SUCCESS)
    return;
```

L'applicazione deve passare alla classe HID un descrittore di report HID e la relativa lunghezza. Il descrittore del report è una raccolta di elementi che descrivono il dispositivo. Per ulteriori informazioni sulla grammatica nascosta, vedere la specifica della classe USB HID.

Oltre al descrittore del report, l'applicazione passa una chiamata quando si verifica un evento HID.

La classe HID USBX supporta i comandi HID standard seguenti dall'host.

| Nome comando                             | Valore | Descrizione                                      |
| ---------------------------------------- | ----- | ------------------------------------------------ |
| UX_DEVICE_CLASS_HID_COMMAND_GET_REPORT   | 0x01  | Ottenere un report dal dispositivo                     |
| UX_DEVICE_CLASS_HID_COMMAND_GET_IDLE     | 0x02  | Ottenere la frequenza di inattività dell'endpoint di interrupt |
| UX_DEVICE_CLASS_HID_COMMAND_GET_PROTOCOL | 0x03  | Ottenere il protocollo in esecuzione nel dispositivo           |
| UX_DEVICE_CLASS_HID_COMMAND_SET_REPORT   | 0x09  | Impostare un report sul dispositivo                       |
| UX_DEVICE_CLASS_HID_COMMAND_SET_IDLE     | 0x0A  | Imposta la frequenza di inattività dell'endpoint di interrupt |
| UX_DEVICE_CLASS_HID_COMMAND_SET_PROTOCOL | 0x0B  | Ottenere il protocollo in esecuzione nel dispositivo           |

Il report Get e set sono i comandi usati più di frequente da HID per trasferire i dati tra l'host e il dispositivo. Nella maggior parte dei casi l'host invia dati nell'endpoint di controllo ma può ricevere dati nell'endpoint di interrupt oppure eseguendo un comando GET_REPORT per recuperare i dati nell'endpoint di controllo.

La classe HID può restituire dati all'host nell'endpoint di interrupt utilizzando la funzione ux_device_class_hid_event_set.

### <a name="ux_device_class_hid_event_set"></a>ux_device_class_hid_event_set

Impostazione di un evento per la classe HID

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_hid_event_set( 
    UX_SLAVE_CLASS_HID *hid,
    UX_SLAVE_CLASS_HID_EVENT *hid_event);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve inviare un evento HID all'host. Poiché la funzione non blocca, il report viene semplicemente inserito in una coda circolare e viene restituito all'applicazione.

### <a name="parameters"></a>Parametri

- **HID**: puntatore all'istanza della classe HID.
- **hid_event**: puntatore alla struttura dell'evento HID.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) questa operazione è stata completata.
- Errore **UX_ERROR** (0xFF) non è disponibile spazio nella coda circolare.

### <a name="example"></a>Esempio

```c
/* Insert a key into the keyboard event. Length is fixed to 8. */
hid_event.ux_device_class_hid_event_length = 8;

/* First byte is a modifier byte. */
hid_event.ux_device_class_hid_event_buffer[0] = 0;

/* Second byte is reserved. */
hid_event.ux_device_class_hid_event_buffer[1] = 0;

/* The 6 next bytes are keys. We only have one key here. */
hid_event.ux_device_class_hid_event_buffer[2] = key;

/* Set the keyboard event. */
ux_device_class_hid_event_set(hid, &hid_event);
```

Il callback definito in fase di inizializzazione della classe HID esegue l'opposto dell'invio di un evento. Ottiene come input l'evento inviato dall'host. Il prototipo del callback è il seguente.

### <a name="hid_callback"></a>hid_callback

Recupero di un evento dalla classe HID

### <a name="prototype"></a>Prototipo

```c
UINT hid_callback(
    UX_SLAVE_CLASS_HID *hid, 
    UX_SLAVE_CLASS_HID_EVENT *hid_event);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando l'host invia un report nascosto all'applicazione.

### <a name="parameters"></a>Parametri

- **HID**: puntatore all'istanza della classe HID.
- **hid_event**: puntatore alla struttura dell'evento HID.

### <a name="example"></a>Esempio

Nell'esempio seguente viene illustrato come interpretare un evento per una tastiera nascosta:

```c
UINT tx_demo_thread_hid_callback(UX_SLAVE_CLASS_HID *hid, UX_SLAVE_CLASS_HID_EVENT *hid_event
{
/* There was an event. Analyze it. Is it NUM LOCK ? */

if (hid_event -\ux_device_class_hid_event_buffer[0] & HID_NUM_LOCK_MASK)
    /* Set the Num lock flag. */
    num_lock_flag = UX_TRUE;
else
    /* Reset the Num lock flag. */
    num_lock_flag = UX_FALSE;

/* There was an event. Analyze it. Is it CAPS LOCK ? */

if (hid_event -\ux_device_class_hid_event_buffer[0] & HID_CAPS_LOCK_MASK)
    /* Set the Caps lock flag. */
    caps_lock_flag = UX_TRUE;
else
    /* Reset the Caps lock flag. */
    caps_lock_flag = UX_FALSE;
}
```
