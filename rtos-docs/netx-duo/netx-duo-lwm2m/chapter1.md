---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo LWM2M client
description: Questo capitolo contiene un'introduzione ad Azure RTO NetX Duo Lightweight Machine a Machine Protocol client.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 12f13c154668b3cadfae0924e59b55631dc27424
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821860"
---
# <a name="chapter-1--introduction-to-lwm2m-client"></a><span data-ttu-id="0e09a-103">Capitolo 1 Introduzione al client LWM2M</span><span class="sxs-lookup"><span data-stu-id="0e09a-103">Chapter 1  Introduction to LWM2M Client</span></span>

<span data-ttu-id="0e09a-104">Il protocollo client di Azure RTO NetX Duo LWM2M implementa la parte client del computer Lightweight per il protocollo machine standard.</span><span class="sxs-lookup"><span data-stu-id="0e09a-104">The Azure RTOS NetX Duo LWM2M Client Protocol implements the client part of the Lightweight Machine to Machine protocol standard.</span></span> <span data-ttu-id="0e09a-105">(LWM2M 1.0-20170208A)</span><span class="sxs-lookup"><span data-stu-id="0e09a-105">(LWM2M 1.0-20170208A)</span></span>

## <a name="netx-lwm2m-client-requirements"></a><span data-ttu-id="0e09a-106">Requisiti del client LWM2M di NetX</span><span class="sxs-lookup"><span data-stu-id="0e09a-106">NetX LWM2M Client Requirements</span></span>

<span data-ttu-id="0e09a-107">Per funzionare correttamente, la libreria di runtime del client LWM2M richiede che sia già stata creata un'istanza IP di NetX.</span><span class="sxs-lookup"><span data-stu-id="0e09a-107">In order to function properly, the LWM2M Client run-time library requires that a NetX IP instance has already been created.</span></span> <span data-ttu-id="0e09a-108">Il pacchetto client LWM2M di NetX non ha altri requisiti.</span><span class="sxs-lookup"><span data-stu-id="0e09a-108">The NetX LWM2M Client package has no further requirements.</span></span>

## <a name="netx-lwm2m-client-rfcs"></a><span data-ttu-id="0e09a-109">RFC client LWM2M di NetX</span><span class="sxs-lookup"><span data-stu-id="0e09a-109">NetX LWM2M Client RFCs</span></span>

<span data-ttu-id="0e09a-110">Il client LWM2M è conforme a OMA-TS-LightweightM2M-V1 \_ 0-20170208-A e ai seguenti RFC correlati al protocollo applicativo vincolato (CoAP).</span><span class="sxs-lookup"><span data-stu-id="0e09a-110">LWM2M Client is compliant with OMA-TS-LightweightM2M-V1\_0-20170208-A and the following RFCs related to the Constrained Application Protocol (CoAP).</span></span>

* <span data-ttu-id="0e09a-111">RFC 7252 il protocollo applicativo vincolato (CoAP)</span><span class="sxs-lookup"><span data-stu-id="0e09a-111">RFC 7252 The Constrained Application Protocol (CoAP)</span></span>

* <span data-ttu-id="0e09a-112">RFC 7641 osservazione delle risorse nel protocollo applicativo vincolato (CoAP)</span><span class="sxs-lookup"><span data-stu-id="0e09a-112">RFC 7641 Observing Resources in the Constrained Application Protocol (CoAP)</span></span>

* <span data-ttu-id="0e09a-113">Formato di collegamento ambienti RESTful (CoRE) con vincoli RFC 6690</span><span class="sxs-lookup"><span data-stu-id="0e09a-113">RFC 6690 Constrained RESTful Environments (CoRE) Link Format</span></span>

<span data-ttu-id="0e09a-114">Per ulteriori informazioni, vedere [OMA-TS-LightweightM2M-V1 \_ 0-2017208-A](http://www.openmobilealliance.org/release/LightweightM2M/V1_0-20170208-A/OMA-TS-LightweightM2M-V1_0-20170208-A.pdf).</span><span class="sxs-lookup"><span data-stu-id="0e09a-114">For more information, please see [OMA-TS-LightweightM2M-V1\_0-2017208-A](http://www.openmobilealliance.org/release/LightweightM2M/V1_0-20170208-A/OMA-TS-LightweightM2M-V1_0-20170208-A.pdf).</span></span>