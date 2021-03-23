---
title: Appendice A-codici opzione DHCPv6 di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i codici delle opzioni di NetX Duo DHCPv6
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 36d673c34479ec2d476eeaa094c0dc02714ee010
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821968"
---
# <a name="appendix-a--azure-rtos-netx-duo-dhcpv6-option-codes"></a>Appendice A-codici opzione DHCPv6 di Azure RTO NetX Duo

| Opzione              | Codice            | Descrizione |
| ------------------- | ------------------- | --------------- |
| Identificatore client DUID | 1 | Identifica in modo univoco un host client nella rete |
| Identificatore Server (DUID) | 2 | Identifica in modo univoco l'host DHCPv6Server sulla rete |
| Associazione di identità per indirizzi non temporanei (IANA) | 3 | Parametri per un'assegnazione di indirizzi IP non temporanei |
| Associazione di identità per indirizzi temporanei (IATA) | 4 | Parametri per l'assegnazione di indirizzi IP temporanei |
| Indirizzo IA | 5 | Durata effettiva degli indirizzi IPv6 e degli indirizzi IPv6 da assegnare al client |
| Richiesta di opzione | 6 | Elenco di richieste di informazioni per ottenere informazioni sulla rete, ad esempio server DNS e altri parametri di configurazione di rete. |
| Preferenza | 7 | Incluso nel server annunciare il messaggio al client per influenzare la scelta dei server da parte del client. Il client deve scegliere un server con un valore di preferenza superiore rispetto agli altri server. 255 è il valore massimo, mentre zero indica che il client può scegliere qualsiasi server che risponde |
| Tempo trascorso | 8 | Contiene l'ora, in 0,01 secondi, quando il client avvia lo scambio DHCPv6 con il server. Utilizzato dai server secondari per determinare se il server primario risponde nel tempo alla richiesta del client. |
| Messaggio di inoltro | 9 | Contiene il messaggio originale nel messaggio di inoltro | 
| Authentication | 11 | Contiene informazioni per autenticare l'identità e il contenuto dei messaggi DHCPv6 |
| Unicast del server | 12 | Il server invia questa opzione per informare il client che il server accetterà i messaggi unicast direttamente dal client anziché da multicast. |

Le opzioni IATA, messaggio di inoltro, autenticazione e unicast del server non sono supportate in questa versione di NetX Duo DHCPv6 server. Il codice di opzione corrente del protocollo DHCPv6 10 non è definito nella specifica RFC 3315.