---
title: Capitolo 4 - Azure RTOS server NetX Duo DHCPv6
description: Questo capitolo contiene una descrizione di tutti i servizi NetX Duo DHCPv6Server
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cf6b43f70a7159af6c24496ec2ae2276d5e271af2ad3af99687181df3bf6be6c
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792027"
---
# <a name="chapter-4---azure-rtos-netx-duo-dhcpv6-server-services"></a>Capitolo 4 - Azure RTOS server NetX Duo DHCPv6

Questo capitolo contiene una descrizione di tutti i servizi NetX Duo DHCPv6Server (elencati di seguito).

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **GRASSETTO** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- nx_dhcpv6_server_create creare *un'istanza del server DHCPv6*
- nx_dhcpv6_server_delete *un'istanza del server DHCPv6*
- nx_dhcpv6_server_start avviare *l'attività del server DHCPv6*
- nx_dhcpv6_server_suspend *l'attività del server DHCPv6*
- nx_dhcpv6_server_resume'elaborazione *del client DHCPv6*
- nx_dhcpv6_server_suspend *l'elaborazione del client DHCPv6*
- nx_dhcpv6_create_dns_address impostare *il server DNS per le richieste di opzioni*
- nx_dhcpv6_create_ip_address_range creare *l'intervallo di indirizzi IP da lease*
- nx_dhcpv6_reserve_ip_address_range *intervallo di riserva di indirizzi IP nell'elenco dei server*
- nx_dhcpv6_set_server_duid *il DUID del server per i pacchetti DHCPv6*
- nx_dhcpv6_add_ip_address_lease aggiungere *un record di lease alla tabella del server DHCPv6*
- Nx_dhcpv6_retrieve_ip_address_lease recuperare *un record di lease IP dalla tabella Server*
- nx_dhcpv6_add_client_record aggiungere *un record client DHCPv6 alla tabella Server*
- nx_dhcpv6_retrieve_client_record recuperare *un record client dalla tabella Server*
- nx_dhcpv6_server_interface_set *l'indice dell'interfaccia per i servizi DHCPv6 del server*
- nx_dhcpv6_server_option_request_handler_set *impostare il gestore delle richieste di opzioni*

## <a name="nx_dhcpv6_create_dns_address"></a>nx_dhcpv6_create_dns_address

### <a name="set-the-network-dns-server"></a>Impostare il server DNS di rete

**Prototipo**

```
UINT nx_dhcpv6_create_dns_address(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *dns_ipv6_address);
```

**Descrizione**

Questo servizio carica il server DHCPv6 con l'indirizzo del server DNS per l'interfaccia di rete Server DHCPv6.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6
- **dns_ipv6_address** Puntatore al server DNS

**Valori restituiti**

- **NX_SUCCESS** server DNS (0x00) salvato nell'istanza del server DHCPv6
- **NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) Viene fornito un indirizzo non valido
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

codice dell'applicazione

**Esempio**

```
/* Set the network DNS server with the input address for the Server DHCPv6interface. */
status = nx_dhcpv6_create__dns_address(&dhcp_server_0, &dns_ipv6_address);
/* If this service returns NX_SUCCESS the DNS server data was accepted. */
```

## <a name="nx_dhcpv6_create_ip_address_range"></a>nx_dhcpv6_create_ip_address_range

### <a name="create-the-server-ip-address-list"></a>Creare l'elenco di indirizzi IP del server

**Prototipo**

```
UINT _nx_dhcpv6_create_ip_address_range(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *start_ipv6_address, NXD_ADDRESS *end_ipv6_address, 
     UINT *addresses_added)
```

**Descrizione**

Questo servizio crea l'elenco di indirizzi IP specificato dagli indirizzi iniziale e finale dell'intervallo di indirizzi assegnabili del server. Gli indirizzi iniziale e finale devono corrispondere al prefisso dell'indirizzo dell'interfaccia server (deve essere sullo stesso collegamento dell'interfaccia Server DHCPv6). Viene restituito il numero di indirizzi effettivamente aggiunti.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6
- **start_ipv6_address** Inizio degli indirizzi da aggiungere
- **end_ipv6_address** Fine degli indirizzi da aggiungere
- ***addresses_added** Output degli indirizzi aggiunti

**Valori restituiti**

- **NX_SUCCESS** (0x00) l'elenco di indirizzi IP è stato creato correttamente
- **NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) Viene fornito un indirizzo non valido
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

codice dell'applicazione

**Esempio**

```
/* Create the Server IP address list for the server DHCPv6 interface. */
status = nx_dhcpv6_create_ip_address_range(&dhcp_server_0,
         &start_ipv6_address, &end_ipv6_address, &addresses_reserved);
/* If status is NX_SUCCESS one or more addresses were successfully added. */
```

## <a name="nx_dhcpv6_reserve_ip_address_range"></a>nx_dhcpv6_reserve_ip_address_range

### <a name="reserve-specified-range-of-ip-addresses"></a>Riservare l'intervallo specificato di indirizzi IP

**Prototipo**

```
UINT _nx_dhcpv6_reserve_ip_address_range(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *start_ipv6_address, NXD_ADDRESS *end_ipv6_address, 
     UINT *addresses_reserved)
```

**Descrizione**

Questo servizio riserva l'intervallo di indirizzi IP specificato dagli indirizzi iniziale e finale. Questi indirizzi devono essere all'interno dell'intervallo di indirizzi IP del server creato in precedenza. Questi indirizzi non verranno assegnati ai client dal server DHCPv6. Gli indirizzi iniziale e finale devono corrispondere al prefisso dell'indirizzo dell'interfaccia server (deve essere sullo stesso collegamento dell'interfaccia di rete Server DHCPv6). Viene restituito il numero di indirizzi effettivamente riservati.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6
- **start_ipv6_address** Inizio degli indirizzi da riservare
- **end_ipv6_address** Fine degli indirizzi da riservare
- ***addresses_reserved** Numero di indirizzi riservati

**Valori restituiti**

- **NX_SUCCESS** (0x00) IL messaggio RELEASE è stato creato ed elaborato correttamente
- **NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) Viene fornito un indirizzo non valido
- **NX_DHCPV6_INVALID_IP_ADDRESS** (0xED1) Indirizzo iniziale non trovato nell'elenco indirizzi del server.
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

codice dell'applicazione

**Esempio**

```
/* Reserve a range of ip addresses in the Server address table for the server DHCPv6 
network interface. */

status = nx_dhcpv6_reserve_ip_address_range(&dhcp_server_0,
         &start_ipv6_address, &end_ipv6_address, &addresses_reserved);

/* If status is NX_SUCCESS one or more addresses were successfully reserved. */
```

## <a name="nx_dhcpv6_server_create"></a>nx_dhcpv6_server_create

### <a name="create-the-dhcpv6-server-instance"></a>Creare l'istanza del server DHCPv6 

**Prototipo**

```
UINT nx_dhcpv6_server_create(NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
        NX_IP *ip_ptr, CHAR *name_ptr, 
        NX_PACKET_POOL *packet_pool_ptr, 
        VOID *stack_ptr,ULONG stack_size,
    VOID (*dhcpv6_address_declined_handler)(struct 
        NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
        NX_DHCPV6_CLIENT *dhcpv6_client_ptr, 
        UINT message),
    VOID (*dhcpv6_option_request_handler)(
        struct NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
        UINT option_request, UCHAR *buffer_ptr, UINT *index));
```

**Descrizione**

Questo servizio crea l'attività server DHCPv6 con l'input specificato. I gestori di callback sono input facoltativi. Sono necessari il puntatore dello stack, l'istanza IP e l'input del pool di pacchetti. L'istanza IP e il pool di pacchetti devono essere già stati creati.

L'utente è invitato a chiamare nx_dhcpv6_server_option_request_handler_set per impostare il gestore delle richieste di opzioni.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6
- **ip_ptr** Puntatore all'istanza IP
- **name_str** Puntatore al nome del server
- **packet_pool_ptr** Puntatore al pool di pacchetti del server
- **stack_ptr** Puntatore alla memoria dello stack del server
- **stack_size** Dimensioni della memoria dello stack del server
- **dhcpv6_address_declined_handler** Puntatore al gestore di messaggi Client Decline o Release
- **dhcpv6_option_request_handler** Puntatore al gestore delle opzioni di richiesta delle opzioni

**Valori restituiti**

- **NX_SUCCESS** (0x00) Il server è stato ripreso correttamente
- NX_PTR_ERROR (0x16) Input puntatore non valido
- NX_DHCPV6_PARAM_ERROR input non puntatore non valido

**Consentito da**

codice dell'applicazione

**Esempio**

```
/* Create the DHCPv6 Server. */
status = nx_dhcpv6_server_create(&dhcp_server_0, &ip_0, "DHCPv6 Server",
         &pool_0, stack_pointer,2048, dhcpv6_decline_handler,
         dhcpv6_get_time_handler);
/* If status is NX_SUCCESS the Server successfully created. */
```

## <a name="nx_dhcpv6_server_delete"></a>nx_dhcpv6_server_delete

### <a name="delete-the-dhcpv6-server"></a>Eliminare il server DHCPv6

**Prototipo**

```
UINT _nx_dhcpv6_server_delee(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

**Descrizione**

Questo servizio elimina l'attività del server DHCPv6 e qualsiasi richiesta elaborata dal server.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6

**Valori restituiti**

- **NX_SUCCESS** server (0x00) eliminato correttamente
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

Thread

**Esempio**

```
/* Delete the DHCPv6 Serve. */
status = nx_dhcpv6_server_delete(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully deleted. */
```

## <a name="nx_dhcpv6_server_resume"></a>nx_dhcpv6_server_resume

### <a name="resume-dhcpv6-server-task"></a>Riprendere l'attività del server DHCPv6 

**Prototipo**

```
UINT _nx_dhcpv6_server_resume(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

**Descrizione**

Questo servizio riprende l'attività del server DHCPv6 e qualsiasi richiesta elaborata dal server.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6

**Valori restituiti**

- **NX_SUCCESS** (0x00) Il server è stato ripreso correttamente
- **NX_DHCPV6_ALREADY_STARTED** server (0xE91) è già in esecuzione
- **stato** (variabile) Stato degli errori ThreadX e NetX Duo
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

Thread

**Esempio**

```
/* Resume the DHCPv6 Server task. */
status = nx_dhcpv6_server_resume(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully resumed. */
```

## <a name="nx_dhcpv6_server_suspend"></a>nx_dhcpv6_server_suspend

### <a name="suspend-dhcpv6-server-task"></a>Attività Sospendi server DHCPv6 

**Prototipo**

```
UINT _nx_dhcpv6_server_suspend(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

**Descrizione**

Questo servizio sospende l'attività del server DHCPv6 e qualsiasi richiesta elaborata dal server.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6

**Valori restituiti**

- **NX_SUCCESS** (0x00) Il server è stato ripreso correttamente
- **NX_DHCPV6_NOT_STARTED** (0xE92) Il server non è stato avviato 
- **Stato** (variabile) Stato degli errori ThreadX e NetX Duo
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

Thread

**Esempio**

```
/* Suspend the DHCPv6 Server task. */
status = nx_dhcpv6_server_suspend(&dhcp_server_0);

/* If status is NX_SUCCESS the Server successfully suspended. */
```

## <a name="nx_dhcpv6_server_start"></a>nx_dhcpv6_server_start

### <a name="start-the-dhcpv6-server-task"></a>Avviare l'attività Server DHCPv6 

**Prototipo**

```
UINT _nx_dhcpv6_server_start(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

**Descrizione**

Questo servizio avvia l'attività server DHCPv6 e richiede al server di elaborare le richieste dell'applicazione per la ricezione di messaggi client DHCPv6. Verifica che l'istanza del server disponga di informazioni sufficienti (DUID server), crea e associa il socket UDP per l'invio e la ricezione di messaggi DHCPv6 e attiva i timer per tenere traccia dell'ora di sessione e della scadenza del lease IP.

>[!NOTE] 
> Prima di poter eseguire il server DHCPv6, l'applicazione host è responsabile della creazione dell'intervallo di indirizzi IP da cui il server può assegnare indirizzi IP. È anche responsabile dell'impostazione dell'interfaccia SERVER DUID e DHCPv6 (vedere nx_dhcpv6_server_duid_set *e* *nx_dhcpv6_server_interface_set* rispettivamente.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6

**Valori restituiti**

- **NX_SUCCESS** server (0x00) avviato correttamente
- **NX_DHCPV6_ALREADY_STARTED** server (0xE91) è già in esecuzione
- **NX_DHCPV6_NO_ASSIGNABLE_ADDRESSES** server (0xEA7) non ha indirizzi assegnabili per il lease
- **NX_DHCPV6_INVALID_GLOBAL_INDEX** (0xE97) Indice indirizzi globali non impostato
- **NX_DHCPV6_NO_SERVER_DUID** (0xE92) Nessun DUID server creato 
- **stato** (variabile) Stato degli errori ThreadX e NetX Duo
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

Thread

**Esempio**

```
/* Start the DHCPv6 Server task. */
status = nx_dhcpv6_server_start(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully started. */
```

## <a name="nx_dhcpv6_retrieve_ip_address_lease"></a>nx_dhcpv6_retrieve_ip_address_lease

### <a name="get-an-ip-address-lease-from-the-server-table"></a>Ottenere un lease di indirizzo IP dalla tabella Server

**Prototipo**

```
UINT _nx_dhcpv6_retrieve_ip_address_lease(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, UINT table_index, 
     NXD_ADDRESS *lease_IP_address, ULONG *T1, ULONG *T2, 
     ULONG *valid_lifetime, ULONG *preferred_lifetime)
```

**Descrizione**

Questo servizio recupera un record di lease dell'indirizzo IP dalla tabella Server nella posizione di indice della tabella specificata. Questa operazione può essere eseguita prima o dopo il recupero dei dati del record client.

La possibilità di archiviare e recuperare dati tra il server DHCPv6 e la memoria non volatile è un requisito del protocollo DHCPv6. Non fa alcuna differenza nell'ordine in cui i dati di lease IP e i dati del record client vengono salvati in memoria non volatile.

>[!NOTE] 
> Non è consigliabile copiare dati in o da tabelle del server senza arrestare o sospendere prima il server DHCPv6.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6
- **table_index** Indice di tabella in cui archiviare il lease
- **lease_IP_address** Puntatore all'indirizzo IP assegnato in lease al client
- **T1** Tempo di rinnovo richiesto dal client
- **T2** Ora di riassociata richiesta dal client
- **valid_lifetime** Il lease client diventa deprecato
- **preferred_lifetime** Lease client non valido

**Valori restituiti**

- **NX_SUCCESS** server (0x00) avviato correttamente
- **NX_DHCPV6_PARAMETER_ERROR** (0xE93) Input dati lease IP non validi
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

Codice dell'applicazione

**Esempio**

```
/* Retrieve the DHCPv6 Server lease data. */
For (I = 0; I < NX_DHCPV6_MAX_LEASES; i++)
{
    /* Get the next lease record. */
    status = nx_dhcpv6_server_startdhcpv6_server_ptr, i, &next_ipv6_address, &T1,
             &T2, &preferred_lifetime, &valid_lifetime);
    /* The host application then saves this record to memory.
}
/* If status is NX_SUCCESS the Server data is successfully downloaded. */
```

## <a name="nx_dhcpv6_add_ip_address_lease"></a>nx_dhcpv6_add_ip_address_lease

### <a name="add-an-ip-address-lease-to-the-server-table"></a>Aggiungere un lease di indirizzo IP alla tabella Server

**Prototipo**

```
UINT _nx_dhcpv6_add_ip_address_lease(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, UINT table_index, NXD_ADDRESS *lease_IP_address, ULONG T1, ULONG T2, 
     ULONG valid_lifetime, ULONG preferred_lifetime)
```

**Descrizione**

Questo servizio carica i dati di lease IP da una sessione precedente del server DHCPv6 dalla memoria non volatile alla tabella lease del server. Questa operazione non è necessaria se il server è in esecuzione per la prima volta e non dispone di dati di lease precedenti. In questo caso, l'applicazione host deve creare un intervallo di indirizzi IP per l'assegnazione di indirizzi IP usando il *nx_dhcpv6_create_ip_address_range* servizio. I dati sono sufficienti per ricostruire un record di lease DHCPv6. L'indice della tabella non deve essere specificato. Se impostato su 0xFFFFFFFF (infinito) il server DHCPv6 troverà il successivo slot disponibile in cui copiare i dati.

>[!NOTE] 
> Il caricamento dei dati di lease IP deve essere eseguito prima di caricare i record client. è necessario eseguire entrambe le operazioni prima di (ri)avviare il server DHCPv6.

La possibilità di archiviare e recuperare dati tra il server DHCPv6 e la memoria non volatile è un requisito del protocollo DHCPv6.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6
- **table_index** Indice di tabella in cui archiviare il lease
- **lease_IP_address** Puntatore all'indirizzo IP assegnato in lease al client
- **T1** Tempo di rinnovo richiesto dal client
- **T2** Ora di riassociata richiesta dal client
- **valid_lifetime** Il lease client diventa deprecato
- **preferred_lifetime** Lease client non valido

**Valori restituiti**

- **NX_SUCCESS** server (0x00) avviato correttamente
- **NX_DHCPV6_TABLE_FULL** (0xEC4) Nessun spazio per altri dati di lease**
- **NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) I dati di lease non sembrano essere in collegamento con l'interfaccia Server DHCPv6
- **NX_DHCPV6_PARAM_ERROR** (0xE93) Input dati lease IP non validi
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

Codice dell'applicazione

**Esempio**

```
/* Copy the IP lease data to the Server address table. Note that the table index
is defaulted to 0xFFFFFFFF meaning the DHCPv6 Server will find an empty slot 
for each lease. */

    For(I = 0; I < NX_DHCPV6_MAX_LEASES; i++)
    {
        status = nx_dhcpv6_add_ip_address_lease(dhcpv6_server_ptr, 0xFFFFFFFF,
                 &next_ipv6_address, &T1, &T2, &preferred_lifetime, &valid_lifetime);
        /* Get the next lease address from memory… */
    }
    
    /* If status is NX_SUCCESS the lease data was successfully uploaded. It is opk
    to add the Client records to the Server table now. */
```

## <a name="nx_dhcpv6_add_client_record"></a>nx_dhcpv6_add_client_record

### <a name="add-a-client-record-to-the-server-table"></a>Aggiungere un record Client alla tabella Server

**Prototipo**

```
UINT _nx_dhcpv6_add_client_record(NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT table_index, ULONG message_xid, 
     NXD_ADDRESS *client_address, UINT client_state, 
     ULONG IP_lease_time_accrued, ULONG valid_lifetime, UINT duid_type, UINTduid_hardware, 
     ULONG physical_address_msw, ULONG physical_address_lsw, ULONG duid_time, 
     ULONG duid_vendor_number, UCHAR *duid_vendor_private, UINT duid_private_length)
```

**Descrizione**

Questo servizio copia i dati client dalla memoria non volatile alla tabella Server un record alla volta. Questa operazione è necessaria solo se il server viene riavviato e dispone di dati client di una sessione precedente da ripristinare dalla memoria. Se un server non ha dati precedenti, il server DHCPv6 inizializza la tabella Client per poter aggiungere record client.

Non è necessario specificare l'indice della tabella. Se impostato su 0xFFFFFFFF (infinito) il server DHCPv6 individua il successivo slot disponibile. Il server DHCPv6 può ricostruire un record client da questi dati.

>[!NOTE] 
> L'applicazione host DEVE caricare i dati del lease IP PRIMA dei dati del record client. In questo modo, internamente il server DHCPv6 può collegare le tabelle in modo che ogni record Client sia unito con il record di lease IP corrispondente nelle rispettive tabelle. Vedere *nx_dhcpv6_add_ip_address_lease* per informazioni dettagliate sul caricamento dei dati di lease IP dalla memoria.

>[!NOTE] 
> A seconda del tipo DUID, non è necessario specificare tutti i dati. Ad esempio, se un client ha un tipo DUID assegnato dal fornitore, può inviare zero per i parametri DUID Link Layer (indirizzo MAC, tipo di hardware, ora DUID).

La possibilità di archiviare e recuperare dati tra il server DHCPv6 e la memoria non volatile è un requisito del protocollo DHCPv6.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6

**Valori restituiti**

- **NX_SUCCESS** server (0x00) avviato correttamente
- **NX_ INVALID_PARAMETERS** (0x4D) Input non puntatore non valido**
- **NX_DHCPV6_TABLE_FULL** (0xEC4) Non sono rimasti slot vuoti per l'aggiunta di un altro record client
- **NX_DHCPV6_ADDRESS_NOT_FOUND** (0xEA8) Indirizzo assegnato dal client non trovato nella tabella lease del server.
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

Codice dell'applicazione

**Esempio**

```
/*Add the IP lease data and Client records back to the server before starting
theServer. */
    /* Copy the 'lease data' to the server table FIRST. */
for (i = 0; i< NX_DHCPV6_MAX_LEASES; i++)
    {

        /* Add the next lease record. Let the server find the next
        available slot. */
        status = nx_dhcpv6_add_ip_address_lease(dhcpv6_server_ptr,
                 0xFFFFFFFF,,&next_ipv6_address, NX_DHCPV6_DEFAULT_T1_TIME, 
                 NX_DHCPV6_DEFAULT_T2_TIME, NX_DHCPV6_DEFAULT_PREFERRED_TIME, 
                 NX_DHCPV6_DEFAULT_VALID_TIME);
if (status != NX_SUCCESS)
return status;
        /* Get the next IP lease record from memory. */
        …
    }
    /* Copy the client records to the Server table NEXT.
    for (i = 0; i< NX_DHCPV6_MAX_LEASES; i++)
    {
        /* Add the next client record. Let the server find the next
        available slot. */
        status = nx_dhcpv6_add_client_record(dhcpv6_server_ptr, 0xFFFFFFFF,
                 message_xid, &client_ipv6_address, NX_DHCPV6_STATE_BOUND,
                 IP_lifetime_time_accrued, valid_lifetime, duid_type, 
                 duid_hardware, physical_address_msw, physical_address_lsw, 
                 duid_time, 0, NX_NULL, 0);
if (status != NX_SUCCESS)
return status;
        /* Get the next Client record from memory. */
        …
    }

/* If status is NX_SUCCESS the Server data was successfully restored and 
it is ok to start the DHCPv6 server now. */
```

## <a name="nx_dhcpv6_retrieve_client_record"></a>nx_dhcpv6_retrieve_client_record

### <a name="retrieve-a-client-record-from-the-server-table"></a>Recuperare un record client dalla tabella Server

**Prototipo**

```
UINT _nx_dhcpv6_retrieve_client_record(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT table_index, ULONG *message_xid, 
     NXD_ADDRESS *client_address, UINT *client_state, 
     ULONG IP_lease_time_accrued, 
     ULONG *valid_lifetime, UINT *duid_type, 
     UINT *duid_hardware, ULONG *physical_address_msw, 
     ULONG *physical_address_lsw, ULONG *duid_time, 
     ULONG *duid_vendor_number, 
     UCHAR *duid_vendor_private, 
     UINT *duid_private_length)
```

**Descrizione**

Questo servizio copia i dati essenziali dalla tabella dei record client del server per l'archiviazione alla memoria non volatile. Il server può ricostruire un record client adeguato da tali dati nel processo inverso (caricamento dei dati nella tabella Server). Indipendentemente dal tipo DUID, nessuno dei puntatori può essere puntatore NULL. i dati vengono inizializzati su zero per tutti i parametri. Ad esempio, se il tipo DUID client è Link Layer Plus Time, il numero del fornitore viene restituito come zero e l'ID privato è una stringa vuota.

La possibilità di archiviare e recuperare dati tra il server DHCPv6 e la memoria non volatile è un requisito del protocollo DHCPv6. Non fa alcuna differenza nell'ordine in cui i dati di lease IP e i dati del record client vengono salvati in memoria non volatile.

>[!NOTE] 
> Non è consigliabile copiare dati in o da tabelle del server senza arrestare o sospendere prima il server DHCPv6.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6
- **table_index** Indice nella tabella client del server
- **message_xid** ID transazione server client
- **client_address** Indirizzo IPv6 assegnato in lease al client
- **client_state** Stato DHCPv6 del client (ad esempio associato)
- **IP_lease_time_accrued** Tempo scaduto nel lease già **dhcpv6_server_ptr** puntatore al server DHCPv6
- **dhcpv6_server_ptr** Puntatore al server DHCPv6

**Valori restituiti**

- **NX_SUCCESS** server (0x00) avviato correttamente
- **NX_DHCPV6_INVALID_DUID** (0xECC) Dati DUID non validi o incoerenti
- **NX_PTR_ERROR** (0x16) Input puntatore non valido
- NX_INVALID_PARAMETERS (0x4D) Input non puntatore non valido

**Consentito da**

Codice dell'applicazione

**Esempio**

```
/* Retrieve the Client records from the DHCPv6 Server table. */
For (i = 0; i< NX_MAX_DHCPV6_CLIENTS; i++)
{
    status = nx_dhcpv6_retrieve_client_recorddhcpv6_server_ptr, i, &message_xid,
             &client_ipv6_address, &client_state, &IP_lifetime_time_accrued, 
             valid_lifetime, &duid_type, &duid_hardware, &physical_address_msw,
             &physical_address_lsw, &duid_time, &duid_vendor_number, &private_id[0], 
             &length);
    /* The host application can save this data to memory now.
}
/* If status is NX_SUCCESS the Server successfully started. */
```

## <a name="nx_dhcpv6_server_interface_set"></a>nx_dhcpv6_server_interface_set

### <a name="setthe-interface-index-for-server-dhcpv6-interface"></a>Impostare l'indice dell'interfaccia per l'interfaccia DHCPv6 del server

**Prototipo**

```
UINT _nx_dhcpv6_server_interface_set(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT iface_index, UINT ga_address_index)
```

**Descrizione**

Questo servizio imposta l'interfaccia di rete in cui il server DHCPv6 gestisce le richieste client DHCPv6. Non che per le versioni di NetX Duo che non supportano multihome, il valore predefinito dell'interfaccia è zero. L'indice degli indirizzi globali è necessario per ottenere l'indirizzo globale del server nella relativa interfaccia DHCPv6. Viene usato dalla logica DHCPv6 per garantire che gli indirizzi di lease e altri dati DHCPv6 siano in collegamento con il server DHCPv6.

Questa operazione deve essere chiamata prima dell'avvio del server DHCPv6, anche per le applicazioni in singoli dispositivi ospitati o senza supporto multihome.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6
- **iface_index** Interfaccia server DHCPv6 del server
- **ga_address_index** Indice dell'indirizzo globale del server nella tabella degli indirizzi dell'istanza IP del server

**Valori restituiti**

- **NX_SUCCESS** server (0x00) avviato correttamente
- **NX_INVALID_INTERFACE(0x4C)** l'interfaccia non esiste
- NX_NO_INTERFACE_ADDRESS (0x50) L'indice globale supera il numero massimo di indirizzi IPv6 dell'istanza IP (NX_MAX_IPV6_ADDRESSES)
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

Codice dell'applicazione

**Esempio**

```
/* Set the Server DHCPv6 interface to the primary interface. The global IP 
address is at the index 1 in the IP address table. */
status = nx_dhcpv6_server_interface_set(&dhcp_server_0, 0, 1);

/* If status is NX_SUCCESS the Server interface is successfully set. */
```
## <a name="nx_dhcpv6_set_server_duid"></a>nx_dhcpv6_set_server_duid

### <a name="set-the-server-duid-for-dhcpv6-packets"></a>Impostare il DUID del server per i pacchetti DHCPv6

**Prototipo**

```
UINT _nx_dhcpv6_set_server_duid(NX_DHCPV6_SERVER *dhcpv6_server_ptr,
     UINT duid_type, UINT hardware_type, 
     ULONG mac_address_msw, ULONG mac_address_lsw, 
     ULONG time)
```

**Descrizione**

Questo servizio imposta il DUID del server e deve essere chiamato prima che l'applicazione host avvia il server. Per i tipi DUID del livello di collegamento e del livello di collegamento, l'applicazione host deve fornire i dati relativi al tipo di hardware e all'indirizzo MAC. Per i DUID di tempo del livello di collegamento, l'indicatore di tempo deve puntare a un'ora valida. Il numero di secondi trascorsi dal 1° gennaio 2000 è un valore di seed tipico. Se il tipo DUID del server è il tipo aziendale assegnato dal fornitore, il DUID verrà creato dalle opzioni configurabili dall'utente NX_DHCPV6_SERVER_DUID_VENDOR_PRIVATE_ID e NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_ID e i valori di ora e indirizzo MAC possono essere impostati su NULL.

>[!NOTE] 
> È responsabilità dell'applicazione host salvare i parametri DUID del server in memoria non volatile in modo che usi lo stesso DUID nei messaggi ai client tra un riavvio e l'altro. Si tratta di un requisito del protocollo DHCPv6 (RFC 3315).

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6
- **duid_type** Tipo DUID del server DHCPv6
- **hardware_type** Tipo di hardware (ad esempio Ethernet)
- **mac_address_msw** Puntatore al server DHCPv6
- **mac_address_lsw** Puntatore al server DHCPv6
- **time** Valore di ora per DUID

**Valori restituiti**

- **NX_SUCCESS** server (0x00) sospeso
- **NX_DHCPV6_INVALID_SERVER_DUID** (0XE98) Tipo DUID sconosciuto o non supportato
- **NX_INVALID_PARAMETERS** (0x4D) Input non puntatore non valido
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

Codice dell'applicazione

**Esempio**

```
/* Set the DHCPv6 ServerDUID as Link layer plus time, over Ethernet hardware. */
duid_time = SECONDS_SINCE_JAN_1_2000_MOD_32 + rand();

status = nx_dhcpv6_set_server_duid(&dhcp_server_0,1, 0x6,
         physical_address_msw,physical_address_lsw,duid_time);

/* If status is NX_SUCCESS the ServerDUID is successfully set. */
```

## <a name="nx_dhcpv6_server_option_request_handler_set"></a>nx_dhcpv6_server_option_request_handler_set

### <a name="set-the-option-request-handler-for-dhcpv6-server-instance"></a>Impostare il gestore delle richieste di opzioni per l'istanza del server DHCPv6 

**Prototipo**

```
UINT nx_dhcpv6_server_option_request_handler_set(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     VOID (*dhcpv6_option_request_handler_extended)(
          struct NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
          UINT option_request, UCHAR *buffer_ptr, 
          UINT *index, UINT available_payload));
```

**Descrizione**

Questo servizio imposta il gestore richieste dell'opzione estesa del server DHCPv6.

**Parametri di input**

- **dhcpv6_server_ptr** Puntatore al server DHCPv6
- **dhcpv6_option_request_handler_extended** Puntatore al gestore di richieste di opzioni estese

**Valori restituiti**

- **NX_SUCCESS** server (0x00) ripreso correttamente
- NX_PTR_ERROR (0x16) Input puntatore non valido

**Consentito da**

codice dell'applicazione

**Esempio**

```
/* Set the option request handler for DHCPv6 Server. */
status = nx_dhcpv6_server_option_request_handler_set(&dhcp_server_0,
         dhcpv6_option_request_handler_extended);

/* If status is NX_SUCCESS the extended handler successfully set. */
```