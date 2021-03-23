---
title: Capitolo 1-Introduzione al server DHCP di Azure RTO NetX Duo
description: In NetX Duo, l'indirizzo IP dell'applicazione è uno dei parametri specificati per la chiamata al servizio *nx_ip_create* .
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 678b9ed77f07d0b526525c740f0fae7adc6d2c95
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822019"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo-dhcp-server"></a>Capitolo 1-Introduzione al server DHCP di Azure RTO NetX Duo

In NetX Duo, l'indirizzo IP dell'applicazione è uno dei parametri specificati per la chiamata al servizio *nx_ip_create* . La fornitura dell'indirizzo IP non costituisce un problema se l'indirizzo IP è noto all'applicazione, in modo statico o tramite la configurazione dell'utente. Tuttavia, esistono alcuni casi in cui l'applicazione non è in grado di conoscere il proprio indirizzo IP. In tali situazioni, è necessario specificare un indirizzo IP zero per la funzione *nx_ip_create* e l'applicazione stabilisce la comunicazione con il server DHCP per richiedere e ottenere un indirizzo IP in modo dinamico.

## <a name="dynamic-ip-address-assignment"></a>Assegnazione di indirizzi IP dinamici

Il servizio di base usato per ottenere un indirizzo IP dinamico dalla rete è il protocollo RARP (Reverse Address Resolution Protocol). Questo protocollo è simile a ARP, ad eccezione del fatto che è stato progettato per ottenere un indirizzo IP per se stesso anziché per trovare l'indirizzo MAC per un altro nodo di rete. Il messaggio RARP di basso livello viene trasmesso sulla rete locale ed è responsabilità di un server nella rete rispondere con una risposta RARP, che contiene un indirizzo IP allocato dinamicamente.

Sebbene RARP fornisca un servizio per l'allocazione dinamica di indirizzi IP, presenta diversi difetti. Il difetto più evidente è che il RARP fornisce solo l'allocazione dinamica dell'indirizzo IP. Nella maggior parte dei casi, è necessario disporre di altre informazioni per consentire a un dispositivo di partecipare correttamente a una rete. Oltre a un indirizzo IP, per la maggior parte dei dispositivi sono necessari il network mask e l'indirizzo IP del gateway. Potrebbe essere necessario anche l'indirizzo IP di un server DNS e altre informazioni sulla rete. RARP non è in grado di fornire queste informazioni.

## <a name="rarp-alternatives"></a>Alternative RARP

Per ovviare alle carenze di RARP, i ricercatori hanno sviluppato un meccanismo di allocazione indirizzi IP più completo denominato BOOTP (Bootstrap Protocol). Questo protocollo è in grado di allocare dinamicamente un indirizzo IP e di fornire altre informazioni importanti sulla rete. Tuttavia, BOOTP presenta lo svantaggio di essere progettato per le configurazioni di rete statiche. Non consente l'assegnazione di indirizzi rapidi o automatici.

Questo è il punto in cui il Dynamic Host Configuration Protocol (DHCP) è estremamente utile. DHCP è progettato per estendere le funzionalità di base di BOOTP per includere l'allocazione del server IP completamente automatizzata e l'allocazione di indirizzi IP completamente dinamica tramite il "leasing" di un indirizzo IP a un client per un periodo di tempo specificato. DHCP può inoltre essere configurato in modo da allocare gli indirizzi IP in modo statico, ad esempio BOOTP.

## <a name="dhcp-messages"></a>Messaggi DHCP

Sebbene DHCP migliori significativamente la funzionalità di BOOTP, DHCP usa lo stesso formato di messaggio BOOTP e supporta le stesse opzioni del fornitore di BOOTP. Per eseguire la funzione, DHCP introduce sette nuove opzioni specifiche di DHCP, come indicato di seguito:

- DISCOVER (1) (inviato dal client DHCP)
- OFFERTA (2) (inviata dal server DHCP)
- REQUEST (3) (inviato dal client DHCP)
- RIFIUTARE (4) (inviato dal client DHCP)
- ACK (5) (inviato dal server DHCP)
- NACK (6) (inviato dal server DHCP)
- VERSIONE (7) (inviata dal client DHCP)
- INFORMA (8) (inviato dal client DHCP)
- FORCERENEW (9) (inviato dal client DHCP)

## <a name="dhcp-communication"></a>Comunicazione DHCP

Il server DHCP utilizza il protocollo UDP per ricevere le richieste dei client DHCP e trasmettere le risposte. Prima di avere un indirizzo IP, i messaggi UDP che contengono le informazioni DHCP vengono inviati e ricevuti tramite l'indirizzo di trasmissione IP di 255.255.255.255. Tuttavia, se il client conosce l'indirizzo del server DHCP, può inviare messaggi DHCP utilizzando messaggi unicast.

## <a name="dhcp-server-state-machine"></a>Macchina a Stati del server DHCP

Il server DHCP viene implementato come macchina a stati in due passaggi elaborata da un thread DHCP interno creato durante *nx_dhcp_server_create* elaborazione. Lo stato principale del server DHCP è 1) la ricezione di un messaggio di individuazione da un client DHCP e 2) la ricezione di un messaggio di richiesta.

Di seguito sono riportati gli Stati client DHCP corrispondenti:

- **NX_DHCP_STATE_BOOT** A partire da un indirizzo IP precedente
- **NX_DHCP_STATE_INIT** A partire da nessun valore dell'indirizzo IP precedente
- **NX_DHCP_STATE_SELECTING** In attesa di una risposta da un server DHCP
- **NX_DHCP_STATE_REQUESTING** Server DHCP identificato, richiesta indirizzo IP inviata
- **NX_DHCP_STATE_BOUND** Lease indirizzi IP DHCP stabilito
- **NX_DHCP_STATE_RENEWING** Tempo di rinnovo del lease di indirizzi IP DHCP scaduto, rinnovo richiesto
- **NX_DHCP_STATE_REBINDING** Tempo di riassociazione lease indirizzi IP DHCP scaduto, rinnovo richiesto
- **NX_DHCP_STATE_FORCERENEW** Lease degli indirizzi IP DHCP stabilito, forzare il rinnovo del server o dell'applicazione
- **NX_DHCP_STATE_FAILED** Non è stato trovato alcun server o non è stata ricevuta alcuna risposta dal server

## <a name="dhcp-additional-parameters"></a>Parametri aggiuntivi DHCP

Il server DHCP NetX Duo dispone di un elenco predefinito di parametri di opzione impostati nell'opzione configurabile NX_DHCP_DEFAULT_SERVER_OPTION_LIST in *nxd_dhcp_server. h* per fornire ai client DHCP i parametri di configurazione di rete comuni/critici, ad esempio l'indirizzo del router o del gateway e il server DNS per il client DHCP.

## <a name="dhcp-rfcs"></a>RFC DHCP

Il server DHCP NetX Duo è conforme a RFC2132, RFC2131 e RFC correlate.
