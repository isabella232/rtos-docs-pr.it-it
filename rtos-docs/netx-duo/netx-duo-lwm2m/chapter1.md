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
# <a name="chapter-1--introduction-to-lwm2m-client"></a>Capitolo 1 Introduzione al client LWM2M

Il protocollo client di Azure RTO NetX Duo LWM2M implementa la parte client del computer Lightweight per il protocollo machine standard. (LWM2M 1.0-20170208A)

## <a name="netx-lwm2m-client-requirements"></a>Requisiti del client LWM2M di NetX

Per funzionare correttamente, la libreria di runtime del client LWM2M richiede che sia già stata creata un'istanza IP di NetX. Il pacchetto client LWM2M di NetX non ha altri requisiti.

## <a name="netx-lwm2m-client-rfcs"></a>RFC client LWM2M di NetX

Il client LWM2M è conforme a OMA-TS-LightweightM2M-V1 \_ 0-20170208-A e ai seguenti RFC correlati al protocollo applicativo vincolato (CoAP).

* RFC 7252 il protocollo applicativo vincolato (CoAP)

* RFC 7641 osservazione delle risorse nel protocollo applicativo vincolato (CoAP)

* Formato di collegamento ambienti RESTful (CoRE) con vincoli RFC 6690

Per ulteriori informazioni, vedere [OMA-TS-LightweightM2M-V1 \_ 0-2017208-A](http://www.openmobilealliance.org/release/LightweightM2M/V1_0-20170208-A/OMA-TS-LightweightM2M-V1_0-20170208-A.pdf).