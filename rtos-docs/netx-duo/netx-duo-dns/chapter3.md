---
title: Capitolo 3-Descrizione dei servizi client DNS di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi DNS di Azure RTO NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9634adab3944c29f64d26dd688b5053dc1bd9bcb
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821920"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-dns-client-services"></a>Capitolo 3-Descrizione dei servizi client DNS di Azure RTO NetX Duo

Questo capitolo contiene una descrizione di tutti i servizi DNS di Azure RTO NetX (elencati di seguito) in ordine alfabetico.

Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_dns_authority_zone_start_get** *ricercare l'inizio di una zona di autorità associata al nome host specificato*

- **nx_dns_cache_initialize** *inizializzare una cache DNS.*

- **nx_dns_cache_notify_clear** *cancellare la funzione di notifica completa della cache.*

- **nx_dns_cache_notify_set** *impostare la funzione di notifica completa della cache.*

- **nx_dns_cname_get** *cercare il nome di dominio canonico per l'alias del nome di dominio di input*

- **nx_dns_create** *creare un'istanza del client DNS*

- **nx_dns_delete** *eliminare un'istanza del client DNS*

- **nx_dns_domain_name_server_get** *cercare i server dei nomi autorevoli per la zona del dominio di input*

- **nx_dns_domain_mail_exchange_get** *cercare lo scambio di posta associato al nome host specificato.*

- **nx_dns_domain_service_get** *cercare i servizi associati al nome host specificato*

- **nx_dns_get_serverlist_size** *restituiscono le dimensioni dell'elenco di server client DNS*

- **nx_dns_info_by_name_get** l' *indirizzo IP restituito, le query sulle porte sul nome host di input*

- **nx_dns_ipv4_address_by_name_get** *cercare l'indirizzo IPv4 dal nome host specificato*

- **nxd_dns_ipv6_address_by_name_get** *cercare l'indirizzo IPv6 dal nome host specificato*

- **nx_dns_host_by_address_get** *funzione wrapper per nxd_dns_host_by_address_get per cercare un nome host da un indirizzo IP specificato (supporta solo indirizzi IPv4)*

- **nxd_dns_host_by_address_get** *cercare un indirizzo IP dal nome host di input (supporta indirizzi IPv4 e IPv6)*

- **nx_dns_host_by_name_get** *funzione wrapper per nxd_dns_host_by_address_get per cercare un nome host dall'indirizzo specificato (supporta solo indirizzi IPv4)*

- **nxd_dns_host_by_name_get** *cercare un indirizzo IP dal nome host di input (supporta indirizzi IPv4 e IPv6)*

- **nx_dns_host_text_get** *cercare i dati di testo per il nome di dominio di input*

- **nx_dns_packet_pool_set** *impostare il pool di pacchetti client DNS*

- **nx_dns_server_add** *funzione wrapper per* NXD_DNS_SERVER_ADD *aggiungere un server DNS all'indirizzo specificato all'elenco client (supporta solo IPv4)*

- **nxd_dns_server_add** *aggiungere un server DNS dell'indirizzo IP specificato all'elenco dei server client (supporta indirizzi sia IPv4 che IPv6)*

- **nx_dns_server_get** *restituire il server DNS nell'elenco client (supporta solo indirizzi IPv4)*

- **nxd_dns_server_get** *restituire il server DNS nell'elenco client (supporta gli indirizzi IPv4 e IPv6)*

- **nx_dns_server_remove** *funzione wrapper per nxd_dns_server_remove per rimuovere un server DNS dall'elenco client*

- **nxd_dns_server_remove** *rimuovere un server DNS dell'indirizzo IP specificato dall'elenco client (supporta gli indirizzi IPv4 e IPv6)*

- **nx_dns_server_remove_all** *rimuovere tutti i server DNS dall'elenco client*

## <a name="nx_dns_authority_zone_start_get"></a>nx_dns_authority_zone_start_get

Cercare l'inizio della zona di autorità per l'host di input

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_authority_zone_start_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                      VOID *record_buffer,                                        
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);
```
### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo SOA con il nome di dominio specificato per ottenere l'inizio della zona di autorità per il nome di dominio di input. Il client DNS copia i record SOA restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

Nel client DNS di NetX Duo, il tipo di record SOA, NX_DNS_SOA_ENTRY, viene salvato come parametri di 7 4 byte, totale di 28 byte:

- **nx_dns_soa_host_mname_ptr** Puntatore all'origine dati primaria per questa zona.
- **nx_dns_soa_host_rname_ptr** Puntatore alla cassetta postale responsabile di questa zona
- **nx_dns_soa_serial** Numero di versione zona
- **nx_dns_soa_refresh** Intervallo di aggiornamento
- **nx_dns_soa_retry** Intervallo tra i tentativi di query SOA
- **nx_dns_soa_expire** Durata dell'ora di scadenza di SOA
- **nx_dns_soa_minmum** Campo TTL minimo nei messaggi di risposta DNS del nome host SOA

L'archiviazione di due record SOA è illustrata di seguito. I record SOA contenenti dati a lunghezza fissa vengono immessi a partire dall'inizio del buffer. I puntatori MNAME e RNAME puntano ai dati a lunghezza variabile (nomi host) archiviati nella parte inferiore del buffer. Vengono immessi record SOA aggiuntivi dopo il primo record ("record SOA aggiuntivi...") e i dati a lunghezza variabile vengono archiviati sopra i dati a lunghezza variabile dell'ultima voce ("dati di lunghezza variabile SOA aggiuntivi"):

![Archiviazione di due record SOA](media/image4.png)

Se l'input *record_buffer* non può contenere tutti i dati SOA nella risposta del server, il *record_buffer* include il numero di record che si adattano e restituisce il numero di record nel buffer.

Con il numero di record SOA restituiti in **record_count,* l'applicazione può analizzare i dati da *record_buffer* ed estrarre l'inizio delle stringhe del nome host dell'autorità di zona.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **HOST_NAME** Puntatore al nome host per cui ottenere i dati SOA
- **record_buffer** Puntatore alla posizione in cui estrarre i dati SOA
- **BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati SOA
- **record_count** Puntatore al numero di record SOA recuperati
- **WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha ottenuto i dati SOA
- L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto
- **NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
UCHAR  record_buffer[50];
UINT   record_count;   
NX_DNS_SOA_ENTRY *nx_dns_soa_entry_ptr;

/* Request the start of authority zone(s) for the specified host. */
status =  nx_dns_authority_zone_start_get(&client_dns, (UCHAR *)"www.my_example.com",  
                                          record _buffer, sizeof(record_buffer), 
                                          &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
         error_counter++;
}
else 
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and SOA data 
       is returned in soa_buffer. */

    /* Set a local pointer to the SOA buffer. */
    nx_dns_soa_entry_ptr = (NX_DNS_SOA_ENTRY *) record_buffer;

    printf("------------------------------------------------------\n");
    printf("Test SOA: \n");
    printf("serial = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_serial );
    printf("refresh = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_refresh );
    printf("retry = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_retry );
    printf("expire = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_expire );
    printf("minmum = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_minmum );

    if(nx_dns_soa_entry_ptr -> nx_dns_soa_host_mname_ptr)
    {
        printf("host mname = %s\n", 
               nx_dns_soa_entry_ptr -> nx_dns_soa_host_mname_ptr);
    }
    else
    {
        printf("host mame is not set\n");
    }

    if(nx_dns_soa_entry_ptr -> nx_dns_soa_host_rname_ptr)
    {
        printf("host rname = %s\n", 
               nx_dns_soa_entry_ptr -> nx_dns_soa_host_rname_ptr);
    }
    else
    {
     
        printf("host rname is not set\n");
    }
}

[Output]
----------------------------------------------------
Test SOA: 
serial = 2012111212
refresh = 7200
retry = 1800
expire = 1209600
minmum = 300
host mname = ns1.www.my_example.com
host rname = dns-admin.www.my_example.com
```

## <a name="nx_dns_cache_initialize"></a>nx_dns_cache_initialize

Inizializzare la cache DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_cache_initialize(NX_DNS *dns_ptr,
                            VOID *cache_ptr, UINT cache_size);
```

### <a name="description"></a>Descrizione

Questo servizio crea e Inizializza una cache DNS.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.
- **cache_ptr** Puntatore alla cache DNS.
- **cache_size** Dimensioni della cache DNS, in byte.

### <a name="return-values"></a>Valori restituiti

- Cache DNS **NX_SUCCESS** (0x00) inizializzata correttamente
- NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido
- Il puntatore della cache NX_DNS_CACHE_ERROR (0xB7) non è valido.
- NX_PTR_ERROR (0x07) puntatore DNS non valido. 
- La cache NX_DNS_ERROR (messaggi 0XA0) non è allineata a 4 byte.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
/* Initialize the DNS Cache.  */
status =  nx_dns_cache_initialize(&my_dns, &dns_cache, 2048);

/* If status is NX_SUCCESS DNS Cache was successfully initialized.  */
```

## <a name="nx_dns_cache_notify_clear"></a>nx_dns_cache_notify_clear

Cancella la funzione di notifica completa della cache DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_cache_notify_clear(NX_DNS *dns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio Cancella la funzione di notifica completa della cache.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.

### <a name="return-values"></a>Valori restituiti

- Notifica della cache DNS **NX_SUCCESS** (0x00) impostata correttamente
- NX_DNS_PARAM_ERROR (0xA8) non è un input non puntatore valido
- NX_PTR_ERROR (0x07) puntatore DNS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
/* Clear the DNS Cache full notify function. */
status =  nx_dns_cache_notify_clear(&my_dns);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully cleared. */
```

## <a name="nx_dns_cache_notify_set"></a>nx_dns_cache_notify_set

Impostare la funzione di notifica completa della cache DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_cache_notify_set(NX_DNS *dns_ptr,
                            VOID (*cache_full_notify_cb)(NX_DNS *dns_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio imposta la funzione di notifica completa della cache.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.
- **cache_full_notify_cb** Funzione di callback da richiamare quando la cache diventa piena.

### <a name="return-values"></a>Valori restituiti

- Notifica della cache DNS **NX_SUCCESS** (0x00) impostata correttamente
- NX_DNS_PARAM_ERROR (0xA8) non è un input non puntatore valido
- NX_PTR_ERROR (0x07) puntatore DNS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
/* Set the DNS Cache full notify function. */
status =  nx_dns_cache_notify_set(&my_dns, cache_full_notify_cb);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully set. */
```

## <a name="nx_dns_cname_get"></a>nx_dns_cname_get

Cercare il nome canonico per il nome host di input

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_cname_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                     UCHAR *record_buffer, UINT buffer_size, 
                     ULONG wait_option);
```

### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES viene definito in *nxd_dns. h*, questo servizio invia una query di tipo CNAME con il nome di dominio specificato per ottenere il nome di dominio canonico. Il client DNS copia la stringa CNAME restituita nella risposta del server DNS nel percorso di memoria *record_buffer* .

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **HOST_NAME** Puntatore al nome host per cui ottenere i dati CNAME
- **record_buffer** Puntatore alla posizione in cui estrarre i dati CNAME
- **BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati CNAME
- **WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha ottenuto i dati CNAME
- L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto
- **NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) non è un input non puntatore valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
CHAR            record _buffer[50];

/* Request the canonical name for the specified host. */
status =  nx_dns_cname_get(&client_dns, (UCHAR *)"www.my_example.com ", 
                                   record_buffer, sizeof(record_buffer), 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and 
   the canonical host name is returned in record_buffer. */

    printf("------------------------------------------------------\n");
    printf("Test CNAME: %s\n", record_buffer);
} 

[Output]
----------------------------------------------------
Test CNAME: my_example.com
```

##  <a name="nx_dns_create"></a>nx_dns_create

Creare un'istanza del client DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_create(NX_DNS *dns_ptr, NX_IP *ip_ptr, CHAR *domain_name);
```
### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client DNS per l'istanza IP creata in precedenza.

> [!IMPORTANT]
> L'applicazione deve garantire che il payload dei pacchetti del pool di pacchetti utilizzato dal client DNS sia sufficientemente grande per il numero massimo di messaggi DNS a 512 byte, più le intestazioni UDP, IP e Ethernet. Se il client DNS crea il proprio pool di pacchetti, viene definito da NX_DNS_PACKET_PAYLOAD e NX_DNS_PACKET_POOL_SIZE.

Se l'applicazione client DNS preferisce fornire un pool di pacchetti creato in precedenza, il payload per il client DNS IPv4 deve essere di 512 byte per il DNS massimo più 20 byte per l'intestazione IP, 8 byte per l'intestazione UDP e 14 byte per l'intestazione Ethernet. Per IPv6, l'unica differenza è che l'intestazione IP è 40 byte, pertanto il pacchetto deve contenere l'intestazione IPv6 di 40 byte.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **ip_ptr** Puntatore a un'istanza IP creata in precedenza.  
- **Domain_name** Puntatore al nome di dominio per l'istanza DNS.

### <a name="return-values"></a>Valori restituiti

- Creazione DNS riuscita **NX_SUCCESS** (0x00)
- Errore di creazione DNS **NX_DNS_ERROR** (messaggi 0XA0)
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
/* Create a DNS Client instance. */
status =  nx_dns_create(&my_dns, &my_ip, "My DNS");

/* If status is NX_SUCCESS a DNS Client instance was successfully
   created. */
```

## <a name="nx_dns_delete"></a>nx_dns_delete

Eliminare un'istanza del client DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_delete(NX_DNS *dns_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio Elimina un'istanza del client DNS creata in precedenza e libera le risorse. 

> [!NOTE]
> Se NX_DNS_CLIENT_USER_CREATE_PACKET_POOL è definito e al client DNS è stato assegnato un pool di pacchetti definito dall'utente, spetta all'applicazione eliminare il pool di pacchetti client DNS se non è più necessario.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore a un'istanza del client DNS creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- Eliminazione del client DNS riuscita **NX_SUCCESS** (0x00).
- NX_PTR_ERROR (0x07) un puntatore client IP o DNS non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
/* Delete a DNS Client instance. */
status =  nx_dns_delete(&my_dns);

/* If status is NX_SUCCESS the DNS Client instance was successfully
   deleted. */
```

## <a name="nx_dns_domain_name_server_get"></a>nx_dns_domain_name_server_get

Cercare i server dei nomi autorevoli per la zona del dominio di input

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_domain_name_server_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                   VOID *record_buffer, UINT buffer_size, 
                                   UINT *record_count, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo NS con il nome di dominio specificato per ottenere i server dei nomi per il nome di dominio di input. Il client DNS copia i record NS restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

Nel client DNS di NetX Duo il tipo di dati NS, NX_DNS_NS_ENTRY, viene salvato come parametri a 2 4 byte:

- **nx_dns_ns_ipv4_address** Indirizzo IPv4 del server dei nomi
- **nx_dns_ns_hostname_ptr** Puntatore al nome host del server dei nomi

Il buffer riportato di seguito contiene quattro record NX_DNS_NS_ENTRY. Il puntatore alla stringa del nome host in ogni voce punta alla stringa del nome host corrispondente nella metà inferiore del buffer:

![Contiene quattro record NX_DNS_NS_ENTRY](media/image5.png)

Se il *record_buffer* di input non può contenere tutti i dati NS nella risposta del server, il *record_buffer* include il numero di record che si adattano e restituisce il numero di record nel buffer.

Con il numero di record NS restituiti in **record_count,* l'applicazione può analizzare l'indirizzo IP e il nome host di ogni record nel *record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **HOST_NAME** Puntatore al nome host per cui ottenere i dati NS
- **record_buffer** Puntatore alla posizione in cui estrarre i dati NS
- **BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati NS
- **record_count** Puntatore al numero di record NS recuperati
- **WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha ottenuto i dati NS
- L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto
- **NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida
- NX_DNS_PARAM_ERROR (0xA8) non è un input non puntatore valido
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
#define RECORD_COUNT    10

ULONG  record_buffer[50];
UINT   record_count;          
NX_DNS_NS_ENTRY  *nx_dns_ns_entry_ptr[RECORD_COUNT];

/* Request the name server(s) for the specified host. */
status =  nx_dns_domain_name_server_get(&client_dns, (UCHAR *)" www.my_example.com ",  
                                        record_buffer, sizeof(record_buffer),  
                                        &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and NS data
   is returned in record_buffer. */

    printf("------------------------------------------------------\n");
    printf("Test NS: ");
    printf("record_count = %d \n", record_count);      

    /* Get the name server. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_ns_entry_ptr[i] = (NX_DNS_NS_ENTRY *)
                               (record_buffer + i * sizeof(NX_DNS_NS_ENTRY)); 

        printf("record %d: IP address: %d.%d.%d.%d\n", i, 
                      nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address  >> 24,
                      nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 16 & 0xFF,                   
                      nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 8 & 0xFF,
                     nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address & 0xFF);
        if(nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr)
        {
            printf("hostname = %s\n", 
                    nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr);
                }
        else
            printf("hostname is not set\n");
    }
}

[Output]
------------------------------------------------------
Test NS: record_count = 4 
record 0: IP address: 192.2.2.10
hostname = ns2.www.my_example.com
record 1: IP address: 192.2.2.11
hostname = ns1.www.my_example.com
record 2: IP address: 192.2.2.12
hostname = ns3.www.my_example.com
record 3: IP address: 192.2.2.13
hostname = ns4.www.my_example.com
```

## <a name="nx_dns_domain_mail_exchange_get"></a>nx_dns_domain_mail_exchange_get

Cerca lo scambio di posta/i per il nome host di input

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_domain_mail_exchange_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                     VOID *record_buffer,                                        
                                     UINT buffer_size, 
                                     UINT *record_count, 
                                     ULONG wait_option);
```

### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo MX con il nome di dominio specificato per ottenere lo scambio di posta elettronica per il nome di dominio di input. Il client DNS copia i record MX restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* . 

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

Nel client DNS di NetX Duo, il tipo di record di scambio di posta, NX_DNS_MAIL_EXCHANGE_ENTRY, viene salvato come quattro parametri, per un totale di 12 byte:

- **nx_dns_mx_ipv4_address** Indirizzo IPv4 di Exchange per posta elettronica 4 byte
- **nx_dns_mx_preference** Preferenza 2 byte
- **nx_dns_mx_reserved0** 2 byte riservati
- **nx_dns_mx_hostname_ptr** Puntatore al nome host del server di posta elettronica di Exchange Server 4 byte

Di seguito è riportato un buffer contenente quattro record MX. Ogni record contiene i dati a lunghezza fissa dall'elenco precedente. Il puntatore al nome host di Exchange Server di posta elettronica punta al nome host corrispondente nella parte inferiore del buffer.

![Buffer contenente quattro record MX](media/image6.png)

Se l'input *record_buffer* non può contenere tutti i dati MX nella risposta del server, il *record_buffer* include il numero di record che si adattano e restituisce il numero di record nel buffer.

Con il numero di record MX restituiti in **record_count,* l'applicazione può analizzare i parametri MX, incluso il nome host della posta elettronica di ogni record nel *record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **HOST_NAME** Puntatore al nome host per cui ottenere i dati MX
- **record_buffer** Puntatore alla posizione in cui estrarre i dati MX
- **BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati MX
- **record_count** Puntatore al numero di record MX recuperati
- **WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha ottenuto i dati MX
- L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto
- **NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida
- NX_DNS_PARAM_ERROR (0xA8) non è un input non puntatore valido
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
#define MAX_RECORD_COUNT 10

ULONG  record_buffer[50];
UINT   record_count;  
NX_DNS_MX_ENTRY  *nx_dns_mx_entry_ptr[MAX_RECORD_COUNT];        

/* Request the mail exchange data for the specified host. */
status =  nx_dns_domain_mail_exchange_get(&client_dns, (UCHAR *)" www.my_example.com ", 
                                          record_buffer, sizeof(record_buffer),   
                                          &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}
       
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and MX
   data is returned in record_buffer. */

    printf("------------------------------------------------------\n");
    printf("Test MX: ");
    printf("record_count = %d \n", record_count);      


    /* Get the mail exchange. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_mx_entry_ptr[i] = (NX_DNS_MX_ENTRY *)
               (record_buffer + i * sizeof(NX_DNS_MX_ENTRY));   

        printf("record %d: IP address: %d.%d.%d.%d\n", i, 
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 24,
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 16 & 0xFF,                   
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 8 & 0xFF,
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address & 0xFF);

        printf("preference = %d \n ", 
            nx_dns_mx_entry_ptr[i] -> nx_dns_mx_preference);

        if(nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr)
            printf("hostname = %s\n", 
                    nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr);
        else
            printf("hostname is not set\n");
}


[Output]

-----------------------------------------------------
Test MX: record_count = 5 
record 0: IP address: 192.2.2.10
preference = 40 
hostname = alt3.aspmx.l.www.my_example.com
record 1: IP address: 192.2.2.11
preference = 50 
hostname = alt4.aspmx.l.www.my_example.com
record 2: IP address: 192.2.2.12
preference = 10 
hostname = aspmx.l.www.my_example.com
record 3: IP address: 192.2.2.13
preference = 20 
hostname = alt1.aspmx.l.www.my_example.com
record 4: IP address: 192.2.2.14
preference = 30 
hostname = alt2.aspmx.l.www.my_example.com
```

## <a name="nx_dns_domain_service_get"></a>nx_dns_domain_service_get

Cerca i servizi forniti dal nome host di input

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_domain_service_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                VOID *record_buffer, UINT buffer_size, 
                                UINT *record_count, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, il servizio invia una query di tipo SRV con il nome di dominio specificato per cercare i servizi e il relativo numero di porta associato al dominio specificato. Il client DNS copia i record SRV restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* . 

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

Nel client DNS di NetX Duo, il tipo di record del servizio, NX_DNS_SRV_ voce, viene salvato come sei parametri, per un totale di 16 byte. Ciò consente di archiviare i dati SRV a lunghezza variabile in modo efficiente in termini di memoria:

- **Indirizzo IPv4 del Server** nx_dns_srv_ipv4_address 4 byte
- **Priorità Server** nx_dns_srv_priority 2 byte
- **Peso Server** nx_dns_srv_weight 2 byte
- **Numero di porta del servizio** nx_dns_srv_port_number 2 byte
- **Riservato per l'allineamento a 4 byte** nx_dns_srv_reserved0 2 byte
- **Puntatore al nome host del server** * nx_dns_srv_hostname_ptr 4 byte

Nel buffer fornito sono archiviati quattro record SRV. Ogni record di NX_DNS_SRV_ENTRY contiene un puntatore, *nx_dns_srv_hostname_ptr*, che punta alla stringa del nome host corrispondente nella parte inferiore del buffer di record:

![Quattro record SRV](media/image7.png)

Se l'input *record_buffer* non è in grado di contenere tutti i dati SRV nella risposta del server, il *record_buffer* include tutti i record che si adattano e restituisce il numero di record nel buffer.

Con il numero di record SRV restituiti in **record_count,* l'applicazione può analizzare i parametri SRV, incluso il nome host del server di ogni record nel *record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **HOST_NAME** Puntatore al nome host per il quale ottenere i dati SRV
- **record_buffer** Puntatore alla posizione in cui estrarre i dati SRV
- **BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati SRV
- **record_count** Puntatore al numero di record SRV recuperati
- **WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha ottenuto i dati SRV
- L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto
- **NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida
- Il parametro NX_DNS_PARAM_ERROR (0xA8) non è valido per il puntatore.
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
#define MAX_RECORD_COUNT  10

UCHAR  record_buffer[50];
UINT   record_count;          
NX_DNS_SRV_ENTRY *nx_dns_srv_entry_ptr[MAX_RECORD_COUNT];

/* Request the service(s) provided by the specified host. */
status =  nx_dns_domain_service_get(&client_dns, (UCHAR *)"www.my_example.com ", 
                                    record_buffer, sizeof(record_buffer), 
                                    &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and SRV data
       is returned in record_buffer. */

        printf("------------------------------------------------------\n");
        printf("Test SRV: ");
        printf("record_count = %d \n", record_count);      

           
        /* Get the location of services. */
        for(i =0; i< record_count; i++)
        {
            nx_dns_srv_entry_ptr[i] = (NX_DNS_SRV_ENTRY *)
                                    (record_buffer + i * sizeof(NX_DNS_SRV_ENTRY)); 

            printf("record %d: IP address: %d.%d.%d.%d\n", i, 
                    nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 24,
                    nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 16 & 0xFF,                   
                    nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 8 & 0xFF,
                    nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address & 0xFF);

           printf("port number = %d\n", 
                   nx_dns_srv_entry_ptr[i] -> nx_dns_srv_port_number );
           printf("priority = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_priority );
           printf("weight = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_weight );

           if(nx_dns_srv_entry_ptr[i] -> nx_dns_srv_hostname_ptr)
           {
                printf("hostname = %s\n", 
                        nx_dns_srv_entry_ptr[i] -> nx_dns_srv_hostname_ptr);
            }
           else
                printf("hostname is not set\n");
        }
}

[Output]
----------------------------------------------------
Test SRV: record_count = 3 
record 0: IP address: 192.2.2.10
port number = 5222
priority = 20
weight = 0
hostname = alt4.xmpp.l.www.my_example.com
record 1: IP address: 192.2.2.11
port number = 5222
priority = 5
weight = 0
hostname = xmpp.l.www.my_example.com
record 2: IP address: 192.2.2.12
port number = 5222
priority = 20
weight = 0
hostname = alt1.xmpp.l.www.my_example.com
```

## <a name="nx_dns_get_serverlist_size"></a>nx_dns_get_serverlist_size

Restituisce le dimensioni dell'elenco di server del client DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_get_serverlist_size (NX_DNS *dns_ptr, UINT *size);
```
### <a name="description"></a>Descrizione

Questo servizio restituisce il numero di server DNS validi (sia IPv4 che IPv6) nell'elenco client.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS  
- **dimensioni** Restituisce il numero di server nell'elenco.

### <a name="return-values"></a>Valori restituiti

- Dimensioni elenco server DNS **NX_SUCCESS** (0x00) restituite correttamente
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
UINT my_listsize;

/* Get the number of non null DNS Servers in the Client list. */
status =  nx_dns_get_serverlist_size (&my_dns, 5, &my_listsize);

/* If status is NX_SUCCESS the size of the DNS Server list was successfully
   returned. */
```

## <a name="nx_dns_info_by_name_get"></a>nx_dns_info_by_name_get

Restituire l'indirizzo IP e la porta del server DNS in base al nome host

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_info_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr,  
                             USHORT *host_port_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'indirizzo IP e la porta del server (record di servizio) in base al nome host di input da parte della query DNS. Se non viene trovato un record del servizio, questa routine restituisce un indirizzo IP zero nel puntatore dell'indirizzo di input e un ritorno di stato di errore diverso da zero per segnalare un errore.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS  
- **HOST_NAME** Puntatore al buffer dei nomi host
- **host_address_ptr** Puntatore all'indirizzo da restituire
- **host_port_ptr** Puntatore alla porta da restituire
- **WAIT_OPTION** Opzione wait per la risposta DNS

### <a name="return-values"></a>Valori restituiti

- Record del server DNS **NX_SUCCESS** (0x00) restituito correttamente
- **NX_DNS_NO_SERVER** (0XA1) nessun server DNS registrato con il client per l'invio di query sul nome host
- La query DNS di **NX_DNS_QUERY_FAILED** (0xA3) non è riuscita. Nessuna risposta da alcun server DNS nell'elenco client o nessun record del servizio disponibile per il nome host di input.
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) chiamante non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
ULONG ip_address
USHORT port;

/* Attempt to resolve the IP address and ports for this host name. */
status =  nx_dns_info_by_name_get(&my_dns, “www.abc1234.com”, &ip_address, &port, 200);

/* If status is NX_SUCCESS the DNS query was successful and the IP address and
   report for the hostname are returned. */
```

## <a name="nx_dns_ipv4_address_by_name_get"></a>nx_dns_ipv4_address_by_name_get

Cercare l'indirizzo IPv4 per il nome host di input

### <a name="prototype"></a>Prototipo
```C
UINT nx_ dns_ipv4_address_by_name_get (NX_DNS *dns_ptr, 
                                      UCHAR *host_name_ptr, VOID *buffer, 
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia una query di tipo A con il nome host specificato per ottenere gli indirizzi IP per il nome host di input. Il client DNS copia l'indirizzo IPv4 dai record A restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* .

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

Più indirizzi IPv4 vengono archiviati nel buffer allineato a 4 byte, come illustrato di seguito:

![buffer allineato a 4 byte a più indirizzi](media/image8.png)

Se il buffer fornito non è in grado di memorizzare tutti i dati degli indirizzi IP, i record A rimanenti non vengono archiviati in *record_buffer*. Ciò consente all'applicazione di recuperare uno, alcuni o tutti i dati degli indirizzi IP disponibili nella risposta del server.

Con il numero di record restituiti in **record_count* l'applicazione può analizzare i dati dell'indirizzo IPv4 dall' *record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **host_name_ptr** Puntatore al nome host per ottenere l'indirizzo IPv4
- **buffer** Puntatore alla posizione in cui estrarre i dati IPv4
- **BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati IPv4
- **WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha ottenuto i dati IPv4
- L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto
- **NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio
- Il parametro NX_DNS_PARAM_ERROR (0xA8) non è valido per il puntatore.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
#define MAX_RECORD_COUNT  20

ULONG           record_buffer[50];
UINT            record_count;
ULONG           *ipv4_address_ptr[MAX_RECORD_COUNT];

/* Request the IPv4 address for the specified host. */
status =  nx_dns_ipv4_address_by_name_get(&client_dns, 
                                          (UCHAR *)"www.my_example.com",  
                                           record_buffer,                  
                                           sizeof(record_buffer),&record_count,                
                                           500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
        error_counter++;
}    
        else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed the IPv4
       address(es) is returned in record_buffer. */

          
            printf("------------------------------------------------------\n");
            printf("Test A: ");
            printf("record_count = %d \n", record_count);      


           /* Get the IPv4 addresses of host. */
           for(i =0; i< record_count; i++)
           {
                ipv4_address_ptr[i] = (ULONG *)(record_buffer + i * sizeof(ULONG)); 
                printf("record %d: IP address: %d.%d.%d.%d\n", i, 
                    *ipv4_address_ptr[i] >> 24,
                    *ipv4_address_ptr[i] >> 16 & 0xFF,                   
                    *ipv4_address_ptr[i] >> 8 & 0xFF,
                    *ipv4_address_ptr[i] & 0xFF);
            }

}

[Output]

------------------------------------------------------
Test A: record_count = 5 
record 0: IP address: 192.2.2.10
record 1: IP address: 192.2.2.11
record 2: IP address: 192.2.2.12
record 3: IP address: 192.2.2.13
record 4: IP address: 192.2.2.14
```

## <a name="nxd_dns_ipv6_address_by_name_get"></a>nxd_dns_ipv6_address_by_name_get

Cercare l'indirizzo IPv6 per il nome host di input

### <a name="prototype"></a>Prototipo
```C
UINT nxd_ dns_ipv6_address_by_name_get(NX_DNS *dns_ptr, 
                                      UCHAR *host_name_ptr, VOID *buffer, 
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia una query di tipo AAAA con il nome di dominio specificato per ottenere gli indirizzi IP per il nome di dominio di input. Il client DNS copia l'indirizzo IPv6 dai record AAAA restituiti nella risposta del server DNS nel percorso di memoria *record_buffer* . 

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

Il formato degli indirizzi IPv6 archiviati nel buffer allineato a 4 byte è illustrato di seguito:

![Buffer allineato a 4 byte in formato IPv6](media/image9.png)

Se l'input *record_buffer* non può contenere tutti i dati aaaa nella risposta del server, il *record_buffer* include il numero di record che si adattano e restituisce il numero di record nel buffer.

Con il numero di record AAAA restituiti in **record_count,* l'applicazione può analizzare gli indirizzi IPv6 da ogni record nel *record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **host_name_ptr** Puntatore al nome host per ottenere l'indirizzo IPv6
- **buffer** Puntatore alla posizione in cui estrarre i dati IPv6
- **BUFFER_SIZE** Dimensioni del buffer per il mantenimento dei dati IPv6
- **WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha ottenuto correttamente i dati IPv6
- L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto
- **NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio
- Il parametro NX_DNS_PARAM_ERROR (0xA8) non è valido per il puntatore.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
#define      MAX_RECORD_COUNT  20

ULONG           record_buffer[50];
UINT            record_count;
NXD_ADDRESS    *ipv6_address_ptr[MAX_RECORD_COUNT];

/* Request the IPv4 address for the specified host. */
status =  nxd_dns_ipv6_address_by_name_get(&client_dns, 
                                           (UCHAR *)"www.my_example.com", 
                                           record__buffer,                  
                                           sizeof(record_buffer), 
                                           &record_count, 500);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
        error_counter++;
}    
        else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed the IPv6 
    address(es) is (are) returned in record_buffer. */
      
    printf("------------------------------------------------------\n");
    printf("Test AAAA: ");
    printf("record_count = %d \n", record_count);      

    /* Get the IPv6 addresses of host. */
    for(i =0; i< record_count; i++)
    {

        ipv6_address_ptr[i] = 
            (NX_DNS_IPV6_ADDRESS *)(record_buffer + i * sizeof(NX_DNS_IPV6_ADDRESS)); 
             
        printf("record %d: IP address: %x:%x:%x:%x:%x:%x:%x:%x\n", i, 
                ipv6_address_ptr[i] -> ipv6_address[0]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[0]  & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[1]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[1]  & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[2]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[2]  & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[3]  >>16 & 0xFFFF,
                ipv6_address_ptr[i] -> ipv6_address[3]  & 0xFFFF);
            }
}


[Output]
------------------------------------------------------
Test AAAA: record_count = 1 
record 0: IP address: 2001:0db8:0000:f101: 0000: 0000: 0000:01003
```

## <a name="nx_dns_host_by_address_get"></a>nx_dns_host_by_address_get

Cerca un nome host da un indirizzo IP

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_host_by_address_get(NX_DNS *dns_ptr, ULONG ip_address, 
                                ULONG *host_name_ptr, 
                                ULONG max_host_name_size, 
                                ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio richiede la risoluzione dei nomi dell'indirizzo IP fornito da uno o più server DNS precedentemente specificati dall'applicazione. In caso di esito positivo, il nome host con terminazione NULL viene restituito nella stringa specificata da *host_name_ptr*. Si tratta di una funzione wrapper per il servizio *nxd_dns_host_by_address_get* e non accetta indirizzi IPv6.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore a un'istanza DNS creata in precedenza.
- **ip_address** Indirizzo IP da risolvere in un nome
- **host_name_ptr** Puntatore all'area di destinazione per il nome host
- **max_host_name_size** Dimensioni dell'area di destinazione per il nome host
- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa nei cicli del timer per una risposta del server DNS dopo ogni tentativo di query e query DNS. Le opzioni di attesa sono definite come segue:

  valore di timeout (0x00000001-0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)

  Selezionando TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server DNS non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risoluzione DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) risoluzione DNS riuscita  
- Timeout di **NX_DNS_TIMEOUT** (0xA2) durante il recupero del mutex DNS
- **NX_DNS_NO_SERVER** (0XA1) non è stato specificato alcun indirizzo del server DNS
- **NX_DNS_QUERY_FAILED** (0xA3) non ha ricevuto risposta alla query
- Indirizzo di input null **NX_DNS_BAD_ADDRESS_ERROR** (0xa4)
- L'indice **NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) fa riferimento a un tipo di indirizzo non valido (ad esempio IPv6)
- **NX_DNS_PARAM_ERROR** (0xA8) non è stato inserito alcun puntatore non valido
- **NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) input puntatore non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

**Esempio**
```C
#define BUFFER_SIZE   200

UCHAR   resolved_name[200];

/* Get the name associated with IP address 192.2.2.10.  */
status =  nx_dns_host_by_address_get(&my_dns, IP_ADDRESS(192.2.2.10),
                                     &resolved_name[0], BUFFER_SIZE, 450);

/* If status is NX_SUCCESS the name associated with the IP address
   can be found in the resolved_name variable.  */
```

## <a name="nxd_dns_host_by_address_get"></a>nxd_dns_host_by_address_get

Cercare un nome host dall'indirizzo IP

### <a name="prototype"></a>Prototipo
```C
UINT nxd_dns_host_by_address_get(NX_DNS *dns_ptr, 
                                 NXD_ADDRESS ip_address, 
                                 ULONG *host_name_ptr, 
                                 ULONG max_host_name_size, 
                                 ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio richiede la risoluzione dei nomi dell'indirizzo IPv6 o IPv4 nell'argomento *ip_address* input da uno o più server DNS precedentemente specificati dall'applicazione. In caso di esito positivo, il nome host con terminazione NULL viene restituito nella stringa specificata da *host_name_ptr*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore a un'istanza DNS creata in precedenza.
- **ip_address** Indirizzo IP da risolvere in un nome
- **host_name_ptr** Puntatore all'area di destinazione per il nome host
- **max_host_name_size** Dimensioni dell'area di destinazione per il nome host
- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa nei cicli del timer per una risposta del server DNS dopo ogni tentativo di query e query DNS. Le opzioni di attesa sono definite come segue:

  valore di timeout (0x00000001 tramite 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)  

  Selezionando TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server DNS non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risoluzione DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) risoluzione DNS riuscita  
- Timeout di **NX_DNS_TIMEOUT** (0xA2) durante il recupero del mutex DNS
- **NX_DNS_NO_SERVER** (0XA1) non è stato specificato alcun indirizzo del server DNS
- **NX_DNS_QUERY_FAILED** (0xA3) non ha ricevuto risposta alla query
- Indirizzo di input null **NX_DNS_BAD_ADDRESS_ERROR** (0xa4)
- **NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

**Esempio**
```C
UCHAR   resolved_name[200];
NXD_ADDRESS host_address;

host_address.nxd_ip_version = NX_IP_VERISON_V6;
host_address.nxd_ip_address.v6[0] = 0x20010db8;
host_address.nxd_ip_address.v6[1] = 0x0;
host_address.nxd_ip_address.v6[2] = 0xf101;
host_address.nxd_ip-address.v6[3] = 0x108;

/* Get the name associated with theinput host_address. */
status =  nxd_dns_host_by_address_get(&my_dns, &host_address,
                                      resolved_name, sizeof(resolved_name), 4000);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
     error_counter++;
}     
else     
{
     printf("------------------------------------------------------\n");
     printf("Test PTR: %s\n", record_buffer);
}

/* If status is NX_SUCCESS the name associated with the IP address
   can be found in the resolved_name variable. */


[Output]

 ------------------------------------------------------
 Test PTR: my_example.net
```

## <a name="nx_dns_host_by_name_get"></a>nx_dns_host_by_name_get

Cercare un indirizzo IP dal nome host

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_host_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio richiede la risoluzione dei nomi del nome fornito da uno o più server DNS precedentemente specificati dall'applicazione. In caso di esito positivo, l'indirizzo IP associato viene restituito nella destinazione a cui punta host_address_ptr. Si tratta di una funzione wrapper per il servizio *nxd_dns_host_by_name_get* ed è limitata all'input dell'indirizzo IPv4.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore a un'istanza DNS creata in precedenza.
- **HOST_NAME** Puntatore al nome host
- **host_address_ptr** Indirizzo IP del server DNS restituito
- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa della risoluzione DNS. Le opzioni di attesa sono definite come segue:

  valore di timeout (0x00000001 tramite 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)

  Selezionando TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server DNS non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risoluzione DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) la risoluzione DNS è riuscita.
- **NX_DNS_NO_SERVER** (0XA1) non è stato specificato alcun indirizzo del server DNS
- **NX_DNS_QUERY_FAILED** (0xA3) non ha ricevuto risposta alla query
- NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido
- NX_PTR_ERROR (0x07) input puntatore non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

**Esempio**
```C
ULONG host_address;

/* Get the IP address for the name “www.my_example.com”. */
   status =  nx_dns_host_by_name_get(&my_dns, “www.my_example.com”, &host_address, 4000);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{

    /* If status is NX_SUCCESS the IP address for “www.my_example.com” can be found 
        in the “ip_address” variable. */
        
    printf("------------------------------------------------------\n");
    printf("Test A: \n");
    printf("IP address: %d.%d.%d.%d\n",
    host_address >> 24,
    host_address >> 16 & 0xFF,                   
    host_address >> 8 & 0xFF,
    host_address & 0xFF);
}

[Output]
 ------------------------------------------------------
Test A: 
IP address: 192.2.2.10
```

## <a name="nxd_dns_host_by_name_get"></a>nxd_dns_host_by_name_get

Ricerca di un indirizzo IP dal nome host

### <a name="prototype"></a>Prototipo
```C
UINT nxd_dns_host_by_name_get(NX_DNS *dns_ptr, ULONG *host_name, 
                              NXD_ADDRESS *host_address_ptr, 
                              ULONG wait_option, UINT lookup_type);
```

### <a name="description"></a>Descrizione

Questo servizio richiede la risoluzione dei nomi dell'indirizzo IP fornito da uno o più server DNS precedentemente specificati dall'applicazione. In caso di esito positivo, l'indirizzo IP associato viene restituito in un NXD_ADDRESS a cui punta *host_address_ptr*. Se il chiamante imposta in modo specifico l'input lookup_type per NX_IP_VERSION_V6, il servizio invierà una query per un indirizzo IPv6 host (record AAAA). Se il chiamante imposta in modo specifico l'input lookup_type per NX_IP_VERSION_V4, il servizio invierà una query per un indirizzo IPv4 host (record A).

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore a un'istanza del client DNS creata in precedenza.
- **HOST_NAME** Puntatore al nome host per trovare un indirizzo IP
- **host_address_ptr** Puntatore alla destinazione per NXD_ADDRESS contenente l'indirizzo IP
- **WAIT_OPTION** Definisce per quanto tempo il servizio resterà in attesa nei cicli del timer per la risposta del server DNS per ogni trasmissione e ritrasmissione della query. Le opzioni di attesa sono definite come segue:

  valore di timeout (0x00000001 tramite 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)  

  Selezionando TX_WAIT_FOREVER il thread chiamante verrà sospeso per un tempo illimitato fino a quando un server DNS non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di segni di spunta del timer per rimanere sospesi durante l'attesa della risoluzione DNS.

- **lookup_type** Indica il tipo di ricerca (A vs AAAA).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) la risoluzione DNS è riuscita.
- **NX_DNS_NO_SERVER** (0XA1) non è stato specificato alcun indirizzo del server DNS
- **NX_DNS_QUERY_FAILED** (0xA3) non ha ricevuto risposta alla query
- Indirizzo di input null **NX_DNS_BAD_ADDRESS_ERROR** (0xa4)
- **NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) input puntatore non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

**Esempio**
```C
NXD_ADDRESS host_ipduo_address;

/* Create an AAAA query to obtain the IPv6 address for the host “www.my_example.com”. */
status =  nxd_dns_host_by_name_get(&my_dns, “www.my_example.com”, 
                                   &host_ipduo_address, 4000, 
                                   NX_IP_VERSION_V6);

if (status != NX_SUCCESS)
{
        error_counter++;
}
else
{
/* If status is NX_SUCCESS the IP address for “www.my_example.com” can be 
   found in the “ip_address” variable. */

    printf("------------------------------------------------------\n");
    printf("Test AAAA: \n");

    printf("IP address: %x:%x:%x:%x:%x:%x:%x:%x\n", 
           host_ipduo_address.nxd_ip_address.v6[0]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[0]  & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[1]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[1]  & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[2]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[2]  & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[3]  >>16 & 0xFFFF,
           host_ipduo_address.nxd_ip_address.v6[3]  & 0xFFFF);
}

[Output]

------------------------------------------------------
Test AAAA: 
IP address: 2607:f8b0:4007:800:0:0:0:1008
```

Un altro esempio di utilizzo di questo servizio ora, questa volta usando gli indirizzi IPv4 e i tipi di record, è illustrato di seguito:
```C
/* Create a query to obtain the IPv4 address for the host “www.my_example.com”. */
status =  nxd_dns_host_by_name_get(&my_dns, “www.my_example.com”, &ip_address, 4000, 
                                   NX_IP_VERSION_V4);

/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else     
{   
/* If status is NX_SUCCESS the IP address for “www.my_example.com” can be 
   found in the “ip_address” variable. */
  
     printf("------------------------------------------------------\n");
     printf("Test A: \n");
     printf("IP address: %d.%d.%d.%d\n",
            host_ipduo_address.nxd_ip_address.v4 >> 24,
            host_ipduo_address.nxd_ip_address.v4 >> 16 & 0xFF,                   
            host_ipduo_address.nxd_ip_address.v4 >> 8 & 0xFF,
            host_ipduo_address.nxd_ip_address.v4 & 0xFF);
 }

[Output]

------------------------------------------------------
Test A: 
IP address: 192.2.2.10
```

## <a name="nx_dns_host_text_get"></a>nx_dns_host_text_get

Cerca la stringa di testo per il nome di dominio di input

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_host_text_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                          UCHAR *record_buffer, 
                          UINT buffer_size, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia una query di tipo TXT con il nome di dominio e il buffer specificati per ottenere i dati stringa arbitrari.

Il client DNS copia la stringa di testo nel record TXT nella risposta del server DNS nel percorso di memoria *record_buffer* . 

> [!NOTE]
> Non è necessario che la record_buffer sia allineata a 4 byte per ricevere i dati.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **HOST_NAME** Puntatore al nome dell'host in cui eseguire la ricerca
- **record_buffer** Puntatore alla posizione in cui estrarre i dati TXT
- **BUFFER_SIZE** Dimensioni del buffer per memorizzare i dati TXT
- **WAIT_OPTION** Opzione wait per la ricezione della risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- Stringa TXT ottenuta **NX_SUCCESS** (0x00) riuscita
- L'elenco dei server client **NX_DNS_NO_SERVER** (0xA1) è vuoto
- **NX_DNS_QUERY_FAILED** (0XA3) non è stata ricevuta alcuna risposta DNS valida
- NX_PTR_ERROR (0x07) input puntatore non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) non è stato inserito alcun puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

######   
Esempio
```C
CHAR            record_buffer[50];

/* Request the text string for the specified host. */
status =  nx_dns_host_text_get(&client_dns, (UCHAR *)"www.my_example.com", 
                               record_buffer, 
                               sizeof(record_buffer), 500);


/* Check for DNS query error. */
if (status != NX_SUCCESS)
{
     error_counter++;
}
else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and the
       text string is returned in record_buffer. */
 
     printf("------------------------------------------------------\n");
     printf("Test TXT:\n %s\n", record_buffer);
} 


[Output]

------------------------------------------------------
Test TXT: 
v=spf1 include:_www.my_example.com ip4:192.2.2.10/31 ip4:192.2.2.11/31 ~all
```

## <a name="nx_dns_packet_pool_set"></a>nx_dns_packet_pool_set

Impostare il pool di pacchetti client DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_packet_pool_set(NX_DNS *dns_ptr, NX_PACKET_POOL *pool_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio imposta un pool di pacchetti creato in precedenza come pool di pacchetti client DNS. Il client DNS userà questo pool di pacchetti per inviare query DNS, quindi il payload del pacchetto non deve essere inferiore a NX_DNS_PACKET_PAYLOAD che include le intestazioni Ethernet, IP e UDP ed è definito in *nxd_dns. h.* 

> [!NOTE]
> *W* Hen il client DNS viene eliminato, il pool di pacchetti non viene eliminato con esso ed è responsabilità dell'applicazione eliminare il pool di pacchetti quando non è più necessario.
>
> Questo servizio è disponibile solo se l'opzione di configurazione NX_DNS_CLIENT_USER_CREATE_PACKET_POOL è definita in *nxd_dns. h*

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore a un'istanza del client DNS creata in precedenza.
- **pool_ptr** Puntatore al pool di pacchetti creato in precedenza

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) completato correttamente.
- Client di **NX_NOT_ENABLED** (0x14) non configurato per questa opzione
- NX_PTR_ERROR (0x07) un puntatore client IP o DNS non valido.
- Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
NXD_DNS my_dns;
NX_PACKET_POOL client_pool;
NX_IP *ip_ptr;


/* Create the DNS Client. */
status =  nx_dns_create(&my_dns, ip_ptr, “My DNS Client”);

/* Create a packet pool for the DNS Client. */
status =  nx_packet_pool_create(&client_pool, "DNS Client Packet Pool", 
                                NX_DNS_PACKET_PAYLOAD, free_mem_pointer, 
                                NX_DNS_PACKET_POOL_SIZE);

/* Set the DNS Client packet pool. */
status =  nx_dns_packet_pool_set(&my_dns, &client_pool);

/* If status is NX_SUCCESS the DNS Client packet pool was successfully set. */
```

## <a name="nx_dns_server_add"></a>nx_dns_server_add

Aggiungi indirizzo IP del server DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_server_add(NX_DNS *dns_ptr, ULONG server_address);
```
### <a name="description"></a>Descrizione

Questo servizio aggiunge un server DNS IPv4 all'elenco dei server.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.  
- **server_address** Indirizzo IP del server DNS

### <a name="return-values"></a>Valori restituiti

- Aggiunta del server **NX_SUCCESS** (0x00) completata
- **NX_DNS_DUPLICATE_ENTRY**  
**NX_NO_MORE_ENTRIES** (0x17) non sono più consentiti server DNS (elenco completo)
- **NX_DNS_PARAM_ERROR** (0xA8) non è stato inserito alcun puntatore non valido
- **NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) input puntatore non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio
- Input dell'indirizzo del server NX_DNS_BAD_ADDRESS_ERROR (0xA4) null

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
/* Add a DNS Server at IP address 202.2.2.13. */
status =  nx_dns_server_add(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully added. */
```

## <a name="nxd_dns_server_add"></a>nxd_dns_server_add

Aggiungere un server DNS all'elenco client

### <a name="prototype"></a>Prototipo
```C
UINT nxd_dns_server_add(NX_DNS *dns_ptr, NXD_ADDRESS *server_address);
```
### <a name="description"></a>Descrizione

Questo servizio aggiunge l'indirizzo IP di un server DNS all'elenco dei server client DNS. È possibile che il server_address sia un indirizzo IPv4 o IPv6. Se il client desidera essere in grado di accedere allo stesso server tramite l'indirizzo IPv4 o IPv6, deve aggiungere entrambi gli indirizzi IP come voci all'elenco dei server.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.
- **server_address** Puntatore al NXD_ADDRESS contenente l'indirizzo IP del server DNS.

### <a name="return-values"></a>Valori restituiti

- Aggiunta del server **NX_SUCCESS** (0x00) completata
- **NX_DNS_DUPLICATE_ENTRY**  
**NX_NO_MORE_ENTRIES** (0x17) non sono più consentiti server DNS (elenco completo) 
- **NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato
- **NX_DNS_PARAM_ERROR** (0xA8) non è stato inserito alcun puntatore non valido
- NX_PTR_ERROR (0x07) input puntatore non valido
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio
- Input dell'indirizzo del server NX_DNS_BAD_ADDRESS_ERROR (0xA4) null
- L'indice NX_DNS_INVALID_ADDRESS_TYPE (0xB2) fa riferimento a un tipo di indirizzo non valido (ad esempio IPv6)

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
NXD_ADDRESS server_address;

server_address.nxd_ip_version = NX_IP_VERISON_V6;
server_address.nxd_ip_address.v6[0] = 0x20010db8;
server_address.nxd_ip_address.v6[1] = 0x0;
server_address.nxd_ip_address.v6[2] = 0xf101;
server_address.nxd_ip-address.v6[3] = 0x108;


/* Add a DNS Server with the IP address pointed to by the server_address input. */
status =  nxd_dns_server_add(&my_dns, &server_address);

/* If status is NX_SUCCESS a DNS Server was successfully added. */
```

## <a name="nx_dns_server_get"></a>nx_dns_server_get

Restituire un server DNS IPv4 dall'elenco client

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_server_get(NX_DNS *dns_ptr, UINT index, 
                        ULONG *dns_server_address);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'indirizzo del server DNS IPv4 dall'elenco dei server in corrispondenza dell'indice specificato. 

> [!NOTE]
> L'indice è in base zero. Se l'indice di input supera le dimensioni dell'elenco dei client DNS, viene trovato un indirizzo IPv6 in corrispondenza dell'indice o viene trovato un indirizzo null in corrispondenza dell'indice specificato. viene restituito un errore. È possibile chiamare il servizio *nx_dns_get_serverlist_size* prima di ottenere il numero di server DNS nell'elenco client.

Questo servizio supporta solo indirizzi IPv4. Chiama il servizio *nxd_dns_server_get* che supporta gli indirizzi sia IPv4 che IPv6.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS  
- **Indice** di Indicizzare nell'elenco dei server del client DNS
- **dns_server_address** Puntatore all'indirizzo IP del server DNS

### <a name="return-values"></a>Valori restituiti

- Il server **NX_SUCCESS** (0x00) ha restituito un esito positivo
- **NX_DNS_SERVER_NOT_FOUND** (0xA9) punta a uno slot vuoto
- L'indice **NX_DNS_BAD_ADDRESS_ERROR** (0xa4) fa riferimento a un indirizzo null
- L'indice **NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) fa riferimento a un tipo di indirizzo non valido (ad esempio IPv6)
- **NX_DNS_PARAM_ERROR** (0xA8) non è un input non puntatore valido
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
ULONG my_server_address;

/* Get the DNS Server at index 5 (zero based) into the Client list. */
status =  nx_dns_server_get(&my_dns, 5, &my_server_addres);

/* If status is NX_SUCCESS a DNS Server was successfully
   returned. */
```

## <a name="nxd_dns_server_get"></a>nxd_dns_server_get

Restituire un server DNS dall'elenco client

### <a name="prototype"></a>Prototipo
```C
UINT nxd_dns_server_get(NX_DNS *dns_ptr, UINT index, 
                        NXD_ADDRESS *dns_server_address);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'indirizzo IP del server DNS dall'elenco dei server in corrispondenza dell'indice specificato. 

> [!NOTE]
> L'indice è in base zero. Se l'indice di input supera la dimensione dell'elenco dei client DNS oppure viene trovato un indirizzo null in corrispondenza dell'indice specificato, viene restituito un errore. Il servizio *nx_dns_get_serverlist_size* può essere chiamato per primo per ottenere il numero di server DNS nell'elenco dei server.

Questo servizio supporta gli indirizzi IPv4 e IPv6.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS  
- **Indice** di Indicizzare nell'elenco dei server del client DNS
- **dns_server_address** Puntatore all'indirizzo IP del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) ha restituito l'indirizzo IP del server
- **NX_DNS_SERVER_NOT_FOUND** (0xA9) punta a uno slot vuoto
- L'indice **NX_DNS_BAD_ADDRESS_ERROR** (0xa4) punta all'indirizzo del server null
- L'indice **NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) fa riferimento a un tipo di indirizzo non valido (ad esempio IPv6)
- **NX_DNS_PARAM_ERROR** (0xA8) non è stato inserito alcun puntatore non valido
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
NXD_ADDRESS my_server_address;

/* Get the DNS Server at index 5 (zero based) into the Client list. */
status =  nxd_dns_server_get(&my_dns, 5, &my_server_addres);

/* If status is NX_SUCCESS a DNS Server was successfully
   returned. */
```

## <a name="nx_dns_server_remove"></a>nx_dns_server_remove

Rimuovere un server DNS IPv4 dall'elenco client

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_server_remove(NX_DNS *dns_ptr, ULONG server_address);
```
### <a name="description"></a>Descrizione

Questo servizio rimuove un server DNS IPv4 dall'elenco client. Si tratta di una funzione wrapper per *nxd_dns_server_remove*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.
- **server_address** Indirizzo IP del server DNS.

### <a name="return-values"></a>Valori restituiti

- Il server DNS **NX_SUCCESS** (0x00) è stato rimosso
- Server **NX_DNS_SERVER_NOT_FOUND** (0xA9) non presente nell'elenco client
- Input dell'indirizzo del server **NX_DNS_BAD_ADDRESS_ERROR** (0XA4) null
- **NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
/* Remove the DNS Server at IP address is 202.2.2.13.  */
status =  nx_dns_server_remove(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully
   removed.  */
```

## <a name="nxd_dns_server_remove"></a>nxd_dns_server_remove

Rimuovere un server DNS dall'elenco client

### <a name="prototype"></a>Prototipo
```C
UINT nxd_dns_server_remove(NX_DNS *dns_ptr, NXD_ADDRESS *server_address);
```
### <a name="description"></a>Descrizione

Questo servizio rimuove dall'elenco client un server DNS dell'indirizzo IP specificato. L'indirizzo IP di input accetta indirizzi IPv4 e IPv6. Dopo la rimozione del server, i server rimanenti spostano verso il basso di un indice nell'elenco per riempire lo slot sgomberato.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.
- **server_address** Puntatore al server DNS NXD_ADDRESS dati che contengono l'indirizzo IP del server.

### <a name="return-values"></a>Valori restituiti

- Il server DNS **NX_SUCCESS** (0x00) è stato rimosso
- Server **NX_DNS_SERVER_NOT_FOUND** (0xA9) non presente nell'elenco client
- Input dell'indirizzo del server **NX_DNS_BAD_ADDRESS_ERROR** (0XA4) null
- **NX_DNS_IPV6_NOT_SUPPORTED** (0XB3) non è in grado di elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio
- L'indice NX_DNS_INVALID_ADDRESS_TYPE (0xB2) fa riferimento a un tipo di indirizzo non valido (ad esempio IPv6)

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
NXD_ADDRESS server_address;

server_address.nxd_ip_version = NX_IP_VERISON_V6;
server_address.nxd_ip_address.v6[0] = 0x20010db8;
server_address.nxd_ip_address.v6[1] = 0x0;
server_address.nxd_ip_address.v6[2] = 0xf101;
server_address.nxd_ip-address.v6[3] = 0x108;


/* Remove the DNS Server at the specified IP address from the Client list. */
status =  nxd_dns_server_remove(&my_dns,&server_ADDRESS);

/* If status is NX_SUCCESS a DNS Server was successfully removed. */
```

## <a name="nx_dns_server_remove_all"></a>nx_dns_server_remove_all

Rimuovere tutti i server DNS dall'elenco client

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_server_remove_all(NX_DNS *dns_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio rimuove tutti i server DNS dall'elenco client.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.

### <a name="return-values"></a>Valori restituiti

- Server DNS **NX_SUCCESS** (0x00) rimossi correttamente
- **NX_DNS_ERROR** (messaggi 0XA0) non è in grado di ottenere il mutex di protezione
- NX_PTR_ERROR (0x07) un puntatore IP o DNS non valido.
- NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
/* Remove all DNS Servers from the Client list. */
status =  nx_dns_server_remove_all(&my_dns);

/* If status is NX_SUCCESS all DNS Servers were successfully removed. */
```