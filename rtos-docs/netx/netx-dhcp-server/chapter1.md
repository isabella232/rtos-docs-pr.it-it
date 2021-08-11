---
title: Capitolo 1 - Introduzione all'Azure RTOS server DHCP NetX
description: L'applicazione stabilisce la comunicazione con il Azure RTOS server DHCP NetX per richiedere dinamicamente e ottenere un indirizzo IP.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f7a286118caf9bca9876d40ecdd176a3f4cb711e9cba39325808bfb6c09c2644
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799558"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-dhcp-server"></a>Capitolo 1 - Introduzione all'Azure RTOS server DHCP NetX

In NetX l'indirizzo IP dell'applicazione è uno dei parametri forniti alla chiamata *nx_ip_create* servizio. Fornire l'indirizzo IP non costituisce un problema se l'indirizzo IP è noto all'applicazione, in modo statico o tramite la configurazione utente. Esistono tuttavia alcuni casi in cui l'applicazione non conosce o non è mittente del relativo indirizzo IP. In tali situazioni, è necessario che alla funzione *nx_ip_create* sia fornito un indirizzo IP pari a zero e l'applicazione stabilirà la comunicazione con il server DHCP Azure RTOS NetX per richiedere e ottenere dinamicamente un indirizzo IP.

## <a name="dynamic-ip-address-assignment"></a>Assegnazione di indirizzi IP dinamici

Il servizio di base usato per ottenere un indirizzo IP dinamico dalla rete è RARP (Reverse Address Resolution Protocol). Questo protocollo è simile a ARP, ad eccezione del fatto che è progettato per ottenere un indirizzo IP per se stesso anziché trovare l'indirizzo MAC per un altro nodo di rete. Il messaggio RARP di basso livello viene trasmesso nella rete locale ed è responsabilità di un server in rete rispondere con una risposta RARP, che contiene un indirizzo IP allocato dinamicamente.

Anche se RARP fornisce un servizio per l'allocazione dinamica degli indirizzi IP, presenta diversi difetti. La più importante è che RARP fornisce solo l'allocazione dinamica dell'indirizzo IP. Nella maggior parte dei casi sono necessarie altre informazioni per consentire a un dispositivo di partecipare correttamente a una rete. Oltre a un indirizzo IP, la maggior parte dei dispositivi deve network mask l'indirizzo IP del gateway. Potrebbero essere necessari anche l'indirizzo IP di un server DNS e altre informazioni di rete. RARP non è in grado di fornire queste informazioni.

## <a name="rarp-alternatives"></a>Alternative RARP

Per superare le difficoltà del protocollo RARP, i ricercatori hanno sviluppato un meccanismo di allocazione degli indirizzi IP più completo denominato protocollo Bootstrap (BOOTP). Questo protocollo è in grado di allocare dinamicamente un indirizzo IP e di fornire anche informazioni importanti sulla rete. BootP presenta tuttavia lo svantaggio di essere progettato per le configurazioni di rete statiche. Non consente l'assegnazione di indirizzi rapida o automatica.

In questo caso il Dynamic Host Configuration Protocol (DHCP) è estremamente utile. DHCP è progettato per estendere le funzionalità di base di BOOTP in modo da includere l'allocazione del server IP completamente automatizzata e l'allocazione di indirizzi IP completamente dinamici tramite il "leasing" di un indirizzo IP a un client per un periodo di tempo specificato. DHCP può anche essere configurato per allocare indirizzi IP in modo statico come BOOTP.

## <a name="dhcp-messages"></a>Messaggi DHCP

Sebbene DHCP migliora notevolmente le funzionalità di BOOTP, DHCP utilizza lo stesso formato di messaggio di BOOTP e supporta le stesse opzioni del fornitore di BOOTP. Per eseguire la funzione, DHCP introduce sette nuove opzioni specifiche di DHCP, come indicato di seguito:

| Opzione     | Valore | Origine                |
| ---------- | ----- | --------------------- |
| Scoprire   | (1)   | (inviato dal client DHCP) |
| Offerta      | (2)   | (inviato dal server DHCP) |
| Richiesta    | (3)   | (inviato dal client DHCP) |
| Declino    | (4)   | (inviato dal client DHCP) |
| ACK        | (5)   | (inviato dal server DHCP) |
| Nack       |  (6)   | (inviato dal server DHCP) |
| RELEASE    | (7)   | (inviato dal client DHCP) |
| Informare     | (8)   | (inviato dal client DHCP) |
| FORCERENEW | (9)   | (inviato dal client DHCP) |

## <a name="dhcp-communication"></a>Comunicazione DHCP

Il server DHCP utilizza il protocollo UDP per ricevere richieste client DHCP e trasmettere risposte. Prima di avere un indirizzo IP, i messaggi UDP che trasportano le informazioni DHCP vengono inviati e ricevuti utilizzando l'indirizzo di trasmissione IP 255.255.255.255. Tuttavia, se il client conosce l'indirizzo del server DHCP, può inviare messaggi DHCP utilizzando messaggi unicast.

## <a name="dhcp-server-state-machine"></a>Macchina a stati del server DHCP

Il server DHCP viene implementato come macchina a stati in due passaggi elaborata da un thread DHCP interno creato durante *l'nx_dhcp_server_create* elaborazione. Gli stati principali del server DHCP sono 1) ricezione di un messaggio DISCOVER da un client DHCP e 2) ricezione di un messaggio REQUEST.

Di seguito sono riportati gli stati client DHCP corrispondenti:

- **NX_DHCP_STATE_BOOT**: a partire da un indirizzo IP precedente
- **NX_DHCP_STATE_INIT**: a partire da nessun valore di indirizzo IP precedente
- **NX_DHCP_STATE_SELECTING**: in attesa di una risposta da qualsiasi server DHCP
- **NX_DHCP_STATE_REQUESTING:** Server DHCP identificato, richiesta indirizzo IP inviata
- **NX_DHCP_STATE_BOUND:** Lease dell'indirizzo IP DHCP stabilito
- **NX_DHCP_STATE_RENEWING:** tempo di rinnovo lease dell'indirizzo IP DHCP trascorso, rinnovo richiesto
- **NX_DHCP_STATE_REBINDING:** tempo di riassociato lease indirizzo IP DHCP trascorso, rinnovo richiesto
- **NX_DHCP_STATE_FORCERENEW:** lease dell'indirizzo IP DHCP stabilito, rinnovo forzato dal server o dall'applicazione
- **NX_DHCP_STATE_FAILED:** non è stato trovato alcun server o non è stata ricevuta alcuna risposta dal server

## <a name="dhcp-additional-parameters"></a>Parametri aggiuntivi DHCP

Il server DHCP NetX dispone di un elenco predefinito di parametri di opzione impostati nell'opzione configurabile NX_DHCP_DEFAULT_SERVER_OPTION_LISTin *nx_dhcp_server.h* per fornire ai client DHCP parametri di configurazione di rete comuni/critici, ad esempio indirizzo router o gateway e server DNS per il client DHCP.

## <a name="dhcp-rfcs"></a>RFC DHCP

Il server DHCP NetX è conforme a RFC2132, RFC2131 e alle RFC correlate.
