---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo Point-to-Point Protocol (PPP)
description: Questo capitolo introduce il modulo Azure RTO NetX Duo Point-to-Point Protocol (PPP).
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f439cf66e6619652ae8ab9097b2de5e584d78c59
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821743"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-duo-point-to-point-protocol-ppp"></a>Capitolo 1-Introduzione ad Azure RTO NetX Duo Point-to-Point Protocol (PPP)

In genere, le applicazioni NetX si connettono alla rete fisica effettiva tramite Ethernet. Questo consente l'accesso alla rete veloce ed efficiente. Tuttavia, esistono situazioni in cui l'applicazione non dispone di accesso Ethernet. In questi casi, l'applicazione potrebbe ancora connettersi alla rete tramite un'interfaccia seriale connessa direttamente a un altro membro di rete. Il protocollo software più comune usato per gestire tale connessione è il Point-to-Point Protocol (PPP).

Sebbene la comunicazione seriale sia relativamente semplice, il PPP è piuttosto complesso. Il PPP è costituito in realtà da più protocolli, ad esempio il protocollo di controllo del collegamento (LCP), il protocollo di controllo del protocollo Internet (protocollo IPCP), il Password Authentication Protocol (PAP) e il protocollo di autenticazione Challenge-Handshake (CHAP). LCP è il protocollo principale per PPP. Questo è il punto in cui i componenti di base del collegamento vengono negoziati dinamicamente in modo peer-to-peer. Una volta che le caratteristiche di base del collegamento sono state negoziate correttamente, vengono usati i PAP e/o CHAP per assicurarsi che un peer connesso sia valido. Se entrambi i peer sono validi, il protocollo IPCP viene quindi utilizzato per negoziare gli indirizzi IP utilizzati dai peer. Al termine dell'esecuzione di protocollo IPCP, PPP sarà in grado di inviare e ricevere pacchetti IP.

NetX Visualizza il PPP principalmente come driver di dispositivo. La funzione *nx_ppp_driver* viene fornita alla funzione di creazione IP di NetX, *nx_ip_create*. In caso contrario, NetX non ha alcuna conoscenza diretta di PPP.

## <a name="ppp-serial-communication"></a>Comunicazione seriale PPP

Per il pacchetto NetX PPP è necessario che l'applicazione fornisca un driver di comunicazione seriale. Il driver deve supportare caratteri a 8 bit e può anche usare il controllo del flusso software. È responsabilità dell'applicazione inizializzare il driver, operazione che deve essere eseguita prima di creare l'istanza di PPP.

Per inviare pacchetti PPP, è necessario fornire una routine di byte di output del driver seriale a PPP (specificato nella funzione *nx_ppp_create* ). Questa routine di output di byte del driver seriale verrà chiamata ripetutamente per trasmettere l'intero pacchetto PPP. È responsabilità del driver seriale memorizzare nel buffer l'output. Sul lato di ricezione, il driver seriale dell'applicazione deve chiamare la funzione *NX_PPP_BYTE_RECEIVE* PPP ogni volta che arriva un nuovo byte. Questa operazione viene in genere eseguita dall'interno del contesto di una routine del servizio di interrupt (ISR). La funzione *nx_ppp_byte_receive* posiziona il byte in ingresso in un buffer circolare e avvisa il thread di ricezione PPP della sua presenza.

## <a name="ppp-over-ethernet-communication"></a>Comunicazione PPP over Ethernet

NetX PPP può anche trasmettere messaggi PPP su Ethernet, in questo caso il pacchetto PPP NetX richiede che l'applicazione fornisca un driver di comunicazione Ethernet.

Per inviare pacchetti PPP su Ethernet, è necessario fornire una routine di output a PPP (specificato nella funzione *nx_ppp_packet_send_set* ). Questa routine di output verrà chiamata ripetutamente per trasmettere l'intero pacchetto PPP. Sul lato di ricezione, il destinatario dell'applicazione deve chiamare la funzione *NX_PPP_PACKET_RECEIVE* PPP ogni volta che arriva un nuovo pacchetto.

## <a name="ppp-packet"></a>Pacchetto PPP

PPP usa il framing AHDLC (un subset di HDLC) per incapsulare tutti i dati utente e il controllo del protocollo PPP. Un frame AHDLC ha un aspetto simile al seguente:

|**Contrassegno**|**Addr**|**CTRL**|**Informazioni**|**CRC**|**Contrassegno**|
|--------|--------|--------|---------------|-------|--------|
|7E |FF|03|[0-1502 byte]|2 byte| 7E|

Ogni frame PPP presenta questo aspetto generale. I primi due byte del campo informazioni contengono il tipo di protocollo PPP. I valori validi sono definiti nel modo seguente:

- C021: LCP
- 8021: PROTOCOLLO IPCP
- C023: PAP
- C223: CHAP
- 0021: pacchetto di dati IP

Se il tipo di protocollo 0x0021 è presente, il pacchetto IP segue immediatamente. In caso contrario, se è presente uno degli altri protocolli, i byte seguenti corrispondono a quel particolare protocollo.

Per garantire che i marcatori di frame iniziali/finali 0x7E univoci e supportino il controllo del flusso software, AHDLC usa le sequenze di escape per rappresentare i diversi valori di byte. Il valore 0x7D specifica che il carattere seguente è codificato, che è fondamentalmente il carattere originale esclusivo ORed con 0x20. Ad esempio, il valore 0x03 per il campo Ctrl nell'intestazione è rappresentato dalla sequenza a due byte: 7D 23. Per impostazione predefinita, i valori minori di 0x20 vengono convertiti in una sequenza di escape, oltre ai valori 0x7E e 0x7D trovati nel campo Information. Si noti che le sequenze di escape si applicano anche al campo CRC.

## <a name="link-control-protocol-lcp"></a>Protocollo di controllo del collegamento (LCP)

LCP è il protocollo PPP primario ed è il primo protocollo da eseguire. LCP è responsabile della negoziazione di diversi parametri PPP, tra cui l'unità di ricezione massima (MRU) e il protocollo di autenticazione (PAP, CHAP o None) da usare. Quando entrambi i lati di LCP accettano i parametri PPP, i protocolli di autenticazione, se disponibili, avviano l'esecuzione.

## <a name="password-authentication-protocol-pap"></a>Password Authentication Protocol (PAP)

Il PAP è un protocollo relativamente semplice che si basa su un nome e una password forniti da un lato della connessione (come negoziato durante l'LCP). L'altro lato verifica quindi queste informazioni. Se il valore è corretto, al mittente viene restituito un messaggio di accettazione e PPP può procedere alla macchina a stati protocollo IPCP. In caso contrario, se il nome o la password non è corretta, la connessione viene rifiutata.

>[!NOTE]
> Entrambi i lati dell'interfaccia possono richiedere un PAP, ma il PAP viene in genere usato in una sola direzione.

## <a name="challenge-handshake-authentication-protocol-chap"></a>Protocollo CHAP (Challenge-Handshake Authentication Protocol)

Il protocollo CHAP è un protocollo di autenticazione più complesso rispetto a PAP. L'autenticatore CHAP fornisce il proprio peer con un nome e un valore. Il peer usa quindi il nome fornito per trovare un "segreto" condiviso tra le due entità. Un calcolo viene quindi eseguito tramite l'ID, il valore e il "segreto". Il risultato di questo calcolo viene restituito nella risposta. Se è corretto, PPP può procedere alla macchina a stati protocollo IPCP. In caso contrario, se il risultato non è corretto, la connessione viene rifiutata.

Un altro aspetto interessante di CHAP è che può verificarsi a intervalli casuali dopo che è stata stabilita una connessione. Viene usato per impedire il Hijack di una connessione, dopo che è stata autenticata. Se una richiesta di verifica ha esito negativo a una di queste ore casuali, la connessione viene immediatamente terminata.

>[!NOTE]
> Entrambi i lati dell'interfaccia possono richiedere l'autenticazione CHAP, ma CHAP viene in genere usato in una sola direzione.

## <a name="internet-protocol-control-protocol-ipcp"></a>Internet Protocol Control Protocol (protocollo IPCP)

PROTOCOLLO IPCP è l'ultimo protocollo da eseguire prima che la comunicazione PPP sia disponibile per il trasferimento di dati IP di NetX. Lo scopo principale di questo protocollo è che un peer comunichi l'altro indirizzo IP. Quando l'indirizzo IP è configurato, il trasferimento dei dati IP di NetX è abilitato.

## <a name="data-transfer"></a>Trasferimento dati

Come indicato in precedenza, i pacchetti di dati IP NetX si trovano in frame PPP con ID protocollo 0x0021. Tutti i pacchetti di dati ricevuti vengono inseriti in una o più strutture di NX_PACKET e trasferiti all'elaborazione di ricezione NetX. In trasmissione, il contenuto del pacchetto NetX viene inserito in un frame AHDLC e trasmesso.

## <a name="ppp-rfcs"></a>RFC per PPP

Il PPP NetX è conforme a RFC1332, RFC1334, RFC1661, RFC1994 e alle RFC correlate.