---
title: Manuale dell'utente dello stack di dispositivi USBX di Azure RTO
description: In questa guida vengono fornite informazioni complete su Azure RTO USBX, il software USB Foundation a prestazioni elevate di Microsoft
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: c8e9360c8b72adbc41f840a48e333668c489399e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821332"
---
# <a name="azure-rtos-usbx-device-stack-user-guide"></a><span data-ttu-id="91586-103">Manuale dell'utente dello stack di dispositivi USBX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="91586-103">Azure RTOS USBX Device Stack User Guide</span></span>

<span data-ttu-id="91586-104">In questa guida vengono fornite informazioni complete su Azure RTO USBX, il software USB Foundation a prestazioni elevate di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="91586-104">This guide provides comprehensive information about Azure RTOS USBX, the high performance USB foundation software from Microsoft.</span></span>

<span data-ttu-id="91586-105">È progettato per lo sviluppatore di software in tempo reale incorporato.</span><span class="sxs-lookup"><span data-stu-id="91586-105">It is intended for the embedded real-time software developer.</span></span> <span data-ttu-id="91586-106">Lo sviluppatore deve avere familiarità con le funzioni standard del sistema operativo in tempo reale, le specifiche USB e il linguaggio di programmazione C.</span><span class="sxs-lookup"><span data-stu-id="91586-106">The developer should be familiar with standard real-time operating system functions, the USB specification, and the C programming language.</span></span>

<span data-ttu-id="91586-107">Per informazioni tecniche relative a USB, vedere la specifica USB e le specifiche della classe USB che è possibile scaricare all'indirizzo https://www.USB.org/developers</span><span class="sxs-lookup"><span data-stu-id="91586-107">For technical information related to USB, see the USB specification and USB Class specifications that can be downloaded at https://www.USB.org/developers</span></span>

## <a name="organization"></a><span data-ttu-id="91586-108">Organization</span><span class="sxs-lookup"><span data-stu-id="91586-108">Organization</span></span>

- <span data-ttu-id="91586-109">[**Capitolo 1**](usbx-device-stack-1.md) -contiene un'introduzione ad Azure RTO USBX</span><span class="sxs-lookup"><span data-stu-id="91586-109">[**Chapter 1**](usbx-device-stack-1.md) - contains an introduction to Azure RTOS USBX</span></span>

- <span data-ttu-id="91586-110">[**Capitolo 2**](usbx-device-stack-2.md) : fornisce i passaggi di base per installare e usare Azure RTO USBX con l'applicazione threadX</span><span class="sxs-lookup"><span data-stu-id="91586-110">[**Chapter 2**](usbx-device-stack-2.md) - gives the basic steps to install and use Azure RTOS USBX with your ThreadX application</span></span>

- <span data-ttu-id="91586-111">[**Capitolo 3**](usbx-device-stack-3.md) : descrive i componenti funzionali dello stack di dispositivi USBX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="91586-111">[**Chapter 3**](usbx-device-stack-3.md) - describes the functional components of the Azure RTOS USBX device stack</span></span>

- <span data-ttu-id="91586-112">[**Capitolo 4**](usbx-device-stack-4.md) : descrive i servizi dello stack di dispositivi USBX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="91586-112">[**Chapter 4**](usbx-device-stack-4.md) - describes the Azure RTOS USBX device stack services</span></span>

- <span data-ttu-id="91586-113">[**Capitolo 5**](usbx-device-stack-5.md) : descrive ogni classe di dispositivi USBX di Azure RTO, incluse le relative API</span><span class="sxs-lookup"><span data-stu-id="91586-113">[**Chapter 5**](usbx-device-stack-5.md) - describes each Azure RTOS USBX device class including their APIs</span></span>

## <a name="customer-support-center"></a><span data-ttu-id="91586-114">Centro assistenza clienti</span><span class="sxs-lookup"><span data-stu-id="91586-114">Customer Support Center</span></span>

<span data-ttu-id="91586-115">Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="91586-115">Please submit a support ticket through the Azure Portal for questions or help using the steps here.</span></span> <span data-ttu-id="91586-116">Fornire le informazioni seguenti in un messaggio di posta elettronica per poter risolvere in modo più efficiente la richiesta di supporto:</span><span class="sxs-lookup"><span data-stu-id="91586-116">Please supply us with the following information in an email message so we can more efficiently resolve your support request:</span></span>

1. <span data-ttu-id="91586-117">Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e se può essere riprodotta in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="91586-117">A detailed description of the problem, including frequency of occurrence and whether it can be reliably reproduced.</span></span>
2. <span data-ttu-id="91586-118">Descrizione dettagliata delle modifiche apportate all'applicazione e/o ThreadX RTO di Azure che hanno preceduto il problema.</span><span class="sxs-lookup"><span data-stu-id="91586-118">A detailed description of any changes to the application and/or Azure RTOS ThreadX that preceded the problem.</span></span>
3. <span data-ttu-id="91586-119">Contenuto della stringa di **_tx_version_id** trovata nel file **_tx_port. h_** della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="91586-119">The contents of the **_tx_version_id** string found in the **_tx_port.h_** file of your distribution.</span></span> <span data-ttu-id="91586-120">Questa stringa fornirà informazioni preziose sull'ambiente di run-time.</span><span class="sxs-lookup"><span data-stu-id="91586-120">This string will provide us valuable information regarding your run-time environment.</span></span>
4. <span data-ttu-id="91586-121">Contenuto della RAM della variabile *_tx_build_options* **ULONG** .</span><span class="sxs-lookup"><span data-stu-id="91586-121">The contents in RAM of the *_tx_build_options* **ULONG** variable.</span></span> <span data-ttu-id="91586-122">Questa variabile fornirà informazioni su come è stata creata la libreria ThreadX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="91586-122">This variable will give us information on how your Azure RTOS ThreadX library was built.</span></span>
