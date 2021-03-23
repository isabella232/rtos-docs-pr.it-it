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
# <a name="chapter-2---installation-and-use-of-netx-http"></a>Capitolo 2-installazione e uso di HTTP NetX

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente HTTP NetX.

## <a name="product-distribution"></a>Distribuzione del prodotto

Azure RTO NetX può essere ottenuto dal repository di codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .

- **nx_http_client. h** File di intestazione per il client HTTP per NetX
- **nx_http_server. h** File di intestazione per il server HTTP per NetX
- **nx_http_client. c** File di origine C per il client HTTP per NetX
- **nx_http_server. c** File di origine C per il server HTTP per NetX
- **nx_md5. c** Algoritmi digest MD5
- **filex_stub. h** File stub se FileX non è presente
- **nx_http.pdf** Descrizione di HTTP per NetX
- **demo_netx_http. c** Dimostrazione HTTP di NetX

## <a name="http-installation"></a>Installazione HTTP

Per poter usare HTTP per NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory "*\threadx\arm7\green*", il *nx_http_client. h* e *nx_http_client. c* per le applicazioni client http NetX e *nx_http_server. h* e *nx_http_server. c* per le applicazioni server http NETX. *nx_md5. c* deve essere copiato in questa directory. Per la demo ' RAM driver ' dell'applicazione NetX client HTTP e i file server devono essere copiati nella stessa directory.

## <a name="using-http"></a>Uso di HTTP

L'uso di HTTP per NetX è facile. In pratica, il codice dell'applicazione deve includere *nx_http_client. h* e/o *nx_http_server. h* dopo aver incluso *tx_api. h, fx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX, FILEX e NETX. Una volta inclusi i file di intestazione HTTP, il codice dell'applicazione è in grado di eseguire le chiamate di funzione HTTP specificate più avanti in questa guida. L'applicazione deve includere anche *nx_http_client. c*, *nx_http_server. c* e *MD5. c* nel processo di compilazione. Questi file devono essere compilati allo stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare HTTP di NetX.

>[!NOTE] 
> Se NX_HTTP_DIGEST_ENABLE non viene specificato nel processo di compilazione, non è necessario aggiungere il file *MD5. c* all'applicazione. Analogamente, se non sono richieste funzionalità client HTTP, il file *nx_http_client. c* può essere omesso.

>[!NOTE] 
> Poiché HTTP usa i servizi TCP NetX, è necessario abilitare TCP con la chiamata *nx_tcp_enable* prima di usare http.

## <a name="small-example-system"></a>Sistema di esempio di piccole dimensioni

Un esempio di come è facile usare HTTP di NetX è descritto nella figura 1,1 riportata di seguito. In questo esempio, il file di inclusione HTTP *nx_http_client. h e nx_http_server. h vengono* portati nella riga 8. Successivamente, il server HTTP viene creato in "*tx_application_define*" alla riga 131.

>[!NOTE] 
> Il blocco di controllo server HTTP "*Server*" è stato definito come variabile globale alla riga 25 in precedenza.

Una volta completata la creazione, un server HTTP viene avviato alla riga 136. Alla riga 149 viene creato il client HTTP. Infine, il client scrive il file alla riga 157 e legge il file alla riga 195.

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

Figura 1,1 esempio di utilizzo HTTP con NetX

## <a name="configuration-options"></a>Opzioni di configurazione

Per la compilazione di HTTP per NetX sono disponibili diverse opzioni di configurazione. Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio. I valori predefiniti sono elencati, ma possono essere ridefiniti prima dell'inclusione di *nx_http_client. h e nx_http_server. h*:

- **NX_DISABLE_ERROR_CHECKING** Definita, questa opzione rimuove il controllo degli errori HTTP di base. Viene in genere usato dopo il debug dell'applicazione.
- **NX_HTTP_SERVER_PRIORITY** Priorità del thread del server HTTP. Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.
- **NX_HTTP_NO_FILEX** Definito, questa opzione fornisce uno stub per le dipendenze FileX. Se questa opzione è definita, il client HTTP funzionerà senza alcuna modifica. Il server HTTP dovrà essere modificato o l'utente dovrà creare un numero limitato di servizi FileX per il corretto funzionamento.
- **NX_HTTP_TYPE_OF_SERVICE** Tipo di servizio richiesto per le richieste TCP HTTP. Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.
- **NX_HTTP_SERVER_THREAD_TIME_SLICE** Numero di cicli del timer che il thread del server può eseguire prima di cedere ai thread con la stessa priorità. Il valore predefinito è 2.
- **NX_HTTP_FRAGMENT_OPTION** L'abilitazione del frammento per le richieste TCP HTTP. Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione TCP HTTP.
- **NX_HTTP_SERVER_WINDOW_SIZE** Dimensioni finestra socket server. Per impostazione predefinita, questo valore è pari a 2048 byte.
- **NX_HTTP_TIME_TO_LIVE** Specifica il numero di router che questo pacchetto può superare prima che venga eliminato. Il valore predefinito è impostato su 0x80.
- **NX_HTTP_SERVER_TIMEOUT** Consente di specificare il numero di cicli ThreadX per i quali i servizi interni sospendono. Il valore predefinito è impostato su 10 secondi (10 * NX_IP_PERIODIC_RATE).
- **NX_HTTP_SERVER_TIMEOUT_ACCEPT** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_server_socket_accept* . Il valore predefinito è impostato su (10 * NX_IP_PERIODIC_RATE).
- **NX_HTTP_SERVER_TIMEOUT_DISCONNECT** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_disconnect* . Il valore predefinito è impostato su 10 secondi (10 * NX_IP_PERIODIC_RATE).
- **NX_HTTP_SERVER_TIMEOUT_RECEIVE** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_receive* . Il valore predefinito è impostato su 10 secondi (10 * NX_IP_PERIODIC_RATE).
- **NX_HTTP_SERVER_TIMEOUT_SEND** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_send* . Il valore predefinito è impostato su 10 secondi (10 * NX_IP_PERIODIC_RATE).
- **NX_HTTP_MAX_HEADER_FIELD** Specifica la dimensione massima del campo dell'intestazione HTTP. Il valore predefinito è 256.
- **NX_HTTP_MULTIPART_ENABLE** Se definito, Abilita il server HTTP per supportare le richieste HTTP multipart.
- **NX_HTTP_SERVER_MAX_PENDING** Specifica il numero di connessioni che possono essere accodate per il server HTTP. Il valore predefinito è impostato su 5.
- **NX_HTTP_MAX_RESOURCE** Specifica il numero di byte consentiti in un *nome di risorsa* fornito dal client. Il valore predefinito è impostato su 40.
- **NX_HTTP_MAX_NAME** Specifica il numero di byte consentiti in un *nome utente* fornito dal client. Il valore predefinito è impostato su 20.
- **NX_HTTP_MAX_PASSWORD** Specifica il numero di byte consentiti in una *password* fornita dal client. Il valore predefinito è impostato su 20.
- **NX_HTTP_SERVER_MIN_PACKET_SIZE** Specifica la dimensione minima dei pacchetti nel pool specificato al momento della creazione del server. La dimensione minima è necessaria per garantire che l'intestazione HTTP completa possa essere contenuta in un unico pacchetto. Il valore predefinito è impostato su 600.
- **NX_HTTP_CLIENT_MIN_PACKET_SIZE** Specifica la dimensione minima dei pacchetti nel pool specificato durante la creazione del client. La dimensione minima è necessaria per garantire che l'intestazione HTTP completa possa essere contenuta in un unico pacchetto. Il valore predefinito è impostato su 300.
- **NX_HTTP_SERVER_RETRY_SECONDS** *impostare il timeout di ritrasmissione del socket del server in secondi. Il* valore predefinito è impostato su 2.
- **NX_HTTP_SERVER_RETRY_MAX** Questo consente di impostare il numero massimo di ritrasmissioni sul socket del server. Il valore predefinito è impostato su 10.
- **NX_HTTP_SERVER_RETRY_SHIFT** Questo valore viene utilizzato per impostare il timeout di ritrasmissione successivo. Il timeout corrente viene moltiplicato per il numero di ritrasmissioni fino a questo punto, spostate in base al valore del turno di timeout del socket. Il valore predefinito è impostato su 1 per raddoppiare il timeout.
- **NX_HTTP_ SERVER_TRANSMIT_QUEUE_DEPTH** Specifica il numero massimo di pacchetti che possono essere accodati nella coda di ritrasmissione del socket server. Se il numero di pacchetti accodati raggiunge questo numero, non sarà più possibile inviare pacchetti fino a quando non vengono rilasciati uno o più pacchetti accodati. Il valore predefinito è impostato su 20.