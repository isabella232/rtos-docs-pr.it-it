---
title: Capitolo 1-Introduzione al client DNS di Azure RTO NetX Duo
description: Il DNS fornisce un database distribuito che contiene il mapping tra i nomi di dominio e gli indirizzi IP fisici.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4c07d6e3183d421c637874dcdeff3767554fca78
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821929"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-duo-dns-client"></a>Capitolo 1-Introduzione al client DNS di Azure RTO NetX Duo

Il DNS fornisce un database distribuito che contiene il mapping tra i nomi di dominio e gli indirizzi IP fisici. Il database viene indicato come *distribuito* perché non esiste una singola entità in Internet che contiene il mapping completo. Un'entità che gestisce una parte del mapping è detta server DNS. Internet è costituito da numerosi server DNS, ognuno dei quali contiene un subset del database. I server DNS rispondono anche alle richieste client DNS per le informazioni di mapping dei nomi di dominio, solo se il server ha il mapping richiesto.

Il protocollo client DNS per NetX Duo fornisce all'applicazione i servizi per richiedere informazioni di mapping da uno o più server DNS.

## <a name="dns-client-setup"></a>Configurazione del client DNS

Per funzionare correttamente, il pacchetto client DNS richiede che sia già stata creata un'istanza IP di NetX Duo.

Dopo aver creato il client DNS, l'applicazione deve aggiungere uno o più server DNS all'elenco dei server gestiti dal client DNS. Per aggiungere i server DNS, l'applicazione usa il servizio *nxd_dns_server_add* . Il *nx_dns_server_add* servizio client DNS NETX Duo può essere usato anche per aggiungere server. Tuttavia, accetta solo indirizzi IPv4 ed è consigliabile che gli sviluppatori utilizzino invece il servizio *nxd_dns_server_add* .

Se l'opzione NX_DNS_IP_GATEWAY_SERVER è abilitata e l'indirizzo del gateway dell'istanza IP è diverso da zero, il gateway dell'istanza IP viene aggiunto automaticamente come server DNS primario. Se le informazioni sul server DNS non sono staticamente note, possono anche essere derivate tramite il Dynamic Host Configuration Protocol (DHCP) per NetX Duo. Per ulteriori informazioni, vedere la guida dell'utente di NetX Duo DHCP.

Il client DNS richiede un pool di pacchetti per la trasmissione di messaggi DNS. Per impostazione predefinita, il client DNS crea questo pool di pacchetti quando viene chiamato il servizio *nx_dns_create* . Le opzioni di configurazione NX_DNS_PACKET_PAYLOAD_UNALIGNED e NX_DNS_PACKET_POOL_SIZE consentono all'applicazione di determinare rispettivamente il payload del pacchetto e le dimensioni del pool di pacchetti (ad esempio, il numero di pacchetti) del pool di pacchetti. Queste opzioni sono descritte nella sezione "opzioni di configurazione" del capitolo due.

Un'alternativa al client DNS che crea il proprio pool di pacchetti consiste nel creare il pool di pacchetti da parte dell'applicazione e impostarlo come pool di pacchetti del client DNS usando il servizio *nx_dns_packet_pool_set* . A tale scopo, è necessario definire l'opzione NX_DNS_CLIENT_USER_CREATE_PACKET_POOL. Questa opzione richiede inoltre un pool di pacchetti creato in precedenza utilizzando *nx_packet_pool_create* come input del puntatore del pool di pacchetti per *nx_dns_packet_pool_set* . Quando viene eliminata l'istanza del client DNS, l'applicazione è responsabile dell'eliminazione del pool di pacchetti client DNS se NX_DNS_CLIENT_USER_CREATE_PACKET_POOL è abilitato se non è più necessario.

> [!NOTE] 
> Per le applicazioni che scelgono di fornire il proprio pool di pacchetti usando l'opzione NX_DNS_CLIENT_USER_CREATE_PACKET_POOL, le dimensioni del pacchetto devono essere in grado di contenere le dimensioni massime del massaggio DNS (512 byte) più le camere per l'intestazione UDP, l'intestazione IPv4 o IPv6 e l'intestazione MAC.

## <a name="dns-messages"></a>Messaggi DNS

Il DNS ha un meccanismo molto semplice per ottenere il mapping tra i nomi host e gli indirizzi IP. Per ottenere un mapping, il client DNS prepara un messaggio di query DNS contenente il nome o l'indirizzo IP che deve essere risolto. Il messaggio viene quindi inviato al primo server DNS nell'elenco Server. Se il server dispone di tale mapping, risponde al client DNS utilizzando un messaggio di risposta DNS che contiene le informazioni di mapping richieste. Se il server non risponde, il client DNS esegue una query sul server successivo nell'elenco fino a quando non viene eseguita una query su tutti i server DNS. Se non viene ricevuta alcuna risposta da tutti i server DNS, il client DNS ha la logica di ripetizione dei tentativi per ritrasmettere il messaggio DNS. Quando si invia nuovamente una query DNS, il timeout di ritrasmissione viene raddoppiato. Questo processo continua fino a raggiungere il timeout di trasmissione massimo (definito come NX_DNS_MAX_RETRANS_TIMEOUT in *nxd_dns. h*) o fino a quando non viene ricevuta una risposta corretta da tale server.

Il client DNS NetX Duo può eseguire sia ricerche di indirizzi IPv6 (tipo AAAA) che ricerche di indirizzi IPv4 (digitare A) specificando la versione dell'indirizzo IP nella chiamata *nxd_dns_host_by_name_get* . Il client DNS può eseguire ricerche inverse degli indirizzi IP (tipo query PTR) per ottenere i nomi host web usando *nxd_dns_host_by_address_get*. Il client DNS NetX Duo supporta ancora la *nx_dns_host_by_name_get* e *nx_dns_host_by_address_get* che sono i servizi equivalenti, ma che sono limitati alla comunicazione di rete IPv4. Tuttavia, gli sviluppatori sono invitati a trasferire le applicazioni client DNS esistenti ai servizi *nxd_dns_host_by_name_get* e *nxd_dns_host_by_address_get* .

La messaggistica DNS usa il protocollo UDP per inviare le richieste e le risposte dei campi. Un server DNS è in ascolto sul numero di porta 53 per le query dai client. Per questo motivo i servizi UDP devono essere abilitati in NetX Duo usando il servizio ***nx_udp_enable** _ in un'istanza IP creata in precedenza (_ *_nx_ip_create_* *).

A questo punto, il client DNS è pronto ad accettare le richieste dall'applicazione e a inviare le query DNS.

## <a name="extended-dns-resource-record-types"></a>Tipi di record di risorse DNS estesi

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è abilitato, il client DNS di NetX Duo supporta anche le query del tipo di record seguenti:

- CNAME: contiene il nome canonico di un alias
- TXT: contiene una stringa di testo
- NS: contiene un server di nomi autorevole
- SOA: contiene l'inizio di una zona di autorità
- MX: usato per lo scambio di posta
- SRV: contiene informazioni sul servizio offerte dal dominio

Fatta eccezione per i tipi di record CNAME e TXT, l'applicazione deve fornire un buffer allineato a 4 byte per ricevere il record di dati DNS.

Nel client DNS di NetX Duo, i dati dei record vengono archiviati in modo da sfruttare al meglio lo spazio del buffer.

Di seguito è riportato un esempio di un buffer di record di lunghezza fissa (record AAAA di tipo):

![Buffer di record di lunghezza fissa](media/image2.png)

Per le query i cui tipi di record hanno una lunghezza di dati variabile, ad esempio record NS i cui nomi host sono di lunghezza variabile, il client DNS di NetX Duo Salva i dati come indicato di seguito. Il buffer fornito nella query del client DNS è organizzato in un'area di dati a lunghezza fissa e in un'area di memoria non strutturata. La parte superiore del buffer di memoria è organizzata in voci di record allineate a 4 byte. Ogni voce di record contiene l'indirizzo IP e un puntatore ai dati a lunghezza variabile per l'indirizzo IP. I dati a lunghezza variabile per ogni indirizzo IP vengono archiviati nella memoria di area non strutturata a partire dalla fine del buffer di memoria. I dati a lunghezza variabile per ogni voce di record successiva vengono salvati nella memoria di area successiva accanto ai dati variabili delle voci di record precedenti. Di conseguenza, i dati delle variabili "crescono" verso l'area strutturata della memoria contenente le voci di record fino a quando non è disponibile memoria sufficiente per archiviare un'altra voce di record e i dati delle variabili.

Questa procedura è illustrata nella figura seguente:

![Figura 2](media/image3.png)

L'esempio di archiviazione dei dati del nome di dominio DNS (NS) è illustrato in precedenza.

Le query client DNS di NetX Duo con il formato di archiviazione dei record restituiscono il numero di record salvati nel buffer di record. Queste informazioni consentono all'applicazione di estrarre i record NS dal buffer di record.

Di seguito è riportato un esempio di query client DNS che archivia i dati DNS a lunghezza variabile usando questo formato di archiviazione di record:

```C
UINT  _nx_dns_domain_name_server_get(NX_DNS *dns_ptr, 
                    UCHAR *host_name, VOID *record_buffer, 
                    UINT buffer_size, UINT *record_count, 
                    ULONG wait_option);
```


Ulteriori informazioni sono disponibili nel capitolo 3 "Descrizione dei servizi client DNS".

## <a name="dns-cache"></a>Cache DNS

Se NX_DNS_CACHE_ENABLE è abilitato, il client DNS di NetX Duo supporta la funzionalità cache DNS. Dopo aver creato il client DNS, l'applicazione può chiamare l'API *nx_dns_cache_initialize ()* per impostare la cache DNS speciale. Se Abilita la funzionalità cache DNS, il client DNS troverà la risposta disponibile dalla cache DNS prima di iniziare a inviare una query DNS, se trova la risposta disponibile, restituirà direttamente la risposta all'applicazione; in caso contrario, il client DNS invia il messaggio di query al server DNS e attende la risposta. Quando il client DNS ottiene il messaggio di risposta ed è disponibile una cache gratuita, il client DNS restituisce la risposta all'applicazione e aggiunge la risposta come record di risorse nella cache DNS.

Ogni risposta a una struttura di dati *NX_DNS_RR* (record di risorse) nella cache. Le stringhe (nome e dati del record di risorse) nei record sono a lunghezza variabile e pertanto non sono archiviate nella struttura di NX_DNS_RR. Il record contiene puntatori alla posizione di memoria effettiva in cui sono archiviate le stringhe. La tabella delle stringhe e i record condividono la cache. I record vengono archiviati dall'inizio della cache e aumentano verso la fine della cache. La tabella delle stringhe inizia dalla fine della cache e cresce verso l'inizio della cache. Ogni stringa nella tabella di stringhe ha un campo lunghezza e un campo contatore. Quando una stringa viene aggiunta alla tabella delle stringhe, se la stessa stringa è già presente nella tabella, il valore del contatore viene incrementato e non viene allocata alcuna memoria per la stringa. La cache è considerata completa se non è possibile aggiungere più record di risorse o nuove stringhe alla cache.

## <a name="dns-client-limitations"></a>Limitazioni del client DNS

Il client DNS supporta una richiesta DNS alla volta. I thread che tentano di eseguire un'altra richiesta DNS sono temporaneamente bloccati fino al completamento della richiesta DNS precedente.

Il client DNS NetX Duo non usa i dati delle risposte autorevoli per inviare query DNS aggiuntive ad altri server DNS.

## <a name="dns-rfcs"></a>RFC DNS

Il DNS di NetX Duo è conforme alle RFC seguenti:

- NOMI DI DOMINIO RFC1034-CONCETTI E FUNZIONALITÀ
- NOMI DI DOMINIO RFC1035-IMPLEMENTAZIONE E SPECIFICA
- RFC1480 dominio degli Stati Uniti
- RFC 2782 un RR DNS per specificare il percorso dei servizi (DNS SRV)
- RFC 3596 estensioni DNS per supportare IP versione 6