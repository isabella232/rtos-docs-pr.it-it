---
title: Capitolo 3 - Descrizione dei Azure RTOS client DNS di NetX Duo
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS DNS di NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 10368edf3cdf15d32bddbd5bd943681b3ff3dd1aa1a7042d1b9bb2bf0e71699f
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116791865"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-dns-client-services"></a>Capitolo 3 - Descrizione dei Azure RTOS client DNS di NetX Duo

Questo capitolo contiene una descrizione di tutti i Azure RTOS DNS NetX (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **grassetto** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_dns_authority_zone_start_get** *cercare l'inizio di una zona di autorità associata al nome host specificato*

- **nx_dns_cache_initialize** *inizializzare una cache DNS.*

- **nx_dns_cache_notify_clear** *cancella la funzione di notifica completa della cache.*

- **nx_dns_cache_notify_set** *impostare la funzione di notifica completa della cache.*

- **nx_dns_cname_get** *cercare il nome di dominio canonico per l'alias del nome di dominio di input*

- **nx_dns_create** *creare un'istanza del client DNS*

- **nx_dns_delete** *eliminare un'istanza del client DNS*

- **nx_dns_domain_name_server_get** *cercare i server dei nomi autorevoli per la zona del dominio di input*

- **nx_dns_domain_mail_exchange_get** *cercare lo scambio di posta associato al nome host specificato.*

- **nx_dns_domain_service_get** cercare i servizi associati *al nome host specificato*

- **nx_dns_get_serverlist_size** *restituire le dimensioni dell'elenco di server client DNS*

- **nx_dns_info_by_name_get** *indirizzo IP mittente, esecuzione di query sulle porte sul nome host di input*

- **nx_dns_ipv4_address_by_name_get** *cercare l'indirizzo IPv4 dal nome host specificato*

- **nxd_dns_ipv6_address_by_name_get** *cercare l'indirizzo IPv6 dal nome host specificato*

- **nx_dns_host_by_address_get** wrapper per nxd_dns_host_by_address_get cercare un nome host da un indirizzo IP specificato *(supporta solo indirizzi IPv4)*

- **nxd_dns_host_by_address_get** *cercare un indirizzo IP dal nome host di input (supporta indirizzi IPv4 e IPv6)*

- **nx_dns_host_by_name_get** wrapper per nxd_dns_host_by_address_get cercare un nome host dall'indirizzo specificato *(supporta solo indirizzi IPv4)*

- **nxd_dns_host_by_name_get** *cercare un indirizzo IP dal nome host di input (supporta sia gli indirizzi IPv4 che IPv6)*

- **nx_dns_host_text_get** *cercare i dati di testo per il nome di dominio di input*

- **nx_dns_packet_pool_set** *impostare il pool di pacchetti del client DNS*

- **nx_dns_server_add** *wrapper per nxd_dns_server_add* aggiungere un server DNS all'indirizzo specificato all'elenco client *(supporta solo IPv4)*

- **nxd_dns_server_add** aggiungere un server DNS dell'indirizzo IP specificato all'elenco *di server client (supporta indirizzi IPv4 o IPv6)*

- **nx_dns_server_get** *restituisce il server DNS nell'elenco Client (supporta solo indirizzi IPv4)*

- **nxd_dns_server_get** *restituisce il server DNS nell'elenco Client (supporta sia gli indirizzi IPv4 che IPv6)*

- **nx_dns_server_remove** *wrapper per nxd_dns_server_remove rimuovere un server DNS dall'elenco client*

- **nxd_dns_server_remove** rimuovere un server DNS dell'indirizzo IP specificato dall'elenco Client (supporta sia *gli indirizzi IPv4 che IPv6)*

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

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, questo servizio invia una query di tipo SOA con il nome di dominio specificato per ottenere l'inizio della zona di autorità per il nome di dominio di input. Il client DNS copia i record SOA restituiti nella risposta del server DNS nel percorso *record_buffer* memoria.

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

In NetX Duo DNS Client il tipo di record SOA, NX_DNS_SOA_ENTRY, viene salvato come sette parametri di 4 byte, per un totale di 28 byte:

- **nx_dns_soa_host_mname_ptr** Puntatore all'origine dati primaria per questa zona.
- **nx_dns_soa_host_rname_ptr** Puntatore alla cassetta postale responsabile di questa zona
- **nx_dns_soa_serial** Numero di versione della zona
- **nx_dns_soa_refresh** Intervallo di aggiornamento
- **nx_dns_soa_retry** Intervallo tra i tentativi di query SOA
- **nx_dns_soa_expire** Durata dell'intervallo di tempo in cui SCADE SOA
- **nx_dns_soa_minmum** Campo TTL minimo nei messaggi di risposta DNS del nome host SOA

L'archiviazione di due record SOA è illustrata di seguito. I record SOA contenenti dati a lunghezza fissa vengono immessi a partire dall'inizio del buffer. I puntatori MNAME e RNAME puntano ai dati a lunghezza variabile (nomi host) archiviati nella parte inferiore del buffer. I record SOA aggiuntivi vengono immessi dopo il primo record ("record SOA aggiuntivi...") e i relativi dati di lunghezza variabile vengono archiviati sopra i dati di lunghezza variabile dell'ultima voce ("dati aggiuntivi di lunghezza variabile SOA"):

![Archiviazione di due record SOA](media/image4.png)

Se il *record_buffer* di input non può contenere tutti i dati SOA nella risposta del server, il *record_buffer* contiene il numero di record che rientra e restituisce il numero di record nel buffer.

Con il numero di record SOA restituiti in **record_count,* l'applicazione può analizzare i dati da *record_buffer* ed estrarre l'inizio delle stringhe del nome host dell'autorità di zona.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **host_name** Puntatore al nome host per cui ottenere i dati SOA
- **record_buffer** Puntatore alla posizione in cui estrarre i dati SOA
- **buffer_size** Dimensioni del buffer per contenere i dati SOA
- **record_count** Puntatore al numero di record SOA recuperati
- **wait_option** Opzione Wait per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) I dati SOA sono stati ottenuti correttamente
- **NX_DNS_NO_SERVER** server client (0xA1) è vuoto
- **NX_DNS_QUERY_FAILED** (0xA3) Nessuna risposta DNS valida ricevuta
- NX_PTR_ERROR (0x07) Puntatore DNS o IP non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) Input non puntatore non valido

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

Questo servizio crea e inizializza una cache DNS.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.
- **cache_ptr** Puntatore alla cache DNS.
- **cache_size** Dimensioni della cache DNS, in byte.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) DNS cache successfully initialized (Cache DNS di NX_SUCCESS (0x00) inizializzata correttamente
- NX_DNS_PARAM_ERROR (0xA8) Input non puntatore non valido
- NX_DNS_CACHE_ERROR (0xB7) Puntatore cache non valido.
- NX_PTR_ERROR (0x07) Puntatore DNS non valido. 
- NX_DNS_ERROR cache (0xA0) non è allineata a 4 byte.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
/* Initialize the DNS Cache.  */
status =  nx_dns_cache_initialize(&my_dns, &dns_cache, 2048);

/* If status is NX_SUCCESS DNS Cache was successfully initialized.  */
```

## <a name="nx_dns_cache_notify_clear"></a>nx_dns_cache_notify_clear

Cancellare la funzione di notifica completa della cache DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_cache_notify_clear(NX_DNS *dns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio cancella la funzione di notifica completa della cache.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** cache DNS (0x00) impostata correttamente
- NX_DNS_PARAM_ERROR (0xA8) Input non puntatore non valido
- NX_PTR_ERROR (0x07) Puntatore DNS non valido.

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

- **NX_SUCCESS** cache DNS (0x00) impostata correttamente
- NX_DNS_PARAM_ERROR (0xA8) Input non puntatore non valido
- NX_PTR_ERROR (0x07) Puntatore DNS non valido.

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

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito in *nxd_dns.h,* questo servizio invia una query di tipo CNAME con il nome di dominio specificato per ottenere il nome di dominio canonico. Il client DNS copia la stringa CNAME restituita nella risposta del server DNS nel percorso *record_buffer* memoria.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **host_name** Puntatore al nome host per cui ottenere i dati CNAME
- **record_buffer** Puntatore alla posizione in cui estrarre i dati CNAME
- **buffer_size** Dimensioni del buffer per contenere i dati CNAME
- **wait_option** Opzione Wait per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) I dati CNAME sono stati ottenuti correttamente
- **NX_DNS_NO_SERVER** server client (0xA1) è vuoto
- **NX_DNS_QUERY_FAILED** (0xA3) Nessuna risposta DNS valida ricevuta
- NX_PTR_ERROR (0x07) Puntatore DNS o IP non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) Input non puntatore non valido

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
> L'applicazione deve garantire che il payload dei pacchetti del pool di pacchetti usato dal client DNS sia sufficientemente grande per il messaggio DNS di 512 byte massimo, oltre alle intestazioni UDP, IP ed Ethernet. Se il client DNS crea un proprio pool di pacchetti, questo viene definito da NX_DNS_PACKET_PAYLOAD e NX_DNS_PACKET_POOL_SIZE.

Se l'applicazione client DNS preferisce fornire un pool di pacchetti creato in precedenza, il payload per il client DNS IPv4 deve essere di 512 byte per il DNS massimo più 20 byte per l'intestazione IP, 8 byte per l'intestazione UDP e 14 byte per l'intestazione Ethernet. Per IPv6 l'unica differenza è che l'intestazione IP è di 40 byte, pertanto il pacchetto deve contenere l'intestazione IPv6 di 40 byte.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **ip_ptr** Puntatore all'istanza IP creata in precedenza.  
- **domain_name** Puntatore al nome di dominio per l'istanza DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Creazione DNS riuscita
- **NX_DNS_ERROR** errore di creazione DNS 0xA0 (0xA0)
- NX_PTR_ERROR (0x07) Puntatore DNS o IP non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio elimina un'istanza del client DNS creata in precedenza e libera le relative risorse. 

> [!NOTE]
> Se NX_DNS_CLIENT_USER_CREATE_PACKET_POOL è definito e al client DNS è stato assegnato un pool di pacchetti definito dall'utente, è responsabilità dell'applicazione eliminare il pool di pacchetti del client DNS se non è più necessario.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore all'istanza del client DNS creata in precedenza.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Eliminazione del client DNS riuscita.
- NX_PTR_ERROR (0x07) Puntatore ip o client DNS non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, questo servizio invia una query di tipo NS con il nome di dominio specificato per ottenere i server dei nomi per il nome di dominio di input. Il client DNS copia i record NS restituiti nella risposta del server DNS nel percorso *record_buffer* memoria.

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

In NetX Duo DNS Client il tipo di dati NS, NX_DNS_NS_ENTRY, viene salvato come due parametri a 4 byte:

- **nx_dns_ns_ipv4_address** Indirizzo IPv4 del server dei nomi
- **nx_dns_ns_hostname_ptr** Puntatore al nome host del server dei nomi

Il buffer illustrato di seguito contiene quattro NX_DNS_NS_ENTRY record. Il puntatore alla stringa del nome host in ogni voce punta alla stringa del nome host corrispondente nella metà inferiore del buffer:

![Contiene quattro NX_DNS_NS_ENTRY record](media/image5.png)

Se il *record_buffer* di input non può contenere tutti i dati NS nella risposta del server, il *record_buffer* contiene tutti i record che saranno adatti e restituisce il numero di record nel buffer.

Con il numero di record NS restituiti in **record_count,* l'applicazione può analizzare l'indirizzo IP e il nome host di ogni record *nel record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **host_name** Puntatore al nome host per cui ottenere i dati NS
- **record_buffer** Puntatore alla posizione in cui estrarre i dati NS
- **buffer_size** Dimensioni del buffer per contenere i dati NS
- **record_count** Puntatore al numero di record NS recuperati
- **wait_option** Opzione Wait per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) I dati NS sono stati ottenuti correttamente
- **NX_DNS_NO_SERVER** (0xA1) L'elenco del server client è vuoto
- **NX_DNS_QUERY_FAILED** (0xA3) Nessuna risposta DNS valida ricevuta
- NX_DNS_PARAM_ERROR (0xA8) Input non puntatore non valido
- NX_PTR_ERROR (0x07) Puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Cercare gli scambi di posta per il nome host di input

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_domain_mail_exchange_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                     VOID *record_buffer,                                        
                                     UINT buffer_size, 
                                     UINT *record_count, 
                                     ULONG wait_option);
```

### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES definito, questo servizio invia una query di tipo MX con il nome di dominio specificato per ottenere lo scambio di posta per il nome di dominio di input. Il client DNS copia i record MX restituiti nella risposta del server DNS nel percorso record_buffer *memoria.* 

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

In NetX Duo DNS Client il tipo di record di scambio di posta elettronica, NX_DNS_MAIL_EXCHANGE_ENTRY, viene salvato come quattro parametri, per un totale di 12 byte:

- **nx_dns_mx_ipv4_address** Indirizzo IPv4 di scambio di posta elettronica 4 byte
- **nx_dns_mx_preference** Preferenza 2 byte
- **nx_dns_mx_reserved0** Riservato 2 byte
- **nx_dns_mx_hostname_ptr** Puntatore al nome host del server di scambio di posta elettronica 4 byte

Di seguito è riportato un buffer contenente quattro record MX. Ogni record contiene i dati a lunghezza fissa dell'elenco precedente. Il puntatore al nome host del server di scambio di posta punta al nome host corrispondente nella parte inferiore del buffer.

![Buffer contenente quattro record MX](media/image6.png)

Se il *record_buffer* di input non può contenere tutti i dati MX nella risposta del server, il *record_buffer* contiene il numero di record che si adatterà e restituisce il numero di record nel buffer.

Con il numero di record MX restituiti in **record_count,* l'applicazione può analizzare i parametri MX, incluso il nome host di posta elettronica di ogni record nel *record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **host_name** Puntatore al nome host per cui ottenere i dati MX
- **record_buffer** Puntatore alla posizione in cui estrarre i dati MX
- **buffer_size** Dimensioni del buffer per contenere i dati MX
- **record_count** Puntatore al numero di record MX recuperati
- **wait_option** Opzione di attesa per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) I dati MX sono stati ottenuti correttamente
- **NX_DNS_NO_SERVER** (0xA1) L'elenco del server client è vuoto
- **NX_DNS_QUERY_FAILED** (0xA3) Nessuna risposta DNS valida ricevuta
- NX_DNS_PARAM_ERROR (0xA8) Input non puntatore non valido
- NX_PTR_ERROR (0x07) Puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Cercare i servizi forniti dal nome host di input

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_domain_service_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                VOID *record_buffer, UINT buffer_size, 
                                UINT *record_count, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES definito, questo servizio invia una query di tipo SRV con il nome di dominio specificato per cercare i servizi e il relativo numero di porta associato al dominio specificato. Il client DNS copia i record SRV restituiti nella risposta del server DNS nel percorso record_buffer *memoria.* 

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

In NetX Duo DNS Client il tipo di record del servizio, NX_DNS_SRV_ ENTRY, viene salvato come sei parametri, per un totale di 16 byte. In questo modo i dati SRV a lunghezza variabile possono essere archiviati in modo efficiente in memoria:

- **Indirizzo IPv4 del** server nx_dns_srv_ipv4_address 4 byte
- **Priorità server** nx_dns_srv_priority 2 byte
- **Peso del** server nx_dns_srv_weight 2 byte
- **Numero di porta del** servizio nx_dns_srv_port_number 2 byte
- **Riservato per l'allineamento a 4 byte** nx_dns_srv_reserved0 2 byte
- **Puntatore al nome host del server** *nx_dns_srv_hostname_ptr 4 byte

Quattro record SRV vengono archiviati nel buffer fornito. Ogni NX_DNS_SRV_ENTRY record contiene un puntatore, *nx_dns_srv_hostname_ptr*, che punta alla stringa del nome host corrispondente nella parte inferiore del buffer dei record:

![Quattro record SRV](media/image7.png)

Se il *record_buffer* di input non può contenere tutti i dati SRV nella risposta del server, il *record_buffer* contiene il numero di record che si adatterà e restituisce il numero di record nel buffer.

Con il numero di record SRV restituiti in **record_count,* l'applicazione può analizzare i parametri SRV, incluso il nome host del server di ogni record *nel record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **host_name** Puntatore al nome host per ottenere i dati SRV per
- **record_buffer** Puntatore alla posizione in cui estrarre i dati SRV
- **buffer_size** Dimensioni del buffer per contenere i dati SRV
- **record_count** Puntatore al numero di record SRV recuperati
- **wait_option** Opzione di attesa per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) I dati SRV sono stati ottenuti correttamente
- **NX_DNS_NO_SERVER** (0xA1) L'elenco del server client è vuoto
- **NX_DNS_QUERY_FAILED** (0xA3) Nessuna risposta DNS valida ricevuta
- NX_DNS_PARAM_ERROR (0xA8) Parametro non puntatore non valido.
- NX_PTR_ERROR (0x07) Puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Restituire le dimensioni dell'elenco di server del client DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_get_serverlist_size (NX_DNS *dns_ptr, UINT *size);
```
### <a name="description"></a>Descrizione

Questo servizio restituisce il numero di server DNS validi (sia IPv4 che IPv6) nell'elenco Client.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS  
- **size** Restituisce il numero di server nell'elenco

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Le dimensioni dell'elenco di server DNS sono state restituite correttamente
- NX_PTR_ERROR (0x07) Puntatore IP o DNS non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio restituisce l'INDIRIZZO IP del server e la porta (record del servizio) in base al nome host di input in base alla query DNS. Se non viene trovato un record del servizio, questa routine restituisce un indirizzo IP zero nel puntatore all'indirizzo di input e uno stato di errore diverso da zero restituisce per segnalare un errore.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS  
- **host_name** Puntatore al buffer dei nomi host
- **host_address_ptr** Puntatore all'indirizzo da restituire
- **host_port_ptr** Puntatore alla porta da restituire
- **wait_option** Opzione di attesa per la risposta DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) record del server DNS restituito correttamente
- **NX_DNS_NO_SERVER** (0xA1) Nessun server DNS registrato con il client per inviare query sul nome host
- **NX_DNS_QUERY_FAILED** query DNS (0xA3) non riuscita. Nessuna risposta da alcun server DNS nell'elenco client o nessun record del servizio è disponibile per il nome host di input.
- NX_PTR_ERROR (0x07) Puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido

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

Questo servizio invia una query di tipo A con il nome host specificato per ottenere gli indirizzi IP per il nome host di input. Il client DNS copia l'indirizzo IPv4 dai record A restituiti nella risposta del server DNS nel percorso record_buffer *memoria.*

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

Più indirizzi IPv4 vengono archiviati nel buffer allineato a 4 byte, come illustrato di seguito:

![buffer con più indirizzi allineati a 4 byte](media/image8.png)

Se il buffer fornito non può contenere tutti i dati dell'indirizzo IP, i record A rimanenti non vengono archiviati in *record_buffer*. In questo modo l'applicazione può recuperare uno, alcuni o tutti i dati degli indirizzi IP disponibili nella risposta del server.

Con il numero di record A restituiti in **record_count'applicazione* può analizzare i dati dell'indirizzo IPv4 *dal* record_buffer .

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **host_name_ptr** Puntatore al nome host per ottenere l'indirizzo IPv4
- **buffer** Puntatore alla posizione in cui estrarre i dati IPv4
- **buffer_size** Dimensioni del buffer per contenere i dati IPv4
- **wait_option** Opzione di attesa per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) I dati IPv4 sono stati ottenuti correttamente
- **NX_DNS_NO_SERVER** (0xA1) L'elenco del server client è vuoto
- **NX_DNS_QUERY_FAILED** (0xA3) Nessuna risposta DNS valida ricevuta
- NX_PTR_ERROR (0x07) Puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) Parametro non puntatore non valido.

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

Questo servizio invia una query di tipo AAAA con il nome di dominio specificato per ottenere gli indirizzi IP per il nome di dominio di input. Il client DNS copia l'indirizzo IPv6 dai record AAAA restituiti nella risposta del server DNS nel percorso record_buffer *memoria.* 

> [!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

Il formato degli indirizzi IPv6 archiviati nel buffer allineato a 4 byte è illustrato di seguito:

![Buffer allineato a 4 byte in formato IPv6](media/image9.png)

Se il record_buffer di *input* non può contenere tutti i dati AAAA nella risposta del server, il *record_buffer* contiene tutti i record che saranno adatti e restituisce il numero di record nel buffer.

Con il numero di record AAAA restituiti in **record_count,* l'applicazione può analizzare gli indirizzi IPv6 da ogni record nel *record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **host_name_ptr** Puntatore al nome host per ottenere l'indirizzo IPv6
- **buffer** Puntatore alla posizione in cui estrarre i dati IPv6
- **buffer_size** Dimensioni del buffer per contenere i dati IPv6
- **wait_option** Opzione di attesa per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) I dati IPv6 sono stati ottenuti correttamente
- **NX_DNS_NO_SERVER** (0xA1) L'elenco del server client è vuoto
- **NX_DNS_QUERY_FAILED** (0xA3) Nessuna risposta DNS valida ricevuta
- NX_PTR_ERROR (0x07) Puntatore IP o DNS non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) Parametro non puntatore non valido.

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

Cercare un nome host da un indirizzo IP

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_host_by_address_get(NX_DNS *dns_ptr, ULONG ip_address, 
                                ULONG *host_name_ptr, 
                                ULONG max_host_name_size, 
                                ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio richiede la risoluzione dei nomi dell'indirizzo IP fornito da uno o più server DNS specificati in precedenza dall'applicazione. In caso di esito positivo, il nome host con terminazione NULL viene restituito nella stringa specificata da *host_name_ptr*. Si tratta di una funzione wrapper *per nxd_dns_host_by_address_get* e non accetta indirizzi IPv6.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore all'istanza DNS creata in precedenza.
- **ip_address** Indirizzo IP da risolvere in un nome
- **host_name_ptr** Puntatore all'area di destinazione per il nome host
- **max_host_name_size** Dimensioni dell'area di destinazione per il nome host
- **wait_option** Definisce per quanto tempo il servizio attenderà nei tick timer una risposta del server DNS dopo ogni query DNS e ogni nuovo tentativo di query. Le opzioni di attesa sono definite nel modo seguente:

  valore di timeout (0x00000001-0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)

  Selezionando TX_WAIT_FOREVER il thread chiamante viene sospeso a tempo indeterminato fino a quando un server DNS non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risoluzione DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Risoluzione DNS riuscita  
- **NX_DNS_TIMEOUT** timeout (0xA2) per ottenere il mutex DNS
- **NX_DNS_NO_SERVER** (0xA1) Nessun indirizzo del server DNS specificato
- **NX_DNS_QUERY_FAILED** (0xA3) Non ha ricevuto alcuna risposta alla query
- **NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Indirizzo di input Null
- **NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) L'indice punta a un tipo di indirizzo non valido ,ad esempio IPv6
- **NX_DNS_PARAM_ERROR** (0xA8) Input non puntatore non valido
- **NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Impossibile elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) Input puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio richiede la risoluzione dei nomi dell'indirizzo IPv6 o IPv4 nell'argomento di input *ip_address* da uno o più server DNS specificati in precedenza dall'applicazione. Se ha esito positivo, il nome host con terminazione NULL viene restituito nella stringa specificata da *host_name_ptr*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore a un'istanza DNS creata in precedenza.
- **ip_address** Indirizzo IP da risolvere in un nome
- **host_name_ptr** Puntatore all'area di destinazione per il nome host
- **max_host_name_size** Dimensioni dell'area di destinazione per il nome host
- **wait_option** Definisce il tempo di attesa del servizio in tick timer per una risposta del server DNS dopo ogni query DNS e ogni nuovo tentativo di query. Le opzioni di attesa sono definite come segue:

  valore di timeout (da 0x00000001 a 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)  

  Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando un server DNS non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa della risoluzione DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Risoluzione DNS riuscita  
- **NX_DNS_TIMEOUT** (0xA2) timeout durante il recupero del mutex DNS
- **NX_DNS_NO_SERVER** (0xA1) Nessun indirizzo server DNS specificato
- **NX_DNS_QUERY_FAILED** (0xA3) Non è stata ricevuta alcuna risposta alla query
- **NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Di input Null
- **NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Impossibile elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) Puntatore DNS o IP non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) Input non puntatore non valido

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

Questo servizio richiede la risoluzione dei nomi del nome fornito da uno o più server DNS specificati in precedenza dall'applicazione. Se ha esito positivo, l'indirizzo IP associato viene restituito nella destinazione a cui punta host_address_ptr. Si tratta di una funzione wrapper per *il nxd_dns_host_by_name_get* ed è limitata all'input di indirizzi IPv4.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore a un'istanza DNS creata in precedenza.
- **host_name** Puntatore al nome host
- **host_address_ptr** Indirizzo IP del server DNS restituito
- **wait_option** Definisce per quanto tempo il servizio attenderà la risoluzione DNS. Le opzioni di attesa sono definite come segue:

  valore di timeout (da 0x00000001 a 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)

  Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando un server DNS non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa della risoluzione DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Risoluzione DNS riuscita.
- **NX_DNS_NO_SERVER** (0xA1) Nessun indirizzo server DNS specificato
- **NX_DNS_QUERY_FAILED** (0xA3) Non è stata ricevuta alcuna risposta alla query
- NX_DNS_PARAM_ERROR (0xA8) Input non puntatore non valido
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Cercare un indirizzo IP dal nome host

### <a name="prototype"></a>Prototipo
```C
UINT nxd_dns_host_by_name_get(NX_DNS *dns_ptr, ULONG *host_name, 
                              NXD_ADDRESS *host_address_ptr, 
                              ULONG wait_option, UINT lookup_type);
```

### <a name="description"></a>Descrizione

Questo servizio richiede la risoluzione dei nomi dell'indirizzo IP fornito da uno o più server DNS specificati in precedenza dall'applicazione. Se ha esito positivo, l'indirizzo IP associato viene restituito in un NXD_ADDRESS a cui punta *host_address_ptr*. Se il chiamante imposta specificamente l'input lookup_type su NX_IP_VERSION_V6, questo servizio invierà una query per un indirizzo IPv6 host (record AAAA). Se il chiamante imposta in modo specifico lookup_type'input NX_IP_VERSION_V4, questo servizio invierà una query per un indirizzo IPv4 host (record A).

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore all'istanza del client DNS creata in precedenza.
- **host_name** Puntatore al nome host di cui trovare l'indirizzo IP
- **host_address_ptr** Puntatore alla destinazione per NXD_ADDRESS contenente l'indirizzo IP
- **wait_option** Definisce il tempo di attesa del servizio in tick timer per la risposta del server DNS per ogni trasmissione e ritrasmissione delle query. Le opzioni di attesa sono definite come segue:

  valore di timeout (da 0x00000001 a 0xFFFFFFFE) TX_WAIT_FOREVER (0xFFFFFFFF)  

  Selezionando TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo illimitato fino a quando un server DNS non risponde alla richiesta.

  La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick del timer che rimangono sospesi durante l'attesa della risoluzione DNS.

- **lookup_type** Indicare il tipo di ricerca (A e AAAA).

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Risoluzione DNS riuscita.
- **NX_DNS_NO_SERVER** (0xA1) Nessun indirizzo server DNS specificato
- **NX_DNS_QUERY_FAILED** (0xA3) Non è stata ricevuta alcuna risposta alla query
- **NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Di input Null
- **NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Impossibile elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) Input non puntatore non valido

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

Di seguito è riportato un altro esempio di uso di questo servizio ora, questa volta con indirizzi IPv4 e tipi di record A:
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

Cercare la stringa di testo per il nome di dominio di input

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_host_text_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                          UCHAR *record_buffer, 
                          UINT buffer_size, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia una query di tipo TXT con il nome di dominio e il buffer specificati per ottenere i dati di stringa arbitrari.

Il client DNS copia la stringa di testo nel record TXT nella risposta del server DNS nel percorso *record_buffer* memoria. 

> [!NOTE]
> Il record_buffer deve essere allineato a 4 byte per ricevere i dati.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al client DNS.  
- **host_name** Puntatore al nome dell'host in cui eseguire la ricerca
- **record_buffer** Puntatore alla posizione in cui estrarre i dati TXT
- **buffer_size** Dimensioni del buffer per contenere i dati TXT
- **wait_option** Opzione Wait per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Stringa TXT ottenuta correttamente
- **NX_DNS_NO_SERVER** server client (0xA1) è vuoto
- **NX_DNS_QUERY_FAILED** (0xA3) Nessuna risposta DNS valida ricevuta
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR (0xA8) Input non puntatore non valido

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

Impostare il pool di pacchetti del client DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_packet_pool_set(NX_DNS *dns_ptr, NX_PACKET_POOL *pool_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio imposta un pool di pacchetti creato in precedenza come pool di pacchetti del client DNS. Il client DNS userà questo pool di pacchetti per inviare query DNS, quindi il payload del pacchetto non deve essere minore di NX_DNS_PACKET_PAYLOAD che include le intestazioni Ethernet, IP e UDP ed è definito in *nxd_dns.h.* 

> [!NOTE]
> *Se* il client DNS viene eliminato, il pool di pacchetti non viene eliminato con esso ed è responsabilità dell'applicazione eliminare il pool di pacchetti quando non è più necessario.
>
> Questo servizio è disponibile solo se l'opzione di NX_DNS_CLIENT_USER_CREATE_PACKET_POOL è definita in *nxd_dns.h*

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore all'istanza del client DNS creata in precedenza.
- **pool_ptr** Puntatore al pool di pacchetti creato in precedenza

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Completamento riuscito.
- **NX_NOT_ENABLED** client (0x14) non configurato per questa opzione
- NX_PTR_ERROR (0x07) Puntatore ip o client DNS non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio.

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

Aggiungere l'indirizzo IP del server DNS

### <a name="prototype"></a>Prototipo
```C
UINT nx_dns_server_add(NX_DNS *dns_ptr, ULONG server_address);
```
### <a name="description"></a>Descrizione

Questo servizio aggiunge un server DNS IPv4 all'elenco di server.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.  
- **server_address** Indirizzo IP del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** server (0x00) aggiunto correttamente
- **NX_DNS_DUPLICATE_ENTRY**  
**NX_NO_MORE_ENTRIES** (0x17) Nessun altro server DNS consentito (l'elenco è pieno)
- **NX_DNS_PARAM_ERROR** (0xA8) Input non puntatore non valido
- **NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Impossibile elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio
- NX_DNS_BAD_ADDRESS_ERROR (0xA4) Input dell'indirizzo del server Null

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

Questo servizio aggiunge l'indirizzo IP di un server DNS all'elenco di server client DNS. Il server_address può essere un indirizzo IPv4 o IPv6. Se il client vuole poter accedere allo stesso server tramite il relativo indirizzo IPv4 o IPv6, deve aggiungere entrambi gli indirizzi IP come voci all'elenco dei server.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.
- **server_address** Puntatore al NXD_ADDRESS contenente l'indirizzo IP del server DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** server (0x00) aggiunto correttamente
- **NX_DNS_DUPLICATE_ENTRY**  
**NX_NO_MORE_ENTRIES** (0x17) Nessun altro server DNS consentito (l'elenco è pieno) 
- **NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Impossibile elaborare il record con IPv6 disabilitato
- **NX_DNS_PARAM_ERROR** (0xA8) Input non puntatore non valido
- NX_PTR_ERROR (0x07) Input del puntatore non valido
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio
- NX_DNS_BAD_ADDRESS_ERROR (0xA4) Input dell'indirizzo del server Null
- NX_DNS_INVALID_ADDRESS_TYPE (0xB2) l'indice punta a un tipo di indirizzo non valido,ad esempio IPv6

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

Questo servizio restituisce l'indirizzo del server DNS IPv4 dall'elenco di server in corrispondenza dell'indice specificato. 

> [!NOTE]
> L'indice è in base zero. Se l'indice di input supera le dimensioni dell'elenco client DNS, viene trovato un indirizzo IPv6 in tale indice o viene trovato un indirizzo Null in corrispondenza dell'indice specificato, viene restituito un errore. Il *nx_dns_get_serverlist_size* può essere chiamato prima ottenere il numero di server DNS nell'elenco Client.

Questo servizio supporta solo indirizzi IPv4. Chiama il servizio *nxd_dns_server_get* che supporta indirizzi IPv4 e IPv6.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS  
- **index** Indicizzare l'elenco di server del client DNS
- **dns_server_address** Puntatore all'indirizzo IP del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Server riuscito restituito
- **NX_DNS_SERVER_NOT_FOUND** (0xA9) l'indice punta a uno slot vuoto
- **NX_DNS_BAD_ADDRESS_ERROR** (0xA4) L'indice punta all'indirizzo Null
- **NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) l'indice punta a un tipo di indirizzo non valido ,ad esempio IPv6
- **NX_DNS_PARAM_ERROR** (0xA8) Input non puntatore non valido
- NX_PTR_ERROR (0x07) Ip o puntatore DNS non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio restituisce l'indirizzo IP del server DNS dall'elenco di server in corrispondenza dell'indice specificato. 

> [!NOTE]
> L'indice è in base zero. Se l'indice di input supera le dimensioni dell'elenco client DNS o viene trovato un indirizzo Null in corrispondenza dell'indice specificato, viene restituito un errore. Il *nx_dns_get_serverlist_size* può essere chiamato per primo per ottenere il numero di server DNS nell'elenco dei server.

Questo servizio supporta gli indirizzi IPv4 e IPv6.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS  
- **index** Indicizzare l'elenco di server del client DNS
- **dns_server_address** Puntatore all'indirizzo IP del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) Ha restituito correttamente l'indirizzo IP del server
- **NX_DNS_SERVER_NOT_FOUND** (0xA9) l'indice punta a uno slot vuoto
- **NX_DNS_BAD_ADDRESS_ERROR** (0xA4) L'indice punta all'indirizzo del server Null
- **NX_DNS_INVALID_ADDRESS_TYPE** (0xB2) l'indice punta a un tipo di indirizzo non valido ,ad esempio IPv6
- **NX_DNS_PARAM_ERROR** (0xA8) Input non puntatore non valido
- NX_PTR_ERROR (0x07) Ip o puntatore DNS non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio rimuove un server DNS IPv4 dall'elenco Client. Si tratta di una funzione wrapper per *nxd_dns_server_remove*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.
- **server_address** Indirizzo IP del server DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** server DNS (0x00) rimosso correttamente
- **NX_DNS_SERVER_NOT_FOUND** server (0xA9) non in elenco client
- **NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Input dell'indirizzo del server Null
- **NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Impossibile elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) Ip o puntatore DNS non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

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

Questo servizio rimuove un server DNS dell'indirizzo IP specificato dall'elenco Client. L'indirizzo IP di input accetta sia indirizzi IPv4 che indirizzi IPv6. Dopo la rimozione del server, i server rimanenti si spostano di un indice verso il basso nell'elenco per riempire lo slot vuoto.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.
- **server_address** Puntatore al server DNS che NXD_ADDRESS dati contenenti l'indirizzo IP del server.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** server DNS (0x00) rimosso correttamente
- **NX_DNS_SERVER_NOT_FOUND** server (0xA9) non in elenco client
- **NX_DNS_BAD_ADDRESS_ERROR** (0xA4) Input dell'indirizzo del server Null
- **NX_DNS_IPV6_NOT_SUPPORTED** (0xB3) Impossibile elaborare il record con IPv6 disabilitato
- NX_PTR_ERROR (0x07) Ip o puntatore DNS non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio
- NX_DNS_INVALID_ADDRESS_TYPE (0xB2) l'indice punta a un tipo di indirizzo non valido,ad esempio IPv6

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

Questo servizio rimuove tutti i server DNS dall'elenco Client.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr** Puntatore al blocco di controllo DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS** (0x00) SERVER DNS rimossi correttamente
- **NX_DNS_ERROR** (0xA0) Impossibile ottenere il mutex di protezione
- NX_PTR_ERROR (0x07) Ip o puntatore DNS non valido.
- NX_CALLER_ERROR (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```C
/* Remove all DNS Servers from the Client list. */
status =  nx_dns_server_remove_all(&my_dns);

/* If status is NX_SUCCESS all DNS Servers were successfully removed. */
```