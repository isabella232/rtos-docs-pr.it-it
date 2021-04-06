---
title: Capitolo 1-Introduzione al kit del profilo di esecuzione
description: Questo capitolo contiene un'introduzione ad Azure RTO ThreadX Execution Profile Kit (EPK).
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7d30676437535229ad5bdbca10dcc9ca009d6e74
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377618"
---
# <a name="chapter-1--introduction-to-the-execution-profile-kit"></a><span data-ttu-id="fb658-103">Capitolo 1 Introduzione al kit del profilo di esecuzione</span><span class="sxs-lookup"><span data-stu-id="fb658-103">Chapter 1  Introduction to the Execution Profile Kit</span></span>

<span data-ttu-id="fb658-104">Il EPK (ThreadX Execution Profile Kit) fornisce un'infrastruttura per le applicazioni che consentono di tenere traccia dinamica del tempo di esecuzione per i thread, le routine del servizio di interrupt (ISRs) e le condizioni di sistema inattive.</span><span class="sxs-lookup"><span data-stu-id="fb658-104">The ThreadX Execution Profile Kit (EPK) provides an infrastructure for applications to dynamically track execution time for threads, Interrupt Service Routines (ISRs), and idle system conditions.</span></span> <span data-ttu-id="fb658-105">Questa operazione è particolarmente utile per l'ottimizzazione e l'ottimizzazione dell'applicazione per ottenere le prestazioni massime.</span><span class="sxs-lookup"><span data-stu-id="fb658-105">This is especially useful for optimization and tuning the application for maximum performance.</span></span> <span data-ttu-id="fb658-106">Tuttavia, è anche un utile strumento di debug.</span><span class="sxs-lookup"><span data-stu-id="fb658-106">However, it is also a valuable debug aid.</span></span>

<span data-ttu-id="fb658-107">EPK si basa sugli \" hook \" incorporati nella logica di pianificazione di threadX nel codice dell'assembly chiamati sulla voce del thread, sulla chiusura del thread, sulla voce ISR e sull'uscita ISR.</span><span class="sxs-lookup"><span data-stu-id="fb658-107">The EPK relies on \"hooks\" built into the ThreadX scheduling logic in assembly code that are called on thread entry, thread exit, ISR entry, and ISR exit.</span></span> <span data-ttu-id="fb658-108">Le routine EPK calcolano l'intervallo di tempo tra questi eventi e archiviano l'ora Delta nelle variabili globali, nonché i membri del blocco di controllo **TX_THREAD** .</span><span class="sxs-lookup"><span data-stu-id="fb658-108">The EPK routines calculate the time in between such events and store the delta time in global variables as well as members of the **TX_THREAD** control block.</span></span>

> [!NOTE]
> <span data-ttu-id="fb658-109">*Lo sviluppatore può modificare o persino sostituire queste funzioni hook con la propria logica per abilitare o disabilitare i pin di i/O in modo da fornire visibilità hardware a un'applicazione threadX in esecuzione*.</span><span class="sxs-lookup"><span data-stu-id="fb658-109">*The developer is free to modify or even replace these hook functions with their own logic to toggle I/O pins in order to provide hardware visibility to a running ThreadX application*.</span></span>

## 

## <a name="epk-requirements"></a><span data-ttu-id="fb658-110">Requisiti di EPK</span><span class="sxs-lookup"><span data-stu-id="fb658-110">EPK Requirements</span></span>

<span data-ttu-id="fb658-111">Per il funzionamento di EPK è necessario ThreadX 6,0 (o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="fb658-111">The EPK requires ThreadX 6.0 (or above) in order to operate.</span></span> <span data-ttu-id="fb658-112">Il EPK richiede anche una \" ragionevole \" risoluzione, incrementando l'origine del tempo hardware.</span><span class="sxs-lookup"><span data-stu-id="fb658-112">The EPK also requires a \"reasonable\" resolution, incrementing hardware time source.</span></span> <span data-ttu-id="fb658-113">La risoluzione più ragionevole sarebbe in genere qualcosa in una scala microsecondo.</span><span class="sxs-lookup"><span data-stu-id="fb658-113">The most reasonable resolution would typically be something on a microsecond scale.</span></span> <span data-ttu-id="fb658-114">Se la risoluzione è troppo grande, il numero massimo di contatori EPK sarà troppo rapido.</span><span class="sxs-lookup"><span data-stu-id="fb658-114">If the resolution is too great, the EPK counters will max out too quickly.</span></span> <span data-ttu-id="fb658-115">Viceversa, se la risoluzione è troppo piccola, non è possibile un intervallo preciso.</span><span class="sxs-lookup"><span data-stu-id="fb658-115">Conversely, if the resolution is too small, accurate timing is not possible.</span></span> <span data-ttu-id="fb658-116">L'origine del tempo applicazione è definita in \***tx_execution_profile. h** _ dalla macro _ \* TX_EXECUTION_TIME_SOURCE \* \*.</span><span class="sxs-lookup"><span data-stu-id="fb658-116">The application time source is defined in ***tx_execution_profile.h** _ by the macro _*TX_EXECUTION_TIME_SOURCE\*\*.</span></span>

<span data-ttu-id="fb658-117">Il compilatore C deve supportare il tipo \" unsigned long long \" per i contatori totali senza segno a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="fb658-117">The C compiler must support the type \"unsigned long long\" for unsigned 64-bit total counters.</span></span> <span data-ttu-id="fb658-118">Inoltre, EPK presuppone che le variabili globali siano inizializzate dal codice di avvio della fase di esecuzione del compilatore.</span><span class="sxs-lookup"><span data-stu-id="fb658-118">Furthermore, the EPK assumes the global variables are initialized by the compiler run-time startup code.</span></span> <span data-ttu-id="fb658-119">In caso contrario, le variabili globali definite in ***tx_execution_profile. c*** devono essere inizializzate su 0 dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fb658-119">If this is not the case, the global variables defined in ***tx_execution_profile.c*** must be initialized to 0 by the application.</span></span>

## <a name="epk-installation"></a><span data-ttu-id="fb658-120">Installazione di EPK</span><span class="sxs-lookup"><span data-stu-id="fb658-120">EPK Installation</span></span>

<span data-ttu-id="fb658-121">Per installare il EPK ThreadX, attenersi alla procedura seguente e ricompilare l'intera applicazione e la libreria ThreadX.</span><span class="sxs-lookup"><span data-stu-id="fb658-121">To install the ThreadX EPK, follow the steps below and rebuild the entire ThreadX library and application.</span></span>

1. <span data-ttu-id="fb658-122">Includere i file di origine EPK (***tx_execution_profile. h** _ e _*_tx_execution_profile. c_\*_) nel progetto di compilazione della libreria threadX.</span><span class="sxs-lookup"><span data-stu-id="fb658-122">Include the EPK source files (***tx_execution_profile.h** _ and _*_tx_execution_profile.c_\*_) in your ThreadX library build project.</span></span> <span data-ttu-id="fb658-123">Questi file possono trovarsi nel [repository threadX di Azure RTO](<https://github.com/azure-rtos/threadx>) nella cartella _ \*_Utility/Execution_Profile_\*\*).</span><span class="sxs-lookup"><span data-stu-id="fb658-123">These files can be in the [Azure RTOS ThreadX repo](<https://github.com/azure-rtos/threadx>) under the _ *_utility/Execution_Profile_*\* folder).</span></span>

1. <span data-ttu-id="fb658-124">In ***tx_port. h** _ definire la macro _ *TX_THREAD_EXTENSION_3** come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="fb658-124">In ***tx_port.h** _, define the _ *TX_THREAD_EXTENSION_3** macro as follows.</span></span>
```
    #define TX_THREAD_EXTENSION_3 unsigned long long tx_thread_execution_time_total; \
    unsigned long tx_thread_execution_time_last_start;
```

3. <span data-ttu-id="fb658-125">Definire la macro **TX_EXECUTION_TIME_SOURCE** in **_tx_execution_profile. h_** per eseguire il mapping all'origine del tempo hardware.</span><span class="sxs-lookup"><span data-stu-id="fb658-125">Define the **TX_EXECUTION_TIME_SOURCE** macro in **_tx_execution_profile.h_** to map to your hardware time source.</span></span>

1. <span data-ttu-id="fb658-126">Verificare che l'ambiente di compilazione definisca **TX_ENABLE_EXECUTION_CHANGE_NOTIFY** in modo che gli hook di pianificazione vengano chiamati dal codice dell'assembly threadX.</span><span class="sxs-lookup"><span data-stu-id="fb658-126">Ensure that the build environment defines **TX_ENABLE_EXECUTION_CHANGE_NOTIFY** so that the scheduling hooks are called from the ThreadX assembly code.</span></span>

1. <span data-ttu-id="fb658-127">Se si vuole usare l'origine ora 64 bit, vedere il file ***tx_execution_profile. h*** per istruzioni su come eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="fb658-127">If you wish to use 64-bit time source, please review the ***tx_execution_profile.h*** file for instructions on how to accomplish this.</span></span>

1. <span data-ttu-id="fb658-128">Ricompilare l'intera libreria e l'applicazione in modo che tutte le opzioni siano compilate correttamente.</span><span class="sxs-lookup"><span data-stu-id="fb658-128">Rebuild the entire library and application so that all of these options are properly compiled-in.</span></span>

<span data-ttu-id="fb658-129">A questo punto è possibile usare EPK con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fb658-129">You are now ready to use EPK with your application.</span></span>

##  <a name="epk-example"></a><span data-ttu-id="fb658-130">Esempio di EPK</span><span class="sxs-lookup"><span data-stu-id="fb658-130">EPK Example</span></span> 

<span data-ttu-id="fb658-131">Di seguito è riportato un esempio di EPK usato in una dimostrazione ThreadX standard, configurato con un'origine timer a 32 bit che incrementa 7,2 volte al microsecondo.</span><span class="sxs-lookup"><span data-stu-id="fb658-131">The following is an example of EPK being used on a standard ThreadX demonstration, configured with a 32-bit timer source that increments 7.2 times per microsecond.</span></span> 

<span data-ttu-id="fb658-132">La macro **TX_EXECUTION_TIME_SOURCE** viene definita per prelevare il registro timer mappato alla memoria in 0xE0001004, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="fb658-132">The **TX_EXECUTION_TIME_SOURCE** macro is defined to pick up the memory-mapped timer register at 0xE0001004, as follows.</span></span>
```
(EXECUTION_TIME_SOURCE_TYPE) \*((ULONG \*) 0xE0001004)
```

<span data-ttu-id="fb658-133">Se si lascia che la dimostrazione venga eseguita per cinque secondi, vengono restituiti i risultati seguenti.</span><span class="sxs-lookup"><span data-stu-id="fb658-133">Letting the demonstration run for five seconds yields the following results.</span></span>

![Risultati dell'esecuzione della demo.](media/demo_results.png)

<span data-ttu-id="fb658-135">Poiché la dimostrazione ThreadX standard non ha tempo di inattività (i thread 1 e 2 vengono eseguiti in modo continuo), il EPK segnala correttamente zero per il tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="fb658-135">Since the standard ThreadX demonstration has no idle time (threads 1 and 2 run continuously), the EPK correctly reports zero for idle time.</span></span> <span data-ttu-id="fb658-136">I valori di tempo totale ISR e thread possono essere divisi per 7,2 per derivare i microsecondi per ogni categoria di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fb658-136">The ISR total time and thread values may be divided by 7.2 in order to derive the microseconds for each execution category.</span></span> <span data-ttu-id="fb658-137">Il EPK fornisce anche le API per accedere a queste informazioni (vedere il [capitolo 2](chapter2.md)).</span><span class="sxs-lookup"><span data-stu-id="fb658-137">The EPK also provides APIs to access this information (please see please see [Chapter 2](chapter2.md)).</span></span>