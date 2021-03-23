---
title: 'Capitolo 6: eventi di traccia di Azure RTO ThreadX'
description: Questo capitolo descrive gli eventi ThreadX di Azure RTO.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 8f0ff03d112597371059d925f64b7511454e123c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823459"
---
# <a name="chapter-6---azure-rtos-threadx-trace-events"></a><span data-ttu-id="bd849-103">Capitolo 6: eventi di traccia di Azure RTO ThreadX</span><span class="sxs-lookup"><span data-stu-id="bd849-103">Chapter 6 - Azure RTOS ThreadX trace events</span></span>

<span data-ttu-id="bd849-104">Questo capitolo descrive gli eventi ThreadX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="bd849-104">This chapter describes the Azure RTOS ThreadX events.</span></span> 

## <a name="list-of-events-and-icons"></a><span data-ttu-id="bd849-105">Elenco di eventi e icone</span><span class="sxs-lookup"><span data-stu-id="bd849-105">List of Events and Icons</span></span>

<span data-ttu-id="bd849-106">Di seguito è riportato un elenco di eventi ThreadX visualizzati da TraceX:</span><span class="sxs-lookup"><span data-stu-id="bd849-106">The following is a list of ThreadX events displayed by TraceX:</span></span>

| <span data-ttu-id="bd849-107">**Icona**</span><span class="sxs-lookup"><span data-stu-id="bd849-107">**Icon**</span></span>                         | <span data-ttu-id="bd849-108">**Significato**</span><span class="sxs-lookup"><span data-stu-id="bd849-108">**Meaning**</span></span> |
| -------------------------------- | ------------------------------------- |
| ![Icona Riprendi thread interno](./media/user-guide/tx-events/image1.png)    | <span data-ttu-id="bd849-110">Ripresa thread interno</span><span class="sxs-lookup"><span data-stu-id="bd849-110">Internal thread resume</span></span>  |
| ![Icona di sospensione thread interno](./media/user-guide/tx-events/image2.png)    | <span data-ttu-id="bd849-112">Sospensione thread interno</span><span class="sxs-lookup"><span data-stu-id="bd849-112">Internal thread suspend</span></span> |
| ![Icona di immissione della routine del servizio di interrupt](./media/user-guide/tx-events/image3.png)    | <span data-ttu-id="bd849-114">Routine del servizio di interrupt (ISR) invio</span><span class="sxs-lookup"><span data-stu-id="bd849-114">Interrupt Service Routine (ISR) Enter</span></span> |
| ![Icona di uscita della routine del servizio di interrupt](./media/user-guide/tx-events/image4.png)    | <span data-ttu-id="bd849-116">Uscita routine servizio di interrupt (ISR)</span><span class="sxs-lookup"><span data-stu-id="bd849-116">Interrupt Service Routine (ISR) Exit</span></span>  |
| ![Icona dell'intervallo di tempo interno](./media/user-guide/tx-events/image5.png)    | <span data-ttu-id="bd849-118">Sezione tempo interna</span><span class="sxs-lookup"><span data-stu-id="bd849-118">Internal time-slice</span></span> |
| ![Icona in esecuzione](./media/user-guide/tx-events/image6.png)    | <span data-ttu-id="bd849-120">In esecuzione</span><span class="sxs-lookup"><span data-stu-id="bd849-120">Running</span></span> |
| ![Icona di allocazione del pool di blocchi](./media/user-guide/tx-events/image7.png)    | <span data-ttu-id="bd849-122">**Alloca pool di blocchi** (*tx_block_allocate*)</span><span class="sxs-lookup"><span data-stu-id="bd849-122">**Block pool allocate** (*tx_block_allocate*)</span></span>  |
| ![Icona di creazione del pool di blocchi](./media/user-guide/tx-events/image8.png)    | <span data-ttu-id="bd849-124">**Creazione del pool di blocchi** (*tx_block_pool_create*)</span><span class="sxs-lookup"><span data-stu-id="bd849-124">**Block pool create** (*tx_block_pool_create*)</span></span> |
| ![Icona di eliminazione del pool di blocchi](./media/user-guide/tx-events/image9.png)    | <span data-ttu-id="bd849-126">**Eliminazione del pool di blocchi** (*tx_block_pool_delete*)</span><span class="sxs-lookup"><span data-stu-id="bd849-126">**Block pool delete** (*tx_block_pool_delete*)</span></span> |
| ![Icona Ottieni informazioni sul pool di blocchi](./media/user-guide/tx-events/image10.png)    | <span data-ttu-id="bd849-128">**Ottieni informazioni sul pool di blocchi** (*tx_block_pool_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-128">**Block pool information get** (*tx_block_pool_info_get*)</span></span> |
| ![Informazioni sulle prestazioni del pool di blocco con](./media/user-guide/tx-events/image11.png)    | <span data-ttu-id="bd849-130">**Informazioni sulle prestazioni del pool di blocco Get** (*tx_block_pool_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-130">**Block pool performance information get** (*tx_block_pool_performance_info_get*)</span></span> |
| ![Icona Ottieni informazioni sulle prestazioni del sistema del pool di blocchi](./media/user-guide/tx-events/image12.png)    | <span data-ttu-id="bd849-132">**Informazioni sulle prestazioni del sistema del pool di blocco Get** (*tx_block_pool_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-132">**Block pool system performance information get** (*tx_block_pool_performance_system_info_get*)</span></span> |
| ![Icona di priorità del pool di blocchi](./media/user-guide/tx-events/image13.png)    | <span data-ttu-id="bd849-134">**Priorità del pool di blocchi** (*tx_block_pool_prioritize*)</span><span class="sxs-lookup"><span data-stu-id="bd849-134">**Block pool prioritize** (*tx_block_pool_prioritize*)</span></span> |
| ![Icona Blocca versione in pool](./media/user-guide/tx-events/image14.png)    | <span data-ttu-id="bd849-136">**Blocca la versione al pool** (*tx_block_release*)</span><span class="sxs-lookup"><span data-stu-id="bd849-136">**Block release to pool** (*tx_block_release*)</span></span> |
| ![Icona alloca memoria pool di byte](./media/user-guide/tx-events/image15.png)    | <span data-ttu-id="bd849-138">**Memoria allocata pool di byte** (*tx_byte_allocate*)</span><span class="sxs-lookup"><span data-stu-id="bd849-138">**Byte pool allocate memory** (*tx_byte_allocate*)</span></span> |
| ![Icona di creazione pool di byte](./media/user-guide/tx-events/image16.png)    | <span data-ttu-id="bd849-140">**Creazione pool di byte** (*tx_byte_pool_create*)</span><span class="sxs-lookup"><span data-stu-id="bd849-140">**Byte pool create** (*tx_byte_pool_create*)</span></span> |
| ![Icona di eliminazione del pool di byte](./media/user-guide/tx-events/image17.png)    | <span data-ttu-id="bd849-142">**Eliminazione pool di byte** (*tx_byte_pool_delete*)</span><span class="sxs-lookup"><span data-stu-id="bd849-142">**Byte pool delete** (*tx_byte_pool_delete*)</span></span> |
| ![Icona ottenere informazioni sul pool di byte](./media/user-guide/tx-events/image18.png)    | <span data-ttu-id="bd849-144">**Informazioni sul pool di byte get** (*tx_byte_pool_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-144">**Byte pool information get** (*tx_byte_pool_info_get*)</span></span> |
| ![Icona ottenere informazioni sulle prestazioni del pool di byte](./media/user-guide/tx-events/image19.png)    | <span data-ttu-id="bd849-146">**Informazioni sulle prestazioni del pool di byte get** (*tx_byte_pool_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-146">**Byte pool performance information get** (*tx_byte_pool_performance_info_get*)</span></span> |
| ![Icona ottenere informazioni sulle prestazioni del sistema del pool di byte](./media/user-guide/tx-events/image20.png)    | <span data-ttu-id="bd849-148">**Informazioni sulle prestazioni del sistema del pool di byte get** (*tx_byte_pool_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-148">**Byte pool system performance information get** (*tx_byte_pool_performance_system_info_get*)</span></span> |
| ![\* Icona priorità pool di byte](./media/user-guide/tx-events/image21.png)    | <span data-ttu-id="bd849-150">**Priorità del pool di byte** (*tx_byte_pool_prioritize*)</span><span class="sxs-lookup"><span data-stu-id="bd849-150">**Byte pool prioritize** (*tx_byte_pool_prioritize*)</span></span> |
| ![Icona versione memoria byte in pool](./media/user-guide/tx-events/image22.png)    | <span data-ttu-id="bd849-152">**Rilascio memoria byte nel pool** (*tx_byte_release*)</span><span class="sxs-lookup"><span data-stu-id="bd849-152">**Byte memory release to pool** (*tx_byte_release*)</span></span> |
| ![Icona di creazione flag evento](./media/user-guide/tx-events/image23.png)    | <span data-ttu-id="bd849-154">**Creazione flag evento** (*tx_event_flags_create*)</span><span class="sxs-lookup"><span data-stu-id="bd849-154">**Event flags create** (*tx_event_flags_create*)</span></span> |
| ![Icona di eliminazione flag evento](./media/user-guide/tx-events/image24.png)    | <span data-ttu-id="bd849-156">**Flag evento Delete** (*tx_event_flags_delete*)</span><span class="sxs-lookup"><span data-stu-id="bd849-156">**Event flags delete** (*tx_event_flags_delete*)</span></span> |
| ![Icona di Get flag evento](./media/user-guide/tx-events/image25.png)    | <span data-ttu-id="bd849-158">**Flag evento Get** (*tx_event_flags_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-158">**Event flags get** (*tx_event_flags_get*)</span></span> |
| ![Icona ottenere informazioni sui flag di evento](./media/user-guide/tx-events/image26.png)    | <span data-ttu-id="bd849-160">**Informazioni sui flag evento Get** (*tx_event_flags_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-160">**Event flags information get** (*tx_event_flags_info_get*)</span></span> |
| ![Icona delle informazioni sulle prestazioni di flag di evento](./media/user-guide/tx-events/image27.png)    | <span data-ttu-id="bd849-162">**Informazioni sulle prestazioni di flag evento Get** (*tx_event_flags_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-162">**Event flags performance information get** (*tx_event_flags_performance_info_get*)</span></span> |
| ![Icona delle informazioni sulle prestazioni del sistema flag di evento](./media/user-guide/tx-events/image28.png)    | <span data-ttu-id="bd849-164">**Flag di evento informazioni sulle prestazioni del sistema Get** (*tx_event_flags_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-164">**Event flags system performance information get** (*tx_event_flags_performance_system_info_get*)</span></span> |
| ![Icona set di flag evento](./media/user-guide/tx-events/image29.png)    | <span data-ttu-id="bd849-166">**Flag evento impostati** (*tx_event_flags_set*)</span><span class="sxs-lookup"><span data-stu-id="bd849-166">**Event flags set** (*tx_event_flags_set*)</span></span> |
| ![Icona di impostazione notifica flag evento](./media/user-guide/tx-events/image30.png)    | <span data-ttu-id="bd849-168">**Flag evento set Notify** (*tx_event_flags_set_notify*)</span><span class="sxs-lookup"><span data-stu-id="bd849-168">**Event flags set notify** (*tx_event_flags_set_notify*)</span></span> |
| ![Icona Abilita/Disabilita interrupt](./media/user-guide/tx-events/image31.png)    | <span data-ttu-id="bd849-170">**Abilita/Disabilita interrupt** (*tx_interrupt_control*)</span><span class="sxs-lookup"><span data-stu-id="bd849-170">**Interrupt enable/disable** (*tx_interrupt_control*)</span></span> |
| ![Icona di creazione mutex](./media/user-guide/tx-events/image32.png)    | <span data-ttu-id="bd849-172">**Creazione mutex** (*tx_mutex_create*)</span><span class="sxs-lookup"><span data-stu-id="bd849-172">**Mutex create** (*tx_mutex_create*)</span></span> |
| ![Icona di eliminazione mutex](./media/user-guide/tx-events/image33.png)    | <span data-ttu-id="bd849-174">**Eliminazione mutex** (*tx_mutex_delete*)</span><span class="sxs-lookup"><span data-stu-id="bd849-174">**Mutex delete** (*tx_mutex_delete*)</span></span> |
| ![Icona di Get mutex](./media/user-guide/tx-events/image34.png)    | <span data-ttu-id="bd849-176">**Mutex Get** (*tx_mutex_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-176">**Mutex get** (*tx_mutex_get*)</span></span> |
| ![Icona Ottieni informazioni mutex](./media/user-guide/tx-events/image35.png)    | <span data-ttu-id="bd849-178">**Informazioni sul mutex Get** (*tx_mutex_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-178">**Mutex information get** (*tx_mutex_info_get*)</span></span> |
| ![Icona ottenere informazioni sulle prestazioni mutex](./media/user-guide/tx-events/image36.png)    | <span data-ttu-id="bd849-180">**Informazioni sulle prestazioni di mutex Get** (*tx_mutex_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-180">**Mutex performance information get** (*tx_mutex_performance_info_get*)</span></span> |
| ![Icona ottenere informazioni sulle prestazioni del sistema mutex](./media/user-guide/tx-events/image37.png)    | <span data-ttu-id="bd849-182">**Informazioni sulle prestazioni del sistema mutex Get** (*tx_mutex_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-182">**Mutex system performance information get** (*tx_mutex_performance_system_info_get*)</span></span> |
| ![Icona di priorità mutex](./media/user-guide/tx-events/image38.png)    | <span data-ttu-id="bd849-184">**Priorità mutex** (*tx_mutex_prioritize*)</span><span class="sxs-lookup"><span data-stu-id="bd849-184">**Mutex prioritize** (*tx_mutex_prioritize*)</span></span> |
| ![Icona put mutex](./media/user-guide/tx-events/image39.png)    | <span data-ttu-id="bd849-186">**Mutex put** (*tx_mutex_put*)</span><span class="sxs-lookup"><span data-stu-id="bd849-186">**Mutex put** (*tx_mutex_put*)</span></span> |
| ![Icona Crea coda](./media/user-guide/tx-events/image40.png)    | <span data-ttu-id="bd849-188">**Creazione coda** (*tx_queue_create*)</span><span class="sxs-lookup"><span data-stu-id="bd849-188">**Queue create** (*tx_queue_create*)</span></span> |
| ![Icona di eliminazione della coda](./media/user-guide/tx-events/image41.png)    | <span data-ttu-id="bd849-190">**Elimina coda** (*tx_queue_delete*)</span><span class="sxs-lookup"><span data-stu-id="bd849-190">**Queue delete** (*tx_queue_delete*)</span></span> |
| ![Icona di svuotamento della coda](./media/user-guide/tx-events/image42.png)    | <span data-ttu-id="bd849-192">**Svuotamento coda** (*tx_queue_flush*)</span><span class="sxs-lookup"><span data-stu-id="bd849-192">**Queue flush** (*tx_queue_flush*)</span></span> |
| ![Icona Invia coda in primo piano](./media/user-guide/tx-events/image43.png)    | <span data-ttu-id="bd849-194">**Invio front** -end coda (*tx_queue_front_send*)</span><span class="sxs-lookup"><span data-stu-id="bd849-194">**Queue front send** (*tx_queue_front_send*)</span></span> |
| ![Icona Ottieni informazioni sulla coda](./media/user-guide/tx-events/image44.png)    | <span data-ttu-id="bd849-196">**Informazioni coda Get** (*tx_queue_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-196">**Queue information get** (*tx_queue_info_get*)</span></span> |
| ![Icona ottenere informazioni sulle prestazioni della coda](./media/user-guide/tx-events/image45.png)    | <span data-ttu-id="bd849-198">**Informazioni sulle prestazioni della coda Get** (*tx_queue_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-198">**Queue performance information get** (*tx_queue_performance_info_get*)</span></span> |
| ![Icona ottenere informazioni sulle prestazioni del sistema di Accodamento](./media/user-guide/tx-events/image46.png)    | <span data-ttu-id="bd849-200">**Informazioni sulle prestazioni del sistema di Accodamento Get** (*tx_queue_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-200">**Queue system performance information get** (*tx_queue_performance_system_info_get*)</span></span> |
| ![Icona Accodamento priorità](./media/user-guide/tx-events/image47.png)    | <span data-ttu-id="bd849-202">**Priorità coda** (*tx_queue_prioritize*)</span><span class="sxs-lookup"><span data-stu-id="bd849-202">**Queue prioritize** (*tx_queue_prioritize*)</span></span> |
| ![Icona del messaggio di ricezione della coda](./media/user-guide/tx-events/image48.png)    | <span data-ttu-id="bd849-204">**Messaggio di ricezione coda** (*tx_queue_receive*)</span><span class="sxs-lookup"><span data-stu-id="bd849-204">**Queue receive message** (*tx_queue_receive*)</span></span> |
| ![Icona Invia messaggio coda](./media/user-guide/tx-events/image49.png)    | <span data-ttu-id="bd849-206">**Messaggio di invio coda** (*tx_queue_send*)</span><span class="sxs-lookup"><span data-stu-id="bd849-206">**Queue send message** (*tx_queue_send*)</span></span> |
| ![Icona Invia notifica coda](./media/user-guide/tx-events/image50.png)    | <span data-ttu-id="bd849-208">**Notifica invio coda** (*tx_queue_send_notify*)</span><span class="sxs-lookup"><span data-stu-id="bd849-208">**Queue send notify** (*tx_queue_send_notify*)</span></span> |
| ![Icona put soffitto semaforo](./media/user-guide/tx-events/image51.png)    | <span data-ttu-id="bd849-210">**Soffitto semaforo put** (*tx_semaphore_ceiling_put*)</span><span class="sxs-lookup"><span data-stu-id="bd849-210">**Semaphore ceiling put** (*tx_semaphore_ceiling_put*)</span></span> |
| ![Icona Crea semaforo](./media/user-guide/tx-events/image52.png)    | <span data-ttu-id="bd849-212">**Creazione semaforo** (*tx_semaphore_create*)</span><span class="sxs-lookup"><span data-stu-id="bd849-212">**Semaphore create** (*tx_semaphore_create*)</span></span> |
| ![Icona Elimina semaforo](./media/user-guide/tx-events/image53.png)    | <span data-ttu-id="bd849-214">**Eliminazione semaforo** (*tx_semaphore_delete*)</span><span class="sxs-lookup"><span data-stu-id="bd849-214">**Semaphore delete** (*tx_semaphore_delete*)</span></span> |
| ![Icona Get semaforo](./media/user-guide/tx-events/image54.png)    | <span data-ttu-id="bd849-216">**Semaforo Get** (*tx_semaphore_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-216">**Semaphore get** (*tx_semaphore_get*)</span></span> |
| ![Icona ottenere informazioni sul semaforo](./media/user-guide/tx-events/image55.png)    | <span data-ttu-id="bd849-218">**Informazioni sul semaforo Get** (*tx_semaphore_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-218">**Semaphore information get** (*tx_semaphore_info_get*)</span></span> |
| ![Icona ottenere informazioni sulle prestazioni del semaforo](./media/user-guide/tx-events/image56.png)    | <span data-ttu-id="bd849-220">**Informazioni sulle prestazioni del semaforo Get** (*tx_semaphroe_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-220">**Semaphore performance information get** (*tx_semaphroe_performance_info_get*)</span></span> |
| ![Icona ottenere informazioni sulle prestazioni del sistema Semaphore](./media/user-guide/tx-events/image57.png)    | <span data-ttu-id="bd849-222">**Informazioni sulle prestazioni del sistema Semaphore Get** (*tx_semaphore_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-222">**Semaphore system performance information get** (*tx_semaphore_performance_system_info_get*)</span></span> |
| ![Icona priorità semaforo](./media/user-guide/tx-events/image58.png)    | <span data-ttu-id="bd849-224">**Priorità del semaforo** (*tx_semaphore_prioritize*)</span><span class="sxs-lookup"><span data-stu-id="bd849-224">**Semaphore prioritize** (*tx_semaphore_prioritize*)</span></span> |
| ![Icona put del semaforo](./media/user-guide/tx-events/image59.png)    | <span data-ttu-id="bd849-226">**Semaforo put** (*tx_semaphore_put*)</span><span class="sxs-lookup"><span data-stu-id="bd849-226">**Semaphore put** (*tx_semaphore_put*)</span></span> |
| ![Icona di notifica put del semaforo](./media/user-guide/tx-events/image60.png)    | <span data-ttu-id="bd849-228">**Notifica put semaforo** (*tx_semaphore_put_notify*)</span><span class="sxs-lookup"><span data-stu-id="bd849-228">**Semaphore put notify** (*tx_semaphore_put_notify*)</span></span> |
| ![Icona Creazione thread](./media/user-guide/tx-events/image61.png)    | <span data-ttu-id="bd849-230">**Creazione thread** (*tx_thread_create*)</span><span class="sxs-lookup"><span data-stu-id="bd849-230">**Thread create** (*tx_thread_create*)</span></span> |
| ![Icona di eliminazione thread](./media/user-guide/tx-events/image62.png)    | <span data-ttu-id="bd849-232">**Eliminazione thread** (*tx_thread_delete*)</span><span class="sxs-lookup"><span data-stu-id="bd849-232">**Thread delete** (*tx_thread_delete*)</span></span> |
| ![Icona di notifica di uscita/immissione thread](./media/user-guide/tx-events/image63.png)    | <span data-ttu-id="bd849-234">**Notifica di uscita/immissione thread** (*tx_thread_entry_exit_notify*)</span><span class="sxs-lookup"><span data-stu-id="bd849-234">**Thread exit/entry notify** (*tx_thread_entry_exit_notify*)</span></span> |
| ![Icona di identificazione del thread](./media/user-guide/tx-events/image64.png)    | <span data-ttu-id="bd849-236">**Identificazione del thread** (*tx_thread_identify*)</span><span class="sxs-lookup"><span data-stu-id="bd849-236">**Thread identify** (*tx_thread_identify*)</span></span> |
| ![Icona ottenere informazioni sul thread](./media/user-guide/tx-events/image65.png)    | <span data-ttu-id="bd849-238">**Informazioni sul thread Get** (*tx_thread_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-238">**Thread information get** (*tx_thread_info_get*)</span></span> |
| ![Icona ottenere informazioni sulle prestazioni del thread](./media/user-guide/tx-events/image66.png)    | <span data-ttu-id="bd849-240">**Informazioni sulle prestazioni del thread Get** (*tx_thread_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-240">**Thread performance information get** (*tx_thread_performance_info_get*)</span></span> |
| ![Icona ottenere informazioni sistema prestazioni thread](./media/user-guide/tx-events/image67.png)    | <span data-ttu-id="bd849-242">**Informazioni sul sistema di prestazioni del thread Get** (*tx_thread_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-242">**Thread performance system information get** (*tx_thread_performance_system_info_get*)</span></span> |
| ![Icona di modifica di precedenza thread](./media/user-guide/tx-events/image68.png)    | <span data-ttu-id="bd849-244">**Modifica di precedenza thread** (*tx_thread_preemption_change*)</span><span class="sxs-lookup"><span data-stu-id="bd849-244">**Thread preemption change** (*tx_thread_preemption_change*)</span></span> |
| ![Icona di modifica della priorità del thread](./media/user-guide/tx-events/image69.png)    | <span data-ttu-id="bd849-246">**Modifica della priorità del thread** (*tx_thread_priority_change*)</span><span class="sxs-lookup"><span data-stu-id="bd849-246">**Thread priority change** (*tx_thread_priority_change*)</span></span> |
| ![Icona di cessione thread](./media/user-guide/tx-events/image70.png)    | <span data-ttu-id="bd849-248">**Cessione thread** (*tx_thread_relinquish*)</span><span class="sxs-lookup"><span data-stu-id="bd849-248">**Thread relinquish** (*tx_thread_relinquish*)</span></span> |
| ![Icona di reimpostazione thread](./media/user-guide/tx-events/image71.png)    | <span data-ttu-id="bd849-250">**Reimpostazione thread** (*tx_thread_reset*)</span><span class="sxs-lookup"><span data-stu-id="bd849-250">**Thread reset** (*tx_thread_reset*)</span></span> |
| ![\* Icona Riprendi thread](./media/user-guide/tx-events/image72.png)    | <span data-ttu-id="bd849-252">**Ripresa thread** (\**tx_thread_resume*)</span><span class="sxs-lookup"><span data-stu-id="bd849-252">**Thread resume** (\**tx_thread_resume*)</span></span> |
| ![Icona sospensione thread](./media/user-guide/tx-events/image73.png)    | <span data-ttu-id="bd849-254">**Sospensione thread** (*tx_thread_sleep*) \*</span><span class="sxs-lookup"><span data-stu-id="bd849-254">**Thread Sleep** (*tx_thread_sleep*)\*</span></span> |
| ![Icona di notifica errori stack di thread](./media/user-guide/tx-events/image74.png)    | <span data-ttu-id="bd849-256">**Notifica errori stack di thread** (*tx_thread_stack_error_notify*)</span><span class="sxs-lookup"><span data-stu-id="bd849-256">**Thread stack error notify** (*tx_thread_stack_error_notify*)</span></span> |
| ![Icona di sospensione thread](./media/user-guide/tx-events/image75.png)    | <span data-ttu-id="bd849-258">**Sospensione thread** (*tx_thread_suspend*)</span><span class="sxs-lookup"><span data-stu-id="bd849-258">**Thread suspend** (*tx_thread_suspend*)</span></span> |
| ![Icona termina thread](./media/user-guide/tx-events/image76.png)    | <span data-ttu-id="bd849-260">**Terminazione thread** (*tx_thread_terminate*)</span><span class="sxs-lookup"><span data-stu-id="bd849-260">**Thread terminate** (*tx_thread_terminate*)</span></span> |
| ![Icona di modifica della sezione Tempo thread](./media/user-guide/tx-events/image77.png)    | <span data-ttu-id="bd849-262">**Modifica sezionamento tempo thread** (*tx_thread_time_slice_change*)</span><span class="sxs-lookup"><span data-stu-id="bd849-262">**Thread time-slice change** (*tx_thread_time_slice_change*)</span></span> |
| ![Icona interruzione thread di attesa](./media/user-guide/tx-events/image78.png)    | <span data-ttu-id="bd849-264">**Interruzione attesa thread** (*tx_thread_wait_abort*)</span><span class="sxs-lookup"><span data-stu-id="bd849-264">**Thread wait abort** (*tx_thread_wait_abort*)</span></span> |
| ![Icona Time Get](./media/user-guide/tx-events/image79.png)    | <span data-ttu-id="bd849-266">**Tempo di Get** (*tx_time_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-266">**Time get** (*tx_time_get*)</span></span> |
| ![Icona del set di tempo](./media/user-guide/tx-events/image80.png)    | <span data-ttu-id="bd849-268">**Set di tempo** (*tx_time_set*)</span><span class="sxs-lookup"><span data-stu-id="bd849-268">**Time set** (*tx_time_set*)</span></span> |
| ![\* Icona attiva timer](./media/user-guide/tx-events/image81.png)    | <span data-ttu-id="bd849-270">**Attivazione timer** (*tx_timer_activate*)</span><span class="sxs-lookup"><span data-stu-id="bd849-270">**Timer activate** (*tx_timer_activate*)</span></span> |
| ![Icona di modifica timer](./media/user-guide/tx-events/image82.png)    | <span data-ttu-id="bd849-272">**Modifica timer** (*tx_timer_change*)</span><span class="sxs-lookup"><span data-stu-id="bd849-272">**Timer change** (*tx_timer_change*)</span></span> |
| ![Icona Crea timer](./media/user-guide/tx-events/image83.png)    | <span data-ttu-id="bd849-274">**Creazione timer** (*tx_timer_create*)</span><span class="sxs-lookup"><span data-stu-id="bd849-274">**Timer create** (*tx_timer_create*)</span></span> |
| ![Icona Disattiva timer](./media/user-guide/tx-events/image84.png)    | <span data-ttu-id="bd849-276">**Disattiva timer** (*tx_timer_deactivate*)</span><span class="sxs-lookup"><span data-stu-id="bd849-276">**Timer deactivate** (*tx_timer_deactivate*)</span></span> |
| ![Icona di eliminazione timer](./media/user-guide/tx-events/image85.png)    | <span data-ttu-id="bd849-278">**Timer Delete** (*tx_timer_delete*)</span><span class="sxs-lookup"><span data-stu-id="bd849-278">**Timer delete** (*tx_timer_delete*)</span></span> |
| ![Icona ottenere informazioni sul timer](./media/user-guide/tx-events/image86.png)    | <span data-ttu-id="bd849-280">**Informazioni sul timer Get** (*tx_timer_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-280">**Timer information get** (*tx_timer_info_get*)</span></span> |
| ![Icona ottenere informazioni sulle prestazioni del timer](./media/user-guide/tx-events/image87.png)    | <span data-ttu-id="bd849-282">**Informazioni sulle prestazioni del timer Get** (*tx_timer_performance_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-282">**Timer performance information get** (*tx_timer_performance_info_get*)</span></span> |
| ![\* Icona ottenere informazioni sul sistema di prestazioni del timer](./media/user-guide/tx-events/image88.png)    | <span data-ttu-id="bd849-284">**Informazioni sul sistema di prestazioni del timer Get** (*tx_timer_performance_system_info_get*)</span><span class="sxs-lookup"><span data-stu-id="bd849-284">**Timer performance system information get** (*tx_timer_performance_system_info_get*)</span></span> |
| ![User-Defined eventicon](./media/user-guide/tx-events/image0.png)    | <span data-ttu-id="bd849-286">**Evento definito dall'utente** (vedere il capitolo 10)</span><span class="sxs-lookup"><span data-stu-id="bd849-286">**User-Defined Event** (See Chapter 10)</span></span>    |

## <a name="event-descriptions"></a><span data-ttu-id="bd849-287">Descrizioni di eventi</span><span class="sxs-lookup"><span data-stu-id="bd849-287">Event Descriptions</span></span>

### <a name="internal-thread-resume"></a><span data-ttu-id="bd849-288">Ripresa thread interno</span><span class="sxs-lookup"><span data-stu-id="bd849-288">Internal thread resume</span></span>

#### <a name="internal-thread-resume"></a><span data-ttu-id="bd849-289">Ripresa thread interno</span><span class="sxs-lookup"><span data-stu-id="bd849-289">Internal thread resume</span></span>

<span data-ttu-id="bd849-290">**Icona** ![ di Icona Riprendi thread interno](./media/user-guide/tx-events/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-290">**Icon** ![Internal thread resume icon](./media/user-guide/tx-events/image1.png)</span></span>

<span data-ttu-id="bd849-291">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-291">**Description**</span></span>

<span data-ttu-id="bd849-292">Questo evento rappresenta l'elaborazione interna in ThreadX che riprende un thread per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bd849-292">This event represents the internal processing in ThreadX that resumes a thread for execution.</span></span> <span data-ttu-id="bd849-293">Se il thread specificato è la priorità più alta e la soglia di precedenza non blocca l'esecuzione, il sistema avvierà l'esecuzione di questo thread appena pronto.</span><span class="sxs-lookup"><span data-stu-id="bd849-293">If the specified thread is the highest priority and preemption-threshold does not block its execution, the system will start executing this newly ready thread.</span></span>

<span data-ttu-id="bd849-294">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-294">**Information Fields**</span></span>

- <span data-ttu-id="bd849-295">Info Field 1: puntatore al thread ripreso.</span><span class="sxs-lookup"><span data-stu-id="bd849-295">Info Field 1: Pointer to the thread being resumed.</span></span>
- <span data-ttu-id="bd849-296">Info Field 2: stato precedente del thread ripreso, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="bd849-296">Info Field 2: Previous state of the thread being resumed, as follows:</span></span>

  |  <span data-ttu-id="bd849-297">Stato thread</span><span class="sxs-lookup"><span data-stu-id="bd849-297">Thread state</span></span>                     | <span data-ttu-id="bd849-298">Valore</span><span class="sxs-lookup"><span data-stu-id="bd849-298">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="bd849-299">TX_READY</span><span class="sxs-lookup"><span data-stu-id="bd849-299">TX_READY</span></span>                         | <span data-ttu-id="bd849-300">0</span><span class="sxs-lookup"><span data-stu-id="bd849-300">0</span></span>       |
  |  <span data-ttu-id="bd849-301">TX_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="bd849-301">TX_COMPLETED</span></span>                     | <span data-ttu-id="bd849-302">1</span><span class="sxs-lookup"><span data-stu-id="bd849-302">1</span></span>       |
  |  <span data-ttu-id="bd849-303">TX_TERMINATED</span><span class="sxs-lookup"><span data-stu-id="bd849-303">TX_TERMINATED</span></span>                    | <span data-ttu-id="bd849-304">2</span><span class="sxs-lookup"><span data-stu-id="bd849-304">2</span></span>       |
  |  <span data-ttu-id="bd849-305">TX_SUSPENDED</span><span class="sxs-lookup"><span data-stu-id="bd849-305">TX_SUSPENDED</span></span>                     | <span data-ttu-id="bd849-306">3</span><span class="sxs-lookup"><span data-stu-id="bd849-306">3</span></span>       |
  |  <span data-ttu-id="bd849-307">TX_SLEEP</span><span class="sxs-lookup"><span data-stu-id="bd849-307">TX_SLEEP</span></span>                         | <span data-ttu-id="bd849-308">4</span><span class="sxs-lookup"><span data-stu-id="bd849-308">4</span></span>       |
  |  <span data-ttu-id="bd849-309">TX_QUEUE_SUSP</span><span class="sxs-lookup"><span data-stu-id="bd849-309">TX_QUEUE_SUSP</span></span>                    | <span data-ttu-id="bd849-310">5</span><span class="sxs-lookup"><span data-stu-id="bd849-310">5</span></span>       |
  |  <span data-ttu-id="bd849-311">TX_SEMAPHORE_SUSP</span><span class="sxs-lookup"><span data-stu-id="bd849-311">TX_SEMAPHORE_SUSP</span></span>                | <span data-ttu-id="bd849-312">6</span><span class="sxs-lookup"><span data-stu-id="bd849-312">6</span></span>       |
  |  <span data-ttu-id="bd849-313">TX_EVENT_FLAG</span><span class="sxs-lookup"><span data-stu-id="bd849-313">TX_EVENT_FLAG</span></span>                    | <span data-ttu-id="bd849-314">7</span><span class="sxs-lookup"><span data-stu-id="bd849-314">7</span></span>       |
  |  <span data-ttu-id="bd849-315">TX_BLOCK_MEMORY</span><span class="sxs-lookup"><span data-stu-id="bd849-315">TX_BLOCK_MEMORY</span></span>                  | <span data-ttu-id="bd849-316">8</span><span class="sxs-lookup"><span data-stu-id="bd849-316">8</span></span>       |
  |  <span data-ttu-id="bd849-317">TX_BYTE_MEMORY</span><span class="sxs-lookup"><span data-stu-id="bd849-317">TX_BYTE_MEMORY</span></span>                   | <span data-ttu-id="bd849-318">9</span><span class="sxs-lookup"><span data-stu-id="bd849-318">9</span></span>       |
  |  <span data-ttu-id="bd849-319">TX_TCP_IP</span><span class="sxs-lookup"><span data-stu-id="bd849-319">TX_TCP_IP</span></span>                        | <span data-ttu-id="bd849-320">12</span><span class="sxs-lookup"><span data-stu-id="bd849-320">12</span></span>      |
  |  <span data-ttu-id="bd849-321">TX_MUTEX_SUSP</span><span class="sxs-lookup"><span data-stu-id="bd849-321">TX_MUTEX_SUSP</span></span>                    | <span data-ttu-id="bd849-322">13</span><span class="sxs-lookup"><span data-stu-id="bd849-322">13</span></span>      |

- <span data-ttu-id="bd849-323">Informazioni sul campo 3: valore del puntatore dello stack durante la chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-323">Info Field 3: Stack pointer value during the call.</span></span> 
- <span data-ttu-id="bd849-324">Info Field 4: puntatore al thread con priorità più alta successiva da eseguire.</span><span class="sxs-lookup"><span data-stu-id="bd849-324">Info Field 4: Pointer to next highest priority thread to execute.</span></span>

### <a name="internal-thread-suspend"></a><span data-ttu-id="bd849-325">Sospensione thread interno</span><span class="sxs-lookup"><span data-stu-id="bd849-325">Internal thread suspend</span></span>

#### <a name="internal-thread-suspend"></a><span data-ttu-id="bd849-326">Sospensione thread interno</span><span class="sxs-lookup"><span data-stu-id="bd849-326">Internal thread suspend</span></span>

<span data-ttu-id="bd849-327">**Icona** ![ di Icona di sospensione thread interno](./media/user-guide/tx-events/image2.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-327">**Icon** ![Internal thread suspend icon](./media/user-guide/tx-events/image2.png)</span></span>

<span data-ttu-id="bd849-328">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-328">**Description**</span></span>

<span data-ttu-id="bd849-329">Questo evento rappresenta l'elaborazione interna in ThreadX che sospende l'esecuzione di un thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-329">This event represents the internal processing in ThreadX that suspends a thread's execution.</span></span> <span data-ttu-id="bd849-330">Il thread successivo con priorità più alta pronto per l'esecuzione viene inserito nel quarto campo informazioni.</span><span class="sxs-lookup"><span data-stu-id="bd849-330">The next highest priority thread ready for execution is placed in the fourth information field.</span></span> <span data-ttu-id="bd849-331">Se questo valore è NULL, nessun altro thread è pronto per l'esecuzione e il sistema è inattivo.</span><span class="sxs-lookup"><span data-stu-id="bd849-331">If this value is NULL, there is no other thread ready for execution and the system is idle.</span></span>

<span data-ttu-id="bd849-332">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-332">**Information Fields**</span></span>

- <span data-ttu-id="bd849-333">Info Field 1: puntatore al thread sospeso.</span><span class="sxs-lookup"><span data-stu-id="bd849-333">Info Field 1: Pointer to the thread being suspended.</span></span>
- <span data-ttu-id="bd849-334">Info Field 2: nuovo stato del thread sospeso, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="bd849-334">Info Field 2: New state of the thread being suspended, as follows:</span></span>

  |  <span data-ttu-id="bd849-335">Stato thread</span><span class="sxs-lookup"><span data-stu-id="bd849-335">Thread state</span></span>                     | <span data-ttu-id="bd849-336">Valore</span><span class="sxs-lookup"><span data-stu-id="bd849-336">Value</span></span>        |
  |---------------------------------- | --------|
  |  <span data-ttu-id="bd849-337">TX_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="bd849-337">TX_COMPLETED</span></span>                     | <span data-ttu-id="bd849-338">1</span><span class="sxs-lookup"><span data-stu-id="bd849-338">1</span></span>       |
  |  <span data-ttu-id="bd849-339">TX_TERMINATED</span><span class="sxs-lookup"><span data-stu-id="bd849-339">TX_TERMINATED</span></span>                    | <span data-ttu-id="bd849-340">2</span><span class="sxs-lookup"><span data-stu-id="bd849-340">2</span></span>       |
  |  <span data-ttu-id="bd849-341">TX_SUSPENDED</span><span class="sxs-lookup"><span data-stu-id="bd849-341">TX_SUSPENDED</span></span>                     | <span data-ttu-id="bd849-342">3</span><span class="sxs-lookup"><span data-stu-id="bd849-342">3</span></span>       |
  |  <span data-ttu-id="bd849-343">TX_SLEEP</span><span class="sxs-lookup"><span data-stu-id="bd849-343">TX_SLEEP</span></span>                         | <span data-ttu-id="bd849-344">4</span><span class="sxs-lookup"><span data-stu-id="bd849-344">4</span></span>       |
  |  <span data-ttu-id="bd849-345">TX_QUEUE_SUSP</span><span class="sxs-lookup"><span data-stu-id="bd849-345">TX_QUEUE_SUSP</span></span>                    | <span data-ttu-id="bd849-346">5</span><span class="sxs-lookup"><span data-stu-id="bd849-346">5</span></span>       |
  |  <span data-ttu-id="bd849-347">TX_SEMAPHORE_SUSP</span><span class="sxs-lookup"><span data-stu-id="bd849-347">TX_SEMAPHORE_SUSP</span></span>                | <span data-ttu-id="bd849-348">6</span><span class="sxs-lookup"><span data-stu-id="bd849-348">6</span></span>       |
  |  <span data-ttu-id="bd849-349">TX_EVENT_FLAG</span><span class="sxs-lookup"><span data-stu-id="bd849-349">TX_EVENT_FLAG</span></span>                    | <span data-ttu-id="bd849-350">7</span><span class="sxs-lookup"><span data-stu-id="bd849-350">7</span></span>       |
  |  <span data-ttu-id="bd849-351">TX_BLOCK_MEMORY</span><span class="sxs-lookup"><span data-stu-id="bd849-351">TX_BLOCK_MEMORY</span></span>                  | <span data-ttu-id="bd849-352">8</span><span class="sxs-lookup"><span data-stu-id="bd849-352">8</span></span>       |
  |  <span data-ttu-id="bd849-353">TX_BYTE_MEMORY</span><span class="sxs-lookup"><span data-stu-id="bd849-353">TX_BYTE_MEMORY</span></span>                   | <span data-ttu-id="bd849-354">9</span><span class="sxs-lookup"><span data-stu-id="bd849-354">9</span></span>       |
  |  <span data-ttu-id="bd849-355">TX_TCP_IP</span><span class="sxs-lookup"><span data-stu-id="bd849-355">TX_TCP_IP</span></span>                        | <span data-ttu-id="bd849-356">12</span><span class="sxs-lookup"><span data-stu-id="bd849-356">12</span></span>      |
  |  <span data-ttu-id="bd849-357">TX_MUTEX_SUSP</span><span class="sxs-lookup"><span data-stu-id="bd849-357">TX_MUTEX_SUSP</span></span>                    | <span data-ttu-id="bd849-358">13</span><span class="sxs-lookup"><span data-stu-id="bd849-358">13</span></span>      |

- <span data-ttu-id="bd849-359">Informazioni sul campo 3: valore del puntatore dello stack durante la chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-359">Info Field 3: Stack pointer value during the call.</span></span> <span data-ttu-id="bd849-360">Info Field 4: puntatore al thread con priorità più alta successiva da eseguire.</span><span class="sxs-lookup"><span data-stu-id="bd849-360">Info Field 4: Pointer to next highest priority thread to execute.</span></span> <span data-ttu-id="bd849-361">Se NULL, il sistema è inattivo.</span><span class="sxs-lookup"><span data-stu-id="bd849-361">If NULL, the system is idle.</span></span>

### <a name="interrupt-service-routine-isr-enter"></a><span data-ttu-id="bd849-362">Routine del servizio di interrupt (ISR) invio</span><span class="sxs-lookup"><span data-stu-id="bd849-362">Interrupt Service Routine (ISR) enter</span></span> 

#### <a name="enter-isr"></a><span data-ttu-id="bd849-363">Immettere ISR</span><span class="sxs-lookup"><span data-stu-id="bd849-363">Enter ISR</span></span> 

<span data-ttu-id="bd849-364">**Icona** ![ di Icona di immissione I S R](./media/user-guide/tx-events/image3.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-364">**Icon** ![Enter I S R icon](./media/user-guide/tx-events/image3.png)</span></span>

<span data-ttu-id="bd849-365">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-365">**Description**</span></span>

<span data-ttu-id="bd849-366">Questo evento rappresenta l'immissione di una routine del servizio di interrupt (ISR) nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bd849-366">This event represents entering an Interrupt Service Routine (ISR) in the application.</span></span> <span data-ttu-id="bd849-367">L'esecuzione della routine del servizio di interrupt continua fino a quando non si verifica l'evento di uscita ISR.</span><span class="sxs-lookup"><span data-stu-id="bd849-367">The interrupt service routine execution continues until the ISR exit event takes place.</span></span>

<span data-ttu-id="bd849-368">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-368">**Information Fields**</span></span>

- <span data-ttu-id="bd849-369">Informazioni campo 1: valore del puntatore dello stack durante la chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-369">Info Field 1: Stack pointer value during the call.</span></span>
- <span data-ttu-id="bd849-370">Informazioni campo 2: numero ISR definito dall'applicazione (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="bd849-370">Info Field 2: Application-defined ISR number (optional).</span></span>
- <span data-ttu-id="bd849-371">Informazioni sul campo 3: numero di interrupt annidati.</span><span class="sxs-lookup"><span data-stu-id="bd849-371">Info Field 3: Nested interrupt count.</span></span>
- <span data-ttu-id="bd849-372">Informazioni campo 4: flag di disabilitazione di precedenza interno.</span><span class="sxs-lookup"><span data-stu-id="bd849-372">Info Field 4: Internal preemption disable flag.</span></span>

### <a name="interrupt-service-routine-isr-exit"></a><span data-ttu-id="bd849-373">Uscita routine servizio di interrupt (ISR)</span><span class="sxs-lookup"><span data-stu-id="bd849-373">Interrupt Service Routine (ISR) exit</span></span> 

#### <a name="exit-isr"></a><span data-ttu-id="bd849-374">Uscita ISR</span><span class="sxs-lookup"><span data-stu-id="bd849-374">Exit ISR</span></span>

<span data-ttu-id="bd849-375">**Icona** ![ di Icona di uscita I S R](./media/user-guide/tx-events/image4.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-375">**Icon** ![Exit I S R icon](./media/user-guide/tx-events/image4.png)</span></span>

<span data-ttu-id="bd849-376">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-376">**Description**</span></span>

<span data-ttu-id="bd849-377">Questo evento rappresenta l'uscita da una routine del servizio di interrupt (ISR) nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bd849-377">This event represents exiting an Interrupt Service Routine (ISR) in the application.</span></span>

<span data-ttu-id="bd849-378">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-378">**Information Fields**</span></span>

- <span data-ttu-id="bd849-379">Informazioni campo 1: valore del puntatore dello stack durante la chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-379">Info Field 1: Stack pointer value during the call.</span></span>
- <span data-ttu-id="bd849-380">Informazioni campo 2: numero ISR definito dall'applicazione (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="bd849-380">Info Field 2: Application-defined ISR number (optional).</span></span>
- <span data-ttu-id="bd849-381">Informazioni sul campo 3: numero di interrupt annidati.</span><span class="sxs-lookup"><span data-stu-id="bd849-381">Info Field 3: Nested interrupt count.</span></span>
- <span data-ttu-id="bd849-382">Informazioni campo 4: flag di disabilitazione di precedenza interno.</span><span class="sxs-lookup"><span data-stu-id="bd849-382">Info Field 4: Internal preemption disable flag.</span></span>

### <a name="internal-time-slice"></a><span data-ttu-id="bd849-383">Sezione tempo interna</span><span class="sxs-lookup"><span data-stu-id="bd849-383">Internal time-slice</span></span>

#### <a name="internal-time-slice"></a><span data-ttu-id="bd849-384">Sezione tempo interna</span><span class="sxs-lookup"><span data-stu-id="bd849-384">Internal time-slice</span></span>

<span data-ttu-id="bd849-385">**Icona** ![ di Icona dell'intervallo di tempo interno](./media/user-guide/tx-events/image5.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-385">**Icon** ![Internal time-slice icon](./media/user-guide/tx-events/image5.png)</span></span>

<span data-ttu-id="bd849-386">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-386">**Description**</span></span>

<span data-ttu-id="bd849-387">Questo evento rappresenta l'elaborazione interna in ThreadX che esegue l'operazione di sezionamento del tempo.</span><span class="sxs-lookup"><span data-stu-id="bd849-387">This event represents the internal processing in ThreadX that performs the time-slice operation.</span></span> <span data-ttu-id="bd849-388">Il thread successivo con la stessa priorità viene inserito nel primo campo informazioni.</span><span class="sxs-lookup"><span data-stu-id="bd849-388">The next thread of the same priority is placed in the first information field.</span></span> <span data-ttu-id="bd849-389">Se questo valore corrisponde al thread corrente, non è stato eseguito alcun intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="bd849-389">If this value is the same as the current thread, no time-slice was performed.</span></span>

- <span data-ttu-id="bd849-390">Info Field 1: puntatore al thread successivo da eseguire.</span><span class="sxs-lookup"><span data-stu-id="bd849-390">Info Field 1: Pointer to the next thread to execute.</span></span>
- <span data-ttu-id="bd849-391">Informazioni sul campo 2: numero di interrupt annidati.</span><span class="sxs-lookup"><span data-stu-id="bd849-391">Info Field 2: Nested interrupt count.</span></span>
- <span data-ttu-id="bd849-392">Informazioni campo 3: flag di disabilitazione di precedenza interno.</span><span class="sxs-lookup"><span data-stu-id="bd849-392">Info Field 3: Internal preemption disable flag.</span></span>
- <span data-ttu-id="bd849-393">Informazioni sul campo 4: valore del puntatore dello stack durante la chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-393">Info Field 4: Stack pointer value during the call.</span></span>

### <a name="running"></a><span data-ttu-id="bd849-394">In esecuzione</span><span class="sxs-lookup"><span data-stu-id="bd849-394">Running</span></span>

#### <a name="running-in-context"></a><span data-ttu-id="bd849-395">In esecuzione nel contesto</span><span class="sxs-lookup"><span data-stu-id="bd849-395">Running in context</span></span>

<span data-ttu-id="bd849-396">**Icona** ![ di Icona in esecuzione](./media/user-guide/tx-events/image6.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-396">**Icon** ![Running icon](./media/user-guide/tx-events/image6.png)</span></span>

<span data-ttu-id="bd849-397">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-397">**Description**</span></span>

<span data-ttu-id="bd849-398">Questo evento rappresenta l'esecuzione in un contesto di thread o in un sistema inattivo.</span><span class="sxs-lookup"><span data-stu-id="bd849-398">This event represents running within a thread context or idle system.</span></span> <span data-ttu-id="bd849-399">Viene usato per illustrare le modifiche successive nel contesto in seguito a un interrupt.</span><span class="sxs-lookup"><span data-stu-id="bd849-399">It is used to illustrate subsequent changes in context as a result of an interrupt.</span></span>

<span data-ttu-id="bd849-400">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-400">**Information Fields**</span></span>
- <span data-ttu-id="bd849-401">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-401">Info Field 1: Not used.</span></span>
- <span data-ttu-id="bd849-402">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-402">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-403">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-403">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-404">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-404">Info Field 4: Not used.</span></span>

### <a name="block-allocate"></a><span data-ttu-id="bd849-405">Alloca blocco</span><span class="sxs-lookup"><span data-stu-id="bd849-405">Block Allocate</span></span> 

#### <a name="tx_block_allocate"></a><span data-ttu-id="bd849-406">tx_block_allocate</span><span class="sxs-lookup"><span data-stu-id="bd849-406">tx_block_allocate</span></span>

<span data-ttu-id="bd849-407">**Icona** ![ di Icona di allocazione blocchi](./media/user-guide/tx-events/image7.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-407">**Icon** ![Block allocate icon](./media/user-guide/tx-events/image7.png)</span></span>

<span data-ttu-id="bd849-408">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-408">**Description**</span></span>

<span data-ttu-id="bd849-409">Questo evento rappresenta l'allocazione di un blocco di memoria tramite tx_block_allocate.</span><span class="sxs-lookup"><span data-stu-id="bd849-409">This event represents allocating a memory block via tx_block_allocate.</span></span> <span data-ttu-id="bd849-410">In caso di esito positivo, l'indirizzo del blocco allocato viene restituito nel secondo campo informazioni.</span><span class="sxs-lookup"><span data-stu-id="bd849-410">If successful, the address of the block allocated is returned in the second information field.</span></span>

<span data-ttu-id="bd849-411">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-411">**Information Fields**</span></span>
- <span data-ttu-id="bd849-412">Info Field 1: puntatore al pool di blocchi corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-412">Info Field 1: Pointer to the corresponding block pool.</span></span>
- <span data-ttu-id="bd849-413">Info Field 2: puntatore al blocco di memoria restituito (in caso di esito positivo).</span><span class="sxs-lookup"><span data-stu-id="bd849-413">Info Field 2: Pointer to the memory block returned (if successful).</span></span>
- <span data-ttu-id="bd849-414">Info Field 3: l'opzione wait fornita alla chiamata tx_block_allocate.</span><span class="sxs-lookup"><span data-stu-id="bd849-414">Info Field 3: The wait option supplied to the tx_block_allocate call.</span></span>
- <span data-ttu-id="bd849-415">Informazioni campo 4: blocchi disponibili rimanenti nel pool dopo questa allocazione.</span><span class="sxs-lookup"><span data-stu-id="bd849-415">Info Field 4: Remaining available blocks in the pool after this allocation.</span></span>

### <a name="block-pool-create"></a><span data-ttu-id="bd849-416">Creazione di un pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="bd849-416">Block Pool Create</span></span>

#### <a name="tx_block_pool_create"></a><span data-ttu-id="bd849-417">tx_block_pool_create</span><span class="sxs-lookup"><span data-stu-id="bd849-417">tx_block_pool_create</span></span>

<span data-ttu-id="bd849-418">**Icona** ![ di Icona di creazione del pool di blocchi](./media/user-guide/tx-events/image8.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-418">**Icon** ![Block pool create icon](./media/user-guide/tx-events/image8.png)</span></span>

<span data-ttu-id="bd849-419">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-419">**Description**</span></span>

<span data-ttu-id="bd849-420">Questo evento rappresenta la creazione di un pool di blocchi di memoria tramite tx_block_pool_create.</span><span class="sxs-lookup"><span data-stu-id="bd849-420">This event represents creating a memory block pool via tx_block_pool_create.</span></span>

<span data-ttu-id="bd849-421">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-421">**Information Fields**</span></span>

- <span data-ttu-id="bd849-422">Info Field 1: puntatore al blocco di controllo del pool di blocchi corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-422">Info Field 1: Pointer to the corresponding block pool control block.</span></span>
- <span data-ttu-id="bd849-423">Info Field 2: puntatore all'area di memoria iniziale del pool.</span><span class="sxs-lookup"><span data-stu-id="bd849-423">Info Field 2: Pointer to the starting memory area of the pool.</span></span>
- <span data-ttu-id="bd849-424">Info Field 3: numero di blocchi nel pool.</span><span class="sxs-lookup"><span data-stu-id="bd849-424">Info Field 3: The number of blocks in the pool.</span></span> <span data-ttu-id="bd849-425">Campo informazioni 4: dimensioni di ogni blocco nel pool in byte.</span><span class="sxs-lookup"><span data-stu-id="bd849-425">Info Field 4: The size of each block in the pool in bytes.</span></span>

### <a name="block-pool-delete"></a><span data-ttu-id="bd849-426">Eliminazione del pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="bd849-426">Block Pool Delete</span></span>

#### <a name="tx_block_pool_delete"></a><span data-ttu-id="bd849-427">tx_block_pool_delete</span><span class="sxs-lookup"><span data-stu-id="bd849-427">tx_block_pool_delete</span></span>

<span data-ttu-id="bd849-428">**Icona** ![ di Icona di eliminazione del pool di blocchi](./media/user-guide/tx-events/image9.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-428">**Icon** ![Block pool delete icon](./media/user-guide/tx-events/image9.png)</span></span>

<span data-ttu-id="bd849-429">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-429">**Description**</span></span>

<span data-ttu-id="bd849-430">Questo evento rappresenta l'eliminazione di un pool di blocchi di memoria tramite tx_block_pool_delete.</span><span class="sxs-lookup"><span data-stu-id="bd849-430">This event represents deleting a memory block pool via tx_block_pool_delete.</span></span>

<span data-ttu-id="bd849-431">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-431">**Information Fields**</span></span>

- <span data-ttu-id="bd849-432">Info Field 1: puntatore al blocco di controllo del pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="bd849-432">Info Field 1: Pointer to the block pool control block.</span></span>
- <span data-ttu-id="bd849-433">Informazioni sul campo 2: valore del puntatore dello stack durante la chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-433">Info Field 2: Stack pointer value during the call.</span></span>
- <span data-ttu-id="bd849-434">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-434">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-435">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-435">Info Field 4: Not used.</span></span>

### <a name="block-pool-information-get"></a><span data-ttu-id="bd849-436">Ottieni informazioni sul pool di blocco</span><span class="sxs-lookup"><span data-stu-id="bd849-436">Block Pool Information Get</span></span> 

#### <a name="tx_block_pool_info_get"></a><span data-ttu-id="bd849-437">tx_block_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-437">tx_block_pool_info_get</span></span>

<span data-ttu-id="bd849-438">**Icona** ![ di Icona Ottieni informazioni sul pool di blocchi](./media/user-guide/tx-events/image10.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-438">**Icon** ![Block pool information get icon](./media/user-guide/tx-events/image10.png)</span></span>

<span data-ttu-id="bd849-439">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-439">**Description**</span></span>

<span data-ttu-id="bd849-440">Questo evento rappresenta il recupero di informazioni su un pool di blocchi di memoria tramite tx_block_pool_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-440">This event represents getting information about a memory block pool via tx_block_pool_info_get.</span></span>

<span data-ttu-id="bd849-441">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-441">**Information Fields**</span></span>

- <span data-ttu-id="bd849-442">Info Field 1: puntatore al blocco di controllo del pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="bd849-442">Info Field 1: Pointer to the block pool control block.</span></span>
- <span data-ttu-id="bd849-443">Informazioni sul campo 2: valore del puntatore dello stack durante la chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-443">Info Field 2: Stack pointer value during the call.</span></span>
- <span data-ttu-id="bd849-444">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-444">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-445">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-445">Info Field 4: Not used.</span></span>

### <a name="block-pool-performance-information-get"></a><span data-ttu-id="bd849-446">Informazioni sulle prestazioni del pool di blocco Get</span><span class="sxs-lookup"><span data-stu-id="bd849-446">Block Pool Performance Information Get</span></span>

#### <a name="tx_block_pool_performance_info_get"></a><span data-ttu-id="bd849-447">tx_block_pool_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-447">tx_block_pool_performance_info_get</span></span>

<span data-ttu-id="bd849-448">**Icona** ![ di Icona Ottieni informazioni sulle prestazioni del pool di blocchi](./media/user-guide/tx-events/image11.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-448">**Icon** ![Block pool performance information get icon](./media/user-guide/tx-events/image11.png)</span></span>

<span data-ttu-id="bd849-449">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-449">**Description**</span></span>

<span data-ttu-id="bd849-450">Questo evento rappresenta il recupero delle informazioni sulle prestazioni di un pool di blocchi di memoria tramite tx_block_pool_performance_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-450">This event represents getting performance information about a memory block pool via tx_block_pool_performance_info_get.</span></span>

<span data-ttu-id="bd849-451">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-451">**Information Fields**</span></span>

- <span data-ttu-id="bd849-452">Info Field 1: puntatore al blocco di controllo del pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="bd849-452">Info Field 1: Pointer to the block pool control block.</span></span>
- <span data-ttu-id="bd849-453">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-453">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-454">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-454">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-455">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-455">Info Field 4: Not used.</span></span>

### <a name="block-pool-performance-system-information-get"></a><span data-ttu-id="bd849-456">Informazioni sul sistema di prestazioni del pool di blocchi Get</span><span class="sxs-lookup"><span data-stu-id="bd849-456">Block Pool Performance System Information Get</span></span>

#### <a name="tx_block_pool_performance_system_info_get"></a><span data-ttu-id="bd849-457">tx_block_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-457">tx_block_pool_performance_system_info_get</span></span>

<span data-ttu-id="bd849-458">**Icona** ![ di Icona Ottieni informazioni sul sistema di prestazioni del pool di blocchi](./media/user-guide/tx-events/image12.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-458">**Icon** ![Block pool performance system information get icon](./media/user-guide/tx-events/image12.png)</span></span>

<span data-ttu-id="bd849-459">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-459">**Description**</span></span>

<span data-ttu-id="bd849-460">Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni relative a tutti i pool di blocchi di memoria tramite tx_block_pool_performance_system_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-460">This event represents getting performance information about all memory block pools via tx_block_pool_performance_system_info_get.</span></span>

<span data-ttu-id="bd849-461">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-461">**Information Fields**</span></span>
- <span data-ttu-id="bd849-462">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-462">Info Field 1: Not used.</span></span>
- <span data-ttu-id="bd849-463">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-463">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-464">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-464">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-465">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-465">Info Field 4: Not used.</span></span>

### <a name="block-pool-prioritize"></a><span data-ttu-id="bd849-466">Priorità del pool di blocchi</span><span class="sxs-lookup"><span data-stu-id="bd849-466">Block Pool Prioritize</span></span>

#### <a name="tx_block_pool_prioritize"></a><span data-ttu-id="bd849-467">tx_block_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="bd849-467">tx_block_pool_prioritize</span></span>

<span data-ttu-id="bd849-468">**Icona** ![ di Icona di priorità del pool di blocchi](./media/user-guide/tx-events/image13.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-468">**Icon** ![Block pool prioritize icon](./media/user-guide/tx-events/image13.png)</span></span>

<span data-ttu-id="bd849-469">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-469">**Description**</span></span>

<span data-ttu-id="bd849-470">Questo evento rappresenta l'inserimento del thread sospeso PrioritàMassima all'inizio dell'elenco di sospensioni del pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="bd849-470">This event represents placing the highestpriority suspended thread at the front of the block pool suspension list.</span></span> <span data-ttu-id="bd849-471">Se questa operazione viene eseguita prima di chiamare tx_block_release, il thread sospeso con la priorità più alta riceverà il blocco rilasciato.</span><span class="sxs-lookup"><span data-stu-id="bd849-471">If this is done prior to calling tx_block_release, the highest priority suspended thread will receive the released block.</span></span>

<span data-ttu-id="bd849-472">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-472">**Information Fields**</span></span>
- <span data-ttu-id="bd849-473">Campo informazioni 1: puntatore al pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="bd849-473">Info Field 1: Memory block pool pointer.</span></span>
- <span data-ttu-id="bd849-474">Campo informazioni 2: numero di thread sospesi in questo pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="bd849-474">Info Field 2: Number of threads suspended on this block pool.</span></span>
- <span data-ttu-id="bd849-475">Campo info 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-475">Info Field 3: Stack pointer at the time of the call.</span></span>
- <span data-ttu-id="bd849-476">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-476">Info Field 4: Not used.</span></span>

### <a name="block-release"></a><span data-ttu-id="bd849-477">Blocca versione</span><span class="sxs-lookup"><span data-stu-id="bd849-477">Block Release</span></span> 

#### <a name="tx_block_release"></a><span data-ttu-id="bd849-478">tx_block_release</span><span class="sxs-lookup"><span data-stu-id="bd849-478">tx_block_release</span></span>

<span data-ttu-id="bd849-479">**Icona** ![ di Icona di rilascio del blocco](./media/user-guide/tx-events/image14.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-479">**Icon** ![Block release icon](./media/user-guide/tx-events/image14.png)</span></span>

<span data-ttu-id="bd849-480">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-480">**Description**</span></span>

<span data-ttu-id="bd849-481">Questo evento rappresenta il rilascio di un blocco precedentemente allocato al pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="bd849-481">This event represents releasing a previously allocated block back to the block pool.</span></span>

<span data-ttu-id="bd849-482">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-482">**Information Fields**</span></span>

- <span data-ttu-id="bd849-483">Campo informazioni 1: puntatore al pool di blocchi di memoria.</span><span class="sxs-lookup"><span data-stu-id="bd849-483">Info Field 1: Memory block pool pointer.</span></span>
- <span data-ttu-id="bd849-484">Informazioni sul campo 2: puntatore a blocco da rilasciare.</span><span class="sxs-lookup"><span data-stu-id="bd849-484">Info Field 2: Pointer to block to release.</span></span>
- <span data-ttu-id="bd849-485">Campo info 3: numero di thread sospesi in questo pool di blocchi.</span><span class="sxs-lookup"><span data-stu-id="bd849-485">Info Field 3: Number of threads suspended on this block pool.</span></span>
- <span data-ttu-id="bd849-486">Informazioni sul campo 4: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-486">Info Field 4: Stack pointer at the time of the call.</span></span>

### <a name="byte-allocate"></a><span data-ttu-id="bd849-487">Allocazione byte</span><span class="sxs-lookup"><span data-stu-id="bd849-487">Byte Allocate</span></span> 

#### <a name="tx_byte_allocate"></a><span data-ttu-id="bd849-488">tx_byte_allocate</span><span class="sxs-lookup"><span data-stu-id="bd849-488">tx_byte_allocate</span></span>

<span data-ttu-id="bd849-489">**Icona** ![ di Icona di allocazione byte](./media/user-guide/tx-events/image15.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-489">**Icon** ![Byte allocate icon](./media/user-guide/tx-events/image15.png)</span></span>

<span data-ttu-id="bd849-490">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-490">**Description**</span></span>

<span data-ttu-id="bd849-491">Questo evento rappresenta l'allocazione della memoria tramite tx_byte_allocate.</span><span class="sxs-lookup"><span data-stu-id="bd849-491">This event represents allocating memory via tx_byte_allocate.</span></span> <span data-ttu-id="bd849-492">In caso di esito positivo, l'indirizzo della memoria allocata viene restituito nel secondo campo informazioni.</span><span class="sxs-lookup"><span data-stu-id="bd849-492">If successful, the address of the memory allocated is returned in the second information field.</span></span>

<span data-ttu-id="bd849-493">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-493">**Information Fields**</span></span>
- <span data-ttu-id="bd849-494">Info Field 1: puntatore al pool di byte corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-494">Info Field 1: Pointer to the corresponding byte pool.</span></span>
- <span data-ttu-id="bd849-495">Info Field 2: puntatore alla memoria restituita (in caso di esito positivo).</span><span class="sxs-lookup"><span data-stu-id="bd849-495">Info Field 2: Pointer to the memory returned (if successful).</span></span>
- <span data-ttu-id="bd849-496">Campo info 3: numero di byte richiesti.</span><span class="sxs-lookup"><span data-stu-id="bd849-496">Info Field 3: Number of bytes requested.</span></span> <span data-ttu-id="bd849-497">Info Field 4: l'opzione wait fornita alla chiamata tx_byte_allocate.</span><span class="sxs-lookup"><span data-stu-id="bd849-497">Info Field 4: The wait option supplied to the tx_byte_allocate call.</span></span>

### <a name="byte-pool-create"></a><span data-ttu-id="bd849-498">Creazione pool di byte</span><span class="sxs-lookup"><span data-stu-id="bd849-498">Byte Pool Create</span></span>

#### <a name="tx_byte_pool_create"></a><span data-ttu-id="bd849-499">tx_byte_pool_create</span><span class="sxs-lookup"><span data-stu-id="bd849-499">tx_byte_pool_create</span></span>

<span data-ttu-id="bd849-500">**Icona** ![ di Icona di creazione pool di byte](./media/user-guide/tx-events/image16.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-500">**Icon** ![Byte pool create icon](./media/user-guide/tx-events/image16.png)</span></span>

<span data-ttu-id="bd849-501">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-501">**Description**</span></span>

<span data-ttu-id="bd849-502">Questo evento rappresenta la creazione di un pool di byte tramite tx_byte_pool_create.</span><span class="sxs-lookup"><span data-stu-id="bd849-502">This event represents creating a byte pool via tx_byte_pool_create.</span></span>

<span data-ttu-id="bd849-503">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-503">**Information Fields**</span></span>

- <span data-ttu-id="bd849-504">Info Field 1: puntatore al pool di byte corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-504">Info Field 1: Pointer to the corresponding byte pool.</span></span>
- <span data-ttu-id="bd849-505">Info Field 2: puntatore all'inizio dell'area di memoria.</span><span class="sxs-lookup"><span data-stu-id="bd849-505">Info Field 2: Pointer to the start of the memory area.</span></span> <span data-ttu-id="bd849-506">Campo info 3: numero di byte nel pool di byte.</span><span class="sxs-lookup"><span data-stu-id="bd849-506">Info Field 3: Number of bytes in the byte pool.</span></span>
- <span data-ttu-id="bd849-507">Info Field 4: il puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-507">Info Field 4: The stack pointer at the time of the call.</span></span>

### <a name="byte-pool-delete"></a><span data-ttu-id="bd849-508">Eliminazione pool di byte</span><span class="sxs-lookup"><span data-stu-id="bd849-508">Byte Pool Delete</span></span> 

#### <a name="tx_byte_pool_delete"></a><span data-ttu-id="bd849-509">tx_byte_pool_delete</span><span class="sxs-lookup"><span data-stu-id="bd849-509">tx_byte_pool_delete</span></span>

<span data-ttu-id="bd849-510">**Icona** ![ di Icona di eliminazione del pool di byte](./media/user-guide/tx-events/image17.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-510">**Icon** ![Byte pool delete icon](./media/user-guide/tx-events/image17.png)</span></span>

<span data-ttu-id="bd849-511">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-511">**Description**</span></span>

<span data-ttu-id="bd849-512">Questo evento rappresenta l'eliminazione di un pool di byte tramite tx_byte_pool_delete.</span><span class="sxs-lookup"><span data-stu-id="bd849-512">This event represents deleting a byte pool via tx_byte_pool_delete.</span></span>

<span data-ttu-id="bd849-513">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-513">**Information Fields**</span></span>

- <span data-ttu-id="bd849-514">Info Field 1: puntatore al pool di byte corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-514">Info Field 1: Pointer to the corresponding byte pool.</span></span>
- <span data-ttu-id="bd849-515">Info Field 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-515">Info Field 2: The stack pointer at the time of the call.</span></span>
- <span data-ttu-id="bd849-516">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-516">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-517">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-517">Info Field 4: Not used.</span></span>

### <a name="byte-pool-information-get"></a><span data-ttu-id="bd849-518">Ottenere informazioni sul pool di byte</span><span class="sxs-lookup"><span data-stu-id="bd849-518">Byte Pool Information Get</span></span>

#### <a name="tx_byte_pool_info_get"></a><span data-ttu-id="bd849-519">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-519">tx_byte_pool_info_get</span></span>

<span data-ttu-id="bd849-520">**Icona** ![ di Icona ottenere informazioni sul pool di byte](./media/user-guide/tx-events/image18.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-520">**Icon** ![Byte pool information get icon](./media/user-guide/tx-events/image18.png)</span></span>

<span data-ttu-id="bd849-521">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-521">**Description**</span></span>

<span data-ttu-id="bd849-522">Questo evento rappresenta il recupero delle informazioni sul pool di byte tramite tx_byte_pool_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-522">This event represents getting byte pool information via tx_byte_pool_info_get.</span></span>

<span data-ttu-id="bd849-523">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-523">**Information Fields**</span></span>

- <span data-ttu-id="bd849-524">Info Field 1: puntatore al pool di byte corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-524">Info Field 1: Pointer to the corresponding byte pool.</span></span>
- <span data-ttu-id="bd849-525">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-525">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-526">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-526">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-527">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-527">Info Field 4: Not used.</span></span>

### <a name="byte-pool-performance-info-get"></a><span data-ttu-id="bd849-528">Informazioni sulle prestazioni del pool di byte Get</span><span class="sxs-lookup"><span data-stu-id="bd849-528">Byte Pool Performance Info Get</span></span> 

#### <a name="tx_byte_pool_info_get"></a><span data-ttu-id="bd849-529">tx_byte_pool_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-529">tx_byte_pool_info_get</span></span>

<span data-ttu-id="bd849-530">**Icona** ![ di Icona Ottieni informazioni sulle prestazioni del pool di byte](./media/user-guide/tx-events/image19.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-530">**Icon** ![Byte pool performance info get icon](./media/user-guide/tx-events/image19.png)</span></span>

<span data-ttu-id="bd849-531">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-531">**Description**</span></span>

<span data-ttu-id="bd849-532">Questo evento rappresenta il recupero delle informazioni sulle prestazioni del pool di byte tramite tx_byte_pool_performance_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-532">This event represents getting byte pool performance information via tx_byte_pool_performance_info_get.</span></span>

<span data-ttu-id="bd849-533">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-533">**Information Fields**</span></span>

- <span data-ttu-id="bd849-534">Info Field 1: puntatore al pool di byte corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-534">Info Field 1: Pointer to the corresponding byte pool.</span></span>
- <span data-ttu-id="bd849-535">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-535">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-536">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-536">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-537">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-537">Info Field 4: Not used.</span></span>

### <a name="byte-pool-performance-system-info-get"></a><span data-ttu-id="bd849-538">Informazioni sul sistema di prestazioni del pool di byte Get</span><span class="sxs-lookup"><span data-stu-id="bd849-538">Byte Pool Performance System Info Get</span></span> 

#### <a name="tx_byte_pool_performance_system_info_get"></a><span data-ttu-id="bd849-539">tx_byte_pool_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-539">tx_byte_pool_performance_system_info_get</span></span>

<span data-ttu-id="bd849-540">**Icona** ![ di Icona di informazioni sul sistema di prestazioni del pool di byte](./media/user-guide/tx-events/image20.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-540">**Icon** ![Byte pool performance system info get icon](./media/user-guide/tx-events/image20.png)</span></span>

<span data-ttu-id="bd849-541">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-541">**Description**</span></span>

<span data-ttu-id="bd849-542">Questo evento rappresenta il recupero delle informazioni sul sistema delle prestazioni del pool di byte tramite tx_byte_pool_performance_system_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-542">This event represents getting byte pool performance system information via tx_byte_pool_performance_system_info_get.</span></span>

<span data-ttu-id="bd849-543">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-543">**Information Fields**</span></span>

- <span data-ttu-id="bd849-544">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-544">Info Field 1: Not used.</span></span>
- <span data-ttu-id="bd849-545">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-545">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-546">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-546">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-547">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-547">Info Field 4: Not used.</span></span>

### <a name="byte-pool-prioritize"></a><span data-ttu-id="bd849-548">Priorità del pool di byte</span><span class="sxs-lookup"><span data-stu-id="bd849-548">Byte Pool Prioritize</span></span>

#### <a name="tx_byte_pool_prioritize"></a><span data-ttu-id="bd849-549">tx_byte_pool_prioritize</span><span class="sxs-lookup"><span data-stu-id="bd849-549">tx_byte_pool_prioritize</span></span>

<span data-ttu-id="bd849-550">**Icona** ![ di Icona priorità pool di byte](./media/user-guide/tx-events/image21.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-550">**Icon** ![Byte pool prioritize icon](./media/user-guide/tx-events/image21.png)</span></span>

<span data-ttu-id="bd849-551">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-551">**Description**</span></span>

<span data-ttu-id="bd849-552">Questo evento rappresenta la priorità dell'elenco di sospensioni del pool di byte tramite tx_byte_pool_prioritize.</span><span class="sxs-lookup"><span data-stu-id="bd849-552">This event represents prioritizing the byte pool's suspension list via tx_byte_pool_prioritize.</span></span>

<span data-ttu-id="bd849-553">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-553">**Information Fields**</span></span>

- <span data-ttu-id="bd849-554">Info Field 1: puntatore al pool di byte corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-554">Info Field 1: Pointer to corresponding byte pool.</span></span>
- <span data-ttu-id="bd849-555">Campo informazioni 2: numero di thread attualmente sospesi nel pool di byte.</span><span class="sxs-lookup"><span data-stu-id="bd849-555">Info Field 2: Number of threads currently suspended on byte pool.</span></span>
- <span data-ttu-id="bd849-556">Informazioni sul campo 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-556">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-557">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-557">Info Field 4: Not used.</span></span>

### <a name="byte-release"></a><span data-ttu-id="bd849-558">Versione byte</span><span class="sxs-lookup"><span data-stu-id="bd849-558">Byte Release</span></span>

#### <a name="tx_byte_release"></a><span data-ttu-id="bd849-559">tx_byte_release</span><span class="sxs-lookup"><span data-stu-id="bd849-559">tx_byte_release</span></span>

<span data-ttu-id="bd849-560">**Icona** ![ di Icona versione byte](./media/user-guide/tx-events/image22.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-560">**Icon** ![Byte release icon](./media/user-guide/tx-events/image22.png)</span></span>

<span data-ttu-id="bd849-561">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-561">**Description**</span></span>

<span data-ttu-id="bd849-562">Questo evento rappresenta il rilascio di un blocco di memoria allocato da un pool di byte tramite tx_byte_release.</span><span class="sxs-lookup"><span data-stu-id="bd849-562">This event represents releasing a block of memory allocated from a byte pool via tx_byte_release.</span></span>

<span data-ttu-id="bd849-563">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-563">**Information Fields**</span></span>

- <span data-ttu-id="bd849-564">Info Field 1: puntatore al pool di byte corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-564">Info Field 1: Pointer to corresponding byte pool.</span></span>
- <span data-ttu-id="bd849-565">Informazioni sul campo 2: puntatore alla memoria del pool di byte allocata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bd849-565">Info Field 2: Pointer to previously allocated byte pool memory.</span></span>
- <span data-ttu-id="bd849-566">Campo info 3: numero di thread sospesi in questo pool di byte.</span><span class="sxs-lookup"><span data-stu-id="bd849-566">Info Field 3: Number of threads suspended on this byte pool.</span></span>
- <span data-ttu-id="bd849-567">Campo informazioni 4: numero di byte di memoria disponibili.</span><span class="sxs-lookup"><span data-stu-id="bd849-567">Info Field 4: Number of available bytes of memory.</span></span>

### <a name="event-flags-create"></a><span data-ttu-id="bd849-568">Creazione flag evento</span><span class="sxs-lookup"><span data-stu-id="bd849-568">Event Flags Create</span></span> 

#### <a name="tx_event_flags_create"></a><span data-ttu-id="bd849-569">tx_event_flags_create</span><span class="sxs-lookup"><span data-stu-id="bd849-569">tx_event_flags_create</span></span>

<span data-ttu-id="bd849-570">**Icona** ![ di Icona di creazione flag evento](./media/user-guide/tx-events/image23.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-570">**Icon** ![Event flags create icon](./media/user-guide/tx-events/image23.png)</span></span>

<span data-ttu-id="bd849-571">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-571">**Description**</span></span>

<span data-ttu-id="bd849-572">Questo evento rappresenta la creazione di un nuovo gruppo di flag di evento tramite tx_event_flags_create.</span><span class="sxs-lookup"><span data-stu-id="bd849-572">This event represents creating a new event flags group via tx_event_flags_create.</span></span>

<span data-ttu-id="bd849-573">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-573">**Information Fields**</span></span> 
- <span data-ttu-id="bd849-574">Info Field 1: puntatore al blocco di controllo del gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="bd849-574">Info Field 1: Pointer to event flags group control block.</span></span>
- <span data-ttu-id="bd849-575">Informazioni sul campo 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-575">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-576">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-576">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-577">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-577">Info Field 4: Not used.</span></span>

### <a name="event-flags-delete"></a><span data-ttu-id="bd849-578">Flag evento Delete</span><span class="sxs-lookup"><span data-stu-id="bd849-578">Event Flags Delete</span></span> 

#### <a name="tx_event_flags_delete"></a><span data-ttu-id="bd849-579">tx_event_flags_delete</span><span class="sxs-lookup"><span data-stu-id="bd849-579">tx_event_flags_delete</span></span>

<span data-ttu-id="bd849-580">**Icona** ![ di Icona di eliminazione flag evento](./media/user-guide/tx-events/image24.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-580">**Icon** ![Event flags delete icon](./media/user-guide/tx-events/image24.png)</span></span>

<span data-ttu-id="bd849-581">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-581">**Description**</span></span>

<span data-ttu-id="bd849-582">Questo evento rappresenta l'eliminazione di un gruppo di flag di evento tramite tx_event_flags_delete.</span><span class="sxs-lookup"><span data-stu-id="bd849-582">This event represents deleting an event flags group via tx_event_flags_delete.</span></span>

<span data-ttu-id="bd849-583">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-583">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-584">Info Field 1: puntatore al gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="bd849-584">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="bd849-585">Informazioni sul campo 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-585">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-586">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-586">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-587">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-587">Info Field 4: Not used.</span></span>

### <a name="event-flags-get"></a><span data-ttu-id="bd849-588">Flag evento Get</span><span class="sxs-lookup"><span data-stu-id="bd849-588">Event Flags Get</span></span> 

#### <a name="tx_event_flags_get"></a><span data-ttu-id="bd849-589">tx_event_flags_get</span><span class="sxs-lookup"><span data-stu-id="bd849-589">tx_event_flags_get</span></span>

<span data-ttu-id="bd849-590">**Icona** ![ di Icona flag evento gt](./media/user-guide/tx-events/image25.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-590">**Icon** ![Event flags gt icon](./media/user-guide/tx-events/image25.png)</span></span>

<span data-ttu-id="bd849-591">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-591">**Description**</span></span>

<span data-ttu-id="bd849-592">Questo evento rappresenta il recupero dei flag di evento da un gruppo di flag di evento esistente tramite tx_event_flags_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-592">This event represents retrieving event flags from an existing event flags group via tx_event_flags_get.</span></span>

<span data-ttu-id="bd849-593">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-593">**Information Fields**</span></span>

- <span data-ttu-id="bd849-594">Info Field 1: puntatore al gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="bd849-594">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="bd849-595">Campo informazioni 2: Flag evento richiesti.</span><span class="sxs-lookup"><span data-stu-id="bd849-595">Info Field 2: Event flags requested.</span></span>
- <span data-ttu-id="bd849-596">Info Field 3: flag di evento attualmente impostati nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="bd849-596">Info Field 3: Event flags currently set in the group.</span></span>
- <span data-ttu-id="bd849-597">Info Field 4: opzione richiesta sui flag di evento Get.</span><span class="sxs-lookup"><span data-stu-id="bd849-597">Info Field 4: Option requested on the event flags get.</span></span>

### <a name="event-flags-information-get"></a><span data-ttu-id="bd849-598">Informazioni sui flag evento Get</span><span class="sxs-lookup"><span data-stu-id="bd849-598">Event Flags Information Get</span></span>

#### <a name="tx_event_flags_info_get"></a><span data-ttu-id="bd849-599">tx_event_flags_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-599">tx_event_flags_info_get</span></span>

<span data-ttu-id="bd849-600">**Icona** ![ di Icona ottenere informazioni sui flag di evento](./media/user-guide/tx-events/image26.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-600">**Icon** ![Event flags information get icon](./media/user-guide/tx-events/image26.png)</span></span>

<span data-ttu-id="bd849-601">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-601">**Description**</span></span>

<span data-ttu-id="bd849-602">Questo evento rappresenta il recupero di informazioni relative a un gruppo di flag di evento esistente tramite tx_event_flags_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-602">This event represents retrieving information regarding an existing event flags group via tx_event_flags_info_get.</span></span>

<span data-ttu-id="bd849-603">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-603">**Information Fields**</span></span>

- <span data-ttu-id="bd849-604">Info Field 1: puntatore al gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="bd849-604">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="bd849-605">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-605">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-606">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-606">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-607">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-607">Info Field 4: Not used.</span></span>

### <a name="event-flags-performance-information-get"></a><span data-ttu-id="bd849-608">Flag evento informazioni sulle prestazioni Get</span><span class="sxs-lookup"><span data-stu-id="bd849-608">Event Flags Performance Information Get</span></span> 

#### <a name="tx_event_flags_performance_info_get"></a><span data-ttu-id="bd849-609">tx_event_flags_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-609">tx_event_flags_performance_info_get</span></span>

<span data-ttu-id="bd849-610">**Icona** ![ di Icona delle informazioni sulle prestazioni di flag di evento](./media/user-guide/tx-events/image27.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-610">**Icon** ![Event flags performance information get icon](./media/user-guide/tx-events/image27.png)</span></span>

<span data-ttu-id="bd849-611">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-611">**Description**</span></span>

<span data-ttu-id="bd849-612">Questo evento rappresenta il recupero delle informazioni sulle prestazioni relative a un gruppo di flag di evento esistente tramite tx_event_flags_performance_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-612">This event represents retrieving performance information regarding an existing event flags group via tx_event_flags_performance_info_get.</span></span>

<span data-ttu-id="bd849-613">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-613">**Information Fields**</span></span> 
- <span data-ttu-id="bd849-614">Info Field 1: puntatore al gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="bd849-614">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="bd849-615">Campo informazioni 2: non usato</span><span class="sxs-lookup"><span data-stu-id="bd849-615">Info Field 2: Not used</span></span>
- <span data-ttu-id="bd849-616">Campo info 3: non usato</span><span class="sxs-lookup"><span data-stu-id="bd849-616">Info Field 3: Not used</span></span>
- <span data-ttu-id="bd849-617">Campo informazioni 4: non usato</span><span class="sxs-lookup"><span data-stu-id="bd849-617">Info Field 4: Not Used</span></span>

### <a name="event-flags-performance-system-info-get"></a><span data-ttu-id="bd849-618">Flag evento prestazioni informazioni sistema Get</span><span class="sxs-lookup"><span data-stu-id="bd849-618">Event Flags Performance System Info Get</span></span>

#### <a name="tx_event_flags_performance_system_info_get"></a><span data-ttu-id="bd849-619">tx_event_flags_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-619">tx_event_flags_performance_system_info_get</span></span>

<span data-ttu-id="bd849-620">**Icona** ![ di Icona di informazioni sul sistema delle prestazioni flag di evento](./media/user-guide/tx-events/image28.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-620">**Icon** ![Event flags performance system info get icon](./media/user-guide/tx-events/image28.png)</span></span>

<span data-ttu-id="bd849-621">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-621">**Description**</span></span>

<span data-ttu-id="bd849-622">Questo evento rappresenta il recupero delle informazioni sulle prestazioni relative a un gruppo di flag di evento esistente tramite tx_event_flags_performance_system_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-622">This event represents retrieving performance information regarding an existing event flags group via tx_event_flags_performance_system_info_get.</span></span>

<span data-ttu-id="bd849-623">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-623">**Information Fields**</span></span>
- <span data-ttu-id="bd849-624">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-624">Info Field 1: Not used.</span></span>
- <span data-ttu-id="bd849-625">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-625">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-626">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-626">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-627">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-627">Info Field 4: Not used.</span></span>

### <a name="event-flags-set"></a><span data-ttu-id="bd849-628">Flag evento impostati</span><span class="sxs-lookup"><span data-stu-id="bd849-628">Event Flags Set</span></span> 

#### <a name="tx_event_flags_set"></a><span data-ttu-id="bd849-629">tx_event_flags_set</span><span class="sxs-lookup"><span data-stu-id="bd849-629">tx_event_flags_set</span></span>

<span data-ttu-id="bd849-630">**Icona** ![ di Icona set di flag evento](./media/user-guide/tx-events/image29.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-630">**Icon** ![Event flags set icon](./media/user-guide/tx-events/image29.png)</span></span>

<span data-ttu-id="bd849-631">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-631">**Description**</span></span>

<span data-ttu-id="bd849-632">Questo evento rappresenta l'impostazione o la cancellazione di flag di evento in un gruppo di flag di evento esistente tramite tx_event_flags_set.</span><span class="sxs-lookup"><span data-stu-id="bd849-632">This event represents setting (or clearing) event flags in an existing event flags group via tx_event_flags_set.</span></span>

<span data-ttu-id="bd849-633">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-633">**Information Fields**</span></span>

- <span data-ttu-id="bd849-634">Info Field 1: puntatore al gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="bd849-634">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="bd849-635">Informazioni sul campo 2: Flag evento da impostare o deselezionare.</span><span class="sxs-lookup"><span data-stu-id="bd849-635">Info Field 2: Event flags to set (or clear).</span></span>
- <span data-ttu-id="bd849-636">Informazioni sul campo 3: e o l'opzione del flag evento.</span><span class="sxs-lookup"><span data-stu-id="bd849-636">Info Field 3: AND or OR event flag option.</span></span>
- <span data-ttu-id="bd849-637">Campo informazioni 4: numero di thread sospesi nel gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="bd849-637">Info Field 4: Number of threads suspended on event flag group.</span></span>

### <a name="event-flags-set-notify"></a><span data-ttu-id="bd849-638">Notifica di impostazione flag evento</span><span class="sxs-lookup"><span data-stu-id="bd849-638">Event Flags Set Notify</span></span>

#### <a name="tx_event_flags_set_notify"></a><span data-ttu-id="bd849-639">tx_event_flags_set_notify</span><span class="sxs-lookup"><span data-stu-id="bd849-639">tx_event_flags_set_notify</span></span>

<span data-ttu-id="bd849-640">**Icona** ![ di Icona di impostazione notifica flag evento](./media/user-guide/tx-events/image30.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-640">**Icon** ![Event flags set notify icon](./media/user-guide/tx-events/image30.png)</span></span>

<span data-ttu-id="bd849-641">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-641">**Description**</span></span>

<span data-ttu-id="bd849-642">Questo evento rappresenta la registrazione di un callback di notifica per qualsiasi operazione di impostazione del flag evento su un gruppo di flag di evento esistente tramite tx_event_flags_set_notify.</span><span class="sxs-lookup"><span data-stu-id="bd849-642">This event represents registering a notification callback for any event flag set operation on an existing event flags group via tx_event_flags_set_notify.</span></span>

<span data-ttu-id="bd849-643">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-643">**Information Fields**</span></span>

- <span data-ttu-id="bd849-644">Info Field 1: puntatore al gruppo di flag di evento.</span><span class="sxs-lookup"><span data-stu-id="bd849-644">Info Field 1: Pointer to event flags group.</span></span>
- <span data-ttu-id="bd849-645">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-645">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-646">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-646">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-647">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-647">Info Field 4: Not used.</span></span>

### <a name="interrupt-control"></a><span data-ttu-id="bd849-648">Interrompi controllo</span><span class="sxs-lookup"><span data-stu-id="bd849-648">Interrupt Control</span></span> 

#### <a name="tx_interrupt_control"></a><span data-ttu-id="bd849-649">tx_interrupt_control</span><span class="sxs-lookup"><span data-stu-id="bd849-649">tx_interrupt_control</span></span>

<span data-ttu-id="bd849-650">**Icona** ![ di Icona di controllo interrupt](./media/user-guide/tx-events/image31.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-650">**Icon** ![Interrupt control icon](./media/user-guide/tx-events/image31.png)</span></span>

<span data-ttu-id="bd849-651">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-651">**Description**</span></span>

<span data-ttu-id="bd849-652">Questo evento rappresenta la modifica della postura di blocco di interrupt del processore tramite tx_interrupt_control.</span><span class="sxs-lookup"><span data-stu-id="bd849-652">This event represents changing the interrupt lockout posture of the processor via tx_interrupt_control.</span></span>

<span data-ttu-id="bd849-653">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-653">**Information Fields**</span></span>

- <span data-ttu-id="bd849-654">Campo informazioni 1: nuova postura interrupt.</span><span class="sxs-lookup"><span data-stu-id="bd849-654">Info Field 1: New interrupt posture.</span></span>
- <span data-ttu-id="bd849-655">Informazioni sul campo 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-655">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-656">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-656">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-657">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-657">Info Field 4: Not used.</span></span>

### <a name="mutex-create"></a><span data-ttu-id="bd849-658">Creazione mutex</span><span class="sxs-lookup"><span data-stu-id="bd849-658">Mutex Create</span></span> 

#### <a name="tx_mutex_create"></a><span data-ttu-id="bd849-659">tx_mutex_create</span><span class="sxs-lookup"><span data-stu-id="bd849-659">tx_mutex_create</span></span>

<span data-ttu-id="bd849-660">**Icona** ![ di Icona di creazione mutex](./media/user-guide/tx-events/image32.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-660">**Icon** ![Mutex create icon](./media/user-guide/tx-events/image32.png)</span></span>

<span data-ttu-id="bd849-661">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-661">**Description**</span></span>

<span data-ttu-id="bd849-662">Questo evento rappresenta la creazione di un mutex tramite tx_mutex_create.</span><span class="sxs-lookup"><span data-stu-id="bd849-662">This event represents creating a mutex via tx_mutex_create.</span></span>

<span data-ttu-id="bd849-663">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-663">**Information Fields**</span></span>

- <span data-ttu-id="bd849-664">Info Field 1: puntatore al blocco di controllo mutex.</span><span class="sxs-lookup"><span data-stu-id="bd849-664">Info Field 1: Pointer to mutex control block.</span></span>
- <span data-ttu-id="bd849-665">Informazioni campo 2: opzione ereditarietà priorità</span><span class="sxs-lookup"><span data-stu-id="bd849-665">Info Field 2: Priority inheritance option</span></span>
- <span data-ttu-id="bd849-666">(TX_INHERIT o TX_NO_INHERIT).</span><span class="sxs-lookup"><span data-stu-id="bd849-666">(TX_INHERIT or TX_NO_INHERIT).</span></span>
- <span data-ttu-id="bd849-667">Informazioni sul campo 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-667">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-668">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-668">Info Field 4: Not used.</span></span>

### <a name="mutex-delete"></a><span data-ttu-id="bd849-669">Eliminazione mutex</span><span class="sxs-lookup"><span data-stu-id="bd849-669">Mutex Delete</span></span> 

#### <a name="tx_mutex_delete"></a><span data-ttu-id="bd849-670">tx_mutex_delete</span><span class="sxs-lookup"><span data-stu-id="bd849-670">tx_mutex_delete</span></span>

<span data-ttu-id="bd849-671">**Icona** ![ di Icona di eliminazione mutex](./media/user-guide/tx-events/image33.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-671">**Icon** ![Mutex delete icon](./media/user-guide/tx-events/image33.png)</span></span>

<span data-ttu-id="bd849-672">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-672">**Description**</span></span>

<span data-ttu-id="bd849-673">Questo evento rappresenta l'eliminazione di un mutex tramite tx_mutex_delete.</span><span class="sxs-lookup"><span data-stu-id="bd849-673">This event represents deleting a mutex via tx_mutex_delete.</span></span>

<span data-ttu-id="bd849-674">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-674">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-675">Info Field 1: puntatore a mutex.</span><span class="sxs-lookup"><span data-stu-id="bd849-675">Info Field 1: Pointer to mutex.</span></span>
- <span data-ttu-id="bd849-676">Informazioni sul campo 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-676">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-677">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-677">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-678">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-678">Info Field 4: Not used.</span></span>

### <a name="mutex-get"></a><span data-ttu-id="bd849-679">Get mutex</span><span class="sxs-lookup"><span data-stu-id="bd849-679">Mutex Get</span></span> 

#### <a name="tx_mutex_get"></a><span data-ttu-id="bd849-680">tx_mutex_get</span><span class="sxs-lookup"><span data-stu-id="bd849-680">tx_mutex_get</span></span>

<span data-ttu-id="bd849-681">**Icona** ![ di Icona di Get mutex](./media/user-guide/tx-events/image34.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-681">**Icon** ![Mutex get icon](./media/user-guide/tx-events/image34.png)</span></span>

<span data-ttu-id="bd849-682">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-682">**Description**</span></span>

<span data-ttu-id="bd849-683">Questo evento rappresenta l'ottenimento di un mutex tramite tx_mutex_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-683">This event represents obtaining a mutex via tx_mutex_get.</span></span>

<span data-ttu-id="bd849-684">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-684">**Information Fields**</span></span>

- <span data-ttu-id="bd849-685">Info Field 1: puntatore a mutex.</span><span class="sxs-lookup"><span data-stu-id="bd849-685">Info Field 1: Pointer to mutex.</span></span>
- <span data-ttu-id="bd849-686">Info Field 2: l'opzione wait fornita alla chiamata tx_mutex_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-686">Info Field 2: The wait option supplied to the tx_mutex_get call.</span></span>
- <span data-ttu-id="bd849-687">Info Field 3: puntatore al thread proprietario del mutex (NULL implica che il mutex non è di proprietà).</span><span class="sxs-lookup"><span data-stu-id="bd849-687">Info Field 3: Pointer to thread that owns the mutex (NULL implies the mutex is not owned).</span></span>
- <span data-ttu-id="bd849-688">Campo info 4: numero di volte in cui il thread proprietario ha chiamato tx_mutex_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-688">Info Field 4: Number of times the owning thread has called tx_mutex_get.</span></span>

### <a name="mutex-information-get"></a><span data-ttu-id="bd849-689">Informazioni sul mutex Get</span><span class="sxs-lookup"><span data-stu-id="bd849-689">Mutex Information Get</span></span>

#### <a name="tx_mutex_info_get"></a><span data-ttu-id="bd849-690">tx_mutex_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-690">tx_mutex_info_get</span></span>

<span data-ttu-id="bd849-691">**Icona** ![ di Icona Ottieni informazioni mutex](./media/user-guide/tx-events/image35.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-691">**Icon** ![Mutex information get icon](./media/user-guide/tx-events/image35.png)</span></span>

<span data-ttu-id="bd849-692">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-692">**Description**</span></span>

<span data-ttu-id="bd849-693">Questo evento rappresenta il recupero delle informazioni mutex tramite tx_mutex_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-693">This event represents retrieving mutex information via tx_mutex_info_get.</span></span>

<span data-ttu-id="bd849-694">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-694">**Information Fields**</span></span>

- <span data-ttu-id="bd849-695">Info Field 1: puntatore a mutex.</span><span class="sxs-lookup"><span data-stu-id="bd849-695">Info Field 1: Pointer to mutex.</span></span>
- <span data-ttu-id="bd849-696">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-696">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-697">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-697">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-698">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-698">Info Field 4: Not used.</span></span>

### <a name="mutex-performance-information-get"></a><span data-ttu-id="bd849-699">Informazioni sulle prestazioni mutex Get</span><span class="sxs-lookup"><span data-stu-id="bd849-699">Mutex Performance Information Get</span></span> 

#### <a name="tx_mutex_performance_info_get"></a><span data-ttu-id="bd849-700">tx_mutex_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-700">tx_mutex_performance_info_get</span></span>

<span data-ttu-id="bd849-701">**Icona** ![ di Icona ottenere informazioni sulle prestazioni mutex](./media/user-guide/tx-events/image36.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-701">**Icon** ![Mutex performance information get icon](./media/user-guide/tx-events/image36.png)</span></span>

<span data-ttu-id="bd849-702">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-702">**Description**</span></span>

<span data-ttu-id="bd849-703">Questo evento rappresenta il recupero delle informazioni sulle prestazioni di mutex tramite tx_mutex_performance_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-703">This event represents retrieving mutex performance information via tx_mutex_performance_info_get.</span></span>

<span data-ttu-id="bd849-704">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-704">**Information Fields**</span></span>

- <span data-ttu-id="bd849-705">Info Field 1: puntatore a mutex.</span><span class="sxs-lookup"><span data-stu-id="bd849-705">Info Field 1: Pointer to mutex.</span></span>
- <span data-ttu-id="bd849-706">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-706">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-707">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-707">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-708">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-708">Info Field 4: Not used.</span></span>

### <a name="mutex-performance-system-info-get"></a><span data-ttu-id="bd849-709">Informazioni sul sistema delle prestazioni mutex Get</span><span class="sxs-lookup"><span data-stu-id="bd849-709">Mutex Performance System Info Get</span></span>

#### <a name="tx_mutex_performance_system_info_get"></a><span data-ttu-id="bd849-710">tx_mutex_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-710">tx_mutex_performance_system_info_get</span></span>

<span data-ttu-id="bd849-711">**Icona** ![ di Icona informazioni sul sistema di prestazioni mutex](./media/user-guide/tx-events/image37.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-711">**Icon** ![Mutex performance system info get icon](./media/user-guide/tx-events/image37.png)</span></span>

<span data-ttu-id="bd849-712">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-712">**Description**</span></span>

<span data-ttu-id="bd849-713">Questo evento rappresenta il recupero delle informazioni sulle prestazioni del sistema mutex tramite tx_mutex_performance_system_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-713">This event represents retrieving mutex system performance information via tx_mutex_performance_system_info_get.</span></span>

<span data-ttu-id="bd849-714">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-714">**Information Fields**</span></span>

- <span data-ttu-id="bd849-715">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-715">Info Field 1: Not used.</span></span>
- <span data-ttu-id="bd849-716">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-716">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-717">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-717">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-718">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-718">Info Field 4: Not used.</span></span>

### <a name="mutex-prioritize"></a><span data-ttu-id="bd849-719">Priorità mutex</span><span class="sxs-lookup"><span data-stu-id="bd849-719">Mutex Prioritize</span></span> 

#### <a name="tx_mutex_prioritize"></a><span data-ttu-id="bd849-720">tx_mutex_prioritize</span><span class="sxs-lookup"><span data-stu-id="bd849-720">tx_mutex_prioritize</span></span>

<span data-ttu-id="bd849-721">**Icona** ![ di Icona di priorità mutex](./media/user-guide/tx-events/image38.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-721">**Icon** ![Mutex prioritize icon](./media/user-guide/tx-events/image38.png)</span></span>

<span data-ttu-id="bd849-722">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-722">**Description**</span></span>

<span data-ttu-id="bd849-723">Questo evento rappresenta la priorità dell'elenco di sospensioni del mutex tramite tx_mutex_prioritize.</span><span class="sxs-lookup"><span data-stu-id="bd849-723">This event represents prioritizing the mutex's suspension list via tx_mutex_prioritize.</span></span>

<span data-ttu-id="bd849-724">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-724">**Information Fields**</span></span>

- <span data-ttu-id="bd849-725">Info Field 1: puntatore al mutex corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-725">Info Field 1: Pointer to corresponding mutex.</span></span>
- <span data-ttu-id="bd849-726">Campo informazioni 2: numero di thread attualmente sospesi sul mutex.</span><span class="sxs-lookup"><span data-stu-id="bd849-726">Info Field 2: Number of threads currently suspended on the mutex.</span></span>
- <span data-ttu-id="bd849-727">Informazioni sul campo 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-727">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-728">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-728">Info Field 4: Not used.</span></span>

### <a name="mutex-put"></a><span data-ttu-id="bd849-729">Mutex put</span><span class="sxs-lookup"><span data-stu-id="bd849-729">Mutex Put</span></span> 

#### <a name="tx_mutex_put"></a><span data-ttu-id="bd849-730">tx_mutex_put</span><span class="sxs-lookup"><span data-stu-id="bd849-730">tx_mutex_put</span></span>

<span data-ttu-id="bd849-731">**Icona** ![ di Icona put mutex](./media/user-guide/tx-events/image39.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-731">**Icon** ![Mutex put icon](./media/user-guide/tx-events/image39.png)</span></span>

<span data-ttu-id="bd849-732">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-732">**Description**</span></span>

<span data-ttu-id="bd849-733">Questo evento rappresenta il rilascio di un mutex di proprietà precedente tramite tx_mutex_put.</span><span class="sxs-lookup"><span data-stu-id="bd849-733">This event represents releasing a previously owned mutex via tx_mutex_put.</span></span>

<span data-ttu-id="bd849-734">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-734">**Information Fields**</span></span>

- <span data-ttu-id="bd849-735">Info Field 1: puntatore al mutex corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-735">Info Field 1: Pointer to corresponding mutex.</span></span>
- <span data-ttu-id="bd849-736">Info Field 2: puntatore del thread proprietario del mutex.</span><span class="sxs-lookup"><span data-stu-id="bd849-736">Info Field 2: Pointer of thread owning the mutex.</span></span>
- <span data-ttu-id="bd849-737">Campo info 3: numero di richieste Get mutex in attesa.</span><span class="sxs-lookup"><span data-stu-id="bd849-737">Info Field 3: Number of outstanding mutex get requests.</span></span>
- <span data-ttu-id="bd849-738">Informazioni sul campo 4: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-738">Info Field 4: Stack pointer at time of call.</span></span>

### <a name="queue-create"></a><span data-ttu-id="bd849-739">Creazione coda</span><span class="sxs-lookup"><span data-stu-id="bd849-739">Queue Create</span></span> 

#### <a name="tx_queue_create"></a><span data-ttu-id="bd849-740">tx_queue_create</span><span class="sxs-lookup"><span data-stu-id="bd849-740">tx_queue_create</span></span>

<span data-ttu-id="bd849-741">**Icona** ![ di Icona Crea coda](./media/user-guide/tx-events/image40.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-741">**Icon** ![Queue create icon](./media/user-guide/tx-events/image40.png)</span></span>

<span data-ttu-id="bd849-742">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-742">**Description**</span></span>

<span data-ttu-id="bd849-743">Questo evento rappresenta la creazione di una coda di messaggi tramite tx_queue_create.</span><span class="sxs-lookup"><span data-stu-id="bd849-743">This event represents creating a message queue via tx_queue_create.</span></span>

<span data-ttu-id="bd849-744">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-744">**Information Fields**</span></span>

- <span data-ttu-id="bd849-745">Info Field 1: puntatore al blocco di controllo Queue.</span><span class="sxs-lookup"><span data-stu-id="bd849-745">Info Field 1: Pointer to queue control block.</span></span>
- <span data-ttu-id="bd849-746">Informazioni sul campo 2: dimensioni del messaggio, in termini di parole a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="bd849-746">Info Field 2: Size of message – in terms of 32-bit words.</span></span>
- <span data-ttu-id="bd849-747">Info Field 3: puntatore all'avvio dell'area di memoria della coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-747">Info Field 3: Pointer to start of queue memory area.</span></span>
- <span data-ttu-id="bd849-748">Campo informazioni 4: numero di byte nell'area memoria coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-748">Info Field 4: Number of bytes in the queue memory area.</span></span>

### <a name="queue-delete"></a><span data-ttu-id="bd849-749">Elimina coda</span><span class="sxs-lookup"><span data-stu-id="bd849-749">Queue Delete</span></span> 

#### <a name="tx_queue_delete"></a><span data-ttu-id="bd849-750">tx_queue_delete</span><span class="sxs-lookup"><span data-stu-id="bd849-750">tx_queue_delete</span></span>

<span data-ttu-id="bd849-751">**Icona** ![ di Icona di eliminazione della coda](./media/user-guide/tx-events/image41.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-751">**Icon** ![Queue delete icon](./media/user-guide/tx-events/image41.png)</span></span>

<span data-ttu-id="bd849-752">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-752">**Description**</span></span>

<span data-ttu-id="bd849-753">Questo evento rappresenta l'eliminazione di una coda tramite tx_queue_delete.</span><span class="sxs-lookup"><span data-stu-id="bd849-753">This event represents deleting a queue via tx_queue_delete.</span></span>

<span data-ttu-id="bd849-754">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-754">**Information Fields**</span></span>

- <span data-ttu-id="bd849-755">Info Field 1: puntatore alla coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-755">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="bd849-756">Informazioni sul campo 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-756">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-757">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-757">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-758">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-758">Info Field 4: Not used.</span></span>

### <a name="queue-flush"></a><span data-ttu-id="bd849-759">Scaricamento coda</span><span class="sxs-lookup"><span data-stu-id="bd849-759">Queue Flush</span></span> 

#### <a name="tx_queue_flush"></a><span data-ttu-id="bd849-760">tx_queue_flush</span><span class="sxs-lookup"><span data-stu-id="bd849-760">tx_queue_flush</span></span>

<span data-ttu-id="bd849-761">**Icona** ![ di Icona di svuotamento della coda](./media/user-guide/tx-events/image42.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-761">**Icon** ![Queue flush icon](./media/user-guide/tx-events/image42.png)</span></span>

<span data-ttu-id="bd849-762">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-762">**Description**</span></span>

<span data-ttu-id="bd849-763">Questo evento rappresenta lo svuotamento (cancellazione di tutti i contenuti della coda) di una coda tramite tx_queue_flush.</span><span class="sxs-lookup"><span data-stu-id="bd849-763">This event represents flushing (clearing all queue contents) of a queue via tx_queue_flush.</span></span>

<span data-ttu-id="bd849-764">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-764">**Information Fields**</span></span>

- <span data-ttu-id="bd849-765">Info Field 1: puntatore alla coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-765">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="bd849-766">Informazioni sul campo 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-766">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-767">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-767">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-768">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-768">Info Field 4: Not used.</span></span>

### <a name="queue-front-send"></a><span data-ttu-id="bd849-769">Invio front-end della coda</span><span class="sxs-lookup"><span data-stu-id="bd849-769">Queue Front Send</span></span> 

#### <a name="tx_queue_front_send"></a><span data-ttu-id="bd849-770">tx_queue_front_send</span><span class="sxs-lookup"><span data-stu-id="bd849-770">tx_queue_front_send</span></span>

<span data-ttu-id="bd849-771">**Icona** ![ di Icona Invia coda in primo piano](./media/user-guide/tx-events/image43.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-771">**Icon** ![Queue front send icon](./media/user-guide/tx-events/image43.png)</span></span>

<span data-ttu-id="bd849-772">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-772">**Description**</span></span>

<span data-ttu-id="bd849-773">Questo evento rappresenta l'invio di un messaggio all'inizio di una coda tramite tx_queue_front_send.</span><span class="sxs-lookup"><span data-stu-id="bd849-773">This event represents sending a message to the front of a queue via tx_queue_front_send.</span></span>

<span data-ttu-id="bd849-774">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-774">**Information Fields**</span></span>

- <span data-ttu-id="bd849-775">Info Field 1: puntatore alla coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-775">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="bd849-776">Informazioni sul campo 2: puntatore all'avvio del messaggio.</span><span class="sxs-lookup"><span data-stu-id="bd849-776">Info Field 2: Pointer to start of message.</span></span>
- <span data-ttu-id="bd849-777">Informazioni sul campo 3: l'opzione wait fornita al</span><span class="sxs-lookup"><span data-stu-id="bd849-777">Info Field 3: Wait option supplied to the</span></span>
- <span data-ttu-id="bd849-778">chiamata tx_queue_front_send.</span><span class="sxs-lookup"><span data-stu-id="bd849-778">tx_queue_front_send call.</span></span>
- <span data-ttu-id="bd849-779">Campo informazioni 4: numero di messaggi già accodati.</span><span class="sxs-lookup"><span data-stu-id="bd849-779">Info Field 4: Number of messages already enqueued.</span></span>

### <a name="queue-information-get"></a><span data-ttu-id="bd849-780">Informazioni coda Get</span><span class="sxs-lookup"><span data-stu-id="bd849-780">Queue Information Get</span></span> 

#### <a name="tx_queue_info_get"></a><span data-ttu-id="bd849-781">tx_queue_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-781">tx_queue_info_get</span></span>

<span data-ttu-id="bd849-782">**Icona** ![ di Icona Ottieni informazioni sulla coda](./media/user-guide/tx-events/image44.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-782">**Icon** ![Queue information get icon](./media/user-guide/tx-events/image44.png)</span></span>

<span data-ttu-id="bd849-783">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-783">**Description**</span></span>

<span data-ttu-id="bd849-784">Questo evento rappresenta il recupero di informazioni su una coda tramite tx_queue_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-784">This event represents getting information about a queue via tx_queue_info_get.</span></span>

<span data-ttu-id="bd849-785">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-785">**Information Fields**</span></span> 
- <span data-ttu-id="bd849-786">Info Field 1: puntatore alla coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-786">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="bd849-787">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-787">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-788">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-788">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-789">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-789">Info Field 4: Not used.</span></span>

### <a name="queue-performance-info-get"></a><span data-ttu-id="bd849-790">Informazioni sulle prestazioni della coda Get</span><span class="sxs-lookup"><span data-stu-id="bd849-790">Queue Performance Info Get</span></span> 

#### <a name="tx_queue_performance_info_get"></a><span data-ttu-id="bd849-791">tx_queue_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-791">tx_queue_performance_info_get</span></span>

<span data-ttu-id="bd849-792">**Icona** ![ di Icona ottenere informazioni sulle prestazioni della coda](./media/user-guide/tx-events/image45.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-792">**Icon** ![Queue performance info get icon](./media/user-guide/tx-events/image45.png)</span></span>

<span data-ttu-id="bd849-793">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-793">**Description**</span></span>

<span data-ttu-id="bd849-794">Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni relative a una coda tramite tx_queue_performance_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-794">This event represents getting performance information about a queue via tx_queue_performance_info_get.</span></span>

<span data-ttu-id="bd849-795">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-795">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-796">Info Field 1: puntatore alla coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-796">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="bd849-797">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-797">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-798">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-798">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-799">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-799">Info Field 4: Not used.</span></span>

### <a name="queue-performance-system-info-get"></a><span data-ttu-id="bd849-800">Informazioni sul sistema di prestazioni della coda Get</span><span class="sxs-lookup"><span data-stu-id="bd849-800">Queue Performance System Info Get</span></span> 

#### <a name="tx_queue_performance_system_info_get"></a><span data-ttu-id="bd849-801">tx_queue_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-801">tx_queue_performance_system_info_get</span></span>

<span data-ttu-id="bd849-802">**Icona** ![ di Icona di informazioni sul sistema delle prestazioni della coda](./media/user-guide/tx-events/image46.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-802">**Icon** ![Queue performance system info get icon](./media/user-guide/tx-events/image46.png)</span></span>

<span data-ttu-id="bd849-803">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-803">**Description**</span></span>

<span data-ttu-id="bd849-804">Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni del sistema relative a tutte le code nel sistema.</span><span class="sxs-lookup"><span data-stu-id="bd849-804">This event represents getting system performance information about all the queues in the system.</span></span>

<span data-ttu-id="bd849-805">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-805">**Information Fields**</span></span>

- <span data-ttu-id="bd849-806">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-806">Info Field 1: Not used.</span></span>
- <span data-ttu-id="bd849-807">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-807">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-808">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-808">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-809">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-809">Info Field 4: Not used.</span></span>

### <a name="queue-prioritize"></a><span data-ttu-id="bd849-810">Priorità coda</span><span class="sxs-lookup"><span data-stu-id="bd849-810">Queue Prioritize</span></span> 

#### <a name="tx_queue_prioritize"></a><span data-ttu-id="bd849-811">tx_queue_prioritize</span><span class="sxs-lookup"><span data-stu-id="bd849-811">tx_queue_prioritize</span></span>

<span data-ttu-id="bd849-812">**Icona** ![ di Icona Accodamento priorità](./media/user-guide/tx-events/image47.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-812">**Icon** ![Queue prioritize icon](./media/user-guide/tx-events/image47.png)</span></span>

<span data-ttu-id="bd849-813">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-813">**Description**</span></span>

<span data-ttu-id="bd849-814">Questo evento rappresenta la priorità dell'elenco di sospensione della coda tramite tx_queue_prioritize.</span><span class="sxs-lookup"><span data-stu-id="bd849-814">This event represents prioritizing the queue's suspension list via tx_queue_prioritize.</span></span>

<span data-ttu-id="bd849-815">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-815">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-816">Info Field 1: puntatore alla coda corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-816">Info Field 1: Pointer to corresponding queue.</span></span>
- <span data-ttu-id="bd849-817">Campo informazioni 2: numero di thread attualmente sospesi nella coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-817">Info Field 2: Number of threads currently suspended on the queue.</span></span>
- <span data-ttu-id="bd849-818">Informazioni sul campo 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-818">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-819">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-819">Info Field 4: Not used.</span></span>

#### <a name="queue-receive"></a><span data-ttu-id="bd849-820">Ricezione coda</span><span class="sxs-lookup"><span data-stu-id="bd849-820">Queue Receive</span></span> 

##### <a name="tx_queue_receive"></a><span data-ttu-id="bd849-821">tx_queue_receive</span><span class="sxs-lookup"><span data-stu-id="bd849-821">tx_queue_receive</span></span>

<span data-ttu-id="bd849-822">**Icona** ![ di Icona di ricezione della coda](./media/user-guide/tx-events/image48.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-822">**Icon** ![Queue receive icon](./media/user-guide/tx-events/image48.png)</span></span>

<span data-ttu-id="bd849-823">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-823">**Description**</span></span>

<span data-ttu-id="bd849-824">Questo evento rappresenta la ricezione di un messaggio da una coda tramite tx_queue_receive.</span><span class="sxs-lookup"><span data-stu-id="bd849-824">This event represents receiving a message from a queue via tx_queue_receive.</span></span>

<span data-ttu-id="bd849-825">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-825">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-826">Info Field 1: puntatore alla coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-826">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="bd849-827">Informazioni sul campo 2: puntatore alla destinazione per il messaggio.</span><span class="sxs-lookup"><span data-stu-id="bd849-827">Info Field 2: Pointer to destination for message.</span></span> <span data-ttu-id="bd849-828">Info Field 3: opzione wait fornita alla chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-828">Info Field 3: Wait option supplied to the call.</span></span>
- <span data-ttu-id="bd849-829">Campo informazioni 4: numero di messaggi attualmente in coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-829">Info Field 4: Number of messages currently queued.</span></span>

### <a name="queue-send"></a><span data-ttu-id="bd849-830">Coda Invio</span><span class="sxs-lookup"><span data-stu-id="bd849-830">Queue Send</span></span> 

#### <a name="tx_queue_send"></a><span data-ttu-id="bd849-831">tx_queue_send</span><span class="sxs-lookup"><span data-stu-id="bd849-831">tx_queue_send</span></span>

<span data-ttu-id="bd849-832">**Icona** ![ di Icona Invia coda](./media/user-guide/tx-events/image49.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-832">**Icon** ![Queue send icon](./media/user-guide/tx-events/image49.png)</span></span>

<span data-ttu-id="bd849-833">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-833">**Description**</span></span>

<span data-ttu-id="bd849-834">Questo evento rappresenta l'invio di un messaggio a una coda tramite tx_queue_send.</span><span class="sxs-lookup"><span data-stu-id="bd849-834">This event represents sending a message to a queue via tx_queue_send.</span></span>

<span data-ttu-id="bd849-835">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-835">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-836">Info Field 1: puntatore alla coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-836">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="bd849-837">Informazioni sul campo 2: puntatore al messaggio.</span><span class="sxs-lookup"><span data-stu-id="bd849-837">Info Field 2: Pointer to message.</span></span>
- <span data-ttu-id="bd849-838">Info Field 3: opzione wait fornita alla chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-838">Info Field 3: Wait option supplied to the call.</span></span>
- <span data-ttu-id="bd849-839">Campo informazioni 4: numero di messaggi attualmente in coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-839">Info Field 4: Number of messages currently queued.</span></span>

### <a name="queue-send-notify"></a><span data-ttu-id="bd849-840">Notifica invio coda</span><span class="sxs-lookup"><span data-stu-id="bd849-840">Queue Send Notify</span></span> 

#### <a name="tx_queue_send_notify"></a><span data-ttu-id="bd849-841">tx_queue_send_notify</span><span class="sxs-lookup"><span data-stu-id="bd849-841">tx_queue_send_notify</span></span>

<span data-ttu-id="bd849-842">**Icona** ![ di Icona Invia notifica coda](./media/user-guide/tx-events/image50.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-842">**Icon** ![Queue send notify icon](./media/user-guide/tx-events/image50.png)</span></span>

<span data-ttu-id="bd849-843">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-843">**Description**</span></span>

<p><span data-ttu-id="bd849-844">Questo evento rappresenta la registrazione di un callback tramite tx_queue_send_notify, che viene chiamato ogni volta che un messaggio viene inviato a una coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-844">This event represents registering a callback via tx_queue_send_notify which is called whenever a message is sent to a queue.</span></span>

<span data-ttu-id="bd849-845">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-845">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-846">Info Field 1: puntatore alla coda.</span><span class="sxs-lookup"><span data-stu-id="bd849-846">Info Field 1: Pointer to queue.</span></span>
- <span data-ttu-id="bd849-847">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-847">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-848">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-848">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-849">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-849">Info Field 4: Not used.</span></span>

### <a name="semaphore-ceiling-put"></a><span data-ttu-id="bd849-850">Soffitto semaforo put</span><span class="sxs-lookup"><span data-stu-id="bd849-850">Semaphore Ceiling Put</span></span> 

#### <a name="tx_semaphore_ceiling_put"></a><span data-ttu-id="bd849-851">tx_semaphore_ceiling_put</span><span class="sxs-lookup"><span data-stu-id="bd849-851">tx_semaphore_ceiling_put</span></span>

<span data-ttu-id="bd849-852">**Icona** ![ di Icona put soffitto semaforo](./media/user-guide/tx-events/image51.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-852">**Icon** ![Semaphore ceiling put icon](./media/user-guide/tx-events/image51.png)</span></span>

<span data-ttu-id="bd849-853">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-853">**Description**</span></span>

<span data-ttu-id="bd849-854">Questo evento rappresenta l'inserimento in un semaforo tramite tx_semaphore_ceiling_put.</span><span class="sxs-lookup"><span data-stu-id="bd849-854">This event represents putting to a semaphore via tx_semaphore_ceiling_put.</span></span> <span data-ttu-id="bd849-855">Questo comportamento è diverso da quello tx_semaphore_put in quanto il valore massimo del semaforo viene esaminato in modo che l'operazione PUT non consentisca di superare il valore massimo o il limite massimo.</span><span class="sxs-lookup"><span data-stu-id="bd849-855">This differs from tx_semaphore_put in that the maximum value of the semaphore is examined such that the put operation is not allowed to exceed the maximum value or ceiling.</span></span>

<span data-ttu-id="bd849-856">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-856">**Information Fields**</span></span>

- <span data-ttu-id="bd849-857">Informazioni sul campo 1: puntatore al semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-857">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="bd849-858">Informazioni sul campo 2: conteggio corrente del semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-858">Info Field 2: Current semaphore count.</span></span>
- <span data-ttu-id="bd849-859">Campo info 3: numero di thread sospesi sul semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-859">Info Field 3: Number of threads suspended on the semaphore.</span></span>
- <span data-ttu-id="bd849-860">Informazioni sul campo 4: limite massimo fornito alla chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-860">Info Field 4: Ceiling limit supplied to the call.</span></span>

#### <a name="semaphore-create"></a><span data-ttu-id="bd849-861">Creazione semaforo</span><span class="sxs-lookup"><span data-stu-id="bd849-861">Semaphore Create</span></span> 

##### <a name="tx_semaphore_create"></a><span data-ttu-id="bd849-862">tx_semaphore_create</span><span class="sxs-lookup"><span data-stu-id="bd849-862">tx_semaphore_create</span></span>

<span data-ttu-id="bd849-863">**Icona** ![ di Icona Crea semaforo](./media/user-guide/tx-events/image52.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-863">**Icon** ![Semaphore create icon](./media/user-guide/tx-events/image52.png)</span></span>

<span data-ttu-id="bd849-864">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-864">**Description**</span></span>

<span data-ttu-id="bd849-865">Questo evento rappresenta la creazione di un semaforo tramite tx_semaphore_create.</span><span class="sxs-lookup"><span data-stu-id="bd849-865">This event represents creating a semaphore via tx_semaphore_create.</span></span>

<span data-ttu-id="bd849-866">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-866">**Information Fields**</span></span>

- <span data-ttu-id="bd849-867">Info Field 1: puntatore al blocco di controllo Semaphore.</span><span class="sxs-lookup"><span data-stu-id="bd849-867">Info Field 1: Pointer to semaphore control block.</span></span>
- <span data-ttu-id="bd849-868">Informazioni sul campo 2: conteggio iniziale del semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-868">Info Field 2: Initial semaphore count.</span></span>
- <span data-ttu-id="bd849-869">Informazioni sul campo 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-869">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-870">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-870">Info Field 4: Not used.</span></span>

### <a name="semaphore-delete"></a><span data-ttu-id="bd849-871">Eliminazione del semaforo</span><span class="sxs-lookup"><span data-stu-id="bd849-871">Semaphore Delete</span></span> 

#### <a name="tx_semaphore_delete"></a><span data-ttu-id="bd849-872">tx_semaphore_delete</span><span class="sxs-lookup"><span data-stu-id="bd849-872">tx_semaphore_delete</span></span>

<span data-ttu-id="bd849-873">**Icona** ![ di Icona Elimina semaforo](./media/user-guide/tx-events/image53.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-873">**Icon** ![Semaphore delete icon](./media/user-guide/tx-events/image53.png)</span></span>

<span data-ttu-id="bd849-874">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-874">**Description**</span></span>

<span data-ttu-id="bd849-875">Questo evento rappresenta l'eliminazione di un semaforo tramite tx_semaphore_delete.</span><span class="sxs-lookup"><span data-stu-id="bd849-875">This event represents deleting a semaphore via tx_semaphore_delete.</span></span>

<span data-ttu-id="bd849-876">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-876">**Information Fields**</span></span>

- <span data-ttu-id="bd849-877">Informazioni sul campo 1: puntatore al semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-877">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="bd849-878">NFO Field 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-878">nfo Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-879">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-879">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-880">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-880">Info Field 4: Not used.</span></span>

### <a name="semaphore-get"></a><span data-ttu-id="bd849-881">Semaforo Get</span><span class="sxs-lookup"><span data-stu-id="bd849-881">Semaphore Get</span></span> 

#### <a name="tx_semaphore_get"></a><span data-ttu-id="bd849-882">tx_semaphore_get</span><span class="sxs-lookup"><span data-stu-id="bd849-882">tx_semaphore_get</span></span>

<span data-ttu-id="bd849-883">**Icona** ![ di Icona Get semaforo](./media/user-guide/tx-events/image54.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-883">**Icon** ![Semaphore get icon](./media/user-guide/tx-events/image54.png)</span></span>

<span data-ttu-id="bd849-884">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-884">**Description**</span></span>

<span data-ttu-id="bd849-885">Questo evento rappresenta l'ottenimento di un semaforo tramite tx_semaphore_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-885">This event represents obtaining a semaphore via tx_semaphore_get.</span></span>

<span data-ttu-id="bd849-886">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-886">**Information Fields**</span></span>

- <span data-ttu-id="bd849-887">Informazioni sul campo 1: puntatore al semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-887">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="bd849-888">Info Field 2: opzione wait fornita alla chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-888">Info Field 2: Wait option supplied to the call.</span></span>
- <span data-ttu-id="bd849-889">Informazioni sul campo 3: conteggio corrente del semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-889">Info Field 3: Current semaphore count.</span></span>
- <span data-ttu-id="bd849-890">Informazioni sul campo 4: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-890">Info Field 4: Stack pointer at time of call.</span></span>

### <a name="semaphore-information-get"></a><span data-ttu-id="bd849-891">Informazioni sul semaforo Get</span><span class="sxs-lookup"><span data-stu-id="bd849-891">Semaphore Information Get</span></span> 

#### <a name="tx_semaphore_info_get"></a><span data-ttu-id="bd849-892">tx_semaphore_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-892">tx_semaphore_info_get</span></span>

<span data-ttu-id="bd849-893">**Icona** ![ di Icona ottenere informazioni sul semaforo](./media/user-guide/tx-events/image55.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-893">**Icon** ![Semaphore information get icon](./media/user-guide/tx-events/image55.png)</span></span>

<span data-ttu-id="bd849-894">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-894">**Description**</span></span>

<span data-ttu-id="bd849-895">Questo evento rappresenta l'ottenimento di informazioni su un semaforo tramite tx_semaphore_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-895">This event represents obtaining information about a semaphore via tx_semaphore_info_get.</span></span>

<span data-ttu-id="bd849-896">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-896">**Information Fields**</span></span>

- <span data-ttu-id="bd849-897">Informazioni sul campo 1: puntatore al semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-897">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="bd849-898">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-898">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-899">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-899">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-900">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-900">Info Field 4: Not used.</span></span>

### <a name="semaphore-performance-info-get"></a><span data-ttu-id="bd849-901">Informazioni sulle prestazioni del semaforo Get</span><span class="sxs-lookup"><span data-stu-id="bd849-901">Semaphore Performance Info Get</span></span> 

#### <a name="tx_semaphore_performance_info_get"></a><span data-ttu-id="bd849-902">tx_semaphore_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-902">tx_semaphore_performance_info_get</span></span>

<span data-ttu-id="bd849-903">**Icona** ![ di Icona delle informazioni sulle prestazioni del semaforo](./media/user-guide/tx-events/image56.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-903">**Icon** ![Semaphore performance info get icon](./media/user-guide/tx-events/image56.png)</span></span>

<span data-ttu-id="bd849-904">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-904">**Description**</span></span>

<span data-ttu-id="bd849-905">Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni relative a un semaforo tramite tx_semaphore_performance_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-905">This event represents obtaining performance information about a semaphore via tx_semaphore_performance_info_get.</span></span>

<span data-ttu-id="bd849-906">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-906">**Information Fields**</span></span>

- <span data-ttu-id="bd849-907">Informazioni sul campo 1: puntatore al semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-907">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="bd849-908">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-908">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-909">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-909">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-910">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-910">Info Field 4: Not used.</span></span>

### <a name="semaphore-performance-system-info"></a><span data-ttu-id="bd849-911">Informazioni sul sistema di prestazioni del semaforo</span><span class="sxs-lookup"><span data-stu-id="bd849-911">Semaphore Performance System Info</span></span> 

#### <a name="tx_semaphore_performance_system_info_get"></a><span data-ttu-id="bd849-912">tx_semaphore_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-912">tx_semaphore_performance_system_info_get</span></span>

<span data-ttu-id="bd849-913">**Icona** ![ di Icona informazioni sistema prestazioni semaforo](./media/user-guide/tx-events/image57.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-913">**Icon** ![Semaphore performance system info icon](./media/user-guide/tx-events/image57.png)</span></span>

<span data-ttu-id="bd849-914">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-914">**Description**</span></span>

<span data-ttu-id="bd849-915">Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni relative a tutti i semafori del sistema tramite tx_semaphore_performance_system_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-915">This event represents obtaining performance information about all semaphores in the system via tx_semaphore_performance_system_info_get.</span></span>

<span data-ttu-id="bd849-916">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-916">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-917">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-917">Info Field 1: Not used.</span></span>
- <span data-ttu-id="bd849-918">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-918">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-919">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-919">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-920">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-920">Info Field 4: Not used.</span></span>

### <a name="semaphore-prioritize"></a><span data-ttu-id="bd849-921">Priorità del semaforo</span><span class="sxs-lookup"><span data-stu-id="bd849-921">Semaphore Prioritize</span></span> 

#### <a name="tx_semaphore_prioritize"></a><span data-ttu-id="bd849-922">tx_semaphore_prioritize</span><span class="sxs-lookup"><span data-stu-id="bd849-922">tx_semaphore_prioritize</span></span>

<span data-ttu-id="bd849-923">**Icona** ![ di Icona priorità semaforo](./media/user-guide/tx-events/image58.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-923">**Icon** ![Semaphore prioritize icon](./media/user-guide/tx-events/image58.png)</span></span>

<span data-ttu-id="bd849-924">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-924">**Description**</span></span>

<span data-ttu-id="bd849-925">Questo evento rappresenta la priorità dell'elenco di sospensioni del semaforo tramite tx_semaphore_prioritize.</span><span class="sxs-lookup"><span data-stu-id="bd849-925">This event represents prioritizing the semaphore's suspension list via tx_semaphore_prioritize.</span></span>

<span data-ttu-id="bd849-926">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-926">**Information Fields**</span></span>

- <span data-ttu-id="bd849-927">Info Field 1: puntatore al semaforo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-927">Info Field 1: Pointer to corresponding semaphore.</span></span>
- <span data-ttu-id="bd849-928">Campo informazioni 2: numero di thread attualmente sospesi sul semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-928">Info Field 2: Number of threads currently suspended on the semaphore.</span></span>
- <span data-ttu-id="bd849-929">Informazioni sul campo 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-929">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-930">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-930">Info Field 4: Not used.</span></span>

### <a name="semaphore-put"></a><span data-ttu-id="bd849-931">Semaforo put</span><span class="sxs-lookup"><span data-stu-id="bd849-931">Semaphore Put</span></span> 

#### <a name="tx_semaphore_put"></a><span data-ttu-id="bd849-932">tx_semaphore_put</span><span class="sxs-lookup"><span data-stu-id="bd849-932">tx_semaphore_put</span></span>

<span data-ttu-id="bd849-933">**Icona** ![ di Icona put del semaforo](./media/user-guide/tx-events/image59.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-933">**Icon** ![Semaphore put icon](./media/user-guide/tx-events/image59.png)</span></span>

<span data-ttu-id="bd849-934">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-934">**Description**</span></span>

<span data-ttu-id="bd849-935">Questo evento rappresenta il rilascio di un'istanza del semaforo tramite tx_semaphore_put.</span><span class="sxs-lookup"><span data-stu-id="bd849-935">This event represents releasing a semaphore instance via tx_semaphore_put.</span></span>

<span data-ttu-id="bd849-936">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-936">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-937">Info Field 1: puntatore al semaforo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd849-937">Info Field 1: Pointer to corresponding semaphore.</span></span> <span data-ttu-id="bd849-938">Informazioni sul campo 2: conteggio corrente del semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-938">Info Field 2: Current semaphore count.</span></span>
- <span data-ttu-id="bd849-939">Campo info 3: numero di thread sospesi sul semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-939">Info Field 3: Number of threads suspended on the semaphore.</span></span>
- <span data-ttu-id="bd849-940">Informazioni sul campo 4: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-940">Info Field 4: Stack pointer at time of call.</span></span>

### <a name="semaphore-put-notify"></a><span data-ttu-id="bd849-941">Notifica put semaforo</span><span class="sxs-lookup"><span data-stu-id="bd849-941">Semaphore Put Notify</span></span> 

#### <a name="tx_semaphore_put_notify"></a><span data-ttu-id="bd849-942">tx_semaphore_put_notify</span><span class="sxs-lookup"><span data-stu-id="bd849-942">tx_semaphore_put_notify</span></span>

<span data-ttu-id="bd849-943">**Icona** ![ di Icona di notifica put del semaforo](./media/user-guide/tx-events/image60.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-943">**Icon** ![Semaphore put notify icon](./media/user-guide/tx-events/image60.png)</span></span>

<span data-ttu-id="bd849-944">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-944">**Description**</span></span>

<span data-ttu-id="bd849-945">Questo evento rappresenta la registrazione di un callback tramite tx_semaphore_put_notify chiamato ogni volta che viene inserita un'istanza del semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-945">This event represents registering a callback via tx_semaphore_put_notify that is called whenever a semaphore instance is put.</span></span>

<span data-ttu-id="bd849-946">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-946">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-947">Informazioni sul campo 1: puntatore al semaforo.</span><span class="sxs-lookup"><span data-stu-id="bd849-947">Info Field 1: Pointer to semaphore.</span></span>
- <span data-ttu-id="bd849-948">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-948">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-949">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-949">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-950">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-950">Info Field 4: Not used.</span></span>

### <a name="thread-create"></a><span data-ttu-id="bd849-951">Creazione thread</span><span class="sxs-lookup"><span data-stu-id="bd849-951">Thread Create</span></span> 

#### <a name="tx_thread_create"></a><span data-ttu-id="bd849-952">tx_thread_create</span><span class="sxs-lookup"><span data-stu-id="bd849-952">tx_thread_create</span></span>

<span data-ttu-id="bd849-953">**Icona** ![ di Icona Creazione thread](./media/user-guide/tx-events/image61.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-953">**Icon** ![Thread create icon](./media/user-guide/tx-events/image61.png)</span></span>

<span data-ttu-id="bd849-954">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-954">**Description**</span></span>

<span data-ttu-id="bd849-955">Questo evento rappresenta la creazione di un thread tramite tx_thread_create.</span><span class="sxs-lookup"><span data-stu-id="bd849-955">This event represents creating a thread via tx_thread_create.</span></span>

<span data-ttu-id="bd849-956">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-956">**Information Fields**</span></span>

- <span data-ttu-id="bd849-957">Info Field 1: puntatore al blocco di controllo thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-957">Info Field 1: Pointer to thread control block.</span></span>
- <span data-ttu-id="bd849-958">Informazioni sul campo 2: priorità del thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-958">Info Field 2: Priority of thread.</span></span>
- <span data-ttu-id="bd849-959">Informazioni sul campo 3: puntatore dello stack per il thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-959">Info Field 3: Stack pointer for thread.</span></span>
- <span data-ttu-id="bd849-960">NFO Field 4: dimensioni dello stack in byte.</span><span class="sxs-lookup"><span data-stu-id="bd849-960">nfo Field 4: Size of stack in bytes.</span></span>

### <a name="thread-delete"></a><span data-ttu-id="bd849-961">Eliminazione thread</span><span class="sxs-lookup"><span data-stu-id="bd849-961">Thread Delete</span></span> 

#### <a name="tx_thread_delete"></a><span data-ttu-id="bd849-962">tx_thread_delete</span><span class="sxs-lookup"><span data-stu-id="bd849-962">tx_thread_delete</span></span>

<span data-ttu-id="bd849-963">**Icona** ![ di Icona di eliminazione thread](./media/user-guide/tx-events/image62.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-963">**Icon** ![Thread delete icon](./media/user-guide/tx-events/image62.png)</span></span>

<span data-ttu-id="bd849-964">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-964">**Description**</span></span>

<span data-ttu-id="bd849-965">Questo evento rappresenta l'eliminazione di un thread tramite tx_thread_delete.</span><span class="sxs-lookup"><span data-stu-id="bd849-965">This event represents deleting a thread via tx_thread_delete.</span></span>

<span data-ttu-id="bd849-966">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-966">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-967">Info Field 1: puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-967">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="bd849-968">Informazioni sul campo 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-968">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-969">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-969">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-970">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-970">Info Field 4: Not used.</span></span>

### <a name="thread-entryexit-notify"></a><span data-ttu-id="bd849-971">Notifica voce/uscita thread</span><span class="sxs-lookup"><span data-stu-id="bd849-971">Thread Entry/Exit Notify</span></span> 

#### <a name="tx_thread_entry_exit_notify"></a><span data-ttu-id="bd849-972">tx_thread_entry_exit_notify</span><span class="sxs-lookup"><span data-stu-id="bd849-972">tx_thread_entry_exit_notify</span></span>

<span data-ttu-id="bd849-973">**Icona** ![ di Icona di immissione/chiusura del thread](./media/user-guide/tx-events/image63.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-973">**Icon** ![Thread entry/exit notify icon](./media/user-guide/tx-events/image63.png)</span></span>

<span data-ttu-id="bd849-974">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-974">**Description**</span></span>

<span data-ttu-id="bd849-975">Questo evento rappresenta la registrazione di un callback tramite tx_thread_entry_exit_notify chiamato ogni volta che un thread viene inserito o chiuso.</span><span class="sxs-lookup"><span data-stu-id="bd849-975">This event represents registering a callback via tx_thread_entry_exit_notify that is called whenever a thread is entered or exits.</span></span>

<span data-ttu-id="bd849-976">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-976">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-977">Info Field 1: puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-977">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="bd849-978">Informazioni sul campo 2: stato del thread al momento della registrazione.</span><span class="sxs-lookup"><span data-stu-id="bd849-978">Info Field 2: Thread state at time of the registration.</span></span>
- <span data-ttu-id="bd849-979">Informazioni sul campo 3: puntatore allo stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-979">Info Field 3: Pointer to stack at time of call.</span></span>
- <span data-ttu-id="bd849-980">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-980">Info Field 4: Not used.</span></span>

#### <a name="thread-identify"></a><span data-ttu-id="bd849-981">Identificazione thread</span><span class="sxs-lookup"><span data-stu-id="bd849-981">Thread Identify</span></span> 

##### <a name="tx_thread_identify"></a><span data-ttu-id="bd849-982">tx_thread_identify</span><span class="sxs-lookup"><span data-stu-id="bd849-982">tx_thread_identify</span></span>

<span data-ttu-id="bd849-983">**Icona** ![ di Icona di identificazione del thread](./media/user-guide/tx-events/image64.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-983">**Icon** ![Thread identify icon](./media/user-guide/tx-events/image64.png)</span></span>

<span data-ttu-id="bd849-984">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-984">**Description**</span></span>

<span data-ttu-id="bd849-985">Questo evento rappresenta il recupero del puntatore al thread corrente tramite tx_thread_identify.</span><span class="sxs-lookup"><span data-stu-id="bd849-985">This event represents getting the current thread pointer via tx_thread_identify.</span></span>

<span data-ttu-id="bd849-986">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-986">**Information Fields**</span></span>

- <span data-ttu-id="bd849-987">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-987">Info Field 1: Not used.</span></span>
- <span data-ttu-id="bd849-988">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-988">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-989">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-989">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-990">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-990">Info Field 4: Not used.</span></span>

### <a name="thread-information-get"></a><span data-ttu-id="bd849-991">Informazioni sul thread Get</span><span class="sxs-lookup"><span data-stu-id="bd849-991">Thread Information Get</span></span> 

#### <a name="tx_thread_info_get"></a><span data-ttu-id="bd849-992">tx_thread_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-992">tx_thread_info_get</span></span>

<span data-ttu-id="bd849-993">**Icona** ![ di Icona ottenere informazioni sul thread](./media/user-guide/tx-events/image65.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-993">**Icon** ![Thread information get icon](./media/user-guide/tx-events/image65.png)</span></span>

<span data-ttu-id="bd849-994">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-994">**Description**</span></span>

<span data-ttu-id="bd849-995">Questo evento rappresenta l'acquisizione di informazioni sul thread specificato tramite tx_thread_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-995">This event represents getting information about the specified thread via tx_thread_info_get.</span></span>

<span data-ttu-id="bd849-996">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-996">**Information Fields**</span></span>

- <span data-ttu-id="bd849-997">Info Field 1: puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-997">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="bd849-998">Informazioni sul campo 2: stato del thread al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-998">Info Field 2: State of thread at time of call.</span></span>
- <span data-ttu-id="bd849-999">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-999">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1000">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1000">Info Field 4: Not used.</span></span>

#### <a name="thread-performance-information-get"></a><span data-ttu-id="bd849-1001">Informazioni sulle prestazioni del thread Get</span><span class="sxs-lookup"><span data-stu-id="bd849-1001">Thread Performance Information Get</span></span> 

##### <a name="tx_thread_performance_info_get"></a><span data-ttu-id="bd849-1002">tx_thread_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-1002">tx_thread_performance_info_get</span></span>

<span data-ttu-id="bd849-1003">**Icona** ![ di Icona ottenere informazioni sulle prestazioni del thread](./media/user-guide/tx-events/image66.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1003">**Icon** ![Thread performance information get icon](./media/user-guide/tx-events/image66.png)</span></span>

<span data-ttu-id="bd849-1004">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1004">**Description**</span></span>

<span data-ttu-id="bd849-1005">Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni relative al thread specificato tramite tx_thread_performance_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-1005">This event represents getting performance information about the specified thread via tx_thread_performance_info_get.</span></span>

<span data-ttu-id="bd849-1006">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1006">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1007">Info Field 1: puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-1007">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="bd849-1008">Informazioni sul campo 2: stato del thread al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1008">Info Field 2: State of thread at time of call.</span></span>
- <span data-ttu-id="bd849-1009">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1009">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1010">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1010">Info Field 4: Not used.</span></span>

### <a name="thread-performance-system-info-get"></a><span data-ttu-id="bd849-1011">Informazioni sul sistema di prestazioni del thread Get</span><span class="sxs-lookup"><span data-stu-id="bd849-1011">Thread Performance System Info Get</span></span> 

#### <a name="tx_thread_performance_system_info_get"></a><span data-ttu-id="bd849-1012">tx_thread_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-1012">tx_thread_performance_system_info_get</span></span>

<span data-ttu-id="bd849-1013">**Icona** ![ di Icona di informazioni sul sistema delle prestazioni del thread](./media/user-guide/tx-events/image67.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1013">**Icon** ![Thread performance system info get icon](./media/user-guide/tx-events/image67.png)</span></span>

<span data-ttu-id="bd849-1014">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1014">**Description**</span></span>

<span data-ttu-id="bd849-1015">Questo evento rappresenta l'ottenimento di informazioni sulle prestazioni su tutti i thread tramite tx_thread_performance_system_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-1015">This event represents getting performance information about all threads via tx_thread_performance_system_info_get.</span></span>

<span data-ttu-id="bd849-1016">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1016">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-1017">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1017">Info Field 1: Not used.</span></span>
- <span data-ttu-id="bd849-1018">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1018">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-1019">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1019">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1020">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1020">Info Field 4: Not used.</span></span>

### <a name="thread-preemption-change"></a><span data-ttu-id="bd849-1021">Modifica di precedenza thread</span><span class="sxs-lookup"><span data-stu-id="bd849-1021">Thread Preemption Change</span></span> 

#### <a name="tx_thread_preemption_change"></a><span data-ttu-id="bd849-1022">tx_thread_preemption_change</span><span class="sxs-lookup"><span data-stu-id="bd849-1022">tx_thread_preemption_change</span></span>

<span data-ttu-id="bd849-1023">**Icona** ![ di Icona di modifica di precedenza thread](./media/user-guide/tx-events/image68.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1023">**Icon** ![Thread preemption change icon](./media/user-guide/tx-events/image68.png)</span></span>

<span data-ttu-id="bd849-1024">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1024">**Description**</span></span>

<span data-ttu-id="bd849-1025">Questo evento rappresenta la modifica della soglia di precedenza di un thread tramite tx_thread_preemption_change.</span><span class="sxs-lookup"><span data-stu-id="bd849-1025">This event represents changing a thread's preemption-threshold via tx_thread_preemption_change.</span></span>

<span data-ttu-id="bd849-1026">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1026">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-1027">Info Field 1: puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-1027">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="bd849-1028">Campo informazioni 2: nuova soglia di precedenza.</span><span class="sxs-lookup"><span data-stu-id="bd849-1028">Info Field 2: New preemption-threshold.</span></span>
- <span data-ttu-id="bd849-1029">Campo informazioni 3: soglia di precedenza precedente.</span><span class="sxs-lookup"><span data-stu-id="bd849-1029">Info Field 3: Previous preemption-threshold.</span></span>
- <span data-ttu-id="bd849-1030">Informazioni sul campo 4: stato del thread al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1030">Info Field 4: Thread's state at time of call.</span></span>

### <a name="thread-priority-change"></a><span data-ttu-id="bd849-1031">Modifica della priorità del thread</span><span class="sxs-lookup"><span data-stu-id="bd849-1031">Thread Priority Change</span></span> 

#### <a name="tx_thread_priority_change"></a><span data-ttu-id="bd849-1032">tx_thread_priority_change</span><span class="sxs-lookup"><span data-stu-id="bd849-1032">tx_thread_priority_change</span></span>

<span data-ttu-id="bd849-1033">**Icona** ![ di Icona di modifica della priorità del thread](./media/user-guide/tx-events/image69.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1033">**Icon** ![Thread priority change icon](./media/user-guide/tx-events/image69.png)</span></span>

<span data-ttu-id="bd849-1034">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1034">**Description**</span></span>

<span data-ttu-id="bd849-1035">Questo evento rappresenta la modifica della priorità di un thread tramite tx_thread_priority_change.</span><span class="sxs-lookup"><span data-stu-id="bd849-1035">This event represents changing a thread's priority via tx_thread_priority_change.</span></span>

- <span data-ttu-id="bd849-1036">Campi informazioni</span><span class="sxs-lookup"><span data-stu-id="bd849-1036">Information Fields</span></span> 
- <span data-ttu-id="bd849-1037">Info Field 1: puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-1037">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="bd849-1038">Informazioni sul campo 2: nuova priorità.</span><span class="sxs-lookup"><span data-stu-id="bd849-1038">Info Field 2: New priority.</span></span>
- <span data-ttu-id="bd849-1039">Informazioni sul campo 3: priorità precedente.</span><span class="sxs-lookup"><span data-stu-id="bd849-1039">Info Field 3: Previous priority.</span></span>
- <span data-ttu-id="bd849-1040">Informazioni sul campo 4: stato del thread al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1040">Info Field 4: Thread's state at time of call.</span></span>

### <a name="thread-relinquish"></a><span data-ttu-id="bd849-1041">Cessione thread</span><span class="sxs-lookup"><span data-stu-id="bd849-1041">Thread Relinquish</span></span> 

#### <a name="tx_thread_relinquish"></a><span data-ttu-id="bd849-1042">tx_thread_relinquish</span><span class="sxs-lookup"><span data-stu-id="bd849-1042">tx_thread_relinquish</span></span>

<span data-ttu-id="bd849-1043">**Icona** ![ di Icona di cessione thread](./media/user-guide/tx-events/image70.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1043">**Icon** ![Thread relinquish icon](./media/user-guide/tx-events/image70.png)</span></span>

<span data-ttu-id="bd849-1044">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1044">**Description**</span></span>

<span data-ttu-id="bd849-1045">Questo evento rappresenta l'abbandono del processore da un thread tramite tx_thread_relinquish.</span><span class="sxs-lookup"><span data-stu-id="bd849-1045">This event represents relinquishing the processor from a thread via tx_thread_relinquish.</span></span>

<span data-ttu-id="bd849-1046">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1046">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1047">Info Field 1: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1047">Info Field 1: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-1048">Info Field 2: puntatore al thread successivo da eseguire.</span><span class="sxs-lookup"><span data-stu-id="bd849-1048">Info Field 2: Pointer to the next thread to execute.</span></span>
- <span data-ttu-id="bd849-1049">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1049">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1050">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1050">Info Field 4: Not used.</span></span>

### <a name="thread-reset"></a><span data-ttu-id="bd849-1051">Reimpostazione thread</span><span class="sxs-lookup"><span data-stu-id="bd849-1051">Thread Reset</span></span> 

#### <a name="tx_thread_reset"></a><span data-ttu-id="bd849-1052">tx_thread_reset</span><span class="sxs-lookup"><span data-stu-id="bd849-1052">tx_thread_reset</span></span>

<span data-ttu-id="bd849-1053">**Icona** ![ di Icona di reimpostazione thread](./media/user-guide/tx-events/image71.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1053">**Icon** ![Thread reset icon](./media/user-guide/tx-events/image71.png)</span></span>

<span data-ttu-id="bd849-1054">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1054">**Description**</span></span>

<span data-ttu-id="bd849-1055">Questo evento rappresenta la reimpostazione di un thread completato o terminato tramite tx_thread_reset.</span><span class="sxs-lookup"><span data-stu-id="bd849-1055">This event represents resetting a completed or terminated thread via tx_thread_reset.</span></span>

<span data-ttu-id="bd849-1056">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1056">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1057">Info Field 1: puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-1057">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="bd849-1058">Informazioni sul campo 2: stato del thread al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1058">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="bd849-1059">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1059">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1060">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1060">Info Field 4: Not used.</span></span>

#### <a name="thread-resume"></a><span data-ttu-id="bd849-1061">Ripresa thread</span><span class="sxs-lookup"><span data-stu-id="bd849-1061">Thread Resume</span></span> 

##### <a name="tx_thread_resume"></a><span data-ttu-id="bd849-1062">tx_thread_resume</span><span class="sxs-lookup"><span data-stu-id="bd849-1062">tx_thread_resume</span></span>

<span data-ttu-id="bd849-1063">**Icona** ![ di Icona Riprendi thread](./media/user-guide/tx-events/image72.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1063">**Icon** ![Thread resume icon](./media/user-guide/tx-events/image72.png)</span></span>

<span data-ttu-id="bd849-1064">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1064">**Description**</span></span>

<span data-ttu-id="bd849-1065">Questo evento rappresenta il ripristino di un thread sospeso tramite tx_thread_resume.</span><span class="sxs-lookup"><span data-stu-id="bd849-1065">This event represents resuming a suspended thread via tx_thread_resume.</span></span>

<span data-ttu-id="bd849-1066">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1066">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1067">Info Field 1: puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-1067">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="bd849-1068">Informazioni sul campo 2: stato del thread al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1068">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="bd849-1069">Informazioni sul campo 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1069">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-1070">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1070">Info Field 4: Not used.</span></span>

### <a name="thread-sleep"></a><span data-ttu-id="bd849-1071">Sospensione thread</span><span class="sxs-lookup"><span data-stu-id="bd849-1071">Thread Sleep</span></span> 

#### <a name="tx_thread_sleep"></a><span data-ttu-id="bd849-1072">tx_thread_sleep</span><span class="sxs-lookup"><span data-stu-id="bd849-1072">tx_thread_sleep</span></span>

<span data-ttu-id="bd849-1073">**Icona** ![ di Icona sospensione thread](./media/user-guide/tx-events/image73.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1073">**Icon** ![Thread sleep icon](./media/user-guide/tx-events/image73.png)</span></span>

<span data-ttu-id="bd849-1074">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1074">**Description**</span></span>

<span data-ttu-id="bd849-1075">Questo evento rappresenta la sospensione del thread corrente per un numero specificato di cicli del timer tramite tx_thread_sleep.</span><span class="sxs-lookup"><span data-stu-id="bd849-1075">This event represents suspending the current thread for a specified number of timer ticks via tx_thread_sleep.</span></span>

<span data-ttu-id="bd849-1076">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1076">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1077">Campo informazioni 1: numero di cicli per la sospensione.</span><span class="sxs-lookup"><span data-stu-id="bd849-1077">Info Field 1: Number of ticks to suspend for.</span></span>
- <span data-ttu-id="bd849-1078">Informazioni sul campo 2: stato del thread al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1078">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="bd849-1079">Informazioni sul campo 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1079">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-1080">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1080">Info Field 4: Not used.</span></span>

### <a name="thread-stack-error-notify"></a><span data-ttu-id="bd849-1081">Notifica errori stack di thread</span><span class="sxs-lookup"><span data-stu-id="bd849-1081">Thread Stack Error Notify</span></span> 

#### <a name="tx_thread_stack_error_notify_event"></a><span data-ttu-id="bd849-1082">tx_thread_stack_error_notify_event</span><span class="sxs-lookup"><span data-stu-id="bd849-1082">tx_thread_stack_error_notify_event</span></span>

<span data-ttu-id="bd849-1083">**Icona** ![ di Icona di notifica errori stack di thread](./media/user-guide/tx-events/image74.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1083">**Icon** ![Thread stack error notify icon](./media/user-guide/tx-events/image74.png)</span></span>

<span data-ttu-id="bd849-1084">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1084">**Description**</span></span>

<span data-ttu-id="bd849-1085">Questo evento rappresenta la registrazione di una routine di notifica degli errori dello stack di thread tramite tx_thread_stack_error_notify_event.</span><span class="sxs-lookup"><span data-stu-id="bd849-1085">This event represents registering a thread stack error notification routine via tx_thread_stack_error_notify_event.</span></span>

<span data-ttu-id="bd849-1086">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1086">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-1087">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1087">Info Field 1: Not used.</span></span>
- <span data-ttu-id="bd849-1088">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1088">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-1089">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1089">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1090">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1090">Info Field 4: Not used.</span></span>

### <a name="thread-suspend"></a><span data-ttu-id="bd849-1091">Sospensione thread</span><span class="sxs-lookup"><span data-stu-id="bd849-1091">Thread Suspend</span></span> 

#### <a name="tx_thread_suspend"></a><span data-ttu-id="bd849-1092">tx_thread_suspend</span><span class="sxs-lookup"><span data-stu-id="bd849-1092">tx_thread_suspend</span></span>

<span data-ttu-id="bd849-1093">**Icona** ![ di Icona di sospensione thread](./media/user-guide/tx-events/image75.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1093">**Icon** ![Thread suspend icon](./media/user-guide/tx-events/image75.png)</span></span>

<span data-ttu-id="bd849-1094">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1094">**Description**</span></span>

<span data-ttu-id="bd849-1095">Questo evento rappresenta la sospensione di un thread tramite tx_thread_suspend.</span><span class="sxs-lookup"><span data-stu-id="bd849-1095">This event represents suspending a thread via tx_thread_suspend.</span></span>

<span data-ttu-id="bd849-1096">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1096">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-1097">Info Field 1: puntatore al thread da sospendere.</span><span class="sxs-lookup"><span data-stu-id="bd849-1097">Info Field 1: Pointer to thread to suspend.</span></span>
- <span data-ttu-id="bd849-1098">Informazioni sul campo 2: stato del thread al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1098">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="bd849-1099">Informazioni sul campo 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1099">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-1100">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1100">Info Field 4: Not used.</span></span>

### <a name="thread-terminate"></a><span data-ttu-id="bd849-1101">Terminazione thread</span><span class="sxs-lookup"><span data-stu-id="bd849-1101">Thread Terminate</span></span> 

#### <a name="tx_thread_terminate"></a><span data-ttu-id="bd849-1102">tx_thread_terminate</span><span class="sxs-lookup"><span data-stu-id="bd849-1102">tx_thread_terminate</span></span>

<span data-ttu-id="bd849-1103">**Icona** ![ di Icona termina thread](./media/user-guide/tx-events/image76.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1103">**Icon** ![Thread terminate icon](./media/user-guide/tx-events/image76.png)</span></span>

<span data-ttu-id="bd849-1104">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1104">**Description**</span></span>

<span data-ttu-id="bd849-1105">Questo evento rappresenta la terminazione di un thread tramite tx_thread_terminate.</span><span class="sxs-lookup"><span data-stu-id="bd849-1105">This event represents terminating a thread via tx_thread_terminate.</span></span>

<span data-ttu-id="bd849-1106">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1106">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-1107">Info Field 1: puntatore al thread da terminare.</span><span class="sxs-lookup"><span data-stu-id="bd849-1107">Info Field 1: Pointer to thread to terminate.</span></span>
- <span data-ttu-id="bd849-1108">Informazioni sul campo 2: stato del thread al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1108">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="bd849-1109">Informazioni sul campo 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1109">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-1110">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1110">Info Field 4: Not used.</span></span>

### <a name="thread-time-slice-change"></a><span data-ttu-id="bd849-1111">Modifica Time-Slice thread</span><span class="sxs-lookup"><span data-stu-id="bd849-1111">Thread Time-Slice Change</span></span> 

#### <a name="tx_thread_time_slice_change"></a><span data-ttu-id="bd849-1112">tx_thread_time_slice_change</span><span class="sxs-lookup"><span data-stu-id="bd849-1112">tx_thread_time_slice_change</span></span>

<span data-ttu-id="bd849-1113">**Icona** ![ di Icona di modifica della sezione Tempo thread](./media/user-guide/tx-events/image77.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1113">**Icon** ![Thread time-slice change icon](./media/user-guide/tx-events/image77.png)</span></span>

<span data-ttu-id="bd849-1114">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1114">**Description**</span></span>

<span data-ttu-id="bd849-1115">Questo evento rappresenta la modifica della sezione temporale di un thread tramite tx_thread_time_slice_change.</span><span class="sxs-lookup"><span data-stu-id="bd849-1115">This event represents changing a thread's time-slice via tx_thread_time_slice_change.</span></span>

<span data-ttu-id="bd849-1116">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1116">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1117">Info Field 1: puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-1117">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="bd849-1118">Campo informazioni 2: nuova sezione di tempo.</span><span class="sxs-lookup"><span data-stu-id="bd849-1118">Info Field 2: New time-slice.</span></span>
- <span data-ttu-id="bd849-1119">Informazioni sul campo 3: intervallo di tempo precedente.</span><span class="sxs-lookup"><span data-stu-id="bd849-1119">Info Field 3: Previous time-slice.</span></span>
- <span data-ttu-id="bd849-1120">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1120">Info Field 4: Not used.</span></span>

### <a name="thread-wait-abort"></a><span data-ttu-id="bd849-1121">Interruzione attesa thread</span><span class="sxs-lookup"><span data-stu-id="bd849-1121">Thread Wait Abort</span></span> 

#### <a name="tx_thread_wait_abort"></a><span data-ttu-id="bd849-1122">tx_thread_wait_abort</span><span class="sxs-lookup"><span data-stu-id="bd849-1122">tx_thread_wait_abort</span></span>

<span data-ttu-id="bd849-1123">**Icona** ![ di Icona interruzione thread di attesa](./media/user-guide/tx-events/image78.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1123">**Icon** ![Thread wait abort icon](./media/user-guide/tx-events/image78.png)</span></span>

<span data-ttu-id="bd849-1124">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1124">**Description**</span></span>

<span data-ttu-id="bd849-1125">Questo evento rappresenta l'interruzione della sospensione di un thread tramite tx_thread_wait_abort.</span><span class="sxs-lookup"><span data-stu-id="bd849-1125">This event represents aborting a thread's suspension via tx_thread_wait_abort.</span></span>

<span data-ttu-id="bd849-1126">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1126">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1127">Info Field 1: puntatore al thread.</span><span class="sxs-lookup"><span data-stu-id="bd849-1127">Info Field 1: Pointer to thread.</span></span>
- <span data-ttu-id="bd849-1128">Informazioni sul campo 2: stato del thread al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1128">Info Field 2: Thread's state at time of call.</span></span>
- <span data-ttu-id="bd849-1129">Informazioni sul campo 3: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1129">Info Field 3: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-1130">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1130">Info Field 4: Not used.</span></span>

### <a name="time-get"></a><span data-ttu-id="bd849-1131">Tempo di ottenimento</span><span class="sxs-lookup"><span data-stu-id="bd849-1131">Time Get</span></span> 

#### <a name="tx_time_get"></a><span data-ttu-id="bd849-1132">tx_time_get</span><span class="sxs-lookup"><span data-stu-id="bd849-1132">tx_time_get</span></span>

<span data-ttu-id="bd849-1133">**Icona** ![ di Icona Time Get](./media/user-guide/tx-events/image79.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1133">**Icon** ![Time get icon](./media/user-guide/tx-events/image79.png)</span></span>

<span data-ttu-id="bd849-1134">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1134">**Description**</span></span>

<span data-ttu-id="bd849-1135">Questo evento rappresenta il recupero del numero corrente di cicli del timer tramite tx_time_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-1135">This event represents getting the current number of timer ticks via tx_time_get.</span></span>

<span data-ttu-id="bd849-1136">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1136">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1137">Campo informazioni 1: numero corrente di cicli del timer.</span><span class="sxs-lookup"><span data-stu-id="bd849-1137">Info Field 1: Current number of timer ticks.</span></span>
- <span data-ttu-id="bd849-1138">Informazioni sul campo 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1138">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-1139">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1139">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1140">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1140">Info Field 4: Not used.</span></span>

### <a name="time-set"></a><span data-ttu-id="bd849-1141">Set di tempo</span><span class="sxs-lookup"><span data-stu-id="bd849-1141">Time Set</span></span> 

#### <a name="tx_time_set"></a><span data-ttu-id="bd849-1142">tx_time_set</span><span class="sxs-lookup"><span data-stu-id="bd849-1142">tx_time_set</span></span>

<span data-ttu-id="bd849-1143">**Icona** ![ di Icona del set di tempo](./media/user-guide/tx-events/image80.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1143">**Icon** ![Time set icon](./media/user-guide/tx-events/image80.png)</span></span>

<span data-ttu-id="bd849-1144">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1144">**Description**</span></span>

<span data-ttu-id="bd849-1145">Questo evento rappresenta l'impostazione del numero corrente di cicli del timer tramite tx_time_set.</span><span class="sxs-lookup"><span data-stu-id="bd849-1145">This event represents setting the current number of timer ticks via tx_time_set.</span></span>

<span data-ttu-id="bd849-1146">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1146">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1147">Campo informazioni 1: nuovo numero di cicli del timer.</span><span class="sxs-lookup"><span data-stu-id="bd849-1147">Info Field 1: New number of timer ticks.</span></span>
- <span data-ttu-id="bd849-1148">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1148">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-1149">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1149">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1150">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1150">Info Field 4: Not used.</span></span>

### <a name="timer-activate"></a><span data-ttu-id="bd849-1151">Attivazione timer</span><span class="sxs-lookup"><span data-stu-id="bd849-1151">Timer Activate</span></span> 

#### <a name="tx_timer_activate"></a><span data-ttu-id="bd849-1152">tx_timer_activate</span><span class="sxs-lookup"><span data-stu-id="bd849-1152">tx_timer_activate</span></span>

<span data-ttu-id="bd849-1153">**Icona** ![ di Icona di attivazione timer](./media/user-guide/tx-events/image81.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1153">**Icon** ![Timer activate icon](./media/user-guide/tx-events/image81.png)</span></span>

<span data-ttu-id="bd849-1154">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1154">**Description**</span></span>

<span data-ttu-id="bd849-1155">Questo evento rappresenta l'attivazione del timer specificato tramite tx_timer_activate.</span><span class="sxs-lookup"><span data-stu-id="bd849-1155">This event represents activating the specified timer via tx_timer_activate.</span></span>

<span data-ttu-id="bd849-1156">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1156">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1157">Informazioni sul campo 1: puntatore al timer.</span><span class="sxs-lookup"><span data-stu-id="bd849-1157">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="bd849-1158">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1158">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-1159">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1159">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1160">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1160">Info Field 4: Not used.</span></span>

### <a name="timer-change"></a><span data-ttu-id="bd849-1161">Modifica timer</span><span class="sxs-lookup"><span data-stu-id="bd849-1161">Timer Change</span></span> 

#### <a name="tx_timer_change"></a><span data-ttu-id="bd849-1162">tx_timer_change</span><span class="sxs-lookup"><span data-stu-id="bd849-1162">tx_timer_change</span></span>

<span data-ttu-id="bd849-1163">**Icona** ![ di Icona di modifica timer](./media/user-guide/tx-events/image82.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1163">**Icon** ![Timer change icon](./media/user-guide/tx-events/image82.png)</span></span>

<span data-ttu-id="bd849-1164">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1164">**Description**</span></span>

<span data-ttu-id="bd849-1165">Questo evento rappresenta la modifica del timer specificato tramite tx_timer_change.</span><span class="sxs-lookup"><span data-stu-id="bd849-1165">This event represents changing the specified timer via tx_timer_change.</span></span>

<span data-ttu-id="bd849-1166">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1166">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1167">Informazioni sul campo 1: puntatore al timer.</span><span class="sxs-lookup"><span data-stu-id="bd849-1167">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="bd849-1168">Campo informazioni 2: cicli di scadenza iniziali.</span><span class="sxs-lookup"><span data-stu-id="bd849-1168">Info Field 2: Initial expiration ticks.</span></span>
- <span data-ttu-id="bd849-1169">Informazioni sul campo 3: pianificare i cicli di scadenza.</span><span class="sxs-lookup"><span data-stu-id="bd849-1169">Info Field 3: Reschedule expiration ticks.</span></span>
- <span data-ttu-id="bd849-1170">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1170">Info Field 4: Not used.</span></span>

### <a name="timer-create"></a><span data-ttu-id="bd849-1171">Creazione timer</span><span class="sxs-lookup"><span data-stu-id="bd849-1171">Timer Create</span></span> 

#### <a name="tx_timer_create"></a><span data-ttu-id="bd849-1172">tx_timer_create</span><span class="sxs-lookup"><span data-stu-id="bd849-1172">tx_timer_create</span></span>

<span data-ttu-id="bd849-1173">**Icona** ![ di Icona Crea timer](./media/user-guide/tx-events/image83.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1173">**Icon** ![Timer create icon](./media/user-guide/tx-events/image83.png)</span></span>

<span data-ttu-id="bd849-1174">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1174">**Description**</span></span>

<span data-ttu-id="bd849-1175">Questo evento rappresenta la creazione di un timer tramite tx_timer_create.</span><span class="sxs-lookup"><span data-stu-id="bd849-1175">This event represents creating a timer via tx_timer_create.</span></span>

<span data-ttu-id="bd849-1176">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1176">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1177">Info Field 1: puntatore al blocco di controllo timer.</span><span class="sxs-lookup"><span data-stu-id="bd849-1177">Info Field 1: Pointer to timer control block.</span></span>
- <span data-ttu-id="bd849-1178">Campo informazioni 2: cicli di scadenza iniziali.</span><span class="sxs-lookup"><span data-stu-id="bd849-1178">Info Field 2: Initial expiration ticks.</span></span>
- <span data-ttu-id="bd849-1179">Informazioni sul campo 3: pianificare i cicli di scadenza.</span><span class="sxs-lookup"><span data-stu-id="bd849-1179">Info Field 3: Reschedule expiration ticks.</span></span>
- <span data-ttu-id="bd849-1180">Informazioni sul campo 4: abilitazione automatica del valore, ovvero TX_AUTO_ACTIVATE (1) o TX_NO_ACTIVATE (0).</span><span class="sxs-lookup"><span data-stu-id="bd849-1180">Info Field 4: Automatic enable value—either TX_AUTO_ACTIVATE (1) or TX_NO_ACTIVATE (0).</span></span>

### <a name="timer-deactivate"></a><span data-ttu-id="bd849-1181">Timer disattivato</span><span class="sxs-lookup"><span data-stu-id="bd849-1181">Timer Deactivate</span></span> 

#### <a name="tx_timer_deactivate"></a><span data-ttu-id="bd849-1182">tx_timer_deactivate</span><span class="sxs-lookup"><span data-stu-id="bd849-1182">tx_timer_deactivate</span></span>

<span data-ttu-id="bd849-1183">**Icona** ![ di Icona Disattiva timer](./media/user-guide/tx-events/image84.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1183">**Icon** ![Timer deactivate icon](./media/user-guide/tx-events/image84.png)</span></span>

<span data-ttu-id="bd849-1184">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1184">**Description**</span></span>

<span data-ttu-id="bd849-1185">Questo evento rappresenta la disattivazione di un timer tramite tx_timer_deactivate.</span><span class="sxs-lookup"><span data-stu-id="bd849-1185">This event represents deactivating a timer via tx_timer_deactivate.</span></span>

<span data-ttu-id="bd849-1186">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1186">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1187">Informazioni sul campo 1: puntatore al timer.</span><span class="sxs-lookup"><span data-stu-id="bd849-1187">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="bd849-1188">Informazioni sul campo 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1188">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-1189">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1189">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1190">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1190">Info Field 4: Not used.</span></span>

### <a name="timer-delete"></a><span data-ttu-id="bd849-1191">Timer Delete</span><span class="sxs-lookup"><span data-stu-id="bd849-1191">Timer Delete</span></span> 

#### <a name="tx_timer_delete"></a><span data-ttu-id="bd849-1192">tx_timer_delete</span><span class="sxs-lookup"><span data-stu-id="bd849-1192">tx_timer_delete</span></span>

<span data-ttu-id="bd849-1193">**Icona** ![ di Icona di eliminazione timer](./media/user-guide/tx-events/image85.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1193">**Icon** ![Timer delete icon](./media/user-guide/tx-events/image85.png)</span></span>

<span data-ttu-id="bd849-1194">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1194">**Description**</span></span>

<span data-ttu-id="bd849-1195">Questo evento rappresenta l'eliminazione di un timer tramite tx_timer_delete.</span><span class="sxs-lookup"><span data-stu-id="bd849-1195">This event represents deleting a timer via tx_timer_delete.</span></span>

<span data-ttu-id="bd849-1196">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1196">**Information Fields**</span></span> 

- <span data-ttu-id="bd849-1197">Informazioni sul campo 1: puntatore al timer.</span><span class="sxs-lookup"><span data-stu-id="bd849-1197">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="bd849-1198">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1198">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-1199">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1199">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1200">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1200">Info Field 4: Not used.</span></span>

### <a name="timer-information-get"></a><span data-ttu-id="bd849-1201">Informazioni sul timer Get</span><span class="sxs-lookup"><span data-stu-id="bd849-1201">Timer Information Get</span></span> 

#### <a name="tx_timer_info_get"></a><span data-ttu-id="bd849-1202">tx_timer_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-1202">tx_timer_info_get</span></span>

<span data-ttu-id="bd849-1203">**Icona** ![ di Icona per ottenere informazioni sul timer](./media/user-guide/tx-events/image86.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1203">**Icon** ![Timer get information icon](./media/user-guide/tx-events/image86.png)</span></span>

<span data-ttu-id="bd849-1204">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1204">**Description**</span></span>

<span data-ttu-id="bd849-1205">Questo evento rappresenta il recupero delle informazioni sul timer tramite tx_timer_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-1205">This event represents getting timer information via tx_timer_info_get.</span></span>

<span data-ttu-id="bd849-1206">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1206">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1207">Informazioni sul campo 1: puntatore al timer.</span><span class="sxs-lookup"><span data-stu-id="bd849-1207">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="bd849-1208">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1208">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-1209">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1209">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1210">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1210">Info Field 4: Not used.</span></span>

### <a name="timer-performance-information-get"></a><span data-ttu-id="bd849-1211">Informazioni sulle prestazioni del timer Get</span><span class="sxs-lookup"><span data-stu-id="bd849-1211">Timer Performance Information Get</span></span> 

#### <a name="tx_timer_performance_info_get"></a><span data-ttu-id="bd849-1212">tx_timer_performance_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-1212">tx_timer_performance_info_get</span></span>

<span data-ttu-id="bd849-1213">**Icona** ![ di Icona ottenere informazioni sulle prestazioni del timer](./media/user-guide/tx-events/image87.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1213">**Icon** ![Timer performance information get icon](./media/user-guide/tx-events/image87.png)</span></span>

<span data-ttu-id="bd849-1214">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1214">**Description**</span></span> 

<span data-ttu-id="bd849-1215">Questo evento rappresenta il recupero delle informazioni sulle prestazioni del timer tramite tx_timer_performance_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-1215">This event represents getting timer performance information via tx_timer_performance_info_get.</span></span>

<span data-ttu-id="bd849-1216">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1216">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1217">Informazioni sul campo 1: puntatore al timer.</span><span class="sxs-lookup"><span data-stu-id="bd849-1217">Info Field 1: Pointer to timer.</span></span>
- <span data-ttu-id="bd849-1218">Informazioni sul campo 2: puntatore dello stack al momento della chiamata.</span><span class="sxs-lookup"><span data-stu-id="bd849-1218">Info Field 2: Stack pointer at time of call.</span></span>
- <span data-ttu-id="bd849-1219">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1219">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1220">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1220">Info Field 4: Not used.</span></span>

### <a name="timer-system-performance-info-get"></a><span data-ttu-id="bd849-1221">Informazioni sulle prestazioni del sistema timer Get</span><span class="sxs-lookup"><span data-stu-id="bd849-1221">Timer System Performance Info Get</span></span> 

#### <a name="tx_timer_performance_system_info_get"></a><span data-ttu-id="bd849-1222">tx_timer_performance_system_info_get</span><span class="sxs-lookup"><span data-stu-id="bd849-1222">tx_timer_performance_system_info_get</span></span>

<span data-ttu-id="bd849-1223">**Icona** ![ di Icona delle informazioni sulle prestazioni del sistema timer Get](./media/user-guide/tx-events/image88.png)</span><span class="sxs-lookup"><span data-stu-id="bd849-1223">**Icon** ![Timer system performance info get icon](./media/user-guide/tx-events/image88.png)</span></span>


<span data-ttu-id="bd849-1224">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="bd849-1224">**Description**</span></span> 

<span data-ttu-id="bd849-1225">Questo evento rappresenta il recupero di tutte le informazioni sulle prestazioni del timer tramite tx_timer_performance_system_info_get.</span><span class="sxs-lookup"><span data-stu-id="bd849-1225">This event represents getting all timer performance information via tx_timer_performance_system_info_get.</span></span>

<span data-ttu-id="bd849-1226">**Campi informazioni**</span><span class="sxs-lookup"><span data-stu-id="bd849-1226">**Information Fields**</span></span>

- <span data-ttu-id="bd849-1227">Campo informazioni 1: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1227">Info Field 1: Not used.</span></span>
- <span data-ttu-id="bd849-1228">Campo informazioni 2: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1228">Info Field 2: Not used.</span></span>
- <span data-ttu-id="bd849-1229">Campo info 3: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1229">Info Field 3: Not used.</span></span>
- <span data-ttu-id="bd849-1230">Campo informazioni 4: non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bd849-1230">Info Field 4: Not used.</span></span>