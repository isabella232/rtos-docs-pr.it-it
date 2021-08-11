---
title: Capitolo 1 - Introduzione al Azure RTOS client NetX Duo LWM2M
description: Questo capitolo contiene un'introduzione Azure RTOS client del protocollo NetX Duo Lightweight Machine to Machine.
author: v-condav
ms.author: v-condav
ms.date: 01/22/2021
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a2722daac76632e492d0f9345103c45da9ba1b321e91c9c04e04c76463984c3a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116783476"
---
# <a name="chapter-1--introduction-to-lwm2m-client"></a>Capitolo 1 Introduzione al client LWM2M

Il Azure RTOS client NetX Duo LWM2M implementa la parte client dello standard del protocollo Lightweight Machine to Machine. (LWM2M 1.0-20170208A)

## <a name="netx-lwm2m-client-requirements"></a>Requisiti del client NetX LWM2M

Per funzionare correttamente, la libreria di runtime del client LWM2M richiede che sia già stata creata un'istanza IP NetX. Il pacchetto client NetX LWM2M non ha altri requisiti.

## <a name="netx-lwm2m-client-rfcs"></a>RFC client NetX LWM2M

Il client LWM2M è conforme a OMA-TS-LightweightM2M-V1 \_ 0-20170208-A e alle RFC seguenti correlate al protocollo CoAP (Constrained Application Protocol).

* RFC 7252 The Constrained Application Protocol (CoAP)

* RFC 7641 Observing Resources in the Constrained Application Protocol (CoAP)

* Formato di collegamento RFC 6690 Constrained RESTful Environments (CoRE)

Per altre informazioni, vedere [OMA-TS-LightweightM2M-V1 \_ 0-2017208-A.](http://www.openmobilealliance.org/release/LightweightM2M/V1_0-20170208-A/OMA-TS-LightweightM2M-V1_0-20170208-A.pdf)