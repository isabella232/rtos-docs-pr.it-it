---
title: Capitolo 2 - Requisiti del modulo
description: Questo articolo contiene una descrizione dei requisiti per la compilazione di un modulo ThreadX.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 24b814e7c2b510093b809b70b02d9a11ed39996d114f2306e0993893799453cc
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791959"
---
# <a name="chapter-2---module-requirements"></a>Capitolo 2 - Requisiti del modulo

Un modulo ThreadX contiene un preambolo, che definisce le caratteristiche di base del modulo. Il preambolo è seguito dall'area di istruzioni del modulo. I moduli possono essere eseguiti sul posto o caricati nell'area di memoria del modulo da Gestione moduli prima dell'esecuzione. L'unico requisito è che il preambolo si trovi sempre al primo indirizzo del modulo. La figura 2 illustra un layout di modulo di base.

| Layout del modulo |
|:---:|
| \[preambolo del modulo\]         |
| \[area di istruzioni del modulo\] |
| \[area RAM del modulo\]         |

**Figura 2** - Layout del modulo

> [!NOTE]
> I moduli devono essere compilati con il codice indipendente dalla posizione e le opzioni del compilatore/linker di dati appropriate. Ciò consente l'esecuzione del modulo in qualsiasi area di memoria.

Quando viene creato un thread Module, viene allocato un secondo spazio dello stack da usare quando il thread si trova nel kernel protetto dalla memoria. Le dimensioni dello spazio dello stack del kernel del thread sono configurabili dall'utente usando TXM_MODULE_KERNEL_STACK_SIZE **in** **_txm_module_port.h_*_. Ciò consente di usare dimensioni* dello stack inferiori quando si crea un thread Module, perché lo stack specificato dall'utente quando chiama _ _tx_thread_create_** viene usato solo nel modulo.

> [!NOTE]
> La parte superiore di uno stack di thread del modulo contiene la struttura delle informazioni sulle voci di thread ( TXM_MODULE_THREAD_ENTRY_INFO ),**quindi** le dimensioni dello stack disponibili vengono ridotte delle dimensioni di questa struttura. Quando si crea un thread in un modulo, aumentarne le dimensioni dello stack almeno di queste dimensioni della struttura.

I passaggi seguenti sono necessari per la creazione e la compilazione di un modulo ThreadX (ogni passaggio è descritto più dettagliatamente di seguito).

1. Tutti i file C in un modulo devono #define **TXM_MODULE** prima di includere **_txm_module.h._** Questa operazione può essere eseguita nel file di origine da compilare o come parte delle impostazioni del progetto. In questo modo viene eseguito di nuovo il mapping delle chiamate DELL'API ThreadX alla versione specifica del modulo dell'API che richiama la funzione dispatch in Gestione moduli residente per eseguire la chiamata alla funzione API effettiva.
2. Ogni modulo deve avere un preambolo al primo indirizzo dell'area di istruzioni che definisce le caratteristiche e le esigenze di risorse del modulo.
3. Ogni modulo deve collegare il preambolo all'inizio dell'area di istruzioni del modulo.
4. Ogni modulo deve essere associato a una libreria di moduli (***txm.a***), che contiene funzioni specifiche del modulo usate per interagire con ThreadX.

## <a name="module-sources"></a>Origini dei moduli

I moduli ThreadX hanno un proprio set di file di origine progettati per essere collegati e posizionati direttamente con il codice sorgente del modulo. Questi file forniscono il bridge tra il modulo separato e Gestione moduli residenti. I file del modulo sono i seguenti.

| File Name | Contenuto |
|---|---|
| **txm_module.h** | File di inclusione che definisce le informazioni sul modulo. |
| **txm_module_port.h** | File di inclusione che definisce le informazioni sul modulo specifiche della porta. |
| **txm_module_user.h** | Definisce e valori che l'utente può personalizzare. |
| **txm_module_initialize.s [1][3]** | Chiama funzioni intrinseche al modulo di avvio. |
| **txm_module_preamble. \{ s/S/68\}** | File di assembly preambolo del modulo. Questo file definisce vari attributi specifici del modulo ed è collegato al codice dell'applicazione del modulo. |
| **txm_module_application_request.c [1]** | La funzione di richiesta dell'applicazione modulo invia una richiesta specifica dell'applicazione al codice residente. |
| **txm_module_callback_request_thread_entry.c &nbsp; [1]** | Thread di callback del modulo responsabile dell'elaborazione dei callback richiesti dal modulo, inclusi i timer e i callback di notifica. |
| **txm_*.c [1][2]** | I servizi API ThreadX standard, che chiamano il dispatcher del kernel.
| **txm_module_object_allocate.c [1]** | Funzione module per allocare memoria per gli oggetti modulo che si trovano nel pool di memoria di gestione. |
| **txm_module_object_deallocate.c [1]** | Funzione module per deallocare la memoria per gli oggetti modulo che si trovano nel pool di memoria di gestione. |
| **txm_module_object_pointer_get.c [1]** | Funzione Module per recuperare un puntatore a un oggetto di sistema. |
| **txm_module_object_pointer_get_extended.c [1]** | Funzione module per recuperare un puntatore a un oggetto di sistema, sicurezza della lunghezza del nome. |
| **txm_module_thread_shell_entry.c [1]** | Funzione di immissione del thread del modulo. |
| **txm_module_thread_system_suspend.c [1]** | Funzione module per sospendere un thread. |

**[1]** Si trova nella libreria **_txm.a_**.

**[2]** Questi file hanno lo stesso nome dei  file dell'API ThreadX, con txm_ prefisso anziché tx_ **prefisso.**

**[3]** Il file **txm_module_initialize.s** è solo per le porte che usano gli strumenti arm.

## <a name="module-preamble"></a>Preambolo del modulo

Il preambolo del modulo definisce le caratteristiche e le risorse del modulo. Informazioni quali la funzione iniziale di immissione del thread e l'area di memoria iniziale associata al thread sono definite nel preambolo. Gli esempi di preambolo specifici della porta sono inclusi [nell'appendice](appendix.md). La figura 3 illustra un esempio di preambolo del modulo ThreadX per una destinazione generica (le righe che iniziano con * sono valori in genere modificati dall'applicazione):

```c
    AREA Init, CODE, READONLY

    /* Define public symbols. */
    EXPORT __txm_module_preamble

    /* Define application-specific start/stop entry points for the module. */
    IMPORT demo_module_start

    /* Define common external refrences. */
    IMPORT _txm_module_thread_shell_entry
    IMPORT _txm_module_callback_request_thread_entry
    IMPORT |Image$$ER_RO$$Length|
    IMPORT |Image$$ER_RW$$Length|

__txm_module_preamble
    DCD     0x4D4F4455                                  ; Module ID
    DCD     0x6                                         ; Module Major Version
    DCD     0x1                                         ; Module Minor Version
    DCD     32                                          ; Module Preamble Size in 32-bit words
*   DCD     0x12345678                                  ; Module ID (application defined)
*   DCD     0x01000001                                  ; Module Properties where:
                                                        ; Bits 31-24: Compiler ID
                                                        ;   0 -> IAR
                                                        ;   1 -> ARM
                                                        ;   2 -> GNU
                                                        ;   Bits 23-1: Reserved
                                                        ;   Bit 0: 0 -> Privileged mode execution (no MMU protection)
                                                        ;          1 -> User mode execution (MMU protection)
    DCD     _txm_module_thread_shell_entry - . + .      ; Module Shell Entry Point
*   DCD     demo_module_start - . + .                   ; Module Start Thread Entry Point
    DCD     0                                           ; Module Stop Thread Entry Point
*   DCD     1                                           ; Module Start/Stop Thread Priority
*   DCD     2048                                        ; Module Start/Stop Thread Stack Size
    DCD     _txm_module_callback_request_thread_entry - . + . ; Module Callback Thread Entry
    DCD     1                                            ; Module Callback Thread Priority
    DCD     2048                                         ; Module Callback Thread Stack Size
    DCD     |Image$$ER_RO$$Length|                       ; Module Code Size
    DCD     |Image$$ER_RW$$Length|                       ; Module Data Size
    DCD     0                                            ; Reserved 0
    DCD     0                                            ; Reserved 1
    DCD     0                                            ; Reserved 2
    DCD     0                                            ; Reserved 3
    DCD     0                                            ; Reserved 4
    DCD     0                                            ; Reserved 5
    DCD     0                                            ; Reserved 6
    DCD     0                                            ; Reserved 7
    DCD     0                                            ; Reserved 8
    DCD     0                                            ; Reserved 9
    DCD     0                                            ; Reserved 10
    DCD     0                                            ; Reserved 11
    DCD     0                                            ; Reserved 12
    DCD     0                                            ; Reserved 13
    DCD     0                                            ; Reserved 14
    DCD     0                                            ; Reserved 15
    END
```

**Figura 3**

Nella maggior parte dei casi, lo sviluppatore deve definire solo il thread iniziale del modulo (offset 0x1C), l'ID del modulo (offset 0x10), la priorità del thread di avvio/arresto (offset 0x24) e le dimensioni dello stack del thread di avvio/arresto (offset 0x28). La dimostrazione precedente è impostata _*_in_*_ modo che il thread iniziale del modulo sia ***demo_module_start** _, l'ID modulo sia 0x12345678 e il thread iniziale abbia una priorità _*_di 1_*_ e una dimensione dello stack di _ *_2048_** byte.

Alcune applicazioni possono facoltativamente definire un thread di arresto, che viene eseguito quando Gestione moduli arresta il modulo. Inoltre, alcune applicazioni potrebbero usare il campo Proprietà modulo, definito come segue.

## <a name="module-properties-bit-map"></a>Mapping di bit delle proprietà del modulo

La tabella seguente illustra un esempio della mappa dei bit delle proprietà. Le bitmap delle proprietà specifiche della porta sono presenti [nell'appendice](appendix.md).

| bit | Valore | Significato |
|---|---|---|
| 0 | 0<br />1 | Esecuzione in modalità privilegiata<br />Esecuzione in modalità utente |
| 1 | 0<br />1 | Nessuna protezione MPU<br />Protezione MPU (deve essere selezionata la modalità utente) |
| 2 | 0<br />1 | Disabilitare l'accesso alla memoria condivisa/esterna<br />Abilitare l'accesso alla memoria condivisa/esterna |
| [23-3] | 0 | Riservato
| [31-24] | <br />0x01<br />0x02<br />0x03 | **ID compilatore**<br />Iar<br />ARM<br />Gnu |


## <a name="module-linker-control-file"></a>File di controllo del linker del modulo

Quando si compila un modulo, il preambolo del modulo deve essere posizionato prima di qualsiasi altra sezione di codice. Un modulo deve essere compilato con sezioni di dati e codice indipendenti dalla posizione. I file del linker di esempio specifici della porta sono disponibili [nell'appendice](appendix.md).

## <a name="module-threadx-library"></a>Libreria ThreadX del modulo

Ogni modulo deve essere correlato a una speciale libreria ThreadX incentrata sui moduli. Questa libreria fornisce l'accesso ai servizi ThreadX nel codice residente. La maggior parte dell'accesso viene eseguita tramite ***txm_ file con estensione \* c.*** Di seguito è riportato un esempio della chiamata di accesso al modulo per la funzione API ThreadX **_tx_thread_relinquish_* _ (in _*_ \_ txm_thread_relinquish.c \* ***).

```c
(_txm_module_kernel_call_dispatcher)(TXM_THREAD_RELINQUISH_CALL, 0, 0, 0);
```

In questo esempio, il puntatore a funzione fornito da Gestione moduli viene usato per chiamare la funzione dispatch di Gestione moduli con l'ID associato ***al tx_thread_relinquish*** servizio. Questo servizio non accetta parametri.

## <a name="module-example"></a>Esempio di modulo

Di seguito è riportato un esempio della dimostrazione threadX standard sotto forma di modulo. Le differenze principali tra la dimostrazione di ThreadX standard e la dimostrazione del modulo sono.

1. Sostituzione di ***tx_api.h** _ con _ *_txm_module.h_**
2. Aggiunta di **#define TXM_MODULE** prima di **_txm_module.h_**
3. Sostituzione di ***main** _ e _ *tx_application_define** con **_demo_module_start_**
4. Dichiarazione di *puntatori* a oggetti ThreadX anziché agli oggetti stessi.

```c
/* Specify that this is a module! */
#define TXM_MODULE

/* Include the ThreadX module header. */
#include "txm_module.h"

/* Define constants. */
#define DEMO_STACK_SIZE         1024
#define DEMO_BYTE_POOL_SIZE     9120
#define DEMO_BLOCK_POOL_SIZE    100
#define DEMO_QUEUE_SIZE         100

/* Define the pool space in the bss section of the module. ULONG is used to
   get word alignment. */
   
ULONG                   demo_module_pool_space[DEMO_BYTE_POOL_SIZE / 4];

/* Define the ThreadX object control block pointers. */

TX_THREAD               *thread_0;
TX_THREAD               *thread_1;
TX_THREAD               *thread_2;
TX_THREAD               *thread_3;
TX_THREAD               *thread_4;
TX_THREAD               *thread_5;
TX_THREAD               *thread_6;
TX_THREAD               *thread_7;
TX_QUEUE                *queue_0;
TX_SEMAPHORE            *semaphore_0;
TX_MUTEX                *mutex_0;
TX_EVENT_FLAGS_GROUP    *event_flags_0;
TX_BYTE_POOL            *byte_pool_0;
TX_BLOCK_POOL           *block_pool_0;


/* Define the counters used in the demo application. */
ULONG       thread_0_counter;
ULONG       thread_1_counter;
ULONG       thread_1_messages_sent;
ULONG       thread_2_counter;
ULONG       thread_2_messages_received;
ULONG       thread_3_counter;
ULONG       thread_4_counter;
ULONG       thread_5_counter;
ULONG       thread_6_counter;
ULONG       thread_7_counter;
ULONG       semaphore_0_puts;
ULONG       event_0_sets;
ULONG       queue_0_sends;

/* Define thread prototypes. */

void    thread_0_entry(ULONG thread_input);
void    thread_1_entry(ULONG thread_input);
void    thread_2_entry(ULONG thread_input);
void    thread_3_and_4_entry(ULONG thread_input);
void    thread_5_entry(ULONG thread_input);
void    thread_6_and_7_entry(ULONG thread_input);

/* Define notify functions. */

void semaphore_0_notify(TX_SEMAPHORE *semaphore_ptr)
{
    if (semaphore_ptr == semaphore_0)
        semaphore_0_puts++;
}


void event_0_notify(TX_EVENT_FLAGS_GROUP *event_flag_group_ptr)
{
    if (event_flag_group_ptr == event_flags_0)
        event_0_sets++;
}


void queue_0_notify(TX_QUEUE *queue_ptr)
{
    if (queue_ptr == queue_0)
        queue_0_sends++;
}

/* Define the module start function. */
void demo_module_start(ULONG id)
{
    CHAR *pointer;

    /* Allocate all the objects. In memory protection mode,
        modules cannot allocate control blocks within their
        own memory area so they cannot corrupt the resident
        portion of ThreadX by corrupting the control block(s). */
    txm_module_object_allocate(&thread_0, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_1, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_2, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_3, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_4, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_5, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_6, sizeof(TX_THREAD));
    txm_module_object_allocate(&thread_7, sizeof(TX_THREAD));
    txm_module_object_allocate(&queue_0, sizeof(TX_QUEUE));
    txm_module_object_allocate(&semaphore_0, sizeof(TX_SEMAPHORE));
    txm_module_object_allocate(&mutex_0, sizeof(TX_MUTEX));
    txm_module_object_allocate(&event_flags_0, sizeof(TX_EVENT_FLAGS_GROUP));
    txm_module_object_allocate(&byte_pool_0, sizeof(TX_BYTE_POOL));
    txm_module_object_allocate(&block_pool_0, sizeof(TX_BLOCK_POOL));

    /* Create a byte memory pool from which to allocate the thread stacks. */
    tx_byte_pool_create(byte_pool_0, "module byte pool 0",
        demo_module_pool_space, DEMO_BYTE_POOL_SIZE);

    /* Allocate the stack for thread 0. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create thread 0. */
    tx_thread_create(thread_0, "module thread 0", thread_0_entry, 0,
        pointer, DEMO_STACK_SIZE,
        1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 1. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 1 and 2. These threads pass information through
        a ThreadX message queue. It is also interesting to note that
        these threads have a time slice. */
    tx_thread_create(thread_1, "module thread 1", thread_1_entry, 1,
        pointer, DEMO_STACK_SIZE,
        16, 16, 4, TX_AUTO_START);

    /* Allocate the stack and create thread 2. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);
    tx_thread_create(thread_2, "module thread 2", thread_2_entry, 2,
        pointer, DEMO_STACK_SIZE,
        16, 16, 4, TX_AUTO_START);

    /* Allocate the stack for thread 3. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 3 and 4. These threads compete for a ThreadX
        counting semaphore. An interesting thing here is that both threads
        share the same instruction area. */
    tx_thread_create(thread_3, "module thread 3",
        thread_3_and_4_entry, 3,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack and create thread 4. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);
    tx_thread_create(thread_4, "module thread 4",
        thread_3_and_4_entry, 4,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 5. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create thread 5. This thread simply pends on an event flag which
        will be set by thread 0. */
    tx_thread_create(thread_5, "module thread 5", thread_5_entry, 5,
        pointer, DEMO_STACK_SIZE,
        4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack for thread 6. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);

    /* Create threads 6 and 7. These threads compete for a ThreadX mutex. */
    tx_thread_create(thread_6, "module thread 6",
        thread_6_and_7_entry, 6,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the stack and create thread 7. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_STACK_SIZE, TX_NO_WAIT);
    tx_thread_create(thread_7, "module thread 7",
        thread_6_and_7_entry, 7,
        pointer, DEMO_STACK_SIZE,
        8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Allocate the message queue. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_QUEUE_SIZE*sizeof(ULONG), TX_NO_WAIT);

    /* Create the message queue shared by threads 1 and 2. */
    tx_queue_create(queue_0, "module queue 0", TX_1_ULONG, pointer,
        DEMO_QUEUE_SIZE*sizeof(ULONG));

    /* Register queue send callback. */
    tx_queue_send_notify(queue_0, queue_0_notify);

    /* Create the semaphore used by threads 3 and 4. */
    tx_semaphore_create(semaphore_0, "module semaphore 0", 1);

    /* Register semaphore put callback. */
    tx_semaphore_put_notify(semaphore_0, semaphore_0_notify);

    /* Create the event flags group used by threads 1 and 5. */
    tx_event_flags_create(event_flags_0, "module event flags 0");

    /* Register event flag set callback. */
    tx_event_flags_set_notify(event_flags_0, event_0_notify);

    /* Create the mutex used by thread 6 and 7 without priority
        inheritance. */
    tx_mutex_create(mutex_0, "module mutex 0", TX_NO_INHERIT);

    /* Allocate the memory for a small block pool. */
    tx_byte_allocate(byte_pool_0, (VOID **) &pointer,
        DEMO_BLOCK_POOL_SIZE, TX_NO_WAIT);

    /* Create a block memory pool. */
    tx_block_pool_create(block_pool_0, "module block pool 0",
        sizeof(ULONG), pointer, DEMO_BLOCK_POOL_SIZE);

    /* Allocate a block. */
    tx_block_allocate(block_pool_0, (VOID **) &pointer,
        TX_NO_WAIT);

    /* Release the block back to the pool. */
    tx_block_release(pointer);

}

/* Define all the threads. */

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

        /* Set event flag 0 to wake up thread 5. */
        status = tx_event_flags_set(event_flags_0, 0x1, TX_OR);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;
    }
}

void thread_1_entry(ULONG thread_input)
{
    UINT status;

    /* This thread simply sends messages to a queue shared by
       thread 2. */
    while(1)
    {
        /* Increment the thread counter. */
        thread_1_counter++;

        /* Send message to queue 0. */
        status = tx_queue_send(queue_0, &thread_1_messages_sent,
            TX_WAIT_FOREVER);

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
        status = tx_queue_receive(queue_0, &received_message, TX_WAIT_FOREVER);

        /* Check completion status and make sure the message is what
           we expected. */
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
        status = tx_semaphore_get(semaphore_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Sleep for 2 ticks to hold the semaphore. */
        tx_thread_sleep(2);

        /* Release the semaphore. */
        status = tx_semaphore_put(semaphore_0);

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
        status = tx_event_flags_get(event_flags_0, 0x1, TX_OR_CLEAR,
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
        status = tx_mutex_get(mutex_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Get the mutex again with suspension. This shows that an
           owning thread may retrieve the mutex it owns multiple times. */
        status = tx_mutex_get(mutex_0, TX_WAIT_FOREVER);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Sleep for 2 ticks to hold the mutex. */
        tx_thread_sleep(2);

        /* Release the mutex. */
        status = tx_mutex_put(mutex_0);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;

        /* Release the mutex again. This will actually release ownership
           since it was obtained twice. */
        status = tx_mutex_put(mutex_0);

        /* Check status. */
        if (status != TX_SUCCESS)
            break;
    }
}
```

## <a name="building-modules"></a>Compilazione di moduli

La compilazione di un modulo dipende dalla catena di strumenti in uso. Vedere [l'appendice](appendix.md) per esempi specifici della porta. Le attività comuni per tutte le porte includono quanto segue.

- Compilazione di una libreria di moduli
- Compilazione dell'applicazione del modulo

Ogni modulo deve avere un txm_module_preamble **(configurazione** specifica per il modulo) e la libreria di moduli (ad **_esempio, txm.a_**).
