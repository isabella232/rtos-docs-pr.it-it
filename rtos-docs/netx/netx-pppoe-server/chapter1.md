---
title: Capitolo 1 - Introduzione a Azure RTOS NetX PPPoE Server
description: Questo documento è in particolare sui dettagli Azure RTOS modulo PPPoE NetX.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2f79cba35991555f7f8d10e589aa251387ce25c48c3b729da371b548f13321bd
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116798316"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pppoe-server"></a>Capitolo 1 - Introduzione a Azure RTOS NetX PPPoE Server

PPP su Ethernet (PPPoE) consente agli host di connettersi al server PPP tramite Ethernet invece della tradizionale comunicazione seriale basata su caratteri. I dettagli tecnici di PPPoE sono descritti in RFC 2516: A Method for Transmitting PPP over Ethernet (PPPoE). Questo documento è in particolare sui dettagli Azure RTOS modulo PPPoE NetX.

Per fornire una connessione da punto a punto tramite Ethernet, ogni sessione PPP deve conoscere l'indirizzo Ethernet del peer remoto, nonché stabilire un identificatore di sessione univoco.

In base a RFC 2516, PPPoE è costituito da due fasi: la fase di individuazione e la fase della sessione PPPoE. Quando un host (client) vuole avviare una sessione PPP, deve prima eseguire l'individuazione per trovare il server PPPoE. Questo passaggio consente inoltre al server e al client di identificare l'indirizzo MAC Ethernet e il SESSION_ID, che verranno usati per il resto della sessione PPP.

Un frame Ethernet è il seguente:

![Diagramma che mostra un frame Ethernet.](media/netx-pppoe-server-01.png)

Il payload Ethernet per PPPoE è il seguente:

![Diagramma che mostra un payload Ethernet per PPPoE.](media/netx-pppoe-server-02.png)

## <a name="pppoe-discovery-stage"></a>Fase di individuazione PPPoE

La fase di individuazione PPPoE consente ai client di selezionare un server da tutti i server disponibili nella rete, in modo efficace per creare una sessione prima dello scambio di frame PPP. Al termine della fase di individuazione, sia il client che il server devono concordare un ID di sessione univoco ed entrambi i lati devono conoscere l'indirizzo MAC del peer.

| Messaggio di individuazione                                  | Codice | Direzione                                     |
| -------------------------------------------------- | ---- | --------------------------------------------- |
| PPPoE Active Discovery Initiation (PADI)           | 0x09 | Dal client alla trasmissione                      |
| PPPoE Active Discovery Offer (PADO)                | 0x07 | Dal server al client                         |
| RICHIESTA DI INDIVIDUAZIONE ATTIVA PPPoE (PADR)              | 0x19 | Da client a server                         |
| Conferma della sessione di individuazione attiva PPPOE (PADS) | 0x65 | Dal server al client                         |
| PPPoE Active Discovery Terminate (PADT)            | 0xa7 | Può essere avviato da server o client |

Per tutti i frame Discovery Ethernet il campo ETHER_TYPE impostato sul valore 0x8863.

## <a name="pppoe-session-message"></a>Messaggio di sessione PPPoE

Dopo che il client e il server hanno creato una sessione, i frame PPP possono essere trasferiti come messaggi di sessione PPPoE. Durante una sessione, il SESSION_ID non deve cambiare e deve essere il valore assegnato dal server durante la fase di individuazione.

Per tutti i frame PPPoE Session Ethernet il campo ETHER_TYPE impostato sul valore 0x8864.