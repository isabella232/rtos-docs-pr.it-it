---
title: Informazioni Azure RTOS ThreadX
description: Azure ThreadX è un sistema operativo avanzato in tempo reale (RTOS) progettato specificamente per applicazioni con integrazione avanzata.
author: philmea
ms.author: philmea
ms.date: 6/9/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 938619170ef51d354fa970134328c17407ae846a
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754863"
---
# <a name="overview-of-azure-rtos-threadx"></a><span data-ttu-id="7dbda-103">Panoramica di Azure RTOS ThreadX</span><span class="sxs-lookup"><span data-stu-id="7dbda-103">Overview of Azure RTOS ThreadX</span></span>

<span data-ttu-id="7dbda-104">Azure RTOS ThreadX è il sistema operativo RTOS (Advanced Industrial Grade Real-Time Operating System) di Microsoft progettato specificamente per applicazioni IoT, real-time e deep embedded.</span><span class="sxs-lookup"><span data-stu-id="7dbda-104">Azure RTOS ThreadX is Microsoft's advanced industrial grade Real-Time Operating System (RTOS) designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="7dbda-105">Azure RTOS ThreadX offre funzionalità avanzate di pianificazione, comunicazione, sincronizzazione, timer, gestione della memoria e gestione degli interrupt.</span><span class="sxs-lookup"><span data-stu-id="7dbda-105">Azure RTOS ThreadX provides advanced scheduling, communication, synchronization, timer, memory management, and interrupt management facilities.</span></span> <span data-ttu-id="7dbda-106">Inoltre, Azure RTOS ThreadX ha molte funzionalità avanzate, tra cui il picokernel™ l'architettura, la soglia di preemption™ la pianificazione, il concatenamento di eventi, la profilatura dell'esecuzione ™, le metriche delle prestazioni e la traccia degli eventi di sistema.</span><span class="sxs-lookup"><span data-stu-id="7dbda-106">In addition, Azure RTOS ThreadX has many advanced features, including its picokernel™ architecture, preemption-threshold™ scheduling, event-chaining,™ execution profiling, performance metrics, and system event tracing.</span></span> <span data-ttu-id="7dbda-107">Insieme alla semplicità d'uso superiore, Azure RTOS ThreadX è la scelta ideale per le applicazioni incorporate più complesse.</span><span class="sxs-lookup"><span data-stu-id="7dbda-107">Combined with its superior ease-of-use, Azure RTOS ThreadX is the ideal choice for the most demanding of embedded applications.</span></span> <span data-ttu-id="7dbda-108">Dal 2017, Azure RTOS ThreadX ha oltre 6,2 miliardi di distribuzioni, in un'ampia gamma di prodotti, tra cui dispositivi consumer, elettronica medicale e apparecchiature di controllo industriale.</span><span class="sxs-lookup"><span data-stu-id="7dbda-108">As of 2017, Azure RTOS ThreadX has over 6.2 billion deployments, in a wide variety of products, including consumer devices, medical electronics, and industrial control equipment.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="7dbda-109">Protocolli API</span><span class="sxs-lookup"><span data-stu-id="7dbda-109">API Protocols</span></span>

### <a name="azure-rtos-threadx-services"></a><span data-ttu-id="7dbda-110">Azure RTOS ThreadX Services</span><span class="sxs-lookup"><span data-stu-id="7dbda-110">Azure RTOS ThreadX Services</span></span>

* <span data-ttu-id="7dbda-111">Creazione dinamica di thread</span><span class="sxs-lookup"><span data-stu-id="7dbda-111">Dynamic thread creation</span></span>
* <span data-ttu-id="7dbda-112">Nessun limite al numero di thread</span><span class="sxs-lookup"><span data-stu-id="7dbda-112">No limits on the number of threads</span></span>
* <span data-ttu-id="7dbda-113">Le API del thread principale includono:</span><span class="sxs-lookup"><span data-stu-id="7dbda-113">Main thread APIs include:</span></span>
  * <span data-ttu-id="7dbda-114">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="7dbda-114">tx_thread_create</span></span>
  * <span data-ttu-id="7dbda-115">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="7dbda-115">tx_thread_delete</span></span>
  * <span data-ttu-id="7dbda-116">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="7dbda-116">tx_thread_preemption_change</span></span>
  * <span data-ttu-id="7dbda-117">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="7dbda-117">tx_thread_priority_change</span></span>
  * <span data-ttu-id="7dbda-118">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="7dbda-118">tx_thread_relinquish</span></span>
  * <span data-ttu-id="7dbda-119">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="7dbda-119">tx_thread_reset</span></span>
  * <span data-ttu-id="7dbda-120">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="7dbda-120">tx_thread_resume</span></span>
  * <span data-ttu-id="7dbda-121">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="7dbda-121">tx_thread_sleep</span></span>
  * <span data-ttu-id="7dbda-122">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="7dbda-122">tx_thread_suspend</span></span>
  * <span data-ttu-id="7dbda-123">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="7dbda-123">tx_thread_terminate</span></span>
  * <span data-ttu-id="7dbda-124">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="7dbda-124">tx_thread_wait_abort</span></span>
* <span data-ttu-id="7dbda-125">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-125">Additional information and performance APIs</span></span>

### <a name="message-queues"></a><span data-ttu-id="7dbda-126">Code di messaggi</span><span class="sxs-lookup"><span data-stu-id="7dbda-126">Message Queues</span></span>

* <span data-ttu-id="7dbda-127">Creazione dinamica della coda</span><span class="sxs-lookup"><span data-stu-id="7dbda-127">Dynamic queue creation</span></span>
* <span data-ttu-id="7dbda-128">Nessun limite al numero di code</span><span class="sxs-lookup"><span data-stu-id="7dbda-128">No limits on the number of queues</span></span>
* <span data-ttu-id="7dbda-129">Messaggi copiati per valore (o per riferimento tramite puntatore)</span><span class="sxs-lookup"><span data-stu-id="7dbda-129">Messages copied by value (or by reference via pointer)</span></span>
* <span data-ttu-id="7dbda-130">Dimensioni dei messaggi da 1 a 16 parole a 32 bit</span><span class="sxs-lookup"><span data-stu-id="7dbda-130">Message sizes from 1 to 16 32-bit words</span></span>
* <span data-ttu-id="7dbda-131">Sospensione del thread facoltativa su vuoto e pieno</span><span class="sxs-lookup"><span data-stu-id="7dbda-131">Optional thread suspension on empty and full</span></span>
* <span data-ttu-id="7dbda-132">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-132">Optional timeout on all suspension</span></span>
* <span data-ttu-id="7dbda-133">Le API principali della coda di messaggi includono:</span><span class="sxs-lookup"><span data-stu-id="7dbda-133">Main message queue APIs include:</span></span>
  * <span data-ttu-id="7dbda-134">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="7dbda-134">tx_queue_create</span></span>
  * <span data-ttu-id="7dbda-135">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="7dbda-135">tx_queue_delete</span></span>
  * <span data-ttu-id="7dbda-136">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="7dbda-136">tx_queue_flush</span></span>
  * <span data-ttu-id="7dbda-137">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="7dbda-137">tx_queue_front_send</span></span>
  * <span data-ttu-id="7dbda-138">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="7dbda-138">tx_queue_receive</span></span>
  * <span data-ttu-id="7dbda-139">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="7dbda-139">tx_queue_send_notify</span></span>
* <span data-ttu-id="7dbda-140">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-140">Additional information and performance APIs</span></span>

### <a name="counting-semaphores"></a><span data-ttu-id="7dbda-141">Conteggio dei semafori</span><span class="sxs-lookup"><span data-stu-id="7dbda-141">Counting Semaphores</span></span>

* <span data-ttu-id="7dbda-142">Creazione dinamica del semaforo</span><span class="sxs-lookup"><span data-stu-id="7dbda-142">Dynamic semaphore creation</span></span>
* <span data-ttu-id="7dbda-143">Nessun limite al numero di semafori</span><span class="sxs-lookup"><span data-stu-id="7dbda-143">No limits on the number of semaphores</span></span>
* <span data-ttu-id="7dbda-144">Semafori di conteggio a 32 bit (da 0 a 4.294.967.295)</span><span class="sxs-lookup"><span data-stu-id="7dbda-144">32-bit counting semaphores (0 to 4,294,967,295)</span></span>
* <span data-ttu-id="7dbda-145">Supporta la protezione dei consumer-producer o delle risorse</span><span class="sxs-lookup"><span data-stu-id="7dbda-145">Supports consumer-producer or resource protection</span></span>
* <span data-ttu-id="7dbda-146">Sospensione del thread facoltativa quando il semaforo non è disponibile</span><span class="sxs-lookup"><span data-stu-id="7dbda-146">Optional thread suspension when semaphore unavailable</span></span>
* <span data-ttu-id="7dbda-147">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-147">Optional timeout on all suspension</span></span>
* <span data-ttu-id="7dbda-148">Le PRINCIPALI API del semaforo includono:</span><span class="sxs-lookup"><span data-stu-id="7dbda-148">Main semaphore APIs include:</span></span>
  * <span data-ttu-id="7dbda-149">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="7dbda-149">tx_semaphore_create</span></span>
  * <span data-ttu-id="7dbda-150">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="7dbda-150">tx_semaphore_delete</span></span>
  * <span data-ttu-id="7dbda-151">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="7dbda-151">tx_semaphore_get</span></span>
  * <span data-ttu-id="7dbda-152">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="7dbda-152">tx_semaphore_put</span></span>
  * <span data-ttu-id="7dbda-153">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="7dbda-153">tx_semaphore_put_notify</span></span>
* <span data-ttu-id="7dbda-154">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-154">Additional information and performance APIs</span></span>

### <a name="mutexes"></a><span data-ttu-id="7dbda-155">Mutex</span><span class="sxs-lookup"><span data-stu-id="7dbda-155">Mutexes</span></span>

* <span data-ttu-id="7dbda-156">Creazione dinamica di mutex</span><span class="sxs-lookup"><span data-stu-id="7dbda-156">Dynamic mutex creation</span></span>
* <span data-ttu-id="7dbda-157">Nessun limite al numero di mutex</span><span class="sxs-lookup"><span data-stu-id="7dbda-157">No limits on the number of mutexes</span></span>
* <span data-ttu-id="7dbda-158">Protezione delle risorse annidate supportata</span><span class="sxs-lookup"><span data-stu-id="7dbda-158">Nested resource protection supported</span></span>
* <span data-ttu-id="7dbda-159">Ereditarietà della priorità facoltativa supportata</span><span class="sxs-lookup"><span data-stu-id="7dbda-159">Optional priority inheritance supported</span></span>
* <span data-ttu-id="7dbda-160">Sospensione del thread facoltativa quando mutex non disponibile</span><span class="sxs-lookup"><span data-stu-id="7dbda-160">Optional thread suspension when mutex unavailable</span></span>
* <span data-ttu-id="7dbda-161">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-161">Optional timeout on all suspension</span></span>
* <span data-ttu-id="7dbda-162">Le PRINCIPALI API mutex includono:</span><span class="sxs-lookup"><span data-stu-id="7dbda-162">Main mutex APIs include:</span></span>
  * <span data-ttu-id="7dbda-163">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="7dbda-163">tx_mutex_create</span></span>
  * <span data-ttu-id="7dbda-164">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="7dbda-164">tx_mutex_delete</span></span>
  * <span data-ttu-id="7dbda-165">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="7dbda-165">tx_mutex_get</span></span>
  * <span data-ttu-id="7dbda-166">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="7dbda-166">tx_mutex_put</span></span>
* <span data-ttu-id="7dbda-167">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-167">Additional information and performance APIs</span></span>

### <a name="event-flags"></a><span data-ttu-id="7dbda-168">Flag di evento</span><span class="sxs-lookup"><span data-stu-id="7dbda-168">Event Flags</span></span>

* <span data-ttu-id="7dbda-169">Creazione dinamica del gruppo di flag di eventi</span><span class="sxs-lookup"><span data-stu-id="7dbda-169">Dynamic event flag group creation</span></span>
* <span data-ttu-id="7dbda-170">Nessun limite al numero di gruppi di flag di eventi</span><span class="sxs-lookup"><span data-stu-id="7dbda-170">No limits on the number of event flag groups</span></span>
* <span data-ttu-id="7dbda-171">Sincronizzazione di uno o più thread</span><span class="sxs-lookup"><span data-stu-id="7dbda-171">Synchronization of one thread or multiple threads</span></span>
* <span data-ttu-id="7dbda-172">Supporto di atomic get e clear</span><span class="sxs-lookup"><span data-stu-id="7dbda-172">Atomic get and clear supported</span></span>
* <span data-ttu-id="7dbda-173">Sospensione multithread facoltativa su un set di eventi AND/OR</span><span class="sxs-lookup"><span data-stu-id="7dbda-173">Optional multithread suspension on AND/OR set of events</span></span>
* <span data-ttu-id="7dbda-174">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-174">Optional timeout on all suspension</span></span>
* <span data-ttu-id="7dbda-175">Le API del flag di evento principale includono:</span><span class="sxs-lookup"><span data-stu-id="7dbda-175">Main event flag APIs include:</span></span>
  * <span data-ttu-id="7dbda-176">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="7dbda-176">tx_event_flags_create</span></span>
  * <span data-ttu-id="7dbda-177">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="7dbda-177">tx_event_flags_delete</span></span>
  * <span data-ttu-id="7dbda-178">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="7dbda-178">tx_event_flags_get</span></span>
  * <span data-ttu-id="7dbda-179">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="7dbda-179">tx_event_flags_set</span></span>
  * <span data-ttu-id="7dbda-180">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="7dbda-180">tx_event_flags_set_notify</span></span>
* <span data-ttu-id="7dbda-181">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-181">Additional information and performance APIs</span></span>

### <a name="block-memory-pools"></a><span data-ttu-id="7dbda-182">Bloccare i pool di memoria</span><span class="sxs-lookup"><span data-stu-id="7dbda-182">Block Memory Pools</span></span>

* <span data-ttu-id="7dbda-183">Creazione dinamica del pool a blocchi</span><span class="sxs-lookup"><span data-stu-id="7dbda-183">Dynamic block pool creation</span></span>
* <span data-ttu-id="7dbda-184">Nessun limite al numero di pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="7dbda-184">No limits on the number of block pools</span></span>
* <span data-ttu-id="7dbda-185">Nessun limite alle dimensioni dei blocchi di dimensioni fisse o delle dimensioni del pool</span><span class="sxs-lookup"><span data-stu-id="7dbda-185">No limits on size of fixed-size blocks or size of pool</span></span>
* <span data-ttu-id="7dbda-186">Più veloce possibile allocazione di memoria/deal-location</span><span class="sxs-lookup"><span data-stu-id="7dbda-186">Fastest possible memory allocation/deal-location</span></span>
* <span data-ttu-id="7dbda-187">Sospensione facoltativa dei thread in un pool vuoto</span><span class="sxs-lookup"><span data-stu-id="7dbda-187">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="7dbda-188">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-188">Optional timeout on all suspension</span></span>
* <span data-ttu-id="7dbda-189">Le API principali del pool di blocchi includono:</span><span class="sxs-lookup"><span data-stu-id="7dbda-189">Main block pool APIs include:</span></span>
  * <span data-ttu-id="7dbda-190">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="7dbda-190">tx_block_pool_create</span></span>
  * <span data-ttu-id="7dbda-191">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="7dbda-191">tx_block_pool_delete</span></span>
  * <span data-ttu-id="7dbda-192">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="7dbda-192">tx_block_allocate</span></span>
  * <span data-ttu-id="7dbda-193">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="7dbda-193">tx_block_release</span></span>
* <span data-ttu-id="7dbda-194">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-194">Additional information and performance APIs</span></span>

### <a name="byte-memory-pools"></a><span data-ttu-id="7dbda-195">Pool di memoria di byte</span><span class="sxs-lookup"><span data-stu-id="7dbda-195">Byte Memory Pools</span></span>

* <span data-ttu-id="7dbda-196">Creazione dinamica del pool di byte</span><span class="sxs-lookup"><span data-stu-id="7dbda-196">Dynamic byte pool creation</span></span>
* <span data-ttu-id="7dbda-197">Nessun limite al numero di pool di byte</span><span class="sxs-lookup"><span data-stu-id="7dbda-197">No limits on the number of byte pools</span></span>
* <span data-ttu-id="7dbda-198">Nessun limite alle dimensioni del pool di byte</span><span class="sxs-lookup"><span data-stu-id="7dbda-198">No limits on size of byte pool</span></span>
* <span data-ttu-id="7dbda-199">Allocazione/deallocazione di memoria a lunghezza variabile più flessibile</span><span class="sxs-lookup"><span data-stu-id="7dbda-199">Most flexible variable-length memory allocation/deallocation</span></span>
* <span data-ttu-id="7dbda-200">Località delle dimensioni di allocazione supportata</span><span class="sxs-lookup"><span data-stu-id="7dbda-200">Allocation size locality supported</span></span>
* <span data-ttu-id="7dbda-201">Sospensione del thread facoltativa in un pool vuoto</span><span class="sxs-lookup"><span data-stu-id="7dbda-201">Optional thread suspension on empty pool</span></span>
* <span data-ttu-id="7dbda-202">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-202">Optional timeout on all suspension</span></span>
* <span data-ttu-id="7dbda-203">Le API principali del pool di byte includono:</span><span class="sxs-lookup"><span data-stu-id="7dbda-203">Main byte pool APIs include:</span></span>
  * <span data-ttu-id="7dbda-204">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="7dbda-204">tx_byte_pool_create</span></span>
  * <span data-ttu-id="7dbda-205">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="7dbda-205">tx_byte_pool_delete</span></span>
  * <span data-ttu-id="7dbda-206">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="7dbda-206">tx_byte_allocate</span></span>
  * <span data-ttu-id="7dbda-207">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="7dbda-207">tx_byte_release</span></span>
* <span data-ttu-id="7dbda-208">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-208">Additional information and performance APIs</span></span>

### <a name="application-timers"></a><span data-ttu-id="7dbda-209">Timer dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="7dbda-209">Application Timers</span></span>

* <span data-ttu-id="7dbda-210">Creazione dinamica del timer</span><span class="sxs-lookup"><span data-stu-id="7dbda-210">Dynamic timer creation</span></span>
* <span data-ttu-id="7dbda-211">Nessun limite al numero di timer</span><span class="sxs-lookup"><span data-stu-id="7dbda-211">No limits on the number of timers</span></span>
* <span data-ttu-id="7dbda-212">Timer periodici o one-shot supportati</span><span class="sxs-lookup"><span data-stu-id="7dbda-212">Periodic or one-shot timers supported</span></span>
* <span data-ttu-id="7dbda-213">I timer periodici possono avere un valore di scadenza iniziale diverso</span><span class="sxs-lookup"><span data-stu-id="7dbda-213">Periodic timers may have different initial expiration value</span></span>
* <span data-ttu-id="7dbda-214">Nessuna ricerca nell'attivazione o disattivazione del timer</span><span class="sxs-lookup"><span data-stu-id="7dbda-214">No searching on timer activation or deactivation</span></span>
* <span data-ttu-id="7dbda-215">Tutti i timer guidati da un interrupt timer hardware</span><span class="sxs-lookup"><span data-stu-id="7dbda-215">All timers driven from one hardware timer interrupt</span></span>
* <span data-ttu-id="7dbda-216">Le API principali del timer includono:</span><span class="sxs-lookup"><span data-stu-id="7dbda-216">Main timer APIs include:</span></span>
  * <span data-ttu-id="7dbda-217">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="7dbda-217">tx_timer_create</span></span>
  * <span data-ttu-id="7dbda-218">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="7dbda-218">tx_timer_delete</span></span>
  * <span data-ttu-id="7dbda-219">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="7dbda-219">tx_timer_activate</span></span>
  * <span data-ttu-id="7dbda-220">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="7dbda-220">tx_timer_change</span></span>
  * <span data-ttu-id="7dbda-221">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="7dbda-221">tx_timer_deactivate</span></span>
* <span data-ttu-id="7dbda-222">Informazioni aggiuntive e API per le prestazioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-222">Additional information and performance APIs</span></span>

### <a name="azure-rtos-threadx-core-scheduler"></a><span data-ttu-id="7dbda-223">Azure RTOS ThreadX Core Scheduler</span><span class="sxs-lookup"><span data-stu-id="7dbda-223">Azure RTOS ThreadX Core Scheduler</span></span>

* <span data-ttu-id="7dbda-224">Memoria FLASH minima da 2 KB, footprint di RAM di 1 KB</span><span class="sxs-lookup"><span data-stu-id="7dbda-224">Minimal 2KB FLASH,1KB RAM footprint</span></span>
* <span data-ttu-id="7dbda-225">Cambio di contesto rapido e sottosecondo</span><span class="sxs-lookup"><span data-stu-id="7dbda-225">Fast, sub-microsecond context-switch</span></span>
* <span data-ttu-id="7dbda-226">Completamente deterministico indipendentemente dal numero di thread</span><span class="sxs-lookup"><span data-stu-id="7dbda-226">Fully deterministic regardless of number of threads</span></span>
* <span data-ttu-id="7dbda-227">Pianificazione preemptive basata sulla priorità</span><span class="sxs-lookup"><span data-stu-id="7dbda-227">Priority-based, fully preemptive-scheduling</span></span>
* <span data-ttu-id="7dbda-228">32 livelli di priorità predefiniti, facoltativamente fino a 1024 livelli</span><span class="sxs-lookup"><span data-stu-id="7dbda-228">32 default priority levels, optionally up to 1024 levels</span></span>
* <span data-ttu-id="7dbda-229">Pianificazione cooperativa all'interno del livello di priorità (FIFO)</span><span class="sxs-lookup"><span data-stu-id="7dbda-229">Cooperative scheduling within priority level (FIFO)</span></span>
* <span data-ttu-id="7dbda-230">Tecnologia di soglia di preemption</span><span class="sxs-lookup"><span data-stu-id="7dbda-230">Preemption-threshold technology</span></span>
* <span data-ttu-id="7dbda-231">Servizi timer facoltativi, tra cui:</span><span class="sxs-lookup"><span data-stu-id="7dbda-231">Optional timer services, including:</span></span>
  * <span data-ttu-id="7dbda-232">Intervallo di tempo facoltativo per thread</span><span class="sxs-lookup"><span data-stu-id="7dbda-232">Per-thread optional time-slice</span></span>
  * <span data-ttu-id="7dbda-233">Timeout facoltativo per tutti i blocchi</span><span class="sxs-lookup"><span data-stu-id="7dbda-233">Optional timeout on all blocking</span></span>
  * <span data-ttu-id="7dbda-234">API richieste per interrupt timer hardware</span><span class="sxs-lookup"><span data-stu-id="7dbda-234">APIs Requires on hardware timer interrupt</span></span>
* <span data-ttu-id="7dbda-235">Profilatura dell'esecuzione</span><span class="sxs-lookup"><span data-stu-id="7dbda-235">Execution profiling</span></span>
* <span data-ttu-id="7dbda-236">Traccia a livello di sistema</span><span class="sxs-lookup"><span data-stu-id="7dbda-236">System-level Trace</span></span>
* <span data-ttu-id="7dbda-237">Sicurezza certificata per molti standard</span><span class="sxs-lookup"><span data-stu-id="7dbda-237">Safety certified to many standards</span></span>

## <a name="threadx-footprint"></a><span data-ttu-id="7dbda-238">Footprint ThreadX</span><span class="sxs-lookup"><span data-stu-id="7dbda-238">ThreadX footprint</span></span>

<span data-ttu-id="7dbda-239">Azure RTOS ThreadX richiede un'area di istruzioni di 2 KB notevolmente ridotta e 1 KB di RAM per il footprint minimo.</span><span class="sxs-lookup"><span data-stu-id="7dbda-239">Azure RTOS ThreadX requires a remarkably small 2KB instruction area and 1KB of RAM for its minimal footprint.</span></span> <span data-ttu-id="7dbda-240">Ciò è dovuto in gran parte all'architettura a ™ a più livelli e alla scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="7dbda-240">This is largely due to its non-layered picokernel™ architecture and automatic scaling.</span></span> <span data-ttu-id="7dbda-241">Il ridimensionamento automatico significa che solo i servizi (e l'infrastruttura di supporto) usati dall'applicazione vengono inclusi nell'immagine finale in fase di collegamento.</span><span class="sxs-lookup"><span data-stu-id="7dbda-241">Automatic scaling means that only the services (and supporting infrastructure) used by the application are included in the final image at link time.</span></span>

<span data-ttu-id="7dbda-242">Ecco alcune caratteristiche tipiche delle Azure RTOS ThreadX.</span><span class="sxs-lookup"><span data-stu-id="7dbda-242">Here are some typical Azure RTOS ThreadX size characteristics.</span></span>

|<span data-ttu-id="7dbda-243">Azure RTOS ThreadX Service</span><span class="sxs-lookup"><span data-stu-id="7dbda-243">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="7dbda-244">Dimensioni tipiche in byte</span><span class="sxs-lookup"><span data-stu-id="7dbda-244">Typical Size in Bytes</span></span>  |
|---------|---------|
|<span data-ttu-id="7dbda-245">Servizi di base (richiesta)</span><span class="sxs-lookup"><span data-stu-id="7dbda-245">Core Services (Require)</span></span> |<span data-ttu-id="7dbda-246">2.000</span><span class="sxs-lookup"><span data-stu-id="7dbda-246">2,000</span></span>  |
|<span data-ttu-id="7dbda-247">Servizi di accodamento</span><span class="sxs-lookup"><span data-stu-id="7dbda-247">Queue Services</span></span>  |<span data-ttu-id="7dbda-248">900</span><span class="sxs-lookup"><span data-stu-id="7dbda-248">900</span></span>  |
|<span data-ttu-id="7dbda-249">Servizi flag di evento</span><span class="sxs-lookup"><span data-stu-id="7dbda-249">Event Flag Services</span></span>  |<span data-ttu-id="7dbda-250">900</span><span class="sxs-lookup"><span data-stu-id="7dbda-250">900</span></span>  |
|<span data-ttu-id="7dbda-251">Servizi semafori</span><span class="sxs-lookup"><span data-stu-id="7dbda-251">Semaphore Services</span></span>  |<span data-ttu-id="7dbda-252">450</span><span class="sxs-lookup"><span data-stu-id="7dbda-252">450</span></span>  |
|<span data-ttu-id="7dbda-253">Servizi mutex</span><span class="sxs-lookup"><span data-stu-id="7dbda-253">Mutex Services</span></span>  |<span data-ttu-id="7dbda-254">1.200</span><span class="sxs-lookup"><span data-stu-id="7dbda-254">1,200</span></span>  |
|<span data-ttu-id="7dbda-255">Servizi di memoria a blocchi</span><span class="sxs-lookup"><span data-stu-id="7dbda-255">Block Memory Services</span></span>  |<span data-ttu-id="7dbda-256">550</span><span class="sxs-lookup"><span data-stu-id="7dbda-256">550</span></span>  |
|<span data-ttu-id="7dbda-257">Servizi byte memory</span><span class="sxs-lookup"><span data-stu-id="7dbda-257">Byte Memory Services</span></span>  |<span data-ttu-id="7dbda-258">900</span><span class="sxs-lookup"><span data-stu-id="7dbda-258">900</span></span>  |

## <a name="threadx-execution-speed"></a><span data-ttu-id="7dbda-259">Velocità di esecuzione di ThreadX</span><span class="sxs-lookup"><span data-stu-id="7dbda-259">ThreadX execution speed</span></span>

<span data-ttu-id="7dbda-260">Azure RTOS ThreadX ottiene un cambio di contesto di sottosecondo nei processori più diffusi ed è notevolmente più veloce rispetto ad altri RTOS commerciali.</span><span class="sxs-lookup"><span data-stu-id="7dbda-260">Azure RTOS ThreadX achieves a sub-microsecond context switch on most popular processors and is significantly faster overall than other commercial RTOSes.</span></span> <span data-ttu-id="7dbda-261">Oltre a essere veloce, Azure RTOS ThreadX è altamente deterministico.</span><span class="sxs-lookup"><span data-stu-id="7dbda-261">In addition to being fast, Azure RTOS ThreadX is also highly deterministic.</span></span> <span data-ttu-id="7dbda-262">Consente di ottenere le stesse prestazioni veloci, sia che siano disponibili 200 thread o solo uno.</span><span class="sxs-lookup"><span data-stu-id="7dbda-262">It achieves the same fast performance whether there are 200 threads ready, or just one.</span></span>

<span data-ttu-id="7dbda-263">Ecco alcune caratteristiche tipiche delle prestazioni di Azure RTOS ThreadX:</span><span class="sxs-lookup"><span data-stu-id="7dbda-263">Here are some typical performance characteristics of Azure RTOS ThreadX:</span></span>

* <span data-ttu-id="7dbda-264">Avvio rapido: Azure RTOS ThreadX viene avviato in meno di 120 cicli.</span><span class="sxs-lookup"><span data-stu-id="7dbda-264">Fast Boot: Azure RTOS ThreadX boots in less than 120 cycles.</span></span>
* <span data-ttu-id="7dbda-265">Rimozione facoltativa del controllo degli errori di base: il controllo degli Azure RTOS threadx di base può essere ignorato in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="7dbda-265">Optional Removal of basic error checking: Basic Azure RTOS ThreadX error checking can be skipped at compile time.</span></span> <span data-ttu-id="7dbda-266">Ciò può essere utile quando il codice dell'applicazione viene verificato e non richiede più il controllo degli errori per ogni parametro.</span><span class="sxs-lookup"><span data-stu-id="7dbda-266">This can be useful when the application code is verified and no longer requires error checking on each parameter.</span></span> <span data-ttu-id="7dbda-267">Si noti che questa operazione può essere eseguita in un'unità di compilazione, anziché a livello di sistema.</span><span class="sxs-lookup"><span data-stu-id="7dbda-267">Note that this can be done on a compilation unit, rather than system-wide.</span></span>
* <span data-ttu-id="7dbda-268">Picokernel™ progettazione: i servizi non sono a livelli l'uno sull'altro, eliminando il sovraccarico delle chiamate di funzione non necessarie.</span><span class="sxs-lookup"><span data-stu-id="7dbda-268">Picokernel™ Design: Services are not layered on each other, thus eliminating unnecessary function call overhead.</span></span>
* <span data-ttu-id="7dbda-269">\*Elaborazione interrupt ottimizzata: al momento dell'ingresso/uscita dell'ISR vengono salvati/ripristinati solo i registri scratch, a meno che non sia necessaria la precedenza.</span><span class="sxs-lookup"><span data-stu-id="7dbda-269">\*Optimized Interrupt Processing: Only scratch registers are saved/restored upon ISR entry/exit, unless preemption is necessary.</span></span>
* <span data-ttu-id="7dbda-270">Elaborazione API ottimizzata:</span><span class="sxs-lookup"><span data-stu-id="7dbda-270">Optimized API Processing:</span></span>

    |<span data-ttu-id="7dbda-271">Azure RTOS ThreadX Service</span><span class="sxs-lookup"><span data-stu-id="7dbda-271">Azure RTOS ThreadX Service</span></span>  |<span data-ttu-id="7dbda-272">Tempo del servizio in microsecondi\*</span><span class="sxs-lookup"><span data-stu-id="7dbda-272">Service Time in Microseconds\*</span></span>  |
    |---------|---------|
    |<span data-ttu-id="7dbda-273">Thread Suspend</span><span class="sxs-lookup"><span data-stu-id="7dbda-273">Thread Suspend</span></span>  |<span data-ttu-id="7dbda-274">0,6</span><span class="sxs-lookup"><span data-stu-id="7dbda-274">0.6</span></span>  |
    |<span data-ttu-id="7dbda-275">Thread Resume</span><span class="sxs-lookup"><span data-stu-id="7dbda-275">Thread Resume</span></span>  |<span data-ttu-id="7dbda-276">0,6</span><span class="sxs-lookup"><span data-stu-id="7dbda-276">0.6</span></span>  |
    |<span data-ttu-id="7dbda-277">Invio in coda</span><span class="sxs-lookup"><span data-stu-id="7dbda-277">Queue Send</span></span>  |<span data-ttu-id="7dbda-278">0,3</span><span class="sxs-lookup"><span data-stu-id="7dbda-278">0.3</span></span>  |
    |<span data-ttu-id="7dbda-279">Ricezione coda</span><span class="sxs-lookup"><span data-stu-id="7dbda-279">Queue Receive</span></span>  |<span data-ttu-id="7dbda-280">0,3</span><span class="sxs-lookup"><span data-stu-id="7dbda-280">0.3</span></span>  |
    |<span data-ttu-id="7dbda-281">Ottenere un semaforo</span><span class="sxs-lookup"><span data-stu-id="7dbda-281">Get Semaphore</span></span>  |<span data-ttu-id="7dbda-282">0,2</span><span class="sxs-lookup"><span data-stu-id="7dbda-282">0.2</span></span>  |
    |<span data-ttu-id="7dbda-283">Put Semaphore</span><span class="sxs-lookup"><span data-stu-id="7dbda-283">Put Semaphore</span></span>  |<span data-ttu-id="7dbda-284">0,2</span><span class="sxs-lookup"><span data-stu-id="7dbda-284">0.2</span></span>  |
    |<span data-ttu-id="7dbda-285">Cambio di contesto</span><span class="sxs-lookup"><span data-stu-id="7dbda-285">Context Switch</span></span>  |<span data-ttu-id="7dbda-286">0,4</span><span class="sxs-lookup"><span data-stu-id="7dbda-286">0.4</span></span>  |
    |<span data-ttu-id="7dbda-287">Risposta di interrupt</span><span class="sxs-lookup"><span data-stu-id="7dbda-287">Interrupt Response</span></span>  |<span data-ttu-id="7dbda-288">0.0 – 0.6</span><span class="sxs-lookup"><span data-stu-id="7dbda-288">0.0 – 0.6</span></span>  |

    <span data-ttu-id="7dbda-289">\**Dati sulle prestazioni basati sul processore tipico in esecuzione a 200 MHz.*</span><span class="sxs-lookup"><span data-stu-id="7dbda-289">\**Performance figures based on typical processor running at 200MHz*.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="7dbda-290">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="7dbda-290">Advanced technology</span></span>

<span data-ttu-id="7dbda-291">Azure RTOS ThreadX è una tecnologia avanzata la cui funzionalità più importante è la pianificazione della soglia di preemption.</span><span class="sxs-lookup"><span data-stu-id="7dbda-291">Azure RTOS ThreadX is advanced technology whose most notable feature is preemption-threshold scheduling.</span></span> <span data-ttu-id="7dbda-292">Questa funzionalità è univoca per Azure RTOS ThreadX ed è stata oggetto di ricerche accademiche approfondite.</span><span class="sxs-lookup"><span data-stu-id="7dbda-292">This feature is unique to Azure RTOS ThreadX and has been the subject of extensive academic research.</span></span> <span data-ttu-id="7dbda-293">Ad esempio, vedere [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf)(Pianificazione di attività di Fixed-Priority con soglia di preemption), di Yun Wang, Concordia University e Manas Sakslde, University of University of Bayh.</span><span class="sxs-lookup"><span data-stu-id="7dbda-293">For example, see [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf), by Yun Wang, Concordia University, and Manas Saksena, University of Pittsburgh.</span></span>

<span data-ttu-id="7dbda-294">Considerare le funzionalità di Azure RTOS ThreadX.</span><span class="sxs-lookup"><span data-stu-id="7dbda-294">Consider the capabilities of Azure RTOS ThreadX.</span></span>

* <span data-ttu-id="7dbda-295">Funzionalità complete e complete per il multitasking</span><span class="sxs-lookup"><span data-stu-id="7dbda-295">Complete and Comprehensive Multitasking Facilities</span></span>
  * <span data-ttu-id="7dbda-296">Thread, timer dell'applicazione, code di messaggi, semafori di conteggio, mutex, flag di eventi, pool di memoria di blocchi e byte</span><span class="sxs-lookup"><span data-stu-id="7dbda-296">Threads, application timers, message queues, counting semaphores, mutexes, event flags, block and byte memory pools</span></span>
* <span data-ttu-id="7dbda-297">Priority-Based preemptive</span><span class="sxs-lookup"><span data-stu-id="7dbda-297">Priority-Based Preemptive Scheduling</span></span>
* <span data-ttu-id="7dbda-298">Flessibilità di priorità: fino a 1024 livelli di priorità</span><span class="sxs-lookup"><span data-stu-id="7dbda-298">Priority Flexibility – Up to 1024 Priority Levels</span></span>
* <span data-ttu-id="7dbda-299">Pianificazione cooperativa</span><span class="sxs-lookup"><span data-stu-id="7dbda-299">Cooperative Scheduling</span></span>
* <span data-ttu-id="7dbda-300">Preemption-Threshold™: univoco per Azure RTOS ThreadX, consente di ridurre i commutatori di contesto e di garantire la pianificazione (in base alla ricerca accademica)</span><span class="sxs-lookup"><span data-stu-id="7dbda-300">Preemption-Threshold™ – Unique to Azure RTOS ThreadX, helps reduce context switches and help guarantee schedulability (per academic research)</span></span>
* <span data-ttu-id="7dbda-301">Protezione della memoria tramite Azure RTOS ThreadX MODULES</span><span class="sxs-lookup"><span data-stu-id="7dbda-301">Memory Protection via Azure RTOS ThreadX MODULES</span></span>
* <span data-ttu-id="7dbda-302">Completamente deterministico</span><span class="sxs-lookup"><span data-stu-id="7dbda-302">Fully Deterministic</span></span>
* <span data-ttu-id="7dbda-303">Traccia eventi: acquisisci gli ultimi *n eventi* di sistema/applicazione</span><span class="sxs-lookup"><span data-stu-id="7dbda-303">Event Trace – Capture last *n* system/application events</span></span>
* <span data-ttu-id="7dbda-304">Event Chaining™: registrare una funzione di callback "notify" specifica dell'applicazione per ogni Azure RTOS di comunicazione o sincronizzazione ThreadX</span><span class="sxs-lookup"><span data-stu-id="7dbda-304">Event Chaining™ – Register an application-specific “notify” callback function for each Azure RTOS ThreadX communication or synchronization object</span></span>
* <span data-ttu-id="7dbda-305">Azure RTOS moduli ThreadX con protezione della memoria facoltativa</span><span class="sxs-lookup"><span data-stu-id="7dbda-305">Azure RTOS ThreadX MODULES with Optional Memory Protection</span></span>
* <span data-ttu-id="7dbda-306">Run-Time metriche delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7dbda-306">Run-Time Performance Metrics</span></span>
  * <span data-ttu-id="7dbda-307">Numero di rievazioni di thread</span><span class="sxs-lookup"><span data-stu-id="7dbda-307">Number of thread resumptions</span></span>
  * <span data-ttu-id="7dbda-308">Numero di sospensioni dei thread</span><span class="sxs-lookup"><span data-stu-id="7dbda-308">Number of thread suspensions</span></span>
  * <span data-ttu-id="7dbda-309">Numero di preemption di thread richieste</span><span class="sxs-lookup"><span data-stu-id="7dbda-309">Number of solicited thread preemptions</span></span>
  * <span data-ttu-id="7dbda-310">Numero di interruzioni asincrone del thread</span><span class="sxs-lookup"><span data-stu-id="7dbda-310">Number of asynchronous thread interrupt preemptions</span></span>
  * <span data-ttu-id="7dbda-311">Numero di inversioni di priorità dei thread</span><span class="sxs-lookup"><span data-stu-id="7dbda-311">Number of thread priority inversions</span></span>
  * <span data-ttu-id="7dbda-312">Numero di richieste di thread</span><span class="sxs-lookup"><span data-stu-id="7dbda-312">Number of thread relinquishes</span></span>
* <span data-ttu-id="7dbda-313">Kit del profilo di esecuzione (EPK)</span><span class="sxs-lookup"><span data-stu-id="7dbda-313">Execution Profile Kit (EPK)</span></span>
* <span data-ttu-id="7dbda-314">Separare lo stack di interrupt</span><span class="sxs-lookup"><span data-stu-id="7dbda-314">Separate Interrupt Stack</span></span>
* <span data-ttu-id="7dbda-315">Run-Time'analisi dello stack</span><span class="sxs-lookup"><span data-stu-id="7dbda-315">Run-Time Stack Analysis</span></span>
* <span data-ttu-id="7dbda-316">Ottimizzazione dell'elaborazione degli interrupt del timer</span><span class="sxs-lookup"><span data-stu-id="7dbda-316">Optimized Timer Interrupt Processing</span></span>

## <a name="multicore-support-amp--smp"></a><span data-ttu-id="7dbda-317">Supporto multicore (AMP & SMP)</span><span class="sxs-lookup"><span data-stu-id="7dbda-317">Multicore support (AMP & SMP)</span></span>

<span data-ttu-id="7dbda-318">ThreadX Azure RTOS standard viene spesso usato in modalità Asimmetrica multiprocessing (AMP), in cui una copia separata di Azure RTOS ThreadX e l'applicazione (o Linux) vengono eseguite in ogni core e comunicano tra loro tramite memoria condivisa o un meccanismo di comunicazione tra processori, ad esempio OpenAMP (Azure RTOS ThreadX supporta OpenAMP).</span><span class="sxs-lookup"><span data-stu-id="7dbda-318">Standard Azure RTOS ThreadX is often used in an Asymmetric Multiprocessing (AMP) fashion, where a separate copy of Azure RTOS ThreadX and the application (or Linux) execute on each core and communicate with each other via shared memory or an inter-processor communication mechanism such as OpenAMP (Azure RTOS ThreadX supports OpenAMP).</span></span> <span data-ttu-id="7dbda-319">Si tratta della configurazione multicore più tipica che usa Azure RTOS ThreadX e può essere la più efficiente se l'applicazione è in grado di caricare in modo efficace i processori.</span><span class="sxs-lookup"><span data-stu-id="7dbda-319">This is the most typical multicore configuration using Azure RTOS ThreadX and can be the most efficient if the application is able to effectively load the processors.</span></span>

<span data-ttu-id="7dbda-320">Per gli ambienti in cui il caricamento dei processori è altamente dinamico, Azure RTOS ThreadX Symetric Multiprocessing (SMP) è disponibile per le famiglie di processori seguenti:</span><span class="sxs-lookup"><span data-stu-id="7dbda-320">For environments where loading the processors is highly dynamic, Azure RTOS ThreadX Symetric Multiprocessing (SMP) is available for the following processor families:</span></span>

* <span data-ttu-id="7dbda-321">Arm Cortex-Ax</span><span class="sxs-lookup"><span data-stu-id="7dbda-321">ARM Cortex-Ax</span></span>
* <span data-ttu-id="7dbda-322">Arm Cortex-Rx</span><span class="sxs-lookup"><span data-stu-id="7dbda-322">ARM Cortex-Rx</span></span>
* <span data-ttu-id="7dbda-323">ARM Cortex-A5x a 64 bit</span><span class="sxs-lookup"><span data-stu-id="7dbda-323">ARM Cortex-A5x 64-bit</span></span>
* <span data-ttu-id="7dbda-324">MIPS 34K, 1004K e interAptiv</span><span class="sxs-lookup"><span data-stu-id="7dbda-324">MIPS 34K, 1004K, and interAptiv</span></span>
* <span data-ttu-id="7dbda-325">PowerPC</span><span class="sxs-lookup"><span data-stu-id="7dbda-325">PowerPC</span></span>
* <span data-ttu-id="7dbda-326">Synopsys ARC HS</span><span class="sxs-lookup"><span data-stu-id="7dbda-326">Synopsys ARC HS</span></span>
* <span data-ttu-id="7dbda-327">x86</span><span class="sxs-lookup"><span data-stu-id="7dbda-327">x86</span></span>

<span data-ttu-id="7dbda-328">Azure RTOS ThreadX SMP esegue il bilanciamento del carico dinamico tra *n* processori e consente a tutte le risorse threadX di Azure RTOS (code, semafori, flag di eventi, pool di memoria e così via) di essere accessibili da qualsiasi thread in qualsiasi core.</span><span class="sxs-lookup"><span data-stu-id="7dbda-328">Azure RTOS ThreadX SMP performs dynamic load balancing across *n* processors and allows all Azure RTOS ThreadX resources (queues, semaphores, event flags, memory pools, etc.) to be accessed by any thread on any core.</span></span> <span data-ttu-id="7dbda-329">Azure RTOS ThreadX SMP abilita l'API ThreadX Azure RTOS completa in tutti i core e introduce la nuova API seguente applicabile all'operazione SMP:</span><span class="sxs-lookup"><span data-stu-id="7dbda-329">Azure RTOS ThreadX SMP enables the complete Azure RTOS ThreadX API on all cores and introduces the following new API’s applicable to SMP operation:</span></span>

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a><span data-ttu-id="7dbda-330">Protezione della memoria tramite Azure RTOS ThreadX</span><span class="sxs-lookup"><span data-stu-id="7dbda-330">Memory protection via Azure RTOS ThreadX Modules</span></span>

<span data-ttu-id="7dbda-331">Un prodotto aggiuntivo denominato Azure RTOS ThreadX MODULES consente di aggregare uno o più thread dell'applicazione in un "modulo" che può essere caricato ed eseguito dinamicamente (o eseguito sul posto) nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="7dbda-331">An add-on product called Azure RTOS ThreadX MODULES enables one or more application threads to be bundled into a “Module” that can be dynamically loaded and run (or executed in place) on the target.</span></span>

<span data-ttu-id="7dbda-332">I moduli consentono l'aggiornamento dei campi, la correzione di bug e il partizionamento dei programmi per consentire alle applicazioni di grandi dimensioni di occupare solo la memoria necessaria per i thread attivi.</span><span class="sxs-lookup"><span data-stu-id="7dbda-332">Modules enable field upgrade, bug fixing, and program partitioning to allow large applications to occupy only the memory needed by active threads.</span></span>

<span data-ttu-id="7dbda-333">I moduli hanno anche uno spazio di indirizzi completamente separato Azure RTOS ThreadX stesso.</span><span class="sxs-lookup"><span data-stu-id="7dbda-333">Modules also have a completely separate address space from Azure RTOS ThreadX itself.</span></span> <span data-ttu-id="7dbda-334">Ciò consente Azure RTOS ThreadX di posizionare la protezione della memoria (tramite MPU o MMU) intorno al modulo in modo che l'accesso accidentale all'esterno del modulo non sia in grado di danneggiare qualsiasi altro componente software.</span><span class="sxs-lookup"><span data-stu-id="7dbda-334">This enables Azure RTOS ThreadX to place memory protection (via MPU or MMU) around the Module such that accidental access outside the module will not be able to corrupt any other software component.</span></span>

## <a name="misra-compliant"></a><span data-ttu-id="7dbda-335">Conforme a MISRA</span><span class="sxs-lookup"><span data-stu-id="7dbda-335">MISRA compliant</span></span>

<span data-ttu-id="7dbda-336">Azure RTOS codice sorgente ThreadX e Azure RTOS ThreadX SMP è conforme a MISRA-C:2004 e MISRA C:2012.</span><span class="sxs-lookup"><span data-stu-id="7dbda-336">Azure RTOS ThreadX and Azure RTOS ThreadX SMP source code is MISRA-C:2004 and MISRA C:2012 compliant.</span></span> <span data-ttu-id="7dbda-337">MISRA C è un set di linee guida di programmazione per i sistemi critici che usano il linguaggio di programmazione C.</span><span class="sxs-lookup"><span data-stu-id="7dbda-337">MISRA C is a set of programming guidelines for critical systems using the C programming language.</span></span> <span data-ttu-id="7dbda-338">Le linee guida originali di MISRA C erano destinate principalmente alle applicazioni automobilistiche; Tuttavia, MISRA C è ora ampiamente riconosciuto come applicabile a qualsiasi applicazione critica per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="7dbda-338">The original MISRA C guidelines were primarily targeted toward automotive applications; however, MISRA C is now widely recognized as being applicable to any safety-critical application.</span></span> <span data-ttu-id="7dbda-339">Azure RTOS ThreadX è conforme a tutte le regole obbligatorie e obbligatorie di MISRA-C:2004 e MISRA C:2012.</span><span class="sxs-lookup"><span data-stu-id="7dbda-339">Azure RTOS ThreadX is compliant with all required and mandatory rules of MISRA-C:2004 and MISRA C:2012.</span></span>

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Certificazione misra":::

## <a name="supports-most-popular-tools"></a><span data-ttu-id="7dbda-341">Supporta gli strumenti più diffusi</span><span class="sxs-lookup"><span data-stu-id="7dbda-341">Supports most popular tools</span></span>

<span data-ttu-id="7dbda-342">Azure RTOS ThreadX supporta la maggior parte degli strumenti di sviluppo incorporati più diffusi, tra cui Embedded Workbench™ di IAR, che offre anche la conoscenza del kernel ThreadX Azure RTOS più completa disponibile.</span><span class="sxs-lookup"><span data-stu-id="7dbda-342">Azure RTOS ThreadX supports most popular embedded development tools, including IAR’s Embedded Workbench™, which also has the most comprehensive Azure RTOS ThreadX kernel awareness available.</span></span> <span data-ttu-id="7dbda-343">L'integrazione aggiuntiva degli strumenti include GNU (GCC), ARM DS-5/uVision®, Green Hudson MULTI®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauterrbac TRACE32®, TI Code-Composer Studio, CrossCore e tutti i dispositivi analoghi.</span><span class="sxs-lookup"><span data-stu-id="7dbda-343">Additional tool integration includes GNU (GCC), ARM DS-5/uVision®, Green Hills MULTI®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauterbach TRACE32®, TI Code-Composer Studio, CrossCore and all analog devices.</span></span>

## <a name="adaptation-layer-for-threadx"></a><span data-ttu-id="7dbda-344">Livello di adattamento per ThreadX</span><span class="sxs-lookup"><span data-stu-id="7dbda-344">Adaptation layer for ThreadX</span></span>

<span data-ttu-id="7dbda-345">Azure RTOS ThreadX è un sistema operativo in tempo reale (RTOS, Real-Time Operating System) avanzato, progettato in modo specifico per applicazioni profondamente incorporate.</span><span class="sxs-lookup"><span data-stu-id="7dbda-345">Azure RTOS ThreadX is an advanced real-time operating system (RTOS) designed specifically for deeply embedded applications.</span></span> <span data-ttu-id="7dbda-346">Per facilitare la migrazione delle applicazioni a Auzre RTOS, ThreadX fornisce livelli di adattamento per varie API RTOS legacy (FreeRTOS, POSIX, OSEK e così via) [](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers)</span><span class="sxs-lookup"><span data-stu-id="7dbda-346">To help ease application migration to Auzre RTOS, ThreadX provides [adaption layers](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers) for various legacy RTOS APIs (FreeRTOS, POSIX, OSEK, etc.)</span></span>
