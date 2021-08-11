---
title: 'Appendice A : Azure RTOS di opzione NetX Duo DHCPv6'
description: Questo capitolo contiene una descrizione di tutti i codici di opzione di NetX Duo DHCPv6
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 58b6e36fab4de02a9fb973894500a48f2656809ec2baa3dfc65fcd80ae33b832
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791829"
---
# <a name="appendix-a--azure-rtos-netx-duo-dhcpv6-option-codes"></a>Appendice A : Azure RTOS di opzione NetX Duo DHCPv6

| Opzione              | Codice            | Descrizione |
| ------------------- | ------------------- | --------------- |
| DUID dell'identificatore client | 1 | Identifica in modo univoco un host client nella rete |
| Identificatore server (DUID) | 2 | Identifica in modo univoco l'host DHCPv6Server nella rete |
| Associazione di identità per indirizzi non temporanei (IANA) | 3 | Parametri per un'assegnazione di indirizzi IP non temporanei |
| Associazione di identità per indirizzi temporanei (IATA) | 4 | Parametri per un'assegnazione di indirizzi IP temporanei |
| Indirizzo IA | 5 | Durata effettiva degli indirizzi IPv6 e IPv6 da assegnare al client |
| Richiesta di opzioni | 6 | Elenco di richieste di informazioni per ottenere informazioni di rete, ad esempio il server DNS e altri parametri di configurazione di rete. |
| Preferenza | 7 | Incluso nel server Annunciare il messaggio al client per influenzare la scelta dei server da parte del client. Il client deve scegliere un server con un valore di preferenza maggiore rispetto ad altri server. 255 è il valore massimo, mentre zero indica che il client può scegliere qualsiasi server che risponde. |
| Tempo trascorso | 8 | Contiene il tempo (in 0,01 secondi) in cui il client avvia lo scambio DHCPv6 con il server. Utilizzato dai server secondari per determinare se il server primario risponde in tempo alla richiesta client. |
| Messaggio di inoltro | 9 | Contiene il messaggio originale nel messaggio di inoltro | 
| Authentication | 11 | Contiene informazioni per autenticare l'identità e il contenuto dei messaggi DHCPv6 |
| Server Unicast | 12 | Il server invia questa opzione per invii al client la conferma che il server accetterà messaggi unicast direttamente dal client anziché dal multicast. |

Le opzioni IATA, Relay Message, Authentication e Server Unicast non sono supportate in questa versione del server NetX Duo DHCPv6. Il codice di opzione del protocollo DHCPv6 corrente 10 non è definito in RFC 3315.