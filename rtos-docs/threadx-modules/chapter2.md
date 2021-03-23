---
title: Capitolo 2-requisiti dei moduli
description: Questo articolo descrive i requisiti per la compilazione di un modulo ThreadX.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 32288d78ceffb74ab088a1d720dbac657f6d3ed4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821398"
---
# <a name="chapter-2---module-requirements"></a><span data-ttu-id="f9a67-103">Capitolo 2-requisiti dei moduli</span><span class="sxs-lookup"><span data-stu-id="f9a67-103">Chapter 2 - Module requirements</span></span>

<span data-ttu-id="f9a67-104">Un modulo ThreadX contiene un preambolo, che definisce le caratteristiche di base del modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-104">A ThreadX Module contains a preamble, which defines the basic characteristics of the module.</span></span> <span data-ttu-id="f9a67-105">Il preambolo è seguito dall'area di istruzione del modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-105">The preamble is followed by the instruction area of the module.</span></span> <span data-ttu-id="f9a67-106">I moduli possono essere eseguiti sul posto o possono essere caricati nell'area memoria del modulo da Gestione moduli prima dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f9a67-106">Modules may be executed in place or they may be loaded into the module memory area by the Module Manager prior to execution.</span></span> <span data-ttu-id="f9a67-107">L'unico requisito è che il preambolo si trovi sempre nel primo indirizzo del modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-107">The only requirement is that the preamble is always located at the first address of the module.</span></span> <span data-ttu-id="f9a67-108">Nella figura 2 viene illustrato un layout di modulo di base.</span><span class="sxs-lookup"><span data-stu-id="f9a67-108">Figure 2 illustrates a basic module layout.</span></span>

| <span data-ttu-id="f9a67-109">Layout del modulo</span><span class="sxs-lookup"><span data-stu-id="f9a67-109">Module Layout</span></span> |
|:---:|
| <span data-ttu-id="f9a67-110">\[preambolo del modulo\]</span><span class="sxs-lookup"><span data-stu-id="f9a67-110">\[module preamble\]</span></span>         |
| <span data-ttu-id="f9a67-111">\[area di istruzione del modulo\]</span><span class="sxs-lookup"><span data-stu-id="f9a67-111">\[module instruction area\]</span></span> |
| <span data-ttu-id="f9a67-112">\[area RAM del modulo\]</span><span class="sxs-lookup"><span data-stu-id="f9a67-112">\[module RAM area\]</span></span>         |

<span data-ttu-id="f9a67-113">**Figura 2** -layout del modulo</span><span class="sxs-lookup"><span data-stu-id="f9a67-113">**Figure 2** - Module Layout</span></span>

> [!NOTE]
> <span data-ttu-id="f9a67-114">I moduli devono essere compilati con il codice indipendente dalla posizione e le opzioni del linker e del compilatore di dati appropriati.</span><span class="sxs-lookup"><span data-stu-id="f9a67-114">Modules must be built with the appropriate position independent code and data compiler/linker options.</span></span> <span data-ttu-id="f9a67-115">Questo consente l'esecuzione del modulo in qualsiasi area di memoria.</span><span class="sxs-lookup"><span data-stu-id="f9a67-115">This enables execution of the module in any memory area.</span></span>

<span data-ttu-id="f9a67-116">Quando viene creato un thread del modulo, viene allocato un secondo spazio dello stack per l'uso quando il thread si trova nel kernel protetto dalla memoria.</span><span class="sxs-lookup"><span data-stu-id="f9a67-116">When a Module thread is created, a second stack space is allocated for use when the thread is in the memory-protected kernel.</span></span> <span data-ttu-id="f9a67-117">La dimensione dello spazio dello stack del kernel del thread è configurabile dall'utente usando **TXM_MODULE_KERNEL_STACK_SIZE** in **_txm_module_port. h_*_. In questo modo è possibile usare dimensioni dello stack più piccole quando si crea un thread del modulo, perché lo stack specificato dall'utente quando chiama _*_tx_thread_create_** viene usato solo nel modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-117">The size of the thread's kernel stack space is user-configurable using **TXM_MODULE_KERNEL_STACK_SIZE** in **_txm_module_port.h_*_. This allows a smaller stack size to be used when creating a Module thread, as the stack specified by the user when calling _*_tx_thread_create_** is only used in the module.</span></span>

> [!NOTE]
> <span data-ttu-id="f9a67-118">La parte superiore dello stack di thread del modulo contiene la struttura delle informazioni sulla voce del thread (**TXM_MODULE_THREAD_ENTRY_INFO**), quindi le dimensioni dello stack disponibili vengono ridotte in base alle dimensioni della struttura.</span><span class="sxs-lookup"><span data-stu-id="f9a67-118">The top of a module thread stack contains the thread entry information structure (**TXM_MODULE_THREAD_ENTRY_INFO**), so the available stack size is decreased by the size of this structure.</span></span> <span data-ttu-id="f9a67-119">Quando si crea un thread in un modulo, aumentare la dimensione dello stack per almeno questa dimensione della struttura.</span><span class="sxs-lookup"><span data-stu-id="f9a67-119">When creating a thread in a module, increase its stack size by at least this the size of this structure.</span></span>

<span data-ttu-id="f9a67-120">I passaggi seguenti sono necessari per la creazione e la compilazione di un modulo ThreadX. ogni passaggio è descritto in dettaglio più avanti.</span><span class="sxs-lookup"><span data-stu-id="f9a67-120">The following steps are required for creating and building a ThreadX Module (each step is described in greater detail below).</span></span>

1. <span data-ttu-id="f9a67-121">Tutti i file C in un modulo devono #define **TXM_MODULE** prima di includere **_txm_module. h_**.</span><span class="sxs-lookup"><span data-stu-id="f9a67-121">All C files in a module must #define **TXM_MODULE** prior to including **_txm_module.h_**.</span></span> <span data-ttu-id="f9a67-122">Questa operazione può essere eseguita nel file di origine compilato o come parte delle impostazioni del progetto.</span><span class="sxs-lookup"><span data-stu-id="f9a67-122">This can be accomplished in the source file being compiled or as part of the project settings.</span></span> <span data-ttu-id="f9a67-123">Questa operazione esegue il mapping delle chiamate all'API ThreadX alla versione specifica del modulo dell'API che richiama la funzione Dispatch nel gestore dei moduli residenti per eseguire la chiamata alla funzione API effettiva.</span><span class="sxs-lookup"><span data-stu-id="f9a67-123">Doing so remaps the ThreadX API calls to the module-specific version of the API that invokes the dispatch function in the resident Module Manager to perform the call to the actual API function.</span></span>
2. <span data-ttu-id="f9a67-124">Ogni modulo deve avere un preambolo nel primo indirizzo dell'area di istruzioni che definisce le caratteristiche e le esigenze delle risorse del modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-124">Each module must have a preamble at its first instruction area address which defines the characteristics and the resource needs of the module.</span></span>
3. <span data-ttu-id="f9a67-125">Ogni modulo deve collegare il preambolo all'inizio dell'area di istruzione del modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-125">Each module must link the preamble at the beginning of the module instruction area.</span></span>
4. <span data-ttu-id="f9a67-126">Ogni modulo deve essere collegato a una libreria di moduli (***TXM. a***), che contiene funzioni specifiche del modulo usate per interagire con threadX.</span><span class="sxs-lookup"><span data-stu-id="f9a67-126">Each module must link against a module library (***txm.a***), which contains module-specific functions used to interact with ThreadX.</span></span>

## <a name="module-sources"></a><span data-ttu-id="f9a67-127">Origini moduli</span><span class="sxs-lookup"><span data-stu-id="f9a67-127">Module sources</span></span>

<span data-ttu-id="f9a67-128">I moduli ThreadX dispongono di un proprio set di file di origine progettati per essere collegati e situati direttamente con il codice sorgente del modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-128">ThreadX Modules have their own set of source files that are designed to be linked and located directly with the module source code.</span></span> <span data-ttu-id="f9a67-129">Questi file forniscono il Bridge tra il modulo separato e il gestore dei moduli residenti.</span><span class="sxs-lookup"><span data-stu-id="f9a67-129">These files provide the bridge between the separate module and resident Module Manager.</span></span> <span data-ttu-id="f9a67-130">I file di modulo sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="f9a67-130">The Module files are as follows.</span></span>

| <span data-ttu-id="f9a67-131">File Name</span><span class="sxs-lookup"><span data-stu-id="f9a67-131">File Name</span></span> | <span data-ttu-id="f9a67-132">Contenuto</span><span class="sxs-lookup"><span data-stu-id="f9a67-132">Contents</span></span> |
|---|---|
| <span data-ttu-id="f9a67-133">**txm_module. h**</span><span class="sxs-lookup"><span data-stu-id="f9a67-133">**txm_module.h**</span></span> | <span data-ttu-id="f9a67-134">File di inclusione che definisce le informazioni sul modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-134">Include file that defines module information.</span></span> |
| <span data-ttu-id="f9a67-135">**txm_module_port. h**</span><span class="sxs-lookup"><span data-stu-id="f9a67-135">**txm_module_port.h**</span></span> | <span data-ttu-id="f9a67-136">File di inclusione che definisce le informazioni sul modulo specifiche delle porte.</span><span class="sxs-lookup"><span data-stu-id="f9a67-136">Include file that defines port-specific module information.</span></span> |
| <span data-ttu-id="f9a67-137">**txm_module_user. h**</span><span class="sxs-lookup"><span data-stu-id="f9a67-137">**txm_module_user.h**</span></span> | <span data-ttu-id="f9a67-138">Definisce i valori e che l'utente può personalizzare.</span><span class="sxs-lookup"><span data-stu-id="f9a67-138">Defines and values the user can customize.</span></span> |
| <span data-ttu-id="f9a67-139">**txm_module_initialize. s [1] [3]**</span><span class="sxs-lookup"><span data-stu-id="f9a67-139">**txm_module_initialize.s [1][3]**</span></span> | <span data-ttu-id="f9a67-140">Chiama funzioni intrinseche al modulo di avvio.</span><span class="sxs-lookup"><span data-stu-id="f9a67-140">Calls intrinsic functions to startup module.</span></span> |
| <span data-ttu-id="f9a67-141">**txm_module_preamble. \{ s/S/68\}**</span><span class="sxs-lookup"><span data-stu-id="f9a67-141">**txm_module_preamble.\{s/S/68\}**</span></span> | <span data-ttu-id="f9a67-142">File di assembly del preambolo del modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-142">Module preamble assembly file.</span></span> <span data-ttu-id="f9a67-143">Questo file definisce diversi attributi specifici del modulo ed è collegato al codice dell'applicazione del modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-143">This file defines various module-specific attributes and is linked with the module application code.</span></span> |
| <span data-ttu-id="f9a67-144">**txm_module_application_request. c [1]**</span><span class="sxs-lookup"><span data-stu-id="f9a67-144">**txm_module_application_request.c [1]**</span></span> | <span data-ttu-id="f9a67-145">La funzione di richiesta dell'applicazione del modulo Invia una richiesta specifica dell'applicazione al codice residente.</span><span class="sxs-lookup"><span data-stu-id="f9a67-145">Module application request function sends an application-specific request to the resident code.</span></span> |
| <span data-ttu-id="f9a67-146">**txm_module_callback_request_thread_entry. c &nbsp; [1]**</span><span class="sxs-lookup"><span data-stu-id="f9a67-146">**txm_module_callback_request_thread_entry.c&nbsp;[1]**</span></span> | <span data-ttu-id="f9a67-147">Thread di callback del modulo responsabile dell'elaborazione dei callback richiesti dal modulo, inclusi i timer e i callback di notifica.</span><span class="sxs-lookup"><span data-stu-id="f9a67-147">Module callback thread that is responsible for processing callbacks requested by the module, including timers and notification callbacks.</span></span> |
| <span data-ttu-id="f9a67-148">\**txm_ *. c [1] [2]**</span><span class="sxs-lookup"><span data-stu-id="f9a67-148">**txm_\*.c [1][2]**</span></span> | <span data-ttu-id="f9a67-149">I servizi API ThreadX standard chiamano il dispatcher del kernel.</span><span class="sxs-lookup"><span data-stu-id="f9a67-149">The standard ThreadX API services, these call the kernel dispatcher.</span></span>
| <span data-ttu-id="f9a67-150">**txm_module_object_allocate. c [1]**</span><span class="sxs-lookup"><span data-stu-id="f9a67-150">**txm_module_object_allocate.c [1]**</span></span> | <span data-ttu-id="f9a67-151">Funzione del modulo per allocare memoria per gli oggetti modulo presenti nel pool di memoria di gestione.</span><span class="sxs-lookup"><span data-stu-id="f9a67-151">Module function to allocate memory for module objects located in the manager memory pool.</span></span> |
| <span data-ttu-id="f9a67-152">**txm_module_object_deallocate. c [1]**</span><span class="sxs-lookup"><span data-stu-id="f9a67-152">**txm_module_object_deallocate.c [1]**</span></span> | <span data-ttu-id="f9a67-153">Funzione del modulo per deallocare la memoria per gli oggetti modulo presenti nel pool di memoria di gestione.</span><span class="sxs-lookup"><span data-stu-id="f9a67-153">Module function to deallocate memory for module objects located in the manager memory pool.</span></span> |
| <span data-ttu-id="f9a67-154">**txm_module_object_pointer_get. c [1]**</span><span class="sxs-lookup"><span data-stu-id="f9a67-154">**txm_module_object_pointer_get.c [1]**</span></span> | <span data-ttu-id="f9a67-155">Funzione module per recuperare un puntatore a un oggetto di sistema.</span><span class="sxs-lookup"><span data-stu-id="f9a67-155">Module function to retrieve a pointer to a system object.</span></span> |
| <span data-ttu-id="f9a67-156">**txm_module_object_pointer_get_extended. c [1]**</span><span class="sxs-lookup"><span data-stu-id="f9a67-156">**txm_module_object_pointer_get_extended.c [1]**</span></span> | <span data-ttu-id="f9a67-157">Funzione module per recuperare un puntatore a un oggetto di sistema, ovvero la lunghezza del nome.</span><span class="sxs-lookup"><span data-stu-id="f9a67-157">Module function to retrieve a pointer to a system object, name length safety.</span></span> |
| <span data-ttu-id="f9a67-158">**txm_module_thread_shell_entry. c [1]**</span><span class="sxs-lookup"><span data-stu-id="f9a67-158">**txm_module_thread_shell_entry.c [1]**</span></span> | <span data-ttu-id="f9a67-159">Funzione entry thread del modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-159">Module thread entry function.</span></span> |
| <span data-ttu-id="f9a67-160">**txm_module_thread_system_suspend. c [1]**</span><span class="sxs-lookup"><span data-stu-id="f9a67-160">**txm_module_thread_system_suspend.c [1]**</span></span> | <span data-ttu-id="f9a67-161">Funzione del modulo per sospendere un thread.</span><span class="sxs-lookup"><span data-stu-id="f9a67-161">Module function to suspend a thread.</span></span> |

<span data-ttu-id="f9a67-162">**[1]** situato nella libreria **_TXM. a_**.</span><span class="sxs-lookup"><span data-stu-id="f9a67-162">**[1]** Located in library **_txm.a_**.</span></span>

<span data-ttu-id="f9a67-163">**[2]** questi file hanno lo stesso nome dei file dell'API threadX, con **txm_** prefisso anziché **tx_** prefisso.</span><span class="sxs-lookup"><span data-stu-id="f9a67-163">**[2]** These files have the same name as the ThreadX API files, with **txm_** prefix instead of **tx_** prefix.</span></span>

<span data-ttu-id="f9a67-164">**[3]** il file **txm_module_initialize. s** è solo per le porte che usano gli strumenti ARM.</span><span class="sxs-lookup"><span data-stu-id="f9a67-164">**[3]** The **txm_module_initialize.s** file is only for ports using ARM tools.</span></span>

## <a name="module-preamble"></a><span data-ttu-id="f9a67-165">Preambolo del modulo</span><span class="sxs-lookup"><span data-stu-id="f9a67-165">Module preamble</span></span>

<span data-ttu-id="f9a67-166">Il preambolo del modulo definisce le caratteristiche e le risorse del modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-166">The Module Preamble defines characteristics and resources of the module.</span></span> <span data-ttu-id="f9a67-167">Le informazioni come la funzione di immissione iniziale dei thread e l'area di memoria iniziale associata al thread sono definite nel preambolo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-167">Information such as the initial thread entry function and the initial memory area associated with the thread are defined in the preamble.</span></span> <span data-ttu-id="f9a67-168">Gli esempi relativi ai preamboli specifici della porta sono disponibili nell' [appendice](appendix.md).</span><span class="sxs-lookup"><span data-stu-id="f9a67-168">Port-specific preamble examples are in the [appendix](appendix.md).</span></span> <span data-ttu-id="f9a67-169">Nella figura 3 viene illustrato un esempio di preambolo del modulo ThreadX per una destinazione generica (le righe che iniziano con \* sono valori generalmente modificati dall'applicazione):</span><span class="sxs-lookup"><span data-stu-id="f9a67-169">Figure 3 shows an example ThreadX module preamble for a generic target (the lines starting with \* are values typically modified by the application):</span></span>

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

<span data-ttu-id="f9a67-170">**Figura 3**</span><span class="sxs-lookup"><span data-stu-id="f9a67-170">**Figure 3**</span></span>

<span data-ttu-id="f9a67-171">Nella maggior parte dei casi, lo sviluppatore deve solo definire il thread iniziale del modulo (offset 0x1C), ID modulo (offset 0x10), priorità dei thread di avvio/arresto (offset 0x24) e dimensioni dello stack dei thread di avvio/arresto (offset 0x28).</span><span class="sxs-lookup"><span data-stu-id="f9a67-171">In most cases, the developer only needs to define the module's starting thread (offset 0x1C), module ID (offset 0x10), start/stop thread priority (offset 0x24), and start/stop thread stack size (offset 0x28).</span></span> <span data-ttu-id="f9a67-172">La dimostrazione precedente è configurata in modo tale che il thread iniziale del modulo sia ***demo_module_start** _, l'ID del modulo è _*_0x12345678._*_ e il thread iniziale ha una priorità pari a _*_1_*_ e una dimensione dello stack di _ *_2048_** byte.</span><span class="sxs-lookup"><span data-stu-id="f9a67-172">The demonstration above is set up such that the starting thread of the module is ***demo_module_start** _, the module ID is _*_0x12345678_*_, and the starting thread has a priority of _*_1_*_, and a stack size of _ *_2048_** bytes.</span></span>

<span data-ttu-id="f9a67-173">Alcune applicazioni possono facoltativamente definire un thread di arresto, che viene eseguito durante l'arresto del modulo da parte di gestione moduli.</span><span class="sxs-lookup"><span data-stu-id="f9a67-173">Some applications may optionally define a stopping thread, which is executed as the Module Manager stops the module.</span></span> <span data-ttu-id="f9a67-174">Inoltre, alcune applicazioni potrebbero utilizzare il campo delle proprietà del modulo, definito nel modo seguente.</span><span class="sxs-lookup"><span data-stu-id="f9a67-174">In addition, some applications might utilize the Module Properties field, defined as follows.</span></span>

## <a name="module-properties-bit-map"></a><span data-ttu-id="f9a67-175">Mappa di bit delle proprietà del modulo</span><span class="sxs-lookup"><span data-stu-id="f9a67-175">Module properties bit map</span></span>

<span data-ttu-id="f9a67-176">La tabella seguente illustra un esempio della mappa di bit Properties.</span><span class="sxs-lookup"><span data-stu-id="f9a67-176">The table below shows an example of the properties bit map.</span></span> <span data-ttu-id="f9a67-177">Le bitmap delle proprietà specifiche delle porte sono disponibili nell' [appendice](appendix.md).</span><span class="sxs-lookup"><span data-stu-id="f9a67-177">Port-specific properties bitmaps are in the [appendix](appendix.md).</span></span>

| <span data-ttu-id="f9a67-178">bit</span><span class="sxs-lookup"><span data-stu-id="f9a67-178">Bit</span></span> | <span data-ttu-id="f9a67-179">Valore</span><span class="sxs-lookup"><span data-stu-id="f9a67-179">Value</span></span> | <span data-ttu-id="f9a67-180">Significato</span><span class="sxs-lookup"><span data-stu-id="f9a67-180">Meaning</span></span> |
|---|---|---|
| <span data-ttu-id="f9a67-181">0</span><span class="sxs-lookup"><span data-stu-id="f9a67-181">0</span></span> | <span data-ttu-id="f9a67-182">0</span><span class="sxs-lookup"><span data-stu-id="f9a67-182">0</span></span><br /><span data-ttu-id="f9a67-183">1</span><span class="sxs-lookup"><span data-stu-id="f9a67-183">1</span></span> | <span data-ttu-id="f9a67-184">Esecuzione in modalità privilegiata</span><span class="sxs-lookup"><span data-stu-id="f9a67-184">Privileged mode execution</span></span><br /><span data-ttu-id="f9a67-185">Esecuzione in modalità utente</span><span class="sxs-lookup"><span data-stu-id="f9a67-185">User mode execution</span></span> |
| <span data-ttu-id="f9a67-186">1</span><span class="sxs-lookup"><span data-stu-id="f9a67-186">1</span></span> | <span data-ttu-id="f9a67-187">0</span><span class="sxs-lookup"><span data-stu-id="f9a67-187">0</span></span><br /><span data-ttu-id="f9a67-188">1</span><span class="sxs-lookup"><span data-stu-id="f9a67-188">1</span></span> | <span data-ttu-id="f9a67-189">Nessuna protezione MPU</span><span class="sxs-lookup"><span data-stu-id="f9a67-189">No MPU protection</span></span><br /><span data-ttu-id="f9a67-190">Protezione MPU (è necessario selezionare la modalità utente)</span><span class="sxs-lookup"><span data-stu-id="f9a67-190">MPU protection (must have user mode selected)</span></span> |
| <span data-ttu-id="f9a67-191">2</span><span class="sxs-lookup"><span data-stu-id="f9a67-191">2</span></span> | <span data-ttu-id="f9a67-192">0</span><span class="sxs-lookup"><span data-stu-id="f9a67-192">0</span></span><br /><span data-ttu-id="f9a67-193">1</span><span class="sxs-lookup"><span data-stu-id="f9a67-193">1</span></span> | <span data-ttu-id="f9a67-194">Disabilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="f9a67-194">Disable shared/external memory access</span></span><br /><span data-ttu-id="f9a67-195">Abilitare l'accesso alla memoria condivisa/esterna</span><span class="sxs-lookup"><span data-stu-id="f9a67-195">Enable shared/external memory access</span></span> |
| <span data-ttu-id="f9a67-196">[23-3]</span><span class="sxs-lookup"><span data-stu-id="f9a67-196">[23-3]</span></span> | <span data-ttu-id="f9a67-197">0</span><span class="sxs-lookup"><span data-stu-id="f9a67-197">0</span></span> | <span data-ttu-id="f9a67-198">Riservato</span><span class="sxs-lookup"><span data-stu-id="f9a67-198">Reserved</span></span>
| <span data-ttu-id="f9a67-199">[31-24]</span><span class="sxs-lookup"><span data-stu-id="f9a67-199">[31-24]</span></span> | <br /><span data-ttu-id="f9a67-200">0x01</span><span class="sxs-lookup"><span data-stu-id="f9a67-200">0x01</span></span><br /><span data-ttu-id="f9a67-201">0x02</span><span class="sxs-lookup"><span data-stu-id="f9a67-201">0x02</span></span><br /><span data-ttu-id="f9a67-202">0x03</span><span class="sxs-lookup"><span data-stu-id="f9a67-202">0x03</span></span> | <span data-ttu-id="f9a67-203">**ID compilatore**</span><span class="sxs-lookup"><span data-stu-id="f9a67-203">**Compiler ID**</span></span><br /><span data-ttu-id="f9a67-204">IAR</span><span class="sxs-lookup"><span data-stu-id="f9a67-204">IAR</span></span><br /><span data-ttu-id="f9a67-205">ARM</span><span class="sxs-lookup"><span data-stu-id="f9a67-205">ARM</span></span><br /><span data-ttu-id="f9a67-206">GNU</span><span class="sxs-lookup"><span data-stu-id="f9a67-206">GNU</span></span> |


## <a name="module-linker-control-file"></a><span data-ttu-id="f9a67-207">File di controllo del linker del modulo</span><span class="sxs-lookup"><span data-stu-id="f9a67-207">Module linker control file</span></span>

<span data-ttu-id="f9a67-208">Quando si compila un modulo, il preambolo del modulo deve essere inserito prima di qualsiasi altra sezione di codice.</span><span class="sxs-lookup"><span data-stu-id="f9a67-208">When building a module, the module preamble must be placed before any other code section.</span></span> <span data-ttu-id="f9a67-209">Un modulo deve essere compilato con il codice indipendente dalla posizione e le sezioni di dati.</span><span class="sxs-lookup"><span data-stu-id="f9a67-209">A module must be built with position-independent code and data sections.</span></span> <span data-ttu-id="f9a67-210">I file del linker di esempio specifici della porta si trovano nell' [appendice](appendix.md).</span><span class="sxs-lookup"><span data-stu-id="f9a67-210">Port-specific example linker files are in the [appendix](appendix.md).</span></span>

## <a name="module-threadx-library"></a><span data-ttu-id="f9a67-211">Libreria ThreadX del modulo</span><span class="sxs-lookup"><span data-stu-id="f9a67-211">Module ThreadX library</span></span>

<span data-ttu-id="f9a67-212">Ogni modulo deve essere collegato a una speciale libreria ThreadX incentrata sul modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-212">Each module must link against a special, module-centric ThreadX library.</span></span> <span data-ttu-id="f9a67-213">Questa libreria fornisce l'accesso ai servizi di ThreadX nel codice residente.</span><span class="sxs-lookup"><span data-stu-id="f9a67-213">This library provides access to ThreadX services in the resident code.</span></span> <span data-ttu-id="f9a67-214">La maggior parte degli accessi viene eseguita tramite i file ***txm_ \* . c*** .</span><span class="sxs-lookup"><span data-stu-id="f9a67-214">Most of the access is accomplished via the ***txm_\*.c*** files.</span></span> <span data-ttu-id="f9a67-215">Di seguito è riportato un esempio della chiamata di accesso al modulo per la funzione API ThreadX **_tx_thread_relinquish_* _ (in _*_ \_ txm_thread_relinquish. c \* \* \* \*).</span><span class="sxs-lookup"><span data-stu-id="f9a67-215">The following is an example of the module access call for the ThreadX API function **_tx_thread_relinquish_* _ (in _*_\_txm_thread_relinquish.c\*\*\*\*).</span></span>

```c
(_txm_module_kernel_call_dispatcher)(TXM_THREAD_RELINQUISH_CALL, 0, 0, 0);
```

<span data-ttu-id="f9a67-216">In questo esempio, il puntatore a funzione fornito da Gestione moduli viene usato per chiamare la funzione di invio di gestione moduli con l'ID associato al servizio ***tx_thread_relinquish*** .</span><span class="sxs-lookup"><span data-stu-id="f9a67-216">In this example, the function pointer supplied by the Module Manager is used to call the Module Manager dispatch function with the ID associated with the ***tx_thread_relinquish*** service.</span></span> <span data-ttu-id="f9a67-217">Questo servizio non accetta parametri.</span><span class="sxs-lookup"><span data-stu-id="f9a67-217">This service takes no parameters.</span></span>

## <a name="module-example"></a><span data-ttu-id="f9a67-218">Esempio di modulo</span><span class="sxs-lookup"><span data-stu-id="f9a67-218">Module example</span></span>

<span data-ttu-id="f9a67-219">Di seguito è riportato un esempio della dimostrazione ThreadX standard sotto forma di modulo.</span><span class="sxs-lookup"><span data-stu-id="f9a67-219">The following is an example of the standard ThreadX demonstration in the form of a module.</span></span> <span data-ttu-id="f9a67-220">Le differenze principali tra la dimostrazione ThreadX standard e la dimostrazione del modulo sono.</span><span class="sxs-lookup"><span data-stu-id="f9a67-220">The main differences between the standard ThreadX demonstration and the module demonstration are.</span></span>

1. <span data-ttu-id="f9a67-221">Sostituzione di ***tx_api. h** _ con _ *_txm_module. h_**</span><span class="sxs-lookup"><span data-stu-id="f9a67-221">Replacement of ***tx_api.h** _ with _ *_txm_module.h_**</span></span>
2. <span data-ttu-id="f9a67-222">Aggiunta di **#define TXM_MODULE** prima di **_txm_module. h_**</span><span class="sxs-lookup"><span data-stu-id="f9a67-222">Addition of **#define TXM_MODULE** prior to **_txm_module.h_**</span></span>
3. <span data-ttu-id="f9a67-223">Sostituzione di ***Main** _ e _ *tx_application_define** con **_demo_module_start_**</span><span class="sxs-lookup"><span data-stu-id="f9a67-223">Replacement of ***main** _ and _ *tx_application_define** with **_demo_module_start_**</span></span>
4. <span data-ttu-id="f9a67-224">Dichiarazione di *puntatori* a oggetti threadX anziché agli oggetti stessi.</span><span class="sxs-lookup"><span data-stu-id="f9a67-224">Declaring *pointers* to ThreadX objects rather than the objects themselves.</span></span>

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

## <a name="building-modules"></a><span data-ttu-id="f9a67-225">Compilazione di moduli</span><span class="sxs-lookup"><span data-stu-id="f9a67-225">Building Modules</span></span>

<span data-ttu-id="f9a67-226">La compilazione di un modulo dipende dalla catena di strumenti usata.</span><span class="sxs-lookup"><span data-stu-id="f9a67-226">Building a module is dependent on the tool chain being used.</span></span> <span data-ttu-id="f9a67-227">Vedere l' [appendice](appendix.md) per esempi specifici delle porte.</span><span class="sxs-lookup"><span data-stu-id="f9a67-227">See [appendix](appendix.md) for port-specific examples.</span></span> <span data-ttu-id="f9a67-228">Di seguito sono riportate le attività comuni a tutte le porte.</span><span class="sxs-lookup"><span data-stu-id="f9a67-228">Common activities to all ports include the following.</span></span>

- <span data-ttu-id="f9a67-229">Compilazione di una libreria di moduli</span><span class="sxs-lookup"><span data-stu-id="f9a67-229">Building a module library</span></span>
- <span data-ttu-id="f9a67-230">Compilazione dell'applicazione del modulo</span><span class="sxs-lookup"><span data-stu-id="f9a67-230">Building the module application</span></span>

<span data-ttu-id="f9a67-231">Ogni modulo deve avere un **txm_module_preamble** (programma di installazione specifico per il modulo) e la libreria di moduli (ad esempio, **_TXM. a_**).</span><span class="sxs-lookup"><span data-stu-id="f9a67-231">Each module is required to have a **txm_module_preamble** (setup specifically for the module) and the module library (for example, **_txm.a_**).</span></span>
