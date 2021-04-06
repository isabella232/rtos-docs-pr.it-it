---
title: Capitolo 1-Introduzione ad Azure RTO USBX stack host
description: Questo capitolo introduce lo stack host USBX, che descrive le applicazioni e i vantaggi.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: a9fdd86d47bd4680409cc550c87bc6f456d146a9
ms.sourcegitcommit: d8edbb3207fe99f8afb431597dac063e73383e68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377051"
---
# <a name="chapter-1---introduction-to-azure-rtos-usbx-host-stack"></a><span data-ttu-id="5ceea-103">Capitolo 1-Introduzione ad Azure RTO USBX stack host</span><span class="sxs-lookup"><span data-stu-id="5ceea-103">Chapter 1 - Introduction to Azure RTOS USBX Host Stack</span></span>

<span data-ttu-id="5ceea-104">USBX è uno stack USB completo per applicazioni con Deep embedded.</span><span class="sxs-lookup"><span data-stu-id="5ceea-104">USBX is a full-featured USB stack for deeply embedded applications.</span></span> <span data-ttu-id="5ceea-105">Questo capitolo introduce USBX, che descrive le applicazioni e i vantaggi.</span><span class="sxs-lookup"><span data-stu-id="5ceea-105">This chapter introduces USBX, describing its applications and benefits.</span></span>

## <a name="usbx-features"></a><span data-ttu-id="5ceea-106">Funzionalità di USBX</span><span class="sxs-lookup"><span data-stu-id="5ceea-106">USBX features</span></span>

<span data-ttu-id="5ceea-107">USBX supportano le tre specifiche USB esistenti: 1,1, 2,0 e OTG.</span><span class="sxs-lookup"><span data-stu-id="5ceea-107">USBX support the three existing USB specifications: 1.1, 2.0 and OTG.</span></span> <span data-ttu-id="5ceea-108">È progettato per essere scalabile e può includere semplici topologie USB con un solo dispositivo connesso, oltre a topologie complesse con più dispositivi e hub a cascata.</span><span class="sxs-lookup"><span data-stu-id="5ceea-108">It is designed to be scalable and will accommodate simple USB topologies with only one connected device as well as complex topologies with multiple devices and cascading hubs.</span></span> <span data-ttu-id="5ceea-109">USBX supporta tutti i tipi di trasferimento dati dei protocolli USB: controllo, bulk, interrupt e isocrono.</span><span class="sxs-lookup"><span data-stu-id="5ceea-109">USBX supports all the data transfer types of the USB protocols: control, bulk, interrupt, and isochronous.</span></span>

<span data-ttu-id="5ceea-110">USBX supporta sia il lato host che il lato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5ceea-110">USBX supports both the host side and the device side.</span></span> <span data-ttu-id="5ceea-111">Ogni lato è costituito da tre livelli.</span><span class="sxs-lookup"><span data-stu-id="5ceea-111">Each side is comprised of three layers.</span></span>

- <span data-ttu-id="5ceea-112">Livello controller</span><span class="sxs-lookup"><span data-stu-id="5ceea-112">Controller layer</span></span>
- <span data-ttu-id="5ceea-113">Livello stack</span><span class="sxs-lookup"><span data-stu-id="5ceea-113">Stack layer</span></span>
- <span data-ttu-id="5ceea-114">Livello classe</span><span class="sxs-lookup"><span data-stu-id="5ceea-114">Class layer</span></span>

<span data-ttu-id="5ceea-115">La relazione tra i livelli USB è la seguente.</span><span class="sxs-lookup"><span data-stu-id="5ceea-115">The relationship between the USB layers is as follows.</span></span>

![Livelli USB](./media/usbx-device-stack/usb-layers.png)

## <a name="product-highlights"></a><span data-ttu-id="5ceea-117">Caratteristiche principali del prodotto</span><span class="sxs-lookup"><span data-stu-id="5ceea-117">Product Highlights</span></span>

- <span data-ttu-id="5ceea-118">Supporto completo del processore ThreadX</span><span class="sxs-lookup"><span data-stu-id="5ceea-118">Complete ThreadX processor support</span></span>
- <span data-ttu-id="5ceea-119">Nessun royalties</span><span class="sxs-lookup"><span data-stu-id="5ceea-119">No royalties</span></span>
- <span data-ttu-id="5ceea-120">Completa codice sorgente ANSI C</span><span class="sxs-lookup"><span data-stu-id="5ceea-120">Complete ANSI C source code</span></span>
- <span data-ttu-id="5ceea-121">Prestazioni in tempo reale</span><span class="sxs-lookup"><span data-stu-id="5ceea-121">Real-time performance</span></span>
- <span data-ttu-id="5ceea-122">Supporto tecnico reattivo</span><span class="sxs-lookup"><span data-stu-id="5ceea-122">Responsive technical support</span></span>
- <span data-ttu-id="5ceea-123">Supporto per più controller host</span><span class="sxs-lookup"><span data-stu-id="5ceea-123">Multiple host controller support</span></span>
- <span data-ttu-id="5ceea-124">Supporto di più classi</span><span class="sxs-lookup"><span data-stu-id="5ceea-124">Multiple class support</span></span>
- <span data-ttu-id="5ceea-125">Istanze di più classi</span><span class="sxs-lookup"><span data-stu-id="5ceea-125">Multiple class instances</span></span>
- <span data-ttu-id="5ceea-126">Integrazione di classi con ThreadX, FileX e NetX</span><span class="sxs-lookup"><span data-stu-id="5ceea-126">Integration of classes with ThreadX, FileX and NetX</span></span>
- <span data-ttu-id="5ceea-127">Supporto per dispositivi USB con più configurazioni</span><span class="sxs-lookup"><span data-stu-id="5ceea-127">Support for USB devices with multiple configuration</span></span>
- <span data-ttu-id="5ceea-128">Supporto per dispositivi compositi USB</span><span class="sxs-lookup"><span data-stu-id="5ceea-128">Support for USB composite devices</span></span>
- <span data-ttu-id="5ceea-129">Supporto per gli hub a catena</span><span class="sxs-lookup"><span data-stu-id="5ceea-129">Support for cascading hubs</span></span>
- <span data-ttu-id="5ceea-130">Supporto per il risparmio energia USB</span><span class="sxs-lookup"><span data-stu-id="5ceea-130">Support for USB power management</span></span>
- <span data-ttu-id="5ceea-131">Supporto per USB OTG</span><span class="sxs-lookup"><span data-stu-id="5ceea-131">Support for USB OTG</span></span>
- <span data-ttu-id="5ceea-132">Esportare eventi di traccia per TraceX</span><span class="sxs-lookup"><span data-stu-id="5ceea-132">Export trace events for TraceX</span></span>

## <a name="powerful-services-of-usbx"></a><span data-ttu-id="5ceea-133">Potenti servizi di USBX</span><span class="sxs-lookup"><span data-stu-id="5ceea-133">Powerful Services of USBX</span></span>

### <a name="multiple-host-controller-support"></a><span data-ttu-id="5ceea-134">Supporto per più controller host</span><span class="sxs-lookup"><span data-stu-id="5ceea-134">Multiple Host Controller Support</span></span>

<span data-ttu-id="5ceea-135">USBX può supportare più controller host USB in esecuzione simultanea.</span><span class="sxs-lookup"><span data-stu-id="5ceea-135">USBX can support multiple USB host controllers running concurrently.</span></span> <span data-ttu-id="5ceea-136">Questa funzionalità consente a USBX di supportare lo standard USB 2,0 usando lo schema di compatibilità con le versioni precedenti associato alla maggior parte dei controller host USB 2,0 attualmente disponibili sul mercato.</span><span class="sxs-lookup"><span data-stu-id="5ceea-136">This feature allows USBX to support the USB 2.0 standard using the backward compatibility scheme associated with most USB 2.0 host controllers on the market today.</span></span>

### <a name="usb-software-scheduler"></a><span data-ttu-id="5ceea-137">Utilità di pianificazione software USB</span><span class="sxs-lookup"><span data-stu-id="5ceea-137">USB Software Scheduler</span></span>

<span data-ttu-id="5ceea-138">USBX contiene un'utilità di pianificazione software USB necessaria per supportare i controller USB per i quali non è disponibile l'elaborazione dell'elenco hardware.</span><span class="sxs-lookup"><span data-stu-id="5ceea-138">USBX contains a USB software scheduler necessary to support USB controllers that do not have hardware list processing.</span></span> <span data-ttu-id="5ceea-139">L'utilità di pianificazione del software USBX organizzerà i trasferimenti USB con la frequenza di servizio e priorità corretta e indicherà al controller USB di eseguire ogni trasferimento.</span><span class="sxs-lookup"><span data-stu-id="5ceea-139">The USBX software scheduler will organize USB transfers with the correct frequency of service and priority, and will instruct the USB controller to execute each transfer.</span></span>

### <a name="complete-usb-device-framework-support"></a><span data-ttu-id="5ceea-140">Supporto completo per il Framework di dispositivi USB</span><span class="sxs-lookup"><span data-stu-id="5ceea-140">Complete USB Device Framework Support</span></span>

<span data-ttu-id="5ceea-141">USBX può supportare i dispositivi USB più complessi, tra cui più configurazioni, più interfacce e più impostazioni alternative.</span><span class="sxs-lookup"><span data-stu-id="5ceea-141">USBX can support the most demanding USB devices, including multiple configurations, multiple interfaces, and multiple alternate settings.</span></span>

### <a name="easy-to-use-apis"></a><span data-ttu-id="5ceea-142">API facili da usare</span><span class="sxs-lookup"><span data-stu-id="5ceea-142">Easy-To-Use APIs</span></span>

<span data-ttu-id="5ceea-143">USBX fornisce lo stack USB molto più efficace in modo che sia facile da comprendere e utilizzare.</span><span class="sxs-lookup"><span data-stu-id="5ceea-143">USBX provides the very best deeply embedded USB stack in a manner that is easy to understand and use.</span></span> <span data-ttu-id="5ceea-144">L'API USBX rende i servizi intuitivi e coerenti.</span><span class="sxs-lookup"><span data-stu-id="5ceea-144">The USBX API makes the services intuitive and consistent.</span></span> <span data-ttu-id="5ceea-145">Utilizzando le API della classe USBX fornite, l'applicazione utente non deve comprendere la complessità dei protocolli USB.</span><span class="sxs-lookup"><span data-stu-id="5ceea-145">By using the provided USBX class APIs, the user application does not need to understand the complexity of the USB protocols.</span></span>
