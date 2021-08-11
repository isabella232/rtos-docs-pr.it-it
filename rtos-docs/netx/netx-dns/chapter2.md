---
title: Capitolo 2 - Installazione e uso del Azure RTOS DNS NetX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS Dns Client NetX.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ffd6e7308775d919818420a2276f28d07ca3e9f467af71bb6e0524b7b3a79de8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799507"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-dns-client"></a>Capitolo 2 - Installazione e uso del Azure RTOS DNS NetX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del Azure RTOS Dns Client NetX.

## <a name="product-distribution"></a>Distribuzione del prodotto

Il client DNS NetX è disponibile all'indirizzo <https://github.com/azure-rtos/netx> . Il pacchetto include i file seguenti:

- **nx_dns.h:** file di intestazione per il client DNS NetX
- **nx_dns.c**: file di origine C per il client DNS NetX
- **nx_dns.pdf**: Descrizione PDF del client DNS NetX

## <a name="dns-client-installation"></a>Installazione del client DNS

Per usare NetX DNS Client, copiare i file di codice *sorgente nx_dns.c* e *nx_dns.h* nella stessa directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_dns.h* e *nx_dns.c* devono essere copiati in questa directory.

## <a name="using-the-dns-client"></a>Uso del client DNS

L'uso del client DNS NetX è semplice. Fondamentalmente, il codice dell'applicazione deve includere *nx_dns.h* dopo aver incluso *rispettivamente tx_api.h* e *nx_api.h*, per poter usare rispettivamente ThreadX e NetX. Dopo *nx_dns.h,* il codice dell'applicazione è in grado di effettuare le chiamate di funzione DNS specificate più avanti in questa guida. L'applicazione deve anche *aggiungere nx_dns.c* al processo di compilazione. Questo file deve essere compilato nello stesso modo degli altri file dell'applicazione e il relativo modulo oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare DNS NetX.

>[!NOTE]
> Poiché DNS usa i servizi UDP NetX,  è necessario nx_udp_enable udp prima di usare DNS.

## <a name="small-example-system-for-dns-client"></a>Small Example System for DNS Client 

Nel programma di applicazione DNS di esempio fornito in questa sezione *nx_dns.h* è incluso alla riga 6. NX_DNS_CLIENT_USER_CREATE_PACKET_POOL, che consente all'applicazione client DNS di creare il pool di pacchetti per il client DNS, viene dichiarato nelle righe 21-23. Questo pool di pacchetti viene usato per allocare pacchetti per l'invio di messaggi DNS. Se NX_DNS_CLIENT_USER_CREATE_PACKET_POOL definito, viene creato un pool di pacchetti nelle righe 71-91. Se questa opzione non è abilitata, il client DNS crea il proprio pool di pacchetti in base al payload del pacchetto e alle dimensioni del pool impostate dai parametri di configurazione in *nx_dns.h* e descritto altrove in questo capitolo.

Un altro pool di pacchetti viene creato nelle righe 93-105 per l'istanza IP client usata per le operazioni NetX interne. Successivamente, l'istanza IP viene creata *usando nx_ip_create* chiamata nella riga 107-119. È possibile che l'attività IP e il client DNS convivino lo stesso pool di pacchetti, ma poiché il client DNS in genere invia messaggi di dimensioni maggiori rispetto ai pacchetti di controllo inviati dall'attività IP, l'uso di pool di pacchetti separati rende più efficiente l'uso della memoria.

ARP e UDP (usati dalle reti IPv4) sono abilitati rispettivamente nelle righe 122 e 134.

>[!NOTE]
> Questa demo usa il driver "ram" dichiarato alla riga 37 e usato nella *nx_ip_create* chiamata. Questo driver ram viene distribuito con il codice sorgente NetX. Per eseguire effettivamente il client DNS, l'applicazione deve fornire un driver di rete fisico effettivo per trasmettere e ricevere pacchetti dal server DNS.

La funzione client thread entry *thread_client_entry* definita sotto la *funzione* tx_application_define client. Inizialmente rinuncia al controllo al sistema per consentire l'inizializzazione del thread dell'attività IP da parte del driver di rete.

Crea quindi il client DNS sulle righe 176-187, inizializza la cache sulle righe 189-200 e imposta il pool di pacchetti creato in precedenza sull'istanza del client DNS nelle righe 202-217. Aggiunge quindi un server DNS IPv4 alle righe 220-229.

Il resto del programma di esempio usa i servizi client DNS per eseguire query DNS. Le ricerche degli indirizzi IP host vengono eseguite nelle righe 240 e 262. La differenza tra questi due servizi, *nx_dns_host_by_name_get* *e nx_dns_ipv4_address_by_name_get*, è che il primo salva un solo indirizzo IP, mentre il secondo salva più indirizzi se il server DNS ha risposto.

Le ricerche inverse (nome host dall'indirizzo IP) vengono eseguite sulle righe 354 (*nx_dns_host_by_address_get*).

Altri due servizi per le ricerche DNS, CNAME e TXT, sono illustrati rispettivamente nelle righe 375 e 420 per individuare CNAME e TXT per il nome di dominio di input. Client DNS NetX come servizi simili per altri tipi di record, ad esempio NS, MX, SRV e SOA. Vedere il capitolo 3 per descrizioni dettagliate di tutte le ricerche di tipi di record disponibili nel client DNS NetX.

Quando il client DNS viene eliminato alla riga 594, usando il servizio *nx_dns_delete,* il pool di pacchetti per il client DNS non viene eliminato a meno che il client DNS non ha creato il proprio pool di pacchetti. In caso contrario, l'applicazione deve eliminare il pool di pacchetti se non ha più alcun utilizzo.

```c
/* This is a small demo of DNS Client for the high-performance NetX TCP/IP stack.*/
#include "tx_api.h"
#include "nx_api.h"
#include "nx_udp.h"
#include "nx_dns.h"

#define     DEMO_STACK_SIZE         4096
#define     NX_PACKET_PAYLOAD       1536
#define     NX_PACKET_POOL_SIZE     30 * NX_PACKET_PAYLOAD
#define     LOCAL_CACHE_SIZE        2048

/* Define the ThreadX and NetX object control blocks... */

NX_DNS             client_dns;
TX_THREAD          client_thread;
NX_IP              client_ip;
NX_PACKET_POOL     main_pool;

#ifdef NX_DNS_CLIENT_USER_CREATE_PACKET_POOL
    NX_PACKET_POOL client_pool;
#endif

UCHAR       local_cache[LOCAL_CACHE_SIZE];
UINT        error_counter = 0;
#define     CLIENT_ADDRESS IP_ADDRESS(192,168,0,11)
#define     DNS_SERVER_ADDRESS IP_ADDRESS(192,168,0,1)

/* Define thread prototypes. */
void        thread_client_entry(ULONG thread_input);

/***** Substitute your ethernet driver entry function here *********/
extern     VOID _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);

/* Define main entry point. */
int main()
{
/* Enter the ThreadX kernel. */
    tx_kernel_enter();
}
/* Define what the initial system looks like. */
void tx_application_define(void *first_unused_memory)
{
    CHAR     *pointer;
    UINT     status;
    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;
    /* Create the main thread. */
    tx_thread_create(&client_thread, "Client thread", 
                     thread_client_entry, 0, pointer, 
                     DEMO_STACK_SIZE, 4, 4, TX_NO_TIME_SLICE, 
                     TX_AUTO_START);
    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

#ifdef NX_DNS_CLIENT_USER_CREATE_PACKET_POOL

    /*Create the packet pool for the DNS Client to send packets. If the DNS Client is configured for letting the host application create the DNS packet pool, 
        (see NX_DNS_CLIENT_USER_CREATE_PACKET_POOL option), see 77 nx_dns_create() for guidelines on packet payload size and pool size. 
        packet traffic for NetX processes.
    */

    status = nx_packet_pool_create(&client_pool, "DNS Client Packet Pool", 
                                   NX_DNS_PACKET_PAYLOAD, pointer, 
                                   NX_DNS_PACKET_POOL_SIZE);

    pointer = pointer + NX_DNS_PACKET_POOL_SIZE;
    /* Check for pool creation error. */
    if (status)
    {
        error_counter++;
        return;
    }

#endif
/* Create the packet pool which the IP task will use to send packets. Also available to the host 94 application to send packet. */

    status = nx_packet_pool_create(&main_pool, "Main Packet Pool", 
                                   NX_PACKET_PAYLOAD, pointer, 
                                   NX_PACKET_POOL_SIZE);
    pointer = pointer + NX_PACKET_POOL_SIZE;

/* Check for pool creation error. */
    if (status)
    {
        error_counter++;
        return;
    }

/* Create an IP instance for the DNS Client. */
    status = nx_ip_create(&client_ip, "DNS Client IP Instance", 
                          CLIENT_ADDRESS, 0xFFFFFF00UL, 
                          &main_pool, _nx_ram_network_driver, 
                          pointer, 2048, 1);
    pointer = pointer + 2048;

/* Check for IP create errors. */
    if (status)
    {
        error_counter++;
        return;
    }
/* Enable ARP and supply ARP cache memory for the DNS Client IP. */
    status = nx_arp_enable(&client_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

/* Check for ARP enable errors. */
    if (status)
    {
        error_counter++;
        return;
    }
/* Enable UDP traffic because DNS is a UDP based protocol. */

    status = nx_udp_enable(&client_ip);
/* Check for UDP enable errors. */
    if (status)
    {
        error_counter++;
        return;
    }

}

#define BUFFER_SIZE 200
#define RECORD_COUNT 10

/* Define the Client thread. */
void thread_client_entry(ULONG thread_input)
{
    UCHAR         record_buffer[200];
    UINT          record_count;
    UINT          status;
    ULONG         host_ip_address;
    UINT          i;
    ULONG         *ipv4_address_ptr[RECORD_COUNT];

#ifdef NX_DNS_ENABLE_EXTENDED_RR_TYPES
    NX_DNS_NS_ENTRY    *nx_dns_ns_entry_ptr[RECORD_COUNT];
    NX_DNS_MX_ENTRY    *nx_dns_mx_entry_ptr[RECORD_COUNT];
    NX_DNS_SRV_ENTRY    *nx_dns_srv_entry_ptr[RECORD_COUNT];
    NX_DNS_SOA_ENTRY    *nx_dns_soa_entry_ptr;
    ULONG                host_address;
    USHORT               host_port;
#endif

    /* Give NetX IP task a chance to get initialized . */
    tx_thread_sleep(100);
    /* Create a DNS instance for the Client. Note this function will create the DNS Client packet pool for creating DNS message packets intended for querying its DNS server. */
    status = nx_dns_create(&client_dns, &client_ip, (UCHAR *)"DNS Client");

    /* Check for DNS create error. */
    if (status)
    {
        error_counter++;
        return;
    }

#ifdef NX_DNS_CACHE_ENABLE
    /* Initialize the cache. */
    status = nx_dns_cache_initialize(&client_dns, local_cache, LOCAL_CACHE_SIZE);

    /* Check for DNS cache error. */
    if (status)
    {
        error_counter++;
        return;
    }
#endif

/* Is the DNS client configured for the host application to create the pecket pool? */
#ifdef NX_DNS_CLIENT_USER_CREATE_PACKET_POOL

    /* Yes, use the packet pool created above which has appropriate payload size for DNS messages. */
    status = nx_dns_packet_pool_set(&client_dns, &client_pool);
    /* Check for set DNS packet pool error. */
        
    if (status)
    {
        error_counter++;
        return;
    }
#endif /* NX_DNS_CLIENT_USER_CREATE_PACKET_POOL */

    /* Add an IPv4 server address to the Client list. */
    status = nx_dns_server_add(&client_dns, DNS_SERVER_ADDRESS);
    /* Check for DNS add server error. */
    if (status)
    {
        error_counter++;
        return;
    }
/********************************************************************************/
/* Type A */
/* Send A type DNS Query to its DNS server and get the IPv4 address. */
/********************************************************************************/

    /* Look up an IPv4 address over IPv4. */
    status = nx_dns_host_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", &host_ip_address, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test A: \n");
        printf("IP address: %lu.%lu.%lu.%lu\n",
        host_ip_address >> 24,
        host_ip_address >> 16 & 0xFF,
        host_ip_address >> 8 & 0xFF,
        host_ip_address & 0xFF);
    }
    /* Look up IPv4 addresses to record multiple IPv4 addresses in record_buffer and return the IPv4 address count. */
    status = nx_dns_ipv4_address_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                             &record_buffer[0], BUFFER_SIZE, &record_count, 400);
    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test A: ");
        printf("record_count = %d \n", record_count);
    }
    /* Get the IPv4 addresses of host. */
    for(i =0; i< record_count; i++)
    {
        ipv4_address_ptr[i] = (ULONG *)(record_buffer + i * sizeof(ULONG));
        printf("record %d: IP address: %lu.%lu.%lu.%lu\n", i,
               *ipv4_address_ptr[i] >> 24,
               *ipv4_address_ptr[i] >> 16 & 0xFF,
               *ipv4_address_ptr[i] >> 8 & 0xFF,
               *ipv4_address_ptr[i] & 0xFF);
    }
/********************************************************************************/
/* Type A + CNAME response */
/* Send A type DNS Query to its DNS server and get the IPv4 address. */
/********************************************************************************/
    
    /* Look up an IPv4 address over IPv4. */
    status = nx_dns_host_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", &host_ip_address, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test A + CNAME response: \n");
        printf("IP address: %lu.%lu.%lu.%lu\n",
        host_ip_address >> 24,
        host_ip_address >> 16 & 0xFF,
        host_ip_address >> 8 & 0xFF,
        host_ip_address & 0xFF);
    }

    /* Look up IPv4 addresses to record multiple IPv4 addresses in record_buffer and return the IPv4 address count. */
    status = nx_dns_ipv4_address_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                             &record_buffer[0], BUFFER_SIZE, 
                                             &record_count, 400);
    
    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test Test A + CNAME response: ");
        printf("record_count = %d \n", record_count);
    }
    
    /* Get the IPv4 addresses of host. */
    for(i =0; i< record_count; i++)
    {
        ipv4_address_ptr[i] = (ULONG *)(record_buffer + i * sizeof(ULONG));
        printf("record %d: IP address: %lu.%lu.%lu.%lu\n", i,
                *ipv4_address_ptr[i] >> 24,
                *ipv4_address_ptr[i] >> 16 & 0xFF,
                *ipv4_address_ptr[i] >> 8 & 0xFF,
                *ipv4_address_ptr[i] & 0xFF);
    }

/********************************************************************************/
/* Type PTR */
/* Send PTR type DNS Query to its DNS server and get the host name. */
/********************************************************************************/

    /* Look up host name over IPv4. */
    host_ip_address = IP_ADDRESS(74, 125, 71, 106);
    status = nx_dns_host_by_address_get(&client_dns, host_ip_address, &record_buffer[0], BUFFER_SIZE, 450);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test PTR: %s\n", record_buffer);
    }

#ifdef NX_DNS_ENABLE_EXTENDED_RR_TYPES
/********************************************************************************/
/* Type CNAME */
/* Send CNAME type DNS Query to its DNS server and get the canonical name . */
/********************************************************************************/

    /* Send CNAME type to record the canonical name of host in record_buffer. */

    status = nx_dns_cname_get(&client_dns, (UCHAR *)"www.my_example.com", 
                              &record_buffer[0], BUFFER_SIZE, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test CNAME: %s\n", record_buffer);
    }
/********************************************************************************/
/* Type TXT */
/* Send TXT type DNS Query to its DNS server and get descriptive text. */
/********************************************************************************/

    /* Send TXT type to record the descriptive test of host in record_buffer. */
    status = nx_dns_host_text_get(&client_dns, (UCHAR *)"www.my_example.com", &record_buffer[0], BUFFER_SIZE, 400);
    
    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test TXT: %s\n", record_buffer);
    }

/********************************************************************************/
/* Type NS */
/* Send NS type DNS Query to its DNS server and get the domain name server. */
/********************************************************************************/

    /* Send NS type to record multiple name servers in record_buffer and return the name server count. If the DNS response includes the IPv4 addresses of name server, record it similarly in record_buffer. */

    status = nx_dns_domain_name_server_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                           &record_buffer[0], BUFFER_SIZE, 
                                           &record_count, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test NS: ");
        printf("record_count = %d \n", record_count);
    }
    /* Get the name server. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_ns_entry_ptr[i] = (NX_DNS_NS_ENTRY *)(record_buffer + i * sizeof(NX_DNS_NS_ENTRY));
        printf("record %d: IP address: %d.%d.%d.%d\n", i,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 24,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 16 & 0xFF,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address >> 8 & 0xFF,
                nx_dns_ns_entry_ptr[i] -> nx_dns_ns_ipv4_address & 0xFF);
        
        if(nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr)
            printf("hostname = %s\n", nx_dns_ns_entry_ptr[i] -> nx_dns_ns_hostname_ptr);
        else
            printf("hostname is not set\n");
    }

/********************************************************************************/
/* Type MX */
/* Send MX type DNS Query to its DNS server and get the domain mail exchange. */
/********************************************************************************/

    /* Send MX DNS query type to record multiple mail exchanges in record_buffer and return the mail exchange count. If the DNS response includes the IPv4 addresses of mail exchange, record it similarly in record_buffer. */

    status = nx_dns_domain_mail_exchange_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                             &record_buffer[0], BUFFER_SIZE, &record_count, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test MX: ");
        printf("record_count = %d \n", record_count);
    }
    /* Get the mail exchange. */
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

/********************************************************************************/
/* Type SRV */
/* Send SRV type DNS Query to its DNS server and get the location of services. */
/********************************************************************************/

    /* Send SRV DNS query type to record the location of services in record_buffer and return count. If the DNS response includes the IPv4 addresses of service name, record it similarly in record_buffer. */

    status = nx_dns_domain_service_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                       &record_buffer[0], BUFFER_SIZE, &record_count, 400);
    
    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test SRV: ");
        printf("record_count = %d \n", record_count);
    }
    
    /* Get the location of services. */
    for(i =0; i< record_count; i++)
    {
        nx_dns_srv_entry_ptr[i] = (NX_DNS_SRV_ENTRY *)(record_buffer + i * sizeof(NX_DNS_SRV_ENTRY));
        printf("record %d: IP address: %d.%d.%d.%d\n", i,
                nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 24,
                nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 16 & 0xFF,
                nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address >> 8 & 0xFF,
                nx_dns_srv_entry_ptr[i] -> nx_dns_srv_ipv4_address & 0xFF);

        printf("port number = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_port_number );
        printf("priority = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_priority );
        printf("weight = %d\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_weight );

        if(nx_dns_srv_entry_ptr[i] -> nx_dns_srv_hostname_ptr)
            printf("hostname = %s\n", nx_dns_srv_entry_ptr[i] -> nx_dns_srv_hostname_ptr);
        else
            printf("hostname is not set\n");
    }

    /* Get the service info, NetX old API.*/
    status = nx_dns_info_by_name_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                     &host_address, &host_port, 200);
    /* Check for DNS add server error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
    {
        printf("------------------------------------------------------> n");
        printf("Test SRV: ");
        printf("IP address: %d.%d.%d.%d\n",
                host_address >> 24,
                host_address >> 16 & 0xFF,
                host_address >> 8 & 0xFF,
                host_address & 0xFF);
        printf("port number = %d\n", host_port);
    }
    
/********************************************************************************/
/* Type SOA */
/* Send SOA type DNS Query to its DNS server and get zone of start of authority.*/
/********************************************************************************/

    /* Send SOA DNS query type to record the zone of start of authority in record_buffer. */

    status = nx_dns_authority_zone_start_get(&client_dns, (UCHAR *)"www.my_example.com", 
                                             &record_buffer[0], BUFFER_SIZE, 400);

    /* Check for DNS query error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    
    /* Get the loc*/
    nx_dns_soa_entry_ptr = (NX_DNS_SOA_ENTRY *) record_buffer;
    printf("------------------------------------------------------> n");
    printf("Test SOA: \n");
    printf("serial = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_serial );
    printf("refresh = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_refresh );
    printf("retry = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_retry );
    printf("expire = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_expire );
    printf("minmum = %d\n", nx_dns_soa_entry_ptr -> nx_dns_soa_minmum );
    if(nx_dns_soa_entry_ptr -> nx_dns_soa_host_mname_ptr)
        printf("host mname = %s\n", nx_dns_soa_entry_ptr -> nx_dns_soa_host_mname_ptr);
    else
        printf("host mame is not set\n");
    if(nx_dns_soa_entry_ptr -> nx_dns_soa_host_rname_ptr)
        printf("host rname = %s\n", nx_dns_soa_entry_ptr -> nx_dns_soa_host_rname_ptr);
    else
        printf("host rname is not set\n");
    #endif

    /* Shutting down...*/
    /* Terminate the DNS Client thread. */
    status = nx_dns_delete(&client_dns);
    return;
}
```

## <a name="configuration-options"></a>Opzioni di configurazione

Esistono diverse opzioni di configurazione per la creazione di DNS per NetX. Queste opzioni possono essere ridefinite in *nx_dns.h.* L'elenco seguente descrive ognuno in dettaglio:  

- **NX_DNS_TYPE_OF_SERVICE:** tipo di servizio necessario per le richieste UDP DNS. Per impostazione predefinita, questo valore è definito come NX_IP_NORMAL per il normale servizio di pacchetti IP.

- **NX_DNS_TIME_TO_LIVE**: specifica il numero massimo di router che un pacchetto può passare prima di essere eliminato. Il valore predefinito è 0x80

- **NX_DNS_FRAGMENT_OPTION**: imposta la proprietà socket per consentire o non consentire la frammentazione dei pacchetti in uscita. Il valore predefinito è NX_DONT_FRAGMENT.

- **NX_DNS_QUEUE_DEPTH**: imposta il numero massimo di pacchetti da archiviare nella coda di ricezione del socket. Il valore predefinito è 5.

- **NX_DNS_MAX_SERVERS**: specifica il numero massimo di server DNS nell'elenco server client.

- **NX_DNS_MESSAGE_MAX:** dimensione massima dei messaggi DNS per l'invio di query DNS. Il valore predefinito è 512, che è anche la dimensione massima specificata in RFC 1035 Section 2.3.4.

- **NX_DNS_PACKET_PAYLOAD_UNALIGNED:** se non è definito, la dimensione del payload del pacchetto client che include le intestazioni Ethernet, IP (o IPv6) e UDP più le dimensioni massime dei messaggi DNS specificate da NX_DNS_MESSAGE_MAX. Indipendentemente dalla definizione, il payload del pacchetto è allineato a 4 byte e archiviato in NX_DNS_PACKET_PAYLOAD.

- **NX_DNS_PACKET_POOL_SIZE**: dimensioni del pool di pacchetti client per l'invio di query DNS se NX_DNS_CLIENT_USER_CREATE_PACKET_POOL non è definito. Il valore predefinito è sufficientemente grande per 16 pacchetti di dimensioni del payload definite da NX_DNS_PACKET_PAYLOAD ed è allineato a 4 byte.

- **NX_DNS_MAX_RETRIES:** numero massimo di volte in cui il client DNS esegue una query sul server DNS corrente prima di provare un altro server o interrompere la query DNS.

- **NX_DNS_MAX_RETRANS_TIMEOUT:** timeout di ritrasmissione massimo per una query DNS in un server DNS specifico. Il valore predefinito è 64 secondi (64 *NX_IP_PERIODIC_RATE).

- **NX_DNS_IP_GATEWAY_AND_DNS_SERVER:** se definito e l'indirizzo del gateway IPv4 client è diverso da zero, il client DNS imposta il gateway IPv4 come server DNS primario del client. Il valore predefinito è Disattivata.

- **NX_DNS_PACKET_ALLOCATE_TIMEOUT**: imposta l'opzione di timeout per l'allocazione di un pacchetto dal pool di pacchetti client DNS. Il valore predefinito è 1 secondo (1*NX_IP_PERIODIC_RATE).

- **NX_DNS_CLIENT_USER_CREATE_PACKET_POOL**: consente al client DNS di consentire all'applicazione di creare e impostare il pool di pacchetti del client DNS. Per impostazione predefinita, questa opzione è disabilitata e il client DNS crea il proprio pool di *pacchetti* nx_dns_create .

- **NX_DNS_CLIENT_CLEAR_QUEUE:** consente al client DNS di cancellare i messaggi DNS precedenti dalla coda di ricezione prima di inviare una nuova query. La rimozione di questi pacchetti dalle query DNS precedenti impedisce alla coda socket del client DNS di sovraccaricare ed eliminare pacchetti validi.

- **NX_DNS_ENABLE_EXTENDED_RR_TYPES:** consente al client DNS di eseguire query su tipi di record DNS aggiuntivi in (ad esempio CNAME, NS, MX, SOA, SRV e TXT).

- **NX_DNS_CACHE_ENABLE**: consente al client DNS di archiviare i record di risposta nella cache DNS.
