---
title: Capitolo 1 - Introduzione al Azure RTOS client PPPoE NetX
description: Questo capitolo contiene i dettagli Azure RTOS modulo PPPoE NetX.
author: philmea
ms.author: philmea
ms.date: 07/13/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 08edb5b332426d4ab5d2f92462438e1cb84245db6c2f6ab2ef72f28eab8a313f
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798911"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pppoe-client"></a>Capitolo 1 - Introduzione al Azure RTOS client PPPoE NetX

PPP su Ethernet (PPPoE) consente agli host di connettersi al server PPP tramite Ethernet anziché la comunicazione linea seriale tradizionale basata su caratteri.  I dettagli tecnici di PPPoE sono descritti in RFC 2516: A Method for Transmitting PPP over Ethernet (PPPoE). Questo documento è in particolare in Azure RTOS modulo PPPoE NetX.

Per fornire una connessione da punto a punto tramite Ethernet, ogni sessione PPP deve apprendere l'indirizzo Ethernet del peer remoto, nonché stabilire un identificatore di sessione univoco.

In base a RFC 2516, PPPoE è costituito da due fasi: la fase di individuazione e la fase sessione PPPoE. Quando un host (client) vuole avviare una sessione PPP, deve prima eseguire l'individuazione per trovare il server PPPoE. Questo passaggio consente inoltre al server e al client di identificare l'altro indirizzo MAC Ethernet e SESSION_ID, che verranno usati per il resto della sessione PPP.

Un frame Ethernet è il seguente:

![Frame Ethernet](media/ethernet-frame.png)

Il payload Ethernet per PPPoE è il seguente:

![Payload Ethernet](media/ethernet-payload.png)

## <a name="pppoe-discovery-stage"></a>Fase di individuazione PPPoE

La fase di individuazione PPPoE consente ai client di selezionare un server da tutti i server disponibili nella rete, in modo efficace per creare una sessione prima dello scambio di frame PPP.  Al termine della fase di individuazione, sia il client che il server devono accettare un ID sessione univoco ed entrambi i lati devono conoscere l'indirizzo MAC del peer.

| Messaggio di individuazione | Codice | Direzione |
| ----------------- | ---- | --------- |
| Avvio dell'individuazione attiva PPPoE (PADI) | 0x09 | Dal client alla trasmissione |
| PpPoe Active Discovery Offer (PADO) | 0x07 | Dal server al client |
| Richiesta di individuazione attiva PPPoE (PADR) | 0x19 | Dal client al server |
| PPPOE Active Discovery Session-confirmation (PADS) | 0x65 | Dal server al client |
| PPPoE Active Discovery Terminate (PADT) | 0xa7 | Può essere avviato da server o client |

Per tutti i frame Ethernet di individuazione il campo ETHER_TYPE impostato sul valore 0x8863.

## <a name="pppoe-session-message"></a>Messaggio di sessione PPPoE

Dopo che il client e il server hanno creato una sessione, i frame PPP possono essere trasferiti come messaggi di sessione PPPoE.  Durante una sessione, il SESSION_ID deve cambiare e deve essere il valore assegnato dal server durante la fase di individuazione.

Per tutti i frame Ethernet di sessione PPPoE il campo ETHER_TYPE impostato sul valore 0x8864.
