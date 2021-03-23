---
title: Capitolo 2-installazione e utilizzo di MDN
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del modulo MDN NetX Duo.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6f9e3d023f1bdbde4546a94da1bc1ccb48578d0e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821824"
---
# <a name="chapter-2---installation-and-use-of-mdns"></a>Capitolo 2-installazione e utilizzo di MDN

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del modulo MDN NetX Duo.

## <a name="product-distribution"></a>Distribuzione del prodotto

NetX Duo MDN è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nxd_mdns. h** File di intestazione per il modulo MDN NetX Duo
- **nxd_mdns. c** File di origine C per il modulo MDN NetX Duo
- **nxd_mdns.pdf** Descrizione PDF di MDN per NetX Duo
- **demo_netxduo_mdns. c** Semplice programma dimostrativa che illustra i servizi forniti da MDN.

## <a name="netx-duo-mdns-installation"></a>Installazione di NetX Duo MDN

Per usare le API MDN di NetX Duo, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo. Se, ad esempio, NetX Duo è installato nella directory "*c:\netxduo*", il *nxd_mdns. h* e *nxd_mdns. c* devono essere copiati in questa directory.

## <a name="using-netx-duo-mdns"></a>Uso di MDN NetX Duo

L'uso del modulo MDN NetX Duo è facile. In pratica, il codice dell'applicazione deve includere *nxd_mdns. h* dopo aver incluso *tx_api. h e* *nx_api. h*, per poter utilizzare rispettivamente threadX e NETX Duo. Il progetto di compilazione deve includere il codice sorgente MDN e il file dell'applicazione e, naturalmente, i file di libreria ThreadX e NetX. Questo è tutto ciò che è necessario per usare MDN Duo NetX.

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la compilazione del modulo MDN NetX Duo. Vengono elencati i valori predefiniti, ma ogni definizione può essere impostata dall'applicazione prima dell'inclusione del file di intestazione MDN NetX Duo specificato. L'elenco seguente descrive tutti i dettagli:

- **NX_MDNS_DISABLE_SERVER** Disabilita la funzionalità del server MDN/DNS-SD. Senza la funzionalità server, il modulo MDN/DNS-SD non annuncia i servizi forniti dall'host locale né risponde alle richieste MDN. Questo simbolo non è definito per impostazione predefinita.
- **NX_MDNS_DISABLE_CLIENT** Disabilita la funzionalità client MDN/DNS-SD. Senza la funzionalità client, MDN/DNS-SD non invia query né gestisce le risposte di query MDN ricevute in rete.
- **NX_MDNS_ENABLE_ADDRESS_CHECK** Definito, il modulo MDN esegue la convalida degli indirizzi (indirizzo di origine, indirizzo di destinazione e numeri di porta) dai messaggi MDN ricevuti. Questo simbolo è definito per impostazione predefinita.
- **NX_MDNS_ENABLE_CLIENT_POOF** Definito, il modulo MDN esegue l'osservazione passiva degli errori, MDN/DNS_SD client (queryr) osserva le query multicast eseguite dagli altri host nella rete. Questo simbolo è definito per impostazione predefinita.
- **NX_MDNS_ENABLE_SERVER_NEGATIVE_RESPONSES** Definito, il server/DNS-SD MDN (risponditore) genera risposte negative alle query per le quali ha una proprietà legittima. Questo simbolo è definito per impostazione predefinita.
- **NX_MDNS_ENABLE_IPV6** Definito, il messaggio MDN/DNS-SD Invia/Elabora MDN sull'indirizzo IPv6. Questo simbolo non è definito per impostazione predefinita.
- **NX_MDNS_IPV6_ADDRESS_COUNT** Numero massimo di indirizzi IPv6 dell'host. Il valore predefinito è 2.
- **NX_MDNS_HOST_NAME_MAX** Dimensioni massime della stringa per il nome host. Il valore predefinito è 64. Non include il carattere di terminazione NULL.
- **NX_MDNS_SERVICE_NAME_MAX** Dimensioni massime della stringa per il nome del servizio. Il valore predefinito è 64. Non include il carattere di terminazione NULL.
- **NX_MDNS_DOMAIN_NAME_MAX** Dimensioni massime della stringa per il nome di dominio. Il valore predefinito è 16. Non include il carattere di terminazione NULL.
- **NX_MDNS_CONFLICT_COUNT** Numero massimo di conflitti per il nome host o il nome del servizio. Il valore predefinito è 8.
- **NX_MDNS_RR_TTL_HOST** Valore TTL per i record di risorse con nome host, in secondi. Il valore predefinito è 120 per 120S.
- **NX_MDNS_RR_TTL_OTHER** Valore TTL per altri record di risorse, in secondi. Il valore predefinito è 4500 per 75 minuti.
- **NX_MDNS_PROBING_TIMER_COUNT** Intervallo di tempo, in cicli, tra i messaggi di probe MDN. Il valore predefinito è 25 cicli per 250ms.
- **NX_MDNS_ANNOUNCING_TIMER_COUNT** Intervallo di tempo, in cicli, tra i messaggi di annuncio MDN. Il valore predefinito è 25 cicli per 250ms.
- **NX_MDNS_GOODBYE_TIMER_COUNT** Intervallo di tempo, in cicli, tra i messaggi "Goodbye" ripetuti. Il valore predefinito è 25 cicli per 250ms.
- **NX_MDNS_QUERY_MIN_TIMER_COUNT** Intervallo di tempo minimo, in cicli, tra due query. Il valore predefinito è 100 cicli per 1 secondo.
- **NX_MDNS_QUERY_MAX_TIMER_COUNT** Intervallo di tempo massimo, in cicli, tra due query. Il valore predefinito è 360000 per 60 secondi.
- **NX_MDNS_QUERY_DELAY_MIN** Ritardo minimo per l'invio della prima query in cicli. Il valore predefinito è 2 cicli per 20ms.
- **NX_MDNS_QUERY_DELAY_RANGE** Intervallo di ritardo per l'invio della prima query, in cicli. Il valore predefinito è 10 cicli per 100 ms.
- **NX_MDNS_RESPONSE_INTERVAL** Intervallo di tempo, in cicli, che risponde a una query per garantire un intervallo di almeno 1S dall'ultima volta in cui il record è stato multicast. Il valore predefinito è 100 cicli.
- **NX_MDNS_RESPONSE_PROBING_TIMER_OUT** Intervallo di tempo, in cicli, che risponde a una query Probe per garantire un intervallo di almeno 250ms dall'ultima volta in cui il record è stato multicast. Il valore predefinito è 25 cicli.
- **NX_MDNS_RESPONSE_UNIQUE_DELAY** Ritardo, in cicli, per la risposta a una query a un servizio univoco per la rete locale. Il valore predefinito è 1 segno di selezione per 10 ms.
- **NX_MDNS_RESPONSE_SHARED_DELAY_MIN** Ritardo minimo, in cicli, durante la risposta a una query a una risorsa condivisa. Il valore predefinito è 2 cicli per 20ms.
- **NX_MDNS_RESPONSE_SHARED_DELAY_RANGE** Intervallo di ritardo, in cicli, in risposta a una query a una risorsa condivisa. Il valore predefinito è 10 cicli per 100 ms.
- **NX_MDNS_RESPONSE_TC_DELAY_MIN** Ritardo minimo, in cicli, per la risposta a una query con bit TC. Il valore predefinito è 40 cicli per 400ms.
- **NX_MDNS_RESPONSE_TC_DELAY_RANGE** Intervallo di ritardo, in cicli, in risposta a una query con bit TC. Il valore predefinito è 10 cicli per 100 ms.
- **NX_MDNS_TIMER_COUNT_RANGE** Quando si inviano risposte MDN, il pacchetto contiene risposte che altrimenti verrebbero inviate all'interno di questo intervallo del contatore del timer. L'intervallo di conteggio dei timer è espresso in cicli. Il valore predefinito è 12 per 120ms. Questo valore consente a una risposta di includere messaggi che verrebbero inviati entro l'intervallo di 120ms successivo se ogni segno di operazione è 10 ms.
- **NX_MDNS_PROBING_RETRANSMIT_COUNT** Numero di messaggi di sondaggio ritrasmessi. Il valore predefinito è 3.
- **NX_MDNS_GOODBYE_RETRANSMIT_COUNT** Numero di messaggi "Goodbye" ritrasmessi. Il valore predefinito è 1.
- **NX_MDNS_POOF_MIN_COUNT** Il numero di query senza risposta multicast, quindi l'host può indicare che il record potrebbe non essere più valido. Il valore predefinito è 2.
- **NX_MDNS_POOF_TIME_COUNT** Intervallo di tempo, in cicli, durante l'eliminazione del record dalla cache dopo la visualizzazione di due o più di queste query e la mancata visualizzazione di una risposta multicast contenente la risposta prevista. Il valore predefinito è 1000 cicli per 10 secondi.
- **NX_MDNS_RR_DELETE_DELAY_TIMER_COUNT** Il ritardo per l'eliminazione di un record di risorse quando la durata (TTL) del record è zero, in cicli, il valore predefinito è 100 cicli per 1 secondo.
