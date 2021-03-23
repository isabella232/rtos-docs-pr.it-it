---
title: Capitolo 1-Introduzione ad Azure RTO NetX client DHCP
description: In NetX, l'indirizzo IP dell'applicazione è uno dei parametri specificati per la chiamata al servizio nx_ip_create.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 44eb764c84a15a1bc96cf94bcbc8f81be7b41eef
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822709"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-dhcp-client"></a>Capitolo 1-Introduzione ad Azure RTO NetX client DHCP

In NetX, l'indirizzo IP dell'applicazione è uno dei parametri specificati per la chiamata al servizio *nx_ip_create* . La fornitura dell'indirizzo IP non costituisce un problema se l'indirizzo IP è noto all'applicazione, in modo statico o tramite la configurazione dell'utente. Tuttavia, esistono alcuni casi in cui l'applicazione non è in grado di conoscere il proprio indirizzo IP. In tali situazioni, è necessario specificare un indirizzo IP zero per la funzione *nx_ip_create* e usare il protocollo client DHCP di Azure RTO per ottenere dinamicamente un indirizzo IP.

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

DHCP utilizza il protocollo UDP per inviare richieste e risposte di campo. Prima di avere un indirizzo IP, i messaggi UDP che contengono le informazioni DHCP vengono inviati e ricevuti tramite l'indirizzo di trasmissione IP di 255.255.255.255.

## <a name="dhcp-client-state-machine"></a>Macchina a stati client DHCP

Il client DHCP viene implementato come macchina a Stati. La macchina a stati viene elaborata da un thread DHCP interno creato durante *nx_dhcp_create* elaborazione. Gli stati principali del client DHCP sono i seguenti:


- **NX_DHCP_STATE_BOOT** A partire da un indirizzo IP precedente

- **NX_DHCP_STATE_INIT** A partire da nessun valore dell'indirizzo IP precedente

- **NX_DHCP_STATE_SELECTING** In attesa di una risposta da un server DHCP

- **NX_DHCP_STATE_REQUESTING** Server DHCP identificato, richiesta indirizzo IP inviata

- **NX_DHCP_STATE_BOUND** Lease indirizzi IP DHCP stabilito

- **NX_DHCP_STATE_RENEWING** Tempo di rinnovo del lease di indirizzi IP DHCP scaduto, rinnovo richiesto

- **NX_DHCP_STATE_REBINDING** Tempo di riassociazione lease indirizzi IP DHCP scaduto, rinnovo richiesto

- **NX_DHCP_STATE_FORCERENEW** Lease di indirizzi IP DHCP stabilito, forzare il rinnovo dal server (attualmente non supportato) o dall'applicazione che chiama nx_dhcp_force_renew

- **NX_DHCP_STATE_ADDRESS_PROBING** Sondaggio di indirizzi IP DHCP, inviare il probe ARP per rilevare il conflitto di indirizzi IP.

## <a name="dhcp-client-multiple-interface-support"></a>Supporto per più interfacce del client DHCP

Il client DHCP è stato precedentemente implementato per l'esecuzione su una sola interfaccia di rete. Il comportamento predefinito era (ed è ancora) per l'esecuzione del client DHCP sull'interfaccia primaria. Chiamando *nx_dhcp_set_interface_index*, l'applicazione può (e ancora possibile) eseguire DHCP su un'interfaccia di rete secondaria anziché sull'interfaccia primaria.

Supporta ora DHCP in esecuzione su più interfacce in parallelo. Vedere **il client DHCP su più interfacce simultaneamente** nel capitolo due per informazioni dettagliate su come eseguire simultaneamente il client DHCP in più di un'interfaccia fisica.

## <a name="dhcp-user-request"></a>Richiesta utente DHCP

Una volta che il server DHCP concede un indirizzo IP, l'elaborazione del client DHCP può richiedere parametri aggiuntivi, uno alla volta, usando il servizio *nx_dhcp_user_option_request* .

## <a name="dhcp-client-socket-queue"></a>Coda socket client DHCP 

Il client DHCP cancella automaticamente i pacchetti broadcast dai server DHCP destinati ad altri client DHCP dalla coda di ricezione del socket in attesa che il server risponda a se stesso. In una rete occupata, questa operazione potrebbe causare l'eliminazione dei pacchetti destinati al client.

## <a name="dhcp-rfcs"></a>RFC DHCP

NetX DHCP è conforme a RFC2132, RFC2131 e RFC correlati.

