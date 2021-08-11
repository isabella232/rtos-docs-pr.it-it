---
title: Capitolo 4 - Descrizione dei servizi mDNS
description: Questo capitolo contiene una descrizione di tutti i servizi MDNS NetX
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6e37698ac6023b4cff6cb4fc05330a73b678ef3d2a813a706c9b821381e123db
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797569"
---
# <a name="chapter-4---description-of-mdns-services"></a>Capitolo 4 - Descrizione dei servizi mDNS

Questo capitolo contiene una descrizione di tutti i servizi mDNS NetX (elencati di seguito).

> [!NOTE]
> Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

## <a name="nx_mdns_create"></a>nx_mdns_create

Creare un'istanza mDNS

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_create(NX_MDNS *mdns_ptr, NX_IP *ip_ptr,
    NX_PACKET_POOL *packet_pool,
    UINT priority, VOID *stack_ptr,
    UINT stack_size, UCHAR *host_name,
    VOID *local_service_cache,
    UINT local_service_cache_size,
    VOID *peer_service_cache,
    UINT peer_service_cache_size,
    VOID (*probing_notify)(NX_MDNS *mdns_ptr,
        UCHAR *name, UINT probing_state));
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza mDNS nell'istanza IP specifica e nelle risorse associate. Viene creato anche un thread per gestire i messaggi mDNS in ingresso, rispondere alle query e trasmettere periodicamente i messaggi di query.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **ip_ptr** Puntatore all'istanza IP associata.
- **packet_pool** Puntatore a un pool di pacchetti valido.
- **priorità** Priorità del thread mDNS.
- **stack_ptr** Puntatore all'area dello stack per il thread mDNS
- **stack_size** Dimensioni dell'area dello stack.
- **host_name** Nome host assegnato a questo nodo.
- **local_service_cache** Archiviazione spazio per i servizi registrati locali.
- **local_service_cache_size** Dimensioni della cache del servizio locale.
- **peer_service_cache** Archiviazione spazio per le informazioni sul servizio ricevute
- **peer_service_cache_size** Dimensioni della cache del servizio peer
- **probing_notify** Funzione di callback facoltativa richiamata alla fine dell'operazione di probe. Notifica all'applicazione se il nome host (quando si abilita mDNS in un'interfaccia locale) o il nome del servizio (dopo la registrazione di un servizio) è univoco.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Istanza mDNS creata correttamente.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
UCHAR stack_ptr[2048];
UCHAR local_cache_ptr[2048];
UCHAR peer_cache_ptr[8192];

/* Create a mDNS instance. */
status = nx_mdns_create(&my_mdns, &ip_0, &pool_0,
    3, stack_ptr, 2048,
    “NETX-MDNS-HOST”,
    local_cache_ptr, 2048,
    peer_cache_ptr, 8192,
    probing_notify);

/* If status is NX_SUCCESS, mDNS instance was created. */
```

## <a name="nx_mdns_delete"></a>nx_mdns_delete

Eliminare un'istanza mDNS

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_delete(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina l'istanza mDNS e libera le relative risorse.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'istanza mDNS è stata eliminata correttamente.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete a previously created mDNS instance. */

status = nx_mdns_delete(&my_mdns);

/* If status is NX_SUCCESS, the mDNS instance has been deleted. */
```

## <a name="nx_mdns_enable"></a>nx_mdns_enable

Avviare il servizio mDNS

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_enable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a>Descrizione

Questa API abilita il servizio mDNS su un'interfaccia fisica specifica. Dopo aver abilitato il servizio, il modulo mDNS esegue innanzitutto il probe di tutti i relativi nomi di servizio univoci nella rete prima di rispondere alle query ricevute sull'interfaccia.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo dell'istanza mDNS.
- **interface_index** Indice dell'interfaccia in cui deve essere abilitato il servizio

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il servizio è stato abilitato correttamente.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Enable mDNS service on specific interface. */

status = nx_mdns_enable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was enabled. */
```

## <a name="nx_mdns_disable"></a>nx_mdns_disable

Disabilitare il servizio mDNS

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_disable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a>Descrizione

Questa API disabilita il servizio mDNS nell'interfaccia fisica specifica. Dopo aver disabilitato il servizio, il servizio mDNS invia messaggi di "arrivederci" per ogni servizio locale alla rete collegata all'interfaccia, in modo che i nodi adiacenti siano informati.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **interface_index** Indice dell'interfaccia in cui deve essere disabilitato il servizio

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il servizio è stato disabilitato correttamente.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Disable mDNS service on specific interface. */

status = nx_mdns_disable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was disabled. */
```

## <a name="nx_mdns_cache_notify_set"></a>nx_mdns_cache_notify_set

Installa la funzione di notifica completa della cache mDNS

### <a name="prototype"></a>Prototipo

```c
UINT nx_mdns_cache_notify_set(NX_MDNS *mdns_ptr,
    VOID (*cache_full_notify_cb)(NX_MDNS *mdns_ptr,
        UINT state, UINT cache_type));
```

### <a name="description"></a>Descrizione

Questo servizio installa una funzione di callback fornita dall'utente, che viene richiamata quando la cache del servizio locale o la peer service cache diventa piena. Quando la cache del servizio è piena, non è possibile aggiungere più record di risorse mDNS. Si noti che la cache del servizio può diventare piena a causa della frammentazione interna, quando i servizi con lunghezze di stringa diverse vengono aggiunti e rimossi. Alla ricezione di una notifica completa della cache nella cache del servizio peer, l'applicazione può usare il servizio *"nx_mdns_service_cache_clear"* per cancellare tutte le voci nella cache del servizio peer.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) È stata installata correttamente la funzione di callback di notifica della cache mDNS.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set mDNS cache notify callback. */

status = nx_mdns_cache_notify_set(&my_mdns, cache_full_nofiy_cb);

/* If status is NX_SUCCESS, mDNS cache notify callback was set. */
```

## <a name="nx_mdns_cache_notify_clear"></a>nx_mdns_cache_notify_clear

Cancellare la funzione di notifica completa della cache del servizio mDNS

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_cache_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio cancella una funzione di callback di notifica della cache del servizio fornita dall'utente.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) La funzione di callback di notifica della cache del servizio mDNS è stata cancellata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Clear mDNS cache notify callback. */

status = nx_mdns_cache_notify_clear(&my_mdns);

/* If status is NX_SUCCESS, mDNS cache notify callback clear. */
```

## <a name="nx_mdns_domain_name_set"></a>nx_mdns_domain_name_set

Imposta il nome di dominio

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_domain_name_set(NX_MDNS *mdns_ptr, CHAR *domain_name);
```

### <a name="description"></a>Descrizione

Questo servizio configura il nome di dominio locale predefinito. Quando viene creata l'istanza di mDNS, il nome di dominio locale predefinito viene impostato su ".local". Questa API consente a un'applicazione di sovrascrivere il nome di dominio locale predefinito.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **domain_name** Nome di dominio da utilizzare.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Correttamente configurato il dominio locale.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the domain name. */

status = nx_mdns_domain_name_set(&my_mdns, “home”);

/* If status is NX_SUCCESS, the “home” domain name was set. */
```

## <a name="nx_mdns_service_announcement_timing_set"></a>nx_mdns_service_announcement_timing_set

Imposta i parametri di intervallo per i messaggi di annuncio del servizio

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_announcement_timing_set(NX_MDNS *mdns_ptr,
    UINT t, UINT p, UINT k, UINT retrans_interval,
    UINT period_interval, UINT max_time);
```

### <a name="description"></a>Descrizione

Questo servizio riconfigura i parametri di intervallo utilizzati da mDNS durante l'invio degli annunci del servizio. Il periodo di pubblicazione inizia *dai segni* di graduazione t e può essere espanso con 2 alla potenza del *fattore k.* Il numero di ripetizioni per annuncio è *p*  , l'intervallo tra ogni annuncio ripetuto è intervalli e il numero di periodi di annuncio è max_time. Per impostazione predefinita, il periodo iniziale è impostato su 1 secondo, con k = 1 (il periodo raddoppia ogni volta), *p = 1* (nessuna ripetizione), retrans_interval = 0 (nessun intervallo di tempo), period_interval = 0xFFFFFFFF (intervallo massimo periodo) e max_time = 3(numero di annunci).

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **t** Numero di tick per il periodo iniziale. Il valore predefinito è 100 tick per 1 secondo.
- **p** Numero di ripetizioni. Il valore predefinito è 1.
- **k** Fattore di disaffezione. Il valore predefinito è 1.
- **retrans_interval** Numero di tick da attendere prima di inviare messaggi di annuncio ripetuti. Il valore predefinito è 0.
- **period_interval** Numero di tick tra due periodi di annuncio. Il valore predefinito è 0xFFFFFFFF.
- **max_time** Numero di periodi di annuncio da usare per l'annuncio. Dopo i *max_time* di annuncio, non vengono inviati altri messaggi di annuncio. Il valore predefinito è 3.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Imposta correttamente i valori di intervallo.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the service announcement timing. */

status = nx_mdns_service_announcement_timing_set(&my_mdns, 100,
    1, 1, 0, 0xFFFFFFFF, 3);

/* If status is NX_SUCCESS, the service announcement timing was set. */
```

## <a name="nx_mdns_service_add"></a>nx_mdns_service_add

Aggiungere un servizio locale

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_add(NX_MDNS *mdns_ptr, CHAR *instance,
    CHAR *service, CHAR *subtype, UINT ttl, USHORT priority,
    USHORT weight, USHORT port, UCHAR *text, UCHAR is_unique,
    UINT interface_index);
```

### <a name="description"></a>Descrizione

Questa API registra un servizio offerto dall'applicazione. Se il flag *is_unique* impostato, mDNS effettua il probe del nome del servizio per assicurarsi che sia univoco nella rete locale prima di iniziare ad annunciare il servizio nella rete. *Istanza* è la parte dell'istanza del nome del servizio. Il *servizio* è la parte del servizio del nome del servizio. Ad esempio, "_http._tcp" è un servizio. Per descrivere un servizio con sottotipo, il chiamante deve usare il *parametro del sottotipo.* Ad esempio, se il servizio desiderato è "_printer._sub._http._tcp", il campo del servizio è "_http._tcp:, e il campo del sottotipo è "_printer".

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **istanza di** Puntatore al nome dell'istanza del servizio.
- **servizio** Puntatore al tipo di servizio mDNS, escluse le informazioni sul sottotipo.
- **sottotipo** Puntatore alla parte del sottotipo del servizio mDNS, se applicabile.
- **priorità** Priorità del servizio
- **peso** Peso del servizio
- **porta** Numero di porta TCP o UDP utilizzato dal servizio
- **text** Informazioni aggiuntive sul testo
- **is_unique** Flag booleano che indica se il servizio è condiviso o univoco. Per i servizi registrati come univoci, mDNS deve eseguire il probe del servizio in rete prima di iniziare a offrirlo.
- **Interface_index** Interfaccia fisica tramite cui viene offerto il servizio. Per un servizio offerto tramite uno dei servizi collegati, viene usato il valore *NX_MDNS_ALL_INTERFACES.*

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il servizio è stato registrato correttamente.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Add local service. */

status = nx_mdns_service_add(&my_mdns, “NETX-SERVICE”,
    “_http._tcp”, NX_NULL,
    NX_NULL, 0, 0, 0, 80, NX_TRUE, 0);

/* If status is NX_SUCCESS, The service (NetX-SERVICE._http._tcp.local) was added. */
```

## <a name="nx_mdns_service_delete"></a>nx_mdns_service_delete

Rimuovere un servizio registrato precedente

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_delete(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service,
    CHAR *subtype);
```

### <a name="description"></a>Descrizione

Questa API elimina un servizio registrato precedente. Quando il servizio viene eliminato, i messaggi "goodbye" vengono inviati alla rete locale in modo che i nodi adiacenti siano informati.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **istanza di** Puntatore al nome dell'istanza del servizio.
- **servizio** Puntatore al tipo di servizio mDNS, escluse le informazioni sul sottotipo.
- **sottotipo** Puntatore alla parte del sottotipo del servizio mDNS, se applicabile.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il servizio è stato eliminato correttamente.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete local service. */

status = nx_mdns_service_delete(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The service (NetX-SERVICE._http._tcp.local) was deleted. */
```

## <a name="nx_mdns_service_one_shot_query"></a>nx_mdns_service_one_shot_query

Avviare l'individuazione del servizio con un'unica operazione

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_one_shot_query(NX_MDNS *mdns_ptr,
    UCHAR *instance,
    UCHAR *service,
    UCHAR *subtype,
    NX_MDNS_SERVICE *service_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio esegue una query mDNS one-shot. Se il servizio specificato viene trovato nella peer service cache, viene restituita la prima istanza. Se non viene trovato alcun servizio nella cache del servizio peer locale, il modulo mDNS esegue un comando di query e attende la risposta. Il servizio viene bloccato fino alla ricezione della prima risposta o al timeout della query.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **istanza di** Puntatore al nome dell'istanza del servizio, se applicabile.
- **servizio** Puntatore al tipo di servizio mDNS, escluse le informazioni sul sottotipo. l'applicazione deve specificare il tipo di servizio.
- **sottotipo** Puntatore alla parte del sottotipo del servizio mDNS, se applicabile.
- **service_ptr** Puntatore fornito dall'utente NX_MDNS_SERVICE struttura che archivia i risultati della query.
- **wait_option** Intervallo di tempo, in tick, per l'attesa di una risposta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Le informazioni sul servizio sono state ottenute correttamente.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start service one shot query. */

status = nx_mdns_service_one_shot_query(&my_mdns, “NETX-SERVICE”, “_http._tcp”,
    NX_NULL, service_ptr, 500);

/* If status is NX_SUCCESS, The query with
    name: NetX-SERVICE._http._tcp.local,
     type: ANY (SRV and TXT) was sent.
    And the answer was stored in service_ptr if success. */
```

## <a name="nx_mdns_service_continuous_query"></a>nx_mdns_service_continuous_query

Avviare l'individuazione continua dei servizi

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_continous_query(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una query continua. Si noti che il servizio restituisce immediatamente . Dopo l'emissione di una query continua, l'applicazione può recuperare il record del servizio usando l'API *nx_mdns_service_lookup*. Per arrestare la query continua, l'applicazione può usare l'API *nx_mdns_service_query_stop*

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **istanza di** Puntatore al nome dell'istanza del servizio, se applicabile.
- **servizio** Puntatore al tipo di servizio mDNS, escluse le informazioni sul sottotipo, se applicabile.
- **sottotipo** Puntatore alla parte del sottotipo del servizio mDNS, se applicabile.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) La query viene avviata correttamente.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Start service continuous query. */

status = nx_mdns_service_continuous_query(&my_mdns,
    “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The continuous query with
    name: NetX-SERVICE._http._tcp.local,
    type: ANY (SRV and TXT) was added.
    And the query will be periodically sent. */
```

## <a name="nx_mdns_service_query_stop"></a>nx_mdns_service_query_stop

Cessare un'individuazione continua del servizio rilasciata in precedenza

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_query_stop(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a>Descrizione

Questa API termina un'individuazione del servizio continua rilasciata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **istanza di** Puntatore al nome dell'istanza del servizio.
- **servizio** Puntatore al tipo di servizio mDNS, informazioni sul sottotipo.
- **sottotipo** Puntatore alla parte del sottotipo del servizio mDNS, se applicabile.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Arresto riuscito continua la query.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Stop service continuous query. */

status = nx_mdns_service_query_stop(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The continuous query with
    name: NetX-SERVICE._http._tcp.local,
    type: ANY (SRV and TXT) was stopped. */
```

## <a name="nx_mdns_service_lookup"></a>nx_mdns_service_lookup

Recupera il servizio dalla cache del servizio peer locale

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_lookup(NXD_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service,
    CHAR *subtype, UINT instance_index,
    NXD_MDNS_SERVICE *service_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio cerca i servizi corrispondenti al nome dell'istanza (se specificato) e al tipo di servizio nella cache del servizio peer locale. L'applicazione avvia la ricerca *del servizio instance_index* impostata su zero per il primo servizio nella cache che corrisponde alla descrizione. L'applicazione continuerà *instance_index* usare questo servizio con un valore crescente per i servizi aggiuntivi trovati nella cache, finché il servizio non restituisce *NX_NO_MORE_ENTRIES*, che indica la fine della cache.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **istanza di** Puntatore al nome dell'istanza del servizio, se applicabile.
- **servizio** Puntatore al tipo di servizio mDNS, escluse le informazioni sul sottotipo, se applicabile.
- **sottotipo** Puntatore alla parte del sottotipo del servizio mDNS, se applicabile.
- **Instance_index** Numero di indice dell'istanza da restituire.
- **service_ptr** Puntatore fornito dall'utente NX_MDNS_SERVICE struttura che archivia i risultati della ricerca.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il servizio è stato recuperato correttamente
- **NX_NO_MORE_ENTRIES** (0x17) Non è stata trovata alcuna voce del servizio in corrispondenza del numero di indice specificato. Questo codice di errore indica la fine della ricerca.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Lookup the service on specific index. */

status = nx_mdns_service_lookup(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL,
    0, service_ptr);

/* If status is NX_SUCCESS, The service with
    name: NetX-SERVICE._http._tcp.local, was retrieved. */
```

## <a name="nx_mdns_service_ignore_set"></a>nx_mdns_service_ignore_set

Configura un set di ignorazioni del servizio

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_ignore_set(NX_MDNS *mdns_ptr, ULONG service_mask);
```

### <a name="description"></a>Descrizione

Questa API configura una maschera per ignorare i servizi specificati dalla maschera service_mask *bit.* L'utente può usare facoltativamente service_mask per selezionare i tipi di servizio che non vuole memorizzare nella cache. Un elenco di servizi è definito nella tabella *nx_mdns_service_types* in *nxd_mdns.c.* La maschera corrispondente del primo tipo di servizio in nx_mdns_service_types[] è 0x00000001, la maschera del secondo tipo di servizio è 0x00000002 e così via.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **service_mask** Tipi di servizio definiti dall'utente da ignorare. La maschera è un tipo ULONG a 32 bit. Ogni bit rappresenta una voce nella matrice di nx_mdns_service_types definita *dall'utente.* Se è impostato un bit, il tipo di servizio corrispondente specificato nella matrice *nx_mdns_service_type* non verrà memorizzato nella peer service cache.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Imposta correttamente la maschera di ignorare il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the service mask to ignore the specified service. */

status = nx_mdns_service_ignore_set(&my_mdns, 0x00000003);

/* If status is NX_SUCCESS, The service with
    type “_device-info” and “_http” will be ignored. */
```

## <a name="nx_mdns_service_notify_set"></a>nx_mdns_service_notify_set

Configura una funzione di callback di notifica delle modifiche del servizio

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_notify_set(NX_MDNS *mdns_ptr, ULONG service_mask,
    VOID (*service_change_notify)(NX_MDNS *mdns_ptr,
    NX_MDNS_SERVICE *service_ptr, UINT state));
```

### <a name="description"></a>Descrizione

Questa API configura una funzione di callback di notifica delle modifiche del servizio. Questa funzione di callback viene richiamata quando un servizio offerto da altri nodi nella rete viene aggiunto, modificato o non è più disponibile. L'utente può usare facoltativamente service_mask per selezionare i tipi di servizio da monitorare. Un elenco di servizi monitorati è hard-coded nella tabella nx_mdns_service_types *in* *nxd_mdns.c.*

La maschera corrispondente del primo tipo di servizio in nx_mdns_service_types[] è 0x00000001, la maschera del secondo tipo di servizio è 0x00000002 e così via.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **service_mask** Tipi di servizio definiti dall'utente da monitorare. La maschera è un tipo ULONG a 32 bit. Ogni bit rappresenta una voce nella *matrice nx_mdns_service_types.*
- **service_change_notify** Funzione di callback da richiamare quando viene modificato il servizio specificato. Le informazioni dettagliate sul servizio vengono restituite nella memoria a cui punta *service_ptr.* Si noti che il contenuto nella memoria non è valido dopo la restituzione dalla funzione di callback notify.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) La funzione di callback è stata installata correttamente.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set the service mask to notify the specified service. */

status = nx_mdns_service_notify_set(&my_mdns, 0x00000002, service_change_notify);

/* If status is NX_SUCCESS, the callback will be called
    if received the service with type “_http”. */
```

## <a name="nx_mdns_service_notify_clear"></a>nx_mdns_service_notify_clear

Cancellare la funzione di callback di notifica della modifica del servizio

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Descrizione

Questa API cancella la funzione di callback di notifica delle modifiche del servizio e .

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) La funzione di callback è stata cancellata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Clear the service notify. */

status = nx_mdns_service_notify_clear(&my_mdns);

/* If status is NX_SUCCESS, the service notify function clear. */
```

## <a name="nx_mdns_host_address_get"></a>nx_mdns_host_address_get

Ottenere l'indirizzo host

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_host_address_get(NX_MDNS *mdns_ptr,
    UCHAR *host_name, ULONG *ipv4_address,
    ULONG *ipv6_address, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio esegue una query mDNS sugli indirizzi IPv4 e IPv6 dell'host. Se l'indirizzo del nome host specificato viene trovato nella cache del servizio peer, viene restituito l'indirizzo. Se nella cache del servizio peer non viene trovato alcun indirizzo, il modulo mDNS esegue query di tipo A e AAAA e attende la risposta. Questa API si blocca fino a quando non viene ricevuta una risposta o non si verifica il timeout della query.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.
- **host_name** Puntatore al nome host.
- **ipv4_address** Puntatore a un indirizzo allineato a 4 byte per lo spazio di archiviazione degli indirizzi IPv4. L'utente deve allocare 4 byte di spazio per l'indirizzo IPv4 - . NX_NULL'indirizzo può essere passato a questa API se l'applicazione non deve recuperare l'indirizzo IPv4.
- **ipv6_address** Puntatore all'indirizzo allineato a 4 byte per lo spazio di archiviazione degli indirizzi IPv6. L'utente deve allocare 16 byte di spazio per l'indirizzo IPv6. NX_NULL'indirizzo può essere passato a questa API se l'applicazione non deve recuperare l'indirizzo IPv6.
- **wait_option** Tempo di attesa, in tick, di una risposta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) È stato ottenuto l'indirizzo host.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
ULONG ipv4_address;
ULONG ipv6_address[4];

/* Get the IP address of specified host. */
status = nx_mdns_host_address_get(&my_mdns, “MDNS-Host”, &ipv4_address, ipv6_address, 500);

/* If status is NX_SUCCESS, the IP address of specified host was retrieved. */
```

## <a name="nx_mdns_local_cache_clear"></a>nx_mdns_local_cache_clear

Cancellare tutti i servizi locali

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_local_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio cancella tutte le voci nella cache del servizio locale dopo l'invio del messaggio Goodbye.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Sono state cancellate tutte le voci nella cache.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Clear the local cache, delete all local service. */

status = nx_mdns_local_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of local cache were deleted. */
```

## <a name="nx_mdns_peer_cache_clear"></a>nx_mdns_peer_cache_clear

Cancellare tutti i servizi individuati

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_peer_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio cancella tutte le voci nella cache del servizio peer.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo mDNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Sono state cancellate tutte le voci nella cache.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Clear the peer cache, delete all peer service. */

status = nx_mdns_peer_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of peer cache were deleted. */
```
