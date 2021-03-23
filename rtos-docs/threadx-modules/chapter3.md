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
# <a name="chapter-3---module-manager-requirements"></a><span data-ttu-id="69c76-103">Capitolo 3-requisiti di gestione moduli</span><span class="sxs-lookup"><span data-stu-id="69c76-103">Chapter 3 - Module Manager requirements</span></span>

<span data-ttu-id="69c76-104">Gestione moduli ThreadX risiede nella parte residente dell'applicazione insieme al RTO ThreadX.</span><span class="sxs-lookup"><span data-stu-id="69c76-104">The ThreadX Module Manager resides in the resident portion of the application along with the ThreadX RTOS.</span></span> <span data-ttu-id="69c76-105">È responsabile dell'avvio del modulo, nonché dell'invio in campo e dell'invio di tutte le richieste di moduli per i servizi API ThreadX.</span><span class="sxs-lookup"><span data-stu-id="69c76-105">It is responsible for starting the module as well as fielding and dispatching all module requests for ThreadX API services.</span></span>

> [!NOTE]
> <span data-ttu-id="69c76-106">I file di origine di ThreadX module **Manager** (C e assembly) devono essere aggiunti al progetto di libreria threadX "**TX**".</span><span class="sxs-lookup"><span data-stu-id="69c76-106">The ThreadX Module **Manager** source files (C and assembly) should be added to the ThreadX library project "**tx**".</span></span>

<span data-ttu-id="69c76-107">I passaggi seguenti sono necessari per la compilazione di ThreadX Module Manager (ogni passaggio è descritto in dettaglio più avanti).</span><span class="sxs-lookup"><span data-stu-id="69c76-107">The following steps are required for building the ThreadX Module Manager (each step is described in greater detail below).</span></span>

1. <span data-ttu-id="69c76-108">È necessario estendere il blocco di controllo **TX_THREAD** per includere le informazioni sul modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-108">The **TX_THREAD** control block must be extended to include module information.</span></span> <span data-ttu-id="69c76-109">Il modo più semplice per eseguire questa operazione consiste nel sostituire la definizione di **TX_THREAD_EXTENSION_2** nel **file _tx_port. h_*_ con la _\* TX_THREAD_EXTENSION_2*\* trovata in **_txm_module_port. h_**.</span><span class="sxs-lookup"><span data-stu-id="69c76-109">The easiest way to accomplish this is to replace the definition of **TX_THREAD_EXTENSION_2** in the **_tx_port.h_*_ file with the _\* TX_THREAD_EXTENSION_2*\* found in **_txm_module_port.h_**.</span></span> <span data-ttu-id="69c76-110">Vedere [appendice](appendix.md) per le estensioni specifiche delle porte.</span><span class="sxs-lookup"><span data-stu-id="69c76-110">See [appendix](appendix.md) for port-specific extensions.</span></span>

<span data-ttu-id="69c76-111">Estensione di esempio:</span><span class="sxs-lookup"><span data-stu-id="69c76-111">Example extension:</span></span>

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

   <span data-ttu-id="69c76-112">In ***tx_port. h*** è necessario definire le estensioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="69c76-112">The following extensions must be defined in ***tx_port.h***.</span></span>

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

2. <span data-ttu-id="69c76-113">Aggiungere tutti i ***file \* txm_module_manager_*** C e assembly al progetto di libreria threadX **_TX_**.</span><span class="sxs-lookup"><span data-stu-id="69c76-113">Add all the ***txm_module_manager_\**** C and assembly files to the ThreadX library project **_tx_**.</span></span>
3. <span data-ttu-id="69c76-114">Ricompila tutte le librerie e i progetti eseguibili.</span><span class="sxs-lookup"><span data-stu-id="69c76-114">Rebuild all libraries and executable projects.</span></span> <span data-ttu-id="69c76-115">Se è necessario NetX Duo, è necessario compilare tutti i moduli e il codice C di Module Manager con **TXM_MODULE_ENABLE_NETX_DUO** definito.</span><span class="sxs-lookup"><span data-stu-id="69c76-115">If NetX Duo is required, all Module and Module Manager C code should be built with **TXM_MODULE_ENABLE_NETX_DUO** defined.</span></span>

## <a name="module-manager-sources"></a><span data-ttu-id="69c76-116">Origini di gestione moduli</span><span class="sxs-lookup"><span data-stu-id="69c76-116">Module Manager sources</span></span>

<span data-ttu-id="69c76-117">Gestione moduli ThreadX dispone di un set di file di origine progettati per essere collegati e situati direttamente con il codice ThreadX residente.</span><span class="sxs-lookup"><span data-stu-id="69c76-117">The ThreadX Module Manager has a set of source files that are designed to be linked and located directly with the resident ThreadX code.</span></span> <span data-ttu-id="69c76-118">Questi file offrono la possibilità di avviare un modulo e il campo delle richieste API ThreadX successive dal modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-118">These files provide the ability to launch a module and field subsequent ThreadX API requests from the module.</span></span> <span data-ttu-id="69c76-119">I file di gestione moduli sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="69c76-119">The module manager files are as follows.</span></span>

| <span data-ttu-id="69c76-120">**Nome file**</span><span class="sxs-lookup"><span data-stu-id="69c76-120">**File Name**</span></span> |  <span data-ttu-id="69c76-121">**Contents**</span><span class="sxs-lookup"><span data-stu-id="69c76-121">**Contents**</span></span> |
|-------------- | ------------- |
| <span data-ttu-id="69c76-122">***txm_module. h***</span><span class="sxs-lookup"><span data-stu-id="69c76-122">***txm_module.h***</span></span> | <span data-ttu-id="69c76-123">File di inclusione che definisce le informazioni sui moduli (incluse anche nel codice sorgente del modulo).</span><span class="sxs-lookup"><span data-stu-id="69c76-123">Include file that defines module information (also included in the module source code).</span></span> |
| <span data-ttu-id="69c76-124">***txm_module_manager_dispatch. h***</span><span class="sxs-lookup"><span data-stu-id="69c76-124">***txm_module_manager_dispatch.h***</span></span> | <span data-ttu-id="69c76-125">File di inclusione che definisce le funzioni di supporto dispatch.</span><span class="sxs-lookup"><span data-stu-id="69c76-125">Include file that defines dispatch helper functions.</span></span>|
| <span data-ttu-id="69c76-126">***txm_module_manager_util. h***</span><span class="sxs-lookup"><span data-stu-id="69c76-126">***txm_module_manager_util.h***</span></span> | <span data-ttu-id="69c76-127">File di inclusione che definisce le macro helper dell'utilità interna & funzioni.</span><span class="sxs-lookup"><span data-stu-id="69c76-127">Include file that defines internal utility helper macros & functions.</span></span> |
| <span data-ttu-id="69c76-128">***txm_module_port. h***</span><span class="sxs-lookup"><span data-stu-id="69c76-128">***txm_module_port.h***</span></span> | <span data-ttu-id="69c76-129">File di inclusione che definisce le informazioni sul modulo specifiche della porta (incluse anche nel codice sorgente del modulo).</span><span class="sxs-lookup"><span data-stu-id="69c76-129">Include file that defines port-specific module information (also included in the module source code).</span></span> |
| <span data-ttu-id="69c76-130">\***tx_initialize_low_level. \[ s, S, 68 \]** _</span><span class="sxs-lookup"><span data-stu-id="69c76-130">\***tx_initialize_low_level.\[s,S,68\]** _</span></span> | <span data-ttu-id="69c76-131">Sostituisce il file della libreria ThreadX esistente.</span><span class="sxs-lookup"><span data-stu-id="69c76-131">Replaces existing ThreadX library file.</span></span> <span data-ttu-id="69c76-132">Tabella Vector aggiornata e gestori di vettori aggiuntivi per le eccezioni di memoria e gestione dei moduli.</span><span class="sxs-lookup"><span data-stu-id="69c76-132">Updated vector table and additional vector handlers for module manager and memory exceptions.</span></span> <span data-ttu-id="69c76-133">_This file è solo in Cortex-A7/ARM, Cortex-M7/ARM, Cortex-R4/ARM, Cortex-R4/IAR, MCF544xx/GHS, RX63/IAR, RX65N/IAR. \*</span><span class="sxs-lookup"><span data-stu-id="69c76-133">_This file is only in Cortex-A7/ARM, Cortex-M7/ARM, Cortex-R4/ARM, Cortex-R4/IAR, MCF544xx/GHS, RX63/IAR, RX65N/IAR.\*</span></span>|
| <span data-ttu-id="69c76-134">\***tx_thread_context_restore. s** _</span><span class="sxs-lookup"><span data-stu-id="69c76-134">\***tx_thread_context_restore.s** _</span></span> | <span data-ttu-id="69c76-135">Sostituisce il file della libreria ThreadX esistente.</span><span class="sxs-lookup"><span data-stu-id="69c76-135">Replaces existing ThreadX library file.</span></span> <span data-ttu-id="69c76-136">Ripristinare il contesto del thread dopo l'elaborazione dell'interrupt.</span><span class="sxs-lookup"><span data-stu-id="69c76-136">Restore thread context after interrupt processing.</span></span> <span data-ttu-id="69c76-137">_This file è solo in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR. \*</span><span class="sxs-lookup"><span data-stu-id="69c76-137">_This file is only in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR.\*</span></span>|
| <span data-ttu-id="69c76-138">***tx_thread_schedule. \[ s, S, 68\]***</span><span class="sxs-lookup"><span data-stu-id="69c76-138">***tx_thread_schedule.\[s,S,68\]***</span></span> | <span data-ttu-id="69c76-139">Sostituisce il file della libreria ThreadX esistente.</span><span class="sxs-lookup"><span data-stu-id="69c76-139">Replaces existing ThreadX library file.</span></span> <span data-ttu-id="69c76-140">Codice dell'utilità di pianificazione esteso, che in questo caso viene usato per aggiornare i registri di gestione della memoria.</span><span class="sxs-lookup"><span data-stu-id="69c76-140">Extended scheduler code, which in this case is used to update memory management registers.</span></span> |
| <span data-ttu-id="69c76-141">\***tx_thread_stack_build. s** _</span><span class="sxs-lookup"><span data-stu-id="69c76-141">\***tx_thread_stack_build.s** _</span></span> | <span data-ttu-id="69c76-142">Sostituisce il file della libreria ThreadX esistente.</span><span class="sxs-lookup"><span data-stu-id="69c76-142">Replaces existing ThreadX library file.</span></span> <span data-ttu-id="69c76-143">Compila la stack frame di un thread.</span><span class="sxs-lookup"><span data-stu-id="69c76-143">Builds the stack frame of a thread.</span></span> <span data-ttu-id="69c76-144">_This file è solo in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR. \*</span><span class="sxs-lookup"><span data-stu-id="69c76-144">_This file is only in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR.\*</span></span>|
| <span data-ttu-id="69c76-145">***txm_module_manager_thread_stack_build. \[ s, S, 68\]***</span><span class="sxs-lookup"><span data-stu-id="69c76-145">***txm_module_manager_thread_stack_build.\[s,S,68\]***</span></span> | <span data-ttu-id="69c76-146">Compila tutti gli stack iniziali del modulo, inclusa la configurazione per l'accesso ai dati indipendente dalla posizione.</span><span class="sxs-lookup"><span data-stu-id="69c76-146">Builds all module initial stacks, includes setup for position-independent data access.</span></span> |
| <span data-ttu-id="69c76-147">\***txm_module_manager_user_mode_entry. \[ s, S \]** _</span><span class="sxs-lookup"><span data-stu-id="69c76-147">\***txm_module_manager_user_mode_entry.\[s,S\]** _</span></span> | <span data-ttu-id="69c76-148">Consente al modulo di passare alla modalità kernel.</span><span class="sxs-lookup"><span data-stu-id="69c76-148">Allows the module to enter kernel mode.</span></span> <span data-ttu-id="69c76-149">_This file è solo in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR. \*</span><span class="sxs-lookup"><span data-stu-id="69c76-149">_This file is only in Cortex-A7/ARM, Cortex-R4/ARM, Cortex-R4/IAR.\*</span></span>|
| <span data-ttu-id="69c76-150">***txm_module_manager_alignment_adjust. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-150">***txm_module_manager_alignment_adjust.c***</span></span> | <span data-ttu-id="69c76-151">Gestisce i requisiti di allineamento specifici delle porte.</span><span class="sxs-lookup"><span data-stu-id="69c76-151">Handles port-specific alignment requirements.</span></span>|
| <span data-ttu-id="69c76-152">***txm_module_manager_application_request. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-152">***txm_module_manager_application_request.c***</span></span> | <span data-ttu-id="69c76-153">Gestisce le richieste specifiche dell'applicazione al codice residente.</span><span class="sxs-lookup"><span data-stu-id="69c76-153">Handles the application-specific requests to the resident code.</span></span> |
| <span data-ttu-id="69c76-154">***txm_module_manager_callback_request. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-154">***txm_module_manager_callback_request.c***</span></span> | <span data-ttu-id="69c76-155">Invia una richiesta di callback a un modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-155">Sends a callback request to a module.</span></span> |
| <span data-ttu-id="69c76-156">***txm_module_manager_event_flags_notify_trampoline. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-156">***txm_module_manager_event_flags_notify_trampoline.c***</span></span> | <span data-ttu-id="69c76-157">Elabora la chiamata di notifica del set di flag di evento da ThreadX.</span><span class="sxs-lookup"><span data-stu-id="69c76-157">Processes the event flags set notification call from ThreadX.</span></span> |
| <span data-ttu-id="69c76-158">***txm_module_manager_external_memory_enable. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-158">***txm_module_manager_external_memory_enable.c***</span></span> | <span data-ttu-id="69c76-159">Crea una voce nella tabella di gestione della memoria per uno spazio di memoria condiviso a cui può accedere il modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-159">Creates an entry in the memory management table for a shared memory space the module can access.</span></span> |
| <span data-ttu-id="69c76-160">***txm_module_manager_file_load. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-160">***txm_module_manager_file_load.c***</span></span> | <span data-ttu-id="69c76-161">Alloca e carica un file di modulo binario nell'area di memoria del modulo e lo prepara per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="69c76-161">Allocates and loads a binary module file into the module memory area and prepares it for execution.</span></span> |
| <span data-ttu-id="69c76-162">***txm_module_manager_in_place_load. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-162">***txm_module_manager_in_place_load.c***</span></span> | <span data-ttu-id="69c76-163">Alloca l'area dati del modulo e prepara l'esecuzione del modulo dall'indirizzo del codice fornito.</span><span class="sxs-lookup"><span data-stu-id="69c76-163">Allocates the module data area and prepares for module execution from the supplied code address.</span></span> |
| <span data-ttu-id="69c76-164">***txm_module_manager_initialize. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-164">***txm_module_manager_initialize.c***</span></span> | <span data-ttu-id="69c76-165">Inizializza la gestione dei moduli, inclusa la specifica dell'area di memoria del modulo disponibile per il caricamento e l'esecuzione di moduli.</span><span class="sxs-lookup"><span data-stu-id="69c76-165">Initializes the Module Manager, including specification of the module memory area available for loading and running modules.</span></span> |
| <span data-ttu-id="69c76-166">\***txm_module_manager_initialize_mmu. c** _</span><span class="sxs-lookup"><span data-stu-id="69c76-166">\***txm_module_manager_initialize_mmu.c** _</span></span> | <span data-ttu-id="69c76-167">Inizializzare MMU.</span><span class="sxs-lookup"><span data-stu-id="69c76-167">Initialize MMU.</span></span> <span data-ttu-id="69c76-168">Gli utenti possono modificare questo file in base alla mappa di memoria.</span><span class="sxs-lookup"><span data-stu-id="69c76-168">Users can edit this file according to their memory map.</span></span> <span data-ttu-id="69c76-169">_This file è solo in Cortex-A7/ARM \*</span><span class="sxs-lookup"><span data-stu-id="69c76-169">_This file is only in Cortex-A7/ARM\*</span></span> |
| <span data-ttu-id="69c76-170">\***txm_module_manager_mm_initialize. c** _</span><span class="sxs-lookup"><span data-stu-id="69c76-170">\***txm_module_manager_mm_initialize.c** _</span></span> | <span data-ttu-id="69c76-171">Inizializzare MPU/MMU.</span><span class="sxs-lookup"><span data-stu-id="69c76-171">Initialize MPU/MMU.</span></span> <span data-ttu-id="69c76-172">Gli utenti possono modificare questo file in base alla mappa di memoria.</span><span class="sxs-lookup"><span data-stu-id="69c76-172">Users can edit this file according to their memory map.</span></span> <span data-ttu-id="69c76-173">_This file è solo in Cortex-A7/ARM \*</span><span class="sxs-lookup"><span data-stu-id="69c76-173">_This file is only in Cortex-A7/ARM\*</span></span> |
| <span data-ttu-id="69c76-174">***txm_module_manager_kernel_dispatch. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-174">***txm_module_manager_kernel_dispatch.c***</span></span> | <span data-ttu-id="69c76-175">Gestisce le richieste API del modulo in base all'ID richiesta.</span><span class="sxs-lookup"><span data-stu-id="69c76-175">Handles the module API requests, based on the request ID.</span></span> |
| <span data-ttu-id="69c76-176">***txm_module_manager_maximum_module_priority_set. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-176">***txm_module_manager_maximum_module_priority_set.c***</span></span> | <span data-ttu-id="69c76-177">Imposta la priorità massima dei thread consentita in un modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-177">Sets the maximum thread priority allowed in a module.</span></span> |
| <span data-ttu-id="69c76-178">***txm_module_manager_memory_fault_handler. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-178">***txm_module_manager_memory_fault_handler.c***</span></span> | <span data-ttu-id="69c76-179">Gestisce gli errori di memoria rilevati in un modulo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="69c76-179">Handles memory faults detected in an executing module.</span></span> |
| <span data-ttu-id="69c76-180">***txm_module_manager_memory_fault_notify. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-180">***txm_module_manager_memory_fault_notify.c***</span></span> | <span data-ttu-id="69c76-181">Registra un callback di notifica dell'applicazione ogni volta che si verifica un errore di memoria.</span><span class="sxs-lookup"><span data-stu-id="69c76-181">Registers an application notification callback whenever a memory fault occurs.</span></span> |
| <span data-ttu-id="69c76-182">***txm_module_manager_memory_load. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-182">***txm_module_manager_memory_load.c***</span></span> | <span data-ttu-id="69c76-183">Alloca e carica il codice e i dati di un modulo e prepara il modulo per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="69c76-183">Allocates and loads a module's code and data and prepares the module for execution.</span></span> |
| <span data-ttu-id="69c76-184">***txm_module_manager_mm_register_setup. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-184">***txm_module_manager_mm_register_setup.c***</span></span> | <span data-ttu-id="69c76-185">Imposta i registri MPU/MMU per il modulo in base alla posizione in cui vengono caricati il codice e i dati.</span><span class="sxs-lookup"><span data-stu-id="69c76-185">Sets up MPU/MMU registers for the module based on where the code and data are loaded.</span></span> |
| <span data-ttu-id="69c76-186">***txm_module_manager_object_allocate. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-186">***txm_module_manager_object_allocate.c***</span></span> | <span data-ttu-id="69c76-187">Alloca memoria per un oggetto modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-187">Allocates memory for a module object.</span></span> |
| <span data-ttu-id="69c76-188">***txm_module_manager_object_deallocate. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-188">***txm_module_manager_object_deallocate.c***</span></span> | <span data-ttu-id="69c76-189">Dealloca la memoria per un oggetto modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-189">Deallocates memory for a module object.</span></span> |
| <span data-ttu-id="69c76-190">***txm_module_manager_object_pointer_get. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-190">***txm_module_manager_object_pointer_get.c***</span></span> | <span data-ttu-id="69c76-191">Cerca il tipo di oggetto e il nome specificati e, se presente, restituisce il puntatore all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="69c76-191">Searches for the supplied object type and name, and if found, returns the object pointer.</span></span> |
| <span data-ttu-id="69c76-192">***txm_module_manager_object_pointer_get_extended. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-192">***txm_module_manager_object_pointer_get_extended.c***</span></span> | <span data-ttu-id="69c76-193">Cerca il tipo di oggetto e il nome specificati e, se presente, restituisce il puntatore all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="69c76-193">Searches for the supplied object type and name, and if found, returns the object pointer.</span></span> <span data-ttu-id="69c76-194">Lunghezza del nome specificata per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="69c76-194">Name length specified for safety.</span></span> |
| <span data-ttu-id="69c76-195">***txm_module_manager_object_pool_create. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-195">***txm_module_manager_object_pool_create.c***</span></span>  | <span data-ttu-id="69c76-196">Crea un pool di oggetti all'esterno dell'area dati del modulo da cui possono essere allocate le applicazioni del modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-196">Creates a pool of objects outside the module's data area that module applications can allocate from.</span></span> |
| <span data-ttu-id="69c76-197">***txm_module_manager_properties_get. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-197">***txm_module_manager_properties_get.c***</span></span> | <span data-ttu-id="69c76-198">Ottiene le proprietà del modulo specificato.</span><span class="sxs-lookup"><span data-stu-id="69c76-198">Gets the properties of the specified module.</span></span> |
| <span data-ttu-id="69c76-199">***txm_module_manager_queue_notify_trampoline. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-199">***txm_module_manager_queue_notify_trampoline.c***</span></span> | <span data-ttu-id="69c76-200">Elabora la chiamata di notifica della coda da ThreadX.</span><span class="sxs-lookup"><span data-stu-id="69c76-200">Processes the queue notification call from ThreadX.</span></span> |
| <span data-ttu-id="69c76-201">***txm_module_manager_semaphore_notify_trampoline. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-201">***txm_module_manager_semaphore_notify_trampoline.c***</span></span> | <span data-ttu-id="69c76-202">Elabora la chiamata di notifica put del semaforo da ThreadX.</span><span class="sxs-lookup"><span data-stu-id="69c76-202">Processes the semaphore put notification call from ThreadX.</span></span>|
| <span data-ttu-id="69c76-203">***txm_module_manager_start. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-203">***txm_module_manager_start.c***</span></span> | <span data-ttu-id="69c76-204">Avvia l'esecuzione di un modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-204">Starts execution of a module.</span></span> |
| <span data-ttu-id="69c76-205">***txm_module_manager_stop. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-205">***txm_module_manager_stop.c***</span></span> | <span data-ttu-id="69c76-206">Arresta l'esecuzione di un modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-206">Stops execution of a module.</span></span> |
| <span data-ttu-id="69c76-207">***txm_module_manager_thread_create. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-207">***txm_module_manager_thread_create.c***</span></span> | <span data-ttu-id="69c76-208">Crea tutti i thread del modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-208">Creates all module threads.</span></span> |
| <span data-ttu-id="69c76-209">***txm_module_manager_thread_notify_trampoline. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-209">***txm_module_manager_thread_notify_trampoline.c***</span></span> | <span data-ttu-id="69c76-210">Elabora la chiamata di notifica di entrata/uscita del thread da ThreadX.</span><span class="sxs-lookup"><span data-stu-id="69c76-210">Processes the thread entry/exit notification call from ThreadX.</span></span> |
| <span data-ttu-id="69c76-211">***txm_module_manager_thread_reset. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-211">***txm_module_manager_thread_reset.c***</span></span> | <span data-ttu-id="69c76-212">Reimpostare un thread del modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-212">Reset a module thread.</span></span> |
| <span data-ttu-id="69c76-213">***txm_module_manager_timer_notify_trampoline. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-213">***txm_module_manager_timer_notify_trampoline.c***</span></span> | <span data-ttu-id="69c76-214">Elabora le scadenze del timer da ThreadX.</span><span class="sxs-lookup"><span data-stu-id="69c76-214">Processes timer expirations from ThreadX.</span></span> |
| <span data-ttu-id="69c76-215">***txm_module_manager_unload. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-215">***txm_module_manager_unload.c***</span></span> | <span data-ttu-id="69c76-216">Scarica il modulo dall'area memoria del modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-216">Unloads the module from the module memory area.</span></span> |
| <span data-ttu-id="69c76-217">***txm_module_manager_util. c***</span><span class="sxs-lookup"><span data-stu-id="69c76-217">***txm_module_manager_util.c***</span></span> | <span data-ttu-id="69c76-218">Funzioni helper interne per Manager.</span><span class="sxs-lookup"><span data-stu-id="69c76-218">Internal helper functions for manager.</span></span> |

## <a name="module-manager-initialization"></a><span data-ttu-id="69c76-219">Inizializzazione di gestione moduli</span><span class="sxs-lookup"><span data-stu-id="69c76-219">Module Manager initialization</span></span>

<span data-ttu-id="69c76-220">La parte residente dell'applicazione è responsabile della chiamata della funzione di inizializzazione di gestione moduli ***txm_module_manager_initialize***.</span><span class="sxs-lookup"><span data-stu-id="69c76-220">The resident portion of the application is responsible for calling the Module Manager initialization function ***txm_module_manager_initialize***.</span></span> <span data-ttu-id="69c76-221">Questa funzione configura le strutture interne per il caricamento e lo scaricamento dei moduli, inclusa la configurazione dell'area di memoria usata per l'allocazione della memoria del modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-221">This function sets up the internal structures for loading and unloading modules, including setting up the memory area used for allocating module memory.</span></span>

## <a name="module-manager-loading"></a><span data-ttu-id="69c76-222">Caricamento di gestione moduli</span><span class="sxs-lookup"><span data-stu-id="69c76-222">Module Manager loading</span></span>

<span data-ttu-id="69c76-223">Gestione moduli può caricare i moduli dinamicamente nella memoria del modulo da file di modulo binari o da una sezione di codice del modulo già presente nell'area di codice residente.</span><span class="sxs-lookup"><span data-stu-id="69c76-223">The Module Manager can load modules dynamically into the module memory from binary module files or from a module code section that is already present in the resident code area.</span></span> <span data-ttu-id="69c76-224">Inoltre, il gestore di moduli può eseguire codice sul posto, ovvero solo i dati del modulo vengono allocati nella memoria del modulo e l'esecuzione del codice viene eseguita sul posto.</span><span class="sxs-lookup"><span data-stu-id="69c76-224">In addition, the module manager can execute code in place, that is, only the module data is allocated in the module memory and the code execution is done in place.</span></span> <span data-ttu-id="69c76-225">Sono disponibili le funzioni API di caricamento di gestione moduli seguenti.</span><span class="sxs-lookup"><span data-stu-id="69c76-225">The following Module Manager load API functions are available.</span></span>

* <span data-ttu-id="69c76-226">***txm_module_manager_file_load***</span><span class="sxs-lookup"><span data-stu-id="69c76-226">***txm_module_manager_file_load***</span></span>

* <span data-ttu-id="69c76-227">***txm_module_manager_in_place_load***</span><span class="sxs-lookup"><span data-stu-id="69c76-227">***txm_module_manager_in_place_load***</span></span>

* <span data-ttu-id="69c76-228">***txm_module_manager_memory_load***</span><span class="sxs-lookup"><span data-stu-id="69c76-228">***txm_module_manager_memory_load***</span></span>

<span data-ttu-id="69c76-229">La versione protetta dalla memoria di gestione moduli garantisce inoltre che il modulo venga caricato con l'allineamento corretto e che i registri di gestione della memoria siano impostati correttamente per ogni modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-229">The memory protected version of the Module Manager also makes sure that the module is loaded with the proper alignment and the memory management registers are set up properly for each module.</span></span> <span data-ttu-id="69c76-230">Quando la protezione della memoria viene abilitata tramite le opzioni del preambolo del modulo, l'accesso alla memoria del modulo è limitato al codice e alle aree dati del modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-230">When memory protection is enabled via the module preamble options, module memory access is restricted to the module code and data areas.</span></span>

## <a name="module-manager-starting"></a><span data-ttu-id="69c76-231">Avvio di gestione moduli</span><span class="sxs-lookup"><span data-stu-id="69c76-231">Module Manager starting</span></span>

<span data-ttu-id="69c76-232">Il gestore dei moduli avvia l'esecuzione di un modulo caricato in precedenza tramite la funzione API ***txm_module_manager_start*** .</span><span class="sxs-lookup"><span data-stu-id="69c76-232">The Module Manager initiates execution of a previously-loaded module via the ***txm_module_manager_start*** API function.</span></span> <span data-ttu-id="69c76-233">Per avviare l'esecuzione del modulo, questa funzione crea un thread che accede al modulo nella posizione iniziale specificata nel preambolo del modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-233">To initiate module execution, this function creates a thread that enters the module at the starting location specified in the module preamble.</span></span> <span data-ttu-id="69c76-234">La priorità e le dimensioni dello stack di questo thread sono specificate anche nel preambolo del modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-234">The priority and stack size of this thread is also specified in the module preamble.</span></span>

## <a name="module-manager-stopping"></a><span data-ttu-id="69c76-235">Arresto di gestione moduli</span><span class="sxs-lookup"><span data-stu-id="69c76-235">Module Manager stopping</span></span>

<span data-ttu-id="69c76-236">Gestione moduli termina l'esecuzione di un modulo caricato in precedenza ed eseguendo il modulo tramite la funzione ***txm_module_manager_stop*** .</span><span class="sxs-lookup"><span data-stu-id="69c76-236">The Module Manager terminates execution of a previously-loaded and executing module via the ***txm_module_manager_stop*** function.</span></span> <span data-ttu-id="69c76-237">Questa funzione API termina prima ed Elimina il thread iniziale iniziale.</span><span class="sxs-lookup"><span data-stu-id="69c76-237">This API function first terminates and deletes the initial starting thread.</span></span> <span data-ttu-id="69c76-238">Se il preambolo del modulo specifica un thread di arresto, questo thread viene creato ed eseguito.</span><span class="sxs-lookup"><span data-stu-id="69c76-238">If the module preamble specifies a stop thread, this thread is created and executed.</span></span> <span data-ttu-id="69c76-239">Gestione moduli attende un periodo di tempo fisso per il completamento del thread di arresto.</span><span class="sxs-lookup"><span data-stu-id="69c76-239">The Module Manager waits for a fixed period of time for the stop thread to complete.</span></span> <span data-ttu-id="69c76-240">Al termine, vengono eliminate tutte le risorse di sistema create dal modulo e il modulo viene inserito in uno stato inattivo, dal quale può essere riavviato o scaricato.</span><span class="sxs-lookup"><span data-stu-id="69c76-240">Once complete, all system resources created by the module are deleted and the module is placed in a dormant state, from which it can be either restarted or unloaded.</span></span>

## <a name="module-manager-unloading"></a><span data-ttu-id="69c76-241">Scaricamento di gestione moduli</span><span class="sxs-lookup"><span data-stu-id="69c76-241">Module Manager unloading</span></span>

<span data-ttu-id="69c76-242">Il gestore dei moduli Scarica un modulo caricato in precedenza ma non in esecuzione tramite la funzione ***txm_module_manager_unload*** .</span><span class="sxs-lookup"><span data-stu-id="69c76-242">The Module Manager unloads a previously-loaded but not executing module via the ***txm_module_manager_unload*** function.</span></span> <span data-ttu-id="69c76-243">Questa API rilascia tutta la memoria associata al modulo, che verrà liberata per l'uso con un altro modulo in futuro.</span><span class="sxs-lookup"><span data-stu-id="69c76-243">This API releases all memory associated with the module, freeing it for use with another module in the future.</span></span>

## <a name="module-manager-requests"></a><span data-ttu-id="69c76-244">Richieste di gestione moduli</span><span class="sxs-lookup"><span data-stu-id="69c76-244">Module Manager requests</span></span>

<span data-ttu-id="69c76-245">Le richieste effettuate dai moduli al gestore dei moduli vengono eseguite tramite le macro in ***txm_module. h*** che eseguono il mapping di tutte le chiamate threadX per chiamare la funzione di invio di gestione moduli tramite un puntatore a funzione fornito al modulo da Gestione moduli.</span><span class="sxs-lookup"><span data-stu-id="69c76-245">Requests made by modules to the Module Manager are done via macros in ***txm_module.h*** that map all ThreadX calls to call the Module Manager dispatch function via a function pointer supplied to the module by the Module Manager.</span></span>

<span data-ttu-id="69c76-246">I servizi aggiuntivi specifici dell'applicazione creati tramite il modulo che chiama ***txm_module_application_request*** vengono gestiti dallo stesso meccanismo macro usato per l'API threadX.</span><span class="sxs-lookup"><span data-stu-id="69c76-246">Additional application-specific services made via the module calling ***txm_module_application_request*** are handled by the same macro mechanism used for the ThreadX API.</span></span> <span data-ttu-id="69c76-247">Per impostazione predefinita, questa funzione di gestione in Gestione moduli è vuota e progettata in modo tale che l'applicazione aggiunga il codice necessario per elaborare le richieste specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="69c76-247">By default, this handling function in the Module Manager is empty and designed such that the application adds the necessary code to process the application-specific requests.</span></span>

<span data-ttu-id="69c76-248">Se la richiesta non è implementata da Gestione moduli, viene restituito un valore di **TX_NOT_AVAILABLE** stato di errore da Gestione moduli.</span><span class="sxs-lookup"><span data-stu-id="69c76-248">If the request is not implemented by the Module Manager, a value of **TX_NOT_AVAILABLE** error status is returned by the Module Manager.</span></span> <span data-ttu-id="69c76-249">Questo codice di errore viene restituito anche se il modulo richiede un'operazione che esula dall'ambito dell'accesso del modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-249">This error code is also returned if the module requests an operation that is outside the scope of the module's access.</span></span> <span data-ttu-id="69c76-250">Un modulo, ad esempio, non è autorizzato a creare un timer con il blocco di controllo timer o l'indirizzo di callback al di fuori dell'area di codice del modulo.</span><span class="sxs-lookup"><span data-stu-id="69c76-250">For example, a module is not allowed to create a timer with the timer control block or callback address outside of the module's code area.</span></span>

## <a name="module-manager-example"></a><span data-ttu-id="69c76-251">Esempio di gestione moduli</span><span class="sxs-lookup"><span data-stu-id="69c76-251">Module Manager example</span></span>

<span data-ttu-id="69c76-252">Di seguito è riportato un esempio di codice di gestione dei moduli che avvia il modulo di esempio precedentemente definito nel capitolo 2.</span><span class="sxs-lookup"><span data-stu-id="69c76-252">The following is an example of Module Manager code that launches the example module previously defined in Chapter 2.</span></span> <span data-ttu-id="69c76-253">Si presuppone che il modulo sia già caricato, presumibilmente dal debugger, all'indirizzo ROM 0x00800000.</span><span class="sxs-lookup"><span data-stu-id="69c76-253">It is assumed that the module is already loaded, presumably by the debugger, at ROM address 0x00800000.</span></span>

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

## <a name="module-manager-building"></a><span data-ttu-id="69c76-254">Compilazione di gestione moduli</span><span class="sxs-lookup"><span data-stu-id="69c76-254">Module Manager building</span></span>

<span data-ttu-id="69c76-255">I file di origine del ***txm_module_manager_ \**** devono essere aggiunti alla libreria threadX.</span><span class="sxs-lookup"><span data-stu-id="69c76-255">The ***txm_module_manager_\**** source files must be added to the ThreadX library.</span></span>

<span data-ttu-id="69c76-256">Un'applicazione di gestione moduli ThreadX è in realtà identica a un'applicazione ThreadX standard, ovvero uno o più file di applicazione collegati con la libreria ThreadX ***TX. a***.</span><span class="sxs-lookup"><span data-stu-id="69c76-256">A ThreadX Module Manager application is effectively the same as a standard ThreadX application, which is one or more application files linked together with the ThreadX library ***tx.a***.</span></span> <span data-ttu-id="69c76-257">La compilazione di un'applicazione di gestione moduli dipende dalla catena di strumenti utilizzata.</span><span class="sxs-lookup"><span data-stu-id="69c76-257">Building a module manager application is dependent on the tool chain being used.</span></span> <span data-ttu-id="69c76-258">Vedere l' [appendice](appendix.md) per esempi specifici delle porte.</span><span class="sxs-lookup"><span data-stu-id="69c76-258">See [appendix](appendix.md) for port-specific examples.</span></span>
