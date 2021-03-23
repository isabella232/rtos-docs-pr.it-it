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
# <a name="chapter-1---introduction-to-azure-rtos-netx-lwm2m"></a>Capitolo 1-Introduzione ad Azure RTO NetX LWM2M

Il protocollo LWM2M di Azure RTO NetX implementa la parte client del computer leggero con il protocollo machine standard.

## <a name="netx-lwm2m-requirements"></a>Requisiti LWM2M di NetX

Per funzionare correttamente, la libreria di runtime NetX LWM2M richiede che sia già stata creata un'istanza IP NetX. Il pacchetto LWM2M NetX non ha altri requisiti.

## <a name="netx-lwm2m-rfcs"></a>RFC NetX LWM2M

LWM2M NetX è conforme a OMA-TS-LightweightM2M-V1_0 -20170208-A e ai seguenti RFC correlati al protocollo applicativo vincolato (CoAP):

- **RFC 7252**: protocollo applicativo vincolato (CoAP)

- **RFC 7641**: osservazione delle risorse nel protocollo applicativo vincolato (CoAP)

- **RFC 6690**: formato di collegamento ambienti RESTful con vincoli (Core)