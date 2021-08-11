---
title: Implementazione di USBX Pictbridge
description: UBSX supporta l'implementazione completa di Pictbridge sia nell'host che nel dispositivo. Pictbridge si trova sopra la classe USBX PIMA su entrambi i lati.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9f4ba97741d2fc5f93afe6866b9ae6e9dc1e98a977eb3d6050c4a7489804c93c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790710"
---
# <a name="chapter-4-usbx-pictbridge-implementation"></a>Capitolo 4: Implementazione di USBX Pictbridge

UBSX supporta l'implementazione completa di Pictbridge sia nell'host che nel dispositivo. Pictbridge si trova sopra la classe USBX PIMA su entrambi i lati. 

Gli standard di PictBridge consentono la connessione di una fotocamera digitale o di uno smart phone direttamente a una stampante senza PC, consentendo la stampa diretta a determinate stampanti in grado di riconoscere Pictbridge.

Quando una fotocamera o un telefono è connesso a una stampante, la stampante è l'host USB e la fotocamera è il dispositivo USB. Tuttavia, con Pictbridge, la fotocamera apparirà come l'host e i comandi vengono guidati dalla fotocamera. La fotocamera è il server di archiviazione, la stampante del client di archiviazione. La fotocamera è il client di stampa e la stampante è ovviamente il server di stampa.

Pictbridge usa USB come livello di trasporto, ma si basa su PTP (Picture Transfer Protocol) per il protocollo di comunicazione.

Di seguito è riportato un diagramma dei comandi/risposte tra il client DPS e il server DPS quando si verifica un processo di stampa.

![Diagramma dei comandi/risposte tra il client D P S e il server D P S quando si verifica un processo di stampa.](./media/usbx-host-stack-supplemental/dps-client-server.png)

## <a name="pictbridge-client-implementation"></a>Implementazione del client Pictbridge

Pictbridge nel client richiede che lo stack di dispositivi USBX e la classe PIMA siano in esecuzione per primi.

Un framework di dispositivi descrive la classe PIMA nel modo seguente.

```C
UCHAR device_framework_full_speed[] =
{
    /* Device descriptor */
       0x12, 0x01, 0x10, 0x01, 0x00, 0x00, 0x00, 0x20,
       0xA9, 0x04, 0xB6, 0x30, 0x00, 0x00, 0x00, 0x00,
       0x00, 0x01,
    /* Configuration descriptor */
       0x09, 0x02, 0x27, 0x00, 0x01, 0x01, 0x00, 0xc0, 0x32,
    /* Interface descriptor */
       0x09, 0x04, 0x00, 0x00, 0x03, 0x06, 0x01, 0x01, 0x00,
    /* Endpoint descriptor (Bulk Out) */
       0x07, 0x05, 0x01, 0x02, 0x40, 0x00, 0x00,
    /* Endpoint descriptor (Bulk In) */
       0x07, 0x05, 0x82, 0x02, 0x40, 0x00, 0x00,
    /* Endpoint descriptor (Interrupt) */
       0x07, 0x05, 0x83, 0x03, 0x08, 0x00, 0x60
};
```

La classe Pima usa il campo ID 0x06 e ha la sottoclasse 0x01 per Still Image e il protocollo è 0x01 per PIMA 15740.

In questa classe sono definiti 3 endpoint, 2 bulk per l'invio/ricezione di dati e un interrupt per gli eventi.

A differenza di altre implementazioni di dispositivi USBX, l'applicazione Pictbridge non deve definire una classe. Richiama invece la funzione ***ux_pictbridge_dpsclient_start***. Di seguito è riportato un esempio:

```C
/* Initialize the Pictbridge string components. */
ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name,
    "Azure RTOS",10);
ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name,
    "EL_Pictbridge_Camera",21);
ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no, "ABC_123",7);
ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_dpsversions,
    "1.0 1.1",7);

pictbridge.ux_pictbridge_dpslocal.
    ux_pictbridge_devinfo_vendor_specific_version = 0x0100;

/* Start the Pictbridge client. */
status = ux_pictbridge_dpsclient_start(&pictbridge);

if(status != UX_SUCCESS)
    return;
```

I parametri passati al client di Pictbridge sono i seguenti:

```C
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name
    : String of Vendor name pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name
    : String of product name pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no,
    : String of serial number pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_dpsversions
    : String of version pictbridge.ux_pictbridge_dpslocal. ux_pictbridge_devinfo_vendor_specific_version
    : Value set to 0x0100;
```

Il passaggio successivo consiste nel sincronizzare il dispositivo e l'host e prepararsi per lo scambio di informazioni.

Questa operazione viene eseguita attendendo un flag di evento come segue:

```C
/* We should wait for the host and the client to discover one another. */
status = ux_utility_event_flags_get
    (&pictbridge.ux_pictbridge_event_flags_group,
    UX_PICTBRIDGE_EVENT_FLAG_DISCOVERY,TX_AND_CLEAR, &actual_flags,
    UX_PICTBRIDGE_EVENT_TIMEOUT);
```

Se la macchina a stati è nello stato **DISCOVERY_COMPLETE,** il lato fotocamera (client DPS) raccoglierà informazioni relative alla stampante e alle relative funzionalità.

Se il client DPS è pronto ad accettare un processo di stampa, il relativo stato verrà impostato **su UX_PICTBRIDGE_NEW_JOB_TRUE**. È possibile verificarlo di seguito:

```C
/* Check if the printer is ready for a print job. */
if (pictbridge.ux_pictbridge_dpsclient.ux_pictbridge_devinfo_newjobok ==
    UX_PICTBRIDGE_NEW_JOB_TRUE)

    /* We can print something … */
```

Successivamente, alcuni descrittori di joib di stampa devono essere compilati come segue:

```C
/* We can start a new job. Fill in the JobConfig and PrintInfo structures. */
jobinfo = &pictbridge.ux_pictbridge_jobinfo;

/* Attach a printinfo structure to the job. */
jobinfo ->ux_pictbridge_jobinfo_printinfo_start = &printinfo;

/* Set the default values for print job. */
jobinfo ->ux_pictbridge_jobinfo_quality =
    UX_PICTBRIDGE_QUALITIES_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_papersize =
    UX_PICTBRIDGE_PAPER_SIZES_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_papertype =
    UX_PICTBRIDGE_PAPER_TYPES_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_filetype =
    UX_PICTBRIDGE_FILE_TYPES_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_dateprint =
    UX_PICTBRIDGE_DATE_PRINTS_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_filenameprint =
    UX_PICTBRIDGE_FILE_NAME_PRINTS_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_imageoptimize =
    UX_PICTBRIDGE_IMAGE_OPTIMIZES_OFF;
jobinfo ->ux_pictbridge_jobinfo_layout =
    UX_PICTBRIDGE_LAYOUTS_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_fixedsize =
    UX_PICTBRIDGE_FIXED_SIZE_DEFAULT;
jobinfo ->ux_pictbridge_jobinfo_cropping =
    UX_PICTBRIDGE_CROPPINGS_DEFAULT;

/* Program the callback function for reading the object data. */
jobinfo ->ux_pictbridge_jobinfo_object_data_read =
    ux_demo_object_data_copy;

/* This is a demo, the fileID is hardwired (1 and 2 for scripts, 3 for photo to be printed. */

printinfo.ux_pictbridge_printinfo_fileid =
    UX_PICTBRIDGE_OBJECT_HANDLE_PRINT;

ux_utility_memory_copy(printinfo.ux_pictbridge_printinfo_filename,
    "Pictbridge demo file", 20);
ux_utility_memory_copy(printinfo.ux_pictbridge_printinfo_date, "01/01/2008",
    10);

/* Fill in the object info to be printed. First get the pointer to the object container in the job info structure. */
object = (UX_SLAVE_CLASS_PIMA_OBJECT *) jobinfo ->
    ux_pictbridge_jobinfo_object;

/* Store the object format: JPEG picture. */
object ->ux_device_class_pima_object_format = UX_DEVICE_CLASS_PIMA_OFC_EXIF_JPEG;
object ->ux_device_class_pima_object_compressed_size = IMAGE_LEN; object ->ux_device_class_pima_object_offset = 0;
object ->ux_device_class_pima_object_handle_id =
    UX_PICTBRIDGE_OBJECT_HANDLE_PRINT;
object ->ux_device_class_pima_object_length = IMAGE_LEN;

/* File name is in Unicode. */
ux_utility_string_to_unicode("JPEG Image", object ->
    ux_device_class_pima_object_filename);

/* And start the job. */
status =ux_pictbridge_dpsclient_api_start_job(&pictbridge);
```

Il client Di Pictbridge ha ora un processo di stampa da eseguire e recupererà i blocchi immagine alla volta dall'applicazione tramite il callback definito nel campo .

```C
jobinfo ->ux_pictbridge_jobinfo_object_data_read
```

Il prototipo di tale funzione viene definito come segue.

## <a name="ux_pictbridge_jobinfo_object_data_read"></a>ux_pictbridge_jobinfo_object_data_read

Copia di un blocco di dati dallo spazio utente per la stampa.

### <a name="prototype"></a>Prototipo

```C
UINT **ux_pictbridge_jobinfo_object_data_read(
    UX_PICTBRIDGE *pictbridge,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length,
    ULONG *actual_length)
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando il client DPS deve recuperare un blocco di dati da stampare sulla stampante Pictbridge di destinazione.

### <a name="parameters"></a>Parametri

- **pictbridge:** puntatore all'istanza della classe pictbridge.
- **object_buffer:** puntatore al buffer dell'oggetto
- **object_offset:** dove si inizia a leggere il blocco di dati
- **object_length:** lunghezza da restituire
- **actual_length:** lunghezza effettiva restituita

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS:**(0x00) L'operazione è riuscita.
- **UX_ERROR**: (0x01) L'applicazione non è stata in grado di recuperare i dati.

### <a name="example"></a>Esempio

```C
/* Copy the object data. */

UINT ux_demo_object_data_copy(UX_PICTBRIDGE *pictbridge,UCHAR *object_buffer,
    ULONG object_offset, ULONG object_length, ULONG *actual_length)
{
    /* Copy the demanded object data portion. */
    ux_utility_memory_copy(object_buffer, image + object_offset,
        object_length);

    /* Update the actual length. */
    *actual_length = object_length;

    /* We have copied the requested data. Return OK. */
    return(UX_SUCCESS);
}
```

## <a name="pictbridge-host-implementation"></a>Implementazione dell'host Di Pictbridge

L'implementazione host di Pictbridge è diversa dal client.

La prima operazione da eseguire in un ambiente host Di Pictbridge è registrare la classe Pima come illustrato nell'esempio seguente:

```C
status = ux_host_stack_class_register(ux_system_host_class_pima_name,
    ux_host_class_pima_entry);
if(status != UX_SUCCESS)
    return;
```

Questa classe è il livello PTP generico tra lo stack host USB e il livello Pictbridge.

Il passaggio successivo consiste nell'inizializzare i valori predefiniti di Pictbridge per i servizi di stampa come indicato di seguito.

| Campo di Pictbridge       | Valore                                  |
|------------------------|----------------------------------------|
| DpsVersion[0]          | 0x00010000                             |
| DpsVersion[1]          | 0x00010001                             |
| DpsVersion[2]          | 0x00000000                             |
| VendorSpecificVersion  | 0x00010000                             |
| PrintServiceAvailable  | 0x30010000                             |
| Qualità[0]           | UX_PICTBRIDGE_QUALITIES_DEFAULT        |
| Qualità[1]           | UX_PICTBRIDGE_QUALITIES_NORMAL         |
| Qualità[2]           | UX_PICTBRIDGE_QUALITIES_DRAFT          |
| Qualità[3]           | UX_PICTBRIDGE_QUALITIES_FINE           |
| PaperSizes[0]          | UX_PICTBRIDGE_PAPER_SIZES_DEFAULT      |
| PaperSizes[1]          | UX_PICTBRIDGE_PAPER_SIZES_4IX6I        |
| PaperSizes[2]          | UX_PICTBRIDGE_PAPER_SIZES_L            |
| PaperSizes[3]          | UX_PICTBRIDGE_PAPER_SIZES_2L           |
| PaperSizes[4]          | UX_PICTBRIDGE_PAPER_SIZES_LETTER       |
| PaperTypes[0]          | UX_PICTBRIDGE_PAPER_TYPES_DEFAULT      |
| PaperTypes[1]          | UX_PICTBRIDGE_PAPER_TYPES_PLAIN        |
| PaperTypes[2]          | UX_PICTBRIDGE_PAPER_TYPES_PHOTO        |
| FileTypes[0]           | UX_PICTBRIDGE_FILE_TYPES_DEFAULT       |
| FileTypes[1]           | UX_PICTBRIDGE_FILE_TYPES_EXIF_JPEG     |
| FileTypes[2]           | UX_PICTBRIDGE_FILE_TYPES_JFIF          |
| FileTypes[3]           | UX_PICTBRIDGE_FILE_TYPES_DPOF          |
| DatePrints[0]          | UX_PICTBRIDGE_DATE_PRINTS_DEFAULT      |
| DatePrints[1]          | UX_PICTBRIDGE_DATE_PRINTS_OFF          |
| DatePrints[2]          | UX_PICTBRIDGE_DATE_PRINTS_ON           |
| FileNamePrints[0]      | UX_PICTBRIDGE_FILE_NAME_PRINTS_DEFAULT |
| FileNamePrints[1]      | UX_PICTBRIDGE_FILE_NAME_PRINTS_OFF     |
| FileNamePrints[2]      | UX_PICTBRIDGE_FILE_NAME_PRINTS_ON      |
| ImageOptimizes[0]      | UX_PICTBRIDGE_IMAGE_OPTIMIZES_DEFAULT  |
| ImageOptimizes[1]      | UX_PICTBRIDGE_IMAGE_OPTIMIZES_OFF      |
| ImageOptimizes[2]      | UX_PICTBRIDGE_IMAGE_OPTIMIZES_ON       |
| Layout[0]             | UX_PICTBRIDGE_LAYOUTS_DEFAULT          |
| layout[1]             | UX_PICTBRIDGE_LAYOUTS_1_UP_BORDER      |
| layout[2]             | UX_PICTBRIDGE_LAYOUTS_INDEX_PRINT      |
| layout[3]             | UX_PICTBRIDGE_LAYOUTS_1_UP_BORDERLESS  |
| FixedSizes[0]          | UX_PICTBRIDGE_FIXED_SIZE_DEFAULT       |
| FixedSizes[1]          | UX_PICTBRIDGE_FIXED_SIZE_35IX5I        |
| FixedSizes[2]          | UX_PICTBRIDGE_FIXED_SIZE_4IX6I         |
| FixedSizes[3]          | UX_PICTBRIDGE_FIXED_SIZE_5IX7I         |
| FixedSizes[4]          | UX_PICTBRIDGE_FIXED_SIZE_7CMX10CM      |
| FixedSizes[5]          | UX_PICTBRIDGE_FIXED_SIZE_LETTER        |
| FixedSizes[6]          | UX_PICTBRIDGE_FIXED_SIZE_A4            |
| Ritaglio[0]           | UX_PICTBRIDGE_CROPPINGS_DEFAULT        |
| Ritaglio[1]           | UX_PICTBRIDGE_CROPPINGS_OFF            |
| Ritaglio[2]           | UX_PICTBRIDGE_CROPPINGS_ON             |

La macchina a stati dell'host DPS verrà impostata su Inattivo e pronta ad accettare un nuovo processo di stampa.

La parte host di Pictbridge può ora essere avviata come illustrato nell'esempio seguente.

```C
/* Activate the pictbridge dpshost. */

status = ux_pictbridge_dpshost_start(&pictbridge, pima);
if (status != UX_SUCCESS)
    return;
```

La funzione host di Pictbridge richiede un callback quando i dati sono pronti per la stampa. Questa operazione viene eseguita passando un puntatore a funzione nella struttura host di Pictbridge come indicato di seguito.

```C
/* Set a callback when an object is being received. */

pictbridge.ux_pictbridge_application_object_data_write =
    tx_demo_object_data_write;
```

Questa funzione ha le proprietà seguenti:

## <a name="ux_pictbridge_application_object_data_write"></a>ux_pictbridge_application_object_data_write

Scrittura di un blocco di dati per la stampa.

### <a name="prototype"></a>Prototipo

```C
UINT **ux_pictbridge_application_object_data_write(
    UX_PICTBRIDGE *pictbridge,
    UCHAR *object_buffer,
    ULONG offset,
    ULONG total_length,
    ULONG length);
```

### <a name="description"></a>Descrizione

Questa funzione viene chiamata quando il server DPS deve recuperare un blocco di dati dal client DPS per stampare sulla stampante locale.

### <a name="parameters"></a>Parametri

- **pictbridge:** puntatore all'istanza della classe pictbridge.
- **object_buffer:** puntatore al buffer dell'oggetto
- **object_offset:** dove si inizia a leggere il blocco di dati
- **total_length:** lunghezza intera dell'oggetto
- **length**: lunghezza del buffer

### <a name="return-value"></a>Valore restituito

- **UX_SUCCESS:**(0x00) L'operazione è riuscita.
- **UX_ERROR**: (0x01) L'applicazione non è stata in grado di stampare i dati.

### <a name="example"></a>Esempio

```C
/* Copy the object data. */

UINT tx_demo_object_data_write(UX_PICTBRIDGE *pictbridge,
    UCHAR *object_buffer, ULONG offset, ULONG total_length, ULONG length);
{
    UINT status;

    /* Send the data to the local printer. */
    status = local_printer_data_send(object_buffer, length);

    /* We have printed the requested data. Return status. */
    return(status);
}
```
