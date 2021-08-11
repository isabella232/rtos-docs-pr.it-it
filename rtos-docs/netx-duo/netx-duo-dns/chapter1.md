---
title: Capitolo 1 - Introduzione al client DNS Azure RTOS NetX Duo
description: Il DNS fornisce un database distribuito che contiene il mapping tra i nomi di dominio e gli indirizzi IP fisici.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e878d32d6bcf514bb75a76b51e66c4d267b1a5b34f6c4b2df6ab231e5814ffc5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792059"
---
# <a name="chapter-1---introduction-to-the-azure-rtos-netx-duo-dns-client"></a>Capitolo 1 - Introduzione al client DNS Azure RTOS NetX Duo

Il DNS fornisce un database distribuito che contiene il mapping tra i nomi di dominio e gli indirizzi IP fisici. Il database viene definito distribuito *perché* non esiste una singola entità su Internet che contiene il mapping completo. Un'entità che gestisce una parte del mapping è denominata server DNS. Internet è costituito da numerosi server DNS, ognuno dei quali contiene un subset del database. I server DNS rispondono anche alle richieste dei client DNS per le informazioni sul mapping dei nomi di dominio, solo se il server dispone del mapping richiesto.

Il protocollo client DNS per NetX Duo fornisce all'applicazione i servizi per richiedere informazioni di mapping da uno o più server DNS.

## <a name="dns-client-setup"></a>Configurazione del client DNS

Per funzionare correttamente, il pacchetto client DNS richiede che sia già stata creata un'istanza IP di NetX Duo.

Dopo aver creato il client DNS, l'applicazione deve aggiungere uno o più server DNS all'elenco di server gestito dal client DNS. Per aggiungere server DNS, l'applicazione usa *il nxd_dns_server_add* servizio. Il servizio client DNS NetX Duo *nx_dns_server_add* può essere usato anche per aggiungere server. Accetta tuttavia solo indirizzi IPv4 ed è consigliabile che gli sviluppatori usino *nxd_dns_server_add* servizio.

Se l NX_DNS_IP_GATEWAY_SERVER è abilitata e l'indirizzo del gateway dell'istanza IP è diverso da zero, il gateway dell'istanza IP viene aggiunto automaticamente come server DNS primario. Se le informazioni sul server DNS non sono note in modo statico, possono essere derivate anche tramite il Dynamic Host Configuration Protocol (DHCP) per NetX Duo. Per altre informazioni, vedere il Manuale dell'utente di NetX Duo DHCP.

Il client DNS richiede un pool di pacchetti per la trasmissione di messaggi DNS. Per impostazione predefinita, il client DNS crea questo pool di pacchetti *quando nx_dns_create* viene chiamato il servizio dns. Le opzioni di configurazione NX_DNS_PACKET_PAYLOAD_UNALIGNED e NX_DNS_PACKET_POOL_SIZE consentono all'applicazione di determinare rispettivamente il payload dei pacchetti e le dimensioni del pool di pacchetti (ad esempio, il numero di pacchetti) di questo pool di pacchetti. Queste opzioni sono descritte nella sezione "Opzioni di configurazione" nel capitolo 2.

Un'alternativa al client DNS che crea il proprio pool di pacchetti è che l'applicazione crei il pool di pacchetti e lo imposta come pool di pacchetti del client DNS usando il *nx_dns_packet_pool_set* dns. A tale scopo, è necessario NX_DNS_CLIENT_USER_CREATE_PACKET_POOL'opzione di configurazione. Questa opzione richiede anche un pool di pacchetti creato in precedenza *usando nx_packet_pool_create* come input del puntatore del pool di pacchetti *nx_dns_packet_pool_set* . Quando l'istanza del client DNS viene eliminata, l'applicazione è responsabile dell'eliminazione del pool di pacchetti del client DNS se NX_DNS_CLIENT_USER_CREATE_PACKET_POOL è abilitato se non è più necessario.

> [!NOTE] 
> Per le applicazioni che scelgono di fornire il proprio pool di pacchetti usando l'opzione NX_DNS_CLIENT_USER_CREATE_PACKET_POOL, le dimensioni del pacchetto devono essere in grado di contenere le dimensioni massime del DNS (512 byte) più le stanze per l'intestazione UDP, l'intestazione IPv4 o IPv6 e l'intestazione MAC.

## <a name="dns-messages"></a>Messaggi DNS

Il DNS ha un meccanismo molto semplice per ottenere il mapping tra nomi host e indirizzi IP. Per ottenere un mapping, il client DNS prepara un messaggio di query DNS contenente il nome o l'indirizzo IP che deve essere risolto. Il messaggio viene quindi inviato al primo server DNS nell'elenco dei server. Se il server ha un mapping di questo tipo, risponde al client DNS usando un messaggio di risposta DNS contenente le informazioni di mapping richieste. Se il server non risponde, il client DNS esegue una query sul server successivo nell'elenco fino a quando non vengono eseguite query su tutti i server DNS. Se non viene ricevuta alcuna risposta da tutti i server DNS, il client DNS ha la logica di ripetizione dei tentativi per ritrasmettere il messaggio DNS. Al nuovo invio di una query DNS, il timeout di ritrasmissione è raddoppiato. Questo processo continua fino a quando non viene raggiunto il timeout massimo di trasmissione (definito come NX_DNS_MAX_RETRANS_TIMEOUT in *nxd_dns.h*) o fino a quando non viene ricevuta una risposta corretta da tale server.

Il client DNS di NetX Duo può eseguire sia ricerche di indirizzi IPv6 (tipo AAAA) che ricerche di indirizzi IPv4 (tipo A) specificando la versione dell'indirizzo IP nella *chiamata nxd_dns_host_by_name_get* chiamata. Il client DNS può eseguire ricerche inverse di indirizzi IP (query PTR di tipo) per ottenere nomi host Web *usando nxd_dns_host_by_address_get*. Il client DNS di NetX  Duo supporta ancora i nx_dns_host_by_name_get e *nx_dns_host_by_address_get* che sono i servizi equivalenti, ma che sono limitati alla comunicazione di rete IPv4. Tuttavia, gli sviluppatori sono invitati a convertire le applicazioni client DNS esistenti *nei servizi* nxd_dns_host_by_name_get e *nxd_dns_host_by_address_get* dns.

La messaggistica DNS usa il protocollo UDP per inviare richieste e risposte sul campo. Un server DNS è in ascolto sulla porta 53 per le query dai client. I servizi UDP devono quindi essere abilitati in NetX Duo usando il servizio ***nx_udp_enable** _ in un'istanza IP creata in precedenza (_*_nx_ip_create_**).

A questo punto, il client DNS è pronto ad accettare le richieste dall'applicazione e inviare query DNS.

## <a name="extended-dns-resource-record-types"></a>Tipi di record di risorse DNS estesi

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è abilitata, il client DNS di NetX Duo supporta anche le query sul tipo di record seguenti:

- CNAME: contiene il nome canonico per un alias
- TXT: contiene una stringa di testo
- NS: contiene un server dei nomi autorevole
- SOA: contiene l'inizio di una zona di autorità
- MX: usato per lo scambio di posta elettronica
- SRV: contiene informazioni sul servizio offerto dal dominio

Ad eccezione dei tipi di record CNAME e TXT, l'applicazione deve fornire un buffer allineato a 4 byte per ricevere il record di dati DNS.

Nel client DNS di NetX Duo i dati dei record vengono archiviati in modo da usare in modo più efficiente lo spazio del buffer.

Di seguito è riportato un esempio di buffer di record di lunghezza fissa (tipo record AAAA):

![Buffer di record di lunghezza fissa](media/image2.png)

Per le query i cui tipi di record hanno una lunghezza dei dati variabile, ad esempio record NS i cui nomi host sono di lunghezza variabile, il client DNS di NetX Duo salva i dati come indicato di seguito. Il buffer fornito nella query del client DNS è organizzato in un'area di dati a lunghezza fissa e in un'area di memoria non strutturata. La parte superiore del buffer di memoria è organizzata in voci di record allineate a 4 byte. Ogni voce di record contiene l'indirizzo IP e un puntatore ai dati a lunghezza variabile per tale indirizzo IP. I dati a lunghezza variabile per ogni indirizzo IP vengono archiviati nella memoria dell'area non strutturata a partire dalla fine del buffer di memoria. I dati a lunghezza variabile per ogni voce di record successiva vengono salvati nella memoria di area successiva adiacente ai dati delle variabili delle voci di record precedenti. Di conseguenza, i dati delle variabili "aumentano" verso l'area strutturata della memoria contenente le voci di record fino a quando la memoria non è insufficiente per archiviare un'altra voce di record e dati variabili.

Come illustrato nella figura seguente:

![Figura 2](media/image3.png)

L'esempio di archiviazione dei dati del nome di dominio DNS (NS) è illustrato in precedenza.

Le query del client DNS di NetX Duo che usano il formato di archiviazione dei record restituiscono il numero di record salvati nel buffer dei record. Queste informazioni consentono all'applicazione di estrarre i record NS dal buffer dei record.

Di seguito è riportato un esempio di query del client DNS che archivia dati DNS a lunghezza variabile usando questo formato di archiviazione dei record:

```C
UINT  _nx_dns_domain_name_server_get(NX_DNS *dns_ptr, 
                    UCHAR *host_name, VOID *record_buffer, 
                    UINT buffer_size, UINT *record_count, 
                    ULONG wait_option);
```


Altri dettagli sono disponibili nel capitolo 3, "Descrizione dei servizi client DNS".

## <a name="dns-cache"></a>DNS Cache

Se NX_DNS_CACHE_ENABLE abilitata, il client DNS di NetX Duo supporta la funzionalità Cache DNS. Dopo aver creato il client DNS, l'applicazione può chiamare l'API *nx_dns_cache_initialize()* per impostare la cache DNS speciale. Se si abilita la funzionalità Cache DNS, il client DNS troverà la risposta disponibile dalla cache DNS prima di iniziare a inviare la query DNS. Se trova la risposta disponibile, restituisce direttamente la risposta all'applicazione. In caso contrario, il client DNS invia il messaggio di query al server DNS e attende la risposta. Quando il client DNS riceve il messaggio di risposta ed è disponibile una cache libera, il client DNS restituisce la risposta all'applicazione e aggiunge la risposta come record di risorse nella cache DNS.

Ogni risposta a una *struttura NX_DNS_RR* dati (record di risorse) nella cache. Le stringhe (nome e dati dei record di risorse) nei record sono di lunghezza variabile, pertanto non vengono archiviate nella NX_DNS_RR dati. Il record contiene puntatori alla posizione di memoria effettiva in cui sono archiviate le stringhe. La tabella di stringhe e i record condividono la cache. I record vengono archiviati dall'inizio della cache e aumentano fino alla fine della cache. La tabella di stringhe inizia dalla fine della cache e aumenta verso l'inizio della cache. Ogni stringa nella tabella di stringhe ha un campo di lunghezza e un campo contatore. Quando viene aggiunta una stringa alla tabella di stringhe, se la stessa stringa è già presente nella tabella, il valore del contatore viene incrementato e non viene allocata memoria per la stringa. La cache viene considerata completa se non è possibile aggiungere altri record di risorse o nuove stringhe alla cache.

## <a name="dns-client-limitations"></a>Limitazioni del client DNS

Il client DNS supporta una richiesta DNS alla volta. I thread che tentano di effettuare un'altra richiesta DNS vengono temporaneamente bloccati fino al completamento della richiesta DNS precedente.

Il client DNS di NetX Duo non usa i dati provenienti da risposte autorevoli per inoltrare query DNS aggiuntive ad altri server DNS.

## <a name="dns-rfcs"></a>RFC DNS

IL DNS di NetX Duo è conforme alle RFC seguenti:

- NOMI DI DOMINIO RFC1034 - CONCETTI E FUNZIONALITÀ
- NOMI DI DOMINIO RFC1035 - IMPLEMENTAZIONE E SPECIFICA
- RFC1480 Dominio degli Stati Uniti
- RFC 2782 A DNS RR for specifying the location of services (DNS SRV)
- RFC 3596 DNS Extensions to Support IP Version 6 (Estensioni DNS RFC 3596 per supportare IP versione 6)