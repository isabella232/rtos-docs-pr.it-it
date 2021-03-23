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
# <a name="chapter-2---installation-and-use-of-ftp"></a>Capitolo 2-installazione e uso di FTP

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo dei servizi FTP NetX Duo.

## <a name="product-distribution"></a>Distribuzione del prodotto

NetX Duo FTP è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nxd_ftp_client. h** File di intestazione per il client FTP NetX Duo
- **nxd_ftp_client. c** File di origine C per il client FTP NetX Duo
- **nxd_ftp_server. h** File di intestazione per il server FTP NetX Duo
- **nxd_ftp_server. c** File di origine C per il server FTP NetX Duo
- **filex_stub. h** File stub se FileX non è presente
- **nxd_ftp.pdf** Descrizione PDF di FTP per NetX Duo
- **demo_netxduo_ftp. c** Sistema di dimostrazione FTP

## <a name="netx-duo-ftp-installation"></a>Installazione FTP di NetX Duo

Per poter usare l'API FTP NetX Duo, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo. Se, ad esempio, NetX Duo è installato nella directory "*\threadx\arm7\green*", il *nxd_ftp_client. h* e *nxd_ftp_client. c* devono essere copiati in questa directory per le applicazioni client FTP e i file *nxd_ftp_server. h* e *nxd_ftp_server. c* devono essere copiati in questa directory per le applicazioni server FTP.

## <a name="using-netx-duo-ftp"></a>Uso di NetX Duo FTP

L'uso dell'API FTP NetX Duo è facile. In pratica, il codice dell'applicazione deve includere *nxd_ftp_client. h* per le applicazioni client ftp o *nxd_ftp_server* per le applicazioni server FTP, dopo aver incluso *tx_api. h, fx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX, FILEX e NETX Duo. Il progetto di compilazione deve includere il codice sorgente FTP e il file dell'applicazione host e, naturalmente, i file di libreria ThreadX e NetX. Questo è tutto ciò che è necessario per l'uso di NetX Duo FTP.

Si noti che poiché FTP utilizza i servizi TCP NetX Duo, è necessario abilitare TCP con la chiamata *nx_tcp_enable* prima di utilizzare FTP.

Si noti che la libreria NetX Duo può essere abilitata per IPv6 e che supporta ancora le reti IPv4. Tuttavia, NetX Duo non supporta IPv6, a meno che non sia abilitato. Per disabilitare l'elaborazione IPv6 in NetX Duo, è necessario definire il **NX_DISABLE_IPV6** nel file *nx_user. h* e tale file deve essere incluso nella compilazione della libreria NETX Duo definendo **NX_INCLUDE_USER_DEFINE_FILE** nel file *nx_port. h* . Per impostazione predefinita, **NX_DISABLE_IPV6** non è definito (IPv6 è abilitato). Si tratta di un servizio diverso da quello *nxd_ipv6_enable* che imposta i protocolli e i servizi IPv6 nell'attività IP e richiede che **NX_DISABLE_IPV6** non sia definito.

## <a name="small-example-system-of-netx-duo-ftp"></a>Piccolo sistema di esempio di NetX Duo FTP

Un esempio di come è facile usare NetX Duo FTP è descritto nella figura 1,1 riportata di seguito. In questo esempio vengono creati sia un server FTP che un client FTP. Pertanto, entrambi i file di inclusione FTP *nxd_ftp_client. h e nxd_ftp_server. h vengono* portati in corrispondenza della riga 10 e 11. Successivamente, il server FTP viene creato in "*tx_application_define*" alla riga 99. Si noti che il server FTP e i blocchi di controllo client sono definiti come variabili globali nella riga 26 precedente.

Questa demo illustra come usare le funzioni Duo disponibili in NetX Duo FTP e nei servizi FTP limitati IPv4 legacy. Per usare le funzioni IPv6, la demo definisce USE_IPV6 nella riga 16

Alla riga 162, il server FTP viene creato con ***nxd_ftp_server_create** _ se l'applicazione host definisce USE_IPV6 che supporta sia IPv4 che IPv6. In caso contrario, il server FTP viene creato con _ *_nx_ftp_server_create_** alla riga 166 con il servizio limitato IPv4. Si noti che la funzione ' Duo ' utilizza diversi argomenti della funzione di accesso e disconnessione rispetto al servizio IPv4, entrambi definiti nella parte inferiore del file nelle righe 534-568.

Il server FTP deve quindi stabilire l'indirizzo IPv6 (globale e collegamento locale) con NetX Duo, a partire dalla riga 466 nella funzione di immissione thread del server FTP. Il server FTP viene quindi avviato alla riga 518 ed è pronto per le richieste client FTP.

Il client FTP viene creato alla riga 316 e passa attraverso lo stesso processo del server FTP per ottenere l'attività IP del client FTP abilitata per IPv6 e i relativi indirizzi IPv6 convalidati a partire dalle righe 263-313.

Il client si connette quindi al server FTP usando ***nxd_ftp_client_connect** _ nella riga 334 se è stato definito USE_IPV6 o la riga 340 se usa il servizio limitato IPv4 _ *_nx_ftp_client_connect_* *. Nel corso della funzione thread client FTP, scrive un file nel server FTP e lo legge prima della disconnessione.

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

**Figura 1,1 esempio di FTP NetX Duo**

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la compilazione di FTP NetX e NetX Duo FTP. Sono elencati i valori predefiniti, ma ogni definizione può essere impostata dal

applicazione prima dell'inclusione del file di intestazione FTP NetX Duo specificato. Se non viene specificato alcun file di intestazione, l'opzione è disponibile sia in *nxd_ftp_client. h che in nxd_ftp_server. h*. L'elenco seguente descrive tutti i dettagli:

- **NX_FTP_SERVER_PRIORITY** Priorità del thread del server FTP. Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.
- **NX_FTP_MAX_CLIENTS** Il numero massimo di client che il server è in grado di gestire in una sola volta. Per impostazione predefinita, questo valore è 4 per supportare contemporaneamente 4 client.
- **NX_FTP_SERVER_MIN_PACKET_PAYLOAD** Dimensioni minime del payload del pool di pacchetti server in byte, incluse le intestazioni TCP, IP e frame di rete oltre ai dati HTTP. Il valore predefinito è 256 (lunghezza massima del nome file in FileX) + 12 byte per le informazioni sui file e NX_PHYSICAL_TRAILER.
- **NX_FTP_SERVER_TIMEOUT** Consente di specificare il numero di cicli ThreadX per i quali i servizi interni sospendono. Il valore predefinito è impostato su 1 secondo (1 * NX_IP_PERIODIC_RATE).
- **NX_FTP_ACTIVITY_TIMEOUT** Specifica il numero di secondi per cui una connessione client viene mantenuta in assenza di attività. Il valore predefinito è impostato su 240.
- **NX_FTP_TIMEOUT_PERIOD** Specifica gli intervalli in secondi durante i quali il server verifica l'attività del client. Il valore predefinito è impostato su 60.
- **NX_FTP_SERVER_RETRY_SECONDS** Specifica il timeout iniziale in secondi prima della ritrasmissione della risposta del server. Il valore predefinito è 2.
- **NX_FTP_SERVER_TRANSMIT_QUEUE_DEPTH** Specifica il livello massimo di profondità dei pacchetti di trasmissione in coda nel socket del server. Il valore predefinito è 20.
- **NX_FTP_SERVER_RETRY_MAX** Specifica il numero massimo di tentativi per pacchetto. Il valore predefinito è 10.
- **NX_FTP_SERVER_RETRY_SHIFT** Specifica il numero di bit da spostare nell'impostazione del timeout di ripetizione dei tentativi. Il valore predefinito è 2, ad esempio ogni timeout di ripetizione dei tentativi è due volte più lungo del tentativo precedente.
- **NX_FTP_NO_FILEX** Definito, questa opzione fornisce uno stub per le dipendenze FileX. Se questa opzione è definita, il client FTP funzionerà senza alcuna modifica. Il server FTP dovrà essere modificato o l'utente dovrà creare una manciata di servizi FileX per funzionare correttamente.
- **NX_FTP_CONTROL_TOS** Tipo di servizio richiesto per le richieste di controllo FTP. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.
- **NX_FTP_DATA_TOS** Tipo di servizio richiesto per le richieste di dati FTP. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.
- **NX_FTP_FRAGMENT_OPTION** Consenti frammenti per richieste FTP. Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione TCP FTP.
- **NX_FTP_CONTROL_WINDOW_SIZE** Dimensioni della finestra socket di controllo TCP. Per impostazione predefinita, questo valore è pari a 400 byte.
- **NX_FTP_DATA_WINDOW_SIZE** Dimensioni della finestra socket di dati TCP. Per impostazione predefinita, questo valore è pari a 2048 byte.
- **NX_FTP_TIME_TO_LIVE** Specifica il numero di router che questo pacchetto può superare prima che venga eliminato. Il valore predefinito è impostato su 0x80.
- **NX_FTP_USERNAME_SIZE** Specifica il numero di byte consentiti in un *nome utente* fornito dal client. Il valore predefinito è impostato su 20 *.*
- **NX_FTP_PASSWORD_SIZE** Specifica il numero di byte consentiti in una *password* fornita dal client. Il valore predefinito è impostato su 20.
