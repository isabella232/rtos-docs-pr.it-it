---
title: Capitolo 4-Descrizione dei servizi SMP ThreadX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi SMP di Azure RTO ThreadX in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4432001b773b4ef4f99b1b34193e90863966aad4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823927"
---
# <a name="chapter-4---description-of-azure-rtos-threadx-smp-services"></a><span data-ttu-id="f7939-103">Capitolo 4-Descrizione dei servizi SMP ThreadX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="f7939-103">Chapter 4 - Description of Azure RTOS ThreadX SMP Services</span></span>

<span data-ttu-id="f7939-104">Questo capitolo contiene una descrizione di tutti i servizi SMP di Azure RTO ThreadX in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="f7939-104">This chapter contains a description of all Azure RTOS ThreadX SMP services in alphabetic order.</span></span> <span data-ttu-id="f7939-105">I nomi sono progettati in modo da raggruppare tutti i servizi simili.</span><span class="sxs-lookup"><span data-stu-id="f7939-105">Their names are designed so all similar services are grouped together.</span></span> <span data-ttu-id="f7939-106">Nella sezione "valori restituiti" nelle descrizioni seguenti i valori in **grassetto** non sono interessati dal **TX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API; mentre i valori visualizzati in non grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="f7939-106">In the “Return Values” section in the following descriptions, values in **BOLD** are not affected by the **TX_DISABLE_ERROR_CHECKING** define used to disable API error checking; while values shown in nonbold are completely disabled.</span></span> <span data-ttu-id="f7939-107">Inoltre, una "**Sì**" elencata sotto l'intestazione "**precedenza possibile**" indica che la chiamata al servizio può riprendere un thread con priorità più alta, in modo da precedere il thread chiamante.</span><span class="sxs-lookup"><span data-stu-id="f7939-107">In addition, a “**Yes**” listed under the “**Preemption Possible**” heading indicates that calling the service may resume a higher-priority thread, thus preempting the calling thread.</span></span>

- <span data-ttu-id="f7939-108">**tx_block_allocate**: *allocare un blocco di memoria a dimensione fissa*</span><span class="sxs-lookup"><span data-stu-id="f7939-108">**tx_block_allocate**: *Allocate fixed-size block of memory*</span></span> 
- <span data-ttu-id="f7939-109">**tx_block_pool_create**: *creare un pool di blocchi di memoria a dimensione fissa*</span><span class="sxs-lookup"><span data-stu-id="f7939-109">**tx_block_pool_create**: *Create pool of fixed-size memory blocks*</span></span> 
- <span data-ttu-id="f7939-110">**tx_block_pool_delete**: *Elimina pool di blocchi di memoria*</span><span class="sxs-lookup"><span data-stu-id="f7939-110">**tx_block_pool_delete**: *Delete memory block pool*</span></span> 
- <span data-ttu-id="f7939-111">**tx_block_pool_info_get**: *recuperare informazioni sul pool di blocchi*</span><span class="sxs-lookup"><span data-stu-id="f7939-111">**tx_block_pool_info_get**: *Retrieve information about block pool*</span></span> 
- <span data-ttu-id="f7939-112">**tx_block_pool_performance_info_get**: *ottenere informazioni sulle prestazioni del pool di blocchi*</span><span class="sxs-lookup"><span data-stu-id="f7939-112">**tx_block_pool_performance_info_get**: *Get block pool performance information*</span></span> 
- <span data-ttu-id="f7939-113">**tx_block_pool_performance_system_info_get**: *ottenere informazioni sulle prestazioni del sistema del pool di blocchi*</span><span class="sxs-lookup"><span data-stu-id="f7939-113">**tx_block_pool_performance_system_info_get**: *Get block pool system performance information*</span></span> 
- <span data-ttu-id="f7939-114">**tx_block_pool_prioritize**: *Priorità elenco sospensioni pool di blocchi*</span><span class="sxs-lookup"><span data-stu-id="f7939-114">**tx_block_pool_prioritize**: *Prioritize block pool suspension list*</span></span> 
- <span data-ttu-id="f7939-115">**tx_block_release**: *rilascia un blocco di memoria a dimensione fissa*</span><span class="sxs-lookup"><span data-stu-id="f7939-115">**tx_block_release**: *Release fixed-size block of memory*</span></span>
- <span data-ttu-id="f7939-116">**tx_byte_allocate**: *allocare byte di memoria*</span><span class="sxs-lookup"><span data-stu-id="f7939-116">**tx_byte_allocate**: *Allocate bytes of memory*</span></span> 
- <span data-ttu-id="f7939-117">**tx_byte_pool_create**: *Crea pool di memoria di byte*</span><span class="sxs-lookup"><span data-stu-id="f7939-117">**tx_byte_pool_create**: *Create memory pool of bytes*</span></span> 
- <span data-ttu-id="f7939-118">**tx_byte_pool_delete**: *eliminare il pool di byte di memoria*</span><span class="sxs-lookup"><span data-stu-id="f7939-118">**tx_byte_pool_delete**: *Delete memory byte pool*</span></span> 
- <span data-ttu-id="f7939-119">**tx_byte_pool_info_get**: *recuperare informazioni sul pool di byte*</span><span class="sxs-lookup"><span data-stu-id="f7939-119">**tx_byte_pool_info_get**: *Retrieve information about byte pool*</span></span> 
- <span data-ttu-id="f7939-120">**tx_byte_pool_performance_info_get**: *ottenere informazioni sulle prestazioni del pool di byte*</span><span class="sxs-lookup"><span data-stu-id="f7939-120">**tx_byte_pool_performance_info_get**: *Get byte pool performance information*</span></span> 
- <span data-ttu-id="f7939-121">**tx_byte_pool_performance_system_info_get**: *ottenere informazioni sulle prestazioni del sistema pool di byte*</span><span class="sxs-lookup"><span data-stu-id="f7939-121">**tx_byte_pool_performance_system_info_get**: *Get byte pool system performance information*</span></span> 
- <span data-ttu-id="f7939-122">**tx_byte_pool_prioritize**: *Priorità elenco di sospensioni del pool di byte*</span><span class="sxs-lookup"><span data-stu-id="f7939-122">**tx_byte_pool_prioritize**: *Prioritize byte pool suspension list*</span></span> 
- <span data-ttu-id="f7939-123">**tx_byte_release**: i *byte di rilascio vengono restituiti al pool di memoria*</span><span class="sxs-lookup"><span data-stu-id="f7939-123">**tx_byte_release**: *Release bytes back to memory pool*</span></span> 
- <span data-ttu-id="f7939-124">**tx_event_flags_create**: *Crea gruppo di flag di evento*</span><span class="sxs-lookup"><span data-stu-id="f7939-124">**tx_event_flags_create**: *Create event flags group*</span></span> 
- <span data-ttu-id="f7939-125">**tx_event_flags_delete**: *Elimina il gruppo di flag di evento*</span><span class="sxs-lookup"><span data-stu-id="f7939-125">**tx_event_flags_delete**: *Delete event flags group*</span></span> 
- <span data-ttu-id="f7939-126">**tx_event_flags_get**: *ottenere i flag di evento dal gruppo di flag di evento*</span><span class="sxs-lookup"><span data-stu-id="f7939-126">**tx_event_flags_get**: *Get event flags from event flags group*</span></span> 
- <span data-ttu-id="f7939-127">**tx_event_flags_info_get**: *recuperare le informazioni sul gruppo di flag di evento*</span><span class="sxs-lookup"><span data-stu-id="f7939-127">**tx_event_flags_info_get**: *Retrieve information about event flags group*</span></span> 
- <span data-ttu-id="f7939-128">**tx_event_flags_performance_info_get**: *ottenere le informazioni sulle prestazioni del gruppo flag evento*</span><span class="sxs-lookup"><span data-stu-id="f7939-128">**tx_event_flags_performance_info_get**: *Get event flags group performance information*</span></span> 
- <span data-ttu-id="f7939-129">**tx_event_flags_performance_system_info_get**: *recuperare informazioni sul sistema delle prestazioni*</span><span class="sxs-lookup"><span data-stu-id="f7939-129">**tx_event_flags_performance_system_info_get**: *Retrieve performance system information*</span></span> 
- <span data-ttu-id="f7939-130">**tx_event_flags_set**: *impostare i flag di evento in un gruppo di flag di evento*</span><span class="sxs-lookup"><span data-stu-id="f7939-130">**tx_event_flags_set**: *Set event flags in an event flags group*</span></span> 
- <span data-ttu-id="f7939-131">**tx_event_flags_set_notify**: *notifica all'applicazione quando vengono impostati i flag di evento*</span><span class="sxs-lookup"><span data-stu-id="f7939-131">**tx_event_flags_set_notify**: *Notify application when event flags are set*</span></span>
- <span data-ttu-id="f7939-132">**tx_interrupt_control**: *Abilitazione e disabilitazione degli interrupt*</span><span class="sxs-lookup"><span data-stu-id="f7939-132">**tx_interrupt_control**: *Enable and disable interrupts*</span></span> 
- <span data-ttu-id="f7939-133">**tx_mutex_create**: *Crea mutex di esclusione reciproca*</span><span class="sxs-lookup"><span data-stu-id="f7939-133">**tx_mutex_create**: *Create mutual exclusion mutex*</span></span> 
- <span data-ttu-id="f7939-134">**tx_mutex_delete**: *eliminazione del mutex di esclusione reciproca*</span><span class="sxs-lookup"><span data-stu-id="f7939-134">**tx_mutex_delete**: *Delete mutual exclusion mutex*</span></span> 
- <span data-ttu-id="f7939-135">**tx_mutex_get**: *ottenere la proprietà di mutex*</span><span class="sxs-lookup"><span data-stu-id="f7939-135">**tx_mutex_get**: *Obtain ownership of mutex*</span></span> 
- <span data-ttu-id="f7939-136">**tx_mutex_info_get**: *recuperare informazioni sul mutex*</span><span class="sxs-lookup"><span data-stu-id="f7939-136">**tx_mutex_info_get**: *Retrieve information about mutex*</span></span> 
- <span data-ttu-id="f7939-137">**tx_mutex_performance_info_get**: *ottenere informazioni sulle prestazioni di mutex*</span><span class="sxs-lookup"><span data-stu-id="f7939-137">**tx_mutex_performance_info_get**: *Get mutex performance information*</span></span> 
- <span data-ttu-id="f7939-138">**tx_mutex_performance_system_info_get**: *ottenere informazioni sulle prestazioni del sistema mutex*</span><span class="sxs-lookup"><span data-stu-id="f7939-138">**tx_mutex_performance_system_info_get**: *Get mutex system performance information*</span></span> 
- <span data-ttu-id="f7939-139">**tx_mutex_prioritize**: *assegnare priorità all'elenco di sospensioni mutex*</span><span class="sxs-lookup"><span data-stu-id="f7939-139">**tx_mutex_prioritize**: *Prioritize mutex suspension list*</span></span> 
- <span data-ttu-id="f7939-140">**tx_mutex_put**: *rilasciare la proprietà di mutex*</span><span class="sxs-lookup"><span data-stu-id="f7939-140">**tx_mutex_put**: *Release ownership of mutex*</span></span> 
- <span data-ttu-id="f7939-141">**tx_queue_create**: *Crea coda messaggi*</span><span class="sxs-lookup"><span data-stu-id="f7939-141">**tx_queue_create**: *Create message queue*</span></span> 
- <span data-ttu-id="f7939-142">**tx_queue_delete**: *Elimina coda messaggi*</span><span class="sxs-lookup"><span data-stu-id="f7939-142">**tx_queue_delete**: *Delete message queue*</span></span> 
- <span data-ttu-id="f7939-143">**tx_queue_flush**: *messaggi vuoti nella coda di messaggi*</span><span class="sxs-lookup"><span data-stu-id="f7939-143">**tx_queue_flush**: *Empty messages in message queue*</span></span> 
- <span data-ttu-id="f7939-144">**tx_queue_front_send**: *inviare un messaggio all'inizio della coda*</span><span class="sxs-lookup"><span data-stu-id="f7939-144">**tx_queue_front_send**: *Send message to the front of queue*</span></span> 
- <span data-ttu-id="f7939-145">**tx_queue_info_get**: *recuperare informazioni sulla coda*</span><span class="sxs-lookup"><span data-stu-id="f7939-145">**tx_queue_info_get**: *Retrieve information about queue*</span></span> 
- <span data-ttu-id="f7939-146">**tx_queue_performance_info_get**: *ottenere informazioni sulle prestazioni della coda*</span><span class="sxs-lookup"><span data-stu-id="f7939-146">**tx_queue_performance_info_get**: *Get queue performance information*</span></span> 
- <span data-ttu-id="f7939-147">**tx_queue_performance_system_info_get**: *ottenere informazioni sulle prestazioni del sistema di Accodamento*</span><span class="sxs-lookup"><span data-stu-id="f7939-147">**tx_queue_performance_system_info_get**: *Get queue system performance information*</span></span>
- <span data-ttu-id="f7939-148">**tx_queue_prioritize**: *assegnare priorità all'elenco di sospensioni della coda*</span><span class="sxs-lookup"><span data-stu-id="f7939-148">**tx_queue_prioritize**: *Prioritize queue suspension list*</span></span> 
- <span data-ttu-id="f7939-149">**tx_queue_receive**: *ottenere un messaggio dalla coda di messaggi*</span><span class="sxs-lookup"><span data-stu-id="f7939-149">**tx_queue_receive**: *Get message from message queue*</span></span> 
- <span data-ttu-id="f7939-150">**tx_queue_send**: *inviare un messaggio alla coda di messaggi*</span><span class="sxs-lookup"><span data-stu-id="f7939-150">**tx_queue_send**: *Send message to message queue*</span></span> 
- <span data-ttu-id="f7939-151">**tx_queue_send_notify**: *notifica all'applicazione quando il messaggio viene inviato alla coda*</span><span class="sxs-lookup"><span data-stu-id="f7939-151">**tx_queue_send_notify**: *Notify application when message is sent to queue*</span></span> 
- <span data-ttu-id="f7939-152">**tx_semaphore_ceiling_put**: *inserire un'istanza in conteggio semaforo con limite massimo*</span><span class="sxs-lookup"><span data-stu-id="f7939-152">**tx_semaphore_ceiling_put**: *Place an instance in counting semaphore with ceiling*</span></span> 
- <span data-ttu-id="f7939-153">**tx_semaphore_create**: *Crea semaforo conteggio*</span><span class="sxs-lookup"><span data-stu-id="f7939-153">**tx_semaphore_create**: *Create counting semaphore*</span></span> 
- <span data-ttu-id="f7939-154">**tx_semaphore_delete**: *Elimina semaforo di conteggio*</span><span class="sxs-lookup"><span data-stu-id="f7939-154">**tx_semaphore_delete**: *Delete counting semaphore*</span></span> 
- <span data-ttu-id="f7939-155">**tx_semaphore_get**: *ottenere un'istanza da un semaforo di conteggio*</span><span class="sxs-lookup"><span data-stu-id="f7939-155">**tx_semaphore_get**: *Get instance from counting semaphore*</span></span> 
- <span data-ttu-id="f7939-156">**tx_semaphore_info_get**: *recuperare informazioni sul semaforo*</span><span class="sxs-lookup"><span data-stu-id="f7939-156">**tx_semaphore_info_get**: *Retrieve information about semaphore*</span></span> 
- <span data-ttu-id="f7939-157">**tx_semaphore_performance_info_get**: *ottenere informazioni sulle prestazioni del semaforo*</span><span class="sxs-lookup"><span data-stu-id="f7939-157">**tx_semaphore_performance_info_get**: *Get semaphore performance information*</span></span> 
- <span data-ttu-id="f7939-158">**tx_semaphore_performance_system_info_get**: *ottenere informazioni sulle prestazioni del sistema Semaphore*</span><span class="sxs-lookup"><span data-stu-id="f7939-158">**tx_semaphore_performance_system_info_get**: *Get semaphore system performance information*</span></span> 
- <span data-ttu-id="f7939-159">**tx_semaphore_prioritize**: *assegnare priorità all'elenco di sospensioni del semaforo*</span><span class="sxs-lookup"><span data-stu-id="f7939-159">**tx_semaphore_prioritize**: *Prioritize semaphore suspension list*</span></span> 
- <span data-ttu-id="f7939-160">**tx_semaphore_put**: *inserire un'istanza in conteggio semaforo*</span><span class="sxs-lookup"><span data-stu-id="f7939-160">**tx_semaphore_put**: *Place an instance in counting semaphore*</span></span> 
- <span data-ttu-id="f7939-161">**tx_semaphore_put_notify**: *notifica all'applicazione quando viene inserito il semaforo*</span><span class="sxs-lookup"><span data-stu-id="f7939-161">**tx_semaphore_put_notify**: *Notify application when semaphore is put*</span></span> 
- <span data-ttu-id="f7939-162">**tx_thread_create**: *creare il thread dell'applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-162">**tx_thread_create**: *Create application thread*</span></span> 
- <span data-ttu-id="f7939-163">**tx_thread_delete**: *eliminare il thread dell'applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-163">**tx_thread_delete**: *Delete application thread*</span></span>
- <span data-ttu-id="f7939-164">**tx_thread_entry_exit_notify**: *notifica l'applicazione al momento della voce e dell'uscita del thread*</span><span class="sxs-lookup"><span data-stu-id="f7939-164">**tx_thread_entry_exit_notify**: *Notify application upon thread entry and exit*</span></span> 
- <span data-ttu-id="f7939-165">**tx_thread_identify**: *Recupera il puntatore al thread attualmente in esecuzione*</span><span class="sxs-lookup"><span data-stu-id="f7939-165">**tx_thread_identify**: *Retrieves pointer to currently executing thread*</span></span> 
- <span data-ttu-id="f7939-166">**tx_thread_info_get**: *recuperare informazioni sul thread*</span><span class="sxs-lookup"><span data-stu-id="f7939-166">**tx_thread_info_get**: *Retrieve information about thread*</span></span> 
- <span data-ttu-id="f7939-167">**tx_thread_performance_info_get**: *ottenere informazioni sulle prestazioni del thread*</span><span class="sxs-lookup"><span data-stu-id="f7939-167">**tx_thread_performance_info_get**: *Get thread performance information*</span></span> 
- <span data-ttu-id="f7939-168">**tx_thread_performance_system_info_get**: *ottenere informazioni sulle prestazioni del sistema di thread*</span><span class="sxs-lookup"><span data-stu-id="f7939-168">**tx_thread_performance_system_info_get**: *Get thread system performance information*</span></span> 
- <span data-ttu-id="f7939-169">**tx_thread_preemption_change**: *modificare la soglia di precedenza del thread dell'applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-169">**tx_thread_preemption_change**: *Change preemption-threshold of application thread*</span></span> 
- <span data-ttu-id="f7939-170">**tx_thread_priority_change**: *modificare la priorità del thread dell'applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-170">**tx_thread_priority_change**: *Change priority of application thread*</span></span> 
- <span data-ttu-id="f7939-171">**tx_thread_relinquish**: *cede il controllo ad altri thread dell'applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-171">**tx_thread_relinquish**: *Relinquish control to other application threads*</span></span> 
- <span data-ttu-id="f7939-172">**tx_thread_reset**: *Reimposta thread*</span><span class="sxs-lookup"><span data-stu-id="f7939-172">**tx_thread_reset**: *Reset thread*</span></span> 
- <span data-ttu-id="f7939-173">**tx_thread_resume**: *riprende il thread dell'applicazione sospesa*</span><span class="sxs-lookup"><span data-stu-id="f7939-173">**tx_thread_resume**: *Resume suspended application thread*</span></span> 
- <span data-ttu-id="f7939-174">**tx_thread_sleep**: *sospende il thread corrente per l'ora specificata*</span><span class="sxs-lookup"><span data-stu-id="f7939-174">**tx_thread_sleep**: *Suspend current thread for specified time*</span></span> 
- <span data-ttu-id="f7939-175">**tx_thread_smp_core_exclude**: *escludere l'esecuzione del thread in un set di core*</span><span class="sxs-lookup"><span data-stu-id="f7939-175">**tx_thread_smp_core_exclude**: *Exclude thread execution on a set of cores*</span></span> 
- <span data-ttu-id="f7939-176">**tx_thread_smp_core_exclude_get**: *Ottiene l'esclusione principale corrente del thread*</span><span class="sxs-lookup"><span data-stu-id="f7939-176">**tx_thread_smp_core_exclude_get**: *Gets the thread's current core exclusion*</span></span> 
- <span data-ttu-id="f7939-177">**tx_thread_smp_core_get**: *recuperare il nucleo del chiamante attualmente in esecuzione*</span><span class="sxs-lookup"><span data-stu-id="f7939-177">**tx_thread_smp_core_get**: *Retrieve currently executing core of caller*</span></span> 
- <span data-ttu-id="f7939-178">**tx_thread_stack_error_notify**: *richiamata della notifica degli errori dello stack di thread*</span><span class="sxs-lookup"><span data-stu-id="f7939-178">**tx_thread_stack_error_notify**: *Register thread stack error notification callback*</span></span> 
- <span data-ttu-id="f7939-179">**tx_thread_suspend**: *sospendere il thread dell'applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-179">**tx_thread_suspend**: *Suspend application thread*</span></span>
- <span data-ttu-id="f7939-180">**tx_thread_terminate**: *termina il thread dell'applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-180">**tx_thread_terminate**: *Terminates application thread*</span></span> 
- <span data-ttu-id="f7939-181">**tx_thread_time_slice_change**: *modifica la sezione temporale del thread dell'applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-181">**tx_thread_time_slice_change**: *Changes time-slice of application thread*</span></span> 
- <span data-ttu-id="f7939-182">**tx_thread_wait_abort**: *interrompere la sospensione del thread specificato*</span><span class="sxs-lookup"><span data-stu-id="f7939-182">**tx_thread_wait_abort**: *Abort suspension of specified thread*</span></span> 
- <span data-ttu-id="f7939-183">**tx_time_get**: *Recupera l'ora corrente*</span><span class="sxs-lookup"><span data-stu-id="f7939-183">**tx_time_get**: *Retrieves the current time*</span></span> 
- <span data-ttu-id="f7939-184">**tx_time_set**: *imposta l'ora corrente*</span><span class="sxs-lookup"><span data-stu-id="f7939-184">**tx_time_set**: *Sets the current time*</span></span> 
- <span data-ttu-id="f7939-185">**tx_timer_activate**: *attiva timer applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-185">**tx_timer_activate**: *Activate application timer*</span></span> 
- <span data-ttu-id="f7939-186">**tx_timer_change**: *Modifica timer applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-186">**tx_timer_change**: *Change application timer*</span></span> 
- <span data-ttu-id="f7939-187">**tx_timer_create**: *Crea timer applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-187">**tx_timer_create**: *Create application timer*</span></span> 
- <span data-ttu-id="f7939-188">**tx_timer_deactivate**: *Disattiva timer applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-188">**tx_timer_deactivate**: *Deactivate application timer*</span></span> 
- <span data-ttu-id="f7939-189">**tx_timer_delete**: *Elimina timer applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-189">**tx_timer_delete**: *Delete application timer*</span></span> 
- <span data-ttu-id="f7939-190">**tx_timer_info_get**: *recuperare informazioni sul timer di un'applicazione*</span><span class="sxs-lookup"><span data-stu-id="f7939-190">**tx_timer_info_get**: *Retrieve information about an application timer*</span></span> 
- <span data-ttu-id="f7939-191">**tx_timer_performance_info_get**: *ottenere informazioni sulle prestazioni del timer*</span><span class="sxs-lookup"><span data-stu-id="f7939-191">**tx_timer_performance_info_get**: *Get timer performance information*</span></span> 
- <span data-ttu-id="f7939-192">**tx_timer_performance_system_info_get**: *ottenere informazioni sulle prestazioni del sistema timer*</span><span class="sxs-lookup"><span data-stu-id="f7939-192">**tx_timer_performance_system_info_get**: *Get timer system performance information*</span></span> 
- <span data-ttu-id="f7939-193">**tx_timer_smp_core_exclude**: *escludere l'esecuzione del timer in un set di core*</span><span class="sxs-lookup"><span data-stu-id="f7939-193">**tx_timer_smp_core_exclude**: *Exclude timer execution on a set of cores*</span></span> 
- <span data-ttu-id="f7939-194">**tx_timer_smp_core_exclude_get**: *Ottiene l'esclusione di base corrente del timer*</span><span class="sxs-lookup"><span data-stu-id="f7939-194">**tx_timer_smp_core_exclude_get**: *Gets the timer's current core exclusion*</span></span>

## <a name="tx_block_allocate"></a><span data-ttu-id="f7939-195">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-195">tx_block_allocate</span></span>
<span data-ttu-id="f7939-196">Allocare un blocco di memoria di dimensioni fisse</span><span class="sxs-lookup"><span data-stu-id="f7939-196">Allocate fixed-size block of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-197">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-197">Prototype</span></span>

```C
UINT tx_block_allocate(TX_BLOCK_POOL *pool_ptr, VOID **block_ptr,
                          ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="f7939-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-198">Description</span></span>

<span data-ttu-id="f7939-199">Questo servizio alloca un blocco di memoria di dimensioni fisse dal pool di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-199">This service allocates a fixed-size memory block from the specified memory pool.</span></span> <span data-ttu-id="f7939-200">La dimensione effettiva del blocco di memoria viene determinata durante la creazione del pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-200">The actual size of the memory block is determined during memory pool creation.</span></span>

> [!WARNING]
> <span data-ttu-id="f7939-201">È importante assicurarsi che il codice dell'applicazione non scriva al di fuori del blocco di memoria allocato.</span><span class="sxs-lookup"><span data-stu-id="f7939-201">It is important to ensure application code does not write outside the allocated memory block.</span></span> <span data-ttu-id="f7939-202">In tal caso, il danneggiamento si verifica in un blocco di memoria adiacente, in genere successivo.</span><span class="sxs-lookup"><span data-stu-id="f7939-202">If this happens, corruption occurs in an adjacent (usually subsequent) memory block.</span></span> <span data-ttu-id="f7939-203">I risultati sono imprevedibili e spesso sono irreversibili.</span><span class="sxs-lookup"><span data-stu-id="f7939-203">The results are unpredictable and are often fatal!</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-204">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-204">Parameters</span></span>

- <span data-ttu-id="f7939-205">**pool_ptr**: puntatore a un pool di blocchi di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-205">**pool_ptr**: Pointer to a previously created memory block pool.</span></span>
- <span data-ttu-id="f7939-206">**block_ptr**: puntatore a un puntatore a blocco di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-206">**block_ptr**: Pointer to a destination block pointer.</span></span> <span data-ttu-id="f7939-207">Al completamento dell'allocazione, l'indirizzo del blocco di memoria allocato viene inserito nel punto in cui questo parametro punta.</span><span class="sxs-lookup"><span data-stu-id="f7939-207">On successful allocation, the address of the allocated memory block is placed where this parameter points.</span></span>
- <span data-ttu-id="f7939-208">**WAIT_OPTION**: definisce il comportamento del servizio se non sono disponibili blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-208">**wait_option**: Defines how the service behaves if there are no memory blocks available.</span></span> <span data-ttu-id="f7939-209">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="f7939-209">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="f7939-210">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="f7939-210">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="f7939-211">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="f7939-211">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="f7939-212">valore di timeout: (0x00000001 tramite 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="f7939-212">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>  
    
    <span data-ttu-id="f7939-213">Se si seleziona TX_NO_WAIT viene restituito immediatamente il risultato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="f7939-213">Selecting TX_NO_WAIT results in an immediate return from this service regardless if it was successful or not.</span></span> <span data-ttu-id="f7939-214">Questa è l'unica opzione valida se il servizio viene chiamato da un non thread. ad esempio, inizializzazione, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-214">This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.</span></span>

    <span data-ttu-id="f7939-215">Se si seleziona TX_WAIT_FOREVER, il thread chiamante sospenderà a tempo indefinito fino a quando non sarà disponibile un blocco di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-215">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a memory block is available.</span></span>

    <span data-ttu-id="f7939-216">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa di un blocco di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-216">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a memory block.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-217">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-217">Return Values</span></span>

- <span data-ttu-id="f7939-218">**TX_SUCCESS**: (0x00) allocazione di blocchi di memoria riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-218">**TX_SUCCESS**: (0x00) Successful memory block allocation.</span></span>
- <span data-ttu-id="f7939-219">**TX_DELETED**: (0x01) il pool di blocchi di memoria è stato eliminato durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-219">**TX_DELETED**: (0x01) Memory block pool was deleted while thread was suspended.</span></span>
- <span data-ttu-id="f7939-220">**TX_NO_MEMORY**: il servizio (0x10) non è stato in grado di allocare un blocco di memoria entro il tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-220">**TX_NO_MEMORY**: (0x10) Service was unable to allocate a block of memory within the specified time to wait.</span></span>
- <span data-ttu-id="f7939-221">**TX_WAIT_ABORTED**: la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-221">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer or ISR.</span></span>
- <span data-ttu-id="f7939-222">TX_POOL_ERROR: (0x02) puntatore al pool di blocchi di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-222">TX_POOL_ERROR: (0x02) Invalid memory block pool pointer.</span></span>
- <span data-ttu-id="f7939-223">TX_PTR_ERROR: (0x03) puntatore non valido al puntatore di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-223">TX_PTR_ERROR: (0x03) Invalid pointer to destination pointer.</span></span>
- <span data-ttu-id="f7939-224">TX_WAIT_ERROR: (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-224">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-225">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-225">Allowed From</span></span>

<span data-ttu-id="f7939-226">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-226">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-227">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-227">Preemption Possible</span></span>

<span data-ttu-id="f7939-228">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-228">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-229">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-229">Example</span></span>

```c
TX_BLOCK_POOL   my_pool;
unsigned char*memory_ptr;
UINT         status;

/* Allocate a memory block from my_pool. Assume that the
   pool has already been created with a call to
   tx_block_pool_create. */
status = tx_block_allocate(&my_pool, (VOID **) &memory_ptr,
                               TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the
   address of the allocated block of memory. */
```

### <a name="see-also"></a><span data-ttu-id="f7939-230">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-230">See Also</span></span>

- <span data-ttu-id="f7939-231">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-231">tx_block_pool_create</span></span>
- <span data-ttu-id="f7939-232">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-232">tx_block_pool_delete</span></span>
- <span data-ttu-id="f7939-233">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-233">tx_block_pool_info_get</span></span>
- <span data-ttu-id="f7939-234">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-234">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-235">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-235">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-236">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-236">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="f7939-237">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="f7939-237">tx_block_release</span></span>

## <a name="tx_block_pool_create"></a><span data-ttu-id="f7939-238">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-238">tx_block_pool_create</span></span>
<span data-ttu-id="f7939-239">Creare un pool di blocchi di memoria a dimensione fissa</span><span class="sxs-lookup"><span data-stu-id="f7939-239">Create pool of fixed-size memory blocks</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-240">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-240">Prototype</span></span>

```C
UINT tx_block_pool_create(TX_BLOCK_POOL *pool_ptr,
                          CHAR *name_ptr, ULONG block_size,
                          VOID *pool_start, ULONG pool_size);
```
### <a name="description"></a><span data-ttu-id="f7939-241">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-241">Description</span></span>

<span data-ttu-id="f7939-242">Questo servizio crea un pool di blocchi di memoria di dimensioni fisse.</span><span class="sxs-lookup"><span data-stu-id="f7939-242">This service creates a pool of fixed-size memory blocks.</span></span> <span data-ttu-id="f7939-243">L'area di memoria specificata è divisa in tutti i blocchi di memoria di dimensioni fisse possibili utilizzando la formula:</span><span class="sxs-lookup"><span data-stu-id="f7939-243">The memory area specified is divided into as many fixed-size memory blocks as possible using the formula:</span></span>    
<span data-ttu-id="f7939-244">**blocchi totali** = (**byte totali**)/(**dimensione blocco** + sizeof (void \*))</span><span class="sxs-lookup"><span data-stu-id="f7939-244">**total blocks** = (**total bytes**) / (**block size** + sizeof(void \*))</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-245">Ogni blocco di memoria contiene un puntatore di overhead invisibile all'utente ed è rappresentato da "sizeof (void \*)" nella formula precedente.</span><span class="sxs-lookup"><span data-stu-id="f7939-245">Each memory block contains one pointer of overhead that is invisible to the user and is represented by the “sizeof(void \*)” in the preceding formula.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-246">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-246">Parameters</span></span>

- <span data-ttu-id="f7939-247">**pool_ptr**: puntatore a un blocco di controllo del pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-247">**pool_ptr**: Pointer to a memory block pool control block.</span></span>
- <span data-ttu-id="f7939-248">**name_ptr**: puntatore al nome del pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-248">**name_ptr**: Pointer to the name of the memory block pool.</span></span>
- <span data-ttu-id="f7939-249">**block_size**: numero di byte in ogni blocco di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-249">**block_size**: Number of bytes in each memory block.</span></span>
- <span data-ttu-id="f7939-250">**pool_start**: indirizzo iniziale del pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-250">**pool_start**: Starting address of the memory block pool.</span></span> <span data-ttu-id="f7939-251">L'indirizzo iniziale deve essere allineato alle dimensioni del tipo di dati ULONG.</span><span class="sxs-lookup"><span data-stu-id="f7939-251">The starting address must be aligned to the size of the ULONG data type..</span></span>
- <span data-ttu-id="f7939-252">**pool_size**: numero totale di byte disponibili per il pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-252">**pool_size**: Total number of bytes available for the memory block pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-253">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-253">Return Values</span></span>

- <span data-ttu-id="f7939-254">**TX_SUCCESS**: (0x00) creazione del pool di blocchi di memoria riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-254">**TX_SUCCESS**: (0x00) Successful memory block pool creation.</span></span>
- <span data-ttu-id="f7939-255">TX_POOL_ERROR: (0x02) puntatore al pool di blocchi di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-255">TX_POOL_ERROR: (0x02) Invalid memory block pool pointer.</span></span> <span data-ttu-id="f7939-256">Il puntatore è NULL o il pool è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="f7939-256">Either the pointer is NULL or the pool is already created.</span></span>
- <span data-ttu-id="f7939-257">TX_PTR_ERROR: (0x03) indirizzo iniziale non valido del pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-257">TX_PTR_ERROR: (0x03) Invalid starting address of the pool.</span></span>
- <span data-ttu-id="f7939-258">TX_SIZE_ERROR: le dimensioni del pool (0x05) non sono valide.</span><span class="sxs-lookup"><span data-stu-id="f7939-258">TX_SIZE_ERROR: (0x05) Size of pool is invalid.</span></span>
- <span data-ttu-id="f7939-259">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-259">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-260">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-260">Allowed From</span></span>

<span data-ttu-id="f7939-261">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="f7939-261">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-262">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-262">Preemption Possible</span></span>

<span data-ttu-id="f7939-263">No</span><span class="sxs-lookup"><span data-stu-id="f7939-263">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-264">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-264">Example</span></span>

```C
TX_BLOCK_POOL  my_pool;
UINT           status;

/* Create a memory pool whose total size is 1000 bytes
   starting at address 0x100000. Each block in this
   pool is defined to be 50 bytes long. */
status = tx_block_pool_create(&my_pool, "my_pool_name",
               50, (VOID *) 0x100000, 1000);

/* If status equals TX_SUCCESS, my_pool contains 18
   memory blocks of 50 bytes each. The reason
   there are not 20 blocks in the pool is
   because of the one overhead pointer associated with each
   block. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-265">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-265">See Also</span></span>

- <span data-ttu-id="f7939-266">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-266">tx_block_allocate</span></span>
- <span data-ttu-id="f7939-267">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-267">tx_block_pool_delete</span></span>
- <span data-ttu-id="f7939-268">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-268">tx_block_pool_info_get</span></span>
- <span data-ttu-id="f7939-269">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-269">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-270">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-270">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-271">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-271">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="f7939-272">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="f7939-272">tx_block_release</span></span>

## <a name="tx_block_pool_delete"></a><span data-ttu-id="f7939-273">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-273">tx_block_pool_delete</span></span>

<span data-ttu-id="f7939-274">Elimina pool di blocchi di memoria</span><span class="sxs-lookup"><span data-stu-id="f7939-274">Delete memory block pool</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-275">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-275">Prototype</span></span>

```C
UINT tx_block_pool_delete(TX_BLOCK_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-276">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-276">Description</span></span>

<span data-ttu-id="f7939-277">Questo servizio Elimina il pool di memoria di blocco specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-277">This service deletes the specified block-memory pool.</span></span> <span data-ttu-id="f7939-278">Tutti i thread sospesi in attesa di un blocco di memoria da questo pool vengono ripresi e viene fornito un TX_DELETED stato restituito.</span><span class="sxs-lookup"><span data-stu-id="f7939-278">All threads suspended waiting for a memory block from this pool are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-279">È responsabilità dell'applicazione gestire l'area di memoria associata al pool, disponibile al termine del servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-279">It is the application’s responsibility to manage the memory area associated with the pool, which is available after this service completes.</span></span> <span data-ttu-id="f7939-280">Inoltre, l'applicazione deve impedire l'uso di un pool eliminato o dei blocchi di memoria precedenti.</span><span class="sxs-lookup"><span data-stu-id="f7939-280">In addition, the application must prevent use of a deleted pool or its former memory blocks.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-281">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-281">Parameters</span></span>

- <span data-ttu-id="f7939-282">**pool_ptr**: puntatore a un pool di blocchi di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-282">**pool_ptr**: Pointer to a previously created memory block pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-283">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-283">Return Values</span></span>

- <span data-ttu-id="f7939-284">**TX_SUCCESS**: (0x00) eliminazione del pool di blocchi di memoria riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-284">**TX_SUCCESS**: (0x00) Successful memory block pool deletion.</span></span>
- <span data-ttu-id="f7939-285">TX_POOL_ERROR: (0x02) puntatore al pool di blocchi di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-285">TX_POOL_ERROR: (0x02) Invalid memory block pool pointer.</span></span>
- <span data-ttu-id="f7939-286">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-286">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-287">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-287">Allowed From</span></span>

<span data-ttu-id="f7939-288">Thread</span><span class="sxs-lookup"><span data-stu-id="f7939-288">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-289">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-289">Preemption Possible</span></span>

<span data-ttu-id="f7939-290">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-290">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-291">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-291">Example</span></span>

```C
TX_BLOCK_POOLmy_pool;
UINT           status;

    /* Delete entire memory block pool. Assume that the pool
      has already been created with a call to
      tx_block_pool_create. */
    status =  tx_block_pool_delete(&my_pool);

    /* If status equals TX_SUCCESS, the memory block pool is
       deleted. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-292">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-292">See Also</span></span>

- <span data-ttu-id="f7939-293">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-293">tx_block_allocate</span></span>
- <span data-ttu-id="f7939-294">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-294">tx_block_pool_create</span></span>
- <span data-ttu-id="f7939-295">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-295">tx_block_pool_info_get</span></span>
- <span data-ttu-id="f7939-296">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-296">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-297">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-297">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-298">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-298">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="f7939-299">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="f7939-299">tx_block_release</span></span>

## <a name="tx_block_pool_info_get"></a><span data-ttu-id="f7939-300">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-300">tx_block_pool_info_get</span></span>

<span data-ttu-id="f7939-301">Recuperare informazioni sul pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="f7939-301">Retrieve information about block pool</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-302">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-302">Prototype</span></span>

```C
UINT tx_block_pool_info_get(TX_BLOCK_POOL *pool_ptr, CHAR **name,
                          ULONG *available, ULONG *total_blocks,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count,
                          TX_BLOCK_POOL **next_pool);
```
### <a name="description"></a><span data-ttu-id="f7939-303">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-303">Description</span></span>

<span data-ttu-id="f7939-304">Questo servizio recupera le informazioni sul pool di memoria del blocco specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-304">This service retrieves information about the specified block memory pool.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-305">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-305">Parameters</span></span>

- <span data-ttu-id="f7939-306">**pool_ptr**: puntatore al pool di blocchi di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-306">**pool_ptr**: Pointer to previously created memory block pool.</span></span>
- <span data-ttu-id="f7939-307">**Name**: puntatore alla destinazione per il puntatore al nome del pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="f7939-307">**name**: Pointer to destination for the pointer to the block pool’s name.</span></span>
- <span data-ttu-id="f7939-308">**available**: puntatore alla destinazione per il numero di blocchi disponibili nel pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="f7939-308">**available**: Pointer to destination for the number of available blocks in the block pool.</span></span>
- <span data-ttu-id="f7939-309">**total_blocks**: puntatore alla destinazione per il numero totale di blocchi nel pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="f7939-309">**total_blocks**: Pointer to destination for the total number of blocks in the block pool.</span></span>
- <span data-ttu-id="f7939-310">**first_suspended**: puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione di questo pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="f7939-310">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this block pool.</span></span>
- <span data-ttu-id="f7939-311">**suspended_count**: puntatore alla destinazione per il numero di thread attualmente sospesi in questo pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="f7939-311">**suspended_count**: Pointer to destination for the number of threads currently suspended on this block pool.</span></span>
- <span data-ttu-id="f7939-312">**next_pool**: puntatore alla destinazione per l'indicatore di misura del pool di blocchi creato successivamente.</span><span class="sxs-lookup"><span data-stu-id="f7939-312">**next_pool**: Pointer to destination for the pointer of the next created block pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-313">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-313">Supplying a TX_NULL for any parameter indicates the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-314">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-314">Return Values</span></span>

- <span data-ttu-id="f7939-315">**TX_SUCCESS**: (0x00) il recupero delle informazioni sul pool di blocchi è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-315">**TX_SUCCESS**: (0x00) Successful block pool information retrieve.</span></span>
- <span data-ttu-id="f7939-316">TX_POOL_ERROR: (0x02) puntatore al pool di blocchi di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-316">TX_POOL_ERROR: (0x02) Invalid memory block pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-317">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-317">Allowed From</span></span>

<span data-ttu-id="f7939-318">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-318">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-319">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-319">Example</span></span>

```C
TX_BLOCK_POOL    my_pool;
CHAR             *name;
ULONG            available;
ULONG            total_blocks;
TX_THREAD        *first_suspended;
ULONG            suspended_count;
TX_BLOCK_POOL    *next_pool;
UINT             status;

/* Retrieve information about the previously created
   block pool "my_pool." */
status = tx_block_pool_info_get(&my_pool, &name,
                &available,&total_blocks,
                &first_suspended, &suspended_count,
                &next_pool);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-320">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-320">See Also</span></span>

- <span data-ttu-id="f7939-321">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-321">tx_block_allocate</span></span>
- <span data-ttu-id="f7939-322">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-322">tx_block_pool_create</span></span>
- <span data-ttu-id="f7939-323">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-323">tx_block_pool_delete</span></span>
- <span data-ttu-id="f7939-324">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-324">tx_block_pool_info_get</span></span>
- <span data-ttu-id="f7939-325">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-325">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-326">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-326">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-327">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-327">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="f7939-328">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="f7939-328">tx_block_release</span></span>

## <a name="tx_block_pool_performance_info_get"></a><span data-ttu-id="f7939-329">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-329">tx_block_pool_performance_info_get</span></span>

<span data-ttu-id="f7939-330">Ottenere informazioni sulle prestazioni del pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="f7939-330">Get block pool performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-331">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-331">Prototype</span></span>

```c
UINT tx_block_pool_performance_info_get(TX_BLOCK_POOL *pool_ptr,
       ULONG *allocates, ULONG *releases,
       ULONG *suspensions, ULONG *timeouts));
```

### <a name="description"></a><span data-ttu-id="f7939-332">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-332">Description</span></span>

<span data-ttu-id="f7939-333">Questo servizio recupera le informazioni sulle prestazioni relative al pool di blocchi di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-333">This service retrieves performance information about the specified memory block pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-334">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-334">The ThreadX SMP library and application must be built with **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-335">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-335">Parameters</span></span>

- <span data-ttu-id="f7939-336">**pool_ptr**: puntatore al pool di blocchi di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-336">**pool_ptr**: Pointer to previously created memory block pool.</span></span>
- <span data-ttu-id="f7939-337">**alloca**: puntatore alla destinazione per il numero di richieste di allocazione eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-337">**allocates**: Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="f7939-338">**versioni**: puntatore alla destinazione per il numero di richieste di versione eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-338">**releases**: Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="f7939-339">**sospensioni**: puntatore alla destinazione per il numero di sospensioni di allocazione di thread nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-339">**suspensions**: Pointer to destination for the number of thread allocation suspensions on this pool.</span></span>
- <span data-ttu-id="f7939-340">**timeout**: puntatore alla destinazione per il numero di timeout di allocazione della sospensione nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-340">**timeouts**: Pointer to destination for the number of allocate suspension timeouts on this pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-341">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-341">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-342">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-342">Return Values</span></span>

- <span data-ttu-id="f7939-343">**TX_SUCCESS**: (0x00) esito positivo del pool di blocchi Get.</span><span class="sxs-lookup"><span data-stu-id="f7939-343">**TX_SUCCESS**: (0x00) Successful block pool performance get.</span></span>
- <span data-ttu-id="f7939-344">**TX_PTR_ERROR**: (0x03) puntatore al pool di blocchi non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-344">**TX_PTR_ERROR**: (0x03) Invalid block pool pointer.</span></span>
- <span data-ttu-id="f7939-345">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-345">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-346">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-346">Allowed From</span></span>

<span data-ttu-id="f7939-347">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-347">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-348">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-348">Example</span></span>

```C
TX_BLOCK_POOL     my_pool;
ULONG             allocates;
ULONG             releases;
ULONG             suspensions;
ULONG             timeouts;

/* Retrieve performance information on the previously created block
   pool. */
status = tx_block_pool_performance_info_get(&my_pool, &allocates,
                                            &releases,
                &suspensions,
                &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-349">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-349">See Also</span></span>

- <span data-ttu-id="f7939-350">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-350">tx_block_allocate</span></span>
- <span data-ttu-id="f7939-351">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-351">tx_block_pool_create</span></span>
- <span data-ttu-id="f7939-352">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-352">tx_block_pool_delete</span></span>
- <span data-ttu-id="f7939-353">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-353">tx_block_pool_info_get</span></span>
- <span data-ttu-id="f7939-354">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-354">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-355">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-355">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-356">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="f7939-356">tx_block_release</span></span>

## <a name="tx_block_pool_performance_system_info_get"></a><span data-ttu-id="f7939-357">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-357">tx_block_pool_performance_system_info_get</span></span>

<span data-ttu-id="f7939-358">Ottenere informazioni sulle prestazioni del sistema del pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="f7939-358">Get block pool system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-359">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-359">Prototype</span></span>

```C
UINT tx_block_pool_performance_system_info_get(ULONG *allocates,
       ULONG *releases, ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="f7939-360">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-360">Description</span></span>

<span data-ttu-id="f7939-361">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i pool di blocchi di memoria nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-361">This service retrieves performance information about all memory block pools in the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-362">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-362">The ThreadX SMP library and application must be built with **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-363">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-363">Parameters</span></span>

- <span data-ttu-id="f7939-364">**alloca**: puntatore alla destinazione per il numero totale di richieste di allocazione eseguite su tutti i pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="f7939-364">**allocates**: Pointer to destination for the total number of allocate requests performed on all block pools.</span></span>
- <span data-ttu-id="f7939-365">**versioni**: puntatore alla destinazione per il numero totale di richieste di rilascio eseguite su tutti i pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="f7939-365">**releases**: Pointer to destination for the total number of release requests performed on all block pools.</span></span>
- <span data-ttu-id="f7939-366">**sospensioni**: puntatore alla destinazione per il numero totale di sospensioni di allocazione di thread in tutti i pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="f7939-366">**suspensions**: Pointer to destination for the total number of thread allocation suspensions on all block pools.</span></span>
- <span data-ttu-id="f7939-367">**timeout**: puntatore alla destinazione per il numero totale di timeout di allocazione della sospensione in tutti i pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="f7939-367">**timeouts**: Pointer to destination for the total number of allocate suspension timeouts on all block pools.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-368">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-368">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-369">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-369">Return Values</span></span>

- <span data-ttu-id="f7939-370">**TX_SUCCESS**: (0x00) prestazioni del sistema del pool di blocchi riusciti Get.</span><span class="sxs-lookup"><span data-stu-id="f7939-370">**TX_SUCCESS**: (0x00) Successful block pool system performance get.</span></span>
- <span data-ttu-id="f7939-371">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-371">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-372">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-372">Allowed From</span></span>

<span data-ttu-id="f7939-373">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-373">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-374">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-374">Example</span></span>

```C
ULONG         allocates;
ULONG         releases;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all the block pools in
   the system. */
status = tx_block_pool_performance_system_info_get(&allocates,
                     &releases,&suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-375">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-375">See Also</span></span>

- <span data-ttu-id="f7939-376">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-376">tx_block_allocate</span></span>
- <span data-ttu-id="f7939-377">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-377">tx_block_pool_create</span></span>
- <span data-ttu-id="f7939-378">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-378">tx_block_pool_delete</span></span>
- <span data-ttu-id="f7939-379">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-379">tx_block_pool_info_get</span></span>
- <span data-ttu-id="f7939-380">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-380">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-381">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-381">tx_block_pool_prioritize</span></span>
- <span data-ttu-id="f7939-382">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="f7939-382">tx_block_release</span></span>

## <a name="tx_block_pool_prioritize"></a><span data-ttu-id="f7939-383">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-383">tx_block_pool_prioritize</span></span>

<span data-ttu-id="f7939-384">Priorità elenco sospensione pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="f7939-384">Prioritize block pool suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-385">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-385">Prototype</span></span>

```C
UINT tx_block_pool_prioritize(TX_BLOCK_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-386">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-386">Description</span></span>

<span data-ttu-id="f7939-387">Questo servizio posiziona il thread con priorità più elevata sospeso per un blocco di memoria in questo pool all'inizio dell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="f7939-387">This service places the highest priority thread suspended for a block of memory on this pool at the front of the suspension list.</span></span> <span data-ttu-id="f7939-388">Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.</span><span class="sxs-lookup"><span data-stu-id="f7939-388">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-389">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-389">Parameters</span></span> 

- <span data-ttu-id="f7939-390">**pool_ptr**: puntatore a un blocco di controllo del pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-390">**pool_ptr**: Pointer to a memory block pool control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-391">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-391">Return Values</span></span>

- <span data-ttu-id="f7939-392">**TX_SUCCESS**: (0x00) priorità del pool di blocchi riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-392">**TX_SUCCESS**: (0x00) Successful block pool prioritize.</span></span>
- <span data-ttu-id="f7939-393">TX_POOL_ERROR: (0x02) puntatore al pool di blocchi di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-393">TX_POOL_ERROR: (0x02) Invalid memory block pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-394">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-394">Allowed From</span></span>

<span data-ttu-id="f7939-395">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-395">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-396">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-396">Preemption Possible</span></span>

<span data-ttu-id="f7939-397">No</span><span class="sxs-lookup"><span data-stu-id="f7939-397">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-398">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-398">Example</span></span>

```C
TX_BLOCK_POOL my_pool;
UINT          status;

/* Ensure that the highest priority thread will receive
   the next free block in this pool. */
status = tx_block_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_block_release call will wake up this thread. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-399">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-399">See Also</span></span>

- <span data-ttu-id="f7939-400">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-400">tx_block_allocate</span></span>
- <span data-ttu-id="f7939-401">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-401">tx_block_pool_create</span></span>
- <span data-ttu-id="f7939-402">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-402">tx_block_pool_delete</span></span>
- <span data-ttu-id="f7939-403">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-403">tx_block_pool_info_get</span></span>
- <span data-ttu-id="f7939-404">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-404">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-405">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-405">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-406">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="f7939-406">tx_block_release</span></span>

## <a name="tx_block_release"></a><span data-ttu-id="f7939-407">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="f7939-407">tx_block_release</span></span>

<span data-ttu-id="f7939-408">Rilasciare un blocco di memoria di dimensioni fisse</span><span class="sxs-lookup"><span data-stu-id="f7939-408">Release fixed-size block of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-409">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-409">Prototype</span></span>

```C
UINT tx_block_release(VOID *block_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-410">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-410">Description</span></span>

<span data-ttu-id="f7939-411">Questo servizio rilascia un blocco precedentemente allocato al pool di memoria associato.</span><span class="sxs-lookup"><span data-stu-id="f7939-411">This service releases a previously allocated block back to its associated memory pool.</span></span> <span data-ttu-id="f7939-412">Se uno o più thread sono sospesi in attesa di blocchi di memoria da questo pool, il primo thread sospeso riceve questo blocco di memoria e riprende.</span><span class="sxs-lookup"><span data-stu-id="f7939-412">If there are one or more threads suspended waiting for memory blocks from this pool, the first thread suspended is given this memory block and resumed.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-413">L'applicazione deve impedire l'uso di un'area del blocco di memoria dopo che è stata rilasciata nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-413">The application must prevent using a memory block area after it has been released back to the pool.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-414">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-414">Parameters</span></span>

- <span data-ttu-id="f7939-415">**block_ptr**: puntatore al blocco di memoria allocato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-415">**block_ptr**: Pointer to the previously allocated memory block.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-416">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-416">Return Values</span></span>

- <span data-ttu-id="f7939-417">**TX_SUCCESS**: (0x00) rilascio del blocco di memoria riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-417">**TX_SUCCESS**: (0x00) Successful memory block release.</span></span>
- <span data-ttu-id="f7939-418">TX_PTR_ERROR: (0x03) puntatore al blocco di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-418">TX_PTR_ERROR: (0x03) Invalid pointer to memory block.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-419">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-419">Allowed From</span></span>

<span data-ttu-id="f7939-420">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-420">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-421">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-421">Preemption Possible</span></span>

<span data-ttu-id="f7939-422">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-422">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-423">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-423">Example</span></span>

```C
TX_BLOCK_POOLmy_pool;
unsigned char*memory_ptr;
UINT         status;

/* Release a memory block back to my_pool. Assume that the
   pool has been created and the memory block has been
   allocated. */
status = tx_block_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the block of memory pointed
   to by memory_ptr has been returned to the pool. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-424">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-424">See Also</span></span>

- <span data-ttu-id="f7939-425">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-425">tx_block_allocate</span></span>
- <span data-ttu-id="f7939-426">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-426">tx_block_pool_create</span></span>
- <span data-ttu-id="f7939-427">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-427">tx_block_pool_delete</span></span>
- <span data-ttu-id="f7939-428">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-428">tx_block_pool_info_get</span></span>
- <span data-ttu-id="f7939-429">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-429">tx_block_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-430">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-430">tx_block_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-431">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-431">tx_block_pool_prioritize</span></span>

## <a name="tx_byte_allocate"></a><span data-ttu-id="f7939-432">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-432">tx_byte_allocate</span></span>

<span data-ttu-id="f7939-433">Alloca byte di memoria</span><span class="sxs-lookup"><span data-stu-id="f7939-433">Allocate bytes of memory</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-434">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-434">Prototype</span></span>

```C
UINT tx_byte_allocate(TX_BYTE_POOL *pool_ptr,
                          VOID **memory_ptr, ULONG memory_size,
                          ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="f7939-435">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-435">Description</span></span>

<span data-ttu-id="f7939-436">Questo servizio alloca il numero specificato di byte dal pool di byte di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-436">This service allocates the specified number of bytes from the specified memory byte pool.</span></span>

> [!WARNING]
> <span data-ttu-id="f7939-437">È importante assicurarsi che il codice dell'applicazione non scriva al di fuori del blocco di memoria allocato.</span><span class="sxs-lookup"><span data-stu-id="f7939-437">It is important to ensure application code does not write outside the allocated memory block.</span></span> <span data-ttu-id="f7939-438">In tal caso, il danneggiamento si verifica in un blocco di memoria adiacente, in genere successivo.</span><span class="sxs-lookup"><span data-stu-id="f7939-438">If this happens, corruption occurs in an adjacent (usually subsequent) memory block.</span></span> <span data-ttu-id="f7939-439">I risultati sono imprevedibili e spesso sono irreversibili.</span><span class="sxs-lookup"><span data-stu-id="f7939-439">The results are unpredictable and are often fatal!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-440">Le prestazioni di questo servizio sono una funzione delle dimensioni del blocco e la quantità di frammentazione nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-440">The performance of this service is a function of the block size and the amount of fragmentation in the pool.</span></span> <span data-ttu-id="f7939-441">Questo servizio non deve pertanto essere utilizzato durante i thread di esecuzione critici per il tempo.</span><span class="sxs-lookup"><span data-stu-id="f7939-441">Hence, this service should not be used during time-critical threads of execution.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-442">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-442">Parameters</span></span>

- <span data-ttu-id="f7939-443">**pool_ptr**: puntatore a un pool di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-443">**pool_ptr**: Pointer to a previously created memory pool.</span></span>
- <span data-ttu-id="f7939-444">**memory_ptr**: puntatore a un puntatore di memoria di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-444">**memory_ptr**: Pointer to a destination memory pointer.</span></span> <span data-ttu-id="f7939-445">Al completamento dell'allocazione, l'indirizzo dell'area di memoria allocata viene inserito a cui punta il parametro.</span><span class="sxs-lookup"><span data-stu-id="f7939-445">On successful allocation, the address of the allocated memory area is placed where this parameter points to.</span></span>
- <span data-ttu-id="f7939-446">**memory_size**: numero di byte richiesti.</span><span class="sxs-lookup"><span data-stu-id="f7939-446">**memory_size**: Number of bytes requested.</span></span>
- <span data-ttu-id="f7939-447">**WAIT_OPTION**: definisce il comportamento del servizio se la memoria disponibile non è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="f7939-447">**wait_option**: Defines how the service behaves if there is not enough memory available.</span></span> <span data-ttu-id="f7939-448">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="f7939-448">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="f7939-449">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="f7939-449">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="f7939-450">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="f7939-450">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="f7939-451">valore di timeout: (0x00000001 tramite 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="f7939-451">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="f7939-452">La selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="f7939-452">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="f7939-453">*Questa è l'unica opzione valida se il servizio viene chiamato dall'inizializzazione.*</span><span class="sxs-lookup"><span data-stu-id="f7939-453">*This is the only valid option if the service is called from initialization.*</span></span>

    <span data-ttu-id="f7939-454">Se si seleziona TX_WAIT_FOREVER, il thread chiamante sospenderà per un tempo illimitato fino a quando non sarà disponibile memoria sufficiente.</span><span class="sxs-lookup"><span data-stu-id="f7939-454">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until enough memory is available.</span></span>

    <span data-ttu-id="f7939-455">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-455">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the memory.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-456">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-456">Return Values</span></span>

- <span data-ttu-id="f7939-457">**TX_SUCCESS**: (0x00) l'allocazione di memoria è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-457">**TX_SUCCESS**: (0x00) Successful memory allocation.</span></span>
- <span data-ttu-id="f7939-458">**TX_DELETED**: il pool di memoria (0x01) è stato eliminato durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-458">**TX_DELETED**: (0x01) Memory pool was deleted while thread was suspended.</span></span>
- <span data-ttu-id="f7939-459">**TX_NO_MEMORY**: il servizio (0x10) non è stato in grado di allocare la memoria entro il tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-459">**TX_NO_MEMORY**: (0x10) Service was unable to allocate the memory within the specified time to wait.</span></span>
- <span data-ttu-id="f7939-460">**TX_WAIT_ABORTED**: la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-460">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="f7939-461">TX_POOL_ERROR: (0x02) puntatore al pool di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-461">TX_POOL_ERROR: (0x02) Invalid memory pool pointer.</span></span>
- <span data-ttu-id="f7939-462">TX_PTR_ERROR: (0x03) puntatore non valido al puntatore di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-462">TX_PTR_ERROR: (0x03) Invalid pointer to destination pointer.</span></span>
- <span data-ttu-id="f7939-463">TX_SIZE_ERROR: (0X05) la dimensione richiesta è zero o maggiore del pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-463">TX_SIZE_ERROR: (0X05) Requested size is zero or larger than the pool.</span></span>
- <span data-ttu-id="f7939-464">TX_WAIT_ERROR: (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-464">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="f7939-465">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-465">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-466">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-466">Allowed From</span></span>

<span data-ttu-id="f7939-467">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="f7939-467">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-468">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-468">Preemption Possible</span></span>

<span data-ttu-id="f7939-469">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-469">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-470">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-470">Example</span></span>

```C
TX_BYTE_POOL my_pool;
unsigned char*memory_ptr;
UINT         status;

/* Allocate a 112 byte memory area from my_pool. Assume
   that the pool has already been created with a call to
   tx_byte_pool_create. */
status =  tx_byte_allocate(&my_pool, (VOID **) &memory_ptr,
                       112, TX_NO_WAIT);

/* If status equals TX_SUCCESS, memory_ptr contains the
   address of the allocated memory area. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-471">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-471">See Also</span></span>

- <span data-ttu-id="f7939-472">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-472">tx_byte_pool_create</span></span>
- <span data-ttu-id="f7939-473">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-473">tx_byte_pool_delete</span></span>
- <span data-ttu-id="f7939-474">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-474">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="f7939-475">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-475">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-476">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-476">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-477">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-477">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="f7939-478">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="f7939-478">tx_byte_release</span></span>

## <a name="tx_byte_pool_create"></a><span data-ttu-id="f7939-479">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-479">tx_byte_pool_create</span></span>

<span data-ttu-id="f7939-480">Crea pool di memoria di byte</span><span class="sxs-lookup"><span data-stu-id="f7939-480">Create memory pool of bytes</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-481">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-481">Prototype</span></span>

```C
UINT tx_byte_pool_create(TX_BYTE_POOL *pool_ptr,
                          CHAR *name_ptr, VOID *pool_start,
                          ULONG pool_size);
```
### <a name="description"></a><span data-ttu-id="f7939-482">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-482">Description</span></span>

<span data-ttu-id="f7939-483">Questo servizio crea un pool di byte di memoria nell'area specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-483">This service creates a memory byte pool in the area specified.</span></span> <span data-ttu-id="f7939-484">Inizialmente il pool è costituito fondamentalmente da un blocco libero di dimensioni molto grandi.</span><span class="sxs-lookup"><span data-stu-id="f7939-484">Initially the pool consists of basically one very large free block.</span></span> <span data-ttu-id="f7939-485">Tuttavia, il pool viene suddiviso in blocchi più piccoli quando vengono apportate allocazioni.</span><span class="sxs-lookup"><span data-stu-id="f7939-485">However, the pool is broken into smaller blocks as allocations are made.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-486">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-486">Parameters</span></span>

- <span data-ttu-id="f7939-487">**pool_ptr**: puntatore a un blocco di controllo del pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-487">**pool_ptr**: Pointer to a memory pool control block.</span></span>
- <span data-ttu-id="f7939-488">**name_ptr**: puntatore al nome del pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-488">**name_ptr**: Pointer to the name of the memory pool.</span></span>
- <span data-ttu-id="f7939-489">**pool_start**: indirizzo iniziale del pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-489">**pool_start**: Starting address of the memory pool.</span></span> <span data-ttu-id="f7939-490">L'indirizzo iniziale deve essere allineato alle dimensioni del tipo di dati ULONG.</span><span class="sxs-lookup"><span data-stu-id="f7939-490">The starting address must be aligned to the size of the ULONG data type.</span></span>
- <span data-ttu-id="f7939-491">**pool_size**: numero totale di byte disponibili per il pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-491">**pool_size**: Total number of bytes available for the memory pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-492">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-492">Return Values</span></span>

- <span data-ttu-id="f7939-493">**TX_SUCCESS**: (0x00) la creazione del pool di memoria è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-493">**TX_SUCCESS**: (0x00) Successful memory pool creation.</span></span>
- <span data-ttu-id="f7939-494">TX_POOL_ERROR: (0x02) puntatore al pool di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-494">TX_POOL_ERROR: (0x02) Invalid memory pool pointer.</span></span> <span data-ttu-id="f7939-495">Il puntatore è NULL o il pool è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="f7939-495">Either the pointer is NULL or the pool is already created.</span></span>
- <span data-ttu-id="f7939-496">TX_PTR_ERROR: (0x03) indirizzo iniziale non valido del pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-496">TX_PTR_ERROR: (0x03) Invalid starting address of the pool.</span></span>
- <span data-ttu-id="f7939-497">TX_SIZE_ERROR: le dimensioni del pool (0x05) non sono valide.</span><span class="sxs-lookup"><span data-stu-id="f7939-497">TX_SIZE_ERROR: (0x05) Size of pool is invalid.</span></span>
- <span data-ttu-id="f7939-498">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-498">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-499">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-499">Allowed From</span></span>

<span data-ttu-id="f7939-500">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="f7939-500">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-501">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-501">Preemption Possible</span></span>

<span data-ttu-id="f7939-502">No</span><span class="sxs-lookup"><span data-stu-id="f7939-502">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-503">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-503">Example</span></span>

```C
TX_BYTE_POOL my_pool;
UINT         status;

/* Create a memory pool whose total size is 2000 bytes
   starting at address 0x500000. */
status =  tx_byte_pool_create(&my_pool, "my_pool_name",
             (VOID *) 0x500000, 2000);

/* If status equals TX_SUCCESS, my_pool is available for
   allocating memory. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-504">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-504">See Also</span></span>

- <span data-ttu-id="f7939-505">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-505">tx_byte_allocate</span></span>
- <span data-ttu-id="f7939-506">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-506">tx_byte_pool_delete</span></span>
- <span data-ttu-id="f7939-507">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-507">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="f7939-508">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-508">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-509">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-509">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-510">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-510">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="f7939-511">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="f7939-511">tx_byte_release</span></span>

## <a name="tx_byte_pool_delete"></a><span data-ttu-id="f7939-512">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-512">tx_byte_pool_delete</span></span>

<span data-ttu-id="f7939-513">Elimina pool di byte di memoria</span><span class="sxs-lookup"><span data-stu-id="f7939-513">Delete memory byte pool</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-514">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-514">Prototype</span></span>

```C
UINT tx_byte_pool_delete(TX_BYTE_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-515">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-515">Description</span></span>

<span data-ttu-id="f7939-516">Questo servizio Elimina il pool di byte di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-516">This service deletes the specified memory byte pool.</span></span> <span data-ttu-id="f7939-517">Tutti i thread sospesi in attesa di memoria da questo pool vengono ripresi e viene fornito un TX_DELETED stato restituito.</span><span class="sxs-lookup"><span data-stu-id="f7939-517">All threads suspended waiting for memory from this pool are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-518">È responsabilità dell'applicazione gestire l'area di memoria associata al pool, disponibile al termine del servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-518">It is the application’s responsibility to manage the memory area associated with the pool, which is available after this service completes.</span></span> <span data-ttu-id="f7939-519">Inoltre, l'applicazione deve impedire l'uso di un pool eliminato o di una memoria precedentemente allocata.</span><span class="sxs-lookup"><span data-stu-id="f7939-519">In addition, the application must prevent use of a deleted pool or memory previously allocated from it.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-520">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-520">Parameters</span></span> 

- <span data-ttu-id="f7939-521">**pool_ptr**: puntatore a un pool di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-521">**pool_ptr**: Pointer to a previously created memory pool.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-522">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-522">Return Values</span></span>

- <span data-ttu-id="f7939-523">**TX_SUCCESS**: (0x00) eliminazione del pool di memoria riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-523">**TX_SUCCESS**: (0x00) Successful memory pool deletion.</span></span>
- <span data-ttu-id="f7939-524">TX_POOL_ERROR: (0x02) puntatore al pool di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-524">TX_POOL_ERROR: (0x02) Invalid memory pool pointer.</span></span>
- <span data-ttu-id="f7939-525">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-525">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-526">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-526">Allowed From</span></span>

<span data-ttu-id="f7939-527">Thread</span><span class="sxs-lookup"><span data-stu-id="f7939-527">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-528">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-528">Preemption Possible</span></span>

<span data-ttu-id="f7939-529">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-529">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-530">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-530">Example</span></span>

```C
TX_BYTE_POOL my_pool;
UINT         status;

/* Delete entire memory pool. Assume that the pool has already
   been created with a call to tx_byte_pool_create. */
status =   tx_byte_pool_delete(&my_pool);

/* If status equals TX_SUCCESS, memory pool is deleted. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-531">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-531">See Also</span></span>

- <span data-ttu-id="f7939-532">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-532">tx_byte_allocate</span></span>
- <span data-ttu-id="f7939-533">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-533">tx_byte_pool_create</span></span>
- <span data-ttu-id="f7939-534">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-534">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="f7939-535">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-535">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-536">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-536">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-537">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-537">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="f7939-538">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="f7939-538">tx_byte_release</span></span>

## <a name="tx_byte_pool_info_get"></a><span data-ttu-id="f7939-539">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-539">tx_byte_pool_info_get</span></span>

<span data-ttu-id="f7939-540">Recuperare informazioni sul pool di byte</span><span class="sxs-lookup"><span data-stu-id="f7939-540">Retrieve information about byte pool</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-541">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-541">Prototype</span></span>

```C
UINT tx_byte_pool_info_get(TX_BYTE_POOL *pool_ptr, CHAR **name,
                          ULONG *available, ULONG *fragments,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count,
                          TX_BYTE_POOL **next_pool);
```
### <a name="description"></a><span data-ttu-id="f7939-542">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-542">Description</span></span>

<span data-ttu-id="f7939-543">Questo servizio recupera le informazioni sul pool di byte di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-543">This service retrieves information about the specified memory byte pool.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-544">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-544">Parameters</span></span>

- <span data-ttu-id="f7939-545">**pool_ptr**: puntatore al pool di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-545">**pool_ptr**: Pointer to previously created memory pool.</span></span>
- <span data-ttu-id="f7939-546">**Name**: puntatore alla destinazione per il puntatore al nome del pool di byte.</span><span class="sxs-lookup"><span data-stu-id="f7939-546">**name**: Pointer to destination for the pointer to the byte pool’s name.</span></span>
- <span data-ttu-id="f7939-547">**available**: puntatore alla destinazione per il numero di byte disponibili nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-547">**available**: Pointer to destination for the number of available bytes in the pool.</span></span>
- <span data-ttu-id="f7939-548">**Fragments**: puntatore alla destinazione per il numero totale di frammenti di memoria nel pool di byte.</span><span class="sxs-lookup"><span data-stu-id="f7939-548">**fragments**: Pointer to destination for the total number of memory fragments in the byte pool.</span></span>
- <span data-ttu-id="f7939-549">**first_suspended**: puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione del pool di byte.</span><span class="sxs-lookup"><span data-stu-id="f7939-549">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this byte pool.</span></span>
- <span data-ttu-id="f7939-550">**suspended_count**: puntatore alla destinazione per il numero di thread attualmente sospesi in questo pool di byte.</span><span class="sxs-lookup"><span data-stu-id="f7939-550">**suspended_count**: Pointer to destination for the number of threads currently suspended on this byte pool.</span></span>
- <span data-ttu-id="f7939-551">**next_pool**: puntatore alla destinazione per il puntatore del pool di byte creato successivamente.</span><span class="sxs-lookup"><span data-stu-id="f7939-551">**next_pool**: Pointer to destination for the pointer of the next created byte pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-552">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-552">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-553">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-553">Return Values</span></span>

- <span data-ttu-id="f7939-554">**TX_SUCCESS**: (0x00) il recupero delle informazioni sul pool è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-554">**TX_SUCCESS**: (0x00) Successful pool information retrieve.</span></span>
- <span data-ttu-id="f7939-555">TX_POOL_ERROR: (0x02) puntatore al pool di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-555">TX_POOL_ERROR: (0x02) Invalid memory pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-556">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-556">Allowed From</span></span>

<span data-ttu-id="f7939-557">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-557">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-558">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-558">Preemption Possible</span></span>

<span data-ttu-id="f7939-559">No</span><span class="sxs-lookup"><span data-stu-id="f7939-559">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-560">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-560">Example</span></span>

```C
TX_BYTE_POOL my_pool;
CHAR         *name;
ULONG        available;
ULONG        fragments;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_BYTE_POOL *next_pool;
UINT         status;

/* Retrieve information about the previously created
   block pool "my_pool." */
status =  tx_byte_pool_info_get(&my_pool, &name,
             &available, &fragments,
             &first_suspended, &suspended_count,
             &next_pool);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-561">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-561">See Also</span></span>

- <span data-ttu-id="f7939-562">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-562">tx_byte_allocate</span></span>
- <span data-ttu-id="f7939-563">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-563">tx_byte_pool_create</span></span>
- <span data-ttu-id="f7939-564">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-564">tx_byte_pool_delete</span></span>
- <span data-ttu-id="f7939-565">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-565">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-566">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-566">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-567">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-567">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="f7939-568">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="f7939-568">tx_byte_release</span></span>

## <a name="tx_byte_pool_performance_info_get"></a><span data-ttu-id="f7939-569">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-569">tx_byte_pool_performance_info_get</span></span>

<span data-ttu-id="f7939-570">Ottenere informazioni sulle prestazioni del pool di byte</span><span class="sxs-lookup"><span data-stu-id="f7939-570">Get byte pool performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-571">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-571">Prototype</span></span>

```C
UINT tx_byte_pool_performance_info_get(TX_BYTE_POOL *pool_ptr,
        ULONG *allocates, ULONG *releases,
        ULONG *fragments_searched, ULONG *merges, ULONG *splits,
        ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="f7939-572">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-572">Description</span></span>

<span data-ttu-id="f7939-573">Questo servizio recupera le informazioni sulle prestazioni relative al pool di byte di memoria specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-573">This service retrieves performance information about the specified memory byte pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-574">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-574">The ThreadX SMP library and application must be built with **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-575">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-575">Parameters</span></span>

- <span data-ttu-id="f7939-576">**pool_ptr**: puntatore al pool di byte di memoria creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-576">**pool_ptr**: Pointer to previously created memory byte pool.</span></span>
- <span data-ttu-id="f7939-577">**alloca**: puntatore alla destinazione per il numero di richieste di allocazione eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-577">**allocates**: Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="f7939-578">**versioni**: puntatore alla destinazione per il numero di richieste di versione eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-578">**releases**: Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="f7939-579">**fragments_searched**: puntatore alla destinazione per il numero di frammenti di memoria interni cercati durante le richieste di allocazione nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-579">**fragments_searched**: Pointer to destination for the number of internal memory fragments searched during allocation requests on this pool.</span></span>
- <span data-ttu-id="f7939-580">**unisce**: puntatore alla destinazione per il numero di blocchi di memoria interni Uniti durante le richieste di allocazione nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-580">**merges**: Pointer to destination for the number of internal memory blocks merged during allocation requests on this pool.</span></span>
- <span data-ttu-id="f7939-581">**Split**: puntatore alla destinazione per il numero di blocchi di memoria interni suddivisi (frammenti) creati durante le richieste di allocazione nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-581">**splits**: Pointer to destination for the number of internal memory blocks split (fragments) created during allocation requests on this pool.</span></span>
- <span data-ttu-id="f7939-582">**sospensioni**: puntatore alla destinazione per il numero di sospensioni di allocazione di thread nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-582">**suspensions**: Pointer to destination for the number of thread allocation suspensions on this pool.</span></span>
- <span data-ttu-id="f7939-583">**timeout**: puntatore alla destinazione per il numero di timeout di allocazione della sospensione nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-583">**timeouts**: Pointer to destination for the number of allocate suspension timeouts on this pool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-584">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-584">Supplying a TX_NULL for any parameter indicates the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-585">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-585">Return Values</span></span>

- <span data-ttu-id="f7939-586">TX_SUCCESS: (0x00) prestazioni del pool di byte riuscite.</span><span class="sxs-lookup"><span data-stu-id="f7939-586">TX_SUCCESS: (0x00) Successful byte pool performance get.</span></span>
- <span data-ttu-id="f7939-587">**TX_PTR_ERROR**: (0x03) puntatore al pool di byte non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-587">**TX_PTR_ERROR**: (0x03) Invalid byte pool pointer.</span></span>
- <span data-ttu-id="f7939-588">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-588">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-589">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-589">Allowed From</span></span>

<span data-ttu-id="f7939-590">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-590">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-591">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-591">Example</span></span>

```C
TX_BYTE_POOL     my_pool;
ULONG            fragments_searched;
ULONG            merges;
ULONG            splits;
ULONG            allocates;
ULONG            releases;
ULONG            suspensions;
ULONG            timeouts;

/* Retrieve performance information on the previously created byte
   pool.  */
status =  tx_byte_pool_performance_info_get(&my_pool,
                &fragments_searched,
                &merges, &splits,
                &allocates, &releases,
                      &suspensions,&timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-592">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-592">See Also</span></span>

- <span data-ttu-id="f7939-593">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-593">tx_byte_allocate</span></span>
- <span data-ttu-id="f7939-594">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-594">tx_byte_pool_create</span></span>
- <span data-ttu-id="f7939-595">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-595">tx_byte_pool_delete</span></span>
- <span data-ttu-id="f7939-596">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-596">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="f7939-597">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-597">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-598">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-598">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="f7939-599">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="f7939-599">tx_byte_release</span></span>

## <a name="tx_byte_pool_performance_system_info_get"></a><span data-ttu-id="f7939-600">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-600">tx_byte_pool_performance_system_info_get</span></span>

<span data-ttu-id="f7939-601">Ottenere informazioni sulle prestazioni del sistema del pool di byte</span><span class="sxs-lookup"><span data-stu-id="f7939-601">Get byte pool system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-602">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-602">Prototype</span></span>

```C
UINT  tx_byte_pool_performance_system_info_get(ULONG *allocates,
        ULONG *releases, ULONG *fragments_searched, ULONG *merges,
        ULONG *splits, ULONG *suspensions, ULONG *timeouts);;
```
### <a name="description"></a><span data-ttu-id="f7939-603">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-603">Description</span></span>

<span data-ttu-id="f7939-604">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i pool di byte di memoria nel sistema.</span><span class="sxs-lookup"><span data-stu-id="f7939-604">This service retrieves performance information about all memory byte pools in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-605">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-605">The ThreadX SMP library and application must be built with **TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-606">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-606">Parameters</span></span>

- <span data-ttu-id="f7939-607">**alloca**: puntatore alla destinazione per il numero di richieste di allocazione eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-607">**allocates**: Pointer to destination for the number of allocate requests performed on this pool.</span></span>
- <span data-ttu-id="f7939-608">**versioni**: puntatore alla destinazione per il numero di richieste di versione eseguite nel pool.</span><span class="sxs-lookup"><span data-stu-id="f7939-608">**releases**: Pointer to destination for the number of release requests performed on this pool.</span></span>
- <span data-ttu-id="f7939-609">**fragments_searched**: puntatore alla destinazione per il numero totale di frammenti di memoria interni cercati durante le richieste di allocazione su tutti i pool di byte.</span><span class="sxs-lookup"><span data-stu-id="f7939-609">**fragments_searched**: Pointer to destination for the total number of internal memory fragments searched during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="f7939-610">**unisce**: puntatore alla destinazione per il numero totale di blocchi di memoria interni Uniti durante le richieste di allocazione in tutti i pool di byte.</span><span class="sxs-lookup"><span data-stu-id="f7939-610">**merges**: Pointer to destination for the total number of internal memory blocks merged during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="f7939-611">**Split**: puntatore alla destinazione per il numero totale di blocchi di memoria interni suddivisi (frammenti) creati durante le richieste di allocazione su tutti i pool di byte.</span><span class="sxs-lookup"><span data-stu-id="f7939-611">**splits**: Pointer to destination for the total number of internal memory blocks split (fragments) created during allocation requests on all byte pools.</span></span>
- <span data-ttu-id="f7939-612">**sospensioni**: puntatore alla destinazione per il numero totale di sospensioni di allocazione di thread in tutti i pool di byte.</span><span class="sxs-lookup"><span data-stu-id="f7939-612">**suspensions**: Pointer to destination for the total number of thread allocation suspensions on all byte pools.</span></span>
- <span data-ttu-id="f7939-613">**timeout**: puntatore alla destinazione per il numero totale di timeout di allocazione della sospensione in tutti i pool di byte.</span><span class="sxs-lookup"><span data-stu-id="f7939-613">**timeouts**: Pointer to destination for the total number of allocate suspension timeouts on all byte pools.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-614">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-614">Supplying a TX_NULL for any parameter indicates the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-615">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-615">Return Values</span></span>

- <span data-ttu-id="f7939-616">**TX_SUCCESS**: (0x00) prestazioni del pool di byte riuscite.</span><span class="sxs-lookup"><span data-stu-id="f7939-616">**TX_SUCCESS**: (0x00) Successful byte pool performance get.</span></span>
- <span data-ttu-id="f7939-617">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-617">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-618">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-618">Allowed From</span></span>

<span data-ttu-id="f7939-619">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-619">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-620">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-620">Example</span></span>

```C
ULONG         fragments_searched;
ULONG         merges;
ULONG         splits;
ULONG         allocates;
ULONG         releases;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all byte pools in the
   system. */
status =
tx_byte_pool_performance_system_info_get(&fragments_searched,
                &merges, &splits, &allocates, &releases,
                &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-621">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-621">See Also</span></span>

- <span data-ttu-id="f7939-622">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-622">tx_byte_allocate</span></span>
- <span data-ttu-id="f7939-623">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-623">tx_byte_pool_create</span></span>
- <span data-ttu-id="f7939-624">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-624">tx_byte_pool_delete</span></span>
- <span data-ttu-id="f7939-625">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-625">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="f7939-626">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-626">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-627">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-627">tx_byte_pool_prioritize</span></span>
- <span data-ttu-id="f7939-628">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="f7939-628">tx_byte_release</span></span>

## <a name="tx_byte_pool_prioritize"></a><span data-ttu-id="f7939-629">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-629">tx_byte_pool_prioritize</span></span>

<span data-ttu-id="f7939-630">Priorità elenco di sospensioni del pool di byte</span><span class="sxs-lookup"><span data-stu-id="f7939-630">Prioritize byte pool suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-631">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-631">Prototype</span></span>

```c
UINT tx_byte_pool_prioritize(TX_BYTE_POOL *pool_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-632">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-632">Description</span></span>

<span data-ttu-id="f7939-633">Questo servizio posiziona il thread con priorità più elevata sospeso per la memoria nel pool all'inizio dell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="f7939-633">This service places the highest priority thread suspended for memory on this pool at the front of the suspension list.</span></span> <span data-ttu-id="f7939-634">Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.</span><span class="sxs-lookup"><span data-stu-id="f7939-634">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-635">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-635">Parameters</span></span> 

- <span data-ttu-id="f7939-636">**pool_ptr**: puntatore a un blocco di controllo del pool di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-636">**pool_ptr**: Pointer to a memory pool control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-637">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-637">Return Values</span></span>

- <span data-ttu-id="f7939-638">**TX_SUCCESS**: (0x00) priorità del pool di memoria riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-638">**TX_SUCCESS**: (0x00) Successful memory pool prioritize.</span></span>
- <span data-ttu-id="f7939-639">TX_POOL_ERROR: (0x02) puntatore al pool di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-639">TX_POOL_ERROR: (0x02) Invalid memory pool pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-640">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-640">Allowed From</span></span>

<span data-ttu-id="f7939-641">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-641">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-642">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-642">Preemption Possible</span></span>

<span data-ttu-id="f7939-643">No</span><span class="sxs-lookup"><span data-stu-id="f7939-643">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-644">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-644">Example</span></span>

```c
TX_BYTE_POOL my_pool;
UINT         status;

/* Ensure that the highest priority thread will receive
   the next free memory from this pool. */
status = tx_byte_pool_prioritize(&my_pool);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_byte_release call will wake up this thread,
   if there is enough memory to satisfy its request. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-645">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-645">See Also</span></span>

- <span data-ttu-id="f7939-646">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-646">tx_byte_allocate</span></span>
- <span data-ttu-id="f7939-647">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-647">tx_byte_pool_create</span></span>
- <span data-ttu-id="f7939-648">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-648">tx_byte_pool_delete</span></span>
- <span data-ttu-id="f7939-649">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-649">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="f7939-650">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-650">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-651">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-651">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-652">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="f7939-652">tx_byte_release</span></span>

## <a name="tx_byte_release"></a><span data-ttu-id="f7939-653">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="f7939-653">tx_byte_release</span></span>

<span data-ttu-id="f7939-654">Byte di rilascio nel pool di memoria</span><span class="sxs-lookup"><span data-stu-id="f7939-654">Release bytes back to memory pool</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-655">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-655">Prototype</span></span>

```C
UINT tx_byte_release(VOID *memory_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-656">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-656">Description</span></span>

<span data-ttu-id="f7939-657">Questo servizio rilascia un'area di memoria precedentemente allocata al pool associato.</span><span class="sxs-lookup"><span data-stu-id="f7939-657">This service releases a previously allocated memory area back to its associated pool.</span></span> <span data-ttu-id="f7939-658">Se uno o più thread sono sospesi in attesa di memoria da questo pool, a ogni thread sospeso viene assegnata la memoria e ripresa fino a esaurimento della memoria o fino a quando non sono presenti altri thread sospesi.</span><span class="sxs-lookup"><span data-stu-id="f7939-658">If there are one or more threads suspended waiting for memory from this pool, each suspended thread is given memory and resumed until the memory is exhausted or until there are no more suspended threads.</span></span> <span data-ttu-id="f7939-659">Questo processo di allocazione della memoria ai thread sospesi inizia sempre con il primo thread sospeso.</span><span class="sxs-lookup"><span data-stu-id="f7939-659">This process of allocating memory to suspended threads always begins with the first thread suspended.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-660">L'applicazione deve impedire l'uso dell'area di memoria dopo che è stata rilasciata.</span><span class="sxs-lookup"><span data-stu-id="f7939-660">The application must prevent using the memory area after it is released.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-661">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-661">Parameters</span></span>

- <span data-ttu-id="f7939-662">**memory_ptr**: puntatore all'area di memoria allocata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-662">**memory_ptr**: Pointer to the previously allocated memory area.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-663">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-663">Return Values</span></span>

- <span data-ttu-id="f7939-664">**TX_SUCCESS**: (0x00) versione di memoria riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-664">**TX_SUCCESS**: (0x00) Successful memory release.</span></span>
- <span data-ttu-id="f7939-665">TX_PTR_ERROR: (0x03) puntatore all'area di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-665">TX_PTR_ERROR: (0x03) Invalid memory area pointer.</span></span>
- <span data-ttu-id="f7939-666">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-666">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-667">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-667">Allowed From</span></span>

<span data-ttu-id="f7939-668">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="f7939-668">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-669">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-669">Preemption Possible</span></span>

<span data-ttu-id="f7939-670">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-670">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-671">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-671">Example</span></span>

```C
unsigned char    *memory_ptr;
UINT             status;

/* Release a memory back to my_pool. Assume that the memory
   area was previously allocated from my_pool. */
status =  tx_byte_release((VOID *) memory_ptr);

/* If status equals TX_SUCCESS, the memory pointed to by
   memory_ptr has been returned to the pool. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-672">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-672">See Also</span></span>

- <span data-ttu-id="f7939-673">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="f7939-673">tx_byte_allocate</span></span>
- <span data-ttu-id="f7939-674">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="f7939-674">tx_byte_pool_create</span></span>
- <span data-ttu-id="f7939-675">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-675">tx_byte_pool_delete</span></span>
- <span data-ttu-id="f7939-676">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-676">tx_byte_pool_info_get</span></span>
- <span data-ttu-id="f7939-677">tx_byte_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-677">tx_byte_pool_performance_info_get</span></span>
- <span data-ttu-id="f7939-678">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-678">tx_byte_pool_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-679">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-679">tx_byte_pool_prioritize</span></span>

## <a name="tx_event_flags_create"></a><span data-ttu-id="f7939-680">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="f7939-680">tx_event_flags_create</span></span>

<span data-ttu-id="f7939-681">Crea gruppo di flag di evento</span><span class="sxs-lookup"><span data-stu-id="f7939-681">Create event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-682">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-682">Prototype</span></span>

```c
UINT tx_event_flags_create(TX_EVENT_FLAGS_GROUP *group_ptr,
                          CHAR *name_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-683">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-683">Description</span></span>

<span data-ttu-id="f7939-684">Questo servizio crea un gruppo di flag di evento 32.</span><span class="sxs-lookup"><span data-stu-id="f7939-684">This service creates a group of 32 event flags.</span></span> <span data-ttu-id="f7939-685">Tutti i flag di evento 32 nel gruppo vengono inizializzati su zero.</span><span class="sxs-lookup"><span data-stu-id="f7939-685">All 32 event flags in the group are initialized to zero.</span></span> <span data-ttu-id="f7939-686">Ogni flag di evento è rappresentato da un solo bit.</span><span class="sxs-lookup"><span data-stu-id="f7939-686">Each event flag is represented by a single bit.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-687">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-687">Parameters</span></span>

- <span data-ttu-id="f7939-688">**group_ptr**: puntatore a un blocco di controllo del gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="f7939-688">**group_ptr**: Pointer to an event flags group control block.</span></span> 
- <span data-ttu-id="f7939-689">**name_ptr**: puntatore al nome del gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="f7939-689">**name_ptr**: Pointer to the name of the event flags group.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-690">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-690">Return Values</span></span>

- <span data-ttu-id="f7939-691">**TX_SUCCESS**: (0x00) la creazione del gruppo di eventi è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-691">**TX_SUCCESS**: (0x00) Successful event group creation.</span></span>
- <span data-ttu-id="f7939-692">TX_GROUP_ERROR: (0x06) puntatore al gruppo di eventi non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-692">TX_GROUP_ERROR: (0x06) Invalid event group pointer.</span></span> <span data-ttu-id="f7939-693">Il puntatore è NULL o il gruppo di eventi è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="f7939-693">Either the pointer is NULL or the event group is already created.</span></span>
- <span data-ttu-id="f7939-694">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-694">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-695">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-695">Allowed From</span></span>

<span data-ttu-id="f7939-696">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="f7939-696">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-697">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-697">Preemption Possible</span></span>

<span data-ttu-id="f7939-698">No</span><span class="sxs-lookup"><span data-stu-id="f7939-698">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-699">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-699">Example</span></span>

```C
TX_EVENT_FLAGS_GROUP my_event_group;
UINT         status;

/* Create an event flags group. */
status = tx_event_flags_create(&my_event_group,
            "my_event_group_name");

/* If status equals TX_SUCCESS, my_event_group is ready
   for get and set services. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-700">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-700">See Also</span></span>

- <span data-ttu-id="f7939-701">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-701">tx_event_flags_delete</span></span>
- <span data-ttu-id="f7939-702">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="f7939-702">tx_event_flags_get</span></span>
- <span data-ttu-id="f7939-703">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-703">tx_event_flags_info_get</span></span>
- <span data-ttu-id="f7939-704">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-704">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="f7939-705">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-705">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-706">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="f7939-706">tx_event_flags_set</span></span>
- <span data-ttu-id="f7939-707">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-707">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_delete"></a><span data-ttu-id="f7939-708">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-708">tx_event_flags_delete</span></span>

<span data-ttu-id="f7939-709">Elimina gruppo di flag di evento</span><span class="sxs-lookup"><span data-stu-id="f7939-709">Delete event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-710">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-710">Prototype</span></span>

```c
UINT tx_event_flags_delete(TX_EVENT_FLAGS_GROUP *group_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-711">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-711">Description</span></span>

<span data-ttu-id="f7939-712">Questo servizio Elimina il gruppo di flag di evento specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-712">This service deletes the specified event flags group.</span></span> <span data-ttu-id="f7939-713">Tutti i thread sospesi in attesa degli eventi da questo gruppo vengono ripresi e viene fornito un TX_DELETED stato restituito.</span><span class="sxs-lookup"><span data-stu-id="f7939-713">All threads suspended waiting for events from this group are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-714">Prima di eliminare il gruppo di flag di evento, l'applicazione deve verificare che un callback di notifica per questo gruppo di flag di evento sia stato completato (o disabilitato).</span><span class="sxs-lookup"><span data-stu-id="f7939-714">The application must ensure that a set notify callback for this event flags group is completed (or disabled) before deleting the event flags group.</span></span> <span data-ttu-id="f7939-715">Inoltre, l'applicazione deve impedire l'uso futuro di un gruppo di flag di evento eliminati.</span><span class="sxs-lookup"><span data-stu-id="f7939-715">In addition, the application must prevent all future use of a deleted event flags group.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-716">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-716">Parameters</span></span> 

- <span data-ttu-id="f7939-717">**group_ptr**: puntatore a un gruppo di flag evento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-717">**group_ptr**: Pointer to a previously created event flags group.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-718">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-718">Return Values</span></span>

- <span data-ttu-id="f7939-719">**TX_SUCCESS**: (0x00) eliminazione del gruppo di flag di evento riusciti.</span><span class="sxs-lookup"><span data-stu-id="f7939-719">**TX_SUCCESS**: (0x00) Successful event flags group deletion.</span></span>
- <span data-ttu-id="f7939-720">TX_GROUP_ERROR: (0x06) puntatore al gruppo di flag evento non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-720">TX_GROUP_ERROR: (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="f7939-721">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-721">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-722">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-722">Allowed From</span></span>

<span data-ttu-id="f7939-723">Thread</span><span class="sxs-lookup"><span data-stu-id="f7939-723">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-724">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-724">Preemption Possible</span></span>

<span data-ttu-id="f7939-725">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-725">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-726">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-726">Example</span></span>

```C
TX_EVENT_FLAGS_GROUP my_event_flags_group;
UINT                 status;

/* Delete event flags group. Assume that the group has
   already been created with a call to
   tx_event_flags_create. */
status = tx_event_flags_delete(&my_event_flags_group);

/* If status equals TX_SUCCESS, the event flags group is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-727">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-727">See Also</span></span>

- <span data-ttu-id="f7939-728">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="f7939-728">tx_event_flags_create</span></span>
- <span data-ttu-id="f7939-729">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="f7939-729">tx_event_flags_get</span></span>
- <span data-ttu-id="f7939-730">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-730">tx_event_flags_info_get</span></span>
- <span data-ttu-id="f7939-731">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-731">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="f7939-732">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-732">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-733">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="f7939-733">tx_event_flags_set</span></span>
- <span data-ttu-id="f7939-734">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-734">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_get"></a><span data-ttu-id="f7939-735">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="f7939-735">tx_event_flags_get</span></span>

<span data-ttu-id="f7939-736">Ottenere i flag di evento dal gruppo di flag di evento</span><span class="sxs-lookup"><span data-stu-id="f7939-736">Get event flags from event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-737">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-737">Prototype</span></span>

```C
UINT tx_event_flags_get(TX_EVENT_FLAGS_GROUP *group_ptr,
                          ULONG requested_flags, UINT get_option,
                          ULONG *actual_flags_ptr, ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="f7939-738">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-738">Description</span></span>

<span data-ttu-id="f7939-739">Questo servizio recupera i flag di evento dal gruppo di flag di evento specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-739">This service retrieves event flags from the specified event flags group.</span></span> <span data-ttu-id="f7939-740">Ogni gruppo di flag di evento contiene 32 flag di evento.</span><span class="sxs-lookup"><span data-stu-id="f7939-740">Each event flags group contains 32 event flags.</span></span> <span data-ttu-id="f7939-741">Ogni flag è rappresentato da un solo bit.</span><span class="sxs-lookup"><span data-stu-id="f7939-741">Each flag is represented by a single bit.</span></span> <span data-ttu-id="f7939-742">Questo servizio può recuperare diverse combinazioni di flag di evento, come selezionate dai parametri di input.</span><span class="sxs-lookup"><span data-stu-id="f7939-742">This service can retrieve a variety of event flag combinations, as selected by the input parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-743">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-743">Parameters</span></span>

- <span data-ttu-id="f7939-744">**group_ptr**: puntatore a un gruppo di flag evento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-744">**group_ptr**: Pointer to a previously created event flags group.</span></span>
- <span data-ttu-id="f7939-745">**requested_flags**: variabile senza segno a 32 bit che rappresenta i flag di evento richiesti.</span><span class="sxs-lookup"><span data-stu-id="f7939-745">**requested_flags**: 32-bit unsigned variable that represents the requested event flags.</span></span>
- <span data-ttu-id="f7939-746">**get_Option**: specifica se sono necessari tutti i flag di evento richiesti o uno di essi.</span><span class="sxs-lookup"><span data-stu-id="f7939-746">**get_option**: Specifies whether all or any of the requested event flags are required.</span></span> <span data-ttu-id="f7939-747">Di seguito sono riportate le selezioni valide:</span><span class="sxs-lookup"><span data-stu-id="f7939-747">The following are valid selections:</span></span>
    - <span data-ttu-id="f7939-748">**TX_AND**: (0x02)</span><span class="sxs-lookup"><span data-stu-id="f7939-748">**TX_AND**: (0x02)</span></span>
    - <span data-ttu-id="f7939-749">**TX_AND_CLEAR**: (0x03)</span><span class="sxs-lookup"><span data-stu-id="f7939-749">**TX_AND_CLEAR**: (0x03)</span></span>
    - <span data-ttu-id="f7939-750">**TX_OR**: (0x00)</span><span class="sxs-lookup"><span data-stu-id="f7939-750">**TX_OR**: (0x00)</span></span>
    - <span data-ttu-id="f7939-751">**TX_OR_CLEAR**: (0x01)</span><span class="sxs-lookup"><span data-stu-id="f7939-751">**TX_OR_CLEAR**: (0x01)</span></span>

    <span data-ttu-id="f7939-752">Selezionando TX_AND o TX_AND_CLEAR si specifica che tutti i flag di evento devono essere presenti nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="f7939-752">Selecting TX_AND or TX_AND_CLEAR specifies that all event flags must be present in the group.</span></span> <span data-ttu-id="f7939-753">Selezionando TX_OR o TX_OR_CLEAR si specifica che qualsiasi flag di evento è soddisfacente.</span><span class="sxs-lookup"><span data-stu-id="f7939-753">Selecting TX_OR or TX_OR_CLEAR specifies that any event flag is satisfactory.</span></span> <span data-ttu-id="f7939-754">Se vengono specificati TX_AND_CLEAR o TX_OR_CLEAR, i flag di evento che soddisfano la richiesta vengono cancellati (impostati su zero).</span><span class="sxs-lookup"><span data-stu-id="f7939-754">Event flags that satisfy the request are cleared (set to zero) if TX_AND_CLEAR or TX_OR_CLEAR are specified.</span></span>

- <span data-ttu-id="f7939-755">**actual_flags_ptr**: puntatore alla destinazione in cui vengono inseriti i flag di evento recuperati.</span><span class="sxs-lookup"><span data-stu-id="f7939-755">**actual_flags_ptr**: Pointer to destination of where the retrieved event flags are placed.</span></span> <span data-ttu-id="f7939-756">Si noti che i flag effettivi ottenuti possono contenere flag non richiesti.</span><span class="sxs-lookup"><span data-stu-id="f7939-756">Note that the actual flags obtained may contain flags that were not requested.</span></span>
- <span data-ttu-id="f7939-757">**WAIT_OPTION**: definisce il comportamento del servizio se i flag di evento selezionati non sono impostati.</span><span class="sxs-lookup"><span data-stu-id="f7939-757">**wait_option**: Defines how the service behaves if the selected event flags are not set.</span></span> <span data-ttu-id="f7939-758">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="f7939-758">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="f7939-759">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="f7939-759">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="f7939-760">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="f7939-760">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="f7939-761">valore di timeout: (0x00000001 tramite 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="f7939-761">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="f7939-762">La selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="f7939-762">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="f7939-763">Questa è l'unica opzione valida se il servizio viene chiamato da un non thread. ad esempio, inizializzazione, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-763">This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.</span></span>

    <span data-ttu-id="f7939-764">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando non saranno disponibili i flag di evento.</span><span class="sxs-lookup"><span data-stu-id="f7939-764">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the event flags are available.</span></span>

    <span data-ttu-id="f7939-765">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa dei flag di evento.</span><span class="sxs-lookup"><span data-stu-id="f7939-765">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the event flags.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-766">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-766">Return Values</span></span>

- <span data-ttu-id="f7939-767">**TX_SUCCESS**: (0x00) flag evento riusciti Get.</span><span class="sxs-lookup"><span data-stu-id="f7939-767">**TX_SUCCESS**: (0x00) Successful event flags get.</span></span>
- <span data-ttu-id="f7939-768">**TX_DELETED**: il gruppo di flag di evento (0x01) è stato eliminato durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-768">**TX_DELETED**: (0x01) Event flags group was deleted while thread was suspended.</span></span>
- <span data-ttu-id="f7939-769">**TX_NO_EVENTS**: il servizio (0x07) non è riuscito a ottenere gli eventi specificati entro il tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-769">**TX_NO_EVENTS**: (0x07) Service was unable to get the specified events within the specified time to wait.</span></span>
- <span data-ttu-id="f7939-770">**TX_WAIT_ABORTED**: la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-770">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="f7939-771">TX_GROUP_ERROR: (0x06) puntatore al gruppo di flag evento non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-771">TX_GROUP_ERROR: (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="f7939-772">TX_PTR_ERROR: (0x03) puntatore non valido per i flag di evento effettivi.</span><span class="sxs-lookup"><span data-stu-id="f7939-772">TX_PTR_ERROR: (0x03) Invalid pointer for actual event flags.</span></span>
- <span data-ttu-id="f7939-773">TX_WAIT_ERROR: (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-773">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="f7939-774">TX_OPTION_ERROR: (0x08) è stato specificato un parametro Get-Option non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-774">TX_OPTION_ERROR: (0x08) Invalid get-option was specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-775">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-775">Allowed From</span></span>

<span data-ttu-id="f7939-776">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-776">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-777">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-777">Preemption Possible</span></span>

<span data-ttu-id="f7939-778">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-778">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-779">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-779">Example</span></span>

```C
TX_EVENT_FLAGS_GROUP my_event_flags_group;
ULONG         actual_events;
UINT          status;

/* Request that event flags 0, 4, and 8 are all set. Also,
   if they are set they should be cleared. If the event
   flags are not set, this service suspends for a maximum of
   20 timer-ticks. */
status = tx_event_flags_get(&my_event_flags_group, 0x111,
                      TX_AND_CLEAR, &actual_events, 20);

/* If status equals TX_SUCCESS, actual_events contains the
   actual events obtained. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-780">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-780">See Also</span></span>

- <span data-ttu-id="f7939-781">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="f7939-781">tx_event_flags_create</span></span>
- <span data-ttu-id="f7939-782">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-782">tx_event_flags_delete</span></span>
- <span data-ttu-id="f7939-783">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-783">tx_event_flags_info_get</span></span>
- <span data-ttu-id="f7939-784">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-784">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="f7939-785">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-785">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-786">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="f7939-786">tx_event_flags_set</span></span>
- <span data-ttu-id="f7939-787">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-787">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_info_get"></a><span data-ttu-id="f7939-788">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-788">tx_event_flags_info_get</span></span>

<span data-ttu-id="f7939-789">Recupera le informazioni sul gruppo di flag di evento</span><span class="sxs-lookup"><span data-stu-id="f7939-789">Retrieve information about event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-790">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-790">Prototype</span></span>

```C
UINT tx_event_flags_info_get(TX_EVENT_FLAGS_GROUP *group_ptr,
                         CHAR **name, ULONG *current_flags,
                         TX_THREAD **first_suspended,
                         ULONG *suspended_count,
                         TX_EVENT_FLAGS_GROUP **next_group);
```
### <a name="description"></a><span data-ttu-id="f7939-791">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-791">Description</span></span>

<span data-ttu-id="f7939-792">Questo servizio recupera le informazioni sul gruppo di flag di evento specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-792">This service retrieves information about the specified event flags group.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-793">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-793">Parameters</span></span>

- <span data-ttu-id="f7939-794">**group_ptr**: puntatore a un blocco di controllo del gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="f7939-794">**group_ptr**: Pointer to an event flags group control block.</span></span>
- <span data-ttu-id="f7939-795">**nome**: puntatore alla destinazione per il puntatore al nome del gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="f7939-795">**name**: Pointer to destination for the pointer to the event flags group’s name.</span></span>
- <span data-ttu-id="f7939-796">**current_flags**: puntatore alla destinazione per i flag del set corrente nel gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="f7939-796">**current_flags**: Pointer to destination for the current set flags in the event flags group.</span></span>
- <span data-ttu-id="f7939-797">**first_suspended**: puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione del gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="f7939-797">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this event flags group.</span></span>
- <span data-ttu-id="f7939-798">**suspended_count**: puntatore alla destinazione per il numero di thread attualmente sospesi in questo gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="f7939-798">**suspended_count**: Pointer to destination for the number of threads currently suspended on this event flags group.</span></span>
- <span data-ttu-id="f7939-799">**next_group**: puntatore alla destinazione per il puntatore del gruppo di flag di evento creato successivo.</span><span class="sxs-lookup"><span data-stu-id="f7939-799">**next_group**: Pointer to destination for the pointer of the next created event flags group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-800">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-800">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-801">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-801">Return Values</span></span>

- <span data-ttu-id="f7939-802">**TX_SUCCESS**: (0x00) il recupero delle informazioni sul gruppo di eventi è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-802">**TX_SUCCESS**: (0x00) Successful event group information retrieval.</span></span>
- <span data-ttu-id="f7939-803">TX_GROUP_ERROR: (0x06) puntatore al gruppo di eventi non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-803">TX_GROUP_ERROR: (0x06) Invalid event group pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-804">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-804">Allowed From</span></span>

<span data-ttu-id="f7939-805">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-805">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-806">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-806">Preemption Possible</span></span>

<span data-ttu-id="f7939-807">No</span><span class="sxs-lookup"><span data-stu-id="f7939-807">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-808">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-808">Example</span></span>

```c
TX_EVENT_FLAGS_GROUPmy_event_group;
CHAR          *name;
ULONG         current_flags;
TX_THREAD     *first_suspended;
ULONG         suspended_count;
TX_EVENT_FLAGS_GROUP*next_group;
UINT          status;

/* Retrieve information about the previously created
   event flags group "my_event_group." */
status =  tx_event_flags_info_get(&my_event_group, &name,
             &current_flags,
             &first_suspended, &suspended_count,
             &next_group);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-809">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-809">See Also</span></span>

- <span data-ttu-id="f7939-810">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="f7939-810">tx_event_flags_create</span></span>
- <span data-ttu-id="f7939-811">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-811">tx_event_flags_delete</span></span>
- <span data-ttu-id="f7939-812">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="f7939-812">tx_event_flags_get</span></span>
- <span data-ttu-id="f7939-813">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-813">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="f7939-814">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-814">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-815">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="f7939-815">tx_event_flags_set</span></span>
- <span data-ttu-id="f7939-816">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-816">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_performance-info_get"></a><span data-ttu-id="f7939-817">tx_event_flags_performance info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-817">tx_event_flags_performance info_get</span></span>

<span data-ttu-id="f7939-818">Ottenere le informazioni sulle prestazioni del gruppo flag evento</span><span class="sxs-lookup"><span data-stu-id="f7939-818">Get event flags group performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-819">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-819">Prototype</span></span>

```C
UINT tx_event_flags_performance_info_get(TX_EVENT_FLAGS_GROUP
                        *group_ptr, ULONG *sets, ULONG *gets,
                        ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="f7939-820">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-820">Description</span></span>

<span data-ttu-id="f7939-821">Questo servizio recupera le informazioni sulle prestazioni relative al gruppo di flag di evento specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-821">This service retrieves performance information about the specified event flags group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-822">Per restituire le informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-822">ThreadX SMP library and application must be built with **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-823">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-823">Parameters</span></span>

- <span data-ttu-id="f7939-824">**group_ptr**: puntatore al gruppo di flag evento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-824">**group_ptr**: Pointer to previously created event flags group.</span></span>
- <span data-ttu-id="f7939-825">**imposta**: puntatore alla destinazione per il numero di richieste set di flag di evento eseguite su questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="f7939-825">**sets**: Pointer to destination for the number of event flags set requests performed on this group.</span></span>
- <span data-ttu-id="f7939-826">**ottiene**: puntatore alla destinazione per il numero di richieste Get dei flag di evento eseguite su questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="f7939-826">**gets**: Pointer to destination for the number of event flags get requests performed on this group.</span></span>
- <span data-ttu-id="f7939-827">**sospensioni**: il puntatore alla destinazione per il numero di flag di evento thread ottiene sospensioni in questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="f7939-827">**suspensions**: Pointer to destination for the number of thread event flags get suspensions on this group.</span></span>
- <span data-ttu-id="f7939-828">**timeout**: puntatore alla destinazione per il numero di flag di evento ottenere i timeout di sospensione in questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="f7939-828">**timeouts**: Pointer to destination for the number of event flags get suspension timeouts on this group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-829">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-829">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-830">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-830">Return Values</span></span>

- <span data-ttu-id="f7939-831">**TX_SUCCESS**: (0x00) risultati del gruppo di flag di evento riusciti Get.</span><span class="sxs-lookup"><span data-stu-id="f7939-831">**TX_SUCCESS**: (0x00) Successful event flags group performance get.</span></span>
- <span data-ttu-id="f7939-832">**TX_PTR_ERROR**: (0x03) puntatore al gruppo di flag evento non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-832">**TX_PTR_ERROR**: (0x03) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="f7939-833">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-833">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-834">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-834">Allowed From</span></span>

<span data-ttu-id="f7939-835">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-835">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-836">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-836">Example</span></span>

```C
TX_EVENT_FLAGS_GROUPmy_event_flag_group;
ULONG           sets;
ULONG           gets;
ULONG           suspensions;
ULONG           timeouts;

/* Retrieve performance information on the previously created event
   flag group. */
status =  tx_event_flags_performance_info_get(&my_event_flag_group,
   &sets, &gets, &suspensions,
   &timeouts);

/* If status is TX_SUCCESS the performance information was successfully
   retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-837">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-837">See Also</span></span>

- <span data-ttu-id="f7939-838">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="f7939-838">tx_event_flags_create</span></span>
- <span data-ttu-id="f7939-839">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-839">tx_event_flags_delete</span></span>
- <span data-ttu-id="f7939-840">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="f7939-840">tx_event_flags_get</span></span>
- <span data-ttu-id="f7939-841">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-841">tx_event_flags_info_get</span></span>
- <span data-ttu-id="f7939-842">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-842">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-843">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="f7939-843">tx_event_flags_set</span></span>
- <span data-ttu-id="f7939-844">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-844">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_performance_system_info_get"></a><span data-ttu-id="f7939-845">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-845">tx_event_flags_performance_system_info_get</span></span>

<span data-ttu-id="f7939-846">Recuperare informazioni sul sistema delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="f7939-846">Retrieve performance system information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-847">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-847">Prototype</span></span>

```c
UINT  tx_event_flags_performance_system_info_get(ULONG *sets,
        ULONG *gets,ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="f7939-848">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-848">Description</span></span>

<span data-ttu-id="f7939-849">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i gruppi di flag di evento nel sistema.</span><span class="sxs-lookup"><span data-stu-id="f7939-849">This service retrieves performance information about all event flags groups in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-850">Per restituire le informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-850">ThreadX SMP library and application must be built with **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-851">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-851">Parameters</span></span>

- <span data-ttu-id="f7939-852">**imposta**: puntatore alla destinazione per il numero totale di richieste set di flag di evento eseguite su tutti i gruppi.</span><span class="sxs-lookup"><span data-stu-id="f7939-852">**sets**: Pointer to destination for the total number of event flags set requests performed on all groups.</span></span>
- <span data-ttu-id="f7939-853">**ottiene**: puntatore alla destinazione per il numero totale di richieste Get dei flag di evento eseguite su tutti i gruppi.</span><span class="sxs-lookup"><span data-stu-id="f7939-853">**gets**: Pointer to destination for the total number of event flags get requests performed on all groups.</span></span>
- <span data-ttu-id="f7939-854">**sospensioni**: il puntatore alla destinazione per il numero totale di flag evento thread ottiene sospensioni in tutti i gruppi.</span><span class="sxs-lookup"><span data-stu-id="f7939-854">**suspensions**: Pointer to destination for the total number of thread event flags get suspensions on all groups.</span></span>
- <span data-ttu-id="f7939-855">**timeout**: puntatore alla destinazione per il numero totale di flag di evento ottenere i timeout di sospensione in tutti i gruppi.</span><span class="sxs-lookup"><span data-stu-id="f7939-855">**timeouts**: Pointer to destination for the total number of event flags get suspension timeouts on all groups.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-856">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-856">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-857">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-857">Return Values</span></span>

- <span data-ttu-id="f7939-858">**TX_SUCCESS**: (0x00) flag di evento riusciti prestazioni del sistema Get.</span><span class="sxs-lookup"><span data-stu-id="f7939-858">**TX_SUCCESS**: (0x00) Successful event flags system performance get.</span></span>
- <span data-ttu-id="f7939-859">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-859">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-860">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-860">Allowed From</span></span>

<span data-ttu-id="f7939-861">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-861">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-862">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-862">Example</span></span>

```c
ULONG         sets;
ULONG         gets;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all previously created event
   flag groups. */
status = tx_event_flags_performance_system_info_get(&sets, &gets,
                &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-863">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-863">See Also</span></span>

- <span data-ttu-id="f7939-864">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="f7939-864">tx_event_flags_create</span></span>
- <span data-ttu-id="f7939-865">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-865">tx_event_flags_delete</span></span>
- <span data-ttu-id="f7939-866">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="f7939-866">tx_event_flags_get</span></span>
- <span data-ttu-id="f7939-867">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-867">tx_event_flags_info_get</span></span>
- <span data-ttu-id="f7939-868">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-868">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="f7939-869">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="f7939-869">tx_event_flags_set</span></span>
- <span data-ttu-id="f7939-870">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-870">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_set"></a><span data-ttu-id="f7939-871">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="f7939-871">tx_event_flags_set</span></span>

<span data-ttu-id="f7939-872">Impostare i flag di evento in un gruppo di flag di evento</span><span class="sxs-lookup"><span data-stu-id="f7939-872">Set event flags in an event flags group</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-873">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-873">Prototype</span></span>

```C
UINT tx_event_flags_set(TX_EVENT_FLAGS_GROUP *group_ptr,
                          ULONG  flags_to_set,UINT set_option);
```
### <a name="description"></a><span data-ttu-id="f7939-874">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-874">Description</span></span>

<span data-ttu-id="f7939-875">Questo servizio imposta o cancella i flag di evento in un gruppo di flag di evento, a seconda dell'opzione set specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-875">This service sets or clears event flags in an event flags group, depending upon the specified set-option.</span></span> <span data-ttu-id="f7939-876">Vengono ripresi tutti i thread sospesi la cui richiesta di flag evento è ora soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="f7939-876">All suspended threads whose event flags request is now satisfied are resumed.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-877">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-877">Parameters</span></span>

- <span data-ttu-id="f7939-878">**group_ptr**: puntatore al blocco di controllo del gruppo di flag di evento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-878">**group_ptr**: Pointer to the previously created event flags group control block.</span></span>
- <span data-ttu-id="f7939-879">**flags_to_set**: specifica i flag di evento da impostare o deselezionare in base all'opzione set selezionata.</span><span class="sxs-lookup"><span data-stu-id="f7939-879">**flags_to_set**: Specifies the event flags to set or clear based upon the set option selected.</span></span>
- <span data-ttu-id="f7939-880">**Set_Option**: specifica se i flag di evento specificati sono individuato o ORed nei flag di evento correnti del gruppo.</span><span class="sxs-lookup"><span data-stu-id="f7939-880">**set_option**: Specifies whether the event flags specified are ANDed or ORed into the current event flags of the group.</span></span> <span data-ttu-id="f7939-881">Di seguito sono riportate le selezioni valide:</span><span class="sxs-lookup"><span data-stu-id="f7939-881">The following are valid selections:</span></span>
    - <span data-ttu-id="f7939-882">**TX_AND**: (0x02)</span><span class="sxs-lookup"><span data-stu-id="f7939-882">**TX_AND**: (0x02)</span></span>
    - <span data-ttu-id="f7939-883">**TX_OR**: (0x00) la selezione di TX_AND specifica che i flag di evento specificati sono **ed** ed è nei flag di evento correnti del gruppo.</span><span class="sxs-lookup"><span data-stu-id="f7939-883">**TX_OR**: (0x00) Selecting TX_AND specifies that the specified event flags are **AND** ed into the current event flags in the group.</span></span> <span data-ttu-id="f7939-884">Questa opzione viene spesso usata per cancellare i flag di evento in un gruppo.</span><span class="sxs-lookup"><span data-stu-id="f7939-884">This option is often used to clear event flags in a group.</span></span> <span data-ttu-id="f7939-885">In caso contrario, se viene specificato TX_OR, i flag di evento specificati sono **o** ed con l'evento corrente nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="f7939-885">Otherwise, if TX_OR is specified, the specified event flags are **OR** ed with the current event in the group.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-886">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-886">Return Values</span></span>

- <span data-ttu-id="f7939-887">**TX_SUCCESS**: (0x00) flag di evento riusciti impostati.</span><span class="sxs-lookup"><span data-stu-id="f7939-887">**TX_SUCCESS**: (0x00) Successful event flags set.</span></span>
- <span data-ttu-id="f7939-888">TX_GROUP_ERROR: (0x06) puntatore non valido al gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="f7939-888">TX_GROUP_ERROR: (0x06) Invalid pointer to event flags group.</span></span>
- <span data-ttu-id="f7939-889">TX_OPTION_ERROR: (0x08) set-Option non valido specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-889">TX_OPTION_ERROR: (0x08) Invalid set-option specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-890">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-890">Allowed From</span></span>

<span data-ttu-id="f7939-891">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-891">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-892">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-892">Preemption Possible</span></span>

<span data-ttu-id="f7939-893">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-893">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-894">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-894">Example</span></span>

```C
TX_EVENT_FLAGS_GROUPmy_event_flags_group;
UINT         status;

/* Set event flags 0, 4, and 8. */
status =  tx_event_flags_set(&my_event_flags_group,
                           0x111, TX_OR);

/* If status equals TX_SUCCESS, the event flags have been
   set and any suspended thread whose request was satisfied
   has been resumed. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-895">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-895">See Also</span></span>

- <span data-ttu-id="f7939-896">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="f7939-896">tx_event_flags_create</span></span>
- <span data-ttu-id="f7939-897">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-897">tx_event_flags_delete</span></span>
- <span data-ttu-id="f7939-898">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="f7939-898">tx_event_flags_get</span></span>
- <span data-ttu-id="f7939-899">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-899">tx_event_flags_info_get</span></span>
- <span data-ttu-id="f7939-900">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-900">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="f7939-901">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-901">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-902">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-902">tx_event_flags_set_notify</span></span>

## <a name="tx_event_flags_set_notify"></a><span data-ttu-id="f7939-903">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-903">tx_event_flags_set_notify</span></span>

<span data-ttu-id="f7939-904">Invia notifica all'applicazione quando vengono impostati i flag evento</span><span class="sxs-lookup"><span data-stu-id="f7939-904">Notify application when event flags are set</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-905">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-905">Prototype</span></span>

```C
UINT tx_event_flags_set_notify(TX_EVENT_FLAGS_GROUP *group_ptr,
       VOID (*events_set_notify)(TX_EVENT_FLAGS_GROUP *));
```
### <a name="description"></a><span data-ttu-id="f7939-906">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-906">Description</span></span>

<span data-ttu-id="f7939-907">Questo servizio registra una funzione di callback delle notifiche chiamata ogni volta che uno o più flag di evento vengono impostati nel gruppo di flag di evento specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-907">This service registers a notification callback function that is called whenever one or more event flags are set in the specified event flags group.</span></span> <span data-ttu-id="f7939-908">L'elaborazione del callback di notifica viene definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-908">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="f7939-909">I flag di evento dell'applicazione set callback di notifica non possono chiamare alcuna API SMP di ThreadX con un'opzione di sospensione.</span><span class="sxs-lookup"><span data-stu-id="f7939-909">The application’s event flags set notification callback is not allowed to call any ThreadX SMP API with a suspension option.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-910">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-910">Parameters</span></span> 
- <span data-ttu-id="f7939-911">**group_ptr**: puntatore al gruppo di flag evento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-911">**group_ptr**: Pointer to previously created event flags group.</span></span>
- <span data-ttu-id="f7939-912">**events_set_notify**: il puntatore ai flag di evento dell'applicazione imposta la funzione di notifica.</span><span class="sxs-lookup"><span data-stu-id="f7939-912">**events_set_notify**: Pointer to application’s event flags set notification function.</span></span> <span data-ttu-id="f7939-913">Se questo valore è TX_NULL, la notifica è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="f7939-913">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-914">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-914">Return Values</span></span>

- <span data-ttu-id="f7939-915">**TX_SUCCESS**: (0x00) la registrazione della notifica del set di flag evento è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-915">**TX_SUCCESS**: (0x00) Successful registration of event flags set notification.</span></span>
- <span data-ttu-id="f7939-916">TX_GROUP_ERROR: (0x06) puntatore al gruppo di flag evento non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-916">TX_GROUP_ERROR: (0x06) Invalid event flags group pointer.</span></span>
- <span data-ttu-id="f7939-917">TX_FEATURE_NOT_ENABLED: (0xFF) il sistema è stato compilato con le funzionalità di notifica disabilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-917">TX_FEATURE_NOT_ENABLED: (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-918">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-918">Allowed From</span></span>

<span data-ttu-id="f7939-919">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-919">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-920">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-920">Example</span></span>

```C
TX_EVENT_FLAGS_GROUPmy_group;

/* Register the "my_event_flags_set_notify" function for monitoring
   event flags set in the event flags group "my_group." */
status =  tx_event_flags_set_notify(&my_group,
                my_event_flags_set_notify);

/* If status is TX_SUCCESS the event flags set notification function
   was successfully registered. */

void my_event_flags_set_notify(TX_EVENT_FLAGS_GROUP *group_ptr)
   /* One or more event flags was set in this group! */
```
### <a name="see-also"></a><span data-ttu-id="f7939-921">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-921">See Also</span></span>

- <span data-ttu-id="f7939-922">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="f7939-922">tx_event_flags_create</span></span>
- <span data-ttu-id="f7939-923">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-923">tx_event_flags_delete</span></span>
- <span data-ttu-id="f7939-924">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="f7939-924">tx_event_flags_get</span></span>
- <span data-ttu-id="f7939-925">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-925">tx_event_flags_info_get</span></span>
- <span data-ttu-id="f7939-926">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-926">tx_event_flags_performance_info_get</span></span>
- <span data-ttu-id="f7939-927">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-927">tx_event_flags_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-928">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="f7939-928">tx_event_flags_set</span></span>

## <a name="tx_interrupt_control"></a><span data-ttu-id="f7939-929">tx_interrupt_control</span><span class="sxs-lookup"><span data-stu-id="f7939-929">tx_interrupt_control</span></span>

<span data-ttu-id="f7939-930">Abilitazione e disabilitazione degli interrupt</span><span class="sxs-lookup"><span data-stu-id="f7939-930">Enable and disable interrupts</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-931">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-931">Prototype</span></span>

```C
UINT tx_interrupt_control(UINT new_posture);
```
### <a name="description"></a><span data-ttu-id="f7939-932">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-932">Description</span></span>

<span data-ttu-id="f7939-933">Questo servizio Abilita o Disabilita gli interrupt come specificato dal parametro di input **new_posture**.</span><span class="sxs-lookup"><span data-stu-id="f7939-933">This service enables or disables interrupts as specified by the input parameter **new_posture**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-934">Se questo servizio viene chiamato da un thread dell'applicazione, la postura di interrupt rimane parte del contesto del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-934">If this service is called from an application thread, the interrupt posture remains part of that thread’s context.</span></span> <span data-ttu-id="f7939-935">Ad esempio, se il thread chiama questa routine per disabilitare gli interrupt e quindi sospendere, quando viene ripreso, gli interrupt vengono nuovamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="f7939-935">For example, if the thread calls this routine to disable interrupts and then suspends, when it is resumed, interrupts are disabled again.</span></span>

> [!WARNING]
> <span data-ttu-id="f7939-936">Questo servizio non deve essere usato per abilitare gli interrupt durante l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-936">This service should not be used to enable interrupts during initialization!</span></span> <span data-ttu-id="f7939-937">Questa operazione può causare risultati imprevedibili.</span><span class="sxs-lookup"><span data-stu-id="f7939-937">Doing so could cause unpredictable results.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-938">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-938">Parameters</span></span>

- <span data-ttu-id="f7939-939">**new_posture**: questo parametro specifica se gli interrupt sono disabilitati o abilitati.</span><span class="sxs-lookup"><span data-stu-id="f7939-939">**new_posture**: This parameter specifies whether interrupts are disabled or enabled.</span></span> <span data-ttu-id="f7939-940">I valori validi includono **TX_INT_DISABLE e TX_INT_ENABLE.**</span><span class="sxs-lookup"><span data-stu-id="f7939-940">Legal values include **TX_INT_DISABLE and TX_INT_ENABLE.**</span></span> <span data-ttu-id="f7939-941">I valori effettivi di questi parametri sono specifici della porta.</span><span class="sxs-lookup"><span data-stu-id="f7939-941">The actual values for these parameters are port specific.</span></span> <span data-ttu-id="f7939-942">Alcune architetture di elaborazione possono inoltre supportare le posture di disabilitazione di interrupt aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="f7939-942">In addition, some processing architectures might support additional interrupt disable postures.</span></span> <span data-ttu-id="f7939-943">Per altri dettagli, vedere le informazioni sul **_readme_threadx.txt_** fornite nel disco di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f7939-943">Please see the **_readme_threadx.txt_** information supplied on the distribution disk for more details.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-944">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-944">Return Values</span></span>

- <span data-ttu-id="f7939-945">comportamento precedente: questo servizio restituisce la postura di interrupt precedente al chiamante.</span><span class="sxs-lookup"><span data-stu-id="f7939-945">previous posture: This service returns the previous interrupt posture to the caller.</span></span> <span data-ttu-id="f7939-946">In questo modo gli utenti del servizio possono ripristinare la postura precedente dopo la disabilitazione degli interrupt.</span><span class="sxs-lookup"><span data-stu-id="f7939-946">This allows users of the service to restore the previous posture after interrupts are disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-947">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-947">Allowed From</span></span>

<span data-ttu-id="f7939-948">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-948">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-949">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-949">Preemption Possible</span></span>

<span data-ttu-id="f7939-950">No</span><span class="sxs-lookup"><span data-stu-id="f7939-950">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-951">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-951">Example</span></span>

```C
UINT my_old_posture;

/* Lockout interrupts */
my_old_posture =  tx_interrupt_control(TX_INT_DISABLE);

/* Perform critical operations that need interrupts
   locked-out.... */

/* Restore previous interrupt lockout posture. */
tx_interrupt_control(my_old_posture);
```
### <a name="see-also"></a><span data-ttu-id="f7939-952">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-952">See Also</span></span>

<span data-ttu-id="f7939-953">nessuno</span><span class="sxs-lookup"><span data-stu-id="f7939-953">None</span></span>

## <a name="tx_mutex_create"></a><span data-ttu-id="f7939-954">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="f7939-954">tx_mutex_create</span></span>

<span data-ttu-id="f7939-955">Crea mutex di esclusione reciproca</span><span class="sxs-lookup"><span data-stu-id="f7939-955">Create mutual exclusion mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-956">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-956">Prototype</span></span>

```C
UINT tx_mutex_create(TX_MUTEX *mutex_ptr,
                          CHAR *name_ptr, UINT priority_inherit);
```
### <a name="description"></a><span data-ttu-id="f7939-957">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-957">Description</span></span>
    
<span data-ttu-id="f7939-958">Questo servizio crea un mutex per l'esclusione reciproca tra thread per la protezione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="f7939-958">This service creates a mutex for inter-thread mutual exclusion for resource protection.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-959">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-959">Parameters</span></span>

- <span data-ttu-id="f7939-960">**mutex_ptr**: puntatore a un blocco di controllo mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-960">**mutex_ptr**: Pointer to a mutex control block.</span></span>
- <span data-ttu-id="f7939-961">**name_ptr**: puntatore al nome del mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-961">**name_ptr**: Pointer to the name of the mutex.</span></span>
- <span data-ttu-id="f7939-962">**priority_inherit**: specifica se questo mutex supporta o meno l'ereditarietà della priorità.</span><span class="sxs-lookup"><span data-stu-id="f7939-962">**priority_inherit**: Specifies whether or not this mutex supports priority inheritance.</span></span> <span data-ttu-id="f7939-963">Se questo valore è TX_INHERIT, l'ereditarietà della priorità è supportata.</span><span class="sxs-lookup"><span data-stu-id="f7939-963">If this value is TX_INHERIT, then priority inheritance is supported.</span></span> <span data-ttu-id="f7939-964">Tuttavia, se si specifica TX_NO_INHERIT, l'ereditarietà della priorità non è supportata da questo mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-964">However, if TX_NO_INHERIT is specified, priority inheritance is not supported by this mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-965">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-965">Return Values</span></span>

- <span data-ttu-id="f7939-966">**TX_SUCCESS**: (0x00) la creazione di mutex è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-966">**TX_SUCCESS**: (0x00) Successful mutex creation.</span></span>
- <span data-ttu-id="f7939-967">TX_MUTEX_ERROR: (0x1C) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-967">TX_MUTEX_ERROR: (0x1C) Invalid mutex pointer.</span></span> <span data-ttu-id="f7939-968">Il puntatore è NULL o il mutex è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="f7939-968">Either the pointer is NULL or the mutex is already created.</span></span>
- <span data-ttu-id="f7939-969">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-969">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>
- <span data-ttu-id="f7939-970">TX_INHERIT_ERROR: (0x1F) la priorità non è valida per il parametro.</span><span class="sxs-lookup"><span data-stu-id="f7939-970">TX_INHERIT_ERROR: (0x1F) Invalid priority inherit parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-971">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-971">Allowed From</span></span>

<span data-ttu-id="f7939-972">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="f7939-972">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-973">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-973">Preemption Possible</span></span>

<span data-ttu-id="f7939-974">No</span><span class="sxs-lookup"><span data-stu-id="f7939-974">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-975">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-975">Example</span></span>

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Create a mutex to provide protection over a
   common resource. */
status =  tx_mutex_create(&my_mutex,"my_mutex_name",
                           TX_NO_INHERIT);

/* If status equals TX_SUCCESS, my_mutex is ready for
   use. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-976">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-976">See Also</span></span>

- <span data-ttu-id="f7939-977">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-977">tx_mutex_delete</span></span>
- <span data-ttu-id="f7939-978">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="f7939-978">tx_mutex_get</span></span>
- <span data-ttu-id="f7939-979">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-979">tx_mutex_info_get</span></span>
- <span data-ttu-id="f7939-980">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-980">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="f7939-981">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-981">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-982">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-982">tx_mutex_prioritize</span></span>
- <span data-ttu-id="f7939-983">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="f7939-983">tx_mutex_put</span></span>

## <a name="tx_mutex_delete"></a><span data-ttu-id="f7939-984">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-984">tx_mutex_delete</span></span>

<span data-ttu-id="f7939-985">Elimina mutex di esclusione reciproca</span><span class="sxs-lookup"><span data-stu-id="f7939-985">Delete mutual exclusion mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-986">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-986">Prototype</span></span>

```C
UINT tx_mutex_delete(TX_MUTEX *mutex_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-987">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-987">Description</span></span>

<span data-ttu-id="f7939-988">Questo servizio Elimina il mutex specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-988">This service deletes the specified mutex.</span></span> <span data-ttu-id="f7939-989">Tutti i thread sospesi in attesa del mutex vengono ripresi e viene fornito un TX_DELETED stato restituito.</span><span class="sxs-lookup"><span data-stu-id="f7939-989">All threads suspended waiting for the mutex are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-990">È responsabilità dell'applicazione impedire l'uso di un mutex eliminato.</span><span class="sxs-lookup"><span data-stu-id="f7939-990">It is the application’s responsibility to prevent use of a deleted mutex.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-991">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-991">Parameters</span></span>

- <span data-ttu-id="f7939-992">**mutex_ptr**: puntatore a un mutex creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-992">**mutex_ptr**: Pointer to a previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-993">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-993">Return Values</span></span>

- <span data-ttu-id="f7939-994">**TX_SUCCESS**: (0x00) eliminazione mutex riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-994">**TX_SUCCESS**: (0x00) Successful mutex deletion.</span></span>
- <span data-ttu-id="f7939-995">TX_MUTEX_ERROR: (0x1C) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-995">TX_MUTEX_ERROR: (0x1C) Invalid mutex pointer.</span></span>
- <span data-ttu-id="f7939-996">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-996">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-997">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-997">Allowed From</span></span>

<span data-ttu-id="f7939-998">Thread</span><span class="sxs-lookup"><span data-stu-id="f7939-998">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-999">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-999">Preemption Possible</span></span>

<span data-ttu-id="f7939-1000">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1000">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1001">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1001">Example</span></span>

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Delete a mutex. Assume that the mutex
   has already been created. */
status =  tx_mutex_delete(&my_mutex);

/* If status equals TX_SUCCESS, the mutex is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1002">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1002">See Also</span></span>

- <span data-ttu-id="f7939-1003">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1003">tx_mutex_create</span></span>
- <span data-ttu-id="f7939-1004">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1004">tx_mutex_get</span></span>
- <span data-ttu-id="f7939-1005">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1005">tx_mutex_info_get</span></span>
- <span data-ttu-id="f7939-1006">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1006">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="f7939-1007">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1007">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1008">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1008">tx_mutex_prioritize</span></span>
- <span data-ttu-id="f7939-1009">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1009">tx_mutex_put</span></span>

## <a name="tx_mutex_get"></a><span data-ttu-id="f7939-1010">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1010">tx_mutex_get</span></span>

<span data-ttu-id="f7939-1011">Ottenere la proprietà di mutex</span><span class="sxs-lookup"><span data-stu-id="f7939-1011">Obtain ownership of mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1012">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1012">Prototype</span></span>

```C
UINT tx_mutex_get(TX_MUTEX *mutex_ptr, ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="f7939-1013">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1013">Description</span></span>

<span data-ttu-id="f7939-1014">Questo servizio tenta di ottenere la proprietà esclusiva del mutex specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1014">This service attempts to obtain exclusive ownership of the specified mutex.</span></span> <span data-ttu-id="f7939-1015">Se il thread chiamante è già proprietario del mutex, viene incrementato un contatore interno e viene restituito uno stato di esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1015">If the calling thread already owns the mutex, an internal counter is incremented and a successful status is returned.</span></span>

<span data-ttu-id="f7939-1016">Se il mutex è di proprietà di un altro thread e questo thread è con priorità più elevata e l'ereditarietà della priorità è stata specificata al momento della creazione del mutex, la priorità del thread con priorità inferiore verrà generata temporaneamente a quella del thread chiamante.</span><span class="sxs-lookup"><span data-stu-id="f7939-1016">If the mutex is owned by another thread and this thread is higher priority and priority inheritance was specified at mutex create, the lower priority thread’s priority will be temporarily raised to that of the calling thread.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1017">La priorità del thread con priorità inferiore che possiede un mutex con priorityinheritance non deve mai essere modificata da un thread esterno durante la proprietà del mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1017">The priority of the lower priority thread owning a mutex with priorityinheritance should never be modified by an external thread during mutex ownership.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1018">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1018">Parameters</span></span>

- <span data-ttu-id="f7939-1019">**mutex_ptr**: puntatore a un mutex creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1019">**mutex_ptr**: Pointer to a previously created mutex.</span></span>
- <span data-ttu-id="f7939-1020">**WAIT_OPTION**: definisce il comportamento del servizio se il mutex è già di proprietà di un altro thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1020">**wait_option**: Defines how the service behaves if the mutex is already owned by another thread.</span></span> <span data-ttu-id="f7939-1021">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="f7939-1021">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="f7939-1022">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="f7939-1022">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="f7939-1023">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="f7939-1023">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="f7939-1024">valore di timeout: (0x00000001 tramite 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="f7939-1024">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="f7939-1025">La selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1025">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="f7939-1026">*Questa è l'unica opzione valida se il servizio viene chiamato dall'inizializzazione.*</span><span class="sxs-lookup"><span data-stu-id="f7939-1026">*This is the only valid option if the service is called from Initialization.*</span></span>

    <span data-ttu-id="f7939-1027">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando non sarà disponibile il mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1027">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until the mutex is available.</span></span>

    <span data-ttu-id="f7939-1028">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi in attesa del mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1028">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for the mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1029">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1029">Return Values</span></span>

- <span data-ttu-id="f7939-1030">**TX_SUCCESS**: (0x00) operazione di Get mutex riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1030">**TX_SUCCESS**: (0x00) Successful mutex get operation.</span></span>
- <span data-ttu-id="f7939-1031">**TX_DELETED**: (0x01) mutex eliminato durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1031">**TX_DELETED**: (0x01) Mutex was deleted while thread was suspended.</span></span>
- <span data-ttu-id="f7939-1032">**TX_NOT_AVAILABLE**: il servizio (0x1d) non è stato in grado di ottenere la proprietà del mutex entro il tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1032">**TX_NOT_AVAILABLE**: (0x1D) Service was unable to get ownership of the mutex within the specified time to wait.</span></span>
- <span data-ttu-id="f7939-1033">**TX_WAIT_ABORTED**: la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-1033">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="f7939-1034">TX_MUTEX_ERROR: (0x1C) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1034">TX_MUTEX_ERROR: (0x1C) Invalid mutex pointer.</span></span>
- <span data-ttu-id="f7939-1035">TX_WAIT_ERROR: (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1035">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>
- <span data-ttu-id="f7939-1036">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1036">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1037">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1037">Allowed From</span></span>

<span data-ttu-id="f7939-1038">Inizializzazione e thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-1038">Initialization and threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1039">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1039">Preemption Possible</span></span>

<span data-ttu-id="f7939-1040">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1040">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1041">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1041">Example</span></span>

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Obtain exclusive ownership of the mutex "my_mutex".
   If the mutex "my_mutex" is not available, suspend until it
   becomes available. */
status =  tx_mutex_get(&my_mutex, TX_WAIT_FOREVER);
```
### <a name="see-also"></a><span data-ttu-id="f7939-1042">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1042">See Also</span></span>

- <span data-ttu-id="f7939-1043">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1043">tx_mutex_create</span></span>
- <span data-ttu-id="f7939-1044">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1044">tx_mutex_delete</span></span>
- <span data-ttu-id="f7939-1045">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1045">tx_mutex_info_get</span></span>
- <span data-ttu-id="f7939-1046">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1046">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="f7939-1047">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1047">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1048">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1048">tx_mutex_prioritize</span></span>
- <span data-ttu-id="f7939-1049">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1049">tx_mutex_put</span></span>

## <a name="tx_mutex_info_get"></a><span data-ttu-id="f7939-1050">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1050">tx_mutex_info_get</span></span>

<span data-ttu-id="f7939-1051">Recuperare informazioni sul mutex</span><span class="sxs-lookup"><span data-stu-id="f7939-1051">Retrieve information about mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1052">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1052">Prototype</span></span>

```C
UINT tx_mutex_info_get(TX_MUTEX *mutex_ptr, CHAR **name,
                          ULONG *count, TX_THREAD **owner,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count, TX_MUTEX **next_mutex);
```
### <a name="description"></a><span data-ttu-id="f7939-1053">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1053">Description</span></span>

<span data-ttu-id="f7939-1054">Questo servizio recupera le informazioni dal mutex specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1054">This service retrieves information from the specified mutex.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1055">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1055">Parameters</span></span>

- <span data-ttu-id="f7939-1056">**mutex_ptr**: puntatore al blocco di controllo mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1056">**mutex_ptr**: Pointer to mutex control block.</span></span>
- <span data-ttu-id="f7939-1057">**Name**: puntatore alla destinazione per il puntatore al nome del mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1057">**name**: Pointer to destination for the pointer to the mutex’s name.</span></span>
- <span data-ttu-id="f7939-1058">**count**: puntatore alla destinazione per il numero di proprietà del mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1058">**count**: Pointer to destination for the ownership count of the mutex.</span></span>
- <span data-ttu-id="f7939-1059">**owner**: puntatore alla destinazione per il puntatore del thread proprietario.</span><span class="sxs-lookup"><span data-stu-id="f7939-1059">**owner**: Pointer to destination for the owning thread’s pointer.</span></span>
- <span data-ttu-id="f7939-1060">**first_suspended**: puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione di questo mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1060">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this mutex.</span></span>
- <span data-ttu-id="f7939-1061">**suspended_count**: puntatore alla destinazione per il numero di thread attualmente sospesi in questo mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1061">**suspended_count**: Pointer to destination for the number of threads currently suspended on this mutex.</span></span>
- <span data-ttu-id="f7939-1062">**next_mutex**: puntatore alla destinazione per il puntatore del mutex creato successivo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1062">**next_mutex**: Pointer to destination for the pointer of the next created mutex.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1063">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1063">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1064">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1064">Return Values</span></span>

- <span data-ttu-id="f7939-1065">**TX_SUCCESS**: (0x00) il recupero delle informazioni mutex è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-1065">**TX_SUCCESS**: (0x00) Successful mutex information retrieval.</span></span>
- <span data-ttu-id="f7939-1066">TX_MUTEX_ERROR: (0x1C) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1066">TX_MUTEX_ERROR: (0x1C) Invalid mutex pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1067">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1067">Allowed From</span></span>

<span data-ttu-id="f7939-1068">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1068">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1069">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1069">Preemption Possible</span></span>

<span data-ttu-id="f7939-1070">No</span><span class="sxs-lookup"><span data-stu-id="f7939-1070">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1071">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1071">Example</span></span>

```C
TX_MUTEX     my_mutex;
CHAR         *name;
ULONG        count;
TX_THREAD    *owner;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_MUTEX     *next_mutex;
UINT         status;

/* Retrieve information about the previously created
   mutex "my_mutex." */
status =  tx_mutex_info_get(&my_mutex, &name,
                          &count, &owner,
                          &first_suspended, &suspended_count,
                          &next_mutex);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1072">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1072">See Also</span></span>

- <span data-ttu-id="f7939-1073">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1073">tx_mutex_create</span></span>
- <span data-ttu-id="f7939-1074">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1074">tx_mutex_delete</span></span>
- <span data-ttu-id="f7939-1075">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1075">tx_mutex_get</span></span>
- <span data-ttu-id="f7939-1076">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1076">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="f7939-1077">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1077">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1078">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1078">tx_mutex_prioritize</span></span>
- <span data-ttu-id="f7939-1079">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1079">tx_mutex_put</span></span>

## <a name="tx_mutex_performance_info_get"></a><span data-ttu-id="f7939-1080">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1080">tx_mutex_performance_info_get</span></span>

<span data-ttu-id="f7939-1081">Ottenere informazioni sulle prestazioni di mutex</span><span class="sxs-lookup"><span data-stu-id="f7939-1081">Get mutex performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1082">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1082">Prototype</span></span>

```C
UINT tx_mutex_performance_info_get(TX_MUTEX *mutex_ptr, ULONG *puts,
       ULONG *gets, ULONG *suspensions, ULONG *timeouts,
       ULONG *inversions, ULONG *inheritances);
```
### <a name="description"></a><span data-ttu-id="f7939-1083">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1083">Description</span></span>

<span data-ttu-id="f7939-1084">Questo servizio recupera le informazioni sulle prestazioni relative al mutex specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1084">This service retrieves performance information about the specified mutex.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1085">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_MUTEX_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1085">The ThreadX SMP library and application must be built with **TX_MUTEX_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1086">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1086">Parameters</span></span>

- <span data-ttu-id="f7939-1087">**mutex_ptr**: puntatore a mutex creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1087">**mutex_ptr**: Pointer to previously created mutex.</span></span>
- <span data-ttu-id="f7939-1088">**inserisce**: puntatore alla destinazione per il numero di richieste PUT eseguite sul mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1088">**puts**: Pointer to destination for the number of put requests performed on this mutex.</span></span>
- <span data-ttu-id="f7939-1089">**ottiene**: puntatore alla destinazione per il numero di richieste Get eseguite sul mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1089">**gets**: Pointer to destination for the number of get requests performed on this mutex.</span></span>
- <span data-ttu-id="f7939-1090">**sospensioni**: puntatore alla destinazione per il numero delle sospensioni mutex del thread Get sul mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1090">**suspensions**: Pointer to destination for the number of thread mutex get suspensions on this mutex.</span></span>
- <span data-ttu-id="f7939-1091">**timeout**: puntatore alla destinazione per il numero di timeout di sospensione del mutex Get in questo mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1091">**timeouts**: Pointer to destination for the number of mutex get suspension timeouts on this mutex.</span></span>
- <span data-ttu-id="f7939-1092">**Inversions**: puntatore alla destinazione per il numero di inversioni di priorità dei thread sul mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1092">**inversions**: Pointer to destination for the number of thread priority inversions on this mutex.</span></span>
- <span data-ttu-id="f7939-1093">**ereditarietà**: puntatore alla destinazione per il numero di operazioni di ereditarietà della priorità dei thread sul mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1093">**inheritances**: Pointer to destination for the number of thread priority inheritance operations on this mutex.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1094">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1094">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1095">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1095">Return Values</span></span>

- <span data-ttu-id="f7939-1096">**TX_SUCCESS**: (0x00) ottenere risultati positivi per mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1096">**TX_SUCCESS**: (0x00) Successful mutex performance get.</span></span> 
- <span data-ttu-id="f7939-1097">**TX_PTR_ERROR**: (0x03) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1097">**TX_PTR_ERROR**: (0x03) Invalid mutex pointer.</span></span>
- <span data-ttu-id="f7939-1098">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-1098">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1099">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1099">Allowed From</span></span>

<span data-ttu-id="f7939-1100">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1100">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1101">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1101">Example</span></span>

```C
TX_MUTEX     my_mutex;
ULONG        puts;
ULONG        gets;
ULONG        suspensions;
ULONG        timeouts;
ULONG        inversions;
ULONG        inheritances;

/* Retrieve performance information on the previously created
   mutex. */
status =  tx_mutex_performance_info_get(&my_mutex_ptr, &puts, &gets,
                &suspensions, &timeouts, &inversions,
                &inheritances);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1102">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1102">See Also</span></span>

- <span data-ttu-id="f7939-1103">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1103">tx_mutex_create</span></span>
- <span data-ttu-id="f7939-1104">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1104">tx_mutex_delete</span></span>
- <span data-ttu-id="f7939-1105">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1105">tx_mutex_get</span></span>
- <span data-ttu-id="f7939-1106">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1106">tx_mutex_info_get</span></span>
- <span data-ttu-id="f7939-1107">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1107">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1108">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1108">tx_mutex_prioritize</span></span>
- <span data-ttu-id="f7939-1109">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1109">tx_mutex_put</span></span>

## <a name="tx_mutex_performance_system_info_get"></a><span data-ttu-id="f7939-1110">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1110">tx_mutex_performance_system_info_get</span></span>

<span data-ttu-id="f7939-1111">Ottenere informazioni sulle prestazioni del sistema mutex</span><span class="sxs-lookup"><span data-stu-id="f7939-1111">Get mutex system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1112">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1112">Prototype</span></span>

```C
UINT  tx_mutex_performance_system_info_get(ULONG *puts, ULONG *gets,
        ULONG *suspensions, ULONG *timeouts,
        ULONG *inversions, ULONG *inheritances);
```
### <a name="description"></a><span data-ttu-id="f7939-1113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1113">Description</span></span>

<span data-ttu-id="f7939-1114">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i mutex nel sistema.</span><span class="sxs-lookup"><span data-stu-id="f7939-1114">This service retrieves performance information about all the mutexes in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1115">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_MUTEX_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1115">The ThreadX SMP library and application must be built with **TX_MUTEX_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1116">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1116">Parameters</span></span>

- <span data-ttu-id="f7939-1117">**inserisce**: puntatore alla destinazione per il numero totale di richieste PUT eseguite su tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1117">**puts**: Pointer to destination for the total number of put requests performed on all mutexes.</span></span>
- <span data-ttu-id="f7939-1118">**ottiene**: puntatore alla destinazione per il numero totale di richieste Get eseguite su tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1118">**gets**: Pointer to destination for the total number of get requests performed on all mutexes.</span></span>
- <span data-ttu-id="f7939-1119">**sospensioni**: puntatore alla destinazione per il numero totale delle sospensioni del mutex di thread per tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1119">**suspensions**: Pointer to destination for the total number of thread mutex get suspensions on all mutexes.</span></span>
- <span data-ttu-id="f7939-1120">**timeout**: puntatore alla destinazione per il numero totale di timeout di sospensione per mutex Get su tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1120">**timeouts**: Pointer to destination for the total number of mutex get suspension timeouts on all mutexes.</span></span>
- <span data-ttu-id="f7939-1121">**Inversions**: puntatore alla destinazione per il numero totale di inversioni di priorità dei thread in tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1121">**inversions**: Pointer to destination for the total number of thread priority inversions on all mutexes.</span></span>
- <span data-ttu-id="f7939-1122">**ereditarietà**: puntatore alla destinazione per il numero totale di operazioni di ereditarietà della priorità dei thread su tutti i mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1122">**inheritances**: Pointer to destination for the total number of thread priority inheritance operations on all mutexes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1123">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1123">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1124">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1124">Return Values</span></span>

- <span data-ttu-id="f7939-1125">**TX_SUCCESS**: (0x00) prestazioni del sistema mutex riuscite.</span><span class="sxs-lookup"><span data-stu-id="f7939-1125">**TX_SUCCESS**: (0x00) Successful mutex system performance get.</span></span>
- <span data-ttu-id="f7939-1126">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-1126">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1127">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1127">Allowed From</span></span>

<span data-ttu-id="f7939-1128">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1128">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1129">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1129">Example</span></span>

```C
ULONG         puts;
ULONG         gets;
ULONG         suspensions;
ULONG         timeouts;
ULONG         inversions;
ULONG         inheritances;

/* Retrieve performance information on all previously created
   mutexes. */
status = tx_mutex_performance_system_info_get(&puts, &gets,
                &suspensions, &timeouts,
                &inversions, &inheritances);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1130">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1130">See Also</span></span>

- <span data-ttu-id="f7939-1131">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1131">tx_mutex_create</span></span>
- <span data-ttu-id="f7939-1132">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1132">tx_mutex_delete</span></span>
- <span data-ttu-id="f7939-1133">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1133">tx_mutex_get</span></span>
- <span data-ttu-id="f7939-1134">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1134">tx_mutex_info_get</span></span>
- <span data-ttu-id="f7939-1135">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1135">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="f7939-1136">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1136">tx_mutex_prioritize</span></span>
- <span data-ttu-id="f7939-1137">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1137">tx_mutex_put</span></span>

## <a name="tx_mutex_prioritize"></a><span data-ttu-id="f7939-1138">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1138">tx_mutex_prioritize</span></span>

<span data-ttu-id="f7939-1139">Elencare le sospensioni mutex</span><span class="sxs-lookup"><span data-stu-id="f7939-1139">Prioritize mutex suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1140">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1140">Prototype</span></span>

```C
UINT tx_mutex_prioritize(TX_MUTEX *mutex_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-1141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1141">Description</span></span>

<span data-ttu-id="f7939-1142">Questo servizio posiziona il thread con priorità più elevata sospeso per la proprietà del mutex all'inizio dell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="f7939-1142">This service places the highest priority thread suspended for ownership of the mutex at the front of the suspension list.</span></span> <span data-ttu-id="f7939-1143">Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.</span><span class="sxs-lookup"><span data-stu-id="f7939-1143">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1144">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1144">Parameters</span></span> 

- <span data-ttu-id="f7939-1145">**mutex_ptr**: puntatore al mutex creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1145">**mutex_ptr**: Pointer to the previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1146">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1146">Return Values</span></span>

- <span data-ttu-id="f7939-1147">**TX_SUCCESS**: (0x00) priorità mutex riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1147">**TX_SUCCESS**: (0x00) Successful mutex prioritize.</span></span>
- <span data-ttu-id="f7939-1148">TX_MUTEX_ERROR: (0x1C) puntatore mutex non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1148">TX_MUTEX_ERROR: (0x1C) Invalid mutex pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1149">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1149">Allowed From</span></span>

<span data-ttu-id="f7939-1150">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1150">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1151">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1151">Preemption Possible</span></span>

<span data-ttu-id="f7939-1152">No</span><span class="sxs-lookup"><span data-stu-id="f7939-1152">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1153">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1153">Example</span></span>

```C
TX_MUTEX     my_mutex;
UINT         status;

/* Ensure that the highest priority thread will receive
   ownership of the mutex when it becomes available. */
status = tx_mutex_prioritize(&my_mutex);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_mutex_put call that releases ownership of the
   mutex will give ownership to this thread and wake it
   up. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1154">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1154">See Also</span></span>

- <span data-ttu-id="f7939-1155">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1155">tx_mutex_create</span></span>
- <span data-ttu-id="f7939-1156">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1156">tx_mutex_delete</span></span>
- <span data-ttu-id="f7939-1157">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1157">tx_mutex_get</span></span>
- <span data-ttu-id="f7939-1158">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1158">tx_mutex_info_get</span></span>
- <span data-ttu-id="f7939-1159">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1159">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="f7939-1160">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1160">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1161">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1161">tx_mutex_put</span></span>

## <a name="tx_mutex_put"></a><span data-ttu-id="f7939-1162">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1162">tx_mutex_put</span></span>

<span data-ttu-id="f7939-1163">Rilascia la proprietà di mutex</span><span class="sxs-lookup"><span data-stu-id="f7939-1163">Release ownership of mutex</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1164">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1164">Prototype</span></span>

```C
UINT tx_mutex_put(TX_MUTEX *mutex_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-1165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1165">Description</span></span>

<span data-ttu-id="f7939-1166">Questo servizio decrementa il numero di proprietà del mutex specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1166">This service decrements the ownership count of the specified mutex.</span></span> <span data-ttu-id="f7939-1167">Se il conteggio proprietà è pari a zero, il mutex viene reso disponibile.</span><span class="sxs-lookup"><span data-stu-id="f7939-1167">If the ownership count is zero, the mutex is made available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1168">Se durante la creazione del mutex è stata selezionata l'ereditarietà prioritaria, la priorità del thread di rilascio verrà ripristinata con la priorità che aveva quando era stata originariamente ottenuta la proprietà del mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1168">If priority inheritance was selected during mutex creation, the priority of the releasing thread will be restored to the priority it had when it originally obtained ownership of the mutex.</span></span> <span data-ttu-id="f7939-1169">Eventuali altre modifiche di priorità apportate al thread di rilascio durante la proprietà del mutex possono essere annullate.</span><span class="sxs-lookup"><span data-stu-id="f7939-1169">Any other priority changes made to the releasing thread during ownership of the mutex may be undone.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1170">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1170">Parameters</span></span>

- <span data-ttu-id="f7939-1171">**mutex_ptr**: puntatore al mutex creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1171">**mutex_ptr**: Pointer to the previously created mutex.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1172">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1172">Return Values</span></span>

- <span data-ttu-id="f7939-1173">**TX_SUCCESS**: (0x00) versione mutex riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1173">**TX_SUCCESS**: (0x00) Successful mutex release.</span></span>
- <span data-ttu-id="f7939-1174">**TX_NOT_OWNED**: (0x1E) mutex non è di proprietà del chiamante.</span><span class="sxs-lookup"><span data-stu-id="f7939-1174">**TX_NOT_OWNED**: (0x1E) Mutex is not owned by caller.</span></span>
- <span data-ttu-id="f7939-1175">TX_MUTEX_ERROR: (0x1C) puntatore non valido a mutex.</span><span class="sxs-lookup"><span data-stu-id="f7939-1175">TX_MUTEX_ERROR: (0x1C) Invalid pointer to mutex.</span></span>
- <span data-ttu-id="f7939-1176">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1176">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1177">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1177">Allowed From</span></span>

<span data-ttu-id="f7939-1178">Inizializzazione e thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-1178">Initialization and threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1179">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1179">Preemption Possible</span></span>

<span data-ttu-id="f7939-1180">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1180">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1181">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1181">Example</span></span>

```C
TX_MUTEX         my_mutex;
UINT             status;
/* Release ownership of "my_mutex." */
status =  tx_mutex_put(&my_mutex);

/* If status equals TX_SUCCESS, the mutex ownership
   count has been decremented and if zero, released. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1182">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1182">See Also</span></span>

- <span data-ttu-id="f7939-1183">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1183">tx_mutex_create</span></span>
- <span data-ttu-id="f7939-1184">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1184">tx_mutex_delete</span></span>
- <span data-ttu-id="f7939-1185">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1185">tx_mutex_get</span></span>
- <span data-ttu-id="f7939-1186">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1186">tx_mutex_info_get</span></span>
- <span data-ttu-id="f7939-1187">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1187">tx_mutex_performance_info_get</span></span>
- <span data-ttu-id="f7939-1188">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1188">tx_mutex_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1189">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1189">tx_mutex_prioritize</span></span>

## <a name="tx_queue_create"></a><span data-ttu-id="f7939-1190">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1190">tx_queue_create</span></span>

<span data-ttu-id="f7939-1191">Crea coda messaggi</span><span class="sxs-lookup"><span data-stu-id="f7939-1191">Create message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1192">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1192">Prototype</span></span>

```c
UINT tx_queue_create(TX_QUEUE *queue_ptr, CHAR *name_ptr,
                          UINT message_size,
                          VOID *queue_start, ULONG queue_size);
```
### <a name="description"></a><span data-ttu-id="f7939-1193">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1193">Description</span></span>

<span data-ttu-id="f7939-1194">Questo servizio crea una coda di messaggi che in genere viene utilizzata per la comunicazione tra thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1194">This service creates a message queue that is typically used for interthread communication.</span></span> <span data-ttu-id="f7939-1195">Il numero totale di messaggi viene calcolato dalla dimensione del messaggio specificata e dal numero totale di byte nella coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1195">The total number of messages is calculated from the specified message size and the total number of bytes in the queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1196">Se il numero totale di byte specificato nell'area di memoria della coda non è divisibile in modo uniforme per la dimensione del messaggio specificata, i byte rimanenti nell'area di memoria non vengono utilizzati.</span><span class="sxs-lookup"><span data-stu-id="f7939-1196">If the total number of bytes specified in the queue’s memory area is not evenly divisible by the specified message size, the remaining bytes in the memory area are not used.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1197">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1197">Parameters</span></span>

- <span data-ttu-id="f7939-1198">**queue_ptr**: puntatore a un blocco di controllo della coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="f7939-1198">**queue_ptr**: Pointer to a message queue control block.</span></span>
- <span data-ttu-id="f7939-1199">**name_ptr**: puntatore al nome della coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="f7939-1199">**name_ptr**: Pointer to the name of the message queue.</span></span>
- <span data-ttu-id="f7939-1200">**message_size**: specifica le dimensioni di ogni messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1200">**message_size**: Specifies the size of each message in the queue.</span></span> <span data-ttu-id="f7939-1201">Le dimensioni dei messaggi variano da Word a 1 32 bit a parole a 16 32 bit.</span><span class="sxs-lookup"><span data-stu-id="f7939-1201">Message sizes range from 1 32-bit word to 16 32-bit words.</span></span> <span data-ttu-id="f7939-1202">Le opzioni valide per le dimensioni dei messaggi sono valori numerici compresi tra 1 e 16.</span><span class="sxs-lookup"><span data-stu-id="f7939-1202">Valid message size options are numerical values from 1 through 16, inclusive.</span></span>
- <span data-ttu-id="f7939-1203">**queue_start**: indirizzo iniziale della coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="f7939-1203">**queue_start**: Starting address of the message queue.</span></span> <span data-ttu-id="f7939-1204">L'indirizzo iniziale deve essere allineato alle dimensioni del tipo di dati ULONG.</span><span class="sxs-lookup"><span data-stu-id="f7939-1204">The starting address must be aligned to the size of the ULONG data type.</span></span>
- <span data-ttu-id="f7939-1205">**queue_size**: numero totale di byte disponibili per la coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="f7939-1205">**queue_size**: Total number of bytes available for the message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1206">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1206">Return Values</span></span>

- <span data-ttu-id="f7939-1207">**TX_SUCCESS**: (0x00) la creazione della coda di messaggi è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1207">**TX_SUCCESS**: (0x00) Successful message queue creation.</span></span>
- <span data-ttu-id="f7939-1208">TX_QUEUE_ERROR: (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1208">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span> <span data-ttu-id="f7939-1209">Il puntatore è NULL o la coda è già stata creata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1209">Either the pointer is NULL or the queue is already created.</span></span>
- <span data-ttu-id="f7939-1210">TX_PTR_ERROR: (0x03) indirizzo iniziale non valido della coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="f7939-1210">TX_PTR_ERROR: (0x03) Invalid starting address of the message queue.</span></span>
- <span data-ttu-id="f7939-1211">TX_SIZE_ERROR: le dimensioni della coda di messaggi (0x05) non sono valide.</span><span class="sxs-lookup"><span data-stu-id="f7939-1211">TX_SIZE_ERROR: (0x05) Size of message queue is invalid.</span></span>
- <span data-ttu-id="f7939-1212">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1212">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1213">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1213">Allowed From</span></span>

<span data-ttu-id="f7939-1214">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="f7939-1214">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1215">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1215">Preemption Possible</span></span>

<span data-ttu-id="f7939-1216">No</span><span class="sxs-lookup"><span data-stu-id="f7939-1216">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1217">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1217">Example</span></span>

```C
TX_QUEUE     my_queue;
UINT         status;

/* Create a message queue whose total size is 2000 bytes
   starting at address 0x300000. Each message in this
   queue is defined to be 4 32-bit words long. */
status = tx_queue_create(&my_queue, "my_queue_name",
            4, (VOID *) 0x300000, 2000);

/* If status equals TX_SUCCESS, my_queue contains room
   for storing 125 messages (2000 bytes/ 16 bytes per
   message). */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1218">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1218">See Also</span></span>

- <span data-ttu-id="f7939-1219">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1219">tx_queue_delete</span></span>
- <span data-ttu-id="f7939-1220">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f7939-1220">tx_queue_flush</span></span>
- <span data-ttu-id="f7939-1221">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1221">tx_queue_front_send</span></span>
- <span data-ttu-id="f7939-1222">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1222">tx_queue_info_get</span></span>
- <span data-ttu-id="f7939-1223">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1223">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="f7939-1224">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1224">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1225">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1225">tx_queue_prioritize</span></span>
- <span data-ttu-id="f7939-1226">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f7939-1226">tx_queue_receive</span></span>
- <span data-ttu-id="f7939-1227">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1227">tx_queue_send</span></span>
- <span data-ttu-id="f7939-1228">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1228">tx_queue_send_notify</span></span>

## <a name="tx_queue_delete"></a><span data-ttu-id="f7939-1229">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1229">tx_queue_delete</span></span>

<span data-ttu-id="f7939-1230">Elimina coda messaggi</span><span class="sxs-lookup"><span data-stu-id="f7939-1230">Delete message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1231">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1231">Prototype</span></span>

```C
UINT tx_queue_delete(TX_QUEUE *queue_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-1232">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1232">Description</span></span>

<span data-ttu-id="f7939-1233">Questo servizio Elimina la coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1233">This service deletes the specified message queue.</span></span> <span data-ttu-id="f7939-1234">Tutti i thread sospesi in attesa di un messaggio da questa coda vengono ripresi e viene fornito un TX_DELETED stato restituito.</span><span class="sxs-lookup"><span data-stu-id="f7939-1234">All threads suspended waiting for a message from this queue are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1235">Prima di eliminare la coda, l'applicazione deve assicurarsi che qualsiasi callback di invio notifica per questa coda venga completato (o disabilitato).</span><span class="sxs-lookup"><span data-stu-id="f7939-1235">The application must ensure that any send notify callback for this queue is completed (or disabled) before deleting the queue.</span></span> <span data-ttu-id="f7939-1236">Inoltre, l'applicazione deve impedire l'uso futuro di una coda eliminata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1236">In addition, the application must prevent any future use of a deleted queue.</span></span>

<span data-ttu-id="f7939-1237">*È inoltre responsabilità dell'applicazione gestire l'area di memoria associata alla coda, disponibile al termine del servizio.*</span><span class="sxs-lookup"><span data-stu-id="f7939-1237">*It is also the application's responsibility to manage the memory area associated with the queue, which is available after this service completes.*</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1238">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1238">Parameters</span></span> 

- <span data-ttu-id="f7939-1239">**queue_ptr**: puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1239">**queue_ptr**: Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1240">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1240">Return Values</span></span>

- <span data-ttu-id="f7939-1241">**TX_SUCCESS**: (0x00) eliminazione della coda di messaggi riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1241">**TX_SUCCESS**: (0x00) Successful message queue deletion.</span></span>
- <span data-ttu-id="f7939-1242">TX_QUEUE_ERROR: (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1242">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="f7939-1243">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1243">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1244">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1244">Allowed From</span></span>

<span data-ttu-id="f7939-1245">Thread</span><span class="sxs-lookup"><span data-stu-id="f7939-1245">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1246">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1246">Preemption Possible</span></span>

<span data-ttu-id="f7939-1247">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1247">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1248">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1248">Example</span></span>

```C
TX_QUEUE     my_queue;
UINT         status;

/* Delete entire message queue. Assume that the queue
   has already been created with a call to
   tx_queue_create. */
status = tx_queue_delete(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1249">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1249">See Also</span></span>

- <span data-ttu-id="f7939-1250">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1250">tx_queue_create</span></span>
- <span data-ttu-id="f7939-1251">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f7939-1251">tx_queue_flush</span></span>
- <span data-ttu-id="f7939-1252">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1252">tx_queue_front_send</span></span>
- <span data-ttu-id="f7939-1253">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1253">tx_queue_info_get</span></span>
- <span data-ttu-id="f7939-1254">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1254">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="f7939-1255">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1255">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1256">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1256">tx_queue_prioritize</span></span>
- <span data-ttu-id="f7939-1257">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f7939-1257">tx_queue_receive</span></span>
- <span data-ttu-id="f7939-1258">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1258">tx_queue_send</span></span>
- <span data-ttu-id="f7939-1259">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1259">tx_queue_send_notify</span></span>

## <a name="tx_queue_flush"></a><span data-ttu-id="f7939-1260">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f7939-1260">tx_queue_flush</span></span>

<span data-ttu-id="f7939-1261">Messaggi vuoti nella coda di messaggi</span><span class="sxs-lookup"><span data-stu-id="f7939-1261">Empty messages in message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1262">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1262">Prototype</span></span>

```C
UINT tx_queue_flush(TX_QUEUE *queue_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-1263">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1263">Description</span></span>

<span data-ttu-id="f7939-1264">Questo servizio Elimina tutti i messaggi archiviati nella coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1264">This service deletes all messages stored in the specified message queue.</span></span> <span data-ttu-id="f7939-1265">Se la coda è piena, i messaggi di tutti i thread sospesi vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="f7939-1265">If the queue is full, messages of all suspended threads are discarded.</span></span> <span data-ttu-id="f7939-1266">Ogni thread sospeso viene quindi ripreso con uno stato restituito che indica che l'invio del messaggio è stato completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="f7939-1266">Each suspended thread is then resumed with a return status that indicates the message send was successful.</span></span> <span data-ttu-id="f7939-1267">Se la coda è vuota, il servizio non esegue alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1267">If the queue is empty, this service does nothing.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1268">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1268">Parameters</span></span> 

- <span data-ttu-id="f7939-1269">**queue_ptr**: puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1269">**queue_ptr**: Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1270">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1270">Return Values</span></span>

- <span data-ttu-id="f7939-1271">**TX_SUCCESS**: (0x00) lo svuotamento della coda messaggi è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-1271">**TX_SUCCESS**: (0x00) Successful message queue flush.</span></span>
- <span data-ttu-id="f7939-1272">TX_QUEUE_ERROR: (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1272">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1273">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1273">Allowed From</span></span>

<span data-ttu-id="f7939-1274">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1274">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1275">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1275">Preemption Possible</span></span>

<span data-ttu-id="f7939-1276">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1276">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1277">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1277">Example</span></span>

```c
TX_QUEUE     my_queue;
UINT         status;

/* Flush out all pending messages in the specified message
   queue. Assume that the queue has already been created
   with a call to tx_queue_create. */
status =  tx_queue_flush(&my_queue);

/* If status equals TX_SUCCESS, the message queue is
    empty. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1278">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1278">See Also</span></span>

- <span data-ttu-id="f7939-1279">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1279">tx_queue_create</span></span>
- <span data-ttu-id="f7939-1280">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1280">tx_queue_delete</span></span>
- <span data-ttu-id="f7939-1281">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1281">tx_queue_front_send</span></span>
- <span data-ttu-id="f7939-1282">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1282">tx_queue_info_get</span></span>
- <span data-ttu-id="f7939-1283">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1283">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="f7939-1284">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1284">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1285">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1285">tx_queue_prioritize</span></span>
- <span data-ttu-id="f7939-1286">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f7939-1286">tx_queue_receive</span></span>
- <span data-ttu-id="f7939-1287">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1287">tx_queue_send</span></span>
- <span data-ttu-id="f7939-1288">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1288">tx_queue_send_notify</span></span>

## <a name="tx_queue_front_send"></a><span data-ttu-id="f7939-1289">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1289">tx_queue_front_send</span></span>

<span data-ttu-id="f7939-1290">Invia messaggio all'inizio della coda</span><span class="sxs-lookup"><span data-stu-id="f7939-1290">Send message to the front of queue</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1291">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1291">Prototype</span></span>

```C
UINT tx_queue_front_send(TX_QUEUE *queue_ptr,
                           VOID *source_ptr, ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="f7939-1292">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1292">Description</span></span>

<span data-ttu-id="f7939-1293">Questo servizio invia un messaggio al percorso front della coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1293">This service sends a message to the front location of the specified message queue.</span></span> <span data-ttu-id="f7939-1294">Il messaggio viene **copiato** all'inizio della coda dall'area di memoria specificata dal puntatore di origine.</span><span class="sxs-lookup"><span data-stu-id="f7939-1294">The message is **copied** to the front of the queue from the memory area specified by the source pointer.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1295">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1295">Parameters</span></span>

- <span data-ttu-id="f7939-1296">**queue_ptr**: puntatore a un blocco di controllo della coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="f7939-1296">**queue_ptr**: Pointer to a message queue control block.</span></span>
- <span data-ttu-id="f7939-1297">**source_ptr**: puntatore al messaggio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1297">**source_ptr**: Pointer to the message.</span></span>
- <span data-ttu-id="f7939-1298">**WAIT_OPTION**: definisce il comportamento del servizio se la coda di messaggi è piena.</span><span class="sxs-lookup"><span data-stu-id="f7939-1298">**wait_option**: Defines how the service behaves if the message queue is full.</span></span> <span data-ttu-id="f7939-1299">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="f7939-1299">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="f7939-1300">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="f7939-1300">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="f7939-1301">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="f7939-1301">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="f7939-1302">valore di timeout: (0x00000001 tramite 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="f7939-1302">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="f7939-1303">La selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1303">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="f7939-1304">*Questa è l'unica opzione valida se il servizio viene chiamato da un non thread. ad esempio, inizializzazione, timer o ISR.*</span><span class="sxs-lookup"><span data-stu-id="f7939-1304">*This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.*</span></span>

    <span data-ttu-id="f7939-1305">Se si seleziona TX_WAIT_FOREVER, il thread chiamante sospenderà per un tempo illimitato fino a quando non sarà disponibile spazio nella coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1305">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until there is room in the queue.</span></span>

    <span data-ttu-id="f7939-1306">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi in attesa di spazio nella coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1306">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for room in the queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1307">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1307">Return Values</span></span>

- <span data-ttu-id="f7939-1308">**TX_SUCCESS**: (0x00) l'invio del messaggio è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-1308">**TX_SUCCESS**: (0x00) Successful sending of message.</span></span>
- <span data-ttu-id="f7939-1309">**TX_DELETED**: (0x01) la coda di messaggi è stata eliminata durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1309">**TX_DELETED**: (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="f7939-1310">**TX_QUEUE_FULL**: il servizio (0x0B) non è stato in grado di inviare il messaggio perché la coda era piena per la durata del tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1310">**TX_QUEUE_FULL**: (0x0B) Service was unable to send message because the queue was full for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="f7939-1311">**TX_WAIT_ABORTED**: la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-1311">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="f7939-1312">TX_QUEUE_ERROR: (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1312">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="f7939-1313">TX_PTR_ERROR: (0x03) puntatore di origine non valido per il messaggio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1313">TX_PTR_ERROR: (0x03) Invalid source pointer for message.</span></span>
- <span data-ttu-id="f7939-1314">TX_WAIT_ERROR: (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1314">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1315">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1315">Allowed From</span></span>

<span data-ttu-id="f7939-1316">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1316">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1317">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1317">Preemption Possible</span></span>

<span data-ttu-id="f7939-1318">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1318">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1319">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1319">Example</span></span>

```C
TX_QUEUE     my_queue;
UINT         status;
ULONG        my_message[4];

/* Send a message to the front of "my_queue." Return
   immediately, regardless of success. This wait
   option is used for calls from initialization, timers,
   and ISRs. */
status = tx_queue_front_send(&my_queue, my_message,
            TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is at the front
   of the specified queue. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1320">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1320">See Also</span></span>

- <span data-ttu-id="f7939-1321">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1321">tx_queue_create</span></span>
- <span data-ttu-id="f7939-1322">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1322">tx_queue_delete</span></span>
- <span data-ttu-id="f7939-1323">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f7939-1323">tx_queue_flush</span></span>
- <span data-ttu-id="f7939-1324">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1324">tx_queue_info_get</span></span>
- <span data-ttu-id="f7939-1325">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1325">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="f7939-1326">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1326">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1327">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1327">tx_queue_prioritize</span></span>
- <span data-ttu-id="f7939-1328">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f7939-1328">tx_queue_receive</span></span>
- <span data-ttu-id="f7939-1329">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1329">tx_queue_send</span></span>
- <span data-ttu-id="f7939-1330">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1330">tx_queue_send_notify</span></span>

## <a name="tx_queue_info_get"></a><span data-ttu-id="f7939-1331">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1331">tx_queue_info_get</span></span>

<span data-ttu-id="f7939-1332">Recuperare le informazioni sulla coda</span><span class="sxs-lookup"><span data-stu-id="f7939-1332">Retrieve information about queue</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1333">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1333">Prototype</span></span>

```C
UINT tx_queue_info_get(TX_QUEUE *queue_ptr, CHAR **name,
        ULONG *enqueued, ULONG *available_storage
        TX_THREAD **first_suspended, ULONG *suspended_count,
        TX_QUEUE **next_queue);
```
### <a name="description"></a><span data-ttu-id="f7939-1334">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1334">Description</span></span>

<span data-ttu-id="f7939-1335">Questo servizio recupera le informazioni sulla coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1335">This service retrieves information about the specified message queue.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1336">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1336">Parameters</span></span>

- <span data-ttu-id="f7939-1337">**queue_ptr**: puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1337">**queue_ptr**: Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="f7939-1338">**Name**: puntatore alla destinazione per il puntatore al nome della coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1338">**name**: Pointer to destination for the pointer to the queue’s name.</span></span>
- <span data-ttu-id="f7939-1339">**accodato**: puntatore alla destinazione per il numero di messaggi attualmente presenti nella coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1339">**enqueued**: Pointer to destination for the number of messages currently in the queue.</span></span>
- <span data-ttu-id="f7939-1340">**available_storage**: puntatore alla destinazione per il numero di messaggi per i quali la coda ha attualmente spazio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1340">**available_storage**: Pointer to destination for the number of messages the queue currently has space for.</span></span>
- <span data-ttu-id="f7939-1341">**first_suspended**: puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione della coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1341">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this queue.</span></span>
- <span data-ttu-id="f7939-1342">**suspended_count**: puntatore alla destinazione per il numero di thread attualmente sospesi in questa coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1342">**suspended_count**: Pointer to destination for the number of threads currently suspended on this queue.</span></span>
- <span data-ttu-id="f7939-1343">**next_queue**: puntatore alla destinazione per il puntatore della coda creata successiva.</span><span class="sxs-lookup"><span data-stu-id="f7939-1343">**next_queue**: Pointer to destination for the pointer of the next created queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1344">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1344">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1345">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1345">Return Values</span></span>

- <span data-ttu-id="f7939-1346">**TX_SUCCESS**: (0x00) informazioni della coda riuscite Get.</span><span class="sxs-lookup"><span data-stu-id="f7939-1346">**TX_SUCCESS**: (0x00) Successful queue information get.</span></span>
- <span data-ttu-id="f7939-1347">TX_QUEUE_ERROR: (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1347">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1348">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1348">Allowed From</span></span>

<span data-ttu-id="f7939-1349">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1349">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1350">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1350">Preemption Possible</span></span>

<span data-ttu-id="f7939-1351">No</span><span class="sxs-lookup"><span data-stu-id="f7939-1351">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1352">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1352">Example</span></span>

```C
TX_QUEUE     my_queue;
CHAR         *name;
ULONG        enqueued;
ULONG        available_storage;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_QUEUE     *next_queue;
UINT         status;

/* Retrieve information about the previously created
   message queue "my_queue." */
status = tx_queue_info_get(&my_queue, &name,
            &enqueued, &available_storage,
            &first_suspended, &suspended_count,
            &next_queue);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1353">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1353">See Also</span></span>

- <span data-ttu-id="f7939-1354">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1354">tx_queue_create</span></span>
- <span data-ttu-id="f7939-1355">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1355">tx_queue_delete</span></span>
- <span data-ttu-id="f7939-1356">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f7939-1356">tx_queue_flush</span></span>
- <span data-ttu-id="f7939-1357">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1357">tx_queue_front_send</span></span>
- <span data-ttu-id="f7939-1358">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1358">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="f7939-1359">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1359">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1360">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1360">tx_queue_prioritize</span></span>
- <span data-ttu-id="f7939-1361">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f7939-1361">tx_queue_receive</span></span>
- <span data-ttu-id="f7939-1362">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1362">tx_queue_send</span></span>
- <span data-ttu-id="f7939-1363">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1363">tx_queue_send_notify</span></span>

## <a name="tx_queue_performance_info_get"></a><span data-ttu-id="f7939-1364">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1364">tx_queue_performance_info_get</span></span>

<span data-ttu-id="f7939-1365">Ottenere le informazioni sulle prestazioni della coda</span><span class="sxs-lookup"><span data-stu-id="f7939-1365">Get queue performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1366">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1366">Prototype</span></span>

```C
UINT  tx_queue_performance_info_get(TX_QUEUE *queue_ptr,
        ULONG *messages_sent, ULONG *messages_received,
        ULONG *empty_suspensions, ULONG *full_suspensions,
        ULONG *full_errors, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="f7939-1367">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1367">Description</span></span>

<span data-ttu-id="f7939-1368">Questo servizio recupera le informazioni sulle prestazioni relative alla coda specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1368">This service retrieves performance information about the specified queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1369">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_QUEUE_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1369">The ThreadX SMP library and application must be built with **TX_QUEUE_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1370">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1370">Parameters</span></span>

- <span data-ttu-id="f7939-1371">**queue_ptr**: puntatore alla coda creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1371">**queue_ptr**: Pointer to previously created queue.</span></span>
- <span data-ttu-id="f7939-1372">**messages_sent**: puntatore alla destinazione per il numero di richieste di invio eseguite su questa coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1372">**messages_sent**: Pointer to destination for the number of send requests performed on this queue.</span></span>
- <span data-ttu-id="f7939-1373">**messages_received**: puntatore alla destinazione per il numero di richieste di ricezione eseguite in questa coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1373">**messages_received**: Pointer to destination for the number of receive requests performed on this queue.</span></span>
- <span data-ttu-id="f7939-1374">**empty_suspensions**: puntatore alla destinazione per il numero di sospensioni vuote della coda in questa coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1374">**empty_suspensions**: Pointer to destination for the number of queue empty suspensions on this queue.</span></span>
- <span data-ttu-id="f7939-1375">**full_suspensions**: puntatore alla destinazione per il numero di sospensioni complete della coda in questa coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1375">**full_suspensions**: Pointer to destination for the number of queue full suspensions on this queue.</span></span>
- <span data-ttu-id="f7939-1376">**full_errors**: puntatore alla destinazione per il numero di errori della coda completa in questa coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1376">**full_errors**: Pointer to destination for the number of queue full errors on this queue.</span></span>
- <span data-ttu-id="f7939-1377">**timeout**: puntatore alla destinazione per il numero di timeout di sospensione del thread in questa coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1377">**timeouts**: Pointer to destination for the number of thread suspension timeouts on this queue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1378">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1378">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1379">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1379">Return Values</span></span>

- <span data-ttu-id="f7939-1380">**TX_SUCCESS**: (0x00) ottenere le prestazioni della coda riuscite.</span><span class="sxs-lookup"><span data-stu-id="f7939-1380">**TX_SUCCESS**: (0x00) Successful queue performance get.</span></span>
- <span data-ttu-id="f7939-1381">**TX_PTR_ERROR**: (0x03) puntatore della coda non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1381">**TX_PTR_ERROR**: (0x03) Invalid queue pointer.</span></span>
- <span data-ttu-id="f7939-1382">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-1382">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1383">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1383">Allowed From</span></span>

<span data-ttu-id="f7939-1384">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1384">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1385">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1385">Example</span></span>

```C
TX_QUEUE     my_queue;
ULONG        messages_sent;
ULONG        messages_received;
ULONG        empty_suspensions;
ULONG        full_suspensions;
ULONG        full_errors;
ULONG        timeouts;

/* Retrieve performance information on the previously created
   queue. */
status = tx_queue_performance_info_get(&my_queue, &messages_sent,
            &messages_received, &empty_suspensions,
            &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1386">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1386">See Also</span></span>

- <span data-ttu-id="f7939-1387">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1387">tx_queue_create</span></span>
- <span data-ttu-id="f7939-1388">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1388">tx_queue_delete</span></span>
- <span data-ttu-id="f7939-1389">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f7939-1389">tx_queue_flush</span></span>
- <span data-ttu-id="f7939-1390">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1390">tx_queue_front_send</span></span>
- <span data-ttu-id="f7939-1391">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1391">tx_queue_info_get</span></span>
- <span data-ttu-id="f7939-1392">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1392">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1393">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1393">tx_queue_prioritize</span></span>
- <span data-ttu-id="f7939-1394">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f7939-1394">tx_queue_receive</span></span>
- <span data-ttu-id="f7939-1395">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1395">tx_queue_send</span></span>
- <span data-ttu-id="f7939-1396">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1396">tx_queue_send_notify</span></span>

## <a name="tx_queue_performance_system_info_get"></a><span data-ttu-id="f7939-1397">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1397">tx_queue_performance_system_info_get</span></span>

<span data-ttu-id="f7939-1398">Ottenere informazioni sulle prestazioni del sistema di Accodamento</span><span class="sxs-lookup"><span data-stu-id="f7939-1398">Get queue system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1399">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1399">Prototype</span></span>

```C
UINT  tx_queue_performance_system_info_get(ULONG *messages_sent,
        ULONG *messages_received, ULONG *empty_suspensions,
        ULONG *full_suspensions, ULONG *full_errors,
        ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="f7939-1400">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1400">Description</span></span>

<span data-ttu-id="f7939-1401">Questo servizio recupera le informazioni sulle prestazioni relative a tutte le code nel sistema.</span><span class="sxs-lookup"><span data-stu-id="f7939-1401">This service retrieves performance information about all the queues in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1402">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_QUEUE_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1402">The ThreadX SMP library and application must be built with **TX_QUEUE_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1403">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1403">Parameters</span></span>

- <span data-ttu-id="f7939-1404">**messages_sent**: puntatore alla destinazione per il numero totale di richieste di invio eseguite su tutte le code.</span><span class="sxs-lookup"><span data-stu-id="f7939-1404">**messages_sent**: Pointer to destination for the total number of send requests performed on all queues.</span></span>
- <span data-ttu-id="f7939-1405">**messages_received**: puntatore alla destinazione per il numero totale di richieste di ricezione eseguite su tutte le code.</span><span class="sxs-lookup"><span data-stu-id="f7939-1405">**messages_received**: Pointer to destination for the total number of receive requests performed on all queues.</span></span>
- <span data-ttu-id="f7939-1406">**empty_suspensions**: puntatore alla destinazione per il numero totale di sospensioni vuote in coda in tutte le code.</span><span class="sxs-lookup"><span data-stu-id="f7939-1406">**empty_suspensions**: Pointer to destination for the total number of queue empty suspensions on all queues.</span></span>
- <span data-ttu-id="f7939-1407">**full_suspensions**: puntatore alla destinazione per il numero totale di sospensioni complete della coda su tutte le code.</span><span class="sxs-lookup"><span data-stu-id="f7939-1407">**full_suspensions**: Pointer to destination for the total number of queue full suspensions on all queues.</span></span>
- <span data-ttu-id="f7939-1408">**full_errors**: puntatore alla destinazione per il numero totale di errori della coda completa su tutte le code.</span><span class="sxs-lookup"><span data-stu-id="f7939-1408">**full_errors**: Pointer to destination for the total number of queue full errors on all queues.</span></span>
- <span data-ttu-id="f7939-1409">**timeout**: puntatore alla destinazione per il numero totale di timeout di sospensione del thread in tutte le code.</span><span class="sxs-lookup"><span data-stu-id="f7939-1409">**timeouts**: Pointer to destination for the total number of thread suspension timeouts on all queues.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1410">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1410">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1411">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1411">Return Values</span></span>

- <span data-ttu-id="f7939-1412">**TX_SUCCESS**: (0x00) esito positivo delle prestazioni del sistema di Accodamento.</span><span class="sxs-lookup"><span data-stu-id="f7939-1412">**TX_SUCCESS**: (0x00) Successful queue system performance get.</span></span>
- <span data-ttu-id="f7939-1413">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-1413">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1414">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1414">Allowed From</span></span>

<span data-ttu-id="f7939-1415">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1415">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1416">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1416">Example</span></span>

```c
ULONG         messages_sent;
ULONG         messages_received;
ULONG         empty_suspensions;
ULONG         full_suspensions;
ULONG         full_errors;
ULONG         timeouts;

/* Retrieve performance information on all previously created
   queues. */
status = tx_queue_performance_system_info_get(&messages_sent,
            &messages_received, &empty_suspensions,
            &full_suspensions, &full_errors, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1417">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1417">See Also</span></span>

- <span data-ttu-id="f7939-1418">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1418">tx_queue_create</span></span>
- <span data-ttu-id="f7939-1419">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1419">tx_queue_delete</span></span>
- <span data-ttu-id="f7939-1420">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f7939-1420">tx_queue_flush</span></span>
- <span data-ttu-id="f7939-1421">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1421">tx_queue_front_send</span></span>
- <span data-ttu-id="f7939-1422">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1422">tx_queue_info_get</span></span>
- <span data-ttu-id="f7939-1423">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1423">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="f7939-1424">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1424">tx_queue_prioritize</span></span>
- <span data-ttu-id="f7939-1425">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f7939-1425">tx_queue_receive</span></span>
- <span data-ttu-id="f7939-1426">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1426">tx_queue_send</span></span>
- <span data-ttu-id="f7939-1427">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1427">tx_queue_send_notify</span></span>

## <a name="tx_queue_prioritize"></a><span data-ttu-id="f7939-1428">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1428">tx_queue_prioritize</span></span>

<span data-ttu-id="f7939-1429">Elencare le priorità di sospensione della coda</span><span class="sxs-lookup"><span data-stu-id="f7939-1429">Prioritize queue suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1430">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1430">Prototype</span></span>

```C
UINT tx_queue_prioritize(TX_QUEUE *queue_ptr);
```

### <a name="description"></a><span data-ttu-id="f7939-1431">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1431">Description</span></span>

<span data-ttu-id="f7939-1432">Questo servizio posiziona il thread con priorità più elevata sospeso per un messaggio o per inserire un messaggio in questa coda all'inizio dell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="f7939-1432">This service places the highest priority thread suspended for a message (or to place a message) on this queue at the front of the suspension list.</span></span> <span data-ttu-id="f7939-1433">Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.</span><span class="sxs-lookup"><span data-stu-id="f7939-1433">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1434">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1434">Parameters</span></span> 

- <span data-ttu-id="f7939-1435">**queue_ptr**: puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1435">**queue_ptr**: Pointer to a previously created message queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1436">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1436">Return Values</span></span>

- <span data-ttu-id="f7939-1437">**TX_SUCCESS**: (0x00) priorità della coda riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1437">**TX_SUCCESS**: (0x00) Successful queue prioritize.</span></span>
- <span data-ttu-id="f7939-1438">TX_QUEUE_ERROR: (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1438">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1439">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1439">Allowed From</span></span>

<span data-ttu-id="f7939-1440">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1440">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1441">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1441">Preemption Possible</span></span>

<span data-ttu-id="f7939-1442">No</span><span class="sxs-lookup"><span data-stu-id="f7939-1442">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1443">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1443">Example</span></span>

```C
TX_QUEUE     my_queue;
UINT         status;

/* Ensure that the highest priority thread will receive
   the next message placed on this queue. */
status = tx_queue_prioritize(&my_queue);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_queue_send or tx_queue_front_send call made
   to this queue will wake up this thread. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1444">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1444">See Also</span></span>

- <span data-ttu-id="f7939-1445">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1445">tx_queue_create</span></span>
- <span data-ttu-id="f7939-1446">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1446">tx_queue_delete</span></span>
- <span data-ttu-id="f7939-1447">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f7939-1447">tx_queue_flush</span></span>
- <span data-ttu-id="f7939-1448">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1448">tx_queue_front_send</span></span>
- <span data-ttu-id="f7939-1449">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1449">tx_queue_info_get</span></span>
- <span data-ttu-id="f7939-1450">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1450">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="f7939-1451">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1451">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1452">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f7939-1452">tx_queue_receive</span></span>
- <span data-ttu-id="f7939-1453">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1453">tx_queue_send</span></span>
- <span data-ttu-id="f7939-1454">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1454">tx_queue_send_notify</span></span>

## <a name="tx_queue_receive"></a><span data-ttu-id="f7939-1455">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f7939-1455">tx_queue_receive</span></span>

<span data-ttu-id="f7939-1456">Ottieni messaggio da coda messaggi</span><span class="sxs-lookup"><span data-stu-id="f7939-1456">Get message from message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1457">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1457">Prototype</span></span>

```C
UINT tx_queue_receive(TX_QUEUE *queue_ptr,
                          VOID *destination_ptr, ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="f7939-1458">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1458">Description</span></span>

<span data-ttu-id="f7939-1459">Questo servizio recupera un messaggio dalla coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1459">This service retrieves a message from the specified message queue.</span></span> <span data-ttu-id="f7939-1460">Il messaggio recuperato viene **copiato** dalla coda nell'area di memoria specificata dal puntatore di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1460">The retrieved message is **copied** from the queue into the memory area specified by the destination pointer.</span></span> <span data-ttu-id="f7939-1461">Il messaggio viene quindi rimosso dalla coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1461">That message is then removed from the queue.</span></span>

> [!WARNING]
> <span data-ttu-id="f7939-1462">L'area di memoria di destinazione specificata deve essere sufficientemente grande da contenere il messaggio; ovvero, la destinazione del messaggio a cui punta **destination_ptr** deve essere almeno uguale alla dimensione del messaggio per la coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1462">The specified destination memory area must be large enough to hold the message; i.e., the message destination pointed to by **destination_ptr** must be at least as large as the message size for this queue.</span></span> <span data-ttu-id="f7939-1463">In caso contrario, se la destinazione non è sufficientemente grande, il danneggiamento della memoria si verifica nella seguente area di memoria.</span><span class="sxs-lookup"><span data-stu-id="f7939-1463">Otherwise, if the destination is not large enough, memory corruption occurs in the following memory area.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1464">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1464">Parameters</span></span>

- <span data-ttu-id="f7939-1465">**queue_ptr**: puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1465">**queue_ptr**: Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="f7939-1466">**destination_ptr**: percorso in cui copiare il messaggio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1466">**destination_ptr**: Location of where to copy the message.</span></span>
- <span data-ttu-id="f7939-1467">**WAIT_OPTION**: definisce il comportamento del servizio se la coda di messaggi è vuota.</span><span class="sxs-lookup"><span data-stu-id="f7939-1467">**wait_option**: Defines how the service behaves if the message queue is empty.</span></span> <span data-ttu-id="f7939-1468">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="f7939-1468">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="f7939-1469">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="f7939-1469">**TX_NO_WAIT**: (0x00000000)</span></span> 
    - <span data-ttu-id="f7939-1470">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="f7939-1470">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span> 
    - <span data-ttu-id="f7939-1471">valore di timeout: (0x00000001 tramite 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="f7939-1471">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="f7939-1472">La selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1472">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="f7939-1473">Questa è l'unica opzione valida se il servizio viene chiamato da un non thread. ad esempio, inizializzazione, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-1473">This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.</span></span>

    <span data-ttu-id="f7939-1474">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando non sarà disponibile un messaggio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1474">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a message is available.</span></span>

    <span data-ttu-id="f7939-1475">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1475">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a message.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1476">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1476">Return Values</span></span>

- <span data-ttu-id="f7939-1477">**TX_SUCCESS**: (0x00) il recupero del messaggio è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-1477">**TX_SUCCESS**: (0x00) Successful retrieval of message.</span></span>
- <span data-ttu-id="f7939-1478">**TX_DELETED**: (0x01) la coda di messaggi è stata eliminata durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1478">**TX_DELETED**: (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="f7939-1479">**TX_QUEUE_EMPTY**: il servizio (0x0A) non è stato in grado di recuperare un messaggio perché la coda è vuota per la durata del tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1479">**TX_QUEUE_EMPTY**: (0x0A) Service was unable to retrieve a message because the queue was empty for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="f7939-1480">**TX_WAIT_ABORTED**: la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-1480">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="f7939-1481">TX_QUEUE_ERROR: (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1481">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="f7939-1482">TX_PTR_ERROR: (0x03) puntatore di destinazione non valido per il messaggio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1482">TX_PTR_ERROR: (0x03) Invalid destination pointer for message.</span></span>
- <span data-ttu-id="f7939-1483">TX_WAIT_ERROR: (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1483">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1484">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1484">Allowed From</span></span>

<span data-ttu-id="f7939-1485">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1485">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1486">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1486">Preemption Possible</span></span>

<span data-ttu-id="f7939-1487">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1487">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1488">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1488">Example</span></span>

```C
TX_QUEUE     my_queue;
UINT         status;
ULONG my_message[4];

/* Retrieve a message from "my_queue." If the queue is
   empty, suspend until a message is present. Note that
   this suspension is only possible from application
   threads. */
status =  tx_queue_receive(&my_queue, my_message,
                          TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the message is in
   "my_message." */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1489">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1489">See Also</span></span>

- <span data-ttu-id="f7939-1490">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1490">tx_queue_create</span></span>
- <span data-ttu-id="f7939-1491">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1491">tx_queue_delete</span></span>
- <span data-ttu-id="f7939-1492">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f7939-1492">tx_queue_flush</span></span>
- <span data-ttu-id="f7939-1493">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1493">tx_queue_front_send</span></span>
- <span data-ttu-id="f7939-1494">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1494">tx_queue_info_get</span></span>
- <span data-ttu-id="f7939-1495">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1495">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="f7939-1496">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1496">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1497">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1497">tx_queue_prioritize</span></span>
- <span data-ttu-id="f7939-1498">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1498">tx_queue_send</span></span>
- <span data-ttu-id="f7939-1499">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1499">tx_queue_send_notify</span></span>

## <a name="tx_queue_send"></a><span data-ttu-id="f7939-1500">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1500">tx_queue_send</span></span>

<span data-ttu-id="f7939-1501">Invia messaggio alla coda di messaggi</span><span class="sxs-lookup"><span data-stu-id="f7939-1501">Send message to message queue</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1502">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1502">Prototype</span></span>

```C
UINT tx_queue_send(TX_QUEUE *queue_ptr,
                          VOID *source_ptr, ULONG wait_option);
```
### <a name="description"></a><span data-ttu-id="f7939-1503">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1503">Description</span></span>

<span data-ttu-id="f7939-1504">Questo servizio invia un messaggio alla coda di messaggi specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1504">This service sends a message to the specified message queue.</span></span> <span data-ttu-id="f7939-1505">Il messaggio inviato viene **copiato** nella coda dall'area di memoria specificata dal puntatore di origine.</span><span class="sxs-lookup"><span data-stu-id="f7939-1505">The sent message is **copied** to the queue from the memory area specified by the source pointer.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1506">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1506">Parameters</span></span>

- <span data-ttu-id="f7939-1507">**queue_ptr**: puntatore a una coda di messaggi creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1507">**queue_ptr**: Pointer to a previously created message queue.</span></span>
- <span data-ttu-id="f7939-1508">**source_ptr**: puntatore al messaggio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1508">**source_ptr**: Pointer to the message.</span></span>
- <span data-ttu-id="f7939-1509">**WAIT_OPTION**: definisce il comportamento del servizio se la coda di messaggi è piena.</span><span class="sxs-lookup"><span data-stu-id="f7939-1509">**wait_option**: Defines how the service behaves if the message queue is full.</span></span> <span data-ttu-id="f7939-1510">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="f7939-1510">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="f7939-1511">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="f7939-1511">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="f7939-1512">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="f7939-1512">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="f7939-1513">valore di timeout: (0x00000001 tramite 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="f7939-1513">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="f7939-1514">La selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1514">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="f7939-1515">*Questa è l'unica opzione valida se il servizio viene chiamato da un non thread. ad esempio, inizializzazione, timer o ISR.*</span><span class="sxs-lookup"><span data-stu-id="f7939-1515">*This is the only valid option if the service is called from a non-thread; e.g., Initialization, timer, or ISR.*</span></span>

    <span data-ttu-id="f7939-1516">Se si seleziona TX_WAIT_FOREVER, il thread chiamante sospenderà per un tempo illimitato fino a quando non sarà disponibile spazio nella coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1516">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until there is room in the queue.</span></span>

    <span data-ttu-id="f7939-1517">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi in attesa di spazio nella coda.</span><span class="sxs-lookup"><span data-stu-id="f7939-1517">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for room in the queue.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1518">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1518">Return Values</span></span>

- <span data-ttu-id="f7939-1519">**TX_SUCCESS**: (0x00) l'invio del messaggio è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-1519">**TX_SUCCESS**: (0x00) Successful sending of message.</span></span>
- <span data-ttu-id="f7939-1520">**TX_DELETED**: (0x01) la coda di messaggi è stata eliminata durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1520">**TX_DELETED**: (0x01) Message queue was deleted while thread was suspended.</span></span>
- <span data-ttu-id="f7939-1521">**TX_QUEUE_FULL**: il servizio (0x0B) non è stato in grado di inviare il messaggio perché la coda era piena per la durata del tempo di attesa specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1521">**TX_QUEUE_FULL**: (0x0B) Service was unable to send message because the queue was full for the duration of the specified time to wait.</span></span>
- <span data-ttu-id="f7939-1522">**TX_WAIT_ABORTED**: la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-1522">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="f7939-1523">TX_QUEUE_ERROR: (0x09) puntatore della coda di messaggi non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1523">TX_QUEUE_ERROR: (0x09) Invalid message queue pointer.</span></span>
- <span data-ttu-id="f7939-1524">TX_PTR_ERROR: (0x03) puntatore di origine non valido per il messaggio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1524">TX_PTR_ERROR: (0x03) Invalid source pointer for message.</span></span>
- <span data-ttu-id="f7939-1525">TX_WAIT_ERROR: (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1525">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a nonthread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1526">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1526">Allowed From</span></span>

<span data-ttu-id="f7939-1527">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1527">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1528">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1528">Preemption Possible</span></span>

<span data-ttu-id="f7939-1529">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1529">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1530">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1530">Example</span></span>

```C
TX_QUEUE my_queue;
UINT status;
ULONG my_message[4];

/* Send a message to "my_queue." Return immediately,
   regardless of success. This wait option is used for
   calls from initialization, timers, and ISRs. */
status =  tx_queue_send(&my_queue, my_message, TX_NO_WAIT);

/* If status equals TX_SUCCESS, the message is in the
   queue. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1531">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1531">See Also</span></span>

- <span data-ttu-id="f7939-1532">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1532">tx_queue_create</span></span>
- <span data-ttu-id="f7939-1533">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1533">tx_queue_delete</span></span>
- <span data-ttu-id="f7939-1534">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f7939-1534">tx_queue_flush</span></span>
- <span data-ttu-id="f7939-1535">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1535">tx_queue_front_send</span></span>
- <span data-ttu-id="f7939-1536">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1536">tx_queue_info_get</span></span>
- <span data-ttu-id="f7939-1537">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1537">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="f7939-1538">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1538">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1539">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1539">tx_queue_prioritize</span></span>
- <span data-ttu-id="f7939-1540">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f7939-1540">tx_queue_receive</span></span>
- <span data-ttu-id="f7939-1541">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1541">tx_queue_send_notify</span></span>

## <a name="tx_queue_send_notify"></a><span data-ttu-id="f7939-1542">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1542">tx_queue_send_notify</span></span> 

<span data-ttu-id="f7939-1543">Invia notifica all'applicazione quando il messaggio viene inviato alla coda</span><span class="sxs-lookup"><span data-stu-id="f7939-1543">Notify application when message is sent to queue</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1544">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1544">Prototype</span></span>

```C
UINT  tx_queue_send_notify(TX_QUEUE *queue_ptr,
        VOID (*queue_send_notify)(TX_QUEUE *));
```
### <a name="description"></a><span data-ttu-id="f7939-1545">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1545">Description</span></span>

<span data-ttu-id="f7939-1546">Questo servizio registra una funzione di callback delle notifiche chiamata ogni volta che un messaggio viene inviato alla coda specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1546">This service registers a notification callback function that is called whenever a message is sent to the specified queue.</span></span> <span data-ttu-id="f7939-1547">L'elaborazione del callback di notifica viene definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1547">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="f7939-1548">Il callback di notifica di invio della coda dell'applicazione non è autorizzato a chiamare alcuna API SMP di ThreadX con un'opzione di sospensione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1548">The application’s queue send notification callback is not allowed to call any ThreadX SMP API with a suspension option.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1549">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1549">Parameters</span></span> 

- <span data-ttu-id="f7939-1550">**queue_ptr**: puntatore alla coda creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1550">**queue_ptr**: Pointer to previously created queue.</span></span>
- <span data-ttu-id="f7939-1551">**queue_send_notify**: puntatore alla funzione di notifica di invio della coda dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1551">**queue_send_notify**: Pointer to application’s queue send notification function.</span></span> <span data-ttu-id="f7939-1552">Se questo valore è TX_NULL, la notifica è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1552">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1553">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1553">Return Values</span></span>

- <span data-ttu-id="f7939-1554">**TX_SUCCESS**: (0x00) registrazione della notifica di invio della coda riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1554">**TX_SUCCESS**: (0x00) Successful registration of queue send notification.</span></span>
- <span data-ttu-id="f7939-1555">TX_QUEUE_ERROR: (0x09) puntatore della coda non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1555">TX_QUEUE_ERROR: (0x09) Invalid queue pointer.</span></span>
- <span data-ttu-id="f7939-1556">TX_FEATURE_NOT_ENABLED: (0xFF) il sistema è stato compilato con le funzionalità di notifica disabilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-1556">TX_FEATURE_NOT_ENABLED: (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1557">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1557">Allowed From</span></span>

<span data-ttu-id="f7939-1558">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1558">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1559">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1559">Example</span></span>

```C
TX_QUEUE         my_queue;

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
### <a name="see-also"></a><span data-ttu-id="f7939-1560">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1560">See Also</span></span>

- <span data-ttu-id="f7939-1561">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1561">tx_queue_create</span></span>
- <span data-ttu-id="f7939-1562">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1562">tx_queue_delete</span></span>
- <span data-ttu-id="f7939-1563">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="f7939-1563">tx_queue_flush</span></span>
- <span data-ttu-id="f7939-1564">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1564">tx_queue_front_send</span></span>
- <span data-ttu-id="f7939-1565">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1565">tx_queue_info_get</span></span>
- <span data-ttu-id="f7939-1566">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1566">tx_queue_performance_info_get</span></span>
- <span data-ttu-id="f7939-1567">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1567">tx_queue_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1568">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1568">tx_queue_prioritize</span></span>
- <span data-ttu-id="f7939-1569">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="f7939-1569">tx_queue_receive</span></span>
- <span data-ttu-id="f7939-1570">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="f7939-1570">tx_queue_send</span></span>

## <a name="tx_semaphore_ceiling_put"></a><span data-ttu-id="f7939-1571">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1571">tx_semaphore_ceiling_put</span></span> 

<span data-ttu-id="f7939-1572">Inserire un'istanza in conteggio semaforo con limite massimo</span><span class="sxs-lookup"><span data-stu-id="f7939-1572">Place an instance in counting semaphore with ceiling</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1573">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1573">Prototype</span></span>

```C
UINT  tx_semaphore_ceiling_put(TX_SEMAPHORE *semaphore_ptr,
        ULONG ceiling);
```
### <a name="description"></a><span data-ttu-id="f7939-1574">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1574">Description</span></span>

<span data-ttu-id="f7939-1575">Questo servizio inserisce un'istanza nel semaforo di conteggio specificato, che in realtà incrementa il semaforo di conteggio di uno.</span><span class="sxs-lookup"><span data-stu-id="f7939-1575">This service puts an instance into the specified counting semaphore, which in reality increments the counting semaphore by one.</span></span> <span data-ttu-id="f7939-1576">Se il valore corrente del semaforo di conteggio è maggiore o uguale al limite specificato, l'istanza non verrà inserita e verrà restituito un errore TX_CEILING_EXCEEDED.</span><span class="sxs-lookup"><span data-stu-id="f7939-1576">If the counting semaphore’s current value is greater than or equal to the specified ceiling, the instance will not be put and a TX_CEILING_EXCEEDED error will be returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1577">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1577">Parameters</span></span> 

- <span data-ttu-id="f7939-1578">**semaphore_ptr**: puntatore al semaforo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1578">**semaphore_ptr**: Pointer to previously created semaphore.</span></span>
- <span data-ttu-id="f7939-1579">**Ceiling**: limite massimo consentito per il semaforo. i valori validi sono compresi tra 1 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="f7939-1579">**ceiling**: Maximum limit allowed for the semaphore (valid values range from 1 through 0xFFFFFFFF).</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1580">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1580">Return Values</span></span>

- <span data-ttu-id="f7939-1581">**TX_SUCCESS**: (0x00) la soglia del semaforo è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1581">**TX_SUCCESS**: (0x00) Successful semaphore ceiling put.</span></span>
- <span data-ttu-id="f7939-1582">**TX_CEILING_EXCEEDED**: (0x21) la richiesta PUT supera il limite massimo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1582">**TX_CEILING_EXCEEDED**: (0x21) Put request exceeds ceiling.</span></span>
- <span data-ttu-id="f7939-1583">TX_INVALID_CEILING: (0x22) è stato specificato un valore non valido pari a zero per il limite massimo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1583">TX_INVALID_CEILING: (0x22) An invalid value of zero was supplied for ceiling.</span></span>
- <span data-ttu-id="f7939-1584">TX_SEMAPHORE_ERROR: (0x0C) puntatore a semaforo non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1584">TX_SEMAPHORE_ERROR: (0x0C) Invalid semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1585">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1585">Allowed From</span></span>

<span data-ttu-id="f7939-1586">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1586">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1587">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1587">Example</span></span>

```c
TX_SEMAPHORE     my_semaphore;

/* Increment the counting semaphore "my_semaphore" but make sure
   that it never exceeds 7 as specified in the call. */
status = tx_semaphore_ceiling_put(&my_semaphore, 7);

/* If status is TX_SUCCESS the semaphore count has been
```
### <a name="see-also"></a><span data-ttu-id="f7939-1588">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1588">See Also</span></span>

- <span data-ttu-id="f7939-1589">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1589">tx_semaphore_create</span></span>
- <span data-ttu-id="f7939-1590">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1590">tx_semaphore_delete</span></span>
- <span data-ttu-id="f7939-1591">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1591">tx_semaphore_get</span></span>
- <span data-ttu-id="f7939-1592">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1592">tx_semaphore_info_get</span></span>
- <span data-ttu-id="f7939-1593">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1593">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="f7939-1594">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1594">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1595">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1595">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="f7939-1596">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1596">tx_semaphore_put</span></span>
- <span data-ttu-id="f7939-1597">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1597">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_create"></a><span data-ttu-id="f7939-1598">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1598">tx_semaphore_create</span></span>

<span data-ttu-id="f7939-1599">Crea semaforo di conteggio</span><span class="sxs-lookup"><span data-stu-id="f7939-1599">Create counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1600">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1600">Prototype</span></span>

```C
UINT tx_semaphore_create(TX_SEMAPHORE *semaphore_ptr,
                           CHAR *name_ptr, ULONG initial_count);
```
### <a name="description"></a><span data-ttu-id="f7939-1601">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1601">Description</span></span>

<span data-ttu-id="f7939-1602">Questo servizio crea un semaforo di conteggio per la sincronizzazione tra thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1602">This service creates a counting semaphore for inter-thread synchronization.</span></span> <span data-ttu-id="f7939-1603">Il numero di semafori iniziale viene specificato come parametro di input.</span><span class="sxs-lookup"><span data-stu-id="f7939-1603">The initial semaphore count is specified as an input parameter.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1604">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1604">Parameters</span></span> 

- <span data-ttu-id="f7939-1605">**semaphore_ptr**: puntatore a un blocco di controllo Semaphore.</span><span class="sxs-lookup"><span data-stu-id="f7939-1605">**semaphore_ptr**: Pointer to a semaphore control block.</span></span> 
- <span data-ttu-id="f7939-1606">**name_ptr**: puntatore al nome del semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1606">**name_ptr**: Pointer to the name of the semaphore.</span></span>
- <span data-ttu-id="f7939-1607">**initial_count**: specifica il numero iniziale per questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1607">**initial_count**: Specifies the initial count for this semaphore.</span></span> <span data-ttu-id="f7939-1608">I valori validi sono compresi tra 0x00000000 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="f7939-1608">Legal values range from 0x00000000 through 0xFFFFFFFF.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1609">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1609">Return Values</span></span>

- <span data-ttu-id="f7939-1610">**TX_SUCCESS**: (0x00) la creazione del semaforo è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1610">**TX_SUCCESS**: (0x00) Successful semaphore creation.</span></span>
- <span data-ttu-id="f7939-1611">TX_SEMAPHORE_ERROR: (0x0C) puntatore a semaforo non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1611">TX_SEMAPHORE_ERROR: (0x0C) Invalid semaphore pointer.</span></span> <span data-ttu-id="f7939-1612">Il puntatore è NULL o il semaforo è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1612">Either the pointer is NULL or the semaphore is already created.</span></span>
- <span data-ttu-id="f7939-1613">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1613">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1614">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1614">Allowed From</span></span>

<span data-ttu-id="f7939-1615">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="f7939-1615">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1616">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1616">Preemption Possible</span></span>

<span data-ttu-id="f7939-1617">No</span><span class="sxs-lookup"><span data-stu-id="f7939-1617">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1618">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1618">Example</span></span>

```C
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Create a counting semaphore whose initial value is 1.
   This is typically the technique used to make a binary
   semaphore. Binary semaphores are used to provide
   protection over a common resource. */
status = tx_semaphore_create(&my_semaphore,
            "my_semaphore_name", 1);

/* If status equals TX_SUCCESS, my_semaphore is ready for
   use. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1619">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1619">See Also</span></span>

- <span data-ttu-id="f7939-1620">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1620">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="f7939-1621">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1621">tx_semaphore_delete</span></span>
- <span data-ttu-id="f7939-1622">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1622">tx_semaphore_get</span></span>
- <span data-ttu-id="f7939-1623">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1623">tx_semaphore_info_get</span></span>
- <span data-ttu-id="f7939-1624">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1624">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="f7939-1625">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1625">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1626">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1626">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="f7939-1627">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1627">tx_semaphore_put</span></span>
- <span data-ttu-id="f7939-1628">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1628">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_delete"></a><span data-ttu-id="f7939-1629">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1629">tx_semaphore_delete</span></span>

<span data-ttu-id="f7939-1630">Elimina semaforo di conteggio</span><span class="sxs-lookup"><span data-stu-id="f7939-1630">Delete counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1631">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1631">Prototype</span></span>

```C
UINT tx_semaphore_delete(TX_SEMAPHORE *semaphore_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-1632">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1632">Description</span></span>

<span data-ttu-id="f7939-1633">Questo servizio Elimina il semaforo di conteggio specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1633">This service deletes the specified counting semaphore.</span></span> <span data-ttu-id="f7939-1634">Tutti i thread sospesi in attesa di un'istanza del semaforo vengono ripresi e viene dato un TX_DELETED stato restituito.</span><span class="sxs-lookup"><span data-stu-id="f7939-1634">All threads suspended waiting for a semaphore instance are resumed and given a TX_DELETED return status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1635">Prima di eliminare il semaforo, l'applicazione deve garantire che un callback di notifica put per questo semaforo venga completato (o disabilitato).</span><span class="sxs-lookup"><span data-stu-id="f7939-1635">The application must ensure that a put notify callback for this semaphore is completed (or disabled) before deleting the semaphore.</span></span> <span data-ttu-id="f7939-1636">Inoltre, l'applicazione deve impedire l'uso futuro di un semaforo eliminato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1636">In addition, the application must prevent all future use of a deleted semaphore.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1637">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1637">Parameters</span></span> 

- <span data-ttu-id="f7939-1638">**semaphore_ptr**: puntatore a un semaforo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1638">**semaphore_ptr**: Pointer to a previously created semaphore.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1639">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1639">Return Values</span></span>

- <span data-ttu-id="f7939-1640">**TX_SUCCESS**: (0x00) il conteggio dell'eliminazione del semaforo è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-1640">**TX_SUCCESS**: (0x00) Successful counting semaphore deletion.</span></span>
- <span data-ttu-id="f7939-1641">TX_SEMAPHORE_ERROR: (0x0C) puntatore del semaforo di conteggio non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1641">TX_SEMAPHORE_ERROR: (0x0C) Invalid counting semaphore pointer.</span></span>
- <span data-ttu-id="f7939-1642">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1642">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1643">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1643">Allowed From</span></span>

<span data-ttu-id="f7939-1644">Thread</span><span class="sxs-lookup"><span data-stu-id="f7939-1644">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1645">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1645">Preemption Possible</span></span>

<span data-ttu-id="f7939-1646">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1646">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1647">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1647">Example</span></span>

```C
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Delete counting semaphore. Assume that the counting
   semaphore has already been created. */
status = tx_semaphore_delete(&my_semaphore);

/* If status equals TX_SUCCESS, the counting semaphore is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1648">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1648">See Also</span></span>

- <span data-ttu-id="f7939-1649">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1649">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="f7939-1650">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1650">tx_semaphore_create</span></span>
- <span data-ttu-id="f7939-1651">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1651">tx_semaphore_get</span></span>
- <span data-ttu-id="f7939-1652">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1652">tx_semaphore_info_get</span></span>
- <span data-ttu-id="f7939-1653">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1653">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="f7939-1654">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1654">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1655">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1655">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="f7939-1656">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1656">tx_semaphore_put</span></span>
- <span data-ttu-id="f7939-1657">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1657">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_get"></a><span data-ttu-id="f7939-1658">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1658">tx_semaphore_get</span></span>

<span data-ttu-id="f7939-1659">Ottenere un'istanza dal semaforo di conteggio</span><span class="sxs-lookup"><span data-stu-id="f7939-1659">Get instance from counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1660">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1660">Prototype</span></span>

```C
UINT tx_semaphore_get(TX_SEMAPHORE *semaphore_ptr,
                          ULONG wait_option)
```
### <a name="description"></a><span data-ttu-id="f7939-1661">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1661">Description</span></span>

<span data-ttu-id="f7939-1662">Questo servizio recupera un'istanza (un numero singolo) dal semaforo di conteggio specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1662">This service retrieves an instance (a single count) from the specified counting semaphore.</span></span> <span data-ttu-id="f7939-1663">Di conseguenza, il conteggio del semaforo specificato viene diminuito di uno.</span><span class="sxs-lookup"><span data-stu-id="f7939-1663">As a result, the specified semaphore’s count is decreased by one.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1664">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1664">Parameters</span></span>

- <span data-ttu-id="f7939-1665">**semaphore_ptr**: puntatore a un semaforo di conteggio creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1665">**semaphore_ptr**: Pointer to a previously created counting semaphore.</span></span>
- <span data-ttu-id="f7939-1666">**WAIT_OPTION**: definisce il comportamento del servizio se non sono disponibili istanze del semaforo. ovvero, il numero di semafori è pari a zero.</span><span class="sxs-lookup"><span data-stu-id="f7939-1666">**wait_option**: Defines how the service behaves if there are no instances of the semaphore available; i.e., the semaphore count is zero.</span></span> <span data-ttu-id="f7939-1667">Le opzioni di attesa sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="f7939-1667">The wait options are defined as follows:</span></span>
    - <span data-ttu-id="f7939-1668">**TX_NO_WAIT**: (0x00000000)</span><span class="sxs-lookup"><span data-stu-id="f7939-1668">**TX_NO_WAIT**: (0x00000000)</span></span>
    - <span data-ttu-id="f7939-1669">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span><span class="sxs-lookup"><span data-stu-id="f7939-1669">**TX_WAIT_FOREVER**: (0xFFFFFFFF)</span></span>
    - <span data-ttu-id="f7939-1670">valore di timeout: (0x00000001 tramite 0xFFFFFFFE)</span><span class="sxs-lookup"><span data-stu-id="f7939-1670">timeout value: (0x00000001 through 0xFFFFFFFE)</span></span>

    <span data-ttu-id="f7939-1671">La selezione di TX_NO_WAIT comporta un ritorno immediato da questo servizio, indipendentemente dal fatto che abbia avuto esito positivo o negativo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1671">Selecting TX_NO_WAIT results in an immediate return from this service regardless of whether or not it was successful.</span></span> <span data-ttu-id="f7939-1672">*Questa è l'unica opzione valida se il servizio viene chiamato da un non thread. ad esempio, inizializzazione, timer o ISR.*</span><span class="sxs-lookup"><span data-stu-id="f7939-1672">*This is the only valid option if the service is called from a non-thread; e.g., initialization, timer, or ISR.*</span></span>

    <span data-ttu-id="f7939-1673">Se si seleziona TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando non sarà disponibile un'istanza del semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1673">Selecting TX_WAIT_FOREVER causes the calling thread to suspend indefinitely until a semaphore instance is available.</span></span> 

    <span data-ttu-id="f7939-1674">La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa di un'istanza del semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1674">Selecting a numeric value (1-0xFFFFFFFE) specifies the maximum number of timer-ticks to stay suspended while waiting for a semaphore instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1675">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1675">Return Values</span></span>

- <span data-ttu-id="f7939-1676">**TX_SUCCESS**: (0x00) il recupero di un'istanza del semaforo è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-1676">**TX_SUCCESS**: (0x00) Successful retrieval of a semaphore instance.</span></span>
- <span data-ttu-id="f7939-1677">**TX_DELETED**: (0x01) il conteggio del semaforo è stato eliminato durante la sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1677">**TX_DELETED**: (0x01) Counting semaphore was deleted while thread was suspended.</span></span>
- <span data-ttu-id="f7939-1678">**TX_NO_INSTANCE**: il servizio (0x0D) non è stato in grado di recuperare un'istanza del semaforo di conteggio (il numero di semafori è pari a zero entro il tempo di attesa specificato).</span><span class="sxs-lookup"><span data-stu-id="f7939-1678">**TX_NO_INSTANCE**: (0x0D) Service was unable to retrieve an instance of the counting semaphore (semaphore count is zero within the specified time to wait).</span></span>
- <span data-ttu-id="f7939-1679">**TX_WAIT_ABORTED**: la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-1679">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="f7939-1680">TX_SEMAPHORE_ERROR: (0x0C) puntatore del semaforo di conteggio non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1680">TX_SEMAPHORE_ERROR: (0x0C) Invalid counting semaphore pointer.</span></span>
- <span data-ttu-id="f7939-1681">TX_WAIT_ERROR: (0x04) è stata specificata un'opzione di attesa diversa da TX_NO_WAIT in una chiamata da un non thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1681">TX_WAIT_ERROR: (0x04) A wait option other than TX_NO_WAIT was specified on a call from a non-thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1682">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1682">Allowed From</span></span>

<span data-ttu-id="f7939-1683">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1683">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1684">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1684">Preemption Possible</span></span>

<span data-ttu-id="f7939-1685">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1685">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1686">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1686">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Get a semaphore instance from the semaphore
   "my_semaphore." If the semaphore count is zero,
   suspend until an instance becomes available.
   Note that this suspension is only possible from
   application threads. */
status =  tx_semaphore_get(&my_semaphore, TX_WAIT_FOREVER);

/* If status equals TX_SUCCESS, the thread has obtained
   an instance of the semaphore. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1687">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1687">See Also</span></span>

- <span data-ttu-id="f7939-1688">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1688">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="f7939-1689">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1689">tx_semaphore_create</span></span>
- <span data-ttu-id="f7939-1690">tx_semahore_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1690">tx_semahore_delete</span></span>
- <span data-ttu-id="f7939-1691">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1691">tx_semaphore_info_get</span></span>
- <span data-ttu-id="f7939-1692">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1692">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="f7939-1693">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1693">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="f7939-1694">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1694">tx_semaphore_put</span></span>
- <span data-ttu-id="f7939-1695">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1695">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_info_get"></a><span data-ttu-id="f7939-1696">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1696">tx_semaphore_info_get</span></span>

<span data-ttu-id="f7939-1697">Recuperare informazioni sul semaforo</span><span class="sxs-lookup"><span data-stu-id="f7939-1697">Retrieve information about semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1698">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1698">Prototype</span></span>

```C
UINT tx_semaphore_info_get(TX_SEMAPHORE *semaphore_ptr,
                          CHAR **name, ULONG *current_value,
                          TX_THREAD **first_suspended,
                          ULONG *suspended_count,
                          TX_SEMAPHORE **next_semaphore)
```
### <a name="description"></a><span data-ttu-id="f7939-1699">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1699">Description</span></span>

<span data-ttu-id="f7939-1700">Questo servizio recupera le informazioni sul semaforo specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1700">This service retrieves information about the specified semaphore.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1701">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1701">Parameters</span></span>

- <span data-ttu-id="f7939-1702">**semaphore_ptr**: puntatore al blocco di controllo del semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1702">**semaphore_ptr**: Pointer to semaphore control block.</span></span>
- <span data-ttu-id="f7939-1703">**Name**: puntatore alla destinazione per il puntatore al nome del semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1703">**name**: Pointer to destination for the pointer to the semaphore’s name.</span></span>
- <span data-ttu-id="f7939-1704">**Current_value**: puntatore alla destinazione per il conteggio del semaforo corrente.</span><span class="sxs-lookup"><span data-stu-id="f7939-1704">**current_value**: Pointer to destination for the current semaphore’s count.</span></span>
- <span data-ttu-id="f7939-1705">**first_suspended**: puntatore alla destinazione per il puntatore al thread che è il primo nell'elenco di sospensione di questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1705">**first_suspended**: Pointer to destination for the pointer to the thread that is first on the suspension list of this semaphore.</span></span>
- <span data-ttu-id="f7939-1706">**suspended_count**: puntatore alla destinazione per il numero di thread attualmente sospesi in questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1706">**suspended_count**: Pointer to destination for the number of threads currently suspended on this semaphore.</span></span>
- <span data-ttu-id="f7939-1707">**next_semaphore**: puntatore alla destinazione per il puntatore del semaforo creato successivo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1707">**next_semaphore**: Pointer to destination for the pointer of the next created semaphore.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1708">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1708">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1709">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1709">Return Values</span></span>

- <span data-ttu-id="f7939-1710">**TX_SUCCESS**: (0x00) il recupero delle informazioni sul semaforo è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-1710">**TX_SUCCESS**: (0x00) Successful semaphore information retrieval.</span></span>
- <span data-ttu-id="f7939-1711">TX_SEMAPHORE_ERROR: (0x0C) puntatore a semaforo non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1711">TX_SEMAPHORE_ERROR: (0x0C) Invalid semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1712">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1712">Allowed From</span></span>

<span data-ttu-id="f7939-1713">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1713">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1714">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1714">Preemption Possible</span></span>

<span data-ttu-id="f7939-1715">No</span><span class="sxs-lookup"><span data-stu-id="f7939-1715">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1716">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1716">Example</span></span>

```c
TX_SEMAPHORE my_semaphore;
CHAR         *name;
ULONG        current_value;
TX_THREAD    *first_suspended;
ULONG        suspended_count;
TX_SEMAPHORE *next_semaphore;
UINT         status;

/* Retrieve information about the previously created
   semaphore "my_semaphore." */
status =  tx_semaphore_info_get(&my_semaphore, &name,
                      &current_value,
                      &first_suspended, &suspended_count,
                      &next_semaphore);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1717">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1717">See Also</span></span>

- <span data-ttu-id="f7939-1718">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1718">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="f7939-1719">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1719">tx_semaphore_create</span></span>
- <span data-ttu-id="f7939-1720">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1720">tx_semaphore_delete</span></span>
- <span data-ttu-id="f7939-1721">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1721">tx_semaphore_get</span></span>
- <span data-ttu-id="f7939-1722">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1722">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="f7939-1723">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1723">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1724">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1724">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="f7939-1725">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1725">tx_semaphore_put</span></span>
- <span data-ttu-id="f7939-1726">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1726">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_performance_info_get"></a><span data-ttu-id="f7939-1727">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1727">tx_semaphore_performance_info_get</span></span> 

<span data-ttu-id="f7939-1728">Ottenere informazioni sulle prestazioni del semaforo</span><span class="sxs-lookup"><span data-stu-id="f7939-1728">Get semaphore performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1729">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1729">Prototype</span></span>

```C
UINT  tx_semaphore_performance_info_get(TX_SEMAPHORE *semaphore_ptr,
        ULONG *puts, ULONG *gets,
        ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="f7939-1730">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1730">Description</span></span>

<span data-ttu-id="f7939-1731">Questo servizio recupera le informazioni sulle prestazioni relative al semaforo specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1731">This service retrieves performance information about the specified semaphore.</span></span>

> [!NOTE]
> <span data-ttu-id="f7939-1732">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1732">The ThreadX SMP library and application must be built with **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1733">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1733">Parameters</span></span>

- <span data-ttu-id="f7939-1734">**semaphore_ptr**: puntatore al semaforo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1734">**semaphore_ptr**: Pointer to previously created semaphore.</span></span>
- <span data-ttu-id="f7939-1735">**inserisce**: puntatore alla destinazione per il numero di richieste PUT eseguite sul semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1735">**puts**: Pointer to destination for the number of put requests performed on this semaphore.</span></span>
- <span data-ttu-id="f7939-1736">**ottiene**: puntatore alla destinazione per il numero di richieste Get eseguite su questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1736">**gets**: Pointer to destination for the number of get requests performed on this semaphore.</span></span>
- <span data-ttu-id="f7939-1737">**sospensioni**: puntatore alla destinazione per il numero di sospensioni dei thread in questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1737">**suspensions**: Pointer to destination for the number of thread suspensions on this semaphore.</span></span>
- <span data-ttu-id="f7939-1738">**timeout**: puntatore alla destinazione per il numero di timeout di sospensione del thread in questo semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1738">**timeouts**: Pointer to destination for the number of thread suspension timeouts on this semaphore.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1739">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1739">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1740">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1740">Return Values</span></span>

- <span data-ttu-id="f7939-1741">**TX_SUCCESS**: (0x00) ottenere prestazioni del semaforo riuscite.</span><span class="sxs-lookup"><span data-stu-id="f7939-1741">**TX_SUCCESS**: (0x00) Successful semaphore performance get.</span></span>
- <span data-ttu-id="f7939-1742">**TX_PTR_ERROR**: (0x03) puntatore a semaforo non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1742">**TX_PTR_ERROR**: (0x03) Invalid semaphore pointer.</span></span>
- <span data-ttu-id="f7939-1743">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-1743">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1744">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1744">Allowed From</span></span>

<span data-ttu-id="f7939-1745">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1745">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1746">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1746">Example</span></span>

```C
TX_SEMAPHORE     my_semaphore;
ULONG            puts;
ULONG            gets;
ULONG            suspensions;
ULONG            timeouts;

/* Retrieve performance information on the previously created
   semaphore. */
status =  tx_semaphore_performance_info_get(&my_semaphore, &puts,
               &gets, &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1747">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1747">See Also</span></span>

- <span data-ttu-id="f7939-1748">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1748">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="f7939-1749">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1749">tx_semaphore_create</span></span>
- <span data-ttu-id="f7939-1750">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1750">tx_semaphore_delete</span></span>
- <span data-ttu-id="f7939-1751">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1751">tx_semaphore_get</span></span>
- <span data-ttu-id="f7939-1752">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1752">tx_semaphore_info_get</span></span>
- <span data-ttu-id="f7939-1753">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1753">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1754">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1754">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="f7939-1755">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1755">tx_semaphore_put</span></span>
- <span data-ttu-id="f7939-1756">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1756">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_performance_system_info_get"></a><span data-ttu-id="f7939-1757">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1757">tx_semaphore_performance_system_info_get</span></span> 

<span data-ttu-id="f7939-1758">Ottenere informazioni sulle prestazioni del sistema Semaphore</span><span class="sxs-lookup"><span data-stu-id="f7939-1758">Get semaphore system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1759">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1759">Prototype</span></span>

```C
UINT tx_semaphore_performance_system_info_get(ULONG *puts,
       ULONG *gets, ULONG *suspensions, ULONG *timeouts);
```
### <a name="description"></a><span data-ttu-id="f7939-1760">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1760">Description</span></span>

<span data-ttu-id="f7939-1761">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i semafori nel sistema.</span><span class="sxs-lookup"><span data-stu-id="f7939-1761">This service retrieves performance information about all the semaphores in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1762">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1762">The ThreadX SMP library and application must be built with **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1763">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1763">Parameters</span></span>

- <span data-ttu-id="f7939-1764">**inserisce**: puntatore alla destinazione per il numero totale di richieste PUT eseguite su tutti i semafori.</span><span class="sxs-lookup"><span data-stu-id="f7939-1764">**puts**: Pointer to destination for the total number of put requests performed on all semaphores.</span></span>
- <span data-ttu-id="f7939-1765">**ottiene**: puntatore alla destinazione per il numero totale di richieste Get eseguite su tutti i semafori.</span><span class="sxs-lookup"><span data-stu-id="f7939-1765">**gets**: Pointer to destination for the total number of get requests performed on all semaphores.</span></span>
- <span data-ttu-id="f7939-1766">**sospensioni**: puntatore alla destinazione per il numero totale di sospensioni di thread in tutti i semafori.</span><span class="sxs-lookup"><span data-stu-id="f7939-1766">**suspensions**: Pointer to destination for the total number of thread suspensions on all semaphores.</span></span>
- <span data-ttu-id="f7939-1767">**timeout**: puntatore alla destinazione per il numero totale di timeout di sospensione del thread in tutti i semafori.</span><span class="sxs-lookup"><span data-stu-id="f7939-1767">**timeouts**: Pointer to destination for the total number of thread suspension timeouts on all semaphores.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1768">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1768">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1769">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1769">Return Values</span></span>

- <span data-ttu-id="f7939-1770">TX_SUCCESS: (0x00) prestazioni del sistema Semaphore riuscite.</span><span class="sxs-lookup"><span data-stu-id="f7939-1770">TX_SUCCESS: (0x00) Successful semaphore system performance get.</span></span>
- <span data-ttu-id="f7939-1771">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-1771">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1772">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1772">Allowed From</span></span>

<span data-ttu-id="f7939-1773">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1773">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1774">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1774">Example</span></span>

```C
ULONG         puts;
ULONG         gets;
ULONG         suspensions;
ULONG         timeouts;

/* Retrieve performance information on all previously created
   semaphores. */
status = tx_semaphore_performance_system_info_get(&puts, &gets,
               &suspensions, &timeouts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1775">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1775">See Also</span></span>

- <span data-ttu-id="f7939-1776">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1776">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="f7939-1777">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1777">tx_semaphore_create</span></span>
- <span data-ttu-id="f7939-1778">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1778">tx_semaphore_delete</span></span>
- <span data-ttu-id="f7939-1779">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1779">tx_semaphore_get</span></span>
- <span data-ttu-id="f7939-1780">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1780">tx_semaphore_info_get</span></span>
- <span data-ttu-id="f7939-1781">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1781">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="f7939-1782">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1782">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="f7939-1783">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1783">tx_semaphore_put</span></span>
- <span data-ttu-id="f7939-1784">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1784">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_prioritize"></a><span data-ttu-id="f7939-1785">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1785">tx_semaphore_prioritize</span></span>

<span data-ttu-id="f7939-1786">Priorità dell'elenco di sospensioni del semaforo</span><span class="sxs-lookup"><span data-stu-id="f7939-1786">Prioritize semaphore suspension list</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1787">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1787">Prototype</span></span>

```C
UINT tx_semaphore_prioritize(TX_SEMAPHORE *semaphore_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-1788">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1788">Description</span></span>

<span data-ttu-id="f7939-1789">Questo servizio posiziona il thread con priorità più elevata sospeso per un'istanza del semaforo all'inizio dell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="f7939-1789">This service places the highest priority thread suspended for an instance of the semaphore at the front of the suspension list.</span></span> <span data-ttu-id="f7939-1790">Tutti gli altri thread rimangono nello stesso ordine FIFO in cui sono stati sospesi.</span><span class="sxs-lookup"><span data-stu-id="f7939-1790">All other threads remain in the same FIFO order they were suspended in.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1791">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1791">Parameters</span></span> 

- <span data-ttu-id="f7939-1792">**semaphore_ptr**: puntatore a un semaforo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1792">**semaphore_ptr**: Pointer to a previously created semaphore.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1793">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1793">Return Values</span></span>

- <span data-ttu-id="f7939-1794">**TX_SUCCESS**: (0x00) priorità semaforo riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1794">**TX_SUCCESS**: (0x00) Successful semaphore prioritize.</span></span>
- <span data-ttu-id="f7939-1795">TX_SEMAPHORE_ERROR: (0x0C) puntatore del semaforo di conteggio non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1795">TX_SEMAPHORE_ERROR: (0x0C) Invalid counting semaphore pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1796">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1796">Allowed From</span></span>

<span data-ttu-id="f7939-1797">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1797">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1798">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1798">Preemption Possible</span></span>

<span data-ttu-id="f7939-1799">No</span><span class="sxs-lookup"><span data-stu-id="f7939-1799">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1800">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1800">Example</span></span>

```C
TX_SEMAPHORE my_semaphore;
UINT         status;

/* Ensure that the highest priority thread will receive
   the next instance of this semaphore. */
status =  tx_semaphore_prioritize(&my_semaphore);

/* If status equals TX_SUCCESS, the highest priority
   suspended thread is at the front of the list. The
   next tx_semaphore_put call made to this semaphore will
   wake up this thread. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1801">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1801">See Also</span></span>

- <span data-ttu-id="f7939-1802">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1802">tx_semaphore_create</span></span>
- <span data-ttu-id="f7939-1803">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1803">tx_semaphore_delete</span></span>
- <span data-ttu-id="f7939-1804">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1804">tx_semaphore_get</span></span>
- <span data-ttu-id="f7939-1805">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1805">tx_semaphore_info_get</span></span>
- <span data-ttu-id="f7939-1806">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1806">tx_semaphore_put</span></span>

## <a name="tx_semaphore_put"></a><span data-ttu-id="f7939-1807">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1807">tx_semaphore_put</span></span>

<span data-ttu-id="f7939-1808">Inserire un'istanza in conteggio semaforo</span><span class="sxs-lookup"><span data-stu-id="f7939-1808">Place an instance in counting semaphore</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1809">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1809">Prototype</span></span>

```C
UINT tx_semaphore_put(TX_SEMAPHORE *semaphore_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-1810">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1810">Description</span></span>

<span data-ttu-id="f7939-1811">Questo servizio inserisce un'istanza nel semaforo di conteggio specificato, che in realtà incrementa il semaforo di conteggio di uno.</span><span class="sxs-lookup"><span data-stu-id="f7939-1811">This service puts an instance into the specified counting semaphore, which in reality increments the counting semaphore by one.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1812">Se questo servizio viene chiamato quando il semaforo è costituito da tutti (OxFFFFFFFF), la nuova operazione Put provocherà la reimpostazione del semaforo su zero.</span><span class="sxs-lookup"><span data-stu-id="f7939-1812">If this service is called when the semaphore is all ones (OxFFFFFFFF), the new put operation will cause the semaphore to be reset to zero.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1813">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1813">Parameters</span></span>

- <span data-ttu-id="f7939-1814">**semaphore_ptr**: puntatore al blocco di controllo semaforo di conteggio creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1814">**semaphore_ptr**: Pointer to the previously created counting semaphore control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1815">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1815">Return Values</span></span>

- <span data-ttu-id="f7939-1816">**TX_SUCCESS**: (0x00) semaforo put riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-1816">**TX_SUCCESS**: (0x00) Successful semaphore put.</span></span>
- <span data-ttu-id="f7939-1817">TX_SEMAPHORE_ERROR: (0x0C) puntatore non valido per il conteggio del semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1817">TX_SEMAPHORE_ERROR: (0x0C) Invalid pointer to counting semaphore.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1818">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1818">Allowed From</span></span>

<span data-ttu-id="f7939-1819">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1819">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1820">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1820">Preemption Possible</span></span>

<span data-ttu-id="f7939-1821">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1821">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1822">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1822">Example</span></span>

```C
TX_SEMAPHORE     my_semaphore;
UINT             status;

/* Increment the counting semaphore "my_semaphore." */
status =  tx_semaphore_put(&my_semaphore);

/* If status equals TX_SUCCESS, the semaphore count has
   been incremented. Of course, if a thread was waiting,
   it was given the semaphore instance and resumed. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1823">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1823">See Also</span></span>

- <span data-ttu-id="f7939-1824">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1824">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="f7939-1825">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1825">tx_semaphore_create</span></span>
- <span data-ttu-id="f7939-1826">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1826">tx_semaphore_delete</span></span>
- <span data-ttu-id="f7939-1827">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1827">tx_semaphore_info_get</span></span>
- <span data-ttu-id="f7939-1828">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1828">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="f7939-1829">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1829">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1830">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1830">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="f7939-1831">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1831">tx_semaphore_get</span></span>
- <span data-ttu-id="f7939-1832">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1832">tx_semaphore_put_notify</span></span>

## <a name="tx_semaphore_put_notify"></a><span data-ttu-id="f7939-1833">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1833">tx_semaphore_put_notify</span></span>

<span data-ttu-id="f7939-1834">Invia una notifica all'applicazione quando viene inserito il semaforo</span><span class="sxs-lookup"><span data-stu-id="f7939-1834">Notify application when semaphore is put</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1835">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1835">Prototype</span></span>

```C
UINT  tx_semaphore_put_notify(TX_SEMAPHORE *semaphore_ptr,
        VOID (*semaphore_put_notify)(TX_SEMAPHORE *));
```
### <a name="description"></a><span data-ttu-id="f7939-1836">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1836">Description</span></span>

<span data-ttu-id="f7939-1837">Questo servizio registra una funzione di callback delle notifiche chiamata ogni volta che viene inserito il semaforo specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1837">This service registers a notification callback function that is called whenever the specified semaphore is put.</span></span> <span data-ttu-id="f7939-1838">L'elaborazione del callback di notifica viene definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1838">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="f7939-1839">Il callback di notifica del semaforo dell'applicazione non è autorizzato a chiamare alcuna API SMP di ThreadX con un'opzione di sospensione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1839">The application’s semaphore notification callback is not allowed to call any ThreadX SMP API with a suspension option.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1840">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1840">Parameters</span></span> 

- <span data-ttu-id="f7939-1841">**semaphore_ptr**: puntatore al semaforo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1841">**semaphore_ptr**: Pointer to previously created semaphore.</span></span>
- <span data-ttu-id="f7939-1842">**semaphore_put_notify**: puntatore alla funzione di notifica put del semaforo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1842">**semaphore_put_notify**: Pointer to application’s semaphore put notification function.</span></span> <span data-ttu-id="f7939-1843">Se questo valore è TX_NULL, la notifica è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1843">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1844">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1844">Return Values</span></span>

- <span data-ttu-id="f7939-1845">**TX_SUCCESS**: (0x00) registrazione corretta della notifica put del semaforo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1845">**TX_SUCCESS**: (0x00) Successful registration of semaphore put notification.</span></span>
- <span data-ttu-id="f7939-1846">TX_SEMAPHORE_ERROR: (0x0C) puntatore a semaforo non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1846">TX_SEMAPHORE_ERROR: (0x0C) Invalid semaphore pointer.</span></span>
- <span data-ttu-id="f7939-1847">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema è stato compilato con le funzionalità di notifica disabilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-1847">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1848">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1848">Allowed From</span></span>

<span data-ttu-id="f7939-1849">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1849">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1850">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1850">Example</span></span>

```C
TX_SEMAPHORE     my_semaphore;

/* Register the "my_semaphore_put_notify" function for monitoring
   the put operations on the semaphore "my_semaphore." */
status =  tx_semaphore_put_notify(&my_semaphore,
                my_semaphore_put_notify);

/* If status is TX_SUCCESS the semaphore put notification function
   was successfully registered. */

void my_semaphore_put_notify(TX_SEMAPHORE *semaphore_ptr)
{
   /* The semaphore was just put! */
}
```
### <a name="see-also"></a><span data-ttu-id="f7939-1851">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1851">See Also</span></span>

- <span data-ttu-id="f7939-1852">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1852">tx_semaphore_ceiling_put</span></span>
- <span data-ttu-id="f7939-1853">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1853">tx_semaphore_create</span></span>
- <span data-ttu-id="f7939-1854">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1854">tx_semaphore_delete</span></span>
- <span data-ttu-id="f7939-1855">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1855">tx_semaphore_get</span></span>
- <span data-ttu-id="f7939-1856">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1856">tx_semaphore_info_get</span></span>
- <span data-ttu-id="f7939-1857">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1857">tx_semaphore_performance_info_get</span></span>
- <span data-ttu-id="f7939-1858">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1858">tx_semaphore_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1859">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="f7939-1859">tx_semaphore_prioritize</span></span>
- <span data-ttu-id="f7939-1860">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="f7939-1860">tx_semaphore_put</span></span>

## <a name="tx_thread_create"></a><span data-ttu-id="f7939-1861">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1861">tx_thread_create</span></span>

<span data-ttu-id="f7939-1862">Crea thread applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-1862">Create application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1863">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1863">Prototype</span></span>

```C
UINT tx_thread_create(TX_THREAD *thread_ptr,
                          CHAR *name_ptr, VOID (*entry_function)(ULONG),
                          ULONG entry_input, VOID *stack_start,
                          ULONG stack_size, UINT priority,
                          UINT preempt_threshold, ULONG time_slice,
                          UINT auto_start);
```
### <a name="description"></a><span data-ttu-id="f7939-1864">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1864">Description</span></span>

<span data-ttu-id="f7939-1865">Questo servizio crea un thread dell'applicazione che avvia l'esecuzione in corrispondenza della funzione di immissione attività specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1865">This service creates an application thread that starts execution at the specified task entry function.</span></span> <span data-ttu-id="f7939-1866">Lo stack, la priorità, la soglia di precedenza e l'intervallo di tempo sono tra gli attributi specificati dai parametri di input.</span><span class="sxs-lookup"><span data-stu-id="f7939-1866">The stack, priority, preemption-threshold, and time-slice are among the attributes specified by the input parameters.</span></span> <span data-ttu-id="f7939-1867">Viene inoltre specificato lo stato di esecuzione iniziale del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1867">In addition, the initial execution state of the thread is also specified.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1868">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1868">Parameters</span></span>

- <span data-ttu-id="f7939-1869">**thread_ptr**: puntatore a un blocco di controllo thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1869">**thread_ptr**: Pointer to a thread control block.</span></span>
- <span data-ttu-id="f7939-1870">**name_ptr**: puntatore al nome del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1870">**name_ptr**: Pointer to the name of the thread.</span></span>
- <span data-ttu-id="f7939-1871">**entry_function**: specifica la funzione C iniziale per l'esecuzione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1871">**entry_function**: Specifies the initial C function for thread execution.</span></span> <span data-ttu-id="f7939-1872">Quando un thread restituisce da questa funzione entry, viene inserito in uno stato completato e sospeso per un periodo illimitato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1872">When a thread returns from this entry function, it is placed in a completed state and suspended indefinitely.</span></span>
- <span data-ttu-id="f7939-1873">**entry_input**: valore a 32 bit che viene passato alla funzione entry del thread al momento della prima esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1873">**entry_input**: A 32-bit value that is passed to the thread’s entry function when it first executes.</span></span> <span data-ttu-id="f7939-1874">L'uso di questo input è determinato esclusivamente dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1874">The use for this input is determined exclusively by the application.</span></span>
- <span data-ttu-id="f7939-1875">**stack_start**: indirizzo iniziale dell'area di memoria dello stack.</span><span class="sxs-lookup"><span data-stu-id="f7939-1875">**stack_start**: Starting address of the stack’s memory area.</span></span> 
- <span data-ttu-id="f7939-1876">**stack_size**: numero di byte nell'area memoria dello stack.</span><span class="sxs-lookup"><span data-stu-id="f7939-1876">**stack_size**: Number bytes in the stack memory area.</span></span> <span data-ttu-id="f7939-1877">L'area dello stack del thread deve essere sufficientemente grande da poter gestire la nidificazione della chiamata di funzione peggiore e l'utilizzo delle variabili locali.</span><span class="sxs-lookup"><span data-stu-id="f7939-1877">The thread’s stack area must be large enough to handle its worst-case function call nesting and local variable usage.</span></span>
- <span data-ttu-id="f7939-1878">**Priority**: priorità numerica del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1878">**priority**: Numerical priority of thread.</span></span> <span data-ttu-id="f7939-1879">I valori validi sono compresi tra 0 e (TX_MAX_PRIORITES-1), dove il valore 0 rappresenta la priorità più alta.</span><span class="sxs-lookup"><span data-stu-id="f7939-1879">Legal values range from 0 through (TX_MAX_PRIORITES-1), where a value of 0 represents the highest priority.</span></span>
- <span data-ttu-id="f7939-1880">**preempt_threshold**: livello di priorità più alto (da 0 a (TX_MAX_PRIORITIES-1)) di precedenza disabilitata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1880">**preempt_threshold**: Highest priority level (0 through (TX_MAX_PRIORITIES-1)) of disabled preemption.</span></span> <span data-ttu-id="f7939-1881">Solo le priorità superiori a questo livello possono essere interrotte dal thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1881">Only priorities higher than this level are allowed to preempt this thread.</span></span> <span data-ttu-id="f7939-1882">Questo valore deve essere minore o uguale alla priorità specificata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1882">This value must be less than or equal to the specified priority.</span></span> <span data-ttu-id="f7939-1883">Un valore uguale alla priorità del thread Disabilita la soglia di precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1883">A value equal to the thread priority disables preemption-threshold.</span></span>
- <span data-ttu-id="f7939-1884">**time_slice**: numero di cicli di esecuzione del timer per cui è consentita l'esecuzione di altri thread pronti con la stessa priorità.</span><span class="sxs-lookup"><span data-stu-id="f7939-1884">**time_slice**: Number of timer-ticks this thread is allowed to run before other ready threads of the same priority are given a chance to run.</span></span> <span data-ttu-id="f7939-1885">Si noti che l'uso della soglia di precedenza Disabilita il sezionamento del tempo.</span><span class="sxs-lookup"><span data-stu-id="f7939-1885">Note that using preemption-threshold disables time-slicing.</span></span> <span data-ttu-id="f7939-1886">I valori validi per le sezioni temporali sono compresi tra 1 e 0xFFFFFFFF (inclusi).</span><span class="sxs-lookup"><span data-stu-id="f7939-1886">Legal time-slice values range from 1 to 0xFFFFFFFF (inclusive).</span></span> <span data-ttu-id="f7939-1887">Il valore **TX_NO_TIME_SLICE** (valore 0) Disabilita il sezionamento del tempo del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1887">A value of **TX_NO_TIME_SLICE** (a value of 0) disables time-slicing of this thread.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f7939-1888">L'uso del sezionamento del tempo comporta una lieve quantità di overhead del sistema.</span><span class="sxs-lookup"><span data-stu-id="f7939-1888">Using time-slicing results in a slight amount of system overhead.</span></span> <span data-ttu-id="f7939-1889">Poiché il sezionamento del tempo è utile solo nei casi in cui più thread condividono la stessa priorità, non è necessario assegnare un intervallo di tempo ai thread con una priorità univoca.</span><span class="sxs-lookup"><span data-stu-id="f7939-1889">Since time-slicing is only useful in cases where multiple threads share the same priority, threads having a unique priority should not be assigned a time-slice.</span></span>

- <span data-ttu-id="f7939-1890">**auto_start**: specifica se il thread viene avviato immediatamente o in stato sospeso.</span><span class="sxs-lookup"><span data-stu-id="f7939-1890">**auto_start**: Specifies whether the thread starts immediately or is placed in a suspended state.</span></span> <span data-ttu-id="f7939-1891">Le opzioni legali sono **TX_AUTO_START** (0x01) e **TX_DONT_START** (0x00).</span><span class="sxs-lookup"><span data-stu-id="f7939-1891">Legal options are **TX_AUTO_START** (0x01) and **TX_DONT_START** (0x00).</span></span> <span data-ttu-id="f7939-1892">Se TX_DONT_START viene specificato, l'applicazione deve chiamare in un secondo momento tx_thread_resume per l'esecuzione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1892">If TX_DONT_START is specified, the application must later call tx_thread_resume in order for the thread to run.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1893">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1893">Return Values</span></span>

- <span data-ttu-id="f7939-1894">**TX_SUCCESS**: (0x00) Creazione thread riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1894">**TX_SUCCESS**: (0x00) Successful thread creation.</span></span>
- <span data-ttu-id="f7939-1895">TX_THREAD_ERROR: (0x0E) puntatore di controllo thread non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1895">TX_THREAD_ERROR: (0x0E) Invalid thread control pointer.</span></span> <span data-ttu-id="f7939-1896">Il puntatore è NULL o il thread è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1896">Either the pointer is NULL or the thread is already created.</span></span>
- <span data-ttu-id="f7939-1897">TX_PTR_ERROR: (0x03) indirizzo iniziale non valido del punto di ingresso o l'area dello stack non è valida, in genere NULL.</span><span class="sxs-lookup"><span data-stu-id="f7939-1897">TX_PTR_ERROR: (0x03) Invalid starting address of the entry point or the stack area is invalid, usually NULL.</span></span>
- <span data-ttu-id="f7939-1898">TX_SIZE_ERROR: le dimensioni (0x05) dell'area dello stack non sono valide.</span><span class="sxs-lookup"><span data-stu-id="f7939-1898">TX_SIZE_ERROR: (0x05) Size of stack area is invalid.</span></span> <span data-ttu-id="f7939-1899">Per eseguire i thread è necessario almeno **TX_MINIMUM_STACK** byte.</span><span class="sxs-lookup"><span data-stu-id="f7939-1899">Threads must have at least **TX_MINIMUM_STACK** bytes to execute.</span></span>
- <span data-ttu-id="f7939-1900">TX_PRIORITY_ERROR: (0x0F) priorità thread non valida, che è un valore non compreso nell'intervallo di (da 0 a (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="f7939-1900">TX_PRIORITY_ERROR: (0x0F) Invalid thread priority, which is a value outside the range of (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="f7939-1901">TX_THRESH_ERROR: (0x18) preemptionthreshold specificato non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1901">TX_THRESH_ERROR: (0x18) Invalid preemptionthreshold specified.</span></span> <span data-ttu-id="f7939-1902">Questo valore deve essere una priorità valida minore o uguale alla priorità iniziale del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1902">This value must be a valid priority less than or equal to the initial priority of the thread.</span></span>
- <span data-ttu-id="f7939-1903">TX_START_ERROR: (0x10) selezione avvio automatico non valida.</span><span class="sxs-lookup"><span data-stu-id="f7939-1903">TX_START_ERROR: (0x10) Invalid auto-start selection.</span></span>
- <span data-ttu-id="f7939-1904">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1904">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1905">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1905">Allowed From</span></span>

<span data-ttu-id="f7939-1906">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="f7939-1906">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1907">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1907">Preemption Possible</span></span>

<span data-ttu-id="f7939-1908">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-1908">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1909">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1909">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Create a thread of priority 15 whose entry point is
   "my_thread_entry". This thread’s stack area is 1000
   bytes in size, starting at address 0x400000. The
   preemption-threshold is setup to allow preemption of threads
   with priorities ranging from 0 through 14. Time-slicing is
   disabled. This thread is automatically put into a ready
   condition. */
status =  tx_thread_create(&my_thread, "my_thread_name",
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
### <a name="see-also"></a><span data-ttu-id="f7939-1910">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1910">See Also</span></span>

- <span data-ttu-id="f7939-1911">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1911">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-1912">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1912">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-1913">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-1913">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-1914">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1914">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-1915">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1915">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-1916">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1916">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1917">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-1917">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-1918">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-1918">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-1919">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-1919">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-1920">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-1920">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-1921">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-1921">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-1922">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-1922">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-1923">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1923">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-1924">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-1924">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-1925">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-1925">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-1926">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-1926">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-1927">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-1927">tx_thread_wait_abort</span></span>

## <a name="tx_thread_delete"></a><span data-ttu-id="f7939-1928">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1928">tx_thread_delete</span></span>

<span data-ttu-id="f7939-1929">Elimina thread applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-1929">Delete application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1930">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1930">Prototype</span></span>

```C
UINT tx_thread_delete(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-1931">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1931">Description</span></span>

<span data-ttu-id="f7939-1932">Questo servizio Elimina il thread dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1932">This service deletes the specified application thread.</span></span> <span data-ttu-id="f7939-1933">Poiché il thread specificato deve essere in uno stato terminato o completato, questo servizio non può essere chiamato da un thread che tenta di eliminare se stesso.</span><span class="sxs-lookup"><span data-stu-id="f7939-1933">Since the specified thread must be in a terminated or completed state, this service cannot be called from a thread attempting to delete itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-1934">È responsabilità dell'applicazione gestire l'area di memoria associata allo stack del thread, disponibile al termine del servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-1934">It is the application’s responsibility to manage the memory area associated with the thread’s stack, which is available after this service completes.</span></span> <span data-ttu-id="f7939-1935">Inoltre, l'applicazione deve impedire l'utilizzo di un thread eliminato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1935">In addition, the application must prevent use of a deleted thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1936">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1936">Parameters</span></span>

- <span data-ttu-id="f7939-1937">**thread_ptr**: puntatore a un thread dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1937">**thread_ptr**: Pointer to a previously created application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1938">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1938">Return Values</span></span>

- <span data-ttu-id="f7939-1939">**TX_SUCCESS**: (0x00) eliminazione thread riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1939">**TX_SUCCESS**: (0x00) Successful thread deletion.</span></span>
- <span data-ttu-id="f7939-1940">TX_THREAD_ERROR: (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1940">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="f7939-1941">**TX_DELETE_ERROR**: (0x11) il thread specificato non è in uno stato terminato o completato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1941">**TX_DELETE_ERROR**: (0x11) Specified thread is not in a terminated or completed state.</span></span>
- <span data-ttu-id="f7939-1942">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1942">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1943">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1943">Allowed From</span></span>

<span data-ttu-id="f7939-1944">Thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-1944">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-1945">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-1945">Preemption Possible</span></span>

<span data-ttu-id="f7939-1946">No</span><span class="sxs-lookup"><span data-stu-id="f7939-1946">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1947">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1947">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Delete an application thread whose control block is
   "my_thread". Assume that the thread has already been
   created with a call to tx_thread_create. */
status =  tx_thread_delete(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-1948">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1948">See Also</span></span>

- <span data-ttu-id="f7939-1949">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1949">tx_thread_create</span></span>
- <span data-ttu-id="f7939-1950">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1950">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-1951">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-1951">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-1952">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1952">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-1953">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1953">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-1954">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1954">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1955">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-1955">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-1956">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-1956">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-1957">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-1957">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-1958">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-1958">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-1959">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-1959">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-1960">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-1960">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-1961">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1961">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-1962">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-1962">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-1963">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-1963">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-1964">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-1964">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-1965">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-1965">tx_thread_wait_abort</span></span>

## <a name="tx_thread_entry_exit_notify"></a><span data-ttu-id="f7939-1966">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1966">tx_thread_entry_exit_notify</span></span>

<span data-ttu-id="f7939-1967">Invia notifica all'applicazione al thread</span><span class="sxs-lookup"><span data-stu-id="f7939-1967">Notify application upon thread entry and exit</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-1968">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-1968">Prototype</span></span>

```C
UINT  tx_thread_entry_exit_notify(TX_THREAD *thread_ptr,
        VOID (*entry_exit_notify)(TX_THREAD *, UINT));
```
### <a name="description"></a><span data-ttu-id="f7939-1969">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-1969">Description</span></span>

<span data-ttu-id="f7939-1970">Questo servizio registra una funzione di callback delle notifiche chiamata ogni volta che il thread specificato viene inserito o chiuso.</span><span class="sxs-lookup"><span data-stu-id="f7939-1970">This service registers a notification callback function that is called whenever the specified thread is entered or exits.</span></span> <span data-ttu-id="f7939-1971">L'elaborazione del callback di notifica viene definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1971">The processing of the notification callback is defined by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="f7939-1972">Il callback di notifica voce/uscita thread dell'applicazione non è autorizzato a chiamare alcuna API SMP di ThreadX con un'opzione di sospensione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1972">The application’s thread entry/exit notification callback is not allowed to call any ThreadX SMP API with a suspension option.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-1973">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-1973">Parameters</span></span>

- <span data-ttu-id="f7939-1974">**thread_ptr**: puntatore al thread creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-1974">**thread_ptr**: Pointer to previously created thread.</span></span>
- <span data-ttu-id="f7939-1975">**entry_exit_notify**: puntatore alla funzione di notifica di ingresso/uscita del thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-1975">**entry_exit_notify**: Pointer to application’s thread entry/exit notification function.</span></span> <span data-ttu-id="f7939-1976">Il secondo parametro della funzione di notifica Entry/Exit indica se è presente una voce o una uscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-1976">The second parameter to the entry/exit notification function designates if an entry or exit is present.</span></span> <span data-ttu-id="f7939-1977">Il valore TX_THREAD_ENTRY (0x00) indica che è stato immesso il thread, mentre il valore TX_THREAD_EXIT (0x01) indica che il thread è stato terminato.</span><span class="sxs-lookup"><span data-stu-id="f7939-1977">The value TX_THREAD_ENTRY (0x00) indicates the thread was entered, while the value TX_THREAD_EXIT (0x01) indicates the thread was exited.</span></span> <span data-ttu-id="f7939-1978">Se questo valore è TX_NULL, la notifica è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="f7939-1978">If this value is TX_NULL, notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-1979">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-1979">Return Values</span></span>

- <span data-ttu-id="f7939-1980">**TX_SUCCESS**: (0x00) registrazione corretta della funzione di notifica di ingresso/uscita del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-1980">**TX_SUCCESS**: (0x00) Successful registration of the thread entry/exit notification function.</span></span>
- <span data-ttu-id="f7939-1981">TX_THREAD_ERROR: (0x0E) puntatore thread non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-1981">TX_THREAD_ERROR: (0x0E) Invalid thread pointer.</span></span>
- <span data-ttu-id="f7939-1982">**TX_FEATURE_NOT_ENABLED (0xFF)** Il sistema è stato compilato con le funzionalità di notifica disabilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-1982">**TX_FEATURE_NOT_ENABLED(0xFF)** The system was compiled with notification capabilities disabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-1983">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-1983">Allowed From</span></span>

<span data-ttu-id="f7939-1984">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-1984">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-1985">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-1985">Example</span></span>

```C
TX_THREAD         my_thread;

/* Register the "my_entry_exit_notify" function for monitoring
   the entry/exit of the thread "my_thread." */
status =  tx_thread_entry_exit_notify(&my_thread,
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

### <a name="see-also"></a><span data-ttu-id="f7939-1986">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-1986">See Also</span></span>

- <span data-ttu-id="f7939-1987">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-1987">tx_thread_create</span></span>
- <span data-ttu-id="f7939-1988">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-1988">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-1989">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-1989">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-1990">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-1990">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-1991">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1991">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-1992">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1992">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-1993">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-1993">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-1994">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-1994">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-1995">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-1995">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-1996">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-1996">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-1997">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-1997">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-1998">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-1998">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-1999">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-1999">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2000">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2000">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2001">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2001">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2002">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2002">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2003">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2003">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2004">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2004">tx_thread_wait_abort</span></span>

## <a name="tx_thread_identify"></a><span data-ttu-id="f7939-2005">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2005">tx_thread_identify</span></span>

<span data-ttu-id="f7939-2006">Recupera il puntatore al thread attualmente in esecuzione</span><span class="sxs-lookup"><span data-stu-id="f7939-2006">Retrieves pointer to currently executing thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2007">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2007">Prototype</span></span>

```C
TX_THREAD* tx_thread_identify(VOID);
```
### <a name="description"></a><span data-ttu-id="f7939-2008">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2008">Description</span></span>

<span data-ttu-id="f7939-2009">Questo servizio restituisce un puntatore al thread attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2009">This service returns a pointer to the currently executing thread.</span></span> <span data-ttu-id="f7939-2010">Se non è in esecuzione alcun thread, il servizio restituisce un puntatore null.</span><span class="sxs-lookup"><span data-stu-id="f7939-2010">If no thread is executing, this service returns a null pointer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2011">Se questo servizio viene chiamato da un ISR, il valore restituito rappresenta il thread in esecuzione prima del gestore di interrupt in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2011">If this service is called from an ISR, the return value represents the thread running prior to the executing interrupt handler.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2012">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2012">Parameters</span></span>

<span data-ttu-id="f7939-2013">nessuno</span><span class="sxs-lookup"><span data-stu-id="f7939-2013">None</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2014">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2014">Return Values</span></span>

- <span data-ttu-id="f7939-2015">puntatore al thread: puntatore al thread attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2015">thread pointer: Pointer to the currently executing thread.</span></span> <span data-ttu-id="f7939-2016">Se non è in esecuzione alcun thread, il valore restituito è TX_NULL.</span><span class="sxs-lookup"><span data-stu-id="f7939-2016">If no thread is executing, the return value is TX_NULL.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2017">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2017">Allowed From</span></span>

<span data-ttu-id="f7939-2018">Thread e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2018">Threads and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2019">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2019">Preemption Possible</span></span>

<span data-ttu-id="f7939-2020">No</span><span class="sxs-lookup"><span data-stu-id="f7939-2020">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2021">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2021">Example</span></span>

```C
TX_THREAD     *my_thread_ptr;

/* Find out who we are! */
my_thread_ptr =  tx_thread_identify();

/* If my_thread_ptr is non-null, we are currently executing
   from that thread or an ISR that interrupted that thread.
   Otherwise, this service was called
   from an ISR when no thread was running when the
   interrupt occurred.  */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2022">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2022">See Also</span></span>

- <span data-ttu-id="f7939-2023">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2023">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2024">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2024">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2025">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2025">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2026">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2026">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2027">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2027">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2028">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2028">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2029">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2029">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2030">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2030">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2031">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2031">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2032">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2032">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2033">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2033">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2034">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2034">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2035">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2035">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2036">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2036">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2037">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2037">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2038">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2038">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2039">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2039">tx_thread_wait_abort</span></span>

## <a name="tx_thread_info_get"></a><span data-ttu-id="f7939-2040">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2040">tx_thread_info_get</span></span>

<span data-ttu-id="f7939-2041">Recuperare informazioni sul thread</span><span class="sxs-lookup"><span data-stu-id="f7939-2041">Retrieve information about thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2042">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2042">Prototype</span></span>

```C
UINT tx_thread_info_get(TX_THREAD *thread_ptr, CHAR **name,
                          UINT *state, ULONG *run_count,
                          UINT *priority,
                          UINT *preemption_threshold,
                          ULONG *time_slice,
                          TX_THREAD **next_thread,
                          TX_THREAD **suspended_thread);
```
### <a name="description"></a><span data-ttu-id="f7939-2043">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2043">Description</span></span>

<span data-ttu-id="f7939-2044">Questo servizio recupera le informazioni sul thread specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2044">This service retrieves information about the specified thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2045">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2045">Parameters</span></span> 

- <span data-ttu-id="f7939-2046">**thread_ptr**: puntatore al blocco di controllo thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2046">**thread_ptr**: Pointer to thread control block.</span></span>
- <span data-ttu-id="f7939-2047">**Name**: puntatore alla destinazione per il puntatore al nome del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2047">**name**: Pointer to destination for the pointer to the thread’s name.</span></span>
- <span data-ttu-id="f7939-2048">**stato**: puntatore alla destinazione per lo stato di esecuzione corrente del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2048">**state**:  Pointer to destination for the thread’s current execution state.</span></span> <span data-ttu-id="f7939-2049">I possibili valori sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="f7939-2049">Possible values are as follows:</span></span>
    - <span data-ttu-id="f7939-2050">**TX_READY**: (0x00)</span><span class="sxs-lookup"><span data-stu-id="f7939-2050">**TX_READY**: (0x00)</span></span>
    - <span data-ttu-id="f7939-2051">**TX_COMPLETED**: (0x01)</span><span class="sxs-lookup"><span data-stu-id="f7939-2051">**TX_COMPLETED**: (0x01)</span></span>
    - <span data-ttu-id="f7939-2052">**TX_TERMINATED**: (0x02)</span><span class="sxs-lookup"><span data-stu-id="f7939-2052">**TX_TERMINATED**: (0x02)</span></span>
    - <span data-ttu-id="f7939-2053">**TX_SUSPENDED**: (0x03)</span><span class="sxs-lookup"><span data-stu-id="f7939-2053">**TX_SUSPENDED**: (0x03)</span></span>
    - <span data-ttu-id="f7939-2054">**TX_SLEEP**: (0x04)</span><span class="sxs-lookup"><span data-stu-id="f7939-2054">**TX_SLEEP**: (0x04)</span></span>
    - <span data-ttu-id="f7939-2055">**TX_QUEUE_SUSP**: (0x05)</span><span class="sxs-lookup"><span data-stu-id="f7939-2055">**TX_QUEUE_SUSP**: (0x05)</span></span>
    - <span data-ttu-id="f7939-2056">**TX_SEMAPHORE_SUSP**: (0x06)</span><span class="sxs-lookup"><span data-stu-id="f7939-2056">**TX_SEMAPHORE_SUSP**: (0x06)</span></span>
    - <span data-ttu-id="f7939-2057">**TX_EVENT_FLAG**: (0x07)</span><span class="sxs-lookup"><span data-stu-id="f7939-2057">**TX_EVENT_FLAG**: (0x07)</span></span>
    - <span data-ttu-id="f7939-2058">**TX_BLOCK_MEMORY**: (0x08)</span><span class="sxs-lookup"><span data-stu-id="f7939-2058">**TX_BLOCK_MEMORY**: (0x08)</span></span>
    - <span data-ttu-id="f7939-2059">**TX_BYTE_MEMORY**: (0x09)</span><span class="sxs-lookup"><span data-stu-id="f7939-2059">**TX_BYTE_MEMORY**: (0x09)</span></span>
    - <span data-ttu-id="f7939-2060">**TX_MUTEX_SUSP**: (0x0D)</span><span class="sxs-lookup"><span data-stu-id="f7939-2060">**TX_MUTEX_SUSP**: (0x0D)</span></span>

- <span data-ttu-id="f7939-2061">**run_count**: puntatore alla destinazione per il numero di esecuzioni del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2061">**run_count**: Pointer to destination for the thread’s run count.</span></span> 
- <span data-ttu-id="f7939-2062">**Priority**: puntatore alla destinazione per la priorità del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2062">**priority**: Pointer to destination for the thread’s priority.</span></span>
- <span data-ttu-id="f7939-2063">**preemption_threshold**: puntatore alla destinazione per la soglia di precedenza del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2063">**preemption_threshold**: Pointer to destination for the thread’s preemption-threshold.</span></span>
- <span data-ttu-id="f7939-2064">**time_slice**: puntatore alla destinazione per la sezione del tempo del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2064">**time_slice**: Pointer to destination for the thread’s time-slice.</span></span> 
- <span data-ttu-id="f7939-2065">**next_thread**: puntatore alla destinazione per il puntatore al thread creato successivo.</span><span class="sxs-lookup"><span data-stu-id="f7939-2065">**next_thread**: Pointer to destination for next created thread pointer.</span></span>
- <span data-ttu-id="f7939-2066">**suspended_thread**: puntatore alla destinazione per il puntatore al thread successivo nell'elenco di sospensioni.</span><span class="sxs-lookup"><span data-stu-id="f7939-2066">**suspended_thread**: Pointer to destination for pointer to next thread in suspension list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2067">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-2067">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2068">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2068">Return Values</span></span>

- <span data-ttu-id="f7939-2069">**TX_SUCCESS**: (0x00) il recupero delle informazioni sul thread riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-2069">**TX_SUCCESS**: (0x00) Successful thread information retrieval.</span></span>
- <span data-ttu-id="f7939-2070">TX_THREAD_ERROR: (0x0E) puntatore di controllo thread non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2070">TX_THREAD_ERROR: (0x0E) Invalid thread control pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2071">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2071">Allowed From</span></span>

<span data-ttu-id="f7939-2072">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2072">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2073">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2073">Preemption Possible</span></span>

<span data-ttu-id="f7939-2074">No</span><span class="sxs-lookup"><span data-stu-id="f7939-2074">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2075">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2075">Example</span></span>

```C
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
status =  tx_thread_info_get(&my_thread, &name,
                  &state, &run_count,
            &priority, &preemption_threshold,
                  &time_slice, &next_thread,&suspended_thread);
/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2076">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2076">See Also</span></span>

- <span data-ttu-id="f7939-2077">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2077">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2078">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2078">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2079">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2079">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2080">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2080">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2081">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2081">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2082">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2082">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2083">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2083">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2084">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2084">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2085">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2085">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2086">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2086">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2087">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2087">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2088">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2088">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2089">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2089">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2090">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2090">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2091">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2091">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2092">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2092">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2093">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2093">tx_thread_wait_abort</span></span>

## <a name="tx_thread_performance_info_get"></a><span data-ttu-id="f7939-2094">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2094">tx_thread_performance_info_get</span></span> 

<span data-ttu-id="f7939-2095">Ottenere informazioni sulle prestazioni del thread</span><span class="sxs-lookup"><span data-stu-id="f7939-2095">Get thread performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2096">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2096">Prototype</span></span>

```C
UINT  tx_thread_performance_info_get(TX_THREAD *thread_ptr,
        ULONG *resumptions, ULONG *suspensions,
        ULONG *solicited_preemptions, ULONG *interrupt_preemptions,
        ULONG *priority_inversions, ULONG *time_slices,
        ULONG *relinquishes, ULONG *timeouts, ULONG *wait_aborts,
        TX_THREAD **last_preempted_by);
```
### <a name="description"></a><span data-ttu-id="f7939-2097">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2097">Description</span></span>

<span data-ttu-id="f7939-2098">Questo servizio recupera le informazioni sulle prestazioni relative al thread specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2098">This service retrieves performance information about the specified thread.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2099">Per consentire a questo servizio di restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_THREAD_ENABLE_PERFORMANCE_INFO** definito.</span><span class="sxs-lookup"><span data-stu-id="f7939-2099">The ThreadX SMP library and application must be built with **TX_THREAD_ENABLE_PERFORMANCE_INFO** defined in order for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2100">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2100">Parameters</span></span> 

- <span data-ttu-id="f7939-2101">**thread_ptr**: puntatore al thread creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-2101">**thread_ptr**: Pointer to previously created thread.</span></span>
- <span data-ttu-id="f7939-2102">**riprese**: puntatore alla destinazione per il numero di ririprese del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2102">**resumptions**: Pointer to destination for the number of resumptions of this thread.</span></span>
- <span data-ttu-id="f7939-2103">**sospensioni**: puntatore alla destinazione per il numero di sospensioni del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2103">**suspensions**: Pointer to destination for the number of suspensions of this thread.</span></span>
- <span data-ttu-id="f7939-2104">**solicited_preemptions**: puntatore alla destinazione per il numero di prelazioni in seguito a una chiamata al servizio API threadX eseguita da questo thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2104">**solicited_preemptions**: Pointer to destination for the number of preemptions as a result of a ThreadX API service call made by this thread.</span></span>
- <span data-ttu-id="f7939-2105">**interrupt_preemptions**: puntatore alla destinazione per il numero di prelazioni di questo thread come risultato dell'elaborazione di interrupt.</span><span class="sxs-lookup"><span data-stu-id="f7939-2105">**interrupt_preemptions**: Pointer to destination for the number of preemptions of this thread as a result of interrupt processing.</span></span>
- <span data-ttu-id="f7939-2106">**priority_inversions**: puntatore alla destinazione per il numero di inversioni di priorità del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2106">**priority_inversions**: Pointer to destination for the number of priority inversions of this thread.</span></span>
- <span data-ttu-id="f7939-2107">**time_slices**: puntatore alla destinazione per il numero di timeslices di questo thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2107">**time_slices**: Pointer to destination for the number of timeslices of this thread.</span></span>
- <span data-ttu-id="f7939-2108">**cede**: puntatore alla destinazione per il numero di thread cedenti eseguiti dal thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2108">**relinquishes**: Pointer to destination for the number of thread relinquishes performed by this thread.</span></span>
- <span data-ttu-id="f7939-2109">**timeout**: puntatore alla destinazione per il numero di timeout di sospensione in questo thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2109">**timeouts**: Pointer to destination for the number of suspension timeouts on this thread.</span></span>
- <span data-ttu-id="f7939-2110">**wait_aborts**: puntatore alla destinazione per il numero di interruzioni di attesa eseguite sul thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2110">**wait_aborts**: Pointer to destination for the number of wait aborts performed on this thread.</span></span>
- <span data-ttu-id="f7939-2111">**last_preempted_by**: puntatore alla destinazione per il puntatore del thread che ha superato l'ultima volta il thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2111">**last_preempted_by**: Pointer to destination for the thread pointer that last preempted this thread.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2112">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-2112">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2113">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2113">Return Values</span></span>

- <span data-ttu-id="f7939-2114">**TX_SUCCESS**: (0x00) ottenere prestazioni thread riuscite.</span><span class="sxs-lookup"><span data-stu-id="f7939-2114">**TX_SUCCESS**: (0x00) Successful thread performance get.</span></span>
- <span data-ttu-id="f7939-2115">**TX_PTR_ERROR**: (0x03) puntatore thread non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2115">**TX_PTR_ERROR**: (0x03) Invalid thread pointer.</span></span>
- <span data-ttu-id="f7939-2116">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-2116">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2117">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2117">Allowed From</span></span>

<span data-ttu-id="f7939-2118">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2118">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2119">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2119">Example</span></span>

```c
TX_THREAD     my_thread;
ULONG         resumptions;
ULONG         suspensions;
ULONG         solicited_preemptions;
ULONG         interrupt_preemptions;
ULONG         priority_inversions;
ULONG         time_slices;
ULONG         relinquishes;
ULONG         timeouts;
ULONG         wait_aborts;
TX_THREAD     *last_preempted_by;

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
### <a name="see-also"></a><span data-ttu-id="f7939-2120">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2120">See Also</span></span>

- <span data-ttu-id="f7939-2121">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2121">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2122">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2122">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2123">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2123">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2124">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2124">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2125">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2125">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2126">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2126">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2127">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2127">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2128">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2128">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2129">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2129">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2130">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2130">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2131">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2131">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2132">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2132">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2133">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2133">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2134">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2134">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2135">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2135">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2136">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2136">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2137">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2137">tx_thread_wait_abort</span></span>

## <a name="tx_thread_performance_system_info_get"></a><span data-ttu-id="f7939-2138">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2138">tx_thread_performance_system_info_get</span></span> 

<span data-ttu-id="f7939-2139">Ottenere informazioni sulle prestazioni del sistema di thread</span><span class="sxs-lookup"><span data-stu-id="f7939-2139">Get thread system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2140">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2140">Prototype</span></span>

```C
UINT tx_thread_performance_system_info_get(ULONG *resumptions,
       ULONG *suspensions, ULONG *solicited_preemptions,
       ULONG *interrupt_preemptions, ULONG *priority_inversions,
       ULONG *time_slices, ULONG *relinquishes, ULONG *timeouts,
       ULONG *wait_aborts, ULONG *non_idle_returns,
       ULONG *idle_returns);
```
### <a name="description"></a><span data-ttu-id="f7939-2141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2141">Description</span></span>

<span data-ttu-id="f7939-2142">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i thread nel sistema.</span><span class="sxs-lookup"><span data-stu-id="f7939-2142">This service retrieves performance information about all the threads in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2143">Per consentire a questo servizio di restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_THREAD_ENABLE_PERFORMANCE_INFO** definito.</span><span class="sxs-lookup"><span data-stu-id="f7939-2143">The ThreadX SMP library and application must be built with **TX_THREAD_ENABLE_PERFORMANCE_INFO** defined in order for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2144">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2144">Parameters</span></span>

- <span data-ttu-id="f7939-2145">**riprese**: puntatore alla destinazione per il numero totale di riprese dei thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2145">**resumptions**: Pointer to destination for the total number of thread resumptions.</span></span>
- <span data-ttu-id="f7939-2146">**sospensioni**: puntatore alla destinazione per il numero totale di sospensioni dei thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2146">**suspensions**: Pointer to destination for the total number of thread suspensions.</span></span>
- <span data-ttu-id="f7939-2147">**solicited_preemptions**: puntatore alla destinazione per il numero totale di operazioni di i/o al secondo di thread in seguito a un thread che chiama un servizio API threadX.</span><span class="sxs-lookup"><span data-stu-id="f7939-2147">**solicited_preemptions**: Pointer to destination for the total number of thread preemptions as a result of a thread calling a ThreadX API service.</span></span>
- <span data-ttu-id="f7939-2148">**interrupt_preemptions**: puntatore alla destinazione per il numero totale di interruzioni di thread in seguito all'elaborazione di interrupt.</span><span class="sxs-lookup"><span data-stu-id="f7939-2148">**interrupt_preemptions**: Pointer to destination for the total number of thread preemptions as a result of interrupt processing.</span></span>
- <span data-ttu-id="f7939-2149">**priority_inversions**: puntatore alla destinazione per il numero totale di inversioni con priorità dei thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2149">**priority_inversions**: Pointer to destination for the total number of thread priority inversions.</span></span>
- <span data-ttu-id="f7939-2150">**time_slices**: puntatore alla destinazione per il numero totale di intervalli di tempo dei thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2150">**time_slices**: Pointer to destination for the total number of thread time-slices.</span></span>
- <span data-ttu-id="f7939-2151">**cede**: puntatore alla destinazione per il numero totale di thread abbandonati.</span><span class="sxs-lookup"><span data-stu-id="f7939-2151">**relinquishes**: Pointer to destination for the total number of thread relinquishes.</span></span>
- <span data-ttu-id="f7939-2152">**timeout**: puntatore alla destinazione per il numero totale di timeout di sospensione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2152">**timeouts**: Pointer to destination for the total number of thread suspension timeouts.</span></span>
- <span data-ttu-id="f7939-2153">**wait_aborts**: puntatore alla destinazione per il numero totale di interruzioni di attesa del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2153">**wait_aborts**: Pointer to destination for the total number of thread wait aborts.</span></span> 
- <span data-ttu-id="f7939-2154">**non_idle_returns**: puntatore alla destinazione per il numero di volte in cui un thread torna al sistema quando un altro thread è pronto per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2154">**non_idle_returns**: Pointer to destination for the number of times a thread returns to the system when another thread is ready to execute.</span></span> 
- <span data-ttu-id="f7939-2155">**idle_returns**: puntatore alla destinazione per il numero di volte in cui un thread torna al sistema quando nessun altro thread è pronto per l'esecuzione (sistema inattivo).</span><span class="sxs-lookup"><span data-stu-id="f7939-2155">**idle_returns**: Pointer to destination for the number of times a thread returns to the system when no other thread is ready to execute (idle system).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2156">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-2156">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2157">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2157">Return Values</span></span>

- <span data-ttu-id="f7939-2158">**TX_SUCCESS**: (0x00) prestazioni del sistema thread riuscite.</span><span class="sxs-lookup"><span data-stu-id="f7939-2158">**TX_SUCCESS**: (0x00) Successful thread system performance get.</span></span>
- <span data-ttu-id="f7939-2159">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-2159">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2160">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2160">Allowed From</span></span>

<span data-ttu-id="f7939-2161">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2161">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2162">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2162">Example</span></span>

```C
ULONG         resumptions;
ULONG         suspensions;
ULONG         solicited_preemptions;
ULONG         interrupt_preemptions;
ULONG         priority_inversions;
ULONG         time_slices;
ULONG         relinquishes;
ULONG         timeouts;
ULONG         wait_aborts;
ULONG         non_idle_returns;
ULONG         idle_returns;

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
### <a name="see-also"></a><span data-ttu-id="f7939-2163">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2163">See Also</span></span>

- <span data-ttu-id="f7939-2164">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2164">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2165">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2165">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2166">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2166">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2167">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2167">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2168">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2168">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2169">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2169">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2170">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2170">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2171">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2171">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2172">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2172">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2173">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2173">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2174">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2174">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2175">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2175">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2176">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2176">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2177">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2177">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2178">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2178">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2179">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2179">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2180">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2180">tx_thread_wait_abort</span></span>

## <a name="tx_thread_preemption_change"></a><span data-ttu-id="f7939-2181">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2181">tx_thread_preemption_change</span></span>

<span data-ttu-id="f7939-2182">Modifica precedenza-soglia del thread dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2182">Change preemption-threshold of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2183">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2183">Prototype</span></span>

```C
UINT tx_thread_preemption_change(TX_THREAD *thread_ptr,
                          UINT new_threshold, UINT *old_threshold);
```
### <a name="description"></a><span data-ttu-id="f7939-2184">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2184">Description</span></span>

<span data-ttu-id="f7939-2185">Questo servizio modifica la soglia di precedenza del thread specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2185">This service changes the preemption-threshold of the specified thread.</span></span> <span data-ttu-id="f7939-2186">La soglia di precedenza impedisce al thread specificato di essere uguale o inferiore al valore della soglia di precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-2186">The preemption-threshold prevents preemption of the specified thread by threads equal to or less than the preemption-threshold value.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2187">Con la soglia di precedenza viene disabilitato il sezionamento del tempo per il thread specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2187">Using preemption-threshold disables time-slicing for the specified thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2188">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2188">Parameters</span></span>

- <span data-ttu-id="f7939-2189">**thread_ptr**: puntatore a un thread dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-2189">**thread_ptr**: Pointer to a previously created application thread.</span></span>
- <span data-ttu-id="f7939-2190">**new_threshold**: nuovo livello di priorità per la soglia di precedenza (da 0 a (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="f7939-2190">**new_threshold**: New preemption-threshold priority level (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="f7939-2191">**old_threshold**: puntatore a una posizione per restituire la soglia di precedenza precedente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2191">**old_threshold**: Pointer to a location to return the previous preemption-threshold.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2192">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2192">Return Values</span></span>

- <span data-ttu-id="f7939-2193">**TX_SUCCESS**: (0x00) la modifica della soglia di precedenza è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2193">**TX_SUCCESS**: (0x00) Successful preemption-threshold change.</span></span>
- <span data-ttu-id="f7939-2194">TX_THREAD_ERROR: (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2194">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="f7939-2195">**TX_THRESH_ERROR**: (0x18) la nuova soglia di precedenza specificata non è una priorità di thread valida (un valore diverso da (da 0 a (TX_MAX_PRIORITIES-1)) o è maggiore di (priorità inferiore) rispetto alla priorità del thread corrente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2195">**TX_THRESH_ERROR**: (0x18) Specified new preemption-threshold is not a valid thread priority (a value other than (0 through (TX_MAX_PRIORITIES-1)) or is greater than (lower priority) than the current thread priority.</span></span>
- <span data-ttu-id="f7939-2196">TX_PTR_ERROR: (0x03) puntatore non valido al percorso di archiviazione preemptionthreshold precedente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2196">TX_PTR_ERROR: (0x03) Invalid pointer to previous preemptionthreshold storage location.</span></span>
- <span data-ttu-id="f7939-2197">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2197">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2198">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2198">Allowed From</span></span>

<span data-ttu-id="f7939-2199">Thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2199">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2200">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2200">Preemption Possible</span></span>

<span data-ttu-id="f7939-2201">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-2201">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2202">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2202">Example</span></span>

```c
TX_THREAD     my_thread;
UINT          my_old_threshold;
UINT          status;

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
### <a name="see-also"></a><span data-ttu-id="f7939-2203">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2203">See Also</span></span>

- <span data-ttu-id="f7939-2204">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2204">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2205">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2205">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2206">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2206">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2207">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2207">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2208">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2208">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2209">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2209">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2210">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2210">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2211">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2211">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2212">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2212">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2213">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2213">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2214">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2214">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2215">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2215">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2216">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2216">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2217">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2217">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2218">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2218">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2219">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2219">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2220">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2220">tx_thread_wait_abort</span></span>

## <a name="tx_thread_priority_change"></a><span data-ttu-id="f7939-2221">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2221">tx_thread_priority_change</span></span>

<span data-ttu-id="f7939-2222">Modificare la priorità del thread dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2222">Change priority of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2223">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2223">Prototype</span></span>

```C
UINT tx_thread_priority_change(TX_THREAD *thread_ptr,
                          UINT new_priority, UINT *old_priority);
```
### <a name="description"></a><span data-ttu-id="f7939-2224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2224">Description</span></span>

<span data-ttu-id="f7939-2225">Questo servizio modifica la priorità del thread specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2225">This service changes the priority of the specified thread.</span></span> <span data-ttu-id="f7939-2226">Le priorità valide sono comprese tra 0 e (TX_MAX_PRIORITES-1), dove 0 rappresenta il livello di priorità più alto.</span><span class="sxs-lookup"><span data-stu-id="f7939-2226">Valid priorities range from 0 through (TX_MAX_PRIORITES-1), where 0 represents the highest priority level.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2227">La soglia di precedenza del thread specificato viene impostata automaticamente sulla nuova priorità.</span><span class="sxs-lookup"><span data-stu-id="f7939-2227">The preemption-threshold of the specified thread is automatically set to the new priority.</span></span> <span data-ttu-id="f7939-2228">Se si desidera una nuova soglia, è necessario utilizzare il servizio **tx_thread_preemption_change** dopo questa chiamata.</span><span class="sxs-lookup"><span data-stu-id="f7939-2228">If a new threshold is desired, the **tx_thread_preemption_change** service must be used after this call.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2229">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2229">Parameters</span></span>

- <span data-ttu-id="f7939-2230">**thread_ptr**: puntatore a un thread dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-2230">**thread_ptr**: Pointer to a previously created application thread.</span></span>
- <span data-ttu-id="f7939-2231">**new_priority**: nuovo livello di priorità del thread (da 0 a (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="f7939-2231">**new_priority**: New thread priority level (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="f7939-2232">**old_priority**: puntatore a una posizione per restituire la priorità precedente del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2232">**old_priority**: Pointer to a location to return the thread’s previous priority.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2233">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2233">Return Values</span></span>

- <span data-ttu-id="f7939-2234">**TX_SUCCESS**: (0x00) la modifica della priorità è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2234">**TX_SUCCESS**: (0x00) Successful priority change.</span></span>
- <span data-ttu-id="f7939-2235">TX_THREAD_ERROR: (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2235">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="f7939-2236">TX_PRIORITY_ERROR: (0x0F) la nuova priorità specificata non è valida (un valore diverso da (da 0 a (TX_MAX_PRIORITIES-1)).</span><span class="sxs-lookup"><span data-stu-id="f7939-2236">TX_PRIORITY_ERROR: (0x0F) Specified new priority is not valid (a value other than (0 through (TX_MAX_PRIORITIES-1)).</span></span>
- <span data-ttu-id="f7939-2237">TX_PTR_ERROR: (0x03) puntatore non valido al percorso di archiviazione con priorità precedente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2237">TX_PTR_ERROR: (0x03) Invalid pointer to previous priority storage location.</span></span>
- <span data-ttu-id="f7939-2238">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2238">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2239">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2239">Allowed From</span></span>

<span data-ttu-id="f7939-2240">Thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2240">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2241">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2241">Preemption Possible</span></span>

<span data-ttu-id="f7939-2242">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-2242">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2243">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2243">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          my_old_priority;
UINT          status;

/* Change the thread represented by "my_thread" to priority
   0. */
status = tx_thread_priority_change(&my_thread,
                            0, &my_old_priority);

/* If status equals TX_SUCCESS, the application thread is
   now at the highest priority level in the system. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2244">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2244">See Also</span></span>

- <span data-ttu-id="f7939-2245">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2245">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2246">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2246">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2247">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2247">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2248">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2248">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2249">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2249">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2250">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2250">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2251">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2251">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2252">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2252">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2253">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2253">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2254">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2254">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2255">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2255">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2256">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2256">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2257">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2257">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2258">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2258">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2259">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2259">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2260">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2260">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2261">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2261">tx_thread_wait_abort</span></span>

## <a name="tx_thread_relinquish"></a><span data-ttu-id="f7939-2262">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2262">tx_thread_relinquish</span></span>

<span data-ttu-id="f7939-2263">Cede il controllo ad altri thread dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2263">Relinquish control to other application threads</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2264">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2264">Prototype</span></span>

```C
VOID tx_thread_relinquish(VOID);
```
### <a name="description"></a><span data-ttu-id="f7939-2265">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2265">Description</span></span>

<span data-ttu-id="f7939-2266">Questo servizio cede il controllo del processore ad altri thread pronti per l'esecuzione con la stessa priorità o con una priorità più alta.</span><span class="sxs-lookup"><span data-stu-id="f7939-2266">This service relinquishes processor control to other ready-to-run threads at the same or higher priority.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2267">Oltre a cedere il controllo ai thread con la stessa priorità, questo servizio rilascia anche il controllo al thread con priorità più elevata impedito dall'esecuzione a causa dell'impostazione della soglia di precedenza del thread corrente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2267">In addition to relinquishing control to threads of the same priority, this service also relinquishes control to the highest-priority thread prevented from execution because of the current thread's preemption-threshold setting.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2268">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2268">Parameters</span></span>

<span data-ttu-id="f7939-2269">nessuno</span><span class="sxs-lookup"><span data-stu-id="f7939-2269">None</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2270">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2270">Return Values</span></span>

<span data-ttu-id="f7939-2271">nessuno</span><span class="sxs-lookup"><span data-stu-id="f7939-2271">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2272">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2272">Allowed From</span></span>

<span data-ttu-id="f7939-2273">Thread</span><span class="sxs-lookup"><span data-stu-id="f7939-2273">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2274">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2274">Preemption Possible</span></span>

<span data-ttu-id="f7939-2275">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-2275">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2276">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2276">Example</span></span>

```C
ULONG run_counter_1 =  0;
ULONG run_counter_2 =  0;

/* Example of two threads relinquishing control to
   each other in an infinite loop. Assume that
   both of these threads are ready and have the same
   priority. The run counters will always stay within one
   of each other. */

VOID  my_first_thread(ULONG thread_input)
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
### <a name="see-also"></a><span data-ttu-id="f7939-2277">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2277">See Also</span></span>

- <span data-ttu-id="f7939-2278">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2278">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2279">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2279">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2280">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2280">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2281">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2281">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2282">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2282">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2283">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2283">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2284">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2284">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2285">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2285">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2286">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2286">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2287">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2287">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2288">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2288">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2289">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2289">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2290">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2290">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2291">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2291">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2292">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2292">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2293">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2293">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2294">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2294">tx_thread_wait_abort</span></span>

## <a name="tx_thread_reset"></a><span data-ttu-id="f7939-2295">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2295">tx_thread_reset</span></span>

<span data-ttu-id="f7939-2296">Reimposta thread</span><span class="sxs-lookup"><span data-stu-id="f7939-2296">Reset thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2297">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2297">Prototype</span></span>

```C
UINT tx_thread_reset(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-2298">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2298">Description</span></span>

<span data-ttu-id="f7939-2299">Questo servizio Reimposta il thread specificato per l'esecuzione nel punto di ingresso definito al momento della creazione del thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2299">This service resets the specified thread to execute at the entry point defined at thread creation.</span></span> <span data-ttu-id="f7939-2300">Il thread deve essere in uno stato **TX_COMPLETED** o **TX_TERMINATED** perché venga reimpostato</span><span class="sxs-lookup"><span data-stu-id="f7939-2300">The thread must be in either a **TX_COMPLETED** or **TX_TERMINATED** state for it to be reset</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2301">Per eseguire nuovamente il thread, è necessario riprenderlo.</span><span class="sxs-lookup"><span data-stu-id="f7939-2301">The thread must be resumed for it to execute again.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2302">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2302">Parameters</span></span> 

- <span data-ttu-id="f7939-2303">**thread_ptr**: puntatore a un thread creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-2303">**thread_ptr**: Pointer to a previously created thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2304">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2304">Return Values</span></span>

- <span data-ttu-id="f7939-2305">**TX_SUCCESS**: (0x00) reimpostazione thread riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2305">**TX_SUCCESS**: (0x00) Successful thread reset.</span></span>
- <span data-ttu-id="f7939-2306">**TX_NOT_DONE**: (0x20) il thread specificato non si trova in uno stato TX_COMPLETED o TX_TERMINATED.</span><span class="sxs-lookup"><span data-stu-id="f7939-2306">**TX_NOT_DONE**: (0x20) Specified thread is not in a TX_COMPLETED or TX_TERMINATED state.</span></span>
- <span data-ttu-id="f7939-2307">TX_THREAD_ERROR: (0x0E) puntatore thread non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2307">TX_THREAD_ERROR: (0x0E) Invalid thread pointer.</span></span>
- <span data-ttu-id="f7939-2308">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2308">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2309">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2309">Allowed From</span></span>

<span data-ttu-id="f7939-2310">Thread</span><span class="sxs-lookup"><span data-stu-id="f7939-2310">Threads</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2311">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2311">Example</span></span>

```C
TX_THREAD     my_thread;

/* Reset the previously created thread "my_thread." */
status = tx_thread_reset(&my_thread);

/* If status is TX_SUCCESS the thread is reset. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2312">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2312">See Also</span></span>

- <span data-ttu-id="f7939-2313">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2313">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2314">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2314">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2315">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2315">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2316">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2316">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2317">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2317">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2318">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2318">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2319">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2319">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2320">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2320">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2321">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2321">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2322">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2322">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2323">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2323">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2324">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2324">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2325">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2325">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2326">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2326">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2327">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2327">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2328">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2328">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2329">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2329">tx_thread_wait_abort</span></span>

## <a name="tx_thread_resume"></a><span data-ttu-id="f7939-2330">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2330">tx_thread_resume</span></span>

<span data-ttu-id="f7939-2331">Riavvia thread dell'applicazione sospesa</span><span class="sxs-lookup"><span data-stu-id="f7939-2331">Resume suspended application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2332">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2332">Prototype</span></span>

```C
UINT tx_thread_resume(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-2333">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2333">Description</span></span>

<span data-ttu-id="f7939-2334">Questo servizio riprende o prepara l'esecuzione di un thread sospeso in precedenza da una chiamata ***tx_thread_suspend*** .</span><span class="sxs-lookup"><span data-stu-id="f7939-2334">This service resumes or prepares for execution a thread that was previously suspended by a ***tx_thread_suspend*** call.</span></span> <span data-ttu-id="f7939-2335">Inoltre, questo servizio riprende i thread creati senza avvio automatico.</span><span class="sxs-lookup"><span data-stu-id="f7939-2335">In addition, this service resumes threads that were created without an automatic start.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2336">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2336">Parameters</span></span>

- <span data-ttu-id="f7939-2337">**thread_ptr**: puntatore a un thread dell'applicazione sospesa.</span><span class="sxs-lookup"><span data-stu-id="f7939-2337">**thread_ptr**: Pointer to a suspended application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2338">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2338">Return Values</span></span>

- <span data-ttu-id="f7939-2339">**TX_SUCCESS**: (0x00) riattivazione thread riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2339">**TX_SUCCESS**: (0x00) Successful thread resume.</span></span>
- <span data-ttu-id="f7939-2340">**TX_SUSPEND_LIFTED**: (0X19) in precedenza l'impostazione della sospensione ritardata è stata revocata.</span><span class="sxs-lookup"><span data-stu-id="f7939-2340">**TX_SUSPEND_LIFTED**: (0x19) Previously set delayed suspension was lifted.</span></span>
- <span data-ttu-id="f7939-2341">TX_THREAD_ERROR: (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2341">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="f7939-2342">**TX_RESUME_ERROR**: (0x12) il thread specificato non è sospeso o è stato precedentemente sospeso da un servizio diverso da **_tx_thread_suspend_**.</span><span class="sxs-lookup"><span data-stu-id="f7939-2342">**TX_RESUME_ERROR**: (0x12) Specified thread is not suspended or was previously suspended by a service other than **_tx_thread_suspend_**.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2343">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2343">Allowed From</span></span>

<span data-ttu-id="f7939-2344">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2344">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2345">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2345">Preemption Possible</span></span>

<span data-ttu-id="f7939-2346">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-2346">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2347">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2347">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Resume the thread represented by "my_thread". */
status =  tx_thread_resume(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
   now ready to execute. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2348">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2348">See Also</span></span>

- <span data-ttu-id="f7939-2349">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2349">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2350">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2350">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2351">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2351">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2352">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2352">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2353">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2353">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2354">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2354">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2355">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2355">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2356">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2356">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2357">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2357">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2358">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2358">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2359">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2359">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2360">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2360">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2361">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2361">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2362">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2362">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2363">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2363">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2364">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2364">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2365">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2365">tx_thread_wait_abort</span></span>

## <a name="tx_thread_sleep"></a><span data-ttu-id="f7939-2366">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2366">tx_thread_sleep</span></span>

<span data-ttu-id="f7939-2367">Sospende il thread corrente per l'ora specificata</span><span class="sxs-lookup"><span data-stu-id="f7939-2367">Suspend current thread for specified time</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2368">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2368">Prototype</span></span>

```C
UINT tx_thread_sleep(ULONG timer_ticks);
```
### <a name="description"></a><span data-ttu-id="f7939-2369">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2369">Description</span></span>

<span data-ttu-id="f7939-2370">Questo servizio fa in modo che il thread chiamante venga sospeso per il numero specificato di cicli del timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2370">This service causes the calling thread to suspend for the specified number of timer ticks.</span></span> <span data-ttu-id="f7939-2371">La quantità di tempo fisico associata a un segno di timer è specifica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2371">The amount of physical time associated with a timer tick is application specific.</span></span> <span data-ttu-id="f7939-2372">Questo servizio può essere chiamato solo da un thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2372">This service can be called only from an application thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2373">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2373">Parameters</span></span>

- <span data-ttu-id="f7939-2374">**timer_ticks**: numero di cicli del timer per sospendere il thread dell'applicazione chiamante, compreso tra 0 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="f7939-2374">**timer_ticks**: The number of timer ticks to suspend the calling application thread, ranging from 0 through 0xFFFFFFFF.</span></span> <span data-ttu-id="f7939-2375">Se viene specificato 0, il servizio restituisce immediatamente il risultato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2375">If 0 is specified, the service returns immediately.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2376">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2376">Return Values</span></span>

- <span data-ttu-id="f7939-2377">**TX_SUCCESS**: (0x00) la sospensione del thread è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2377">**TX_SUCCESS**: (0x00) Successful thread sleep.</span></span>
- <span data-ttu-id="f7939-2378">**TX_WAIT_ABORTED**: la sospensione (0x1A) è stata interrotta da un altro thread, timer o ISR.</span><span class="sxs-lookup"><span data-stu-id="f7939-2378">**TX_WAIT_ABORTED**: (0x1A) Suspension was aborted by another thread, timer, or ISR.</span></span>
- <span data-ttu-id="f7939-2379">**TX_CALLER_ERROR**: servizio (0x13) chiamato da un non thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2379">**TX_CALLER_ERROR**: (0x13) Service called from a non-thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2380">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2380">Allowed From</span></span>

<span data-ttu-id="f7939-2381">Thread</span><span class="sxs-lookup"><span data-stu-id="f7939-2381">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2382">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2382">Preemption Possible</span></span>

<span data-ttu-id="f7939-2383">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-2383">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2384">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2384">Example</span></span>

```C
UINT status;

/* Make the calling thread sleep for 100
   timer-ticks. */
status = tx_thread_sleep(100);

/* If status equals TX_SUCCESS, the currently running
   application thread slept for the specified number of
   timer-ticks. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2385">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2385">See Also</span></span>

- <span data-ttu-id="f7939-2386">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2386">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2387">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2387">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2388">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2388">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2389">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2389">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2390">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2390">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2391">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2391">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2392">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2392">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2393">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2393">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2394">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2394">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2395">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2395">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2396">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2396">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2397">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2397">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2398">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2398">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2399">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2399">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2400">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2400">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2401">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2401">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2402">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2402">tx_thread_wait_abort</span></span>

## <a name="tx_thread_smp_core_exclude"></a><span data-ttu-id="f7939-2403">tx_thread_smp_core_exclude</span><span class="sxs-lookup"><span data-stu-id="f7939-2403">tx_thread_smp_core_exclude</span></span>

<span data-ttu-id="f7939-2404">Escludere l'esecuzione dei thread in un set di core</span><span class="sxs-lookup"><span data-stu-id="f7939-2404">Exclude thread execution on a set of cores</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2405">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2405">Prototype</span></span>

```C
UINT  tx_thread_smp_core_exclude(TX_THREAD *thread_ptr,
                          ULONG exclusion_map);
```
### <a name="description"></a><span data-ttu-id="f7939-2406">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2406">Description</span></span>

<span data-ttu-id="f7939-2407">Questa funzione esclude il thread specificato dall'esecuzione nei core specificati nella mappa di bit denominata "*exclusion_map*".</span><span class="sxs-lookup"><span data-stu-id="f7939-2407">This function excludes the specified thread from executing on the core(s) specified in the bit map called "*exclusion_map*."</span></span> <span data-ttu-id="f7939-2408">Ogni bit in "*exclusion_map*" rappresenta un core (bit 0 rappresenta il nucleo 0 e così via).</span><span class="sxs-lookup"><span data-stu-id="f7939-2408">Each bit in "*exclusion_map*" represents a core (bit 0 represents core 0, etc.).</span></span> <span data-ttu-id="f7939-2409">Se viene impostato il bit, il nucleo corrispondente viene escluso dall'esecuzione del thread specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2409">If the bit is set, the corresponding core is excluded from executing the specified thread.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2410">L'uso dell'esclusione del processore può causare un'ulteriore elaborazione nel thread alla logica di mapping di base per trovare la corrispondenza ottimale.</span><span class="sxs-lookup"><span data-stu-id="f7939-2410">Use of processor exclusion may cause additional processing in the thread to core mapping logic in order to find the optimal match.</span></span> <span data-ttu-id="f7939-2411">Questa elaborazione è limitata dal numero di thread pronti.</span><span class="sxs-lookup"><span data-stu-id="f7939-2411">This processing is bounded by the number of ready threads.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2412">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2412">Parameters</span></span> 

- <span data-ttu-id="f7939-2413">**thread_ptr**: puntatore al thread per modificare l'esclusione di base.</span><span class="sxs-lookup"><span data-stu-id="f7939-2413">**thread_ptr**: Pointer to thread to change the core exclusion.</span></span>
- <span data-ttu-id="f7939-2414">**exclusion_map**: mappa di bit in cui un bit sit indica che tale Core è escluso.</span><span class="sxs-lookup"><span data-stu-id="f7939-2414">**exclusion_map**: Bit map where a sit bit indicates that that core is excluded.</span></span> <span data-ttu-id="f7939-2415">Se si specifica un valore 0, il thread verrà eseguito su qualsiasi core (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="f7939-2415">Supplying a 0 value enables the thread to execute on any core (default).</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2416">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2416">Return Values</span></span>

- <span data-ttu-id="f7939-2417">TX_SUCCESS: (0x00) l'esclusione di base è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2417">TX_SUCCESS: (0x00) Successful core exclusion.</span></span>
- <span data-ttu-id="f7939-2418">TX_THREAD_ERROR: (0x0E) puntatore thread non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2418">TX_THREAD_ERROR: (0x0E) Invalid thread pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2419">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2419">Allowed From</span></span>

<span data-ttu-id="f7939-2420">Inizializzazione, ISRs, thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2420">Initialization, ISRs, threads, and timers</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2421">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2421">Example</span></span>

```C
/* Exclude core 0 for "Thread 0". */
tx_thread_smp_core_exclude(&thread_0, 0x01);
```

### <a name="see-also"></a><span data-ttu-id="f7939-2422">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2422">See Also</span></span>

- <span data-ttu-id="f7939-2423">tx_thread_smp_core_exclude_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2423">tx_thread_smp_core_exclude_get</span></span>
- <span data-ttu-id="f7939-2424">tx_thread_smp_core_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2424">tx_thread_smp_core_get</span></span>

## <a name="tx_thread_smp_core_exclude_get"></a><span data-ttu-id="f7939-2425">tx_thread_smp_core_exclude_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2425">tx_thread_smp_core_exclude_get</span></span>

<span data-ttu-id="f7939-2426">Ottiene l'esclusione principale corrente del thread</span><span class="sxs-lookup"><span data-stu-id="f7939-2426">Gets the thread's current core exclusion</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2427">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2427">Prototype</span></span>

```C
UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr,
                         ULONG *exclusion_map_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-2428">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2428">Description</span></span>

<span data-ttu-id="f7939-2429">Questa funzione restituisce l'elenco di esclusione principale corrente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2429">This function returns the current core exclusion list.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2430">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2430">Parameters</span></span>

- <span data-ttu-id="f7939-2431">**thread_ptr**: puntatore al thread da cui recuperare l'esclusione di base.</span><span class="sxs-lookup"><span data-stu-id="f7939-2431">**thread_ptr**: Pointer to thread from which to retrieve the core exclusion.</span></span>
- <span data-ttu-id="f7939-2432">**exclusion_map_ptr**: destinazione per la mappa di bit di esclusione principale corrente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2432">**exclusion_map_ptr**: Destination for current core exclusion bit map.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2433">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2433">Return Values</span></span>

- <span data-ttu-id="f7939-2434">TX_SUCCESS: (0x00) il recupero dell'esclusione principale del thread è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-2434">TX_SUCCESS: (0x00) Successful retrieval of thread's core exclusion.</span></span>
- <span data-ttu-id="f7939-2435">TX_THREAD_ERROR: (0x0E) puntatore thread non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2435">TX_THREAD_ERROR: (0x0E) Invalid thread pointer.</span></span>
- <span data-ttu-id="f7939-2436">TX_PTR_ERROR: (0x03) puntatore di destinazione di esclusione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2436">TX_PTR_ERROR: (0x03) Invalid exclusion destination pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2437">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2437">Allowed From</span></span>

<span data-ttu-id="f7939-2438">Inizializzazione, ISRs, thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2438">Initialization, ISRs, threads, and timers</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2439">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2439">Example</span></span>

```C
ULONGexcluded_cores;
/* Retrieve the core exclusion for "Thread 0". */
tx_thread_smp_core_exclude_get(&thread_0, &excluded_cores);
```

### <a name="see-also"></a><span data-ttu-id="f7939-2440">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2440">See Also</span></span>

- <span data-ttu-id="f7939-2441">tx_thread_smp_core_exclude</span><span class="sxs-lookup"><span data-stu-id="f7939-2441">tx_thread_smp_core_exclude</span></span>
- <span data-ttu-id="f7939-2442">tx_thread_smp_core_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2442">tx_thread_smp_core_get</span></span>

## <a name="tx_thread_smp_core_get"></a><span data-ttu-id="f7939-2443">tx_thread_smp_core_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2443">tx_thread_smp_core_get</span></span>

<span data-ttu-id="f7939-2444">Recupera il nucleo del chiamante attualmente in esecuzione</span><span class="sxs-lookup"><span data-stu-id="f7939-2444">Retrieve currently executing core of caller</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2445">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2445">Prototype</span></span>

```C
UINT  tx_thread_smp_core_get(void);
```
### <a name="description"></a><span data-ttu-id="f7939-2446">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2446">Description</span></span>

<span data-ttu-id="f7939-2447">Questa funzione restituisce l'ID principale del nucleo che esegue il servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-2447">This function returns the core ID of the core executing this service.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2448">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2448">Parameters</span></span>

<span data-ttu-id="f7939-2449">nessuno</span><span class="sxs-lookup"><span data-stu-id="f7939-2449">None</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2450">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2450">Return Values</span></span>

- <span data-ttu-id="f7939-2451">core_id: ID del nucleo attualmente in esecuzione, da 0 a TX_THREAD_SMP_MAX_CORES-1</span><span class="sxs-lookup"><span data-stu-id="f7939-2451">core_id: ID of currently executing core, (0 through TX_THREAD_SMP_MAX_CORES-1)</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2452">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2452">Allowed From</span></span>

<span data-ttu-id="f7939-2453">Inizializzazione, ISRs, thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2453">Initialization, ISRs, threads, and timers</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2454">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2454">Example</span></span>

```C
UINTcore;
/* Pickup the currently executing core. */
core = tx_thread_smp_core_get();

/* At this point, “core” contains the executing core ID. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2455">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2455">See Also</span></span>

- <span data-ttu-id="f7939-2456">tx_thread_smp_core_exclude</span><span class="sxs-lookup"><span data-stu-id="f7939-2456">tx_thread_smp_core_exclude</span></span>
- <span data-ttu-id="f7939-2457">tx_thread_smp_core_exclude_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2457">tx_thread_smp_core_exclude_get</span></span>

## <a name="tx_thread_stack_error_notify"></a><span data-ttu-id="f7939-2458">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2458">tx_thread_stack_error_notify</span></span>

<span data-ttu-id="f7939-2459">Richiamata della notifica di errore dello stack di thread</span><span class="sxs-lookup"><span data-stu-id="f7939-2459">Register thread stack error notification callback</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2460">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2460">Prototype</span></span>

```C
UINT tx_thread_stack_error_notify(VOID (*error_handler)(TX_THREAD *));
```
### <a name="description"></a><span data-ttu-id="f7939-2461">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2461">Description</span></span>

<span data-ttu-id="f7939-2462">Questo servizio registra una funzione di callback di notifica per la gestione degli errori dello stack di thread.</span><span class="sxs-lookup"><span data-stu-id="f7939-2462">This service registers a notification callback function for handling thread stack errors.</span></span> <span data-ttu-id="f7939-2463">Quando ThreadX SMP rileva un errore dello stack di thread durante l'esecuzione, chiamerà questa funzione di notifica per elaborare l'errore.</span><span class="sxs-lookup"><span data-stu-id="f7939-2463">When ThreadX SMP detects a thread stack error during execution, it will call this notification function to process the error.</span></span> <span data-ttu-id="f7939-2464">L'elaborazione dell'errore è completamente definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2464">Processing of the error is completely defined by the application.</span></span> <span data-ttu-id="f7939-2465">Qualsiasi operazione di sospensione del thread violato per la reimpostazione dell'intero sistema potrebbe essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2465">Anything from suspending the violating thread to resetting the entire system may be done.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2466">Per consentire a questo servizio di restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX con **TX_ENABLE_STACK_CHECKING** definito.</span><span class="sxs-lookup"><span data-stu-id="f7939-2466">The ThreadX SMP library must be built with **TX_ENABLE_STACK_CHECKING** defined in order for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2467">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2467">Parameters</span></span>

- <span data-ttu-id="f7939-2468">**Error_Handler**: puntatore alla funzione di gestione degli errori dello stack dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2468">**error_handler**: Pointer to application’s stack error handling function.</span></span> <span data-ttu-id="f7939-2469">Se questo valore è TX_NULL, la notifica viene disabilitata.</span><span class="sxs-lookup"><span data-stu-id="f7939-2469">If this value is TX_NULL, the notification is disabled.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2470">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2470">Return Values</span></span>

- <span data-ttu-id="f7939-2471">**TX_SUCCESS**: (0x00) reimpostazione thread riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2471">**TX_SUCCESS**: (0x00) Successful thread reset.</span></span>
- <span data-ttu-id="f7939-2472">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-2472">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2473">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2473">Allowed From</span></span>

<span data-ttu-id="f7939-2474">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2474">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2475">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2475">Example</span></span>

```C
void my_stack_error_handler(TX_THREAD *thread_ptr);

/* Register the "my_stack_error_handler" function with ThreadX SMP
   so that thread stack errors can be handled by the application. */
status =  tx_thread_stack_error_notify(my_stack_error_handler);

/* If status is TX_SUCCESS the stack error handler is registered.*/
```
### <a name="see-also"></a><span data-ttu-id="f7939-2476">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2476">See Also</span></span>

- <span data-ttu-id="f7939-2477">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2477">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2478">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2478">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2479">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2479">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2480">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2480">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2481">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2481">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2482">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2482">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2483">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2483">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2484">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2484">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2485">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2485">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2486">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2486">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2487">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2487">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2488">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2488">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2489">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2489">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2490">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2490">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2491">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2491">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2492">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2492">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2493">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2493">tx_thread_wait_abort</span></span>

## <a name="tx_thread_suspend"></a><span data-ttu-id="f7939-2494">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2494">tx_thread_suspend</span></span>

<span data-ttu-id="f7939-2495">Sospendi thread applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2495">Suspend application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2496">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2496">Prototype</span></span>

```C
UINT tx_thread_suspend(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-2497">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2497">Description</span></span>

<span data-ttu-id="f7939-2498">Questo servizio sospende il thread dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2498">This service suspends the specified application thread.</span></span> <span data-ttu-id="f7939-2499">Un thread può chiamare questo servizio per sospendere se stesso.</span><span class="sxs-lookup"><span data-stu-id="f7939-2499">A thread may call this service to suspend itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2500">Se il thread specificato è già sospeso per un altro motivo, questa sospensione viene mantenuta internamente fino a quando non viene sollevata la sospensione precedente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2500">If the specified thread is already suspended for another reason, this suspension is held internally until the prior suspension is lifted.</span></span> <span data-ttu-id="f7939-2501">In tal caso, viene eseguita questa sospensione non condizionale del thread specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2501">When that happens, this unconditional suspension of the specified thread is performed.</span></span> <span data-ttu-id="f7939-2502">Altre richieste di sospensione non condizionale non hanno alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="f7939-2502">Further unconditional suspension requests have no effect.</span></span>

<span data-ttu-id="f7939-2503">Dopo la sospensione, il thread deve essere ripreso da ***tx_thread_resume*** per eseguirlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="f7939-2503">After being suspended, the thread must be resumed by ***tx_thread_resume*** to execute again.</span></span>

## <a name="parameters"></a><span data-ttu-id="f7939-2504">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2504">Parameters</span></span>

- <span data-ttu-id="f7939-2505">**thread_ptr**: puntatore a un thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2505">**thread_ptr**: Pointer to an application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2506">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2506">Return Values</span></span>

- <span data-ttu-id="f7939-2507">**TX_SUCCESS**: (0x00) la sospensione del thread è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2507">**TX_SUCCESS**: (0x00) Successful thread suspend.</span></span>
- <span data-ttu-id="f7939-2508">TX_THREAD_ERROR: (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2508">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="f7939-2509">**TX_SUSPEND_ERROR**: (0x14) il thread specificato è in stato terminato o completato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2509">**TX_SUSPEND_ERROR**: (0x14) Specified thread is in a terminated or completed state.</span></span>
- <span data-ttu-id="f7939-2510">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2510">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2511">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2511">Allowed From</span></span>

<span data-ttu-id="f7939-2512">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2512">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2513">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2513">Preemption Possible</span></span>

<span data-ttu-id="f7939-2514">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-2514">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2515">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2515">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Suspend the thread represented by "my_thread". */
status = tx_thread_suspend(&my_thread);

/* If status equals TX_SUCCESS, the application thread is
   unconditionally suspended. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2516">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2516">See Also</span></span>

- <span data-ttu-id="f7939-2517">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2517">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2518">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2518">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2519">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2519">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2520">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2520">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2521">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2521">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2522">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2522">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2523">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2523">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2524">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2524">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2525">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2525">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2526">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2526">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2527">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2527">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2528">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2528">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2529">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2529">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2530">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2530">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2531">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2531">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2532">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2532">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2533">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2533">tx_thread_wait_abort</span></span>

## <a name="tx_thread_terminate"></a><span data-ttu-id="f7939-2534">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2534">tx_thread_terminate</span></span>

<span data-ttu-id="f7939-2535">Termina il thread dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2535">Terminates application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2536">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2536">Prototype</span></span>

```C
UINT tx_thread_terminate(TX_THREAD *thread_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-2537">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2537">Description</span></span>

<span data-ttu-id="f7939-2538">Questo servizio termina il thread dell'applicazione specificato indipendentemente dal fatto che il thread sia sospeso o meno.</span><span class="sxs-lookup"><span data-stu-id="f7939-2538">This service terminates the specified application thread regardless of whether the thread is suspended or not.</span></span> <span data-ttu-id="f7939-2539">Un thread può chiamare questo servizio per terminare se stesso.</span><span class="sxs-lookup"><span data-stu-id="f7939-2539">A thread may call this service to terminate itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2540">Dopo la terminazione, è necessario reimpostare il thread affinché venga eseguito nuovamente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2540">After being terminated, the thread must be reset for it to execute again.</span></span>

> [!WARNING]
> <span data-ttu-id="f7939-2541">È responsabilità dell'applicazione assicurarsi che il thread si trovi in uno stato appropriato per la terminazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2541">It is the application's responsibility to ensure the thread is in a state suitable for termination.</span></span> <span data-ttu-id="f7939-2542">Un thread, ad esempio, non deve terminare durante l'elaborazione critica dell'applicazione o all'interno di altri componenti del middleware in cui potrebbe lasciare tale elaborazione in uno stato sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="f7939-2542">For example, a thread should not be terminated during critical application processing or inside of other middleware components where it could leave such processing in an unknown state.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2543">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2543">Parameters</span></span>

- <span data-ttu-id="f7939-2544">**thread_ptr**: puntatore al thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2544">**thread_ptr**: Pointer to application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2545">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2545">Return Values</span></span>

- <span data-ttu-id="f7939-2546">**TX_SUCCESS**: (0x00) la terminazione del thread è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2546">**TX_SUCCESS**: (0x00) Successful thread terminate.</span></span>
- <span data-ttu-id="f7939-2547">TX_THREAD_ERROR: (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2547">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="f7939-2548">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2548">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2549">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2549">Allowed From</span></span>

<span data-ttu-id="f7939-2550">Thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2550">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2551">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2551">Preemption Possible</span></span>

<span data-ttu-id="f7939-2552">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-2552">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2553">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2553">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Terminate the thread represented by "my_thread". */
status =  tx_thread_terminate(&my_thread);

/* If status equals TX_SUCCESS, the thread is terminated
   and cannot execute again until it is reset. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2554">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2554">See Also</span></span>

- <span data-ttu-id="f7939-2555">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2555">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2556">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2556">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2557">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2557">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2558">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2558">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2559">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2559">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2560">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2560">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2561">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2561">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2562">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2562">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2563">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2563">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2564">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2564">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2565">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2565">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2566">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2566">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2567">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2567">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2568">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2568">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2569">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2569">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2570">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2570">tx_thread_time_slice_change</span></span>
- <span data-ttu-id="f7939-2571">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2571">tx_thread_wait_abort</span></span>

## <a name="tx_thread_time_slice_change"></a><span data-ttu-id="f7939-2572">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2572">tx_thread_time_slice_change</span></span>

<span data-ttu-id="f7939-2573">Modifica la sezione temporale del thread dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2573">Changes time-slice of application thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2574">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2574">Prototype</span></span>

```C
UINT tx_thread_time_slice_change(TX_THREAD *thread_ptr,
                          ULONG new_time_slice, ULONG *old_time_slice);
```
### <a name="description"></a><span data-ttu-id="f7939-2575">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2575">Description</span></span>

<span data-ttu-id="f7939-2576">Questo servizio modifica la porzione di tempo del thread dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2576">This service changes the time-slice of the specified application thread.</span></span> <span data-ttu-id="f7939-2577">Se si seleziona un intervallo di tempo per un thread, si assicura che non venga eseguito un numero di cicli del timer superiore a quello specificato prima che sia possibile eseguire gli altri thread con priorità uguale o superiore.</span><span class="sxs-lookup"><span data-stu-id="f7939-2577">Selecting a time-slice for a thread insures that it won’t execute more than the specified number of timer ticks before other threads of the same or higher priorities have a chance to execute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2578">Con la soglia di precedenza viene disabilitato il sezionamento del tempo per il thread specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2578">Using preemption-threshold disables time-slicing for the specified thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2579">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2579">Parameters</span></span>

- <span data-ttu-id="f7939-2580">**thread_ptr**: puntatore al thread dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2580">**thread_ptr**: Pointer to application thread.</span></span>
- <span data-ttu-id="f7939-2581">**new_time_slice**: nuovo valore della sezione di tempo.</span><span class="sxs-lookup"><span data-stu-id="f7939-2581">**new_time_slice**: New time slice value.</span></span> <span data-ttu-id="f7939-2582">I valori validi includono TX_NO_TIME_SLICE e i valori numerici da 1 a 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="f7939-2582">Legal values include TX_NO_TIME_SLICE and numeric values from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="f7939-2583">**old_time_slice**: puntatore alla posizione per archiviare il valore TimeSlice precedente del thread specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2583">**old_time_slice**: Pointer to location for storing the previous timeslice value of the specified thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2584">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2584">Return Values</span></span>

- <span data-ttu-id="f7939-2585">**TX_SUCCESS**: (0x00) la probabilità del tempo di sezionamento è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2585">**TX_SUCCESS**: (0x00) Successful time-slice chance.</span></span>
- <span data-ttu-id="f7939-2586">TX_THREAD_ERROR: (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2586">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="f7939-2587">TX_PTR_ERROR: (0x03) puntatore non valido al percorso di archiviazione del periodo di tempo precedente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2587">TX_PTR_ERROR: (0x03) Invalid pointer to previous time-slice storage location.</span></span>
- <span data-ttu-id="f7939-2588">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2588">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2589">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2589">Allowed From</span></span>

<span data-ttu-id="f7939-2590">Thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2590">Threads and timers</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2591">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2591">Preemption Possible</span></span>

<span data-ttu-id="f7939-2592">No</span><span class="sxs-lookup"><span data-stu-id="f7939-2592">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2593">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2593">Example</span></span>

```C
TX_THREAD     my_thread;
ULONG         my_old_time_slice;
UINT          status;

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
### <a name="see-also"></a><span data-ttu-id="f7939-2594">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2594">See Also</span></span>

- <span data-ttu-id="f7939-2595">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2595">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2596">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2596">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2597">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2597">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2598">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2598">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2599">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2599">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2600">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2600">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2601">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2601">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2602">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2602">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2603">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2603">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2604">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2604">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2605">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2605">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2606">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2606">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2607">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2607">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2608">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2608">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2609">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2609">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2610">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2610">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2611">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2611">tx_thread_wait_abort</span></span>

## <a name="tx_thread_wait_abort"></a><span data-ttu-id="f7939-2612">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="f7939-2612">tx_thread_wait_abort</span></span>

<span data-ttu-id="f7939-2613">Interrompi sospensione del thread specificato</span><span class="sxs-lookup"><span data-stu-id="f7939-2613">Abort suspension of specified thread</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2614">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2614">Prototype</span></span>

```C
UINT tx_thread_wait_abort(TX_THREAD *thread_ptr);
```

### <a name="description"></a><span data-ttu-id="f7939-2615">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2615">Description</span></span>

<span data-ttu-id="f7939-2616">Questo servizio interrompe il sonno o qualsiasi altra sospensione di oggetti del thread specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2616">This service aborts sleep or any other object suspension of the specified thread.</span></span> <span data-ttu-id="f7939-2617">Se l'attesa viene interrotta, viene restituito un valore TX_WAIT_ABORTED dal servizio su cui il thread era in attesa.</span><span class="sxs-lookup"><span data-stu-id="f7939-2617">If the wait is aborted, a TX_WAIT_ABORTED value is returned from the service that the thread was waiting on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2618">Questo servizio non rilascia sospensioni esplicite effettuate dal servizio tx_thread_suspend.</span><span class="sxs-lookup"><span data-stu-id="f7939-2618">This service does not release explicit suspension that is made by the tx_thread_suspend service.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2619">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2619">Parameters</span></span>

- <span data-ttu-id="f7939-2620">**thread_ptr**: puntatore a un thread dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-2620">**thread_ptr**: Pointer to a previously created application thread.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2621">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2621">Return Values</span></span>

- <span data-ttu-id="f7939-2622">**TX_SUCCESS**: (0x00) interruzione attesa thread riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2622">**TX_SUCCESS**: (0x00) Successful thread wait abort.</span></span>
- <span data-ttu-id="f7939-2623">TX_THREAD_ERROR: (0x0E) puntatore al thread dell'applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2623">TX_THREAD_ERROR: (0x0E) Invalid application thread pointer.</span></span>
- <span data-ttu-id="f7939-2624">**TX_WAIT_ABORT_ERROR**: (0x1B) il thread specificato non si trova in uno stato di attesa.</span><span class="sxs-lookup"><span data-stu-id="f7939-2624">**TX_WAIT_ABORT_ERROR**: (0x1B) Specified thread is not in a waiting state.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2625">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2625">Allowed From</span></span>

<span data-ttu-id="f7939-2626">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2626">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2627">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2627">Preemption Possible</span></span>

<span data-ttu-id="f7939-2628">Sì</span><span class="sxs-lookup"><span data-stu-id="f7939-2628">Yes</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2629">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2629">Example</span></span>

```C
TX_THREAD     my_thread;
UINT          status;

/* Abort the suspension condition of "my_thread." */
status =  tx_thread_wait_abort(&my_thread);

/* If status equals TX_SUCCESS, the thread is now ready
   again, with a return value showing its suspension
   was aborted (TX_WAIT_ABORTED). */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2630">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2630">See Also</span></span>

- <span data-ttu-id="f7939-2631">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2631">tx_thread_create</span></span>
- <span data-ttu-id="f7939-2632">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2632">tx_thread_delete</span></span>
- <span data-ttu-id="f7939-2633">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2633">tx_thread_entry_exit_notify</span></span>
- <span data-ttu-id="f7939-2634">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="f7939-2634">tx_thread_identify</span></span>
- <span data-ttu-id="f7939-2635">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2635">tx_thread_info_get</span></span>
- <span data-ttu-id="f7939-2636">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2636">tx_thread_performance_info_get</span></span>
- <span data-ttu-id="f7939-2637">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2637">tx_thread_performance_system_info_get</span></span>
- <span data-ttu-id="f7939-2638">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2638">tx_thread_preemption_change</span></span>
- <span data-ttu-id="f7939-2639">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2639">tx_thread_priority_change</span></span>
- <span data-ttu-id="f7939-2640">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="f7939-2640">tx_thread_relinquish</span></span>
- <span data-ttu-id="f7939-2641">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="f7939-2641">tx_thread_reset</span></span>
- <span data-ttu-id="f7939-2642">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="f7939-2642">tx_thread_resume</span></span>
- <span data-ttu-id="f7939-2643">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="f7939-2643">tx_thread_sleep</span></span>
- <span data-ttu-id="f7939-2644">tx_thread_stack_error_notify</span><span class="sxs-lookup"><span data-stu-id="f7939-2644">tx_thread_stack_error_notify</span></span>
- <span data-ttu-id="f7939-2645">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="f7939-2645">tx_thread_suspend</span></span>
- <span data-ttu-id="f7939-2646">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="f7939-2646">tx_thread_terminate</span></span>
- <span data-ttu-id="f7939-2647">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2647">tx_thread_time_slice_change</span></span>

## <a name="tx_time_get"></a><span data-ttu-id="f7939-2648">tx_time_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2648">tx_time_get</span></span>

<span data-ttu-id="f7939-2649">Recupera l'ora corrente</span><span class="sxs-lookup"><span data-stu-id="f7939-2649">Retrieves the current time</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2650">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2650">Prototype</span></span>

```C
ULONG tx_time_get(VOID);
```
### <a name="description"></a><span data-ttu-id="f7939-2651">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2651">Description</span></span>

<span data-ttu-id="f7939-2652">Questo servizio restituisce il contenuto del clock di sistema interno.</span><span class="sxs-lookup"><span data-stu-id="f7939-2652">This service returns the contents of the internal system clock.</span></span> <span data-ttu-id="f7939-2653">Ogni TimerTick aumenta il clock di sistema interno di uno.</span><span class="sxs-lookup"><span data-stu-id="f7939-2653">Each timertick increases the internal system clock by one.</span></span> <span data-ttu-id="f7939-2654">Il clock di sistema è impostato su zero durante l'inizializzazione e può essere modificato in un valore specifico dal servizio ***tx_time_set***.</span><span class="sxs-lookup"><span data-stu-id="f7939-2654">The system clock is set to zero during initialization and can be changed to a specific value by the service ***tx_time_set***.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2655">Il tempo effettivo rappresentato da ogni segno di timer è specifico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2655">The actual time each timer-tick represents is application specific.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2656">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2656">Parameters</span></span>

<span data-ttu-id="f7939-2657">nessuno</span><span class="sxs-lookup"><span data-stu-id="f7939-2657">None</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2658">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2658">Return Values</span></span>

- <span data-ttu-id="f7939-2659">Tick dell'orologio di sistema: valore dell'orologio di sistema interno, libero in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2659">system clock ticks: Value of the internal, free running, system clock.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2660">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2660">Allowed From</span></span>

<span data-ttu-id="f7939-2661">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2661">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2662">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2662">Preemption Possible</span></span>

<span data-ttu-id="f7939-2663">No</span><span class="sxs-lookup"><span data-stu-id="f7939-2663">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2664">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2664">Example</span></span>

```C
ULONG current_time;

/* Pickup the current system time, in timer-ticks. */
current_time =  tx_time_get();

/* Current time now contains a copy of the internal system
   clock. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2665">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2665">See Also</span></span>

- <span data-ttu-id="f7939-2666">tx_time_set</span><span class="sxs-lookup"><span data-stu-id="f7939-2666">tx_time_set</span></span>

## <a name="tx_time_set"></a><span data-ttu-id="f7939-2667">tx_time_set</span><span class="sxs-lookup"><span data-stu-id="f7939-2667">tx_time_set</span></span>

<span data-ttu-id="f7939-2668">Imposta l'ora corrente</span><span class="sxs-lookup"><span data-stu-id="f7939-2668">Sets the current time</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2669">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2669">Prototype</span></span>

```C
VOID tx_time_set(ULONG new_time);
```
### <a name="description"></a><span data-ttu-id="f7939-2670">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2670">Description</span></span>

<span data-ttu-id="f7939-2671">Questo servizio imposta l'orologio di sistema interno sul valore specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2671">This service sets the internal system clock to the specified value.</span></span> <span data-ttu-id="f7939-2672">Ogni timer-tick aumenta il clock di sistema interno di uno.</span><span class="sxs-lookup"><span data-stu-id="f7939-2672">Each timer-tick increases the internal system clock by one.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2673">Il tempo effettivo rappresentato da ogni segno di timer è specifico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2673">The actual time each timer-tick represents is application specific.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2674">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2674">Parameters</span></span>

- <span data-ttu-id="f7939-2675">**New_time**: nuova ora da inserire nel clock di sistema, i valori validi sono compresi tra 0 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="f7939-2675">**new_time**: New time to put in the system clock, legal values range from 0 through 0xFFFFFFFF.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2676">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2676">Return Values</span></span>

<span data-ttu-id="f7939-2677">nessuno</span><span class="sxs-lookup"><span data-stu-id="f7939-2677">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2678">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2678">Allowed From</span></span>

<span data-ttu-id="f7939-2679">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2679">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2680">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2680">Preemption Possible</span></span>

<span data-ttu-id="f7939-2681">No</span><span class="sxs-lookup"><span data-stu-id="f7939-2681">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2682">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2682">Example</span></span>

```c
/* Set the internal system time to 0x1234. */
tx_time_set(0x1234);

/* Current time now contains 0x1234 until the next timer
   interrupt. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2683">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2683">See Also</span></span>

- <span data-ttu-id="f7939-2684">tx_time_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2684">tx_time_get</span></span>

## <a name="tx_timer_activate"></a><span data-ttu-id="f7939-2685">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="f7939-2685">tx_timer_activate</span></span>

<span data-ttu-id="f7939-2686">Attiva timer applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2686">Activate application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2687">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2687">Prototype</span></span>

```C
UINT tx_timer_activate(TX_TIMER *timer_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-2688">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2688">Description</span></span>

<span data-ttu-id="f7939-2689">Questo servizio attiva il timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2689">This service activates the specified application timer.</span></span> <span data-ttu-id="f7939-2690">Le routine di scadenza dei timer che scadono nello stesso momento vengono eseguite nell'ordine in cui sono state attivate.</span><span class="sxs-lookup"><span data-stu-id="f7939-2690">The expiration routines of timers that expire at the same time are executed in the order they were activated.</span></span>

> [!NOTE]
> <span data-ttu-id="f7939-2691">Che un timer scaduto scaduto debba essere reimpostato tramite **tx_timer_change** prima che possa essere nuovamente attivato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2691">That an expired one-shot timer must be reset via **tx_timer_change** before it can be activated again.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2692">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2692">Parameters</span></span>

- <span data-ttu-id="f7939-2693">**timer_ptr**: puntatore a un timer dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-2693">**timer_ptr**: Pointer to a previously created application timer.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2694">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2694">Return Values</span></span>

- <span data-ttu-id="f7939-2695">**TX_SUCCESS**: (0x00) attivazione del timer applicazione completata.</span><span class="sxs-lookup"><span data-stu-id="f7939-2695">**TX_SUCCESS**: (0x00) Successful application timer activation.</span></span>
- <span data-ttu-id="f7939-2696">**TX_TIMER_ERROR**: (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2696">**TX_TIMER_ERROR**: (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="f7939-2697">**TX_ACTIVATE_ERROR**: il timer (0x17) è già attivo o è un timer monouso che è già scaduto.</span><span class="sxs-lookup"><span data-stu-id="f7939-2697">**TX_ACTIVATE_ERROR**: (0x17) Timer was already active or is a one-shot timer that has already expired.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2698">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2698">Allowed From</span></span>

<span data-ttu-id="f7939-2699">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2699">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2700">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2700">Preemption Possible</span></span>

<span data-ttu-id="f7939-2701">No</span><span class="sxs-lookup"><span data-stu-id="f7939-2701">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2702">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2702">Example</span></span>

```C
TX_TIMER     my_timer;
UINT         status;

/* Activate an application timer. Assume that the
   application timer has already been created. */
status = tx_timer_activate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
   now active. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2703">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2703">See Also</span></span>

- <span data-ttu-id="f7939-2704">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2704">tx_timer_change</span></span>
- <span data-ttu-id="f7939-2705">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2705">tx_timer_create</span></span>
- <span data-ttu-id="f7939-2706">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="f7939-2706">tx_timer_deactivate</span></span>
- <span data-ttu-id="f7939-2707">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2707">tx_timer_delete</span></span>
- <span data-ttu-id="f7939-2708">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2708">tx_timer_info_get</span></span>
- <span data-ttu-id="f7939-2709">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2709">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="f7939-2710">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2710">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_change"></a><span data-ttu-id="f7939-2711">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2711">tx_timer_change</span></span>

<span data-ttu-id="f7939-2712">Modifica timer applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2712">Change application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2713">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2713">Prototype</span></span>

```C
UINT tx_timer_change(TX_TIMER *timer_ptr,
                          ULONG initial_ticks, ULONG reschedule_ticks);
```
### <a name="description"></a><span data-ttu-id="f7939-2714">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2714">Description</span></span>

<span data-ttu-id="f7939-2715">Questo servizio modifica le caratteristiche di scadenza del timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2715">This service changes the expiration characteristics of the specified application timer.</span></span> <span data-ttu-id="f7939-2716">Il timer deve essere disattivato prima di chiamare il servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-2716">The timer must be deactivated prior to calling this service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2717">Una chiamata al servizio **tx_timer_activate** è necessaria dopo questo servizio per poter riavviare il timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2717">A call to the **tx_timer_activate** service is required after this service in order to start the timer again.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2718">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2718">Parameters</span></span>

- <span data-ttu-id="f7939-2719">**timer_ptr**: puntatore a un blocco di controllo timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2719">**timer_ptr**: Pointer to a timer control block.</span></span>
- <span data-ttu-id="f7939-2720">**initial_ticks**: specifica il numero iniziale di cicli per la scadenza del timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2720">**initial_ticks**: Specifies the initial number of ticks for timer expiration.</span></span> <span data-ttu-id="f7939-2721">I valori validi sono compresi tra 1 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="f7939-2721">Legal values range from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="f7939-2722">**reschedule_ticks**: specifica il numero di cicli per tutte le scadenze del timer dopo la prima.</span><span class="sxs-lookup"><span data-stu-id="f7939-2722">**reschedule_ticks**: Specifies the number of ticks for all timer expirations after the first.</span></span> <span data-ttu-id="f7939-2723">Uno zero per questo parametro rende il timer un timer unico.</span><span class="sxs-lookup"><span data-stu-id="f7939-2723">A zero for this parameter makes the timer a one-shot timer.</span></span> <span data-ttu-id="f7939-2724">In caso contrario, per i timer periodici i valori validi sono compresi tra 1 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="f7939-2724">Otherwise, for periodic timers, legal values range from 1 through 0xFFFFFFFF.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f7939-2725">Che un timer scaduto scaduto debba essere reimpostato tramite **tx_timer_change** prima che possa essere nuovamente attivato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2725">That an expired one-shot timer must be reset via **tx_timer_change** before it can be activated again.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2726">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2726">Return Values</span></span>

- <span data-ttu-id="f7939-2727">**TX_SUCCESS**: (0x00) la modifica del timer applicazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2727">**TX_SUCCESS**: (0x00) Successful application timer change.</span></span>
- <span data-ttu-id="f7939-2728">TX_TIMER_ERROR: (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2728">TX_TIMER_ERROR: (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="f7939-2729">TX_TICK_ERROR: (0x16) valore non valido (zero) fornito per i cicli iniziali.</span><span class="sxs-lookup"><span data-stu-id="f7939-2729">TX_TICK_ERROR: (0x16) Invalid value (a zero) supplied for initial ticks.</span></span>
- <span data-ttu-id="f7939-2730">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2730">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2731">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2731">Allowed From</span></span>

<span data-ttu-id="f7939-2732">Thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2732">Threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2733">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2733">Preemption Possible</span></span>

<span data-ttu-id="f7939-2734">No</span><span class="sxs-lookup"><span data-stu-id="f7939-2734">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2735">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2735">Example</span></span>

```C
TX_TIMER         my_timer;
UINT             status;

/* Change a previously created and now deactivated timer
   to expire every 50 timer ticks, including the initial
   expiration. */
status =  tx_timer_change(&my_timer,50, 50);

/* If status equals TX_SUCCESS, the specified timer is
   changed to expire every 50 ticks. */

/* Activate the specified timer to get it started again. */
status = tx_timer_activate(&my_timer);
```
### <a name="see-also"></a><span data-ttu-id="f7939-2736">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2736">See Also</span></span>

- <span data-ttu-id="f7939-2737">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="f7939-2737">tx_timer_activate</span></span>
- <span data-ttu-id="f7939-2738">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2738">tx_timer_create</span></span>
- <span data-ttu-id="f7939-2739">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="f7939-2739">tx_timer_deactivate</span></span>
- <span data-ttu-id="f7939-2740">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2740">tx_timer_delete</span></span>
- <span data-ttu-id="f7939-2741">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2741">tx_timer_info_get</span></span>
- <span data-ttu-id="f7939-2742">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2742">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="f7939-2743">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2743">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_create"></a><span data-ttu-id="f7939-2744">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2744">tx_timer_create</span></span>

<span data-ttu-id="f7939-2745">Crea timer applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2745">Create application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2746">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2746">Prototype</span></span>

```C
UINT tx_timer_create(TX_TIMER *timer_ptr, CHAR *name_ptr,
                          VOID (*expiration_function)(ULONG),
                          ULONG expiration_input, ULONG initial_ticks,
                          ULONG reschedule_ticks, UINT auto_activate)
```
### <a name="description"></a><span data-ttu-id="f7939-2747">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2747">Description</span></span>

<span data-ttu-id="f7939-2748">Questo servizio crea un timer dell'applicazione con la funzione di scadenza specificata e periodica.</span><span class="sxs-lookup"><span data-stu-id="f7939-2748">This service creates an application timer with the specified expiration function and periodic.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2749">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2749">Parameters</span></span>

- <span data-ttu-id="f7939-2750">**timer_ptr**: puntatore a un blocco di controllo timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2750">**timer_ptr**: Pointer to a timer control block</span></span>
- <span data-ttu-id="f7939-2751">**name_ptr**: puntatore al nome del timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2751">**name_ptr**: Pointer to the name of the timer.</span></span>
- <span data-ttu-id="f7939-2752">**expiration_function**: funzione dell'applicazione da chiamare quando il timer scade.</span><span class="sxs-lookup"><span data-stu-id="f7939-2752">**expiration_function**: Application function to call when the timer expires.</span></span>
- <span data-ttu-id="f7939-2753">**expiration_input**: input da passare alla funzione di scadenza quando il timer scade.</span><span class="sxs-lookup"><span data-stu-id="f7939-2753">**expiration_input**: Input to pass to expiration function when timer expires.</span></span>
- <span data-ttu-id="f7939-2754">**initial_ticks**: specifica il numero iniziale di cicli per la scadenza del timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2754">**initial_ticks**: Specifies the initial number of ticks for timer expiration.</span></span> <span data-ttu-id="f7939-2755">I valori validi sono compresi tra 1 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="f7939-2755">Legal values range from 1 through 0xFFFFFFFF.</span></span>
- <span data-ttu-id="f7939-2756">**reschedule_ticks**: specifica il numero di cicli per tutte le scadenze del timer dopo la prima.</span><span class="sxs-lookup"><span data-stu-id="f7939-2756">**reschedule_ticks**: Specifies the number of ticks for all timer expirations after the first.</span></span> <span data-ttu-id="f7939-2757">Uno zero per questo parametro rende il timer un timer unico.</span><span class="sxs-lookup"><span data-stu-id="f7939-2757">A zero for this parameter makes the timer a one-shot timer.</span></span> <span data-ttu-id="f7939-2758">In caso contrario, per i timer periodici i valori validi sono compresi tra 1 e 0xFFFFFFFF.</span><span class="sxs-lookup"><span data-stu-id="f7939-2758">Otherwise, for periodic timers, legal values range from 1 through 0xFFFFFFFF.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f7939-2759">Dopo la scadenza di un timer, è necessario reimpostarlo tramite tx_timer_change prima che sia possibile attivarlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="f7939-2759">After a one-shot timer expires, it must be reset via tx_timer_change before it can be activated again.</span></span>

- <span data-ttu-id="f7939-2760">**AUTO_ACTIVATE**: determina se il timer viene attivato automaticamente durante la creazione.</span><span class="sxs-lookup"><span data-stu-id="f7939-2760">**auto_activate**: Determines if the timer is automatically activated during creation.</span></span> <span data-ttu-id="f7939-2761">Se questo valore è **TX_AUTO_ACTIVATE** (0x01), il timer viene reso attivo.</span><span class="sxs-lookup"><span data-stu-id="f7939-2761">If this value is **TX_AUTO_ACTIVATE** (0x01) the timer is made active.</span></span> <span data-ttu-id="f7939-2762">In caso contrario, se si seleziona il valore **TX_NO_ACTIVATE** (0x00), il timer viene creato in uno stato non attivo.</span><span class="sxs-lookup"><span data-stu-id="f7939-2762">Otherwise, if the value **TX_NO_ACTIVATE** (0x00) is selected, the timer is created in a non-active state.</span></span> <span data-ttu-id="f7939-2763">In questo caso, è necessaria una chiamata al servizio **_tx_timer_activate_** successiva per avviare effettivamente il timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2763">In this case, a subsequent **_tx_timer_activate_** service call is necessary to get the timer actually started.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2764">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2764">Return Values</span></span>

- <span data-ttu-id="f7939-2765">**TX_SUCCESS**: (0x00) la creazione del timer applicazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2765">**TX_SUCCESS**: (0x00) Successful application timer creation.</span></span>
- <span data-ttu-id="f7939-2766">TX_TIMER_ERROR: (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2766">TX_TIMER_ERROR: (0x15) Invalid application timer pointer.</span></span> <span data-ttu-id="f7939-2767">Il puntatore è NULL o il timer è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2767">Either the pointer is NULL or the timer is already created.</span></span>
- <span data-ttu-id="f7939-2768">TX_TICK_ERROR: (0x16) valore non valido (zero) fornito per i cicli iniziali.</span><span class="sxs-lookup"><span data-stu-id="f7939-2768">TX_TICK_ERROR: (0x16) Invalid value (a zero) supplied for initial ticks.</span></span>
- <span data-ttu-id="f7939-2769">TX_ACTIVATE_ERROR: (0x17) è stata selezionata l'attivazione non valida.</span><span class="sxs-lookup"><span data-stu-id="f7939-2769">TX_ACTIVATE_ERROR: (0x17) Invalid activation selected.</span></span>
- <span data-ttu-id="f7939-2770">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2770">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2771">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2771">Allowed From</span></span>

<span data-ttu-id="f7939-2772">Inizializzazione e thread</span><span class="sxs-lookup"><span data-stu-id="f7939-2772">Initialization and threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2773">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2773">Preemption Possible</span></span>

<span data-ttu-id="f7939-2774">No</span><span class="sxs-lookup"><span data-stu-id="f7939-2774">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2775">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2775">Example</span></span>

```C
TX_TIMER     my_timer;
UINT         status;

/* Create an application timer that executes
   "my_timer_function" after 100 ticks initially and then
   after every 25 ticks. This timer is specified to start
   immediately! */
status =  tx_timer_create(&my_timer,"my_timer_name",
                my_timer_function, 0x1234, 100, 25,
                TX_AUTO_ACTIVATE);

/* If status equals TX_SUCCESS, my_timer_function will
   be called 100 timer ticks later and then called every
   25 timer ticks. Note that the value 0x1234 is passed to
   my_timer_function every time it is called. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2776">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2776">See Also</span></span>

- <span data-ttu-id="f7939-2777">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="f7939-2777">tx_timer_activate</span></span>
- <span data-ttu-id="f7939-2778">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2778">tx_timer_change</span></span>
- <span data-ttu-id="f7939-2779">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="f7939-2779">tx_timer_deactivate</span></span>
- <span data-ttu-id="f7939-2780">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2780">tx_timer_delete</span></span>
- <span data-ttu-id="f7939-2781">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2781">tx_timer_info_get</span></span>
- <span data-ttu-id="f7939-2782">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2782">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="f7939-2783">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2783">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_deactivate"></a><span data-ttu-id="f7939-2784">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="f7939-2784">tx_timer_deactivate</span></span>

<span data-ttu-id="f7939-2785">Disattiva timer applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2785">Deactivate application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2786">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2786">Prototype</span></span>

```C
UINT tx_timer_deactivate(TX_TIMER *timer_ptr);
```

### <a name="description"></a><span data-ttu-id="f7939-2787">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2787">Description</span></span>

<span data-ttu-id="f7939-2788">Questo servizio disattiva il timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2788">This service deactivates the specified application timer.</span></span> <span data-ttu-id="f7939-2789">Se il timer è già disattivato, questo servizio non ha alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="f7939-2789">If the timer is already deactivated, this service has no effect.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2790">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2790">Parameters</span></span> 

- <span data-ttu-id="f7939-2791">**timer_ptr**: puntatore a un timer dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-2791">**timer_ptr**: Pointer to a previously created application timer.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2792">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2792">Return Values</span></span>

- <span data-ttu-id="f7939-2793">**TX_SUCCESS**: (0x00) la disattivazione del timer applicazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2793">**TX_SUCCESS**: (0x00) Successful application timer deactivation.</span></span>
- <span data-ttu-id="f7939-2794">TX_TIMER_ERROR: (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2794">TX_TIMER_ERROR: (0x15) Invalid application timer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2795">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2795">Allowed From</span></span>

<span data-ttu-id="f7939-2796">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2796">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2797">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2797">Preemption Possible</span></span>

<span data-ttu-id="f7939-2798">No</span><span class="sxs-lookup"><span data-stu-id="f7939-2798">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2799">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2799">Example</span></span>

```C
TX_TIMER     my_timer;
UINT         status;

/* Deactivate an application timer. Assume that the
   application timer has already been created. */
status =  tx_timer_deactivate(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
   now deactivated. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2800">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2800">See Also</span></span>

- <span data-ttu-id="f7939-2801">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="f7939-2801">tx_timer_activate</span></span>
- <span data-ttu-id="f7939-2802">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2802">tx_timer_change</span></span>
- <span data-ttu-id="f7939-2803">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2803">tx_timer_create</span></span>
- <span data-ttu-id="f7939-2804">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2804">tx_timer_delete</span></span>
- <span data-ttu-id="f7939-2805">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2805">tx_timer_info_get</span></span>
- <span data-ttu-id="f7939-2806">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2806">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="f7939-2807">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2807">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_delete"></a><span data-ttu-id="f7939-2808">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2808">tx_timer_delete</span></span>

<span data-ttu-id="f7939-2809">Elimina timer applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2809">Delete application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2810">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2810">Prototype</span></span>

```C
UINT tx_timer_delete(TX_TIMER *timer_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-2811">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2811">Description</span></span>

<span data-ttu-id="f7939-2812">Questo servizio Elimina il timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2812">This service deletes the specified application timer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2813">È responsabilità dell'applicazione impedire l'uso di un timer eliminato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2813">It is the application’s responsibility to prevent use of a deleted timer.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2814">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2814">Parameters</span></span> 

- <span data-ttu-id="f7939-2815">**timer_ptr**: puntatore a un timer dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-2815">**timer_ptr**: Pointer to a previously created application timer.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2816">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2816">Return Values</span></span>

- <span data-ttu-id="f7939-2817">**TX_SUCCESS**: (0x00) l'eliminazione del timer applicazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2817">**TX_SUCCESS**: (0x00) Successful application timer deletion.</span></span>
- <span data-ttu-id="f7939-2818">TX_TIMER_ERROR: (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2818">TX_TIMER_ERROR: (0x15) Invalid application timer pointer.</span></span>
- <span data-ttu-id="f7939-2819">TX_CALLER_ERROR: (0x13) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2819">TX_CALLER_ERROR: (0x13) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2820">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2820">Allowed From</span></span>

<span data-ttu-id="f7939-2821">Thread</span><span class="sxs-lookup"><span data-stu-id="f7939-2821">Threads</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2822">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2822">Preemption Possible</span></span>

<span data-ttu-id="f7939-2823">No</span><span class="sxs-lookup"><span data-stu-id="f7939-2823">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2824">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2824">Example</span></span>

```c
TX_TIMER     my_timer;
UINT         status;

/* Delete application timer. Assume that the application
   timer has already been created. */
status =  tx_timer_delete(&my_timer);

/* If status equals TX_SUCCESS, the application timer is
   deleted. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2825">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2825">See Also</span></span>

- <span data-ttu-id="f7939-2826">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="f7939-2826">tx_timer_activate</span></span>
- <span data-ttu-id="f7939-2827">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2827">tx_timer_change</span></span>
- <span data-ttu-id="f7939-2828">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2828">tx_timer_create</span></span>
- <span data-ttu-id="f7939-2829">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="f7939-2829">tx_timer_deactivate</span></span>
- <span data-ttu-id="f7939-2830">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2830">tx_timer_info_get</span></span>
- <span data-ttu-id="f7939-2831">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2831">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="f7939-2832">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2832">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_info_get"></a><span data-ttu-id="f7939-2833">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2833">tx_timer_info_get</span></span>

<span data-ttu-id="f7939-2834">Recuperare informazioni sul timer di un'applicazione</span><span class="sxs-lookup"><span data-stu-id="f7939-2834">Retrieve information about an application timer</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2835">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2835">Prototype</span></span>

```C
UINT tx_timer_info_get(TX_TIMER *timer_ptr, CHAR **name,
                          UINT *active, ULONG *remaining_ticks,
                          ULONG *reschedule_ticks,
                          TX_TIMER **next_timer)
```
### <a name="description"></a><span data-ttu-id="f7939-2836">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2836">Description</span></span>

<span data-ttu-id="f7939-2837">Questo servizio recupera le informazioni sul timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2837">This service retrieves information about the specified application timer.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2838">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2838">Parameters</span></span>

- <span data-ttu-id="f7939-2839">**timer_ptr**: puntatore a un timer dell'applicazione creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-2839">**timer_ptr**: Pointer to a previously created application timer.</span></span>
- <span data-ttu-id="f7939-2840">**Name**: puntatore alla destinazione per il puntatore al nome del timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2840">**name**: Pointer to destination for the pointer to the timer’s name.</span></span>
- <span data-ttu-id="f7939-2841">**attivo**: puntatore alla destinazione per l'indicazione attiva del timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2841">**active**: Pointer to destination for the timer active indication.</span></span> <span data-ttu-id="f7939-2842">Se il timer è inattivo o questo servizio viene chiamato dal timer stesso, viene restituito un valore TX_FALSE.</span><span class="sxs-lookup"><span data-stu-id="f7939-2842">If the timer is inactive or this service is called from the timer itself, a TX_FALSE value is returned.</span></span> <span data-ttu-id="f7939-2843">In caso contrario, se il timer è attivo, viene restituito un valore TX_TRUE.</span><span class="sxs-lookup"><span data-stu-id="f7939-2843">Otherwise, if the timer is active, a TX_TRUE value is returned.</span></span>
- <span data-ttu-id="f7939-2844">**remaining_ticks**: puntatore alla destinazione per il numero di cicli del timer rimasti prima della scadenza del timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2844">**remaining_ticks**: Pointer to destination for the number of timer ticks left before the timer expires.</span></span>
- <span data-ttu-id="f7939-2845">**reschedule_ticks**: puntatore alla destinazione per il numero di cicli del timer che verranno utilizzati per ripianificare automaticamente il timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2845">**reschedule_ticks**: Pointer to destination for the number of timer ticks that will be used to automatically reschedule this timer.</span></span> <span data-ttu-id="f7939-2846">Se il valore è zero, il timer è una volta e non verrà ripianificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2846">If the value is zero, then the timer is a one-shot and won’t be rescheduled.</span></span>
- <span data-ttu-id="f7939-2847">**next_timer**: puntatore alla destinazione per il puntatore del timer applicazione creato successivo.</span><span class="sxs-lookup"><span data-stu-id="f7939-2847">**next_timer**: Pointer to destination for the pointer of the next created application timer.</span></span>

> [!NOTE]
> <span data-ttu-id="f7939-2848">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-2848">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2849">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2849">Return Values</span></span>

- <span data-ttu-id="f7939-2850">**TX_SUCCESS**: (0x00) il recupero delle informazioni sul timer è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-2850">**TX_SUCCESS**: (0x00) Successful timer information retrieval.</span></span>
- <span data-ttu-id="f7939-2851">TX_TIMER_ERROR: (0x15) puntatore del timer applicazione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2851">TX_TIMER_ERROR: (0x15) Invalid application timer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2852">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2852">Allowed From</span></span>

<span data-ttu-id="f7939-2853">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2853">Initialization, threads, timers, and ISRs</span></span>

### <a name="preemption-possible"></a><span data-ttu-id="f7939-2854">Precedenza possibile</span><span class="sxs-lookup"><span data-stu-id="f7939-2854">Preemption Possible</span></span>

<span data-ttu-id="f7939-2855">No</span><span class="sxs-lookup"><span data-stu-id="f7939-2855">No</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2856">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2856">Example</span></span>

```C
TX_TIMER     my_timer;
CHAR         *name;
UINT         active;
ULONG        remaining_ticks;
ULONG        reschedule_ticks;
TX_TIMER     *next_timer;
UINT         status;

/* Retrieve information about the previously created
   application timer "my_timer." */
status =  tx_timer_info_get(&my_timer, &name,
                          &active,&remaining_ticks,
                &reschedule_ticks,
                         &next_timer);

/* If status equals TX_SUCCESS, the information requested is
   valid. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2857">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2857">See Also</span></span>

- <span data-ttu-id="f7939-2858">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="f7939-2858">tx_timer_activate</span></span>
- <span data-ttu-id="f7939-2859">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2859">tx_timer_change</span></span>
- <span data-ttu-id="f7939-2860">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2860">tx_timer_create</span></span>
- <span data-ttu-id="f7939-2861">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="f7939-2861">tx_timer_deactivate</span></span>
- <span data-ttu-id="f7939-2862">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2862">tx_timer_delete</span></span>
- <span data-ttu-id="f7939-2863">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2863">tx_timer_info_get</span></span>
- <span data-ttu-id="f7939-2864">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2864">tx_timer_performance_info_get</span></span>
- <span data-ttu-id="f7939-2865">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2865">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_performance_info_get"></a><span data-ttu-id="f7939-2866">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2866">tx_timer_performance_info_get</span></span> 

<span data-ttu-id="f7939-2867">Ottenere le informazioni sulle prestazioni del timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2867">Get timer performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2868">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2868">Prototype</span></span>

```C
UINT  tx_timer_performance_info_get(TX_TIMER *timer_ptr,
        ULONG *activates, ULONG *reactivates,
        ULONG *deactivates, ULONG *expirations,
        ULONG *expiration_adjusts);
```
### <a name="description"></a><span data-ttu-id="f7939-2869">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2869">Description</span></span>

<span data-ttu-id="f7939-2870">Questo servizio recupera le informazioni sulle prestazioni relative al timer dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2870">This service retrieves performance information about the specified application timer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2871">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_TIMER_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-2871">The ThreadX SMP library and application must be built with **TX_TIMER_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2872">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2872">Parameters</span></span> 

- <span data-ttu-id="f7939-2873">**timer_ptr**: puntatore al timer creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7939-2873">**timer_ptr**: Pointer to previously created timer.</span></span>
- <span data-ttu-id="f7939-2874">**attiva**: puntatore alla destinazione per il numero di richieste di attivazione eseguite su questo timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2874">**activates**: Pointer to destination for the number of activation requests performed on this timer.</span></span>
- <span data-ttu-id="f7939-2875">**riattiva**: puntatore alla destinazione per il numero di riattivazioni automatiche eseguite su questo timer periodico.</span><span class="sxs-lookup"><span data-stu-id="f7939-2875">**reactivates**: Pointer to destination for the number of automatic reactivations performed on this periodic timer.</span></span>
- <span data-ttu-id="f7939-2876">**Disattiva**: puntatore alla destinazione per il numero di richieste di disattivazione eseguite su questo timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2876">**deactivates**: Pointer to destination for the number of deactivation requests performed on this timer.</span></span>
- <span data-ttu-id="f7939-2877">**scadenze**: puntatore alla destinazione per il numero di scadenze del timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2877">**expirations**: Pointer to destination for the number of expirations of this timer.</span></span>
- <span data-ttu-id="f7939-2878">**expiration_adjusts**: puntatore alla destinazione per il numero di rettifiche di scadenza interne eseguite su questo timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2878">**expiration_adjusts**: Pointer to destination for the number of internal expiration adjustments performed on this timer.</span></span> <span data-ttu-id="f7939-2879">Queste rettifiche vengono eseguite nell'elaborazione dell'interrupt del timer per i timer di dimensioni maggiori rispetto alle dimensioni predefinite dell'elenco di timer (per impostazione predefinita, i timer con scadenze maggiori di 32 cicli).</span><span class="sxs-lookup"><span data-stu-id="f7939-2879">These adjustments are done in the timer interrupt processing for timers that are larger than the default timer list size (by default timers with expirations greater than 32 ticks).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2880">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-2880">Supplying a TX_NULL for any parameter indicates the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2881">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2881">Return Values</span></span>

- <span data-ttu-id="f7939-2882">**TX_SUCCESS**: (0x00) operazione timer riuscita Get.</span><span class="sxs-lookup"><span data-stu-id="f7939-2882">**TX_SUCCESS**: (0x00) Successful timer performance get.</span></span>
- <span data-ttu-id="f7939-2883">**TX_PTR_ERROR**: (0x03) puntatore del timer non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2883">**TX_PTR_ERROR**: (0x03) Invalid timer pointer.</span></span>
- <span data-ttu-id="f7939-2884">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-2884">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2885">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2885">Allowed From</span></span>

<span data-ttu-id="f7939-2886">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2886">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2887">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2887">Example</span></span>

```C
TX_TIMER     my_timer;
ULONG        activates;
ULONG        reactivates;
ULONG        deactivates;
ULONG        expirations;
ULONG        expiration_adjusts;

/* Retrieve performance information on the previously created
   timer.  */
status =  tx_timer_performance_info_get(&my_timer, &activates,
                &reactivates,&deactivates, &expirations,
                &expiration_adjusts);

/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2888">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2888">See Also</span></span>

- <span data-ttu-id="f7939-2889">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="f7939-2889">tx_timer_activate</span></span>
- <span data-ttu-id="f7939-2890">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2890">tx_timer_change</span></span>
- <span data-ttu-id="f7939-2891">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2891">tx_timer_create</span></span>
- <span data-ttu-id="f7939-2892">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="f7939-2892">tx_timer_deactivate</span></span>
- <span data-ttu-id="f7939-2893">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2893">tx_timer_delete</span></span>
- <span data-ttu-id="f7939-2894">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2894">tx_timer_info_get</span></span>
- <span data-ttu-id="f7939-2895">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2895">tx_timer_performance_system_info_get</span></span>

## <a name="tx_timer_performance_system_info_get"></a><span data-ttu-id="f7939-2896">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2896">tx_timer_performance_system_info_get</span></span> 

<span data-ttu-id="f7939-2897">Ottenere informazioni sulle prestazioni del sistema timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2897">Get timer system performance information</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2898">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2898">Prototype</span></span>

```C
UINT  tx_timer_performance_system_info_get(ULONG *activates,
        ULONG *reactivates, ULONG *deactivates,
        ULONG *expirations, ULONG *expiration_adjusts);
```
### <a name="description"></a><span data-ttu-id="f7939-2899">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2899">Description</span></span>

<span data-ttu-id="f7939-2900">Questo servizio recupera le informazioni sulle prestazioni relative a tutti i timer dell'applicazione nel sistema.</span><span class="sxs-lookup"><span data-stu-id="f7939-2900">This service retrieves performance information about all the application timers in the system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2901">Per restituire informazioni sulle prestazioni, è necessario compilare la libreria SMP di ThreadX e l'applicazione con **TX_TIMER_ENABLE_PERFORMANCE_INFO** definite per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="f7939-2901">The ThreadX SMP library and application must be built with **TX_TIMER_ENABLE_PERFORMANCE_INFO** defined for this service to return performance information.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2902">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2902">Parameters</span></span>

- <span data-ttu-id="f7939-2903">**attiva**: puntatore alla destinazione per il numero totale di richieste di attivazione eseguite su tutti i timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2903">**activates**: Pointer to destination for the total number of activation requests performed on all timers.</span></span>
- <span data-ttu-id="f7939-2904">**riattiva**: puntatore alla destinazione per il numero totale di riattivazioni automatiche eseguite su tutti i timer periodici.</span><span class="sxs-lookup"><span data-stu-id="f7939-2904">**reactivates**: Pointer to destination for the total number of automatic reactivation performed on all periodic timers.</span></span>
- <span data-ttu-id="f7939-2905">**Disattiva**: puntatore alla destinazione per il numero totale di richieste di disattivazione eseguite su tutti i timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2905">**deactivates**: Pointer to destination for the total number of deactivation requests performed on all timers.</span></span>
- <span data-ttu-id="f7939-2906">**scadenze**: puntatore alla destinazione per il numero totale di scadenze in tutti i timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2906">**expirations**: Pointer to destination for the total number of expirations on all timers.</span></span>
- <span data-ttu-id="f7939-2907">**expiration_adjusts**: puntatore alla destinazione per il numero totale di rettifiche di scadenza interne eseguite su tutti i timer.</span><span class="sxs-lookup"><span data-stu-id="f7939-2907">**expiration_adjusts**: Pointer to destination for the total number of internal expiration adjustments performed on all timers.</span></span> <span data-ttu-id="f7939-2908">Queste rettifiche vengono eseguite nell'elaborazione dell'interrupt del timer per i timer di dimensioni maggiori rispetto alle dimensioni predefinite dell'elenco di timer (per impostazione predefinita, i timer con scadenze maggiori di 32 cicli).</span><span class="sxs-lookup"><span data-stu-id="f7939-2908">These adjustments are done in the timer interrupt processing for timers that are larger than the default timer list size (by default timers with expirations greater than 32 ticks).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2909">La specifica di un TX_NULL per qualsiasi parametro indica che il parametro non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f7939-2909">Supplying a TX_NULL for any parameter indicates that the parameter is not required.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2910">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2910">Return Values</span></span>

- <span data-ttu-id="f7939-2911">**TX_SUCCESS**: (0x00) la riuscita delle prestazioni del sistema timer è Get.</span><span class="sxs-lookup"><span data-stu-id="f7939-2911">**TX_SUCCESS**: (0x00) Successful timer system performance get.</span></span>
- <span data-ttu-id="f7939-2912">**TX_FEATURE_NOT_ENABLED**: (0Xff) il sistema non è stato compilato con le informazioni sulle prestazioni abilitate.</span><span class="sxs-lookup"><span data-stu-id="f7939-2912">**TX_FEATURE_NOT_ENABLED**: (0xFF) The system was not compiled with performance information enabled.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2913">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2913">Allowed From</span></span>

<span data-ttu-id="f7939-2914">Inizializzazione, thread, timer e ISRs</span><span class="sxs-lookup"><span data-stu-id="f7939-2914">Initialization, threads, timers, and ISRs</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2915">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2915">Example</span></span>

```C
ULONG     activates;
ULONG     reactivates;
ULONG     deactivates;
ULONG     expirations;
ULONG     expiration_adjusts;

/* Retrieve performance information on all previously created
   timers.  */
status =  tx_timer_performance_system_info_get(&activates,
                &reactivates, &deactivates, &expirations,
                &expiration_adjusts);
/* If status is TX_SUCCESS the performance information was
   successfully retrieved. */
```
### <a name="see-also"></a><span data-ttu-id="f7939-2916">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2916">See Also</span></span>

- <span data-ttu-id="f7939-2917">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="f7939-2917">tx_timer_activate</span></span>
- <span data-ttu-id="f7939-2918">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="f7939-2918">tx_timer_change</span></span>
- <span data-ttu-id="f7939-2919">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="f7939-2919">tx_timer_create</span></span>
- <span data-ttu-id="f7939-2920">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="f7939-2920">tx_timer_deactivate</span></span>
- <span data-ttu-id="f7939-2921">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="f7939-2921">tx_timer_delete</span></span>
- <span data-ttu-id="f7939-2922">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2922">tx_timer_info_get</span></span>
- <span data-ttu-id="f7939-2923">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2923">tx_timer_performance_info_get</span></span>

## <a name="tx_timer_smp_core_exclude"></a><span data-ttu-id="f7939-2924">tx_timer_smp_core_exclude</span><span class="sxs-lookup"><span data-stu-id="f7939-2924">tx_timer_smp_core_exclude</span></span>

<span data-ttu-id="f7939-2925">Escludere l'esecuzione del timer in un set di core</span><span class="sxs-lookup"><span data-stu-id="f7939-2925">Exclude timer execution on a set of cores</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2926">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2926">Prototype</span></span>

```C
UINT  tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);
```
### <a name="description"></a><span data-ttu-id="f7939-2927">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2927">Description</span></span>

<span data-ttu-id="f7939-2928">Questa funzione esclude il timer specificato dall'esecuzione nei core specificati nella mappa di bit denominata "*exclusion_map*".</span><span class="sxs-lookup"><span data-stu-id="f7939-2928">This function excludes the specified timer from executing on the core(s) specified in the bit map called "*exclusion_map*."</span></span> <span data-ttu-id="f7939-2929">Ogni bit in "*exclusion_map*" rappresenta un core (bit 0 rappresenta il nucleo 0 e così via).</span><span class="sxs-lookup"><span data-stu-id="f7939-2929">Each bit in "*exclusion_map*" represents a core (bit 0 represents core 0, etc.).</span></span> <span data-ttu-id="f7939-2930">Se il bit è impostato, il nucleo corrispondente viene escluso dall'esecuzione del timer specificato.</span><span class="sxs-lookup"><span data-stu-id="f7939-2930">If the bit is set, the corresponding core is excluded from executing the specified timer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7939-2931">L'uso dell'esclusione del processore può causare un'ulteriore elaborazione nel thread alla logica di mapping di base per trovare la corrispondenza ottimale.</span><span class="sxs-lookup"><span data-stu-id="f7939-2931">Use of processor exclusion may cause additional processing in the thread to core mapping logic in order to find the optimal match.</span></span> <span data-ttu-id="f7939-2932">Questa elaborazione è limitata dal numero di thread pronti.</span><span class="sxs-lookup"><span data-stu-id="f7939-2932">This processing is bounded by the number of ready threads.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2933">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2933">Parameters</span></span>

- <span data-ttu-id="f7939-2934">**timer_ptr**: puntatore al timer per modificare l'esclusione di base.</span><span class="sxs-lookup"><span data-stu-id="f7939-2934">**timer_ptr**: Pointer to timer to change the core exclusion.</span></span>
- <span data-ttu-id="f7939-2935">**exclusion_map**: mappa di bit in cui un bit sit indica che tale Core è escluso.</span><span class="sxs-lookup"><span data-stu-id="f7939-2935">**exclusion_map**: Bit map where a sit bit indicates that that core is excluded.</span></span> <span data-ttu-id="f7939-2936">Se si specifica un valore 0, il timer verrà eseguito su qualsiasi core (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="f7939-2936">Supplying a 0 value enables the timer to execute on any core (default).</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2937">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2937">Return Values</span></span>

- <span data-ttu-id="f7939-2938">Esclusione di base **TX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="f7939-2938">**TX_SUCCESS** (0x00) Successful core exclusion.</span></span>
- <span data-ttu-id="f7939-2939">**TX_TIMER_ERROR** (0x0E) puntatore del timer non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2939">**TX_TIMER_ERROR** (0x0E) Invalid timer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2940">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2940">Allowed From</span></span>

<span data-ttu-id="f7939-2941">Inizializzazione, ISRs, thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2941">Initialization, ISRs, threads, and timers</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2942">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2942">Example</span></span>

```C
/* Exclude core 0 for "Timer 0". */
tx_timer_smp_core_exclude(&timer_0, 0x01);
```

### <a name="see-also"></a><span data-ttu-id="f7939-2943">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2943">See Also</span></span>

- <span data-ttu-id="f7939-2944">tx_timer_smp_core_exclude_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2944">tx_timer_smp_core_exclude_get</span></span>

## <a name="tx_timer_smp_core_exclude_get"></a><span data-ttu-id="f7939-2945">tx_timer_smp_core_exclude_get</span><span class="sxs-lookup"><span data-stu-id="f7939-2945">tx_timer_smp_core_exclude_get</span></span>

<span data-ttu-id="f7939-2946">Ottiene l'esclusione di base corrente del timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2946">Gets the timer's current core exclusion</span></span>

### <a name="prototype"></a><span data-ttu-id="f7939-2947">Prototipo</span><span class="sxs-lookup"><span data-stu-id="f7939-2947">Prototype</span></span>

```C
UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr,
                         ULONG *exclusion_map_ptr);
```
### <a name="description"></a><span data-ttu-id="f7939-2948">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7939-2948">Description</span></span>

<span data-ttu-id="f7939-2949">Questa funzione restituisce l'elenco di esclusione principale corrente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2949">This function returns the current core exclusion list.</span></span>

### <a name="parameters"></a><span data-ttu-id="f7939-2950">Parametri</span><span class="sxs-lookup"><span data-stu-id="f7939-2950">Parameters</span></span>

- <span data-ttu-id="f7939-2951">**timer_ptr**: puntatore al timer da cui recuperare l'esclusione di base.</span><span class="sxs-lookup"><span data-stu-id="f7939-2951">**timer_ptr**: Pointer to timer from which to retrieve the core exclusion.</span></span>
- <span data-ttu-id="f7939-2952">**exclusion_map_ptr**: destinazione per la mappa di bit di esclusione principale corrente.</span><span class="sxs-lookup"><span data-stu-id="f7939-2952">**exclusion_map_ptr**: Destination for current core exclusion bit map.</span></span>

### <a name="return-values"></a><span data-ttu-id="f7939-2953">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="f7939-2953">Return Values</span></span>

- <span data-ttu-id="f7939-2954">TX_SUCCESS: (0x00) il recupero dell'esclusione di base del timer è riuscito.</span><span class="sxs-lookup"><span data-stu-id="f7939-2954">TX_SUCCESS: (0x00) Successful retrieval of timer's core exclusion.</span></span>
- <span data-ttu-id="f7939-2955">TX_TIMER_ERROR: (0x0E) puntatore del timer non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2955">TX_TIMER_ERROR: (0x0E) Invalid timer pointer.</span></span>
- <span data-ttu-id="f7939-2956">TX_PTR_ERROR: (0x03) puntatore di destinazione di esclusione non valido.</span><span class="sxs-lookup"><span data-stu-id="f7939-2956">TX_PTR_ERROR: (0x03) Invalid exclusion destination pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="f7939-2957">Consentito da</span><span class="sxs-lookup"><span data-stu-id="f7939-2957">Allowed From</span></span>

<span data-ttu-id="f7939-2958">Inizializzazione, ISRs, thread e timer</span><span class="sxs-lookup"><span data-stu-id="f7939-2958">Initialization, ISRs, threads, and timers</span></span>

### <a name="example"></a><span data-ttu-id="f7939-2959">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7939-2959">Example</span></span>

```C
ULONGexcluded_cores;

/* Retrieve the core exclusion for "Timer 0". */
tx_timer_smp_core_exclude_get(&timer_0,&excluded_cores);
```
### <a name="see-also"></a><span data-ttu-id="f7939-2960">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f7939-2960">See Also</span></span>

- <span data-ttu-id="f7939-2961">tx_timer_smp_core_exclude</span><span class="sxs-lookup"><span data-stu-id="f7939-2961">tx_timer_smp_core_exclude</span></span>