---
title: Informazioni sul manuale dell'utente di Azure RTO NetX
description: Questa guida contiene informazioni complete su Azure RTO NetX, lo stack di rete a prestazioni elevate Microsoft.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 01077e3315e87b918cdfd47423d8e0c1b6bbdbbd
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550270"
---
# <a name="about-the-azure-rtos-netx-user-guide"></a><span data-ttu-id="8829a-103">Informazioni sul manuale dell'utente di Azure RTO NetX</span><span class="sxs-lookup"><span data-stu-id="8829a-103">About The Azure RTOS NetX User Guide</span></span>

<span data-ttu-id="8829a-104">Questa guida contiene informazioni complete su Azure RTO NetX, lo stack di rete a prestazioni elevate Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8829a-104">This guide contains comprehensive information about Azure RTOS NetX, the Microsoft high-performance network stack.</span></span>

<span data-ttu-id="8829a-105">È concepito per gli sviluppatori di software in tempo reale incorporati che conoscono i concetti di base sulla rete, Azure RTO ThreadX e il linguaggio di programmazione C.</span><span class="sxs-lookup"><span data-stu-id="8829a-105">It is intended for embedded real-time software developers familiar with basic networking concepts, Azure RTOS ThreadX, and the C programming language.</span></span>

## <a name="organization"></a><span data-ttu-id="8829a-106">Organization</span><span class="sxs-lookup"><span data-stu-id="8829a-106">Organization</span></span>

<span data-ttu-id="8829a-107">[Capitolo 1](chapter1.md) -introduce Azure RTO NETX</span><span class="sxs-lookup"><span data-stu-id="8829a-107">[Chapter 1](chapter1.md) - Introduces Azure RTOS NetX</span></span>

<span data-ttu-id="8829a-108">[Capitolo 2](chapter2.md) : descrive i passaggi di base per installare e usare Azure RTO NETX con l'applicazione threadX.</span><span class="sxs-lookup"><span data-stu-id="8829a-108">[Chapter 2](chapter2.md) - Gives the basic steps to install and use Azure RTOS NetX with your ThreadX application.</span></span>

<span data-ttu-id="8829a-109">[Capitolo 3](chapter3.md) : viene fornita una panoramica funzionale del sistema NETX di Azure RTO e delle informazioni di base sugli standard di rete TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="8829a-109">[Chapter 3](chapter3.md) - Provides a functional overview of the Azure RTOS NetX system and basic information about the TCP/IP networking standards.</span></span>

<span data-ttu-id="8829a-110">[Capitolo 4](chapter4.md) : informazioni dettagliate sull'interfaccia dell'applicazione per Azure RTO NETX.</span><span class="sxs-lookup"><span data-stu-id="8829a-110">[Chapter 4](chapter4.md) - Details the application's interface to Azure RTOS NetX.</span></span>

<span data-ttu-id="8829a-111">[Capitolo 5](chapter5.md) : descrive i driver di rete per Azure RTO NETX.</span><span class="sxs-lookup"><span data-stu-id="8829a-111">[Chapter 5](chapter5.md) - Describes network drivers for Azure RTOS NetX.</span></span>

<span data-ttu-id="8829a-112">[Appendice A](appendix-a.md) -Servizi NETX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="8829a-112">[Appendix A](appendix-a.md) - Azure RTOS NetX Services</span></span>

<span data-ttu-id="8829a-113">[Appendice B](appendix-b.md) -costanti NETX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="8829a-113">[Appendix B](appendix-b.md) - Azure RTOS NetX Constants</span></span>

<span data-ttu-id="8829a-114">[Appendice C](appendix-c.md) -tipi di dati NETX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="8829a-114">[Appendix C](appendix-c.md) - Azure RTOS NetX Data Types</span></span>

<span data-ttu-id="8829a-115">[Appendice D](appendix-d.md) -BSD-Compatible API socket</span><span class="sxs-lookup"><span data-stu-id="8829a-115">[Appendix D](appendix-d.md) - BSD-Compatible Socket API</span></span>

<span data-ttu-id="8829a-116">[Appendice E](appendix-e.md) -grafico ASCII</span><span class="sxs-lookup"><span data-stu-id="8829a-116">[Appendix E](appendix-e.md) - ASCII Chart</span></span>

## <a name="azure-rtos-netx-data-types"></a><span data-ttu-id="8829a-117">Tipi di dati NetX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="8829a-117">Azure RTOS NetX Data Types</span></span>

<span data-ttu-id="8829a-118">Oltre ai tipi di dati della struttura di controllo NetX di Azure RTO personalizzati, sono disponibili diversi tipi di dati speciali usati nelle interfacce di chiamata del servizio NetX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="8829a-118">In addition to the custom Azure RTOS NetX control structure data types, there are several special data types that are used in Azure RTOS NetX service call interfaces.</span></span> <span data-ttu-id="8829a-119">Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante.</span><span class="sxs-lookup"><span data-stu-id="8829a-119">These special data types map directly to data types of the underlying C compiler.</span></span> <span data-ttu-id="8829a-120">Questa operazione viene eseguita per garantire la portabilità tra diversi compilatori C.</span><span class="sxs-lookup"><span data-stu-id="8829a-120">This is done to ensure portability between different C compilers.</span></span> <span data-ttu-id="8829a-121">L'implementazione esatta viene ereditata da ThreadX ed è disponibile nel file ***tx_port. h*** incluso nella distribuzione di threadX.</span><span class="sxs-lookup"><span data-stu-id="8829a-121">The exact implementation is inherited from ThreadX and can be found in the ***tx_port.h*** file included in the ThreadX distribution.</span></span>

<span data-ttu-id="8829a-122">Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio NetX di Azure RTO e dei relativi significati:</span><span class="sxs-lookup"><span data-stu-id="8829a-122">The following is a list of Azure RTOS NetX service call data types and their associated meanings:</span></span>

| <span data-ttu-id="8829a-123">Tipi di dati</span><span class="sxs-lookup"><span data-stu-id="8829a-123">Data Types</span></span> | <span data-ttu-id="8829a-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8829a-124">Description</span></span>  |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="8829a-125">**UINT**</span><span class="sxs-lookup"><span data-stu-id="8829a-125">**UINT**</span></span>  | <span data-ttu-id="8829a-126">Unsigned Integer di base.</span><span class="sxs-lookup"><span data-stu-id="8829a-126">Basic unsigned integer.</span></span> <span data-ttu-id="8829a-127">Questo tipo deve supportare i dati senza segno a 32 bit; viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico.</span><span class="sxs-lookup"><span data-stu-id="8829a-127">This type must support 32-bit unsigned data; however, it is mapped to the most convenient unsigned data type.</span></span> |
| <span data-ttu-id="8829a-128">**ULONG**</span><span class="sxs-lookup"><span data-stu-id="8829a-128">**ULONG**</span></span> | <span data-ttu-id="8829a-129">Tipo long senza segno.</span><span class="sxs-lookup"><span data-stu-id="8829a-129">Unsigned long type.</span></span> <span data-ttu-id="8829a-130">Questo tipo deve supportare i dati senza segno a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="8829a-130">This type must support 32-bit unsigned data.</span></span>                                                                      |
| <span data-ttu-id="8829a-131">**VUOTO**</span><span class="sxs-lookup"><span data-stu-id="8829a-131">**VOID**</span></span>  | <span data-ttu-id="8829a-132">Quasi sempre equivalente al tipo void del compilatore.</span><span class="sxs-lookup"><span data-stu-id="8829a-132">Almost always equivalent to the compiler's void type.</span></span>                                                                                 |
| <span data-ttu-id="8829a-133">**CHAR**</span><span class="sxs-lookup"><span data-stu-id="8829a-133">**CHAR**</span></span>  | <span data-ttu-id="8829a-134">Spesso un tipo di carattere standard a 8 bit.</span><span class="sxs-lookup"><span data-stu-id="8829a-134">Most often a standard 8-bit character type.</span></span>                                                                                           |

<span data-ttu-id="8829a-135">I tipi di dati aggiuntivi vengono usati all'interno dell'origine NetX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="8829a-135">Additional data types are used within the Azure RTOS NetX source.</span></span> <span data-ttu-id="8829a-136">Si trovano nei file \***tx_port. h** _ o _ \*_nx_port. h_\*\*.</span><span class="sxs-lookup"><span data-stu-id="8829a-136">They are located in either the ***tx_port.h** _ or _ *_nx_port.h_** files.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="8829a-137">Centro assistenza clienti</span><span class="sxs-lookup"><span data-stu-id="8829a-137">Customer Support Center</span></span>

<span data-ttu-id="8829a-138">Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="8829a-138">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="8829a-139">Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:</span><span class="sxs-lookup"><span data-stu-id="8829a-139">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="8829a-140">Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="8829a-140">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>

2. <span data-ttu-id="8829a-141">Descrizione dettagliata delle modifiche apportate all'applicazione e/o NetX RTO di Azure che hanno preceduto il problema.</span><span class="sxs-lookup"><span data-stu-id="8829a-141">A detailed description of any changes to the application and/or Azure RTOS NetX that preceded the problem.</span></span>

3. <span data-ttu-id="8829a-142">Il contenuto delle stringhe **_tx_version_id** e **_nx_version_id** trovate nei file **_tx_port. h_*_ e _*_nx_port. h_** della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8829a-142">The contents of the **_tx_version_id** and **_nx_version_id** strings found in the **_tx_port.h_*_ and _*_nx_port.h_** files of your distribution.</span></span> <span data-ttu-id="8829a-143">Queste stringhe forniranno informazioni preziose sull'ambiente di run-time.</span><span class="sxs-lookup"><span data-stu-id="8829a-143">These strings will provide us valuable information regarding your run-time environment.</span></span>

4. <span data-ttu-id="8829a-144">Contenuto della RAM delle variabili **ULONG** seguenti:</span><span class="sxs-lookup"><span data-stu-id="8829a-144">The contents in RAM of the following **ULONG** variables:</span></span>

    <span data-ttu-id="8829a-145">**_tx_build_options**</span><span class="sxs-lookup"><span data-stu-id="8829a-145">**_tx_build_options**</span></span>

    <span data-ttu-id="8829a-146">**_nx_system_build_options1**</span><span class="sxs-lookup"><span data-stu-id="8829a-146">**_nx_system_build_options1**</span></span>

    <span data-ttu-id="8829a-147">**_nx_system_build_options2**</span><span class="sxs-lookup"><span data-stu-id="8829a-147">**_nx_system_build_options2**</span></span>

    <span data-ttu-id="8829a-148">**_nx_system_build_options3**</span><span class="sxs-lookup"><span data-stu-id="8829a-148">**_nx_system_build_options3**</span></span>

    <span data-ttu-id="8829a-149">**_nx_system_build_options4**</span><span class="sxs-lookup"><span data-stu-id="8829a-149">**_nx_system_build_options4**</span></span>

    <span data-ttu-id="8829a-150">**_nx_system_build_options5**</span><span class="sxs-lookup"><span data-stu-id="8829a-150">**_nx_system_build_options5**</span></span>

    <span data-ttu-id="8829a-151">Queste variabili forniranno informazioni su come sono state compilate le librerie di Azure RTO ThreadX e Azure RTO NetX.</span><span class="sxs-lookup"><span data-stu-id="8829a-151">These variables will give us information on how your Azure RTOS ThreadX and Azure RTOS NetX libraries were built.</span></span>

5. <span data-ttu-id="8829a-152">Un buffer di traccia acquisito immediatamente dopo che il problema è stato rilevato.</span><span class="sxs-lookup"><span data-stu-id="8829a-152">A trace buffer captured immediately after the problem was detected.</span></span> <span data-ttu-id="8829a-153">Questa operazione viene eseguita compilando le librerie Azure RTO ThreadX e Azure RTO NetX con **TX_ENABLE_EVENT_TRACE** e chiamando **tx_trace_enable** con le informazioni sul buffer di traccia.</span><span class="sxs-lookup"><span data-stu-id="8829a-153">This is accomplished by building the Azure RTOS ThreadX and Azure RTOS NetX libraries with **TX_ENABLE_EVENT_TRACE** and calling **tx_trace_enable** with the trace buffer information.</span></span> <span data-ttu-id="8829a-154">Per informazioni dettagliate, vedere la guida dell'utente di Azure RTO TraceX.</span><span class="sxs-lookup"><span data-stu-id="8829a-154">Refer to the Azure RTOS TraceX User Guide for details.</span></span>
