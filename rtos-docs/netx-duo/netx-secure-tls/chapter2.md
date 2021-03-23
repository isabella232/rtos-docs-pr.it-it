---
title: Capitolo 2-installazione e uso di Azure RTO NetX Secure
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente NetX Secure.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b3ef82bd113518b35105fb2eefe23bd3e755ca06
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822856"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-secure"></a>Capitolo 2-installazione e uso di Azure RTO NetX Secure

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente protetto Azure RTO NetX.

## <a name="product-version-number"></a>Numero di versione del prodotto

L'utente può verificare il numero di versione del prodotto individuando i simboli seguenti in nx_secure_tls. h:

***NETX_SECURE_MAJOR_VERSION***

***NETX_SECURE_MINOR_VERSION***

Le versioni del Service Pack hanno il simbolo seguente definito per indicare il numero Service Pack:

***NETX_SECURE_SERVICE_PACK_VERSION***

## <a name="product-distribution"></a>Distribuzione del prodotto

NetX Secure è disponibile all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) . Il pacchetto include i file di origine, i file di inclusione e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_secure_tls_api. h** File di intestazione dell'API pubblica per NetX Secure TLS
- **nx_secure_tls_user. h** Il file di intestazione definito dall'utente per NetX Secure TLS
- **nx_secure_tls_port. h** Definizioni specifiche della piattaforma per NetX Secure
- **nx_secure_tls. h** File di intestazione per NetX Secure TLS
- **nx_secure_tls&#42;. c/h** File di origine C/H per NetX Secure TLS
- **nx_crypto&#42;. c/h** File di origine C/H per crittografia sicura NetX
- **nx_secure_x509&#42;. c/h** File di origine C/H per i certificati digitali X. 509.
- **demo_netx_secure_tls. c** File di origine C per NetX Secure TLS demo
- **NetX_Secure_User_Guide.pdf** Descrizione PDF del prodotto NetX Secure

> [!NOTE]
> I file nx_crypto * vengono forniti per diverse piattaforme hardware in una sottodirectory della directory padre protetta NetX.

## <a name="netx-secure-installation"></a>Installazione sicura di NetX

Per poter usare NetX Secure, l'intera distribuzione indicata in precedenza deve essere copiata nello stesso livello di directory in cui è installato NetX. Ad esempio, se NetX è installato nella directory "*\threadx\arm7\NetX*" *, il nx_secure * *.* le directory devono essere copiate in "*\threadx\arm7\NetXSecure*".

## <a name="using-netx-secure"></a>Uso di NetX Secure

L'uso di NetX Secure TLS è semplice. In pratica, il codice dell'applicazione deve includere *nx_secure_tls_api. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter usare threadX e NETX. Una volta incluso *nx_secure_tls_api. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione NETX Secure specificate più avanti in questa guida. L'applicazione deve inoltre importare la *nx_secure * *.* file in una libreria NetXSecure e *nx_crypto * ** specifici della piattaforma. file in una libreria NetXCrypto.

## <a name="small-example-system-tls-client"></a>Sistema di esempio di piccole dimensioni (client TLS)

Un esempio di come è facile usare NetX Secure è descritto nella figura 1,1, che viene visualizzato di seguito. Questo esempio illustra un semplice client TLS, che usa moduli di crittografia software (non specifici dell'hardware) per la crittografia. È progettato per l'uso con il server echo OpenSSL Reverse (OpenSSL s_server-REV).

Si noti che per eseguire questo esempio, sarà necessario un certificato della CA X. 509 per autenticare il certificato del server di destinazione. Per l'esempio OpenSSL, è sufficiente una semplice infrastruttura a chiave pubblica (PKI) a 2 livelli, ovvero un certificato CA radice-> >certificato server. Sarà necessario compilare la matrice "trusted_ca_data" con una versione binaria con codifica DER del certificato della CA e aggiornare la variabile "trusted_ca_length" per riflettere la lunghezza effettiva del certificato.

Sarà inoltre necessario il driver di rete per l'hardware (sostituire il parametro "nx_driver_xx" nella chiamata nx_ip_create).

```C
#include "tx_api.h"
#include "nx_api.h"
#include "nx_secure_tls_api.h"
#include "nx_secure_x509.h"

/* Define the size of our application stack. */
#define     DEMO_STACK_SIZE             4096

/* Define the remote server IP address using NetX IP_ADDRESS macro. */
#define     REMOTE_SERVER_IP_ADDRESS    IP_ADDRESS(192, 168, 1, 1)

/* Define the IP address for this device. */
#define     DEVICE_IP_ADDRESS           IP_ADDRESS(192, 168, 1, 2)

/* Define the remote server port. 443 is the HTTPS default. */
#define     REMOTE_SERVER_PORT          443

/* Define the ThreadX and NetX object control blocks...  */

NX_PACKET_POOL          pool_0;
NX_IP                   ip_0;
NX_TCP_SOCKET tcp_socket;
NX_SECURE_TLS_SESSION tls_session;
NX_SECURE_X509_CERT certificate;

/* Define an HTTP request to be sent to the HTTPS web server not defined here but
  represented by the ellipsis. */
UCHAR http_request[] = { "GET /example.html HTTP/1.1"  };

/* Define the IP thread's stack area.  */
ULONG ip_thread_stack[3 * 1024 / sizeof(ULONG)];

/* Define packet pool for the demonstration.  */
#define NX_PACKET_POOL_SIZE ((1536 + sizeof(NX_PACKET)) * 32)

ULONG packet_pool_area[NX_PACKET_POOL_SIZE/sizeof(ULONG) + 64 / sizeof(ULONG)];

/* Define the ARP cache area.  */
ULONG arp_space_area[512 / sizeof(ULONG)];

/* Define the TLS Client thread.  */
ULONG             tls_client_thread_stack[6 * 1024 / sizeof(ULONG)];
TX_THREAD         tls_client_thread;
void              client_thread_entry(ULONG thread_input);

/* Define the TLS packet reassembly buffer. */
UCHAR tls_packet_buffer[18000];

/* Define the metadata area for TLS cryptography. The actual size needed can be
   Ascertained by calling nx_secure_tls_metadata_size_calculate.
*/
UCHAR tls_crypto_metadata[18000];

/* Pointer to the TLS ciphersuite table that is included in the platform-specific
   cryptography subdirectory. The table maps the cryptographic routines for the
   platform to function pointers usable by the TLS library.
*/
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers_ecc;
extern const USHORT nx_crypto_ecc_supported_groups[];
extern const NX_CRYPTO_METHOD *nx_crypto_ecc_curves[];
extern const UINT nx_crypto_ecc_supported_groups_size;

/* Binary data for the TLS Client X.509 trusted root CA certificate, ASN.1 DER-
   encoded. A trusted certificate must be provided for TLS Client applications
   (unless X.509 authentication is disabled) or TLS will treat all certificates as
   untrusted and the handshake will fail.
*/

/* DER-encoded binary certificate, not defined here but represented by the ellipsis,
   for the sake of brevity. */
const UCHAR trusted_ca_data[] = { … };
const UINT trusted_ca_length = 0x574;

/* Define the application – initialize drivers and TCP/IP setup.
   NOTE: the variable “status” should be checked after every API call. Most error
         checking has been omitted for clarity. */
void    tx_application_define(void *first_unused_memory)
{
UINT  status;

   /* Initialize the NetX system.  */
   nx_system_initialize();

   /* Create a packet pool. Check status for errors. */
   status =  nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 1536,
                                   (ULONG*)(((int)packet_pool_area + 64) & ~63) ,
                                   NX_PACKET_POOL_SIZE);

   /* Create an IP instance for the specific target. Check status for errors. This
      call is not completely defined. Please see other demo files for proper usage
      of the nx_ip_create call. */
   status = nx_ip_create(&ip_0, "NetX IP Instance 0",
                         DEVICE_IP_ADDRESS ,
                         0xFFFFFF00UL,
                         &pool_0, nx_driver_xx,
                         (UCHAR*)ip_thread_stack,
                         sizeof(ip_thread_stack),
                         1);

   /* Enable ARP and supply ARP cache memory for IP Instance 0. Check status for
       errors. */
   status =  nx_arp_enable(&ip_0, (void *)arp_space_area, sizeof(arp_space_area));

   /* Enable TCP traffic. Check status for errors. */
   status =  nx_tcp_enable(&ip_0);

   status =  nx_ip_fragment_enable(&ip_0);

   /* Initialize the NetX Secure TLS system.  */
   nx_secure_tls_initialize();

    /* Create the TLS client thread to start handling incoming requests. */
   tx_thread_create(&tls_client_thread, "TLS Client thread", client_thread_entry, 0,
                     tls_client_thread_stack, sizeof(tls_client_thread_stack),
                     16, 16, 4, TX_AUTO_START);
   return;
}

/* Thread to handle the TLS Client instance. */
void client_thread_entry(ULONG thread_input)
{
UINT       status;
ULONG       actual_status;
NX_PACKET *send_packet;
NX_PACKET *receive_packet;
UCHAR receive_buffer[100];
ULONG bytes;
ULONG server_ipv4_address;

    /* We are not using the thread input parameter so suppress compiler warning. */
    NX_PARAMETER_NOT_USED(thread_input);

   /* Ensure the IP instance has been initialized.  */
   status =  nx_ip_status_check(&ip_0, NX_IP_INITIALIZE_DONE, &actual_status,
                                 NX_IP_PERIODIC_RATE);

   /* Create a TCP socket to use for our TLS session.  */
   status =  nx_tcp_socket_create(&ip_0, &tcp_socket, "TLS Client Socket",
                                  NX_IP_NORMAL, NX_FRAGMENT_OKAY,
                                  NX_IP_TIME_TO_LIVE, 8192, NX_NULL, NX_NULL);

   /* Create a TLS session for our socket. This sets up the TLS session object for
          later use */
   status =  nx_secure_tls_session_create(&tls_session,
                                          &nx_crypto_tls_ciphers_ecc,
                                          tls_crypto_metadata,
                                          sizeof(tls_crypto_metadata));

   /* Initialize ECC parameters for this session. */
   status = nx_secure_tls_ecc_initialize(&tls_session,
                                             nx_crypto_ecc_supported_groups,
                                             nx_crypto_ecc_supported_groups_size,
                                             nx_crypto_ecc_curves);

   /* Set the packet reassembly buffer for this TLS session. */
   status = nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                    sizeof(tls_packet_buffer));

   /* Initialize an X.509 certificate with our CA root certificate data. */
   nx_secure_x509_certificate_initialize(&certificate, trusted_ca_data,
                                         trusted_ca_length, NX_NULL, 0, NX_NULL, 0,
                                         NX_SECURE_X509_KEY_TYPE_NONE);

   /* Add the initialized certificate as a trusted root certificate. */
   nx_secure_tls_trusted_certificate_add(&tls_session, &certificate);

   /* Setup this thread to open a connection on the TCP socket to a remote server.
      The IP address can be used directly or it can be obtained via DNS or other
      means.*/
   server_ipv4_address = REMOTE_SERVER_IP_ADDRESS;
   status = nx_tcp_client_socket_connect(&tcp_socket, server_ipv4_address,
                                         REMOTE_SERVER_PORT, NX_WAIT_FOREVER);

   /* Start the TLS Session using the connected TCP socket. This function will
      ascertain from the TCP socket state that this is a TLS Client session. */
   status = nx_secure_tls_session_start(&tls_session, &tcp_socket,
                                         NX_WAIT_FOREVER);

    /* Allocate a TLS packet to send an HTTP request over TLS (HTTPS). */
    status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                          NX_WAIT_FOREVER);

    /* Populate the packet with our HTTP request. */
    nx_packet_data_append(send_packet, http_request, sizeof(http_request), &pool_0,
                          NX_WAIT_FOREVER);


   /* Send the HTTP request over the TLS Session, turning it into HTTPS. */
   status = nx_secure_tls_session_send(&tls_session, send_packet, NX_WAIT_FOREVER);

   /* If the send fails, you must release the packet.  */
   if (status != NX_SUCCESS)
   {
         /* Release the packet since the packet was not sent.  */
         nx_packet_release(send_packet);
   }

   /* Receive the HTTP response and any data from the server. */
   status = nx_secure_tls_session_receive(&tls_session, &receive_packet,
   NX_WAIT_FOREVER);
   if (status == NX_SUCCESS)
   {
       /* Extract the data we received from the remote server. */
       status = nx_packet_data_extract_offset(receive_packet, 0, receive_buffer,
                                             100,  &bytes);
        /* Display the response data. */
       receive_buffer[bytes] = 0;
       printf("Received data: %s\n", receive_buffer);

        /* Release the packet when done with it. */
       nx_packet_release(receive_packet);
   }

   /* End the TLS session now that we have received our HTTPS/HTML response. */
   status = nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);

   /* Check for errors to make sure the session ended cleanly. */

   /* Disconnect the TCP socket. */
   status =  nx_tcp_socket_disconnect(&tcp_socket, NX_WAIT_FOREVER);

}
```

**Figura 1,1 esempio di uso sicuro di NetX con NetX**

## <a name="small-example-system-tls-web-server"></a>Sistema di esempio di piccole dimensioni (server Web TLS)

Un esempio di come è facile usare NetX Secure è descritto nella figura 1,1, che viene visualizzato di seguito e viene illustrato un semplice server Web TLS (HTTPS).

Si noti che per eseguire questo esempio, è necessario un certificato X. 509 per identificare il server nei client TLS. Per la maggior parte dei Web browser è sufficiente un certificato autofirmato semplice. Il browser si lamenta di non essere in grado di autenticare il server e, in alcuni casi, potrebbe non essere in grado di stabilire una connessione TLS/HTTPS al server<sup>3</sup>. Sarà necessario compilare la matrice "certificate_data" con una versione binaria con codifica DER del certificato del server e aggiornare la variabile "certificate_length" per riflettere la lunghezza effettiva del certificato. È anche necessario compilare la matrice "private_key" con una versione con codifica DER della chiave privata del certificato, formattata con PKCS # 1 per la chiave RSA e RFC 5915 per le chiavi ECC. Compilare la variabile "private_key_length" con la lunghezza effettiva dei dati della chiave.

> [!IMPORTANT]
> Alcuni browser (in particolare alcune versioni del browser Chrome) potrebbero rifiutare i certificati autofirmati. In questo caso è possibile creare un'infrastruttura a chiave pubblica a due livelli con un certificato CA radice usato per firmare il certificato del server. In questa situazione, il certificato CA radice viene installato come certificato radice attendibile nel browser. !!! IMPORTANTE: rimuovere il certificato CA radice dal browser al termine e non usarlo per applicazioni di produzione!!!

Sarà inoltre necessario il driver di rete per l'hardware (sostituire il parametro "nx_driver_xx" nella chiamata nx_ip_create).

```C
#include "tx_api.h"
#include "nx_api.h"
#include "nx_secure_tls_api.h"
#include "nx_secure_x509.h"

#define     DEMO_STACK_SIZE         4096

/* Define the IP address for this device. */
#define     DEVICE_IP_ADDRESS             IP_ADDRESS(192, 168, 1, 2)

/* Define the ThreadX and NetX object control blocks...  */

NX_PACKET_POOL          pool_0;
NX_IP                   ip_0;
NX_TCP_SOCKET tcp_socket;
NX_SECURE_TLS_SESSION tls_session;
NX_SECURE_X509_CERT certificate;

/* Define the IP thread's stack area.  */
ULONG ip_thread_stack[3 * 1024 / sizeof(ULONG)];

/* Define packet pool for the demonstration.  */
#define NX_PACKET_POOL_SIZE ((1536 + sizeof(NX_PACKET)) * 32)

ULONG packet_pool_area[NX_PACKET_POOL_SIZE/sizeof(ULONG) + 64 / sizeof(ULONG)];

/* Define the ARP cache area.  */
ULONG arp_space_area[512 / sizeof(ULONG)];


/* Define the TLS Server thread.  */
ULONG             tls_server_thread_stack[6 * 1024 / sizeof(ULONG)];
TX_THREAD         tls_server_thread;
void              server_thread_entry(ULONG thread_input);

/* Define the TLS packet reassembly buffer. */
UCHAR tls_packet_buffer[18000];

/* Define the metadata area for TLS cryptography. The actual size needed can be
   Ascertained by calling nx_secure_tls_metadata_size_calculate.
*/
UCHAR tls_crypto_metadata[18000];

/* Pointer to the TLS ciphersuite table that is included in the platform-specific
   cryptography subdirectory. The table maps the cryptographic routines for the
   platform to function pointers usable by the TLS library.
*/
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers_ecc;
extern const USHORT nx_crypto_ecc_supported_groups[];
extern const NX_CRYPTO_METHOD *nx_crypto_ecc_curves[];
extern const UINT nx_crypto_ecc_supported_groups_size;

/* Binary data for the TLS Server X.509 certificate, ASN.1 DER-encoded. Note that the
   certificate data and private key data is represented by an ellipsis for the sake
   of brevity.
*/
const UCHAR certificate_data[] = { … }; /* DER-encoded binary certificate. */
const UINT certificate_length = 0x574;

/* Binary data for the TLS Server Private Key, from private key
   file generated at the time of the X.509 certificate creation. ASN.1 DER-encoded. */
const UCHAR private_key[] = { … }; /* DER-encoded private key file (PKCS#1 RSA or ECC) */
const UINT private_key_length = 0x40;

/* Define some HTML data (web page) with an HTTPS header to serve to connecting
   clients. */
UCHAR html_data[] = { "HTTP/1.1 200 OK\r\n" \
        "Date: Tue, 19 May 2020 23:59:59 GMT\r\n" \
        "Content-Type: text/html\r\n" \
        "Content-Length: 200\r\n\r\n" \
        "<html>\r\n"\
        "<body>\r\n"\
        "<b>Hello NetX Secure User!</b>\r\n"\
        "This is a simple webpage\r\n"\
        "served up using NetX Secure!\r\n"\
        "</body>\r\n"\
        "</html>\r\n" };

/* Define the application – initialize drivers and TCP/IP setup.  */
void    tx_application_define(void *first_unused_memory)
{
UINT  status;


    /* Initialize the NetX system.  */
    nx_system_initialize();

    /* Create a packet pool. Check status for errors. */
    status =  nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 1536,
                                    (ULONG*)(((int)packet_pool_area + 64) & ~63) ,
                                    NX_PACKET_POOL_SIZE);

    /* Create an IP instance for the specific target. Check status for errors. */
    status = nx_ip_create(&ip_0, "NetX IP Instance 0",
                          DEVICE_IP_ADDRESS,
                          0xFFFFFF00UL,
                          &pool_0, nx_driver_xx,
                          (UCHAR*)ip_thread_stack,
                          sizeof(ip_thread_stack),
                          1);

    /* Enable ARP and supply ARP cache memory for IP Instance 0. Check status for
         errors. */
    status =  nx_arp_enable(&ip_0, (void *)arp_space_area, sizeof(arp_space_area));

    /* Enable TCP traffic. Check status for errors. */
    status =  nx_tcp_enable(&ip_0);

    status =  nx_ip_fragment_enable(&ip_0);

    /* Initialize the NetX Secure TLS system.  */
    nx_secure_tls_initialize();

    /* Create the TLS server thread to start handling incoming requests. */
    tx_thread_create(&tls_server_thread, "TLS Server thread", server_thread_entry, 0,
                   tls_server_thread_stack, sizeof(tls_server_thread_stack),
                   16, 16, 4, TX_AUTO_START);
    return;
}

/* Thread to handle the TLS Server instance. */
void server_thread_entry(ULONG thread_input)
{
UINT       status;
ULONG      actual_status;
NX_PACKET *send_packet;
NX_PACKET *receive_packet;
UCHAR receive_buffer[100];
ULONG bytes;

    NX_PARAMETER_NOT_USED(thread_input);

    /* Ensure the IP instance has been initialized.  */
    status =  nx_ip_status_check(&ip_0, NX_IP_INITIALIZE_DONE, &actual_status,
                                 NX_IP_PERIODIC_RATE);

    /* Create a TCP socket to use for our TLS session.  */
    status =  nx_tcp_socket_create(&ip_0, &tcp_socket, "TLS Server Socket",
                                   NX_IP_NORMAL, NX_FRAGMENT_OKAY,
                                   NX_IP_TIME_TO_LIVE, 8192, NX_NULL, NX_NULL);

    /* Create a TLS session for our socket.  */
    status =  nx_secure_tls_session_create(&tls_session,
                                        &nx_crypto_tls_ciphers_ecc,
                                        tls_crypto_metadata,
                                        sizeof(tls_crypto_metadata));

    status = nx_secure_tls_ecc_initialize(&tls_session,
                                          nx_crypto_ecc_supported_groups,
                                          nx_crypto_ecc_supported_groups_size,
                                          nx_crypto_ecc_curves);

     /* Set the packet reassembly buffer for this TLS session. */
     status = nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                      sizeof(tls_packet_buffer));

    /* Initialize an X.509 certificate and private ECC key for our TLS Session. */
    nx_secure_x509_certificate_initialize(&certificate, certificate_data, NX_NULL, 0,
                                          certificate_length, private_key,
                                          private_key_length,
                                          NX_SECURE_X509_KEY_TYPE_EC_DER);

    /* Add the initialized certificate as a local identity certificate. */
    nx_secure_tls_local_certificate_add(&tls_session, &certificate);


    /* Setup this thread to listen on the TCP socket.
       Port 443 is standard for HTTPS. */
    status =  nx_tcp_server_socket_listen(&ip_0, 443, &tcp_socket, 5, NX_NULL);

    while(1)
     {
         /* Accept a client TCP socket connection.  */
         status =  nx_tcp_server_socket_accept(&tcp_socket, NX_WAIT_FOREVER);

         /* Start the TLS Session using the connected TCP socket. */
         status = nx_secure_tls_session_start(&tls_session, &tcp_socket,
                                              NX_WAIT_FOREVER);

         /* Receive the HTTPS request. */
         status = nx_secure_tls_session_receive(&tls_session, &receive_packet,
                                                NX_WAIT_FOREVER);

if (status == NX_SUCCESS)
      {
         /* Extract the HTTP request information from the HTTPS request. */
            status = nx_packet_data_extract_offset(receive_packet, 0, receive_buffer,
                                                  100, &bytes);
         /* Display the HTTP request data. */
            receive_buffer[bytes] = 0;
            printf("Received data: %s\n", receive_buffer);

         /* Release the packet when done with it */
            nx_packet_release(receive_packet);
      }

         /* Allocate a TLS packet to send HTML data back to client. */
         status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                                NX_WAIT_FOREVER);

         /* Populate the packet with our HTTP response and HTML web page data. */
         nx_packet_data_append(send_packet, html_data, sizeof(html_data), &pool_0,
                               NX_WAIT_FOREVER);

         /* Send the HTTP response over the TLS Session, turning it into HTTPS. */
         status = nx_secure_tls_session_send(&tls_session, send_packet,
                                                 NX_WAIT_FOREVER);

         /* If the send fails, you must release the packet.  */
         if (status != NX_SUCCESS)
         {
              /* Release the packet since it was not sent.  */
              nx_packet_release(send_packet);
         }

         /* End the TLS session now that we have sent our HTTPS/HTML response. */
         status = nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);

         /* Check for errors to make sure the session ended cleanly! */

         /* Disconnect the TCP socket so we can be ready for the next request. */
         status =  nx_tcp_socket_disconnect(&tcp_socket, NX_WAIT_FOREVER);

         /* Unaccept the server socket.  */
         status =  nx_tcp_server_socket_unaccept(&tcp_socket);

         /* Setup server socket for listening again.  */
         status =  nx_tcp_server_socket_relisten(&ip_0, 443, &tcp_socket);
     }
}
```

**Figura 1,2 esempio di uso sicuro di NetX con NetX**

## <a name="a-note-on-tls-session-error-recovery"></a>Nota sul ripristino degli errori di sessione TLS

I sistemi di esempio descritti in precedenza mostrano rispettivamente le strutture di base per un client e un server TLS, ma per chiarezza la gestione degli errori viene omessa. Tuttavia, parte della sicurezza fornita da TLS dipende dalla corretta gestione delle condizioni di errore. In genere, i problemi potenziali più gravi verranno gestiti nello stack TLS stesso, ma è importante per l'applicazione TLS rispondere e ripristinare correttamente da errori TLS non gestiti nell'implementazione TLS.

Per illustrare la logica necessaria per la corretta gestione degli errori, la funzione seguente illustra una raccolta tipica di servizi API che può essere usata per gestire correttamente gli errori TLS e per reimpostare correttamente lo stato di TLS dopo che è stata rilevata una condizione di errore. A parte la sezione, se nota, la logica si applica alle istanze del server TLS e del client TLS.

Si noti che le chiamate API più importanti nella funzione sono per i servizi *nx_secure_tls_session_end*, che chiude la sessione TLS o l'handshake e *nx_secure_tls_session_reset*, che cancella lo stato della sessione TLS, in modo che l'istanza della struttura del controllo tls_session possa essere riutilizzata per una nuova sessione TLS. Si noti inoltre che *nx_secure_tls_session_reset* non cancella lo stato configurato dall'utente, ad esempio i certificati o i buffer assegnati, consentendo il riutilizzo della sessione senza chiamare di nuovo *nx_secure_tls_session_create* . Per cancellare completamente tutti gli Stati della sessione TLS, è possibile utilizzare il *nx_secure_tls_session_delete* del servizio.

```C
/* Define a helper function to clean up a broken TLS session (to be called on any
   error from nx_secure_tls_session_start onwards). Note that the variables
   tls_session, tcp_socket, and ip_0 are global in the above examples. */
VOID tls_session_error_cleanup(VOID)
{
UINT status;
UINT alert_level, alert_value;

      /* If we got an error back from a TLS API call, there may be an alert from the
         remote host. Extract the alert level and value to print out. Note that the TLS
         API will return NX_SECURE_TLS_ALERT_RECEIVED (0x114) if an alert was received.
         For other error codes the alert value and level are not valid. */
      status = nx_secure_tls_session_alert_value_get(&tls_session, &alert_level,
                                                     &alert_value);
      if(status)
      {
         printf("Pointer error in getting alert value.\n");
      }
      else
      {
         printf("Alert recieved. Value: %d, Level: %d\n", alert_value, alert_level);
      }

      /* End the TLS session. This is required to properly shut down the TLS
         connection. */
      status = nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);

      /* If the session did not shut down cleanly, this is a possible security issue. */
      if (status)
      {
         printf("Error in TLS session end: %x\n", status);
      }

      /* Reset the TLS session to re-use the control structure for the next connection.
         This API service resets the TLS session state but does not remove user-
         configured options such as certificates, PSKs, buffers, and cipher routines. */
      nx_secure_tls_session_reset(&tls_session);

      /* Disconnect the TCP socket, closing the connection. */
      status =  nx_tcp_socket_disconnect(&tcp_socket, NX_WAIT_FOREVER);

      /* Check for error.  */
      if (status)
      {
           printf("Error in TCP socket close: %x\n", status);
      }

   /* The following code applies only to a TLS server instance. */
   #if NX_SECURE_TLS_SERVER
      /* Unaccept the server socket.  */
      status =  nx_tcp_server_socket_unaccept(&tcp_socket);

      /* Check for error.  */
      if (status)
      {
           printf("Error in TCP socket unaccept: %x\n", status);
      }

      /* Setup server socket for listening again.  */
      status =  nx_tcp_server_socket_relisten(&ip_0, DEVICE_SERVER_PORT, &tcp_socket);

      /* Check for error.  */
      if (status)
      {
           printf("Error in TCP socket relisten: %x\n", status);
      }
#endif
} /* End function. */
```

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la creazione di NetX Secure. Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio:

| Definire | Significato |
|----------------------|------------------------------------------------|
| **NX_SECURE_DISABLE_ERROR_CHECKING**                | Definita, questa opzione rimuove il controllo degli errori di base di NetX Secure. Viene in genere usato dopo il debug dell'applicazione. |
| **NX_CRYPTO_MAX_RSA_MODULUS_SIZE**                  | Definita, questa opzione fornisce il modulo RSA massimo previsto in bit. Il valore predefinito è 4096 per un modulo a 4096 bit. Gli altri valori possono essere 3072, 2048 o 1024 (scelta non consigliata). |
| **NX_SECURE_ALLOW_SELF_SIGNED_CERTIFICATES**        | Definita, questa opzione consente a TLS di accettare certificati autofirmati da un host remoto. Per impostazione predefinita, i certificati del server autofirmato vengono rifiutati da TLS come misura di sicurezza. Se questa macro è definita, i certificati autofirmati devono comunque essere aggiunti all'archivio attendibile per essere accettati. |
| **NX_SECURE_ENABLE_CLIENT_CERTIFICATE_VERIFY**      | Definita, questa opzione Abilita la verifica facoltativa del certificato client X. 509 per i server TLS<sup>4</sup>.  |
| **NX_SECURE_ENABLE_PSK_CIPHERSUITES**               | Definita, questa opzione Abilita la funzionalità di chiave precondivisa (PSK). Non Disabilita i certificati digitali. |
| **NX_SECURE_TLS_CLIENT_DISABLED**                   | Definita, questa opzione rimuove tutti i codici dello stack TLS correlati alla modalità client TLS, riducendo il codice e l'utilizzo dei dati. |
| **NX_SECURE_TLS_SERVER_DISABLED**                   | Definita, questa opzione rimuove tutti i codici dello stack TLS correlati alla modalità server TLS, riducendo il codice e l'utilizzo dei dati.  |
| **NX_SECURE_DISABLE_ECC_CIPHERSUITE**               | Definita, questa opzione rimuove tutta la logica TLS per la crittografia a curva ellittica (ECC) ciphersuites. Questi ciphersuites sono facoltativi in TLS 1,2 e versioni precedenti e la loro disabilitazione può comportare una riduzione significativa del codice e della dimensione dei dati.|
| **NX_SECURE_TLS_ENABLE_TLS_1_3**                    | Definita, questa opzione Abilita la modalità TLSv 1.3. TLS 1,3 è la versione più recente di TLS ed è disabilitato per impostazione predefinita. |
| **NX_SECURE_TLS_ENABLE_TLS_1_0**                    | Definita, questa opzione Abilita la modalità legacy TLSv 1.0. TLSv 1.0 è considerato obsoleto, quindi deve essere abilitato solo per la compatibilità con le versioni precedenti. |
| **NX_SECURE_TLS_ENABLE_TLS_1_1**                    | Definita, questa opzione Abilita la modalità legacy TLSv 1.1. TLSv 1.1 è considerato obsoleto, quindi deve essere abilitato solo per la compatibilità con le versioni precedenti. |
| **NX_SECURE_TLS_DISABLE_TLS_1_1**                   | Definita, questa opzione Disabilita la modalità TLSv 1.1. Viene definito per impostazione predefinita. TLSv 1.1 è disabilitato a favore dell'uso di TLSv 1.2<sup>5</sup>più protetti.  |
| **NX_SECURE_X509_STRICT_NAME_COMPARE**              | Definita, questa opzione Abilita il confronto dei nomi distinti per i certificati X. 509 per la ricerca e la verifica dei certificati. Il valore predefinito è confrontare solo i campi del nome comune dei nomi distinti.|
| **NX_SECURE_X509_USE_EXTENDED_DISTINGUISHED_NAMES** | Definita, questa opzione Abilita i campi del nome distinto X. 509 facoltativi, a scapito dell'utilizzo di memoria aggiuntivo per i certificati X. 509. |

4. Si noti che questa opzione consente solo di collegare il codice nell'applicazione. La funzionalità deve essere abilitata con il servizio API nx_secure_tls_session_client_verify_enable o configurata usando nx_secure_tls_session_x509_client_verify_configure per usare la verifica del certificato client.

5. Si noti che è anche possibile disabilitare TLSv 1.2 Se si usa solo TLS 1,0 o TLS 1,1. Questa operazione non è tuttavia consigliata e non è supportata direttamente.
