---
title: Capitolo 4-Descrizione dei servizi MDN
description: Questo capitolo contiene una descrizione di tutti i servizi MDN NetX
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 89df0ab5f09be8ad50a27d23bae8b20d71caa0b4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821821"
---
# <a name="chapter-4---description-of-mdns-services"></a>Capitolo 4-Descrizione dei servizi MDN

Questo capitolo contiene una descrizione di tutti i servizi MDN NetX (elencati di seguito).

> [!NOTE]
> Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

## <a name="nx_mdns_create"></a>nx_mdns_create

Creare un'istanza di MDN

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

Questo servizio crea un'istanza MDN sull'istanza IP specifica e sulle risorse associate. Viene inoltre creato un thread per gestire i messaggi MDN in ingresso, rispondere alle query e trasmettere periodicamente messaggi di query.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **ip_ptr** Puntatore all'istanza IP associata.
- **packet_pool** Puntatore a un pool di pacchetti valido.
- **priorità** di Priorità del thread MDN.
- **stack_ptr** Puntatore all'area dello stack per il thread MDN
- **stack_size** Dimensioni dell'area dello stack.
- **HOST_NAME** Nome host assegnato a questo nodo.
- **local_service_cache** Spazio di archiviazione per servizi registrati locali.
- **local_service_cache_size** Dimensione della cache del servizio locale.
- **peer_service_cache** Spazio di archiviazione per le informazioni sul servizio ricevute
- **peer_service_cache_size** Dimensione della cache del servizio peer
- **probing_notify** Funzione di callback facoltativa richiamata alla fine dell'operazione di sondaggio. Invia una notifica all'applicazione indipendentemente dal fatto che il nome host (in caso di abilitazione di MDN in un'interfaccia locale) o il nome del servizio (dopo la registrazione di un servizio) sia univoco.

### <a name="return-values"></a>Valori restituiti

- L'istanza MDN è stata creata **NX_SUCCESS** (0x00).

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

Eliminare un'istanza MDN

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_delete(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina l'istanza MDN e libera le risorse.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha eliminato correttamente l'istanza MDN.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete a previously created mDNS instance. */

status = nx_mdns_delete(&my_mdns);

/* If status is NX_SUCCESS, the mDNS instance has been deleted. */
```

## <a name="nx_mdns_enable"></a>nx_mdns_enable

Avviare il servizio MDN

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_enable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a>Descrizione

Questa API Abilita il servizio MDN in un'interfaccia fisica specifica. Quando il servizio è abilitato, il modulo MDN verifica innanzitutto tutti i nomi di servizio univoci sulla rete prima di rispondere alle query ricevute sull'interfaccia.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo dell'istanza MDN.
- **interface_index** Indice dell'interfaccia in cui deve essere abilitato il servizio

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha abilitato correttamente il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Enable mDNS service on specific interface. */

status = nx_mdns_enable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was enabled. */
```

## <a name="nx_mdns_disable"></a>nx_mdns_disable

Disabilitare il servizio MDN

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_disable(NX_MDNS *mdns_ptr, UINT interface_index);
```

### <a name="description"></a>Descrizione

Questa API Disabilita il servizio MDN sull'interfaccia fisica specifica. Quando il servizio è disabilitato, MDN invia messaggi "Goodbye" per ogni servizio locale alla rete collegata all'interfaccia, in modo che i nodi adiacenti ricevano una notifica.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **interface_index** Indice dell'interfaccia in cui deve essere disabilitato il servizio

### <a name="return-values"></a>Valori restituiti

- Il servizio è stato disabilitato **NX_SUCCESS** (0x00).

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Disable mDNS service on specific interface. */

status = nx_mdns_disable(&my_mdns, 0);

/* If status is NX_SUCCESS, mDNS service was disabled. */
```

## <a name="nx_mdns_cache_notify_set"></a>nx_mdns_cache_notify_set

Installa la funzione di notifica completa della cache MDN

### <a name="prototype"></a>Prototipo

```c
UINT nx_mdns_cache_notify_set(NX_MDNS *mdns_ptr,
    VOID (*cache_full_notify_cb)(NX_MDNS *mdns_ptr,
        UINT state, UINT cache_type));
```

### <a name="description"></a>Descrizione

Questo servizio installa una funzione di callback fornita dall'utente, che viene richiamata quando la cache del servizio locale o la cache del servizio peer diventa piena. Quando la cache del servizio è completa, non è possibile aggiungere altri record di risorse MDN. Si noti che la cache del servizio può diventare piena a causa della frammentazione interna, quando vengono aggiunti e rimossi servizi con diverse lunghezze di stringa. Quando viene ricevuta una notifica completa della cache nella cache del servizio peer, l'applicazione può usare il servizio "*nx_mdns_service_cache_clear"* per cancellare tutte le voci nella cache del servizio peer.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha installato correttamente la funzione di callback Notify cache MDN.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Set mDNS cache notify callback. */

status = nx_mdns_cache_notify_set(&my_mdns, cache_full_nofiy_cb);

/* If status is NX_SUCCESS, mDNS cache notify callback was set. */
```

## <a name="nx_mdns_cache_notify_clear"></a>nx_mdns_cache_notify_clear

Cancella la funzione di notifica completa della cache del servizio MDN

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_cache_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Cancella una funzione di callback di notifica della cache del servizio fornita dall'utente.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha cancellato correttamente la funzione di callback Notify della cache del servizio MDN.

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

Questo servizio configura il nome di dominio locale predefinito. Quando viene creata l'istanza di MDN, il nome di dominio locale predefinito viene impostato su ". local". Questa API consente a un'applicazione di sovrascrivere il nome di dominio locale predefinito.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **Domain_name** Nome di dominio da utilizzare.

### <a name="return-values"></a>Valori restituiti

- Il dominio locale è stato configurato con **NX_SUCCESS** (0x00).

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

Questo servizio riconfigura i parametri di intervallo utilizzati da MDN durante l'invio degli annunci di servizio. Il periodo di pubblicazione *inizia da un segno di* graduazione e può essere espanso in modo telescopico con 2 alla potenza di *k* Factor. Il numero di ripetizioni per annuncio è *p*, l'intervallo tra ogni annuncio ripetuto è il ciclo di *intervallo* e il numero di periodi di annuncio max_time. Per impostazione predefinita, il periodo iniziale è impostato su 1 secondo, con k = 1 (il periodo raddoppia ogni volta), *p = 1* (nessuna ripetizione), retrans_interval = 0 (nessun intervallo di tempo), Period_interval = 0xFFFFFFFF (intervallo massimo periodo) e max_time = 3 (numero di annunci).

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **t** numero di cicli per il periodo iniziale. Il valore predefinito è 100 cicli per 1 secondo.
- numero **p** di ripetizioni. Il valore predefinito è 1.
- fattore telescopico **k** . Il valore predefinito è 1.
- **retrans_interval** Numero di cicli di attesa prima dell'invio di messaggi di annuncio ripetuti. Il valore predefinito è 0.
- **period_interval** Numero di cicli tra due periodi di annuncio. Il valore predefinito è 0xFFFFFFFF.
- **max_time** Numero di periodi di annuncio da utilizzare per l'annuncio. Dopo i periodi di annuncio *max_time* , non vengono inviati altri messaggi di annuncio. Il valore predefinito è 3.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) imposta correttamente i valori di intervallo.

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

Questa API registra un servizio offerto dall'applicazione. Se viene impostato il flag *is_unique* , MDN verifica il nome del servizio per assicurarsi che sia univoco nella rete locale prima di iniziare ad annunciare il servizio sulla rete. *Instance* è la parte dell'istanza del nome del servizio. Il *servizio* è la parte del servizio del nome del servizio. Ad esempio, "_http. _tcp" è un servizio. Per descrivere un servizio con sottotipo, il chiamante deve utilizzare il parametro del *sottotipo* . Ad esempio, se il servizio desiderato è "_printer. _sub. _http. _tcp", il campo del servizio è "_http. _tcp: e il campo del sottotipo è" _printer ".

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **istanza** di Puntatore al nome dell'istanza del servizio.
- **servizio** di Puntatore al tipo di servizio MDN, escluse le informazioni sul sottotipo.
- **sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.
- **priorità** di Priorità del servizio
- **peso** Peso del servizio
- **porta** Numero di porta TCP o UDP utilizzato dal servizio
- **testo** Informazioni aggiuntive sul testo
- **is_unique** Flag booleano che indica se il servizio è condiviso o univoco. Per i servizi registrati come univoci, gli MDN devono verificare il servizio sulla rete prima di iniziare a offrirlo.
- **Interface_index** Interfaccia fisica a cui viene offerto il servizio. Per un servizio offerto tramite uno dei servizi collegati, viene usato il valore *NX_MDNS_ALL_INTERFACES* .

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha registrato correttamente il servizio.

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

Questa API Elimina un servizio registrato precedente. Quando il servizio viene eliminato, i messaggi "Goodbye" vengono inviati alla rete locale, in modo che i nodi adiacenti ricevano una notifica.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **istanza** di Puntatore al nome dell'istanza del servizio.
- **servizio** di Puntatore al tipo di servizio MDN, escluse le informazioni sul sottotipo.
- **sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha eliminato correttamente il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Delete local service. */

status = nx_mdns_service_delete(&my_mdns, “NETX-SERVICE”, “_http._tcp”, NX_NULL);

/* If status is NX_SUCCESS, The service (NetX-SERVICE._http._tcp.local) was deleted. */
```

## <a name="nx_mdns_service_one_shot_query"></a>nx_mdns_service_one_shot_query

Avviare l'individuazione del servizio One-Shot

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_one_shot_query(NX_MDNS *mdns_ptr,
    UCHAR *instance,
    UCHAR *service,
    UCHAR *subtype,
    NX_MDNS_SERVICE *service_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio esegue una query MDN monouso. Se il servizio specificato viene trovato nella cache del servizio peer, viene restituita la prima istanza. Se non vengono trovati servizi nella cache del servizio peer locale, il modulo MDN emette un comando di query e attende la risposta. Il servizio è bloccato fino a quando non viene ricevuta la prima risposta o si verifica il timeout della query.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **istanza** di Puntatore al nome dell'istanza del servizio, se applicabile.
- **servizio** di Puntatore al tipo di servizio MDN, escluse le informazioni sul sottotipo. l'applicazione deve specificare il tipo di servizio.
- **sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.
- **service_ptr** Puntatore fornito dall'utente alla struttura NX_MDNS_SERVICE che archivia i risultati della query.
- **WAIT_OPTION** Quantità di tempo, espressa in cicli, per l'attesa di una risposta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha ottenuto correttamente le informazioni sul servizio.

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

Avviare l'individuazione continua del servizio

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_continous_query(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a>Descrizione

Questo servizio avvia una query continua. Si noti che il servizio viene restituito immediatamente. Dopo aver emesso una query continua, l'applicazione può recuperare il record di servizio usando l'API *nx_mdns_service_lookup*. Per arrestare la query continua, l'applicazione può usare l'API *nx_mdns_service_query_stop*

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **istanza** di Puntatore al nome dell'istanza del servizio, se applicabile.
- **servizio** di Puntatore al tipo di servizio MDN, escluse le informazioni sul sottotipo, se applicabile.
- **sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.

### <a name="return-values"></a>Valori restituiti

- La query continua è stata avviata **NX_SUCCESS** (0x00).

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

Interrompere l'individuazione di un servizio continuo emesso in precedenza

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_query_stop(NX_MDNS *mdns_ptr,
    CHAR *instance, CHAR *service, CHAR *subtype);
```

### <a name="description"></a>Descrizione

Questa API termina un'individuazione del servizio continua rilasciata in precedenza.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **istanza** di Puntatore al nome dell'istanza del servizio.
- **servizio** di Puntatore al tipo di servizio MDN, informazioni sul sottotipo.
- **sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha arrestato correttamente la query continua.

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

Questo servizio Cerca i servizi che corrispondono al nome dell'istanza (se specificati) e il tipo di servizio nella cache del servizio peer locale. L'applicazione deve avviare la ricerca del servizio con *instance_index* impostato su zero per il primo servizio nella cache che corrisponde alla descrizione. L'applicazione continuerà a usare questo servizio aumentando *instance_index* valore per i servizi aggiuntivi presenti nella cache, fino a quando il servizio non restituisce *NX_NO_MORE_ENTRIES*, che indica la fine della cache.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **istanza** di Puntatore al nome dell'istanza del servizio, se applicabile.
- **servizio** di Puntatore al tipo di servizio MDN, escluse le informazioni sul sottotipo, se applicabile.
- **sottotipo** Puntatore alla parte del sottotipo del servizio MDN, se applicabile.
- **Instance_index** Numero di indice dell'istanza da restituire.
- **service_ptr** Puntatore fornito dall'utente alla struttura NX_MDNS_SERVICE che archivia i risultati della ricerca.

### <a name="return-values"></a>Valori restituiti

- Il servizio è stato recuperato da **NX_SUCCESS** (0x00)
- **NX_NO_MORE_ENTRIES** (0x17) non viene trovata alcuna voce di servizio in corrispondenza del numero di indice specificato. Questo codice di errore indica la fine della ricerca.

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

Configura un set di ignoramenti del servizio

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_ignore_set(NX_MDNS *mdns_ptr, ULONG service_mask);
```

### <a name="description"></a>Descrizione

Questa API configura una maschera per ignorare i servizi specificati dalla maschera di maschera *service_mask* . L'utente può facoltativamente utilizzare il service_mask per selezionare i tipi di servizio che non si desidera memorizzare nella cache. Nella tabella *nx_mdns_service_types* in *nxd_mdns. c* viene definito un elenco di servizi. La maschera corrispondente del primo tipo di servizio in nx_mdns_service_types [] è 0x00000001, la maschera del secondo tipo di servizio è 0x00000002 e così via.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **service_mask** Tipi di servizio definiti dall'utente da ignorare. La maschera è un tipo ULONG a 32 bit. Ogni bit rappresenta una voce nella matrice *nx_mdns_service_types* definita dall'utente. Se viene impostato un bit, il tipo di servizio corrispondente specificato nella *nx_mdns_service_type* matrice non verrà archiviato nella cache del servizio peer.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) imposta correttamente il servizio ignora maschera.

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

Configura una funzione di callback per la notifica della modifica del servizio

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_notify_set(NX_MDNS *mdns_ptr, ULONG service_mask,
    VOID (*service_change_notify)(NX_MDNS *mdns_ptr,
    NX_MDNS_SERVICE *service_ptr, UINT state));
```

### <a name="description"></a>Descrizione

Questa API configura una funzione di callback di notifica della modifica del servizio. Questa funzione di callback viene richiamata quando un servizio offerto da altri nodi sulla rete viene aggiunto, modificato o non più disponibile. L'utente può facoltativamente utilizzare il service_mask per selezionare i tipi di servizio che si desidera monitorare. Un elenco di servizi monitorati è hardcoded nella tabella *nx_mdns_service_types* in *nxd_mdns. c.*

La maschera corrispondente del primo tipo di servizio in nx_mdns_service_types [] è 0x00000001, la maschera del secondo tipo di servizio è 0x00000002 e così via.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **service_mask** Tipi di servizio definiti dall'utente da monitorare. La maschera è un tipo ULONG a 32 bit. Ogni bit rappresenta una voce nella matrice *nx_mdns_service_types* .
- **service_change_notify** Funzione di callback da richiamare quando viene modificato il servizio specificato. Le informazioni dettagliate sul servizio vengono restituite nella memoria a cui punta *service_ptr.* Si noti che il contenuto nella memoria non è valido dopo la restituzione dalla funzione Notify callback.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha installato correttamente la funzione di callback.

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

Cancellare la funzione di callback notifica modifica servizio

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_service_notify_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Descrizione

Questa API Cancella la funzione di callback notifica di modifica del servizio e.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN..

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha cancellato correttamente la funzione di callback.

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

Questo servizio esegue una query MDN sugli indirizzi IPv4 e IPv6 host. Se l'indirizzo del nome host specificato si trova nella cache del servizio peer, viene restituito l'indirizzo. Se non viene trovato alcun indirizzo nella cache dei servizi peer, il modulo MDN rilascia una query di tipo e AAAA e attende la risposta. Questa API si blocca fino a quando non viene ricevuta una risposta o si verifica il timeout della query.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.
- **HOST_NAME** Puntatore al nome host.
- **Ipv4_address** Puntatore a un indirizzo allineato a 4 byte per lo spazio di archiviazione degli indirizzi IPv4. L'utente deve allocare 4 byte di spazio per l'indirizzo IPv4. NX_NULL indirizzo può essere passato all'API se non è necessario che l'applicazione recuperi l'indirizzo IPv4.
- **Ipv6_address** Puntatore all'indirizzo allineato a 4 byte per lo spazio di archiviazione degli indirizzi IPv6. L'utente deve allocare 16 byte di spazio per l'indirizzo IPv6. NX_NULL indirizzo può essere passato all'API se non è necessario che l'applicazione recuperi l'indirizzo IPv6.
- **WAIT_OPTION** Quantità di tempo, espressa in cicli, per l'attesa di una risposta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha ottenuto correttamente l'indirizzo host.

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

Cancella tutti i servizi locali

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_local_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Cancella tutte le voci nella cache del servizio locale dopo aver inviato il messaggio di addio.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha cancellato correttamente tutte le voci nella cache.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Clear the local cache, delete all local service. */

status = nx_mdns_local_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of local cache were deleted. */
```

## <a name="nx_mdns_peer_cache_clear"></a>nx_mdns_peer_cache_clear

Cancella tutti i servizi individuati

### <a name="prototype"></a>Prototipo

```C
UINT nx_mdns_peer_cache_clear(NX_MDNS *mdns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Cancella tutte le voci della cache dei servizi peer.

### <a name="input-parameters"></a>Parametri di input

- **mdns_ptr** Puntatore al blocco di controllo MDN.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha cancellato correttamente tutte le voci nella cache.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```C
/* Clear the peer cache, delete all peer service. */

status = nx_mdns_peer_cache_clear(&my_mdns);

/* If status is NX_SUCCESS, all services and resource records of peer cache were deleted. */
```
