---
title: Guida dell'utente di Azure RTO FileX
description: Questa guida contiene informazioni complete su Azure RTO FileX, il file system in tempo reale ad alte prestazioni di Microsoft.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 640d9ed4c8037d3af6c5f45158c9496ad1258a3c
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550100"
---
# <a name="about-this-filex-user-guide"></a><span data-ttu-id="e59f6-103">Informazioni su questo manuale dell'utente di FileX</span><span class="sxs-lookup"><span data-stu-id="e59f6-103">About This FileX User Guide</span></span>

<span data-ttu-id="e59f6-104">Questa guida contiene informazioni complete su Azure RTO FileX, il file system incorporato a prestazioni elevate e in tempo reale da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e59f6-104">This guide contains comprehensive information about Azure RTOS FileX, the high-performance, real-time embedded file system from Microsoft.</span></span> <span data-ttu-id="e59f6-105">Per ottenere il massimo da questa guida, è necessario avere familiarità con le funzioni del sistema operativo in tempo reale standard, i servizi FAT file system e il linguaggio di programmazione C.</span><span class="sxs-lookup"><span data-stu-id="e59f6-105">To gain the most from this guide, you should be familiar with standard real-time operating system functions, FAT file system services, and the C programming language.</span></span>

## <a name="organization"></a><span data-ttu-id="e59f6-106">Organization</span><span class="sxs-lookup"><span data-stu-id="e59f6-106">Organization</span></span>

<span data-ttu-id="e59f6-107">[Capitolo 1](chapter1.md) -introduce Azure RTO FILEX</span><span class="sxs-lookup"><span data-stu-id="e59f6-107">[Chapter 1](chapter1.md) - Introduces Azure RTOS FileX</span></span>

<span data-ttu-id="e59f6-108">[Capitolo 2](chapter2.md) : descrive i passaggi di base per installare e usare Azure RTO FILEX con l'applicazione Azure RTO threadX</span><span class="sxs-lookup"><span data-stu-id="e59f6-108">[Chapter 2](chapter2.md) - Gives the basic steps to install and use Azure RTOS FileX with your Azure RTOS ThreadX application</span></span>

<span data-ttu-id="e59f6-109">[Capitolo 3](chapter3.md) -Panoramica funzionale del sistema Azure RTO FILEX e informazioni di base sui formati FAT file System</span><span class="sxs-lookup"><span data-stu-id="e59f6-109">[Chapter 3](chapter3.md) - Provides a functional overview of the Azure RTOS FileX system and basic information about FAT file system formats</span></span>

<span data-ttu-id="e59f6-110">[Capitolo 4](chapter4.md) : informazioni dettagliate sull'interfaccia dell'applicazione per Azure RTO FILEX</span><span class="sxs-lookup"><span data-stu-id="e59f6-110">[Chapter 4](chapter4.md) - Details the application's interface to Azure RTOS FileX</span></span>

<span data-ttu-id="e59f6-111">[Capitolo 5](chapter5.md) -descrive il driver RAM FILEX di Azure RTO fornito e come scrivere i driver FILEX di Azure RTO personalizzati</span><span class="sxs-lookup"><span data-stu-id="e59f6-111">[Chapter 5](chapter5.md) - Describes the supplied Azure RTOS FileX RAM driver and how to write your own custom Azure RTOS FileX drivers</span></span>

<span data-ttu-id="e59f6-112">[Capitolo 6](chapter6.md) : descrive il modulo a tolleranza di errore FILEX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e59f6-112">[Chapter 6](chapter6.md) - Describes the Azure RTOS FileX Fault Tolerant Module</span></span>

<span data-ttu-id="e59f6-113">[Appendice A](appendix-a.md) -Servizi FILEX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e59f6-113">[Appendix A](appendix-a.md) - Azure RTOS FileX Services</span></span>

<span data-ttu-id="e59f6-114">[Appendice B](appendix-b.md) -costanti FILEX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e59f6-114">[Appendix B](appendix-b.md) - Azure RTOS FileX Constants</span></span>

<span data-ttu-id="e59f6-115">[Appendice C](appendix-c.md) -tipi di dati FILEX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e59f6-115">[Appendix C](appendix-c.md) - Azure RTOS FileX Data Types</span></span>

<span data-ttu-id="e59f6-116">[Appendice D](appendix-d.md) -grafico ASCII</span><span class="sxs-lookup"><span data-stu-id="e59f6-116">[Appendix D](appendix-d.md) - ASCII Chart</span></span>

## <a name="guide-conventions"></a><span data-ttu-id="e59f6-117">Convenzioni della Guida</span><span class="sxs-lookup"><span data-stu-id="e59f6-117">Guide Conventions</span></span>

<span data-ttu-id="e59f6-118">*Italics* : il carattere tipografico denota i titoli dei libri, enfatizza le parole importanti e indica le variabili.</span><span class="sxs-lookup"><span data-stu-id="e59f6-118">*Italics* - Typeface denotes book titles, emphasizes important words, and indicates variables.</span></span>

<span data-ttu-id="e59f6-119">**Grassetto** -Typeface indica i nomi di file, le parole chiave e enfatizza ulteriormente le parole e le variabili importanti.</span><span class="sxs-lookup"><span data-stu-id="e59f6-119">**Boldface** - Typeface denotes file names, key words, and further emphasizes important words and variables.</span></span>

> [!NOTE]
> <span data-ttu-id="e59f6-120">I simboli informativi attirano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulla funzione.</span><span class="sxs-lookup"><span data-stu-id="e59f6-120">Information symbols draw attention to important or additional information that could affect performance or function.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e59f6-121">I simboli di avviso attirano l'attenzione sulle situazioni che gli sviluppatori devono evitare perché potrebbero causare errori irreversibili.</span><span class="sxs-lookup"><span data-stu-id="e59f6-121">Warning symbols draw attention to situations that developers should avoid because they could cause fatal errors.</span></span>

## <a name="filex-data-types"></a><span data-ttu-id="e59f6-122">Tipi di dati FileX</span><span class="sxs-lookup"><span data-stu-id="e59f6-122">FileX Data Types</span></span>

<span data-ttu-id="e59f6-123">Oltre ai tipi di dati personalizzati della struttura di controllo FileX di Azure RTO, è disponibile una serie di tipi di dati speciali usati nelle interfacce di chiamata del servizio FileX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="e59f6-123">In addition to the custom Azure RTOS FileX control structure data types, there is a series of special data types that are used in Azure RTOS FileX service call interfaces.</span></span> <span data-ttu-id="e59f6-124">Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante.</span><span class="sxs-lookup"><span data-stu-id="e59f6-124">These special data types map directly to data types of the underlying C compiler.</span></span> <span data-ttu-id="e59f6-125">Questa operazione viene eseguita per garantire la portabilità tra diversi compilatori C.</span><span class="sxs-lookup"><span data-stu-id="e59f6-125">This is done to ensure portability between different C compilers.</span></span> <span data-ttu-id="e59f6-126">L'implementazione esatta viene ereditata da Azure RTO ThreadX ed è disponibile nel file tx_port. h incluso nella distribuzione ThreadX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="e59f6-126">The exact implementation is inherited from Azure RTOS ThreadX and can be found in the tx_port.h file included in the Azure RTOS ThreadX distribution.</span></span>

<span data-ttu-id="e59f6-127">Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio FileX di Azure RTO e dei relativi significati.</span><span class="sxs-lookup"><span data-stu-id="e59f6-127">The following is a list of Azure RTOS FileX service call data types and their associated meanings.</span></span>

| <span data-ttu-id="e59f6-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="e59f6-128">Type</span></span>  | <span data-ttu-id="e59f6-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e59f6-129">Description</span></span>  |
|---|---|
| <span data-ttu-id="e59f6-130">**UINT**</span><span class="sxs-lookup"><span data-stu-id="e59f6-130">**UINT**</span></span> | <span data-ttu-id="e59f6-131">Unsigned Integer di base.</span><span class="sxs-lookup"><span data-stu-id="e59f6-131">Basic unsigned integer.</span></span> <span data-ttu-id="e59f6-132">Questo tipo deve supportare i dati senza segno a 8 bit; viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico.</span><span class="sxs-lookup"><span data-stu-id="e59f6-132">This type must support 8-bit unsigned data; however, it is mapped to the most convenient unsigned data type.</span></span> |
| <span data-ttu-id="e59f6-133">**ULONG**</span><span class="sxs-lookup"><span data-stu-id="e59f6-133">**ULONG**</span></span> | <span data-ttu-id="e59f6-134">Tipo long senza segno.</span><span class="sxs-lookup"><span data-stu-id="e59f6-134">Unsigned long type.</span></span> <span data-ttu-id="e59f6-135">Questo tipo deve supportare i dati senza segno a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="e59f6-135">This type must support 32-bit unsigned data.</span></span> |
| <span data-ttu-id="e59f6-136">**VUOTO**</span><span class="sxs-lookup"><span data-stu-id="e59f6-136">**VOID**</span></span> | <span data-ttu-id="e59f6-137">Quasi sempre equivalente al tipo void del compilatore.</span><span class="sxs-lookup"><span data-stu-id="e59f6-137">Almost always equivalent to the compiler’s void type.</span></span> |
| <span data-ttu-id="e59f6-138">**CHAR**</span><span class="sxs-lookup"><span data-stu-id="e59f6-138">**CHAR**</span></span> | <span data-ttu-id="e59f6-139">Spesso un tipo di carattere standard a 8 bit.</span><span class="sxs-lookup"><span data-stu-id="e59f6-139">Most often a standard 8-bit character type.</span></span> |
| <span data-ttu-id="e59f6-140">**ULONG64**</span><span class="sxs-lookup"><span data-stu-id="e59f6-140">**ULONG64**</span></span> | <span data-ttu-id="e59f6-141">tipo di dati Unsigned Integer a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="e59f6-141">64-bit unsigned integer data type.</span></span> |

<span data-ttu-id="e59f6-142">I tipi di dati aggiuntivi vengono usati all'interno dell'origine FileX.</span><span class="sxs-lookup"><span data-stu-id="e59f6-142">Additional data types are used within the FileX source.</span></span> <span data-ttu-id="e59f6-143">Si trovano nei file \***tx_port. h** _ o _ \*_fx_port. h_\*\*.</span><span class="sxs-lookup"><span data-stu-id="e59f6-143">They are located in either the ***tx_port.h** _ or _ *_fx_port.h_** files.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="e59f6-144">Centro assistenza clienti</span><span class="sxs-lookup"><span data-stu-id="e59f6-144">Customer Support Center</span></span>

<span data-ttu-id="e59f6-145">Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="e59f6-145">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="e59f6-146">Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="e59f6-146">Please supply us with the following information in an email message so we can more efficiently resolve your support request.</span></span>

1. <span data-ttu-id="e59f6-147">Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="e59f6-147">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="e59f6-148">Descrizione dettagliata delle modifiche apportate all'applicazione e/o FileX che hanno preceduto il problema.</span><span class="sxs-lookup"><span data-stu-id="e59f6-148">A detailed description of any changes to the application and/or FileX that preceded the problem.</span></span>
3. <span data-ttu-id="e59f6-149">Il contenuto delle stringhe _tx_version_id e _fx_version_id trovate nei file \***tx_port. h**_ e _ *_fx_port. h_*\* della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e59f6-149">The contents of the _tx_version_id and _fx_version_id strings found in the \***tx_port.h**_ and _ *_fx_port.h_*\* files of your distribution.</span></span> <span data-ttu-id="e59f6-150">Queste stringhe forniranno informazioni preziose sull'ambiente di run-time.</span><span class="sxs-lookup"><span data-stu-id="e59f6-150">These strings will provide us valuable information regarding your run-time environment.</span></span>
4. <span data-ttu-id="e59f6-151">Contenuto della RAM delle variabili **ULONG** seguenti.</span><span class="sxs-lookup"><span data-stu-id="e59f6-151">The contents in RAM of the following **ULONG** variables.</span></span> <span data-ttu-id="e59f6-152">Queste variabili forniranno informazioni sulla modalità di compilazione delle librerie ThreadX e FileX:</span><span class="sxs-lookup"><span data-stu-id="e59f6-152">These variables will give us information on how your ThreadX and FileX libraries were built:</span></span>

    <span data-ttu-id="e59f6-153">**_tx_build_options**</span><span class="sxs-lookup"><span data-stu-id="e59f6-153">**_tx_build_options**</span></span>

    <span data-ttu-id="e59f6-154">**_fx_system_build_options1**</span><span class="sxs-lookup"><span data-stu-id="e59f6-154">**_fx_system_build_options1**</span></span>

    <span data-ttu-id="e59f6-155">**_fx_system_build_options2**</span><span class="sxs-lookup"><span data-stu-id="e59f6-155">**_fx_system_build_options2**</span></span>

    <span data-ttu-id="e59f6-156">**_fx_system_build_options3**</span><span class="sxs-lookup"><span data-stu-id="e59f6-156">**_fx_system_build_options3**</span></span>
