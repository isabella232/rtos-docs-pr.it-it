---
title: Capitolo 4 - Descrizione dei Azure RTOS NetX Services
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f1ebbd4d78f96a257fc6cf62474917a1d618524ff6f27f99c108f904589f84fe
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116801938"
---
# <a name="chapter-4---description-of-azure-rtos-netx-services"></a>Capitolo 4 - Descrizione dei Azure RTOS NetX Services

Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX in ordine alfabetico. I nomi dei servizi sono progettati in modo da raggruppare tutti i servizi simili. Ad esempio, tutti i servizi ARP si trovano all'inizio di questo capitolo.

> [!NOTE]
> *Si noti che è disponibile BSD-Compatible API Socket per il codice dell'applicazione legacy che non può sfruttare appieno l'API NetX ad alte prestazioni. Fare riferimento all'appendice D per altre informazioni sull'API BSD-Compatible Socket.*

Nella sezione "Valori restituiti" di ogni descrizione i valori in **GRASSETTO** non sono interessati dall'opzione NX_DISABLE_ERROR_CHECKING usata per disabilitare il controllo degli errori dell'API, mentre i valori in grassetto non sono completamente disabilitati. Le sezioni "Allowed From" indicano da cui è possibile chiamare ogni servizio NetX.

## <a name="nx_arp_dynamic_entries_invalidate"></a>nx_arp_dynamic_entries_invalidate

Invalidare tutte le voci dinamiche nella cache ARP

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_dynamic_entries_invalidate(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invalida tutte le voci ARP dinamiche attualmente nella cache ARP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invalidazione della cache ARP completata.
- **NX_NOT_ENABLED** (0x14) ARP non è abilitato.
- **NX_PTR_ERROR** (0x07) Indirizzo IP non valido.
- **NX_CALLER_ERROR** (0x11) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Invalidate all dynamic entries in the ARP cache. */
status = nx_arp_dynamic_entries_invalidate(&ip_0);
/* If status is NX_SUCCESS the dynamic ARP entries were successfully invalidated. */
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entry_set, nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create, nx_arp_static_entry_delete

## <a name="nx_arp_dynamic_entry_set"></a>nx_arp_dynamic_entry_set

Impostare una voce ARP dinamica

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_dynamic_entry_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a>Descrizione

Questo servizio alloca una voce dinamica dalla cache ARP e configura il mapping dell'indirizzo IP specificato a quello fisico. Se viene specificato un indirizzo fisico pari a zero, viene inviata alla rete una richiesta ARP effettiva per risolvere l'indirizzo fisico. Si noti anche che questa voce verrà rimossa se il periodo di aging ARP è attivo o se la cache ARP è esaurita e si tratta della voce ARP usata meno di recente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP di cui eseguire il mapping.
- **physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico.
- **physical_lsw** 32 bit inferiori (31-0) dell'indirizzo fisico.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Set di voci dinamiche ARP riuscito.
- **NX_NO_MORE_ENTRIES** (0x17) Non sono disponibili altre voci ARP nella cache ARP.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) Puntatore di istanza IP non valido.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Setup a dynamic ARP entry on the previously created IP Instance 0. */
status = nx_arp_dynamic_entry_set(&ip_0, IP_ADDRESS(1,2,3,4),
    0x1022, 0x1234);
/* If status is NX_SUCCESS, there is now a dynamic mapping between
    the IP address of 1.2.3.4 and the physical hardware address of
    10:22:00:00:12:34. */
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate, nx_arp_enable,
- nx_arp_gratuitous_send, nx_arp_hardware_address_find,
- nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create, nx_arp_static_entry_delete

## <a name="nx_arp_enable"></a>nx_arp_enable

Abilita il protocollo ARP (Address Resolution Protocol).

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_enable(
    NX_IP *ip_ptr, 
    VOID *arp_cache_memory, 
    ULONG arp_cache_size);
```

### <a name="description"></a>Descrizione

Questo servizio inizializza il componente ARP di NetX per l'istanza IP specifica. L'inizializzazione ARP include la configurazione della cache ARP e varie routine di elaborazione ARP necessarie per l'invio e la ricezione di messaggi ARP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **arp_cache_memory** Puntatore all'area di memoria per inserire la cache ARP.
- **arp_cache_size** Ogni voce ARP è di 52 byte, il numero totale di voci ARP è quindi la dimensione divisa per 52.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ARP abilitato.
- **NX_PTR_ERROR** (0x07) Indirizzo IP o puntatore di memoria della cache non valido.
- **NX_SIZE_ERROR** (0x09) La memoria cache ARP fornita dall'utente è troppo piccola.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_ALREADY_ENABLED** (0x15) Questo componente è già stato abilitato.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Enable ARP and supply 1024 bytes of ARP cache memory for
    previously created IP Instance ip_0. */
status = nx_arp_enable(&ip_0, (void *) pointer, 1024);
/* If status is NX_SUCCESS, ARP was successfully enabled for this IP instance.*/
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_gratuitous_send, nx_arp_hardware_address_find,
- nx_arp_info_get, nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create, nx_arp_static_entry_delete

## <a name="nx_arp_gratuitous_send"></a>nx_arp_gratuitous_send

Inviare una richiesta ARP gratuita

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_gratuitous_send(
    NX_IP *ip_ptr,
    VOID (*response_handler) (NX_IP *ip_ptr, NX_PACKET *packet_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio passa attraverso tutte le interfacce fisiche per trasmettere richieste ARP gratuite, purché l'indirizzo IP dell'interfaccia sia valido. Se successivamente viene ricevuta una risposta ARP, il gestore della risposta fornito viene chiamato per elaborare la risposta al componente ARP gratuito.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **response_handler** Puntatore alla funzione di gestione della risposta. Se NX_NULL viene specificato , le risposte vengono ignorate.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio gratuito gratuito ARP.
- **NX_NO_PACKET** (0x01) Nessun pacchetto disponibile.
- **NX_NOT_ENABLED** (0x14) ARP non è abilitato.
- **NX_IP_ADDRESS_ERROR** (0x21) L'indirizzo IP corrente non è valido.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Caller non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Send gratuitous ARP without any response handler. */
status = nx_arp_gratuitous_send(&ip_0, NX_NULL);

/* If status is NX_SUCCESS the gratuitous ARP was successfully sent. */
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create, nx_arp_static_entry_delete

## <a name="nx_arp_hardware_address_find"></a>nx_arp_hardware_address_find

Individuare l'indirizzo hardware fisico dato un indirizzo IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_hardware_address_find(
    NX_IP *ip_ptr,
    ULONG ip_address, 
    ULONG *physical_msw, 
    ULONG *physical_lsw);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di trovare un indirizzo hardware fisico nella cache ARP associata all'indirizzo IP fornito.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP da cercare.
- **physical_msw** Puntatore alla variabile per restituire i primi 16 bit (47-32) dell'indirizzo fisico.
- **physical_lsw** Puntatore alla variabile per restituire i 32 bit inferiori (31-0) dell'indirizzo fisico.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Trovato indirizzo hardware ARP riuscito.
- **NX_ENTRY_NOT_FOUND** mapping (0x16) non è stato trovato nella cache ARP.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) IP o puntatore di memoria non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Search for the hardware address associated with the IP address of
    1.2.3.4 in the ARP cache of the previously created IP
    Instance 0. */
status = nx_arp_hardware_address_find(
    &ip_0, 
    IP_ADDRESS(1,2,3,4),
    &physical_msw, 
    &physical_lsw);

/* If status is NX_SUCCESS, the variables physical_msw and
    physical_lsw contain the hardware address.*/
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create, nx_arp_static_entry_delete

## <a name="nx_arp_info_get"></a>nx_arp_info_get

Recuperare informazioni sulle attività ARP

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_info_get(
    NX_IP *ip_ptr,
    ULONG *arp_requests_sent,
    ULONG *arp_requests_received,
    ULONG *arp_responses_sent,
    ULONG *arp_responses_received,
    ULONG *arp_dynamic_entries,
    ULONG *arp_static_entries,
    ULONG *arp_aged_entries,
    ULONG *arp_invalid_messages);
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle attività ARP per l'istanza IP associata.

*Se un puntatore di destinazione NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **arp_requests_sent** Puntatore alla destinazione per le richieste ARP totali inviate da questa istanza IP.
- **arp_requests_received** Puntatore alla destinazione per le richieste ARP totali ricevute dalla rete.
- **arp_responses_sent** Puntatore alla destinazione per le risposte ARP totali inviate da questa istanza IP.
- **arp_responses_received** Puntatore alla destinazione per le risposte ARP totali ricevute dalla rete.
- **arp_dynamic_entries** Puntatore alla destinazione per il numero corrente di voci ARP dinamiche.
- **arp_static_entries** Puntatore alla destinazione per il numero corrente di voci ARP statiche.
- **arp_aged_entries** Puntatore alla destinazione del numero totale di voci ARP che sono diventate non valide e che sono diventate obsolete.
- **arp_invalid_messages** Puntatore alla destinazione dei messaggi ARP non validi totali ricevuti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero delle informazioni ARP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Pickup ARP information for ip_0. */
status = nx_arp_info_get(
    &ip_0, 
    &arp_requests_sent,
    &arp_requests_received,
    &arp_responses_sent,
    &arp_responses_received,
    &arp_dynamic_entries,
    &arp_static_entries,
    &arp_aged_entries,
    &arp_invalid_messages);
/* If status is NX_SUCCESS, the ARP information has been stored in
    the supplied variables. */
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_ip_address_find,
- nx_arp_static_entries_delete, nx_arp_static_entry_create,
- nx_arp_static_entry_delete

## <a name="nx_arp_ip_address_find"></a>nx_arp_ip_address_find

Individuare l'indirizzo IP dato un indirizzo fisico

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_ip_address_find(
    NX_IP *ip_ptr, 
    ULONG *ip_address,
    ULONG physical_msw, 
    ULONG physical_lsw);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di trovare un indirizzo IP nella cache ARP associato all'indirizzo fisico fornito.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** Puntatore all'indirizzo IP restituito, se ne viene trovato uno mappato.
- **physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico da cercare.
- **physical_lsw** 32 bit inferiori (31-0) dell'indirizzo fisico da cercare.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Trovato indirizzo IP ARP riuscito
- **NX_ENTRY_NOT_FOUND** mapping (0x16) non è stato trovato nella cache ARP.
- **NX_PTR_ERROR** (0x07) IP o puntatore di memoria non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_INVALID_PARAMETERS** (0x4D) Physical_msw e physical_lsw sono entrambi 0.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Search for the IP address associated with the hardware address of
    0x0:0x01234 in the ARP cache of the previously created IP
    Instance ip_0. */
status = nx_arp_ip_address_find(&ip_0, &ip_address, 0x0, 0x1234);

/* If status is NX_SUCCESS, the variables ip_address contains the
    associated IP address.*/
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_static_entries_delete,nx_arp_static_entry_create,
- nx_arp_static_entry_delete

## <a name="nx_arp_static_entries_delete"></a>nx_arp_static_entries_delete

Eliminare tutte le voci ARP statiche

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_static_entries_delete(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina tutte le voci statiche nella cache ARP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Le voci statiche vengono eliminate.
- **NX_PTR_ERROR** (0x07) Puntatore ip_ptr non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Delete all the static ARP entries for IP Instance 0, assuming
    "ip_0" is the NX_IP structure for IP Instance 0. */

status = nx_arp_static_entries_delete(&ip_0);

/* If status is NX_SUCCESS all static ARP entries in the ARP cache
have been deleted. */
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entry_create,
- nx_arp_static_entry_delete

## <a name="nx_arp_static_entry_create"></a>nx_arp_static_entry_create

Creare un mapping da IP statico a hardware nella cache ARP

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_static_entry_create(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a>Descrizione

Questo servizio crea un mapping statico da IP a indirizzo fisico nella cache ARP per l'istanza IP specificata. Le voci ARP statiche non sono soggette a aggiornamenti periodici ARP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP di cui eseguire il mapping.
- **physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico da mappare.
- **physical_lsw** 32 bit inferiori (31-0) dell'indirizzo fisico di cui eseguire il mapping.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione della voce statica ARP completata.
- **NX_NO_MORE_ENTRIES** (0x17) Non sono disponibili altre voci ARP nella cache ARP.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_INVALID_PARAMETERS** (0x4D) Physical_msw e physical_lsw sono entrambi 0.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Create a static ARP entry on the previously created IP
    Instance 0. */

status = nx_arp_static_entry_create(&ip_0, IP_ADDRESS(1,2,3,4),
    0x0, 0x1234);

/* If status is NX_SUCCESS, there is now a static mapping between
    the IP address of 1.2.3.4 and the physical hardware address of
    00:00:00:00:12:34. */
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_delete

## <a name="nx_arp_static_entry_delete"></a>nx_arp_static_entry_delete

Eliminare l'indirizzo IP statico per il mapping hardware nella cache ARP


### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_static_entry_delete(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a>Descrizione

Questo servizio trova ed elimina un mapping statico da IP a indirizzo fisico creato in precedenza nella cache ARP per l'istanza IP specificata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP mappato in modo statico.
- **physical_msw** Primi 16 bit (47 - 32) dell'indirizzo fisico mappato in modo statico.
- **physical_lsw** 32 bit inferiori (31 - 0) dell'indirizzo fisico mappato in modo statico.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione della voce statica ARP completata.
- **NX_ENTRY_NOT_FOUND** (0x16) Voce ARP statica non trovata nella cache ARP.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido.
- **NX_INVALID_PARAMETERS** (0x4D) Physical_msw e physical_lsw sono entrambi 0.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Delete a static ARP entry on the previously created IP
    instance ip_0. */
status = nx_arp_static_entry_delete(&ip_0, IP_ADDRESS(1,2,3,4),
    0x0, 0x1234);
/* If status is NX_SUCCESS, the previously created static ARP entry
    was successfully deleted. */
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate, nx_arp_dynamic_entry_set,
- nx_arp_enable, nx_arp_gratuitous_send,
- nx_arp_hardware_address_find, nx_arp_info_get,
- nx_arp_ip_address_find, nx_arp_static_entries_delete,
- nx_arp_static_entry_create

## <a name="nx_icmp_enable"></a>nx_icmp_enable

Abilitare Internet Control Message Protocol (ICMP)

### <a name="prototype"></a>Prototipo

```C
UINT nx_icmp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio abilita il componente ICMP per l'istanza IP specificata.
Il componente ICMP è responsabile della gestione dei messaggi di errore Internet e delle richieste ping e delle risposte.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Abilita ICMP riuscito.
- **NX_ALREADY_ENABLED** (0x15) ICMP è già abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Enable ICMP on the previously created IP Instance ip_0. */
status = nx_icmp_enable(&ip_0);

/* If status is NX_SUCCESS, ICMP is enabled. */
```

### <a name="see-also"></a>Vedere anche

- nx_icmp_info_get, nx_icmp_ping

## <a name="nx_icmp_info_get"></a>nx_icmp_info_get

Recuperare informazioni sulle attività ICMP

### <a name="prototype"></a>Prototipo

```C
UINT nx_icmp_info_get(
    NX_IP *ip_ptr,
    ULONG *pings_sent,
    ULONG *ping_timeouts,
    ULONG *ping_threads_suspended,
    ULONG *ping_responses_received,
    ULONG *icmp_checksum_errors,
    ULONG *icmp_unhandled_messages);
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle attività ICMP per l'istanza IP specificata.

*Se un puntatore di destinazione NX_NULL, queste informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **pings_sent** Puntatore alla destinazione per il numero totale di ping inviati.
- **ping_timeouts** Puntatore alla destinazione per il numero totale di timeout ping.
- **ping_threads_suspended** Puntatore alla destinazione del numero totale di thread sospesi nelle richieste ping.
- **ping_responses_received** Puntatore all'estinazione del numero totale di risposte ping ricevute.
- **icmp_checksum_errors** Puntatore alla destinazione del numero totale di errori di checksum ICMP.
- **icmp_unhandled_messages** Puntatore all'estinazione del numero totale di messaggi ICMP non gestiti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero delle informazioni ICMP riuscito.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Retrieve ICMP information from previously created IP
    instance ip_0. */
status = nx_icmp_info_get(
    &ip_0, 
    &pings_sent, 
    &ping_timeouts,
    &ping_threads_suspended,
    &ping_responses_received,
    &icmp_checksum_errors,
    &icmp_unhandled_messages);

/* If status is NX_SUCCESS, ICMP information was retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_icmp_enable, nx_icmp_ping

## <a name="nx_icmp_ping"></a>nx_icmp_ping

Inviare una richiesta ping all'indirizzo IP specificato

### <a name="prototype"></a>Prototipo

```C
UINT nx_icmp_ping(
    NX_IP *ip_ptr,
    ULONG ip_address,
    CHAR *data, ULONG data_size,
    NX_PACKET **response_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia una richiesta ping all'indirizzo IP specificato e attende la quantità di tempo specificata per un messaggio di risposta ping. Se non viene ricevuta alcuna risposta, viene restituito un errore. In caso contrario, l'intero messaggio di risposta viene restituito nella variabile a cui punta response_ptr.

*Se NX_SUCCESS restituito, l'applicazione è responsabile del rilascio del pacchetto ricevuto dopo che non è più necessario.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP, in ordine di byte host, per eseguire il ping. data Puntatore all'area dati per il messaggio ping.
- **data_size** Numero di byte nei dati ping
- **response_ptr** Puntatore al puntatore a pacchetto in cui restituire il messaggio di risposta ping.
- **wait_option** Definisce per quanto tempo attendere una risposta ping. Le opzioni di attesa sono definite nel modo seguente:

  - NX_NO_WAIT (0x00000000)
  - NX_WAIT_FOREVER (0xFFFFFFFF)
  - valore di timeout in tick (0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ping riuscito. Il puntatore del messaggio di risposta è stato inserito nella variabile a cui punta response_ptr.
- **NX_NO_PACKET** (0x01) Impossibile allocare un pacchetto di richiesta ping.
- **NX_OVERFLOW** (0x03) L'area dati specificata supera le dimensioni predefinite del pacchetto per questa istanza IP.
- **NX_NO_RESPONSE** (0x29) L'INDIRIZZO IP richiesto non ha risposto.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) Indirizzo IP o puntatore di risposta non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Issue a ping to IP address 1.2.3.5 from the previously created IP
    Instance ip_0. */
status = nx_icmp_ping(&ip_0, IP_ADDRESS(1,2,3,5), "abcd", 4,
    &response_ptr, 10);

/* If status is NX_SUCCESS, a ping response was received from IP
    address 1.2.3.5 and the response packet is contained in the
    packet pointed to by response_ptr. It should have the same "abcd"
    four bytes of data. */
```

### <a name="see-also"></a>Vedere anche

- nx_icmp_enable, nx_icmp_info_get

## <a name="nx_igmp_enable"></a>nx_igmp_enable

Abilitare Internet Group Management Protocol (IGMP)

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio abilita il componente IGMP nell'istanza IP specificata.
Il componente IGMP è responsabile del supporto per le operazioni di gestione dei gruppi multicast IP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Abilita IGMP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_ALREADY_ENABLED** (0x15) Questo componente è già stato abilitato.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Enable IGMP on the previously created IP Instance ip_0. */
status = nx_igmp_enable(&ip_0);

/* If status is NX_SUCCESS, IGMP is enabled. */
```

### <a name="see-also"></a>Vedere anche

- nx_igmp_info_get,nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,
- nx_igmp_multicast_join, nx_igmp_multicast_leave

## <a name="nx_igmp_info_get"></a>nx_igmp_info_get

Recuperare informazioni sulle attività IGMP

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_info_get(
    NX_IP *ip_ptr,
    ULONG *igmp_reports_sent,
    ULONG *igmp_queries_received,
    ULONG *igmp_checksum_errors,
    ULONG *current_groups_joined);
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle attività IGMP per l'istanza IP specificata.

*Se un puntatore di destinazione NX_NULL, queste informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **igmp_reports_sent** Puntatore alla destinazione per il numero totale di report ICMP inviati.
- **igmp_queries_received** Puntatore alla destinazione per il numero totale di query ricevute dal router multicast.
- **igmp_checksum_errors** Puntatore alla destinazione del numero totale di errori di checksum IGMP nei pacchetti di ricezione.
- **current_groups_joined** Puntatore alla destinazione del numero corrente di gruppi uniti tramite questa istanza IP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero delle informazioni IGMP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Retrieve IGMP information
    from previously created IP Instance ip_0. */
status = nx_igmp_info_get(
    &ip_0, 
    &igmp_reports_sent,
    &igmp_queries_received,
    &igmp_checksum_errors,
    &current_groups_joined);
/* If status is NX_SUCCESS, IGMP information was retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_igmp_enable, nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,
- nx_igmp_multicast_join, nx_igmp_multicast_leave

## <a name="nx_igmp_loopback_disable"></a>nx_igmp_loopback_disable

Disabilitare il loopback IGMP

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_loopback_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita il loopback IGMP per tutti i gruppi multicast successivi aggiunti.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Fail IGMP loopback disable (Disabilitazione loopback IGMP riuscita).
- **NX_NOT_ENABLED** (0x14) IGMP non è abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** chiamante (0x11) non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Disable IGMP loopback for all subsequent multicast groups joined. */
status = nx_igmp_loopback_disable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is disabled. */
```

### <a name="see-also"></a>Vedere anche

- nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_enable,
- nx_igmp_multicast_interface_join, nx_igmp_multicast_join,
- nx_igmp_multicast_leave

## <a name="nx_igmp_loopback_enable"></a>nx_igmp_loopback_enable

Abilitare il loopback IGMP

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_loopback_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio abilita il loopback IGMP per tutti i gruppi multicast successivi aggiunti.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Fail IGMP loopback disable (Disabilitazione loopback IGMP riuscita).
- **NX_NOT_ENABLED** (0x14) IGMP non è abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** chiamante (0x11) non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Enable IGMP loopback for all subsequent multicast groups joined. */
status = nx_igmp_loopback_enable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is enabled. */
```

### <a name="see-also"></a>Vedere anche

- nx_igmp_enable, nx_igmp_info_get,nx_igmp_loopback_disable,
- nx_igmp_multicast_interface_join, nx_igmp_multicast_join,
- nx_igmp_multicast_leave

## <a name="nx_igmp_multicast_interface_join"></a>nx_igmp_multicast_interface_join

Aggiungere un'istanza IP a un gruppo multicast specificato tramite un'interfaccia

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_multicast_interface_join(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un'istanza IP al gruppo multicast specificato tramite un'interfaccia di rete specificata. Viene mantenuto un contatore interno per tenere traccia del numero di volte in cui lo stesso gruppo è stato unito. Dopo l'aggiunta al gruppo multicast, il componente IGMP consentirà la ricezione di pacchetti IP con questo indirizzo di gruppo tramite l'interfaccia di rete specificata e segnalerà anche ai router che questo indirizzo IP è membro di questo gruppo multicast. I messaggi di appartenenza, report e uscita IGMP vengono inviati anche tramite l'interfaccia di rete specificata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **group_address** Indirizzo del gruppo multicast IP di classe D da aggiungere nell'ordine dei byte dell'host.
- **interface_index** Indice dell'interfaccia associata all'istanza di NetX.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Join a gruppi multicast riuscito.
- **NX_NO_MORE_ENTRIES** (0x17) Non è possibile aggiungere altri gruppi multicast, il massimo è stato superato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_INVALID_INTERFACE** (0x4C) L'indice del dispositivo punta a un'interfaccia di rete non valida.
- **NX_IP_ADDRESS_ERROR** indirizzo del gruppo multicast (0x21) specificato non è un indirizzo di classe D valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** il supporto multicast IP (0x14) IP non è abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Previously created IP Instance joins the multicast group
    244.0.0.200, via the interface at index 1 in the IP interface list. */
#define INTERFACE_INDEX 1
status = nx_igmp_multicast_interface_join
    (&ip, IP_ADDRESS(244,0,0,200),
    INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully joined
    the multicast group. */
```

### <a name="see-also"></a>Vedere anche

- nx_igmp_enable, nx_igmp_info_get,nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_join,
- nx_igmp_multicast_leave

## <a name="nx_igmp_multicast_join"></a>nx_igmp_multicast_join

Aggiungere l'istanza IP al gruppo multicast specificato

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_multicast_join(
    NX_IP *ip_ptr, 
    ULONG group_address);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un'istanza IP al gruppo multicast specificato. Viene mantenuto un contatore interno per tenere traccia del numero di volte in cui lo stesso gruppo è stato unito. Al driver viene richiesto di inviare un report IGMP se si tratta della prima richiesta di join in rete che indica l'intenzione dell'host di partecipare al gruppo. Dopo l'aggiunta, il componente IGMP consentirà la ricezione di pacchetti IP con questo indirizzo di gruppo e segnalerà ai router che questo indirizzo IP è membro di questo gruppo multicast.

> [!NOTE]
> *Per aggiungere un gruppo multicast in un dispositivo non primario, usare il servizio **nx_igmp_multicast_interface_join.***

- **Parametri**

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **group_address** Indirizzo del gruppo multicast IP di classe D da aggiungere.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Join a gruppi multicast riuscito.
- **NX_NO_MORE_ENTRIES** (0x17) Non è possibile aggiungere altri gruppi multicast, il massimo è stato superato.
- **NX_INVALID_INTERFACE** (0x4C) L'indice del dispositivo punta a un'interfaccia di rete non valida.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo del gruppo IP non valido.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Previously created IP Instance ip_0 joins the multicast group
    224.0.0.200. */
status = nx_igmp_multicast_join(&ip_0, IP_ADDRESS(224,0,0,200));

/* If status is NX_SUCCESS, this IP instance has successfully
    joined the multicast group 224.0.0.200. */
```

### <a name="see-also"></a>Vedere anche

- nx_igmp_enable, nx_igmp_info_get,nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,
- nx_igmp_multicast_leave

## <a name="nx_igmp_multicast_leave"></a>nx_igmp_multicast_leave

Fare in modo che l'istanza IP lasci il gruppo multicast specificato

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_multicast_leave(
    NX_IP *ip_ptr, 
    ULONG group_address);
```

### <a name="description"></a>Descrizione

Questo servizio fa in modo che un'istanza IP lasci il gruppo multicast specificato, se il numero di richieste leave corrisponde al numero di richieste di join. In caso contrario, il conteggio dei join interni viene semplicemente decrementato.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **group_address** Gruppo multicast da lasciare.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta al gruppo multicast riuscita.
- **NX_ENTRY_NOT_FOUND** (0x16) Richiesta di join precedente non trovata.
- **NX_INVALID_INTERFACE** (0x4C) L'indice del dispositivo punta a un'interfaccia di rete non valida.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo del gruppo IP non valido.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Cause IP instance to leave the multicast group 224.0.0.200. */
status = nx_igmp_multicast_leave(&ip_0, IP_ADDRESS(224,0,0,200);

/* If status is NX_SUCCESS, this IP instance has successfully left
    the multicast group 224.0.0.200. */
```
### <a name="see-also"></a>Vedere anche

- nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,
- nx_igmp_multicast_join

## <a name="nx_ip_address_change_notifiy"></a>nx_ip_address_change_notifiy

Notificare all'applicazione se l'indirizzo IP cambia


### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_address_change_notify(
    NX_IP *ip_ptr,
    VOID(*change_notify)(NX_IP *,VOID *),
    VOID *additional_info);
```

### <a name="description"></a>Descrizione

Questo servizio registra una funzione di notifica dell'applicazione che viene chiamata ogni volta che viene modificato l'indirizzo IP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **change_notify** Puntatore alla funzione di notifica delle modifiche IP. Se questo parametro è NX_NULL, la notifica di modifica dell'indirizzo IP è disabilitata.
- **additional_info** Puntatore a informazioni aggiuntive facoltative che vengono fornite anche alla funzione di notifica quando viene modificato l'indirizzo IP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Notifica di modifica dell'indirizzo IP completata.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Register the function "my_ip_changed" to be called whenever
the IP address is changed. */
status = nx_ip_address_change_notify(&ip_0, my_ip_changed, NX_NULL);

/* If status is NX_SUCCESS, the "my_ip_changed" function will be
    called whenever the IP address changes. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_get, nx_ip_address_set, nx_ip_create, nx_ip_delete,
- nx_ip_driver_direct_command, nx_ip_driver_interface_direct_command,
- nx_ip_forwarding_disable, nx_ip_forwarding_enable,
- nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_address_get"></a>nx_ip_address_get

Recuperare l'indirizzo IP e network mask

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_address_get(
    NX_IP *ip_ptr,
    ULONG *ip_address,
    ULONG *network_mask);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IP e il subnet mask'interfaccia di rete primaria.

*Per ottenere informazioni sul dispositivo secondario, usare il servizio
- **nx_ip_interface_address_get**.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** Puntatore alla destinazione per l'indirizzo IP.
- **network_mask** Puntatore alla destinazione per network mask.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ottenere l'indirizzo IP corretto.
- **NX_PTR_ERROR** (0x07) Ip non valido o puntatore a variabile restituita.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Get the IP address and network mask from the previously created
    IP Instance ip_0. */
status = nx_ip_address_get(&ip_0,
    &ip_address, &network_mask);

/* If status is NX_SUCCESS, the variables ip_address and
    network_mask contain the IP and network mask respectively. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_set, nx_ip_create,
- nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,
- nx_system_initialize

## <a name="nx_ip_address_set"></a>nx_ip_address_set

Impostare l'indirizzo IP e network mask

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_address_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG network_mask);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP e network mask per l'interfaccia di rete primaria.

*Per impostare l'indirizzo IP e network mask per il dispositivo secondario, usare il servizio **nx_ip_interface_address_set**.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** Nuovo indirizzo IP.
- **network_mask** Nuovo network mask.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'indirizzo IP è stato impostato correttamente.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Set the IP address and network mask to 1.2.3.4 and 0xFFFFFF00
    for the previously created IP Instance ip_0. */
status = nx_ip_address_set(&ip_0, IP_ADDRESS(1,2,3,4), 0xFFFFFF00UL);

/* If status is NX_SUCCESS, the IP instance now has an IP address
    of 1.2.3.4 and a network mask of 0xFFFFFF00. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_create,
- nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,
- nx_system_initialize

## <a name="nx_ip_create"></a>nx_ip_create

Creare un'istanza IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_create(
    NX_IP *ip_ptr, 
    CHAR *name, 
    ULONG ip_address,
    ULONG network_mask, 
    NX_PACKET_POOL *default_pool,
    VOID (*ip_network_driver)(NX_IP_DRIVER *),
    VOID *memory_ptr, 
    ULONG memory_size,
    UINT priority);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza IP con l'indirizzo IP e il driver di rete specificati dall'utente. Inoltre, l'applicazione deve fornire un pool di pacchetti creato in precedenza per l'istanza IP da usare per l'allocazione interna dei pacchetti. Si noti che il driver di rete dell'applicazione fornito non viene chiamato fino all'esecuzione del thread di questo indirizzo IP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore al blocco di controllo per creare una nuova istanza IP.
- **name** Nome della nuova istanza IP.
- **ip_address** Indirizzo IP per questa nuova istanza IP.
- **network_mask** Maschera per delineare la parte di rete dell'indirizzo IP per gli usi di rete secondaria e super-rete.
- **default_pool** Puntatore al blocco di controllo del pool di pacchetti NetX creato in precedenza.
- **ip_network_driver** Driver di rete fornito dall'utente usato per inviare e ricevere pacchetti IP.
- **memory_ptr** Puntatore all'area di memoria per l'area dello stack del thread helper IP.
- **memory_size** Numero di byte nell'area di memoria per lo stack del thread helper IP.
- **priorità** Priorità del thread helper IP.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Creazione dell'istanza IP riuscita.
- **NX_NOT_IMPLEMENTED** libreria NetX (0x4A) non è configurata correttamente.
- **NX_PTR_ERROR** (0x07) IP non valido, puntatore a funzione del driver di rete, pool di pacchetti o puntatore di memoria.
- **NX_SIZE_ERROR** (0x09) La dimensione dello stack fornita è troppo piccola.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_IP_ADDRESS_ERROR** (0x21) L'indirizzo IP specificato non è valido.
- **NX_OPTION_ERROR** (0x21) La priorità del thread IP specificata non è valida.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Create an IP instance with an IP address of 1.2.3.4 and a network
    mask of 0xFFFFFF00UL. The "ethernet_driver" specifies the entry
    point of the application specific network driver and the
    "stack_memory_ptr" specifies the start of a 1024 byte memory
    area that is used for this IP instance’s helper thread.  */
status = nx_ip_create(
    &ip_0, 
    "NetX IP Instance ip_0",
    IP_ADDRESS(1, 2, 3, 4),
    0xFFFFFF00UL, &pool_0, 
    ethernet_driver,
    stack_memory_ptr, 
    1024, 
    1);

/* If status is NX_SUCCESS, the IP instance has been created. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,
- nx_system_initialize

## <a name="nx_ip_delete"></a>nx_ip_delete

Eliminare un'istanza IP creata in precedenza


### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_delete(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza IP creata in precedenza e rilascia tutte le risorse di sistema di proprietà dell'istanza IP.

### <a name="parameters"></a>Parametri
- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione ip riuscita.
- **NX_SOCKETS_BOUND** (0x28) A questa istanza IP sono ancora associati socket UDP o TCP. Tutti i socket devono essere non associati ed eliminati prima di eliminare l'istanza IP.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
/* Delete a previously created IP instance. */
status = nx_ip_delete(&ip_0);

/* If status is NX_SUCCESS, the IP instance has been deleted. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check,
- nx_system_initialize

## <a name="nx_ip_driver_direct_command"></a>nx_ip_driver_direct_command

Eseguire il comando per il driver di rete

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_driver_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    ULONG *return_value_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio fornisce un'interfaccia diretta al driver di interfaccia di rete primario dell'applicazione specificato durante la ***nx_ip_create*** chiamata.

È possibile usare comandi specifici dell'applicazione specificando che il valore numerico è maggiore o uguale a NX_LINK_USER_COMMAND.

*Per eseguire il comando per il dispositivo secondario, usare **il nx_ip_driver_interface_direct_command** secondario.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **comando** Codice di comando numerico. I comandi standard sono definiti come segue:

- NX_LINK_GET_STATUS (10)
- NX_LINK_GET_SPEED (11)
- NX_LINK_GET_DUPLEX_TYPE (12)
- NX_LINK_GET_ERROR_COUNT (13)
- NX_LINK_GET_RX_COUNT (14)
- NX_LINK_GET_TX_COUNT (15)
- NX_LINK_GET_ALLOC_ERRORS (16)
- NX_LINK_USER_COMMAND (50)

- **return_value_ptr** Puntatore alla variabile restituita nel chiamante.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Comando diretto del driver di rete riuscito.
- **NX_UNHANDLED_COMMAND** comando (0x44) Unhandled or unimplemented network driver (Driver di rete non gestito o non implementata).
- **NX_PTR_ERROR** (0x07) Ip non valido o puntatore al valore restituito.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_INVALID_INTERFACE** (0x4C) Indice di interfaccia non valido.

### <a name="allowed-from"></a>Consentito da

Thread

- **Possibile preemption**

No

### <a name="example"></a>Esempio

```C
/* Make a direct call to the application-specific network driver
    for the previously created IP instance. For this example, the
    network driver is interrogated for the link status. */
status = nx_ip_driver_direct_command(
    &ip_0, NX_LINK_GET_STATUS,
    &link_status);

/* If status is NX_SUCCESS, the link_status variable contains a
    NX_TRUE or NX_FALSE value representing the status of the
    physical link. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_interface_direct_command,
- nx_ip_forwarding_disable, nx_ip_forwarding_enable,
- nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_driver_interface_direct_command"></a>nx_ip_driver_interface_direct_command

Eseguire il comando per il driver di rete

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_driver_interface_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    UINT interface_index,
    ULONG *return_value_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio fornisce un comando diretto al driver di dispositivo di rete dell'applicazione nell'istanza IP. È possibile usare comandi specifici dell'applicazione specificando che il valore numerico è maggiore o uguale *NX_LINK_USER_COMMAND*.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **comando** Codice di comando numerico. I comandi standard sono definiti come segue:
- NX_LINK_GET_STATUS (10)
- NX_LINK_GET_SPEED (11)
- NX_LINK_GET_DUPLEX_TYPE (12)
- NX_LINK_GET_ERROR_COUNT (13)
- NX_LINK_GET_RX_COUNT (14)
- NX_LINK_GET_TX_COUNT (15)
- NX_LINK_GET_ALLOC_ERRORS (16)
- NX_LINK_USER_COMMAND (50)
- **interface_index** Indice dell'interfaccia di rete a cui deve essere inviato il comando.
- **return_value_ptr** Puntatore alla variabile restituita nel chiamante.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Comando diretto del driver di rete riuscito.
- **NX_UNHANDLED_COMMAND** comando (0x44) Unhandled or unimplemented network driver (Driver di rete non gestito o non implementata).
- **NX_INVALID_INTERFACE** (0x4C) Indice di interfaccia non valido
- **NX_PTR_ERROR** (0x07) Ip non valido o puntatore al valore restituito.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Make a direct call to the application-specific network driver
    for the previously created IP instance. For this example, the
    network driver is interrogated for the link status. */

/* Set the interface index to the primary device. */
UINT interface_index = 0;
    status = nx_ip_driver_interface_direct_command(&ip_0,
    NX_LINK_GET_STATUS,
    interface_index,
    &link_status);
/* If status is NX_SUCCESS, the link_status variable contains a
    NX_TRUE or NX_FALSE value representing the status of the
    physical link. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_forwarding_disable, nx_ip_forwarding_enable,
- nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_forwarding_disable"></a>nx_ip_forwarding_disable

Disabilitare l'inoltro di pacchetti IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_forwarding_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita l'inoltro di pacchetti IP all'interno del componente IP NetX. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Disabilitazione dell'inoltro IP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Disable IP forwarding on this IP instance. */
status = nx_ip_forwarding_disable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been disabled on the
    previously created IP instance. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_enable,
- nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_forwarding_enable"></a>nx_ip_forwarding_enable

Abilitare l'inoltro di pacchetti IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_forwarding_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio consente l'inoltro di pacchetti IP all'interno del componente IP NetX. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) L'inoltro IP è riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Enable IP forwarding on this IP instance. */
status = nx_ip_forwarding_enable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been enabled on the
    previously created IP instance. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_fragment_disable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_fragment_disable"></a>nx_ip_fragment_disable

Disabilitare la frammentazione dei pacchetti IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_fragment_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita la frammentazione e il riassemblamento dei pacchetti IP. Per i pacchetti in attesa di essere riassemblati, questo servizio rilascia questi pacchetti. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Il frammento IP è stato disabilitato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) la frammentazione IP non è abilitata nell'istanza IP.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Disable IP fragmenting on this IP instance. */
status = nx_ip_fragment_disable(&ip_0);

/* If status is NX_SUCCESS, disables IP fragmenting on the
    previously created IP instance. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_enable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_fragment_enable"></a>nx_ip_fragment_enable

Abilitare la frammentazione dei pacchetti IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_fragment_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio abilita la funzionalità di frammentazione e riassemblamento dei pacchetti IP. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Correttamente abilitato il frammento IP.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** funzionalità 0x14 frammentazione IP non vengono compilate in NetX.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Enable IP fragmenting on this IP instance. */
status = nx_ip_fragment_enable(&ip_0);

/* If status is NX_SUCCESS, IP fragmenting has been enabled on the
    previously created IP instance. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable, nx_ip_info_get,
- nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_gateway_address_set"></a>nx_ip_gateway_address_set

Impostare l'indirizzo IP del gateway

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_gateway_address_set(
    NX_IP *ip_ptr, 
    ULONG ip_address);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP del gateway IP. Tutto il traffico fuori rete viene instradato a questo gateway per la trasmissione. Il gateway deve essere accessibile direttamente tramite una delle interfacce di rete.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP del gateway.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'indirizzo IP del gateway è stato impostato correttamente.
- **NX_PTR_ERROR** (0x07) Puntatore all'istanza IP non valido.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Setup the Gateway address for previously created IP
    Instance ip_0. */
status = nx_ip_gateway_address_set(&ip_0, IP_ADDRESS(1,2,3,99));

/* If status is NX_SUCCESS, all out-of-network send requests are
    routed to 1.2.3.99. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_info_get, nx_ip_static_route_add, nx_ip_static_route_delete

## <a name="nx_ip_info_get"></a>nx_ip_info_get

Recuperare informazioni sulle attività IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_info_get(
    NX_IP *ip_ptr,
    ULONG *ip_total_packets_sent,
    ULONG *ip_total_bytes_sent,
    ULONG *ip_total_packets_received,
    ULONG *ip_total_bytes_received,
    ULONG *ip_invalid_packets,
    ULONG *ip_receive_packets_dropped,
    ULONG *ip_receive_checksum_errors,
    ULONG *ip_send_packets_dropped,
    ULONG *ip_total_fragments_sent,
    ULONG *ip_total_fragments_received);
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle attività IP per l'istanza IP specificata.

*Se un puntatore di destinazione NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_total_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti IP inviati.
- **ip_total_bytes_sent** Puntatore alla destinazione per il numero totale di byte inviati.
- **ip_total_packets_received** Puntatore alla destinazione del numero totale di pacchetti di ricezione IP.
- **ip_total_bytes_received** Puntatore alla destinazione del numero totale di byte IP ricevuti.
- **ip_invalid_packets** Puntatore alla destinazione del numero totale di pacchetti IP non validi.
- **ip_receive_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di ricezione eliminati.
- **ip_receive_checksum_errors** Puntatore alla destinazione del numero totale di errori di checksum nei pacchetti di ricezione.
- **ip_send_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di invio eliminati.
- **ip_total_fragments_sent** Puntatore alla destinazione del numero totale di frammenti inviati.
- **ip_total_fragments_received** Puntatore alla destinazione del numero totale di frammenti ricevuti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero delle informazioni IP riuscito.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Retrieve IP information from previously created IP
Instance 0. */
status = nx_ip_info_get(&ip_0,
    &ip_total_packets_sent,
    &ip_total_bytes_sent,
    &ip_total_packets_received,
    &ip_total_bytes_received,
    &ip_invalid_packets,
    &ip_receive_packets_dropped,
    &ip_receive_checksum_errors,
    &ip_send_packets_dropped,
    &ip_total_fragments_sent,
    &ip_total_fragments_received);

/* If status is NX_SUCCESS, IP information was retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_status_check, nx_system_initialize

## <a name="nx_ip_interface_address_get"></a>nx_ip_interface_address_get

Recuperare l'indirizzo IP dell'interfaccia

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_interface_address_get (
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG *ip_address,
    ULONG *network_mask);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IP di un'interfaccia di rete specificata.

*Il dispositivo specificato, se non il dispositivo primario, deve essere collegato in precedenza all'istanza IP.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **interface_index** Indice dell'interfaccia, lo stesso valore dell'indice dell'interfaccia di rete collegata all'istanza IP.
- **ip_address** Puntatore alla destinazione per l'indirizzo IP dell'interfaccia del dispositivo.
- **network_mask** Puntatore alla destinazione per l'interfaccia network mask.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ottenere l'indirizzo IP corretto.
- **NX_INVALID_INTERFACE** (0x4C) L'interfaccia di rete specificata non è valida.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
#define INTERFACE_INDEX 1
/* Get device IP address and network mask for the specified
    interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_get(ip_ptr,INTERFACE_INDEX,
    &ip_address, &network_mask);

/* If status is NX_SUCCESS the interface address was successfully
    retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_set, nx_ip_interface_attach,
- nx_ip_interface_info_get, nx_ip_interface_status_check,
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_address_set"></a>nx_ip_interface_address_set

Impostare l'indirizzo IP dell'interfaccia e network mask

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_interface_address_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG ip_address,
    ULONG network_mask);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP e network mask per l'interfaccia IP specificata.

*L'interfaccia specificata deve essere collegata in precedenza all'istanza IP.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **interface_index** Indice dell'interfaccia collegata all'istanza di NetX.
- **ip_address** Nuovo indirizzo IP dell'interfaccia di rete.
- **network_mask** Nuova interfaccia network mask.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'indirizzo IP è stato impostato correttamente.
- **NX_INVALID_INTERFACE** (0x4C) L'interfaccia di rete specificata non è valida.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Puntatori non validi.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
#define INTERFACE_INDEX 1
/* Set device IP address and network mask for the specified
    interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_set(ip_ptr, INTERFACE_INDEX,
    ip_address, network_mask);

/* If status is NX_SUCCESS the interface IP address and mask was
successfully set. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get, nx_ip_interface_attach,
- nx_ip_interface_info_get, nx_ip_interface_status_check,
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_attach"></a>nx_ip_interface_attach

Collegare l'interfaccia di rete all'istanza IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_interface_attach(
    NX_IP *ip_ptr, 
    CHAR *interface_name,
    ULONG ip_address,
    ULONG network_mask,
    VOID(*ip_link_driver)
    (struct NX_IP_DRIVER_STRUCT *));
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un'interfaccia di rete fisica all'interfaccia IP. Si noti che l'istanza IP viene creata con l'interfaccia primaria, quindi ogni interfaccia aggiuntiva è secondaria all'interfaccia primaria. Il numero totale di interfacce di rete collegate all'istanza IP (inclusa l'interfaccia **primaria)** non può superare NX_MAX_PHYSICAL_INTERFACES .

Se il thread IP non è ancora in esecuzione, le interfacce secondarie verranno inizializzate come parte del processo di avvio del thread IP che inizializza tutte le interfacce fisiche.

Se il thread IP non è ancora in esecuzione, l'interfaccia secondaria viene inizializzata come parte del ***nx_ip_interface_attach*** servizio.

*ip_ptr deve puntare a una struttura IP NetX valida.*

- ***NX_MAX_PHYSICAL_INTERFACES** deve essere configurato per il numero di interfacce di rete per l'istanza IP. Il valore predefinito è uno.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **interface_name** Puntatore alla stringa del nome dell'interfaccia.
- **ip_address** Indirizzo IP del dispositivo nell'ordine dei byte dell'host.
- **network_mask** I network mask nell'ordine dei byte dell'host.
- **ip_link_driver** Driver Ethernet per l'interfaccia.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) viene aggiunta alla tabella di routing statica.
- **NX_NO_MORE_ENTRIES** (0x17) Numero massimo di interfacce.
- **NX_MAX_PHYSICAL_INTERFACES** è stato superato.
- **NX_DUPLICATED_ENTRY** (0x52) L'indirizzo IP specificato è già usato in questa istanza IP.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Input del puntatore non valido.
- **NX_IP_ADDRESS_ERROR** (0x21) Input indirizzo IP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Attach secondary device for device IP address 192.168.1.68 with
    the specified Ethernet driver. */
status = nx_ip_interface_attach(ip_ptr, “secondary_port”,
    IP_ADDRESS(192,168,1,68),
    0xFFFFFF00UL,
    nx_etherDriver);
/* If status is NX_SUCCESS the interface was successfully added to
    the IP instance interface table. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get, nx_ip_interface_address_set,
- nx_ip_interface_info_get, nx_ip_interface_status_check,
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_info_get"></a>nx_ip_interface_info_get

Recuperare i parametri dell'interfaccia di rete


### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_interface_info_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    CHAR **interface_name,
    ULONG *ip_address,
    ULONG *network_mask,
    ULONG *mtu_size,
    ULONG *physical_address_msw,
    ULONG *physical_address_lsw);
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sui parametri di rete per l'interfaccia di rete specificata. Tutti i dati vengono recuperati nell'ordine dei byte dell'host.

*ip_ptr deve puntare a una struttura IP NetX valida. L'interfaccia specificata, se non l'interfaccia primaria, deve essere collegata in precedenza all'istanza IP.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **interface_index** Indice che specifica l'interfaccia di rete.
- **interface_name** Puntatore al buffer che contiene il nome dell'interfaccia di rete.
- **ip_address** Puntatore alla destinazione per l'indirizzo IP dell'interfaccia.
- **network_mask** Puntatore alla destinazione per network mask.
- **mtu_size** Puntatore alla destinazione per l'unità di trasferimento massima per questa interfaccia.
- **physical_address_msw** Puntatore alla destinazione per i primi 16 bit dell'indirizzo MAC del dispositivo.
- **physical_address_lsw** Puntatore alla destinazione per i 32 bit inferiori dell'indirizzo MAC del dispositivo.


### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) informazioni sull'interfaccia.
- **NX_PTR_ERROR** (0x07) Input del puntatore non valido.
- **NX_INVALID_INTERFACE** (0x4C) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Retrieve interface parameters for the specified interface (index
    1 in IP instance list of interfaces). */
#define INTERFACE_INDEX 1

status = nx_ip_interface_info_get(ip_ptr, INTERFACE_INDEX,
    &name_ptr, &ip_address,
    &network_mask,
    &mtu_size,
    &physical_address_msw,
    &physical_address_lsw);

/* If status is NX_SUCCESS the interface information is
    successfully retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get, nx_ip_interface_address_set,
- nx_ip_interface_attach, nx_ip_interface_status_check,
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_status_check"></a>nx_ip_interface_status_check

Controllare lo stato di un'istanza IP


### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_interface_status_check(
    NX_IP *ip_ptr,
    UINT interface_index
    ULONG needed_status,
    ULONG *actual_status,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio controlla e, facoltativamente, attende lo stato specificato dell'interfaccia di rete di un'istanza IP creata in precedenza.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **interface_index** Numero di indice dell'interfaccia
- **needed_status** Lo stato IP richiesto, definito nel formato mappa di bit come indicato di seguito:
    - NX_IP_INITIALIZE_DONE (0x0001)
    - NX_IP_ADDRESS_RESOLVED (0x0002)
    - NX_IP_LINK_ENABLED (0x0004)
    - NX_IP_ARP_ENABLED (0x0008)
    - NX_IP_UDP_ENABLED (0x0010)
    - NX_IP_TCP_ENABLED (0x0020)
    - NX_IP_IGMP_ENABLED (0x0040)
    - NX_IP_RARP_COMPLETE (0x0080)
    - NX_IP_INTERFACE_LINK_ENABLED (0x0100)
- **actual_status** Puntatore alla destinazione dei bit effettivi impostati.
- **wait_option** Definisce il comportamento del servizio se i bit di stato richiesti non sono disponibili. Le opzioni di attesa sono definite come segue:
    - NX_NO_WAIT (0x00000000)
    - NX_WAIT_FOREVER (0xFFFFFFFF)
    - valore di timeout in tick (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Controllo dello stato IP riuscito.
- **NX_NOT_SUCCESSFUL** richiesta di stato (0x43) non è stata soddisfatta entro il timeout specificato.
- **NX_PTR_ERROR** puntatore IP (0x07) è o è diventato non valido oppure il puntatore di stato effettivo non è valido.
- **NX_OPTION_ERROR** (0x0a) Stato necessario non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_INVALID_INTERFACE** (0x4C) Interface_index non è compreso nell'intervallo. o l'interfaccia non è valida.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Wait 10 ticks for the link up status on the previously created IP
    instance. */
status = nx_ip_interface_status_check(&ip_0, 1, NX_IP_LINK_ENABLED,
    &actual_status, 10);

/* If status is NX_SUCCESS, the secondary link for the specified IP
    instance is up. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get, nx_ip_interface_address_set,
- nx_ip_interface_attach, nx_ip_interface_info_get,
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_link_status_change_notify_set"></a>nx_ip_link_status_change_notify_set

Impostare la funzione di callback di notifica della modifica dello stato del collegamento

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_link_status_change_notify_set(
    NX_IP *ip_ptr,
    VOID (*link_status_change_notify)(NX_IP *ip_ptr, UINT interface_index, UINT link_up));
```

### <a name="description"></a>Descrizione

Questo servizio configura la funzione di callback di notifica della modifica dello stato del collegamento. La routine di  link_status_change_notify specificata dall'utente viene richiamata quando viene modificato lo stato dell'interfaccia primaria o secondaria,ad esempio quando viene modificato l'indirizzo IP. Se *link_status_change_notify* è NULL, la funzionalità di callback di notifica della modifica dello stato del collegamento è disabilitata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP
- **link_status_change_notify** Funzione di callback fornita dall'utente da chiamare in base a una modifica all'interfaccia fisica.


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Operazione riuscita
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido o nuovo puntatore di indirizzo fisico
- **NX_CALLER_ERROR** (0x11) non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.


### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Configure a callback function to be used when the physical
    interface status is changed. */
status = nx_ip_link_status_change_notify_set(&ip_0, my_change_cb);

/* If status == NX_SUCCESS, the link status change notify function
    is set. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get, nx_ip_interface_address_set,
- nx_ip_interface_attach, nx_ip_interface_info_get,
- nx_ip_interface_status_check

## <a name="nx_ip_raw_packet_disable"></a>nx_ip_raw_packet_disable

Disabilitare l'invio/ricezione di pacchetti non elaborati


### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_raw_packet_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita la trasmissione e la ricezione di pacchetti IP non elaborati per questa istanza IP. Se il servizio di pacchetti non elaborati è stato abilitato in precedenza e nella coda di ricezione sono presenti pacchetti non elaborati, questo servizio rilascerà tutti i pacchetti non elaborati ricevuti.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il pacchetto IP non elaborato è stato disabilitato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Disable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_disable(&ip_0);

/* If status is NX_SUCCESS, raw IP packet sending/receiving has
    been disabled for the previously created IP instance. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_enable, nx_ip_raw_packet_receive,
- nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send

## <a name="nx_ip_raw_packet_enable"></a>nx_ip_raw_packet_enable

Abilitare l'elaborazione di pacchetti non elaborati


### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_raw_packet_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio consente la trasmissione e la ricezione di pacchetti IP non elaborati per questa istanza IP. I pacchetti TCP, UDP, ICMP e IGMP in ingresso vengono comunque elaborati da NetX. I pacchetti con tipi di protocollo di livello superiore sconosciuti vengono elaborati dalla routine di ricezione dei pacchetti non elaborati.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il pacchetto IP non elaborato è stato abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Enable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_enable(&ip_0);

/* If status is NX_SUCCESS, raw IP packet sending/receiving has
    been enabled for the previously created IP instance. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable, nx_ip_raw_packet_receive,
- nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send

## <a name="nx_ip_raw_packet_interface_send"></a>nx_ip_raw_packet_interface_send

Invia pacchetto IP non elaborato tramite l'interfaccia di rete specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_raw_packet_interface_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    UINT address_index,
    ULONG type_of_service);
```

### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto IP non elaborato all'indirizzo IP di destinazione usando l'indirizzo IP locale specificato come indirizzo di origine e tramite l'interfaccia di rete associata. Si noti che questa routine viene restituita immediatamente e pertanto non è noto se il pacchetto IP è stato effettivamente inviato. Il driver di rete sarà responsabile del rilascio del pacchetto al termine della trasmissione. Questo servizio è diverso dagli altri servizi perché non è possibile sapere se il pacchetto è stato effettivamente inviato. Potrebbe andare perso su Internet.

*Si noti che l'elaborazione IP non elaborata deve essere abilitata.*

*Questo servizio è simile a **nx_ip_raw_packet_send**, ad eccezione del fatto che questo servizio consente a un'applicazione di inviare pacchetti IP non elaborati da interfacce fisiche specificate.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'attività IP creata in precedenza.
- **packet_ptr** Puntatore al pacchetto da trasmettere.
- **destination_ip** Indirizzo IP per l'invio del pacchetto.
- **address_index** Indice dell'indirizzo dell'interfaccia su cui inviare il pacchetto.
- **type_of_service** Tipo di servizio per il pacchetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il pacchetto è stato trasmesso correttamente.
- **NX_IP_ADDRESS_ERROR** (0x21) Nessuna interfaccia in uscita appropriata disponibile.
- **NX_NOT_ENABLED** (0x14) elaborazione di pacchetti IP non elaborati non è abilitata.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Input del puntatore non valido.
- **NX_OPTION_ERROR** (0x0A) Specificato tipo di servizio non valido.
- **NX_OVERFLOW** (0x03) Puntatore anteposto pacchetto non valido.
- **NX_UNDERFLOW** (0x02) Puntatore anteposto pacchetto non valido.
- **NX_INVALID_INTERFACE** (0x4C) Specificato indice di interfaccia non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
#define ADDRESS_IDNEX 1
/* Send packet out on interface 1 with normal type of service. */
status = nx_ip_raw_packet_interface_send(ip_ptr, packet_ptr,
    destination_ip,
    ADDRESS_INDEX,
    NX_IP_NORMAL);
/* If status is NX_SUCCESS the packet was successfully transmitted. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,
- nx_ip_raw_packet_receive, nx_ip_raw_packet_send

## <a name="nx_ip_raw_packet_receive"></a>nx_ip_raw_packet_receive

Ricevere un pacchetto IP non elaborato

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_raw_packet_receive(
    NX_IP *ip_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio riceve un pacchetto IP non elaborato dall'istanza IP specificata. Se sono presenti pacchetti IP nella coda di ricezione di pacchetti non elaborati, il primo pacchetto (meno recente) viene restituito al chiamante. In caso contrario, se non sono disponibili pacchetti, il chiamante può sospendere come specificato dall'opzione wait.

*Se NX_SUCCESS, viene restituito , l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **packet_ptr** Puntatore al puntatore in cui inserire il pacchetto IP non elaborato ricevuto.
- **wait_option** Definisce il comportamento del servizio se non sono disponibili pacchetti IP non elaborati. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ricezione di pacchetti IP non elaborati riuscita.
- **NX_NO_PACKET** (0x01) Nessun pacchetto disponibile.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_PTR_ERROR** (0x07) IP non valido o puntatore a pacchetto restituito.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Receive a raw IP packet for this IP instance, wait for a maximum
    of 4 timer ticks. */
status = nx_ip_raw_packet_receive(&ip_0, &packet_ptr, 4);

/* If status is NX_SUCCESS, the raw IP packet pointer is in the
    variable packet_ptr. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,
- nx_ip_raw_packet_send, nx_ip_raw_packet_interface_send

## <a name="nx_ip_raw_packet_send"></a>nx_ip_raw_packet_send

Inviare un pacchetto IP non elaborato

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_raw_packet_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    ULONG type_of_service);
```

### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto IP non elaborato all'indirizzo IP di destinazione. Si noti che questa routine viene restituita immediatamente e pertanto non è noto se il pacchetto IP è stato effettivamente inviato. Il driver di rete sarà responsabile del rilascio del pacchetto al termine della trasmissione.

Per un sistema multihome, NetX usa l'indirizzo IP di destinazione per trovare un'interfaccia di rete appropriata e usa l'indirizzo IP dell'interfaccia come indirizzo di origine. Se l'indirizzo IP di destinazione è broadcast o multicast, viene usata la prima interfaccia valida. In questo caso ***nx_ip_raw_packet_interface_send*** applicazioni.

*A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché il driver di rete rilascerà il pacchetto dopo la trasmissione.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **packet_ptr** Puntatore al pacchetto IP non elaborato da inviare.
- **destination_ip** Indirizzo IP di destinazione, che può essere un indirizzo IP host specifico, una trasmissione di rete, un loop-back interno o un indirizzo multicast.
- **type_of_service** Definisce il tipo di servizio per la trasmissione, i valori validi sono i seguenti:
- NX_IP_NORMAL (0x00000000)
- NX_IP_MIN_DELAY (0x00100000)
- NX_IP_MAX_DATA (0x00080000)
- NX_IP_MAX_RELIABLE (0x00040000)
- NX_IP_MIN_COST (0x00020000)


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Avvio dell'invio di pacchetti ip non elaborati riuscito.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido.
- **NX_NOT_ENABLED** (0x14) La funzionalità IP non elaborato non è abilitata.
- **NX_OPTION_ERROR** (0x0A) Tipo di servizio non valido.
- **NX_UNDERFLOW** (0x02) Spazio insufficiente per anteporre un'intestazione IP al pacchetto.
- **NX_OVERFLOW** (0x03) Puntatore di accodamento pacchetti non valido.
- **NX_PTR_ERROR** (0x07) IP o puntatore a pacchetto non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Send a raw IP packet to IP address 1.2.3.5. */
status = nx_ip_raw_packet_send(&ip_0, packet_ptr,
    IP_ADDRESS(1,2,3,5),
    NX_IP_NORMAL);

/* If status is NX_SUCCESS, the raw IP packet pointed to by
    packet_ptr has been sent. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable, nx_ip_raw_packet_enable,
- nx_ip_raw_packet_receive, nx_ip_raw_packet_send,
- nx_ip_raw_packet_interface_send

## <a name="nx_ip_static_route_add"></a>nx_ip_static_route_add

Aggiungere una route statica alla tabella di routing

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_static_route_add(
    NX_IP *ip_ptr,
    ULONG network_address,
    ULONG net_mask,
    ULONG next_hop);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una voce alla tabella di routing statico. Si noti che *next_hop'indirizzo* deve essere direttamente accessibile da uno dei dispositivi di rete locale.

*Si noti ip_ptr deve puntare a una struttura IP NetX valida e che la libreria NetX deve essere compilata con NX_ENABLE_IP_STATIC_ROUTING definito per usare questo servizio. Per impostazione predefinita, NetX viene compilato senza NX_ENABLE_IP_STATIC_ROUTING definito.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **network_address** Indirizzo di rete di destinazione, in ordine di byte host
- **net_mask** Destinazione network mask, nell'ordine dei byte dell'host
- **next_hop** Indirizzo hop successivo per la rete di destinazione, in ordine di byte host

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** voce (0x00) viene aggiunta alla tabella di routing statica.
- **NX_OVERFLOW** (0x03) La tabella di routing statica è piena.
- **NX_NOT_SUPPORTED** (0x4B) Questa funzionalità non viene compilata in .
- **NX_IP_ADDRESS_ERROR** (0x21) L'hop successivo non è direttamente accessibile tramite interfacce locali.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Puntatore ip_ptr non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Specify the next hop for the 192.168.10.0 through the gateway
    192.168.1.1. */
status = nx_ip_static_route_add(ip_ptr, IP_ADDRESS(192,168,10,0),
    0xFFFFFF00UL,
    IP_ADDRESS(192,168,1,1));

/* If status is NX_SUCCESS the route was successfully added to the
    static routing table. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_delete

## <a name="nx_ip_static_route_delete"></a>nx_ip_static_route_delete

Eliminare una route statica dalla tabella di routing

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_static_route_delete(
    NX_IP *ip_ptr,
    ULONG network_address, 
    ULONG net_mask);
```

### <a name="description"></a>Descrizione

Questo servizio elimina una voce dalla tabella di routing statico.

*Si noti ip_ptr deve puntare a una struttura IP NetX valida e che la libreria NetX deve essere compilata con NX_ENABLE_IP_STATIC_ROUTING definito per usare questo servizio. Per impostazione predefinita, NetX viene compilato senza NX_ENABLE_IP_STATIC_ROUTING definito.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **network_address** Indirizzo di rete di destinazione, in ordine di byte host.
- **net_mask** Destinazione network mask, nell'ordine dei byte dell'host.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Remove the static route for 192.168.10.0 from the routing table.*/
status = nx_ip_static_route_delete(ip_ptr,
    IP_ADDRESS(192,168,10,0), 0xFFFFFF00UL,);

/* If status is NX_SUCCESS the route was successfully removed from
    the static routing table. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_gateway_address_set, nx_ip_info_get, nx_ip_static_route_add

## <a name="nx_ip_status_check"></a>nx_ip_status_check

Controllare lo stato di un'istanza IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_status_check(
    NX_IP *ip_ptr,
    ULONG needed_status,
    ULONG *actual_status,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio controlla e, facoltativamente, attende lo stato specificato dell'interfaccia di rete primaria di un'istanza IP creata in precedenza. Per ottenere lo stato nelle interfacce secondarie, le applicazioni devono usare il servizio ***nx_ip_interface_status_check.***

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **needed_status** Lo stato IP richiesto, definito nel formato mappa di bit, è il seguente:
- NX_IP_INITIALIZE_DONE (0x0001)
- NX_IP_ADDRESS_RESOLVED (0x0002)
- NX_IP_LINK_ENABLED (0x0004)
- NX_IP_ARP_ENABLED (0x0008)
- NX_IP_UDP_ENABLED (0x0010)
- NX_IP_TCP_ENABLED (0x0020)
- NX_IP_IGMP_ENABLED (0x0040)
- NX_IP_RARP_COMPLETE (0x0080)
- NX_IP_INTERFACE_LINK_ENABLED (0x0100)
- **actual_status** Puntatore alla destinazione dei bit effettivi impostati.
- **wait_option** Definisce il comportamento del servizio se i bit di stato richiesti non sono disponibili. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Controllo stato IP riuscito.
- **NX_NOT_SUCCESSFUL** (0x43) La richiesta di stato non è stata soddisfatta entro il timeout specificato.
- **NX_PTR_ERROR** puntatore IP (0x07) è o è diventato non valido oppure il puntatore di stato effettivo non è valido.
- **NX_OPTION_ERROR** (0x0a) Stato necessario non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Wait 10 ticks for the link up status on the previously created IP
    instance. */
status = nx_ip_status_check(&ip_0, NX_IP_LINK_ENABLED,
    &actual_status, 10);

/* If status is NX_SUCCESS, the link for the specified IP instance
    is up. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_system_initialize

## <a name="nx_packet_allocate"></a>nx_packet_allocate

Allocare il pacchetto dal pool specificato

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_allocate(
    NX_PACKET_POOL *pool_ptr,
    NX_PACKET **packet_ptr,
    ULONG packet_type,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio alloca un pacchetto dal pool specificato e regola il puntatore anteposto nel pacchetto in base al tipo di pacchetto specificato. Se non è disponibile alcun pacchetto, il servizio viene sospeso in base all'opzione di attesa fornita.

### <a name="parameters"></a>Parametri

- **pool_ptr** Puntatore al pool di pacchetti creato in precedenza.
- **packet_ptr** Puntatore al puntatore del puntatore a pacchetto allocato.
- **packet_type** Definisce il tipo di pacchetto richiesto. Per un elenco dei tipi di pacchetti supportati, vedere "Pool di pacchetti" a pagina 49 nel capitolo 3.
- **wait_option** Definisce il tempo di attesa in tick se non sono disponibili pacchetti nel pool di pacchetti. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'allocazione dei pacchetti è riuscita.
- **NX_NO_PACKET** (0x01) Nessun pacchetto disponibile.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_INVALID_PARAMETERS** (0x4D) Le dimensioni del pacchetto non supportano il protocollo.
- **NX_OPTION_ERROR** (0x0A) Tipo di pacchetto non valido.
- **NX_PTR_ERROR** (0x07) Pool o puntatore restituito pacchetto non valido.
- **NX_CALLER_ERROR** (0x11) Opzione di attesa non valida da non thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR (driver di rete dell'applicazione). L'opzione wait deve essere NX_NO_WAIT se usata in ISR o nel contesto del timer.

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Allocate a new UDP packet from the previously created packet pool
    and suspend for a maximum of 5 timer ticks if the pool is
    empty. */
status = nx_packet_allocate(&pool_0, &packet_ptr, NX_UDP_PACKET, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is
    found in the variable packet_ptr. */
```

### <a name="see-also"></a>Vedere anche

- nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_copy"></a>nx_packet_copy

Copiare un pacchetto

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_copy(
    NX_PACKET *packet_ptr,
    NX_PACKET **new_packet_ptr,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio copia le informazioni nel pacchetto fornito in uno o più nuovi pacchetti allocati dal pool di pacchetti fornito. In caso di esito positivo, il puntatore al nuovo pacchetto viene restituito nella destinazione a cui punta **new_packet_ptr**.

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto di origine.
- **new_packet_ptr** Puntatore alla destinazione di dove restituire il puntatore alla nuova copia del pacchetto.
- **pool_ptr** Puntatore al pool di pacchetti creato in precedenza utilizzato per allocare uno o più pacchetti per la copia.
- **wait_option** Definisce il modo in cui il servizio attende se non sono disponibili pacchetti. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Copia del pacchetto completata.
- **NX_NO_PACKET** (0x01) Pacchetto non disponibile per la copia.
- **NX_INVALID_PACKET** (0x12) Pacchetto di origine vuoto o copia non riuscita.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_INVALID_PARAMETERS** (0x4D) Le dimensioni del pacchetto non supportano il protocollo.
- **NX_PTR_ERROR** (0x07) Pool, pacchetto o puntatore di destinazione non valido.
- **NX_UNDERFLOW** (0x02) Puntatore anteposto pacchetto non valido.
- **NX_OVERFLOW** (0x03) Puntatore di accodamento pacchetti non valido.
- **NX_CALLER_ERROR** (0x11) È stata specificata un'opzione di attesa nell'inizializzazione o in un ISR.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
NX_PACKET *new_copy_ptr;

/* Copy packet pointed to by "old_packet_ptr" using packets from
    previously created packet pool_0. */
status = nx_packet_copy(old_packet, &new_copy_ptr, &pool_0, 20);

/* If status is NX_SUCCESS, new_copy_ptr points to the packet copy. */
```

### <a name="see-also"></a>Vedere anche

- nx_packet_allocate, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_data_append"></a>nx_packet_data_append

Aggiungere dati alla fine del pacchetto

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_data_append(
    NX_PACKET *packet_ptr,
    VOID *data_start, 
    ULONG data_size,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge dati alla fine del pacchetto specificato. L'area dati fornita viene copiata nel pacchetto. Se la memoria disponibile non è sufficiente e la funzionalità dei pacchetti concatenati è abilitata, verranno allocati uno o più pacchetti per soddisfare la richiesta. Se la funzionalità del pacchetto concatenato non è abilitata, *NX_SIZE_ERROR* restituito.

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore a pacchetto.
- **data_start** Puntatore all'inizio dell'area dati dell'utente da aggiungere al pacchetto.
- **data_size** Dimensioni dell'area dati dell'utente.
- **pool_ptr** Puntatore al pool di pacchetti da cui allocare un altro pacchetto se non c'è spazio sufficiente nel pacchetto corrente.
- **wait_option** Definisce il comportamento del servizio se non sono disponibili pacchetti. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta pacchetti riuscita.
- **NX_NO_PACKET** (0x01) Nessun pacchetto disponibile.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a *tx_thread_wait_abort*.
- **NX_INVALID_PARAMETERS** (0x4D) Le dimensioni del pacchetto non supportano il protocollo.
- **NX_UNDERFLOW** (0x02) Il puntatore anteposto è minore dell'inizio del payload.
- **NX_OVERFLOW** (0x03) Il puntatore Append è maggiore dell'estremità del payload.
- **NX_PTR_ERROR** (0x07) Pool, pacchetto o puntatore dati non valido.
- **NX_SIZE_ERROR** (0x09) Dimensioni dei dati non valide.
- **NX_CALLER_ERROR** (0x11) Opzione di attesa non valida da nonthread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR (driver di rete dell'applicazione)

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Append "abcd" to the specified packet. */
status = nx_packet_data_append(packet_ptr, "abcd", 4, &pool_0, 5);

/* If status is NX_SUCCESS, the additional four bytes "abcd" have
    been appended to the packet. */
```


### <a name="see-also"></a>Vedere anche

- nx_packet_allocate, nx_packet_copy, nx_packet_data_extract_offset,
- nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,
- nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_data_extract_offset"></a>nx_packet_data_extract_offset

Estrarre dati dal pacchetto tramite un offset

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_data_extract_offset(
    NX_PACKET *packet_ptr,
    ULONG offset,
    VOID *buffer_start,
    ULONG buffer_length,
    ULONG *bytes_copied);
```

### <a name="description"></a>Descrizione

Questo servizio copia i dati da un pacchetto NetX (o catena di pacchetti) a partire dall'offset specificato dal puntatore anteposto al pacchetto della dimensione specificata in byte nel buffer specificato. Il numero di byte effettivamente copiati viene restituito in *bytes_copied.* Questo servizio non rimuove i dati dal pacchetto né regola il puntatore anteposto o altre informazioni sullo stato interno.

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto da estrarre
- **offset** Offset dal puntatore anteposto corrente.
- **buffer_start** Puntatore all'inizio del buffer di salvataggio
- **buffer_length** Numero di byte da copiare
- **bytes_copied** Numero di byte effettivamente copiati

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Copia del pacchetto riuscita
- **NX_PACKET_OFFSET_ERROR** (0x53) È stato specificato un valore di offset non valido
- **NX_PTR_ERROR** (0x07) Puntatore a pacchetto o puntatore al buffer non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Extract 10 bytes from the start of the received packet buffer
    into the specified memory area. */
status = nx_packet_data_extract_offset(my_packet, 0, &data[0], 10,
    &bytes_copied);

/* If status is NX_SUCCESS, 10 bytes were successfully copied into
    the data buffer. */
```

### <a name="see-also"></a>Vedere anche

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_retrieve, nx_packet_length_get, nx_packet_pool_create,
- nx_packet_pool_delete, nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_data_retrieve"></a>nx_packet_data_retrieve

Recuperare i dati dal pacchetto

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_data_retrieve(
    NX_PACKET *packet_ptr,
    VOID *buffer_start, 
    ULONG *bytes_copied);
```

### <a name="description"></a>Descrizione

Questo servizio copia i dati dal pacchetto fornito nel buffer fornito. Il numero effettivo di byte copiati viene restituito nella destinazione a cui punta **bytes_copied**.

Si noti che questo servizio non modifica lo stato interno del pacchetto. I dati recuperati sono ancora disponibili nel pacchetto.

*Il buffer di destinazione deve essere sufficientemente grande da contenere il contenuto del pacchetto. In caso contrario, la memoria verrà danneggiata causando risultati imprevedibili.*

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto di origine.
- **buffer_start** Puntatore all'inizio dell'area del buffer.
- **bytes_copied** Puntatore alla destinazione per il numero di byte copiati.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero dei dati dei pacchetti riuscito.
- **NX_INVALID_PACKET** (0x12) Pacchetto non valido.
- **NX_PTR_ERROR** (0x07) Puntatore non valido per pacchetto, avvio del buffer o byte copiati.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
UCHAR buffer[512];
ULONG bytes_copied;

/* Retrieve data from packet pointed to by "packet_ptr". */
status = nx_packet_data_retrieve(packet_ptr, buffer, &bytes_copied);

/* If status is NX_SUCCESS, buffer contains the contents of the
    packet, the size of which is contained in "bytes_copied." */
```

### <a name="see-also"></a>Vedere anche

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_length_get,
- nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_length_get"></a>nx_packet_length_get

Ottenere la lunghezza dei dati dei pacchetti

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_length_get(
    NX_PACKET *packet_ptr, 
    ULONG *length);
```

### <a name="description"></a>Descrizione

Questo servizio ottiene la lunghezza dei dati nel pacchetto specificato.

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto.
- **length** Destinazione per la lunghezza del pacchetto.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Get the length of the data in "my_packet." */
status = nx_packet_length_get(my_packet, &my_length);

/* If status is NX_SUCCESS, data length is in "my_length". */
```

### <a name="see-also"></a>Vedere anche

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_pool_create"></a>nx_packet_pool_create

Crea pool di pacchetti nell'area di memoria specificata

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_pool_create(
    NX_PACKET_POOL *pool_ptr,
    CHAR *name,
    ULONG payload_size,
    VOID *memory_ptr,
    ULONG memory_size);
```

### <a name="description"></a>Descrizione

Questo servizio crea un pool di pacchetti delle dimensioni del pacchetto specificate nell'area di memoria fornita dall'utente.

### <a name="parameters"></a>Parametri

- **pool_ptr** Puntatore al blocco di controllo del pool di pacchetti.
- **name** Puntatore al nome dell'applicazione per il pool di pacchetti.
- **payload_size** Numero di byte in ogni pacchetto nel pool. Questo valore deve essere di almeno 40 byte e deve anche essere divisibile in modo uniforme per 4.
- **memory_ptr** Puntatore all'area di memoria in cui inserire il pool di pacchetti. Il puntatore deve essere allineato su un limite ULONG.
- **memory_size** Dimensioni dell'area di memoria del pool.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione del pool di pacchetti riuscita.
- **NX_PTR_ERROR** (0x07) Pool o puntatore di memoria non valido.
- **NX_SIZE_ERROR** (0x09) Blocco o dimensione di memoria non valida.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Create a packet pool of 32000 bytes starting at physical
    address 0x10000000. */
status = nx_packet_pool_create(&pool_0, "Default Pool", 128,
    (void *) 0x10000000, 32000);

/* If status is NX_SUCCESS, the packet pool has been successfully
    created. */
```

### <a name="see-also"></a>Vedere anche

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_delete, nx_packet_pool_info_get,
- nx_packet_release, nx_packet_transmit_release

## <a name="nx_packet_pool_delete"></a>nx_packet_pool_delete

Eliminare il pool di pacchetti creato in precedenza

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_pool_delete(NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un pool di pacchetti creato in precedenza. NetX verifica la presenza di tutti i thread attualmente sospesi sui pacchetti nel pool di pacchetti e cancella la sospensione.

### <a name="parameters"></a>Parametri

- **pool_ptr** Puntatore a blocco di controllo del pool di pacchetti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del pool di pacchetti completata.
- **NX_PTR_ERROR** (0x07) Puntatore del pool non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
/* Delete a previously created packet pool. */
status = nx_packet_pool_delete(&pool_0);

/* If status is NX_SUCCESS, the packet pool has been successfully
    deleted. */
```

### <a name="see-also"></a>Vedere anche

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create,
- nx_packet_pool_info_get, nx_packet_release,
- nx_packet_transmit_release

## <a name="nx_packet_pool_info_get"></a>nx_packet_pool_info_get

Recuperare informazioni su un pool di pacchetti

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_pool_info_get(
    NX_PACKET_POOL *pool_ptr,
    ULONG *total_packets,
    ULONG *free_packets,
    ULONG *empty_pool_requests,
    ULONG *empty_pool_suspensions,
    ULONG *invalid_packet_releases);
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sul pool di pacchetti specificato.

*Se un puntatore di destinazione NX_NULL, queste informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **pool_ptr** Puntatore al pool di pacchetti creato in precedenza.
- **total_packets** Puntatore alla destinazione per il numero totale di pacchetti nel pool.
- **free_packets** Puntatore alla destinazione per il numero totale di pacchetti attualmente disponibili.
- **empty_pool_requests** Puntatore alla destinazione del numero totale di richieste di allocazione quando il pool era vuoto.
- **empty_pool_suspensions** Puntatore alla destinazione del numero totale di sospensioni del pool vuoto.
- **invalid_packet_releases** Puntatore alla destinazione del numero totale di versioni di pacchetti non validi.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero delle informazioni del pool di pacchetti riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread e timer

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Retrieve packet pool information. */
status = nx_packet_pool_info_get(&pool_0,
    &total_packets,
    &free_packets,
    &empty_pool_requests,
    &empty_pool_suspensions,
    &invalid_packet_releases);

/* If status is NX_SUCCESS, packet pool information was
    retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete
- nx_packet_release, nx_packet_transmit_release

## <a name="nx_packet_release"></a>nx_packet_release

Rilasciare un pacchetto allocato in precedenza

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_release(NX_PACKET *packet_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia un pacchetto, inclusi eventuali pacchetti aggiuntivi concatenati al pacchetto specificato. Se un altro thread viene bloccato per l'allocazione dei pacchetti, viene assegnato il pacchetto e ripreso.

*L'applicazione deve impedire il rilascio di un pacchetto più di una volta, perché questa operazione causerà risultati imprevedibili.*

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore a pacchetto.


### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Rilascio del pacchetto riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore a pacchetto non valido.
- **NX_UNDERFLOW** (0x02) Il puntatore anteposto è minore dell'inizio del payload.
- **NX_OVERFLOW** (0x03) Il puntatore Append è maggiore dell'estremità del payload.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR (driver di rete dell'applicazione)

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
/* Release a previously allocated packet. */
status = nx_packet_release(packet_ptr);

/* If status is NX_SUCCESS, the packet has been returned to the
    packet pool it was allocated from. */
```

### <a name="see-also"></a>Vedere anche

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_transmit_release

## <a name="nx_packet_transmit_release"></a>nx_packet_transmit_release

Rilasciare un pacchetto trasmesso

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_transmit_release(NX_PACKET *packet_ptr);
```

### <a name="description"></a>Descrizione

Per i pacchetti non TCP, questo servizio rilascia un pacchetto trasmesso, inclusi eventuali pacchetti aggiuntivi concatenati al pacchetto specificato. Se un altro thread viene bloccato all'allocazione dei pacchetti, il pacchetto viene assegnato e ripreso. Per un pacchetto TCP trasmesso, il pacchetto viene contrassegnato come trasmesso ma non rilasciato fino a quando il pacchetto non viene riconosciuto. Questo servizio viene in genere chiamato dal driver di rete dell'applicazione dopo la trasmissione di un pacchetto.

*Il driver di rete deve rimuovere l'intestazione del supporto fisico e regolare la lunghezza del pacchetto prima di chiamare questo servizio.*

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Rilascio del pacchetto di trasmissione riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore a pacchetto non valido.
- **NX_UNDERFLOW** (0x02) Il puntatore anteposto è minore dell'inizio del payload.
- **NX_OVERFLOW** (0x03) Il puntatore Append è maggiore dell'estremità del payload.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, driver di rete dell'applicazione (inclusi gli ISR)

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
/* Release a previously allocated packet that was just transmitted
    from the application network driver. */
status = nx_packet_transmit_release(packet_ptr);

/* If status is NX_SUCCESS, the transmitted packet has been
    returned to the packet pool it was allocated from. */
```

### <a name="see-also"></a>Vedere anche

- nx_packet_allocate, nx_packet_copy, nx_packet_data_append,
- nx_packet_data_extract_offset, nx_packet_data_retrieve,
- nx_packet_length_get, nx_packet_pool_create, nx_packet_pool_delete,
- nx_packet_pool_info_get, nx_packet_release

## <a name="nx_rarp_disable"></a>nx_rarp_disable

Disabilitare RARP (Reverse Address Resolution Protocol)

### <a name="prototype"></a>Prototipo

```C
UINT nx_rarp_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita il componente RARP di NetX per l'istanza IP specifica. Per un sistema multihome, questo servizio disabilita RARP in tutte le interfacce.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Riuscito RARP disabilitare.
- **NX_NOT_ENABLED** raRP (0x14) non è stato abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Disable RARP on the previously created IP instance. */
status = nx_rarp_disable(&ip_0);

/* If status is NX_SUCCESS, RARP is disabled. */
```

### <a name="see-also"></a>Vedere anche

- nx_rarp_enable, nx_rarp_info_get

## <a name="nx_rarp_enable"></a>nx_rarp_enable

Abilitare RARP (Reverse Address Resolution Protocol)

### <a name="prototype"></a>Prototipo

```C
UINT nx_rarp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio abilita il componente RARP di NetX per l'istanza IP specifica. I componenti RARP cerca in tutte le interfacce di rete collegate l'indirizzo IP zero. Un indirizzo IP zero indica che l'interfaccia non ha ancora un'assegnazione di indirizzo IP. RARP tenta di risolvere l'indirizzo IP abilitando il processo RARP su tale interfaccia.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'opzione RARP è stata abilitata.
- **NX_IP_ADDRESS_ERROR(0x21)** è già valido.
- **NX_ALREADY_ENABLED** (0x15) RARP era già abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Enable RARP on the previously created IP instance. */
status = nx_rarp_enable(&ip_0);

/* If status is NX_SUCCESS, RARP is enabled and is attempting to
    resolve this IP instance’s address by querying the network. */
```

### <a name="see-also"></a>Vedere anche

- nx_rarp_disable, nx_rarp_info_get

## <a name="nx_rarp_info_get"></a>nx_rarp_info_get

Recuperare informazioni sulle attività RARP

### <a name="prototype"></a>Prototipo

```C
UINT nx_rarp_info_get(
    NX_IP *ip_ptr,
    ULONG *rarp_requests_sent,
    ULONG *rarp_responses_received,
    ULONG *rarp_invalid_messages);
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle attività RARP per l'istanza IP specificata.

*Se un puntatore di destinazione NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **rarp_requests_sent** Puntatore alla destinazione per il numero totale di richieste RARP inviate.
- **rarp_responses_received** Puntatore alla destinazione per il numero totale di risposte RARP ricevute.
- **rarp_invalid_messages** Puntatore alla destinazione del numero totale di messaggi non validi.


### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Recupero delle informazioni RARP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Retrieve RARP information from previously created IP
    Instance 0. */
status = nx_rarp_info_get(&ip_0,
    &rarp_requests_sent,
    &rarp_responses_received,
    &rarp_invalid_messages);

/* If status is NX_SUCCESS, RARP information was retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_rarp_disable, nx_rarp_enable

## <a name="nx_system_initialize"></a>nx_system_initialize

Inizializzare il sistema NetX

### <a name="prototype"></a>Prototipo

```C
VOID nx_system_initialize(VOID);
```

### <a name="description"></a>Descrizione

Questo servizio inizializza le risorse di sistema NetX di base in preparazione all'uso. Deve essere chiamato dall'applicazione durante l'inizializzazione e prima che venga effettuata qualsiasi altra chiamata NetX.

### <a name="parameters"></a>Parametri

nessuno

### <a name="return-values"></a>Valori restituiti

Nessuno

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Initialize NetX for operation. */
nx_system_initialize();

/* At this point, NetX is ready for IP creation and all subsequent
    network operations. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_address_change_notify, nx_ip_address_get, nx_ip_address_set,
- nx_ip_create, nx_ip_delete, nx_ip_driver_direct_command,
- nx_ip_driver_interface_direct_command, nx_ip_forwarding_disable,
- nx_ip_forwarding_enable, nx_ip_fragment_disable,
- nx_ip_fragment_enable, nx_ip_info_get, nx_ip_status_check

## <a name="nx_tcp_client_socket_bind"></a>nx_tcp_client_socket_bind

Associare il socket TCP client alla porta TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_client_socket_bind(
    NX_TCP_SOCKET *socket_ptr,
    UINT port, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio associa il socket client TCP creato in precedenza alla porta TCP specificata. I socket TCP validi sono compreso tra 0 e 0xFFFF. Se la porta TCP specificata non è disponibile, il servizio viene sospeso in base all'opzione di attesa fornita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP creata in precedenza.
- **porta** Numero di porta da associare (da 1 a 0xFFFF). Se il numero di porta NX_ANY_PORT (0x0000), l'istanza IP cerca la porta gratuita successiva e la usa per l'associazione.
- **wait_option** Definisce il comportamento del servizio se la porta è già associata a un altro socket. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Associazione socket riuscita.
- **NX_ALREADY_BOUND** (0x22) Questo socket è già associato a un'altra porta TCP.
- **NX_PORT_UNAVAILABLE** (0x23) La porta è già associata a un socket diverso.
- **NX_NO_FREE_PORTS** (0x45) Nessuna porta disponibile.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a *tx_thread_wait_abort*.
- **NX_INVALID_PORT** (0x46) Porta non valida.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Bind a previously created client socket to port 12 and wait for 7
    timer ticks for the bind to complete. */
status = nx_tcp_client_socket_bind(&client_socket, 12, 7);

/* If status is NX_SUCCESS, the previously created client_socket is
    bound to port 12 on the associated IP instance. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_connect, nx_tcp_client_socket_port_get,
- nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,
- nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_client_socket_connect"></a>nx_tcp_client_socket_connect

Connessione socket TCP del client

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_client_socket_connect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG server_ip,
    UINT server_port,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio connette il socket client TCP creato in precedenza alla porta del server specificato. Le porte del server TCP valide sono da 0 a 0xFFFF. Se la connessione non viene completata immediatamente, il servizio viene sospeso in base all'opzione di attesa fornita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP creata in precedenza.
- **server_ip** Indirizzo IP del server.
- **server_port** Numero di porta del server a cui connettersi (da 1 a 0xFFFF).
- **wait_option** Definisce il comportamento del servizio mentre viene stabilita la connessione. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Connessione socket riuscita.
- **NX_NOT_BOUND** (0x24) Socket non è associato.
- **NX_NOT_CLOSED** (0x35) Il socket non è in stato chiuso.
- **NX_IN_PROGRESS** (0x37) Non è stata specificata alcuna attesa, il tentativo di connessione è in corso.
- **NX_INVALID_INTERFACE** (0x4C) Interfaccia non valida specificata.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP del server non valido.
- **NX_INVALID_PORT** (0x46) Porta non valida.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Initiate a TCP connection from a previously created and bound
    client socket. The connection requested in this example is to
    port 12 on the server with the IP address of 1.2.3.5. This
    service will wait 300 timer ticks for the connection to take
    place before giving up. */
status = nx_tcp_client_socket_connect(&client_socket,
    IP_ADDRESS(1,2,3,5), 12, 300);

/* If status is NX_SUCCESS, the previously created and bound
    client_socket is connected to port 12 on IP 1.2.3.5. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_port_get,
- nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,
- nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_client_socket_port_get"></a>nx_tcp_client_socket_port_get

Ottenere il numero di porta associato al socket TCP client

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_client_socket_port_get(
    NX_TCP_SOCKET *socket_ptr,
    UINT *port_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il numero di porta associato al socket, utile per trovare la porta allocata da NetX nelle situazioni in cui il NX_ANY_PORT è stato specificato al momento dell'associazione del socket.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP creata in precedenza.
- **port_ptr** Puntatore alla destinazione per il numero di porta restituito. I numeri di porta validi sono (da 1 a 0xFFFF).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Associazione socket riuscita.
- **NX_NOT_BOUND** (0x24) Questo socket non è associato a una porta.
- **NX_PTR_ERROR** (0x07) Puntatore socket o puntatore di porta restituito non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Get the port number of previously created and bound client
    socket. */
status = nx_tcp_client_socket_port_get(&client_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
    socket is bound to. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_unbind, nx_tcp_enable, nx_tcp_free_port_find,
- nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_client_socket_unbind"></a>nx_tcp_client_socket_unbind

Scollegare il socket client TCP dalla porta TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_client_socket_unbind(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia l'associazione tra il socket del client TCP e una porta TCP. Se sono presenti altri thread in attesa di associare un altro socket allo stesso numero di porta, il primo thread sospeso viene quindi associato a questa porta.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Operazione riuscita di annullamento dell'associazione del socket.
- **NX_NOT_BOUND** (0x24) Il socket non è stato associato ad alcuna porta.
- **NX_NOT_CLOSED** (0x35) Il socket non è stato disconnesso.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
/* Unbind a previously created and bound client TCP socket. */
status = nx_tcp_client_socket_unbind(&client_socket);

/* If status is NX_SUCCESS, the client socket is no longer
    bound. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_enable, nx_tcp_free_port_find,
- nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_enable"></a>nx_tcp_enable

Abilitare il componente TCP di NetX

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio abilita il Transmission Control Protocol (TCP) di NetX. Dopo l'abilit, le connessioni TCP possono essere stabilite dall'applicazione.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'abilitazione TCP è riuscita.
- **NX_ALREADY_ENABLED** TCP (0x15) è già abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Enable TCP on a previously created IP instance ip_0. */
status = nx_tcp_enable(&ip_0);

/* If status is NX_SUCCESS, TCP is enabled on the IP instance. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_free_port_find"></a>nx_tcp_free_port_find

Trovare la porta TCP disponibile successiva

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_free_port_find(
    NX_IP *ip_ptr,
    UINT port, UINT *free_port_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di individuare una porta TCP gratuita (non associata) a partire dalla porta fornita dall'applicazione. La logica di ricerca verrà incapsulata se la ricerca raggiunge il valore di porta massimo di 0xFFFF. Se la ricerca ha esito positivo, la porta libera viene restituita nella variabile a cui punta *free_port_ptr*.

*Questo servizio può essere chiamato da un altro thread e restituire la stessa porta. Per evitare questo race condition, l'applicazione potrebbe voler inserire questo servizio e l'effettivo binding del socket client sotto la protezione di un mutex.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **porta** Numero di porta da cui iniziare la ricerca (da 1 a 0xFFFF).
- **free_port_ptr** Puntatore al valore restituito della porta libera di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ricerca porta gratuita riuscita.
- **NX_NO_FREE_PORTS** (0x45) Nessuna porta disponibile trovata.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_INVALID_PORT** (0x46) Il numero di porta specificato non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Locate a free TCP port, starting at port 12, on a previously
    created IP instance. */
status = nx_tcp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS, "free_port" contains the next free port
    on the IP instance. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_info_get"></a>nx_tcp_info_get

Recuperare informazioni sulle attività TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_info_get(
    NX_IP *ip_ptr,
    ULONG *tcp_packets_sent,
    ULONG *tcp_bytes_sent,
    ULONG *tcp_packets_received,
    ULONG *tcp_bytes_received,
    ULONG *tcp_invalid_packets,
    ULONG *tcp_receive_packets_dropped,
    ULONG *tcp_checksum_errors,
    ULONG *tcp_connections,
    ULONG *tcp_disconnections,
    ULONG *tcp_connections_dropped,
    ULONG *tcp_retransmit_packets);
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle attività TCP per l'istanza IP specificata.

*Se un puntatore di destinazione NX_NULL, queste informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **tcp_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti TCP inviati.
- **tcp_bytes_sent** Puntatore alla destinazione per il numero totale di byte TCP inviati.
- **tcp_packets_received** Puntatore alla destinazione del numero totale di pacchetti TCP ricevuti.
- **tcp_bytes_received** Puntatore alla destinazione del numero totale di byte TCP ricevuti.
- **tcp_invalid_packets** Puntatore alla destinazione del numero totale di pacchetti TCP non validi.
- **tcp_receive_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di ricezione TCP eliminati.
- **tcp_checksum_errors** Puntatore alla destinazione del numero totale di pacchetti TCP con errori di checksum.
- **tcp_connections** Puntatore alla destinazione del numero totale di connessioni TCP.
- **tcp_disconnections** Puntatore alla destinazione del numero totale di disconnessioni TCP.
- **tcp_connections_dropped** Puntatore alla destinazione del numero totale di connessioni TCP eliminate.
- **tcp_retransmit_packets** Puntatore alla destinazione del numero totale di pacchetti TCP ritrasmessi.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero delle informazioni TCP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Retrieve TCP information from previously created IP Instance ip_0. */
status = nx_tcp_info_get(&ip_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_invalid_packets,
    &tcp_receive_packets_dropped,
    &tcp_checksum_errors,
    &tcp_connections,
    &tcp_disconnections
    &tcp_connections_dropped,
    &tcp_retransmit_packets);

/* If status is NX_SUCCESS, TCP information was retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_server_socket_accept"></a>nx_tcp_server_socket_accept

Accettare la connessione TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_server_socket_accept(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio accetta (o si prepara ad accettare) una richiesta di connessione socket client TCP per una porta precedentemente impostata per l'ascolto. Questo servizio può essere chiamato immediatamente dopo che l'applicazione chiama il servizio di ascolto o di ascolto oppure dopo che la routine di callback di ascolto viene chiamata quando la connessione client è effettivamente presente. Se non è possibile stabilire subito una connessione, il servizio viene sospeso in base all'opzione di attesa fornita.

*L'applicazione deve **nx_tcp_server_socket_unaccept** dopo che la connessione non è più necessaria per rimuovere l'associazione del socket del server alla porta del server.*

*Le routine di callback dell'applicazione vengono chiamate dall'interno del thread helper dell'indirizzo IP.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al blocco di controllo socket del server TCP.
- **wait_option** Definisce il comportamento del servizio mentre viene stabilita la connessione. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (0x00000001 a 0xFFFFFFFE)


### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Accettazione socket del server TCP (connessione passiva) riuscita.
- **NX_NOT_LISTEN_STATE** (0x36) Il socket del server fornito non è in stato di ascolto.
- **NX_IN_PROGRESS** (0x37) Non è stata specificata alcuna attesa, il tentativo di connessione è in corso.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a *tx_thread_wait_abort*.
- **NX_PTR_ERROR** (0x07) Errore del puntatore del socket.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;
void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This
    example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;
    /* Assuming that:
        "port_12_semaphore" has already been created with an
        initial count of 0 "my_ip" has already been created and the
        link is enabled "my_pool" packet pool has already been
        created */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to each client and then disconnecting.*/
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
            request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
            complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye"
                message */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is called
            even if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket
            again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }

    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_server_socket_listen"></a>nx_tcp_server_socket_listen

Abilitare l'ascolto della connessione client sulla porta TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_server_socket_listen(
    NX_IP *ip_ptr, 
    UINT port,
    NX_TCP_SOCKET *socket_ptr,
    UINT listen_queue_size,
    VOID (*listen_callback)(NX_TCP_SOCKET *socket_ptr, UINT port));
```

### <a name="description"></a>Descrizione

Questo servizio consente l'ascolto di una richiesta di connessione client sulla porta TCP specificata. Quando viene ricevuta una richiesta di connessione client, il socket del server fornito viene associato alla porta specificata e viene chiamata la funzione di callback listen fornita.

L'elaborazione della routine di callback di ascolto è interamente a livello dell'applicazione. Può contenere la logica per riattivare un thread dell'applicazione che successivamente esegue un'operazione di accettazione. Se l'applicazione dispone già di un thread sospeso all'elaborazione di accettazione per questo socket, la routine di callback di ascolto potrebbe non essere necessaria.

Se l'applicazione desidera gestire connessioni client aggiuntive sulla stessa porta, il ***nx_tcp_server_socket_relisten*** deve essere chiamato con un socket disponibile (un socket nello stato CLOSED) per la connessione successiva. Fino a quando non viene chiamato il servizio di nuovo ascolto, le connessioni client aggiuntive vengono accodati. Quando viene superata la profondità massima della coda, la richiesta di connessione meno recente viene eliminata a favore dell'accodamento della nuova richiesta di connessione. La profondità massima della coda viene specificata da questo servizio.

*Le routine di callback dell'applicazione vengono chiamate dal thread helper IP interno.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **porta** Numero di porta su cui restare in ascolto (da 1 a 0xFFFF).
- **socket_ptr** Puntatore al socket da utilizzare per la connessione.
- **listen_queue_size** Numero di richieste di connessione client che possono essere accodati.
- **listen_callback** Funzione dell'applicazione da chiamare quando viene ricevuta la connessione. Se viene specificato un valore NULL, la funzionalità di callback di ascolto è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'ascolto della porta TCP è riuscito.
- **NX_MAX_LISTEN** (0x33) Non sono disponibili altre strutture di richiesta di ascolto. La costante NX_MAX_LISTEN_REQUESTS in nx_api.h definisce il numero di richieste di ascolto attive possibili.
- **NX_NOT_CLOSED** (0x35) Il socket del server fornito non si trova in uno stato chiuso.
- **NX_ALREADY_BOUND** (0x22) Il socket del server fornito è già associato a una porta.
- **NX_DUPLICATE_LISTEN** (0x34) Esiste già una richiesta di ascolto attiva per questa porta.
- **NX_INVALID_PORT** (0x46) È stata specificata una porta non valida.
- **NX_PTR_ERROR** (0x07) IP o puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread.*/
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket.
        This example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an
        initial count of 0 "my_ip" has already been created
        and the link is enabled "my_pool" packet pool has already
        been created.
    */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server
        Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to
        each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
            request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

    /* Wait for 200 ticks for the client socket connection
        to complete. */
    status = nx_tcp_server_socket_accept(&server_socket, 200);

    /* Check for a successful connection. */
    if (status == NX_SUCCESS)
    {
        /* Allocate a packet for the "Hello_and_Goodbye"
            message. */
        nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
            NX_WAIT_FOREVER);

        /* Place "Hello_and_Goodbye" in the packet. */
        nx_packet_data_append(my_packet, "Hello_and_Goodbye",
            sizeof("Hello_and_Goodbye"),
            &my_pool,
            NX_WAIT_FOREVER);

        /* Send "Hello_and_Goodbye" to client. */
        nx_tcp_socket_send(&server_socket, my_packet, 200);

        /* Check for an error. */
        if (status)
        {
            /* Error, release the packet. */
            nx_packet_release(my_packet);
        }
        /* Now disconnect the server socket from the client. */
        nx_tcp_socket_disconnect(&server_socket, 200);
    }

    /* Unaccept the server socket. Note that unaccept is called
        even if disconnect or accept fails. */
    nx_tcp_server_socket_unaccept(&server_socket);

    /* Setup server socket for listening with this socket
    again. */
    nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
}

/* We are now done so unlisten on server port 12. */
nx_tcp_server_socket_unlisten(&my_ip, 12);

/* Delete the server socket. */
nx_tcp_socket_delete(&server_socket);
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_server_socket_relisten"></a>nx_tcp_server_socket_relisten

Re-listen for client connection on TCP port (Re-ascolto della connessione client sulla porta TCP)

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_server_socket_relisten(
    NX_IP *ip_ptr, 
    UINT port,
    NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio viene chiamato dopo che è stata ricevuta una connessione su una porta precedentemente impostata per l'ascolto. Lo scopo principale di questo servizio è fornire un nuovo socket del server per la connessione client successiva. Se una richiesta di connessione viene accodata, la connessione verrà elaborata immediatamente durante questa chiamata al servizio.

*La stessa routine di callback specificata dalla richiesta di ascolto originale viene chiamata anche quando è presente una connessione per questo nuovo socket del server.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **porta** Numero di porta su cui restare di nuovo in ascolto (da 1 a 0xFFFF).
- **socket_ptr** Socket da usare per la connessione client successiva.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Riascolta porta TCP riuscita.
- **NX_NOT_CLOSED** (0x35) Il socket del server fornito non si trova in uno stato chiuso.
- **NX_ALREADY_BOUND** (0x22) Il socket del server fornito è già associato a una porta.
- **NX_INVALID_RELISTEN** (0x47) È già presente un puntatore socket valido per questa porta oppure la porta specificata non ha una richiesta di ascolto attiva.
- **NX_CONNECTION_PENDING** (0x48) Uguale a NX_SUCCESS, ad eccezione della richiesta di connessione in coda che è stata elaborata durante questa chiamata.
- **NX_INVALID_PORT** (0x46) È stata specificata una porta non valida.
- **NX_PTR_ERROR** (0x07) IP non valido o puntatore di callback di ascolto.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread.*/
    tx_semaphore_put(&port_12_semaphore);
    }

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This
    example doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
    "port_12_semaphore" has already been created with an initial
        count of 0.
        "my_ip" has already been created and the link is enabled.
        "my_pool" packet pool has already been created. */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL,
        port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);
    /* Loop to process 5 server connections, sending
        "Hello_and_Goodbye" to each client then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection
        request is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
        complete. */
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye"
            message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is
        called even if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket
        again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_unaccept, nx_tcp_server_socket_unlisten,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_server_socket_unaccept"></a>nx_tcp_server_socket_unaccept

Rimuovere l'associazione socket alla porta di ascolto

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_server_socket_unaccept(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rimuove l'associazione tra questo socket del server e la porta del server specificata. L'applicazione deve chiamare questo servizio dopo una disconnessione o dopo una chiamata di accettazione non riuscita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket del server impostata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il socket del server ha avuto esito positivo.
- **NX_NOT_LISTEN_STATE** (0x36) Il socket del server si trova in uno stato non corretto e probabilmente non è disconnesso.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This example
    doesn't use this callback. */
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an initial count
        of 0 "my_ip" has already been created and the link is enabled
        "my_pool" packet pool has already been created
        */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket,
        "Port 12 Server Socket",NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,NX_NULL,
        port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending "Hello_and_Goodbye"
        to each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection request
            is present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to
            complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye" message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet,
                "Hello_and_Goodbye",sizeof("Hello_and_Goodbye"),
                &my_pool, NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }

            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }

        /* Unaccept the server socket. Note that unaccept is called even
            if disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind, nx_tcp_enable,
- nx_tcp_free_port_find, nx_tcp_info_get, nx_tcp_server_socket_accept,
- nx_tcp_server_socket_listen, nx_tcp_server_socket_relisten,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_server_socket_unlisten"></a>nx_tcp_server_socket_unlisten

Disabilitare l'ascolto della connessione client sulla porta TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_server_socket_unlisten(NX_IP *ip_ptr, UINT port);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita l'ascolto di una richiesta di connessione client sulla porta TCP specificata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **porta** Numero di porte per disabilitare l'ascolto (da 0 a 0xFFFF).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'ascolto TCP riuscito è disabilitato.
- **NX_ENTRY_NOT_FOUND** (0x16) L'ascolto non è stato abilitato per la porta specificata.
- **NX_INVALID_PORT** (0x46) È stata specificata una porta non valida.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
NX_PACKET_POOL my_pool;
NX_IP my_ip;
NX_TCP_SOCKET server_socket;

void port_12_connect_request(NX_TCP_SOCKET *socket_ptr, UINT port)
{
    /* Simply set the semaphore to wake up the server thread. */
    tx_semaphore_put(&port_12_semaphore);
}

void port_12_disconnect_request(NX_TCP_SOCKET *socket_ptr)
{
    /* The client has initiated a disconnect on this socket. This example
    doesn't use this callback.*/
}

void port_12_server_thread_entry(ULONG id)
{
    NX_PACKET *my_packet;
    UINT status, i;

    /* Assuming that:
        "port_12_semaphore" has already been created with an initial count
        of 0 "my_ip" has already been created and the link is enabled
        "my_pool" packet pool has already been created
    */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY,
        NX_IP_TIME_TO_LIVE, 100,
        NX_NULL, port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
        port_12_connect_request);

    /* Loop to process 5 server connections, sending "Hello_and_Goodbye" to
        each client and then disconnecting. */
    for (i = 0; i < 5; i++)
    {
        /* Get the semaphore that indicates a client connection request is
            present. */
        tx_semaphore_get(&port_12_semaphore, TX_WAIT_FOREVER);

        /* Wait for 200 ticks for the client socket connection to complete.*/
        status = nx_tcp_server_socket_accept(&server_socket, 200);

        /* Check for a successful connection. */
        if (status == NX_SUCCESS)
        {
            /* Allocate a packet for the "Hello_and_Goodbye" message. */
            nx_packet_allocate(&my_pool, &my_packet, NX_TCP_PACKET,
                NX_WAIT_FOREVER);

            /* Place "Hello_and_Goodbye" in the packet. */
            nx_packet_data_append(my_packet, "Hello_and_Goodbye",
                sizeof("Hello_and_Goodbye"), &my_pool,
                NX_WAIT_FOREVER);

            /* Send "Hello_and_Goodbye" to client. */
            nx_tcp_socket_send(&server_socket, my_packet, 200);

            /* Check for an error. */
            if (status)
            {
                /* Error, release the packet. */
                nx_packet_release(my_packet);
            }
            /* Now disconnect the server socket from the client. */
            nx_tcp_socket_disconnect(&server_socket, 200);
        }
        /* Unaccept the server socket. Note that unaccept is called even if
        disconnect or accept fails. */
        nx_tcp_server_socket_unaccept(&server_socket);

        /* Setup server socket for listening with this socket again. */
        nx_tcp_server_socket_relisten(&my_ip, 12, &server_socket);
    }
    /* We are now done so unlisten on server port 12. */
    nx_tcp_server_socket_unlisten(&my_ip, 12);

    /* Delete the server socket. */
    nx_tcp_socket_delete(&server_socket);
}
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_socket_bytes_available, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_bytes_available"></a>nx_tcp_socket_bytes_available

Recupera il numero di byte disponibili per il recupero

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_bytes_available(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *bytes_available);
```

### <a name="description"></a>Descrizione

Questo servizio ottiene il numero di byte disponibili per il recupero nel socket TCP specificato. Si noti che il socket TCP deve essere già connesso.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP creato in precedenza e connesso.
- **bytes_available** Puntatore alla destinazione per i byte disponibili.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) viene eseguito correttamente. Il numero di byte disponibili per la lettura viene restituito al chiamante.
- **NX_NOT_CONNECTED** socket (0x38) non è connesso.
- **NX_PTR_ERROR** (0x07) Puntatori non validi.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitato.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Get the bytes available for retrieval on the specified socket. */
status = nx_tcp_socket_bytes_available(&my_socket,
    &bytes_available);

/* Is status = NX_SUCCESS, the available bytes is returned in
    bytes_available. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_create,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_create"></a>nx_tcp_socket_create

Creare un socket client o server TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_create(
    NX_IP *ip_ptr, 
    NX_TCP_SOCKET *socket_ptr,
    CHAR *name, ULONG type_of_service, 
    ULONG fragment,
    UINT time_to_live, 
    ULONG window_size,
    VOID (*urgent_data_callback)(NX_TCP_SOCKET *socket_ptr),
    VOID (*disconnect_callback)(NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio crea un socket client o server TCP per l'istanza IP specificata.

*Le routine di callback dell'applicazione vengono chiamate dal thread associato a questa istanza IP.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **socket_ptr** Puntatore al nuovo blocco di controllo socket TCP.
- **name** Nome dell'applicazione per questo socket TCP.
- **type_of_service** Definisce il tipo di servizio per la trasmissione. I valori validi sono i seguenti:

- NX_IP_NORMAL (0x00000000)
- NX_IP_MIN_DELAY (0x00100000)
- NX_IP_MAX_DATA (0x00080000)
- NX_IP_MAX_RELIABLE (0x00040000)
- NX_IP_MIN_COST (0x00020000)

- **frammento**  Specifica se la frammentazione IP è consentita o meno. Se NX_FRAGMENT_OKAY (0x0), la frammentazione IP è consentita. Se NX_DONT_FRAGMENT (0x4000), la frammentazione IP è disabilitata.
- **time_to_live** Specifica il valore a 8 bit che definisce il numero di router che questo pacchetto può passare prima di essere buttato via. Il valore predefinito viene specificato da NX_IP_TIME_TO_LIVE.
- **window_size** Definisce il numero massimo di byte consentiti nella coda di ricezione per questo socket
- **urgent_data_callback** Funzione dell'applicazione che viene chiamata ogni volta che vengono rilevati dati urgenti nel flusso di ricezione. Se questo valore è NX_NULL, i dati urgenti vengono ignorati.
- **disconnect_callback** Funzione dell'applicazione che viene chiamata ogni volta che viene stabilita una disconnessione dal socket all'altra estremità della connessione. Se questo valore è NX_NULL, la funzione di callback di disconnessione è disabilitata.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Creazione del socket client TCP riuscita.
- **NX_OPTION_ERROR** (0x0A) Tipo di servizio, frammento, dimensione della finestra non valida o opzione time-to-live non valida.
- **NX_PTR_ERROR** (0x07) Puntatore IP o socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Create a TCP client socket on the previously created IP instance,
    with normal delivery, IP fragmentation enabled, 0x80 time to
    live, a 200-byte receive window, no urgent callback routine, and
    the "client_disconnect" routine to handle disconnection initiated
    from the other end of the connection. */
status = nx_tcp_socket_create(&ip_0, &client_socket,
    "Client Socket",
    NX_IP_NORMAL, NX_FRAGMENT_OKAY,
    0x80, 200, NX_NULL
    client_disconnect);

/* If status is NX_SUCCESS, the client socket is created and ready
    to be bound. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_delete"></a>nx_tcp_socket_delete

Eliminare un socket TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_delete(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un socket TCP creato in precedenza. Se il socket è ancora associato o connesso, il servizio restituisce un codice di errore.

### <a name="parameters"></a>Parametri

- **socket_ptr** Socket TCP creato in precedenza

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del socket riuscita.
- **NX_NOT_CREATED** (0x27) Socket non è stato creato.
- **NX_STILL_BOUND** (0x42) Il socket è ancora associato.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Delete a previously created TCP client socket. */
status = nx_tcp_socket_delete(&client_socket);

/* If status is NX_SUCCESS, the client socket is deleted. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send,
- nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_disconnect"></a>nx_tcp_socket_disconnect

Disconnettere le connessioni socket client e server

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_disconnect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio disconnette una connessione socket client o server stabilita. Una disconnessione di un socket del server deve essere seguita da una richiesta non crittografata, mentre un socket client disconnesso viene lasciato in uno stato pronto per un'altra richiesta di connessione. Se il processo di disconnessione non può terminare immediatamente, il servizio viene sospeso in base all'opzione di attesa fornita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket client o server connessa in precedenza.
- **wait_option** Definisce il comportamento del servizio mentre è in corso la disconnessione. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Disconnessione socket riuscita.
- **NX_NOT_CONNECTED** (0x38) Il socket specificato non è connesso.
- **NX_IN_PROGRESS** (0x37) Disconnessione in corso, non è stata specificata alcuna attesa.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```C
/* Disconnect from a previously established connection and wait a
    maximum of 400 timer ticks. */
status = nx_tcp_socket_disconnect(&client_socket, 400);

/* If status is NX_SUCCESS, the previously connected socket (either
    as a result of the client socket connect or the server accept) is
    disconnected. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_info_get,
- nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,
- nx_tcp_socket_send, nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_disconnect_complete_notify"></a>nx_tcp_socket_disconnect_complete_notify

Installare la funzione di callback di notifica completa disconnessione TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_disconnect_complete_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_disconnect_complete_notify)
    (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback che viene richiamata dopo il completamento di un'operazione di disconnessione del socket. La funzione di callback di disconnessione completa del socket TCP è disponibile se NetX viene compilato con l'opzione

- ***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** definito.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket client o server connessa in precedenza.
- **tcp_disconnect_complete_notify** Funzione di callback da installare.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) La funzione di callback è stata registrata correttamente.
- **NX_NOT_SUPPORTED** (0x4B) La funzionalità di notifica estesa non è incorporata nella libreria NetX
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) la funzionalità TCP non è abilitata.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Install the disconnect complete notify callback function. */
status = nx_tcp_socket_disconnect_complete_notify(&client_socket,
    callback);
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable, nx_tcp_socket_create, nx_tcp_socket_establish_notify,
- nx_tcp_socket_mss_get, nx_tcp_socket_mss_peer_get,
- nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,
- nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_establish_notify"></a>nx_tcp_socket_establish_notify

Impostare la funzione di callback di notifica tcp establish

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_establish_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_establish_notify)(NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback, che viene chiamata dopo che un socket TCP effettua una connessione. La funzione di callback tcp socket establish è disponibile se NetX viene compilato con ***l'opzione NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** definita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket client o server connessa in precedenza.
- **tcp_establish_notify** Funzione di callback richiamata dopo che è stata stabilita una connessione TCP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Imposta correttamente la funzione notify.
- **NX_NOT_SUPPORTED** (0x4B) La funzionalità di notifica estesa non è incorporata nella libreria NetX
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) TCP non è stato abilitato dall'applicazione.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Set the function pointer "callback" as the notify function NetX
will call when the connection is in the established state. */
status = nx_tcp_socket_establish_notify(&client_socket, callback);
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,
- nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_info_get"></a>nx_tcp_socket_info_get

Recuperare informazioni sulle attività socket TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *tcp_packets_sent,
    ULONG *tcp_bytes_sent,
    ULONG *tcp_packets_received,
    ULONG *tcp_bytes_received,
    ULONG *tcp_retransmit_packets,
    ULONG *tcp_packets_queued,
    ULONG *tcp_checksum_errors,
    ULONG *tcp_socket_state,
    ULONG *tcp_transmit_queue_depth,
    ULONG *tcp_transmit_window,
    ULONG *tcp_receive_window);
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle attività socket TCP per l'istanza del socket TCP specificata.

*Se un puntatore di destinazione NX_NULL, queste informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP creata in precedenza.
- **tcp_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti TCP inviati sul socket.
- **tcp_bytes_sent** Puntatore alla destinazione per il numero totale di byte TCP inviati sul socket.
- **tcp_packets_received** Puntatore alla destinazione del numero totale di pacchetti TCP ricevuti nel socket.
- **tcp_bytes_received** Puntatore alla destinazione del numero totale di byte TCP ricevuti nel socket.
- **tcp_retransmit_packets** Puntatore alla destinazione del numero totale di ritrasmissioni di pacchetti TCP.
- **tcp_packets_queued** Puntatore alla destinazione del numero totale di pacchetti TCP in coda nel socket.
- **tcp_checksum_errors** Puntatore alla destinazione del numero totale di pacchetti TCP con errori di checksum nel socket.
- **tcp_socket_state** Puntatore alla destinazione dello stato corrente del socket.
- **tcp_transmit_queue_depth** Puntatore alla destinazione del numero totale di pacchetti di trasmissione ancora in coda in attesa di ACK.
- **tcp_transmit_window** Puntatore alla destinazione delle dimensioni correnti della finestra di trasmissione.
- **tcp_receive_window** Puntatore alla destinazione delle dimensioni correnti della finestra di ricezione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero delle informazioni sul socket TCP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="return-values"></a>Valori restituiti

```C
/* Retrieve TCP socket information from previously created socket_0.*/
status = nx_tcp_socket_info_get(&socket_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_retransmit_packets,
    &tcp_packets_queued,
    &tcp_checksum_errors,
    &tcp_socket_state,
    &tcp_transmit_queue_depth,
    &tcp_transmit_window,
    &tcp_receive_window);

/* If status is NX_SUCCESS, TCP socket information was retrieved. */
```

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Retrieve TCP socket information from previously created socket_0.*/
status = nx_tcp_socket_info_get(&socket_0,
    &tcp_packets_sent,
    &tcp_bytes_sent,
    &tcp_packets_received,
    &tcp_bytes_received,
    &tcp_retransmit_packets,
    &tcp_packets_queued,
    &tcp_checksum_errors,
    &tcp_socket_state,
    &tcp_transmit_queue_depth,
    &tcp_transmit_window,
    &tcp_receive_window);

/* If status is NX_SUCCESS, TCP socket information was retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_receive, nx_tcp_socket_receive_queue_max_set,
- nx_tcp_socket_send, nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_mss_get"></a>nx_tcp_socket_mss_get

Ottenere MSS del socket

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_mss_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
```

### <a name="description"></a>Descrizione

Questo servizio recupera le dimensioni massime del segmento (MSS) locali del socket specificato.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket creato in precedenza.
- **mss** Destinazione per la restituzione di MSS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** mss (0x00) riuscito.
- **NX_PTR_ERROR** (0x07) Socket o puntatore di destinazione MSS non valido.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitato.
- **NX_CALLER_ERROR** chiamante (0x11) non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Get the MSS for the socket "my_socket". */
status = nx_tcp_socket_mss_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
    socket's current MSS value. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_peer_get,
- nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,
- nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_mss_peer_get"></a>nx_tcp_socket_mss_peer_get

Ottenere MSS del socket TCP peer

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_mss_peer_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
```

### <a name="description"></a>Descrizione

Questo servizio recupera la dimensione massima del segmento (MSS) annunciata dal socket peer.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket creato in precedenza e connesso.
- **mss** Destinazione per la restituzione di MSS.


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) MsS peer riuscito.
- **NX_PTR_ERROR** (0x07) Socket o puntatore di destinazione MSS non valido.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitato.
- **NX_CALLER_ERROR** chiamante (0x11) non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Get the MSS of the connected peer to the socket "my_socket". */
status = nx_tcp_socket_mss_peer_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
    socket peer’s advertised MSS value. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_set, nx_tcp_socket_peer_info_get,
- nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_mss_set"></a>nx_tcp_socket_mss_set

Impostare MSS del socket

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_mss_set(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG mss);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la dimensione massima del segmento (MSS) del socket specificato. Si noti che il valore MSS deve essere all'interno dell'interfaccia di rete MTU IP, consentendo spazio per le intestazioni IP e TCP.

Questo servizio deve essere usato prima che un socket TCP inizi il processo di connessione. Se il servizio viene utilizzato dopo che è stata stabilita una connessione TCP, il nuovo valore non ha alcun effetto sulla connessione.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket creato in precedenza.
- **mss** Valore di MSS da impostare.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) mss impostato correttamente.
- **NX_SIZE_ERROR** valore MSS 0x09 specificato è troppo grande.
- **NX_NOT_CONNECTED** stata stabilita 0x38 connessione TCP (0x38)
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitato.
- **NX_CALLER_ERROR** chiamante (0x11) non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Set the MSS of the socket "my_socket" to 1000 bytes. */
status = nx_tcp_socket_mss_set(&my_socket, 1000);

/* If status is NX_SUCCESS, the MSS of "my_socket" is 1000 bytes. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_peer_info_get,
- nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_peer_info_get"></a>nx_tcp_socket_peer_info_get

Recuperare informazioni sul socket TCP peer

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_peer_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *peer_ip_address, 
    ULONG *peer_port);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IP peer e le informazioni sulla porta per il socket TCP connesso sulla rete IP.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP creato in precedenza.
- **peer_ip_address** Puntatore alla destinazione per l'indirizzo IP peer, nell'ordine dei byte dell'host.
- **peer_port** Puntatore alla destinazione per il numero di porta peer, nell'ordine dei byte dell'host.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) viene eseguito correttamente. L'indirizzo IP peer e il numero di porta vengono restituiti al chiamante.
- **NX_NOT_CONNECTED** socket (0x38) non è connesso.
- **NX_PTR_ERROR** (0x07) Puntatori non validi.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitato.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Obtain peer IP address and port on the specified TCP socket. */
status = nx_tcp_socket_peer_info_get(&my_socket, &peer_ip_address,
    &peer_port);

/* If status = NX_SUCCESS, the data was successfully obtained. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_receive_notify, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_receive"></a>nx_tcp_socket_receive

Ricevere dati dal socket TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_receive(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio riceve i dati TCP dal socket specificato. Se nessun dato viene accodato nel socket specificato, il chiamante viene sospeso in base all'opzione di attesa fornita.

*Se NX_SUCCESS restituito, l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP creata in precedenza.
- **packet_ptr** Puntatore al puntatore a pacchetto TCP.
- **wait_option** Definisce il comportamento del servizio se nessun dato è attualmente accodato in questo socket. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Ricezione dei dati socket riuscita.
- **NX_NOT_BOUND** (0x24) Socket non è ancora associato.
- **NX_NO_PACKET** (0x01) Nessun dato ricevuto.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_NOT_CONNECTED** (0x38) Il socket non è più connesso.
- **NX_PTR_ERROR** (0x07) Socket non valido o puntatore a pacchetto restituito.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

/* Riceve un pacchetto dal socket client TCP creato in precedenza e connesso. Se non è disponibile alcun pacchetto, attendere 200 tick timer prima di rinunciare. */ status = nx_tcp_socket_receive(&client_socket, &packet_ptr, 200);

/* Se lo stato è NX_SUCCESS, il pacchetto ricevuto è puntato da "packet_ptr". */

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive_queue_max_set,
- nx_tcp_socket_send, nx_tcp_socket_state_wait

## <a name="nx_tcp_socket_receive_notify"></a>nx_tcp_socket_receive_notify

Notificare all'applicazione i pacchetti ricevuti


### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_receive_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_receive_notify) (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio configura il puntatore a funzione receive notify con la funzione di callback specificata dall'applicazione. Questa funzione di callback viene quindi chiamata ogni volta che uno o più pacchetti vengono ricevuti nel socket. Se viene NX_NULL un puntatore di notifica, la funzione notify è disabilitata.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP.
- **tcp_receive_notify** Puntatore a funzione di callback dell'applicazione chiamato quando uno o più pacchetti vengono ricevuti nel socket.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Notifica di ricezione socket riuscita.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) la funzionalità TCP non è abilitata.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Setup a receive packet callback function for the "client_socket"
socket. */
status = nx_tcp_socket_receive_notify(&client_socket,
    my_receive_notify);

/* If status is NX_SUCCESS, NetX will call the function named
    "my_receive_notify" whenever one or more packets are received for
    "client_socket". */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_peer_info_get, nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_send"></a>nx_tcp_socket_send

Inviare dati tramite un socket TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_send(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia i dati TCP tramite un socket TCP connesso in precedenza. Se le dimensioni dell'ultima finestra annunciata del ricevitore sono inferiori a questa richiesta, il servizio viene sospeso facoltativamente in base all'opzione di attesa specificata. Questo servizio garantisce che al livello IP non siano inviati dati di pacchetti di dimensioni superiori a MSS.

*A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché anche il driver di rete tenterà di rilasciare il pacchetto dopo la trasmissione.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP precedentemente connessa.
- **packet_ptr** Puntatore a pacchetti di dati TCP.
- **wait_option** Definisce il comportamento del servizio se la richiesta è maggiore delle dimensioni della finestra del ricevitore. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio socket riuscito.
- **NX_NOT_BOUND** (0x24) Il socket non è stato associato ad alcuna porta.
- **NX_NO_INTERFACE_ADDRESS** (0x50) Nessuna interfaccia in uscita appropriata trovata.
- **NX_NOT_CONNECTED** (0x38) Il socket non è più connesso.
- **NX_WINDOW_OVERFLOW** (0x39) La richiesta è maggiore della dimensione della finestra annunciata del ricevitore in byte.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_INVALID_PACKET** (0x12) Il pacchetto non viene allocato.
- **NX_TX_QUEUE_DEPTH** (0x49) È stata raggiunta la profondità massima della coda di trasmissione.
- **NX_OVERFLOW** (0x03) Puntatore di accodamento pacchetti non valido.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_UNDERFLOW** (0x02) Il puntatore anteposto al pacchetto non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Send a packet out on the previously created and connected TCP
    socket. If the receive window on the other side of the connection
    is less than the packet size, wait 200 timer ticks before giving up. */
status = nx_tcp_socket_send(&client_socket, packet_ptr, 200);

/* If status is NX_SUCCESS, the packet has been sent! */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_state_wait

### <a name="nx_tcp_socket_state_wait"></a>nx_tcp_socket_state_wait

Attendere che il socket TCP entri in uno stato specifico

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_state_wait(
    NX_TCP_SOCKET *socket_ptr,
    UINT desired_state, 
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio attende che il socket entri nello stato desiderato. Se il socket non è nello stato desiderato, il servizio viene sospeso in base all'opzione di attesa fornita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP precedentemente connessa.
- **desired_state** Stato TCP desiderato. Gli stati del socket TCP validi sono definiti come segue:
- NX_TCP_CLOSED (0x01)
- NX_TCP_LISTEN_STATE (0x02)
- NX_TCP_SYN_SENT (0x03)
- NX_TCP_SYN_RECEIVED (0x04)
- NX_TCP_ESTABLISHED (0x05)
- NX_TCP_CLOSE_WAIT (0x06)
- NX_TCP_FIN_WAIT_1 (0x07)
- NX_TCP_FIN_WAIT_2 (0x08)
- NX_TCP_CLOSING (0x09)
- NX_TCP_TIMED_WAIT (0x0A)
- NX_TCP_LAST_ACK (0x0B)
- **wait_option** Definisce il comportamento del servizio se lo stato richiesto non è presente. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Attesa di stato riuscita.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_NOT_SUCCESSFUL** (0x43) Stato non presente entro il tempo di attesa specificato.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_OPTION_ERROR** (0x0A) Lo stato del socket desiderato non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Wait 300 timer ticks for the previously created socket to enter
    the established state in the TCP state machine. */
status = nx_tcp_socket_state_wait(&client_socket,
    NX_TCP_ESTABLISHED, 300);

/* If status is NX_SUCCESS, the socket is now in the established
    state! */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind, nx_tcp_client_socket_connect,
- nx_tcp_client_socket_port_get, nx_tcp_client_socket_unbind,
- nx_tcp_enable, nx_tcp_free_port_find, nx_tcp_info_get,
- nx_tcp_server_socket_accept, nx_tcp_server_socket_listen,
- nx_tcp_server_socket_relisten, nx_tcp_server_socket_unaccept,
- nx_tcp_server_socket_unlisten, nx_tcp_socket_bytes_available,
- nx_tcp_socket_create, nx_tcp_socket_delete, nx_tcp_socket_disconnect,
- nx_tcp_socket_info_get, nx_tcp_socket_receive,
- nx_tcp_socket_receive_queue_max_set, nx_tcp_socket_send

## <a name="nx_tcp_socket_timed_wait_callback"></a>nx_tcp_socket_timed_wait_callback

Callback di installazione per lo stato di attesa a tempo

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_timed_wait_callback(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_timed_wait_callback) (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback che viene richiamata quando il socket TCP è in stato di attesa a tempo. Per usare questo servizio, la libreria NetX deve essere compilata con ***l'opzione NX_ENABLE_EXTENDED_NOTIFY*** definita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket client o server connessa in precedenza.
- **tcp_timed_wait_callback** Funzione di callback di attesa a tempo

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Registra correttamente il socket della funzione di callback
- **NX_NOT_SUPPORTED** libreria NetX (0x4B) viene compilata senza la funzionalità di notifica estesa abilitata.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) la funzionalità TCP non è abilitata.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Install the timed wait callback function */
nx_tcp_socket_timed_wait_callback(&client_socket, callback);
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,
- nx_tcp_socket_transmit_configure,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_transmit_configure"></a>nx_tcp_socket_transmit_configure

Configurare i parametri di trasmissione del socket

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_transmit_configure(
    NX_TCP_SOCKET *socket_ptr,
    ULONG max_queue_depth,
    ULONG timeout,
    ULONG max_retries,
    ULONG timeout_shift);
```

### <a name="description"></a>Descrizione

Questo servizio configura vari parametri di trasmissione del socket TCP specificato.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP.
- **max_queue_depth** Numero massimo di pacchetti che possono essere accodati per la trasmissione.
- **timeout** Numero di tick del timer ThreadX che un ACK attende prima che il pacchetto venga inviato di nuovo.
- **max_retries** Numero massimo di tentativi consentiti.
- **timeout_shift** Valore per spostare il timeout per ogni tentativo successivo. Il valore 0 comporta lo stesso timeout tra tentativi successivi. Il valore 1 raddoppia il timeout tra i tentativi.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) Configurazione del socket di trasmissione riuscita.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_OPTION_ERROR** (0x0a) Opzione Profondità coda non valida.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitata.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Configure the "client_socket" for a maximum transmit queue depth
    of 12, 100 tick timeouts, a maximum of 20 retries, and a timeout
    double on each successive retry. */
status = nx_tcp_socket_transmit_configure(&client_socket,
    12,100,20, 1);

/* If status is NX_SUCCESS, the socket’s transmit retry has been
    configured. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,
- nx_tcp_socket_timed_wait_callback,
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_window_update_notify_set"></a>nx_tcp_socket_window_update_notify_set

Notificare all'applicazione gli aggiornamenti delle dimensioni della finestra

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_window_update_notify_set(
    NX_TCP_SOCKET
    *socket_ptr,
    VOID (*tcp_window_update_notify)
    (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio installa una routine di callback di aggiornamento della finestra socket. Questa routine viene chiamata automaticamente ogni volta che il socket specificato riceve un pacchetto che indica un aumento delle dimensioni della finestra dell'host remoto.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP creato in precedenza.
- **tcp_window_update_notify** Routine di callback da chiamare quando le dimensioni della finestra cambiano. Il valore NULL disabilita l'aggiornamento delle modifiche della finestra.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) callback viene installata nel socket.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Puntatori non validi.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitata.


### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Set the function pointer to the windows update callback after creating the
socket. */
status = nx_tcp_socket_window_update_notify_set(&data_socket,
    my_windows_update_callback);

/* Define the window callback function in the host application. */
void my_windows_update_callback(NX_TCP_SCOCKET *data_socket)
{
    /* Process update on increase TCP transmit socket window size. */
    return;
}
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable, nx_tcp_socket_create,
- nx_tcp_socket_disconnect_complete_notify,
- nx_tcp_socket_establish_notify, nx_tcp_socket_mss_get,
- nx_tcp_socket_mss_peer_get, nx_tcp_socket_mss_set,
- nx_tcp_socket_peer_info_get, nx_tcp_socket_receive_notify,
- nx_tcp_socket_timed_wait_callback, nx_tcp_socket_transmit_configure

## <a name="nx_udp_enable"></a>nx_udp_enable

Abilitare il componente UDP di NetX

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio abilita il componente User Datagram Protocol (UDP) di NetX. Dopo l'a attivazione, i datagrammi UDP possono essere inviati e ricevuti dall'applicazione.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Udp riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_ALREADY_ENABLED** (0x15) Questo componente è già stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Enable UDP on the previously created IP instance. */
status = nx_udp_enable(&ip_0);

/* If status is NX_SUCCESS, UDP is now enabled on the specified IP
    instance. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_free_port_find, nx_udp_info_get, nx_udp_packet_info_extract,
- nx_udp_socket_bind, nx_udp_socket_bytes_available,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_free_port_find"></a>nx_udp_free_port_find

Trovare la porta UDP successiva disponibile

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_free_port_find(
    NX_IP *ip_ptr, 
    UINT port,
    UINT *free_port_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio cerca una porta UDP gratuita (non in ingresso) a partire dal numero di porta fornito dall'applicazione. La logica di ricerca verrà restituita se la ricerca raggiunge il valore massimo della porta 0xFFFF. Se la ricerca ha esito positivo, la porta libera viene restituita nella variabile a cui punta *free_port_ptr*.

*Questo servizio può essere chiamato da un altro thread e può avere la stessa porta restituita. Per evitare questo race condition, l'applicazione potrebbe voler posizionare questo servizio e l'associazione socket effettiva sotto la protezione di un mutex.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **porta** Numero di porta per avviare la ricerca (da 1 a 0xFFFF).
- **free_port_ptr** Puntatore alla variabile restituita della porta libera di destinazione.


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ricerca porta libera riuscita.
- **NX_NO_FREE_PORTS** (0x45) Nessuna porta disponibile trovata.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_INVALID_PORT** (0x46) Il numero di porta specificato non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Locate a free UDP port, starting at port 12, on a previously
    created IP instance. */
status = nx_udp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS pointer, "free_port" identifies the next
    free UDP port on the IP instance. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_info_get, nx_udp_packet_info_extract,
- nx_udp_socket_bind, nx_udp_socket_bytes_available,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_info_get"></a>nx_udp_info_get

Recuperare informazioni sulle attività UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_info_get(
    NX_IP *ip_ptr,
    ULONG *udp_packets_sent,
    ULONG *udp_bytes_sent,
    ULONG *udp_packets_received,
    ULONG *udp_bytes_received,
    ULONG *udp_invalid_packets,
    ULONG *udp_receive_packets_dropped,
    ULONG *udp_checksum_errors);
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle attività UDP per l'istanza IP specificata.

*Se un puntatore di destinazione NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **udp_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti UDP inviati.
- **udp_bytes_sent** Puntatore alla destinazione per il numero totale di byte UDP inviati.
- **udp_packets_received** Puntatore alla destinazione del numero totale di pacchetti UDP ricevuti.
- **udp_bytes_received** Puntatore alla destinazione del numero totale di byte UDP ricevuti.
- **udp_invalid_packets** Puntatore alla destinazione del numero totale di pacchetti UDP non validi.
- **udp_receive_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di ricezione UDP eliminati.
- **udp_checksum_errors** Puntatore alla destinazione del numero totale di pacchetti UDP con errori di checksum.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero delle informazioni UDP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.


### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread e timer

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Retrieve UDP information from previously created IP Instance ip_0. */
status = nx_udp_info_get(&ip_0, &udp_packets_sent,
    &udp_bytes_sent,
    &udp_packets_received,
    &udp_bytes_received,
    &udp_invalid_packets,
    &udp_receive_packets_dropped,
    &udp_checksum_errors);

/* If status is NX_SUCCESS, UDP information was retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_packet_info_extract,
- nx_udp_socket_bind, nx_udp_socket_bytes_available,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_packet_info_extract"></a>nx_udp_packet_info_extract

Estrarre i parametri di rete dal pacchetto UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_packet_info_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address,
    UINT *protocol,
    UINT *port,
    UINT *interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio estrae i parametri di rete, ad esempio indirizzo IP, numero di porta peer, tipo di protocollo (questo servizio restituisce sempre il tipo UDP) da un pacchetto ricevuto su un'interfaccia in ingresso.

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto.
- **ip_address** Puntatore all'indirizzo IP del mittente.
- **protocollo** Puntatore al protocollo (UDP).
- **porta** Puntatore al numero di porta del mittente.
- **interface_index** Puntatore alla ricezione dell'indice dell'interfaccia.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Packet interface data successfully extracted ( Dati dell'interfaccia di pacchetto estratti correttamente).
- **NX_INVALID_PACKET** (0x12) Il pacchetto non contiene frame IP.
- **NX_PTR_ERROR** (0x07) Input puntatore non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Extract network data from UDP packet interface.*/
status = nx_udp_packet_info_extract( packet_ptr, &ip_address,
    &protocol, &port,
    &interface_index);

/* If status is NX_SUCCESS packet data was successfully retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_socket_bind, nx_udp_socket_bytes_available,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_bind"></a>nx_udp_socket_bind

Associare un socket UDP alla porta UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_bind(
    NX_UDP_SOCKET *socket_ptr, 
    UINT port,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio associa il socket UDP creato in precedenza alla porta UDP specificata. I socket UDP validi sono compreso tra 0 e 0xFFFF. Se il numero di porta richiesto è associato a un altro socket, il servizio attende il periodo di tempo specificato per la disassociazione del socket dal numero di porta.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.
- **porta** Numero di porta a cui eseguire il binding (da 1 a 0xFFFF). Se il numero di porta NX_ANY_PORT (0x0000), l'istanza IP cerca la porta libera successiva e la usa per l'associazione.
- **wait_option** Definisce il comportamento del servizio se la porta è già associata a un altro socket. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Associazione socket riuscita.
- **NX_ALREADY_BOUND** (0x22) Questo socket è già associato a un'altra porta.
- **NX_PORT_UNAVAILABLE** porta (0x23) è già associata a un socket diverso.
- **NX_NO_FREE_PORTS** (0x45) Nessuna porta disponibile.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_INVALID_PORT** (0x46) È stata specificata una porta non valida.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Bind the previously created UDP socket to port 12 on the
    previously created IP instance. If the port is already bound,
    wait for 300 timer ticks before giving up. */
status = nx_udp_socket_bind(&udp_socket, 12, 300);

/* If status is NX_SUCCESS, the UDP socket is now bound to
    port 12.*/
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bytes_available,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_bytes_available"></a>nx_udp_socket_bytes_available

Recupera il numero di byte disponibili per il recupero

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_bytes_available(
    NX_UDP_SOCKET *socket_ptr,
    ULONG *bytes_available);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il numero di byte disponibili per la ricezione nel socket UDP specificato.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket UDP creato in precedenza.
- **bytes_available** Puntatore alla destinazione per i byte disponibili.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero disponibile byte riusciti.
- **NX_NOT_SUCCESSFUL** (0x43) Socket non associato a una porta.
- **NX_PTR_ERROR** (0x07) Puntatori non validi.
- **NX_NOT_ENABLED** (0x14) UDP non è abilitata.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Get the bytes available for retrieval from the UDP socket. */
status = nx_udp_socket_bytes_available(&my_socket, &bytes_available);

/* If status == NX_SUCCESS, the number of bytes was successfully
    retrieved.*/
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_checksum_disable, nx_udp_socket_checksum_enable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_checksum_disable"></a>nx_udp_socket_checksum_disable

Disabilitare il checksum per il socket UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_checksum_disable(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita la logica di checksum per l'invio e la ricezione di pacchetti sul socket UDP specificato. Quando la logica di checksum è disabilitata, il valore zero viene caricato nel campo checksum dell'intestazione UDP per tutti i pacchetti inviati tramite questo socket. Un valore di checksum di valore zero nell'intestazione UDP segnala al ricevitore che il checksum non viene calcolato per questo pacchetto.

Si noti anche che questa operazione non ha alcun effetto se ***NX_DISABLE_UDP_RX_CHECKSUM** _ e _ *_NX_DISABLE_UDP_TX_CHECKSUM_** vengono definiti rispettivamente durante la ricezione e l'invio di pacchetti UDP.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Checksum socket riuscito disabilitato.
- **NX_NOT_BOUND** (0x24) Socket non è associato.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Disable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_disable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will not have a checksum
    calculated. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_checksum_enable"></a>nx_udp_socket_checksum_enable

Abilitare il checksum per il socket UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_checksum_enable(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio abilita la logica di checksum per l'invio e la ricezione di pacchetti sul socket UDP specificato. Il checksum copre l'intera area dati UDP e una pseudo-intestazione IP.

Si noti inoltre che questa operazione non ha alcun effetto **se NX_DISABLE_UDP_RX_CHECKSUM** e **NX_DISABLE_UDP_TX_CHECKSUM** vengono definiti rispettivamente durante la ricezione e l'invio di pacchetti UDP.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Checksum socket riuscito.
- **NX_NOT_BOUND** (0x24) Socket non è associato.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Enable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_enable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will have a checksum
    calculated. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_create, nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_create"></a>nx_udp_socket_create

Creare un socket UDP.

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_create(
    NX_IP *ip_ptr,
    NX_UDP_SOCKET *socket_ptr, CHAR *name,
    ULONG type_of_service, ULONG fragment,
    UINT time_to_live, ULONG queue_maximum);
```

### <a name="description"></a>Descrizione

Questo servizio crea un socket UDP per l'istanza IP specificata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **socket_ptr** Puntatore al nuovo blocco di controllo socket UDP.
- **name** Nome dell'applicazione per questo socket UDP.
- **type_of_service** Definisce il tipo di servizio per la trasmissione, i valori validi sono i seguenti:
    - NX_IP_NORMAL (0x00000000)
    - NX_IP_MIN_DELAY (0x00100000)
    - NX_IP_MAX_DATA (0x00080000)
    - NX_IP_MAX_RELIABLE (0x00040000)
    - NX_IP_MIN_COST (0x00020000)
- **frammento** Specifica se è consentita o meno la frammentazione IP. Se NX_FRAGMENT_OKAY (0x0), la frammentazione IP è consentita. Se NX_DONT_FRAGMENT (0x4000), la frammentazione IP è disabilitata.
- **time_to_live** Specifica il valore a 8 bit che definisce il numero di router che questo pacchetto può passare prima di essere buttato via. Il valore predefinito viene specificato da NX_IP_TIME_TO_LIVE.
- **queue_maximum** Definisce il numero massimo di datagrammi UDP che possono essere accodati per questo socket. Dopo aver raggiunto il limite della coda, per ogni nuovo pacchetto ricevuto viene rilasciato il pacchetto UDP meno recente.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione socket UDP riuscita.
- **NX_OPTION_ERROR** (0x0A) Tipo di servizio, frammento o opzione time-to-live non valida.
- **NX_PTR_ERROR** (0x07) Puntatore IP o socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Create a UDP socket with a maximum receive queue of 30 packets.*/
status = nx_udp_socket_create(&ip_0, &udp_socket, "Sample UDP Socket",
    NX_IP_NORMAL, NX_FRAGMENT_OKAY, 0x80, 30);

/* If status is NX_SUCCESS, the new UDP socket has been created and
    is ready for binding. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_delete,
- nx_udp_socket_info_get, nx_udp_socket_port_get,
- nx_udp_socket_receive, nx_udp_socket_receive_notify,
- nx_udp_socket_send, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_delete"></a>nx_udp_socket_delete

Eliminare un socket UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_delete(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un socket UDP creato in precedenza. Se il socket è stato associato a una porta, il socket deve essere prima non associato.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket UDP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del socket riuscita.
- **NX_STILL_BOUND** (0x42) Il socket è ancora associato.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Delete a previously created UDP socket. */
status = nx_udp_socket_delete(&udp_socket);

/* If status is NX_SUCCESS, the previously created UDP socket has
    been deleted. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_info_get, nx_udp_socket_port_get,
- nx_udp_socket_receive, nx_udp_socket_receive_notify,
- nx_udp_socket_send, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_info_get"></a>nx_udp_socket_info_get

Recuperare informazioni sulle attività socket UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_info_get(
    NX_UDP_SOCKET *socket_ptr,
    ULONG *udp_packets_sent,
    ULONG *udp_bytes_sent,
    ULONG *udp_packets_received,
    ULONG *udp_bytes_received,
    ULONG *udp_packets_queued,
    ULONG *udp_receive_packets_dropped,
    ULONG *udp_checksum_errors);
```

### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle attività socket UDP per l'istanza del socket UDP specificata.

*Se un puntatore di destinazione NX_NULL, queste informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket UDP creata in precedenza.
- **udp_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti UDP inviati sul socket.
- **udp_bytes_sent** Puntatore alla destinazione per il numero totale di byte UDP inviati sul socket.
- **udp_packets_received** Puntatore alla destinazione del numero totale di pacchetti UDP ricevuti nel socket.
- **udp_bytes_received** Puntatore alla destinazione del numero totale di byte UDP ricevuti nel socket.
- **udp_packets_queued** Puntatore alla destinazione del numero totale di pacchetti UDP in coda nel socket.
- **udp_receive_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di ricezione UDP eliminati per il socket a causa del superamento delle dimensioni della coda.
- **udp_checksum_errors** Puntatore alla destinazione del numero totale di pacchetti UDP con errori di checksum nel socket.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero delle informazioni sul socket UDP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread e timer

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Retrieve UDP socket information from socket 0.*/
status = nx_udp_socket_info_get(&socket_0,
    &udp_packets_sent,
    &udp_bytes_sent,
    &udp_packets_received,
    &udp_bytes_received,
    &udp_queued_packets,
    &udp_receive_packets_dropped,
    &udp_checksum_errors);

/* If status is NX_SUCCESS, UDP socket information was retrieved.*/
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_port_get,
- nx_udp_socket_receive, nx_udp_socket_receive_notify,
- nx_udp_socket_send, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_port_get"></a>nx_udp_socket_port_get

Selezionare il numero di porta associato al socket UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_port_get(NX_UDP_SOCKET *socket_ptr, UINT *port_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il numero di porta associato al socket, utile per trovare la porta allocata da NetX nelle situazioni in cui il NX_ANY_PORT è stato specificato al momento dell'associazione del socket.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket UDP creata in precedenza.
- **port_ptr** Puntatore alla destinazione per il numero di porta restituito. I numeri di porta validi sono (1- 0xFFFF).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Associazione socket riuscita.
- **NX_NOT_BOUND** (0x24) Questo socket non è associato a una porta.
- **NX_PTR_ERROR** (0x07) Puntatore socket o puntatore di porta restituito non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Get the port number of created and bound UDP socket. */
status = nx_udp_socket_port_get(&udp_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
    socket is bound to. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_receive, nx_udp_socket_receive_notify,
- nx_udp_socket_send, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_receive"></a>nx_udp_socket_receive

Ricevere un datagramma dal socket UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_receive(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio riceve un datagramma UDP dal socket specificato. Se nessun datagramma viene accodato nel socket specificato, il chiamante viene sospeso in base all'opzione di attesa fornita.

*Se NX_SUCCESS restituito, l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket UDP creata in precedenza.
- **packet_ptr** Puntatore al puntatore a pacchetti di datagrammi UDP.
- **wait_option** Definisce il comportamento del servizio se un datagramma non è attualmente accodato in questo socket. Le opzioni di attesa sono definite nel modo seguente:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in tick (0x00000001 a 0xFFFFFFFE)

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Receive a packet from a previously created and bound UDP socket.
    If no packets are currently available, wait for 500 timer ticks
    before giving up. */
status = nx_udp_socket_receive(&udp_socket, &packet_ptr, 500);

/* If status is NX_SUCCESS, the received UDP packet is pointed to by
    packet_ptr. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive_notify,
- nx_udp_socket_send, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_receive_notify"></a>nx_udp_socket_receive_notify

Notificare all'applicazione ogni pacchetto ricevuto

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_receive_notify(
    NX_UDP_SOCKET *socket_ptr,
    VOID (*udp_receive_notify)
    (NX_UDP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio imposta il puntatore a funzione receive notify sulla funzione di callback specificata dall'applicazione. Questa funzione di callback viene quindi chiamata ogni volta che viene ricevuto un pacchetto nel socket. Se viene NX_NULL un puntatore di notifica, la funzione di notifica di ricezione è disabilitata.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket UDP.
- **udp_receive_notify** Puntatore a funzione di callback dell'applicazione chiamato quando viene ricevuto un pacchetto nel socket.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```C
/* Setup a receive packet callback function for the "udp_socket"
socket. */
status = nx_udp_socket_receive_notify(&udp_socket,
    my_receive_notify);

/* If status is NX_SUCCESS, NetX will call the function named
    "my_receive_notify" whenever a packet is received for
    "udp_socket". */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind,
- nx_udp_source_extract

## <a name="nx_udp_socket_send"></a>nx_udp_socket_send

Inviare un datagramma UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address,
    UINT port);
```

### <a name="description"></a>Descrizione

Questo servizio invia un datagramma UDP tramite un socket UDP creato in precedenza e associato. NetX trova un indirizzo IP locale appropriato come indirizzo di origine in base all'indirizzo IP di destinazione. Per specificare un'interfaccia e un indirizzo IP di origine specifici, l'applicazione deve usare il **nx_udp_socket_interface_send** servizio.

Si noti che questo servizio viene restituito immediatamente indipendentemente dal fatto che il datagramma UDP sia stato inviato correttamente.

Il socket deve essere associato a una porta locale.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza
- **packet_ptr** Puntatore al pacchetto del datagramma UDP
- **ip_address** Indirizzo IP di destinazione
- **porta** Numero di porta di destinazione valido compreso tra 1 e 0xFFFF), nell'ordine dei byte dell'host

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio socket UDP riuscito
- **NX_NOT_BOUND** (0x24) Socket non associato ad alcuna porta
- **NX_NO_INTERFACE_ADDRESS** (0x50) Non è possibile trovare alcuna interfaccia in uscita appropriata.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP del server non valido
- **NX_UNDERFLOW** (0x02) Spazio insufficiente per l'intestazione UDP nel pacchetto
- **NX_OVERFLOW** (0x03) Puntatore di accodamento pacchetti non valido
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_NOT_ENABLED** udp (0x14) non è stato abilitato
- **NX_INVALID_PORT** (0x46) Il numero di porta non è compreso in un intervallo valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
ULONG server_address;

/* Set the UDP Client IP address. */
server_address = IP_ADDRESS(1,2,3,5);

/* Send a packet to the UDP server at server_address on port 12. */
status = nx_udp_socket_send(&client_socket, packet_ptr,
    server_address, 12);

/* If status == NX_SUCCESS, the application successfully transmitted
    the packet out the UDP socket to its peer. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_interface_send,
- nx_udp_socket_unbind, nx_udp_source_extract

## <a name="nx_udp_socket_interface_send"></a>nx_udp_socket_interface_send

Inviare un datagramma tramite socket UDP.

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_interface_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address,
    UINT port,
    UINT address_index);
```

### <a name="description"></a>Descrizione

Questo servizio invia un datagramma UDP tramite un socket UDP creato in precedenza e associato tramite l'interfaccia di rete con l'indirizzo IP specificato come indirizzo di origine. Si noti che il servizio viene restituito immediatamente, indipendentemente dal fatto che il datagramma UDP sia stato inviato correttamente o meno.

### <a name="parameters"></a>Parametri

- **socket_ptr** Socket su cui trasmettere il pacchetto.
- **packet_ptr** Puntatore al pacchetto da trasmettere.
- **ip_address** Indirizzo IP di destinazione per l'invio del pacchetto.
- **porta** Porta di destinazione.
- **address_index** Indice dell'indirizzo associato all'interfaccia su cui inviare il pacchetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Il pacchetto è stato inviato correttamente.
- **NX_NOT_BOUND** (0x24) Socket non associato a una porta.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido.
- **NX_NOT_ENABLED** (0x14) UDP non abilitata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido.
- **NX_OVERFLOW** (0x03) Puntatore di accodamento di pacchetti non valido.
- **NX_UNDERFLOW** (0x02) Puntatore anteposto pacchetto non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_INVALID_INTERFACE** (0x4C) Indice di indirizzi non valido.
- **NX_INVALID_PORT** (0x46) Numero di porta superiore al numero massimo.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
#define ADDRESS_INDEX 1

/* Send packet out on port 80 to the specified destination IP on the
interface at index 1 in the IP task interface list. */
status = nx_udp_packet_interface_send(socket_ptr, packet_ptr,
    destination_ip, 80,
    ADDRESS_INDEX);

/* If status is NX_SUCCESS packet was successfully transmitted. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_unbind

## <a name="nx_udp_socket_unbind"></a>nx_udp_socket_unbind

Disassociare un socket UDP dalla porta UDP.

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_unbind(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia l'associazione tra il socket UDP e una porta UDP. Tutti i pacchetti ricevuti archiviati nella coda di ricezione vengono rilasciati come parte dell'operazione di annullamento dell'associazione.

Se sono presenti altri thread in attesa di associare un altro socket alla porta non associata, il primo thread sospeso viene quindi associato alla porta appena non associata.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Socket completato.
- **NX_NOT_BOUND** (0x24) Socket non è stato associato ad alcuna porta.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```C
/* Unbind the previously bound UDP socket. */
status = nx_udp_socket_unbind(&udp_socket);

/* If status is NX_SUCCESS, the previously bound socket is now
    unbound. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_source_extract

## <a name="nx_udp_source_extract"></a>nx_udp_source_extract

Estrarre l'INDIRIZZO IP e inviare la porta dal datagramma UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_source_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address, UINT *port);
```

### <a name="description"></a>Descrizione

Questo servizio estrae l'indirizzo IP e il numero di porta del mittente dalle intestazioni IP e UDP del datagramma UDP fornito.

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto del datagramma UDP.
- **ip_address** Puntatore valido alla variabile dell'indirizzo IP restituito.
- **porta** Puntatore valido alla variabile della porta restituita.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Estrazione porta/IP di origine completata.
- **NX_INVALID_PACKET** (0x12) Il pacchetto fornito non è valido.
- **NX_PTR_ERROR** (0x07) Pacchetto o IP o destinazione porta non valida.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```C
/* Extract the IP and port information from the sender of the UPD
    packet. */
status = nx_udp_source_extract(packet_ptr, &sender_ip_address,
    &sender_port);

/* If status is NX_SUCCESS, the sender IP and port information has
    been stored in sender_ip_address and sender_port respectively.*/
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable, nx_udp_free_port_find, nx_udp_info_get,
- nx_udp_packet_info_extract, nx_udp_socket_bind,
- nx_udp_socket_bytes_available, nx_udp_socket_checksum_disable,
- nx_udp_socket_checksum_enable, nx_udp_socket_create,
- nx_udp_socket_delete, nx_udp_socket_info_get,
- nx_udp_socket_port_get, nx_udp_socket_receive,
- nx_udp_socket_receive_notify, nx_udp_socket_send,
- nx_udp_socket_interface_send, nx_udp_socket_unbind