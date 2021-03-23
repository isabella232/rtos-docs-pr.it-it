---
title: Capitolo 3-requisiti di gestione moduli
description: Questo articolo descrive i passaggi necessari per la creazione di gestione moduli ThreadX.
author: philmea
ms.author: philmea
ms.date: 07/15/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e8ea1a05096b5975de203648fddfb19c1a6105e0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822499"
---
# <a name="chapter-3---module-manager-requirements"></a>Capitolo 3-requisiti di gestione moduli

Gestione moduli ThreadX risiede nella parte residente dell'applicazione insieme al RTO ThreadX. È responsabile dell'avvio del modulo, nonché dell'invio in campo e dell'invio di tutte le richieste di moduli per i servizi API ThreadX.

> [!NOTE]
> I file di origine di ThreadX module **Manager** (C e assembly) devono essere aggiunti al progetto di libreria threadX "**TX**".

I passaggi seguenti sono necessari per la compilazione di ThreadX Module Manager (ogni passaggio è descritto in dettaglio più avanti).

1. È necessario estendere il blocco di controllo **TX_THREAD** per includere le informazioni sul modulo. Il modo più semplice per eseguire questa operazione consiste nel sostituire la definizione di **TX_THREAD_EXTENSION_2** nel **file _tx_port. h_*_ con la _* TX_THREAD_EXTENSION_2** trovata in **_txm_module_port. h_**. Vedere [appendice](appendix.md) per le estensioni specifiche delle porte.

Estensione di esempio:

   ```c
   #define TX_THREAD_EXTENSION_2                     \
       VOID      tx_thread_module_instance_ptr;      \
       VOID      tx_thread_module_entry_info_ptr;    \
       ULONG     tx_thread_module_current_user_mode; \
       ULONG     tx_thread_module_user_mode;         \
       VOID     *tx_thread_module_kernel_stack_start;\
       VOID     *tx_thread_module_kernel_stack_end;  \
       ULONG     tx_thread_module_kernel_stack_size; \
       VOID     *tx_thread_module_stack_ptr;         \
       VOID     *tx_thread_module_stack_start;       \
       VOID     *tx_thread_module_stack_end;         \
       ULONG     tx_thread_module_stack_size;        \
       VOID     *tx_thread_module_reserved;
   ```

   In ***tx_port. h*** è necessario definire le estensioni seguenti.

   ```c
   #define TX_EVENT_FLAGS_GROUP_EXTENSION  VOID    *tx_event_flags_group_module_instance; \
        VOID   (*tx_event_flags_group_set_module_notify)(struct TX_EVENT_FLAGS_GROUP_STRUCT *group_ptr);

   #define TX_QUEUE_EXTENSION              VOID    *tx_queue_module_instance; \
        VOID   (*tx_queue_send_module_notify)(struct TX_QUEUE_STRUCT *queue_ptr);

   #define TX_SEMAPHORE_EXTENSION          VOID    *tx_semaphore_module_instance; \
        VOID   (*tx_semaphore_put_module_notify)(struct TX_SEMAPHORE_STRUCT *semaphore_ptr);

   #define TX_TIMER_EXTENSION              VOID    *tx_timer_module_instance; \
        VOID   (*tx_timer_module_expiration_function)(ULONG id);
   ```

2. Aggiungere tutti i ***file \* txm_module_manager_*** C e assembly al progetto di libreria threadX **_TX_**.
3. Ricompila tutte le librerie e i progetti eseguibili. Se è necessario NetX Duo, è necessario compilare tutti i moduli e il codice C di Module Manager con **TXM_MODULE_ENABLE_NETX_DUO** definito.

## <a name="module-manager-sources"></a>Origini di gestione moduli

Gestione moduli ThreadX dispone di un set di file di origine progettati per essere collegati e situati direttamente con il codice ThreadX residente. Questi file offrono la possibilità di avviare un modulo e il campo delle richieste API ThreadX successive dal modulo. I file di gestione moduli sono i seguenti.

| **Nome file** |  **Contents** |
|-------------- | ------------- |
| ***txm_module. h*** | File di inclusione che definisce le informazioni sui moduli (incluse anche nel codice sorgente del modulo). |
| ***txm_module_manager_dispatch. h*** | File di inclusione che definisce le funzioni di supporto dispatch.|
| ***txm_module_manager_util. h*** | File di inclusione che definisce le macro helper dell'utilità interna & funzioni. |
| ***txm_module_port. h*** | File di inclusione che definisce le informazioni sul modulo specifiche della porta (incluse anche nel codice sorgente del modulo). |
| ***tx_initialize_low_level. \[ s, S, 68 \]** _ | Sostituisce il file della libreria ThreadX esistente. Tabella Vector aggiornata e gestori di vettori aggiuntivi per le eccezioni di memoria e gestione dei moduli. _This file è solo in Cortex-A7/ARM, Cortex-M7/ARM, Cortex-R4/ARM, Cortex-R4/IAR, MCF544xx/GHS, RX63/IAR, RX65N/IAR. *|
| ***tx_thread_context_restore. s** _ | Sostituisce il file della libreria ThreadX esistente. Ripristinare il contesto del thread dopo l'elaborazione dell'interrupt. _This file è solo in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR. *|
| ***tx_thread_schedule. \[ s, S, 68\]*** | Sostituisce il file della libreria ThreadX esistente. Codice dell'utilità di pianificazione esteso, che in questo caso viene usato per aggiornare i registri di gestione della memoria. |
| ***tx_thread_stack_build. s** _ | Sostituisce il file della libreria ThreadX esistente. Compila la stack frame di un thread. _This file è solo in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR. *|
| ***txm_module_manager_thread_stack_build. \[ s, S, 68\]*** | Compila tutti gli stack iniziali del modulo, inclusa la configurazione per l'accesso ai dati indipendente dalla posizione. |
| ***txm_module_manager_user_mode_entry. \[ s, S \]** _ | Consente al modulo di passare alla modalità kernel. _This file è solo in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR. *|
| ***txm_module_manager_alignment_adjust. c*** | Gestisce i requisiti di allineamento specifici delle porte.|
| ***txm_module_manager_application_request. c*** | Gestisce le richieste specifiche dell'applicazione al codice residente. |
| ***txm_module_manager_callback_request. c*** | Invia una richiesta di callback a un modulo. |
| ***txm_module_manager_event_flags_notify_trampoline. c*** | Elabora la chiamata di notifica del set di flag di evento da ThreadX. |
| ***txm_module_manager_external_memory_enable. c*** | Crea una voce nella tabella di gestione della memoria per uno spazio di memoria condiviso a cui può accedere il modulo. |
| ***txm_module_manager_file_load. c*** | Alloca e carica un file di modulo binario nell'area di memoria del modulo e lo prepara per l'esecuzione. |
| ***txm_module_manager_in_place_load. c*** | Alloca l'area dati del modulo e prepara l'esecuzione del modulo dall'indirizzo del codice fornito. |
| ***txm_module_manager_initialize. c*** | Inizializza la gestione dei moduli, inclusa la specifica dell'area di memoria del modulo disponibile per il caricamento e l'esecuzione di moduli. |
| ***txm_module_manager_initialize_mmu. c** _ | Inizializzare MMU. Gli utenti possono modificare questo file in base alla mappa di memoria. _This file è solo in Cortex-A7/ARM * |
| ***txm_module_manager_mm_initialize. c** _ | Inizializzare MPU/MMU. Gli utenti possono modificare questo file in base alla mappa di memoria. _This file è solo in Cortex-A7/ARM * |
| ***txm_module_manager_kernel_dispatch. c*** | Gestisce le richieste API del modulo in base all'ID richiesta. |
| ***txm_module_manager_maximum_module_priority_set. c*** | Imposta la priorità massima dei thread consentita in un modulo. |
| ***txm_module_manager_memory_fault_handler. c*** | Gestisce gli errori di memoria rilevati in un modulo in esecuzione. |
| ***txm_module_manager_memory_fault_notify. c*** | Registra un callback di notifica dell'applicazione ogni volta che si verifica un errore di memoria. |
| ***txm_module_manager_memory_load. c*** | Alloca e carica il codice e i dati di un modulo e prepara il modulo per l'esecuzione. |
| ***txm_module_manager_mm_register_setup. c*** | Imposta i registri MPU/MMU per il modulo in base alla posizione in cui vengono caricati il codice e i dati. |
| ***txm_module_manager_object_allocate. c*** | Alloca memoria per un oggetto modulo. |
| ***txm_module_manager_object_deallocate. c*** | Dealloca la memoria per un oggetto modulo. |
| ***txm_module_manager_object_pointer_get. c*** | Cerca il tipo di oggetto e il nome specificati e, se presente, restituisce il puntatore all'oggetto. |
| ***txm_module_manager_object_pointer_get_extended. c*** | Cerca il tipo di oggetto e il nome specificati e, se presente, restituisce il puntatore all'oggetto. Lunghezza del nome specificata per la sicurezza. |
| ***txm_module_manager_object_pool_create. c***  | Crea un pool di oggetti all'esterno dell'area dati del modulo da cui possono essere allocate le applicazioni del modulo. |
| ***txm_module_manager_properties_get. c*** | Ottiene le proprietà del modulo specificato. |
| ***txm_module_manager_queue_notify_trampoline. c*** | Elabora la chiamata di notifica della coda da ThreadX. |
| ***txm_module_manager_semaphore_notify_trampoline. c*** | Elabora la chiamata di notifica put del semaforo da ThreadX.|
| ***txm_module_manager_start. c*** | Avvia l'esecuzione di un modulo. |
| ***txm_module_manager_stop. c*** | Arresta l'esecuzione di un modulo. |
| ***txm_module_manager_thread_create. c*** | Crea tutti i thread del modulo. |
| ***txm_module_manager_thread_notify_trampoline. c*** | Elabora la chiamata di notifica di entrata/uscita del thread da ThreadX. |
| ***txm_module_manager_thread_reset. c*** | Reimpostare un thread del modulo. |
| ***txm_module_manager_timer_notify_trampoline. c*** | Elabora le scadenze del timer da ThreadX. |
| ***txm_module_manager_unload. c*** | Scarica il modulo dall'area memoria del modulo. |
| ***txm_module_manager_util. c*** | Funzioni helper interne per Manager. |

## <a name="module-manager-initialization"></a>Inizializzazione di gestione moduli

La parte residente dell'applicazione è responsabile della chiamata della funzione di inizializzazione di gestione moduli ***txm_module_manager_initialize***. Questa funzione configura le strutture interne per il caricamento e lo scaricamento dei moduli, inclusa la configurazione dell'area di memoria usata per l'allocazione della memoria del modulo.

## <a name="module-manager-loading"></a>Caricamento di gestione moduli

Gestione moduli può caricare i moduli dinamicamente nella memoria del modulo da file di modulo binari o da una sezione di codice del modulo già presente nell'area di codice residente. Inoltre, il gestore di moduli può eseguire codice sul posto, ovvero solo i dati del modulo vengono allocati nella memoria del modulo e l'esecuzione del codice viene eseguita sul posto. Sono disponibili le funzioni API di caricamento di gestione moduli seguenti.

* ***txm_module_manager_file_load***

* ***txm_module_manager_in_place_load***

* ***txm_module_manager_memory_load***

La versione protetta dalla memoria di gestione moduli garantisce inoltre che il modulo venga caricato con l'allineamento corretto e che i registri di gestione della memoria siano impostati correttamente per ogni modulo. Quando la protezione della memoria viene abilitata tramite le opzioni del preambolo del modulo, l'accesso alla memoria del modulo è limitato al codice e alle aree dati del modulo.

## <a name="module-manager-starting"></a>Avvio di gestione moduli

Il gestore dei moduli avvia l'esecuzione di un modulo caricato in precedenza tramite la funzione API ***txm_module_manager_start*** . Per avviare l'esecuzione del modulo, questa funzione crea un thread che accede al modulo nella posizione iniziale specificata nel preambolo del modulo. La priorità e le dimensioni dello stack di questo thread sono specificate anche nel preambolo del modulo.

## <a name="module-manager-stopping"></a>Arresto di gestione moduli

Gestione moduli termina l'esecuzione di un modulo caricato in precedenza ed eseguendo il modulo tramite la funzione ***txm_module_manager_stop*** . Questa funzione API termina prima ed Elimina il thread iniziale iniziale. Se il preambolo del modulo specifica un thread di arresto, questo thread viene creato ed eseguito. Gestione moduli attende un periodo di tempo fisso per il completamento del thread di arresto. Al termine, vengono eliminate tutte le risorse di sistema create dal modulo e il modulo viene inserito in uno stato inattivo, dal quale può essere riavviato o scaricato.

## <a name="module-manager-unloading"></a>Scaricamento di gestione moduli

Il gestore dei moduli Scarica un modulo caricato in precedenza ma non in esecuzione tramite la funzione ***txm_module_manager_unload*** . Questa API rilascia tutta la memoria associata al modulo, che verrà liberata per l'uso con un altro modulo in futuro.

## <a name="module-manager-requests"></a>Richieste di gestione moduli

Le richieste effettuate dai moduli al gestore dei moduli vengono eseguite tramite le macro in ***txm_module. h*** che eseguono il mapping di tutte le chiamate threadX per chiamare la funzione di invio di gestione moduli tramite un puntatore a funzione fornito al modulo da Gestione moduli.

I servizi aggiuntivi specifici dell'applicazione creati tramite il modulo che chiama ***txm_module_application_request*** vengono gestiti dallo stesso meccanismo macro usato per l'API threadX. Per impostazione predefinita, questa funzione di gestione in Gestione moduli è vuota e progettata in modo tale che l'applicazione aggiunga il codice necessario per elaborare le richieste specifiche dell'applicazione.

Se la richiesta non è implementata da Gestione moduli, viene restituito un valore di **TX_NOT_AVAILABLE** stato di errore da Gestione moduli. Questo codice di errore viene restituito anche se il modulo richiede un'operazione che esula dall'ambito dell'accesso del modulo. Un modulo, ad esempio, non è autorizzato a creare un timer con il blocco di controllo timer o l'indirizzo di callback al di fuori dell'area di codice del modulo.

## <a name="module-manager-example"></a>Esempio di gestione moduli

Di seguito è riportato un esempio di codice di gestione dei moduli che avvia il modulo di esempio precedentemente definito nel capitolo 2. Si presuppone che il modulo sia già caricato, presumibilmente dal debugger, all'indirizzo ROM 0x00800000.

```c
#include "tx_api.h"
#include "txm_module.h"

#define DEMO_STACK_SIZE 1024

/* Define the ThreadX object control blocks. */
TX_THREAD   module_manager;

/* Define thread prototype. */
void        module_manager_entry(ULONG thread_input);

/* Define the module object pool area. */
UCHAR       object_memory[8192];

/* Define the module data pool area. */
#define MODULE_DATA_SIZE 65536
UCHAR       module_data_area[MODULE_DATA_SIZE];

/* Define module instances. */
TXM_MODULE_INSTANCE     my_module1;
TXM_MODULE_INSTANCE     my_module2;

/* Define the count of memory faults. */
ULONG memory_faults;

/* Define fault handler. */
VOID module_fault_handler(TX_THREAD *thread, TXM_MODULE_INSTANCE *module)
{
    /* Just increment the fault counter. */
    memory_faults++;
}

/* Define main entry point. */
int main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */
void tx_application_define(void *first_unused_memory)
{
    /* Create the module manager thread. */
    tx_thread_create(&module_manager, "Module Manager Thread", module_manager_entry, 0,
                    first_unused_memory, DEMO_STACK_SIZE,
                    1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);
}

/* Define the test threads. */
void module_manager_entry(ULONG thread_input)
{
    /* Initialize the module manager. */
    txm_module_manager_initialize((VOID *) module_data_area, MODULE_DATA_SIZE);

    /* Create a pool for module objects. */
    txm_module_manager_object_pool_create(object_memory, sizeof(object_memory));

    /* Register a fault handler. */
    txm_module_manager_memory_fault_notify(module_fault_handler);

    /* Load the module that is already there,
        in this example it is placed at 0x00800000. */
    txm_module_manager_in_place_load(&my_module1, "my module1", (VOID *) 0x00800000);

    /* Load a second instance of the module. */
    txm_module_manager_in_place_load(&my_module2, "my module2", (VOID *) 0x00800000);

    /* Enable shared memory region for module2. */
    txm_module_manager_external_memory_enable(&my_module2, (void*)0x20600000, 0x010000, 0x3F);

    /* Start the modules. */
    txm_module_manager_start(&my_module1);
    txm_module_manager_start(&my_module2);

    /* Sleep for a while and let the modules run... */
    tx_thread_sleep(300);

    /* Stop the modules. */
    txm_module_manager_stop(&my_module1);
    txm_module_manager_stop(&my_module2);

    /* Unload the modules. */
    txm_module_manager_unload(&my_module1);
    txm_module_manager_unload(&my_module2);

    /* Reload the modules. */
    txm_module_manager_in_place_load(&my_module2, "my module2", (VOID *) 0x00800000);
    txm_module_manager_in_place_load(&my_module1, "my module1", (VOID *) 0x00800000);

    /* Give both modules shared memory. */
    txm_module_manager_external_memory_enable(&my_module2, (void*)0x20600000, 0x010000, 0x3F);
    txm_module_manager_external_memory_enable(&my_module1, (void*)0x20600000, 0x010000, 0x3F);

    /* Set maximum module1 priority to 5. */
    txm_module_manager_maximum_module_priority_set(&my_module1, 5);

    /* Start the modules again. */
    txm_module_manager_start(&my_module2);
    txm_module_manager_start(&my_module1);

    /* Now just spin... */
    while(1)
    {
        tx_thread_sleep(100);

        /* Threads 0 and 5 in module1 are not created because they violate the maximum priority. */
    }
}
```

## <a name="module-manager-building"></a>Compilazione di gestione moduli

I file di origine del ***txm_module_manager_ \**** devono essere aggiunti alla libreria threadX.

Un'applicazione di gestione moduli ThreadX è in realtà identica a un'applicazione ThreadX standard, ovvero uno o più file di applicazione collegati con la libreria ThreadX ***TX. a***. La compilazione di un'applicazione di gestione moduli dipende dalla catena di strumenti utilizzata. Vedere l' [appendice](appendix.md) per esempi specifici delle porte.
