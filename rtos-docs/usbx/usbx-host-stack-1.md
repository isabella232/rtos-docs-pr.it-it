---
title: Capitolo 1-Introduzione ad Azure RTO USBX stack host
description: USBX è uno stack USB completo per applicazioni con Deep embedded. Questo capitolo introduce USBX, che descrive le applicazioni e i vantaggi.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 9ee49903e764e20316438be16b47d2d9208b1363
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824449"
---
# <a name="chapter-1---introduction-to-azure-rtos-usbx-host-stack"></a><span data-ttu-id="b8e89-104">Capitolo 1-Introduzione ad Azure RTO USBX stack host</span><span class="sxs-lookup"><span data-stu-id="b8e89-104">Chapter 1 - Introduction to Azure RTOS USBX Host Stack</span></span>

<span data-ttu-id="b8e89-105">USBX è uno stack USB completo per applicazioni con Deep embedded.</span><span class="sxs-lookup"><span data-stu-id="b8e89-105">USBX is a full-featured USB stack for deeply embedded applications.</span></span> <span data-ttu-id="b8e89-106">Questo capitolo introduce USBX, che descrive le applicazioni e i vantaggi.</span><span class="sxs-lookup"><span data-stu-id="b8e89-106">This chapter introduces USBX, describing its applications and benefits.</span></span>

## <a name="usbx-features"></a><span data-ttu-id="b8e89-107">Funzionalità di USBX</span><span class="sxs-lookup"><span data-stu-id="b8e89-107">USBX features</span></span>

<span data-ttu-id="b8e89-108">USBX supportano le tre specifiche USB esistenti: 1,1, 2,0 e OTG.</span><span class="sxs-lookup"><span data-stu-id="b8e89-108">USBX support the three existing USB specifications: 1.1, 2.0 and OTG.</span></span> <span data-ttu-id="b8e89-109">È progettato per essere scalabile e può includere semplici topologie USB con un solo dispositivo connesso, oltre a topologie complesse con più dispositivi e hub a cascata.</span><span class="sxs-lookup"><span data-stu-id="b8e89-109">It is designed to be scalable and will accommodate simple USB topologies with only one connected device as well as complex topologies with multiple devices and cascading hubs.</span></span> <span data-ttu-id="b8e89-110">USBX supporta tutti i tipi di trasferimento dati dei protocolli USB: controllo, bulk, interrupt e isocrono.</span><span class="sxs-lookup"><span data-stu-id="b8e89-110">USBX supports all the data transfer types of the USB protocols: control, bulk, interrupt, and isochronous.</span></span>

<span data-ttu-id="b8e89-111">USBX supporta sia il lato host che il lato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b8e89-111">USBX supports both the host side and the device side.</span></span> <span data-ttu-id="b8e89-112">Ogni lato è costituito da tre livelli.</span><span class="sxs-lookup"><span data-stu-id="b8e89-112">Each side is comprised of three layers.</span></span>

- <span data-ttu-id="b8e89-113">Livello controller</span><span class="sxs-lookup"><span data-stu-id="b8e89-113">Controller layer</span></span>
- <span data-ttu-id="b8e89-114">Livello stack</span><span class="sxs-lookup"><span data-stu-id="b8e89-114">Stack layer</span></span>
- <span data-ttu-id="b8e89-115">Livello classe</span><span class="sxs-lookup"><span data-stu-id="b8e89-115">Class layer</span></span>

<span data-ttu-id="b8e89-116">La relazione tra i livelli USB è la seguente.</span><span class="sxs-lookup"><span data-stu-id="b8e89-116">The relationship between the USB layers is as follows.</span></span>

![Livelli USB](./media/usbx-device-stack/usb-layers.png)

## <a name="product-highlights"></a><span data-ttu-id="b8e89-118">Caratteristiche principali del prodotto</span><span class="sxs-lookup"><span data-stu-id="b8e89-118">Product Highlights</span></span>

- <span data-ttu-id="b8e89-119">Supporto completo del processore ThreadX</span><span class="sxs-lookup"><span data-stu-id="b8e89-119">Complete ThreadX processor support</span></span>
- <span data-ttu-id="b8e89-120">Nessun royalties</span><span class="sxs-lookup"><span data-stu-id="b8e89-120">No royalties</span></span>
- <span data-ttu-id="b8e89-121">Completa codice sorgente ANSI C</span><span class="sxs-lookup"><span data-stu-id="b8e89-121">Complete ANSI C source code</span></span>
- <span data-ttu-id="b8e89-122">Prestazioni in tempo reale</span><span class="sxs-lookup"><span data-stu-id="b8e89-122">Real-time performance</span></span>
- <span data-ttu-id="b8e89-123">Supporto tecnico reattivo</span><span class="sxs-lookup"><span data-stu-id="b8e89-123">Responsive technical support</span></span>
- <span data-ttu-id="b8e89-124">Supporto per più controller host</span><span class="sxs-lookup"><span data-stu-id="b8e89-124">Multiple host controller support</span></span>
- <span data-ttu-id="b8e89-125">Supporto di più classi</span><span class="sxs-lookup"><span data-stu-id="b8e89-125">Multiple class support</span></span>
- <span data-ttu-id="b8e89-126">Istanze di più classi</span><span class="sxs-lookup"><span data-stu-id="b8e89-126">Multiple class instances</span></span>
- <span data-ttu-id="b8e89-127">Integrazione di classi con ThreadX, FileX e NetX</span><span class="sxs-lookup"><span data-stu-id="b8e89-127">Integration of classes with ThreadX, FileX and NetX</span></span>
- <span data-ttu-id="b8e89-128">Supporto per dispositivi USB con più configurazioni</span><span class="sxs-lookup"><span data-stu-id="b8e89-128">Support for USB devices with multiple configuration</span></span>
- <span data-ttu-id="b8e89-129">Supporto per dispositivi compositi USB</span><span class="sxs-lookup"><span data-stu-id="b8e89-129">Support for USB composite devices</span></span>
- <span data-ttu-id="b8e89-130">Supporto per gli hub a catena</span><span class="sxs-lookup"><span data-stu-id="b8e89-130">Support for cascading hubs</span></span>
- <span data-ttu-id="b8e89-131">Supporto per il risparmio energia USB</span><span class="sxs-lookup"><span data-stu-id="b8e89-131">Support for USB power management</span></span>
- <span data-ttu-id="b8e89-132">Supporto per USB OTG</span><span class="sxs-lookup"><span data-stu-id="b8e89-132">Support for USB OTG</span></span>
- <span data-ttu-id="b8e89-133">Esportare eventi di traccia per TraceX</span><span class="sxs-lookup"><span data-stu-id="b8e89-133">Export trace events for TraceX</span></span>

## <a name="powerful-services-of-usbx"></a><span data-ttu-id="b8e89-134">Potenti servizi di USBX</span><span class="sxs-lookup"><span data-stu-id="b8e89-134">Powerful Services of USBX</span></span>

### <a name="multiple-host-controller-support"></a><span data-ttu-id="b8e89-135">Supporto per più controller host</span><span class="sxs-lookup"><span data-stu-id="b8e89-135">Multiple Host Controller Support</span></span>

<span data-ttu-id="b8e89-136">USBX può supportare più controller host USB in esecuzione simultanea.</span><span class="sxs-lookup"><span data-stu-id="b8e89-136">USBX can support multiple USB host controllers running concurrently.</span></span> <span data-ttu-id="b8e89-137">Questa funzionalità consente a USBX di supportare lo standard USB 2,0 usando lo schema di compatibilità con le versioni precedenti associato alla maggior parte dei controller host USB 2,0 attualmente disponibili sul mercato.</span><span class="sxs-lookup"><span data-stu-id="b8e89-137">This feature allows USBX to support the USB 2.0 standard using the backward compatibility scheme associated with most USB 2.0 host controllers on the market today.</span></span>

### <a name="usb-software-scheduler"></a><span data-ttu-id="b8e89-138">Utilità di pianificazione software USB</span><span class="sxs-lookup"><span data-stu-id="b8e89-138">USB Software Scheduler</span></span>

<span data-ttu-id="b8e89-139">USBX contiene un'utilità di pianificazione software USB necessaria per supportare i controller USB per i quali non è disponibile l'elaborazione dell'elenco hardware.</span><span class="sxs-lookup"><span data-stu-id="b8e89-139">USBX contains a USB software scheduler necessary to support USB controllers that do not have hardware list processing.</span></span> <span data-ttu-id="b8e89-140">L'utilità di pianificazione del software USBX organizzerà i trasferimenti USB con la frequenza di servizio e priorità corretta e indicherà al controller USB di eseguire ogni trasferimento.</span><span class="sxs-lookup"><span data-stu-id="b8e89-140">The USBX software scheduler will organize USB transfers with the correct frequency of service and priority, and will instruct the USB controller to execute each transfer.</span></span>

### <a name="complete-usb-device-framework-support"></a><span data-ttu-id="b8e89-141">Supporto completo per il Framework di dispositivi USB</span><span class="sxs-lookup"><span data-stu-id="b8e89-141">Complete USB Device Framework Support</span></span>

<span data-ttu-id="b8e89-142">USBX può supportare i dispositivi USB più complessi, tra cui più configurazioni, più interfacce e più impostazioni alternative.</span><span class="sxs-lookup"><span data-stu-id="b8e89-142">USBX can support the most demanding USB devices, including multiple configurations, multiple interfaces, and multiple alternate settings.</span></span>

### <a name="easy-to-use-apis"></a><span data-ttu-id="b8e89-143">API facili da usare</span><span class="sxs-lookup"><span data-stu-id="b8e89-143">Easy-To-Use APIs</span></span>

<span data-ttu-id="b8e89-144">USBX fornisce lo stack USB molto più efficace in modo che sia facile da comprendere e utilizzare.</span><span class="sxs-lookup"><span data-stu-id="b8e89-144">USBX provides the very best deeply embedded USB stack in a manner that is easy to understand and use.</span></span> <span data-ttu-id="b8e89-145">L'API USBX rende i servizi intuitivi e coerenti.</span><span class="sxs-lookup"><span data-stu-id="b8e89-145">The USBX API makes the services intuitive and consistent.</span></span> <span data-ttu-id="b8e89-146">Utilizzando le API della classe USBX fornite, l'applicazione utente non deve comprendere la complessità dei protocolli USB.</span><span class="sxs-lookup"><span data-stu-id="b8e89-146">By using the provided USBX class APIs, the user application does not need to understand the complexity of the USB protocols.</span></span>
