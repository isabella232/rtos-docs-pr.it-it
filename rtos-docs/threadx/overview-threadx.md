---
title: Informazioni Azure RTOS ThreadX
description: Azure ThreadX è un sistema operativo avanzato in tempo reale (RTOS) progettato specificamente per applicazioni con integrazione avanzata.
author: philmea
ms.author: philmea
ms.date: 6/9/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: e786e5bf1f434ec9543823dee8784b677a2b371f
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171387"
---
# <a name="overview-of-azure-rtos-threadx"></a><span data-ttu-id="f686a-103">Panoramica di Azure RTOS ThreadX</span><span class="sxs-lookup"><span data-stu-id="f686a-103">Overview of Azure RTOS ThreadX</span></span>

<span data-ttu-id="f686a-104">Azure RTOS ThreadX è il sistema operativo RTOS (Advanced Industrial Grade Real-Time Operating System) di Microsoft progettato specificamente per applicazioni IoT, real-time e deep embedded.</span><span class="sxs-lookup"><span data-stu-id="f686a-104">Azure RTOS ThreadX is Microsoft's advanced industrial grade Real-Time Operating System (RTOS) designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="f686a-105">Azure RTOS ThreadX offre funzionalità avanzate di pianificazione, comunicazione, sincronizzazione, timer, gestione della memoria e gestione degli interrupt.</span><span class="sxs-lookup"><span data-stu-id="f686a-105">Azure RTOS ThreadX provides advanced scheduling, communication, synchronization, timer, memory management, and interrupt management facilities.</span></span> <span data-ttu-id="f686a-106">Inoltre, Azure RTOS ThreadX ha molte funzionalità avanzate, tra cui il picokernel™ l'architettura, la soglia di preemption™ la pianificazione, il concatenamento di eventi, la profilatura dell'esecuzione ™, le metriche delle prestazioni e la traccia degli eventi di sistema.</span><span class="sxs-lookup"><span data-stu-id="f686a-106">In addition, Azure RTOS ThreadX has many advanced features, including its picokernel™ architecture, preemption-threshold™ scheduling, event-chaining,™ execution profiling, performance metrics, and system event tracing.</span></span> <span data-ttu-id="f686a-107">Insieme alla semplicità d'uso superiore, Azure RTOS ThreadX è la scelta ideale per le applicazioni incorporate più complesse.</span><span class="sxs-lookup"><span data-stu-id="f686a-107">Combined with its superior ease-of-use, Azure RTOS ThreadX is the ideal choice for the most demanding of embedded applications.</span></span> <span data-ttu-id="f686a-108">Dal 2017, Azure RTOS ThreadX ha oltre 6,2 miliardi di distribuzioni, in un'ampia gamma di prodotti, tra cui dispositivi consumer, elettronica medicale e apparecchiature di controllo industriale.</span><span class="sxs-lookup"><span data-stu-id="f686a-108">As of 2017, Azure RTOS ThreadX has over 6.2 billion deployments, in a wide variety of products, including consumer devices, medical electronics, and industrial control equipment.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="f686a-109">Protocolli API</span><span class="sxs-lookup"><span data-stu-id="f686a-109">API Protocols</span></span>

### <a name="azure-rtos-threadx-services"></a><span data-ttu-id="f686a-110">Azure RTOS ThreadX Services</span><span class="sxs-lookup"><span data-stu-id="f686a-110">Azure RTOS ThreadX Services</span></span>

* <span data-ttu-id="f686a-111">Creazione dinamica di thread</span><span class="sxs-lookup"><span data-stu-id="f686a-111">Dynamic thread creation</span></span>
* <span data-ttu-id="f686a-112">Nessun limite al numero di thread</span><span class="sxs-lookup"><span data-stu-id="f686a-112">No limits on the number of threads</span></span>
* <span data-ttu-id="f686a-113">Le API del thread principale includono:</span><span class="sxs-lookup"><span data-stu-id="f686a-113">Main thread APIs include:</span></span>
  * <span data-ttu-id="f686a-114">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f686a-114">tx_thread_create</span></span>
  * <span data-ttu-id="f686a-115">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f686a-115">tx_thread_delete</span></span>
  * <span data-ttu-id="f686a-116">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f686a-116">tx_thread_preemption_change</span></span>
  * <span data-ttu-id="f686a-117">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f686a-117">tx_thread_priority_change</span></span>
  * <span data-ttu-id="f686a-118">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f686a-118">tx_thread_relinquish</span></span>
  * <span data-ttu-id="f686a-119">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f686a-119">tx_thread_reset</span></span>
  * <span data-ttu-id="f686a-120">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f686a-120">tx_thread_resume</span></span>
  * <span data-ttu-id="f686a-121">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f686a-121">tx_thread_sleep</span></span>
  * <span data-ttu-id="f686a-122">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f686a-122">tx_thread_suspend</span></span>
  * <span data-ttu-id="f686a-123">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f686a-123">tx_thread_terminate</span></span>
  * <span data-ttu-id="f686a-124">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f686a-124">tx_thread_wait_abort</span></span>
* <span data-ttu-id="f686a-125">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="f686a-125">Additional information and performance APIs</span></span>

### <a name="message-queues"></a><span data-ttu-id="f686a-126">Code di messaggi</span><span class="sxs-lookup"><span data-stu-id="f686a-126">Message Queues</span></span>

* <span data-ttu-id="f686a-127">Creazione dinamica della coda</span><span class="sxs-lookup"><span data-stu-id="f686a-127">Dynamic queue creation</span></span>
* <span data-ttu-id="f686a-128">Nessun limite al numero di code</span><span class="sxs-lookup"><span data-stu-id="f686a-128">No limits on the number of queues</span></span>
* <span data-ttu-id="f686a-129">Messaggi copiati per valore (o per riferimento tramite puntatore)</span><span class="sxs-lookup"><span data-stu-id="f686a-129">Messages copied by value (or by reference via pointer)</span></span>
* <span data-ttu-id="f686a-130">Dimensioni dei messaggi da 1 a 16 parole a 32 bit</span><span class="sxs-lookup"><span data-stu-id="f686a-130">Message sizes from 1 to 16 32-bit words</span></span>
* <span data-ttu-id="f686a-131">Sospensione di thread facoltativa in modalità vuota e completa</span><span class="sxs-lookup"><span data-stu-id="f686a-131">Optional thread suspension on empty and full</span></span>
* <span data-ttu-id="f686a-132">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="f686a-132">Optional timeout on all suspension</span></span>
* <span data-ttu-id="f686a-133">Le API principali della coda di messaggi includono:</span><span class="sxs-lookup"><span data-stu-id="f686a-133">Main message queue APIs include:</span></span>
  * <span data-ttu-id="f686a-134">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f686a-134">tx_queue_create</span></span>
  * <span data-ttu-id="f686a-135">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f686a-135">tx_queue_delete</span></span>
  * <span data-ttu-id="f686a-136">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f686a-136">tx_queue_flush</span></span>
  * <span data-ttu-id="f686a-137">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f686a-137">tx_queue_front_send</span></span>
  * <span data-ttu-id="f686a-138">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f686a-138">tx_queue_receive</span></span>
  * <span data-ttu-id="f686a-139">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f686a-139">tx_queue_send_notify</span></span>
* <span data-ttu-id="f686a-140">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="f686a-140">Additional information and performance APIs</span></span>

### <a name="counting-semaphores"></a><span data-ttu-id="f686a-141">Conteggio dei semafori</span><span class="sxs-lookup"><span data-stu-id="f686a-141">Counting Semaphores</span></span>

* <span data-ttu-id="f686a-142">Creazione dinamica del semaforo</span><span class="sxs-lookup"><span data-stu-id="f686a-142">Dynamic semaphore creation</span></span>
* <span data-ttu-id="f686a-143">Nessun limite al numero di semafori</span><span class="sxs-lookup"><span data-stu-id="f686a-143">No limits on the number of semaphores</span></span>
* <span data-ttu-id="f686a-144">Semafori di conteggio a 32 bit (da 0 a 4.294.967.295)</span><span class="sxs-lookup"><span data-stu-id="f686a-144">32-bit counting semaphores (0 to 4,294,967,295)</span></span>
* <span data-ttu-id="f686a-145">Supporta la protezione dei consumer-producer o delle risorse</span><span class="sxs-lookup"><span data-stu-id="f686a-145">Supports consumer-producer or resource protection</span></span>
* <span data-ttu-id="f686a-146">Sospensione del thread facoltativa quando il semaforo non è disponibile</span><span class="sxs-lookup"><span data-stu-id="f686a-146">Optional thread suspension when semaphore unavailable</span></span>
* <span data-ttu-id="f686a-147">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="f686a-147">Optional timeout on all suspension</span></span>
* <span data-ttu-id="f686a-148">Le PRINCIPALI API del semaforo includono:</span><span class="sxs-lookup"><span data-stu-id="f686a-148">Main semaphore APIs include:</span></span>
  * <span data-ttu-id="f686a-149">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="f686a-149">tx_semaphore_create</span></span>
  * <span data-ttu-id="f686a-150">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="f686a-150">tx_semaphore_delete</span></span>
  * <span data-ttu-id="f686a-151">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="f686a-151">tx_semaphore_get</span></span>
  * <span data-ttu-id="f686a-152">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="f686a-152">tx_semaphore_put</span></span>
  * <span data-ttu-id="f686a-153">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="f686a-153">tx_semaphore_put_notify</span></span>
* <span data-ttu-id="f686a-154">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="f686a-154">Additional information and performance APIs</span></span>

### <a name="mutexes"></a><span data-ttu-id="f686a-155">Mutex</span><span class="sxs-lookup"><span data-stu-id="f686a-155">Mutexes</span></span>

* <span data-ttu-id="f686a-156">Creazione dinamica di mutex</span><span class="sxs-lookup"><span data-stu-id="f686a-156">Dynamic mutex creation</span></span>
* <span data-ttu-id="f686a-157">Nessun limite al numero di mutex</span><span class="sxs-lookup"><span data-stu-id="f686a-157">No limits on the number of mutexes</span></span>
* <span data-ttu-id="f686a-158">Protezione delle risorse annidate supportata</span><span class="sxs-lookup"><span data-stu-id="f686a-158">Nested resource protection supported</span></span>
* <span data-ttu-id="f686a-159">Ereditarietà della priorità facoltativa supportata</span><span class="sxs-lookup"><span data-stu-id="f686a-159">Optional priority inheritance supported</span></span>
* <span data-ttu-id="f686a-160">Sospensione del thread facoltativa quando mutex non disponibile</span><span class="sxs-lookup"><span data-stu-id="f686a-160">Optional thread suspension when mutex unavailable</span></span>
* <span data-ttu-id="f686a-161">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="f686a-161">Optional timeout on all suspension</span></span>
* <span data-ttu-id="f686a-162">Le PRINCIPALI API mutex includono:</span><span class="sxs-lookup"><span data-stu-id="f686a-162">Main mutex APIs include:</span></span>
  * <span data-ttu-id="f686a-163">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="f686a-163">tx_mutex_create</span></span>
  * <span data-ttu-id="f686a-164">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="f686a-164">tx_mutex_delete</span></span>
  * <span data-ttu-id="f686a-165">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="f686a-165">tx_mutex_get</span></span>
  * <span data-ttu-id="f686a-166">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="f686a-166">tx_mutex_put</span></span>
* <span data-ttu-id="f686a-167">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="f686a-167">Additional information and performance APIs</span></span>

### <a name="event-flags"></a><span data-ttu-id="f686a-168">Flag di evento</span><span class="sxs-lookup"><span data-stu-id="f686a-168">Event Flags</span></span>

* <span data-ttu-id="f686a-169">Creazione di gruppi di flag di eventi dinamici</span><span class="sxs-lookup"><span data-stu-id="f686a-169">Dynamic event flag group creation</span></span>
* <span data-ttu-id="f686a-170">Nessun limite al numero di gruppi di flag di eventi</span><span class="sxs-lookup"><span data-stu-id="f686a-170">No limits on the number of event flag groups</span></span>
* <span data-ttu-id="f686a-171">Sincronizzazione di uno o più thread</span><span class="sxs-lookup"><span data-stu-id="f686a-171">Synchronization of one thread or multiple threads</span></span>
* <span data-ttu-id="f686a-172">Supporto di operazioni get e clear atomiche</span><span class="sxs-lookup"><span data-stu-id="f686a-172">Atomic get and clear supported</span></span>
* <span data-ttu-id="f686a-173">Sospensione multithread facoltativa nel set di eventi AND/OR</span><span class="sxs-lookup"><span data-stu-id="f686a-173">Optional multithread suspension on AND/OR set of events</span></span>
* <span data-ttu-id="f686a-174">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="f686a-174">Optional timeout on all suspension</span></span>
* <span data-ttu-id="f686a-175">Le API dei flag di eventi principali includono:</span><span class="sxs-lookup"><span data-stu-id="f686a-175">Main event flag APIs include:</span></span>
  * <span data-ttu-id="f686a-176">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="f686a-176">tx_event_flags_create</span></span>
  * <span data-ttu-id="f686a-177">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="f686a-177">tx_event_flags_delete</span></span>
  * <span data-ttu-id="f686a-178">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="f686a-178">tx_event_flags_get</span></span>
  * <span data-ttu-id="f686a-179">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="f686a-179">tx_event_flags_set</span></span>
  * <span data-ttu-id="f686a-180">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="f686a-180">tx_event_flags_set_notify</span></span>
* <span data-ttu-id="f686a-181">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="f686a-181">Additional information and performance APIs</span></span>

### <a name="block-memory-pools"></a><span data-ttu-id="f686a-182">Bloccare i pool di memoria</span><span class="sxs-lookup"><span data-stu-id="f686a-182">Block Memory Pools</span></span>

* <span data-ttu-id="f686a-183">Creazione dinamica del pool a blocchi</span><span class="sxs-lookup"><span data-stu-id="f686a-183">Dynamic block pool creation</span></span>
* <span data-ttu-id="f686a-184">Nessun limite al numero di pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="f686a-184">No limits on the number of block pools</span></span>
* <span data-ttu-id="f686a-185">Nessun limite alle dimensioni dei blocchi di dimensioni fisse o delle dimensioni del pool</span><span class="sxs-lookup"><span data-stu-id="f686a-185">No limits on size of fixed-size blocks or size of pool</span></span>
* <span data-ttu-id="f686a-186">Più veloce possibile allocazione di memoria/deal-location</span><span class="sxs-lookup"><span data-stu-id="f686a-186">Fastest possible memory allocation/deal-location</span></span>
* <span data-ttu-id="f686a-187">Sospensione facoltativa dei thread nel pool vuoto</span><span class="sxs-lookup"><span data-stu-id="f686a-187">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="f686a-188">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="f686a-188">Optional timeout on all suspension</span></span>
* <span data-ttu-id="f686a-189">Le API principali del pool di blocchi includono:</span><span class="sxs-lookup"><span data-stu-id="f686a-189">Main block pool APIs include:</span></span>
  * <span data-ttu-id="f686a-190">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="f686a-190">tx_block_pool_create</span></span>
  * <span data-ttu-id="f686a-191">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f686a-191">tx_block_pool_delete</span></span>
  * <span data-ttu-id="f686a-192">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="f686a-192">tx_block_allocate</span></span>
  * <span data-ttu-id="f686a-193">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="f686a-193">tx_block_release</span></span>
* <span data-ttu-id="f686a-194">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="f686a-194">Additional information and performance APIs</span></span>

### <a name="byte-memory-pools"></a><span data-ttu-id="f686a-195">Pool di memoria di byte</span><span class="sxs-lookup"><span data-stu-id="f686a-195">Byte Memory Pools</span></span>

* <span data-ttu-id="f686a-196">Creazione dinamica del pool di byte</span><span class="sxs-lookup"><span data-stu-id="f686a-196">Dynamic byte pool creation</span></span>
* <span data-ttu-id="f686a-197">Nessun limite al numero di pool di byte</span><span class="sxs-lookup"><span data-stu-id="f686a-197">No limits on the number of byte pools</span></span>
* <span data-ttu-id="f686a-198">Nessun limite alle dimensioni del pool di byte</span><span class="sxs-lookup"><span data-stu-id="f686a-198">No limits on size of byte pool</span></span>
* <span data-ttu-id="f686a-199">Allocazione/deallocazione di memoria a lunghezza variabile più flessibile</span><span class="sxs-lookup"><span data-stu-id="f686a-199">Most flexible variable-length memory allocation/deallocation</span></span>
* <span data-ttu-id="f686a-200">Località delle dimensioni di allocazione supportata</span><span class="sxs-lookup"><span data-stu-id="f686a-200">Allocation size locality supported</span></span>
* <span data-ttu-id="f686a-201">Sospensione facoltativa dei thread in un pool vuoto</span><span class="sxs-lookup"><span data-stu-id="f686a-201">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="f686a-202">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="f686a-202">Optional timeout on all suspension</span></span>
* <span data-ttu-id="f686a-203">Le API principali del pool di byte includono:</span><span class="sxs-lookup"><span data-stu-id="f686a-203">Main byte pool APIs include:</span></span>
  * <span data-ttu-id="f686a-204">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="f686a-204">tx_byte_pool_create</span></span>
  * <span data-ttu-id="f686a-205">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f686a-205">tx_byte_pool_delete</span></span>
  * <span data-ttu-id="f686a-206">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="f686a-206">tx_byte_allocate</span></span>
  * <span data-ttu-id="f686a-207">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="f686a-207">tx_byte_release</span></span>
* <span data-ttu-id="f686a-208">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="f686a-208">Additional information and performance APIs</span></span>

### <a name="application-timers"></a><span data-ttu-id="f686a-209">Timer dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f686a-209">Application Timers</span></span>

* <span data-ttu-id="f686a-210">Creazione dinamica del timer</span><span class="sxs-lookup"><span data-stu-id="f686a-210">Dynamic timer creation</span></span>
* <span data-ttu-id="f686a-211">Nessun limite al numero di timer</span><span class="sxs-lookup"><span data-stu-id="f686a-211">No limits on the number of timers</span></span>
* <span data-ttu-id="f686a-212">Timer periodici o one-shot supportati</span><span class="sxs-lookup"><span data-stu-id="f686a-212">Periodic or one-shot timers supported</span></span>
* <span data-ttu-id="f686a-213">I timer periodici possono avere un valore di scadenza iniziale diverso</span><span class="sxs-lookup"><span data-stu-id="f686a-213">Periodic timers may have different initial expiration value</span></span>
* <span data-ttu-id="f686a-214">Nessuna ricerca nell'attivazione o disattivazione del timer</span><span class="sxs-lookup"><span data-stu-id="f686a-214">No searching on timer activation or deactivation</span></span>
* <span data-ttu-id="f686a-215">Tutti i timer guidati da un interrupt timer hardware</span><span class="sxs-lookup"><span data-stu-id="f686a-215">All timers driven from one hardware timer interrupt</span></span>
* <span data-ttu-id="f686a-216">Le API principali del timer includono:</span><span class="sxs-lookup"><span data-stu-id="f686a-216">Main timer APIs include:</span></span>
  * <span data-ttu-id="f686a-217">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="f686a-217">tx_timer_create</span></span>
  * <span data-ttu-id="f686a-218">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="f686a-218">tx_timer_delete</span></span>
  * <span data-ttu-id="f686a-219">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="f686a-219">tx_timer_activate</span></span>
  * <span data-ttu-id="f686a-220">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="f686a-220">tx_timer_change</span></span>
  * <span data-ttu-id="f686a-221">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="f686a-221">tx_timer_deactivate</span></span>
* <span data-ttu-id="f686a-222">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="f686a-222">Additional information and performance APIs</span></span>

### <a name="azure-rtos-threadx-core-scheduler"></a><span data-ttu-id="f686a-223">Azure RTOS ThreadX Core Scheduler</span><span class="sxs-lookup"><span data-stu-id="f686a-223">Azure RTOS ThreadX Core Scheduler</span></span>

* <span data-ttu-id="f686a-224">Footprint minimo di RAM da 2 KB FLASH, 1 KB</span><span class="sxs-lookup"><span data-stu-id="f686a-224">Minimal 2KB FLASH,1KB RAM footprint</span></span>
* <span data-ttu-id="f686a-225">Cambio di contesto rapido e secondario</span><span class="sxs-lookup"><span data-stu-id="f686a-225">Fast, sub-microsecond context-switch</span></span>
* <span data-ttu-id="f686a-226">Completamente deterministico indipendentemente dal numero di thread</span><span class="sxs-lookup"><span data-stu-id="f686a-226">Fully deterministic regardless of number of threads</span></span>
* <span data-ttu-id="f686a-227">Pianificazione preventiva basata sulla priorità</span><span class="sxs-lookup"><span data-stu-id="f686a-227">Priority-based, fully preemptive-scheduling</span></span>
* <span data-ttu-id="f686a-228">32 livelli di priorità predefiniti, facoltativamente fino a 1024 livelli</span><span class="sxs-lookup"><span data-stu-id="f686a-228">32 default priority levels, optionally up to 1024 levels</span></span>
* <span data-ttu-id="f686a-229">Pianificazione cooperativa entro il livello di priorità (FIFO)</span><span class="sxs-lookup"><span data-stu-id="f686a-229">Cooperative scheduling within priority level (FIFO)</span></span>
* <span data-ttu-id="f686a-230">Tecnologia preemption-threshold</span><span class="sxs-lookup"><span data-stu-id="f686a-230">Preemption-threshold technology</span></span>
* <span data-ttu-id="f686a-231">Servizi timer facoltativi, tra cui:</span><span class="sxs-lookup"><span data-stu-id="f686a-231">Optional timer services, including:</span></span>
  * <span data-ttu-id="f686a-232">Intervallo di tempo facoltativo per thread</span><span class="sxs-lookup"><span data-stu-id="f686a-232">Per-thread optional time-slice</span></span>
  * <span data-ttu-id="f686a-233">Timeout facoltativo per tutti i blocchi</span><span class="sxs-lookup"><span data-stu-id="f686a-233">Optional timeout on all blocking</span></span>
  * <span data-ttu-id="f686a-234">LE API richiedono l'interrupt del timer hardware</span><span class="sxs-lookup"><span data-stu-id="f686a-234">APIs Requires on hardware timer interrupt</span></span>
* <span data-ttu-id="f686a-235">Profilatura dell'esecuzione</span><span class="sxs-lookup"><span data-stu-id="f686a-235">Execution profiling</span></span>
* <span data-ttu-id="f686a-236">Traccia a livello di sistema</span><span class="sxs-lookup"><span data-stu-id="f686a-236">System-level Trace</span></span>
* <span data-ttu-id="f686a-237">Sicurezza certificata per molti standard</span><span class="sxs-lookup"><span data-stu-id="f686a-237">Safety certified to many standards</span></span>

## <a name="most-deployed-rtos"></a><span data-ttu-id="f686a-238">RTOS più distribuito</span><span class="sxs-lookup"><span data-stu-id="f686a-238">Most deployed RTOS</span></span>

<span data-ttu-id="f686a-239">Azure RTOS ThreadX ha oltre 6,2 miliardi di distribuzioni in tutto il mondo, secondo la società leader di intelligence di mercato M2M, VDC Research.</span><span class="sxs-lookup"><span data-stu-id="f686a-239">Azure RTOS ThreadX has over 6.2 billion deployments worldwide, according to the leading M2M market intelligence firm, VDC Research.</span></span> <span data-ttu-id="f686a-240">La popolarità di Azure RTOS ThreadX è un esempio di affidabilità, qualità, dimensioni, prestazioni, funzionalità avanzate, facilità d'uso e vantaggi complessivi del time-to-market.</span><span class="sxs-lookup"><span data-stu-id="f686a-240">The popularity of Azure RTOS ThreadX is a testament to its reliability, quality, size, performance, advanced features, ease-of-use, and overall time-to-market advantages.</span></span>

> <span data-ttu-id="f686a-241">*"Abbiamo seguito la crescita di THREADX nei mercati wireless e IoT fin dalla sua creazione e siamo sempre più impressionati dall'adozione diffusa di THREADX nel settore".*</span><span class="sxs-lookup"><span data-stu-id="f686a-241">*“We have followed the growth trajectory of THREADX in the wireless and IoT markets since the company’s founding, and are increasingly impressed by the widespread industry adoption of THREADX.”*</span></span> <span data-ttu-id="f686a-242">– Chris Rommel, Executive Vice President, VDC Research</span><span class="sxs-lookup"><span data-stu-id="f686a-242">– Chris Rommel, Executive Vice President, VDC Research</span></span>

## <a name="small-footprint"></a><span data-ttu-id="f686a-243">Ingombro</span><span class="sxs-lookup"><span data-stu-id="f686a-243">Small footprint</span></span>

<span data-ttu-id="f686a-244">Azure RTOS ThreadX richiede un'area di istruzioni di 2 KB notevolmente ridotta e 1 KB di RAM per il footprint minimo.</span><span class="sxs-lookup"><span data-stu-id="f686a-244">Azure RTOS ThreadX requires a remarkably small 2KB instruction area and 1KB of RAM for its minimal footprint.</span></span> <span data-ttu-id="f686a-245">Ciò è dovuto in gran parte all'architettura a ™ a più livelli e alla scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="f686a-245">This is largely due to its non-layered picokernel™ architecture and automatic scaling.</span></span> <span data-ttu-id="f686a-246">Il ridimensionamento automatico significa che solo i servizi (e l'infrastruttura di supporto) usati dall'applicazione vengono inclusi nell'immagine finale in fase di collegamento.</span><span class="sxs-lookup"><span data-stu-id="f686a-246">Automatic scaling means that only the services (and supporting infrastructure) used by the application are included in the final image at link time.</span></span>

<span data-ttu-id="f686a-247">Ecco alcune caratteristiche tipiche delle Azure RTOS ThreadX.</span><span class="sxs-lookup"><span data-stu-id="f686a-247">Here are some typical Azure RTOS ThreadX size characteristics.</span></span>

|<span data-ttu-id="f686a-248">Azure RTOS ThreadX Service</span><span class="sxs-lookup"><span data-stu-id="f686a-248">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="f686a-249">Dimensioni tipiche in byte</span><span class="sxs-lookup"><span data-stu-id="f686a-249">Typical Size in Bytes</span></span>  |
|---------|---------|
|<span data-ttu-id="f686a-250">Servizi di base (richiesta)</span><span class="sxs-lookup"><span data-stu-id="f686a-250">Core Services (Require)</span></span> |<span data-ttu-id="f686a-251">2.000</span><span class="sxs-lookup"><span data-stu-id="f686a-251">2,000</span></span>  |
|<span data-ttu-id="f686a-252">Servizi di accodamento</span><span class="sxs-lookup"><span data-stu-id="f686a-252">Queue Services</span></span>  |<span data-ttu-id="f686a-253">900</span><span class="sxs-lookup"><span data-stu-id="f686a-253">900</span></span>  |
|<span data-ttu-id="f686a-254">Servizi flag di evento</span><span class="sxs-lookup"><span data-stu-id="f686a-254">Event Flag Services</span></span>  |<span data-ttu-id="f686a-255">900</span><span class="sxs-lookup"><span data-stu-id="f686a-255">900</span></span>  |
|<span data-ttu-id="f686a-256">Servizi semafori</span><span class="sxs-lookup"><span data-stu-id="f686a-256">Semaphore Services</span></span>  |<span data-ttu-id="f686a-257">450</span><span class="sxs-lookup"><span data-stu-id="f686a-257">450</span></span>  |
|<span data-ttu-id="f686a-258">Servizi mutex</span><span class="sxs-lookup"><span data-stu-id="f686a-258">Mutex Services</span></span>  |<span data-ttu-id="f686a-259">1.200</span><span class="sxs-lookup"><span data-stu-id="f686a-259">1,200</span></span>  |
|<span data-ttu-id="f686a-260">Servizi di memoria a blocchi</span><span class="sxs-lookup"><span data-stu-id="f686a-260">Block Memory Services</span></span>  |<span data-ttu-id="f686a-261">550</span><span class="sxs-lookup"><span data-stu-id="f686a-261">550</span></span>  |
|<span data-ttu-id="f686a-262">Servizi byte memory</span><span class="sxs-lookup"><span data-stu-id="f686a-262">Byte Memory Services</span></span>  |<span data-ttu-id="f686a-263">900</span><span class="sxs-lookup"><span data-stu-id="f686a-263">900</span></span>  |

## <a name="fast-execution"></a><span data-ttu-id="f686a-264">Esecuzione rapida</span><span class="sxs-lookup"><span data-stu-id="f686a-264">Fast execution</span></span>

<span data-ttu-id="f686a-265">Azure RTOS ThreadX ottiene un cambio di contesto di sottosecondo nei processori più diffusi ed è notevolmente più veloce rispetto ad altri RTOS commerciali.</span><span class="sxs-lookup"><span data-stu-id="f686a-265">Azure RTOS ThreadX achieves a sub-microsecond context switch on most popular processors and is significantly faster overall than other commercial RTOSes.</span></span> <span data-ttu-id="f686a-266">Oltre a essere veloce, Azure RTOS ThreadX è altamente deterministico.</span><span class="sxs-lookup"><span data-stu-id="f686a-266">In addition to being fast, Azure RTOS ThreadX is also highly deterministic.</span></span> <span data-ttu-id="f686a-267">Consente di ottenere le stesse prestazioni veloci, sia che siano disponibili 200 thread o solo uno.</span><span class="sxs-lookup"><span data-stu-id="f686a-267">It achieves the same fast performance whether there are 200 threads ready, or just one.</span></span>

<span data-ttu-id="f686a-268">Ecco alcune caratteristiche tipiche delle prestazioni di Azure RTOS ThreadX:</span><span class="sxs-lookup"><span data-stu-id="f686a-268">Here are some typical performance characteristics of Azure RTOS ThreadX:</span></span>

* <span data-ttu-id="f686a-269">Avvio rapido: Azure RTOS ThreadX viene avviato in meno di 120 cicli.</span><span class="sxs-lookup"><span data-stu-id="f686a-269">Fast Boot: Azure RTOS ThreadX boots in less than 120 cycles.</span></span>
* <span data-ttu-id="f686a-270">Rimozione facoltativa del controllo degli errori di base: è Azure RTOS controllo degli errori ThreadX di base può essere ignorato in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="f686a-270">Optional Removal of basic error checking: Basic Azure RTOS ThreadX error checking can be skipped at compile time.</span></span> <span data-ttu-id="f686a-271">Ciò può essere utile quando il codice dell'applicazione viene verificato e non richiede più il controllo degli errori per ogni parametro.</span><span class="sxs-lookup"><span data-stu-id="f686a-271">This can be useful when the application code is verified and no longer requires error checking on each parameter.</span></span> <span data-ttu-id="f686a-272">Si noti che questa operazione può essere eseguita su un'unità di compilazione, anziché a livello di sistema.</span><span class="sxs-lookup"><span data-stu-id="f686a-272">Note that this can be done on a compilation unit, rather than system-wide.</span></span>
* <span data-ttu-id="f686a-273">Picokernel™ Progettazione: i servizi non sono a livelli l'uno sull'altro, eliminando così l'overhead delle chiamate di funzione non necessarie.</span><span class="sxs-lookup"><span data-stu-id="f686a-273">Picokernel™ Design: Services are not layered on each other, thus eliminating unnecessary function call overhead.</span></span>
* <span data-ttu-id="f686a-274">\*Elaborazione interrupt ottimizzata: solo i registri scratch vengono salvati/ripristinati al momento dell'ingresso/uscita di ISR, a meno che non sia necessaria la precedenza.</span><span class="sxs-lookup"><span data-stu-id="f686a-274">\*Optimized Interrupt Processing: Only scratch registers are saved/restored upon ISR entry/exit, unless preemption is necessary.</span></span>
* <span data-ttu-id="f686a-275">Elaborazione API ottimizzata:</span><span class="sxs-lookup"><span data-stu-id="f686a-275">Optimized API Processing:</span></span>

    |<span data-ttu-id="f686a-276">Azure RTOS servizio ThreadX</span><span class="sxs-lookup"><span data-stu-id="f686a-276">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="f686a-277">Tempo di servizio in microsecondi\*</span><span class="sxs-lookup"><span data-stu-id="f686a-277">Service Time in Microseconds\*</span></span>  |
    |---------|---------|
    |<span data-ttu-id="f686a-278">Sospensione dei thread</span><span class="sxs-lookup"><span data-stu-id="f686a-278">Thread Suspend</span></span>  |<span data-ttu-id="f686a-279">0,6</span><span class="sxs-lookup"><span data-stu-id="f686a-279">0.6</span></span>  |
    |<span data-ttu-id="f686a-280">Ripresa di thread</span><span class="sxs-lookup"><span data-stu-id="f686a-280">Thread Resume</span></span>  |<span data-ttu-id="f686a-281">0,6</span><span class="sxs-lookup"><span data-stu-id="f686a-281">0.6</span></span>  |
    |<span data-ttu-id="f686a-282">Invio in coda</span><span class="sxs-lookup"><span data-stu-id="f686a-282">Queue Send</span></span>  |<span data-ttu-id="f686a-283">0,3</span><span class="sxs-lookup"><span data-stu-id="f686a-283">0.3</span></span>  |
    |<span data-ttu-id="f686a-284">Ricezione coda</span><span class="sxs-lookup"><span data-stu-id="f686a-284">Queue Receive</span></span>  |<span data-ttu-id="f686a-285">0,3</span><span class="sxs-lookup"><span data-stu-id="f686a-285">0.3</span></span>  |
    |<span data-ttu-id="f686a-286">Ottenere un semaforo</span><span class="sxs-lookup"><span data-stu-id="f686a-286">Get Semaphore</span></span>  |<span data-ttu-id="f686a-287">0,2</span><span class="sxs-lookup"><span data-stu-id="f686a-287">0.2</span></span>  |
    |<span data-ttu-id="f686a-288">Inserire un semaforo</span><span class="sxs-lookup"><span data-stu-id="f686a-288">Put Semaphore</span></span>  |<span data-ttu-id="f686a-289">0,2</span><span class="sxs-lookup"><span data-stu-id="f686a-289">0.2</span></span>  |
    |<span data-ttu-id="f686a-290">Cambio di contesto</span><span class="sxs-lookup"><span data-stu-id="f686a-290">Context Switch</span></span>  |<span data-ttu-id="f686a-291">0,4</span><span class="sxs-lookup"><span data-stu-id="f686a-291">0.4</span></span>  |
    |<span data-ttu-id="f686a-292">Risposta di interrupt</span><span class="sxs-lookup"><span data-stu-id="f686a-292">Interrupt Response</span></span>  |<span data-ttu-id="f686a-293">0.0 – 0.6</span><span class="sxs-lookup"><span data-stu-id="f686a-293">0.0 – 0.6</span></span>  |

    <span data-ttu-id="f686a-294">\**Dati sulle prestazioni basati sul processore tipico in esecuzione a 200 MHz.*</span><span class="sxs-lookup"><span data-stu-id="f686a-294">\**Performance figures based on typical processor running at 200MHz*.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="f686a-295">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="f686a-295">Advanced technology</span></span>

<span data-ttu-id="f686a-296">Azure RTOS ThreadX è una tecnologia avanzata la cui funzionalità più importante è la pianificazione della soglia di priorità.</span><span class="sxs-lookup"><span data-stu-id="f686a-296">Azure RTOS ThreadX is advanced technology whose most notable feature is preemption-threshold scheduling.</span></span> <span data-ttu-id="f686a-297">Questa funzionalità è univoca per Azure RTOS ThreadX ed è stata oggetto di ricerche accademiche approfondite.</span><span class="sxs-lookup"><span data-stu-id="f686a-297">This feature is unique to Azure RTOS ThreadX and has been the subject of extensive academic research.</span></span> <span data-ttu-id="f686a-298">Ad esempio, vedere [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf)(Pianificazione di attività di Fixed-Priority con soglia di preemption), di Yun Wang, Concordia University e Manas Sakslde, University of University of Bayh.</span><span class="sxs-lookup"><span data-stu-id="f686a-298">For example, see [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf), by Yun Wang, Concordia University, and Manas Saksena, University of Pittsburgh.</span></span>

<span data-ttu-id="f686a-299">Considerare le funzionalità di Azure RTOS ThreadX.</span><span class="sxs-lookup"><span data-stu-id="f686a-299">Consider the capabilities of Azure RTOS ThreadX.</span></span>

* <span data-ttu-id="f686a-300">Funzionalità complete e complete per il multitasking</span><span class="sxs-lookup"><span data-stu-id="f686a-300">Complete and Comprehensive Multitasking Facilities</span></span>
  * <span data-ttu-id="f686a-301">Thread, timer dell'applicazione, code di messaggi, semafori di conteggio, mutex, flag di eventi, pool di memoria di blocchi e byte</span><span class="sxs-lookup"><span data-stu-id="f686a-301">Threads, application timers, message queues, counting semaphores, mutexes, event flags, block and byte memory pools</span></span>
* <span data-ttu-id="f686a-302">Priority-Based preemptive</span><span class="sxs-lookup"><span data-stu-id="f686a-302">Priority-Based Preemptive Scheduling</span></span>
* <span data-ttu-id="f686a-303">Flessibilità di priorità: fino a 1024 livelli di priorità</span><span class="sxs-lookup"><span data-stu-id="f686a-303">Priority Flexibility – Up to 1024 Priority Levels</span></span>
* <span data-ttu-id="f686a-304">Pianificazione cooperativa</span><span class="sxs-lookup"><span data-stu-id="f686a-304">Cooperative Scheduling</span></span>
* <span data-ttu-id="f686a-305">Preemption-Threshold™: univoco per Azure RTOS ThreadX, consente di ridurre i commutatori di contesto e di garantire la pianificazione (in base alla ricerca accademica)</span><span class="sxs-lookup"><span data-stu-id="f686a-305">Preemption-Threshold™ – Unique to Azure RTOS ThreadX, helps reduce context switches and help guarantee schedulability (per academic research)</span></span>
* <span data-ttu-id="f686a-306">Protezione della memoria tramite Azure RTOS ThreadX MODULES</span><span class="sxs-lookup"><span data-stu-id="f686a-306">Memory Protection via Azure RTOS ThreadX MODULES</span></span>
* <span data-ttu-id="f686a-307">Completamente deterministico</span><span class="sxs-lookup"><span data-stu-id="f686a-307">Fully Deterministic</span></span>
* <span data-ttu-id="f686a-308">Traccia eventi: acquisisce gli ultimi *n* eventi di sistema/applicazione</span><span class="sxs-lookup"><span data-stu-id="f686a-308">Event Trace – Capture last *n* system/application events</span></span>
* <span data-ttu-id="f686a-309">Concatenamento di ™: registrare una funzione di callback di notifica specifica dell'applicazione per ogni Azure RTOS di comunicazione ThreadX o di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="f686a-309">Event Chaining™ – Register an application-specific “notify” callback function for each Azure RTOS ThreadX communication or synchronization object</span></span>
* <span data-ttu-id="f686a-310">Azure RTOS ThreadX MODULES con protezione della memoria facoltativa</span><span class="sxs-lookup"><span data-stu-id="f686a-310">Azure RTOS ThreadX MODULES with Optional Memory Protection</span></span>
* <span data-ttu-id="f686a-311">Run-Time delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="f686a-311">Run-Time Performance Metrics</span></span>
  * <span data-ttu-id="f686a-312">Numero di ripresi di thread</span><span class="sxs-lookup"><span data-stu-id="f686a-312">Number of thread resumptions</span></span>
  * <span data-ttu-id="f686a-313">Numero di sospensioni dei thread</span><span class="sxs-lookup"><span data-stu-id="f686a-313">Number of thread suspensions</span></span>
  * <span data-ttu-id="f686a-314">Numero di preemption di thread su cui si è richiesto</span><span class="sxs-lookup"><span data-stu-id="f686a-314">Number of solicited thread preemptions</span></span>
  * <span data-ttu-id="f686a-315">Numero di interruzioni di thread asincrone</span><span class="sxs-lookup"><span data-stu-id="f686a-315">Number of asynchronous thread interrupt preemptions</span></span>
  * <span data-ttu-id="f686a-316">Numero di inversione della priorità dei thread</span><span class="sxs-lookup"><span data-stu-id="f686a-316">Number of thread priority inversions</span></span>
  * <span data-ttu-id="f686a-317">Numero di richieste di thread</span><span class="sxs-lookup"><span data-stu-id="f686a-317">Number of thread relinquishes</span></span>
* <span data-ttu-id="f686a-318">Execution Profile Kit (EPK)</span><span class="sxs-lookup"><span data-stu-id="f686a-318">Execution Profile Kit (EPK)</span></span>
* <span data-ttu-id="f686a-319">Separare lo stack di interrupt</span><span class="sxs-lookup"><span data-stu-id="f686a-319">Separate Interrupt Stack</span></span>
* <span data-ttu-id="f686a-320">Run-Time'analisi dello stack</span><span class="sxs-lookup"><span data-stu-id="f686a-320">Run-Time Stack Analysis</span></span>
* <span data-ttu-id="f686a-321">Elaborazione ottimizzata degli interrupt del timer</span><span class="sxs-lookup"><span data-stu-id="f686a-321">Optimized Timer Interrupt Processing</span></span>

## <a name="multicore-support-amp--smp"></a><span data-ttu-id="f686a-322">Supporto multicore (AMP & SMP)</span><span class="sxs-lookup"><span data-stu-id="f686a-322">Multicore support (AMP & SMP)</span></span>

<span data-ttu-id="f686a-323">ThreadX Azure RTOS standard viene spesso usato in modalità Asimmetrica multiprocessing (AMP), in cui una copia separata di Azure RTOS ThreadX e l'applicazione (o Linux) vengono eseguite in ogni core e comunicano tra loro tramite memoria condivisa o un meccanismo di comunicazione tra processori, ad esempio OpenAMP (Azure RTOS ThreadX supporta OpenAMP).</span><span class="sxs-lookup"><span data-stu-id="f686a-323">Standard Azure RTOS ThreadX is often used in an Asymmetric Multiprocessing (AMP) fashion, where a separate copy of Azure RTOS ThreadX and the application (or Linux) execute on each core and communicate with each other via shared memory or an inter-processor communication mechanism such as OpenAMP (Azure RTOS ThreadX supports OpenAMP).</span></span> <span data-ttu-id="f686a-324">Si tratta della configurazione multicore più tipica che usa Azure RTOS ThreadX e può essere la più efficiente se l'applicazione è in grado di caricare in modo efficace i processori.</span><span class="sxs-lookup"><span data-stu-id="f686a-324">This is the most typical multicore configuration using Azure RTOS ThreadX and can be the most efficient if the application is able to effectively load the processors.</span></span>

<span data-ttu-id="f686a-325">Per gli ambienti in cui il caricamento dei processori è altamente dinamico, Azure RTOS ThreadX Symetric Multiprocessing (SMP) è disponibile per le famiglie di processori seguenti:</span><span class="sxs-lookup"><span data-stu-id="f686a-325">For environments where loading the processors is highly dynamic, Azure RTOS ThreadX Symetric Multiprocessing (SMP) is available for the following processor families:</span></span>

* <span data-ttu-id="f686a-326">Arm Cortex-Ax</span><span class="sxs-lookup"><span data-stu-id="f686a-326">ARM Cortex-Ax</span></span>
* <span data-ttu-id="f686a-327">Arm Cortex-Rx</span><span class="sxs-lookup"><span data-stu-id="f686a-327">ARM Cortex-Rx</span></span>
* <span data-ttu-id="f686a-328">ARM Cortex-A5x a 64 bit</span><span class="sxs-lookup"><span data-stu-id="f686a-328">ARM Cortex-A5x 64-bit</span></span>
* <span data-ttu-id="f686a-329">MIPS 34K, 1004K e interAptiv</span><span class="sxs-lookup"><span data-stu-id="f686a-329">MIPS 34K, 1004K, and interAptiv</span></span>
* <span data-ttu-id="f686a-330">PowerPC</span><span class="sxs-lookup"><span data-stu-id="f686a-330">PowerPC</span></span>
* <span data-ttu-id="f686a-331">Synopsys ARC HS</span><span class="sxs-lookup"><span data-stu-id="f686a-331">Synopsys ARC HS</span></span>
* <span data-ttu-id="f686a-332">x86</span><span class="sxs-lookup"><span data-stu-id="f686a-332">x86</span></span>

<span data-ttu-id="f686a-333">Azure RTOS ThreadX SMP esegue il bilanciamento del carico dinamico tra *n* processori e consente a tutte le risorse threadX di Azure RTOS (code, semafori, flag di eventi, pool di memoria e così via) di essere accessibili da qualsiasi thread in qualsiasi core.</span><span class="sxs-lookup"><span data-stu-id="f686a-333">Azure RTOS ThreadX SMP performs dynamic load balancing across *n* processors and allows all Azure RTOS ThreadX resources (queues, semaphores, event flags, memory pools, etc.) to be accessed by any thread on any core.</span></span> <span data-ttu-id="f686a-334">Azure RTOS ThreadX SMP abilita l'API ThreadX Azure RTOS completa in tutti i core e introduce la nuova API seguente applicabile all'operazione SMP:</span><span class="sxs-lookup"><span data-stu-id="f686a-334">Azure RTOS ThreadX SMP enables the complete Azure RTOS ThreadX API on all cores and introduces the following new API’s applicable to SMP operation:</span></span>

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a><span data-ttu-id="f686a-335">Protezione della memoria tramite Azure RTOS ThreadX</span><span class="sxs-lookup"><span data-stu-id="f686a-335">Memory protection via Azure RTOS ThreadX Modules</span></span>

<span data-ttu-id="f686a-336">Un prodotto aggiuntivo denominato Azure RTOS ThreadX MODULES consente di aggregare uno o più thread dell'applicazione in un "modulo" che può essere caricato ed eseguito dinamicamente (o eseguito sul posto) nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="f686a-336">An add-on product called Azure RTOS ThreadX MODULES enables one or more application threads to be bundled into a “Module” that can be dynamically loaded and run (or executed in place) on the target.</span></span>

<span data-ttu-id="f686a-337">I moduli consentono l'aggiornamento dei campi, la correzione di bug e il partizionamento dei programmi per consentire alle applicazioni di grandi dimensioni di occupare solo la memoria necessaria per i thread attivi.</span><span class="sxs-lookup"><span data-stu-id="f686a-337">Modules enable field upgrade, bug fixing, and program partitioning to allow large applications to occupy only the memory needed by active threads.</span></span>

<span data-ttu-id="f686a-338">I moduli hanno anche uno spazio di indirizzi completamente separato Azure RTOS ThreadX stesso.</span><span class="sxs-lookup"><span data-stu-id="f686a-338">Modules also have a completely separate address space from Azure RTOS ThreadX itself.</span></span> <span data-ttu-id="f686a-339">Ciò consente Azure RTOS ThreadX di posizionare la protezione della memoria (tramite MPU o MMU) intorno al modulo in modo che l'accesso accidentale all'esterno del modulo non sia in grado di danneggiare altri componenti software.</span><span class="sxs-lookup"><span data-stu-id="f686a-339">This enables Azure RTOS ThreadX to place memory protection (via MPU or MMU) around the Module such that accidental access outside the module will not be able to corrupt any other software component.</span></span>


## <a name="misra-compliant"></a><span data-ttu-id="f686a-340">Conforme a MISRA</span><span class="sxs-lookup"><span data-stu-id="f686a-340">MISRA compliant</span></span>

<span data-ttu-id="f686a-341">Azure RTOS threadx e Azure RTOS codice SMP ThreadX è conforme a MISRA-C:2004 e MISRA C:2012.</span><span class="sxs-lookup"><span data-stu-id="f686a-341">Azure RTOS ThreadX and Azure RTOS ThreadX SMP souce code is MISRA-C:2004 and MISRA C:2012 compliant.</span></span> <span data-ttu-id="f686a-342">MISRA C è un set di linee guida per la programmazione per sistemi critici che usano il linguaggio di programmazione C.</span><span class="sxs-lookup"><span data-stu-id="f686a-342">MISRA C is a set of programming guidelines for critical systems using the C programming language.</span></span> <span data-ttu-id="f686a-343">Le linee guida originali di MISRA C erano destinate principalmente alle applicazioni per il settore automobilistico; Tuttavia, MISRA C è ora ampiamente riconosciuto come applicabile a qualsiasi applicazione critica per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f686a-343">The original MISRA C guidelines were primarily targeted toward automotive applications; however, MISRA C is now widely recognized as being applicable to any safety-critical application.</span></span> <span data-ttu-id="f686a-344">Azure RTOS ThreadX è conforme a tutte le regole obbligatorie e obbligatorie di MISRA-C:2004 e MISRA C:2012.</span><span class="sxs-lookup"><span data-stu-id="f686a-344">Azure RTOS ThreadX is compliant with all required and mandatory rules of MISRA-C:2004 and MISRA C:2012.</span></span>

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Certificazione errata":::

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="f686a-346">Supporta le architetture più comuni</span><span class="sxs-lookup"><span data-stu-id="f686a-346">Supports most popular architectures</span></span>

<span data-ttu-id="f686a-347">Azure RTOS ThreadX viene eseguito nei microprocessori a 32/64 bit più diffusi, preimpresciati, completamente testati e completamente supportati, inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="f686a-347">Azure RTOS ThreadX runs on most popular 32/64-bit microprocessors, out-of-the-box, fully tested and fully supported, including the following:</span></span>

* <span data-ttu-id="f686a-348">Dispositivi analoghi: SHARC, Blackfin, CM4xx</span><span class="sxs-lookup"><span data-stu-id="f686a-348">Analog Devices: SHARC, Blackfin, CM4xx</span></span>
* <span data-ttu-id="f686a-349">Andes Core: RISC-V</span><span class="sxs-lookup"><span data-stu-id="f686a-349">Andes Core: RISC-V</span></span>
* <span data-ttu-id="f686a-350">Ambiqmicro: Cpu avi</span><span class="sxs-lookup"><span data-stu-id="f686a-350">Ambiqmicro: Apollo MCUs</span></span>
* <span data-ttu-id="f686a-351">ARM: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x a 64 bit/R4/R5, TrustZone ARMv8-M</span><span class="sxs-lookup"><span data-stu-id="f686a-351">ARM: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>
* <span data-ttu-id="f686a-352">Cadenza: Xtensa, Diamond</span><span class="sxs-lookup"><span data-stu-id="f686a-352">Cadence: Xtensa, Diamond</span></span>
* <span data-ttu-id="f686a-353">CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span><span class="sxs-lookup"><span data-stu-id="f686a-353">CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>
* <span data-ttu-id="f686a-354">Cypress: RISC-V</span><span class="sxs-lookup"><span data-stu-id="f686a-354">Cypress: RISC-V</span></span>
* <span data-ttu-id="f686a-355">EnSilica: eSi-RISC</span><span class="sxs-lookup"><span data-stu-id="f686a-355">EnSilica: eSi-RISC</span></span>
* <span data-ttu-id="f686a-356">Infineon: XMC1000, XMC4000, TriCore</span><span class="sxs-lookup"><span data-stu-id="f686a-356">Infineon: XMC1000, XMC4000, TriCore</span></span>
* <span data-ttu-id="f686a-357">Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Kpine, Arria 10</span><span class="sxs-lookup"><span data-stu-id="f686a-357">Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>
* <span data-ttu-id="f686a-358">Microchip: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="f686a-358">Microchip: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>
* <span data-ttu-id="f686a-359">Microsemi: RISC-V</span><span class="sxs-lookup"><span data-stu-id="f686a-359">Microsemi: RISC-V</span></span>
* <span data-ttu-id="f686a-360">NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="f686a-360">NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>
* <span data-ttu-id="f686a-361">Renesas: SH, HS, V850, RX, RZ, Synergy</span><span class="sxs-lookup"><span data-stu-id="f686a-361">Renesas: SH, HS, V850, RX, RZ, Synergy</span></span>
* <span data-ttu-id="f686a-362">Silicon Labs: EFM32</span><span class="sxs-lookup"><span data-stu-id="f686a-362">Silicon Labs: EFM32</span></span>
* <span data-ttu-id="f686a-363">Synopsys: ARC 600, 700, ARC EM, ARC HS</span><span class="sxs-lookup"><span data-stu-id="f686a-363">Synopsys: ARC 600, 700, ARC EM, ARC HS</span></span>
* <span data-ttu-id="f686a-364">ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="f686a-364">ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>
* <span data-ttu-id="f686a-365">Tl: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span><span class="sxs-lookup"><span data-stu-id="f686a-365">Tl: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>
* <span data-ttu-id="f686a-366">Wave Computing: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span><span class="sxs-lookup"><span data-stu-id="f686a-366">Wave Computing: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>
* <span data-ttu-id="f686a-367">Xilinx: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="f686a-367">Xilinx: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>

## <a name="supports-most-popular-tools"></a><span data-ttu-id="f686a-368">Supporta gli strumenti più diffusi</span><span class="sxs-lookup"><span data-stu-id="f686a-368">Supports most popular tools</span></span>

<span data-ttu-id="f686a-369">Azure RTOS ThreadX supporta la maggior parte degli strumenti di sviluppo incorporati più diffusi, tra cui Embedded Workbench™ di IAR, che offre anche la conoscenza del kernel ThreadX Azure RTOS più completa disponibile.</span><span class="sxs-lookup"><span data-stu-id="f686a-369">Azure RTOS ThreadX supports most popular embedded development tools, including IAR’s Embedded Workbench™, which also has the most comprehensive Azure RTOS ThreadX kernel awareness available.</span></span> <span data-ttu-id="f686a-370">L'integrazione aggiuntiva degli strumenti include GNU (GCC), ARM DS-5/uVision®, Green Hudson MULTI®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauterrbac TRACE32®, TI Code-Composer Studio, CrossCore e tutti i dispositivi analogici.</span><span class="sxs-lookup"><span data-stu-id="f686a-370">Additional tool integration includes GNU (GCC), ARM DS-5/uVision®, Green Hills MULTI®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauterbach TRACE32®, TI Code-Composer Studio, CrossCore and all analog devices.</span></span>
