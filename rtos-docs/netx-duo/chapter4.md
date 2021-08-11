---
title: Capitolo 4 - Descrizione di Azure RTOS NetX Duo Services
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX Duo in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d28ca64a6a655bb3f1ad10c563450a0e65b645a1e1a2a464c4137f9a999815bc
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785023"
---
# <a name="chapter-4---description-of-azure-rtos-netx-duo-services"></a>Capitolo 4 - Descrizione di Azure RTOS NetX Duo Services

Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX Duo in ordine alfabetico. I nomi dei servizi sono progettati in modo da raggruppare tutti i servizi simili. Ad esempio, tutti i servizi ARP si trovano all'inizio di questo capitolo. 

In NetX Duo sono stati introdotti numerosi nuovi servizi per supportare le operazioni e i protocolli basati su IPv6. I servizi abilitati per IPv6 in Net Duo hanno il prefisso ***nxd**,* che indica che sono progettati per l'operazione dual stack IPv4 e IPv6.

I servizi esistenti in NetX sono completamente supportati in NetX Duo. È possibile eseguire la migrazione di applicazioni NetX a NetX Duo con un minimo sforzo di porting.

> [!NOTE]
> Si noti che è disponibile BSD-Compatible API Socket per il codice dell'applicazione legacy che non può sfruttare appieno *l'API NetX Duo ad alte prestazioni. Per altre informazioni sull'API socket di BSD-Compatible, vedere l'appendice D.*

Nella sezione "Valori restituiti" di ogni descrizione i valori in **GRASSETTO** non sono interessati dall'opzione NX_DISABLE_ERROR_CHECKING usata per disabilitare il controllo degli errori dell'API, mentre i valori in grassetto non sono completamente disabilitati. Le sezioni "Allowed From" indicano da cui è possibile chiamare ogni servizio NetX Duo.

## <a name="nx_arp_dynamic_entries_invalidate"></a>nx_arp_dynamic_entries_invalidate   
Invalidare tutte le voci dinamiche nella cache ARP

### <a name="prototype"></a>Prototipo     

```c
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

/* If status is NX_SUCCESS the dynamic ARP entries were
   successfully invalidated. */
```
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_dynamic_entry_set"></a>nx_arp_dynamic_entry_set  
Impostare una voce ARP dinamica

### <a name="prototype"></a>Prototipo  

```c
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

```c
/* Setup a dynamic ARP entry on the previously created IP
   Instance 0. */
status = nx_arp_dynamic_entry_set(&ip_0, IP_ADDRESS(1,2,3,4),
                                  0x1022, 0x1234);

/* If status is NX_SUCCESS, there is now a dynamic mapping between
   the IP address of 1.2.3.4 and the physical hardware address of
   10:22:00:00:12:34. */
```
### <a name="see-also"></a>Vedere anche 

- nx_arp_dynamic_entries_invalidate
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_enable"></a>nx_arp_enable  
Abilitare il protocollo ARP (Address Resolution Protocol)

### <a name="prototype"></a>Prototipo    

```c
UINT nx_arp_enable(
    NX_IP *ip_ptr, 
    VOID *arp_cache_memory,
    ULONG arp_cache_size);
```

### <a name="description"></a>Descrizione

Questo servizio inizializza il componente ARP di NetX Duo per l'istanza IP specifica. L'inizializzazione ARP include la configurazione della cache ARP e varie routine di elaborazione ARP necessarie per l'invio e la ricezione di messaggi ARP.

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
Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible  
No

### <a name="example"></a>Esempio

```c
/* Enable ARP and supply 1024 bytes of ARP cache memory for
   previously created IP Instance ip_0. */
status = nx_arp_enable(&ip_0, (void *) pointer, 1024);

/* If status is NX_SUCCESS, ARP was successfully enabled for this IP
instance.*/
```
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_entry_delete"></a>nx_arp_entry_delete   
Eliminare una voce ARP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_arp_entry_delete(
    NX_IP *ip_ptr, 
    ULONG ip_address);
```
### <a name="description"></a>Descrizione

Questo servizio rimuove una voce ARP per l'indirizzo IP specificato dalla relativa tabella ARP interna IP.

### <a name="parameters"></a>Parametri  

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** La voce ARP con l'indirizzo IP specificato deve essere eliminata.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ARP riuscito.
- **NX_ENTRY_NOT_FOUND** (0x16) Non è possibile trovare alcuna voce con l'indirizzo IP specificato.
- **NX_PTR_ERROR** (0x07) IP o puntatore di memoria della cache non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_IP_ADDRESS_ERROR** (0x21) L'indirizzo IP specificato non è valido.

### <a name="allowed-from"></a>Consentito da  
Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible  
No

### <a name="example"></a>Esempio

```c
/* Delete the ARP entry with the IP address 1.2.3.4. */
status = nx_arp_entry_delete(&ip_0, IP_ADDRESS(1, 2, 3, 4));

/* If status is NX_SUCCESS, ARP entry with the specified IP address
   is deleted.*/
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_gratuitous_send"></a>nx_arp_gratuitous_send   
Inviare una richiesta ARP gratuita

### <a name="prototype"></a>Prototipo  

```c
UINT nx_arp_gratuitous_send(
    NX_IP *ip_ptr,
    VOID (*response_handler)(NX_IP *ip_ptr, NX_PACKET *packet_ptr));
```                               
### <a name="description"></a>Descrizione

Questo servizio passa attraverso tutte le interfacce fisiche per trasmettere richieste ARP gratuite, purché l'indirizzo IP dell'interfaccia sia valido. Se successivamente viene ricevuta una risposta ARP, viene chiamato il gestore di risposta fornito per elaborare la risposta all'ARP gratuito.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **response_handler** Puntatore alla funzione di gestione della risposta. Se NX_NULL viene specificato , le risposte vengono ignorate.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio gratuito ARP riuscito.
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

```
/* Send gratuitous ARP without any response handler. */
status = nx_arp_gratuitous_send(&ip_0, NX_NULL);

/* If status is NX_SUCCESS the gratuitous ARP was successfully
   sent. */
```

### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_hardware_address_find"></a>nx_arp_hardware_address_find
Individuare l'indirizzo hardware fisico dato un indirizzo IP

### <a name="prototype"></a>Prototipo  

```c
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
- **NX_PTR_ERROR** (0x07) Indirizzo IP o puntatore di memoria non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Search for the hardware address associated with the IP address of
   1.2.3.4 in the ARP cache of the previously created IP
   Instance 0. */
status = nx_arp_hardware_address_find(&ip_0, IP_ADDRESS(1,2,3,4),
                                      &physical_msw,
                                      &physical_lsw);

/* If status is NX_SUCCESS, the variables physical_msw and
   physical_lsw contain the hardware address.*/
```   
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_info_get"></a>nx_arp_info_get
Recuperare informazioni sulle attività ARP

### <a name="prototype"></a>Prototipo  

```c
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

> [!NOTE]
> *Se un puntatore di destinazione NX_NULL, queste informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **arp_requests_sent** Puntatore alla destinazione per il totale delle richieste ARP inviate da questa istanza IP.
- **arp_requests_received** Puntatore alla destinazione per il totale delle richieste ARP ricevute dalla rete.
- **arp_responses_sent** Puntatore alla destinazione per il totale delle risposte ARP inviate da questa istanza IP.
- **arp_responses_received** Puntatore alla destinazione per il totale delle risposte ARP ricevute dalla rete.
- **arp_dynamic_entries** Puntatore alla destinazione per il numero corrente di voci ARP dinamiche.
- **arp_static_entries** Puntatore alla destinazione per il numero corrente di voci ARP statiche.
- **arp_aged_entries** Puntatore alla destinazione del numero totale di voci ARP obsolete e non valide.
- **arp_invalid_messages** Puntatore alla destinazione dei messaggi ARP non validi totali ricevuti.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero delle informazioni ARP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Pickup ARP information for ip_0. */
status = nx_arp_info_get(&ip_0, &arp_requests_sent,
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

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_ip_address_find"></a>nx_arp_ip_address_find
Individuare l'indirizzo IP dato un indirizzo fisico

### <a name="prototype"></a>Prototipo  

```c
UINT nx_arp_ip_address_find(
    NX_IP *ip_ptr, 
    ULONG *ip_address,
    ULONG physical_msw, 
    ULONG physical_lsw);
```
### <a name="description"></a>Descrizione

Questo servizio tenta di trovare un indirizzo IP nella cache ARP associata all'indirizzo fisico fornito.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** Puntatore all'indirizzo IP restituito, se ne viene trovato uno di cui è stato eseguito il mapping.
- **physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico da cercare.
- **physical_lsw** 32 bit inferiori (31-0) dell'indirizzo fisico da cercare.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ricerca dell'indirizzo IP ARP riuscita 
- **NX_ENTRY_NOT_FOUND** mapping (0x16) non è stato trovato nella cache ARP.
- **NX_PTR_ERROR** (0x07) Indirizzo IP o puntatore di memoria non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_INVALID_PARAMETERS** (0x4D) Physical_msw e physical_lsw sono entrambi 0.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Search for the IP address associated with the hardware address of
   0x0:0x01234 in the ARP cache of the previously created IP
   Instance ip_0. */
status = nx_arp_ip_address_find(&ip_0, &ip_address, 0x0, 0x1234);

/* If status is NX_SUCCESS, the variables ip_address contains the
   associated IP address. */
```
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_static_entries_delete"></a>nx_arp_static_entries_delete
Eliminare tutte le voci ARP statiche

### <a name="prototype"></a>Prototipo  

```c
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

```c
/* Delete all the static ARP entries for IP Instance 0, assuming
   "ip_0" is the NX_IP structure for IP Instance 0. */
status = nx_arp_static_entries_delete(&ip_0);

/* If status is NX_SUCCESS all static ARP entries in the ARP cache
   have been deleted. */
```
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_static_entry_create"></a>nx_arp_static_entry_create
Creare un mapping da IP statico a hardware nella cache ARP

### <a name="prototype"></a>Prototipo  

```c
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

```c
/* Create a static ARP entry on the previously created IP
   Instance 0. */
status = nx_arp_static_entry_create(&ip_0, IP_ADDRESS(1,2,3,4),
                                    0x0, 0x1234);

/* If status is NX_SUCCESS, there is now a static mapping between
   the IP address of 1.2.3.4 and the physical hardware address of
   0x00:0x1234. */
```
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_arp_static_entry_delete"></a>nx_arp_static_entry_delete 
Eliminare l'indirizzo IP statico per il mapping hardware nella cache ARP

### <a name="prototype"></a>Prototipo  

```c
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
- **physical_msw** Primi 16 bit (47 - **32) dell'indirizzo fisico mappato in modo statico.
- **physical_lsw** 32 bit inferiori (31 - **0) dell'indirizzo fisico mappato in modo statico.

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

```c
/* Delete a static ARP entry on the previously created IP
   instance ip_0. */
status = nx_arp_static_entry_delete(&ip_0, IP_ADDRESS(1,2,3,4),
                                    0x0, 0x1234);

/* If status is NX_SUCCESS, the previously created static ARP entry
   was successfully deleted. */
```
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nx_icmp_enable"></a>nx_icmp_enable
Abilitare Internet Control Message Protocol (ICMP)

### <a name="prototype"></a>Prototipo  

```c
UINT nx_icmp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio abilita il componente ICMP per l'istanza IP specificata. Il componente ICMP è responsabile della gestione dei messaggi di errore Internet e delle richieste ping e delle risposte. 

> [!IMPORTANT]  
> *Questo servizio abilita solo ICMP per il servizio IPv4. Per abilitare sia  ICMPv4 che ICMPv6, le* applicazioni devono usare il nxd_icmp_enable servizio .

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

```c
/* Enable ICMP on the previously created IP Instance ip_0. */
status = nx_icmp_enable(&ip_0);

/* If status is NX_SUCCESS, ICMP is enabled. */
```
### <a name="see-also"></a>Vedere anche

- nx_icmp_info_get
- nx_icmp_ping
- nxd_icmp_enable
- nxd_icmp_ping
- nxd_icmp_source_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nx_icmp_info_get"></a>nx_icmp_info_get
Recuperare informazioni sulle attività ICMP

### <a name="prototype"></a>Prototipo  

```c
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

> [!NOTE]  
> *Se un puntatore di destinazione NX_NULL, queste informazioni specifiche non vengono restituite al chiamante.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **pings_sent** Puntatore alla destinazione per il numero totale di ping inviati.
- **ping_timeouts** Puntatore alla destinazione per il numero totale di timeout ping.
- **ping_threads_suspended** Puntatore alla destinazione del numero totale di thread sospesi nelle richieste ping.
- **ping_responses_received** Puntatore alla destinazione del numero totale di risposte ping ricevute.
- **icmp_checksum_errors** Puntatore alla destinazione del numero totale di errori di checksum ICMP.
- **icmp_unhandled_messages** Puntatore alla destinazione del numero totale di messaggi ICMP non gestiti.

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

```c
/* Retrieve ICMP information from previously created IP
   instance ip_0. */
status = nx_icmp_info_get(&ip_0, &pings_sent, &ping_timeouts,
                          &ping_threads_suspended,
                          &ping_responses_received,
                          &icmp_checksum_errors,
                          &icmp_unhandled_messages);
/* If status is NX_SUCCESS, ICMP information was retrieved. */
```
### <a name="see-also"></a>Vedere anche

- nx_icmp_enable
- nx_icmp_ping
- nxd_icmp_enable
- nxd_icmp_ping
- nxd_icmp_source_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nx_icmp_ping"></a>nx_icmp_ping  
Inviare una richiesta ping all'indirizzo IP specificato

### <a name="prototype"></a>Prototipo  

```c
UINT nx_icmp_ping(
    NX_IP *ip_ptr,
    ULONG ip_address,
    CHAR *data, ULONG data_size,
    NX_PACKET **response_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio invia una richiesta ping all'indirizzo IP specificato e attende la quantità di tempo specificata per un messaggio di risposta ping. Se non viene ricevuta alcuna risposta, viene restituito un errore. In caso contrario, l'intero messaggio di risposta viene restituito nella variabile a cui punta response_ptr. 

Per inviare una richiesta ping a una destinazione IPv6, le applicazioni devono usare il servizio ***nxd_icmp_ping** _ o _ *_nxd_icmp_source_ping_** .

> [!WARNING]  
> *Se NX_SUCCESS viene restituito , l'applicazione è* responsabile del rilascio del pacchetto ricevuto dopo che non è più necessario .

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **ip_address** Indirizzo IP, in ordine di byte host, per eseguire il ping.
- **dati** Puntatore all'area dati per il messaggio ping.
- **data_size** Numero di byte nei dati ping
- **response_ptr** Puntatore al puntatore a pacchetto in cui restituire il messaggio di risposta ping.
- **wait_option** Definisce il numero di tick del timer ThreadX in attesa di una risposta ping. Le opzioni di attesa sono definite nel modo seguente:

| Opzione Wait            | Valore                           |
| -----------------------|---------------------------------|
| NX_NO_WAIT             | (0x00000000)                    |
| valore di timeout in tick | (da 0x00000001 a 0xFFFFFFFE) |
| NX_WAIT_FOREVER        | 0xffffffff                      |

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Ping riuscito. Il puntatore del messaggio di risposta è stato inserito nella variabile a cui punta response_ptr.
- **NX_NO_PACKET** (0x01) Impossibile allocare un pacchetto di richiesta ping.
- **NX_OVERFLOW** (0x03) L'area dati specificata supera le dimensioni predefinite del pacchetto per questa istanza IP.
- **NX_NO_RESPONSE** (0x29) L'INDIRIZZO IP richiesto non ha risposto.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) IP o puntatore di risposta non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
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

- nx_icmp_enable
- nx_icmp_info_get
- nxd_icmp_enable
- nxd_icmp_ping
- nxd_icmp_source_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nx_igmp_enable"></a>nx_igmp_enable
Abilitare Internet Group Management Protocol (IGMP)

### <a name="prototype"></a>Prototipo  

```c
UINT nx_igmp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio abilita il componente IGMP nell'istanza IP specificata. Il componente IGMP è responsabile del supporto per le operazioni di gestione del gruppo multicast IP.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) IGMP riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_ALREADY_ENABLED** (0x15) Questo componente è già stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Enable IGMP on the previously created IP Instance ip_0. */
status = nx_igmp_enable(&ip_0);

/* If status is NX_SUCCESS, IGMP is enabled. */
```
### <a name="see-also"></a>Vedere anche

- nx_igmp_info_get
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_info_get"></a>nx_igmp_info_get
Recuperare informazioni sulle attività IGMP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_igmp_info_get(
    NX_IP *ip_ptr,
    ULONG *igmp_reports_sent,
    ULONG *igmp_queries_received,
    ULONG *igmp_checksum_errors,
    ULONG *current_groups_joined);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle attività IGMP per l'istanza IP specificata.

> [!IMPORTANT]  
> *Se viene utilizzato un puntatore NX_NULL destinazione, le informazioni specifiche non vengono restituite al chiamante.*

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

```c
/* Retrieve IGMP information from previously created IP Instance ip_0. */
status = nx_igmp_info_get(&ip_0, &igmp_reports_sent,
                          &igmp_queries_received,
                          &igmp_checksum_errors,
                          &current_groups_joined);

/* If status is NX_SUCCESS, IGMP information was retrieved. */
```

### <a name="see-also"></a>Vedere anche

- nx_igmp_enable
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_loopback_disable"></a>nx_igmp_loopback_disable
Disabilitare il loopback IGMP

### <a name="prototype"></a>Prototipo  

```c
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

```c
/* Disable IGMP loopback for all subsequent multicast groups
   joined. */
status = nx_igmp_loopback_disable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is disabled. */
```
### <a name="see-also"></a>Vedere anche

- nx_igmp_enable
- nx_igmp_info_get
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_loopback_enable"></a>nx_igmp_loopback_enable
Abilitare il loopback IGMP

### <a name="prototype"></a>Prototipo  

```c
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

```c
/* Enable IGMP loopback for all subsequent multicast
   groups joined. */
status = nx_igmp_loopback_enable(&ip_0);

/* If status is NX_SUCCESS IGMP loopback is enabled. */
```
### <a name="see-also"></a>Vedere anche

- nx_igmp_enable
- nx_igmp_info_getnx_igmp_loopback_disable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_multicast_interface_join"></a>nx_igmp_multicast_interface_join
Aggiungere un'istanza IP a un gruppo multicast specificato tramite un'interfaccia

### <a name="prototype"></a>Prototipo  

```c
UINT nx_igmp_multicast_interface_join(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio aggiunge un'istanza IP al gruppo multicast specificato tramite un'interfaccia di rete specificata. Viene mantenuto un contatore interno per tenere traccia del numero di volte in cui lo stesso gruppo è stato unito. Dopo l'aggiunta al gruppo multicast, il componente IGMP consentirà la ricezione di pacchetti IP con questo indirizzo di gruppo tramite l'interfaccia di rete specificata e segnalerà anche ai router che questo indirizzo IP è membro di questo gruppo multicast. I messaggi di appartenenza, report e uscita IGMP vengono inviati anche tramite l'interfaccia di rete specificata. Per partecipare a un gruppo multicast IPv4 senza inviare il report di appartenenza al gruppo IGMP, l'applicazione deve usare il servizio ***nx_ipv4_multicast_interface_join***.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **group_address** Indirizzo del gruppo multicast IP di classe D da aggiungere nell'ordine dei byte dell'host.
- **interface_index** Indice dell'interfaccia collegata all'istanza di NetX Duo.

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

```c
/* Previously created IP Instance joins the multicast group
   244.0.0.200, via the interface at index 1 in the IP interface
   list. */
#define INTERFACE_INDEX 1
status = nx_igmp_multicast_interface_join
                                 (&ip IP_ADDRESS(244,0,0,200),
                                  INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully joined
   the multicast group. */
```   
### <a name="see-also"></a>Vedere anche

- nx_igmp_enable
- nx_igmp_info_getnx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_multicast_interface_leave"></a>nx_igmp_multicast_interface_leave
Lasciare il gruppo multicast specificato tramite un'interfaccia

### <a name="prototype"></a>Prototipo  

```c
UINT nx_igmp_multicast_interface_leave(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio lascia il gruppo multicast specificato tramite un'interfaccia di rete specificata. Viene mantenuto un contatore interno per tenere traccia del numero di volte in cui lo stesso gruppo è stato membro. Dopo aver lasciato il gruppo multicast, il componente IGMP invierà un report di appartenenza appropriato e potrebbe lasciare il gruppo se non sono presenti membri da questo nodo. Per lasciare un gruppo multicast IPv4 senza inviare il report di appartenenza al gruppo IGMP, l'applicazione userà il servizio ***nx_ipv4_multicast_interface_leave***.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **group_address** Indirizzo del gruppo multicast IP di classe D da lasciare. L'indirizzo IP è nell'ordine dei byte dell'host.
- **interface_index** Indice dell'interfaccia collegata all'istanza di NetX Duo.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Join a gruppi multicast riuscito.
- **NX_ENTRY_NOT_FOUND** (0x16) L'indirizzo del gruppo multicast specificato non è stato trovato nella tabella multicast locale.
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

```c
/* Leave the multicast group 244.0.0.200. */
#define INTERFACE_INDEX 1
status = nx_igmp_multicast_interface_leave
                                (&ip IP_ADDRESS(244,0,0,200),
                                 INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully leaves
   the multicast group 244.0.0.200. */
```
### <a name="see-also"></a>Vedere anche

- nx_igmp_enable
- nx_igmp_info_getnx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_multicast_join"></a>nx_igmp_multicast_join
Aggiungere l'istanza IP al gruppo multicast specificato

### <a name="prototype"></a>Prototipo  

```c
UINT nx_igmp_multicast_join(
    NX_IP *ip_ptr, 
    ULONG group_address);
```
### <a name="description"></a>Descrizione

Questo servizio aggiunge un'istanza IP al gruppo multicast specificato. Viene mantenuto un contatore interno per tenere traccia del numero di volte in cui lo stesso gruppo è stato unito. Al driver viene richiesto di inviare un report IGMP se si tratta della prima richiesta di join in rete che indica l'intenzione dell'host di partecipare al gruppo. Dopo l'aggiunta, il componente IGMP consentirà la ricezione di pacchetti IP con questo indirizzo di gruppo e segnalerà ai router che questo indirizzo IP è membro di questo gruppo multicast. Per partecipare a un gruppo multicast IPv4 senza inviare il report di appartenenza al gruppo IGMP, l'applicazione deve usare il servizio ***nx_ipv4_multicast_interface_join***.

> [!NOTE]  
> *Per aggiungere un gruppo multicast in un dispositivo non primario, usare il servizio **nx_igmp_multicast_interface_join.***

### <a name="parameters"></a>Parametri

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

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Previously created IP Instance ip_0 joins the multicast group
   224.0.0.200. */
status = nx_igmp_multicast_join(&ip_0, IP_ADDRESS(224,0,0,200);

/* If status is NX_SUCCESS, this IP instance has successfully
   joined the multicast group 224.0.0.200. */
```
### <a name="see-also"></a>Vedere anche

- nx_igmp_enable
- nx_igmp_info_get
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_igmp_multicast_leave"></a>nx_igmp_multicast_leave
Fare in modo che l'istanza IP lasci il gruppo multicast specificato

### <a name="prototype"></a>Prototipo  

```c
UINT nx_igmp_multicast_leave(
    NX_IP *ip_ptr, 
    ULONG group_address);
```
### <a name="description"></a>Descrizione

Questo servizio fa in modo che un'istanza IP lasci il gruppo multicast specificato, se il numero di richieste di partecipazione corrisponde al numero di richieste di join. In caso contrario, il numero di join interno viene semplicemente decrementato. Per lasciare un gruppo multicast IPv4 senza inviare il report di appartenenza al gruppo IGMP, l'applicazione userà il servizio ***nx_ipv4_multicast_interface_leave***.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **group_address** Gruppo multicast da lasciare.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Join a gruppi multicast riuscito.
- **NX_ENTRY_NOT_FOUND** (0x16) Richiesta di join precedente non trovata.
- **NX_INVALID_INTERFACE** (0x4C) L'indice del dispositivo punta a un'interfaccia di rete non valida.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo del gruppo IP non valido.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Cause IP instance to leave the multicast group 224.0.0.200. */
status = nx_igmp_multicast_leave(&ip_0, IP_ADDRESS(224,0,0,200);

/* If status is NX_SUCCESS, this IP instance has successfully left
   the multicast group 224.0.0.200. */
```
### <a name="see-also"></a>Vedere anche

- nx_igmp_enable
- nx_igmp_info_get
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_ip_address_change_notifiy"></a>nx_ip_address_change_notifiy
Notificare all'applicazione se l'indirizzo IP cambia

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_address_change_notify(
    NX_IP *ip_ptr,
    VOID(*change_notify)(NX_IP *, VOID *),
    VOID *additional_info);
```
### <a name="description"></a>Descrizione

Questo servizio registra una funzione di notifica dell'applicazione che viene chiamata ogni volta che viene modificato l'indirizzo IPv4.

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

```c
/* Register the function "my_ip_changed" to be called whenever the
   IP address is changed. */
status = nx_ip_address_change_notify(&ip_0, my_ip_changed,
                                      NX_NULL);

/* If status is NX_SUCCESS, the "my_ip_changed" function will be
   called whenever the IP address changes. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_address_get"></a>nx_ip_address_get
Recuperare l'indirizzo IPv4 e network mask

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_address_get(
    NX_IP *ip_ptr,
    ULONG *ip_address,
    ULONG *network_mask);
```
### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IPv4 e il subnet mask'interfaccia di rete primaria.

> [!IMPORTANT]   
> *Per ottenere informazioni sul dispositivo secondario, usare il servizio **nx_ip_interface_address_get***.

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

```c
/* Get the IP address and network mask from the previously created
   IP Instance ip_0. */
status = nx_ip_address_get(&ip_0, &ip_address, &network_mask);

/* If status is NX_SUCCESS, the variables ip_address and
   network_mask contain the IP and network mask respectively. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_address_set"></a>nx_ip_address_set
Impostare l'indirizzo IPv4 e network mask

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_address_set(
    NX_IP *ip_ptr,
    ULONG ip_address,
    ULONG network_mask);
```
### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IPv4 e network mask per l'interfaccia di rete primaria.

> [!IMPORTANT]  
> *Per impostare l'indirizzo IP e network mask per il dispositivo secondario, usare il servizio **nx_ip_interface_address_set****.

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

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Set the IP address and network mask to 1.2.3.4 and 0xFFFFFF00 for
   the previously created IP Instance ip_0. */
status = nx_ip_address_set(&ip_0, IP_ADDRESS(1,2,3,4),
                           0xFFFFFF00UL);

/* If status is NX_SUCCESS, the IP instance now has an IP address of
   1.2.3.4 and a network mask of 0xFFFFFF00. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_auxiliary_packet_pool_set"></a>nx_ip_auxiliary_packet_pool_set
Configurare un pool di pacchetti ausiliario

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_auxiliary_packet_pool_set(
    NX_IP *ip_ptr,
    NX_PACKET_POOL *aux_pool);
```
### <a name="description"></a>Descrizione

Questo servizio configura un pool di pacchetti ausiliario nell'istanza IP. Per un sistema vincolato alla memoria, l'utente può aumentare l'efficienza della memoria creando il pool di pacchetti predefinito con dimensioni del pacchetto MTU e creando un pool di pacchetti ausiliario con dimensioni di pacchetto inferiori con cui il thread IP trasmette pacchetti di piccole dimensioni. Le dimensioni dei pacchetti consigliate per il pool ausiliario sono di 256 byte, presupponendo che IPv6 e IPsec siano entrambi abilitati.

Per impostazione predefinita, l'istanza IP non accetta il pool di pacchetti ausiliario. Per abilitare questa funzionalità, *NX_DUAL_PACKET_POOL_ENABLE* deve essere definito durante la compilazione della libreria NetX Duo.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **aux_pool** Pool di pacchetti ausiliario da configurare per l'istanza IP.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) L'indirizzo IP è stato impostato correttamente.
- **NX_NOT_SUPPORTED** (0x4B) La funzionalità dual packet pool non viene compilata nella libreria.
- **NX_PTR_ERROR** (0x07) Puntatore IP o puntatore pool non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption  

No

### <a name="example"></a>Esempio

```c
#define SMALL_PAYLOAD_SIZE 256
NX_PACKET small_pool;

nx_packet_pool_create(&small_pool, "small pool", SMALL_PAYLOAD_SIZE,
                       small_pool_memory_ptr, small_pool_size);

/* Add the small packet pool to the IP instance. */
status = nx_ip_auxiliary_packet_pool_set(&ip_0, &small_pool);

/* If status is NX_SUCCESS, the IP instance now is able to use the
   small pool for transmitting small datagram. */
```
### <a name="see-also"></a>Vedere anche

- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_ip_create"></a>nx_ip_create
Creare un'istanza IP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_create(
    NX_IP *ip_ptr, 
    CHAR *name, ULONG ip_address,
    ULONG network_mask, 
    NX_PACKET_POOL *default_pool,
    VOID (*ip_network_driver)(NX_IP_DRIVER *),
    VOID *memory_ptr, 
    ULONG memory_size,
    UINT priority);
```
### <a name="description"></a>Descrizione

Questo servizio crea un'istanza IP con l'indirizzo IP e il driver di rete specificati dall'utente. Inoltre, l'applicazione deve fornire un pool di pacchetti creato in precedenza per l'istanza IP da usare per l'allocazione interna dei pacchetti. Si noti che il driver di rete dell'applicazione fornito non viene chiamato finché non viene eseguito il thread di questo indirizzo IP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore al blocco di controllo per creare una nuova istanza IP.
- **name** Nome della nuova istanza IP.
- **ip_address** Indirizzo IP per questa nuova istanza IP.
- **network_mask** Maschera per delineare la parte di rete dell'indirizzo IP per gli usi di rete secondaria e super-rete.
- **default_pool** Puntatore al blocco di controllo del pool di pacchetti NetX Duo creato in precedenza.
- **ip_network_driver** Driver di rete fornito dall'utente usato per inviare e ricevere pacchetti IP.
- **memory_ptr** Puntatore all'area di memoria per l'area dello stack del thread helper IP.
- **memory_size** Numero di byte nell'area di memoria per lo stack del thread helper IP.
- **priorità** Priorità del thread helper IP.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Creazione dell'istanza IP completata.
- **NX_NOT_IMPLEMENTED** libreria NetX Duo (0x4A) non è configurata correttamente.
- **NX_PTR_ERROR** (0x07) IP non valido, puntatore a funzione del driver di rete, pool di pacchetti o puntatore di memoria.
- **NX_SIZE_ERROR** (0x09) Le dimensioni dello stack fornite sono troppo piccole.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_IP_ADDRESS_ERROR** (0x21) L'indirizzo IP fornito non è valido.
- **NX_OPTION_ERROR** (0x21) La priorità del thread IP fornita non è valida.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Create an IP instance with an IP address of 1.2.3.4 and a network
   mask of 0xFFFFFF00UL. The "ethernet_driver" specifies the entry
   point of the application specific network driver and the
   "stack_memory_ptr" specifies the start of a 1024 byte memory
   area that is used for this IP instance’s helper thread. */
status = nx_ip_create(&ip_0, "NetX IP Instance ip_0",
                      IP_ADDRESS(1, 2, 3, 4),
                      0xFFFFFF00UL, &pool_0, ethernet_driver,
                      stack_memory_ptr, 1024, 1);

/* If status is NX_SUCCESS, the IP instance has been created. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_delete"></a>nx_ip_delete
Eliminare un'istanza IP creata in precedenza

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_delete(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza IP creata in precedenza e rilascia tutte le risorse di sistema di proprietà dell'istanza IP.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione IP riuscita.
- **NX_SOCKETS_BOUND** (0x28) A questa istanza IP sono ancora associati socket UDP o TCP. Tutti i socket devono essere non associati ed eliminati prima di eliminare l'istanza IP.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```c
/* Delete a previously created IP instance. */
status = nx_ip_delete(&ip_0);

/* If status is NX_SUCCESS, the IP instance has been deleted. */
```

### <a name="see-also"></a>Vedere anche 

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_driver_direct_command"></a>nx_ip_driver_direct_command
Eseguire il comando per il driver di rete

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_driver_direct_command
    (NX_IP *ip_ptr,
    UINT command,
    ULONG *return_value_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio fornisce un'interfaccia diretta al driver dell'interfaccia di rete principale dell'applicazione specificato durante la ***nx_ip_create*** chiamata. È possibile usare comandi specifici dell'applicazione specificando che il valore numerico è maggiore o uguale a NX_LINK_USER_COMMAND.

> [!IMPORTANT]  
> *Per eseguire il comando per il dispositivo secondario, usare il **nx_ip_driver_interface_direct_command** .*

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

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Make a direct call to the application-specific network driver
   for the previously created IP instance. For this example, the
   network driver is interrogated for the link status. */
status = nx_ip_driver_direct_command(&ip_0, NX_LINK_GET_STATUS,
                                     &link_status);

/* If status is NX_SUCCESS, the link_status variable contains a
   NX_TRUE or NX_FALSE value representing the status of the
   physical link. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_driver_interface_direct_command"></a>nx_ip_driver_interface_direct_command
Eseguire il comando per il driver di rete

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_driver_interface_direct_command(
    NX_IP *ip_ptr,
    UINT command,
    UINT interface_index,
    ULONG *return_value_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio fornisce un comando diretto al driver di dispositivo di rete dell'applicazione nell'istanza IP. È possibile usare comandi specifici dell'applicazione specificando che il valore numerico è maggiore o uguale *a NX_LINK_USER_COMMAND*.

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
- **NX_PTR_ERROR** (0x07) IP non valido o puntatore al valore restituito.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
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

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_forwarding_disable"></a>nx_ip_forwarding_disable  
Disabilitare l'inoltro di pacchetti IP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_forwarding_disable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio disabilita l'inoltro dei pacchetti IP all'interno del componente IP di NetX Duo. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) L'inoltro IP ha avuto esito positivo.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Preemption Possible  

No

### <a name="example"></a>Esempio

```c
/* Disable IP forwarding on this IP instance. */
status = nx_ip_forwarding_disable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been disabled on the
   previously created IP instance. */
```
### <a name="see-also"></a>Vedere anche  

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_forwarding_enable"></a>nx_ip_forwarding_enable
Abilitare l'inoltro di pacchetti IP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_forwarding_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio consente l'inoltro di pacchetti IP all'interno del componente IP NetX Duo. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

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

```c
/* Enable IP forwarding on this IP instance. */
status = nx_ip_forwarding_enable(&ip_0);

/* If status is NX_SUCCESS, IP forwarding has been enabled on the
   previously created IP instance. */
```
### <a name="see-also"></a>Vedere anche 

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_fragment_disable"></a>nx_ip_fragment_disable
Disabilitare la frammentazione dei pacchetti IP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_fragment_disable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio disabilita la funzionalità di frammentazione e riassemblamento dei pacchetti IPv4 e IPv6. Per i pacchetti in attesa di essere riassemblati, questo servizio rilascia questi pacchetti. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Frammento IP riuscito disabilitato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** frammentazione IP (0x14) non è abilitata nell'istanza IP.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Disable IP fragmenting on this IP instance. */
status = nx_ip_fragment_disable(&ip_0);

/* If status is NX_SUCCESS, disables IP fragmenting on the
   previously created IP instance. */
```

### <a name="see-also"></a>Vedere anche  

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_fragment_enable"></a>nx_ip_fragment_enable
Abilitare la frammentazione dei pacchetti IP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_fragment_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio consente la frammentazione e il riassemblamento dei pacchetti IPv4 e IPv6. Al momento della creazione dell'attività IP, questo servizio viene disabilitato automaticamente.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Correttamente abilitato il frammento IP.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** funzionalità di 0x14 IP non vengono compilate in NetX Duo.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Enable IP fragmenting on this IP instance. */
status = nx_ip_fragment_enable(&ip_0);

/* If status is NX_SUCCESS, IP fragmenting has been enabled on the
   previously created IP instance. */
```
### <a name="see-also"></a>Vedere anche  

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_gateway_address_clear"></a>nx_ip_gateway_address_clear
Cancellare l'indirizzo del gateway IPv4

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_gateway_address_clear(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio cancella l'indirizzo del gateway IPv4 configurato nell'istanza di . Per cancellare un valore predefinito IPv6 esterno dall'istanza IP, le applicazioni devono usare il servizio ***nxd_ipv6_default_router_delete.***

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) L'indirizzo del gateway IP è stato cancellato.
- **NX_PTR_ERROR** (0x07) Blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Clear the gateway address of IP instance. */
status = nx_ip_gateway_address_clear(&ip_0);

/* If status == NX_SUCCESS, the gateway address was successfully
   cleared from the IP instance. */
```
### <a name="see-also"></a>Vedere anche

-nx_ip_gateway_address_get -nx_ip_gateway_address_set -nx_ip_info_get -nx_ip_static_route_add -nx_ip_static_route_delete -nxd_ipv6_default_router_add -nxd_ipv6_default_router_delete -nxd_ipv6_default_router_entry_get -nxd_ipv6_default_router_get -nxd_ipv6_default_router_number_of_entries_get

## <a name="nx_ip_gateway_address_get"></a>nx_ip_gateway_address_get
Ottenere l'indirizzo del gateway IPv4

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_gateway_address_get(
    NX_IP *ip_ptr, 
    ULONG *ip_address);
```
### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo del gateway IPv4 configurato nell'istanza IP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP
- **ip_address** Puntatore alla memoria in cui è archiviato l'indirizzo del gateway

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Operazione get riuscita 
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP o puntatore all'indirizzo IP non valido
- **NX_NOT_FOUND** (0x4E) Gateway non trovato
- **NX_CALLER_ERROR** (0x11) S non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
ULONG ip_address;

/* Get the gateway address of IP instance. */
status = nx_ip_gateway_address_get(&ip_0, &ip_address);

/* If status == NX_SUCCESS, the gateway address was successfully
   got. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nx_ip_gateway_address_set"></a>nx_ip_gateway_address_set
Impostare l'indirizzo IP del gateway

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_gateway_address_set(
    NX_IP *ip_ptr, 
    ULONG ip_address);
```
### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IP del gateway IPv4. Tutto il traffico fuori rete viene instradato a questo gateway per la trasmissione. Il gateway deve essere accessibile direttamente tramite una delle interfacce di rete. Per configurare l'indirizzo del gateway IPv6, usare il ***nxd_ipv6_default_router_add.*** 

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

```c
/* Setup the Gateway address for previously created IP
   Instance ip_0. */
status = nx_ip_gateway_address_set(&ip_0, IP_ADDRESS(1,2,3,99);

/* If status is NX_SUCCESS, all out-of-network send requests are
   routed to 1.2.3.99. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nx_ip_info_get"></a>nx_ip_info_get
Recuperare informazioni sulle attività IP

### <a name="prototype"></a>Prototipo  

```c
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

> [!NOTE]  
> *Se viene utilizzato un puntatore NX_NULL destinazione, le informazioni specifiche non vengono restituite al chiamante.*

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

```c
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

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_interface_address_get"></a>nx_ip_interface_address_get
Recuperare l'indirizzo IP dell'interfaccia

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_interface_address_get (
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG *ip_address,
    ULONG *network_mask);
```
### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IPv4 di un'interfaccia di rete specificata. Per recuperare l'indirizzo IPv6, l'applicazione userà il servizio ***nxd_ipv6_address_get***

> [!CAUTION]  
> *Il dispositivo specificato, se non il dispositivo primario, deve essere* collegato in precedenza all'istanza IP .

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

```c
#define INTERFACE_INDEX 1

/* Get device IP address and network mask for the specified
   interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_get(ip_ptr,INTERFACE_INDEX,
                                     &ip_address,
                                     &network_mask);

/* If status is NX_SUCCESS the interface address was successfully
   retrieved. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_address_mapping_configure"></a>nx_ip_interface_address_mapping_configure
Configurare se è necessario il mapping degli indirizzi

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_interface_address_mapping_configure(
    NX_IP *ip_ptr,
    UINT interface_index,
    UINT mapping_needed);
```
### <a name="description"></a>Descrizione

Questo servizio configura se l'indirizzo IP e il mapping degli indirizzi MAC sono necessari per l'interfaccia di rete specificata. Questo servizio viene in genere chiamato dal driver di dispositivo dell'interfaccia per notificare lo stack IP se l'interfaccia sottostante richiede il mapping degli indirizzi IP al livello 2 (MAC).

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP
- **interface_index** Indicizzare l'interfaccia di rete
- **mapping_needed** NX_TRUE -- mapping degli indirizzi necessario NX_FALSE -- mapping degli indirizzi non necessario

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Configurazione riuscita
- **NX_INVALID_INTERFACE** (0x4C) Indice del dispositivo non valido
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) il servizio non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE 0
UCHAR mapping_needed = NX_TRUE;

/* Configure address mapping needed specified interface. */
status = nx_ip_interface_address_mapping_configure(&ip_0,
                                             PRIMARY_INTERFACE,
                                             mapping_needed);

/* If status == NX_SUCCESS, the address mapping needed was
   successfully configured. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_address_set"></a>nx_ip_interface_address_set
Impostare l'indirizzo IP dell'interfaccia e network mask

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_interface_address_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG ip_address,
    ULONG network_mask);
```
### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IPv4 e network mask per l'interfaccia IP specificata. Per configurare l'indirizzo dell'interfaccia IPv6, l'applicazione deve usare il servizio ***nxd_ipv6_address_set***. 
 
> [!WARNING]  
> *L'interfaccia specificata deve essere collegata in precedenza all'istanza IP*. 

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **interface_index** Indice dell'interfaccia collegata all'istanza di NetX Duo.
- **ip_address** Nuovo indirizzo IP dell'interfaccia di rete.
- **network_mask** Nuova interfaccia network mask.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'indirizzo IP è stato impostato correttamente.
- **NX_INVALID_INTERFACE** (0x4C) L'interfaccia di rete specificata non è valida.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Puntatori non validi.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define INTERFACE_INDEX 1

/* Set device IP address and network mask for the specified
   interface index 1 in IP instance list of interfaces). */
status = nx_ip_interface_address_set(ip_ptr, INTERFACE_INDEX,
                                     ip_address,
                                     network_mask);

/* If status is NX_SUCCESS the interface IP address and mask was
   successfully set. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_attach"></a>nx_ip_interface_attach
Collegare l'interfaccia di rete all'istanza IP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_interface_attach(
    NX_IP *ip_ptr, 
    CHAR *interface_name,
    ULONG ip_address,
    ULONG network_mask,
    VOID(*ip_link_driver)(struct NX_IP_DRIVER_STRUCT *));
```
### <a name="description"></a>Descrizione

Questo servizio aggiunge un'interfaccia di rete fisica all'interfaccia IP. Si noti che l'istanza IP viene creata con l'interfaccia primaria, quindi ogni interfaccia aggiuntiva è secondaria all'interfaccia primaria. Il numero totale di interfacce di rete collegate all'istanza IP (inclusa **l'interfaccia primaria)** non può superare NX_MAX_PHYSICAL_INTERFACES .

Se il thread IP non è ancora in esecuzione, le interfacce secondarie verranno inizializzate come parte del processo di avvio del thread IP che inizializza tutte le interfacce fisiche.

Se il thread IP non è ancora in esecuzione, l'interfaccia secondaria viene inizializzata come parte del ***nx_ip_interface_attach*** servizio.

> [!WARNING]  
> *ip_ptr deve puntare a una struttura IP NetX Duo valida. **NX_MAX_PHYSICAL_INTERFACES** deve essere configurato per il numero di interfacce di rete per l'istanza IP. Il valore predefinito è .*

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **interface_name** Puntatore alla stringa del nome dell'interfaccia.
- **ip_address** Indirizzo IP del dispositivo nell'ordine dei byte dell'host.
- **network_mask** L'network mask del dispositivo nell'ordine dei byte dell'host.
- **ip_link_driver** Driver Ethernet per l'interfaccia.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** voce (0x00) viene aggiunta alla tabella di routing statica.
- **NX_NO_MORE_ENTRIES** (0x17) Numero massimo di interfacce. NX_MAX_PHYSICAL_INTERFACES superato. Se IPv6 è abilitato, questo errore può anche indicare che il driver potrebbe non avere risorse sufficienti per gestire le operazioni multicast IPv6.
- **NX_DUPLICATED_ENTRY** (0x52) L'indirizzo IP fornito è già usato in questa istanza IP.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Input puntatore non valido.
- **NX_IP_ADDRESS_ERROR** (0x21) Input indirizzo IP non valido.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
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

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_capability_get"></a>nx_ip_interface_capability_get
Ottenere la funzionalità hardware dell'interfaccia

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_interface_capability_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG *interface_capability_flag);
```
### <a name="description"></a>Descrizione

Questo servizio recupera il flag di funzionalità dall'interfaccia di rete specificata. Per usare questo servizio, la libreria NetX Duo deve essere compilata con l'opzione ***NX_ENABLE_INTERFACE_CAPABILITY*** abilitata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP
- **interface_index** Indice dell'interfaccia di rete
- **interface_capability_flag** Puntatore allo spazio di memoria per il flag di funzionalità

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Le informazioni sulle funzionalità dell'interfaccia sono state ottenute correttamente.
- **NX_NOT_SUPPORTED** funzionalità dell'0x4B (0x4B) non è supportata in questa build.
- **NX_INVALID_INTERFACE** (0x4C) L'indice dell'interfaccia non è valido
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido o Puntatore al flag di funzionalità non valido
- **NX_CALLER_ERROR** (0x11) il servizio non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE 0
ULONG       capability_flag;

/* Get the hardware capability flag of specified interface. */
status = nx_ip_interface_capability_get(&ip_0,
                                        PRIMARY_INTERFACE,
                                        &capability_flag);

/* If status == NX_SUCCESS, the capability flag from the primary
   interface was successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_capability_set"></a>nx_ip_interface_capability_set
Impostare il flag di funzionalità hardware

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_interface_capability_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG interface_capability_flag);
```                           
### <a name="description"></a>Descrizione

Questo servizio viene usato dal driver di dispositivo di rete per configurare il flag di funzionalità per un'interfaccia di rete specificata. Per usare questo servizio, la libreria NetX Duo deve essere compilata con ***l'opzione NX_ENABLE_INTERFACE_CAPABILITY*** definita.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP
- **interface_index** Indice dell'interfaccia di rete
- **interface_capability_flag** Flag di funzionalità per l'output

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostare correttamente il flag di funzionalità hardware dell'interfaccia.
- **NX_NOT_SUPPORTED** funzionalità dell'0x4B (0x4B) non è supportata in questa build.
- **NX_INVALID_INTERFACE** (0x4C) L'indice dell'interfaccia non è valido 
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido 
- **NX_CALLER_ERROR** (0x11) S ervice non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE 0
ULONG capability_flag = \
                 NX_INTERFACE_CAPABILITY_IPV4_TX_CHECKSUM |\
                 NX_INTERFACE_CAPABILITY_IPV4_RX_CHECKSUM;
UINT device_index = 0;

/* Set the hardware capability flag of specified interface. */
status = nx_ip_interface_capability_set(&ip_0,
                                        PRIMARY_INTERFACE,
                                        capability_flag);

/* If status == NX_SUCCESS, the hardware capability flag was
   successfully set. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_detach"></a>nx_ip_interface_detach
Scollegare l'interfaccia specificata dall'istanza IP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_interface_address_set(
    NX_IP *ip_ptr, 
    UINT index);
```
### <a name="description"></a>Descrizione

Questo servizio scollega l'interfaccia IP specificata dall'istanza IP. Dopo lo scollegamento di un'interfaccia, tutti i socket TCP connessi vengono chiusi e le voci ND cache e ARP per questa interfaccia vengono rimosse dalle rispettive tabelle. Le appartenenze IGMP per questa interfaccia vengono rimosse.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **index** Indice dell'interfaccia da rimuovere.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) È stata rimossa correttamente un'interfaccia fisica.
- **NX_INVALID_INTERFACE** (0x4C) L'interfaccia di rete specificata non è valida.
- **NX_PTR_ERROR** (0x07) Puntatori non validi.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define INTERFACE_INDEX 1

/* Detach interface 1. */
status = nx_ip_interface_detach(&IP_0, INTERFACE_INDEX);

/* If status is NX_SUCCESS the interface is successfully detached
   from the IP instance. */
```

### <a name="see-also"></a>Vedere anche  

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_info_get"></a>nx_ip_interface_info_get
Recuperare i parametri dell'interfaccia di rete

### <a name="prototype"></a>Prototipo  

```c
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

> [!WARNING]  
> *ip_ptr deve puntare a una struttura IP NetX Duo valida. L'interfaccia specificata, se non l'interfaccia primaria, deve essere collegata in precedenza all'istanza IP*.

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

- **NX_SUCCESS** (0x00) Sono state ottenute informazioni sull'interfaccia.
- **NX_PTR_ERROR** (0x07) Input puntatore non valido.
- **NX_INVALID_INTERFACE** (0x4C) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) il servizio non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
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

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_mtu_set"></a>nx_ip_interface_mtu_set
Impostare il valore MTU di un'interfaccia di rete

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_interface_mtu_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG mtu_size);
```
### <a name="description"></a>Descrizione

Questo servizio viene usato dal driver di dispositivo per configurare il valore MTU IP per l'interfaccia di rete specificata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP
- **interface_index** Indicizzare l'interfaccia di rete
- **mtu_size** Dimensioni MTU IP

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Impostare correttamente il valore MTU
- **NX_INVALID_INTERFACE** (0x4C) L'indice dell'interfaccia non è valido
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) il servizio non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE 0
ULONG       mtu_size = 1500;

/* Set the MTU size of specified interface. */
status = nx_ip_interface_mtu_set(&ip_0,
                                 PRIMARY_INTERFACE, mtu_size);

/* If status == NX_SUCCESS, the MTU size was successfully set. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_physical_address_get"></a>nx_ip_interface_physical_address_get
Ottenere l'indirizzo fisico di un dispositivo di rete

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_interface_physical_address_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG *physical_msw,
    ULONG *physical_lsw);
```
### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo fisico di un'interfaccia di rete dall'istanza IP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP
- **interface_index** Indice dell'interfaccia di rete
- **physical_msw** Puntatore alla destinazione per i primi 16 bit dell'indirizzo MAC del dispositivo
- **physical_lsw** Puntatore alla destinazione per i 32 bit inferiori dell'indirizzo MAC del dispositivo

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Operazione riuscita
- **NX_INVALID_INTERFACE** (0x4C) L'indice dell'interfaccia non è valido
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido o puntatore di indirizzo fisico
- **NX_CALLER_ERROR** (0x11) non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE 0
ULONG   physical_msw;
ULONG   physical_lsw;

/* Get the physical address of specified interface. */
status = nx_ip_interface_physical_address_get(&ip_0,
                                              PRIMARY_INTERFACE,
                                              &physical_msw,
                                              &physical_lsw);

/* If status == NX_SUCCESS, the physical address was successfully
   retrieved. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_physical_address_set"></a>nx_ip_interface_physical_address_set
Impostare l'indirizzo fisico per un'interfaccia di rete specificata

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_interface_physical_address_set(
    NX_IP *ip_ptr,
    UINT interface_index,
    ULONG physical_msw,
    ULONG physical_lsw,
    UINT update_driver);
```
### <a name="description"></a>Descrizione

Questo servizio viene usato dall'applicazione o da un driver di dispositivo per configurare l'indirizzo fisico dell'indirizzo MAC dell'interfaccia di rete specificata. Il nuovo indirizzo MAC viene applicato al blocco di controllo della struttura dell'interfaccia. Se il flag ***update_driver*** è impostato, viene eseguito un comando a livello di driver in modo che il driver di dispositivo sia in grado di aggiornare l'indirizzo MAC programmato nel controller Ethernet.

In una situazione tipica, questo servizio viene chiamato dal driver di dispositivo dell'interfaccia durante la fase di inizializzazione per notificare lo stack IP del relativo indirizzo MAC. In questo caso, il ***flag update_driver*** non deve essere impostato.

Questa routine può essere chiamata anche dall'applicazione utente per riconfigurare l'indirizzo MAC dell'interfaccia in fase di esecuzione. In questo caso ***d'uso, update_driver*** deve essere impostato il flag , in modo che il nuovo indirizzo MAC possa essere applicato al driver di dispositivo.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP
- **interface_index** Indicizzare l'interfaccia di rete
- **physical_msw** Puntatore alla destinazione per i primi 16 bit dell'indirizzo MAC del dispositivo
- **physical_lsw** Puntatore alla destinazione per i 32 bit inferiori dell'indirizzo MAC del dispositivo

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Operazione riuscita
- **NX_UNHANDLED_COMMAND** (0x4B) non riconosciuto dal driver
- **NX_INVALID_INTERFACE** (0x4C) Interface index is not valid (Indice dell'interfaccia di 0x4C non valido)
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE 0
ULONG       physical_msw = 0x00CF;
ULONG       physical_lsw = 0x01020304;

/* Set the physical address of specified device. */
status = nx_ip_interface_physical_address_set(&ip_0,
                                              PRIMARY_INTERFACE,
                                              physical_msw,
                                              physical_lsw,
                                              NX_TRUE);

/* If status == NX_SUCCESS, the physical address was successfully
   set. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_status_check
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_interface_status_check"></a>nx_ip_interface_status_check
Controllare lo stato di un'istanza IP

### <a name="prototype"></a>Prototipo  

```c
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
- **interface_index** Il numero di indice needed_status lo stato IP richiesto, definito nel formato mappa di bit come segue:
  - **NX_IP_INITIALIZE_DONE** (0x0001)
  - **NX_IP_ADDRESS_RESOLVED** (0x0002)
  - **NX_IP_LINK_ENABLED** (0x0004)
  - **NX_IP_ARP_ENABLED** (0x0008)
  - **NX_IP_UDP_ENABLED** (0x0010)
  - **NX_IP_TCP_ENABLED** (0x0020)
  - **NX_IP_IGMP_ENABLED** (0x0040)
  - **NX_IP_RARP_COMPLETE** (0x0080)
  - **NX_IP_INTERFACE_LINK_ENABLED** (0x0100)
- **actual_status** Puntatore alla destinazione dei bit effettivi impostati. wait_option definisce il comportamento del servizio se i bit di stato richiesti non sono disponibili. Le opzioni di attesa sono definite come segue:
  - **NX_NO_WAIT** (0x00000000)
  - **valore di timeout** (0x00000001 tramite 0xFFFFFFFE)
  - **NX_WAIT_FOREVER** 0xFFFFFFFF

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

```c
/* Wait 10 ticks for the link up status on the previously created IP
   instance. */
status = nx_ip_interface_status_check(&ip_0, 1, NX_IP_LINK_ENABLED,
                                      &actual_status, 10);

/* If status is NX_SUCCESS, the secondary link for the specified IP
   instance is up. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_link_status_change_notify_set

## <a name="nx_ip_link_status_change_notify_set"></a>nx_ip_link_status_change_notify_set
Impostare la funzione di callback di notifica della modifica dello stato del collegamento

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_link_status_change_notify_set(
    NX_IP *ip_ptr,
    VOID(*link_status_change_notify)(NX_IP *ip_ptr, UINT interface_index, UINT link_up));
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

```c
/* Configure a callback function to be used when the physical
   interface status is changed. */
status = nx_ip_link_status_change_notify_set(&ip_0,
                                             my_change_cb);

/* If status == NX_SUCCESS, the link status change notify function
   is set. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_interface_address_get
- nx_ip_interface_address_mapping_configure
- nx_ip_interface_address_set
- nx_ip_interface_attach
- nx_ip_interface_capability_get
- nx_ip_interface_capability_set
- nx_ip_interface_detach
- nx_ip_interface_info_get
- nx_ip_interface_mtu_set
- nx_ip_interface_physical_address_get
- nx_ip_interface_physical_address_set
- nx_ip_interface_status_check

## <a name="nx_ip_max_payload_size_find"></a>nx_ip_max_payload_size_find
Calcolare il payload massimo dei dati dei pacchetti

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_max_payload_size_find(
    NX_IP *ip_ptr,
    NXD_ADDRESS *dest_address,
    UINT if_index,
    UINT src_port,
    UINT dest_port,
    ULONG protocol,
    ULONG *start_offset_ptr,
    ULONG *payload_length_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio trova le dimensioni massime del payload dell'applicazione che non richiederanno la frammentazione IP per raggiungere la destinazione. Ad esempio, il payload è inferiore o inferiore alle dimensioni MTU dell'interfaccia locale. (o il valore MTU del percorso ottenuto tramite l'individuazione MTU del percorso IPv6). L'intestazione IP e le dimensioni superiori dell'intestazione dell'applicazione (TCP o UDP) vengono sottratti dal payload totale. Se i criteri di sicurezza IPsec di NetX Duo si applicano a questo punto finale, anche le intestazioni IPsec (ESP/AH) e il sovraccarico associato, ad esempio vettore iniziale, vengono sottratti dall'MTU. Questo servizio è applicabile sia per i pacchetti IPv4 che per i pacchetti IPv6.

Il parametro *if_index* specifica l'interfaccia da usare per inviare il pacchetto. Per un sistema multihome, il chiamante deve specificare il parametro if_index se la destinazione è un indirizzo locale di collegamento *broadcast* (solo IPv4), multicast o IPv6.

Questo servizio restituisce due valori al chiamante:

1) start_offset_ptr: questo è il percorso dopo le intestazioni TCP/UDP/IP/IPsec.
2) payload_length_ptr: la quantità di dati che l'applicazione può trasferire senza superare MTU.

Non esiste un servizio NetX equivalente.

### <a name="restrictions"></a>Restrizioni 

L'istanza IP deve essere creata in precedenza.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP
- **dest_address** Puntatore all'indirizzo di destinazione del pacchetto
- **if_index** Indica l'indice dell'interfaccia da utilizzare
- **src_port** Numero di porta di origine
- **dest_port** Numero di porta di destinazione
- **protocollo** Protocollo di livello superiore da usare
- **start_offset_ptr** Puntatore all'inizio dei dati per il payload massimo dei pacchetti
- **payload_length_ptr** Puntatore alle dimensioni del payload escluse le intestazioni

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** payload (0x00) calcolato correttamente
- **NX_INVALID_INTERFACE** di interfaccia (0x4C) non è valido o l'interfaccia non è valida.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP non valido.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido o indirizzo di destinazione non valido
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo non valido specificato 
- **NX_NOT_SUPPORTED** (0x4B) Protocollo non valido (non UDP o TCP)
- **NX_CALLER_ERROR** (0x11) non viene chiamato dall'inizializzazione del sistema o dal contesto del thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* The following example determines the maximum payload for UDP
   packet to remote host. */
#define PRIMARY_INTERFACE 0
status = nx_ip_max_payload_size_find(&ip_0,
                                     &dest_ipv6_address,
                                     PRIMARY_INTERFACE,
                                     source_port,
                                     dest_port, NX_PROTOCOL_UDP,
                                     &start_offset,
                                     &payload_length);

/* A return value of NX_SUCCESS indicates the packet payload
   payload_length starting at the offset start_offset is
   successfully computed. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ip_raw_packet_disable"></a>nx_ip_raw_packet_disable
Disabilitare l'invio/ricezione di pacchetti non elaborati

### <a name="prototype"></a>Prototipo  

```c
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

```c
/* Disable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_disable(&ip_0);
/* If status is NX_SUCCESS, raw IP packet sending/receiving has
   been disabled for the previously created IP instance. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_packet_enable"></a>nx_ip_raw_packet_enable
Abilitare l'elaborazione di pacchetti non elaborati

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_raw_packet_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio consente la trasmissione e la ricezione di pacchetti IP non elaborati per questa istanza IP. I pacchetti TCP, UDP, ICMP e IGMP in ingresso vengono comunque elaborati da NetX Duo. I pacchetti con tipi di protocollo di livello superiore sconosciuti vengono elaborati dalla routine di ricezione dei pacchetti non elaborati.

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

```c
/* Enable raw packet sending/receiving for this IP instance. */
status = nx_ip_raw_packet_enable(&ip_0);

/* If status is NX_SUCCESS, raw IP packet sending/receiving has
   been enabled for the previously created IP instance. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_packet_filter_set"></a>nx_ip_raw_packet_filter_set
Impostare il filtro di pacchetti IP non elaborati

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_raw_packet_filter_set(
    NX_IP *ip_ptr,
    UINT (*raw_packet_filter)(NX_IP *, ULONG, NX_PACKET *));
```
### <a name="description"></a>Descrizione

Questo servizio configura il filtro di pacchetti non elaborati IP. La funzione di filtro dei pacchetti non elaborati, implementata dall'applicazione utente, consente a un'applicazione di ricevere pacchetti non elaborati in base ai criteri specificati dall'utente. Si noti che il livello wrapper BSD di NetX Duo usa la funzionalità di filtro di pacchetti non elaborati per gestire i socket non elaborati nel livello BSD. Per usare questo servizio, la libreria NetX Duo deve essere compilata con ***l'opzione NX_ENABLE_IP_RAW_PACKET_FILTER*** definita.

### <a name="parameters"></a>Parametri  

- **ip_ptr** Puntatore a blocco di controllo IP
- **raw_packet_filter** Puntatore a funzione del filtro di pacchetti non elaborati

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Impostare correttamente la routine del filtro di pacchetti non elaborati
- **NX_NOT_SUPPORT** (0x4B) Non è disponibile il supporto per pacchetti non elaborati
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
UINT raw_packet_filter(NX_IP *ip_ptr, ULONG protocol,
                       NX_PACKET *packet_ptr)
{

/* Simply filter protocol. */
if(protocol == NX_IP_RAW)
   return NX_SUCCESS;
else
   return NX_NOT_SUCCESSFUL;
}

void raw_packet_thread_entry(ULONG id)
{

/* Set the raw packet filter of IP instance. */
status = nx_ip_raw_packet_filter_set(&ip_0,
                                     raw_packet_filter);

/* If status == NX_SUCCESS, the raw packet filter of IP instance
   was successfully set. */
}
```
### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_packet_receive"></a>nx_ip_raw_packet_receive
Ricevere un pacchetto IP non elaborato

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_raw_packet_receive(
    NX_IP *ip_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio riceve un pacchetto IP non elaborato dall'istanza IP specificata. Se sono presenti pacchetti IP nella coda di ricezione di pacchetti non elaborati, il primo pacchetto (meno recente) viene restituito al chiamante. In caso contrario, se non sono disponibili pacchetti, il chiamante può sospendere come specificato dall'opzione wait.

> [!CAUTION]   
> *Se NX_SUCCESS, viene restituito , l'applicazione* è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **packet_ptr** Puntatore al puntatore in cui inserire il pacchetto IP non elaborato ricevuto.
- **wait_option** Definisce il comportamento del servizio se i pacchetti non sono disponibili. Le opzioni di attesa sono definite come segue:
   - **NX_NO_WAIT** (0x00000000)
   - **NX_WAIT_FOREVER** (0xFFFFFFFF)
   - **valore di timeout nei tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Ricezione di pacchetti ip non elaborati riuscita.
- **NX_NO_PACKET** (0x01) Nessun pacchetto disponibile.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_PTR_ERROR** (0x07) IP non valido o puntatore a pacchetto restituito.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Receive a raw IP packet for this IP instance, wait for a maximum
   of 4 timer ticks. */
status = nx_ip_raw_packet_receive(&ip_0, &packet_ptr, 4);

/* If status is NX_SUCCESS, the raw IP packet pointer is in the
   variable packet_ptr. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_packet_send"></a>nx_ip_raw_packet_send
Inviare un pacchetto IP non elaborato

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_raw_packet_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    ULONG type_of_service);
```
### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto IPv4 non elaborato all'indirizzo IP di destinazione. Si noti che questa routine restituisce immediatamente e non è quindi noto se il pacchetto IP è stato effettivamente inviato. Il driver di rete sarà responsabile del rilascio del pacchetto al termine della trasmissione.

Per un sistema multihome, NetX Duo usa l'indirizzo IP di destinazione per trovare un'interfaccia di rete appropriata e usa l'indirizzo IP dell'interfaccia come indirizzo di origine. Se l'indirizzo IP di destinazione è broadcast o multicast, viene usata la prima interfaccia valida. Le applicazioni usano ***nx_ip_raw_packet_source_send*** in questo caso.

Per inviare un pacchetto IPv6 non elaborato, l'applicazione deve usare il servizio ***nxd_ip_raw_packet_send,** _ o _ *_nxd_ip_raw_packet_source_send._**

> [!WARNING]  
> *A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché il driver di rete rilascerà il pacchetto dopo la trasmissione* di .

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **packet_ptr** Puntatore al pacchetto IP non elaborato da inviare.
- **destination_ip** Indirizzo IP di destinazione, che può essere un indirizzo IP host specifico, una trasmissione di rete, un loop-back interno o un indirizzo multicast.
- **type_of_service** Definisce il tipo di servizio per la trasmissione, i valori validi sono i seguenti:
    - **NX_IP_NORMAL** (0x00000000)
    - **NX_IP_MIN_DELAY** (0x00100000)
    - **NX_IP_MAX_DATA** (0x00080000)
    - **NX_IP_MAX_RELIABLE** (0x00040000)
    - **NX_IP_MIN_COST** (0x00020000)

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

```c
/* Send a raw IP packet to IP address 1.2.3.5. */
status = nx_ip_raw_packet_send(&ip_0, packet_ptr,
                               IP_ADDRESS(1,2,3,5),
                               NX_IP_NORMAL);

/* If status is NX_SUCCESS, the raw IP packet pointed to by
   packet_ptr has been sent. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_packet_source_send"></a>nx_ip_raw_packet_source_send
Inviare un pacchetto IP non elaborato tramite l'interfaccia di rete specificata

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_raw_packet_source_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    ULONG destination_ip,
    UINT address_index,
    ULONG type_of_service);
```
### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto IP non elaborato all'indirizzo IP di destinazione usando l'indirizzo IPv4 locale specificato come indirizzo di origine e tramite l'interfaccia di rete associata. Si noti che questa routine restituisce immediatamente e pertanto non è noto se il pacchetto IP è stato effettivamente inviato. Il driver di rete sarà responsabile del rilascio del pacchetto al termine della trasmissione. Questo servizio è diverso da altri servizi in quanto non è possibile sapere se il pacchetto è stato effettivamente inviato. Potrebbe perdersi in Internet.

> [!CAUTION]  
> *Si noti che l'elaborazione IP non elaborata deve essere abilitata.*

> [!WARNING]  
> *Questo servizio è simile a **nx_ip_raw_packet_send,*** ad eccezione del fatto che questo servizio consente a un'applicazione di inviare un pacchetto IPv4 non elaborato da un'interfaccia fisica specificata.

### <a name="parameters"></a>Parametri  

- **ip_ptr** Puntatore all'attività IP creata in precedenza.
- **packet_ptr** Puntatore al pacchetto da trasmettere.
- **destination_ip** Indirizzo IP per l'invio del pacchetto.
- **address_index** Indice dell'indirizzo dell'interfaccia su cui inviare il pacchetto.
- **type_of_service** Tipo di servizio per il pacchetto.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Il pacchetto è stato trasmesso correttamente.
- **NX_IP_ADDRESS_ERROR** (0x21) Nessuna interfaccia in uscita adatta disponibile.
- **NX_NOT_ENABLED** (0x14) L'elaborazione di pacchetti IP non elaborati non è abilitata.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Input puntatore non valido.
- **NX_OPTION_ERROR** (0x0A) Specificato tipo di servizio non valido.
- **NX_OVERFLOW** (0x03) Puntatore anteposto pacchetto non valido.
- **NX_UNDERFLOW** (0x02) Puntatore anteposto pacchetto non valido.
- **NX_INVALID_INTERFACE** (0x4C) Indice di interfaccia non valido specificato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define ADDRESS_IDNEX 1

/* Send packet out on interface 1 with normal type of service. */
status = nx_ip_raw_packet_source_send(ip_ptr, packet_ptr,
                                      destination_ip,
                                      ADDRESS_INDEX,
                                      NX_IP_NORMAL);

/* If status is NX_SUCCESS the packet was successfully
   transmitted. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_raw_receive_queue_max_set"></a>nx_ip_raw_receive_queue_max_set
Impostare le dimensioni massime della coda di ricezione non elaborata

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_raw_receive_queue_max_set(
    NX_IP *ip_ptr, 
    ULONG queue_max);
```
### <a name="description"></a>Descrizione

Questo servizio configura la profondità massima della coda di ricezione di pacchetti non elaborati IP. Si noti che la coda di ricezione di pacchetti non elaborati IP è condivisa con i pacchetti IPv4 e IPv6. Quando la coda di ricezione di pacchetti non elaborati raggiunge la profondità massima configurata dall'utente, i pacchetti non elaborati appena ricevuti vengono eliminati. La profondità predefinita della coda di ricezione pacchetti non elaborati IP è 20.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP
- **queue_max** Nuovo valore per le dimensioni della coda

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Impostare correttamente la profondità massima della coda di ricezione non elaborata
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
ULONG queue_max = 10;

/* Set the maximum size of the IP raw packet receive queue. */
status = nx_ip_raw_receive_queue_max_set (&ip_0,
                                          queue_max);

/* If status == NX_SUCCESS, the maximum size of the IP raw packet
   receive queue was successfully set. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nxd_ip_raw_packet_send
- nxd_ip_raw_packet_source_send

## <a name="nx_ip_static_route_add"></a>nx_ip_static_route_add
Aggiungere una route statica alla tabella di routing

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_static_route_add(
    NX_IP *ip_ptr,
    ULONG network_address,
    ULONG net_mask,
    ULONG next_hop);
```
### <a name="description"></a>Descrizione

Questo servizio aggiunge una voce alla tabella di routing statico. Si noti che *next_hop'indirizzo* deve essere direttamente accessibile da uno dei dispositivi di rete locale.

> [!CAUTION]  
> Si noti ip_ptr deve puntare a una struttura IP di NetX Duo valida e che la libreria NetX Duo deve essere compilata con NX_ENABLE_IP_STATIC_ROUTING definito per *usare questo servizio. Per impostazione predefinita, NetX Duo viene compilato senza NX_ENABLE_IP_STATIC_ROUTING definito.*

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

```c
/* Specify the next hop for 192.168.1.68 through the gateway
   192.168.1.1. */
status = nx_ip_static_route_add(ip_ptr, IP_ADDRESS(192,168,1,0),
                                0xFFFFFF00UL,
                                IP_ADDRESS(192,168,1,1));

/* If status is NX_SUCCESS the route was successfully added to the
   static routing table. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nx_ip_static_route_delete"></a>nx_ip_static_route_delete
Eliminare una route statica dalla tabella di routing

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ip_static_route_delete(
    NX_IP *ip_ptr,
    ULONG network_address,
    ULONG net_mask);
```
### <a name="description"></a>Descrizione

Questo servizio elimina una voce dalla tabella di routing statico.

> [!WARNING]  
> Si noti ip_ptr deve puntare a una struttura IP di NetX Duo valida e che la libreria NetX Duo deve essere compilata con NX_ENABLE_IP_STATIC_ROUTING definito per *usare questo servizio. Per impostazione predefinita, NetX Duo viene compilato senza NX_ENABLE_IP_STATIC_ROUTING definito.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **network_address** Indirizzo di rete di destinazione, in ordine di byte host.
- **net_mask** Destinazione network mask, nell'ordine dei byte dell'host.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Eliminazione riuscita dalla tabella di routing statica.
- **NX_NOT_SUCCESSFUL** (0x43) Impossibile trovare la voce nella tabella di routing.
- **NX_NOT_SUPPORTED** (0x4B) Questa funzionalità non viene compilata in .
- **NX_PTR_ERROR** (0x07) Puntatore ip_ptr non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Remove the static route for 192.168.1.68 from the routing
   table.*/
status = nx_ip_static_route_delete(ip_ptr,
                                   IP_ADDRESS(192,168,1,0),
                                   0xFFFFFF00UL,);

/* If status is NX_SUCCESS the route was successfully removed from
   the static routing table. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nx_ip_status_check"></a>nx_ip_status_check
Controllare lo stato di un'istanza IP

### <a name="prototype"></a>Prototipo  

```c
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
- **needed_status** Lo stato IP richiesto, definito nel formato mappa di bit come indicato di seguito:
  - **NX_IP_INITIALIZE_DONE** (0x0001)
  - **NX_IP_ADDRESS_RESOLVED** (0x0002)
  - **NX_IP_LINK_ENABLED** (0x0004)
  - **NX_IP_ARP_ENABLED** (0x0008)
  - **NX_IP_UDP_ENABLED** (0x0010)
  - **NX_IP_TCP_ENABLED** (0x0020)
  - **NX_IP_IGMP_ENABLED** (0x0040)
  - **NX_IP_RARP_COMPLETE** (0x0080)
  - **NX_IP_INTERFACE_LINK_ENABLED** (0x0100)
- **actual_status** Puntatore alla destinazione dei bit effettivi impostati.
- **wait_option** Definisce il comportamento del servizio se i bit di stato richiesti non sono disponibili. Le opzioni di attesa sono definite come segue:
  - **NX_NO_WAIT** 0x00000000)
  - **valore di timeout in tick** (da 0x00000001 a 0xFFFFFFFE)
  - **NX_WAIT_FOREVER** 0xFFFFFFFF

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Controllo dello stato IP riuscito.
- **NX_NOT_SUCCESSFUL** richiesta di stato (0x43) non è stata soddisfatta entro il timeout specificato.
- **NX_PTR_ERROR** puntatore IP (0x07) è o è diventato non valido oppure il puntatore di stato effettivo non è valido.
- **NX_OPTION_ERROR** (0x0a) Stato necessario non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Wait 10 ticks for the link up status on the previously created IP
   instance. */
status = nx_ip_status_check(&ip_0, NX_IP_LINK_ENABLED,
                            &actual_status, 10);

/* If status is NX_SUCCESS, the link for the specified IP instance
   is up. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_ipv4_multicast_interface_join"></a>nx_ipv4_multicast_interface_join
Aggiungere un'istanza IP a un gruppo multicast specificato tramite un'interfaccia

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ipv4_multicast_interface_join(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio aggiunge un'istanza IP al gruppo multicast specificato tramite un'interfaccia di rete specificata. Quando l'istanza IP viene aggiunta a un gruppo multicast, la logica di ricezione IP inizia a inoltrare i pacchetti di dati dal gruppo di assegnazione multicast al livello superiore. Si noti che questo servizio aggiunge un gruppo multicast senza inviare report IGMP.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **group_address** Indirizzo del gruppo multicast IP di classe D da aggiungere nell'ordine dei byte dell'host.
- **interface_index** Indice dell'interfaccia collegata all'istanza di NetX Duo.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Join a gruppi multicast riuscito.
- **NX_NO_MORE_ENTRIES** (0x17) Non è possibile aggiungere altri gruppi multicast, il massimo è stato superato.
- **NX_PTR_ERROR** (0x07) Puntatore non valido all'istanza IP oppure l'istanza IP non è valida
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_EANABLED** IGMP (0x14) non è abilitato in questa istanza IP
- **NX_IP_ADDRESS_ERROR** indirizzo del gruppo multicast (0x21) specificato non è un indirizzo di classe D valido.
- **NX_INVALID_INTERFACE** (0x4C) L'indice del dispositivo punta a un'interfaccia di rete non valida.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Previously created IP Instance joins the multicast group
   224.0.0.200, via the interface at index 1 in the IP interface
   list. */
#define INTERFACE_INDEX 1
status = nx_ipv4_multicast_interface_join
                                 (&ip IP_ADDRESS(224,0,0,200),
                                  INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully joined
   the multicast group. */
```
### <a name="see-also"></a>Vedere anche

- nx_igmp_enable
- nx_igmp_info_getnx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_ipv4_multicast_interface_leave"></a>nx_ipv4_multicast_interface_leave
Lasciare il gruppo multicast specificato tramite un'interfaccia

### <a name="prototype"></a>Prototipo  

```c
UINT nx_ipv4_multicast_interface_leave(
    NX_IP *ip_ptr,
    ULONG group_address,
    UINT interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio lascia il gruppo multicast specificato tramite un'interfaccia di rete specificata. Dopo aver lasciato il gruppo, questo servizio non attiva la generazione di messaggi IGMP.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **group_address** Indirizzo del gruppo multicast IP di classe D da lasciare. L'indirizzo IP è in ordine di byte host.
- **interface_index** Indice dell'interfaccia associata all'istanza di NetX Duo.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Aggiunta al gruppo multicast riuscita.
- **NX_ENTRY_NOT_FOUND** (0x16) Impossibile trovare l'indirizzo del gruppo multicast specificato nella tabella multicast locale.
- **NX_INVALID_INTERFACE** (0x4C) L'indice del dispositivo punta a un'interfaccia di rete non valida.
- **NX_IP_ADDRESS_ERROR** (0x21) l'indirizzo del gruppo multicast specificato non è un indirizzo di classe D valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Puntatore non valido all'istanza IP oppure l'istanza IP non è valida

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Leave the multicast group 224.0.0.200. */
#define INTERFACE_INDEX 1
status = nx_ipv4_multicast_interface_leave
                                (&ip, IP_ADDRESS(224,0,0,200),
                                 INTERFACE_INDEX);

/* If status is NX_SUCCESS, the IP instance has successfully leaves
   the multicast group 244.0.0.200. */
```
### <a name="see-also"></a>Vedere anche

- nx_igmp_enable
- nx_igmp_info_get
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nxd_ipv6_multicast_interface_join
- nxd_ipv6_multicast_interface_leave

## <a name="nx_packet_allocate"></a>nx_packet_allocate
Allocare il pacchetto dal pool specificato

### <a name="prototype"></a>Prototipo  

```c
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
- **packet_ptr** Puntatore al puntatore del puntatore del pacchetto allocato.
- **packet_type** Definisce il tipo di pacchetto richiesto. Per un elenco dei tipi di pacchetti supportati, vedere "Pool di pacchetti" a pagina 63 nel capitolo 3.
- **wait_option** Definisce il tempo di attesa in tick se non sono disponibili pacchetti nel pool di pacchetti. Le opzioni di attesa sono definite nel modo seguente:
  - **NX_NO_WAIT** (0x00000000)
  - **NX_WAIT_FOREVER** (0xFFFFFFFF)
  - **valore di timeout nei tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) L'allocazione dei pacchetti è riuscita.
- **NX_NO_PACKET** (0x01) Nessun pacchetto disponibile.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_INVALID_PARAMETERS** (0x4D) Le dimensioni del pacchetto non supportano il protocollo.
- **NX_OPTION_ERROR** (0x0A) Tipo di pacchetto non valido.
- **NX_PTR_ERROR** (0x07) Pool o puntatore restituito pacchetto non valido.
- **NX_CALLER_ERROR** (0x11) Opzione di attesa non valida da non thread.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR (driver di rete dell'applicazione). L'opzione wait deve *essere NX_NO_WAIT* se usata in ISR o nel contesto del timer.

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Allocate a new UDP packet from the previously created packet pool
   and suspend for a maximum of 5 timer ticks if the pool is
   empty. */
status = nx_packet_allocate(&pool_0, &packet_ptr,
                            NX_UDP_PACKET, 5);

/* If status is NX_SUCCESS, the newly allocated packet pointer is
   found in the variable packet_ptr. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_copy"></a>nx_packet_copy
Copiare un pacchetto

### <a name="prototype"></a>Prototipo  

```c
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
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **valore di timeout nei tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Copia del pacchetto completata.
- **NX_NO_PACKET** (0x01) Pacchetto non disponibile per la copia.
- **NX_INVALID_PACKET** (0x12) Pacchetto di origine vuoto o copia non riuscita.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_INVALID_PARAMETERS** (0x4D) Le dimensioni del pacchetto non supportano il protocollo.
- **NX_PTR_ERROR** (0x07) Pool, pacchetto o puntatore di destinazione non valido.
- **NX_UNDERFLOW** (0x02) Puntatore anteposto pacchetto non valido.
- **NX_OVERFLOW** (0x03) Puntatore di accodamento di pacchetti non valido.
- **NX_CALLER_ERROR** (0x11) È stata specificata un'opzione di attesa nell'inizializzazione o in un ISR.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
NX_PACKET *new_copy_ptr;

/* Copy packet pointed to by "old_packet_ptr" using packets from
   previously created packet pool_0. */
status = nx_packet_copy(old_packet, &new_copy_ptr, &pool_0, 20);

/* If status is NX_SUCCESS, new_copy_ptr points to the packet copy. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_data_append"></a>nx_packet_data_append
Accodare dati alla fine del pacchetto

### <a name="prototype"></a>Prototipo  

```c
UINT nx_packet_data_append(
    NX_PACKET *packet_ptr,
    VOID *data_start, ULONG data_size,
    NX_PACKET_POOL *pool_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio aggiunge i dati alla fine del pacchetto specificato. L'area dati fornita viene copiata nel pacchetto. Se la memoria disponibile non è sufficiente e la funzionalità dei pacchetti concatenati è abilitata, verranno allocati uno o più pacchetti per soddisfare la richiesta. Se la funzionalità dei pacchetti concatenati non è abilitata, *NX_SIZE_ERROR* viene restituito .

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto.
- **data_start** Puntatore all'inizio dell'area dati dell'utente da aggiungere al pacchetto.
- **data_size** Dimensioni dell'area dati dell'utente.
- **pool_ptr** Puntatore al pool di pacchetti da cui allocare un altro pacchetto se lo spazio nel pacchetto corrente non è sufficiente.
- **wait_option** Definisce il comportamento del servizio se non sono disponibili pacchetti. Le opzioni di attesa sono definite come segue:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **valore di timeout in tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Aggiunta pacchetti riuscita.
- **NX_NO_PACKET** (0x01) Nessun pacchetto disponibile.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
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

```c
/* Append "abcd" to the specified packet. */
status = nx_packet_data_append(packet_ptr, "abcd", 4, &pool_0, 5);

/* If status is NX_SUCCESS, the additional four bytes "abcd" have
   been appended to the packet. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release


## <a name="nx_packet_data_extract_offset"></a>nx_packet_data_extract_offset
Estrarre dati dal pacchetto tramite un offset

### <a name="prototype"></a>Prototipo  

```c
UINT nx_packet_data_extract_offset(
    NX_PACKET *packet_ptr,
    ULONG offset,
    VOID *buffer_start,
    ULONG buffer_length,
    ULONG *bytes_copied);
```
### <a name="description"></a>Descrizione

Questo servizio copia i dati da un pacchetto NetX Duo (o catena di pacchetti) a partire dall'offset specificato dal puntatore anteposto al pacchetto della dimensione specificata in byte nel buffer specificato. Il numero di byte effettivamente copiati viene restituito in *bytes_copied.* Questo servizio non rimuove i dati dal pacchetto né regola il puntatore anteposto o altre informazioni sullo stato interno.

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

```c
/* Extract 10 bytes from the start of the received packet buffer
   into the specified memory area. */
status = nx_packet_data_extract_offset(my_packet, 0, &data[0], 10,
                                       &bytes_copied) ;
/* If status is NX_SUCCESS, 10 bytes were successfully copied into
   the data buffer. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_data_retrieve"></a>nx_packet_data_retrieve
Recuperare dati dal pacchetto

### <a name="prototype"></a>Prototipo  

```c
UINT nx_packet_data_retrieve(
    NX_PACKET *packet_ptr,
    VOID *buffer_start,
    ULONG *bytes_copied);
```
### <a name="description"></a>Descrizione

Questo servizio copia i dati dal pacchetto fornito nel buffer fornito. Il numero effettivo di byte copiati viene restituito nella destinazione a cui punta **bytes_copied**.

Si noti che questo servizio non modifica lo stato interno del pacchetto. I dati recuperati sono ancora disponibili nel pacchetto. 

> [!CAUTION]  
> *Il buffer di destinazione deve essere sufficientemente grande da contenere il contenuto del pacchetto. In caso contrario, la memoria verrà danneggiata causando risultati imprevedibili.*

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto di origine.
- **buffer_start** Puntatore all'inizio dell'area del buffer.
- **bytes_copied** Puntatore alla destinazione per il numero di byte copiati.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Recupero dei dati del pacchetto riuscito.
- **NX_INVALID_PACKET** (0x12) Pacchetto non valido.
- **NX_PTR_ERROR** (0x07) Puntatore non valido per il pacchetto, l'avvio del buffer o i byte copiati.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
UCHAR                 buffer[512];
ULONG                 bytes_copied;

/* Retrieve data from packet pointed to by "packet_ptr". */
status = nx_packet_data_retrieve(packet_ptr, buffer, &bytes_copied);

/* If status is NX_SUCCESS, buffer contains the contents of the
   packet, the size of which is contained in "bytes_copied." */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_length_get"></a>nx_packet_length_get
Ottenere la lunghezza dei dati dei pacchetti

### <a name="prototype"></a>Prototipo  

```c
UINT nx_packet_length_get(
    NX_PACKET *packet_ptr, 
    ULONG *length);
```
### <a name="description"></a>Descrizione

Questo servizio ottiene la lunghezza dei dati nel pacchetto specificato.

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto.
- **lunghezza** Destinazione per la lunghezza del pacchetto.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Ottiene la lunghezza del pacchetto riuscita.
- **NX_PTR_ERROR** (0x07) Puntatore a pacchetto non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Get the length of the data in "my_packet." */
status = nx_packet_length_get(my_packet, &my_length);

/* If status is NX_SUCCESS, data length is in "my_length". */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_pool_create"></a>nx_packet_pool_create
Creare un pool di pacchetti nell'area di memoria specificata

### <a name="prototype"></a>Prototipo  

```c
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

```c
/* Create a packet pool of 32000 bytes starting at physical
   address 0x10000000. */
status = nx_packet_pool_create(&pool_0, "Default Pool", 128,
                               (void *) 0x10000000, 32000);

/* If status is NX_SUCCESS, the packet pool has been successfully
   created. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_pool_delete"></a>nx_packet_pool_delete
Eliminare il pool di pacchetti creato in precedenza

### <a name="prototype"></a>Prototipo  

```c
UINT  nx_packet_pool_delete(NX_PACKET_POOL *pool_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina un pool di pacchetti creato in precedenza. NetX Duo verifica la presenza di thread attualmente sospesi sui pacchetti nel pool di pacchetti e cancella la sospensione.

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

```c
/* Delete a previously created packet pool. */
status = nx_packet_pool_delete(&pool_0);

/* If status is NX_SUCCESS, the packet pool has been successfully
   deleted. */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_pool_info_get"></a>nx_packet_pool_info_get
Recuperare informazioni su un pool di pacchetti

### <a name="prototype"></a>Prototipo  

```c
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

> [!IMPORTANT]  
> *Se un puntatore di destinazione NX_NULL, queste informazioni specifiche non vengono restituite al chiamante.*

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

```c
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

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_low_watermark_set
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_pool_low_watermark_set"></a>nx_packet_pool_low_watermark_set
Impostare il limite minimo del pool di pacchetti

### <a name="prototype"></a>Prototipo  

```c
UINT nx_packet_pool_low_watermark_set(
    NX_PACKET_POOL *pool_ptr,
    ULONG low_watermark);
```
### <a name="description"></a>Descrizione

Questo servizio configura il limite basso per il pool di pacchetti specificato. Dopo aver impostato il valore limite basso, TCP o UDP non accoderà i pacchetti ricevuti se il numero di pacchetti disponibili nel pool di pacchetti è inferiore al limite basso del pool di pacchetti, impedendo al pool di pacchetti di essere affamato di pacchetti. Questo servizio è disponibile se la libreria NetX Duo viene compilata con ***l'opzione NX_ENABLE_LOW_WATERMARK*** definita.

### <a name="parameters"></a>Parametri

- **pool_ptr** Puntatore al blocco di controllo del pool di pacchetti.
- **low_watermark** Valore limite basso da configurare

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Impostare correttamente il valore limite basso.
- **NX_NOT_SUPPORTED** (0x4B) La funzionalità limite basso non è incorporata in NetX Duo.
- **NX_PTR_ERROR** (0x07) Puntatore del pool non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Set pool_0 low watermark value to 2. */
status = nx_packet_pool_create(&pool_0, 2);

/* If status is NX_SUCCESS, the low watermark value is set for
   pool_0.*/
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_release
- nx_packet_transmit_release

## <a name="nx_packet_release"></a>nx_packet_release
Rilasciare un pacchetto allocato in precedenza

### <a name="prototype"></a>Prototipo  

```c
UINT nx_packet_release(NX_PACKET *packet_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio rilascia un pacchetto, inclusi eventuali pacchetti aggiuntivi concatenati al pacchetto specificato. Se un altro thread viene bloccato all'allocazione dei pacchetti, il pacchetto viene assegnato e ripreso.

> [!NOTE]  
> *L'applicazione deve impedire il rilascio di un pacchetto più di una volta, perché questa operazione causerà risultati imprevedibili.*

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Rilascio pacchetti riuscito.
- **NX_PTR_ERROR** (0x07) Puntatore a pacchetto non valido.
- **NX_UNDERFLOW** (0x02) Il puntatore anteposto è minore dell'inizio del payload.
- **NX_OVERFLOW** (0x03) Il puntatore Append è maggiore dell'estremità del payload.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR (driver di rete dell'applicazione)

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```c
/* Release a previously allocated packet. */
status = nx_packet_release(packet_ptr);

/* If status is NX_SUCCESS, the packet has been returned to the
   packet pool it was allocated from. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_transmit_release

## <a name="nx_packet_transmit_release"></a>nx_packet_transmit_release
Rilasciare un pacchetto trasmesso

### <a name="prototype"></a>Prototipo  

```c
UINT nx_packet_transmit_release(NX_PACKET *packet_ptr);
```
### <a name="description"></a>Descrizione

Per i pacchetti non TCP, questo servizio rilascia un pacchetto trasmesso, inclusi eventuali pacchetti aggiuntivi concatenati al pacchetto specificato. Se un altro thread viene bloccato all'allocazione dei pacchetti, il pacchetto viene assegnato e ripreso. Per un pacchetto TCP trasmesso, il pacchetto viene contrassegnato come trasmesso ma non rilasciato fino a quando il pacchetto non viene riconosciuto. Questo servizio viene in genere chiamato dal driver di rete dell'applicazione dopo la trasmissione di un pacchetto.

> [!WARNING] 
> *Il driver di rete deve rimuovere l'intestazione del supporto fisico e regolare la lunghezza del pacchetto prima di chiamare questo servizio*.

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

```c
/* Release a previously allocated packet that was just transmitted
   from the application network driver. */
status = nx_packet_transmit_release(packet_ptr);

/* If status is NX_SUCCESS, the transmitted packet has been
   returned to the packet pool it was allocated from. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_packet_allocate
- nx_packet_copy
- nx_packet_data_append
- nx_packet_data_extract_offset
- nx_packet_data_retrieve
- nx_packet_length_get
- nx_packet_pool_create
- nx_packet_pool_delete
- nx_packet_pool_info_get
- nx_packet_pool_low_watermark_set
- nx_packet_release

## <a name="nx_rarp_disable"></a>nx_rarp_disable
Disabilitare RARP (Reverse Address Resolution Protocol)

### <a name="prototype"></a>Prototipo  

```c
UINT nx_rarp_disable(NX_IP *ip_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio disabilita il componente RARP di NetX Duo per l'istanza IP specifica. Per un sistema multihome, questo servizio disabilita RARP in tutte le interfacce.

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

```c
/* Disable RARP on the previously created IP instance. */
status = nx_rarp_disable(&ip_0);

/* If status is NX_SUCCESS, RARP is disabled. */
```
### <a name="see-also"></a>Vedere anche

- nx_rarp_enable
- nx_rarp_info_get

## <a name="nx_rarp_enable"></a>nx_rarp_enable
Abilitare RARP (Reverse Address Resolution Protocol)

### <a name="prototype"></a>Prototipo  

```c
UINT nx_rarp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio abilita il componente RARP di NetX Duo per l'istanza IP specifica. I componenti RARP cerca in tutte le interfacce di rete collegate l'indirizzo IP zero. Un indirizzo IP zero indica che l'interfaccia non ha ancora un'assegnazione di indirizzo IP. RARP tenta di risolvere l'indirizzo IP abilitando il processo RARP su tale interfaccia.

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

```c
/* Enable RARP on the previously created IP instance. */
status = nx_rarp_enable(&ip_0);

/* If status is NX_SUCCESS, RARP is enabled and is attempting to
   resolve this IP instance’s address by querying the network. */
```
### <a name="see-also"></a>Vedere anche

- nx_rarp_disable
- nx_rarp_info_get

## <a name="nx_rarp_info_get"></a>nx_rarp_info_get
Recuperare informazioni sulle attività RARP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_rarp_info_get(
    NX_IP *ip_ptr,
    ULONG *rarp_requests_sent,
    ULONG *rarp_responses_received,
    ULONG *rarp_invalid_messages);
```
### <a name="description"></a>Descrizione

Questo servizio recupera informazioni sulle attività RARP per l'istanza IP specificata.

> [!IMPORTANT]  
> *Se viene utilizzato un puntatore NX_NULL destinazione, le informazioni specifiche non vengono restituite al chiamante.*

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

```c
/* Retrieve RARP information from previously created IP
   Instance 0. */
status = nx_rarp_info_get(&ip_0,
                          &rarp_requests_sent,
                          &rarp_responses_received,
                          &rarp_invalid_messages);

/* If status is NX_SUCCESS, RARP information was retrieved. */
```
### <a name="see-also"></a>Vedere anche

- nx_rarp_disable
- nx_rarp_enable

## <a name="nx_system_initialize"></a>nx_system_initialize
Inizializzare il sistema NetX Duo

### <a name="prototype"></a>Prototipo  

```c
VOID nx_system_initialize(VOID);
```
### <a name="description"></a>Descrizione

Questo servizio inizializza le risorse di sistema NetX Duo di base in preparazione all'uso. Deve essere chiamato dall'applicazione durante l'inizializzazione e prima che venga effettuata qualsiasi altra chiamata a NetX Duo.

### <a name="parameters"></a>Parametri

nessuno

### <a name="return-values"></a>Valori restituiti

Nessuno

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer, ISR

### <a name="preemption-possible"></a>Preemption Possible

No

Gestione dei sistemi

### <a name="example"></a>Esempio

```c
/* Initialize NetX Duo for operation. */
nx_system_initialize();

/* At this point, NetX Duo is ready for IP creation and all
   subsequent network operations. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nx_tcp_client_socket_bind"></a>nx_tcp_client_socket_bind
Associare il socket TCP del client alla porta TCP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_client_socket_bind(
    NX_TCP_SOCKET *socket_ptr,
    UINT port,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio associa il socket client TCP creato in precedenza alla porta TCP specificata. I socket TCP validi sono compreso tra 0 e 0xFFFF. Se la porta TCP specificata non è disponibile, il servizio viene sospeso in base all'opzione di attesa fornita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP creata in precedenza.
- **numero di porta** da associare (da 1 a 0xFFFF). Se il numero di porta NX_ANY_PORT (0x0000), l'istanza IP cerca la porta libera successiva e la usa per l'associazione.
- **wait_option** Definisce il comportamento del servizio se la porta è già associata a un altro socket. Le opzioni di attesa sono definite come segue:
- **NX_NO_WAIT** (0x00000000)
- **NX_WAIT_FOREVER** (0xFFFFFFFF)
- **valore di timeout in tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Associazione socket riuscita.
- **NX_ALREADY_BOUND** (0x22) Questo socket è già associato a un'altra porta TCP.
- **NX_PORT_UNAVAILABLE** porta (0x23) è già associata a un socket diverso.
- **NX_NO_FREE_PORTS** (0x45) Nessuna porta disponibile.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_INVALID_PORT** (0x46) Porta non valida.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Bind a previously created client socket to port 12 and wait for 7
   timer ticks for the bind to complete. */
status = nx_tcp_client_socket_bind(&client_socket, 12, 7);

/* If status is NX_SUCCESS, the previously created client_socket is
   bound to port 12 on the associated IP instance. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_client_socket_connect"></a>nx_tcp_client_socket_connect
Connessione socket TCP del client

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_client_socket_connect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG server_ip,
    UINT server_port,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio connette il socket client TCP creato in precedenza e associato alla porta del server specificato. Le porte del server TCP valide sono da 0 a 0xFFFF. Se la connessione non viene completata immediatamente, il servizio viene sospeso in base all'opzione di attesa fornita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP creata in precedenza.
- **server_ip** Indirizzo IP del server.
- **server_port** Numero di porta del server a cui connettersi** (da 1 a 0xFFFF).
- **wait_option** Definisce il comportamento del servizio mentre viene stabilita la connessione. Le opzioni di attesa sono definite come segue:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **valore di timeout in tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Connessione socket riuscita.
- **NX_NOT_BOUND** (0x24) Socket non è associato.
- **NX_NOT_CLOSED** socket (0x35) non è chiuso.
- **NX_IN_PROGRESS** (0x37) Non è stata specificata alcuna attesa, il tentativo di connessione è in corso.
- **NX_INVALID_INTERFACE** (0x4C) È stata specificata un'interfaccia non valida.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP del server non valido.
- **NX_INVALID_PORT** (0x46) Porta non valida.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Initiate a TCP connection from a previously created and bound
   client socket. The connection requested in this example is to
   port 12 on the server with the IP address of 1.2.3.5. This
   service will wait 300 timer ticks for the connection to take
   place before giving up. */
status = nx_tcp_client_socket_connect(&client_socket,
                                      IP_ADDRESS(1,2,3,5),
                                      12, 300);

/* If status is NX_SUCCESS, the previously created and bound
   client_socket is connected to port 12 on IP 1.2.3.5. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_client_socket_port_get"></a>nx_tcp_client_socket_port_get
Ottenere il numero di porta associato al socket TCP del client

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_client_socket_port_get(
    NX_TCP_SOCKET *socket_ptr,
    UINT *port_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio recupera il numero di porta associato al socket, utile per trovare la porta allocata da NetX Duo nelle situazioni in cui il NX_ANY_PORT è stato specificato al momento dell'associazione del socket.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP creata in precedenza.
- **port_ptr** Puntatore alla destinazione per il numero di porta restituito. I numeri di porta validi sono (da 1 a 0xFFFF).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Associazione socket riuscita.
- **NX_NOT_BOUND** (0x24) Questo socket non è associato a una porta.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido o puntatore di porta restituito.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Get the port number of previously created and bound client
   socket. */
status = nx_tcp_client_socket_port_get(&client_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
   socket is bound to. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_client_socket_unbind"></a>nx_tcp_client_socket_unbind
Disassociare il socket client TCP dalla porta TCP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_client_socket_unbind(NX_TCP_SOCKET *socket_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio rilascia l'associazione tra il socket client TCP e una porta TCP. Se sono presenti altri thread in attesa di associare un altro socket allo stesso numero di porta, il primo thread sospeso viene quindi associato a questa porta.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP creata in precedenza.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Socket completato.
- **NX_NOT_BOUND** (0x24) Socket non è stato associato ad alcuna porta.
- **NX_NOT_CLOSED** socket (0x35) non è stato disconnesso.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

Sì

### <a name="example"></a>Esempio

```c
/* Unbind a previously created and bound client TCP socket. */
status = nx_tcp_client_socket_unbind(&client_socket);

/* If status is NX_SUCCESS, the client socket is no longer
   bound. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_enable"></a>nx_tcp_enable
Abilitare il componente TCP di NetX Duo

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio abilita il Transmission Control Protocol (TCP) di NetX Duo. Dopo l'abilito, le connessioni TCP possono essere stabilite dall'applicazione.

### <a name="parameters"></a>Parametri  

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) TCP riuscito.
- **NX_ALREADY_ENABLED** tcp (0x15) è già abilitato.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Enable TCP on a previously created IP instance ip_0. */
status = nx_tcp_enable(&ip_0);

/* If status is NX_SUCCESS, TCP is enabled on the IP instance. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_free_port_find"></a>nx_tcp_free_port_find
Trovare la porta TCP successiva disponibile

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_free_port_find(
    NX_IP *ip_ptr,
    UINT port,
    UINT *free_port_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio tenta di individuare una porta TCP libera (non in ingresso) a partire dalla porta fornita dall'applicazione. La logica di ricerca va a capo se la ricerca raggiunge il valore massimo della porta 0xFFFF. Se la ricerca ha esito positivo, la porta libera viene restituita nella variabile a cui punta *free_port_ptr*.

> [!WARNING]  
> *Questo servizio può essere chiamato da un altro thread e restituire la stessa porta. Per evitare questo race condition,* l'applicazione potrebbe voler inserire questo servizio e l'effettiva associazione socket client sotto la protezione di un mutex.

### <a name="parameters"></a>Parametri  

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **porta** Numero di porta da cui iniziare la ricerca (da 1 a 0xFFFF).
- **free_port_ptr** Puntatore al valore restituito della porta libera di destinazione.

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

```c
/* Locate a free TCP port, starting at port 12, on a previously
   created IP instance. */
status = nx_tcp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS, "free_port" contains the next free port
   on the IP instance. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_info_get"></a>nx_tcp_info_get
Recuperare informazioni sulle attività TCP

### <a name="prototype"></a>Prototipo  

```c
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

> [!IMPORTANT]  
> *Se viene utilizzato un puntatore NX_NULL destinazione, le informazioni specifiche non vengono restituite al chiamante.*

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

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Retrieve TCP information from previously created IP Instance
   ip_0. */
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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_server_socket_accept"></a>nx_tcp_server_socket_accept
Accettare la connessione TCP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_server_socket_accept(
    NX_TCP_SOCKET *socket_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio accetta (o si prepara ad accettare) una richiesta di connessione socket client TCP per una porta precedentemente impostata per l'ascolto. Questo servizio può essere chiamato immediatamente dopo che l'applicazione chiama il servizio di ascolto o di ascolto oppure dopo che la routine di callback di ascolto viene chiamata quando la connessione client è effettivamente presente. Se non è possibile stabilire subito una connessione, il servizio viene sospeso in base all'opzione di attesa fornita.

> [!WARNING]  
> *L'applicazione deve **nx_tcp_server_socket_unaccept** dopo che la connessione* non è più necessaria per rimuovere l'associazione del socket del server alla porta del server .

> [!IMPORTANT]  
> *Le routine di callback dell'applicazione vengono chiamate dall'interno del thread helper dell'indirizzo IP.*

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al blocco di controllo socket del server TCP.
- **wait_option** Definisce il comportamento del servizio mentre viene stabilita la connessione. Le opzioni di attesa sono definite nel modo seguente:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **valore di timeout nei tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Accettazione socket del server TCP (connessione passiva) riuscita.
- **NX_NOT_LISTEN_STATE** (0x36) Il socket del server fornito non è in stato di ascolto.
- **NX_IN_PROGRESS** (0x37) Non è stata specificata alcuna attesa, il tentativo di connessione è in corso.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_PTR_ERROR** (0x07) Errore del puntatore del socket.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
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
        created
    */

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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_server_socket_listen"></a>nx_tcp_server_socket_listen
Abilitare l'ascolto per la connessione client sulla porta TCP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_server_socket_listen(
    NX_IP *ip_ptr, UINT port,
    NX_TCP_SOCKET *socket_ptr,
    UINT listen_queue_size,
    VOID (*listen_callback)(NX_TCP_SOCKET *socket_ptr, UINT port));
```
### <a name="description"></a>Descrizione

Questo servizio abilita l'ascolto di una richiesta di connessione client sulla porta TCP specificata. Quando viene ricevuta una richiesta di connessione client, il socket del server fornito viene associato alla porta specificata e viene chiamata la funzione di callback di ascolto fornita.

L'elaborazione della routine di callback di ascolto è completamente all'applicazione. Può contenere logica per riattivare un thread dell'applicazione che successivamente esegue un'operazione di accettazione. Se l'applicazione ha già un thread sospeso durante l'elaborazione di accettazione per questo socket, la routine di callback di ascolto potrebbe non essere necessaria.

Se l'applicazione vuole gestire connessioni client aggiuntive sulla stessa porta, il ***nx_tcp_server_socket_relisten*** deve essere chiamato con un socket disponibile (un socket nello stato CLOSED) per la connessione successiva. Fino a quando non viene chiamato il servizio di ri ascolto, vengono accodati ulteriori connessioni client. Quando viene superata la profondità massima della coda, la richiesta di connessione meno recente viene eliminata a favore dell'accodamento della nuova richiesta di connessione. La profondità massima della coda viene specificata da questo servizio.

> [!IMPORTANT]  
> *Le routine di callback dell'applicazione vengono chiamate dal thread helper IP interno.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **porta** Numero di porta su cui restare in ascolto (da 1 a 0xFFFF).
- **socket_ptr** Puntatore al socket da utilizzare per la connessione.
- **listen_queue_size** Numero di richieste di connessione client che possono essere accodati.
- **listen_callback** Funzione dell'applicazione da chiamare quando viene ricevuta la connessione. Se viene specificato un valore NULL, la funzionalità di callback di ascolto è disabilitata.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Abilitare l'ascolto porta TCP riuscita.
- **NX_MAX_LISTEN** (0x33) Non sono disponibili altre strutture di richiesta di ascolto. La costante NX_MAX_LISTEN_REQUESTS in **_nx_api.h_** definisce il numero di richieste di ascolto attive possibili.
- **NX_NOT_CLOSED** (0x35) Il socket del server fornito non è in stato chiuso.
- **NX_ALREADY_BOUND** (0x22) Il socket del server fornito è già associato a una porta.
- **NX_DUPLICATE_LISTEN** (0x34) Esiste già una richiesta di ascolto attiva per questa porta.
- **NX_INVALID_PORT** (0x46) È stata specificata una porta non valida.
- **NX_PTR_ERROR** (0x07) Puntatore IP o socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
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
}
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_server_socket_relisten"></a>nx_tcp_server_socket_relisten
Riascolta la connessione client sulla porta TCP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_server_socket_relisten(
    NX_IP *ip_ptr, 
    UINT port,
    NX_TCP_SOCKET *socket_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio viene chiamato dopo la ricezione di una connessione su una porta precedentemente impostata per l'ascolto. Lo scopo principale di questo servizio è fornire un nuovo socket del server per la connessione client successiva. Se una richiesta di connessione viene accodata, la connessione verrà elaborata immediatamente durante questa chiamata al servizio.

> [!IMPORTANT]  
> *La stessa routine di callback specificata dalla richiesta di ascolto originale* viene chiamata anche quando è presente una connessione per questo nuovo socket del server.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **porta** Numero di porta su cui eseguire nuovamente l'ascolto (da 1 a 0xFFFF).
- **socket_ptr** Socket da usare per la connessione client successiva.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Riascolta porta TCP riuscita.
- **NX_NOT_CLOSED** (0x35) Il socket del server fornito non è in stato chiuso.
- **NX_ALREADY_BOUND** (0x22) Il socket del server fornito è già associato a una porta.
- **NX_INVALID_RELISTEN** (0x47) È già presente un puntatore socket valido per questa porta o la porta specificata non ha una richiesta di ascolto attiva.
- **NX_CONNECTION_PENDING** (0x48) Uguale a NX_SUCCESS, ad eccezione della richiesta di connessione in coda che è stata elaborata durante questa chiamata.
- **NX_INVALID_PORT** (0x46) È stata specificata una porta non valida.
- **NX_PTR_ERROR** (0x07) Ip non valido o puntatore di callback di ascolto.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
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
   nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server Socket",
                                 NX_IP_NORMAL, NX_FRAGMENT_OKAY,
                                 NX_IP_TIME_TO_LIVE, 100,
                                 NX_NULL, port_12_disconnect_request);

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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_server_socket_unaccept"></a>nx_tcp_server_socket_unaccept
Rimuovere l'associazione socket con la porta di ascolto

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_server_socket_unaccept(NX_TCP_SOCKET *socket_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio rimuove l'associazione tra questo socket del server e la porta del server specificata. L'applicazione deve chiamare questo servizio dopo una disconnessione o dopo una chiamata accept non riuscita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket del server precedentemente impostata.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Socket del server non cept riuscito.
- **NX_NOT_LISTEN_STATE** (0x36) Il socket del server si trova in uno stato non corretto e probabilmente non è disconnesso.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
NX_PACKET_POOL        my_pool;
NX_IP                 my_ip;
NX_TCP_SOCKET         server_socket;
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

NX_PACKET  *my_packet;
UINT       status, i;

   /* Assuming that:
     "port_12_semaphore" has already been created with an initial count
      of 0 "my_ip" has already been created and the link is enabled
     "my_pool" packet pool has already been created
   */

    /* Create the server socket. */
    nx_tcp_socket_create(&my_ip, &server_socket, "Port 12 Server
                         Socket",NX_IP_NORMAL, NX_FRAGMENT_OKAY,
                         NX_IP_TIME_TO_LIVE, 100,NX_NULL,
                         port_12_disconnect_request);

    /* Setup server listening on port 12. */
    nx_tcp_server_socket_listen(&my_ip, 12, &server_socket, 5,
                                port_12_connect_request);

    /* Loop to process 5 server connections, sending "Hello_and_Goodbye"
       to
       each client and then disconnecting. */
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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_server_socket_unlisten"></a>nx_tcp_server_socket_unlisten
Disabilitare l'ascolto della connessione client sulla porta TCP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_server_socket_unlisten(
    NX_IP *ip_ptr, 
    UINT port);
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

```c
NX_PACKET_POOL       my_pool;
NX_IP                my_ip;
NX_TCP_SOCKET        server_socket;

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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_bytes_available"></a>nx_tcp_socket_bytes_available
Recupera il numero di byte disponibili per il recupero

### <a name="prototype"></a>Prototipo  

```c
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

```c
/* Get the bytes available for retrieval on the specified socket. */
status = nx_tcp_socket_bytes_available(&my_socket,&bytes_available);

/* Is status = NX_SUCCESS, the available bytes is returned in
   bytes_available. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_create"></a>nx_tcp_socket_create
Creare un socket client o server TCP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_create(
    NX_IP *ip_ptr, 
    NX_TCP_SOCKET *socket_ptr,
    CHAR *name, 
    ULONG type_of_service, 
    ULONG fragment,
    UINT time_to_live, 
    ULONG window_size,
    VOID (*urgent_data_callback)(NX_TCP_SOCKET *socket_ptr),
    VOID (*disconnect_callback)(NX_TCP_SOCKET *socket_ptr));
```
### <a name="description"></a>Descrizione

Questo servizio crea un socket client o server TCP per l'istanza IP specificata.

> [!NOTE]  
> *Le routine di callback dell'applicazione vengono chiamate dal thread associato a questa istanza IP.*

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **socket_ptr** Puntatore al nuovo blocco di controllo socket TCP.
- **name** Nome dell'applicazione per questo socket TCP.
- **type_of_service** Definisce il tipo di servizio per la trasmissione, i valori validi sono i seguenti:
    - **NX_IP_NORMAL** (0x00000000)
    - **NX_IP_MIN_DELAY** (0x00100000)
    - **NX_IP_MAX_DATA** (0x00080000)
    - **NX_IP_MAX_RELIABLE** (0x00040000)
    - **NX_IP_MIN_COST** (0x00020000)
- **frammento** Specifica se è consentita o meno la frammentazione IP. Se NX_FRAGMENT_OKAY** (0x0), la frammentazione IP è consentita. Se NX_DONT_FRAGMENT (0x4000), la frammentazione IP è disabilitata.
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

```c
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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_delete"></a>nx_tcp_socket_delete
Eliminare un socket TCP

### <a name="prototype"></a>Prototipo  

```c
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

```c
/* Delete a previously created TCP client socket. */
status = nx_tcp_socket_delete(&client_socket);

/* If status is NX_SUCCESS, the client socket is deleted. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_disconnect"></a>nx_tcp_socket_disconnect
Disconnettere le connessioni socket client e server

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_disconnect(
    NX_TCP_SOCKET *socket_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio disconnette una connessione socket client o server stabilita. Una disconnessione di un socket del server deve essere seguita da una richiesta non crittografata, mentre un socket client disconnesso viene lasciato in uno stato pronto per un'altra richiesta di connessione. Se il processo di disconnessione non può terminare immediatamente, il servizio viene sospeso in base all'opzione di attesa fornita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket client o server connessa in precedenza.
- **wait_option** Definisce il comportamento del servizio mentre è in corso la disconnessione. Le opzioni di attesa sono definite nel modo seguente:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **valore di timeout nei tick** (da 0x00000001 a 0xFFFFFFFE)

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

```c
/* Disconnect from a previously established connection and wait a
   maximum of 400 timer ticks. */
status = nx_tcp_socket_disconnect(&client_socket, 400);

/* If status is NX_SUCCESS, the previously connected socket (either
   as a result of the client socket connect or the server accept) is
   disconnected. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_disconnect_complete_notify"></a>nx_tcp_socket_disconnect_complete_notify
Installare la funzione di callback di notifica completa disconnessione TCP
 
### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_disconnect_complete_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_disconnect_complete_notify)(NX_TCP_SOCKET *socket_ptr));
```
### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback che viene richiamata dopo il completamento di un'operazione di disconnessione del socket. La funzione di callback di disconnessione completa del socket TCP è disponibile se NetX Duo viene compilato con ***l'opzione NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** definita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket client o server connessa in precedenza.
- **tcp_disconnect_complete_notify** Funzione di callback da installare.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) La funzione di callback è stata registrata correttamente.
- **NX_NOT_SUPPORTED** (0x4B) La funzionalità di notifica estesa non è incorporata nella libreria NetX Duo NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) la funzionalità TCP non è abilitata.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Install the disconnect complete notify callback function. */
status = nx_tcp_socket_disconnect_complete_notify(&client_socket,
                                                  callback);
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_setnx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_establish_notify"></a>nx_tcp_socket_establish_notify
Impostare la funzione di callback di notifica tcp establish

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_establish_notify(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_establish_notify)(NX_TCP_SOCKET *socket_ptr));
```
### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback, che viene chiamata dopo che un socket TCP effettua una connessione. La funzione di callback tcp socket establish è disponibile se NetX Duo viene compilato con ***l'opzione NX_ENABLE_EXTENDED_NOTIFY_SUPPORT*** definita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket client o server connessa in precedenza.
- **tcp_establish_notify** Funzione di callback richiamata dopo che è stata stabilita una connessione TCP.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Imposta correttamente la funzione notify.
- **NX_NOT_SUPPORTED** (0x4B) La funzionalità di notifica estesa non è incorporata nella libreria NetX Duo 
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) TCP non è stato abilitato dall'applicazione.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Set the function pointer "callback" as the notify function NetX
   Duo will call when the connection is in the established state. */
status = nx_tcp_socket_establish_notify(&client_socket, callback);
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_info_get"></a>nx_tcp_socket_info_get
Recuperare informazioni sulle attività socket TCP

### <a name="prototype"></a>Prototipo  

```c
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

> [!NOTE]  
> *Se un puntatore di destinazione NX_NULL, queste informazioni specifiche non vengono restituite al chiamante.*

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

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Retrieve TCP socket information from previously created
   socket_0.*/
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

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_mss_get"></a>nx_tcp_socket_mss_get
Ottenere MSS del socket

### <a name="prototype"></a>Prototipo  

```c
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

- **NX_SUCCESS** (0x00) MSS riuscito.
- **NX_PTR_ERROR** (0x07) Socket o puntatore di destinazione MSS non valido.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitato.
- **NX_CALLER_ERROR** (0x11) Caller non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Get the MSS for the socket "my_socket". */
status = nx_tcp_socket_mss_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
   socket's current MSS value. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_mss_peer_get"></a>nx_tcp_socket_mss_peer_get
Ottenere MSS del socket TCP peer

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_mss_peer_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *mss);
```
### <a name="description"></a>Descrizione

Questo servizio recupera le dimensioni massime del segmento annunciate dal socket peer.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket creato e connesso in precedenza.
- **mss** Destinazione per la restituzione di MSS.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Ottiene MSS peer riuscito.
- **NX_PTR_ERROR** (0x07) Socket o puntatore di destinazione MSS non valido.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitato.
- **NX_CALLER_ERROR** (0x11) Caller non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Get the MSS of the connected peer to the socket "my_socket". */
status = nx_tcp_socket_mss_peer_get(&my_socket, &mss_value);

/* If status is NX_SUCCESS, the "mss_value" variable contains the
   socket peer’s advertised MSS value. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_mss_set"></a>nx_tcp_socket_mss_set
Impostare MSS del socket

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_mss_set(
    NX_TCP_SOCKET *socket_ptr, 
    ULONG mss);
```
### <a name="description"></a>Descrizione

Questo servizio imposta la dimensione massima del segmento (MSS) del socket specificato. Si noti che il valore MSS deve essere all'interno dell'interfaccia di rete MTU IP, consentendo spazio per le intestazioni IP e TCP.

Questo servizio deve essere usato prima che un socket TCP inizi il processo di connessione. Se il servizio viene usato dopo che è stata stabilita una connessione TCP, il nuovo valore non ha alcun effetto sulla connessione.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket creato in precedenza.
- **mss** Valore di MSS da impostare.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) set MSS riuscito.
- **NX_SIZE_ERROR** (0x09) Il valore MSS specificato è troppo grande.
- **NX_NOT_CONNECTED** (0x38) non è stata stabilita una connessione TCP 
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitato.
- **NX_CALLER_ERROR** (0x11) Caller non è un thread o un'inizializzazione.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Set the MSS of the socket "my_socket" to 1000 bytes. */
status = nx_tcp_socket_mss_set(&my_socket, 1000);

/* If status is NX_SUCCESS, the MSS of "my_socket" is 1000 bytes. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_peer_info_get"></a>nx_tcp_socket_peer_info_get
Recuperare informazioni sul socket TCP peer

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_peer_info_get(
    NX_TCP_SOCKET *socket_ptr,
    ULONG *peer_ip_address,
    ULONG *peer_port);
```
### <a name="description"></a>Descrizione

Questo servizio recupera le informazioni sull'indirizzo IP peer e sulla porta per il socket TCP connesso sulla rete IPv4. Il servizio equivalente che supporta anche la rete IPv6 è ***nxd_tcp_socket_peer_info_get.***

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP creato in precedenza.
- **peer_ip_address** Puntatore alla destinazione per l'indirizzo IP peer, nell'ordine dei byte dell'host.
- **peer_port** Puntatore alla destinazione per il numero di porta peer, nell'ordine dei byte dell'host.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) il servizio viene eseguito correttamente. L'indirizzo IP peer e il numero di porta vengono restituiti al chiamante.
- **NX_NOT_CONNECTED** (0x38) Il socket non è in stato connesso.
- **NX_PTR_ERROR** (0x07) Puntatori non validi.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitato.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Obtain peer IP address and port on the specified TCP socket. */
status = nx_tcp_socket_peer_info_get(&my_socket, &peer_ip_address,
                                     &peer_port);

/* If status = NX_SUCCESS, the data was successfully obtained. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_queue_depth_notify_set"></a>nx_tcp_socket_queue_depth_notify_set
Impostare la funzione di notifica della coda di trasmissione TCP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_queue_depth_notify_set(
              NX_TCP_SOCKET *socket_ptr,
              VOID(*tcp_socket_queue_depth_notify)(NX_TCP_SOCKET *));
```
### <a name="description"></a>Descrizione

Questo servizio imposta la funzione di notifica dell'aggiornamento della profondità della coda di trasmissione specificata dall'applicazione, che viene chiamata ogni volta che il socket specificato determina che ha rilasciato pacchetti dalla coda di trasmissione in modo che la profondità della coda non superi più il limite. Se un'applicazione viene bloccata durante la trasmissione a causa della profondità della coda, la funzione di callback funge da notifica all'applicazione che potrebbe avviare nuovamente la trasmissione. Questo servizio è disponibile solo se la libreria NetX Duo viene compilata con ***l'opzione NX_ENABLE_TCP_QUEUE_DEPTH_UPDATE_NOTIFY*** definita.

### <a name="parameters"></a>Parametri 

- **socket_ptr** Puntatore alla struttura del socket 
- **tcp_socket_queue_depth_notify** Funzione notify da installare

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) La funzione notify è stata installata correttamente
- **NX_NOT_SUPPORTED** (0x4B) La funzionalità di notifica della profondità della coda del socket TCP non è incorporata nella libreria NetX Duo
- **NX_PTR_ERROR** (0x07) Puntatore non valido al blocco di controllo socket o alla funzione notify
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitata.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
VOID tcp_socket_queue_depth_notify(NX_TCP_SOCKET *socket_ptr)
{
   /* Notify the application to resume sending. */

}
/* Install the TCP transmit queue notify function .*/
status = nxd_tcp_socket_queue_depth_notify_set(&tcp_socket,
                                  tcp_socket_queue_depth_notify);

/* If status == NX_SUCCESS, the callback function is successfully
   installed. */
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_receive"></a>nx_tcp_socket_receive
Ricevere dati dal socket TCP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_receive(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio riceve i dati TCP dal socket specificato. Se nessun dato viene accodato nel socket specificato, il chiamante viene sospeso in base all'opzione di attesa fornita.

> [!CAUTION]  
> *Se NX_SUCCESS viene restituito , l'applicazione* è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP creata in precedenza.
- **packet_ptr** Puntatore al puntatore al pacchetto TCP.
- **wait_option** Definisce il comportamento del servizio se i dati vengono attualmente accodati in questo socket. Le opzioni di attesa sono definite come segue:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **valore di timeout in tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Ricezione di dati socket riuscita.
- **NX_NOT_BOUND** (0x24) Socket non è ancora associato.
- **NX_NO_PACKET** (0x01) Nessun dato ricevuto.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_NOT_CONNECTED** (0x38) Il socket non è più connesso.
- **NX_PTR_ERROR** (0x07) Socket non valido o puntatore a pacchetto restituito.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Receive a packet from the previously created and connected TCP
   client socket. If no packet is available, wait for 200 timer
   ticks before giving up. */
status = nx_tcp_socket_receive(&client_socket, &packet_ptr, 200);

/* If status is NX_SUCCESS, the received packet is pointed to by
   "packet_ptr". */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_receive_notify"></a>nx_tcp_socket_receive_notify
Notificare all'applicazione i pacchetti ricevuti

### <a name="prototype"></a>Prototipo   

```c
UINT nx_tcp_socket_receive_notify(
    NX_TCP_SOCKET *socket_ptr, 
    VOID (*tcp_receive_notify)(NX_TCP_SOCKET *socket_ptr));
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

```c
/* Setup a receive packet callback function for the "client_socket"
   socket. */
status = nx_tcp_socket_receive_notify(&client_socket,
                                      my_receive_notify);

/* If status is NX_SUCCESS, NetX Duo will call the function named
   "my_receive_notify" whenever one or more packets are received for
   "client_socket". */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_send"></a>nx_tcp_socket_send
Inviare dati tramite un socket TCP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_send(
    NX_TCP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio invia i dati TCP tramite un socket TCP connesso in precedenza. Se le dimensioni dell'ultima finestra annunciata del ricevitore sono inferiori a questa richiesta, il servizio viene sospeso facoltativamente in base all'opzione di attesa specificata. Questo servizio garantisce che al livello IP non siano inviati dati di pacchetti di dimensioni superiori a MSS. 

> [!WARNING]  
> *A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché anche il driver* di rete tenterà di rilasciare il pacchetto dopo la trasmissione di .

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket TCP precedentemente connessa.
- **packet_ptr** Puntatore a pacchetti di dati TCP.
- **wait_option** Definisce il comportamento del servizio se la richiesta è maggiore delle dimensioni della finestra del ricevitore. Le opzioni di attesa sono definite nel modo seguente:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **valore di timeout nei tick** (da 0x00000001 a 0xFFFFFFFE)

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

```c
/* Send a packet out on the previously created and connected TCP
   socket. If the receive window on the other side of the connection
   is less than the packet size, wait 200 timer ticks before giving
   up. */
status = nx_tcp_socket_send(&client_socket, packet_ptr, 200);

/* If status is NX_SUCCESS, the packet has been sent! */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_state_wait"></a>nx_tcp_socket_state_wait
Attendere che il socket TCP entri in uno stato specifico

### <a name="prototype"></a>Prototipo  

```c
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
    - **NX_TCP_CLOSED** (0x01)
    - **NX_TCP_LISTEN_STATE** (0x02)
    - **NX_TCP_SYN_SENT** (0x03)
    - **NX_TCP_SYN_RECEIVED** (0x04)
    - **NX_TCP_ESTABLISHED** (0x05)
    - **NX_TCP_CLOSE_WAIT** (0x06)
    - **NX_TCP_FIN_WAIT_1** (0x07)
    - **NX_TCP_FIN_WAIT_2** (0x08)
    - **NX_TCP_CLOSING** (0x09)
    - **NX_TCP_TIMED_WAIT** (0x0A)
    - **NX_TCP_LAST_ACK** (0x0B)
- **wait_option** Definisce il comportamento del servizio se lo stato richiesto non è presente. Le opzioni di attesa sono definite come segue:
    - **NX_NO_WAIT** (0x00000000)
    - **valore di timeout in tick** (da 0x00000001 a 0xFFFFFFFF)

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Operazione riuscita.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_NOT_SUCCESSFUL** (0x43) non presente entro il tempo di attesa specificato.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.
- **NX_OPTION_ERROR** (0x0A) Lo stato del socket desiderato non è valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Wait 300 timer ticks for the previously created socket to enter
   the established state in the TCP state machine. */
status = nx_tcp_socket_state_wait(&client_socket,
                                  NX_TCP_ESTABLISHED, 300);

/* If status is NX_SUCCESS, the socket is now in the established
   state! */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nxd_tcp_client_socket_connect
- nxd_tcp_socket_peer_info_get

## <a name="nx_tcp_socket_timed_wait_callback"></a>nx_tcp_socket_timed_wait_callback
Callback di installazione per lo stato di attesa programmato

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_timed_wait_callback(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_timed_wait_callback)(NX_TCP_SOCKET *socket_ptr));
```
### <a name="description"></a>Descrizione

Questo servizio registra una funzione di callback che viene richiamata quando il socket TCP è in stato di attesa a tempo. Per usare questo servizio, la libreria NetX Duo deve essere compilata con ***l'opzione NX_ENABLE_EXTENDED_NOTIFY*** definita.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket client o server precedentemente connessa.
- **tcp_timed_wait_callback** Funzione di callback di attesa a tempo

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Registra correttamente il socket della funzione di callback
- **NX_NOT_SUPPORTED** libreria NetX Duo (0x4B) viene compilata senza la funzionalità di notifica estesa abilitata.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) TCP non è abilitata.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Install the timed wait callback function */
nx_tcp_socket_timed_wait_callback(&client_socket, callback);
```

### <a name="see-also"></a>Vedere anche

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_transmit_configure
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_transmit_configure"></a>nx_tcp_socket_transmit_configure
Configurare i parametri di trasmissione del socket

### <a name="prototype"></a>Prototipo  

```c
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

```c
/* Configure the "client_socket" for a maximum transmit queue depth of
   12, 100 tick timeouts, a maximum of 20 retries, and a timeout double
   on each successive retry. */
status = nx_tcp_socket_transmit_configure(&client_socket,12,100,20,1);

/* If status is NX_SUCCESS, the socket’s transmit retry has been
   configured. */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_window_update_notify_set

## <a name="nx_tcp_socket_window_update_notify_set"></a>nx_tcp_socket_window_update_notify_set
Notificare all'applicazione gli aggiornamenti delle dimensioni della finestra

### <a name="prototype"></a>Prototipo  

```c
UINT nx_tcp_socket_window_update_notify_set(
    NX_TCP_SOCKET *socket_ptr,
    VOID (*tcp_window_update_notify)(NX_TCP_SOCKET *socket_ptr));
```
### <a name="description"></a>Descrizione

Questo servizio installa una routine di callback di aggiornamento della finestra socket. Questa routine viene chiamata automaticamente ogni volta che il socket specificato riceve un pacchetto che indica un aumento delle dimensioni della finestra dell'host remoto.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP creato in precedenza.
- **tcp_window_update_notify** Routine di callback da chiamare quando le dimensioni della finestra cambiano. Il valore NULL disabilita l'aggiornamento delle modifiche della finestra.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** routine di callback (0x00) viene installata nel socket.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_PTR_ERROR** (0x07) Puntatori non validi.
- **NX_NOT_ENABLED** (0x14) la funzionalità TCP non è abilitata.

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Set the function pointer to the windows update callback after creating the
   socket. */
status = nx_tcp_socket_window_update_notify_set(&data_socket,
                                                my_windows_update_callback);

/* Define the window callback function in the host application. */
void my_windows_update_callback(&data_socket)
{

/* Process update on increase TCP transmit socket window size. */
   return;
}
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_enable
- nx_tcp_socket_create
- nx_tcp_socket_disconnect_complete_notify
- nx_tcp_socket_establish_notify
- nx_tcp_socket_mss_get
- nx_tcp_socket_mss_peer_get
- nx_tcp_socket_mss_set
- nx_tcp_socket_peer_info_get
- nx_tcp_socket_queue_depth_notify_set
- nx_tcp_socket_receive_notify
- nx_tcp_socket_timed_wait_callback
- nx_tcp_socket_transmit_configure

## <a name="nx_udp_enable"></a>nx_udp_enable
Abilitare il componente UDP di NetX Duo

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio abilita il componente USER Datagram Protocol (UDP) di NetX Duo. Dopo aver abilitato, i datagrammi UDP possono essere inviati e ricevuti dall'applicazione.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'abilitazione UDP è riuscita.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_ALREADY_ENABLED** (0x15) Questo componente è già stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Enable UDP on the previously created IP instance. */
status = nx_udp_enable(&ip_0);

/* If status is NX_SUCCESS, UDP is now enabled on the specified IP
   instance. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_free_port_find"></a>nx_udp_free_port_find
Trovare la porta UDP disponibile successiva

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_free_port_find(
    NX_IP *ip_ptr, 
    UINT port,
    UINT *free_port_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio cerca una porta UDP gratuita (non associata) a partire dal numero di porta fornito dall'applicazione. La logica di ricerca verrà incapsulata se la ricerca raggiunge il valore di porta massimo di 0xFFFF. Se la ricerca ha esito positivo, la porta disponibile viene restituita nella variabile a cui punta free_port_ptr.

> [!WARNING]  
> *Questo servizio può essere chiamato da un altro thread e può avere la stessa porta restituita. Per evitare questo race condition,* l'applicazione potrebbe voler inserire questo servizio e l'effettivo binding socket sotto la protezione di un mutex.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **porta** Numero di porta per avviare la ricerca (da 1 a 0xFFFF).
- **free_port_ptr** Puntatore alla variabile restituita della porta libera di destinazione.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Ricerca porta gratuita riuscita.
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

```c
/* Locate a free UDP port, starting at port 12, on a previously
   created IP instance. */
status = nx_udp_free_port_find(&ip_0, 12, &free_port);

/* If status is NX_SUCCESS pointer, "free_port" identifies the next
   free UDP port on the IP instance. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_info_get"></a>nx_udp_info_get
Recuperare informazioni sulle attività UDP

### <a name="prototype"></a>Prototipo  

```c
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

> [!IMPORTANT]  
> *Se viene utilizzato un puntatore NX_NULL destinazione, le informazioni specifiche non vengono restituite al chiamante.*

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

```c
/* Retrieve UDP information from previously created IP Instance
   ip_0. */
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

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_packet_info_extract"></a>nx_udp_packet_info_extract
Estrarre i parametri di rete dal pacchetto UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_packet_info_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address,
    UINT *protocol,
    UINT *port,
    UINT *interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio estrae i parametri di rete, ad esempio indirizzo IPv4, numero di porta peer, tipo di protocollo (questo servizio restituisce sempre il tipo UDP) da un pacchetto ricevuto su un'interfaccia in ingresso. Per ottenere informazioni su un pacchetto proveniente dalla rete IPv4 o IPv6, l'applicazione deve usare il servizio ***nxd_udp_packet_info_extract.***

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto.
- **ip_address** Puntatore all'indirizzo IP del mittente.
- **protocollo** Puntatore al protocollo (UDP).
- **porta** Puntatore al numero di porta del mittente.
- **interface_index** Puntatore alla ricezione dell'indice dell'interfaccia.

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Packet interface data successfully extracted ( Dati dell'interfaccia di pacchetto estratti correttamente).
- **NX_INVALID_PACKET** (0x12) Packet non contiene frame IPv4.
- **NX_PTR_ERROR** (0x07) Input puntatore non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Extract network data from UDP packet interface.*/
status = nx_udp_packet_info_extract(packet_ptr, &ip_address,
                                     &protocol, &port,
                                     &interface_index);

/* If status is NX_SUCCESS packet data was successfully
   retrieved. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_bind"></a>nx_udp_socket_bind
Associare il socket UDP alla porta UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_socket_bind(
    NX_UDP_SOCKET *socket_ptr, 
    UINT port,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio associa il socket UDP creato in precedenza alla porta UDP specificata. I socket UDP validi sono compreso tra 0 e 0xFFFF. Se il numero di porta richiesto è associato a un altro socket, questo servizio attende il periodo di tempo specificato per la dissociazione del socket dal numero di porta.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket UDP creata in precedenza.
- **porta** Numero di porta da associare a** (da 1 a 0xFFFF). Se il numero di porta NX_ANY_PORT** (0x0000), l'istanza IP cerca la porta gratuita successiva e la usa per l'associazione.
- **wait_option** Definisce il comportamento del servizio se la porta è già associata a un altro socket. Le opzioni di attesa sono definite nel modo seguente:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **valore di timeout nei tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Associazione socket riuscita.
- **NX_ALREADY_BOUND** (0x22) Questo socket è già associato a un'altra porta.
- **NX_PORT_UNAVAILABLE** (0x23) La porta è già associata a un socket diverso.
- **NX_NO_FREE_PORTS** (0x45) Nessuna porta disponibile.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_INVALID_PORT** (0x46) È stata specificata una porta non valida.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Bind the previously created UDP socket to port 12 on the
   previously created IP instance. If the port is already bound,
   wait for 300 timer ticks before giving up. */
status = nx_udp_socket_bind(&udp_socket, 12, 300);

/* If status is NX_SUCCESS, the UDP socket is now bound to
   port 12.*/
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_bytes_available"></a>nx_udp_socket_bytes_available
Recupera il numero di byte disponibili per il recupero

### <a name="prototype"></a>Prototipo  

```c
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

- **NX_SUCCESS** (0x00) Recupero dei byte disponibili riuscito.
- **NX_NOT_SUCCESSFUL** (0x43) Socket non associato a una porta.
- **NX_PTR_ERROR** (0x07) Puntatori non validi.
- **NX_NOT_ENABLED** la funzionalità UDP (0x14) non è abilitata.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Get the bytes available for retrieval from the UDP socket. */
status = nx_udp_socket_bytes_available(&my_socket,
                                       &bytes_available);

/* If status == NX_SUCCESS, the number of bytes was successfully
   retrieved.*/
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_checksum_disable"></a>nx_udp_socket_checksum_disable
Disabilitare il checksum per il socket UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_socket_checksum_disable(NX_UDP_SOCKET *socket_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio disabilita la logica di checksum per l'invio e la ricezione di pacchetti sul socket UDP specificato. Quando la logica di checksum è disabilitata, il valore zero viene caricato nel campo checksum dell'intestazione UDP per tutti i pacchetti inviati tramite questo socket. Un valore di checksum di valore zero nell'intestazione UDP segnala al ricevitore che il checksum non viene calcolato per questo pacchetto.

Si noti anche che  questa operazione non ha alcun effetto se NX_DISABLE_UDP_RX_CHECKSUM e **NX_DISABLE_UDP_TX_CHECKSUM** vengono definiti rispettivamente durante la ricezione e l'invio di pacchetti UDP,

Si noti che questo servizio non ha alcun effetto sui pacchetti nella rete IPv6 perché il checksum UDP è obbligatorio per IPv6.

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

```c
/* Disable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_disable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will not have a checksum
   calculated. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_checksum_enable"></a>nx_udp_socket_checksum_enable
Abilitare il checksum per il socket UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_socket_checksum_enable(NX_UDP_SOCKET *socket_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio abilita la logica di checksum per l'invio e la ricezione di pacchetti sul socket UDP specificato. Il checksum copre l'intera area dati UDP e una pseudo-intestazione IP.

Si noti inoltre che questa operazione non ha alcun effetto **se NX_DISABLE_UDP_RX_CHECKSUM** e **NX_DISABLE_UDP_TX_CHECKSUM** vengono definiti rispettivamente durante la ricezione e l'invio di pacchetti UDP.

Si noti che questo servizio non ha alcun effetto sui pacchetti nella rete IPv6. Il checksum UDP è obbligatorio in IPv6.

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

```c
/* Enable the UDP checksum logic for packets sent on this socket. */
status = nx_udp_socket_checksum_enable(&udp_socket);

/* If status is NX_SUCCESS, outgoing packets will have a checksum
   calculated. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_create"></a>nx_udp_socket_create
Creare un socket UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_socket_create(
    NX_IP *ip_ptr,
    NX_UDP_SOCKET *socket_ptr, 
    CHAR *name,
    ULONG type_of_service, 
    ULONG fragment,
    UINT time_to_live, 
    ULONG queue_maximum);
```
### <a name="description"></a>Descrizione

Questo servizio crea un socket UDP per l'istanza IP specificata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza.
- **socket_ptr** Puntatore al blocco di controllo del nuovo socket UDP.
- **name** Nome dell'applicazione per questo socket UDP.
- **type_of_service** Definisce il tipo di servizio per la trasmissione. I valori validi sono i seguenti:
    - **NX_IP_NORMAL** (0x00000000)
    - **NX_IP_MIN_DELAY** (0x00100000)
    - **NX_IP_MAX_DATA** (0x00080000)
    - **NX_IP_MAX_RELIABLE** (0x00040000)
    - **NX_IP_MIN_COST** (0x00020000)
- **fragment Specifica se è** consentita o meno la frammentazione IP. Se NX_FRAGMENT_OKAY (0x0), la frammentazione IP è consentita. Se NX_DONT_FRAGMENT (0x4000), la frammentazione IP è disabilitata.
- **time_to_live** Specifica il valore a 8 bit che definisce il numero di router che questo pacchetto può passare prima di essere buttato via. Il valore predefinito viene specificato da NX_IP_TIME_TO_LIVE.
- **queue_maximum** Definisce il numero massimo di datagrammi UDP che possono essere accodati per questo socket. Dopo aver raggiunto il limite della coda, per ogni nuovo pacchetto ricevuto viene rilasciato il pacchetto UDP meno recente.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Creazione socket UDP riuscita.
- **NX_OPTION_ERROR** (0x0A) Tipo di servizio, frammento o opzione di time-to-live non valido.
- **NX_PTR_ERROR** (0x07) IP o puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Inizializzazione e thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Create a UDP socket with a maximum receive queue of 30 packets.*/
status = nx_udp_socket_create(&ip_0, &udp_socket, "Sample UDP Socket",
                              NX_IP_NORMAL, NX_FRAGMENT_OKAY, 0x80,
                              30);

/* If status is NX_SUCCESS, the new UDP socket has been created and
   is ready for binding. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_delete"></a>nx_udp_socket_delete
Eliminare un socket UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_socket_delete(NX_UDP_SOCKET *socket_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio elimina un socket UDP creato in precedenza. Se il socket è stato associato a una porta, il socket deve essere prima di tutto non associato.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Eliminazione socket riuscita.
- **NX_STILL_BOUND** (0x42) Socket è ancora associato.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Delete a previously created UDP socket. */
status = nx_udp_socket_delete(&udp_socket);

/* If status is NX_SUCCESS, the previously created UDP socket has
   been deleted. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_info_get"></a>nx_udp_socket_info_get
Recuperare informazioni sulle attività socket UDP

### <a name="prototype"></a>Prototipo  

```c
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

> [!IMPORTANT]  
> *Se un puntatore di destinazione NX_NULL, queste informazioni specifiche non vengono restituite al chiamante.*

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

```c
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

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_port_get"></a>nx_udp_socket_port_get
Selezionare il numero di porta associato al socket UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_socket_port_get(
    NX_UDP_SOCKET *socket_ptr,
    UINT *port_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio recupera il numero di porta associato al socket, utile per trovare la porta allocata da NetX Duo nelle situazioni in cui il NX_ANY_PORT è stato specificato al momento dell'associazione del socket.

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

```c
/* Get the port number of created and bound UDP socket. */
status = nx_udp_socket_port_get(&udp_socket, &port);

/* If status is NX_SUCCESS, the port variable contains the port this
   socket is bound to. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_receive"></a>nx_udp_socket_receive
Ricevere un datagramma dal socket UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_socket_receive(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET **packet_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio riceve un datagramma UDP dal socket specificato. Se nessun datagramma viene accodato nel socket specificato, il chiamante viene sospeso in base all'opzione di attesa fornita.

> [!CAUTION]  
> *Se NX_SUCCESS viene restituito , l'applicazione è* responsabile del rilascio del pacchetto ricevuto quando non è più necessario .

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket UDP creata in precedenza.
- **packet_ptr** Puntatore al puntatore a pacchetti di datagrammi UDP.
- **wait_option** Definisce il comportamento del servizio se un datagramma non è attualmente accodato in questo socket. Le opzioni di attesa sono definite nel modo seguente:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **valore di timeout nei tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Ricezione socket riuscita.
- **NX_NOT_BOUND** (0x24) Il socket non è stato associato ad alcuna porta.
- **NX_NO_PACKET** (0x01) Non è stato ricevuto alcun datagramma UDP.
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort.
- **NX_PTR_ERROR** (0x07) Socket o puntatore restituito pacchetto non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Receive a packet from a previously created and bound UDP socket.
   If no packets are currently available, wait for 500 timer ticks
   before giving up. */
status = nx_udp_socket_receive(&udp_socket, &packet_ptr, 500);

/* If status is NX_SUCCESS, the received UDP packet is pointed to by
   packet_ptr. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_receive_notify"></a>nx_udp_socket_receive_notify
Notificare all'applicazione ogni pacchetto ricevuto

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_socket_receive_notify(
    NX_UDP_SOCKET *socket_ptr,
    VOID (*udp_receive_notify)(NX_UDP_SOCKET *socket_ptr));
```
### <a name="description"></a>Descrizione 

Questo servizio imposta il puntatore a funzione receive notify sulla funzione di callback specificata dall'applicazione. Questa funzione di callback viene quindi chiamata ogni volta che viene ricevuto un pacchetto nel socket. Se viene NX_NULL un puntatore di notifica, la funzione di notifica di ricezione è disabilitata.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket UDP.
- **udp_receive_notify** Puntatore a funzione di callback dell'applicazione chiamato quando viene ricevuto un pacchetto nel socket.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Impostare correttamente la funzione di notifica di ricezione socket.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread, timer e ISR

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Setup a receive packet callback function for the "udp_socket"
   socket. */
status = nx_udp_socket_receive_notify(&udp_socket,
                                      my_receive_notify);

/* If status is NX_SUCCESS, NetX Duo will call the function named
   "my_receive_notify" whenever a packet is received for
   "udp_socket". */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_send"></a>nx_udp_socket_send
Inviare un datagramma UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_socket_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address, 
    UINT port);
```
### <a name="description"></a>Descrizione

Questo servizio invia un datagramma UDP tramite un socket UDP creato in precedenza e associato per le reti IPv4. NetX Duo trova un indirizzo IP locale appropriato come indirizzo di origine in base all'indirizzo IP di destinazione. Per specificare un'interfaccia e un indirizzo IP di origine specifici, l'applicazione deve usare il  **nxd_udp_socket_source_send** servizio.

Si noti che questo servizio restituisce immediatamente indipendentemente dal fatto che il datagramma UDP sia stato inviato correttamente. Il servizio equivalente NetX Duo (IPv4/IPv6) è ***nxd_udp_socket_send***.

Il socket deve essere associato a una porta locale.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket UDP creata in precedenza
- **packet_ptr** Puntatore a pacchetti di datagrammi UDP
- **ip_address** Indirizzo IPv4 di destinazione
- **porta** Numero di porta di destinazione valido compreso tra 1 e 0xFFFF), nell'ordine dei byte dell'host

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio socket UDP riuscito
- **NX_NOT_BOUND** (0x24) Socket non associato ad alcuna porta
- **NX_NO_INTERFACE_ADDRESS** (0x50) Non è possibile trovare un'interfaccia in uscita appropriata.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IP del server non valido
- **NX_UNDERFLOW** (0x02) Spazio insufficiente per l'intestazione UDP nel pacchetto
- **NX_OVERFLOW** (0x03) Il puntatore di accodamento del pacchetto non è valido
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_NOT_ENABLED** (0x14) UDP non è stato abilitato
- **NX_INVALID_PORT** (0x46) Il numero di porta non è compreso in un intervallo valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
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

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_source_send"></a>nx_udp_socket_source_send
Inviare un datagramma tramite socket UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_socket_source_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    ULONG ip_address,
    UINT port,
    UINT address_index);
```
### <a name="description"></a>Descrizione

Questo servizio invia un datagramma UDP tramite un socket UDP creato in precedenza e associato tramite l'interfaccia di rete con l'indirizzo IP specificato come indirizzo di origine. Si noti che il servizio restituisce immediatamente, indipendentemente dal fatto che il datagramma UDP sia stato inviato correttamente o meno. ***nxd_udp_socket_source_send*** funziona sia per le reti IPv4 che per le reti IPv6.

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
- **NX_NOT_ENABLED** (0x14) l'elaborazione UDP non è abilitata.
- **NX_PTR_ERROR** (0x07) Puntatore non valido.
- **NX_OVERFLOW** (0x03) Puntatore di accodamento pacchetti non valido.
- **NX_UNDERFLOW** (0x02) Puntatore anteposto pacchetto non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_INVALID_INTERFACE** (0x4C) Indice di indirizzi non valido.
- **NX_INVALID_PORT** (0x46) Il numero di porta supera il numero massimo di porta.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define ADDRESS_INDEX 1

/* Send packet out on port 80 to the specified destination IP on the
   interface at index 1 in the IP task interface list. */
status = nx_udp_socket_source_send(socket_ptr, packet_ptr,
                                   destination_ip, 80,
                                   ADDRESS_INDEX);

/* If status is NX_SUCCESS packet was successfully transmitted. */
```

### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_socket_unbind"></a>nx_udp_socket_unbind
Scollegare il socket UDP dalla porta UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_socket_unbind(NX_UDP_SOCKET *socket_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio rilascia l'associazione tra il socket UDP e una porta UDP. Tutti i pacchetti ricevuti archiviati nella coda di ricezione vengono rilasciati come parte dell'operazione di annullamento dell'associazione.

Se sono presenti altri thread in attesa di associare un altro socket alla porta non associata, il primo thread sospeso viene quindi associato alla porta appena non associata.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket UDP creata in precedenza.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Operazione riuscita di annullamento dell'associazione del socket.
- **NX_NOT_BOUND** (0x24) Il socket non è stato associato ad alcuna porta.
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio.
- **NX_NOT_ENABLED** (0x14) Questo componente non è stato abilitato.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

Sì

### <a name="example"></a>Esempio

```c
/* Unbind the previously bound UDP socket. */
status = nx_udp_socket_unbind(&udp_socket);

/* If status is NX_SUCCESS, the previously bound socket is now
   unbound. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nx_udp_source_extract"></a>nx_udp_source_extract
Estrarre l'INDIRIZZO IP e inviare la porta dal datagramma UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nx_udp_source_extract(
    NX_PACKET *packet_ptr,
    ULONG *ip_address, 
    UINT *port);
```
### <a name="description"></a>Descrizione

Questo servizio estrae l'indirizzo IP e il numero di porta del mittente dalle intestazioni IP e UDP del datagramma UDP fornito. Si noti che il ***nxd_udp_source_extract*** funziona con i pacchetti provenienti dalla rete IPv4 o IPv6.

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

```c
/* Extract the IP and port information from the sender of the UPD packet. */
status = nx_udp_source_extract(packet_ptr, &sender_ip_address, &sender_port);

/* If status is NX_SUCCESS, the sender IP and port information has been stored
   in sender_ip_address and sender_port respectively.*/
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nxd_icmp_enable"></a>nxd_icmp_enable
Abilitare i servizi ICMPv4 e ICMPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_icmp_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio abilita i servizi ICMPv4 e ICMPv6 e può essere chiamato solo dopo la creazione dell'istanza IP. Il servizio può essere abilitato prima o dopo aver abilitato IPv6 (vedere *nxd_ipv6_enable*). I servizi ICMPv4 includono Echo Request/Reply. I servizi ICMPv6 includono Echo Request/Reply, Neighbor Discovery, Duplicate Address Detection, Router Discovery e Stateless Address Auto-configuration. L'equivalente IPv4 in NetX *è nx_icmp_enable*.

> [!NOTE] 
> *Se l'indirizzo IPv6* viene configurato manualmente prima di abilitare ICMPv6, il IPv6 configurato manualmente non è soggetto al processo di rilevamento degli indirizzi duplicati .

*nx_icmp_enable* avvia i servizi ICMP solo per le operazioni IPv4. Le applicazioni che usano servizi ICMPv6 *devono usare nxd_icmp_enable* anziché *nx_icmp_enable*.

Per utilizzare la richiesta di router IPv6 e la configurazione dell'indirizzo automatico senza stato IPv6, È necessario che ICMPv6 sia abilitato.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** i servizi ICMP 0x00 (0x00) sono stati abilitati correttamente
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Enable ICMP on the IP instance. */
status = nxd_icmp_enable(&ip_0);

/* A status return of NX_SUCCESS indicates that the IP instance is
   enabled for ICMP services. */
```
### <a name="see-also"></a>Vedere anche

- nx_icmp_enable
- nx_icmp_info_get
- nx_icmp_ping
- nxd_icmp_ping
- nxd_icmp_source_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nxd_icmp_ping"></a>nxd_icmp_ping
Eseguire richieste echo ICMPv4 o ICMPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_icmp_ping(
    NX_IP *ip_ptr, 
    NXD_ADDRESS *ip_address,
    CHAR *data_ptr, 
    ULONG data_size,
    NX_PACKET **response_ptr, 
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto Echo Request ICMP tramite un'interfaccia fisica appropriata e attende una risposta Echo dall'host di destinazione. NetX Duo determina l'interfaccia appropriata, in base all'indirizzo di destinazione, per inviare il messaggio ping . Le applicazioni devono usare il ***servizio*** nxd_icmp_source_ping specificare l'interfaccia fisica e l'indirizzo IP di origine preciso da usare per la trasmissione dei pacchetti.

L'istanza IP deve essere stata creata e i servizi ICMPv4/ICMPv6 devono essere abilitati (vedere ***nxd_icmp_enable***).

> [!WARNING]  
> Se NX_SUCCESS viene restituito , l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP
- **ip_address** Indirizzo IP di destinazione per il ping, nell'ordine dei byte dell'host
- **data_ptr** Puntatore all'area dati del pacchetto ping
- **data_size** Numero di byte di dati ping
- **response_ptr** Puntatore al puntatore al pacchetto di risposta
- **wait_option** Tempo di attesa per una risposta. Le opzioni di attesa sono definite come segue:
    - **NX_NO_WAIT** (0x00000000)
    - **valore di timeout in tick** (da 0x00000001 a 
    - **NX_WAIT_FOREVER** 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ping inviato e ricevuto
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è abilitato
- **NX_OVERFLOW** (0x03) I dati ping superano il payload del pacchetto
- **NX_NO_RESPONSE(0x29)** L'host di destinazione non ha risposto
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da tx_thread_wait_abort
- **NX_NO_INTERFACE_ADDRESS** (0x50) Non è possibile trovare alcuna interfaccia in uscita appropriata.
- **NX_PTR_ERROR** (0x07) IP o puntatore di risposta non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_NOT_ENABLED** ip (0x14) o componente ICMP non è abilitato
- **NX_IP_ADDRESS_ERROR'indirizzo** IP di input 0x21 (0x21) non è valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* The following two examples illustrate how to use this API to send
   ping packets to IPv6 or IPv4 destinations. */

/* The first example: Send a ping packet to an IPv6 host
   2001:1234:5678::1 */
   
/* Declare variable address to hold the destination address. */
NXD_ADDRESS ip_address;

char *buffer = “abcd”;
UINT prefix_length = 10;

/* Set the IPv6 address. */
ip_address.nxd_ip_address_version  = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0]    = 0x20011234;
ip_address.nxd_ip_address.v6[1]    = 0x56780000;
ip_address.nxd_ip_address.v6[2]    = 0;
ip_address.nxd_ip_address.v6[3]    = 1;

status = nxd_icmp_ping(&ip_0, &ip_address, buffer,
                       strlen(buffer),&response_ptr,
                       NX_WAIT_FOREVER);

/* A return value of NX_SUCCESS indicates a ping reply has been
   received from IP address 2001:1234:5678::1 and the response
   packet is contained in the packet pointed to by response_ptr.It
   should have the same “abcd” four bytes of data. */

/* The second example: Send a ping packet to an IPv4 host 1.2.3.4 */

/* Program the IPv4 address. */
ip_address.nxd_ip_address_version  = NX_IP_VERSION_V4;
ip_address.nxd_ip_address.v4[0]    = 0x01020304;

status = nxd_icmp_ping(&ip_0, &ip_address, buffer,
                       strlen(buffer),&response_ptr, 10);

/* A return value of NX_SUCCESS indicates a ping reply was received
   from IP address 1.2.3.4 and the response packet is contained in
   the packet pointed to by response_ptr. It should have the same
   “abcd” four bytes of data. */
```
### <a name="see-also"></a>Vedere anche

- nx_icmp_enable
- nx_icmp_info_get
- nx_icmp_ping
- nxd_icmp_enable
- nxd_icmp_source_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nxd_icmp_source_ping"></a>nxd_icmp_source_ping
Eseguire richieste echo ICMPv4 o ICMPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_icmp_source_ping(
    NX_IP *ip_ptr, 
    NXD_ADDRESS *ip_address,
    UINT address_index,
    CHAR *data_ptr, 
    ULONG data_size,
    NX_PACKET **response_ptr,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto echo request ICMP usando l'indice specificato di un indirizzo IPv4 o IPv6 e tramite l'interfaccia di rete a cui è associato l'indirizzo di origine e attende una risposta Echo dall'host di destinazione. Questo servizio funziona sia con gli indirizzi IPv4 che con gli indirizzi IPv6. Il parametro *address_index* indica l'indirizzo IPv4 o IPv6 di origine da utilizzare. Per l'indirizzo IPv4, *address_index* è lo stesso indice dell'interfaccia di rete collegata. Per IPv6, *il address_index* indica la voce nella tabella degli indirizzi IPv6.

L'istanza IP deve essere stata creata e i servizi ICMPv4 e ICMPv6 devono essere abilitati (vedere *nxd_icmp_enable*).

> [!CAUTION] 
> *Se NX_SUCCESS viene restituito , l'applicazione è* responsabile del rilascio del pacchetto ricevuto quando non è più necessario.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP
- **ip_address** Indirizzo IP di destinazione per il ping, nell'ordine dei byte dell'host
- **address_index** Indica l'indirizzo IP da usare come indirizzo di origine
- **data_ptr** Puntatore all'area dati del pacchetto ping
- **data_size** Numero di byte di dati ping
- **response_ptr** Puntatore al puntatore del pacchetto di risposta
- **wait_option** Tempo di attesa per una risposta. Le opzioni di attesa sono definite come segue:
    - **NX_NO_WAIT** (0x00000000)
    - **valore di timeout in tick** (da 0x00000001 a 0xFFFFFFFE
    - **NX_WAIT_FOREVER** 0xFFFFFFFF)

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Ping inviato e ricevuto
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è abilitato
- **NX_OVERFLOW** (0x03) I dati ping superano il payload del pacchetto
- **NX_NO_RESPONSE(0x29)** L'host di destinazione non ha risposto
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da tx_thread_wait_abort
- **NX_NO_INTERFACE_ADDRESS** (0x50) Non è possibile trovare alcuna interfaccia in uscita appropriata
- **NX_PTR_ERROR** (0x07) IP o puntatore di risposta non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_NOT_ENABLED** ip (0x14) o componente ICMP non è abilitato
- **NX_IP_ADDRESS_ERROR'indirizzo** IP di input 0x21 (0x21) non è valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* The following two examples illustrate how to use this API to send ping
   packets to IPv6 or IPv4 destinations. */

/* The first example: Send a ping packet to an IPv6 host
   FE80::411:7B23:40dc:f181 */

/* Declare variable address to hold the destination address. */

#define PRIMARY_INTERFACE 0
#define GLOBAL_IPv6_ADDRESS 1

NXD_ADDRESS ip_address;
char *buffer = “abcd”;
UINT prefix_length = 10;

/* Set the IPv6 address. */
ip_address.nxd_ip_address_version  = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0]    = 0xFE800000;
ip_address.nxd_ip_address.v6[1]    = 0x00000000;
ip_address.nxd_ip_address.v6[2]    = 0x04117B23;
ip_address.nxd_ip_address.v6[3]    = 0x40DCF181;

status = nxd_icmp_source_ping(&ip_0, &ip_address,
                              GLOBAL_IPv6_ADDRESS,
                              buffer,
                              strlen(buffer),
                              &response_ptr,
                              NX_WAIT_FOREVER);

/* A return value of NX_SUCCESS indicates a ping reply has been received
   from IP address FE80::411:7B23:40dc:f181 and the response packet is
   contained in the packet pointed to by response_ptr. It should have the
   same “abcd” four bytes of data. */

/* The second example: Send a ping packet to an IPv4 host 1.2.3.4 */

/* Program the IPv4 address. */
ip_address.nxd_ip_address_version  = NX_IP_VERSION_V4;
ip_address.nxd_ip_address.v4       = 0x01020304;

status = nxd_icmp_source_ping(&ip_0, &ip_address,
                              PRIMARY_INTERFACE,
                              buffer,
                              strlen(buffer),
                              &response_ptr,
                              NX_WAIT_FOREVER);

/* A return value of NX_SUCCESS indicates a ping reply was received from
   IP address 1.2.3.4 and the response packet is contained in the packet
   pointed to by response_ptr. It should have the same “abcd” four bytes
   of data. */
```

### <a name="see-also"></a>Vedere anche

- nx_icmp_enable
- nx_icmp_info_get
- nx_icmp_ping
- nxd_icmp_enable
- nxd_icmp_ping
- nxd_icmpv6_ra_flag_callback_set

## <a name="nxd_icmpv6_ra_flag_callback_set"></a>nxd_icmpv6_ra_flag_callback_set
Impostare la funzione di callback di modifica del flag ra ICMPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_icmpv6_ra_flag_callback_set(
    NX_IP *ip_ptr, 
    VOID(*ra_callback)(NX_IP*ip_ptr, UINT ra_flag));
```
### <a name="description"></a>Descrizione

Questo servizio imposta la funzione di callback di modifica del flag router advertisement ICMPv6. La funzione di callback fornita dall'utente viene richiamata quando NetX Duo riceve un messaggio di annuncio router.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP
- **ra_callback** Funzione di callback fornita dall'utente

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Impostare correttamente la funzione di callback del flag RA
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è abilitato
- **NX_PTR_ERROR** (0x07) IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
VOID icmpv6_ra_flag_callback(NX_IP *ip_ptr, UINT ra_flag)
{
   /* RA flag has changed. The updated value is passed in via the
      ra_flag parameter. */
}

/* Configure the user-defined ICMPv6 RA flag change callback
   function. */
status = nxd_icmpv6_ra_flag_callback_set(&ip_0,
                                         icmpv6_ra_flag_callback);

/* A status return of NX_SUCCESS indicates the callback function has
   been successfully configured. */
```
### <a name="see-also"></a>Vedere anche

- nx_icmp_enable
- nx_icmp_info_get
- nx_icmp_ping
- nxd_icmp_enable
- nxd_icmp_ping
- nxd_icmp_source_ping

## <a name="nxd_ip_raw_packet_send"></a>nxd_ip_raw_packet_send
Inviare un pacchetto IP non elaborato

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ip_raw_packet_send(
    NX_IP *ip_ptr, 
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *destination
    ULONG protocol, 
    UINT ttl, 
    ULONG tos);
```
### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto IPv4 o IPv6 non elaborato (nessuna intestazione del protocollo a livello di trasporto). In un sistema multihome, se il sistema non è in grado di determinare un'interfaccia appropriata (ad esempio, se l'indirizzo IP di destinazione è un indirizzo multicast IPv4 broadcast, multicast o IPv6), viene selezionato il dispositivo primario. Il servizio ***nxd_ip_raw_packet_source_send** _ può essere usato per specificare un'interfaccia in uscita. L'equivalente di NetX è _ *_nx_ip_raw_packet_send_.**

L'istanza IP deve essere creata in precedenza e la gestione dei pacchetti IP non elaborati deve essere abilitata usando ***nx_ip_raw_packet_enable*** servizio.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza
- **packet_ptr** Puntatore al pacchetto da trasmettere
- **destination_ip** Puntatore all'indirizzo di destinazione
- **protocollo** Protocollo di pacchetti archiviato nell'intestazione IP
- **ttl** Valore per TTL o limite hop
- **tos** Valore per TOS o classe di traffico ed etichetta di flusso

### <a name="return-value"></a>Valore restituito 

- **NX_SUCCESS** (0x00) Il pacchetto IP non elaborato è stato inviato correttamente
- **NX_NO_INTERFACE_ADDRESS** (0x50) Non è possibile trovare un'interfaccia in uscita adatta
- **NX_NOT_ENABLED** (0x14) Gestione ip non elaborato non abilitata
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IPv4 o IPv6 non valido
- **NX_UNDERFLOW** (0x02) Spazio insufficiente per l'intestazione IPv4 o IPv6 nel pacchetto
- **NX_OVERFLOW** (0x03) Il puntatore di accodamento del pacchetto non è valido
- **NX_PTR_ERROR** (0x07) Puntatore IP o puntatore a pacchetto non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_INVALID_PARAMETERS** (0x4D) Input indirizzo IPv6 non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
NXD_ADDRESS dest_address;

/* Set the destination address,in this case an IPv6 address. */
dest_address.nxd_ip_address_version  = NX_IP_VERSION_V6;
dest_address.nxd_ip_address.v6[0]    = 0x20011234;
dest_address.nxd_ip_address.v6[1]    = 0x56780000;
dest_address.nxd_ip_address.v6[2]    = 0;
dest_address.nxd_ip_address.v6[3]    = 1;

UINT ttl, tos;

ttl = 128;

tos = 0;

/* Enable RAW IP handling on the previously created IP instance.*/
status = nx_raw_ip_packet_enable(&ip_0);

/* Allocate a packet pointed to by packet_ptr from the IP packet
   pool. */
/* Then transmit the packet to the destination address. */

status = nxd_ip_raw_packet_send(&ip_0, packet_ptr, dest_address,
                                NX_PROTOCOL_UDP, ttl, tos);

/* A status return of NX_SUCCESS indicates the packet was
   successfully transmitted. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_source_send

## <a name="nxd_ip_raw_packet_source_send"></a>nxd_ip_raw_packet_source_send
Inviare un pacchetto non elaborato usando l'indirizzo di origine specificato

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ip_raw_packet_source_send(
    NX_IP *ip_ptr,
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *destination_ip,
    UINT address_index,
    ULONG protocol,
    UINT ttl,
    ULONG tos);
```
### <a name="description"></a>Descrizione

Questo servizio invia un pacchetto IPv4 o IPv6 non elaborato usando l'indirizzo IPv4 o IPv6 specificato come indirizzo di origine. Questo servizio viene in genere usato in un sistema multihome, se il sistema non è in grado di determinare un'interfaccia appropriata, ad esempio se l'indirizzo IP di destinazione è un indirizzo multicast IPv4 broadcast, multicast o IPv6. Il parametro *address_index* consente all'applicazione di specificare l'indirizzo di origine da usare per l'invio di questo pacchetto non elaborato.

L'istanza IP deve essere creata in precedenza e la gestione dei pacchetti IP non elaborati deve essere abilitata usando ***nx_ip_raw_packet_enable*** servizio.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP
- **packet_ptr** Puntatore al pacchetto da inviare
- **destination_ip** Indirizzo IP di destinazione
- **address_index** Indice degli indirizzi IPv4 o IPv6 da usare come indirizzo di origine.
- **protocollo** Valore per il campo del protocollo
- **ttl** Valore per il limite di ttl o hop
- **tos** Valore per tos o traffic class e flow label

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Il pacchetto viene inviato correttamente
- **NX_UNDERFLOW** (0x02) Spazio insufficiente per l'intestazione IPv4 o IPv6 nel pacchetto
- **NX_OVERFLOW** (0x03) Il puntatore di accodamento del pacchetto non è valido
- **NX_PTR_ERROR** (0x07) Puntatore non valido a blocco di controllo IP, pacchetto o destination_ip
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_NOT_ENABLED** (0x14) Elaborazione non elaborata non abilitata
- **NX_IP_ADDRESS_ERROR** (0x21) Errore di indirizzo
- **NX_INVALID_INTERFACE** (0x4C) Indice di interfaccia non valido
- **NX_INVALID_PARAMETERS** (0x4D) Input indirizzo IPv6 non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define SOURCE_ADDRESS_INDEX 2

/* Send a raw packet from specified interface. */
status = nxd_ip_raw_packet_source_send(&ip_0, packet_ptr,
                                       dest_ip,
                                       SOURCE_ADDRESS_INDEX,
                                       NX_IP_RAW,
                                       NX_IP_TIME_TO_LIVE,
                                       NX_IP_NORMAL);

/* If status == NX_SUCCESS, raw packet has been sent out on the
   specified interface. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_raw_packet_disable
- nx_ip_raw_packet_enable
- nx_ip_raw_packet_filter_set
- nx_ip_raw_packet_receive
- nx_ip_raw_packet_send
- nx_ip_raw_packet_source_send
- nx_ip_raw_receive_queue_max_set
- nxd_ip_raw_packet_send

## <a name="nxd_ipv6_address_change_notify"></a>nxd_ipv6_address_change_notify
Impostare una notifica di modifica dell'indirizzo ipv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_address_change_notify(
    NX_IP *ip_ptr,
    VOID (*ip_address_change_notify)(NX_IP *, UINT, UINT, UINT, ULONG *));
```
### <a name="description"></a>Descrizione

Questo servizio registra una routine di callback dell'applicazione chiamata da NetX Duo ogni volta che viene modificato l'indirizzo IPv6.

Questo servizio è disponibile se la libreria NetX Duo è compilata è ***l'opzione NX_ENABLE_IPV6_ADDRESS_CHANGE_NOTIFY*** definita.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore a blocco di controllo IP
- **ip_address_change_notify** Funzione di callback dell'applicazione

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Operazione riuscita
- **NX_NOT_SUPPORTED** funzionalità di notifica della modifica dell'indirizzo IPv6 (0x4B) non è incorporata nella libreria NetX Duo
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_NOT_ENABLED** notifica della modifica dell'indirizzo IPv6 0x14 (0x14) non è stata compilata

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
VOID ip_address_change_notify(NX_IP *ip_ptr, UINT status,
                              UINT interface_index,
                              UINT address_index,
                              ULONG *ip_address)
{

   /* Do something when ip address changed. */
}

void ip_address_thread_entry(ULONG id)
{

   /* Set the ip address change notify of IP instance. */
   status = nxd_ipv6_address_change_notify (&ip_0, ip_address_change_notify);

/* If status == NX_SUCCESS, the ip address change notify of IP
   instance was successfully set. */
}
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_address_delete"></a>nxd_ipv6_address_delete
Elimina indirizzo IPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_address_delete(
    NX_IP *ip_ptr, 
    UINT address_index);
```
### <a name="description"></a>Descrizione

Questo servizio elimina l'indirizzo IPv6 in corrispondenza dell'indice specificato nella tabella degli indirizzi IPv6 dell'istanza IP specificata. Non esiste un equivalente NetX.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza
- **address_index** Indice nella tabella degli indirizzi IPv6 dell'istanza IP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'indirizzo è stato eliminato
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è incorporata nella libreria NetX Duo
- **NX_NO_INTERFACE_ADDRESS** (0x50) Non è possibile trovare alcuna interfaccia in uscita appropriata
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
NXD_ADDRESS ip_address;
UINT        address_index;

/* Delete the IPv6 address at the specified address table index. */
address_index = 1;
status = nxd_ipv6_address_delete(&ip_0, address_index);

/* A status return of NX_SUCCESS indicates that the IP instance
   address is successfully deleted. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_address_get"></a>nxd_ipv6_address_get
Recuperare l'indirizzo e il prefisso IPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_address_get(
    NX_IP *ip_ptr, 
    UINT address_index, 
    NXD_ADDRESS *ip_address,
    ULONG *prefix_length,
    UINT *interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio recupera l'indirizzo IPv6 e il prefisso in corrispondenza dell'indice specificato nella tabella degli indirizzi dell'istanza IP specificata. L'indice dell'interfaccia fisica a cui è associato l'indirizzo IPv6 viene restituito nel *puntatore interface_index* corrente. I servizi equivalenti NetX sono ***nx_ip_address_get** _ e _*_nx_ip_interface_address_get_**.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza
- **address_index** Indice nella tabella degli indirizzi dell'istanza IP
- **ip_address** Puntatore all'indirizzo da impostare
- **prefix_length** Lunghezza del prefisso dell'indirizzo (subnet mask)
- **interface_index** Puntatore all'indice dell'interfaccia

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) IPv6 è stato abilitato correttamente
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è incorporata nella libreria NetX Duo.
- **NX_NO_INTERFACE_ADDRESS** (0x50) Nessun indirizzo di interfaccia o indirizzo di address_index
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
NXD_ADDRESS ip_address;
UINT        address_index;
ULONG       prefix_length;
UINT        interface_index;

/* Get the IPv6 address at the specified address table index. If
   found, the address network interface is returned in the
   interface_index input, as well as the address prefix in the
   prefix_length input. */

address_index = 1;
status = nxd_ipv6_address_get(&ip_0, address_index, &ip_address,
                              &prefix_length, &interface_index);

/* A status return of NX_SUCCESS indicates that the IP instance
   address is successfully retrieved. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_address_set"></a>nxd_ipv6_address_set
Impostare l'indirizzo e il prefisso IPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_address_set(
    NX_IP *ip_ptr, 
    UINT interface_index,
    NXD_ADDRESS *ip_address,
    ULONG prefix_length,
    UINT *address_index);
```
### <a name="description"></a>Descrizione

Questo servizio imposta l'indirizzo IPv6 e il prefisso specificati sull'istanza IP specificata. Se *l address_index'argomento* non è Null, viene restituito l'indice nella tabella degli indirizzi IPv6 in cui viene inserito l'indirizzo. I servizi equivalenti NetX sono ***nx_ip_address_set** _ e _*_nx_ip_interface_address_set_**.

### <a name="parameters"></a>Parametri  

- **ip_ptr** Puntatore all'istanza IP creata in precedenza
- **interface_index** Indice dell'interfaccia a cui è associato l'indirizzo IPv6
- **ip_address** Puntatore all'indirizzo da impostare
- **prefix_length** Lunghezza del prefisso dell'indirizzo (subnet mask)
- **address_index** Puntatore all'indice nella tabella degli indirizzi in cui viene inserito l'indirizzo

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) IPv6 è stato abilitato correttamente
- **NX_NO_MORE_ENTRIES** tabella degli indirizzi IP 0x15 (0x15) è piena
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è incorporata nella libreria NetX Duo.
- **NX_DUPLICATED_ENTRY** (0x52) L'indirizzo IP specificato è già usato in questa istanza IP
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IPv6 non valido
- **NX_INVALID_INTERFACE** (0x4C) punta a un'interfaccia di rete non valida

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
NXD_ADDRESS ip_address;
UINT        address_index;
UINT        interface_index;

ip_address.nxd_ip_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0] = 0x20010000;
ip_address.nxd_ip_address.v6[1] = 0;
ip_address.nxd_ip_address.v6[2] = 0;
ip_address.nxd_ip_address.v6[3] = 1;

/* First create an IP instance with packet pool, source address, and
   driver.*/
status = nx_ip_create(&ip_0, "NetX IP Instance 0",
                     IP_ADDRESS(1,2,3,4),
                     0xFFFFFF00UL, &pool_0,_nx_ram_network_driver,
                     pointer, 2048, 1);

/* Then enable IPv6 on the IP instance. */
status = nxd_ipv6_enable(&ip_0);

/* Set the IPv6 address (a global address as indicated by the 64 bit
   prefix) using the IPv6 address just created on the primary device
   (index zero). The index into the address table is returned in
   address_index. */
interface_index = 0;
status = nxd_ipv6_address_set(&ip_0, interface_index, &ip_address,
                              64,&address_index);

/* A status return of NX_SUCCESS indicates that the IPv6 address is
   successfully assigned to the primary interface (interface 0). */
```

### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_default_router_add"></a>nxd_ipv6_default_router_add
Aggiungere un router IPv6 alla tabella router predefinita

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_default_router_add(
    NX_IP *ip_ptr,
    NXD_ADDRESS *router_address,
    ULONG router_lifetime,
    UINT index_index);
```
### <a name="description"></a>Descrizione

Questo servizio aggiunge un router predefinito IPv6 nell'interfaccia fisica specificata alla tabella del router predefinito. Il servizio IPv4 NetX equivalente è ***nx_ip_gateway_address_set***.

*router_address* deve puntare a un indirizzo IPv6 valido e il router deve essere accessibile direttamente dall'interfaccia fisica specificata.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza
- **router_address** Puntatore all'indirizzo del router predefinito, nell'ordine dei byte dell'host
- **router_lifetime** Durata predefinita del router, in secondi. I valori validi sono:
    - **0xFFFF:** Nessun timeout
    - **0-0xFFFE:** Valore di timeout, in secondi
- **index_index** Puntatore alla posizione di memoria valida per l'indice di rete attraverso il quale è possibile raggiungere il router

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** router predefinito (0x00) è stato aggiunto correttamente
- **NX_NO_MORE_ENTRIES** (0x17) Non sono disponibili altre voci nella tabella del router predefinito.
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IPv6 non valido
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è incorporata nella libreria NetX Duo.
- **NX_INVALID_PARAMETERS** (0x4D) Input indirizzo IPv6 non valido
- **NX_PTR_ERROR** (0x07) Istanza IP o spazio di archiviazione non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_INVALID_INTERFACE** (0x4C) Indice dell'interfaccia router non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* This example adds a default router for the primary interface at
   fe80::1219:B9FF:FE37:ac to the default router table. */

#define PRIMARY_INTERFACE 0

NXD_ADDRESS router_address;

/* Set the router address version to IPv6 */
router_address.nxd_ip_version   = NX_IP_VERSION_V6;

/* Set the IPv6 address, in host byte order. */
router_address.nxd_ip_address[0] = 0xfe800000;
router_address.nxd_ip_address[1] = 0x0;
router_address.nxd_ip_address[2] = 0x1219B9FF;
router_address.nxd_ip_address[3] = 0xFE3700AC;

/* Set IPv6 default router. */
status = nxd_ipv6_default_router_add(ip_ptr, &router_address,
                                     0xFFFF, PRIMARY_INTERFACE);

/* Unless invalid pointer input is detected by the error checking
   Service, status return is always NX_SUCCESS. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nxd_ipv6_default_router_delete"></a>nxd_ipv6_default_router_delete
Rimuovere il router IPv6 dalla tabella router predefinita

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_default_router_delete (
    NX_IP *ip_ptr,
    NXD_ADDRESS *router_address);
```
### <a name="description"></a>Descrizione

Questo servizio elimina un router predefinito IPv6 dalla tabella del router predefinito. Il servizio NetX IPv4 equivalente è ***nx_ip_gateway_address_clear***.

### <a name="restrictions"></a>Restrizioni

L'istanza IP è stata creata. *router_address* deve puntare a informazioni valide.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a un'istanza IP creata in precedenza
- **router_address** Puntatore all'indirizzo del gateway predefinito IPv6

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** router (0x00) eliminato correttamente
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è incorporata nella libreria NetX Duo.
- **NX_NOT_FOUND** (0x4E) Impossibile trovare la voce del router
- **NX_PTR_ERROR** (0x07) Istanza IP o spazio di archiviazione non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_INVALID_PARAMETERS** (0x82) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/*This example removes a default router:fe80::1219:B9FF:FE37:ac */

NXD_ADDRESS router_address;

/* Set the router_address version to IPv6 */
router_address.nxd_ip_version = NX_IP_VERSION_V6;

/* Program the IPv6 address, in host byte order. */
router_address.nxd_ip_address[0] = 0xfe800000;
router_address.nxd_ip_address[1] = 0x0;
router_address.nxd_ip_address[2] = 0x1219B9FF;
router_address.nxd_ip_address[3] = 0xFE3700AC;

/* Delete the IPv6 default router. */
nxd_ipv6_default_router_delete(ip_ptr, &router_address);
```
### <a name="see-also"></a>Vedere anche

- nx_ip_gateway_address_clearnx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_getnx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nxd_ipv6_default_router_entry_get"></a>nxd_ipv6_default_router_entry_get
Ottenere la voce predefinita del router

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_default_router_entry_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    UINT entry_index,
    NXD_ADDRESS *router_addr,
    ULONG *router_lifetime,
    ULONG *prefix_length,
    ULONG *configuration_method);
```
### <a name="description"></a>Descrizione

Questo servizio recupera una voce del router dalla tabella di routing IPv6 predefinita collegata a un dispositivo di rete specificato.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP
- **interface_index** Indice dell'interfaccia di rete
- **entry_index** Indice delle voci
- **router_addr** Indirizzo IPv6 router
- **router_lifetime** Puntatore al tempo di vita del router
- **prefix_length** Puntatore alla lunghezza del prefisso
- **configuration_method** Puntatore alle informazioni sulla configurazione della voce

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Operazione get riuscita
- **NX_NOT_FOUND** (0x4E) Router non trovato
- **NX_INVALID_INTERFACE** (0x4C) Interface index is not valid (Indice dell'interfaccia di 0x4C non valido)
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE 0
NXD_ADDRESS            router_addr;
ULONG                  router_lifetime;
ULONG                  prefix_length;
ULONG                  configuration_method;

/* Get the router entry of specified interface. */
status = nxd_ipv6_default_router_entry_get (&ip_0,
                                            PRIMARY_INTERFACE,
                                            entry_index,
                                            &router_addr,
                                            &router_lifetime,
                                            &prefix_length,
                                            &configuration_method);

/* If status == NX_SUCCESS, the router entry was successfully
   got. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nxd_ipv6_default_router_get"></a>nxd_ipv6_default_router_get
Recuperare un router IPv6 dalla tabella router predefinita

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_default_router_get(
    NX_IP *ip_ptr, 
    UINT interface_index
    NXD_ADDRESS *router_address,
    ULONG *router_lifetime,
    ULONG *prefix_length);
```
### <a name="description"></a>Descrizione

Questo servizio recupera un indirizzo del router predefinito IPv6, la durata e la lunghezza del prefisso nell'interfaccia fisica specificata dalla tabella del router predefinito. Il servizio IPv4 NetX equivalente è ***nx_ip_gateway_address_get*.**

*router_address* deve puntare a una struttura di NXD_ADDRESS valida, in modo che questo servizio possa compilare l'indirizzo IPv6 del router predefinito.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza
- **interface_index** Indice dell'interfaccia di rete tramite cui il router è accessibile
- **router_address** Puntatore allo spazio di archiviazione per il valore restituito dell'indirizzo del router predefinito, nell'ordine dei byte dell'host.
- **router_lifetime** Puntatore alla durata del router
- **prefix_length** Puntatore alla lunghezza del prefisso dell'indirizzo del router

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** router predefinito (0x00) è stato aggiunto correttamente
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è incorporata nella libreria NetX Duo.
- **NX_NOT_FOUND** (0x4E) Router predefinito non trovato
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_INVALID_INTERFACE** (0x4C) Indice dell'interfaccia router non valido
- **NX_PTR_ERROR** (0x07) Istanza IP o spazio di archiviazione non valido

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* This example retrieves a default router for the primary device
   from the default router table. */

#define PRIMARY_INTERFACE 0

NXD_ADDRESS router_address;
ULONG       router_lifetime;
ULONG       prefix_length;

/* Get IPv6 default router. */
status = nxd_ipv6_default_router_get(ip_ptr, PRIMARY_INTERFACE,
                                     &router_address,
                                     &router_lifetime,
                                     &prefix_length);

/* If status returns NX_SUCCESS, the router address and related
   information is returned successfully. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_number_of_entries_get

## <a name="nxd_ipv6_default_router_number_of_entries_get"></a>nxd_ipv6_default_router_number_of_entries_get
Ottenere il numero di router IPv6 predefiniti

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_default_router_number_of_entries_get(
    NX_IP *ip_ptr,
    UINT interface_index,
    UINT *num_entries);
```
### <a name="description"></a>Descrizione

Questo servizio recupera il numero di router IPv6 predefiniti configurati in una determinata interfaccia di rete.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore a blocco di controllo IP
- **interface_index** Indice dell'interfaccia di rete
- **num_entries** Destinazione per il numero di router IPv6 in un dispositivo di rete specificato

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Operazione get riuscita
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è incorporata nella libreria NetX Duo.
- **NX_INVALID_INTERFACE** (0x4C) Il valore di indice del dispositivo non è valido
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido o num_entries puntatore

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE 0
UINT                   num_entries;

/* Get the router entries of specified interface. */
status = nxd_ipv6_default_router_number_of_entries_get(&ip_0,
                                                       PRIMARY_INTERFACE,
                                                       &num_entries);

/* If status == NX_SUCCESS, the router entries was successfully
   retrieved. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_gateway_address_clear
- nx_ip_gateway_address_get
- nx_ip_gateway_address_set
- nx_ip_info_get
- nx_ip_static_route_add
- nx_ip_static_route_delete
- nxd_ipv6_default_router_add
- nxd_ipv6_default_router_delete
- nxd_ipv6_default_router_entry_get
- nxd_ipv6_default_router_get

## <a name="nxd_ipv6_disable"></a>nxd_ipv6_disable
Disabilitare la funzionalità IPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_disable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio disabilita il protocollo IPv6 per l'istanza IP specificata. Cancella anche la tabella del router predefinita, la cache ND e la tabella degli indirizzi IPv6, lascia tutti i gruppi multicast e reimposta le variabili di richiesta del router. Questo servizio non ha alcun effetto se IPv6 non è abilitato.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Disabilitazione riuscita
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è incorporata nella libreria NetX Duo.
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_NOT_SUPPORT** modulo IPv6 (0x4B) non è compilato
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* Disable IPv6 feature on this IP instance. */
status = nxd_ipv6_disable(&ip_0);

/* If status == NX_SUCCESS, disables IPv6 feature on IP instance.*/
```
### <a name="see-also"></a>Vedere anche 

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_enable"></a>nxd_ipv6_enable
Abilitare i servizi IPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_enable(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio abilita i servizi IPv6. Quando i servizi IPv6 sono abilitati, l'istanza IP viene aggiunta al gruppo multicast tutti i nodi (FF02::1). Questo servizio non imposta l'indirizzo locale del collegamento o l'indirizzo globale. Le applicazioni devono usare *nxd_ipv6_address_set* per configurare gli indirizzi di rete del dispositivo. Non esiste alcun equivalente NetX.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) IPv6 è stato abilitato correttamente
- **NX_ALREADY_ENABLED** (0x15) IPv6 è già abilitato
- **NX_NOT_SUPPORTED** (0x4B) la funzionalità IPv6 non è incorporata nella libreria NetX Duo.
- **NX_PTR_ERROR** (0x07) Puntatore IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* First create an IP instance with packet pool, source address, and
   driver.*/
status = nx_ip_create(&ip_0, "NetX IP Instance 0",
                      IP_ADDRESS(1,2,3,4),
                      0xFFFFFF00UL, &pool_0,_nx_ram_network_driver,
                      pointer, 2048, 1);

/* Then enable IPv6 on the IP instance. */
status = nxd_ipv6_enable(&ip_0);

/* A status return of NX_SUCCESS indicates that the IP instance is
   enabled for IPv6 services. */
```
### <a name="see-also"></a>Vedere anche

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_stateless_address_autoconfig_disable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_multicast_interface_join"></a>nxd_ipv6_multicast_interface_join
Aggiungere un gruppo multicast IPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_multicast_interface_join(
    NX_IP *ip_ptr,
    NXD_ADDRESS *group_address,
    UINT interface_index);
```

### <a name="description"></a>Descrizione

Questo servizio consente a un'applicazione di aggiungere un indirizzo multicast IPv6 specifico in un'interfaccia di rete specifica. Al driver di collegamento viene notificato di aggiungere l'indirizzo multicast. Questo servizio è disponibile se la libreria NetX Duo viene compilata con ***l'opzione NX_ENABLE_IPV6_MULTICAST*** definita.

### <a name="parameters"></a>Parametri  

- **ip_ptr** Puntatore all'istanza IP
- **group_address** Indirizzo multicast IPv6
- **interface_index** Indice dell'interfaccia di rete associata al gruppo multicast

### <a name="return-values"></a>Valori restituiti  

- **NX_SUCCESS** (0x00) Abilita correttamente la ricezione sull'indirizzo multicast IPv6
- **NX_NO_MORE_ENTRIES** (0x17) Non sono presenti altre voci nella tabella multicast IPv6.
- **NX_OVERFLOW** (0x03) Nessun altro indirizzo di gruppo disponibile nel driver di dispositivo
- **NX_NOT_SUPPORTED** funzionalità IPv6 (0x4B) o multicast IPv6 non è incorporata nella libreria NetX Duo
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IPv6 non valido
- **NX_INVALID_INTERFACE** (0x4C) L'indice dell'interfaccia non è valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE 0

/* Join multicast group on this IP instance. */
status = nxd_ipv6_multicast_interface_join(&ip_0,
                                           &group_address,
                                           PRIMARY_INTERFACE);

/* If status == NX_SUCCESS, interface of index on IP instance
   has joined the multicast group. */
```
### <a name="see-also"></a>Vedere anche

- nx_igmp_enable
- nx_igmp_info_getnx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_leave

## <a name="nxd_ipv6_multicast_interface_leave"></a>nxd_ipv6_multicast_interface_leave
Lasciare un gruppo multicast IPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_multicast_interface_leave(
    NX_IP *ip_ptr,
    NXD_ADDRESS *group_address,
    UINT interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio rimuove l'indirizzo multicast IPv6 specifico dal dispositivo di rete specifico. Il driver di collegamento viene inoltre informato della rimozione dell'indirizzo multicast IPv6. Questo servizio è disponibile se la libreria NetX Duo viene compilata con ***l'opzione NX_ENABLE_IPV6_MULTICAST*** definita.

### <a name="parameters"></a>Parametri  

- **ip_ptr** Puntatore all'istanza IP
- **group_address** Indirizzo multicast IPv6
- **interface_index** Indice dell'interfaccia di rete associata al gruppo

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Lasciare multicast riuscito
- **NX_ENTRY_NOT_FOUND** (0x16) Voce non trovata
- **NX_NOT_SUPPORTED** funzionalità IPv6 (0x4B) o multicast IPv6 non è incorporata nella libreria NetX Duo
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IPv6 non valido
- **NX_INVALID_INTERFACE** (0x4C) L'indice dell'interfaccia non è valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE 0

/* Leave multicast address on this IP instance. */
status = nxd_ipv6_multicast_interface_leave(&ip_0,
                                            &group_address,
                                            primary_interface);

/* If status == NX_SUCCESS, interface of index on IP instance
   has left the multicast group. */
```
### <a name="see-also"></a>Vedere anche

- nx_igmp_enable
- nx_igmp_info_get
- nx_igmp_loopback_disable
- nx_igmp_loopback_enable
- nx_igmp_multicast_interface_join
- nx_igmp_multicast_join
- nx_igmp_multicast_interface_leave
- nx_igmp_multicast_leave
- nx_ipv4_multicast_interface_join
- nx_ipv4_multicast_interface_leave
- nxd_ipv6_multicast_interface_join

## <a name="nxd_ipv6_stateless_address_autoconfig_disable"></a>nxd_ipv6_stateless_address_autoconfig_disable
Disabilitare la configurazione automatica degli indirizzi senza stato

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_stateless_address_autoconfig_disable(
    NX_IP *ip_ptr,
    UINT interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio disabilita la funzionalità di configurazione automatica degli indirizzi senza stato IPv6 in un dispositivo di rete specificato. Non ha alcun effetto se l'indirizzo IPv6 è stato configurato.

Questo servizio è disponibile se la libreria NetX Duo viene compilata con ***l'opzione NX_IPV6_STATELESS_AUTOCONFIG_CONTROL*** definita.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP
- **interface_index** Indice dell'interfaccia di rete in cui deve essere disabilitata la configurazione automatica degli indirizzi senza stato IPv6.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Disabilita correttamente la funzionalità di configurazione automatica degli indirizzi senza stato.
- **NX_NOT_SUPPORTED** funzionalità IPv6 (0x4B) o la funzionalità di controllo della configurazione automatica degli indirizzi senza stato IPv6 non è incorporata nella libreria NetX Duo
- **NX_INVALID_INTERFACE** (0x4C) L'indice dell'interfaccia non è valido
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE 0

/* Disable stateless address auto configuration on this IP instance. */
status = nxd_ipv6_stateless_address_autoconfig_disable(&ip_0,
                                                       PRIMARY_INTERFACE);

/* If status == NX_SUCCESS, disables stateless address auto
   configuration on IP instance. */
```
### <a name="see-also"></a>Vedere anche 

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_enable

## <a name="nxd_ipv6_stateless_address_autoconfig_enable"></a>nxd_ipv6_stateless_address_autoconfig_enable
Abilitare la configurazione automatica degli indirizzi senza stato

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_ipv6_stateless_address_autoconfig_enable(
    NX_IP *ip_ptr,
    UINT interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio abilita la funzionalità di configurazione automatica degli indirizzi senza stato IPv6 in un dispositivo di rete specificato.

Questo servizio è disponibile se la libreria NetX Duo viene compilata con ***l'opzione NX_IPV6_STATELESS_AUTOCONFIG_CONTROL*** definita.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP
- **interface_index** Indice dell'interfaccia di rete in cui deve essere abilitata la configurazione automatica degli indirizzi senza stato IPv6.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) Abilita correttamente la funzionalità di configurazione automatica degli indirizzi senza stato.
- **NX_ALREADY_ENABLED** (0x15) Già abilitato
- **NX_NOT_SUPPORTED** funzionalità IPv6 (0x4B) o la funzionalità di controllo della configurazione automatica degli indirizzi senza stato IPv6 non è incorporata nella libreria NetX Duo
- **NX_INVALID_INTERFACE** (0x4C) L'indice dell'interfaccia non è valido
- **NX_PTR_ERROR** (0x07) Puntatore a blocco di controllo IP non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

inizializzazione, thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
#define PRIMARY_INTERFACE

/* Enable stateless address auto configuration on this
   IP instance. */
status = nxd_ipv6_stateless_address_autoconfig_enable(&ip_0,
                                                      PRIMARY_INTERFACE);

/* If status == NX_SUCCESS, enables stateless address auto
   configuration on IP instance. */
```
### <a name="see-also"></a>Vedere anche 

- nx_ip_auxiliary_packet_pool_set
- nx_ip_address_change_notify
- nx_ip_address_get
- nx_ip_address_set
- nx_ip_create
- nx_ip_delete
- nx_ip_driver_direct_command
- nx_ip_driver_interface_direct_command
- nx_ip_forwarding_disable
- nx_ip_forwarding_enable
- nx_ip_fragment_disable
- nx_ip_fragment_enable
- nx_ip_info_get
- nx_ip_max_payload_size_find
- nx_ip_status_check
- nx_system_initialize
- nxd_ipv6_address_change_notify
- nxd_ipv6_address_delete
- nxd_ipv6_address_get
- nxd_ipv6_address_set
- nxd_ipv6_disable
- nxd_ipv6_enable
- nxd_ipv6_stateless_address_autoconfig_disable

## <a name="nxd_nd_cache_entry_delete"></a>nxd_nd_cache_entry_delete
Eliminare la voce indirizzo IPv6 nella cache dei router adiacenti

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_nd_cache_entry_delete(
    NX_IP *ip_ptr, 
    ULONG *ip_address);
```
### <a name="description"></a>Descrizione

Questo servizio elimina una voce della cache di individuazione adiacente IPv6 per l'indirizzo IP fornito. La funzione NetX IPv4 equivalente è ***nx_arp_static_entry_delete***.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP creata in precedenza
- **ip_address** Puntatore all'indirizzo IPv6 da eliminare, nell'ordine dei byte dell'host

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'indirizzo è stato eliminato
- **NX_ENTRY_NOT_FOUND** (0x16) non trovato nella cache adiacente IPv6
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è incorporata nella libreria NetX Duo
- **NX_PTR_ERROR** (0x07) Istanza IP o spazio di archiviazione non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* This example deletes an entry from the neighbor cache table. */

NXD_ADDRESS ip_address;

ip_address.nxd_ip_address_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0]   = 0x20011234;
ip_address.nxd_ip_address.v6[1]   = 0x56780000;
ip_address.nxd_ip_address.v6[2]   = 0;
ip_address.nxd_ip_address.v6[3]   = 1;

/* Delete an entry in the neighbor cache table with the specified IPv6
   address and hardware address. */
status = nxd_nd_cache_entry_delete(&ip_0,
                                   &ip_address.nxd_ip_address.v6[0]);

/* If status == NX_SUCCESS, the entry was deleted from the neighbor cache
   table. */
```
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nxd_nd_cache_entry_set"></a>nxd_nd_cache_entry_set
Aggiungere un mapping indirizzo IPv6/MAC alla cache adiacente

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_nd_cache_entry_set(
    NX_IP *ip_ptr, 
    NXD_ADDRESS *dest_ip,
    UINT interface_index, 
    char *mac);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge una voce alla cache di individuazione adiacente per l'indirizzo IP specificato *ip_address* mappato all'indirizzo MAC hardware nell'indice dell'interfaccia di rete (interface_index). Il servizio IPv4 NetX equivalente è ***nx_arp_static_entry_create***.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza
- **dest_ip** Puntatore all'istanza dell'indirizzo IPv6
- **interface_index** Indice che specifica l'interfaccia di rete fisica in cui è possibile raggiungere l'indirizzo IPv6 di destinazione 
- **mac** Puntatore all'indirizzo hardware.

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) entry successfully added (Aggiunta della voce (0x00) completata
- **NX_NOT_SUCCESSFUL** (0x43) Cache non valida o nessuna voce della cache adiacente disponibile
- **NX_NOT_SUPPORTED** (0x4B) IPv6 non è incorporata nella libreria NetX Duo
- **NX_PTR_ERROR** (0x07) Istanza IP o spazio di archiviazione non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_INVALID_INTERFACE** (0x4C) Valore di indice dell'interfaccia non valido.

### <a name="allowed-from"></a>Consentito da

Inizializzazione, thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
/* This example adds an entry on the primary network interface to
   the neighbor cache table. */

#define PRIMARY_INTEFACE 0

NXD_ADDRESS ip_address;
UCHAR hw_address[6] = {0x0, 0xcf,0x01,0x02, 0x03, 0x04};
CHAR  *mac;

mac = (CHAR *)&hw_address[0];

ip_address.nxd_ip_address_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0]   = 0x20011234;
ip_address.nxd_ip_address.v6[1]   = 0x56780000;
ip_address.nxd_ip_address.v6[2]   = 0;
ip_address.nxd_ip_address.v6[3]   = 1;

/* Create an entry in the neighbor cache table with the specified
   IPv6 address and hardware address. */
status = nxd_nd_cache_entry_set(&ip_0,
                                &ip_address.nxd_ip_address.v6[0],
                                PRIMARY_INTERFACE, mac);

/* If status == NX_SUCCESS, the entry was added to the neighbor
   cache table. */
```
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nxd_nd_cache_hardware_address_find"></a>nxd_nd_cache_hardware_address_find
Individuare l'indirizzo hardware per un indirizzo IPv6

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_nd_cache_hardware_address_find(
    NX_IP *ip_ptr,
    NXD_ADDRESS *ip_address,
    ULONG *physical_msw,
    ULONG *physical_lsw
    UINT *interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio tenta di trovare un indirizzo hardware fisico nella cache di individuazione adiacente IPv6 associata all'indirizzo IPv6 fornito. L'indice dell'interfaccia di rete tramite cui è possibile raggiungere l'elemento adiacente viene restituito anche nel parametro *interface_index.* Il servizio NetX IPv4 equivalente è ***nx_arp_hardware_address_find***.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza
- **ip_address** Puntatore all'indirizzo IP da trovare, ordine dei byte dell'host
- **physical_msw** Puntatore ai primi 16 bit (47-32) dell'indirizzo fisico, nell'ordine dei byte dell'host 
- **physical_lsw** Puntatore ai 32 bit inferiori (31-0) dell'indirizzo fisico nell'ordine dei byte dell'host
- **interface_index** Puntatore alla posizione di memoria valida per l'indice di interfaccia che specifica il dispositivo di rete in cui è possibile raggiungere l'indirizzo IPv6.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'indirizzo è stato trovato correttamente
- **NX_ENTRY_NOT_FOUND** (0x16) Mapping non presente nella cache adiacente
- **NX_NOT_SUPPORTED** (0x4B) la funzionalità IPv6 non è incorporata nella libreria NetX Duo
- **NX_INVALID_PARAMETERS** (0x4D) L'indirizzo IP fornito non è la versione 6.
- **NX_PTR_ERROR** (0x07) Spazio di archiviazione o istanza IP non valida
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* This example inputs an IP address on the primary network in order
   to obtain the hardware address it is mapped to in the neighbor
   cache able. */

NXD_ADDRESS  ip_address;
ULONG physical_msw, physical_lsw;
UINT  interface_index;

ip_address.nxd_ip_address_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0]   = 0x20011234;
ip_address.nxd_ip_address.v6[1]   = 0x56780000;
ip_address.nxd_ip_address.v6[2]   = 0;
ip_address.nxd_ip_address.v6[3]   = 1;

/* Obtain the hardware address mapped to the supplied global IPv6
   address. */
status = nxd_nd_cache_hardware_address_find(&ip_0, &ip_address,
                                            &physical_msw,
                                            &physical_lsw
                                            &interface_index);

/* If status == NX_SUCCESS, a matching entry was found in the
   neighbor cache table and the hardware address returned in
   variables physical_msw and physical_lsw, the index of the network
   interface through which the neighbor can be reached is stored in
   interface_index. */
```
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_invalidate
- nxd_nd_cache_ip_address_find

## <a name="nxd_nd_cache_invalidate"></a>nxd_nd_cache_invalidate
Invalidare la cache dell'individuazione adiacente

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_nd_cache_invalidate(NX_IP *ip_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio invalida l'intera cache di individuazione adiacente IPv6. Questo servizio può essere richiamato prima o dopo che ICMPv6 è stato abilitato. Questo servizio non è applicabile alla connettività IPv4, quindi non esiste alcun servizio equivalente a NetX.

### <a name="parameters"></a>Parametri

- **ip_ptr** Puntatore all'istanza IP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Cache invalidata correttamente
- **NX_NOT_SUPPORTED** (0x4B) la funzionalità IPv6 non è incorporata nella libreria NetX Duo
- **NX_PTR_ERROR** (0x07) Istanza IP non valida
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* This example invalidates the host neighbor cache table. */

/* Invalidate the cache table bound to the IP instance. */
status = nxd_nd_cache_invalidate (&ip_0);

/* If status == NX_SUCCESS, all entries in the neighbor cache table
   are invalidated. */
```
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_ip_address_find

## <a name="nxd_nd_cache_ip_address_find"></a>nxd_nd_cache_ip_address_find
Recuperare l'indirizzo IPv6 per un indirizzo fisico

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_nd_cache_ip_address_find(
    NX_IP *ip_ptr,
    NXD_ADDRESS *ip_address,
    ULONG physical_msw,
    ULONG physical_lsw,
    UINT *interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio tenta di trovare un indirizzo IPv6 nella cache di individuazione adiacente IPv6 associata all'indirizzo fisico fornito. Viene restituito anche l'indice dell'interfaccia di rete tramite cui è possibile raggiungere l'adiacente. Il servizio NetX IPv4 equivalente è ***nx_arp_ip_address_find***.

### <a name="parameters"></a>Parametri 

- **ip_ptr** Puntatore all'istanza IP creata in precedenza
- **ip_address** Puntatore a una struttura NXD_ADDRESS valida
- **physical_msw** Primi 16 bit (47-32) dell'indirizzo fisico da trovare, ordine dei byte host
- **physical_lsw** 32 bit inferiori (31-0) dell'indirizzo fisico da trovare, ordine dei byte host
- **interface_index** Puntatore all'indice del dispositivo di rete tramite il quale è possibile raggiungere l'indirizzo IPv6

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) L'indirizzo è stato trovato correttamente
- **NX_ENTRY_NOT_FOUND** (0x16) Indirizzo fisico non trovato nella cache adiacente
- **NX_NOT_SUPPORTED** (0x4B) la funzionalità IPv6 non è incorporata nella libreria NetX Duo
- **NX_PTR_ERROR** (0x07) Spazio di archiviazione o istanza IP non valida
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio 
- **NX_INVALID_PARAMETERS** (0x4D) l'indirizzo MAC è zero.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* This example inputs a hardware address to search on for the
   matching IPv6 global address in the neighbor cache table. */

NXD_ADDRESS ip_address;
ULONG physical_msw = 0xcf;
ULONG physical_lsw = 0x01020304;
UINT  interface_index;

/* Obtain the IPv6 address mapped to the supplied hardware
   Address on the primary device. */
status = nxd_nd_cache_ip_address_find(&ip_0, &ip_address,
                                      physical_msw, physical_lsw,
                                      &interface_index);

/* If status == NX_SUCCESS, a matching entry was found in the
   neighbor cache table and the global IPv6 address returned in
   variable ip_address. */
```
### <a name="see-also"></a>Vedere anche

- nx_arp_dynamic_entries_invalidate
- nx_arp_dynamic_entry_set
- nx_arp_enable
- nx_arp_entry_delete
- nx_arp_gratuitous_send
- nx_arp_hardware_address_find
- nx_arp_info_get
- nx_arp_ip_address_find
- nx_arp_static_entries_delete
- nx_arp_static_entry_create
- nx_arp_static_entry_delete
- nxd_nd_cache_entry_delete
- nxd_nd_cache_entry_set
- nxd_nd_cache_hardware_address_find
- nxd_nd_cache_invalidate

## <a name="nxd_tcp_client_socket_connect"></a>nxd_tcp_client_socket_connect
Stabilire una connessione TCP

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_tcp_client_socket_connect(
    NX_TCP_SOCKET *socket_ptr
    NXD_ADDRESSS *server_ip,
    UINT server_port,
    ULONG wait_option);
```
### <a name="description"></a>Descrizione

Questo servizio esegue la connessione TCP usando un socket client TCP creato in precedenza alla porta del server specificato. Questo servizio funziona su reti IPv4 o IPv6. Le porte del server TCP valide sono da 0 a 0xFFFF. NetX Duo determina l'interfaccia fisica appropriata in base all'indirizzo IP del server. L'equivalente netx IPv4 è ***nx_tcp_client_socket_connect***.

Il socket deve essere stato associato a una porta locale.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP creato in precedenza
- **server_ip** Puntatore all'indirizzo di destinazione IPv4 o IPv6, in ordine di byte host
- **server_port** Numero di porta del server a cui connettersi (da 1 a 0xFFFF), nell'ordine dei byte dell'host
- **wait_option** Opzione di attesa durante la connessione. Le opzioni di attesa sono definite nel modo seguente:
    - **NX_NO_WAIT** (0x00000000)
    - **NX_WAIT_FOREVER** (0xFFFFFFFF)
    - **valore di timeout nei tick** (da 0x00000001 a 0xFFFFFFFE)

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Connessione socket riuscita
- **NX_WAIT_ABORTED** (0x1A) La sospensione richiesta è stata interrotta da una chiamata a tx_thread_wait_abort
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IPv4 o IPv6 del server non valido
- **NX_NOT_BOUND** (0x24) Il socket non è associato
- **NX_NOT_CLOSED** (0x35) Il socket non è in stato chiuso
- **NX_IN_PROGRESS** (0x37) Non è stata specificata alcuna attesa, è in corso un tentativo di connessione
- **NX_INVALID_INTERFACE** (0x4C) Indice di interfaccia non valido.
- **NX_NO_INTERFACE_ADDRESS** (0x50) L'interfaccia di rete non ha un indirizzo IPv6 valido
- **NX_NOT_ENABLED** TCP (0x14) non abilitato
- **NX_INVALID_PORT** (0x46) Porta non valida
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_NOT_CONNECTED** (0x38) La connessione ha esito negativo.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
NXD_ADDRESS peer_ip_address;
ULONG       peer_port;

/* Set Peer IPv6 address */
peer_ip_address.nxd_ip_version = NX_IP_VERSION_V6;
peer_ip_address.nxd_ip_address.v6[0] = 0x20010000;
peer_ip_address.nxd_ip_address.v6[1] = 0;
peer_ip_address.nxd_ip_address.v6[2] = 0;
peer_ip_address.nxd_ip_address.v6[3] = 0x101;

/* Set peer port number */
peer_port = 2563;

/* Connect to the peer */
status = nxd_tcp_client_socket_connect(socket_ptr,
                                       &peer_ip_address,
                                       peer_port, NX_WAIT_FOREVER);
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_socket_peer_info_get

## <a name="nxd_tcp_socket_peer_info_get"></a>nxd_tcp_socket_peer_info_get
Recupera l'indirizzo IP del socket TCP peer e il numero di porta

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_tcp_socket_peer_info_get
    (NX_TCP_SOCKET *socket_ptr,
    NXD_ADDRESS *peer_ip_address,
    ULONG *peer_port);
```
### <a name="description"></a>Descrizione

Questo servizio recupera le informazioni sull'indirizzo IP peer e sulla porta per il socket TCP connesso tramite la rete IPv4 o IPv6. Il servizio NetX IPv4 equivalente è ***nx_tcp_socket_peer_info_get***.

Si noti *socket_ptr* deve puntare a un socket TCP che si trova già nello stato connesso.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore al socket TCP connesso all'host peer
- **peer_ip_address** Puntatore all'indirizzo peer IPv4 o IPv6. L'indirizzo IP restituito è in ordine di byte host.
- **peer_port** Puntatore al numero di porta peer. Il numero di porta restituito è in ordine di byte host.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Le informazioni sul socket sono state recuperate correttamente
- **NX_NOT_CONNECTED** (0x38) Socket non connesso al peer
- **NX_NOT_ENABLED** TCP (0x14) non abilitato
- **NX_PTR_ERROR** (0x07) Input puntatore non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
NXD_ADDRESS  peer_ip_address;
ULONG        peer_port;

/* Get TCP socket information. */
status = nxd_tcp_socket_peer_info_get(socket_ptr, &peer_ip_address,
                                      &peer_port);

/* If status == NX_SUCCESS, the service returns valid peer info: */
if(peer_ip_address.nxd_ip_version == NX_IP_VERSION_V4)
    /* Peer IP address is stored in
       peer_ip_address.nxd_ip_address.v4 */

if(peer_ip_address.nxd_ip_version == NX_IP_VERSION_V6)
    /* Peer IP address is stored in
       peer_ip_address.nxd_ip_address.v6 */
```
### <a name="see-also"></a>Vedere anche

- nx_tcp_client_socket_bind
- nx_tcp_client_socket_connect
- nx_tcp_client_socket_port_get
- nx_tcp_client_socket_unbind
- nx_tcp_enable
- nx_tcp_free_port_find
- nx_tcp_info_get
- nx_tcp_server_socket_accept
- nx_tcp_server_socket_listen
- nx_tcp_server_socket_relisten
- nx_tcp_server_socket_unaccept
- nx_tcp_server_socket_unlisten
- nx_tcp_socket_bytes_available
- nx_tcp_socket_create
- nx_tcp_socket_delete
- nx_tcp_socket_disconnect
- nx_tcp_socket_info_get
- nx_tcp_socket_receive
- nx_tcp_socket_receive_queue_max_set
- nx_tcp_socket_send
- nx_tcp_socket_state_wait
- nxd_tcp_client_socket_connect

## <a name="nxd_udp_packet_info_extract"></a>nxd_udp_packet_info_extract
Estrarre i parametri di rete dal pacchetto UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_udp_packet_info_extract(
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *ip_address,
    UINT *protocol,
    UINT *port,
    UINT *interface_index);
```
### <a name="description"></a>Descrizione

Questo servizio estrae i parametri di rete da un pacchetto ricevuto su reti UDP IPv4 o IPv6. Il servizio equivalente NetX è ***nx_udp_packet_info_extract.***

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto.
- **ip_address** Puntatore all'indirizzo IP del mittente.
- **protocollo** Puntatore al protocollo da restituire.
- **porta** Puntatore al numero di porta del mittente.
- **interface_index** Puntatore all'indice dell'interfaccia di rete da cui viene ricevuto il pacchetto

### <a name="return-values"></a>Valori restituiti 

- **NX_SUCCESS** (0x00) I dati dell'interfaccia di pacchetto sono stati estratti correttamente.
- **NX_INVALID_PACKET** (0x12) Il pacchetto non è IPv4 o IPv6.
- **NX_PTR_ERROR** (0x07) Input puntatore non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
/* Extract network data from UDP packet interface.*/
status = nxd_udp_packet_info_extract(packet_ptr, &ip_address,
                                    &protocol, &port,
                                    &interface_index);

/* If status is NX_SUCCESS packet data was successfully retrieved.*/
```
### <a name="see-also"></a>Vedere anche 

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nxd_udp_socket_send"></a>nxd_udp_socket_send
Inviare un datagramma UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_udp_socket_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *ip_address,
    UINT port);
```
### <a name="description"></a>Descrizione

Questo servizio invia un datagramma UDP tramite un socket UDP creato in precedenza e associato per reti IPv4 o IPv6. NetX Duo trova un indirizzo IP locale appropriato come indirizzo di origine in base all'indirizzo IP di destinazione. Per specificare un'interfaccia e un indirizzo IP di origine specifici, l'applicazione deve usare il ***nxd_udp_socket_source_send*** servizio.

Si noti che questo servizio restituisce immediatamente indipendentemente dal fatto che il datagramma UDP sia stato inviato correttamente. Il servizio equivalente NetX (IPv4) è ***nx_udp_socket_send***.

Il socket deve essere associato a una porta locale.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore all'istanza del socket UDP creata in precedenza
- **packet_ptr** Puntatore a pacchetti di datagrammi UDP
- **ip_address** Puntatore all'indirizzo IPv4 o IPv6 di destinazione
- **porta** Numero di porta di destinazione valido compreso tra 1 e 0xFFFF), nell'ordine dei byte dell'host

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio socket UDP riuscito
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IPv4 o IPv6 del server non valido
- **NX_NOT_BOUND** (0x24) Socket non associato ad alcuna porta
- **NX_NO_INTERFACE_ADDRESS** (0x50) Non è possibile trovare un'interfaccia in uscita appropriata.
- **NX_UNDERFLOW** (0x02) Spazio insufficiente per l'intestazione UDP nel pacchetto
- **NX_OVERFLOW** (0x03) Il puntatore di accodamento del pacchetto non è valido
- **NX_PTR_ERROR** (0x07) Puntatore socket, puntatore di indirizzo o puntatore a pacchetto non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_NOT_ENABLED** (0x14) UDP non è stato abilitato
- **NX_INVALID_PORT** (0x46) Il numero di porta non è compreso in un intervallo valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Possibile preemption

No

### <a name="example"></a>Esempio

```c
NXD_ADDRESS ip_address, server_address;

/* Set the UDP Client IPv6 address. */
ip_address.nxd_ip_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0] = 0x20010000;
ip_address.nxd_ip_address.v6[1] = 0;
ip_address.nxd_ip_address.v6[2] = 0;
ip_address.nxd_ip_address.v6[3] = 1;

/* Set the UDP server IPv6 address to send to. */
server_address.nxd_ip_version = NX_IP_VERSION_V6;
server_address.nxd_ip_address.v6[0] = 0x20010000;
server_address.nxd_ip_address.v6[1] = 0;
server_address.nxd_ip_address.v6[2] = 0;
server_address.nxd_ip_address.v6[3] = 2;

/* Set the global address (indicated by the 64 bit prefix) using the
   IPv6 address just created on the primary device (index 0). We
   don’t need the index into the address table, so the last argument
   is set to null. */

interface_index = 0;
status = nxd_ipv6_address_set(&client_ip, interface_index,
                              &ip_address, 64, NX_NULL);

/* Create the UDP socket client_socket with the ip_address and
   allocate a packet pointed to by packet_ptr (not shown). */

/* Send a packet to the UDP server at server_address on port 12. */
status = nxd_udp_socket_send(&client_socket, packet_ptr,
                             &server_address, 12);

/* If status == NX_SUCCESS, the UDP host successfully transmitted
   the packet out the UDP socket to the server. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_source_send
- nxd_udp_source_extract

## <a name="nxd_udp_socket_source_send"></a>nxd_udp_socket_source_send
Inviare un datagramma UDP

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_udp_socket_source_send(
    NX_UDP_SOCKET *socket_ptr,
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *ip_address,
    UINT port, 
    UINT address_index);
```
### <a name="description"></a>Descrizione

Questo servizio invia un datagramma UDP tramite un socket UDP creato e associato in precedenza per reti IPv4 o IPv6. Il parametro *address_index* specifica l'indirizzo IP di origine da usare per il pacchetto in uscita. Si noti che la funzione restituisce immediatamente indipendentemente dal fatto che il datagramma UDP sia stato inviato correttamente.

Il socket deve essere associato a una porta locale.

Il servizio equivalente NetX (IPv4) ***è nx_udp_socket_source_send***.

### <a name="parameters"></a>Parametri

- **socket_ptr** Puntatore a un'istanza del socket UDP creata in precedenza
- **packet_ptr** Puntatore al pacchetto del datagramma UDP
- **ip_address** Puntatore alla porta dell'indirizzo IPv4 o IPv6 di destinazione Numero di porta di destinazione valido compreso tra 1 e 0xFFFF), nell'ordine dei byte dell'host
- **address_index** Indice che specifica l'indirizzo di origine da usare per il pacchetto

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Invio socket UDP riuscito
- **NX_IP_ADDRESS_ERROR** (0x21) Indirizzo IPv4 o IPv6 del server non valido
- **NX_NOT_BOUND** (0x24) Socket non associato ad alcuna porta
- **NX_NO_INTERFACE_ADDRESS** (0x50) Non è possibile trovare alcuna interfaccia in uscita appropriata.
- **NX_NOT_FOUND** (0x4E) Non è possibile trovare alcuna interfaccia appropriata
- **NX_PTR_ERROR** (0x07) Puntatore socket, indirizzo o puntatore a pacchetto non valido.
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio
- **NX_NOT_ENABLED** udp (0x14) non è stato abilitato
- **NX_INVALID_PORT** (0x46) Il numero di porta non è compreso nell'intervallo valido.
- **NX_INVALID_INTERFACE** (0x4C) L'interfaccia di rete specificata è valida
- **NX_UNDERFLOW** (0x02) Spazio insufficiente per l'intestazione UDP nel pacchetto
- **NX_OVERFLOW** (0x03) Puntatore di accodamento pacchetti non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
NXD_ADDRESS ip_address, server_address;
UINT address_index;

/* Set the UDP Client IPv6 address. */
ip_address.nxd_ip_version = NX_IP_VERSION_V6;
ip_address.nxd_ip_address.v6[0] = 0x20010000;
ip_address.nxd_ip_address.v6[1] = 0;
ip_address.nxd_ip_address.v6[2] = 0;
ip_address.nxd_ip_address.v6[3] = 1;

/* Set the UDP server IPv6 address to send to. */
server_address.nxd_ip_version = NX_IP_VERSION_V6;
server_address.nxd_ip_address.v6[0] = 0x20010000;
server_address.nxd_ip_address.v6[1] = 0;
server_address.nxd_ip_address.v6[2] = 0;
server_address.nxd_ip_address.v6[3] = 2;

/* Set the global address (indicated by the 64 bit prefix) using the IPv6
   address just created on the primary device (index 0). The address index
   is needed for nxd_udp_socket_source_send. */

status = nxd_ipv6_address_set(&client_ip, 0,
                              &ip_address, 64, &address_index);

/* Create the UDP socket client_socket with the ip_address and
   allocate a packet pointed to by packet_ptr (not shown). */

/* Send a packet to the UDP server at server_address on port 12. */
status = nxd_udp_socket_source_send(&client_socket, packet_ptr,
                                    &server_address, 12, address_index);

/* If status == NX_SUCCESS, the UDP host successfully transmitted the
   packet out the UDP socket to the server. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_source_extract

## <a name="nxd_udp_source_extract"></a>nxd_udp_source_extract
Recuperare le informazioni sull'origine dei pacchetti UPD

### <a name="prototype"></a>Prototipo  

```c
UINT nxd_udp_source_extract(
    NX_PACKET *packet_ptr,
    NXD_ADDRESS *ip_address, 
    UINT *port);
```
### <a name="description"></a>Descrizione

Questo servizio estrae l'indirizzo IP di origine e il numero di porta da un pacchetto UDP ricevuto tramite il socket UDP dell'host. L'equivalente NetX (IPv4) ***è nx_udp_source_extract***.

### <a name="parameters"></a>Parametri

- **packet_ptr** Puntatore al pacchetto UDP ricevuto
- **ip_address** Puntatore alla struttura NXD_ADDRESS per archiviare l'indirizzo IP di origine dei pacchetti
- **porta** Puntatore al numero di porta del socket UDP

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Estrazione origine riuscita
- **NX_INVALID_PACKET** pacchetto (0x12) non è valido
- **NX_PTR_ERROR** (0x07) Puntatore socket non valido
- **NX_CALLER_ERROR** (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="preemption-possible"></a>Preemption Possible

No

### <a name="example"></a>Esempio

```c
NXD_ADDRESS ip_address;
UINT         port;

/* Create the UDP socket client_socket and
   allocate the packet pointed to by packet_ptr (not shown). */

/* Extract the IP address and port of the packet received on the UDP
   socket specified in the packet interface. */
status = nxd_udp_source_extract(&packet_ptr, &ip_address, &port);

/* If status == NX_SUCCESS, the source IP address and port of the
   packet received on the UDP socket was successfully extracted. */
```
### <a name="see-also"></a>Vedere anche

- nx_udp_enable
- nx_udp_free_port_find
- nx_udp_info_get
- nx_udp_packet_info_extract
- nx_udp_socket_bind
- nx_udp_socket_bytes_available
- nx_udp_socket_checksum_disable
- nx_udp_socket_checksum_enable
- nx_udp_socket_create
- nx_udp_socket_delete
- nx_udp_socket_info_get
- nx_udp_socket_port_get
- nx_udp_socket_receive
- nx_udp_socket_receive_notify
- nx_udp_socket_send
- nx_udp_socket_source_send
- nx_udp_socket_unbind
- nx_udp_source_extract
- nxd_udp_packet_info_extract
- nxd_udp_socket_send
- nxd_udp_socket_source_send