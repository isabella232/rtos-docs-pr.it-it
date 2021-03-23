---
title: Capitolo 3-Descrizione della cache interna del servizio
description: 'Il modulo NetX Duo MDN gestisce due cache dei servizi interni: la cache del servizio locale e la cache del servizio peer.'
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 007f1080a076730cfbcdedc9f063ac0c427a414c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821818"
---
# <a name="chapter-3---description-of-internal-service-cache"></a>Capitolo 3-Descrizione della cache interna del servizio

Il modulo NetX Duo MDN gestisce due cache dei servizi interni: la cache del servizio locale e la cache del servizio peer. La cache del servizio locale archivia i record di risorse correlati ai servizi offerti dalle applicazioni in esecuzione nel nodo. Per le query in ingresso, se la domanda corrisponde al servizio offerto, risposte MDN con risposte memorizzate nella cache del servizio locale. Le applicazioni registrano i servizi chiamando l'API *nx_mdns_service_add ()*. Per rimuovere i servizi, le applicazioni usano l'API *nx_mdns_service_delete ()*, che a sua volta inviano messaggi "Goodbye" prima di rimuovere le voci corrispondenti nella cache del servizio locale.

Quando viene aggiunto un servizio, MDN gestisce almeno 3 record di risorse nella cache del servizio locale: SRV, PTR e TXT. È possibile aggiungere un record di risorse PTR aggiuntivo se il tipo di servizio include il sottotipo. Ad esempio, un'applicazione registra un servizio:

```
*name*._*subtype*._sub._*type*._tcp.local,
```

due record di risorse PTR vengono aggiunti alla cache del servizio locale, uno per

```
“*_subtype._*sub*._type._*tcp.local *PTR name.type._*tcp*.*local”
```

e l'altro per

```
*“_type._*tcp*.*local *PTR name.type._*tcp*.*local”.
```

La cache del servizio peer contiene i record di risorse MDN ricevuti dai nodi adiacenti. il modulo MDN raccoglie i record di risorse annunciati da altri nodi nella rete e archivia le informazioni ricevute nella cache dei servizi peer. Quando l'applicazione esegue query su informazioni quali indirizzi IPv4 o IPv6 host, MDN Cerca nella cache del servizio peer le risposte memorizzate nella cache locale. Quando l'applicazione esegue query per i servizi offerti da peer, MDN Cerca nella cache i record di indirizzi PTR, SRV, TXT e IPv4/IPv6 correlati. La cache del servizio peer archivia anche le query inviate al nodo. Ad esempio, un'applicazione può richiedere un particolare servizio chiamando *nx_mdns_service_one_shot_query.* Se il servizio non viene trovato nella cache dei servizi peer, MDN crea domande di query (PTR, SRV e TXT) nella cache del servizio peer. Queste domande di query verranno inviate periodicamente alla rete fino a quando il servizio non viene risolto o si verifica il timeout. Analogamente, l'applicazione può usare l'API *nx_mdns_service_continous_query ()* per richiedere un particolare servizio in un lungo periodo di tempo (l'applicazione annulla una query continua rilasciata in precedenza tramite l'API *nx_mdns_service_query_stop ()* ). Per cercare un servizio specifico nella cache del servizio peer senza inviare query alla rete, le applicazioni possono usare l'API *nx_mdns_serivce_lookup ().* Questa API cerca solo i record di risorse nella cache dei servizi peer.

Ogni record di risorse viene archiviato in una struttura di dati *NX_MDNS_RR* nelle cache dei servizi. Le stringhe nei record di risorse sono a lunghezza variabile e pertanto non sono archiviate nella struttura di *NX_MDNS_RR* . Il record di risorse contiene un puntatore alla posizione di memoria effettiva in cui è archiviata la stringa. La tabella delle stringhe e i record di risorse condividono la cache del servizio. I record di risorse vengono archiviati dall'inizio della cache del servizio e aumentano verso la fine della cache. La tabella delle stringhe inizia dalla fine della cache del servizio e aumenta verso l'inizio della cache. Ogni stringa nella tabella di stringhe ha un campo lunghezza e un campo contatore. Quando una stringa viene aggiunta alla tabella delle stringhe, se la stessa stringa è già presente nella tabella, il valore del contatore viene incrementato e non viene allocata alcuna memoria per la stringa. La cache del servizio è considerata completa se non è possibile aggiungere più record di risorse o nuove stringhe alla cache del servizio.

Esistono due modi per trovare i servizi offerti nella rete locale da parte di un'applicazione. Può emettere una ricerca di un servizio specifico tramite una query di tipo One-Shot oppure può avviare una query continua per "monitorare" le attività sulla rete. In uno scenario di query a breve, l'applicazione deve specificare il tipo di servizio. MDN esegue la ricerca attraverso la cache del servizio locale e la cache del servizio peer. Se viene individuata un'istanza del servizio, la query monouso restituisce le informazioni contenute nei record di risorse. Se nella cache del servizio locale o nella cache del servizio peer non sono presenti record, MDN invia messaggi di query. Se viene specificato il nome dell'istanza, un *qualsiasi* tipo (eseguire una query sul tipo SRV e txt) con il nome dell'istanza specifico, nel formato "nome. Type. local", viene inviato alla rete locale. Se il nome dell'istanza non è specificato, viene inviato un tipo di query PTR alla rete locale. Il primo servizio completo ricevuto viene restituito al chiamante.

La query continua funziona in modo diverso. Il caso d'uso tipico per una query continua consiste nel monitorare la rete locale per un servizio specifico, ad esempio per cercare costantemente i servizi di stampa nella rete locale. In questo caso l'applicazione esegue una query di ricerca (tramite la query API *nx_mdns_service_continious_*) per determinati tipi di servizi. Il chiamante in genere non attende una determinata risposta. Per le query inviate come query continua, il modulo MDN trasmette periodicamente le query con intervalli esponenzialmente crescenti. Per arrestare la query, l'applicazione deve usare l'API *nx_mdns_service_query_stop* per arrestare il timer interno in queste query. Il tipo di query può essere NULL, nel qual caso il tipo di query è impostato su speciale tipo PTR "_services. _dns-SD. _udp. local". Questo tipo di servizio è definito da MDN come modo per individuare tutti i servizi disponibili nella rete locale. Se viene specificato il nome dell'istanza, alla rete locale viene inviato un qualsiasi tipo (eseguire una query sul tipo SRV e TXT) con il nome di istanza specifico "Name. Type. local". Se il nome dell'istanza è NULL, viene inviato un tipo di query PTR alla rete locale.

Tutte le risposte, incluse le risposte da query non richieste, vengono registrate nella cache dei servizi peer. In un secondo momento, l'applicazione utilizza l'API *nx_mdns_service_lookup* per recuperare un servizio specifico dalla cache del servizio peer.

Nota speciale sulla frammentazione: ogni *NX_MDNS_RR* struttura è di dimensioni fisse e pertanto non è soggetta a frammentazione quando MDN aggiunge ed Elimina RRS. Tuttavia, le stringhe sono a lunghezza variabile. Dopo l'eliminazione di una stringa, lo spazio diventa disponibile e potrebbe essere usato per una nuova stringa se la nuova stringa può adattarsi. Questa operazione comporta tuttavia la frammentazione della memoria. Quando i servizi vengono aggiunti e rimossi, la tabella delle stringhe può essere frammentata nel punto in cui non è possibile aggiungere nuove stringhe anche se la cache del servizio contiene un numero sufficiente di byte non utilizzati per la stringa. Le applicazioni locali tendono a essere più stabili e prevedibili. Pertanto è meno probabile che la cache del servizio locale soffra di frammentazione. La cache del servizio peer, d'altra parte, aggiunge costantemente RRs quando i servizi diventano disponibili o rimuove RRs come i servizi vengono eliminati dai nodi sulla rete. I servizi sulla rete sono disponibili, causando operazioni di allocazione/eliminazione più frequenti nella tabella di stringhe. Nel tempo è possibile che la tabella delle stringhe diventi frammentata. Quando si verifica questa situazione, una soluzione semplice consiste nello scaricare l'intera cache del servizio peer. Questa operazione può essere eseguita chiamando l'API *nx_mdns_peer_cache_clear ().* Si noti che questa API termina automaticamente le query continue in attesa.
