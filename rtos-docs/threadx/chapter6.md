---
title: Capitolo 6-sistema dimostrativo per Azure RTO ThreadX
description: Questo capitolo contiene una descrizione del sistema di dimostrazione fornito con tutti i pacchetti di supporto del processore ThreadX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: be85ba77e5c27366f61899c0939be7cad1845bbe
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821356"
---
# <a name="chapter-6---demonstration-system-for-azure-rtos-threadx"></a><span data-ttu-id="2de7e-103">Capitolo 6-sistema dimostrativo per Azure RTO ThreadX</span><span class="sxs-lookup"><span data-stu-id="2de7e-103">Chapter 6 - Demonstration System for Azure RTOS ThreadX</span></span>

<span data-ttu-id="2de7e-104">Questo capitolo contiene una descrizione del sistema di dimostrazione fornito con tutti i pacchetti di supporto del processore ThreadX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="2de7e-104">This chapter contains a description of the demonstration system that is delivered with all Azure RTOS ThreadX processor support packages.</span></span>

## <a name="overview"></a><span data-ttu-id="2de7e-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2de7e-105">Overview</span></span>

<span data-ttu-id="2de7e-106">Ogni distribuzione del prodotto ThreadX contiene un sistema dimostrativo che viene eseguito su tutti i microprocessori supportati.</span><span class="sxs-lookup"><span data-stu-id="2de7e-106">Each ThreadX product distribution contains a demonstration system that runs on all supported microprocessors.</span></span>

<span data-ttu-id="2de7e-107">Questo sistema di esempio è definito nel file di distribuzione ***demo_threadx. c*** ed è progettato per illustrare il modo in cui threadX viene usato in un ambiente multithread incorporato.</span><span class="sxs-lookup"><span data-stu-id="2de7e-107">This example system is defined in the distribution file ***demo_threadx.c*** and is designed to illustrate how ThreadX is used in an embedded multithread environment.</span></span> <span data-ttu-id="2de7e-108">La dimostrazione è costituita dall'inizializzazione, da otto thread, da un pool di byte, da un pool di blocchi, da una coda, da un semaforo, da un mutex e da un gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="2de7e-108">The demonstration consists of initialization, eight threads, one byte pool, one block pool, one queue, one semaphore, one mutex, and one event flags group.</span></span>

> [!NOTE]
> <span data-ttu-id="2de7e-109">*Ad eccezione delle dimensioni dello stack del thread, l'applicazione dimostrativa è identica in tutti i processori supportati da ThreadX.*</span><span class="sxs-lookup"><span data-stu-id="2de7e-109">*Except for the thread's stack size, the demonstration application is identical on all ThreadX supported processors.*</span></span>

<span data-ttu-id="2de7e-110">Elenco completo di ***demo_threadx. c***, inclusi i numeri di riga a cui si fa riferimento nel resto di questo capitolo.</span><span class="sxs-lookup"><span data-stu-id="2de7e-110">The complete listing of ***demo_threadx.c***, including the line numbers referenced throughout the remainder of this chapter.</span></span>

## <a name="application-define"></a><span data-ttu-id="2de7e-111">Definizione applicazione</span><span class="sxs-lookup"><span data-stu-id="2de7e-111">Application Define</span></span>

<span data-ttu-id="2de7e-112">La funzione ***tx_application_define*** viene eseguita dopo il completamento dell'inizializzazione di base di threadX.</span><span class="sxs-lookup"><span data-stu-id="2de7e-112">The ***tx_application_define*** function executes after the basic ThreadX initialization is complete.</span></span> <span data-ttu-id="2de7e-113">È responsabile della configurazione di tutte le risorse di sistema iniziali, inclusi thread, code, semafori, mutex, flag di evento e pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="2de7e-113">It is responsible for setting up all of the initial system resources, including threads, queues, semaphores, mutexes, event flags, and memory pools.</span></span>

<span data-ttu-id="2de7e-114">La \***tx_application_define** _ (_line numbers 60-164 \*) del sistema di dimostrazione crea gli oggetti dimostrativi nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="2de7e-114">The demonstration system's ***tx_application_define** _ (_line numbers 60-164*) creates the demonstration objects in the following order:</span></span>

- <span data-ttu-id="2de7e-115">byte_pool_0</span><span class="sxs-lookup"><span data-stu-id="2de7e-115">byte_pool_0</span></span>
- <span data-ttu-id="2de7e-116">thread_0</span><span class="sxs-lookup"><span data-stu-id="2de7e-116">thread_0</span></span>
- <span data-ttu-id="2de7e-117">thread_1</span><span class="sxs-lookup"><span data-stu-id="2de7e-117">thread_1</span></span>
- <span data-ttu-id="2de7e-118">thread_2</span><span class="sxs-lookup"><span data-stu-id="2de7e-118">thread_2</span></span>
- <span data-ttu-id="2de7e-119">thread_3</span><span class="sxs-lookup"><span data-stu-id="2de7e-119">thread_3</span></span>
- <span data-ttu-id="2de7e-120">thread_4</span><span class="sxs-lookup"><span data-stu-id="2de7e-120">thread_4</span></span>
- <span data-ttu-id="2de7e-121">thread_5</span><span class="sxs-lookup"><span data-stu-id="2de7e-121">thread_5</span></span>
- <span data-ttu-id="2de7e-122">thread_6</span><span class="sxs-lookup"><span data-stu-id="2de7e-122">thread_6</span></span>
- <span data-ttu-id="2de7e-123">thread_7</span><span class="sxs-lookup"><span data-stu-id="2de7e-123">thread_7</span></span>
- <span data-ttu-id="2de7e-124">queue_0</span><span class="sxs-lookup"><span data-stu-id="2de7e-124">queue_0</span></span>
- <span data-ttu-id="2de7e-125">semaphore_0</span><span class="sxs-lookup"><span data-stu-id="2de7e-125">semaphore_0</span></span>
- <span data-ttu-id="2de7e-126">event_flags_0</span><span class="sxs-lookup"><span data-stu-id="2de7e-126">event_flags_0</span></span>
- <span data-ttu-id="2de7e-127">mutex_0</span><span class="sxs-lookup"><span data-stu-id="2de7e-127">mutex_0</span></span>
- <span data-ttu-id="2de7e-128">block_pool_0</span><span class="sxs-lookup"><span data-stu-id="2de7e-128">block_pool_0</span></span>

<span data-ttu-id="2de7e-129">Il sistema dimostrativo non crea altri oggetti ThreadX aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="2de7e-129">The demonstration system does not create any other additional ThreadX objects.</span></span> <span data-ttu-id="2de7e-130">Tuttavia, un'applicazione effettiva può creare oggetti di sistema durante il runtime all'interno dei thread in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2de7e-130">However, an actual application may create system objects during runtime inside of executing threads.</span></span>

### <a name="initial-execution"></a><span data-ttu-id="2de7e-131">Esecuzione iniziale</span><span class="sxs-lookup"><span data-stu-id="2de7e-131">Initial Execution</span></span>

<span data-ttu-id="2de7e-132">Tutti i thread vengono creati con l'opzione **TX_AUTO_START** .</span><span class="sxs-lookup"><span data-stu-id="2de7e-132">All threads are created with the **TX_AUTO_START** option.</span></span> <span data-ttu-id="2de7e-133">Che li rende inizialmente pronti per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2de7e-133">This makes them initially ready for execution.</span></span> <span data-ttu-id="2de7e-134">Al termine dell' ***tx_application_define*** , il controllo viene trasferito all'utilità di pianificazione dei thread e da tale posizione a ogni singolo thread.</span><span class="sxs-lookup"><span data-stu-id="2de7e-134">After ***tx_application_define*** completes, control is transferred to the thread scheduler and from there to each individual thread.</span></span>

<span data-ttu-id="2de7e-135">L'ordine in cui vengono eseguiti i thread è determinato dalla loro priorità e dall'ordine in cui sono stati creati.</span><span class="sxs-lookup"><span data-stu-id="2de7e-135">The order in which the threads execute is determined by their priority and the order that they were created.</span></span> <span data-ttu-id="2de7e-136">Nel sistema di dimostrazione, ***Thread_0*** viene eseguito per primo perché ha la priorità più alta, ovvero è *stata creata con una priorità pari a 1*.</span><span class="sxs-lookup"><span data-stu-id="2de7e-136">In the demonstration system, ***thread_0*** executes first because it has the highest priority (*it was created with a priority of 1*).</span></span> <span data-ttu-id="2de7e-137">Dopo la sospensione ***Thread_0*** , viene eseguito ***Thread_5*** , seguito dall'esecuzione di ***Thread_3** _, _*_Thread_4_*_, _*_Thread_6_*_, _* _Thread_7_\* \*, \***Thread_1**_ e infine _ *_Thread_2_* \*.</span><span class="sxs-lookup"><span data-stu-id="2de7e-137">After ***thread_0*** suspends, ***thread_5*** is executed, followed by the execution of ***thread_3** _, _*_thread_4_*_, _*_thread_6_*_, _*_thread_7_\*\*, \***thread_1**_, and finally _\*_thread_2_\*\*.</span></span>

> [!NOTE]
> <span data-ttu-id="2de7e-138">*Anche se **Thread_3** e **Thread_4** hanno la stessa priorità (entrambi creati con una priorità pari a 8), **Thread_3** viene eseguita per prima. Questo perché **Thread_3** è stato creato e pronto prima di **Thread_4**. I thread con uguale priorità vengono eseguiti in modalità FIFO.*</span><span class="sxs-lookup"><span data-stu-id="2de7e-138">*Even though **thread_3** and **thread_4** have the same priority (both created with a priority of 8), **thread_3** executes first. This is because **thread_3** was created and became ready before **thread_4**. Threads of equal priority execute in a FIFO fashion.*</span></span>

## <a name="thread-0"></a><span data-ttu-id="2de7e-139">Thread 0</span><span class="sxs-lookup"><span data-stu-id="2de7e-139">Thread 0</span></span>

<span data-ttu-id="2de7e-140">La funzione ***thread_0_entry*** contrassegna il punto di ingresso del thread *(righe 167-190*).</span><span class="sxs-lookup"><span data-stu-id="2de7e-140">The function ***thread_0_entry*** marks the entry point of the thread *(lines 167-190*).</span></span> <span data-ttu-id="2de7e-141">***Thread_0*** è il primo thread del sistema dimostrativo da eseguire.</span><span class="sxs-lookup"><span data-stu-id="2de7e-141">***Thread_0*** is the first thread in the demonstration system to execute.</span></span> <span data-ttu-id="2de7e-142">L'elaborazione è semplice: incrementa il contatore, dorme per 10 cicli del timer, imposta un flag di evento per riattivare ***Thread_5***, quindi ripete la sequenza.</span><span class="sxs-lookup"><span data-stu-id="2de7e-142">Its processing is simple: it increments its counter, sleeps for 10 timer ticks, sets an event flag to wake up ***thread_5***, then repeats the sequence.</span></span>

<span data-ttu-id="2de7e-143">***Thread_0*** è il thread con priorità più elevata nel sistema.</span><span class="sxs-lookup"><span data-stu-id="2de7e-143">***Thread_0*** is the highest priority thread in the system.</span></span> <span data-ttu-id="2de7e-144">Quando la sospensione richiesta scade, viene interrotta qualsiasi altro thread in esecuzione nella dimostrazione.</span><span class="sxs-lookup"><span data-stu-id="2de7e-144">When its requested sleep expires, it will preempt any other executing thread in the demonstration.</span></span>

## <a name="thread-1"></a><span data-ttu-id="2de7e-145">Thread 1</span><span class="sxs-lookup"><span data-stu-id="2de7e-145">Thread 1</span></span>

<span data-ttu-id="2de7e-146">La funzione \***thread_1_entry** _ contrassegna il punto di ingresso del thread _(righe 193-216 *). ***Thread_1*** è il penultimo thread del sistema dimostrativo da eseguire. L'elaborazione è costituita dall'incremento del contatore, dall'invio di un messaggio a ***Thread_2*** (* tramite \* ***queue_0***) e dalla ripetizione della sequenza. Si noti che \***Thread_1**_ viene sospeso ogni volta che _*_queue_0_*_ diventa pieno (_line 207 \*).</span><span class="sxs-lookup"><span data-stu-id="2de7e-146">The function ***thread_1_entry** _ marks the entry point of the thread _(lines 193-216 *). ***Thread_1*** is the second-to-last thread in the demonstration system to execute. Its processing consists of incrementing its counter, sending a message to ***thread_2*** (* through* ***queue_0***), and repeating the sequence. Notice that \***thread_1**_ suspends whenever _*_queue_0_*_ becomes full (_line 207\*).</span></span>

## <a name="thread-2"></a><span data-ttu-id="2de7e-147">Thread 2</span><span class="sxs-lookup"><span data-stu-id="2de7e-147">Thread 2</span></span>

<span data-ttu-id="2de7e-148">La funzione ***thread_2_entry*** contrassegna il punto di ingresso del thread *(righe 219-243*).</span><span class="sxs-lookup"><span data-stu-id="2de7e-148">The function ***thread_2_entry*** marks the entry point of the thread *(lines 219-243*).</span></span> <span data-ttu-id="2de7e-149">***Thread_2*** è l'ultimo thread del sistema dimostrativo da eseguire.</span><span class="sxs-lookup"><span data-stu-id="2de7e-149">***Thread_2*** is the last thread in the demonstration system to execute.</span></span> <span data-ttu-id="2de7e-150">L'elaborazione prevede l'incremento del contatore, il recupero di un messaggio da ***Thread_1*** (tramite ***queue_0***) e la ripetizione della sequenza.</span><span class="sxs-lookup"><span data-stu-id="2de7e-150">Its processing consists of incrementing its counter, getting a message from ***thread_1*** (through ***queue_0***), and repeating the sequence.</span></span> <span data-ttu-id="2de7e-151">Si noti che ***Thread_2** _ sospende ogni volta che _*_queue_0_\*_ diventa vuoto (_line 233 \*).</span><span class="sxs-lookup"><span data-stu-id="2de7e-151">Notice that ***thread_2** _ suspends whenever _*_queue_0_*_ becomes empty (_line 233*).</span></span>

<span data-ttu-id="2de7e-152">Anche se ***Thread_1** _ e _ *_Thread_2_** condividono la priorità più bassa nel sistema dimostrativo (\* priorità 16 \*), i *thread 3 e 4*</span><span class="sxs-lookup"><span data-stu-id="2de7e-152">Although ***thread_1** _ and _ *_thread_2_** share the lowest priority in the demonstration system (\* priority 16\*), they *Threads 3 and 4*</span></span>

<span data-ttu-id="2de7e-153">sono anche gli unici thread pronti per l'esecuzione nella maggior parte dei casi.</span><span class="sxs-lookup"><span data-stu-id="2de7e-153">are also the only threads that are ready for execution most of the time.</span></span> <span data-ttu-id="2de7e-154">Sono anche gli unici thread creati con il sezionamento del tempo (*righe 87 e 93*).</span><span class="sxs-lookup"><span data-stu-id="2de7e-154">They are also the only threads created with time-slicing (*lines 87 and 93*).</span></span> <span data-ttu-id="2de7e-155">Ogni thread può essere eseguito per un massimo di 4 cicli di timer prima dell'esecuzione dell'altro thread.</span><span class="sxs-lookup"><span data-stu-id="2de7e-155">Each thread is allowed to execute for a maximum of 4 timer ticks before the other thread is executed.</span></span>

## <a name="threads-3-and-4"></a><span data-ttu-id="2de7e-156">Thread 3 e 4</span><span class="sxs-lookup"><span data-stu-id="2de7e-156">Threads 3 and 4</span></span>

<span data-ttu-id="2de7e-157">La funzione ***thread_3_and_4_entry*** contrassegna il punto di ingresso di ***Thread_3** _ e _ *_Thread_4_** (righe 246-280).</span><span class="sxs-lookup"><span data-stu-id="2de7e-157">The function ***thread_3_and_4_entry*** marks the entry point of both ***thread_3** _ and _ *_thread_4_** (lines 246-280).</span></span> <span data-ttu-id="2de7e-158">Entrambi i thread hanno una priorità di 8, che li rende il terzo e il quarto thread del sistema dimostrativo da eseguire.</span><span class="sxs-lookup"><span data-stu-id="2de7e-158">Both threads have a priority of 8, which makes them the third and fourth threads in the demonstration system to execute.</span></span> <span data-ttu-id="2de7e-159">L'elaborazione di ogni thread è la stessa: incrementando il contatore, ottenendo ***semaphore_0***, dormendo due cicli del timer, rilasciando ***semaphore_0*** e ripetendo la sequenza.</span><span class="sxs-lookup"><span data-stu-id="2de7e-159">The processing for each thread is the same: incrementing its counter, getting ***semaphore_0***, sleeping for 2 timer ticks, releasing ***semaphore_0***, and repeating the sequence.</span></span> <span data-ttu-id="2de7e-160">Si noti che ogni thread viene sospeso ogni volta che ***semaphore_0*** non è disponibile (riga 264).</span><span class="sxs-lookup"><span data-stu-id="2de7e-160">Notice that each thread suspends whenever ***semaphore_0*** is unavailable (line 264).</span></span>

<span data-ttu-id="2de7e-161">Inoltre, entrambi i thread utilizzano la stessa funzione per l'elaborazione principale.</span><span class="sxs-lookup"><span data-stu-id="2de7e-161">Also both threads use the same function for their main processing.</span></span>
<span data-ttu-id="2de7e-162">Questo non presenta alcun problema perché entrambi hanno uno stack univoco e C è naturalmente rientrante.</span><span class="sxs-lookup"><span data-stu-id="2de7e-162">This presents no problems because they both have their own unique stack, and C is naturally reentrant.</span></span> <span data-ttu-id="2de7e-163">Ogni thread determina quale sia l'esame del parametro di input del thread (riga 258), che viene configurato quando vengono create (righe 102 e 109).</span><span class="sxs-lookup"><span data-stu-id="2de7e-163">Each thread determines which one it is by examination of the thread input parameter (line 258), which is setup when they are created (lines 102 and 109).</span></span>

> [!NOTE]
> <span data-ttu-id="2de7e-164">*È anche ragionevole ottenere il punto di thread corrente durante l'esecuzione del thread e confrontarlo con l'indirizzo del blocco di controllo per determinare l'identità del thread.*</span><span class="sxs-lookup"><span data-stu-id="2de7e-164">*It is also reasonable to obtain the current thread point during thread execution and compare it with the control block's address to determine thread identity.*</span></span>

## <a name="thread-5"></a><span data-ttu-id="2de7e-165">Thread 5</span><span class="sxs-lookup"><span data-stu-id="2de7e-165">Thread 5</span></span>

<span data-ttu-id="2de7e-166">La funzione ***thread_5_entry*** contrassegna il punto di ingresso del thread (righe 283-305).</span><span class="sxs-lookup"><span data-stu-id="2de7e-166">The function ***thread_5_entry*** marks the entry point of the thread (lines 283-305).</span></span> <span data-ttu-id="2de7e-167">***Thread_5*** è il secondo thread del sistema di dimostrazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="2de7e-167">***Thread_5*** is the second thread in the demonstration system to execute.</span></span> <span data-ttu-id="2de7e-168">L'elaborazione prevede l'incremento del contatore, il recupero di un flag di evento da ***Thread_0*** (tramite ***event_flags_0***) e la ripetizione della sequenza.</span><span class="sxs-lookup"><span data-stu-id="2de7e-168">Its processing consists of incrementing its counter, getting an event flag from ***thread_0*** (through ***event_flags_0***), and repeating the sequence.</span></span> <span data-ttu-id="2de7e-169">Si noti che ***Thread_5*** viene sospesa ogni volta che il flag di evento ***event_flags_0*** non è disponibile (riga 298).</span><span class="sxs-lookup"><span data-stu-id="2de7e-169">Notice that ***thread_5*** suspends whenever the event flag in ***event_flags_0*** is not available (line 298).</span></span>

## <a name="threads-6-and-7"></a><span data-ttu-id="2de7e-170">Thread 6 e 7</span><span class="sxs-lookup"><span data-stu-id="2de7e-170">Threads 6 and 7</span></span>

<span data-ttu-id="2de7e-171">La funzione ***thread_6_and_7_entry*** contrassegna il punto di ingresso di ***Thread_6** _ e _ *_Thread_7_** (righe 307-358).</span><span class="sxs-lookup"><span data-stu-id="2de7e-171">The function ***thread_6_and_7_entry*** marks the entry point of both ***thread_6** _ and _ *_thread_7_** (lines 307-358).</span></span> <span data-ttu-id="2de7e-172">Entrambi i thread hanno una priorità di 8, che li rende il quinto e il sesto thread del sistema dimostrativo da eseguire.</span><span class="sxs-lookup"><span data-stu-id="2de7e-172">Both threads have a priority of 8, which makes them the fifth and sixth threads in the demonstration system to execute.</span></span> <span data-ttu-id="2de7e-173">L'elaborazione di ogni thread è la stessa: incrementando il contatore, ottenendo ***mutex_0*** due volte, dormendo per due cicli timer, rilasciando ***mutex_0*** due volte e ripetendo la sequenza.</span><span class="sxs-lookup"><span data-stu-id="2de7e-173">The processing for each thread is the same: incrementing its counter, getting ***mutex_0*** twice, sleeping for 2 timer ticks, releasing ***mutex_0*** twice, and repeating the sequence.</span></span> <span data-ttu-id="2de7e-174">Si noti che ogni thread viene sospeso ogni volta che ***mutex_0*** non è disponibile (riga 325).</span><span class="sxs-lookup"><span data-stu-id="2de7e-174">Notice that each thread suspends whenever ***mutex_0*** is unavailable (line 325).</span></span>

<span data-ttu-id="2de7e-175">Inoltre, entrambi i thread utilizzano la stessa funzione per l'elaborazione principale.</span><span class="sxs-lookup"><span data-stu-id="2de7e-175">Also both threads use the same function for their main processing.</span></span> <span data-ttu-id="2de7e-176">Questo non presenta alcun problema perché entrambi hanno uno stack univoco e C è naturalmente rientrante.</span><span class="sxs-lookup"><span data-stu-id="2de7e-176">This presents no problems because they both have their own unique stack, and C is naturally reentrant.</span></span>
<span data-ttu-id="2de7e-177">Ogni thread determina quale sia l'esame del parametro di input del thread (riga 319), che viene configurato quando vengono create (righe 126 e 133).</span><span class="sxs-lookup"><span data-stu-id="2de7e-177">Each thread determines which one it is by examination of the thread input parameter (line 319), which is setup when they are created (lines 126 and 133).</span></span>

## <a name="observing-the-demonstration"></a><span data-ttu-id="2de7e-178">Osservazione della dimostrazione</span><span class="sxs-lookup"><span data-stu-id="2de7e-178">Observing the Demonstration</span></span>

<span data-ttu-id="2de7e-179">Ognuno dei thread dimostrativi incrementa il proprio contatore univoco.</span><span class="sxs-lookup"><span data-stu-id="2de7e-179">Each of the demonstration threads increments its own unique counter.</span></span>
<span data-ttu-id="2de7e-180">È possibile esaminare i contatori seguenti per verificare l'operazione della demo:</span><span class="sxs-lookup"><span data-stu-id="2de7e-180">The following counters may be examined to check on the demo's operation:</span></span>

- <span data-ttu-id="2de7e-181">thread_0_counter</span><span class="sxs-lookup"><span data-stu-id="2de7e-181">thread_0_counter</span></span>
- <span data-ttu-id="2de7e-182">thread_1_counter</span><span class="sxs-lookup"><span data-stu-id="2de7e-182">thread_1_counter</span></span>
- <span data-ttu-id="2de7e-183">thread_2_counter</span><span class="sxs-lookup"><span data-stu-id="2de7e-183">thread_2_counter</span></span>
- <span data-ttu-id="2de7e-184">thread_3_counter</span><span class="sxs-lookup"><span data-stu-id="2de7e-184">thread_3_counter</span></span>
- <span data-ttu-id="2de7e-185">thread_4_counter</span><span class="sxs-lookup"><span data-stu-id="2de7e-185">thread_4_counter</span></span>
- <span data-ttu-id="2de7e-186">thread_5_counter</span><span class="sxs-lookup"><span data-stu-id="2de7e-186">thread_5_counter</span></span>
- <span data-ttu-id="2de7e-187">thread_6_counter</span><span class="sxs-lookup"><span data-stu-id="2de7e-187">thread_6_counter</span></span>
- <span data-ttu-id="2de7e-188">thread_7_counter</span><span class="sxs-lookup"><span data-stu-id="2de7e-188">thread_7_counter</span></span>

<span data-ttu-id="2de7e-189">Ognuno di questi contatori dovrebbe continuare ad aumentare quando viene eseguita la dimostrazione, con ***thread_1_counter** _ e _ *_thread_2_counter_** aumentando alla velocità più elevata.</span><span class="sxs-lookup"><span data-stu-id="2de7e-189">Each of these counters should continue to increase as the demonstration executes, with ***thread_1_counter** _ and _ *_thread_2_counter_** increasing at the fastest rate.</span></span>

## <a name="distribution-file-demo_threadxc"></a><span data-ttu-id="2de7e-190">File di distribuzione: demo_threadx. c</span><span class="sxs-lookup"><span data-stu-id="2de7e-190">Distribution file: demo_threadx.c</span></span>

<span data-ttu-id="2de7e-191">In questa sezione viene visualizzato l'elenco completo di ***demo_threadx. c***, inclusi i numeri di riga a cui si fa riferimento in questo capitolo.</span><span class="sxs-lookup"><span data-stu-id="2de7e-191">This section displays the complete listing of ***demo_threadx.c***, including the line numbers referenced throughout this chapter.</span></span>

```c
/* This is a small demo of the high-performance ThreadX kernel. It includes examples of eight
threads of different priorities, using a message queue, semaphore, mutex, event flags group,
byte pool, and block pool. */

#include "tx_api.h"

#define DEMO_STACK_SIZE 1024
#define DEMO_BYTE_POOL_SIZE 9120
#define DEMO_BLOCK_POOL_SIZE 100
#define DEMO_QUEUE_SIZE 100

/* Define the ThreadX object control blocks... */

TX_THREAD thread_0;
TX_THREAD thread_1;
TX_THREAD thread_2;
TX_THREAD thread_3;
TX_THREAD thread_4;
TX_THREAD thread_5;
TX_THREAD thread_6;
TX_THREAD thread_7;
TX_QUEUE queue_0;
TX_SEMAPHORE semaphore_0;
TX_MUTEX mutex_0;
TX_EVENT_FLAGS_GROUP event_flags_0;
TX_BYTE_POOL byte_pool_0;
TX_BLOCK_POOL block_pool_0;

/* Define the counters used in the demo application... */

ULONG thread_0_counter;
ULONG thread_1_counter;
ULONG thread_1_messages_sent;
ULONG thread_2_counter;
ULONG thread_2_messages_received;
ULONG thread_3_counter;
ULONG thread_4_counter;
ULONG thread_5_counter;
ULONG thread_6_counter;
ULONG thread_7_counter;

/* Define thread prototypes. */

void thread_0_entry(ULONG thread_input);
void thread_1_entry(ULONG thread_input);
void thread_2_entry(ULONG thread_input);
void thread_3_and_4_entry(ULONG thread_input);
void thread_5_entry(ULONG thread_input);
void thread_6_and_7_entry(ULONG thread_input);


/* Define main entry point. */

int main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */
void tx_application_define(void *first_unused_memory)
{

    CHAR *pointer;

    /* Create a byte memory pool from which to allocate the thread stacks. */
    tx_byte_pool_create(&byte_pool_0, "byte pool 0", first_unused_memory,
        DEMO_BYTE_POOL_SIZE);

    /* Put system definition stuff in here, e.g., thread creates and other assorted
        create information. */

    /* Allocate the stack for thread 0. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create the main thread. */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
        pointer, DEMO_STACK_SIZE,
        1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 1. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 1 and 2. These threads pass information through a ThreadX
        message queue. It is also interesting to note that these threads have a time
        slice. */
    tx_thread_create(&thread_1, "thread 1", thread_1_entry, 1,
        pointer, DEMO_STACK_SIZE,
        16, 16, 4, TX_AUTO_START);

    /* Allocate the stack for thread 2. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);
        tx_thread_create(&thread_2, "thread 2", thread_2_entry, 2,
        pointer, DEMO_STACK_SIZE,
        16, 16, 4, TX_AUTO_START);

    /* Allocate the stack for thread 3. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 3 and 4. These threads compete for a ThreadX counting semaphore.
        An interesting thing here is that both threads share the same instruction area. */
    tx_thread_create(&thread_3, "thread 3", thread_3_and_4_entry, 3,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 4. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    tx_thread_create(&thread_4, "thread 4", thread_3_and_4_entry, 4,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 5. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create thread 5. This thread simply pends on an event flag, which will be set
        by thread_0. */
    tx_thread_create(&thread_5, "thread 5", thread_5_entry, 5,
        pointer, DEMO_STACK_SIZE,
        4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 6. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 6 and 7. These threads compete for a ThreadX mutex. */
    tx_thread_create(&thread_6, "thread 6", thread_6_and_7_entry, 6,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 7. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_STACK_SIZE, TX_NO_WAIT);

    tx_thread_create(&thread_7, "thread 7", thread_6_and_7_entry, 7,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the message queue. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_QUEUE_SIZE*sizeof(ULONG), TX_NO_WAIT);

    /* Create the message queue shared by threads 1 and 2. */
    tx_queue_create(&queue_0, "queue 0", TX_1_ULONG, pointer, DEMO_QUEUE_SIZE*sizeof(ULONG));

    /* Create the semaphore used by threads 3 and 4. */
    tx_semaphore_create(&semaphore_0, "semaphore 0", 1);

    /* Create the event flags group used by threads 1 and 5. */
    tx_event_flags_create(&event_flags_0, "event flags 0");

    /* Create the mutex used by thread 6 and 7 without priority inheritance. */
    tx_mutex_create(&mutex_0, "mutex 0", TX_NO_INHERIT);

    /* Allocate the memory for a small block pool. */
    tx_byte_allocate(&byte_pool_0, &pointer, DEMO_BLOCK_POOL_SIZE, TX_NO_WAIT);

    /* Create a block memory pool to allocate a message buffer from. */
    tx_block_pool_create(&block_pool_0, "block pool 0", sizeof(ULONG), pointer,
        DEMO_BLOCK_POOL_SIZE);

    /* Allocate a block and release the block memory. */
    tx_block_allocate(&block_pool_0, &pointer, TX_NO_WAIT);

    /* Release the block back to the pool. */
    tx_block_release(pointer);
}

/* Define the test threads. */
void thread_0_entry(ULONG thread_input)
{
    UINT status;


    /* This thread simply sits in while-forever-sleep loop. */
    while(1)
    {

        /* Increment the thread counter. */
        thread_0_counter++;

        /* Sleep for 10 ticks. */
        tx_thread_sleep(10);

        /* Set event flag 0 to wakeup thread 5. */
        status = tx_event_flags_set(&event_flags_0, 0x1, TX_OR);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;
    }
}


void thread_1_entry(ULONG thread_input)
{
    UINT status;


    /* This thread simply sends messages to a queue shared by thread 2. */
    while(1)
    {
        /* Increment the thread counter. */
        thread_1_counter++;

        /* Send message to queue 0. */
        status = tx_queue_send(&queue_0, &thread_1_messages_sent, TX_WAIT_FOREVER);

        /* Check completion status. */
        if (status != TX_SUCCESS)
            break;

        /* Increment the message sent. */
        thread_1_messages_sent++;
    }
}


void thread_2_entry(ULONG thread_input)
{
    ULONG received_message;
    UINT status;

    /* This thread retrieves messages placed on the queue by thread 1. */
    while(1)
    {
        /* Increment the thread counter. */
        thread_2_counter++;

        /* Retrieve a message from the queue. */
        status = tx_queue_receive(&queue_0, &received_message, TX_WAIT_FOREVER);

        /* Check completion status and make sure the message is what we
        expected. */
        if ((status != TX_SUCCESS) || (received_message != thread_2_messages_received))
            break;

        /* Otherwise, all is okay. Increment the received message count. */
        thread_2_messages_received++;
    }
}


void thread_3_and_4_entry(ULONG thread_input)
{
    UINT status;


    /* This function is executed from thread 3 and thread 4. As the loop
    below shows, these function compete for ownership of semaphore_0. */
    while(1)
    {
        /* Increment the thread counter. */
        if (thread_input == 3)
            thread_3_counter++;
        else
            thread_4_counter++;

        /* Get the semaphore with suspension. */
        status = tx_semaphore_get(&semaphore_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Sleep for 2 ticks to hold the semaphore. */
        tx_thread_sleep(2);

        /* Release the semaphore. */
        status = tx_semaphore_put(&semaphore_0);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;
    }
}


void thread_5_entry(ULONG thread_input)
{
    UINT status;
    ULONG actual_flags;


    /* This thread simply waits for an event in a forever loop. */
    while(1)
    {
        /* Increment the thread counter. */
        thread_5_counter++;

        /* Wait for event flag 0. */
        status = tx_event_flags_get(&event_flags_0, 0x1, TX_OR_CLEAR,
            &actual_flags, TX_WAIT_FOREVER);

        /* Check status. */
        if ((status != TX_SUCCESS) || (actual_flags != 0x1))
            break;
    }
}

void thread_6_and_7_entry(ULONG thread_input)
{
    UINT status;

    /* This function is executed from thread 6 and thread 7. As the loop
        below shows, these function compete for ownership of mutex_0. */
    while(1)
    {
        /* Increment the thread counter. */
        if (thread_input == 6)
            thread_6_counter++;
        else
            thread_7_counter++;

        /* Get the mutex with suspension. */
        status = tx_mutex_get(&mutex_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Get the mutex again with suspension. This shows
            that an owning thread may retrieve the mutex it
            owns multiple times. */
        status = tx_mutex_get(&mutex_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Sleep for 2 ticks to hold the mutex. */
        tx_thread_sleep(2);

        /* Release the mutex. */
        status = tx_mutex_put(&mutex_0);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Release the mutex again. This will actually
            release ownership since it was obtained twice. */
        status = tx_mutex_put(&mutex_0);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;
    }
}
```
