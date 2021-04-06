---
title: Capitolo 3-API ThreadX per ARMv8-M
description: Questo capitolo descrive i servizi ThreadX specifici di ARMv8-M.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 14bdfab3d56476d52ba91f859cec4af4ab7f4bef
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377598"
---
# <a name="chapter-3--threadx-apis-for-armv8-m"></a><span data-ttu-id="35f87-103">Capitolo 3 API ThreadX per ARMv8-M</span><span class="sxs-lookup"><span data-stu-id="35f87-103">Chapter 3  ThreadX APIs for ARMv8-M</span></span>

<span data-ttu-id="35f87-104">Questo capitolo contiene una descrizione dei servizi ThreadX specifici di ARMv8-M in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="35f87-104">This chapter contains a description of the ARMv8-M-specific ThreadX services in alphabetic order.</span></span> <span data-ttu-id="35f87-105">I nomi sono progettati in modo da raggruppare tutti i servizi simili.</span><span class="sxs-lookup"><span data-stu-id="35f87-105">Their names are designed so all similar services are grouped together.</span></span> <span data-ttu-id="35f87-106">Nella sezione "valori restituiti" nelle descrizioni seguenti i valori in **grassetto** non sono interessati dal **TX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API; mentre i valori visualizzati in non grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="35f87-106">In the "Return Values" section in the following descriptions, values in **BOLD** are not affected by the **TX_DISABLE_ERROR_CHECKING** define used to disable API error checking; while values shown in non-bold are completely disabled.</span></span>

- <span data-ttu-id="35f87-107">[tx_thread_secure_stack_allocate](#tx_thread_secure_stack_allocate) Allocare uno stack di thread nella memoria protetta.</span><span class="sxs-lookup"><span data-stu-id="35f87-107">[tx_thread_secure_stack_allocate](#tx_thread_secure_stack_allocate) Allocate a thread stack in secure memory.</span></span>
- <span data-ttu-id="35f87-108">[tx_thread_secure_stack_free](#tx_thread_secure_stack_free) Stack di thread libero in memoria protetta</span><span class="sxs-lookup"><span data-stu-id="35f87-108">[tx_thread_secure_stack_free](#tx_thread_secure_stack_free) Free thread stack in secure memory</span></span>

## <a name="tx_thread_secure_stack_allocate"></a><span data-ttu-id="35f87-109">tx_thread_secure_stack_allocate</span><span class="sxs-lookup"><span data-stu-id="35f87-109">tx_thread_secure_stack_allocate</span></span>

<span data-ttu-id="35f87-110">Allocare uno stack di thread nella memoria protetta.</span><span class="sxs-lookup"><span data-stu-id="35f87-110">Allocate a thread stack in secure memory.</span></span>

### <a name="prototype"></a><span data-ttu-id="35f87-111">Prototipo</span><span class="sxs-lookup"><span data-stu-id="35f87-111">Prototype</span></span>

```c
UINT tx_thread_secure_stack_allocate(
    TX_THREAD *thread_ptr, 
    ULONG stack_size);
```

### <a name="description"></a><span data-ttu-id="35f87-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="35f87-112">Description</span></span>

<span data-ttu-id="35f87-113">Questo servizio alloca uno stack di dimensioni stack_size byte nella memoria protetta.</span><span class="sxs-lookup"><span data-stu-id="35f87-113">This service allocates a stack of size stack_size bytes in secure memory.</span></span> <span data-ttu-id="35f87-114">Questa funzione deve essere chiamata per ogni thread che chiama funzioni protette.</span><span class="sxs-lookup"><span data-stu-id="35f87-114">This function should be called for every thread that calls secure functions.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="35f87-115">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="35f87-115">Input Parameters</span></span>

- <span data-ttu-id="35f87-116">**thread_ptr** Puntatore al thread creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="35f87-116">**thread_ptr** Pointer to previously created thread.</span></span>

- <span data-ttu-id="35f87-117">**stack_size** Dimensioni dello stack protetto.</span><span class="sxs-lookup"><span data-stu-id="35f87-117">**stack_size** Size of secure stack.</span></span>

### <a name="return-values"></a><span data-ttu-id="35f87-118">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="35f87-118">Return Values</span></span>

- <span data-ttu-id="35f87-119">La richiesta di **TX_SUCCESS** (0x00) è riuscita.</span><span class="sxs-lookup"><span data-stu-id="35f87-119">**TX_SUCCESS** (0x00) Successful request.</span></span>

- <span data-ttu-id="35f87-120">Dimensioni dello stack di **TX_SIZE_ERROR** (0x05) non comprese nell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="35f87-120">**TX_SIZE_ERROR** (0x05) Stack size out of range.</span></span>

- <span data-ttu-id="35f87-121">**TX_THREAD_ERROR** (0x0E) puntatore al thread non valido.</span><span class="sxs-lookup"><span data-stu-id="35f87-121">**TX_THREAD_ERROR** (0x0E) Invalid thread pointer.</span></span>

- <span data-ttu-id="35f87-122">**TX_NO_MEMORY** (0x10) non è in grado di allocare memoria.</span><span class="sxs-lookup"><span data-stu-id="35f87-122">**TX_NO_MEMORY** (0x10) Unable to allocate memory.</span></span>

- <span data-ttu-id="35f87-123">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="35f87-123">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

- <span data-ttu-id="35f87-124">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema è stato compilato per l'esecuzione in modalità protetta.</span><span class="sxs-lookup"><span data-stu-id="35f87-124">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled to run in secure mode.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="35f87-125">Consentito da</span><span class="sxs-lookup"><span data-stu-id="35f87-125">Allowed From</span></span>

<span data-ttu-id="35f87-126">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="35f87-126">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="35f87-127">Esempio</span><span class="sxs-lookup"><span data-stu-id="35f87-127">Example</span></span>

```c
/* Create thread.  */
tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0, pointer, DEMO_STACK_SIZE, 1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);

/* Allocate secure stack so this thread can call secure functions.  */
status = tx_thread_secure_stack_allocate(&thread_0, 256);

/* If status is TX_SUCCESS the request was successful.  */
```

### <a name="see-also"></a><span data-ttu-id="35f87-128">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="35f87-128">See Also</span></span>

<span data-ttu-id="35f87-129">tx_thread_secure_stack_free</span><span class="sxs-lookup"><span data-stu-id="35f87-129">tx_thread_secure_stack_free</span></span>

##  <a name="tx_thread_secure_stack_free"></a><span data-ttu-id="35f87-130">tx_thread_secure_stack_free</span><span class="sxs-lookup"><span data-stu-id="35f87-130">tx_thread_secure_stack_free</span></span>

<span data-ttu-id="35f87-131">Liberare uno stack di thread nella memoria protetta.</span><span class="sxs-lookup"><span data-stu-id="35f87-131">Free a thread stack in secure memory.</span></span> 

### <a name="prototype"></a><span data-ttu-id="35f87-132">Prototipo</span><span class="sxs-lookup"><span data-stu-id="35f87-132">Prototype</span></span>

```c
UINT tx_thread_secure_stack_free(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="35f87-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="35f87-133">Description</span></span>

<span data-ttu-id="35f87-134">Questo servizio libera lo stack sicuro di un thread nella memoria protetta.</span><span class="sxs-lookup"><span data-stu-id="35f87-134">This service frees a thread's secure stack in secure memory.</span></span> <span data-ttu-id="35f87-135">Questa funzione deve essere chiamata se un thread dispone di uno stack sicuro e quando il thread non deve più chiamare funzioni protette o se il thread viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="35f87-135">This function should be called if a thread has a secure stack and when the thread no longer needs to call secure functions or the thread is deleted.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="35f87-136">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="35f87-136">Input Parameters</span></span>

- <span data-ttu-id="35f87-137">**thread_ptr** Puntatore al thread creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="35f87-137">**thread_ptr** Pointer to previously created thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="35f87-138">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="35f87-138">Return Values</span></span>

- <span data-ttu-id="35f87-139">La richiesta di **TX_SUCCESS** (0x00) è riuscita.</span><span class="sxs-lookup"><span data-stu-id="35f87-139">**TX_SUCCESS** (0x00) Successful request.</span></span>

- <span data-ttu-id="35f87-140">**TX_THREAD_ERROR** (0x0E) puntatore al thread non valido.</span><span class="sxs-lookup"><span data-stu-id="35f87-140">**TX_THREAD_ERROR** (0x0E) Invalid thread pointer.</span></span>

- <span data-ttu-id="35f87-141">Il chiamante **TX_CALLER_ERROR** (0X13) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="35f87-141">**TX_CALLER_ERROR** (0x13) Invalid caller of this service.</span></span>

- <span data-ttu-id="35f87-142">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema è stato compilato per l'esecuzione in modalità protetta.</span><span class="sxs-lookup"><span data-stu-id="35f87-142">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was compiled to run in secure mode.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="35f87-143">Consentito da</span><span class="sxs-lookup"><span data-stu-id="35f87-143">Allowed From</span></span>

<span data-ttu-id="35f87-144">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="35f87-144">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="35f87-145">Esempio</span><span class="sxs-lookup"><span data-stu-id="35f87-145">Example</span></span>

```c
/* Free thread’s secure stack.  */
status = tx_thread_secure_stack_free(&thread_0);

/* If status is TX_SUCCESS the request was successful.  */

/* Delete thread.  */
tx_thread_delete(&thread_0);
```

## <a name="see-also"></a><span data-ttu-id="35f87-146">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="35f87-146">See Also</span></span>

<span data-ttu-id="35f87-147">tx_thread_secure_stack_allocate</span><span class="sxs-lookup"><span data-stu-id="35f87-147">tx_thread_secure_stack_allocate</span></span>
