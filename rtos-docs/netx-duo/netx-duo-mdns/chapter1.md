---
title: Capitolo 1 - Introduzione a Azure RTOS NetX Duo mDNS/DNS-SD
description: Azure RTOS NetX Duo mDNS/DNS-SD amplia il servizio DNS tradizionale.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7cde8e81809dcc74ee5d0b09d8e7a8d2ae96850cd84250a5bf003fdd5763925a
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796447"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-mdnsdns-sd"></a>Capitolo 1 - Introduzione a Azure RTOS NetX Duo mDNS/DNS-SD

MDNS e DNS-SD sono protocolli progettati per aumentare il servizio DNS tradizionale. mDNS fornisce la ricerca del nome host e del servizio ai nodi nella rete locale. Ogni nodo usa il canale multicast IPv4 o IPv6 per annunciare i servizi che offre agli elementi adiacenti, risponde alle query dagli elementi adiacenti e invia query sul comportamento delle applicazioni. Per impostazione predefinita, mDNS opera in un ambiente distribuito, eliminando così un servizio centralizzato.

DNS-SD si basa su mDNS. DNS-SD consente ai nodi di annunciare i servizi forniti alla rete locale o di individuare i servizi offerti da altri nodi nella rete locale. In tutto il documento, il termine *mDNS* si riferisce ai servizi che coprono sia la specifica mDNS che la specifica DNS-SD.

## <a name="mdns-standard"></a>mDNS Standard

L'implementazione di mDNS/DNS-SD di NetX Duo è conforme alle RFC seguenti:

- RFC 6762: specifica mDNS
- RFC 6763: Specifica DNS-SD