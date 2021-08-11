---
title: Capitolo 3 - Descrizione della cache del servizio interno
description: 'Il modulo mDNS di NetX Duo gestisce due cache dei servizi interni: la cache del servizio locale e la peer service cache.'
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: edf52cb2d7df293a4606d6c5b5b63075969933fb1a093a1d83b91b2709c08f0c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791721"
---
# <a name="chapter-3---description-of-internal-service-cache"></a>Capitolo 3 - Descrizione della cache del servizio interno

Il modulo mDNS di NetX Duo gestisce due cache dei servizi interni: la cache del servizio locale e la peer service cache. La cache del servizio locale archivia i record di risorse correlati ai servizi offerti dalle applicazioni in esecuzione nel nodo. Per le query in ingresso, se la domanda corrisponde al servizio offerto, le risposte mDNS con le risposte archiviate nella cache del servizio locale. Le applicazioni registrano i servizi chiamando l'API *nx_mdns_service_add()*. Per rimuovere i servizi, le applicazioni usano l'API *nx_mdns_service_delete()*, che a sua volta invierà messaggi di saluto prima di rimuovere le voci corrispondenti nella cache del servizio locale.

Quando viene aggiunto un servizio, mDNS mantiene almeno 3 record di risorse nella cache del servizio locale: SRV, PTR e TXT. È possibile aggiungere un record di risorse PTR aggiuntivo se il tipo di servizio include un sottotipo. Ad esempio, un'applicazione registra un servizio:

```
*name*._*subtype*._sub._*type*._tcp.local,
```

vengono aggiunti due record di risorse PTR alla cache del servizio locale, uno per

```
“*_subtype._*sub*._type._*tcp.local *PTR name.type._*tcp*.*local”
```

e l'altra per

```
*“_type._*tcp*.*local *PTR name.type._*tcp*.*local”.
```

La cache del servizio peer contiene i record di risorse mDNS ricevuti dai nodi adiacenti. Il modulo mDNS raccoglie i record di risorse annunciati da altri nodi nella rete e archivia le informazioni ricevute nella cache del servizio peer. Quando l'applicazione esegue una query per informazioni, ad esempio indirizzi IPv4 o IPv6 host, mDNS cerca nella cache del servizio peer le risposte memorizzate nella cache locale. Quando l'applicazione esegue query per i servizi offerti dai peer, mDNS cerca nella cache i record di indirizzi PTR, SRV, TXT e IPv4/IPv6 correlati. La cache del servizio peer archivia anche le query inviate al nodo. Ad esempio, un'applicazione può richiedere un particolare servizio chiamando *nx_mdns_service_one_shot_query.* Se il servizio non viene trovato nella peer service cache, mDNS crea domande di query (PTR, SRV e TXT) nella peer service cache. Queste domande di query verranno inviate periodicamente alla rete fino a quando il servizio non viene risolto o si verifica il timeout. Analogamente, l'applicazione può usare l'API *nx_mdns_service_continous_query()* per richiedere un particolare servizio per un lungo periodo di tempo (l'applicazione annulla una query continua emessa in precedenza usando l'API *nx_mdns_service_query_stop()* ). Per cercare un particolare servizio nella peer service cache senza inviare query alla rete, le applicazioni possono usare l'API *nx_mdns_serivce_lookup().* Questa API cerca solo i record di risorse nella cache del servizio peer.

Ogni record di risorse viene archiviato in una struttura di *dati NX_MDNS_RR* nelle cache del servizio. Le stringhe nei record di risorse sono di lunghezza variabile, pertanto non vengono archiviate nella *NX_MDNS_RR* struttura. Il record di risorse contiene un puntatore alla posizione di memoria effettiva in cui è archiviata la stringa. La tabella di stringhe e i record di risorse condividono la cache del servizio. I record di risorse vengono archiviati dall'inizio della cache del servizio e aumentano fino alla fine della cache. La tabella di stringhe inizia dalla fine della cache del servizio e si sviluppa verso l'inizio della cache. Ogni stringa nella tabella delle stringhe ha un campo di lunghezza e un campo contatore. Quando viene aggiunta una stringa alla tabella di stringhe, se la stessa stringa è già presente nella tabella, il valore del contatore viene incrementato e non viene allocata memoria per la stringa. La cache del servizio viene considerata completa se non è possibile aggiungere altri record di risorse o nuove stringhe alla cache del servizio.

Un'applicazione può trovare i servizi offerti nella rete locale in due modi. Può eseguire una ricerca di un servizio specifico tramite una query con un'unica operazione oppure può avviare una query continua per "monitorare" le attività nella rete. Nello scenario di query one-short, l'applicazione deve specificare il tipo di servizio. mDNS cerca nella cache del servizio locale e nella cache del servizio peer. Se si trova un'istanza del servizio, la query viene restituita con le informazioni presenti nei record di risorse. Se non sono presenti record nella cache del servizio locale o nella peer service cache, mDNS invia messaggi di query. Se si specifica il nome dell'istanza, alla rete locale viene inviato un tipo *ANY* (query sul tipo SRV e TXT) con il nome dell'istanza specifico, sotto forma di "name.type.local". Se il nome dell'istanza non viene specificato, viene inviato un tipo PTR di query alla rete locale. Il primo servizio completo ricevuto viene restituito al chiamante.

Le query continue funzionano in modo diverso. Il caso d'uso tipico per una query continua è monitorare la rete locale per un servizio specifico, ad esempio per cercare costantemente i servizi di stampa nella rete locale. In questo caso l'applicazione esegue una query di ricerca (tramite l'API *nx_mdns_service_continious_* query) per un determinato tipo di servizi. Il chiamante in genere non attende una risposta specifica. Per le query inviate come query continue, il modulo mDNS trasmette periodicamente le query con intervalli in aumento esponenziale. Per arrestare la query, l'applicazione deve usare l'API *nx_mdns_service_query_stop* per arrestare il timer interno in queste query. Il tipo di query può essere NULL, nel qual caso il tipo di query è impostato sul tipo PTR speciale "_services._dns-sd._udp.local". Questo tipo di servizio è definito da mDNS come modo per individuare tutti i servizi disponibili nella rete locale. Se viene specificato il nome dell'istanza, alla rete locale viene inviato un tipo ANY (eseguire una query sul tipo SRV e TXT) con il nome di istanza specifico "name.type.local". Se il nome dell'istanza è NULL, viene inviato un tipo PTR di query alla rete locale,

Tutte le risposte, incluse le risposte provenienti da query non richieste, vengono registrate nella cache del servizio peer. In un secondo momento, l'applicazione usa l'API *nx_mdns_service_lookup* per recuperare un servizio specifico dalla peer service cache.

Nota speciale sulla frammentazione: ogni *NX_MDNS_RR* struttura è fissa e pertanto non è soggetta a frammentazione in quanto mDNS aggiunge ed elimina rR. Tuttavia, le stringhe sono di lunghezza variabile. Dopo l'eliminazione di una stringa, lo spazio diventa disponibile e può essere usato per una nuova stringa se la nuova stringa è in grado di adattarsi. Ma questa operazione causa la frammentazione della memoria. Quando i servizi vengono aggiunti e rimossi, la tabella di stringhe può essere frammentata al punto che non è possibile aggiungere nuove stringhe anche se la cache del servizio contiene un numero sufficiente di byte inutilizzati per la stringa. Le applicazioni locali tendono a essere più stabili e prevedibili. Di conseguenza, la cache del servizio locale ha meno probabilità di subire la frammentazione. La cache del servizio peer, d'altra parte, aggiunge continuamente rR man mano che i servizi diventano disponibili o rimuove gli RR quando i servizi vengono eliminati dai nodi nella rete. I servizi in rete vengono e vengono esere, causando operazioni di allocazione/eliminazione più frequenti nella tabella delle stringhe. Nel corso del tempo è possibile che la tabella di stringhe diventi frammentata. Quando si verifica questa situazione, una soluzione semplice consiste nel scaricare l'intera cache del servizio peer. Questa operazione può essere eseguita chiamando l'API *nx_mdns_peer_cache_clear().* Si noti che questa API termina automaticamente tutte le query continue in sospeso.
