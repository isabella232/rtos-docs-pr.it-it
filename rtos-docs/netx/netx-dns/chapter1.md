---
title: Capitolo 1 - Introduzione al client DNS NetX Azure RTOS
description: Il Azure RTOS DNS NetX fornisce un database distribuito che contiene il mapping tra i nomi di dominio e gli indirizzi IP fisici.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: fda8c5b1bdb35e8312204374592e411a6a1e44f79a4a75a035a7886223c22b53
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796387"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-dns-client"></a>Capitolo 1 - Introduzione al client DNS NetX Azure RTOS

Il Azure RTOS DNS NetX fornisce un database distribuito che contiene il mapping tra i nomi di dominio e gli indirizzi IP fisici. Il database viene definito *distribuito* perché in Internet non è presente una singola entità che contiene il mapping completo. Un'entità che gestisce una parte del mapping è denominata server DNS. Internet è costituito da numerosi server DNS, ognuno dei quali contiene un subset del database. I server DNS rispondono anche alle richieste client DNS per le informazioni sul mapping dei nomi di dominio, solo se il server ha il mapping richiesto.

Il protocollo client DNS per NetX fornisce all'applicazione servizi per richiedere informazioni di mapping da uno o più server DNS.

## <a name="dns-client-setup"></a>Configurazione del client DNS

Per funzionare correttamente, il pacchetto client DNS richiede che sia già stata creata un'istanza IP NetX.

Dopo aver creato il client DNS, l'applicazione deve aggiungere uno o più server DNS all'elenco di server gestito dal client DNS. Per aggiungere server DNS, l'applicazione usa il *nx_dns_server_add* dns.

Se l'NX_DNS_IP_GATEWAY_SERVER è abilitata e l'indirizzo del gateway dell'istanza IP è diverso da zero, il gateway dell'istanza IP viene aggiunto automaticamente come server DNS primario. Se le informazioni sul server DNS non sono note in modo statico, possono essere derivate anche tramite il Dynamic Host Configuration Protocol (DHCP) per NetX. Per altre informazioni, fare riferimento al Manuale dell'utente di NetX DHCP.

Il client DNS richiede un pool di pacchetti per la trasmissione di messaggi DNS. Per impostazione predefinita, il client DNS crea questo pool di pacchetti quando viene *chiamato nx_dns_create* servizio. Le opzioni di NX_DNS_PACKET_PAYLOAD e NX_DNS_PACKET_POOL_SIZE consentono all'applicazione di determinare rispettivamente il payload del pacchetto e le dimensioni del pool di pacchetti (ad esempio, il numero di pacchetti) di questo pool di pacchetti. Queste opzioni sono descritte nella sezione "Opzioni di configurazione" nel capitolo 2.

Un'alternativa al client DNS che crea il proprio pool di pacchetti consiste nel creare il pool di pacchetti e impostarlo come pool di pacchetti del client DNS usando il *servizio nx_dns_packet_pool_set* DNS. A tale scopo, è necessario NX_DNS_CLIENT_USER_CREATE_PACKET_POOL'opzione . Questa opzione richiede anche un pool di pacchetti creato in precedenza *usando nx_packet_pool_create* come input del puntatore del pool di pacchetti *nx_dns_packet_pool_set*. Quando l'istanza del client DNS viene eliminata, l'applicazione è responsabile dell'eliminazione del pool di pacchetti del client DNS se NX_DNS_CLIENT_USER_CREATE_PACKET_POOL è abilitato se non è più necessario.

>[!NOTE] 
> Per le applicazioni che scelgono di fornire il proprio pool di pacchetti usando l'opzione **NX_DNS_CLIENT_USER_CREATE_PACKET_POOL,** le dimensioni del pacchetto devono essere in grado di contenere le dimensioni massime del massaggio DNS (512 byte) più le stanze per l'intestazione UDP, l'intestazione IPv4 e l'intestazione MAC.

## <a name="dns-messages"></a>Messaggi DNS

Il DNS ha un meccanismo molto semplice per ottenere il mapping tra i nomi host e gli indirizzi IP. Per ottenere un mapping, il client DNS prepara un messaggio di query DNS contenente il nome o l'indirizzo IP che deve essere risolto. Il messaggio viene quindi inviato al primo server DNS nell'elenco dei server. Se il server ha un mapping di questo tipo, risponde al client DNS usando un messaggio di risposta DNS contenente le informazioni di mapping richieste. Se il server non risponde, il client DNS esegue una query sul server successivo nel relativo elenco fino a quando non vengono eseguite query su tutti i relativi server DNS. Se non viene ricevuta alcuna risposta da tutti i server DNS, il client DNS dispone della logica di ripetizione dei tentativi per ritrasmettere il messaggio DNS. Al nuovo invio di una query DNS, il timeout di ritrasmissione è raddoppiato. Questo processo continua fino a quando non viene raggiunto il timeout massimo di trasmissione (definito come NX_DNS_MAX_RETRANS_TIMEOUT in *nxd_dns.h)* o fino a quando non viene ricevuta una risposta corretta da tale server.

Il client DNS NetX può eseguire ricerche di indirizzi IPv4 (tipo A) chiamando nx_dns_host_by_name_get *o* *nx_dns_ipv4_address_by_name_get*. Il client DNS può eseguire ricerche inverse di indirizzi IP (query di tipo PTR) per ottenere nomi host *Web usando* nx_dns_host_by_address_get .

La messaggistica DNS usa il protocollo UDP per inviare richieste e risposte sul campo. Un server DNS è in ascolto sulla porta 53 per le query dai client. I servizi UDP devono quindi essere abilitati in NetX usando il servizio ***nx_udp_enable** _ in un'istanza IP creata in precedenza (_*_nx_ip_create_**).

A questo punto, il client DNS è pronto ad accettare richieste dall'applicazione e inviare query DNS.

## <a name="extended-dns-resource-record-types"></a>Tipi di record di risorse DNS estesi

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES abilitata, il client DNS NetX supporta anche le query sui tipi di record seguenti:

- **CNAME:** contiene il nome canonico per un alias

- **TXT:** contiene una stringa di testo

- **NS:** contiene un server dei nomi autorevole

- **SOA:** contiene l'inizio di una zona di autorità

- **MX:** usato per lo scambio di posta elettronica

- **SRV:** contiene informazioni sul servizio offerto dal dominio

Ad eccezione dei tipi di record CNAME e TXT, l'applicazione deve fornire un buffer allineato a 4 byte per ricevere il record di dati DNS.

Nel client DNS NetX i dati dei record vengono archiviati in modo da usare in modo più efficiente lo spazio del buffer.

Per le query i cui tipi di record hanno una lunghezza dei dati variabile, ad esempio record NS i cui nomi host sono di lunghezza variabile, il client DNS NetX salva i dati come indicato di seguito. Il buffer fornito nella query del client DNS è organizzato in un'area di dati a lunghezza fissa e in un'area di memoria non strutturata. La parte superiore del buffer di memoria è organizzata in voci di record allineate a 4 byte. Ogni voce di record contiene l'indirizzo IP e un puntatore ai dati a lunghezza variabile per tale indirizzo IP. I dati a lunghezza variabile per ogni indirizzo IP vengono archiviati nella memoria dell'area non strutturata a partire dalla fine del buffer di memoria. I dati a lunghezza variabile per ogni voce di record successiva vengono salvati nella memoria dell'area successiva adiacente ai dati delle variabili delle voci di record precedenti. Di conseguenza, i dati delle variabili "aumentano" verso l'area strutturata della memoria contenente le voci di record fino a quando la memoria non è insufficiente per archiviare un'altra voce di record e dati variabili.

Questa operazione è illustrata nella figura seguente:

![Diagramma di un esempio dell'archiviazione dati D N S domain name (N S)](media/image1.png)

L'esempio dell'archiviazione dati del nome di dominio DNS (NS) è illustrato in precedenza.

Le query del client DNS NetX che usano il formato di archiviazione dei record restituiscono il numero di record salvati nel buffer dei record. Queste informazioni consentono all'applicazione di estrarre record NS dal buffer dei record.

Di seguito è riportato un esempio di query client DNS che archivia dati DNS a lunghezza variabile usando questo formato di archiviazione dei record:

```c
UINT     _nx_dns_domain_name_server_get(NX_DNS *dns_ptr, UCHAR  *host_name, 
                                        VOID *record_buffer, UINT buffer_size, 
                                        UINT *record_count, ULONG wait_option);
```

Altri dettagli sono disponibili nel capitolo 3, "Descrizione dei servizi client DNS".

## <a name="dns-cache"></a>DNS Cache

Se NX_DNS_CACHE_ENABLE abilitata, il client DNS NetX supporta la funzionalità Cache DNS. Dopo aver creato il client DNS, l'applicazione può chiamare l'API *nx_dns_cache_initialize()* per impostare la cache DNS speciale. Se si abilita la funzionalità Cache DNS, il client DNS troverà la risposta disponibile dalla cache DNS prima di iniziare a inviare la query DNS. Se trova la risposta disponibile, restituisce direttamente la risposta all'applicazione, in caso contrario il client DNS invia un messaggio di query al server DNS e attende la risposta. Quando il client DNS ottiene il messaggio di risposta ed è disponibile una cache gratuita, il client DNS restituisce la risposta all'applicazione e aggiunge anche la risposta come record di risorse nella cache DNS.

Ognuno risponde a una struttura *NX_DNS_RR* (record di risorse) nella cache. Le stringhe (nome e dati dei record di risorse) nei record sono di lunghezza variabile, pertanto non vengono archiviate nella NX_DNS_RR struttura. Record contiene puntatori alla posizione di memoria effettiva in cui vengono archiviate le stringhe. La tabella di stringhe e i record condividono la cache. I record vengono archiviati dall'inizio della cache e aumentano fino alla fine della cache. La tabella di stringhe inizia dalla fine della cache e si avvia verso l'inizio della cache. Ogni stringa nella tabella delle stringhe ha un campo di lunghezza e un campo contatore. Quando viene aggiunta una stringa alla tabella di stringhe, se la stessa stringa è già presente nella tabella, il valore del contatore viene incrementato e non viene allocata memoria per la stringa. La cache viene considerata completa se non è possibile aggiungere altri record di risorse o nuove stringhe alla cache.

## <a name="dns-client-limitations"></a>Limitazioni del client DNS

Il client DNS supporta una richiesta DNS alla volta. I thread che tentano di effettuare un'altra richiesta DNS vengono temporaneamente bloccati fino al completamento della richiesta DNS precedente.

Il client DNS NetX non usa i dati delle risposte autorevoli per inoltrare query DNS aggiuntive ad altri server DNS.

## <a name="dns-rfcs"></a>RFC DNS

Dns NetX è conforme alle RFC seguenti:

- NOMI DI DOMINIO RFC1034 - CONCETTI E FUNZIONALITÀ
- NOMI DI DOMINIO RFC1035 - IMPLEMENTAZIONE E SPECIFICA
- RFC1480 The US Domain
- RFC 2782 A DNS RR per specificare la posizione dei servizi (DNS SRV)