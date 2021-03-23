---
title: Capitolo 5-generazione di buffer di traccia
description: Questo capitolo contiene una descrizione della creazione di un buffer di eventi TraceX di Azure RTO e descrive anche il formato sottostante del buffer.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: f296137d23b9f3c1c4fd115947bb50a32b768123
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823426"
---
# <a name="chapter-5---generating-trace-buffers"></a><span data-ttu-id="7365f-103">Capitolo 5-generazione di buffer di traccia</span><span class="sxs-lookup"><span data-stu-id="7365f-103">Chapter 5 - Generating trace buffers</span></span>

<span data-ttu-id="7365f-104">Questo capitolo contiene una descrizione della creazione di un buffer di eventi TraceX di Azure RTO e descrive anche il formato sottostante del buffer.</span><span class="sxs-lookup"><span data-stu-id="7365f-104">This chapter contains a description about how to build a Azure RTOS TraceX event buffer and also describes the underlying format of the buffer.</span></span>

## <a name="threadx-event-trace-support"></a><span data-ttu-id="7365f-105">Supporto per la traccia eventi ThreadX</span><span class="sxs-lookup"><span data-stu-id="7365f-105">ThreadX Event Trace Support</span></span>

<span data-ttu-id="7365f-106">ThreadX fornisce il supporto predefinito per la traccia degli eventi per tutti i servizi ThreadX, le modifiche allo stato del thread e gli eventi definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="7365f-106">ThreadX provides built-in event trace support for all ThreadX services, thread state changes, and user-defined events.</span></span> <span data-ttu-id="7365f-107">La funzionalità di traccia degli eventi di ThreadX è progettata principalmente come strumento post-mortem per analizzare le ultime attività "n" nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7365f-107">The ThreadX event-trace capability is primarily designed as a post-mortem tool to analyze the last "n" activities in the application.</span></span> <span data-ttu-id="7365f-108">Da queste informazioni, lo sviluppatore può individuare problemi e/o potenziali destinazioni di ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="7365f-108">From this information, the developer may spot problems and/or potential targets of optimization.</span></span>

<span data-ttu-id="7365f-109">TraceX Visualizza graficamente il buffer di traccia eventi compilato da ThreadX.</span><span class="sxs-lookup"><span data-stu-id="7365f-109">TraceX graphically displays the event trace buffer built by ThreadX.</span></span> <span data-ttu-id="7365f-110">Di seguito viene descritto come compilare il buffer e viene descritto il formato sottostante del buffer.</span><span class="sxs-lookup"><span data-stu-id="7365f-110">The following describes how to build the buffer and describes the underlying format of the buffer.</span></span>

## <a name="enabling-event-trace"></a><span data-ttu-id="7365f-111">Abilitazione della traccia eventi</span><span class="sxs-lookup"><span data-stu-id="7365f-111">Enabling Event Trace</span></span>

<span data-ttu-id="7365f-112">Per abilitare la traccia eventi, definire le costanti timestamp, compilare la libreria ThreadX con **TX_ENABLE_EVENT_TRACE** definito e abilitare la traccia chiamando la funzione **tx_trace_enable** .</span><span class="sxs-lookup"><span data-stu-id="7365f-112">To enable event trace, define the time-stamp constants, build the ThreadX library with **TX_ENABLE_EVENT_TRACE** defined, and enable tracing by calling the **tx_trace_enable** function.</span></span>

## <a name="defining-time-stamp-constants"></a><span data-ttu-id="7365f-113">Definizione di costanti Time-Stamp</span><span class="sxs-lookup"><span data-stu-id="7365f-113">Defining Time-Stamp Constants</span></span>

<span data-ttu-id="7365f-114">Le costanti timestamp sono progettate per fornire al controllo dello sviluppatore il timestamp usato nelle voci della traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="7365f-114">The time-stamp constants are designed to provide the developer control over the time-stamp used in the event trace entries.</span></span> <span data-ttu-id="7365f-115">Di seguito sono riportate le due costanti timestamp e i relativi valori predefiniti:</span><span class="sxs-lookup"><span data-stu-id="7365f-115">The two time-stamp constants and their default values are as follows:</span></span>

```c
#ifndef TX_TRACE_TIME_SOURCE
#define TX_TRACE_TIME_SOURCE ++_tx_trace_simulated_time
#endif
#ifndef TX_TRACE_TIME_MASK
#define TX_TRACE_TIME_MASK   0xFFFFFFFFUL
#endif
```

<span data-ttu-id="7365f-116">Le costanti precedenti sono definite in **tx_port. h** e creano un timestamp "Fake" che viene semplicemente incrementato di uno per ogni evento.</span><span class="sxs-lookup"><span data-stu-id="7365f-116">The above constants are defined in **tx_port.h** and create a "fake" time-stamp that simply increments by one on each event.</span></span> <span data-ttu-id="7365f-117">Di seguito è riportato un esempio di definizione di timestamp effettiva:</span><span class="sxs-lookup"><span data-stu-id="7365f-117">The following is an example of an actual timestamp definition:</span></span>

```c
#ifndef TX_TRACE_TIME_SOURCE
#define TX_TRACE_TIME_SOURCE ((ULONG) 0x0x13000004)
#endif
#ifndef TX_TRACE_TIME_MASK
#define TX_TRACE_TIME_MASK 0xFFFFFFFFUL
#endif
```

<span data-ttu-id="7365f-118">Le costanti sopra indicate specificano un timer a 32 bit ottenuto leggendo l'indirizzo 0x13000004.</span><span class="sxs-lookup"><span data-stu-id="7365f-118">The above constants specify a 32-bit timer that is obtained by reading the address 0x13000004.</span></span> <span data-ttu-id="7365f-119">La maggior parte dei timestamp specifici dell'applicazione devono essere impostati in modo analogo.</span><span class="sxs-lookup"><span data-stu-id="7365f-119">Most application specific time-stamps should be setup in a similar fashion.</span></span>

## <a name="exporting-the-trace-buffer"></a><span data-ttu-id="7365f-120">Esportazione del buffer di traccia</span><span class="sxs-lookup"><span data-stu-id="7365f-120">Exporting the Trace Buffer</span></span>

<span data-ttu-id="7365f-121">TraceX richiede il buffer di traccia in un formato di file binario, Intel HEX o Motorola S-record nell'host.</span><span class="sxs-lookup"><span data-stu-id="7365f-121">TraceX needs the trace buffer in a binary, Intel HEX, or Motorola S-Record file format on the host.</span></span> <span data-ttu-id="7365f-122">Il modo più semplice per eseguire questa operazione consiste nell'arrestare la destinazione e indicare al debugger di eseguire il dump dell'area di memoria fornita per ***tx_trace_enable*** funzione in un file nell'host.</span><span class="sxs-lookup"><span data-stu-id="7365f-122">The easiest way to accomplish this is to stop the target and instruct your debugger to dump the memory area you supplied to ***tx_trace_enable*** function into a file on the host.</span></span>

> [!WARNING]
><span data-ttu-id="7365f-123">***Prestare attenzione a non arrestare la destinazione all'interno di un codice di raccolta della traccia. Questa operazione può causare informazioni di traccia non valide. Se il programma viene interrotto all'interno di ThreadX, è preferibile eseguire un'istruzione/routine di ogni macro di inserimento della traccia prima di eseguire il dump del buffer di traccia.***</span><span class="sxs-lookup"><span data-stu-id="7365f-123">***Be careful not to stop the target within a trace gathering code itself. Doing so can cause invalid trace information. If the program is halted within ThreadX, it is best to step over any trace insert macro before dumping the trace buffer.***</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7365f-124">*Nell'Appendice D viene illustrato come eseguire il dump del buffer di traccia da un'ampia gamma di strumenti di sviluppo.*</span><span class="sxs-lookup"><span data-stu-id="7365f-124">*Appendix D shows how to dump the trace buffer from within a variety of development tools.*</span></span>

## <a name="extended-event-trace-api"></a><span data-ttu-id="7365f-125">API di traccia degli eventi estesi</span><span class="sxs-lookup"><span data-stu-id="7365f-125">Extended Event Trace API</span></span>

<span data-ttu-id="7365f-126">Quando ThreadX viene compilato con **TX_ENABLE_EVENT_TRACE** definito, per l'applicazione sono disponibili le nuove API di traccia eventi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7365f-126">When ThreadX is built with **TX_ENABLE_EVENT_TRACE** defined, the following new event trace APIs are available to the application:</span></span>

- <span data-ttu-id="7365f-127">tx_trace_enable: *Abilita traccia eventi*</span><span class="sxs-lookup"><span data-stu-id="7365f-127">tx_trace_enable: *Enable event tracing*</span></span>
- <span data-ttu-id="7365f-128">tx_trace_event_filter: *Filtra evento/i specificato/i*</span><span class="sxs-lookup"><span data-stu-id="7365f-128">tx_trace_event_filter: *Filter specified event(s)*</span></span>
- <span data-ttu-id="7365f-129">tx_trace_event_unfilter: non *filtrare gli eventi specificati*</span><span class="sxs-lookup"><span data-stu-id="7365f-129">tx_trace_event_unfilter: *Unfilter specified event(s)*</span></span>
- <span data-ttu-id="7365f-130">tx_trace_disable: *Disabilita traccia eventi*</span><span class="sxs-lookup"><span data-stu-id="7365f-130">tx_trace_disable: *Disable event tracing*</span></span>
- <span data-ttu-id="7365f-131">tx_trace_isr_enter_insert: *Inserisci l'evento di traccia ISR*</span><span class="sxs-lookup"><span data-stu-id="7365f-131">tx_trace_isr_enter_insert: *Insert ISR enter trace event*</span></span>
- <span data-ttu-id="7365f-132">tx_trace_isr_exit_insert: *Inserisci evento di traccia di uscita ISR*</span><span class="sxs-lookup"><span data-stu-id="7365f-132">tx_trace_isr_exit_insert: *Insert ISR exit trace event*</span></span>
- <span data-ttu-id="7365f-133">tx_trace_buffer_full_notify: *registrare il callback dell'applicazione completo del buffer di traccia*</span><span class="sxs-lookup"><span data-stu-id="7365f-133">tx_trace_buffer_full_notify: *Register trace buffer full application callback*</span></span>
- <span data-ttu-id="7365f-134">tx_trace_user_event_insert: *Inserisci evento utente*</span><span class="sxs-lookup"><span data-stu-id="7365f-134">tx_trace_user_event_insert: *Insert user event*</span></span>

### <a name="tx_trace_enable"></a><span data-ttu-id="7365f-135">tx_trace_enable</span><span class="sxs-lookup"><span data-stu-id="7365f-135">tx_trace_enable</span></span>

<span data-ttu-id="7365f-136">Abilitare la traccia eventi</span><span class="sxs-lookup"><span data-stu-id="7365f-136">Enable event tracing</span></span>

#### <a name="prototype"></a><span data-ttu-id="7365f-137">Prototipo</span><span class="sxs-lookup"><span data-stu-id="7365f-137">Prototype</span></span>

```c
UINT tx_trace_enable (VOID *trace_buffer_start,
     ULONG trace_buffer_size, ULONG registry_entries);
```

#### <a name="description"></a><span data-ttu-id="7365f-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7365f-138">Description</span></span>
<span data-ttu-id="7365f-139">Questo servizio Abilita la traccia eventi all'interno di ThreadX.</span><span class="sxs-lookup"><span data-stu-id="7365f-139">This service enables event tracing inside ThreadX.</span></span> <span data-ttu-id="7365f-140">Il buffer di traccia e il numero massimo di oggetti ThreadX vengono forniti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7365f-140">The trace buffer and the maximum number of ThreadX objects are supplied by the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7365f-141">La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="7365f-141">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="7365f-142">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="7365f-142">Input Parameters</span></span>

- <span data-ttu-id="7365f-143">**trace_buffer_start**: puntatore all'inizio del buffer di traccia fornito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="7365f-143">**trace_buffer_start**: Pointer to the start of the user-supplied trace buffer.</span></span>
- <span data-ttu-id="7365f-144">**trace_buffer_size**: numero totale di byte nella memoria per il buffer di traccia.</span><span class="sxs-lookup"><span data-stu-id="7365f-144">**trace_buffer_size**: Total number of bytes in the memory for the trace buffer.</span></span> <span data-ttu-id="7365f-145">Maggiore è il buffer di traccia, maggiore è il numero di voci che è in grado di archiviare.</span><span class="sxs-lookup"><span data-stu-id="7365f-145">The larger the trace buffer, the more entries it is able to store.</span></span>
- <span data-ttu-id="7365f-146">**registry_entries**: numero di oggetti threadX dell'applicazione da tenere nel registro di traccia.</span><span class="sxs-lookup"><span data-stu-id="7365f-146">**registry_entries**: Number of application ThreadX objects to keep in the trace registry.</span></span> <span data-ttu-id="7365f-147">Il registro di sistema viene utilizzato per correlare gli indirizzi di oggetto con i nomi degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="7365f-147">The registry is used to correlate object addresses with object names.</span></span> <span data-ttu-id="7365f-148">Questa operazione è particolarmente utile per gli strumenti di analisi della traccia GUI.</span><span class="sxs-lookup"><span data-stu-id="7365f-148">This is highly useful for GUI trace analysis tools.</span></span>

#### <a name="return-values"></a><span data-ttu-id="7365f-149">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="7365f-149">Return Values</span></span>

- <span data-ttu-id="7365f-150">Abilitazione della traccia eventi riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="7365f-150">**TX_SUCCESS** (0x00) Successful event trace enable.</span></span>
- <span data-ttu-id="7365f-151">Dimensioni del buffer di traccia **TX_SIZE_ERROR** (0x05) specificate troppo piccole.</span><span class="sxs-lookup"><span data-stu-id="7365f-151">**TX_SIZE_ERROR** (0x05) Specified trace buffer size is too small.</span></span> <span data-ttu-id="7365f-152">Deve essere sufficientemente grande per l'intestazione di traccia, il registro oggetti e almeno una voce di traccia.</span><span class="sxs-lookup"><span data-stu-id="7365f-152">It must be large enough for the trace header, the object registry, and at least one trace entry.</span></span>
- <span data-ttu-id="7365f-153">La traccia eventi **TX_NOT_DONE** (0x20) è già stata abilitata.</span><span class="sxs-lookup"><span data-stu-id="7365f-153">**TX_NOT_DONE** (0x20) Event tracing was already enabled.</span></span>
- <span data-ttu-id="7365f-154">Il sistema **TX_FEATURE_NOT_ENABLED** (0xFF) non è stato compilato con la traccia abilitata.</span><span class="sxs-lookup"><span data-stu-id="7365f-154">**TX_FEATURE_NOT_ENABLED** (0xFF) System was not compiled with trace enabled.</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="7365f-155">Consentito da</span><span class="sxs-lookup"><span data-stu-id="7365f-155">Allowed From</span></span>

<span data-ttu-id="7365f-156">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="7365f-156">Initialization and threads</span></span>

#### <a name="example"></a><span data-ttu-id="7365f-157">Esempio</span><span class="sxs-lookup"><span data-stu-id="7365f-157">Example</span></span>

```c
UCHAR my_trace_buffer[64000];

/* Enable event tracing using the global "my_trace_buffer" memory and supporting a maximum of 30 ThreadX objects in the registry. */
status = tx_trace_enable (&my_trace_buffer, 64000, 30);

/* If status is TX_SUCCESS the event tracing is enabled. */
```

#### <a name="see-also"></a><span data-ttu-id="7365f-158">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7365f-158">See Also</span></span>

<span data-ttu-id="7365f-159">tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="7365f-159">tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_event_filter"></a><span data-ttu-id="7365f-160">tx_trace_event_filter</span><span class="sxs-lookup"><span data-stu-id="7365f-160">tx_trace_event_filter</span></span>

<span data-ttu-id="7365f-161">Filtra eventi specificati</span><span class="sxs-lookup"><span data-stu-id="7365f-161">Filter specified events</span></span>

#### <a name="prototype"></a><span data-ttu-id="7365f-162">Prototipo</span><span class="sxs-lookup"><span data-stu-id="7365f-162">Prototype</span></span>

```c
UINT tx_trace_event_filter (ULONG  vent_filter_bits);
```

#### <a name="description"></a><span data-ttu-id="7365f-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7365f-163">Description</span></span>

<span data-ttu-id="7365f-164">Questo servizio filtra gli eventi specificati da inserire nel buffer di traccia attivo.</span><span class="sxs-lookup"><span data-stu-id="7365f-164">This service filters the specified event(s) from being inserted into the active trace buffer.</span></span> <span data-ttu-id="7365f-165">Si noti che per impostazione predefinita nessun evento viene filtrato dopo la chiamata di *tx_trace_enable* .</span><span class="sxs-lookup"><span data-stu-id="7365f-165">Note that by default no events are filtered after *tx_trace_enable* is called.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7365f-166">La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="7365f-166">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="7365f-167">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="7365f-167">Input Parameters</span></span>

- <span data-ttu-id="7365f-168">**event_filter_bits**: bit che corrispondono agli eventi da filtrare.</span><span class="sxs-lookup"><span data-stu-id="7365f-168">**event_filter_bits**: Bits that correspond to events to filter.</span></span> <span data-ttu-id="7365f-169">È possibile filtrare più eventi semplicemente ORing insieme le costanti appropriate.</span><span class="sxs-lookup"><span data-stu-id="7365f-169">Multiple events may be filtered by simply oring together the appropriate constants.</span></span> <span data-ttu-id="7365f-170">Le costanti valide per questa variabile sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="7365f-170">Valid constants for this variable are defined as follows:</span></span>

```c
TX_TRACE_ALL_EVENTS                   0x000007FF
TX_TRACE_INTERNAL_EVENTS              0x00000001
TX_TRACE_BLOCK_POOL_EVENTS            0x00000002
TX_TRACE_BYTE_POOL_EVENTS             0x00000004
TX_TRACE_EVENT_FLAGS_EVENTS           0x00000008
TX_TRACE_INTERRUPT_CONTROL_EVENT      0x00000010
TX_TRACE_MUTEX_EVENTS                 0x00000020
TX_TRACE_QUEUE_EVENTS                 0x00000040
TX_TRACE_SEMAPHORE_EVENTS             0x00000080
TX_TRACE_THREAD_EVENTS                0x00000100
TX_TRACE_TIME_EVENTS                  0x00000200
TX_TRACE_TIMER_EVENTS                 0x00000400
FX_TRACE_ALL_EVENTS                   0x00007800
FX_TRACE_INTERNAL_EVENTS              0x00000800
FX_TRACE_MEDIA_EVENTS                 0x00001000
FX_TRACE_DIRECTORY_EVENTS             0x00002000
FX_TRACE_FILE_EVENTS                  0x00004000
NX_TRACE_ALL_EVENTS                   0x00FF8000
NX_TRACE_INTERNAL_EVENTS              0x00008000
NX_TRACE_ARP_EVENTS                   0x00010000
NX_TRACE_ICMP_EVENTS                  0x00020000
NX_TRACE_IGMP_EVENTS                  0x00040000
NX_TRACE_IP_EVENTS                    0x00080000
NX_TRACE_PACKET_EVENTS                0x00100000
NX_TRACE_RARP_EVENTS                  0x00200000
NX_TRACE_TCP_EVENTS                   0x00400000
NX_TRACE_UDP_EVENTS                   0x00800000
UX_TRACE_ALL_EVENTS                   0x7F000000
UX_TRACE_ERRORS                       0x01000000
UX_TRACE_HOST_STACK_EVENTS            0x02000000
UX_TRACE_DEVICE_STACK_EVENTS          0x04000000
UX_TRACE_HOST_CONTROLLER_EVENTS       0x08000000
UX_TRACE_DEVICE_CONTROLLER_EVENTS     0x10000000
UX_TRACE_HOST_CLASS_EVENTS            0x20000000
UX_TRACE_DEVICE_CLASS_EVENTS          0x40000000
```

#### <a name="return-values"></a><span data-ttu-id="7365f-171">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="7365f-171">Return Values</span></span>

- <span data-ttu-id="7365f-172">**TX_SUCCESS** (0x00) filtro eventi riuscito.</span><span class="sxs-lookup"><span data-stu-id="7365f-172">**TX_SUCCESS** (0x00) Successful event filter.</span></span>
- <span data-ttu-id="7365f-173">Il sistema **TX_FEATURE_NOT_ENABLED** (0xFF) non è stato compilato con la traccia abilitata.</span><span class="sxs-lookup"><span data-stu-id="7365f-173">**TX_FEATURE_NOT_ENABLED** (0xFF) System was not compiled with trace enabled.</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="7365f-174">Consentito da</span><span class="sxs-lookup"><span data-stu-id="7365f-174">Allowed From</span></span>

<span data-ttu-id="7365f-175">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="7365f-175">Initialization and threads</span></span>

#### <a name="example"></a><span data-ttu-id="7365f-176">Esempio</span><span class="sxs-lookup"><span data-stu-id="7365f-176">Example</span></span>

```c
/* Filter queue and byte pool events from trace buffer. */

status = tx_trace_event_filter (TX_TRACE_QUEUE_EVENTS | TX_TRACE_BYTE_POOL_EVENTS);

/* If status is TX_SUCCESS all queue and byte pool events are filtered. */
```

#### <a name="see-also"></a><span data-ttu-id="7365f-177">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7365f-177">See Also</span></span>

<span data-ttu-id="7365f-178">tx_trace_enable, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="7365f-178">tx_trace_enable, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_event_unfilter"></a><span data-ttu-id="7365f-179">tx_trace_event_unfilter</span><span class="sxs-lookup"><span data-stu-id="7365f-179">tx_trace_event_unfilter</span></span>

<span data-ttu-id="7365f-180">Non filtrare gli eventi specificati</span><span class="sxs-lookup"><span data-stu-id="7365f-180">Unfilter specified events</span></span>

#### <a name="prototype"></a><span data-ttu-id="7365f-181">Prototipo</span><span class="sxs-lookup"><span data-stu-id="7365f-181">Prototype</span></span>

```c
UINT tx_trace_event_unfilter (ULONG event_unfilter_bits);
```

#### <a name="description"></a><span data-ttu-id="7365f-182">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7365f-182">Description</span></span>

<span data-ttu-id="7365f-183">Questo servizio è in grado di filtrare gli eventi specificati in modo che vengano inseriti nel buffer di traccia attivo.</span><span class="sxs-lookup"><span data-stu-id="7365f-183">This service unfilters the specified event(s) such that they will be inserted into the active trace buffer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7365f-184">La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="7365f-184">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="7365f-185">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="7365f-185">Input Parameters</span></span>

- <span data-ttu-id="7365f-186">**event_unfilter_bits**: bit che corrispondono agli eventi da defiltrare.</span><span class="sxs-lookup"><span data-stu-id="7365f-186">**event_unfilter_bits**: Bits that correspond to events to unfilter.</span></span> <span data-ttu-id="7365f-187">È possibile che più eventi non vengano filtrati semplicemente o-insieme alle costanti appropriate.</span><span class="sxs-lookup"><span data-stu-id="7365f-187">Multiple events may be unfiltered by simply or-ing together the appropriate constants.</span></span> <span data-ttu-id="7365f-188">Le costanti valide per questa variabile sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="7365f-188">Valid constants for this variable are defined as follows:</span></span>

```c
TX_TRACE_ALL_EVENTS                  0x000007FF
TX_TRACE_INTERNAL_EVENTS             0x00000001
TX_TRACE_BLOCK_POOL_EVENTS           0x00000002
TX_TRACE_BYTE_POOL_EVENTS            0x00000004
TX_TRACE_EVENT_FLAGS_EVENTS          0x00000008
TX_TRACE_INTERRUPT_CONTROL_EVENT     0x00000010
TX_TRACE_MUTEX_EVENTS                0x00000020
TX_TRACE_QUEUE_EVENTS                0x00000040
TX_TRACE_SEMAPHORE_EVENTS            0x00000080
TX_TRACE_THREAD_EVENTS               0x00000100
TX_TRACE_TIME_EVENTS                 0x00000200
TX_TRACE_TIMER_EVENTS                0x00000400
FX_TRACE_ALL_EVENTS                  0x00007800
FX_TRACE_INTERNAL_EVENTS             0x00000800
FX_TRACE_MEDIA_EVENTS                0x00001000
FX_TRACE_DIRECTORY_EVENTS            0x00002000
FX_TRACE_FILE_EVENTS                 0x00004000
NX_TRACE_ALL_EVENTS                  0x00FF8000
NX_TRACE_INTERNAL_EVENTS             0x00008000
NX_TRACE_ARP_EVENTS                  0x00010000
NX_TRACE_ICMP_EVENTS                 0x00020000
NX_TRACE_IGMP_EVENTS                 0x00040000
NX_TRACE_IP_EVENTS                   0x00080000
NX_TRACE_PACKET_EVENTS               0x00100000
NX_TRACE_RARP_EVENTS                 0x00200000
NX_TRACE_TCP_EVENTS                  0x00400000
NX_TRACE_UDP_EVENTS                  0x00800000
UX_TRACE_ALL_EVENTS                  0x7F000000
UX_TRACE_ERRORS                      0x01000000
UX_TRACE_HOST_STACK_EVENTS           0x02000000
UX_TRACE_DEVICE_STACK_EVENTS         0x04000000
UX_TRACE_HOST_CONTROLLER_EVENTS      0x08000000
UX_TRACE_DEVICE_CONTROLLER_EVENTS    0x10000000
UX_TRACE_HOST_CLASS_EVENTS           0x20000000
UX_TRACE_DEVICE_CLASS_EVENTS         0x40000000
```

#### <a name="return-values"></a><span data-ttu-id="7365f-189">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="7365f-189">Return Values</span></span>

- <span data-ttu-id="7365f-190">Defiltro evento riuscito **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="7365f-190">**TX_SUCCESS** (0x00) Successful event unfilter.</span></span>
- <span data-ttu-id="7365f-191">Il sistema **TX_FEATURE_NOT_ENABLED** (0xFF) non è stato compilato con la traccia abilitata.</span><span class="sxs-lookup"><span data-stu-id="7365f-191">**TX_FEATURE_NOT_ENABLED** (0xFF) System was not compiled with trace enabled.</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="7365f-192">Consentito da</span><span class="sxs-lookup"><span data-stu-id="7365f-192">Allowed From</span></span>

<span data-ttu-id="7365f-193">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="7365f-193">Initialization and threads</span></span>

#### <a name="example"></a><span data-ttu-id="7365f-194">Esempio</span><span class="sxs-lookup"><span data-stu-id="7365f-194">Example</span></span>

```c
/* Un-filter queue and byte pool events from trace buffer. */ 
status = 
  tx_trace_event_unfilter (TX_TRACE_QUEUE_EVENTS | TX_TRACE_BYTE_POOL_EVENTS);

/* If status is TX_SUCCESS all queue and byte pool events are un-filtered. */
```

#### <a name="see-also"></a><span data-ttu-id="7365f-195">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7365f-195">See Also</span></span>

<span data-ttu-id="7365f-196">tx_trace_enable, tx_trace_event_filter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="7365f-196">tx_trace_enable, tx_trace_event_filter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_disable"></a><span data-ttu-id="7365f-197">tx_trace_disable</span><span class="sxs-lookup"><span data-stu-id="7365f-197">tx_trace_disable</span></span>

#### <a name="disable-event-tracing"></a><span data-ttu-id="7365f-198">Disabilita traccia eventi</span><span class="sxs-lookup"><span data-stu-id="7365f-198">Disable event tracing</span></span>

#### <a name="prototype"></a><span data-ttu-id="7365f-199">Prototipo</span><span class="sxs-lookup"><span data-stu-id="7365f-199">Prototype</span></span>

```c
UINT tx_trace_disable (VOID);
```

#### <a name="description"></a><span data-ttu-id="7365f-200">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7365f-200">Description</span></span>

<span data-ttu-id="7365f-201">Questo servizio Disabilita la traccia eventi all'interno di ThreadX.</span><span class="sxs-lookup"><span data-stu-id="7365f-201">This service disables event tracing inside ThreadX.</span></span> <span data-ttu-id="7365f-202">Questa operazione può essere utile se l'applicazione desidera bloccare il buffer di traccia dell'evento corrente ed eventualmente trasferirlo esternamente durante la fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7365f-202">This can be useful if the application wants to freeze the current event trace buffer and possibly transport it externally during run-time.</span></span> <span data-ttu-id="7365f-203">Una volta disabilitato, è possibile chiamare il **tx_trace_enable** per avviare di nuovo la traccia.</span><span class="sxs-lookup"><span data-stu-id="7365f-203">Once disabled, the **tx_trace_enable** can be called to start tracing again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7365f-204">La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="7365f-204">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="7365f-205">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="7365f-205">Input Parameters</span></span>

<span data-ttu-id="7365f-206">Nessuna.</span><span class="sxs-lookup"><span data-stu-id="7365f-206">None.</span></span>

#### <a name="return-values"></a><span data-ttu-id="7365f-207">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="7365f-207">Return Values</span></span>

- <span data-ttu-id="7365f-208">Disattivazione della traccia eventi riuscita **TX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="7365f-208">**TX_SUCCESS** (0x00) Successful event trace disable.</span></span>
- <span data-ttu-id="7365f-209">La traccia eventi **TX_NOT_DONE** (0x20) non è stata abilitata.</span><span class="sxs-lookup"><span data-stu-id="7365f-209">**TX_NOT_DONE** (0x20) Event tracing was not enabled.</span></span>
- <span data-ttu-id="7365f-210">Il sistema **TX_FEATURE_NOT_ENABLED** (0xFF) non è stato compilato con la traccia abilitata.</span><span class="sxs-lookup"><span data-stu-id="7365f-210">**TX_FEATURE_NOT_ENABLED** (0xFF) System was not compiled with trace enabled.</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="7365f-211">Consentito da</span><span class="sxs-lookup"><span data-stu-id="7365f-211">Allowed From</span></span>

<span data-ttu-id="7365f-212">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="7365f-212">Initialization and threads</span></span>

#### <a name="example"></a><span data-ttu-id="7365f-213">Esempio</span><span class="sxs-lookup"><span data-stu-id="7365f-213">Example</span></span> 

```c
/* Disable event tracing. */ 
status = tx_trace_disable ();

/* If status is TX_SUCCESS the event tracing is disabled. */
```

#### <a name="see-also"></a><span data-ttu-id="7365f-214">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7365f-214">See Also</span></span>

<span data-ttu-id="7365f-215">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="7365f-215">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_isr_enter_insert"></a><span data-ttu-id="7365f-216">tx_trace_isr_enter_insert</span><span class="sxs-lookup"><span data-stu-id="7365f-216">tx_trace_isr_enter_insert</span></span>

#### <a name="insert-isr-enter-event"></a><span data-ttu-id="7365f-217">Inserisci evento di immissione ISR</span><span class="sxs-lookup"><span data-stu-id="7365f-217">Insert ISR enter event</span></span>

#### <a name="prototype"></a><span data-ttu-id="7365f-218">Prototipo</span><span class="sxs-lookup"><span data-stu-id="7365f-218">Prototype</span></span>

```c
VOID tx_trace_isr_enter_insert (ULONG isr_id);
```

#### <a name="description"></a><span data-ttu-id="7365f-219">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7365f-219">Description</span></span>

<span data-ttu-id="7365f-220">Questo servizio inserisce l'evento di immissione ISR nel buffer di traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="7365f-220">This service inserts the ISR enter event into the event trace buffer.</span></span> <span data-ttu-id="7365f-221">Deve essere chiamato dall'applicazione all'inizio dell'elaborazione ISR.</span><span class="sxs-lookup"><span data-stu-id="7365f-221">It should be called by the application at the beginning of ISR processing.</span></span> <span data-ttu-id="7365f-222">Il parametro fornito deve identificare l'ISR specifico per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7365f-222">The supplied parameter should identify the specific ISR to the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7365f-223">La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="7365f-223">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="7365f-224">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="7365f-224">Input Parameters</span></span> 
- <span data-ttu-id="7365f-225">**isr_id**: valore specifico dell'applicazione per identificare l'ISR.</span><span class="sxs-lookup"><span data-stu-id="7365f-225">**isr_id**: Application specific value to identify the ISR.</span></span>

#### <a name="return-values"></a><span data-ttu-id="7365f-226">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="7365f-226">Return Values</span></span>

<span data-ttu-id="7365f-227">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="7365f-227">**None**</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="7365f-228">Consentito da</span><span class="sxs-lookup"><span data-stu-id="7365f-228">Allowed From</span></span> 

<span data-ttu-id="7365f-229">ISRs</span><span class="sxs-lookup"><span data-stu-id="7365f-229">ISRs</span></span>

#### <a name="example"></a><span data-ttu-id="7365f-230">Esempio</span><span class="sxs-lookup"><span data-stu-id="7365f-230">Example</span></span>

```c
/* Insert trace event to identify the application's ISR with an ID of 3. */

status = tx_trace_isr_enter_insert (3);

/* If status is TX_SUCCESS the ISR entry event was inserted. */
```

#### <a name="see-also"></a><span data-ttu-id="7365f-231">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7365f-231">See Also</span></span>

<span data-ttu-id="7365f-232">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="7365f-232">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_isr_exit_insert"></a><span data-ttu-id="7365f-233">tx_trace_isr_exit_insert</span><span class="sxs-lookup"><span data-stu-id="7365f-233">tx_trace_isr_exit_insert</span></span>

#### <a name="insert-isr-exit-event"></a><span data-ttu-id="7365f-234">Inserisci evento di uscita ISR</span><span class="sxs-lookup"><span data-stu-id="7365f-234">Insert ISR exit event</span></span>

#### <a name="prototype"></a><span data-ttu-id="7365f-235">Prototipo</span><span class="sxs-lookup"><span data-stu-id="7365f-235">Prototype</span></span>

```c
VOID tx_trace_isr_exit_insert (ULONG isr_id);
```

#### <a name="description"></a><span data-ttu-id="7365f-236">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7365f-236">Description</span></span>

<span data-ttu-id="7365f-237">Questo servizio inserisce l'evento di immissione ISR nel buffer di traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="7365f-237">This service inserts the ISR entry event into the event trace buffer.</span></span> <span data-ttu-id="7365f-238">Deve essere chiamato dall'applicazione all'inizio dell'elaborazione ISR.</span><span class="sxs-lookup"><span data-stu-id="7365f-238">It should be called by the application at the beginning of ISR processing.</span></span> <span data-ttu-id="7365f-239">Il parametro fornito dovrebbe identificare l'ISR per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7365f-239">The supplied parameter should identify the ISR to the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7365f-240">La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="7365f-240">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="7365f-241">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="7365f-241">Input Parameters</span></span> 

- <span data-ttu-id="7365f-242">**isr_id**: valore specifico dell'applicazione per identificare l'ISR.</span><span class="sxs-lookup"><span data-stu-id="7365f-242">**isr_id**: Application specific value to identify the ISR.</span></span>

#### <a name="return-values"></a><span data-ttu-id="7365f-243">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="7365f-243">Return Values</span></span>

<span data-ttu-id="7365f-244">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="7365f-244">**None**</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="7365f-245">Consentito da</span><span class="sxs-lookup"><span data-stu-id="7365f-245">Allowed From</span></span>

<span data-ttu-id="7365f-246">ISRs</span><span class="sxs-lookup"><span data-stu-id="7365f-246">ISRs</span></span>

#### <a name="example"></a><span data-ttu-id="7365f-247">Esempio</span><span class="sxs-lookup"><span data-stu-id="7365f-247">Example</span></span>

```c
/* Insert trace event to identify the application's ISR with an ID of 3. */ 

status = tx_trace_isr_exit_insert (3);

/* If status is TX_SUCCESS the ISR exit event was inserted. */
```

#### <a name="see-also"></a><span data-ttu-id="7365f-248">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7365f-248">See Also</span></span>

<span data-ttu-id="7365f-249">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="7365f-249">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_buffer_full_notify, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_buffer_full_notify"></a><span data-ttu-id="7365f-250">tx_trace_buffer_full_notify</span><span class="sxs-lookup"><span data-stu-id="7365f-250">tx_trace_buffer_full_notify</span></span>

#### <a name="register-trace-buffer-full-application-callback"></a><span data-ttu-id="7365f-251">Registra callback dell'applicazione completo del buffer di traccia</span><span class="sxs-lookup"><span data-stu-id="7365f-251">Register trace buffer full application callback</span></span>

#### <a name="prototype"></a><span data-ttu-id="7365f-252">Prototipo</span><span class="sxs-lookup"><span data-stu-id="7365f-252">Prototype</span></span>

```c
VOID tx_trace_buffer_full_notify (VOID (*full_buffer_callback)(VOID *));
```

#### <a name="description"></a><span data-ttu-id="7365f-253">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7365f-253">Description</span></span>

<span data-ttu-id="7365f-254">Questo servizio registra una funzione di callback dell'applicazione che viene chiamata da ThreadX quando il buffer di traccia diventa pieno.</span><span class="sxs-lookup"><span data-stu-id="7365f-254">This service registers an application callback function that is called by ThreadX when the trace buffer becomes full.</span></span> <span data-ttu-id="7365f-255">L'applicazione può quindi scegliere di disabilitare la traccia e/o possibilmente di configurare un nuovo buffer di traccia.</span><span class="sxs-lookup"><span data-stu-id="7365f-255">The application can then choose to disable tracing and/or possibly setup a new trace buffer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7365f-256">La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="7365f-256">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="7365f-257">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="7365f-257">Input Parameters</span></span>

- <span data-ttu-id="7365f-258">**full_buffer_callback**: funzione dell'applicazione da chiamare quando il buffer di traccia è pieno.</span><span class="sxs-lookup"><span data-stu-id="7365f-258">**full_buffer_callback**: Application function to call when the trace buffer is full.</span></span> <span data-ttu-id="7365f-259">Il valore NULL disabilita il callback di notifica.</span><span class="sxs-lookup"><span data-stu-id="7365f-259">A value of NULL disables the notification callback.</span></span>

#### <a name="return-values"></a><span data-ttu-id="7365f-260">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="7365f-260">Return Values</span></span>

<span data-ttu-id="7365f-261">**Nessuno**</span><span class="sxs-lookup"><span data-stu-id="7365f-261">**None**</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="7365f-262">Consentito da</span><span class="sxs-lookup"><span data-stu-id="7365f-262">Allowed From</span></span>

<span data-ttu-id="7365f-263">ISRs</span><span class="sxs-lookup"><span data-stu-id="7365f-263">ISRs</span></span>

#### <a name="example"></a><span data-ttu-id="7365f-264">Esempio</span><span class="sxs-lookup"><span data-stu-id="7365f-264">Example</span></span>

```c
y_trace_is_full(void *trace_buffer_start)

{

     /* Application specific processing goes here! */

}

/* Register the "my_trace_is_full" function to be called whenever the trace buffer fills. */

status = tx_trace_buffer_full_notify (my_trace_is_full);

/* If status is TX_SUCCESS the "my_trace_is_full" function is registered. */
```

#### <a name="see-also"></a><span data-ttu-id="7365f-265">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7365f-265">See Also</span></span>

<span data-ttu-id="7365f-266">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="7365f-266">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_user_event_insert</span></span>

### <a name="tx_trace_user_event_insert"></a><span data-ttu-id="7365f-267">tx_trace_user_event_insert</span><span class="sxs-lookup"><span data-stu-id="7365f-267">tx_trace_user_event_insert</span></span>

#### <a name="insert-user-event"></a><span data-ttu-id="7365f-268">Inserisci evento utente</span><span class="sxs-lookup"><span data-stu-id="7365f-268">Insert user event</span></span>

#### <a name="prototype"></a><span data-ttu-id="7365f-269">Prototipo</span><span class="sxs-lookup"><span data-stu-id="7365f-269">Prototype</span></span>

```c
UINT tx_trace_user_event_insert (ULONG event_id, 
   ULONG info_field_1, ULONG info_field_2,
   ULONG info_field_3, ULONG info_field_4);
```

#### <a name="description"></a><span data-ttu-id="7365f-270">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7365f-270">Description</span></span>

<span data-ttu-id="7365f-271">Questo servizio inserisce l'evento utente nel buffer di traccia.</span><span class="sxs-lookup"><span data-stu-id="7365f-271">This service inserts the user event into the trace buffer.</span></span> <span data-ttu-id="7365f-272">Gli ID evento utente devono essere maggiori della costante **TX_TRACE_USER_EVENT_START**, che è definita come 4096.</span><span class="sxs-lookup"><span data-stu-id="7365f-272">User event IDs must be greater than the constant **TX_TRACE_USER_EVENT_START**, which is defined to be 4096.</span></span> <span data-ttu-id="7365f-273">Il numero massimo di eventi utente è definito dalla costante **TX_TRACE_USER_EVENT_END**, che è definita come 65535.</span><span class="sxs-lookup"><span data-stu-id="7365f-273">The maximum user event is defined by the constant **TX_TRACE_USER_EVENT_END**, which is defined to be 65535.</span></span> <span data-ttu-id="7365f-274">Tutti gli eventi all'interno di questo intervallo sono disponibili per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7365f-274">All events within this range are available to the application.</span></span> <span data-ttu-id="7365f-275">I campi delle informazioni sono specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7365f-275">The information fields are application specific.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7365f-276">La libreria ThreadX e l'applicazione devono essere compilate con **TX_ENABLE_EVENT_TRACE** definito per poter usare la traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="7365f-276">The ThreadX library and application must be built with **TX_ENABLE_EVENT_TRACE** defined in order to use event tracing.</span></span>

#### <a name="input-parameters"></a><span data-ttu-id="7365f-277">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="7365f-277">Input Parameters</span></span>

- <span data-ttu-id="7365f-278">**event_id**: l'identificazione dell'evento specifico dell'applicazione e deve iniziare essere maggiore di **TX_TRACE_USER_EVENT_START** e minore o uguale a **TX_TRACE_USER_EVENT_END**.</span><span class="sxs-lookup"><span data-stu-id="7365f-278">**event_id**: Application-specific event identification and must start be greater than **TX_TRACE_USER_EVENT_START** and less than or equal to **TX_TRACE_USER_EVENT_END**.</span></span>
- <span data-ttu-id="7365f-279">**info_field_1**: campo delle informazioni specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7365f-279">**info_field_1**: Application-specific information field.</span></span>
- <span data-ttu-id="7365f-280">**info_field_2**: campo delle informazioni specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7365f-280">**info_field_2**: Application-specific information field.</span></span>
- <span data-ttu-id="7365f-281">**info_field_3**: campo delle informazioni specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7365f-281">**info_field_3**: Application-specific information field.</span></span>
- <span data-ttu-id="7365f-282">**info_field_4**: campo delle informazioni specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7365f-282">**info_field_4**: Application-specific information field.</span></span>

#### <a name="return-values"></a><span data-ttu-id="7365f-283">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="7365f-283">Return Values</span></span>
- <span data-ttu-id="7365f-284">**TX_SUCCESS** (0x00) inserimento evento utente riuscito.</span><span class="sxs-lookup"><span data-stu-id="7365f-284">**TX_SUCCESS** (0x00) Successful user event insert.</span></span>
- <span data-ttu-id="7365f-285">La traccia eventi **TX_NOT_DONE** (0x20) non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="7365f-285">**TX_NOT_DONE** (0x20) Event tracing is not enabled.</span></span>
- <span data-ttu-id="7365f-286">**TX_FEATURE_NOT_ENABLED** (0Xff) il sistema non è stato compilato con la traccia abilitata.</span><span class="sxs-lookup"><span data-stu-id="7365f-286">**TX_FEATURE_NOT_ENABLED** (0xFF) The system was not compiled with trace enabled.</span></span>

#### <a name="allowed-from"></a><span data-ttu-id="7365f-287">Consentito da</span><span class="sxs-lookup"><span data-stu-id="7365f-287">Allowed From</span></span>

<span data-ttu-id="7365f-288">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="7365f-288">Initialization and threads</span></span>

#### <a name="example"></a><span data-ttu-id="7365f-289">Esempio</span><span class="sxs-lookup"><span data-stu-id="7365f-289">Example</span></span>

```c
/* Insert user event 3000, with info fields of 1, 2, 3, 4. */ 

status = tx_trace_user_event_insert (3000, 1, 2, 3, 4);

/* If status is TX_SUCCESS the user event was inserted. */
```

#### <a name="see-also"></a><span data-ttu-id="7365f-290">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7365f-290">See Also</span></span>

<span data-ttu-id="7365f-291">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify</span><span class="sxs-lookup"><span data-stu-id="7365f-291">tx_trace_enable, tx_trace_event_filter, tx_trace_event_unfilter, tx_trace_disable, tx_trace_isr_enter_insert, tx_trace_isr_exit_insert, tx_trace_buffer_full_notify</span></span>