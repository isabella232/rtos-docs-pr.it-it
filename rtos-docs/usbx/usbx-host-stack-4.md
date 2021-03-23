---
title: Capitolo 4-Descrizione dei servizi host USBX
description: Informazioni sui servizi host USBX.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: d730658c07f3cd7cec8c75a47818314bdc63f35a
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824359"
---
# <a name="chapter-4---description-of-usbx-host-services"></a><span data-ttu-id="b7d90-103">Capitolo 4-Descrizione dei servizi host USBX</span><span class="sxs-lookup"><span data-stu-id="b7d90-103">Chapter 4 - Description of USBX Host Services</span></span>

## <a name="ux_host_stack_initialize"></a><span data-ttu-id="b7d90-104">ux_host_stack_initialize</span><span class="sxs-lookup"><span data-stu-id="b7d90-104">ux_host_stack_initialize</span></span>

<span data-ttu-id="b7d90-105">Inizializzare USBX per l'operazione host.</span><span class="sxs-lookup"><span data-stu-id="b7d90-105">Initialize USBX for host operation.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-106">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-106">Prototype</span></span>

```c
UINT ux_host_stack_initialize(
    UINT (*system_change_function)
    (ULONG, UX_HOST_CLASS *));
```

### <a name="description"></a><span data-ttu-id="b7d90-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-107">Description</span></span>

<span data-ttu-id="b7d90-108">Questa funzione Inizializza lo stack host USB.</span><span class="sxs-lookup"><span data-stu-id="b7d90-108">This function will initialize the USB host stack.</span></span> <span data-ttu-id="b7d90-109">L'area di memoria specificata verrà impostata per l'uso interno di USBX.</span><span class="sxs-lookup"><span data-stu-id="b7d90-109">The supplied memory area will be setup for USBX internal use.</span></span> <span data-ttu-id="b7d90-110">Se viene restituito UX_SUCCESS, USBX è pronto per il controller host e la registrazione della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-110">If UX_SUCCESS is returned, USBX is ready for host controller and class registration.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="b7d90-111">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="b7d90-111">Input Parameter</span></span>

- <span data-ttu-id="b7d90-112">**system_change_function** Puntatore alla routine di callback facoltativa per notificare l'applicazione delle modifiche del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b7d90-112">**system_change_function** Pointer to optional callback routine for notifying application of device changes.</span></span>

### <a name="return-value"></a><span data-ttu-id="b7d90-113">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="b7d90-113">Return Value</span></span>

- <span data-ttu-id="b7d90-114">**UX_SUCCESS** (0x00) inizializzazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="b7d90-114">**UX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="b7d90-115">**UX_MEMORY_INSUFFICIENT** (0X12) un'allocazione di memoria non riuscita.</span><span class="sxs-lookup"><span data-stu-id="b7d90-115">**UX_MEMORY_INSUFFICIENT** (0x12) A memory allocation failed.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-116">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-116">Example</span></span>

```c
UINT status;

/* Initialize USBX for host operation, without notification. */
status = ux_host_stack_initialize(UX_NULL);

/* If status equals UX_SUCCESS, USBX has been successfully initialized for host operation. */
```

## <a name="ux_host_stack_endpoint_transfer_abort"></a><span data-ttu-id="b7d90-117">ux_host_stack_endpoint_transfer_abort</span><span class="sxs-lookup"><span data-stu-id="b7d90-117">ux_host_stack_endpoint_transfer_abort</span></span>

<span data-ttu-id="b7d90-118">Interrompi tutte le transazioni associate a una richiesta di trasferimento per un endpoint.</span><span class="sxs-lookup"><span data-stu-id="b7d90-118">Abort all transactions attached to a transfer request for an endpoint.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-119">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-119">Prototype</span></span>

```c
UINT ux_host_stack_endpoint_transfer_abort(UX_ENDPOINT *endpoint);
```

### <a name="description"></a><span data-ttu-id="b7d90-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-120">Description</span></span>

<span data-ttu-id="b7d90-121">Questa funzione cancellerà tutte le transazioni attive o in sospeso per una richiesta di trasferimento specifica collegata a un endpoint.</span><span class="sxs-lookup"><span data-stu-id="b7d90-121">This function will cancel all transactions active or pending for a specific transfer request attached to an endpoint.</span></span> <span data-ttu-id="b7d90-122">La richiesta di trasferimento ha una funzione di callback collegata, la funzione di callback verrà chiamata con lo stato UX_TRANSACTION_ABORTED.</span><span class="sxs-lookup"><span data-stu-id="b7d90-122">It the transfer request has a callback function attached, the callback function will be called with the UX_TRANSACTION_ABORTED status.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="b7d90-123">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="b7d90-123">Input Parameter</span></span>

- <span data-ttu-id="b7d90-124">**endpoint** di Puntatore a un endpoint.</span><span class="sxs-lookup"><span data-stu-id="b7d90-124">**endpoint** Pointer to an endpoint.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-125">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-125">Return Values</span></span>

- <span data-ttu-id="b7d90-126">**UX_SUCCESS** (0x00) non sono presenti errori.</span><span class="sxs-lookup"><span data-stu-id="b7d90-126">**UX_SUCCESS** (0x00) No errors.</span></span>
- <span data-ttu-id="b7d90-127">HANDLE dell'endpoint **UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) non valido.</span><span class="sxs-lookup"><span data-stu-id="b7d90-127">**UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) Endpoint handle is not valid.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-128">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-128">Example</span></span>

```c
UX_HOST_CLASS_PRINTER *printer;
UINT status;

/* Get the instance for this class. */
printer = (UX_HOST_CLASS_PRINTER *) command ->
    ux_host_class_command_instance;

/* The printer is being shut down. */

printer -> printer_state = UX_HOST_CLASS_INSTANCE_SHUTDOWN;

/* We need to abort transactions on the bulk out pipe. */
status = ux_host_stack_endpoint_transfer_abort
    (printer -> printer_bulk_out_endpoint);

/* If status equals UX_SUCCESS, the operation was successful */
```

## <a name="ux_host_stack_class_get"></a><span data-ttu-id="b7d90-129">ux_host_stack_class_get</span><span class="sxs-lookup"><span data-stu-id="b7d90-129">ux_host_stack_class_get</span></span>

<span data-ttu-id="b7d90-130">Ottenere il puntatore a un contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-130">Get the pointer to a class container.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-131">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-131">Prototype</span></span>

```c
UINT ux_host_stack_class_get(
    UCHAR *class_name,
    UX_HOST_CLASS **class);
```

### <a name="description"></a><span data-ttu-id="b7d90-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-132">Description</span></span>

<span data-ttu-id="b7d90-133">Questa funzione restituisce un puntatore al contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-133">This function returns a pointer to the class container.</span></span> <span data-ttu-id="b7d90-134">Una classe deve ottenere il relativo contenitore dallo stack USB per cercare le istanze quando una classe o un'applicazione vuole aprire un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b7d90-134">A class needs to obtain its container from the USB stack to search for instances when a class or an application wants to open a device.</span></span>

> [!NOTE]
> <span data-ttu-id="b7d90-135">La stringa C di class_name deve essere con terminazione NULL e la lunghezza (senza il carattere di terminazione NULL) non deve essere maggiore di UX_MAX_CLASS_NAME_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="b7d90-135">The C string of class_name must be NULL-terminated and the length of it (without the NULL-terminator itself) must be no larger than UX_MAX_CLASS_NAME_LENGTH.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-136">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-136">Parameters</span></span>

- <span data-ttu-id="b7d90-137">**class_name** Puntatore al nome della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-137">**class_name** Pointer to the class name.</span></span>
- <span data-ttu-id="b7d90-138">**classe** Puntatore aggiornato dalla chiamata di funzione che contiene il contenitore della classe per il nome della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-138">**class** A pointer updated by the function call that contains the class container for the name of the class.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-139">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-139">Return Values</span></span>

- <span data-ttu-id="b7d90-140">**UX_SUCCESS** (0x00) nessun errore, al ritorno il campo della classe viene archiviato con il puntatore al contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-140">**UX_SUCCESS** (0x00) No errors, on return the class field is filed with the pointer to the class container.</span></span>
- <span data-ttu-id="b7d90-141">La classe **UX_HOST_CLASS_UNKNOWN** (0x59) è sconosciuta dallo stack.</span><span class="sxs-lookup"><span data-stu-id="b7d90-141">**UX_HOST_CLASS_UNKNOWN** (0x59) Class is unknown by the stack.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-142">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-142">Example</span></span>

```c
UX_HOST_CLASS *printer_container;
UINT status;

/* Get the container for this class. */
status = ux_host_stack_class_get("ux_host_class_printer", &printer_container);

/* If status equals UX_SUCCESS, the operation was successful */
```

## <a name="ux_host_stack_class_register"></a><span data-ttu-id="b7d90-143">ux_host_stack_class_register</span><span class="sxs-lookup"><span data-stu-id="b7d90-143">ux_host_stack_class_register</span></span>

<span data-ttu-id="b7d90-144">Registrare una classe USB nello stack USB.</span><span class="sxs-lookup"><span data-stu-id="b7d90-144">Register a USB class to the USB stack.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-145">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-145">Prototype</span></span>

```c
UINT ux_host_stack_class_register(
    UCHAR *class_name,
    UINT (*class_entry_address) (struct UX_HOST_CLASS_COMMAND_STRUCT *));
```

### <a name="description"></a><span data-ttu-id="b7d90-146">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-146">Description</span></span>

<span data-ttu-id="b7d90-147">Questa funzione registra una classe USB nello stack USB.</span><span class="sxs-lookup"><span data-stu-id="b7d90-147">This function registers a USB class to the USB stack.</span></span> <span data-ttu-id="b7d90-148">La classe deve specificare un punto di ingresso per lo stack USB per inviare comandi come il seguente.</span><span class="sxs-lookup"><span data-stu-id="b7d90-148">The class must specify an entry point for the USB stack to send commands such as the following.</span></span>

- <span data-ttu-id="b7d90-149">**UX_HOST_CLASS_COMMAND_QUERY**</span><span class="sxs-lookup"><span data-stu-id="b7d90-149">**UX_HOST_CLASS_COMMAND_QUERY**</span></span>
- <span data-ttu-id="b7d90-150">**UX_HOST_CLASS_COMMAND_ACTIVATE**</span><span class="sxs-lookup"><span data-stu-id="b7d90-150">**UX_HOST_CLASS_COMMAND_ACTIVATE**</span></span>
- <span data-ttu-id="b7d90-151">**UX_HOST_CLASS_COMMAND_DESTROY**</span><span class="sxs-lookup"><span data-stu-id="b7d90-151">**UX_HOST_CLASS_COMMAND_DESTROY**</span></span>

> [!NOTE]
> <span data-ttu-id="b7d90-152">La stringa C di *class_name* deve essere con terminazione null e la lunghezza (senza il carattere di terminazione null) non deve essere maggiore di **UX_MAX_CLASS_NAME_LENGTH**.</span><span class="sxs-lookup"><span data-stu-id="b7d90-152">The C string of *class_name* must be NULL-terminated and the length of it (without the NULL-terminator itself) must be no larger than **UX_MAX_CLASS_NAME_LENGTH**.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-153">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-153">Parameters</span></span>

- <span data-ttu-id="b7d90-154">**class_name** Puntatore al nome della classe, le voci valide si trovano nel file ux_system_initialize. c nelle classi USB di USBX.</span><span class="sxs-lookup"><span data-stu-id="b7d90-154">**class_name** Pointer to the name of the class, valid entries are found in the file ux_system_initialize.c under the USB Classes of USBX.</span></span>
- <span data-ttu-id="b7d90-155">**class_entry_address** Indirizzo della funzione entry della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-155">**class_entry_address** Address of the entry function of the class.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-156">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-156">Return Values</span></span>

- <span data-ttu-id="b7d90-157">Classe **UX_SUCCESS** (0x00) installata correttamente.</span><span class="sxs-lookup"><span data-stu-id="b7d90-157">**UX_SUCCESS** (0x00) Class installed successfully.</span></span>
- <span data-ttu-id="b7d90-158">**UX_MEMORY_ARRAY_FULL** (0X1a) non è più disponibile memoria per archiviare questa classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-158">**UX_MEMORY_ARRAY_FULL** (0x1a) No more memory to store this class.</span></span>
- <span data-ttu-id="b7d90-159">La classe host **UX_HOST_CLASS_ALREADY_INSTALLED** (0x58) è già installata.</span><span class="sxs-lookup"><span data-stu-id="b7d90-159">**UX_HOST_CLASS_ALREADY_INSTALLED** (0x58) Host class already installed.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-160">Esempio:</span><span class="sxs-lookup"><span data-stu-id="b7d90-160">Example:</span></span>

```c
UINT status;

/* Register all the classes for this implementation. */
status = ux_host_stack_class_register("ux_host_class_hub", ux_host_class_hub_entry);

/* If status equals UX_SUCCESS, class was successfully installed. */
```

## <a name="ux_host_stack_class_instance_create"></a><span data-ttu-id="b7d90-161">ux_host_stack_class_instance_create</span><span class="sxs-lookup"><span data-stu-id="b7d90-161">ux_host_stack_class_instance_create</span></span>

<span data-ttu-id="b7d90-162">Creare una nuova istanza della classe per un contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-162">Create a new class instance for a class container.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-163">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-163">Prototype</span></span>

```c
UINT ux_host_stack_class_instance_create(
    UX_HOST_CLASS *class, 
    VOID *class_instance);
```

### <a name="description"></a><span data-ttu-id="b7d90-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-164">Description</span></span>

<span data-ttu-id="b7d90-165">Questa funzione crea una nuova istanza della classe per un contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-165">This function creates a new class instance for a class container.</span></span> <span data-ttu-id="b7d90-166">L'istanza di una classe non è contenuta nel codice della classe per ridurre la complessità della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-166">The instance of a class is not contained in the class code to reduce the class complexity.</span></span> <span data-ttu-id="b7d90-167">Ogni istanza di classe è invece collegata al contenitore della classe presente nello stack principale.</span><span class="sxs-lookup"><span data-stu-id="b7d90-167">Rather, each class instance is attached to the class container located in the main stack.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-168">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-168">Parameters</span></span>

- <span data-ttu-id="b7d90-169">**classe** Puntatore al contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-169">**class** Pointer to the class container.</span></span>
- <span data-ttu-id="b7d90-170">**class_instance** Puntatore all'istanza della classe da creare.</span><span class="sxs-lookup"><span data-stu-id="b7d90-170">**class_instance** Pointer to the class instance to be created.</span></span>

### <a name="return-value"></a><span data-ttu-id="b7d90-171">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="b7d90-171">Return Value</span></span>

- <span data-ttu-id="b7d90-172">**UX_SUCCESS** (0x00) l'istanza della classe è stata collegata al contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-172">**UX_SUCCESS** (0x00) The class instance was attached to the class container.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-173">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-173">Example</span></span>

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* Obtain memory for this class instance. */

printer = ux_memory_allocate(UX_NO_ALIGN, sizeof(UX_HOST_CLASS_PRINTER));

if (printer == UX_NULL)
    return(UX_MEMORY_INSUFFICIENT);

/* Store the class container into this instance. */
printer -> printer_class = command -> ux_host_class;

/* Create this class instance. */
status = ux_host_stack_class_instance_create(printer -> printer_class, (VOID *)printer);

/* If status equals UX_SUCCESS, the class instance was successfully created and attached to the class container. */
```

## <a name="ux_host_stack_class_instance_destroy"></a><span data-ttu-id="b7d90-174">ux_host_stack_class_instance_destroy</span><span class="sxs-lookup"><span data-stu-id="b7d90-174">ux_host_stack_class_instance_destroy</span></span>

<span data-ttu-id="b7d90-175">Eliminare un'istanza della classe per un contenitore di classi.</span><span class="sxs-lookup"><span data-stu-id="b7d90-175">Destroy a class instance for a class container.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-176">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-176">Prototype</span></span>

```c
UINT ux_host_stack_class_instance_destroy(
    UX_HOST_CLASS *class, 
    VOID *class_instance);
```

### <a name="description"></a><span data-ttu-id="b7d90-177">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-177">Description</span></span>

<span data-ttu-id="b7d90-178">Questa funzione Elimina un'istanza della classe per un contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-178">This function destroys a class instance for a class container.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-179">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-179">Parameters</span></span>

- <span data-ttu-id="b7d90-180">**classe** Puntatore al contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-180">**class** Pointer to the class container.</span></span>
- <span data-ttu-id="b7d90-181">**class_instance** Puntatore all'istanza da eliminare definitivamente.</span><span class="sxs-lookup"><span data-stu-id="b7d90-181">**class_instance** Pointer to the instance to destroy.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-182">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-182">Return Values</span></span>

- <span data-ttu-id="b7d90-183">**UX_SUCCESS** (0x00) l'istanza della classe è stata eliminata definitivamente.</span><span class="sxs-lookup"><span data-stu-id="b7d90-183">**UX_SUCCESS** (0x00) The class instance was destroyed.</span></span>
- <span data-ttu-id="b7d90-184">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0X5b) l'istanza della classe non è collegata al contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-184">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) The class instance is not attached to the class container.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-185">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-185">Example</span></span>

```c
UINT status;
UX_HOST_CLASS_PRINTER *printer;

/* Get the instance for this class. */
printer = (UX_HOST_CLASS_PRINTER *) command -> ux_host_class_command_instance;

/* The printer is being shut down. */
printer -> printer_state = UX_HOST_CLASS_INSTANCE_SHUTDOWN;

/* Destroy the instance. */
status = ux_host_stack_class_instance_destroy(printer -> printer_class, (VOID *) printer);

/* If status equals UX_SUCCESS, the class instance was successfully destroyed. */
```

## <a name="ux_host_stack_class_instance_get"></a><span data-ttu-id="b7d90-186">ux_host_stack_class_instance_get</span><span class="sxs-lookup"><span data-stu-id="b7d90-186">ux_host_stack_class_instance_get</span></span>

<span data-ttu-id="b7d90-187">Ottenere un puntatore a un'istanza di classe per una classe specifica.</span><span class="sxs-lookup"><span data-stu-id="b7d90-187">Get a class instance pointer for a specific class.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-188">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-188">Prototype</span></span>

```c
UINT ux_host_stack_class_instance_get(
    UX_HOST_CLASS *class,
    UINT class_index, 
    VOID **class_instance);
```

### <a name="description"></a><span data-ttu-id="b7d90-189">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-189">Description</span></span>

<span data-ttu-id="b7d90-190">Questa funzione restituisce un puntatore all'istanza della classe per una classe specifica.</span><span class="sxs-lookup"><span data-stu-id="b7d90-190">This function returns a class instance pointer for a specific class.</span></span> <span data-ttu-id="b7d90-191">L'istanza di una classe non è contenuta nel codice della classe per ridurre la complessità della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-191">The instance of a class is not contained in the class code to reduce the class complexity.</span></span> <span data-ttu-id="b7d90-192">Ogni istanza di classe è invece collegata al contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-192">Rather, each class instance is attached to the class container.</span></span> <span data-ttu-id="b7d90-193">Questa funzione viene usata per cercare le istanze della classe all'interno di un contenitore di classi.</span><span class="sxs-lookup"><span data-stu-id="b7d90-193">This function is used to search for class instances within a class container.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-194">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-194">Parameters</span></span>

- <span data-ttu-id="b7d90-195">**classe** Puntatore al contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-195">**class** Pointer to the class container.</span></span>
- <span data-ttu-id="b7d90-196">**class_index** Indice che deve essere utilizzato dalla chiamata di funzione all'interno dell'elenco di classi associate al contenitore.</span><span class="sxs-lookup"><span data-stu-id="b7d90-196">**class_index** An index to be used by the function call within the list of attached classes to the container.</span></span>
- <span data-ttu-id="b7d90-197">**class_instance** Puntatore all'istanza di che deve essere restituita dalla chiamata di funzione.</span><span class="sxs-lookup"><span data-stu-id="b7d90-197">**class_instance** Pointer to the instance to be returned by the function call.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-198">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-198">Return Values</span></span>

- <span data-ttu-id="b7d90-199">**UX_SUCCESS** (0x00) l'istanza della classe è stata trovata.</span><span class="sxs-lookup"><span data-stu-id="b7d90-199">**UX_SUCCESS** (0x00) The class instance was found.</span></span>

- <span data-ttu-id="b7d90-200">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) non sono presenti altre istanze di classe associate al contenitore della classe.</span><span class="sxs-lookup"><span data-stu-id="b7d90-200">**UX_HOST_CLASS_INSTANCE_UNKNOWN** (0x5b) There are no more class instances attached to the class container.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-201">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-201">Example</span></span>

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* Obtain memory for this class instance. */
printer = ux_memory_allocate(UX_NO_ALIGN, sizeof(UX_HOST_CLASS_PRINTER));

if (printer == UX_NULL) return(UX_MEMORY_INSUFFICIENT);

/* Search for instance index 2. */
status = ux_host_stack_class_instance_get(class, 2, (VOID *) printer);

/* If status equals UX_SUCCESS, the class instance was found. */
```

## <a name="ux_host_stack_device_configuration_get"></a><span data-ttu-id="b7d90-202">ux_host_stack_device_configuration_get</span><span class="sxs-lookup"><span data-stu-id="b7d90-202">ux_host_stack_device_configuration_get</span></span>

<span data-ttu-id="b7d90-203">Ottenere un puntatore a un contenitore di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b7d90-203">Get a pointer to a configuration container.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-204">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-204">Prototype</span></span>

```c
UINT ux_host_stack_device_configuration_get(
    UX_DEVICE *device,
    UINT configuration_index, 
    UX_CONFIGURATION *configuration);
```

### <a name="description"></a><span data-ttu-id="b7d90-205">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-205">Description</span></span>

<span data-ttu-id="b7d90-206">Questa funzione restituisce un contenitore di configurazione basato su un handle di dispositivo e un indice di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b7d90-206">This function returns a configuration container based on a device handle and a configuration index.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-207">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-207">Parameters</span></span>

- <span data-ttu-id="b7d90-208">**dispositivo** Puntatore al contenitore di dispositivi proprietario della configurazione richiesta.</span><span class="sxs-lookup"><span data-stu-id="b7d90-208">**device** Pointer to the device container that owns the configuration requested.</span></span>
- <span data-ttu-id="b7d90-209">**configuration_index** Indice della configurazione in cui eseguire la ricerca.</span><span class="sxs-lookup"><span data-stu-id="b7d90-209">**configuration_index** Index of the configuration to be searched.</span></span>
- <span data-ttu-id="b7d90-210">**configurazione** di Indirizzo del puntatore al contenitore di configurazione da restituire.</span><span class="sxs-lookup"><span data-stu-id="b7d90-210">**configuration** Address of the pointer to the configuration container to be returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-211">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-211">Return Values</span></span>

- <span data-ttu-id="b7d90-212">**UX_SUCCESS** (0x00) la configurazione è stata trovata.</span><span class="sxs-lookup"><span data-stu-id="b7d90-212">**UX_SUCCESS** (0x00) The configuration was found.</span></span>
- <span data-ttu-id="b7d90-213">**UX_DEVICE_HANDLE_UNKNOWN** (0X50) il contenitore di dispositivi non esiste.</span><span class="sxs-lookup"><span data-stu-id="b7d90-213">**UX_DEVICE_HANDLE_UNKNOWN** (0x50) The device container does not exist.</span></span>
- <span data-ttu-id="b7d90-214">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'handle di configurazione per l'indice non esiste.</span><span class="sxs-lookup"><span data-stu-id="b7d90-214">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The configuration handle for the index does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-215">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-215">Example</span></span>

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* If the device has been configured already, we don't need to do it
again. */

if (printer -> printer_device -> ux_device_state == UX_DEVICE_CONFIGURED)
    return(UX_SUCCESS);

/* A printer normally has one configuration, retrieve 1st configuration only. */

status = ux_host_stack_device_configuration_get(printer -> printer_device,
    0, configuration);

/* If status equals UX_SUCCESS, the configuration was found. */
```

## <a name="ux_host_stack_device_configuration_select"></a><span data-ttu-id="b7d90-216">ux_host_stack_device_configuration_select</span><span class="sxs-lookup"><span data-stu-id="b7d90-216">ux_host_stack_device_configuration_select</span></span>

<span data-ttu-id="b7d90-217">Selezionare una configurazione specifica per un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b7d90-217">Select a specific configuration for a device.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-218">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-218">Prototype</span></span>

```c
UINT ux_host_stack_device_configuration_select (UX_CONFIGURATION *configuration);
```

### <a name="description"></a><span data-ttu-id="b7d90-219">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-219">Description</span></span>

<span data-ttu-id="b7d90-220">Questa funzione seleziona una configurazione specifica per un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b7d90-220">This function selects a specific configuration for a device.</span></span> <span data-ttu-id="b7d90-221">Quando questa configurazione è impostata sul dispositivo, per impostazione predefinita ogni interfaccia del dispositivo e l'impostazione alternativa 0 associata viene attivata sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b7d90-221">When this configuration is set to the device, by default, each device interface and its associated alternate setting 0 is activated on the device.</span></span> <span data-ttu-id="b7d90-222">Se la classe del dispositivo/interfaccia desidera modificare l'impostazione di una particolare interfaccia, è necessario eseguire una chiamata al servizio **ux_host_stack_interface_setting_select** .</span><span class="sxs-lookup"><span data-stu-id="b7d90-222">If the device/interface class wishes to change the setting of a particular interface, it needs to issue a **ux_host_stack_interface_setting_select** service call.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-223">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-223">Parameters</span></span>

- <span data-ttu-id="b7d90-224">**configurazione** di Puntatore al contenitore di configurazione che deve essere abilitato per questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b7d90-224">**configuration** Pointer to the configuration container that is to be enabled for this device.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-225">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-225">Return Values</span></span>

- <span data-ttu-id="b7d90-226">**UX_SUCCESS** (0x00) la selezione della configurazione è stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="b7d90-226">**UX_SUCCESS** (0x00) The configuration selection was successful.</span></span>
- <span data-ttu-id="b7d90-227">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) l'handle di configurazione non esiste.</span><span class="sxs-lookup"><span data-stu-id="b7d90-227">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The configuration handle does not exist.</span></span>
- <span data-ttu-id="b7d90-228">**UX_OVER_CURRENT_CONDITION** (0x43) è presente una condizione Over Current sul bus per questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="b7d90-228">**UX_OVER_CURRENT_CONDITION** (0x43) An over current condition exists on the bus for this configuration.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-229">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-229">Example</span></span>

```c
UINT status;

UX_HOST_CLASS_PRINTER *printer;

/* If the device has been configured already, we don't need to do it again. */
if (printer -> printer_device -> ux_device_state == UX_DEVICE_CONFIGURED)
    return(UX_SUCCESS);

/* A printer normally has one configuration - retrieve 1st configuration only. */
status = ux_host_stack_device_configuration_get(printer -> printer_device, 0,configuration);

/* If status equals UX_SUCCESS, the configuration selection was successful. */

/* If valid configuration, ask USBX to set this configuration. */
status = ux_host_stack_device_configuration_select(configuration);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_device_get"></a><span data-ttu-id="b7d90-230">ux_host_stack_device_get</span><span class="sxs-lookup"><span data-stu-id="b7d90-230">ux_host_stack_device_get</span></span>

<span data-ttu-id="b7d90-231">Ottenere un puntatore a un contenitore di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="b7d90-231">Get a pointer to a device container.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-232">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-232">Prototype</span></span>

```c
UINT ux_host_stack_device_get(
    ULONG device_index, 
    UX_DEVICE *device);
```

### <a name="description"></a><span data-ttu-id="b7d90-233">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-233">Description</span></span>

<span data-ttu-id="b7d90-234">Questa funzione restituisce un contenitore di dispositivi in base al relativo indice.</span><span class="sxs-lookup"><span data-stu-id="b7d90-234">This function returns a device container based on its index.</span></span> <span data-ttu-id="b7d90-235">L'indice del dispositivo inizia con 0.</span><span class="sxs-lookup"><span data-stu-id="b7d90-235">The device index starts with 0.</span></span> <span data-ttu-id="b7d90-236">Si noti che l'indice è un ULONG perché potrebbero essere presenti più controller e un indice byte potrebbe non essere sufficiente.</span><span class="sxs-lookup"><span data-stu-id="b7d90-236">Note that the index is a ULONG because we could have several controllers and a byte index might not be enough.</span></span> <span data-ttu-id="b7d90-237">L'indice del dispositivo non deve essere confuso con l'indirizzo del dispositivo specifico del bus.</span><span class="sxs-lookup"><span data-stu-id="b7d90-237">The device index should not be confused with the device address that is bus specific.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-238">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-238">Parameters</span></span>

- <span data-ttu-id="b7d90-239">**device_index** Indice del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b7d90-239">**device_index** Index of the device.</span></span>
- <span data-ttu-id="b7d90-240">**dispositivo** Indirizzo dell'indicatore di misura per il contenitore di dispositivi da restituire.</span><span class="sxs-lookup"><span data-stu-id="b7d90-240">**device** Address of the pointer for the device container to return.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-241">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-241">Return Values</span></span>

- <span data-ttu-id="b7d90-242">**UX_SUCCESS** (0x00) il contenitore di dispositivi esiste e viene restituito</span><span class="sxs-lookup"><span data-stu-id="b7d90-242">**UX_SUCCESS** (0x00) The device container exists and is returned</span></span>
- <span data-ttu-id="b7d90-243">Dispositivo **UX_DEVICE_HANDLE_UNKNOWN** (0x50) sconosciuto</span><span class="sxs-lookup"><span data-stu-id="b7d90-243">**UX_DEVICE_HANDLE_UNKNOWN** (0x50) Device unknown</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-244">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-244">Example</span></span>

```c
UINT status;

/* Locate the first device in USBX. */
status = ux_host_stack_device_get(0, device);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_interface_endpoint_get"></a><span data-ttu-id="b7d90-245">ux_host_stack_interface_endpoint_get</span><span class="sxs-lookup"><span data-stu-id="b7d90-245">ux_host_stack_interface_endpoint_get</span></span>

<span data-ttu-id="b7d90-246">Ottenere un contenitore di endpoint.</span><span class="sxs-lookup"><span data-stu-id="b7d90-246">Get an endpoint container.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-247">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-247">Prototype</span></span>

```c
UINT ux_host_stack_interface_endpoint_get(
    UX_INTERFACE *interface,
    UINT endpoint_index,
    UX_ENDPOINT *endpoint);
```

### <a name="description"></a><span data-ttu-id="b7d90-248">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-248">Description</span></span>

<span data-ttu-id="b7d90-249">Questa funzione restituisce un contenitore di endpoint basato sull'handle dell'interfaccia e un indice dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="b7d90-249">This function returns an endpoint container based on the interface handle and an endpoint index.</span></span> <span data-ttu-id="b7d90-250">Si presuppone che sia stata selezionata l'impostazione alternativa per l'interfaccia o che l'impostazione predefinita venga utilizzata prima degli endpoint di cui viene eseguita la ricerca.</span><span class="sxs-lookup"><span data-stu-id="b7d90-250">It is assumed that the alternate setting for the interface has been selected or the default setting is being used prior to the endpoint(s) being searched.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-251">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-251">Parameters</span></span>

- <span data-ttu-id="b7d90-252">**interfaccia** di Puntatore al contenitore dell'interfaccia che contiene l'endpoint richiesto.</span><span class="sxs-lookup"><span data-stu-id="b7d90-252">**interface** Pointer to the interface container that contains the endpoint requested.</span></span>
- <span data-ttu-id="b7d90-253">**endpoint_index** Indice dell'endpoint in questa interfaccia.</span><span class="sxs-lookup"><span data-stu-id="b7d90-253">**endpoint_index** Index of the endpoint in this interface.</span></span>
- <span data-ttu-id="b7d90-254">**endpoint** di Indirizzo del contenitore dell'endpoint da restituire.</span><span class="sxs-lookup"><span data-stu-id="b7d90-254">**endpoint** Address of the endpoint container to be returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-255">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-255">Return Values</span></span>

- <span data-ttu-id="b7d90-256">**UX_SUCCESS** (0x00) il contenitore dell'endpoint esiste e viene restituito.</span><span class="sxs-lookup"><span data-stu-id="b7d90-256">**UX_SUCCESS** (0x00) The endpoint container exists and is returned.</span></span>
- <span data-ttu-id="b7d90-257">L'interfaccia **UX_INTERFACE_HANDLE_UNKNOWN** (0x52) specificata non esiste.</span><span class="sxs-lookup"><span data-stu-id="b7d90-257">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) Interface specified does not exist.</span></span>
- <span data-ttu-id="b7d90-258">L'indice dell'endpoint **UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) non esiste.</span><span class="sxs-lookup"><span data-stu-id="b7d90-258">**UX_ENDPOINT_HANDLE_UNKNOWN** (0x53) Endpoint index does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-259">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-259">Example</span></span>

```c
UINT status;
UX_HOST_CLASS_PRINTER *printer;

for(endpoint_index = 0;
    endpoint_index < printer -> printer_interface ->
        ux_interface_descriptor.bNumEndpoints;
    endpoint_index++)
{
    status = ux_host_stack_interface_endpoint_get (printer -> printer_interface,
        endpoint_index, &endpoint);

    if (status == UX_SUCCESS)
    {
        /* Check if endpoint is bulk and OUT. */
        if (((endpoint -> ux_endpoint_descriptor.bEndpointAddress &
            UX_ENDPOINT_DIRECTION) == UX_ENDPOINT_OUT) &&
            ((endpoint -> ux_endpoint_descriptor.bmAttributes &
            UX_MASK_ENDPOINT_TYPE) == UX_BULK_ENDPOINT))
        return(UX_SUCCESS);
    }
}
```

## <a name="ux_host_stack_hcd_register"></a><span data-ttu-id="b7d90-260">ux_host_stack_hcd_register</span><span class="sxs-lookup"><span data-stu-id="b7d90-260">ux_host_stack_hcd_register</span></span>

<span data-ttu-id="b7d90-261">Registrare un controller USB nello stack USB.</span><span class="sxs-lookup"><span data-stu-id="b7d90-261">Register a USB controller to the USB stack.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-262">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-262">Prototype</span></span>

```c
UINT ux_host_stack_hcd_register(
    UCHAR *hcd_name,
    UINT (*hcd_function)(struct UX_HCD_STRUCT *),
    ULONG hcd_param1, ULONG hcd_param2);
```

### <a name="description"></a><span data-ttu-id="b7d90-263">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-263">Description</span></span>

<span data-ttu-id="b7d90-264">Questa funzione registra un controller USB nello stack USB.</span><span class="sxs-lookup"><span data-stu-id="b7d90-264">This function registers a USB controller to the USB stack.</span></span> <span data-ttu-id="b7d90-265">Alloca principalmente la memoria utilizzata da questo controller e passa il comando di inizializzazione al controller.</span><span class="sxs-lookup"><span data-stu-id="b7d90-265">It mainly allocates the memory used by this controller and passes the initialization command to the controller.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-266">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-266">Parameters</span></span>

- <span data-ttu-id="b7d90-267">**hcd_name** Nome del controller host</span><span class="sxs-lookup"><span data-stu-id="b7d90-267">**hcd_name** Name of the host controller</span></span>
- <span data-ttu-id="b7d90-268">**hcd_function** Funzione nel controller host responsabile dell'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="b7d90-268">**hcd_function** The function in the host controller responsible for the initialization.</span></span>
- <span data-ttu-id="b7d90-269">**hcd_param1** Il IO o la risorsa di memoria utilizzata da HCD.</span><span class="sxs-lookup"><span data-stu-id="b7d90-269">**hcd_param1** The IO or memory resource used by the hcd.</span></span>
- <span data-ttu-id="b7d90-270">**hcd_param2** IRQ utilizzato dal controller host.</span><span class="sxs-lookup"><span data-stu-id="b7d90-270">**hcd_param2** The IRQ used by the host controller.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-271">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-271">Return Values</span></span>

- <span data-ttu-id="b7d90-272">**UX_SUCCESS** (0x00) il controller è stato inizializzato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b7d90-272">**UX_SUCCESS** (0x00) The controller was initialized properly.</span></span>
- <span data-ttu-id="b7d90-273">**UX_MEMORY_INSUFFICIENT** (0x12) memoria insufficiente per questo controller.</span><span class="sxs-lookup"><span data-stu-id="b7d90-273">**UX_MEMORY_INSUFFICIENT** (0x12) Not enough memory for this controller.</span></span>
- <span data-ttu-id="b7d90-274">**UX_PORT_RESET_FAILED** (0X31) la reimpostazione del controller non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="b7d90-274">**UX_PORT_RESET_FAILED** (0x31) The reset of the controller failed.</span></span>
- <span data-ttu-id="b7d90-275">**UX_CONTROLLER_INIT_FAILED** (0x32) non è stato possibile inizializzare correttamente il controller.</span><span class="sxs-lookup"><span data-stu-id="b7d90-275">**UX_CONTROLLER_INIT_FAILED** (0x32) The controller failed to initialize properly.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-276">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-276">Example</span></span>

```c
UINT status;

/* Initialize a host controller mapped at address 0xd0000 and using IRQ 10. */

status = ux_host_stack_hcd_register("ux_hcd_controller",
    ux_hcd_controller_initialize, 0xd0000, 0x0a);

/* If status equals UX_SUCCESS, the controller was initialized properly. */

/* Note that the application must also setup a call to the
    interrupt handler for the controller.
    The function for the controller is called _ux_hch_controller_interrupt_handler. */
```

## <a name="ux_host_stack_configuration_interface_get"></a><span data-ttu-id="b7d90-277">ux_host_stack_configuration_interface_get</span><span class="sxs-lookup"><span data-stu-id="b7d90-277">ux_host_stack_configuration_interface_get</span></span>

<span data-ttu-id="b7d90-278">Ottenere un puntatore del contenitore di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="b7d90-278">Get an interface container pointer.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-279">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-279">Prototype</span></span>

```c
UINT ux_host_stack_configuration_interface_get (
    UX_CONFIGURATION *configuration,
    UINT interface_index, 
    UINT alternate_setting_index, 
    UX_INTERFACE **interface);
```

### <a name="description"></a><span data-ttu-id="b7d90-280">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-280">Description</span></span>

<span data-ttu-id="b7d90-281">Questa funzione restituisce un contenitore di interfaccia basato su un handle di configurazione, un indice dell'interfaccia e un indice di impostazione alternativo.</span><span class="sxs-lookup"><span data-stu-id="b7d90-281">This function returns an interface container based on a configuration handle, an interface index, and an alternate setting index.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-282">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-282">Parameters</span></span>

- <span data-ttu-id="b7d90-283">**configurazione** di Puntatore al contenitore di configurazione che possiede l'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="b7d90-283">**configuration** Pointer to the configuration container that owns the interface.</span></span>
- <span data-ttu-id="b7d90-284">**interface_index** Indice dell'interfaccia in cui eseguire la ricerca.</span><span class="sxs-lookup"><span data-stu-id="b7d90-284">**interface_index** Interface index to be searched.</span></span>
- <span data-ttu-id="b7d90-285">**alternate_setting_index** Impostazione alternativa all'interno dell'interfaccia in cui eseguire la ricerca.</span><span class="sxs-lookup"><span data-stu-id="b7d90-285">**alternate_setting_index** Alternate setting within the interface to search.</span></span>
- <span data-ttu-id="b7d90-286">**interfaccia** di Indirizzo del puntatore del contenitore di interfaccia da restituire.</span><span class="sxs-lookup"><span data-stu-id="b7d90-286">**interface** Address of the interface container pointer to be returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-287">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-287">Return Values</span></span>

- <span data-ttu-id="b7d90-288">**UX_SUCCESS** (0x00) il contenitore dell'interfaccia per l'indice dell'interfaccia e l'impostazione alternativa è stato trovato e restituito.</span><span class="sxs-lookup"><span data-stu-id="b7d90-288">**UX_SUCCESS** (0x00) The interface container for the interface index and the alternate setting was found and returned.</span></span>
- <span data-ttu-id="b7d90-289">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0X51) la configurazione non esiste.</span><span class="sxs-lookup"><span data-stu-id="b7d90-289">**UX_CONFIGURATION_HANDLE_UNKNOWN** (0x51) The configuration does not exist.</span></span>
- <span data-ttu-id="b7d90-290">**UX_INTERFACE_HANDLE_UNKNOWN** (0X52) l'interfaccia non esiste.</span><span class="sxs-lookup"><span data-stu-id="b7d90-290">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) The interface does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-291">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-291">Example</span></span>

```c
UINT status;

/* Search for the default alternate setting on the first interface for the printer. */
status = ux_host_stack_configuration_interface_get(configuration, 0, 0,
    &printer -> printer_interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_interface_setting_select"></a><span data-ttu-id="b7d90-292">ux_host_stack_interface_setting_select</span><span class="sxs-lookup"><span data-stu-id="b7d90-292">ux_host_stack_interface_setting_select</span></span>

<span data-ttu-id="b7d90-293">Selezionare un'impostazione alternativa per un'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="b7d90-293">Select an alternate setting for an interface.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-294">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-294">Prototype</span></span>

```c
UINT ux_host_stack_interface_setting_select(UX_INTERFACE *interface);
```

### <a name="description"></a><span data-ttu-id="b7d90-295">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-295">Description</span></span>

<span data-ttu-id="b7d90-296">Questa funzione seleziona una specifica impostazione alternativa per un'interfaccia specificata che appartiene alla configurazione selezionata.</span><span class="sxs-lookup"><span data-stu-id="b7d90-296">This function selects a specific alternate setting for a given interface belonging to the selected configuration.</span></span> <span data-ttu-id="b7d90-297">Questa funzione viene usata per passare dall'impostazione alternativa predefinita a una nuova impostazione o per tornare all'impostazione predefinita alternativa.</span><span class="sxs-lookup"><span data-stu-id="b7d90-297">This function is used to change from the default alternate setting to a new setting or to go back to the default alternate setting.</span></span> <span data-ttu-id="b7d90-298">Quando viene selezionata una nuova impostazione alternativa, le caratteristiche precedenti dell'endpoint non sono valide e devono essere ricaricate.</span><span class="sxs-lookup"><span data-stu-id="b7d90-298">When a new alternate setting is selected, the previous endpoint characteristics are invalid and should be reloaded.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="b7d90-299">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="b7d90-299">Input Parameter</span></span>

- <span data-ttu-id="b7d90-300">**interfaccia** di Puntatore al contenitore dell'interfaccia di cui è necessario selezionare l'impostazione alternativa.</span><span class="sxs-lookup"><span data-stu-id="b7d90-300">**interface** Pointer to the interface container whose alternate setting is to be selected.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-301">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-301">Return Values</span></span>

- <span data-ttu-id="b7d90-302">**UX_SUCCESS** (0x00) la selezione dell'impostazione alternativa per questa interfaccia è stata completata.</span><span class="sxs-lookup"><span data-stu-id="b7d90-302">**UX_SUCCESS** (0x00) The alternate setting for this interface has been successfully selected.</span></span>
- <span data-ttu-id="b7d90-303">**UX_INTERFACE_HANDLE_UNKNOWN** (0X52) l'interfaccia non esiste.</span><span class="sxs-lookup"><span data-stu-id="b7d90-303">**UX_INTERFACE_HANDLE_UNKNOWN** (0x52) The interface does not exist.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-304">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-304">Example</span></span>

```c
UINT status;

/* Select a new alternate setting for this interface. */
status = ux_host_stack_interface_setting_select(interface);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_transfer_request_abort"></a><span data-ttu-id="b7d90-305">ux_host_stack_transfer_request_abort</span><span class="sxs-lookup"><span data-stu-id="b7d90-305">ux_host_stack_transfer_request_abort</span></span>

<span data-ttu-id="b7d90-306">Interrompere una richiesta di trasferimento in sospeso.</span><span class="sxs-lookup"><span data-stu-id="b7d90-306">Abort a pending transfer request.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-307">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-307">Prototype</span></span>

```c
UINT ux_host_stack_transfer_request_abort(UX_TRANSFER REQUEST *transfer request);
```

### <a name="description"></a><span data-ttu-id="b7d90-308">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-308">Description</span></span>

<span data-ttu-id="b7d90-309">Questa funzione interrompe una richiesta di trasferimento in sospeso inviata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b7d90-309">This function aborts a pending transfer request that has been previously submitted.</span></span> <span data-ttu-id="b7d90-310">Questa funzione Annulla solo una richiesta di trasferimento specifica.</span><span class="sxs-lookup"><span data-stu-id="b7d90-310">This function only cancels a specific transfer request.</span></span> <span data-ttu-id="b7d90-311">La chiamata alla funzione avrà lo stato UX_TRANSFER REQUEST_STATUS_ABORT.</span><span class="sxs-lookup"><span data-stu-id="b7d90-311">The call back to the function will have the UX_TRANSFER REQUEST_STATUS_ABORT status.</span></span>

### <a name="parameters"></a><span data-ttu-id="b7d90-312">Parametri</span><span class="sxs-lookup"><span data-stu-id="b7d90-312">Parameters</span></span>

- <span data-ttu-id="b7d90-313">**richiesta di trasferimento** Puntatore alla richiesta di trasferimento da interrompere.</span><span class="sxs-lookup"><span data-stu-id="b7d90-313">**transfer request** Pointer to the transfer request to be aborted.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-314">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-314">Return Values</span></span>

- <span data-ttu-id="b7d90-315">**UX_SUCCESS** (0x00) il trasferimento USB per la richiesta di trasferimento è stato annullato.</span><span class="sxs-lookup"><span data-stu-id="b7d90-315">**UX_SUCCESS** (0x00) The USB transfer for this transfer request was canceled.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-316">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7d90-316">Example</span></span>

```c
UINT status;

/* The following example illustrates this service. */
status = ux_host_stack_transfer_request_abort(transfer request);

/* If status equals UX_SUCCESS, the operation was successful. */
```

## <a name="ux_host_stack_transfer_request"></a><span data-ttu-id="b7d90-317">ux_host_stack_transfer_request</span><span class="sxs-lookup"><span data-stu-id="b7d90-317">ux_host_stack_transfer_request</span></span>

<span data-ttu-id="b7d90-318">Richiedere un trasferimento USB.</span><span class="sxs-lookup"><span data-stu-id="b7d90-318">Request a USB transfer.</span></span>

### <a name="prototype"></a><span data-ttu-id="b7d90-319">Prototipo</span><span class="sxs-lookup"><span data-stu-id="b7d90-319">Prototype</span></span>

```c
UINT ux_host_stack_transfer_request(UX_TRANSFER REQUEST *transfer request);
```

### <a name="description"></a><span data-ttu-id="b7d90-320">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b7d90-320">Description</span></span>

<span data-ttu-id="b7d90-321">Questa funzione esegue una transazione USB.</span><span class="sxs-lookup"><span data-stu-id="b7d90-321">This function performs a USB transaction.</span></span> <span data-ttu-id="b7d90-322">All'immissione della richiesta di trasferimento viene assegnata la pipe dell'endpoint selezionata per la transazione e i parametri associati al trasferimento (payload dei dati, lunghezza della transazione).</span><span class="sxs-lookup"><span data-stu-id="b7d90-322">On entry the transfer request gives the endpoint pipe selected for this transaction and the parameters associated with the transfer (data payload, length of transaction).</span></span> <span data-ttu-id="b7d90-323">Per la pipe di controllo, la transazione è bloccata e restituirà solo quando le tre fasi del trasferimento del controllo sono state completate o se si è verificato un errore precedente.</span><span class="sxs-lookup"><span data-stu-id="b7d90-323">For Control pipe, the transaction is blocking and will only return when the three phases of the control transfer have been completed or if there is a previous error.</span></span> <span data-ttu-id="b7d90-324">Per le altre pipe, lo stack USB pianifica la transazione sull'USB ma non ne attende il completamento.</span><span class="sxs-lookup"><span data-stu-id="b7d90-324">For other pipes, the USB stack will schedule the transaction on the USB but will not wait for its completion.</span></span> <span data-ttu-id="b7d90-325">Ogni richiesta di trasferimento per le pipe non bloccanti deve specificare un gestore routine di completamento.</span><span class="sxs-lookup"><span data-stu-id="b7d90-325">Each transfer request for non-blocking pipes has to specify a completion routine handler.</span></span>

<span data-ttu-id="b7d90-326">Quando la chiamata di funzione restituisce, lo stato della richiesta di trasferimento deve essere esaminato in quanto contiene il risultato della transazione.</span><span class="sxs-lookup"><span data-stu-id="b7d90-326">When the function call returns, the status of the transfer request should be examined as it contains the result of the transaction.</span></span>

### <a name="input-parameter"></a><span data-ttu-id="b7d90-327">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="b7d90-327">Input Parameter</span></span>

- <span data-ttu-id="b7d90-328">**transfer_request** Puntatore alla richiesta di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="b7d90-328">**transfer_request** Pointer to the transfer request.</span></span> <span data-ttu-id="b7d90-329">La richiesta di trasferimento contiene tutte le informazioni necessarie per il trasferimento.</span><span class="sxs-lookup"><span data-stu-id="b7d90-329">The transfer request contains all the necessary information required for the transfer.</span></span>

### <a name="return-values"></a><span data-ttu-id="b7d90-330">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="b7d90-330">Return Values</span></span>

- <span data-ttu-id="b7d90-331">**UX_SUCCESS** (0x00) il trasferimento USB per la richiesta di trasferimento è stato pianificato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b7d90-331">**UX_SUCCESS** (0x00) The USB transfer for this transfer request was scheduled properly.</span></span> <span data-ttu-id="b7d90-332">Il codice di stato della richiesta di trasferimento deve essere esaminato al completamento della richiesta di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="b7d90-332">The status code of the transfer request should be examined when the transfer request completes.</span></span>
- <span data-ttu-id="b7d90-333">**UX_MEMORY_INSUFFICIENT** (0x12) memoria insufficiente per allocare le risorse del controller necessarie.</span><span class="sxs-lookup"><span data-stu-id="b7d90-333">**UX_MEMORY_INSUFFICIENT** (0x12) Not enough memory to allocate the necessary controller resources.</span></span>
- <span data-ttu-id="b7d90-334">**UX_TRANSFER_NOT_READY** (0x25) il dispositivo si trova in uno stato non valido. deve essere collegato, risolto o configurato.</span><span class="sxs-lookup"><span data-stu-id="b7d90-334">**UX_TRANSFER_NOT_READY** (0x25) The device was in an invalid state – must be ATTACHED,ADDRESSED, or CONFIGURED.</span></span>

### <a name="example"></a><span data-ttu-id="b7d90-335">Esempio:</span><span class="sxs-lookup"><span data-stu-id="b7d90-335">Example:</span></span>

```c
UINT status;

/* Create a transfer request for the SET_CONFIGURATION request. No data for this request. */
transfer_request -> ux_transfer_request_requested_length = 0;
transfer_request -> ux_transfer_request_function = UX_SET_CONFIGURATION;
transfer_request -> ux_transfer_request_type =
    UX_REQUEST_OUT |
    UX_REQUEST_TYPE_STANDARD |
    UX_REQUEST_TARGET_DEVICE;

transfer_request -> ux_transfer_request_value = (USHORT)
    configuration -> ux_configuration_descriptor.bConfigurationValue;
transfer_request -> ux_transfer_request_index = 0;

/* Send request to HCD layer. */
status = ux_host_stack_transfer_request(transfer_request);

/* If status equals UX_SUCCESS, the operation was successful. */
```
