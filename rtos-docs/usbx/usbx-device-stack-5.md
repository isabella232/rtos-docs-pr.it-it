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
# <a name="chapter-5---usbx-device-class-considerations"></a><span data-ttu-id="1b8ca-103">Capitolo 5-considerazioni sulle classi di dispositivi USBX</span><span class="sxs-lookup"><span data-stu-id="1b8ca-103">Chapter 5 - USBX Device Class Considerations</span></span>

## <a name="device-class-registration"></a><span data-ttu-id="1b8ca-104">Registrazione classe dispositivo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-104">Device Class registration</span></span>

<span data-ttu-id="1b8ca-105">Ogni classe di dispositivo segue lo stesso principio per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-105">Each device class follows the same principle for registration.</span></span> <span data-ttu-id="1b8ca-106">Una struttura che contiene parametri di classe specifici viene passata alla funzione di inizializzazione della classe.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-106">A structure containing specific class parameters is passed to the class initialize function.</span></span>

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

<span data-ttu-id="1b8ca-107">Ogni classe può registrare, facoltativamente, una funzione di callback quando viene attivata un'istanza della classe.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-107">Each class can register, optionally, a callback function when a instance of the class gets activated.</span></span> <span data-ttu-id="1b8ca-108">Il callback viene quindi chiamato dallo stack del dispositivo per informare l'applicazione che è stata creata un'istanza.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-108">The callback is then called by the device stack to inform the application that an instance was created.</span></span>

<span data-ttu-id="1b8ca-109">L'applicazione avrebbe nel corpo le 2 funzioni per l'attivazione e la disattivazione, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-109">The application would have in its body the 2 functions for activation and deactivation, as shown in the following example.</span></span>

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

<span data-ttu-id="1b8ca-110">Non è consigliabile eseguire alcuna operazione all'interno di queste funzioni, ma per memorizzare l'istanza della classe e sincronizzarla con il resto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-110">It is not recommended to do anything within these functions but to memorize the instance of the class and synchronize with the rest of the application.</span></span>

## <a name="usb-device-storage-class"></a><span data-ttu-id="1b8ca-111">Classe di archiviazione dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="1b8ca-111">USB Device Storage Class</span></span>

<span data-ttu-id="1b8ca-112">La classe di archiviazione dispositivo USB consente a un dispositivo di archiviazione incorporato nel sistema di essere reso visibile a un host USB.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-112">The USB device storage class allows for a storage device embedded in the system to be made visible to a USB host.</span></span>

<span data-ttu-id="1b8ca-113">La classe di archiviazione del dispositivo USB non fornisce una soluzione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-113">The USB device storage class does not by itself provide a storage solution.</span></span> <span data-ttu-id="1b8ca-114">Accetta e interpreta semplicemente le richieste SCSI provenienti dall'host.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-114">It merely accepts and interprets SCSI requests coming from the host.</span></span> <span data-ttu-id="1b8ca-115">Quando una di queste richieste è un comando Read o Write, richiama una chiamata predefinita a un gestore di dispositivi di archiviazione reale, ad esempio un driver di dispositivo ATA o un driver di dispositivo flash.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-115">When one of these requests is a read or a write command, it will invoke a pre-defined call back to a real storage device handler, such as an ATA device driver or a Flash device driver.</span></span>

<span data-ttu-id="1b8ca-116">Quando si inizializza la classe di archiviazione del dispositivo, viene assegnata una struttura del puntatore alla classe che contiene tutte le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-116">When initializing the device storage class, a pointer structure is given to the class that contains all the information necessary.</span></span> <span data-ttu-id="1b8ca-117">Di seguito è illustrato un esempio.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-117">An example is given below.</span></span>

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

<span data-ttu-id="1b8ca-118">In questo esempio, le stringhe di archiviazione del driver vengono personalizzate assegnando puntatori di stringa al parametro corrispondente.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-118">In this example, the driver storage strings are customized by assigning string pointers to corresponding parameter.</span></span> <span data-ttu-id="1b8ca-119">Se uno dei puntatore di stringa viene lasciato UX_NULL, viene utilizzata la stringa di Azure RTO predefinita.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-119">If any one of the string pointer is left to UX_NULL, the default Azure RTOS string is used.</span></span>

<span data-ttu-id="1b8ca-120">In questo esempio viene fornito l'ultimo indirizzo del blocco o l'LBA dell'unità, nonché le dimensioni del settore logico.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-120">In this example, the drive's last block address or LBA is given as well as the logical sector size.</span></span> <span data-ttu-id="1b8ca-121">LBA è il numero di settori disponibili nel supporto – 1.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-121">The LBA is the number of sectors available in the media –1.</span></span> <span data-ttu-id="1b8ca-122">La lunghezza del blocco è impostata su 512 nei supporti di archiviazione normali.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-122">The block length is set to 512 in regular storage media.</span></span> <span data-ttu-id="1b8ca-123">Può essere impostato su 2048 per le unità ottiche.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-123">It can be set to 2048 for optical drives.</span></span>

<span data-ttu-id="1b8ca-124">L'applicazione deve passare tre puntatori a funzione di callback per consentire alla classe di archiviazione di leggere, scrivere e ottenere lo stato del supporto.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-124">The application needs to pass three callback function pointers to allow the storage class to read, write and obtain status for the media.</span></span>

<span data-ttu-id="1b8ca-125">Nell'esempio riportato di seguito vengono illustrati i prototipi per le funzioni di lettura e scrittura.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-125">The prototypes for the read and write functions are shown in the example below.</span></span>

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

<span data-ttu-id="1b8ca-126">Dove:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-126">Where:</span></span>

- <span data-ttu-id="1b8ca-127">l' *archiviazione* è l'istanza della classe di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-127">*storage* is the instance of the storage class.</span></span>
- <span data-ttu-id="1b8ca-128">*lun* è il lun a cui viene indirizzato il comando.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-128">*lun* is the LUN the command is directed to.</span></span>
- <span data-ttu-id="1b8ca-129">*data_pointer* è l'indirizzo del buffer da utilizzare per la lettura o la scrittura.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-129">*data_pointer* is the address of the buffer to be used for reading or writing.</span></span>
- <span data-ttu-id="1b8ca-130">*number_blocks* è il numero di settori di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-130">*number_blocks* is the number of sectors to read/write.</span></span>
- <span data-ttu-id="1b8ca-131">*LBA* è l'indirizzo di settore da leggere.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-131">*lba* is the sector address to read.</span></span>
- <span data-ttu-id="1b8ca-132">*media_status* deve essere compilato esattamente come il valore restituito del callback dello stato dei supporti.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-132">*media_status* should be filled out exactly like the media status callback return value.</span></span>

<span data-ttu-id="1b8ca-133">Il valore restituito può contenere il valore UX_SUCCESS o UX_ERROR che indica un'operazione riuscita o non riuscita.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-133">The return value can have either the value UX_SUCCESS or UX_ERROR indicating a successful or unsuccessful operation.</span></span> <span data-ttu-id="1b8ca-134">Queste operazioni non devono restituire altri codici di errore.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-134">These operations do not need to return any other error codes.</span></span> <span data-ttu-id="1b8ca-135">Se si verifica un errore in qualsiasi operazione, la classe di archiviazione richiama la funzione di richiamata dello stato.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-135">If there is an error in any operation, the storage class will invoke the status call back function.</span></span>

<span data-ttu-id="1b8ca-136">Questa funzione presenta il seguente prototipo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-136">This function has the following prototype.</span></span>

```c
ULONG media_status( 
    VOID *storage,  
    ULONG lun,  
    ULONG media_id,  
    ULONG *media_status);
```

<span data-ttu-id="1b8ca-137">Il parametro chiamante media_id non è attualmente in uso e deve essere sempre 0.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-137">The calling parameter media_id is not currently used and should always be 0.</span></span> <span data-ttu-id="1b8ca-138">In futuro può essere usato per distinguere più dispositivi di archiviazione o dispositivi di archiviazione con più LUN SCSI.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-138">In the future it may be used to distinguish multiple storage devices or storage devices with multiple SCSI LUNs.</span></span> <span data-ttu-id="1b8ca-139">Questa versione della classe di archiviazione non supporta più istanze della classe di archiviazione o dei dispositivi di archiviazione con più LUN SCSI.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-139">This version of the storage class does not support multiple instances of the storage class or storage devices with multiple SCSI LUNs.</span></span>

<span data-ttu-id="1b8ca-140">Il valore restituito è un codice di errore SCSI che può avere il formato seguente.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-140">The return value is a SCSI error code that can have the following format.</span></span>

- <span data-ttu-id="1b8ca-141">**Bits 0-7** Sense_key</span><span class="sxs-lookup"><span data-stu-id="1b8ca-141">**Bits 0-7** Sense_key</span></span>
- <span data-ttu-id="1b8ca-142">**Bits 8-15** Codice di rilevamento aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-142">**Bits 8-15** Additional Sense Code</span></span>
- <span data-ttu-id="1b8ca-143">**Bits 16-23** Qualificatore del codice di rilevamento aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-143">**Bits 16-23** Additional Sense Code Qualifier</span></span>

<span data-ttu-id="1b8ca-144">La tabella seguente fornisce le combinazioni possibili/ASC/ASCQ.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-144">The following table provides the possible Sense/ASC/ASCQ combinations.</span></span>

| <span data-ttu-id="1b8ca-145">Chiave Sense</span><span class="sxs-lookup"><span data-stu-id="1b8ca-145">Sense Key</span></span> | <span data-ttu-id="1b8ca-146">ASC</span><span class="sxs-lookup"><span data-stu-id="1b8ca-146">ASC</span></span> | <span data-ttu-id="1b8ca-147">ASCQ</span><span class="sxs-lookup"><span data-stu-id="1b8ca-147">ASCQ</span></span> | <span data-ttu-id="1b8ca-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-148">Description</span></span>                                       |
| --------- | --- | ---- | ------------------------------------------------- |
| <span data-ttu-id="1b8ca-149">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-149">00</span></span>        | <span data-ttu-id="1b8ca-150">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-150">00</span></span>  | <span data-ttu-id="1b8ca-151">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-151">00</span></span>   | <span data-ttu-id="1b8ca-152">NESSUN SIGNIFICATO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-152">NO SENSE</span></span>                                          |
| <span data-ttu-id="1b8ca-153">01</span><span class="sxs-lookup"><span data-stu-id="1b8ca-153">01</span></span>        | <span data-ttu-id="1b8ca-154">17</span><span class="sxs-lookup"><span data-stu-id="1b8ca-154">17</span></span>  | <span data-ttu-id="1b8ca-155">01</span><span class="sxs-lookup"><span data-stu-id="1b8ca-155">01</span></span>   | <span data-ttu-id="1b8ca-156">DATI RIPRISTINATI CON TENTATIVI</span><span class="sxs-lookup"><span data-stu-id="1b8ca-156">RECOVERED DATA WITH RETRIES</span></span>                       |
| <span data-ttu-id="1b8ca-157">01</span><span class="sxs-lookup"><span data-stu-id="1b8ca-157">01</span></span>        | <span data-ttu-id="1b8ca-158">18</span><span class="sxs-lookup"><span data-stu-id="1b8ca-158">18</span></span>  | <span data-ttu-id="1b8ca-159">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-159">00</span></span>   | <span data-ttu-id="1b8ca-160">DATI RIPRISTINATI CON ECC</span><span class="sxs-lookup"><span data-stu-id="1b8ca-160">RECOVERED DATA WITH ECC</span></span>                           |
| <span data-ttu-id="1b8ca-161">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-161">02</span></span>        | <span data-ttu-id="1b8ca-162">04</span><span class="sxs-lookup"><span data-stu-id="1b8ca-162">04</span></span>  | <span data-ttu-id="1b8ca-163">01</span><span class="sxs-lookup"><span data-stu-id="1b8ca-163">01</span></span>   | <span data-ttu-id="1b8ca-164">L'UNITÀ LOGICA NON È PRONTA PER ESSERE PRONTA</span><span class="sxs-lookup"><span data-stu-id="1b8ca-164">LOGICAL DRIVE NOT READY - BECOMING READY</span></span>          |
| <span data-ttu-id="1b8ca-165">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-165">02</span></span>        | <span data-ttu-id="1b8ca-166">04</span><span class="sxs-lookup"><span data-stu-id="1b8ca-166">04</span></span>  | <span data-ttu-id="1b8ca-167">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-167">02</span></span>   | <span data-ttu-id="1b8ca-168">UNITÀ LOGICA NON PRONTA-INIZIALIZZAZIONE RICHIESTA</span><span class="sxs-lookup"><span data-stu-id="1b8ca-168">LOGICAL DRIVE NOT READY - INITIALIZATION REQUIRED</span></span> |
| <span data-ttu-id="1b8ca-169">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-169">02</span></span>        | <span data-ttu-id="1b8ca-170">04</span><span class="sxs-lookup"><span data-stu-id="1b8ca-170">04</span></span>  | <span data-ttu-id="1b8ca-171">04</span><span class="sxs-lookup"><span data-stu-id="1b8ca-171">04</span></span>   | <span data-ttu-id="1b8ca-172">UNITÀ LOGICA NON PRONTA-FORMATO IN CORSO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-172">LOGICAL UNIT NOT READY - FORMAT IN PROGRESS</span></span>       |
| <span data-ttu-id="1b8ca-173">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-173">02</span></span>        | <span data-ttu-id="1b8ca-174">04</span><span class="sxs-lookup"><span data-stu-id="1b8ca-174">04</span></span>  | <span data-ttu-id="1b8ca-175">FF</span><span class="sxs-lookup"><span data-stu-id="1b8ca-175">FF</span></span>   | <span data-ttu-id="1b8ca-176">UNITÀ LOGICA NON PRONTA-IL DISPOSITIVO È OCCUPATO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-176">LOGICAL DRIVE NOT READY - DEVICE IS BUSY</span></span>          |
| <span data-ttu-id="1b8ca-177">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-177">02</span></span>        | <span data-ttu-id="1b8ca-178">06</span><span class="sxs-lookup"><span data-stu-id="1b8ca-178">06</span></span>  | <span data-ttu-id="1b8ca-179">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-179">00</span></span>   | <span data-ttu-id="1b8ca-180">NON SONO STATE TROVATE POSIZIONI DI RIFERIMENTO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-180">NO REFERENCE POSITION FOUND</span></span>                       |
| <span data-ttu-id="1b8ca-181">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-181">02</span></span>        | <span data-ttu-id="1b8ca-182">08</span><span class="sxs-lookup"><span data-stu-id="1b8ca-182">08</span></span>  | <span data-ttu-id="1b8ca-183">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-183">00</span></span>   | <span data-ttu-id="1b8ca-184">ERRORE DI COMUNICAZIONE UNITÀ LOGICA</span><span class="sxs-lookup"><span data-stu-id="1b8ca-184">LOGICAL UNIT COMMUNICATION FAILURE</span></span>                |
| <span data-ttu-id="1b8ca-185">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-185">02</span></span>        | <span data-ttu-id="1b8ca-186">08</span><span class="sxs-lookup"><span data-stu-id="1b8ca-186">08</span></span>  | <span data-ttu-id="1b8ca-187">01</span><span class="sxs-lookup"><span data-stu-id="1b8ca-187">01</span></span>   | <span data-ttu-id="1b8ca-188">TIMEOUT COMUNICAZIONE UNITÀ LOGICA</span><span class="sxs-lookup"><span data-stu-id="1b8ca-188">LOGICAL UNIT COMMUNICATION TIME-OUT</span></span>               |
| <span data-ttu-id="1b8ca-189">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-189">02</span></span>        | <span data-ttu-id="1b8ca-190">08</span><span class="sxs-lookup"><span data-stu-id="1b8ca-190">08</span></span>  | <span data-ttu-id="1b8ca-191">80</span><span class="sxs-lookup"><span data-stu-id="1b8ca-191">80</span></span>   | <span data-ttu-id="1b8ca-192">SOVRACCARICO DELLE COMUNICAZIONI TRA UNITÀ LOGICHE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-192">LOGICAL UNIT COMMUNICATION OVERRUN</span></span>                |
| <span data-ttu-id="1b8ca-193">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-193">02</span></span>        | <span data-ttu-id="1b8ca-194">3A</span><span class="sxs-lookup"><span data-stu-id="1b8ca-194">3A</span></span>  | <span data-ttu-id="1b8ca-195">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-195">00</span></span>   | <span data-ttu-id="1b8ca-196">MEDIA NON PRESENTE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-196">MEDIUM NOT PRESENT</span></span>                                |
| <span data-ttu-id="1b8ca-197">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-197">02</span></span>        | <span data-ttu-id="1b8ca-198">54</span><span class="sxs-lookup"><span data-stu-id="1b8ca-198">54</span></span>  | <span data-ttu-id="1b8ca-199">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-199">00</span></span>   | <span data-ttu-id="1b8ca-200">ERRORE DELL'INTERFACCIA DI SISTEMA DA USB A HOST</span><span class="sxs-lookup"><span data-stu-id="1b8ca-200">USB TO HOST SYSTEM INTERFACE FAILURE</span></span>              |
| <span data-ttu-id="1b8ca-201">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-201">02</span></span>        | <span data-ttu-id="1b8ca-202">80</span><span class="sxs-lookup"><span data-stu-id="1b8ca-202">80</span></span>  | <span data-ttu-id="1b8ca-203">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-203">00</span></span>   | <span data-ttu-id="1b8ca-204">RISORSE INSUFFICIENTI</span><span class="sxs-lookup"><span data-stu-id="1b8ca-204">INSUFFICIENT RESOURCES</span></span>                            |
| <span data-ttu-id="1b8ca-205">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-205">02</span></span>        | <span data-ttu-id="1b8ca-206">FF</span><span class="sxs-lookup"><span data-stu-id="1b8ca-206">FF</span></span>  | <span data-ttu-id="1b8ca-207">FF</span><span class="sxs-lookup"><span data-stu-id="1b8ca-207">FF</span></span>   | <span data-ttu-id="1b8ca-208">ERRORE SCONOSCIUTO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-208">UNKNOWN ERROR</span></span>                                     |
| <span data-ttu-id="1b8ca-209">03</span><span class="sxs-lookup"><span data-stu-id="1b8ca-209">03</span></span>        | <span data-ttu-id="1b8ca-210">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-210">02</span></span>  | <span data-ttu-id="1b8ca-211">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-211">00</span></span>   | <span data-ttu-id="1b8ca-212">NESSUNA RICERCA COMPLETATA</span><span class="sxs-lookup"><span data-stu-id="1b8ca-212">NO SEEK COMPLETE</span></span>                                  |
| <span data-ttu-id="1b8ca-213">03</span><span class="sxs-lookup"><span data-stu-id="1b8ca-213">03</span></span>        | <span data-ttu-id="1b8ca-214">03</span><span class="sxs-lookup"><span data-stu-id="1b8ca-214">03</span></span>  | <span data-ttu-id="1b8ca-215">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-215">00</span></span>   | <span data-ttu-id="1b8ca-216">ERRORE DI SCRITTURA</span><span class="sxs-lookup"><span data-stu-id="1b8ca-216">WRITE FAULT</span></span>                                       |
| <span data-ttu-id="1b8ca-217">03</span><span class="sxs-lookup"><span data-stu-id="1b8ca-217">03</span></span>        | <span data-ttu-id="1b8ca-218">10</span><span class="sxs-lookup"><span data-stu-id="1b8ca-218">10</span></span>  | <span data-ttu-id="1b8ca-219">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-219">00</span></span>   | <span data-ttu-id="1b8ca-220">ERRORE CRC ID</span><span class="sxs-lookup"><span data-stu-id="1b8ca-220">ID CRC ERROR</span></span>                                      |
| <span data-ttu-id="1b8ca-221">03</span><span class="sxs-lookup"><span data-stu-id="1b8ca-221">03</span></span>        | <span data-ttu-id="1b8ca-222">11</span><span class="sxs-lookup"><span data-stu-id="1b8ca-222">11</span></span>  | <span data-ttu-id="1b8ca-223">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-223">00</span></span>   | <span data-ttu-id="1b8ca-224">ERRORE DI LETTURA NON RECUPERATO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-224">UNRECOVERED READ ERROR</span></span>                            |
| <span data-ttu-id="1b8ca-225">03</span><span class="sxs-lookup"><span data-stu-id="1b8ca-225">03</span></span>        | <span data-ttu-id="1b8ca-226">12</span><span class="sxs-lookup"><span data-stu-id="1b8ca-226">12</span></span>  | <span data-ttu-id="1b8ca-227">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-227">00</span></span>   | <span data-ttu-id="1b8ca-228">CONTRASSEGNO INDIRIZZO NON TROVATO PER IL CAMPO ID</span><span class="sxs-lookup"><span data-stu-id="1b8ca-228">ADDRESS MARK NOT FOUND FOR ID FIELD</span></span>               |
| <span data-ttu-id="1b8ca-229">03</span><span class="sxs-lookup"><span data-stu-id="1b8ca-229">03</span></span>        | <span data-ttu-id="1b8ca-230">13</span><span class="sxs-lookup"><span data-stu-id="1b8ca-230">13</span></span>  | <span data-ttu-id="1b8ca-231">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-231">00</span></span>   | <span data-ttu-id="1b8ca-232">CONTRASSEGNO INDIRIZZO NON TROVATO PER IL CAMPO DATI</span><span class="sxs-lookup"><span data-stu-id="1b8ca-232">ADDRESS MARK NOT FOUND FOR DATA FIELD</span></span>             |
| <span data-ttu-id="1b8ca-233">03</span><span class="sxs-lookup"><span data-stu-id="1b8ca-233">03</span></span>        | <span data-ttu-id="1b8ca-234">14</span><span class="sxs-lookup"><span data-stu-id="1b8ca-234">14</span></span>  | <span data-ttu-id="1b8ca-235">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-235">00</span></span>   | <span data-ttu-id="1b8ca-236">ENTITÀ REGISTRATA NON TROVATA</span><span class="sxs-lookup"><span data-stu-id="1b8ca-236">RECORDED ENTITY NOT FOUND</span></span>                         |
| <span data-ttu-id="1b8ca-237">03</span><span class="sxs-lookup"><span data-stu-id="1b8ca-237">03</span></span>        | <span data-ttu-id="1b8ca-238">30</span><span class="sxs-lookup"><span data-stu-id="1b8ca-238">30</span></span>  | <span data-ttu-id="1b8ca-239">01</span><span class="sxs-lookup"><span data-stu-id="1b8ca-239">01</span></span>   | <span data-ttu-id="1b8ca-240">NON È POSSIBILE LEGGERE IL FORMATO MEDIO-SCONOSCIUTO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-240">CANNOT READ MEDIUM - UNKNOWN FORMAT</span></span>               |
| <span data-ttu-id="1b8ca-241">03</span><span class="sxs-lookup"><span data-stu-id="1b8ca-241">03</span></span>        | <span data-ttu-id="1b8ca-242">31</span><span class="sxs-lookup"><span data-stu-id="1b8ca-242">31</span></span>  | <span data-ttu-id="1b8ca-243">01</span><span class="sxs-lookup"><span data-stu-id="1b8ca-243">01</span></span>   | <span data-ttu-id="1b8ca-244">COMANDO FORMAT NON RIUSCITO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-244">FORMAT COMMAND FAILED</span></span>                             |
| <span data-ttu-id="1b8ca-245">04</span><span class="sxs-lookup"><span data-stu-id="1b8ca-245">04</span></span>        | <span data-ttu-id="1b8ca-246">40</span><span class="sxs-lookup"><span data-stu-id="1b8ca-246">40</span></span>  | <span data-ttu-id="1b8ca-247">NN</span><span class="sxs-lookup"><span data-stu-id="1b8ca-247">NN</span></span>   | <span data-ttu-id="1b8ca-248">ERRORE DI DIAGNOSTICA SUL COMPONENTE NN (80H-FFH)</span><span class="sxs-lookup"><span data-stu-id="1b8ca-248">DIAGNOSTIC FAILURE ON COMPONENT NN (80H-FFH)</span></span>      |
| <span data-ttu-id="1b8ca-249">05</span><span class="sxs-lookup"><span data-stu-id="1b8ca-249">05</span></span>        | <span data-ttu-id="1b8ca-250">1A</span><span class="sxs-lookup"><span data-stu-id="1b8ca-250">1A</span></span>  | <span data-ttu-id="1b8ca-251">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-251">00</span></span>   | <span data-ttu-id="1b8ca-252">ERRORE DI LUNGHEZZA DELL'ELENCO DI PARAMETRI</span><span class="sxs-lookup"><span data-stu-id="1b8ca-252">PARAMETER LIST LENGTH ERROR</span></span>                       |
| <span data-ttu-id="1b8ca-253">05</span><span class="sxs-lookup"><span data-stu-id="1b8ca-253">05</span></span>        | <span data-ttu-id="1b8ca-254">20</span><span class="sxs-lookup"><span data-stu-id="1b8ca-254">20</span></span>  | <span data-ttu-id="1b8ca-255">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-255">00</span></span>   | <span data-ttu-id="1b8ca-256">CODICE OPERAZIONE COMANDO NON VALIDO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-256">INVALID COMMAND OPERATION CODE</span></span>                    |
| <span data-ttu-id="1b8ca-257">05</span><span class="sxs-lookup"><span data-stu-id="1b8ca-257">05</span></span>        | <span data-ttu-id="1b8ca-258">21</span><span class="sxs-lookup"><span data-stu-id="1b8ca-258">21</span></span>  | <span data-ttu-id="1b8ca-259">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-259">00</span></span>   | <span data-ttu-id="1b8ca-260">INDIRIZZO BLOCCO LOGICO NON COMPRESO NELL'INTERVALLO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-260">LOGICAL BLOCK ADDRESS OUT OF RANGE</span></span>                |
| <span data-ttu-id="1b8ca-261">05</span><span class="sxs-lookup"><span data-stu-id="1b8ca-261">05</span></span>        | <span data-ttu-id="1b8ca-262">24</span><span class="sxs-lookup"><span data-stu-id="1b8ca-262">24</span></span>  | <span data-ttu-id="1b8ca-263">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-263">00</span></span>   | <span data-ttu-id="1b8ca-264">CAMPO NON VALIDO NEL PACCHETTO DI COMANDI</span><span class="sxs-lookup"><span data-stu-id="1b8ca-264">INVALID FIELD IN COMMAND PACKET</span></span>                   |
| <span data-ttu-id="1b8ca-265">05</span><span class="sxs-lookup"><span data-stu-id="1b8ca-265">05</span></span>        | <span data-ttu-id="1b8ca-266">25</span><span class="sxs-lookup"><span data-stu-id="1b8ca-266">25</span></span>  | <span data-ttu-id="1b8ca-267">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-267">00</span></span>   | <span data-ttu-id="1b8ca-268">UNITÀ LOGICA NON SUPPORTATA</span><span class="sxs-lookup"><span data-stu-id="1b8ca-268">LOGICAL UNIT NOT SUPPORTED</span></span>                        |
| <span data-ttu-id="1b8ca-269">05</span><span class="sxs-lookup"><span data-stu-id="1b8ca-269">05</span></span>        | <span data-ttu-id="1b8ca-270">26</span><span class="sxs-lookup"><span data-stu-id="1b8ca-270">26</span></span>  | <span data-ttu-id="1b8ca-271">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-271">00</span></span>   | <span data-ttu-id="1b8ca-272">CAMPO NON VALIDO NELL'ELENCO DI PARAMETRI</span><span class="sxs-lookup"><span data-stu-id="1b8ca-272">INVALID FIELD IN PARAMETER LIST</span></span>                   |
| <span data-ttu-id="1b8ca-273">05</span><span class="sxs-lookup"><span data-stu-id="1b8ca-273">05</span></span>        | <span data-ttu-id="1b8ca-274">26</span><span class="sxs-lookup"><span data-stu-id="1b8ca-274">26</span></span>  | <span data-ttu-id="1b8ca-275">01</span><span class="sxs-lookup"><span data-stu-id="1b8ca-275">01</span></span>   | <span data-ttu-id="1b8ca-276">PARAMETRO NON SUPPORTATO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-276">PARAMETER NOT SUPPORTED</span></span>                           |
| <span data-ttu-id="1b8ca-277">05</span><span class="sxs-lookup"><span data-stu-id="1b8ca-277">05</span></span>        | <span data-ttu-id="1b8ca-278">26</span><span class="sxs-lookup"><span data-stu-id="1b8ca-278">26</span></span>  | <span data-ttu-id="1b8ca-279">02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-279">02</span></span>   | <span data-ttu-id="1b8ca-280">VALORE PARAMETRO NON VALIDO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-280">PARAMETER VALUE INVALID</span></span>                           |
| <span data-ttu-id="1b8ca-281">05</span><span class="sxs-lookup"><span data-stu-id="1b8ca-281">05</span></span>        | <span data-ttu-id="1b8ca-282">39</span><span class="sxs-lookup"><span data-stu-id="1b8ca-282">39</span></span>  | <span data-ttu-id="1b8ca-283">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-283">00</span></span>   | <span data-ttu-id="1b8ca-284">SALVATAGGIO DEI PARAMETRI NON SUPPORTATO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-284">SAVING PARAMETERS NOT SUPPORT</span></span>                     |
| <span data-ttu-id="1b8ca-285">06</span><span class="sxs-lookup"><span data-stu-id="1b8ca-285">06</span></span>        | <span data-ttu-id="1b8ca-286">28</span><span class="sxs-lookup"><span data-stu-id="1b8ca-286">28</span></span>  | <span data-ttu-id="1b8ca-287">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-287">00</span></span>   | <span data-ttu-id="1b8ca-288">TRANSIZIONE NON PRONTA PER LA PREPARAZIONE: I SUPPORTI SONO STATI MODIFICATI</span><span class="sxs-lookup"><span data-stu-id="1b8ca-288">NOT READY TO READY TRANSITION – MEDIA CHANGED</span></span>     |
| <span data-ttu-id="1b8ca-289">06</span><span class="sxs-lookup"><span data-stu-id="1b8ca-289">06</span></span>        | <span data-ttu-id="1b8ca-290">29</span><span class="sxs-lookup"><span data-stu-id="1b8ca-290">29</span></span>  | <span data-ttu-id="1b8ca-291">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-291">00</span></span>   | <span data-ttu-id="1b8ca-292">RIPRISTINO DELL'ACCENSIONE O DELLA REIMPOSTAZIONE DEL DISPOSITIVO BUS</span><span class="sxs-lookup"><span data-stu-id="1b8ca-292">POWER ON RESET OR BUS DEVICE RESET OCCURRED</span></span>       |
| <span data-ttu-id="1b8ca-293">06</span><span class="sxs-lookup"><span data-stu-id="1b8ca-293">06</span></span>        | <span data-ttu-id="1b8ca-294">2F</span><span class="sxs-lookup"><span data-stu-id="1b8ca-294">2F</span></span>  | <span data-ttu-id="1b8ca-295">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-295">00</span></span>   | <span data-ttu-id="1b8ca-296">COMANDI CANCELLATI DA UN ALTRO INIZIATORE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-296">COMMANDS CLEARED BY ANOTHER INITIATOR</span></span>             |
| <span data-ttu-id="1b8ca-297">07</span><span class="sxs-lookup"><span data-stu-id="1b8ca-297">07</span></span>        | <span data-ttu-id="1b8ca-298">27</span><span class="sxs-lookup"><span data-stu-id="1b8ca-298">27</span></span>  | <span data-ttu-id="1b8ca-299">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-299">00</span></span>   | <span data-ttu-id="1b8ca-300">SCRIVI SUPPORTO PROTETTO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-300">WRITE PROTECTED MEDIA</span></span>                             |
| <span data-ttu-id="1b8ca-301">0B</span><span class="sxs-lookup"><span data-stu-id="1b8ca-301">0B</span></span>        | <span data-ttu-id="1b8ca-302">4E</span><span class="sxs-lookup"><span data-stu-id="1b8ca-302">4E</span></span>  | <span data-ttu-id="1b8ca-303">00</span><span class="sxs-lookup"><span data-stu-id="1b8ca-303">00</span></span>   | <span data-ttu-id="1b8ca-304">TENTATIVO DI COMANDO SOVRAPPOSTO</span><span class="sxs-lookup"><span data-stu-id="1b8ca-304">OVERLAPPED COMMAND ATTEMPTED</span></span>                      |

<span data-ttu-id="1b8ca-305">Sono disponibili altri due callback facoltativi che l'applicazione può implementare; uno è per rispondere a un comando **GET_STATUS_NOTIFICATION** e l'altro per rispondere al comando **SYNCHRONIZE_CACHE** .</span><span class="sxs-lookup"><span data-stu-id="1b8ca-305">There are two additional, optional callbacks the application may implement; one is for responding to a **GET_STATUS_NOTIFICATION** command and the other is for responding to the **SYNCHRONIZE_CACHE** command.</span></span>

<span data-ttu-id="1b8ca-306">Se l'applicazione desidera gestire il comando GET_STATUS_NOTIFICATION dall'host, deve implementare un callback con il prototipo seguente.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-306">If the application would like to handle the GET_STATUS_NOTIFICATION command from the host, it should implement a callback with the following prototype.</span></span>

```c
UINT ux_slave_class_storage_media_notification( 
    VOID *storage,  
    ULONG lun,
    ULONG media_id,  
    ULONG notification_class,
    UCHAR **media_notification,  
    ULONG *media_notification_length);
```

<span data-ttu-id="1b8ca-307">Dove:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-307">Where:</span></span>

- <span data-ttu-id="1b8ca-308">l' *archiviazione* è l'istanza della classe di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-308">*storage* is the instance of the storage class.</span></span>
- <span data-ttu-id="1b8ca-309">*media_id* non è attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-309">*media_id* is not currently used.</span></span> <span data-ttu-id="1b8ca-310">notification_class specifica la classe di notifica.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-310">notification_class specifies the class of notification.</span></span>
- <span data-ttu-id="1b8ca-311">*media_notification* deve essere impostato dall'applicazione sul buffer contenente la risposta per la notifica.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-311">*media_notification* should be set by the application to the buffer containing the response for the notification.</span></span>
- <span data-ttu-id="1b8ca-312">*media_notification_length* necessario impostare l'applicazione in modo che contenga la lunghezza del buffer di risposta.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-312">*media_notification_length* should be set by the application to contain the length of the response buffer.</span></span>

<span data-ttu-id="1b8ca-313">Il valore restituito indica se il comando ha avuto esito positivo o meno, **UX_SUCCESS** o **UX_ERROR**.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-313">The return value indicates whether or not the command succeeded – should be either **UX_SUCCESS** or **UX_ERROR**.</span></span>

<span data-ttu-id="1b8ca-314">Se l'applicazione non implementa questo callback, al momento della ricezione del comando di **GET_STATUS_NOTIFICATION** , USBX informerà l'host che il comando non è implementato.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-314">If the application does not implement this callback, then upon receiving the **GET_STATUS_NOTIFICATION** command, USBX will notify the host that the command is not implemented.</span></span>

<span data-ttu-id="1b8ca-315">Il **SYNCHRONIZE_CACHE** comando deve essere gestito se l'applicazione utilizza una cache per le Scritture dall'host.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-315">The **SYNCHRONIZE_CACHE** command should be handled if the application is utilizing a cache for writes from the host.</span></span> <span data-ttu-id="1b8ca-316">Un host può inviare questo comando se sa che il dispositivo di archiviazione sta per essere disconnesso, ad esempio in Windows, se si fa clic con il pulsante destro del mouse sull'icona di un'unità flash sulla barra degli strumenti e si seleziona "Rimuovi \[ nome dispositivo \] di archiviazione", Windows emetterà il comando **SYNCHRONIZE_CACHE** al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-316">A host may send this command if it knows the storage device is about to be disconnected, for example, in Windows, if you right click a flash drive icon in the toolbar and select "Eject \[storage device name\]", Windows will issue the **SYNCHRONIZE_CACHE** command to that device.</span></span>

<span data-ttu-id="1b8ca-317">Se l'applicazione desidera gestire il comando **GET_STATUS_NOTIFICATION** dall'host, deve implementare un callback con il prototipo seguente.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-317">If the application would like to handle the **GET_STATUS_NOTIFICATION** command from the host, it should implement a callback with the following prototype.</span></span>

```c
UINT ux_slave_class_storage_media_flush(
    VOID *storage, 
    ULONG lun,
    ULONG number_blocks, 
    ULONG lba, 
    ULONG *media_status);
```

<span data-ttu-id="1b8ca-318">Dove:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-318">Where:</span></span>

- <span data-ttu-id="1b8ca-319">l' *archiviazione* è l'istanza della classe di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-319">*storage* is the instance of the storage class.</span></span>
- <span data-ttu-id="1b8ca-320">il parametro *lun* specifica il lun a cui viene indirizzato il comando.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-320">*lun* parameter specifies which LUN the command is directed to.</span></span>
- <span data-ttu-id="1b8ca-321">*number_blocks* specifica il numero di blocchi da sincronizzare.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-321">*number_blocks* specifies the number of blocks to synchronize.</span></span>
- <span data-ttu-id="1b8ca-322">*LBA* è l'indirizzo di settore del primo blocco da sincronizzare.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-322">*lba* is the sector address of the first block to synchronize.</span></span>
- <span data-ttu-id="1b8ca-323">*media_status* deve essere compilato esattamente come il valore restituito del callback dello stato dei supporti.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-323">*media_status* should be filled out exactly like the media status callback return value.</span></span>

<span data-ttu-id="1b8ca-324">Il valore restituito indica se il comando ha avuto esito positivo o meno, **UX_SUCCESS** o **UX_ERROR**.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-324">The return value indicates whether or not the command succeeded – should be either **UX_SUCCESS** or **UX_ERROR**.</span></span>

### <a name="multiple-scsi-lun"></a><span data-ttu-id="1b8ca-325">LUN multiplo SCSI</span><span class="sxs-lookup"><span data-stu-id="1b8ca-325">Multiple SCSI LUN</span></span>

<span data-ttu-id="1b8ca-326">La classe di archiviazione del dispositivo USBX supporta più lun.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-326">The USBX device storage class supports multiple LUNs.</span></span> <span data-ttu-id="1b8ca-327">È pertanto possibile creare un dispositivo di archiviazione che funga da CD-ROM e da un disco flash nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-327">It is therefore possible to create a storage device that acts as a CD-ROM and a Flash disk at the same time.</span></span> <span data-ttu-id="1b8ca-328">In tal caso, l'inizializzazione è leggermente diversa.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-328">In such a case, the initialization would be slightly different.</span></span> <span data-ttu-id="1b8ca-329">Di seguito è riportato un esempio per un disco flash e un CD-ROM:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-329">Here is an example for a Flash Disk and CD-ROM:</span></span>

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

## <a name="usb-device-cdc-acm-class"></a><span data-ttu-id="1b8ca-330">Classe dispositivo USB CDC-ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-330">USB Device CDC-ACM Class</span></span>

<span data-ttu-id="1b8ca-331">La classe CDC-ACM del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come un dispositivo seriale.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-331">The USB device CDC-ACM class allows for a USB host system to communicate with the device as a serial device.</span></span> <span data-ttu-id="1b8ca-332">Questa classe è basata sullo standard USB ed è un subset dello standard CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-332">This class is based on the USB standard and is a subset of the CDC standard.</span></span>

<span data-ttu-id="1b8ca-333">Un Framework di dispositivi conformi a CDC-ACM deve essere dichiarato dallo stack del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-333">A CDC-ACM compliant device framework needs to be declared by the device stack.</span></span> <span data-ttu-id="1b8ca-334">Un esempio è disponibile qui di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-334">An example is found here below.</span></span>

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

<span data-ttu-id="1b8ca-335">La classe CDC-ACM usa un Framework per dispositivi composito per raggruppare le interfacce (controllo e dati).</span><span class="sxs-lookup"><span data-stu-id="1b8ca-335">The CDC-ACM class uses a composite device framework to group interfaces (control and data).</span></span> <span data-ttu-id="1b8ca-336">È necessario prestare attenzione quando si definisce il descrittore del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-336">As a result care should be taken when defining the device descriptor.</span></span> <span data-ttu-id="1b8ca-337">USBX si basa sul descrittore IAD per comprendere internamente come associare le interfacce.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-337">USBX relies on the IAD descriptor to know internally how to bind interfaces.</span></span> <span data-ttu-id="1b8ca-338">Il descrittore IAD deve essere dichiarato prima delle interfacce e contenere la prima interfaccia della classe CDC-ACM e il numero di interfacce associate.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-338">The IAD descriptor should be declared before the interfaces and contain the first interface of the CDC-ACM class and how many interfaces are attached.</span></span>

<span data-ttu-id="1b8ca-339">La classe CDC-ACM usa anche un descrittore di funzionalità di Unione che esegue la stessa funzione del descrittore IAD più recente.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-339">The CDC-ACM class also uses a union functional descriptor which performs the same function as the newer IAD descriptor.</span></span> <span data-ttu-id="1b8ca-340">Sebbene sia necessario dichiarare un descrittore funzionale Unione per motivi cronologici e la compatibilità con il lato host, questo non viene usato da USBX.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-340">Although a Union Functional descriptor must be declared for historical reasons and compatibility with the host side, it is not used by USBX.</span></span>

<span data-ttu-id="1b8ca-341">L'inizializzazione della classe CDC-ACM prevede i parametri seguenti.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-341">The initialization of the CDC-ACM class expects the following parameters.</span></span>

```c
/* Set the parameters for callback when insertion/extraction of a CDC device. */

parameter.ux_slave_class_cdc_acm_instance_activate = tx_demo_cdc_instance_activate;

parameter.ux_slave_class_cdc_acm_instance_deactivate = tx_demo_cdc_instance_deactivate;

parameter.ux_slave_class_cdc_acm_parameter_change = tx_demo_cdc_instance_parameter_change;

/* Initialize the device cdc class. This class owns both interfaces starting with 0. */
status = ux_device_stack_class_register(_ux_system_slave_class_cdc_acm_name,ux_device_class_cdc_acm_entry,
    1,0, &parameter);
```

<span data-ttu-id="1b8ca-342">I 2 parametri definiti sono puntatori di callback nelle applicazioni utente che verranno chiamate quando lo stack attiva o disattiva questa classe.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-342">The 2 parameters defined are callback pointers into the user applications that will be called when the stack activates or deactivate this class.</span></span>

<span data-ttu-id="1b8ca-343">Il terzo parametro definito è un puntatore di callback all'applicazione utente che verrà chiamato in caso di modifica del parametro della riga o del codice di riga.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-343">The third parameter defined is a callback pointer to the user application that will be called when there is line coding or line states parameter change.</span></span> <span data-ttu-id="1b8ca-344">Ad esempio, quando è presente una richiesta da host per modificare lo stato di DTR su **true**, viene richiamato il callback, nell'applicazione utente it è possibile controllare gli Stati della riga tramite la funzione IOCTL per l'host Kow è pronto per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-344">E.g., when there is request from host to change DTR state to **TRUE**, the callback is invoked, in it user application can check line states through IOCTL function to kow host is ready for communication.</span></span>

<span data-ttu-id="1b8ca-345">CDC-ACM si basa su uno standard USB-IF e viene riconosciuto automaticamente dai sistemi operativi MACOs e Linux.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-345">The CDC-ACM is based on a USB-IF standard and is automatically recognized by MACOs and Linux operating systems.</span></span> <span data-ttu-id="1b8ca-346">Nelle piattaforme Windows questa classe richiede un file inf per la versione di Windows precedente alla 10.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-346">On Windows platforms, this class requires a .inf file for Windows version prior to 10.</span></span> <span data-ttu-id="1b8ca-347">Windows 10 non richiede alcun file inf.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-347">Windows 10 does not require any .inf files.</span></span> <span data-ttu-id="1b8ca-348">Viene fornito un modello per la classe CDC-ACM, che è possibile trovare nella directory ***usbx_windows_host_files*** .</span><span class="sxs-lookup"><span data-stu-id="1b8ca-348">We supply a template for the CDC-ACM class and it can be found in the ***usbx_windows_host_files*** directory.</span></span> <span data-ttu-id="1b8ca-349">Per la versione più recente di Windows, è necessario utilizzare il file CDC_ACM_Template_Win7_64bit. inf (ad eccezione di Win10).</span><span class="sxs-lookup"><span data-stu-id="1b8ca-349">For more recent version of Windows the file CDC_ACM_Template_Win7_64bit.inf should be used (except Win10).</span></span> <span data-ttu-id="1b8ca-350">Questo file deve essere modificato in modo da riflettere il PID/VID usato dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-350">This file needs to be modified to reflect the PID/VID used by the device.</span></span> <span data-ttu-id="1b8ca-351">Il PID/VID sarà specifico per il cliente finale quando la società e il prodotto vengono registrati con il dispositivo USB-IF.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-351">The PID/VID will be specific to the final customer when the company and the product are registered with the USB-IF.</span></span> <span data-ttu-id="1b8ca-352">Nel file inf i campi da modificare si trovano qui.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-352">In the inf file, the fields to modify are located here.</span></span>

```INF
[DeviceList]
%DESCRIPTION%=DriverInstall, USB\VID_8484&PID_0000

[DeviceList.NTamd64]
%DESCRIPTION%=DriverInstall, USB\VID_8484&PID_0000
```

<span data-ttu-id="1b8ca-353">Nel Framework del dispositivo del dispositivo CDC-ACM, il PID/VID viene archiviato nel descrittore del dispositivo (vedere il descrittore del dispositivo dichiarato in precedenza).</span><span class="sxs-lookup"><span data-stu-id="1b8ca-353">In the device framework of the CDC-ACM device, the PID/VID are stored in the device descriptor (see the device descriptor declared above).</span></span>

<span data-ttu-id="1b8ca-354">Quando un sistema host USB individua il dispositivo USB CDC-ACM, viene montata una classe seriale e il dispositivo può essere usato con qualsiasi programma terminale seriale.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-354">When a USB host systems discovers the USB CDC-ACM device, it will mount a serial class and the device can be used with any serial terminal program.</span></span> <span data-ttu-id="1b8ca-355">Per informazioni di riferimento, vedere il sistema operativo host.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-355">See the host Operating System for reference.</span></span>

<span data-ttu-id="1b8ca-356">Le funzioni API della classe CDC-ACM sono definite di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-356">The CDC-ACM class API functions are defined below.</span></span>

### <a name="ux_device_class_cdc_acm_ioctl"></a><span data-ttu-id="1b8ca-357">ux_device_class_cdc_acm_ioctl</span><span class="sxs-lookup"><span data-stu-id="1b8ca-357">ux_device_class_cdc_acm_ioctl</span></span>

<span data-ttu-id="1b8ca-358">Eseguire IOCTL sull'interfaccia CDC-ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-358">Perform IOCTL on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-359">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-359">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm, 
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="1b8ca-360">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-360">Description</span></span>

<span data-ttu-id="1b8ca-361">Questa funzione viene chiamata quando un'applicazione deve eseguire varie chiamate ioctl all'interfaccia di CDC ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-361">This function is called when an application needs to perform various ioctl calls to the cdc acm interface</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-362">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-362">Parameters</span></span>

- <span data-ttu-id="1b8ca-363">**cdc_acm**: puntatore all'istanza della classe CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-363">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="1b8ca-364">**ioctl_function**: funzione IOCTL da eseguire.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-364">**ioctl_function**: Ioctl function to be performed.</span></span>
- <span data-ttu-id="1b8ca-365">**Parameter**: puntatore a un parametro specifico della chiamata IOCTL.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-365">**parameter**: Pointer to a parameter specific to the ioctl call.</span></span>

### <a name="return-value"></a><span data-ttu-id="1b8ca-366">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-366">Return Value</span></span>

- <span data-ttu-id="1b8ca-367">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-367">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="1b8ca-368">Errore di **UX_ERROR** (0xFF) dalla funzione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-368">**UX_ERROR** (0xFF) Error from function</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-369">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-369">Example</span></span>

```c
/* Start cdc acm callback transmission. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START, &callback);

if(status != UX_SUCCESS)
    return;
```

### <a name="ioctl-functions"></a><span data-ttu-id="1b8ca-370">Funzioni IOCTL:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-370">Ioctl functions:</span></span>

| <span data-ttu-id="1b8ca-371">Funzione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-371">Function</span></span>                                        | <span data-ttu-id="1b8ca-372">Valore</span><span class="sxs-lookup"><span data-stu-id="1b8ca-372">Value</span></span> |
| ----------------------------------------------- | - |
| <span data-ttu-id="1b8ca-373">UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="1b8ca-373">UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span></span>    | <span data-ttu-id="1b8ca-374">1</span><span class="sxs-lookup"><span data-stu-id="1b8ca-374">1</span></span> |
| <span data-ttu-id="1b8ca-375">UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="1b8ca-375">UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span></span>    | <span data-ttu-id="1b8ca-376">2</span><span class="sxs-lookup"><span data-stu-id="1b8ca-376">2</span></span> |
| <span data-ttu-id="1b8ca-377">UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-377">UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span></span>     | <span data-ttu-id="1b8ca-378">3</span><span class="sxs-lookup"><span data-stu-id="1b8ca-378">3</span></span> |
| <span data-ttu-id="1b8ca-379">UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-379">UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span></span>         | <span data-ttu-id="1b8ca-380">4</span><span class="sxs-lookup"><span data-stu-id="1b8ca-380">4</span></span> |
| <span data-ttu-id="1b8ca-381">UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-381">UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span></span>     | <span data-ttu-id="1b8ca-382">5</span><span class="sxs-lookup"><span data-stu-id="1b8ca-382">5</span></span> |
| <span data-ttu-id="1b8ca-383">UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span><span class="sxs-lookup"><span data-stu-id="1b8ca-383">UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span></span> | <span data-ttu-id="1b8ca-384">6</span><span class="sxs-lookup"><span data-stu-id="1b8ca-384">6</span></span> |
| <span data-ttu-id="1b8ca-385">UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP</span><span class="sxs-lookup"><span data-stu-id="1b8ca-385">UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP</span></span>  | <span data-ttu-id="1b8ca-386">7</span><span class="sxs-lookup"><span data-stu-id="1b8ca-386">7</span></span> |

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_set_line_coding"></a><span data-ttu-id="1b8ca-387">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="1b8ca-387">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span></span>

<span data-ttu-id="1b8ca-388">Eseguire la codifica a linee del set IOCTL sull'interfaccia CDC-ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-388">Perform IOCTL Set Line Coding on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-389">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-389">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM*cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="1b8ca-390">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-390">Description</span></span>

<span data-ttu-id="1b8ca-391">Questa funzione viene chiamata quando un'applicazione deve impostare i parametri di codifica della riga.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-391">This function is called when an application needs to Set the Line Coding parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-392">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-392">Parameters</span></span>

- <span data-ttu-id="1b8ca-393">**cdc_acm**: puntatore all'istanza della classe CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-393">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="1b8ca-394">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="1b8ca-394">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span></span>
- <span data-ttu-id="1b8ca-395">**parametro**: puntatore a una struttura di parametri di linea:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-395">**parameter**: Pointer to a line parameter structure:</span></span>

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER_STRUCT
{
    ULONG ux_slave_class_cdc_acm_parameter_baudrate;
    UCHAR ux_slave_class_cdc_acm_parameter_stop_bit;
    UCHAR ux_slave_class_cdc_acm_parameter_parity;
    UCHAR ux_slave_class_cdc_acm_parameter_data_bit;
} UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER;
```

### <a name="return-value"></a><span data-ttu-id="1b8ca-396">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-396">Return Value</span></span>

<span data-ttu-id="1b8ca-397">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-397">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-398">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-398">Example</span></span>

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

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_get_line_coding"></a><span data-ttu-id="1b8ca-399">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="1b8ca-399">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span></span>

<span data-ttu-id="1b8ca-400">Eseguire IOCTL per ottenere la codifica della riga sull'interfaccia CDC-ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-400">Perform IOCTL Get Line Coding on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-401">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-401">Prototype</span></span>

```c
device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="1b8ca-402">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-402">Description</span></span>

<span data-ttu-id="1b8ca-403">Questa funzione viene chiamata quando un'applicazione deve ottenere i parametri di codifica della riga.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-403">This function is called when an application needs to Get the Line Coding parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-404">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-404">Parameters</span></span>

- <span data-ttu-id="1b8ca-405">**cdc_acm**: puntatore all'istanza della classe CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-405">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="1b8ca-406">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_ LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="1b8ca-406">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_ LINE_CODING</span></span>
- <span data-ttu-id="1b8ca-407">**parametro**: puntatore a una struttura di parametri di linea:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-407">**parameter**: Pointer to a line parameter structure:</span></span>

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER_STRUCT
{
    ULONG ux_slave_class_cdc_acm_parameter_baudrate;
    UCHAR ux_slave_class_cdc_acm_parameter_stop_bit;
    UCHAR ux_slave_class_cdc_acm_parameter_parity;
    UCHAR ux_slave_class_cdc_acm_parameter_data_bit;
} UX_SLAVE_CLASS_CDC_ACM_LINE_CODING_PARAMETER;
```

### <a name="return-value"></a><span data-ttu-id="1b8ca-408">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-408">Return Value</span></span>

- <span data-ttu-id="1b8ca-409">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-409">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-410">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-410">Example</span></span>

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

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_get_line_state"></a><span data-ttu-id="1b8ca-411">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-411">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span></span>

<span data-ttu-id="1b8ca-412">Eseguire IOCTL ottenere lo stato della riga sull'interfaccia CDC-ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-412">Perform IOCTL Get Line State on the CDC-ACM interface</span></span>

## <a name="prototype"></a><span data-ttu-id="1b8ca-413">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-413">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM*cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="1b8ca-414">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-414">Description</span></span>

<span data-ttu-id="1b8ca-415">Questa funzione viene chiamata quando un'applicazione deve ottenere i parametri dello stato della riga.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-415">This function is called when an application needs to Get the Line State parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-416">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-416">Parameters</span></span>

- <span data-ttu-id="1b8ca-417">**cdc_acm**: puntatore all'istanza della classe CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-417">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="1b8ca-418">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-418">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_GET_LINE_STATE</span></span>
- <span data-ttu-id="1b8ca-419">**parametro**: puntatore a una struttura di parametri di linea:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-419">**parameter**: Pointer to a line parameter structure:</span></span>

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER_STRUCT
{
    UCHAR ux_slave_class_cdc_acm_parameter_rts;
    UCHAR ux_slave_class_cdc_acm_parameter_dtr;
} UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER;
```

### <a name="return-value"></a><span data-ttu-id="1b8ca-420">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-420">Return Value</span></span>

- <span data-ttu-id="1b8ca-421">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-421">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-422">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-422">Example</span></span>

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

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_set_line_state"></a><span data-ttu-id="1b8ca-423">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-423">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span></span>

<span data-ttu-id="1b8ca-424">Eseguire lo stato della linea di set IOCTL sull'interfaccia CDC-ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-424">Perform IOCTL Set Line State on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-425">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-425">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="1b8ca-426">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-426">Description</span></span>

<span data-ttu-id="1b8ca-427">Questa funzione viene chiamata quando un'applicazione deve ottenere i parametri dello stato della riga</span><span class="sxs-lookup"><span data-stu-id="1b8ca-427">This function is called when an application needs to Get the Line State parameters</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-428">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-428">Parameters</span></span>

- <span data-ttu-id="1b8ca-429">**cdc_acm**: puntatore all'istanza della classe CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-429">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="1b8ca-430">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-430">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span></span>
- <span data-ttu-id="1b8ca-431">**parametro**: puntatore a una struttura di parametri di linea:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-431">**parameter**: Pointer to a line parameter structure:</span></span>

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER_STRUCT
{
    UCHAR ux_slave_class_cdc_acm_parameter_rts;
    UCHAR ux_slave_class_cdc_acm_parameter_dtr;
} UX_SLAVE_CLASS_CDC_ACM_LINE_STATE_PARAMETER;
```

### <a name="return-value"></a><span data-ttu-id="1b8ca-432">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-432">Return Value</span></span>

- <span data-ttu-id="1b8ca-433">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-433">**UX_SUCCESS** (0x00) This operation was successful.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-434">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-434">Example</span></span>

```c
/* This is to set RTS state. */

line_state.ux_slave_class_cdc_acm_parameter_rts = UX_TRUE;
status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE, &line_state);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_abort_pipe"></a><span data-ttu-id="1b8ca-435">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-435">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span></span>

<span data-ttu-id="1b8ca-436">Eseguire la PIPE di interruzione IOCTL nell'interfaccia CDC-ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-436">Perform IOCTL ABORT PIPE on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-437">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-437">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="1b8ca-438">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-438">Description</span></span>

<span data-ttu-id="1b8ca-439">Questa funzione viene chiamata quando un'applicazione deve interrompere una pipe.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-439">This function is called when an application needs to abort a pipe.</span></span> <span data-ttu-id="1b8ca-440">Ad esempio, per interrompere una scrittura in corso, UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT deve essere passata come parametro.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-440">For example, to abort an ongoing write, UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT should be passed as the parameter.</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-441">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-441">Parameters</span></span>

- <span data-ttu-id="1b8ca-442">**cdc_acm**: puntatore all'istanza della classe CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-442">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="1b8ca-443">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-443">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE</span></span>
- <span data-ttu-id="1b8ca-444">**parametro**: direzione pipe:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-444">**parameter**: The pipe direction:</span></span>

```c
UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT 1

UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_RCV 2
```

### <a name="return-value"></a><span data-ttu-id="1b8ca-445">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-445">Return Value</span></span>

- <span data-ttu-id="1b8ca-446">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-446">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="1b8ca-447">La direzione della pipe **UX_ENDPOINT_HANDLE_UNKNOWN** (0X53) non è valida.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-447">**UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) Invalid pipe direction.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-448">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-448">Example</span></span>

```c
/* This is to abort the Xmit pipe. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_ABORT_PIPE,
    UX_SLAVE_CLASS_CDC_ACM_ENDPOINT_XMIT);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_transmission_start"></a><span data-ttu-id="1b8ca-449">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span><span class="sxs-lookup"><span data-stu-id="1b8ca-449">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span></span>

<span data-ttu-id="1b8ca-450">Eseguire l'avvio della trasmissione IOCTL sull'interfaccia CDC-ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-450">Perform IOCTL Transmission Start on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-451">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-451">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl ( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="1b8ca-452">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-452">Description</span></span>

<span data-ttu-id="1b8ca-453">Questa funzione viene chiamata quando un'applicazione vuole usare la trasmissione con callback.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-453">This function is called when an application wants to use transmission with callback.</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-454">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-454">Parameters</span></span>

- <span data-ttu-id="1b8ca-455">**cdc_acm**: puntatore all'istanza della classe CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-455">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="1b8ca-456">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span><span class="sxs-lookup"><span data-stu-id="1b8ca-456">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START</span></span>
- <span data-ttu-id="1b8ca-457">**parametro**: puntatore alla struttura del parametro di trasmissione iniziale:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-457">**parameter**: Pointer to the Start Transmission parameter structure:</span></span>

```c
typedef struct UX_SLAVE_CLASS_CDC_ACM_CALLBACK_PARAMETER_STRUCT
{
    UINT (*ux_device_class_cdc_acm_parameter_write_callback)(struct UX_SLAVE_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, ULONG length);
    UINT (*ux_device_class_cdc_acm_parameter_read_callback)(struct UX_SLAVE_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, UCHAR *data_pointer, ULONG length);
} UX_SLAVE_CLASS_CDC_ACM_CALLBACK_PARAMETER;
```

### <a name="return-value"></a><span data-ttu-id="1b8ca-458">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-458">Return Value</span></span>

- <span data-ttu-id="1b8ca-459">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-459">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="1b8ca-460">Trasmissione **UX_ERROR** (0xFF) già avviata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-460">**UX_ERROR** (0xFF) Transmission already started.</span></span>
- <span data-ttu-id="1b8ca-461">**UX_MEMORY_INSUFFICIENT** (0X12) un'allocazione di memoria non riuscita.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-461">**UX_MEMORY_INSUFFICIENT** (0x12) A memory allocation failed.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-462">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-462">Example</span></span>

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

### <a name="ux_device_class_cdc_acm_ioctl-ux_slave_class_cdc_acm_ioctl_transmission_stop"></a><span data-ttu-id="1b8ca-463">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP</span><span class="sxs-lookup"><span data-stu-id="1b8ca-463">ux_device_class_cdc_acm_ioctl: UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP</span></span>

<span data-ttu-id="1b8ca-464">Eseguire l'arresto della trasmissione IOCTL sull'interfaccia CDC-ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-464">Perform IOCTL Transmission Stop on the CDC-ACM interface</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-465">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-465">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_ioctl( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function,  
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="1b8ca-466">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-466">Description</span></span>

<span data-ttu-id="1b8ca-467">Questa funzione viene chiamata quando un'applicazione desidera interrompere l'utilizzo della trasmissione con callback.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-467">This function is called when an application wants to stop using transmission with callback.</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-468">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-468">Parameters</span></span>

- <span data-ttu-id="1b8ca-469">**cdc_acm**: puntatore all'istanza della classe CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-469">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="1b8ca-470">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSI ON_STOP</span><span class="sxs-lookup"><span data-stu-id="1b8ca-470">**ioctl_function**: ux_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSI ON_STOP</span></span>
- <span data-ttu-id="1b8ca-471">**parametro**: non usato</span><span class="sxs-lookup"><span data-stu-id="1b8ca-471">**parameter**: Not used</span></span>

### <a name="return-value"></a><span data-ttu-id="1b8ca-472">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-472">Return Value</span></span>

- <span data-ttu-id="1b8ca-473">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-473">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="1b8ca-474">**UX_ERROR** (0Xff) nessuna trasmissione in corso.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-474">**UX_ERROR** (0xFF) No ongoing transmission.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-475">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-475">Example</span></span>

```c
/* Program the stop of transmission. */

status = _ux_device_class_cdc_acm_ioctl(cdc_acm_slave,
    UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_STOP, UX_NULL);

/* If status is UX_SUCCESS, the operation was successful. */
```

### <a name="ux_device_class_cdc_acm_read"></a><span data-ttu-id="1b8ca-476">ux_device_class_cdc_acm_read</span><span class="sxs-lookup"><span data-stu-id="1b8ca-476">ux_device_class_cdc_acm_read</span></span>

<span data-ttu-id="1b8ca-477">Lettura dalla pipe CDC-ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-477">Read from CDC-ACM pipe</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-478">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-478">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_read( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length,  
    ULONG *actual_length);
```

### <a name="description"></a><span data-ttu-id="1b8ca-479">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-479">Description</span></span>

<span data-ttu-id="1b8ca-480">Questa funzione viene chiamata quando un'applicazione deve leggere dalla pipe di dati OUT (dall'host, IN dal dispositivo).</span><span class="sxs-lookup"><span data-stu-id="1b8ca-480">This function is called when an application needs to read from the OUT data pipe (OUT from the host, IN from the device).</span></span> <span data-ttu-id="1b8ca-481">Si tratta di un blocco.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-481">It is blocking.</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-482">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-482">Parameters</span></span>

- <span data-ttu-id="1b8ca-483">**cdc_acm**: puntatore all'istanza della classe CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-483">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="1b8ca-484">**buffer**: indirizzo del buffer in cui verranno archiviati i dati.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-484">**buffer**: Buffer address where data will be stored.</span></span>
- <span data-ttu-id="1b8ca-485">**requested_length**: lunghezza massima prevista.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-485">**requested_length**: The maximum length we expect.</span></span>
- <span data-ttu-id="1b8ca-486">**actual_length**: lunghezza restituita nel buffer.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-486">**actual_length**: The length returned into the buffer.</span></span>

### <a name="return-value"></a><span data-ttu-id="1b8ca-487">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-487">Return Value</span></span>

- <span data-ttu-id="1b8ca-488">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-488">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="1b8ca-489">Lo stato del dispositivo **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) non è più configurato.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-489">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Device is no longer in the configured state.</span></span>
- <span data-ttu-id="1b8ca-490">**UX_TRANSFER_NO_ANSWER** (0X22) nessuna risposta dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-490">**UX_TRANSFER_NO_ANSWER** (0x22) No answer from device.</span></span> <span data-ttu-id="1b8ca-491">Il dispositivo è stato probabilmente disconnesso mentre il trasferimento era in sospeso.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-491">The device was probably disconnected while the transfer was pending.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-492">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-492">Example</span></span>

```c
/* Read from the CDC class. */

status = ux_device_class_cdc_acm_read(cdc, buffer, UX_DEMO_BUFFER_SIZE, &actual_length);

if(status != UX_SUCCESS) return;
```

### <a name="ux_device_class_cdc_acm_write"></a><span data-ttu-id="1b8ca-493">ux_device_class_cdc_acm_write</span><span class="sxs-lookup"><span data-stu-id="1b8ca-493">ux_device_class_cdc_acm_write</span></span>

<span data-ttu-id="1b8ca-494">Scrivere in una pipe CDC-ACM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-494">Write to a CDC-ACM pipe</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-495">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-495">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_write( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length,  
    ULONG *actual_length);
```

### <a name="description"></a><span data-ttu-id="1b8ca-496">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-496">Description</span></span>

<span data-ttu-id="1b8ca-497">Questa funzione viene chiamata quando un'applicazione deve scrivere nella pipe di dati (IN dall'host, dal dispositivo).</span><span class="sxs-lookup"><span data-stu-id="1b8ca-497">This function is called when an application needs to write to the IN data pipe (IN from the host, OUT from the device).</span></span> <span data-ttu-id="1b8ca-498">Si tratta di un blocco.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-498">It is blocking.</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-499">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-499">Parameters</span></span>

- <span data-ttu-id="1b8ca-500">**cdc_acm**: puntatore all'istanza della classe CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-500">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="1b8ca-501">**buffer**: indirizzo del buffer in cui vengono archiviati i dati.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-501">**buffer**: Buffer address where data is stored.</span></span>
- <span data-ttu-id="1b8ca-502">**requested_length**: lunghezza del buffer da scrivere.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-502">**requested_length**: The length of the buffer to write.</span></span>
- <span data-ttu-id="1b8ca-503">**actual_length**: lunghezza restituita nel buffer dopo l'esecuzione della scrittura.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-503">**actual_length**: The length returned into the buffer after write is performed.</span></span>

### <a name="return-value"></a><span data-ttu-id="1b8ca-504">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-504">Return Value</span></span>
- <span data-ttu-id="1b8ca-505">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-505">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="1b8ca-506">Lo stato del dispositivo **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) non è più configurato.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-506">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Device is no longer in the configured state.</span></span>
- <span data-ttu-id="1b8ca-507">**UX_TRANSFER_NO_ANSWER** (0X22) nessuna risposta dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-507">**UX_TRANSFER_NO_ANSWER** (0x22) No answer from device.</span></span> <span data-ttu-id="1b8ca-508">Il dispositivo è stato probabilmente disconnesso mentre il trasferimento era in sospeso.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-508">The device was probably disconnected while the transfer was pending.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-509">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-509">Example</span></span>

```c
/* Write to the CDC class bulk in pipe. */

status = ux_device_class_cdc_acm_write(cdc, buffer, UX_DEMO_BUFFER_SIZE, &actual_length);

if(status != UX_SUCCESS)
    return;
```

### <a name="ux_device_class_cdc_acm_write_with_callback"></a><span data-ttu-id="1b8ca-510">ux_device_class_cdc_acm_write_with_callback</span><span class="sxs-lookup"><span data-stu-id="1b8ca-510">ux_device_class_cdc_acm_write_with_callback</span></span>

<span data-ttu-id="1b8ca-511">Scrittura in una pipe CDC-ACM con callback</span><span class="sxs-lookup"><span data-stu-id="1b8ca-511">Writing to a CDC-ACM pipe with callback</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-512">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-512">Prototype</span></span>

```c
UINT ux_device_class_cdc_acm_write_with_callback( 
    UX_SLAVE_CLASS_CDC_ACM *cdc_acm,
    UCHAR *buffer,  
    ULONG requested_length);
```

### <a name="description"></a><span data-ttu-id="1b8ca-513">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-513">Description</span></span>

<span data-ttu-id="1b8ca-514">Questa funzione viene chiamata quando un'applicazione deve scrivere nella pipe di dati (IN dall'host, dal dispositivo).</span><span class="sxs-lookup"><span data-stu-id="1b8ca-514">This function is called when an application needs to write to the IN data pipe (IN from the host, OUT from the device).</span></span> <span data-ttu-id="1b8ca-515">Questa funzione non è bloccata e il completamento verrà eseguito tramite un set di callback in UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-515">This function is non-blocking and the completion will be done through a callback set in UX_SLAVE_CLASS_CDC_ACM_IOCTL_TRANSMISSION_START.</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-516">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-516">Parameters</span></span>

- <span data-ttu-id="1b8ca-517">**cdc_acm**: puntatore all'istanza della classe CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-517">**cdc_acm**: Pointer to the cdc class instance.</span></span>
- <span data-ttu-id="1b8ca-518">**buffer**: indirizzo del buffer in cui vengono archiviati i dati.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-518">**buffer**: Buffer address where data is stored.</span></span>
- <span data-ttu-id="1b8ca-519">**requested_length**: lunghezza del buffer da scrivere.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-519">**requested_length**: The length of the buffer to write.</span></span>
- <span data-ttu-id="1b8ca-520">**actual_length**: lunghezza restituita nel buffer dopo l'esecuzione della scrittura</span><span class="sxs-lookup"><span data-stu-id="1b8ca-520">**actual_length**: The length returned into the buffer after write is performed</span></span>

### <a name="return-value"></a><span data-ttu-id="1b8ca-521">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-521">Return Value</span></span>

- <span data-ttu-id="1b8ca-522">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-522">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="1b8ca-523">Lo stato del dispositivo **UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) non è più configurato.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-523">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) Device is no longer in the configured state.</span></span>
- <span data-ttu-id="1b8ca-524">**UX_TRANSFER_NO_ANSWER** (0X22) nessuna risposta dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-524">**UX_TRANSFER_NO_ANSWER** (0x22) No answer from device.</span></span> <span data-ttu-id="1b8ca-525">Il dispositivo è stato probabilmente disconnesso mentre il trasferimento era in sospeso.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-525">The device was probably disconnected while the transfer was pending.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-526">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-526">Example</span></span>

```c
/* Write to the CDC class bulk in pipe non blocking mode. */
status = ux_device_class_cdc_acm_write_with_callback(cdc, buffer, UX_DEMO_BUFFER_SIZE);

if(status != UX_SUCCESS)
    return;
```

### <a name="usb-device-cdc-ecm-class"></a><span data-ttu-id="1b8ca-527">Classe dispositivo USB CDC-ECM</span><span class="sxs-lookup"><span data-stu-id="1b8ca-527">USB Device CDC-ECM Class</span></span>

<span data-ttu-id="1b8ca-528">La classe CDC-ECM del dispositivo USB consente a un sistema host USB di comunicare con il dispositivo come dispositivo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-528">The USB device CDC-ECM class allows for a USB host system to communicate with the device as a ethernet device.</span></span> <span data-ttu-id="1b8ca-529">Questa classe è basata sullo standard USB ed è un subset dello standard CDC.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-529">This class is based on the USB standard and is a subset of the CDC standard.</span></span>

<span data-ttu-id="1b8ca-530">Un Framework di dispositivi conformi a CDC-ACM deve essere dichiarato dallo stack del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-530">A CDC-ACM compliant device framework needs to be declared by the device stack.</span></span> <span data-ttu-id="1b8ca-531">Un esempio è disponibile qui di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-531">An example is found here below.</span></span>

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

<span data-ttu-id="1b8ca-532">La classe CDC-ECM usa un approccio del descrittore di dispositivo molto simile a CDC-ACM e richiede anche un descrittore IAD.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-532">The CDC-ECM class uses a very similar device descriptor approach to the CDC-ACM and also requires an IAD descriptor.</span></span> <span data-ttu-id="1b8ca-533">Vedere la classe CDC-ACM per la definizione.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-533">See the CDC-ACM class for definition.</span></span>

<span data-ttu-id="1b8ca-534">Oltre al normale Framework per dispositivi, CDC-ECM richiede descrittori di stringa speciali.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-534">In addition to the regular device framework, the CDC-ECM requires special string descriptors.</span></span> <span data-ttu-id="1b8ca-535">Di seguito è illustrato un esempio.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-535">An example is given below.</span></span>

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

<span data-ttu-id="1b8ca-536">Il descrittore della stringa dell'indirizzo MAC viene usato dalla classe CDC-ECM per rispondere alle query host per l'indirizzo MAC a cui il dispositivo risponde al protocollo TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-536">The MAC address string descriptor is used by the CDC-ECM class to reply to the host queries as to what MAC address the device is answering to at the TCP/IP protocol.</span></span> <span data-ttu-id="1b8ca-537">Può essere impostata sulla scelta del dispositivo, ma deve essere definita qui.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-537">It can be set to the device choice but must be defined here.</span></span>

<span data-ttu-id="1b8ca-538">L'inizializzazione della classe CDC-ECM è la seguente.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-538">The initialization of the CDC-ECM class is as follows.</span></span>

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

<span data-ttu-id="1b8ca-539">L'inizializzazione di questa classe prevede lo stesso callback di funzione per l'attivazione e la disattivazione, anche se in questo caso viene impostato su NULL in modo che non venga eseguito alcun callback.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-539">The initialization of this class expects the same function callback for activation and deactivation, although here as an exercise they are set to NULL so that no callback is performed.</span></span>

<span data-ttu-id="1b8ca-540">I parametri successivi sono per la definizione degli ID del nodo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-540">The next parameters are for the definition of the node IDs.</span></span> <span data-ttu-id="1b8ca-541">2 nodi sono necessari per CDC-ECM, un nodo locale e un nodo remoto.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-541">2 Nodes are necessary for the CDC-ECM, a local node and a remote node.</span></span> <span data-ttu-id="1b8ca-542">Il nodo locale specifica l'indirizzo MAC del dispositivo, mentre il nodo remoto specifica l'indirizzo MAC dell'host.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-542">The local node specifies the MAC address of the device, while the remote node specifies the MAC address of the host.</span></span> <span data-ttu-id="1b8ca-543">Il nodo remoto deve essere uguale a quello dichiarato nel descrittore di stringa del Framework del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-543">The remote node must be the same one as the one declared in the device framework string descriptor.</span></span>

<span data-ttu-id="1b8ca-544">La classe CDC-ECM include API incorporate per il trasferimento dei dati in entrambe le direzioni, ma nascoste all'applicazione perché l'applicazione utente comunicherà con il dispositivo Ethernet USB tramite NetX.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-544">The CDC-ECM class has built-in APIs for transferring data both ways but they are hidden to the application as the user application will communicate with the USB Ethernet device through NetX.</span></span>

<span data-ttu-id="1b8ca-545">La classe USBX CDC-ECM è strettamente legata allo stack di rete NetX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-545">The USBX CDC-ECM class is closely tied to Azure RTOS NetX Network stack.</span></span> <span data-ttu-id="1b8ca-546">Un'applicazione che usa sia NetX che la classe CDC-ECM USBX attiverà lo stack di rete NetX nel modo consueto, ma in aggiunta deve attivare lo stack di rete USB come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-546">An application using both NetX and USBX CDC-ECM class will activate the NetX network stack in its usual way but in addition needs to activate the USB network stack as follows.</span></span>

```c
/* Initialize the NetX system. */
nx_system_initialize();

/* Perform the initialization of the network driver. This will initialize the USBX network layer.*/
ux_network_driver_init();
```

<span data-ttu-id="1b8ca-547">Lo stack di rete USB deve essere attivato solo una volta e non è specifico di CDCECM, ma è richiesto da qualsiasi classe USB che richiede i servizi di NetX.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-547">The USB network stack needs to be activated only once and is not specific to CDCECM but is required by any USB class that requires NetX services.</span></span>

<span data-ttu-id="1b8ca-548">La classe CDC-ECM verrà riconosciuta dagli host MAC OS e Linux.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-548">The CDC-ECM class will be recognized by MAC OS and Linux hosts.</span></span> <span data-ttu-id="1b8ca-549">Non è tuttavia disponibile alcun driver fornito da Microsoft Windows per riconoscere CDC-ECM in modo nativo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-549">But there is no driver supplied by Microsoft Windows to recognize CDC-ECM natively.</span></span> <span data-ttu-id="1b8ca-550">Per le piattaforme Windows sono presenti prodotti commerciali che forniscono il proprio file con estensione inf.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-550">Some commercial products do exist for Windows platforms and they supply their own .inf file.</span></span> <span data-ttu-id="1b8ca-551">Questo file deve essere modificato nello stesso modo in cui si trova il modello CDC-ACM inf per corrispondere al PID/VID del dispositivo di rete USB.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-551">This file will need to be modified the same way as the CDC-ACM inf template to match the PID/VID of the USB network device.</span></span>

## <a name="usb-device-hid-class"></a><span data-ttu-id="1b8ca-552">Classe dispositivo HID USB</span><span class="sxs-lookup"><span data-stu-id="1b8ca-552">USB Device HID Class</span></span>

<span data-ttu-id="1b8ca-553">La classe HID del dispositivo USB consente a un sistema host USB di connettersi a un dispositivo HID con funzionalità client HID specifiche.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-553">The USB device HID class allows for a USB host system to connect to a HID device with specific HID client capabilities.</span></span>

<span data-ttu-id="1b8ca-554">La classe del dispositivo HID USBX è relativamente semplice rispetto al lato host.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-554">USBX HID device class is relatively simple compared to the host side.</span></span> <span data-ttu-id="1b8ca-555">È strettamente legata al comportamento del dispositivo e del relativo descrittore HID.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-555">It is closely tied to the behavior of the device and its HID descriptor.</span></span>

<span data-ttu-id="1b8ca-556">Per tutti i client HID è necessario innanzitutto definire un Framework per dispositivi HID come riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-556">Any HID client requires first to define a HID device framework as the example below.</span></span>

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

<span data-ttu-id="1b8ca-557">Il Framework HID contiene un descrittore di interfaccia che descrive la classe HID e la sottoclasse del dispositivo HID.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-557">The HID framework contains an interface descriptor that describes the HID class and the HID device subclass.</span></span> <span data-ttu-id="1b8ca-558">L'interfaccia HID può essere una classe autonoma o una parte di un dispositivo composito.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-558">The HID interface can be a standalone class or part of a composite device.</span></span>

<span data-ttu-id="1b8ca-559">Attualmente la classe HID USBX non supporta più ID report, perché la maggior parte delle applicazioni richiede un solo ID (ID zero).</span><span class="sxs-lookup"><span data-stu-id="1b8ca-559">Currently, the USBX HID class does not support multiple report IDs, as most applications only require one ID (ID zero).</span></span> <span data-ttu-id="1b8ca-560">Se più ID report sono una funzionalità a cui si è interessati, contattare Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-560">If multiple report IDs is a feature you are interested in, please contact us.</span></span>

<span data-ttu-id="1b8ca-561">L'inizializzazione della classe HID è la seguente, usando una tastiera USB come esempio.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-561">The initialization of the HID class is as follow, using a USB keyboard as an example.</span></span>

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

<span data-ttu-id="1b8ca-562">L'applicazione deve passare alla classe HID un descrittore di report HID e la relativa lunghezza.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-562">The application needs to pass to the HID class a HID report descriptor and its length.</span></span> <span data-ttu-id="1b8ca-563">Il descrittore del report è una raccolta di elementi che descrivono il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-563">The report descriptor is a collection of items that describe the device.</span></span> <span data-ttu-id="1b8ca-564">Per ulteriori informazioni sulla grammatica nascosta, vedere la specifica della classe USB HID.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-564">For more information on the HID grammar refer to the HID USB class specification.</span></span>

<span data-ttu-id="1b8ca-565">Oltre al descrittore del report, l'applicazione passa una chiamata quando si verifica un evento HID.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-565">In addition to the report descriptor, the application passes a call back when a HID event happens.</span></span>

<span data-ttu-id="1b8ca-566">La classe HID USBX supporta i comandi HID standard seguenti dall'host.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-566">The USBX HID class supports the following standard HID commands from the host.</span></span>

| <span data-ttu-id="1b8ca-567">Nome comando</span><span class="sxs-lookup"><span data-stu-id="1b8ca-567">Command name</span></span>                             | <span data-ttu-id="1b8ca-568">Valore</span><span class="sxs-lookup"><span data-stu-id="1b8ca-568">Value</span></span> | <span data-ttu-id="1b8ca-569">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-569">Description</span></span>                                      |
| ---------------------------------------- | ----- | ------------------------------------------------ |
| <span data-ttu-id="1b8ca-570">UX_DEVICE_CLASS_HID_COMMAND_GET_REPORT</span><span class="sxs-lookup"><span data-stu-id="1b8ca-570">UX_DEVICE_CLASS_HID_COMMAND_GET_REPORT</span></span>   | <span data-ttu-id="1b8ca-571">0x01</span><span class="sxs-lookup"><span data-stu-id="1b8ca-571">0x01</span></span>  | <span data-ttu-id="1b8ca-572">Ottenere un report dal dispositivo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-572">Get a report from the device</span></span>                     |
| <span data-ttu-id="1b8ca-573">UX_DEVICE_CLASS_HID_COMMAND_GET_IDLE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-573">UX_DEVICE_CLASS_HID_COMMAND_GET_IDLE</span></span>     | <span data-ttu-id="1b8ca-574">0x02</span><span class="sxs-lookup"><span data-stu-id="1b8ca-574">0x02</span></span>  | <span data-ttu-id="1b8ca-575">Ottenere la frequenza di inattività dell'endpoint di interrupt</span><span class="sxs-lookup"><span data-stu-id="1b8ca-575">Get the idle frequency of the interrupt endpoint</span></span> |
| <span data-ttu-id="1b8ca-576">UX_DEVICE_CLASS_HID_COMMAND_GET_PROTOCOL</span><span class="sxs-lookup"><span data-stu-id="1b8ca-576">UX_DEVICE_CLASS_HID_COMMAND_GET_PROTOCOL</span></span> | <span data-ttu-id="1b8ca-577">0x03</span><span class="sxs-lookup"><span data-stu-id="1b8ca-577">0x03</span></span>  | <span data-ttu-id="1b8ca-578">Ottenere il protocollo in esecuzione nel dispositivo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-578">Get the protocol running on the device</span></span>           |
| <span data-ttu-id="1b8ca-579">UX_DEVICE_CLASS_HID_COMMAND_SET_REPORT</span><span class="sxs-lookup"><span data-stu-id="1b8ca-579">UX_DEVICE_CLASS_HID_COMMAND_SET_REPORT</span></span>   | <span data-ttu-id="1b8ca-580">0x09</span><span class="sxs-lookup"><span data-stu-id="1b8ca-580">0x09</span></span>  | <span data-ttu-id="1b8ca-581">Impostare un report sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-581">Set a report to the device</span></span>                       |
| <span data-ttu-id="1b8ca-582">UX_DEVICE_CLASS_HID_COMMAND_SET_IDLE</span><span class="sxs-lookup"><span data-stu-id="1b8ca-582">UX_DEVICE_CLASS_HID_COMMAND_SET_IDLE</span></span>     | <span data-ttu-id="1b8ca-583">0x0A</span><span class="sxs-lookup"><span data-stu-id="1b8ca-583">0x0a</span></span>  | <span data-ttu-id="1b8ca-584">Imposta la frequenza di inattività dell'endpoint di interrupt</span><span class="sxs-lookup"><span data-stu-id="1b8ca-584">Set the idle frequency of the interrupt endpoint</span></span> |
| <span data-ttu-id="1b8ca-585">UX_DEVICE_CLASS_HID_COMMAND_SET_PROTOCOL</span><span class="sxs-lookup"><span data-stu-id="1b8ca-585">UX_DEVICE_CLASS_HID_COMMAND_SET_PROTOCOL</span></span> | <span data-ttu-id="1b8ca-586">0x0B</span><span class="sxs-lookup"><span data-stu-id="1b8ca-586">0x0b</span></span>  | <span data-ttu-id="1b8ca-587">Ottenere il protocollo in esecuzione nel dispositivo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-587">Get the protocol running on the device</span></span>           |

<span data-ttu-id="1b8ca-588">Il report Get e set sono i comandi usati più di frequente da HID per trasferire i dati tra l'host e il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-588">The Get and Set report are the most commonly used commands by HID to transfer data back and forth between the host and the device.</span></span> <span data-ttu-id="1b8ca-589">Nella maggior parte dei casi l'host invia dati nell'endpoint di controllo ma può ricevere dati nell'endpoint di interrupt oppure eseguendo un comando GET_REPORT per recuperare i dati nell'endpoint di controllo.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-589">Most commonly the host sends data on the control endpoint but can receive data either on the interrupt endpoint or by issuing a GET_REPORT command to fetch the data on the control endpoint.</span></span>

<span data-ttu-id="1b8ca-590">La classe HID può restituire dati all'host nell'endpoint di interrupt utilizzando la funzione ux_device_class_hid_event_set.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-590">The HID class can send data back to the host on the interrupt endpoint by using the ux_device_class_hid_event_set function.</span></span>

### <a name="ux_device_class_hid_event_set"></a><span data-ttu-id="1b8ca-591">ux_device_class_hid_event_set</span><span class="sxs-lookup"><span data-stu-id="1b8ca-591">ux_device_class_hid_event_set</span></span>

<span data-ttu-id="1b8ca-592">Impostazione di un evento per la classe HID</span><span class="sxs-lookup"><span data-stu-id="1b8ca-592">Setting an event to the HID class</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-593">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-593">Prototype</span></span>

```c
UINT ux_device_class_hid_event_set( 
    UX_SLAVE_CLASS_HID *hid,
    UX_SLAVE_CLASS_HID_EVENT *hid_event);
```

### <a name="description"></a><span data-ttu-id="1b8ca-594">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-594">Description</span></span>

<span data-ttu-id="1b8ca-595">Questa funzione viene chiamata quando un'applicazione deve inviare un evento HID all'host.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-595">This function is called when an application needs to send a HID event back to the host.</span></span> <span data-ttu-id="1b8ca-596">Poiché la funzione non blocca, il report viene semplicemente inserito in una coda circolare e viene restituito all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-596">The function is not blocking, it merely puts the report into a circular queue and returns to the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-597">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-597">Parameters</span></span>

- <span data-ttu-id="1b8ca-598">**HID**: puntatore all'istanza della classe HID.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-598">**hid**: Pointer to the hid class instance.</span></span>
- <span data-ttu-id="1b8ca-599">**hid_event**: puntatore alla struttura dell'evento HID.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-599">**hid_event**: Pointer to structure of the hid event.</span></span>

### <a name="return-value"></a><span data-ttu-id="1b8ca-600">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="1b8ca-600">Return Value</span></span>

- <span data-ttu-id="1b8ca-601">**UX_SUCCESS** (0x00) questa operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-601">**UX_SUCCESS** (0x00) This operation was successful.</span></span>
- <span data-ttu-id="1b8ca-602">Errore **UX_ERROR** (0xFF) non è disponibile spazio nella coda circolare.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-602">**UX_ERROR** (0xFF) Error no space available in circular queue.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-603">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-603">Example</span></span>

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

<span data-ttu-id="1b8ca-604">Il callback definito in fase di inizializzazione della classe HID esegue l'opposto dell'invio di un evento.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-604">The callback defined at the initialization of the HID class performs the opposite of sending an event.</span></span> <span data-ttu-id="1b8ca-605">Ottiene come input l'evento inviato dall'host.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-605">It gets as input the event sent by the host.</span></span> <span data-ttu-id="1b8ca-606">Il prototipo del callback è il seguente.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-606">The prototype of the callback is as follows.</span></span>

### <a name="hid_callback"></a><span data-ttu-id="1b8ca-607">hid_callback</span><span class="sxs-lookup"><span data-stu-id="1b8ca-607">hid_callback</span></span>

<span data-ttu-id="1b8ca-608">Recupero di un evento dalla classe HID</span><span class="sxs-lookup"><span data-stu-id="1b8ca-608">Getting an event from the HID class</span></span>

### <a name="prototype"></a><span data-ttu-id="1b8ca-609">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1b8ca-609">Prototype</span></span>

```c
UINT hid_callback(
    UX_SLAVE_CLASS_HID *hid, 
    UX_SLAVE_CLASS_HID_EVENT *hid_event);
```

### <a name="description"></a><span data-ttu-id="1b8ca-610">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1b8ca-610">Description</span></span>

<span data-ttu-id="1b8ca-611">Questa funzione viene chiamata quando l'host invia un report nascosto all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-611">This function is called when the host sends a HID report to the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="1b8ca-612">Parametri</span><span class="sxs-lookup"><span data-stu-id="1b8ca-612">Parameters</span></span>

- <span data-ttu-id="1b8ca-613">**HID**: puntatore all'istanza della classe HID.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-613">**hid**: Pointer to the hid class instance.</span></span>
- <span data-ttu-id="1b8ca-614">**hid_event**: puntatore alla struttura dell'evento HID.</span><span class="sxs-lookup"><span data-stu-id="1b8ca-614">**hid_event**: Pointer to structure of the hid event.</span></span>

### <a name="example"></a><span data-ttu-id="1b8ca-615">Esempio</span><span class="sxs-lookup"><span data-stu-id="1b8ca-615">Example</span></span>

<span data-ttu-id="1b8ca-616">Nell'esempio seguente viene illustrato come interpretare un evento per una tastiera nascosta:</span><span class="sxs-lookup"><span data-stu-id="1b8ca-616">The following example shows how to interpret an event for a HID keyboard:</span></span>

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
