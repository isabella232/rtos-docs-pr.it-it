---
title: Guida dell'utente dello stack host di Azure RTO USBX
description: In questa guida vengono fornite informazioni complete su Azure RTO USBX, il software USB Foundation a prestazioni elevate di Microsoft.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 243b12c4757ee945def8fea01c0d4114e39312ce
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823234"
---
# <a name="azure-rtos-usbx-host-stack-user-guide"></a><span data-ttu-id="c8dc3-103">Guida dell'utente dello stack host di Azure RTO USBX</span><span class="sxs-lookup"><span data-stu-id="c8dc3-103">Azure RTOS USBX Host Stack User Guide</span></span>

<span data-ttu-id="c8dc3-104">In questa guida vengono fornite informazioni complete su Azure RTO USBX, il software USB Foundation a prestazioni elevate di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-104">This guide provides comprehensive information about Azure RTOS USBX, the high-performance USB foundation software from Microsoft.</span></span>

<span data-ttu-id="c8dc3-105">È progettato per lo sviluppatore di software in tempo reale incorporato.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-105">It is intended for the embedded real-time software developer.</span></span> <span data-ttu-id="c8dc3-106">Lo sviluppatore deve avere familiarità con le funzioni standard del sistema operativo in tempo reale, le specifiche USB e il linguaggio di programmazione C.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-106">The developer should be familiar with standard real-time operating system functions, the USB specification, and the C programming language.</span></span>

<span data-ttu-id="c8dc3-107">Per informazioni tecniche relative a USB, vedere la specifica USB e le specifiche della classe USB che è possibile scaricare all'indirizzo [https://www.USB.org/developers](https://www.USB.org/developers)</span><span class="sxs-lookup"><span data-stu-id="c8dc3-107">For technical information related to USB, see the USB specification and USB Class specifications that can be downloaded at [https://www.USB.org/developers](https://www.USB.org/developers)</span></span>

## <a name="organization"></a><span data-ttu-id="c8dc3-108">Organization</span><span class="sxs-lookup"><span data-stu-id="c8dc3-108">Organization</span></span>

- <span data-ttu-id="c8dc3-109">[**Capitolo 1**](usbx-host-stack-1.md) -contiene un'introduzione ad Azure RTO USBX</span><span class="sxs-lookup"><span data-stu-id="c8dc3-109">[**Chapter 1**](usbx-host-stack-1.md) - contains an introduction to Azure RTOS USBX</span></span>

- <span data-ttu-id="c8dc3-110">[**Capitolo 2**](usbx-host-stack-2.md) : descrive i passaggi di base per installare e usare Azure RTO USBX con l'applicazione Azure RTO threadX</span><span class="sxs-lookup"><span data-stu-id="c8dc3-110">[**Chapter 2**](usbx-host-stack-2.md) - gives the basic steps to install and use Azure RTOS USBX with your Azure RTOS ThreadX application</span></span>

- <span data-ttu-id="c8dc3-111">[**Capitolo 3**](usbx-host-stack-3.md) -Panoramica funzionale di Azure RTO USBX e informazioni di base su USB</span><span class="sxs-lookup"><span data-stu-id="c8dc3-111">[**Chapter 3**](usbx-host-stack-3.md) - provides a functional overview of Azure RTOS USBX and basic information about USB</span></span>

- <span data-ttu-id="c8dc3-112">[**Capitolo 4**](usbx-host-stack-4.md) : informazioni dettagliate sull'interfaccia dell'applicazione per Azure RTO USBX in modalità host</span><span class="sxs-lookup"><span data-stu-id="c8dc3-112">[**Chapter 4**](usbx-host-stack-4.md) - details the application's interface to Azure RTOS USBX in host mode</span></span>

- <span data-ttu-id="c8dc3-113">[**Capitolo 5**](usbx-host-stack-5.md) -descrive le API delle classi host USBX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="c8dc3-113">[**Chapter 5**](usbx-host-stack-5.md) - describes the APIs of the Azure RTOS USBX Host classes</span></span>

- <span data-ttu-id="c8dc3-114">[**Capitolo 6**](usbx-host-stack-6.md) -Descrizione della classe CDC-ECM USBX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="c8dc3-114">[**Chapter 6**](usbx-host-stack-6.md) - describes the Azure RTOS USBX CDC-ECM class</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="c8dc3-115">Centro assistenza clienti</span><span class="sxs-lookup"><span data-stu-id="c8dc3-115">Customer Support Center</span></span>

<span data-ttu-id="c8dc3-116">Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-116">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="c8dc3-117">Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-117">Please supply us with the following information in an email message so we can more efficiently resolve your support request.</span></span>

1. <span data-ttu-id="c8dc3-118">Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-118">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="c8dc3-119">Descrizione dettagliata delle modifiche apportate all'applicazione e/o ThreadX RTO di Azure che hanno preceduto il problema.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-119">A detailed description of any changes to the application and/or Azure RTOS ThreadX that preceded the problem.</span></span>
3. <span data-ttu-id="c8dc3-120">Contenuto della stringa di *_tx_version_id* trovata nel file *tx_port. h* della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-120">The contents of the *_tx_version_id* string found in the *tx_port.h* file of your distribution.</span></span> <span data-ttu-id="c8dc3-121">Questa stringa fornirà informazioni preziose sull'ambiente di run-time.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-121">This string will provide us valuable information regarding your run-time environment.</span></span>
4. <span data-ttu-id="c8dc3-122">Contenuto della RAM della variabile *_tx_build_options* ULONG.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-122">The contents in RAM of the *_tx_build_options* ULONG variable.</span></span> <span data-ttu-id="c8dc3-123">Questa variabile fornirà informazioni su come è stata creata la libreria ThreadX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-123">This variable will give us information on how your Azure RTOS ThreadX library was built.</span></span>
