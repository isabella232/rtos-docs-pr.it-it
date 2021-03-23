---
title: Capitolo 11-formato del buffer di traccia eventi
description: ThreadX fornisce il supporto predefinito per la traccia degli eventi per tutti i servizi ThreadX di Azure RTO, le modifiche dello stato dei thread e gli eventi definiti dall'utente.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: d11b827558e9c96df44f462329b7807a500a64a4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823480"
---
# <a name="chapter-11---format-of-event-trace-buffer"></a><span data-ttu-id="f89b3-103">Capitolo 11-formato del buffer di traccia eventi</span><span class="sxs-lookup"><span data-stu-id="f89b3-103">Chapter 11 - Format of event trace buffer</span></span>

<span data-ttu-id="f89b3-104">Azure RTO ThreadX offre supporto predefinito per la traccia degli eventi per tutti i servizi ThreadX, le modifiche allo stato del thread e gli eventi definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="f89b3-104">Azure RTOS ThreadX provides built-in event trace support for all ThreadX services, thread state changes, and user-defined events.</span></span> <span data-ttu-id="f89b3-105">Per usare la traccia eventi, è sufficiente compilare le librerie ThreadX, NetX e FileX con **TX_ENABLE_EVENT_TRACE** definite e abilitare la traccia chiamando la funzione **_tx_trace_enable_** .</span><span class="sxs-lookup"><span data-stu-id="f89b3-105">To use event trace, simply build the ThreadX, NetX, and FileX libraries with **TX_ENABLE_EVENT_TRACE** defined and enable tracing by calling the **_tx_trace_enable_** function.</span></span> <span data-ttu-id="f89b3-106">In questo capitolo viene descritto il processo.</span><span class="sxs-lookup"><span data-stu-id="f89b3-106">This chapter describes that process.</span></span>

## <a name="event-trace-format"></a><span data-ttu-id="f89b3-107">Formato traccia eventi</span><span class="sxs-lookup"><span data-stu-id="f89b3-107">Event Trace Format</span></span>

<span data-ttu-id="f89b3-108">Il formato del buffer di traccia dell'evento ThreadX è suddiviso in tre sezioni, ovvero l'intestazione del controllo, il registro oggetti e le voci di traccia.</span><span class="sxs-lookup"><span data-stu-id="f89b3-108">The format of the ThreadX event trace buffer is divided into three sections, namely the control header, object registry, and the trace entries.</span></span> <span data-ttu-id="f89b3-109">Di seguito viene descritto il layout generale del buffer di traccia dell'evento ThreadX:</span><span class="sxs-lookup"><span data-stu-id="f89b3-109">The following describes the general layout of the ThreadX event trace buffer:</span></span>

<span data-ttu-id="f89b3-110">**Intestazione del controllo**</span><span class="sxs-lookup"><span data-stu-id="f89b3-110">**Control Header**</span></span>

<span data-ttu-id="f89b3-111">**Voce del registro di sistema dell'oggetto 0**</span><span class="sxs-lookup"><span data-stu-id="f89b3-111">**Object Registry Entry 0**</span></span>

<span data-ttu-id="f89b3-112">**…**</span><span class="sxs-lookup"><span data-stu-id="f89b3-112">**…**</span></span>

<span data-ttu-id="f89b3-113">**Voce del registro oggetti "n"**</span><span class="sxs-lookup"><span data-stu-id="f89b3-113">**Object Register Entry "n"**</span></span>

<span data-ttu-id="f89b3-114">**Immissione traccia eventi 0**</span><span class="sxs-lookup"><span data-stu-id="f89b3-114">**Event Trace Entry 0**</span></span>

<span data-ttu-id="f89b3-115">**…**</span><span class="sxs-lookup"><span data-stu-id="f89b3-115">**…**</span></span>

<span data-ttu-id="f89b3-116">**Voce di traccia eventi "n"**</span><span class="sxs-lookup"><span data-stu-id="f89b3-116">**Event Trace Entry "n"**</span></span>

### <a name="event-trace-control-header"></a><span data-ttu-id="f89b3-117">Intestazione controllo traccia eventi</span><span class="sxs-lookup"><span data-stu-id="f89b3-117">Event Trace Control Header</span></span>

<span data-ttu-id="f89b3-118">L'intestazione del controllo definisce il layout esatto del buffer di traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="f89b3-118">The control header defines the exact layout of the event trace buffer.</span></span> <span data-ttu-id="f89b3-119">Ciò include il numero di oggetti ThreadX che è possibile registrare e il numero di eventi che possono essere registrati.</span><span class="sxs-lookup"><span data-stu-id="f89b3-119">This includes how many ThreadX objects can be registered as well as how many events can be recorded.</span></span> <span data-ttu-id="f89b3-120">Inoltre, l'intestazione del controllo definisce la posizione in cui si trovano tutti gli elementi del buffer di traccia.</span><span class="sxs-lookup"><span data-stu-id="f89b3-120">In addition, the control header defines where each of the elements of the trace buffer resides.</span></span> <span data-ttu-id="f89b3-121">La struttura dei dati seguente definisce l'intestazione del controllo:</span><span class="sxs-lookup"><span data-stu-id="f89b3-121">The following data structure defines the control header:</span></span>

```c
typedef struct TX_TRACE_CONTROL_HEADER_STRUCT
{
    ULONG    tx_trace_control_header_id;
    ULONG    tx_trace_control_header_timer_valid_mask;
    ULONG    tx_trace_control_header_trace_base_address;
    ULONG    tx_trace_control_header_object_registry_start_pointer;
    USHORT   tx_trace_control_header_reserved1;
    USHORT   tx_trace_control_header_object_registry_name_size;
    ULONG    tx_trace_control_header_object_registry_end_pointer;
    ULONG    tx_trace_control_header_buffer_start_pointer;
    ULONG    tx_trace_control_header_buffer_end_pointer;
    ULONG    tx_trace_control_header_buffer_current_pointer;
    ULONG    tx_trace_control_header_reserved2;
    ULONG    tx_trace_control_header_reserved3;
    ULONG    tx_trace_control_header_reserved4;
} TX_TRACE_CONTROL_HEADER;
```

### <a name="control-header-id"></a><span data-ttu-id="f89b3-122">ID intestazione del controllo</span><span class="sxs-lookup"><span data-stu-id="f89b3-122">Control Header ID</span></span>

<span data-ttu-id="f89b3-123">L'ID dell'intestazione del controllo è costituito dal valore ESADECIMALe a 32 bit di 0x54585442, che corrisponde ai caratteri ASCII ***TXTB***.</span><span class="sxs-lookup"><span data-stu-id="f89b3-123">The control header ID consists of the 32-bit HEX value of 0x54585442, which corresponds to the ASCII characters ***TXTB***.</span></span> <span data-ttu-id="f89b3-124">Poiché questo valore viene scritto come variabile senza segno a 32 bit, può essere utilizzato anche per rilevare l'oggetto dell'oggetto buffer di traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="f89b3-124">Since this value is written as a 32-bit unsigned variable, it can also be used to detect the endianness of the event trace buffer.</span></span> <span data-ttu-id="f89b3-125">Se, ad esempio, il valore nei primi quattro addii di memoria è 0x54, 0x58, 0x54, 0x42, il buffer di traccia eventi è stato scritto in formato big endian.</span><span class="sxs-lookup"><span data-stu-id="f89b3-125">For example, if the value in the first four byes of memory is 0x54, 0x58, 0x54, 0x42, the event trace buffer was written in big endian format.</span></span> <span data-ttu-id="f89b3-126">In caso contrario, il buffer di traccia eventi è stato scritto in formato little endian.</span><span class="sxs-lookup"><span data-stu-id="f89b3-126">Otherwise, the event trace buffer was written in little endian format.</span></span>

### <a name="timer-valid-mask"></a><span data-ttu-id="f89b3-127">Maschera del timer valida</span><span class="sxs-lookup"><span data-stu-id="f89b3-127">Timer Valid Mask</span></span>

<span data-ttu-id="f89b3-128">La maschera timer valida definisce il numero di bit del timestamp nelle voci della traccia eventi effettivi validi.</span><span class="sxs-lookup"><span data-stu-id="f89b3-128">The timer valid mask defines how many bits of the timestamp in the actual event trace entries are valid.</span></span> <span data-ttu-id="f89b3-129">Se, ad esempio, l'origine timestamp dispone di 16 bit, il valore in questo campo dovrebbe essere 0xFFFF.</span><span class="sxs-lookup"><span data-stu-id="f89b3-129">For example, if the time-stamp source has 16-bits, the value in this field should be 0xFFFF.</span></span> <span data-ttu-id="f89b3-130">Un'origine timestamp a 32 bit avrà un valore 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="f89b3-130">A 32-bit time-stamp source would have a value of 0xFFFFFFFF.</span></span> <span data-ttu-id="f89b3-131">Questo valore è definito dalla costante \***TX_TRACE_TIME_MASK** _ in _ *_tx_port. h_* \*.</span><span class="sxs-lookup"><span data-stu-id="f89b3-131">This value is defined by the ***TX_TRACE_TIME_MASK** _ constant in _*_tx_port.h_\*\*.</span></span>

### <a name="trace-base-address"></a><span data-ttu-id="f89b3-132">Indirizzo di base della traccia</span><span class="sxs-lookup"><span data-stu-id="f89b3-132">Trace Base Address</span></span>

<span data-ttu-id="f89b3-133">L'indirizzo di base del buffer di traccia è l'indirizzo specificato dall'applicazione come inizio del buffer di traccia nella chiamata ***tx_trace_enable*** .</span><span class="sxs-lookup"><span data-stu-id="f89b3-133">The trace buffer base address is the address the application specified as the start of the trace buffer in the ***tx_trace_enable*** call.</span></span> <span data-ttu-id="f89b3-134">Questo indirizzo viene mantenuto per l'utilizzo esclusivo dello strumento di analisi per derivare gli offset bufferrelative per i vari elementi nel buffer.</span><span class="sxs-lookup"><span data-stu-id="f89b3-134">This address is maintained for the sole use of the analysis tool to derive bufferrelative offsets for the various elements in the buffer.</span></span> <span data-ttu-id="f89b3-135">Ad esempio, l'offset relativo del buffer dell'evento corrente nel buffer di traccia viene calcolato dalla semplice sottrazione dell'indirizzo di base dall'indirizzo dell'evento corrente.</span><span class="sxs-lookup"><span data-stu-id="f89b3-135">For example, the buffer relative offset of the current event in the trace buffer is calculated by simple subtraction of the base address from the current event address.</span></span>

### <a name="registry-start-and-end-pointers"></a><span data-ttu-id="f89b3-136">Puntatori di inizio e fine del registro di sistema</span><span class="sxs-lookup"><span data-stu-id="f89b3-136">Registry Start and End Pointers</span></span>

<span data-ttu-id="f89b3-137">Il puntatore di avvio del registro di sistema punta all'indirizzo della prima voce del registro di sistema dell'oggetto, mentre il puntatore di fine del registro di sistema punta all'indirizzo im. /mediately dopo l'ultima voce di registro.</span><span class="sxs-lookup"><span data-stu-id="f89b3-137">The registry start pointer points to the address of the first object registry entry, while the registry end pointer points to the address im../mediately following the last register entry.</span></span> <span data-ttu-id="f89b3-138">Questi valori vengono impostati durante l'elaborazione del *tx_trace_enable* e non vengono modificati durante la durata della traccia.</span><span class="sxs-lookup"><span data-stu-id="f89b3-138">These values are setup during the *tx_trace_enable* processing and are not changed throughout the duration of tracing.</span></span>

### <a name="registry-name-size"></a><span data-ttu-id="f89b3-139">Dimensioni Nome registro</span><span class="sxs-lookup"><span data-stu-id="f89b3-139">Registry Name Size</span></span>

<span data-ttu-id="f89b3-140">Le dimensioni del nome del registro di sistema definiscono le dimensioni massime in byte per ogni nome di oggetto nella voce del registro di sistema ed è definito dal simbolo \***TX_TRACE_OBJECT_REGISTRY_NAME** _.</span><span class="sxs-lookup"><span data-stu-id="f89b3-140">The registry name size defines maximum size in bytes for each object name in the registry entry and is defined by the symbol \***TX_TRACE_OBJECT_REGISTRY_NAME** _.</span></span> <span data-ttu-id="f89b3-141">Il valore predefinito è 32 ed è definito in _*_tx_trace. h_*_.</span><span class="sxs-lookup"><span data-stu-id="f89b3-141">The default value is 32 and is defined in _*_tx_trace.h_*_.</span></span> <span data-ttu-id="f89b3-142">Il nome dell'oggetto corrisponde al nome assegnato dall'applicazione al momento della creazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="f89b3-142">The object name corresponds to the name given by the application when the object was created.</span></span> <span data-ttu-id="f89b3-143">Ad esempio, il nome del registro di sistema dell'oggetto per un thread è il nome fornito dall'applicazione alla chiamata _ *_tx_thread_create_* \*.</span><span class="sxs-lookup"><span data-stu-id="f89b3-143">For example, the object registry name for a thread is the name supplied by the application to the _\*_tx_thread_create_\*\*call.</span></span>

### <a name="buffer-start-and-end-pointers"></a><span data-ttu-id="f89b3-144">Puntatori di inizio e fine del buffer</span><span class="sxs-lookup"><span data-stu-id="f89b3-144">Buffer Start and End Pointers</span></span>

<span data-ttu-id="f89b3-145">Il puntatore di avvio del buffer di traccia eventi punta all'indirizzo della prima voce di traccia, mentre il puntatore finale del registro di sistema punta all'indirizzo im. /mediately che segue l'ultima voce di traccia.</span><span class="sxs-lookup"><span data-stu-id="f89b3-145">The event trace buffer start pointer points to the address of the first trace entry, while the registry end pointer points to the address im../mediately following the last trace entry.</span></span> <span data-ttu-id="f89b3-146">Questi valori vengono impostati durante l' ***tx_trace_enable</*** elaborazione e non vengono modificati durante la durata della traccia.</span><span class="sxs-lookup"><span data-stu-id="f89b3-146">These values are setup during the ***tx_trace_enable</*** processing and are not changed throughout the duration of tracing.</span></span>

### <a name="current-buffer-pointer"></a><span data-ttu-id="f89b3-147">Puntatore al buffer corrente</span><span class="sxs-lookup"><span data-stu-id="f89b3-147">Current Buffer Pointer</span></span>

<span data-ttu-id="f89b3-148">Il puntatore corrente del buffer di traccia eventi punta all'indirizzo della voce di traccia meno recente.</span><span class="sxs-lookup"><span data-stu-id="f89b3-148">The event trace buffer current pointer points to the address of the oldest trace entry.</span></span> <span data-ttu-id="f89b3-149">Poiché le voci di traccia vengono mantenute in un elenco circolare, il puntatore al buffer corrente rappresenta anche la voce di traccia successiva da scrivere.</span><span class="sxs-lookup"><span data-stu-id="f89b3-149">Since the trace entries are maintained in a circular list, the current buffer pointer is also represents the next trace entry to be written.</span></span> |

## <a name="event-trace-object-registry"></a><span data-ttu-id="f89b3-150">Registro oggetti traccia eventi</span><span class="sxs-lookup"><span data-stu-id="f89b3-150">Event Trace Object Registry</span></span>

<span data-ttu-id="f89b3-151">Il registro degli oggetti di traccia eventi contiene le voci del registro di sistema dell'oggetto \***n** che corrispondono agli oggetti creati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f89b3-151">The event trace object registry contains \***n** _ object registry entries that correspond to the objects created by the application.</span></span> <span data-ttu-id="f89b3-152">Lo scopo principale del registro oggetti è per gli strumenti di analisi esterna correlare i nomi di oggetto effettivi con gli indirizzi degli oggetti delle voci del buffer di traccia.</span><span class="sxs-lookup"><span data-stu-id="f89b3-152">The main purpose of the object registry is for external analysis tools to correlate actual object names with the object addresses of the trace buffer entries.</span></span> <span data-ttu-id="f89b3-153">Il numero di voci del registro di sistema viene specificato dall'applicazione nella chiamata _ \*_tx_trace_enable_\*\*.</span><span class="sxs-lookup"><span data-stu-id="f89b3-153">The number of registry entries is specified by the application in the _ *_tx_trace_enable_*\* call.</span></span>

<span data-ttu-id="f89b3-154">Ogni voce del registro oggetti contiene informazioni su un oggetto ThreadX specifico creato in precedenza dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f89b3-154">Each object register entry contains information about a specific ThreadX object previously created by the application.</span></span> <span data-ttu-id="f89b3-155">La struttura dei dati seguente definisce la voce del registro di sistema di ogni oggetto:</span><span class="sxs-lookup"><span data-stu-id="f89b3-155">The following data structure defines each object registry entry:</span></span>

```c
typedef struct TX_TRACE_OBJECT_REGISTRY_ENTRY_STRUCT
{
    UCHAR    tx_trace_object_registry_entry_object_available**;
    UCHAR    tx_trace_object_registry_entry_object_type**;
    UCHAR    tx_trace_object_registry_entry_object_reserved1;
    UCHAR    tx_trace_object_registry_entry_object_reserved2;
    ULONG    tx_trace_thread_registry_entry_object_pointer;
    ULONG    tx_trace_object_registry_entry_object_parameter_1;
    ULONG    tx_trace_object_registry_entry_object_parameter_2;
    UCHAR    tx_trace_thread_registry_entry_object_name[TX_TRACE_OBJECT_REGISTRY_NAME];

} TX_TRACE_OBJECT_REGISTRY_ENTRY;
```

### <a name="object-available-flag"></a><span data-ttu-id="f89b3-156">Flag oggetto disponibile</span><span class="sxs-lookup"><span data-stu-id="f89b3-156">Object Available Flag</span></span>

<span data-ttu-id="f89b3-157">Il flag oggetto disponibile viene impostato su 1 se è disponibile la voce del registro di sistema dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="f89b3-157">The object available flag is set to 1 if the object registry entry is available.</span></span> <span data-ttu-id="f89b3-158">In caso contrario, se il valore non è 1, la voce del registro di sistema dell'oggetto non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="f89b3-158">Otherwise, if the value is not 1, the object registry entry is not available.</span></span> <span data-ttu-id="f89b3-159">Si noti che la voce potrebbe ancora contenere informazioni valide anche se disponibile.</span><span class="sxs-lookup"><span data-stu-id="f89b3-159">Note that the entry could still contain valid information even though it is available.</span></span>

### <a name="object-entry-type"></a><span data-ttu-id="f89b3-160">Tipo voce oggetto</span><span class="sxs-lookup"><span data-stu-id="f89b3-160">Object Entry Type</span></span>

<span data-ttu-id="f89b3-161">Il tipo di voce dell'oggetto identifica il tipo di oggetto in questa voce.</span><span class="sxs-lookup"><span data-stu-id="f89b3-161">The object entry type identifies the type of object in this entry.</span></span> <span data-ttu-id="f89b3-162">Di seguito è riportato un elenco dei tipi di oggetto validi:</span><span class="sxs-lookup"><span data-stu-id="f89b3-162">The following is a list of the valid object types:</span></span>

| <span data-ttu-id="f89b3-163">**Valore**</span><span class="sxs-lookup"><span data-stu-id="f89b3-163">**Value**</span></span> | <span data-ttu-id="f89b3-164">**Tipo oggetto**</span><span class="sxs-lookup"><span data-stu-id="f89b3-164">**Object Type**</span></span> |
|---------- | --------------- |
| <span data-ttu-id="f89b3-165">0</span><span class="sxs-lookup"><span data-stu-id="f89b3-165">0</span></span>         | <span data-ttu-id="f89b3-166">Non valido</span><span class="sxs-lookup"><span data-stu-id="f89b3-166">Not Valid</span></span>       |
| <span data-ttu-id="f89b3-167">1</span><span class="sxs-lookup"><span data-stu-id="f89b3-167">1</span></span>         | <span data-ttu-id="f89b3-168">Thread</span><span class="sxs-lookup"><span data-stu-id="f89b3-168">Thread</span></span>          |
| <span data-ttu-id="f89b3-169">2</span><span class="sxs-lookup"><span data-stu-id="f89b3-169">2</span></span>         | <span data-ttu-id="f89b3-170">Timer</span><span class="sxs-lookup"><span data-stu-id="f89b3-170">Timer</span></span> |
| <span data-ttu-id="f89b3-171">3</span><span class="sxs-lookup"><span data-stu-id="f89b3-171">3</span></span>         | <span data-ttu-id="f89b3-172">Coda</span><span class="sxs-lookup"><span data-stu-id="f89b3-172">Queue</span></span> |
| <span data-ttu-id="f89b3-173">4</span><span class="sxs-lookup"><span data-stu-id="f89b3-173">4</span></span>         | <span data-ttu-id="f89b3-174">Semaphore</span><span class="sxs-lookup"><span data-stu-id="f89b3-174">Semaphore</span></span> |
| <span data-ttu-id="f89b3-175">5</span><span class="sxs-lookup"><span data-stu-id="f89b3-175">5</span></span>         | <span data-ttu-id="f89b3-176">Mutex</span><span class="sxs-lookup"><span data-stu-id="f89b3-176">Mutex</span></span> |
| <span data-ttu-id="f89b3-177">6</span><span class="sxs-lookup"><span data-stu-id="f89b3-177">6</span></span>         | <span data-ttu-id="f89b3-178">Gruppo flag di evento</span><span class="sxs-lookup"><span data-stu-id="f89b3-178">Event Flags Group</span></span> |
| <span data-ttu-id="f89b3-179">7</span><span class="sxs-lookup"><span data-stu-id="f89b3-179">7</span></span>         | <span data-ttu-id="f89b3-180">Blocca pool</span><span class="sxs-lookup"><span data-stu-id="f89b3-180">Block Pool</span></span> |
| <span data-ttu-id="f89b3-181">8</span><span class="sxs-lookup"><span data-stu-id="f89b3-181">8</span></span>         | <span data-ttu-id="f89b3-182">Pool di byte</span><span class="sxs-lookup"><span data-stu-id="f89b3-182">Byte Pool</span></span> |
| <span data-ttu-id="f89b3-183">9</span><span class="sxs-lookup"><span data-stu-id="f89b3-183">9</span></span>         | <span data-ttu-id="f89b3-184">.. /media</span><span class="sxs-lookup"><span data-stu-id="f89b3-184">../media</span></span> |
| <span data-ttu-id="f89b3-185">10</span><span class="sxs-lookup"><span data-stu-id="f89b3-185">10</span></span>        | <span data-ttu-id="f89b3-186">File</span><span class="sxs-lookup"><span data-stu-id="f89b3-186">File</span></span> |
| <span data-ttu-id="f89b3-187">11</span><span class="sxs-lookup"><span data-stu-id="f89b3-187">11</span></span>        | <span data-ttu-id="f89b3-188">IP</span><span class="sxs-lookup"><span data-stu-id="f89b3-188">IP</span></span> |
| <span data-ttu-id="f89b3-189">12</span><span class="sxs-lookup"><span data-stu-id="f89b3-189">12</span></span>        | <span data-ttu-id="f89b3-190">Pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f89b3-190">Packet Pool</span></span> |
| <span data-ttu-id="f89b3-191">13</span><span class="sxs-lookup"><span data-stu-id="f89b3-191">13</span></span>        | <span data-ttu-id="f89b3-192">Socket TCP</span><span class="sxs-lookup"><span data-stu-id="f89b3-192">TCP Socket</span></span> |
| <span data-ttu-id="f89b3-193">14</span><span class="sxs-lookup"><span data-stu-id="f89b3-193">14</span></span>        | <span data-ttu-id="f89b3-194">Socket UDP</span><span class="sxs-lookup"><span data-stu-id="f89b3-194">UDP Socket</span></span> |
| <span data-ttu-id="f89b3-195">15-20</span><span class="sxs-lookup"><span data-stu-id="f89b3-195">15-20</span></span>     | <span data-ttu-id="f89b3-196">Riservato</span><span class="sxs-lookup"><span data-stu-id="f89b3-196">Reserved</span></span> |  
| <span data-ttu-id="f89b3-197">21</span><span class="sxs-lookup"><span data-stu-id="f89b3-197">21</span></span>        | <span data-ttu-id="f89b3-198">Dispositivo stack host USB</span><span class="sxs-lookup"><span data-stu-id="f89b3-198">USB Host Stack Device</span></span> |
| <span data-ttu-id="f89b3-199">22</span><span class="sxs-lookup"><span data-stu-id="f89b3-199">22</span></span>        | <span data-ttu-id="f89b3-200">Interfaccia stack host USB</span><span class="sxs-lookup"><span data-stu-id="f89b3-200">USB Host Stack Interface</span></span> |
| <span data-ttu-id="f89b3-201">23</span><span class="sxs-lookup"><span data-stu-id="f89b3-201">23</span></span>        | <span data-ttu-id="f89b3-202">Endpoint host USB</span><span class="sxs-lookup"><span data-stu-id="f89b3-202">USB Host Endpoint</span></span> |
| <span data-ttu-id="f89b3-203">24</span><span class="sxs-lookup"><span data-stu-id="f89b3-203">24</span></span>        | <span data-ttu-id="f89b3-204">Classe host USB</span><span class="sxs-lookup"><span data-stu-id="f89b3-204">USB Host Class</span></span> |
| <span data-ttu-id="f89b3-205">25</span><span class="sxs-lookup"><span data-stu-id="f89b3-205">25</span></span>        | <span data-ttu-id="f89b3-206">Dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="f89b3-206">USB Device</span></span> |
| <span data-ttu-id="f89b3-207">26</span><span class="sxs-lookup"><span data-stu-id="f89b3-207">26</span></span>        | <span data-ttu-id="f89b3-208">Interfaccia del dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="f89b3-208">USB Device Interface</span></span> |
| <span data-ttu-id="f89b3-209">27</span><span class="sxs-lookup"><span data-stu-id="f89b3-209">27</span></span>        | <span data-ttu-id="f89b3-210">Endpoint dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="f89b3-210">USB Device Endpoint</span></span> |
| <span data-ttu-id="f89b3-211">28</span><span class="sxs-lookup"><span data-stu-id="f89b3-211">28</span></span>        | <span data-ttu-id="f89b3-212">Classe dispositivo USB</span><span class="sxs-lookup"><span data-stu-id="f89b3-212">USB Device Class</span></span> |

### <a name="object-pointer"></a><span data-ttu-id="f89b3-213">Puntatore all'oggetto</span><span class="sxs-lookup"><span data-stu-id="f89b3-213">Object Pointer</span></span>

<span data-ttu-id="f89b3-214">Il puntatore all'oggetto specifica l'indirizzo dell'oggetto usato per accedere all'oggetto usando l'API ThreadX.</span><span class="sxs-lookup"><span data-stu-id="f89b3-214">The object pointer specifies the object address that is used for accessing the object using the ThreadX API.</span></span>

### <a name="object-reserved-fields"></a><span data-ttu-id="f89b3-215">Campi riservati oggetto</span><span class="sxs-lookup"><span data-stu-id="f89b3-215">Object Reserved Fields</span></span>

<span data-ttu-id="f89b3-216">Per tutti gli oggetti diversi dai thread, questi campi riservati devono essere 0.</span><span class="sxs-lookup"><span data-stu-id="f89b3-216">For all objects other than threads, these reserved fields should be 0.</span></span> <span data-ttu-id="f89b3-217">Per i thread, la priorità del thread nel momento in cui viene immessa nel registro di sistema viene inserita in questi due campi riservati.</span><span class="sxs-lookup"><span data-stu-id="f89b3-217">For threads, the priority of the thread at the time it is entered into the registry is placed in these two reserved fields.</span></span>

### <a name="object-parameters"></a><span data-ttu-id="f89b3-218">Parametri oggetto</span><span class="sxs-lookup"><span data-stu-id="f89b3-218">Object Parameters</span></span>

<span data-ttu-id="f89b3-219">I parametri dell'oggetto contengono informazioni aggiuntive sull'oggetto.</span><span class="sxs-lookup"><span data-stu-id="f89b3-219">The object parameters contain supplemental information about the object.</span></span> <span data-ttu-id="f89b3-220">Di seguito vengono descritte le informazioni aggiuntive per ogni oggetto ThreadX:</span><span class="sxs-lookup"><span data-stu-id="f89b3-220">The following describes the supplemental information for each ThreadX object:</span></span>

| <span data-ttu-id="f89b3-221">**Tipo oggetto**</span><span class="sxs-lookup"><span data-stu-id="f89b3-221">**Object Type**</span></span>        | <span data-ttu-id="f89b3-222">**Parametro 1**</span><span class="sxs-lookup"><span data-stu-id="f89b3-222">**Parameter 1**</span></span>  | <span data-ttu-id="f89b3-223">**Parametro 2**</span><span class="sxs-lookup"><span data-stu-id="f89b3-223">**Parameter 2**</span></span> |
|----------------------- | ---------------- | --------------- |
| <span data-ttu-id="f89b3-224">Thread</span><span class="sxs-lookup"><span data-stu-id="f89b3-224">Thread</span></span>                 | <span data-ttu-id="f89b3-225">Inizio dello stack</span><span class="sxs-lookup"><span data-stu-id="f89b3-225">Stack Start</span></span>      | <span data-ttu-id="f89b3-226">Dimensioni dello stack</span><span class="sxs-lookup"><span data-stu-id="f89b3-226">Stack Size</span></span> |
| <span data-ttu-id="f89b3-227">Timer</span><span class="sxs-lookup"><span data-stu-id="f89b3-227">Timer</span></span>                  | <span data-ttu-id="f89b3-228">Cicli iniziali</span><span class="sxs-lookup"><span data-stu-id="f89b3-228">Initial Ticks</span></span> | <span data-ttu-id="f89b3-229">Ripianificazione di cicli</span><span class="sxs-lookup"><span data-stu-id="f89b3-229">Reschedule Ticks</span></span> |
| <span data-ttu-id="f89b3-230">Coda</span><span class="sxs-lookup"><span data-stu-id="f89b3-230">Queue</span></span>                  | <span data-ttu-id="f89b3-231">Dimensione della coda</span><span class="sxs-lookup"><span data-stu-id="f89b3-231">Queue Size</span></span> | <span data-ttu-id="f89b3-232">Dimensioni del messaggio</span><span class="sxs-lookup"><span data-stu-id="f89b3-232">Message Size</span></span> |
| <span data-ttu-id="f89b3-233">Semaphore</span><span class="sxs-lookup"><span data-stu-id="f89b3-233">Semaphore</span></span>              | <span data-ttu-id="f89b3-234">Istanze iniziali</span><span class="sxs-lookup"><span data-stu-id="f89b3-234">Initial Instances</span></span> | - |
| <span data-ttu-id="f89b3-235">Mutex</span><span class="sxs-lookup"><span data-stu-id="f89b3-235">Mutex</span></span>                  | <span data-ttu-id="f89b3-236">Flag ereditarietà</span><span class="sxs-lookup"><span data-stu-id="f89b3-236">Inheritance Flag</span></span> | - |
| <span data-ttu-id="f89b3-237">Gruppo flag di evento</span><span class="sxs-lookup"><span data-stu-id="f89b3-237">Event Flags Group</span></span>      | - | - |
| <span data-ttu-id="f89b3-238">Blocca pool</span><span class="sxs-lookup"><span data-stu-id="f89b3-238">Block Pool</span></span>             | <span data-ttu-id="f89b3-239">Blocchi totali</span><span class="sxs-lookup"><span data-stu-id="f89b3-239">Total Blocks</span></span> | <span data-ttu-id="f89b3-240">Dimensione blocco</span><span class="sxs-lookup"><span data-stu-id="f89b3-240">Block Size</span></span> |
| <span data-ttu-id="f89b3-241">Pool di byte</span><span class="sxs-lookup"><span data-stu-id="f89b3-241">Byte Pool</span></span>              | <span data-ttu-id="f89b3-242">Total Bytes</span><span class="sxs-lookup"><span data-stu-id="f89b3-242">Total Bytes</span></span> | - |
| <span data-ttu-id="f89b3-243">.. /media</span><span class="sxs-lookup"><span data-stu-id="f89b3-243">../media</span></span>                  | <span data-ttu-id="f89b3-244">Dimensioni cache FAT</span><span class="sxs-lookup"><span data-stu-id="f89b3-244">Fat Cache Size</span></span> | <span data-ttu-id="f89b3-245">Dimensioni della cache del settore</span><span class="sxs-lookup"><span data-stu-id="f89b3-245">Sector Cache Size</span></span> |
| <span data-ttu-id="f89b3-246">File</span><span class="sxs-lookup"><span data-stu-id="f89b3-246">File</span></span>                   | - | - |
| <span data-ttu-id="f89b3-247">IP</span><span class="sxs-lookup"><span data-stu-id="f89b3-247">IP</span></span>                     | <span data-ttu-id="f89b3-248">Inizio dello stack</span><span class="sxs-lookup"><span data-stu-id="f89b3-248">Stack Start</span></span> | <span data-ttu-id="f89b3-249">Dimensioni dello stack</span><span class="sxs-lookup"><span data-stu-id="f89b3-249">Stack Size</span></span> |
| <span data-ttu-id="f89b3-250">Pool di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f89b3-250">Packet Pool</span></span>            | <span data-ttu-id="f89b3-251">Dimensione pacchetti</span><span class="sxs-lookup"><span data-stu-id="f89b3-251">Packet Size</span></span> | <span data-ttu-id="f89b3-252">Numero di pacchetti</span><span class="sxs-lookup"><span data-stu-id="f89b3-252">Number of Packets</span></span> |
| <span data-ttu-id="f89b3-253">Socket TCP</span><span class="sxs-lookup"><span data-stu-id="f89b3-253">TCP Socket</span></span>             | <span data-ttu-id="f89b3-254">Indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="f89b3-254">IP address</span></span> | <span data-ttu-id="f89b3-255">Dimensioni della finestra</span><span class="sxs-lookup"><span data-stu-id="f89b3-255">Window Size</span></span> |
| <span data-ttu-id="f89b3-256">Socket UDP</span><span class="sxs-lookup"><span data-stu-id="f89b3-256">UDP Socket</span></span>             | <span data-ttu-id="f89b3-257">Indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="f89b3-257">IP address</span></span> | <span data-ttu-id="f89b3-258">Massimo coda RX</span><span class="sxs-lookup"><span data-stu-id="f89b3-258">RX Queue Max</span></span> |

### <a name="object-name"></a><span data-ttu-id="f89b3-259">Nome oggetto</span><span class="sxs-lookup"><span data-stu-id="f89b3-259">Object Name</span></span>

<span data-ttu-id="f89b3-260">Il nome dell'oggetto contiene il nome dell'oggetto ThreadX.</span><span class="sxs-lookup"><span data-stu-id="f89b3-260">The object name contains the name of the ThreadX object.</span></span> <span data-ttu-id="f89b3-261">Il nome è il nome fornito a ThreadX al momento della creazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="f89b3-261">The name is the name provided to ThreadX at the time the object was created.</span></span> <span data-ttu-id="f89b3-262">Per impostazione predefinita, il nome dell'oggetto è costituito da un massimo di 32 caratteri.</span><span class="sxs-lookup"><span data-stu-id="f89b3-262">By default, the object name has a maximum of 32 characters.</span></span> <span data-ttu-id="f89b3-263">I nomi effettivi maggiori di 32 caratteri vengono troncati.</span><span class="sxs-lookup"><span data-stu-id="f89b3-263">Actual names greater than 32 characters are truncated.</span></span>

## <a name="event-trace-entries"></a><span data-ttu-id="f89b3-264">Voci di traccia eventi</span><span class="sxs-lookup"><span data-stu-id="f89b3-264">Event Trace Entries</span></span>

<span data-ttu-id="f89b3-265">Le voci della traccia eventi si trovano nella parte inferiore del buffer di traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="f89b3-265">The event trace entries are found in the bottom portion of the event trace buffer.</span></span> <span data-ttu-id="f89b3-266">Le voci vengono mantenute in un elenco circolare, con il puntatore alla voce corrente che punta alla voce meno recente.</span><span class="sxs-lookup"><span data-stu-id="f89b3-266">The entries are maintained in a circular list, with the current entry pointer pointing to the oldest entry.</span></span> <span data-ttu-id="f89b3-267">Il numero di voci nell'elenco viene calcolato dalla chiamata ***tx_trace_enable*** .</span><span class="sxs-lookup"><span data-stu-id="f89b3-267">The number of entries in the list is calculated by the ***tx_trace_enable*** call.</span></span>

<span data-ttu-id="f89b3-268">Ogni voce del registro oggetti contiene informazioni su un evento di traccia ThreadX specifico.</span><span class="sxs-lookup"><span data-stu-id="f89b3-268">Each object register entry contains information about a specific ThreadX trace event.</span></span> <span data-ttu-id="f89b3-269">La struttura dei dati seguente definisce ogni voce dell'evento di traccia:</span><span class="sxs-lookup"><span data-stu-id="f89b3-269">The following data structure defines each trace event entry:</span></span>

```c
typedef struct TX_TRACE_BUFFER_ENTRY_STRUCT
{
    ULONG     tx_trace_buffer_entry_thread_pointer;
    ULONG     tx_trace_buffer_entry_thread_priority;
    ULONG     tx_trace_buffer_entry_event_id;
    ULONG     tx_trace_buffer_entry_time_stamp;
    ULONG     tx_trace_buffer_entry_information_field_1;
    ULONG     tx_trace_buffer_entry_information_field_2;
    ULONG     tx_trace_buffer_entry_information_field_3;
    ULONG     tx_trace_buffer_entry_information_field_4;
} TX_TRACE_BUFFER_ENTRY;
```

### <a name="thread-pointer"></a><span data-ttu-id="f89b3-270">Puntatore thread</span><span class="sxs-lookup"><span data-stu-id="f89b3-270">Thread Pointer</span></span>

<span data-ttu-id="f89b3-271">Il puntatore al thread contiene l'indirizzo del thread in esecuzione al momento dell'evento.</span><span class="sxs-lookup"><span data-stu-id="f89b3-271">The thread pointer contains the address of the thread running at the time of this event.</span></span> <span data-ttu-id="f89b3-272">Se l'evento si è verificato durante l'inizializzazione (nessun thread in esecuzione), il valore di questo puntatore è 0xF0F0F0F0.</span><span class="sxs-lookup"><span data-stu-id="f89b3-272">If the event occurred during initialization (no thread running), the value of this pointer is 0xF0F0F0F0.</span></span> <span data-ttu-id="f89b3-273">Se l'evento si è verificato durante una routine del servizio di interrupt (ISR), il valore di questo puntatore è 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="f89b3-273">If the event occurred during an Interrupt Service Routine (ISR), the value of this pointer is 0xFFFFFFFF.</span></span> <span data-ttu-id="f89b3-274">Se la voce non è ancora stata utilizzata, il valore di questo puntatore è 0.</span><span class="sxs-lookup"><span data-stu-id="f89b3-274">If the entry has not yet been used, the value of this pointer is 0.</span></span>

### <a name="thread-priority"></a><span data-ttu-id="f89b3-275">Priorità thread</span><span class="sxs-lookup"><span data-stu-id="f89b3-275">Thread Priority</span></span>

<span data-ttu-id="f89b3-276">Il campo priorità thread contiene la priorità del thread e la soglia di precedenza del thread che era in esecuzione al momento dell'evento.</span><span class="sxs-lookup"><span data-stu-id="f89b3-276">The thread priority field contains the thread priority and preemption-threshold of the thread that was running at the time of this event.</span></span> <span data-ttu-id="f89b3-277">Se è presente un contesto di interrupt (puntatore al thread è 0xFFFFFFFF), il valore di questo campo non è la priorità, ma il valore di ***_tx_thread_current_ptr*** al momento dell'evento.</span><span class="sxs-lookup"><span data-stu-id="f89b3-277">If an interrupt context is present (thread pointer is 0xFFFFFFFF), the value of this field is not the priority but instead the value of ***_tx_thread_current_ptr*** at the time of the event.</span></span> <span data-ttu-id="f89b3-278">In caso contrario, il valore di questo campo è 0.</span><span class="sxs-lookup"><span data-stu-id="f89b3-278">Otherwise, the value of this field is 0.</span></span>

### <a name="event-id"></a><span data-ttu-id="f89b3-279">ID evento</span><span class="sxs-lookup"><span data-stu-id="f89b3-279">Event ID</span></span>

<span data-ttu-id="f89b3-280">L'ID evento specifica l'evento che ha avuto luogo.</span><span class="sxs-lookup"><span data-stu-id="f89b3-280">The event ID specifies the event that took place.</span></span> <span data-ttu-id="f89b3-281">Gli ID evento di traccia ThreadX validi sono compresi tra 1 e 1024.</span><span class="sxs-lookup"><span data-stu-id="f89b3-281">Valid ThreadX trace event IDs range from 1 through 1024.</span></span> <span data-ttu-id="f89b3-282">I valori a partire da 1025 e versioni successive sono riservati per gli eventi specifici dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f89b3-282">Values starting at 1025 and above are reserved for user-specific events.</span></span> <span data-ttu-id="f89b3-283">Per la definizione completa degli ID evento ThreadX, vedere il file ***tx_trace. h*** .</span><span class="sxs-lookup"><span data-stu-id="f89b3-283">Please refer to the ***tx_trace.h*** file for the complete definition of ThreadX event IDs.</span></span></td>

### <a name="information-fields-1-4"></a><span data-ttu-id="f89b3-284">Campi informazioni (1-4)</span><span class="sxs-lookup"><span data-stu-id="f89b3-284">Information Fields (1-4)</span></span>

<span data-ttu-id="f89b3-285">I campi informativi contengono informazioni aggiuntive sull'evento specifico.</span><span class="sxs-lookup"><span data-stu-id="f89b3-285">The information fields contain additional information about the specific event.</span></span> <span data-ttu-id="f89b3-286">Per una descrizione completa dei campi di informazioni per ogni ID evento ThreadX definito, vedere il file ***tx_trace. h*** .</span><span class="sxs-lookup"><span data-stu-id="f89b3-286">Please refer to the ***tx_trace.h*** file for the complete description of the information fields for each of the defined ThreadX event IDs.</span></span>