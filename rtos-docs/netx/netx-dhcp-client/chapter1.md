---
title: Capitolo 1 - Introduzione al client DHCP NetX Azure RTOS
description: In NetX l'indirizzo IP dell'applicazione è uno dei parametri forniti per la chiamata nx_ip_create servizio.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 54853fd3677b8d60b7fbe1445ca67c7e7a4a6e832683f65cbfca86158cb7fbd3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116788810"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-dhcp-client"></a>Capitolo 1 - Introduzione al client DHCP NetX Azure RTOS

In NetX l'indirizzo IP dell'applicazione è uno dei parametri forniti per la chiamata nx_ip_create *servizio.* La fornitura dell'indirizzo IP non comporta alcun problema se l'indirizzo IP è noto all'applicazione, in modo statico o tramite la configurazione utente. Esistono tuttavia alcuni casi in cui l'applicazione non conosce o non si preoccupa dell'indirizzo IP. In questi casi, è necessario che alla funzione *nx_ip_create* sia specificato zero indirizzo IP e che il protocollo client DHCP Azure RTOS sia usato per ottenere dinamicamente un indirizzo IP.

## <a name="dynamic-ip-address-assignment"></a>Assegnazione di indirizzi IP dinamici

Il servizio di base usato per ottenere un indirizzo IP dinamico dalla rete è il protocollo RARP (Reverse Address Resolution Protocol). Questo protocollo è simile a ARP, ma è progettato per ottenere un indirizzo IP per se stesso anziché trovare l'indirizzo MAC per un altro nodo di rete. Il messaggio RARP di basso livello viene trasmesso nella rete locale ed è responsabilità di un server nella rete rispondere con una risposta RARP, che contiene un indirizzo IP allocato dinamicamente.

Sebbene RARP ofni un servizio per l'allocazione dinamica degli indirizzi IP, presenta diverse lacune. La mancanza più importante è che RARP fornisce solo l'allocazione dinamica dell'indirizzo IP. Nella maggior parte dei casi, sono necessarie altre informazioni per consentire a un dispositivo di partecipare correttamente a una rete. Oltre a un indirizzo IP, la maggior parte dei dispositivi network mask l'indirizzo IP del gateway. Potrebbe essere necessario anche l'indirizzo IP di un server DNS e altre informazioni di rete. RARP non ha la possibilità di fornire queste informazioni.

## <a name="rarp-alternatives"></a>Alternative RARP

Per superare le carenze di RARP, i ricercatori hanno sviluppato un meccanismo di allocazione degli indirizzi IP più completo denominato protocollo Bootstrap (BOOTP). Questo protocollo ha la possibilità di allocare dinamicamente un indirizzo IP e fornire anche informazioni di rete importanti aggiuntive. BootP presenta tuttavia lo svantaggio di essere progettato per le configurazioni di rete statiche. Non consente l'assegnazione rapida o automatica degli indirizzi.

In questo caso il Dynamic Host Configuration Protocol (DHCP) è estremamente utile. DHCP è progettato per estendere le funzionalità di base di BOOTP per includere l'allocazione del server IP completamente automatizzata e l'allocazione di indirizzi IP completamente dinamici tramite il "leasing" di un indirizzo IP a un client per un periodo di tempo specificato. È anche possibile configurare DHCP per allocare indirizzi IP in modo statico, ad esempio BOOTP.

## <a name="dhcp-messages"></a>Messaggi DHCP

Anche se DHCP migliora notevolmente le funzionalità di BOOTP, DHCP usa lo stesso formato di messaggio di BOOTP e supporta le stesse opzioni del fornitore di BOOTP. Per eseguire la funzione, DHCP introduce sette nuove opzioni specifiche di DHCP, come indicato di seguito:

- DISCOVER (1) (inviato dal client DHCP)

- OFFER (2) (inviato dal server DHCP)

- REQUEST (3) (inviato dal client DHCP)

- DECLINE (4) (inviato dal client DHCP)

- ACK (5) (inviato dal server DHCP)

- NACK (6) (inviato dal server DHCP)

- RELEASE (7) (inviato dal client DHCP)

- INFORM (8) (inviato dal client DHCP)

- FORCERENEW (9) (inviato dal client DHCP)

## <a name="dhcp-communication"></a>Comunicazione DHCP

DHCP usa il protocollo UDP per inviare richieste e risposte sul campo. Prima di avere un indirizzo IP, i messaggi UDP che trasportano le informazioni DHCP vengono inviati e ricevuti usando l'indirizzo di trasmissione IP 255.255.255.255.

## <a name="dhcp-client-state-machine"></a>Computer a stati client DHCP

Il client DHCP viene implementato come macchina a stati. La macchina a stati viene elaborata da un thread DHCP interno creato durante *l nx_dhcp_create* di elaborazione. Gli stati principali del client DHCP sono i seguenti:


- **NX_DHCP_STATE_BOOT** A partire da un indirizzo IP precedente

- **NX_DHCP_STATE_INIT** A partire da nessun valore di indirizzo IP precedente

- **NX_DHCP_STATE_SELECTING** In attesa di una risposta da qualsiasi server DHCP

- **NX_DHCP_STATE_REQUESTING** Server DHCP identificato, richiesta di indirizzo IP inviata

- **NX_DHCP_STATE_BOUND** Lease dell'indirizzo IP DHCP stabilito

- **NX_DHCP_STATE_RENEWING** Tempo di rinnovo lease indirizzo IP DHCP trascorso, rinnovo richiesto

- **NX_DHCP_STATE_REBINDING** Tempo di riassociato lease indirizzo IP DHCP trascorso, rinnovo richiesto

- **NX_DHCP_STATE_FORCERENEW** Lease dell'indirizzo IP DHCP stabilito, rinnovo forzato dal server (attualmente non supportato) o dall'applicazione che nx_dhcp_force_renew

- **NX_DHCP_STATE_ADDRESS_PROBING** Probe dell'indirizzo IP DHCP, inviare il probe ARP per rilevare il conflitto di indirizzi IP.

## <a name="dhcp-client-multiple-interface-support"></a>Supporto di più interfacce client DHCP

Il client DHCP è stato precedentemente implementato per l'esecuzione in una sola interfaccia di rete. Il comportamento predefinito era (e lo è ancora) per l'esecuzione del client DHCP nell'interfaccia primaria. Chiamando *nx_dhcp_set_interface_index*, l'applicazione potrebbe (e comunque può) eseguire DHCP su un'interfaccia di rete secondaria anziché sull'interfaccia primaria.

Supporta ora DHCP in esecuzione su più interfacce in parallelo. Per **informazioni dettagliate** specifiche su come eseguire il client DHCP in più interfacce fisiche contemporaneamente, vedere Client DHCP su più interfacce contemporaneamente nel capitolo 2.

## <a name="dhcp-user-request"></a>Richiesta utente DHCP

Dopo che il server DHCP ha concesso un indirizzo IP, l'elaborazione del client DHCP può richiedere parametri aggiuntivi, uno alla volta, usando il *nx_dhcp_user_option_request* servizio.

## <a name="dhcp-client-socket-queue"></a>Coda socket client DHCP 

Il client DHCP cancella automaticamente i pacchetti broadcast dai server DHCP destinati ad altri client DHCP dalla coda di ricezione socket durante l'attesa che il server risponda a se stesso. In una rete occupata non è possibile eliminare i pacchetti destinati al client.

## <a name="dhcp-rfcs"></a>RFC DHCP

NetX DHCP è conforme a RFC2132, RFC2131 e alle RFC correlate.

