---
title: Capitolo 1-Introduzione ad Azure RTO USBX Device stack
description: USBX è uno stack USB completo per applicazioni con Deep embedded. Questo capitolo introduce USBX, che descrive i vantaggi e le applicazioni.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 8b1e08130d4531fd82629378761cd5b1752f0a07
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550287"
---
# <a name="chapter-1---introduction-to-azure-rtos-usbx-device-stack"></a><span data-ttu-id="5a46d-104">Capitolo 1-Introduzione ad Azure RTO USBX Device stack</span><span class="sxs-lookup"><span data-stu-id="5a46d-104">Chapter 1 - Introduction to Azure RTOS USBX Device Stack</span></span>

<span data-ttu-id="5a46d-105">USBX è uno stack USB completo per applicazioni con Deep embedded.</span><span class="sxs-lookup"><span data-stu-id="5a46d-105">USBX is a full-featured USB stack for deeply embedded applications.</span></span> <span data-ttu-id="5a46d-106">Questo capitolo introduce USBX, che descrive le applicazioni e i vantaggi</span><span class="sxs-lookup"><span data-stu-id="5a46d-106">This chapter introduces USBX, describing its applications and benefits</span></span> 

## <a name="usbx-features"></a><span data-ttu-id="5a46d-107">Funzionalità di USBX</span><span class="sxs-lookup"><span data-stu-id="5a46d-107">USBX features</span></span>

<span data-ttu-id="5a46d-108">USBX supporta le tre specifiche USB esistenti: 1,1, 2,0 e OTG.</span><span class="sxs-lookup"><span data-stu-id="5a46d-108">USBX supports the three existing USB specifications: 1.1, 2.0 and OTG.</span></span> <span data-ttu-id="5a46d-109">È progettato per essere scalabile e può includere semplici topologie USB con un solo dispositivo connesso, oltre a topologie complesse con più dispositivi e hub a cascata.</span><span class="sxs-lookup"><span data-stu-id="5a46d-109">It is designed to be scalable and will accommodate simple USB topologies with only one connected device as well as complex topologies with multiple devices and cascading hubs.</span></span> <span data-ttu-id="5a46d-110">USBX supporta tutti i tipi di trasferimento dati dei protocolli USB: controllo, bulk, interrupt e isocrono.</span><span class="sxs-lookup"><span data-stu-id="5a46d-110">USBX supports all the data transfer types of the USB protocols: control, bulk, interrupt, and isochronous.</span></span>

<span data-ttu-id="5a46d-111">USBX supporta sia il lato host che il lato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5a46d-111">USBX supports both the host side and the device side.</span></span> <span data-ttu-id="5a46d-112">Ogni lato è costituito da tre livelli.</span><span class="sxs-lookup"><span data-stu-id="5a46d-112">Each side is composed of three layers.</span></span>

- <span data-ttu-id="5a46d-113">Livello controller</span><span class="sxs-lookup"><span data-stu-id="5a46d-113">Controller layer</span></span>
- <span data-ttu-id="5a46d-114">Livello stack</span><span class="sxs-lookup"><span data-stu-id="5a46d-114">Stack layer</span></span>
- <span data-ttu-id="5a46d-115">Livello classe</span><span class="sxs-lookup"><span data-stu-id="5a46d-115">Class layer</span></span>

<span data-ttu-id="5a46d-116">La relazione tra i livelli USB è la seguente:</span><span class="sxs-lookup"><span data-stu-id="5a46d-116">The relationship between the USB layers is as follows:</span></span>

![Livelli USB](media/usbx-device-stack/usb-layers.png)

## <a name="product-highlights"></a><span data-ttu-id="5a46d-118">Caratteristiche principali del prodotto</span><span class="sxs-lookup"><span data-stu-id="5a46d-118">Product Highlights</span></span>

- <span data-ttu-id="5a46d-119">Supporto completo del processore ThreadX</span><span class="sxs-lookup"><span data-stu-id="5a46d-119">Complete ThreadX processor support</span></span>
- <span data-ttu-id="5a46d-120">Nessun royalties</span><span class="sxs-lookup"><span data-stu-id="5a46d-120">No royalties</span></span>
- <span data-ttu-id="5a46d-121">Completa codice sorgente ANSI C</span><span class="sxs-lookup"><span data-stu-id="5a46d-121">Complete ANSI C source code</span></span>
- <span data-ttu-id="5a46d-122">Prestazioni in tempo reale</span><span class="sxs-lookup"><span data-stu-id="5a46d-122">Real-time performance</span></span>
- <span data-ttu-id="5a46d-123">Supporto tecnico reattivo</span><span class="sxs-lookup"><span data-stu-id="5a46d-123">Responsive technical support</span></span>
- <span data-ttu-id="5a46d-124">Supporto di più classi</span><span class="sxs-lookup"><span data-stu-id="5a46d-124">Multiple class support</span></span>
- <span data-ttu-id="5a46d-125">Istanze di più classi</span><span class="sxs-lookup"><span data-stu-id="5a46d-125">Multiple class instances</span></span>
- <span data-ttu-id="5a46d-126">Integrazione di classi con ThreadX, FileX e NetX</span><span class="sxs-lookup"><span data-stu-id="5a46d-126">Integration of classes with ThreadX, FileX, and NetX</span></span>
- <span data-ttu-id="5a46d-127">Supporto per dispositivi USB con più configurazioni</span><span class="sxs-lookup"><span data-stu-id="5a46d-127">Support for USB devices with multiple configurations</span></span>
- <span data-ttu-id="5a46d-128">Supporto per dispositivi compositi USB</span><span class="sxs-lookup"><span data-stu-id="5a46d-128">Support for USB composite devices</span></span>
- <span data-ttu-id="5a46d-129">Supporto per il risparmio energia USB</span><span class="sxs-lookup"><span data-stu-id="5a46d-129">Support for USB power management</span></span>
- <span data-ttu-id="5a46d-130">Supporto per USB OTG</span><span class="sxs-lookup"><span data-stu-id="5a46d-130">Support for USB OTG</span></span>
- <span data-ttu-id="5a46d-131">Esportare eventi di traccia per TraceX</span><span class="sxs-lookup"><span data-stu-id="5a46d-131">Export trace events for TraceX</span></span>

## <a name="powerful-services-of-usbx"></a><span data-ttu-id="5a46d-132">Potenti servizi di USBX</span><span class="sxs-lookup"><span data-stu-id="5a46d-132">Powerful Services of USBX</span></span>

### <a name="complete-usb-device-framework-support"></a><span data-ttu-id="5a46d-133">Supporto completo per il Framework di dispositivi USB</span><span class="sxs-lookup"><span data-stu-id="5a46d-133">Complete USB Device Framework Support</span></span>

<span data-ttu-id="5a46d-134">USBX può supportare i dispositivi USB più complessi, tra cui più configurazioni, più interfacce e più impostazioni alternative.</span><span class="sxs-lookup"><span data-stu-id="5a46d-134">USBX can support the most demanding USB devices, including multiple configurations, multiple interfaces, and multiple alternate settings.</span></span>

### <a name="easy-to-use-apis"></a><span data-ttu-id="5a46d-135">API facili da usare</span><span class="sxs-lookup"><span data-stu-id="5a46d-135">Easy-To-Use APIs</span></span>

<span data-ttu-id="5a46d-136">USBX fornisce lo stack USB migliore con la massima incorporata in modo facile da comprendere e utilizzare.</span><span class="sxs-lookup"><span data-stu-id="5a46d-136">USBX provides the best deeply embedded USB stack in a manner that is easy to understand and use.</span></span> <span data-ttu-id="5a46d-137">L'API USBX rende i servizi intuitivi e coerenti.</span><span class="sxs-lookup"><span data-stu-id="5a46d-137">The USBX API makes the services intuitive and consistent.</span></span> <span data-ttu-id="5a46d-138">Utilizzando le API della classe USBX fornite, l'applicazione utente non deve comprendere la complessità dei protocolli USB.</span><span class="sxs-lookup"><span data-stu-id="5a46d-138">By using the provided USBX class APIs, the user application does not need to understand the complexity of the USB protocols.</span></span>
