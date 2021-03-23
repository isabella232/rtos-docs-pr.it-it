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
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-secure"></a><span data-ttu-id="73769-103">Capitolo 2-installazione e uso di Azure RTO NetX Secure</span><span class="sxs-lookup"><span data-stu-id="73769-103">Chapter 2 - Installation and use of Azure RTOS NetX Secure</span></span>

<span data-ttu-id="73769-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente protetto Azure RTO NetX.</span><span class="sxs-lookup"><span data-stu-id="73769-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Secure component.</span></span>

## <a name="product-version-number"></a><span data-ttu-id="73769-105">Numero di versione del prodotto</span><span class="sxs-lookup"><span data-stu-id="73769-105">Product Version Number</span></span>

<span data-ttu-id="73769-106">L'utente può verificare il numero di versione del prodotto individuando i simboli seguenti in nx_secure_tls. h:</span><span class="sxs-lookup"><span data-stu-id="73769-106">User may verify the product version number by finding the following symbols in nx_secure_tls.h:</span></span>

<span data-ttu-id="73769-107">***NETX_SECURE_MAJOR_VERSION***</span><span class="sxs-lookup"><span data-stu-id="73769-107">***NETX_SECURE_MAJOR_VERSION***</span></span>

<span data-ttu-id="73769-108">***NETX_SECURE_MINOR_VERSION***</span><span class="sxs-lookup"><span data-stu-id="73769-108">***NETX_SECURE_MINOR_VERSION***</span></span>

<span data-ttu-id="73769-109">Le versioni del Service Pack hanno il simbolo seguente definito per indicare il numero Service Pack:</span><span class="sxs-lookup"><span data-stu-id="73769-109">Service Pack releases has the following symbol defined to indicate the service pack number:</span></span>

<span data-ttu-id="73769-110">***NETX_SECURE_SERVICE_PACK_VERSION***</span><span class="sxs-lookup"><span data-stu-id="73769-110">***NETX_SECURE_SERVICE_PACK_VERSION***</span></span>

## <a name="product-distribution"></a><span data-ttu-id="73769-111">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="73769-111">Product Distribution</span></span>

<span data-ttu-id="73769-112">NetX Secure è disponibile all'indirizzo [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx) .</span><span class="sxs-lookup"><span data-stu-id="73769-112">NetX Secure is available at [https://github.com/azure-rtos/netx](https://github.com/azure-rtos/netx).</span></span> <span data-ttu-id="73769-113">Il pacchetto include i file di origine, i file di inclusione e un file PDF che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="73769-113">The package includes source files, include files, and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="73769-114">**nx_secure_tls_api. h** File di intestazione dell'API pubblica per NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="73769-114">**nx_secure_tls_api.h** Public API header file for NetX Secure TLS</span></span>
- <span data-ttu-id="73769-115">**nx_secure_tls_user. h** Il file di intestazione definito dall'utente per NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="73769-115">**nx_secure_tls_user.h** User defines header file for NetX Secure TLS</span></span>
- <span data-ttu-id="73769-116">**nx_secure_tls_port. h** Definizioni specifiche della piattaforma per NetX Secure</span><span class="sxs-lookup"><span data-stu-id="73769-116">**nx_secure_tls_port.h** Platform-specific definitions for NetX Secure</span></span>
- <span data-ttu-id="73769-117">**nx_secure_tls. h** File di intestazione per NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="73769-117">**nx_secure_tls.h** Header file for NetX Secure TLS</span></span>
- <span data-ttu-id="73769-118">**nx_secure_tls&#42;. c/h** File di origine C/H per NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="73769-118">**nx_secure_tls&#42;.c/h** C/H Source files for NetX Secure TLS</span></span>
- <span data-ttu-id="73769-119">**nx_crypto&#42;. c/h** File di origine C/H per crittografia sicura NetX</span><span class="sxs-lookup"><span data-stu-id="73769-119">**nx_crypto&#42;.c/h** C/H Source files for NetX Secure Cryptography</span></span>
- <span data-ttu-id="73769-120">**nx_secure_x509&#42;. c/h** File di origine C/H per i certificati digitali X. 509.</span><span class="sxs-lookup"><span data-stu-id="73769-120">**nx_secure_x509&#42;.c/h** C/H Source files for X.509 digital certificates.</span></span>
- <span data-ttu-id="73769-121">**demo_netx_secure_tls. c** File di origine C per NetX Secure TLS demo</span><span class="sxs-lookup"><span data-stu-id="73769-121">**demo_netx_secure_tls.c** C Source file for NetX Secure TLS Demo</span></span>
- <span data-ttu-id="73769-122">**NetX_Secure_User_Guide.pdf** Descrizione PDF del prodotto NetX Secure</span><span class="sxs-lookup"><span data-stu-id="73769-122">**NetX_Secure_User_Guide.pdf** PDF description of NetX Secure product</span></span>

> [!NOTE]
> <span data-ttu-id="73769-123">I file nx_crypto \* vengono forniti per diverse piattaforme hardware in una sottodirectory della directory padre protetta NetX.</span><span class="sxs-lookup"><span data-stu-id="73769-123">The nx_crypto\* files are provided for different hardware platforms in a subdirectory of the NetX Secure parent directory.</span></span>

## <a name="netx-secure-installation"></a><span data-ttu-id="73769-124">Installazione sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="73769-124">NetX Secure Installation</span></span>

<span data-ttu-id="73769-125">Per poter usare NetX Secure, l'intera distribuzione indicata in precedenza deve essere copiata nello stesso livello di directory in cui è installato NetX.</span><span class="sxs-lookup"><span data-stu-id="73769-125">In order to use NetX Secure, the entire distribution mentioned previously should be copied to the same directory level where NetX is installed.</span></span> <span data-ttu-id="73769-126">Ad esempio, se NetX è installato nella directory "*\threadx\arm7\NetX*" \*, il nx_secure \* *.*</span><span class="sxs-lookup"><span data-stu-id="73769-126">For example, if NetX is installed in the directory "*\threadx\arm7\NetX*" then the *nx_secure\*\*.*</span></span> <span data-ttu-id="73769-127">le directory devono essere copiate in "*\threadx\arm7\NetXSecure*".</span><span class="sxs-lookup"><span data-stu-id="73769-127">directories should be copied into "*\threadx\arm7\NetXSecure*".</span></span>

## <a name="using-netx-secure"></a><span data-ttu-id="73769-128">Uso di NetX Secure</span><span class="sxs-lookup"><span data-stu-id="73769-128">Using NetX Secure</span></span>

<span data-ttu-id="73769-129">L'uso di NetX Secure TLS è semplice.</span><span class="sxs-lookup"><span data-stu-id="73769-129">Using NetX Secure TLS is straightforward.</span></span> <span data-ttu-id="73769-130">In pratica, il codice dell'applicazione deve includere *nx_secure_tls_api. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter usare threadX e NETX.</span><span class="sxs-lookup"><span data-stu-id="73769-130">Basically, the application code must include *nx_secure_tls_api.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX.</span></span> <span data-ttu-id="73769-131">Una volta incluso *nx_secure_tls_api. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione NETX Secure specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="73769-131">Once *nx_secure_tls_api.h* is included, the application code is then able to make the NetX Secure function calls specified later in this guide.</span></span> <span data-ttu-id="73769-132">L'applicazione deve inoltre importare la \*nx_secure \* *.*</span><span class="sxs-lookup"><span data-stu-id="73769-132">The application must also import the *nx_secure\*\*.*</span></span> <span data-ttu-id="73769-133">file in una libreria NetXSecure e \*nx_crypto \* \*\* specifici della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="73769-133">files into a NetXSecure library, and the platform-specific *nx_crypto\*\*.*</span></span> <span data-ttu-id="73769-134">file in una libreria NetXCrypto.</span><span class="sxs-lookup"><span data-stu-id="73769-134">files into a NetXCrypto library.</span></span>

## <a name="small-example-system-tls-client"></a><span data-ttu-id="73769-135">Sistema di esempio di piccole dimensioni (client TLS)</span><span class="sxs-lookup"><span data-stu-id="73769-135">Small Example System (TLS Client)</span></span>

<span data-ttu-id="73769-136">Un esempio di come è facile usare NetX Secure è descritto nella figura 1,1, che viene visualizzato di seguito.</span><span class="sxs-lookup"><span data-stu-id="73769-136">An example of how easy it is to use NetX Secure is described in Figure 1.1, which appears below.</span></span> <span data-ttu-id="73769-137">Questo esempio illustra un semplice client TLS, che usa moduli di crittografia software (non specifici dell'hardware) per la crittografia.</span><span class="sxs-lookup"><span data-stu-id="73769-137">This demonstrates a simple TLS Client, using software crypto modules (not hardware specific) for encryption.</span></span> <span data-ttu-id="73769-138">È progettato per l'uso con il server echo OpenSSL Reverse (OpenSSL s_server-REV).</span><span class="sxs-lookup"><span data-stu-id="73769-138">It is designed to work with the OpenSSL reverse-echo server (openssl s_server -rev).</span></span>

<span data-ttu-id="73769-139">Si noti che per eseguire questo esempio, sarà necessario un certificato della CA X. 509 per autenticare il certificato del server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="73769-139">Note that in order to run this example, you will need an X.509 CA certificate to authenticate your target server's certificate.</span></span> <span data-ttu-id="73769-140">Per l'esempio OpenSSL, è sufficiente una semplice infrastruttura a chiave pubblica (PKI) a 2 livelli, ovvero un certificato CA radice-> >certificato server.</span><span class="sxs-lookup"><span data-stu-id="73769-140">For the OpenSSL example, a simple 2-level PKI (root CA certificate-> >server certificate) will suffice.</span></span> <span data-ttu-id="73769-141">Sarà necessario compilare la matrice "trusted_ca_data" con una versione binaria con codifica DER del certificato della CA e aggiornare la variabile "trusted_ca_length" per riflettere la lunghezza effettiva del certificato.</span><span class="sxs-lookup"><span data-stu-id="73769-141">You will need to fill in the "trusted_ca_data" array with a DER-encoded binary version of your CA certificate and update the "trusted_ca_length" variable to reflect your certificate's actual length.</span></span>

<span data-ttu-id="73769-142">Sarà inoltre necessario il driver di rete per l'hardware (sostituire il parametro "nx_driver_xx" nella chiamata nx_ip_create).</span><span class="sxs-lookup"><span data-stu-id="73769-142">You will also need the network driver for your hardware (replace "nx_driver_xx" parameter in nx_ip_create call).</span></span>

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

<span data-ttu-id="73769-143">**Figura 1,1 esempio di uso sicuro di NetX con NetX**</span><span class="sxs-lookup"><span data-stu-id="73769-143">**Figure 1.1 Example of NetX Secure use with NetX**</span></span>

## <a name="small-example-system-tls-web-server"></a><span data-ttu-id="73769-144">Sistema di esempio di piccole dimensioni (server Web TLS)</span><span class="sxs-lookup"><span data-stu-id="73769-144">Small Example System (TLS Web Server)</span></span>

<span data-ttu-id="73769-145">Un esempio di come è facile usare NetX Secure è descritto nella figura 1,1, che viene visualizzato di seguito e viene illustrato un semplice server Web TLS (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="73769-145">An example of how easy it is to use NetX Secure is described in Figure 1.1, which appears below and demonstrates a simple TLS Web Server (HTTPS).</span></span>

<span data-ttu-id="73769-146">Si noti che per eseguire questo esempio, è necessario un certificato X. 509 per identificare il server nei client TLS.</span><span class="sxs-lookup"><span data-stu-id="73769-146">Note that in order to run this example, you will need an X.509 certificate to identify your server to TLS clients.</span></span> <span data-ttu-id="73769-147">Per la maggior parte dei Web browser è sufficiente un certificato autofirmato semplice.</span><span class="sxs-lookup"><span data-stu-id="73769-147">For most web browers a simple self-signed certificate should be sufficient.</span></span> <span data-ttu-id="73769-148">Il browser si lamenta di non essere in grado di autenticare il server e, in alcuni casi, potrebbe non essere in grado di stabilire una connessione TLS/HTTPS al server<sup>3</sup>.</span><span class="sxs-lookup"><span data-stu-id="73769-148">Your browser will complain about not being able to authenticate the server and in some cases may be unable to establish a TLS/HTTPS connection to your server<sup>3</sup>.</span></span> <span data-ttu-id="73769-149">Sarà necessario compilare la matrice "certificate_data" con una versione binaria con codifica DER del certificato del server e aggiornare la variabile "certificate_length" per riflettere la lunghezza effettiva del certificato.</span><span class="sxs-lookup"><span data-stu-id="73769-149">You will need to fill in the "certificate_data" array with a DER-encoded binary version of your server certificate and update the "certificate_length" variable to reflect your certificate's actual length.</span></span> <span data-ttu-id="73769-150">È anche necessario compilare la matrice "private_key" con una versione con codifica DER della chiave privata del certificato, formattata con PKCS # 1 per la chiave RSA e RFC 5915 per le chiavi ECC.</span><span class="sxs-lookup"><span data-stu-id="73769-150">You also need to fill in the "private_key" array with a DER-encoded version of your certificate's private key, formatted using PKCS#1 for RSA key and RFC 5915 for ECC keys.</span></span> <span data-ttu-id="73769-151">Compilare la variabile "private_key_length" con la lunghezza effettiva dei dati della chiave.</span><span class="sxs-lookup"><span data-stu-id="73769-151">Fill in the "private_key_length" variable with the actual length of your key data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73769-152">Alcuni browser (in particolare alcune versioni del browser Chrome) potrebbero rifiutare i certificati autofirmati.</span><span class="sxs-lookup"><span data-stu-id="73769-152">Some browsers (particularly some versions of the Chrome browser) may reject self-signed certificates.</span></span> <span data-ttu-id="73769-153">In questo caso è possibile creare un'infrastruttura a chiave pubblica a due livelli con un certificato CA radice usato per firmare il certificato del server.</span><span class="sxs-lookup"><span data-stu-id="73769-153">In this case you can create a 2-level PKI with a root CA certificate that is used to sign your server certificate.</span></span> <span data-ttu-id="73769-154">In questa situazione, il certificato CA radice viene installato come certificato radice attendibile nel browser.</span><span class="sxs-lookup"><span data-stu-id="73769-154">In this situation, the root CA certificate is installed as a trusted root certificate in your browser.</span></span> <span data-ttu-id="73769-155">!!!</span><span class="sxs-lookup"><span data-stu-id="73769-155">!!!</span></span> <span data-ttu-id="73769-156">IMPORTANTE: rimuovere il certificato CA radice dal browser al termine e non usarlo per applicazioni di produzione!!!</span><span class="sxs-lookup"><span data-stu-id="73769-156">IMPORTANT – remove your root CA certificate from your browser when done and do not use it for any production applications !!!</span></span>

<span data-ttu-id="73769-157">Sarà inoltre necessario il driver di rete per l'hardware (sostituire il parametro "nx_driver_xx" nella chiamata nx_ip_create).</span><span class="sxs-lookup"><span data-stu-id="73769-157">You will also need the network driver for your hardware (replace "nx_driver_xx" parameter in nx_ip_create call).</span></span>

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

<span data-ttu-id="73769-158">**Figura 1,2 esempio di uso sicuro di NetX con NetX**</span><span class="sxs-lookup"><span data-stu-id="73769-158">**Figure 1.2 Example of NetX Secure use with NetX**</span></span>

## <a name="a-note-on-tls-session-error-recovery"></a><span data-ttu-id="73769-159">Nota sul ripristino degli errori di sessione TLS</span><span class="sxs-lookup"><span data-stu-id="73769-159">A Note on TLS Session Error Recovery</span></span>

<span data-ttu-id="73769-160">I sistemi di esempio descritti in precedenza mostrano rispettivamente le strutture di base per un client e un server TLS, ma per chiarezza la gestione degli errori viene omessa.</span><span class="sxs-lookup"><span data-stu-id="73769-160">The example systems described above show the basic outlines for a TLS Client and Server, respectively, but for clarity the error handling is omitted.</span></span> <span data-ttu-id="73769-161">Tuttavia, parte della sicurezza fornita da TLS dipende dalla corretta gestione delle condizioni di errore.</span><span class="sxs-lookup"><span data-stu-id="73769-161">However, part of the security TLS provides is dependent on the proper handling of error conditions.</span></span> <span data-ttu-id="73769-162">In genere, i problemi potenziali più gravi verranno gestiti nello stack TLS stesso, ma è importante per l'applicazione TLS rispondere e ripristinare correttamente da errori TLS non gestiti nell'implementazione TLS.</span><span class="sxs-lookup"><span data-stu-id="73769-162">Generally, the most serious potential problems will be handled within the TLS stack itself, but it is important for the TLS application to properly respond to and recover from TLS errors that are not handled within the TLS implementation.</span></span>

<span data-ttu-id="73769-163">Per illustrare la logica necessaria per la corretta gestione degli errori, la funzione seguente illustra una raccolta tipica di servizi API che può essere usata per gestire correttamente gli errori TLS e per reimpostare correttamente lo stato di TLS dopo che è stata rilevata una condizione di errore.</span><span class="sxs-lookup"><span data-stu-id="73769-163">In order to illustrate the necessary logic for proper error handling, the following function demonstrates a typical collection of API services that can be used to properly handle TLS errors and cleanly reset the TLS state after an error condition is encountered.</span></span> <span data-ttu-id="73769-164">A parte la sezione, se nota, la logica si applica alle istanze del server TLS e del client TLS.</span><span class="sxs-lookup"><span data-stu-id="73769-164">Other than the section where noted, the logic applies to both TLS Client and TLS Server instances.</span></span>

<span data-ttu-id="73769-165">Si noti che le chiamate API più importanti nella funzione sono per i servizi *nx_secure_tls_session_end*, che chiude la sessione TLS o l'handshake e *nx_secure_tls_session_reset*, che cancella lo stato della sessione TLS, in modo che l'istanza della struttura del controllo tls_session possa essere riutilizzata per una nuova sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="73769-165">Note that the most important API calls in the function are to the services *nx_secure_tls_session_end*, which cleanly closes the TLS session or handshake, and *nx_secure_tls_session_reset*, which clears the TLS session state so the tls_session control structure instance can be reused for a new TLS session.</span></span> <span data-ttu-id="73769-166">Si noti inoltre che *nx_secure_tls_session_reset* non cancella lo stato configurato dall'utente, ad esempio i certificati o i buffer assegnati, consentendo il riutilizzo della sessione senza chiamare di nuovo *nx_secure_tls_session_create* .</span><span class="sxs-lookup"><span data-stu-id="73769-166">Also note that *nx_secure_tls_session_reset* does not clear the user-configured state such as certificates or assigned buffers, allowing the session to be reused without calling *nx_secure_tls_session_create* again.</span></span> <span data-ttu-id="73769-167">Per cancellare completamente tutti gli Stati della sessione TLS, è possibile utilizzare il *nx_secure_tls_session_delete* del servizio.</span><span class="sxs-lookup"><span data-stu-id="73769-167">To completely clear all TLS session state, the service *nx_secure_tls_session_delete* may be used instead.</span></span>

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

## <a name="configuration-options"></a><span data-ttu-id="73769-168">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="73769-168">Configuration Options</span></span>

<span data-ttu-id="73769-169">Sono disponibili diverse opzioni di configurazione per la creazione di NetX Secure.</span><span class="sxs-lookup"><span data-stu-id="73769-169">There are several configuration options for building NetX Secure.</span></span> <span data-ttu-id="73769-170">Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio:</span><span class="sxs-lookup"><span data-stu-id="73769-170">Following is a list of all options, where each is described in detail:</span></span>

| <span data-ttu-id="73769-171">Definire</span><span class="sxs-lookup"><span data-stu-id="73769-171">Define</span></span> | <span data-ttu-id="73769-172">Significato</span><span class="sxs-lookup"><span data-stu-id="73769-172">Meaning</span></span> |
|----------------------|------------------------------------------------|
| <span data-ttu-id="73769-173">**NX_SECURE_DISABLE_ERROR_CHECKING**</span><span class="sxs-lookup"><span data-stu-id="73769-173">**NX_SECURE_DISABLE_ERROR_CHECKING**</span></span>                | <span data-ttu-id="73769-174">Definita, questa opzione rimuove il controllo degli errori di base di NetX Secure.</span><span class="sxs-lookup"><span data-stu-id="73769-174">Defined, this option removes the basic NetX Secure error checking.</span></span> <span data-ttu-id="73769-175">Viene in genere usato dopo il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="73769-175">It is typically used after the application has been debugged.</span></span> |
| <span data-ttu-id="73769-176">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**</span><span class="sxs-lookup"><span data-stu-id="73769-176">**NX_CRYPTO_MAX_RSA_MODULUS_SIZE**</span></span>                  | <span data-ttu-id="73769-177">Definita, questa opzione fornisce il modulo RSA massimo previsto in bit.</span><span class="sxs-lookup"><span data-stu-id="73769-177">Defined, this option gives the maximum RSA modulus expected, in bits.</span></span> <span data-ttu-id="73769-178">Il valore predefinito è 4096 per un modulo a 4096 bit.</span><span class="sxs-lookup"><span data-stu-id="73769-178">The default value is 4096 for a 4096-bit modulus.</span></span> <span data-ttu-id="73769-179">Gli altri valori possono essere 3072, 2048 o 1024 (scelta non consigliata).</span><span class="sxs-lookup"><span data-stu-id="73769-179">Other values can be 3072, 2048, or 1024 (not recommended).</span></span> |
| <span data-ttu-id="73769-180">**NX_SECURE_ALLOW_SELF_SIGNED_CERTIFICATES**</span><span class="sxs-lookup"><span data-stu-id="73769-180">**NX_SECURE_ALLOW_SELF_SIGNED_CERTIFICATES**</span></span>        | <span data-ttu-id="73769-181">Definita, questa opzione consente a TLS di accettare certificati autofirmati da un host remoto.</span><span class="sxs-lookup"><span data-stu-id="73769-181">Defined, this option allows TLS to accept self-signed certificates from a remote host.</span></span> <span data-ttu-id="73769-182">Per impostazione predefinita, i certificati del server autofirmato vengono rifiutati da TLS come misura di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="73769-182">By default, TLS will reject self-signed server certificates as a security precaution.</span></span> <span data-ttu-id="73769-183">Se questa macro è definita, i certificati autofirmati devono comunque essere aggiunti all'archivio attendibile per essere accettati.</span><span class="sxs-lookup"><span data-stu-id="73769-183">If this macro is defined, self-signed certificates must still be added to the trusted store to be accepted.</span></span> |
| <span data-ttu-id="73769-184">**NX_SECURE_ENABLE_CLIENT_CERTIFICATE_VERIFY**</span><span class="sxs-lookup"><span data-stu-id="73769-184">**NX_SECURE_ENABLE_CLIENT_CERTIFICATE_VERIFY**</span></span>      | <span data-ttu-id="73769-185">Definita, questa opzione Abilita la verifica facoltativa del certificato client X. 509 per i server TLS<sup>4</sup>.</span><span class="sxs-lookup"><span data-stu-id="73769-185">Defined, this option enables the optional X.509 Client Certificate Verification for TLS Servers<sup>4</sup>.</span></span>  |
| <span data-ttu-id="73769-186">**NX_SECURE_ENABLE_PSK_CIPHERSUITES**</span><span class="sxs-lookup"><span data-stu-id="73769-186">**NX_SECURE_ENABLE_PSK_CIPHERSUITES**</span></span>               | <span data-ttu-id="73769-187">Definita, questa opzione Abilita la funzionalità di chiave precondivisa (PSK).</span><span class="sxs-lookup"><span data-stu-id="73769-187">Defined, this option enables Pre-Shared Key (PSK) functionality.</span></span> <span data-ttu-id="73769-188">Non Disabilita i certificati digitali.</span><span class="sxs-lookup"><span data-stu-id="73769-188">It does not disable digital certificates.</span></span> |
| <span data-ttu-id="73769-189">**NX_SECURE_TLS_CLIENT_DISABLED**</span><span class="sxs-lookup"><span data-stu-id="73769-189">**NX_SECURE_TLS_CLIENT_DISABLED**</span></span>                   | <span data-ttu-id="73769-190">Definita, questa opzione rimuove tutti i codici dello stack TLS correlati alla modalità client TLS, riducendo il codice e l'utilizzo dei dati.</span><span class="sxs-lookup"><span data-stu-id="73769-190">Defined, this option removes all TLS stack code related to TLS Client mode, reducing code and data usage.</span></span> |
| <span data-ttu-id="73769-191">**NX_SECURE_TLS_SERVER_DISABLED**</span><span class="sxs-lookup"><span data-stu-id="73769-191">**NX_SECURE_TLS_SERVER_DISABLED**</span></span>                   | <span data-ttu-id="73769-192">Definita, questa opzione rimuove tutti i codici dello stack TLS correlati alla modalità server TLS, riducendo il codice e l'utilizzo dei dati.</span><span class="sxs-lookup"><span data-stu-id="73769-192">Defined, this option removes all TLS stack code related to TLS Server mode, reducing code and data usage.</span></span>  |
| <span data-ttu-id="73769-193">**NX_SECURE_DISABLE_ECC_CIPHERSUITE**</span><span class="sxs-lookup"><span data-stu-id="73769-193">**NX_SECURE_DISABLE_ECC_CIPHERSUITE**</span></span>               | <span data-ttu-id="73769-194">Definita, questa opzione rimuove tutta la logica TLS per la crittografia a curva ellittica (ECC) ciphersuites.</span><span class="sxs-lookup"><span data-stu-id="73769-194">Defined, this option removes all TLS logic for Elliptic Curve Cryptography (ECC) ciphersuites.</span></span> <span data-ttu-id="73769-195">Questi ciphersuites sono facoltativi in TLS 1,2 e versioni precedenti e la loro disabilitazione può comportare una riduzione significativa del codice e della dimensione dei dati.</span><span class="sxs-lookup"><span data-stu-id="73769-195">These ciphersuites are optional in TLS 1.2 and earlier and disabling them can result in significant code and data size reduction.</span></span>|
| <span data-ttu-id="73769-196">**NX_SECURE_TLS_ENABLE_TLS_1_3**</span><span class="sxs-lookup"><span data-stu-id="73769-196">**NX_SECURE_TLS_ENABLE_TLS_1_3**</span></span>                    | <span data-ttu-id="73769-197">Definita, questa opzione Abilita la modalità TLSv 1.3.</span><span class="sxs-lookup"><span data-stu-id="73769-197">Defined, this option enables TLSv1.3 mode.</span></span> <span data-ttu-id="73769-198">TLS 1,3 è la versione più recente di TLS ed è disabilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="73769-198">TLS 1.3 is the newest version of TLS and is disabled by default.</span></span> |
| <span data-ttu-id="73769-199">**NX_SECURE_TLS_ENABLE_TLS_1_0**</span><span class="sxs-lookup"><span data-stu-id="73769-199">**NX_SECURE_TLS_ENABLE_TLS_1_0**</span></span>                    | <span data-ttu-id="73769-200">Definita, questa opzione Abilita la modalità legacy TLSv 1.0.</span><span class="sxs-lookup"><span data-stu-id="73769-200">Defined, this option enables the legacy TLSv1.0 mode.</span></span> <span data-ttu-id="73769-201">TLSv 1.0 è considerato obsoleto, quindi deve essere abilitato solo per la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="73769-201">TLSv1.0 is considered obsolete so it should only be enabled for backward-compatibility with older applications.</span></span> |
| <span data-ttu-id="73769-202">**NX_SECURE_TLS_ENABLE_TLS_1_1**</span><span class="sxs-lookup"><span data-stu-id="73769-202">**NX_SECURE_TLS_ENABLE_TLS_1_1**</span></span>                    | <span data-ttu-id="73769-203">Definita, questa opzione Abilita la modalità legacy TLSv 1.1.</span><span class="sxs-lookup"><span data-stu-id="73769-203">Defined, this option enables the legacy TLSv1.1 mode.</span></span> <span data-ttu-id="73769-204">TLSv 1.1 è considerato obsoleto, quindi deve essere abilitato solo per la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="73769-204">TLSv1.1 is considered obsolete so it should only be enabled for backward-compatibility with older applications.</span></span> |
| <span data-ttu-id="73769-205">**NX_SECURE_TLS_DISABLE_TLS_1_1**</span><span class="sxs-lookup"><span data-stu-id="73769-205">**NX_SECURE_TLS_DISABLE_TLS_1_1**</span></span>                   | <span data-ttu-id="73769-206">Definita, questa opzione Disabilita la modalità TLSv 1.1.</span><span class="sxs-lookup"><span data-stu-id="73769-206">Defined, this option disables TLSv1.1 mode.</span></span> <span data-ttu-id="73769-207">Viene definito per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="73769-207">It is defined by default.</span></span> <span data-ttu-id="73769-208">TLSv 1.1 è disabilitato a favore dell'uso di TLSv 1.2<sup>5</sup>più protetti.</span><span class="sxs-lookup"><span data-stu-id="73769-208">TLSv1.1 is disabled in favor of using only the more-secure TLSv1.2<sup>5</sup>.</span></span>  |
| <span data-ttu-id="73769-209">**NX_SECURE_X509_STRICT_NAME_COMPARE**</span><span class="sxs-lookup"><span data-stu-id="73769-209">**NX_SECURE_X509_STRICT_NAME_COMPARE**</span></span>              | <span data-ttu-id="73769-210">Definita, questa opzione Abilita il confronto dei nomi distinti per i certificati X. 509 per la ricerca e la verifica dei certificati.</span><span class="sxs-lookup"><span data-stu-id="73769-210">Defined, this option enables strict distinguished name comparison for X.509 certificates for certificate searching and verification.</span></span> <span data-ttu-id="73769-211">Il valore predefinito è confrontare solo i campi del nome comune dei nomi distinti.</span><span class="sxs-lookup"><span data-stu-id="73769-211">The default is to only compare the Common Name fields of the Distinguished Names.</span></span>|
| <span data-ttu-id="73769-212">**NX_SECURE_X509_USE_EXTENDED_DISTINGUISHED_NAMES**</span><span class="sxs-lookup"><span data-stu-id="73769-212">**NX_SECURE_X509_USE_EXTENDED_DISTINGUISHED_NAMES**</span></span> | <span data-ttu-id="73769-213">Definita, questa opzione Abilita i campi del nome distinto X. 509 facoltativi, a scapito dell'utilizzo di memoria aggiuntivo per i certificati X. 509.</span><span class="sxs-lookup"><span data-stu-id="73769-213">Defined, this option enables the optional X.509 Distinguished Name fields, at the expense of extra memory use for X.509 certificates.</span></span> |

4. <span data-ttu-id="73769-214">Si noti che questa opzione consente solo di collegare il codice nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="73769-214">Note that this option only enables the code to be linked into the application.</span></span> <span data-ttu-id="73769-215">La funzionalità deve essere abilitata con il servizio API nx_secure_tls_session_client_verify_enable o configurata usando nx_secure_tls_session_x509_client_verify_configure per usare la verifica del certificato client.</span><span class="sxs-lookup"><span data-stu-id="73769-215">The feature will need to be enabled with the API service nx_secure_tls_session_client_verify_enable or configured using nx_secure_tls_session_x509_client_verify_configure in order to use Client Certificate Verification.</span></span>

5. <span data-ttu-id="73769-216">Si noti che è anche possibile disabilitare TLSv 1.2 Se si usa solo TLS 1,0 o TLS 1,1.</span><span class="sxs-lookup"><span data-stu-id="73769-216">Note that it is also possible to disable TLSv1.2 if using TLS 1.0 or TLS 1.1 only.</span></span> <span data-ttu-id="73769-217">Questa operazione non è tuttavia consigliata e non è supportata direttamente.</span><span class="sxs-lookup"><span data-stu-id="73769-217">However, this is not recommended and not directly supported.</span></span>
