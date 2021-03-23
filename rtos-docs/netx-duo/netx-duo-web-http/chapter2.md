---
title: Capitolo 2-installazione e uso di HTTP e HTTPS
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente HTTP Web NetX.
author: philmea
ms.author: philmea
ms.date: 07/24/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 99e649781588b56e72b509c2aa077c38423379d1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821608"
---
# <a name="chapter-2---installation-and-use-of-http-and-https"></a><span data-ttu-id="df9a0-103">Capitolo 2-installazione e uso di HTTP e HTTPS</span><span class="sxs-lookup"><span data-stu-id="df9a0-103">Chapter 2 - Installation and use of HTTP and HTTPS</span></span>

<span data-ttu-id="df9a0-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente HTTP Web NetX.</span><span class="sxs-lookup"><span data-stu-id="df9a0-104">This chapter contains a description of various issues related to installation, setup, and usage of the NetX Web HTTP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="df9a0-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="df9a0-105">Product Distribution</span></span>

<span data-ttu-id="df9a0-106">HTTP per NetX è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="df9a0-106">HTTP for NetX is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="df9a0-107">Il pacchetto include tre file di origine, due file di inclusione e un file che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="df9a0-107">The package includes three source files, two include files, and a file that contains this document, as follows:</span></span>

- <span data-ttu-id="df9a0-108">**nx_web_http_common. h** File di intestazione comune per HTTP Web NetX</span><span class="sxs-lookup"><span data-stu-id="df9a0-108">**nx_web_http_common.h** Common header file for NetX Web HTTP</span></span>
- <span data-ttu-id="df9a0-109">**nx_web_http_client. h** File di intestazione per il client HTTP per NetX Web</span><span class="sxs-lookup"><span data-stu-id="df9a0-109">**nx_web_http_client.h** Header file for HTTP Client for NetX Web</span></span>
- <span data-ttu-id="df9a0-110">**nx_web_http_server. h** File di intestazione per il server HTTP per NetX Web</span><span class="sxs-lookup"><span data-stu-id="df9a0-110">**nx_web_http_server.h** Header file for HTTP Server for NetX Web</span></span>
- <span data-ttu-id="df9a0-111">**nx_web_http_client. c** File di origine C per il client HTTP per NetX Web</span><span class="sxs-lookup"><span data-stu-id="df9a0-111">**nx_web_http_client.c** C Source file for HTTP Client for NetX Web</span></span>
- <span data-ttu-id="df9a0-112">**nx_web_http_server. c** File di origine C per il server HTTP per NetX Web</span><span class="sxs-lookup"><span data-stu-id="df9a0-112">**nx_web_http_server.c** C Source file for HTTP Server for NetX Web</span></span>
- <span data-ttu-id="df9a0-113">**nx_tcpserver. c** File di origine C per più socket TCP</span><span class="sxs-lookup"><span data-stu-id="df9a0-113">**nx_tcpserver.c** C Source file for multiple TCP sockets</span></span>
- <span data-ttu-id="df9a0-114">**nx_tcpserver. h** File di intestazione per la definizione dei simboli del server HTTPS</span><span class="sxs-lookup"><span data-stu-id="df9a0-114">**nx_tcpserver.h** Header file for defining HTTPS Server symbols</span></span>
- <span data-ttu-id="df9a0-115">**nx_md5. c** Algoritmi digest MD5</span><span class="sxs-lookup"><span data-stu-id="df9a0-115">**nx_md5.c** MD5 digest algorithms</span></span>
- <span data-ttu-id="df9a0-116">**filex_stub. h** File stub se FileX non è presente</span><span class="sxs-lookup"><span data-stu-id="df9a0-116">**filex_stub.h** Stub file if FileX is not present</span></span>
- <span data-ttu-id="df9a0-117">**nx_web_http.pdf** Descrizione di HTTP per NetX Web</span><span class="sxs-lookup"><span data-stu-id="df9a0-117">**nx_web_http.pdf** Description of HTTP for NetX Web</span></span>
- <span data-ttu-id="df9a0-118">**demo_netx_web_http. c** Dimostrazione HTTP Web NetX</span><span class="sxs-lookup"><span data-stu-id="df9a0-118">**demo_netx_web_http.c** NetX Web HTTP demonstration</span></span>

## <a name="http-installation"></a><span data-ttu-id="df9a0-119">Installazione HTTP</span><span class="sxs-lookup"><span data-stu-id="df9a0-119">HTTP Installation</span></span>

<span data-ttu-id="df9a0-120">Per usare HTTP Web NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="df9a0-120">In order to use NetX Web HTTP, the entire distribution mentioned previously should be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="df9a0-121">Se, ad esempio, NetX Duo è installato nella directory "*\threadx\arm7\green*", il *nx_web_http_client. h* e *nx_web_http_client. c per le applicazioni client HTTP Web NETX e nx_web_http_server. h*, *nx_web_http_server. c, nx_tcpserver. c e NX_TCPSERVER. h per le applicazioni server HTTP Web NETX. Per le applicazioni client e server, anche nx_web_http_common. h deve trovarsi in questa directory.* se viene utilizzata l'autenticazione del digest, è necessario copiare anche nx_md5. c in questa directory.</span><span class="sxs-lookup"><span data-stu-id="df9a0-121">For example, if NetX Duo is installed in the directory “*\threadx\arm7\green*” then the *nx_web_http_client.h* and *nx_web_http_client.c for NetX Web HTTP Client applications, and nx_web_http_server.h*, *nx_web_http_server.c, nx_tcpserver.c and nx_tcpserver.h for NetX Web HTTP Server applications. For both client and server applications, nx_web_http_common.h must be in this directory as well. nx_md5.c* should also be copied into this directory if digest authentication is being used.</span></span> <span data-ttu-id="df9a0-122">Per il client HTTP dell'applicazione demo ' RAM driver ' e i file server devono essere copiati nella stessa directory.</span><span class="sxs-lookup"><span data-stu-id="df9a0-122">For the demo ‘ram driver’ application HTTP Client and Server files should be copied into the same directory.</span></span>

<span data-ttu-id="df9a0-123">Se si usa TLS, è necessario disporre di una directory protetta NetX distinta contenente i file di origine TLS.</span><span class="sxs-lookup"><span data-stu-id="df9a0-123">If using TLS, you should have a separate NetX Secure directory containing the TLS source files.</span></span>

## <a name="using-http"></a><span data-ttu-id="df9a0-124">Uso di HTTP</span><span class="sxs-lookup"><span data-stu-id="df9a0-124">Using HTTP</span></span>

<span data-ttu-id="df9a0-125">L'uso di HTTP Web NetX è facile.</span><span class="sxs-lookup"><span data-stu-id="df9a0-125">Using NetX Web HTTP is easy.</span></span> <span data-ttu-id="df9a0-126">In pratica, il codice dell'applicazione deve includere *nx_web_http_client. h* e/o *nx_web_http_server. h* dopo aver compreso *tx_api. h, fx_api. h* e *nx_api. h* (*nx_web_http_common. h* viene incluso automaticamente).</span><span class="sxs-lookup"><span data-stu-id="df9a0-126">Basically, the application code must include *nx_web_http_client.h* and/or *nx_web_http_server.h* after it includes *tx_api.h, fx_api.h,* and *nx_api.h* (*nx_web_http_common.h* is automatically included).</span></span> <span data-ttu-id="df9a0-127">Tali intestazioni consentono all'applicazione di utilizzare rispettivamente ThreadX, FileX e NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="df9a0-127">Those headers enable the application to use ThreadX, FileX, and NetX Duo, respectively.</span></span> <span data-ttu-id="df9a0-128">Per il supporto HTTPS, le intestazioni devono essere incluse dopo che il file *nx_secure_tls. h* è incluso per il supporto TLS.</span><span class="sxs-lookup"><span data-stu-id="df9a0-128">For HTTPS support, the headers must be included after the *nx_secure_tls.h* file is included to bring in TLS support.</span></span>

<span data-ttu-id="df9a0-129">Una volta inclusi i file di intestazione HTTP, il codice dell'applicazione è in grado di eseguire le chiamate di funzione HTTP specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="df9a0-129">Once the HTTP header files are included, the application code is then able to make the HTTP function calls specified later in this guide.</span></span> <span data-ttu-id="df9a0-130">L'applicazione deve inoltre collegarsi a *nx_web_http_client. c per i client HTTP (s)*, *nx_web_http_server. c e nx_tcpserver. c per i server http (s)* e *nx_md5. c (per l'autenticazione del digest)* nel processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="df9a0-130">The application must also link with *nx_web_http_client.c for HTTP(S) clients*, *nx_web_http_server.c and nx_tcpserver.c for HTTP(S) servers*, and *nx_md5.c (for digest authentication)* in the build process.</span></span> <span data-ttu-id="df9a0-131">Questi file devono essere compilati allo stesso modo degli altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="df9a0-131">These files must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="df9a0-132">Questo è tutto ciò che è necessario per usare HTTP Web NetX.</span><span class="sxs-lookup"><span data-stu-id="df9a0-132">This is all that is required to use NetX Web HTTP.</span></span>

> [!NOTE]
> <span data-ttu-id="df9a0-133">Se NX_WEB_HTTP_DIGEST_ENABLE non viene specificato nel processo di compilazione, non è necessario aggiungere il file *MD5. c* all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="df9a0-133">If NX_WEB_HTTP_DIGEST_ENABLE is not specified in the build process, the *md5.c* file does not need to be added to the application.</span></span> <span data-ttu-id="df9a0-134">Analogamente, se non sono richieste funzionalità client HTTP, il file *nx_web_http_client. c* può essere omesso e, se non sono necessarie funzionalità server http, è possibile che *nx_web_http_server. c* venga omesso.</span><span class="sxs-lookup"><span data-stu-id="df9a0-134">Similarly, if no HTTP Client capabilities are required, the *nx_web_http_client.c* file may be omitted and if no HTTP Server capabilities are required, *nx_web_http_server.c* may be omitted.</span></span>
>
> <span data-ttu-id="df9a0-135">A meno che non sia stato definito NX_WEB_HTTPS_ENABLE per abilitare HTTPS, anziché usare solo HTTP non crittografato, non è necessario che NetX Secure TLS sia nella compilazione.</span><span class="sxs-lookup"><span data-stu-id="df9a0-135">Unless NX_WEB_HTTPS_ENABLE is defined in order to enable HTTPS (instead of using only plaintext HTTP) then NetX Secure TLS does not need to be in the build.</span></span>
>
> <span data-ttu-id="df9a0-136">Poiché HTTP usa i servizi TCP NetX, è necessario abilitare TCP con la chiamata *nx_tcp_enable ()* prima di usare http.</span><span class="sxs-lookup"><span data-stu-id="df9a0-136">Since HTTP utilizes NetX TCP services, TCP must be enabled with the *nx_tcp_enable()* call prior to using HTTP.</span></span>
>
> <span data-ttu-id="df9a0-137">Quando si usa HTTPS con NetX Secure TLS, è necessario inizializzare TLS con *nx_secure_tls_initialize ()* prima di chiamare le routine HTTPS.</span><span class="sxs-lookup"><span data-stu-id="df9a0-137">When using HTTPS with NetX Secure TLS, TLS must be initialized with *nx_secure_tls_initialize()* prior to calling HTTPS routines.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="df9a0-138">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="df9a0-138">Small Example System</span></span>

<span data-ttu-id="df9a0-139">Un esempio di come usare HTTP Web NetX è descritto nella figura 1,1 riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="df9a0-139">An example of how to use NetX Web HTTP is described in Figure 1.1 below.</span></span>

> [!CAUTION]
> <span data-ttu-id="df9a0-140">Questa operazione viene fornita solo a scopo dimostrativo e non è garantita la compilazione e l'esecuzione così come sono.</span><span class="sxs-lookup"><span data-stu-id="df9a0-140">This is provided for demonstration purposes only and is not guaranteed to compile and run as is.</span></span>
>
> <span data-ttu-id="df9a0-141">Vedere la distribuzione del codice di rilascio HTTPS di NetX Duo per i file di codice sorgente demo che compileranno correttamente nell'ambiente di logica Express nativo.</span><span class="sxs-lookup"><span data-stu-id="df9a0-141">Please refer to the NetX Duo HTTPS release code distribution for  demo source code file(s) that will properly build in the native Express Logic environment.</span></span>  <span data-ttu-id="df9a0-142">Tenere inoltre presente che queste demo sono intenzionalmente mantenute molto semplici, in quanto hanno lo scopo di introdurre l'applicazione HTTPS e/o NetX Duo HTTPS ai nuovi utenti.</span><span class="sxs-lookup"><span data-stu-id="df9a0-142">Also be aware that these demos are intentionally kept very simple as they are intended to introduce HTTPS and/or NetX Duo HTTPS application to new users.</span></span>

<span data-ttu-id="df9a0-143">In questo esempio, il file di inclusione HTTP *nx_web_http_client. h e nx_web_http_server. h vengono* introdotti (*netx_web_http_common. h* viene incluso automaticamente).</span><span class="sxs-lookup"><span data-stu-id="df9a0-143">In this example, the HTTP include file *nx_web_http_client.h and nx_web_http_server.h are* brought in (*netx_web_http_common.h* is included automatically).</span></span> <span data-ttu-id="df9a0-144">Il server HTTP viene quindi creato in "*tx_application_define*".</span><span class="sxs-lookup"><span data-stu-id="df9a0-144">Next, the HTTP Server is created in “*tx_application_define*”.</span></span> <span data-ttu-id="df9a0-145">Si noti che il blocco di controllo server HTTP "*Server*" è stato definito in precedenza come variabile globale.</span><span class="sxs-lookup"><span data-stu-id="df9a0-145">Note that the HTTP Server control block “*Server*” was defined as a global variable previously.</span></span> <span data-ttu-id="df9a0-146">Al termine della creazione, il server HTTPS viene avviato.</span><span class="sxs-lookup"><span data-stu-id="df9a0-146">After successful creation, the HTTPS Server is started.</span></span> <span data-ttu-id="df9a0-147">Viene quindi creato il client HTTPS.</span><span class="sxs-lookup"><span data-stu-id="df9a0-147">The HTTPS Client is then created.</span></span> <span data-ttu-id="df9a0-148">Il file viene scritto e letto nuovamente.</span><span class="sxs-lookup"><span data-stu-id="df9a0-148">It writes the file and reads the file back.</span></span>

> [!NOTE]
> <span data-ttu-id="df9a0-149">NX_WEB_HTTPS_ENABLE è definito nel sistema.</span><span class="sxs-lookup"><span data-stu-id="df9a0-149">NX_WEB_HTTPS_ENABLE is defined on this system.</span></span>

```c
/* This is a small demo of HTTPS on the high-performance NetX Duo TCP/IP stack.
   This demo relies on ThreadX, NetX Duo, and FileX to show an HTML
   transfer from the client and then back from the server.  */

#include  "tx_api.h"
#include  "fx_api.h"
#include  "nx_api.h"
#include  “nx_crypto.h”
#include  “nx_secure_tls_api.h”
#include  “nx_secure_x509.h”
#include  "nx_web_http_client.h"
#include  "nx_web_http_server.h"
#define    DEMO_STACK_SIZE         4096


/* Define the ThreadX and NetX object control blocks...  */

TX_THREAD               thread_0;
TX_THREAD               thread_1;
NX_PACKET_POOL          pool_0;
NX_PACKET_POOL          pool_1;
NX_IP                   ip_0;
NX_IP                   ip_1;
FX_MEDIA                ram_disk;

/* Define HTTP objects.  */

NX_WEB_HTTP_SERVER      my_server;
NX_WEB_HTTP_CLIENT      my_client;

/* Define the counters used in the demo application...  */

ULONG                   error_counter;


/* Define the RAM disk memory.  */

UCHAR                   ram_disk_memory[32000];

/* Include cryptographic routines for TLS. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Define TLS data for HTTPS. */
CHAR crypto_metadata[8928 * NX_WEB_HTTP_SESSION_MAX];
UCHAR tls_packet_buffer[16500];

/* NX_WEB_HTTP_SERVER_SESSION_MAX defaults to 2 in nx_web_http_server.h */
UCHAR server_tls_packet_buffer[16500 * NX_WEB_HTTP_SERVER_SESSION_MAX];

/* Define certificate containers. The server certificate is used to identify the NetX
   Web HTTPS server and the trusted certificate is used by the client to verify the
   server’s identity certificate.  */
NX_SECURE_X509_CERT server_certificate;
NX_SECURE_X509_CERT trusted_certificate;

/* Remote certificates need both an NX_SECURE_X509_CERT container and an associated
   buffer. The number of certificates depends on the remote host, but usually at least
   two certificates will be sent – the identity certificate for the host and the
   certificate that issued the identity certificate. */
NX_SECURE_X509_CERT remote_certificate, remote_issuer;

UCHAR remote_cert_buffer[2000];
UCHAR remote_issuer_buffer[2000];

/* Certificate information for server and client (see NetX Secure TLS reference on X.509
    certificates for more information). Arrays are populated with binary versions Of
    certificates and keys and the corresponding “len” variables are assigned the lengths
    of that data. Trusted certificates do not need a private key. */
const UCHAR server_cert_der[] = { … };
const UINT  server_cert_derlen = … ;
const UCHAR server_cert_key_der[] = { … };
const UINT  server_cert_key_derlen = … ;

const UCHAR trusted_cert_der[] = { … };
const UINT  trusted_cert_derlen = … ;


/* Define function prototypes.  */

void    thread_0_entry(ULONG thread_input);
VOID    _fx_ram_driver(FX_MEDIA *media_ptr) ;
void    _nx_ram_network_driver(struct NX_IP_DRIVER_STRUCT *driver_req);
UINT    authentication_check(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
             CHAR *resource, CHAR **name, CHAR **password, CHAR **realm);
UINT tls_setup_callback(NX_WEB_HTTP_CLIENT *client_ptr,
   NX_SECURE_TLS_SESSION *tls_session);

/* Define the application's authentication check.  This is called by
   the HTTP server whenever a new request is received.  */
UINT  authentication_check(NX_WEB_HTTP_SERVER *server_ptr, UINT request_type,
            CHAR *resource, CHAR **name, CHAR **password, CHAR **realm)
{
    /* Just use a simple name, password, and realm for all
       requests and resources.  */
    *name =     "name";
    *password = "password";
    *realm =    "NetX Web HTTP demo";

    /* Request basic authentication.  */
    return(NX_WEB_HTTP_BASIC_AUTHENTICATE);
}

/* Define the TLS setup callback for HTTPS Client. This function is invoked when the
   HTTPS client is started – all TLS per-session initialization should go in here. */
UINT tls_setup_callback(NX_WEB_HTTP_CLIENT *client_ptr,
  NX_SECURE_TLS_SESSION *tls_session)
{
    UINT status;

    /* Initialize and create TLS session. */
    nx_secure_tls_session_create(tls_session, &nx_crypto_tls_ciphers,
        crypto_metadata, sizeof(crypto_metadata));

    /* Allocate space for packet reassembly. */
    nx_secure_tls_session_packet_buffer_set(tls_session, tls_packet_buffer,
        sizeof(tls_packet_buffer));


    /* Add a CA Certificate to our trusted store for verifying incoming server
        certificates. */
    nx_secure_x509_certificate_initialize(&trusted_certificate, trusted_cert_der,
        trusted_cert_der_len, NX_NULL, 0, NULL, 0,
        NX_SECURE_X509_KEY_TYPE_NONE);
    nx_secure_tls_trusted_certificate_add(tls_session, &trusted_certificate);

    /* Need to allocate space for the certificate coming in from the remote host. */
    nx_secure_tls_remote_certificate_allocate(tls_session, &remote_certificate,
        remote_cert_buffer, sizeof(remote_cert_buffer));
    nx_secure_tls_remote_certificate_allocate(tls_session,
        &remote_issuer, remote_issuer_buffer,
        sizeof(remote_issuer_buffer));

    return(NX_SUCCESS);
 }

/* Define main entry point.  */

 int main()
 {
     /* Enter the ThreadX kernel.  */
     tx_kernel_enter();
 }

/* Define what the initial system looks like.  */
void    tx_application_define(void *first_unused_memory)
{

    CHAR    *pointer;

    /* Setup the working pointer.  */
    pointer =  (CHAR *) first_unused_memory;

    /* Create the main thread.  */
    tx_thread_create(&thread_0, "thread 0", thread_0_entry, 0,
        pointer, DEMO_STACK_SIZE,
        2, 2, TX_NO_TIME_SLICE, TX_AUTO_START);
    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system.  */
    nx_system_initialize();

    /* Create packet pool.  */
    nx_packet_pool_create(&pool_0, "NetX Packet Pool 0",
        600, pointer, 8192);
    pointer = pointer + 8192;

    /* Create an IP instance.  */
    nx_ip_create(&ip_0, "NetX IP Instance 0", IP_ADDRESS(1, 2, 3, 4),
        0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
        pointer, 4096, 1);
    pointer =  pointer + 4096;

    /* Create another packet pool. */
    nx_packet_pool_create(&pool_1, "NetX Packet Pool 1", 600, pointer, 8192);
    pointer = pointer + 8192;

    /* Create another IP instance.  */
    nx_ip_create(&ip_1, "NetX IP Instance 1", IP_ADDRESS(1, 2, 3, 5),
        0xFFFFFF00UL, &pool_1, _nx_ram_network_driver,
        pointer, 4096, 1);
    pointer = pointer + 4096;

    /* Enable ARP and supply ARP cache memory for IP Instance 0.  */
    nx_arp_enable(&ip_0, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Enable ARP and supply ARP cache memory for IP Instance 1.  */
    nx_arp_enable(&ip_1, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Enable TCP processing for both IP instances.  */
    nx_tcp_enable(&ip_0);
    nx_tcp_enable(&ip_1);

    /* Open the RAM disk.  */
    fx_media_open(&ram_disk, "RAM DISK",
        _fx_ram_driver, ram_disk_memory, pointer, 4096);
    pointer += 4096;

    /* Create the NetX Web HTTP Server.  */
    nx_web_http_server_create(&my_server, "My HTTP Server", &ip_1,
        NX_WEB_HTTPS_SERVER_PORT, &ram_disk,
        pointer, 4096, &pool_1, authentication_check, NX_NULL);
    pointer = pointer + 4096;

    /* The TLS server needs an identity certificate which is imported as a binary DER-
        encoded X.509 certificate and its associated private key (e.g. DER-encoded PKCS#1
        RSA private key). */
    nx_secure_x509_certificate_initialize(&server_certificate, server_cert_der,
        server_cert_der_len, NX_NULL, 0,
        server_cert_key_der, server_cert_key_der_len,
        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Setup TLS session data for the TCP server.
        This enables TLS and HTTPS for the server.  */
    nx_web_http_server_secure_configure(&my_server, &nx_crypto_tls_ciphers,
        crypto_metadata, sizeof(crypto_metadata), server_tls_packet_buffer,
        sizeof(server_tls_packet_buffer), &server_certificate, NX_NULL, 0,
        NX_NULL, 0, NX_NULL, 0);

    /* Start the HTTP Server.  */
    nx_web_http_server_start(&my_server);
}

/* Define the test thread.  */
void    thread_0_entry(ULONG thread_input)
{
    NX_PACKET   *my_packet;
    UINT        status;

    /* Create an HTTP client instance.  */
    status = nx_web_http_client_create(&my_client, "My Client", &ip_0, &pool_0, 600);

    /* Check status.  */
    if (status)
        error_counter++;

    /* Prepare to send the simple 103-byte HTML file to the Server over HTTPS.  */
    status = nx_web_http_client_put_secure_start(&my_client, IP_ADDRESS(1,2,3,5),
        NX_WEB_HTTPS_SERVER_PORT, "/test.htm", "name", "password", 103, tls_setup_callback, 50);

    /* Check status.  */
    if (status)
        error_counter++;

    /* Allocate a packet.  */
     tatus = nx_web_http_client_request_packet_allocate(&pool_0, &my_packet,
        NX_TCP_PACKET, NX_WAIT_FOREVER);

    /* Check status.  */
    if (status != NX_SUCCESS)
        return;

    /* Build a simple 103-byte HTML page.  */
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

    /* Complete the PUT by writing the total length.  */
    status =  nx_web_http_client_put_packet(&my_client, my_packet, 50);

    /* Check status.  */
    if (status)
        error_counter++;

    /* Now GET the file back!  */
    status =  nx_web_http_client_get_secure_start(&my_client, IP_ADDRESS(1,2,3,5),
        NX_WEB_HTTPS_SERVER_PORT, "/test.htm",
        "name", "password", tls_setup_callback, 50);
 
    /* Check status.  */
    if (status)
        error_counter++;

    /* Get a packet.  */
    status =  nx_web_http_client_response_body_get(&my_client, &my_packet, 20);

    /* Check for an error.  */
    if ((status) || (my_packet -> nx_packet_length != 103))
        error_counter++;

    /* Check to see if we have a packet.  */
    if (status == NX_SUCCESS)
    {

        /* Yes, release it!  */
        nx_packet_release(my_packet);
    }

    /* Make sure TLS shuts down properly. */
    nx_web_http_client_delete(&my_client);

    /* Flush the media.  */
    fx_media_flush(&ram_disk);
}
```

<span data-ttu-id="df9a0-150">**Figura 1,1 esempio di uso di HTTPS con NetX e NetX Secure TLS**</span><span class="sxs-lookup"><span data-stu-id="df9a0-150">**Figure 1.1 Example of HTTPS use with NetX and NetX Secure TLS**</span></span>

## <a name="configuration-options"></a><span data-ttu-id="df9a0-151">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="df9a0-151">Configuration Options</span></span>

<span data-ttu-id="df9a0-152">Per la compilazione di HTTP per NetX sono disponibili diverse opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="df9a0-152">There are several configuration options for building HTTP for NetX.</span></span> <span data-ttu-id="df9a0-153">Di seguito è riportato un elenco di tutte le opzioni, in cui ciascuna è descritta in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="df9a0-153">Following is a list of all options, where each is described in detail.</span></span> <span data-ttu-id="df9a0-154">I valori predefiniti sono elencati ma possono essere ridefiniti prima dell'inclusione di *nx_web_http_client. h e nx_web_http_server. h*:</span><span class="sxs-lookup"><span data-stu-id="df9a0-154">The default values are listed but can be redefined prior to inclusion of *nx_web_http_client.h and nx_web_http_server.h*:</span></span>

- <span data-ttu-id="df9a0-155">**NX_DISABLE_ERROR_CHECKING** Definita, questa opzione rimuove il controllo degli errori HTTP di base.</span><span class="sxs-lookup"><span data-stu-id="df9a0-155">**NX_DISABLE_ERROR_CHECKING** Defined, this option removes the basic HTTP error checking.</span></span> <span data-ttu-id="df9a0-156">Viene in genere usato dopo il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="df9a0-156">It is typically used after the application has been debugged.</span></span>
- <span data-ttu-id="df9a0-157">**NX_WEB_HTTP_DIGEST_ENABLE** Se definito, l'autenticazione che usa il digest MD5 è abilitata nel server HTTPS.</span><span class="sxs-lookup"><span data-stu-id="df9a0-157">**NX_WEB_HTTP_DIGEST_ENABLE** If defined, authentication using the MD5 digest is enabled on the HTTPS Server.</span></span> <span data-ttu-id="df9a0-158">Per impostazione predefinita, non è definito.</span><span class="sxs-lookup"><span data-stu-id="df9a0-158">By default it is not defined.</span></span>
- <span data-ttu-id="df9a0-159">**NX_WEB_HTTP_SERVER_PRIORITY** Priorità del thread del server HTTPS.</span><span class="sxs-lookup"><span data-stu-id="df9a0-159">**NX_WEB_HTTP_SERVER_PRIORITY** The priority of the HTTPS Server thread.</span></span> <span data-ttu-id="df9a0-160">Per impostazione predefinita, questo valore è definito come 16 per specificare la priorità 16.</span><span class="sxs-lookup"><span data-stu-id="df9a0-160">By default, this value is defined as 16 to specify priority 16.</span></span>
- <span data-ttu-id="df9a0-161">**NX_WEB_HTTP_NO_FILEX** Definito, questa opzione fornisce uno stub per le dipendenze FileX.</span><span class="sxs-lookup"><span data-stu-id="df9a0-161">**NX_WEB_HTTP_NO_FILEX** Defined, this option provides a stub for FileX dependencies.</span></span> <span data-ttu-id="df9a0-162">Se questa opzione è definita, il client HTTPS funzionerà senza alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="df9a0-162">The HTTPS Client will function without any change if this option is defined.</span></span> <span data-ttu-id="df9a0-163">Il server HTTPS deve essere modificato o l'utente dovrà creare un numero limitato di servizi FileX per il corretto funzionamento.</span><span class="sxs-lookup"><span data-stu-id="df9a0-163">The HTTPS Server will need to either be modified or the user will have to create a handful of FileX services in order to function properly.</span></span>
- <span data-ttu-id="df9a0-164">**NX_WEB_HTTP_TYPE_OF_SERVICE** Tipo di servizio richiesto per le richieste TCP HTTPS.</span><span class="sxs-lookup"><span data-stu-id="df9a0-164">**NX_WEB_HTTP_TYPE_OF_SERVICE** Type of service required for the HTTPS TCP requests.</span></span> <span data-ttu-id="df9a0-165">Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.</span><span class="sxs-lookup"><span data-stu-id="df9a0-165">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span>
- <span data-ttu-id="df9a0-166">**NX_WEB_HTTP_SERVER_THREAD_TIME_SLICE** Numero di cicli del timer che il thread del server può eseguire prima di cedere ai thread con la stessa priorità.</span><span class="sxs-lookup"><span data-stu-id="df9a0-166">**NX_WEB_HTTP_SERVER_THREAD_TIME_SLICE** The number of timer ticks the Server thread is allowed to run before yielding to threads of the same priority.</span></span> <span data-ttu-id="df9a0-167">Il valore predefinito è 2.</span><span class="sxs-lookup"><span data-stu-id="df9a0-167">The default value is 2.</span></span> <span data-ttu-id="df9a0-168">Nota Questa opzione è deprecata.</span><span class="sxs-lookup"><span data-stu-id="df9a0-168">Note this option is deprecated.</span></span>
- <span data-ttu-id="df9a0-169">**NX_WEB_HTTP_FRAGMENT_OPTION** L'abilitazione del frammento per le richieste TCP HTTP.</span><span class="sxs-lookup"><span data-stu-id="df9a0-169">**NX_WEB_HTTP_FRAGMENT_OPTION** Fragment enable for HTTP TCP requests.</span></span> <span data-ttu-id="df9a0-170">Per impostazione predefinita, questo valore è NX_DONT_FRAGMENT per disabilitare la frammentazione TCP HTTP.</span><span class="sxs-lookup"><span data-stu-id="df9a0-170">By default, this value is NX_DONT_FRAGMENT to disable HTTP TCP fragmenting.</span></span>
- <span data-ttu-id="df9a0-171">**NX_WEB_HTTP_SERVER_WINDOW_SIZE** Dimensioni finestra socket server.</span><span class="sxs-lookup"><span data-stu-id="df9a0-171">**NX_WEB_HTTP_SERVER_WINDOW_SIZE** Server socket window size.</span></span> <span data-ttu-id="df9a0-172">Per impostazione predefinita, questo valore è pari a 2048 byte.</span><span class="sxs-lookup"><span data-stu-id="df9a0-172">By default, this value is 2048 bytes.</span></span>
- <span data-ttu-id="df9a0-173">**NX_WEB_HTTP_TIME_TO_LIVE** Specifica il numero di router che questo pacchetto può superare prima che venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="df9a0-173">**NX_WEB_HTTP_TIME_TO_LIVE** Specifies the number of routers this packet can pass before it is discarded.</span></span> <span data-ttu-id="df9a0-174">Il valore predefinito è impostato su 0x80.</span><span class="sxs-lookup"><span data-stu-id="df9a0-174">The default value is set to 0x80.</span></span>
- <span data-ttu-id="df9a0-175">**NX_WEB_HTTP_SERVER_TIMEOUT** Consente di specificare il numero di cicli ThreadX per i quali i servizi interni sospendono.</span><span class="sxs-lookup"><span data-stu-id="df9a0-175">**NX_WEB_HTTP_SERVER_TIMEOUT** Specifies the number of ThreadX ticks that internal services will suspend for.</span></span> <span data-ttu-id="df9a0-176">Il valore predefinito è impostato su 10 secondi (10 \* *NX_IP_PERIODIC_RATE*).</span><span class="sxs-lookup"><span data-stu-id="df9a0-176">The default value is set to 10 seconds (10 \* *NX_IP_PERIODIC_RATE*).</span></span>
- <span data-ttu-id="df9a0-177">**NX_WEB_HTTP_SERVER_TIMEOUT_ACCEPT** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_server_socket_accept ()* .</span><span class="sxs-lookup"><span data-stu-id="df9a0-177">**NX_WEB_HTTP_SERVER_TIMEOUT_ACCEPT** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_server_socket_accept()* calls.</span></span> <span data-ttu-id="df9a0-178">Il valore predefinito è impostato su (10 \* *NX_IP_PERIODIC_RATE*).</span><span class="sxs-lookup"><span data-stu-id="df9a0-178">The default value is set to (10 \* *NX_IP_PERIODIC_RATE*).</span></span>
- <span data-ttu-id="df9a0-179">**NX_WEB_HTTP_SERVER_TIMEOUT_DISCONNECT** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_disconnect ()* .</span><span class="sxs-lookup"><span data-stu-id="df9a0-179">**NX_WEB_HTTP_SERVER_TIMEOUT_DISCONNECT** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_disconnect()* calls.</span></span> <span data-ttu-id="df9a0-180">Il valore predefinito è impostato su 10 secondi (10 \* *NX_IP_PERIODIC_RATE*).</span><span class="sxs-lookup"><span data-stu-id="df9a0-180">The default value is set to 10 seconds (10 \* *NX_IP_PERIODIC_RATE*).</span></span>
- <span data-ttu-id="df9a0-181">**NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_receive ()* .</span><span class="sxs-lookup"><span data-stu-id="df9a0-181">**NX_WEB_HTTP_SERVER_TIMEOUT_RECEIVE** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_receive()* calls.</span></span> <span data-ttu-id="df9a0-182">Il valore predefinito è impostato su 10 secondi (10 \* *NX_IP_PERIODIC_RATE*).</span><span class="sxs-lookup"><span data-stu-id="df9a0-182">The default value is set to 10 seconds (10 \* *NX_IP_PERIODIC_RATE*).</span></span>
- <span data-ttu-id="df9a0-183">**NX_WEB_HTTP_SERVER_TIMEOUT_SEND** Specifica il numero di cicli ThreadX per i quali i servizi interni vengono sospesi per le chiamate interne *nx_tcp_socket_send ()* .</span><span class="sxs-lookup"><span data-stu-id="df9a0-183">**NX_WEB_HTTP_SERVER_TIMEOUT_SEND** Specifies the number of ThreadX ticks that internal services will suspend for in internal *nx_tcp_socket_send()* calls.</span></span> <span data-ttu-id="df9a0-184">Il valore predefinito è impostato su 10 secondi (10 \* *NX_IP_PERIODIC_RATE*).</span><span class="sxs-lookup"><span data-stu-id="df9a0-184">The default value is set to 10 seconds (10 \* *NX_IP_PERIODIC_RATE*).</span></span>
- <span data-ttu-id="df9a0-185">**NX_WEB_HTTP_MAX_HEADER_FIELD** **specifica la dimensione massima del campo dell'intestazione HTTP. Il valore predefinito è 256.**</span><span class="sxs-lookup"><span data-stu-id="df9a0-185">**NX_WEB_HTTP_MAX_HEADER_FIELD** **Specifies the maximum size of the HTTP header field. The default value is 256.**</span></span>
- <span data-ttu-id="df9a0-186">\* \* NX_WEB_HTTP_MULTIPART_ENABLE \* \* \* \* se definito, Abilita il server HTTPS per supportare le richieste HTTP multipart.</span><span class="sxs-lookup"><span data-stu-id="df9a0-186">\*\*NX_WEB_HTTP_MULTIPART_ENABLE \*\* \*\*If defined, enables HTTPS Server to support multipart HTTP requests.</span></span> **
- <span data-ttu-id="df9a0-187">**NX_WEB_HTTP_SERVER_MAX_PENDING** Specifica il numero di connessioni che possono essere accodate per il server HTTPS.</span><span class="sxs-lookup"><span data-stu-id="df9a0-187">**NX_WEB_HTTP_SERVER_MAX_PENDING** Specifies the number of connections that can be queued for the HTTPS Server.</span></span> <span data-ttu-id="df9a0-188">Il valore predefinito è impostato su due volte il numero massimo di sessioni del server.</span><span class="sxs-lookup"><span data-stu-id="df9a0-188">The default value is set to twice the maximum number of server sessions.</span></span>
- <span data-ttu-id="df9a0-189">**NX_WEB_HTTP_MAX_RESOURCE** Specifica il numero di byte consentiti in un *nome di risorsa* fornito dal client.</span><span class="sxs-lookup"><span data-stu-id="df9a0-189">**NX_WEB_HTTP_MAX_RESOURCE** Specifies the number of bytes allowed in a client supplied *resource name*.</span></span> <span data-ttu-id="df9a0-190">Il valore predefinito è impostato su 40.</span><span class="sxs-lookup"><span data-stu-id="df9a0-190">The default value is set to 40.</span></span>
- <span data-ttu-id="df9a0-191">**NX_WEB_HTTP_MAX_NAME** Specifica il numero di byte consentiti in un *nome utente* fornito dal client.</span><span class="sxs-lookup"><span data-stu-id="df9a0-191">**NX_WEB_HTTP_MAX_NAME** Specifies the number of bytes allowed in a client supplied *username*.</span></span> <span data-ttu-id="df9a0-192">Il valore predefinito è impostato su 20.</span><span class="sxs-lookup"><span data-stu-id="df9a0-192">The default value is set to 20.</span></span>
- <span data-ttu-id="df9a0-193">**NX_WEB_HTTP_MAX_PASSWORD** Specifica il numero di byte consentiti in una *password* fornita dal client.</span><span class="sxs-lookup"><span data-stu-id="df9a0-193">**NX_WEB_HTTP_MAX_PASSWORD** Specifies the number of bytes allowed in a client supplied *password*.</span></span> <span data-ttu-id="df9a0-194">Il valore predefinito è impostato su 20.</span><span class="sxs-lookup"><span data-stu-id="df9a0-194">The default value is set to 20.</span></span>
- <span data-ttu-id="df9a0-195">**NX_WEB_HTTP_SERVER_SESSION_MAX** Specifica il numero di sessioni simultanee per un server HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="df9a0-195">**NX_WEB_HTTP_SERVER_SESSION_MAX** Specifies the number of simultaneous sessions for an HTTP or HTTPS Server.</span></span> <span data-ttu-id="df9a0-196">Per ogni sessione vengono allocati un socket TCP e una sessione TLS (se HTTPS è abilitato).</span><span class="sxs-lookup"><span data-stu-id="df9a0-196">A TCP socket and a TLS session (if HTTPS is enabled) are allocated for each session.</span></span> <span data-ttu-id="df9a0-197">Il valore predefinito è impostato su 2.</span><span class="sxs-lookup"><span data-stu-id="df9a0-197">The default value is set to 2.</span></span>
- <span data-ttu-id="df9a0-198">**NX_WEB_HTTPS_ENABLE** Se definito, questa macro Abilita TLS e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="df9a0-198">**NX_WEB_HTTPS_ENABLE** If defined, this macro enables TLS and HTTPS.</span></span> <span data-ttu-id="df9a0-199">Lasciare undefined per liberare risorse se si desidera solo HTTP non crittografato.</span><span class="sxs-lookup"><span data-stu-id="df9a0-199">Leave undefined to free up resources if only plaintext HTTP is desired.</span></span> <span data-ttu-id="df9a0-200">Per impostazione predefinita, questa macro non è definita.</span><span class="sxs-lookup"><span data-stu-id="df9a0-200">By default, this macro is not defined.</span></span>
- <span data-ttu-id="df9a0-201">**NX_WEB_HTTPS_KEEPALIVE_DISABLE** Se definito, questa macro Disabilita la funzionalità keep-alive HTTP.</span><span class="sxs-lookup"><span data-stu-id="df9a0-201">**NX_WEB_HTTPS_KEEPALIVE_DISABLE** If defined, this macro disables HTTP keep-alive feature.</span></span> <span data-ttu-id="df9a0-202">Per impostazione predefinita, questa macro non è definita.</span><span class="sxs-lookup"><span data-stu-id="df9a0-202">By default, this macro is not defined.</span></span>
- <span data-ttu-id="df9a0-203">**NX_WEB_HTTP_SERVER_MIN_PACKET_SIZE** Specifica la dimensione minima dei pacchetti nel pool specificato al momento della creazione del server.</span><span class="sxs-lookup"><span data-stu-id="df9a0-203">**NX_WEB_HTTP_SERVER_MIN_PACKET_SIZE** Specifies the minimum size of the packets in the pool specified at server creation.</span></span> <span data-ttu-id="df9a0-204">La dimensione minima è necessaria per garantire che l'intestazione HTTP completa possa essere contenuta in un unico pacchetto.</span><span class="sxs-lookup"><span data-stu-id="df9a0-204">The minimum size is needed to ensure the complete HTTP header can be contained in one packet.</span></span> <span data-ttu-id="df9a0-205">Il valore predefinito è impostato su 600.</span><span class="sxs-lookup"><span data-stu-id="df9a0-205">The default value is set to 600.</span></span>
- <span data-ttu-id="df9a0-206">**NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE** Specifica la dimensione minima dei pacchetti nel pool specificato durante la creazione del client.</span><span class="sxs-lookup"><span data-stu-id="df9a0-206">**NX_WEB_HTTP_CLIENT_MIN_PACKET_SIZE** Specifies the minimum size of the packets in the pool specified at Client creation.</span></span> <span data-ttu-id="df9a0-207">La dimensione minima è necessaria per garantire che l'intestazione HTTP completa possa essere contenuta in un unico pacchetto.</span><span class="sxs-lookup"><span data-stu-id="df9a0-207">The minimum size is needed to ensure the complete HTTP header can be contained in one packet.</span></span> <span data-ttu-id="df9a0-208">Il valore predefinito è impostato su 600.</span><span class="sxs-lookup"><span data-stu-id="df9a0-208">The default value is set to 600.</span></span>
- <span data-ttu-id="df9a0-209">**NX_WEB_HTTP_SERVER_RETRY_SECONDS** Imposta il timeout di ritrasmissione del socket del server in secondi.</span><span class="sxs-lookup"><span data-stu-id="df9a0-209">**NX_WEB_HTTP_SERVER_RETRY_SECONDS** Set the Server socket retransmission timeout in seconds.</span></span> <span data-ttu-id="df9a0-210">Il valore predefinito è impostato su 2.</span><span class="sxs-lookup"><span data-stu-id="df9a0-210">The default value is set to 2.</span></span>
- <span data-ttu-id="df9a0-211">**NX_WEB_HTTP_ SERVER_RETRY_MAX** Questo consente di impostare il numero massimo di ritrasmissioni sul socket del server.</span><span class="sxs-lookup"><span data-stu-id="df9a0-211">**NX_WEB_HTTP_ SERVER_RETRY_MAX** This sets the maximum number of retransmissions on Server socket.</span></span> <span data-ttu-id="df9a0-212">Il valore predefinito è impostato su 10.</span><span class="sxs-lookup"><span data-stu-id="df9a0-212">The default value is set to 10.</span></span>
- <span data-ttu-id="df9a0-213">**NX_WEB_HTTP_ SERVER_RETRY_SHIFT** Questo valore viene utilizzato per impostare il timeout di ritrasmissione successivo.</span><span class="sxs-lookup"><span data-stu-id="df9a0-213">**NX_WEB_HTTP_ SERVER_RETRY_SHIFT** This value is used to set the next retransmission timeout.</span></span> <span data-ttu-id="df9a0-214">Il timeout corrente viene moltiplicato per il numero di ritrasmissioni fino a questo punto, spostate in base al valore del turno di timeout del socket.</span><span class="sxs-lookup"><span data-stu-id="df9a0-214">The current timeout is multiplied by the number of retransmissions thus far, shifted by the value of the socket timeout shift.</span></span> <span data-ttu-id="df9a0-215">Il valore predefinito è impostato su 1 per raddoppiare il timeout.</span><span class="sxs-lookup"><span data-stu-id="df9a0-215">The default value is set to 1 for doubling the timeout.</span></span>
- <span data-ttu-id="df9a0-216">**NX_WEB_HTTP_SERVER_RETRY_TRANSMIT_QUEUE_DEPTH** Specifica il numero massimo di pacchetti che possono essere accodati nella coda di ritrasmissione del socket server.</span><span class="sxs-lookup"><span data-stu-id="df9a0-216">**NX_WEB_HTTP_SERVER_RETRY_TRANSMIT_QUEUE_DEPTH** This specifies the maximum number of packets that can be enqueued on the Server socket retransmission queue.</span></span> <span data-ttu-id="df9a0-217">Se il numero di pacchetti accodati raggiunge questo numero, non sarà più possibile inviare pacchetti fino a quando non vengono rilasciati uno o più pacchetti accodati.</span><span class="sxs-lookup"><span data-stu-id="df9a0-217">If the number of packets enqueued reaches this number, no more packets can be sent until one or more enqueued packets are released.</span></span> <span data-ttu-id="df9a0-218">Il valore predefinito è impostato su 20.</span><span class="sxs-lookup"><span data-stu-id="df9a0-218">The default value is set to 20.</span></span>
