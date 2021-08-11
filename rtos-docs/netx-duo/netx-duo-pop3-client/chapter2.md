---
title: Capitolo 2 - Installazione e uso del client POP3 NetX Duo
description: NetX Duo POP3 Client include un file di origine, un file di intestazione e un file demo.
author: philmea
ms.author: philmea
ms.date: 07/09/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 5a3cbded6224617571941f58ffb6a08bde9575eba8791544182fb8499c14bf43
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116797195"
---
# <a name="chapter-2---installation-and-use-of-netx-duo-pop3-client"></a>Capitolo 2 - Installazione e uso del client POP3 NetX Duo

NetX POP3 Client include un file di origine, un file di intestazione e un file demo. Sono disponibili due file aggiuntivi per i servizi digest MD5. È anche disponibile un file PDF della Guida dell'utente (questo documento).

- **nxd_pop3_client.c** File di origine C per l'API client POP3 di NetX Duo
- **nxd_pop3_client.h** File di intestazione C per l'API client POP3 di NetX Duo
- **demo_netxduo_pop3_client.c** File demo per la creazione del client POP3 e l'avvio della sessione
- **nx_md5.c** File di origine C che definisce i servizi digest MD5
- **nx_md5.h** File di intestazione C che definisce i servizi digest MD5
- **nxd_pop3_client.pdf** Guida dell'utente del client POP3 di NetX Duo

Per usare netx Duo POP3 Client, l'intera distribuzione indicata in precedenza può essere copiata nella stessa directory in cui è installato NetX Duo. Ad esempio, se NetX Duo è installato nella directory "*\threadx\mcf5272\green*", i file *nx_md5.h*, *nx_md5.c,* *nxd_pop3_client.h e nxd_pop3_client.c* devono essere copiati in questa directory.

## <a name="using-netx-duo-pop3-client"></a>Uso del client POP3 NetX Duo

Per usare il servizio client POP3 NetX Duo, l'applicazione deve aggiungere *nxd_pop3_client.c* al progetto di compilazione. Il codice dell'applicazione deve includere *nx_md5.h e nxd_pop3_client.h* dopo *tx_api.h* e *nx_api.h*, per poter usare ThreadX e NetX Duo.

Questi file devono essere compilati nello stesso modo degli altri file dell'applicazione e il codice oggetto deve essere collegato insieme ai file dell'applicazione. Questo è tutto ciò che è necessario per usare il client POP3 NetX Duo.

## <a name="small-example-of-the-netx-duo-pop3-client"></a>Piccolo esempio del client POP3 NetX Duo

Un esempio di come usare i servizi client POP3 di NetX Duo è descritto nella figura 1 riportata di seguito. Questa demo configura i due callback per la notifica del download della posta e del completamento della sessione nelle righe 37 e 38. Il pool di pacchetti client POP3 viene creato alla riga 76. L'attività thread IP viene creata alla riga 88. Si noti che questo pool di pacchetti viene usato anche per il pool di pacchetti client POP3. TCP è abilitato nell'attività IP nella riga 107.

Il client POP3 viene creato alla riga 133 all'interno della funzione di immissione del thread *dell'applicazione, demo_thread_entry*. Questo perché il *nx_pop3_client_create* tenta anche di stabilire una connessione TCP con il server POP3. In caso di esito positivo, l'applicazione esegue una query sul server POP3 per il numero di elementi nel relativo maildrop alla riga 149 usando il *nx_pop3_client_mail_items_get* servizio.

Se sono presenti uno o più elementi, l'applicazione scorre il ciclo while per ogni elemento di posta per scaricare il messaggio di posta elettronica. La richiesta RETR viene effettuata alla riga 149 *nella nx_pop3_client_mail_item_get* chiamata. In caso di esito positivo, l'applicazione scarica i pacchetti usando il servizio *nx_pop3_client_mail_item_message_get* alla riga 177 finché non rileva che l'ultimo pacchetto nel messaggio è stato ricevuto alla riga 196. Infine, l'applicazione elimina l'elemento di posta, presupponendo che si sia verificato un download riuscito alla riga 199 *della* nx_pop3_client_mail_item_delete chiamata. Rfc 1939 consiglia ai client POP3 di indicare al server di eliminare gli elementi di posta scaricati per impedire l'accumulo di posta elettronica nel maildrop del client. Il server può eseguire automaticamente questa operazione in ogni caso.

Dopo aver scaricato tutti gli elementi di posta elettronica o se una chiamata al servizio client POP3 ha esito negativo, l'applicazione esce dal ciclo ed elimina il client POP3 alla riga 217 usando il servizio *nx_pop3_client_delete.*

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

**Figura 1. Esempio di un'applicazione client POP3 NetX Duo**

## <a name="pop3-client-configuration-options"></a>Opzioni di configurazione del client POP3

Sono disponibili diverse opzioni di configurazione con il client POP3 di NetX Duo. Di seguito è riportato un elenco di tutte le opzioni descritte in dettaglio:

- **NX_POP3_CLIENT_PACKET_TIMEOUT** Definisce l'opzione di attesa in secondi per l'allocazione di un pacchetto da parte del client POP3. Il valore predefinito è 1 secondo.
- **NX_POP3_CLIENT_CONNECTION_TIMEOUT** Definisce l'opzione di attesa in secondi per la connessione del client POP3 al server POP3. Il valore predefinito è 30 secondi.
- **NX_POP3_CLIENT_DISCONNECT_TIMEOUT** Definisce l'opzione di attesa in secondi per la disconnessione del client POP3 dal server POP3. Il valore predefinito è 2 secondi.
- **NX_POP3_TCP_SOCKET_SEND_WAIT** Questa opzione imposta l'opzione di attesa in secondi nelle chiamate *nx_tcp_socket_send* servizio. Il valore predefinito è 2 secondi.
- **NX_POP3_SERVER_REPLY_TIMEOUT** Questa opzione imposta l'opzione wait *nx_tcp_socket_receive* chiamate del servizio per la risposta del server a una richiesta client. Il valore predefinito è 10 secondi.
- **NX_POP3_CLIENT_TCP_WINDOW_SIZE** Questa opzione imposta le dimensioni della finestra di ricezione TCP client. Deve essere impostata sulla dimensione MTU dell'istanza IP meno l'intestazione IP e TCP. Il valore predefinito è 1460. Dovrebbe essere inferiore se l'applicazione invia pacchetti POP3 tramite IPv6 (1440 byte) per prendere in considerazione l'intestazione IPv6 più grande.
- **NX_POP3_MAX_USERNAME** Questa opzione imposta le dimensioni del buffer del nome utente del client POP3. Il valore predefinito è 40 byte.
- **NX_POP3_MAX_PASSWORD** Questa opzione imposta le dimensioni del buffer della password del client POP3. Il valore predefinito è 20 byte.
