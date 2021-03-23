---
title: Informazioni sulla guida di Azure RTO ThreadX
description: Questa guida fornisce informazioni complete su Azure RTO ThreadX, il kernel in tempo reale a prestazioni elevate Microsoft.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ad9f782942bcdbb2dc49a9c841d865d97bcb1d4e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822496"
---
# <a name="about-the-azure-rtos-threadx-guide"></a><span data-ttu-id="e0724-103">Informazioni sulla guida di Azure RTO ThreadX</span><span class="sxs-lookup"><span data-stu-id="e0724-103">About the Azure RTOS ThreadX Guide</span></span>

<span data-ttu-id="e0724-104">Questa guida fornisce informazioni complete su Azure RTO ThreadX, il kernel in tempo reale a prestazioni elevate Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e0724-104">This guide provides comprehensive information about Azure RTOS ThreadX, the Microsoft high-performance real-time kernel.</span></span> 

<span data-ttu-id="e0724-105">È progettato per lo sviluppatore di software in tempo reale incorporato.</span><span class="sxs-lookup"><span data-stu-id="e0724-105">It is intended for the embedded real-time software developer.</span></span> <span data-ttu-id="e0724-106">Lo sviluppatore deve avere familiarità con le funzioni standard del sistema operativo in tempo reale e il linguaggio di programmazione C.</span><span class="sxs-lookup"><span data-stu-id="e0724-106">The developer should be familiar with standard real-time operating system functions and the C programming language.</span></span>

## <a name="organization"></a><span data-ttu-id="e0724-107">Organization</span><span class="sxs-lookup"><span data-stu-id="e0724-107">Organization</span></span>

<span data-ttu-id="e0724-108">[Capitolo 1](chapter1.md) : viene fornita una panoramica di base di Azure RTO threadX e della relativa relazione con lo sviluppo incorporato in tempo reale</span><span class="sxs-lookup"><span data-stu-id="e0724-108">[Chapter 1](chapter1.md) - Provides a basic overview of Azure RTOS ThreadX and its relationship to real-time embedded development</span></span>

<span data-ttu-id="e0724-109">[Capitolo 2](chapter2.md) : fornisce i *passaggi di base* per installare e usare Azure RTO threadX nell'applicazione immediatamente</span><span class="sxs-lookup"><span data-stu-id="e0724-109">[Chapter 2](chapter2.md) - Gives the basic steps to install and use Azure RTOS ThreadX in your application right *out of the box*</span></span>

<span data-ttu-id="e0724-110">[Capitolo 3](chapter3.md) : descrive in dettaglio il funzionamento funzionale di Azure RTO threadX, il kernel in tempo reale a prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="e0724-110">[Chapter 3](chapter3.md) - Describes in detail the functional operation of Azure RTOS ThreadX, the high performance real-time kernel</span></span>

<span data-ttu-id="e0724-111">[Capitolo 4](chapter4.md) : informazioni dettagliate sull'interfaccia dell'applicazione per Azure RTO threadX</span><span class="sxs-lookup"><span data-stu-id="e0724-111">[Chapter 4](chapter4.md) - Details the application's interface to Azure RTOS ThreadX</span></span>

<span data-ttu-id="e0724-112">[Capitolo 5](chapter5.md) -Descrizione della scrittura di driver i/O per le applicazioni threadX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e0724-112">[Chapter 5](chapter5.md) - Describes writing I/O drivers for Azure RTOS ThreadX applications</span></span>

<span data-ttu-id="e0724-113">[Capitolo 6](chapter6.md) : descrive l'applicazione dimostrativa fornita con ogni pacchetto per il supporto del processore threadX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e0724-113">[Chapter 6](chapter6.md) - Describes the demonstration application that is supplied with every Azure RTOS ThreadX processor support package</span></span>

<span data-ttu-id="e0724-114">[Appendice A](appendix-a.md) -API threadX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e0724-114">[Appendix A](appendix-a.md) - Azure RTOS ThreadX API</span></span>

<span data-ttu-id="e0724-115">[Appendice B](appendix-b.md) -costanti threadX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e0724-115">[Appendix B](appendix-b.md) - Azure RTOS ThreadX constants</span></span>

<span data-ttu-id="e0724-116">[Appendice C](appendix-c.md) -tipi di dati threadX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e0724-116">[Appendix C](appendix-c.md) - Azure RTOS ThreadX data types</span></span>

<span data-ttu-id="e0724-117">[Appendice D](appendix-d.md) -grafico ASCII</span><span class="sxs-lookup"><span data-stu-id="e0724-117">[Appendix D](appendix-d.md) - ASCII chart</span></span>

## <a name="guide-conventions"></a><span data-ttu-id="e0724-118">Convenzioni della Guida</span><span class="sxs-lookup"><span data-stu-id="e0724-118">Guide Conventions</span></span>

<span data-ttu-id="e0724-119">*Corsivo* : il carattere tipografico denota i titoli dei libri, enfatizza le parole importanti e indica i parametri.</span><span class="sxs-lookup"><span data-stu-id="e0724-119">*Italics* - typeface denotes book titles, emphasizes important words, and indicates parameters.</span></span>

<span data-ttu-id="e0724-120">**Grassetto** -Typeface indica parole chiave, costanti, nomi di tipi, elementi dell'interfaccia utente, nomi di variabili e enfatizza ulteriormente le parole importanti.</span><span class="sxs-lookup"><span data-stu-id="e0724-120">**Boldface** - typeface denotes key words, constants, type names, user interface elements, variable names, and further emphasizes important words.</span></span>

<span data-ttu-id="e0724-121">***Italics e grassetto*** -Typeface denota i nomi di file e di funzione.</span><span class="sxs-lookup"><span data-stu-id="e0724-121">***Italics and Boldface*** - typeface denotes file names and function names.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0724-122">I simboli informativi attirano l'attenzione su informazioni importanti o aggiuntive che potrebbero influire sulle prestazioni o sulla funzione.</span><span class="sxs-lookup"><span data-stu-id="e0724-122">Information symbols draw attention to important or additional information that could affect performance or function.</span></span>

> [!WARNING]
> <span data-ttu-id="e0724-123">I simboli di avviso attirano l'attenzione sulle situazioni in cui gli sviluppatori devono essere attenti a evitare perché potrebbero causare errori irreversibili.</span><span class="sxs-lookup"><span data-stu-id="e0724-123">Warning symbols draw attention to situations in which developers should take care to avoid because they could cause fatal errors.</span></span>

## <a name="azure-rtos-threadx-data-types"></a><span data-ttu-id="e0724-124">Tipi di dati ThreadX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="e0724-124">Azure RTOS ThreadX Data Types</span></span>

<span data-ttu-id="e0724-125">Oltre ai tipi di dati personalizzati della struttura di controllo ThreadX di Azure RTO, è disponibile una serie di tipi di dati speciali usati nelle interfacce di chiamata del servizio ThreadX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="e0724-125">In addition to the custom Azure RTOS ThreadX control structure data types, there are a series of special data types that are used in Azure RTOS ThreadX service call interfaces.</span></span> <span data-ttu-id="e0724-126">Questi tipi di dati speciali vengono mappati direttamente ai tipi di dati del compilatore C sottostante.</span><span class="sxs-lookup"><span data-stu-id="e0724-126">These special data types map directly to data types of the underlying C compiler.</span></span> <span data-ttu-id="e0724-127">Questa operazione viene eseguita per assicurare la portabilità tra diversi compilatori C.</span><span class="sxs-lookup"><span data-stu-id="e0724-127">This is done to insure portability between different C compilers.</span></span> <span data-ttu-id="e0724-128">L'implementazione esatta si trova nel file ***tx_port. h*** incluso nell'origine.</span><span class="sxs-lookup"><span data-stu-id="e0724-128">The exact implementation can be found in the ***tx_port.h*** file included with the source.</span></span>

<span data-ttu-id="e0724-129">Di seguito è riportato un elenco dei tipi di dati delle chiamate al servizio ThreadX di Azure RTO e dei relativi significati:</span><span class="sxs-lookup"><span data-stu-id="e0724-129">The following is a list of Azure RTOS ThreadX service call data types and their associated meanings:</span></span>

| <span data-ttu-id="e0724-130">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="e0724-130">Data type</span></span>  | <span data-ttu-id="e0724-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e0724-131">Description</span></span> |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| <span data-ttu-id="e0724-132">**UINT**</span><span class="sxs-lookup"><span data-stu-id="e0724-132">**UINT**</span></span> | <span data-ttu-id="e0724-133">Unsigned Integer di base.</span><span class="sxs-lookup"><span data-stu-id="e0724-133">Basic unsigned integer.</span></span> <span data-ttu-id="e0724-134">Questo tipo deve supportare i dati senza segno a 8 bit; viene tuttavia eseguito il mapping al tipo di dati senza segno più pratico.</span><span class="sxs-lookup"><span data-stu-id="e0724-134">This type must support 8-bit unsigned data; however, it is mapped to the most convenient unsigned data type.</span></span> |
| <span data-ttu-id="e0724-135">**ULONG**</span><span class="sxs-lookup"><span data-stu-id="e0724-135">**ULONG**</span></span> | <span data-ttu-id="e0724-136">Tipo long senza segno.</span><span class="sxs-lookup"><span data-stu-id="e0724-136">Unsigned long type.</span></span> <span data-ttu-id="e0724-137">Questo tipo deve supportare i dati senza segno a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="e0724-137">This type must support 32-bit unsigned data.</span></span> |
| <span data-ttu-id="e0724-138">**VUOTO**</span><span class="sxs-lookup"><span data-stu-id="e0724-138">**VOID**</span></span> | <span data-ttu-id="e0724-139">Quasi sempre equivalente al tipo void del compilatore.</span><span class="sxs-lookup"><span data-stu-id="e0724-139">Almost always equivalent to the compiler's void type.</span></span> |
| <span data-ttu-id="e0724-140">**CHAR**</span><span class="sxs-lookup"><span data-stu-id="e0724-140">**CHAR**</span></span> | <span data-ttu-id="e0724-141">Spesso un tipo di carattere standard a 8 bit.</span><span class="sxs-lookup"><span data-stu-id="e0724-141">Most often a standard 8-bit character type.</span></span> |
|  |  |

<span data-ttu-id="e0724-142">I tipi di dati aggiuntivi vengono usati all'interno dell'origine ThreadX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="e0724-142">Additional data types are used within the Azure RTOS ThreadX source.</span></span> <span data-ttu-id="e0724-143">Si trovano anche nel file ***tx_port. h*** .</span><span class="sxs-lookup"><span data-stu-id="e0724-143">They are also located in the ***tx_port.h*** file.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="e0724-144">Centro assistenza clienti</span><span class="sxs-lookup"><span data-stu-id="e0724-144">Customer Support Center</span></span>

<span data-ttu-id="e0724-145">Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="e0724-145">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="e0724-146">Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:</span><span class="sxs-lookup"><span data-stu-id="e0724-146">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="e0724-147">Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="e0724-147">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="e0724-148">Descrizione dettagliata delle modifiche apportate all'applicazione e/o ThreadX RTO di Azure che hanno preceduto il problema.</span><span class="sxs-lookup"><span data-stu-id="e0724-148">A detailed description of any changes to the application and/or Azure RTOS ThreadX that preceded the problem.</span></span>
3. <span data-ttu-id="e0724-149">Contenuto della stringa di *_tx_version_id* trovata nel file *tx_port. h* della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e0724-149">The contents of the *_tx_version_id* string found in the *tx_port.h* file of your distribution.</span></span> <span data-ttu-id="e0724-150">Questa stringa fornirà informazioni preziose sull'ambiente di run-time.</span><span class="sxs-lookup"><span data-stu-id="e0724-150">This string will provide us valuable information regarding your run-time environment.</span></span>
4. <span data-ttu-id="e0724-151">Contenuto della RAM della variabile **_tx_build_options** **ULONG** .</span><span class="sxs-lookup"><span data-stu-id="e0724-151">The contents in RAM of the **_tx_build_options** **ULONG** variable.</span></span> <span data-ttu-id="e0724-152">Questa variabile fornirà informazioni su come è stata creata la libreria ThreadX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="e0724-152">This variable will give us information on how your Azure RTOS ThreadX library was built.</span></span>
