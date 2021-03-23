---
title: Capitolo 4-Descrizione dei servizi ThreadX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi ThreadX di Azure RTO in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 60ecc96df07b1f77b9b448814c4420133f3e2afc
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821362"
---
# <a name="chapter-4---description-of-azure-rtos-threadx-services"></a><span data-ttu-id="94e54-103">Capitolo 4-Descrizione dei servizi ThreadX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="94e54-103">Chapter 4 - Description of Azure RTOS ThreadX Services</span></span>

<span data-ttu-id="94e54-104">Questo capitolo contiene una descrizione di tutti i servizi ThreadX di Azure RTO in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="94e54-104">This chapter contains a description of all Azure RTOS ThreadX services in alphabetic order.</span></span> <span data-ttu-id="94e54-105">I nomi sono progettati in modo da raggruppare tutti i servizi simili.</span><span class="sxs-lookup"><span data-stu-id="94e54-105">Their names are designed so all similar services are grouped together.</span></span> <span data-ttu-id="94e54-106">Nella sezione "valori restituiti" nelle descrizioni seguenti i valori in **grassetto** non sono interessati dal **TX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API; mentre i valori visualizzati in non grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="94e54-106">In the "Return Values" section in the following descriptions, values in **BOLD** are not affected by the **TX_DISABLE_ERROR_CHECKING** define used to disable API error checking; while values shown in nonbold are completely disabled.</span></span> <span data-ttu-id="94e54-107">Inoltre, una "**Sì**" elencata sotto l'intestazione "**precedenza possibile**" indica che la chiamata al servizio può riprendere un thread con priorità più alta, in modo da precedere il thread chiamante.</span><span class="sxs-lookup"><span data-stu-id="94e54-107">In addition, a "**Yes**" listed under the "**Preemption Possible**" heading indicates that calling the service may resume a higher-priority thread, thus preempting the calling thread.</span></span>

## <a name="tx_block_allocate"></a><span data-ttu-id="94e54-108">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-108">tx_block_allocate</span></span>

<span data-ttu-id="94e54-109">Allocare un blocco di memoria di dimensioni fisse</span><span class="sxs-lookup"><span data-stu-id="94e54-109">Allocate fixed-size block of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-110">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-110">Prototype</span></span>

```c
UINT tx_block_allocate(
    TX_BLOCK_POOL *pool_ptr, 
    VOID **block_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="94e54-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-111">Description</span></span>

<span data-ttu-id="94e54-112">Questo servizio alloca un blocco di memoria di dimensioni fisse dal pool di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-112">This service allocates a fixed-size memory block from the specified memory pool.</span></span> <span data-ttu-id="94e54-113">La dimensione effettiva del blocco di memoria viene determinata durante la creazione del pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-113">The actual size of the memory block is determined during memory pool creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-114">*È importante assicurarsi che il codice dell'applicazione non scriva al di fuori del blocco di memoria allocato. In tal caso, il danneggiamento si verifica in un blocco di memoria adiacente, in genere successivo. I risultati sono imprevedibili e spesso fatali.*</span><span class="sxs-lookup"><span data-stu-id="94e54-114">*It is important to ensure application code does not write outside the allocated memory block. If this happens, corruption occurs in an adjacent (usually subsequent) memory block. The results are unpredictable and often fatal!*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-115">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-115">Parameters</span></span>

- <span data-ttu-id="94e54-116">**pool_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-116">**pool_ptr**</span></span> <br><span data-ttu-id="94e54-117">Puntatore a un pool di blocchi di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-117">Pointer to a previously created memory block pool.</span></span>
- <span data-ttu-id="94e54-118">**block_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-118">**block_ptr**</span></span> <br><span data-ttu-id="94e54-119">Puntatore a un puntatore a un blocco di destinazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-119">Pointer to a destination block pointer.</span></span> <span data-ttu-id="94e54-120">Al completamento dell'allocazione, l'indirizzo del blocco di memoria allocato viene inserito nel punto in cui questo parametro punta.</span><span class="sxs-lookup"><span data-stu-id="94e54-120">On successful allocation, the address of the allocated memory block is placed where this parameter points.</span></span>
- <span data-ttu-id="94e54-121">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="94e54-121">**wait_option**</span></span> <br><span data-ttu-id="94e54-122">Definisce il comportamento del servizio se non sono disponibili blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-122">Defines how the service behaves if there are no memory blocks available.</span></span> <span data-ttu-id="94e54-123">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="94e54-123">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="94e54-124">**TX_NO_WAIT** (0x00000000): la selezione di **TX_NO_WAIT** comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="94e54-124">**TX_NO_WAIT** (0x00000000) - Selecting **TX_NO_WAIT** results in an immediate return from this service regardless if it was successful or not.</span></span> <span data-ttu-id="94e54-125">*Questa è l'unica opzione valida se il servizio viene chiamato da un non thread, ad esempio inizializzazione, timer o ISR*.</span><span class="sxs-lookup"><span data-stu-id="94e54-125">*This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR*.</span></span>
  - <span data-ttu-id="94e54-126">**TX_WAIT_FOREVER** (0xFFFFFFF): se si seleziona **TX_WAIT_FOREVER** , il thread chiamante sospenderà per un tempo illimitato fino a quando non sarà disponibile un blocco di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-126">**TX_WAIT_FOREVER** (0xFFFFFFF) - Selecting **TX_WAIT_FOREVER** causes the calling thread to suspend indefinitely until a memory block is available.</span></span>
  - <span data-ttu-id="94e54-127">*valore di timeout* (0x00000001 tramite 0xfffffffe)-la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa di un blocco di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-127">*timeout value* (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a memory block.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-128">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-128">Return Values</span></span>

- <span data-ttu-id="94e54-129">Allocazione di blocchi di memoria riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-129">**TX_SUCCESS**    (0x00)  Successful memory block allocation.</span></span>
- <span data-ttu-id="94e54-130">Il pool di blocchi di memoria **TX_DELETED** (0x01) è stato eliminato durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-130">**TX_DELETED**    (0x01)  Memory block pool was deleted while thread was suspended.</span></span>
- <span data-ttu-id="94e54-131">Il servizio **TX_NO_MEMORY** (0x10) non è stato in grado di allocare un blocco di memoria entro il tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-131">**TX_NO_MEMORY**  (0x10)  Service was unable to allocate a block of memory within the specified time to wait.</span></span>
- <span data-ttu-id="94e54-132">La sospensione **TX_WAIT_ABORTED** (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="94e54-132">**TX_WAIT_ABORTED**   (0x1A)  Suspension was aborted by another thread, timer or ISR.</span></span>
- <span data-ttu-id="94e54-133">**TX_POOL_ERROR** (0x02) puntatore al pool di blocchi di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-133">**TX_POOL_ERROR** (0x02)  Invalid memory block pool pointer.</span></span>
- <span data-ttu-id="94e54-134">**TX_WAIT_ERROR** (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-134">**TX_WAIT_ERROR** (0x04)  A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="94e54-135">**TX_PTR_ERROR**  (0x03) puntatore non valido al puntatore di destinazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-135">**TX_PTR_ERROR**  (0x03)  Invalid pointer to destination pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-136">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-136">Allowed From</span></span>

<span data-ttu-id="94e54-137">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-137">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-138">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-138">Preemption Possible</span></span>

<span data-ttu-id="94e54-139">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-139">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-140">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-140">Example</span></span>

```c
TX_BLOCK_POOL my_pool;
unsigned char *memory_ptr;

UINT status;

/* Allocate a memory block from my_pool. Assume that the pool has
already been created with a call to tx_block_pool_create. */

status = tx_block_allocate(&my_pool, (VOID **) &memory_ptr,
  TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the address of
the allocated block of memory. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-141">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-141">See Also</span></span>

- <span data-ttu-id="94e54-142">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-142">tx_block_pool_create</span></span>
- <span data-ttu-id="94e54-143">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-143">tx_block_pool_delete</span></span>
- <span data-ttu-id="94e54-144">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-144">tx_block_pool_info_get</span></span>
- <span data-ttu-id="94e54-145">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-145">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-146">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-146">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-147">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-147">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="94e54-148">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="94e54-148">tx_block_release</span></span>

## <a name="tx_block_pool_create"></a><span data-ttu-id="94e54-149">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-149">tx_block_pool_create</span></span>

<span data-ttu-id="94e54-150">Creare un pool di blocchi di memoria a dimensione fissa</span><span class="sxs-lookup"><span data-stu-id="94e54-150">Create pool of fixed-size memory blocks</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-151">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-151">Prototype</span></span>

```c
UINT tx_block_pool_create(
    TX_BLOCK_POOL pool_ptr,
    CHAR name_ptr, 
    ULONG block_size,
    VOID pool_start, 
    ULONG pool_size);
```

### <a name="description"></a><span data-ttu-id="94e54-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-152">Description</span></span>

<span data-ttu-id="94e54-153">Questo servizio crea un pool di blocchi di memoria di dimensioni fisse.</span><span class="sxs-lookup"><span data-stu-id="94e54-153">This service creates a pool of fixed-size memory blocks.</span></span> <span data-ttu-id="94e54-154">L'area di memoria specificata è divisa in tutti i blocchi di memoria di dimensioni fisse possibili utilizzando la formula:</span><span class="sxs-lookup"><span data-stu-id="94e54-154">The memory area specified is divided into as many fixed-size memory blocks as possible using the formula:</span></span>

<span data-ttu-id="94e54-155">**blocchi totali** = (**byte totali**)/(**dimensione blocco** + sizeof (void \*))</span><span class="sxs-lookup"><span data-stu-id="94e54-155">**total blocks** = (**total bytes**) / (**block size** + sizeof(void \*))</span></span>

> [!NOTE]
><span data-ttu-id="94e54-156">\* Ogni blocco di memoria contiene un puntatore di overhead invisibile all'utente e rappresentato da "sizeof (void *)" nella formula precedente.*</span><span class="sxs-lookup"><span data-stu-id="94e54-156">\*Each memory block contains one pointer of overhead that is invisible to the user and is represented by the "sizeof(void *)" in the preceding formula.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-157">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-157">Parameters</span></span>

- <span data-ttu-id="94e54-158">**pool_ptr**  Puntatore a un blocco di controllo del pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-158">**pool_ptr**  Pointer to a memory block pool control block.</span></span>
- <span data-ttu-id="94e54-159">**name_ptr**  Puntatore al nome del pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-159">**name_ptr**  Pointer to the name of the memory block pool.</span></span>
- <span data-ttu-id="94e54-160">**block_size**    Numero di byte in ogni blocco di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-160">**block_size**    Number of bytes in each memory block.</span></span>
- <span data-ttu-id="94e54-161">**pool_start**    Indirizzo iniziale del pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-161">**pool_start**    Starting address of the memory block pool.</span></span> <span data-ttu-id="94e54-162">L'indirizzo iniziale deve essere allineato alle dimensioni del tipo di dati ULONG.</span><span class="sxs-lookup"><span data-stu-id="94e54-162">The starting address must be aligned to the size of the ULONG data type.</span></span>
- <span data-ttu-id="94e54-163">**pool_size** Numero totale di byte disponibili per il pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-163">**pool_size** Total number of bytes available for the memory block pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-164">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-164">Return Values</span></span>

- <span data-ttu-id="94e54-165">Creazione del pool di blocchi di memoria riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-165">**TX_SUCCESS**    (0x00)  Successful memory block pool creation.</span></span>
- <span data-ttu-id="94e54-166">**TX_POOL_ERROR** (0x02) puntatore al pool di blocchi di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-166">**TX_POOL_ERROR** (0x02)  Invalid memory block pool pointer.</span></span> <span data-ttu-id="94e54-167">Il puntatore è NULL o il pool è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="94e54-167">Either the pointer is NULL or the pool is already created.</span></span>
- <span data-ttu-id="94e54-168">**TX_PTR_ERROR**  (0x03) indirizzo iniziale non valido del pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-168">**TX_PTR_ERROR**  (0x03)  Invalid starting address of the pool.</span></span>
- <span data-ttu-id="94e54-169">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-169">**TX_CALLER_ERROR**   (0x13)  Invalid caller of this service.</span></span>
- <span data-ttu-id="94e54-170">Le dimensioni **TX_SIZE_ERROR** (0x05) del pool non sono valide.</span><span class="sxs-lookup"><span data-stu-id="94e54-170">**TX_SIZE_ERROR** (0x05)  Size of pool is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-171">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-171">Allowed From</span></span>

<span data-ttu-id="94e54-172">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="94e54-172">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-173">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-173">Preemption Possible</span></span>

<span data-ttu-id="94e54-174">No</span><span class="sxs-lookup"><span data-stu-id="94e54-174">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-175">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-175">Example</span></span>

```c
TX_BLOCK_POOL my_pool;

UINT status;

/* Create a memory pool whose total size is 1000 bytes starting at
address 0x100000. Each block in this pool is defined to be 50 bytes
long. */
status = tx_block_pool_create(&my_pool, "my_pool_name",
  50, (VOID *) 0x100000, 1000);

/* If status equals TX_SUCCESS, my_pool contains 18 memory blocks
of 50 bytes each. The reason there are not 20 blocks in the pool is
because of the one overhead pointer associated with each block. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-176">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-176">See Also</span></span>

- <span data-ttu-id="94e54-177">tx_block_allocate, tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-177">tx_block_allocate, tx_block_pool_delete</span></span>
- <span data-ttu-id="94e54-178">tx_block_pool_info_get, tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-178">tx_block_pool_info_get, tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-179">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-179">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-180">tx_block_pool_prioritize, tx_block_release</span><span class="sxs-lookup"><span data-stu-id="94e54-180">tx_block_pool_prioritize, tx_block_release</span></span>

## <a name="tx_block_pool_delete"></a><span data-ttu-id="94e54-181">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-181">tx_block_pool_delete</span></span>

<span data-ttu-id="94e54-182">Elimina pool di blocchi di memoria</span><span class="sxs-lookup"><span data-stu-id="94e54-182">Delete memory block pool</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-183">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-183">Prototype</span></span>

```c
UINT tx_block_pool_delete(TX_BLOCK_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-184">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-184">Description</span></span>

<span data-ttu-id="94e54-185">Questo servizio Elimina il pool di memoria di blocco specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-185">This service deletes the specified block-memory pool.</span></span> <span data-ttu-id="94e54-186">Tutti i thread sospesi in attesa di un blocco di memoria da questo pool vengono ripresi e viene fornito un **TX_DELETED** stato restituito.</span><span class="sxs-lookup"><span data-stu-id="94e54-186">All threads suspended waiting for a memory block from this pool are resumed and given a **TX_DELETED** return status.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-187">*È responsabilità dell'applicazione gestire l'area di memoria associata al pool, disponibile al termine del servizio. Inoltre, l'applicazione deve impedire l'uso di un pool eliminato o dei blocchi di memoria precedenti.*</span><span class="sxs-lookup"><span data-stu-id="94e54-187">*It is the application's responsibility to manage the memory area associated with the pool, which is available after this service completes. In addition, the application must prevent use of a deleted pool or its former memory blocks.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-188">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-188">Parameters</span></span>

- <span data-ttu-id="94e54-189">**pool_ptr** Puntatore a un pool di blocchi di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-189">**pool_ptr** Pointer to a previously created memory block pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-190">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-190">Return Values</span></span>

- <span data-ttu-id="94e54-191">Eliminazione del pool di blocchi di memoria riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-191">**TX_SUCCESS** (0x00) Successful memory block pool deletion.</span></span>
- <span data-ttu-id="94e54-192">**TX_POOL_ERROR** (0x02) puntatore al pool di blocchi di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-192">**TX_POOL_ERROR** (0x02) Invalid memory block pool pointer.</span></span>
- <span data-ttu-id="94e54-193">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-193">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-194">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-194">Allowed From</span></span>

<span data-ttu-id="94e54-195">Thread</span><span class="sxs-lookup"><span data-stu-id="94e54-195">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-196">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-196">Preemption Possible</span></span>

<span data-ttu-id="94e54-197">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-197">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-198">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-198">Example</span></span>

```c
TX_BLOCK_POOL my_pool;

UINT           status;

/* Delete entire memory block
pool. Assume that the pool has already been created with a call to
tx_block_pool_create. */
status = tx_block_pool_delete(&my_pool);

/* If status equals TX_SUCCESS, the memory block pool is deleted.*/
```

### <a name="see-also"></a><span data-ttu-id="94e54-199">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-199">See Also</span></span>

- <span data-ttu-id="94e54-200">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-200">tx_block_allocate</span></span>
- <span data-ttu-id="94e54-201">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-201">tx_block_pool_create</span></span>
- <span data-ttu-id="94e54-202">tx_block_pool_info_get, tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-202">tx_block_pool_info_get, tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-203">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-203">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-204">tx_block_pool_prioritize, tx_block_release</span><span class="sxs-lookup"><span data-stu-id="94e54-204">tx_block_pool_prioritize, tx_block_release</span></span>

## <a name="tx_block_pool_info_get"></a><span data-ttu-id="94e54-205">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-205">tx_block_pool_info_get</span></span>

<span data-ttu-id="94e54-206">Recuperare informazioni sul pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="94e54-206">Retrieve information about block pool</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-207">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-207">Prototype</span></span>

```c
UINT tx_block_pool_info_get(
    TX_BLOCK_POOL *pool_ptr, 
    CHAR **name,
    ULONG *available, 
    ULONG *total_blocks,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_BLOCK_POOL **next_pool);
```

### <a name="description"></a><span data-ttu-id="94e54-208">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-208">Description</span></span>

<span data-ttu-id="94e54-209">Questo servizio recupera le informazioni sul pool di memoria del blocco specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-209">This service retrieves information about the specified block memory pool.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-210">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-210">Parameters</span></span>

- <span data-ttu-id="94e54-211">**pool_ptr**  Puntatore al pool di blocchi di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-211">**pool_ptr**  Pointer to previously created memory block pool.</span></span>
- <span data-ttu-id="94e54-212">**nome**  Puntatore alla destinazione per il puntatore al nome del pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="94e54-212">**name**  Pointer to destination for the pointer to the block pool's name.</span></span>
- <span data-ttu-id="94e54-213">**disponibile** Puntatore alla destinazione per il numero di blocchi disponibili nel pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="94e54-213">**available** Pointer to destination for the number of available blocks in the block pool.</span></span>
- <span data-ttu-id="94e54-214">**total_blocks**  Puntatore alla destinazione per il numero totale di blocchi nel pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="94e54-214">**total_blocks**  Pointer to destination for the total number of blocks in the block pool.</span></span>
- <span data-ttu-id="94e54-215">**first_suspended**   Puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione del pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="94e54-215">**first_suspended**   Pointer to destination for the pointer to the thread that is first on the suspension list of this block pool.</span></span>
- <span data-ttu-id="94e54-216">**suspended_count**   Puntatore alla destinazione per il numero di thread attualmente sospesi in questo pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="94e54-216">**suspended_count**   Pointer to destination for the number of threads currently suspended on this block pool.</span></span>
- <span data-ttu-id="94e54-217">**next_pool** Puntatore alla destinazione per l'indicatore di misura del pool di blocchi creato successivamente.</span><span class="sxs-lookup"><span data-stu-id="94e54-217">**next_pool** Pointer to destination for the pointer of the next created block pool.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-218">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-218">*Supplying a TX_NULL for any parameter indicates the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-219">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-219">Return Values</span></span>

- <span data-ttu-id="94e54-220">Recupero delle informazioni riuscite del pool di blocchi **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-220">**TX_SUCCESS** (0x00) Successful block pool information retrieve.</span></span>
- <span data-ttu-id="94e54-221">**TX_POOL_ERROR** (0x02) puntatore al pool di blocchi di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-221">**TX_POOL_ERROR** (0x02) Invalid memory block pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-222">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-222">Allowed From</span></span>

<span data-ttu-id="94e54-223">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-223">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-224">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-224">Example</span></span>

```c
TX_BLOCK_POOL my_pool;
CHAR *name;
ULONG available;
ULONG total_blocks;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_BLOCK_POOL *next_pool;
UINT status;

/* Retrieve information about the previously created
block pool "my_pool." */
status = tx_block_pool_info_get(&my_pool, &name,
  &available,&total_blocks,
  &first_suspended, &suspended_count,
  &next_pool);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-225">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-225">See Also</span></span>

- <span data-ttu-id="94e54-226">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-226">tx_block_allocate</span></span>
- <span data-ttu-id="94e54-227">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-227">tx_block_pool_create</span></span>
- <span data-ttu-id="94e54-228">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-228">tx_block_pool_delete</span></span>
- <span data-ttu-id="94e54-229">tx_block_pool_info_get, tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-229">tx_block_pool_info_get, tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-230">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-230">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-231">tx_block_pool_prioritize, tx_block_release</span><span class="sxs-lookup"><span data-stu-id="94e54-231">tx_block_pool_prioritize, tx_block_release</span></span>

## <a name="tx_block_pool_performance_info_get"></a><span data-ttu-id="94e54-232">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-232">tx_block_pool_performance_info_get</span></span>

<span data-ttu-id="94e54-233">Ottenere informazioni sulle prestazioni del pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="94e54-233">Get block pool performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-234">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-234">Prototype</span></span>

```c
UINT tx_block_pool_performance_info_get(
    TX_BLOCK_POOL *pool_ptr,
    ULONG *allocates, 
    ULONG *releases,
    ULONG *suspensions, 
    ULONG *timeouts));
```

### <a name="description"></a><span data-ttu-id="94e54-235">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-235">Description</span></span>

<span data-ttu-id="94e54-236">Questo servizio recupera le informazioni sulle prestazioni relative al pool di blocchi di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-236">This service retrieves performance information about the specified memory block pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-237">Per restituire informazioni sulle prestazioni, *è necessario compilare la libreria threadX e l'applicazione con* **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** *definite per questo servizio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-237">*The ThreadX library and application must be built with* **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-238">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-238">Parameters</span></span>

- <span data-ttu-id="94e54-239">**pool_ptr**  Puntatore al pool di blocchi di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-239">**pool_ptr**  Pointer to previously created memory block pool.</span></span>
- <span data-ttu-id="94e54-240">**allocazioni** Puntatore alla destinazione per il numero di richieste di allocazione eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-240">**allocates** Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="94e54-241">**versioni**  di  Puntatore alla destinazione per il numero di richieste di rilascio eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-241">**releases**  Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="94e54-242">**sospensioni**   Puntatore alla destinazione per il numero di sospensioni di allocazione di thread nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-242">**suspensions**   Pointer to destination for the number of thread allocation suspensions on this pool.</span></span>
- <span data-ttu-id="94e54-243">**timeout**  Puntatore alla destinazione per il numero di timeout di allocazione della sospensione nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-243">**timeouts**  Pointer to destination for the number of allocate suspension timeouts on this pool.</span></span>

>[!NOTE]
> <span data-ttu-id="94e54-244">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-244">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-245">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-245">Return Values</span></span>

- <span data-ttu-id="94e54-246">**TX_SUCCESS**    (0x00) ottenere prestazioni del pool di blocchi riuscite.</span><span class="sxs-lookup"><span data-stu-id="94e54-246">**TX_SUCCESS**    (0x00)  Successful block pool performance get.</span></span>
- <span data-ttu-id="94e54-247">**TX_PTR_ERROR**  (0x03) puntatore al pool di blocchi non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-247">**TX_PTR_ERROR**  (0x03)  Invalid block pool pointer.</span></span>
- <span data-ttu-id="94e54-248">**TX_FEATURE_NOT_ENABLED**    (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-248">**TX_FEATURE_NOT_ENABLED**    (0xFF)  The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-249">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-249">Allowed From</span></span>

<span data-ttu-id="94e54-250">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-250">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-251">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-251">Example</span></span>

```c
TX_BLOCK_POOL my_pool;
ULONG allocates;
ULONG releases;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created block
pool. */
status = tx_block_pool_performance_info_get(&my_pool, &allocates,
  &releases,
  &suspensions,
  &timeouts);

/* If status is TX_SUCCESS the performance information was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-252">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-252">See Also</span></span>

- <span data-ttu-id="94e54-253">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-253">tx_block_allocate</span></span>
- <span data-ttu-id="94e54-254">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-254">tx_block_pool_create</span></span>
- <span data-ttu-id="94e54-255">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-255">tx_block_pool_delete</span></span>
- <span data-ttu-id="94e54-256">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-256">tx_block_pool_info_get</span></span>
- <span data-ttu-id="94e54-257">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-257">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-258">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-258">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-259">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="94e54-259">tx_block_release</span></span>

## <a name="tx_block_pool_performance_system_info_get"></a><span data-ttu-id="94e54-260">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-260">tx_block_pool_performance_system_info_get</span></span>

<span data-ttu-id="94e54-261">Ottenere informazioni sulle prestazioni del sistema del pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="94e54-261">Get block pool system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-262">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-262">Prototype</span></span>

```c
UINT tx_block_pool_performance_system_info_get(
    ULONG *allocates,
    ULONG *releases, 
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="94e54-263">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-263">Description</span></span>

<span data-ttu-id="94e54-264">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i pool di blocchi di memoria nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-264">This service retrieves performance information about all memory block pools in the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-265">Per restituire informazioni sulle prestazioni, *è necessario compilare la libreria threadX e l'applicazione con* **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** *definite per questo servizio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-265">*The ThreadX library and application must be built with* **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-266">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-266">Parameters</span></span>

- <span data-ttu-id="94e54-267">**allocazioni** Puntatore alla destinazione per il numero totale di richieste di allocazione eseguite su tutti i pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="94e54-267">**allocates** Pointer to destination for the total number of allocate requests performed on all block pools.</span></span>
- <span data-ttu-id="94e54-268">**versioni**  di  Puntatore alla destinazione per il numero totale di richieste di rilascio eseguite su tutti i pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="94e54-268">**releases**  Pointer to destination for the total number of release requests performed on all block pools.</span></span>
- <span data-ttu-id="94e54-269">**sospensioni**   Puntatore alla destinazione per il numero totale di sospensioni di allocazione di thread in tutti i pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="94e54-269">**suspensions**   Pointer to destination for the total number of thread allocation suspensions on all block pools.</span></span>
- <span data-ttu-id="94e54-270">**timeout**  Puntatore alla destinazione per il numero totale di timeout di allocazione della sospensione in tutti i pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="94e54-270">**timeouts**  Pointer to destination for the total number of allocate suspension timeouts on all block pools.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-271">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-271">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-272">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-272">Return Values</span></span>

- <span data-ttu-id="94e54-273">**TX_SUCCESS** (0x00) prestazioni del sistema del pool di blocchi riusciti Get.</span><span class="sxs-lookup"><span data-stu-id="94e54-273">**TX_SUCCESS** (0x00) Successful block pool system performance get.</span></span>
- <span data-ttu-id="94e54-274">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-274">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-275">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-275">Allowed From</span></span>

<span data-ttu-id="94e54-276">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-276">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-277">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-277">Example</span></span>

```c
ULONG       allocates;
ULONG       releases;
ULONG       suspensions;
ULONG       timeouts;

/* Retrieve performance information on all the block pools in
the system. */
status = tx_block_pool_performance_system_info_get(&allocates,
    &releases,&suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-278">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-278">See Also</span></span>

- <span data-ttu-id="94e54-279">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-279">tx_block_allocate</span></span>
- <span data-ttu-id="94e54-280">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-280">tx_block_pool_create</span></span>
- <span data-ttu-id="94e54-281">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-281">tx_block_pool_delete</span></span>
- <span data-ttu-id="94e54-282">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-282">tx_block_pool_info_get</span></span>
- <span data-ttu-id="94e54-283">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-283">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-284">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-284">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="94e54-285">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="94e54-285">tx_block_release</span></span>

## <a name="tx_block_pool_prioritize"></a><span data-ttu-id="94e54-286">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-286">tx_block_pool_prioritize</span></span>

<span data-ttu-id="94e54-287">Priorità elenco sospensione pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="94e54-287">Prioritize block pool suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-288">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-288">Prototype</span></span>

```c
UINT tx_block_pool_prioritize(TX_BLOCK_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-289">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-289">Description</span></span>

<span data-ttu-id="94e54-290">Questo servizio posiziona il thread con priorità più elevata sospeso per un blocco di memoria in questo pool all'inizio dell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="94e54-290">This service places the highest priority thread suspended for a block of memory on this pool at the front of the suspension list.</span></span> <span data-ttu-id="94e54-291">Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.</span><span class="sxs-lookup"><span data-stu-id="94e54-291">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-292">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-292">Parameters</span></span>

- <span data-ttu-id="94e54-293">**pool_ptr** Puntatore a un blocco di controllo del pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-293">**pool_ptr** Pointer to a memory block pool control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-294">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-294">Return Values</span></span>

- <span data-ttu-id="94e54-295">**TX_SUCCESS** (0x00) priorità del pool di blocchi riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-295">**TX_SUCCESS** (0x00) Successful block pool prioritize.</span></span>
- <span data-ttu-id="94e54-296">**TX_POOL_ERROR** (0x02) puntatore al pool di blocchi di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-296">**TX_POOL_ERROR** (0x02) Invalid memory block pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-297">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-297">Allowed From</span></span>

<span data-ttu-id="94e54-298">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-298">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-299">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-299">Preemption Possible</span></span>

<span data-ttu-id="94e54-300">No</span><span class="sxs-lookup"><span data-stu-id="94e54-300">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-301">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-301">Example</span></span>
```c
TX_BLOCK_POOL my_pool;
UINT status;

/* Ensure that the highest priority thread will receive
the next free block in this pool. */
status = tx_block_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_block_release call will wake up this thread. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-302">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-302">See Also</span></span>

- <span data-ttu-id="94e54-303">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-303">tx_block_allocate</span></span>
- <span data-ttu-id="94e54-304">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-304">tx_block_pool_create</span></span>
- <span data-ttu-id="94e54-305">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-305">tx_block_pool_delete</span></span>
- <span data-ttu-id="94e54-306">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-306">tx_block_pool_info_get</span></span>
- <span data-ttu-id="94e54-307">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-307">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-308">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-308">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-309">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="94e54-309">tx_block_release</span></span>

## <a name="tx_block_release"></a><span data-ttu-id="94e54-310">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="94e54-310">tx_block_release</span></span>

<span data-ttu-id="94e54-311">Rilasciare un blocco di memoria di dimensioni fisse</span><span class="sxs-lookup"><span data-stu-id="94e54-311">Release fixed-size block of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-312">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-312">Prototype</span></span>

```c
UINT tx_block_release(VOID *block_ptr);
``````

### <a name="description"></a><span data-ttu-id="94e54-313">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-313">Description</span></span>

<span data-ttu-id="94e54-314">Questo servizio rilascia un blocco precedentemente allocato al pool di memoria associato.</span><span class="sxs-lookup"><span data-stu-id="94e54-314">This service releases a previously allocated block back to its associated memory pool.</span></span> <span data-ttu-id="94e54-315">Se uno o più thread sono sospesi in attesa di blocchi di memoria da questo pool, il primo thread sospeso riceve questo blocco di memoria e riprende.</span><span class="sxs-lookup"><span data-stu-id="94e54-315">If there are one or more threads suspended waiting for memory blocks from this pool, the first thread suspended is given this memory block and resumed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="94e54-316">*L'applicazione deve impedire l'uso di un'area del blocco di memoria dopo che è stata rilasciata nel pool.*</span><span class="sxs-lookup"><span data-stu-id="94e54-316">*The application must prevent using a memory block area after it has been released back to the pool.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-317">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-317">Parameters</span></span>

- <span data-ttu-id="94e54-318">**block_ptr** Puntatore al blocco di memoria allocato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-318">**block_ptr** Pointer to the previously allocated memory block.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-319">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-319">Return Values</span></span>

- <span data-ttu-id="94e54-320">**TX_SUCCESS** (0x00) versione di blocco di memoria riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-320">**TX_SUCCESS** (0x00) Successful memory block release.</span></span>
- <span data-ttu-id="94e54-321">**TX_PTR_ERROR** (0x03) puntatore al blocco di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-321">**TX_PTR_ERROR** (0x03) Invalid pointer to memory block.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-322">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-322">Allowed From</span></span>

<span data-ttu-id="94e54-323">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-323">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-324">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-324">Preemption Possible</span></span>

<span data-ttu-id="94e54-325">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-325">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-326">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-326">Example</span></span>

```c
TX_BLOCK_POOL my_pool;
unsigned char *memory_ptr;
UINT status;

/* Release a memory block back to my_pool. Assume that the
pool has been created and the memory block has been
allocated. */
status = tx_block_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the block of memory pointed
to by memory_ptr has been returned to the pool. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-327">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-327">See Also</span></span>

- <span data-ttu-id="94e54-328">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-328">tx_block_allocate</span></span>
- <span data-ttu-id="94e54-329">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-329">tx_block_pool_create</span></span>
- <span data-ttu-id="94e54-330">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-330">tx_block_pool_delete</span></span>
- <span data-ttu-id="94e54-331">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-331">tx_block_pool_info_get</span></span>
- <span data-ttu-id="94e54-332">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-332">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-333">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-333">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-334">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-334">tx_block_pool_prioritize</span></span>

## <a name="tx_byte_allocate"></a><span data-ttu-id="94e54-335">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-335">tx_byte_allocate</span></span>

<span data-ttu-id="94e54-336">Alloca byte di memoria</span><span class="sxs-lookup"><span data-stu-id="94e54-336">Allocate bytes of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-337">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-337">Prototype</span></span>

```c
UINT tx_byte_allocate(
    TX_BYTE_POOL *pool_ptr,
    VOID **memory_ptr, 
    ULONG memory_size,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="94e54-338">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-338">Description</span></span>

<span data-ttu-id="94e54-339">Questo servizio alloca il numero specificato di byte dal pool di byte di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-339">This service allocates the specified number of bytes from the specified memory byte pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-340">*È importante assicurarsi che il codice dell'applicazione non scriva al di fuori del blocco di memoria allocato. In tal caso, il danneggiamento si verifica in un blocco di memoria adiacente, in genere successivo. I risultati sono imprevedibili e spesso fatali.*</span><span class="sxs-lookup"><span data-stu-id="94e54-340">*It is important to ensure application code does not write outside the allocated memory block. If this happens, corruption occurs in an adjacent (usually subsequent) memory block. The results are unpredictable and often fatal!*</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-341">*Le prestazioni di questo servizio sono una funzione delle dimensioni del blocco e la quantità di frammentazione nel pool. Questo servizio non deve pertanto essere utilizzato durante i thread di esecuzione critici per il tempo.*</span><span class="sxs-lookup"><span data-stu-id="94e54-341">*The performance of this service is a function of the block size and the amount of fragmentation in the pool. Hence, this service should not be used during time-critical threads of execution.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-342">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-342">Parameters</span></span>

- <span data-ttu-id="94e54-343">**pool_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-343">**pool_ptr**</span></span> <br><span data-ttu-id="94e54-344">Puntatore a un pool di blocchi di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-344">Pointer to a previously created memory block pool.</span></span>
- <span data-ttu-id="94e54-345">**memory_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-345">**memory_ptr**</span></span> <br><span data-ttu-id="94e54-346">Puntatore a un puntatore di memoria di destinazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-346">Pointer to a destination memory pointer.</span></span> <span data-ttu-id="94e54-347">Al completamento dell'allocazione, l'indirizzo dell'area di memoria allocata viene inserito a cui punta il parametro.</span><span class="sxs-lookup"><span data-stu-id="94e54-347">On successful allocation, the address of the allocated memory area is placed where this parameter points to.</span></span>
- <span data-ttu-id="94e54-348">**memory_size**</span><span class="sxs-lookup"><span data-stu-id="94e54-348">**memory_size**</span></span> <br><span data-ttu-id="94e54-349">Numero di byte richiesti.</span><span class="sxs-lookup"><span data-stu-id="94e54-349">Number of bytes requested.</span></span>
- <span data-ttu-id="94e54-350">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="94e54-350">**wait_option**</span></span> <br><span data-ttu-id="94e54-351">Definisce il comportamento del servizio se la memoria disponibile non è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="94e54-351">Defines how the service behaves if there is not enough memory available.</span></span> <span data-ttu-id="94e54-352">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="94e54-352">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="94e54-353">**TX_NO_WAIT** (0x00000000): la selezione di **TX_NO_WAIT** comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="94e54-353">**TX_NO_WAIT** (0x00000000) - Selecting **TX_NO_WAIT** results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="94e54-354">*Questa è l'unica opzione valida se il servizio viene chiamato dall'inizializzazione.*</span><span class="sxs-lookup"><span data-stu-id="94e54-354">*This is the only valid option if the service is called from initialization.*</span></span>
  - <span data-ttu-id="94e54-355">**TX_WAIT_FOREVER** 0xFFFFFFFF): se si seleziona **TX_WAIT_FOREVER** , il thread chiamante sospenderà per un tempo illimitato fino a quando non sarà disponibile memoria sufficiente.</span><span class="sxs-lookup"><span data-stu-id="94e54-355">**TX_WAIT_FOREVER** 0xFFFFFFFF) - Selecting **TX_WAIT_FOREVER** causes the calling thread to suspend indefinitely until enough memory is available.</span></span>
  - <span data-ttu-id="94e54-356">*valore di timeout* (0x00000001 tramite 0xfffffffe)-la selezione di un valore numerico (1-0xfffffffe) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-356">*timeout value* (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the memory.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-357">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-357">Return Values</span></span>

- <span data-ttu-id="94e54-358">Allocazione di memoria riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-358">**TX_SUCCESS** (0x00) Successful memory allocation.</span></span>
- <span data-ttu-id="94e54-359">Il pool di memoria **TX_DELETED** (0x01) è stato eliminato durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-359">**TX_DELETED** (0x01) Memory pool was deleted while thread was suspended.</span></span>
- <span data-ttu-id="94e54-360">Il servizio **TX_NO_MEMORY** (0x10) non è stato in grado di allocare la memoria entro il tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-360">**TX_NO_MEMORY** (0x10) Service was unable to allocate the memory within the specified time to wait.</span></span>
- <span data-ttu-id="94e54-361">La sospensione **TX_WAIT_ABORTED** (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="94e54-361">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="94e54-362">**TX_POOL_ERROR** (0x02) puntatore al pool di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-362">**TX_POOL_ERROR** (0x02) Invalid memory pool pointer.</span></span>
- <span data-ttu-id="94e54-363">**TX_PTR_ERROR** (0x03) puntatore non valido al puntatore di destinazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-363">**TX_PTR_ERROR** (0x03) Invalid pointer to destination pointer.</span></span>
- <span data-ttu-id="94e54-364">La dimensione richiesta **TX_SIZE_ERROR** (0x05) è zero o maggiore del pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-364">**TX_SIZE_ERROR** (0X05) Requested size is zero or larger than the pool.</span></span>
- <span data-ttu-id="94e54-365">**TX_WAIT_ERROR** (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-365">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="94e54-366">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-366">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-367">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-367">Allowed From</span></span>

<span data-ttu-id="94e54-368">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="94e54-368">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-369">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-369">Preemption Possible</span></span>

<span data-ttu-id="94e54-370">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-370">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-371">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-371">Example</span></span>
```c
TX_BYTE_POOL my_pool;
unsigned char*memory_ptr;
UINT status;
/* Allocate a 112 byte memory area from my_pool. Assume
that the pool has already been created with a call to
tx_byte_pool_create. */
status = tx_byte_allocate(&my_pool, (VOID **) &memory_ptr,
    112, TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the
address of the allocated memory area. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-372">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-372">See Also</span></span>

- <span data-ttu-id="94e54-373">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-373">tx_byte_pool_create</span></span>
- <span data-ttu-id="94e54-374">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-374">tx_byte_pool_delete</span></span>
- <span data-ttu-id="94e54-375">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-375">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="94e54-376">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-376">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-377">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-377">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-378">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-378">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="94e54-379">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="94e54-379">tx_byte_release</span></span>

## <a name="tx_byte_pool_create"></a><span data-ttu-id="94e54-380">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-380">tx_byte_pool_create</span></span>

<span data-ttu-id="94e54-381">Crea pool di memoria di byte</span><span class="sxs-lookup"><span data-stu-id="94e54-381">Create memory pool of bytes</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-382">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-382">Prototype</span></span>

```c
UINT tx_byte_pool_create(
    TX_BYTE_POOL *pool_ptr,
    CHAR *name_ptr, 
    VOID *pool_start,
    ULONG pool_size);
```

### <a name="description"></a><span data-ttu-id="94e54-383">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-383">Description</span></span>

<span data-ttu-id="94e54-384">Questo servizio crea un pool di byte di memoria nell'area specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-384">This service creates a memory byte pool in the area specified.</span></span> <span data-ttu-id="94e54-385">Inizialmente il pool è costituito fondamentalmente da un blocco libero di dimensioni molto grandi.</span><span class="sxs-lookup"><span data-stu-id="94e54-385">Initially the pool consists of basically one very large free block.</span></span> <span data-ttu-id="94e54-386">Tuttavia, il pool viene suddiviso in blocchi più piccoli quando vengono apportate allocazioni.</span><span class="sxs-lookup"><span data-stu-id="94e54-386">However, the pool is broken into smaller blocks as allocations are made.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-387">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-387">Parameters</span></span>

- <span data-ttu-id="94e54-388">**pool_ptr** Puntatore a un blocco di controllo del pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-388">**pool_ptr** Pointer to a memory pool control block.</span></span>
- <span data-ttu-id="94e54-389">**name_ptr** Puntatore al nome del pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-389">**name_ptr** Pointer to the name of the memory pool.</span></span>
- <span data-ttu-id="94e54-390">**pool_start** Indirizzo iniziale del pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-390">**pool_start** Starting address of the memory pool.</span></span> <span data-ttu-id="94e54-391">L'indirizzo iniziale deve essere allineato alle dimensioni del tipo di dati ULONG.</span><span class="sxs-lookup"><span data-stu-id="94e54-391">The starting address must be aligned to the size of the ULONG data type.</span></span>
- <span data-ttu-id="94e54-392">**pool_size** Numero totale di byte disponibili per il pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-392">**pool_size** Total number of bytes available for the memory pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-393">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-393">Return Values</span></span>

- <span data-ttu-id="94e54-394">Creazione del pool di memoria riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-394">**TX_SUCCESS** (0x00) Successful memory pool creation.</span></span>
- <span data-ttu-id="94e54-395">**TX_POOL_ERROR** (0x02) puntatore al pool di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-395">**TX_POOL_ERROR** (0x02) Invalid memory pool pointer.</span></span> <span data-ttu-id="94e54-396">Il puntatore è NULL o il pool è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="94e54-396">Either the pointer is NULL or the pool is already created.</span></span>
- <span data-ttu-id="94e54-397">**TX_PTR_ERROR** (0x03) indirizzo iniziale non valido del pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-397">**TX_PTR_ERROR** (0x03) Invalid starting address of the pool.</span></span>
- <span data-ttu-id="94e54-398">Le dimensioni **TX_SIZE_ERROR** (0x05) del pool non sono valide.</span><span class="sxs-lookup"><span data-stu-id="94e54-398">**TX_SIZE_ERROR** (0x05) Size of pool is invalid.</span></span>
- <span data-ttu-id="94e54-399">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-399">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-400">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-400">Allowed From</span></span>

<span data-ttu-id="94e54-401">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="94e54-401">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-402">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-402">Preemption Possible</span></span>

<span data-ttu-id="94e54-403">No</span><span class="sxs-lookup"><span data-stu-id="94e54-403">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-404">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-404">Example</span></span>

```c
TX_BYTE_POOL my_pool;
UINT status;
/* Create a memory pool whose total size is 2000 bytes
starting at address 0x500000. */
status = tx_byte_pool_create(&my_pool, "my_pool_name",
    (VOID *) 0x500000, 2000);

/* If status equals TX_SUCCESS, my_pool is available for
allocating memory. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-405">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-405">See Also</span></span>

- <span data-ttu-id="94e54-406">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-406">tx_byte_allocate</span></span>
- <span data-ttu-id="94e54-407">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-407">tx_byte_pool_delete</span></span>
- <span data-ttu-id="94e54-408">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-408">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="94e54-409">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-409">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-410">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-410">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-411">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-411">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="94e54-412">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="94e54-412">tx_byte_release</span></span>

## <a name="tx_byte_pool_delete"></a><span data-ttu-id="94e54-413">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-413">tx_byte_pool_delete</span></span>

<span data-ttu-id="94e54-414">Elimina pool di byte di memoria</span><span class="sxs-lookup"><span data-stu-id="94e54-414">Delete memory byte pool</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-415">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-415">Prototype</span></span>

```c
UINT tx_byte_pool_delete(TX_BYTE_POOL *pool_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-416">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-416">Description</span></span>

<span data-ttu-id="94e54-417">Questo servizio Elimina il pool di byte di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-417">This service deletes the specified memory byte pool.</span></span> <span data-ttu-id="94e54-418">Tutti i thread sospesi in attesa di memoria da questo pool vengono ripresi e viene fornito un **TX_DELETED** stato restituito.</span><span class="sxs-lookup"><span data-stu-id="94e54-418">All threads suspended waiting for memory from this pool are resumed and given a **TX_DELETED** return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-419">*È responsabilità dell'applicazione gestire l'area di memoria associata al pool, disponibile al termine del servizio. Inoltre, l'applicazione deve impedire l'uso di un pool eliminato o di una memoria precedentemente allocata.*</span><span class="sxs-lookup"><span data-stu-id="94e54-419">*It is the application's responsibility to manage the memory area associated with the pool, which is available after this service completes. In addition, the application must prevent use of a deleted pool or memory previously allocated from it.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-420">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-420">Parameters</span></span>

- <span data-ttu-id="94e54-421">**pool_ptr** Puntatore a un pool di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-421">**pool_ptr** Pointer to a previously created memory pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-422">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-422">Return Values</span></span>

- <span data-ttu-id="94e54-423">Eliminazione del pool di memoria riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-423">**TX_SUCCESS** (0x00) Successful memory pool deletion.</span></span>
- <span data-ttu-id="94e54-424">**TX_POOL_ERROR** (0x02) puntatore al pool di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-424">**TX_POOL_ERROR** (0x02) Invalid memory pool pointer.</span></span>
- <span data-ttu-id="94e54-425">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-425">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-426">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-426">Allowed From</span></span>

<span data-ttu-id="94e54-427">Thread</span><span class="sxs-lookup"><span data-stu-id="94e54-427">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-428">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-428">Preemption Possible</span></span>

<span data-ttu-id="94e54-429">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-429">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-430">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-430">Example</span></span>

```c
TX_BYTE_POOL my_pool;
UINT status;
/* Delete entire memory pool. Assume that the pool has already
been created with a call to tx_byte_pool_create. */
status = tx_byte_pool_delete(&my_pool);

/* If status equals TX_SUCCESS, memory pool is deleted. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-431">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-431">See Also</span></span>

- <span data-ttu-id="94e54-432">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-432">tx_byte_allocate</span></span>
- <span data-ttu-id="94e54-433">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-433">tx_byte_pool_create</span></span>
- <span data-ttu-id="94e54-434">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-434">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="94e54-435">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-435">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-436">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-436">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-437">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-437">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="94e54-438">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="94e54-438">tx_byte_release</span></span>

## <a name="tx_byte_pool_info_get"></a><span data-ttu-id="94e54-439">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-439">tx_byte_pool_info_get</span></span>

<span data-ttu-id="94e54-440">Recuperare informazioni sul pool di byte</span><span class="sxs-lookup"><span data-stu-id="94e54-440">Retrieve information about byte pool</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-441">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-441">Prototype</span></span>

```c
UINT tx_byte_pool_info_get(
    TX_BYTE_POOL *pool_ptr, 
    CHAR **name,
    ULONG *available, 
    ULONG *fragments,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_BYTE_POOL **next_pool);
```

### <a name="description"></a><span data-ttu-id="94e54-442">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-442">Description</span></span>

<span data-ttu-id="94e54-443">Questo servizio recupera le informazioni sul pool di byte di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-443">This service retrieves information about the specified memory byte pool.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-444">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-444">Parameters</span></span>

- <span data-ttu-id="94e54-445">**pool_ptr** Puntatore al pool di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-445">**pool_ptr** Pointer to previously created memory pool.</span></span>
- <span data-ttu-id="94e54-446">**nome** Puntatore alla destinazione per il puntatore al nome del pool di byte.</span><span class="sxs-lookup"><span data-stu-id="94e54-446">**name** Pointer to destination for the pointer to the byte pool's name.</span></span>
- <span data-ttu-id="94e54-447">**disponibile** Puntatore alla destinazione per il numero di byte disponibili nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-447">**available** Pointer to destination for the number of available bytes in the pool.</span></span>
- <span data-ttu-id="94e54-448">**frammenti** Puntatore alla destinazione per il numero totale di frammenti di memoria nel pool di byte.</span><span class="sxs-lookup"><span data-stu-id="94e54-448">**fragments** Pointer to destination for the total number of memory fragments in the byte pool.</span></span>
- <span data-ttu-id="94e54-449">**first_suspended** Puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione del pool di byte.</span><span class="sxs-lookup"><span data-stu-id="94e54-449">**first_suspended** Pointer to destination for the pointer to the thread that is first on the suspension list of this byte pool.</span></span>
- <span data-ttu-id="94e54-450">**suspended_count** Puntatore alla destinazione per il numero di thread attualmente sospesi in questo pool di byte.</span><span class="sxs-lookup"><span data-stu-id="94e54-450">**suspended_count** Pointer to destination for the number of threads currently suspended on this byte pool.</span></span>
- <span data-ttu-id="94e54-451">**next_pool** Puntatore alla destinazione per l'indicatore di misura del pool di byte creato successivamente.</span><span class="sxs-lookup"><span data-stu-id="94e54-451">**next_pool** Pointer to destination for the pointer of the next created byte pool.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-452">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-452">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-453">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-453">Return Values</span></span>

- <span data-ttu-id="94e54-454">Il recupero delle informazioni sul pool riuscite **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-454">**TX_SUCCESS** (0x00) Successful pool information retrieve.</span></span>
- <span data-ttu-id="94e54-455">**TX_POOL_ERROR** (0x02) puntatore al pool di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-455">**TX_POOL_ERROR** (0x02) Invalid memory pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-456">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-456">Allowed From</span></span>

<span data-ttu-id="94e54-457">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-457">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-458">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-458">Preemption Possible</span></span>

<span data-ttu-id="94e54-459">No</span><span class="sxs-lookup"><span data-stu-id="94e54-459">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-460">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-460">Example</span></span>

```c
TX_BYTE_POOL my_pool;
CHAR *name;
ULONG available;
ULONG fragments;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_BYTE_POOL *next_pool;
UINT status;

/* Retrieve information about the previously created
block pool "my_pool." */
status = tx_byte_pool_info_get(&my_pool, &name,
  &available, &fragments,
  &first_suspended, &suspended_count,
  &next_pool);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-461">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-461">See Also</span></span>

- <span data-ttu-id="94e54-462">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-462">tx_byte_allocate</span></span>
- <span data-ttu-id="94e54-463">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-463">tx_byte_pool_create</span></span>
- <span data-ttu-id="94e54-464">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-464">tx_byte_pool_delete</span></span>
- <span data-ttu-id="94e54-465">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-465">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-466">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-466">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-467">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-467">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="94e54-468">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="94e54-468">tx_byte_release</span></span>

## <a name="tx_byte_pool_performance_info_get"></a><span data-ttu-id="94e54-469">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-469">tx_byte_pool_performance_info_get</span></span>

<span data-ttu-id="94e54-470">Ottenere informazioni sulle prestazioni del pool di byte</span><span class="sxs-lookup"><span data-stu-id="94e54-470">Get byte pool performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-471">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-471">Prototype</span></span>

```c
UINT tx_byte_pool_performance_info_get(
    TX_BYTE_POOL *pool_ptr,
    ULONG *allocates, 
    ULONG *releases,
    ULONG *fragments_searched, 
    ULONG *merges, 
    ULONG *splits,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="94e54-472">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-472">Description</span></span>

<span data-ttu-id="94e54-473">Questo servizio recupera le informazioni sulle prestazioni relative al pool di byte di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-473">This service retrieves performance information about the specified memory byte pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-474">Per restituire informazioni sulle prestazioni, *è necessario compilare la libreria threadX e l'applicazione con* **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** *definite per questo servizio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-474">*The ThreadX library and application must be built with* **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-475">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-475">Parameters</span></span>

- <span data-ttu-id="94e54-476">**pool_ptr** Puntatore al pool di byte di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-476">**pool_ptr** Pointer to previously created memory byte pool.</span></span>
- <span data-ttu-id="94e54-477">**allocazioni** Puntatore alla destinazione per il numero di richieste di allocazione eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-477">**allocates** Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="94e54-478">**versioni** di Puntatore alla destinazione per il numero di richieste di rilascio eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-478">**releases** Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="94e54-479">**fragments_searched** Puntatore alla destinazione per il numero di frammenti di memoria interni cercati durante le richieste di allocazione nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-479">**fragments_searched** Pointer to destination for the number of internal memory fragments searched during allocation requests on this pool.</span></span>
- <span data-ttu-id="94e54-480">**unioni** Puntatore alla destinazione per il numero di blocchi di memoria interni Uniti durante le richieste di allocazione nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-480">**merges** Pointer to destination for the number of internal memory blocks merged during allocation requests on this pool.</span></span>
- <span data-ttu-id="94e54-481">**divisioni** Puntatore alla destinazione per il numero di blocchi di memoria interni suddivisi (frammenti) creati durante le richieste di allocazione nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-481">**splits** Pointer to destination for the number of internal memory blocks split (fragments) created during allocation requests on this pool.</span></span>
- <span data-ttu-id="94e54-482">**sospensioni** Puntatore alla destinazione per il numero di sospensioni di allocazione di thread nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-482">**suspensions** Pointer to destination for the number of thread allocation suspensions on this pool.</span></span>
- <span data-ttu-id="94e54-483">**timeout** Puntatore alla destinazione per il numero di timeout di allocazione della sospensione nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-483">**timeouts** Pointer to destination for the number of allocate suspension timeouts on this pool.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-484">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-484">*Supplying a TX_NULL for any parameter indicates the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-485">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-485">Return Values</span></span>

- <span data-ttu-id="94e54-486">**TX_SUCCESS** (0x00) prestazioni del pool di byte riuscite.</span><span class="sxs-lookup"><span data-stu-id="94e54-486">**TX_SUCCESS** (0x00) Successful byte pool performance get.</span></span>
- <span data-ttu-id="94e54-487">**TX_PTR_ERROR** (0x03) puntatore al pool di byte non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-487">**TX_PTR_ERROR** (0x03) Invalid byte pool pointer.</span></span>
- <span data-ttu-id="94e54-488">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-488">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-489">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-489">Allowed From</span></span>

<span data-ttu-id="94e54-490">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-490">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-491">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-491">Example</span></span>

```c
TX_BYTE_POOL my_pool;
ULONG fragments_searched;
ULONG merges;
ULONG splits;
ULONG allocates;
ULONG releases;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created byte
pool. */
status = tx_byte_pool_performance_info_get(&my_pool,
  &fragments_searched,
  &merges, &splits,
  &allocates, &releases,
  &suspensions,&timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="94e54-492">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-492">See Also</span></span>

- <span data-ttu-id="94e54-493">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-493">tx_byte_allocate</span></span>
- <span data-ttu-id="94e54-494">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-494">tx_byte_pool_create</span></span>
- <span data-ttu-id="94e54-495">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-495">tx_byte_pool_delete</span></span>
- <span data-ttu-id="94e54-496">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-496">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="94e54-497">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-497">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-498">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-498">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="94e54-499">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="94e54-499">tx_byte_release</span></span>

## <a name="tx_byte_pool_performance_system_info_get"></a><span data-ttu-id="94e54-500">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-500">tx_byte_pool_performance_system_info_get</span></span>

<span data-ttu-id="94e54-501">Ottenere informazioni sulle prestazioni del sistema del pool di byte</span><span class="sxs-lookup"><span data-stu-id="94e54-501">Get byte pool system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-502">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-502">Prototype</span></span>

```c
UINT tx_byte_pool_performance_system_info_get(
    ULONG *allocates,
    ULONG *releases, 
    ULONG *fragments_searched, 
    ULONG *merges,
    ULONG *splits, 
    ULONG *suspensions, 
    ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="94e54-503">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-503">Description</span></span>

<span data-ttu-id="94e54-504">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i pool di byte di memoria nel sistema.</span><span class="sxs-lookup"><span data-stu-id="94e54-504">This service retrieves performance information about all memory byte pools in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-505">Per restituire informazioni sulle prestazioni, *è necessario compilare la libreria threadX e l'applicazione con* **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** *definite per questo servizio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-505">*The ThreadX library and application must be built with* **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-506">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-506">Parameters</span></span>

- <span data-ttu-id="94e54-507">**allocazioni** Puntatore alla destinazione per il numero di richieste di allocazione eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-507">**allocates** Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="94e54-508">**versioni** di Puntatore alla destinazione per il numero di richieste di rilascio eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="94e54-508">**releases** Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="94e54-509">**fragments_searched** Puntatore alla destinazione per il numero totale di frammenti di memoria interni ricercati durante le richieste di allocazione su tutti i pool di byte.</span><span class="sxs-lookup"><span data-stu-id="94e54-509">**fragments_searched** Pointer to destination for the total number of internal memory fragments searched during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="94e54-510">**unioni** Puntatore alla destinazione per il numero totale di blocchi di memoria interni Uniti durante le richieste di allocazione in tutti i pool di byte.</span><span class="sxs-lookup"><span data-stu-id="94e54-510">**merges** Pointer to destination for the total number of internal memory blocks merged during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="94e54-511">**divisioni** Puntatore alla destinazione per il numero totale di blocchi di memoria interni suddivisi (frammenti) creati durante le richieste di allocazione in tutti i pool di byte.</span><span class="sxs-lookup"><span data-stu-id="94e54-511">**splits** Pointer to destination for the total number of internal memory blocks split (fragments) created during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="94e54-512">**sospensioni** Puntatore alla destinazione per il numero totale di sospensioni di allocazione di thread in tutti i pool di byte.</span><span class="sxs-lookup"><span data-stu-id="94e54-512">**suspensions** Pointer to destination for the total number of thread allocation suspensions on all byte pools.</span></span>
- <span data-ttu-id="94e54-513">**timeout** Puntatore alla destinazione per il numero totale di timeout di allocazione della sospensione in tutti i pool di byte.</span><span class="sxs-lookup"><span data-stu-id="94e54-513">**timeouts** Pointer to destination for the total number of allocate suspension timeouts on all byte pools.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-514">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-514">*Supplying a TX_NULL for any parameter indicates the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-515">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-515">Return Values</span></span>

- <span data-ttu-id="94e54-516">**TX_SUCCESS** (0x00) prestazioni del pool di byte riuscite.</span><span class="sxs-lookup"><span data-stu-id="94e54-516">**TX_SUCCESS** (0x00) Successful byte pool performance get.</span></span>
- <span data-ttu-id="94e54-517">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-517">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-518">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-518">Allowed From</span></span>

 <span data-ttu-id="94e54-519">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-519">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-520">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-520">Example</span></span>

```c
ULONG fragments_searched;
ULONG merges;
ULONG splits;
ULONG allocates;
ULONG releases;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on all byte pools in the
system. */
status =
tx_byte_pool_performance_system_info_get(&fragments_searched,
  &merges, &splits, &allocates, &releases,
  &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-521">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-521">See Also</span></span>

- <span data-ttu-id="94e54-522">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-522">tx_byte_allocate</span></span>
- <span data-ttu-id="94e54-523">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-523">tx_byte_pool_create</span></span>
- <span data-ttu-id="94e54-524">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-524">tx_byte_pool_delete</span></span>
- <span data-ttu-id="94e54-525">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-525">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="94e54-526">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-526">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-527">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-527">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="94e54-528">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="94e54-528">tx_byte_release</span></span>

## <a name="tx_byte_pool_prioritize"></a><span data-ttu-id="94e54-529">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-529">tx_byte_pool_prioritize</span></span>

<span data-ttu-id="94e54-530">Priorità elenco di sospensioni del pool di byte</span><span class="sxs-lookup"><span data-stu-id="94e54-530">Prioritize byte pool suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-531">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-531">Prototype</span></span>

```c
UINT tx_byte_pool_prioritize(TX_BYTE_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="94e54-532">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-532">Description</span></span>

<span data-ttu-id="94e54-533">Questo servizio posiziona il thread con priorità più elevata sospeso per la memoria nel pool all'inizio dell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="94e54-533">This service places the highest priority thread suspended for memory on this pool at the front of the suspension list.</span></span> <span data-ttu-id="94e54-534">Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.</span><span class="sxs-lookup"><span data-stu-id="94e54-534">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-535">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-535">Parameters</span></span>

- <span data-ttu-id="94e54-536">**pool_ptr** Puntatore a un blocco di controllo del pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="94e54-536">**pool_ptr** Pointer to a memory pool control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-537">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-537">Return Values</span></span>

- <span data-ttu-id="94e54-538">**TX_SUCCESS** (0x00) priorità del pool di memoria riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-538">**TX_SUCCESS** (0x00) Successful memory pool prioritize.</span></span>
- <span data-ttu-id="94e54-539">**TX_POOL_ERROR** (0x02) puntatore al pool di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-539">**TX_POOL_ERROR** (0x02) Invalid memory pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-540">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-540">Allowed From</span></span>

<span data-ttu-id="94e54-541">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-541">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-542">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-542">Preemption Possible</span></span>

<span data-ttu-id="94e54-543">No</span><span class="sxs-lookup"><span data-stu-id="94e54-543">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-544">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-544">Example</span></span>

```c
TX_BYTE_POOL my_pool;
UINT status;

/* Ensure that the highest priority thread will receive
the next free memory from this pool. */
status = tx_byte_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_byte_release call will wake up this thread,
if there is enough memory to satisfy its request. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-545">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-545">See Also</span></span>

- <span data-ttu-id="94e54-546">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-546">tx_byte_allocate</span></span>
- <span data-ttu-id="94e54-547">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-547">tx_byte_pool_create</span></span>
- <span data-ttu-id="94e54-548">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-548">tx_byte_pool_delete</span></span>
- <span data-ttu-id="94e54-549">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-549">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="94e54-550">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-550">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-551">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-551">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-552">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="94e54-552">tx_byte_release</span></span>

## <a name="tx_byte_release"></a><span data-ttu-id="94e54-553">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="94e54-553">tx_byte_release</span></span>

<span data-ttu-id="94e54-554">Byte di rilascio nel pool di memoria</span><span class="sxs-lookup"><span data-stu-id="94e54-554">Release bytes back to memory pool</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-555">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-555">Prototype</span></span>

```c
UINT tx_byte_release(VOID *memory_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-556">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-556">Description</span></span>

<span data-ttu-id="94e54-557">Questo servizio rilascia un'area di memoria precedentemente allocata al pool associato.</span><span class="sxs-lookup"><span data-stu-id="94e54-557">This service releases a previously allocated memory area back to its associated pool.</span></span> <span data-ttu-id="94e54-558">Se uno o più thread sono sospesi in attesa di memoria da questo pool, a ogni thread sospeso viene assegnata la memoria e ripresa fino a esaurimento della memoria o fino a quando non sono presenti altri thread sospesi.</span><span class="sxs-lookup"><span data-stu-id="94e54-558">If there are one or more threads suspended waiting for memory from this pool, each suspended thread is given memory and resumed until the memory is exhausted or until there are no more suspended threads.</span></span> <span data-ttu-id="94e54-559">Questo processo di allocazione della memoria ai thread sospesi inizia sempre con il primo thread sospeso.</span><span class="sxs-lookup"><span data-stu-id="94e54-559">This process of allocating memory to suspended threads always begins with the first thread suspended.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-560">*L'applicazione deve impedire l'uso dell'area di memoria dopo che è stata rilasciata.*</span><span class="sxs-lookup"><span data-stu-id="94e54-560">*The application must prevent using the memory area after it is released.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-561">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-561">Parameters</span></span>

- <span data-ttu-id="94e54-562">**memory_ptr** Puntatore all'area di memoria allocata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-562">**memory_ptr** Pointer to the previously allocated memory area.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-563">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-563">Return Values</span></span>

- <span data-ttu-id="94e54-564">**TX_SUCCESS** (0x00) versione di memoria riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-564">**TX_SUCCESS** (0x00) Successful memory release.</span></span>
- <span data-ttu-id="94e54-565">**TX_PTR_ERROR** (0x03) puntatore all'area di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-565">**TX_PTR_ERROR** (0x03) Invalid memory area pointer.</span></span>
- <span data-ttu-id="94e54-566">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-566">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-567">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-567">Allowed From</span></span>

<span data-ttu-id="94e54-568">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="94e54-568">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-569">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-569">Preemption Possible</span></span>

<span data-ttu-id="94e54-570">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-570">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-571">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-571">Example</span></span>

```c
unsigned char *memory_ptr;
UINT status;

/* Release a memory back to my_pool. Assume that the memory
area was previously allocated from my_pool. */
status = tx_byte_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the memory pointed to by
memory_ptr has been returned to the pool. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-572">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-572">See Also</span></span>

- <span data-ttu-id="94e54-573">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="94e54-573">tx_byte_allocate</span></span>
- <span data-ttu-id="94e54-574">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="94e54-574">tx_byte_pool_create</span></span>
- <span data-ttu-id="94e54-575">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-575">tx_byte_pool_delete</span></span>
- <span data-ttu-id="94e54-576">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-576">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="94e54-577">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-577">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="94e54-578">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-578">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-579">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-579">tx_byte_pool_prioritize</span></span>

## <a name="tx_event_flags_create"></a><span data-ttu-id="94e54-580">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="94e54-580">tx_event_flags_create</span></span>

<span data-ttu-id="94e54-581">Crea gruppo di flag di evento</span><span class="sxs-lookup"><span data-stu-id="94e54-581">Create event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-582">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-582">Prototype</span></span>

```c
UINT tx_event_flags_create(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    CHAR *name_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-583">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-583">Description</span></span>

<span data-ttu-id="94e54-584">Questo servizio crea un gruppo di flag di evento 32.</span><span class="sxs-lookup"><span data-stu-id="94e54-584">This service creates a group of 32 event flags.</span></span> <span data-ttu-id="94e54-585">Tutti i flag di evento 32 nel gruppo vengono inizializzati su zero.</span><span class="sxs-lookup"><span data-stu-id="94e54-585">All 32 event flags in the group are initialized to zero.</span></span> <span data-ttu-id="94e54-586">Ogni flag di evento è rappresentato da un solo bit.</span><span class="sxs-lookup"><span data-stu-id="94e54-586">Each event flag is represented by a single bit.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-587">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-587">Parameters</span></span>

- <span data-ttu-id="94e54-588">**group_ptr** Puntatore a un blocco di controllo gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-588">**group_ptr** Pointer to an event flags group control block.</span></span>
- <span data-ttu-id="94e54-589">**name_ptr** Puntatore al nome del gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-589">**name_ptr** Pointer to the name of the event flags group.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-590">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-590">Return Values</span></span>

- <span data-ttu-id="94e54-591">Creazione del gruppo di eventi riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-591">**TX_SUCCESS** (0x00) Successful event group creation.</span></span>
- <span data-ttu-id="94e54-592">**TX_GROUP_ERROR** (0x06) puntatore al gruppo di eventi non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-592">**TX_GROUP_ERROR** (0x06) Invalid event group pointer.</span></span> <span data-ttu-id="94e54-593">Il puntatore è **null** o il gruppo di eventi è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="94e54-593">Either the pointer is **NULL** or the event group is already created.</span></span>
- <span data-ttu-id="94e54-594">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-594">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-595">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-595">Allowed From</span></span>

<span data-ttu-id="94e54-596">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="94e54-596">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-597">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-597">Preemption Possible</span></span>

<span data-ttu-id="94e54-598">No</span><span class="sxs-lookup"><span data-stu-id="94e54-598">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-599">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-599">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_group;
UINT status;

/* Create an event flags group. */
status = tx_event_flags_create(&my_event_group,
  "my_event_group_name");

/* If status equals TX_SUCCESS, my_event_group is ready
for get and set services. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-600">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-600">See Also</span></span>

- <span data-ttu-id="94e54-601">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-601">tx_event_flags_delete</span></span>
- <span data-ttu-id="94e54-602">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="94e54-602">tx_event_flags_get</span></span>
- <span data-ttu-id="94e54-603">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-603">tx_event_flags_info_get</span></span>
- <span data-ttu-id="94e54-604">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-604">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="94e54-605">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-605">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-606">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="94e54-606">tx_event_flags_set</span></span>
- <span data-ttu-id="94e54-607">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-607">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_delete"></a><span data-ttu-id="94e54-608">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-608">tx_event_flags_delete</span></span>

<span data-ttu-id="94e54-609">Elimina gruppo di flag di evento</span><span class="sxs-lookup"><span data-stu-id="94e54-609">Delete event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-610">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-610">Prototype</span></span>

```c
UINT tx_event_flags_delete(TX_EVENT_FLAGS_GROUP *group_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-611">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-611">Description</span></span>

<span data-ttu-id="94e54-612">Questo servizio Elimina il gruppo di flag di evento specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-612">This service deletes the specified event flags group.</span></span> <span data-ttu-id="94e54-613">Tutti i thread sospesi in attesa degli eventi da questo gruppo vengono ripresi e viene fornito un TX_DELETED stato restituito.</span><span class="sxs-lookup"><span data-stu-id="94e54-613">All threads suspended waiting for events from this group are resumed and given a TX_DELETED return status.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="94e54-614">*Prima di eliminare il gruppo di flag di evento, l'applicazione deve verificare che un callback di notifica per questo gruppo di flag di evento sia stato completato (o disabilitato). Inoltre, l'applicazione deve impedire l'uso futuro di un gruppo di flag di evento eliminati.*</span><span class="sxs-lookup"><span data-stu-id="94e54-614">*The application must ensure that a set notify callback for this event flags group is completed (or disabled) before deleting the event flags group. In addition, the application must prevent all future use of a deleted event flags group.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-615">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-615">Parameters</span></span>

- <span data-ttu-id="94e54-616">**group_ptr** Puntatore a un gruppo di flag evento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-616">**group_ptr** Pointer to a previously created event flags group.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-617">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-617">Return Values</span></span>

- <span data-ttu-id="94e54-618">Eliminazione del gruppo di flag di evento riuscite **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-618">**TX_SUCCESS** (0x00) Successful event flags group deletion.</span></span>
- <span data-ttu-id="94e54-619">**TX_GROUP_ERROR** (0x06) puntatore al gruppo di flag evento non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-619">**TX_GROUP_ERROR** (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="94e54-620">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-620">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-621">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-621">Allowed From</span></span>

<span data-ttu-id="94e54-622">Thread</span><span class="sxs-lookup"><span data-stu-id="94e54-622">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-623">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-623">Preemption Possible</span></span>

<span data-ttu-id="94e54-624">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-624">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-625">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-625">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_flags_group;
UINT status;

/* Delete event flags group. Assume that the group has
already been created with a call to
tx_event_flags_create. */
status = tx_event_flags_delete(&my_event_flags_group);

/* If status equals TX_SUCCESS, the event flags group is
deleted. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-626">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-626">See Also</span></span>

- <span data-ttu-id="94e54-627">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="94e54-627">tx_event_flags_create</span></span>
- <span data-ttu-id="94e54-628">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="94e54-628">tx_event_flags_get</span></span>
- <span data-ttu-id="94e54-629">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-629">tx_event_flags_info_get</span></span>
- <span data-ttu-id="94e54-630">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-630">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="94e54-631">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-631">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-632">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="94e54-632">tx_event_flags_set</span></span>
- <span data-ttu-id="94e54-633">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-633">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_get"></a><span data-ttu-id="94e54-634">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="94e54-634">tx_event_flags_get</span></span>

<span data-ttu-id="94e54-635">Ottenere i flag di evento dal gruppo di flag di evento</span><span class="sxs-lookup"><span data-stu-id="94e54-635">Get event flags from event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-636">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-636">Prototype</span></span>

```c
UINT tx_event_flags_get(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    ULONG requested_flags, 
    UINT get_option,
    ULONG *actual_flags_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="94e54-637">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-637">Description</span></span>

<span data-ttu-id="94e54-638">Questo servizio recupera i flag di evento dal gruppo di flag di evento specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-638">This service retrieves event flags from the specified event flags group.</span></span> <span data-ttu-id="94e54-639">Ogni gruppo di flag di evento contiene 32 flag di evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-639">Each event flags group contains 32 event flags.</span></span> <span data-ttu-id="94e54-640">Ogni flag è rappresentato da un solo bit.</span><span class="sxs-lookup"><span data-stu-id="94e54-640">Each flag is represented by a single bit.</span></span> <span data-ttu-id="94e54-641">Questo servizio può recuperare diverse combinazioni di flag di evento, come selezionate dai parametri di input.</span><span class="sxs-lookup"><span data-stu-id="94e54-641">This service can retrieve a variety of event flag combinations, as selected by the input parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-642">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-642">Parameters</span></span>

- <span data-ttu-id="94e54-643">**group_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-643">**group_ptr**</span></span> <br><span data-ttu-id="94e54-644">Puntatore a un gruppo di flag evento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-644">Pointer to a previously created event flags group.</span></span>
- <span data-ttu-id="94e54-645">**requested_flags**</span><span class="sxs-lookup"><span data-stu-id="94e54-645">**requested_flags**</span></span> <br><span data-ttu-id="94e54-646">variabile senza segno a 32 bit che rappresenta i flag di evento richiesti.</span><span class="sxs-lookup"><span data-stu-id="94e54-646">32-bit unsigned variable that represents the requested event flags.</span></span>
- <span data-ttu-id="94e54-647">**get_option**</span><span class="sxs-lookup"><span data-stu-id="94e54-647">**get_option**</span></span> <br><span data-ttu-id="94e54-648">Specifica se sono necessari tutti i flag di evento richiesti.</span><span class="sxs-lookup"><span data-stu-id="94e54-648">Specifies whether all or any of the requested event flags are required.</span></span> <span data-ttu-id="94e54-649">Di seguito sono riportate le selezioni valide:</span><span class="sxs-lookup"><span data-stu-id="94e54-649">The following are valid selections:</span></span>

  - <span data-ttu-id="94e54-650">**TX_AND** (0x02)</span><span class="sxs-lookup"><span data-stu-id="94e54-650">**TX_AND** (0x02)</span></span>
  - <span data-ttu-id="94e54-651">**TX_AND_CLEAR** (0x03)</span><span class="sxs-lookup"><span data-stu-id="94e54-651">**TX_AND_CLEAR** (0x03)</span></span>
  - <span data-ttu-id="94e54-652">**TX_OR** (0x00)</span><span class="sxs-lookup"><span data-stu-id="94e54-652">**TX_OR** (0x00)</span></span>
  - <span data-ttu-id="94e54-653">**TX_OR_CLEAR** (0x01)</span><span class="sxs-lookup"><span data-stu-id="94e54-653">**TX_OR_CLEAR** (0x01)</span></span>

    <span data-ttu-id="94e54-654">Selezionando TX_AND o TX_AND_CLEAR si specifica che tutti i flag di evento devono essere presenti nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="94e54-654">Selecting TX_AND or TX_AND_CLEAR specifies that all event flags must be present in the group.</span></span> <span data-ttu-id="94e54-655">Selezionando TX_OR o TX_OR_CLEAR si specifica che qualsiasi flag di evento è soddisfacente.</span><span class="sxs-lookup"><span data-stu-id="94e54-655">Selecting TX_OR or TX_OR_CLEAR     specifies that any event flag is satisfactory.</span></span> <span data-ttu-id="94e54-656">Se vengono specificati TX_AND_CLEAR o TX_OR_CLEAR, i flag di evento che soddisfano la richiesta vengono cancellati (impostati su zero).</span><span class="sxs-lookup"><span data-stu-id="94e54-656">Event flags that satisfy the request are cleared (set to zero) if TX_AND_CLEAR or TX_OR_CLEAR are specified.</span></span>

- <span data-ttu-id="94e54-657">**actual_flags_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-657">**actual_flags_ptr**</span></span> <br><span data-ttu-id="94e54-658">Puntatore alla destinazione in cui vengono inseriti i flag di evento recuperati.</span><span class="sxs-lookup"><span data-stu-id="94e54-658">Pointer to destination of where the retrieved event flags are placed.</span></span> <span data-ttu-id="94e54-659">Si noti che i flag effettivi ottenuti possono contenere flag non richiesti.</span><span class="sxs-lookup"><span data-stu-id="94e54-659">Note that the actual flags obtained may contain flags that were not requested.</span></span>
- <span data-ttu-id="94e54-660">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="94e54-660">**wait_option**</span></span>  <br><span data-ttu-id="94e54-661">Definisce il comportamento del servizio se i flag di evento selezionati non sono impostati.</span><span class="sxs-lookup"><span data-stu-id="94e54-661">Defines how the service behaves if the selected event flags are not set.</span></span> <span data-ttu-id="94e54-662">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="94e54-662">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="94e54-663">**TX_NO_WAIT** (0x00000000): la selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="94e54-663">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="94e54-664">Questa è l'unica opzione valida se il servizio viene chiamato da un non thread. ad esempio, inizializzazione, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="94e54-664">This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.</span></span>
  - <span data-ttu-id="94e54-665">Valore di timeout **TX_WAIT_FOREVER** (0xFFFFFFFF): se si seleziona TX_WAIT_FOREVER, il thread chiamante verrà sospeso per un periodo illimitato fino a quando non saranno disponibili i flag di evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-665">**TX_WAIT_FOREVER** timeout value  (0xFFFFFFFF) - Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the event flags are available.</span></span>
  - <span data-ttu-id="94e54-666">valore di timeout (0x00000001 tramite 0xFFFFFFFE)-la selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa dei flag di evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-666">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the event flags.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-667">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-667">Return Values</span></span>

- <span data-ttu-id="94e54-668">**TX_SUCCESS** (0x00) flag di evento riusciti Get.</span><span class="sxs-lookup"><span data-stu-id="94e54-668">**TX_SUCCESS** (0x00) Successful event flags get.</span></span>
- <span data-ttu-id="94e54-669">Il gruppo di flag di evento **TX_DELETED** (0x01) è stato eliminato durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-669">**TX_DELETED** (0x01) Event flags group was deleted while thread was suspended.</span></span>
- <span data-ttu-id="94e54-670">Il servizio **TX_NO_EVENTS** (0x07) non è riuscito a ottenere gli eventi specificati entro il tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-670">**TX_NO_EVENTS** (0x07) Service was unable to get the specified events within the specified time to wait.</span></span>
- <span data-ttu-id="94e54-671">La sospensione **TX_WAIT_ABORTED** (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="94e54-671">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="94e54-672">**TX_GROUP_ERROR** (0x06) puntatore al gruppo di flag evento non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-672">**TX_GROUP_ERROR** (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="94e54-673">**TX_PTR_ERROR** (0x03) puntatore non valido per i flag di evento effettivi.</span><span class="sxs-lookup"><span data-stu-id="94e54-673">**TX_PTR_ERROR** (0x03) Invalid pointer for actual event flags.</span></span>
- <span data-ttu-id="94e54-674">**TX_WAIT_ERROR** (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-674">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="94e54-675">È stato specificato **TX_OPTION_ERROR** (0x08) non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-675">**TX_OPTION_ERROR** (0x08) Invalid get-option was specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-676">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-676">Allowed From</span></span>

<span data-ttu-id="94e54-677">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-677">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-678">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-678">Preemption Possible</span></span>

<span data-ttu-id="94e54-679">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-679">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-680">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-680">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_flags_group;
ULONG actual_events;
UINT status;

/* Request that event flags 0, 4, and 8 are all set. Also,
if they are set they should be cleared. If the event
flags are not set, this service suspends for a maximum of
20 timer-ticks. */
status = tx_event_flags_get(&my_event_flags_group, 0x111,
    TX_AND_CLEAR, &actual_events, 20);

/* If status equals TX_SUCCESS, actual_events contains the
actual events obtained. */
```

<span data-ttu-id="94e54-681">**Vedere anche**</span><span class="sxs-lookup"><span data-stu-id="94e54-681">**See Also**</span></span>

- <span data-ttu-id="94e54-682">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="94e54-682">tx_event_flags_create</span></span>
- <span data-ttu-id="94e54-683">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-683">tx_event_flags_delete</span></span>
- <span data-ttu-id="94e54-684">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-684">tx_event_flags_info_get</span></span>
- <span data-ttu-id="94e54-685">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-685">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="94e54-686">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-686">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-687">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="94e54-687">tx_event_flags_set</span></span>
- <span data-ttu-id="94e54-688">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-688">tx_event_flags_set_notify</span></span>

### <a name="tx_event_flags_info_get"></a><span data-ttu-id="94e54-689">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-689">tx_event_flags_info_get</span></span>

<span data-ttu-id="94e54-690">Recupera le informazioni sul gruppo di flag di evento</span><span class="sxs-lookup"><span data-stu-id="94e54-690">Retrieve information about event flags group</span></span>

<span data-ttu-id="94e54-691">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="94e54-691">**Prototype**</span></span>

```c
UINT tx_event_flags_info_get(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    CHAR **name, ULONG *current_flags,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_EVENT_FLAGS_GROUP **next_group);
```

<span data-ttu-id="94e54-692">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="94e54-692">**Description**</span></span>

<span data-ttu-id="94e54-693">Questo servizio recupera le informazioni sul gruppo di flag di evento specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-693">This service retrieves information about the specified event flags group.</span></span>

<span data-ttu-id="94e54-694">**Parametri**</span><span class="sxs-lookup"><span data-stu-id="94e54-694">**Parameters**</span></span>

- <span data-ttu-id="94e54-695">**group_ptr** Puntatore a un blocco di controllo gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-695">**group_ptr** Pointer to an event flags group control block.</span></span>
- <span data-ttu-id="94e54-696">**nome** Puntatore alla destinazione per il puntatore al nome del gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-696">**name** Pointer to destination for the pointer to the event flags group's name.</span></span>
- <span data-ttu-id="94e54-697">**current_flags** Puntatore alla destinazione per i flag del set corrente nel gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-697">**current_flags** Pointer to destination for the current set flags in the event flags group.</span></span>
- <span data-ttu-id="94e54-698">**first_suspended** Puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione del gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-698">**first_suspended** Pointer to destination for the pointer to the thread that is first on the suspension list of this event flags group.</span></span>
- <span data-ttu-id="94e54-699">**suspended_count** Puntatore alla destinazione per il numero di thread attualmente sospesi in questo gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-699">**suspended_count** Pointer to destination for the number of threads currently suspended on this event flags group.</span></span>
- <span data-ttu-id="94e54-700">**next_group** Puntatore alla destinazione per l'indicatore di misura del gruppo di flag di evento creato successivo.</span><span class="sxs-lookup"><span data-stu-id="94e54-700">**next_group** Pointer to destination for the pointer of the next created event flags group.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-701">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-701">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-702">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-702">Return Values</span></span>

- <span data-ttu-id="94e54-703">Il recupero delle informazioni del gruppo di eventi **TX_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="94e54-703">**TX_SUCCESS** (0x00) Successful event group information retrieval.</span></span>
- <span data-ttu-id="94e54-704">**TX_GROUP_ERROR** (0x06) puntatore al gruppo di eventi non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-704">**TX_GROUP_ERROR** (0x06) Invalid event group pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-705">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-705">Allowed From</span></span>

<span data-ttu-id="94e54-706">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-706">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-707">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-707">Preemption Possible</span></span>

<span data-ttu-id="94e54-708">No</span><span class="sxs-lookup"><span data-stu-id="94e54-708">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-709">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-709">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_group;
CHAR *name;
ULONG current_flags;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_EVENT_FLAGS_GROUP *next_group;
UINT status;

/* Retrieve information about the previously created
event flags group "my_event_group." */
status = tx_event_flags_info_get(&my_event_group, &name,
    &current_flags,
    &first_suspended, &suspended_count,
    &next_group);
/* If status equals TX_SUCCESS, the information requested is
valid. */
```
<span data-ttu-id="94e54-710">**Vedere anche**</span><span class="sxs-lookup"><span data-stu-id="94e54-710">**See Also**</span></span>

- <span data-ttu-id="94e54-711">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="94e54-711">tx_event_flags_create</span></span>
- <span data-ttu-id="94e54-712">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-712">tx_event_flags_delete</span></span>
- <span data-ttu-id="94e54-713">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="94e54-713">tx_event_flags_get</span></span>
- <span data-ttu-id="94e54-714">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-714">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="94e54-715">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-715">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-716">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="94e54-716">tx_event_flags_set</span></span>
- <span data-ttu-id="94e54-717">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-717">tx_event_flags_set_notify</span></span>

### <a name="tx_event_flags_performance_info_get"></a><span data-ttu-id="94e54-718">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-718">tx_event_flags_performance_info_get</span></span>

<span data-ttu-id="94e54-719">Ottenere le informazioni sulle prestazioni del gruppo flag evento</span><span class="sxs-lookup"><span data-stu-id="94e54-719">Get event flags group performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-720">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-720">Prototype</span></span>

```c
UINT tx_event_flags_performance_info_get(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    ULONG *sets, ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="94e54-721">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-721">Description</span></span>

<span data-ttu-id="94e54-722">Questo servizio recupera le informazioni sulle prestazioni relative al gruppo di flag di evento specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-722">This service retrieves performance information about the specified event flags group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-723">Per restituire informazioni sulle prestazioni, *è necessario compilare la libreria threadX e l'applicazione con* **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** *definite per questo servizio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-723">*ThreadX library and application must be built with* **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-724">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-724">Parameters</span></span>

- <span data-ttu-id="94e54-725">**group_ptr** Puntatore al gruppo di flag evento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-725">**group_ptr** Pointer to previously created event flags group.</span></span>
- <span data-ttu-id="94e54-726">**set** di Puntatore alla destinazione per il numero di flag di evento impostati richieste eseguite su questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="94e54-726">**sets** Pointer to destination for the number of event flags set requests performed on this group.</span></span>
- <span data-ttu-id="94e54-727">**ottiene** Puntatore alla destinazione per il numero di richieste Get dei flag di evento eseguite su questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="94e54-727">**gets** Pointer to destination for the number of event flags get requests performed on this group.</span></span>
- <span data-ttu-id="94e54-728">**sospensioni** Puntatore alla destinazione per il numero di flag evento thread Get suspends in questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="94e54-728">**suspensions** Pointer to destination for the number of thread event flags get suspensions on this group.</span></span>
- <span data-ttu-id="94e54-729">**timeout** Puntatore alla destinazione per il numero di flag di evento ottenere i timeout di sospensione in questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="94e54-729">**timeouts** Pointer to destination for the number of event flags get suspension timeouts on this group.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-730">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-730">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-731">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-731">Return Values</span></span>

- <span data-ttu-id="94e54-732">**TX_SUCCESS** (0x00) risultati del gruppo di flag di evento riusciti Get.</span><span class="sxs-lookup"><span data-stu-id="94e54-732">**TX_SUCCESS** (0x00) Successful event flags group performance get.</span></span>
- <span data-ttu-id="94e54-733">**TX_PTR_ERROR** (0x03) puntatore al gruppo di flag evento non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-733">**TX_PTR_ERROR** (0x03) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="94e54-734">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-734">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-735">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-735">Allowed From</span></span>

<span data-ttu-id="94e54-736">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-736">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-737">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-737">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_flag_group;
ULONG sets;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created event
flag group. */
status = tx_event_flags_performance_info_get(&my_event_flag_group,
    &sets, &gets, &suspensions,
    &timeouts);

/* If status is TX_SUCCESS the performance information was successfully
retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-738">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-738">See Also</span></span>

- <span data-ttu-id="94e54-739">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="94e54-739">tx_event_flags_create</span></span>
- <span data-ttu-id="94e54-740">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-740">tx_event_flags_delete</span></span>
- <span data-ttu-id="94e54-741">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="94e54-741">tx_event_flags_get</span></span>
- <span data-ttu-id="94e54-742">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-742">tx_event_flags_info_get</span></span>
- <span data-ttu-id="94e54-743">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-743">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-744">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="94e54-744">tx_event_flags_set</span></span>
- <span data-ttu-id="94e54-745">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-745">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_performance_system_info_get"></a><span data-ttu-id="94e54-746">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-746">tx_event_flags_performance_system_info_get</span></span>

<span data-ttu-id="94e54-747">Recuperare informazioni sul sistema delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="94e54-747">Retrieve performance system information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-748">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-748">Prototype</span></span>

```c
UINT tx_event_flags_performance_system_info_get(
    ULONG *sets,
    ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="94e54-749">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-749">Description</span></span>

<span data-ttu-id="94e54-750">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i gruppi di flag di evento nel sistema.</span><span class="sxs-lookup"><span data-stu-id="94e54-750">This service retrieves performance information about all event flags groups in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-751">Per restituire informazioni sulle prestazioni, *è necessario compilare la libreria threadX e l'applicazione con* **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** *definite per questo servizio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-751">*ThreadX library and application must be built with* **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-752">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-752">Parameters</span></span>

- <span data-ttu-id="94e54-753">**set** di Puntatore alla destinazione per il numero totale di flag di evento che impostano le richieste eseguite su tutti i gruppi.</span><span class="sxs-lookup"><span data-stu-id="94e54-753">**sets** Pointer to destination for the total number of event flags set requests performed on all groups.</span></span>
- <span data-ttu-id="94e54-754">**ottiene** Puntatore alla destinazione per il numero totale di richieste Get dei flag di evento eseguite su tutti i gruppi.</span><span class="sxs-lookup"><span data-stu-id="94e54-754">**gets** Pointer to destination for the total number of event flags get requests performed on all groups.</span></span>
- <span data-ttu-id="94e54-755">**sospensioni** Puntatore alla destinazione per il numero totale di flag evento thread Get suspends in tutti i gruppi.</span><span class="sxs-lookup"><span data-stu-id="94e54-755">**suspensions** Pointer to destination for the total number of thread event flags get suspensions on all groups.</span></span>
- <span data-ttu-id="94e54-756">**timeout** Puntatore alla destinazione per il numero totale di flag evento ottenere i timeout di sospensione in tutti i gruppi.</span><span class="sxs-lookup"><span data-stu-id="94e54-756">**timeouts** Pointer to destination for the total number of event flags get suspension timeouts on all groups.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-757">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-757">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-758">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-758">Return Values</span></span>

- <span data-ttu-id="94e54-759">**TX_SUCCESS** (0x00) flag di evento riusciti prestazioni del sistema Get.</span><span class="sxs-lookup"><span data-stu-id="94e54-759">**TX_SUCCESS** (0x00) Successful event flags system performance get.</span></span>
- <span data-ttu-id="94e54-760">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-760">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="example"></a><span data-ttu-id="94e54-761">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-761">Example</span></span>

```c
ULONG sets;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on all previously created event
flag groups. */
status = tx_event_flags_performance_system_info_get(&sets, &gets,
    &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-762">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-762">See Also</span></span>

- <span data-ttu-id="94e54-763">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="94e54-763">tx_event_flags_create</span></span>
- <span data-ttu-id="94e54-764">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-764">tx_event_flags_delete</span></span>
- <span data-ttu-id="94e54-765">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="94e54-765">tx_event_flags_get</span></span>
- <span data-ttu-id="94e54-766">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-766">tx_event_flags_info_get</span></span>
- <span data-ttu-id="94e54-767">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-767">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="94e54-768">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="94e54-768">tx_event_flags_set</span></span>
- <span data-ttu-id="94e54-769">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-769">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_set"></a><span data-ttu-id="94e54-770">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="94e54-770">tx_event_flags_set</span></span>

<span data-ttu-id="94e54-771">Impostare i flag di evento in un gruppo di flag di evento</span><span class="sxs-lookup"><span data-stu-id="94e54-771">Set event flags in an event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-772">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-772">Prototype</span></span>

```c
UINT tx_event_flags_set(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    ULONG flags_to_set,
    UINT set_option);
```

### <a name="description"></a><span data-ttu-id="94e54-773">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-773">Description</span></span>

<span data-ttu-id="94e54-774">Questo servizio imposta o cancella i flag di evento in un gruppo di flag di evento, a seconda dell'opzione set specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-774">This service sets or clears event flags in an event flags group, depending upon the specified set-option.</span></span> <span data-ttu-id="94e54-775">Vengono ripresi tutti i thread sospesi la cui richiesta di flag evento è ora soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="94e54-775">All suspended threads whose event flags request is now satisfied are resumed.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-776">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-776">Parameters</span></span>

- <span data-ttu-id="94e54-777">**group_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-777">**group_ptr**</span></span> <br><span data-ttu-id="94e54-778">Puntatore al blocco di controllo del gruppo di flag di evento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-778">Pointer to the previously created event flags group control block.</span></span>
- <span data-ttu-id="94e54-779">**flags_to_set**</span><span class="sxs-lookup"><span data-stu-id="94e54-779">**flags_to_set**</span></span> <br><span data-ttu-id="94e54-780">Specifica i flag evento da impostare o deselezionare in base all'opzione set selezionata.</span><span class="sxs-lookup"><span data-stu-id="94e54-780">Specifies the event flags to set or clear based upon the set option selected.</span></span>
- <span data-ttu-id="94e54-781">**set_option**</span><span class="sxs-lookup"><span data-stu-id="94e54-781">**set_option**</span></span> <br><span data-ttu-id="94e54-782">Specifica se i flag di evento specificati sono individuato o ORed nei flag di evento correnti del gruppo.</span><span class="sxs-lookup"><span data-stu-id="94e54-782">Specifies whether the event flags specified are ANDed or ORed into the current event flags of the group.</span></span> <span data-ttu-id="94e54-783">Di seguito sono riportate le selezioni valide:</span><span class="sxs-lookup"><span data-stu-id="94e54-783">The following are valid selections:</span></span>
  - <span data-ttu-id="94e54-784">**TX_AND** (0x02)</span><span class="sxs-lookup"><span data-stu-id="94e54-784">**TX_AND** (0x02)</span></span>
  - <span data-ttu-id="94e54-785">**TX_OR** (0x00)</span><span class="sxs-lookup"><span data-stu-id="94e54-785">**TX_OR** (0x00)</span></span>

  <span data-ttu-id="94e54-786">Selezionando TX_AND si specifica che i flag di evento specificati sono **e e** nei flag di evento correnti del gruppo.</span><span class="sxs-lookup"><span data-stu-id="94e54-786">Selecting TX_AND specifies that the specified event flags are **AND** ed into the current event flags in the group.</span></span> <span data-ttu-id="94e54-787">Questa opzione viene spesso usata per cancellare i flag di evento in un gruppo.</span><span class="sxs-lookup"><span data-stu-id="94e54-787">This option is often used to clear event flags in a group.</span></span> <span data-ttu-id="94e54-788">In caso contrario, se viene specificato TX_OR, i flag di evento specificati sono **o** ed con l'evento corrente nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="94e54-788">Otherwise, if TX_OR is specified, the specified event flags are **OR** ed with the current event in the group.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-789">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-789">Return Values</span></span>
- <span data-ttu-id="94e54-790">**TX_SUCCESS** (0x00) flag di evento riusciti impostati.</span><span class="sxs-lookup"><span data-stu-id="94e54-790">**TX_SUCCESS** (0x00) Successful event flags set.</span></span>
- <span data-ttu-id="94e54-791">**TX_GROUP_ERROR** (0x06) puntatore non valido al gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-791">**TX_GROUP_ERROR** (0x06) Invalid pointer to event flags group.</span></span>
- <span data-ttu-id="94e54-792">**TX_OPTION_ERROR** (0x08) set-Option non valido specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-792">**TX_OPTION_ERROR** (0x08) Invalid set-option specified.</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-793">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-793">Preemption Possible</span></span>

<span data-ttu-id="94e54-794">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-794">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-795">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-795">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_event_flags_group;
UINT status;

/* Set event flags 0, 4, and 8. */
status = tx_event_flags_set(&my_event_flags_group,
    0x111, TX_OR);

/* If status equals TX_SUCCESS, the event flags have been
set and any suspended thread whose request was satisfied
has been resumed. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-796">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-796">See Also</span></span>

- <span data-ttu-id="94e54-797">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="94e54-797">tx_event_flags_create</span></span>
- <span data-ttu-id="94e54-798">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-798">tx_event_flags_delete</span></span>
- <span data-ttu-id="94e54-799">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="94e54-799">tx_event_flags_get</span></span>
- <span data-ttu-id="94e54-800">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-800">tx_event_flags_info_get</span></span>
- <span data-ttu-id="94e54-801">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-801">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="94e54-802">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-802">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-803">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-803">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_set_notify"></a><span data-ttu-id="94e54-804">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-804">tx_event_flags_set_notify</span></span>

<span data-ttu-id="94e54-805">Invia notifica all'applicazione quando vengono impostati i flag evento</span><span class="sxs-lookup"><span data-stu-id="94e54-805">Notify application when event flags are set</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-806">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-806">Prototype</span></span>

```c
UINT tx_event_flags_set_notify(
    TX_EVENT_FLAGS_GROUP *group_ptr,
    VOID (*events_set_notify)(TX_EVENT_FLAGS_GROUP *));
```

### <a name="description"></a><span data-ttu-id="94e54-807">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-807">Description</span></span>

<span data-ttu-id="94e54-808">Questo servizio registra una funzione di callback delle notifiche chiamata ogni volta che uno o più flag di evento vengono impostati nel gruppo di flag di evento specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-808">This service registers a notification callback function that is called whenever one or more event flags are set in the specified event flags group.</span></span> <span data-ttu-id="94e54-809">L'elaborazione del callback di notifica è definita dal</span><span class="sxs-lookup"><span data-stu-id="94e54-809">The processing of the notification callback is defined by the</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-810">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-810">Parameters</span></span>
- <span data-ttu-id="94e54-811">**group_ptr** Puntatore al gruppo di flag evento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-811">**group_ptr** Pointer to previously created event flags group.</span></span>
- <span data-ttu-id="94e54-812">**events_set_notify** Puntatore alla funzione di notifica del set di flag evento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-812">**events_set_notify** Pointer to application's event flags set notification function.</span></span> <span data-ttu-id="94e54-813">Se questo valore è TX_NULL, la notifica è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="94e54-813">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-814">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-814">Return Values</span></span>

- <span data-ttu-id="94e54-815">**TX_SUCCESS** (0x00) registrazione corretta della notifica del set di flag evento.</span><span class="sxs-lookup"><span data-stu-id="94e54-815">**TX_SUCCESS** (0x00) Successful registration of event flags set notification.</span></span>
- <span data-ttu-id="94e54-816">**TX_GROUP_ERROR** (0x06) puntatore al gruppo di flag evento non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-816">**TX_GROUP_ERROR** (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="94e54-817">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema è stato compilato con le funzionalità di notifica disabilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-817">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="example"></a><span data-ttu-id="94e54-818">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-818">Example</span></span>

```c
TX_EVENT_FLAGS_GROUP my_group;

/* Register the "my_event_flags_set_notify" function for monitoring
event flags set in the event flags group "my_group." */
status = tx_event_flags_set_notify(&my_group, my_event_flags_set_notify);

/* If status is TX_SUCCESS the event flags set notification function
was successfully registered. */
void my_event_flags_set_notify(TX_EVENT_FLAGS_GROUP *group_ptr)

/* One or more event flags was set in this group! */
```

### <a name="see-also"></a><span data-ttu-id="94e54-819">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-819">See Also</span></span>

- <span data-ttu-id="94e54-820">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="94e54-820">tx_event_flags_create</span></span>
- <span data-ttu-id="94e54-821">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-821">tx_event_flags_delete</span></span>
- <span data-ttu-id="94e54-822">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="94e54-822">tx_event_flags_get</span></span>
- <span data-ttu-id="94e54-823">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-823">tx_event_flags_info_get</span></span>
- <span data-ttu-id="94e54-824">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-824">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="94e54-825">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-825">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-826">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="94e54-826">tx_event_flags_set</span></span>

## <a name="tx_interrupt_control"></a><span data-ttu-id="94e54-827">tx_interrupt_control</span><span class="sxs-lookup"><span data-stu-id="94e54-827">tx_interrupt_control</span></span>

<span data-ttu-id="94e54-828">Abilitazione e disabilitazione degli interrupt</span><span class="sxs-lookup"><span data-stu-id="94e54-828">Enable and disable interrupts</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-829">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-829">Prototype</span></span>

```c
UINT tx_interrupt_control(UINT new_posture);
```

### <a name="description"></a><span data-ttu-id="94e54-830">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-830">Description</span></span>

<span data-ttu-id="94e54-831">Questo servizio Abilita o Disabilita gli interrupt come specificato dal parametro di input *new_posture*.</span><span class="sxs-lookup"><span data-stu-id="94e54-831">This service enables or disables interrupts as specified by the input parameter *new_posture*.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-832">*Se questo servizio viene chiamato da un thread dell'applicazione, la postura di interrupt rimane parte del contesto del thread. Ad esempio, se il thread chiama questa routine per disabilitare gli interrupt e quindi sospendere, quando viene ripreso, gli interrupt vengono nuovamente disabilitati.*</span><span class="sxs-lookup"><span data-stu-id="94e54-832">*If this service is called from an application thread, the interrupt posture remains part of that thread's context. For example, if the thread calls this routine to disable interrupts and then suspends, when it is resumed, interrupts are disabled again.*</span></span>

> [!WARNING]
> <span data-ttu-id="94e54-833">*Questo servizio non deve essere usato per abilitare gli interrupt durante l'inizializzazione. Questa operazione può causare risultati imprevedibili.*</span><span class="sxs-lookup"><span data-stu-id="94e54-833">*This service should not be used to enable interrupts during initialization! Doing so could cause unpredictable results.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-834">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-834">Parameters</span></span>

- <span data-ttu-id="94e54-835">**new_posture** Questo parametro specifica se gli interrupt sono disabilitati o abilitati.</span><span class="sxs-lookup"><span data-stu-id="94e54-835">**new_posture** This parameter specifies whether interrupts are disabled or enabled.</span></span> <span data-ttu-id="94e54-836">I valori validi includono **TX_INT_DISABLE** e **TX_INT_ENABLE**.</span><span class="sxs-lookup"><span data-stu-id="94e54-836">Legal values include **TX_INT_DISABLE** and **TX_INT_ENABLE**.</span></span> <span data-ttu-id="94e54-837">I valori effettivi di questi parametri sono specifici della porta.</span><span class="sxs-lookup"><span data-stu-id="94e54-837">The actual values for these parameters are port specific.</span></span> <span data-ttu-id="94e54-838">Alcune architetture di elaborazione possono inoltre supportare le posture di disabilitazione di interrupt aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="94e54-838">In addition, some processing architectures might support additional interrupt disable postures.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-839">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-839">Return Values</span></span>
- <span data-ttu-id="94e54-840">**posizione precedente** Questo servizio restituisce la postura di interrupt precedente al chiamante.</span><span class="sxs-lookup"><span data-stu-id="94e54-840">**previous posture** This service returns the previous interrupt posture to the caller.</span></span> <span data-ttu-id="94e54-841">In questo modo gli utenti del servizio possono ripristinare la postura precedente dopo la disabilitazione degli interrupt.</span><span class="sxs-lookup"><span data-stu-id="94e54-841">This allows users of the service to restore the previous posture after interrupts are disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-842">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-842">Allowed From</span></span>

<span data-ttu-id="94e54-843">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-843">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-844">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-844">Preemption Possible</span></span>

<span data-ttu-id="94e54-845">No</span><span class="sxs-lookup"><span data-stu-id="94e54-845">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-846">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-846">Example</span></span>

```c
UINT my_old_posture;

/* Lockout interrupts */
my_old_posture = tx_interrupt_control(TX_INT_DISABLE);

/* Perform critical operations that need interrupts
locked-out.... */

/* Restore previous interrupt lockout posture. */
tx_interrupt_control(my_old_posture);
```

### <a name="see-also"></a><span data-ttu-id="94e54-847">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-847">See Also</span></span>

<span data-ttu-id="94e54-848">nessuno</span><span class="sxs-lookup"><span data-stu-id="94e54-848">None</span></span>

## <a name="tx_mutex_create"></a><span data-ttu-id="94e54-849">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="94e54-849">tx_mutex_create</span></span>

<span data-ttu-id="94e54-850">Crea mutex di esclusione reciproca</span><span class="sxs-lookup"><span data-stu-id="94e54-850">Create mutual exclusion mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-851">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-851">Prototype</span></span>

```c
UINT tx_mutex_create(
    TX_MUTEX *mutex_ptr,
    CHAR *name_ptr, 
    UINT priority_inherit);
```

### <a name="description"></a><span data-ttu-id="94e54-852">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-852">Description</span></span>

<span data-ttu-id="94e54-853">Questo servizio crea un mutex per l'esclusione reciproca tra thread per la protezione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="94e54-853">This service creates a mutex for inter-thread mutual exclusion for resource protection.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-854">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-854">Parameters</span></span>

- <span data-ttu-id="94e54-855">**mutex_ptr** Puntatore a un blocco di controllo mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-855">**mutex_ptr** Pointer to a mutex control block.</span></span>
- <span data-ttu-id="94e54-856">**name_ptr** Puntatore al nome del mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-856">**name_ptr** Pointer to the name of the mutex.</span></span>
- <span data-ttu-id="94e54-857">**priority_inherit** Specifica se questo mutex supporta l'ereditarietà prioritaria.</span><span class="sxs-lookup"><span data-stu-id="94e54-857">**priority_inherit** Specifies whether or not this mutex supports priority inheritance.</span></span> <span data-ttu-id="94e54-858">Se questo valore è TX_INHERIT, l'ereditarietà della priorità è supportata.</span><span class="sxs-lookup"><span data-stu-id="94e54-858">If this value is TX_INHERIT, then priority inheritance is supported.</span></span> <span data-ttu-id="94e54-859">Tuttavia, se si specifica TX_NO_INHERIT, l'ereditarietà della priorità non è supportata da questo mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-859">However, if TX_NO_INHERIT is specified, priority inheritance is not supported by this mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-860">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-860">Return Values</span></span>

- <span data-ttu-id="94e54-861">Creazione mutex riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-861">**TX_SUCCESS** (0x00) Successful mutex creation.</span></span>
- <span data-ttu-id="94e54-862">**TX_MUTEX_ERROR** (0x1C) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-862">**TX_MUTEX_ERROR** (0x1C) Invalid mutex pointer.</span></span> <span data-ttu-id="94e54-863">Il puntatore è NULL o il mutex è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="94e54-863">Either the pointer is NULL or the mutex is already created.</span></span>
- <span data-ttu-id="94e54-864">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-864">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>
- <span data-ttu-id="94e54-865">Il parametro **TX_INHERIT_ERROR** (0X1F) non valido eredita la priorità.</span><span class="sxs-lookup"><span data-stu-id="94e54-865">**TX_INHERIT_ERROR** (0x1F) Invalid priority inherit parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-866">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-866">Allowed From</span></span>

<span data-ttu-id="94e54-867">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="94e54-867">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-868">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-868">Preemption Possible</span></span>

<span data-ttu-id="94e54-869">No</span><span class="sxs-lookup"><span data-stu-id="94e54-869">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-870">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-870">Example</span></span>

```c
TX_MUTEX my_mutex;
UINT status;

/* Create a mutex to provide protection over a
common resource. */
status = tx_mutex_create(&my_mutex,"my_mutex_name",
    TX_NO_INHERIT);

/* If status equals TX_SUCCESS, my_mutex is ready for
use. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-871">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-871">See Also</span></span>

- <span data-ttu-id="94e54-872">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-872">tx_mutex_delete</span></span>
- <span data-ttu-id="94e54-873">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="94e54-873">tx_mutex_get</span></span>
- <span data-ttu-id="94e54-874">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-874">tx_mutex_info_get</span></span>
- <span data-ttu-id="94e54-875">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-875">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="94e54-876">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-876">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-877">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-877">tx_mutex_prioritize</span></span>
- <span data-ttu-id="94e54-878">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="94e54-878">tx_mutex_put</span></span>

## <a name="tx_mutex_delete"></a><span data-ttu-id="94e54-879">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-879">tx_mutex_delete</span></span>

<span data-ttu-id="94e54-880">Elimina mutex di esclusione reciproca</span><span class="sxs-lookup"><span data-stu-id="94e54-880">Delete mutual exclusion mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-881">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-881">Prototype</span></span>

```c
UINT tx_mutex_delete(TX_MUTEX *mutex_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-882">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-882">Description</span></span>

<span data-ttu-id="94e54-883">Questo servizio Elimina il mutex specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-883">This service deletes the specified mutex.</span></span> <span data-ttu-id="94e54-884">Tutti i thread sospesi in attesa del mutex vengono ripresi e viene fornito un **TX_DELETED** stato restituito.</span><span class="sxs-lookup"><span data-stu-id="94e54-884">All threads suspended waiting for the mutex are resumed and given a **TX_DELETED** return status.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-885">*È responsabilità dell'applicazione impedire l'uso di un mutex eliminato.*</span><span class="sxs-lookup"><span data-stu-id="94e54-885">*It is the application's responsibility to prevent use of a deleted mutex.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-886">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-886">Parameters</span></span>

- <span data-ttu-id="94e54-887">**mutex_ptr** Puntatore a un mutex creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-887">**mutex_ptr** Pointer to a previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-888">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-888">Return Values</span></span>

- <span data-ttu-id="94e54-889">Eliminazione di mutex riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-889">**TX_SUCCESS** (0x00) Successful mutex deletion.</span></span>
- <span data-ttu-id="94e54-890">**TX_MUTEX_ERROR** (0x1C) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-890">**TX_MUTEX_ERROR** (0x1C) Invalid mutex pointer.</span></span>
- <span data-ttu-id="94e54-891">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-891">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-892">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-892">Allowed From</span></span>

<span data-ttu-id="94e54-893">Thread</span><span class="sxs-lookup"><span data-stu-id="94e54-893">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-894">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-894">Preemption Possible</span></span>

<span data-ttu-id="94e54-895">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-895">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-896">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-896">Example</span></span>

```c
TX_MUTEX my_mutex;
UINT status;

/* Delete a mutex. Assume that the mutex
has already been created. */
status = tx_mutex_delete(&my_mutex);

/* If status equals TX_SUCCESS, the mutex is
deleted. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-897">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-897">See Also</span></span>

- <span data-ttu-id="94e54-898">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="94e54-898">tx_mutex_create</span></span>
- <span data-ttu-id="94e54-899">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="94e54-899">tx_mutex_get</span></span>
- <span data-ttu-id="94e54-900">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-900">tx_mutex_info_get</span></span>
- <span data-ttu-id="94e54-901">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-901">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="94e54-902">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-902">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-903">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-903">tx_mutex_prioritize</span></span>
- <span data-ttu-id="94e54-904">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="94e54-904">tx_mutex_put</span></span>

## <a name="tx_mutex_get"></a><span data-ttu-id="94e54-905">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="94e54-905">tx_mutex_get</span></span>

<span data-ttu-id="94e54-906">Ottenere la proprietà di mutex</span><span class="sxs-lookup"><span data-stu-id="94e54-906">Obtain ownership of mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-907">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-907">Prototype</span></span>

```c
UINT tx_mutex_get(
    TX_MUTEX *mutex_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="94e54-908">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-908">Description</span></span>

<span data-ttu-id="94e54-909">Questo servizio tenta di ottenere la proprietà esclusiva del mutex specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-909">This service attempts to obtain exclusive ownership of the specified mutex.</span></span> <span data-ttu-id="94e54-910">Se il thread chiamante è già proprietario del mutex, viene incrementato un contatore interno e viene restituito uno stato di esito positivo.</span><span class="sxs-lookup"><span data-stu-id="94e54-910">If the calling thread already owns the mutex, an internal counter is incremented and a successful status is returned.</span></span>

<span data-ttu-id="94e54-911">Se il mutex è di proprietà di un altro thread e questo thread è con priorità più elevata e l'ereditarietà della priorità è stata specificata al momento della creazione del mutex, la priorità del thread con priorità inferiore verrà generata temporaneamente a quella del thread chiamante.</span><span class="sxs-lookup"><span data-stu-id="94e54-911">If the mutex is owned by another thread and this thread is higher priority and priority inheritance was specified at mutex create, the lower priority thread's priority will be temporarily raised to that of the calling thread.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-912">*La priorità del thread con priorità inferiore che possiede un mutex con priorityinheritance non deve mai essere modificata da un thread esterno durante la proprietà del mutex.*</span><span class="sxs-lookup"><span data-stu-id="94e54-912">*The priority of the lower priority thread owning a mutex with priorityinheritance should never be modified by an external thread during mutex ownership.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-913">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-913">Parameters</span></span>

- <span data-ttu-id="94e54-914">**mutex_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-914">**mutex_ptr**</span></span>   <br><span data-ttu-id="94e54-915">Puntatore a un mutex creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-915">Pointer to a previously created mutex.</span></span>
- <span data-ttu-id="94e54-916">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="94e54-916">**wait_option**</span></span> <br><span data-ttu-id="94e54-917">Definisce il comportamento del servizio se il mutex è già di proprietà di un altro thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-917">Defines how the service behaves if the mutex is already owned by another thread.</span></span> <span data-ttu-id="94e54-918">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="94e54-918">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="94e54-919">**TX_NO_WAIT** (0x00000000): la selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="94e54-919">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="94e54-920">*Questa è l'unica opzione valida se il servizio viene chiamato dall'inizializzazione.*</span><span class="sxs-lookup"><span data-stu-id="94e54-920">*This is the only valid option if the service is called from Initialization.*</span></span>
  - <span data-ttu-id="94e54-921">Valore di timeout **TX_WAIT_FOREVER** (0xFFFFFFFF): se si seleziona **TX_WAIT_FOREVER** , il thread chiamante verrà sospeso per un tempo illimitato fino a quando non sarà disponibile il mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-921">**TX_WAIT_FOREVER** timeout value (0xFFFFFFFF) - Selecting **TX_WAIT_FOREVER** causes the calling thread to suspend indefinitely until the mutex is available.</span></span>
  - <span data-ttu-id="94e54-922">valore di timeout (0x00000001 tramite 0xFFFFFFFE)-la selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi in attesa del mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-922">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-923">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-923">Return Values</span></span>

- <span data-ttu-id="94e54-924">**TX_SUCCESS** (0x00) operazione di Get mutex riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-924">**TX_SUCCESS** (0x00) Successful mutex get operation.</span></span>
- <span data-ttu-id="94e54-925">Il mutex **TX_DELETED** (0x01) è stato eliminato durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-925">**TX_DELETED** (0x01) Mutex was deleted while thread was suspended.</span></span>
- <span data-ttu-id="94e54-926">Il servizio **TX_NOT_AVAILABLE** (0x1d) non è stato in grado di ottenere la proprietà del mutex entro il tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-926">**TX_NOT_AVAILABLE** (0x1D) Service was unable to get ownership of the mutex within the specified time to wait.</span></span>
- <span data-ttu-id="94e54-927">La sospensione **TX_WAIT_ABORTED** (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="94e54-927">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="94e54-928">**TX_MUTEX_ERROR** (0x1C) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-928">**TX_MUTEX_ERROR** (0x1C) Invalid mutex pointer.</span></span>
- <span data-ttu-id="94e54-929">**TX_WAIT_ERROR** (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-929">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a non-thread.</span></span>
- <span data-ttu-id="94e54-930">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-930">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-931">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-931">Allowed From</span></span>

<span data-ttu-id="94e54-932">Inizializzazione e thread e timer</span><span class="sxs-lookup"><span data-stu-id="94e54-932">Initialization and threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-933">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-933">Preemption Possible</span></span>

<span data-ttu-id="94e54-934">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-934">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-935">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-935">Example</span></span>

```c
TX_MUTEX my_mutex;
UINT status;

/* Obtain exclusive ownership of the mutex "my_mutex".
If the mutex "my_mutex" is not available, suspend until it
becomes available. */
status = tx_mutex_get(&my_mutex, TX_WAIT_FOREVER);
```

### <a name="see-also"></a><span data-ttu-id="94e54-936">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-936">See Also</span></span>

- <span data-ttu-id="94e54-937">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="94e54-937">tx_mutex_create</span></span>
- <span data-ttu-id="94e54-938">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-938">tx_mutex_delete</span></span>
- <span data-ttu-id="94e54-939">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-939">tx_mutex_info_get</span></span>
- <span data-ttu-id="94e54-940">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-940">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="94e54-941">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-941">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-942">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-942">tx_mutex_prioritize</span></span>
- <span data-ttu-id="94e54-943">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="94e54-943">tx_mutex_put</span></span>

## <a name="tx_mutex_info_get"></a><span data-ttu-id="94e54-944">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-944">tx_mutex_info_get</span></span>

<span data-ttu-id="94e54-945">Recuperare informazioni sul mutex</span><span class="sxs-lookup"><span data-stu-id="94e54-945">Retrieve information about mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-946">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-946">Prototype</span></span>

```c
UINT tx_mutex_info_get(
    TX_MUTEX *mutex_ptr, 
    CHAR **name,
    ULONG *count, 
    TX_THREAD **owner,
    TX_THREAD **first_suspended,
    ULONG *suspended_count, 
    TX_MUTEX **next_mutex);
```

### <a name="description"></a><span data-ttu-id="94e54-947">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-947">Description</span></span>

<span data-ttu-id="94e54-948">Questo servizio recupera le informazioni dal mutex specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-948">This service retrieves information from the specified mutex.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-949">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-949">Parameters</span></span>

- <span data-ttu-id="94e54-950">**mutex_ptr** Puntatore al blocco di controllo mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-950">**mutex_ptr** Pointer to mutex control block.</span></span>
- <span data-ttu-id="94e54-951">**nome** Puntatore alla destinazione per il puntatore al nome del mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-951">**name** Pointer to destination for the pointer to the mutex's name.</span></span>
- <span data-ttu-id="94e54-952">**numero** di Puntatore alla destinazione per il numero di proprietà del mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-952">**count** Pointer to destination for the ownership count of the mutex.</span></span>
- <span data-ttu-id="94e54-953">**proprietario** Puntatore alla destinazione per il puntatore del thread proprietario.</span><span class="sxs-lookup"><span data-stu-id="94e54-953">**owner** Pointer to destination for the owning thread's pointer.</span></span>
- <span data-ttu-id="94e54-954">**first_suspended** Puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione del mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-954">**first_suspended** Pointer to destination for the pointer to the thread that is first on the suspension list of this mutex.</span></span>
- <span data-ttu-id="94e54-955">**suspended_count** Puntatore alla destinazione per il numero di thread attualmente sospesi in questo mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-955">**suspended_count** Pointer to destination for the number of threads currently suspended on this mutex.</span></span>
- <span data-ttu-id="94e54-956">**next_mutex** Puntatore alla destinazione per il puntatore del mutex creato successivo.</span><span class="sxs-lookup"><span data-stu-id="94e54-956">**next_mutex** Pointer to destination for the pointer of the next created mutex.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-957">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-957">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-958">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-958">Return Values</span></span>

- <span data-ttu-id="94e54-959">Il recupero delle informazioni mutex riuscite **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-959">**TX_SUCCESS** (0x00) Successful mutex information retrieval.</span></span>
- <span data-ttu-id="94e54-960">**TX_MUTEX_ERROR** (0x1C) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-960">**TX_MUTEX_ERROR** (0x1C) Invalid mutex pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-961">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-961">Allowed From</span></span>

<span data-ttu-id="94e54-962">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-962">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-963">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-963">Preemption Possible</span></span>

<span data-ttu-id="94e54-964">No</span><span class="sxs-lookup"><span data-stu-id="94e54-964">No</span></span>

<span data-ttu-id="94e54-965">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="94e54-965">**Example**</span></span>

```c
TX_MUTEX my_mutex;
CHAR *name;
ULONG count;
TX_THREAD *owner;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_MUTEX *next_mutex;
UINT status;

/* Retrieve information about the previously created
mutex "my_mutex." */
status = tx_mutex_info_get(&my_mutex, &name,
    &count, &owner,
    &first_suspended, &suspended_count,
    &next_mutex);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-966">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-966">See Also</span></span>

- <span data-ttu-id="94e54-967">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="94e54-967">tx_mutex_create</span></span>
- <span data-ttu-id="94e54-968">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-968">tx_mutex_delete</span></span>
- <span data-ttu-id="94e54-969">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="94e54-969">tx_mutex_get</span></span>
- <span data-ttu-id="94e54-970">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-970">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="94e54-971">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-971">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-972">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-972">tx_mutex_prioritize</span></span>
- <span data-ttu-id="94e54-973">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="94e54-973">tx_mutex_put</span></span>

## <a name="tx_mutex_performance_info_get"></a><span data-ttu-id="94e54-974">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-974">tx_mutex_performance_info_get</span></span>

<span data-ttu-id="94e54-975">Ottenere informazioni sulle prestazioni di mutex</span><span class="sxs-lookup"><span data-stu-id="94e54-975">Get mutex performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-976">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-976">Prototype</span></span>

```c
UINT tx_mutex_performance_info_get(
    TX_MUTEX *mutex_ptr, 
    ULONG *puts,
    ULONG *gets, 
    ULONG *suspensions, 
    ULONG *timeouts,
    ULONG *inversions, 
    ULONG *inheritances);
```

### <a name="description"></a><span data-ttu-id="94e54-977">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-977">Description</span></span>

<span data-ttu-id="94e54-978">Questo servizio recupera le informazioni sulle prestazioni relative al mutex specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-978">This service retrieves performance information about the specified mutex.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-979">*La libreria e l'applicazione threadX devono essere compilate con*  \* **TX_MUTEX_ENABLE_PERFORMANCE_INFO** _ _defined per il servizio per restituire informazioni sulle prestazioni. \*</span><span class="sxs-lookup"><span data-stu-id="94e54-979">*The ThreadX library and application must be built with* ***TX_MUTEX_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-980">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-980">Parameters</span></span>

- <span data-ttu-id="94e54-981">**mutex_ptr** Puntatore a mutex creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-981">**mutex_ptr** Pointer to previously created mutex.</span></span>
- <span data-ttu-id="94e54-982">**inserisce** Puntatore alla destinazione per il numero di richieste PUT eseguite sul mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-982">**puts** Pointer to destination for the number of put requests performed on this mutex.</span></span>
- <span data-ttu-id="94e54-983">**ottiene** Puntatore alla destinazione per il numero di richieste Get eseguite sul mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-983">**gets** Pointer to destination for the number of get requests performed on this mutex.</span></span>
- <span data-ttu-id="94e54-984">**sospensioni** Puntatore alla destinazione per il numero delle sospensioni del mutex di thread Get sul mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-984">**suspensions** Pointer to destination for the number of thread mutex get suspensions on this mutex.</span></span>
- <span data-ttu-id="94e54-985">**timeout** Puntatore alla destinazione per il numero di timeout di sospensione del mutex Get sul mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-985">**timeouts** Pointer to destination for the number of mutex get suspension timeouts on this mutex.</span></span>
- <span data-ttu-id="94e54-986">**inversioni** Puntatore alla destinazione per il numero di inversioni di priorità dei thread sul mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-986">**inversions** Pointer to destination for the number of thread priority inversions on this mutex.</span></span>
- <span data-ttu-id="94e54-987">**ereditarietà** Puntatore alla destinazione per il numero di operazioni di ereditarietà della priorità dei thread sul mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-987">**inheritances** Pointer to destination for the number of thread priority inheritance operations on this mutex.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-988">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-988">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-989">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-989">Return Values</span></span>

- <span data-ttu-id="94e54-990">**TX_SUCCESS** (0x00) ottenere prestazioni mutex riuscite.</span><span class="sxs-lookup"><span data-stu-id="94e54-990">**TX_SUCCESS** (0x00) Successful mutex performance get.</span></span>
- <span data-ttu-id="94e54-991">**TX_PTR_ERROR** (0x03) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-991">**TX_PTR_ERROR** (0x03) Invalid mutex pointer.</span></span>
- <span data-ttu-id="94e54-992">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-992">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-993">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-993">Allowed From</span></span>

<span data-ttu-id="94e54-994">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-994">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-995">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-995">Example</span></span>

```c
TX_MUTEX my_mutex;
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;
ULONG inversions;
ULONG inheritances;

/* Retrieve performance information on the previously created
mutex. */
status = tx_mutex_performance_info_get(&my_mutex_ptr, &puts, &gets,
    &suspensions, &timeouts, &inversions, &inheritances);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-996">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-996">See Also</span></span>

- <span data-ttu-id="94e54-997">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="94e54-997">tx_mutex_create</span></span>
- <span data-ttu-id="94e54-998">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-998">tx_mutex_delete</span></span>
- <span data-ttu-id="94e54-999">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="94e54-999">tx_mutex_get</span></span>
- <span data-ttu-id="94e54-1000">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1000">tx_mutex_info_get</span></span>
- <span data-ttu-id="94e54-1001">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1001">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1002">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1002">tx_mutex_prioritize</span></span>
- <span data-ttu-id="94e54-1003">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1003">tx_mutex_put</span></span>

## <a name="tx_mutex_performance_system_info_get"></a><span data-ttu-id="94e54-1004">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1004">tx_mutex_performance_system_info_get</span></span>

<span data-ttu-id="94e54-1005">Ottenere informazioni sulle prestazioni del sistema mutex</span><span class="sxs-lookup"><span data-stu-id="94e54-1005">Get mutex system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1006">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1006">Prototype</span></span>

```c
UINT tx_mutex_performance_system_info_get(
    ULONG *puts, 
    ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts,
    ULONG *inversions, 
    ULONG *inheritances);
```

### <a name="description"></a><span data-ttu-id="94e54-1007">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1007">Description</span></span>

<span data-ttu-id="94e54-1008">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i mutex nel sistema.</span><span class="sxs-lookup"><span data-stu-id="94e54-1008">This service retrieves performance information about all the mutexes in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-1009">Per restituire informazioni sulle prestazioni, *è necessario compilare la libreria threadX e l'applicazione con* **TX_MUTEX_ENABLE_PERFORMANCE_INFO** *definite per questo servizio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1009">*The ThreadX library and application must be built with* **TX_MUTEX_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1010">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1010">Parameters</span></span>

- <span data-ttu-id="94e54-1011">**inserisce** Puntatore alla destinazione per il numero totale di richieste PUT eseguite su tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-1011">**puts** Pointer to destination for the total number of put requests performed on all mutexes.</span></span>
- <span data-ttu-id="94e54-1012">**ottiene** Puntatore alla destinazione per il numero totale di richieste Get eseguite su tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-1012">**gets** Pointer to destination for the total number of get requests performed on all mutexes.</span></span>
- <span data-ttu-id="94e54-1013">**sospensioni** Puntatore alla destinazione per il numero totale delle sospensioni del mutex di thread per tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-1013">**suspensions** Pointer to destination for the total number of thread mutex get suspensions on all mutexes.</span></span>
- <span data-ttu-id="94e54-1014">**timeout** Puntatore alla destinazione per il numero totale di timeout di sospensione del mutex Get su tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-1014">**timeouts** Pointer to destination for the total number of mutex get suspension timeouts on all mutexes.</span></span>
- <span data-ttu-id="94e54-1015">**inversioni** Puntatore alla destinazione per il numero totale di inversioni di priorità dei thread in tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-1015">**inversions** Pointer to destination for the total number of thread priority inversions on all mutexes.</span></span>
- <span data-ttu-id="94e54-1016">**ereditarietà** Puntatore alla destinazione per il numero totale di operazioni di ereditarietà della priorità dei thread su tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-1016">**inheritances** Pointer to destination for the total number of thread priority inheritance operations on all mutexes.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1017">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1017">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1018">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1018">Return Values</span></span>

- <span data-ttu-id="94e54-1019">Le prestazioni del sistema mutex riuscite **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-1019">**TX_SUCCESS** (0x00) Successful mutex system performance get.</span></span>
- <span data-ttu-id="94e54-1020">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-1020">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1021">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1021">Allowed From</span></span>

<span data-ttu-id="94e54-1022">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1022">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1023">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1023">Example</span></span>

```c
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;
ULONG inversions;
ULONG inheritances;

/* Retrieve performance information on all previously created
mutexes. */
status = tx_mutex_performance_system_info_get(&puts, &gets,
    &suspensions, &timeouts,
    &inversions, &inheritances);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1024">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1024">See Also</span></span>

- <span data-ttu-id="94e54-1025">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1025">tx_mutex_create</span></span>
- <span data-ttu-id="94e54-1026">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1026">tx_mutex_delete</span></span>
- <span data-ttu-id="94e54-1027">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1027">tx_mutex_get</span></span>
- <span data-ttu-id="94e54-1028">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1028">tx_mutex_info_get</span></span>
- <span data-ttu-id="94e54-1029">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1029">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="94e54-1030">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1030">tx_mutex_prioritize</span></span>
- <span data-ttu-id="94e54-1031">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1031">tx_mutex_put</span></span>

## <a name="tx_mutex_prioritize"></a><span data-ttu-id="94e54-1032">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1032">tx_mutex_prioritize</span></span>

<span data-ttu-id="94e54-1033">Elencare le sospensioni mutex</span><span class="sxs-lookup"><span data-stu-id="94e54-1033">Prioritize mutex suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1034">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1034">Prototype</span></span>

```c
UINT tx_mutex_prioritize(TX_MUTEX *mutex_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-1035">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1035">Description</span></span>

<span data-ttu-id="94e54-1036">Questo servizio posiziona il thread con priorità più elevata sospeso per la proprietà del mutex all'inizio dell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="94e54-1036">This service places the highest priority thread suspended for ownership of the mutex at the front of the suspension list.</span></span> <span data-ttu-id="94e54-1037">Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.</span><span class="sxs-lookup"><span data-stu-id="94e54-1037">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1038">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1038">Parameters</span></span>

- <span data-ttu-id="94e54-1039">**mutex_ptr** Puntatore al mutex creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1039">**mutex_ptr** Pointer to the previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1040">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1040">Return Values</span></span>

- <span data-ttu-id="94e54-1041">**TX_SUCCESS** (0x00) priorità mutex riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-1041">**TX_SUCCESS** (0x00) Successful mutex prioritize.</span></span>
- <span data-ttu-id="94e54-1042">**TX_MUTEX_ERROR** (0x1C) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1042">**TX_MUTEX_ERROR** (0x1C) Invalid mutex pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1043">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1043">Allowed From</span></span>

<span data-ttu-id="94e54-1044">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1044">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1045">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1045">Preemption Possible</span></span>

<span data-ttu-id="94e54-1046">No</span><span class="sxs-lookup"><span data-stu-id="94e54-1046">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1047">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1047">Example</span></span>

```c
TX_MUTEX my_mutex;
UINT status;

/* Ensure that the highest priority thread will receive
ownership of the mutex when it becomes available. */
status = tx_mutex_prioritize(&my_mutex);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_mutex_put call that releases ownership of the
mutex will give ownership to this thread and wake it
up. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1048">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1048">See Also</span></span>

- <span data-ttu-id="94e54-1049">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1049">tx_mutex_create</span></span>
- <span data-ttu-id="94e54-1050">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1050">tx_mutex_delete</span></span>
- <span data-ttu-id="94e54-1051">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1051">tx_mutex_get</span></span>
- <span data-ttu-id="94e54-1052">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1052">tx_mutex_info_get</span></span>
- <span data-ttu-id="94e54-1053">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1053">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="94e54-1054">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1054">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1055">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1055">tx_mutex_put</span></span>

## <a name="tx_mutex_put"></a><span data-ttu-id="94e54-1056">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1056">tx_mutex_put</span></span>

<span data-ttu-id="94e54-1057">Rilascia la proprietà di mutex</span><span class="sxs-lookup"><span data-stu-id="94e54-1057">Release ownership of mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1058">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1058">Prototype</span></span>

```c
UINT tx_mutex_put(TX_MUTEX *mutex_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-1059">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1059">Description</span></span>

<span data-ttu-id="94e54-1060">Questo servizio decrementa il numero di proprietà del mutex specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1060">This service decrements the ownership count of the specified mutex.</span></span> <span data-ttu-id="94e54-1061">Se il conteggio proprietà è pari a zero, il mutex viene reso disponibile.</span><span class="sxs-lookup"><span data-stu-id="94e54-1061">If the ownership count is zero, the mutex is made available.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1062">*Se durante la creazione del mutex è stata selezionata l'ereditarietà prioritaria, la priorità del thread di rilascio verrà ripristinata con la priorità che aveva quando era stata originariamente ottenuta la proprietà del mutex. Eventuali altre modifiche di priorità apportate al thread di rilascio durante la proprietà del mutex possono essere annullate.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1062">*If priority inheritance was selected during mutex creation, the priority of the releasing thread will be restored to the priority it had when it originally obtained ownership of the mutex. Any other priority changes made to the releasing thread during ownership of the mutex may be undone.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1063">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1063">Parameters</span></span>
- <span data-ttu-id="94e54-1064">mutex_ptr puntatore al mutex creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1064">mutex_ptr Pointer to the previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1065">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1065">Return Values</span></span>
- <span data-ttu-id="94e54-1066">**TX_SUCCESS** (0x00) versione mutex riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-1066">**TX_SUCCESS** (0x00) Successful mutex release.</span></span>
- <span data-ttu-id="94e54-1067">Il mutex **TX_NOT_OWNED** (0x1E) non è di proprietà del chiamante.</span><span class="sxs-lookup"><span data-stu-id="94e54-1067">**TX_NOT_OWNED** (0x1E) Mutex is not owned by caller.</span></span>
- <span data-ttu-id="94e54-1068">**TX_MUTEX_ERROR** (0x1C) puntatore non valido a mutex.</span><span class="sxs-lookup"><span data-stu-id="94e54-1068">**TX_MUTEX_ERROR** (0x1C) Invalid pointer to mutex.</span></span>
- <span data-ttu-id="94e54-1069">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1069">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1070">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1070">Allowed From</span></span>

<span data-ttu-id="94e54-1071">Inizializzazione e thread e timer</span><span class="sxs-lookup"><span data-stu-id="94e54-1071">Initialization and threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1072">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1072">Preemption Possible</span></span>

<span data-ttu-id="94e54-1073">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-1073">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1074">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1074">Example</span></span>

```c
TX_MUTEX my_mutex;
UINT status;

/* Release ownership of "my_mutex." */
status = tx_mutex_put(&my_mutex);

/* If status equals TX_SUCCESS, the mutex ownership
count has been decremented and if zero, released. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1075">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1075">See Also</span></span>

- <span data-ttu-id="94e54-1076">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1076">tx_mutex_create</span></span>
- <span data-ttu-id="94e54-1077">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1077">tx_mutex_delete</span></span>
- <span data-ttu-id="94e54-1078">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1078">tx_mutex_get</span></span>
- <span data-ttu-id="94e54-1079">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1079">tx_mutex_info_get</span></span>
- <span data-ttu-id="94e54-1080">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1080">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="94e54-1081">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1081">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1082">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1082">tx_mutex_prioritize</span></span>

## <a name="tx_queue_create"></a><span data-ttu-id="94e54-1083">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1083">tx_queue_create</span></span>

<span data-ttu-id="94e54-1084">Crea coda messaggi</span><span class="sxs-lookup"><span data-stu-id="94e54-1084">Create message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1085">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1085">Prototype</span></span>

```c
UINT tx_queue_create(
    TX_QUEUE *queue_ptr, 
    CHAR *name_ptr,
    UINT message_size,
    VOID *queue_start, 
    ULONG queue_size);
```

### <a name="description"></a><span data-ttu-id="94e54-1086">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1086">Description</span></span>

<span data-ttu-id="94e54-1087">Questo servizio crea una coda di messaggi che in genere viene utilizzata per la comunicazione tra thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1087">This service creates a message queue that is typically used for interthread communication.</span></span> <span data-ttu-id="94e54-1088">Il numero totale di messaggi viene calcolato dalla dimensione del messaggio specificata e dal numero totale di byte nella coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1088">The total number of messages is calculated from the specified message size and the total number of bytes in the queue.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1089">*Se il numero totale di byte specificato nell'area di memoria della coda non è divisibile in modo uniforme per la dimensione del messaggio specificata, i byte rimanenti nell'area di memoria non vengono utilizzati.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1089">*If the total number of bytes specified in the queue's memory area is not evenly divisible by the specified message size, the remaining bytes in the memory area are not used.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1090">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1090">Parameters</span></span>

- <span data-ttu-id="94e54-1091">**queue_ptr** Puntatore a un blocco di controllo della coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="94e54-1091">**queue_ptr** Pointer to a message queue control block.</span></span>
- <span data-ttu-id="94e54-1092">**name_ptr** Puntatore al nome della coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="94e54-1092">**name_ptr** Pointer to the name of the message queue.</span></span>
- <span data-ttu-id="94e54-1093">**message_size** Specifica le dimensioni di ogni messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1093">**message_size** Specifies the size of each message in the queue.</span></span> <span data-ttu-id="94e54-1094">Le dimensioni dei messaggi variano da Word a 1 32 bit a parole a 16 32 bit.</span><span class="sxs-lookup"><span data-stu-id="94e54-1094">Message sizes range from 1 32-bit word to 16 32-bit words.</span></span> <span data-ttu-id="94e54-1095">Le opzioni valide per le dimensioni dei messaggi sono valori numerici compresi tra 1 e 16.</span><span class="sxs-lookup"><span data-stu-id="94e54-1095">Valid message size options are numerical values from 1 through 16, inclusive.</span></span>
- <span data-ttu-id="94e54-1096">**queue_start** Indirizzo iniziale della coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="94e54-1096">**queue_start** Starting address of the message queue.</span></span> <span data-ttu-id="94e54-1097">L'indirizzo iniziale deve essere allineato alle dimensioni del tipo di dati ULONG.</span><span class="sxs-lookup"><span data-stu-id="94e54-1097">The starting address must be aligned to the size of the ULONG data type.</span></span>
- <span data-ttu-id="94e54-1098">**queue_size** Numero totale di byte disponibili per la coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="94e54-1098">**queue_size** Total number of bytes available for the message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1099">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1099">Return Values</span></span>

- <span data-ttu-id="94e54-1100">Creazione coda messaggi riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-1100">**TX_SUCCESS** (0x00) Successful message queue creation.</span></span>
- <span data-ttu-id="94e54-1101">**TX_QUEUE_ERROR** (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1101">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span> <span data-ttu-id="94e54-1102">Il puntatore è NULL o la coda è già stata creata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1102">Either the pointer is NULL or the queue is already created.</span></span>
- <span data-ttu-id="94e54-1103">**TX_PTR_ERROR** (0x03) indirizzo iniziale non valido della coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="94e54-1103">**TX_PTR_ERROR** (0x03) Invalid starting address of the message queue.</span></span>
- <span data-ttu-id="94e54-1104">Le dimensioni **TX_SIZE_ERROR** (0x05) della coda di messaggi non sono valide.</span><span class="sxs-lookup"><span data-stu-id="94e54-1104">**TX_SIZE_ERROR** (0x05) Size of message queue is invalid.</span></span>
- <span data-ttu-id="94e54-1105">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1105">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1106">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1106">Allowed From</span></span>

<span data-ttu-id="94e54-1107">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="94e54-1107">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1108">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1108">Preemption Possible</span></span>

<span data-ttu-id="94e54-1109">No</span><span class="sxs-lookup"><span data-stu-id="94e54-1109">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1110">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1110">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;

/* Create a message queue whose total size is 2000 bytes
starting at address 0x300000. Each message in this
queue is defined to be 4 32-bit words long. */
status = tx_queue_create(&my_queue, "my_queue_name",
    4, (VOID *) 0x300000, 2000);

/* If status equals TX_SUCCESS, my_queue contains room
for storing 125 messages (2000 bytes/ 16 bytes per
message). */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1111">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1111">See Also</span></span>

- <span data-ttu-id="94e54-1112">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1112">tx_queue_delete</span></span>
- <span data-ttu-id="94e54-1113">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="94e54-1113">tx_queue_flush</span></span>
- <span data-ttu-id="94e54-1114">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1114">tx_queue_front_send</span></span>
- <span data-ttu-id="94e54-1115">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1115">tx_queue_info_get</span></span>
- <span data-ttu-id="94e54-1116">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1116">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="94e54-1117">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1117">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1118">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1118">tx_queue_prioritize</span></span>
- <span data-ttu-id="94e54-1119">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="94e54-1119">tx_queue_receive</span></span>
- <span data-ttu-id="94e54-1120">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1120">tx_queue_send</span></span>
- <span data-ttu-id="94e54-1121">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1121">tx_queue_send_notify</span></span>

## <a name="tx_queue_delete"></a><span data-ttu-id="94e54-1122">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1122">tx_queue_delete</span></span>

<span data-ttu-id="94e54-1123">Elimina coda messaggi</span><span class="sxs-lookup"><span data-stu-id="94e54-1123">Delete message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1124">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1124">Prototype</span></span>

```c
UINT tx_queue_delete(TX_QUEUE *queue_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-1125">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1125">Description</span></span>

<span data-ttu-id="94e54-1126">Questo servizio Elimina la coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1126">This service deletes the specified message queue.</span></span> <span data-ttu-id="94e54-1127">Tutti i thread sospesi in attesa di un messaggio da questa coda vengono ripresi e viene fornito un TX_DELETED stato restituito.</span><span class="sxs-lookup"><span data-stu-id="94e54-1127">All threads suspended waiting for a message from this queue are resumed and given a TX_DELETED return status.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="94e54-1128">*Prima di eliminare la coda, l'applicazione deve assicurarsi che qualsiasi callback di invio notifica per questa coda venga completato (o disabilitato). Inoltre, l'applicazione deve impedire l'uso futuro di una coda eliminata.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1128">*The application must ensure that any send notify callback for this queue is completed (or disabled) before deleting the queue. In addition, the application must prevent any future use of a deleted queue.*</span></span> <br><br><span data-ttu-id="94e54-1129">*È inoltre responsabilità dell'applicazione gestire l'area di memoria associata alla coda, disponibile al termine del servizio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1129">*It is also the application's responsibility to manage the memory area associated with the queue, which is available after this service completes.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1130">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1130">Parameters</span></span>

- <span data-ttu-id="94e54-1131">**queue_ptr** Puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1131">**queue_ptr** Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1132">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1132">Return Values</span></span>

- <span data-ttu-id="94e54-1133">Eliminazione della coda messaggi riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-1133">**TX_SUCCESS** (0x00) Successful message queue deletion.</span></span>
- <span data-ttu-id="94e54-1134">**TX_QUEUE_ERROR** (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1134">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="94e54-1135">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1135">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1136">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1136">Allowed From</span></span>

<span data-ttu-id="94e54-1137">Thread</span><span class="sxs-lookup"><span data-stu-id="94e54-1137">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1138">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1138">Preemption Possible</span></span>

<span data-ttu-id="94e54-1139">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-1139">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1140">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1140">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;

/* Delete entire message queue. Assume that the queue
has already been created with a call to
tx_queue_create. */
status = tx_queue_delete(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
deleted. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1141">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1141">See Also</span></span>

- <span data-ttu-id="94e54-1142">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1142">tx_queue_create</span></span>
- <span data-ttu-id="94e54-1143">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="94e54-1143">tx_queue_flush</span></span>
- <span data-ttu-id="94e54-1144">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1144">tx_queue_front_send</span></span>
- <span data-ttu-id="94e54-1145">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1145">tx_queue_info_get</span></span>
- <span data-ttu-id="94e54-1146">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1146">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="94e54-1147">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1147">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1148">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1148">tx_queue_prioritize</span></span>
- <span data-ttu-id="94e54-1149">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="94e54-1149">tx_queue_receive</span></span>
- <span data-ttu-id="94e54-1150">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1150">tx_queue_send</span></span>
- <span data-ttu-id="94e54-1151">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1151">tx_queue_send_notify</span></span>

## <a name="tx_queue_flush"></a><span data-ttu-id="94e54-1152">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="94e54-1152">tx_queue_flush</span></span>

<span data-ttu-id="94e54-1153">Messaggi vuoti nella coda di messaggi</span><span class="sxs-lookup"><span data-stu-id="94e54-1153">Empty messages in message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1154">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1154">Prototype</span></span>

```c
UINT tx_queue_flush(TX_QUEUE *queue_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-1155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1155">Description</span></span>

<span data-ttu-id="94e54-1156">Questo servizio Elimina tutti i messaggi archiviati nella coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1156">This service deletes all messages stored in the specified message queue.</span></span>

<span data-ttu-id="94e54-1157">Se la coda è piena, i messaggi di tutti i thread sospesi vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="94e54-1157">If the queue is full, messages of all suspended threads are discarded.</span></span> <span data-ttu-id="94e54-1158">Ogni thread sospeso viene quindi ripreso con uno stato restituito che indica che l'invio del messaggio è stato completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="94e54-1158">Each suspended thread is then resumed with a return status that indicates the message send was successful.</span></span> <span data-ttu-id="94e54-1159">Se la coda è vuota, il servizio non esegue alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1159">If the queue is empty, this service does nothing.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1160">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1160">Parameters</span></span>

- <span data-ttu-id="94e54-1161">**queue_ptr** Puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1161">**queue_ptr** Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1162">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1162">Return Values</span></span>

- <span data-ttu-id="94e54-1163">Scaricamento coda messaggi riuscito **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-1163">**TX_SUCCESS** (0x00) Successful message queue flush.</span></span>
- <span data-ttu-id="94e54-1164">**TX_QUEUE_ERROR** (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1164">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1165">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1165">Allowed From</span></span>

<span data-ttu-id="94e54-1166">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1166">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1167">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1167">Preemption Possible</span></span>

<span data-ttu-id="94e54-1168">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-1168">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1169">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1169">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;

/* Flush out all pending messages in the specified message
queue. Assume that the queue has already been created
with a call to tx_queue_create. */
status = tx_queue_flush(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
empty. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1170">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1170">See Also</span></span>

- <span data-ttu-id="94e54-1171">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1171">tx_queue_create</span></span>
- <span data-ttu-id="94e54-1172">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1172">tx_queue_delete</span></span>
- <span data-ttu-id="94e54-1173">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1173">tx_queue_front_send</span></span>
- <span data-ttu-id="94e54-1174">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1174">tx_queue_info_get</span></span>
- <span data-ttu-id="94e54-1175">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1175">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="94e54-1176">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1176">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1177">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1177">tx_queue_prioritize</span></span>
- <span data-ttu-id="94e54-1178">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="94e54-1178">tx_queue_receive</span></span>
- <span data-ttu-id="94e54-1179">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1179">tx_queue_send</span></span>
- <span data-ttu-id="94e54-1180">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1180">tx_queue_send_notify</span></span>

## <a name="tx_queue_front_send"></a><span data-ttu-id="94e54-1181">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1181">tx_queue_front_send</span></span>

<span data-ttu-id="94e54-1182">Invia messaggio all'inizio della coda</span><span class="sxs-lookup"><span data-stu-id="94e54-1182">Send message to the front of queue</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1183">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1183">Prototype</span></span>

```c
UINT tx_queue_front_send(
    TX_QUEUE *queue_ptr,
    VOID *source_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="94e54-1184">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1184">Description</span></span>

<span data-ttu-id="94e54-1185">Questo servizio invia un messaggio al percorso front della coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1185">This service sends a message to the front location of the specified message queue.</span></span> <span data-ttu-id="94e54-1186">Il messaggio viene **copiato** all'inizio della coda dall'area di memoria specificata dal puntatore di origine.</span><span class="sxs-lookup"><span data-stu-id="94e54-1186">The message is **copied** to the front of the queue from the memory area specified by the source pointer.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1187">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1187">Parameters</span></span>

- <span data-ttu-id="94e54-1188">**queue_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-1188">**queue_ptr**</span></span> <br><span data-ttu-id="94e54-1189">Puntatore a un blocco di controllo della coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="94e54-1189">Pointer to a message queue control block.</span></span>
- <span data-ttu-id="94e54-1190">**source_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-1190">**source_ptr**</span></span> <br><span data-ttu-id="94e54-1191">Puntatore al messaggio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1191">Pointer to the message.</span></span>
- <span data-ttu-id="94e54-1192">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="94e54-1192">**wait_option**</span></span>  <br><span data-ttu-id="94e54-1193">Definisce il comportamento del servizio se la coda di messaggi è piena.</span><span class="sxs-lookup"><span data-stu-id="94e54-1193">Defines how the service behaves if the message queue is full.</span></span> <span data-ttu-id="94e54-1194">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="94e54-1194">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="94e54-1195">**TX_NO_WAIT** (0x00000000): la selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1195">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="94e54-1196">*Questa è l'unica opzione valida se il servizio viene chiamato da un non thread. ad esempio, inizializzazione, timer o ISR.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1196">*This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.*</span></span>
  - <span data-ttu-id="94e54-1197">**TX_WAIT_FOREVER** (0xFFFFFFFF): se si seleziona TX_WAIT_FOREVER si fa in modo che il thread chiamante venga sospeso per un tempo illimitato fino a quando non è disponibile spazio nella coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1197">**TX_WAIT_FOREVER** (0xFFFFFFFF) - Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until there is room in the queue.</span></span>
  - <span data-ttu-id="94e54-1198">valore di timeout (0x00000001 tramite 0xFFFFFFFE)-la selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi in attesa di spazio nella coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1198">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for room in the queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1199">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1199">Return Values</span></span>

- <span data-ttu-id="94e54-1200">**TX_SUCCESS** (0x00) invio del messaggio riuscito.</span><span class="sxs-lookup"><span data-stu-id="94e54-1200">**TX_SUCCESS** (0x00) Successful sending of message.</span></span>
- <span data-ttu-id="94e54-1201">La coda di messaggi **TX_DELETED** (0x01) è stata eliminata durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1201">**TX_DELETED** (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="94e54-1202">Il servizio **TX_QUEUE_FULL** (0x0B) non è riuscito a inviare il messaggio perché la coda era piena per la durata del tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1202">**TX_QUEUE_FULL** (0x0B) Service was unable to send message because the queue was full for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="94e54-1203">La sospensione **TX_WAIT_ABORTED** (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="94e54-1203">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="94e54-1204">**TX_QUEUE_ERROR** (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1204">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="94e54-1205">**TX_PTR_ERROR** (0x03) puntatore di origine non valido per il messaggio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1205">**TX_PTR_ERROR** (0x03) Invalid source pointer for message.</span></span>
- <span data-ttu-id="94e54-1206">**TX_WAIT_ERROR** (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1206">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a non-thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1207">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1207">Allowed From</span></span>

<span data-ttu-id="94e54-1208">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1208">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1209">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1209">Preemption Possible</span></span>

<span data-ttu-id="94e54-1210">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-1210">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1211">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1211">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Send a message to the front of "my_queue." Return
immediately, regardless of success. This wait
option is used for calls from initialization, timers,
and ISRs. */
status = tx_queue_front_send(&my_queue, my_message,
    TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is at the front
of the specified queue. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1212">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1212">See Also</span></span>

- <span data-ttu-id="94e54-1213">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1213">tx_queue_create</span></span>
- <span data-ttu-id="94e54-1214">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1214">tx_queue_delete</span></span>
- <span data-ttu-id="94e54-1215">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="94e54-1215">tx_queue_flush</span></span>
- <span data-ttu-id="94e54-1216">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1216">tx_queue_info_get</span></span>
- <span data-ttu-id="94e54-1217">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1217">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="94e54-1218">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1218">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1219">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1219">tx_queue_prioritize</span></span>
- <span data-ttu-id="94e54-1220">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="94e54-1220">tx_queue_receive</span></span>
- <span data-ttu-id="94e54-1221">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1221">tx_queue_send</span></span>
- <span data-ttu-id="94e54-1222">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1222">tx_queue_send_notify</span></span>

## <a name="tx_queue_info_get"></a><span data-ttu-id="94e54-1223">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1223">tx_queue_info_get</span></span>

<span data-ttu-id="94e54-1224">Recuperare le informazioni sulla coda</span><span class="sxs-lookup"><span data-stu-id="94e54-1224">Retrieve information about queue</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1225">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1225">Prototype</span></span>

```c
UINT tx_queue_info_get(
    TX_QUEUE *queue_ptr, 
    CHAR **name,
    ULONG *enqueued, 
    ULONG *available_storage
    TX_THREAD **first_suspended, 
    ULONG *suspended_count,
    TX_QUEUE **next_queue);
```

### <a name="description"></a><span data-ttu-id="94e54-1226">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1226">Description</span></span>

<span data-ttu-id="94e54-1227">Questo servizio recupera le informazioni sulla coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1227">This service retrieves information about the specified message queue.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1228">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1228">Parameters</span></span>

- <span data-ttu-id="94e54-1229">**queue_ptr** Puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1229">**queue_ptr** Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="94e54-1230">**nome** Puntatore alla destinazione per il puntatore al nome della coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1230">**name** Pointer to destination for the pointer to the queue's name.</span></span>
- <span data-ttu-id="94e54-1231">**accodato** Puntatore alla destinazione per il numero di messaggi attualmente presenti nella coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1231">**enqueued** Pointer to destination for the number of messages currently in the queue.</span></span>
- <span data-ttu-id="94e54-1232">**available_storage** Puntatore alla destinazione per il numero di messaggi per i quali la coda ha attualmente spazio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1232">**available_storage** Pointer to destination for the number of messages the queue currently has space for.</span></span>
- <span data-ttu-id="94e54-1233">**first_suspended** Puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione della coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1233">**first_suspended** Pointer to destination for the pointer to the thread that is first on the suspension list of this queue.</span></span>
- <span data-ttu-id="94e54-1234">**suspended_count** Puntatore alla destinazione per il numero di thread attualmente sospesi in questa coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1234">**suspended_count** Pointer to destination for the number of threads currently suspended on this queue.</span></span>
- <span data-ttu-id="94e54-1235">**next_queue** Puntatore alla destinazione per il puntatore della coda creata successiva.</span><span class="sxs-lookup"><span data-stu-id="94e54-1235">**next_queue** Pointer to destination for the pointer of the next created queue.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1236">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1236">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1237">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1237">Return Values</span></span>

- <span data-ttu-id="94e54-1238">**TX_SUCCESS** (0x00) informazioni della coda riuscite Get.</span><span class="sxs-lookup"><span data-stu-id="94e54-1238">**TX_SUCCESS** (0x00) Successful queue information get.</span></span>
- <span data-ttu-id="94e54-1239">**TX_QUEUE_ERROR** (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1239">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1240">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1240">Allowed From</span></span>

<span data-ttu-id="94e54-1241">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1241">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1242">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1242">Preemption Possible</span></span>

<span data-ttu-id="94e54-1243">No</span><span class="sxs-lookup"><span data-stu-id="94e54-1243">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1244">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1244">Example</span></span>

```c
TX_QUEUE my_queue;
CHAR *name;
ULONG enqueued;
ULONG available_storage;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_QUEUE *next_queue;
UINT status;

/* Retrieve information about the previously created
message queue "my_queue." */
status = tx_queue_info_get(&my_queue, &name,
    &enqueued, &available_storage,
    &first_suspended, &suspended_count,
    &next_queue);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1245">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1245">See Also</span></span>

- <span data-ttu-id="94e54-1246">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1246">tx_queue_create</span></span>
- <span data-ttu-id="94e54-1247">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1247">tx_queue_delete</span></span>
- <span data-ttu-id="94e54-1248">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="94e54-1248">tx_queue_flush</span></span>
- <span data-ttu-id="94e54-1249">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1249">tx_queue_front_send</span></span>
- <span data-ttu-id="94e54-1250">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1250">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="94e54-1251">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1251">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1252">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1252">tx_queue_prioritize</span></span>
- <span data-ttu-id="94e54-1253">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="94e54-1253">tx_queue_receive</span></span>
- <span data-ttu-id="94e54-1254">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1254">tx_queue_send</span></span>
- <span data-ttu-id="94e54-1255">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1255">tx_queue_send_notify</span></span>

## <a name="tx_queue_performance_info_get"></a><span data-ttu-id="94e54-1256">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1256">tx_queue_performance_info_get</span></span>

<span data-ttu-id="94e54-1257">Ottenere le informazioni sulle prestazioni della coda</span><span class="sxs-lookup"><span data-stu-id="94e54-1257">Get queue performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1258">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1258">Prototype</span></span>

```c
UINT tx_queue_performance_info_get(
    TX_QUEUE *queue_ptr,
    ULONG *messages_sent, 
    ULONG *messages_received,
    ULONG *empty_suspensions, 
    ULONG *full_suspensions,
    ULONG *full_errors, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="94e54-1259">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1259">Description</span></span>

<span data-ttu-id="94e54-1260">Questo servizio recupera le informazioni sulle prestazioni relative alla coda specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1260">This service retrieves performance information about the specified queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-1261">*La libreria e l'applicazione threadX devono essere compilate con*  \* **TX_QUEUE_ENABLE_PERFORMANCE_INFO** _ _defined per il servizio per restituire informazioni sulle prestazioni. \*</span><span class="sxs-lookup"><span data-stu-id="94e54-1261">*The ThreadX library and application must be built with* ***TX_QUEUE_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1262">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1262">Parameters</span></span>

- <span data-ttu-id="94e54-1263">**queue_ptr** Puntatore alla coda creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1263">**queue_ptr** Pointer to previously created queue.</span></span>
- <span data-ttu-id="94e54-1264">**messages_sent** Puntatore alla destinazione per il numero di richieste di invio eseguite su questa coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1264">**messages_sent** Pointer to destination for the number of send requests performed on this queue.</span></span>
- <span data-ttu-id="94e54-1265">**messages_received** Puntatore alla destinazione per il numero di richieste di ricezione eseguite in questa coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1265">**messages_received** Pointer to destination for the number of receive requests performed on this queue.</span></span>
- <span data-ttu-id="94e54-1266">**empty_suspensions** Puntatore alla destinazione per il numero di sospensioni vuote della coda in questa coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1266">**empty_suspensions** Pointer to destination for the number of queue empty suspensions on this queue.</span></span>
- <span data-ttu-id="94e54-1267">**full_suspensions** Puntatore alla destinazione per il numero di sospensioni complete della coda in questa coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1267">**full_suspensions** Pointer to destination for the number of queue full suspensions on this queue.</span></span>
- <span data-ttu-id="94e54-1268">**full_errors** Puntatore alla destinazione per il numero di errori della coda completa in questa coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1268">**full_errors** Pointer to destination for the number of queue full errors on this queue.</span></span>
- <span data-ttu-id="94e54-1269">**timeout** Puntatore alla destinazione per il numero di timeout di sospensione del thread in questa coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1269">**timeouts** Pointer to destination for the number of thread suspension timeouts on this queue.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1270">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1270">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1271">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1271">Return Values</span></span>

- <span data-ttu-id="94e54-1272">**TX_SUCCESS** (0x00) ottenere le prestazioni della coda riuscite.</span><span class="sxs-lookup"><span data-stu-id="94e54-1272">**TX_SUCCESS** (0x00) Successful queue performance get.</span></span>
- <span data-ttu-id="94e54-1273">Il puntatore della coda **TX_PTR_ERROR** (0X03) non è valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1273">**TX_PTR_ERROR** (0x03) Invalid queue pointer.</span></span>
- <span data-ttu-id="94e54-1274">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-1274">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1275">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1275">Allowed From</span></span>

<span data-ttu-id="94e54-1276">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1276">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1277">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1277">Example</span></span>

```c
TX_QUEUE my_queue;
ULONG messages_sent;
ULONG messages_received;
ULONG empty_suspensions;
ULONG full_suspensions;
ULONG full_errors;
ULONG timeouts;

/* Retrieve performance information on the previously created
queue. */
status = tx_queue_performance_info_get(&my_queue, &messages_sent,
    &messages_received, &empty_suspensions,
    &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1278">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1278">See Also</span></span>

- <span data-ttu-id="94e54-1279">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1279">tx_queue_create</span></span>
- <span data-ttu-id="94e54-1280">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1280">tx_queue_delete</span></span>
- <span data-ttu-id="94e54-1281">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="94e54-1281">tx_queue_flush</span></span>
- <span data-ttu-id="94e54-1282">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1282">tx_queue_front_send</span></span>
- <span data-ttu-id="94e54-1283">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1283">tx_queue_info_get</span></span>
- <span data-ttu-id="94e54-1284">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1284">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1285">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1285">tx_queue_prioritize</span></span>
- <span data-ttu-id="94e54-1286">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="94e54-1286">tx_queue_receive</span></span>
- <span data-ttu-id="94e54-1287">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1287">tx_queue_send</span></span>
- <span data-ttu-id="94e54-1288">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1288">tx_queue_send_notify</span></span>

## <a name="tx_queue_performance_system_info_get"></a><span data-ttu-id="94e54-1289">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1289">tx_queue_performance_system_info_get</span></span>

<span data-ttu-id="94e54-1290">Ottenere informazioni sulle prestazioni del sistema di Accodamento</span><span class="sxs-lookup"><span data-stu-id="94e54-1290">Get queue system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1291">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1291">Prototype</span></span>

```c
UINT tx_queue_performance_system_info_get(
    ULONG *messages_sent,
    ULONG *messages_received, 
    ULONG *empty_suspensions,
    ULONG *full_suspensions, 
    ULONG *full_errors,
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="94e54-1292">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1292">Description</span></span>

<span data-ttu-id="94e54-1293">Questo servizio recupera le informazioni sulle prestazioni relative a tutte le code nel sistema.</span><span class="sxs-lookup"><span data-stu-id="94e54-1293">This service retrieves performance information about all the queues in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-1294">*La libreria e l'applicazione threadX devono essere compilate con*  \* **TX_QUEUE_ENABLE_PERFORMANCE_INFO** _ _defined per il servizio per restituire informazioni sulle prestazioni. \*</span><span class="sxs-lookup"><span data-stu-id="94e54-1294">*The ThreadX library and application must be built with* ***TX_QUEUE_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1295">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1295">Parameters</span></span>

- <span data-ttu-id="94e54-1296">**messages_sent** Puntatore alla destinazione per il numero totale di richieste di invio eseguite su tutte le code.</span><span class="sxs-lookup"><span data-stu-id="94e54-1296">**messages_sent** Pointer to destination for the total number of send requests performed on all queues.</span></span>
- <span data-ttu-id="94e54-1297">**messages_received** Puntatore alla destinazione per il numero totale di richieste di ricezione eseguite su tutte le code.</span><span class="sxs-lookup"><span data-stu-id="94e54-1297">**messages_received** Pointer to destination for the total number of receive requests performed on all queues.</span></span>
- <span data-ttu-id="94e54-1298">**empty_suspensions** Puntatore alla destinazione per il numero totale di sospensioni vuote in coda in tutte le code.</span><span class="sxs-lookup"><span data-stu-id="94e54-1298">**empty_suspensions** Pointer to destination for the total number of queue empty suspensions on all queues.</span></span>
- <span data-ttu-id="94e54-1299">**full_suspensions** Puntatore alla destinazione per il numero totale di sospensioni complete della coda su tutte le code.</span><span class="sxs-lookup"><span data-stu-id="94e54-1299">**full_suspensions** Pointer to destination for the total number of queue full suspensions on all queues.</span></span>
- <span data-ttu-id="94e54-1300">**full_errors** Puntatore alla destinazione per il numero totale di errori della coda completa su tutte le code.</span><span class="sxs-lookup"><span data-stu-id="94e54-1300">**full_errors** Pointer to destination for the total number of queue full errors on all queues.</span></span>
- <span data-ttu-id="94e54-1301">**timeout** Puntatore alla destinazione per il numero totale di timeout di sospensione del thread in tutte le code.</span><span class="sxs-lookup"><span data-stu-id="94e54-1301">**timeouts** Pointer to destination for the total number of thread suspension timeouts on all queues.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1302">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1302">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

<span data-ttu-id="94e54-1303">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="94e54-1303">**Return Values**</span></span>

- <span data-ttu-id="94e54-1304">**TX_SUCCESS** (0x00) ottenere prestazioni del sistema di Accodamento riuscite.</span><span class="sxs-lookup"><span data-stu-id="94e54-1304">**TX_SUCCESS** (0x00) Successful queue system performance get.</span></span>
- <span data-ttu-id="94e54-1305">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-1305">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1306">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1306">Allowed From</span></span>

<span data-ttu-id="94e54-1307">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1307">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1308">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1308">Example</span></span>

```c
ULONG messages_sent;
ULONG messages_received;
ULONG empty_suspensions;
ULONG full_suspensions;
ULONG full_errors;
ULONG timeouts;

/* Retrieve performance information on all previously created
queues. */
status = tx_queue_performance_system_info_get(&messages_sent,
    &messages_received, &empty_suspensions,
    &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1309">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1309">See Also</span></span>

- <span data-ttu-id="94e54-1310">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1310">tx_queue_create</span></span>
- <span data-ttu-id="94e54-1311">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1311">tx_queue_delete</span></span>
- <span data-ttu-id="94e54-1312">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="94e54-1312">tx_queue_flush</span></span>
- <span data-ttu-id="94e54-1313">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1313">tx_queue_front_send</span></span>
- <span data-ttu-id="94e54-1314">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1314">tx_queue_info_get</span></span>
- <span data-ttu-id="94e54-1315">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1315">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="94e54-1316">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1316">tx_queue_prioritize</span></span>
- <span data-ttu-id="94e54-1317">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="94e54-1317">tx_queue_receive</span></span>
- <span data-ttu-id="94e54-1318">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1318">tx_queue_send</span></span>
- <span data-ttu-id="94e54-1319">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1319">tx_queue_send_notify</span></span>

## <a name="tx_queue_prioritize"></a><span data-ttu-id="94e54-1320">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1320">tx_queue_prioritize</span></span>

<span data-ttu-id="94e54-1321">Elencare le priorità di sospensione della coda</span><span class="sxs-lookup"><span data-stu-id="94e54-1321">Prioritize queue suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1322">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1322">Prototype</span></span>

```c
UINT tx_queue_prioritize(TX_QUEUE *queue_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-1323">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1323">Description</span></span>

<span data-ttu-id="94e54-1324">Questo servizio posiziona il thread con priorità più elevata sospeso per un messaggio o per inserire un messaggio in questa coda all'inizio dell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="94e54-1324">This service places the highest priority thread suspended for a message (or to place a message) on this queue at the front of the suspension list.</span></span>

<span data-ttu-id="94e54-1325">Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.</span><span class="sxs-lookup"><span data-stu-id="94e54-1325">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1326">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1326">Parameters</span></span>

- <span data-ttu-id="94e54-1327">**queue_ptr** Puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1327">**queue_ptr** Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1328">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1328">Return Values</span></span>

- <span data-ttu-id="94e54-1329">**TX_SUCCESS** (0x00) priorità della coda riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-1329">**TX_SUCCESS** (0x00) Successful queue prioritize.</span></span>
- <span data-ttu-id="94e54-1330">**TX_QUEUE_ERROR** (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1330">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1331">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1331">Allowed From</span></span>

<span data-ttu-id="94e54-1332">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1332">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1333">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1333">Preemption Possible</span></span>

<span data-ttu-id="94e54-1334">No</span><span class="sxs-lookup"><span data-stu-id="94e54-1334">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1335">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1335">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;

/* Ensure that the highest priority thread will receive
the next message placed on this queue. */
status = tx_queue_prioritize(&my_queue);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_queue_send or tx_queue_front_send call made
to this queue will wake up this thread. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1336">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1336">See Also</span></span>

- <span data-ttu-id="94e54-1337">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1337">tx_queue_create</span></span>
- <span data-ttu-id="94e54-1338">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1338">tx_queue_delete</span></span>
- <span data-ttu-id="94e54-1339">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="94e54-1339">tx_queue_flush</span></span>
- <span data-ttu-id="94e54-1340">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1340">tx_queue_front_send</span></span>
- <span data-ttu-id="94e54-1341">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1341">tx_queue_info_get</span></span>
- <span data-ttu-id="94e54-1342">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1342">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="94e54-1343">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1343">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1344">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="94e54-1344">tx_queue_receive</span></span>
- <span data-ttu-id="94e54-1345">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1345">tx_queue_send</span></span>
- <span data-ttu-id="94e54-1346">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1346">tx_queue_send_notify</span></span>

## <a name="tx_queue_receive"></a><span data-ttu-id="94e54-1347">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="94e54-1347">tx_queue_receive</span></span>

<span data-ttu-id="94e54-1348">Ottieni messaggio da coda messaggi</span><span class="sxs-lookup"><span data-stu-id="94e54-1348">Get message from message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1349">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1349">Prototype</span></span>

```c
UINT tx_queue_receive(
    TX_QUEUE *queue_ptr,
    VOID *destination_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="94e54-1350">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1350">Description</span></span>

<span data-ttu-id="94e54-1351">Questo servizio recupera un messaggio dalla coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1351">This service retrieves a message from the specified message queue.</span></span> <span data-ttu-id="94e54-1352">Il messaggio recuperato viene **copiato** dalla coda nell'area di memoria specificata dal puntatore di destinazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1352">The retrieved message is **copied** from the queue into the memory area specified by the destination pointer.</span></span> <span data-ttu-id="94e54-1353">Il messaggio viene quindi rimosso dalla coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1353">That message is then removed from the queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-1354">*L'area di memoria di destinazione specificata deve essere sufficientemente grande da contenere il messaggio, ovvero la destinazione del messaggio a cui punta*  \* **destination_ptr** _ _must essere pari almeno alle dimensioni del messaggio per la coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1354">*The specified destination memory area must be large enough to hold the message; i.e., the message destination pointed to by* \***destination_ptr** _ _must be at least as large as the message size for this queue.</span></span> <span data-ttu-id="94e54-1355">In caso contrario, se la destinazione non è sufficientemente grande, si verifica un danneggiamento della memoria nell'area di memoria seguente. \*</span><span class="sxs-lookup"><span data-stu-id="94e54-1355">Otherwise, if the destination is not large enough, memory corruption occurs in the following memory area.\*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1356">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1356">Parameters</span></span>

- <span data-ttu-id="94e54-1357">**queue_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-1357">**queue_ptr**</span></span> <br><span data-ttu-id="94e54-1358">Puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1358">Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="94e54-1359">**destination_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-1359">**destination_ptr**</span></span> <br><span data-ttu-id="94e54-1360">Percorso in cui copiare il messaggio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1360">Location of where to copy the message.</span></span>
- <span data-ttu-id="94e54-1361">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="94e54-1361">**wait_option**</span></span> <br><span data-ttu-id="94e54-1362">Definisce il comportamento del servizio se la coda di messaggi è vuota.</span><span class="sxs-lookup"><span data-stu-id="94e54-1362">Defines how the service behaves if the message queue is empty.</span></span> <span data-ttu-id="94e54-1363">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="94e54-1363">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="94e54-1364">**TX_NO_WAIT** (0x00000000): la selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1364">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="94e54-1365">Questa è l'unica opzione valida se il servizio viene chiamato da un non thread. ad esempio, inizializzazione, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="94e54-1365">This is the only valid option if the service is called from a non-thread; e.g.,  Initialization, timer, or ISR.</span></span>
  - <span data-ttu-id="94e54-1366">**TX_WAIT_FOREVER** (0xFFFFFFFF): se si seleziona TX_WAIT_FOREVER, il thread chiamante sospenderà per un periodo illimitato fino a quando non sarà disponibile un messaggio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1366">**TX_WAIT_FOREVER** (0xFFFFFFFF) - Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a message is available.</span></span>
  - <span data-ttu-id="94e54-1367">valore di timeout (0x00000001 tramite 0xFFFFFFFE)-la selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1367">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a message.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1368">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1368">Return Values</span></span>

- <span data-ttu-id="94e54-1369">**TX_SUCCESS** (0x00) il recupero del messaggio è riuscito.</span><span class="sxs-lookup"><span data-stu-id="94e54-1369">**TX_SUCCESS** (0x00) Successful retrieval of message.</span></span>
- <span data-ttu-id="94e54-1370">La coda di messaggi **TX_DELETED** (0x01) è stata eliminata durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1370">**TX_DELETED** (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="94e54-1371">Il servizio **TX_QUEUE_EMPTY** (0x0A) non è stato in grado di recuperare un messaggio perché la coda è vuota per la durata del tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1371">**TX_QUEUE_EMPTY** (0x0A) Service was unable to retrieve a message because the queue was empty for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="94e54-1372">La sospensione **TX_WAIT_ABORTED** (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="94e54-1372">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="94e54-1373">**TX_QUEUE_ERROR** (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1373">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="94e54-1374">**TX_PTR_ERROR** (0x03) puntatore di destinazione non valido per il messaggio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1374">**TX_PTR_ERROR** (0x03) Invalid destination pointer for message.</span></span>
- <span data-ttu-id="94e54-1375">**TX_WAIT_ERROR** (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1375">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1376">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1376">Allowed From</span></span>

<span data-ttu-id="94e54-1377">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1377">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1378">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1378">Preemption Possible</span></span>

<span data-ttu-id="94e54-1379">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-1379">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1380">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1380">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Retrieve a message from "my_queue." If the queue is
empty, suspend until a message is present. Note that
this suspension is only possible from application
threads. */
status = tx_queue_receive(&my_queue, my_message,
    TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the message is in
"my_message." */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1381">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1381">See Also</span></span>

- <span data-ttu-id="94e54-1382">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1382">tx_queue_create</span></span>
- <span data-ttu-id="94e54-1383">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1383">tx_queue_delete</span></span>
- <span data-ttu-id="94e54-1384">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="94e54-1384">tx_queue_flush</span></span>
- <span data-ttu-id="94e54-1385">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1385">tx_queue_front_send</span></span>
- <span data-ttu-id="94e54-1386">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1386">tx_queue_info_get</span></span>
- <span data-ttu-id="94e54-1387">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1387">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="94e54-1388">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1388">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1389">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1389">tx_queue_prioritize</span></span>
- <span data-ttu-id="94e54-1390">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1390">tx_queue_send</span></span>
- <span data-ttu-id="94e54-1391">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1391">tx_queue_send_notify</span></span>

## <a name="tx_queue_send"></a><span data-ttu-id="94e54-1392">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1392">tx_queue_send</span></span>

<span data-ttu-id="94e54-1393">Invia messaggio alla coda di messaggi</span><span class="sxs-lookup"><span data-stu-id="94e54-1393">Send message to message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1394">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1394">Prototype</span></span>

```c
UINT tx_queue_send(
    TX_QUEUE *queue_ptr,
    VOID *source_ptr, 
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="94e54-1395">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1395">Description</span></span>

<span data-ttu-id="94e54-1396">Questo servizio invia un messaggio alla coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1396">This service sends a message to the specified message queue.</span></span> <span data-ttu-id="94e54-1397">Il messaggio inviato viene **copiato** nella coda dall'area di memoria specificata dal puntatore di origine.</span><span class="sxs-lookup"><span data-stu-id="94e54-1397">The sent message is **copied** to the queue from the memory area specified by the source pointer.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1398">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1398">Parameters</span></span>
- <span data-ttu-id="94e54-1399">**queue_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-1399">**queue_ptr**</span></span> <br><span data-ttu-id="94e54-1400">Puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1400">Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="94e54-1401">**source_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-1401">**source_ptr**</span></span> <br><span data-ttu-id="94e54-1402">Puntatore al messaggio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1402">Pointer to the message.</span></span>
- <span data-ttu-id="94e54-1403">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="94e54-1403">**wait_option**</span></span> <br><span data-ttu-id="94e54-1404">Definisce il comportamento del servizio se la coda di messaggi è piena.</span><span class="sxs-lookup"><span data-stu-id="94e54-1404">Defines how the service behaves if the message queue is full.</span></span> <span data-ttu-id="94e54-1405">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="94e54-1405">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="94e54-1406">**TX_NO_WAIT** (0x00000000): la selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1406">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="94e54-1407">*Questa è l'unica opzione valida se il servizio viene chiamato da un non thread, ad esempio inizializzazione, timer o ISR*.</span><span class="sxs-lookup"><span data-stu-id="94e54-1407">*This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR*.</span></span>
  - <span data-ttu-id="94e54-1408">**TX_WAIT_FOREVER** (0xFFFFFFFF): se si seleziona TX_WAIT_FOREVER si fa in modo che il thread chiamante venga sospeso per un tempo illimitato fino a quando non è disponibile spazio nella coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1408">**TX_WAIT_FOREVER** (0xFFFFFFFF) - Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until there is room in the queue.</span></span>
  - <span data-ttu-id="94e54-1409">valore di timeout (0x00000001 tramite 0xFFFFFFFE)-la selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi in attesa di spazio nella coda.</span><span class="sxs-lookup"><span data-stu-id="94e54-1409">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for room in the queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1410">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1410">Return Values</span></span>

- <span data-ttu-id="94e54-1411">**TX_SUCCESS** (0x00) invio del messaggio riuscito.</span><span class="sxs-lookup"><span data-stu-id="94e54-1411">**TX_SUCCESS** (0x00) Successful sending of message.</span></span>
- <span data-ttu-id="94e54-1412">La coda di messaggi **TX_DELETED** (0x01) è stata eliminata durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1412">**TX_DELETED** (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="94e54-1413">Il servizio **TX_QUEUE_FULL** (0x0B) non è riuscito a inviare il messaggio perché la coda era piena per la durata del tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1413">**TX_QUEUE_FULL** (0x0B) Service was unable to send message because the queue was full for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="94e54-1414">La sospensione **TX_WAIT_ABORTED** (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="94e54-1414">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="94e54-1415">**TX_QUEUE_ERROR** (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1415">**TX_QUEUE_ERROR** (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="94e54-1416">**TX_PTR_ERROR** (0x03) puntatore di origine non valido per il messaggio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1416">**TX_PTR_ERROR** (0x03) Invalid source pointer for message.</span></span>
- <span data-ttu-id="94e54-1417">**TX_WAIT_ERROR** (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1417">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1418">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1418">Allowed From</span></span>

<span data-ttu-id="94e54-1419">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1419">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1420">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1420">Preemption Possible</span></span>

<span data-ttu-id="94e54-1421">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-1421">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1422">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1422">Example</span></span>

```c
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Send a message to "my_queue." Return immediately,
regardless of success. This wait option is used for
calls from initialization, timers, and ISRs. */
status = tx_queue_send(&my_queue, my_message, TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is in the
queue. */
```

<span data-ttu-id="94e54-1423">**Vedere anche**</span><span class="sxs-lookup"><span data-stu-id="94e54-1423">**See Also**</span></span>

- <span data-ttu-id="94e54-1424">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1424">tx_queue_create</span></span>
- <span data-ttu-id="94e54-1425">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1425">tx_queue_delete</span></span>
- <span data-ttu-id="94e54-1426">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="94e54-1426">tx_queue_flush</span></span>
- <span data-ttu-id="94e54-1427">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1427">tx_queue_front_send</span></span>
- <span data-ttu-id="94e54-1428">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1428">tx_queue_info_get</span></span>
- <span data-ttu-id="94e54-1429">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1429">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="94e54-1430">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1430">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1431">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1431">tx_queue_prioritize</span></span>
- <span data-ttu-id="94e54-1432">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="94e54-1432">tx_queue_receive</span></span>
- <span data-ttu-id="94e54-1433">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1433">tx_queue_send_notify</span></span>

## <a name="tx_queue_send_notify"></a><span data-ttu-id="94e54-1434">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1434">tx_queue_send_notify</span></span>

<span data-ttu-id="94e54-1435">Invia notifica all'applicazione quando il messaggio viene inviato alla coda</span><span class="sxs-lookup"><span data-stu-id="94e54-1435">Notify application when message is sent to queue</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1436">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1436">Prototype</span></span>

```c
UINT tx_queue_send_notify(
    TX_QUEUE *queue_ptr,
    VOID (*queue_send_notify)(TX_QUEUE *));
```

### <a name="description"></a><span data-ttu-id="94e54-1437">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1437">Description</span></span>

<span data-ttu-id="94e54-1438">Questo servizio registra una funzione di callback delle notifiche chiamata ogni volta che un messaggio viene inviato alla coda specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1438">This service registers a notification callback function that is called whenever a message is sent to the specified queue.</span></span> <span data-ttu-id="94e54-1439">L'elaborazione del callback di notifica viene definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1439">The processing of the notification callback is defined by the application.</span></span>

>[!NOTE]
> <span data-ttu-id="94e54-1440">*Il callback di notifica di invio della coda dell'applicazione non è autorizzato a chiamare alcuna API ThreadX con un'opzione di sospensione.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1440">*The application's queue send notification callback is not allowed to call any ThreadX API with a suspension option.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1441">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1441">Parameters</span></span>

- <span data-ttu-id="94e54-1442">**queue_ptr** Puntatore alla coda creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1442">**queue_ptr** Pointer to previously created queue.</span></span>
- <span data-ttu-id="94e54-1443">**queue_send_notify** Puntatore alla funzione di notifica di invio della coda dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1443">**queue_send_notify** Pointer to application's queue send notification function.</span></span> <span data-ttu-id="94e54-1444">Se questo valore è TX_NULL, la notifica è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1444">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1445">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1445">Return Values</span></span>

- <span data-ttu-id="94e54-1446">**TX_SUCCESS** (0x00) registrazione della notifica di invio della coda riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-1446">**TX_SUCCESS** (0x00) Successful registration of queue send notification.</span></span>
- <span data-ttu-id="94e54-1447">Il puntatore della coda **TX_QUEUE_ERROR** (0x09) non è valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1447">**TX_QUEUE_ERROR** (0x09) Invalid queue pointer.</span></span>
- <span data-ttu-id="94e54-1448">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema è stato compilato con le funzionalità di notifica disabilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-1448">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1449">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1449">Allowed From</span></span>

<span data-ttu-id="94e54-1450">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1450">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1451">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1451">Example</span></span>

```c
TX_QUEUE my_queue;
/* Register the "my_queue_send_notify" function for monitoring
messages sent to the queue "my_queue." */
status = tx_queue_send_notify(&my_queue, my_queue_send_notify);

/* If status is TX_SUCCESS the queue send notification function was
successfully registered. */
void my_queue_send_notify(TX_QUEUE *queue_ptr)
{
    /* A message was just sent to this queue! */
}
```

### <a name="see-also"></a><span data-ttu-id="94e54-1452">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1452">See Also</span></span>

- <span data-ttu-id="94e54-1453">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1453">tx_queue_create</span></span>
- <span data-ttu-id="94e54-1454">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1454">tx_queue_delete</span></span>
- <span data-ttu-id="94e54-1455">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="94e54-1455">tx_queue_flush</span></span>
- <span data-ttu-id="94e54-1456">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1456">tx_queue_front_send</span></span>
- <span data-ttu-id="94e54-1457">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1457">tx_queue_info_get</span></span>
- <span data-ttu-id="94e54-1458">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1458">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="94e54-1459">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1459">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1460">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1460">tx_queue_prioritize</span></span>
- <span data-ttu-id="94e54-1461">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="94e54-1461">tx_queue_receive</span></span>
- <span data-ttu-id="94e54-1462">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="94e54-1462">tx_queue_send</span></span>

## <a name="tx_semaphore_ceiling_put"></a><span data-ttu-id="94e54-1463">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1463">tx_semaphore_ceiling_put</span></span>

<span data-ttu-id="94e54-1464">Inserire un'istanza in conteggio semaforo con limite massimo</span><span class="sxs-lookup"><span data-stu-id="94e54-1464">Place an instance in counting semaphore with ceiling</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1465">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1465">Prototype</span></span>

```c
UINT tx_semaphore_ceiling_put(
    TX_SEMAPHORE *semaphore_ptr,
    ULONG ceiling);
```

### <a name="description"></a><span data-ttu-id="94e54-1466">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1466">Description</span></span>

<span data-ttu-id="94e54-1467">Questo servizio inserisce un'istanza nel semaforo di conteggio specificato, che in realtà incrementa il semaforo di conteggio di uno.</span><span class="sxs-lookup"><span data-stu-id="94e54-1467">This service puts an instance into the specified counting semaphore, which in reality increments the counting semaphore by one.</span></span> <span data-ttu-id="94e54-1468">Se il valore corrente del semaforo di conteggio è maggiore o uguale al limite specificato, l'istanza non verrà inserita e verrà restituito un errore TX_CEILING_EXCEEDED.</span><span class="sxs-lookup"><span data-stu-id="94e54-1468">If the counting semaphore's current value is greater than or equal to the specified ceiling, the instance will not be put and a TX_CEILING_EXCEEDED error will be returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1469">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1469">Parameters</span></span>

- <span data-ttu-id="94e54-1470">**semaphore_ptr** Puntatore al semaforo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1470">**semaphore_ptr** Pointer to previously created semaphore.</span></span>
- <span data-ttu-id="94e54-1471">**limite massimo** Limite massimo consentito per il semaforo. i valori validi sono compresi tra 1 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="94e54-1471">**ceiling** Maximum limit allowed for the semaphore (valid values range from 1 through 0xFFFFFFFF).</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1472">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1472">Return Values</span></span>

- <span data-ttu-id="94e54-1473">**TX_SUCCESS (0x00)** Tetto del semaforo riuscito inserito.</span><span class="sxs-lookup"><span data-stu-id="94e54-1473">**TX_SUCCESS (0x00)** Successful semaphore ceiling put.</span></span>
- <span data-ttu-id="94e54-1474">La richiesta PUT **TX_CEILING_EXCEEDED** (0x21) supera il limite massimo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1474">**TX_CEILING_EXCEEDED** (0x21) Put request exceeds ceiling.</span></span>
- <span data-ttu-id="94e54-1475">**TX_INVALID_CEILING** (0x22) è stato specificato un valore non valido pari a zero per il limite massimo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1475">**TX_INVALID_CEILING** (0x22) An invalid value of zero was supplied for ceiling.</span></span>
- <span data-ttu-id="94e54-1476">**TX_SEMAPHORE_ERROR** (0x0C) puntatore a semaforo non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1476">**TX_SEMAPHORE_ERROR** (0x0C) Invalid semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1477">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1477">Allowed From</span></span>

<span data-ttu-id="94e54-1478">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1478">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1479">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1479">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;

/* Increment the counting semaphore "my_semaphore" but make sure
that it never exceeds 7 as specified in the call. */
status = tx_semaphore_ceiling_put(&my_semaphore, 7);

/* If status is TX_SUCCESS the semaphore count has been
incremented. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1480">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1480">See Also</span></span>

- <span data-ttu-id="94e54-1481">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1481">tx_semaphore_create</span></span>
- <span data-ttu-id="94e54-1482">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1482">tx_semaphore_delete</span></span>
- <span data-ttu-id="94e54-1483">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1483">tx_semaphore_get</span></span>
- <span data-ttu-id="94e54-1484">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1484">tx_semaphore_info_get</span></span>
- <span data-ttu-id="94e54-1485">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1485">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="94e54-1486">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1486">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1487">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1487">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="94e54-1488">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1488">tx_semaphore_put</span></span>
- <span data-ttu-id="94e54-1489">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1489">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_create"></a><span data-ttu-id="94e54-1490">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1490">tx_semaphore_create</span></span>

<span data-ttu-id="94e54-1491">Crea semaforo di conteggio</span><span class="sxs-lookup"><span data-stu-id="94e54-1491">Create counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1492">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1492">Prototype</span></span>

```c
UINT tx_semaphore_create(
    TX_SEMAPHORE *semaphore_ptr,
    CHAR *name_ptr, 
    ULONG initial_count);
```

### <a name="description"></a><span data-ttu-id="94e54-1493">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1493">Description</span></span>

<span data-ttu-id="94e54-1494">Questo servizio crea un semaforo di conteggio per la sincronizzazione tra thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1494">This service creates a counting semaphore for inter-thread synchronization.</span></span> <span data-ttu-id="94e54-1495">Il numero di semafori iniziale viene specificato come parametro di input.</span><span class="sxs-lookup"><span data-stu-id="94e54-1495">The initial semaphore count is specified as an input parameter.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1496">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1496">Parameters</span></span>

- <span data-ttu-id="94e54-1497">**semaphore_ptr** Puntatore a un blocco di controllo del semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1497">**semaphore_ptr** Pointer to a semaphore control block.</span></span>
- <span data-ttu-id="94e54-1498">**name_ptr** Puntatore al nome del semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1498">**name_ptr** Pointer to the name of the semaphore.</span></span>
- <span data-ttu-id="94e54-1499">**initial_count** Specifica il numero iniziale per questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1499">**initial_count** Specifies the initial count for this semaphore.</span></span> <span data-ttu-id="94e54-1500">I valori validi sono compresi tra 0x00000000 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="94e54-1500">Legal values range from 0x00000000 through 0xFFFFFFFF.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1501">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1501">Return Values</span></span>

- <span data-ttu-id="94e54-1502">**TX_SUCCESS** (0x00) riuscita della creazione del semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1502">**TX_SUCCESS** (0x00) Successful semaphore creation.</span></span>
- <span data-ttu-id="94e54-1503">**TX_SEMAPHORE_ERROR** (0x0C) puntatore a semaforo non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1503">**TX_SEMAPHORE_ERROR** (0x0C) Invalid semaphore pointer.</span></span> <span data-ttu-id="94e54-1504">Il puntatore è NULL o il semaforo è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1504">Either the pointer is NULL or the semaphore is already created.</span></span>
- <span data-ttu-id="94e54-1505">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1505">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1506">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1506">Allowed From</span></span>

<span data-ttu-id="94e54-1507">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="94e54-1507">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1508">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1508">Preemption Possible</span></span>

<span data-ttu-id="94e54-1509">No</span><span class="sxs-lookup"><span data-stu-id="94e54-1509">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1510">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1510">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Create a counting semaphore whose initial value is 1.
This is typically the technique used to make a binary
semaphore. Binary semaphores are used to provide
protection over a common resource. */
status = tx_semaphore_create(&my_semaphore,
    "my_semaphore_name", 1);

/* If status equals TX_SUCCESS, my_semaphore is ready for
use. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1511">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1511">See Also</span></span>

- <span data-ttu-id="94e54-1512">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1512">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="94e54-1513">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1513">tx_semaphore_delete</span></span>
- <span data-ttu-id="94e54-1514">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1514">tx_semaphore_get</span></span>
- <span data-ttu-id="94e54-1515">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1515">tx_semaphore_info_get</span></span>
- <span data-ttu-id="94e54-1516">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1516">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="94e54-1517">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1517">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1518">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1518">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="94e54-1519">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1519">tx_semaphore_put</span></span>
- <span data-ttu-id="94e54-1520">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1520">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_delete"></a><span data-ttu-id="94e54-1521">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1521">tx_semaphore_delete</span></span>

<span data-ttu-id="94e54-1522">Elimina semaforo di conteggio</span><span class="sxs-lookup"><span data-stu-id="94e54-1522">Delete counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1523">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1523">Prototype</span></span>
```c
UINT tx_semaphore_delete(TX_SEMAPHORE *semaphore_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-1524">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1524">Description</span></span>

<span data-ttu-id="94e54-1525">Questo servizio Elimina il semaforo di conteggio specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1525">This service deletes the specified counting semaphore.</span></span> <span data-ttu-id="94e54-1526">Tutti i thread sospesi in attesa di un'istanza del semaforo vengono ripresi e viene dato un TX_DELETED stato restituito.</span><span class="sxs-lookup"><span data-stu-id="94e54-1526">All threads suspended waiting for a semaphore instance are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-1527">*Prima di eliminare il semaforo, l'applicazione deve garantire che un callback di notifica put per questo semaforo venga completato (o disabilitato). Inoltre, l'applicazione deve impedire l'uso futuro di un semaforo eliminato.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1527">*The application must ensure that a put notify callback for this semaphore is completed (or disabled) before deleting the semaphore. In addition, the application must prevent all future use of a deleted semaphore.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1528">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1528">Parameters</span></span>

- <span data-ttu-id="94e54-1529">**semaphore_ptr** Puntatore a un semaforo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1529">**semaphore_ptr** Pointer to a previously created semaphore.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1530">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1530">Return Values</span></span>

- <span data-ttu-id="94e54-1531">**TX_SUCCESS** (0x00) il conteggio dell'eliminazione del semaforo è riuscito.</span><span class="sxs-lookup"><span data-stu-id="94e54-1531">**TX_SUCCESS** (0x00) Successful counting semaphore deletion.</span></span>
- <span data-ttu-id="94e54-1532">**TX_SEMAPHORE_ERROR** (0x0C) puntatore del semaforo di conteggio non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1532">**TX_SEMAPHORE_ERROR** (0x0C) Invalid counting semaphore pointer.</span></span>
- <span data-ttu-id="94e54-1533">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1533">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1534">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1534">Allowed From</span></span>

<span data-ttu-id="94e54-1535">Thread</span><span class="sxs-lookup"><span data-stu-id="94e54-1535">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1536">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1536">Preemption Possible</span></span>

<span data-ttu-id="94e54-1537">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-1537">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1538">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1538">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Delete counting semaphore. Assume that the counting
semaphore has already been created. */
status = tx_semaphore_delete(&my_semaphore);

/* If status equals TX_SUCCESS, the counting semaphore is
deleted. */
```

<span data-ttu-id="94e54-1539">**Vedere anche**</span><span class="sxs-lookup"><span data-stu-id="94e54-1539">**See Also**</span></span>

- <span data-ttu-id="94e54-1540">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1540">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="94e54-1541">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1541">tx_semaphore_create</span></span>
- <span data-ttu-id="94e54-1542">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1542">tx_semaphore_get</span></span>
- <span data-ttu-id="94e54-1543">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1543">tx_semaphore_info_get</span></span>
- <span data-ttu-id="94e54-1544">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1544">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="94e54-1545">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1545">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1546">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1546">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="94e54-1547">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1547">tx_semaphore_put</span></span>
- <span data-ttu-id="94e54-1548">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1548">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_get"></a><span data-ttu-id="94e54-1549">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1549">tx_semaphore_get</span></span>

<span data-ttu-id="94e54-1550">Ottenere un'istanza dal semaforo di conteggio</span><span class="sxs-lookup"><span data-stu-id="94e54-1550">Get instance from counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1551">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1551">Prototype</span></span>

```c
UINT tx_semaphore_get(
    TX_SEMAPHORE *semaphore_ptr,
    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="94e54-1552">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1552">Description</span></span>

<span data-ttu-id="94e54-1553">Questo servizio recupera un'istanza (un numero singolo) dal semaforo di conteggio specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1553">This service retrieves an instance (a single count) from the specified counting semaphore.</span></span> <span data-ttu-id="94e54-1554">Di conseguenza, il conteggio del semaforo specificato viene diminuito di uno.</span><span class="sxs-lookup"><span data-stu-id="94e54-1554">As a result, the specified semaphore's count is decreased by one.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1555">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1555">Parameters</span></span>

- <span data-ttu-id="94e54-1556">**semaphore_ptr**</span><span class="sxs-lookup"><span data-stu-id="94e54-1556">**semaphore_ptr**</span></span> <br><span data-ttu-id="94e54-1557">Puntatore a un semaforo di conteggio creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1557">Pointer to a previously created counting semaphore.</span></span>
- <span data-ttu-id="94e54-1558">**wait_option**</span><span class="sxs-lookup"><span data-stu-id="94e54-1558">**wait_option**</span></span> <br><span data-ttu-id="94e54-1559">Definisce il comportamento del servizio se non sono disponibili istanze del semaforo. ovvero, il numero di semafori è pari a zero.</span><span class="sxs-lookup"><span data-stu-id="94e54-1559">Defines how the service behaves if there are no instances of the semaphore available; i.e., the semaphore count is zero.</span></span> <span data-ttu-id="94e54-1560">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="94e54-1560">The wait options are defined as follows:</span></span>
  - <span data-ttu-id="94e54-1561">**TX_NO_WAIT** (0x00000000): la selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1561">**TX_NO_WAIT** (0x00000000) - Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="94e54-1562">*Questa è l'unica opzione valida se il servizio viene chiamato da un non thread. ad esempio, inizializzazione, timer o ISR.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1562">*This is the only valid option if the service is called from a non-thread; e.g., initialization, timer, or ISR.*</span></span>
  - <span data-ttu-id="94e54-1563">**TX_WAIT_FOREVER** (0xFFFFFFFF): se si seleziona TX_WAIT_FOREVER, il thread chiamante sospenderà per un tempo illimitato fino a quando non sarà disponibile un'istanza del semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1563">**TX_WAIT_FOREVER** (0xFFFFFFFF) - Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a semaphore instance is available.</span></span>
  - <span data-ttu-id="94e54-1564">valore di timeout (0x00000001 tramite 0xFFFFFFFE)-la selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa di un'istanza del semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1564">timeout value (0x00000001 through 0xFFFFFFFE) - Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a semaphore instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1565">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1565">Return Values</span></span>

- <span data-ttu-id="94e54-1566">**TX_SUCCESS** (0x00) il recupero di un'istanza del semaforo è riuscito.</span><span class="sxs-lookup"><span data-stu-id="94e54-1566">**TX_SUCCESS** (0x00) Successful retrieval of a semaphore instance.</span></span>
- <span data-ttu-id="94e54-1567">Il semaforo di conteggio **TX_DELETED** (0x01) è stato eliminato mentre il thread è stato sospeso.</span><span class="sxs-lookup"><span data-stu-id="94e54-1567">**TX_DELETED** (0x01) Counting semaphore was deleted while thread was suspended.</span></span>
- <span data-ttu-id="94e54-1568">Il servizio **TX_NO_INSTANCE** (0x0D) non è stato in grado di recuperare un'istanza del semaforo di conteggio (il numero di semafori è pari a zero entro il tempo di attesa specificato).</span><span class="sxs-lookup"><span data-stu-id="94e54-1568">**TX_NO_INSTANCE** (0x0D) Service was unable to retrieve an instance of the counting semaphore (semaphore count is zero within the specified time to wait).</span></span>
- <span data-ttu-id="94e54-1569">La sospensione **TX_WAIT_ABORTED** (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="94e54-1569">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="94e54-1570">**TX_SEMAPHORE_ERROR** (0x0C) puntatore del semaforo di conteggio non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1570">**TX_SEMAPHORE_ERROR** (0x0C) Invalid counting semaphore pointer.</span></span>
- <span data-ttu-id="94e54-1571">**TX_WAIT_ERROR** (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1571">**TX_WAIT_ERROR** (0x04) A wait option other than TX_NO_WAIT was specified on a call from a non-thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1572">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1572">Allowed From</span></span>

<span data-ttu-id="94e54-1573">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1573">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1574">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1574">Preemption Possible</span></span>

<span data-ttu-id="94e54-1575">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-1575">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1576">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1576">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Get a semaphore instance from the semaphore
"my_semaphore." If the semaphore count is zero,
suspend until an instance becomes available.
Note that this suspension is only possible from
application threads. */
status = tx_semaphore_get(&my_semaphore, TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the thread has obtained
an instance of the semaphore. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1577">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1577">See Also</span></span>

- <span data-ttu-id="94e54-1578">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1578">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="94e54-1579">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1579">tx_semaphore_create</span></span>
- <span data-ttu-id="94e54-1580">tx_semahore_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1580">tx_semahore_delete</span></span>
- <span data-ttu-id="94e54-1581">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1581">tx_semaphore_info_get</span></span>
- <span data-ttu-id="94e54-1582">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1582">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="94e54-1583">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1583">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="94e54-1584">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1584">tx_semaphore_put</span></span>
- <span data-ttu-id="94e54-1585">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1585">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_info_get"></a><span data-ttu-id="94e54-1586">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1586">tx_semaphore_info_get</span></span>

<span data-ttu-id="94e54-1587">Recuperare informazioni sul semaforo</span><span class="sxs-lookup"><span data-stu-id="94e54-1587">Retrieve information about semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1588">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1588">Prototype</span></span>

```c
UINT tx_semaphore_info_get(
    TX_SEMAPHORE *semaphore_ptr,
    CHAR **name, ULONG *current_value,
    TX_THREAD **first_suspended,
    ULONG *suspended_count,
    TX_SEMAPHORE **next_semaphore);
```

### <a name="description"></a><span data-ttu-id="94e54-1589">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1589">Description</span></span>

<span data-ttu-id="94e54-1590">Questo servizio recupera le informazioni sul semaforo specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1590">This service retrieves information about the specified semaphore.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1591">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1591">Parameters</span></span>

- <span data-ttu-id="94e54-1592">**semaphore_ptr** Puntatore al blocco di controllo del semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1592">**semaphore_ptr** Pointer to semaphore control block.</span></span>
- <span data-ttu-id="94e54-1593">**nome** Puntatore alla destinazione per il puntatore al nome del semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1593">**name** Pointer to destination for the pointer to the semaphore's name.</span></span>
- <span data-ttu-id="94e54-1594">**Current_value** Puntatore alla destinazione per il conteggio del semaforo corrente.</span><span class="sxs-lookup"><span data-stu-id="94e54-1594">**current_value** Pointer to destination for the current semaphore's count.</span></span>
- <span data-ttu-id="94e54-1595">**first_suspended** Puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione di questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1595">**first_suspended** Pointer to destination for the pointer to the thread that is first on the suspension list of this semaphore.</span></span>
- <span data-ttu-id="94e54-1596">**suspended_count** Puntatore alla destinazione per il numero di thread attualmente sospesi in questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1596">**suspended_count** Pointer to destination for the number of threads currently suspended on this semaphore.</span></span>
- <span data-ttu-id="94e54-1597">**next_semaphore** Puntatore alla destinazione per il puntatore del semaforo creato successivo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1597">**next_semaphore** Pointer to destination for the pointer of the next created semaphore.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1598">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1598">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1599">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1599">Return Values</span></span>

- <span data-ttu-id="94e54-1600">Recupero delle informazioni **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-1600">**TX_SUCCESS** (0x00) information retrieval.</span></span>

- <span data-ttu-id="94e54-1601">**TX_SEMAPHORE_ERROR** (0x0C) puntatore a semaforo non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1601">**TX_SEMAPHORE_ERROR** (0x0C) Invalid semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1602">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1602">Allowed From</span></span>

<span data-ttu-id="94e54-1603">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1603">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1604">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1604">Preemption Possible</span></span>

<span data-ttu-id="94e54-1605">No</span><span class="sxs-lookup"><span data-stu-id="94e54-1605">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1606">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1606">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
CHAR *name;
ULONG current_value;
TX_THREAD *first_suspended;
ULONG suspended_count;
TX_SEMAPHORE *next_semaphore;
UINT status;

/* Retrieve information about the previously created
semaphore "my_semaphore." */
status = tx_semaphore_info_get(&my_semaphore, &name,
    &current_value,
    &first_suspended, &suspended_count,
    &next_semaphore);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1607">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1607">See Also</span></span>

- <span data-ttu-id="94e54-1608">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1608">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="94e54-1609">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1609">tx_semaphore_create</span></span>
- <span data-ttu-id="94e54-1610">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1610">tx_semaphore_delete</span></span>
- <span data-ttu-id="94e54-1611">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1611">tx_semaphore_get</span></span>
- <span data-ttu-id="94e54-1612">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1612">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="94e54-1613">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1613">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1614">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1614">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="94e54-1615">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1615">tx_semaphore_put</span></span>
- <span data-ttu-id="94e54-1616">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1616">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_performance_info_get"></a><span data-ttu-id="94e54-1617">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1617">tx_semaphore_performance_info_get</span></span>

<span data-ttu-id="94e54-1618">Ottenere informazioni sulle prestazioni del semaforo</span><span class="sxs-lookup"><span data-stu-id="94e54-1618">Get semaphore performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1619">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1619">Prototype</span></span>

```c
UINT tx_semaphore_performance_info_get(
    TX_SEMAPHORE *semaphore_ptr,
    ULONG *puts, 
    ULONG *gets,
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="94e54-1620">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1620">Description</span></span>

<span data-ttu-id="94e54-1621">Questo servizio recupera le informazioni sulle prestazioni relative al semaforo specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1621">This service retrieves performance information about the specified semaphore.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-1622">*La libreria e l'applicazione threadX devono essere compilate con*  \* **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** _ _defined per il servizio per restituire informazioni sulle prestazioni. \*</span><span class="sxs-lookup"><span data-stu-id="94e54-1622">*The ThreadX library and application must be built with* ***TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information.*</span></span>

<span data-ttu-id="94e54-1623">**Parametri**</span><span class="sxs-lookup"><span data-stu-id="94e54-1623">**Parameters**</span></span>

-  <span data-ttu-id="94e54-1624">**semaphore_ptr** Puntatore al semaforo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1624">**semaphore_ptr** Pointer to previously created semaphore.</span></span>
-  <span data-ttu-id="94e54-1625">**inserisce** Puntatore alla destinazione per il numero di richieste PUT eseguite sul semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1625">**puts** Pointer to destination for the number of put requests performed on this semaphore.</span></span>
-  <span data-ttu-id="94e54-1626">**ottiene** Puntatore alla destinazione per il numero di richieste Get eseguite su questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1626">**gets** Pointer to destination for the number of get requests performed on this semaphore.</span></span>
-  <span data-ttu-id="94e54-1627">**sospensioni** Puntatore alla destinazione per il numero di sospensioni del thread in questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1627">**suspensions** Pointer to destination for the number of thread suspensions on this semaphore.</span></span>
-  <span data-ttu-id="94e54-1628">**timeout** Puntatore alla destinazione per il numero di timeout di sospensione del thread in questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1628">**timeouts** Pointer to destination for the number of thread suspension timeouts on this semaphore.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1629">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1629">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1630">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1630">Return Values</span></span>

- <span data-ttu-id="94e54-1631">**TX_SUCCESS** (0x00) prestazioni del semaforo riuscite.</span><span class="sxs-lookup"><span data-stu-id="94e54-1631">**TX_SUCCESS** (0x00) Successful semaphore performance get.</span></span>
- <span data-ttu-id="94e54-1632">**TX_PTR_ERROR** (0x03) puntatore a semaforo non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1632">**TX_PTR_ERROR** (0x03) Invalid semaphore pointer.</span></span>
- <span data-ttu-id="94e54-1633">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-1633">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1634">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1634">Allowed From</span></span>

<span data-ttu-id="94e54-1635">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1635">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1636">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1636">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on the previously created
semaphore. */
status = tx_semaphore_performance_info_get(&my_semaphore, &puts,
    &gets, &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1637">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1637">See Also</span></span>

- <span data-ttu-id="94e54-1638">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1638">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="94e54-1639">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1639">tx_semaphore_create</span></span>
- <span data-ttu-id="94e54-1640">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1640">tx_semaphore_delete</span></span>
- <span data-ttu-id="94e54-1641">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1641">tx_semaphore_get</span></span>
- <span data-ttu-id="94e54-1642">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1642">tx_semaphore_info_get</span></span>
- <span data-ttu-id="94e54-1643">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1643">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1644">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1644">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="94e54-1645">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1645">tx_semaphore_put</span></span>
- <span data-ttu-id="94e54-1646">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1646">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_performance_system_info_get"></a><span data-ttu-id="94e54-1647">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1647">tx_semaphore_performance_system_info_get</span></span>

<span data-ttu-id="94e54-1648">Ottenere informazioni sulle prestazioni del sistema Semaphore</span><span class="sxs-lookup"><span data-stu-id="94e54-1648">Get semaphore system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1649">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1649">Prototype</span></span>

```c
UINT tx_semaphore_performance_system_info_get(
    ULONG *puts,
    ULONG *gets, 
    ULONG *suspensions, 
    ULONG *timeouts);
```

### <a name="description"></a><span data-ttu-id="94e54-1650">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1650">Description</span></span>

<span data-ttu-id="94e54-1651">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i semafori nel sistema.</span><span class="sxs-lookup"><span data-stu-id="94e54-1651">This service retrieves performance information about all the semaphores in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-1652">*La libreria e l'applicazione threadX devono essere compilate con*  \* **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** _ _defined per il servizio per restituire informazioni sulle prestazioni \*</span><span class="sxs-lookup"><span data-stu-id="94e54-1652">*The ThreadX library and application must be built with* ***TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1653">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1653">Parameters</span></span>

- <span data-ttu-id="94e54-1654">**inserisce** Puntatore alla destinazione per il numero totale di richieste PUT eseguite su tutti i semafori.</span><span class="sxs-lookup"><span data-stu-id="94e54-1654">**puts** Pointer to destination for the total number of put requests performed on all semaphores.</span></span>
- <span data-ttu-id="94e54-1655">**ottiene** Puntatore alla destinazione per il numero totale di richieste Get eseguite su tutti i semafori.</span><span class="sxs-lookup"><span data-stu-id="94e54-1655">**gets** Pointer to destination for the total number of get requests performed on all semaphores.</span></span>
- <span data-ttu-id="94e54-1656">**sospensioni** Puntatore alla destinazione per il numero totale di sospensioni dei thread in tutti i semafori.</span><span class="sxs-lookup"><span data-stu-id="94e54-1656">**suspensions** Pointer to destination for the total number of thread suspensions on all semaphores.</span></span>
- <span data-ttu-id="94e54-1657">**timeout** Puntatore alla destinazione per il numero totale di timeout di sospensione del thread in tutti i semafori.</span><span class="sxs-lookup"><span data-stu-id="94e54-1657">**timeouts** Pointer to destination for the total number of thread suspension timeouts on all semaphores.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1658">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1658">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1659">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1659">Return Values</span></span>

- <span data-ttu-id="94e54-1660">Prestazioni del sistema **TX_SUCCESS** (0x00) Get.</span><span class="sxs-lookup"><span data-stu-id="94e54-1660">**TX_SUCCESS** (0x00) system performance get.</span></span>
- <span data-ttu-id="94e54-1661">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-1661">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1662">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1662">Allowed From</span></span>

<span data-ttu-id="94e54-1663">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1663">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1664">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1664">Example</span></span>

```c
ULONG puts;
ULONG gets;
ULONG suspensions;
ULONG timeouts;

/* Retrieve performance information on all previously created
semaphores. */
status = tx_semaphore_performance_system_info_get(&puts, &gets,
    &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1665">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1665">See Also</span></span>

- <span data-ttu-id="94e54-1666">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1666">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="94e54-1667">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1667">tx_semaphore_create</span></span>
- <span data-ttu-id="94e54-1668">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1668">tx_semaphore_delete</span></span>
- <span data-ttu-id="94e54-1669">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1669">tx_semaphore_get</span></span>
- <span data-ttu-id="94e54-1670">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1670">tx_semaphore_info_get</span></span>
- <span data-ttu-id="94e54-1671">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1671">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="94e54-1672">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1672">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="94e54-1673">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1673">tx_semaphore_put</span></span>
- <span data-ttu-id="94e54-1674">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1674">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_prioritize"></a><span data-ttu-id="94e54-1675">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1675">tx_semaphore_prioritize</span></span>

<span data-ttu-id="94e54-1676">Priorità dell'elenco di sospensioni del semaforo</span><span class="sxs-lookup"><span data-stu-id="94e54-1676">Prioritize semaphore suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1677">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1677">Prototype</span></span>

```c
UINT tx_semaphore_prioritize(TX_SEMAPHORE *semaphore_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-1678">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1678">Description</span></span>

<span data-ttu-id="94e54-1679">Questo servizio posiziona il thread con priorità più elevata sospeso per un'istanza del semaforo all'inizio dell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="94e54-1679">This service places the highest priority thread suspended for an instance of the semaphore at the front of the suspension list.</span></span> <span data-ttu-id="94e54-1680">Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.</span><span class="sxs-lookup"><span data-stu-id="94e54-1680">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1681">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1681">Parameters</span></span>

- <span data-ttu-id="94e54-1682">**semaphore_ptr** Puntatore a un semaforo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1682">**semaphore_ptr** Pointer to a previously created semaphore.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1683">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1683">Return Values</span></span>

- <span data-ttu-id="94e54-1684">**TX_SUCCESS** (0x00) la priorità del semaforo è riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-1684">**TX_SUCCESS** (0x00) Successful semaphore prioritize.</span></span>
- <span data-ttu-id="94e54-1685">**TX_SEMAPHORE_ERROR** (0x0C) puntatore del semaforo di conteggio non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1685">**TX_SEMAPHORE_ERROR** (0x0C) Invalid counting semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1686">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1686">Allowed From</span></span>

<span data-ttu-id="94e54-1687">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1687">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1688">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1688">Preemption Possible</span></span>

<span data-ttu-id="94e54-1689">No</span><span class="sxs-lookup"><span data-stu-id="94e54-1689">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1690">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1690">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Ensure that the highest priority thread will receive
the next instance of this semaphore. */
status = tx_semaphore_prioritize(&my_semaphore);

/* If status equals TX_SUCCESS, the highest priority
suspended thread is at the front of the list. The
next tx_semaphore_put call made to this semaphore will
wake up this thread. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1691">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1691">See Also</span></span>

- <span data-ttu-id="94e54-1692">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1692">tx_semaphore_create</span></span>
- <span data-ttu-id="94e54-1693">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1693">tx_semaphore_delete</span></span>
- <span data-ttu-id="94e54-1694">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1694">tx_semaphore_get</span></span>
- <span data-ttu-id="94e54-1695">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1695">tx_semaphore_info_get</span></span>
- <span data-ttu-id="94e54-1696">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1696">tx_semaphore_put</span></span>

## <a name="tx_semaphore_put"></a><span data-ttu-id="94e54-1697">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1697">tx_semaphore_put</span></span>

<span data-ttu-id="94e54-1698">Inserire un'istanza in conteggio semaforo</span><span class="sxs-lookup"><span data-stu-id="94e54-1698">Place an instance in counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1699">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1699">Prototype</span></span>

```c
UINT tx_semaphore_put(TX_SEMAPHORE *semaphore_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-1700">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1700">Description</span></span>

<span data-ttu-id="94e54-1701">Questo servizio inserisce un'istanza nel semaforo di conteggio specificato, che in realtà incrementa il semaforo di conteggio di uno.</span><span class="sxs-lookup"><span data-stu-id="94e54-1701">This service puts an instance into the specified counting semaphore, which in reality increments the counting semaphore by one.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1702">*Se questo servizio viene chiamato quando il semaforo è costituito da tutti (OxFFFFFFFF), la nuova operazione Put provocherà la reimpostazione del semaforo su zero.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1702">*If this service is called when the semaphore is all ones (OxFFFFFFFF), the new put operation will cause the semaphore to be reset to zero.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1703">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1703">Parameters</span></span>

- <span data-ttu-id="94e54-1704">**semaphore_ptr** Puntatore al blocco di controllo semaforo di conteggio creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1704">**semaphore_ptr** Pointer to the previously created counting semaphore control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1705">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1705">Return Values</span></span>

- <span data-ttu-id="94e54-1706">**TX_SUCCESS** (0x00) semaforo riuscito put.</span><span class="sxs-lookup"><span data-stu-id="94e54-1706">**TX_SUCCESS** (0x00) Successful semaphore put.</span></span>
- <span data-ttu-id="94e54-1707">Il puntatore **TX_SEMAPHORE_ERROR** (0X0C) non è valido per il conteggio del semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1707">**TX_SEMAPHORE_ERROR** (0x0C) Invalid pointer to counting semaphore.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1708">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1708">Allowed From</span></span>

<span data-ttu-id="94e54-1709">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1709">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1710">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1710">Preemption Possible</span></span>

<span data-ttu-id="94e54-1711">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-1711">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1712">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1712">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT status;

/* Increment the counting semaphore "my_semaphore." */
status = tx_semaphore_put(&my_semaphore);

/* If status equals TX_SUCCESS, the semaphore count has
been incremented. Of course, if a thread was waiting,
it was given the semaphore instance and resumed. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1713">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1713">See Also</span></span>

- <span data-ttu-id="94e54-1714">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1714">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="94e54-1715">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1715">tx_semaphore_create</span></span>
- <span data-ttu-id="94e54-1716">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1716">tx_semaphore_delete</span></span>
- <span data-ttu-id="94e54-1717">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1717">tx_semaphore_info_get</span></span>
- <span data-ttu-id="94e54-1718">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1718">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="94e54-1719">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1719">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1720">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1720">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="94e54-1721">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1721">tx_semaphore_get</span></span>
- <span data-ttu-id="94e54-1722">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1722">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_put_notify"></a><span data-ttu-id="94e54-1723">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1723">tx_semaphore_put_notify</span></span>

<span data-ttu-id="94e54-1724">Invia una notifica all'applicazione quando viene inserito il semaforo</span><span class="sxs-lookup"><span data-stu-id="94e54-1724">Notify application when semaphore is put</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1725">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1725">Prototype</span></span>

```c
UINT tx_semaphore_put_notify(
    TX_SEMAPHORE *semaphore_ptr,
    VOID (*semaphore_put_notify)(TX_SEMAPHORE *));
```

### <a name="description"></a><span data-ttu-id="94e54-1726">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1726">Description</span></span>

<span data-ttu-id="94e54-1727">Questo servizio registra una funzione di callback delle notifiche chiamata ogni volta che viene inserito il semaforo specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1727">This service registers a notification callback function that is called whenever the specified semaphore is put.</span></span> <span data-ttu-id="94e54-1728">L'elaborazione del callback di notifica viene definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1728">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1729">*Il callback di notifica del semaforo dell'applicazione non è autorizzato a chiamare alcuna API ThreadX con un'opzione di sospensione.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1729">*The application's semaphore notification callback is not allowed to call any ThreadX API with a suspension option.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1730">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1730">Parameters</span></span>

- <span data-ttu-id="94e54-1731">**semaphore_ptr** Puntatore al semaforo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1731">**semaphore_ptr** Pointer to previously created semaphore.</span></span>
- <span data-ttu-id="94e54-1732">**semaphore_put_notify** Puntatore alla funzione di notifica put del semaforo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1732">**semaphore_put_notify** Pointer to application's semaphore put notification function.</span></span> <span data-ttu-id="94e54-1733">Se questo valore è TX_NULL, la notifica è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1733">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1734">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1734">Return Values</span></span>

- <span data-ttu-id="94e54-1735">**TX_SUCCESS** (0x00) registrazione corretta della notifica put del semaforo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1735">**TX_SUCCESS** (0x00) Successful registration of semaphore put notification.</span></span>
- <span data-ttu-id="94e54-1736">**TX_SEMAPHORE_ERROR** (0x0C) puntatore a semaforo non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1736">**TX_SEMAPHORE_ERROR** (0x0C) Invalid semaphore pointer.</span></span>
- <span data-ttu-id="94e54-1737">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema è stato compilato con le funzionalità di notifica disabilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-1737">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1738">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1738">Allowed From</span></span>

<span data-ttu-id="94e54-1739">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1739">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1740">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1740">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;

/* Register the "my_semaphore_put_notify" function for monitoring
the put operations on the semaphore "my_semaphore." */
status = tx_semaphore_put_notify(&my_semaphore, my_semaphore_put_notify);

/* If status is TX_SUCCESS the semaphore put notification function
was successfully registered. */
void my_semaphore_put_notify(TX_SEMAPHORE *semaphore_ptr)
{
    /* The semaphore was just put! */
}
```

### <a name="see-also"></a><span data-ttu-id="94e54-1741">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1741">See Also</span></span>

- <span data-ttu-id="94e54-1742">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1742">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="94e54-1743">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1743">tx_semaphore_create</span></span>
- <span data-ttu-id="94e54-1744">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1744">tx_semaphore_delete</span></span>
- <span data-ttu-id="94e54-1745">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1745">tx_semaphore_get</span></span>
- <span data-ttu-id="94e54-1746">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1746">tx_semaphore_info_get</span></span>
- <span data-ttu-id="94e54-1747">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1747">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="94e54-1748">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1748">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1749">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="94e54-1749">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="94e54-1750">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="94e54-1750">tx_semaphore_put</span></span>

## <a name="tx_thread_create"></a><span data-ttu-id="94e54-1751">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1751">tx_thread_create</span></span>

<span data-ttu-id="94e54-1752">Crea thread applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-1752">Create application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1753">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1753">Prototype</span></span>

```c
UINT tx_thread_create(
    TX_THREAD *thread_ptr,
    CHAR *name_ptr, 
    VOID (*entry_function)(ULONG),
    ULONG entry_input, 
    VOID *stack_start,
    ULONG stack_size, 
    UINT priority,
    UINT preempt_threshold, 
    ULONG time_slice,
    UINT auto_start);
```

### <a name="description"></a><span data-ttu-id="94e54-1754">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1754">Description</span></span>

<span data-ttu-id="94e54-1755">Questo servizio crea un thread dell'applicazione che avvia l'esecuzione in corrispondenza della funzione di immissione attività specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1755">This service creates an application thread that starts execution at the specified task entry function.</span></span> <span data-ttu-id="94e54-1756">Lo stack, la priorità, la soglia di precedenza e l'intervallo di tempo sono tra gli attributi specificati dai parametri di input.</span><span class="sxs-lookup"><span data-stu-id="94e54-1756">The stack, priority, preemption-threshold, and time-slice are among the attributes specified by the input parameters.</span></span> <span data-ttu-id="94e54-1757">Viene inoltre specificato lo stato di esecuzione iniziale del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1757">In addition, the initial execution state of the thread is also specified.</span></span>

<span data-ttu-id="94e54-1758">**Parametri**</span><span class="sxs-lookup"><span data-stu-id="94e54-1758">**Parameters**</span></span>

- <span data-ttu-id="94e54-1759">**thread_ptr** Puntatore a un blocco di controllo thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1759">**thread_ptr** Pointer to a thread control block.</span></span>
- <span data-ttu-id="94e54-1760">**name_ptr** Puntatore al nome del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1760">**name_ptr** Pointer to the name of the thread.</span></span>
- <span data-ttu-id="94e54-1761">**entry_function** Specifica la funzione C iniziale per l'esecuzione del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1761">**entry_function** Specifies the initial C function for thread execution.</span></span> <span data-ttu-id="94e54-1762">Quando un thread restituisce da questa funzione entry, viene inserito in uno stato *completato* e sospeso per un periodo illimitato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1762">When a thread returns from this entry function, it is placed in a *completed* state and suspended indefinitely.</span></span>
- <span data-ttu-id="94e54-1763">**entry_input** Valore a 32 bit che viene passato alla funzione entry del thread al momento della prima esecuzione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1763">**entry_input** A 32-bit value that is passed to the thread's entry function when it first executes.</span></span> <span data-ttu-id="94e54-1764">L'uso di questo input è determinato esclusivamente dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1764">The use for this input is determined exclusively by the application.</span></span>
- <span data-ttu-id="94e54-1765">**stack_start** Indirizzo iniziale dell'area di memoria dello stack.</span><span class="sxs-lookup"><span data-stu-id="94e54-1765">**stack_start** Starting address of the stack's memory area.</span></span>
- <span data-ttu-id="94e54-1766">**stack_size** Numero di byte nell'area memoria dello stack.</span><span class="sxs-lookup"><span data-stu-id="94e54-1766">**stack_size** Number bytes in the stack memory area.</span></span> <span data-ttu-id="94e54-1767">L'area dello stack del thread deve essere sufficientemente grande da poter gestire la nidificazione della chiamata di funzione peggiore e l'utilizzo delle variabili locali.</span><span class="sxs-lookup"><span data-stu-id="94e54-1767">The thread's stack area must be large enough to handle its worst-case function call nesting and local variable usage.</span></span>
- <span data-ttu-id="94e54-1768">**priorità** di Priorità numerica del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1768">**priority** Numerical priority of thread.</span></span> <span data-ttu-id="94e54-1769">I valori validi sono compresi tra 0 e (TX_MAX_PRIORITES-1), dove il valore 0 rappresenta la priorità più alta.</span><span class="sxs-lookup"><span data-stu-id="94e54-1769">Legal values range from 0 through (TX_MAX_PRIORITES-1), where a value of 0 represents the highest priority.</span></span>
- <span data-ttu-id="94e54-1770">**preempt_threshold** Livello di priorità più alto (da 0 a (TX_MAX_PRIORITIES-1)) di precedenza disabilitata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1770">**preempt_threshold** Highest priority level (0 through (TX_MAX_PRIORITIES-1)) of disabled preemption.</span></span> <span data-ttu-id="94e54-1771">Solo le priorità superiori a questo livello possono essere interrotte dal thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1771">Only priorities higher than this level are allowed to preempt this thread.</span></span> <span data-ttu-id="94e54-1772">Questo valore deve essere minore o uguale alla priorità specificata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1772">This value must be less than or equal to the specified priority.</span></span> <span data-ttu-id="94e54-1773">Un valore uguale alla priorità del thread Disabilita la soglia di precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1773">A value equal to the thread priority disables preemption-threshold.</span></span>
- <span data-ttu-id="94e54-1774">**time_slice** Numero di cicli timer: è consentita l'esecuzione di un thread prima che venga fornita la possibilità di eseguire altri thread pronti con la stessa priorità.</span><span class="sxs-lookup"><span data-stu-id="94e54-1774">**time_slice** Number of timer-ticks this thread is allowed to run before other ready threads of the same priority are given a chance to run.</span></span> <span data-ttu-id="94e54-1775">Si noti che l'uso della soglia di precedenza Disabilita il sezionamento del tempo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1775">Note that using preemption-threshold disables time-slicing.</span></span> <span data-ttu-id="94e54-1776">I valori validi per le sezioni temporali sono compresi tra 1 e 0xFFFFFFFF (inclusi).</span><span class="sxs-lookup"><span data-stu-id="94e54-1776">Legal time-slice values range from 1 to 0xFFFFFFFF (inclusive).</span></span> <span data-ttu-id="94e54-1777">Il valore **TX_NO_TIME_SLICE** (valore 0) Disabilita il sezionamento del tempo del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1777">A value of **TX_NO_TIME_SLICE** (a value of 0) disables time-slicing of this thread.</span></span>

  > [!NOTE]
  > <span data-ttu-id="94e54-1778">*L'uso del sezionamento del tempo comporta una lieve quantità di overhead del sistema.   Poiché il sezionamento del tempo è utile solo nei casi in cui più thread condividono la stessa priorità, non è necessario assegnare un intervallo di tempo ai thread con una priorità univoca.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1778">*Using time-slicing results in a slight amount of system overhead.   Since time-slicing is only useful in cases where multiple threads   share the same priority, threads having a unique priority should not   be assigned a time-slice.*</span></span>

- <span data-ttu-id="94e54-1779">**auto_start** Specifica se il thread viene avviato immediatamente o in stato sospeso.</span><span class="sxs-lookup"><span data-stu-id="94e54-1779">**auto_start** Specifies whether the thread starts immediately or is placed in a suspended state.</span></span> <span data-ttu-id="94e54-1780">Le opzioni legali sono **TX_AUTO_START** (0x01) e **TX_DONT_START** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-1780">Legal options are **TX_AUTO_START** (0x01) and **TX_DONT_START** (0x00).</span></span> <span data-ttu-id="94e54-1781">Se TX_DONT_START viene specificato, l'applicazione deve chiamare in un secondo momento tx_thread_resume per l'esecuzione del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1781">If TX_DONT_START is specified, the application must later call tx_thread_resume in order for the thread to run.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1782">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1782">Return Values</span></span>

- <span data-ttu-id="94e54-1783">Creazione thread riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-1783">**TX_SUCCESS** (0x00) Successful thread creation.</span></span>
- <span data-ttu-id="94e54-1784">**TX_THREAD_ERROR** (0x0E) puntatore di controllo thread non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1784">**TX_THREAD_ERROR** (0x0E) Invalid thread control pointer.</span></span> <span data-ttu-id="94e54-1785">Il puntatore è NULL o il thread è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1785">Either the pointer is NULL or the thread is already created.</span></span>
- <span data-ttu-id="94e54-1786">**TX_PTR_ERROR** (0x03) indirizzo iniziale non valido del punto di ingresso o l'area dello stack non è valida, in genere null.</span><span class="sxs-lookup"><span data-stu-id="94e54-1786">**TX_PTR_ERROR** (0x03) Invalid starting address of the entry point or the stack area is invalid, usually NULL.</span></span>
- <span data-ttu-id="94e54-1787">Le dimensioni **TX_SIZE_ERROR** (0x05) dell'area dello stack non sono valide.</span><span class="sxs-lookup"><span data-stu-id="94e54-1787">**TX_SIZE_ERROR** (0x05) Size of stack area is invalid.</span></span> <span data-ttu-id="94e54-1788">Per eseguire i thread è necessario almeno **TX_MINIMUM_STACK** byte.</span><span class="sxs-lookup"><span data-stu-id="94e54-1788">Threads must have at least **TX_MINIMUM_STACK** bytes to execute.</span></span>
- <span data-ttu-id="94e54-1789">**TX_PRIORITY_ERROR** (0x0F) priorità del thread non valida, che è un valore non compreso nell'intervallo di (da 0 a (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="94e54-1789">**TX_PRIORITY_ERROR** (0x0F) Invalid thread priority, which is a value outside the range of (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="94e54-1790">**TX_THRESH_ERROR** (0x18) Preemptionthreshold non valido specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1790">**TX_THRESH_ERROR** (0x18) Invalid preemptionthreshold specified.</span></span> <span data-ttu-id="94e54-1791">Questo valore deve essere una priorità valida minore o uguale alla priorità iniziale del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1791">This value must be a valid priority less than or equal to the initial priority of the thread.</span></span>
- <span data-ttu-id="94e54-1792">La selezione di avvio automatico **TX_START_ERROR** (0x10) non è valida.</span><span class="sxs-lookup"><span data-stu-id="94e54-1792">**TX_START_ERROR** (0x10) Invalid auto-start selection.</span></span>
- <span data-ttu-id="94e54-1793">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1793">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1794">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1794">Allowed From</span></span>

<span data-ttu-id="94e54-1795">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="94e54-1795">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1796">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1796">Preemption Possible</span></span>

<span data-ttu-id="94e54-1797">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-1797">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1798">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1798">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Create a thread of priority 15 whose entry point is
"my_thread_entry". This thread’s stack area is 1000
bytes in size, starting at address 0x400000. The
preemption-threshold is setup to allow preemption of threads
with priorities ranging from 0 through 14. Time-slicing is
disabled. This thread is automatically put into a ready
condition. */
status = tx_thread_create(&my_thread, "my_thread_name",
    my_thread_entry, 0x1234,
    (VOID *) 0x400000, 1000,
    15, 15, TX_NO_TIME_SLICE,
    TX_AUTO_START);

/* If status equals TX_SUCCESS, my_thread is ready
for execution! */

...

/* Thread’s entry function. When "my_thread" actually
begins execution, control is transferred to this
function. */

VOID my_thread_entry (ULONG initial_input)
{
    /* When we get here, the value of initial_input is
    0x1234. See how this was specified during
    creation. */
    /* The real work of the thread, including calls to
    other function should be called from here! */
    /* When this function returns, the corresponding
    thread is placed into a "completed" state. */
}
```

### <a name="see-also"></a><span data-ttu-id="94e54-1799">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1799">See Also</span></span>

- <span data-ttu-id="94e54-1800">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1800">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-1801">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1801">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-1802">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-1802">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-1803">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1803">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-1804">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1804">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-1805">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1805">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1806">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1806">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-1807">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1807">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-1808">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-1808">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-1809">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-1809">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-1810">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-1810">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-1811">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-1811">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-1812">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1812">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-1813">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-1813">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-1814">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-1814">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-1815">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1815">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-1816">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-1816">tx_thread_wait_abort</span></span>

## <a name="tx_thread_delete"></a><span data-ttu-id="94e54-1817">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1817">tx_thread_delete</span></span>

<span data-ttu-id="94e54-1818">Elimina thread applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-1818">Delete application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1819">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1819">Prototype</span></span>

```c
UINT tx_thread_delete(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-1820">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1820">Description</span></span>

<span data-ttu-id="94e54-1821">Questo servizio Elimina il thread dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1821">This service deletes the specified application thread.</span></span> <span data-ttu-id="94e54-1822">Poiché il thread specificato deve essere in uno stato terminato o completato, questo servizio non può essere chiamato da un thread che tenta di eliminare se stesso.</span><span class="sxs-lookup"><span data-stu-id="94e54-1822">Since the specified thread must be in a terminated or completed state, this service cannot be called from a thread attempting to delete itself.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1823">*È responsabilità dell'applicazione gestire l'area di memoria associata allo stack del thread, disponibile al termine del servizio. Inoltre, l'applicazione deve impedire l'utilizzo di un thread eliminato.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1823">*It is the application's responsibility to manage the memory area associated with the thread's stack, which is available after this service completes. In addition, the application must prevent use of a deleted thread.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1824">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1824">Parameters</span></span>

- <span data-ttu-id="94e54-1825">**thread_ptr** Puntatore a un thread dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1825">**thread_ptr** Pointer to a previously created application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1826">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1826">Return Values</span></span>

- <span data-ttu-id="94e54-1827">Eliminazione thread riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-1827">**TX_SUCCESS** (0x00) Successful thread deletion.</span></span>
- <span data-ttu-id="94e54-1828">**TX_THREAD_ERROR** (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1828">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="94e54-1829">Il thread specificato **TX_DELETE_ERROR** (0x11) non è in uno stato terminato o completato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1829">**TX_DELETE_ERROR** (0x11) Specified thread is not in a terminated or completed state.</span></span>
- <span data-ttu-id="94e54-1830">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-1830">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1831">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1831">Allowed From</span></span>

<span data-ttu-id="94e54-1832">Thread e timer</span><span class="sxs-lookup"><span data-stu-id="94e54-1832">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1833">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1833">Preemption Possible</span></span>

<span data-ttu-id="94e54-1834">No</span><span class="sxs-lookup"><span data-stu-id="94e54-1834">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1835">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1835">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Delete an application thread whose control block is
"my_thread". Assume that the thread has already been
created with a call to tx_thread_create. */
status = tx_thread_delete(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
deleted. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1836">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1836">See Also</span></span>

- <span data-ttu-id="94e54-1837">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1837">tx_thread_create</span></span>
- <span data-ttu-id="94e54-1838">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1838">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-1839">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-1839">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-1840">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1840">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-1841">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1841">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-1842">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1842">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1843">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1843">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-1844">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1844">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-1845">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-1845">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-1846">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-1846">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-1847">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-1847">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-1848">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-1848">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-1849">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1849">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-1850">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-1850">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-1851">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-1851">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-1852">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1852">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-1853">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-1853">tx_thread_wait_abort</span></span>

## <a name="tx_thread_entry_exit_notify"></a><span data-ttu-id="94e54-1854">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1854">tx_thread_entry_exit_notify</span></span>

<span data-ttu-id="94e54-1855">Invia notifica all'applicazione al thread</span><span class="sxs-lookup"><span data-stu-id="94e54-1855">Notify application upon thread entry and exit</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1856">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1856">Prototype</span></span>

```c
UINT tx_thread_entry_exit_notify(
    TX_THREAD *thread_ptr,
    VOID (*entry_exit_notify)(TX_THREAD *, UINT));
```

### <a name="description"></a><span data-ttu-id="94e54-1857">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1857">Description</span></span>

<span data-ttu-id="94e54-1858">Questo servizio registra una funzione di callback delle notifiche chiamata ogni volta che il thread specificato viene inserito o chiuso.</span><span class="sxs-lookup"><span data-stu-id="94e54-1858">This service registers a notification callback function that is called whenever the specified thread is entered or exits.</span></span> <span data-ttu-id="94e54-1859">L'elaborazione del callback di notifica viene definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1859">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1860">Il callback di notifica voce/uscita thread dell'applicazione non è autorizzato a chiamare alcuna API ThreadX con un'opzione di sospensione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1860">The application's thread entry/exit notification callback is not allowed to call any ThreadX API with a suspension option.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1861">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1861">Parameters</span></span>

- <span data-ttu-id="94e54-1862">**thread_ptr** Puntatore al thread creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1862">**thread_ptr** Pointer to previously created thread.</span></span>
- <span data-ttu-id="94e54-1863">**entry_exit_notify** Puntatore alla funzione di notifica di ingresso/uscita del thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1863">**entry_exit_notify** Pointer to application's thread entry/exit notification function.</span></span> <span data-ttu-id="94e54-1864">Il secondo parametro della funzione di notifica Entry/Exit indica se è presente una voce o una uscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-1864">The second parameter to the entry/exit notification function designates if an entry or exit is present.</span></span> <span data-ttu-id="94e54-1865">Il valore **TX_THREAD_ENTRY** (0x00) indica che è stato immesso il thread, mentre il valore **TX_THREAD_EXIT** (0x01) indica che il thread è stato terminato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1865">The value **TX_THREAD_ENTRY** (0x00) indicates the thread was entered, while the value **TX_THREAD_EXIT** (0x01) indicates the thread was exited.</span></span> <span data-ttu-id="94e54-1866">Se questo valore è **TX_NULL**, la notifica è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="94e54-1866">If this value is **TX_NULL**, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1867">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1867">Return Values</span></span>

- <span data-ttu-id="94e54-1868">**TX_SUCCESS** (0x00) registrazione riuscita della funzione di notifica di ingresso/uscita del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1868">**TX_SUCCESS** (0x00) Successful registration of the thread entry/exit notification function.</span></span>
- <span data-ttu-id="94e54-1869">**TX_THREAD_ERROR** (0x0E) puntatore al thread non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1869">**TX_THREAD_ERROR** (0x0E) Invalid thread pointer.</span></span>
- <span data-ttu-id="94e54-1870">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema è stato compilato con le funzionalità di notifica disabilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-1870">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1871">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1871">Allowed From</span></span>

<span data-ttu-id="94e54-1872">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1872">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1873">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1873">Example</span></span>

```c
TX_THREAD my_thread;
/* Register the "my_entry_exit_notify" function for monitoring
the entry/exit of the thread "my_thread." */
status = tx_thread_entry_exit_notify(&my_thread,
    my_entry_exit_notify);

/* If status is TX_SUCCESS the entry/exit notification function was
successfully registered. */
void my_entry_exit_notify(TX_THREAD *thread_ptr, UINT condition)
{
    /* Determine if the thread was entered or exited. */
    if (condition == TX_THREAD_ENTRY)
        /* Thread entry! */
    else if (condition == TX_THREAD_EXIT)
        /* Thread exit! */
}
```

### <a name="see-also"></a><span data-ttu-id="94e54-1874">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1874">See Also</span></span>

- <span data-ttu-id="94e54-1875">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1875">tx_thread_create</span></span>
- <span data-ttu-id="94e54-1876">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1876">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-1877">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1877">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-1878">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-1878">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-1879">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1879">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-1880">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1880">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-1881">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1881">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1882">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1882">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-1883">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1883">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-1884">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-1884">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-1885">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-1885">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-1886">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-1886">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-1887">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-1887">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-1888">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1888">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-1889">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-1889">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-1890">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-1890">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-1891">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1891">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-1892">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-1892">tx_thread_wait_abort</span></span>

## <a name="tx_thread_identify"></a><span data-ttu-id="94e54-1893">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-1893">tx_thread_identify</span></span>

<span data-ttu-id="94e54-1894">Recupera il puntatore al thread attualmente in esecuzione</span><span class="sxs-lookup"><span data-stu-id="94e54-1894">Retrieves pointer to currently executing thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1895">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1895">Prototype</span></span>

```c
TX_THREAD* tx_thread_identify(VOID);
```
### <a name="description"></a><span data-ttu-id="94e54-1896">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1896">Description</span></span>

<span data-ttu-id="94e54-1897">Questo servizio restituisce un puntatore al thread attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1897">This service returns a pointer to the currently executing thread.</span></span> <span data-ttu-id="94e54-1898">Se non è in esecuzione alcun thread, il servizio restituisce un puntatore null.</span><span class="sxs-lookup"><span data-stu-id="94e54-1898">If no thread is executing, this service returns a null pointer.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1899">*Se questo servizio viene chiamato da un ISR, il valore restituito rappresenta il thread in esecuzione prima del gestore di interrupt in esecuzione.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1899">*If this service is called from an ISR, the return value represents the thread running prior to the executing interrupt handler.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1900">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1900">Parameters</span></span>

<span data-ttu-id="94e54-1901">nessuno</span><span class="sxs-lookup"><span data-stu-id="94e54-1901">None</span></span>

### <a name="retuen-values"></a><span data-ttu-id="94e54-1902">Valori retuen</span><span class="sxs-lookup"><span data-stu-id="94e54-1902">Retuen Values</span></span>

- <span data-ttu-id="94e54-1903">**puntatore thread** Puntatore al thread attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="94e54-1903">**thread pointer** Pointer to the currently executing thread.</span></span> <span data-ttu-id="94e54-1904">Se non è in esecuzione alcun thread, il valore restituito è **TX_NULL**.</span><span class="sxs-lookup"><span data-stu-id="94e54-1904">If no thread is executing, the return value is **TX_NULL**.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1905">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1905">Allowed From</span></span>

<span data-ttu-id="94e54-1906">Thread e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1906">Threads and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1907">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1907">Preemption Possible</span></span>

<span data-ttu-id="94e54-1908">No</span><span class="sxs-lookup"><span data-stu-id="94e54-1908">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1909">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1909">Example</span></span>

<span data-ttu-id="94e54-1910">TX_THREAD \* my_thread_ptr;</span><span class="sxs-lookup"><span data-stu-id="94e54-1910">TX_THREAD \*my_thread_ptr;</span></span>

```c
TX_THREAD *my_thread_ptr;

/* Find out who we are! */
my_thread_ptr = tx_thread_identify();

/* If my_thread_ptr is non-null, we are currently executing
from that thread or an ISR that interrupted that thread.
Otherwise, this service was called
from an ISR when no thread was running when the
interrupt occurred. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1911">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1911">See Also</span></span>

- <span data-ttu-id="94e54-1912">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1912">tx_thread_create</span></span>
- <span data-ttu-id="94e54-1913">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1913">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-1914">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1914">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-1915">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1915">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-1916">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1916">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-1917">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1917">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1918">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1918">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-1919">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1919">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-1920">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-1920">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-1921">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-1921">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-1922">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-1922">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-1923">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-1923">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-1924">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1924">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-1925">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-1925">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-1926">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-1926">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-1927">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1927">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-1928">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-1928">tx_thread_wait_abort</span></span>

## <a name="tx_thread_info_get"></a><span data-ttu-id="94e54-1929">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1929">tx_thread_info_get</span></span>

<span data-ttu-id="94e54-1930">Recuperare informazioni sul thread</span><span class="sxs-lookup"><span data-stu-id="94e54-1930">Retrieve information about thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1931">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1931">Prototype</span></span>

```c
UINT tx_thread_info_get(
    TX_THREAD *thread_ptr, 
    CHAR **name,
    UINT *state, 
    ULONG *run_count,
    UINT *priority,
    UINT *preemption_threshold,
    ULONG *time_slice,
    TX_THREAD **next_thread,
    TX_THREAD **suspended_thread);
```

### <a name="description"></a><span data-ttu-id="94e54-1932">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1932">Description</span></span>

<span data-ttu-id="94e54-1933">Questo servizio recupera le informazioni sul thread specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1933">This service retrieves information about the specified thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1934">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1934">Parameters</span></span>
- <span data-ttu-id="94e54-1935">**thread_ptr** Puntatore al blocco di controllo thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1935">**thread_ptr** Pointer to thread control block.</span></span>
- <span data-ttu-id="94e54-1936">**nome** Puntatore alla destinazione per il puntatore al nome del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1936">**name** Pointer to destination for the pointer to the thread's name.</span></span>
- <span data-ttu-id="94e54-1937">**stato** di Puntatore alla destinazione per lo stato di esecuzione corrente del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1937">**state** Pointer to destination for the thread's current execution state.</span></span> <span data-ttu-id="94e54-1938">I valori possibili sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="94e54-1938">Possible values are as follows.</span></span>
    - <span data-ttu-id="94e54-1939">**TX_READY** (0x00)</span><span class="sxs-lookup"><span data-stu-id="94e54-1939">**TX_READY** (0x00)</span></span>
    - <span data-ttu-id="94e54-1940">**TX_COMPLETED** (0x01)</span><span class="sxs-lookup"><span data-stu-id="94e54-1940">**TX_COMPLETED** (0x01)</span></span>
    - <span data-ttu-id="94e54-1941">**TX_TERMINATED** (0x02)</span><span class="sxs-lookup"><span data-stu-id="94e54-1941">**TX_TERMINATED** (0x02)</span></span>
    - <span data-ttu-id="94e54-1942">**TX_SUSPENDED** (0x03)</span><span class="sxs-lookup"><span data-stu-id="94e54-1942">**TX_SUSPENDED** (0x03)</span></span>
    - <span data-ttu-id="94e54-1943">**TX_SLEEP** (0x04)</span><span class="sxs-lookup"><span data-stu-id="94e54-1943">**TX_SLEEP** (0x04)</span></span>
    - <span data-ttu-id="94e54-1944">**TX_QUEUE_SUSP** (0x05)</span><span class="sxs-lookup"><span data-stu-id="94e54-1944">**TX_QUEUE_SUSP** (0x05)</span></span>
    - <span data-ttu-id="94e54-1945">**TX_SEMAPHORE_SUSP** (0x06)</span><span class="sxs-lookup"><span data-stu-id="94e54-1945">**TX_SEMAPHORE_SUSP** (0x06)</span></span>
    - <span data-ttu-id="94e54-1946">**TX_EVENT_FLAG** (0x07)</span><span class="sxs-lookup"><span data-stu-id="94e54-1946">**TX_EVENT_FLAG** (0x07)</span></span>
    - <span data-ttu-id="94e54-1947">**TX_BLOCK_MEMORY** (0x08)</span><span class="sxs-lookup"><span data-stu-id="94e54-1947">**TX_BLOCK_MEMORY** (0x08)</span></span>
    - <span data-ttu-id="94e54-1948">**TX_BYTE_MEMORY** (0x09)</span><span class="sxs-lookup"><span data-stu-id="94e54-1948">**TX_BYTE_MEMORY** (0x09)</span></span>
    - <span data-ttu-id="94e54-1949">**TX_MUTEX_SUSP** (0x0D)</span><span class="sxs-lookup"><span data-stu-id="94e54-1949">**TX_MUTEX_SUSP** (0x0D)</span></span>  

- <span data-ttu-id="94e54-1950">**run_count** Puntatore alla destinazione per il conteggio delle esecuzioni del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1950">**run_count** Pointer to destination for the thread's run count.</span></span>
- <span data-ttu-id="94e54-1951">**priorità** di Puntatore alla destinazione per la priorità del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1951">**priority** Pointer to destination for the thread's priority.</span></span>
- <span data-ttu-id="94e54-1952">**preemption_threshold** Puntatore alla destinazione per la soglia di precedenza del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1952">**preemption_threshold** Pointer to destination for the thread's preemption-threshold.</span></span>
<span data-ttu-id="94e54-1953">**time_slice** Puntatore alla destinazione per la sezione del tempo del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1953">**time_slice** Pointer to destination for the thread's time-slice.</span></span>
<span data-ttu-id="94e54-1954">**next_thread** Puntatore alla destinazione per il puntatore al thread creato successivo.</span><span class="sxs-lookup"><span data-stu-id="94e54-1954">**next_thread** Pointer to destination for next created thread pointer.</span></span>

<span data-ttu-id="94e54-1955">**suspended_thread** Puntatore alla destinazione per il puntatore al thread successivo nell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="94e54-1955">**suspended_thread** Pointer to destination for pointer to next thread in suspension list.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-1956">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-1956">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-1957">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-1957">Return Values</span></span>

- <span data-ttu-id="94e54-1958">Il recupero delle informazioni sul thread riuscito **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-1958">**TX_SUCCESS** (0x00) Successful thread information retrieval.</span></span>
- <span data-ttu-id="94e54-1959">**TX_THREAD_ERROR** (0x0E) puntatore di controllo thread non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-1959">**TX_THREAD_ERROR** (0x0E) Invalid thread control pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-1960">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-1960">Allowed From</span></span>

<span data-ttu-id="94e54-1961">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-1961">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-1962">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-1962">Preemption Possible</span></span>

<span data-ttu-id="94e54-1963">No</span><span class="sxs-lookup"><span data-stu-id="94e54-1963">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-1964">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-1964">Example</span></span>

```c
TX_THREAD my_thread;
CHAR *name;
UINT state;
ULONG run_count;
UINT priority;
UINT preemption_threshold;
UINT time_slice;
TX_THREAD *next_thread;
TX_THREAD *suspended_thread;
UINT status;

/* Retrieve information about the previously created
thread "my_thread." */

status = tx_thread_info_get(&my_thread, &name,
    &state, &run_count,
    &priority, &preemption_threshold,
    &time_slice, &next_thread,&suspended_thread);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-1965">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-1965">See Also</span></span>

- <span data-ttu-id="94e54-1966">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-1966">tx_thread_create</span></span>
- <span data-ttu-id="94e54-1967">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-1967">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-1968">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1968">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-1969">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-1969">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-1970">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1970">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-1971">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1971">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-1972">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1972">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-1973">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1973">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-1974">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-1974">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-1975">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-1975">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-1976">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-1976">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-1977">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-1977">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-1978">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-1978">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-1979">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-1979">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-1980">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-1980">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-1981">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-1981">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-1982">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-1982">tx_thread_wait_abort</span></span>

## <a name="tx_thread_performance_info_get"></a><span data-ttu-id="94e54-1983">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-1983">tx_thread_performance_info_get</span></span>

<span data-ttu-id="94e54-1984">Ottenere informazioni sulle prestazioni del thread</span><span class="sxs-lookup"><span data-stu-id="94e54-1984">Get thread performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-1985">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-1985">Prototype</span></span>

```c
UINT tx_thread_performance_info_get(
    TX_THREAD *thread_ptr,
    LONG *resumptions, 
    ULONG *suspensions,
    ULONG *solicited_preemptions, 
    ULONG *interrupt_preemptions,
    ULONG *priority_inversions, 
    ULONG *time_slices,
    ULONG *relinquishes, 
    ULONG *timeouts, 
    ULONG *wait_aborts,
    TX_THREAD **last_preempted_by);
```

### <a name="description"></a><span data-ttu-id="94e54-1986">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-1986">Description</span></span>

<span data-ttu-id="94e54-1987">Questo servizio recupera le informazioni sulle prestazioni relative al thread specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-1987">This service retrieves performance information about the specified thread.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-1988">*La libreria e l'applicazione threadX devono essere compilate con*  \* **TX_THREAD_ENABLE_PERFORMANCE_INFO** _ _defined affinché il servizio restituisca informazioni sulle prestazioni. \*</span><span class="sxs-lookup"><span data-stu-id="94e54-1988">*The ThreadX library and application must be built with* ***TX_THREAD_ENABLE_PERFORMANCE_INFO** _ _defined in order for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-1989">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-1989">Parameters</span></span>
- <span data-ttu-id="94e54-1990">**thread_ptr** Puntatore al thread creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-1990">**thread_ptr** Pointer to previously created thread.</span></span>
- <span data-ttu-id="94e54-1991">**riprese** Puntatore alla destinazione per il numero di ririprese del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1991">**resumptions** Pointer to destination for the number of resumptions of this thread.</span></span>
- <span data-ttu-id="94e54-1992">**sospensioni** Puntatore alla destinazione per il numero di sospensioni del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1992">**suspensions** Pointer to destination for the number of suspensions of this thread.</span></span>
- <span data-ttu-id="94e54-1993">**solicited_preemptions** Puntatore alla destinazione per il numero di prelazioni in seguito a una chiamata al servizio API ThreadX eseguita da questo thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1993">**solicited_preemptions** Pointer to destination for the number of preemptions as a result of a ThreadX API service call made by this thread.</span></span>
- <span data-ttu-id="94e54-1994">**interrupt_preemptions** Puntatore alla destinazione per il numero di prelazioni di questo thread come risultato dell'elaborazione di interrupt.</span><span class="sxs-lookup"><span data-stu-id="94e54-1994">**interrupt_preemptions** Pointer to destination for the number of preemptions of this thread as a result of interrupt processing.</span></span>
- <span data-ttu-id="94e54-1995">**priority_inversions** Puntatore alla destinazione per il numero di inversioni di priorità del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1995">**priority_inversions** Pointer to destination for the number of priority inversions of this thread.</span></span>
- <span data-ttu-id="94e54-1996">**time_slices** Puntatore alla destinazione per il numero di sezioni temporali del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1996">**time_slices** Pointer to destination for the number of time-slices of this thread.</span></span>
- <span data-ttu-id="94e54-1997">**cede** Puntatore alla destinazione per il numero di thread abbandonati eseguiti dal thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1997">**relinquishes** Pointer to destination for the number of thread relinquishes performed by this thread.</span></span>
- <span data-ttu-id="94e54-1998">**timeout** Puntatore alla destinazione per il numero di timeout di sospensione in questo thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1998">**timeouts** Pointer to destination for the number of suspension timeouts on this thread.</span></span>
- <span data-ttu-id="94e54-1999">**wait_aborts** Puntatore alla destinazione per il numero di interruzioni di attesa eseguite sul thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-1999">**wait_aborts** Pointer to destination for the number of wait aborts performed on this thread.</span></span>
- <span data-ttu-id="94e54-2000">**last_preempted_by** Puntatore alla destinazione per il puntatore del thread che ha superato l'ultima volta il thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-2000">**last_preempted_by** Pointer to destination for the thread pointer that last preempted this thread.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2001">*La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2001">*Supplying a TX_NULL for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2002">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2002">Return Values</span></span>

- <span data-ttu-id="94e54-2003">**TX_SUCCESS** (0x00) ottenere prestazioni thread riuscite.</span><span class="sxs-lookup"><span data-stu-id="94e54-2003">**TX_SUCCESS** (0x00) Successful thread performance get.</span></span>
- <span data-ttu-id="94e54-2004">**TX_PTR_ERROR** (0x03) puntatore al thread non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2004">**TX_PTR_ERROR** (0x03) Invalid thread pointer.</span></span>
- <span data-ttu-id="94e54-2005">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-2005">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2006">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2006">Allowed From</span></span>

<span data-ttu-id="94e54-2007">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2007">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2008">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2008">Example</span></span>

```c
TX_THREAD my_thread;
ULONG resumptions;
ULONG suspensions;
ULONG solicited_preemptions;
ULONG interrupt_preemptions;
ULONG priority_inversions;
ULONG time_slices;
ULONG relinquishes;
ULONG timeouts;
ULONG wait_aborts;
TX_THREAD *last_preempted_by;

/* Retrieve performance information on the previously created
thread. */

status = tx_thread_performance_info_get(&my_thread, &resumptions,
    &suspensions,
    &solicited_preemptions, &interrupt_preemptions,
    &priority_inversions, &time_slices,
    &relinquishes, &timeouts,
    &wait_aborts, &last_preempted_by);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2009">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2009">See Also</span></span>

- <span data-ttu-id="94e54-2010">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2010">tx_thread_create</span></span>
- <span data-ttu-id="94e54-2011">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2011">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2012">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2012">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2013">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2013">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2014">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2014">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2015">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2015">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-2016">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2016">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2017">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2017">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2018">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2018">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2019">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2019">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2020">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2020">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2021">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2021">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2022">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2022">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2023">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2023">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2024">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2024">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2025">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2025">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-2026">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2026">tx_thread_wait_abort</span></span>

## <a name="tx_thread_performance_system_info_get"></a><span data-ttu-id="94e54-2027">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2027">tx_thread_performance_system_info_get</span></span>

<span data-ttu-id="94e54-2028">Ottenere informazioni sulle prestazioni del sistema di thread</span><span class="sxs-lookup"><span data-stu-id="94e54-2028">Get thread system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2029">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2029">Prototype</span></span>

```c
UINT tx_thread_performance_system_info_get(
    ULONG *resumptions,
    ULONG *suspensions, 
    ULONG *solicited_preemptions,
    ULONG *interrupt_preemptions, 
    ULONG *priority_inversions,
    ULONG *time_slices, 
    ULONG *relinquishes, 
    ULONG *timeouts,
    ULONG *wait_aborts, 
    ULONG *non_idle_returns,
    ULONG *idle_returns);
```

### <a name="description"></a><span data-ttu-id="94e54-2030">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2030">Description</span></span>

<span data-ttu-id="94e54-2031">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i thread nel sistema.</span><span class="sxs-lookup"><span data-stu-id="94e54-2031">This service retrieves performance information about all the threads in the system.</span></span>

<span data-ttu-id="94e54-2032">*La libreria e l'applicazione ThreadX devono essere compilate con*</span><span class="sxs-lookup"><span data-stu-id="94e54-2032">*The ThreadX library and application must be built with*</span></span>

<span data-ttu-id="94e54-2033">\***TX_THREAD_ENABLE_PERFORMANCE_INFO** _ _defined affinché il servizio restituisca informazioni sulle prestazioni. \*</span><span class="sxs-lookup"><span data-stu-id="94e54-2033">***TX_THREAD_ENABLE_PERFORMANCE_INFO** _ _defined in order for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2034">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2034">Parameters</span></span>

- <span data-ttu-id="94e54-2035">**riprese** Puntatore alla destinazione per il numero totale di riprese dei thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-2035">**resumptions** Pointer to destination for the total number of thread resumptions.</span></span>
- <span data-ttu-id="94e54-2036">**sospensioni** Puntatore alla destinazione per il numero totale di sospensioni dei thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-2036">**suspensions** Pointer to destination for the total number of thread suspensions.</span></span>
- <span data-ttu-id="94e54-2037">**solicited_preemptions** Puntatore alla destinazione per il numero totale di thread di precedenza in seguito a un thread che chiama un servizio API ThreadX.</span><span class="sxs-lookup"><span data-stu-id="94e54-2037">**solicited_preemptions** Pointer to destination for the total number of thread preemptions as a result of a thread calling a ThreadX API service.</span></span>
- <span data-ttu-id="94e54-2038">**interrupt_preemptions** Puntatore alla destinazione per il numero totale di interruzioni di thread in seguito all'elaborazione di interrupt.</span><span class="sxs-lookup"><span data-stu-id="94e54-2038">**interrupt_preemptions** Pointer to destination for the total number of thread preemptions as a result of interrupt processing.</span></span>
- <span data-ttu-id="94e54-2039">**priority_inversions** Puntatore alla destinazione per il numero totale di inversioni di priorità dei thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-2039">**priority_inversions** Pointer to destination for the total number of thread priority inversions.</span></span>
- <span data-ttu-id="94e54-2040">**time_slices** Puntatore alla destinazione per il numero totale di intervalli di tempo dei thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-2040">**time_slices** Pointer to destination for the total number of thread time-slices.</span></span>
- <span data-ttu-id="94e54-2041">**cede** Puntatore alla destinazione per il numero totale di thread abbandonati.</span><span class="sxs-lookup"><span data-stu-id="94e54-2041">**relinquishes** Pointer to destination for the total number of thread relinquishes.</span></span>
- <span data-ttu-id="94e54-2042">**timeout** Puntatore alla destinazione per il numero totale di timeout di sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-2042">**timeouts** Pointer to destination for the total number of thread suspension timeouts.</span></span>
- <span data-ttu-id="94e54-2043">**wait_aborts** Puntatore alla destinazione per il numero totale di interruzioni di attesa del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-2043">**wait_aborts** Pointer to destination for the total number of thread wait aborts.</span></span>
- <span data-ttu-id="94e54-2044">**non_idle_returns** Puntatore alla destinazione per il numero di volte in cui un thread torna al sistema quando un altro thread è pronto per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="94e54-2044">**non_idle_returns** Pointer to destination for the number of times a thread returns to the system when another thread is ready to execute.</span></span>
- <span data-ttu-id="94e54-2045">**idle_returns** Puntatore alla destinazione per il numero di volte in cui un thread torna al sistema quando nessun altro thread è pronto per l'esecuzione (sistema inattivo).</span><span class="sxs-lookup"><span data-stu-id="94e54-2045">**idle_returns** Pointer to destination for the number of times a thread returns to the system when no other thread is ready to execute (idle system).</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2046">*La specifica di un **TX_NULL** per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2046">*Supplying a **TX_NULL** for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2047">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2047">Return Values</span></span>

- <span data-ttu-id="94e54-2048">**TX_SUCCESS** (0x00) prestazioni del sistema thread riuscite.</span><span class="sxs-lookup"><span data-stu-id="94e54-2048">**TX_SUCCESS** (0x00) Successful thread system performance get.</span></span>
- <span data-ttu-id="94e54-2049">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-2049">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2050">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2050">Allowed From</span></span>

<span data-ttu-id="94e54-2051">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2051">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2052">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2052">Example</span></span>

```c
ULONG resumptions;
ULONG suspensions;
ULONG solicited_preemptions;
ULONG interrupt_preemptions;
ULONG priority_inversions;
ULONG time_slices;
ULONG relinquishes;
ULONG timeouts;
ULONG wait_aborts;
ULONG non_idle_returns;
ULONG idle_returns;

/* Retrieve performance information on all previously created
thread. */

status = tx_thread_performance_system_info_get(&resumptions,
    &suspensions,
    &solicited_preemptions, &interrupt_preemptions,
    &priority_inversions, &time_slices, &relinquishes,
    &timeouts, &wait_aborts, &non_idle_returns,
    &idle_returns);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2053">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2053">See Also</span></span>

- <span data-ttu-id="94e54-2054">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2054">tx_thread_create</span></span>
- <span data-ttu-id="94e54-2055">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2055">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2056">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2056">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2057">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2057">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2058">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2058">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2059">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2059">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2060">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2060">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2061">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2061">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2062">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2062">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2063">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2063">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2064">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2064">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2065">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2065">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2066">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2066">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2067">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2067">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2068">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2068">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2069">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2069">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-2070">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2070">tx_thread_wait_abort</span></span>

## <a name="tx_thread_preemption_change"></a><span data-ttu-id="94e54-2071">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2071">tx_thread_preemption_change</span></span>

<span data-ttu-id="94e54-2072">Modifica precedenza-soglia del thread dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2072">Change preemption-threshold of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2073">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2073">Prototype</span></span>

```c
UINT tx_thread_preemption_change(
    TX_THREAD *thread_ptr,
    UINT new_threshold, 
    UINT *old_threshold);
```

### <a name="description"></a><span data-ttu-id="94e54-2074">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2074">Description</span></span>

<span data-ttu-id="94e54-2075">Questo servizio modifica la soglia di precedenza del thread specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2075">This service changes the preemption-threshold of the specified thread.</span></span> <span data-ttu-id="94e54-2076">La soglia di precedenza impedisce al thread specificato di essere uguale o inferiore al valore della soglia di precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-2076">The preemption-threshold prevents preemption of the specified thread by threads equal to or less than the preemption-threshold value.</span></span>

>[!NOTE]
> <span data-ttu-id="94e54-2077">*Con la soglia di precedenza viene disabilitato il sezionamento del tempo per il thread specificato.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2077">*Using preemption-threshold disables time-slicing for the specified thread.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2078">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2078">Parameters</span></span>
- <span data-ttu-id="94e54-2079">**thread_ptr** Puntatore a un thread dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-2079">**thread_ptr** Pointer to a previously created application thread.</span></span>
- <span data-ttu-id="94e54-2080">**new_threshold** Nuovo livello di priorità per la soglia di precedenza (da 0 a (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="94e54-2080">**new_threshold** New preemption-threshold priority level (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="94e54-2081">**old_threshold** Puntatore a una posizione per restituire la soglia di precedenza precedente.</span><span class="sxs-lookup"><span data-stu-id="94e54-2081">**old_threshold** Pointer to a location to return the previous preemption-threshold.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2082">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2082">Return Values</span></span>

- <span data-ttu-id="94e54-2083">Modifica della soglia di precedenza **TX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-2083">**TX_SUCCESS** (0x00) Successful preemption-threshold change.</span></span>
- <span data-ttu-id="94e54-2084">**TX_THREAD_ERROR** (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2084">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="94e54-2085">**TX_THRESH_ERROR** (0x18) specificata la nuova soglia di precedenza non è una priorità di thread valida (un valore diverso da (da 0 a (**TX_MAX_PRIORITIES**-1)) o è maggiore di (priorità inferiore) rispetto alla priorità del thread corrente.</span><span class="sxs-lookup"><span data-stu-id="94e54-2085">**TX_THRESH_ERROR** (0x18) Specified new preemption-threshold is not a valid thread priority (a value other than (0 through (**TX_MAX_PRIORITIES**-1)) or is greater than (lower priority) than the current thread priority.</span></span>
- <span data-ttu-id="94e54-2086">**TX_PTR_ERROR** (0x03) puntatore non valido al percorso di archiviazione preemptionthreshold precedente.</span><span class="sxs-lookup"><span data-stu-id="94e54-2086">**TX_PTR_ERROR** (0x03) Invalid pointer to previous preemptionthreshold storage location.</span></span>
- <span data-ttu-id="94e54-2087">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-2087">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2088">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2088">Allowed From</span></span>

<span data-ttu-id="94e54-2089">Thread e timer</span><span class="sxs-lookup"><span data-stu-id="94e54-2089">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2090">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2090">Preemption Possible</span></span>

<span data-ttu-id="94e54-2091">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-2091">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2092">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2092">Example</span></span>

```c
TX_THREAD my_thread;
UINT my_old_threshold;
UINT status;

/* Disable all preemption of the specified thread. The
current preemption-threshold is returned in
"my_old_threshold". Assume that "my_thread" has
already been created. */

status = tx_thread_preemption_change(&my_thread,
    0, &my_old_threshold);

/* If status equals TX_SUCCESS, the application thread is
non-preemptable by another thread. Note that ISRs are
not prevented by preemption disabling. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2093">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2093">See Also</span></span>

- <span data-ttu-id="94e54-2094">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2094">tx_thread_create</span></span>
- <span data-ttu-id="94e54-2095">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2095">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2096">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2096">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2097">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2097">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2098">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2098">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2099">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2099">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2100">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2100">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-2101">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2101">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2102">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2102">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2103">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2103">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2104">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2104">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2105">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2105">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2106">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2106">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2107">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2107">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2108">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2108">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2109">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2109">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-2110">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2110">tx_thread_wait_abort</span></span>

## <a name="tx_thread_priority_change"></a><span data-ttu-id="94e54-2111">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2111">tx_thread_priority_change</span></span>

<span data-ttu-id="94e54-2112">Modificare la priorità del thread dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2112">Change priority of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2113">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2113">Prototype</span></span>

```c
UINT tx_thread_priority_change(
    TX_THREAD *thread_ptr,
    UINT new_priority, 
    UINT *old_priority);
```

### <a name="description"></a><span data-ttu-id="94e54-2114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2114">Description</span></span>

<span data-ttu-id="94e54-2115">Questo servizio modifica la priorità del thread specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2115">This service changes the priority of the specified thread.</span></span> <span data-ttu-id="94e54-2116">Le priorità valide sono comprese tra 0 e (TX_MAX_PRIORITES-1), dove 0 rappresenta il livello di priorità più alto.</span><span class="sxs-lookup"><span data-stu-id="94e54-2116">Valid priorities range from 0 through (TX_MAX_PRIORITES-1), where 0 represents the highest priority level.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-2117">\* La soglia di precedenza del thread specificato viene impostata automaticamente sulla nuova priorità.</span><span class="sxs-lookup"><span data-stu-id="94e54-2117">\*The preemption-threshold of the specified thread is automatically set to the new priority.</span></span> <span data-ttu-id="94e54-2118">Se si desidera una nuova soglia, è necessario utilizzare il servizio \***tx_thread_preemption_change** _ dopo questa call._</span><span class="sxs-lookup"><span data-stu-id="94e54-2118">If a new threshold is desired, the \***tx_thread_preemption_change** _ service must be used after this call._</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2119">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2119">Parameters</span></span>

- <span data-ttu-id="94e54-2120">**thread_ptr** Puntatore a un thread dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-2120">**thread_ptr** Pointer to a previously created application thread.</span></span>
- <span data-ttu-id="94e54-2121">**new_priority** Nuovo livello di priorità dei thread (da 0 a (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="94e54-2121">**new_priority** New thread priority level (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="94e54-2122">**old_priority** Puntatore a una posizione per restituire la priorità precedente del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-2122">**old_priority** Pointer to a location to return the thread's previous priority.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2123">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2123">Return Values</span></span>

- <span data-ttu-id="94e54-2124">**TX_SUCCESS** (0x00) la modifica della priorità è riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-2124">**TX_SUCCESS** (0x00) Successful priority change.</span></span>
- <span data-ttu-id="94e54-2125">**TX_THREAD_ERROR** (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2125">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="94e54-2126">**TX_PRIORITY_ERROR** (0X0F) specifica la nuova priorità non è valida (un valore diverso da (da 0 a (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="94e54-2126">**TX_PRIORITY_ERROR** (0x0F) Specified new priority is not valid (a value other than (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="94e54-2127">**TX_PTR_ERROR** (0x03) puntatore non valido al percorso di archiviazione con priorità precedente.</span><span class="sxs-lookup"><span data-stu-id="94e54-2127">**TX_PTR_ERROR** (0x03) Invalid pointer to previous priority storage location.</span></span>
- <span data-ttu-id="94e54-2128">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-2128">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2129">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2129">Allowed From</span></span>

<span data-ttu-id="94e54-2130">Thread e timer</span><span class="sxs-lookup"><span data-stu-id="94e54-2130">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2131">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2131">Preemption Possible</span></span>

<span data-ttu-id="94e54-2132">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-2132">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2133">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2133">Example</span></span>

```c
TX_THREAD my_thread;
UINT my_old_priority;
UINT status;

/* Change the thread represented by "my_thread" to priority
0. */

status = tx_thread_priority_change(&my_thread,
    0, &my_old_priority);

/* If status equals TX_SUCCESS, the application thread is
now at the highest priority level in the system. */
```
### <a name="see-also"></a><span data-ttu-id="94e54-2134">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2134">See Also</span></span>

- <span data-ttu-id="94e54-2135">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2135">tx_thread_create</span></span>
- <span data-ttu-id="94e54-2136">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2136">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2137">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2137">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2138">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2138">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2139">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2139">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2140">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2140">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2141">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2141">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-2142">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2142">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2143">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2143">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2144">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2144">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2145">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2145">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2146">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2146">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2147">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2147">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2148">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2148">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2149">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2149">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2150">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2150">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-2151">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2151">tx_thread_wait_abort</span></span>

## <a name="tx_thread_relinquish"></a><span data-ttu-id="94e54-2152">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2152">tx_thread_relinquish</span></span>

<span data-ttu-id="94e54-2153">Cede il controllo ad altri thread dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2153">Relinquish control to other application threads</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2154">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2154">Prototype</span></span>

```c
VOID tx_thread_relinquish(VOID);
```

### <a name="description"></a><span data-ttu-id="94e54-2155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2155">Description</span></span>

<span data-ttu-id="94e54-2156">Questo servizio cede il controllo del processore ad altri thread pronti per l'esecuzione con la stessa priorità o con una priorità più alta.</span><span class="sxs-lookup"><span data-stu-id="94e54-2156">This service relinquishes processor control to other ready-to-run threads at the same or higher priority.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2157">*Oltre a cedere il controllo ai thread con la stessa priorità, questo servizio rilascia anche il controllo al thread con priorità più elevata impedito dall'esecuzione a causa dell'impostazione della soglia di precedenza del thread corrente.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2157">*In addition to relinquishing control to threads of the same priority, this service also relinquishes control to the highest-priority thread prevented from execution because of the current thread's preemption-threshold setting.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2158">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2158">Parameters</span></span>

<span data-ttu-id="94e54-2159">nessuno</span><span class="sxs-lookup"><span data-stu-id="94e54-2159">None</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2160">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2160">Return Values</span></span>

<span data-ttu-id="94e54-2161">nessuno</span><span class="sxs-lookup"><span data-stu-id="94e54-2161">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2162">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2162">Allowed From</span></span>

<span data-ttu-id="94e54-2163">Thread</span><span class="sxs-lookup"><span data-stu-id="94e54-2163">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2164">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2164">Preemption Possible</span></span>

<span data-ttu-id="94e54-2165">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-2165">Yes</span></span>

### <a name="examples"></a><span data-ttu-id="94e54-2166">Esempi</span><span class="sxs-lookup"><span data-stu-id="94e54-2166">Examples</span></span>

```c
ULONG run_counter_1 = 0;
ULONG run_counter_2 = 0;

/* Example of two threads relinquishing control to
each other in an infinite loop. Assume that
both of these threads are ready and have the same
priority. The run counters will always stay within one
of each other. */

VOID my_first_thread(ULONG thread_input)
{
    /* Endless loop of relinquish. */
    while(1)
    {
        /* Increment the run counter. */
        run_counter_1++;

        /* Relinquish control to other thread. */
        tx_thread_relinquish();
    }
}

VOID my_second_thread(ULONG thread_input)
{

    /* Endless loop of relinquish. */
    while(1)
    {
        /* Increment the run counter. */
        run_counter_2++;

        /* Relinquish control to other thread. */
        tx_thread_relinquish();
    }
}
```

### <a name="see-also"></a><span data-ttu-id="94e54-2167">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2167">See Also</span></span>

- <span data-ttu-id="94e54-2168">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2168">tx_thread_create</span></span>
- <span data-ttu-id="94e54-2169">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2169">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2170">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2170">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2171">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2171">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2172">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2172">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2173">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2173">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2174">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2174">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-2175">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2175">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2176">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2176">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2177">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2177">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2178">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2178">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2179">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2179">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2180">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2180">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2181">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2181">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2182">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2182">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2183">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2183">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-2184">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2184">tx_thread_wait_abort</span></span>

## <a name="tx_thread_reset"></a><span data-ttu-id="94e54-2185">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2185">tx_thread_reset</span></span>

<span data-ttu-id="94e54-2186">Reimposta thread</span><span class="sxs-lookup"><span data-stu-id="94e54-2186">Reset thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2187">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2187">Prototype</span></span>

```c
UINT tx_thread_reset(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-2188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2188">Description</span></span>

<span data-ttu-id="94e54-2189">Questo servizio Reimposta il thread specificato per l'esecuzione nel punto di ingresso definito al momento della creazione del thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-2189">This service resets the specified thread to execute at the entry point defined at thread creation.</span></span> <span data-ttu-id="94e54-2190">Il thread deve essere in uno stato **TX_COMPLETED** o **TX_TERMINATED** perché venga reimpostato</span><span class="sxs-lookup"><span data-stu-id="94e54-2190">The thread must be in either a **TX_COMPLETED** or **TX_TERMINATED** state for it to be reset</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-2191">*Per eseguire nuovamente il thread, è necessario riprenderlo.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2191">*The thread must be resumed for it to execute again.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2192">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2192">Parameters</span></span>

- <span data-ttu-id="94e54-2193">**thread_ptr** Puntatore a un thread creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-2193">**thread_ptr** Pointer to a previously created thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2194">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2194">Return Values</span></span>

- <span data-ttu-id="94e54-2195">Reimpostazione thread riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-2195">**TX_SUCCESS** (0x00) Successful thread reset.</span></span>
- <span data-ttu-id="94e54-2196">Il thread specificato **TX_NOT_DONE** (0x20) non è in uno stato **TX_COMPLETED** o **TX_TERMINATED** .</span><span class="sxs-lookup"><span data-stu-id="94e54-2196">**TX_NOT_DONE** (0x20) Specified thread is not in a **TX_COMPLETED** or **TX_TERMINATED** state.</span></span>
- <span data-ttu-id="94e54-2197">**TX_THREAD_ERROR** (0x0E) puntatore al thread non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2197">**TX_THREAD_ERROR** (0x0E) Invalid thread pointer.</span></span>
- <span data-ttu-id="94e54-2198">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-2198">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2199">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2199">Allowed From</span></span>

<span data-ttu-id="94e54-2200">Thread</span><span class="sxs-lookup"><span data-stu-id="94e54-2200">Threads</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2201">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2201">Example</span></span>

<span data-ttu-id="94e54-2202">TX_THREAD my_thread;</span><span class="sxs-lookup"><span data-stu-id="94e54-2202">TX_THREAD my_thread;</span></span>

```c
TX_THREAD my_thread;

/* Reset the previously created thread "my_thread." */

status = tx_thread_reset(&my_thread);

/* If status is TX_SUCCESS the thread is reset. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2203">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2203">See Also</span></span>

- <span data-ttu-id="94e54-2204">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2204">tx_thread_create</span></span>
- <span data-ttu-id="94e54-2205">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2205">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2206">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2206">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2207">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2207">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2208">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2208">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2209">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2209">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2210">tx_thread_preformance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2210">tx_thread_preformance_system_info_get</span></span>
- <span data-ttu-id="94e54-2211">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2211">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2212">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2212">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2213">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2213">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2214">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2214">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2215">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2215">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2216">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2216">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2217">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2217">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2218">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2218">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2219">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2219">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-2220">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2220">tx_thread_wait_abort</span></span>

## <a name="tx_thread_resume"></a><span data-ttu-id="94e54-2221">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2221">tx_thread_resume</span></span>

<span data-ttu-id="94e54-2222">Riavvia thread dell'applicazione sospesa</span><span class="sxs-lookup"><span data-stu-id="94e54-2222">Resume suspended application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2223">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2223">Prototype</span></span>

```c
UINT tx_thread_resume(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-2224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2224">Description</span></span>

<span data-ttu-id="94e54-2225">Questo servizio riprende o prepara l'esecuzione di un thread sospeso in precedenza da una chiamata ***tx_thread_suspend*** .</span><span class="sxs-lookup"><span data-stu-id="94e54-2225">This service resumes or prepares for execution a thread that was previously suspended by a ***tx_thread_suspend*** call.</span></span> <span data-ttu-id="94e54-2226">Inoltre, questo servizio riprende i thread creati senza avvio automatico.</span><span class="sxs-lookup"><span data-stu-id="94e54-2226">In addition, this service resumes threads that were created without an automatic start.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2227">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2227">Parameters</span></span>

- <span data-ttu-id="94e54-2228">**thread_ptr** Puntatore a un thread dell'applicazione sospesa.</span><span class="sxs-lookup"><span data-stu-id="94e54-2228">**thread_ptr** Pointer to a suspended application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2229">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2229">Return Values</span></span>

- <span data-ttu-id="94e54-2230">Riattivazione del thread **TX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-2230">**TX_SUCCESS** (0x00) Successful thread resume.</span></span>
- <span data-ttu-id="94e54-2231">La **TX_SUSPEND_LIFTED** (0X19) precedentemente impostata per la sospensione ritardata è stata revocata.</span><span class="sxs-lookup"><span data-stu-id="94e54-2231">**TX_SUSPEND_LIFTED** (0x19) Previously set delayed suspension was lifted.</span></span>
- <span data-ttu-id="94e54-2232">**TX_THREAD_ERROR** (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2232">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="94e54-2233">Il thread specificato **TX_RESUME_ERROR** (0x12) non è sospeso o è stato precedentemente sospeso da un servizio diverso da **_tx_thread_suspend_**.</span><span class="sxs-lookup"><span data-stu-id="94e54-2233">**TX_RESUME_ERROR** (0x12) Specified thread is not suspended or was previously suspended by a service other than **_tx_thread_suspend_**.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2234">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2234">Allowed From</span></span>

<span data-ttu-id="94e54-2235">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2235">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2236">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2236">Preemption Possible</span></span>

<span data-ttu-id="94e54-2237">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-2237">Yes</span></span>

<span data-ttu-id="94e54-2238">TX_THREAD my_thread;</span><span class="sxs-lookup"><span data-stu-id="94e54-2238">TX_THREAD my_thread;</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2239">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2239">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Resume the thread represented by "my_thread". */
status = tx_thread_resume(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
now ready to execute. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2240">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2240">See Also</span></span>

- <span data-ttu-id="94e54-2241">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2241">tx_thread_create</span></span>
- <span data-ttu-id="94e54-2242">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2242">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2243">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2243">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2244">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2244">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2245">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2245">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2246">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2246">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2247">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2247">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-2248">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2248">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2249">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2249">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2250">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2250">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2251">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2251">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2252">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2252">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2253">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2253">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2254">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2254">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2255">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2255">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2256">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2256">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-2257">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2257">tx_thread_wait_abort</span></span>

## <a name="tx_thread_sleep"></a><span data-ttu-id="94e54-2258">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2258">tx_thread_sleep</span></span>

<span data-ttu-id="94e54-2259">Sospende il thread corrente per l'ora specificata</span><span class="sxs-lookup"><span data-stu-id="94e54-2259">Suspend current thread for specified time</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2260">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2260">Prototype</span></span>

```c
UINT tx_thread_sleep(ULONG timer_ticks);
```

### <a name="description"></a><span data-ttu-id="94e54-2261">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2261">Description</span></span>

<span data-ttu-id="94e54-2262">Questo servizio fa in modo che il thread chiamante venga sospeso per il numero specificato di cicli del timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2262">This service causes the calling thread to suspend for the specified number of timer ticks.</span></span> <span data-ttu-id="94e54-2263">La quantità di tempo fisico associata a un segno di timer è specifica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-2263">The amount of physical time associated with a timer tick is application specific.</span></span> <span data-ttu-id="94e54-2264">Questo servizio può essere chiamato solo da un thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-2264">This service can be called only from an application thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2265">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2265">Parameters</span></span>

- <span data-ttu-id="94e54-2266">**timer_ticks** Numero di cicli del timer per sospendere il thread dell'applicazione chiamante, compreso tra 0 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="94e54-2266">**timer_ticks** The number of timer ticks to suspend the calling application thread, ranging from 0 through 0xFFFFFFFF.</span></span> <span data-ttu-id="94e54-2267">Se viene specificato 0, il servizio restituisce immediatamente il risultato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2267">If 0 is specified, the service returns immediately.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2268">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2268">Return Values</span></span>

- <span data-ttu-id="94e54-2269">Sospensione thread riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-2269">**TX_SUCCESS** (0x00) Successful thread sleep.</span></span>
- <span data-ttu-id="94e54-2270">La sospensione **TX_WAIT_ABORTED** (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="94e54-2270">**TX_WAIT_ABORTED** (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="94e54-2271">Il servizio **TX_CALLER_ERROR** (0x13) chiamato da un non thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-2271">**TX_CALLER_ERROR** (0x13) Service called from a non-thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2272">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2272">Allowed From</span></span>

<span data-ttu-id="94e54-2273">Thread</span><span class="sxs-lookup"><span data-stu-id="94e54-2273">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2274">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2274">Preemption Possible</span></span>

<span data-ttu-id="94e54-2275">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-2275">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2276">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2276">Example</span></span>

```c
UINT status;

/* Make the calling thread sleep for 100
timer-ticks. */
status = tx_thread_sleep(100);

/* If status equals TX_SUCCESS, the currently running
application thread slept for the specified number of
timer-ticks. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2277">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2277">See Also</span></span>

- <span data-ttu-id="94e54-2278">tx_thread_create, tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2278">tx_thread_create, tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2279">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2279">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2280">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2280">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2281">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2281">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2282">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2282">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2283">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2283">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-2284">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2284">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2285">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2285">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2286">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2286">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2287">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2287">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2288">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2288">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2289">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2289">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2290">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2290">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2291">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2291">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2292">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2292">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-2293">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2293">tx_thread_wait_abort</span></span>

## <a name="tx_thread_stack_error_notify"></a><span data-ttu-id="94e54-2294">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2294">tx_thread_stack_error_notify</span></span>

<span data-ttu-id="94e54-2295">Richiamata della notifica di errore dello stack di thread</span><span class="sxs-lookup"><span data-stu-id="94e54-2295">Register thread stack error notification callback</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2296">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2296">Prototype</span></span>

```c
UINT tx_thread_stack_error_notify(VOID (*error_handler)(TX_THREAD *));
```

### <a name="description"></a><span data-ttu-id="94e54-2297">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2297">Description</span></span>

<span data-ttu-id="94e54-2298">Questo servizio registra una funzione di callback di notifica per la gestione degli errori dello stack di thread.</span><span class="sxs-lookup"><span data-stu-id="94e54-2298">This service registers a notification callback function for handling thread stack errors.</span></span> <span data-ttu-id="94e54-2299">Quando ThreadX rileva un errore dello stack di thread durante l'esecuzione, chiamerà questa funzione di notifica per elaborare l'errore.</span><span class="sxs-lookup"><span data-stu-id="94e54-2299">When ThreadX detects a thread stack error during execution, it will call this notification function to process the error.</span></span> <span data-ttu-id="94e54-2300">L'elaborazione dell'errore è completamente definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-2300">Processing of the error is completely defined by the application.</span></span> <span data-ttu-id="94e54-2301">Qualsiasi operazione di sospensione del thread violato per la reimpostazione dell'intero sistema potrebbe essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="94e54-2301">Anything from suspending the violating thread to resetting the entire system may be done.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-2302">*Per consentire a questo servizio di restituire informazioni sulle prestazioni,* *è necessario compilare la libreria threadX con* **TX_ENABLE_STACK_CHECKING** definito.</span><span class="sxs-lookup"><span data-stu-id="94e54-2302">*The ThreadX library must be built with* **TX_ENABLE_STACK_CHECKING** *defined in order for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2303">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2303">Parameters</span></span>
- <span data-ttu-id="94e54-2304">**Error_Handler** Puntatore alla funzione di gestione degli errori dello stack dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-2304">**error_handler** Pointer to application's stack error handling function.</span></span> <span data-ttu-id="94e54-2305">Se questo valore è TX_NULL, la notifica viene disabilitata.</span><span class="sxs-lookup"><span data-stu-id="94e54-2305">If this value is TX_NULL, the notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2306">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2306">Return Values</span></span>

- <span data-ttu-id="94e54-2307">Reimpostazione thread riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-2307">**TX_SUCCESS** (0x00) Successful thread reset.</span></span>
- <span data-ttu-id="94e54-2308">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-2308">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2309">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2309">Allowed From</span></span>

<span data-ttu-id="94e54-2310">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2310">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2311">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2311">Example</span></span>

```c
void my_stack_error_handler(TX_THREAD *thread_ptr);

/* Register the "my_stack_error_handler" function with ThreadX
so that thread stack errors can be handled by the application. */
status = tx_thread_stack_error_notify(my_stack_error_handler);

/* If status is TX_SUCCESS the stack error handler is registered.*/
```

### <a name="see-also"></a><span data-ttu-id="94e54-2312">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2312">See Also</span></span>

- <span data-ttu-id="94e54-2313">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2313">tx_thread_create</span></span>
- <span data-ttu-id="94e54-2314">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2314">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2315">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2315">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2316">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2316">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2317">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2317">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2318">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2318">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2319">tx_thread_preformance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2319">tx_thread_preformance_system_info_get</span></span>
- <span data-ttu-id="94e54-2320">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2320">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2321">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2321">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2322">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2322">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2323">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2323">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2324">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2324">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2325">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2325">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2326">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2326">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2327">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2327">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2328">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2328">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-2329">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2329">tx_thread_wait_abort</span></span>

## <a name="tx_thread_suspend"></a><span data-ttu-id="94e54-2330">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2330">tx_thread_suspend</span></span>

<span data-ttu-id="94e54-2331">Sospendi thread applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2331">Suspend application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2332">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2332">Prototype</span></span>

```c
UINT tx_thread_suspend(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-2333">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2333">Description</span></span>

<span data-ttu-id="94e54-2334">Questo servizio sospende il thread dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2334">This service suspends the specified application thread.</span></span> <span data-ttu-id="94e54-2335">Un thread può chiamare questo servizio per sospendere se stesso.</span><span class="sxs-lookup"><span data-stu-id="94e54-2335">A thread may call this service to suspend itself.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2336">*Se il thread specificato è già sospeso per un altro motivo, questa sospensione viene mantenuta internamente fino a quando non viene sollevata la sospensione precedente. In tal caso, viene eseguita questa sospensione non condizionale del thread specificato. Altre richieste di sospensione non condizionale non hanno alcun effetto.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2336">*If the specified thread is already suspended for another reason, this suspension is held internally until the prior suspension is lifted. When that happens, this unconditional suspension of the specified thread is performed. Further unconditional suspension requests have no effect.*</span></span>

<span data-ttu-id="94e54-2337">Dopo la sospensione, il thread deve essere ripreso da ***tx_thread_resume*** per eseguirlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="94e54-2337">After being suspended, the thread must be resumed by ***tx_thread_resume*** to execute again.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2338">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2338">Parameters</span></span>

- <span data-ttu-id="94e54-2339">**thread_ptr** Puntatore a un thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-2339">**thread_ptr** Pointer to an application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2340">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2340">Return Values</span></span>

- <span data-ttu-id="94e54-2341">Sospensione thread riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-2341">**TX_SUCCESS** (0x00) Successful thread suspend.</span></span>
- <span data-ttu-id="94e54-2342">**TX_THREAD_ERROR** (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2342">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="94e54-2343">Il thread specificato **TX_SUSPEND_ERROR** (0x14) è in stato terminato o completato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2343">**TX_SUSPEND_ERROR** (0x14) Specified thread is in a terminated or completed state.</span></span>
- <span data-ttu-id="94e54-2344">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-2344">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2345">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2345">Allowed From</span></span>

<span data-ttu-id="94e54-2346">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2346">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2347">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2347">Preemption Possible</span></span>

<span data-ttu-id="94e54-2348">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-2348">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2349">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2349">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Suspend the thread represented by "my_thread". */
status = tx_thread_suspend(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
unconditionally suspended. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2350">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2350">See Also</span></span>

- <span data-ttu-id="94e54-2351">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2351">tx_thread_create</span></span>
- <span data-ttu-id="94e54-2352">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2352">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2353">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2353">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2354">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2354">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2355">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2355">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2356">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2356">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2357">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2357">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-2358">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2358">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2359">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2359">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2360">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2360">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2361">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2361">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2362">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2362">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2363">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2363">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2364">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2364">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2365">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2365">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2366">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2366">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-2367">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2367">tx_thread_wait_abort</span></span>

## <a name="tx_thread_terminate"></a><span data-ttu-id="94e54-2368">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2368">tx_thread_terminate</span></span>

<span data-ttu-id="94e54-2369">Termina il thread dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2369">Terminates application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2370">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2370">Prototype</span></span>

```c
UINT tx_thread_terminate(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="94e54-2371">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2371">Description</span></span>

<span data-ttu-id="94e54-2372">Questo servizio termina il thread dell'applicazione specificato indipendentemente dal fatto che il thread sia sospeso o meno.</span><span class="sxs-lookup"><span data-stu-id="94e54-2372">This service terminates the specified application thread regardless of whether the thread is suspended or not.</span></span> <span data-ttu-id="94e54-2373">Un thread può chiamare questo servizio per terminare se stesso.</span><span class="sxs-lookup"><span data-stu-id="94e54-2373">A thread may call this service to terminate itself.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2374">*È responsabilità dell'applicazione assicurarsi che il thread si trovi in uno stato appropriato per la terminazione. Un thread, ad esempio, non deve terminare durante l'elaborazione critica dell'applicazione o all'interno di altri componenti del middleware in cui potrebbe lasciare tale elaborazione in uno stato sconosciuto.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2374">*It is the application's responsibility to ensure that the thread is in a state suitable for termination. For example, a thread should not be terminated during critical application processing or inside of other middleware components where it could leave such processing in an unknown state.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-2375">*Dopo la terminazione, è necessario reimpostare il thread affinché venga eseguito nuovamente.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2375">*After being terminated, the thread must be reset for it to execute again.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2376">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2376">Parameters</span></span>

- <span data-ttu-id="94e54-2377">**thread_ptr** Puntatore al thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-2377">**thread_ptr** Pointer to application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2378">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2378">Return Values</span></span>
- <span data-ttu-id="94e54-2379">Terminazione del thread **TX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="94e54-2379">**TX_SUCCESS** (0x00) Successful thread terminate.</span></span>
- <span data-ttu-id="94e54-2380">**TX_THREAD_ERROR** (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2380">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="94e54-2381">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-2381">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2382">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2382">Allowed From</span></span>

<span data-ttu-id="94e54-2383">Thread e timer</span><span class="sxs-lookup"><span data-stu-id="94e54-2383">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2384">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2384">Preemption Possible</span></span>

<span data-ttu-id="94e54-2385">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-2385">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2386">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2386">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Terminate the thread represented by "my_thread". */
status = tx_thread_terminate(&my_thread);

/* If status equals TX_SUCCESS, the thread is terminated
and cannot execute again until it is reset. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2387">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2387">See Also</span></span>

- <span data-ttu-id="94e54-2388">tx_thread_create tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2388">tx_thread_create tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2389">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2389">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2390">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2390">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2391">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2391">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2392">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2392">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2393">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2393">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-2394">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2394">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2395">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2395">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2396">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2396">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2397">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2397">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2398">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2398">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2399">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2399">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2400">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2400">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2401">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2401">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2402">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2402">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="94e54-2403">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2403">tx_thread_wait_abort</span></span>

## <a name="tx_thread_time_slice_change"></a><span data-ttu-id="94e54-2404">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2404">tx_thread_time_slice_change</span></span>

<span data-ttu-id="94e54-2405">Modifica la sezione temporale del thread dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2405">Changes time-slice of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2406">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2406">Prototype</span></span>

```c
UINT tx_thread_time_slice_change(
    TX_THREAD *thread_ptr,
    ULONG new_time_slice, 
    ULONG *old_time_slice);
```

### <a name="description"></a><span data-ttu-id="94e54-2407">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2407">Description</span></span>

<span data-ttu-id="94e54-2408">Questo servizio modifica la porzione di tempo del thread dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2408">This service changes the time-slice of the specified application thread.</span></span> <span data-ttu-id="94e54-2409">Se si seleziona un intervallo di tempo per un thread, si assicura che non venga eseguito un numero di cicli del timer superiore a quello specificato prima che sia possibile eseguire gli altri thread con priorità uguale o superiore.</span><span class="sxs-lookup"><span data-stu-id="94e54-2409">Selecting a time-slice for a thread insures that it won't execute more than the specified number of timer ticks before other threads of the same or higher priorities have a chance to execute.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2410">*Con la soglia di precedenza viene disabilitato il sezionamento del tempo per il thread specificato.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2410">*Using preemption-threshold disables time-slicing for the specified thread.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2411">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2411">Parameters</span></span>

- <span data-ttu-id="94e54-2412">**thread_ptr** Puntatore al thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-2412">**thread_ptr** Pointer to application thread.</span></span>
- <span data-ttu-id="94e54-2413">**new_time_slice** Nuovo valore della sezione di tempo.</span><span class="sxs-lookup"><span data-stu-id="94e54-2413">**new_time_slice** New time slice value.</span></span> <span data-ttu-id="94e54-2414">I valori validi includono TX_NO_TIME_SLICE e i valori numerici da 1 a 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="94e54-2414">Legal values include TX_NO_TIME_SLICE and numeric values from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="94e54-2415">**old_time_slice** Puntatore alla posizione in cui archiviare il valore TimeSlice precedente del thread specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2415">**old_time_slice** Pointer to location for storing the previous timeslice value of the specified thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2416">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2416">Return Values</span></span>

- <span data-ttu-id="94e54-2417">**TX_SUCCESS** (0x00) ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="94e54-2417">**TX_SUCCESS** (0x00) Successful time-slice chance.</span></span>
- <span data-ttu-id="94e54-2418">**TX_THREAD_ERROR** (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2418">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="94e54-2419">**TX_PTR_ERROR** (0x03) puntatore non valido al percorso di archiviazione del periodo di tempo precedente.</span><span class="sxs-lookup"><span data-stu-id="94e54-2419">**TX_PTR_ERROR** (0x03) Invalid pointer to previous time-slice storage location.</span></span>
- <span data-ttu-id="94e54-2420">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-2420">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2421">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2421">Allowed From</span></span>

<span data-ttu-id="94e54-2422">Thread e timer</span><span class="sxs-lookup"><span data-stu-id="94e54-2422">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2423">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2423">Preemption Possible</span></span>

<span data-ttu-id="94e54-2424">No</span><span class="sxs-lookup"><span data-stu-id="94e54-2424">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2425">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2425">Example</span></span>

```c
TX_THREAD my_thread;
ULONG my_old_time_slice;
UINT status;

/* Change the time-slice of the thread associated with
"my_thread" to 20. This will mean that "my_thread"
can only run for 20 timer-ticks consecutively before
other threads of equal or higher priority get a chance
to run. */
status = tx_thread_time_slice_change(&my_thread, 20,
    &my_old_time_slice);

/* If status equals TX_SUCCESS, the thread’s time-slice
has been changed to 20 and the previous time-slice is
in "my_old_time_slice." */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2426">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2426">See Also</span></span>

- <span data-ttu-id="94e54-2427">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2427">tx_thread_create</span></span>
- <span data-ttu-id="94e54-2428">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2428">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2429">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2429">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2430">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2430">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2431">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2431">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2432">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2432">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2433">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2433">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-2434">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2434">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2435">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2435">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2436">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2436">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2437">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2437">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2438">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2438">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2439">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2439">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2440">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2440">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2441">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2441">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2442">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2442">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2443">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2443">tx_thread_wait_abort</span></span>

## <a name="tx_thread_wait_abort"></a><span data-ttu-id="94e54-2444">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="94e54-2444">tx_thread_wait_abort</span></span>

<span data-ttu-id="94e54-2445">Interrompi sospensione del thread specificato</span><span class="sxs-lookup"><span data-stu-id="94e54-2445">Abort suspension of specified thread</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2446">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2446">Prototype</span></span>

```c
UINT tx_thread_wait_abort(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-2447">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2447">Description</span></span>

<span data-ttu-id="94e54-2448">Questo servizio interrompe il sonno o qualsiasi altra sospensione di oggetti del thread specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2448">This service aborts sleep or any other object suspension of the specified thread.</span></span> <span data-ttu-id="94e54-2449">Se l'attesa viene interrotta, viene restituito un valore **TX_WAIT_ABORTED** dal servizio su cui il thread era in attesa.</span><span class="sxs-lookup"><span data-stu-id="94e54-2449">If the wait is aborted, a **TX_WAIT_ABORTED** value is returned from the service that the thread was waiting on.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2450">*Questo servizio non rilascia sospensioni esplicite effettuate dal servizio tx_thread_suspend.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2450">*This service does not release explicit suspension that is made by the tx_thread_suspend service.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2451">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2451">Parameters</span></span>

- <span data-ttu-id="94e54-2452">**thread_ptr** Puntatore a un thread dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-2452">**thread_ptr** Pointer to a previously created application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2453">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2453">Return Values</span></span>

- <span data-ttu-id="94e54-2454">Interruzione attesa thread riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-2454">**TX_SUCCESS** (0x00) Successful thread wait abort.</span></span>
- <span data-ttu-id="94e54-2455">**TX_THREAD_ERROR** (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2455">**TX_THREAD_ERROR** (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="94e54-2456">Il thread specificato **TX_WAIT_ABORT_ERROR** (0x1B) non è in uno stato di attesa.</span><span class="sxs-lookup"><span data-stu-id="94e54-2456">**TX_WAIT_ABORT_ERROR** (0x1B) Specified thread is not in a waiting state.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2457">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2457">Allowed From</span></span>

<span data-ttu-id="94e54-2458">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2458">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2459">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2459">Preemption Possible</span></span>
<span data-ttu-id="94e54-2460">Sì</span><span class="sxs-lookup"><span data-stu-id="94e54-2460">Yes</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2461">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2461">Example</span></span>

```c
TX_THREAD my_thread;
UINT status;

/* Abort the suspension condition of "my_thread." */
status = tx_thread_wait_abort(&my_thread);

/* If status equals TX_SUCCESS, the thread is now ready
again, with a return value showing its suspension
was aborted (TX_WAIT_ABORTED). */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2462">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2462">See Also</span></span>

- <span data-ttu-id="94e54-2463">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2463">tx_thread_create</span></span>
- <span data-ttu-id="94e54-2464">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2464">tx_thread_delete</span></span>
- <span data-ttu-id="94e54-2465">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2465">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="94e54-2466">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="94e54-2466">tx_thread_identify</span></span>
- <span data-ttu-id="94e54-2467">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2467">tx_thread_info_get</span></span>
- <span data-ttu-id="94e54-2468">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2468">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="94e54-2469">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2469">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="94e54-2470">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2470">tx_thread_preemption_change</span></span>
- <span data-ttu-id="94e54-2471">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2471">tx_thread_priority_change</span></span>
- <span data-ttu-id="94e54-2472">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="94e54-2472">tx_thread_relinquish</span></span>
- <span data-ttu-id="94e54-2473">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="94e54-2473">tx_thread_reset</span></span>
- <span data-ttu-id="94e54-2474">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="94e54-2474">tx_thread_resume</span></span>
- <span data-ttu-id="94e54-2475">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="94e54-2475">tx_thread_sleep</span></span>
- <span data-ttu-id="94e54-2476">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="94e54-2476">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="94e54-2477">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="94e54-2477">tx_thread_suspend</span></span>
- <span data-ttu-id="94e54-2478">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="94e54-2478">tx_thread_terminate</span></span>
- <span data-ttu-id="94e54-2479">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2479">tx_thread_time_slice_change</span></span>

## <a name="tx_time_get"></a><span data-ttu-id="94e54-2480">tx_time_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2480">tx_time_get</span></span>

<span data-ttu-id="94e54-2481">Recupera l'ora corrente</span><span class="sxs-lookup"><span data-stu-id="94e54-2481">Retrieves the current time</span></span>

<span data-ttu-id="94e54-2482">Timer applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2482">Application Timers</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2483">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2483">Prototype</span></span>

```c
ULONG tx_time_get(VOID);
```

### <a name="description"></a><span data-ttu-id="94e54-2484">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2484">Description</span></span>

<span data-ttu-id="94e54-2485">Questo servizio restituisce il contenuto del clock di sistema interno.</span><span class="sxs-lookup"><span data-stu-id="94e54-2485">This service returns the contents of the internal system clock.</span></span> <span data-ttu-id="94e54-2486">Ogni TimerTick aumenta il clock di sistema interno di uno.</span><span class="sxs-lookup"><span data-stu-id="94e54-2486">Each timertick increases the internal system clock by one.</span></span> <span data-ttu-id="94e54-2487">Il clock di sistema è impostato su zero durante l'inizializzazione e può essere modificato in un valore specifico dal servizio ***tx_time_set***.</span><span class="sxs-lookup"><span data-stu-id="94e54-2487">The system clock is set to zero during initialization and can be changed to a specific value by the service ***tx_time_set***.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2488">*Il tempo effettivo rappresentato da ogni segno di timer è specifico dell'applicazione.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2488">*The actual time each timer-tick represents is application specific.*</span></span>

<span data-ttu-id="94e54-2489">**Parametri**</span><span class="sxs-lookup"><span data-stu-id="94e54-2489">**Parameters**</span></span>

<span data-ttu-id="94e54-2490">nessuno</span><span class="sxs-lookup"><span data-stu-id="94e54-2490">None</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2491">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2491">Return Values</span></span>

- <span data-ttu-id="94e54-2492">**tick del clock di sistema** Valore del clock di sistema interno, libero in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="94e54-2492">**system clock ticks** Value of the internal, free running, system clock.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2493">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2493">Allowed From</span></span>

<span data-ttu-id="94e54-2494">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2494">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2495">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2495">Preemption Possible</span></span>
<span data-ttu-id="94e54-2496">No</span><span class="sxs-lookup"><span data-stu-id="94e54-2496">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2497">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2497">Example</span></span>

```c
ULONG current_time;

/* Pickup the current system time, in timer-ticks. */
current_time = tx_time_get();

/* Current time now contains a copy of the internal system
clock. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2498">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2498">See Also</span></span>

- <span data-ttu-id="94e54-2499">tx_time_set</span><span class="sxs-lookup"><span data-stu-id="94e54-2499">tx_time_set</span></span>

## <a name="tx_time_set"></a><span data-ttu-id="94e54-2500">tx_time_set</span><span class="sxs-lookup"><span data-stu-id="94e54-2500">tx_time_set</span></span>

<span data-ttu-id="94e54-2501">Imposta l'ora corrente</span><span class="sxs-lookup"><span data-stu-id="94e54-2501">Sets the current time</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2502">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2502">Prototype</span></span>

```c
VOID tx_time_set(ULONG new_time);
```

### <a name="description"></a><span data-ttu-id="94e54-2503">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2503">Description</span></span>

<span data-ttu-id="94e54-2504">Questo servizio imposta l'orologio di sistema interno sul valore specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2504">This service sets the internal system clock to the specified value.</span></span> <span data-ttu-id="94e54-2505">Ogni timer-tick aumenta il clock di sistema interno di uno.</span><span class="sxs-lookup"><span data-stu-id="94e54-2505">Each timer-tick increases the internal system clock by one.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2506">*Il tempo effettivo rappresentato da ogni segno di timer è specifico dell'applicazione.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2506">*The actual time each timer-tick represents is application specific.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2507">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2507">Parameters</span></span>

- <span data-ttu-id="94e54-2508">**New_time** Nuova ora da inserire nell'orologio di sistema, i valori validi sono compresi tra 0 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="94e54-2508">**new_time** New time to put in the system clock, legal values range from 0 through 0xFFFFFFFF.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2509">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2509">Return Values</span></span>

<span data-ttu-id="94e54-2510">nessuno</span><span class="sxs-lookup"><span data-stu-id="94e54-2510">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2511">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2511">Allowed From</span></span>

<span data-ttu-id="94e54-2512">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2512">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2513">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2513">Preemption Possible</span></span>

<span data-ttu-id="94e54-2514">No</span><span class="sxs-lookup"><span data-stu-id="94e54-2514">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2515">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2515">Example</span></span>

```c
/* Set the internal system time to 0x1234. */
tx_time_set(0x1234);

/* Current time now contains 0x1234 until the next timer
interrupt. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2516">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2516">See Also</span></span>

- <span data-ttu-id="94e54-2517">tx_time_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2517">tx_time_get</span></span>

## <a name="tx_timer_activate"></a><span data-ttu-id="94e54-2518">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="94e54-2518">tx_timer_activate</span></span>

<span data-ttu-id="94e54-2519">Attiva timer applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2519">Activate application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2520">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2520">Prototype</span></span>

```c
UINT tx_timer_activate(TX_TIMER *timer_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-2521">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2521">Description</span></span>

<span data-ttu-id="94e54-2522">Questo servizio attiva il timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2522">This service activates the specified application timer.</span></span> <span data-ttu-id="94e54-2523">Le routine di scadenza dei timer che scadono nello stesso momento vengono eseguite nell'ordine in cui sono state attivate.</span><span class="sxs-lookup"><span data-stu-id="94e54-2523">The expiration routines of timers that expire at the same time are executed in the order they were activated.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2524">*È necessario reimpostare un timer di una volta scaduto tramite*  \* **tx_timer_change** _ _before può essere nuovamente attivata. \*</span><span class="sxs-lookup"><span data-stu-id="94e54-2524">*An expired one-shot timer must be reset via* ***tx_timer_change** _ _before it can be activated again.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2525">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2525">Parameters</span></span>

- <span data-ttu-id="94e54-2526">**timer_ptr** Puntatore a un timer dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-2526">**timer_ptr** Pointer to a previously created application timer.</span></span>

<span data-ttu-id="94e54-2527">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="94e54-2527">**Return Values**</span></span>

- <span data-ttu-id="94e54-2528">Attivazione del timer applicazione riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-2528">**TX_SUCCESS** (0x00) Successful application timer activation.</span></span>
- <span data-ttu-id="94e54-2529">**TX_TIMER_ERROR** (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2529">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="94e54-2530">Il timer **TX_ACTIVATE_ERROR** (0x17) era già attivo o è un timer monouso che è già scaduto.</span><span class="sxs-lookup"><span data-stu-id="94e54-2530">**TX_ACTIVATE_ERROR** (0x17) Timer was already active or is a one-shot timer that has already expired.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2531">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2531">Allowed From</span></span>

<span data-ttu-id="94e54-2532">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2532">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2533">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2533">Preemption Possible</span></span>

<span data-ttu-id="94e54-2534">No</span><span class="sxs-lookup"><span data-stu-id="94e54-2534">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2535">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2535">Example</span></span>

```c
TX_TIMER my_timer;
UINT status;

/* Activate an application timer. Assume that the
application timer has already been created. */
status = tx_timer_activate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
now active. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2536">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2536">See Also</span></span>

- <span data-ttu-id="94e54-2537">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2537">tx_timer_change</span></span>
- <span data-ttu-id="94e54-2538">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2538">tx_timer_create</span></span>
- <span data-ttu-id="94e54-2539">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="94e54-2539">tx_timer_deactivate</span></span>
- <span data-ttu-id="94e54-2540">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2540">tx_timer_delete</span></span>
- <span data-ttu-id="94e54-2541">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2541">tx_timer_info_get</span></span>
- <span data-ttu-id="94e54-2542">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2542">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="94e54-2543">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2543">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_change"></a><span data-ttu-id="94e54-2544">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2544">tx_timer_change</span></span>

<span data-ttu-id="94e54-2545">Modifica timer applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2545">Change application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2546">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2546">Prototype</span></span>

```c
UINT tx_timer_change(
    TX_TIMER *timer_ptr,
    ULONG initial_ticks, 
    ULONG reschedule_ticks);
```

### <a name="description"></a><span data-ttu-id="94e54-2547">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2547">Description</span></span>

<span data-ttu-id="94e54-2548">Questo servizio modifica le caratteristiche di scadenza del timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2548">This service changes the expiration characteristics of the specified application timer.</span></span> <span data-ttu-id="94e54-2549">Il timer deve essere disattivato prima di chiamare il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-2549">The timer must be deactivated prior to calling this service.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2550">*Una chiamata al*  \* **tx_timer_activate** _ _service è necessario dopo il servizio per poter riavviare il timer. \*</span><span class="sxs-lookup"><span data-stu-id="94e54-2550">*A call to the* ***tx_timer_activate** _ _service is required after this service in order to start the timer again.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2551">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2551">Parameters</span></span>

- <span data-ttu-id="94e54-2552">**timer_ptr** Puntatore a un blocco di controllo del timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2552">**timer_ptr** Pointer to a timer control block.</span></span>
- <span data-ttu-id="94e54-2553">**initial_ticks** Specifica il numero iniziale di cicli per la scadenza del timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2553">**initial_ticks** Specifies the initial number of ticks for timer expiration.</span></span> <span data-ttu-id="94e54-2554">I valori validi sono compresi tra 1 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="94e54-2554">Legal values range from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="94e54-2555">**reschedule_ticks** Specifica il numero di cicli per tutte le scadenze del timer dopo la prima.</span><span class="sxs-lookup"><span data-stu-id="94e54-2555">**reschedule_ticks** Specifies the number of ticks for all timer expirations after the first.</span></span> <span data-ttu-id="94e54-2556">Uno zero per questo parametro rende il timer un timer *unico* .</span><span class="sxs-lookup"><span data-stu-id="94e54-2556">A zero for this parameter makes the timer a *one-shot* timer.</span></span> <span data-ttu-id="94e54-2557">In caso contrario, per i timer periodici i valori validi sono compresi tra 1 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="94e54-2557">Otherwise, for periodic timers, legal values range from 1 through 0xFFFFFFFF.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2558">*È necessario reimpostare un timer di una volta scaduto tramite* 
\* **tx_timer_change** _ _before può essere nuovamente attivata. \*</span><span class="sxs-lookup"><span data-stu-id="94e54-2558">*An expired one-shot timer must be reset via*
***tx_timer_change** _ _before it can be activated again.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2559">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2559">Return Values</span></span>

- <span data-ttu-id="94e54-2560">**TX_SUCCESS** (0x00) modifica del timer applicazione completata.</span><span class="sxs-lookup"><span data-stu-id="94e54-2560">**TX_SUCCESS** (0x00) Successful application timer change.</span></span>
- <span data-ttu-id="94e54-2561">**TX_TIMER_ERROR** (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2561">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="94e54-2562">**TX_TICK_ERROR** (0x16) valore non valido (zero) fornito per i cicli iniziali.</span><span class="sxs-lookup"><span data-stu-id="94e54-2562">**TX_TICK_ERROR** (0x16) Invalid value (a zero) supplied for initial ticks.</span></span>
- <span data-ttu-id="94e54-2563">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-2563">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2564">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2564">Allowed From</span></span>

<span data-ttu-id="94e54-2565">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2565">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2566">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2566">Preemption Possible</span></span>

<span data-ttu-id="94e54-2567">No</span><span class="sxs-lookup"><span data-stu-id="94e54-2567">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2568">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2568">Example</span></span>

```c
TX_TIMER my_timer;
UINT status;

/* Change a previously created and now deactivated timer
to expire every 50 timer ticks, including the initial
expiration. */
status = tx_timer_change(&my_timer,50, 50);

/* If status equals TX_SUCCESS, the specified timer is
changed to expire every 50 ticks. */

/* Activate the specified timer to get it started again. */
status = tx_timer_activate(&my_timer);
```

### <a name="see-also"></a><span data-ttu-id="94e54-2569">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2569">See Also</span></span>

- <span data-ttu-id="94e54-2570">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="94e54-2570">tx_timer_activate</span></span>
- <span data-ttu-id="94e54-2571">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2571">tx_timer_create</span></span>
- <span data-ttu-id="94e54-2572">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="94e54-2572">tx_timer_deactivate</span></span>
- <span data-ttu-id="94e54-2573">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2573">tx_timer_delete</span></span>
- <span data-ttu-id="94e54-2574">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2574">tx_timer_info_get</span></span>
- <span data-ttu-id="94e54-2575">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2575">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="94e54-2576">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2576">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_create"></a><span data-ttu-id="94e54-2577">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2577">tx_timer_create</span></span>

<span data-ttu-id="94e54-2578">Crea timer applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2578">Create application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2579">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2579">Prototype</span></span>

```c
UINT tx_timer_create(
    TX_TIMER *timer_ptr, 
    CHAR *name_ptr,
    VOID (*expiration_function)(ULONG),
    ULONG expiration_input, 
    ULONG initial_ticks,
    ULONG reschedule_ticks, 
    UINT auto_activate);
```

### <a name="description"></a><span data-ttu-id="94e54-2580">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2580">Description</span></span>

<span data-ttu-id="94e54-2581">Questo servizio crea un timer dell'applicazione con la funzione di scadenza specificata e periodica.</span><span class="sxs-lookup"><span data-stu-id="94e54-2581">This service creates an application timer with the specified expiration function and periodic.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2582">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2582">Parameters</span></span>

- <span data-ttu-id="94e54-2583">**timer_ptr** Puntatore a un blocco di controllo timer</span><span class="sxs-lookup"><span data-stu-id="94e54-2583">**timer_ptr** Pointer to a timer control block</span></span>
- <span data-ttu-id="94e54-2584">**name_ptr** Puntatore al nome del timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2584">**name_ptr** Pointer to the name of the timer.</span></span>
- <span data-ttu-id="94e54-2585">**expiration_function** Funzione dell'applicazione da chiamare quando il timer scade.</span><span class="sxs-lookup"><span data-stu-id="94e54-2585">**expiration_function** Application function to call when the timer expires.</span></span>
- <span data-ttu-id="94e54-2586">**expiration_input** Input da passare alla funzione di scadenza quando il timer scade.</span><span class="sxs-lookup"><span data-stu-id="94e54-2586">**expiration_input** Input to pass to expiration function when timer expires.</span></span>
- <span data-ttu-id="94e54-2587">**initial_ticks** Specifica il numero iniziale di cicli per la scadenza del timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2587">**initial_ticks** Specifies the initial number of ticks for timer expiration.</span></span> <span data-ttu-id="94e54-2588">I valori validi sono compresi tra 1 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="94e54-2588">Legal values range from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="94e54-2589">**reschedule_ticks** Specifica il numero di cicli per tutte le scadenze del timer dopo la prima.</span><span class="sxs-lookup"><span data-stu-id="94e54-2589">**reschedule_ticks** Specifies the number of ticks for all timer expirations after the first.</span></span> <span data-ttu-id="94e54-2590">Uno zero per questo parametro rende il timer un timer *unico* .</span><span class="sxs-lookup"><span data-stu-id="94e54-2590">A zero for this parameter makes the timer a *one-shot* timer.</span></span> <span data-ttu-id="94e54-2591">In caso contrario, per i timer periodici i valori validi sono compresi tra 1 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="94e54-2591">Otherwise, for periodic timers, legal values range from 1 through 0xFFFFFFFF.</span></span>

  > [!NOTE]
  > <span data-ttu-id="94e54-2592">*Dopo la scadenza di un timer, è necessario reimpostarlo tramite tx_timer_change prima che sia possibile attivarlo di nuovo.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2592">*After a one-shot timer expires, it must be reset via   tx_timer_change before it can be activated again.*</span></span>

- <span data-ttu-id="94e54-2593">**AUTO_ACTIVATE** Determina se il timer viene attivato automaticamente durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="94e54-2593">**auto_activate** Determines if the timer is automatically activated during creation.</span></span> <span data-ttu-id="94e54-2594">Se questo valore è **TX_AUTO_ACTIVATE** (0x01), il timer viene reso attivo.</span><span class="sxs-lookup"><span data-stu-id="94e54-2594">If this value is **TX_AUTO_ACTIVATE** (0x01) the timer is made active.</span></span> <span data-ttu-id="94e54-2595">In caso contrario, se si seleziona il valore **TX_NO_ACTIVATE** (0x00), il timer viene creato in uno stato non attivo.</span><span class="sxs-lookup"><span data-stu-id="94e54-2595">Otherwise, if the value **TX_NO_ACTIVATE** (0x00) is selected, the timer is created in a non-active state.</span></span> <span data-ttu-id="94e54-2596">In questo caso, è necessaria una chiamata al servizio **_tx_timer_activate_** successiva per avviare effettivamente il timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2596">In this case, a subsequent **_tx_timer_activate_** service call is necessary to get the timer actually started.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2597">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2597">Return Values</span></span>

- <span data-ttu-id="94e54-2598">Creazione del timer applicazione riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-2598">**TX_SUCCESS** (0x00) Successful application timer creation.</span></span>
- <span data-ttu-id="94e54-2599">**TX_TIMER_ERROR** (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2599">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span> <span data-ttu-id="94e54-2600">Il puntatore è NULL o il timer è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2600">Either the pointer is NULL or the timer is already created.</span></span>
- <span data-ttu-id="94e54-2601">**TX_TICK_ERROR** (0x16) valore non valido (zero) fornito per i cicli iniziali.</span><span class="sxs-lookup"><span data-stu-id="94e54-2601">**TX_TICK_ERROR** (0x16) Invalid value (a zero) supplied for initial ticks.</span></span>
- <span data-ttu-id="94e54-2602">È stata selezionata l'attivazione **TX_ACTIVATE_ERROR** (0x17) non valida.</span><span class="sxs-lookup"><span data-stu-id="94e54-2602">**TX_ACTIVATE_ERROR** (0x17) Invalid activation selected.</span></span>
- <span data-ttu-id="94e54-2603">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-2603">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2604">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2604">Allowed From</span></span>

<span data-ttu-id="94e54-2605">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="94e54-2605">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2606">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2606">Preemption Possible</span></span>

<span data-ttu-id="94e54-2607">No</span><span class="sxs-lookup"><span data-stu-id="94e54-2607">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2608">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2608">Example</span></span>

```c
TX_TIMER my_timer;
UINT status;

/* Create an application timer that executes
"my_timer_function" after 100 ticks initially and then
after every 25 ticks. This timer is specified to start
immediately! */
status = tx_timer_create(&my_timer,"my_timer_name",
    my_timer_function, 0x1234, 100, 25,
    TX_AUTO_ACTIVATE);

/* If status equals TX_SUCCESS, my_timer_function will
be called 100 timer ticks later and then called every
25 timer ticks. Note that the value 0x1234 is passed to
my_timer_function every time it is called. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2609">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2609">See Also</span></span>

- <span data-ttu-id="94e54-2610">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="94e54-2610">tx_timer_activate</span></span>
- <span data-ttu-id="94e54-2611">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2611">tx_timer_change</span></span>
- <span data-ttu-id="94e54-2612">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="94e54-2612">tx_timer_deactivate</span></span>
- <span data-ttu-id="94e54-2613">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2613">tx_timer_delete</span></span>
- <span data-ttu-id="94e54-2614">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2614">tx_timer_info_get</span></span>
- <span data-ttu-id="94e54-2615">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2615">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="94e54-2616">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2616">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_deactivate"></a><span data-ttu-id="94e54-2617">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="94e54-2617">tx_timer_deactivate</span></span>

<span data-ttu-id="94e54-2618">Disattiva timer applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2618">Deactivate application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2619">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2619">Prototype</span></span>

```c
UINT tx_timer_deactivate(TX_TIMER *timer_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-2620">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2620">Description</span></span>

<span data-ttu-id="94e54-2621">Questo servizio disattiva il timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2621">This service deactivates the specified application timer.</span></span> <span data-ttu-id="94e54-2622">Se il timer è già disattivato, questo servizio non ha alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="94e54-2622">If the timer is already deactivated, this service has no effect.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2623">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2623">Parameters</span></span>

- <span data-ttu-id="94e54-2624">**timer_ptr** Puntatore a un timer dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-2624">**timer_ptr** Pointer to a previously created application timer.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2625">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2625">Return Values</span></span>

- <span data-ttu-id="94e54-2626">La disattivazione del timer applicazione riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-2626">**TX_SUCCESS** (0x00) Successful application timer deactivation.</span></span>
- <span data-ttu-id="94e54-2627">**TX_TIMER_ERROR** (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2627">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2628">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2628">Allowed From</span></span>

<span data-ttu-id="94e54-2629">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2629">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2630">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2630">Preemption Possible</span></span>

<span data-ttu-id="94e54-2631">No</span><span class="sxs-lookup"><span data-stu-id="94e54-2631">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2632">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2632">Example</span></span>

```c
TX_TIMER my_timer;
UINT status;

/* Deactivate an application timer. Assume that the
application timer has already been created. */
status = tx_timer_deactivate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
now deactivated. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2633">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2633">See Also</span></span>

- <span data-ttu-id="94e54-2634">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="94e54-2634">tx_timer_activate</span></span>
- <span data-ttu-id="94e54-2635">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2635">tx_timer_change</span></span>
- <span data-ttu-id="94e54-2636">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2636">tx_timer_create</span></span>
- <span data-ttu-id="94e54-2637">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2637">tx_timer_delete</span></span>
- <span data-ttu-id="94e54-2638">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2638">tx_timer_info_get</span></span>
- <span data-ttu-id="94e54-2639">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2639">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="94e54-2640">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2640">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_delete"></a><span data-ttu-id="94e54-2641">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2641">tx_timer_delete</span></span>

<span data-ttu-id="94e54-2642">Elimina timer applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2642">Delete application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2643">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2643">Prototype</span></span>

```c
UINT tx_timer_delete(TX_TIMER *timer_ptr);
```

### <a name="description"></a><span data-ttu-id="94e54-2644">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2644">Description</span></span>

<span data-ttu-id="94e54-2645">Questo servizio Elimina il timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2645">This service deletes the specified application timer.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2646">*È responsabilità dell'applicazione impedire l'uso di un timer eliminato.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2646">*It is the application's responsibility to prevent use of a deleted timer.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2647">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2647">Parameters</span></span>

- <span data-ttu-id="94e54-2648">**timer_ptr** Puntatore a un timer dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-2648">**timer_ptr** Pointer to a previously created application timer.</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2649">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2649">Return Values</span></span>

- <span data-ttu-id="94e54-2650">Eliminazione del timer applicazione riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-2650">**TX_SUCCESS** (0x00) Successful application timer deletion.</span></span>
- <span data-ttu-id="94e54-2651">**TX_TIMER_ERROR** (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2651">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="94e54-2652">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="94e54-2652">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2653">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2653">Allowed From</span></span>

<span data-ttu-id="94e54-2654">Thread</span><span class="sxs-lookup"><span data-stu-id="94e54-2654">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2655">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2655">Preemption Possible</span></span>

<span data-ttu-id="94e54-2656">No</span><span class="sxs-lookup"><span data-stu-id="94e54-2656">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2657">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2657">Example</span></span>

```c
TX_TIMER my_timer;
UINT status;

/* Delete application timer. Assume that the application
timer has already been created. */
status = tx_timer_delete(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
deleted. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2658">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2658">See Also</span></span>

- <span data-ttu-id="94e54-2659">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="94e54-2659">tx_timer_activate</span></span>
- <span data-ttu-id="94e54-2660">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2660">tx_timer_change</span></span>
- <span data-ttu-id="94e54-2661">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2661">tx_timer_create</span></span>
- <span data-ttu-id="94e54-2662">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="94e54-2662">tx_timer_deactivate</span></span>
- <span data-ttu-id="94e54-2663">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2663">tx_timer_info_get</span></span>
- <span data-ttu-id="94e54-2664">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2664">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="94e54-2665">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2665">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_info_get"></a><span data-ttu-id="94e54-2666">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2666">tx_timer_info_get</span></span>

<span data-ttu-id="94e54-2667">Recuperare informazioni sul timer di un'applicazione</span><span class="sxs-lookup"><span data-stu-id="94e54-2667">Retrieve information about an application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2668">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2668">Prototype</span></span>

```c
UINT tx_timer_info_get(
    TX_TIMER *timer_ptr, 
    CHAR **name,
    UINT *active,
    ULONG *remaining_ticks,
    ULONG *reschedule_ticks,
    TX_TIMER **next_timer);
```

### <a name="description"></a><span data-ttu-id="94e54-2669">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2669">Description</span></span>

<span data-ttu-id="94e54-2670">Questo servizio recupera le informazioni sul timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2670">This service retrieves information about the specified application timer.</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2671">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2671">Parameters</span></span>

- <span data-ttu-id="94e54-2672">**timer_ptr** Puntatore a un timer dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-2672">**timer_ptr** Pointer to a previously created application timer.</span></span>
- <span data-ttu-id="94e54-2673">**nome** Puntatore alla destinazione per il puntatore al nome del timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2673">**name** Pointer to destination for the pointer to the timer's name.</span></span>
- <span data-ttu-id="94e54-2674">**attivo** Puntatore alla destinazione per l'indicazione attiva del timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2674">**active** Pointer to destination for the timer active indication.</span></span> <span data-ttu-id="94e54-2675">Se il timer è inattivo o questo servizio viene chiamato dal timer stesso, viene restituito un valore **TX_FALSE** .</span><span class="sxs-lookup"><span data-stu-id="94e54-2675">If the timer is inactive or this service is called from the timer itself, a **TX_FALSE** value is returned.</span></span> <span data-ttu-id="94e54-2676">In caso contrario, se il timer è attivo, viene restituito un valore **TX_TRUE** .</span><span class="sxs-lookup"><span data-stu-id="94e54-2676">Otherwise, if the timer is active, a **TX_TRUE** value is returned.</span></span>
- <span data-ttu-id="94e54-2677">**remaining_ticks** Puntatore alla destinazione per il numero di cicli del timer rimasti prima della scadenza del timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2677">**remaining_ticks** Pointer to destination for the number of timer ticks left before the timer expires.</span></span>
- <span data-ttu-id="94e54-2678">**reschedule_ticks** Puntatore alla destinazione per il numero di cicli del timer che verranno utilizzati per ripianificare automaticamente questo timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2678">**reschedule_ticks** Pointer to destination for the number of timer ticks that will be used to automatically reschedule this timer.</span></span> <span data-ttu-id="94e54-2679">Se il valore è zero, il timer è una volta e non verrà ripianificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2679">If the value is zero, then the timer is a one-shot and won't be rescheduled.</span></span>
- <span data-ttu-id="94e54-2680">**next_timer** Puntatore alla destinazione per l'indicatore di misura del timer dell'applicazione creato successivo.</span><span class="sxs-lookup"><span data-stu-id="94e54-2680">**next_timer** Pointer to destination for the pointer of the next created application timer.</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2681">*La specifica di un **TX_NULL** per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2681">*Supplying a **TX_NULL** for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2682">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2682">Return Values</span></span>

- <span data-ttu-id="94e54-2683">Il recupero delle informazioni sul timer riuscito **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="94e54-2683">**TX_SUCCESS** (0x00) Successful timer information retrieval.</span></span>
- <span data-ttu-id="94e54-2684">**TX_TIMER_ERROR** (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2684">**TX_TIMER_ERROR** (0x15) Invalid application timer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2685">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2685">Allowed From</span></span>

<span data-ttu-id="94e54-2686">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2686">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="94e54-2687">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="94e54-2687">Preemption Possible</span></span>

<span data-ttu-id="94e54-2688">No</span><span class="sxs-lookup"><span data-stu-id="94e54-2688">No</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2689">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2689">Example</span></span>

```c
TX_TIMER my_timer;
CHAR *name;
UINT active;
ULONG remaining_ticks;
ULONG reschedule_ticks;
TX_TIMER *next_timer;
UINT status;

/* Retrieve information about the previously created
application timer "my_timer." */
status = tx_timer_info_get(&my_timer, &name,
    &active,&remaining_ticks,
    &reschedule_ticks,
    &next_timer);

/* If status equals TX_SUCCESS, the information requested is
valid. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2690">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2690">See Also</span></span>

- <span data-ttu-id="94e54-2691">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="94e54-2691">tx_timer_activate</span></span>
- <span data-ttu-id="94e54-2692">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2692">tx_timer_change</span></span>
- <span data-ttu-id="94e54-2693">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2693">tx_timer_create</span></span>
- <span data-ttu-id="94e54-2694">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="94e54-2694">tx_timer_deactivate</span></span>
- <span data-ttu-id="94e54-2695">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2695">tx_timer_delete</span></span>
- <span data-ttu-id="94e54-2696">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2696">tx_timer_info_get</span></span>
- <span data-ttu-id="94e54-2697">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2697">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="94e54-2698">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2698">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_performance_info_get"></a><span data-ttu-id="94e54-2699">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2699">tx_timer_performance_info_get</span></span>

<span data-ttu-id="94e54-2700">Ottenere le informazioni sulle prestazioni del timer</span><span class="sxs-lookup"><span data-stu-id="94e54-2700">Get timer performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2701">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2701">Prototype</span></span>

```c
UINT tx_timer_performance_info_get(
    TX_TIMER *timer_ptr,
    ULONG *activates, 
    ULONG *reactivates,
    ULONG *deactivates, 
    ULONG *expirations,
    ULONG *expiration_adjusts);
```

### <a name="description"></a><span data-ttu-id="94e54-2702">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2702">Description</span></span>

<span data-ttu-id="94e54-2703">Questo servizio recupera le informazioni sulle prestazioni relative al timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="94e54-2703">This service retrieves performance information about the specified application timer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-2704">*La libreria e l'applicazione threadX devono essere compilate con*  \* **TX_TIMER_ENABLE_PERFORMANCE_INFO** _ _defined per il servizio per restituire informazioni sulle prestazioni. \*</span><span class="sxs-lookup"><span data-stu-id="94e54-2704">*The ThreadX library and application must be built with* ***TX_TIMER_ENABLE_PERFORMANCE_INFO** _ _defined for this service to return performance information.*</span></span>

### <a name="parameters"></a><span data-ttu-id="94e54-2705">Parametri</span><span class="sxs-lookup"><span data-stu-id="94e54-2705">Parameters</span></span>
- <span data-ttu-id="94e54-2706">**timer_ptr** Puntatore al timer creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94e54-2706">**timer_ptr** Pointer to previously created timer.</span></span>
- <span data-ttu-id="94e54-2707">**attiva** Puntatore alla destinazione per il numero di richieste di attivazione eseguite su questo timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2707">**activates** Pointer to destination for the number of activation requests performed on this timer.</span></span>
- <span data-ttu-id="94e54-2708">**riattiva** Puntatore alla destinazione per il numero di riattivazioni automatiche eseguite su questo timer periodico.</span><span class="sxs-lookup"><span data-stu-id="94e54-2708">**reactivates** Pointer to destination for the number of automatic reactivations performed on this periodic timer.</span></span>
- <span data-ttu-id="94e54-2709">**Disattiva** Puntatore alla destinazione per il numero di richieste di disattivazione eseguite su questo timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2709">**deactivates** Pointer to destination for the number of deactivation requests performed on this timer.</span></span>
- <span data-ttu-id="94e54-2710">**scadenze** Puntatore alla destinazione per il numero di scadenze del timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2710">**expirations** Pointer to destination for the number of expirations of this timer.</span></span>
- <span data-ttu-id="94e54-2711">**expiration_adjusts** Puntatore alla destinazione per il numero di rettifiche di scadenza interne eseguite su questo timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2711">**expiration_adjusts** Pointer to destination for the number of internal expiration adjustments performed on this timer.</span></span> <span data-ttu-id="94e54-2712">Queste rettifiche vengono eseguite nell'elaborazione dell'interrupt del timer per i timer di dimensioni maggiori rispetto alle dimensioni predefinite dell'elenco di timer (per impostazione predefinita, i timer con scadenze maggiori di 32 cicli).</span><span class="sxs-lookup"><span data-stu-id="94e54-2712">These adjustments are done in the timer interrupt processing for timers that are larger than the default timer list size (by default timers with expirations greater than 32 ticks).</span></span>

> <span data-ttu-id="94e54-2713">Si noti *La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2713">[NOTE] *Supplying a TX_NULL for any parameter indicates the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2714">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2714">Return Values</span></span>

- <span data-ttu-id="94e54-2715">**TX_SUCCESS** (0x00) prestazioni timer riuscite.</span><span class="sxs-lookup"><span data-stu-id="94e54-2715">**TX_SUCCESS** (0x00) Successful timer performance get.</span></span>
- <span data-ttu-id="94e54-2716">**TX_PTR_ERROR** (0x03) puntatore del timer non valido.</span><span class="sxs-lookup"><span data-stu-id="94e54-2716">**TX_PTR_ERROR** (0x03) Invalid timer pointer.</span></span>
- <span data-ttu-id="94e54-2717">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-2717">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2718">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2718">Allowed From</span></span>

<span data-ttu-id="94e54-2719">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2719">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2720">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2720">Example</span></span>

```c
TX_TIMER my_timer;
ULONG activates;
ULONG reactivates;
ULONG deactivates;
ULONG expirations;
ULONG expiration_adjusts;

/* Retrieve performance information on the previously created
timer. */
status = tx_timer_performance_info_get(&my_timer, &activates,
    &reactivates,&deactivates, &expirations,
    &expiration_adjusts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2721">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2721">See Also</span></span>

- <span data-ttu-id="94e54-2722">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="94e54-2722">tx_timer_activate</span></span>
- <span data-ttu-id="94e54-2723">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2723">tx_timer_change</span></span>
- <span data-ttu-id="94e54-2724">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2724">tx_timer_create</span></span>
- <span data-ttu-id="94e54-2725">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="94e54-2725">tx_timer_deactivate</span></span>
- <span data-ttu-id="94e54-2726">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2726">tx_timer_delete</span></span>
- <span data-ttu-id="94e54-2727">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2727">tx_timer_info_get</span></span>
- <span data-ttu-id="94e54-2728">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2728">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_performance_system_info_get"></a><span data-ttu-id="94e54-2729">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2729">tx_timer_performance_system_info_get</span></span>

<span data-ttu-id="94e54-2730">Ottenere informazioni sulle prestazioni del sistema timer</span><span class="sxs-lookup"><span data-stu-id="94e54-2730">Get timer system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="94e54-2731">Prototipo</span><span class="sxs-lookup"><span data-stu-id="94e54-2731">Prototype</span></span>

```c
UINT tx_timer_performance_system_info_get(
    ULONG *activates,
    ULONG *reactivates, 
    ULONG *deactivates,
    ULONG *expirations, 
    ULONG *expiration_adjusts);
```

### <a name="description"></a><span data-ttu-id="94e54-2732">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94e54-2732">Description</span></span>

<span data-ttu-id="94e54-2733">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i timer dell'applicazione nel sistema.</span><span class="sxs-lookup"><span data-stu-id="94e54-2733">This service retrieves performance information about all the application timers in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94e54-2734">Per restituire informazioni sulle prestazioni, *è necessario compilare la libreria threadX e l'applicazione con* **TX_TIMER_ENABLE_PERFORMANCE_INFO** *definite per questo servizio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2734">*The ThreadX library and application must be built with* **TX_TIMER_ENABLE_PERFORMANCE_INFO** *defined for this service to return performance information.*</span></span>

<span data-ttu-id="94e54-2735">**Parametri**</span><span class="sxs-lookup"><span data-stu-id="94e54-2735">**Parameters**</span></span>

- <span data-ttu-id="94e54-2736">**attiva** Puntatore alla destinazione per il numero totale di richieste di attivazione eseguite su tutti i timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2736">**activates** Pointer to destination for the total number of activation requests performed on all timers.</span></span>
- <span data-ttu-id="94e54-2737">**riattiva** Puntatore alla destinazione per il numero totale di riattivazioni automatiche eseguite su tutti i timer periodici.</span><span class="sxs-lookup"><span data-stu-id="94e54-2737">**reactivates** Pointer to destination for the total number of automatic reactivation performed on all periodic timers.</span></span>
- <span data-ttu-id="94e54-2738">**Disattiva** Puntatore alla destinazione per il numero totale di richieste di disattivazione eseguite su tutti i timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2738">**deactivates** Pointer to destination for the total number of deactivation requests performed on all timers.</span></span>
- <span data-ttu-id="94e54-2739">**scadenze** Puntatore alla destinazione per il numero totale di scadenze in tutti i timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2739">**expirations** Pointer to destination for the total number of expirations on all timers.</span></span>
- <span data-ttu-id="94e54-2740">**expiration_adjusts** Puntatore alla destinazione per il numero totale di rettifiche di scadenza interne eseguite su tutti i timer.</span><span class="sxs-lookup"><span data-stu-id="94e54-2740">**expiration_adjusts** Pointer to destination for the total number of internal expiration adjustments performed on all timers.</span></span> <span data-ttu-id="94e54-2741">Queste rettifiche vengono eseguite nell'elaborazione dell'interrupt del timer per i timer di dimensioni maggiori rispetto alle dimensioni predefinite dell'elenco di timer (per impostazione predefinita, i timer con scadenze maggiori di 32 cicli).</span><span class="sxs-lookup"><span data-stu-id="94e54-2741">These adjustments are done in the timer interrupt processing for timers that are larger than the default timer list size (by default timers with expirations greater than 32 ticks).</span></span>

> [!NOTE]
> <span data-ttu-id="94e54-2742">*La specifica di un **TX_NULL** per qualsiasi parametro indica che il parametro non è obbligatorio.*</span><span class="sxs-lookup"><span data-stu-id="94e54-2742">*Supplying a **TX_NULL** for any parameter indicates that the parameter is not required.*</span></span>

### <a name="return-values"></a><span data-ttu-id="94e54-2743">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="94e54-2743">Return Values</span></span>

- <span data-ttu-id="94e54-2744">**TX_SUCCESS** (0x00) ottenere prestazioni del sistema timer riuscite.</span><span class="sxs-lookup"><span data-stu-id="94e54-2744">**TX_SUCCESS** (0x00) Successful timer system performance get.</span></span>
- <span data-ttu-id="94e54-2745">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="94e54-2745">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="94e54-2746">Consentito da</span><span class="sxs-lookup"><span data-stu-id="94e54-2746">Allowed From</span></span>

<span data-ttu-id="94e54-2747">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="94e54-2747">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="94e54-2748">Esempio</span><span class="sxs-lookup"><span data-stu-id="94e54-2748">Example</span></span>

```c
ULONG activates;
ULONG reactivates;
ULONG deactivates;
ULONG expirations;
ULONG expiration_adjusts;

/* Retrieve performance information on all previously created
timers. */
status = tx_timer_performance_system_info_get(&activates,
    &reactivates, &deactivates, &expirations,
    &expiration_adjusts);

/* If status is TX_SUCCESS the performance information was
successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="94e54-2749">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="94e54-2749">See Also</span></span>

- <span data-ttu-id="94e54-2750">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="94e54-2750">tx_timer_activate</span></span>
- <span data-ttu-id="94e54-2751">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="94e54-2751">tx_timer_change</span></span>
- <span data-ttu-id="94e54-2752">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="94e54-2752">tx_timer_create</span></span>
- <span data-ttu-id="94e54-2753">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="94e54-2753">tx_timer_deactivate</span></span>
- <span data-ttu-id="94e54-2754">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="94e54-2754">tx_timer_delete</span></span>
- <span data-ttu-id="94e54-2755">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2755">tx_timer_info_get</span></span>
- <span data-ttu-id="94e54-2756">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="94e54-2756">tx_timer_performance_info_get</span></span>
