---
title: Capitolo 1-Introduzione al server PPPoE NetX di Azure RTO
description: Questo documento è incentrato sui dettagli del modulo PPPoE NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 85a762f669e31c7e753f78b270ced15677a87c4c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822514"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-pppoe-server"></a>Capitolo 1-Introduzione al server PPPoE NetX di Azure RTO

PPP over Ethernet (PPPoE) consente agli host di connettersi al server PPP tramite Ethernet invece della tradizionale comunicazione della linea seriale basata su caratteri. I dettagli tecnici di PPPoE sono descritti in RFC 2516: un metodo per la trasmissione di PPP over Ethernet (PPPoE). Questo documento è incentrato sui dettagli del modulo PPPoE NetX di Azure RTO.

Per fornire una connessione Point-to-Point su Ethernet, ogni sessione PPP deve apprendere l'indirizzo Ethernet del peer remoto, nonché stabilire un identificatore di sessione univoco.

In base allo standard RFC 2516, PPPoE è costituito da due fasi: la fase di individuazione e la fase della sessione PPPoE. Quando un host (client) desidera avviare una sessione PPP, deve prima eseguire l'individuazione per trovare il server PPPoE. Questo passaggio consente inoltre al server e al client di identificare gli indirizzi MAC Ethernet e SESSION_ID, che verranno usati per il resto della sessione PPP.

Un frame Ethernet è il seguente:

![Diagramma che mostra un frame Ethernet.](media/netx-pppoe-server-01.png)

Il payload Ethernet per PPPoE è il seguente:

![Diagramma che mostra un payload Ethernet per PPPoE.](media/netx-pppoe-server-02.png)

## <a name="pppoe-discovery-stage"></a>Fase di individuazione PPPoE

La fase di individuazione PPPoE consente ai client di selezionare un server da tutti i server disponibili sulla rete, in modo da creare una sessione prima di scambiare i frame PPP. Al termine della fase di individuazione, sia il client che il server devono accettare un ID di sessione univoco ed entrambi i lati devono essere a conoscenza dell'indirizzo MAC del peer.

| Messaggio di individuazione                                  | Codice | Direzione                                     |
| -------------------------------------------------- | ---- | --------------------------------------------- |
| Avvio di individuazione attiva PPPoE (PADI)           | 0x09 | Da client a broadcast                      |
| Offerta di individuazione attiva PPPoE (PADO)                | 0x07 | Da server a client                         |
| Richiesta di individuazione attiva PPPoE (PADR)              | 0x19 | Da client a server                         |
| Sessione di individuazione attiva PPPOE-conferma (rilievi) | 0x65 | Da server a client                         |
| Termina individuazione attiva PPPoE (PADT)            | 0xa7 | Può essere avviato dal server o dal client |

Tutti i frame Ethernet di individuazione hanno il campo ETHER_TYPE impostato sul valore 0x8863.

## <a name="pppoe-session-message"></a>Messaggio di sessione PPPoE

Dopo che il client e il server hanno creato una sessione, i frame PPP possono essere trasferiti come messaggi di sessione PPPoE. Durante una sessione, il SESSION_ID non deve cambiare e deve essere il valore assegnato dal server durante la fase di individuazione.

Tutti i frame Ethernet della sessione PPPoE hanno il campo ETHER_TYPE impostato sul valore 0x8864.