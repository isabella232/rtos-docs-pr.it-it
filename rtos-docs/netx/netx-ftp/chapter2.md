---
title: Capitolo 2-installazione e uso di Azure RTO NetX FTP
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente FTP NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 812422566b9761baac5f9c2477dba1f0fcc0a778
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822628"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-ftp"></a>Capitolo 2-installazione e uso di Azure RTO NetX FTP

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente FTP NetX di Azure RTO.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTO NetX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/]) . Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_ftp. h**: file di intestazione per FTP per NETX
- **nx_ftp_client. c**: file di origine c per il client FTP per NETX
- **nx_ftp_server. c**: file di origine c per il server FTP per NETX
- **filex_stub. h**: file stub se FILEX non è presente
- **nx_ftp.pdf**: Descrizione PDF di FTP per NETX
- **demo_netx_ftp. c**: sistema di dimostrazione FTP

## <a name="ftp-installation"></a>Installazione FTP

Per poter usare FTP per NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Se, ad esempio, NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_ftp. h*, *nx_ftp_client. c* e *nx_ftp_server. c* devono essere copiati in questa directory.

## <a name="using-ftp"></a>Uso di FTP

L'uso di FTP per NetX è facile. In pratica, il codice dell'applicazione deve includere *nx_ftp. h* dopo aver incluso *tx_api. h, fx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX, FILEX e NETX. Una volta incluso *nx_ftp. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione FTP specificate più avanti in questa guida. L'applicazione deve includere anche *nx_ftp_client. c* e *nx_ftp_server. c* nel processo di compilazione. Questi file devono essere compilati allo stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare FTP NetX.

> [!NOTE]
> Poiché FTP utilizza i servizi TCP NetX, è necessario abilitare TCP con la chiamata *nx_tcp_enable* prima di utilizzare FTP.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di come è facile usare l'FTP NetX è descritto nella figura 1,1 riportata di seguito.

> [!NOTE]
> Si tratta di un dispositivo host con una sola interfaccia di rete.

In questo esempio il file di inclusione FTP *nx_ftp_client. h* e *nx_ftp_server. h* vengono portati alla riga 10 e 11. Successivamente, il server FTP viene creato in "*tx_application_define*" alla riga 134. Si noti che il blocco di controllo server FTP "*Server*" è stato definito come variabile globale alla riga 31 in precedenza. Una volta completata la creazione, un server FTP viene avviato alla riga 363. Alla riga 183 viene creato il client FTP. Infine, il client scrive il file alla riga 229 e legge il file alla riga 318.

```c
/* This is a small demo of NetX FTP on the high-performance NetX TCP/IP stack. This demo
relies on ThreadX, NetX, and FileX to show a simple file transfer from the client
and then back to the server. */

#include     "tx_api.h"
#include     "fx_api.h"
#include     "nx_api.h"
#include     "nx_ftp_client.h"
#include     "nx_ftp_server.h"

#define     DEMO_STACK_SIZE     4096

/* Define the ThreadX, NetX, and FileX object control blocks... */

TX_THREAD          server_thread;
TX_THREAD          client_thread;
NX_PACKET_POOL     server_pool;
NX_IP              server_ip;
NX_PACKET_POOL     client_pool;
NX_IP              client_ip;
FX_MEDIA           ram_disk;

/* Define the NetX FTP object control blocks. */

NX_FTP_CLIENT     ftp_client;
NX_FTP_SERVER     ftp_server;

/* Define the counters used in the demo application... */

ULONG     error_counter = 0;

/* Define the memory area for the FileX RAM disk. */

UCHAR     ram_disk_memory[32000];
UCHAR     ram_disk_sector_cache[512];

#define FTP_SERVER_ADDRESS IP_ADDRESS(1,2,3,4)
#define FTP_CLIENT_ADDRESS IP_ADDRESS(1,2,3,5)

extern UINT _fx_media_format(FX_MEDIA *media_ptr, VOID (*driver)(FX_MEDIA *media),
                    VOID *driver_info_ptr, UCHAR *memory_ptr, UINT memory_size,
                    CHAR *volume_name, UINT number_of_fats, UINT directory_entries,
                    UINT hidden_sectors, ULONG total_sectors, UINT bytes_per_sector,
                    UINT sectors_per_cluster, UINT heads, UINT sectors_per_track);

/* Define the FileX and NetX driver entry functions. */
VOID     _fx_ram_driver(FX_MEDIA *media_ptr);

/* Replace the 'ram' driver with your own Ethernet driver. */
VOID     _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);

void     client_thread_entry(ULONG thread_input);
void     thread_server_entry(ULONG thread_input);

/* Define server login/logout functions. These are stubs for functions that would
validate a client login request. */

UINT     server_login(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
                ULONG client_ip_address, UINT client_port, CHAR *name,
                CHAR *password, CHAR *extra_info);

UINT     server_logout(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
                    ULONG client_ip_address, UINT client_port, CHAR *name,
                    CHAR *password, CHAR *extra_info);

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
    return(0);
}

/* Define what the initial system looks like. */

void     tx_application_define(void *first_unused_memory)
{

UINT      status;
UCHAR     *pointer;

    /* Setup the working pointer. */
    pointer = (UCHAR *) first_unused_memory;

    /* Create a helper thread for the server. */
    tx_thread_create(&server_thread, "FTP Server thread", thread_server_entry,
                    0, pointer, DEMO_STACK_SIZE,
                    4, 4, TX_NO_TIME_SLICE, TX_AUTO_START);

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize NetX. */
    nx_system_initialize();

    /* Create the packet pool for the FTP Server. */
    status = nx_packet_pool_create(&server_pool, "NetX Server Packet Pool",
                                    256, pointer, 8192);
    pointer = pointer + 8192;

    /* Check for errors. */
    if (status)
        error_counter++;

    /* Create the IP instance for the FTP Server. */
    status = nx_ip_create(&server_ip, "NetX Server IP Instance",
                        FTP_SERVER_ADDRESS, 0xFFFFFF00UL, &server_pool,
                        _nx_ram_network_driver, pointer, 2048, 1);
    pointer = pointer + 2048;

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Enable ARP and supply ARP cache memory for server IP instance. */
    nx_arp_enable(&server_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Enable TCP. */
    nx_tcp_enable(&server_ip);

    /* Create the FTP server. */
    status = nx_ftp_server_create(&ftp_server, "FTP Server Instance",
                    &server_ip, &ram_disk, pointer, DEMO_STACK_SIZE,
                    &server_pool, server_login, server_logout);
    pointer = pointer + DEMO_STACK_SIZE;

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Now set up the FTP Client. */

    /* Create the main FTP client thread. */
    status = tx_thread_create(&client_thread, "FTP Client thread ",
                            client_thread_entry, 0,
                            pointer, DEMO_STACK_SIZE,
                            6, 6, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer = pointer + DEMO_STACK_SIZE;

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Create a packet pool for the FTP client. */
    status = nx_packet_pool_create(&client_pool, "NetX Client Packet Pool",
                                    256, pointer, 8192);
    pointer = pointer + 8192;

    /* Create an IP instance for the FTP client. */
    status = nx_ip_create(&client_ip, "NetX Client IP Instance", FTP_CLIENT_ADDRESS,
            0xFFFFFF00UL, &client_pool, _nx_ram_network_driver, pointer, 2048, 1);
    pointer = pointer + 2048;

    /* Enable ARP and supply ARP cache memory for the FTP Client IP. */
    nx_arp_enable(&client_ip, (void *) pointer, 1024);

    pointer = pointer + 1024;

    /* Enable TCP for client IP instance. */
    nx_tcp_enable(&client_ip);

    return;
}

/* Define the FTP client thread. */
void     client_thread_entry(ULONG thread_input)
{

NX_PACKET     *my_packet;
UINT          status;

    /* Format the RAM disk - the memory for the RAM disk was defined above. */
    status = _fx_media_format(&ram_disk,
            _fx_ram_driver, /* Driver entry */
            ram_disk_memory, /* RAM disk memory pointer */
            ram_disk_sector_cache, /* Media buffer pointer */
            sizeof(ram_disk_sector_cache), /* Media buffer size */
            "MY_RAM_DISK", /* Volume Name */
            1, /* Number of FATs */
            32, /* Directory Entries */
            0, /* Hidden sectors */
            256, /* Total sectors */
            128, /* Sector size */
            1, /* Sectors per cluster */
            1, /* Heads */
            1); /* Sectors per track */

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Open the RAM disk. */
    status = fx_media_open(&ram_disk, "RAM DISK", _fx_ram_driver, ram_disk_memory,
                            ram_disk_sector_cache, sizeof(ram_disk_sector_cache));

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

     /* Let the IP threads and driver initialize the system. */
    tx_thread_sleep(100);

    /* Create an FTP client. */
    status = nx_ftp_client_create(&ftp_client, "FTP Client", &client_ip, 2000, &client_pool);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    printf("Created the FTP Client\n");

    /* Now connect with the NetX FTP (IPv4) server. */
    status = nx_ftp_client_connect(&ftp_client, FTP_SERVER_ADDRESS,
                                    "name", "password", 100);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    printf("Connected to the FTP Server\n");

    /* Open a FTP file for writing. */
    status = nx_ftp_client_file_open(&ftp_client, "test.txt", NX_FTP_OPEN_FOR_WRITE, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    printf("Opened the FTP client test.txt file\n");

    /* Allocate a FTP packet. */
    status = nx_packet_allocate(&client_pool, &my_packet, NX_TCP_PACKET, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Write ABCs into the packet payload! */
    memcpy(my_packet -> nx_packet_prepend_ptr, "ABCDEFGHIJKLMNOPQRSTUVWXYZ ", 28);

    /* Adjust the write pointer. */
    my_packet -> nx_packet_length = 28;
    my_packet -> nx_packet_append_ptr = my_packet -> nx_packet_prepend_ptr + 28;

    /* Write the packet to the file test.txt. */
    status = nx_ftp_client_file_write(&ftp_client, my_packet, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }
    else
        printf("Wrote to the FTP client test.txt file\n");

    /* Close the file. */
    status = nx_ftp_client_file_close(&ftp_client, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
        error_counter++;
    else
        printf("Closed the FTP client test.txt file\n");

    /* Now open the same file for reading. */
    status = nx_ftp_client_file_open(&ftp_client, "test.txt", NX_FTP_OPEN_FOR_READ, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
        error_counter++;

    else
        printf("Reopened the FTP client test.txt file\n");

    /* Read the file. */
    status = nx_ftp_client_file_read(&ftp_client, &my_packet, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
        error_counter++;
    else
    {
        printf("Reread the FTP client test.txt file\n");
        nx_packet_release(my_packet);
    }

    /* Close this file. */
    status = nx_ftp_client_file_close(&ftp_client, 100);

    if (status != NX_SUCCESS)
        error_counter++;

    /* Disconnect from the server. */
    status = nx_ftp_client_disconnect(&ftp_client, 100);

    /* Check status. */
    if (status != NX_SUCCESS)
        error_counter++;

    /* Delete the FTP client. */
    status = nx_ftp_client_delete(&ftp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
        error_counter++;
}

/* Define the helper FTP server thread. */
void     thread_server_entry(ULONG thread_input)
{

UINT     status;

    /* Wait till the IP thread and driver have initialized the system. */
    tx_thread_sleep(100);

    /* OK to start the FTP Server. */
    status = nx_ftp_server_start(&ftp_server);

    if (status != NX_SUCCESS)
        error_counter++;

    printf("Server started!\n");

    /* FTP server ready to take requests! */

    /* Let the IP threads execute. */
    tx_thread_relinquish();

    return;
}

UINT     server_login(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
                ULONG client_ip_address, UINT client_port,
                CHAR *name, CHAR *password, CHAR *extra_info)
{

    printf("Logged in!\n");
    /* Always return success. */
    return(NX_SUCCESS);
}

UINT     server_logout(struct NX_FTP_SERVER_STRUCT *ftp_server_ptr,
                    ULONG client_ip_address, UINT client_port,
                    CHAR *name, CHAR *password, CHAR *extra_info)
{
    printf("Logged out!\n");

    /* Always return success. */
    return(NX_SUCCESS);
}
```

Figura 1,1 esempio di client e server FTP con NetX (Single Network Interface host)

## <a name="configuration-options"></a>Opzioni di configurazione

Per la creazione di FTP per NetX sono disponibili diverse opzioni di configurazione. L'elenco seguente descrive tutti i dettagli:  

- **NX_FTP_SERVER_PRIORITY**: priorità del thread del server FTP. Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.

- **NX_FTP_MAX_CLIENTS**: il numero massimo di client che il server è in grado di gestire in una sola volta. Per impostazione predefinita, questo valore è 4 per supportare contemporaneamente 4 client.

- **NX_FTP_SERVER_MIN_PACKET_PAYLOAD**: dimensioni minime del payload del pool di pacchetti server in byte, incluse le intestazioni TCP, IP e frame di rete oltre ai dati http. Il valore predefinito è 256 (lunghezza massima del nome file in FileX) + 12 byte per le informazioni sui file e NX_PHYSICAL_TRAILER.

- **NX_FTP_NO_FILEX**: definito, questa opzione fornisce uno stub per le dipendenze FILEX. Se questa opzione è definita, il client FTP funzionerà senza alcuna modifica. Il server FTP dovrà essere modificato o l'utente dovrà creare una manciata di servizi FileX per funzionare correttamente.

- **NX_FTP_CONTROL_TOS**: tipo di servizio necessario per le richieste di controllo TCP FTP. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP. Questa definizione può essere impostata dall'applicazione prima di includere *nx_ftp. h*.

- **NX_FTP_DATA_TOS**: tipo di servizio necessario per le richieste di dati TCP FTP. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP. Questa definizione può essere impostata dall'applicazione prima di includere *nx_ftp. h*.

- **NX_FTP_FRAGMENT_OPTION**: abilitazione del frammento per le richieste TCP FTP. Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione TCP FTP. Questa definizione può essere impostata dall'applicazione prima di includere *nx_ftp. h*.

- **NX_FTP_CONTROL_WINDOW_SIZE**: dimensioni della finestra socket del controllo. Per impostazione predefinita, questo valore è pari a 400 byte. Questa definizione può essere impostata dall'applicazione prima di includere *nx_ftp. h*.

- **NX_FTP_DATA_WINDOW_SIZE**: dimensioni della finestra del socket di dati. Per impostazione predefinita, questo valore è pari a 2048 byte. Questa definizione può essere impostata dall'applicazione prima di includere *nx_ftp. h*.

- **NX_FTP_TIME_TO_LIVE**: specifica il numero di router che questo pacchetto può superare prima che venga eliminato. Il valore predefinito è impostato su 0x80, ma può essere ridefinito prima dell'inclusione di *nx_ftp. h.*

- **NX_FTP_SERVER_TIMEOUT**: specifica il numero di cicli di threadX per i quali i servizi interni vengono sospesi. Il valore predefinito è impostato su 100, ma può essere ridefinito prima dell'inclusione di *nx_ftp. h.*

- **NX_FTP_USERNAME_SIZE**: specifica il numero di byte consentiti in un *nome utente* fornito dal client. Il valore predefinito è impostato su 20, ma può essere ridefinito prima dell'inclusione di *nx_ftp. h.*

- **NX_FTP_PASSWORD_SIZE**: specifica il numero di byte consentiti in una *password* fornita dal client. Il valore predefinito è impostato su 20, ma può essere ridefinito prima dell'inclusione di *nx_ftp. h.*

- **NX_FTP_ACTIVITY_TIMEOUT**: specifica il numero di secondi per cui una connessione client viene mantenuta in assenza di attività. Il valore predefinito è impostato su 240, ma può essere ridefinito prima dell'inclusione di *nx_ftp. h.*

- **NX_FTP_TIMEOUT_PERIOD**: specifica il numero di secondi tra il controllo del server per l'inattività del client. Il valore predefinito è impostato su 60, ma può essere ridefinito prima dell'inclusione di *nx_ftp. h.*
