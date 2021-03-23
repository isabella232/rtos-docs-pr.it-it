---
title: 'Capitolo 4: implementazione di USBX PictBridge'
description: UBSX supporta l'implementazione di PictBridge completa sia nell'host che nel dispositivo. PictBridge si trova sopra la classe USBX PIMA su entrambi i lati.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2ef1809dac046d49b15aba000cabed6c9fd458a3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824458"
---
# <a name="chapter-4---usbx-pictbridge-implementation"></a><span data-ttu-id="1035d-104">Capitolo 4: implementazione di USBX PictBridge</span><span class="sxs-lookup"><span data-stu-id="1035d-104">Chapter 4 - USBX Pictbridge implementation</span></span>

<span data-ttu-id="1035d-105">UBSX supporta l'implementazione di PictBridge completa sia nell'host che nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1035d-105">UBSX supports the full Pictbridge implementation both on the host and the device.</span></span> <span data-ttu-id="1035d-106">PictBridge si trova sopra la classe USBX PIMA su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="1035d-106">Pictbridge sits on top of USBX PIMA class on both sides.</span></span>

<span data-ttu-id="1035d-107">Gli standard PictBridge consentono la connessione di una fotocamera digitale o di uno smartphone direttamente a una stampante senza PC, consentendo la stampa diretta a determinate stampanti compatibili con PictBridge.</span><span class="sxs-lookup"><span data-stu-id="1035d-107">The PictBridge standards allows the connection of a digital still camera or a smart phone directly to a printer without a PC, enabling direct printing to certain Pictbridge aware printers.</span></span>

<span data-ttu-id="1035d-108">Quando una fotocamera o un telefono è connesso a una stampante, la stampante è l'host USB e la fotocamera è il dispositivo USB.</span><span class="sxs-lookup"><span data-stu-id="1035d-108">When a camera or phone is connected to a printer, the printer is the USB host and the camera is the USB device.</span></span> <span data-ttu-id="1035d-109">Con la tecnologia PictBridge, tuttavia, la fotocamera viene visualizzata come host e i comandi vengono gestiti dalla fotocamera.</span><span class="sxs-lookup"><span data-stu-id="1035d-109">However, with Pictbridge, the camera will appear as being the host and commands are driven from the camera.</span></span> <span data-ttu-id="1035d-110">La fotocamera è il server di archiviazione, ovvero la stampante il client di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1035d-110">The camera is the storage server, the printer the storage client.</span></span> <span data-ttu-id="1035d-111">La fotocamera è il client di stampa e la stampante è naturalmente il server di stampa.</span><span class="sxs-lookup"><span data-stu-id="1035d-111">The camera is the print client and the printer is of course the print server.</span></span>

<span data-ttu-id="1035d-112">PictBridge utilizza USB come livello di trasporto, ma si basa su PTP (Picture Transfer Protocol) per il protocollo di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="1035d-112">Pictbridge uses USB as a transport layer but relies on PTP (Picture Transfer Protocol) for the communication protocol.</span></span>

<span data-ttu-id="1035d-113">Di seguito è riportato un diagramma dei comandi/risposte tra il client DPS e il server DPS quando si verifica un processo di stampa:</span><span class="sxs-lookup"><span data-stu-id="1035d-113">The following is a diagram of the commands/responses between the DPS client and the DPS server when a print job occurs:</span></span>

![Comandi e risposte DPS](./media/usbx-device-stack-supplemental/dps-client-server.png)

## <a name="pictbridge-client-implementation"></a><span data-ttu-id="1035d-115">Implementazione del client PictBridge</span><span class="sxs-lookup"><span data-stu-id="1035d-115">Pictbridge client implementation</span></span>

<span data-ttu-id="1035d-116">La tecnologia PictBridge sul client richiede che lo stack di dispositivi USBX e la classe PIMA vengano eseguiti per primi.</span><span class="sxs-lookup"><span data-stu-id="1035d-116">The Pictbridge on the client requires the USBX device stack and the PIMA class to be running first.</span></span>

<span data-ttu-id="1035d-117">Un Framework di dispositivi descrive la classe PIMA nel modo seguente.</span><span class="sxs-lookup"><span data-stu-id="1035d-117">A device framework describes the PIMA class in the following way.</span></span>

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

<span data-ttu-id="1035d-118">La classe Pima usa il campo ID 0x06 e la relativa sottoclasse è 0x01 per l'immagine ancora e il protocollo è 0x01 per PIMA 15740.</span><span class="sxs-lookup"><span data-stu-id="1035d-118">The Pima class is using the ID field 0x06 and has its subclass is 0x01 for Still Image and the protocol is 0x01 for PIMA 15740.</span></span>

<span data-ttu-id="1035d-119">In questa classe sono definiti tre endpoint; due operazioni bulk per l'invio e la ricezione di dati e un interrupt per gli eventi.</span><span class="sxs-lookup"><span data-stu-id="1035d-119">Three endpoints are defined in this class; two bulks for sending/receiving data and one interrupt for events.</span></span>

<span data-ttu-id="1035d-120">A differenza di altre implementazioni di dispositivi USBX, l'applicazione PictBridge non deve definire una classe.</span><span class="sxs-lookup"><span data-stu-id="1035d-120">Unlike other USBX device implementations, the Pictbridge application does not need to define a class itself.</span></span> <span data-ttu-id="1035d-121">Richiama invece la funzione ***ux_pictbridge_dpsclient_start***.</span><span class="sxs-lookup"><span data-stu-id="1035d-121">Rather it invokes the function ***ux_pictbridge_dpsclient_start***.</span></span> <span data-ttu-id="1035d-122">Di seguito è riportato un esempio.</span><span class="sxs-lookup"><span data-stu-id="1035d-122">An example is below.</span></span>

```C
/* Initialize the Pictbridge string components. */
ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name,
    "ExpressLogic",13);

ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name,
    "EL_Pictbridge_Camera",21);

ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no, "ABC_123",7);

ux_utility_memory_copy
    (pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_dpsversions,
    "1.0 1.1",7);

pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_specific_version = 0x0100;

/* Start the Pictbridge client. */
status = ux_pictbridge_dpsclient_start(&pictbridge);

if(status != UX_SUCCESS)
    return;
```

<span data-ttu-id="1035d-123">I parametri passati al client PictBridge sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="1035d-123">The parameters passed to the pictbridge client are as follows.</span></span>

```C
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_name
    : String of Vendor name
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_product_name
    : String of product name
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_serial_no
    : String of serial number
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_dpsversions
    : String of version
pictbridge.ux_pictbridge_dpslocal.ux_pictbridge_devinfo_vendor_specific_version
    : Value set to 0x0100;
```

<span data-ttu-id="1035d-124">Il passaggio successivo consiste nel fare in modo che il dispositivo e l'host vengano sincronizzati e siano pronti per lo scambio di informazioni.</span><span class="sxs-lookup"><span data-stu-id="1035d-124">The next step is for the device and the host to synchronize and be ready to exchange information.</span></span>

<span data-ttu-id="1035d-125">Questa operazione viene eseguita attendendo un flag di evento come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1035d-125">This is done by waiting on an event flag as follows.</span></span>

```C
/* We should wait for the host and the client to discover one another. */
status = ux_utility_event_flags_get(&pictbridge.ux_pictbridge_event_flags_group,
    UX_PICTBRIDGE_EVENT_FLAG_DISCOVERY,TX_AND_CLEAR,
    &actual_flags, UX_PICTBRIDGE_EVENT_TIMEOUT);
```

<span data-ttu-id="1035d-126">Se la macchina a Stati è nello stato **DISCOVERY_COMPLETE** , il lato della fotocamera (il client DPS) raccoglierà le informazioni relative alla stampante e alle relative funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1035d-126">If the state machine is in the **DISCOVERY_COMPLETE** state, the camera side (the DPS client) will gather information regarding the printer and its capabilities.</span></span>

<span data-ttu-id="1035d-127">Se il client DPS è pronto per accettare un processo di stampa, il relativo stato verrà impostato su **UX_PICTBRIDGE_NEW_JOB_TRUE**.</span><span class="sxs-lookup"><span data-stu-id="1035d-127">If the DPS client is ready to accept a print job, its status will be set to **UX_PICTBRIDGE_NEW_JOB_TRUE**.</span></span> <span data-ttu-id="1035d-128">È possibile controllarlo di seguito.</span><span class="sxs-lookup"><span data-stu-id="1035d-128">It can be checked below.</span></span>

```C
/* Check if the printer is ready for a print job. */
if (pictbridge.ux_pictbridge_dpsclient.ux_pictbridge_devinfo_newjobok ==
    UX_PICTBRIDGE_NEW_JOB_TRUE)
/* We can print something … */
```

<span data-ttu-id="1035d-129">Successivamente, alcuni descrittori di joib di stampa devono essere riempiti come segue:</span><span class="sxs-lookup"><span data-stu-id="1035d-129">Next some print joib descriptors need to be filled as follows:</span></span>

```C
/* We can start a new job. Fill in the JobConfig and PrintInfo structures. */
jobinfo = &pictbridge.ux_pictbridge_jobinfo;

/* Attach a printinfo structure to the job. */
jobinfo -> ux_pictbridge_jobinfo_printinfo_start = &printinfo;

/* Set the default values for print job. */
jobinfo -> ux_pictbridge_jobinfo_quality =
    UX_PICTBRIDGE_QUALITIES_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_papersize =
    UX_PICTBRIDGE_PAPER_SIZES_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_papertype =
    UX_PICTBRIDGE_PAPER_TYPES_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_filetype =
    UX_PICTBRIDGE_FILE_TYPES_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_dateprint =
    UX_PICTBRIDGE_DATE_PRINTS_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_filenameprint =
    UX_PICTBRIDGE_FILE_NAME_PRINTS_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_imageoptimize =
    UX_PICTBRIDGE_IMAGE_OPTIMIZES_OFF;
jobinfo -> ux_pictbridge_jobinfo_layout =
    UX_PICTBRIDGE_LAYOUTS_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_fixedsize =
    UX_PICTBRIDGE_FIXED_SIZE_DEFAULT;
jobinfo -> ux_pictbridge_jobinfo_cropping =
    UX_PICTBRIDGE_CROPPINGS_DEFAULT;

/* Program the callback function for reading the object data. */
jobinfo -> ux_pictbridge_jobinfo_object_data_read =
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
object -> ux_device_class_pima_object_format = UX_DEVICE_CLASS_PIMA_OFC_EXIF_JPEG;
object -> ux_device_class_pima_object_compressed_size = IMAGE_LEN;
object -> ux_device_class_pima_object_offset = 0;
object -> ux_device_class_pima_object_handle_id =
    UX_PICTBRIDGE_OBJECT_HANDLE_PRINT;
object -> ux_device_class_pima_object_length = IMAGE_LEN;

/* File name is in Unicode. */
ux_utility_string_to_unicode("JPEG Image", object ->
    ux_device_class_pima_object_filename);

/* And start the job. */
status =ux_pictbridge_dpsclient_api_start_job(&pictbridge);
```

<span data-ttu-id="1035d-130">Il client PictBridge dispone ora di un processo di stampa che consente di recuperare i blocchi di immagine alla volta dall'applicazione tramite il callback definito nel campo</span><span class="sxs-lookup"><span data-stu-id="1035d-130">The Pictbridge client now has a print job to do and will fetch the image blocks at a time from the application through the callback defined in the field</span></span>

```C
jobinfo -> ux_pictbridge_jobinfo_object_data_read
```

<span data-ttu-id="1035d-131">Il prototipo della funzione è definito come segue:</span><span class="sxs-lookup"><span data-stu-id="1035d-131">The prototype of that function is defined as:</span></span>

## <a name="ux_pictbridge_jobinfo_object_data_read"></a><span data-ttu-id="1035d-132">ux_pictbridge_jobinfo_object_data_read</span><span class="sxs-lookup"><span data-stu-id="1035d-132">ux_pictbridge_jobinfo_object_data_read</span></span>

<span data-ttu-id="1035d-133">Copia di un blocco di dati dallo spazio utente per la stampa</span><span class="sxs-lookup"><span data-stu-id="1035d-133">Copying a block of data from user space for printing</span></span>

### <a name="prototype"></a><span data-ttu-id="1035d-134">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1035d-134">Prototype</span></span>

```C
UINT ux_pictbridge_jobinfo_object_data_read( 
    UX_PICTBRIDGE *pictbridge,
    UCHAR *object_buffer,  
    ULONG object_offset,  
    ULONG object_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="1035d-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1035d-135">Description</span></span>

<span data-ttu-id="1035d-136">Questa funzione viene chiamata quando il client DPS deve recuperare un blocco di dati da stampare sulla stampante PictBridge di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1035d-136">This function is called when the DPS client needs to retrieve a data block to print to the target Pictbridge printer.</span></span>

### <a name="parameters"></a><span data-ttu-id="1035d-137">Parametri</span><span class="sxs-lookup"><span data-stu-id="1035d-137">Parameters</span></span>

- <span data-ttu-id="1035d-138">**PictBridge**: puntatore all'istanza della classe PictBridge.</span><span class="sxs-lookup"><span data-stu-id="1035d-138">**pictbridge**: Pointer to the pictbridge class instance.</span></span>
- <span data-ttu-id="1035d-139">**object_buffer**: puntatore al buffer oggetto</span><span class="sxs-lookup"><span data-stu-id="1035d-139">**object_buffer**: Pointer to object buffer</span></span>
- <span data-ttu-id="1035d-140">**object_offset**: inizio della lettura del blocco di dati</span><span class="sxs-lookup"><span data-stu-id="1035d-140">**object_offset**: Where we are starting to read the data block</span></span>
- <span data-ttu-id="1035d-141">**object_length**: lunghezza da restituire</span><span class="sxs-lookup"><span data-stu-id="1035d-141">**object_length**: Length to be returned</span></span>
- <span data-ttu-id="1035d-142">**actual_length**: lunghezza effettiva restituita</span><span class="sxs-lookup"><span data-stu-id="1035d-142">**actual_length**: Actual length returned</span></span>

### <a name="return-value"></a><span data-ttu-id="1035d-143">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1035d-143">Return Value</span></span>

- <span data-ttu-id="1035d-144">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1035d-144">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="1035d-145">**UX_ERROR** (0x01) l'applicazione non è in grado di recuperare i dati.</span><span class="sxs-lookup"><span data-stu-id="1035d-145">**UX_ERROR** (0x01) The application could not retrieve data.</span></span>

### <a name="example"></a><span data-ttu-id="1035d-146">Esempio</span><span class="sxs-lookup"><span data-stu-id="1035d-146">Example</span></span>

```C
/* Copy the object data. */
UINT ux_demo_object_data_copy(
    UX_PICTBRIDGE *pictbridge,
    UCHAR *object_buffer,
    ULONG object_offset,
    ULONG object_length,
    ULONG *actual_length)
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

## <a name="pictbridge-host-implementation"></a><span data-ttu-id="1035d-147">Implementazione dell'host PictBridge</span><span class="sxs-lookup"><span data-stu-id="1035d-147">Pictbridge host implementation</span></span>

<span data-ttu-id="1035d-148">L'implementazione dell'host di PictBridge è diversa dal client.</span><span class="sxs-lookup"><span data-stu-id="1035d-148">The host implementation of Pictbridge is different from the client.</span></span>

<span data-ttu-id="1035d-149">La prima cosa da fare in un ambiente host PictBridge consiste nel registrare la classe Pima come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1035d-149">The first thing to do in a Pictbridge host environment is to register the Pima class as the example below shows:</span></span>

```C
status = ux_host_stack_class_register(_ux_system_host_class_pima_name,
    ux_host_class_pima_entry);
if(status != UX_SUCCESS)
    return;
```

<span data-ttu-id="1035d-150">Questa classe è il livello generico PTP situato tra lo stack USB e il livello PictBridge.</span><span class="sxs-lookup"><span data-stu-id="1035d-150">This class is the generic PTP layer sitting between the USB stack and the Pictbridge layer.</span></span>

<span data-ttu-id="1035d-151">Il passaggio successivo consiste nell'inizializzare i valori predefiniti di PictBridge per i servizi di stampa come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1035d-151">The next step is to initialize the Pictbridge default values for print services as follows:</span></span>

| <span data-ttu-id="1035d-152">Campo PictBridge</span><span class="sxs-lookup"><span data-stu-id="1035d-152">Pictbridge field</span></span>       | <span data-ttu-id="1035d-153">Valore</span><span class="sxs-lookup"><span data-stu-id="1035d-153">Value</span></span>                                  |
|------------------------|----------------------------------------|
| <span data-ttu-id="1035d-154">DpsVersion [0]</span><span class="sxs-lookup"><span data-stu-id="1035d-154">DpsVersion[0]</span></span>          | <span data-ttu-id="1035d-155">0x00010000</span><span class="sxs-lookup"><span data-stu-id="1035d-155">0x00010000</span></span>                             |
| <span data-ttu-id="1035d-156">DpsVersion [1]</span><span class="sxs-lookup"><span data-stu-id="1035d-156">DpsVersion[1]</span></span>          | <span data-ttu-id="1035d-157">0x00010001</span><span class="sxs-lookup"><span data-stu-id="1035d-157">0x00010001</span></span>                             |
| <span data-ttu-id="1035d-158">DpsVersion [2]</span><span class="sxs-lookup"><span data-stu-id="1035d-158">DpsVersion[2]</span></span>          | <span data-ttu-id="1035d-159">0x00000000</span><span class="sxs-lookup"><span data-stu-id="1035d-159">0x00000000</span></span>                             |
| <span data-ttu-id="1035d-160">VendorSpecificVersion</span><span class="sxs-lookup"><span data-stu-id="1035d-160">VendorSpecificVersion</span></span>  | <span data-ttu-id="1035d-161">0x00010000</span><span class="sxs-lookup"><span data-stu-id="1035d-161">0x00010000</span></span>                             |
| <span data-ttu-id="1035d-162">PrintServiceAvailable</span><span class="sxs-lookup"><span data-stu-id="1035d-162">PrintServiceAvailable</span></span>  | <span data-ttu-id="1035d-163">0x30010000</span><span class="sxs-lookup"><span data-stu-id="1035d-163">0x30010000</span></span>                             |
| <span data-ttu-id="1035d-164">Qualità [0]</span><span class="sxs-lookup"><span data-stu-id="1035d-164">Qualities[0]</span></span>           | <span data-ttu-id="1035d-165">UX_PICTBRIDGE_QUALITIES_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="1035d-165">UX_PICTBRIDGE_QUALITIES_DEFAULT</span></span>        |
| <span data-ttu-id="1035d-166">Qualità [1]</span><span class="sxs-lookup"><span data-stu-id="1035d-166">Qualities[1]</span></span>           | <span data-ttu-id="1035d-167">UX_PICTBRIDGE_QUALITIES_NORMAL</span><span class="sxs-lookup"><span data-stu-id="1035d-167">UX_PICTBRIDGE_QUALITIES_NORMAL</span></span>         |
| <span data-ttu-id="1035d-168">Qualità [2]</span><span class="sxs-lookup"><span data-stu-id="1035d-168">Qualities[2]</span></span>           | <span data-ttu-id="1035d-169">UX_PICTBRIDGE_QUALITIES_DRAFT</span><span class="sxs-lookup"><span data-stu-id="1035d-169">UX_PICTBRIDGE_QUALITIES_DRAFT</span></span>          |
| <span data-ttu-id="1035d-170">Qualità [3]</span><span class="sxs-lookup"><span data-stu-id="1035d-170">Qualities[3]</span></span>           | <span data-ttu-id="1035d-171">UX_PICTBRIDGE_QUALITIES_FINE</span><span class="sxs-lookup"><span data-stu-id="1035d-171">UX_PICTBRIDGE_QUALITIES_FINE</span></span>           |
| <span data-ttu-id="1035d-172">PaperSizes [0]</span><span class="sxs-lookup"><span data-stu-id="1035d-172">PaperSizes[0]</span></span>          | <span data-ttu-id="1035d-173">UX_PICTBRIDGE_PAPER_SIZES_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="1035d-173">UX_PICTBRIDGE_PAPER_SIZES_DEFAULT</span></span>      |
| <span data-ttu-id="1035d-174">PaperSizes [1]</span><span class="sxs-lookup"><span data-stu-id="1035d-174">PaperSizes[1]</span></span>          | <span data-ttu-id="1035d-175">UX_PICTBRIDGE_PAPER_SIZES_4IX6I</span><span class="sxs-lookup"><span data-stu-id="1035d-175">UX_PICTBRIDGE_PAPER_SIZES_4IX6I</span></span>        |
| <span data-ttu-id="1035d-176">PaperSizes [2]</span><span class="sxs-lookup"><span data-stu-id="1035d-176">PaperSizes[2]</span></span>          | <span data-ttu-id="1035d-177">UX_PICTBRIDGE_PAPER_SIZES_L</span><span class="sxs-lookup"><span data-stu-id="1035d-177">UX_PICTBRIDGE_PAPER_SIZES_L</span></span>            |
| <span data-ttu-id="1035d-178">PaperSizes [3]</span><span class="sxs-lookup"><span data-stu-id="1035d-178">PaperSizes[3]</span></span>          | <span data-ttu-id="1035d-179">UX_PICTBRIDGE_PAPER_SIZES_2L</span><span class="sxs-lookup"><span data-stu-id="1035d-179">UX_PICTBRIDGE_PAPER_SIZES_2L</span></span>           |
| <span data-ttu-id="1035d-180">PaperSizes [4]</span><span class="sxs-lookup"><span data-stu-id="1035d-180">PaperSizes[4]</span></span>          | <span data-ttu-id="1035d-181">UX_PICTBRIDGE_PAPER_SIZES_LETTER</span><span class="sxs-lookup"><span data-stu-id="1035d-181">UX_PICTBRIDGE_PAPER_SIZES_LETTER</span></span>       |
| <span data-ttu-id="1035d-182">PaperTypes [0]</span><span class="sxs-lookup"><span data-stu-id="1035d-182">PaperTypes[0]</span></span>          | <span data-ttu-id="1035d-183">UX_PICTBRIDGE_PAPER_TYPES_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="1035d-183">UX_PICTBRIDGE_PAPER_TYPES_DEFAULT</span></span>      |
| <span data-ttu-id="1035d-184">PaperTypes [1]</span><span class="sxs-lookup"><span data-stu-id="1035d-184">PaperTypes[1]</span></span>          | <span data-ttu-id="1035d-185">UX_PICTBRIDGE_PAPER_TYPES_PLAIN</span><span class="sxs-lookup"><span data-stu-id="1035d-185">UX_PICTBRIDGE_PAPER_TYPES_PLAIN</span></span>        |
| <span data-ttu-id="1035d-186">PaperTypes [2</span><span class="sxs-lookup"><span data-stu-id="1035d-186">PaperTypes[2</span></span>           | <span data-ttu-id="1035d-187">UX_PICTBRIDGE_PAPER_TYPES_PHOTO</span><span class="sxs-lookup"><span data-stu-id="1035d-187">UX_PICTBRIDGE_PAPER_TYPES_PHOTO</span></span>        |
| <span data-ttu-id="1035d-188">Tipi di tipo [0]</span><span class="sxs-lookup"><span data-stu-id="1035d-188">FileTypes[0]</span></span>           | <span data-ttu-id="1035d-189">UX_PICTBRIDGE_FILE_TYPES_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="1035d-189">UX_PICTBRIDGE_FILE_TYPES_DEFAULT</span></span>       |
| <span data-ttu-id="1035d-190">Tipi di tipo [1]</span><span class="sxs-lookup"><span data-stu-id="1035d-190">FileTypes[1]</span></span>           | <span data-ttu-id="1035d-191">UX_PICTBRIDGE_FILE_TYPES_EXIF_JPEG</span><span class="sxs-lookup"><span data-stu-id="1035d-191">UX_PICTBRIDGE_FILE_TYPES_EXIF_JPEG</span></span>     |
| <span data-ttu-id="1035d-192">Tipi di tipo [2]</span><span class="sxs-lookup"><span data-stu-id="1035d-192">FileTypes[2]</span></span>           | <span data-ttu-id="1035d-193">UX_PICTBRIDGE_FILE_TYPES_JFIF</span><span class="sxs-lookup"><span data-stu-id="1035d-193">UX_PICTBRIDGE_FILE_TYPES_JFIF</span></span>          |
| <span data-ttu-id="1035d-194">Tipi di tipo [3]</span><span class="sxs-lookup"><span data-stu-id="1035d-194">FileTypes[3]</span></span>           | <span data-ttu-id="1035d-195">UX_PICTBRIDGE_FILE_TYPES_DPOF</span><span class="sxs-lookup"><span data-stu-id="1035d-195">UX_PICTBRIDGE_FILE_TYPES_DPOF</span></span>          |
| <span data-ttu-id="1035d-196">DatePrints [0]</span><span class="sxs-lookup"><span data-stu-id="1035d-196">DatePrints[0]</span></span>          | <span data-ttu-id="1035d-197">UX_PICTBRIDGE_DATE_PRINTS_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="1035d-197">UX_PICTBRIDGE_DATE_PRINTS_DEFAULT</span></span>      |
| <span data-ttu-id="1035d-198">DatePrints [1]</span><span class="sxs-lookup"><span data-stu-id="1035d-198">DatePrints[1]</span></span>          | <span data-ttu-id="1035d-199">UX_PICTBRIDGE_DATE_PRINTS_OFF</span><span class="sxs-lookup"><span data-stu-id="1035d-199">UX_PICTBRIDGE_DATE_PRINTS_OFF</span></span>          |
| <span data-ttu-id="1035d-200">DatePrints [2]</span><span class="sxs-lookup"><span data-stu-id="1035d-200">DatePrints[2]</span></span>          | <span data-ttu-id="1035d-201">UX_PICTBRIDGE_DATE_PRINTS_ON</span><span class="sxs-lookup"><span data-stu-id="1035d-201">UX_PICTBRIDGE_DATE_PRINTS_ON</span></span>           |
| <span data-ttu-id="1035d-202">FileNamePrints [0]</span><span class="sxs-lookup"><span data-stu-id="1035d-202">FileNamePrints[0]</span></span>      | <span data-ttu-id="1035d-203">UX_PICTBRIDGE_FILE_NAME_PRINTS_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="1035d-203">UX_PICTBRIDGE_FILE_NAME_PRINTS_DEFAULT</span></span> |
| <span data-ttu-id="1035d-204">FileNamePrints [1]</span><span class="sxs-lookup"><span data-stu-id="1035d-204">FileNamePrints[1]</span></span>      | <span data-ttu-id="1035d-205">UX_PICTBRIDGE_FILE_NAME_PRINTS_OFF</span><span class="sxs-lookup"><span data-stu-id="1035d-205">UX_PICTBRIDGE_FILE_NAME_PRINTS_OFF</span></span>     |
| <span data-ttu-id="1035d-206">FileNamePrints [2]</span><span class="sxs-lookup"><span data-stu-id="1035d-206">FileNamePrints[2]</span></span>      | <span data-ttu-id="1035d-207">UX_PICTBRIDGE_FILE_NAME_PRINTS_ON</span><span class="sxs-lookup"><span data-stu-id="1035d-207">UX_PICTBRIDGE_FILE_NAME_PRINTS_ON</span></span>      |
| <span data-ttu-id="1035d-208">ImageOptimizes [0]</span><span class="sxs-lookup"><span data-stu-id="1035d-208">ImageOptimizes[0]</span></span>      | <span data-ttu-id="1035d-209">UX_PICTBRIDGE_IMAGE_OPTIMIZES_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="1035d-209">UX_PICTBRIDGE_IMAGE_OPTIMIZES_DEFAULT</span></span>  |
| <span data-ttu-id="1035d-210">ImageOptimizes [1]</span><span class="sxs-lookup"><span data-stu-id="1035d-210">ImageOptimizes[1]</span></span>      | <span data-ttu-id="1035d-211">UX_PICTBRIDGE_IMAGE_OPTIMIZES_OFF</span><span class="sxs-lookup"><span data-stu-id="1035d-211">UX_PICTBRIDGE_IMAGE_OPTIMIZES_OFF</span></span>      |
| <span data-ttu-id="1035d-212">ImageOptimizes [2]</span><span class="sxs-lookup"><span data-stu-id="1035d-212">ImageOptimizes[2]</span></span>      | <span data-ttu-id="1035d-213">UX_PICTBRIDGE_IMAGE_OPTIMIZES_ON</span><span class="sxs-lookup"><span data-stu-id="1035d-213">UX_PICTBRIDGE_IMAGE_OPTIMIZES_ON</span></span>       |
| <span data-ttu-id="1035d-214">Layout [0]</span><span class="sxs-lookup"><span data-stu-id="1035d-214">Layouts[0]</span></span>             | <span data-ttu-id="1035d-215">UX_PICTBRIDGE_LAYOUTS_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="1035d-215">UX_PICTBRIDGE_LAYOUTS_DEFAULT</span></span>          |
| <span data-ttu-id="1035d-216">Layout [1]</span><span class="sxs-lookup"><span data-stu-id="1035d-216">Layouts[1]</span></span>             | <span data-ttu-id="1035d-217">UX_PICTBRIDGE_LAYOUTS_1_UP_BORDER</span><span class="sxs-lookup"><span data-stu-id="1035d-217">UX_PICTBRIDGE_LAYOUTS_1_UP_BORDER</span></span>      |
| <span data-ttu-id="1035d-218">Layout [2]</span><span class="sxs-lookup"><span data-stu-id="1035d-218">Layouts[2]</span></span>             | <span data-ttu-id="1035d-219">UX_PICTBRIDGE_LAYOUTS_INDEX_PRINT</span><span class="sxs-lookup"><span data-stu-id="1035d-219">UX_PICTBRIDGE_LAYOUTS_INDEX_PRINT</span></span>      |
| <span data-ttu-id="1035d-220">Layout [3]</span><span class="sxs-lookup"><span data-stu-id="1035d-220">Layouts[3]</span></span>             | <span data-ttu-id="1035d-221">UX_PICTBRIDGE_LAYOUTS_1_UP_BORDERLESS</span><span class="sxs-lookup"><span data-stu-id="1035d-221">UX_PICTBRIDGE_LAYOUTS_1_UP_BORDERLESS</span></span>  |
| <span data-ttu-id="1035d-222">FixedSizes [0]</span><span class="sxs-lookup"><span data-stu-id="1035d-222">FixedSizes[0]</span></span>          | <span data-ttu-id="1035d-223">UX_PICTBRIDGE_FIXED_SIZE_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="1035d-223">UX_PICTBRIDGE_FIXED_SIZE_DEFAULT</span></span>       |
| <span data-ttu-id="1035d-224">FixedSizes [1]</span><span class="sxs-lookup"><span data-stu-id="1035d-224">FixedSizes[1]</span></span>          | <span data-ttu-id="1035d-225">UX_PICTBRIDGE_FIXED_SIZE_35IX5I</span><span class="sxs-lookup"><span data-stu-id="1035d-225">UX_PICTBRIDGE_FIXED_SIZE_35IX5I</span></span>        |
| <span data-ttu-id="1035d-226">FixedSizes [2]</span><span class="sxs-lookup"><span data-stu-id="1035d-226">FixedSizes[2]</span></span>          | <span data-ttu-id="1035d-227">UX_PICTBRIDGE_FIXED_SIZE_4IX6I</span><span class="sxs-lookup"><span data-stu-id="1035d-227">UX_PICTBRIDGE_FIXED_SIZE_4IX6I</span></span>         |
| <span data-ttu-id="1035d-228">FixedSizes [3]</span><span class="sxs-lookup"><span data-stu-id="1035d-228">FixedSizes[3]</span></span>          | <span data-ttu-id="1035d-229">UX_PICTBRIDGE_FIXED_SIZE_5IX7I</span><span class="sxs-lookup"><span data-stu-id="1035d-229">UX_PICTBRIDGE_FIXED_SIZE_5IX7I</span></span>         |
| <span data-ttu-id="1035d-230">FixedSizes [4]</span><span class="sxs-lookup"><span data-stu-id="1035d-230">FixedSizes[4]</span></span>          | <span data-ttu-id="1035d-231">UX_PICTBRIDGE_FIXED_SIZE_7CMX10CM</span><span class="sxs-lookup"><span data-stu-id="1035d-231">UX_PICTBRIDGE_FIXED_SIZE_7CMX10CM</span></span>      |
| <span data-ttu-id="1035d-232">FixedSizes [5]</span><span class="sxs-lookup"><span data-stu-id="1035d-232">FixedSizes[5]</span></span>          | <span data-ttu-id="1035d-233">UX_PICTBRIDGE_FIXED_SIZE_LETTER</span><span class="sxs-lookup"><span data-stu-id="1035d-233">UX_PICTBRIDGE_FIXED_SIZE_LETTER</span></span>        |
| <span data-ttu-id="1035d-234">FixedSizes [6]</span><span class="sxs-lookup"><span data-stu-id="1035d-234">FixedSizes[6]</span></span>          | <span data-ttu-id="1035d-235">UX_PICTBRIDGE_FIXED_SIZE_A4</span><span class="sxs-lookup"><span data-stu-id="1035d-235">UX_PICTBRIDGE_FIXED_SIZE_A4</span></span>            |
| <span data-ttu-id="1035d-236">Ritaglio [0]</span><span class="sxs-lookup"><span data-stu-id="1035d-236">Croppings[0]</span></span>           | <span data-ttu-id="1035d-237">UX_PICTBRIDGE_CROPPINGS_DEFAULT</span><span class="sxs-lookup"><span data-stu-id="1035d-237">UX_PICTBRIDGE_CROPPINGS_DEFAULT</span></span>        |
| <span data-ttu-id="1035d-238">Ritaglio [1]</span><span class="sxs-lookup"><span data-stu-id="1035d-238">Croppings[1]</span></span>           | <span data-ttu-id="1035d-239">UX_PICTBRIDGE_CROPPINGS_OFF</span><span class="sxs-lookup"><span data-stu-id="1035d-239">UX_PICTBRIDGE_CROPPINGS_OFF</span></span>            |
| <span data-ttu-id="1035d-240">Ritaglio [2]</span><span class="sxs-lookup"><span data-stu-id="1035d-240">Croppings[2]</span></span>           | <span data-ttu-id="1035d-241">UX_PICTBRIDGE_CROPPINGS_ON</span><span class="sxs-lookup"><span data-stu-id="1035d-241">UX_PICTBRIDGE_CROPPINGS_ON</span></span>             |

<span data-ttu-id="1035d-242">La macchina a Stati dell'host DPS verrà impostata su inattivo e sarà pronta per accettare un nuovo processo di stampa.</span><span class="sxs-lookup"><span data-stu-id="1035d-242">The state machine of the DPS host will be set to Idle and ready to accept a new print job.</span></span>

<span data-ttu-id="1035d-243">È ora possibile avviare la porzione host di PictBridge come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1035d-243">The host portion of Pictbridge can now be started as the example below shows:</span></span>

```C
/* Activate the pictbridge dpshost. */
status = ux_pictbridge_dpshost_start(&pictbridge, pima);

if (status != UX_SUCCESS)
    return;
```

<span data-ttu-id="1035d-244">La funzione host PictBridge richiede un callback quando i dati sono pronti per la stampa.</span><span class="sxs-lookup"><span data-stu-id="1035d-244">The Pictbridge host function requires a callback when data is ready to be printed.</span></span> <span data-ttu-id="1035d-245">Questa operazione viene eseguita passando un puntatore a funzione nella struttura dell'host PictBridge come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1035d-245">This is accomplished by passing a function pointer in the pictbridge host structure as follows.</span></span>

```C
/* Set a callback when an object is being received. */
pictbridge.ux_pictbridge_application_object_data_write =
    tx_demo_object_data_write;
```

<span data-ttu-id="1035d-246">Questa funzione presenta le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="1035d-246">This function has the following properties.</span></span>

## <a name="ux_pictbridge_application_object_data_write"></a><span data-ttu-id="1035d-247">ux_pictbridge_application_object_data_write</span><span class="sxs-lookup"><span data-stu-id="1035d-247">ux_pictbridge_application_object_data_write</span></span>

<span data-ttu-id="1035d-248">Scrittura di un blocco di dati per la stampa</span><span class="sxs-lookup"><span data-stu-id="1035d-248">Writing a block of data for printing</span></span>

### <a name="prototype"></a><span data-ttu-id="1035d-249">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1035d-249">Prototype</span></span>

```C
UINT ux_pictbridge_application_object_data_write(
    UX_PICTBRIDGE *pictbridge, 
    UCHAR *object_buffer,
    ULONG offset,
    ULONG total_length,
    ULONG length);
```

### <a name="description"></a><span data-ttu-id="1035d-250">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1035d-250">Description</span></span>

<span data-ttu-id="1035d-251">Questa funzione viene chiamata quando il server DPS deve recuperare un blocco di dati dal client DPS per la stampa sulla stampante locale.</span><span class="sxs-lookup"><span data-stu-id="1035d-251">This function is called when the DPS server needs to retrieve a data block from the DPS client to print to the local printer.</span></span>

### <a name="parameters"></a><span data-ttu-id="1035d-252">Parametri</span><span class="sxs-lookup"><span data-stu-id="1035d-252">Parameters</span></span>

- <span data-ttu-id="1035d-253">**PictBridge**: puntatore all'istanza della classe PictBridge.</span><span class="sxs-lookup"><span data-stu-id="1035d-253">**pictbridge**: Pointer to the pictbridge class instance.</span></span>
- <span data-ttu-id="1035d-254">**object_buffer**: puntatore al buffer oggetto</span><span class="sxs-lookup"><span data-stu-id="1035d-254">**object_buffer**: Pointer to object buffer</span></span>
- <span data-ttu-id="1035d-255">**object_offset**: inizio della lettura del blocco di dati</span><span class="sxs-lookup"><span data-stu-id="1035d-255">**object_offset**: Where we are starting to read the data block</span></span>
- <span data-ttu-id="1035d-256">**TOTAL_LENGTH**: lunghezza intera dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="1035d-256">**total_length**: Entire length of object</span></span>
- <span data-ttu-id="1035d-257">**length**: lunghezza del buffer</span><span class="sxs-lookup"><span data-stu-id="1035d-257">**length**: Length of this buffer</span></span>

### <a name="return-value"></a><span data-ttu-id="1035d-258">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1035d-258">Return Value</span></span>

- <span data-ttu-id="1035d-259">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1035d-259">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="1035d-260">**UX_ERROR** (0x01) l'applicazione non è in grado di stampare i dati.</span><span class="sxs-lookup"><span data-stu-id="1035d-260">**UX_ERROR** (0x01) The application could not print data.</span></span>

### <a name="example"></a><span data-ttu-id="1035d-261">Esempio</span><span class="sxs-lookup"><span data-stu-id="1035d-261">Example</span></span>

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
