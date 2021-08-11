---
title: Appendice B - Azure RTOS di stato del server NetX Duo DHCPv6
description: Questo capitolo contiene una descrizione di tutti i codici di stato del server NetX Duo DHCPv6
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8b9795607c0fed80646ee01e36edf4ecd2aaadad7f0a023e6979e123b81e1660
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791772"
---
# <a name="appendix-b---azure-rtos-netx-duo-dhcpv6-server-status-codes"></a>Appendice B - Azure RTOS di stato del server NetX Duo DHCPv6

| Nome              | Codice            | Descrizione |
| ------------------- | ------------------- | --------------- |
| Operazione completata | 0 | Operazione completata |
| Errore non specificato | 1 | Errore, motivo non specificato; Questo codice di stato viene impostato dal server per indicare un errore generale nella concessione della richiesta client che non corrisponde agli altri codici |
| NoAddress disponibile | 2 | Il server non ha indirizzi disponibili per l'assegnazione al client |
| NoBinding | 3 | L'indirizzo IA client (binding) non è disponibile, ad esempio l'indirizzo IP richiesto non è disponibile per il server per il lease o assegnato a un altro client. |
| NotOnLink | 4 | Il prefisso per l'indirizzo indica che l'indirizzo IP non è un indirizzo di collegamento |
| UseMulticast | 5 | Inviato da un server in risposta alla ricezione di un messaggio client usando l'indirizzo unicast del server *anziché l'All_DHCP_Relay_Agents_and_Servers* multicast |