---
title: Capitolo 4-Descrizione dei servizi NetX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi NetX di Azure RTO in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 720e573b53070a754618830134f63a8421b9fd29
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821545"
---
# <a name="chapter-4---description-of-azure-rtos-netx-services"></a>Capitolo 4-Descrizione dei servizi NetX di Azure RTO

Questo capitolo contiene una descrizione di tutti i servizi NetX di Azure RTO in ordine alfabetico. I nomi dei servizi sono progettati in modo da raggruppare tutti i servizi simili. Ad esempio, tutti i servizi ARP sono disponibili all'inizio di questo capitolo.

> [!NOTE]
> *Si noti che un'API socket BSD-Compatible è disponibile per il codice dell'applicazione legacy che non è in grado di sfruttare appieno l'API NetX a prestazioni elevate. Per altre informazioni sull'API socket BSD-Compatible, vedere l'Appendice D.*

Nella sezione "valori restituiti" di ogni descrizione, i valori in **grassetto** non sono interessati dall'opzione NX_DISABLE_ERROR_CHECKING usata per disabilitare il controllo degli errori dell'API, mentre i valori in grassetto non sono completamente disabilitati. Le sezioni "consentito da" indicano che è possibile chiamare ogni servizio NetX.

## <a name="nx_arp_dynamic_entries_invalidate"></a>nx_arp_dynamic_entries_invalidate

Invalida tutte le voci dinamiche nella cache ARP

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_dynamic_entries_invalidate(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio invalida tutte le voci ARP dinamiche attualmente presenti nella cache ARP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- L'invalidamento della cache ARP riuscita **NX_SUCCESS** (0x00).
- **NX_NOT_ENABLED** (0X14) ARP non è abilitato.
- **NX_PTR_ERROR** (0x07) indirizzo IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Imposta voce ARP dinamica

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_dynamic_entry_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a>Descrizione

Questo servizio alloca una voce dinamica dalla cache ARP e imposta l'indirizzo IP specificato sul mapping degli indirizzi fisici. Se viene specificato un indirizzo fisico zero, alla rete viene inviata una richiesta ARP effettiva per poter risolvere l'indirizzo fisico. Si noti inoltre che questa voce verrà rimossa se ARP aging è attivo o se la cache ARP è esaurita e si tratta della voce ARP usata meno di recente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP da mappare.
- **physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico.
- **physical_lsw** Inferiore 32 bit (31-0) dell'indirizzo fisico.

### <a name="return-values"></a>Valori restituiti

- Il set di voci dinamiche ARP riuscite **NX_SUCCESS** (0x00).
- **NX_NO_MORE_ENTRIES** (0x17) non sono disponibili altre voci ARP nella cache ARP.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) puntatore a istanza IP non valido.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio Inizializza il componente ARP di NetX per l'istanza IP specifica. L'inizializzazione ARP include la configurazione della cache ARP e delle varie routine di elaborazione ARP necessarie per l'invio e la ricezione di messaggi ARP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **arp_cache_memory** Puntatore all'area memoria per inserire la cache ARP.
- **arp_cache_size** Ogni voce ARP è 52 byte, il numero totale di voci ARP è, di conseguenza, la dimensione divisa per 52.

### <a name="return-values"></a>Valori restituiti

- Abilitazione ARP riuscita **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) un puntatore di memoria cache o un indirizzo IP non valido.
- La memoria della cache ARP fornita dall'utente **NX_SIZE_ERROR** (0x09) è troppo piccola.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_ALREADY_ENABLED** (0X15) questo componente è già stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio attraversa tutte le interfacce fisiche per trasmettere richieste ARP gratuite, purché l'indirizzo IP dell'interfaccia sia valido. Se successivamente viene ricevuta una risposta ARP, viene chiamato il gestore di risposta fornito per elaborare la risposta all'ARP gratuito.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **response_handler** Puntatore alla funzione di gestione delle risposte. Se viene specificato NX_NULL, le risposte verranno ignorate.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) la trasmissione ARP gratuita è stata completata.
- **NX_NO_PACKET** (0x01) non è disponibile alcun pacchetto.
- **NX_NOT_ENABLED** (0X14) ARP non è abilitato.
- L'indirizzo IP corrente **NX_IP_ADDRESS_ERROR** (0x21) non è valido.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio tenta di trovare un indirizzo hardware fisico nella cache ARP che è associato all'indirizzo IP specificato.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP da cercare.
- **physical_msw** Puntatore alla variabile per la restituzione dei primi 16 bit (47-32) dell'indirizzo fisico.
- **physical_lsw** Puntatore alla variabile per la restituzione dei 32 bit inferiori (31-0) dell'indirizzo fisico.

### <a name="return-values"></a>Valori restituiti

- Ricerca di indirizzi hardware ARP riuscita **NX_SUCCESS** (0x00).
- Il mapping di **NX_ENTRY_NOT_FOUND** (0x16) non è stato trovato nella cache ARP.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) un puntatore di memoria o un indirizzo IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **arp_requests_sent** Puntatore alla destinazione per le richieste ARP totali inviate da questa istanza IP.
- **arp_requests_received** Puntatore alla destinazione per le richieste ARP totali ricevute dalla rete.
- **arp_responses_sent** Puntatore alla destinazione per le risposte ARP totali inviate da questa istanza IP.
- **arp_responses_received** Puntatore alla destinazione per le risposte ARP totali ricevute dalla rete.
- **arp_dynamic_entries** Puntatore alla destinazione per il numero corrente di voci ARP dinamiche.
- **arp_static_entries** Puntatore alla destinazione per il numero corrente di voci ARP statiche.
- **arp_aged_entries** Puntatore alla destinazione del numero totale di voci ARP obsolete e diventate non valide.
- **arp_invalid_messages** Puntatore alla destinazione del totale dei messaggi ARP non validi ricevuti.

### <a name="return-values"></a>Valori restituiti

- Il recupero delle informazioni ARP riuscite **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Individuare l'indirizzo IP in base a un indirizzo fisico

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_ip_address_find(
    NX_IP *ip_ptr, 
    ULONG *ip_address,
    ULONG physical_msw, 
    ULONG physical_lsw);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di trovare un indirizzo IP nella cache ARP associata all'indirizzo fisico fornito.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **ip_address** Puntatore per restituire l'indirizzo IP, se ne viene trovato uno mappato.
- **physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico da cercare.
- **physical_lsw** Inferiore 32 bit (31-0) dell'indirizzo fisico da cercare.

### <a name="return-values"></a>Valori restituiti

- Ricerca di indirizzi IP ARP riusciti **NX_SUCCESS** (0x00)
- Il mapping di **NX_ENTRY_NOT_FOUND** (0x16) non è stato trovato nella cache ARP.
- **NX_PTR_ERROR** (0x07) un puntatore di memoria o un indirizzo IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.
- **NX_INVALID_PARAMETERS** (irreversibile 0x4d) Physical_msw e physical_lsw sono entrambi 0.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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
- nx_arp_static_entries_delete, nx_arp_static_entry_create,
- nx_arp_static_entry_delete

## <a name="nx_arp_static_entries_delete"></a>nx_arp_static_entries_delete

Elimina tutte le voci ARP statiche

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_static_entries_delete(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina tutte le voci statiche nella cache ARP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- Vengono eliminate le voci statiche **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) Ip_ptr puntatore non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Creare un indirizzo IP statico al mapping hardware nella cache ARP

### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_static_entry_create(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a>Descrizione

Questo servizio crea un mapping statico da indirizzo IP a fisico nella cache ARP per l'istanza IP specificata. Le voci ARP statiche non sono soggette ad aggiornamenti periodici ARP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP da mappare.
- **physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico da mappare.
- **physical_lsw** Inferiore 32 bit (31-0) dell'indirizzo fisico da mappare.

### <a name="return-values"></a>Valori restituiti

- Creazione di una voce statica ARP riuscita **NX_SUCCESS** (0x00).
- **NX_NO_MORE_ENTRIES** (0x17) non sono disponibili altre voci ARP nella cache ARP.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.
- **NX_INVALID_PARAMETERS** (irreversibile 0x4d) Physical_msw e physical_lsw sono entrambi 0.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Eliminare l'indirizzo IP statico al mapping hardware nella cache ARP


### <a name="prototype"></a>Prototipo

```C
UINT nx_arp_static_entry_delete(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG physical_msw,
    ULONG physical_lsw);
```

### <a name="description"></a>Descrizione

Questo servizio trova ed elimina un mapping statico da indirizzo IP a fisico creato in precedenza nella cache ARP per l'istanza IP specificata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP mappato in modo statico.
- **physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico mappato in modo statico.
- **physical_lsw** Inferiore 32 bit (31-0) dell'indirizzo fisico mappato in modo statico.

### <a name="return-values"></a>Valori restituiti

- Eliminazione di una voce statica ARP riuscita **NX_SUCCESS** (0x00).
- La voce ARP statica **NX_ENTRY_NOT_FOUND** (0x16) non è stata trovata nella cache ARP.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.
- **NX_INVALID_PARAMETERS** (irreversibile 0x4d) Physical_msw e physical_lsw sono entrambi 0.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Abilita Internet Control Message Protocol (ICMP)

### <a name="prototype"></a>Prototipo

```C
UINT nx_icmp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita il componente ICMP per l'istanza IP specificata.
Il componente ICMP è responsabile della gestione dei messaggi di errore Internet e delle richieste di ping e delle risposte.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- Abilitazione ICMP riuscita **NX_SUCCESS** (0x00).
- Il protocollo ICMP **NX_ALREADY_ENABLED** (0x15) è già abilitato.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **pings_sent** Puntatore alla destinazione per il numero totale di ping inviati.
- **ping_timeouts** Puntatore alla destinazione per il numero totale di timeout del ping.
- **ping_threads_suspended** Puntatore alla destinazione del numero totale di thread sospesi nelle richieste di ping.
- **ping_responses_received** Puntatore a ESTINAZIONE del numero totale di risposte ping ricevute.
- **icmp_checksum_errors** Puntatore alla destinazione del numero totale di errori di checksum ICMP.
- **icmp_unhandled_messages** Puntatore a ESTINAZIONE del numero totale di messaggi ICMP non gestiti.

### <a name="return-values"></a>Valori restituiti

- Il recupero delle informazioni ICMP riuscite **NX_SUCCESS** (0x00).
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Invia richiesta ping all'indirizzo IP specificato

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

Questo servizio invia una richiesta ping all'indirizzo IP specificato e attende il periodo di tempo specificato per un messaggio di risposta ping. Se non viene ricevuta alcuna risposta, viene restituito un errore. In caso contrario, viene restituito l'intero messaggio di risposta nella variabile a cui punta response_ptr.

*Se viene restituito NX_SUCCESS, l'applicazione è responsabile del rilascio del pacchetto ricevuto dopo che non è più necessario.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP, in ordine byte host, per eseguire il ping. Puntatore dati all'area dati per il messaggio ping.
- **DATA_SIZE** Numero di byte nei dati ping
- **response_ptr** Puntatore al puntatore del pacchetto per restituire il messaggio di risposta ping in.
- **WAIT_OPTION** Definisce il tempo di attesa per una risposta ping. le opzioni di attesa sono definite come segue:

  - NX_NO_WAIT (0x00000000)
  - NX_WAIT_FOREVER (0xFFFFFFFF)
  - valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ping riuscito. Il puntatore del messaggio di risposta è stato inserito nella variabile a cui punta response_ptr.
- **NX_NO_PACKET** (0x01) non è in grado di allocare un pacchetto di richieste ping.
- L'area dati specificata **NX_OVERFLOW** (0x03) supera la dimensione predefinita del pacchetto per questa istanza IP.
- L'IP richiesto **NX_NO_RESPONSE** (0x29) non ha risposto.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) un puntatore IP o risposta non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Abilita IGMP (Internet Group Management Protocol)

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita il componente IGMP nell'istanza IP specificata.
Il componente IGMP è responsabile della fornitura del supporto per le operazioni di gestione dei gruppi multicast IP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- L'abilitazione di IGMP è riuscita **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_ALREADY_ENABLED** (0X15) questo componente è già stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

No

### <a name="example"></a>Esempio

```C
/* Enable IGMP on the previously created IP Instance ip_0. */
status = nx_igmp_enable(&ip_0);

/* If status is NX_SUCCESS, IGMP is enabled. */
```

### <a name="see-also"></a>Vedere anche

- nx_igmp_info_get, nx_igmp_loopback_disable,
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

*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **igmp_reports_sent** Puntatore alla destinazione per il numero totale di report ICMP inviati.
- **igmp_queries_received** Puntatore alla destinazione per il numero totale di query ricevute dal router multicast.
- **igmp_checksum_errors** Puntatore alla destinazione del numero totale di errori di checksum IGMP nei pacchetti di ricezione.
- **current_groups_joined** Puntatore alla destinazione del numero corrente di gruppi Uniti tramite questa istanza IP.

### <a name="return-values"></a>Valori restituiti

- Il recupero delle informazioni IGMP riuscite **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio Disabilita il loopback IGMP per tutti i gruppi multicast successivi Uniti in join.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) la disabilitazione del loopback IGMP è riuscita.
- Il **NX_NOT_ENABLED** (0X14) IGMP non è abilitato.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Abilita loopback loopback

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_loopback_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita il loopback IGMP per tutti i gruppi multicast successivi Uniti in join.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) la disabilitazione del loopback IGMP è riuscita.
- Il **NX_NOT_ENABLED** (0X14) IGMP non è abilitato.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

No

### <a name="example"></a>Esempio

```C
/* Enable IGMP loopback for all subsequent multicast groups joined. */
status = nx_igmp_loopback_enable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is enabled. */
```

### <a name="see-also"></a>Vedere anche

- nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,
- nx_igmp_multicast_interface_join, nx_igmp_multicast_join,
- nx_igmp_multicast_leave

## <a name="nx_igmp_multicast_interface_join"></a>nx_igmp_multicast_interface_join

Unisci istanza IP al gruppo multicast specificato tramite un'interfaccia

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_multicast_interface_join(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio unisce un'istanza IP al gruppo multicast specificato tramite un'interfaccia di rete specificata. Viene mantenuto un contatore interno per tenere traccia del numero di volte in cui lo stesso gruppo è stato aggiunto. Dopo l'aggiunta al gruppo multicast, il componente IGMP consentirà la ricezione di pacchetti IP con questo indirizzo di gruppo tramite l'interfaccia di rete specificata e segnalerà anche ai router che questo IP è membro di questo gruppo multicast. I messaggi di join di appartenenza IGMP, di report e di uscita vengono inviati anche tramite l'interfaccia di rete specificata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **group_address** Indirizzo del gruppo multicast IP di classe D da unire in ordine byte host.
- **interface_index** Indice dell'interfaccia associata all'istanza di NetX.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) il join del gruppo multicast è riuscito.
- **NX_NO_MORE_ENTRIES** (0x17) non è possibile unire in join più gruppi multicast. è stato superato il limite massimo.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- L'indice del dispositivo **NX_INVALID_INTERFACE** (0x4C) punta a un'interfaccia di rete non valida.
- L'indirizzo del gruppo multicast **NX_IP_ADDRESS_ERROR** (0x21) specificato non è un indirizzo di classe D valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- Il supporto multicast IP **NX_NOT_ENABLED** (0x14) non è abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

- nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_join,
- nx_igmp_multicast_leave

## <a name="nx_igmp_multicast_join"></a>nx_igmp_multicast_join

Unisci istanza IP al gruppo multicast specificato

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_multicast_join(
    NX_IP *ip_ptr, 
    ULONG group_address);
```

### <a name="description"></a>Descrizione

Questo servizio unisce un'istanza IP al gruppo multicast specificato. Viene mantenuto un contatore interno per tenere traccia del numero di volte in cui lo stesso gruppo è stato aggiunto. Il driver viene indirizzato per l'invio di un report IGMP se si tratta della prima richiesta di join in rete che indica l'intenzione dell'host di partecipare al gruppo. Dopo l'Unione, il componente IGMP consentirà la ricezione di pacchetti IP con questo indirizzo di gruppo e report ai router che questo IP è membro di questo gruppo multicast.

> [!NOTE]
> *Per aggiungere un gruppo multicast in un dispositivo non primario, usare il nx_igmp_multicast_interface_join di servizio **.***

- **Parametri**

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **group_address** Indirizzo del gruppo multicast IP di classe D da unire.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) il join del gruppo multicast è riuscito.
- **NX_NO_MORE_ENTRIES** (0x17) non è possibile unire in join più gruppi multicast. è stato superato il limite massimo.
- L'indice del dispositivo **NX_INVALID_INTERFACE** (0x4C) punta a un'interfaccia di rete non valida.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo del gruppo IP non valido.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

- nx_igmp_enable, nx_igmp_info_get, nx_igmp_loopback_disable,
- nx_igmp_loopback_enable, nx_igmp_multicast_interface_join,
- nx_igmp_multicast_leave

## <a name="nx_igmp_multicast_leave"></a>nx_igmp_multicast_leave

Genera l'istanza IP per uscire dal gruppo multicast specificato

### <a name="prototype"></a>Prototipo

```C
UINT nx_igmp_multicast_leave(
    NX_IP *ip_ptr, 
    ULONG group_address);
```

### <a name="description"></a>Descrizione

Questo servizio fa in modo che un'istanza IP lasci il gruppo multicast specificato, se il numero di richieste Leave corrisponde al numero di richieste di join. In caso contrario, il conteggio interno dei join viene semplicemente decrementato.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **group_address** Gruppo multicast da lasciare.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) il join del gruppo multicast è riuscito.
- Impossibile trovare **NX_ENTRY_NOT_FOUND** (0x16) la richiesta di join precedente.
- L'indice del dispositivo **NX_INVALID_INTERFACE** (0x4C) punta a un'interfaccia di rete non valida.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo del gruppo IP non valido.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Notifica all'applicazione se le modifiche all'indirizzo IP


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

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **CHANGE_NOTIFY** Puntatore alla funzione di notifica della modifica IP. Se questo parametro è NX_NULL, la notifica di modifica degli indirizzi IP è disabilitata.
- **additional_info** Puntatore a informazioni aggiuntive facoltative fornite anche alla funzione di notifica quando viene modificato l'indirizzo IP.

### <a name="return-values"></a>Valori restituiti

- Notifica di modifica dell'indirizzo IP riuscita **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Recuperare l'indirizzo IP e la network mask

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_address_get(
    NX_IP *ip_ptr,
    ULONG *ip_address,
    ULONG *network_mask);
```

### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IP e il relativo subnet mask dell'interfaccia di rete primaria.

* Per ottenere informazioni sul dispositivo secondario, usare il servizio
- **nx_ip_interface_address_get**. *

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **ip_address** Puntatore alla destinazione per l'indirizzo IP.
- **network_mask** Puntatore alla destinazione per network mask.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) indirizzo IP riuscito Get.
- **NX_PTR_ERROR** (0x07) indirizzo IP non valido o puntatore alla variabile restituita.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Imposta indirizzo IP e network mask

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_address_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG network_mask);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP e il network mask per l'interfaccia di rete primaria.

*Per impostare l'indirizzo IP e il network mask per il dispositivo secondario, usare il **nx_ip_interface_address_set** del servizio.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **ip_address** Nuovo indirizzo IP.
- **network_mask** Nuovo network mask.

### <a name="return-values"></a>Valori restituiti

- Set di indirizzi IP riusciti **NX_SUCCESS** (0x00).
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio crea un'istanza IP con l'indirizzo IP e il driver di rete specificati dall'utente. Inoltre, l'applicazione deve fornire un pool di pacchetti creato in precedenza per l'istanza IP da usare per l'allocazione dei pacchetti interna. Si noti che il driver di rete dell'applicazione fornito non viene chiamato fino a quando non viene eseguito il thread di questo indirizzo IP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore al blocco di controllo per creare una nuova istanza di IP.
- **nome** Nome della nuova istanza di IP.
- **ip_address** Indirizzo IP per la nuova istanza di IP.
- **network_mask** Maschera per delineare la parte di rete dell'indirizzo IP per la suddivisione in subnet e l'uso di super-reti.
- **default_pool** Puntatore al blocco di controllo del pool di pacchetti NetX creato in precedenza.
- **ip_network_driver** Driver di rete fornito dall'utente utilizzato per inviare e ricevere pacchetti IP.
- **memory_ptr** Puntatore all'area di memoria per l'area dello stack del thread helper IP.
- **memory_size** Numero di byte nell'area di memoria per lo stack del thread helper IP.
- **priorità** di Priorità del thread helper IP.

### <a name="return-values"></a>Valori restituiti
- Creazione dell'istanza IP riuscita **NX_SUCCESS** (0x00).
- La libreria NetX **NX_NOT_IMPLEMENTED** (0x4A) non è configurata correttamente.
- **NX_PTR_ERROR** (0x07) IP non valido, puntatore alla funzione del driver di rete, pool di pacchetti o puntatore di memoria.
- **NX_SIZE_ERROR** (0x09) la dimensione dello stack fornita è troppo piccola.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_IP_ADDRESS_ERROR** (0X21) l'indirizzo IP specificato non è valido.
- **NX_OPTION_ERROR** (0X21) la priorità del thread IP specificata non è valida.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Elimina istanza IP creata in precedenza


### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_delete(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza IP creata in precedenza e rilascia tutte le risorse di sistema di proprietà dell'istanza IP.

### <a name="parameters"></a>Parametri
- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- Eliminazione IP riuscita **NX_SUCCESS** (0x00).
- **NX_SOCKETS_BOUND** (0x28) a questa istanza IP sono ancora associati socket UDP o TCP. Prima di eliminare l'istanza IP, è necessario che tutti i socket siano non associati ed eliminati.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Invia comando al driver di rete

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_driver_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    ULONG *return_value_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio fornisce un'interfaccia diretta al driver dell'interfaccia di rete primaria dell'applicazione specificato durante la chiamata di ***nx_ip_create*** .

I comandi specifici dell'applicazione possono essere utilizzati per fornire un valore numerico maggiore o uguale a NX_LINK_USER_COMMAND.

*Per eseguire il comando per il dispositivo secondario, usare il servizio **nx_ip_driver_interface_direct_command** .*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **comando** Codice di comando numerico. I comandi standard vengono definiti come segue:

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

- **NX_SUCCESS** (0x00) il comando diretto del driver di rete è riuscito.
- Comando del driver di rete non gestito o non implementato **NX_UNHANDLED_COMMAND** (0x44).
- **NX_PTR_ERROR** (0x07) un indirizzo IP o un puntatore al valore restituito non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_INVALID_INTERFACE** (0x4C) indice di interfaccia non valido.

### <a name="allowed-from"></a>Consentito da

Thread

- **Precedenza possibile**

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

Invia comando al driver di rete

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_driver_interface_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    UINT interface_index,
    ULONG *return_value_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio fornisce un comando diretto al driver di dispositivo di rete dell'applicazione nell'istanza di IP. I comandi specifici dell'applicazione possono essere utilizzati per fornire un valore numerico maggiore o uguale a *NX_LINK_USER_COMMAND*.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **comando** Codice di comando numerico. I comandi standard vengono definiti come segue:
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
- **NX_SUCCESS** (0x00) il comando diretto del driver di rete è riuscito.
- Comando del driver di rete non gestito o non implementato **NX_UNHANDLED_COMMAND** (0x44).
- Indice di interfaccia **NX_INVALID_INTERFACE** (0X4C) non valido
- **NX_PTR_ERROR** (0x07) un indirizzo IP o un puntatore al valore restituito non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Disabilitare l'invio di pacchetti IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_forwarding_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Disabilita l'invio di pacchetti IP all'interno del componente NetX IP. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) la disabilitazione dell'invio IP è riuscita.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Precedenza possibile

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

Abilita l'invio di pacchetti IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_forwarding_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio consente l'invio di pacchetti IP all'interno del componente NetX IP. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) abilitata per l'invio di indirizzi IP riuscita.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Precedenza possibile

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

Disabilitare la frammentazione di pacchetti IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_fragment_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Disabilita la funzionalità di riassemblaggio e frammentazione di pacchetti IP. Per i pacchetti in attesa di essere riassemblati, questo servizio rilascia questi pacchetti. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) la disabilitazione del FRAMMENTo IP è riuscita.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- La frammentazione IP **NX_NOT_ENABLED** (0x14) non è abilitata nell'istanza IP.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Abilitare la frammentazione di pacchetti IP

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_fragment_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita la funzionalità di frammentazione e riassemblaggio di pacchetti IP. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- Abilitazione del frammento IP **NX_SUCCESS** (0x00) riuscita.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- Le funzionalità di frammentazione IP **NX_NOT_ENABLED** (0x14) non vengono compilate in NETX.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio imposta l'indirizzo IP del gateway IP. Tutto il traffico fuori rete viene indirizzato a questo gateway per la trasmissione. Il gateway deve essere direttamente accessibile tramite una delle interfacce di rete.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP del gateway.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) set di indirizzi IP del gateway riuscito.
- **NX_PTR_ERROR** (0x07) puntatore a istanza IP non valido.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
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

- Il recupero delle informazioni IP riuscite **NX_SUCCESS** (0x00).
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

*Il dispositivo specificato, se non il dispositivo primario, deve essere precedentemente collegato all'istanza IP.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **interface_index** Indice dell'interfaccia, lo stesso valore dell'indice per l'interfaccia di rete collegata all'istanza IP.
- **ip_address** Puntatore alla destinazione per l'indirizzo IP dell'interfaccia del dispositivo.
- **network_mask** Puntatore alla destinazione per l'interfaccia del dispositivo network mask.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) indirizzo IP riuscito Get.
- L'interfaccia di rete specificata **NX_INVALID_INTERFACE** (0x4C) non è valida.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Impostare l'indirizzo IP e la network mask dell'interfaccia

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_interface_address_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG ip_address,
    ULONG network_mask);
```

### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP e il network mask per l'interfaccia IP specificata.

*L'interfaccia specificata deve essere precedentemente collegata all'istanza IP.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **interface_index** Indice dell'interfaccia associata all'istanza di NetX.
- **ip_address** Nuovo indirizzo IP dell'interfaccia di rete.
- **network_mask** Nuova interfaccia network mask.

### <a name="return-values"></a>Valori restituiti

- Set di indirizzi IP riusciti **NX_SUCCESS** (0x00).
- L'interfaccia di rete specificata **NX_INVALID_INTERFACE** (0x4C) non è valida.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_PTR_ERROR** (0x07) puntatori non validi.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio aggiunge un'interfaccia di rete fisica all'interfaccia IP. Si noti che l'istanza IP viene creata con l'interfaccia primaria, quindi ogni interfaccia aggiuntiva è secondaria all'interfaccia primaria. Il numero totale di interfacce di rete collegate all'istanza IP (inclusa l'interfaccia primaria) non può superare **NX_MAX_PHYSICAL_INTERFACES**.

Se il thread IP non è ancora in esecuzione, le interfacce secondarie verranno inizializzate come parte del processo di avvio del thread IP che inizializza tutte le interfacce fisiche.

Se il thread IP non è ancora in esecuzione, l'interfaccia secondaria viene inizializzata come parte del servizio ***nx_ip_interface_attach*** .

*ip_ptr deve puntare a una struttura IP NetX valida.*

- *Per il numero di interfacce di rete per l'istanza IP, è necessario configurare **NX_MAX_PHYSICAL_INTERFACES** . Il valore predefinito è uno.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **INTERFACE_NAME** Puntatore alla stringa del nome di interfaccia.
- **ip_address** Indirizzo IP del dispositivo nell'ordine dei byte dell'host.
- **network_mask** Network mask del dispositivo nell'ordine dei byte dell'host.
- **ip_link_driver** Driver Ethernet per l'interfaccia.

### <a name="return-values"></a>Valori restituiti

- La voce **NX_SUCCESS** (0x00) viene aggiunta alla tabella di routing statica.
- Numero massimo di interfacce **NX_NO_MORE_ENTRIES** (0x17).
- Viene superato **NX_MAX_PHYSICAL_INTERFACES** .
- **NX_DUPLICATED_ENTRY** (0X52) l'indirizzo IP specificato è già in uso in questa istanza IP.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- L'input del puntatore **NX_PTR_ERROR** (0x07) non è valido.
- **NX_IP_ADDRESS_ERROR** (0x21) l'input dell'indirizzo IP non è valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

*ip_ptr deve puntare a una struttura IP NetX valida. L'interfaccia specificata, se non l'interfaccia primaria, deve essere precedentemente collegata all'istanza IP.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **interface_index** Indice che specifica l'interfaccia di rete.
- **INTERFACE_NAME** Puntatore al buffer che include il nome dell'interfaccia di rete.
- **ip_address** Puntatore alla destinazione per l'indirizzo IP dell'interfaccia.
- **network_mask** Puntatore alla destinazione per network mask.
- **mtu_size** Puntatore alla destinazione per l'unità di trasferimento massima per questa interfaccia.
- **physical_address_msw** Puntatore alla destinazione per i primi 16 bit dell'indirizzo MAC del dispositivo.
- **physical_address_lsw** Puntatore alla destinazione per i 32 bit inferiori dell'indirizzo MAC del dispositivo.


### <a name="return-values"></a>Valori restituiti
- Sono state ottenute le informazioni sull'interfaccia **NX_SUCCESS** (0x00).
- L'input del puntatore **NX_PTR_ERROR** (0x07) non è valido.
- **NX_INVALID_INTERFACE** (0x4C) puntatore IP non valido.
- Il servizio **NX_CALLER_ERROR** (0x11) non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio controlla ed eventualmente attende lo stato specificato dell'interfaccia di rete di un'istanza IP creata in precedenza.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **interface_index** Numero di indice dell'interfaccia
- **needed_status** Stato IP richiesto, definito in formato mappa di bit, come indicato di seguito:
    - NX_IP_INITIALIZE_DONE (0x0001)
    - NX_IP_ADDRESS_RESOLVED (0x0002)
    - NX_IP_LINK_ENABLED (0x0004)
    - NX_IP_ARP_ENABLED (0x0008)
    - NX_IP_UDP_ENABLED (0x0010)
    - NX_IP_TCP_ENABLED (0x0020)
    - NX_IP_IGMP_ENABLED (0x0040)
    - NX_IP_RARP_COMPLETE (0x0080)
    - NX_IP_INTERFACE_LINK_ENABLED (0x0100)
- **actual_status** Puntatore alla destinazione del set di bit effettivo.
- **WAIT_OPTION** Definisce il comportamento del servizio se i bit di stato richiesti non sono disponibili. Le opzioni di attesa sono definite come segue:
    - NX_NO_WAIT (0x00000000)
    - NX_WAIT_FOREVER (0xFFFFFFFF)
    - valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Verifica stato IP riuscito.
- La richiesta di stato **NX_NOT_SUCCESSFUL** (0x43) non è stata soddisfatta entro il timeout specificato.
- Il puntatore IP **NX_PTR_ERROR** (0x07) è o è diventato non valido oppure il puntatore di stato effettivo non è valido.
- **NX_OPTION_ERROR** (0x0A) opzione di stato necessaria non valida.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- Il Interface_index **NX_INVALID_INTERFACE** (0x4C) non è compreso nell'intervallo. oppure l'interfaccia non è valida.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Impostare la funzione di callback notifica modifica stato collegamento

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_link_status_change_notify_set(
    NX_IP *ip_ptr,
    VOID (*link_status_change_notify)(NX_IP *ip_ptr, UINT interface_index, UINT link_up));
```

### <a name="description"></a>Descrizione

Questo servizio configura la funzione di callback notifica modifica stato collegamento. La routine di *link_status_change_notify* fornita dall'utente viene richiamata quando viene modificato lo stato dell'interfaccia primaria o secondaria, ad esempio se viene modificato l'indirizzo IP. Se *link_status_change_notify* è null, la funzionalità di callback notifica modifica stato collegamento è disabilitata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore del blocco di controllo IP
- **link_status_change_notify** Funzione di callback fornita dall'utente da chiamare su una modifica all'interfaccia fisica.


### <a name="return-values"></a>Valori restituiti

- Set di **NX_SUCCESS** (0x00) riuscito
- **NX_PTR_ERROR** (0x07) puntatore a blocco di controllo IP non valido o nuovo puntatore a indirizzo fisico
- Il servizio **NX_CALLER_ERROR** (0x11) non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.


### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio Disabilita la trasmissione e la ricezione di pacchetti IP non elaborati per questa istanza IP. Se il servizio pacchetti non elaborati è stato precedentemente abilitato e sono presenti pacchetti non elaborati nella coda di ricezione, il servizio rilascerà tutti i pacchetti non elaborati ricevuti.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) la disabilitazione del pacchetto non elaborato IP è riuscita.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Abilita elaborazione pacchetti non elaborati


### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_raw_packet_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio consente la trasmissione e la ricezione di pacchetti IP non elaborati per questa istanza IP. I pacchetti TCP, UDP, ICMP e IGMP in ingresso vengono ancora elaborati da NetX. I pacchetti con tipi di protocollo di livello superiore sconosciuti vengono elaborati dalla routine di ricezione dei pacchetti non elaborati.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) abilitata per i pacchetti non elaborati IP riusciti.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio invia un pacchetto IP non elaborato all'indirizzo IP di destinazione utilizzando l'indirizzo IP locale specificato come indirizzo di origine e tramite l'interfaccia di rete associata. Si noti che questa routine restituisce immediatamente un risultato e, pertanto, non è noto se il pacchetto IP è effettivamente stato inviato. Il driver di rete sarà responsabile del rilascio del pacchetto al termine della trasmissione. Questo servizio differisce da altri servizi in quanto non esiste alcun modo per sapere se il pacchetto è stato effettivamente inviato. Potrebbe andare persa in Internet.

*Si noti che è necessario abilitare l'elaborazione di indirizzi IP non elaborati.*

*Questo servizio è simile a **nx_ip_raw_packet_send**, ad eccezione del fatto che questo servizio consente a un'applicazione di inviare pacchetti IP non elaborati da un'interfaccia fisica specificata.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'attività IP creata in precedenza.
- **packet_ptr** Puntatore al pacchetto da trasmettere.
- **destination_ip** Indirizzo IP per l'invio del pacchetto.
- **address_index** Indice dell'indirizzo dell'interfaccia su cui inviare il pacchetto.
- **Type_of_Service** Tipo di servizio per il pacchetto.

### <a name="return-values"></a>Valori restituiti

- Il pacchetto **NX_SUCCESS** (0x00) è stato trasmesso correttamente.
- **NX_IP_ADDRESS_ERROR** (0X21) non è disponibile alcuna interfaccia in uscita adatta.
- L'elaborazione dei pacchetti IP non elaborati **NX_NOT_ENABLED** (0x14) non è abilitata.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- L'input del puntatore **NX_PTR_ERROR** (0x07) non è valido.
- Il tipo di servizio specificato **NX_OPTION_ERROR** (0X0A) non è valido.
- **NX_OVERFLOW** (0x03) puntatore a anteporre il pacchetto non valido.
- **NX_UNDERFLOW** (0x02) puntatore a anteporre il pacchetto non valido.
- **NX_INVALID_INTERFACE** (0x4C) è stato specificato un indice di interfaccia non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Ricevi pacchetto IP non elaborato

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_raw_packet_receive(
    NX_IP *ip_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio riceve un pacchetto IP non elaborato dall'istanza IP specificata. Se nella coda di ricezione di pacchetti non elaborati sono presenti pacchetti IP, il primo pacchetto (meno recente) viene restituito al chiamante. In caso contrario, se non sono disponibili pacchetti, il chiamante potrebbe sospendere come specificato dall'opzione wait.

*Se viene restituito NX_SUCCESS, l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **packet_ptr** Puntatore al puntatore in cui inserire il pacchetto IP non elaborato ricevuto.
- **WAIT_OPTION** Definisce il comportamento del servizio se non sono disponibili pacchetti IP non elaborati. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) la ricezione di pacchetti non elaborati IP riuscita.
- **NX_NO_PACKET** (0x01) non è disponibile alcun pacchetto.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.
- **NX_PTR_ERROR** (0x07) indirizzo IP non valido o puntatore al pacchetto restituito.
- **NX_CALLER_ERROR** (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Invia pacchetto IP non elaborato

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_raw_packet_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    ULONG type_of_service);
```

### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto IP non elaborato all'indirizzo IP di destinazione. Si noti che questa routine viene restituita immediatamente e non è quindi noto se il pacchetto IP è stato effettivamente inviato. Il driver di rete sarà responsabile del rilascio del pacchetto al termine della trasmissione.

Per un sistema multihome, NetX usa l'indirizzo IP di destinazione per trovare un'interfaccia di rete appropriata e usa l'indirizzo IP dell'interfaccia come indirizzo di origine. Se l'indirizzo IP di destinazione è broadcast o multicast, viene utilizzata la prima interfaccia valida. In questo caso, le applicazioni usano la ***nx_ip_raw_packet_interface_send*** .

*A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché il driver di rete rilascerà il pacchetto dopo la trasmissione.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **packet_ptr** Puntatore al pacchetto IP non elaborato da inviare.
- **destination_ip** Indirizzo IP di destinazione, che può essere un indirizzo IP host specifico, una trasmissione di rete, un ciclo interno o un indirizzo multicast.
- **Type_of_Service** Definisce il tipo di servizio per la trasmissione. i valori validi sono i seguenti:
- NX_IP_NORMAL (0x00000000)
- NX_IP_MIN_DELAY (0x00100000)
- NX_IP_MAX_DATA (0x00080000)
- NX_IP_MAX_RELIABLE (0x00040000)
- NX_IP_MIN_COST (0x00020000)


### <a name="return-values"></a>Valori restituiti

- È stata avviata l'operazione di invio di pacchetti non elaborati non elaborati (0x00) **NX_SUCCESS**
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.
- La funzionalità IP raw **NX_NOT_ENABLED** (0x14) non è abilitata.
- Il tipo di servizio **NX_OPTION_ERROR** (0X0A) non è valido.
- **NX_UNDERFLOW** (0x02) spazio insufficiente per anteporre un'intestazione IP al pacchetto.
- Il puntatore di aggiunta del pacchetto **NX_OVERFLOW** (0x03) non è valido.
- **NX_PTR_ERROR** (0x07) un puntatore IP o di pacchetto non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio aggiunge una voce alla tabella di routing statica. Si noti che l'indirizzo di *next_hop* deve essere direttamente accessibile da uno dei dispositivi di rete locali.

*Si noti che ip_ptr necessario puntare a una struttura IP NetX valida e che la libreria NetX deve essere compilata con NX_ENABLE_IP_STATIC_ROUTING definito per l'uso di questo servizio. Per impostazione predefinita, NetX viene compilato senza NX_ENABLE_IP_STATIC_ROUTING definito.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **Network_Address** Indirizzo di rete di destinazione, in ordine byte host
- **net_mask** Network mask di destinazione, in ordine byte host
- **next_hop** Indirizzo hop successivo per la rete di destinazione, in ordine byte host

### <a name="return-values"></a>Valori restituiti

- La voce **NX_SUCCESS** (0x00) viene aggiunta alla tabella di routing statica.
- La tabella di routing statica **NX_OVERFLOW** (0x03) è piena.
- **NX_NOT_SUPPORTED** (0X4B) questa funzionalità non è compilata in.
- L'hop successivo **NX_IP_ADDRESS_ERROR** (0x21) non è direttamente accessibile tramite interfacce locali.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_PTR_ERROR** (0x07) Ip_ptr puntatore non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Elimina route statica dalla tabella di routing

### <a name="prototype"></a>Prototipo

```C
UINT nx_ip_static_route_delete(
    NX_IP *ip_ptr,
    ULONG network_address, 
    ULONG net_mask);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina una voce dalla tabella di routing statica.

*Si noti che ip_ptr necessario puntare a una struttura IP NetX valida e che la libreria NetX deve essere compilata con NX_ENABLE_IP_STATIC_ROUTING definito per l'uso di questo servizio. Per impostazione predefinita, NetX viene compilato senza NX_ENABLE_IP_STATIC_ROUTING definito.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **Network_Address** Indirizzo di rete di destinazione, in ordine byte host.
- **net_mask** Network mask di destinazione, in ordine byte host.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio controlla ed eventualmente attende lo stato specificato dell'interfaccia di rete primaria di un'istanza IP creata in precedenza. Per ottenere lo stato sulle interfacce secondarie, le applicazioni devono utilizzare il servizio ***nx_ip_interface_status_check.***

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **needed_status** Stato IP richiesto, definito in formato mappa di bit, come indicato di seguito:
- NX_IP_INITIALIZE_DONE (0x0001)
- NX_IP_ADDRESS_RESOLVED (0x0002)
- NX_IP_LINK_ENABLED (0x0004)
- NX_IP_ARP_ENABLED (0x0008)
- NX_IP_UDP_ENABLED (0x0010)
- NX_IP_TCP_ENABLED (0x0020)
- NX_IP_IGMP_ENABLED (0x0040)
- NX_IP_RARP_COMPLETE (0x0080)
- NX_IP_INTERFACE_LINK_ENABLED (0x0100)
- **actual_status** Puntatore alla destinazione del set di bit effettivo.
- **WAIT_OPTION** Definisce il comportamento del servizio se i bit di stato richiesti non sono disponibili. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Verifica stato IP riuscito.
- La richiesta di stato **NX_NOT_SUCCESSFUL** (0x43) non è stata soddisfatta entro il timeout specificato.
- Il puntatore IP **NX_PTR_ERROR** (0x07) è o è diventato non valido oppure il puntatore di stato effettivo non è valido.
- **NX_OPTION_ERROR** (0x0A) opzione di stato necessaria non valida.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Alloca pacchetto dal pool specificato

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_allocate(
    NX_PACKET_POOL *pool_ptr,
    NX_PACKET **packet_ptr,
    ULONG packet_type,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio alloca un pacchetto dal pool specificato e regola il puntatore anteposto nel pacchetto in base al tipo di pacchetto specificato. Se non è disponibile alcun pacchetto, il servizio viene sospeso in base all'opzione wait specificata.

### <a name="parameters"></a>Parametri

- **pool_ptr** Puntatore al pool di pacchetti creato in precedenza.
- **packet_ptr** Puntatore al puntatore del puntatore del pacchetto allocato.
- **packet_type** Definisce il tipo di pacchetto richiesto. Per un elenco dei tipi di pacchetti supportati, vedere "pool di pacchetti" nella pagina 49 del capitolo 3.
- **WAIT_OPTION** Definisce il tempo di attesa in cicli se non sono disponibili pacchetti nel pool di pacchetti. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) allocare il pacchetto correttamente.
- **NX_NO_PACKET** (0x01) non è disponibile alcun pacchetto.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.
- Le dimensioni del pacchetto **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non supportano il protocollo.
- Il tipo di pacchetto **NX_OPTION_ERROR** (0X0A) non è valido.
- **NX_PTR_ERROR** (0x07) il pool o il puntatore di ritorno al pacchetto non valido.
- **NX_CALLER_ERROR** (0x11) opzione di attesa non valida da un thread non.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISRs (driver di rete dell'applicazione). L'opzione wait deve essere NX_NO_WAIT quando viene usata in ISR o nel contesto del timer.

### <a name="preemption-possible"></a>Precedenza possibile

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

Copia pacchetto

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_copy(
    NX_PACKET *packet_ptr,
    NX_PACKET **new_packet_ptr,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio Copia le informazioni del pacchetto fornito in uno o più nuovi pacchetti allocati dal pool di pacchetti fornito. In caso di esito positivo, il puntatore al nuovo pacchetto viene restituito nella destinazione a cui punta **new_packet_ptr**.

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto di origine.
- **new_packet_ptr** Puntatore alla destinazione di dove restituire il puntatore alla nuova copia del pacchetto.
- **pool_ptr** Puntatore al pool di pacchetti creato in precedenza usato per allocare uno o più pacchetti per la copia.
- **WAIT_OPTION** Definisce il modo in cui il servizio resta in attesa se non sono disponibili pacchetti. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) copia di pacchetti riuscita.
- Il pacchetto **NX_NO_PACKET** (0x01) non è disponibile per la copia.
- Il pacchetto o la copia di origine vuota **NX_INVALID_PACKET** (0x12) non è riuscito.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.
- Le dimensioni del pacchetto **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non supportano il protocollo.
- **NX_PTR_ERROR** (0x07) un pool, un pacchetto o un puntatore di destinazione non valido.
- **NX_UNDERFLOW** (0x02) puntatore a anteporre il pacchetto non valido.
- **NX_OVERFLOW** (0x03) puntatore di Accodamento pacchetti non valido.
- **NX_CALLER_ERROR** (0x11) è stata specificata un'opzione Wait nell'inizializzazione o in un ISR.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISRs

### <a name="preemption-possible"></a>Precedenza possibile

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

Accoda dati alla fine del pacchetto

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

Questo servizio aggiunge i dati alla fine del pacchetto specificato. L'area dati fornita viene copiata nel pacchetto. Se la memoria disponibile non è sufficiente e la funzionalità per i pacchetti concatenati è abilitata, per soddisfare la richiesta verranno allocati uno o più pacchetti. Se la funzionalità di pacchetto concatenato non è abilitata, viene restituito *NX_SIZE_ERROR* .

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore del pacchetto.
- **DATA_START** Puntatore all'inizio dell'area dati dell'utente da accodare al pacchetto.
- **DATA_SIZE** Dimensioni dell'area dati dell'utente.
- **pool_ptr** Puntatore al pool di pacchetti da cui allocare un altro pacchetto se non c'è spazio sufficiente nel pacchetto corrente.
- **WAIT_OPTION** Definisce il comportamento del servizio se non sono disponibili pacchetti. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Accodamento pacchetti riuscito.
- **NX_NO_PACKET** (0x01) non è disponibile alcun pacchetto.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al *tx_thread_wait_abort*.
- Le dimensioni del pacchetto **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non supportano il protocollo.
- Il puntatore **NX_UNDERFLOW** (0x02) Prepend è inferiore all'avvio del payload.
- Il puntatore di Accodamento **NX_OVERFLOW** (0x03) è maggiore della fine del payload.
- **NX_PTR_ERROR** (0x07) il pool, il pacchetto o il puntatore ai dati non valido.
- Dimensioni dei dati **NX_SIZE_ERROR** (0x09) non valide.
- **NX_CALLER_ERROR** (0x11) opzione di attesa non valida da un thread non.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISRs (driver di rete dell'applicazione)

### <a name="preemption-possible"></a>Precedenza possibile

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

Estrai i dati dal pacchetto tramite un offset

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

Questo servizio copia i dati da un pacchetto NetX (o catena di pacchetti) a partire dall'offset specificato, dal puntatore a prependi del pacchetto della dimensione specificata, in byte, nel buffer specificato. Il numero di byte effettivamente copiati viene restituito in *bytes_copied.* Questo servizio non rimuove i dati dal pacchetto, né modifica il puntatore anteposto o altre informazioni sullo stato interno.

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto da estrarre
- **offset** Offset dal puntatore a anteporre corrente.
- **buffer_start** Puntatore all'inizio del buffer di salvataggio
- **BUFFER_LENGTH** Numero di byte da copiare
- **bytes_copied** Numero di byte effettivamente copiati

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) copia di pacchetti riuscita
- È stato specificato un valore di offset non valido **NX_PACKET_OFFSET_ERROR** (0x53)
- **NX_PTR_ERROR** (0x07) puntatore a pacchetto o puntatore al buffer non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISRs

### <a name="preemption-possible"></a>Precedenza possibile

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

Recuperare dati dal pacchetto

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

- Il recupero dei dati del pacchetto **NX_SUCCESS** (0x00) riuscito.
- Il pacchetto **NX_INVALID_PACKET** (0X12) non è valido.
- **NX_PTR_ERROR** (0x07) pacchetto non valido, avvio del buffer o puntatore di byte copiato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISRs

### <a name="preemption-possible"></a>Precedenza possibile

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

Ottenere la lunghezza dei dati del pacchetto

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
- **lunghezza** Destinazione per la lunghezza del pacchetto.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISRs

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio crea un pool di pacchetti con le dimensioni del pacchetto specificate nell'area di memoria fornita dall'utente.

### <a name="parameters"></a>Parametri

- **pool_ptr** Puntatore al blocco di controllo del pool di pacchetti.
- **nome** Puntatore al nome dell'applicazione per il pool di pacchetti.
- **payload_size** Numero di byte in ogni pacchetto nel pool. Questo valore deve essere almeno di 40 byte e deve essere divisibile anche per 4.
- **memory_ptr** Puntatore all'area di memoria in cui inserire il pool di pacchetti. Il puntatore deve essere allineato su un limite ULONG.
- **memory_size** Dimensioni dell'area di memoria del pool.

### <a name="return-values"></a>Valori restituiti

- Creazione pool di pacchetti riuscita **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) il pool o il puntatore di memoria non valido.
- **NX_SIZE_ERROR** (0x09) dimensione del blocco o della memoria non valida.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Elimina pool di pacchetti creato in precedenza

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_pool_delete(NX_PACKET_POOL *pool_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un pool di pacchetti creato in precedenza. NetX verifica la presenza di eventuali thread attualmente sospesi nei pacchetti nel pool di pacchetti e cancella la sospensione.

### <a name="parameters"></a>Parametri

- **pool_ptr** Puntatore al blocco di controllo del pool di pacchetti.

### <a name="return-values"></a>Valori restituiti

- Eliminazione del pool di pacchetti riuscita **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore al pool non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio recupera le informazioni sul pool di pacchetti specificato.

*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **pool_ptr** Puntatore al pool di pacchetti creato in precedenza.
- **total_packets** Puntatore alla destinazione per il numero totale di pacchetti nel pool.
- **free_packets** Puntatore alla destinazione per il numero totale di pacchetti attualmente disponibili.
- **empty_pool_requests** Puntatore alla destinazione del numero totale di richieste di allocazione quando il pool è vuoto.
- **empty_pool_suspensions** Puntatore alla destinazione del numero totale di sospensioni del pool vuote.
- **invalid_packet_releases** Puntatore alla destinazione del numero totale di versioni di pacchetti non valide.

### <a name="return-values"></a>Valori restituiti

- Il recupero delle informazioni sul pool di pacchetti è stato completato **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread e timer

### <a name="preemption-possible"></a>Precedenza possibile

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

Versione del pacchetto allocato in precedenza

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_release(NX_PACKET *packet_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia un pacchetto, inclusi eventuali pacchetti aggiuntivi concatenati al pacchetto specificato. Se un altro thread è bloccato per l'allocazione dei pacchetti, riceve il pacchetto e lo riprende.

*L'applicazione deve impedire il rilascio di un pacchetto più di una volta, perché questa operazione provocherà risultati imprevedibili.*

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore del pacchetto.


### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) versione del pacchetto completata.
- **NX_PTR_ERROR** (0x07) puntatore al pacchetto non valido.
- Il puntatore **NX_UNDERFLOW** (0x02) Prepend è inferiore all'avvio del payload.
- Il puntatore di Accodamento **NX_OVERFLOW** (0x03) è maggiore della fine del payload.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISRs (driver di rete dell'applicazione)

### <a name="preemption-possible"></a>Precedenza possibile

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

Rilascia un pacchetto trasmesso

### <a name="prototype"></a>Prototipo

```C
UINT nx_packet_transmit_release(NX_PACKET *packet_ptr);
```

### <a name="description"></a>Descrizione

Per i pacchetti non TCP, questo servizio rilascia un pacchetto trasmesso, inclusi eventuali pacchetti aggiuntivi concatenati al pacchetto specificato. Se un altro thread è bloccato per l'allocazione dei pacchetti, riceve il pacchetto e lo riprende. Per un pacchetto TCP trasmesso, il pacchetto è contrassegnato come trasmesso ma non rilasciato finché il pacchetto non viene riconosciuto. Questo servizio viene in genere chiamato dal driver di rete dell'applicazione dopo la trasmissione di un pacchetto.

*Il driver di rete deve rimuovere l'intestazione supporto fisico e regolare la lunghezza del pacchetto prima di chiamare il servizio.*

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore del pacchetto.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha completato la trasmissione del pacchetto.
- **NX_PTR_ERROR** (0x07) puntatore al pacchetto non valido.
- Il puntatore **NX_UNDERFLOW** (0x02) Prepend è inferiore all'avvio del payload.
- Il puntatore di Accodamento **NX_OVERFLOW** (0x03) è maggiore della fine del payload.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, driver di rete dell'applicazione (incluso ISRs)

### <a name="preemption-possible"></a>Precedenza possibile

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

Disabilitare il protocollo RARP (inverse Address Resolution Protocol)

### <a name="prototype"></a>Prototipo

```C
UINT nx_rarp_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Disabilita il componente RARP di NetX per l'istanza IP specifica. Per un sistema multihome, questo servizio Disabilita RARP su tutte le interfacce.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) DISABILITAto RARP con esito positivo.
- **NX_NOT_ENABLED** (0X14) RARP non è stato abilitato.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Abilita il protocollo RARP (Reverse Address Resolution Protocol)

### <a name="prototype"></a>Prototipo

```C
UINT nx_rarp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita il componente RARP di NetX per l'istanza IP specifica. Il componente RARP esegue la ricerca in tutte le interfacce di rete collegate per un indirizzo IP zero. Un indirizzo IP zero indica che l'interfaccia non è ancora stata assegnata all'indirizzo IP. RARP tenta di risolvere l'indirizzo IP abilitando il processo RARP su tale interfaccia.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- Abilitazione di **NX_SUCCESS** (0x00) RARP riuscita.
- L'indirizzo IP **NX_IP_ADDRESS_ERROR** (0x21) è già valido.
- **NX_ALREADY_ENABLED** (0X15) RARP è già abilitato.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Precedenza possibile

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

*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **rarp_requests_sent** Puntatore alla destinazione per il numero totale di richieste RARP inviate.
- **rarp_responses_received** Puntatore alla destinazione per il numero totale di risposte RARP ricevute.
- **rarp_invalid_messages** Puntatore alla destinazione del numero totale di messaggi non validi.


### <a name="return-values"></a>Valori restituiti
- Il recupero delle informazioni RARP riuscito **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio Inizializza le risorse di sistema NetX di base in preparazione per l'uso. Deve essere chiamata dall'applicazione durante l'inizializzazione e prima che venga eseguita qualsiasi altra chiamata a NetX.

### <a name="parameters"></a>Parametri

nessuno

### <a name="return-values"></a>Valori restituiti

nessuno

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISRs

### <a name="preemption-possible"></a>Precedenza possibile

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

Associa socket TCP client a porta TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_client_socket_bind(
    NX_TCP_SOCKET *socket_ptr,
    UINT port, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio associa il socket client TCP creato in precedenza alla porta TCP specificata. I socket TCP validi sono compresi tra 0 e 0xFFFF. Se la porta TCP specificata non è disponibile, il servizio viene sospeso in base all'opzione di attesa fornita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.
- **porta** Numero di porta da associare (da 1 a 0xFFFF). Se il numero di porta è NX_ANY_PORT (0x0000), l'istanza IP cercherà la porta libera successiva e la utilizzerà per l'associazione.
- **WAIT_OPTION** Definisce il comportamento del servizio se la porta è già associata a un altro socket. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) associazione Socket riuscita.
- **NX_ALREADY_BOUND** (0X22) questo socket è già associato a un'altra porta TCP.
- La porta **NX_PORT_UNAVAILABLE** (0x23) è già associata a un socket diverso.
- **NX_NO_FREE_PORTS** (0X45) non è disponibile alcuna porta.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al *tx_thread_wait_abort*.
- La porta **NX_INVALID_PORT** (0x46) non è valida.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Connetti socket TCP client

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_client_socket_connect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG server_ip,
    UINT server_port,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio connette il socket client TCP creato in precedenza e associato alla porta del server specificato. Le porte del server TCP valide sono comprese tra 0 e 0xFFFF. Se la connessione non viene completata immediatamente, il servizio viene sospeso in base all'opzione wait specificata.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.
- **server_ip** Indirizzo IP del server.
- **SERVER_PORT** Numero di porta del server a cui connettersi (da 1 a 0xFFFF).
- **WAIT_OPTION** Definisce il comportamento del servizio mentre viene stabilita la connessione. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) connessione socket riuscita.
- Il socket **NX_NOT_BOUND** (0x24) non è associato.
- Il socket **NX_NOT_CLOSED** (0x35) non è in uno stato chiuso.
- **NX_IN_PROGRESS** (0x37) non è stata specificata alcuna attesa. il tentativo di connessione è in corso.
- Non è stata specificata l'interfaccia **NX_INVALID_INTERFACE** (0x4C).
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP del server non valido.
- La porta **NX_INVALID_PORT** (0x46) non è valida.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio recupera il numero di porta associato al socket, che è utile per trovare la porta allocata da NetX nelle situazioni in cui è stato specificato il NX_ANY_PORT nel momento in cui il socket è stato associato.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.
- **port_ptr** Puntatore alla destinazione per il numero di porta restituito. I numeri di porta validi sono compresi tra 1 e 0xFFFF.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) associazione Socket riuscita.
- **NX_NOT_BOUND** (0X24) questo socket non è associato a una porta.
- **NX_PTR_ERROR** (0x07) puntatore a socket non valido o puntatore a porta restituita.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Annulla Binding socket client TCP dalla porta TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_client_socket_unbind(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rilascia l'associazione tra il socket client TCP e una porta TCP. Se sono presenti altri thread in attesa di associare un altro socket allo stesso numero di porta, il primo thread sospeso viene quindi associato a questa porta.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- La disassociazione del socket è riuscita **NX_SUCCESS** (0x00).
- Il socket **NX_NOT_BOUND** (0x24) non è stato associato ad alcuna porta.
- Il socket **NX_NOT_CLOSED** (0x35) non è stato disconnesso.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio Abilita il componente Transmission Control Protocol (TCP) di NetX. Dopo l'abilitazione, le connessioni TCP possono essere stabilite dall'applicazione.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) abilitato per TCP.
- **NX_ALREADY_ENABLED** (0X15) TCP è già abilitato.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Precedenza possibile

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

Trova la porta TCP successiva disponibile

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_free_port_find(
    NX_IP *ip_ptr,
    UINT port, UINT *free_port_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio tenta di individuare una porta TCP gratuita (senza binding) a partire dalla porta fornita dall'applicazione. La logica di ricerca eseguirà il wrapping se la ricerca viene eseguita per raggiungere il valore di porta massimo di 0xFFFF. Se la ricerca ha esito positivo, la porta libera viene restituita nella variabile a cui punta *free_port_ptr*.

*Questo servizio può essere chiamato da un altro thread e deve essere restituita la stessa porta. Per evitare questo race condition, è possibile che l'applicazione inserisca il servizio e che il socket client effettivo venga associato sotto la protezione di un mutex.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **porta** Numero di porta da cui iniziare la ricerca (da 1 a 0xFFFF).
- **free_port_ptr** Puntatore al valore restituito della porta libera di destinazione.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) riuscite dalla porta libera.
- **NX_NO_FREE_PORTS** (0X45) non sono state trovate porte gratuite.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.
- **NX_INVALID_PORT** (0x46) il numero di porta specificato non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
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

- Il recupero delle informazioni TCP riuscite **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Accetta connessione TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_server_socket_accept(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio accetta o prepara l'accettazione di una richiesta di connessione socket client TCP per una porta precedentemente configurata per l'ascolto. Questo servizio può essere chiamato immediatamente dopo che l'applicazione chiama il servizio di ascolto o di riascolto oppure dopo che la routine di callback di ascolto viene chiamata quando la connessione client è effettivamente presente. Se non è possibile stabilire una connessione immediatamente, il servizio viene sospeso in base all'opzione wait specificata.

*L'applicazione deve chiamare **nx_tcp_server_socket_unaccept** dopo che la connessione non è più necessaria per rimuovere l'associazione del socket server alla porta del server.*

*Le routine di callback dell'applicazione vengono chiamate dall'interno del thread helper dell'IP.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al blocco di controllo socket del server TCP.
- **WAIT_OPTION** Definisce il comportamento del servizio mentre viene stabilita la connessione. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)


### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) accettazione socket server TCP riuscita (connessione passiva).
- **NX_NOT_LISTEN_STATE** (0X36) il socket del server specificato non è in uno stato di attesa.
- **NX_IN_PROGRESS** (0x37) non è stata specificata alcuna attesa. il tentativo di connessione è in corso.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al *tx_thread_wait_abort*.
- Errore del puntatore del socket **NX_PTR_ERROR** (0x07).
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Abilita l'ascolto della connessione client sulla porta TCP

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

Questo servizio consente l'attesa di una richiesta di connessione client sulla porta TCP specificata. Quando viene ricevuta una richiesta di connessione client, il socket del server fornito viene associato alla porta specificata e viene chiamata la funzione di callback di ascolto fornita.

L'elaborazione della routine di callback di ascolto è stata completata fino all'applicazione. Può contenere la logica per riattivare un thread dell'applicazione che esegue successivamente un'operazione Accept. Se l'applicazione dispone già di un thread sospeso durante l'accettazione dell'elaborazione per questo socket, la routine di callback di ascolto potrebbe non essere necessaria.

Se l'applicazione desidera gestire connessioni client aggiuntive sulla stessa porta, il ***nx_tcp_server_socket_relisten*** deve essere chiamato con un socket disponibile (un socket nello stato Closed) per la connessione successiva. Fino a quando non viene chiamato il servizio di riascolto, le connessioni client aggiuntive vengono accodate. Quando viene superata la profondità massima della coda, la richiesta di connessione meno recente viene eliminata a favore dell'accodamento della nuova richiesta di connessione. La profondità massima della coda è specificata da questo servizio.

*Le routine di callback dell'applicazione vengono chiamate dal thread di supporto IP interno.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **porta** Numero di porta su cui restare in ascolto (da 1 a 0xFFFF).
- **socket_ptr** Puntatore al socket da utilizzare per la connessione.
- **listen_queue_size** Numero di richieste di connessione client che possono essere accodate.
- **Listen_Callback** Funzione dell'applicazione da chiamare quando viene ricevuta la connessione. Se viene specificato un valore NULL, la funzionalità di callback di ascolto è disabilitata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) la porta TCP abilitata per l'ascolto è riuscita.
- **NX_MAX_LISTEN** (0X33) non sono disponibili altre strutture di richiesta di ascolto. La costante NX_MAX_LISTEN_REQUESTS in nx_api. h definisce il numero di richieste di ascolto attive possibili.
- **NX_NOT_CLOSED** (0x35) il socket server specificato non si trova in uno stato chiuso.
- **NX_ALREADY_BOUND** (0X22) il socket del server specificato è già associato a una porta.
- **NX_DUPLICATE_LISTEN** (0x34) è già presente una richiesta di ascolto attiva per questa porta.
- La porta **NX_INVALID_PORT** (0x46) specificata non è valida.
- **NX_PTR_ERROR** (0x07) un puntatore IP o socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Re-ascolto della connessione client sulla porta TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_server_socket_relisten(
    NX_IP *ip_ptr, 
    UINT port,
    NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio viene chiamato dopo la ricezione di una connessione su una porta che è stata impostata in precedenza per l'ascolto. Lo scopo principale di questo servizio è fornire un nuovo socket server per la successiva connessione client. Se una richiesta di connessione viene accodata, la connessione verrà elaborata immediatamente durante la chiamata al servizio.

*La stessa routine di callback specificata dalla richiesta di ascolto originale viene chiamata anche quando è presente una connessione per questo nuovo socket del server.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **porta** Numero di porta su cui eseguire di nuovo l'ascolto (da 1 a 0xFFFF).
- **socket_ptr** Socket da utilizzare per la connessione client successiva.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) la porta TCP riascoltata è riuscita.
- **NX_NOT_CLOSED** (0x35) il socket server specificato non si trova in uno stato chiuso.
- **NX_ALREADY_BOUND** (0X22) il socket del server specificato è già associato a una porta.
- **NX_INVALID_RELISTEN** (0x47) è già presente un puntatore socket valido per questa porta oppure la porta specificata non ha una richiesta di ascolto attiva.
- **NX_CONNECTION_PENDING** (0X48) uguale NX_SUCCESS, ad eccezione del fatto che è stata eseguita una richiesta di connessione in coda ed è stata elaborata durante questa chiamata.
- La porta **NX_INVALID_PORT** (0x46) specificata non è valida.
- **NX_PTR_ERROR** (0x07) un IP non valido o un puntatore di callback di ascolto.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Rimuovi associazione socket con porta di ascolto

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_server_socket_unaccept(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rimuove l'associazione tra questo socket server e la porta del server specificata. L'applicazione deve chiamare questo servizio dopo una disconnessione o dopo una chiamata Accept non riuscita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket del server di installazione precedente.

### <a name="return-values"></a>Valori restituiti

- Impossibile accettare il socket server riuscito **NX_SUCCESS** (0x00).
- Il socket del server **NX_NOT_LISTEN_STATE** (0x36) si trova in uno stato non valido e probabilmente non è disconnesso.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio Disabilita l'attesa di una richiesta di connessione client sulla porta TCP specificata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **porta** Numero di porta da disabilitare in ascolto (da 0 a 0xFFFF).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) la disabilitazione dell'ascolto TCP è riuscita.
- L'attesa **NX_ENTRY_NOT_FOUND** (0x16) non è stata abilitata per la porta specificata.
- La porta **NX_INVALID_PORT** (0x46) specificata non è valida.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

- **socket_ptr** Puntatore al socket TCP precedentemente creato e connesso.
- **bytes_available** Puntatore alla destinazione per byte disponibili.

### <a name="return-values"></a>Valori restituiti

- Il servizio **NX_SUCCESS** (0x00) viene eseguito correttamente. Il numero di byte disponibili per la lettura viene restituito al chiamante.
- Il socket **NX_NOT_CONNECTED** (0x38) non si trova in uno stato connesso.
- **NX_PTR_ERROR** (0x07) puntatori non validi.
- **NX_NOT_ENABLED** TCP (0x14) non è abilitato.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Creazione di un client TCP o di un server socket

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

Questo servizio crea un client TCP o un socket server per l'istanza IP specificata.

*Le routine di callback dell'applicazione vengono chiamate dal thread associato a questa istanza IP.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **socket_ptr** Puntatore al nuovo blocco di controllo socket TCP.
- **nome** Nome dell'applicazione per questo socket TCP.
- **Type_of_Service** Definisce il tipo di servizio per la trasmissione. i valori validi sono i seguenti:

- NX_IP_NORMAL (0x00000000)
- NX_IP_MIN_DELAY (0x00100000)
- NX_IP_MAX_DATA (0x00080000)
- NX_IP_MAX_RELIABLE (0x00040000)
- NX_IP_MIN_COST (0x00020000)

- **frammento**  Specifica se la frammentazione IP è consentita o meno. Se viene specificato NX_FRAGMENT_OKAY (0x0), è consentita la frammentazione IP. Se viene specificato NX_DONT_FRAGMENT (0x4000), la frammentazione IP è disabilitata.
- **Time_to_live** Specifica il valore a 8 bit che definisce il numero di router che questo pacchetto può superare prima di essere eliminato. Il valore predefinito è specificato dal NX_IP_TIME_TO_LIVE.
- **window_size** Definisce il numero massimo di byte consentiti nella coda di ricezione per questo socket
- **urgent_data_callback** Funzione dell'applicazione che viene chiamata ogni volta che vengono rilevati dati urgenti nel flusso di ricezione. Se questo valore è NX_NULL, i dati urgenti vengono ignorati.
- **disconnect_callback** Funzione dell'applicazione che viene chiamata ogni volta che una disconnessione viene emessa dal socket all'altra estremità della connessione. Se questo valore è NX_NULL, la funzione di callback di disconnessione è disabilitata.

### <a name="return-values"></a>Valori restituiti
- Creazione socket client TCP riuscita **NX_SUCCESS** (0x00).
- **NX_OPTION_ERROR** (0x0A) tipo di servizio non valido, frammento, dimensioni della finestra non valide o opzione Time-tolive.
- **NX_PTR_ERROR** (0x07) un puntatore IP o socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Elimina socket TCP

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_delete(NX_TCP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un socket TCP creato in precedenza. Se il socket è ancora associato o connesso, il servizio restituisce un codice di errore.

### <a name="parameters"></a>Parametri

- **socket_ptr** Socket TCP creato in precedenza

### <a name="return-values"></a>Valori restituiti

- Eliminazione del socket riuscita **NX_SUCCESS** (0x00).
- Il socket **NX_NOT_CREATED** (0x27) non è stato creato.
- Il socket **NX_STILL_BOUND** (0x42) è ancora associato.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio disconnette una connessione client o socket server stabilita. Una disconnessione di un socket del server deve essere seguita da una richiesta di non accettazione, mentre un socket client disconnesso viene lasciato in uno stato pronto per un'altra richiesta di connessione. Se non è possibile completare immediatamente il processo di disconnessione, il servizio viene sospeso in base all'opzione wait specificata.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del client o del socket del server connessa in precedenza.
- **WAIT_OPTION** Definisce il comportamento del servizio mentre è in corso la disconnessione. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- Disconnessione socket riuscite **NX_SUCCESS** (0x00).
- Il socket specificato **NX_NOT_CONNECTED** (0x38) non è connesso.
- È in corso la disconnessione **NX_IN_PROGRESS** (0x37). non è stata specificata alcuna attesa.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Installazione della funzione di callback di disconnessione TCP completata

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_disconnect_complete_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_disconnect_complete_notify)
    (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback che viene richiamata dopo il completamento di un'operazione di disconnessione del socket. La funzione di callback di disconnessione socket TCP è disponibile se NetX è compilato con l'opzione

- ***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** definito.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del client o del socket del server connessa in precedenza.
- **tcp_disconnect_complete_notify** Funzione di callback da installare.

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) ha registrato correttamente la funzione di callback.
- **NX_NOT_SUPPORTED** (0X4B) la funzionalità di notifica estesa non è incorporata nella libreria NETX
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- La funzionalità TCP **NX_NOT_ENABLED** (0x14) non è abilitata.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Impostare la funzione TCP establishe Notify callback

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_establish_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_establish_notify)(NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback, che viene chiamata dopo che un socket TCP crea una connessione. Il socket TCP stabilisce la funzione di callback è disponibile se NetX viene compilato con l'opzione ***NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** definita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del client o del socket del server connessa in precedenza.
- **tcp_establish_notify** Funzione di callback richiamata dopo che è stata stabilita una connessione TCP.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) imposta correttamente la funzione Notify.
- **NX_NOT_SUPPORTED** (0X4B) la funzionalità di notifica estesa non è incorporata nella libreria NETX
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) TCP non è stato abilitato dall'applicazione.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Recuperare informazioni sulle attività dei socket TCP

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

Questo servizio recupera informazioni sulle attività socket TCP per l'istanza di socket TCP specificata.

*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.
- **tcp_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti TCP inviati al socket.
- **tcp_bytes_sent** Puntatore alla destinazione per il numero totale di byte TCP inviati al socket.
- **tcp_packets_received** Puntatore alla destinazione del numero totale di pacchetti TCP ricevuti sul socket.
- **tcp_bytes_received** Puntatore alla destinazione del numero totale di byte TCP ricevuti sul socket.
- **tcp_retransmit_packets** Puntatore alla destinazione del numero totale di ritrasmissioni di pacchetti TCP.
- **tcp_packets_queued** Puntatore alla destinazione del numero totale di pacchetti TCP in coda nel socket.
- **tcp_checksum_errors** Puntatore alla destinazione del numero totale di pacchetti TCP con errori di checksum nel socket.
- **tcp_socket_state** Puntatore alla destinazione dello stato corrente del socket.
- **tcp_transmit_queue_depth** Puntatore alla destinazione del numero totale di pacchetti di trasmissione ancora in coda in attesa di ACK.
- **tcp_transmit_window** Puntatore alla destinazione della dimensione della finestra di trasmissione corrente.
- **tcp_receive_window** Puntatore alla destinazione delle dimensioni correnti della finestra di ricezione.

### <a name="return-values"></a>Valori restituiti

- Il recupero delle informazioni sul socket TCP riuscite **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

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

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Ottenere la MSS del socket

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_mss_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
```

### <a name="description"></a>Descrizione

Questo servizio recupera la dimensione del segmento massimo locale (MSS) del socket specificato.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket creato in precedenza.
- **MSS** Destinazione per la restituzione di MSS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) riuscite MSS Get.
- **NX_PTR_ERROR** (0x07) o un puntatore di destinazione MSS non valido.
- **NX_NOT_ENABLED** TCP (0x14) non è abilitato.
- Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Ottenere la MSS del socket TCP peer

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_mss_peer_get(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG *mss);
```

### <a name="description"></a>Descrizione

Questo servizio recupera le dimensioni massime del segmento (MSS) annunciate dal socket peer.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket precedentemente creato e connesso.
- **MSS** Destinazione per la restituzione dell'oggetto MSS.


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) il peer MSS riuscito Get.
- **NX_PTR_ERROR** (0x07) o un puntatore di destinazione MSS non valido.
- **NX_NOT_ENABLED** TCP (0x14) non è abilitato.
- Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Imposta MSS del socket

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_mss_set(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG mss);
```

### <a name="description"></a>Descrizione

Questo servizio imposta la dimensione massima del segmento (MSS) del socket specificato. Si noti che il valore MSS deve rientrare nell'IP dell'interfaccia di rete MTU, consentendo spazio per le intestazioni IP e TCP.

Questo servizio deve essere utilizzato prima che un socket TCP avvii il processo di connessione. Se il servizio viene utilizzato dopo che è stata stabilita una connessione TCP, il nuovo valore non ha alcun effetto sulla connessione.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket creato in precedenza.
- **MSS** Valore di MSS da impostare.

### <a name="return-values"></a>Valori restituiti

- Set di MSS riusciti **NX_SUCCESS** (0x00).
- Il valore MSS specificato per **NX_SIZE_ERROR** (0x09) è troppo grande.
- Non è stata stabilita la connessione TCP **NX_NOT_CONNECTED** (0x38)
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- **NX_NOT_ENABLED** TCP (0x14) non è abilitato.
- Il chiamante **NX_CALLER_ERROR** (0x11) non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio recupera le informazioni sull'indirizzo IP e sulla porta del peer per il socket TCP connesso sulla rete IP.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP creato in precedenza.
- **peer_ip_address** Puntatore alla destinazione per l'indirizzo IP del peer nell'ordine dei byte dell'host.
- **peer_port** Puntatore alla destinazione per il numero di porta peer nell'ordine dei byte dell'host.

### <a name="return-values"></a>Valori restituiti

- Il servizio **NX_SUCCESS** (0x00) viene eseguito correttamente. Il numero di porta e l'indirizzo IP del peer vengono restituiti al chiamante.
- Il socket **NX_NOT_CONNECTED** (0x38) non si trova in uno stato connesso.
- **NX_PTR_ERROR** (0x07) puntatori non validi.
- **NX_NOT_ENABLED** TCP (0x14) non è abilitato.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio riceve i dati TCP dal socket specificato. Se non viene accodato alcun dato nel socket specificato, il chiamante viene sospeso in base all'opzione wait fornita.

*Se viene restituito NX_SUCCESS, l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza di socket TCP creata in precedenza.
- **packet_ptr** Puntatore al puntatore del pacchetto TCP.
- **WAIT_OPTION** Definisce il comportamento del servizio se nessun dato è attualmente accodato in questo socket. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti
- **NX_SUCCESS** (0x00) la ricezione dei dati socket è riuscita.
- Il socket **NX_NOT_BOUND** (0x24) non è ancora associato.
- **NX_NO_PACKET** (0x01) non sono stati ricevuti dati.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.
- **NX_NOT_CONNECTED** (0X38) il socket non è più connesso.
- **NX_PTR_ERROR** (0x07) socket non valido o puntatore al pacchetto restituito.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

No

### <a name="example"></a>Esempio

/* Ricevere un pacchetto dal socket client TCP creato e connesso in precedenza. Se non è disponibile alcun pacchetto, attendere i cicli di 200 timer prima di rinunciare. */status = nx_tcp_socket_receive (&client_socket, &packet_ptr, 200);

/* Se lo stato è NX_SUCCESS, il pacchetto ricevuto fa riferimento a "packet_ptr". */

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

Questo servizio configura il puntatore della funzione receive Notify con la funzione di callback specificata dall'applicazione. Questa funzione di callback viene quindi chiamata ogni volta che vengono ricevuti uno o più pacchetti nel socket. Se viene fornito un puntatore NX_NULL, la funzione Notify è disabilitata.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP.
- **tcp_receive_notify** Puntatore alla funzione di callback dell'applicazione che viene chiamato quando uno o più pacchetti vengono ricevuti sul socket.

### <a name="return-values"></a>Valori restituiti

- La notifica di ricezione del socket riuscite **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- La funzionalità TCP **NX_NOT_ENABLED** (0x14) non è abilitata.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio invia dati TCP tramite un socket TCP connesso in precedenza. Se le ultime dimensioni della finestra annunciata del ricevitore sono inferiori a questa richiesta, il servizio viene sospeso facoltativamente in base all'opzione wait specificata. Questo servizio garantisce che non vengano inviati dati di pacchetto di dimensioni superiori a MSS al livello IP.

*A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché il driver di rete tenterà anche di rilasciare il pacchetto dopo la trasmissione.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza di socket TCP connessa in precedenza.
- **packet_ptr** Puntatore al pacchetto di dati TCP.
- **WAIT_OPTION** Definisce il comportamento del servizio se la richiesta è maggiore delle dimensioni della finestra del destinatario. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) del socket inviato correttamente.
- Il socket **NX_NOT_BOUND** (0x24) non è stato associato ad alcuna porta.
- **NX_NO_INTERFACE_ADDRESS** (0X50) non è stata trovata alcuna interfaccia in uscita adatta.
- Il socket **NX_NOT_CONNECTED** (0x38) non è più connesso.
- La richiesta **NX_WINDOW_OVERFLOW** (0x39) è maggiore della dimensione della finestra annunciata del ricevitore in byte.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.
- Il pacchetto **NX_INVALID_PACKET** (0x12) non è allocato.
- È stata raggiunta la profondità massima della coda di trasmissione **NX_TX_QUEUE_DEPTH** (0x49).
- Il puntatore di aggiunta del pacchetto **NX_OVERFLOW** (0x03) non è valido.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.
- Il puntatore **NX_UNDERFLOW** (0x02) non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio attende che il socket entri nello stato desiderato. Se il socket non è nello stato desiderato, il servizio viene sospeso in base all'opzione wait specificata.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza di socket TCP connessa in precedenza.
- **desired_state** Stato TCP desiderato. Gli Stati di socket TCP validi sono definiti come segue:
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
- **WAIT_OPTION** Definisce il comportamento del servizio se lo stato richiesto non è presente. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti
- Attesa stato riuscita **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Lo stato **NX_NOT_SUCCESSFUL** (0x43) non è presente entro il tempo di attesa specificato.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.
- **NX_OPTION_ERROR** (0X0A) lo stato del socket desiderato non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Installa callback per lo stato di attesa programmato

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_timed_wait_callback(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_timed_wait_callback) (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback che viene richiamata quando il socket TCP è in stato di attesa programmato. Per utilizzare questo servizio, è necessario compilare la libreria NetX con l'opzione ***NX_ENABLE_EXTENDED_NOTIFY*** definita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del client o del socket del server connessa in precedenza.
- **tcp_timed_wait_callback** Funzione di callback Wait temporizzata

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) registra correttamente il socket della funzione di callback
- La libreria NetX **NX_NOT_SUPPORTED** (0x4B) viene compilata senza la funzionalità di notifica estesa abilitata.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- La funzionalità TCP **NX_NOT_ENABLED** (0x14) non è abilitata.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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
- **timeout** Numero di cicli del timer ThreadX in attesa di un ACK prima che il pacchetto venga nuovamente inviato.
- **max_retries** Numero massimo di tentativi consentiti.
- **timeout_shift** Valore per spostare il timeout per ogni nuovo tentativo successivo. Il valore 0 comporta lo stesso timeout tra i tentativi successivi. Il valore 1, raddoppia il timeout tra i tentativi.

### <a name="return-values"></a>Valori restituiti
- Configurazione socket di trasmissione riuscita **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Opzione profondità coda non valida **NX_OPTION_ERROR** (0x0A).
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- La funzionalità TCP **NX_NOT_ENABLED** (0x14) non è abilitata.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Notifica dell'applicazione degli aggiornamenti delle dimensioni della finestra

### <a name="prototype"></a>Prototipo

```C
UINT nx_tcp_socket_window_update_notify_set(
    NX_TCP_SOCKET
    *socket_ptr,
    VOID (*tcp_window_update_notify)
    (NX_TCP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio installa una routine di callback di aggiornamento della finestra del socket. Questa routine viene chiamata automaticamente ogni volta che il socket specificato riceve un pacchetto che indica un aumento delle dimensioni della finestra dell'host remoto.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP creato in precedenza.
- **tcp_window_update_notify** Routine di callback da chiamare quando cambiano le dimensioni della finestra. Il valore NULL disabilita l'aggiornamento delle modifiche della finestra.

### <a name="return-values"></a>Valori restituiti
- Nel socket è installata la routine di callback **NX_SUCCESS** (0x00).
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_PTR_ERROR** (0x07) puntatori non validi.
- La funzionalità TCP **NX_NOT_ENABLED** (0x14) non è abilitata.


### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Abilita componente UDP di NetX

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_enable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita il componente UDP (User Datagram Protocol) di NetX. Dopo l'abilitazione, i datagrammi UDP possono essere inviati e ricevuti dall'applicazione.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Enable UDP riuscito.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_ALREADY_ENABLED** (0X15) questo componente è già stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Precedenza possibile

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

Trova la porta UDP successiva disponibile

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_free_port_find(
    NX_IP *ip_ptr, 
    UINT port,
    UINT *free_port_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio cerca una porta UDP gratuita (senza binding) a partire dal numero di porta fornito dall'applicazione. Se la ricerca raggiunge il valore massimo della porta di 0xFFFF, viene eseguito il wrapping della logica di ricerca. Se la ricerca ha esito positivo, la porta libera viene restituita nella variabile a cui punta *free_port_ptr*.

*Questo servizio può essere chiamato da un altro thread e può avere la stessa porta restituita. Per evitare questo race condition, è possibile che l'applicazione inserisca il servizio e il socket effettivo associato alla protezione di un mutex.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **porta** Numero di porta da cui iniziare la ricerca (da 1 a 0xFFFF).
- **free_port_ptr** Puntatore alla variabile di restituzione della porta libera di destinazione.


### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) riuscite dalla porta libera.
- **NX_NO_FREE_PORTS** (0X45) non sono state trovate porte gratuite.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.
- Il numero di porta specificato **NX_INVALID_PORT** (0x46) non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **udp_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti UDP inviati.
- **udp_bytes_sent** Puntatore alla destinazione per il numero totale di byte UDP inviati.
- **udp_packets_received** Puntatore alla destinazione del numero totale di pacchetti UDP ricevuti.
- **udp_bytes_received** Puntatore alla destinazione del numero totale di byte UDP ricevuti.
- **udp_invalid_packets** Puntatore alla destinazione del numero totale di pacchetti UDP non validi.
- **udp_receive_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di ricezione UDP eliminati.
- **udp_checksum_errors** Puntatore alla destinazione del numero totale di pacchetti UDP con errori di checksum.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) il recupero delle informazioni UDP è riuscito.
- **NX_PTR_ERROR** (0x07) puntatore IP non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.


### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread e timer

### <a name="preemption-possible"></a>Precedenza possibile

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

Estrai parametri di rete dal pacchetto UDP

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
- **protocollo** di Puntatore a protocollo (UDP).
- **porta** Puntatore al numero di porta del mittente.
- **interface_index** Puntatore all'indice dell'interfaccia ricevente.

### <a name="return-values"></a>Valori restituiti

- Estrazione dei dati dell'interfaccia di pacchetti **NX_SUCCESS** (0x00) completata.
- Il pacchetto **NX_INVALID_PACKET** (0x12) non contiene un frame IP.
- **NX_PTR_ERROR** (0x07) input puntatore non valido
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Associa socket UDP a porta UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_bind(
    NX_UDP_SOCKET *socket_ptr, 
    UINT port,
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio associa il socket UDP creato in precedenza alla porta UDP specificata. I socket UDP validi sono compresi tra 0 e 0xFFFF. Se il numero di porta richiesto è associato a un altro socket, il servizio attende il periodo di tempo specificato affinché il socket venga dissociato dal numero di porta.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.
- **porta** Numero di porta da associare (da 1 a 0xFFFF). Se il numero di porta è NX_ANY_PORT (0x0000), l'istanza IP cercherà la porta libera successiva e la utilizzerà per l'associazione.
- **WAIT_OPTION** Definisce il comportamento del servizio se la porta è già associata a un altro socket. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) associazione Socket riuscita.
- **NX_ALREADY_BOUND** (0X22) questo socket è già associato a un'altra porta.
- La porta **NX_PORT_UNAVAILABLE** (0x23) è già associata a un socket diverso.
- **NX_NO_FREE_PORTS** (0X45) non è disponibile alcuna porta.
- La sospensione richiesta **NX_WAIT_ABORTED** (0x1A) è stata interrotta da una chiamata al tx_thread_wait_abort.
- La porta **NX_INVALID_PORT** (0x46) specificata non è valida.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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
- **bytes_available** Puntatore alla destinazione per byte disponibili.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) byte riusciti di recupero disponibili.
- Il socket **NX_NOT_SUCCESSFUL** (0x43) non è associato a una porta.
- **NX_PTR_ERROR** (0x07) puntatori non validi.
- La funzionalità UDP **NX_NOT_ENABLED** (0x14) non è abilitata.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio Disabilita la logica di checksum per l'invio e la ricezione di pacchetti sul socket UDP specificato. Quando la logica di checksum è disabilitata, il valore zero viene caricato nel campo checksum dell'intestazione UDP per tutti i pacchetti inviati tramite questo socket. Un valore di checksum con valore zero nell'intestazione UDP segnala al ricevitore che checksum non viene calcolato per questo pacchetto.

Si noti inoltre che questa operazione non ha effetto se vengono definiti ***NX_DISABLE_UDP_RX_CHECKSUM** _ e _ *_NX_DISABLE_UDP_TX_CHECKSUM_** durante la ricezione e l'invio di pacchetti UDP rispettivamente.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) disabilitato checksum del socket riuscito.
- Il socket **NX_NOT_BOUND** (0x24) non è associato.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Precedenza possibile

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

Abilita checksum per socket UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_checksum_enable(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Abilita la logica di checksum per l'invio e la ricezione di pacchetti sul socket UDP specificato. Il checksum copre l'intera area dati UDP e un'intestazione pseudo-IP.

Si noti inoltre che questa operazione non ha effetto se vengono definiti **NX_DISABLE_UDP_RX_CHECKSUM** e **NX_DISABLE_UDP_TX_CHECKSUM** durante la ricezione e l'invio di pacchetti UDP rispettivamente.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- Abilitazione del checksum del socket **NX_SUCCESS** (0x00) riuscita.
- Il socket **NX_NOT_BOUND** (0x24) non è associato.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Precedenza possibile

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

Crea socket UDP.

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

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.
- **socket_ptr** Puntatore al nuovo blocco di controllo socket UDP.
- **nome** Nome dell'applicazione per questo socket UDP.
- **Type_of_Service** Definisce il tipo di servizio per la trasmissione. i valori validi sono i seguenti:
    - NX_IP_NORMAL (0x00000000)
    - NX_IP_MIN_DELAY (0x00100000)
    - NX_IP_MAX_DATA (0x00080000)
    - NX_IP_MAX_RELIABLE (0x00040000)
    - NX_IP_MIN_COST (0x00020000)
- **frammento** Specifica se la frammentazione IP è consentita o meno. Se viene specificato NX_FRAGMENT_OKAY (0x0), è consentita la frammentazione IP. Se viene specificato NX_DONT_FRAGMENT (0x4000), la frammentazione IP è disabilitata.
- **Time_to_live** Specifica il valore a 8 bit che definisce il numero di router che questo pacchetto può superare prima di essere eliminato. Il valore predefinito è specificato dal NX_IP_TIME_TO_LIVE.
- **queue_maximum** Definisce il numero massimo di datagrammi UDP che possono essere accodati per il socket. Una volta raggiunto il limite della coda, per ogni nuovo pacchetto ricevuto viene rilasciato il pacchetto UDP meno recente.

### <a name="return-values"></a>Valori restituiti

- Creazione socket UDP riuscita **NX_SUCCESS** (0x00).
- **NX_OPTION_ERROR** (0x0A) tipo di servizio, frammento o opzione di durata (TTL) non valida.
- **NX_PTR_ERROR** (0x07) un puntatore IP o socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Elimina socket UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_delete(NX_UDP_SOCKET *socket_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Elimina un socket UDP creato in precedenza. Se il socket è stato associato a una porta, il socket deve essere prima non associato.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- Eliminazione del socket riuscita **NX_SUCCESS** (0x00).
- Il socket **NX_STILL_BOUND** (0x42) è ancora associato.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Recuperare informazioni sulle attività del socket UDP

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

*Se un puntatore di destinazione è NX_NULL, le informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.
- **udp_packets_sent** Puntatore alla destinazione per il numero totale di pacchetti UDP inviati al socket.
- **udp_bytes_sent** Puntatore alla destinazione per il numero totale di byte UDP inviati al socket.
- **udp_packets_received** Puntatore alla destinazione del numero totale di pacchetti UDP ricevuti sul socket.
- **udp_bytes_received** Puntatore alla destinazione del numero totale di byte UDP ricevuti sul socket.
- **udp_packets_queued** Puntatore alla destinazione del numero totale di pacchetti UDP in coda nel socket.
- **udp_receive_packets_dropped** Puntatore alla destinazione del numero totale di pacchetti di ricezione UDP eliminati per il socket a causa del superamento della dimensione della coda.
- **udp_checksum_errors** Puntatore alla destinazione del numero totale di pacchetti UDP con errori di checksum nel socket.

### <a name="return-values"></a>Valori restituiti

- Il recupero delle informazioni sul socket UDP riuscite **NX_SUCCESS** (0x00).
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread e timer

### <a name="preemption-possible"></a>Precedenza possibile

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

Preleva il numero di porta associato al socket UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_port_get(NX_UDP_SOCKET *socket_ptr, UINT *port_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio recupera il numero di porta associato al socket, che è utile per trovare la porta allocata da NetX nelle situazioni in cui è stato specificato il NX_ANY_PORT nel momento in cui il socket è stato associato.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.
- **port_ptr** Puntatore alla destinazione per il numero di porta restituito. I numeri di porta validi sono (1-0xFFFF).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) associazione Socket riuscita.
- **NX_NOT_BOUND** (0X24) questo socket non è associato a una porta.
- **NX_PTR_ERROR** (0x07) puntatore a socket non valido o puntatore a porta restituita.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Ricevi datagramma dal socket UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_receive(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr, 
    ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio riceve un datagramma UDP dal socket specificato. Se non viene accodato alcun datagramma sul socket specificato, il chiamante viene sospeso in base all'opzione wait fornita.

*Se viene restituito NX_SUCCESS, l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.
- **packet_ptr** Puntatore al puntatore del pacchetto del datagramma UDP.
- **WAIT_OPTION** Definisce il comportamento del servizio se un datagramma non è attualmente accodato in questo socket. Le opzioni di attesa sono definite come segue:
- NX_NO_WAIT (0x00000000)
- NX_WAIT_FOREVER (0xFFFFFFFF)
- valore di timeout in cicli (da 0x00000001 a 0xFFFFFFFE)

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Invia una notifica all'applicazione di ogni pacchetto ricevuto

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_socket_receive_notify(
    NX_UDP_SOCKET *socket_ptr,
    VOID (*udp_receive_notify)
    (NX_UDP_SOCKET *socket_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio imposta il puntatore della funzione receive Notify per la funzione di callback specificata dall'applicazione. Questa funzione di callback viene quindi chiamata ogni volta che viene ricevuto un pacchetto nel socket. Se viene fornito un puntatore NX_NULL, la funzione receive Notify è disabilitata.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket UDP.
- **udp_receive_notify** Puntatore alla funzione di callback dell'applicazione che viene chiamato quando viene ricevuto un pacchetto nel socket.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISRs

### <a name="preemption-possible"></a>Precedenza possibile

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

Questo servizio invia un datagramma UDP tramite un socket UDP precedentemente creato e associato. NetX trova un indirizzo IP locale appropriato come indirizzo di origine in base all'indirizzo IP di destinazione. Per specificare un'interfaccia e un indirizzo IP di origine specifici, l'applicazione deve usare il servizio **nx_udp_socket_interface_send** .

Si noti che questo servizio viene restituito immediatamente, indipendentemente dal fatto che il datagramma UDP sia stato inviato correttamente.

Il socket deve essere associato a una porta locale.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza Socket UDP creata in precedenza
- **packet_ptr** Puntatore al pacchetto del datagramma UDP
- **ip_address** Indirizzo IP di destinazione
- **porta** Numero di porta di destinazione valido compreso tra 1 e 0xFFFF), in ordine byte host

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) trasmissione socket UDP riuscita
- Socket **NX_NOT_BOUND** (0x24) non associato ad alcuna porta
- **NX_NO_INTERFACE_ADDRESS** (0X50) non è possibile trovare un'interfaccia in uscita adatta.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP del server non valido
- Lo spazio di **NX_UNDERFLOW** (0x02) non è sufficiente per l'intestazione UDP nel pacchetto
- Puntatore di aggiunta pacchetto di **NX_OVERFLOW** (0x03) non valido
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido
- **NX_CALLER_ERROR** (0x11) chiamante non valido di questo servizio
- Il **NX_NOT_ENABLED** UDP (0x14) non è stato abilitato
- Il numero di porta **NX_INVALID_PORT** (0x46) non è compreso in un intervallo valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Invia datagramma tramite socket UDP.

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

Questo servizio invia un datagramma UDP tramite un socket UDP precedentemente creato e associato tramite l'interfaccia di rete con l'indirizzo IP specificato come indirizzo di origine. Si noti che il servizio restituisce immediatamente un risultato, indipendentemente dal fatto che il datagramma UDP sia stato inviato correttamente o meno.

### <a name="parameters"></a>Parametri

- **socket_ptr** Socket per la trasmissione del pacchetto.
- **packet_ptr** Puntatore al pacchetto da trasmettere.
- **ip_address** Indirizzo IP di destinazione per l'invio del pacchetto.
- **porta** Porta di destinazione.
- **address_index** Indice dell'indirizzo associato all'interfaccia su cui inviare il pacchetto.

### <a name="return-values"></a>Valori restituiti

- Il pacchetto **NX_SUCCESS** (0x00) è stato inviato correttamente.
- Il socket **NX_NOT_BOUND** (0x24) non è associato a una porta.
- **NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP non valido.
- L'elaborazione UDP di **NX_NOT_ENABLED** (0x14) non è abilitata.
- **NX_PTR_ERROR** (0x07) puntatore non valido.
- **NX_OVERFLOW** (0x03) puntatore di Accodamento pacchetti non valido.
- **NX_UNDERFLOW** (0x02) puntatore a anteporre il pacchetto non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_INVALID_INTERFACE** (0x4C) indice di indirizzo non valido.
- Il numero di porta **NX_INVALID_PORT** (0x46) supera il numero di porta massimo.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Separare il socket UDP dalla porta UDP.

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

- La disassociazione del socket è riuscita **NX_SUCCESS** (0x00).
- Il socket **NX_NOT_BOUND** (0x24) non è stato associato ad alcuna porta.
- **NX_PTR_ERROR** (0x07) puntatore al socket non valido.
- Il chiamante **NX_CALLER_ERROR** (0X11) non è valido per il servizio.
- **NX_NOT_ENABLED** (0X14) questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Precedenza possibile

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

Estrarre IP e la porta di trasmissione dal datagramma UDP

### <a name="prototype"></a>Prototipo

```C
UINT nx_udp_source_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address, UINT *port);
```

### <a name="description"></a>Descrizione

Questo servizio estrae l'IP e il numero di porta del mittente dalle intestazioni IP e UDP del datagramma UDP fornito.

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto del datagramma UDP.
- **ip_address** Puntatore valido alla variabile dell'indirizzo IP restituito.
- **porta** Puntatore valido alla variabile della porta restituita.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) l'estrazione IP/porta di origine è riuscita.
- **NX_INVALID_PACKET** (0X12) il pacchetto fornito non è valido.
- **NX_PTR_ERROR** (0x07) pacchetto non valido o destinazione IP o porta.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISR

### <a name="preemption-possible"></a>Precedenza possibile

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