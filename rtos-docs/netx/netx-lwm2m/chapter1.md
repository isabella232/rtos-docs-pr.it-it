---
title: Capitolo 1 - Introduzione a Azure RTOS NetX LWM2M
description: Il Azure RTOS NetX LWM2M implementa la parte client dello standard del protocollo Lightweight Machine to Machine.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: fe9c90ec10b241c72c71882b28b5fe0e3e60e3913435ec27f797eade4ca4eca5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784921"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-lwm2m"></a>Capitolo 1 - Introduzione a Azure RTOS NetX LWM2M

Il Azure RTOS NetX LWM2M implementa la parte client dello standard del protocollo Lightweight Machine to Machine.

## <a name="netx-lwm2m-requirements"></a>Requisiti di NetX LWM2M

Per funzionare correttamente, la libreria di runtime NetX LWM2M richiede che sia già stata creata un'istanza IP NetX. Il pacchetto NetX LWM2M non ha altri requisiti.

## <a name="netx-lwm2m-rfcs"></a>RFC NetX LWM2M

NetX LWM2M è conforme a OMA-TS-LightweightM2M-V1_0-20170208-A e alle RFC seguenti correlate al protocollo CoAP (Constrained Application Protocol):

- **RFC 7252:** Protocollo coAP (Constrained Application Protocol)

- **RFC 7641:** Osservazione delle risorse nel protocollo CoAP (Constrained Application Protocol)

- **RFC 6690:** Constrained RESTful Environments (CoRE) Link Format