---
title: Capitolo 2-installazione e uso di Azure RTO NetX Secure DTLS
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente DTLS protetto NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 3533471edf17ec6e812027ef0af672a00773f968
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821596"
---
# <a name="chapter-2-installation-and-use-of-azure-rtos-netx-secure-dtls"></a>Capitolo 2: installazione e uso di Azure RTO NetX Secure DTLS

Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente DTLS protetto NetX di Azure RTO.

## <a name="product-distribution"></a>Distribuzione del prodotto

NetX Secure è disponibile all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) . Il pacchetto include i file di origine, i file di inclusione e un file PDF che contiene questo documento, come indicato di seguito:

- **nx_secure_dtls_api. h** File di intestazione dell'API pubblica per NetX Secure DTLS
- **nx_secure_dtls_user. h** Il file di intestazione definito dall'utente per NetX Secure DTLS
- **nx_secure_ Port. h** Definizioni specifiche della piattaforma per NetX Secure
- **nx_secure_dtls. h** File di intestazione per NetX Secure DTLS
- **nx_secure_tls. h** File di intestazione per NetX Secure TLS
- file di origine **nx_secure_dtls \* . c/h** c/h per NETX Secure DTLS
- nx_secure_tls file di origine c/h c/h per NetX Secure TLS **\***
- file di origine **nx_crypto \* . c/h** c/h per la crittografia sicura NETX
- **nx_secure_x509 \*** file di origine c/h c/h per i certificati digitali X. 509.
- **demo_netx_secure_dtls. c** File di origine C per NetX Secure DTLS demo
- **NetX_Secure_DTLS_User_Guide.pdf** Descrizione PDF del prodotto NetX Secure

> [!NOTE]
> I file nx_crypto * vengono forniti per diverse piattaforme hardware in una sottodirectory della directory padre protetta NetX.

## <a name="netx-secure-dtls-installation"></a>Installazione di DTLS Secure NetX

Per usare NetX Secure DTLS, l'intera distribuzione indicata in precedenza deve essere copiata nello stesso livello di directory in cui è installato NetX. Ad esempio, se NETX è installato nella directory "*\threadx\arm7\NetX*", il *nx_secure \* . \** directory deve essere copiato in "*\threadx\arm7\NetXSecure*".

## <a name="using-netx-secure-dlts"></a>Uso di NetX Secure DLTS

L'uso di NetX Secure DTLS è semplice. Il codice dell'applicazione deve includere *nx_secure_dtls_api. h* dopo aver incluso *tx_api. h* e *nx_api. h* (rispettivamente per threadX e NETX). Una volta incluso *nx_secure_dtls_api. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione NETX Secure DTLS specificate più avanti in questa guida. L'applicazione deve inoltre importare i *file \* nx_secure \* .* files in una libreria NetXSecure e i file *nx_crypto \* \** specifici della piattaforma in una libreria NetXCrypto che vengono quindi collegati al file binario dell'applicazione finale.

## <a name="small-example-system-dtls-client"></a>Sistema di esempio di piccole dimensioni (client DTLS)

Un esempio di come è facile usare NetX Secure DTLS è descritto nella figura 1,1, che viene visualizzato di seguito e illustra un semplice client DTLS, progettato per funzionare con un server DTLS OpenSSL (o simile). Si noti che la struttura del programma client DTLS è molto simile a un client TLS protetto da NetX (vedere la documentazione di NetX Secure TLS). Questo è dovuto al fatto che il protocollo DTLS è essenzialmente una versione di TLS per l'uso su protocolli di rete di trasporto non affidabili, ad esempio UDP.

```C
#include "tx_api.h"
#include "nx_api.h"
#include "nx_secure_dtls_api.h"

/* Define the size of our application stack. */
#define     DEMO_STACK_SIZE             4096

/* Define the remote server IP address using NetX IP_ADDRESS macro. */
#define     REMOTE_SERVER_IP_ADDRESS      IP_ADDRESS(192, 168, 1, 1)

/* Define the remote server port. */
#define     REMOTE_SERVER_PORT           4443

/* Define the size of the buffer used for incoming certificates. The
   Buffer will contain both the raw certificate data and an instance
   of the NX_SECURE_X509_CERT structure used for X.509 parsing. */
#define     REMOTE_CERT_BUFFER_SIZE     (sizeof(NX_SECURE_X509_CERT) + 2000)

/* Define the number of certificates we expect to receive from the server
   so we can allocate enough space for them. */
#define     REMOTE_CERT_NUMBER          2

/* Define the ThreadX and NetX object control blocks...  */

NX_PACKET_POOL          pool_0;
NX_IP                   ip_0;
NX_UDP_SOCKET udp_socket;
NX_SECURE_DTLS_SESSION dtls_session;
NX_SECURE_X509_CERTIFICATE dtls_certificate;

/* Define space for remote certificate storage. The size of the
buffer is determined by the expected number of certificates times
the expected size of each certificate.   */
UCHAR remote_certificate_buffer[REMOTE_CERT_BUFFER_SIZE * REMOTE_CERT_NUMBER];

/* Define some data to send to the DTLS server. */
UCHAR request_data[] = { … };

/* Define the IP thread's stack area.  */
ULONG ip_thread_stack[3 * 1024 / sizeof(ULONG)];

/* Define packet pool for the demonstration.  */
#define NX_PACKET_POOL_SIZE ((1536 + sizeof(NX_PACKET)) * 32)

ULONG packet_pool_area[NX_PACKET_POOL_SIZE/sizeof(ULONG) + 64 / sizeof(ULONG)];

/* Define the ARP cache area.  */
ULONG arp_space_area[512 / sizeof(ULONG)];

/* Define the DTLS Client thread.  */
ULONG             dtls_client_thread_stack[6 * 1024 / sizeof(ULONG)];
TX_THREAD         dtls_client_thread;
void              client_thread_entry(ULONG thread_input);

/* Define the DTLS packet reassembly buffer. */
UCHAR dtls_packet_buffer[4000];

/* Define the metadata area for TLS cryptography. The actual size needed can be
   Ascertained by calling nx_secure_tls_metadata_size_calculate.
*/
UCHAR dtls_crypto_metadata[14000];

/* Pointer to the TLS/DTLS ciphersuite table that is included in the platform-
specific cryptography subdirectory. The table maps the cryptographic routines for
the platform to function pointers usable by the DTLS library.
*/
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Binary data for the DTLS Client X.509 trusted root CA certificate: ASN.1 DER-
   encoded. A trusted certificate must be provided for TLS/DTLS Client applications
   (unless an alternate authentication mechanism is used, such as PSK) or DTLS will
treat all certificates as untrusted and the handshake will fail.
*/
const UCHAR trusted_ca_data[] = { … }; /* DER-encoded binary certificate. */
const UINT trusted_ca_length[] = 0x574;

/* Define the application – initialize drivers and UDP setup.  */
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
    status = nx_ip_create(&ip_0, …);

    /* Enable ARP and supply ARP cache memory for IP Instance 0. Check status for
         errors. */
    status =  nx_arp_enable(&ip_0, (void *)arp_space_area, sizeof(arp_space_area));

    /* Enable UDP traffic. Check status for errors. */
    status =  nx_udp_enable(&ip_0);

    status =  nx_ip_fragment_enable(&ip_0);

    /* Initialize the NetX Secure TLS/DTLS system.  */
   nx_secure_tls_initialize();

    /* Create the client thread to start handling incoming requests. */
    tx_thread_create(&dtls_client_thread, "DTLS Client thread", client_thread_entry,
        0, dtls_client_thread_stack, sizeof(dtls_client_thread_stack),
        16, 16, 4, TX_AUTO_START);
}

     /* Thread to handle the DTLS Client instance. */
void client_thread_entry(ULONG thread_input)
{
    UINT       status;
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

    /* Check status for errors... */

    /* Create a UDP socket to use for our DTLS session.  */
    status =  nx_udp_socket_create(&ip_0, &udp_socket, "DTLS Client Socket",
        NX_IP_NORMAL, NX_FRAGMENT_OKAY, NX_IP_TIME_TO_LIVE, 8192);

    /* Check status for errors... */

    /* Create a DTLS session for our socket. This sets up the DTLS session object for
            later use with encryption, packet buffer space for decryption, and buffer
    space for incoming server X.509 certificates. */
    status =  nx_secure_dtls_session_create(&dtls_session,
        &nx_crypto_tls_ciphers,
        tls_crypto_metadata,
        sizeof(tls_crypto_metadata),
        dtls_packet_buffer,
        sizeof(dtls_packet_buffer),
        REMOTE_CERT_NUMBER,
        remote_certificate_buffer,
        sizeof(remote_certificate_buffer) );

    /* Initialize an X.509 certificate with our CA root certificate data. */
    nx_secure_x509_certificate_initialize(&certificate, trusted_ca_data,
        trusted_ca_length, NX_NULL, 0, NX_NULL, 0,
        NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the initialized certificate as a trusted root certificate. */
    nx_secure_dtls_session_trusted_certificate_add(&dtls_session, &certificate);

    /* Setup this thread to open a connection on the UDP socket to a remote server.
       The IP address can be used directly or it can be obtained via DNS or other
       means.  */
   server_ipv4_address = REMOTE_SERVER_IP_ADDRESS;

   /* Check for errors…  */

    /* Start the DTLS Session using the given UDP socket, remote server IP Address,
        and remote server port. */
    status = nx_secure_dtls_client_session_start(&dtls_session, &udp_socket,
        &ip_address, REMOTE_SERVER_PORT, NX_WAIT_FOREVER);

        /* Allocate a DTLS packet to send some encrypted data to the server. */
        status = nx_secure_dtls_packet_allocate(&dtls_session, &pool_0, &send_packet,
     NX_TLS_PACKET, NX_WAIT_FOREVER);

        /* Check for errors…  */

         /* Populate the packet with some data. */
        nx_packet_data_append(send_packet, request_data, sizeof(request_data), &pool_0,
            NX_WAIT_FOREVER);

         /* Send the request over the DTLS Session, encrypting it before sending. */
    status = nx_secure_dtls_session_send(&dtls_session, send_packet, NX_WAIT_FOREVER);

        /* Check for errors…  */
        if (status)
        {
              /* Release the packet since we could not send it.  */
              nx_packet_release(send_packet);
        }

     /* Receive the response from the server. */
    status = nx_secure_dtls_session_receive(&dtls_session, &receive_packet,
       NX_WAIT_FOREVER);

    /* Extract the data we received from the remote server. */
    status = nx_packet_data_extract_offset(receive_packet, 0, receive_buffer, 100,
        &bytes);
    /* Display the response data. */
    receive_buffer[bytes] = 0;
    printf("Received data: %s\n", receive_buffer)
     /* End the DTLS session now that we have received our response. */
    status = nx_secure_dtls_session_end(&tls_session, NX_WAIT_FOREVER)

     /* Check for errors to make sure the session ended cleanly. */
     /* Clean up the UDP socket. */
    status =  nx_udp_socket_delete(&udp_socket)

    /* Check for errors... */

}
```

**Figura 1,1 esempio di uso sicuro di NetX con NetX**

## <a name="small-example-system-dtls-server"></a>Sistema di esempio di piccole dimensioni (server DTLS)

Un esempio di come è facile usare NetX Secure è descritto nella figura 1,2, che viene visualizzato di seguito e viene illustrato un semplice server DTLS. Si noti che le funzionalità del server DTLS sono piuttosto diverse dal client di DTLS e dal client/server TLS poiché il server DTLS deve gestire più richieste client in ingresso su una singola porta UDP, archiviata nell'istanza del server DTLS.

```C
#include "tx_api.h"
#include "nx_api.h"
#include "nx_secure_dtls_api.h"

#define     DEMO_STACK_SIZE         4096

/* Define the ThreadX and NetX object control blocks.
   NOTE: These must be initialized for the target platform. See the
   NetX documentation for details. */

NX_PACKET_POOL          pool_0;
NX_IP                   ip_0;

/* Define the IP thread's stack area.  */
ULONG ip_thread_stack[3 * 1024 / sizeof(ULONG)];

/* Define packet pool for the demonstration.  */
#define NX_PACKET_POOL_SIZE ((1536 + sizeof(NX_PACKET)) * 32)

ULONG packet_pool_area[NX_PACKET_POOL_SIZE/sizeof(ULONG) + 64 / sizeof(ULONG)];

/* Define the ARP cache area.  */
ULONG arp_space_area[512 / sizeof(ULONG)];


/* Define the DTLS Server thread.  */
ULONG             dtls_server_thread_stack[6 * 1024 / sizeof(ULONG)];
TX_THREAD         dtls_server_thread;
void              server_thread_entry(ULONG thread_input);

/* Define the DTLS packet reassembly buffer. */
UCHAR packet_buffer[4000];

/* Define the metadata area for TLS/DTLS cryptography. The actual size needed can be
   Ascertained by calling nx_secure_tls_metadata_size_calculate.
*/
UCHAR crypto_metadata_buffer[4000];

/* Pointer to the TLS ciphersuite table that is included in the platform-specific
   cryptography subdirectory. The table maps the cryptographic routines for the
   platform to function pointers usable by the TLS library. The TLS structure is also
   used for DTLS. See the NetX Secure TLS User Guide for more information.
*/
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Define our server certificate structure. */
NX_SECURE_X509_CERTIFICATE certificate;

/* DER-encoded certificate data for the server identity X.509 certificate. */
UCHAR device_cert_der[] = { … };
UCHAR device_cert_der_length[] = { … };
UCHAR device_cert_key_der[] = { … };
UCHAR device_cert_key_der_length[] = { … };

/* Define the number of sessions we want to allocate to our DTLS Server. */
#define DTLS_SERVER_SESSIONS (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION) * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive. NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session,
    NXD_ADDRESS *ip_address, UINT port)
{
    /* NOTE: proper inter-thread communication procedures (e.g. mutex handling)
             Omitted for clarity. */

    /* Notify application thread that a connection request has been received. */
    connect_flag = 1;
    new_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Receive notify callback routine invoked when DTLS application data is received
   on an existing DTLS server session. */
UINT dtls_server_receive_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Define the application – initialize drivers and UDP setup.  */
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
    status = nx_ip_create(&ip_0, …);

    /* Enable ARP and supply ARP cache memory for IP Instance 0. Check status for
         errors. */
    status =  nx_arp_enable(&ip_0, (void *)arp_space_area, sizeof(arp_space_area));

    /* Enable UDP traffic. Check status for errors. */
    status =  nx_udp_enable(&ip_0);

    status =  nx_ip_fragment_enable(&ip_0);

    /* Initialize the NetX Secure TLS/DTLS system.  */
    nx_secure_tls_initialize();

     /* Create the server thread to start handling incoming requests. */
    tx_thread_create(&dtls_server_thread, "DTLS Server thread", server_thread_entry,
       0, dtls_server_thread_stack, sizeof(dtls_server_thread_stack),
       16, 16, 4, TX_AUTO_START);
}


/* Primary application thread for handling DTLS server operations. */
void server_thread_entry(ULONG thread_input)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UCHAR receive_buffer[100];
    ULONG bytes;
    UINT status;

    NX_PARAMETER_NOT_USED(thread_input);

    /* Ensure the IP instance has been initialized.  */
    status =  nx_ip_status_check(&ip_0, NX_IP_INITIALIZE_DONE, &actual_status,
        NX_IP_PERIODIC_RATE);

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance, LOCAL_SERVER_PORT,
        NX_IP_PERIODIC_RATE, dtls_server_session_buffer,
        sizeof(dtls_server_session_buffer),
        &tls_crypto_table, crypto_metadata_buffer,
        sizeof(crypto_metadata_buffer), packet_buffer,
        sizeof(packet_buffer),
        dtls_server_connect_notify,
        dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                        device_cert_der_len, NX_NULL, 0,
                        device_cert_key_der, device_cert_key_der_len,
                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server, &certificate, 1);


    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Check for new connections. Muxtex handling omitted for clarity. */
        if(connect_flag)
        {
            /* We have a new connection attempt, start the DTLS session. */
            status = nx_secure_dtls_server_session_start(new_dtls_session,
                                            NX_IP_PERIODIC_RATE);

        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            status = nx_secure_dtls_session_receive(receive_dtls_session, &receive_packet,
            NX_IP_PERIODIC_RATE);


            /* Process received data… */
            status = nx_packet_data_extract_offset(receive_packet, 0, receive_buffer, 100,
                 &bytes);
            /* Display the Client request data. */
           receive_buffer[bytes] = 0;
           printf("Received data: %s\n", receive_buffer);


            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session, &packet_pool,
                &send_packet, NX_IP_PERIODIC_RATE);


           /* Populate the packet with our response data. */
           nx_packet_data_append(send_packet, response_data, response_data_length,
                &pool_0, NX_WAIT_FOREVER);

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,send_packet);
        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* Server processing is done, stop the server instance from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}
```

**Figura 1,2 esempio di NetX Secure DTLS server**

## <a name="configuration-options"></a>Opzioni di configurazione

Sono disponibili diverse opzioni di configurazione per la creazione di NetX Secure.
Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio:

| Definire                                                 | Significato                                                                                                                                                                                                                |
|--------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **NX_SECURE_ENABLE_DTLS**                           | Per abilitare la logica DTLS in NetX Secure, è necessario definire questa macro.                                                                                                                                                       |
| **NX_SECURE_DISABLE_ERROR_CHECKING**               | Definita, questa opzione rimuove il controllo degli errori di base di NetX Secure. Viene in genere usato dopo il debug dell'applicazione.                                                                                     |
| **NX_SECURE_TLS_CLIENT_DISABLED**                  | Definita, questa opzione rimuove tutti i codici dello stack TLS/DTLS correlati alla modalità client, riducendo il codice e l'utilizzo dei dati.                                                                                                            |
| **NX_SECURE_TLS_SERVER_DISABLED**                  | Definita, questa opzione rimuove tutti i codici dello stack TLS/DTLS correlati alla modalità server, riducendo il codice e l'utilizzo dei dati.                                                                                                            |
| **NX_SECURE_ENABLE_PSK_CIPHERSUITES**              | Definita, questa opzione Abilita la funzionalità di chiave precondivisa (PSK). Non Disabilita i certificati digitali.                                                                                                        |
| **NX_SECURE_X509_STRICT_NAME_COMPARE**            | Definita, questa opzione Abilita il confronto dei nomi distinti per i certificati X. 509 per la ricerca e la verifica dei certificati. Il valore predefinito è confrontare solo i campi nome comune, ovvero i nomi distinti. |
| **NX_SECURE_X509_USE_EXTENDED_DISTINGUISHED_NAMES**     | Definita, questa opzione Abilita i campi del nome distinto X. 509 facoltativi, a scapito dell'utilizzo di memoria aggiuntivo per i certificati X. 509.                                                                               |
| **NX_CRYPTO_MAX_RSA_MODULUS_SIZE**                | Definita, questa opzione fornisce il modulo RSA massimo previsto in bit. Il valore predefinito è 4096 per un modulo a 4096 \- bit. Gli altri valori possono essere 3072, 2048 o 1024 (scelta non consigliata).                               |
