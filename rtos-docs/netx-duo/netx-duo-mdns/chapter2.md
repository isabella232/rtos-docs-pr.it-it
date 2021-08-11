---
title: Capitolo 2 - Installazione e uso di mDNS
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del modulo mDNS di NetX Duo.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b27671f82c100db4e6a70a568e8a68f14b3ab45e3a33f46dd1f2e1852010f500
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796430"
---
# <a name="chapter-2---installation-and-use-of-mdns"></a>Capitolo 2 - Installazione e uso di mDNS

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'uso del modulo mDNS di NetX Duo.

## <a name="product-distribution"></a>Distribuzione del prodotto

NetX Duo mDNS è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nxd_mdns.h** File di intestazione per il modulo mDNS di NetX Duo
- **nxd_mdns.c** File di origine C per il modulo mDNS di NetX Duo
- **nxd_mdns.pdf** Descrizione PDF di mDNS per NetX Duo
- **demo_netxduo_mdns.c** Semplice programma dimostrativo che illustra i servizi forniti da mDNS.

## <a name="netx-duo-mdns-installation"></a>Installazione di NetX Duo mDNS

Per usare le API mDNS di NetX Duo, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo. Ad esempio, se NetX Duo è installato nella directory "*c:\netxduo*", i file *nxd_mdns.h* e *nxd_mdns.c* devono essere copiati in questa directory.

## <a name="using-netx-duo-mdns"></a>Uso di NetX Duo mDNS

L'uso del modulo mDNS di NetX Duo è semplice. In pratica, il codice dell'applicazione deve includere *nxd_mdns.h* dopo aver incluso *tx_api.h* e *nx_api.h*, per poter usare rispettivamente ThreadX e NetX Duo. Il progetto di compilazione deve includere il codice sorgente mDNS e il file dell'applicazione e, naturalmente, i file della libreria ThreadX e NetX. Questo è tutto ciò che è necessario per usare mDNS di NetX Duo.

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la creazione del modulo mDNS di NetX Duo. Vengono elencati i valori predefiniti, ma ogni definizione può essere impostata dall'applicazione prima dell'inclusione del file di intestazione mDNS di NetX Duo specificato. L'elenco seguente descrive ogni elemento in dettaglio:

- **NX_MDNS_DISABLE_SERVER** Disabilita la funzionalità del server mDNS/DNS-SD. Senza la funzionalità del server, il modulo mDNS/DNS-SD non annuncia i servizi forniti dall'host locale né risponde alle richieste mDNS. Questo simbolo non è definito per impostazione predefinita.
- **NX_MDNS_DISABLE_CLIENT** Disabilita la funzionalità del client mDNS/DNS-SD. Senza la funzionalità client, mDNS/DNS-SD non invia query né mantiene le risposte alle query mDNS ricevute in rete.
- **NX_MDNS_ENABLE_ADDRESS_CHECK** Definito, il modulo mDNS esegue la convalida degli indirizzi (indirizzo di origine, indirizzo di destinazione e numeri di porta) dai messaggi mDNS ricevuti. Questo simbolo è definito per impostazione predefinita.
- **NX_MDNS_ENABLE_CLIENT_POOF** Definito, il modulo mDNS esegue l'osservazione passiva degli errori, il client mDNS /DNS_SD (query) osserva le query multicast eseguite dagli altri host nella rete. Questo simbolo è definito per impostazione predefinita.
- **NX_MDNS_ENABLE_SERVER_NEGATIVE_RESPONSES** Definito, il server mDNS /DNS-SD (risponditore) genera risposte negative alle query per cui ha la proprietà legittima. Questo simbolo è definito per impostazione predefinita.
- **NX_MDNS_ENABLE_IPV6** Definito, il messaggio mDNS/DNS-SD send/process mDNS sull'indirizzo IPv6. Questo simbolo non è definito per impostazione predefinita.
- **NX_MDNS_IPV6_ADDRESS_COUNT** Numero massimo di indirizzi IPv6 dell'host. Il valore predefinito è 2.
- **NX_MDNS_HOST_NAME_MAX** Dimensioni massime della stringa per il nome host. Il valore predefinito è 64. Non include il carattere di terminazione NULL.
- **NX_MDNS_SERVICE_NAME_MAX** Dimensioni massime della stringa per il nome del servizio. Il valore predefinito è 64. Non include il carattere di terminazione NULL.
- **NX_MDNS_DOMAIN_NAME_MAX** Dimensioni massime della stringa per il nome di dominio. Il valore predefinito è 16. Non include il carattere di terminazione NULL.
- **NX_MDNS_CONFLICT_COUNT** Numero massimo di conflitti per il nome host o il nome del servizio. Il valore predefinito è 8.
- **NX_MDNS_RR_TTL_HOST** Valore TTL per i record di risorse con nome host, in secondi. Il valore predefinito è 120 per 120s.
- **NX_MDNS_RR_TTL_OTHER** Valore TTL per altri record di risorse, in secondi. Il valore predefinito è 4500 per 75 minuti.
- **NX_MDNS_PROBING_TIMER_COUNT** Intervallo di tempo, in tick, tra i messaggi di probe mDNS. Il valore predefinito è 25 tick per 250 ms.
- **NX_MDNS_ANNOUNCING_TIMER_COUNT** Intervallo di tempo, in tick, tra i messaggi di annuncio mDNS. Il valore predefinito è 25 tick per 250 ms.
- **NX_MDNS_GOODBYE_TIMER_COUNT** Intervallo di tempo, in tick, tra i messaggi "goodbye" ripetuti. Il valore predefinito è 25 tick per 250 ms.
- **NX_MDNS_QUERY_MIN_TIMER_COUNT** Intervallo di tempo minimo, in tick, tra due query. Il valore predefinito è 100 tick per 1 secondo.
- **NX_MDNS_QUERY_MAX_TIMER_COUNT** Intervallo di tempo massimo, in tick, tra due query. Il valore predefinito è 360000 per 60 secondi.
- **NX_MDNS_QUERY_DELAY_MIN** Ritardo minimo per l'invio della prima query, in tick. Il valore predefinito è 2 tick per 20 ms.
- **NX_MDNS_QUERY_DELAY_RANGE** Intervallo di ritardo per l'invio della prima query, in tick. Il valore predefinito è 10 tick per 100 ms.
- **NX_MDNS_RESPONSE_INTERVAL** Intervallo di tempo, in tick, nella risposta a una query per garantire un intervallo di almeno 1 secondi dall'ultima volta in cui il record è stato multicast. Il valore predefinito è 100 tick.
- **NX_MDNS_RESPONSE_PROBING_TIMER_OUT** Intervallo di tempo, in tick, nella risposta a una query probe per garantire un intervallo di almeno 250 ms dall'ultima volta in cui il record è stato multicast. Il valore predefinito è 25 tick.
- **NX_MDNS_RESPONSE_UNIQUE_DELAY** Ritardo, in tick, nella risposta a una query a un servizio univoco per la rete locale. Il valore predefinito è 1 tick per 10 ms.
- **NX_MDNS_RESPONSE_SHARED_DELAY_MIN** Ritardo minimo, in tick, nella risposta a una query a una risorsa condivisa. Il valore predefinito è 2 tick per 20 ms.
- **NX_MDNS_RESPONSE_SHARED_DELAY_RANGE** Intervallo di ritardo, in tick, nella risposta a una query a una risorsa condivisa. Il valore predefinito è 10 tick per 100 ms.
- **NX_MDNS_RESPONSE_TC_DELAY_MIN** Ritardo minimo, in tick, nella risposta a una query con bit TC. Il valore predefinito è 40 tick per 400 ms.
- **NX_MDNS_RESPONSE_TC_DELAY_RANGE** Intervallo di ritardo, in tick, nella risposta a una query con bit TC. Il valore predefinito è 10 tick per 100 ms.
- **NX_MDNS_TIMER_COUNT_RANGE** Quando si inviano risposte mDNS, il pacchetto contiene risposte che altrimenti verrebbero inviate entro questo intervallo di contatori timer. L'intervallo di conteggio timer è espresso in tick. Il valore predefinito è 12 per 120 ms. Questo valore consente a una risposta di includere i messaggi che verrebbero inviati entro il successivo intervallo di 120 ms se ogni tick è 10 ms.
- **NX_MDNS_PROBING_RETRANSMIT_COUNT** Numero di messaggi di probe ritrasmessi. Il valore predefinito è 3.
- **NX_MDNS_GOODBYE_RETRANSMIT_COUNT** Numero di messaggi "goodbye" ritrasmessi. Il valore predefinito è 1.
- **NX_MDNS_POOF_MIN_COUNT** Numero di query che non hanno risposta multicast, quindi l'host può prendere questo valore come indicazione che il record potrebbe non essere più valido. Il valore predefinito è 2.
- **NX_MDNS_POOF_TIME_COUNT** Intervallo di tempo, in tick, nell'eliminazione del record dalla cache dopo la visualizzazione di due o più di queste query e la visualizzazione di nessuna risposta multicast contenente la risposta prevista. Il valore predefinito è 1000 tick per 10 secondi.
- **NX_MDNS_RR_DELETE_DELAY_TIMER_COUNT** Ritardo per l'eliminazione di un record di risorse quando il valore TTL di questo record è zero, in tick, Il valore predefinito è 100 tick per 1 secondo.
