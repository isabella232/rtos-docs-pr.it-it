---
title: Appendice B-codici di stato del server DHCPv6 di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i codici di stato del server DHCPv6 di NetX Duo
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 7c79a0c0bc9acfcfca69c7333d30cd7cab35ba5f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821962"
---
# <a name="appendix-b---azure-rtos-netx-duo-dhcpv6-server-status-codes"></a>Appendice B-codici di stato del server DHCPv6 di Azure RTO NetX Duo

| Nome              | Codice            | Descrizione |
| ------------------- | ------------------- | --------------- |
| Operazione completata | 0 | Operazione completata |
| Errore non specificato | 1 | Errore, motivo non specificato; Questo codice di stato viene impostato dal server per indicare un errore generale durante la concessione della richiesta client non corrispondente agli altri codici |
| Noaddress disponibile | 2 | Il server non dispone di indirizzi disponibili da assegnare al client |
| NoBinding | 3 | L'indirizzo del client IA (Binding) non è disponibile, ad esempio, l'indirizzo IP richiesto non è disponibile per il server per il lease o l'assegnazione a un altro client. |
| NotOnLink | 4 | Il prefisso per l'indirizzo indica che l'indirizzo IP non è un indirizzo di collegamento |
| UseMulticast | 5 | Inviato da un server in risposta alla ricezione di un messaggio client utilizzando l'indirizzo unicast del server anziché l'indirizzo multicast *All_DHCP_Relay_Agents_and_Servers* |