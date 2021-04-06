---
title: Capitolo 2-riferimenti alle API del kit del profilo di esecuzione
description: Questo capitolo documenta le funzioni API fornite da EPK.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a198e48bdacbc141fb3de4670cc7ea5ba079612d
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377601"
---
#  <a name="chapter-2--execution-profile-kit-api-references"></a><span data-ttu-id="69341-103">Capitolo 2 riferimenti all'API del kit del profilo di esecuzione</span><span class="sxs-lookup"><span data-stu-id="69341-103">Chapter 2  Execution Profile Kit API References</span></span>

<span data-ttu-id="69341-104">Il EPK ThreadX fornisce funzioni di accesso per ottenere le informazioni sul profilo di esecuzione, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="69341-104">The ThreadX EPK provides access functions to get the execution profile information, as follows.</span></span>

| <span data-ttu-id="69341-105">&nbsp;Nome funzione</span><span class="sxs-lookup"><span data-stu-id="69341-105">Function&nbsp;Name</span></span> | <span data-ttu-id="69341-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="69341-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69341-107">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-107">_tx_execution_thread_time_reset</span></span> | <span data-ttu-id="69341-108">Reimposta il tempo accumulato per un thread.</span><span class="sxs-lookup"><span data-stu-id="69341-108">Reset the accumulated time for a thread.</span></span> |
| <span data-ttu-id="69341-109">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-109">_tx_execution_thread_total_time_reset</span></span> | <span data-ttu-id="69341-110">Reimposta il tempo totale di thread accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-110">Reset the accumulated total thread time.</span></span> |
| <span data-ttu-id="69341-111">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-111">_tx_execution_isr_time_reset</span></span> | <span data-ttu-id="69341-112">Reimposta il tempo ISR accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-112">Reset the accumulated ISR time.</span></span> |
| <span data-ttu-id="69341-113">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-113">_tx_execution_idle_time_reset</span></span> | <span data-ttu-id="69341-114">Reimposta il tempo di inattività accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-114">Reset the accumulated idle time.</span></span> |
| <span data-ttu-id="69341-115">_tx_execution_thread_time_get ottenere il tempo di accumulo per un thread.</span><span class="sxs-lookup"><span data-stu-id="69341-115">_tx_execution_thread_time_get Get the accumulated time for a thread.</span></span> |
| <span data-ttu-id="69341-116">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-116">_tx_execution_thread_total_time_get</span></span> | <span data-ttu-id="69341-117">Ottiene il tempo totale di thread accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-117">Get the accumulated total thread time.</span></span> |
| <span data-ttu-id="69341-118">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-118">_tx_execution_isr_time_get</span></span> | <span data-ttu-id="69341-119">Ottenere il tempo ISR accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-119">Get the accumulated ISR time.</span></span> |
| <span data-ttu-id="69341-120">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-120">_tx_execution_idle_time_get</span></span> | <span data-ttu-id="69341-121">Ottenere il tempo di inattività accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-121">Get the accumulated idle time.</span></span> |

##  <a name="_tx_execution_thread_time_reset"></a><span data-ttu-id="69341-122">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-122">_tx_execution_thread_time_reset</span></span>

<span data-ttu-id="69341-123">Reimposta il tempo accumulato per un thread.</span><span class="sxs-lookup"><span data-stu-id="69341-123">Reset the accumulated time for a thread.</span></span>

### <a name="prototype"></a><span data-ttu-id="69341-124">Prototipo</span><span class="sxs-lookup"><span data-stu-id="69341-124">Prototype</span></span>

```C
UINT _tx_execution_thread_time_reset(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="69341-125">Descrizione</span><span class="sxs-lookup"><span data-stu-id="69341-125">Description</span></span>

<span data-ttu-id="69341-126">Questo servizio imposta di nuovo il tempo di esecuzione del thread accumulato su zero.</span><span class="sxs-lookup"><span data-stu-id="69341-126">This service sets the accumulated thread execution time back to zero.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="69341-127">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="69341-127">Input Parameters</span></span>

- <span data-ttu-id="69341-128">**thread_ptr** Puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="69341-128">**thread_ptr** Pointer to thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="69341-129">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="69341-129">Return Values</span></span>

- <span data-ttu-id="69341-130">**TX_SUCCESS** (0x00) reimpostazione EPK riuscita.</span><span class="sxs-lookup"><span data-stu-id="69341-130">**TX_SUCCESS** (0x00) Successful EPK reset.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="69341-131">Consentito da</span><span class="sxs-lookup"><span data-stu-id="69341-131">Allowed From</span></span>

<span data-ttu-id="69341-132">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="69341-132">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="69341-133">Esempio</span><span class="sxs-lookup"><span data-stu-id="69341-133">Example</span></span>

```c
/* Reset the execution time for thread_0.  */
status =  tx_execution_thread_time_reset(&thread_0);

/* If status is TX_SUCCESS thread_0's execution time is now 0.  */
```

### <a name="see-also"></a><span data-ttu-id="69341-134">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="69341-134">See Also</span></span>

- <span data-ttu-id="69341-135">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-135">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="69341-136">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-136">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="69341-137">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-137">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="69341-138">tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-138">tx_execution_thread_time_get</span></span>
- <span data-ttu-id="69341-139">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-139">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="69341-140">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-140">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="69341-141">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-141">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_thread_total_time_reset"></a><span data-ttu-id="69341-142">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-142">_tx_execution_thread_total_time_reset</span></span>

<span data-ttu-id="69341-143">Reimposta il tempo totale di thread accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-143">Reset the total accumulated thread time.</span></span>

### <a name="prototype"></a><span data-ttu-id="69341-144">Prototipo</span><span class="sxs-lookup"><span data-stu-id="69341-144">Prototype</span></span>
```c
UINT _tx_execution_thread_total_time_reset(void);
```

### <a name="description"></a><span data-ttu-id="69341-145">Descrizione</span><span class="sxs-lookup"><span data-stu-id="69341-145">Description</span></span>

<span data-ttu-id="69341-146">Questo servizio imposta il tempo totale di esecuzione del thread accumulato su zero.</span><span class="sxs-lookup"><span data-stu-id="69341-146">This service sets the accumulated total thread execution time back to zero.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="69341-147">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="69341-147">Input Parameters</span></span>

<span data-ttu-id="69341-148">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="69341-148">None.</span></span>

### <a name="return-values"></a><span data-ttu-id="69341-149">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="69341-149">Return Values</span></span>

- <span data-ttu-id="69341-150">**TX_SUCCESS** (0x00) reimpostazione EPK riuscita.</span><span class="sxs-lookup"><span data-stu-id="69341-150">**TX_SUCCESS** (0x00) Successful EPK reset.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="69341-151">Consentito da</span><span class="sxs-lookup"><span data-stu-id="69341-151">Allowed From</span></span>

- <span data-ttu-id="69341-152">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="69341-152">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="69341-153">Esempio</span><span class="sxs-lookup"><span data-stu-id="69341-153">Example</span></span>

```c
/* Reset the total execution time for all threads.  */
status =  tx_execution_thread_total_time_reset();

/* If status is TX_SUCCESS the total thread execution time is now 0.  */
```

### <a name="see-also"></a><span data-ttu-id="69341-154">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="69341-154">See Also</span></span>

- <span data-ttu-id="69341-155">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-155">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="69341-156">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-156">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="69341-157">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-157">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="69341-158">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-158">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="69341-159">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-159">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="69341-160">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-160">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="69341-161">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-161">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_isr_time_reset"></a><span data-ttu-id="69341-162">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-162">_tx_execution_isr_time_reset</span></span>

<span data-ttu-id="69341-163">Reimposta il tempo ISR accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-163">Reset the accumulated ISR time.</span></span>

### <a name="prototype"></a><span data-ttu-id="69341-164">Prototipo</span><span class="sxs-lookup"><span data-stu-id="69341-164">Prototype</span></span>

```c
UINT _tx_execution_isr_time_reset(void);
```

### <a name="description"></a><span data-ttu-id="69341-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="69341-165">Description</span></span>

<span data-ttu-id="69341-166">Questo servizio imposta il tempo totale di esecuzione ISR accumulato su zero.</span><span class="sxs-lookup"><span data-stu-id="69341-166">This service sets the accumulated total ISR execution time back to zero.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="69341-167">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="69341-167">Input Parameters</span></span>

<span data-ttu-id="69341-168">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="69341-168">None.</span></span>

### <a name="return-values"></a><span data-ttu-id="69341-169">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="69341-169">Return Values</span></span>

- <span data-ttu-id="69341-170">**TX_SUCCESS** (0x00) reimpostazione EPK riuscita.</span><span class="sxs-lookup"><span data-stu-id="69341-170">**TX_SUCCESS** (0x00) Successful EPK reset.</span></span>

<span data-ttu-id="69341-171">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="69341-171">**Allowed From**</span></span>

- <span data-ttu-id="69341-172">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="69341-172">Threads, timers, and ISRs</span></span>

<span data-ttu-id="69341-173">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="69341-173">**Example**</span></span>

```c
/* Reset the total ISR execution time.  */
status =  tx_execution_isr_time_reset();

/* If status is TX_SUCCESS the total ISR execution time is now 0.  */
```

### <a name="see-also"></a><span data-ttu-id="69341-174">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="69341-174">See Also</span></span>

- <span data-ttu-id="69341-175">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-175">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="69341-176">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-176">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="69341-177">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-177">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="69341-178">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-178">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="69341-179">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-179">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="69341-180">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-180">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="69341-181">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-181">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_idle_time_reset"></a><span data-ttu-id="69341-182">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-182">_tx_execution_idle_time_reset</span></span>

<span data-ttu-id="69341-183">Reimposta il tempo di inattività accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-183">Reset the accumulated idle time.</span></span>

### <a name="prototype"></a><span data-ttu-id="69341-184">Prototipo</span><span class="sxs-lookup"><span data-stu-id="69341-184">Prototype</span></span>

```c
UINT _tx_execution_idle_time_reset(void);
```

### <a name="description"></a><span data-ttu-id="69341-185">Descrizione</span><span class="sxs-lookup"><span data-stu-id="69341-185">Description</span></span>

<span data-ttu-id="69341-186">Questo servizio imposta su zero il tempo di esecuzione totale inattivo accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-186">This service sets the accumulated total idle execution time back to zero.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="69341-187">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="69341-187">Input Parameters</span></span>

<span data-ttu-id="69341-188">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="69341-188">None.</span></span>

### <a name="return-values"></a><span data-ttu-id="69341-189">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="69341-189">Return Values</span></span>

- <span data-ttu-id="69341-190">**TX_SUCCESS** (0x00) reimpostazione EPK riuscita.</span><span class="sxs-lookup"><span data-stu-id="69341-190">**TX_SUCCESS** (0x00) Successful EPK reset.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="69341-191">Consentito da</span><span class="sxs-lookup"><span data-stu-id="69341-191">Allowed From</span></span>

- <span data-ttu-id="69341-192">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="69341-192">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="69341-193">Esempio</span><span class="sxs-lookup"><span data-stu-id="69341-193">Example</span></span>

```c
/* Reset the total idle execution time.  */
status =  tx_execution_idle_time_reset();

/* If status is TX_SUCCESS the total idle execution time is now 0.  */
```

### <a name="see-also"></a><span data-ttu-id="69341-194">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="69341-194">See Also</span></span>

- <span data-ttu-id="69341-195">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-195">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="69341-196">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-196">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="69341-197">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-197">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="69341-198">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-198">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="69341-199">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-199">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="69341-200">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-200">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="69341-201">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-201">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_thread_time_get"></a><span data-ttu-id="69341-202">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-202">_tx_execution_thread_time_get</span></span>

<span data-ttu-id="69341-203">Ottenere il tempo di accumulo per un thread.</span><span class="sxs-lookup"><span data-stu-id="69341-203">Get the accumulated time for a thread.</span></span>

### <a name="prototype"></a><span data-ttu-id="69341-204">Prototipo</span><span class="sxs-lookup"><span data-stu-id="69341-204">Prototype</span></span>

```c
UINT _tx_execution_thread_time_get(
    TX_THREAD *thread_ptr,
    EXECUTION_TIME *total_time);
```

### <a name="description"></a><span data-ttu-id="69341-205">Descrizione</span><span class="sxs-lookup"><span data-stu-id="69341-205">Description</span></span>

<span data-ttu-id="69341-206">Questo servizio ottiene il tempo di esecuzione accumulato per un thread.</span><span class="sxs-lookup"><span data-stu-id="69341-206">This service gets the accumulated execution time for a thread.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="69341-207">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="69341-207">Input Parameters</span></span>

- <span data-ttu-id="69341-208">**thread_ptr** Puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="69341-208">**thread_ptr** Pointer to thread.</span></span>

- <span data-ttu-id="69341-209">**Total_time** Destinazione per \' i tempi di esecuzione del thread.</span><span class="sxs-lookup"><span data-stu-id="69341-209">**total_time** Destination for thread\'s execution time.</span></span>

### <a name="return-values"></a><span data-ttu-id="69341-210">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="69341-210">Return Values</span></span>

- <span data-ttu-id="69341-211">**TX_SUCCESS** (0x00) EPK tempo riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="69341-211">**TX_SUCCESS** (0x00) Successful EPK time get.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="69341-212">Consentito da</span><span class="sxs-lookup"><span data-stu-id="69341-212">Allowed From</span></span>

<span data-ttu-id="69341-213">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="69341-213">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="69341-214">Esempio</span><span class="sxs-lookup"><span data-stu-id="69341-214">Example</span></span>

```c

/* Get the total thread execution time for thread_0.  */
status =  tx_execution_thread_time_get(&thread_0, &execution_time);

/* If status is TX_SUCCESS, execution_time contains the thread's
   execution time.  */
```

### <a name="see-also"></a><span data-ttu-id="69341-215">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="69341-215">See Also</span></span>

- <span data-ttu-id="69341-216">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-216">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="69341-217">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-217">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="69341-218">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-218">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="69341-219">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-219">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="69341-220">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-220">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="69341-221">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-221">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="69341-222">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-222">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_thread_total_time_get"></a><span data-ttu-id="69341-223">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-223">_tx_execution_thread_total_time_get</span></span>

<span data-ttu-id="69341-224">Ottiene il tempo totale di thread accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-224">Get the accumulated thread total time.</span></span>

### <a name="prototype"></a><span data-ttu-id="69341-225">Prototipo</span><span class="sxs-lookup"><span data-stu-id="69341-225">Prototype</span></span>

```c
UINT _tx_execution_thread_total_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a><span data-ttu-id="69341-226">Descrizione</span><span class="sxs-lookup"><span data-stu-id="69341-226">Description</span></span>

<span data-ttu-id="69341-227">Questo servizio ottiene il tempo totale di esecuzione del thread accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-227">This service gets the accumulated total thread execution time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="69341-228">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="69341-228">Input Parameters</span></span>

- <span data-ttu-id="69341-229">**Total_time** Destinazione per il tempo totale di esecuzione del thread.</span><span class="sxs-lookup"><span data-stu-id="69341-229">**total_time** Destination for total thread execution time.</span></span>

### <a name="return-values"></a><span data-ttu-id="69341-230">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="69341-230">Return Values</span></span>

- <span data-ttu-id="69341-231">**TX_SUCCESS** (0x00) EPK tempo riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="69341-231">**TX_SUCCESS** (0x00) Successful EPK time get.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="69341-232">Consentito da</span><span class="sxs-lookup"><span data-stu-id="69341-232">Allowed From</span></span>

- <span data-ttu-id="69341-233">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="69341-233">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="69341-234">Esempio</span><span class="sxs-lookup"><span data-stu-id="69341-234">Example</span></span>

```c
EXECUTION_TIME *execution_time;

/* Get the total thread execution time.  */
status =  tx_execution_thread_total_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the thread
   execution time.  */
```

### <a name="see-also"></a><span data-ttu-id="69341-235">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="69341-235">See Also</span></span>

- <span data-ttu-id="69341-236">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-236">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="69341-237">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-237">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="69341-238">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-238">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="69341-239">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-239">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="69341-240">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-240">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="69341-241">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-241">_tx_execution_isr_time_get</span></span>
- <span data-ttu-id="69341-242">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-242">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_isr_time_get"></a><span data-ttu-id="69341-243">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-243">_tx_execution_isr_time_get</span></span>

<span data-ttu-id="69341-244">Ottenere il tempo ISR accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-244">Get the accumulated ISR time.</span></span>

### <a name="prototype"></a><span data-ttu-id="69341-245">Prototipo</span><span class="sxs-lookup"><span data-stu-id="69341-245">Prototype</span></span>

```c
UINT _tx_execution_isr_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a><span data-ttu-id="69341-246">Descrizione</span><span class="sxs-lookup"><span data-stu-id="69341-246">Description</span></span>

<span data-ttu-id="69341-247">Questo servizio ottiene il tempo di esecuzione ISR accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-247">This service gets the accumulated ISR execution time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="69341-248">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="69341-248">Input Parameters</span></span>

- <span data-ttu-id="69341-249">**Total_time** Destinazione per il tempo di esecuzione ISR totale.</span><span class="sxs-lookup"><span data-stu-id="69341-249">**total_time** Destination for total ISR execution time.</span></span>

### <a name="return-values"></a><span data-ttu-id="69341-250">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="69341-250">Return Values</span></span>

- <span data-ttu-id="69341-251">**TX_SUCCESS** (0x00) EPK tempo riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="69341-251">**TX_SUCCESS** (0x00) Successful EPK time get.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="69341-252">Consentito da</span><span class="sxs-lookup"><span data-stu-id="69341-252">Allowed From</span></span>

<span data-ttu-id="69341-253">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="69341-253">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="69341-254">Esempio</span><span class="sxs-lookup"><span data-stu-id="69341-254">Example</span></span>

```c
EXECUTION_TIME  *execution_time;

/* Get the total ISR execution time.  */
status =  tx_execution_isr_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the ISR
   execution time.  */
```

### <a name="see-also"></a><span data-ttu-id="69341-255">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="69341-255">See Also</span></span>

- <span data-ttu-id="69341-256">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-256">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="69341-257">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-257">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="69341-258">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-258">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="69341-259">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-259">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="69341-260">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-260">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="69341-261">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-261">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="69341-262">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-262">_tx_execution_idle_time_get</span></span>

## <a name="_tx_execution_idle_time_get"></a><span data-ttu-id="69341-263">_tx_execution_idle_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-263">_tx_execution_idle_time_get</span></span>

### <a name="get-the-accumulated-idle-time"></a><span data-ttu-id="69341-264">Ottenere il tempo di inattività accumulato</span><span class="sxs-lookup"><span data-stu-id="69341-264">Get the accumulated idle time</span></span>

### <a name="prototype"></a><span data-ttu-id="69341-265">Prototipo</span><span class="sxs-lookup"><span data-stu-id="69341-265">Prototype</span></span>

```c
UINT _tx_execution_idle_time_get(EXECUTION_TIME *total_time);
```

### <a name="description"></a><span data-ttu-id="69341-266">Descrizione</span><span class="sxs-lookup"><span data-stu-id="69341-266">Description</span></span>

<span data-ttu-id="69341-267">Questo servizio ottiene il tempo di esecuzione inattivo accumulato.</span><span class="sxs-lookup"><span data-stu-id="69341-267">This service gets the accumulated idle execution time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="69341-268">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="69341-268">Input Parameters</span></span>

- <span data-ttu-id="69341-269">**Total_time** Destinazione per il tempo di esecuzione totale di inattività.</span><span class="sxs-lookup"><span data-stu-id="69341-269">**total_time** Destination for total idle execution time.</span></span>

### <a name="return-values"></a><span data-ttu-id="69341-270">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="69341-270">Return Values</span></span>

- <span data-ttu-id="69341-271">**TX_SUCCESS** (0x00) EPK tempo riuscito Get.</span><span class="sxs-lookup"><span data-stu-id="69341-271">**TX_SUCCESS** (0x00) Successful EPK time get.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="69341-272">Consentito da</span><span class="sxs-lookup"><span data-stu-id="69341-272">Allowed From</span></span>

- <span data-ttu-id="69341-273">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="69341-273">Threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="69341-274">Esempio</span><span class="sxs-lookup"><span data-stu-id="69341-274">Example</span></span>

```c
EXECUTION_TIME  *execution_time;

/* Get the total idle execution time.  */
status =  tx_execution_idle_time_get(&execution_time);

/* If status is TX_SUCCESS, execution_time contains the all the idle
   execution time.  */
```

### <a name="see-also"></a><span data-ttu-id="69341-275">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="69341-275">See Also</span></span>

- <span data-ttu-id="69341-276">_tx_execution_thread_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-276">_tx_execution_thread_time_reset</span></span>
- <span data-ttu-id="69341-277">_tx_execution_thread_total_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-277">_tx_execution_thread_total_time_reset</span></span>
- <span data-ttu-id="69341-278">_tx_execution_isr_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-278">_tx_execution_isr_time_reset</span></span>
- <span data-ttu-id="69341-279">_tx_execution_idle_time_reset</span><span class="sxs-lookup"><span data-stu-id="69341-279">_tx_execution_idle_time_reset</span></span>
- <span data-ttu-id="69341-280">_tx_execution_thread_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-280">_tx_execution_thread_time_get</span></span>
- <span data-ttu-id="69341-281">_tx_execution_thread_total_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-281">_tx_execution_thread_total_time_get</span></span>
- <span data-ttu-id="69341-282">_tx_execution_isr_time_get</span><span class="sxs-lookup"><span data-stu-id="69341-282">_tx_execution_isr_time_get</span></span>
