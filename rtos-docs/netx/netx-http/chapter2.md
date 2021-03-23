---
title: Capitolo 2-installazione e uso di HTTP NetX
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente HTTP NetX.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: db621e38e9d2324ca3ce2398aee9f729b05886ee
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822619"
---
# <a name="chapter-2---installation-and-use-of-netx-http"></a><span data-ttu-id="0304d-103">Capitolo 2-installazione e uso di HTTP NetX</span><span class="sxs-lookup"><span data-stu-id="0304d-103">Chapter 2 - Installation and use of NetX HTTP</span></span>

<span data-ttu-id="0304d-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente HTTP NetX.</span><span class="sxs-lookup"><span data-stu-id="0304d-104">This chapter contains a description of various issues related to installation, setup, and usage of the NetX HTTP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="0304d-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="0304d-105">Product Distribution</span></span>

<span data-ttu-id="0304d-106">Azure RTO NetX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .</span><span class="sxs-lookup"><span data-stu-id="0304d-106">Azure RTOS NetX can be obtained from our public source code repository at [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx).</span></span>

- <span data-ttu-id="0304d-107">**nx_http_client. h** File di intestazione per il client HTTP per NetX</span><span class="sxs-lookup"><span data-stu-id="0304d-107">**nx_http_client.h** Header file for HTTP Client for NetX</span></span>
- <span data-ttu-id="0304d-108">**nx_http_server. h** File di intestazione per il server HTTP per NetX</span><span class="sxs-lookup"><span data-stu-id="0304d-108">**nx_http_server.h** Header file for HTTP Server for NetX</span></span>
- <span data-ttu-id="0304d-109">**nx_http_client. c** File di origine C per il client HTTP per NetX</span><span class="sxs-lookup"><span data-stu-id="0304d-109">**nx_http_client.c** C Source file for HTTP Client for NetX</span></span>
- <span data-ttu-id="0304d-110">**nx_http_server. c** File di origine C per il server HTTP per NetX</span><span class="sxs-lookup"><span data-stu-id="0304d-110">**nx_http_server.c** C Source file for HTTP Server for NetX</span></span>
- <span data-ttu-id="0304d-111">**nx_md5. c** Algoritmi digest MD5</span><span class="sxs-lookup"><span data-stu-id="0304d-111">**nx_md5.c** MD5 digest algorithms</span></span>
- <span data-ttu-id="0304d-112">**filex_stub. h** File stub se FileX non è presente</span><span class="sxs-lookup"><span data-stu-id="0304d-112">**filex_stub.h** Stub file if FileX is not present</span></span>
- <span data-ttu-id="0304d-113">**nx_http.pdf** Descrizione di HTTP per NetX</span><span class="sxs-lookup"><span data-stu-id="0304d-113">**nx_http.pdf** Description of HTTP for NetX</span></span>
- <span data-ttu-id="0304d-114">**demo_netx_http. c** Dimostrazione HTTP di NetX</span><span class="sxs-lookup"><span data-stu-id="0304d-114">**demo_netx_http.c** NetX HTTP demonstration</span></span>

## <a name="http-installation"></a><span data-ttu-id="0304d-115">Installazione HTTP</span><span class="sxs-lookup"><span data-stu-id="0304d-115">HTTP Installation</span></span>

<span data-ttu-id="0304d-116">Per poter usare HTTP per NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX.</span><span class="sxs-lookup"><span data-stu-id="0304d-116">In order to use HTTP for NetX, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="0304d-117">Ad esempio, se NetX è installato nella directory "*\threadx\arm7\green*", il *nx_http_client. h* e *nx_http_client. c* per le applicazioni client http NetX e *nx_http_server. h* e *nx_http_server. c* per le applicazioni server http NETX.</span><span class="sxs-lookup"><span data-stu-id="0304d-117">For example, if NetX is installed in the directory “*\threadx\arm7\green*” then the *nx_http_client.h* and *nx_http_client.c* for NetX HTTP Client applications, and *nx_http_server.h* and *nx_http_server.c* for NetX HTTP Server applications.</span></span> <span data-ttu-id="0304d-118">*nx_md5. c* deve essere copiato in questa directory.</span><span class="sxs-lookup"><span data-stu-id="0304d-118">*nx_md5.c* should be copied into this directory.</span></span> <span data-ttu-id="0304d-119">Per la demo ' RAM driver ' dell'applicazione NetX client HTTP e i file server devono essere copiati nella stessa directory.</span><span class="sxs-lookup"><span data-stu-id="0304d-119">For the demo ‘ram driver’ application NetX HTTP Client and Server files should be copied into the same directory.</span></span>

## <a name="using-http"></a><span data-ttu-id="0304d-120">Uso di HTTP</span><span class="sxs-lookup"><span data-stu-id="0304d-120">Using HTTP</span></span>

<span data-ttu-id="0304d-121">L'uso di HTTP per NetX è facile.</span><span class="sxs-lookup"><span data-stu-id="0304d-121">Using HTTP for NetX is easy.</span></span> <span data-ttu-id="0304d-122">In pratica, il codice dell'applicazione deve includere *nx_http_client. h* e/o *nx_http_server. h* dopo aver incluso *tx_api. h, fx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX, FILEX e NETX.</span><span class="sxs-lookup"><span data-stu-id="0304d-122">Basically, the application code must include *nx_http_client.h* and/or *nx_http_server.h* after it includes *tx_api.h, fx_api.h,* and *nx_api.h*, in order to use ThreadX, FileX, and NetX, respectively.</span></span> <span data-ttu-id="0304d-123">Una volta inclusi i file di intestazione HTTP, il codice dell'applicazione è in grado di eseguire le chiamate di funzione HTTP specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="0304d-123">Once the HTTP header files are included, the application code is then able to make the HTTP function calls specified later in this guide.</span></span> <span data-ttu-id="0304d-124">L'applicazione deve includere anche *nx_http_client. c*, *nx_http_server. c* e *MD5. c* nel processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="0304d-124">The application must also include *nx_http_client.c*, *nx_http_server.c*, and *md5.c* in the build process.</span></span> <span data-ttu-id="0304d-125">Questi file devono essere compilati allo stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0304d-125">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="0304d-126">Questo è tutto ciò che è necessario per usare HTTP di NetX.</span><span class="sxs-lookup"><span data-stu-id="0304d-126">This is all that is required to use NetX HTTP.</span></span>

>[!NOTE] 
> <span data-ttu-id="0304d-127">Se NX_HTTP_DIGEST_ENABLE non viene specificato nel processo di compilazione, non è necessario aggiungere il file *MD5. c* all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0304d-127">If NX_HTTP_DIGEST_ENABLE is not specified in the build process, the *md5.c* file does not need to be added to the application.</span></span> <span data-ttu-id="0304d-128">Analogamente, se non sono richieste funzionalità client HTTP, il file *nx_http_client. c* può essere omesso.</span><span class="sxs-lookup"><span data-stu-id="0304d-128">Similarly, if no HTTP Client capabilities are required, the *nx_http_client.c* file may be omitted.</span></span>

>[!NOTE] 
> <span data-ttu-id="0304d-129">Poiché HTTP usa i servizi TCP NetX, è necessario abilitare TCP con la chiamata *nx_tcp_enable* prima di usare http.</span><span class="sxs-lookup"><span data-stu-id="0304d-129">Since HTTP utilizes NetX TCP services, TCP must be enabled with the *nx_tcp_enable* call prior to using HTTP.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="0304d-130">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="0304d-130">Small Example System</span></span>

<span data-ttu-id="0304d-131">Un esempio di come è facile usare HTTP di NetX è descritto nella figura 1,1 riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="0304d-131">An example of how easy it is to use NetX HTTP is described in Figure 1.1 that appears below.</span></span> <span data-ttu-id="0304d-132">In questo esempio, il file di inclusione HTTP *nx_http_client. h e nx_http_server. h vengono* portati nella riga 8.</span><span class="sxs-lookup"><span data-stu-id="0304d-132">In this example, the HTTP include file *nx_http_client.h and nx_http_server.h are* brought in at line 8.</span></span> <span data-ttu-id="0304d-133">Successivamente, il server HTTP viene creato in "*tx_application_define*" alla riga 131.</span><span class="sxs-lookup"><span data-stu-id="0304d-133">Next, the HTTP Server is created in “*tx_application_define*” at line 131.</span></span>

>[!NOTE] 
> <span data-ttu-id="0304d-134">Il blocco di controllo server HTTP "*Server*" è stato definito come variabile globale alla riga 25 in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0304d-134">The HTTP Server control block “*Server*” was defined as a global variable at line 25 previously.</span></span>

<span data-ttu-id="0304d-135">Una volta completata la creazione, un server HTTP viene avviato alla riga 136.</span><span class="sxs-lookup"><span data-stu-id="0304d-135">After successful creation, an HTTP Server is started at line 136.</span></span> <span data-ttu-id="0304d-136">Alla riga 149 viene creato il client HTTP.</span><span class="sxs-lookup"><span data-stu-id="0304d-136">At line 149 the HTTP Client is created.</span></span> <span data-ttu-id="0304d-137">Infine, il client scrive il file alla riga 157 e legge il file alla riga 195.</span><span class="sxs-lookup"><span data-stu-id="0304d-137">And finally, the Client writes the file at line 157 and reads the file back at line 195.</span></span>

```c
/* This is a small demo of HTTP on the high-performance NetX TCP/IP stack.
This demo relies on ThreadX, NetX, and FileX to show a simple HTML
transfer from the client and then back from the server. */

#include "tx_api.h"
#include "fx_api.h"
#include "nx_api.h"
#include "nx_http_client.h"
#include "nx_http_server.h"
#define     DEMO_STACK_SIZE     4096

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD         thread_0;
TX_THREAD         thread_1;
NX_PACKET_POOL    pool_0;
NX_PACKET_POOL    pool_1;
NX_IP             ip_0;
NX_IP             ip_1;
FX_MEDIA          ram_disk;

/* Define HTTP objects. */

NX_HTTP_SERVER    my_server;
NX_HTTP_CLIENT    my_client;

/* Define the counters used in the demo application... */

ULONG             error_counter;

/* Define the RAM disk memory. */

UCHAR             ram_disk_memory[32000];

/* Define function prototypes. */

void     thread_0_entry(ULONG thread_input);
VOID     _fx_ram_driver(FX_MEDIA *media_ptr) ;
void     _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
UINT     authentication_check(NX_HTTP_SERVER *server_ptr, UINT request_type,
                              CHAR *resource, CHAR **name, CHAR **password, 
                              CHAR **realm);

/* Define the application's authentication check. This is called by
the HTTP server whenever a new request is received. */
UINT authentication_check(NX_HTTP_SERVER *server_ptr, UINT request_type,
                         CHAR *resource, CHAR **name, CHAR **password, 
                         CHAR **realm);
{

    /* Just use a simple name, password, and realm for all
    requests and resources. */
    *name = "name";
    *password = "password";
    *realm = "NetX HTTP demo";

    /* Request basic authentication. */
    return(NX_HTTP_BASIC_AUTHENTICATE);
}

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */
void     tx_application_define(void *first_unused_memory)
{

CHAR     *pointer;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create the main thread. */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
                    pointer, DEMO_STACK_SIZE,
                    2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
                    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create packet pool. */
    nx_packet_pool_create(&pool_0, "NetX Packet Pool 0",
                         600, pointer, 8192);
                         pointer = pointer + 8192;

    /* Create an IP instance. */
    nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(1, 2, 3, 4),
                0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                pointer, 4096, 1);
                pointer = pointer + 4096;

    /* Create another packet pool. */
    nx_packet_pool_create(&pool_1, "NetX Packet Pool 1", 600, pointer, 8192);
                         pointer = pointer + 8192;

    /* Create another IP instance. */
    nx_ip_create(&ip_1, "NetX IP Instance 1", IP_ADDRESS(1, 2, 3, 5),
                0xFFFFFF00UL, &pool_1, _nx_ram_network_driver,
                pointer, 4096, 1);
                pointer = pointer + 4096;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    nx_arp_enable(&ip_0, (void *) pointer, 1024);
                 pointer = pointer + 1024;

    /* Enable ARP and supply ARP cache memory for IP Instance 1. */
    nx_arp_enable(&ip_1, (void *) pointer, 1024);
                 pointer = pointer + 1024;

    /* Enable TCP processing for both IP instances. */
    nx_tcp_enable(&ip_0);
    nx_tcp_enable(&ip_1);

    /* Open the RAM disk. */
                 _fx_ram_driver, ram_disk_memory, pointer, 4096) ;
                 pointer += 4096;

    /* Create the NetX HTTP Server. */
    nx_http_server_create(&my_server, "My HTTP Server", &ip_1, &ram_disk,
                         pointer, 4096, &pool_1, authentication_check, NX_NULL);
                         pointer = pointer + 4096;

    /* Start the HTTP Server. */
    nx_http_server_start(&my_server);
}

/* Define the test thread. */
void     thread_0_entry(ULONG thread_input)
{

NX_PACKET     *my_packet;
UINT          status;

    /* Create an HTTP client instance. */
    status = nx_http_client_create(&my_client, "My Client", &ip_0,
                                  &pool_0, 600);

    /* Check status. */
    if (status)
        error_counter++;

    /* Prepare to send the simple 103-byte HTML file to the Server. */
    status = nx_http_client_put_start(&my_client, IP_ADDRESS(1,2,3,5),
                                      "/test.htm", "name", "password", 103, 50);
    /* Check status. */
    if (status)
        error_counter++;

    /* Allocate a packet. */
    status = nx_packet_allocate(&pool_0, &my_packet, NX_TCP_PACKET,
                               NX_WAIT_FOREVER);
    /* Check status. */
    if (status != NX_SUCCESS)
        return;

    /* Build a simple 103-byte HTML page. */
    nx_packet_data_append(my_packet, "<HTML>\r\n", 8,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet,
                         "<HEAD><TITLE>NetX HTTP Test</TITLE></HEAD>\r\n", 44,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "<BODY>\r\n", 8,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "<H1>NetX Test Page</H1>\r\n", 25,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "</BODY>\r\n", 9,
                         &pool_0, NX_WAIT_FOREVER);
    nx_packet_data_append(my_packet, "</HTML>\r\n", 9,
                         &pool_0, NX_WAIT_FOREVER);

    /* Complete the PUT by writing the total length. */
    status = **nx_http_client_put_packet**(&my_client, my_packet, 50);

    /* Check status. */
    if (status)
        error_counter++;

    /* Now GET the file back! */
    status = nx_http_client_get_start(&my_client, IP_ADDRESS(1,2,3,5),
                                     "/test.htm", NX_NULL, 0, "name", 
                                     "password", 50);

    /* Check status. */
    if (status)
        error_counter++;

    /* Get a packet. */
    status = nx_http_client_get_packet(&my_client, &my_packet, 20);

    /* Check for an error. */
    if ((status) || (my_packet -> nx_packet_length != 103))
        error_counter++;

    /* Check to see if we have a packet. */
    if (status == NX_SUCCESS)
    {

        /* Yes, release it! */
        nx_packet_release(my_packet);
    }

    /* Flush the media. */
     fx_media_flush(&ram_disk);
 }
```

<span data-ttu-id="0304d-138">Figura 1,1 esempio di utilizzo HTTP con NetX</span><span class="sxs-lookup"><span data-stu-id="0304d-138">Figure 1.1 Example of HTTP use with NetX</span></span>

## <a name="configuration-options"></a><span data-ttu-id="0304d-139">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="0304d-139">Configuration Options</span></span>

<span data-ttu-id="0304d-140">Per la compilazione di HTTP per NetX sono disponibili diverse opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="0304d-140">There are several configuration options for building HTTP for NetX.</span></span> <span data-ttu-id="0304d-141">Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="0304d-141">Following is a list of all options, where each is described in detail.</span></span> <span data-ttu-id="0304d-142">I valori predefiniti sono elencati, ma possono essere ridefiniti prima dell'inclusione di *nx_http_client. h e nx_http_server. h*:</span><span class="sxs-lookup"><span data-stu-id="0304d-142">The default values are listed, but can be redefined prior to inclusion of *nx_http_client.h and nx_http_server.h*:</span></span>

- <span data-ttu-id="0304d-143">**NX_DISABLE_ERROR_CHECKING** Definita, questa opzione rimuove il controllo degli errori HTTP di base.</span><span class="sxs-lookup"><span data-stu-id="0304d-143">**NX_DISABLE_ERROR_CHECKING** Defined, this option removes the basic HTTP error checking.</span></span> <span data-ttu-id="0304d-144">Viene in genere usato dopo il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0304d-144">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="0304d-145">**NX_HTTP_SERVER_PRIORITY** Priorità del thread del server HTTP.</span><span class="sxs-lookup"><span data-stu-id="0304d-145">**NX_HTTP_SERVER_PRIORITY** The priority of the HTTP Server thread.</span></span> <span data-ttu-id="0304d-146">Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.</span><span class="sxs-lookup"><span data-stu-id="0304d-146">By default, this value is defined as 16 to specify priority 16.</span></span>
- <span data-ttu-id="0304d-147">**NX_HTTP_NO_FILEX** Definito, questa opzione fornisce uno stub per le dipendenze FileX.</span><span class="sxs-lookup"><span data-stu-id="0304d-147">**NX_HTTP_NO_FILEX** Defined, this option provides a stub for FileX dependencies.</span></span> <span data-ttu-id="0304d-148">Se questa opzione è definita, il client HTTP funzionerà senza alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="0304d-148">The HTTP Client will function without any change if this option is defined.</span></span> <span data-ttu-id="0304d-149">Il server HTTP dovrà essere modificato o l'utente dovrà creare un numero limitato di servizi FileX per il corretto funzionamento.</span><span class="sxs-lookup"><span data-stu-id="0304d-149">The HTTP Server will need to either be modified or the user will have to create a handful of FileX services in order to function properly.</span></span>
- <span data-ttu-id="0304d-150">**NX_HTTP_TYPE_OF_SERVICE** Tipo di servizio richiesto per le richieste TCP HTTP.</span><span class="sxs-lookup"><span data-stu-id="0304d-150">**NX_HTTP_TYPE_OF_SERVICE** Type of service required for the HTTP TCP requests.</span></span> <span data-ttu-id="0304d-151">Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.</span><span class="sxs-lookup"><span data-stu-id="0304d-151">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span>
- <span data-ttu-id="0304d-152">**NX_HTTP_SERVER_THREAD_TIME_SLICE** Numero di cicli del timer che il thread del server può eseguire prima di cedere ai thread con la stessa priorità.</span><span class="sxs-lookup"><span data-stu-id="0304d-152">**NX_HTTP_SERVER_THREAD_TIME_SLICE** The number of timer ticks the Server thread is allowed to run before yielding to threads of the same priority.</span></span> <span data-ttu-id="0304d-153">Il valore predefinito è 2.</span><span class="sxs-lookup"><span data-stu-id="0304d-153">The default value is 2.</span></span>
- <span data-ttu-id="0304d-154">**NX_HTTP_FRAGMENT_OPTION** L'abilitazione del frammento per le richieste TCP HTTP.</span><span class="sxs-lookup"><span data-stu-id="0304d-154">**NX_HTTP_FRAGMENT_OPTION** Fragment enable for HTTP TCP requests.</span></span> <span data-ttu-id="0304d-155">Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione TCP HTTP.</span><span class="sxs-lookup"><span data-stu-id="0304d-155">By default, this value is NX_DONT_FRAGMENT to disable HTTP TCP fragmenting.</span></span>
- <span data-ttu-id="0304d-156">**NX_HTTP_SERVER_WINDOW_SIZE** Dimensioni finestra socket server.</span><span class="sxs-lookup"><span data-stu-id="0304d-156">**NX_HTTP_SERVER_WINDOW_SIZE** Server socket window size.</span></span> <span data-ttu-id="0304d-157">Per impostazione predefinita, questo valore è pari a 2048 byte.</span><span class="sxs-lookup"><span data-stu-id="0304d-157">By default, this value is 2048 bytes.</span></span>
- <span data-ttu-id="0304d-158">**NX_HTTP_TIME_TO_LIVE** Specifica il numero di router che questo pacchetto può superare prima che venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="0304d-158">**NX_HTTP_TIME_TO_LIVE** Specifies the number of routers this packet can pass before it is discarded.</span></span> <span data-ttu-id="0304d-159">Il valore predefinito è impostato su 0x80.</span><span class="sxs-lookup"><span data-stu-id="0304d-159">The default value is set to 0x80.</span></span>
- <span data-ttu-id="0304d-160">**NX_HTTP_SERVER_TIMEOUT** Consente di specificare il numero di cicli ThreadX per i quali i servizi interni sospendono.</span><span class="sxs-lookup"><span data-stu-id="0304d-160">**NX_HTTP_SERVER_TIMEOUT** Specifies the number of ThreadX ticks that internal services will suspend for.</span></span> <span data-ttu-id="0304d-161">Il valore predefinito è impostato su 10 secondi (10 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="0304d-161">The default value is set to 10 seconds (10 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="0304d-162">**NX_HTTP_SERVER_TIMEOUT_ACCEPT** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_server_socket_accept* .</span><span class="sxs-lookup"><span data-stu-id="0304d-162">**NX_HTTP_SERVER_TIMEOUT_ACCEPT** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_server_socket_accept* calls.</span></span> <span data-ttu-id="0304d-163">Il valore predefinito è impostato su (10 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="0304d-163">The default value is set to (10 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="0304d-164">**NX_HTTP_SERVER_TIMEOUT_DISCONNECT** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_disconnect* .</span><span class="sxs-lookup"><span data-stu-id="0304d-164">**NX_HTTP_SERVER_TIMEOUT_DISCONNECT** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_disconnect* calls.</span></span> <span data-ttu-id="0304d-165">Il valore predefinito è impostato su 10 secondi (10 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="0304d-165">The default value is set to 10 seconds (10 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="0304d-166">**NX_HTTP_SERVER_TIMEOUT_RECEIVE** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_receive* .</span><span class="sxs-lookup"><span data-stu-id="0304d-166">**NX_HTTP_SERVER_TIMEOUT_RECEIVE** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_receive* calls.</span></span> <span data-ttu-id="0304d-167">Il valore predefinito è impostato su 10 secondi (10 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="0304d-167">The default value is set to 10 seconds (10 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="0304d-168">**NX_HTTP_SERVER_TIMEOUT_SEND** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_send* .</span><span class="sxs-lookup"><span data-stu-id="0304d-168">**NX_HTTP_SERVER_TIMEOUT_SEND** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_send* calls.</span></span> <span data-ttu-id="0304d-169">Il valore predefinito è impostato su 10 secondi (10 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="0304d-169">The default value is set to 10 seconds (10 \* NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="0304d-170">**NX_HTTP_MAX_HEADER_FIELD** Specifica la dimensione massima del campo dell'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="0304d-170">**NX_HTTP_MAX_HEADER_FIELD** Specifies the maximum size of the HTTP header field.</span></span> <span data-ttu-id="0304d-171">Il valore predefinito è 256.</span><span class="sxs-lookup"><span data-stu-id="0304d-171">The default value is 256.</span></span>
- <span data-ttu-id="0304d-172">**NX_HTTP_MULTIPART_ENABLE** Se definito, Abilita il server HTTP per supportare le richieste HTTP multipart.</span><span class="sxs-lookup"><span data-stu-id="0304d-172">**NX_HTTP_MULTIPART_ENABLE** If defined, enables HTTP Server to support multipart HTTP requests.</span></span>
- <span data-ttu-id="0304d-173">**NX_HTTP_SERVER_MAX_PENDING** Specifica il numero di connessioni che possono essere accodate per il server HTTP.</span><span class="sxs-lookup"><span data-stu-id="0304d-173">**NX_HTTP_SERVER_MAX_PENDING** Specifies the number of connections that can be queued for the HTTP Server.</span></span> <span data-ttu-id="0304d-174">Il valore predefinito è impostato su 5.</span><span class="sxs-lookup"><span data-stu-id="0304d-174">The default value is set to 5.</span></span>
- <span data-ttu-id="0304d-175">**NX_HTTP_MAX_RESOURCE** Specifica il numero di byte consentiti in un *nome di risorsa* fornito dal client.</span><span class="sxs-lookup"><span data-stu-id="0304d-175">**NX_HTTP_MAX_RESOURCE** Specifies the number of bytes allowed in a client supplied *resource name*.</span></span> <span data-ttu-id="0304d-176">Il valore predefinito è impostato su 40.</span><span class="sxs-lookup"><span data-stu-id="0304d-176">The default value is set to 40.</span></span>
- <span data-ttu-id="0304d-177">**NX_HTTP_MAX_NAME** Specifica il numero di byte consentiti in un *nome utente* fornito dal client.</span><span class="sxs-lookup"><span data-stu-id="0304d-177">**NX_HTTP_MAX_NAME** Specifies the number of bytes allowed in a client supplied *username*.</span></span> <span data-ttu-id="0304d-178">Il valore predefinito è impostato su 20.</span><span class="sxs-lookup"><span data-stu-id="0304d-178">The default value is set to 20.</span></span>
- <span data-ttu-id="0304d-179">**NX_HTTP_MAX_PASSWORD** Specifica il numero di byte consentiti in una *password* fornita dal client.</span><span class="sxs-lookup"><span data-stu-id="0304d-179">**NX_HTTP_MAX_PASSWORD** Specifies the number of bytes allowed in a client supplied *password*.</span></span> <span data-ttu-id="0304d-180">Il valore predefinito è impostato su 20.</span><span class="sxs-lookup"><span data-stu-id="0304d-180">The default value is set to 20.</span></span>
- <span data-ttu-id="0304d-181">**NX_HTTP_SERVER_MIN_PACKET_SIZE** Specifica la dimensione minima dei pacchetti nel pool specificato al momento della creazione del server.</span><span class="sxs-lookup"><span data-stu-id="0304d-181">**NX_HTTP_SERVER_MIN_PACKET_SIZE** Specifies the minimum size of the packets in the pool specified at Server creation.</span></span> <span data-ttu-id="0304d-182">La dimensione minima è necessaria per garantire che l'intestazione HTTP completa possa essere contenuta in un unico pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0304d-182">The minimum size is needed to ensure the complete HTTP header can be contained in one packet.</span></span> <span data-ttu-id="0304d-183">Il valore predefinito è impostato su 600.</span><span class="sxs-lookup"><span data-stu-id="0304d-183">The default value is set to 600.</span></span>
- <span data-ttu-id="0304d-184">**NX_HTTP_CLIENT_MIN_PACKET_SIZE** Specifica la dimensione minima dei pacchetti nel pool specificato durante la creazione del client.</span><span class="sxs-lookup"><span data-stu-id="0304d-184">**NX_HTTP_CLIENT_MIN_PACKET_SIZE** Specifies the minimum size of the packets in the pool specified at Client creation.</span></span> <span data-ttu-id="0304d-185">La dimensione minima è necessaria per garantire che l'intestazione HTTP completa possa essere contenuta in un unico pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0304d-185">The minimum size is needed to ensure the complete HTTP header can be contained in one packet.</span></span> <span data-ttu-id="0304d-186">Il valore predefinito è impostato su 300.</span><span class="sxs-lookup"><span data-stu-id="0304d-186">The default value is set to 300.</span></span>
- <span data-ttu-id="0304d-187">**NX_HTTP_SERVER_RETRY_SECONDS** *impostare il timeout di ritrasmissione del socket del server in secondi. Il* valore predefinito è impostato su 2.</span><span class="sxs-lookup"><span data-stu-id="0304d-187">**NX_HTTP_SERVER_RETRY_SECONDS** *Set the Server socket retransmission timeout in seconds. The* default value is set to 2.</span></span>
- <span data-ttu-id="0304d-188">**NX_HTTP_SERVER_RETRY_MAX** Questo consente di impostare il numero massimo di ritrasmissioni sul socket del server.</span><span class="sxs-lookup"><span data-stu-id="0304d-188">**NX_HTTP_SERVER_RETRY_MAX** This sets the maximum number of retransmissions on Server socket.</span></span> <span data-ttu-id="0304d-189">Il valore predefinito è impostato su 10.</span><span class="sxs-lookup"><span data-stu-id="0304d-189">The default value is set to 10.</span></span>
- <span data-ttu-id="0304d-190">**NX_HTTP_SERVER_RETRY_SHIFT** Questo valore viene utilizzato per impostare il timeout di ritrasmissione successivo.</span><span class="sxs-lookup"><span data-stu-id="0304d-190">**NX_HTTP_SERVER_RETRY_SHIFT** This value is used to set the next retransmission timeout.</span></span> <span data-ttu-id="0304d-191">Il timeout corrente viene moltiplicato per il numero di ritrasmissioni fino a questo punto, spostate in base al valore del turno di timeout del socket.</span><span class="sxs-lookup"><span data-stu-id="0304d-191">The current timeout is multiplied by the number of retransmissions thus far, shifted by the value of the socket timeout shift.</span></span> <span data-ttu-id="0304d-192">Il valore predefinito è impostato su 1 per raddoppiare il timeout.</span><span class="sxs-lookup"><span data-stu-id="0304d-192">The default value is set to 1 for doubling the timeout.</span></span>
- <span data-ttu-id="0304d-193">**NX_HTTP_ SERVER_TRANSMIT_QUEUE_DEPTH** Specifica il numero massimo di pacchetti che possono essere accodati nella coda di ritrasmissione del socket server.</span><span class="sxs-lookup"><span data-stu-id="0304d-193">**NX_HTTP_ SERVER_TRANSMIT_QUEUE_DEPTH** This specifies the maximum number of packets that can be enqueued on the Server socket retransmission queue.</span></span> <span data-ttu-id="0304d-194">Se il numero di pacchetti accodati raggiunge questo numero, non sarà più possibile inviare pacchetti fino a quando non vengono rilasciati uno o più pacchetti accodati.</span><span class="sxs-lookup"><span data-stu-id="0304d-194">If the number of packets enqueued reaches this number, no more packets can be sent until one or more enqueued packets are released.</span></span> <span data-ttu-id="0304d-195">Il valore predefinito è impostato su 20.</span><span class="sxs-lookup"><span data-stu-id="0304d-195">The default value is set to 20.</span></span>