---
title: Appendice A-servizi API ThreadX di Azure RTO
description: Esplorare i servizi API ThreadX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 30a2dc6284b413fe79ae6214e972b01d1321d031
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821377"
---
# <a name="appendix-a---azure-rtos-threadx-api-services"></a><span data-ttu-id="a002d-103">Appendice A-servizi API ThreadX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="a002d-103">Appendix A - Azure RTOS ThreadX API Services</span></span>

## <a name="entry-function"></a><span data-ttu-id="a002d-104">Entry (funzione)</span><span class="sxs-lookup"><span data-stu-id="a002d-104">Entry Function</span></span>

```c
VOID      tx_kernel_enter(VOID);
```

## <a name="block-memory-services"></a><span data-ttu-id="a002d-105">Blocca servizi di memoria</span><span class="sxs-lookup"><span data-stu-id="a002d-105">Block Memory Services</span></span>

```c
UINT      tx_block_allocate(TX_BLOCK_POOL *pool_ptr,
            VOID **block_ptr, ULONG wait_option);
```

```c
UINT      tx_block_pool_create(TX_BLOCK_POOL *pool_ptr,
            CHAR *name_ptr, ULONG block_size,
            VOID *pool_start, ULONG pool_size);
```

```c
UINT      tx_block_pool_delete(TX_BLOCK_POOL *pool_ptr);
```

```c
UINT      tx_block_pool_info_get(TX_BLOCK_POOL *pool_ptr,
            CHAR **name,
            ULONG *available_blocks, ULONG *total_blocks,
            TX_THREAD **first_suspended,
            ULONG *suspended_count,
            TX_BLOCK_POOL **next_pool);
```

```c
UINT      tx_block_pool_performance_info_get(TX_BLOCK_POOL *pool_ptr,
            ULONG *allocates, ULONG *releases, ULONG *suspensions,
            ULONG *timeouts);
```

```c
UINT      tx_block_pool_performance_system_info_get(ULONG *allocates,
            ULONG *releases, ULONG *suspensions, ULONG *timeouts);
```

```c
UINT      tx_block_pool_prioritize(TX_BLOCK_POOL *pool_ptr);
```

```c
UINT      tx_block_release(VOID *block_ptr);
```

## <a name="byte-memory-services"></a><span data-ttu-id="a002d-106">Servizi di memoria byte</span><span class="sxs-lookup"><span data-stu-id="a002d-106">Byte Memory Services</span></span>

```c
UINT      tx_byte_allocate(TX_BYTE_POOL *pool_ptr,
              VOID **memory_ptr,
              ULONG memory_size, ULONG wait_option);
```

```c
UINT      tx_byte_pool_create(TX_BYTE_POOL *pool_ptr,
              CHAR *name_ptr,
              VOID *pool_start, ULONG pool_size);
```

```c
UINT      tx_byte_pool_delete(TX_BYTE_POOL *pool_ptr);
```

```c
UINT      tx_byte_pool_info_get(TX_BYTE_POOL *pool_ptr,
              CHAR **name, ULONG *available_bytes,
              ULONG *fragments, TX_THREAD **first_suspended,
              ULONG *suspended_count,
              TX_BYTE_POOL **next_pool);
```

```c
UINT      tx_byte_pool_performance_info_get(TX_BYTE_POOL *pool_ptr,
              ULONG *allocates,
              ULONG *releases, ULONG *fragments_searched, ULONG *merges,
              ULONG *splits, ULONG *suspensions, ULONG *timeouts);
```

```c
UINT      tx_byte_pool_performance_system_info_get(ULONG *allocates,
              ULONG *releases, ULONG *fragments_searched, ULONG *merges,
              ULONG *splits, ULONG *suspensions, ULONG *timeouts);
```

```c
UINT      tx_byte_pool_prioritize(TX_BYTE_POOL *pool_ptr);
```

```c
UINT      tx_byte_release(VOID *memory_ptr);
```

## <a name="event-flags-services"></a><span data-ttu-id="a002d-107">Servizi flag di evento</span><span class="sxs-lookup"><span data-stu-id="a002d-107">Event Flags Services</span></span>

```c
UINT      tx_event_flags_create(TX_EVENT_FLAGS_GROUP *group_ptr,
            CHAR *name_ptr);
```

```c
UINT      tx_event_flags_delete(TX_EVENT_FLAGS_GROUP *group_ptr);
```

```c
UINT      tx_event_flags_get(TX_EVENT_FLAGS_GROUP *group_ptr,
            ULONG requested_flags, UINT get_option,
            ULONG *actual_flags_ptr, ULONG wait_option);
```

```c
UINT      tx_event_flags_info_get(TX_EVENT_FLAGS_GROUP *group_ptr,
            CHAR **name, ULONG *current_flags,
            TX_THREAD **first_suspended,
            ULONG *suspended_count,
            TX_EVENT_FLAGS_GROUP **next_group);
```

```c
UINT      tx_event_flags_performance_info_get(TX_EVENT_FLAGS_GROUP
            *group_ptr, ULONG *sets, ULONG *gets, ULONG *suspensions,
            ULONG *timeouts);
```

```c
UINT      tx_event_flags_performance_system_info_get(ULONG *sets,
            ULONG *gets,
            ULONG *suspensions, ULONG *timeouts);
```

```c
UINT      tx_event_flags_set(TX_EVENT_FLAGS_GROUP *group_ptr,
            ULONG flags_to_set, UINT set_option);
```

```c
UINT      tx_event_flags_set_notify(TX_EVENT_FLAGS_GROUP *group_ptr,
            VOID (*events_set_notify)(TX_EVENT_FLAGS_GROUP *));
```

## <a name="interrupt-control"></a><span data-ttu-id="a002d-108">Interrompi controllo</span><span class="sxs-lookup"><span data-stu-id="a002d-108">Interrupt Control</span></span>

```c
UINT      tx_interrupt_control(UINT new_posture);
```

## <a name="mutex-services"></a><span data-ttu-id="a002d-109">Servizi mutex</span><span class="sxs-lookup"><span data-stu-id="a002d-109">Mutex Services</span></span>

```c
UINT       tx_mutex_create(TX_MUTEX *mutex_ptr, CHAR *name_ptr,
              UINT inherit);
```

```c
UINT       tx_mutex_delete(TX_MUTEX *mutex_ptr);
```

```c
UINT       tx_mutex_get(TX_MUTEX *mutex_ptr, ULONG wait_option);
```

```c
UINT       tx_mutex_info_get(TX_MUTEX *mutex_ptr, CHAR **name,
              ULONG *count, TX_THREAD **owner,
              TX_THREAD **first_suspended,
              ULONG *suspended_count,
              TX_MUTEX **next_mutex);
```

```c
UINT       tx_mutex_performance_info_get(TX_MUTEX *mutex_ptr, ULONG
              *puts, ULONG *gets, ULONG *suspensions, ULONG *timeouts,
              ULONG *inversions, ULONG *inheritances);
```

```c
UINT       tx_mutex_performance_system_info_get(ULONG *puts, ULONG
              *gets,
              ULONG *suspensions, ULONG *timeouts, ULONG *inversions,
              ULONG *inheritances);
```

```c
UINT       tx_mutex_prioritize(TX_MUTEX *mutex_ptr);
```

```c
UINT       tx_mutex_put(TX_MUTEX *mutex_ptr);
```
## <a name="queue-services"></a><span data-ttu-id="a002d-110">Servizi di Accodamento</span><span class="sxs-lookup"><span data-stu-id="a002d-110">Queue Services</span></span>

```c
UINT       tx_queue_create(TX_QUEUE *queue_ptr, CHAR *name_ptr,
              UINT message_size, VOID *queue_start,
              ULONG queue_size);
```

```c
UINT       tx_queue_delete(TX_QUEUE *queue_ptr);
```

```c
UINT       tx_queue_flush(TX_QUEUE *queue_ptr);
```

```c
UINT       tx_queue_front_send(TX_QUEUE *queue_ptr, VOID *source_ptr,
              ULONG wait_option);
```

```c
UINT       tx_queue_info_get(TX_QUEUE *queue_ptr, CHAR **name,
              ULONG *enqueued, ULONG *available_storage,
              TX_THREAD **first_suspended,
              ULONG *suspended_count, TX_QUEUE **next_queue);
```

```c
UINT       tx_queue_performance_info_get(TX_QUEUE *queue_ptr,
              ULONG *messages_sent, ULONG *messages_received,
              ULONG *empty_suspensions, ULONG *full_suspensions,
              ULONG *full_errors, ULONG *timeouts);
```

```c
UINT       tx_queue_performance_system_info_get(ULONG *messages_sent,
              ULONG *messages_received, ULONG *empty_suspensions,
              ULONG *full_suspensions, ULONG *full_errors,
              ULONG *timeouts);
```

```c
UINT       tx_queue_prioritize(TX_QUEUE *queue_ptr);
```

```c
UINT       tx_queue_receive(TX_QUEUE *queue_ptr,
              VOID *destination_ptr, ULONG wait_option);
```

```c
UINT       tx_queue_send(TX_QUEUE *queue_ptr, VOID *source_ptr,
              ULONG wait_option);
```

```c
UINT       tx_queue_send_notify(TX_QUEUE *queue_ptr, VOID
              (*queue_send_notify)(TX_QUEUE *));
```

## <a name="semaphore-services"></a><span data-ttu-id="a002d-111">Servizi semaforo</span><span class="sxs-lookup"><span data-stu-id="a002d-111">Semaphore Services</span></span>

```c
UINT       tx_semaphore_ceiling_put(TX_SEMAPHORE *semaphore_ptr,
              ULONG ceiling);
```

```c
UINT       tx_semaphore_create(TX_SEMAPHORE *semaphore_ptr,
              CHAR *name_ptr, ULONG initial_count);
```

```c
UINT       tx_semaphore_delete(TX_SEMAPHORE *semaphore_ptr);
```

```c
UINT       tx_semaphore_get(TX_SEMAPHORE *semaphore_ptr,
              ULONG wait_option);
```

```c
UINT       tx_semaphore_info_get(TX_SEMAPHORE *semaphore_ptr, CHAR **name,
              ULONG *current_value,
              TX_THREAD **first_suspended,
              ULONG *suspended_count,
              TX_SEMAPHORE **next_semaphore);
```

```c
UINT       tx_semaphore_performance_info_get(TX_SEMAPHORE *semaphore_ptr,
              ULONG *puts, ULONG *gets, ULONG *suspensions,
              ULONG *timeouts);
```

```c
UINT       tx_semaphore_performance_system_info_get(ULONG *puts,
              ULONG *gets, ULONG *suspensions, ULONG *timeouts);
```

```c
UINT       tx_semaphore_prioritize(TX_SEMAPHORE *semaphore_ptr);
```

```c
UINT       tx_semaphore_put(TX_SEMAPHORE *semaphore_ptr);
```

```c
UINT       tx_semaphore_put_notify(TX_SEMAPHORE *semaphore_ptr,
              VOID (*semaphore_put_notify)(TX_SEMAPHORE *));
```

## <a name="thread-control-services"></a><span data-ttu-id="a002d-112">Servizi di controllo thread</span><span class="sxs-lookup"><span data-stu-id="a002d-112">Thread Control Services</span></span>

```c
UINT       tx_thread_create(TX_THREAD *thread_ptr,
              CHAR *name_ptr,
              VOID (*entry_function)(ULONG), ULONG entry_input,
              VOID *stack_start, ULONG stack_size,
              UINT priority, UINT preempt_threshold,
              ULONG time_slice, UINT auto_start);
```

```c
UINT       tx_thread_delete(TX_THREAD *thread_ptr);
```

```c
UINT       tx_thread_entry_exit_notify(TX_THREAD *thread_ptr,
              VOID (*thread_entry_exit_notify)(TX_THREAD *, UINT));
```

```c
TX_THREAD      *tx_thread_identify(VOID);
```

```c
UINT       tx_thread_info_get(TX_THREAD *thread_ptr, CHAR **name,
              UINT *state, ULONG *run_count, UINT *priority,
              UINT *preemption_threshold, ULONG *time_slice,
              TX_THREAD **next_thread,
              TX_THREAD **next_suspended_thread);
```

```c
UINT       tx_thread_performance_info_get(TX_THREAD *thread_ptr,
              ULONG *resumptions, ULONG *suspensions,
              ULONG *solicited_preemptions,
              ULONG *interrupt_preemptions,
              ULONG *priority_inversions,ULONG *time_slices, ULONG
              *relinquishes, ULONG *timeouts,
              ULONG *wait_aborts, TX_THREAD **last_preempted_by);
```

```c
UINT       tx_thread_performance_system_info_get(ULONG *resumptions,
              ULONG *suspensions,
              ULONG *solicited_preemptions,
              ULONG *interrupt_preemptions,
              ULONG *priority_inversions,ULONG *time_slices, ULONG
              *relinquishes, ULONG *timeouts,
              ULONG *wait_aborts, ULONG *non_idle_returns,
              ULONG *idle_returns);
```

```c
UINT       tx_thread_preemption_change(TX_THREAD *thread_ptr,
              UINT new_threshold, UINT *old_threshold);
```

```c
UINT       tx_thread_priority_change(TX_THREAD *thread_ptr,
              UINT new_priority, UINT *old_priority);
```

```c
VOID       tx_thread_relinquish(VOID);
```

```c
UINT       tx_thread_reset(TX_THREAD *thread_ptr);
```

```c
UINT       tx_thread_resume(TX_THREAD *thread_ptr);
```

```c
UINT       tx_thread_sleep(ULONG timer_ticks);
```

```c
UINT       tx_thread_stack_error_notify
              VOID(*stack_error_handler)(TX_THREAD *));
```

```c
UINT       tx_thread_suspend(TX_THREAD *thread_ptr);
```

```c
UINT       tx_thread_terminate(TX_THREAD *thread_ptr);
```

```c
UINT       tx_thread_time_slice_change(TX_THREAD *thread_ptr,
              ULONG new_time_slice, ULONG *old_time_slice);
```

```c
UINT       tx_thread_wait_abort(TX_THREAD *thread_ptr);
```

## <a name="time-services"></a><span data-ttu-id="a002d-113">Servizi temporali</span><span class="sxs-lookup"><span data-stu-id="a002d-113">Time Services</span></span>

```c
ULONG      tx_time_get(VOID);
VOID       tx_time_set(ULONG new_time);
```

## <a name="timer-services"></a><span data-ttu-id="a002d-114">Servizi timer</span><span class="sxs-lookup"><span data-stu-id="a002d-114">Timer Services</span></span>

```c
UINT       tx_timer_activate(TX_TIMER *timer_ptr);
```

```c
UINT       tx_timer_change(TX_TIMER *timer_ptr,
              ULONG initial_ticks,
              ULONG reschedule_ticks);
```

```c
UINT       tx_timer_create(TX_TIMER *timer_ptr,
              CHAR *name_ptr,
              VOID (*expiration_function)(ULONG),
              ULONG expiration_input, ULONG initial_ticks,
              ULONG reschedule_ticks, UINT auto_activate);
```

```c
UINT       tx_timer_deactivate(TX_TIMER *timer_ptr);
```

```c
UINT       tx_timer_delete(TX_TIMER *timer_ptr);
```

```c
UINT       tx_timer_info_get(TX_TIMER *timer_ptr, CHAR **name,
              UINT *active, ULONG *remaining_ticks,
              ULONG *reschedule_ticks,
              TX_TIMER **next_timer);
```

```c
UINT       tx_timer_performance_info_get(TX_TIMER *timer_ptr,
              ULONG *activates,
              ULONG *reactivates, ULONG *deactivates,
              ULONG *expirations,
              ULONG *expiration_adjusts);
```

```c
UINT       tx_timer_performance_system_info_get
              ULONG *activates, ULONG *reactivates,
              ULONG *deactivates, ULONG *expirations,
              ULONG *expiration_adjusts);
```
