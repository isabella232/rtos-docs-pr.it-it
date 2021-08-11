---
title: Capitolo 5 - Considerazioni sulle classi di dispositivi USBX
description: Informazioni sulle considerazioni sulla classe di dispositivi USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: b8fcfa251df9140d23b50a99f13f2755d2bdfae0ca6b9529633f25e263c7edcc
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798741"
---
# <a name="chapter-5---usbx-device-class-considerations"></a>Capitolo 5 - Considerazioni sulle classi di dispositivi USBX

## <a name="device-class-registration"></a>Registrazione della classe di dispositivi

Ogni classe di dispositivo segue lo stesso principio per la registrazione. Una struttura contenente parametri di classe specifici viene passata alla funzione di inizializzazione della classe.

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

Ogni classe può registrare, facoltativamente, una funzione di callback quando viene attivata un'istanza della classe. Il callback viene quindi chiamato dallo stack di dispositivi per informare l'applicazione che è stata creata un'istanza di .

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

Non è consigliabile eseguire operazioni all'interno di queste funzioni, ma memorizzare l'istanza della classe e sincronizzarla con il resto dell'applicazione.

## <a name="general-considerations-for-bulk-transfer"></a>Considerazioni generali sul trasferimento bulk

In base alla specifica USB 2.0, un endpoint deve sempre trasmettere payload di dati con un campo dati minore o uguale al valore wMaxPacketSize segnalato dall'endpoint. Le dimensioni di un pacchetto di dati sono limitate a bMaxPacketSize. Il trasferimento può essere completato nei casi seguenti
1. L'endpoint ha trasferito esattamente la quantità di dati prevista
2. Quando un dispositivo o un endpoint host viene ricevuto da un pacchetto con dimensioni inferiori alle dimensioni massime del pacchetto (wMaxPacketSize). Questo pacchetto breve indica che non è più disponibile alcun pacchetto di dati e che il trasferimento è stato completato oppure quando i pacchetti di dati da trasmettere sono tutti uguali a wMaxPacketSize, non è possibile determinare la fine del trasferimento. Per il completamento del trasferimento, è necessario inviare un pacchetto di lunghezza zero (ZLP) pacchetti brevi e pacchetti di lunghezza zero indica la fine di un trasferimento di dati in blocco. Le considerazioni precedenti si applicano alle API di trasferimento dati bulk non elaborati, ad esempio ux_device_class_cdc_acm_read().

## <a name="usb-device-storage-class"></a>Classe device Archiviazione USB

La classe di archiviazione del dispositivo USB consente di visualizzare un dispositivo di archiviazione incorporato nel sistema in un host USB.

La classe di archiviazione del dispositivo USB non fornisce da sola una soluzione di archiviazione. Accetta e interpreta semplicemente le richieste SCSI provenienti dall'host. Quando una di queste richieste è un comando di lettura o scrittura, richiama una chiamata predefinita a un gestore di dispositivo di archiviazione reale, ad esempio un driver di dispositivo ATA o un driver di dispositivo Flash.

Quando si inizializza la classe di archiviazione del dispositivo, alla classe viene assegnato un puntatore che contiene tutte le informazioni necessarie. Di seguito è illustrato un esempio.

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

In questo esempio le stringhe di archiviazione dei driver vengono personalizzate assegnando puntatori di stringa al parametro corrispondente. Se uno dei puntatori alla stringa viene lasciato UX_NULL, viene usata la Azure RTOS predefinita.

In questo esempio viene fornito l'ultimo indirizzo di blocco o LBA dell'unità, nonché le dimensioni del settore logico. L'LBA è il numero di settori disponibili nei supporti -1. La lunghezza del blocco è impostata su 512 nei normali supporti di archiviazione. Può essere impostato su 2048 per le unità ottiche.

L'applicazione deve passare tre puntatori di funzione di callback per consentire alla classe di archiviazione di leggere, scrivere e ottenere lo stato per il supporto.

I prototipi per le funzioni di lettura e scrittura sono illustrati nell'esempio seguente.

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

- *storage* è l'istanza della classe di archiviazione.
- *lun* è il LUN a cui viene indirizzato il comando.
- *data_pointer* è l'indirizzo del buffer da usare per la lettura o la scrittura.
- *number_blocks* è il numero di settori da leggere/scrivere.
- *lba* è l'indirizzo del settore da leggere.
- *media_status* deve essere compilato esattamente come il valore restituito del callback dello stato multimediale.

Il valore restituito può avere il valore UX_SUCCESS o UX_ERROR che indica un'operazione riuscita o non riuscita. Queste operazioni non devono restituire altri codici di errore. Se si verifica un errore in qualsiasi operazione, la classe di archiviazione richiama la funzione di callback dello stato.

Questa funzione ha il prototipo seguente.

```c
ULONG media_status( 
    VOID *storage,  
    ULONG lun,  
    ULONG media_id,  
    ULONG *media_status);
```

Il parametro chiamante media_id non è attualmente usato e deve essere sempre 0. In futuro può essere usato per distinguere più dispositivi di archiviazione o dispositivi di archiviazione con più LUN SCSI. Questa versione della classe di archiviazione non supporta più istanze della classe di archiviazione o dei dispositivi di archiviazione con più LUN SCSI.

Il valore restituito è un codice di errore SCSI che può avere il formato seguente.

- **Bit 0-7** Sense_key
- **Bit 8-15** Codice di senso aggiuntivo
- **Bit 16-23** Qualificatore del codice di senso aggiuntivo

La tabella seguente fornisce le possibili combinazioni Sense/ASC/ASCQ.

| Sense Key | ASC | Ascq | Descrizione                                       |
| --------- | --- | ---- | ------------------------------------------------- |
| 00        | 00  | 00   | NESSUN SENSO                                          |
| 01        | 17  | 01   | DATI RIPRISTINATI CON TENTATIVI                       |
| 01        | 18  | 00   | DATI RIPRISTINATI CON ECC                           |
| 02        | 04  | 01   | UNITÀ LOGICA NON PRONTA - PREPARARSI          |
| 02        | 04  | 02   | UNITÀ LOGICA NON PRONTA- INIZIALIZZAZIONE NECESSARIA |
| 02        | 04  | 04   | UNITÀ LOGICA NON PRONTA - FORMATO IN CORSO       |
| 02        | 04  | FF   | UNITÀ LOGICA NON PRONTA - IL DISPOSITIVO È OCCUPATO          |
| 02        | 06  | 00   | NON È STATA TROVATA ALCUNA POSIZIONE DI RIFERIMENTO                       |
| 02        | 08  | 00   | ERRORE DI COMUNICAZIONE DELL'UNITÀ LOGICA                |
| 02        | 08  | 01   | TIMEOUT COMUNICAZIONE UNITÀ LOGICA               |
| 02        | 08  | 80   | SOVRACCARICO DI COMUNICAZIONE DELLE UNITÀ LOGICHE                |
| 02        | 3A  | 00   | MEDIUM NOT PRESENT                                |
| 02        | 54  | 00   | ERRORE DELL'INTERFACCIA DEL SISTEMA DA USB A HOST              |
| 02        | 80  | 00   | RISORSE INSUFFICIENTI                            |
| 02        | FF  | FF   | ERRORE SCONOSCIUTO                                     |
| 03        | 02  | 00   | NESSUNA RICERCA COMPLETATA                                  |
| 03        | 03  | 00   | WRITE FAULT                                       |
| 03        | 10  | 00   | ID ERRORE CRC                                      |
| 03        | 11  | 00   | ERRORE DI LETTURA NON IRREVERSIBILE                            |
| 03        | 12  | 00   | CONTRASSEGNO INDIRIZZO NON TROVATO PER IL CAMPO ID               |
| 03        | 13  | 00   | CONTRASSEGNO DI INDIRIZZO NON TROVATO PER IL CAMPO DATI             |
| 03        | 14  | 00   | ENTITÀ REGISTRATA NON TROVATA                         |
| 03        | 30  | 01   | IMPOSSIBILE LEGGERE IL SUPPORTO - FORMATO SCONOSCIUTO               |
| 03        | 31  | 01   | COMANDO FORMAT NON RIUSCITO                             |
| 04        | 40  | NN   | ERRORE DI DIAGNOSTICA NEL COMPONENTE NN (80H-FFH)      |
| 05        | 1A  | 00   | ERRORE DI LUNGHEZZA ELENCO PARAMETRI                       |
| 05        | 20  | 00   | CODICE OPERAZIONE COMANDO NON VALIDO                    |
| 05        | 21  | 00   | INDIRIZZO DEL BLOCCO LOGICO NON COMPRESO NELL'INTERVALLO                |
| 05        | 24  | 00   | CAMPO NON VALIDO NEL PACCHETTO DI COMANDO                   |
| 05        | 25  | 00   | UNITÀ LOGICA NON SUPPORTATA                        |
| 05        | 26  | 00   | CAMPO NON VALIDO NELL'ELENCO DI PARAMETRI                   |
| 05        | 26  | 01   | PARAMETRO NON SUPPORTATO                           |
| 05        | 26  | 02   | VALORE DEL PARAMETRO NON VALIDO                           |
| 05        | 39  | 00   | SALVATAGGIO DI PARAMETRI NON SUPPORTATI                     |
| 06        | 28  | 00   | NON PRONTO PER LA TRANSIZIONE - SUPPORTO MODIFICATO     |
| 06        | 29  | 00   | ACCENSIONE A REIMPOSTAZIONE O REIMPOSTAZIONE DEL DISPOSITIVO BUS       |
| 06        | 2f  | 00   | COMANDI CANCELLATI DA UN ALTRO INIZIATORE             |
| 07        | 27  | 00   | SCRIVERE SUPPORTI PROTETTI                             |
| 0b        | 4E  | 00   | TENTATIVO DI COMANDO SOVRAPPOSTO                      |

Sono disponibili due callback facoltativi aggiuntivi che l'applicazione può implementare. uno è per rispondere a un **comando GET_STATUS_NOTIFICATION** e l'altro per rispondere al **comando SYNCHRONIZE_CACHE** comando.

Se l'applicazione vuole gestire il comando GET_STATUS_NOTIFICATION dall'host, deve implementare un callback con il prototipo seguente.

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

- *storage* è l'istanza della classe di archiviazione.
- *media_id* non è attualmente in uso. notification_class specifica la classe di notifica.
- *media_notification* deve essere impostato dall'applicazione sul buffer contenente la risposta per la notifica.
- *media_notification_length* deve essere impostato dall'applicazione per contenere la lunghezza del buffer di risposta.

Il valore restituito indica se il comando ha avuto esito positivo. Deve **essere** UX_SUCCESS o **UX_ERROR**.

Se l'applicazione non implementa questo callback, alla ricezione del comando **GET_STATUS_NOTIFICATION** USBX invierà una notifica all'host che il comando non è implementato.

Il **SYNCHRONIZE_CACHE** deve essere gestito se l'applicazione usa una cache per le scritture dall'host. Un host può inviare questo comando se sa che il dispositivo di archiviazione sta per essere disconnesso, ad esempio in Windows, se si fa clic con il pulsante destro del mouse sull'icona di un'unità flash sulla barra degli strumenti e si seleziona "Eject storage device name", Windows invia il \[ \] comando SYNCHRONIZE_CACHE **a** tale dispositivo.

Se l'applicazione vuole gestire il **comando GET_STATUS_NOTIFICATION** dall'host, deve implementare un callback con il prototipo seguente.

```c
UINT ux_slave_class_storage_media_flush(
    VOID *storage, 
    ULONG lun,
    ULONG number_blocks, 
    ULONG lba, 
    ULONG *media_status);
```

Dove:

- *storage* è l'istanza della classe di archiviazione.
- *Il parametro lun* specifica il LUN a cui viene indirizzato il comando.
- *number_blocks* specifica il numero di blocchi da sincronizzare.
- *lba* è l'indirizzo del settore del primo blocco da sincronizzare.
- *media_status* deve essere compilato esattamente come il valore restituito del callback dello stato multimediale.

Il valore restituito indica se il comando ha avuto esito positivo. Deve **essere** UX_SUCCESS o **UX_ERROR**.

### <a name="multiple-scsi-lun"></a>LUN SCSI multiplo

La classe di archiviazione del dispositivo USBX supporta più LUN. È quindi possibile creare contemporaneamente un dispositivo di archiviazione che funge da CD-ROM e un disco flash. In tal caso, l'inizializzazione sarebbe leggermente diversa. Ecco un esempio per un disco flash e un CD-ROM:

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

## <a name="usb-device-cdc-acm-class"></a>Classe USB Device CDC-ACM

La classe CDC-ACM del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come dispositivo seriale. Questa classe è basata sullo standard USB ed è un subset dello standard CDC.

Un framework di dispositivi conforme a CDC-ACM deve essere dichiarato dallo stack di dispositivi. Di seguito è riportato un esempio.

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

La classe CDC-ACM usa un framework di dispositivo composito per raggruppare le interfacce (controllo e dati). Di conseguenza, è necessario fare attenzione quando si definisce il descrittore del dispositivo. USBX si basa sul descrittore IAD per sapere internamente come associare le interfacce. Il descrittore IAD deve essere dichiarato prima delle interfacce e contenere la prima interfaccia della classe CDC-ACM e il numero di interfacce associate.

La classe CDC-ACM usa anche un descrittore funzionale di unione che esegue la stessa funzione del descrittore IAD più recente. Anche se un descrittore funzionale dell'unione deve essere dichiarato per motivi cronologici e per la compatibilità con il lato host, non viene usato da USBX.

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

I 2 parametri definiti sono puntatori di callback nelle applicazioni utente che verranno chiamati quando lo stack attiva o disattiva questa classe.

Il terzo parametro definito è un puntatore di callback all'applicazione utente che verrà chiamato in caso di modifica del parametro di stato della riga o della codifica della riga. Ad esempio, quando viene richiesta dall'host di modificare lo stato DTR in **TRUE,** viene richiamato il callback, in cui l'applicazione utente può controllare gli stati della riga tramite la funzione IOCTL per fare in modo che l'host kow sia pronto per la comunicazione.

CDC-ACM è basato su uno standard USB-IF e viene riconosciuto automaticamente dai sistemi operativi MACO e Linux. Nelle Windows, questa classe richiede un file inf per Windows versione precedente alla 10. Windows 10 non richiede file con estensione inf. Viene fornito un modello per la classe CDC-ACM, disponibile nella directory ***usbx_windows_host_files.*** Per una versione più recente Windows usare il file CDC_ACM_Template_Win7_64bit.inf (ad eccezione di Win10). Questo file deve essere modificato in base al PID/VID usato dal dispositivo. Il PID/VID sarà specifico per il cliente finale quando l'azienda e il prodotto vengono registrati con USB-IF. Nel file inf i campi da modificare si trovano qui.

```INF
[DeviceList]
%DESCRIPTION%=DriverInstall, USB\VID_8484&PID_0000

[DeviceList.NTamd64]
%DESCRIPTION%=DriverInstall, USB\VID_8484&PID_0000
```

Nel framework di dispositivo del dispositivo CDC-ACM, il PID/VID viene archiviato nel descrittore del dispositivo (vedere il descrittore del dispositivo dichiarato in precedenza).

Quando un sistema host USB individua il dispositivo USB CDC-ACM, monta una classe seriale e il dispositivo può essere usato con qualsiasi programma di terminale seriale. Per informazioni di riferimento, vedere il sistema operativo host.

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

Questa funzione viene chiamata quando un'applicazione deve eseguire varie chiamate ioctl all'interfaccia acm cdc

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe cdc.
- **ioctl_function:** funzione Ioctl da eseguire.
- **parameter**: puntatore a un parametro specifico della chiamata ioctl.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_ERROR** (0xFF) dalla funzione

### <a name="example"></a>Esempio

```c
/* Start cdc acm callback transmission. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START, &callback);

if(status != UX_SUCCESS)
    return;
```

### <a name="ioctl-functions"></a>Funzioni Ioctl:

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

Eseguire la codifica della riga del set IOCTL sull'interfaccia CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM*cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve impostare i parametri line coding.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe cdc.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING
- **parameter**: puntatore a una struttura di parametri di riga:

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

**UX_SUCCESS** (0x00) L'operazione è riuscita.

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

Eseguire ioCTL Get Line Coding sull'interfaccia CDC-ACM

### <a name="prototype"></a>Prototipo

```c
device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve ottenere i parametri line-coding.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe cdc.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_ LINE_CODING
- **parameter**: puntatore a una struttura di parametri di riga:

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

- **UX_SUCCESS** (0x00) L'operazione è riuscita.

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

Eseguire IOCTL Get Line State sull'interfaccia CDC-ACM

## <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM*cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve ottenere i parametri line state.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe cdc.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE
- **parameter**: puntatore a una struttura di parametri di riga:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER_STRUCT
{
    UCHAR ux_slave_class_cdc_acm_parameter_rts;
    UCHAR ux_slave_class_cdc_acm_parameter_dtr;
} UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER;
```

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.

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

Eseguire IOCTL Set Line State nell'interfaccia CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve ottenere i parametri line state

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe cdc.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE
- **parameter**: puntatore a una struttura di parametri di riga:

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER_STRUCT
{
    UCHAR ux_slave_class_cdc_acm_parameter_rts;
    UCHAR ux_slave_class_cdc_acm_parameter_dtr;
} UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER;
```

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.

### <a name="example"></a>Esempio

```c
/* This is to set RTS state. */

line_state.ux_slave_class_cdc_acm_parameter_rts = UX_TRUE;
status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE, &line_state);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_abort_pipe"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE

Eseguire IOCTL ABORT PIPE sull'interfaccia CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve interrompere una pipe. Ad esempio, per interrompere una scrittura in corso, UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT deve essere passato come parametro .

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe cdc.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE
- **parameter**: direzione della pipe:

```c
UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT 1

UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_RCV 2
```

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) Direzione pipe non valida.

### <a name="example"></a>Esempio

```c
/* This is to abort the Xmit pipe. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE,
    UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_transmission_start"></a>ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START

Eseguire l'avvio della trasmissione IOCTL nell'interfaccia CDC-ACM

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

- **cdc_acm**: puntatore all'istanza della classe cdc.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START
- **parameter**: puntatore alla struttura del parametro Start Transmission:

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

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_ERROR** (0xFF) Trasmissione già avviata.
- **UX_MEMORY_INSUFFICIENT** (0x12) Allocazione di memoria non riuscita.

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

Questa funzione viene chiamata quando un'applicazione vuole interrompere l'uso della trasmissione con callback.

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe cdc.
- **ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSI ON_STOP
- **parametro**: non usato

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_ERROR** (0xFF) Nessuna trasmissione in corso.

### <a name="example"></a>Esempio

```c
/* Program the stop of transmission. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP, UX_NULL);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_read"></a>ux_device_class_cdc_acm_read

Leggere dalla pipe CDC-ACM

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_cdc_acm_read( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length,  
    ULONG *actual_length);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve leggere dalla pipe di dati OUT (OUT dall'host, IN dal dispositivo). Si sta bloccando.

> [!Note]
> Questa funzione legge i dati bulk non elaborati dall'host, quindi rimane in sospeso fino a quando il buffer non è pieno o l'host termina il trasferimento con un pacchetto breve (incluso un pacchetto di lunghezza zero). Per altre informazioni, vedere la sezione [**Considerazioni generali sul trasferimento bulk.**](#general-considerations-for-bulk-transfer)

### <a name="parameters"></a>Parametri

- **cdc_acm**: puntatore all'istanza della classe cdc.
- **buffer:** indirizzo del buffer in cui verranno archiviati i dati.
- **requested_length**: lunghezza massima prevista.
- **actual_length**: lunghezza restituita nel buffer.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Il dispositivo non è più nello stato configurato.
- **UX_TRANSFER_NO_ANSWER** (0x22) Nessuna risposta dal dispositivo. Il dispositivo è stato probabilmente disconnesso mentre il trasferimento era in sospeso.

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

Questa funzione viene chiamata quando un'applicazione deve scrivere nella pipe di dati IN (IN dall'host, OUT dal dispositivo). Si sta bloccando.

### <a name="parameters"></a>Parametri

- **cdc_acm:** puntatore all'istanza della classe cdc.
- **buffer**: indirizzo del buffer in cui vengono archiviati i dati.
- **requested_length:** lunghezza del buffer da scrivere.
- **actual_length**: lunghezza restituita nel buffer dopo l'esecuzione della scrittura.

### <a name="return-value"></a>Valore restituito
- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Il dispositivo non è più nello stato configurato.
- **UX_TRANSFER_NO_ANSWER** (0x22) Nessuna risposta dal dispositivo. Il dispositivo è stato probabilmente disconnesso mentre il trasferimento era in sospeso.

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

Questa funzione viene chiamata quando un'applicazione deve scrivere nella pipe di dati IN (IN dall'host, OUT dal dispositivo). Questa funzione non è bloccante e il completamento verrà eseguito tramite un callback impostato in UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START.

### <a name="parameters"></a>Parametri

- **cdc_acm:** puntatore all'istanza della classe cdc.
- **buffer**: indirizzo del buffer in cui vengono archiviati i dati.
- **requested_length:** lunghezza del buffer da scrivere.
- **actual_length:** lunghezza restituita nel buffer dopo l'esecuzione della scrittura

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Il dispositivo non è più nello stato configurato.
- **UX_TRANSFER_NO_ANSWER** (0x22) Nessuna risposta dal dispositivo. Il dispositivo è stato probabilmente disconnesso mentre il trasferimento era in sospeso.

### <a name="example"></a>Esempio

```c
/* Write to the CDC class bulk in pipe non blocking mode. */
status = ux_device_class_cdc_acm_write_with_callback(cdc, buffer, UX_DEMO_BUFFER_SIZE);

if(status != UX_SUCCESS)
    return;
```

### <a name="usb-device-cdc-ecm-class"></a>Classe CDC-ECM del dispositivo USB

La classe CDC-ECM del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come dispositivo ethernet. Questa classe è basata sullo standard USB ed è un subset dello standard CDC.

Un framework di dispositivo conforme a CDC-ACM deve essere dichiarato dallo stack di dispositivi. Di seguito è riportato un esempio.

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

La classe CDC-ECM usa un approccio descrittore di dispositivo molto simile a CDC-ACM e richiede anche un descrittore IAD. Per la definizione, vedere la classe CDC-ACM.

Oltre al normale framework di dispositivi, CDC-ECM richiede descrittori di stringa speciali. Di seguito è illustrato un esempio.

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

Il descrittore della stringa di indirizzi MAC viene usato dalla classe CDC-ECM per rispondere alle query host sull'indirizzo MAC a cui il dispositivo risponde al protocollo TCP/IP. Può essere impostato sulla scelta del dispositivo, ma deve essere definito qui.

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

L'inizializzazione di questa classe prevede lo stesso callback di funzione per l'attivazione e la disattivazione, anche se in questo caso come esercizio sono impostate su NULL in modo che non sia eseguito alcun callback.

I parametri successivi sono per la definizione degli ID nodo. 2 I nodi sono necessari per CDC-ECM, un nodo locale e un nodo remoto. Il nodo locale specifica l'indirizzo MAC del dispositivo, mentre il nodo remoto specifica l'indirizzo MAC dell'host. Il nodo remoto deve essere uguale a quello dichiarato nel descrittore di stringa del framework di dispositivo.

La classe CDC-ECM include API incorporate per il trasferimento dei dati in entrambi i modi, ma sono nascoste all'applicazione perché l'applicazione utente comunicherà con il dispositivo USB Ethernet tramite NetX.

La classe USBX CDC-ECM è strettamente associata Azure RTOS stack di rete NetX. Un'applicazione che usa la classe NetX e USBX CDC-ECM attiverà lo stack di rete NetX nel modo consueto, ma deve anche attivare lo stack di rete USB come indicato di seguito.

```c
/* Initialize the NetX system. */
nx_system_initialize();

/* Perform the initialization of the network driver. This will initialize the USBX network layer.*/
ux_network_driver_init();
```

Lo stack di rete USB deve essere attivato una sola volta e non è specifico di CDCECM, ma è richiesto da qualsiasi classe USB che richiede servizi NetX.

La classe CDC-ECM verrà riconosciuta dagli host MAC OS e Linux. Non è tuttavia disponibile alcun driver fornito da Microsoft Windows riconoscere CDC-ECM in modo nativo. Alcuni prodotti commerciali esistono per le piattaforme Windows e forniscono il proprio file inf. Questo file dovrà essere modificato allo stesso modo del modello inf CDC-ACM in modo che corrisponda al PID/VID del dispositivo di rete USB.

## <a name="usb-device-hid-class"></a>Classe HID del dispositivo USB

La classe HID del dispositivo USB consente a un sistema host USB di connettersi a un dispositivo HID con funzionalità client HID specifiche.

La classe di dispositivo USBX HID è relativamente semplice rispetto al lato host. È strettamente legato al comportamento del dispositivo e al relativo descrittore HID.

Qualsiasi client HID richiede prima di tutto di definire un framework di dispositivo HID come nell'esempio seguente.

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

Il framework HID contiene un descrittore di interfaccia che descrive la classe HID e la sottoclasse del dispositivo HID. L'interfaccia HID può essere una classe autonoma o parte di un dispositivo composito.

Attualmente, la classe HID USBX non supporta più ID report, perché la maggior parte delle applicazioni richiede un solo ID (ID zero). Se più ID report sono una funzionalità a cui si è interessati, contattare Microsoft.

L'inizializzazione della classe HID è la seguente, usando come esempio una tastiera USB.

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

L'applicazione deve passare alla classe HID un descrittore di report HID e la relativa lunghezza. Il descrittore del report è una raccolta di elementi che descrivono il dispositivo. Per altre informazioni sulla grammatica HID, vedere la specifica della classe USB HID.

Oltre al descrittore del report, l'applicazione passa una chiamata quando si verifica un evento HID.

La classe HID USBX supporta i comandi HID standard seguenti dall'host.

| Nome comando                             | Valore | Descrizione                                      |
| ---------------------------------------- | ----- | ------------------------------------------------ |
| UX_DEVICE_CLASS_HID_COMMAND_GET_REPORT   | 0x01  | Ottenere un report dal dispositivo                     |
| UX_DEVICE_CLASS_HID_COMMAND_GET_IDLE     | 0x02  | Ottenere la frequenza di inattività dell'endpoint di interrupt |
| UX_DEVICE_CLASS_HID_COMMAND_GET_PROTOCOL | 0x03  | Ottenere il protocollo in esecuzione nel dispositivo           |
| UX_DEVICE_CLASS_HID_COMMAND_SET_REPORT   | 0x09  | Impostare un report sul dispositivo                       |
| UX_DEVICE_CLASS_HID_COMMAND_SET_IDLE     | 0x0a  | Impostare la frequenza di inattività dell'endpoint di interrupt |
| UX_DEVICE_CLASS_HID_COMMAND_SET_PROTOCOL | 0x0b  | Ottenere il protocollo in esecuzione nel dispositivo           |

Il report Get e Set sono i comandi usati più di frequente da HID per trasferire i dati tra l'host e il dispositivo. In genere l'host invia i dati sull'endpoint di controllo, ma può ricevere dati sull'endpoint di interrupt o inviando un comando GET_REPORT per recuperare i dati nell'endpoint di controllo.

La classe HID può inviare i dati all'host nell'endpoint di interrupt usando la ux_device_class_hid_event_set funzione .

### <a name="ux_device_class_hid_event_set"></a>ux_device_class_hid_event_set

Impostazione di un evento sulla classe HID

### <a name="prototype"></a>Prototipo

```c
UINT ux_device_class_hid_event_set( 
    UX_SLAVE_CLASS_HID *hid,
    UX_SLAVE_CLASS_HID_EVENT *hid_event);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando un'applicazione deve inviare un evento HID all'host. La funzione non blocca, ma inserisce semplicemente il report in una coda circolare e torna all'applicazione.

### <a name="parameters"></a>Parametri

- **hid:** puntatore all'istanza della classe hid.
- **hid_event:** puntatore alla struttura dell'evento nascosto.

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS** (0x00) L'operazione è riuscita.
- **UX_ERROR** errore (0xFF) Non è disponibile spazio nella coda circolare.

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

Il callback definito all'inizializzazione della classe HID esegue l'opposto dell'invio di un evento. Ottiene come input l'evento inviato dall'host. Il prototipo del callback è il seguente.

### <a name="hid_callback"></a>hid_callback

Recupero di un evento dalla classe HID

### <a name="prototype"></a>Prototipo

```c
UINT hid_callback(
    UX_SLAVE_CLASS_HID *hid, 
    UX_SLAVE_CLASS_HID_EVENT *hid_event);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando l'host invia un report HID all'applicazione.

### <a name="parameters"></a>Parametri

- **hid:** puntatore all'istanza della classe hid.
- **hid_event:** puntatore alla struttura dell'evento nascosto.

### <a name="example"></a>Esempio

L'esempio seguente illustra come interpretare un evento per una tastiera HID:

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
