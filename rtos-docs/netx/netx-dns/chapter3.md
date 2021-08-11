---
title: Capitolo 3 - Descrizione dei Azure RTOS client DNS NetX
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS DNS NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 922d41dc374ccd782809404776f18f2aed8f5e3c34b7c9e143075c0ee5567220
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782491"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dns-client-services"></a>Capitolo 3 - Descrizione dei Azure RTOS client DNS NetX

Questo capitolo contiene una descrizione di tutti i Azure RTOS DNS NetX (elencati di seguito) in ordine alfabetico.

Nella sezione "Valori restituiti" nelle descrizioni api seguenti i valori in **grassetto** non sono interessati dalla definizione **NX_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.

- **nx_dns_authority_zone_start_get**: *cercare l'inizio di una zona di autorità associata al nome host specificato*
- **nx_dns_cache_initialize**: *inizializzare una cache DNS.*
- **nx_dns_cache_notify_clear**: *cancella la funzione di notifica completa della cache.*
- **nx_dns_cache_notify_set:** impostare *la funzione di notifica completa della cache.*
- **nx_dns_cname_get**: *cercare il nome di dominio canonico per l'alias del nome di dominio di input*
- **nx_dns_create:** Creare *un'istanza del client DNS*
- **nx_dns_delete:** Eliminare *un'istanza del client DNS*
- **nx_dns_domain_name_server_get**: *Cercare i server dei nomi autorevoli per la zona del dominio di input*
- **nx_dns_domain_mail_exchange_get**: *cercare lo scambio di posta associato al nome host specificato.*
- **nx_dns_domain_service_get**: *cercare i servizi* associati al nome host specificato
- **nx_dns_get_serverlist_size**: *restituisce le dimensioni dell'elenco di server client DNS*
- **nx_dns_info_by_name_get:** indirizzo *IP mittente, esecuzione di query sulle porte sul nome host di input*
- **nx_dns_ipv4_address_by_name_get**: *cercare l'indirizzo IPv4 dal nome host specificato*
- **nx_dns_host_by_address_get:** cercare *un nome host da un indirizzo IP specificato*
- **nx_dns_host_by_name_get**: *cercare l'indirizzo IPv4 dal nome host specificato*
- **nx_dns_host_text_get**: *Cercare i dati di testo per il nome di dominio di input*
- **nx_dns_packet_pool_set**: *Impostare il pool di pacchetti del client DNS*
- **nx_dns_server_add**: *aggiungere un server DNS all'indirizzo specificato all'elenco client*
- **nx_dns_server_get**: *Restituisce il server DNS nell'elenco client*
- **nx_dns_server_remove**: *Rimuovere un server DNS dall'elenco client*
- **nx_dns_server_remove_all**: *Rimuovere tutti i server DNS dall'elenco client*

## <a name="nx_dns_authority_zone_start_get"></a>nx_dns_authority_zone_start_get

Cercare l'inizio della zona di autorità per l'host di input

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_authority_zone_start_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                      VOID *record_buffer,
                                      UINT buffer_size, 
                                      UINT *record_count, 
                                      ULONG wait_option);

```

### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, questo servizio invia una query di tipo SOA con il nome di dominio specificato per ottenere l'inizio della zona di autorità per il nome di dominio di input. Il client DNS copia i record SOA restituiti nella risposta del server DNS nel percorso *record_buffer* memoria. 
>[!NOTE]
> Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

In NetX DNS Client il tipo di record SOA, NX_DNS_SOA_ENTRY, viene salvato come sette parametri di 4 byte, per un totale di 28 byte:

- **nx_dns_soa_host_mname_ptr:** Puntatore all'origine dati primaria per questa zona
- **nx_dns_soa_host_rname_ptr:** puntatore alla cassetta postale responsabile di questa zona
- **nx_dns_soa_serial:** Numero di versione della zona
- **nx_dns_soa_refresh:** Intervallo di aggiornamento
- **nx_dns_soa_retry:** Intervallo tra i tentativi di query SOA
- **nx_dns_soa_expire:** durata della scadenza soa
- **nx_dns_soa_minmum:** Campo TTL minimo nei messaggi di risposta DNS del nome host SOA

L'archiviazione di due record SOA è illustrata di seguito. I record SOA contenenti dati a lunghezza fissa vengono immessi a partire dall'inizio del buffer. I puntatori MNAME e RNAME puntano ai dati a lunghezza variabile (nomi host) archiviati nella parte inferiore del buffer. I record SOA aggiuntivi vengono immessi dopo il primo record ("record SOA aggiuntivi...") e i relativi dati di lunghezza variabile vengono archiviati sopra i dati di lunghezza variabile dell'ultima voce ("dati aggiuntivi di lunghezza variabile SOA"):

![Diagramma che rappresenta l'archiviazione di due record S O A](media/image2.png)

Se il *record_buffer* di input non può contenere tutti i dati SOA nella risposta del server, il *record_buffer* contiene il numero di record che rientra e restituisce il numero di record nel buffer.

Con il numero di record SOA restituiti in **record_count,* l'applicazione può analizzare i dati da *record_buffer* ed estrarre l'inizio delle stringhe del nome host dell'autorità di zona.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al client DNS.  
- **host_name:** puntatore al nome host per ottenere i dati SOA per
- **record_buffer:** puntatore alla posizione in cui estrarre i dati SOA
- **buffer_size**: Dimensioni del buffer per contenere i dati SOA
- **record_count:** puntatore al numero di record SOA recuperati
- **wait_option:** Opzione Wait per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) I dati SOA sono stati ottenuti correttamente
- **NX_DNS_NO_SERVER:**(0xA1) L'elenco dei server client è vuoto
- **NX_DNS_QUERY_FAILED:**(0xA3) Nessuna risposta DNS valida ricevuta
- NX_PTR_ERROR: (0x07) Puntatore DNS o IP non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR: (0xA8) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```c
UCHAR                  record_buffer[50];
UINT                   record_count;   
NX_DNS_SOA_ENTRY       *nx_dns_soa_entry_ptr;

/* Request the start of authority zone(s) for the specified host.  */
status =  nx_dns_authority_zone_start_get(&client_dns, (UCHAR *)"www.my_example.com",
                                          record _buffer, sizeof(record_buffer), 
                                          &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else 
{
/* If status is NX_SUCCESS a DNS query was successfully completed and SOA data is returned in soa_buffer.  */

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

```

```Output
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

```c
UINT nx_dns_cache_initialize(NX_DNS *dns_ptr,
                             VOID *cache_ptr, UINT cache_size);

```
### <a name="description"></a>Descrizione

Questo servizio crea e inizializza una cache DNS.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al blocco di controllo DNS.
- **cache_ptr:** puntatore alla cache DNS.
- **cache_size:** dimensioni della cache DNS, in byte.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) DNS Cache successfully initialized (Cache DNS inizializzata correttamente)
- NX_DNS_ERROR: (0xA0) La cache non è allineata a 4 byte.
- NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.
- NX_PTR_ERROR: (0x07) Puntatore DNS non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```c
UCHAR          dns_cache [2048]; 

/* Initialize the DNS Cache.  */
status =  nx_dns_cache_initialize(&my_dns, dns_cache, 2048);
/* If status is NX_SUCCESS DNS Cache was successfully initialized.  */
```

## <a name="nx_dns_cache_notify_clear"></a>nx_dns_cache_notify_clear

Cancellare la funzione di notifica completa della cache DNS

### <a name="prototype"></a>Prototipo

```c
UINT     nx_dns_cache_notify_clear(NX_DNS *dns_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio cancella la funzione di notifica completa della cache.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al blocco di controllo DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** notifica della cache DNS (0x00) impostata correttamente
- NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.
- NX_PTR_ERROR: (0x07) Puntatore DNS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Clear the DNS Cache full notify function.  */
status =  nx_dns_cache_notify_clear(&my_dns);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully cleared. */
```

## <a name="nx_dns_cache_notify_set"></a>nx_dns_cache_notify_set

Impostare la funzione di notifica completa della cache DNS

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_cache_notify_set(NX_DNS *dns_ptr, VOID (*cache_full_notify_cb)(NX_DNS *dns_ptr));
```

### <a name="description"></a>Descrizione

Questo servizio imposta la funzione di notifica completa della cache.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al blocco di controllo DNS.
- **cache_full_notify_cb:** funzione di callback da richiamare quando la cache diventa piena.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** notifica della cache DNS (0x00) impostata correttamente
- NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.
- NX_PTR_ERROR: (0x07) Puntatore DNS non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Set the DNS Cache full notify function.  */
status =  nx_dns_cache_notify_set(&my_dns, cache_full_notify_cb);

/* If status is NX_SUCCESS DNS Cache full notify function was successfully set.  */
 
```

## <a name="nx_dns_cname_get"></a>nx_dns_cname_get

Cercare il nome canonico per il nome host di input

### <a name="prototype"></a>Prototipo
```c
UINT nx_dns_cname_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                      UCHAR *record_buffer, UINT buffer_size, 
                      ULONG wait_option);
```

### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito in *nx_dns.h,* questo servizio invia una query di tipo CNAME con il nome di dominio specificato per ottenere il nome di dominio canonico. Il client DNS copia la stringa CNAME restituita nella risposta del server DNS nel percorso *record_buffer* memoria.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al client DNS.  
- **host_name:** Puntatore al nome host per cui ottenere i dati CNAME
- **record_buffer:** Puntatore alla posizione in cui estrarre i dati CNAME
- **buffer_size**: Dimensioni del buffer per contenere i dati CNAME
- **wait_option:** Opzione Wait per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) I dati CNAME sono stati ottenuti correttamente
- **NX_DNS_NO_SERVER:**(0xA1) L'elenco dei server client è vuoto
- **NX_DNS_QUERY_FAILED:**(0xA3) Nessuna risposta DNS valida ricevuta
- NX_PTR_ERROR: (0x07) Puntatore DNS o IP non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR: (0xA8) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
CHAR            record _buffer[50];

/* Request the canonical name for the specified host.  */
status =  nx_dns_cname_get(&client_dns, (UCHAR *)"www.my_example.com ", 
                            record_buffer, sizeof(record_buffer), 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and the canonical host name is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test CNAME: %s\n", record_buffer);
} 
```

```Output
Test CNAME: **my_example**.com
```

## <a name="nx_dns_create"></a>nx_dns_create

Creare un'istanza del client DNS

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_create(NX_DNS *dns_ptr, NX_IP *ip_ptr, CHAR *domain_name);
```

### <a name="description"></a>Descrizione

Questo servizio crea un'istanza del client DNS per l'istanza IP creata in precedenza.

>[!NOTE]
>L'applicazione deve garantire che il payload dei pacchetti del pool di pacchetti usato dal client DNS sia sufficientemente grande per il messaggio DNS di 512 byte massimo, oltre alle intestazioni UDP, IP ed Ethernet. Se il client DNS crea il proprio pool di pacchetti, questo viene definito da NX_DNS_PACKET_POOL_SIZE e NX_DNS_PACKET_PAYLOAD. Se l'applicazione client DNS preferisce fornire un pool di pacchetti creato in precedenza, il payload per il client DNS IPv4 deve essere di 512 byte per il DNS massimo più 20 byte per l'intestazione IP, 8 byte per l'intestazione UDP e 14 byte per l'intestazione Ethernet.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al client DNS.  
- **ip_ptr:** puntatore a un'istanza IP creata in precedenza.  
- **domain_name:** puntatore al nome di dominio per l'istanza DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Creazione DNS riuscita
- **NX_DNS_ERROR:**(0xA0) Errore di creazione DNS
- NX_PTR_ERROR: (0x07) Puntatore DNS o IP non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Create a DNS Client instance.  */
status =  nx_dns_create(&my_dns, &my_ip, "My DNS");

/* If status is NX_SUCCESS a DNS Client instance was successfully
   created.  */
```
## <a name="nx_dns_delete"></a>nx_dns_delete

Eliminare un'istanza del client DNS

### <a name="prototype"></a>Prototipo

```c
UINT     nx_dns_delete(NX_DNS *dns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio elimina un'istanza del client DNS creata in precedenza e libera le relative risorse. 
>[!NOTE]
> Se **NX_DNS_CLIENT_USER_CREATE_PACKET_POOL** è definito e al client DNS è stato assegnato un pool di pacchetti definito dall'utente, è responsabilità dell'applicazione eliminare il pool di pacchetti del client DNS se non è più necessario.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr**: puntatore all'istanza del client DNS **creata in precedenza.**

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Eliminazione del client DNS riuscita.
- NX_PTR_ERROR: (0x07) Ip o puntatore client DNS non valido.
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Delete a DNS Client instance.  */
status =  nx_dns_delete(&my_dns);

/* If status is NX_SUCCESS the DNS Client instance was successfully
   deleted.  */
```
## <a name="nx_dns_domain_name_server_get"></a>nx_dns_domain_name_server_get

Cercare i server dei nomi autorevoli per la zona del dominio di input

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_domain_name_server_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                   VOID *record_buffer, UINT buffer_size, 
                                   UINT *record_count, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, questo servizio invia una query di tipo NS con il nome di dominio specificato per ottenere i server dei nomi per il nome di dominio di input. Il client DNS copia i record NS restituiti nella risposta del server DNS nel percorso *record_buffer* memoria. 

>[!NOTE]
>Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

Nel client DNS NetX il tipo di dati NS, NX_DNS_NS_ENTRY, viene salvato come due parametri a 4 byte:

- **nx_dns_ns_ipv4_address:** Indirizzo IPv4 del server dei nomi
- **nx_dns_ns_hostname_ptr:** puntatore al nome host del server dei nomi

Il buffer illustrato di seguito contiene quattro NX_DNS_NS_ENTRY record. Il puntatore alla stringa del nome host in ogni voce punta alla stringa del nome host corrispondente nella metà inferiore del buffer:

![Diagramma del buffer che contiene quattro record di immissione N X D N S S S.](media/image3.png)

Se il *record_buffer* di input non può contenere tutti i dati NS nella risposta del server, il *record_buffer* contiene tutti i record che saranno adatti e restituisce il numero di record nel buffer.

Con il numero di record NS restituiti in **record_count,* l'applicazione può analizzare l'indirizzo IP e il nome host di ogni record *nel record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al client DNS.  
- **host_name:** Puntatore al nome host per ottenere i dati NS per
- **record_buffer:** Puntatore alla posizione in cui estrarre i dati NS
- **buffer_size**: Dimensioni del buffer per contenere i dati NS
- **record_count:** puntatore al numero di record NS recuperati
- **wait_option:** Opzione Wait per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Successfully obtained NS data
- **NX_DNS_NO_SERVER:**(0xA1) L'elenco dei server client è vuoto
- **NX_DNS_QUERY_FAILED:**(0xA3) Nessuna risposta DNS valida ricevuta
- NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.
- NX_PTR_ERROR: (0x07) Puntatore DNS o IP non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```c
#define RECORD_COUNT        10

ULONG                      record_buffer[50];
UINT                       record_count;          
NX_DNS_NS_ENTRY            *nx_dns_ns_entry_ptr[RECORD_COUNT];

/* Request the name server(s) for the specified host.  */
status =  nx_dns_domain_name_server_get(&client_dns, (UCHAR *)" www.my_example.com ",  
                                        record_buffer, sizeof(record_buffer),  
                                        &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and NS data is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test NS: ");
    printf("record_count = %d \n", record_count);      

    /* Get the name server.  */
    for(i =0; i< record_count; i++)
    {
        nx_dns_ns_entry_ptr[i] = (NX_DNS_NS_ENTRY *)(record_buffer + i * sizeof(NX_DNS_NS_ENTRY)); 

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
```

```Output
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

Cercare lo scambio di posta per il nome host di input

### <a name="prototype"></a>Prototipo
```c
UINT     nx_dns_domain_mail_exchange_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                                        VOID *record_buffer,                                        
                                        UINT buffer_size, 
                                        UINT *record_count, 
                                        ULONG wait_option);

```

### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES è definito, questo servizio invia una query di tipo MX con il nome di dominio specificato per ottenere lo scambio di posta per il nome di dominio di input. Il client DNS copia i record MX restituiti nella risposta del server DNS nel percorso *record_buffer* memoria.

>[!NOTE]
>Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

In NetX DNS Client il tipo di record di scambio della posta elettronica, NX_DNS_MAIL_EXCHANGE_ENTRY, viene salvato come quattro parametri, per un totale di 12 byte:

- **nx_dns_mx_ipv4_address:** indirizzo IPv4 scambio posta elettronica 4 byte
- **nx_dns_mx_preference:** Preferenza 2 byte
- **nx_dns_mx_reserved0:** 2 byte riservati
- **nx_dns_mx_hostname_ptr:** Puntatore al nome host del server di scambio di posta elettronica di 4 byte

Di seguito è riportato un buffer contenente quattro record MX. Ogni record contiene i dati a lunghezza fissa dell'elenco precedente. Il puntatore al nome host del server di scambio della posta punta al nome host corrispondente nella parte inferiore del buffer.

![Diagramma che mostra il buffer contenente quattro record M X.](media/image4.png)

Se il *record_buffer* di input non può contenere tutti i dati MX nella risposta del server, il *record_buffer* contiene il numero di record che rientra e restituisce il numero di record nel buffer.

Con il numero di record MX restituiti in **record_count,* l'applicazione può analizzare i parametri MX, incluso il nome host di posta di ogni record *nel record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al client DNS.  
- **host_name:** Puntatore al nome host per cui ottenere i dati MX
- **record_buffer:** Puntatore alla posizione in cui estrarre i dati MX
- **buffer_size**: Dimensioni del buffer per contenere i dati MX
- **record_count:** puntatore al numero di record MX recuperati
- **wait_option:** Opzione Wait per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Successfully obtained MX data
- **NX_DNS_NO_SERVER:**(0xA1) L'elenco dei server client è vuoto
- **NX_DNS_QUERY_FAILED:**(0xA3) Nessuna risposta DNS valida ricevuta
- NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.
- NX_PTR_ERROR: (0x07) Puntatore DNS o IP non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```c
#define           MAX_RECORD_COUNT 10

ULONG             record_buffer[50];
UINT              record_count;  
NX_DNS_MX_ENTRY  *nx_dns_mx_entry_ptr[MAX_RECORD_COUNT];        

/* Request the mail exchange data for the specified host.  */
status =  nx_dns_domain_mail_exchange_get(&client_dns, (UCHAR *)" www.my_example.com ", 
                                          record_buffer, sizeof(record_buffer),   
                                          &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}
       
else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and MX data is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test MX: ");
    printf("record_count = %d \n", record_count);      


    /* Get the mail exchange.  */
    for(i =0; i< record_count; i++)
    {
        nx_dns_mx_entry_ptr[i] = (NX_DNS_MX_ENTRY *)(record_buffer + i * sizeof(NX_DNS_MX_ENTRY));   

        printf("record %d: IP address: %d.%d.%d.%d\n", i, 
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 24,
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 16 & 0xFF,                   
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address >> 8 & 0xFF,
                nx_dns_mx_entry_ptr[i] -> nx_dns_mx_ipv4_address & 0xFF);

        printf("preference = %d \n ", nx_dns_mx_entry_ptr[i] -> nx_dns_mx_preference);

        if(nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr)
            printf("hostname = %s\n", nx_dns_mx_entry_ptr[i] -> nx_dns_mx_hostname_ptr);
        else
            printf("hostname is not set\n");
    }
}
```

```Output
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

```c
UINT nx_dns_domain_service_get (NX_DNS *dns_ptr, UCHAR *host_name, 
                                VOID *record_buffer, UINT buffer_size, 
                                UINT *record_count, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Se NX_DNS_ENABLE_EXTENDED_RR_TYPES definito, questo servizio invia una query di tipo SRV con il nome di dominio specificato per cercare i servizi e il relativo numero di porta associati al dominio specificato. Il client DNS copia i record SRV restituiti nella risposta del server DNS nel percorso *record_buffer* memoria. 

>[!NOTE]
>Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

In NetX DNS Client il tipo di record del servizio, NX_DNS_SRV_ ENTRY, viene salvato come sei parametri, per un totale di 16 byte. In questo modo i dati SRV a lunghezza variabile possono essere archiviati in modo efficiente in memoria:

- **Indirizzo IPv4 del server:** nx_dns_srv_ipv4_address 4 byte
- **Priorità server:** nx_dns_srv_priority 2 byte
- **Peso server:** nx_dns_srv_weight 2 byte
- **Numero di porta del** servizio: nx_dns_srv_port_number 2 byte
- **Riservato per l'allineamento a 4 byte:** nx_dns_srv_reserved0 2 byte
- **Puntatore al nome host del server:***nx_dns_srv_hostname_ptr 4 byte

Quattro record SRV vengono archiviati nel buffer fornito. Ogni NX_DNS_SRV_ENTRY record contiene un puntatore, *nx_dns_srv_hostname_ptr*, che punta alla stringa del nome host corrispondente nella parte inferiore del buffer del record:

![Diagramma di quattro record S R V archiviati nel buffer fornito.](media/image5.png)

Se il *record_buffer* di input non può contenere tutti i dati SRV nella risposta del server, il *record_buffer* contiene il numero di record che rientra e restituisce il numero di record nel buffer.

Con il numero di record SRV restituiti in **record_count,* l'applicazione può analizzare i parametri SRV, incluso il nome host del server di ogni record *nel record_buffer*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al client DNS.  
- **host_name:** Puntatore al nome host per ottenere i dati SRV per
- **record_buffer:** Puntatore alla posizione in cui estrarre i dati SRV
- **buffer_size:** Dimensioni del buffer per contenere i dati SRV
- **record_count:** puntatore al numero di record SRV recuperati
- **wait_option:** Opzione Wait per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) I dati SRV sono stati ottenuti correttamente
- **NX_DNS_NO_SERVER:**(0xA1) L'elenco dei server client è vuoto
- **NX_DNS_QUERY_FAILED:**(0xA3) Nessuna risposta DNS valida ricevuta
- NX_DNS_PARAM_ERROR: (0xA8) ID DNS non valido.
- NX_PTR_ERROR: (0x07) Puntatore DNS o IP non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
#define MAX_RECORD_COUNT  10

UCHAR                  record_buffer[50];
UINT                   record_count;
NX_DNS_SRV_ENTRY       *nx_dns_srv_entry_ptr[MAX_RECORD_COUNT];

/* Request the service(s) provided by the specified host.  */
status =  nx_dns_domain_service_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                    record_buffer, sizeof(record_buffer), 
                                    &record_count, 500);

/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
    error_counter++;
}

else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed and SRV data is returned in record_buffer.  */

    printf("------------------------------------------------------\n");
    printf("Test SRV: ");
    printf("record_count = %d \n", record_count);      

       
    /* Get the location of services.  */
    for(i =0; i< record_count; i++)
    {
        nx_dns_srv_entry_ptr[i] = (NX_DNS_SRV_ENTRY *)(record_buffer + i * sizeof(NX_DNS_SRV_ENTRY)); 

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
```

```Output
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

```c
UINT nx_dns_get_serverlist_size (NX_DNS *dns_ptr, UINT *size);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce il numero di server DNS validi nell'elenco Client.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** Puntatore al blocco di controllo DNS  
- **size**: restituisce il numero di server nell'elenco

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Le dimensioni dell'elenco di server DNS sono state restituite correttamente
- NX_PTR_ERROR: (0x07) Puntatore DNS o IP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
UINT my_listsize;

/* Get the number of non null DNS Servers in the Client list.  */
status =  nx_dns_get_serverlist_size (&my_dns, 5, &my_listsize);

/* If status is NX_SUCCESS the size of the DNS Server list was successfully
   returned.  */
```

## <a name="nx_dns_info_by_name_get"></a>nx_dns_info_by_name_get

Indirizzo IP restituito e porta del server DNS in base al nome host

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_info_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr,  
                             USHORT *host_port_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'INDIRIZZO IP del server e la porta (record del servizio) in base al nome host di input tramite query DNS. Se non viene trovato un record del servizio, questa routine restituisce un indirizzo IP zero nel puntatore dell'indirizzo di input e uno stato di errore diverso da zero restituisce per segnalare un errore.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** Puntatore al blocco di controllo DNS  
- **host_name:** Puntatore al buffer dei nomi host
- **host_address_ptr:** Puntatore all'indirizzo da restituire
- **host_port_ptr:** Puntatore alla porta per restituire wait_option'opzione Wait per la risposta DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Record del server DNS restituito correttamente
- **NX_DNS_NO_SERVER**: (0xA1) Nessun server DNS registrato con il client per inviare query sul nome host
- **NX_DNS_QUERY_FAILED:** query DNS (0xA3) non riuscita. Nessuna risposta da alcun server DNS nell'elenco client o nessun record del servizio è disponibile per il nome host di input.
- NX_PTR_ERROR: (0x07) Puntatore IP o DNS non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```c
ULONG         ip_address;
USHORT         port;

/* Attempt to resolve the IP address and ports for this host name.  */
status =  nx_dns_info_by_name_get(&my_dns, “www.abc1234.com”, &ip_address, &port, 200);

/* If status is NX_SUCCESS the DNS query was successful and the IP address and
   report for the hostname are returned.  */
```

## <a name="nx_dns_ipv4_address_by_name_get"></a>nx_dns_ipv4_address_by_name_get

Cercare l'indirizzo IPv4 per il nome host di input

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_ipv4_address_by_name_get (NX_DNS *dns_ptr, 
                                       UCHAR *host_name_ptr, VOID *buffer, 
                                       UINT buffer_size, 
                                       UINT *record_count,
                                       ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia una query di tipo A con il nome host specificato per ottenere gli indirizzi IP per il nome host di input. Il client DNS copia l'indirizzo IPv4 dai record A restituiti nella risposta del server DNS nel percorso record_buffer *memoria.* 

>[!NOTE]
>Il *record_buffer* deve essere allineato a 4 byte per ricevere i dati.

Più indirizzi IPv4 vengono archiviati nel buffer allineato a 4 byte, come illustrato di seguito:

![Diagramma di più indirizzi I P v 4 archiviati nel buffer allineato a 4 byte.](media/image6.png)

Se il buffer fornito non può contenere tutti i dati dell'indirizzo IP, i record A rimanenti non vengono archiviati in *record_buffer*. In questo modo l'applicazione può recuperare uno, alcuni o tutti i dati degli indirizzi IP disponibili nella risposta del server.

Con il numero di record A restituiti in **record_count'applicazione* può analizzare i dati dell'indirizzo IPv4 *dal* record_buffer .

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al client DNS.  
- **host_name_ptr:** puntatore al nome host per ottenere il buffer degli indirizzi IPv4 Puntatore alla posizione in cui estrarre i dati IPv4
- **buffer_size:** dimensioni del buffer per contenere i dati IPv4
- **wait_option**: opzione Wait per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) I dati IPv4 sono stati ottenuti correttamente
- **NX_DNS_NO_SERVER:**(0xA1) L'elenco del server client è vuoto
- **NX_DNS_QUERY_FAILED:**(0xA3) Nessuna risposta DNS valida ricevuta
- NX_DNS_PARAM_ERROR: (0xA8) Parametro di input non valido.
- NX_PTR_ERROR: (0x07) Puntatore IP o DNS non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
#define MAX_RECORD_COUNT  20

ULONG           record_buffer[50];
UINT            record_count;
ULONG           *ipv4_address_ptr[MAX_RECORD_COUNT];

/* Request the IPv4 address for the specified host.  */
status =  nx_dns_ipv4_address_by_name_get(&client_dns, 
                                          (UCHAR *)"www.my_example.com",  
                                           record_buffer,                  
                                           sizeof(record_buffer),&record_count,                
                                           500);

        /* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
        error_counter++;
}    
else     
{
    /* If status is NX_SUCCESS a DNS query was successfully completed the IPv4 address(es) is returned in record_buffer.  */
    printf("------------------------------------------------------\n");
    printf("Test A: ");
    printf("record_count = %d \n", record_count);      


    /* Get the IPv4 addresses of host.  */
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
```

```Output
------------------------------------------------------
Test A: record_count = 5 
record 0: IP address: 192.2.2.10
record 1: IP address: 192.2.2.11
record 2: IP address: 192.2.2.12
record 3: IP address: 192.2.2.13
record 4: IP address: 192.2.2.14
```

## <a name="nx_dns_host_by_address_get"></a>nx_dns_host_by_address_get

Cercare un nome host da un indirizzo IP

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_host_by_address_get(NX_DNS *dns_ptr, ULONG ip_address, 
                                ULONG *host_name_ptr, 
                                ULONG max_host_name_size, 
                                ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio richiede la risoluzione dei nomi dell'indirizzo IP fornito da uno o più server DNS specificati in precedenza dall'applicazione. In caso di esito positivo, il nome host con terminazione NULL viene restituito nella stringa specificata da *host_name_ptr*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore a un'istanza DNS creata in precedenza.
- **ip_address**: indirizzo IP da risolvere in un nome
- **host_name_ptr:** puntatore all'area di destinazione per il nome host
- **max_host_name_size:** dimensioni dell'area di destinazione per il nome host
- **wait_option**: definisce per quanto tempo il servizio attenderà nei tick timer una risposta del server DNS dopo ogni query DNS e ogni nuovo tentativo di query Le opzioni di attesa sono definite come segue:
    - **valore** di timeout : (0x00000001-0xFFFFFFFE) La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risoluzione DNS.
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando un server DNS non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Risoluzione DNS riuscita  
- **NX_DNS_TIMEOUT:** timeout (0xA2) per ottenere il mutex DNS
- **NX_DNS_NO_SERVER**: (0xA1) Nessun indirizzo del server DNS specificato
- **NX_DNS_QUERY_FAILED**: (0xA3) Non ha ricevuto alcuna risposta alla query
- **NX_DNS_BAD_ADDRESS_ERROR**: (0xA4) Indirizzo di input Null
- **NX_DNS_INVALID_ADDRESS_TYPE:**(0xB2) L'indice punta a un tipo di indirizzo non valido ,ad esempio IPv6
- **NX_DNS_PARAM_ERROR:**(0xA8) Input non puntatore non valido
- NX_PTR_ERROR: (0x07) Input puntatore non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
#define BUFFER_SIZE   200

UCHAR   resolved_name[200];

/* Get the name associated with IP address 192.2.2.10.  */
status =  nx_dns_host_by_address_get(&my_dns, IP_ADDRESS(192.2.2.10),
                                     &resolved_name[0], BUFFER_SIZE, 450);

/* If status is NX_SUCCESS the name associated with the IP address
   can be found in the resolved_name variable.  */

```

## <a name="nx_dns_host_by_name_get"></a>nx_dns_host_by_name_get

Cercare un indirizzo IP dal nome host

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_host_by_name_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                             ULONG *host_address_ptr, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio richiede la risoluzione dei nomi del nome fornito, a cui punta *host_name*, da uno o più server DNS specificati in precedenza dall'applicazione. In caso di esito positivo, l'indirizzo IP associato viene restituito nella destinazione a cui punta *host_address_ptr*.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore a un'istanza DNS creata in precedenza.
- **host_name:** puntatore al nome host
- **host_address_ptr:** Puntatore all'indirizzo IP dell'host DNS
- **wait_option**: definisce per quanto tempo il servizio attenderà la risoluzione DNS. Le opzioni di attesa sono definite nel modo seguente:
    - **valore timeout**: (0x00000001-0xFFFFFFFE) La selezione di un valore numerico (1-0xFFFFFFFE) specifica il numero massimo di tick timer da mantenere sospesi durante l'attesa della risoluzione DNS.
    - **TX_WAIT_FOREVER**: (0xFFFFFFFF) Se si seleziona TX_WAIT_FOREVER, il thread chiamante viene sospeso per un periodo indefinito fino a quando un server DNS non risponde alla richiesta.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Risoluzione DNS riuscita.
- **NX_DNS_NO_SERVER**: (0xA1) Nessun indirizzo del server DNS specificato
- **NX_DNS_QUERY_FAILED**: (0xA3) Non ha ricevuto alcuna risposta alla query
- NX_DNS_PARAM_ERROR: (0xA8) Input non puntatore non valido
- NX_PTR_ERROR: (0x07) Input puntatore non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```c
ULONG ip_address;

    /* Get the IP address for the name “www.my_example.com”.  */
    status =  nx_dns_host_by_name_get(&my_dns, “www.my_example.com”, &ip_address, 4000);

    /* Check for DNS query error.  */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    else     
    {

    /* If status is NX_SUCCESS the IP address for “www.my_example.com” can be found in the “ip_address” variable.  */
        
        printf("------------------------------------------------------\n");
        printf("Test A: \n");
        printf("IP address: %d.%d.%d.%d\n",
                host_ip_address >> 24,
                host_ip_address >> 16 & 0xFF,                   
                host_ip_address >> 8 & 0xFF,
                host_ip_address & 0xFF);
    }
```

```Output
Test A: 
IP address: 192.2.2.10
```

## <a name="nx_dns_host_text_get"></a>nx_dns_host_text_get

Cercare la stringa di testo per il nome di dominio di input

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_host_text_get(NX_DNS *dns_ptr, UCHAR *host_name, 
                          UCHAR *record_buffer, 
                          UINT buffer_size, ULONG wait_option);
```

### <a name="description"></a>Descrizione

Questo servizio invia una query di tipo TXT con il nome di dominio e il buffer specificati per ottenere i dati di stringa arbitrari.

Il client DNS copia la stringa di testo nel record TXT nella risposta del server DNS nel percorso record_buffer *memoria.* 

>[!NOTE]
>Il *record_buffer* non deve essere allineato a 4 byte per ricevere i dati.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al client DNS.  
- **host_name:** puntatore al nome dell'host in cui eseguire la ricerca
- **record_buffer:** puntatore al percorso in cui estrarre i dati TXT
- **buffer_size**: dimensioni del buffer per contenere i dati TXT
- **wait_option**: opzione Wait per ricevere la risposta del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Stringa TXT ottenuta correttamente
- **NX_DNS_NO_SERVER:**(0xA1) L'elenco dei server client è vuoto
- **NX_DNS_QUERY_FAILED:**(0xA3) Nessuna risposta DNS valida ricevuta
- NX_PTR_ERROR: (0x07) Input puntatore non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio
- NX_DNS_PARAM_ERROR: (0xA8) Input non puntatore non valido

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
CHAR            record_buffer[50];

/* Request the text string for the specified host.  */
status =  nx_dns_host_text_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                record_buffer, 
                                sizeof(record_buffer), 500);


/* Check for DNS query error.  */
if (status != NX_SUCCESS)
{
     error_counter++;
}
else     
{
/* If status is NX_SUCCESS a DNS query was successfully completed and the text string is returned in record_buffer.  */
 
     printf("------------------------------------------------------\n");
     printf("Test TXT:\n %s\n", record_buffer);
} 
```

```Output
Test TXT: 
v=spf1 include:_www.my_example.com ip4:192.2.2.10/31 ip4:192.2.2.11/31 ~all
```

## <a name="nx_dns_packet_pool_set"></a>nx_dns_packet_pool_set

Impostare il pool di pacchetti del client DNS

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_packet_pool_set(NX_DNS *dns_ptr, NX_PACKET_POOL *pool_ptr);
```
### <a name="description"></a>Descrizione

Questo servizio imposta un pool di pacchetti creato in precedenza come pool di **pacchetti del client** DNS. Il client DNS userà questo pool di pacchetti per inviare query DNS, quindi il payload del pacchetto non deve essere minore di NX_DNS_PACKET_PAYLOAD_UNALIGNED che include il frame Ethernet, le intestazioni IP e UDP ed è definito in *nx_dns.h*.
 
>[!NOTE]
>Quando il client DNS viene eliminato, il pool di pacchetti non viene eliminato con esso ed è responsabilità dell'applicazione eliminare il pool di pacchetti quando non è più necessario.

>[!NOTE]
>Questo servizio è disponibile solo se l'opzione di NX_DNS_CLIENT_USER_CREATE_PACKET_POOL è definita in *nx_dns.h*

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr**: puntatore all'istanza del client DNS **creata in precedenza.**
- **pool_ptr:** Puntatore al pool di pacchetti creato in precedenza

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS**: (0x00) Completamento riuscito.
- **NX_NOT_ENABLED:**(0x14) Client non configurato per questa opzione
- NX_PTR_ERROR: (0x07) Puntatore IP o client DNS **non** valido.
- NX_CALLER_ERROR: (0x11) Chiamante del servizio non valido.

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio
```c
NX_DNS             my_dns;
NX_PACKET_POOL     client_pool;
NX_IP             *ip_ptr;


/* Create the DNS Client.  */
status =  nx_dns_create(&my_dns, ip_ptr, “My DNS Client”);

/* Create a packet pool for the DNS Client.  */
status =  nx_packet_pool_create(&client_pool, "DNS Client Packet Pool", 
                                 NX_DNS_PACKET_PAYLOAD, free_mem_pointer, 
                                 NX_DNS_PACKET_POOL_SIZE);

/* Set the DNS Client packet pool.  */
status =  nx_dns_packet_pool_set(&my_dns, &client_pool);

/* If status is NX_SUCCESS the DNS Client packet pool was successfully set.  */
```

## <a name="nx_dns_server_add"></a>nx_dns_server_add

Aggiungere l'indirizzo IP del server DNS

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_server_add(NX_DNS *dns_ptr, ULONG server_address);
```

### <a name="description"></a>Descrizione

Questo servizio aggiunge un server DNS IPv4 all'elenco di server.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al blocco di controllo DNS.  
- **server_address:** indirizzo IP del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Server successfully added (Aggiunta del server completata)
- **NX_DNS_DUPLICATE_ENTRY** o **NX_NO_MORE_ENTRIES:**(0x17) Nessun altro server DNS consentito (l'elenco è pieno)
- **NX_DNS_PARAM_ERROR:**(0xA8) Input non puntatore non valido
- NX_PTR_ERROR: (0x07) Input puntatore non valido
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio
- NX_DNS_BAD_ADDRESS_ERROR: (0xA4) Input dell'indirizzo del server Null

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Add a DNS Server at IP address 202.2.2.13.  */
status =  nx_dns_server_add(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully added.  */
```

## <a name="nx_dns_server_get"></a>nx_dns_server_get

Restituire un server DNS IPv4 dall'elenco client

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_server_get(NX_DNS *dns_ptr, UINT index, 
                       ULONG *dns_server_address);
```

### <a name="description"></a>Descrizione

Questo servizio restituisce l'indirizzo del server DNS IPv4 dall'elenco di server in corrispondenza dell'indice specificato. Si noti che l'indice è in base zero. Se l'indice di input supera le dimensioni dell'elenco client DNS, viene restituito un errore. Il *nx_dns_get_serverlist_size* può essere chiamato prima ottenere il numero di server DNS nell'elenco Client.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** Puntatore al blocco di controllo DNS  
- **index:** indice nell'elenco di server del client DNS
- **dns_server_address:** Puntatore all'indirizzo IP del server DNS

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Server riuscito restituito
- **NX_DNS_SERVER_NOT_FOUND**: (0xA9) L'indice punta a uno slot vuoto
- **NX_DNS_BAD_ADDRESS_ERROR**: (0xA4) L'indice punta all'indirizzo Null
- **NX_DNS_PARAM_ERROR:** l'indice (0xA8) supera le dimensioni dell'elenco
- NX_PTR_ERROR: (0x07) Puntatore DNS o IP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
ULONG     my_server_address;

/* Get the DNS Server at index 5 (zero based) into the Client list.  */
status =  nx_dns_server_get(&my_dns, 5, &my_server_addres);

/* If status is NX_SUCCESS a DNS Server was successfully
   returned.  */
```

## <a name="nx_dns_server_remove"></a>nx_dns_server_remove

Rimuovere un server DNS IPv4 dall'elenco client

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_server_remove(NX_DNS *dns_ptr, ULONG server_address);
```

### <a name="description"></a>Descrizione

Questo servizio rimuove un server DNS IPv4 dall'elenco Client.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al blocco di controllo DNS.
- **server_address**: indirizzo IP del server DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:** Rimozione del server DNS (0x00) completata
- **NX_DNS_SERVER_NOT_FOUND**: (0xA9) Server non in elenco client
- **NX_DNS_BAD_ADDRESS_ERROR:**(0xA4) Input dell'indirizzo del server Null
- NX_PTR_ERROR: (0x07) Puntatore DNS o IP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c
/* Remove the DNS Server at IP address is 202.2.2.13.  */
status =  nx_dns_server_remove(&my_dns, IP_ADDRESS(202,2,2,13));

/* If status is NX_SUCCESS a DNS Server was successfully
   removed.  */
```

## <a name="nx_dns_server_remove_all"></a>nx_dns_server_remove_all

Rimuovere tutti i server DNS dall'elenco client

### <a name="prototype"></a>Prototipo

```c
UINT nx_dns_server_remove_all(NX_DNS *dns_ptr);
```

### <a name="description"></a>Descrizione

Questo servizio rimuove tutti i server DNS dall'elenco Client.

### <a name="input-parameters"></a>Parametri di input

- **dns_ptr:** puntatore al blocco di controllo DNS.

### <a name="return-values"></a>Valori restituiti

- **NX_SUCCESS:**(0x00) Server DNS rimossi correttamente
- **NX_DNS_ERROR:**(0xA0) Impossibile ottenere il mutex di protezione
- NX_PTR_ERROR: (0x07) Puntatore DNS o IP non valido.
- NX_CALLER_ERROR: (0x11) Chiamante non valido di questo servizio

### <a name="allowed-from"></a>Consentito da

Thread

### <a name="example"></a>Esempio

```c

/* Remove all DNS Servers from the Client list.  */
status =  nx_dns_server_remove_all(&my_dns);

/* If status is NX_SUCCESS all DNS Servers were successfully removed.  */
```