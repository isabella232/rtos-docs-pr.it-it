---
title: Informazioni sul manuale dell'utente di Azure RTO NetX Duo
description: Questa guida contiene informazioni complete su Azure RTO NetX Duo, lo stack Dual Network IPv4/IPv6 a prestazioni elevate Microsoft.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b1eef5bfa28f13d7a6b627792f96039b252f2355
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822142"
---
# <a name="about-the-azure-rtos-netx-duo-user-guide"></a><span data-ttu-id="645b8-103">Informazioni sul manuale dell'utente di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="645b8-103">About The Azure RTOS NetX Duo User Guide</span></span>

<span data-ttu-id="645b8-104">Questa guida contiene informazioni complete su Azure RTO NetX Duo, lo stack Dual Network IPv4/IPv6 a prestazioni elevate Microsoft.</span><span class="sxs-lookup"><span data-stu-id="645b8-104">This guide contains comprehensive information about Azure RTOS NetX Duo, the Microsoft high-performance IPv4/IPv6 dual network stack.</span></span> 

<span data-ttu-id="645b8-105">È concepito per gli sviluppatori di software in tempo reale incorporati che conoscono i concetti di base sulla rete, Azure RTO ThreadX e il linguaggio di programmazione C.</span><span class="sxs-lookup"><span data-stu-id="645b8-105">It is intended for embedded real-time software developers familiar with basic networking concepts, Azure RTOS ThreadX, and the C programming language.</span></span>

## <a name="organization"></a><span data-ttu-id="645b8-106">Organization</span><span class="sxs-lookup"><span data-stu-id="645b8-106">Organization</span></span>

<span data-ttu-id="645b8-107">[Capitolo 1](chapter1.md) -introduce Azure RTO NETX Duo</span><span class="sxs-lookup"><span data-stu-id="645b8-107">[Chapter 1](chapter1.md) - Introduces Azure RTOS NetX Duo</span></span>

<span data-ttu-id="645b8-108">[Capitolo 2](chapter2.md) : fornisce i passaggi di base per installare e usare Azure RTO NETX Duo con l'applicazione threadX</span><span class="sxs-lookup"><span data-stu-id="645b8-108">[Chapter 2](chapter2.md) - Gives the basic steps to install and use Azure RTOS NetX Duo with your ThreadX application</span></span>

<span data-ttu-id="645b8-109">[Capitolo 3](chapter3.md) -Panoramica funzionale del sistema Azure RTO NETX Duo e informazioni di base sugli standard di rete TCP/IP</span><span class="sxs-lookup"><span data-stu-id="645b8-109">[Chapter 3](chapter3.md) - Provides a functional overview of the Azure RTOS NetX Duo system and basic information about the TCP/IP networking standards</span></span>

<span data-ttu-id="645b8-110">[Capitolo 4](chapter4.md) : informazioni dettagliate sull'interfaccia dell'applicazione per Azure RTO NETX Duo</span><span class="sxs-lookup"><span data-stu-id="645b8-110">[Chapter 4](chapter4.md) - Details the application's interface to Azure RTOS NetX Duo</span></span>

<span data-ttu-id="645b8-111">[Capitolo 5](chapter5.md) -descrive i driver di rete per Azure RTO NETX Duo</span><span class="sxs-lookup"><span data-stu-id="645b8-111">[Chapter 5](chapter5.md) - Describes network drivers for Azure RTOS NetX Duo</span></span>

<span data-ttu-id="645b8-112">[Appendice A](appendix-a.md) -Azure RTO NETX Duo Services</span><span class="sxs-lookup"><span data-stu-id="645b8-112">[Appendix A](appendix-a.md) - Azure RTOS NetX Duo Services</span></span>

<span data-ttu-id="645b8-113">[Appendice B](appendix-b.md) -costanti di Azure RTO NETX Duo</span><span class="sxs-lookup"><span data-stu-id="645b8-113">[Appendix B](appendix-b.md) - Azure RTOS NetX Duo Constants</span></span>

<span data-ttu-id="645b8-114">[Appendice C](appendix-c.md) -tipi di dati di Azure RTO NETX Duo</span><span class="sxs-lookup"><span data-stu-id="645b8-114">[Appendix C](appendix-c.md) - Azure RTOS NetX Duo Data Types</span></span>

<span data-ttu-id="645b8-115">[Appendice D](appendix-d.md) -BSD-Compatible API socket</span><span class="sxs-lookup"><span data-stu-id="645b8-115">[Appendix D](appendix-d.md) - BSD-Compatible Socket API</span></span>

<span data-ttu-id="645b8-116">[Appendice E](appendix-e.md) -grafico ASCII</span><span class="sxs-lookup"><span data-stu-id="645b8-116">[Appendix E](appendix-e.md) - ASCII Chart</span></span>

## <a name="guide-conventions"></a><span data-ttu-id="645b8-117">Convenzioni della Guida</span><span class="sxs-lookup"><span data-stu-id="645b8-117">Guide Conventions</span></span>

<span data-ttu-id="645b8-118">Italics: il carattere tipografico denota i titoli dei libri, enfatizza le parole importanti e indica le variabili.</span><span class="sxs-lookup"><span data-stu-id="645b8-118">Italics - Typeface denotes book titles, emphasizes important words, and indicates variables.</span></span>

<span data-ttu-id="645b8-119">**Grassetto** -Typeface indica i nomi di file, le parole chiave e enfatizza ulteriormente le parole e le variabili importanti.</span><span class="sxs-lookup"><span data-stu-id="645b8-119">**Boldface** - Typeface denotes file names, key words, and further emphasizes important words and variables.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="645b8-120">I simboli informativi attirano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulla funzione.</span><span class="sxs-lookup"><span data-stu-id="645b8-120">Information symbols draw attention to important or additional information that could affect performance or function.</span></span>
 
> [!WARNING]
> <span data-ttu-id="645b8-121">I simboli di avviso attirano l'attenzione sulle situazioni che gli sviluppatori devono evitare perché potrebbero causare errori irreversibili.</span><span class="sxs-lookup"><span data-stu-id="645b8-121">Warning symbols draw attention to situations that developers should avoid because they could cause fatal errors.</span></span>

## <a name="azure-rtos-netx-duo-data-types"></a><span data-ttu-id="645b8-122">Tipi di dati di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="645b8-122">Azure RTOS NetX Duo Data Types</span></span>

<span data-ttu-id="645b8-123">Oltre ai tipi di dati personalizzati della struttura di controllo di Azure RTO NetX Duo, sono disponibili diversi tipi di dati speciali usati nelle interfacce di chiamata del servizio Azure RTO NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="645b8-123">In addition to the custom Azure RTOS NetX Duo control structure data types, there are several special data types that are used in Azure RTOS NetX Duo service call interfaces.</span></span> <span data-ttu-id="645b8-124">Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante.</span><span class="sxs-lookup"><span data-stu-id="645b8-124">These special data types map directly to data types of the underlying C compiler.</span></span> <span data-ttu-id="645b8-125">Questa operazione viene eseguita per garantire la portabilità tra diversi compilatori C.</span><span class="sxs-lookup"><span data-stu-id="645b8-125">This is done to ensure portability between different C compilers.</span></span> <span data-ttu-id="645b8-126">L'implementazione esatta viene ereditata da ThreadX ed è disponibile nel file ***tx_port. h*** incluso nella distribuzione di threadX.</span><span class="sxs-lookup"><span data-stu-id="645b8-126">The exact implementation is inherited from ThreadX and can be found in the ***tx_port.h*** file included in the ThreadX distribution.</span></span>

<span data-ttu-id="645b8-127">Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio RTO NetX duo di Azure e dei relativi significati:</span><span class="sxs-lookup"><span data-stu-id="645b8-127">The following is a list of Azure RTOS NetX Duo service call data types and their associated meanings:</span></span>

<span data-ttu-id="645b8-128">**Uint**: Unsigned Integer di base.</span><span class="sxs-lookup"><span data-stu-id="645b8-128">**UINT**: Basic unsigned integer.</span></span> <span data-ttu-id="645b8-129">Questo tipo deve supportare i dati senza segno a 32 bit; viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico.</span><span class="sxs-lookup"><span data-stu-id="645b8-129">This type must support 32-bit unsigned data; however, it is mapped to the most convenient unsigned data type.</span></span>  
<span data-ttu-id="645b8-130">**ULONG**: tipo long senza segno.</span><span class="sxs-lookup"><span data-stu-id="645b8-130">**ULONG**: Unsigned long type.</span></span> <span data-ttu-id="645b8-131">Questo tipo deve supportare i dati senza segno a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="645b8-131">This type must support 32-bit unsigned  data.</span></span>
<span data-ttu-id="645b8-132">**Void**: quasi sempre equivalente al tipo void del compilatore.</span><span class="sxs-lookup"><span data-stu-id="645b8-132">**VOID**: Almost always equivalent to the compiler's void type.</span></span>  
<span data-ttu-id="645b8-133">**Char**: più spesso un tipo di carattere standard a 8 bit.</span><span class="sxs-lookup"><span data-stu-id="645b8-133">**CHAR**: Most often a standard 8-bit character type.</span></span>  

<span data-ttu-id="645b8-134">I tipi di dati aggiuntivi vengono usati nell'origine Azure RTO NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="645b8-134">Additional data types are used within the Azure RTOS NetX Duo source.</span></span> <span data-ttu-id="645b8-135">Si trovano nei file \***tx_port. h** _ o _ \*_nx_port. h_\*\*.</span><span class="sxs-lookup"><span data-stu-id="645b8-135">They are located in either the ***tx_port.h** _ or _ *_nx_port.h_** files.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="645b8-136">Centro assistenza clienti</span><span class="sxs-lookup"><span data-stu-id="645b8-136">Customer Support Center</span></span>

<span data-ttu-id="645b8-137">Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="645b8-137">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="645b8-138">Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:</span><span class="sxs-lookup"><span data-stu-id="645b8-138">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="645b8-139">Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="645b8-139">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="645b8-140">Descrizione dettagliata delle modifiche apportate all'applicazione e/o al duo NetX di Azure RTO che hanno preceduto il problema.</span><span class="sxs-lookup"><span data-stu-id="645b8-140">A detailed description of any changes to the application and/or Azure RTOS NetX Duo that preceded the problem.</span></span>
3. <span data-ttu-id="645b8-141">Il contenuto delle stringhe _tx_version_id e _nx_version_id trovate nei file tx_port. h e nx_port. h della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="645b8-141">The contents of the _tx_version_id and _nx_version_id strings found in the tx_port.h and nx_port.h files of your distribution.</span></span> <span data-ttu-id="645b8-142">Queste stringhe forniranno informazioni preziose sull'ambiente di run-time.</span><span class="sxs-lookup"><span data-stu-id="645b8-142">These strings will provide us valuable information regarding your run- time environment.</span></span>
4. <span data-ttu-id="645b8-143">Contenuto della RAM delle variabili ULONG seguenti:</span><span class="sxs-lookup"><span data-stu-id="645b8-143">The contents in RAM of the following ULONG variables:</span></span>

    <span data-ttu-id="645b8-144">**_tx_build_options**</span><span class="sxs-lookup"><span data-stu-id="645b8-144">**_tx_build_options**</span></span>

    <span data-ttu-id="645b8-145">**_nx_system_build_options1**</span><span class="sxs-lookup"><span data-stu-id="645b8-145">**_nx_system_build_options1**</span></span>

    <span data-ttu-id="645b8-146">**_nx_system_build_options2**</span><span class="sxs-lookup"><span data-stu-id="645b8-146">**_nx_system_build_options2**</span></span>

    <span data-ttu-id="645b8-147">**_nx_system_build_options3**</span><span class="sxs-lookup"><span data-stu-id="645b8-147">**_nx_system_build_options3**</span></span>

    <span data-ttu-id="645b8-148">**_nx_system_build_options4**</span><span class="sxs-lookup"><span data-stu-id="645b8-148">**_nx_system_build_options4**</span></span>

    <span data-ttu-id="645b8-149">**_nx_system_build_options5**</span><span class="sxs-lookup"><span data-stu-id="645b8-149">**_nx_system_build_options5**</span></span>

    <span data-ttu-id="645b8-150">Queste variabili forniranno informazioni su come sono state compilate le librerie di Azure RTO ThreadX e Azure RTO NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="645b8-150">These variables will give us information on how your Azure RTOS ThreadX and Azure RTOS NetX Duo libraries were built.</span></span>

5. <span data-ttu-id="645b8-151">Un buffer di traccia acquisito immediatamente dopo che il problema è stato rilevato.</span><span class="sxs-lookup"><span data-stu-id="645b8-151">A trace buffer captured immediately after the problem was detected.</span></span> <span data-ttu-id="645b8-152">Questa operazione viene eseguita compilando le librerie di Azure RTO ThreadX e Azure RTO NetX Duo con TX_ENABLE_EVENT_TRACE e chiamando tx_trace_enable con le informazioni del buffer di traccia.</span><span class="sxs-lookup"><span data-stu-id="645b8-152">This is accomplished by building the Azure RTOS ThreadX and Azure RTOS NetX Duo libraries with TX_ENABLE_EVENT_TRACE and calling tx_trace_enable with the trace buffer information.</span></span>
