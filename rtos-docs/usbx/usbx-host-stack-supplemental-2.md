---
title: API delle classi host USBX
description: In questo capitolo vengono illustrate tutte le API esposte delle classi host USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 39f3a71c28dd14e0093f72d1a3b1ff6837c6f1f7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824017"
---
# <a name="chapter-2-usbx-host-classes-api"></a><span data-ttu-id="9899c-103">Capitolo 2: API delle classi host USBX</span><span class="sxs-lookup"><span data-stu-id="9899c-103">Chapter 2: USBX Host Classes API</span></span>

<span data-ttu-id="9899c-104">In questo capitolo vengono illustrate tutte le API esposte delle classi host USBX.</span><span class="sxs-lookup"><span data-stu-id="9899c-104">This chapter covers all the exposed APIs of the USBX host classes.</span></span> <span data-ttu-id="9899c-105">Le API seguenti per ogni classe sono descritte in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="9899c-105">The following APIs for each class are described in detail.</span></span>

- <span data-ttu-id="9899c-106">Classe Printer</span><span class="sxs-lookup"><span data-stu-id="9899c-106">Printer class</span></span>
- <span data-ttu-id="9899c-107">Classe audio</span><span class="sxs-lookup"><span data-stu-id="9899c-107">Audio class</span></span>
- <span data-ttu-id="9899c-108">Classe ASIX</span><span class="sxs-lookup"><span data-stu-id="9899c-108">Asix class</span></span>
- <span data-ttu-id="9899c-109">Classe Pima/PTP</span><span class="sxs-lookup"><span data-stu-id="9899c-109">Pima/PTP class</span></span>
- <span data-ttu-id="9899c-110">Classe Prolific</span><span class="sxs-lookup"><span data-stu-id="9899c-110">Prolific class</span></span>
- <span data-ttu-id="9899c-111">Classe seriale generica</span><span class="sxs-lookup"><span data-stu-id="9899c-111">Generic Serial class</span></span>

## <a name="ux_host_class_printer_read"></a><span data-ttu-id="9899c-112">ux_host_class_printer_read</span><span class="sxs-lookup"><span data-stu-id="9899c-112">ux_host_class_printer_read</span></span>

<span data-ttu-id="9899c-113">Leggere dall'interfaccia stampante.</span><span class="sxs-lookup"><span data-stu-id="9899c-113">Read from the printer interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-114">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-114">Prototype</span></span>

```C
UINT ux_host_class_printer_read(
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="9899c-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-115">Description</span></span>

<span data-ttu-id="9899c-116">Questa funzione legge dall'interfaccia stampante.</span><span class="sxs-lookup"><span data-stu-id="9899c-116">This function reads from the printer interface.</span></span> <span data-ttu-id="9899c-117">La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.</span><span class="sxs-lookup"><span data-stu-id="9899c-117">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span> <span data-ttu-id="9899c-118">Una lettura è consentita solo su stampanti bidirezionali.</span><span class="sxs-lookup"><span data-stu-id="9899c-118">A read is allowed only on bi-directional printers.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-119">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-119">Parameters</span></span>

- <span data-ttu-id="9899c-120">**Printer**: puntatore all'istanza della classe Printer.</span><span class="sxs-lookup"><span data-stu-id="9899c-120">**printer**: Pointer to the printer class instance.</span></span>
- <span data-ttu-id="9899c-121">**data_pointer**: puntatore all'indirizzo del buffer del payload di dati.</span><span class="sxs-lookup"><span data-stu-id="9899c-121">**data_pointer**: Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="9899c-122">**requested_length**: lunghezza da ricevere.</span><span class="sxs-lookup"><span data-stu-id="9899c-122">**requested_length**: Length to be received.</span></span>
- <span data-ttu-id="9899c-123">**actual_length**: lunghezza effettivamente ricevuta.</span><span class="sxs-lookup"><span data-stu-id="9899c-123">**actual_length**: Length actually received.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-124">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-124">Return Value</span></span>

- <span data-ttu-id="9899c-125">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-125">**UX_SUCCESS**:  (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-126">La funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non è supportata perché la stampante non è bidirezionale.</span><span class="sxs-lookup"><span data-stu-id="9899c-126">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported because the printer is not bi-directional.</span></span>
- <span data-ttu-id="9899c-127">**UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, lettura incompleta.</span><span class="sxs-lookup"><span data-stu-id="9899c-127">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, reading incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-128">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-128">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_read(printer, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_write"></a><span data-ttu-id="9899c-129">ux_host_class_printer_write</span><span class="sxs-lookup"><span data-stu-id="9899c-129">ux_host_class_printer_write</span></span>

<span data-ttu-id="9899c-130">Scrivere nell'interfaccia stampante.</span><span class="sxs-lookup"><span data-stu-id="9899c-130">Write to the printer interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-131">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-131">Prototype</span></span>

```C
UINT ux_host_class_printer_write(
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *data_pointer,  
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="9899c-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-132">Description</span></span>

<span data-ttu-id="9899c-133">Questa funzione scrive nell'interfaccia stampante.</span><span class="sxs-lookup"><span data-stu-id="9899c-133">This function writes to the printer interface.</span></span> <span data-ttu-id="9899c-134">La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.</span><span class="sxs-lookup"><span data-stu-id="9899c-134">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-135">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-135">Parameters</span></span>

- <span data-ttu-id="9899c-136">**Printer**: puntatore all'istanza della classe Printer.</span><span class="sxs-lookup"><span data-stu-id="9899c-136">**printer**: Pointer to the printer class instance.</span></span>
- <span data-ttu-id="9899c-137">**data_pointer**: puntatore all'indirizzo del buffer del payload di dati.</span><span class="sxs-lookup"><span data-stu-id="9899c-137">**data_pointer**: Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="9899c-138">**requested_length**: lunghezza da inviare.</span><span class="sxs-lookup"><span data-stu-id="9899c-138">**requested_length**: Length to be sent.</span></span>
- <span data-ttu-id="9899c-139">**actual_length**: lunghezza effettivamente inviata.</span><span class="sxs-lookup"><span data-stu-id="9899c-139">**actual_length**: Length actually sent.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-140">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-140">Return Value</span></span>

- <span data-ttu-id="9899c-141">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-141">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-142">**UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, scrittura incompleta.</span><span class="sxs-lookup"><span data-stu-id="9899c-142">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, writing incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-143">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-143">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_write(printer, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_soft_reset"></a><span data-ttu-id="9899c-144">ux_host_class_printer_soft_reset</span><span class="sxs-lookup"><span data-stu-id="9899c-144">ux_host_class_printer_soft_reset</span></span>

<span data-ttu-id="9899c-145">Eseguire un ripristino soft alla stampante.</span><span class="sxs-lookup"><span data-stu-id="9899c-145">Perform a soft reset to the printer.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-146">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-146">Prototype</span></span>

```C
UINT ux_host_class_printer_soft_reset(UX_HOST_CLASS_PRINTER *printer)
```

### <a name="description"></a><span data-ttu-id="9899c-147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-147">Description</span></span>

<span data-ttu-id="9899c-148">Questa funzione esegue un ripristino soft alla stampante.</span><span class="sxs-lookup"><span data-stu-id="9899c-148">This function performs a soft reset to the printer.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="9899c-149">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="9899c-149">Input Parameter</span></span>

- <span data-ttu-id="9899c-150">**Printer**: puntatore all'istanza della classe Printer.</span><span class="sxs-lookup"><span data-stu-id="9899c-150">**printer**: Pointer to the printer class instance.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-151">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-151">Return Value</span></span>

- <span data-ttu-id="9899c-152">**UX_SUCCESS**: (0x00) la reimpostazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="9899c-152">**UX_SUCCESS**: (0x00)The reset was completed.</span></span>
- <span data-ttu-id="9899c-153">**UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, reimpostazione non completata.</span><span class="sxs-lookup"><span data-stu-id="9899c-153">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, reset not completed.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-154">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-154">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_soft_reset(printer);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_status_get"></a><span data-ttu-id="9899c-155">ux_host_class_printer_status_get</span><span class="sxs-lookup"><span data-stu-id="9899c-155">ux_host_class_printer_status_get</span></span>

<span data-ttu-id="9899c-156">Ottenere lo stato della stampante</span><span class="sxs-lookup"><span data-stu-id="9899c-156">Get the printer status</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-157">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-157">Prototype</span></span>

```C
UINT ux_host_class_printer_status_get( 
    UX_HOST_CLASS_PRINTER *printer,
    ULONG *printer_status)
```

### <a name="description"></a><span data-ttu-id="9899c-158">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-158">Description</span></span>

<span data-ttu-id="9899c-159">Questa funzione ottiene lo stato della stampante.</span><span class="sxs-lookup"><span data-stu-id="9899c-159">This function obtains the printer status.</span></span> <span data-ttu-id="9899c-160">Lo stato della stampante è simile allo stato di LPT (1284 standard).</span><span class="sxs-lookup"><span data-stu-id="9899c-160">The printer status is similar to the LPT status (1284 standard).</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-161">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-161">Parameters</span></span>

- <span data-ttu-id="9899c-162">**Printer**: puntatore all'istanza della classe Printer.</span><span class="sxs-lookup"><span data-stu-id="9899c-162">**printer**: Pointer to the printer class instance.</span></span>
- <span data-ttu-id="9899c-163">**printer_status**: indirizzo dello stato da restituire.</span><span class="sxs-lookup"><span data-stu-id="9899c-163">**printer_status**: Address of the status to be returned.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-164">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-164">Return Value</span></span>

- <span data-ttu-id="9899c-165">**UX_SUCCESS** (0x00): la reimpostazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="9899c-165">**UX_SUCCESS** (0x00): The reset was completed.</span></span>
- <span data-ttu-id="9899c-166">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per eseguire l'operazione.</span><span class="sxs-lookup"><span data-stu-id="9899c-166">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to perform the operation.</span></span>
- <span data-ttu-id="9899c-167">**UX_TRANSFER_TIMEOUT**: (0x5c) Timeout trasferimento, reimpostazione non completata</span><span class="sxs-lookup"><span data-stu-id="9899c-167">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, reset not completed</span></span>

### <a name="example"></a><span data-ttu-id="9899c-168">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-168">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_status_get(printer, printer_status);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_printer_device_id_get"></a><span data-ttu-id="9899c-169">ux_host_class_printer_device_id_get</span><span class="sxs-lookup"><span data-stu-id="9899c-169">ux_host_class_printer_device_id_get</span></span>

<span data-ttu-id="9899c-170">Ottenere l'ID del dispositivo stampante.</span><span class="sxs-lookup"><span data-stu-id="9899c-170">Get the printer device id.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-171">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-171">Prototype</span></span>

```C
UINT ux_host_class_printer_device_id_get( 
    UX_HOST_CLASS_PRINTER *printer,
    UCHAR *descriptor_buffer, 
    ULONG length)
```

### <a name="description"></a><span data-ttu-id="9899c-172">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-172">Description</span></span>

<span data-ttu-id="9899c-173">Questa funzione ottiene la stringa dell'ID dispositivo IEEE 1284 (inclusa la lunghezza nei primi due byte nel formato big endian).</span><span class="sxs-lookup"><span data-stu-id="9899c-173">This function obtains the printer IEEE 1284 device ID string (including length in the first two bytes in big endian format).</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-174">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-174">Parameters</span></span>

- <span data-ttu-id="9899c-175">**Printer**: puntatore all'istanza della classe Printer.</span><span class="sxs-lookup"><span data-stu-id="9899c-175">**printer**: Pointer to the printer class instance.</span></span>
- <span data-ttu-id="9899c-176">**descriptor_buffer**: puntatore a un buffer per riempire la stringa dell'ID dispositivo IEEE 1284 (inclusa la lunghezza nei primi due byte nel formato)</span><span class="sxs-lookup"><span data-stu-id="9899c-176">**descriptor_buffer**: Pointer to a buffer to fill IEEE 1284 device ID string (including length in the first two bytes in BE format)</span></span> 
- <span data-ttu-id="9899c-177">**length**: lunghezza del buffer in byte.</span><span class="sxs-lookup"><span data-stu-id="9899c-177">**length**: Length of buffer in bytes.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-178">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-178">Return Value</span></span>

- <span data-ttu-id="9899c-179">**UX_SUCCESS** (0x00): l'operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="9899c-179">**UX_SUCCESS** (0x00): The operation was successful.</span></span>
- <span data-ttu-id="9899c-180">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per eseguire l'operazione.</span><span class="sxs-lookup"><span data-stu-id="9899c-180">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to perform the operation.</span></span>
- <span data-ttu-id="9899c-181">**UX_TRANSFER_TIMEOUT**: (0x5c) Timeout trasferimento, richiesta non completata</span><span class="sxs-lookup"><span data-stu-id="9899c-181">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, request not completed</span></span>
- <span data-ttu-id="9899c-182">**UX_TRANSFER_NOT_READY**: (0x25) il dispositivo si trova in uno stato non valido. deve essere collegato, risolto o configurato.</span><span class="sxs-lookup"><span data-stu-id="9899c-182">**UX_TRANSFER_NOT_READY**: (0x25) The device was in an invalid state – must be ATTACHED,ADDRESSED, or CONFIGURED.</span></span>
- <span data-ttu-id="9899c-183">**UX_TRANSFER_STALL**: (0x21) il trasferimento è bloccato.</span><span class="sxs-lookup"><span data-stu-id="9899c-183">**UX_TRANSFER_STALL**: (0x21) Transfer stalled.</span></span>
- <span data-ttu-id="9899c-184">La sospensione **TX_WAIT_ABORTED** (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="9899c-184">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="9899c-185">**TX_SEMAPHORE_ERROR** (0x0C) puntatore del semaforo di conteggio non valido.</span><span class="sxs-lookup"><span data-stu-id="9899c-185">**TX_SEMAPHORE_ERROR** (0x0C) Invalid counting semaphore pointer.</span></span>
- <span data-ttu-id="9899c-186">**TX_WAIT_ERROR** (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="9899c-186">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a non-thread.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-187">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-187">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_printer_device_id_get(printer, descriptor_buffer, length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_read"></a><span data-ttu-id="9899c-188">ux_host_class_audio_read</span><span class="sxs-lookup"><span data-stu-id="9899c-188">ux_host_class_audio_read</span></span>

<span data-ttu-id="9899c-189">Leggere dall'interfaccia audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-189">Read from the audio interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-190">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-190">Prototype</span></span>

```C
UINT ux_host_class_audio_read(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_TRANSFER_REQUEST
    *audio_transfer_request)
```

### <a name="description"></a><span data-ttu-id="9899c-191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-191">Description</span></span>

<span data-ttu-id="9899c-192">Questa funzione legge dall'interfaccia audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-192">This function reads from the audio interface.</span></span> <span data-ttu-id="9899c-193">La chiamata non è bloccata.</span><span class="sxs-lookup"><span data-stu-id="9899c-193">The call is non-blocking.</span></span> <span data-ttu-id="9899c-194">L'applicazione deve verificare che sia stata selezionata l'impostazione alternativa appropriata per l'interfaccia di streaming audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-194">The application must ensure that the appropriate alternate setting has been selected for the audio streaming interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-195">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-195">Parameters</span></span>

- <span data-ttu-id="9899c-196">**audio**: puntatore all'istanza della classe audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-196">**audio**: Pointer to the audio class instance.</span></span>
- <span data-ttu-id="9899c-197">**audio_transfer_request**: puntatore alla struttura di trasferimento audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-197">**audio_transfer_request**: Pointer to the audio transfer structure.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-198">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-198">Return Value</span></span>

- <span data-ttu-id="9899c-199">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato</span><span class="sxs-lookup"><span data-stu-id="9899c-199">**UX_SUCCESS**: (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="9899c-200">Funzione **UX_FUNCTION_NOT_SUPPORTED**"(0x54) non supportata</span><span class="sxs-lookup"><span data-stu-id="9899c-200">**UX_FUNCTION_NOT_SUPPORTED**" (0x54) Function not supported</span></span>

### <a name="example"></a><span data-ttu-id="9899c-201">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-201">Example</span></span>

```C
/* The following example reads from the audio interface. */

audio_transfer_request.ux_host_class_audio_transfer_request_completion_function = tx_audio_transfer_completion_function;
audio_transfer_request.ux_host_class_audio_transfer_request_class_instance = audio;
audio_transfer_request.ux_host_class_audio_transfer_request_next_audio_audio_transfer_request = UX_NULL;
audio_transfer_request.ux_host_class_audio_transfer_request_data_pointer = audio_buffer;
audio_transfer_request.ux_host_class_audio_transfer_request_requested_length = requested_length;
audio_transfer_request.ux_host_class_audio_transfer_request_packet_length = AUDIO_FRAME_LENGTH;

status = ux_host_class_audio_read(audio, audio_transfer_request);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_write"></a><span data-ttu-id="9899c-202">ux_host_class_audio_write</span><span class="sxs-lookup"><span data-stu-id="9899c-202">ux_host_class_audio_write</span></span>

<span data-ttu-id="9899c-203">Scrivere nell'interfaccia audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-203">Write to the audio interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-204">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-204">Prototype</span></span>

```C
UINT ux_host_class_audio_write(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_TRANSFER_REQUEST *audio_transfer_request)
```

### <a name="description"></a><span data-ttu-id="9899c-205">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-205">Description</span></span>

<span data-ttu-id="9899c-206">Questa funzione scrive nell'interfaccia audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-206">This function writes to the audio interface.</span></span> <span data-ttu-id="9899c-207">La chiamata non è bloccata.</span><span class="sxs-lookup"><span data-stu-id="9899c-207">The call is non-blocking.</span></span> <span data-ttu-id="9899c-208">L'applicazione deve verificare che sia stata selezionata l'impostazione alternativa appropriata per l'interfaccia di streaming audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-208">The application must ensure that the appropriate alternate setting has been selected for the audio streaming interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-209">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-209">Parameters</span></span>

- <span data-ttu-id="9899c-210">**audio**: puntatore all'istanza della classe audio</span><span class="sxs-lookup"><span data-stu-id="9899c-210">**audio**: Pointer to the audio class instance</span></span>
- <span data-ttu-id="9899c-211">**audio_transfer_request**: puntatore alla struttura di trasferimento audio</span><span class="sxs-lookup"><span data-stu-id="9899c-211">**audio_transfer_request**: Pointer to the audio transfer structure</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-212">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-212">Return Value</span></span>

- <span data-ttu-id="9899c-213">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-213">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-214">Funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non supportata.</span><span class="sxs-lookup"><span data-stu-id="9899c-214">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported.</span></span>
- <span data-ttu-id="9899c-215">Interfaccia **ux_host_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) non corretta.</span><span class="sxs-lookup"><span data-stu-id="9899c-215">**ux_host_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) Interface incorrect.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-216">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-216">Example</span></span>

```C
UINT status;

/* The following example writes to the audio interface */

audio_transfer_request.ux_host_class_audio_transfer_request_completion_function = tx_audio_transfer_completion_function;
audio_transfer_request.ux_host_class_audio_transfer_request_class_instance = audio;
audio_transfer_request.ux_host_class_audio_transfer_request_next_audio_audio_transfer_request = UX_NULL;
audio_transfer_request.ux_host_class_audio_transfer_request_data_pointer = audio_buffer;
audio_transfer_request.ux_host_class_audio_transfer_request_requested_length = requested_length;
audio_transfer_request.ux_host_class_audio_transfer_request_packet_length = AUDIO_FRAME_LENGTH;
status = ux_host_class_audio_write(audio, audio_transfer_request);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_control_get"></a><span data-ttu-id="9899c-217">ux_host_class_audio_control_get</span><span class="sxs-lookup"><span data-stu-id="9899c-217">ux_host_class_audio_control_get</span></span>

<span data-ttu-id="9899c-218">Ottenere un controllo specifico dall'interfaccia del controllo audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-218">Get a specific control from the audio control interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-219">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-219">Prototype</span></span>

```C
UINT ux_host_class_audio_control_get(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_CONTROL *audio_control)
```

### <a name="description"></a><span data-ttu-id="9899c-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-220">Description</span></span>

<span data-ttu-id="9899c-221">Questa funzione legge un controllo specifico dall'interfaccia del controllo audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-221">This function reads a specific control from the audio control interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-222">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-222">Parameters</span></span>

- <span data-ttu-id="9899c-223">**audio**: puntatore all'istanza della classe audio</span><span class="sxs-lookup"><span data-stu-id="9899c-223">**audio**: Pointer to the audio class instance</span></span>
- <span data-ttu-id="9899c-224">**audio_control**: puntatore alla struttura del controllo audio</span><span class="sxs-lookup"><span data-stu-id="9899c-224">**audio_control**: Pointer to the audio control structure</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-225">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-225">Return Value</span></span>

- <span data-ttu-id="9899c-226">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato</span><span class="sxs-lookup"><span data-stu-id="9899c-226">**UX_SUCCESS**: (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="9899c-227">Funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non supportata</span><span class="sxs-lookup"><span data-stu-id="9899c-227">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported</span></span>
- <span data-ttu-id="9899c-228">Interfaccia **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) non corretta</span><span class="sxs-lookup"><span data-stu-id="9899c-228">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) Interface incorrect</span></span>

### <a name="example"></a><span data-ttu-id="9899c-229">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-229">Example</span></span>

```C
UINT status;

/* The following example reads the volume control from a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_CONTROL audio_control;

audio_control.ux_host_class_audio_control_channel = 1;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;

status = ux_host_class_audio_control_get(audio, &audio_control);

/* If status equals UX_SUCCESS, the operation was successful. */

audio_control.ux_host_class_audio_control_channel = 2;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;

status = ux_host_class_audio_control_get(audio, &audio_control);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_control_value_set"></a><span data-ttu-id="9899c-230">ux_host_class_audio_control_value_set</span><span class="sxs-lookup"><span data-stu-id="9899c-230">ux_host_class_audio_control_value_set</span></span>

<span data-ttu-id="9899c-231">Impostare un controllo specifico sull'interfaccia del controllo audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-231">Set a specific control to the audio control interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-232">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-232">Prototype</span></span>

```C
UINT ux_host_class_audio_control_value_set(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_CONTROL *audio_control)
```

<span data-ttu-id="9899c-233">\* \* Descrizione \* \*</span><span class="sxs-lookup"><span data-stu-id="9899c-233">\*\*Description \*\*</span></span>

<span data-ttu-id="9899c-234">Questa funzione imposta un controllo specifico sull'interfaccia del controllo audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-234">This function sets a specific control to the audio control interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-235">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-235">Parameters</span></span>

- <span data-ttu-id="9899c-236">**audio**: puntatore all'istanza della classe audio</span><span class="sxs-lookup"><span data-stu-id="9899c-236">**audio**: Pointer to the audio class instance</span></span>
- <span data-ttu-id="9899c-237">**audio_control**: puntatore alla struttura del controllo audio</span><span class="sxs-lookup"><span data-stu-id="9899c-237">**audio_control**: Pointer to the audio control structure</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-238">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-238">Return Value</span></span>

- <span data-ttu-id="9899c-239">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato</span><span class="sxs-lookup"><span data-stu-id="9899c-239">**UX_SUCCESS**: (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="9899c-240">Funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non supportata</span><span class="sxs-lookup"><span data-stu-id="9899c-240">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported</span></span>
- <span data-ttu-id="9899c-241">Interfaccia **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) non corretta</span><span class="sxs-lookup"><span data-stu-id="9899c-241">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) Interface incorrect</span></span>

### <a name="example"></a><span data-ttu-id="9899c-242">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-242">Example</span></span>

```C
/* The following example sets the volume control of a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_CONTROL audio_control;

UINT status;

audio_control.ux_host_class_audio_control_channel = 1;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
audio_control.ux_host_class_audio_control_cur = 0xf000;

status = ux_host_class_audio_control_value_set(audio, &audio_control);
/* If status equals UX_SUCCESS, the operation was successful. */

current_volume = audio_control.audio_control_cur;
audio_control.ux_host_class_audio_control_channel = 2;
audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
audio_control.ux_host_class_audio_control_cur = 0xf000;

status = ux_host_class_audio_control_value_set(audio, &audio_control);
/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_streaming_sampling_set"></a><span data-ttu-id="9899c-243">ux_host_class_audio_streaming_sampling_set</span><span class="sxs-lookup"><span data-stu-id="9899c-243">ux_host_class_audio_streaming_sampling_set</span></span>

<span data-ttu-id="9899c-244">Impostare un'interfaccia di impostazione alternativa dell'interfaccia di streaming audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-244">Set an alternate setting interface of the audio streaming interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-245">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-245">Prototype</span></span>

```C
UINT ux_host_class_audio_streaming_sampling_set
    (UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_SAMPLING *audio_sampling)
```

### <a name="description"></a><span data-ttu-id="9899c-246">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-246">Description</span></span>

<span data-ttu-id="9899c-247">Questa funzione imposta l'interfaccia di impostazione alternativa appropriata dell'interfaccia di streaming audio in base a una struttura di campionamento specifica.</span><span class="sxs-lookup"><span data-stu-id="9899c-247">This function sets the appropriate alternate setting interface of the audio streaming interface according to a specific sampling structure.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-248">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-248">Parameters</span></span>

- <span data-ttu-id="9899c-249">**audio**: puntatore all'istanza della classe audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-249">**audio**: Pointer to the audio class instance.</span></span>
- <span data-ttu-id="9899c-250">**audio_sampling**: puntatore alla struttura di campionamento audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-250">**audio_sampling**: Pointer to the audio sampling structure.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-251">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-251">Return Value</span></span>

- <span data-ttu-id="9899c-252">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato</span><span class="sxs-lookup"><span data-stu-id="9899c-252">**UX_SUCCESS**: (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="9899c-253">Funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non supportata</span><span class="sxs-lookup"><span data-stu-id="9899c-253">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported</span></span>
- <span data-ttu-id="9899c-254">Interfaccia **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) non corretta</span><span class="sxs-lookup"><span data-stu-id="9899c-254">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) Interface incorrect</span></span>
- <span data-ttu-id="9899c-255">**UX_NO_ALTERNATE_SETTING**: (0X5e) nessuna impostazione alternativa per i valori di campionamento</span><span class="sxs-lookup"><span data-stu-id="9899c-255">**UX_NO_ALTERNATE_SETTING**: (0x5e) No alternate setting for the sampling values</span></span>

### <a name="example"></a><span data-ttu-id="9899c-256">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-256">Example</span></span>

```C
/* The following example sets the alternate setting interface of a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_SAMPLING audio_sampling;

UINT status;

sampling.ux_host_class_audio_sampling_channels = 2;
sampling.ux_host_class_audio_sampling_frequency = AUDIO_FREQUENCY;
sampling. ux_host_class_audio_sampling_resolution = 16;

status = ux_host_class_audio_streaming_sampling_set(audio, &sampling);
/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_audio_streaming_sampling_get"></a><span data-ttu-id="9899c-257">ux_host_class_audio_streaming_sampling_get</span><span class="sxs-lookup"><span data-stu-id="9899c-257">ux_host_class_audio_streaming_sampling_get</span></span>

<span data-ttu-id="9899c-258">Ottenere le possibili impostazioni di campionamento dell'interfaccia di streaming audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-258">Get possible sampling settings of audio streaming interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-259">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-259">Prototype</span></span>

```C
UINT ux_host_class_audio_streaming_sampling_get(
    UX_HOST_CLASS_AUDIO *audio,
    UX_HOST_CLASS_AUDIO_SAMPLING_CHARACTERISTICS *audio_sampling)
```

### <a name="description"></a><span data-ttu-id="9899c-260">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-260">Description</span></span>

<span data-ttu-id="9899c-261">Questa funzione ottiene, una alla volta, tutte le possibili impostazioni di campionamento disponibili in ognuna delle impostazioni alternative dell'interfaccia di streaming audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-261">This function gets, one by one, all the possible sampling settings available in each of the alternate settings of the audio streaming interface.</span></span> <span data-ttu-id="9899c-262">La prima volta che si usa la funzione, è necessario reimpostare tutti i campi nel puntatore della struttura chiamante.</span><span class="sxs-lookup"><span data-stu-id="9899c-262">The first time the function is used, all the fields in the calling structure pointer must be reset.</span></span> <span data-ttu-id="9899c-263">La funzione restituirà un set specifico di valori di flusso alla restituzione, a meno che non sia stata raggiunta la fine delle impostazioni alternative.</span><span class="sxs-lookup"><span data-stu-id="9899c-263">The function will return a specific set of streaming values upon return unless the end of the alternate settings has been reached.</span></span> <span data-ttu-id="9899c-264">Quando questa funzione viene riutilizzata, per individuare i valori di campionamento successivi verranno utilizzati i valori di campionamento precedenti.</span><span class="sxs-lookup"><span data-stu-id="9899c-264">When this function is reused, the previous sampling values will be used to find the next sampling values.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-265">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-265">Parameters</span></span>

- <span data-ttu-id="9899c-266">**audio**: puntatore all'istanza della classe audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-266">**audio**: Pointer to the audio class instance.</span></span>
- <span data-ttu-id="9899c-267">**audio_sampling**: puntatore alla struttura di campionamento audio.</span><span class="sxs-lookup"><span data-stu-id="9899c-267">**audio_sampling**: Pointer to the audio sampling structure.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-268">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-268">Return Value</span></span>

- <span data-ttu-id="9899c-269">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato</span><span class="sxs-lookup"><span data-stu-id="9899c-269">**UX_SUCCESS**: (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="9899c-270">Funzione **UX_FUNCTION_NOT_SUPPORTED**: (0x54) non supportata</span><span class="sxs-lookup"><span data-stu-id="9899c-270">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Function not supported</span></span>
- <span data-ttu-id="9899c-271">Interfaccia **UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) non corretta</span><span class="sxs-lookup"><span data-stu-id="9899c-271">**UX_HOST_CLASS_AUDIO_WRONG_INTERFACE**: (0x81) Interface incorrect</span></span>
- <span data-ttu-id="9899c-272">**UX_NO_ALTERNATE_SETTING**: (0X5e) nessuna impostazione alternativa per i valori di campionamento</span><span class="sxs-lookup"><span data-stu-id="9899c-272">**UX_NO_ALTERNATE_SETTING**: (0x5e) No alternate setting for the sampling values</span></span>

### <a name="example"></a><span data-ttu-id="9899c-273">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-273">Example</span></span>

```C
/* The following example gets the sampling values for the first alternate setting interface of a stereo USB speaker. */

UX_HOST_CLASS_AUDIO_SAMPLING_CHARACTERISTICS audio_sampling;

UINT status;

sampling.ux_host_class_audio_sampling_channels=0;
sampling.ux_host_class_audio_sampling_frequency_low=0;
sampling.ux_host_class_audio_sampling_frequency_high=0;
sampling.ux_host_class_audio_sampling_resolution=0;

status = ux_host_class_audio_streaming_sampling_get(audio, &sampling);

/* If status equals UX_SUCCESS, the operation was successful and information could be displayed as follows:

printf("Number of channels %d, Resolution %d bits, frequency range %d-%d\n",
    sampling.audio_channels, sampling.audio_resolution,
    sampling.audio_frequency_low, sampling.audio_frequency_high);

*/
```

## <a name="ux_host_class_asix_read"></a><span data-ttu-id="9899c-274">ux_host_class_asix_read</span><span class="sxs-lookup"><span data-stu-id="9899c-274">ux_host_class_asix_read</span></span>

<span data-ttu-id="9899c-275">Leggere dall'interfaccia ASIX.</span><span class="sxs-lookup"><span data-stu-id="9899c-275">Read from the asix interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-276">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-276">Prototype</span></span>

```C
UINT ux_host_class_asix_read(
    UX_HOST_CLASS_ASIX *asix,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="9899c-277">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-277">Description</span></span>

<span data-ttu-id="9899c-278">Questa funzione legge dall'interfaccia ASIX.</span><span class="sxs-lookup"><span data-stu-id="9899c-278">This function reads from the asix interface.</span></span> <span data-ttu-id="9899c-279">La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.</span><span class="sxs-lookup"><span data-stu-id="9899c-279">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-280">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-280">Parameters</span></span>

- <span data-ttu-id="9899c-281">**ASIX**: puntatore all'istanza della classe ASIX.</span><span class="sxs-lookup"><span data-stu-id="9899c-281">**asix**: Pointer to the asix class instance.</span></span>
- <span data-ttu-id="9899c-282">**data_pointer**: puntatore all'indirizzo del buffer del payload di dati.</span><span class="sxs-lookup"><span data-stu-id="9899c-282">**data_pointer**: Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="9899c-283">**requested_length**: lunghezza da ricevere.</span><span class="sxs-lookup"><span data-stu-id="9899c-283">**requested_length**: Length to be received.</span></span>
- <span data-ttu-id="9899c-284">**actual_length**: lunghezza effettivamente ricevuta.</span><span class="sxs-lookup"><span data-stu-id="9899c-284">**actual_length**: Length actually received.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-285">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-285">Return Value</span></span>

- <span data-ttu-id="9899c-286">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-286">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-287">**UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, lettura incompleta.</span><span class="sxs-lookup"><span data-stu-id="9899c-287">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, reading incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-288">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-288">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_asix_read(asix, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_asix_write"></a><span data-ttu-id="9899c-289">ux_host_class_asix_write</span><span class="sxs-lookup"><span data-stu-id="9899c-289">ux_host_class_asix_write</span></span>

<span data-ttu-id="9899c-290">Scrivere nell'interfaccia ASIX.</span><span class="sxs-lookup"><span data-stu-id="9899c-290">Write to the asix interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-291">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-291">Prototype</span></span>

```C
UINT ux_host_class_asix_write(
    VOID *asix_class,
    NX_PACKET *packet)
```

### <a name="description"></a><span data-ttu-id="9899c-292">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-292">Description</span></span>

<span data-ttu-id="9899c-293">Questa funzione scrive nell'interfaccia ASIX.</span><span class="sxs-lookup"><span data-stu-id="9899c-293">This function writes to the asix interface.</span></span> <span data-ttu-id="9899c-294">La chiamata non è bloccata.</span><span class="sxs-lookup"><span data-stu-id="9899c-294">The call is non blocking.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-295">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-295">Parameters</span></span>

- <span data-ttu-id="9899c-296">**ASIX**: puntatore all'istanza della classe ASIX.</span><span class="sxs-lookup"><span data-stu-id="9899c-296">**asix**: Pointer to the asix class instance.</span></span>
- <span data-ttu-id="9899c-297">**pacchetto: pacchetto** di dati NETX</span><span class="sxs-lookup"><span data-stu-id="9899c-297">**packet**: Netx data packet</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-298">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-298">Return Value</span></span>

- <span data-ttu-id="9899c-299">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-299">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-300">Non è stato possibile richiedere il trasferimento **UX_ERROR**: (0xFF).</span><span class="sxs-lookup"><span data-stu-id="9899c-300">**UX_ERROR**: (0xFF) Transfer could not be requested.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-301">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-301">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_asix_write(asix, packet);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_pima_session_open"></a><span data-ttu-id="9899c-302">ux_host_class_pima_session_open</span><span class="sxs-lookup"><span data-stu-id="9899c-302">ux_host_class_pima_session_open</span></span>

<span data-ttu-id="9899c-303">Apre una sessione tra l'iniziatore e il risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-303">Open a session between Initiator and Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-304">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-304">Prototype</span></span>

```C
UINT ux_host_class_pima_session_open(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session)
```

### <a name="description"></a><span data-ttu-id="9899c-305">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-305">Description</span></span>

<span data-ttu-id="9899c-306">Questa funzione apre una sessione tra un iniziatore PIMA e un risponditore PIMA.</span><span class="sxs-lookup"><span data-stu-id="9899c-306">This function opens a session between a PIMA Initiator and a PIMA Responder.</span></span> <span data-ttu-id="9899c-307">Una volta aperta correttamente una sessione, è possibile eseguire la maggior parte dei comandi PIMA.</span><span class="sxs-lookup"><span data-stu-id="9899c-307">Once a session is successfully opened, most PIMA commands can be executed.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-308">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-308">Parameters</span></span>

- <span data-ttu-id="9899c-309">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-309">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-310">**pima_sessio**: puntatore alla sessione Pima<</span><span class="sxs-lookup"><span data-stu-id="9899c-310">**pima_sessio**: Pointer to PIMA session<</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-311">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-311">Return Value</span></span>

- <span data-ttu-id="9899c-312">**UX_SUCCESS** sessione: (0x00) aperta correttamente</span><span class="sxs-lookup"><span data-stu-id="9899c-312">**UX_SUCCESS**: (0x00) Session successfully opened</span></span>
- <span data-ttu-id="9899c-313">**UX_HOST_CLASS_PIMA_RC_SESSION_ALREADY_OPENED**: (0X201E) sessione già aperta</span><span class="sxs-lookup"><span data-stu-id="9899c-313">**UX_HOST_CLASS_PIMA_RC_SESSION_ALREADY_OPENED**: (0x201E) Session already opened</span></span>

### <a name="example"></a><span data-ttu-id="9899c-314">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-314">Example</span></span>

```C
/* Open a pima session. */

status = ux_host_class_pima_session_open(pima, pima_session);

if (status != UX_SUCCESS)
    return(UX_PICTBRIDGE_ERROR_SESSION_NOT_OPEN);
```

## <a name="ux_host_class_pima_session_close"></a><span data-ttu-id="9899c-315">ux_host_class_pima_session_close</span><span class="sxs-lookup"><span data-stu-id="9899c-315">ux_host_class_pima_session_close</span></span>

<span data-ttu-id="9899c-316">Chiude una sessione tra l'iniziatore e il risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-316">Close a session between Initiator and Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-317">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-317">Prototype</span></span>

```C
UINT ux_host_class_pima_session_close(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session)
```

### <a name="description"></a><span data-ttu-id="9899c-318">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-318">Description</span></span>

<span data-ttu-id="9899c-319">Questa funzione chiude una sessione precedentemente aperta tra un iniziatore PIMA e un risponditore PIMA.</span><span class="sxs-lookup"><span data-stu-id="9899c-319">This function closes a session that was previously opened between a PIMA Initiator and a PIMA Responder.</span></span> <span data-ttu-id="9899c-320">Dopo la chiusura di una sessione, la maggior parte dei comandi PIMA non può più essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="9899c-320">Once a session is closed, most PIMA commands can no longer be executed.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-321">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-321">Parameters</span></span>

- <span data-ttu-id="9899c-322">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-322">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-323">**pima_session**: puntatore alla sessione Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-323">**pima_session**: Pointer to PIMA session.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-324">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-324">Return Value</span></span>

- <span data-ttu-id="9899c-325">**UX_SUCCESS**: (0x00) la sessione è stata chiusa.</span><span class="sxs-lookup"><span data-stu-id="9899c-325">**UX_SUCCESS**: (0x00) The session was closed.</span></span>
- <span data-ttu-id="9899c-326">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: la sessione (0x2003) non è aperta.</span><span class="sxs-lookup"><span data-stu-id="9899c-326">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-327">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-327">Example</span></span>

```C
/* Close the pima session. */

status = ux_host_class_pima_session_close(pima, pima_session);
```

## <a name="ux_host_class_pima_storage_ids_get"></a><span data-ttu-id="9899c-328">ux_host_class_pima_storage_ids_get</span><span class="sxs-lookup"><span data-stu-id="9899c-328">ux_host_class_pima_storage_ids_get</span></span>

<span data-ttu-id="9899c-329">Ottenere la matrice di ID di archiviazione dal risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-329">Obtain the storage ID array from Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-330">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-330">Prototype</span></span>

```C
UINT ux_host_class_pima_storage_ids_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG *storage_ids_array,
    ULONG storage_id_length)
```

### <a name="description"></a><span data-ttu-id="9899c-331">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-331">Description</span></span>

<span data-ttu-id="9899c-332">Questa funzione ottiene la matrice di ID di archiviazione dal risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-332">This function obtains the storage ID array from the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-333">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-333">Parameters</span></span>

- <span data-ttu-id="9899c-334">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-334">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-335">**pima_session**: puntatore alla sessione Pima</span><span class="sxs-lookup"><span data-stu-id="9899c-335">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="9899c-336">**storage_ids_array**: matrice in cui verranno restituiti gli ID di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9899c-336">**storage_ids_array**: Array where storage IDs will be returned</span></span>
- <span data-ttu-id="9899c-337">**storage_id_length**: lunghezza dell'array di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9899c-337">**storage_id_length**: Length of the storage array</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-338">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-338">Return Value</span></span>

- <span data-ttu-id="9899c-339">**UX_SUCCESS**: (0x00) la matrice di ID archiviazione è stata popolata</span><span class="sxs-lookup"><span data-stu-id="9899c-339">**UX_SUCCESS**: (0x00) The storage ID array has been populated</span></span>
- <span data-ttu-id="9899c-340">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta</span><span class="sxs-lookup"><span data-stu-id="9899c-340">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="9899c-341">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-341">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-342">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-342">Example</span></span>

```C
/* Get the number of storage IDs. */
status = ux_host_class_pima_storage_ids_get(pima, pima_session,
    pictbridge ->ux_pictbridge_storage_ids, 64);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pima, pima_session);

    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
}
```

## <a name="ux_host_class_pima_storage_info_get"></a><span data-ttu-id="9899c-343">ux_host_class_pima_storage_info_get</span><span class="sxs-lookup"><span data-stu-id="9899c-343">ux_host_class_pima_storage_info_get</span></span>

<span data-ttu-id="9899c-344">Ottenere le informazioni di archiviazione dal risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-344">Obtain the storage information from Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-345">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-345">Prototype</span></span>

```C
UINT ux_host_class_pima_storage_info_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    UX_HOST_CLASS_PIMA_STORAGE *storage)
```

### <a name="description"></a><span data-ttu-id="9899c-346">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-346">Description</span></span>

<span data-ttu-id="9899c-347">Questa funzione ottiene le informazioni di archiviazione per un contenitore di archiviazione di valore *storage_id*.</span><span class="sxs-lookup"><span data-stu-id="9899c-347">This function obtains the storage information for a storage container of value *storage_id*.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-348">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-348">Parameters</span></span>

- <span data-ttu-id="9899c-349">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-349">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-350">**pima_session**: puntatore alla sessione Pima</span><span class="sxs-lookup"><span data-stu-id="9899c-350">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="9899c-351">**storage_id**: ID del contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9899c-351">**storage_id**: ID of the storage container</span></span>
- <span data-ttu-id="9899c-352">**archiviazione**: puntatore al contenitore di informazioni di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9899c-352">**storage**: Pointer to storage information container</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-353">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-353">Return Value</span></span>

- <span data-ttu-id="9899c-354">**UX_SUCCESS**: (0x00) sono state recuperate le informazioni di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9899c-354">**UX_SUCCESS**: (0x00) The storage information was retrieved</span></span>
- <span data-ttu-id="9899c-355">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta</span><span class="sxs-lookup"><span data-stu-id="9899c-355">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="9899c-356">**UX_MEMORY_INSUFFICIENT** (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-356">**UX_MEMORY_INSUFFICIENT** (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-357">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-357">Example</span></span>

```C
/* Get the first storage ID info container. */
status = ux_host_class_pima_storage_info_get(pima, pima_session,
    pictbridge ->ux_pictbridge_storage_ids[0],
    (UX_HOST_CLASS_PIMA_STORAGE *)pictbridge ->ux_pictbridge_storage);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pictbridge ->
        ux_pictbridge_pima, pima_session);
    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
}
```

## <a name="ux_host_class_pima_num_objects_get"></a><span data-ttu-id="9899c-358">ux_host_class_pima_num_objects_get</span><span class="sxs-lookup"><span data-stu-id="9899c-358">ux_host_class_pima_num_objects_get</span></span>

<span data-ttu-id="9899c-359">Ottenere il numero di oggetti in un contenitore di archiviazione dal risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-359">Obtain the number of objects on a storage container from Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-360">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-360">Prototype</span></span>

```C
UINT ux_host_class_pima_num_objects_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    ULONG object_format_code)
```

### <a name="description"></a><span data-ttu-id="9899c-361">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-361">Description</span></span>

<span data-ttu-id="9899c-362">Questa funzione ottiene il numero di oggetti archiviati in un contenitore di archiviazione specifico di value storage_id corrispondente a un codice di formato specifico.</span><span class="sxs-lookup"><span data-stu-id="9899c-362">This function obtains the number of objects stored on a specific storage container of value storage_id matching a specific format code.</span></span> <span data-ttu-id="9899c-363">Il numero di oggetti viene restituito nel campo: ux_host_class_pima_session_nb_objects della struttura di pima_session.</span><span class="sxs-lookup"><span data-stu-id="9899c-363">The number of objects is returned in the field: ux_host_class_pima_session_nb_objects of the pima_session structure.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-364">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-364">Parameters</span></span>

- <span data-ttu-id="9899c-365">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-365">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-366">**pima_session**: puntatore alla sessione Pima</span><span class="sxs-lookup"><span data-stu-id="9899c-366">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="9899c-367">**storage_id**: ID del contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9899c-367">**storage_id**: ID of the storage container</span></span>
- <span data-ttu-id="9899c-368">**object_format_code**: filtro del codice del formato degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="9899c-368">**object_format_code**: Objects format code filter.</span></span>

<span data-ttu-id="9899c-369">I codici di formato dell'oggetto possono avere uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="9899c-369">The Object Format Codes can have one of the following values.</span></span>

| <span data-ttu-id="9899c-370">Codice del formato dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-370">Object Format Code</span></span>               | <span data-ttu-id="9899c-371">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-371">Description</span></span>   |     <span data-ttu-id="9899c-372">Codice USBX</span><span class="sxs-lookup"><span data-stu-id="9899c-372">USBX code</span></span>                          |
|----------------------------------|---------------|------------------------------------------|
| <span data-ttu-id="9899c-373">0x3000</span><span class="sxs-lookup"><span data-stu-id="9899c-373">0x3000</span></span>                           | <span data-ttu-id="9899c-374">Oggetto non definito non definito</span><span class="sxs-lookup"><span data-stu-id="9899c-374">Undefined Undefined non-image object</span></span> | <span data-ttu-id="9899c-375">UX_HOST_CLASS_PIMA_OFC_UNDEFINED</span><span class="sxs-lookup"><span data-stu-id="9899c-375">UX_HOST_CLASS_PIMA_OFC_UNDEFINED</span></span>   |
| <span data-ttu-id="9899c-376">0x3001</span><span class="sxs-lookup"><span data-stu-id="9899c-376">0x3001</span></span>                           | <span data-ttu-id="9899c-377">Associazione di associazione (ad esempio, cartella)</span><span class="sxs-lookup"><span data-stu-id="9899c-377">Association Association (e.g. folder)</span></span> | <span data-ttu-id="9899c-378">UX_HOST_CLASS_PIMA_OFC_ASSOCIATION</span><span class="sxs-lookup"><span data-stu-id="9899c-378">UX_HOST_CLASS_PIMA_OFC_ASSOCIATION</span></span> |
| <span data-ttu-id="9899c-379">0x3002</span><span class="sxs-lookup"><span data-stu-id="9899c-379">0x3002</span></span>                           | <span data-ttu-id="9899c-380">Script del dispositivo-script specifico del modello</span><span class="sxs-lookup"><span data-stu-id="9899c-380">Script Device-model specific script</span></span> | <span data-ttu-id="9899c-381">UX_HOST_CLASS_PIMA_OFC_SCRIPT</span><span class="sxs-lookup"><span data-stu-id="9899c-381">UX_HOST_CLASS_PIMA_OFC_SCRIPT</span></span>      |
| <span data-ttu-id="9899c-382">0x3003</span><span class="sxs-lookup"><span data-stu-id="9899c-382">0x3003</span></span>                           | <span data-ttu-id="9899c-383">Eseguibile binario specifico del modello di dispositivo eseguibile</span><span class="sxs-lookup"><span data-stu-id="9899c-383">Executable Device model-specific binary executable</span></span> | <span data-ttu-id="9899c-384">UX_HOST_CLASS_PIMA_OFC_EXECUTABLE</span><span class="sxs-lookup"><span data-stu-id="9899c-384">UX_HOST_CLASS_PIMA_OFC_EXECUTABLE</span></span>  |
| <span data-ttu-id="9899c-385">0x3004</span><span class="sxs-lookup"><span data-stu-id="9899c-385">0x3004</span></span>                           | <span data-ttu-id="9899c-386">File di testo di testo</span><span class="sxs-lookup"><span data-stu-id="9899c-386">Text Text file</span></span>  |   <span data-ttu-id="9899c-387">UX_HOST_CLASS_PIMA_OFC_TEXT</span><span class="sxs-lookup"><span data-stu-id="9899c-387">UX_HOST_CLASS_PIMA_OFC_TEXT</span></span>        |
| <span data-ttu-id="9899c-388">0x3005</span><span class="sxs-lookup"><span data-stu-id="9899c-388">0x3005</span></span>                           | <span data-ttu-id="9899c-389">File HTML HyperText Markup Language (testo)</span><span class="sxs-lookup"><span data-stu-id="9899c-389">HTML HyperText Markup Language file (text)</span></span> | <span data-ttu-id="9899c-390">UX_HOST_CLASS_PIMA_OFC_HTML</span><span class="sxs-lookup"><span data-stu-id="9899c-390">UX_HOST_CLASS_PIMA_OFC_HTML</span></span>        |
| <span data-ttu-id="9899c-391">0x3006</span><span class="sxs-lookup"><span data-stu-id="9899c-391">0x3006</span></span>                           | <span data-ttu-id="9899c-392">File di formato dell'ordine di stampa digitale DPOF (testo)</span><span class="sxs-lookup"><span data-stu-id="9899c-392">DPOF Digital Print Order Format file (text)</span></span> | <span data-ttu-id="9899c-393">UX_HOST_CLASS_PIMA_OFC_DPOF</span><span class="sxs-lookup"><span data-stu-id="9899c-393">UX_HOST_CLASS_PIMA_OFC_DPOF</span></span>        |
| <span data-ttu-id="9899c-394">0x3007</span><span class="sxs-lookup"><span data-stu-id="9899c-394">0x3007</span></span>                           | <span data-ttu-id="9899c-395">Clip audio AIFF</span><span class="sxs-lookup"><span data-stu-id="9899c-395">AIFF Audio clip</span></span>  |  <span data-ttu-id="9899c-396">UX_HOST_CLASS_PIMA_OFC_AIFF</span><span class="sxs-lookup"><span data-stu-id="9899c-396">UX_HOST_CLASS_PIMA_OFC_AIFF</span></span>        |
| <span data-ttu-id="9899c-397">0x3008</span><span class="sxs-lookup"><span data-stu-id="9899c-397">0x3008</span></span>                           | <span data-ttu-id="9899c-398">Clip audio WAV</span><span class="sxs-lookup"><span data-stu-id="9899c-398">WAV Audio clip</span></span>   |  <span data-ttu-id="9899c-399">UX_HOST_CLASS_PIMA_OFC_WAV</span><span class="sxs-lookup"><span data-stu-id="9899c-399">UX_HOST_CLASS_PIMA_OFC_WAV</span></span>         |
| <span data-ttu-id="9899c-400">0x3009</span><span class="sxs-lookup"><span data-stu-id="9899c-400">0x3009</span></span>                           | <span data-ttu-id="9899c-401">Clip audio MP3</span><span class="sxs-lookup"><span data-stu-id="9899c-401">MP3 Audio clip</span></span>   |  <span data-ttu-id="9899c-402">UX_HOST_CLASS_PIMA_OFC_MP3</span><span class="sxs-lookup"><span data-stu-id="9899c-402">UX_HOST_CLASS_PIMA_OFC_MP3</span></span>         |
| <span data-ttu-id="9899c-403">0x300A</span><span class="sxs-lookup"><span data-stu-id="9899c-403">0x300A</span></span>                           | <span data-ttu-id="9899c-404">Clip video AVI</span><span class="sxs-lookup"><span data-stu-id="9899c-404">AVI Video clip</span></span>   |  <span data-ttu-id="9899c-405">UX_HOST_CLASS_PIMA_OFC_AVI</span><span class="sxs-lookup"><span data-stu-id="9899c-405">UX_HOST_CLASS_PIMA_OFC_AVI</span></span>         |
| <span data-ttu-id="9899c-406">0x300B</span><span class="sxs-lookup"><span data-stu-id="9899c-406">0x300B</span></span>                           | <span data-ttu-id="9899c-407">Clip video MPEG</span><span class="sxs-lookup"><span data-stu-id="9899c-407">MPEG Video clip</span></span>  |  <span data-ttu-id="9899c-408">UX_HOST_CLASS_PIMA_OFC_MPEG</span><span class="sxs-lookup"><span data-stu-id="9899c-408">UX_HOST_CLASS_PIMA_OFC_MPEG</span></span>        |
| <span data-ttu-id="9899c-409">0x300C</span><span class="sxs-lookup"><span data-stu-id="9899c-409">0x300C</span></span>                           | <span data-ttu-id="9899c-410">Formato ASF Microsoft Advanced Streaming (video)</span><span class="sxs-lookup"><span data-stu-id="9899c-410">ASF Microsoft Advanced Streaming Format (video)</span></span> | <span data-ttu-id="9899c-411">UX_HOST_CLASS_PIMA_OFC_ASF</span><span class="sxs-lookup"><span data-stu-id="9899c-411">UX_HOST_CLASS_PIMA_OFC_ASF</span></span>         |
| <span data-ttu-id="9899c-412">0x3800</span><span class="sxs-lookup"><span data-stu-id="9899c-412">0x3800</span></span>                           | <span data-ttu-id="9899c-413">Oggetto immagine sconosciuto non definito</span><span class="sxs-lookup"><span data-stu-id="9899c-413">Undefined Unknown image object</span></span> | <span data-ttu-id="9899c-414">UX_HOST_CLASS_PIMA_OFC_QT</span><span class="sxs-lookup"><span data-stu-id="9899c-414">UX_HOST_CLASS_PIMA_OFC_QT</span></span>          |
| <span data-ttu-id="9899c-415">0x3801</span><span class="sxs-lookup"><span data-stu-id="9899c-415">0x3801</span></span>                           | <span data-ttu-id="9899c-416">Formato di file con scambio di formato EXIF/JPEG, JEIDA standard</span><span class="sxs-lookup"><span data-stu-id="9899c-416">EXIF/JPEG Exchangeable File Format, JEIDA standard</span></span> | <span data-ttu-id="9899c-417">UX_HOST_CLASS_PIMA_OFC_EXIF_JPEG</span><span class="sxs-lookup"><span data-stu-id="9899c-417">UX_HOST_CLASS_PIMA_OFC_EXIF_JPEG</span></span>   |
| <span data-ttu-id="9899c-418">0x3802</span><span class="sxs-lookup"><span data-stu-id="9899c-418">0x3802</span></span>                           | <span data-ttu-id="9899c-419">Formato file di immagine Tag TIFF/EP per la fotografia elettronica</span><span class="sxs-lookup"><span data-stu-id="9899c-419">TIFF/EP Tag Image File Format for Electronic Photography</span></span> | <span data-ttu-id="9899c-420">UX_HOST_CLASS_PIMA_OFC_TIFF_EP</span><span class="sxs-lookup"><span data-stu-id="9899c-420">UX_HOST_CLASS_PIMA_OFC_TIFF_EP</span></span>     |
| <span data-ttu-id="9899c-421">0x3803</span><span class="sxs-lookup"><span data-stu-id="9899c-421">0x3803</span></span>                           | <span data-ttu-id="9899c-422">Formato dell'immagine di archiviazione strutturata FlashPix</span><span class="sxs-lookup"><span data-stu-id="9899c-422">FlashPix Structured Storage Image Format</span></span> | <span data-ttu-id="9899c-423">UX_HOST_CLASS_PIMA_OFC_FLASHPIX</span><span class="sxs-lookup"><span data-stu-id="9899c-423">UX_HOST_CLASS_PIMA_OFC_FLASHPIX</span></span>    |
| <span data-ttu-id="9899c-424">0x3804</span><span class="sxs-lookup"><span data-stu-id="9899c-424">0x3804</span></span>                           | <span data-ttu-id="9899c-425">File bitmap Microsoft Windows BMP</span><span class="sxs-lookup"><span data-stu-id="9899c-425">BMP Microsoft Windows Bitmap file</span></span> | <span data-ttu-id="9899c-426">UX_HOST_CLASS_PIMA_OFC_BMP</span><span class="sxs-lookup"><span data-stu-id="9899c-426">UX_HOST_CLASS_PIMA_OFC_BMP</span></span>         |
| <span data-ttu-id="9899c-427">0x3805</span><span class="sxs-lookup"><span data-stu-id="9899c-427">0x3805</span></span>                           | <span data-ttu-id="9899c-428">Formato file di immagine della fotocamera Canon CIFF</span><span class="sxs-lookup"><span data-stu-id="9899c-428">CIFF Canon Camera Image File Format</span></span> | <span data-ttu-id="9899c-429">UX_HOST_CLASS_PIMA_OFC_CIFF</span><span class="sxs-lookup"><span data-stu-id="9899c-429">UX_HOST_CLASS_PIMA_OFC_CIFF</span></span>        |
| <span data-ttu-id="9899c-430">0x3806</span><span class="sxs-lookup"><span data-stu-id="9899c-430">0x3806</span></span>                           | <span data-ttu-id="9899c-431">Riservato non definito</span><span class="sxs-lookup"><span data-stu-id="9899c-431">Undefined Reserved</span></span> |  |
| <span data-ttu-id="9899c-432">0x3807</span><span class="sxs-lookup"><span data-stu-id="9899c-432">0x3807</span></span>                           | <span data-ttu-id="9899c-433">Graphics Interchange Format GIF</span><span class="sxs-lookup"><span data-stu-id="9899c-433">GIF Graphics Interchange Format</span></span> | <span data-ttu-id="9899c-434">UX_HOST_CLASS_PIMA_OFC_GIF</span><span class="sxs-lookup"><span data-stu-id="9899c-434">UX_HOST_CLASS_PIMA_OFC_GIF</span></span>         |
| <span data-ttu-id="9899c-435">0x3808</span><span class="sxs-lookup"><span data-stu-id="9899c-435">0x3808</span></span>                           | <span data-ttu-id="9899c-436">Formato di interscambio file JPEG JFIF</span><span class="sxs-lookup"><span data-stu-id="9899c-436">JFIF JPEG File Interchange Format</span></span> | <span data-ttu-id="9899c-437">UX_HOST_CLASS_PIMA_OFC_JFIF</span><span class="sxs-lookup"><span data-stu-id="9899c-437">UX_HOST_CLASS_PIMA_OFC_JFIF</span></span>        |
| <span data-ttu-id="9899c-438">0x3809</span><span class="sxs-lookup"><span data-stu-id="9899c-438">0x3809</span></span>                           | <span data-ttu-id="9899c-439">Immagine PAC PhotoCD PCD</span><span class="sxs-lookup"><span data-stu-id="9899c-439">PCD PhotoCD Image Pac</span></span> | <span data-ttu-id="9899c-440">UX_HOST_CLASS_PIMA_OFC_PCD</span><span class="sxs-lookup"><span data-stu-id="9899c-440">UX_HOST_CLASS_PIMA_OFC_PCD</span></span>         |
| <span data-ttu-id="9899c-441">0x380A</span><span class="sxs-lookup"><span data-stu-id="9899c-441">0x380A</span></span>                           | <span data-ttu-id="9899c-442">Formato immagine rinvio PICT</span><span class="sxs-lookup"><span data-stu-id="9899c-442">PICT Quickdraw Image Format</span></span> | <span data-ttu-id="9899c-443">UX_HOST_CLASS_PIMA_OFC_PICT</span><span class="sxs-lookup"><span data-stu-id="9899c-443">UX_HOST_CLASS_PIMA_OFC_PICT</span></span>        |
| <span data-ttu-id="9899c-444">0x380B</span><span class="sxs-lookup"><span data-stu-id="9899c-444">0x380B</span></span>                           | <span data-ttu-id="9899c-445">Portable Network Graphics PNG</span><span class="sxs-lookup"><span data-stu-id="9899c-445">PNG Portable Network Graphics</span></span> | <span data-ttu-id="9899c-446">UX_HOST_CLASS_PIMA_OFC_PNG</span><span class="sxs-lookup"><span data-stu-id="9899c-446">UX_HOST_CLASS_PIMA_OFC_PNG</span></span>         |
| <span data-ttu-id="9899c-447">0x380C</span><span class="sxs-lookup"><span data-stu-id="9899c-447">0x380C</span></span>                           | <span data-ttu-id="9899c-448">Riservato non definito</span><span class="sxs-lookup"><span data-stu-id="9899c-448">Undefined Reserved</span></span> |   |
| <span data-ttu-id="9899c-449">0x380D</span><span class="sxs-lookup"><span data-stu-id="9899c-449">0x380D</span></span>                           | <span data-ttu-id="9899c-450">Formato file immagine Tag TIFF</span><span class="sxs-lookup"><span data-stu-id="9899c-450">TIFF Tag Image File Format</span></span> | <span data-ttu-id="9899c-451">UX_HOST_CLASS_PIMA_OFC_TIFF</span><span class="sxs-lookup"><span data-stu-id="9899c-451">UX_HOST_CLASS_PIMA_OFC_TIFF</span></span>        |
| <span data-ttu-id="9899c-452">0x380E</span><span class="sxs-lookup"><span data-stu-id="9899c-452">0x380E</span></span>                           | <span data-ttu-id="9899c-453">Formato file di immagine Tag TIFF/IT per Information Technology (Graphic Arts)</span><span class="sxs-lookup"><span data-stu-id="9899c-453">TIFF/IT Tag Image File Format for Information Technology (graphic arts)</span></span> | <span data-ttu-id="9899c-454">UX_HOST_CLASS_PIMA_OFC_TIFF_IT</span><span class="sxs-lookup"><span data-stu-id="9899c-454">UX_HOST_CLASS_PIMA_OFC_TIFF_IT</span></span>     |
| <span data-ttu-id="9899c-455">0x380F</span><span class="sxs-lookup"><span data-stu-id="9899c-455">0x380F</span></span>                           | <span data-ttu-id="9899c-456">Formato file baseline JPEG2000 JP2</span><span class="sxs-lookup"><span data-stu-id="9899c-456">JP2 JPEG2000 Baseline File Format</span></span> | <span data-ttu-id="9899c-457">UX_HOST_CLASS_PIMA_OFC_JP2</span><span class="sxs-lookup"><span data-stu-id="9899c-457">UX_HOST_CLASS_PIMA_OFC_JP2</span></span>         |
| <span data-ttu-id="9899c-458">0x3810</span><span class="sxs-lookup"><span data-stu-id="9899c-458">0x3810</span></span>                           | <span data-ttu-id="9899c-459">Formato file esteso JPX JPEG2000</span><span class="sxs-lookup"><span data-stu-id="9899c-459">JPX JPEG2000 Extended File Format</span></span> | <span data-ttu-id="9899c-460">UX_HOST_CLASS_PIMA_OFC_JPX</span><span class="sxs-lookup"><span data-stu-id="9899c-460">UX_HOST_CLASS_PIMA_OFC_JPX</span></span>         |
| <span data-ttu-id="9899c-461">Tutti gli altri codici con MSN di 0011</span><span class="sxs-lookup"><span data-stu-id="9899c-461">All other codes with MSN of 0011</span></span> | <span data-ttu-id="9899c-462">Qualsiasi riservato non definito per usi futuri</span><span class="sxs-lookup"><span data-stu-id="9899c-462">Any Undefined Reserved for future use</span></span> |                                    |
| <span data-ttu-id="9899c-463">Tutti gli altri codici con MSN di 1011</span><span class="sxs-lookup"><span data-stu-id="9899c-463">All other codes with MSN of 1011</span></span> | <span data-ttu-id="9899c-464">Qualsiasi tipo definito dal fornitore definito dal fornitore: immagine</span><span class="sxs-lookup"><span data-stu-id="9899c-464">Any Vendor-Defined Vendor-Defined type: Image</span></span> |                                    |

### <a name="return-value"></a><span data-ttu-id="9899c-465">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-465">Return Value</span></span>

- <span data-ttu-id="9899c-466">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-466">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-467">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta</span><span class="sxs-lookup"><span data-stu-id="9899c-467">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="9899c-468">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-468">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-469">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-469">Example</span></span>

```C
/* Get the number of objects on all containers matching a SCRIPT object. */
status = ux_host_class_pima_num_objects_get(pima, pima_session,
    UX_PICTBRIDGE_ALL_CONTAINERS, UX_PICTBRIDGE_OBJECT_SCRIPT);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_**host_class_pima_session_close(pima, pima_session);

    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
} else
    /* The number of objects is returned in the field: pima_session -> ux_host_class_pima_session_nb_objects */
```

## <a name="ux_host_class_pima_object_handles_get"></a><span data-ttu-id="9899c-470">ux_host_class_pima_object_handles_get</span><span class="sxs-lookup"><span data-stu-id="9899c-470">ux_host_class_pima_object_handles_get</span></span>

<span data-ttu-id="9899c-471">Ottenere handle di oggetto dal risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-471">Obtain object handles from Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-472">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-472">Prototype</span></span>

```C
UINT ux_host_class_pima_object_handles_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG *object_handles_array,
    ULONG object_handles_length,
    ULONG storage_id,
    ULONG object_format_code,
    ULONG object_handle_association)
```

### <a name="description"></a><span data-ttu-id="9899c-473">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-473">Description</span></span>

<span data-ttu-id="9899c-474">Restituisce una matrice di handle di oggetto presenti nel contenitore di archiviazione indicato dal parametro storage_id.</span><span class="sxs-lookup"><span data-stu-id="9899c-474">Returns an array of Object Handles present in the storage container indicated by the storage_id parameter.</span></span> <span data-ttu-id="9899c-475">Se si desidera un elenco aggregato in tutti i punti vendita, questo valore deve essere impostato su 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="9899c-475">If an aggregated list across all stores is desired, this value shall be set to 0xFFFFFFFF.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-476">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-476">Parameters</span></span>

- <span data-ttu-id="9899c-477">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-477">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-478">**pima_session**: puntatore alla sessione Pima</span><span class="sxs-lookup"><span data-stu-id="9899c-478">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="9899c-479">**object_handes_array**: matrice in cui vengono restituiti gli handle</span><span class="sxs-lookup"><span data-stu-id="9899c-479">**object_handes_array**: Array where handles are returned</span></span>
- <span data-ttu-id="9899c-480">**object_handles_length**: lunghezza della matrice</span><span class="sxs-lookup"><span data-stu-id="9899c-480">**object_handles_length**: Length of the array</span></span>
- <span data-ttu-id="9899c-481">**storage_id**: ID del contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9899c-481">**storage_id**: ID of the storage container</span></span>
- <span data-ttu-id="9899c-482">**object_format_code**: formattare il codice per l'oggetto (vedere la tabella per la funzione ux_host_class_pima_num_objects_get)</span><span class="sxs-lookup"><span data-stu-id="9899c-482">**object_format_code**: Format code for object (see table for function ux_host_class_pima_num_objects_get)</span></span>
- <span data-ttu-id="9899c-483">**object_handle_association**: valore facoltativo dell'associazione di oggetti</span><span class="sxs-lookup"><span data-stu-id="9899c-483">**object_handle_association**: Optional object association value</span></span>

<span data-ttu-id="9899c-484">L'associazione dell'handle di oggetto può essere uno dei valori della tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="9899c-484">The object handle association can be one of the value from the table below:</span></span>

| <span data-ttu-id="9899c-485">AssociationCode</span><span class="sxs-lookup"><span data-stu-id="9899c-485">AssociationCode</span></span>                        | <span data-ttu-id="9899c-486">AssociationType</span><span class="sxs-lookup"><span data-stu-id="9899c-486">AssociationType</span></span>      | <span data-ttu-id="9899c-487">Interpretazione</span><span class="sxs-lookup"><span data-stu-id="9899c-487">Interpretation</span></span>       |
|----------------------------------------|----------------------|----------------------|
| <span data-ttu-id="9899c-488">0x0000</span><span class="sxs-lookup"><span data-stu-id="9899c-488">0x0000</span></span>                                 | <span data-ttu-id="9899c-489">Non definito</span><span class="sxs-lookup"><span data-stu-id="9899c-489">Undefined</span></span>            | <span data-ttu-id="9899c-490">Non definito</span><span class="sxs-lookup"><span data-stu-id="9899c-490">Undefined</span></span>            |
| <span data-ttu-id="9899c-491">0x0001</span><span class="sxs-lookup"><span data-stu-id="9899c-491">0x0001</span></span>                                 | <span data-ttu-id="9899c-492">GenericFolder</span><span class="sxs-lookup"><span data-stu-id="9899c-492">GenericFolder</span></span>        | <span data-ttu-id="9899c-493">Non utilizzato</span><span class="sxs-lookup"><span data-stu-id="9899c-493">Unused</span></span>               |
| <span data-ttu-id="9899c-494">0x0002</span><span class="sxs-lookup"><span data-stu-id="9899c-494">0x0002</span></span>                                 | <span data-ttu-id="9899c-495">Album</span><span class="sxs-lookup"><span data-stu-id="9899c-495">Album</span></span>                | <span data-ttu-id="9899c-496">Riservato</span><span class="sxs-lookup"><span data-stu-id="9899c-496">Reserved</span></span>             |
| <span data-ttu-id="9899c-497">0x0003</span><span class="sxs-lookup"><span data-stu-id="9899c-497">0x0003</span></span>                                 | <span data-ttu-id="9899c-498">TimeSequence</span><span class="sxs-lookup"><span data-stu-id="9899c-498">TimeSequence</span></span>         | <span data-ttu-id="9899c-499">DefaultPlaybackDelta</span><span class="sxs-lookup"><span data-stu-id="9899c-499">DefaultPlaybackDelta</span></span> |
| <span data-ttu-id="9899c-500">0x0004</span><span class="sxs-lookup"><span data-stu-id="9899c-500">0x0004</span></span>                                 | <span data-ttu-id="9899c-501">HorizontalPanoramic</span><span class="sxs-lookup"><span data-stu-id="9899c-501">HorizontalPanoramic</span></span>  | <span data-ttu-id="9899c-502">Non utilizzato</span><span class="sxs-lookup"><span data-stu-id="9899c-502">Unused</span></span>               |
| <span data-ttu-id="9899c-503">0x0005</span><span class="sxs-lookup"><span data-stu-id="9899c-503">0x0005</span></span>                                 | <span data-ttu-id="9899c-504">VerticalPanoramic</span><span class="sxs-lookup"><span data-stu-id="9899c-504">VerticalPanoramic</span></span>    | <span data-ttu-id="9899c-505">Non utilizzato</span><span class="sxs-lookup"><span data-stu-id="9899c-505">Unused</span></span>               |
| <span data-ttu-id="9899c-506">0x0006</span><span class="sxs-lookup"><span data-stu-id="9899c-506">0x0006</span></span>                                 | <span data-ttu-id="9899c-507">2DPanoramic</span><span class="sxs-lookup"><span data-stu-id="9899c-507">2DPanoramic</span></span>          | <span data-ttu-id="9899c-508">ImagesPerRow</span><span class="sxs-lookup"><span data-stu-id="9899c-508">ImagesPerRow</span></span>         |
| <span data-ttu-id="9899c-509">0x0007</span><span class="sxs-lookup"><span data-stu-id="9899c-509">0x0007</span></span>                                 | <span data-ttu-id="9899c-510">AncillaryData</span><span class="sxs-lookup"><span data-stu-id="9899c-510">AncillaryData</span></span>        | <span data-ttu-id="9899c-511">Non definito</span><span class="sxs-lookup"><span data-stu-id="9899c-511">Undefined</span></span>            |
| <span data-ttu-id="9899c-512">Tutti gli altri valori con bit 15 impostati su 0</span><span class="sxs-lookup"><span data-stu-id="9899c-512">All other values with bit 15 set to 0</span></span>  | <span data-ttu-id="9899c-513">Riservato</span><span class="sxs-lookup"><span data-stu-id="9899c-513">Reserved</span></span>             | <span data-ttu-id="9899c-514">Non definito</span><span class="sxs-lookup"><span data-stu-id="9899c-514">Undefined</span></span>            |
| <span data-ttu-id="9899c-515">Tutti i valori con bit 15 impostati su 1</span><span class="sxs-lookup"><span data-stu-id="9899c-515">All values with bit 15 set to 1</span></span>        | <span data-ttu-id="9899c-516">Definito dal fornitore</span><span class="sxs-lookup"><span data-stu-id="9899c-516">Vendor-Defined</span></span>       | <span data-ttu-id="9899c-517">Definito dal fornitore</span><span class="sxs-lookup"><span data-stu-id="9899c-517">Vendor-Defined</span></span>       |

### <a name="return-value"></a><span data-ttu-id="9899c-518">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-518">Return Value</span></span>

- <span data-ttu-id="9899c-519">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-519">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-520">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta</span><span class="sxs-lookup"><span data-stu-id="9899c-520">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="9899c-521">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-521">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-522">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-522">Example</span></span>

```C
/* Get the array of objects handles on the container. */
status = ux_**host_class_pima_object_handles_get(pima, pima_session,
    pictbridge ->ux_pictbridge_object_handles_array,
    4 * pima_session ->ux_host_class_pima_session_nb_objects,
    UX_PICTBRIDGE_ALL_CONTAINERS,
    UX_PICTBRIDGE_OBJECT_SCRIPT, 0);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pima, pima_session);
    return(UX_PICTBRIDGE_ERROR_STORE_NOT_AVAILABLE);
}
```

## <a name="ux_host_class_pima_object_info_get"></a><span data-ttu-id="9899c-523">ux_host_class_pima_object_info_get</span><span class="sxs-lookup"><span data-stu-id="9899c-523">ux_host_class_pima_object_info_get</span></span>

<span data-ttu-id="9899c-524">Ottenere le informazioni sull'oggetto dal risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-524">Obtain the object information from Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-525">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-525">Prototype</span></span>

```C
UINT ux_host_class_pima_object_info_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a><span data-ttu-id="9899c-526">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-526">Description</span></span>

<span data-ttu-id="9899c-527">Questa funzione ottiene le informazioni sull'oggetto per un handle di oggetto.</span><span class="sxs-lookup"><span data-stu-id="9899c-527">This function obtains the object information for an object handle.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-528">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-528">Parameters</span></span>

- <span data-ttu-id="9899c-529">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-529">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-530">**pima_session**: puntatore alla sessione Pima</span><span class="sxs-lookup"><span data-stu-id="9899c-530">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="9899c-531">**object_handle**: handle dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-531">**object_handle**: Handle of the object</span></span>
- <span data-ttu-id="9899c-532">**oggetto**: puntatore al contenitore di informazioni sugli oggetti</span><span class="sxs-lookup"><span data-stu-id="9899c-532">**object**: Pointer to object information container</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-533">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-533">Return Value</span></span>

- <span data-ttu-id="9899c-534">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-534">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-535">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta</span><span class="sxs-lookup"><span data-stu-id="9899c-535">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="9899c-536">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-536">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-537">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-537">Example</span></span>

```C
/* We search for an object that is a picture or a script. */
object_index = 0;

while (object_index < pima_session -> ux_host_class_pima_session_nb_objects)
{
    /* Get the object info structure. */
    status = ux_**host_class_pima_object_info_get(pima, pima_session,
        pictbridge -> ux_pictbridge_object_handles_array[object_index], 
        pima_object);

    if (status != UX_SUCCESS)
    {
        /* Close the pima session. */
        status = ux_host_class_pima_session_close(pima, pima_session);

        return(UX_PICTBRIDGE_ERROR_INVALID_OBJECT_HANDLE );
    }
}
```

## <a name="ux_host_class_pima_object_info_send"></a><span data-ttu-id="9899c-538">ux_host_class_pima_object_info_send</span><span class="sxs-lookup"><span data-stu-id="9899c-538">ux_host_class_pima_object_info_send</span></span>

<span data-ttu-id="9899c-539">Invia le informazioni sull'oggetto al risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-539">Send the object information to Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-540">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-540">Prototype</span></span>

```C
UINT ux_host_class_pima_object_info_send(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG storage_id,
    ULONG parent_object_id,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a><span data-ttu-id="9899c-541">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-541">Description</span></span>

<span data-ttu-id="9899c-542">Questa funzione Invia le informazioni di archiviazione per un contenitore di archiviazione di valore storage_id.</span><span class="sxs-lookup"><span data-stu-id="9899c-542">This function sends the storage information for a storage container of value storage_id.</span></span> <span data-ttu-id="9899c-543">L'initiator deve usare questo comando prima di inviare un oggetto al risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-543">The Initiator should use this command before sending an object to the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-544">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-544">Parameters</span></span>

- <span data-ttu-id="9899c-545">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-545">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-546">**pima_session**: puntatore alla sessione Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-546">**pima_session**: Pointer to PIMA session.</span></span>
- <span data-ttu-id="9899c-547">**storage_id**: ID archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9899c-547">**storage_id**: Destination storage ID.</span></span>
- <span data-ttu-id="9899c-548">**parent_object_id**: ObjectHandle padre sul risponditore in cui deve essere inserito l'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9899c-548">**parent_object_id**: Parent ObjectHandle on Responder where object should be placed.</span></span>
- <span data-ttu-id="9899c-549">**oggetto**: puntatore al contenitore di informazioni sugli oggetti.</span><span class="sxs-lookup"><span data-stu-id="9899c-549">**object**: Pointer to object information container.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-550">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-550">Return Value</span></span>

- <span data-ttu-id="9899c-551">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-551">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-552">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta</span><span class="sxs-lookup"><span data-stu-id="9899c-552">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="9899c-553">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-553">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-554">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-554">Example</span></span>

```C
/* Send a script info. */
status = ux_host_class_pima_object_info_send(pima, pima_session,
    0, 0, pima_object);

if (status != UX_SUCCESS)
{
    /* Close the pima session. */
    status = ux_host_class_pima_session_close(pima, pima_session);

    return(UX_ERROR);
}
```

## <a name="ux_host_class_pima_object_open"></a><span data-ttu-id="9899c-555">ux_host_class_pima_object_open</span><span class="sxs-lookup"><span data-stu-id="9899c-555">ux_host_class_pima_object_open</span></span>

<span data-ttu-id="9899c-556">Apre un oggetto archiviato nel risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-556">Open an object stored in the Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-557">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-557">Prototype</span></span>

```C
UINT ux_host_class_pima_object_open(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a><span data-ttu-id="9899c-558">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-558">Description</span></span>

<span data-ttu-id="9899c-559">Questa funzione apre un oggetto nel risponditore prima della lettura o della scrittura.</span><span class="sxs-lookup"><span data-stu-id="9899c-559">This function opens an object on the responder before reading or writing.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-560">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-560">Parameters</span></span>

- <span data-ttu-id="9899c-561">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-561">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-562">**pima_session**: puntatore alla sessione Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-562">**pima_session**: Pointer to PIMA session.</span></span>
- <span data-ttu-id="9899c-563">**object_handle**: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9899c-563">**object_handle**: handle of the object.</span></span>
- <span data-ttu-id="9899c-564">**oggetto**: puntatore al contenitore di informazioni sugli oggetti.</span><span class="sxs-lookup"><span data-stu-id="9899c-564">**objec**: Pointer to object information container.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-565">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-565">Return Value</span></span>

- <span data-ttu-id="9899c-566">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-566">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-567">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta</span><span class="sxs-lookup"><span data-stu-id="9899c-567">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="9899c-568">**UX_HOST_CLASS_PIMA_RC_OBJECT_ALREADY_OPENED**: l'oggetto (0x2021) è già aperto.</span><span class="sxs-lookup"><span data-stu-id="9899c-568">**UX_HOST_CLASS_PIMA_RC_OBJECT_ALREADY_OPENED**: (0x2021) Object already opened.</span></span>
- <span data-ttu-id="9899c-569">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-569">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-570">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-570">Example</span></span>

```C
/* Open the object. */

status = ux_host_class_pima_object_open(pima, pima_session,
    object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);
```

## <a name="ux_host_class_pima_object_get"></a><span data-ttu-id="9899c-571">ux_host_class_pima_object_get</span><span class="sxs-lookup"><span data-stu-id="9899c-571">ux_host_class_pima_object_get</span></span>

<span data-ttu-id="9899c-572">Ottiene un oggetto archiviato nel risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-572">Get an object stored in the Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-573">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-573">Prototype</span></span>

```C
UINT ux_host_class_pima_object_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *object_buffer,
    ULONG object_buffer_length,
    ULONG *object_actual_length)
```

### <a name="description"></a><span data-ttu-id="9899c-574">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-574">Description</span></span>

<span data-ttu-id="9899c-575">Questa funzione ottiene un oggetto nel risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-575">This function gets an object on the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-576">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-576">Parameters</span></span>

- <span data-ttu-id="9899c-577">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-577">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-578">**pima_session**: puntatore alla sessione Pima</span><span class="sxs-lookup"><span data-stu-id="9899c-578">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="9899c-579">**object_handle**: handle dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-579">**object_handle**: handle of the object</span></span>
- <span data-ttu-id="9899c-580">**oggetto**: puntatore al contenitore di informazioni sugli oggetti</span><span class="sxs-lookup"><span data-stu-id="9899c-580">**object**: Pointer to object information container</span></span>
- <span data-ttu-id="9899c-581">**object_buffer**: indirizzo dei dati oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-581">**object_buffer**: Address of object data</span></span>
- <span data-ttu-id="9899c-582">**object_buffer_length**: lunghezza richiesta dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-582">**object_buffer_length**: Requested length of object</span></span>
- <span data-ttu-id="9899c-583">**object_actual_length**: lunghezza dell'oggetto restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-583">**object_actual_length**: Length of object returned</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-584">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-584">Return Value</span></span>

- <span data-ttu-id="9899c-585">**UX_SUCCESS**: (0x00) l'oggetto è stato trasferito</span><span class="sxs-lookup"><span data-stu-id="9899c-585">**UX_SUCCESS**: (0x00) The object was transfered</span></span>
- <span data-ttu-id="9899c-586">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta</span><span class="sxs-lookup"><span data-stu-id="9899c-586">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="9899c-587">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) oggetto non aperto.</span><span class="sxs-lookup"><span data-stu-id="9899c-587">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0x2023) Object not opened.</span></span>
- <span data-ttu-id="9899c-588">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0X200f) accesso negato all'oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-588">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) Access to object denied</span></span>
- <span data-ttu-id="9899c-589">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: il trasferimento (0x2007) è incompleto</span><span class="sxs-lookup"><span data-stu-id="9899c-589">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) Transfer is incomplete</span></span>
- <span data-ttu-id="9899c-590">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-590">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>
- <span data-ttu-id="9899c-591">**UX_TRANSFER_ERROR**: (0x23) errore di trasferimento durante la lettura dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-591">**UX_TRANSFER_ERROR**: (0x23) Transfer error while reading object</span></span>

### <a name="example"></a><span data-ttu-id="9899c-592">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-592">Example</span></span>

```C
/* Open the object. */

status = ux_host_class_pima_object_open(pima, pima_session,
    object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);

/* Set the object buffer pointer. */
object_buffer = pima_object ->ux_host_class_pima_object_buffer;

/* Obtain all the object data. */
while(object_length != 0)
{
    /* Calculate what length to request. */
    if (object_length > UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER)
        /* Request maximum length. */
        requested_length = UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER;
    else
        /* Request remaining length. */
        requested_length = object_length;

    /* Get the object data. */
    status = ux_host_class_pima_object_get(pima, pima_session,
        object_handle, pima_object, object_buffer,
        requested_length, &actual_length);

    if (status != UX_SUCCESS)
    {
        /* We had a problem, abort the transfer. */
        ux_host_class_pima_object_transfer_abort(pima, pima_session,
            object_handle, pima_object);

        /* And close the object. */
        ux_host_class_pima_object_close(pima, pima_session,
            object_handle, pima_object, object);

        return(status);

    }

    /* We have received some data, update the length remaining. */
    object_length -= actual_length;

    /* Update the buffer address. */
    object_buffer += actual_length;

}

/* Close the object. */
status = ux_host_class_pima_object_close(pima, pima_session,
    object_handle, pima_object, object);
```

## <a name="ux_host_class_pima_object_send"></a><span data-ttu-id="9899c-593">ux_host_class_pima_object_send</span><span class="sxs-lookup"><span data-stu-id="9899c-593">ux_host_class_pima_object_send</span></span>

<span data-ttu-id="9899c-594">Invia un oggetto archiviato nel risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-594">Send an object stored in the Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-595">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-595">Prototype</span></span>

```C
UINT ux_host_class_pima_object_send(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *object_buffer, ULONG object_buffer_length)
```

### <a name="description"></a><span data-ttu-id="9899c-596">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-596">Description</span></span>

<span data-ttu-id="9899c-597">Questa funzione Invia un oggetto al risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-597">This function sends an object to the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-598">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-598">Parameters</span></span>

- <span data-ttu-id="9899c-599">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-599">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-600">**pima_sessio**: puntatore alla sessione Pima</span><span class="sxs-lookup"><span data-stu-id="9899c-600">**pima_sessio**: Pointer to PIMA session</span></span>
- <span data-ttu-id="9899c-601">**object_handle**: handle dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-601">**object_handle**: handle of the object</span></span>
- <span data-ttu-id="9899c-602">**oggetto**: puntatore al contenitore di informazioni sugli oggetti</span><span class="sxs-lookup"><span data-stu-id="9899c-602">**object**: Pointer to object information container</span></span>
- <span data-ttu-id="9899c-603">**object_buffer**: indirizzo dei dati oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-603">**object_buffer**: Address of object data</span></span>
- <span data-ttu-id="9899c-604">**object_buffer_length**: lunghezza richiesta dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-604">**object_buffer_length**: Requested length of object</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-605">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-605">Return Value</span></span>

- <span data-ttu-id="9899c-606">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-606">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-607">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0X2003) sessione non aperta</span><span class="sxs-lookup"><span data-stu-id="9899c-607">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened</span></span>
- <span data-ttu-id="9899c-608">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) oggetto non aperto.</span><span class="sxs-lookup"><span data-stu-id="9899c-608">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0x2023) Object not opened.</span></span>
- <span data-ttu-id="9899c-609">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0X200f) accesso negato all'oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-609">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) Access to object denied</span></span>
- <span data-ttu-id="9899c-610">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: il trasferimento (0x2007) è incompleto</span><span class="sxs-lookup"><span data-stu-id="9899c-610">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) Transfer is incomplete</span></span>
- <span data-ttu-id="9899c-611">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-611">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>
- <span data-ttu-id="9899c-612">**UX_TRANSFER_ERROR**: (0x23) errore di trasferimento durante la scrittura dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-612">**UX_TRANSFER_ERROR**: (0x23) Transfer error while writing object</span></span>

### <a name="example"></a><span data-ttu-id="9899c-613">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-613">Example</span></span>

```C
/* Open the object. */
status = ux_host_class_pima_object_open(pima, pima_session,
    object_handle, pima_object);

/* Get the object length. */
object_length = pima_object ->ux_host_class_pima_object_compressed_size;

/* Recall the object buffer address. */
pima_object_buffer = pima_object ->ux_host_class_pima_object_buffer;

/* Send all the object data. */
while(object_length != 0)
{
    /* Calculate what length to request. */
    if (object_length > UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER)
        /* Request maximum length. */
        requested_length = UX_PICTBRIDGE_MAX_PIMA_OBJECT_BUFFER;
    else
        /* Request remaining length. */
        requested_length = object_length;

    /* Send the object data. */
    status = ux_host_class_pima_object_send(pima,
        pima_session, pima_object,
        pima_object_buffer, requested_length);

    if (status != UX_SUCCESS)
    {
        /* Abort the transfer. */
        ux_host_class_pima_object_transfer_abort(pima, pima_session,
            object_handle, pima_object);

        /* Return status. */
        return(status);
    }

    /* We have sent some data, update the length remaining. */
    object_length -= requested_length;
}

/* Close the object. */
status = ux_host_class_pima_object_close(pima, pima_session, object_handle,
    pima_object, object);
```

## <a name="ux_host_class_pima_thumb_get"></a><span data-ttu-id="9899c-614">ux_host_class_pima_thumb_get</span><span class="sxs-lookup"><span data-stu-id="9899c-614">ux_host_class_pima_thumb_get</span></span>

<span data-ttu-id="9899c-615">Ottiene un oggetto Thumb archiviato nel risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-615">Get a thumb object stored in the Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-616">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-616">Prototype</span></span>

```C
UINT ux_host_class_pima_thumb_get(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle,
    UX_HOST_CLASS_PIMA_OBJECT *object,
    UCHAR *thumb_buffer, ULONG thumb_buffer_length,
    ULONG *thumb_actual_length)
```

### <a name="description"></a><span data-ttu-id="9899c-617">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-617">Description</span></span>

<span data-ttu-id="9899c-618">Questa funzione ottiene un oggetto Thumb sul risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-618">This function gets a thumb object on the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-619">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-619">Parameters</span></span>

- <span data-ttu-id="9899c-620">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-620">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-621">**pima_session**: puntatore alla sessione Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-621">**pima_session**: Pointer to PIMA session.</span></span>
- <span data-ttu-id="9899c-622">**object_handle**: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9899c-622">**object_handle**: handle of the object.</span></span>
- <span data-ttu-id="9899c-623">**oggetto**: puntatore al contenitore di informazioni sugli oggetti.</span><span class="sxs-lookup"><span data-stu-id="9899c-623">**object**: Pointer to object information container.</span></span>
- <span data-ttu-id="9899c-624">**thumb_buffer**: indirizzo dei dati dell'oggetto Thumb.</span><span class="sxs-lookup"><span data-stu-id="9899c-624">**thumb_buffer**: Address of thumb object data.</span></span>
- <span data-ttu-id="9899c-625">**thumb_buffer_length**: lunghezza richiesta dell'oggetto Thumb.</span><span class="sxs-lookup"><span data-stu-id="9899c-625">**thumb_buffer_length**: Requested length of thumb object.</span></span>
- <span data-ttu-id="9899c-626">**thumb_actual_length**: viene restituita la lunghezza dell'oggetto Thumb.</span><span class="sxs-lookup"><span data-stu-id="9899c-626">**thumb_actual_length**: Length of thumb object returned.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-627">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-627">Return Value</span></span>

- <span data-ttu-id="9899c-628">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-628">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-629">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: la sessione (0x2003) non è aperta.</span><span class="sxs-lookup"><span data-stu-id="9899c-629">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened.</span></span>
- <span data-ttu-id="9899c-630">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) oggetto non aperto.</span><span class="sxs-lookup"><span data-stu-id="9899c-630">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0x2023) Object not opened.</span></span>
- <span data-ttu-id="9899c-631">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0X200f) accesso negato all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9899c-631">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) Access to object denied.</span></span>
- <span data-ttu-id="9899c-632">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: il trasferimento (0x2007) è incompleto.</span><span class="sxs-lookup"><span data-stu-id="9899c-632">**UX_HOST_CLASS_PIMA_RC_INCOMPLETE_TRANSFER**: (0x2007) Transfer is incomplete.</span></span>
- <span data-ttu-id="9899c-633">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-633">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>
- <span data-ttu-id="9899c-634">**UX_TRANSFER_ERROR**: (0x23) errore di trasferimento durante la lettura dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9899c-634">**UX_TRANSFER_ERROR**: (0x23) Transfer error while reading object.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-635">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-635">Example</span></span>

```C
/* Get the thumb object data. */

status = ux_host_class_pima_thumb_get(pima, pima_session,
    object_handle, pima_object, object_buffer,
    requested_length, &actual_length);

if (status != UX_SUCCESS)
{
    /* And close the object. */
    ux_host_class_pima_object_close(pima, pima_session, object_handle, pima_object, object);

    return(status);
}
```

## <a name="ux_host_class_pima_object_delete"></a><span data-ttu-id="9899c-636">ux_host_class_pima_object_delete</span><span class="sxs-lookup"><span data-stu-id="9899c-636">ux_host_class_pima_object_delete</span></span>

<span data-ttu-id="9899c-637">Elimina un oggetto archiviato nel risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-637">Delete an object stored in the Responder.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-638">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-638">Prototype</span></span>

```C
UINT ux_host_class_pima_object_delete(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle)
```

### <a name="description"></a><span data-ttu-id="9899c-639">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-639">Description</span></span>

<span data-ttu-id="9899c-640">Questa funzione Elimina un oggetto nel risponditore</span><span class="sxs-lookup"><span data-stu-id="9899c-640">This function deletes an object on the responder</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-641">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-641">Parameters</span></span>

- <span data-ttu-id="9899c-642">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-642">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-643">**pima_session**: puntatore alla sessione Pima</span><span class="sxs-lookup"><span data-stu-id="9899c-643">**pima_session**: Pointer to PIMA session</span></span>
- <span data-ttu-id="9899c-644">**object_handle**: handle dell'oggetto</span><span class="sxs-lookup"><span data-stu-id="9899c-644">**object_handle**: handle of the object</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-645">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-645">Return Value</span></span>

- <span data-ttu-id="9899c-646">**UX_SUCCESS**: (0x00) l'oggetto è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="9899c-646">**UX_SUCCESS**: (0x00) The object was deleted.</span></span>
- <span data-ttu-id="9899c-647">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: la sessione (0x2003) non è aperta.</span><span class="sxs-lookup"><span data-stu-id="9899c-647">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened.</span></span>
- <span data-ttu-id="9899c-648">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0X200f) non è possibile eliminare l'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9899c-648">**UX_HOST_CLASS_PIMA_RC_ACCESS_DENIED**: (0x200f) Cannot delete object.</span></span>
- <span data-ttu-id="9899c-649">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-649">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-650">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-650">Example</span></span>

```C
/* Delete the object. */
status = ux_host_class_pima_object_delete(pima, pima_session, object_handle, pima_object);

/* Check status. */
if (status != UX_SUCCESS)
    return(status);
```

## <a name="ux_host_class_pima_object_close"></a><span data-ttu-id="9899c-651">ux_host_class_pima_object_close</span><span class="sxs-lookup"><span data-stu-id="9899c-651">ux_host_class_pima_object_close</span></span>

<span data-ttu-id="9899c-652">Chiude un oggetto archiviato nel risponditore</span><span class="sxs-lookup"><span data-stu-id="9899c-652">Close an object stored in the Responder</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-653">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-653">Prototype</span></span>

```C
UINT ux_host_class_pima_object_close(
    UX_HOST_CLASS_PIMA *pima,
    UX_HOST_CLASS_PIMA_SESSION *pima_session,
    ULONG object_handle, UX_HOST_CLASS_PIMA_OBJECT *object)
```

### <a name="description"></a><span data-ttu-id="9899c-654">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-654">Description</span></span>

<span data-ttu-id="9899c-655">Questa funzione chiude un oggetto nel risponditore.</span><span class="sxs-lookup"><span data-stu-id="9899c-655">This function closes an object on the responder.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-656">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-656">Parameters</span></span>

- <span data-ttu-id="9899c-657">**Pima**: puntatore all'istanza della classe Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-657">**pima**: Pointer to the pima class instance.</span></span>
- <span data-ttu-id="9899c-658">**pima_session**: puntatore alla sessione Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-658">**pima_session**: Pointer to PIMA session.</span></span>
- <span data-ttu-id="9899c-659">**object_handle**: handle dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9899c-659">**object_handle**: Handle of the object.</span></span>
- <span data-ttu-id="9899c-660">**oggetto**: puntatore all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9899c-660">**object**: Pointer to object.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-661">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-661">Return Value</span></span>

- <span data-ttu-id="9899c-662">**UX_SUCCESS**: (0x00) l'oggetto è stato chiuso.</span><span class="sxs-lookup"><span data-stu-id="9899c-662">**UX_SUCCESS**: (0x00) The object was closed.</span></span>
- <span data-ttu-id="9899c-663">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: la sessione (0x2003) non è aperta.</span><span class="sxs-lookup"><span data-stu-id="9899c-663">**UX_HOST_CLASS_PIMA_RC_SESSION_NOT_OPEN**: (0x2003) Session not opened.</span></span>
- <span data-ttu-id="9899c-664">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0X2023) oggetto non aperto.</span><span class="sxs-lookup"><span data-stu-id="9899c-664">**UX_HOST_CLASS_PIMA_RC_OBJECT_NOT_OPENED**: (0x2023) Object not opened.</span></span>
- <span data-ttu-id="9899c-665">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente per creare il comando Pima.</span><span class="sxs-lookup"><span data-stu-id="9899c-665">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory to create PIMA command.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-666">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-666">Example</span></span>

```C
/* Close the object. */
status = ux_host_class_pima_object_close(pima, pima_session, object_handle, object);
```

## <a name="ux_host_class_gser_read"></a><span data-ttu-id="9899c-667">ux_host_class_gser_read</span><span class="sxs-lookup"><span data-stu-id="9899c-667">ux_host_class_gser_read</span></span>

<span data-ttu-id="9899c-668">Leggere dall'interfaccia seriale generica.</span><span class="sxs-lookup"><span data-stu-id="9899c-668">Read from the generic serial interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-669">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-669">Prototype</span></span>

```C
UINT ux_host_class_gser_read(
    UX_HOST_CLASS_GSER *gser,
    ULONG interface_index,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="9899c-670">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-670">Description</span></span>

<span data-ttu-id="9899c-671">Questa funzione legge dall'interfaccia seriale generica.</span><span class="sxs-lookup"><span data-stu-id="9899c-671">This function reads from the generic serial interface.</span></span> <span data-ttu-id="9899c-672">La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.</span><span class="sxs-lookup"><span data-stu-id="9899c-672">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-673">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-673">Parameters</span></span>

- <span data-ttu-id="9899c-674">**gser**: puntatore all'istanza della classe gser.</span><span class="sxs-lookup"><span data-stu-id="9899c-674">**gser**: Pointer to the gser class instance.</span></span>
- <span data-ttu-id="9899c-675">**interface_index**: Indice dell'interfaccia da cui leggere.</span><span class="sxs-lookup"><span data-stu-id="9899c-675">**interface_index**: Interface index to read from.</span></span>
- <span data-ttu-id="9899c-676">**data_pointer**: puntatore all'indirizzo del buffer del payload di dati.</span><span class="sxs-lookup"><span data-stu-id="9899c-676">**data_pointer**: Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="9899c-677">**requested_length**: lunghezza da ricevere.</span><span class="sxs-lookup"><span data-stu-id="9899c-677">**requested_length**: Length to be received.</span></span>
- <span data-ttu-id="9899c-678">**actual_length**: lunghezza effettivamente ricevuta.</span><span class="sxs-lookup"><span data-stu-id="9899c-678">**actual_length**: Length actually received.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-679">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-679">Return Value</span></span>

- <span data-ttu-id="9899c-680">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-680">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-681">**UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, lettura incompleta.</span><span class="sxs-lookup"><span data-stu-id="9899c-681">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, reading incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-682">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-682">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_gser_read(cdc_acm, interface_index,data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_write"></a><span data-ttu-id="9899c-683">ux_host_class_gser_write</span><span class="sxs-lookup"><span data-stu-id="9899c-683">ux_host_class_gser_write</span></span>

<span data-ttu-id="9899c-684">Scrivere nell'interfaccia seriale generica.</span><span class="sxs-lookup"><span data-stu-id="9899c-684">Write to the generic serial interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-685">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-685">Prototype</span></span>

```C
UINT ux_host_class_gser_write(
    UX_HOST_CLASS_GSER *gser,
    ULONG interface_index,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length)
```

### <a name="description"></a><span data-ttu-id="9899c-686">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-686">Description</span></span>

<span data-ttu-id="9899c-687">Questa funzione scrive nell'interfaccia seriale generica.</span><span class="sxs-lookup"><span data-stu-id="9899c-687">This function writes to the generic serial interface.</span></span> <span data-ttu-id="9899c-688">La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.</span><span class="sxs-lookup"><span data-stu-id="9899c-688">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-689">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-689">Parameters</span></span>

- <span data-ttu-id="9899c-690">**gser**: puntatore all'istanza della classe gser.</span><span class="sxs-lookup"><span data-stu-id="9899c-690">**gser**: Pointer to the gser class instance.</span></span>
- <span data-ttu-id="9899c-691">**interface_index**: interfaccia in cui scrivere.</span><span class="sxs-lookup"><span data-stu-id="9899c-691">**interface_index**: Interface to which to write.</span></span>
- <span data-ttu-id="9899c-692">**data_pointer**: puntatore all'indirizzo del buffer del payload di dati.</span><span class="sxs-lookup"><span data-stu-id="9899c-692">**data_pointer**: Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="9899c-693">**requested_length**: lunghezza da inviare.</span><span class="sxs-lookup"><span data-stu-id="9899c-693">**requested_length**: Length to be sent.</span></span>
- <span data-ttu-id="9899c-694">**actual_length**: lunghezza effettivamente inviata.</span><span class="sxs-lookup"><span data-stu-id="9899c-694">**actual_length**: Length actually sent.</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-695">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-695">Return Value</span></span>

- <span data-ttu-id="9899c-696">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-696">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-697">**UX_TRANSFER_TIMEOUT**: (0x5c) timeout di trasferimento, scrittura incompleta.</span><span class="sxs-lookup"><span data-stu-id="9899c-697">**UX_TRANSFER_TIMEOUT**: (0x5c) Transfer timeout, writing incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="9899c-698">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-698">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */
status = ux_host_class_cdc_acm_write(gser, data_pointer, requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_ioctl"></a><span data-ttu-id="9899c-699">ux_host_class_gser_ioctl</span><span class="sxs-lookup"><span data-stu-id="9899c-699">ux_host_class_gser_ioctl</span></span>

<span data-ttu-id="9899c-700">Eseguire una funzione IOCTL nell'interfaccia seriale generica.</span><span class="sxs-lookup"><span data-stu-id="9899c-700">Perform an IOCTL function to the generic serial interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-701">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-701">Prototype</span></span>

```C
UINT ux_host_class_gser_ioctl(
    UX_HOST_CLASS_GSER *gser,
    ULONG ioctl_function,
    VOID *parameter)
```

### <a name="description"></a><span data-ttu-id="9899c-702">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-702">Description</span></span>

<span data-ttu-id="9899c-703">Questa funzione esegue una specifica funzione IOCTL per l'interfaccia gser.</span><span class="sxs-lookup"><span data-stu-id="9899c-703">This function performs a specific ioctl function to the gser interface.</span></span> <span data-ttu-id="9899c-704">La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il comando viene completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-704">The call is blocking and only returns when there is either an error or when the command is completed.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-705">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-705">Parameters</span></span>

- <span data-ttu-id="9899c-706">**gser**: puntatore all'istanza della classe gser.</span><span class="sxs-lookup"><span data-stu-id="9899c-706">**gser**: Pointer to the gser class instance.</span></span>
- <span data-ttu-id="9899c-707">**ioctl_function**: funzione IOCTL da eseguire.</span><span class="sxs-lookup"><span data-stu-id="9899c-707">**ioctl_function**: ioctl function to be performed.</span></span> <span data-ttu-id="9899c-708">Vedere la tabella seguente per una delle funzioni IOCTL consentite.</span><span class="sxs-lookup"><span data-stu-id="9899c-708">See table below for one of the allowed ioctl functions.</span></span>
- <span data-ttu-id="9899c-709">**parametro**: Pointerto un parametro specifico per IOCTL</span><span class="sxs-lookup"><span data-stu-id="9899c-709">**parameter**: Pointerto a parameter specific to the ioctl</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-710">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-710">Return Value</span></span>

- <span data-ttu-id="9899c-711">**UX_SUCCESS**: (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-711">**UX_SUCCESS**: (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-712">**UX_MEMORY_INSUFFICIENT**: (0x12) memoria insufficiente.</span><span class="sxs-lookup"><span data-stu-id="9899c-712">**UX_MEMORY_INSUFFICIENT**: (0x12) Not enough memory.</span></span>
- <span data-ttu-id="9899c-713">**UX_HOST_CLASS_UNKNOWN**: (0x59) istanza di classe errata</span><span class="sxs-lookup"><span data-stu-id="9899c-713">**UX_HOST_CLASS_UNKNOWN**: (0x59) Wrong class instance</span></span>
- <span data-ttu-id="9899c-714">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) funzione IOCTL sconosciuta.</span><span class="sxs-lookup"><span data-stu-id="9899c-714">**UX_FUNCTION_NOT_SUPPORTED**: (0x54) Unknown IOCTL function.</span></span>

### <a name="ioctl-functions"></a><span data-ttu-id="9899c-715">Funzioni IOCTL</span><span class="sxs-lookup"><span data-stu-id="9899c-715">IOCTL functions</span></span>

- <span data-ttu-id="9899c-716">UX_HOST_CLASS_GSER_IOCTL_SET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="9899c-716">UX_HOST_CLASS_GSER_IOCTL_SET_LINE_CODING</span></span>
- <span data-ttu-id="9899c-717">UX_HOST_CLASS_GSER_IOCTL_GET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="9899c-717">UX_HOST_CLASS_GSER_IOCTL_GET_LINE_CODING</span></span>
- <span data-ttu-id="9899c-718">UX_HOST_CLASS_GSER_IOCTL_SET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="9899c-718">UX_HOST_CLASS_GSER_IOCTL_SET_LINE_STATE</span></span>
- <span data-ttu-id="9899c-719">UX_HOST_CLASS_GSER_IOCTL_SEND_BREAK</span><span class="sxs-lookup"><span data-stu-id="9899c-719">UX_HOST_CLASS_GSER_IOCTL_SEND_BREAK</span></span>
- <span data-ttu-id="9899c-720">UX_HOST_CLASS_GSER_IOCTL_ABORT_IN_PIPE</span><span class="sxs-lookup"><span data-stu-id="9899c-720">UX_HOST_CLASS_GSER_IOCTL_ABORT_IN_PIPE</span></span>
- <span data-ttu-id="9899c-721">UX_HOST_CLASS_GSER_IOCTL_ABORT_OUT_PIPE</span><span class="sxs-lookup"><span data-stu-id="9899c-721">UX_HOST_CLASS_GSER_IOCTL_ABORT_OUT_PIPE</span></span>
- <span data-ttu-id="9899c-722">UX_HOST_CLASS_GSER_IOCTL_NOTIFICATION_CALLBACK</span><span class="sxs-lookup"><span data-stu-id="9899c-722">UX_HOST_CLASS_GSER_IOCTL_NOTIFICATION_CALLBACK</span></span>
- <span data-ttu-id="9899c-723">UX_HOST_CLASS_GSER_IOCTL_GET_DEVICE_STATUS</span><span class="sxs-lookup"><span data-stu-id="9899c-723">UX_HOST_CLASS_GSER_IOCTL_GET_DEVICE_STATUS</span></span>

### <a name="example"></a><span data-ttu-id="9899c-724">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-724">Example</span></span>

```C
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_gser_ioctl(gser,
    UX_HOST_CLASS_GSER_IOCTL_GET_LINE_CODING,
    (VOID *)&line_coding);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_gser_reception_start"></a><span data-ttu-id="9899c-725">ux_host_class_gser_reception_start</span><span class="sxs-lookup"><span data-stu-id="9899c-725">ux_host_class_gser_reception_start</span></span>

<span data-ttu-id="9899c-726">Avviare la ricezione sull'interfaccia seriale generica</span><span class="sxs-lookup"><span data-stu-id="9899c-726">Start reception on the generic serial interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-727">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-727">Prototype</span></span>

```C
UINT ux_host_class_gser_reception_start(
    UX_HOST_CLASS_GSER *gser,
    UX_HOST_CLASS_GSER_RECEPTION *gser_reception)
```

### <a name="description"></a><span data-ttu-id="9899c-728">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-728">Description</span></span>

<span data-ttu-id="9899c-729">Questa funzione avvia la ricezione sull'interfaccia della classe seriale generica.</span><span class="sxs-lookup"><span data-stu-id="9899c-729">This function starts the reception on the generic serial class interface.</span></span> <span data-ttu-id="9899c-730">Questa funzione consente la ricezione senza blocco.</span><span class="sxs-lookup"><span data-stu-id="9899c-730">This function allows for non-blocking reception.</span></span> <span data-ttu-id="9899c-731">Quando viene ricevuto un buffer, viene richiamato un callback nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9899c-731">When a buffer is received, a callback in invoked into the application.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-732">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-732">Parameters</span></span>

- <span data-ttu-id="9899c-733">**gser** Puntatore all'istanza della classe gser.</span><span class="sxs-lookup"><span data-stu-id="9899c-733">**gser** Pointer to the gser class instance.</span></span>
- <span data-ttu-id="9899c-734">**gser_reception** Struttura che contiene i parametri di ricezione</span><span class="sxs-lookup"><span data-stu-id="9899c-734">**gser_reception** Structure containing the reception parameters</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-735">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-735">Return Value</span></span>

- <span data-ttu-id="9899c-736">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-736">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-737">Istanza di classe non corretta **UX_HOST_CLASS_UNKNOWN** (0x59)</span><span class="sxs-lookup"><span data-stu-id="9899c-737">**UX_HOST_CLASS_UNKNOWN** (0x59) Wrong class instance</span></span>
- <span data-ttu-id="9899c-738">Errore **UX_ERROR** (0x01)</span><span class="sxs-lookup"><span data-stu-id="9899c-738">**UX_ERROR** (0x01) Error</span></span>

### <a name="example"></a><span data-ttu-id="9899c-739">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-739">Example</span></span>

```C
/* Start the reception for gser. AT commands are on interface 2. */
gser_reception.ux_host_class_gser_reception_interface_index =
    UX_DEMO_GSER_AT_INTERFACE;
gser_reception.ux_host_class_gser_reception_block_size =
    UX_DEMO_RECEPTION_BLOCK_SIZE;
gser_reception.ux_host_class_gser_reception_data_buffer =
    gser_reception_buffer;
gser_reception.ux_host_class_gser_reception_data_buffer_size =
    UX_DEMO_RECEPTION_BUFFER_SIZE;
gser_reception.ux_host_class_gser_reception_callback =
    tx_demo_thread_callback;

ux_host_class_gser_reception_start(gser, &gser_reception);
```

## <a name="ux_host_class_gser_reception_stop"></a><span data-ttu-id="9899c-740">ux_host_class_gser_reception_stop</span><span class="sxs-lookup"><span data-stu-id="9899c-740">ux_host_class_gser_reception_stop</span></span>

<span data-ttu-id="9899c-741">Arrestare la ricezione sull'interfaccia seriale generica</span><span class="sxs-lookup"><span data-stu-id="9899c-741">Stop reception on the generic serial interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9899c-742">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9899c-742">Prototype</span></span>

```C
UINT ux_host_class_gser_reception_stop(
    UX_HOST_CLASS_GSER *gser,
    UX_HOST_CLASS_GSER_RECEPTION *gser_reception)
```

### <a name="description"></a><span data-ttu-id="9899c-743">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9899c-743">Description</span></span>

<span data-ttu-id="9899c-744">Questa funzione arresta la ricezione sull'interfaccia della classe seriale generica.</span><span class="sxs-lookup"><span data-stu-id="9899c-744">This function stops the reception on the generic serial class interface.</span></span>

### <a name="parameters"></a><span data-ttu-id="9899c-745">Parametri</span><span class="sxs-lookup"><span data-stu-id="9899c-745">Parameters</span></span>

- <span data-ttu-id="9899c-746">**gser** Puntatore all'istanza della classe gser.</span><span class="sxs-lookup"><span data-stu-id="9899c-746">**gser** Pointer to the gser class instance.</span></span>
- <span data-ttu-id="9899c-747">**gser_reception** Struttura che contiene i parametri di ricezione</span><span class="sxs-lookup"><span data-stu-id="9899c-747">**gser_reception** Structure containing the reception parameters</span></span>

### <a name="return-value"></a><span data-ttu-id="9899c-748">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="9899c-748">Return Value</span></span>

- <span data-ttu-id="9899c-749">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="9899c-749">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="9899c-750">Istanza di classe non corretta **UX_HOST_CLASS_UNKNOWN** (0x59)</span><span class="sxs-lookup"><span data-stu-id="9899c-750">**UX_HOST_CLASS_UNKNOWN** (0x59) Wrong class instance</span></span>
- <span data-ttu-id="9899c-751">Errore **UX_ERROR** (0x01)</span><span class="sxs-lookup"><span data-stu-id="9899c-751">**UX_ERROR** (0x01) Error</span></span>

### <a name="example"></a><span data-ttu-id="9899c-752">Esempio</span><span class="sxs-lookup"><span data-stu-id="9899c-752">Example</span></span>

```C
/* Stops the reception for gser. */
ux_host_class_gser_reception_stop(gser, &gser_reception);
```
