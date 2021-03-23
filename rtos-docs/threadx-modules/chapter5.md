---
title: Capitolo 5-API di gestione moduli
author: philmea
description: Questo articolo è un riepilogo delle API di gestione dei moduli disponibili per la parte residente dell'applicazione.
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ca0fee443c23fd1bdd34651f4a7b31cf71f886f0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821389"
---
# <a name="chapter-5---module-manager-apis"></a><span data-ttu-id="ffae3-103">Capitolo 5-API di gestione moduli</span><span class="sxs-lookup"><span data-stu-id="ffae3-103">Chapter 5 - Module Manager APIs</span></span>

## <a name="summary-of-module-manager-apis"></a><span data-ttu-id="ffae3-104">Riepilogo delle API di gestione dei moduli</span><span class="sxs-lookup"><span data-stu-id="ffae3-104">Summary of Module Manager APIs</span></span>

<span data-ttu-id="ffae3-105">Sono disponibili diverse API aggiuntive per la parte residente dell'applicazione, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ffae3-105">There are several additional APIs available to the resident portion of the application, as follows.</span></span>

- <span data-ttu-id="ffae3-106">\***txm_module_manager_external_memory_enable** _-_Enable accedere al modulo a uno spazio di memoria condiviso \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-106">***txm_module_manager_external_memory_enable** _ - _Enable module access to a shared memory space*</span></span>
- <span data-ttu-id="ffae3-107">\***txm_module_manager_file_load** il modulo _-_Load dal file tramite FILEX \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-107">***txm_module_manager_file_load** _ - _Load module from file via FileX*</span></span>
- <span data-ttu-id="ffae3-108">\***txm_module_manager_in_place_load** _-_Load dati del modulo, eseguire sul posto \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-108">***txm_module_manager_in_place_load** _ - _Load module data, execute in place*</span></span>
- <span data-ttu-id="ffae3-109">\***txm_module_manager_initialize** _-_Initialize gestione moduli \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-109">***txm_module_manager_initialize** _ - _Initialize the module manager*</span></span>
- <span data-ttu-id="ffae3-110">\***txm_module_manager_mm_initialize** _-_Initialize l'hardware di gestione della memoria \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-110">***txm_module_manager_mm_initialize** _ - _Initialize the memory management hardware*</span></span>
- <span data-ttu-id="ffae3-111">\***txm_module_manager_maximum_module_priority_set** _-_Set priorità massima consentita per il thread in un modulo \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-111">***txm_module_manager_maximum_module_priority_set** _ - _Set the maximum thread priority allowed in a module*</span></span>
- <span data-ttu-id="ffae3-112">\***txm_module_manager_memory_fault_notify** _-_Register un callback dell'applicazione in un errore di memoria \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-112">***txm_module_manager_memory_fault_notify** _ - _Register an application callback on memory fault*</span></span>
- <span data-ttu-id="ffae3-113">\***txm_module_manager_memory_load** _-_Load il modulo dalla memoria \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-113">***txm_module_manager_memory_load** _ - _Load the module from memory*</span></span>
- <span data-ttu-id="ffae3-114">\***txm_module_manager_object_pool_create** _-_Create un pool di oggetti per i moduli \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-114">***txm_module_manager_object_pool_create** _ - _Create an object pool for modules*</span></span>
- <span data-ttu-id="ffae3-115">\***txm_module_manager_properties_get** _-_Get proprietà del modulo \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-115">***txm_module_manager_properties_get** _ - _Get module properties*</span></span>
- <span data-ttu-id="ffae3-116">\***txm_module_manager_start** _-_Start l'esecuzione del modulo specificato \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-116">***txm_module_manager_start** _ - _Start execution of the specified module*</span></span>
- <span data-ttu-id="ffae3-117">\***txm_module_manager_stop** _-_Stop l'esecuzione del modulo specificato \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-117">***txm_module_manager_stop** _ - _Stop execution of the specified module*</span></span>
- <span data-ttu-id="ffae3-118">\***txm_module_manager_unload** _-_Unload il modulo \*</span><span class="sxs-lookup"><span data-stu-id="ffae3-118">***txm_module_manager_unload** _ - _Unload the module*</span></span>

---

## <a name="txm_module_manager_external_memory_enable"></a><span data-ttu-id="ffae3-119">txm_module_manager_external_memory_enable</span><span class="sxs-lookup"><span data-stu-id="ffae3-119">txm_module_manager_external_memory_enable</span></span>

<span data-ttu-id="ffae3-120">Abilitare il modulo per accedere a uno spazio di memoria condiviso.</span><span class="sxs-lookup"><span data-stu-id="ffae3-120">Enable module to access a shared memory space.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-121">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-121">Prototype</span></span>

```c
UINT txm_module_manager_external_memory_enable(
     TXM_MODULE_INSTANCE *module_instance,
     VOID *start_address,
     ULONG length,
     UINT attributes);
```

### <a name="description"></a><span data-ttu-id="ffae3-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-122">Description</span></span>

<span data-ttu-id="ffae3-123">Questo servizio crea una voce nella tabella hardware di gestione della memoria per un'area di memoria condivisa a cui il modulo può accedere.</span><span class="sxs-lookup"><span data-stu-id="ffae3-123">This service creates an entry in the memory management hardware table for a shared memory region that the module can access.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-124">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-124">Input parameters</span></span>

- <span data-ttu-id="ffae3-125">**module_instance** Puntatore all'istanza del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-125">**module_instance** Pointer to the instance of the module.</span></span>
- <span data-ttu-id="ffae3-126">**start_address** Indirizzo iniziale dell'area di memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="ffae3-126">**start_address** Starting address of shared memory region.</span></span>
- <span data-ttu-id="ffae3-127">**lunghezza** Lunghezza dell'area di memoria condivisa.</span><span class="sxs-lookup"><span data-stu-id="ffae3-127">**length** Length of shared memory region.</span></span>
- <span data-ttu-id="ffae3-128">**attributi** di Attributi dell'area di memoria (cache, lettura, scrittura e così via).</span><span class="sxs-lookup"><span data-stu-id="ffae3-128">**attributes** Attributes of memory region (cache, read, write, etc.).</span></span> <span data-ttu-id="ffae3-129">Gli attributi sono specifici della porta; vedere [appendice](appendix.md) per formato attributi.</span><span class="sxs-lookup"><span data-stu-id="ffae3-129">Attributes are port-specific; see [appendix](appendix.md) for attributes format.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-130">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-130">Return values</span></span>

- <span data-ttu-id="ffae3-131">Creazione della voce di memoria **TX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="ffae3-131">**TX_SUCCESS** (0x00) Memory entry created successfully.</span></span>
- <span data-ttu-id="ffae3-132">Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata o funzionalità non disponibile.</span><span class="sxs-lookup"><span data-stu-id="ffae3-132">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized or feature not available.</span></span>
- <span data-ttu-id="ffae3-133">L'istanza del modulo **TX_PTR_ERROR** (0X03) non è valida.</span><span class="sxs-lookup"><span data-stu-id="ffae3-133">**TX_PTR_ERROR** (0x03) Invalid module instance.</span></span>
- <span data-ttu-id="ffae3-134">Il modulo **TX_START_ERROR** (0x10) non è in stato caricato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-134">**TX_START_ERROR** (0x10) Module not in loaded state.</span></span>
- <span data-ttu-id="ffae3-135">**TXM_MODULE_ALIGNMENT_ERROR** (0xF0) non valido per l'allineamento degli indirizzi iniziali.</span><span class="sxs-lookup"><span data-stu-id="ffae3-135">**TXM_MODULE_ALIGNMENT_ERROR** (0xF0) Invalid start address alignment.</span></span>
- <span data-ttu-id="ffae3-136">Proprietà incompatibili **TXM_MODULE_INVALID_PROPERTIES** (0xf3).</span><span class="sxs-lookup"><span data-stu-id="ffae3-136">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) Incompatible properties.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-137">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-137">Allowed from</span></span>

<span data-ttu-id="ffae3-138">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-138">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-139">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-139">Example</span></span>

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Create a shared memory space 256 bytes long at address 0x64005000
   with read & write, no execute, outer & inner write back cache
   attributes. Note that these attributes are port-specific. */
txm_module_manager_external_memory_enable(&my_module, (VOID*)0x64005000, 256, 0x3F);
```

---

## <a name="txm_module_manager_file_load"></a><span data-ttu-id="ffae3-140">txm_module_manager_file_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-140">txm_module_manager_file_load</span></span>

<span data-ttu-id="ffae3-141">Caricare il modulo dal file tramite FileX.</span><span class="sxs-lookup"><span data-stu-id="ffae3-141">Load module from file via FileX.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-142">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-142">Prototype</span></span>

```c
UINT txm_module_manager_file_load(
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```

### <a name="description"></a><span data-ttu-id="ffae3-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-143">Description</span></span>

<span data-ttu-id="ffae3-144">Questo servizio carica l'immagine binaria del modulo contenuto nel file specificato nell'area di memoria del modulo e la prepara per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ffae3-144">This service loads the binary image of the module contained in the specified file into the module memory area and prepares it for execution.</span></span> <span data-ttu-id="ffae3-145">Si presuppone che il supporto fornito sia già aperto.</span><span class="sxs-lookup"><span data-stu-id="ffae3-145">It is assumed that the supplied media is already opened.</span></span>

> [!NOTE]
> <span data-ttu-id="ffae3-146">Il sistema FileX viene usato per caricare il file.</span><span class="sxs-lookup"><span data-stu-id="ffae3-146">The FileX system is utilized to load the file.</span></span> <span data-ttu-id="ffae3-147">Per abilitare l'accesso FileX, è necessario compilare il modulo, la libreria di moduli, il gestore dei moduli e la libreria ThreadX (con le origini di Module Manager) con **FX_FILEX_PRESENT** definito nei progetti.</span><span class="sxs-lookup"><span data-stu-id="ffae3-147">In order to enable FileX access, the module, module library, Module Manager and the ThreadX library (with the Module Manager sources) must be built with **FX_FILEX_PRESENT** defined in the projects.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-148">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-148">Input parameters</span></span>

- <span data-ttu-id="ffae3-149">**module_instance** Puntatore all'istanza del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-149">**module_instance** Pointer to the instance of the module.</span></span>
- <span data-ttu-id="ffae3-150">**module_name** Nome del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-150">**module_name** Name of the module.</span></span>
- <span data-ttu-id="ffae3-151">**media_ptr** Puntatore ai supporti FileX già aperti.</span><span class="sxs-lookup"><span data-stu-id="ffae3-151">**media_ptr** Pointer to already opened FileX media.</span></span>
- <span data-ttu-id="ffae3-152">**file_name** Nome del file binario del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-152">**file_name** Name of module's binary file.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-153">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-153">Return values</span></span>

- <span data-ttu-id="ffae3-154">Il caricamento del modulo **TX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="ffae3-154">**TX_SUCCESS** (0x00) Successful module load.</span></span>
- <span data-ttu-id="ffae3-155">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-155">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="ffae3-156">Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.</span><span class="sxs-lookup"><span data-stu-id="ffae3-156">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="ffae3-157">**TX_NO_MEMORY** (0x10) memoria insufficiente per caricare il modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-157">**TX_NO_MEMORY** (0x10) Not enough memory to load module.</span></span>
- <span data-ttu-id="ffae3-158">Il supporto **TX_NOT_DONE** (0x20) non è aperto, il file non è stato trovato o il file non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-158">**TX_NOT_DONE** (0x20) Media not open, file not found or file is invalid.</span></span>
- <span data-ttu-id="ffae3-159">Puntatore al modulo **TX_PTR_ERROR** (0X03) non valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-159">**TX_PTR_ERROR** (0x03) Invalid module pointer.</span></span>
- <span data-ttu-id="ffae3-160">Allineamento di **TXM_MODULE_ALIGNMENT_ERROR** (0xF0) non valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-160">**TXM_MODULE_ALIGNMENT_ERROR** (0xF0) Invalid alignment.</span></span>
- <span data-ttu-id="ffae3-161">Il modulo **TXM_MODULE_ALREADY_LOADED** (0xF1) è già caricato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-161">**TXM_MODULE_ALREADY_LOADED** (0xF1) Module already loaded.</span></span>
- <span data-ttu-id="ffae3-162">**TXM_MODULE_INVALID** (0xF2) | Preambolo del modulo non valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-162">**TXM_MODULE_INVALID** (0xF2) | Invalid module preamble.</span></span>
- <span data-ttu-id="ffae3-163">Proprietà incompatibili **TXM_MODULE_INVALID_PROPERTIES** (0xf3).</span><span class="sxs-lookup"><span data-stu-id="ffae3-163">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) Incompatible properties.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-164">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-164">Allowed from</span></span>

<span data-ttu-id="ffae3-165">Thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-165">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-166">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-166">Example</span></span>

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager. */
status = txm_module_manager_initialize((VOID*)0x64010000,0x10000);

/* Load the module from a binary file. */
status = txm_module_manager_file_load(&my_module, "my module",
                                      &sdio_disk, "demo_thread_module.bin");

/* Start the module. */
status = txm_module_manager_start(&my_module);
```

### <a name="see-also"></a><span data-ttu-id="ffae3-167">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ffae3-167">See also</span></span>

- <span data-ttu-id="ffae3-168">txm_module_manager_in_place_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-168">txm_module_manager_in_place_load</span></span>
- <span data-ttu-id="ffae3-169">txm_module_manager_memory_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-169">txm_module_manager_memory_load</span></span>
- <span data-ttu-id="ffae3-170">txm_module_manager_unload</span><span class="sxs-lookup"><span data-stu-id="ffae3-170">txm_module_manager_unload</span></span>

---

## <a name="txm_module_manager_in_place_load"></a><span data-ttu-id="ffae3-171">txm_module_manager_in_place_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-171">txm_module_manager_in_place_load</span></span>

<span data-ttu-id="ffae3-172">Caricare solo i dati del modulo, eseguire il modulo in un percorso esistente.</span><span class="sxs-lookup"><span data-stu-id="ffae3-172">Load module data only, execute module in existing location.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-173">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-173">Prototype</span></span>

```c
UINT txm_module_manager_in_place_load(
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    VOID *location);
```

### <a name="description"></a><span data-ttu-id="ffae3-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-174">Description</span></span>

<span data-ttu-id="ffae3-175">Questo servizio carica l'area dati del modulo solo nell'area di memoria del modulo e la prepara per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ffae3-175">This service loads the module's data area only into the module memory area and prepares it for execution.</span></span> <span data-ttu-id="ffae3-176">L'esecuzione del codice del modulo sarà sul posto, ovvero dall'offset degli indirizzi specificato dal preambolo del modulo nella posizione specificata.</span><span class="sxs-lookup"><span data-stu-id="ffae3-176">Module code execution will be in-place, that is, from the address offset specified by the module preamble at the supplied location.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-177">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-177">Input parameters</span></span>

- <span data-ttu-id="ffae3-178">**module_instance** Puntatore all'istanza del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-178">**module_instance** Pointer to the instance of the module.</span></span>
- <span data-ttu-id="ffae3-179">**module_name** Nome del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-179">**module_name** Name of the module.</span></span>
- <span data-ttu-id="ffae3-180">**posizione** Puntatore all'area di codice del modulo, preambolo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-180">**location** Pointer to module's code area, preamble first.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-181">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-181">Return values</span></span>

- <span data-ttu-id="ffae3-182">Il caricamento del modulo **TX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="ffae3-182">**TX_SUCCESS** (0x00) Successful module load.</span></span>
- <span data-ttu-id="ffae3-183">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-183">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="ffae3-184">Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.</span><span class="sxs-lookup"><span data-stu-id="ffae3-184">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="ffae3-185">**TX_NO_MEMORY** (0x10) memoria insufficiente per caricare il modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-185">**TX_NO_MEMORY** (0x10) Not enough memory to load module.</span></span>
- <span data-ttu-id="ffae3-186">**TX_PTR_ERROR** (0x03) puntatore non valido, istanza del modulo o preambolo del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-186">**TX_PTR_ERROR** (0x03) Invalid pointer, module instance, or module preamble.</span></span>
- <span data-ttu-id="ffae3-187">Allineamento di **TXM_MODULE_ALIGNMENT_ERROR** (0xF0) non valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-187">**TXM_MODULE_ALIGNMENT_ERROR** (0xF0) Invalid alignment.</span></span>
- <span data-ttu-id="ffae3-188">Il modulo **TXM_MODULE_ALREADY_LOADED** (0xF1) è già caricato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-188">**TXM_MODULE_ALREADY_LOADED** (0xF1) Module already loaded.</span></span>
- <span data-ttu-id="ffae3-189">Preambolo del modulo **TXM_MODULE_INVALID** (0XF2) non valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-189">**TXM_MODULE_INVALID** (0xF2) Invalid module preamble.</span></span>
- <span data-ttu-id="ffae3-190">Proprietà incompatibili **TXM_MODULE_INVALID_PROPERTIES** (0xf3).</span><span class="sxs-lookup"><span data-stu-id="ffae3-190">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) Incompatible properties.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-191">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-191">Allowed from</span></span>

<span data-ttu-id="ffae3-192">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-192">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-193">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-193">Example</span></span>

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Start the module. */
txm_module_manager_start(&my_module);
```

### <a name="see-also"></a><span data-ttu-id="ffae3-194">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ffae3-194">See also</span></span>

- <span data-ttu-id="ffae3-195">txm_module_manager_file_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-195">txm_module_manager_file_load</span></span>
- <span data-ttu-id="ffae3-196">txm_module_manager_memory_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-196">txm_module_manager_memory_load</span></span>
- <span data-ttu-id="ffae3-197">txm_module_manager_unload</span><span class="sxs-lookup"><span data-stu-id="ffae3-197">txm_module_manager_unload</span></span>

---

## <a name="txm_module_manager_initialize"></a><span data-ttu-id="ffae3-198">txm_module_manager_initialize</span><span class="sxs-lookup"><span data-stu-id="ffae3-198">txm_module_manager_initialize</span></span>

<span data-ttu-id="ffae3-199">Inizializzare Gestione moduli.</span><span class="sxs-lookup"><span data-stu-id="ffae3-199">Initialize the module manager.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-200">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-200">Prototype</span></span>

```c
UINT txm_module_manager_initialize(
    VOID *module_memory_start,
    ULONG module_memory_size);
```

### <a name="description"></a><span data-ttu-id="ffae3-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-201">Description</span></span>

<span data-ttu-id="ffae3-202">Questo servizio Inizializza le risorse interne di gestione moduli, inclusa l'area di memoria usata per il caricamento dei moduli.</span><span class="sxs-lookup"><span data-stu-id="ffae3-202">This service initializes the Module Manager's internal resources, including the memory area used for loading modules.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-203">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-203">Input parameters</span></span>

- <span data-ttu-id="ffae3-204">**module_memory_start** Puntatore all'inizio della memoria del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-204">**module_memory_start** Pointer to the start of module memory.</span></span>
- <span data-ttu-id="ffae3-205">**module_memory_size** Dimensioni in byte della memoria del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-205">**module_memory_size** Size in bytes of the module memory.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-206">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-206">Return values</span></span>

- <span data-ttu-id="ffae3-207">**TX_SUCCESS** (0x00) inizializzazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="ffae3-207">**TX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="ffae3-208">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-208">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-209">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-209">Allowed from</span></span>

<span data-ttu-id="ffae3-210">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-210">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-211">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-211">Example</span></span>

```c
/* Initialize the module manager with 64KB of RAM starting at
   address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);
```

### <a name="see-also"></a><span data-ttu-id="ffae3-212">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ffae3-212">See also</span></span>

- <span data-ttu-id="ffae3-213">txm_module_manager_object_pool_create</span><span class="sxs-lookup"><span data-stu-id="ffae3-213">txm_module_manager_object_pool_create</span></span>

---

## <a name="txm_module_manager_initialize_mmu"></a><span data-ttu-id="ffae3-214">txm_module_manager_initialize_mmu</span><span class="sxs-lookup"><span data-stu-id="ffae3-214">txm_module_manager_initialize_mmu</span></span>

<span data-ttu-id="ffae3-215">Inizializzare l'hardware di gestione della memoria.</span><span class="sxs-lookup"><span data-stu-id="ffae3-215">Initialize the memory management hardware.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-216">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-216">Prototype</span></span>

```c
UINT txm_module_manager_initialize_mmu(VOID);
```

### <a name="description"></a><span data-ttu-id="ffae3-217">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-217">Description</span></span>

<span data-ttu-id="ffae3-218">Questo servizio Inizializza la MMU.</span><span class="sxs-lookup"><span data-stu-id="ffae3-218">This service initializes the MMU.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-219">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-219">Input parameters</span></span>

<span data-ttu-id="ffae3-220">Nessuno</span><span class="sxs-lookup"><span data-stu-id="ffae3-220">none</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-221">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-221">Return values</span></span>

- <span data-ttu-id="ffae3-222">**TX_SUCCESS** (0x00) inizializzazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="ffae3-222">**TX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="ffae3-223">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-223">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-224">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-224">Allowed from</span></span>

<span data-ttu-id="ffae3-225">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-225">Initialization and Threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-226">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-226">Example</span></span>

```c
/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Initialize the MMU. */
txm_module_manager_initialize_mmu();
```

---

## <a name="txm_module_manager_maximum_module_priority_set"></a><span data-ttu-id="ffae3-227">txm_module_manager_maximum_module_priority_set</span><span class="sxs-lookup"><span data-stu-id="ffae3-227">txm_module_manager_maximum_module_priority_set</span></span>

<span data-ttu-id="ffae3-228">Imposta la priorità massima dei thread consentita in un modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-228">Set the maximum thread priority allowed in a module.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-229">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-229">Prototype</span></span>

```c
UINT txm_module_manager_maximum_module_priority_set(
         TXM_MODULE_INSTANCE *module_instance,
         UINT priority);
```

### <a name="description"></a><span data-ttu-id="ffae3-230">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-230">Description</span></span>

<span data-ttu-id="ffae3-231">Questo servizio imposta la priorità massima dei thread consentita in un modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-231">This service sets the maximum thread priority allowed in a module.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-232">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-232">Input parameters</span></span>

- <span data-ttu-id="ffae3-233">**module_instance** Puntatore all'istanza del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-233">**module_instance** Pointer to the instance of the module.</span></span>
- <span data-ttu-id="ffae3-234">**priorità** di Priorità massima thread.</span><span class="sxs-lookup"><span data-stu-id="ffae3-234">**priority** Maximum thread priority.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-235">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-235">Return values</span></span>

- <span data-ttu-id="ffae3-236">**TX_SUCCESS** (0x00) inizializzazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="ffae3-236">**TX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="ffae3-237">Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.</span><span class="sxs-lookup"><span data-stu-id="ffae3-237">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="ffae3-238">L'istanza del modulo **TX_PTR_ERROR** (0X03) non è valida.</span><span class="sxs-lookup"><span data-stu-id="ffae3-238">**TX_PTR_ERROR** (0x03) Invalid module instance.</span></span>
- <span data-ttu-id="ffae3-239">Il modulo **TX_START_ERROR** (0x10) non è in stato caricato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-239">**TX_START_ERROR** (0x10) Module not in loaded state.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-240">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-240">Allowed from</span></span>

<span data-ttu-id="ffae3-241">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-241">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-242">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-242">Example</span></span>

```c
/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Set the maximum thread priority in my_module to 5. */
txm_module_manager_maximum_module_priority_set(&my_module, 5);
```

---

## <a name="txm_module_manager_memory_fault_notify"></a><span data-ttu-id="ffae3-243">txm_module_manager_memory_fault_notify</span><span class="sxs-lookup"><span data-stu-id="ffae3-243">txm_module_manager_memory_fault_notify</span></span>

<span data-ttu-id="ffae3-244">Registrare un callback dell'applicazione in un errore di memoria.</span><span class="sxs-lookup"><span data-stu-id="ffae3-244">Register an application callback on memory fault.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-245">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-245">Prototype</span></span>

```c
UINT txm_module_manager_memory_fault_notify(
     VOID (*notify_function)(TX_THREAD *, MODULE_INSTANCE *));
```

### <a name="description"></a><span data-ttu-id="ffae3-246">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-246">Description</span></span>

<span data-ttu-id="ffae3-247">Questo servizio registra la funzione di callback di notifica di errore di memoria dell'applicazione specificata con gestione moduli.</span><span class="sxs-lookup"><span data-stu-id="ffae3-247">This service registers the specified application memory fault notification callback function with the Module Manager.</span></span> <span data-ttu-id="ffae3-248">Se si verifica un errore di memoria, questa funzione viene chiamata con un puntatore al thread danneggiato e l'istanza del modulo corrispondente al thread danneggiato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-248">If a memory fault occurs, this function is called with a pointer to the offending thread and the module instance corresponding to the offending thread.</span></span> <span data-ttu-id="ffae3-249">L'elaborazione del gestore dei moduli termina automaticamente il thread danneggiato, ma lascia invariati tutti gli altri thread del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-249">The Module Manager processing automatically terminates the offending thread, but leaves any other threads in the module untouched.</span></span> <span data-ttu-id="ffae3-250">Spetta all'applicazione decidere cosa fare con il modulo associato all'errore di memoria.</span><span class="sxs-lookup"><span data-stu-id="ffae3-250">It is up to the application to decide what to do with the module associated with the memory fault.</span></span>

<span data-ttu-id="ffae3-251">Vedere lo struct **_txm_module_manager_memory_fault_info** interno per informazioni specifiche sullo stesso errore di memoria.</span><span class="sxs-lookup"><span data-stu-id="ffae3-251">Please see the internal **_txm_module_manager_memory_fault_info** struct for specific information on the memory fault itself.</span></span>

> [!NOTE]
> <span data-ttu-id="ffae3-252">La funzione di callback di notifica di errore di memoria viene eseguita direttamente dall'eccezione di errore della memoria, quindi è possibile chiamare solo le API ThreadX consentite dalle routine del servizio di interrupt.</span><span class="sxs-lookup"><span data-stu-id="ffae3-252">The memory fault notification callback function is executed directly from the memory fault exception, so only ThreadX APIs Allowed from interrupt service routines can be called.</span></span> <span data-ttu-id="ffae3-253">Pertanto, per arrestare e scaricare il modulo che causa il danneggiamento, il callback di notifica dell'applicazione deve inviare un segnale a un'attività dell'applicazione in modo che il modulo possa essere arrestato e scaricato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-253">Thus, in order to stop and unload the offending module, the application notification callback must send a signal to an application task so that the module can be stopped and unloaded.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-254">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-254">Input parameters</span></span>

- <span data-ttu-id="ffae3-255">**notify_function** Puntatore a funzione al callback di notifica di errore di memoria dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ffae3-255">**notify_function** Function pointer to the application's memory fault notification callback.</span></span> <span data-ttu-id="ffae3-256">Se si specifica un valore NULL, la notifica di errore di memoria viene disabilitata.</span><span class="sxs-lookup"><span data-stu-id="ffae3-256">Supplying a NULL value disables the memory fault notification.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-257">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-257">Return values</span></span>

- <span data-ttu-id="ffae3-258">**TX_SUCCESS** (0x00) registrazione della funzione di notifica riuscita.</span><span class="sxs-lookup"><span data-stu-id="ffae3-258">**TX_SUCCESS** (0x00) Successful notification function registration.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-259">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-259">Allowed from</span></span>

<span data-ttu-id="ffae3-260">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-260">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-261">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-261">Example</span></span>

```c
/* Register a memory fault callback. */
txm_module_manager_memory_fault_notify(my_memory_fault_handler);
```

---

## <a name="txm_module_manager_memory_load"></a><span data-ttu-id="ffae3-262">txm_module_manager_memory_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-262">txm_module_manager_memory_load</span></span>

<span data-ttu-id="ffae3-263">Caricare il modulo dalla memoria.</span><span class="sxs-lookup"><span data-stu-id="ffae3-263">Load module from memory.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-264">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-264">Prototype</span></span>

```c
UINT txm_module_manager_memory_load (
    TXM_MODULE_INSTANCE *module_instance,
    CHAR *module_name,
    VOID *location);
```

### <a name="description"></a><span data-ttu-id="ffae3-265">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-265">Description</span></span>

<span data-ttu-id="ffae3-266">Questo servizio carica il codice e l'area dati del modulo nell'area di memoria del modulo configurata da ***txm_module_manager_initialize*** e la prepara per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ffae3-266">This service loads the module's code and data area into the module memory area set up by ***txm_module_manager_initialize*** and prepares it for execution.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-267">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-267">Input parameters</span></span>

- <span data-ttu-id="ffae3-268">**module_instance** Puntatore all'istanza del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-268">**module_instance** Pointer to the instance of the module.</span></span>
- <span data-ttu-id="ffae3-269">**module_name** Nome del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-269">**module_name** Name of the module.</span></span>
- <span data-ttu-id="ffae3-270">**posizione** Puntatore all'area di codice del modulo, preambolo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-270">**location** Pointer to module's code area, preamble first.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-271">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-271">Return values</span></span>

- <span data-ttu-id="ffae3-272">Il caricamento del modulo **TX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="ffae3-272">**TX_SUCCESS** (0x00) Successful module load.</span></span>
- <span data-ttu-id="ffae3-273">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-273">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="ffae3-274">Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.</span><span class="sxs-lookup"><span data-stu-id="ffae3-274">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="ffae3-275">**TX_NO_MEMORY** (0x10) memoria insufficiente per caricare il modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-275">**TX_NO_MEMORY** (0x10) Not enough memory to load module.</span></span>
- <span data-ttu-id="ffae3-276">**TX_PTR_ERROR** (0x03) puntatore non valido, istanza del modulo o preambolo del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-276">**TX_PTR_ERROR** (0x03) Invalid pointer, module instance, or module preamble.</span></span>
- <span data-ttu-id="ffae3-277">Allineamento di **TXM_MODULE_ALIGNMENT_ERROR** (0xF0) non valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-277">**TXM_MODULE_ALIGNMENT_ERROR** (0xF0) Invalid alignment.</span></span>
- <span data-ttu-id="ffae3-278">Il modulo **TXM_MODULE_ALREADY_LOADED** (0xF1) è già caricato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-278">**TXM_MODULE_ALREADY_LOADED** (0xF1) Module already loaded.</span></span>
- <span data-ttu-id="ffae3-279">Preambolo del modulo **TXM_MODULE_INVALID** (0XF2) non valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-279">**TXM_MODULE_INVALID** (0xF2) Invalid module preamble.</span></span>
- <span data-ttu-id="ffae3-280">Proprietà incompatibili **TXM_MODULE_INVALID_PROPERTIES** (0xf3).</span><span class="sxs-lookup"><span data-stu-id="ffae3-280">**TXM_MODULE_INVALID_PROPERTIES** (0xF3) Incompatible properties.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-281">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-281">Allowed from</span></span>

<span data-ttu-id="ffae3-282">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-282">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-283">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-283">Example</span></span>

```c
TXM_MODULE_INSTANCE     my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
 txm_module_manager_memory_load(&my_module, "my module", (VOID *) 0x080F0000);
```

### <a name="see-also"></a><span data-ttu-id="ffae3-284">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ffae3-284">See also</span></span>

- <span data-ttu-id="ffae3-285">txm_module_manager_file_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-285">txm_module_manager_file_load</span></span>
- <span data-ttu-id="ffae3-286">txm_module_manager_in_place_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-286">txm_module_manager_in_place_load</span></span>
- <span data-ttu-id="ffae3-287">txm_module_manager_unload</span><span class="sxs-lookup"><span data-stu-id="ffae3-287">txm_module_manager_unload</span></span>

---

## <a name="txm_module_manager_object_pool_create"></a><span data-ttu-id="ffae3-288">txm_module_manager_object_pool_create</span><span class="sxs-lookup"><span data-stu-id="ffae3-288">txm_module_manager_object_pool_create</span></span>

<span data-ttu-id="ffae3-289">Creare un pool di oggetti per i moduli.</span><span class="sxs-lookup"><span data-stu-id="ffae3-289">Create an object pool for modules.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-290">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-290">Prototype</span></span>

```c
UINT txm_module_manager_object_pool_create(
    VOID *pool_memory_start,
    ULONG pool_memory_size);
```

### <a name="description"></a><span data-ttu-id="ffae3-291">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-291">Description</span></span>

<span data-ttu-id="ffae3-292">Questo servizio crea un pool di memoria oggetto di gestione moduli da cui i moduli possono allocare oggetti ThreadX/NetX, mantenendo l'oggetto di sistema fuori dall'area di memoria del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-292">This service creates a Module Manager object memory pool that the modules can allocate ThreadX/NetX objects from, thereby keeping the system object out of the module's memory area.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-293">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-293">Input parameters</span></span>

- <span data-ttu-id="ffae3-294">**pool_memory_start** Puntatore all'inizio della memoria dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="ffae3-294">**pool_memory_start** Pointer to the start of object memory.</span></span>
- <span data-ttu-id="ffae3-295">**pool_memory_size** Dimensioni in byte del pool di memoria dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="ffae3-295">**pool_memory_size** Size in bytes of the object memory pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-296">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-296">Return values</span></span>

- <span data-ttu-id="ffae3-297">**TX_SUCCESS** (0x00) inizializzazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="ffae3-297">**TX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="ffae3-298">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-298">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-299">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-299">Allowed from</span></span>

<span data-ttu-id="ffae3-300">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-300">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-301">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-301">Example</span></span>

```c
TXM_MODULE_INSTANCE my_module;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Create an object memory pool in the next 64KB of memory. */
txm_module_manager_object_pool_create((VOID *) 0x64020000, 0x10000);
```

### <a name="see-also"></a><span data-ttu-id="ffae3-302">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ffae3-302">See also</span></span>

- <span data-ttu-id="ffae3-303">txm_module_manager_initialize</span><span class="sxs-lookup"><span data-stu-id="ffae3-303">txm_module_manager_initialize</span></span>

---

## <a name="txm_module_manager_properties_get"></a><span data-ttu-id="ffae3-304">txm_module_manager_properties_get</span><span class="sxs-lookup"><span data-stu-id="ffae3-304">txm_module_manager_properties_get</span></span>

<span data-ttu-id="ffae3-305">Ottenere le proprietà del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-305">Get module properties.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-306">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-306">Prototype</span></span>

```c
UINT txm_module_manager_properties_get(
    TXM_MODULE_INSTANCE *module_instance,
    ULONG *module_properties_ptr);
```

### <a name="description"></a><span data-ttu-id="ffae3-307">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-307">Description</span></span>

<span data-ttu-id="ffae3-308">Questo servizio restituisce le proprietà (specificate nel preambolo) di un modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-308">This service returns the properties (specified in the preamble) of a module.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-309">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-309">Input parameters</span></span>

- <span data-ttu-id="ffae3-310">**module_instance** Puntatore all'istanza del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-310">**module_instance** Pointer to the module instance.</span></span>
- <span data-ttu-id="ffae3-311">**module_properties_ptr** Puntatore alla destinazione per le proprietà del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-311">**module_properties_ptr** Pointer to destination for module's properties.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-312">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-312">Return values</span></span>

- <span data-ttu-id="ffae3-313">**TX_SUCCESS** (0x00) inizializzazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="ffae3-313">**TX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="ffae3-314">**TX_PTR_ERROR** (0x03) puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-314">**TX_PTR_ERROR** (0x03) Invalid pointer.</span></span>
- <span data-ttu-id="ffae3-315">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-315">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-316">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-316">Allowed from</span></span>

<span data-ttu-id="ffae3-317">Thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-317">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-318">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-318">Example</span></span>

```c
TXM_MODULE_INSTANCE     my_module;
ULONG                   module_properties;

/* Initialize the module manager with 64KB of RAM starting at address 0x64010000. */
txm_module_manager_initialize((VOID *) 0x64010000, 0x10000);

/* Create an object memory pool in the next 64KB of memory. */
txm_module_manager_object_pool_create((VOID *) 0x64020000, 0x10000);

/* Load the module that has its code area at address 0x080F0000. */
txm_module_manager_in_place_load(&my_module, "my module", (VOID *) 0x080F0000);

/* Get module properties. */
txm_module_manager_properties_get(&my_module, &module_properties);
```

---

## <a name="txm_module_manager_start"></a><span data-ttu-id="ffae3-319">txm_module_manager_start</span><span class="sxs-lookup"><span data-stu-id="ffae3-319">txm_module_manager_start</span></span>

<span data-ttu-id="ffae3-320">Avviare l'esecuzione del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-320">Start execution of the module.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-321">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-321">Prototype</span></span>

```c
UINT txm_module_manager_start(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a><span data-ttu-id="ffae3-322">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-322">Description</span></span>

<span data-ttu-id="ffae3-323">Questo servizio avvia l'esecuzione del modulo già caricato specificato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-323">This service starts execution of the specified, already loaded module.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-324">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-324">Input parameters</span></span>

- <span data-ttu-id="ffae3-325">**module_instance** Puntatore a un'istanza del modulo caricata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ffae3-325">**module_instance** Pointer to previously loaded module instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-326">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-326">Return values</span></span>

- <span data-ttu-id="ffae3-327">Inizio del modulo **TX_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="ffae3-327">**TX_SUCCESS** (0x00) Successful module start.</span></span>
- <span data-ttu-id="ffae3-328">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-328">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="ffae3-329">Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.</span><span class="sxs-lookup"><span data-stu-id="ffae3-329">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="ffae3-330">Il puntatore o l'istanza del modulo **TX_PTR_ERROR** (0X03) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-330">**TX_PTR_ERROR** (0x03) Invalid pointer or module instance.</span></span>
- <span data-ttu-id="ffae3-331">Il modulo **TX_START_ERROR** (0x10) è già stato avviato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-331">**TX_START_ERROR** (0x10) Module already started.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-332">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-332">Allowed from</span></span>

<span data-ttu-id="ffae3-333">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-333">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-334">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-334">Example</span></span>

```c
/* Start the module. */
txm_module_manager_start(&my_module);

/* Let the module run for a while. */
tx_thread_sleep(2000);

/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a><span data-ttu-id="ffae3-335">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ffae3-335">See also</span></span>

- <span data-ttu-id="ffae3-336">txm_module_manager_stop</span><span class="sxs-lookup"><span data-stu-id="ffae3-336">txm_module_manager_stop</span></span>

---

## <a name="txm_module_manager_stop"></a><span data-ttu-id="ffae3-337">txm_module_manager_stop</span><span class="sxs-lookup"><span data-stu-id="ffae3-337">txm_module_manager_stop</span></span>

<span data-ttu-id="ffae3-338">Arrestare l'esecuzione del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-338">Stop execution of the module.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-339">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-339">Prototype</span></span>

```c
UINT txm_module_manager_stop(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a><span data-ttu-id="ffae3-340">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-340">Description</span></span>

<span data-ttu-id="ffae3-341">Questo servizio arresta un modulo caricato in precedenza e avviato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-341">This service stops a module that was previously loaded and started.</span></span> <span data-ttu-id="ffae3-342">L'arresto di un modulo include l'esecuzione del thread di arresto facoltativo del modulo, la terminazione di tutti i thread e l'eliminazione di tutte le risorse associate al modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-342">Stopping a module includes executing the module's optional stop thread, terminating all threads, and deleting all resources associated with the module.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-343">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-343">Input parameters</span></span>

- <span data-ttu-id="ffae3-344">**module_instance** Puntatore all'istanza del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-344">**module_instance** Pointer to module instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-345">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-345">Return values</span></span>

- <span data-ttu-id="ffae3-346">Interruzione del modulo riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="ffae3-346">**TX_SUCCESS** (0x00) Successful module stop.</span></span>
- <span data-ttu-id="ffae3-347">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-347">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="ffae3-348">Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.</span><span class="sxs-lookup"><span data-stu-id="ffae3-348">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="ffae3-349">Il puntatore o l'istanza del modulo **TX_PTR_ERROR** (0X03) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-349">**TX_PTR_ERROR** (0x03) Invalid pointer or module instance.</span></span>
- <span data-ttu-id="ffae3-350">Il modulo **TX_START_ERROR** (0x10) non è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-350">**TX_START_ERROR** (0x10) Module not started.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-351">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-351">Allowed from</span></span>

<span data-ttu-id="ffae3-352">Thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-352">Threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-353">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-353">Example</span></span>

```c
/* Start the module. */
txm_module_manager_start(&my_module);

/* Let the module run for a while. */
tx_thread_sleep(20000);

/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a><span data-ttu-id="ffae3-354">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ffae3-354">See also</span></span>

- <span data-ttu-id="ffae3-355">txm_module_manager_start</span><span class="sxs-lookup"><span data-stu-id="ffae3-355">txm_module_manager_start</span></span>

---

## <a name="txm_module_manager_unload"></a><span data-ttu-id="ffae3-356">txm_module_manager_unload</span><span class="sxs-lookup"><span data-stu-id="ffae3-356">txm_module_manager_unload</span></span>

<span data-ttu-id="ffae3-357">Scaricare il modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-357">Unload the module.</span></span>

### <a name="prototype"></a><span data-ttu-id="ffae3-358">Prototipo</span><span class="sxs-lookup"><span data-stu-id="ffae3-358">Prototype</span></span>

```c
UINT txm_module_manager_unload(TXM_MODULE_INSTANCE *module_instance);
```

### <a name="description"></a><span data-ttu-id="ffae3-359">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffae3-359">Description</span></span>

<span data-ttu-id="ffae3-360">Questo servizio Scarica il modulo caricato e arrestato in precedenza, liberando tutte le risorse di memoria del modulo associate.</span><span class="sxs-lookup"><span data-stu-id="ffae3-360">This service unloads the previously loaded and stopped module, freeing all the associated module memory resources.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ffae3-361">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="ffae3-361">Input parameters</span></span>

- <span data-ttu-id="ffae3-362">**module_instance** Puntatore all'istanza del modulo.</span><span class="sxs-lookup"><span data-stu-id="ffae3-362">**module_instance** Pointer to the instance of the module.</span></span>

### <a name="return-values"></a><span data-ttu-id="ffae3-363">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="ffae3-363">Return values</span></span>

- <span data-ttu-id="ffae3-364">**TX_SUCCESS** 0x00) lo scaricamento del modulo è riuscito.</span><span class="sxs-lookup"><span data-stu-id="ffae3-364">**TX_SUCCESS** 0x00) Successful module unload.</span></span>
- <span data-ttu-id="ffae3-365">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-365">**TX_CALLER_ERROR** (0x13) Invalid caller.</span></span>
- <span data-ttu-id="ffae3-366">Gestione **TX_NOT_AVAILABLE** (0x1d) non inizializzata.</span><span class="sxs-lookup"><span data-stu-id="ffae3-366">**TX_NOT_AVAILABLE** (0x1D) Manager not initialized.</span></span>
- <span data-ttu-id="ffae3-367">Il modulo o il modulo **TX_NOT_DONE** (0x20) non è stato arrestato.</span><span class="sxs-lookup"><span data-stu-id="ffae3-367">**TX_NOT_DONE** (0x20) Invalid module or module not stopped.</span></span>
- <span data-ttu-id="ffae3-368">Il puntatore o l'istanza del modulo **TX_PTR_ERROR** (0X03) non è valido.</span><span class="sxs-lookup"><span data-stu-id="ffae3-368">**TX_PTR_ERROR** (0x03) Invalid pointer or module instance.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="ffae3-369">Consentito da</span><span class="sxs-lookup"><span data-stu-id="ffae3-369">Allowed from</span></span>

<span data-ttu-id="ffae3-370">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="ffae3-370">Initialization and threads</span></span>

### <a name="example"></a><span data-ttu-id="ffae3-371">Esempio</span><span class="sxs-lookup"><span data-stu-id="ffae3-371">Example</span></span>

```c
/* Stop the module. */
txm_module_manager_stop(&my_module);

/* Unload the module. */
status = txm_module_manager_unload(&my_module);
```

### <a name="see-also"></a><span data-ttu-id="ffae3-372">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ffae3-372">See also</span></span>

- <span data-ttu-id="ffae3-373">txm_module_manager_file_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-373">txm_module_manager_file_load</span></span>
- <span data-ttu-id="ffae3-374">txm_module_manager_in_place_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-374">txm_module_manager_in_place_load</span></span>
- <span data-ttu-id="ffae3-375">txm_module_manager_memory_load</span><span class="sxs-lookup"><span data-stu-id="ffae3-375">txm_module_manager_memory_load</span></span>
- <span data-ttu-id="ffae3-376">txm_module_manager_stop</span><span class="sxs-lookup"><span data-stu-id="ffae3-376">txm_module_manager_stop</span></span>
