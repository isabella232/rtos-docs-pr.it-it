---
title: Capitolo 6 - Sistema dimostrativo per Azure RTOS ThreadX
description: Questo capitolo contiene una descrizione del sistema dimostrativo fornito con tutti i Azure RTOS di supporto del processore ThreadX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 67054d67d0a6babc50a489c4ec4b738abf3efccab10060d307106e8344b00d02
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783374"
---
# <a name="chapter-6---demonstration-system-for-azure-rtos-threadx"></a>Capitolo 6 - Sistema dimostrativo per Azure RTOS ThreadX

Questo capitolo contiene una descrizione del sistema dimostrativo fornito con tutti i Azure RTOS di supporto del processore ThreadX.

## <a name="overview"></a>Panoramica

Ogni distribuzione del prodotto ThreadX contiene un sistema dimostrativo che viene eseguito su tutti i microprocessori supportati.

Questo sistema di esempio è definito nel file di ***distribuzione demo_threadx.c*** ed è progettato per illustrare l'uso di ThreadX in un ambiente multithread incorporato. La dimostrazione è costituita da inizializzazione, otto thread, un pool di byte, un pool di blocchi, una coda, un semaforo, un mutex e un gruppo di flag di evento.

> [!NOTE]
> *Fatta eccezione per le dimensioni dello stack del thread, l'applicazione dimostrativa è identica in tutti i processori supportati da ThreadX.*

Elenco completo di ***demo_threadx.c,*** inclusi i numeri di riga a cui si fa riferimento nel resto di questo capitolo.

## <a name="application-define"></a>Definizione dell'applicazione

La ***tx_application_define*** viene eseguita dopo il completamento dell'inizializzazione ThreadX di base. È responsabile della configurazione di tutte le risorse di sistema iniziali, inclusi thread, code, semafori, mutex, flag di eventi e pool di memoria.

Il sistema dimostrativo ***tx_application_define** _ (numeri _line 60-164*) crea gli oggetti dimostrativi nell'ordine seguente:

- byte_pool_0
- thread_0
- thread_1
- thread_2
- thread_3
- thread_4
- thread_5
- thread_6
- thread_7
- queue_0
- semaphore_0
- event_flags_0
- mutex_0
- block_pool_0

Il sistema dimostrativo non crea altri oggetti ThreadX aggiuntivi. Tuttavia, un'applicazione effettiva può creare oggetti di sistema durante il runtime all'interno dei thread in esecuzione.

### <a name="initial-execution"></a>Esecuzione iniziale

Tutti i thread vengono creati con **l'TX_AUTO_START** predefinita. Questo li rende inizialmente pronti per l'esecuzione. Al ***tx_application_define,*** il controllo viene trasferito all'utilità di pianificazione dei thread e da qui a ogni singolo thread.

L'ordine di esecuzione dei thread è determinato dalla priorità e dall'ordine in cui sono stati creati. Nel sistema dimostrativo, ***thread_0*** viene eseguito per primo perché ha la priorità più alta ( è stato creato *con una priorità di 1*). Dopo ***thread_0,*** viene eseguito ***thread_5,*** seguito dall'esecuzione di ***thread_3** _, _*_thread_4_*_, _*_thread_6_*_, _* _thread_7_**, ***thread_1**_ e infine _*_thread_2_**.

> [!NOTE]
> *Anche se **thread_3** e **thread_4** hanno la stessa priorità (entrambe create con priorità 8), thread_3 viene eseguita per prima.  Ciò è dovuto **al thread_3** stato creato e pronto **prima thread_4**. I thread con uguale priorità vengono eseguiti in modo FIFO.*

## <a name="thread-0"></a>Thread 0

La funzione ***thread_0_entry*** il punto di ingresso del thread *(righe 167-190*). ***Thread_0*** è il primo thread del sistema dimostrativo da eseguire. L'elaborazione è semplice: incrementa il contatore, viene inattiva per 10 tick timer, imposta un flag di evento per la riattivazione thread_5 ***e*** quindi ripete la sequenza.

***Thread_0*** è il thread con la priorità più alta nel sistema. Alla scadenza della sospensione richiesta, verrà eseguito qualsiasi altro thread in esecuzione nella dimostrazione.

## <a name="thread-1"></a>Thread 1

La funzione ***thread_1_entry** _ contrassegna il punto di ingresso del thread _(righe 193-216).****Thread_1*** è il secondo e ultimo thread del sistema dimostrativo da eseguire. L'elaborazione consiste  nell'incremento* del contatore, nell'invio di un messaggio thread_2 ( da * ***queue_0***) e nella ripetizione della sequenza. Si noti che *** thread_1**_ sospende ogni _*_queue_0_*_ diventa piena (_line 207*).

## <a name="thread-2"></a>Thread 2

La funzione ***thread_2_entry*** contrassegna il punto di ingresso del thread *(righe 219-243).* ***Thread_2*** è l'ultimo thread del sistema dimostrativo da eseguire. L'elaborazione consiste nell'incremento del contatore, nel recupero di un messaggio ***thread_1*** (tramite ***queue_0***) e nella ripetizione della sequenza. Si noti che *** thread_2** _ sospende ogni _*_queue_0_*_ vuoto (_line 233*).

Anche ***thread_1** _ e _ *_thread_2_*** condividono la priorità più bassa nel sistema dimostrativo (priorità 16*), i thread *3 e 4*

sono anche gli unici thread pronti per l'esecuzione nella maggior parte dei casi. Sono anche gli unici thread creati con la sezione temporale (*righe 87 e 93*). Ogni thread può essere eseguito per un massimo di 4 tick timer prima dell'esecuzione dell'altro thread.

## <a name="threads-3-and-4"></a>Thread 3 e 4

La funzione ***thread_3_and_4_entry*** il punto di ingresso di ***thread_3** _ e _ *_thread_4_** (righe 246-280). Entrambi i thread hanno una priorità di 8, che li rende il terzo e il quarto thread del sistema dimostrativo da eseguire. L'elaborazione per ogni thread è la stessa: incremento del contatore, recupero di ***semaphore_0,*** sospensione per 2 tick timer, rilascio ***semaphore_0*** e ripetizione della sequenza. Si noti che ogni thread viene sospeso ***ogni semaphore_0*** non è disponibile (riga 264).

Entrambi i thread usano anche la stessa funzione per l'elaborazione principale.
Questo non presenta problemi perché entrambi hanno un proprio stack univoco e C è naturalmente rientrante. Ogni thread determina quale si tratta verificando il parametro di input del thread (riga 258), che viene impostato al momento della creazione (righe 102 e 109).

> [!NOTE]
> *È anche ragionevole ottenere il punto di thread corrente durante l'esecuzione del thread e confrontarlo con l'indirizzo del blocco di controllo per determinare l'identità del thread.*

## <a name="thread-5"></a>Thread 5

La funzione ***thread_5_entry*** contrassegna il punto di ingresso del thread (righe 283-305). ***Thread_5*** è il secondo thread del sistema dimostrativo da eseguire. L'elaborazione consiste nell'incrementare il contatore, ottenere un flag di evento ***da*** thread_0 (tramite ***event_flags_0***) e ripetere la sequenza. Si noti ***thread_5*** viene sospesa ogni volta che il flag di evento ***event_flags_0*** non è disponibile (riga 298).

## <a name="threads-6-and-7"></a>Thread 6 e 7

La funzione ***thread_6_and_7_entry*** contrassegna il punto di ingresso di ***thread_6** _ e _ *_thread_7_** (righe 307-358). Entrambi i thread hanno una priorità di 8, che li rende il quinto e il sesto thread del sistema dimostrativo da eseguire. L'elaborazione per ogni thread è la stessa: incremento del contatore, recupero di mutex_0 due volte, sospensione di 2 tick timer, rilascio ***mutex_0 due*** volte e ripetizione della sequenza.  Si noti che ogni thread viene sospeso ogni ***mutex_0*** non è disponibile (riga 325).

Entrambi i thread usano anche la stessa funzione per l'elaborazione principale. Questo non presenta problemi perché entrambi hanno un proprio stack univoco e C è naturalmente rientrante.
Ogni thread determina quale si tratta verificando il parametro di input del thread (riga 319), che viene impostato al momento della creazione (righe 126 e 133).

## <a name="observing-the-demonstration"></a>Osservazione della dimostrazione

Ognuno dei thread dimostrativi incrementa il proprio contatore univoco.
I contatori seguenti possono essere esaminati per verificare l'operazione della demo:

- thread_0_counter
- thread_1_counter
- thread_2_counter
- thread_3_counter
- thread_4_counter
- thread_5_counter
- thread_6_counter
- thread_7_counter

Ognuno di questi contatori dovrebbe continuare ad aumentare durante l'esecuzione della dimostrazione, con ***thread_1_counter** _ e _ *_thread_2_counter_** che aumentano alla velocità più rapida.

## <a name="distribution-file-demo_threadxc"></a>File di distribuzione: demo_threadx.c

In questa sezione viene visualizzato l'elenco completo ***di demo_threadx.c***, inclusi i numeri di riga a cui si fa riferimento in questo capitolo.

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
