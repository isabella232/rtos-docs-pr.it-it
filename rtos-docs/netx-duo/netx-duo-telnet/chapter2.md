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
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-telnet"></a><span data-ttu-id="0c290-103">Capitolo 2-installazione e uso di Azure RTO NetX Duo Telnet</span><span class="sxs-lookup"><span data-stu-id="0c290-103">Chapter 2 - Installation and use of Azure RTOS NetX Duo Telnet</span></span>

<span data-ttu-id="0c290-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente Telnet Azure RTO NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="0c290-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Duo Telnet component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="0c290-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="0c290-105">Product Distribution</span></span>

<span data-ttu-id="0c290-106">Il pacchetto telnet Azure RTO NetX Duo è disponibile all'indirizzo <https://github.com/azure-rtos/netxduo> .</span><span class="sxs-lookup"><span data-stu-id="0c290-106">The Azure RTOS NetX Duo Telnet package is available at <https://github.com/azure-rtos/netxduo>.</span></span> <span data-ttu-id="0c290-107">Il pacchetto include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="0c290-107">The package includes the following files:</span></span>

- <span data-ttu-id="0c290-108">**nxd_telnet_client. h**: file di intestazione per il client Telnet per NETX Duo</span><span class="sxs-lookup"><span data-stu-id="0c290-108">**nxd_telnet_client.h**: Header file for Telnet Client for NetX Duo</span></span>
- <span data-ttu-id="0c290-109">**nxd_telnet_client. c**: file di origine c per il client Telnet per NETX Duo</span><span class="sxs-lookup"><span data-stu-id="0c290-109">**nxd_telnet_client.c**: C Source file for Telnet Client for NetX Duo</span></span>
- <span data-ttu-id="0c290-110">**nxd_telnet_server. h**: file di intestazione per il server Telnet per NETX Duo</span><span class="sxs-lookup"><span data-stu-id="0c290-110">**nxd_telnet_server.h**: Header file for Telnet Server for NetX Duo</span></span>
- <span data-ttu-id="0c290-111">**nxd_telnet_server. c**: file di origine c per il server Telnet per NETX Duo</span><span class="sxs-lookup"><span data-stu-id="0c290-111">**nxd_telnet_server.c**: C Source file for Telnet Server for NetX Duo</span></span>
- <span data-ttu-id="0c290-112">**nxd_telnet.pdf**: Descrizione PDF di Telnet per NETX Duo</span><span class="sxs-lookup"><span data-stu-id="0c290-112">**nxd_telnet.pdf**: PDF description of Telnet for NetX Duo</span></span>
- <span data-ttu-id="0c290-113">dimostrazione di **demo_netxduo_telnet. c**: NETX Duo Telnet</span><span class="sxs-lookup"><span data-stu-id="0c290-113">**demo_netxduo_telnet.c**: NetX Duo Telnet demonstration</span></span>

## <a name="telnet-installation"></a><span data-ttu-id="0c290-114">Installazione Telnet</span><span class="sxs-lookup"><span data-stu-id="0c290-114">Telnet Installation</span></span>

<span data-ttu-id="0c290-115">Per utilizzare Telnet per NetX Duo, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="0c290-115">In order to use Telnet for NetX Duo, the entire distribution mentioned previously should be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="0c290-116">Se, ad esempio, NetX Duo è installato nella directory "*\threadx\arm7\green*", i file *nxd_telnet_client. h*, *nxd_telnet_client. c*, *nxd_telnet_server. c e nxd_telnet_server. h* devono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="0c290-116">For example, if NetX Duo is installed in the directory “*\threadx\arm7\green*” then the *nxd_telnet_client.h*, *nxd_telnet_client.c*, *nxd_telnet_server.c and nxd_telnet_server.h* files should be copied into this directory.</span></span>

## <a name="using-telnet"></a><span data-ttu-id="0c290-117">Uso di Telnet</span><span class="sxs-lookup"><span data-stu-id="0c290-117">Using Telnet</span></span>

<span data-ttu-id="0c290-118">L'uso di Telnet per NetX Duo è facile.</span><span class="sxs-lookup"><span data-stu-id="0c290-118">Using Telnet for NetX Duo is easy.</span></span> <span data-ttu-id="0c290-119">In pratica, il codice dell'applicazione deve includere *nxd_telnet_server. h* per le applicazioni server telnet e *nxd_telnet_client. h* per le applicazioni client telnet dopo aver incluso *tx_api. h* e *nx_api. h*, per usare threadX e NETX Duo.</span><span class="sxs-lookup"><span data-stu-id="0c290-119">Basically, the application code must include *nxd_telnet_server.h* for Telnet Server applications and *nxd_telnet_client.h* for Telnet Client applications after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX Duo.</span></span> <span data-ttu-id="0c290-120">Dopo che *l'intestazione* è stata inclusa, il codice dell'applicazione è quindi in grado di effettuare le chiamate di funzione Telnet specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="0c290-120">Once *the header* is included, the application code is then able to make the Telnet function calls specified later in this guide.</span></span> <span data-ttu-id="0c290-121">L'applicazione deve includere anche *nxd_telnet_client. c* e *nxd_telnet_server. c* nel processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="0c290-121">The application must also include *nxd_telnet_client.c* and *nxd_telnet_server.c* in the build process.</span></span> <span data-ttu-id="0c290-122">Questi file devono essere compilati allo stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0c290-122">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="0c290-123">Questo è tutto ciò che è necessario per usare NetX Duo Telnet.</span><span class="sxs-lookup"><span data-stu-id="0c290-123">This is all that is required to use NetX Duo Telnet.</span></span>

<span data-ttu-id="0c290-124">Se non sono necessarie funzionalità client Telnet, il file *nxd_telnet_client. c* può essere omesso.</span><span class="sxs-lookup"><span data-stu-id="0c290-124">If no Telnet Client capabilities are required, the *nxd_telnet_client.c* file may be omitted.</span></span>

<span data-ttu-id="0c290-125">Si noti inoltre che, poiché Telnet utilizza i servizi TCP NetX Duo, è necessario abilitare TCP con la chiamata *nx_tcp_enable* prima di utilizzare Telnet.</span><span class="sxs-lookup"><span data-stu-id="0c290-125">Note also that because Telnet utilizes NetX Duo TCP services, TCP must be enabled with the *nx_tcp_enable* call prior to using Telnet.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="0c290-126">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="0c290-126">Small Example System</span></span>

<span data-ttu-id="0c290-127">Un esempio di come usare NetX Duo Telnet è illustrato nella figura 1,1 riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="0c290-127">An example of how to use NetX Duo Telnet is shown in Figure 1.1 below.</span></span> <span data-ttu-id="0c290-128">In questo esempio, i file di inclusione telnet *vengono* introdotti nella riga 7 e 8.</span><span class="sxs-lookup"><span data-stu-id="0c290-128">In this example, the Telnet include files *are* brought in at line 7 and 8.</span></span> <span data-ttu-id="0c290-129">Successivamente, il server Telnet viene creato in "*tx_application_define*" alla riga 146.</span><span class="sxs-lookup"><span data-stu-id="0c290-129">Next, the Telnet Server is created in “*tx_application_define*” at line 146.</span></span> <span data-ttu-id="0c290-130">Si noti che i blocchi di controllo client e server Telnet sono definiti come variabili globali alla riga 23-24 in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0c290-130">Note that the Telnet Server and Client control blocks are defined as global variables at line 23-24 previously.</span></span>

<span data-ttu-id="0c290-131">Prima di poter avviare il server Telnet o il client, è necessario convalidare l'indirizzo IP con NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="0c290-131">Before the Telnet Server or Client can be started they must validate their IP address with NetX Duo.</span></span> <span data-ttu-id="0c290-132">Per le connessioni IPv4 questa operazione viene eseguita semplicemente aspettando brevemente di consentire al driver NetX di inizializzare il sistema alla riga 166.</span><span class="sxs-lookup"><span data-stu-id="0c290-132">For IPv4 connections this is accomplished by simply waiting briefly to let the NetX driver initialize the system on line 166.</span></span> <span data-ttu-id="0c290-133">Per le connessioni IPv6, è necessario abilitare IPv6 e ICMPv6 che esegue nelle righe 171-172.</span><span class="sxs-lookup"><span data-stu-id="0c290-133">For IPv6 connections, this requires enabling IPv6 and ICMPv6 which it does in lines 171-172.</span></span> <span data-ttu-id="0c290-134">Il client imposta i relativi indirizzi IPv6 globali e collega indirizzi IPv6 locali sull'interfaccia primaria sulla riga 181-186 e attende il completamento della convalida di NetX Duo in background.</span><span class="sxs-lookup"><span data-stu-id="0c290-134">The Client sets its global and link local IPv6 addresses on the primary interface on lines 181-186 and waits for NetX Duo validation to complete in the background.</span></span> <span data-ttu-id="0c290-135">Il server imposta inoltre i relativi indirizzi globali e di collegamento locale sulla relativa interfaccia principale nelle righe 192 – 198.</span><span class="sxs-lookup"><span data-stu-id="0c290-135">The Server also sets its global and link local addresses on its primary interface in lines 192 – 198.</span></span> <span data-ttu-id="0c290-136">Si noti che i due servizi, *nxd_ipv6_global_address_set* e *nxd_ipv6_linklocal_address_set* sono sostituiti con *nxd_ipv6_address_set servizio*.</span><span class="sxs-lookup"><span data-stu-id="0c290-136">Note that the two services, *nxd_ipv6_global_address_set* and *nxd_ipv6_linklocal_address_set* are replaced with *nxd_ipv6_address_set service*.</span></span> <span data-ttu-id="0c290-137">I due servizi precedenti sono ancora disponibili per le applicazioni legacy NetX Duo, ma sono deprecati.</span><span class="sxs-lookup"><span data-stu-id="0c290-137">The former two services are still available for legacy NetX Duo applications but are eventually deprecated.</span></span> <span data-ttu-id="0c290-138">Gli sviluppatori sono invitati a usare invece *nxd_ipv6_address_set* .</span><span class="sxs-lookup"><span data-stu-id="0c290-138">Developers are encouraged to use *nxd_ipv6_address_set* instead.</span></span>

<span data-ttu-id="0c290-139">Una volta completata la convalida degli indirizzi IP con NetX Duo, il server Telnet viene avviato alla riga 215 usando il servizio *nxd_telnet_server_start* .</span><span class="sxs-lookup"><span data-stu-id="0c290-139">After successful IP address validation with NetX Duo, the Telnet Server is started at line 215 using the *nxd_telnet_server_start* service.</span></span> <span data-ttu-id="0c290-140">Alla riga 226, il client Telnet viene creato usando il servizio *nx_telnet_client_create* .</span><span class="sxs-lookup"><span data-stu-id="0c290-140">At line 226 the Telnet Client is created using the *nx_telnet_client_create* service.</span></span> <span data-ttu-id="0c290-141">Si connette quindi al server Telnet alla riga 242 per le applicazioni IPv4 e alla riga 238 per le applicazioni IPv6 usando rispettivamente i servizi *nxd_telnet_client_connect* e *nx_telnet_client_connect* .</span><span class="sxs-lookup"><span data-stu-id="0c290-141">It then connects with the Telnet Server on line 242 for IPv4 applications and line 238 for IPv6 applications using the *nxd_telnet_client_connect* and *nx_telnet_client_connect* services respectively.</span></span> <span data-ttu-id="0c290-142">Dopo aver eseguito correttamente la convalida e la connessione al server, vengono apportati alcuni scambi prima della disconnessione.</span><span class="sxs-lookup"><span data-stu-id="0c290-142">After successful validation and connection with the server, it makes a few exchanges before disconnecting.</span></span>

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

## <a name="configuration-options"></a><span data-ttu-id="0c290-143">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="0c290-143">Configuration Options</span></span>

<span data-ttu-id="0c290-144">Per la compilazione di Telnet per NetX Duo sono disponibili diverse opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="0c290-144">There are several configuration options for building Telnet for NetX Duo.</span></span> <span data-ttu-id="0c290-145">Queste #defines possono essere impostate dall'applicazione prima dell'inclusione di *nxd_telnet_server. h*. e *nxd_telnet_client. h.*</span><span class="sxs-lookup"><span data-stu-id="0c290-145">These #defines can be set by the application prior to inclusion of *nxd_telnet_server.h*.and *nxd_telnet_client.h.*</span></span>

<span data-ttu-id="0c290-146">Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio:</span><span class="sxs-lookup"><span data-stu-id="0c290-146">Following is a list of all options, where each is described in detail:</span></span>  
  
- <span data-ttu-id="0c290-147">**NX_DISABLE_ERROR_CHECKING**: definito, questa opzione rimuove il controllo degli errori Telnet di base.</span><span class="sxs-lookup"><span data-stu-id="0c290-147">**NX_DISABLE_ERROR_CHECKING**: Defined, this option removes the basic Telnet error checking.</span></span> <span data-ttu-id="0c290-148">Viene in genere usato dopo il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0c290-148">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="0c290-149">**NX_TELNET_MAX_CLIENTS**: numero massimo di client Telnet supportati dal thread del server.</span><span class="sxs-lookup"><span data-stu-id="0c290-149">**NX_TELNET_MAX_CLIENTS**: The maximum number of Telnet Clients supported by the Server thread.</span></span> <span data-ttu-id="0c290-150">Per impostazione predefinita, questo valore è definito come 4 per specificare un massimo di 4 client alla volta.</span><span class="sxs-lookup"><span data-stu-id="0c290-150">By default, this value is defined as 4 to specify a maximum of 4 clients at a time.</span></span>
- <span data-ttu-id="0c290-151">**NX_TELNET_SERVER_PRIORITY**: priorità del thread del server Telnet.</span><span class="sxs-lookup"><span data-stu-id="0c290-151">**NX_TELNET_SERVER_PRIORITY**: The priority of the Telnet Server thread.</span></span> <span data-ttu-id="0c290-152">Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.</span><span class="sxs-lookup"><span data-stu-id="0c290-152">By default, this value is defined as 16 to specify priority 16.</span></span>
- <span data-ttu-id="0c290-153">**NX_TELNET_TOS**: tipo di servizio necessario per le richieste TCP Telnet.</span><span class="sxs-lookup"><span data-stu-id="0c290-153">**NX_TELNET_TOS**: Type of service required for the Telnet TCP requests.</span></span> <span data-ttu-id="0c290-154">Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare</span><span class="sxs-lookup"><span data-stu-id="0c290-154">By default, this value is defined as NX_IP_NORMAL to indicate</span></span>  
<span data-ttu-id="0c290-155">normale servizio pacchetti IP.</span><span class="sxs-lookup"><span data-stu-id="0c290-155">normal IP packet service.</span></span>
- <span data-ttu-id="0c290-156">**NX_TELNET_FRAGMENT_OPTION**: abilitazione del frammento per le richieste TCP Telnet.</span><span class="sxs-lookup"><span data-stu-id="0c290-156">**NX_TELNET_FRAGMENT_OPTION**: Fragment enable for Telnet TCP requests.</span></span> <span data-ttu-id="0c290-157">Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione TCP Telnet.</span><span class="sxs-lookup"><span data-stu-id="0c290-157">By default, this value is NX_DONT_FRAGMENT to disable Telnet TCP fragmenting.</span></span>
- <span data-ttu-id="0c290-158">**NX_TELNET_SERVER_WINDOW_SIZE**: dimensioni finestra socket server.</span><span class="sxs-lookup"><span data-stu-id="0c290-158">**NX_TELNET_SERVER_WINDOW_SIZE**: Server socket window size.</span></span> <span data-ttu-id="0c290-159">Per impostazione predefinita, questo valore è pari a 2048 byte.</span><span class="sxs-lookup"><span data-stu-id="0c290-159">By default, this value is 2048 bytes.</span></span>
- <span data-ttu-id="0c290-160">**NX_TELNET_TIME_TO_LIVE**: specifica il numero di router che questo pacchetto può superare prima che venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="0c290-160">**NX_TELNET_TIME_TO_LIVE**: Specifies the number of routers this packet can pass before it is discarded.</span></span> <span data-ttu-id="0c290-161">Il valore predefinito è impostato su 0x80.</span><span class="sxs-lookup"><span data-stu-id="0c290-161">The default value is set to 0x80.</span></span>
- <span data-ttu-id="0c290-162">**NX_TELNET_SERVER_TIMEOUT**: specifica il numero di cicli di threadX per i quali i servizi interni vengono sospesi.</span><span class="sxs-lookup"><span data-stu-id="0c290-162">**NX_TELNET_SERVER_TIMEOUT**: Specifies the number of ThreadX ticks that internal services will suspend for.</span></span> <span data-ttu-id="0c290-163">Il valore predefinito è impostato su 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="0c290-163">The default value is set to 10 seconds.</span></span>
- <span data-ttu-id="0c290-164">**NX_TELNET_ACTIVITY_TIMEOUT**: specifica il numero di secondi che possono trascorrere senza alcuna attività prima che il server disconnetta la connessione client.</span><span class="sxs-lookup"><span data-stu-id="0c290-164">**NX_TELNET_ACTIVITY_TIMEOUT**: Specifies the number of seconds that can elapse without any activity before the Server disconnects the Client connection.</span></span> <span data-ttu-id="0c290-165">Il valore predefinito è impostato su 600 secondi.</span><span class="sxs-lookup"><span data-stu-id="0c290-165">The default value is set to 600 seconds.</span></span>
- <span data-ttu-id="0c290-166">**NX_TELNET_TIMEOUT_PERIOD**: specifica il numero di secondi che intercorre tra il controllo dei timeout dell'attività client.</span><span class="sxs-lookup"><span data-stu-id="0c290-166">**NX_TELNET_TIMEOUT_PERIOD**: Specifies the number of seconds between checking for Client activity timeouts.</span></span> <span data-ttu-id="0c290-167">Il valore predefinito è impostato su 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="0c290-167">The default value is set to 60 seconds.</span></span>
- <span data-ttu-id="0c290-168">**NX_TELNET_SERVER_OPTION_DISABLE**: definito, la negoziazione delle opzioni Telnet è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="0c290-168">**NX_TELNET_SERVER_OPTION_DISABLE**: Defined, Telnet option negotiation is disabled.</span></span> <span data-ttu-id="0c290-169">Per impostazione predefinita, questa opzione non è definita.</span><span class="sxs-lookup"><span data-stu-id="0c290-169">By default this option is not defined.</span></span>
- <span data-ttu-id="0c290-170">**NX_TELNET_SERVER_USER_CREATE_PACKET_POOL**: se definito, il pool di pacchetti del server Telnet deve essere creato esternamente.</span><span class="sxs-lookup"><span data-stu-id="0c290-170">**NX_TELNET_SERVER_USER_CREATE_PACKET_POOL**: If defined, the Telnet Server packet pool must be created externally.</span></span> <span data-ttu-id="0c290-171">Questa operazione è significativa solo se NX_TELNET_SERVER_OPTION_DISABLE non è definito.</span><span class="sxs-lookup"><span data-stu-id="0c290-171">This is only meaningful if NX_TELNET_SERVER_OPTION_DISABLE is not defined.</span></span> <span data-ttu-id="0c290-172">Per impostazione predefinita, questa opzione non è definita e il thread del server Telnet crea il proprio pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="0c290-172">By default this option is not defined and the Telnet Server thread creates its own packet pool.</span></span>
- <span data-ttu-id="0c290-173">**NX_TELNET_SERVER_PACKET_PAYLOAD**: definisce le dimensioni del payload di pacchetti creato dal server Telnet per la negoziazione di opzioni.</span><span class="sxs-lookup"><span data-stu-id="0c290-173">**NX_TELNET_SERVER_PACKET_PAYLOAD**: Defines the size of the packet payload created by the Telnet Server for option negotiation.</span></span> <span data-ttu-id="0c290-174">Si noti che il server Telnet crea questo pool di pacchetti solo se NX_TELNET_SERVER _OPTION_DISABLE non è definito (le opzioni Telnet sono abilitate).</span><span class="sxs-lookup"><span data-stu-id="0c290-174">Note that the Telnet Server only creates this packet pool if NX_TELNET_SERVER _OPTION_DISABLE is not defined (Telnet options are enabled).</span></span> <span data-ttu-id="0c290-175">Il valore predefinito di questa opzione è 300.</span><span class="sxs-lookup"><span data-stu-id="0c290-175">The default value of this option is 300.</span></span>
- <span data-ttu-id="0c290-176">**NX_TELNET_SERVER_PACKET_POOL_SIZE**: definisce le dimensioni del pool di pacchetti del server Telnet utilizzato per le negoziazioni Telnet.</span><span class="sxs-lookup"><span data-stu-id="0c290-176">**NX_TELNET_SERVER_PACKET_POOL_SIZE**: Defines the size of the Telnet Server packet pool used for Telnet negotiations.</span></span> <span data-ttu-id="0c290-177">Si noti che il server Telnet crea questo pool di pacchetti solo se NX_TELNET_SERVER _OPTION_DISABLE non è definito (le opzioni Telnet sono abilitate).</span><span class="sxs-lookup"><span data-stu-id="0c290-177">Note that the Telnet Server only creates this packet pool if NX_TELNET_SERVER _OPTION_DISABLE is not defined (Telnet options are enabled).</span></span> <span data-ttu-id="0c290-178">Il valore predefinito di questa opzione è 2048 ( \~ pacchetti 5-6).</span><span class="sxs-lookup"><span data-stu-id="0c290-178">The default value of this option is 2048 (\~5-6 packets).</span></span>
