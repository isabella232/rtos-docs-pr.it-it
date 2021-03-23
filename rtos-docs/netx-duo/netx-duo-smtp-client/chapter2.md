---
title: Capitolo 2-installazione e utilizzo del client SMTP NetX Duo
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client SMTP NetX Duo.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 86f324935ba32aab010b81f825be0a6564983a2e
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821689"
---
# <a name="chapter-2---installation-and-use-of-netx-duo-smtp-client"></a><span data-ttu-id="4a5da-103">Capitolo 2-installazione e utilizzo del client SMTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="4a5da-103">Chapter 2 - Installation and use of NetX Duo SMTP client</span></span>

<span data-ttu-id="4a5da-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client SMTP NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="4a5da-104">This chapter contains a description of various issues related to installation, setup, and usage of the NetX Duo SMTP Client component.</span></span>

## <a name="netx-duo-smtp-client-installation"></a><span data-ttu-id="4a5da-105">Installazione client SMTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="4a5da-105">NetX Duo SMTP Client Installation</span></span>

<span data-ttu-id="4a5da-106">Il client SMTP NetX Duo è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="4a5da-106">The NetX Duo SMTP Client is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="4a5da-107">Il pacchetto include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a5da-107">The package includes the following files:</span></span>

- <span data-ttu-id="4a5da-108">**nxd_smtp_client. c** File di origine C per l'API client SMTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="4a5da-108">**nxd_smtp_client.c** C Source file for NetX Duo SMTP Client API</span></span>
- <span data-ttu-id="4a5da-109">**nxd_smtp_client. h** File di intestazione C per l'API client SMTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="4a5da-109">**nxd_smtp_client.h** C Header file for NetX Duo SMTP Client API</span></span>
- <span data-ttu-id="4a5da-110">**demo_netxduo_smtp_client. c** Demo per il client SMTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="4a5da-110">**demo_netxduo_smtp_client.c** Demo for NetX Duo SMTP Client</span></span>
- <span data-ttu-id="4a5da-111">**nxd_smtp_client.pdf manuale dell'utente per** API client SMTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="4a5da-111">**nxd_smtp_client.pdf User Guide for** NetX Duo SMTP Client API</span></span>

<span data-ttu-id="4a5da-112">Per usare l'API client SMTP NetX Duo, l'intera distribuzione indicata in precedenza può essere copiata nella stessa directory in cui è installato NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="4a5da-112">To use the NetX Duo SMTP Client API, the entire distribution mentioned previously may be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="4a5da-113">Se, ad esempio, NetX Duo è installato nella directory "c:*\Progetto nel*", i file *nxd_smtp_client. h e nxd_smtp_client. c* devono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="4a5da-113">For example, if NetX Duo is installed in the directory “c:*\myproject*” then the *nxd_smtp_client.h, and nxd_smtp_client.c* files should be copied into this directory.</span></span>

## <a name="using-netx-duo-smtp-client"></a><span data-ttu-id="4a5da-114">Uso del client SMTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="4a5da-114">Using NetX Duo SMTP Client</span></span>

<span data-ttu-id="4a5da-115">Per creare l'applicazione client SMTP NetX Duo, è necessario innanzitutto compilare le librerie ThreadX e NetX Duo e includerle nel progetto di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a5da-115">To create the NetX Duo SMTP Client application, it must first build the ThreadX and NetX Duo libraries and include them in the build project.</span></span> <span data-ttu-id="4a5da-116">L'applicazione deve quindi includere TX *_api. h* e *nx_api. h nel codice sorgente dell'applicazione*.</span><span class="sxs-lookup"><span data-stu-id="4a5da-116">The application must then include tx *_api.h* and *nx_api.h in its application source code*.</span></span> <span data-ttu-id="4a5da-117">Questa operazione consentirà di abilitare i servizi ThreadX e NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="4a5da-117">This will enable ThreadX and NetX Duo services.</span></span> <span data-ttu-id="4a5da-118">Deve inoltre includere *nxd_smtp_client. c* e *nxd_smtp_client. h* dopo *tx_api. h* e *nx_api. h per l'utilizzo dei servizi client SMTP.*</span><span class="sxs-lookup"><span data-stu-id="4a5da-118">It must also include *nxd_smtp_client.c* and *nxd_smtp_client.h* after *tx_api.h* and *nx_api.h to use SMTP Client services.*</span></span>

<span data-ttu-id="4a5da-119">Questi file devono essere compilati in modo analogo agli altri file dell'applicazione e il codice oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a5da-119">These files must be compiled in the same manner as other application files and the object code must be linked along with the files of the application.</span></span> <span data-ttu-id="4a5da-120">Questo è tutto ciò che è necessario per creare un'applicazione client SMTP NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="4a5da-120">This is all that is required to create a NetX Duo SMTP Client application.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="4a5da-121">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="4a5da-121">Small Example System</span></span>

<span data-ttu-id="4a5da-122">Un esempio di utilizzo del client SMTP NetX Duo è descritto nella figura 1 riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="4a5da-122">An example of using the NetX Duo SMTP Client is described in Figure 1 that appears below.</span></span> <span data-ttu-id="4a5da-123">Il pool di pacchetti per l'istanza IP viene creato usando il servizio nx_packet_pool_create, alla riga 68 e ha un payload di pacchetti molto piccolo.</span><span class="sxs-lookup"><span data-stu-id="4a5da-123">The packet pool for the IP instance is created using the nx_packet_pool_create service, on line 68 and has a very small packet payload.</span></span> <span data-ttu-id="4a5da-124">Questo perché l'istanza IP invia solo pacchetti di controllo che non richiedono un payload molto elevato.</span><span class="sxs-lookup"><span data-stu-id="4a5da-124">This is because the IP instance only sends control packets which don’t require much payload.</span></span> <span data-ttu-id="4a5da-125">Il pool di pacchetti client SMTP creato alla riga 84 e viene utilizzato per trasmettere messaggi client SMTP ai dati del server e del messaggio.</span><span class="sxs-lookup"><span data-stu-id="4a5da-125">The SMTP Client packet pool created on line 84 and is used for transmitting SMTP Client messages to the server and message data.</span></span> <span data-ttu-id="4a5da-126">Il payload del pacchetto è molto più grande.</span><span class="sxs-lookup"><span data-stu-id="4a5da-126">Its packet payload is much larger.</span></span> <span data-ttu-id="4a5da-127">L'istanza IP viene creata nella riga 118 usando lo stesso pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="4a5da-127">The IP instance is created in line 118 using the same packet pool.</span></span> <span data-ttu-id="4a5da-128">TCP, obbligatorio per il protocollo SMTP, è abilitato nell'istanza IP alla riga 130.</span><span class="sxs-lookup"><span data-stu-id="4a5da-128">TCP, required for the SMTP protocol, is enabled on the IP instance in line 130.</span></span>

<span data-ttu-id="4a5da-129">Nel thread dell'applicazione, il client SMTP viene creato usando il servizio *nxd_smtp_client_create* , alla riga 170.</span><span class="sxs-lookup"><span data-stu-id="4a5da-129">In the application thread, the SMTP Client is created using the *nxd_smtp_client_create* service, in line 170.</span></span> <span data-ttu-id="4a5da-130">Il servizio *nxd_smtp_client_create* supporta le connessioni al server SMTP sia IPv4 che IPv6, sebbene questo esempio sia limitato a IPv4.</span><span class="sxs-lookup"><span data-stu-id="4a5da-130">The *nxd_smtp_client_create* service supports both IPv4 and IPv6 SMTP server connections although this example is limited to IPv4.</span></span> <span data-ttu-id="4a5da-131">Il messaggio di posta elettronica viene quindi inviato al client SMTP per la trasmissione alla riga 184 usando il servizio *nx_smtp_mail_send* .</span><span class="sxs-lookup"><span data-stu-id="4a5da-131">Then the mail message is submitted to the SMTP Client for transmission on line 184 using the *nx_smtp_mail_send* service.</span></span> <span data-ttu-id="4a5da-132">Si noti che la riga dell'oggetto con l'intestazione del contenuto della posta viene creata separatamente dal corpo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="4a5da-132">Note that the subject line with the mail content header is created separately from the message body.</span></span> <span data-ttu-id="4a5da-133">Si noti inoltre che la richiesta invia messaggi accetta un solo indirizzo di posta elettronica destinatario che si presuppone sia sintatticamente corretto.</span><span class="sxs-lookup"><span data-stu-id="4a5da-133">Also note that the send mail request accepts only one recipient mail address which is assumed to be syntactically correct.</span></span>

<span data-ttu-id="4a5da-134">Quindi, l'applicazione termina il client SMTP alla riga 200.</span><span class="sxs-lookup"><span data-stu-id="4a5da-134">Then the application terminates the SMTP Client on line 200.</span></span> <span data-ttu-id="4a5da-135">Il servizio *nx_smtp_client_delete* verifica che la connessione socket sia chiusa e che la porta non sia associata.</span><span class="sxs-lookup"><span data-stu-id="4a5da-135">The *nx_smtp_client_delete* service checks that the socket connection is closed and the port is unbound.</span></span> <span data-ttu-id="4a5da-136">Si noti che spetta all'applicazione client SMTP eliminare il pool di pacchetti se non è più usato.</span><span class="sxs-lookup"><span data-stu-id="4a5da-136">Note that it is up to the SMTP Client application to delete the packet pool if it no longer has use for it.</span></span>

```c
/*
   demo_netxduo_smtp_client.c

   This is a small demo of the NetX Duo SMTP Client on the high-performance NetX
   Duo TCP/IP stack.  This demo relies on Thread, NetX Duo and SMTP Client API to
   perform simple SMTP mail transfers in an SMTP client application to an SMTP mail
   server.   */

#include "nx_api.h"
#include "nx_ip.h"
#include "nxd_smtp_client.h"


/* Define the host user name and mail box parameters */
#define USERNAME               "myusername"
#define PASSWORD               "mypassword"
#define FROM_ADDRESS           "my@mycompany.com"
#define RECIPIENT_ADDRESS      "your@yourcompany.com"
#define LOCAL_DOMAIN           "mycompany.com"

#define SUBJECT_LINE           "NetX Duo SMTP Client Demo"
#define MAIL_BODY              "NetX Duo SMTP client is an SMTP client \r\n" \
                               “implementation for embedded devices to send  \r\n" \
                               "email to SMTP servers. This feature is \r\n" \
                               "intended to allow a device to send simple \r\n " \
                               "status reports using the most universal \r\n " \
                               “Internet application, email.\r\n"

/* See the NetX Duo SMTP Client User Guide for how to set the authentication type.
   The most common authentication type is PLAIN. */
#define CLIENT_AUTHENTICATION_TYPE 3


#define CLIENT_IP_ADDRESS  IP_ADDRESS(1,2,3,5)
#define SERVER_IP_ADDRESS  IP_ADDRESS(1,2,3,4)
#define SERVER_PORT        25


/* Define the NetX Duo and ThreadX structures for the SMTP client appliciation. */
NX_PACKET_POOL                  ip_packet_pool;
NX_PACKET_POOL                  client_packet_pool;
NX_IP                           client_ip;
TX_THREAD                       demo_client_thread;
static NX_SMTP_CLIENT           demo_client;


void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
void    demo_client_thread_entry(ULONG info);

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
    CHAR    *free_memory_pointer;


    /* Setup the pointer to unallocated memory.  */
    free_memory_pointer =  (CHAR *) first_unused_memory;

    /* Create IP default packet pool. */
    status =  nx_packet_pool_create(&ip_packet_pool, "Default IP Packet Pool",
                                    128, free_memory_pointer, 2048);

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 2048;

    /* Create SMTP Client packet pool. This is only for transmitting packets to the
       server. It need not be a separate packet pool than the IP default packet pool
       but for more efficient resource use, we use two different packet pools
       because the CLient SMTP messages generally require more payload than IP
       control packets.

       Packet payload depends on the SMTP Client application requirements.  Size of
       packet payload must include IP and TCP headers. For IPv6 connections, IP and
       TCP header data is 60 bytes. For IPv4 IP and TCP header data is 40 bytes (not
       including TCP options). */
    status |=  nx_packet_pool_create(&client_packet_pool, "SMTP Client Packet Pool",
                                     800, free_memory_pointer, (10*800));

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + (10*800);

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create the client thread */
    status = tx_thread_create(&demo_client_thread, "client_thread",
                              demo_client_thread_entry, 0, free_memory_pointer,
                              2048, 16, 16,
                              TX_NO_TIME_SLICE, TX_DONT_START);

    if (status != NX_SUCCESS)
    {

        printf("Error creating Client thread. Status 0x%x\r\n", status);
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer =  free_memory_pointer + 4096;


    /* Create Client IP instance. Remember to replace the generic driver
       with a real ethernet driver to actually run this demo! */

    status = nx_ip_create(&client_ip, "SMTP Client IP Instance", CLIENT_IP_ADDRESS,
                          0xFFFFFF00UL, &ip_packet_pool, _nx_ram_network_driver,
                          free_memory_pointer, 2048, 1);


    free_memory_pointer =  free_memory_pointer + 2048;

    /* Enable ARP and supply ARP cache memory. */
    status =  nx_arp_enable(&client_ip, (void **) free_memory_pointer, 1040);

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 1040;

    /* Enable TCP for client. */
    status =  nx_tcp_enable(&client_ip);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Enable ICMP for client. */
    status =  nx_icmp_enable(&client_ip);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Start the client thread. */
    tx_thread_resume(&demo_client_thread);

    return;
}


/* Define the smtp application thread task.   */
void    demo_client_thread_entry(ULONG info)
{

    UINT        status;
    UINT        error_counter = 0;
    NXD_ADDRESS server_ip_address;


    tx_thread_sleep(100);

    /* Set up the server IP address. */
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip_address.nxd_ip_address.v4 = SERVER_IP_ADDRESS;

    /* The demo client username and password is the authentication
       data used when the server attempts to authentication the client. */

    status =  nxd_smtp_client_create(&demo_client, &client_ip, &client_packet_pool,
                                     USERNAME,
                                     PASSWORD,
                                     FROM_ADDRESS,
                                     LOCAL_DOMAIN, CLIENT_AUTHENTICATION_TYPE,
                                     &server_ip_address, SERVER_PORT);

    if (status != NX_SUCCESS)
    {
        printf("Error creating the client. Status: 0x%x.\n\r", status);
        return;
    }

    /* Create a mail instance with the above text message and recipient info. */
    status =  nx_smtp_mail_send(&demo_client, RECIPIENT_ADDRESS,
                                TP_MAIL_PRIORITY_NORMAL,
                                SUBJECT_LINE, MAIL_BODY, sizeof(MAIL_BODY) - 1);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {

        /* Mail item was not sent. Note that we need not delete the client. The
           error status may be a failed authentication check or a broken connection.
           We can simply call nx_smtp_mail_send again.  */
        error_counter++;
    }

    /* Release resources used by client. Note that the transmit packet
       pool must be deleted by the application if it no longer has use for it.*/
    status = nx_smtp_client_delete(&demo_client);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    return;
}
```

<span data-ttu-id="4a5da-137">**Figura 1. Esempio di utilizzo del client SMTP con NetX Duo**</span><span class="sxs-lookup"><span data-stu-id="4a5da-137">**Figure 1. Example of SMTP Client use with NetX Duo**</span></span>

## <a name="client-configuration-options"></a><span data-ttu-id="4a5da-138">Opzioni di configurazione client</span><span class="sxs-lookup"><span data-stu-id="4a5da-138">Client Configuration Options</span></span>

<span data-ttu-id="4a5da-139">Sono disponibili diverse opzioni di configurazione con l'API client SMTP NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="4a5da-139">There are several configuration options with the NetX Duo SMTP Client API.</span></span> <span data-ttu-id="4a5da-140">Di seguito è riportato un elenco di tutte le opzioni descritte in dettaglio:</span><span class="sxs-lookup"><span data-stu-id="4a5da-140">Following is a list of all options described in detail:</span></span>

- <span data-ttu-id="4a5da-141">**NX_SMTP_CLIENT_TCP_WINDOW_SIZE** Questa opzione consente di impostare le dimensioni della finestra di ricezione TCP del client.</span><span class="sxs-lookup"><span data-stu-id="4a5da-141">**NX_SMTP_CLIENT_TCP_WINDOW_SIZE** This option sets the size of the Client TCP receive window.</span></span> <span data-ttu-id="4a5da-142">Questo deve essere impostato su un numero inferiore alle dimensioni MTU dell'hardware Ethernet sottostante e consentire le intestazioni IP e TCP.</span><span class="sxs-lookup"><span data-stu-id="4a5da-142">This should be set to below the MTU size of the underlying Ethernet hardware and allow room for IP and TCP headers.</span></span> <span data-ttu-id="4a5da-143">La dimensione predefinita della finestra TCP del client SMTP NetX Duo è 1460.</span><span class="sxs-lookup"><span data-stu-id="4a5da-143">The default NetX Duo SMTP Client TCP window size is 1460.</span></span>
- <span data-ttu-id="4a5da-144">**NX_SMTP_CLIENT_PACKET_TIMEOUT** Questa opzione imposta il timeout per l'allocazione dei pacchetti NetX.</span><span class="sxs-lookup"><span data-stu-id="4a5da-144">**NX_SMTP_CLIENT_PACKET_TIMEOUT** This option sets the timeout on NetX packet allocation.</span></span> <span data-ttu-id="4a5da-145">Il timeout del pacchetto client SMTP NetX Duo predefinito è di 2 secondi.</span><span class="sxs-lookup"><span data-stu-id="4a5da-145">The default NetX Duo SMTP Client packet timeout is 2 seconds.</span></span>
- <span data-ttu-id="4a5da-146">**NX_SMTP_CLIENT_CONNECTION_TIMEOUT** Questa opzione imposta il timeout di connessione socket TCP client.</span><span class="sxs-lookup"><span data-stu-id="4a5da-146">**NX_SMTP_CLIENT_CONNECTION_TIMEOUT** This option sets the Client TCP socket connect timeout.</span></span> <span data-ttu-id="4a5da-147">Il timeout di connessione del client SMTP NetX Duo predefinito è di 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="4a5da-147">The default NetX Duo SMTP Client connect timeout is 10 seconds.</span></span>
- <span data-ttu-id="4a5da-148">**NX_SMTP_CLIENT_DISCONNECT_TIMEOUT** Questa opzione imposta il timeout di disconnessione socket TCP client.</span><span class="sxs-lookup"><span data-stu-id="4a5da-148">**NX_SMTP_CLIENT_DISCONNECT_TIMEOUT** This option sets the Client TCP socket disconnect timeout.</span></span> <span data-ttu-id="4a5da-149">Il timeout di disconnessione del client SMTP NetX Duo predefinito è 5 secondi \*.</span><span class="sxs-lookup"><span data-stu-id="4a5da-149">The default NetX Duo SMTP Client disconnect timeout is 5 seconds\*.</span></span> <span data-ttu-id="4a5da-150">Si noti che se il client SMTP rileva un errore interno, ad esempio una connessione interrotta, può terminare la connessione con un timeout di attesa zero.</span><span class="sxs-lookup"><span data-stu-id="4a5da-150">Note that if the SMTP Client encounters an internal error such as a broken connection it may terminate the connection with a zero wait timeout.</span></span>
- <span data-ttu-id="4a5da-151">**NX_SMTP_GREETING_TIMEOUT** Questa opzione imposta il timeout per il client per ricevere la risposta del server al messaggio di saluto.</span><span class="sxs-lookup"><span data-stu-id="4a5da-151">**NX_SMTP_GREETING_TIMEOUT** This option sets the timeout for the Client to receive the Server reply to its greeting.</span></span> <span data-ttu-id="4a5da-152">Il valore predefinito del client SMTP NetX Duo è 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="4a5da-152">The default NetX Duo SMTP Client value is 10 seconds.</span></span>
- <span data-ttu-id="4a5da-153">**NX_SMTP_ENVELOPE_TIMEOUT** Questa opzione imposta il timeout per il client per ricevere la risposta del server a un comando client.</span><span class="sxs-lookup"><span data-stu-id="4a5da-153">**NX_SMTP_ENVELOPE_TIMEOUT** This option sets the timeout for the Client to receive the Server reply to a Client command.</span></span> <span data-ttu-id="4a5da-154">Il valore predefinito del client SMTP NetX Duo è 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="4a5da-154">The default NetX Duo SMTP Client value is 10 seconds.</span></span>
- <span data-ttu-id="4a5da-155">**NX_SMTP_MESSAGE_TIMEOUT** Questa opzione imposta il timeout per il client per ricevere la risposta del server alla ricezione dei dati del messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="4a5da-155">**NX_SMTP_MESSAGE_TIMEOUT** This option sets the timeout for the Client to receive the Server reply to receiving the mail message data.</span></span> <span data-ttu-id="4a5da-156">Il valore predefinito del client SMTP NetX Duo è 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="4a5da-156">The default NetX Duo SMTP Client value is 30 seconds.</span></span>
- <span data-ttu-id="4a5da-157">**NX_SMTP_CLIENT_SEND_TIMEOUT** Questa opzione definisce l'opzione di attesa del buffer per archiviare la password dell'utente durante l'autenticazione SMTP con il server.</span><span class="sxs-lookup"><span data-stu-id="4a5da-157">**NX_SMTP_CLIENT_SEND_TIMEOUT** This option defines the wait option of the buffer to store the user password during SMTP authentication with the Server.</span></span> <span data-ttu-id="4a5da-158">Il valore predefinito è 20 byte.</span><span class="sxs-lookup"><span data-stu-id="4a5da-158">The default value is 20 bytes.</span></span>
- <span data-ttu-id="4a5da-159">**NX_SMTP_SERVER_CHALLENGE_MAX_STRING** Questa opzione definisce la dimensione del buffer per l'estrazione della richiesta di verifica del server durante l'autenticazione SMTP.</span><span class="sxs-lookup"><span data-stu-id="4a5da-159">**NX_SMTP_SERVER_CHALLENGE_MAX_STRING** This option defines the size of the buffer for extracting the Server challenge during SMTP authentication.</span></span> <span data-ttu-id="4a5da-160">Il valore predefinito è 200 byte.</span><span class="sxs-lookup"><span data-stu-id="4a5da-160">The default value is 200 bytes.</span></span> <span data-ttu-id="4a5da-161">Per l'accesso e l'autenticazione normale, il client SMTP può probabilmente usare un buffer più piccolo.</span><span class="sxs-lookup"><span data-stu-id="4a5da-161">For LOGIN and PLAIN authentication, the SMTP Client can probably use a smaller buffer.</span></span>
- <span data-ttu-id="4a5da-162">**NX_SMTP_CLIENT_MAX_PASSWORD** Questa opzione definisce la dimensione del buffer in cui archiviare la password dell'utente durante l'autenticazione SMTP con il server.</span><span class="sxs-lookup"><span data-stu-id="4a5da-162">**NX_SMTP_CLIENT_MAX_PASSWORD** This option defines the size of the buffer to store the user password during SMTP authentication with the Server.</span></span> <span data-ttu-id="4a5da-163">Il valore predefinito è 20 byte.</span><span class="sxs-lookup"><span data-stu-id="4a5da-163">The default value is 20 bytes.</span></span> 
- <span data-ttu-id="4a5da-164">**NX_SMTP_CLIENT_MAX_USERNAME** Questa opzione definisce la dimensione del buffer in cui archiviare il nome utente dell'host durante l'autenticazione SMTP con il server.</span><span class="sxs-lookup"><span data-stu-id="4a5da-164">**NX_SMTP_CLIENT_MAX_USERNAME** This option defines the size of the buffer to store the host username during SMTP authentication with the Server.</span></span> <span data-ttu-id="4a5da-165">Il valore predefinito è 40 byte.</span><span class="sxs-lookup"><span data-stu-id="4a5da-165">The default value is 40 bytes.</span></span> 
