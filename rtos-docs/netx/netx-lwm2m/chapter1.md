---
title: Capitolo 1-Introduzione ad Azure RTO NetX LWM2M
description: Il protocollo LWM2M di Azure RTO NetX implementa la parte client del computer leggero con il protocollo machine standard.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: c29af430975266eed684bd1de38d9e5d7e2586a6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822613"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-lwm2m"></a><span data-ttu-id="2b332-103">Capitolo 1-Introduzione ad Azure RTO NetX LWM2M</span><span class="sxs-lookup"><span data-stu-id="2b332-103">Chapter 1 - Introduction to Azure RTOS NetX LWM2M</span></span>

<span data-ttu-id="2b332-104">Il protocollo LWM2M di Azure RTO NetX implementa la parte client del computer leggero con il protocollo machine standard.</span><span class="sxs-lookup"><span data-stu-id="2b332-104">The Azure RTOS NetX LWM2M Protocol implements the client part of the Lightweight Machine to Machine protocol standard.</span></span>

## <a name="netx-lwm2m-requirements"></a><span data-ttu-id="2b332-105">Requisiti LWM2M di NetX</span><span class="sxs-lookup"><span data-stu-id="2b332-105">NetX LWM2M Requirements</span></span>

<span data-ttu-id="2b332-106">Per funzionare correttamente, la libreria di runtime NetX LWM2M richiede che sia già stata creata un'istanza IP NetX.</span><span class="sxs-lookup"><span data-stu-id="2b332-106">In order to function properly, the NetX LWM2M run-time library requires that a NetX IP instance has already been created.</span></span> <span data-ttu-id="2b332-107">Il pacchetto LWM2M NetX non ha altri requisiti.</span><span class="sxs-lookup"><span data-stu-id="2b332-107">The NetX LWM2M package has no further requirements.</span></span>

## <a name="netx-lwm2m-rfcs"></a><span data-ttu-id="2b332-108">RFC NetX LWM2M</span><span class="sxs-lookup"><span data-stu-id="2b332-108">NetX LWM2M RFCs</span></span>

<span data-ttu-id="2b332-109">LWM2M NetX è conforme a OMA-TS-LightweightM2M-V1_0 -20170208-A e ai seguenti RFC correlati al protocollo applicativo vincolato (CoAP):</span><span class="sxs-lookup"><span data-stu-id="2b332-109">NetX LWM2M is compliant with OMA-TS-LightweightM2M-V1_0-20170208-A and the following RFCs related to the Constrained Application Protocol (CoAP):</span></span>

- <span data-ttu-id="2b332-110">**RFC 7252**: protocollo applicativo vincolato (CoAP)</span><span class="sxs-lookup"><span data-stu-id="2b332-110">**RFC 7252**: The Constrained Application Protocol (CoAP)</span></span>

- <span data-ttu-id="2b332-111">**RFC 7641**: osservazione delle risorse nel protocollo applicativo vincolato (CoAP)</span><span class="sxs-lookup"><span data-stu-id="2b332-111">**RFC 7641**: Observing Resources in the Constrained Application Protocol (CoAP)</span></span>

- <span data-ttu-id="2b332-112">**RFC 6690**: formato di collegamento ambienti RESTful con vincoli (Core)</span><span class="sxs-lookup"><span data-stu-id="2b332-112">**RFC 6690**: Constrained RESTful Environments (CoRE) Link Format</span></span>