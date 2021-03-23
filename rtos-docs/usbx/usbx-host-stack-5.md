---
title: Capitolo 5-API delle classi host USBX
description: Informazioni sulle API delle classi host USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: bf5876042e08a59979adcd429917bfc3fbfdbc20
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824524"
---
# <a name="chapter-5---usbx-host-classes-api"></a><span data-ttu-id="cc862-103">Capitolo 5-API delle classi host USBX</span><span class="sxs-lookup"><span data-stu-id="cc862-103">Chapter 5 - USBX Host Classes API</span></span>

<span data-ttu-id="cc862-104">In questo capitolo vengono illustrate tutte le API esposte delle classi host USBX.</span><span class="sxs-lookup"><span data-stu-id="cc862-104">This chapter covers all the exposed APIs of the USBX host classes.</span></span> <span data-ttu-id="cc862-105">Le API seguenti per ogni classe sono descritte in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="cc862-105">The following APIs for each class are described in detail.</span></span>

- <span data-ttu-id="cc862-106">Classe HID</span><span class="sxs-lookup"><span data-stu-id="cc862-106">HID class</span></span>
- <span data-ttu-id="cc862-107">CDC-ACM (classe)</span><span class="sxs-lookup"><span data-stu-id="cc862-107">CDC-ACM class</span></span>
- <span data-ttu-id="cc862-108">Classe CDC-ECM</span><span class="sxs-lookup"><span data-stu-id="cc862-108">CDC-ECM class</span></span>
- <span data-ttu-id="cc862-109">Classe di archiviazione</span><span class="sxs-lookup"><span data-stu-id="cc862-109">Storage class</span></span>

## <a name="ux_host_class_hid_client_register"></a><span data-ttu-id="cc862-110">ux_host_class_hid_client_register</span><span class="sxs-lookup"><span data-stu-id="cc862-110">ux_host_class_hid_client_register</span></span>

<span data-ttu-id="cc862-111">Registrare un client nascosto nella classe HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-111">Register a HID client to the HID class.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-112">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-112">Prototype</span></span>

```c
UINT ux_host_class_hid_client_register(
    UCHAR *hid_client_name,
    UINT (*hid_client_handler)
    (struct UX_HOST_CLASS_HID_CLIENT_COMMAND_STRUCT *));
```

### <a name="description"></a><span data-ttu-id="cc862-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-113">Description</span></span>

<span data-ttu-id="cc862-114">Questa funzione viene utilizzata per registrare un client nascosto nella classe HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-114">This function is used to register a HID client to the HID class.</span></span> <span data-ttu-id="cc862-115">La classe HID deve trovare una corrispondenza tra un dispositivo HID e un client nascosto prima di richiedere i dati da questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc862-115">The HID class needs to find a match between a HID device and HID client before requesting data from this device.</span></span>

> [!NOTE]
> <span data-ttu-id="cc862-116">La stringa C di hid_client_name deve essere con terminazione NULL e la lunghezza (senza il carattere di terminazione NULL) non deve essere maggiore di **UX_HOST_CLASS_HID_MAX_CLIENT_NAME_LENGTH**.</span><span class="sxs-lookup"><span data-stu-id="cc862-116">The C string of hid_client_name must be NULL-terminated and the length of it (without the NULL-terminator itself) must be no larger than **UX_HOST_CLASS_HID_MAX_CLIENT_NAME_LENGTH**.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-117">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-117">Parameters</span></span>

- <span data-ttu-id="cc862-118">**hid_client_name** Puntatore al nome del client HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-118">**hid_client_name** Pointer to the HID client name.</span></span>
- <span data-ttu-id="cc862-119">**hid_client_handler** Puntatore al gestore client nascosto.</span><span class="sxs-lookup"><span data-stu-id="cc862-119">**hid_client_handler** Pointer to the HID client handler.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-120">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-120">Return Values</span></span>

- <span data-ttu-id="cc862-121">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato</span><span class="sxs-lookup"><span data-stu-id="cc862-121">**UX_SUCCESS** (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="cc862-122">L'allocazione di memoria **UX_MEMORY_INSUFFICIENT** (0x12) per il client non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="cc862-122">**UX_MEMORY_INSUFFICIENT** (0x12) Memory allocation for client failed.</span></span>
- <span data-ttu-id="cc862-123">Il numero massimo di client **UX_MEMORY_ARRAY_FULL** (0x1A) è già registrato.</span><span class="sxs-lookup"><span data-stu-id="cc862-123">**UX_MEMORY_ARRAY_FULL** (0x1a) Max clients already registered.</span></span>
- <span data-ttu-id="cc862-124">**UX_HOST_CLASS_ALREADY_INSTALLED** (0X58) questa classe esiste già</span><span class="sxs-lookup"><span data-stu-id="cc862-124">**UX_HOST_CLASS_ALREADY_INSTALLED** (0x58) This class already exists</span></span>

### <a name="example"></a><span data-ttu-id="cc862-125">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-125">Example</span></span>

```c
UINT status;

/* The following example illustrates how to register a HID client, in
this case a USB mouse, to the HID class. */

status = ux_host_class_hid_client_register("ux_host_class_hid_client_mouse",
    ux_host_class_hid_mouse_entry);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_callback_register"></a><span data-ttu-id="cc862-126">ux_host_class_hid_report_callback_register</span><span class="sxs-lookup"><span data-stu-id="cc862-126">ux_host_class_hid_report_callback_register</span></span>

<span data-ttu-id="cc862-127">Registrare un callback dalla classe HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-127">Register a callback from the HID class.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-128">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-128">Prototype</span></span>

```c
UINT ux_host_class_hid_report_callback_register(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_REPORT_CALLBACK *call_back);
```

### <a name="description"></a><span data-ttu-id="cc862-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-129">Description</span></span>

<span data-ttu-id="cc862-130">Questa funzione viene utilizzata per registrare un callback dalla classe HID al client HID quando viene ricevuto un report.</span><span class="sxs-lookup"><span data-stu-id="cc862-130">This function is used to register a callback from the HID class to the HID client when a report is received.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-131">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-131">Parameters</span></span>

- <span data-ttu-id="cc862-132">**nascosto** Puntatore all'istanza della classe HID</span><span class="sxs-lookup"><span data-stu-id="cc862-132">**hid** Pointer to the HID class instance</span></span>
- <span data-ttu-id="cc862-133">**call_back** Puntatore alla struttura call_back</span><span class="sxs-lookup"><span data-stu-id="cc862-133">**call_back** Pointer to the call_back structure</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-134">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-134">Return values</span></span>

- <span data-ttu-id="cc862-135">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato</span><span class="sxs-lookup"><span data-stu-id="cc862-135">**UX_SUCCESS** (0x00) The data transfer was completed</span></span>
- <span data-ttu-id="cc862-136">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) istanza HID non valida.</span><span class="sxs-lookup"><span data-stu-id="cc862-136">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) Invalid HID instance.</span></span>
- <span data-ttu-id="cc862-137">Errore **UX_HOST_CLASS_HID_REPORT_ERROR** (0x79) nella registrazione del callback del report.</span><span class="sxs-lookup"><span data-stu-id="cc862-137">**UX_HOST_CLASS_HID_REPORT_ERROR** (0x79) Error in the report callback registration.</span></span>

### <a name="example"></a><span data-ttu-id="cc862-138">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-138">Example</span></span>

```c
UINT status;

/* This example illustrates how to register a HID client, in this case a USB mouse, to the HID class. In this case, the HID client is asking the HID class to call the client for each usage received in the HID report. */

call_back.ux_host_class_hid_report_callback_id = 0;
call_back.ux_host_class_hid_report_callback_function = ux_host_class_hid_mouse_callback;

call_back.ux_host_class_hid_report_callback_buffer = UX_NULL;
call_back.ux_host_class_hid_report_callback_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

call_back.ux_host_class_hid_report_callback_length = 0;

status = ux_host_class_hid_report_callback_register(hid, &call_back);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_periodic_report_start"></a><span data-ttu-id="cc862-139">ux_host_class_hid_periodic_report_start</span><span class="sxs-lookup"><span data-stu-id="cc862-139">ux_host_class_hid_periodic_report_start</span></span>

<span data-ttu-id="cc862-140">Avviare l'endpoint periodico per un'istanza della classe HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-140">Start the periodic endpoint for a HID class instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-141">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-141">Prototype</span></span>

```c
UINT ux_host_class_hid_periodic_report_start(UX_HOST_CLASS_HID *hid);
```

### <a name="description"></a><span data-ttu-id="cc862-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-142">Description</span></span>

<span data-ttu-id="cc862-143">Questa funzione viene utilizzata per avviare l'endpoint periodico (interrupt) per l'istanza della classe HID associata a questo client nascosto.</span><span class="sxs-lookup"><span data-stu-id="cc862-143">This function is used to start the periodic (interrupt) endpoint for the instance of the HID class that is bound to this HID client.</span></span> <span data-ttu-id="cc862-144">La classe HID non può avviare l'endpoint periodico finché il client HID non viene attivato e pertanto viene lasciato al client HID per avviare l'endpoint per la ricezione dei report.</span><span class="sxs-lookup"><span data-stu-id="cc862-144">The HID class cannot start the periodic endpoint until the HID client is activated and therefore it is left to the HID client to start this endpoint to receive reports.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="cc862-145">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="cc862-145">Input Parameter</span></span>

- <span data-ttu-id="cc862-146">**nascosto** Puntatore all'istanza della classe HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-146">**hid** Pointer to the HID class instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-147">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-147">Return Values</span></span>

- <span data-ttu-id="cc862-148">Creazione di report periodici **UX_SUCCESS** (0x00) avviata correttamente.</span><span class="sxs-lookup"><span data-stu-id="cc862-148">**UX_SUCCESS** (0x00) Periodic reporting successfully started.</span></span>
- <span data-ttu-id="cc862-149">Errore **ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) nel rapporto periodico.</span><span class="sxs-lookup"><span data-stu-id="cc862-149">**ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) Error in the periodic report.</span></span>
- <span data-ttu-id="cc862-150">L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.</span><span class="sxs-lookup"><span data-stu-id="cc862-150">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="cc862-151">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-151">Example</span></span>

```c
UINT status;

/* The following example illustrates how to start the periodic
endpoint. */

status = ux_host_class_hid_periodic_report_start(hid);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_periodic_report_stop"></a><span data-ttu-id="cc862-152">ux_host_class_hid_periodic_report_stop</span><span class="sxs-lookup"><span data-stu-id="cc862-152">ux_host_class_hid_periodic_report_stop</span></span>

<span data-ttu-id="cc862-153">Arrestare l'endpoint periodico per un'istanza della classe HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-153">Stop the periodic endpoint for a HID class instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-154">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-154">Prototype</span></span>

```c
UINT ux_host_class_hid_periodic_report_stop(UX_HOST_CLASS_HID *hid);
```

### <a name="description"></a><span data-ttu-id="cc862-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-155">Description</span></span>

<span data-ttu-id="cc862-156">Questa funzione viene utilizzata per arrestare l'endpoint periodico (interrupt) per l'istanza della classe HID associata a questo client nascosto.</span><span class="sxs-lookup"><span data-stu-id="cc862-156">This function is used to stop the periodic (interrupt) endpoint for the instance of the HID class that is bound to this HID client.</span></span> <span data-ttu-id="cc862-157">La classe HID non può arrestare l'endpoint periodico finché il client HID non viene disattivato, tutte le relative risorse vengono liberate e pertanto viene lasciato al client nascosto per arrestare l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="cc862-157">The HID class cannot stop the periodic endpoint until the HID client is deactivated, all its resources freed and therefore it is left to the HID client to stop this endpoint.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="cc862-158">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="cc862-158">Input Parameter</span></span>

- <span data-ttu-id="cc862-159">**nascosto** Puntatore all'istanza della classe HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-159">**hid** Pointer to the HID class instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-160">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-160">Return Values</span></span>

- <span data-ttu-id="cc862-161">Report periodici di **UX_SUCCESS** (0x00) arrestato correttamente.</span><span class="sxs-lookup"><span data-stu-id="cc862-161">**UX_SUCCESS** (0x00) Periodic reporting successfully stopped.</span></span>
- <span data-ttu-id="cc862-162">Errore **ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) nel rapporto periodico.</span><span class="sxs-lookup"><span data-stu-id="cc862-162">**ux_host_class_hid_PERIODIC_REPORT_ERROR** (0x7A) Error in the periodic report.</span></span>
- <span data-ttu-id="cc862-163">L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste</span><span class="sxs-lookup"><span data-stu-id="cc862-163">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist</span></span>

### <a name="example"></a><span data-ttu-id="cc862-164">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-164">Example</span></span>

```c
UINT status;

/* The following example illustrates how to stop the periodic endpoint. */

status = ux_host_class_hid_periodic_report_stop(hid);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_get"></a><span data-ttu-id="cc862-165">ux_host_class_hid_report_get</span><span class="sxs-lookup"><span data-stu-id="cc862-165">ux_host_class_hid_report_get</span></span>

<span data-ttu-id="cc862-166">Ottenere un report da un'istanza della classe HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-166">Get a report from a HID class instance.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-167">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-167">Prototype</span></span>

```c
UINT ux_host_class_hid_report_get(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_CLIENT_REPORT *client_report);
```

### <a name="description"></a><span data-ttu-id="cc862-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-168">Description</span></span>

<span data-ttu-id="cc862-169">Questa funzione viene usata per ricevere un report direttamente dal dispositivo senza basarsi sull'endpoint periodico.</span><span class="sxs-lookup"><span data-stu-id="cc862-169">This function is used to receive a report directly from the device without relying on the periodic endpoint.</span></span> <span data-ttu-id="cc862-170">Questo report è proveniente dall'endpoint di controllo, ma il suo trattamento è identico a quello che era in arrivo nell'endpoint periodico.</span><span class="sxs-lookup"><span data-stu-id="cc862-170">This report is coming from the control endpoint but its treatment is the same as though it were coming on the periodic endpoint.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-171">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-171">Parameters</span></span>

- <span data-ttu-id="cc862-172">**nascosto** Puntatore all'istanza della classe HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-172">**hid** Pointer to the HID class instance.</span></span>
- <span data-ttu-id="cc862-173">**client_report** Puntatore al report client nascosto.</span><span class="sxs-lookup"><span data-stu-id="cc862-173">**client_report** Pointer to the HID client report.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-174">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-174">Return Values</span></span>

- <span data-ttu-id="cc862-175">**UX_SUCCESS** (0x00) il report è stato ricevuto correttamente.</span><span class="sxs-lookup"><span data-stu-id="cc862-175">**UX_SUCCESS** (0x00) The report was successfully received.</span></span>
- <span data-ttu-id="cc862-176">**UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) il report del client non è valido o si è verificato un errore durante il trasferimento.</span><span class="sxs-lookup"><span data-stu-id="cc862-176">**UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) Either client report was invalid or error during transfer.</span></span>
- <span data-ttu-id="cc862-177">L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.</span><span class="sxs-lookup"><span data-stu-id="cc862-177">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>
- <span data-ttu-id="cc862-178">**UX_BUFFER_OVERFLOW** (0X5d) il buffer fornito non è sufficientemente grande da contenere il report non compresso.</span><span class="sxs-lookup"><span data-stu-id="cc862-178">**UX_BUFFER_OVERFLOW** (0x5d) The buffer supplied is not big enough to accommodate the uncompressed report.</span></span>

### <a name="example"></a><span data-ttu-id="cc862-179">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-179">Example</span></span>

```c
UX_HOST_CLASS_HID_CLIENT_REPORT input_report;

UINT status;

/* The following example illustrates how to get a report. */

input_report.ux_host_class_hid_client_report = hid_report;
input_report.ux_host_class_hid_client_report_buffer = buffer;
input_report.ux_host_class_hid_client_report_length = length;
input_report.ux_host_class_hid_client_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

status = ux_host_class_hid_report_get(hid, &input_report);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_report_set"></a><span data-ttu-id="cc862-180">ux_host_class_hid_report_set</span><span class="sxs-lookup"><span data-stu-id="cc862-180">ux_host_class_hid_report_set</span></span>

<span data-ttu-id="cc862-181">Inviare un report</span><span class="sxs-lookup"><span data-stu-id="cc862-181">Send a report</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-182">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-182">Prototype</span></span>

```c
UINT ux_host_class_hid_report_set(
    UX_HOST_CLASS_HID *hid,
    UX_HOST_CLASS_HID_CLIENT_REPORT *client_report);
```

### <a name="description"></a><span data-ttu-id="cc862-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-183">Description</span></span>

<span data-ttu-id="cc862-184">Questa funzione viene usata per inviare un report direttamente al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc862-184">This function is used to send a report directly to the device.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-185">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-185">Parameters</span></span>

- <span data-ttu-id="cc862-186">**nascosto** Puntatore all'istanza della classe HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-186">**hid** Pointer to the HID class instance.</span></span>
- <span data-ttu-id="cc862-187">**client_report** Puntatore al report client nascosto.</span><span class="sxs-lookup"><span data-stu-id="cc862-187">**client_report** Pointer to the HID client report.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-188">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-188">Return Values</span></span>

- <span data-ttu-id="cc862-189">**UX_SUCCESS** (0x00) il report è stato inviato correttamente.</span><span class="sxs-lookup"><span data-stu-id="cc862-189">**UX_SUCCESS** (0x00) The report was successfully sent.</span></span>
- <span data-ttu-id="cc862-190">**UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) il report del client non è valido o si è verificato un errore durante il trasferimento.</span><span class="sxs-lookup"><span data-stu-id="cc862-190">**UX_HOST_CLASS_HID_REPORT_ERROR** (0x70) Either client report was invalid or error during transfer.</span></span>
- <span data-ttu-id="cc862-191">L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.</span><span class="sxs-lookup"><span data-stu-id="cc862-191">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>
- <span data-ttu-id="cc862-192">**UX_HOST_CLASS_HID_REPORT_OVERFLOW** (0X5d) il buffer fornito non è sufficientemente grande da contenere il report non compresso.</span><span class="sxs-lookup"><span data-stu-id="cc862-192">**UX_HOST_CLASS_HID_REPORT_OVERFLOW** (0x5d) The buffer supplied is not big enough to accommodate the uncompressed report.</span></span>

### <a name="example"></a><span data-ttu-id="cc862-193">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-193">Example</span></span>

```c
/* The following example illustrates how to send a report. */

UX_HOST_CLASS_HID_CLIENT_REPORT input_report;

input_report.ux_host_class_hid_client_report = hid_report;
input_report.ux_host_class_hid_client_report_buffer = buffer;
input_report.ux_host_class_hid_client_report_length = length;
input_report.ux_host_class_hid_client_report_flags = UX_HOST_CLASS_HID_REPORT_INDIVIDUAL_USAGE;

status = ux_host_class_hid_report_set(hid, &input_report);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_mouse_buttons_get"></a><span data-ttu-id="cc862-194">ux_host_class_hid_mouse_buttons_get</span><span class="sxs-lookup"><span data-stu-id="cc862-194">ux_host_class_hid_mouse_buttons_get</span></span>

<span data-ttu-id="cc862-195">Ottenere i pulsanti del mouse.</span><span class="sxs-lookup"><span data-stu-id="cc862-195">Get mouse buttons.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-196">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-196">Prototype</span></span>

```c
UINT ux_host_class_hid_mouse_buttons_get(
    UX_HOST_CLASS_HID_MOUSE *mouse_instance,
    ULONG *mouse_buttons);
```

### <a name="description"></a><span data-ttu-id="cc862-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-197">Description</span></span>

<span data-ttu-id="cc862-198">Questa funzione viene utilizzata per ottenere i pulsanti del mouse</span><span class="sxs-lookup"><span data-stu-id="cc862-198">This function is used to get the mouse buttons</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-199">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-199">Parameters</span></span>

- <span data-ttu-id="cc862-200">**mouse_instance** Puntatore all'istanza del mouse HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-200">**mouse_instance** Pointer to the HID mouse instance.</span></span>
- <span data-ttu-id="cc862-201">**mouse_buttons** Puntatore ai pulsanti restituiti.</span><span class="sxs-lookup"><span data-stu-id="cc862-201">**mouse_buttons** Pointer to the return buttons.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-202">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-202">Return Values</span></span>

- <span data-ttu-id="cc862-203">Il pulsante del mouse **UX_SUCCESS** (0x00) è stato recuperato.</span><span class="sxs-lookup"><span data-stu-id="cc862-203">**UX_SUCCESS** (0x00) Mouse button successfully retrieved.</span></span>
- <span data-ttu-id="cc862-204">L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.</span><span class="sxs-lookup"><span data-stu-id="cc862-204">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="cc862-205">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-205">Example</span></span>

```c
/* The following example illustrates how to obtain mouse buttons. */

UX_HOST_CLASS_HID_MOUSE *mouse_instance;

ULONG mouse_buttons;

status = ux_host_class_hid_mouse_button_get(mouse_instance, &mouse_buttons);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_mouse_position_get"></a><span data-ttu-id="cc862-206">ux_host_class_hid_mouse_position_get</span><span class="sxs-lookup"><span data-stu-id="cc862-206">ux_host_class_hid_mouse_position_get</span></span>

<span data-ttu-id="cc862-207">Ottiene la posizione del mouse.</span><span class="sxs-lookup"><span data-stu-id="cc862-207">Get mouse position.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-208">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-208">Prototype</span></span>

```c
UINT ux_host_class_hid_mouse_position_get(
    UX_HOST_CLASS_HID_MOUSE *mouse_instance,
    SLONG *mouse_x_position, 
    SLONG *mouse_y_position);
```

### <a name="description"></a><span data-ttu-id="cc862-209">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-209">Description</span></span>

<span data-ttu-id="cc862-210">Questa funzione viene utilizzata per ottenere la posizione del mouse in coordinate x & y.</span><span class="sxs-lookup"><span data-stu-id="cc862-210">This function is used to get the mouse position in x & y coordinates.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-211">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-211">Parameters</span></span>

- <span data-ttu-id="cc862-212">**mouse_instance** Puntatore all'istanza del mouse HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-212">**mouse_instance** Pointer to the HID mouse instance.</span></span>
- <span data-ttu-id="cc862-213">**mouse_x_position** Puntatore alla coordinata x.</span><span class="sxs-lookup"><span data-stu-id="cc862-213">**mouse_x_position** Pointer to the x coordinate.</span></span>
- <span data-ttu-id="cc862-214">**mouse_y_position** Puntatore alla coordinata y.</span><span class="sxs-lookup"><span data-stu-id="cc862-214">**mouse_y_position** Pointer to the y coordinate.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-215">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-215">Return Values</span></span>

- <span data-ttu-id="cc862-216">Sono state recuperate le coordinate di **UX_SUCCESS** (0x00) X &amp; Y.</span><span class="sxs-lookup"><span data-stu-id="cc862-216">**UX_SUCCESS** (0x00) X &amp; Y coordinates successfully retrieved.</span></span>
- <span data-ttu-id="cc862-217">L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.</span><span class="sxs-lookup"><span data-stu-id="cc862-217">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="cc862-218">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-218">Example</span></span>

```c
/* The following example illustrates how to obtain mouse coordinates. */

UX_HOST_CLASS_HID_MOUSE *mouse_instance;

SLONG mouse_x_position;
SLONG mouse_y_position;

status = ux_host_class_hid_mouse_position_get(mouse_instance,
    &mouse_x_position, &mouse_y_position);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_keyboard_key_get"></a><span data-ttu-id="cc862-219">ux_host_class_hid_keyboard_key_get</span><span class="sxs-lookup"><span data-stu-id="cc862-219">ux_host_class_hid_keyboard_key_get</span></span>

<span data-ttu-id="cc862-220">Ottenere la chiave e lo stato della tastiera.</span><span class="sxs-lookup"><span data-stu-id="cc862-220">Get keyboard key and state.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-221">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-221">Prototype</span></span>

```c
UINT ux_host_class_hid_keyboard_key_get(
    UX_HOST_CLASS_HID_KEYBOARD *keyboard_instance,
    ULONG *keyboard_key, 
    ULONG *keyboard_state);
```

### <a name="description"></a><span data-ttu-id="cc862-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-222">Description</span></span>

<span data-ttu-id="cc862-223">Questa funzione viene usata per ottenere il tasto e lo stato della tastiera.</span><span class="sxs-lookup"><span data-stu-id="cc862-223">This function is used to get the keyboard key and state.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-224">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-224">Parameters</span></span>

- <span data-ttu-id="cc862-225">**keyboard_instance** Puntatore all'istanza della tastiera HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-225">**keyboard_instance** Pointer to the HID keyboard instance.</span></span>
- <span data-ttu-id="cc862-226">**keyboard_key** Puntatore al contenitore di tasti della tastiera.</span><span class="sxs-lookup"><span data-stu-id="cc862-226">**keyboard_key** Pointer to keyboard key container.</span></span>
- <span data-ttu-id="cc862-227">**keyboard_state** Puntatore al contenitore dello stato della tastiera.</span><span class="sxs-lookup"><span data-stu-id="cc862-227">**keyboard_state** Pointer to the keyboard state container.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-228">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-228">Return Values</span></span>

- <span data-ttu-id="cc862-229">La chiave e lo stato di **UX_SUCCESS** (0x00) sono stati recuperati correttamente.</span><span class="sxs-lookup"><span data-stu-id="cc862-229">**UX_SUCCESS** (0x00) Key and state successfully retrieved.</span></span>
- <span data-ttu-id="cc862-230">**UX_ERROR** (0Xff) nulla da segnalare.</span><span class="sxs-lookup"><span data-stu-id="cc862-230">**UX_ERROR** (0xff) Nothing to report.</span></span>
- <span data-ttu-id="cc862-231">L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.</span><span class="sxs-lookup"><span data-stu-id="cc862-231">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>

<span data-ttu-id="cc862-232">Lo stato della tastiera può includere i valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="cc862-232">The keyboard state can have the following values.</span></span>

- <span data-ttu-id="cc862-233">**UX_HID_KEYBOARD_STATE_KEY_UP** 0x10000</span><span class="sxs-lookup"><span data-stu-id="cc862-233">**UX_HID_KEYBOARD_STATE_KEY_UP** 0x10000</span></span>
- <span data-ttu-id="cc862-234">**UX_HID_KEYBOARD_STATE_NUM_LOCK** 0x0001</span><span class="sxs-lookup"><span data-stu-id="cc862-234">**UX_HID_KEYBOARD_STATE_NUM_LOCK** 0x0001</span></span>
- <span data-ttu-id="cc862-235">**UX_HID_KEYBOARD_STATE_CAPS_LOCK** 0x0002</span><span class="sxs-lookup"><span data-stu-id="cc862-235">**UX_HID_KEYBOARD_STATE_CAPS_LOCK** 0x0002</span></span>
- <span data-ttu-id="cc862-236">**UX_HID_KEYBOARD_STATE_SCROLL_LOCK** 0x0004</span><span class="sxs-lookup"><span data-stu-id="cc862-236">**UX_HID_KEYBOARD_STATE_SCROLL_LOCK** 0x0004</span></span>
- <span data-ttu-id="cc862-237">**UX_HID_KEYBOARD_STATE_MASK_LOCK** 0x0007</span><span class="sxs-lookup"><span data-stu-id="cc862-237">**UX_HID_KEYBOARD_STATE_MASK_LOCK** 0x0007</span></span>
- <span data-ttu-id="cc862-238">**UX_HID_KEYBOARD_STATE_LEFT_SHIFT** 0x0100</span><span class="sxs-lookup"><span data-stu-id="cc862-238">**UX_HID_KEYBOARD_STATE_LEFT_SHIFT** 0x0100</span></span>
- <span data-ttu-id="cc862-239">**UX_HID_KEYBOARD_STATE_RIGHT_SHIFT** 0x0200</span><span class="sxs-lookup"><span data-stu-id="cc862-239">**UX_HID_KEYBOARD_STATE_RIGHT_SHIFT** 0x0200</span></span>
- <span data-ttu-id="cc862-240">**UX_HID_KEYBOARD_STATE_SHIFT** 0x0300</span><span class="sxs-lookup"><span data-stu-id="cc862-240">**UX_HID_KEYBOARD_STATE_SHIFT** 0x0300</span></span>
- <span data-ttu-id="cc862-241">**UX_HID_KEYBOARD_STATE_LEFT_ALT** 0x0400</span><span class="sxs-lookup"><span data-stu-id="cc862-241">**UX_HID_KEYBOARD_STATE_LEFT_ALT** 0x0400</span></span>
- <span data-ttu-id="cc862-242">**UX_HID_KEYBOARD_STATE_RIGHT_ALT** 0x0800</span><span class="sxs-lookup"><span data-stu-id="cc862-242">**UX_HID_KEYBOARD_STATE_RIGHT_ALT** 0x0800</span></span>
- <span data-ttu-id="cc862-243">**UX_HID_KEYBOARD_STATE_ALT** 0x0A00</span><span class="sxs-lookup"><span data-stu-id="cc862-243">**UX_HID_KEYBOARD_STATE_ALT** 0x0a00</span></span>
- <span data-ttu-id="cc862-244">**UX_HID_KEYBOARD_STATE_LEFT_CTRL** 0x1000</span><span class="sxs-lookup"><span data-stu-id="cc862-244">**UX_HID_KEYBOARD_STATE_LEFT_CTRL** 0x1000</span></span>
- <span data-ttu-id="cc862-245">**UX_HID_KEYBOARD_STATE_RIGHT_CTRL** 0x2000</span><span class="sxs-lookup"><span data-stu-id="cc862-245">**UX_HID_KEYBOARD_STATE_RIGHT_CTRL** 0x2000</span></span>
- <span data-ttu-id="cc862-246">**UX_HID_KEYBOARD_STATE_CTRL** 0x3000</span><span class="sxs-lookup"><span data-stu-id="cc862-246">**UX_HID_KEYBOARD_STATE_CTRL** 0x3000</span></span>
- <span data-ttu-id="cc862-247">**UX_HID_KEYBOARD_STATE_LEFT_GUI** 0x4000</span><span class="sxs-lookup"><span data-stu-id="cc862-247">**UX_HID_KEYBOARD_STATE_LEFT_GUI** 0x4000</span></span>
- <span data-ttu-id="cc862-248">**UX_HID_KEYBOARD_STATE_RIGHT_GUI** 0x8000</span><span class="sxs-lookup"><span data-stu-id="cc862-248">**UX_HID_KEYBOARD_STATE_RIGHT_GUI** 0x8000</span></span>
- <span data-ttu-id="cc862-249">**UX_HID_KEYBOARD_STATE_GUI** 0xA000</span><span class="sxs-lookup"><span data-stu-id="cc862-249">**UX_HID_KEYBOARD_STATE_GUI** 0xa000</span></span>

### <a name="example"></a><span data-ttu-id="cc862-250">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-250">Example</span></span>

```c
while (1)
{

    /* Get a key/state from the keyboard. */
    status = ux_host_class_hid_keyboard_key_get(keyboard,
        &keyboard_char, &keyboard_state);

    /* Check if there is something. */
    if (status == UX_SUCCESS)
    {

        #ifdef UX_HOST_CLASS_HID_KEYBOARD_EVENTS_KEY_CHANGES_MODE
            if (keyboard_state & UX_HID_KEYBOARD_STATE_KEY_UP)
            {
                /* The key was released. */
            } else
            {
                /* The key was pressed. */
            }
        #endif

        /* We have a character in the queue. */
        keyboard_queue[keyboard_queue_index] = (UCHAR) keyboard_char;

        /* Can we accept more ? */
        if(keyboard_queue_index < 1024)
            keyboard_queue_index++;
    }

    tx_thread_sleep(10);

}
```

## <a name="ux_host_class_hid_keyboard_ioctl"></a><span data-ttu-id="cc862-251">ux_host_class_hid_keyboard_ioctl</span><span class="sxs-lookup"><span data-stu-id="cc862-251">ux_host_class_hid_keyboard_ioctl</span></span>

<span data-ttu-id="cc862-252">Eseguire una funzione IOCTL sulla tastiera HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-252">Perform an IOCTL function to the HID keyboard.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-253">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-253">Prototype</span></span>

```c
UINT ux_host_class_hid_keyboard_ioctl(
    UX_HOST_CLASS_HID_KEYBOARD *keyboard_instance,
    ULONG ioctl_function, VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="cc862-254">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-254">Description</span></span>

<span data-ttu-id="cc862-255">Questa funzione esegue una specifica funzione IOCTL sulla tastiera HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-255">This function performs a specific ioctl function to the HID keyboard.</span></span> <span data-ttu-id="cc862-256">La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il comando viene completato.</span><span class="sxs-lookup"><span data-stu-id="cc862-256">The call is blocking and only returns when there is either an error or when the command is completed.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-257">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-257">Parameters</span></span>

- <span data-ttu-id="cc862-258">**keyboard_instance** Puntatore all'istanza della tastiera HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-258">**keyboard_instance** Pointer to the HID keyboard instance.</span></span>
- <span data-ttu-id="cc862-259">**ioctl_function** funzione IOCTL da eseguire.</span><span class="sxs-lookup"><span data-stu-id="cc862-259">**ioctl_function** ioctl function to be performed.</span></span> <span data-ttu-id="cc862-260">Vedere la tabella seguente per una delle funzioni IOCTL consentite.</span><span class="sxs-lookup"><span data-stu-id="cc862-260">See table below for one of the allowed ioctl functions.</span></span>
- <span data-ttu-id="cc862-261">**parametro** di Puntatore a un parametro specifico del comando IOCTL.</span><span class="sxs-lookup"><span data-stu-id="cc862-261">**parameter** Pointer to a parameter specific to the ioctl.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-262">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-262">Return Values</span></span>

- <span data-ttu-id="cc862-263">**UX_SUCCESS** (0x00) la funzione IOCTL è stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="cc862-263">**UX_SUCCESS** (0x00) The ioctl function completed successfully.</span></span>
- <span data-ttu-id="cc862-264">**UX_FUNCTION_NOT_SUPPORTED** (0x54) funzione IOCTL sconosciuta</span><span class="sxs-lookup"><span data-stu-id="cc862-264">**UX_FUNCTION_NOT_SUPPORTED** (0x54) Unknown IOCTL function</span></span>

### <a name="ioctl-functions"></a><span data-ttu-id="cc862-265">Funzioni IOCTL</span><span class="sxs-lookup"><span data-stu-id="cc862-265">IOCTL functions</span></span>

- <span data-ttu-id="cc862-266">UX_HID_KEYBOARD_IOCTL_SET_LAYOUT</span><span class="sxs-lookup"><span data-stu-id="cc862-266">UX_HID_KEYBOARD_IOCTL_SET_LAYOUT</span></span>
- <span data-ttu-id="cc862-267">UX_HID_KEYBOARD_IOCTL_KEY_DECODING_ENABLE</span><span class="sxs-lookup"><span data-stu-id="cc862-267">UX_HID_KEYBOARD_IOCTL_KEY_DECODING_ENABLE</span></span>
- <span data-ttu-id="cc862-268">UX_HID_KEYBOARD_IOCTL_KEY_DECODING_DISABLE</span><span class="sxs-lookup"><span data-stu-id="cc862-268">UX_HID_KEYBOARD_IOCTL_KEY_DECODING_DISABLE</span></span>

### <a name="example--change-keyboard-layout"></a><span data-ttu-id="cc862-269">Esempio: modificare il layout della tastiera</span><span class="sxs-lookup"><span data-stu-id="cc862-269">Example – change keyboard layout</span></span>

```c
UINT status;

/* This example shows usage of the SET_LAYOUT IOCTL function.
    USBX receives raw key values from the device (these raw values
    are defined in the HID usage table specification) and optionally
    decodes them for application usage. The decoding is performed
    based on a set of arrays that act as maps – which array is used
    depends on the raw key value (i.e. keypad and non-keypad) and
    the current state of the keyboard (i.e. shift, caps lock, etc.). */

/* When the shift condition is not present and the raw key value
    is not within the keypad value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_unshifted_map[] =
{
    0,0,0,0,
    'a','b','c','d','e','f','g',
    'h','i','j','k','l','m','n',
    'o','p','q','r','s','t',
    'u','v','w','x','y','z',
    '1','2','3','4','5','6','7','8','9','0',
    0x0d,0x1b,0x08,0x07,0x20,'-','=','[',']',
    '\\','#',';',0x27,'`',',','.','/',0xf0,
    0xbb,0xbc,0xbd,0xbe,0xbf,0xc0,0xc1,0xc2,0xc3,0xc4,0xc5,0xc6,
    0x00,0xf1,0x00,0xd2,0xc7,0xc9,0xd3,0xcf,0xd1,0xcd,0xcd,0xd0,0xc8,0xf2,
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
    0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
};

/* When the shift condition is present and the raw key value
    is not within the keypad value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_shifted_map[] =
{
    0,0,0,0,
    'A','B','C','D','E','F','G',
    'H','I','J','K','L','M','N',
    'O','P','Q','R','S','T',
    'U','V','W','X','Y','Z',
    '!','@','#','$','%','^','&','*','(',')',
    0x0d,0x1b,0x08,0x07,0x20,'_','+','{','}',
    '|','~',':','"','~','<','>','?',0xf0,
    0xbb,0xbc,0xbd,0xbe,0xbf,0xc0,0xc1,0xc2,0xc3,0xc4,0xc5,0xc6,
    0x00,0xf1,0x00,0xd2,0xc7,0xc9,0xd3,0xcf,0xd1,0xcd,0xcd,0xd0,0xc8,0xf2,
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
    0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,
};

/* When numlock is on and the raw key value is within the keypad
    value range, this array will be used to decode the raw key value. */

static UCHAR keyboard_layout_raw_to_numlock_on_map[] =
{
    '/','*','-','+',
    0x0d,'1','2','3','4','5','6','7','8','9','0','.','\\',0x00,0x00,'=',
};

/* When numlock is off and the raw key value is within the keypad value
    range, this array will be used to decode the raw key value. */
static UCHAR keyboard_layout_raw_to_numlock_off_map[] =
{
    '/','*','-','+',
    0x0d,0xcf,0xd0,0xd1,0xcb,'5',0xcd,0xc7,0xc8,0xc9,0xd2,0xd3,'\\',0x00,0x
    00,'=',
};

/* Specify the keyboard layout for USBX usage. */
static UX_HOST_CLASS_HID_KEYBOARD_LAYOUT keyboard_layout =
{
    keyboard_layout_raw_to_shifted_map,
    keyboard_layout_raw_to_unshifted_map,
    keyboard_layout_raw_to_numlock_on_map,
    keyboard_layout_raw_to_numlock_off_map,
    /* The maximum raw key value. Values larger than this are discarded. */
    UX_HID_KEYBOARD_KEYS_UPPER_RANGE,
    /* The raw key value for the letter 'a'. */
    UX_HID_KEYBOARD_KEY_LETTER_A,
    /* The raw key value for the letter 'z'. */
    UX_HID_KEYBOARD_KEY_LETTER_Z,
    /* The lower range raw key value for keypad keys - inclusive. */
    UX_HID_KEYBOARD_KEYS_KEYPAD_LOWER_RANGE,
    /* The upper range raw key value for keypad keys. */
    UX_HID_KEYBOARD_KEYS_KEYPAD_UPPER_RANGE
};

/* Call the IOCTL function to change the keyboard layout. */
status = ux_host_class_hid_keyboard_ioctl(keyboard,
    UX_HID_KEYBOARD_IOCTL_SET_LAYOUT, (VOID *)&keyboard_layout);

/* If status equals UX_SUCCESS, the operation was successful. */
```

### <a name="example--disable-keyboard-key-decode"></a><span data-ttu-id="cc862-270">Esempio: disabilitare la decodifica del tasto tastiera</span><span class="sxs-lookup"><span data-stu-id="cc862-270">Example – disable keyboard key decode</span></span>

```c
UINT status;

/* The following example illustrates IOCTL function of Disable key decode from keyboard layout. */
status = ux_host_class_hid_keyboard_ioctl(keyboard,
    UX_HID_KEYBOARD_IOCTL_DISABLE_KEYS_DECODE, UX_NULL);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_hid_remote_control_usage_get"></a><span data-ttu-id="cc862-271">ux_host_class_hid_remote_control_usage_get</span><span class="sxs-lookup"><span data-stu-id="cc862-271">ux_host_class_hid_remote_control_usage_get</span></span>

<span data-ttu-id="cc862-272">Ottenere l'utilizzo del controllo remoto</span><span class="sxs-lookup"><span data-stu-id="cc862-272">Get remote control usage</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-273">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-273">Prototype</span></span>

```c
UINT ux_host_class_hid_remote_control_usage_get(
    UX_HOST_CLASS_HID_REMOTE_CONTROL *remote_control_instance,
    LONG *usage, 
    ULONG *value);
```

### <a name="description"></a><span data-ttu-id="cc862-274">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-274">Description</span></span>

<span data-ttu-id="cc862-275">Questa funzione viene usata per ottenere gli utilizzi del controllo remoto.</span><span class="sxs-lookup"><span data-stu-id="cc862-275">This function is used to get the remote control usages.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-276">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-276">Parameters</span></span>

- <span data-ttu-id="cc862-277">**remote_control_instance** Puntatore all'istanza di controllo remoto HID.</span><span class="sxs-lookup"><span data-stu-id="cc862-277">**remote_control_instance** Pointer to the HID remote control instance.</span></span>
- <span data-ttu-id="cc862-278">**utilizzo** di Puntatore all'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="cc862-278">**usage** Pointer to the usage.</span></span>
- <span data-ttu-id="cc862-279">**valore** di Puntatore al valore per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="cc862-279">**value** Pointer to the value for the usage.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-280">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-280">Return Values</span></span>

- <span data-ttu-id="cc862-281">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="cc862-281">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="cc862-282">**UX_ERROR** (0Xff) nulla da segnalare.</span><span class="sxs-lookup"><span data-stu-id="cc862-282">**UX_ERROR** (0xff) Nothing to report.</span></span>
- <span data-ttu-id="cc862-283">L'istanza della classe HID **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non esiste.</span><span class="sxs-lookup"><span data-stu-id="cc862-283">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) HID class instance does not exist.</span></span>

<span data-ttu-id="cc862-284">L'elenco di tutti gli utilizzi possibili è troppo lungo per questo manuale dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cc862-284">The list of all possible usages is too long to fit in this user guide.</span></span> <span data-ttu-id="cc862-285">Per una descrizione completa, il ux_host_class_hid. h include l'intero set di valori possibili.</span><span class="sxs-lookup"><span data-stu-id="cc862-285">For a full description, the ux_host_class_hid.h has the entire set of possible values.</span></span>

### <a name="example"></a><span data-ttu-id="cc862-286">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-286">Example</span></span>

```c
/* Read usages and values as the user changes the vol/bass/treble buttons on the speaker */

while (remote_control != UX_NULL)
{
    status = ux_host_class_hid_remote_control_usage_get(remote_control, &usage, &value);
    if (status == UX_SUCCESS)
    {
        /* We have something coming from the HID remote control,
        we filter the usage here and only allow the
        volume usage which can be VOLUME, VOLUME_INCREMENT or VOLUME_DECREMENT */
        switch(usage)
        {
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME :
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME_INCREMENT :
            case UX_HOST_CLASS_HID_CONSUMER_VOLUME_DECREMENT :

            if (value<0x80)
            {
                if (current_volume + audio_control.ux_host_class_audio_control_res < 0xffff)
                    current_volume = current_volume + audio_control.ux_host_class_audio_control_res;
                } else {
                if (current_volume > audio_control.ux_host_class_audio_control_res)
                    current_volume = current_volumeaudio_control.ux_host_class_audio_control_res;
            }

            audio_control.ux_host_class_audio_control_channel = 1;
            audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
            audio_control.ux_host_class_audio_control_cur = current_volume;
            status = ux_host_class_audio_control_value_set(audio, &audio_control);
            audio_control.ux_host_class_audio_control_channel = 2;
            audio_control.ux_host_class_audio_control = UX_HOST_CLASS_AUDIO_VOLUME_CONTROL;
            audio_control.ux_host_class_audio_control_cur = current_volume;
            status = ux_host_class_audio_control_value_set(audio, &audio_control);
            break;

        }
    }
    tx_thread_sleep(10);

}
```

### <a name="ux_host_class_cdc_acm_read"></a><span data-ttu-id="cc862-287">ux_host_class_cdc_acm_read</span><span class="sxs-lookup"><span data-stu-id="cc862-287">ux_host_class_cdc_acm_read</span></span>

<span data-ttu-id="cc862-288">Leggere dall'interfaccia cdc_acm.</span><span class="sxs-lookup"><span data-stu-id="cc862-288">Read from the cdc_acm interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-289">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-289">Prototype</span></span>

```c
UINT ux_host_class_cdc_acm_read(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UCHAR *data_pointer,
    ULONG requested_length,
    ULONG *actual_length);
```

### <a name="description"></a><span data-ttu-id="cc862-290">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-290">Description</span></span>

<span data-ttu-id="cc862-291">Questa funzione legge dall'interfaccia cdc_acm.</span><span class="sxs-lookup"><span data-stu-id="cc862-291">This function reads from the cdc_acm interface.</span></span> <span data-ttu-id="cc862-292">La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.</span><span class="sxs-lookup"><span data-stu-id="cc862-292">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-293">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-293">Parameters</span></span>

- <span data-ttu-id="cc862-294">**cdc_acm** Puntatore all'istanza della classe cdc_acm.</span><span class="sxs-lookup"><span data-stu-id="cc862-294">**cdc_acm** Pointer to the cdc_acm class instance.</span></span>
- <span data-ttu-id="cc862-295">**data_pointer** Puntatore all'indirizzo del buffer del payload di dati.</span><span class="sxs-lookup"><span data-stu-id="cc862-295">**data_pointer** Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="cc862-296">**requested_length** Lunghezza da ricevere.</span><span class="sxs-lookup"><span data-stu-id="cc862-296">**requested_length** Length to be received.</span></span>
- <span data-ttu-id="cc862-297">**actual_length** Lunghezza effettivamente ricevuta.</span><span class="sxs-lookup"><span data-stu-id="cc862-297">**actual_length** Length actually received.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-298">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-298">Return Values</span></span>

- <span data-ttu-id="cc862-299">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="cc862-299">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="cc862-300">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5b) l'istanza di cdc_acm non è valida.</span><span class="sxs-lookup"><span data-stu-id="cc862-300">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) The cdc_acm instance is invalid.</span></span>
- <span data-ttu-id="cc862-301">TIMEOUT di trasferimento **UX_TRANSFER_TIMEOUT** (0x5c), lettura incompleta.</span><span class="sxs-lookup"><span data-stu-id="cc862-301">**UX_TRANSFER_TIMEOUT** (0x5c) Transfer timeout, reading incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="cc862-302">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-302">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_read(cdc_acm, data_pointer,
    requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_write"></a><span data-ttu-id="cc862-303">ux_host_class_cdc_acm_write</span><span class="sxs-lookup"><span data-stu-id="cc862-303">ux_host_class_cdc_acm_write</span></span>

<span data-ttu-id="cc862-304">Scrivere nell'interfaccia cdc_acm</span><span class="sxs-lookup"><span data-stu-id="cc862-304">Write to the cdc_acm interface</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-305">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-305">Prototype</span></span>

```c
UINT ux_host_class_cdc_acm_write(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UCHAR *data_pointer, 
    ULONG requested_length, 
    ULONG *actual_length);
```

### <a name="description"></a><span data-ttu-id="cc862-306">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-306">Description</span></span>

<span data-ttu-id="cc862-307">Questa funzione scrive nell'interfaccia cdc_acm.</span><span class="sxs-lookup"><span data-stu-id="cc862-307">This function writes to the cdc_acm interface.</span></span> <span data-ttu-id="cc862-308">La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il trasferimento è completo.</span><span class="sxs-lookup"><span data-stu-id="cc862-308">The call is blocking and only returns when there is either an error or when the transfer is complete.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-309">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-309">Parameters</span></span>

- <span data-ttu-id="cc862-310">**cdc_acm** Puntatore all'istanza della classe cdc_acm.</span><span class="sxs-lookup"><span data-stu-id="cc862-310">**cdc_acm** Pointer to the cdc_acm class instance.</span></span>
- <span data-ttu-id="cc862-311">**data_pointer** Puntatore all'indirizzo del buffer del payload di dati.</span><span class="sxs-lookup"><span data-stu-id="cc862-311">**data_pointer** Pointer to the buffer address of the data payload.</span></span>
- <span data-ttu-id="cc862-312">**requested_length** Lunghezza da inviare.</span><span class="sxs-lookup"><span data-stu-id="cc862-312">**requested_length** Length to be sent.</span></span>
- <span data-ttu-id="cc862-313">**actual_length** Lunghezza effettivamente inviata.</span><span class="sxs-lookup"><span data-stu-id="cc862-313">**actual_length** Length actually sent.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc862-314">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="cc862-314">Return Values</span></span>

- <span data-ttu-id="cc862-315">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="cc862-315">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="cc862-316">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5b) l'istanza di cdc_acm non è valida.</span><span class="sxs-lookup"><span data-stu-id="cc862-316">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) The cdc_acm instance is invalid.</span></span>
- <span data-ttu-id="cc862-317">TIMEOUT di trasferimento **UX_TRANSFER_TIMEOUT** (0x5c), scrittura incompleta.</span><span class="sxs-lookup"><span data-stu-id="cc862-317">**UX_TRANSFER_TIMEOUT** (0x5c) Transfer timeout, writing incomplete.</span></span>

### <a name="example"></a><span data-ttu-id="cc862-318">Esempio</span><span class="sxs-lookup"><span data-stu-id="cc862-318">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_write(cdc_acm, data_pointer,
    requested_length, &actual_length);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_ioctl"></a><span data-ttu-id="cc862-319">ux_host_class_cdc_acm_ioctl</span><span class="sxs-lookup"><span data-stu-id="cc862-319">ux_host_class_cdc_acm_ioctl</span></span>

<span data-ttu-id="cc862-320">Eseguire una funzione IOCTL nell'interfaccia cdc_acm.</span><span class="sxs-lookup"><span data-stu-id="cc862-320">Perform an IOCTL function to the cdc_acm interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-321">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-321">Prototype</span></span>

```c
UINT ux_host_class_cdc_acm_ioctl(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    ULONG ioctl_function, 
    VOID *parameter);
```

### <a name="description"></a><span data-ttu-id="cc862-322">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-322">Description</span></span>

<span data-ttu-id="cc862-323">Questa funzione esegue una specifica funzione IOCTL nell'interfaccia cdc_acm.</span><span class="sxs-lookup"><span data-stu-id="cc862-323">This function performs a specific ioctl function to the cdc_acm interface.</span></span> <span data-ttu-id="cc862-324">La chiamata è bloccata e restituisce solo quando si verifica un errore o quando il comando viene completato.</span><span class="sxs-lookup"><span data-stu-id="cc862-324">The call is blocking and only returns when there is either an error or when the command is completed.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-325">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-325">Parameters</span></span>

- <span data-ttu-id="cc862-326">**cdc_acm** Puntatore all'istanza della classe cdc_acm.</span><span class="sxs-lookup"><span data-stu-id="cc862-326">**cdc_acm** Pointer to the cdc_acm class instance.</span></span>
- <span data-ttu-id="cc862-327">**ioctl_function** funzione IOCTL da eseguire.</span><span class="sxs-lookup"><span data-stu-id="cc862-327">**ioctl_function** ioctl function to be performed.</span></span> <span data-ttu-id="cc862-328">Vedere la tabella seguente per una delle funzioni IOCTL consentite.</span><span class="sxs-lookup"><span data-stu-id="cc862-328">See table below for one of the allowed ioctl functions.</span></span>
- <span data-ttu-id="cc862-329">**parametro** di Puntatore a un parametro specifico di IOCTL</span><span class="sxs-lookup"><span data-stu-id="cc862-329">**parameter** Pointer to a parameter specific to the ioctl</span></span>

### <a name="return-value"></a><span data-ttu-id="cc862-330">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="cc862-330">Return Value</span></span>

- <span data-ttu-id="cc862-331">**UX_SUCCESS** (0x00) il trasferimento dei dati è stato completato.</span><span class="sxs-lookup"><span data-stu-id="cc862-331">**UX_SUCCESS** (0x00) The data transfer was completed.</span></span>
- <span data-ttu-id="cc862-332">**UX_MEMORY_INSUFFICIENT** (0x12) memoria insufficiente.</span><span class="sxs-lookup"><span data-stu-id="cc862-332">**UX_MEMORY_INSUFFICIENT** (0x12) Not enough memory.</span></span>
- <span data-ttu-id="cc862-333">L'istanza di **UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5B) CDC-ACM è in uno stato non valido.</span><span class="sxs-lookup"><span data-stu-id="cc862-333">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) CDC-ACM instance is in an invalid state.</span></span>
- <span data-ttu-id="cc862-334">**UX_FUNCTION_NOT_SUPPORTED** (0x54) funzione IOCTL sconosciuta.</span><span class="sxs-lookup"><span data-stu-id="cc862-334">**UX_FUNCTION_NOT_SUPPORTED** (0x54) Unknown IOCTL function.</span></span>

### <a name="ioctl-functions"></a><span data-ttu-id="cc862-335">Funzioni IOCTL:</span><span class="sxs-lookup"><span data-stu-id="cc862-335">IOCTL functions:</span></span>

- <span data-ttu-id="cc862-336">UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="cc862-336">UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_CODING</span></span>
- <span data-ttu-id="cc862-337">UX_HOST_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span><span class="sxs-lookup"><span data-stu-id="cc862-337">UX_HOST_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING</span></span>
- <span data-ttu-id="cc862-338">UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span><span class="sxs-lookup"><span data-stu-id="cc862-338">UX_HOST_CLASS_CDC_ACM_IOCTL_SET_LINE_STATE</span></span>
- <span data-ttu-id="cc862-339">UX_HOST_CLASS_CDC_ACM_IOCTL_SEND_BREAK</span><span class="sxs-lookup"><span data-stu-id="cc862-339">UX_HOST_CLASS_CDC_ACM_IOCTL_SEND_BREAK</span></span>
- <span data-ttu-id="cc862-340">UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_IN_PIPE</span><span class="sxs-lookup"><span data-stu-id="cc862-340">UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_IN_PIPE</span></span>
- <span data-ttu-id="cc862-341">UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_OUT_PIPE</span><span class="sxs-lookup"><span data-stu-id="cc862-341">UX_HOST_CLASS_CDC_ACM_IOCTL_ABORT_OUT_PIPE</span></span>
- <span data-ttu-id="cc862-342">UX_HOST_CLASS_CDC_ACM_IOCTL_NOTIFICATION_CALLBACK</span><span class="sxs-lookup"><span data-stu-id="cc862-342">UX_HOST_CLASS_CDC_ACM_IOCTL_NOTIFICATION_CALLBACK</span></span>
- <span data-ttu-id="cc862-343">UX_HOST_CLASS_CDC_ACM_IOCTL_GET_DEVICE_STATUS</span><span class="sxs-lookup"><span data-stu-id="cc862-343">UX_HOST_CLASS_CDC_ACM_IOCTL_GET_DEVICE_STATUS</span></span>

```c
UINT status;

/* The following example illustrates this service. */

status = ux_host_class_cdc_acm_ioctl(cdc_acm,
    UX_HOST_CLASS_CDC_ACM_IOCTL_GET_LINE_CODING, (VOID *)&line_coding);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_class_cdc_acm_reception_start"></a><span data-ttu-id="cc862-344">ux_host_class_cdc_acm_reception_start</span><span class="sxs-lookup"><span data-stu-id="cc862-344">ux_host_class_cdc_acm_reception_start</span></span>

<span data-ttu-id="cc862-345">Inizia la ricezione in background dei dati dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cc862-345">Begins background reception of data from the device.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-346">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-346">Prototype</span></span>

```c
UINT ux_host_class_cdc_acm_reception_start(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UX_HOST_CLASS_CDC_ACM_RECEPTION *cdc_acm_reception);
```

### <a name="description"></a><span data-ttu-id="cc862-347">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-347">Description</span></span>

<span data-ttu-id="cc862-348">Questa funzione fa in modo che USBX legga continuamente i dati dal dispositivo in background.</span><span class="sxs-lookup"><span data-stu-id="cc862-348">This function causes USBX to continuously read data from the device in the background.</span></span> <span data-ttu-id="cc862-349">Al completamento di ogni transazione, viene richiamato il callback specificato in **cdc_acm_reception** , in modo che l'applicazione possa eseguire un'ulteriore elaborazione dei dati della transazione.</span><span class="sxs-lookup"><span data-stu-id="cc862-349">Upon completion of each transaction, the callback specified in **cdc_acm_reception** is invoked so the application may perform further processing of the transaction's data.</span></span>

> [!NOTE]
> <span data-ttu-id="cc862-350">non è necessario usare **ux_host_class_cdc_acm_read** mentre è in uso la ricezione in background.</span><span class="sxs-lookup"><span data-stu-id="cc862-350">**ux_host_class_cdc_acm_read** must not be used while background reception is in use.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-351">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-351">Parameters</span></span>

- <span data-ttu-id="cc862-352">**cdc_acm** Puntatore all'istanza della classe cdc_acm.</span><span class="sxs-lookup"><span data-stu-id="cc862-352">**cdc_acm** Pointer to the cdc_acm class instance.</span></span>
- <span data-ttu-id="cc862-353">**cdc_acm_reception** Puntatore al parametro che contiene i valori che definiscono il comportamento della ricezione in background.</span><span class="sxs-lookup"><span data-stu-id="cc862-353">**cdc_acm_reception** Pointer to parameter that contains values defining behavior of background reception.</span></span> <span data-ttu-id="cc862-354">Il layout di questo parametro è il seguente:</span><span class="sxs-lookup"><span data-stu-id="cc862-354">The layout of this parameter follows:</span></span>

```c
typedef struct UX_HOST_CLASS_CDC_ACM_RECEPTION_STRUCT
{
    ULONG ux_host_class_cdc_acm_reception_state;
    ULONG ux_host_class_cdc_acm_reception_block_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_buffer;
    ULONG ux_host_class_cdc_acm_reception_data_buffer_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_head;
    UCHAR *ux_host_class_cdc_acm_reception_data_tail;
    VOID (*ux_host_class_cdc_acm_reception_callback)(struct UX_HOST_CLASS_CDC_ACM_STRUCT *cdc_acm,
        UINT status, UCHAR *reception_buffer, ULONG reception_size);
} UX_HOST_CLASS_CDC_ACM_RECEPTION;
```

### <a name="return-value"></a><span data-ttu-id="cc862-355">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="cc862-355">Return Value</span></span>

- <span data-ttu-id="cc862-356">Ricezione in background **UX_SUCCESS** (0x00) avviata correttamente.</span><span class="sxs-lookup"><span data-stu-id="cc862-356">**UX_SUCCESS** (0x00) Background reception successfully started.</span></span>
- <span data-ttu-id="cc862-357">Istanza di classe non corretta **UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b).</span><span class="sxs-lookup"><span data-stu-id="cc862-357">**UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b) Wrong class instance.</span></span>

```c
UINT status;
UX_HOST_CLASS_CDC_ACM_RECEPTION cdc_acm_reception;

/* Setup the background reception parameter. */

/* Set the desired max read size for each transaction.
    For example, if this value is 64, then the maximum amount of
    data received from the device in a single transaction is 64.
    If the amount of data received from the device is less than this value,
    the callback will still be invoked with the actual amount of data received. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_block_size = block_size;

/* Set the buffer where the data from the device is read to. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_data_buffer = cdc_acm_reception_buffer;

/* Set the size of the data reception buffer.
    Note that this should be at least as large as ux_host_class_cdc_acm_reception_block_size. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_data_buffer_size = cdc_acm_reception_buffer_size;

/* Set the callback that is to be invoked upon each reception transfer completion. */
cdc_acm_reception.ux_host_class_cdc_acm_reception_callback = reception_callback;

/* Start background reception using the values we defined in the reception parameter. */
status = ux_host_class_cdc_acm_reception_start(cdc_acm_host_data, &cdc_acm_reception);

/* If status equals UX_SUCCESS, background reception has successfully started. */
```

## <a name="ux_host_class_cdc_acm_reception_stop"></a><span data-ttu-id="cc862-358">ux_host_class_cdc_acm_reception_stop</span><span class="sxs-lookup"><span data-stu-id="cc862-358">ux_host_class_cdc_acm_reception_stop</span></span>

<span data-ttu-id="cc862-359">Arresta la ricezione dei pacchetti in background.</span><span class="sxs-lookup"><span data-stu-id="cc862-359">Stops background reception of packets.</span></span>

### <a name="prototype"></a><span data-ttu-id="cc862-360">Prototipo</span><span class="sxs-lookup"><span data-stu-id="cc862-360">Prototype</span></span>

```c
UINT ux_host_class_cdc_acm_reception_stop(
    UX_HOST_CLASS_CDC_ACM *cdc_acm,
    UX_HOST_CLASS_CDC_ACM_RECEPTION *cdc_acm_reception);
```

### <a name="description"></a><span data-ttu-id="cc862-361">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cc862-361">Description</span></span>

<span data-ttu-id="cc862-362">Questa funzione fa in modo che USBX arresti la ricezione in background avviata in precedenza da **ux_host_class_cdc_acm_reception_start**.</span><span class="sxs-lookup"><span data-stu-id="cc862-362">This function causes USBX to stop background reception previously started by **ux_host_class_cdc_acm_reception_start**.</span></span>

### <a name="parameters"></a><span data-ttu-id="cc862-363">Parametri</span><span class="sxs-lookup"><span data-stu-id="cc862-363">Parameters</span></span>

- <span data-ttu-id="cc862-364">**cdc_acm** Puntatore all'istanza della classe cdc_acm.</span><span class="sxs-lookup"><span data-stu-id="cc862-364">**cdc_acm** Pointer to the cdc_acm class instance.</span></span>
- <span data-ttu-id="cc862-365">**cdc_acm_reception** Puntatore allo stesso parametro utilizzato per avviare la ricezione in background.</span><span class="sxs-lookup"><span data-stu-id="cc862-365">**cdc_acm_reception** Pointer to the same parameter that was used to start background reception.</span></span> <span data-ttu-id="cc862-366">Il layout di questo parametro è il seguente:</span><span class="sxs-lookup"><span data-stu-id="cc862-366">The layout of this parameter follows:</span></span>

```c
typedef struct UX_HOST_CLASS_CDC_ACM_RECEPTION_STRUCT
{
    ULONG ux_host_class_cdc_acm_reception_state;
    ULONG ux_host_class_cdc_acm_reception_block_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_buffer;
    ULONG ux_host_class_cdc_acm_reception_data_buffer_size;
    UCHAR *ux_host_class_cdc_acm_reception_data_head;
    UCHAR *ux_host_class_cdc_acm_reception_data_tail;
    VOID (*ux_host_class_cdc_acm_reception_callback)(
            struct UX_HOST_CLASS_CDC_ACM_STRUCT *cdc_acm, UINT status,
            UCHAR *reception_buffer, ULONG reception_size);
} UX_HOST_CLASS_CDC_ACM_RECEPTION;
```

### <a name="return-value"></a><span data-ttu-id="cc862-367">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="cc862-367">Return Value</span></span>

- <span data-ttu-id="cc862-368">La ricezione in background **UX_SUCCESS** (0x00) è stata arrestata.</span><span class="sxs-lookup"><span data-stu-id="cc862-368">**UX_SUCCESS** (0x00) Background reception successfully stopped.</span></span>
- <span data-ttu-id="cc862-369">Istanza di classe non corretta **UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b).</span><span class="sxs-lookup"><span data-stu-id="cc862-369">**UX_HOST_CLASS_INSTANCE _UNKNOWN** (0x5b) Wrong class instance.</span></span>

```c
UINT status;
UX_HOST_CLASS_CDC_ACM_RECEPTION cdc_acm_reception;

/* Stop background reception. The reception parameter should be the same
    that was passed to ux_host_class_cdc_acm_reception_start. */
status = ux_host_class_cdc_acm_reception_stop(cdc_acm, &cdc_acm_reception);

/* If status equals UX_SUCCESS, background reception has successfully stopped. */
```
