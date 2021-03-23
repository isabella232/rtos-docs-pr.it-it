---
title: Capitolo 2-installazione e utilizzo del client POP3 NetX Duo
description: Il client POP3 NetX Duo include un file di origine, un file di intestazione e un file dimostrativo.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 6ef4b6ba7aadf77ab95a4a12235eda847f32f3d5
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821749"
---
# <a name="chapter-2---installation-and-use-of-netx-duo-pop3-client"></a><span data-ttu-id="8df4d-103">Capitolo 2-installazione e utilizzo del client POP3 NetX Duo</span><span class="sxs-lookup"><span data-stu-id="8df4d-103">Chapter 2 - Installation and Use of NetX Duo POP3 Client</span></span>

<span data-ttu-id="8df4d-104">Il client POP3 NetX include un file di origine, un file di intestazione e un file dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="8df4d-104">NetX POP3 Client includes one source file, one header file, and a demo file.</span></span> <span data-ttu-id="8df4d-105">Per i servizi digest MD5 sono disponibili due file aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="8df4d-105">There are two additional files for MD5 digest services.</span></span> <span data-ttu-id="8df4d-106">È disponibile anche un file PDF della Guida per l'utente (questo documento).</span><span class="sxs-lookup"><span data-stu-id="8df4d-106">There is also a User Guide PDF file (this document).</span></span>

- <span data-ttu-id="8df4d-107">**nxd_pop3_client. c** File di origine C per l'API client POP3 NetX Duo</span><span class="sxs-lookup"><span data-stu-id="8df4d-107">**nxd_pop3_client.c** C Source file for NetX Duo POP3 Client API</span></span>
- <span data-ttu-id="8df4d-108">**nxd_pop3_client. h** File di intestazione C per l'API client POP3 NetX Duo</span><span class="sxs-lookup"><span data-stu-id="8df4d-108">**nxd_pop3_client.h** C Header file for NetX Duo POP3 Client API</span></span>
- <span data-ttu-id="8df4d-109">**demo_netxduo_pop3_client. c** File demo per la creazione e l'avvio di sessioni di client POP3</span><span class="sxs-lookup"><span data-stu-id="8df4d-109">**demo_netxduo_pop3_client.c** Demo file for POP3 Client creation and session initiation</span></span>
- <span data-ttu-id="8df4d-110">**nx_md5. c** File di origine C che definisce i servizi digest MD5</span><span class="sxs-lookup"><span data-stu-id="8df4d-110">**nx_md5.c** C Source file defining MD5 digest services</span></span>
- <span data-ttu-id="8df4d-111">**nx_md5. h** File di intestazione C che definisce i servizi digest MD5</span><span class="sxs-lookup"><span data-stu-id="8df4d-111">**nx_md5.h** C Header file defining MD5 digest services</span></span>
- <span data-ttu-id="8df4d-112">**nxd_pop3_client.pdf** Manuale dell'utente del client POP3 di NetX Duo</span><span class="sxs-lookup"><span data-stu-id="8df4d-112">**nxd_pop3_client.pdf** NetX Duo POP3 Client User Guide</span></span>

<span data-ttu-id="8df4d-113">Per usare il client POP3 NetX Duo, l'intera distribuzione indicata in precedenza può essere copiata nella stessa directory in cui è installato NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="8df4d-113">To use NetX Duo POP3 Client, the entire distribution mentioned previously can be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="8df4d-114">Se, ad esempio, NetX Duo è installato nella directory "*\threadx\mcf5272\green*", i file *nx_md5. h*, *nx_md5. c,* *nxd_pop3_client. h e nxd_pop3_client. c* devono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="8df4d-114">For example, if NetX Duo is installed in the directory “*\threadx\mcf5272\green*” then the *nx_md5.h*, *nx_md5.c,* *nxd_pop3_client.h, and nxd_pop3_client.c* files should be copied into this directory.</span></span>

## <a name="using-netx-duo-pop3-client"></a><span data-ttu-id="8df4d-115">Uso di NetX Duo POP3 client</span><span class="sxs-lookup"><span data-stu-id="8df4d-115">Using NetX Duo POP3 Client</span></span>

<span data-ttu-id="8df4d-116">Per usare il servizio client POP3 NetX Duo, l'applicazione deve aggiungere *nxd_pop3_client. c* al relativo progetto di compilazione.</span><span class="sxs-lookup"><span data-stu-id="8df4d-116">To use the NetX Duo POP3 Client service, the application must add *nxd_pop3_client.c* to its build project.</span></span> <span data-ttu-id="8df4d-117">Il codice dell'applicazione deve includere *nx_md5. h e nxd_pop3_client. h* dopo *tx_api. h* e *nx_api. h*, per usare threadX e NETX Duo.</span><span class="sxs-lookup"><span data-stu-id="8df4d-117">The application code must include *nx_md5.h, and nxd_pop3_client.h* after *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX Duo.</span></span>

<span data-ttu-id="8df4d-118">Questi file devono essere compilati in modo analogo agli altri file dell'applicazione e il codice oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8df4d-118">These files must be compiled in the same manner as other application files and the object code must be linked along with the files of the application.</span></span> <span data-ttu-id="8df4d-119">Questo è tutto ciò che è necessario per usare il client POP3 NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="8df4d-119">This is all that is required to use the NetX Duo POP3 Client.</span></span>

## <a name="small-example-of-the-netx-duo-pop3-client"></a><span data-ttu-id="8df4d-120">Piccolo esempio del client POP3 NetX Duo</span><span class="sxs-lookup"><span data-stu-id="8df4d-120">Small Example of the NetX Duo POP3 Client</span></span>

<span data-ttu-id="8df4d-121">Un esempio di come usare i servizi client POP3 di NetX Duo è descritto nella figura 1 riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="8df4d-121">An example of how to use NetX Duo POP3 Client services is described in Figure 1 that appears below.</span></span> <span data-ttu-id="8df4d-122">Questa demo imposta le due richiamate per la notifica del download della posta e il completamento della sessione sulle righe 37 e 38.</span><span class="sxs-lookup"><span data-stu-id="8df4d-122">This demo sets up the two callbacks for notification of mail download and session completion on lines 37 and 38.</span></span> <span data-ttu-id="8df4d-123">Il pool di pacchetti client POP3 viene creato alla riga 76.</span><span class="sxs-lookup"><span data-stu-id="8df4d-123">The POP3 Client packet pool is created on line 76.</span></span> <span data-ttu-id="8df4d-124">L'attività thread IP viene creata alla riga 88.</span><span class="sxs-lookup"><span data-stu-id="8df4d-124">The IP thread task is created on line 88.</span></span> <span data-ttu-id="8df4d-125">Si noti che questo pool di pacchetti viene utilizzato anche per il pool di pacchetti client POP3.</span><span class="sxs-lookup"><span data-stu-id="8df4d-125">Note that this packet pool is also used for the POP3 Client packet pool.</span></span> <span data-ttu-id="8df4d-126">TCP è abilitato nell'attività IP alla riga 107.</span><span class="sxs-lookup"><span data-stu-id="8df4d-126">TCP is enabled on the IP task in line 107.</span></span>

<span data-ttu-id="8df4d-127">Il client POP3 viene creato alla riga 133 all'interno della funzione entry thread dell'applicazione *demo_thread_entry*.</span><span class="sxs-lookup"><span data-stu-id="8df4d-127">The POP3 Client is created on line 133 inside the application thread entry function, *demo_thread_entry*.</span></span> <span data-ttu-id="8df4d-128">Questo perché il servizio *nx_pop3_client_create* tenta anche di effettuare una connessione TCP con il server POP3.</span><span class="sxs-lookup"><span data-stu-id="8df4d-128">This is because the *nx_pop3_client_create* service also attempts to make a TCP connection with the POP3 server.</span></span> <span data-ttu-id="8df4d-129">Se l'operazione ha esito positivo, l'applicazione esegue una query sul server POP3 per il numero di elementi nella relativa alla maildrop. alla riga 149 usando il servizio *nx_pop3_client_mail_items_get* .</span><span class="sxs-lookup"><span data-stu-id="8df4d-129">If successful, the application queries the POP3 server for the number of items in its maildrop on line 149 using the *nx_pop3_client_mail_items_get* service.</span></span>

<span data-ttu-id="8df4d-130">Se sono presenti uno o più elementi, l'applicazione scorre il ciclo while per ogni elemento di posta elettronica per scaricare il messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="8df4d-130">If there are one or more items, the application iterates through the while loop for each mail item to download the mail message.</span></span> <span data-ttu-id="8df4d-131">La richiesta RETR viene effettuata alla riga 149 nella chiamata *nx_pop3_client_mail_item_get* .</span><span class="sxs-lookup"><span data-stu-id="8df4d-131">The RETR request is made on line 149 in the *nx_pop3_client_mail_item_get* call.</span></span> <span data-ttu-id="8df4d-132">Se l'operazione ha esito positivo, l'applicazione Scarica i pacchetti usando il servizio *nx_pop3_client_mail_item_message_get* alla riga 177 fino a quando non rileva l'ultimo pacchetto nel messaggio ricevuto alla riga 196.</span><span class="sxs-lookup"><span data-stu-id="8df4d-132">If successful, the application downloads packets using the *nx_pop3_client_mail_item_message_get* service on line 177 till it detects the last packet in the message has been received on line 196.</span></span> <span data-ttu-id="8df4d-133">Infine, l'applicazione elimina l'elemento di posta elettronica, supponendo che si sia verificato un download corretto alla riga 199 della chiamata *nx_pop3_client_mail_item_delete* .</span><span class="sxs-lookup"><span data-stu-id="8df4d-133">Lastly, the application deletes the mail item, assuming a successful download has occurred on line 199 in *the nx_pop3_client_mail_item_delete* call.</span></span> <span data-ttu-id="8df4d-134">La RFC 1939 consiglia ai client POP3 di indicare al server di eliminare gli elementi di posta scaricati per evitare che la posta si accumuli nell'alla maildrop. del client.</span><span class="sxs-lookup"><span data-stu-id="8df4d-134">The RFC 1939 recommends that POP3 Clients instruct the Server to delete downloaded mail items to prevent mail accumulating in the Client’s maildrop.</span></span> <span data-ttu-id="8df4d-135">Il server può comunque eseguire questa operazione in modo automatico.</span><span class="sxs-lookup"><span data-stu-id="8df4d-135">The Server may automatically do so anyway.</span></span>

<span data-ttu-id="8df4d-136">Una volta scaricati tutti gli elementi di posta o se una chiamata al servizio client POP3 non riesce, l'applicazione termina il ciclo ed Elimina il client POP3 alla riga 217 usando il servizio *nx_pop3_client_delete* .</span><span class="sxs-lookup"><span data-stu-id="8df4d-136">Once all the mail items are downloaded, or if a POP3 Client service call fails, the application exits of the loop and deletes the POP3 Client on line 217 using the *nx_pop3_client_delete* service.</span></span>

```C
/*
   demo_netxduo_pop3.c

   This is a small demo of POP3 Client on the NetX Duo TCP/IP stack.
   This demo relies on Thread, NetX Duo and POP3 Client API to conduct
   a POP3 mail session.
 */

#include  "tx_api.h"
#include  "nx_api.h"
#include  "nxd_pop3_client.h"

#define DEMO_STACK_SIZE             4096
#define CLIENT_ADDRESS              IP_ADDRESS(192,2,2,61)
#define SERVER_ADDRESS              IP_ADDRESS(192,2,2,89)
#define SERVER_PORT                 110

/* Replace the 'ram' driver with your own Ethernet driver. */
void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Set up the POP3 Client.  */

TX_THREAD           demo_client_thread;
NX_POP3_CLIENT      demo_client;
NX_PACKET_POOL      client_packet_pool;
NX_IP               client_ip;

#define PAYLOAD_SIZE 500

/* Set up Client thread entry point. */
void    demo_thread_entry(ULONG info);


  /* Shared secret is the same as password. */

#define LOCALHOST                               "recipient@domain.com"
#define LOCALHOST_PASSWORD                      "testpwd"

/* Define main entry point.  */
int main()
{
    /* Enter the ThreadX kernel.  */
    tx_kernel_enter();
}

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

    UINT     status;
    UCHAR    *free_memory_pointer;


    /* Setup the working pointer.  */
    free_memory_pointer =  first_unused_memory;

    /* Create a client thread.  */
    tx_thread_create(&demo_client_thread, "Client", demo_thread_entry, 0,
                     free_memory_pointer, DEMO_STACK_SIZE, 1, 1,
                     TX_NO_TIME_SLICE, TX_AUTO_START);

    free_memory_pointer =  free_memory_pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system.  */
    nx_system_initialize();

    /* The demo client username and password is the authentication
       data used when the server attempts to authentication the client. */

    /* Create Client packet pool. */
    status =  nx_packet_pool_create(&client_packet_pool,"POP3 Client Packet Pool",
                                    PAYLOAD_SIZE, free_memory_pointer,
                                    (PAYLOAD_SIZE * 10));
    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + (PAYLOAD_SIZE * 10);


    /* Create IP instance for demo Client */
    status = nx_ip_create(&client_ip, "POP3 Client IP Instance",
                          CLIENT_ADDRESS, 0xFFFFFF00UL, &client_packet_pool,
                          _nx_ram_network_driver, free_memory_pointer,
                          2048, 1);

    if (status != NX_SUCCESS)
    {
        return;
    }

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer =  free_memory_pointer + 2048;

    /* Enable ARP and supply ARP cache memory. */
    nx_arp_enable(&client_ip, (void **) free_memory_pointer, 1024);

    /* Update pointer to unallocated (free) memory. */
    free_memory_pointer = free_memory_pointer + 1024;

    /* Enable TCP and ICMP for Client IP. */
    nx_tcp_enable(&client_ip);
    nx_icmp_enable(&client_ip);

    return;
}



/* Define the application thread entry function. */

void    demo_thread_entry(ULONG info)
{

    UINT        status;
    UINT        mail_item, number_mail_items;
    UINT        bytes_downloaded = 0;
    UINT        final_packet = NX_FALSE;
    ULONG       total_size, mail_item_size, bytes_retrieved;
    NX_PACKET   *packet_ptr;

    /* Let the IP instance get initialized with driver parameters. */
    tx_thread_sleep(40);


    /* Create a NetX POP3 Client instance with no byte or block memory pools.
       Note that it uses its password for its APOP shared secret. */
    status =  nx_pop3_client_create(&demo_client,
                                    NX_TRUE,
                                    &client_ip, &client_packet_pool, SERVER_ADDRESS,
                                    SERVER_PORT, LOCALHOST, LOCALHOST_PASSWORD);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {

        status = nx_pop3_client_delete(&demo_client);

        /* Abort. */
        return;
    }

    /* Find out how many items are in our mailbox.  */
    status = nx_pop3_client_mail_items_get(&demo_client, &number_mail_items,
                                            &total_size);

    printf("Got %d mail items, total size%d \n", number_mail_items, total_size);

    /* If nothing in the mailbox, disconnect. */
    if (number_mail_items == 0)
    {

        nx_pop3_client_delete(&demo_client);

        return;
    }

    /* Download all mail items.  */
    mail_item = 1;

    while (mail_item <= number_mail_items)
    {


        /* This submits a RETR request and gets the mail message size. */
        status = nx_pop3_client_mail_item_get(&demo_client, mail_item,
                                               &mail_item_size);

        /* Loop to get all mail message packets until the mail item is completely
           downloaded. */
        while((final_packet ==  NX_FALSE) && (status == NX_SUCCESS))
        {

            status = nx_pop3_client_mail_item_message_get(&demo_client, &packet_ptr,
                                                        &bytes_retrieved,
                                                        &final_packet);

            if (status != NX_SUCCESS)
            {

                break;
            }

            if (bytes_retrieved != 0)
            {

                printf("Received %d bytes of data for item %d: %s\n",
                        packet_ptr -> nx_packet_length,
                        mail_item, packet_ptr -> nx_packet_prepend_ptr);
            }

            nx_packet_release(packet_ptr);

            /* Determine if this is the last data packet. */
            if (final_packet)
            {
                /* It is. Let the server know it can delete this mail item. */
                status = nx_pop3_client_mail_item_delete(&demo_client, mail_item);
            }

            /* Keep track of how much mail message data is left. */
            bytes_downloaded += bytes_retrieved;
        }

        /* Get the next mail item. */
        mail_item++;

        tx_thread_sleep(100);

    }

    /* Disconnect from the POP3 server. */
    status = nx_pop3_client_quit(&demo_client);

    /* Delete the POP3 Client.  This will not delete the Client packet pool. */
    status = nx_pop3_client_delete(&demo_client);

}
```

<span data-ttu-id="8df4d-137">**Figura 1. Esempio di applicazione client POP3 NetX Duo**</span><span class="sxs-lookup"><span data-stu-id="8df4d-137">**Figure 1. Example of a NetX Duo POP3 Client application**</span></span>

## <a name="pop3-client-configuration-options"></a><span data-ttu-id="8df4d-138">Opzioni di configurazione del client POP3</span><span class="sxs-lookup"><span data-stu-id="8df4d-138">POP3 Client Configuration Options</span></span>

<span data-ttu-id="8df4d-139">Sono disponibili diverse opzioni di configurazione con il client POP3 NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="8df4d-139">There are several configuration options with the NetX Duo POP3 Client.</span></span> <span data-ttu-id="8df4d-140">Di seguito è riportato un elenco di tutte le opzioni descritte in dettaglio:</span><span class="sxs-lookup"><span data-stu-id="8df4d-140">Following is a list of all options described in detail:</span></span>

- <span data-ttu-id="8df4d-141">**NX_POP3_CLIENT_PACKET_TIMEOUT** Definisce l'opzione wait in secondi per l'allocazione di un pacchetto da parte del client POP3.</span><span class="sxs-lookup"><span data-stu-id="8df4d-141">**NX_POP3_CLIENT_PACKET_TIMEOUT** This defines the wait option in seconds for the POP3 Client to allocate a packet.</span></span> <span data-ttu-id="8df4d-142">Il valore predefinito è 1 secondo.</span><span class="sxs-lookup"><span data-stu-id="8df4d-142">The default value is 1 second.</span></span>
- <span data-ttu-id="8df4d-143">**NX_POP3_CLIENT_CONNECTION_TIMEOUT** Definisce l'opzione wait in secondi per la connessione del client POP3 al server POP3.</span><span class="sxs-lookup"><span data-stu-id="8df4d-143">**NX_POP3_CLIENT_CONNECTION_TIMEOUT** This defines the wait option in seconds for the POP3 Client to connect with the POP3 Server.</span></span> <span data-ttu-id="8df4d-144">Il valore predefinito è 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="8df4d-144">The default value is 30 seconds.</span></span>
- <span data-ttu-id="8df4d-145">**NX_POP3_CLIENT_DISCONNECT_TIMEOUT** Definisce l'opzione wait in secondi per la disconnessione del client POP3 dal server POP3.</span><span class="sxs-lookup"><span data-stu-id="8df4d-145">**NX_POP3_CLIENT_DISCONNECT_TIMEOUT** This defines the wait option in seconds for the POP3 Client to disconnect from the POP3 Server.</span></span> <span data-ttu-id="8df4d-146">Il valore predefinito è 2 secondi.</span><span class="sxs-lookup"><span data-stu-id="8df4d-146">The default value is 2 seconds.</span></span>
- <span data-ttu-id="8df4d-147">**NX_POP3_TCP_SOCKET_SEND_WAIT** Questa opzione imposta l'opzione wait in secondi nelle chiamate al servizio *nx_tcp_socket_send* .</span><span class="sxs-lookup"><span data-stu-id="8df4d-147">**NX_POP3_TCP_SOCKET_SEND_WAIT** This option sets the wait option in seconds in *nx_tcp_socket_send* service calls.</span></span> <span data-ttu-id="8df4d-148">Il valore predefinito è 2 secondi.</span><span class="sxs-lookup"><span data-stu-id="8df4d-148">The default value is 2 seconds.</span></span>
- <span data-ttu-id="8df4d-149">**NX_POP3_SERVER_REPLY_TIMEOUT** Questa opzione consente di impostare l'opzione wait in *nx_tcp_socket_receive* servizio per la risposta del server a una richiesta client.</span><span class="sxs-lookup"><span data-stu-id="8df4d-149">**NX_POP3_SERVER_REPLY_TIMEOUT** This option sets the wait option in *nx_tcp_socket_receive* service calls for the Server reply to a Client request.</span></span> <span data-ttu-id="8df4d-150">Il valore predefinito è 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="8df4d-150">The default value is 10 seconds.</span></span>
- <span data-ttu-id="8df4d-151">**NX_POP3_CLIENT_TCP_WINDOW_SIZE** Questa opzione consente di impostare le dimensioni della finestra di ricezione TCP del client.</span><span class="sxs-lookup"><span data-stu-id="8df4d-151">**NX_POP3_CLIENT_TCP_WINDOW_SIZE** This option sets the size of the Client TCP receive window.</span></span> <span data-ttu-id="8df4d-152">Questa impostazione deve essere impostata sulla dimensione MTU dell'istanza IP meno l'intestazione IP e TCP.</span><span class="sxs-lookup"><span data-stu-id="8df4d-152">This should be set to the IP instance MTU size minus the IP and TCP header.</span></span> <span data-ttu-id="8df4d-153">Il valore predefinito è 1460.</span><span class="sxs-lookup"><span data-stu-id="8df4d-153">The default value is 1460.</span></span> <span data-ttu-id="8df4d-154">Questa operazione dovrebbe essere inferiore se l'applicazione invia pacchetti POP3 su IPv6 (1440 byte) per tenere conto dell'intestazione IPv6 più grande.</span><span class="sxs-lookup"><span data-stu-id="8df4d-154">This should be less if the application is sending POP3 packets over IPv6 (1440 bytes) to account for the larger IPv6 header.</span></span>
- <span data-ttu-id="8df4d-155">**NX_POP3_MAX_USERNAME** Questa opzione consente di impostare le dimensioni del buffer del nome utente del client POP3.</span><span class="sxs-lookup"><span data-stu-id="8df4d-155">**NX_POP3_MAX_USERNAME** This option sets the size of the buffer of the POP3 Client user name.</span></span> <span data-ttu-id="8df4d-156">Il valore predefinito è 40 byte.</span><span class="sxs-lookup"><span data-stu-id="8df4d-156">The default value is 40 bytes.</span></span>
- <span data-ttu-id="8df4d-157">**NX_POP3_MAX_PASSWORD** Questa opzione consente di impostare le dimensioni del buffer della password del client POP3.</span><span class="sxs-lookup"><span data-stu-id="8df4d-157">**NX_POP3_MAX_PASSWORD** This option sets the size of the buffer of the POP3 Client password.</span></span> <span data-ttu-id="8df4d-158">Il valore predefinito è 20 byte.</span><span class="sxs-lookup"><span data-stu-id="8df4d-158">The default value is 20 bytes.</span></span>
