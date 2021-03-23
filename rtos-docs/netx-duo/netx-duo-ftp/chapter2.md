---
title: Capitolo 2-installazione e uso di FTP
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo dei servizi FTP NetX Duo.
author: philmea
ms.author: philmea
ms.date: 07/14/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ac58658af93f59556d99d340ae38570908d63fc1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821881"
---
# <a name="chapter-2---installation-and-use-of-ftp"></a><span data-ttu-id="deb0d-103">Capitolo 2-installazione e uso di FTP</span><span class="sxs-lookup"><span data-stu-id="deb0d-103">Chapter 2 - Installation and use of FTP</span></span>

<span data-ttu-id="deb0d-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo dei servizi FTP NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="deb0d-104">This chapter contains a description of various issues related to installation, set up, and usage of the NetX Duo FTP services.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="deb0d-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="deb0d-105">Product Distribution</span></span>

<span data-ttu-id="deb0d-106">NetX Duo FTP è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="deb0d-106">NetX Duo FTP is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="deb0d-107">Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="deb0d-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="deb0d-108">**nxd_ftp_client. h** File di intestazione per il client FTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="deb0d-108">**nxd_ftp_client.h** Header file for NetX Duo FTP Client</span></span>
- <span data-ttu-id="deb0d-109">**nxd_ftp_client. c** File di origine C per il client FTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="deb0d-109">**nxd_ftp_client.c** C Source file for NetX Duo FTP Client</span></span>
- <span data-ttu-id="deb0d-110">**nxd_ftp_server. h** File di intestazione per il server FTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="deb0d-110">**nxd_ftp_server.h** Header file for NetX Duo FTP Server</span></span>
- <span data-ttu-id="deb0d-111">**nxd_ftp_server. c** File di origine C per il server FTP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="deb0d-111">**nxd_ftp_server.c** C Source file for NetX Duo FTP Server</span></span>
- <span data-ttu-id="deb0d-112">**filex_stub. h** File stub se FileX non è presente</span><span class="sxs-lookup"><span data-stu-id="deb0d-112">**filex_stub.h** Stub file if FileX is not present</span></span>
- <span data-ttu-id="deb0d-113">**nxd_ftp.pdf** Descrizione PDF di FTP per NetX Duo</span><span class="sxs-lookup"><span data-stu-id="deb0d-113">**nxd_ftp.pdf** PDF description of FTP for NetX Duo</span></span>
- <span data-ttu-id="deb0d-114">**demo_netxduo_ftp. c** Sistema di dimostrazione FTP</span><span class="sxs-lookup"><span data-stu-id="deb0d-114">**demo_netxduo_ftp.c** FTP demonstration system</span></span>

## <a name="netx-duo-ftp-installation"></a><span data-ttu-id="deb0d-115">Installazione FTP di NetX Duo</span><span class="sxs-lookup"><span data-stu-id="deb0d-115">NetX Duo FTP Installation</span></span>

<span data-ttu-id="deb0d-116">Per poter usare l'API FTP NetX Duo, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="deb0d-116">In order to use the NetX Duo FTP API, the entire distribution mentioned previously should be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="deb0d-117">Se, ad esempio, NetX Duo è installato nella directory "*\threadx\arm7\green*", il *nxd_ftp_client. h* e *nxd_ftp_client. c* devono essere copiati in questa directory per le applicazioni client FTP e i file *nxd_ftp_server. h* e *nxd_ftp_server. c* devono essere copiati in questa directory per le applicazioni server FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-117">For example, if NetX Duo is installed in the directory “*\threadx\arm7\green*” then the *nxd_ftp_client.h* and *nxd_ftp_client.c* should be copied into this directory for FTP Client applications, and *nxd_ftp_server.h* and *nxd_ftp_server.c* files should be copied into this directory for FTP Server applications.</span></span>

## <a name="using-netx-duo-ftp"></a><span data-ttu-id="deb0d-118">Uso di NetX Duo FTP</span><span class="sxs-lookup"><span data-stu-id="deb0d-118">Using NetX Duo FTP</span></span>

<span data-ttu-id="deb0d-119">L'uso dell'API FTP NetX Duo è facile.</span><span class="sxs-lookup"><span data-stu-id="deb0d-119">Using the NetX Duo FTP API is easy.</span></span> <span data-ttu-id="deb0d-120">In pratica, il codice dell'applicazione deve includere *nxd_ftp_client. h* per le applicazioni client ftp o *nxd_ftp_server* per le applicazioni server FTP, dopo aver incluso *tx_api. h, fx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX, FILEX e NETX Duo.</span><span class="sxs-lookup"><span data-stu-id="deb0d-120">Basically, the application code must include either *nxd_ftp_client.h* for FTP Client applications or *nxd_ftp_server* for FTP Server applications, after it includes *tx_api.h, fx_api.h,* and *nx_api.h*, in order to use ThreadX, FileX, and NetX Duo, respectively.</span></span> <span data-ttu-id="deb0d-121">Il progetto di compilazione deve includere il codice sorgente FTP e il file dell'applicazione host e, naturalmente, i file di libreria ThreadX e NetX.</span><span class="sxs-lookup"><span data-stu-id="deb0d-121">The build project must include the FTP source code and the host application file, and of course the ThreadX and NetX library files.</span></span> <span data-ttu-id="deb0d-122">Questo è tutto ciò che è necessario per l'uso di NetX Duo FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-122">This is all that is required to use NetX Duo FTP.</span></span>

<span data-ttu-id="deb0d-123">Si noti che poiché FTP utilizza i servizi TCP NetX Duo, è necessario abilitare TCP con la chiamata *nx_tcp_enable* prima di utilizzare FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-123">Note that since FTP utilizes NetX Duo TCP services, TCP must be enabled with the *nx_tcp_enable* call prior to using FTP.</span></span>

<span data-ttu-id="deb0d-124">Si noti che la libreria NetX Duo può essere abilitata per IPv6 e che supporta ancora le reti IPv4.</span><span class="sxs-lookup"><span data-stu-id="deb0d-124">Note that the NetX Duo library can be enabled for IPv6 and still support IPv4 networks.</span></span> <span data-ttu-id="deb0d-125">Tuttavia, NetX Duo non supporta IPv6, a meno che non sia abilitato.</span><span class="sxs-lookup"><span data-stu-id="deb0d-125">However, NetX Duo cannot support IPv6 unless it is enabled.</span></span> <span data-ttu-id="deb0d-126">Per disabilitare l'elaborazione IPv6 in NetX Duo, è necessario definire il **NX_DISABLE_IPV6** nel file *nx_user. h* e tale file deve essere incluso nella compilazione della libreria NETX Duo definendo **NX_INCLUDE_USER_DEFINE_FILE** nel file *nx_port. h* .</span><span class="sxs-lookup"><span data-stu-id="deb0d-126">To disable IPv6 processing in NetX Duo, the **NX_DISABLE_IPV6** must be defined in the *nx_user.h* file, and that file must be included in the NetX Duo library build by defining **NX_INCLUDE_USER_DEFINE_FILE** in the *nx_port.h* file.</span></span> <span data-ttu-id="deb0d-127">Per impostazione predefinita, **NX_DISABLE_IPV6** non è definito (IPv6 è abilitato).</span><span class="sxs-lookup"><span data-stu-id="deb0d-127">By default, **NX_DISABLE_IPV6** is not defined (IPv6 is enabled).</span></span> <span data-ttu-id="deb0d-128">Si tratta di un servizio diverso da quello *nxd_ipv6_enable* che imposta i protocolli e i servizi IPv6 nell'attività IP e richiede che **NX_DISABLE_IPV6** non sia definito.</span><span class="sxs-lookup"><span data-stu-id="deb0d-128">This is different from the *nxd_ipv6_enable* service that sets up the IPv6 protocols and services on the IP task, and requires **NX_DISABLE_IPV6** to be not defined.</span></span>

## <a name="small-example-system-of-netx-duo-ftp"></a><span data-ttu-id="deb0d-129">Piccolo sistema di esempio di NetX Duo FTP</span><span class="sxs-lookup"><span data-stu-id="deb0d-129">Small Example System of NetX Duo FTP</span></span>

<span data-ttu-id="deb0d-130">Un esempio di come è facile usare NetX Duo FTP è descritto nella figura 1,1 riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="deb0d-130">An example of how easy it is to use NetX Duo FTP is described in Figure 1.1 that appears below.</span></span> <span data-ttu-id="deb0d-131">In questo esempio vengono creati sia un server FTP che un client FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-131">In this example, both an FTP Server and an FTP Client are created.</span></span> <span data-ttu-id="deb0d-132">Pertanto, entrambi i file di inclusione FTP *nxd_ftp_client. h e nxd_ftp_server. h vengono* portati in corrispondenza della riga 10 e 11.</span><span class="sxs-lookup"><span data-stu-id="deb0d-132">Therefore both FTP include files *nxd_ftp_client.h and nxd_ftp_server.h are* brought in at line 10 and 11.</span></span> <span data-ttu-id="deb0d-133">Successivamente, il server FTP viene creato in "*tx_application_define*" alla riga 99.</span><span class="sxs-lookup"><span data-stu-id="deb0d-133">Next, the FTP Server is created in “*tx_application_define*” at line 99.</span></span> <span data-ttu-id="deb0d-134">Si noti che il server FTP e i blocchi di controllo client sono definiti come variabili globali nella riga 26 precedente.</span><span class="sxs-lookup"><span data-stu-id="deb0d-134">Note that the FTP Server and Client control blocks are defined as global variables at line 26 previously.</span></span>

<span data-ttu-id="deb0d-135">Questa demo illustra come usare le funzioni Duo disponibili in NetX Duo FTP e nei servizi FTP limitati IPv4 legacy.</span><span class="sxs-lookup"><span data-stu-id="deb0d-135">This demo shows how to use the duo functions available in NetX Duo FTP as well as the legacy IPv4 limited FTP services.</span></span> <span data-ttu-id="deb0d-136">Per usare le funzioni IPv6, la demo definisce USE_IPV6 nella riga 16</span><span class="sxs-lookup"><span data-stu-id="deb0d-136">To use the IPv6 functions, the demo defines USE_IPV6 in line 16</span></span>

<span data-ttu-id="deb0d-137">Alla riga 162, il server FTP viene creato con \***nxd_ftp_server_create** _ se l'applicazione host definisce USE_IPV6 che supporta sia IPv4 che IPv6.</span><span class="sxs-lookup"><span data-stu-id="deb0d-137">At line 162 the FTP Server is created with \***nxd_ftp_server_create** _ if the host application defines USE_IPV6 which supports both IPv4 and IPv6.</span></span> <span data-ttu-id="deb0d-138">In caso contrario, il server FTP viene creato con _ *_nx_ftp_server_create_*\* alla riga 166 con il servizio limitato IPv4.</span><span class="sxs-lookup"><span data-stu-id="deb0d-138">If it is not, the FTP Server is created with _ *_nx_ftp_server_create_*\* on line 166 with the IPv4 limited service.</span></span> <span data-ttu-id="deb0d-139">Si noti che la funzione ' Duo ' utilizza diversi argomenti della funzione di accesso e disconnessione rispetto al servizio IPv4, entrambi definiti nella parte inferiore del file nelle righe 534-568.</span><span class="sxs-lookup"><span data-stu-id="deb0d-139">Note that the ‘duo’ function uses different login and logout function arguments than the IPv4 service, both of which are defined at the bottom of the file on lines 534 -568.</span></span>

<span data-ttu-id="deb0d-140">Il server FTP deve quindi stabilire l'indirizzo IPv6 (globale e collegamento locale) con NetX Duo, a partire dalla riga 466 nella funzione di immissione thread del server FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-140">The FTP server must then establish its IPv6 address (global and link local) with NetX Duo, starting at line 466 in the FTP server thread entry function.</span></span> <span data-ttu-id="deb0d-141">Il server FTP viene quindi avviato alla riga 518 ed è pronto per le richieste client FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-141">The FTP server is then started on line 518 and is ready for FTP client requests.</span></span>

<span data-ttu-id="deb0d-142">Il client FTP viene creato alla riga 316 e passa attraverso lo stesso processo del server FTP per ottenere l'attività IP del client FTP abilitata per IPv6 e i relativi indirizzi IPv6 convalidati a partire dalle righe 263-313.</span><span class="sxs-lookup"><span data-stu-id="deb0d-142">The FTP Client is created in line 316 and goes through the same process as the FTP Server to get the FTP Client IP task IPv6 enabled, and its IPv6 addresses validated starting on lines 263-313.</span></span>

<span data-ttu-id="deb0d-143">Il client si connette quindi al server FTP usando \***nxd_ftp_client_connect** _ nella riga 334 se è stato definito USE_IPV6 o la riga 340 se usa il servizio limitato IPv4 _ *_nx_ftp_client_connect_* \*.</span><span class="sxs-lookup"><span data-stu-id="deb0d-143">Then the Client connects to the FTP Server using ***nxd_ftp_client_connect** _ in line 334 if it has defined USE_IPV6, or line 340 if it is using the IPv4 limited service _*_nx_ftp_client_connect_\*\*.</span></span> <span data-ttu-id="deb0d-144">Nel corso della funzione thread client FTP, scrive un file nel server FTP e lo legge prima della disconnessione.</span><span class="sxs-lookup"><span data-stu-id="deb0d-144">Over the course of the FTP Client thread function, it writes a file to the FTP server and reads it back before disconnecting.</span></span>

```C
/* This is a small demo of NetX FTP on the high-performance NetX TCP/IP stack.  This demo
   relies on ThreadX, NetX, and FileX to show a simple file transfer from the client
   and then back to the server.  */



#include    "tx_api.h"
#include    "fx_api.h"
#include    "nx_api.h"
#include    "nxd_ftp_client.h"
#include    "nxd_ftp_server.h"

#define     DEMO_STACK_SIZE         4096

#ifdef FEATURE_NX_IPV6
#define USE_IPV6
#endif /* FEATURE_NX_IPV6 */


/* Define the ThreadX, NetX, and FileX object control blocks...  */

TX_THREAD               server_thread;
TX_THREAD               client_thread;
NX_PACKET_POOL          server_pool;
NX_IP                   server_ip;
NX_PACKET_POOL          client_pool;
NX_IP                   client_ip;
FX_MEDIA                ram_disk;


/* Define the NetX FTP object control blocks.  */

NX_FTP_CLIENT           ftp_client;
NX_FTP_SERVER           ftp_server;


/* Define the counters used in the demo application...  */

ULONG                   error_counter = 0;


/* Define the memory area for the FileX RAM disk.  */

UCHAR                   ram_disk_memory[32000];
UCHAR                   ram_disk_sector_cache[512];


#define FTP_SERVER_ADDRESS  IP_ADDRESS(1,2,3,4)
#define FTP_CLIENT_ADDRESS  IP_ADDRESS(1,2,3,5)

extern UINT  _fx_media_format(FX_MEDIA *media_ptr, VOID (*driver)(FX_MEDIA *media),
                        VOID *driver_info_ptr, UCHAR *memory_ptr, UINT memory_size,
                        CHAR *volume_name, UINT number_of_fats, UINT directory_entries,
                        UINT hidden_sectors, ULONG total_sectors, UINT bytes_per_sector,
                        UINT sectors_per_cluster, UINT heads, UINT sectors_per_track);

/* Define the FileX and NetX driver entry functions.  */
VOID    _fx_ram_driver(FX_MEDIA *media_ptr);

/* Replace the 'ram' driver with your own Ethernet driver. */
VOID    _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);


void    client_thread_entry(ULONG thread_input);
void    thread_server_entry(ULONG thread_input);


#ifdef USE_IPV6
/* Define NetX Duo IP address for the NetX Duo FTP Server and Client. */
NXD_ADDRESS     server_ip_address;
NXD_ADDRESS     client_ip_address;
endif


/* Define server login/logout functions.  These are stubs for functions that would
   validate a client login request.   */

#ifdef USE_IPV6
UINT    server_login6(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr, NXD_ADDRESS *client_ipduo_address,
    UINT client_port, CHAR *name, CHAR *password, CHAR *extra_info);
UINT    server_logout6(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr, NXD_ADDRESS *client_ipduo_address,
    UINT client_port, CHAR *name, CHAR *password, CHAR *extra_info);
#else
UINT    server_login(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
    ULONG client_ip_address, UINT client_port,
    CHAR *name, CHAR *password, CHAR *extra_info);
UINT    server_logout(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
    ULONG client_ip_address, UINT client_port,
    CHAR *name, CHAR *password, CHAR *extra_info);
#endif


/* Define main entry point.  */

int main()
{

    /* Enter the ThreadX kernel.  */
    tx_kernel_enter();
    return(0);
}


/* Define what the initial system looks like.  */

void    tx_application_define(void *first_unused_memory)
{

    UINT    status;
    UCHAR   *pointer;


    /* Setup the working pointer.  */
    pointer =  (UCHAR *) first_unused_memory;

    /* Create a helper thread for the server. */
    tx_thread_create(&server_thread, "FTP Server thread", thread_server_entry, 0,
                     pointer, DEMO_STACK_SIZE,
                     4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize NetX.  */
    nx_system_initialize();

    /* Create the packet pool for the FTP Server.  */
    status = nx_packet_pool_create(&server_pool, "NetX Server Packet Pool", 256, pointer, 8192);
    pointer = pointer + 8192;

    /* Check for errors.  */
    if (status)
        error_counter++;

    /* Create the IP instance for the FTP Server.  */
    status = nx_ip_create(&server_ip, "NetX Server IP Instance", FTP_SERVER_ADDRESS, 0xFFFFFF00UL,
                                        &server_pool, _nx_ram_network_driver, pointer, 2048, 1);
    pointer = pointer + 2048;

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Enable ARP and supply ARP cache memory for server IP instance.  */
    nx_arp_enable(&server_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Enable TCP.  */
    nx_tcp_enable(&server_ip);

#ifdef USE_IPV6

    /* Next set the NetX Duo FTP Server and Client addresses. */
    server_ip_address.nxd_ip_address.v6[3] = 0x105;
    server_ip_address.nxd_ip_address.v6[2] = 0x0;
    server_ip_address.nxd_ip_address.v6[1] = 0x0000f101;
    server_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    server_ip_address.nxd_ip_version = NX_IP_VERSION_V6;

    client_ip_address.nxd_ip_address.v6[3] = 0x101;
    client_ip_address.nxd_ip_address.v6[2] = 0x0;
    client_ip_address.nxd_ip_address.v6[1] = 0x0000f101;
    client_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    client_ip_address.nxd_ip_version = NX_IP_VERSION_V6;

    /* Create the FTP server.  */
    status =  nxd_ftp_server_create(&ftp_server, "FTP Server Instance", &server_ip,
                                    &ram_disk, pointer, DEMO_STACK_SIZE, &server_pool,
                                    server_login6, server_logout6);
#else
    /* Create the FTP server.  */
    status =  nx_ftp_server_create(&ftp_server, "FTP Server Instance", &server_ip,
                                    &ram_disk, pointer, DEMO_STACK_SIZE, &server_pool,
                                    server_login, server_logout);
#endif
    pointer =  pointer + DEMO_STACK_SIZE;

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Now set up the FTP Client. */

    /* Create the main FTP client thread.  */
    status = tx_thread_create(&client_thread, "FTP Client thread ", client_thread_entry, 0,
            pointer, DEMO_STACK_SIZE,
            6, 6, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer = pointer + DEMO_STACK_SIZE ;

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Create a packet pool for the FTP client.  */
    status =  nx_packet_pool_create(&client_pool, "NetX Client Packet Pool", 256, pointer, 8192);
    pointer =  pointer + 8192;

    /* Create an IP instance for the FTP client.  */
    status = nx_ip_create(&client_ip, "NetX Client IP Instance", FTP_CLIENT_ADDRESS, 0xFFFFFF00UL,
                                                &client_pool, _nx_ram_network_driver, pointer, 2048, 1);
    pointer = pointer + 2048;

    /* Enable ARP and supply ARP cache memory for the FTP Client IP.  */
    nx_arp_enable(&client_ip, (void *) pointer, 1024);

    pointer = pointer + 1024;

    /* Enable TCP for client IP instance.  */
    nx_tcp_enable(&client_ip);

    return;

}

/* Define the FTP client thread.  */

void    client_thread_entry(ULONG thread_input)
{

NX_PACKET   *my_packet;
UINT        status;

#ifdef USE_IPV6
UINT        iface_index, address_index;
#endif


    /* Format the RAM disk - the memory for the RAM disk was defined above.  */
    status = _fx_media_format(&ram_disk,
                            _fx_ram_driver,                  /* Driver entry                */
                            ram_disk_memory,                 /* RAM disk memory pointer     */
                            ram_disk_sector_cache,           /* Media buffer pointer        */
                            sizeof(ram_disk_sector_cache),   /* Media buffer size           */
                            "MY_RAM_DISK",                   /* Volume Name                 */
                            1,                               /* Number of FATs              */
                            32,                              /* Directory Entries           */
                            0,                               /* Hidden sectors              */
                            256,                             /* Total sectors               */
                            128,                             /* Sector size                 */
                            1,                               /* Sectors per cluster         */
                            1,                               /* Heads                       */
                            1);                              /* Sectors per track           */

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Open the RAM disk.  */
    status = fx_media_open(&ram_disk, "RAM DISK", _fx_ram_driver, ram_disk_memory,
        ram_disk_sector_cache, sizeof(ram_disk_sector_cache));

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Let the IP threads and driver initialize the system.    */
    tx_thread_sleep(100);

#ifdef USE_IPV6

    /* Here's where we make the FTP Client IPv6 enabled. */
    status = nxd_ipv6_enable(&client_ip);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    status = nxd_icmp_enable(&client_ip);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Set the Client link local and global addresses. */
    iface_index = 0;

    /* This assumes we are using the primary network interface (index 0). */
    status = nxd_ipv6_address_set(&client_ip, iface_index, NX_NULL, 10, &address_index);

    /* Check for link local address set error.  */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
     }

     /* Set the host global IP address. We are assuming a 64
       bit prefix here but this can be any value (< 128). */
    status = nxd_ipv6_address_set(&client_ip, iface_index, &client_ip_address, 64, &address_index);

    /* Check for global address set error.  */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
     }

    /* Let NetX Duo validate the addresses. */
    tx_thread_sleep(400);

#endif  /* USE_IPV6 */

    /* Create an FTP client.  */
    status =  nx_ftp_client_create(&ftp_client, "FTP Client", &client_ip, 2000, &client_pool);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
     }

    printf("Created the FTP Client\n");

#ifdef USE_IPV6

    do
    {

        /* Now connect with the NetX Duo FTP (IPv6) server. */
        status =  nxd_ftp_client_connect(&ftp_client, &server_ip_address, "name", "password", 100);
    } while (status != NX_SUCCESS);

#else

    /* Now connect with the NetX FTP (IPv4) server. */
    status =  nx_ftp_client_connect(&ftp_client, FTP_SERVER_ADDRESS, "name", "password", 100);

#endif  /* USE_IPV6 */

    /* Check status.  */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
     }

    printf("Connected to the FTP Server\n");

    /* Open a FTP file for writing.  */
    status =  nx_ftp_client_file_open(&ftp_client, "test.txt", NX_FTP_OPEN_FOR_WRITE, 100);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
     }

    printf("Opened the FTP client test.txt file\n");

    /* Allocate a FTP packet.  */
    status =  nx_packet_allocate(&client_pool, &my_packet, NX_TCP_PACKET, 100);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
     }

    /* Write ABCs into the packet payload!  */
    memcpy(my_packet -> nx_packet_prepend_ptr, "ABCDEFGHIJKLMNOPQRSTUVWXYZ  ", 28);

    /* Adjust the write pointer.  */
    my_packet -> nx_packet_length =  28;
    my_packet -> nx_packet_append_ptr =  my_packet -> nx_packet_prepend_ptr + 28;

    /* Write the packet to the file test.txt.  */
    status =  nx_ftp_client_file_write(&ftp_client, my_packet, 100);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
        printf("Wrote to the FTP client test.txt file\n");


    /* Close the file.  */
    status =  nx_ftp_client_file_close(&ftp_client, 100);

    /* Check status.  */
    if (status != NX_SUCCESS)
        error_counter++;
    else
        printf("Closed the FTP client test.txt file\n");


    /* Now open the same file for reading.  */
    status =  nx_ftp_client_file_open(&ftp_client, "test.txt", NX_FTP_OPEN_FOR_READ, 100);

    /* Check status.  */
    if (status != NX_SUCCESS)
        error_counter++;
    else
        printf("Reopened the FTP client test.txt file\n");

    /* Read the file.  */
    status =  nx_ftp_client_file_read(&ftp_client, &my_packet, 100);

    /* Check status.  */
    if (status != NX_SUCCESS)
        error_counter++;
    else
    {
            printf("Reread the FTP client test.txt file\n");
            nx_packet_release(my_packet);
    }

    /* Close this file.  */
    status =  nx_ftp_client_file_close(&ftp_client, 100);

    if (status != NX_SUCCESS)
        error_counter++;

    /* Disconnect from the server.  */
    status =  nx_ftp_client_disconnect(&ftp_client, 100);

    /* Check status.  */
    if (status != NX_SUCCESS)
        error_counter++;


    /* Delete the FTP client.  */
    status =  nx_ftp_client_delete(&ftp_client);

    /* Check status.  */
    if (status != NX_SUCCESS)
        error_counter++;
}


/* Define the helper FTP server thread.  */
void    thread_server_entry(ULONG thread_input)
{

    UINT            status;
#ifdef  USE_IPV6
    UINT            iface_index, address_index;
#endif

    /* Wait till the IP thread and driver have initialized the system. */
    tx_thread_sleep(100);

#ifdef USE_IPV6

    /* Here's where we make the FTP server IPv6 enabled. */
    status = nxd_ipv6_enable(&server_ip);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
     }

    status = nxd_icmp_enable(&server_ip);

    /* Check status.  */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
     }

     /* Set the link local address with the host MAC address. */
    iface_index = 0;

    /* This assumes we are using the primary network interface (index 0). */
    status = nxd_ipv6_address_set(&server_ip, iface_index, NX_NULL, 10, &address_index);

    /* Check for link local address set error.  */
    if (status)
    {

        error_counter++;
        return;
     }

    /* Set the host global IP address. We are assuming a 64
       bit prefix here but this can be any value (< 128). */
    status = nxd_ipv6_address_set(&server_ip, iface_index, &server_ip_address, 64, &address_index);

    /* Check for global address set error.  */
    if (status)
    {

        error_counter++;
        return;
     }

    /* Wait while NetX Duo validates the link local and global address. */
    tx_thread_sleep(500);

#endif /* USE_IPV6 */

    /* OK to start the FTP Server.   */
    status = nx_ftp_server_start(&ftp_server);

    if (status != NX_SUCCESS)
        error_counter++;

    printf("Server started!\n");

    /* FTP server ready to take requests! */

    /* Let the IP threads execute.    */
    tx_thread_relinquish();

    return;
}


#ifdef USE_IPV6
UINT  server_login6(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
                    NXD_ADDRESS *client_ipduo_address, UINT client_port,
                    CHAR *name, CHAR *password, CHAR *extra_info)
{
    printf("Logged in6!\n");

    /* Always return success.  */
    return(NX_SUCCESS);
}

UINT  server_logout6(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr, NXD_ADDRESS *client_ipduo_address,
                     UINT client_port, CHAR *name, CHAR *password, CHAR *extra_info)
{
    printf("Logged out6!\n");

    /* Always return success.  */
    return(NX_SUCCESS);
}
#else
UINT  server_login(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr, ULONG client_ip_address,
                    UINT client_port, CHAR *name, CHAR *password, CHAR *extra_info)
{

    printf("Logged in!\n");
    /* Always return success.  */
    return(NX_SUCCESS);
}

UINT  server_logout(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr, ULONG client_ip_address,
                    UINT client_port, CHAR *name, CHAR *password, CHAR *extra_info)
{
    printf("Logged out!\n");

    /* Always return success.  */
    return(NX_SUCCESS);
}
#endif  /* USE_IPV6 */
```

<span data-ttu-id="deb0d-145">**Figura 1,1 esempio di FTP NetX Duo**</span><span class="sxs-lookup"><span data-stu-id="deb0d-145">**Figure 1.1 Example of NetX Duo FTP**</span></span>

## <a name="configuration-options"></a><span data-ttu-id="deb0d-146">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="deb0d-146">Configuration Options</span></span>

<span data-ttu-id="deb0d-147">Sono disponibili diverse opzioni di configurazione per la compilazione di FTP NetX e NetX Duo FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-147">There are several configuration options for building NetX FTP and NetX Duo FTP.</span></span> <span data-ttu-id="deb0d-148">Sono elencati i valori predefiniti, ma ogni definizione può essere impostata dal</span><span class="sxs-lookup"><span data-stu-id="deb0d-148">The default values are listed, but each define can be set by the</span></span>

<span data-ttu-id="deb0d-149">applicazione prima dell'inclusione del file di intestazione FTP NetX Duo specificato.</span><span class="sxs-lookup"><span data-stu-id="deb0d-149">application prior to inclusion of the specified NetX Duo FTP header file.</span></span> <span data-ttu-id="deb0d-150">Se non viene specificato alcun file di intestazione, l'opzione è disponibile sia in *nxd_ftp_client. h che in nxd_ftp_server. h*.</span><span class="sxs-lookup"><span data-stu-id="deb0d-150">If no header file is specified, the option is available in both *nxd_ftp_client.h and nxd_ftp_server.h*.</span></span> <span data-ttu-id="deb0d-151">L'elenco seguente descrive tutti i dettagli:</span><span class="sxs-lookup"><span data-stu-id="deb0d-151">The following list describes each in detail:</span></span>

- <span data-ttu-id="deb0d-152">**NX_FTP_SERVER_PRIORITY** Priorità del thread del server FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-152">**NX_FTP_SERVER_PRIORITY** The priority of the FTP Server thread.</span></span> <span data-ttu-id="deb0d-153">Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.</span><span class="sxs-lookup"><span data-stu-id="deb0d-153">By default, this value is defined as 16 to specify priority 16.</span></span>
- <span data-ttu-id="deb0d-154">**NX_FTP_MAX_CLIENTS** Il numero massimo di client che il server è in grado di gestire in una sola volta.</span><span class="sxs-lookup"><span data-stu-id="deb0d-154">**NX_FTP_MAX_CLIENTS** The maximum number of Clients the Server can handle at one time.</span></span> <span data-ttu-id="deb0d-155">Per impostazione predefinita, questo valore è 4 per supportare contemporaneamente 4 client.</span><span class="sxs-lookup"><span data-stu-id="deb0d-155">By default, this value is 4 to support 4 Clients at once.</span></span>
- <span data-ttu-id="deb0d-156">**NX_FTP_SERVER_MIN_PACKET_PAYLOAD** Dimensioni minime del payload del pool di pacchetti server in byte, incluse le intestazioni TCP, IP e frame di rete oltre ai dati HTTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-156">**NX_FTP_SERVER_MIN_PACKET_PAYLOAD** The minimum size of the Server packet pool payload in bytes, including TCP, IP and network frame headers plus HTTP data.</span></span> <span data-ttu-id="deb0d-157">Il valore predefinito è 256 (lunghezza massima del nome file in FileX) + 12 byte per le informazioni sui file e NX_PHYSICAL_TRAILER.</span><span class="sxs-lookup"><span data-stu-id="deb0d-157">The default value is 256 (maximum length of filename in FileX) + 12 bytes for file information, and NX_PHYSICAL_TRAILER.</span></span>
- <span data-ttu-id="deb0d-158">**NX_FTP_SERVER_TIMEOUT** Consente di specificare il numero di cicli ThreadX per i quali i servizi interni sospendono.</span><span class="sxs-lookup"><span data-stu-id="deb0d-158">**NX_FTP_SERVER_TIMEOUT** Specifies the number of ThreadX  ticks that internal services will  suspend for.</span></span> <span data-ttu-id="deb0d-159">Il valore predefinito è impostato su 1 secondo (1 \* NX_IP_PERIODIC_RATE).</span><span class="sxs-lookup"><span data-stu-id="deb0d-159">The default value  is set to 1 second (1 \*  NX_IP_PERIODIC_RATE).</span></span>
- <span data-ttu-id="deb0d-160">**NX_FTP_ACTIVITY_TIMEOUT** Specifica il numero di secondi per cui una connessione client viene mantenuta in assenza di attività.</span><span class="sxs-lookup"><span data-stu-id="deb0d-160">**NX_FTP_ACTIVITY_TIMEOUT** Specifies the number of seconds  a Client connection is maintained  if there is no activity.</span></span> <span data-ttu-id="deb0d-161">Il valore predefinito è impostato su 240.</span><span class="sxs-lookup"><span data-stu-id="deb0d-161">The default  value is set to 240.</span></span>
- <span data-ttu-id="deb0d-162">**NX_FTP_TIMEOUT_PERIOD** Specifica gli intervalli in secondi durante i quali il server verifica l'attività del client.</span><span class="sxs-lookup"><span data-stu-id="deb0d-162">**NX_FTP_TIMEOUT_PERIOD** Specifies the intervals in seconds  when the Server checks for  Client activity.</span></span> <span data-ttu-id="deb0d-163">Il valore predefinito è impostato su 60.</span><span class="sxs-lookup"><span data-stu-id="deb0d-163">The default value is set to 60.</span></span>
- <span data-ttu-id="deb0d-164">**NX_FTP_SERVER_RETRY_SECONDS** Specifica il timeout iniziale in secondi prima della ritrasmissione della risposta del server.</span><span class="sxs-lookup"><span data-stu-id="deb0d-164">**NX_FTP_SERVER_RETRY_SECONDS** Specifies the initial timeout in seconds before retransmitting server response.</span></span> <span data-ttu-id="deb0d-165">Il valore predefinito è 2.</span><span class="sxs-lookup"><span data-stu-id="deb0d-165">The default value is 2.</span></span>
- <span data-ttu-id="deb0d-166">**NX_FTP_SERVER_TRANSMIT_QUEUE_DEPTH** Specifica il livello massimo di profondità dei pacchetti di trasmissione in coda nel socket del server.</span><span class="sxs-lookup"><span data-stu-id="deb0d-166">**NX_FTP_SERVER_TRANSMIT_QUEUE_DEPTH** Specifies the maximum of depth of queued transmit packets on Server socket.</span></span> <span data-ttu-id="deb0d-167">Il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="deb0d-167">The default value is 20.</span></span>
- <span data-ttu-id="deb0d-168">**NX_FTP_SERVER_RETRY_MAX** Specifica il numero massimo di tentativi per pacchetto.</span><span class="sxs-lookup"><span data-stu-id="deb0d-168">**NX_FTP_SERVER_RETRY_MAX** Specifies the maximum retries per packet.</span></span> <span data-ttu-id="deb0d-169">Il valore predefinito è 10.</span><span class="sxs-lookup"><span data-stu-id="deb0d-169">The default value is 10.</span></span>
- <span data-ttu-id="deb0d-170">**NX_FTP_SERVER_RETRY_SHIFT** Specifica il numero di bit da spostare nell'impostazione del timeout di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="deb0d-170">**NX_FTP_SERVER_RETRY_SHIFT** Specifies the number of bits to shift in setting the retry timeout.</span></span> <span data-ttu-id="deb0d-171">Il valore predefinito è 2, ad esempio ogni timeout di ripetizione dei tentativi è due volte più lungo del tentativo precedente.</span><span class="sxs-lookup"><span data-stu-id="deb0d-171">The default value is 2, e.g. every retry timeout is twice as long as the previous retry.</span></span>
- <span data-ttu-id="deb0d-172">**NX_FTP_NO_FILEX** Definito, questa opzione fornisce uno stub per le dipendenze FileX.</span><span class="sxs-lookup"><span data-stu-id="deb0d-172">**NX_FTP_NO_FILEX** Defined, this option provides a  stub for FileX dependencies.</span></span> <span data-ttu-id="deb0d-173">Se questa opzione è definita, il client FTP funzionerà senza alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="deb0d-173">The  FTP Client will function without  any change if this option is  defined.</span></span> <span data-ttu-id="deb0d-174">Il server FTP dovrà essere modificato o l'utente dovrà creare una manciata di servizi FileX per funzionare correttamente.</span><span class="sxs-lookup"><span data-stu-id="deb0d-174">The FTP Server will  need to either be modified or the  user will have to create a handful  of FileX services in order to  function properly.</span></span>
- <span data-ttu-id="deb0d-175">**NX_FTP_CONTROL_TOS** Tipo di servizio richiesto per le richieste di controllo FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-175">**NX_FTP_CONTROL_TOS** Type of service required for the FTP control requests.</span></span> <span data-ttu-id="deb0d-176">Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-176">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span>
- <span data-ttu-id="deb0d-177">**NX_FTP_DATA_TOS** Tipo di servizio richiesto per le richieste di dati FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-177">**NX_FTP_DATA_TOS** Type of service required for the FTP data requests.</span></span> <span data-ttu-id="deb0d-178">Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-178">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span>
- <span data-ttu-id="deb0d-179">**NX_FTP_FRAGMENT_OPTION** Consenti frammenti per richieste FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-179">**NX_FTP_FRAGMENT_OPTION** Fragment enable for FTP requests.</span></span> <span data-ttu-id="deb0d-180">Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione TCP FTP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-180">By default, this value is NX_DONT_FRAGMENT to disable FTP TCP fragmenting.</span></span>
- <span data-ttu-id="deb0d-181">**NX_FTP_CONTROL_WINDOW_SIZE** Dimensioni della finestra socket di controllo TCP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-181">**NX_FTP_CONTROL_WINDOW_SIZE** TCP Control socket window size.</span></span> <span data-ttu-id="deb0d-182">Per impostazione predefinita, questo valore è pari a 400 byte.</span><span class="sxs-lookup"><span data-stu-id="deb0d-182">By default, this value is 400 bytes.</span></span>
- <span data-ttu-id="deb0d-183">**NX_FTP_DATA_WINDOW_SIZE** Dimensioni della finestra socket di dati TCP.</span><span class="sxs-lookup"><span data-stu-id="deb0d-183">**NX_FTP_DATA_WINDOW_SIZE** TCP Data socket window size.</span></span> <span data-ttu-id="deb0d-184">Per impostazione predefinita, questo valore è pari a 2048 byte.</span><span class="sxs-lookup"><span data-stu-id="deb0d-184">By default, this value is 2048 bytes.</span></span>
- <span data-ttu-id="deb0d-185">**NX_FTP_TIME_TO_LIVE** Specifica il numero di router che questo pacchetto può superare prima che venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="deb0d-185">**NX_FTP_TIME_TO_LIVE** Specifies the number of routers this packet can pass before it is discarded.</span></span> <span data-ttu-id="deb0d-186">Il valore predefinito è impostato su 0x80.</span><span class="sxs-lookup"><span data-stu-id="deb0d-186">The default value is set to 0x80.</span></span>
- <span data-ttu-id="deb0d-187">**NX_FTP_USERNAME_SIZE** Specifica il numero di byte consentiti in un *nome utente* fornito dal client.</span><span class="sxs-lookup"><span data-stu-id="deb0d-187">**NX_FTP_USERNAME_SIZE** Specifies the number of bytes allowed in a Client supplied *username*.</span></span> <span data-ttu-id="deb0d-188">Il valore predefinito è impostato su 20 *.*</span><span class="sxs-lookup"><span data-stu-id="deb0d-188">The default value is set to 20 *.*</span></span>
- <span data-ttu-id="deb0d-189">**NX_FTP_PASSWORD_SIZE** Specifica il numero di byte consentiti in una *password* fornita dal client.</span><span class="sxs-lookup"><span data-stu-id="deb0d-189">**NX_FTP_PASSWORD_SIZE** Specifies the number of bytes allowed in a client supplied *password*.</span></span> <span data-ttu-id="deb0d-190">Il valore predefinito è impostato su 20.</span><span class="sxs-lookup"><span data-stu-id="deb0d-190">The default value is set to 20.</span></span>
