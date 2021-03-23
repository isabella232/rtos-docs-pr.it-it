---
title: 'Capitolo 1: introduzione ad Azure RTO NetX Duo MDN/DNS-SD'
description: Azure RTO NetX Duo MDN/DNS-SD aumenta il servizio DNS tradizionale.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b46539ee4d502fa4c90fb3392e25cd3bee40dc5b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821830"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-mdnsdns-sd"></a>Capitolo 1: introduzione ad Azure RTO NetX Duo MDN/DNS-SD

I messaggi MDN e DNS-SD sono protocolli progettati per potenziare il servizio DNS tradizionale. MDN fornisce il nome host e il servizio di ricerca ai nodi della rete locale. Ogni nodo utilizza il canale multicast IPv4 o IPv6 per annunciare i servizi che offre ai propri vicini, risponde alle query dagli elementi adiacenti e invia query sul comportamento delle proprie applicazioni. Per impostazione predefinita, i messaggi MDN operano in un ambiente distribuito, eliminando in tal modo una funzione centralizzata.

DNS-SD si basa su MDN. DNS-SD consente ai nodi di annunciare i servizi forniti alla rete locale o di individuare i servizi offerti da altri nodi nella rete locale. Nel documento il termine *MDN* si riferisce ai servizi che coprono sia la specifica MDN che la specifica DNS-SD.

## <a name="mdns-standard"></a>Standard MDN

L'implementazione di NetX Duo MDN/DNS-SD è conforme alle RFC seguenti:

- RFC 6762: specifica MDN
- RFC 6763: specifica DNS-SD