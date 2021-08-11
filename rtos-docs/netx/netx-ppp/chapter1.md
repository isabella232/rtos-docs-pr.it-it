---
title: Capitolo 1 - Introduzione al Azure RTOS NetX Point-to-Point Protocol (PPP)
description: In genere, le applicazioni NetX si connettono alla rete fisica effettiva tramite Ethernet.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4027d79f80928804a757e5801c74865389ab1d0237510e63348945ebe2b30045
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801972"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-point-to-point-protocol-ppp"></a>Capitolo 1 - Introduzione al Azure RTOS NetX Point-to-Point Protocol (PPP)

In genere, le applicazioni NetX si connettono alla rete fisica effettiva tramite Ethernet. In questo modo, l'accesso alla rete è veloce ed efficiente. Esistono tuttavia situazioni in cui l'applicazione non dispone dell'accesso Ethernet. In questi casi, l'applicazione può comunque connettersi alla rete tramite un'interfaccia seriale connessa direttamente a un altro membro della rete. Il protocollo software più comune usato per gestire tale connessione è Point-to-Point Protocol (PPP).

Anche se la comunicazione seriale è relativamente semplice, il PPP è piuttosto complesso. Il protocollo PPP è costituito in realtà da più protocolli, ad esempio Link Control Protocol (LCP), IPCP (Internet Protocol Control Protocol), Password Authentication Protocol (PAP) e chap (Challenge-Handshake Authentication Protocol). LCP è il protocollo principale per PPP. Qui i componenti di base del collegamento vengono negoziati dinamicamente in modalità peer-to-peer. Dopo che le caratteristiche di base del collegamento sono state negoziate correttamente, vengono usati PAP e/o CHAP per garantire la validità di un peer connesso. Se entrambi i peer sono validi, ipCP viene quindi utilizzato per negoziare gli indirizzi IP usati dai peer. Al termine di IPCP, PPP è in grado di inviare e ricevere pacchetti IP.

NetX visualizza il PPP principalmente come driver di dispositivo. La *nx_ppp_driver* viene fornita alla funzione di creazione ip NetX, *nx_ip_create*. In caso contrario, NetX non ha alcuna conoscenza diretta di PPP.

## <a name="ppp-serial-communication"></a>Comunicazione seriale PPP

Il pacchetto PPP NetX richiede all'applicazione di fornire un driver di comunicazione seriale. Il driver deve supportare caratteri a 8 bit e può anche utilizzare il controllo di flusso software. È responsabilità dell'applicazione inizializzare il driver, operazione che deve essere eseguita prima di creare l'istanza PPP.

Per inviare pacchetti PPP, è necessario fornire una routine di byte di output del driver seriale a PPP (specificata nella *funzione nx_ppp_create* seriale). Questa routine di output dei byte del driver seriale verrà chiamata in modo ripetitivo per trasmettere l'intero pacchetto PPP. È responsabilità del driver seriale eseguire il buffer dell'output. Sul lato ricezione, il driver seriale dell'applicazione deve chiamare la funzione PPP *nx_ppp_byte_receive* ogni volta che arriva un nuovo byte. Questa operazione viene in genere eseguita dall'interno del contesto di un'isr (Interrupt Service Routine). La *nx_ppp_byte_receive* inserisce il byte in ingresso in un buffer circolare e avvisa il thread di ricezione PPP della sua presenza.

## <a name="ppp-over-ethernet-communication"></a>Comunicazione PPP su Ethernet

Il PPP NetX può anche trasmettere un messaggio PPP tramite Ethernet. In questo caso, il pacchetto PPP NetX richiede che l'applicazione fornissi un driver di comunicazione Ethernet.

Per inviare pacchetti PPP tramite Ethernet, è necessario fornire una routine di output a PPP (specificata nella funzione *nx_ppp_packet_send_set.* Questa routine di output verrà chiamata in modo ripetitivo per trasmettere l'intero pacchetto PPP. Sul lato ricezione, il ricevitore dell'applicazione deve chiamare la funzione PPP *nx_ppp_packet_receive* ogni volta che arriva un nuovo pacchetto.

## <a name="ppp-packet"></a>Pacchetto PPP

PPP usa il framing AHDLC (un subset di HDLC) per incapsulare tutti i dati utente e il controllo del protocollo PPP. Un frame AHDLC è simile al seguente:

|**Contrassegno**|**Addr**|**Ctrl**|**Informazioni**|**CRC**|**Contrassegno**|
|--------|--------|--------|---------------|-------|--------|
|7E |FF|03|[0-1502 byte]|2 byte| 7E|

Ogni frame PPP ha questo aspetto complessivo. I primi due byte del campo informazioni contengono il tipo di protocollo PPP. I valori validi sono definiti come segue:

- C021: LCP
- 8021: IPCP
- C023: PAP
- C223: CHAP
- 0021: Pacchetto di dati IP

Se il 0x0021 protocollo è presente, il pacchetto IP segue immediatamente. In caso contrario, se è presente uno degli altri protocolli, i byte seguenti corrispondono al protocollo specifico.

Per garantire valori univoci 0x7E marcatori di frame di inizio/fine e per supportare il controllo di flusso software, AHDLC usa sequenze di escape per rappresentare diversi valori di byte. Il 0x7D valore specifica che il carattere seguente è codificato, che è fondamentalmente il carattere originale esclusivo ORed con 0x20. Ad esempio, il 0x03 per il campo CTRL nell'intestazione è rappresentato dalla sequenza di due byte: 7D 23. Per impostazione predefinita, i valori minori 0x20 vengono convertiti in una sequenza di escape, nonché i valori 0x7E e 0x7D specificati nel campo Informazioni. Si noti che le sequenze di escape si applicano anche al campo CRC.

## <a name="link-control-protocol-lcp"></a>Link Control Protocol (LCP)

LCP è il protocollo PPP primario ed è il primo protocollo da eseguire. LCP è responsabile della negoziazione di vari parametri PPP, tra cui l'unità di ricezione massima (MRU) e il protocollo di autenticazione (PAP, CHAP o nessuno) da utilizzare. Quando entrambi i lati di LCP concordano sui parametri PPP, i protocolli di autenticazione, se presenti, iniziano l'esecuzione.

## <a name="password-authentication-protocol-pap"></a>Password Authentication Protocol (PAP)

PAP è un protocollo relativamente semplice che si basa su un nome e una password forniti da un lato della connessione (come negoziato durante LCP). L'altro lato verifica quindi queste informazioni. Se corretto, viene restituito un messaggio di accettazione al mittente e PPP può quindi passare alla macchina a stati IPCP. In caso contrario, se il nome o la password non è corretta, la connessione viene rifiutata.

>[!NOTE]
> Entrambi i lati dell'interfaccia possono richiedere PAP, ma PAP viene in genere usato in una sola direzione.

## <a name="challenge-handshake-authentication-protocol-chap"></a>Challenge-Handshake Authentication Protocol (CHAP)

CHAP è un protocollo di autenticazione più complesso rispetto a PAP. L'autenticatore CHAP fornisce al peer un nome e un valore. Il peer usa quindi il nome fornito per trovare un "segreto" condiviso tra le due entità. Viene quindi eseguito un calcolo sull'ID, il valore e il "segreto". Il risultato di questo calcolo viene restituito nella risposta. Se corretto, PPP può quindi passare alla macchina a stati IPCP. In caso contrario, se il risultato non è corretto, la connessione viene rifiutata.

Un altro aspetto interessante di CHAP è che può verificarsi a intervalli casuali dopo che è stata stabilita una connessione. Viene usato per impedire l'hijack di una connessione dopo l'autenticazione. Se una richiesta di verifica ha esito negativo in uno di questi momenti casuali, la connessione viene terminata immediatamente.

>[!NOTE]
> Entrambi i lati dell'interfaccia possono richiedere CHAP, ma CHAP viene in genere utilizzato in una sola direzione.

## <a name="internet-protocol-control-protocol-ipcp"></a>IPCP (Internet Protocol Control Protocol)

IPCP è l'ultimo protocollo da eseguire prima che la comunicazione PPP sia disponibile per il trasferimento dei dati IP NetX. Lo scopo principale di questo protocollo è che un peer informi l'altro del relativo indirizzo IP. Dopo la configurazione dell'indirizzo IP, il trasferimento dei dati IP NetX è abilitato.

## <a name="data-transfer"></a>Trasferimento dati

Come accennato in precedenza, i pacchetti di dati IP NetX risiedono in frame PPP con un ID protocollo 0x0021. Tutti i pacchetti di dati ricevuti vengono inseriti in una o più NX_PACKET e trasferiti all'elaborazione di ricezione NetX. Durante la trasmissione, il contenuto del pacchetto NetX viene inserito in un frame AHDLC e trasmesso.

## <a name="ppp-rfcs"></a>RFC PPP

Il protocollo PPP NetX è conforme a RFC1332, RFC1334, RFC1661, RFC1994 e alle RFC correlate.