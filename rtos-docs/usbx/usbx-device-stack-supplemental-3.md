---
title: Capitolo 3-Considerazioni sulle classi DPUMP di USBX
description: USBX contiene una classe DPUMP per l'host e il lato dispositivo. Questa classe non è una classe standard, ma piuttosto un esempio che illustra come creare un dispositivo semplice usando due pipe bulk e inviando i dati in queste due pipe
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c7870f1984fe3104d30e3b9efd82010218acbe27
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824518"
---
# <a name="chapter-3---usbx-dpump-class-considerations"></a><span data-ttu-id="150e7-104">Capitolo 3-Considerazioni sulle classi DPUMP di USBX</span><span class="sxs-lookup"><span data-stu-id="150e7-104">Chapter 3 - USBX DPUMP Class Considerations</span></span>

<span data-ttu-id="150e7-105">USBX contiene una classe **DPUMP** per l'host e il lato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="150e7-105">USBX contains a **DPUMP** class for the host and device side.</span></span> <span data-ttu-id="150e7-106">Questa classe non è una classe standard, ma piuttosto un esempio in cui viene illustrato come creare un dispositivo semplice utilizzando due pipe bulk e inviando i dati in queste due pipe.</span><span class="sxs-lookup"><span data-stu-id="150e7-106">This class is not a standard class in itself, but rather an example that illustrates how to create a simple device by using two bulk pipes and sending data back and forth on these two pipes.</span></span> <span data-ttu-id="150e7-107">La classe **DPUMP** può essere usata per avviare una classe personalizzata o per i dispositivi RS232 legacy.</span><span class="sxs-lookup"><span data-stu-id="150e7-107">The **DPUMP** class could be used to start a custom class or for legacy RS232 devices.</span></span>

<span data-ttu-id="150e7-108">Diagramma di flusso DPUMP USB:</span><span class="sxs-lookup"><span data-stu-id="150e7-108">USB DPUMP flow chart:</span></span>

![Diagramma di flusso DPUMP USB](./media/usbx-device-stack-supplemental/usb-dpump-flow-chart.png)

## <a name="usbx-dpump-device-class"></a><span data-ttu-id="150e7-110">Classe USBX DPUMP Device</span><span class="sxs-lookup"><span data-stu-id="150e7-110">USBX DPUMP Device Class</span></span>

<span data-ttu-id="150e7-111">La classe Device **DPUMP** usa un thread, che viene avviato al momento della connessione all'host USB.</span><span class="sxs-lookup"><span data-stu-id="150e7-111">The device **DPUMP** class uses a thread, which is started upon connection to the USB host.</span></span> <span data-ttu-id="150e7-112">Il thread attende un pacchetto in arrivo nell'endpoint in blocco.</span><span class="sxs-lookup"><span data-stu-id="150e7-112">The thread waits for a packet coming on the Bulk Out endpoint.</span></span> <span data-ttu-id="150e7-113">Quando viene ricevuto un pacchetto, il contenuto viene copiato in blocco nel buffer dell'endpoint e viene inviata una transazione sull'endpoint, in attesa che l'host invii una richiesta di lettura da questo endpoint.</span><span class="sxs-lookup"><span data-stu-id="150e7-113">When a packet is received, it copies the content to the Bulk In endpoint buffer and posts a transaction on this endpoint, waiting for the host to issue a request to read from this endpoint.</span></span> <span data-ttu-id="150e7-114">In questo modo viene fornito un meccanismo di loopback tra le operazioni bulk e bulk negli endpoint.</span><span class="sxs-lookup"><span data-stu-id="150e7-114">This provides a loopback mechanism between the Bulk Out and Bulk In endpoints.</span></span>
