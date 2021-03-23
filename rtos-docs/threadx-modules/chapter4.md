---
title: Capitolo 4-API del modulo
author: philmea
ms.author: philmea
description: Questo articolo è un riepilogo delle API aggiuntive disponibili per un modulo.
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b5804e2dbb8d08a272abc85a583576f43b7204c1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821392"
---
# <a name="chapter-4---module-apis"></a><span data-ttu-id="0612a-103">Capitolo 4-API del modulo</span><span class="sxs-lookup"><span data-stu-id="0612a-103">Chapter 4 - Module APIs</span></span>

## <a name="summary-of-module-apis"></a><span data-ttu-id="0612a-104">Riepilogo delle API del modulo</span><span class="sxs-lookup"><span data-stu-id="0612a-104">Summary of Module APIs</span></span>

<span data-ttu-id="0612a-105">Sono disponibili diverse funzioni API aggiuntive per un modulo, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0612a-105">There are several additional API functions available to a module, as follows:</span></span>

- <span data-ttu-id="0612a-106">\***txm_module_application_request** _-_Application richiesta specifica al codice residente \*</span><span class="sxs-lookup"><span data-stu-id="0612a-106">***txm_module_application_request** _ - _Application-specific request to resident code*</span></span>
- <span data-ttu-id="0612a-107">\***txm_module_object_allocate** _-_Allocate memoria esterna al modulo per l'oggetto \*</span><span class="sxs-lookup"><span data-stu-id="0612a-107">***txm_module_object_allocate** _ - _Allocate memory outside of module for object*</span></span>
- <span data-ttu-id="0612a-108">\***txm_module_object_deallocate** _-_Deallocate memoria oggetto allocata in precedenza \*</span><span class="sxs-lookup"><span data-stu-id="0612a-108">***txm_module_object_deallocate** _ - _Deallocate previously allocated object memory*</span></span>
- <span data-ttu-id="0612a-109">\***txm_module_object_pointer_get** _-_Find oggetto di sistema e recuperare il puntatore a oggetti \*</span><span class="sxs-lookup"><span data-stu-id="0612a-109">***txm_module_object_pointer_get** _ - _Find system object and retrieve object pointer*</span></span>
- <span data-ttu-id="0612a-110">\***txm_module_object_pointer_get_extended** _-_Find oggetto di sistema e recuperare il puntatore all'oggetto, lunghezza del nome Safety \*</span><span class="sxs-lookup"><span data-stu-id="0612a-110">***txm_module_object_pointer_get_extended** _ - _Find system object and retrieve object pointer, name length safety*</span></span>

## <a name="return-values"></a><span data-ttu-id="0612a-111">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="0612a-111">Return values</span></span>

<span data-ttu-id="0612a-112">Per alcune API RTO di Azure vengono restituiti codici di errore aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="0612a-112">Additional error codes are returned for some Azure RTOS APIs.</span></span> <span data-ttu-id="0612a-113">Questi codici di errore aggiuntivi sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="0612a-113">These additional error codes are defined as follows:</span></span>

- <span data-ttu-id="0612a-114">**TXM_MODULE_INVALID_PROPERTIES** (0xf3): indica che il modulo non dispone delle proprietà corrette per effettuare una chiamata API.</span><span class="sxs-lookup"><span data-stu-id="0612a-114">**TXM_MODULE_INVALID_PROPERTIES** (0xF3): Indicates the module does not have the correct properties to make an API call.</span></span> <span data-ttu-id="0612a-115">Ad esempio, la chiamata di API di traccia in modalità utente.</span><span class="sxs-lookup"><span data-stu-id="0612a-115">For example, calling trace APIs in user mode.</span></span>
- <span data-ttu-id="0612a-116">**TXM_MODULE_INVALID_MEMORY** (0xF4): indica che la memoria fornita dal modulo non è valida o si trova in una posizione non valida.</span><span class="sxs-lookup"><span data-stu-id="0612a-116">**TXM_MODULE_INVALID_MEMORY** (0xF4): Indicates the memory supplied by the module is invalid or is in an invalid location.</span></span> <span data-ttu-id="0612a-117">Ad esempio, nei moduli protetti da memoria, i blocchi di controllo degli oggetti non possono essere individuati in memoria a cui il modulo può accedere.</span><span class="sxs-lookup"><span data-stu-id="0612a-117">For example, in memory protected modules, object control blocks are not allowed to be located in memory the module can access.</span></span>
- <span data-ttu-id="0612a-118">**TXM_MODULE_INVALID_CALLBACK** (0xf5): il callback specificato nell'API non è compreso nell'intervallo del codice del modulo e pertanto non è valido.</span><span class="sxs-lookup"><span data-stu-id="0612a-118">**TXM_MODULE_INVALID_CALLBACK** (0xF5): Callback specified in the API is outside the range of the module's code and is therefore invalid.</span></span>

---

## <a name="txm_module_application_request"></a><span data-ttu-id="0612a-119">txm_module_application_request</span><span class="sxs-lookup"><span data-stu-id="0612a-119">txm_module_application_request</span></span>

<span data-ttu-id="0612a-120">Richiesta specifica dell'applicazione al codice residente.</span><span class="sxs-lookup"><span data-stu-id="0612a-120">Application-specific request to resident code.</span></span>

### <a name="prototype"></a><span data-ttu-id="0612a-121">Prototipo</span><span class="sxs-lookup"><span data-stu-id="0612a-121">Prototype</span></span>

```c
UINT txm_module_application_request(
    ULONG request, 
    ULONG param_1,
    ULONG param_2,
    ULONG param_3);
```

### <a name="description"></a><span data-ttu-id="0612a-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0612a-122">Description</span></span>

<span data-ttu-id="0612a-123">Questo servizio effettua la richiesta specificata alla parte residente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0612a-123">This service makes the specified request to the resident portion of the application.</span></span> <span data-ttu-id="0612a-124">Si presuppone che la struttura della richiesta venga preparata prima della chiamata.</span><span class="sxs-lookup"><span data-stu-id="0612a-124">It is assumed that the request structure is prepared prior to the call.</span></span> <span data-ttu-id="0612a-125">L'elaborazione effettiva della richiesta viene svolta nel codice residente della funzione ***_txm_module_manager_application_request***.</span><span class="sxs-lookup"><span data-stu-id="0612a-125">The actual processing of the request takes place in the resident code in the function ***_txm_module_manager_application_request***.</span></span> <span data-ttu-id="0612a-126">Per impostazione predefinita, questa funzione viene lasciata vuota ed è progettata per la modifica da parte dello sviluppatore dell'applicazione residente.</span><span class="sxs-lookup"><span data-stu-id="0612a-126">By default, this function is left empty and is designed for the resident application developer to modify.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0612a-127">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="0612a-127">Input parameters</span></span>

- <span data-ttu-id="0612a-128">**richiesta** ID richiesta (applicazione definita)</span><span class="sxs-lookup"><span data-stu-id="0612a-128">**request** Request ID (application defined)</span></span>
- <span data-ttu-id="0612a-129">**Param_1** Primo parametro</span><span class="sxs-lookup"><span data-stu-id="0612a-129">**param_1** First parameter</span></span>
- <span data-ttu-id="0612a-130">**param_2** Secondo parametro</span><span class="sxs-lookup"><span data-stu-id="0612a-130">**param_2** Second parameter</span></span>
- <span data-ttu-id="0612a-131">**param_3** Terzo parametro</span><span class="sxs-lookup"><span data-stu-id="0612a-131">**param_3** Third parameter</span></span>

### <a name="return-values"></a><span data-ttu-id="0612a-132">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="0612a-132">Return values</span></span>

- <span data-ttu-id="0612a-133">La richiesta di **TX_SUCCESS** (0x00) è riuscita.</span><span class="sxs-lookup"><span data-stu-id="0612a-133">**TX_SUCCESS** (0x00) Successful request.</span></span>
- <span data-ttu-id="0612a-134">La richiesta **TX_NOT_AVAILABLE** (0x1d) non è supportata dal codice residente.</span><span class="sxs-lookup"><span data-stu-id="0612a-134">**TX_NOT_AVAILABLE** (0x1D) Request not supported by resident code.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0612a-135">Consentito da</span><span class="sxs-lookup"><span data-stu-id="0612a-135">Allowed from</span></span>

<span data-ttu-id="0612a-136">Thread del modulo</span><span class="sxs-lookup"><span data-stu-id="0612a-136">Module threads</span></span>

### <a name="example"></a><span data-ttu-id="0612a-137">Esempio</span><span class="sxs-lookup"><span data-stu-id="0612a-137">Example</span></span>

```c
/* Call application resident code with ID=77 and the
   parameters set to 1, 2, 3. */
status = txm_module_application_request(77, 1, 2, 3);

/* If status is TX_SUCCESS the request was successful. */
```

---

## <a name="txm_module_object_allocate"></a><span data-ttu-id="0612a-138">txm_module_object_allocate</span><span class="sxs-lookup"><span data-stu-id="0612a-138">txm_module_object_allocate</span></span>

<span data-ttu-id="0612a-139">Allocare memoria nel pool di oggetti (creata dall'applicazione residente) per un blocco di controllo dell'oggetto modulo.</span><span class="sxs-lookup"><span data-stu-id="0612a-139">Allocate memory in the object pool (created by the resident application) for a module object control block.</span></span>

### <a name="prototype"></a><span data-ttu-id="0612a-140">Prototipo</span><span class="sxs-lookup"><span data-stu-id="0612a-140">Prototype</span></span>

```c
UINT txm_module_object_allocate(
   VOID **object_ptr, 
   ULONG object_size);
```

### <a name="description"></a><span data-ttu-id="0612a-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0612a-141">Description</span></span>

<span data-ttu-id="0612a-142">Questo servizio alloca memoria per un oggetto modulo dalla memoria esterna al modulo, che consente di evitare il danneggiamento del blocco di controllo degli oggetti da parte del codice del modulo.</span><span class="sxs-lookup"><span data-stu-id="0612a-142">This service allocates memory for a module object from memory outside of the module, which helps prevent corruption of the object control block by the module's code.</span></span> <span data-ttu-id="0612a-143">Nei sistemi protetti da memoria tutti i blocchi di controllo degli oggetti devono essere allocati con questa API prima di poter essere creati.</span><span class="sxs-lookup"><span data-stu-id="0612a-143">In memory protected systems, all object control blocks must be allocated with this API before they can be created.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0612a-144">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="0612a-144">Input parameters</span></span>

- <span data-ttu-id="0612a-145">**object_ptr** Destinazione del puntatore all'oggetto al completamento dell'allocazione.</span><span class="sxs-lookup"><span data-stu-id="0612a-145">**object_ptr** Destination of object pointer on successful allocation.</span></span>
- <span data-ttu-id="0612a-146">**object_size** Dimensioni in byte dell'oggetto da allocare.</span><span class="sxs-lookup"><span data-stu-id="0612a-146">**object_size** Size in bytes of the object to be allocated.</span></span>

### <a name="return-values"></a><span data-ttu-id="0612a-147">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="0612a-147">Return values</span></span>

- <span data-ttu-id="0612a-148">**TX_SUCCESS** (0x00) allocare l'oggetto riuscito.</span><span class="sxs-lookup"><span data-stu-id="0612a-148">**TX_SUCCESS** (0x00) Successful object allocate.</span></span>
- <span data-ttu-id="0612a-149">**TX_NO_MEMORY** (0x10) memoria insufficiente.</span><span class="sxs-lookup"><span data-stu-id="0612a-149">**TX_NO_MEMORY** (0x10) Not enough memory.</span></span>
- <span data-ttu-id="0612a-150">Gestione moduli **TX_NOT_AVAILABLE** (0x1d) non ha creato un pool di oggetti da cui allocare</span><span class="sxs-lookup"><span data-stu-id="0612a-150">**TX_NOT_AVAILABLE** (0x1D) Module manager has not created an object pool to allocate from</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0612a-151">Consentito da</span><span class="sxs-lookup"><span data-stu-id="0612a-151">Allowed from</span></span>

<span data-ttu-id="0612a-152">Thread del modulo</span><span class="sxs-lookup"><span data-stu-id="0612a-152">Module threads</span></span>

### <a name="example"></a><span data-ttu-id="0612a-153">Esempio</span><span class="sxs-lookup"><span data-stu-id="0612a-153">Example</span></span>

```c
TX_QUEUE *queue_pointer;

/* Allocate a control block for a module message queue. */
status = txm_module_object_allocate(&queue_pointer, sizeof(TX_QUEUE));

/* If status is TX_SUCCESS the queue_pointer points to
   memory allocated outside of the module and can be supplied
   to tx_queue_create to create a queue for the module. */
```

### <a name="see-also"></a><span data-ttu-id="0612a-154">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0612a-154">See also</span></span>

- <span data-ttu-id="0612a-155">txm_module_object_deallocate</span><span class="sxs-lookup"><span data-stu-id="0612a-155">txm_module_object_deallocate</span></span>
- <span data-ttu-id="0612a-156">txm_module_object_pointer_get</span><span class="sxs-lookup"><span data-stu-id="0612a-156">txm_module_object_pointer_get</span></span>

---

## <a name="txm_module_object_deallocate"></a><span data-ttu-id="0612a-157">txm_module_object_deallocate</span><span class="sxs-lookup"><span data-stu-id="0612a-157">txm_module_object_deallocate</span></span>

<span data-ttu-id="0612a-158">Deallocare memoria oggetto allocata in precedenza</span><span class="sxs-lookup"><span data-stu-id="0612a-158">Deallocate previously allocated object memory</span></span>

### <a name="prototype"></a><span data-ttu-id="0612a-159">Prototipo</span><span class="sxs-lookup"><span data-stu-id="0612a-159">Prototype</span></span>

```c
UINT txm_module_object_deallocate(VOID *object_ptr);
```

### <a name="description"></a><span data-ttu-id="0612a-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0612a-160">Description</span></span>

<span data-ttu-id="0612a-161">***Questo servizio è stato deprecato perché non è più necessario***.</span><span class="sxs-lookup"><span data-stu-id="0612a-161">***This service has been deprecated because it is no longer needed***.</span></span>

<span data-ttu-id="0612a-162">La memoria allocata in precedenza tramite \*\*\*txm_module_object_allocate \**_ viene deallocata nel servizio _*_TX_ \_ _delete\*\*\*.</span><span class="sxs-lookup"><span data-stu-id="0612a-162">The memory that was previously allocated via ***txm_module_object_allocate\**_ is deallocated in the _*_tx_\__delete service***.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0612a-163">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="0612a-163">Input parameters</span></span>

- <span data-ttu-id="0612a-164">**object_ptr** Puntatore all'oggetto da deallocare.</span><span class="sxs-lookup"><span data-stu-id="0612a-164">**object_ptr** Object pointer to deallocate.</span></span>

### <a name="return-values"></a><span data-ttu-id="0612a-165">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="0612a-165">Return values</span></span>

- <span data-ttu-id="0612a-166">**TX_SUCCESS** (0x00) allocare l'oggetto riuscito.</span><span class="sxs-lookup"><span data-stu-id="0612a-166">**TX_SUCCESS** (0x00) Successful object allocate.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0612a-167">Consentito da</span><span class="sxs-lookup"><span data-stu-id="0612a-167">Allowed from</span></span>

<span data-ttu-id="0612a-168">Thread del modulo</span><span class="sxs-lookup"><span data-stu-id="0612a-168">Module threads</span></span>

### <a name="example"></a><span data-ttu-id="0612a-169">Esempio</span><span class="sxs-lookup"><span data-stu-id="0612a-169">Example</span></span>

```c
TX_QUEUE *queue_pointer;

/* Deallocate control block for a module message queue. */
status = txm_module_object_deallocate(queue_pointer);

/* If status is TX_SUCCESS the object memory associated
   with queue_pointer is deallocated. */
```

### <a name="see-also"></a><span data-ttu-id="0612a-170">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0612a-170">See also</span></span>

- <span data-ttu-id="0612a-171">txm_module_object_allocate</span><span class="sxs-lookup"><span data-stu-id="0612a-171">txm_module_object_allocate</span></span>
- <span data-ttu-id="0612a-172">txm_module_object_pointer_get</span><span class="sxs-lookup"><span data-stu-id="0612a-172">txm_module_object_pointer_get</span></span>

---

## <a name="txm_module_object_pointer_get"></a><span data-ttu-id="0612a-173">txm_module_object_pointer_get</span><span class="sxs-lookup"><span data-stu-id="0612a-173">txm_module_object_pointer_get</span></span>

<span data-ttu-id="0612a-174">Trovare un oggetto di sistema e recuperare il puntatore all'oggetto</span><span class="sxs-lookup"><span data-stu-id="0612a-174">Find system object and retrieve object pointer</span></span>

### <a name="prototype"></a><span data-ttu-id="0612a-175">Prototipo</span><span class="sxs-lookup"><span data-stu-id="0612a-175">Prototype</span></span>

```c
UINT txm_module_object_pointer_get(
   UINT object_type, CHAR *name, 
   VOID **object_ptr);
```

### <a name="description"></a><span data-ttu-id="0612a-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0612a-176">Description</span></span>

<span data-ttu-id="0612a-177">Questo servizio recupera il puntatore all'oggetto di un determinato tipo con un nome specifico.</span><span class="sxs-lookup"><span data-stu-id="0612a-177">This service retrieves the object pointer of a particular type with a particular name.</span></span> <span data-ttu-id="0612a-178">Se l'oggetto non viene trovato, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="0612a-178">If the object is not found, an error is returned.</span></span> <span data-ttu-id="0612a-179">In caso contrario, se l'oggetto viene trovato, l'indirizzo di quell'oggetto viene inserito in "object_ptr".</span><span class="sxs-lookup"><span data-stu-id="0612a-179">Otherwise, if the object is found, the address of that object is placed in "object_ptr."</span></span> <span data-ttu-id="0612a-180">Questo puntatore può quindi essere usato per effettuare chiamate al servizio di sistema, per interagire con il codice residente e/o altri moduli caricati nel sistema.</span><span class="sxs-lookup"><span data-stu-id="0612a-180">This pointer can then be used to make system service calls, to interact with the resident code, and/or other loaded modules in the system.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0612a-181">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="0612a-181">Input parameters</span></span>

- <span data-ttu-id="0612a-182">**object_type** Tipo di oggetto ThreadX richiesto.</span><span class="sxs-lookup"><span data-stu-id="0612a-182">**object_type** Type of ThreadX object requested.</span></span> <span data-ttu-id="0612a-183">I tipi validi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="0612a-183">Valid types are as follows:</span></span>
  - <span data-ttu-id="0612a-184">TXM_BLOCK_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-184">TXM_BLOCK_POOL_OBJECT</span></span>
  - <span data-ttu-id="0612a-185">TXM_BYTE_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-185">TXM_BYTE_POOL_OBJECT</span></span>
  - <span data-ttu-id="0612a-186">TXM_EVENT_FLAGS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-186">TXM_EVENT_FLAGS_OBJECT</span></span>
  - <span data-ttu-id="0612a-187">TXM_MUTEX_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-187">TXM_MUTEX_OBJECT</span></span>
  - <span data-ttu-id="0612a-188">TXM_QUEUE_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-188">TXM_QUEUE_OBJECT</span></span>
  - <span data-ttu-id="0612a-189">TXM_SEMAPHORE_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-189">TXM_SEMAPHORE_OBJECT</span></span>
  - <span data-ttu-id="0612a-190">TXM_THREAD_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-190">TXM_THREAD_OBJECT</span></span>
  - <span data-ttu-id="0612a-191">TXM_TIMER_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-191">TXM_TIMER_OBJECT</span></span>
  - <span data-ttu-id="0612a-192">TXM_IP_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-192">TXM_IP_OBJECT</span></span>
  - <span data-ttu-id="0612a-193">TXM_PACKET_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-193">TXM_PACKET_POOL_OBJECT</span></span>
  - <span data-ttu-id="0612a-194">TXM_UDP_SOCKET_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-194">TXM_UDP_SOCKET_OBJECT</span></span>
  - <span data-ttu-id="0612a-195">TXM_TCP_SOCKET_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-195">TXM_TCP_SOCKET_OBJECT</span></span>
- <span data-ttu-id="0612a-196">**nome** Nome dell'oggetto specifico dell'applicazione come definito al momento della creazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="0612a-196">**name** Application-specific object name as defined when the object was created.</span></span>
- <span data-ttu-id="0612a-197">**object_ptr** Destinazione per il puntatore all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="0612a-197">**object_ptr** Destination for object pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="0612a-198">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="0612a-198">Return values</span></span>

- <span data-ttu-id="0612a-199">**TX_SUCCESS** (0x00) oggetto riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="0612a-199">**TX_SUCCESS** (0x00) Successful object get.</span></span>
- <span data-ttu-id="0612a-200">Il tipo di oggetto **TX_OPTION_ERROR** (0x08) non è valido.</span><span class="sxs-lookup"><span data-stu-id="0612a-200">**TX_OPTION_ERROR** (0x08) Invalid object type.</span></span>
- <span data-ttu-id="0612a-201">**TX_PTR_ERROR** (0x03) destinazione non valida.</span><span class="sxs-lookup"><span data-stu-id="0612a-201">**TX_PTR_ERROR** (0x03) Invalid destination.</span></span>
- <span data-ttu-id="0612a-202">Dimensioni **TX_SIZE_ERROR** (0x05) non valide.</span><span class="sxs-lookup"><span data-stu-id="0612a-202">**TX_SIZE_ERROR** (0x05) Invalid size.</span></span>
- <span data-ttu-id="0612a-203">Impossibile trovare l'oggetto **TX_NO_INSTANCE** (0x0D).</span><span class="sxs-lookup"><span data-stu-id="0612a-203">**TX_NO_INSTANCE** (0x0D) Object not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0612a-204">Consentito da</span><span class="sxs-lookup"><span data-stu-id="0612a-204">Allowed from</span></span>

<span data-ttu-id="0612a-205">Thread del modulo</span><span class="sxs-lookup"><span data-stu-id="0612a-205">Module threads</span></span>

### <a name="example"></a><span data-ttu-id="0612a-206">Esempio</span><span class="sxs-lookup"><span data-stu-id="0612a-206">Example</span></span>

```c
TX_QUEUE *queue_pointer;

/* Find the pointer for "fft_queue" in the resident part
   of the application. */
status = txm_module_object_pointer_get(TXM_QUEUE_OBJECT,
         "fft_queue", &queue_pointer);

/* If status is TX_SUCCESS the found queue pointer is in
   "queue_pointer". This queue pointer can then be used to
   send messages to the "fft_queue." */
```

### <a name="see-also"></a><span data-ttu-id="0612a-207">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0612a-207">See also</span></span>

- <span data-ttu-id="0612a-208">txm_module_manager_object_pointer_get_extended</span><span class="sxs-lookup"><span data-stu-id="0612a-208">txm_module_manager_object_pointer_get_extended</span></span>

---

## <a name="txm_module_object_pointer_get_extended"></a><span data-ttu-id="0612a-209">txm_module_object_pointer_get_extended</span><span class="sxs-lookup"><span data-stu-id="0612a-209">txm_module_object_pointer_get_extended</span></span>

<span data-ttu-id="0612a-210">Trovare un oggetto di sistema e recuperare il puntatore all'oggetto</span><span class="sxs-lookup"><span data-stu-id="0612a-210">Find system object and retrieve object pointer</span></span>

### <a name="prototype"></a><span data-ttu-id="0612a-211">Prototipo</span><span class="sxs-lookup"><span data-stu-id="0612a-211">Prototype</span></span>

```c
UINT txm_module_object_pointer_get_extended(UINT object_type,
                                            CHAR *name,
                                            UINT name_length,
                                            VOID **object_ptr);
```

### <a name="description"></a><span data-ttu-id="0612a-212">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0612a-212">Description</span></span>

<span data-ttu-id="0612a-213">Questo servizio recupera il puntatore all'oggetto di un determinato tipo con un nome specifico.</span><span class="sxs-lookup"><span data-stu-id="0612a-213">This service retrieves the object pointer of a particular type with a particular name.</span></span> <span data-ttu-id="0612a-214">Se l'oggetto non viene trovato, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="0612a-214">If the object is not found, an error is returned.</span></span> <span data-ttu-id="0612a-215">In caso contrario, se l'oggetto viene trovato, l'indirizzo di quell'oggetto viene inserito in "object_ptr".</span><span class="sxs-lookup"><span data-stu-id="0612a-215">Otherwise, if the object is found, the address of that object is placed in "object_ptr."</span></span> <span data-ttu-id="0612a-216">Questo puntatore può quindi essere usato per effettuare chiamate al servizio di sistema, per interagire con il codice residente e/o altri moduli caricati nel sistema.</span><span class="sxs-lookup"><span data-stu-id="0612a-216">This pointer can then be used to make system service calls, to interact with the resident code, and/or other loaded modules in the system.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="0612a-217">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="0612a-217">Input parameters</span></span>

- <span data-ttu-id="0612a-218">**object_type** Tipo di oggetto ThreadX richiesto.</span><span class="sxs-lookup"><span data-stu-id="0612a-218">**object_type** Type of ThreadX object requested.</span></span> <span data-ttu-id="0612a-219">I tipi validi sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="0612a-219">Valid types are as follows:</span></span>
  - <span data-ttu-id="0612a-220">TXM_BLOCK_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-220">TXM_BLOCK_POOL_OBJECT</span></span>
  - <span data-ttu-id="0612a-221">TXM_BYTE_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-221">TXM_BYTE_POOL_OBJECT</span></span>
  - <span data-ttu-id="0612a-222">TXM_EVENT_FLAGS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-222">TXM_EVENT_FLAGS_OBJECT</span></span>
  - <span data-ttu-id="0612a-223">TXM_MUTEX_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-223">TXM_MUTEX_OBJECT</span></span>
  - <span data-ttu-id="0612a-224">TXM_QUEUE_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-224">TXM_QUEUE_OBJECT</span></span>
  - <span data-ttu-id="0612a-225">TXM_SEMAPHORE_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-225">TXM_SEMAPHORE_OBJECT</span></span>
  - <span data-ttu-id="0612a-226">TXM_THREAD_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-226">TXM_THREAD_OBJECT</span></span>
  - <span data-ttu-id="0612a-227">TXM_TIMER_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-227">TXM_TIMER_OBJECT</span></span>
  - <span data-ttu-id="0612a-228">TXM_IP_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-228">TXM_IP_OBJECT</span></span>
  - <span data-ttu-id="0612a-229">TXM_PACKET_POOL_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-229">TXM_PACKET_POOL_OBJECT</span></span>
  - <span data-ttu-id="0612a-230">TXM_UDP_SOCKET_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-230">TXM_UDP_SOCKET_OBJECT</span></span>
  - <span data-ttu-id="0612a-231">TXM_TCP_SOCKET_OBJECT</span><span class="sxs-lookup"><span data-stu-id="0612a-231">TXM_TCP_SOCKET_OBJECT</span></span>
- <span data-ttu-id="0612a-232">**nome** Nome dell'oggetto specifico dell'applicazione come definito al momento della creazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="0612a-232">**name** Application-specific object name as defined when the object was created.</span></span>
- <span data-ttu-id="0612a-233">**name_length** Lunghezza del nome.</span><span class="sxs-lookup"><span data-stu-id="0612a-233">**name_length** Length of name.</span></span>
- <span data-ttu-id="0612a-234">**object_ptr** Destinazione per il puntatore all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="0612a-234">**object_ptr** Destination for object pointer.</span></span>

### <a name="return-values"></a><span data-ttu-id="0612a-235">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="0612a-235">Return values</span></span>

- <span data-ttu-id="0612a-236">**TX_SUCCESS** (0x00) oggetto riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="0612a-236">**TX_SUCCESS** (0x00) Successful object get.</span></span>
- <span data-ttu-id="0612a-237">Il tipo di oggetto **TX_OPTION_ERROR** (0x08) non è valido.</span><span class="sxs-lookup"><span data-stu-id="0612a-237">**TX_OPTION_ERROR** (0x08) Invalid object type.</span></span>
- <span data-ttu-id="0612a-238">**TX_PTR_ERROR** (0x03) destinazione non valida.</span><span class="sxs-lookup"><span data-stu-id="0612a-238">**TX_PTR_ERROR** (0x03) Invalid destination.</span></span>
- <span data-ttu-id="0612a-239">Dimensioni **TX_SIZE_ERROR** (0x05) non valide.</span><span class="sxs-lookup"><span data-stu-id="0612a-239">**TX_SIZE_ERROR** (0x05) Invalid size.</span></span>
- <span data-ttu-id="0612a-240">Impossibile trovare l'oggetto **TX_NO_INSTANCE** (0x0D).</span><span class="sxs-lookup"><span data-stu-id="0612a-240">**TX_NO_INSTANCE** (0x0D) Object not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="0612a-241">Consentito da</span><span class="sxs-lookup"><span data-stu-id="0612a-241">Allowed from</span></span>

<span data-ttu-id="0612a-242">Thread del modulo</span><span class="sxs-lookup"><span data-stu-id="0612a-242">Module threads</span></span>

### <a name="example"></a><span data-ttu-id="0612a-243">Esempio</span><span class="sxs-lookup"><span data-stu-id="0612a-243">Example</span></span>

```c
TX_QUEUE *queue_pointer;

/* Find the pointer for "fft_queue" in the resident part
   of the application. */
   status = txm_module_object_pointer_get_extended(TXM_QUEUE_OBJECT,
            "fft_queue", 9, &queue_pointer);

/* If status is TX_SUCCESS the found queue pointer is in
   "queue_pointer". This queue pointer can then be used to
   send messages to the "fft_queue." */
```

### <a name="see-also"></a><span data-ttu-id="0612a-244">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0612a-244">See also</span></span>

- <span data-ttu-id="0612a-245">txm_module_manager_object_pointer_get</span><span class="sxs-lookup"><span data-stu-id="0612a-245">txm_module_manager_object_pointer_get</span></span>
