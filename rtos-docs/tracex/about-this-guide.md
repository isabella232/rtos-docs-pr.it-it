---
title: Guida dell'utente di Azure RTO TraceX
description: Questa guida contiene informazioni complete su Azure RTO TraceX, lo strumento di analisi del sistema basato su Microsoft Windows di Microsoft.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 92d886b19a0c67292cd4f6a5f8bd7f9d3106374b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823774"
---
# <a name="about-this-guide"></a><span data-ttu-id="a8f7a-103">Informazioni sulla guida</span><span class="sxs-lookup"><span data-stu-id="a8f7a-103">About this guide</span></span>

<span data-ttu-id="a8f7a-104">Questa guida contiene informazioni complete su Azure RTO TraceX, lo strumento di analisi del sistema basato su Microsoft Windows per Microsoft Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-104">This guide contains comprehensive information about Azure RTOS TraceX, the Microsoft Windows-based system analysis tool for Microsoft Azure RTOS.</span></span>

<span data-ttu-id="a8f7a-105">È destinato agli sviluppatori di software embedded in tempo reale che usano Azure RTO ThreadX Real-Time sistema operativo (RTO) e componenti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-105">It is intended for the embedded real-time software developer using Azure RTOS ThreadX Real-Time Operating System (RTOS) and add-on components.</span></span> <span data-ttu-id="a8f7a-106">Lo sviluppatore deve avere familiarità con i concetti standard di Azure RTO ThreadX Azure RTO FileX e Azure RTO NetX.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-106">The developer should be familiar with standard Azure RTOS ThreadX Azure RTOS FileX, and Azure RTOS NetX concepts.</span></span>

## <a name="organization"></a><span data-ttu-id="a8f7a-107">Organization</span><span class="sxs-lookup"><span data-stu-id="a8f7a-107">Organization</span></span>

- <span data-ttu-id="a8f7a-108">[Capitolo 1](chapter1.md) : contiene una panoramica di base di Azure RTO TraceX e ne descrive la relazione con lo sviluppo in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-108">[Chapter 1](chapter1.md) - contains an basic overview of Azure RTOS TraceX and describes its relationship to real-time development.</span></span>
- <span data-ttu-id="a8f7a-109">[Capitolo 2](chapter2.md) : fornisce i passaggi di base per installare e usare Azure RTO TraceX per analizzare immediatamente l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-109">[Chapter 2](chapter2.md) - gives the basic steps to install and use Azure RTOS TraceX to analyze your application right out of the box.</span></span>
- <span data-ttu-id="a8f7a-110">[Capitolo 3](chapter3.md) : descrive le funzionalità principali di Azure RTO TraceX.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-110">[Chapter 3](chapter3.md) - describes the main features of Azure RTOS TraceX.</span></span>
- <span data-ttu-id="a8f7a-111">[Capitolo 4](chapter4.md) : dettagli delle funzionalità di analisi delle prestazioni di Azure RTO TraceX.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-111">[Chapter 4](chapter4.md) - details performance analysis features of Azure RTOS TraceX.</span></span>
- <span data-ttu-id="a8f7a-112">[Capitolo 5](chapter5.md) : descrive come configurare Azure RTO threadX, Azure RTO FILEX e Azure RTO NETX per generare un buffer di traccia visualizzabile da Azure RTO TraceX.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-112">[Chapter 5](chapter5.md) - describes how to set up Azure RTOS ThreadX, Azure RTOS FileX, and Azure RTOS NetX in order to generate a trace buffer that is viewable by Azure RTOS TraceX.</span></span>
- <span data-ttu-id="a8f7a-113">[Capitolo 6](chapter6.md) : descrive in modo dettagliato gli eventi TraceX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-113">[Chapter 6](chapter6.md) - describes Azure RTOS TraceX events in detail.</span></span>
- <span data-ttu-id="a8f7a-114">[Capitolo 7](chapter7.md) : descrive in modo dettagliato gli eventi FILEX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-114">[Chapter 7](chapter7.md) - describes Azure RTOS FileX events in detail.</span></span>
- <span data-ttu-id="a8f7a-115">[Capitolo 8](chapter8.md) : descrive in modo dettagliato gli eventi NETX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-115">[Chapter 8](chapter8.md) - describes Azure RTOS NetX events in detail.</span></span>
- <span data-ttu-id="a8f7a-116">[Capitolo 9](chapter9.md) : descrive in modo dettagliato gli eventi USBX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-116">[Chapter 9](chapter9.md) - describes Azure RTOS USBX events in detail.</span></span>
- <span data-ttu-id="a8f7a-117">[Capitolo 10](chapter10.md) : descrive in modo dettagliato la creazione di eventi utente personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-117">[Chapter 10](chapter10.md) - describes creating custom user events in detail.</span></span>
- <span data-ttu-id="a8f7a-118">[Capitolo 11](chapter11.md) -Descrizione dettagliata del buffer di traccia interno.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-118">[Chapter 11](chapter11.md) - describes the internal trace buffer in detail.</span></span>
- <span data-ttu-id="a8f7a-119">[Appendice a](appendix-a.md) -file specifico della porta di Azure RTO threadX con l'origine timestamp per la raccolta di eventi di traccia.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-119">[Appendix A](appendix-a.md) - Azure RTOS ThreadX port-specific file with its time-stamp source for gathering trace events.</span></span>
- <span data-ttu-id="a8f7a-120">[Appendice B](appendix-b.md) -Azure rto threadX *tx_trace file con estensione h* che mostra i dettagli di implementazione relativi al buffer di traccia eventi.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-120">[Appendix B](appendix-b.md) - Azure RTOS ThreadX *tx_trace.h* file that shows implementation details regarding the event trace buffer.</span></span>
- <span data-ttu-id="a8f7a-121">[Appendice C](appendix-c.md) -riepiloga le utilità della riga di comando per la conversione di diversi formati di file in file binari TraceX RTO di Azure appropriati.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-121">[Appendix C](appendix-c.md) - Summarizes command line utilities for converting various file formats into proper Azure RTOS TraceX binary files.</span></span>
- <span data-ttu-id="a8f7a-122">[Appendice D](appendix-d.md) -esempi di dump dei file di traccia da diversi strumenti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-122">[Appendix D](appendix-d.md) - Examples of dumping trace files from various development tools.</span></span>

## <a name="guide-conventions"></a><span data-ttu-id="a8f7a-123">Convenzioni della Guida</span><span class="sxs-lookup"><span data-stu-id="a8f7a-123">Guide Conventions</span></span>

<span data-ttu-id="a8f7a-124">*Italics* : il carattere tipografico denota i titoli dei libri, enfatizza le parole importanti e indica le variabili.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-124">*Italics* - Typeface denotes book titles, emphasizes important words, and indicates variables.</span></span>

<span data-ttu-id="a8f7a-125">**Grassetto** -Typeface indica i nomi di file, le parole chiave e enfatizza ulteriormente le parole e le variabili importanti.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-125">**Boldface** - Typeface denotes file names, key words, and further emphasizes important words and variables.</span></span>

> [!NOTE]
> <span data-ttu-id="a8f7a-126">Indica le informazioni di nota.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-126">Indicates information of note.</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="a8f7a-127">Centro assistenza clienti</span><span class="sxs-lookup"><span data-stu-id="a8f7a-127">Customer Support Center</span></span>

<span data-ttu-id="a8f7a-128">Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-128">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="a8f7a-129">Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:</span><span class="sxs-lookup"><span data-stu-id="a8f7a-129">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="a8f7a-130">Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-130">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="a8f7a-131">Descrizione dettagliata delle modifiche apportate all'applicazione e/o ThreadX RTO di Azure che hanno preceduto il problema.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-131">A detailed description of any changes to the application and/or Azure RTOS ThreadX that preceded the problem.</span></span>
3. <span data-ttu-id="a8f7a-132">Contenuto della stringa di *_tx_version_id* trovata nel file *tx_port. h* della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-132">The contents of the *_tx_version_id* string found in the *tx_port.h* file of your distribution.</span></span> <span data-ttu-id="a8f7a-133">Questa stringa fornirà informazioni preziose sull'ambiente di run-time.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-133">This string will provide us valuable information regarding your run-time environment.</span></span>
4. <span data-ttu-id="a8f7a-134">Contenuto della RAM della variabile *_tx_build_options* ULONG.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-134">The contents in RAM of the *_tx_build_options* ULONG variable.</span></span> <span data-ttu-id="a8f7a-135">Questa variabile fornirà informazioni su come è stata creata la libreria ThreadX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="a8f7a-135">This variable will give us information on how your Azure RTOS ThreadX library was built.</span></span>
