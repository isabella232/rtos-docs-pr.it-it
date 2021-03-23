---
title: Guida per l'utente di Azure RTOS GUIX
description: Questa guida contiene informazioni complete su Azure RTO GUIX, il prodotto GUI a prestazioni elevate di Microsoft.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: b7af0fba59b599c9c8db3ab80a3271eacfd11992
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823195"
---
# <a name="about-guix-user-guide"></a><span data-ttu-id="fd499-103">Informazioni sul manuale dell'utente di GUIX</span><span class="sxs-lookup"><span data-stu-id="fd499-103">About GUIX User Guide</span></span>

<span data-ttu-id="fd499-104">Questa guida contiene informazioni complete su Azure RTO GUIX, il prodotto GUI a prestazioni elevate di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fd499-104">This guide contains comprehensive information about Azure RTOS GUIX, the high-performance GUI product from Microsoft.</span></span> <span data-ttu-id="fd499-105">È destinato agli sviluppatori di software in tempo reale incorporati che conoscono i concetti di base dell'interfaccia utente grafica, Azure RTO ThreadX e il linguaggio di programmazione C.</span><span class="sxs-lookup"><span data-stu-id="fd499-105">It is intended for embedded real-time software developers familiar with basic GUI concepts, Azure RTOS ThreadX, and the C programming language.</span></span>

## <a name="organization"></a><span data-ttu-id="fd499-106">Organization</span><span class="sxs-lookup"><span data-stu-id="fd499-106">Organization</span></span>

[<span data-ttu-id="fd499-107">Capitolo 1-Introduzione ad Azure RTO GUIX</span><span class="sxs-lookup"><span data-stu-id="fd499-107">Chapter 1 - Introduction to Azure RTOS GUIX</span></span>](chapter-1.md)

[<span data-ttu-id="fd499-108">Capitolo 2-installazione e uso di Azure RTO GUIX</span><span class="sxs-lookup"><span data-stu-id="fd499-108">Chapter 2 - Installation and use of Azure RTOS GUIX</span></span>](chapter-2.md)

[<span data-ttu-id="fd499-109">Capitolo 3-Panoramica funzionale di Azure RTO GUIX</span><span class="sxs-lookup"><span data-stu-id="fd499-109">Chapter 3 - Functional Overview of Azure RTOS GUIX</span></span>](chapter-3.md)

[<span data-ttu-id="fd499-110">Capitolo 4-Descrizione dei servizi GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="fd499-110">Chapter 4 - Description of Azure RTOS GUIX Services</span></span>](chapter-4.md)

[<span data-ttu-id="fd499-111">Capitolo 5-driver di visualizzazione GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="fd499-111">Chapter 5 - Azure RTOS GUIX Display Drivers</span></span>](chapter-5.md)  

[<span data-ttu-id="fd499-112">Esempio di GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="fd499-112">Azure RTOS GUIX Example</span></span>](guix-example.md)

[<span data-ttu-id="fd499-113">Appendice A-definizioni dei colori GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="fd499-113">Appendix A - Azure RTOS GUIX Color Definitions</span></span>](appendix-a.md)

[<span data-ttu-id="fd499-114">Appendice B-formati di colore GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="fd499-114">Appendix B - Azure RTOS GUIX Color Formats</span></span>](appendix-b.md)

[<span data-ttu-id="fd499-115">Appendice C-stili del widget GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="fd499-115">Appendix C - Azure RTOS GUIX Widget Styles</span></span>](appendix-c.md)

[<span data-ttu-id="fd499-116">Appendice D: attributi pennello, Canvas e sfumatura di Azure RTO GUIX</span><span class="sxs-lookup"><span data-stu-id="fd499-116">Appendix D - Azure RTOS GUIX Brush, Canvas and Gradient Attributes</span></span>](appendix-d.md)

[<span data-ttu-id="fd499-117">Appendice E-Descrizione evento GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="fd499-117">Appendix E - Azure RTOS GUIX Event Description</span></span>](appendix-e.md)

[<span data-ttu-id="fd499-118">Appendice F-Azure RTO GUIX RTO binding Services</span><span class="sxs-lookup"><span data-stu-id="fd499-118">Appendix F - Azure RTOS GUIX RTOS Binding Services</span></span>](appendix-f.md)

[<span data-ttu-id="fd499-119">Appendice G-struttura del tipo di carattere GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="fd499-119">Appendix G - Azure RTOS GUIX Font Structure</span></span>](appendix-g.md)

[<span data-ttu-id="fd499-120">Appendice H-Azure RTO GUIX Build-Time flag di configurazione</span><span class="sxs-lookup"><span data-stu-id="fd499-120">Appendix H - Azure RTOS GUIX Build-Time Configuration flags</span></span>](appendix-h.md)

[<span data-ttu-id="fd499-121">Appendice I-strutture di informazioni GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="fd499-121">Appendix I - Azure RTOS GUIX Information Structures</span></span>](appendix-i.md)

## <a name="guide-conventions"></a><span data-ttu-id="fd499-122">Convenzioni della Guida</span><span class="sxs-lookup"><span data-stu-id="fd499-122">Guide Conventions</span></span>

<span data-ttu-id="fd499-123">*Italics* : il carattere tipografico denota i titoli dei libri, enfatizza le parole importanti e indica le variabili.</span><span class="sxs-lookup"><span data-stu-id="fd499-123">*Italics* - Typeface denotes book titles, emphasizes important words, and indicates variables.</span></span>

<span data-ttu-id="fd499-124">**Grassetto** -Typeface indica i nomi di file, le parole chiave e enfatizza ulteriormente le parole e le variabili importanti.</span><span class="sxs-lookup"><span data-stu-id="fd499-124">**Boldface** - Typeface denotes file names, key words, and further emphasizes important words and variables.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd499-125">I simboli informativi attirano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulla funzione.</span><span class="sxs-lookup"><span data-stu-id="fd499-125">Information symbols draw attention to important or additional information that could affect performance or function.</span></span>

## <a name="azure-rtos-guix-data-types"></a><span data-ttu-id="fd499-126">Tipi di dati GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="fd499-126">Azure RTOS GUIX Data Types</span></span>

<span data-ttu-id="fd499-127">Oltre ai tipi di dati della struttura di controllo GUIX di Azure RTO personalizzati, sono disponibili diversi tipi di dati speciali usati nelle interfacce di chiamata del servizio GUIX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="fd499-127">In addition to the custom Azure RTOS GUIX control structure data types, there are several special data types that are used in Azure RTOS GUIX service call interfaces.</span></span> <span data-ttu-id="fd499-128">Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante.</span><span class="sxs-lookup"><span data-stu-id="fd499-128">These special data types map directly to data types of the underlying C compiler.</span></span> <span data-ttu-id="fd499-129">Questa operazione viene eseguita per garantire la portabilità tra diversi compilatori C.</span><span class="sxs-lookup"><span data-stu-id="fd499-129">This is done to ensure portability between different C compilers.</span></span> <span data-ttu-id="fd499-130">L'implementazione esatta viene ereditata da ThreadX ed è disponibile nel file ***tx_port. h*** incluso nella distribuzione di threadX.</span><span class="sxs-lookup"><span data-stu-id="fd499-130">The exact implementation is inherited from ThreadX and can be found in the ***tx_port.h*** file included in the ThreadX distribution.</span></span>

<span data-ttu-id="fd499-131">Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio GUIX di Azure RTO e dei relativi significati:</span><span class="sxs-lookup"><span data-stu-id="fd499-131">The following is a list of Azure RTOS GUIX service call data types and their associated meanings:</span></span>

| <!-- --> | <!-- --> |
| --------------------- | --------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="fd499-132">**UINT**</span><span class="sxs-lookup"><span data-stu-id="fd499-132">**UINT**</span></span>             | <span data-ttu-id="fd499-133">Unsigned Integer di base.</span><span class="sxs-lookup"><span data-stu-id="fd499-133">Basic unsigned integer.</span></span> <span data-ttu-id="fd499-134">Questo tipo è mappato al tipo di dati senza segno più pratico.</span><span class="sxs-lookup"><span data-stu-id="fd499-134">This type is mapped to the most convenient unsigned data type.</span></span>                                |
| <span data-ttu-id="fd499-135">**INT**</span><span class="sxs-lookup"><span data-stu-id="fd499-135">**INT**</span></span>              | <span data-ttu-id="fd499-136">Intero con segno di base.</span><span class="sxs-lookup"><span data-stu-id="fd499-136">Basic signed integer.</span></span> <span data-ttu-id="fd499-137">Questo tipo è mappato al tipo di dati con segno più pratico.</span><span class="sxs-lookup"><span data-stu-id="fd499-137">This type is mapped to the most convenient signed data type.</span></span>                                    |
| <span data-ttu-id="fd499-138">**ULONG**</span><span class="sxs-lookup"><span data-stu-id="fd499-138">**ULONG**</span></span>            | <span data-ttu-id="fd499-139">Tipo long senza segno.</span><span class="sxs-lookup"><span data-stu-id="fd499-139">Unsigned long type.</span></span> <span data-ttu-id="fd499-140">Questo tipo deve supportare i dati senza segno a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="fd499-140">This type must support 32-bit unsigned data.</span></span>                                                      |
| <span data-ttu-id="fd499-141">**VUOTO**</span><span class="sxs-lookup"><span data-stu-id="fd499-141">**VOID**</span></span>             | <span data-ttu-id="fd499-142">Quasi sempre equivalente al tipo void del compilatore.</span><span class="sxs-lookup"><span data-stu-id="fd499-142">Almost always equivalent to the compiler’s void type.</span></span>                                                                 |
| <span data-ttu-id="fd499-143">**GX_CHAR**</span><span class="sxs-lookup"><span data-stu-id="fd499-143">**GX_CHAR**</span></span>         | <span data-ttu-id="fd499-144">Spesso typedef come tipo char definito dal compilatore.</span><span class="sxs-lookup"><span data-stu-id="fd499-144">Most often typedefed as the compiler defined char type.</span></span>                                                               |
| <span data-ttu-id="fd499-145">**GX_BYTE**</span><span class="sxs-lookup"><span data-stu-id="fd499-145">**GX_BYTE**</span></span>          | <span data-ttu-id="fd499-146">tipo con segno a 8 bit.</span><span class="sxs-lookup"><span data-stu-id="fd499-146">8-bit signed type.</span></span>                                                                                                    |
| <span data-ttu-id="fd499-147">**GX_UBYTE**</span><span class="sxs-lookup"><span data-stu-id="fd499-147">**GX_UBYTE**</span></span>         | <span data-ttu-id="fd499-148">tipo senza segno a 8 bit.</span><span class="sxs-lookup"><span data-stu-id="fd499-148">8-bit unsigned type.</span></span>                                                                                                  |
| <span data-ttu-id="fd499-149">**GX_VALUE**</span><span class="sxs-lookup"><span data-stu-id="fd499-149">**GX_VALUE**</span></span>        | <span data-ttu-id="fd499-150">tipo con segno a 16 o 32 bit.</span><span class="sxs-lookup"><span data-stu-id="fd499-150">16 or 32 bit signed type.</span></span> <span data-ttu-id="fd499-151">Definito in base alle esigenze per ottenere prestazioni ottimali sul sistema di destinazione.</span><span class="sxs-lookup"><span data-stu-id="fd499-151">Defined as needed for best performance on the target system.</span></span>                                |
| <span data-ttu-id="fd499-152">**GX_FIXED_VAL**</span><span class="sxs-lookup"><span data-stu-id="fd499-152">**GX_FIXED_VAL**</span></span>   | <span data-ttu-id="fd499-153">Tipo di dati numerico a virgola fissa.</span><span class="sxs-lookup"><span data-stu-id="fd499-153">Fixed point numeric data type.</span></span>                                                                                        |
| <span data-ttu-id="fd499-154">**GX_RESOURCE_ID**</span><span class="sxs-lookup"><span data-stu-id="fd499-154">**GX_RESOURCE_ID**</span></span> | <span data-ttu-id="fd499-155">Tipo long senza segno.</span><span class="sxs-lookup"><span data-stu-id="fd499-155">Unsigned long type.</span></span>                                                                                                   |
| <span data-ttu-id="fd499-156">**GX_COLOR**</span><span class="sxs-lookup"><span data-stu-id="fd499-156">**GX_COLOR**</span></span>        | <span data-ttu-id="fd499-157">Tipo long senza segno.</span><span class="sxs-lookup"><span data-stu-id="fd499-157">Unsigned long type.</span></span>                                                                                                   |
| <span data-ttu-id="fd499-158">**GX_STRING**</span><span class="sxs-lookup"><span data-stu-id="fd499-158">**GX_STRING**</span></span>       | <span data-ttu-id="fd499-159">Struttura che contiene GX_CHAR \* gx_string_ptr e UINT gx_string_length.</span><span class="sxs-lookup"><span data-stu-id="fd499-159">Structure containing GX_CHAR \*gx_string_ptr and UINT gx_string_length.</span></span>                                          |
| <span data-ttu-id="fd499-160">**GX_POINT**</span><span class="sxs-lookup"><span data-stu-id="fd499-160">**GX_POINT**</span></span>        | <span data-ttu-id="fd499-161">Struttura contenente gx_point_x e gx_point_y.</span><span class="sxs-lookup"><span data-stu-id="fd499-161">Structure containing gx_point_x and gx_point_y.</span></span>                                                                   |
| <span data-ttu-id="fd499-162">**GX_RECTANGLE**</span><span class="sxs-lookup"><span data-stu-id="fd499-162">**GX_RECTANGLE**</span></span>    | <span data-ttu-id="fd499-163">Struttura che contiene i campi gx_rectangle_left, gx_rectangle_top, gx_rectangle_right e gx_rectangle_bottom.</span><span class="sxs-lookup"><span data-stu-id="fd499-163">Structure containing gx_rectangle_left, gx_rectangle_top, gx_rectangle_right, and gx_rectangle_bottom fields.</span></span> |
| <span data-ttu-id="fd499-164">**GX_GLYPH**</span><span class="sxs-lookup"><span data-stu-id="fd499-164">**GX_GLYPH**</span></span>        | <span data-ttu-id="fd499-165">Struttura che contiene le metriche del glifo.</span><span class="sxs-lookup"><span data-stu-id="fd499-165">Structure containing glyph metrics.</span></span>                                                                                   |
| <span data-ttu-id="fd499-166">**GX_FONT**</span><span class="sxs-lookup"><span data-stu-id="fd499-166">**GX_FONT**</span></span>         | <span data-ttu-id="fd499-167">Struttura che contiene le metriche dei tipi di carattere.</span><span class="sxs-lookup"><span data-stu-id="fd499-167">Structure containing font metrics.</span></span>                                                                                    |
| <span data-ttu-id="fd499-168">**GX_BRUSH**</span><span class="sxs-lookup"><span data-stu-id="fd499-168">**GX_BRUSH**</span></span>        | <span data-ttu-id="fd499-169">Struttura che contiene le metriche del pennello.</span><span class="sxs-lookup"><span data-stu-id="fd499-169">Structure containing brush metrics.</span></span>                                                                               |
<span data-ttu-id="fd499-170">**GX_PIXELMAP**</span><span class="sxs-lookup"><span data-stu-id="fd499-170">**GX_PIXELMAP**</span></span>       | <span data-ttu-id="fd499-171">Struttura che contiene le metriche di Pixelmap.</span><span class="sxs-lookup"><span data-stu-id="fd499-171">Structure containing pixelmap metrics.</span></span>

<span data-ttu-id="fd499-172">I tipi di dati aggiuntivi vengono usati all'interno dell'origine GUIX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="fd499-172">Additional data types are used within the Azure RTOS GUIX source.</span></span> <span data-ttu-id="fd499-173">Si trovano nei file \***tx_port. h** _ o _ \*_gx_port. h_\*\*.</span><span class="sxs-lookup"><span data-stu-id="fd499-173">They are located in either the ***tx_port.h** _ or _ *_gx_port.h_** files.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="fd499-174">Centro assistenza clienti</span><span class="sxs-lookup"><span data-stu-id="fd499-174">Customer Support Center</span></span>

<span data-ttu-id="fd499-175">Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="fd499-175">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="fd499-176">Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:</span><span class="sxs-lookup"><span data-stu-id="fd499-176">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="fd499-177">Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="fd499-177">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>

2. <span data-ttu-id="fd499-178">Descrizione dettagliata delle modifiche apportate all'applicazione e/o GUIX RTO di Azure che hanno preceduto il problema.</span><span class="sxs-lookup"><span data-stu-id="fd499-178">A detailed description of any changes to the application and/or Azure RTOS GUIX that preceded the problem.</span></span>

3. <span data-ttu-id="fd499-179">Il contenuto delle stringhe _tx_version_id e _gx_version_id trovate nei file \***tx_port. h**_ e _ *_gx_port. h_*\* della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fd499-179">The contents of the _tx_version_id and _gx_version_id strings found in the \***tx_port.h**_ and _ *_gx_port.h_*\* files of your distribution.</span></span> <span data-ttu-id="fd499-180">Queste stringhe forniranno informazioni preziose sull'ambiente di run-time.</span><span class="sxs-lookup"><span data-stu-id="fd499-180">These strings will provide us valuable Information regarding your run-time environment.</span></span>

4. <span data-ttu-id="fd499-181">Contenuto della RAM delle variabili ULONG seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd499-181">The contents in RAM of the following ULONG variables:</span></span>

    <span data-ttu-id="fd499-182">**_tx_build_options** **_gx_system_build_options**</span><span class="sxs-lookup"><span data-stu-id="fd499-182">**_tx_build_options** **_gx_system_build_options**</span></span>

    <span data-ttu-id="fd499-183">Queste variabili forniranno informazioni su come sono state compilate le librerie di Azure RTO ThreadX e Azure RTO GUIX.</span><span class="sxs-lookup"><span data-stu-id="fd499-183">These variables will give us information on how your Azure RTOS ThreadX and Azure RTOS GUIX libraries were built.</span></span>

5. <span data-ttu-id="fd499-184">Contenuto della RAM delle variabili ULONG seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd499-184">The contents in RAM of the following ULONG variables:</span></span>

    <span data-ttu-id="fd499-185">**_gx_system_last_error** **_gx_system_error_count**</span><span class="sxs-lookup"><span data-stu-id="fd499-185">**_gx_system_last_error** **_gx_system_error_count**</span></span>

    <span data-ttu-id="fd499-186">Queste variabili tengono traccia degli errori interni del sistema in Azure RTO GUIX.</span><span class="sxs-lookup"><span data-stu-id="fd499-186">These variables keep track of internal system errors in Azure RTOS GUIX.</span></span> <span data-ttu-id="fd499-187">Se il _gx_system_error_count è maggiore di uno, impostare un punto di interruzione sulla funzione return nella funzione _gx_system_error_process e fornire il valore di _gx_system_last_error a questo punto.</span><span class="sxs-lookup"><span data-stu-id="fd499-187">If the _gx_system_error_count is greater than one, please set a breakpoint on the function return in the _gx_system_error_process function and provide the value of _gx_system_last_error at this point.</span></span> <span data-ttu-id="fd499-188">Verrà restituito il primo errore interno del sistema GUIX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="fd499-188">This will yield the first internal Azure RTOS GUIX system error.</span></span>

6. <span data-ttu-id="fd499-189">Un buffer di traccia acquisito immediatamente dopo che il problema è stato rilevato.</span><span class="sxs-lookup"><span data-stu-id="fd499-189">A trace buffer captured immediately after the problem was detected.</span></span> <span data-ttu-id="fd499-190">Questa operazione viene eseguita compilando le librerie Azure RTO ThreadX e Azure RTO GUIX con TX_ENABLE_EVENT_TRACE e chiamando tx_trace_enable con le informazioni sul buffer di traccia.</span><span class="sxs-lookup"><span data-stu-id="fd499-190">This is accomplished by building the Azure RTOS ThreadX and Azure RTOS GUIX libraries with TX_ENABLE_EVENT_TRACE and calling tx_trace_enable with the trace buffer information.</span></span>

7. <span data-ttu-id="fd499-191">Il progetto di Azure RTO GUIX studio in uso, se applicabile, o almeno un piccolo progetto sufficiente per dimostrare la carenza di report.</span><span class="sxs-lookup"><span data-stu-id="fd499-191">The Azure RTOS GUIX Studio project you are using, if applicable, or at a minimum a small project sufficient to demonstrate the deficiency you are reporting.</span></span>
