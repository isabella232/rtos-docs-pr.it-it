---
title: Capitolo 2-installazione e uso di Azure RTO NetX Duo Telnet
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente Telnet Azure RTO NetX Duo.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d5b24690db6ccbc582387dd9dba5b0471e6f278d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821629"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-telnet"></a>Capitolo 2-installazione e uso di Azure RTO NetX Duo Telnet

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente Telnet Azure RTO NetX Duo.

## <a name="product-distribution"></a>Distribuzione del prodotto

Il pacchetto telnet Azure RTO NetX Duo è disponibile all'indirizzo <https://github.com/azure-rtos/netxduo> . Il pacchetto include i file seguenti:

- **nxd_telnet_client. h**: file di intestazione per il client Telnet per NETX Duo
- **nxd_telnet_client. c**: file di origine c per il client Telnet per NETX Duo
- **nxd_telnet_server. h**: file di intestazione per il server Telnet per NETX Duo
- **nxd_telnet_server. c**: file di origine c per il server Telnet per NETX Duo
- **nxd_telnet.pdf**: Descrizione PDF di Telnet per NETX Duo
- dimostrazione di **demo_netxduo_telnet. c**: NETX Duo Telnet

## <a name="telnet-installation"></a>Installazione Telnet

Per utilizzare Telnet per NetX Duo, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo. Se, ad esempio, NetX Duo è installato nella directory "*\threadx\arm7\green*", i file *nxd_telnet_client. h*, *nxd_telnet_client. c*, *nxd_telnet_server. c e nxd_telnet_server. h* devono essere copiati in questa directory.

## <a name="using-telnet"></a>Uso di Telnet

L'uso di Telnet per NetX Duo è facile. In pratica, il codice dell'applicazione deve includere *nxd_telnet_server. h* per le applicazioni server telnet e *nxd_telnet_client. h* per le applicazioni client telnet dopo aver incluso *tx_api. h* e *nx_api. h*, per usare threadX e NETX Duo. Dopo che *l'intestazione* è stata inclusa, il codice dell'applicazione è quindi in grado di effettuare le chiamate di funzione Telnet specificate più avanti in questa guida. L'applicazione deve includere anche *nxd_telnet_client. c* e *nxd_telnet_server. c* nel processo di compilazione. Questi file devono essere compilati allo stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare NetX Duo Telnet.

Se non sono necessarie funzionalità client Telnet, il file *nxd_telnet_client. c* può essere omesso.

Si noti inoltre che, poiché Telnet utilizza i servizi TCP NetX Duo, è necessario abilitare TCP con la chiamata *nx_tcp_enable* prima di utilizzare Telnet.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di come usare NetX Duo Telnet è illustrato nella figura 1,1 riportata di seguito. In questo esempio, i file di inclusione telnet *vengono* introdotti nella riga 7 e 8. Successivamente, il server Telnet viene creato in "*tx_application_define*" alla riga 146. Si noti che i blocchi di controllo client e server Telnet sono definiti come variabili globali alla riga 23-24 in precedenza.

Prima di poter avviare il server Telnet o il client, è necessario convalidare l'indirizzo IP con NetX Duo. Per le connessioni IPv4 questa operazione viene eseguita semplicemente aspettando brevemente di consentire al driver NetX di inizializzare il sistema alla riga 166. Per le connessioni IPv6, è necessario abilitare IPv6 e ICMPv6 che esegue nelle righe 171-172. Il client imposta i relativi indirizzi IPv6 globali e collega indirizzi IPv6 locali sull'interfaccia primaria sulla riga 181-186 e attende il completamento della convalida di NetX Duo in background. Il server imposta inoltre i relativi indirizzi globali e di collegamento locale sulla relativa interfaccia principale nelle righe 192 – 198. Si noti che i due servizi, *nxd_ipv6_global_address_set* e *nxd_ipv6_linklocal_address_set* sono sostituiti con *nxd_ipv6_address_set servizio*. I due servizi precedenti sono ancora disponibili per le applicazioni legacy NetX Duo, ma sono deprecati. Gli sviluppatori sono invitati a usare invece *nxd_ipv6_address_set* .

Una volta completata la convalida degli indirizzi IP con NetX Duo, il server Telnet viene avviato alla riga 215 usando il servizio *nxd_telnet_server_start* . Alla riga 226, il client Telnet viene creato usando il servizio *nx_telnet_client_create* . Si connette quindi al server Telnet alla riga 242 per le applicazioni IPv4 e alla riga 238 per le applicazioni IPv6 usando rispettivamente i servizi *nxd_telnet_client_connect* e *nx_telnet_client_connect* . Dopo aver eseguito correttamente la convalida e la connessione al server, vengono apportati alcuni scambi prima della disconnessione.

```c
/* This is a small demo of TELNET on the high-performance NetX Duo TCP/IP stack.  
       This demo relies on ThreadX and NetX Duo to show a simple TELNET connection,
       send, server echo, and then disconnection from the TELNET server.  */
    
#include  "tx_api.h"
#include  "nx_api.h"
#include  "nxd_telnet_client.h"
#include  "nxd_telnet_server.h"
#define     DEMO_STACK_SIZE         4096    
   
/* Define the ThreadX and NetX object control blocks...  */
TX_THREAD               test_thread;
NX_PACKET_POOL          pool_server;
NX_PACKET_POOL          pool_client;
NX_IP                   ip_server;
NX_IP                   ip_client;
   
/* Define TELNET objects.  */

NX_TELNET_SERVER        my_server;
NX_TELNET_CLIENT        my_client;


#ifdef FEATURE_NX_IPV6

/* Define NetX Duo IP address for the NetX Duo Telnet Server and Client. */

NXD_ADDRESS     server_ip_address;
NXD_ADDRESS     client_ip_address;

#endif

#define         SERVER_ADDRESS          IP_ADDRESS(1,2,3,4)
#define         CLIENT_ADDRESS          IP_ADDRESS(1,2,3,5)

/* Define the counters used in the demo application...  */
ULONG                   error_counter;

/* Define timeout in ticks for connecting and sending/receiving data. */

#define                 TELNET_TIMEOUT  200

/* Define function prototypes.  */

void    thread_test_entry(ULONG thread_input);
void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);


/* Define the application's TELNET Server callback routines.  */

void    telnet_new_connection(NX_TELNET_SERVER *server_ptr, UINT 
                              logical_connection); 
void    telnet_receive_data(NX_TELNET_SERVER *server_ptr, UINT logical_connection, 
                            NX_PACKET *packet_ptr);
void    telnet_connection_end(NX_TELNET_SERVER *server_ptr, UINT 
                              logical_connection);

/* Define main entry point.  */

int main()
{

    /* Enter the ThreadX kernel.  */
    tx_kernel_enter();
}

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

UINT    status;
CHAR    *pointer;
UINT    iface_index, address_index;
    
    /* Setup the working pointer.  */
    pointer =  (CHAR *) first_unused_memory;
    
    /* Create the main thread.  */
    tx_thread_create(&test_thread, "test thread", thread_test_entry, 0,  
                     pointer, DEMO_STACK_SIZE, 
                     2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer =  pointer + DEMO_STACK_SIZE;
    
    /* Initialize the NetX system.  */
    nx_system_initialize();
    
    /* Create packet pool.  */
    nx_packet_pool_create(&pool_server, "Server NetX Packet Pool", 600, pointer, 8192);
    pointer = pointer + 8192;
    
    /* Create an IP instance.  */
    nx_ip_create(&ip_server, "Server NetX IP Instance", SERVER_ADDRESS, 
                 0xFFFFFF00UL, &pool_server, _nx_ram_network_driver,
                 pointer, 4096, 1);
    
    pointer =  pointer + 4096;
    
    /* Create another packet pool. */
    nx_packet_pool_create(&pool_client, "Client NetX Packet Pool", 600, 
                          pointer, 8192);
    pointer = pointer + 8192;
    
    /* Create another IP instance.  */
    nx_ip_create(&ip_client, "Client NetX IP Instance", CLIENT_ADDRESS, 
                 0xFFFFFF00UL, &pool_client, _nx_ram_network_driver, 
                 pointer, 4096, 1);
    
    pointer = pointer + 4096;
    
    /* Enable ARP and supply ARP cache memory for IP Instance 0.  */
    nx_arp_enable(&ip_server, (void *) pointer, 1024);
    pointer = pointer + 1024;
    
    /* Enable ARP and supply ARP cache memory for IP Instance 1.  */
    nx_arp_enable(&ip_client, (void *) pointer, 1024);
    pointer = pointer + 1024;
    
    /* Enable TCP processing for both IP instances.  */
    nx_tcp_enable(&ip_server);
    nx_tcp_enable(&ip_client);

#ifdef FEATURE_NX_IPV6

    /* Next set the NetX Duo Telnet Server and Client addresses. */
    server_ip_address.nxd_ip_address.v6[3] = 0x105;
    server_ip_address.nxd_ip_address.v6[2] = 0x0;
    server_ip_address.nxd_ip_address.v6[1] = 0x0000f101;
    server_ip_address.nxd_ip_address.v6[0] = 0x20010db1;
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;

    client_ip_address.nxd_ip_address.v6[3] = 0x101;
    client_ip_address.nxd_ip_address.v6[2] = 0x0;
    client_ip_address.nxd_ip_address.v6[1] = 0x0000f101;
    client_ip_address.nxd_ip_address.v6[0] = 0x20010db1;
    client_ip_address.nxd_ip_version = NX_IP_VERSION_V6;

#endif

    /* Create the NetX Duo TELNET Server.  */
    status =  nx_telnet_server_create(&my_server, "Telnet Server", &ip_server, 
                                      pointer, 2048, telnet_new_connection, telnet_receive_data, 
                                      telnet_connection_end);
    
    /* Check for errors.  */
    if (status)
        error_counter++;
    
    return;
}

/* Define the test thread.  */
void    thread_test_entry(ULONG thread_input)
{

NX_PACKET   *my_packet;
UINT        status;
    
    /* Allow other threads (e.g. IP thread task) to run first. */
    tx_thread_sleep(100);
    
    #ifdef FEATURE_NX_IPV6
    /* Here's where we make the Telnet Client IPv6 enabled. */
    nxd_ipv6_enable(&ip_client);
    nxd_icmp_enable(&ip_client);     
    
    /* Wait till the IP task thread initializes the system. */
    tx_thread_sleep(100);
        
    /* Set up the Client addresses on the Client IP for the primary interface. */
    if_index = 0;
    
    status = nxd_ipv6_address_set(&ip_ client, iface_index, NX_NULL, 10, 
                                  &address_index);
    status = nxd_ipv6_address_set(&ip_ client, iface_index, & client _ip_address, 
                                   64, &address_index);
        
    /* Allow NetX Duo time to validate addresses. */
    tx_thread_sleep(400);
    
    /* Set up the Server addresses on the Client IP. */
    iface_index = 0;
    status = nxd_ipv6_address_set (&ip_server, iface_index, NX_NULL, 10, 
                                   &address_index);
    
    status = nxd_ ipv6_address _set(&ip_server, iface_index, & server _ip_address, 
                                     64, &address_index);
        
    /* Allow NetX Duo time to validate addresses. */     
    tx_thread_sleep(400);
    
    #endif
    
    /* Start the TELNET Server.  */
    status =  nx_telnet_server_start(&my_server);
    
    /* Check for errors.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* Create a TELENT client instance.  */
    status =  nx_telnet_client_create(&my_client, "My TELNET Client", 
                                      &ip_client, 600);
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    #ifdef FEATURE_NX_IPV6
    
        /* Connect the TELNET client to the TELNET Server at port 23.  */
        status =  nxd_telnet_client_connect(&my_client, &server_ip_address, 23, 
                                             TELNET_TIMEOUT);
    
    #else
        /* Connect the TELNET client to the TELNET Server at port 23.  */
        status =  nx_telnet_client_connect(&my_client, SERVER_ADDRESS, 23,
                                            TELNET_TIMEOUT);
    #endif
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* Allocate a packet.  */
    status =  nx_packet_allocate(&pool_client, &my_packet, NX_TCP_PACKET, 
                                  NX_WAIT_FOREVER);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* Build a simple 1-byte message.  */
    nx_packet_data_append(my_packet, "a", 1, &pool_client, NX_WAIT_FOREVER);
    
    /* Send the packet to the TELNET Server.  */
    status =  nx_telnet_client_packet_send(&my_client, my_packet, TELNET_TIMEOUT);
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* Pickup the Server header.  */
    status =  nx_telnet_client_packet_receive(&my_client, &my_packet, 
                                               TELNET_TIMEOUT);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* At this point the packet should contain the Server's banner
        message sent by the Server callback function below.  Just
        release it for this demo.  */
    nx_packet_release(my_packet);
    
    /* Pickup the Server echo of the character.  */
    status =  nx_telnet_client_packet_receive(&my_client, &my_packet, 
                                               TELNET_TIMEOUT);
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
    
    /* At this point the packet should contain the character 'a' that
        we sent earlier.  Just release the packet for now.  */
    nx_packet_release(my_packet);
    
    /* Now disconnect form the TELNET Server.  */
    status =  nx_telnet_client_disconnect(&my_client, TELNET_TIMEOUT);
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Delete the TELNET Client.  */
    status =  nx_telnet_client_delete(&my_client);
    
    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        return;
    }
}

/* This routine is called by the NetX Telnet Server whenever a new Telnet client 
    connection is established.  */
void  telnet_new_connection(NX_TELNET_SERVER *server_ptr, UINT logical_connection)
{

UINT        status;
NX_PACKET   *packet_ptr;

    /* Allocate a packet for client greeting. */
    status =  nx_packet_allocate(&pool_server, &packet_ptr, NX_TCP_PACKET, 
                                  NX_NO_WAIT);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Build a banner message and a prompt.  */
    nx_packet_data_append(packet_ptr,"**** Welcome to NetX TELNET Server ****\r\n\r\n\r\n", 45,                            
                         &pool_server, NX_NO_WAIT);

    nx_packet_data_append(packet_ptr, "NETX> ", 6, &pool_server, NX_NO_WAIT);
    
    /* Send the packet to the client.  */
    status =  nx_telnet_server_packet_send(server_ptr, logical_connection, 
                                           packet_ptr, TELNET_TIMEOUT);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        nx_packet_release(packet_ptr);
    }
    return;
}

/* This routine is called by the NetX Telnet Server whenever data is present on a 
    Telnet client connection.  */          
void  telnet_receive_data(NX_TELNET_SERVER *server_ptr, UINT logical_connection,
                          NX_PACKET *packet_ptr)
{

UINT    status;
UCHAR   alpha;

    /* This demo echoes the character back; on <cr,lf> sends a new prompt back to 
        the client.  A real system would likely buffer the character(s) received in a 
        buffer associated with the supplied logical connection and process it.  */

    /* Just throw away carriage returns.  */
    if ((packet_ptr -> nx_packet_prepend_ptr[0] == '\r') && (packet_ptr -> nx_packet_length == 1))
    {
        printf("telnet server received just a CRLF\n");

        nx_packet_release(packet_ptr);
        return;
    }

    /* Setup new line on line feed.  */
    if ((packet_ptr -> nx_packet_prepend_ptr[0] == '\n') || (packet_ptr -> nx_packet_prepend_ptr[1] == '\n'))
    {
        /* Clean up the packet.  */
        packet_ptr -> nx_packet_length =  0;
        packet_ptr -> nx_packet_prepend_ptr =  packet_ptr -> nx_packet_data_start + NX_TCP_PACKET;
        packet_ptr -> nx_packet_append_ptr =   packet_ptr -> nx_packet_data_start + NX_TCP_PACKET;

        /* Build the next prompt.  */
        nx_packet_data_append(packet_ptr, "\r\nNETX> ", 8, &pool_server, 
                              NX_NO_WAIT);

        /* Send the packet to the client.  */
        status =  nx_telnet_server_packet_send(server_ptr, logical_connection, 
                                               packet_ptr, TELNET_TIMEOUT);

        if (status != NX_SUCCESS)
        {
            error_counter++;
            nx_packet_release(packet_ptr);
        }
        return;
    }

    /* Pickup first character (usually only one from client).  */
    alpha =  packet_ptr -> nx_packet_prepend_ptr[0];

    /* Echo character.  */
    status =  nx_telnet_server_packet_send(server_ptr, logical_connection, 
                                           packet_ptr, TELNET_TIMEOUT);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        nx_packet_release(packet_ptr);
    }

    /* Check for a disconnection.  */
    if (alpha == 'q')
    {
        /* Initiate server disconnection.  */
        nx_telnet_server_disconnect(server_ptr, logical_connection);
    }
}


/* This routine is called by the NetX Telnet Server when the client disconnects.  */
void  telnet_connection_end(NX_TELNET_SERVER *server_ptr, UINT logical_connection)
{
    /* Cleanup any application specific connection or buffer information.  */
    return;
}
```

## <a name="configuration-options"></a>Opzioni di configurazione

Per la compilazione di Telnet per NetX Duo sono disponibili diverse opzioni di configurazione. Queste #defines possono essere impostate dall'applicazione prima dell'inclusione di *nxd_telnet_server. h*. e *nxd_telnet_client. h.*

Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio:  
  
- **NX_DISABLE_ERROR_CHECKING**: definito, questa opzione rimuove il controllo degli errori Telnet di base. Viene in genere usato dopo il debug dell'applicazione.
- **NX_TELNET_MAX_CLIENTS**: numero massimo di client Telnet supportati dal thread del server. Per impostazione predefinita, questo valore è definito come 4 per specificare un massimo di 4 client alla volta.
- **NX_TELNET_SERVER_PRIORITY**: priorità del thread del server Telnet. Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.
- **NX_TELNET_TOS**: tipo di servizio necessario per le richieste TCP Telnet. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare  
normale servizio pacchetti IP.
- **NX_TELNET_FRAGMENT_OPTION**: abilitazione del frammento per le richieste TCP Telnet. Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione TCP Telnet.
- **NX_TELNET_SERVER_WINDOW_SIZE**: dimensioni finestra socket server. Per impostazione predefinita, questo valore è pari a 2048 byte.
- **NX_TELNET_TIME_TO_LIVE**: specifica il numero di router che questo pacchetto può superare prima che venga eliminato. Il valore predefinito è impostato su 0x80.
- **NX_TELNET_SERVER_TIMEOUT**: specifica il numero di cicli di threadX per i quali i servizi interni vengono sospesi. Il valore predefinito è impostato su 10 secondi.
- **NX_TELNET_ACTIVITY_TIMEOUT**: specifica il numero di secondi che possono trascorrere senza alcuna attività prima che il server disconnetta la connessione client. Il valore predefinito è impostato su 600 secondi.
- **NX_TELNET_TIMEOUT_PERIOD**: specifica il numero di secondi che intercorre tra il controllo dei timeout dell'attività client. Il valore predefinito è impostato su 60 secondi.
- **NX_TELNET_SERVER_OPTION_DISABLE**: definito, la negoziazione delle opzioni Telnet è disabilitata. Per impostazione predefinita, questa opzione non è definita.
- **NX_TELNET_SERVER_USER_CREATE_PACKET_POOL**: se definito, il pool di pacchetti del server Telnet deve essere creato esternamente. Questa operazione è significativa solo se NX_TELNET_SERVER_OPTION_DISABLE non è definito. Per impostazione predefinita, questa opzione non è definita e il thread del server Telnet crea il proprio pool di pacchetti.
- **NX_TELNET_SERVER_PACKET_PAYLOAD**: definisce le dimensioni del payload di pacchetti creato dal server Telnet per la negoziazione di opzioni. Si noti che il server Telnet crea questo pool di pacchetti solo se NX_TELNET_SERVER _OPTION_DISABLE non è definito (le opzioni Telnet sono abilitate). Il valore predefinito di questa opzione è 300.
- **NX_TELNET_SERVER_PACKET_POOL_SIZE**: definisce le dimensioni del pool di pacchetti del server Telnet utilizzato per le negoziazioni Telnet. Si noti che il server Telnet crea questo pool di pacchetti solo se NX_TELNET_SERVER _OPTION_DISABLE non è definito (le opzioni Telnet sono abilitate). Il valore predefinito di questa opzione è 2048 ( \~ pacchetti 5-6).
