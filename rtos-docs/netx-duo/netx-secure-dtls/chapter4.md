---
title: Capitolo 4-Descrizione di Azure RTO NetX Secure DTLS Services
description: Questo capitolo contiene una descrizione di tutti i servizi DTLS di Azure RTO NetX protetti elencati in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: e795a5fa35a4590e508c7fe2eec53f5494809657
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821593"
---
# <a name="chapter-4-description-of-azure-rtos-netx-secure-dtls-services"></a><span data-ttu-id="1a36b-103">Capitolo 4: Descrizione di Azure RTO NetX Secure DTLS Services</span><span class="sxs-lookup"><span data-stu-id="1a36b-103">Chapter 4: Description of Azure RTOS NetX Secure DTLS services</span></span>

<span data-ttu-id="1a36b-104">Questo capitolo contiene una descrizione di tutti i servizi DTLS protetti di Azure RTO NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="1a36b-104">This chapter contains a description of all Azure RTOS NetX Secure DTLS services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="1a36b-105">Nella sezione "valori restituiti" nelle descrizioni API seguenti i valori in **grassetto** non sono interessati dalla macro **NX_SECURE_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="1a36b-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_SECURE_DISABLE_ERROR_CHECKING** macro that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- [<span data-ttu-id="1a36b-106">nx_secure_dtls_client_session_start</span><span class="sxs-lookup"><span data-stu-id="1a36b-106">nx_secure_dtls_client_session_start</span></span>](#nx_secure_dtls_client_session_start)
- [<span data-ttu-id="1a36b-107">nx_secure_dtls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="1a36b-107">nx_secure_dtls_packet_allocate</span></span>](#nx_secure_dtls_packet_allocate)
- [<span data-ttu-id="1a36b-108">nx_secure_dtls_psk_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-108">nx_secure_dtls_psk_add</span></span>](#nx_secure_dtls_psk_add)
- [<span data-ttu-id="1a36b-109">nx_secure_dtls_server_create</span><span class="sxs-lookup"><span data-stu-id="1a36b-109">nx_secure_dtls_server_create</span></span>](#nx_secure_dtls_server_create)
- [<span data-ttu-id="1a36b-110">nx_secure_dtls_server_delete</span><span class="sxs-lookup"><span data-stu-id="1a36b-110">nx_secure_dtls_server_delete</span></span>](#nx_secure_dtls_server_delete)
- [<span data-ttu-id="1a36b-111">nx_secure_dtls_server_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-111">nx_secure_dtls_server_local_certificate_add</span></span>](#nx_secure_dtls_server_local_certificate_add)
- [<span data-ttu-id="1a36b-112">nx_secure_dtls_server_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1a36b-112">nx_secure_dtls_server_local_certificate_remove</span></span>](#nx_secure_dtls_server_local_certificate_remove)
- [<span data-ttu-id="1a36b-113">nx_secure_dtls_server_notify_set</span><span class="sxs-lookup"><span data-stu-id="1a36b-113">nx_secure_dtls_server_notify_set</span></span>](#nx_secure_dtls_server_notify_set)
- [<span data-ttu-id="1a36b-114">nx_secure_dtls_server_psk_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-114">nx_secure_dtls_server_psk_add</span></span>](#nx_secure_dtls_server_psk_add)
- [<span data-ttu-id="1a36b-115">nx_secure_dtls_server_session_send</span><span class="sxs-lookup"><span data-stu-id="1a36b-115">nx_secure_dtls_server_session_send</span></span>](#nx_secure_dtls_server_session_send)
- [<span data-ttu-id="1a36b-116">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="1a36b-116">nx_secure_dtls_server_session_start</span></span>](#nx_secure_dtls_server_session_start)
- [<span data-ttu-id="1a36b-117">nx_secure_dtls_server_start</span><span class="sxs-lookup"><span data-stu-id="1a36b-117">nx_secure_dtls_server_start</span></span>](#nx_secure_dtls_server_start)
- [<span data-ttu-id="1a36b-118">nx_secure_dtls_server_stop</span><span class="sxs-lookup"><span data-stu-id="1a36b-118">nx_secure_dtls_server_stop</span></span>](#nx_secure_dtls_server_stop)
- [<span data-ttu-id="1a36b-119">nx_secure_dtls_server_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-119">nx_secure_dtls_server_trusted_certificate_add</span></span>](#nx_secure_dtls_server_trusted_certificate_add)
- [<span data-ttu-id="1a36b-120">nx_secure_dtls_server_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1a36b-120">nx_secure_dtls_server_trusted_certificate_remove</span></span>](#nx_secure_dtls_server_trusted_certificate_remove)
- [<span data-ttu-id="1a36b-121">nx_secure_dtls_server_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="1a36b-121">nx_secure_dtls_server_x509_client_verify_configure</span></span>](#nx_secure_dtls_server_x509_client_verify_configure)
- [<span data-ttu-id="1a36b-122">nx_secure_dtls_server_x509_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="1a36b-122">nx_secure_dtls_server_x509_client_verify_disable</span></span>](#nx_secure_dtls_server_x509_client_verify_disable)
- [<span data-ttu-id="1a36b-123">nx_secure_dtls_session_client_info_get</span><span class="sxs-lookup"><span data-stu-id="1a36b-123">nx_secure_dtls_session_client_info_get</span></span>](#nx_secure_dtls_session_client_info_get)
- [<span data-ttu-id="1a36b-124">nx_secure_dtls_session_create</span><span class="sxs-lookup"><span data-stu-id="1a36b-124">nx_secure_dtls_session_create</span></span>](#nx_secure_dtls_session_create)
- [<span data-ttu-id="1a36b-125">nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1a36b-125">nx_secure_dtls_session_delete</span></span>](#nx_secure_dtls_session_delete)
- [<span data-ttu-id="1a36b-126">nx_secure_dtls_session_end</span><span class="sxs-lookup"><span data-stu-id="1a36b-126">nx_secure_dtls_session_end</span></span>](#nx_secure_dtls_session_end)
- [<span data-ttu-id="1a36b-127">nx_secure_dtls_session_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-127">nx_secure_dtls_session_local_certificate_add</span></span>](#nx_secure_dtls_session_local_certificate_add)
- [<span data-ttu-id="1a36b-128">nx_secure_dtls_session_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1a36b-128">nx_secure_dtls_session_local_certificate_remove</span></span>](#nx_secure_dtls_session_local_certificate_remove)
- [<span data-ttu-id="1a36b-129">nx_secure_dtls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1a36b-129">nx_secure_dtls_session_receive</span></span>](#nx_secure_dtls_session_receive)
- [<span data-ttu-id="1a36b-130">nx_secure_dtls_session_reset</span><span class="sxs-lookup"><span data-stu-id="1a36b-130">nx_secure_dtls_session_reset</span></span>](#nx_secure_dtls_session_reset)
- [<span data-ttu-id="1a36b-131">nx_secure_dtls_ session_send</span><span class="sxs-lookup"><span data-stu-id="1a36b-131">nx_secure_dtls_ session_send</span></span>](#nx_secure_dtls_-session_send)
- [<span data-ttu-id="1a36b-132">nx_secure_dtls_session_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-132">nx_secure_dtls_session_trusted_certificate_add</span></span>](#nx_secure_dtls_session_trusted_certificate_add)
- [<span data-ttu-id="1a36b-133">nx_secure_dtls_session_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1a36b-133">nx_secure_dtls_session_trusted_certificate_remove</span></span>](#nx_secure_dtls_session_trusted_certificate_remove)


## <a name="nx_secure_dtls_client_session_start"></a><span data-ttu-id="1a36b-134">nx_secure_dtls_client_session_start</span><span class="sxs-lookup"><span data-stu-id="1a36b-134">nx_secure_dtls_client_session_start</span></span>

<span data-ttu-id="1a36b-135">Avviare una sessione client NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-135">Start a NetX Secure DTLS Client Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-136">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-136">Prototype</span></span>

```C
UINT nx_secure_dtls_client_session_start(
                        NX_SECURE_DTLS_SESSION *dtls_session,
                        NX_UDP_SOCKET *udp_socket,
                        NXD_ADDRESS *ip_address, UINT port,
                        UINT wait_option);

```

### <a name="description"></a><span data-ttu-id="1a36b-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-137">Description</span></span>

<span data-ttu-id="1a36b-138">Questo servizio avvia una sessione client DTLS, connettendosi al server all'indirizzo IP e alla porta UDP specificati, usando il socket UDP fornito per le comunicazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="1a36b-138">This service starts a DTLS Client session, connecting to the server at the provided IP address and UDP port, using the provided UDP socket for network communications.</span></span>

<span data-ttu-id="1a36b-139">Il blocco di controllo della sessione DTLS deve essere inizializzato prima di chiamare il servizio utilizzando nx_secure_dtls_session_create.</span><span class="sxs-lookup"><span data-stu-id="1a36b-139">The DTLS session control block must be initialized prior to calling this service using nx_secure_dtls_session_create.</span></span> <span data-ttu-id="1a36b-140">Inoltre, il client di DTLS richiede che almeno un certificato CA attendibile sia stato aggiunto alla sessione utilizzando nx_secure_dtls_session_trusted_certificate_add o che siano abilitate e configurate chiavi precondivise.</span><span class="sxs-lookup"><span data-stu-id="1a36b-140">Additionally, the DTLS Client requires that at least one trusted CA certificate has been added to the session using nx_secure_dtls_session_trusted_certificate_add or Pre-Shared Keys are enabled and configured.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-141">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-141">Parameters</span></span>

- <span data-ttu-id="1a36b-142">**dtls_session** Puntatore a una struttura di sessione DTLS inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-142">**dtls_session** Pointer to a DTLS Session structure that was initialized previously.</span></span>
- <span data-ttu-id="1a36b-143">**udp_socket** Socket UDP inizializzato che verrà usato per stabilire le comunicazioni di rete con il server DTLS remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-143">**udp_socket** Initialized UDP socket that will be used to establish network communications with the remote DTLS server.</span></span>
- <span data-ttu-id="1a36b-144">**ip_address** Puntatore alla struttura degli indirizzi IP che contiene l'indirizzo del server DTLS remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-144">**ip_address** Pointer to IP address structure containing the address of the remote DTLS server.</span></span>
- <span data-ttu-id="1a36b-145">**porta** Socket UDP inizializzato che verrà usato per stabilire le comunicazioni di rete con il server DTLS remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-145">**port** Initialized UDP socket that will be used to establish network communications with the remote DTLS server.</span></span>
- <span data-ttu-id="1a36b-146">**WAIT_OPTION** Opzione di sospensione per il tentativo di connessione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-146">**wait_option** Suspension option for connection attempt.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-147">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-147">Return Values</span></span>

- <span data-ttu-id="1a36b-148">**NX_SUCCESS** (0x00) assegnazione del certificato alla sessione completata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-148">**NX_SUCCESS** (0x00) Successful assignment of certificate to session.</span></span>
- <span data-ttu-id="1a36b-149">**NX_NOT_CONNECTED** (0x38) non è possibile raggiungere il server con l'indirizzo e la porta specificati.</span><span class="sxs-lookup"><span data-stu-id="1a36b-149">**NX_NOT_CONNECTED** (0x38) The server cannot be reached at the given address and port.</span></span>
- <span data-ttu-id="1a36b-150">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0X102) un tipo di messaggio TLS/DTLS ricevuto non è corretto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-150">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) A received TLS/DTLS message type is incorrect.</span></span>
- <span data-ttu-id="1a36b-151">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0X106) una crittografia fornita dall'host remoto non è supportata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-151">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A cipher provided by the remote host is not supported.</span></span>
- <span data-ttu-id="1a36b-152">L'elaborazione del messaggio **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) durante l'handshake TLS non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-152">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) Message processing during the TLS handshake has failed.</span></span>
- <span data-ttu-id="1a36b-153">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0X108) un messaggio in arrivo non ha superato un controllo Mac hash.</span><span class="sxs-lookup"><span data-stu-id="1a36b-153">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) An incoming message failed a hash MAC check.</span></span>
- <span data-ttu-id="1a36b-154">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) non è stato possibile inviare un socket TCP sottostante.</span><span class="sxs-lookup"><span data-stu-id="1a36b-154">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) An underlying TCP socket send failed.</span></span>
- <span data-ttu-id="1a36b-155">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0X10A) un messaggio in ingresso ha un campo di lunghezza non valido.</span><span class="sxs-lookup"><span data-stu-id="1a36b-155">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) An incoming message had an invalid length field.</span></span>
- <span data-ttu-id="1a36b-156">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0X10B) un messaggio ChangeCipherSpec in ingresso non è corretto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-156">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10B) An incoming ChangeCipherSpec message was incorrect.</span></span>
- <span data-ttu-id="1a36b-157">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0X10C) un certificato TLS in ingresso non è utilizzabile per identificare il server DTLS remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-157">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10C) An incoming TLS certificate is unusable for identifying the remote DTLS server.</span></span>
- <span data-ttu-id="1a36b-158">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0X10D) la crittografia a chiave pubblica fornita dall'host remoto non è supportata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-158">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) The public-key cipher provided by the remote host is unsupported.</span></span>
- <span data-ttu-id="1a36b-159">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0X10E) l'host remoto non ha indicato ciphersuites supportati dallo stack NETX Secure DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-159">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) The remote host has indicated no ciphersuites that are supported by the NetX Secure DTLS stack.</span></span>
- <span data-ttu-id="1a36b-160">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0X10F) un messaggio DTLS ricevuto ha una versione DTLS sconosciuta nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-160">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received DTLS message had an unknown DTLS version in its header.</span></span>
- <span data-ttu-id="1a36b-161">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) un messaggio DTLS ricevuto ha una versione DTLS nota ma non supportata nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-161">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) A received DTLS message had a known but unsupported DTLS version in its header.</span></span>
- <span data-ttu-id="1a36b-162">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0X111) l'allocazione di pacchetti TLS interna non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-162">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) An internal TLS packet allocation failed.</span></span>
- <span data-ttu-id="1a36b-163">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0X112) l'host remoto ha fornito un certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="1a36b-163">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) The remote host provided an invalid certificate.</span></span>
- <span data-ttu-id="1a36b-164">**NX_SECURE_TLS_ALERT_RECEIVED** (0X114) l'host remoto ha inviato un avviso che indica un errore e termina la sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-164">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) The remote host sent an alert indicating an error and ending the TLS session.</span></span>
- <span data-ttu-id="1a36b-165">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0X13B) una voce nella tabella ciphersuite include un puntatore a funzione null.</span><span class="sxs-lookup"><span data-stu-id="1a36b-165">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13B) An entry in the ciphersuite table had a NULL function pointer.</span></span>
- <span data-ttu-id="1a36b-166">**NX_PTR_ERROR** (0x07) una sessione, un socket o un puntatore di indirizzo non valido.</span><span class="sxs-lookup"><span data-stu-id="1a36b-166">**NX_PTR_ERROR** (0x07) Invalid session, socket, or address pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-167">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-167">Allowed From</span></span>

<span data-ttu-id="1a36b-168">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-168">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-169">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-169">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                           &nx_crypto_tls_ciphers,
                                           crypto_metadata,
                                           sizeof(crypto_metadata),
                                           packet_buffer,
                                           sizeof(packet_buffer),
                                           REMOTE_CERT_NUMBER,
                                           remote_certs_buffer,
                                           sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
       Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                      trusted_cert_der,
                                      trusted_cert_der_len,
                                      NX_NULL, 0, NX_NULL, 0,
                                      NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                   &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                                  &udp_socket, &server_ip,
                                                  4443,
                                                  NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
      /* Error! */
      return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session, &receive_packet,
                                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session, NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-170">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-170">See Also</span></span>

- <span data-ttu-id="1a36b-171">nx_secure_dtls_session_receive, nx_secure_dtls_session_send,</span><span class="sxs-lookup"><span data-stu-id="1a36b-171">nx_secure_dtls_session_receive, nx_secure_dtls_session_send,</span></span>
- <span data-ttu-id="1a36b-172">nx_secure_dtls_session_create</span><span class="sxs-lookup"><span data-stu-id="1a36b-172">nx_secure_dtls_session_create</span></span>

## <a name="nx_secure_dtls_packet_allocate"></a><span data-ttu-id="1a36b-173">nx_secure_dtls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="1a36b-173">nx_secure_dtls_packet_allocate</span></span>

<span data-ttu-id="1a36b-174">Allocare un pacchetto per una sessione DTLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="1a36b-174">Allocate a packet for a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-175">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-175">Prototype</span></span>

```C
UINT  nx_secure_dtls_packet_allocate(
                              NX_SECURE_DTLS_SESSION *session_ptr,
                         NX_PACKET_POOL *pool_ptr,
                         NX_PACKET **packet_ptr,
                              ULONG wait_option);

```

### <a name="description"></a><span data-ttu-id="1a36b-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-176">Description</span></span>

<span data-ttu-id="1a36b-177">Questo servizio alloca un NX_PACKET per la sessione DTLS attiva specificata dalla NX_PACKET_POOL specificata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-177">This service allocates an NX_PACKET for the specified active DTLS session from the specified NX_PACKET_POOL.</span></span> <span data-ttu-id="1a36b-178">Questo servizio deve essere chiamato dall'applicazione per allocare i pacchetti di dati da inviare tramite una connessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-178">This service should be called by the application to allocate data packets to be sent over a DTLS connection.</span></span> <span data-ttu-id="1a36b-179">La sessione DTLS deve essere inizializzata prima di chiamare il servizio.</span><span class="sxs-lookup"><span data-stu-id="1a36b-179">The DTLS session must be initialized before calling this service.</span></span>

<span data-ttu-id="1a36b-180">Il pacchetto allocato è stato inizializzato correttamente in modo che i dati di intestazione e piè di pagina DTLS possano essere aggiunti dopo il popolamento dei dati del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-180">The allocated packet is properly initialized so that DTLS header and footer data may be added after the packet data is populated.</span></span> <span data-ttu-id="1a36b-181">In caso contrario, il comportamento è identico a *nx_packet_allocate*.</span><span class="sxs-lookup"><span data-stu-id="1a36b-181">The behavior is otherwise identical to *nx_packet_allocate*.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-182">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-182">Parameters</span></span>

- <span data-ttu-id="1a36b-183">**session_ptr** Puntatore a un'istanza di sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-183">**session_ptr** Pointer to a DTLS Session instance.</span></span>
- <span data-ttu-id="1a36b-184">**pool_ptr** Puntatore a un NX_PACKET_POOL da cui allocare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-184">**pool_ptr** Pointer to an NX_PACKET_POOL from which to allocate the packet.</span></span>
- <span data-ttu-id="1a36b-185">**packet_ptr** Puntatore di output al pacchetto appena allocato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-185">**packet_ptr** Output pointer to the newly-allocated packet.</span></span>
- <span data-ttu-id="1a36b-186">**WAIT_OPTION** Opzione di sospensione per l'allocazione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1a36b-186">**wait_option** Suspension option for packet allocation.</span></span>


### <a name="return-values"></a><span data-ttu-id="1a36b-187">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-187">Return Values</span></span>

- <span data-ttu-id="1a36b-188">**NX_SUCCESS** (0x00) allocare il pacchetto correttamente.</span><span class="sxs-lookup"><span data-stu-id="1a36b-188">**NX_SUCCESS** (0x00) Successful packet allocate.</span></span>
- <span data-ttu-id="1a36b-189">L'allocazione del pacchetto sottostante **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-189">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Underlying packet allocation failed.</span></span>
- <span data-ttu-id="1a36b-190">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0X101) la sessione DTLS fornita non è stata inizializzata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-190">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied DTLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-191">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-191">Allowed From</span></span>

<span data-ttu-id="1a36b-192">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-192">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-193">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-193">Example</span></span>

```C
/* Allocate a new DTLS packet from the previously created packet pool and
previously initialized DTLS session.   */

status = nx_secure_dtls_packet_allocate(&dtls_session, &pool_0, &packet_ptr,
                                                              NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in
the variable packet_ptr.  */

```

### <a name="see-also"></a><span data-ttu-id="1a36b-194">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-194">See Also</span></span>

- <span data-ttu-id="1a36b-195">nx_secure_x509_certificate_initialize, nx_secure_dtls_session_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-195">nx_secure_x509_certificate_initialize, nx_secure_dtls_session_create,</span></span>
- <span data-ttu-id="1a36b-196">nx_secure_dtls_session_trusted_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="1a36b-196">nx_secure_dtls_session_trusted_certificate_add,</span></span>
- <span data-ttu-id="1a36b-197">nx_secure_dtls_session_send, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-197">nx_secure_dtls_session_send, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-198">nx_secure_dtls_session_end, nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1a36b-198">nx_secure_dtls_session_end, nx_secure_dtls_session_delete</span></span>

## <a name="nx_secure_dtls_psk_add"></a><span data-ttu-id="1a36b-199">nx_secure_dtls_psk_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-199">nx_secure_dtls_psk_add</span></span>

<span data-ttu-id="1a36b-200">Aggiungere una chiave precondivisa a una sessione di DTLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="1a36b-200">Add a Pre-Shared Key to a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-201">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-201">Prototype</span></span>

```C
UINT  nx_secure_dtls_psk_add(NX_SECURE_DTLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a><span data-ttu-id="1a36b-202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-202">Description</span></span>

<span data-ttu-id="1a36b-203">Questo servizio aggiunge una chiave precondivisa (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo della sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-203">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a DTLS Session control block.</span></span> <span data-ttu-id="1a36b-204">Il valore PSK viene usato al posto di un certificato digitale quando si Abilita e si usa PSK ciphersuites.</span><span class="sxs-lookup"><span data-stu-id="1a36b-204">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-205">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-205">Parameters</span></span>

- <span data-ttu-id="1a36b-206">**session_ptr** Puntatore a un'istanza di sessione DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-206">**session_ptr** Pointer to a previously created DTLS Session instance.</span></span>
- <span data-ttu-id="1a36b-207">**pre_shared_key** Valore PSK effettivo.</span><span class="sxs-lookup"><span data-stu-id="1a36b-207">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="1a36b-208">**psk_length** Lunghezza del valore PSK.</span><span class="sxs-lookup"><span data-stu-id="1a36b-208">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="1a36b-209">**psk_identity** Stringa utilizzata per identificare il valore PSK.</span><span class="sxs-lookup"><span data-stu-id="1a36b-209">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="1a36b-210">**identity_length** Lunghezza dell'identità PSK.</span><span class="sxs-lookup"><span data-stu-id="1a36b-210">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="1a36b-211">**hint** Stringa utilizzata per indicare il gruppo di precondivise da scegliere in un server TLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-211">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="1a36b-212">**hint_length** Lunghezza della stringa del suggerimento.</span><span class="sxs-lookup"><span data-stu-id="1a36b-212">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-213">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-213">Return Values</span></span>

- <span data-ttu-id="1a36b-214">L'aggiunta di PSK è stata completata **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1a36b-214">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="1a36b-215">**NX_PTR_ERROR** (0x07) puntatore di sessione DTLS non valido.</span><span class="sxs-lookup"><span data-stu-id="1a36b-215">**NX_PTR_ERROR** (0x07) Invalid DTLS session pointer.</span></span>
- <span data-ttu-id="1a36b-216">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0X125) non è in grado di aggiungere un'altra PSK.</span><span class="sxs-lookup"><span data-stu-id="1a36b-216">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-217">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-217">Allowed From</span></span>

<span data-ttu-id="1a36b-218">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-218">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-219">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-219">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to DTLS session.  */
status =  nx_secure_dtls_psk_add(&dtls_session, psk,
                            sizeof(psk), “psk_1”, 4,
                            “Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */


```

### <a name="see-also"></a><span data-ttu-id="1a36b-220">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-220">See Also</span></span>

- <span data-ttu-id="1a36b-221">nx_secure_dtls_server_psk_add, nx_secure_dtls_client_session_create</span><span class="sxs-lookup"><span data-stu-id="1a36b-221">nx_secure_dtls_server_psk_add, nx_secure_dtls_client_session_create</span></span>

## <a name="nx_secure_dtls_server_create"></a><span data-ttu-id="1a36b-222">nx_secure_dtls_server_create</span><span class="sxs-lookup"><span data-stu-id="1a36b-222">nx_secure_dtls_server_create</span></span>

<span data-ttu-id="1a36b-223">Creare un server DTLS Secure NetX</span><span class="sxs-lookup"><span data-stu-id="1a36b-223">Create a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-224">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-224">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_create(
                NX_SECURE_DTLS_SERVER *server_ptr, NX_IP *ip_ptr,
                UINT port, ULONG timeout, VOID *session_buffer,
                UINT session_buffer_size,
                const NX_SECURE_TLS_CRYPTO *crypto_table,
                VOID *crypto_metadata_buffer, ULONG crypto_metadata_size,
                UCHAR *packet_reassembly_buffer,
                UINT packet_reassembly_buffer_size,
                UINT (*connect_notify)(
                              NX_SECURE_DTLS_SESSION *dtls_session,
                              NXD_ADDRESS *ip_address, UINT port),
                UINT (*receive_notify)(
                              NX_SECURE_DTLS_SESSION *dtls_session)));

```

### <a name="description"></a><span data-ttu-id="1a36b-225">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-225">Description</span></span>

<span data-ttu-id="1a36b-226">Questo servizio crea un'istanza di un server DTLS per gestire le richieste DTLS in ingresso su una determinata porta UDP.</span><span class="sxs-lookup"><span data-stu-id="1a36b-226">This service creates an instance of a DTLS server to handle incoming DTLS requests on a particular UDP port.</span></span> <span data-ttu-id="1a36b-227">A causa del fatto che UDP è senza stato, le richieste DTLS da più client possono entrare in un'unica porta mentre altre sessioni DTLS sono attive.</span><span class="sxs-lookup"><span data-stu-id="1a36b-227">Due to the fact that UDP is stateless, DTLS requests from multiple clients can come in on a single port while other DTLS sessions are active.</span></span> <span data-ttu-id="1a36b-228">Il server è quindi necessario per mantenere le sessioni attive e indirizzare correttamente i messaggi in ingresso al gestore appropriato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-228">Thus, the server is needed to maintain active sessions and properly route incoming messages to the proper handler.</span></span>

<span data-ttu-id="1a36b-229">Il parametro ip_ptr punta a un'istanza di NX_IP da utilizzare per il socket UDP interno associato al server DTLS (e archiviato nel blocco di controllo NX_SECURE_DTLS_SERVER).</span><span class="sxs-lookup"><span data-stu-id="1a36b-229">The ip_ptr parameter points to an NX_IP instance to be used for the internal UDP socket associated with the DTLS Server (and stored in the NX_SECURE_DTLS_SERVER control block).</span></span> <span data-ttu-id="1a36b-230">L'istanza e la porta IP vengono utilizzate per definire l'interfaccia UDP su cui viene creata un'istanza del server con il servizio nx_secure_dtls_server_start.</span><span class="sxs-lookup"><span data-stu-id="1a36b-230">The IP instance and port are used to define the UDP interface upon which the server is instantiated with the nx_secure_dtls_server_start service.</span></span>

<span data-ttu-id="1a36b-231">Il parametro buffer sessione viene usato per memorizzare i blocchi di controllo per tutte le sessioni DTLS simultanee possibili per il server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-231">The session buffer parameter is used to hold the control blocks for all the possible simultaneous DTLS sessions for the DTLS server.</span></span> <span data-ttu-id="1a36b-232">Deve essere allocato con una dimensione pari a un multiplo della dimensione della struttura del blocco di controllo NX_SECURE_DTLS_SESSION.</span><span class="sxs-lookup"><span data-stu-id="1a36b-232">It should be allocated with a size that is an even multiple of the size of the NX_SECURE_DTLS_SESSION control block structure.</span></span>

<span data-ttu-id="1a36b-233">Per calcolare le dimensioni necessarie per i metadati, è possibile usare l'API nx_secure_tls_metadata_size_calculate.</span><span class="sxs-lookup"><span data-stu-id="1a36b-233">To calculate the necessary metadata size, the API nx_secure_tls_metadata_size_calculate may be used.</span></span>

<span data-ttu-id="1a36b-234">Il parametro packet_reassembly_buffer viene usato da DTLS per riassemblare i datagrammi UDP in un record DTLS completo ai fini della decrittografia e deve essere sufficientemente grande da contenere il record DTLS previsto più grande (16KB è la DTLS dimensioni massime dei record, ma molte applicazioni non inviano la quantità di dati in un singolo record).</span><span class="sxs-lookup"><span data-stu-id="1a36b-234">The packet_reassembly_buffer parameter is used by DTLS to reassemble UDP datagrams into a complete DTLS record for the purposes of decryption and should be large enough to accommodate the largest expected DTLS record (16KB is the DTLS maximum record size but many applications don’t send that much data in a single record).</span></span>

<span data-ttu-id="1a36b-235">La routine di callback connect_notify viene richiamata ogni volta che un nuovo client DTLS si connette al server.</span><span class="sxs-lookup"><span data-stu-id="1a36b-235">The connect_notify callback routine is invoked whenever a new DTLS client connects to the server.</span></span> <span data-ttu-id="1a36b-236">Spetta all'applicazione avviare la sessione DTLS usando il servizio *nx_secure_dtls_server_session_start*.</span><span class="sxs-lookup"><span data-stu-id="1a36b-236">It is up to the application to then start the DTLS session using the service *nx_secure_dtls_server_session_start*.</span></span> <span data-ttu-id="1a36b-237">Sebbene la sessione possa essere avviata nel callback stesso, è consigliabile usare il callback solo per notificare al thread dell'applicazione (o a un thread DTLS dedicato creato dall'applicazione) la connessione, perché il callback viene richiamato dal thread IP usato per elaborare tutte le operazioni di elaborazione di rete di livello inferiore (ad esempio UDP).</span><span class="sxs-lookup"><span data-stu-id="1a36b-237">While the session may be started in the callback itself, it is recommended that the callback only be used to notify the application thread (or dedicated DTLS thread created by the application) of the connection as the callback is invoked by the IP thread which is used to process all lower-level network processing (e.g. UDP).</span></span> <span data-ttu-id="1a36b-238">Questa operazione può essere semplice quanto il salvataggio del parametro della sessione DTLS, fornito come parametro al callback, e la chiamata di nx_secure_dtls_server_session_start nell'altro thread.</span><span class="sxs-lookup"><span data-stu-id="1a36b-238">This can be as simple as saving the DTLS session parameter (provided as a parameter to the callback) and invoking nx_secure_dtls_server_session_start in the other thread.</span></span> <span data-ttu-id="1a36b-239">Il callback connect_notify in genere restituisce NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-239">The connect_notify callback should generally return NX_SUCCESS.</span></span>

<span data-ttu-id="1a36b-240">La routine di callback receive_notify viene richiamata ogni volta che viene ricevuto un record DTLS che corrisponde a una sessione DTLS stabilita esistente (l'indirizzo IP e la porta dell'host remoto vengono usati per identificare una sessione esistente).</span><span class="sxs-lookup"><span data-stu-id="1a36b-240">The receive_notify callback routine is invoked whenever a DTLS record is received that matches an existing established DTLS session (the remote host IP address and port are used to identify an existing session).</span></span> <span data-ttu-id="1a36b-241">Rappresenta i "dati dell'applicazione" crittografati e inviati tramite DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-241">This represents the “application data” that is encrypted and sent over DTLS.</span></span> <span data-ttu-id="1a36b-242">Per recuperare i dati ricevuti, l'applicazione deve chiamare il servizio *nx_secure_dtls_session_receive* nella sessione DTLS fornita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-242">The application must call the service *nx_secure_dtls_session_receive* on the provided DTLS session to retrieve the received data.</span></span> <span data-ttu-id="1a36b-243">Come per l'connect_receive callback, è consigliabile passare la sessione a un altro thread per gestire l'elaborazione del messaggio in quanto il callback viene richiamato dal thread IP.</span><span class="sxs-lookup"><span data-stu-id="1a36b-243">As with the connect_receive callback, it is recommended that the session be passed to another thread to handle the message processing as the callback is invoked from the IP thread.</span></span> <span data-ttu-id="1a36b-244">Il callback receive_notify in genere restituisce NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-244">The receive_notify callback should generally return NX_SUCCESS.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-245">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-245">Parameters</span></span>

- <span data-ttu-id="1a36b-246">**server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-246">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="1a36b-247">**ip_ptr** Puntatore a un blocco di controllo NX_IP inizializzato da utilizzare come interfaccia di rete per il server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-247">**ip_ptr** Pointer to an initialized NX_IP control block to use as the network interface for the DTLS server.</span></span>
- <span data-ttu-id="1a36b-248">**porta** Porta UDP locale a cui è associato il socket UDP del server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-248">**port** The local UDP port to which the DTLS server UDP socket is bound.</span></span>
- <span data-ttu-id="1a36b-249">**timeout** Valore di timeout da utilizzare per le operazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="1a36b-249">**timeout** Timeout value to use for network operations.</span></span>
- <span data-ttu-id="1a36b-250">**session_buffer** Spazio del buffer che contiene i blocchi di controllo per tutte le istanze di NX_SECURE_DTLS_SESSION assegnati a questa istanza del server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-250">**session_buffer** Buffer space to contain control blocks for all instances of NX_SECURE_DTLS_SESSION assigned to this DTLS Server instance.</span></span>
- <span data-ttu-id="1a36b-251">**session_buffer_size** Dimensioni del buffer della sessione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-251">**session_buffer_size** Size of the session buffer.</span></span> <span data-ttu-id="1a36b-252">Questo determina il numero di sessioni DTLS assegnate al server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-252">This determines the number of DTLS sessions assigned to the DTLS Server.</span></span>
- <span data-ttu-id="1a36b-253">**crypto_table** Puntatore a una struttura della tabella di crittografia TLS/DTLS utilizzata per tutte le operazioni di crittografia.</span><span class="sxs-lookup"><span data-stu-id="1a36b-253">**crypto_table** Pointer to a TLS/DTLS encryption table structure used for all cryptographic operations.</span></span>
- <span data-ttu-id="1a36b-254">**crypto_metadata_buffer** Spazio del buffer per i calcoli delle operazioni di crittografia e le informazioni sullo stato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-254">**crypto_metadata_buffer** Buffer space for cryptographic operation calculations and state information.</span></span>
- <span data-ttu-id="1a36b-255">**crypto_metadata_size** Dimensioni del buffer dei metadati.</span><span class="sxs-lookup"><span data-stu-id="1a36b-255">**crypto_metadata_size** Size of metadata buffer.</span></span>
- <span data-ttu-id="1a36b-256">**packet_reassembly_buffer** Buffer utilizzato da DTLS per riassemblare i dati UDP nei record DTLS per la decrittografia.</span><span class="sxs-lookup"><span data-stu-id="1a36b-256">**packet_reassembly_buffer** Buffer used by DTLS to reassemble UDP data into DTLS records for decryption.</span></span>
- <span data-ttu-id="1a36b-257">**packet_reassembly_buffer_size** Dimensioni del buffer di riassemblaggio.</span><span class="sxs-lookup"><span data-stu-id="1a36b-257">**packet_reassembly_buffer_size** Size of reassembly buffer.</span></span> <span data-ttu-id="1a36b-258">In genere deve essere maggiore di 16KB, ma può essere minore a seconda dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-258">Generally should be greater than 16KB but may be smaller depending on application.</span></span>
- <span data-ttu-id="1a36b-259">**connect_notify** Routine di callback richiamata ogni volta che un client DTLS remoto tenta di connettersi a questo server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-259">**connect_notify** Callback routine invoked whenever a remote DTLS Client attempts to connect to this DTLS server.</span></span>
- <span data-ttu-id="1a36b-260">**receive_notify** Callback richiamato ogni volta che vengono ricevuti i dati dell'applicazione su una sessione DTLS esistente.</span><span class="sxs-lookup"><span data-stu-id="1a36b-260">**receive_notify** Callback invoked whenever application data is received over an existing DTLS session.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-261">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-261">Return Values</span></span>

- <span data-ttu-id="1a36b-262">**NX_SUCCESS** (0x00) la creazione del server DTLS è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-262">**NX_SUCCESS** (0x00) Successful creation of DTLS server.</span></span>
- <span data-ttu-id="1a36b-263">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-263">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-264">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) non è sufficiente spazio del buffer per le sessioni, il riassemblaggio dei pacchetti o la crittografia.</span><span class="sxs-lookup"><span data-stu-id="1a36b-264">**NX_INVALID_PARAMETERS** (0x4D) Not enough buffer space for sessions, packet reassembly, or cryptography.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-265">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-265">Allowed From</span></span>

<span data-ttu-id="1a36b-266">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-266">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-267">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-267">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
    *ip_address, UINT port)
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

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
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
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

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
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                           NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session, &packet_pool,
                                                   &send_packet, NX_IP_PERIODIC_RATE);

        /* Check for errors and prepare response data
        (e.g. nx_packet_data_append). */

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

        }

        /* If not processing connections or received data,
        let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* Server processing is done, stop the server
    instance from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-268">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-268">See Also</span></span>

- <span data-ttu-id="1a36b-269">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span><span class="sxs-lookup"><span data-stu-id="1a36b-269">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span></span>
- <span data-ttu-id="1a36b-270">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="1a36b-270">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="1a36b-271">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-271">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="1a36b-272">nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="1a36b-272">nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="1a36b-273">nx_secure_dtls_server_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-273">nx_secure_dtls_server_local_certificate_add</span></span>

## <a name="nx_secure_dtls_server_delete"></a><span data-ttu-id="1a36b-274">nx_secure_dtls_server_delete</span><span class="sxs-lookup"><span data-stu-id="1a36b-274">nx_secure_dtls_server_delete</span></span>

<span data-ttu-id="1a36b-275">Liberare le risorse usate da un server DTLS sicuro NetX</span><span class="sxs-lookup"><span data-stu-id="1a36b-275">Free up resources used by a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-276">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-276">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_delete(NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a><span data-ttu-id="1a36b-277">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-277">Description</span></span>

<span data-ttu-id="1a36b-278">Questo servizio consente di liberare le risorse allocate a un'istanza del server DTLS, incluso il socket UDP interno usato dal server.</span><span class="sxs-lookup"><span data-stu-id="1a36b-278">This service frees up the resources allocated to a DTLS Server instance, including the internal UDP socket used by the server.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-279">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-279">Parameters</span></span>

- <span data-ttu-id="1a36b-280">**server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-280">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-281">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-281">Return Values</span></span>

- <span data-ttu-id="1a36b-282">L'eliminazione del server è riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1a36b-282">**NX_SUCCESS** (0x00) Successful deletion of server.</span></span>
- <span data-ttu-id="1a36b-283">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-283">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-284">Il socket UDP **NX_STILL_BOUND** (0x42) è ancora associato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-284">**NX_STILL_BOUND** (0x42) UDP socket is still bound.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-285">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-285">Allowed From</span></span>

<span data-ttu-id="1a36b-286">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-286">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-287">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-287">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
*ip_address, UINT port)
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

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                            LOCAL_SERVER_PORT,
                                            NX_IP_PERIODIC_RATE,
                                            dtls_server_session_buffer,
                                            sizeof(dtls_server_session_buffer),
                                            &tls_crypto_table,
                                            crypto_metadata_buffer,
                                            sizeof(crypto_metadata_buffer),
                                            packet_buffer, sizeof(packet_buffer),
                                            dtls_server_connect_notify,
                                            dtls_server_receive_notify);


    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);


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
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                         NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                        &packet_pool,
                                                        &send_packet,
                                                        NX_IP_PERIODIC_RATE);

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-288">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-288">See Also</span></span>

- <span data-ttu-id="1a36b-289">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-289">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="1a36b-290">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="1a36b-290">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="1a36b-291">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="1a36b-291">nx_secure_dtls_server_session_start</span></span>

## <a name="nx_secure_dtls_server_local_certificate_add"></a><span data-ttu-id="1a36b-292">nx_secure_dtls_server_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-292">nx_secure_dtls_server_local_certificate_add</span></span>

<span data-ttu-id="1a36b-293">Aggiungere un certificato di identità del server locale a un server NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-293">Add a local server identity certificate to a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-294">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-294">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_local_certificate_add(
                                   NX_SECURE_DTLS_SERVER *server_ptr,
                                 NX_SECURE_X509_CERT *certificate,
                                 UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="1a36b-295">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-295">Description</span></span>

<span data-ttu-id="1a36b-296">Questo servizio aggiunge un certificato di identità del server locale a un'istanza del server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-296">This service adds a local server identity certificate to a DTLS Server instance.</span></span> <span data-ttu-id="1a36b-297">Per la connessione dei client a un server DTLS è necessario almeno un certificato di identità, a meno che non venga utilizzato un meccanismo di autenticazione alternativo, ad esempio chiavi precondivise.</span><span class="sxs-lookup"><span data-stu-id="1a36b-297">At least one identity certificate is required for clients to connect to a DTLS server unless an alternate authentication mechanism (e.g. Pre-Shared Keys) is used.</span></span>

<span data-ttu-id="1a36b-298">Il parametro cert_id è un identificatore numerico diverso da zero per il certificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-298">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="1a36b-299">In questo modo il certificato viene facilmente rimosso o trovato nel caso in cui siano presenti più certificati di identità con lo stesso nome comune X. 509 presente nell'archivio del server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-299">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS server store.</span></span> <span data-ttu-id="1a36b-300">Per ulteriori informazioni sui certificati del server X. 509, vedere la guida dell'utente di NetX Secure TLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-300">See the NetX Secure TLS User Guide for more information about X.509 server certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-301">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-301">Parameters</span></span>

- <span data-ttu-id="1a36b-302">**server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-302">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="1a36b-303">**certificato** di Puntatore a una struttura di certificato X. 509 inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-303">**certificate** Pointer to a previously initialized X.509 certificate structure.</span></span>
- <span data-ttu-id="1a36b-304">**cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-304">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-305">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-305">Return Values</span></span>

- <span data-ttu-id="1a36b-306">**NX_SUCCESS** (0x00) aggiunta del certificato al server DTLS completata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-306">**NX_SUCCESS** (0x00) Successful addition of certificate to DTLS server.</span></span>
- <span data-ttu-id="1a36b-307">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-307">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-308">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) è stato passato un ID certificato 0.</span><span class="sxs-lookup"><span data-stu-id="1a36b-308">**NX_INVALID_PARAMETERS** (0x4D) A certificate ID of 0 was passed in.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-309">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-309">Allowed From</span></span>

<span data-ttu-id="1a36b-310">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-310">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-311">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-311">Example</span></span>

<span data-ttu-id="1a36b-312">\* Per un esempio più completo, vedere informazioni di riferimento per *nx_secure_dtls_server_create* .</span><span class="sxs-lookup"><span data-stu-id="1a36b-312">\*See reference for *nx_secure_dtls_server_create* for a more complete example.</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                            certificate_der_data,
                            sizeof(certificate_der_data),
                            NX_NULL, 0,
                            certificate_key_der_data,
                            sizeof(certificate_key_der_data),
                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Process incoming requests and data. */
    }

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-313">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-313">See Also</span></span>

- <span data-ttu-id="1a36b-314">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-314">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="1a36b-315">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="1a36b-315">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="1a36b-316">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-316">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="1a36b-317">nx_secure_dtls_server_local_certificate_remove,</span><span class="sxs-lookup"><span data-stu-id="1a36b-317">nx_secure_dtls_server_local_certificate_remove,</span></span>
- <span data-ttu-id="1a36b-318">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1a36b-318">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_server_local_certificate_remove"></a><span data-ttu-id="1a36b-319">nx_secure_dtls_server_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1a36b-319">nx_secure_dtls_server_local_certificate_remove</span></span>

<span data-ttu-id="1a36b-320">Rimuovere un certificato di identità del server locale da un server NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-320">Remove a local server identity certificate from a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-321">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-321">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_local_certificate_remove(
                                   NX_SECURE_DTLS_SERVER *server_ptr,
                                   UCHAR *common_name,
                                   UINT common_name_length,
                                   UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="1a36b-322">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-322">Description</span></span>

<span data-ttu-id="1a36b-323">Questo servizio rimuove un certificato di identità del server locale da un'istanza del server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-323">This service removes a local server identity certificate from a DTLS Server instance.</span></span> <span data-ttu-id="1a36b-324">Per la connessione dei client a un server DTLS è necessario almeno un certificato di identità, a meno che non venga utilizzato un meccanismo di autenticazione alternativo, ad esempio chiavi precondivise.</span><span class="sxs-lookup"><span data-stu-id="1a36b-324">At least one identity certificate is required for clients to connect to a DTLS server unless an alternate authentication mechanism (e.g. Pre-Shared Keys) is used.</span></span>

<span data-ttu-id="1a36b-325">Il certificato da rimuovere può essere identificato dal nome comune X. 509 o dal cert_id numerico assegnato nella chiamata a *nx_secure_dtls_server_local_certificate_add*.</span><span class="sxs-lookup"><span data-stu-id="1a36b-325">The certificate to be removed can be identified either by its X.509 Common Name or by the numeric cert_id that was assigned in the call to *nx_secure_dtls_server_local_certificate_add*.</span></span> <span data-ttu-id="1a36b-326">Il cert_id viene usato solo per identificare il certificato ed è gestito dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-326">The cert_id is only used to identify the certificate and is maintained by the application.</span></span> <span data-ttu-id="1a36b-327">Se viene usato il nome comune anziché l'identificatore numerico del certificato, il parametro cert_id deve essere impostato su 0.</span><span class="sxs-lookup"><span data-stu-id="1a36b-327">If the Common Name is used instead of the numeric certificate identifier, the cert_id parameter should be set to 0.</span></span>

> [!NOTE]
> <span data-ttu-id="1a36b-328">La rimozione di un certificato durante l'elaborazione di un handshake DTLS provocherà un comportamento imprevisto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-328">Removing a certificate while a DTLS handshake is being processed will result in unexpected behavior.</span></span> <span data-ttu-id="1a36b-329">Il *nx_secure_dtls_server_stop* del servizio deve essere chiamato prima di rimuovere i certificati.</span><span class="sxs-lookup"><span data-stu-id="1a36b-329">The service *nx_secure_dtls_server_stop* should be called before removing certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-330">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-330">Parameters</span></span>

- <span data-ttu-id="1a36b-331">**server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-331">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="1a36b-332">**common_name** X. 509 CommonName del certificato da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="1a36b-332">**common_name** X.509 CommonName of the certificate to remove.</span></span> <span data-ttu-id="1a36b-333">Se viene usato, passare cert_id come zero.</span><span class="sxs-lookup"><span data-stu-id="1a36b-333">If this is used, pass cert_id as zero.</span></span>
- <span data-ttu-id="1a36b-334">**common_name_length** Lunghezza di common_name stringa in byte.</span><span class="sxs-lookup"><span data-stu-id="1a36b-334">**common_name_length** Length of common_name string in bytes.</span></span>
- <span data-ttu-id="1a36b-335">**cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-335">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span> <span data-ttu-id="1a36b-336">Se si utilizza questa proprietà, passare NX_NULL per il parametro common_name.</span><span class="sxs-lookup"><span data-stu-id="1a36b-336">If this is used, pass NX_NULL for the common_name parameter.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-337">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-337">Return Values</span></span>

- <span data-ttu-id="1a36b-338">**NX_SUCCESS** (0x00) la rimozione del certificato dal server DTLS è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-338">**NX_SUCCESS** (0x00) Successful removal of certificate from DTLS server.</span></span>
- <span data-ttu-id="1a36b-339">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-339">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-340">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0X119) non è stato trovato alcun certificato corrispondente al cert_id o common_name nel server DTLS specificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-340">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate matching the cert_id or common_name was found in the given DTLS server.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-341">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-341">Allowed From</span></span>

<span data-ttu-id="1a36b-342">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-342">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-343">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-343">Example</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT, NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table, crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer), packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                        certificate_der_data,
                                        sizeof(certificate_der_data),
                                        NX_NULL, 0, certificate_key_der_data,
                                        sizeof(certificate_key_der_data),
                                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                     &certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before removing a certificate. */
    Status = nx_secure_dtls_server_stop(&dtls_server);

    /* At some point in the future we decide to remove the certificate we added.
    We can use the certificate identifier we passed into the call to
    nx_secure_dtls_local_certificate_add (value = 1); */
    status = nx_secure_dtls_server_local_certificate_remove(&dtls_server,
                                                          NX_NULL, 0, 1);

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-344">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-344">See Also</span></span>

- <span data-ttu-id="1a36b-345">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-345">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="1a36b-346">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-346">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="1a36b-347">nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="1a36b-347">nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="1a36b-348">nx_secure_dtls_server_local_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="1a36b-348">nx_secure_dtls_server_local_certificate_add,</span></span>
- <span data-ttu-id="1a36b-349">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1a36b-349">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_server_notify_set"></a><span data-ttu-id="1a36b-350">nx_secure_dtls_server_notify_set</span><span class="sxs-lookup"><span data-stu-id="1a36b-350">nx_secure_dtls_server_notify_set</span></span>

<span data-ttu-id="1a36b-351">Assegnare routine di callback di notifica facoltative a un server NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-351">Assign optional notification callback routines to a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-352">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-352">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_notify_set(
                         NX_SECURE_DTLS_SERVER *server_ptr,
                         UINT (*disconnect_notify)(
                                      NX_SECURE_DTLS_SESSION *dtls_session),
                         UINT (*error_notify)(
                                      NX_SECURE_DTLS_SESSION *dtls_session,
                                      UINT error_code));

```

### <a name="description"></a><span data-ttu-id="1a36b-353">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-353">Description</span></span>

<span data-ttu-id="1a36b-354">Questo servizio può essere usato per aggiungere routine di callback di notifica facoltative a un server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-354">This service can be used to add optional notification callback routines to a DTLS server.</span></span> <span data-ttu-id="1a36b-355">Il parametro di callback può essere passato come NX_NULL se si desidera solo un callback.</span><span class="sxs-lookup"><span data-stu-id="1a36b-355">Either callback parameter may be passed as NX_NULL if only one callback is desired.</span></span>

<span data-ttu-id="1a36b-356">Il callback disconnect_notify viene richiamato quando un client remoto termina una sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-356">The disconnect_notify callback is invoked when a remote client ends a DTLS session.</span></span> <span data-ttu-id="1a36b-357">Il dtls_session parametro è l'istanza di sessione che è stata chiusa.</span><span class="sxs-lookup"><span data-stu-id="1a36b-357">The dtls_session parameter is the session instance that was closed.</span></span> <span data-ttu-id="1a36b-358">Il callback generalmente restituisce NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-358">The callback should generally return NX_SUCCESS.</span></span>

<span data-ttu-id="1a36b-359">Il callback error_notify viene richiamato ogni volta che si verifica un errore o un timeout DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-359">The error_notify callback is invoked whenever a DTLS error or timeout occurs.</span></span> <span data-ttu-id="1a36b-360">Il parametro dtls_session è l'istanza di sessione per cui si è verificato l'errore e error_code è il codice di stato numerico per l'errore che ha causato il problema (vedere l'Appendice A)</span><span class="sxs-lookup"><span data-stu-id="1a36b-360">The dtls_session parameter is the session instance for which the error occurred, and error_code is the numeric status code for the error that caused the issue (see Appendix A)</span></span>

<span data-ttu-id="1a36b-361">NetX i codici di errore e di ritorno protetti per un elenco di codici di errore che possono essere restituiti.</span><span class="sxs-lookup"><span data-stu-id="1a36b-361">NetX Secure Return/Error Codes for a list of error codes that may be returned).</span></span> <span data-ttu-id="1a36b-362">Il callback generalmente restituisce NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-362">The callback should generally return NX_SUCCESS.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-363">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-363">Parameters</span></span>

- <span data-ttu-id="1a36b-364">**server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-364">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="1a36b-365">**disconnect_notify** Routine di callback richiamata ogni volta che un host client remoto chiude una sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-365">**disconnect_notify** Callback routine invoked whenever a remote client host closes a DTLS session.</span></span>
- <span data-ttu-id="1a36b-366">**error_notify** Routine di callback richiamata ogni volta che DTLS rileva un errore o un timeout.</span><span class="sxs-lookup"><span data-stu-id="1a36b-366">**error_notify** Callback routine invoked whenever DTLS encounters an error or timeout.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-367">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-367">Return Values</span></span>

- <span data-ttu-id="1a36b-368">**NX_SUCCESS** (0x00) assegnazione riuscita delle routine di callback.</span><span class="sxs-lookup"><span data-stu-id="1a36b-368">**NX_SUCCESS** (0x00) Successful assignment of callback routines.</span></span>
- <span data-ttu-id="1a36b-369">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-369">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-370">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-370">Allowed From</span></span>

<span data-ttu-id="1a36b-371">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-371">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-372">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-372">Example</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

UINT disconnect_notify(NX_SECURE_DTLS_SESSION *dtls_session)
{
NXD_ADDRESS client_ip_addr;
UINT client_port;
UINT local_port;

    /* We have received a disconnection notice (CloseNotify message) from a
       remote client. Application can use the dtls_session parameter for any
       desired processing. */

    /* See what client disconnected by extracting its IP address and port.
       NOTE: depending on how the session ended, the client information may
             no longer be available. */
    status  = nx_secure_dtls_session_client_info_get(dtls_session,
                                                    &ip_addr,
                                                    &client_port,
                                                    &local_port);

    return(NX_SUCCESS);
}

UINT error_notify(NX_SECURE_DTLS_SESSION *dtls_session, UINT error_code)
{
    /* The DTLS server has encountered an error or timeout condition. We
    can use the error_code parameter to determine the error and we
    can insect the dtls_session for more information. */

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Other setup (e.g. certificates) goes here … */

    status = nx_secure_dtls_server_notify_set(&dtls_server, disconnect_notify,
                                                                 error_notify);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-373">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-373">See Also</span></span>

- <span data-ttu-id="1a36b-374">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-374">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="1a36b-375">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-375">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="1a36b-376">nx_secure_dtls_server_session_stop</span><span class="sxs-lookup"><span data-stu-id="1a36b-376">nx_secure_dtls_server_session_stop</span></span>

## <a name="nx_secure_dtls_server_psk_add"></a><span data-ttu-id="1a36b-377">nx_secure_dtls_server_psk_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-377">nx_secure_dtls_server_psk_add</span></span>

<span data-ttu-id="1a36b-378">Aggiungere una chiave precondivisa a un server DTLS sicuro NetX</span><span class="sxs-lookup"><span data-stu-id="1a36b-378">Add a Pre-Shared Key to a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-379">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-379">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_psk_add(
                                NX_SECURE_DTLS_SERVER *server_ptr,
                                UCHAR *pre_shared_key, UINT psk_length,
                                UCHAR *psk_identity,
                                UINT identity_length, UCHAR *hint,
                                UINT hint_length);

```

### <a name="description"></a><span data-ttu-id="1a36b-380">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-380">Description</span></span>

<span data-ttu-id="1a36b-381">Questo servizio aggiunge una chiave precondivisa (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-381">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a DTLS Server control block.</span></span> <span data-ttu-id="1a36b-382">Il valore PSK viene usato al posto di un certificato digitale quando si Abilita e si usa PSK ciphersuites.</span><span class="sxs-lookup"><span data-stu-id="1a36b-382">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

<span data-ttu-id="1a36b-383">La PSK aggiunta viene replicata in tutte le sessioni DTLS assegnate al server DTLS (tramite il buffer della sessione specificato nella chiamata a nx_secure_dtls_server_create).</span><span class="sxs-lookup"><span data-stu-id="1a36b-383">The PSK that is added is replicated across all the DTLS sessions assigned to the DTLS Server (via the session buffer given in the call to nx_secure_dtls_server_create).</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-384">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-384">Parameters</span></span>

- <span data-ttu-id="1a36b-385">**server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-385">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="1a36b-386">**pre_shared_key** Valore PSK effettivo.</span><span class="sxs-lookup"><span data-stu-id="1a36b-386">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="1a36b-387">**psk_length** Lunghezza del valore PSK.</span><span class="sxs-lookup"><span data-stu-id="1a36b-387">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="1a36b-388">**psk_identity** Stringa utilizzata per identificare il valore PSK.</span><span class="sxs-lookup"><span data-stu-id="1a36b-388">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="1a36b-389">**identity_length** Lunghezza dell'identità PSK.</span><span class="sxs-lookup"><span data-stu-id="1a36b-389">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="1a36b-390">**hint** Stringa utilizzata per indicare il gruppo di precondivise da scegliere in un server TLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-390">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="1a36b-391">**hint_length** Lunghezza della stringa del suggerimento.</span><span class="sxs-lookup"><span data-stu-id="1a36b-391">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-392">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-392">Return Values</span></span>

- <span data-ttu-id="1a36b-393">L'aggiunta di PSK è stata completata **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1a36b-393">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="1a36b-394">**NX_PTR_ERROR** (0x07) puntatore al server DTLS non valido.</span><span class="sxs-lookup"><span data-stu-id="1a36b-394">**NX_PTR_ERROR** (0x07) Invalid DTLS server pointer.</span></span>
- <span data-ttu-id="1a36b-395">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0X125) non è in grado di aggiungere un'altra PSK.</span><span class="sxs-lookup"><span data-stu-id="1a36b-395">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-396">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-396">Allowed From</span></span>

<span data-ttu-id="1a36b-397">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-397">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-398">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-398">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to DTLS session.  */
status =  nx_secure_dtls_server_psk_add(&dtls_server, psk, sizeof(psk), “psk_1”,
   4, “Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */

```

### <a name="see-also"></a><span data-ttu-id="1a36b-399">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-399">See Also</span></span>

- <span data-ttu-id="1a36b-400">nx_secure_dtls_psk_add, nx_secure_dtls_server_create</span><span class="sxs-lookup"><span data-stu-id="1a36b-400">nx_secure_dtls_psk_add, nx_secure_dtls_server_create</span></span>

## <a name="nx_secure_dtls_server_session_send"></a><span data-ttu-id="1a36b-401">nx_secure_dtls_server_session_send</span><span class="sxs-lookup"><span data-stu-id="1a36b-401">nx_secure_dtls_server_session_send</span></span>

<span data-ttu-id="1a36b-402">Inviare dati su una sessione DTLS stabilita con un server DTLS protetto NetX</span><span class="sxs-lookup"><span data-stu-id="1a36b-402">Send data over a DTLS session established with a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-403">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-403">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_session_send(
                                NX_SECURE_DTLS_SESSION *session_ptr,
                               NX_PACKET *packet_ptr);

```

### <a name="description"></a><span data-ttu-id="1a36b-404">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-404">Description</span></span>

<span data-ttu-id="1a36b-405">Questo servizio invia un pacchetto di dati su una sessione del server DTLS stabilita a un host client DTLS remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-405">This service sends a packet of data over an established DTLS Server session to a remote DTLS Client host.</span></span> <span data-ttu-id="1a36b-406">La sessione utilizzata viene ottenuta nella routine di callback receive_notify fornita nx_secure_dtls_session_create.</span><span class="sxs-lookup"><span data-stu-id="1a36b-406">The session used is obtained in the receive_notify callback routine provided to nx_secure_dtls_session_create.</span></span>

<span data-ttu-id="1a36b-407">I dati forniti nel pacchetto, che devono essere allocati tramite *nx_secure_dtls_packet_allocate*, vengono crittografati usando le routine e i parametri crittografici della sessione DTLS e quindi inviati all'host remoto tramite la porta UDP interna del server DTLS all'indirizzo IP e alla porta del client collegato (archiviati nella sessione DTLS).</span><span class="sxs-lookup"><span data-stu-id="1a36b-407">The data provided in the packet, which must be allocated using *nx_secure_dtls_packet_allocate*, is encrypted using the DTLS session cryptographic parameters and routines and then sent to the remote host over the DTLS Server internal UDP port to the attached client’s IP address and port (stored in the DTLS Session).</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-408">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-408">Parameters</span></span>

- <span data-ttu-id="1a36b-409">**session_ptr** Puntatore a un'istanza di sessione DTLS ottenuta dalla routine di callback receive_notify fornita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-409">**session_ptr** Pointer to a DTLS session instance obtained from the receive_notify callback routine provided by the application.</span></span>
- <span data-ttu-id="1a36b-410">**packet_ptr** Puntatore a un'istanza di NX_PACKET allocata in precedenza e popolata con i dati dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-410">**packet_ptr** Pointer to an NX_PACKET instance allocated previously and populated with application data.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-411">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-411">Return Values</span></span>

- <span data-ttu-id="1a36b-412">**NX_SUCCESS** (0x00) la creazione del server DTLS è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-412">**NX_SUCCESS** (0x00) Successful creation of DTLS server.</span></span>
- <span data-ttu-id="1a36b-413">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-413">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-414">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) si è verificato un errore nell'operazione di invio UDP sottostante.</span><span class="sxs-lookup"><span data-stu-id="1a36b-414">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) An error occurred in the underlying UDP send operation.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-415">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-415">Allowed From</span></span>

<span data-ttu-id="1a36b-416">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-416">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-417">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-417">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;


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

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key
    and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                        device_cert_der,
                                        device_cert_der_len,
                                        NX_NULL,
                                        0, device_cert_key_der,
                                        device_cert_key_der_len,
                                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);


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

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
        status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

        /* Check for errors and prepare response data
        (e.g. nx_packet_data_append). */

        /* Send response to client. */
        status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                            send_packet);

}

/* If not processing connections or received data, let the thread sleep. */
if(!connect_flag && !receive_flag)
{
    tx_thread_sleep(100);
}
    }

    /* Server processing is done, stop the server instance
    from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-418">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-418">See Also</span></span>

- <span data-ttu-id="1a36b-419">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span><span class="sxs-lookup"><span data-stu-id="1a36b-419">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span></span>
- <span data-ttu-id="1a36b-420">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-420">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_create,</span></span>
- <span data-ttu-id="1a36b-421">nx_secure_dtls_server_session_start, nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="1a36b-421">nx_secure_dtls_server_session_start, nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="1a36b-422">nx_secure_dtls_server_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-422">nx_secure_dtls_server_local_certificate_add</span></span>

## <a name="nx_secure_dtls_server_session_start"></a><span data-ttu-id="1a36b-423">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="1a36b-423">nx_secure_dtls_server_session_start</span></span>

<span data-ttu-id="1a36b-424">Avviare una sessione DTLS da un server NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-424">Start a DTLS Session from a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-425">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-425">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_session_start(
                 NX_SECURE_DTLS_SESSION *session_ptr, UINT wait_option);

```

### <a name="description"></a><span data-ttu-id="1a36b-426">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-426">Description</span></span>

<span data-ttu-id="1a36b-427">Questo servizio avvia una sessione del server DTLS eseguendo l'handshake DTLS sul lato server quando un client DTLS remoto si connette al server e richiede una connessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-427">This service starts a DTLS Server session by performing the server-side DTLS handshake when a remote DTLS Client has connected to the server and requested a DTLS connection.</span></span>

<span data-ttu-id="1a36b-428">La sessione DTLS viene ottenuta nella routine di callback connect_notify fornita nx_secure_dtls_server_create.</span><span class="sxs-lookup"><span data-stu-id="1a36b-428">The DTLS Session is obtained in the connect_notify callback routine provided to nx_secure_dtls_server_create.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-429">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-429">Parameters</span></span>

- <span data-ttu-id="1a36b-430">**session_ptr** Puntatore a un'istanza di sessione DTLS ottenuta da un callback del server DTLS connect_notify.</span><span class="sxs-lookup"><span data-stu-id="1a36b-430">**session_ptr** Pointer to a DTLS Session instance obtained from a DTLS Server connect_notify callback.</span></span>
- <span data-ttu-id="1a36b-431">**WAIT_OPTION** Valore di attesa ThreadX da utilizzare per le operazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="1a36b-431">**wait_option** ThreadX wait value to use for network operations.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-432">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-432">Return Values</span></span>

- <span data-ttu-id="1a36b-433">**NX_SUCCESS** (0x00) la creazione del server DTLS è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-433">**NX_SUCCESS** (0x00) Successful creation of DTLS server.</span></span>
- <span data-ttu-id="1a36b-434">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-434">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-435">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) non è in grado di allocare un pacchetto di handshake DTLS (pool di pacchetti vuoto).</span><span class="sxs-lookup"><span data-stu-id="1a36b-435">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Could not allocate a DTLS handshake packet (packet pool empty).</span></span>
- <span data-ttu-id="1a36b-436">**NX_SECURE_TLS_INVALID_PACKET** (0X104) recevied dati che non sono record DTLS validi.</span><span class="sxs-lookup"><span data-stu-id="1a36b-436">**NX_SECURE_TLS_INVALID_PACKET** (0x104) Recevied data that was not a valid DTLS record.</span></span>
- <span data-ttu-id="1a36b-437">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) non è stato possibile eseguire correttamente l'hashing di un record DTLS (errore di crittografia).</span><span class="sxs-lookup"><span data-stu-id="1a36b-437">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A DTLS record failed to be properly hashed (encryption error).</span></span>
- <span data-ttu-id="1a36b-438">Verifica della riempimento della crittografia **NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12A) non riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-438">**NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12A) Encryption padding check failure.</span></span>
- <span data-ttu-id="1a36b-439">**NX_SECURE_TLS_ALERT_RECEIVED** (0X114) recevied un avviso dall'host remoto durante l'handshake DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-439">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Recevied an alert from the remote host during the DTLS handshake.</span></span>
- <span data-ttu-id="1a36b-440">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0X102) ha ricevuto un messaggio non riconosciuto durante l'handshake DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-440">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) Received an unrecognized message during the DTLS handshake.</span></span>
- <span data-ttu-id="1a36b-441">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0X10A) recevied un record DTLS con una lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="1a36b-441">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) Recevied a DTLS record with an invalid length.</span></span>
- <span data-ttu-id="1a36b-442">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0X10E) ha ricevuto un CLIENTHELLO senza DTLS supportato ciphersuites.</span><span class="sxs-lookup"><span data-stu-id="1a36b-442">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) Received a ClientHello with no supported DTLS ciphersuites.</span></span>
- <span data-ttu-id="1a36b-443">**NX_SECURE_TLS_BAD_COMPRESSION_METHOD** (0X118) recevied un ClientHello con un metodo di compressione sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-443">**NX_SECURE_TLS_BAD_COMPRESSION_METHOD** (0x118) Recevied a ClientHello with a unknown compression method.</span></span>
- <span data-ttu-id="1a36b-444">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) errore di handshake generico (non specificato), in genere a causa di problemi relativi all'elaborazione delle estensioni.</span><span class="sxs-lookup"><span data-stu-id="1a36b-444">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) Generic (unspecified) handshake failure, usually due to problems with extension processing.</span></span>
- <span data-ttu-id="1a36b-445">**NX_SECURE_TLS_UNSUPPORTED_FEATURE** (0X130) una funzionalità non ancora supportata è stata richiamata durante l'handshake DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-445">**NX_SECURE_TLS_UNSUPPORTED_FEATURE** (0x130) A feature that is not yet supported was invoked during the DTLS handshake.</span></span>
- <span data-ttu-id="1a36b-446">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) è stato rilevato un CIPHERSUITE sconosciuto (errore di crittografia interno indicato).</span><span class="sxs-lookup"><span data-stu-id="1a36b-446">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) An unknown ciphersuite was encountered (indicated internal cryptography error).</span></span>
- <span data-ttu-id="1a36b-447">**NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0X12E) recevied un record DTLS con una versione di DTLS non corrispondente.</span><span class="sxs-lookup"><span data-stu-id="1a36b-447">**NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0x12E) Recevied a DTLS record with a mismatched DTLS version.</span></span>
- <span data-ttu-id="1a36b-448">**NX_SECURE_TLS_FINISHED_HASH_FAILURE** (0X115) non è riuscito a convalidare l'hash di handshake DTLS, la sessione non è valida.</span><span class="sxs-lookup"><span data-stu-id="1a36b-448">**NX_SECURE_TLS_FINISHED_HASH_FAILURE** (0x115) Failed to validate the DTLS handshake hash, session is invalid.</span></span>
- <span data-ttu-id="1a36b-449">Invio di UDP interno **NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) non riuscito.</span><span class="sxs-lookup"><span data-stu-id="1a36b-449">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Internal UDP send failed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-450">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-450">Allowed From</span></span>

<span data-ttu-id="1a36b-451">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-451">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-452">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-452">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
* DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
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

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT, NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table, crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer), packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len, NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                    &certificate, 1);

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
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                        NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                    &packet_pool, &send_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                                                                send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* Server processing is done,
    stop the server instance from accepting requests. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-453">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-453">See Also</span></span>

- <span data-ttu-id="1a36b-454">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span><span class="sxs-lookup"><span data-stu-id="1a36b-454">nx_secure_dtls_server_start, nx_secure_dtls_server_delete,</span></span>
- <span data-ttu-id="1a36b-455">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="1a36b-455">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="1a36b-456">nx_secure_dtls_server_session_create, nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="1a36b-456">nx_secure_dtls_server_session_create, nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="1a36b-457">nx_secure_dtls_server_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-457">nx_secure_dtls_server_local_certificate_add</span></span>

## <a name="nx_secure_dtls_server_start"></a><span data-ttu-id="1a36b-458">nx_secure_dtls_server_start</span><span class="sxs-lookup"><span data-stu-id="1a36b-458">nx_secure_dtls_server_start</span></span>

<span data-ttu-id="1a36b-459">Avviare un'istanza del server NetX Secure DTLS in ascolto sulla porta UDP configurata</span><span class="sxs-lookup"><span data-stu-id="1a36b-459">Start a NetX Secure DTLS Server instance listening on the configured UDP port</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-460">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-460">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_start(
                  NX_SECURE_DTLS_SERVER *server_ptr);

```

### <a name="description"></a><span data-ttu-id="1a36b-461">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-461">Description</span></span>

<span data-ttu-id="1a36b-462">Questo servizio avvia un server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-462">This service starts a DTLS Server.</span></span> <span data-ttu-id="1a36b-463">Al termine della chiamata, il server è attivo e inizierà a elaborare le richieste in ingresso dai client di DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-463">After the call returns, the server is active and will begin processing incoming requests from DTLS clients.</span></span> <span data-ttu-id="1a36b-464">L'istanza del server deve essere stata configurata con l' *nx_secure_dtls_server_create* del servizio.</span><span class="sxs-lookup"><span data-stu-id="1a36b-464">The server instance must have been configured with the service *nx_secure_dtls_server_create*.</span></span>

> [!NOTE]
> <span data-ttu-id="1a36b-465">Questo servizio associa la porta UDP interna del server DTLS alla porta locale configurata in modo che la maggior parte dei problemi rilevati sarà eseguita con le comunicazioni UDP e la configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="1a36b-465">This service binds the internal DTLS Server UDP port to the configured local port so most issues encountered will have to do with UDP communications and network configuration.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-466">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-466">Parameters</span></span>

- <span data-ttu-id="1a36b-467">**server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-467">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-468">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-468">Return Values</span></span>

- <span data-ttu-id="1a36b-469">Inizio del server **NX_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="1a36b-469">**NX_SUCCESS** (0x00) Successful start of server.</span></span>
- <span data-ttu-id="1a36b-470">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-470">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-471">UDP **NX_NOT_ENABLED** (0x14) non abilitato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-471">**NX_NOT_ENABLED** (0x14) UDP not enabled.</span></span>
- <span data-ttu-id="1a36b-472">**NX_NO_FREE_PORTS** (0X45) senza porte UDP disponibili.</span><span class="sxs-lookup"><span data-stu-id="1a36b-472">**NX_NO_FREE_PORTS** (0x45) No available UDP ports.</span></span>
- <span data-ttu-id="1a36b-473">**NX_INVALID_PORT** (0x46) porta UDP non valida.</span><span class="sxs-lookup"><span data-stu-id="1a36b-473">**NX_INVALID_PORT** (0x46) Invalid UDP port.</span></span>
- <span data-ttu-id="1a36b-474">La porta UDP **NX_ALREADY_BOUND** (0x22) è già associata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-474">**NX_ALREADY_BOUND** (0x22) UDP port already bound.</span></span>
- <span data-ttu-id="1a36b-475">La porta UDP **NX_PORT_UNAVAILABLE** (0x23) non è disponibile per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="1a36b-475">**NX_PORT_UNAVAILABLE** (0x23) UDP port not available for use.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-476">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-476">Allowed From</span></span>

<span data-ttu-id="1a36b-477">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-477">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-478">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-478">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
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

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);

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

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                        &receive_packet,
                                                        NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session, &packet_pool,
                &send_packet, NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
                (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);
        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-479">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-479">See Also</span></span>

- <span data-ttu-id="1a36b-480">nx_secure_dtls_server_stop, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-480">nx_secure_dtls_server_stop, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="1a36b-481">nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-481">nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-482">nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="1a36b-482">nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="1a36b-483">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="1a36b-483">nx_secure_dtls_server_session_start</span></span>

## <a name="nx_secure_dtls_server_stop"></a><span data-ttu-id="1a36b-484">nx_secure_dtls_server_stop</span><span class="sxs-lookup"><span data-stu-id="1a36b-484">nx_secure_dtls_server_stop</span></span>

<span data-ttu-id="1a36b-485">Arrestare un'istanza del server DTLS Active NetX Secure</span><span class="sxs-lookup"><span data-stu-id="1a36b-485">Stop an active NetX Secure DTLS Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-486">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-486">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_stop(NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a><span data-ttu-id="1a36b-487">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-487">Description</span></span>

<span data-ttu-id="1a36b-488">Questo servizio interrompe l'ascolto da parte di un server DTLS sulla porta UDP configure e Reimposta tutte le sessioni DTLS associate, bloccando le comunicazioni DTLS in corso.</span><span class="sxs-lookup"><span data-stu-id="1a36b-488">This service stops a DTLS Server from listening on the configure UDP port and resets all the associated DTLS sessions, halting any in-progress DTLS communications.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-489">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-489">Parameters</span></span>

- <span data-ttu-id="1a36b-490">**server_ptr** Puntatore a un'istanza del server DTLS attiva.</span><span class="sxs-lookup"><span data-stu-id="1a36b-490">**server_ptr** Pointer to an active DTLS Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-491">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-491">Return Values</span></span>

- <span data-ttu-id="1a36b-492">L'arresto del server **NX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="1a36b-492">**NX_SUCCESS** (0x00) Successful stop of server.</span></span>
- <span data-ttu-id="1a36b-493">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-493">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-494">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-494">Allowed From</span></span>

<span data-ttu-id="1a36b-495">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-495">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-496">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-496">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array or list in case a new connection is
         attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
   NOTE: Should be an array or list as
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

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate, device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);


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

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);

        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* We have exited the processing loop, stop the server. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-497">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-497">See Also</span></span>

- <span data-ttu-id="1a36b-498">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-498">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="1a36b-499">nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-499">nx_secure_dtls_server_delete, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-500">nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="1a36b-500">nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="1a36b-501">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="1a36b-501">nx_secure_dtls_server_session_start</span></span>

## <a name="nx_secure_dtls_server_trusted_certificate_add"></a><span data-ttu-id="1a36b-502">nx_secure_dtls_server_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-502">nx_secure_dtls_server_trusted_certificate_add</span></span>

<span data-ttu-id="1a36b-503">Aggiungere un certificato CA attendibile a un server NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-503">Add a trusted CA certificate to a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-504">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-504">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_trusted_certificate_add(
                                         NX_SECURE_DTLS_SERVER *server_ptr,
                                         NX_SECURE_X509_CERT *certificate,
                                         UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="1a36b-505">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-505">Description</span></span>

<span data-ttu-id="1a36b-506">Questo servizio aggiunge una CA attendibile o un certificato CA intermedio a un'istanza del server DTLS e assegnata a tutte le sessioni del server DTLS interno.</span><span class="sxs-lookup"><span data-stu-id="1a36b-506">This service adds a trusted CA or intermediate CA certificate to a DTLS Server instance and assigned to all the internal DTLS server sessions.</span></span> <span data-ttu-id="1a36b-507">Questa operazione è necessaria solo se l'autenticazione del certificato client X. 509 è abilitata usando *nx_secure_dtls_server_x509_client_verify_configure*.</span><span class="sxs-lookup"><span data-stu-id="1a36b-507">This is only necessary if X.509 Client certificate authentication is enabled using *nx_secure_dtls_server_x509_client_verify_configure*.</span></span> <span data-ttu-id="1a36b-508">Il certificato aggiunto verrà usato per verificare i certificati X. 509 client in ingresso.</span><span class="sxs-lookup"><span data-stu-id="1a36b-508">The added certificate will be used to verify incoming Client X.509 certificates.</span></span>

<span data-ttu-id="1a36b-509">Il parametro cert_id è un identificatore numerico diverso da zero per il certificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-509">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="1a36b-510">In questo modo il certificato viene facilmente rimosso o trovato nel caso in cui siano presenti più certificati di identità con lo stesso nome comune X. 509 presente nell'archivio del server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-510">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS server store.</span></span> <span data-ttu-id="1a36b-511">Per ulteriori informazioni sui certificati del server X. 509, vedere la guida dell'utente di NetX Secure TLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-511">See the NetX Secure TLS User Guide for more information about X.509 server certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-512">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-512">Parameters</span></span>

- <span data-ttu-id="1a36b-513">**server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-513">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="1a36b-514">**certificato** di Puntatore a una struttura di certificato X. 509 inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-514">**certificate** Pointer to a previously initialized X.509 certificate structure.</span></span>
- <span data-ttu-id="1a36b-515">**cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-515">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-516">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-516">Return Values</span></span>

- <span data-ttu-id="1a36b-517">**NX_SUCCESS** (0x00) aggiunta del certificato al server DTLS completata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-517">**NX_SUCCESS** (0x00) Successful addition of certificate to DTLS server.</span></span>
- <span data-ttu-id="1a36b-518">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-518">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-519">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) è stato passato un ID certificato 0.</span><span class="sxs-lookup"><span data-stu-id="1a36b-519">**NX_INVALID_PARAMETERS** (0x4D) A certificate ID of 0 was passed in.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-520">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-520">Allowed From</span></span>

<span data-ttu-id="1a36b-521">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-521">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-522">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-522">Example</span></span>

<span data-ttu-id="1a36b-523">\* Per un esempio più completo, vedere informazioni di riferimento per *nx_secure_dtls_server_create* .</span><span class="sxs-lookup"><span data-stu-id="1a36b-523">\*See reference for *nx_secure_dtls_server_create* for a more complete example.</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                LOCAL_SERVER_PORT,
                                NX_IP_PERIODIC_RATE,
                                dtls_server_session_buffer,
                                sizeof(dtls_server_session_buffer),
                                &tls_crypto_table,
                                crypto_metadata_buffer,
                                sizeof(crypto_metadata_buffer),
                                packet_buffer,
                                sizeof(packet_buffer),
                                dtls_server_connect_notify,
                                dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0, NX_NULL,
                                            0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add trusted CA certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                            &trusted_ca_certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Loop continuously to handle incoming data. */
    while(1)
    {
        /* Process incoming requests and data. */
    }

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-524">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-524">See Also</span></span>

- <span data-ttu-id="1a36b-525">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-525">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="1a36b-526">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="1a36b-526">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="1a36b-527">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-527">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="1a36b-528">nx_secure_dtls_server_local_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="1a36b-528">nx_secure_dtls_server_local_certificate_add,</span></span>
- <span data-ttu-id="1a36b-529">nx_secure_dtls_server_trusted_certificate_remove,</span><span class="sxs-lookup"><span data-stu-id="1a36b-529">nx_secure_dtls_server_trusted_certificate_remove,</span></span>
- <span data-ttu-id="1a36b-530">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1a36b-530">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_server_trusted_certificate_remove"></a><span data-ttu-id="1a36b-531">nx_secure_dtls_server_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1a36b-531">nx_secure_dtls_server_trusted_certificate_remove</span></span>

<span data-ttu-id="1a36b-532">Rimuovere un certificato CA attendibile da un server NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-532">Remove a trusted CA certificate from a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-533">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-533">Prototype</span></span>

```C
UINT  nx_secure_dtls_server_trusted_certificate_remove(
                                NX_SECURE_DTLS_SERVER *server_ptr,
                                UCHAR *common_name,
                                UINT common_name_length,
                                UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="1a36b-534">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-534">Description</span></span>

<span data-ttu-id="1a36b-535">Questo servizio rimuove un certificato CA attendibile da un'istanza del server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-535">This service removes a trusted CA certificate from a DTLS Server instance.</span></span> <span data-ttu-id="1a36b-536">I certificati CA attendibili sono necessari solo per un server DTLS per cui è stata abilitata la verifica del certificato client X. 509 chiamando *nx_secure_dtls_server_x509_client_verify_configure*.</span><span class="sxs-lookup"><span data-stu-id="1a36b-536">Trusted CA certificates are only necessary for a DTLS Server for which X.509 Client certificate verification has been enabled by calling *nx_secure_dtls_server_x509_client_verify_configure*.</span></span>

<span data-ttu-id="1a36b-537">Il certificato da rimuovere può essere identificato dal nome comune X. 509 o dal cert_id numerico assegnato nella chiamata a *nx_secure_dtls_server_trusted_certificate_add*.</span><span class="sxs-lookup"><span data-stu-id="1a36b-537">The certificate to be removed can be identified either by its X.509 Common Name or by the numeric cert_id that was assigned in the call to *nx_secure_dtls_server_trusted_certificate_add*.</span></span> <span data-ttu-id="1a36b-538">Il cert_id viene usato solo per identificare il certificato ed è gestito dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-538">The cert_id is only used to identify the certificate and is maintained by the application.</span></span> <span data-ttu-id="1a36b-539">Se viene usato il nome comune anziché l'identificatore numerico del certificato, il parametro cert_id deve essere impostato su 0.</span><span class="sxs-lookup"><span data-stu-id="1a36b-539">If the Common Name is used instead of the numeric certificate identifier, the cert_id parameter should be set to 0.</span></span>

> [!NOTE]
> <span data-ttu-id="1a36b-540">La rimozione di un certificato mentre è in corso l'elaborazione di un handshake DTLS può causare un comportamento imprevisto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-540">Removing a certificate while a DTLS handshake is being processed may result in unexpected behavior.</span></span> <span data-ttu-id="1a36b-541">Il *nx_secure_dtls_server_stop* del servizio deve essere chiamato prima di rimuovere i certificati.</span><span class="sxs-lookup"><span data-stu-id="1a36b-541">The service *nx_secure_dtls_server_stop* should be called before removing certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-542">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-542">Parameters</span></span>

- <span data-ttu-id="1a36b-543">**server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-543">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="1a36b-544">**common_name** X. 509 CommonName del certificato da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="1a36b-544">**common_name** X.509 CommonName of the certificate to remove.</span></span> <span data-ttu-id="1a36b-545">Se viene usato, passare cert_id come zero.</span><span class="sxs-lookup"><span data-stu-id="1a36b-545">If this is used, pass cert_id as zero.</span></span>
- <span data-ttu-id="1a36b-546">**common_name_length** Lunghezza di common_name stringa in byte.</span><span class="sxs-lookup"><span data-stu-id="1a36b-546">**common_name_length** Length of common_name string in bytes.</span></span>
- <span data-ttu-id="1a36b-547">**cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-547">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span> <span data-ttu-id="1a36b-548">Se si utilizza questa proprietà, passare NX_NULL per il parametro common_name.</span><span class="sxs-lookup"><span data-stu-id="1a36b-548">If this is used, pass NX_NULL for the common_name parameter.</span></span>


### <a name="return-values"></a><span data-ttu-id="1a36b-549">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-549">Return Values</span></span>

- <span data-ttu-id="1a36b-550">**NX_SUCCESS** (0x00) la rimozione del certificato dal server DTLS è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-550">**NX_SUCCESS** (0x00) Successful removal of certificate from DTLS server.</span></span>
- <span data-ttu-id="1a36b-551">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-551">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-552">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0X119) non è stato trovato alcun certificato corrispondente al cert_id o common_name nel server DTLS specificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-552">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate matching the cert_id or common_name was found in the given DTLS server.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-553">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-553">Allowed From</span></span>

<span data-ttu-id="1a36b-554">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-554">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-555">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-555">Example</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                                    certificate_der_data,
                                                    sizeof(certificate_der_data),
                                                    NX_NULL, 0, NX_NULL, 0,
                                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                                       &trusted_ca_certificate, 1);

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before removing a certificate. */
    Status = nx_secure_dtls_server_stop(&dtls_server);


/* At some point in the future we decide to remove the certificate we added. We can
       use the certificate identifier we passed into the call to
       nx_secure_dtls_trusted_certificate_add (value = 1); */
    status = nx_secure_dtls_server_trusted_certificate_remove(&dtls_server,
                                                          NX_NULL, 0, 1);

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-556">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-556">See Also</span></span>

- <span data-ttu-id="1a36b-557">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-557">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="1a36b-558">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-558">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="1a36b-559">nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="1a36b-559">nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="1a36b-560">nx_secure_dtls_server_trusted_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="1a36b-560">nx_secure_dtls_server_trusted_certificate_add,</span></span>
- <span data-ttu-id="1a36b-561">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1a36b-561">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_server_x509_client_verify_configure"></a><span data-ttu-id="1a36b-562">nx_secure_dtls_server_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="1a36b-562">nx_secure_dtls_server_x509_client_verify_configure</span></span>

<span data-ttu-id="1a36b-563">Configurare un server NetX Secure DTLS per richiedere e verificare i certificati client</span><span class="sxs-lookup"><span data-stu-id="1a36b-563">Configure a NetX Secure DTLS Server to request and verify client certificates</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-564">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-564">Prototype</span></span>

```C
UINT nx_secure_dtls_server_x509_client_verify_configure(
                           NX_SECURE_DTLS_SERVER *server_ptr,
                               UINT certs_per_session,
                               UCHAR *certs_buffer, ULONG buffer_size);

```

### <a name="description"></a><span data-ttu-id="1a36b-565">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-565">Description</span></span>

<span data-ttu-id="1a36b-566">Questo servizio configura un server DTLS per richiedere e verificare i certificati client DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-566">This service configures a DTLS Server to request and verify DTLS Client certificates.</span></span> <span data-ttu-id="1a36b-567">Questa funzionalità facoltativa viene usata quando si desiderano certificati X. 509 per l'autenticazione client al posto di altri meccanismi, ad esempio una chiave precondivisa.</span><span class="sxs-lookup"><span data-stu-id="1a36b-567">This optional feature is used when X.509 certificates are desired for client authentication in place of other mechanisms (e.g. a Pre-Shared Key).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a36b-568">*Quando un server DTLS è configurato per verificare i certificati client con questo servizio, è necessario aggiungere almeno un certificato CA attendibile al server utilizzando nx_secure_dtls_server_trusted_certificate_add o il server rifiuterà tutte le connessioni client in ingresso perché non sarà in grado di verificare i certificati client rispetto all'archivio attendibile.*</span><span class="sxs-lookup"><span data-stu-id="1a36b-568">*When a DTLS Server is configured to verify client certificates using this service, at least one trusted CA certificate must be added to the server using nx_secure_dtls_server_trusted_certificate_add or the server will reject all incoming client connections because it will be unable to verify client certificates against the trusted store.*</span></span>

<span data-ttu-id="1a36b-569">Quando si chiama questo servizio, l'istanza del server DTLS (una volta avviata) richiede i certificati client come parte dell'handshake DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-569">Upon calling this service, the DTLS Server instance will (once started) request client certificates as part of the DTLS handshake.</span></span> <span data-ttu-id="1a36b-570">Supponendo che il client sia configurato correttamente con un certificato di identità (e una catena di certificati associata quando applicabile), il server DTLS richiede l'allocazione della memoria per elaborare i dati del certificato client.</span><span class="sxs-lookup"><span data-stu-id="1a36b-570">Assuming the client is properly configured with an identity certificate (and associated certificate chain when applicable), the DTLS Server requires memory to be allocated to process the client certificate data.</span></span> <span data-ttu-id="1a36b-571">Questa memoria viene passata come parametro *certs_buffer* .</span><span class="sxs-lookup"><span data-stu-id="1a36b-571">This memory is passed in as the *certs_buffer* parameter.</span></span>

<span data-ttu-id="1a36b-572">Il certs_buffer deve essere dimensionato per supportare la catena di certificati più grande prevista da un client DTLS, per *il numero di sessioni del server DTLS*.</span><span class="sxs-lookup"><span data-stu-id="1a36b-572">The certs_buffer must be sized to accommodate the largest expected certificate chain from a DTLS client, *times the number of DTLS server sessions*.</span></span> <span data-ttu-id="1a36b-573">Il buffer è diviso tra le sessioni disponibili usando il parametro *certs_per_session* che rappresenta il numero massimo previsto di certificati in una catena di certificati client.</span><span class="sxs-lookup"><span data-stu-id="1a36b-573">The buffer is divided amongst the available sessions using the *certs_per_session* parameter which represents the maximum expected number of certificates in a Client certificate chain.</span></span> <span data-ttu-id="1a36b-574">Il buffer deve inoltre fornire spazio per la struttura dei dati NX_SECURE_X509_CERT utilizzata per analizzare i dati del certificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-574">The buffer also needs to provide space for the NX_SECURE_X509_CERT data structure which is used to parse the certificate data.</span></span>

<span data-ttu-id="1a36b-575">Il calcolo delle dimensioni del buffer appropriate può essere eseguito con la formula seguente:</span><span class="sxs-lookup"><span data-stu-id="1a36b-575">Calculating the proper buffer size can be done with the following formula:</span></span>

```C
buffer_size = (# of DTLS sessions in server) *
                (certs_per_session) *
                (    maximum expected certificate size +
                      sizeof(NX_SECURE_X509_CERT)    )

```

- <span data-ttu-id="1a36b-576">Il numero di sessioni DTLS è determinato dalla dimensione del buffer di sessione passato in nx_secure_dtls_server_create.</span><span class="sxs-lookup"><span data-stu-id="1a36b-576">The number of DTLS sessions is determined by the size of the session buffer passed into nx_secure_dtls_server_create.</span></span>
- <span data-ttu-id="1a36b-577">certs_per_session deve essere impostato sul numero massimo di certificati previsto in qualsiasi catena di certificati client.</span><span class="sxs-lookup"><span data-stu-id="1a36b-577">certs_per_session should be set to the maximum expected number of certificates in any client certificate chain.</span></span>
- <span data-ttu-id="1a36b-578">Le dimensioni massime del certificato previste dipendono dall'applicazione, dalle dimensioni delle chiavi e da altri fattori, ma 2 KB è in genere sufficiente.</span><span class="sxs-lookup"><span data-stu-id="1a36b-578">The maximum expected certificate size is dependent on the application, key sizes, and other factors but 2KB is generally sufficient.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-579">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-579">Parameters</span></span>

- <span data-ttu-id="1a36b-580">**server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-580">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>
- <span data-ttu-id="1a36b-581">**certs_per_session** Numero di certificati da allocare a ogni sessione del server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-581">**certs_per_session** Number of certificates to allocate to each DTLS server session.</span></span>
- <span data-ttu-id="1a36b-582">**certs_buffer** Spazio del buffer per i dati del certificato in ingresso.</span><span class="sxs-lookup"><span data-stu-id="1a36b-582">**certs_buffer** Buffer space for incoming certificate data.</span></span>
- <span data-ttu-id="1a36b-583">**BUFFER_SIZE** Dimensioni del buffer del certificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-583">**buffer_size** Size of the certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-584">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-584">Return Values</span></span>

- <span data-ttu-id="1a36b-585">**NX_SUCCESS** (0x00) configurazione corretta della verifica del client X. 509.</span><span class="sxs-lookup"><span data-stu-id="1a36b-585">**NX_SUCCESS** (0x00) Successful configuration of X.509 Client verification.</span></span>
- <span data-ttu-id="1a36b-586">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-586">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-587">L'archivio certificati **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non è valido (l'istanza DTLSserver non è stata initale?).</span><span class="sxs-lookup"><span data-stu-id="1a36b-587">**NX_INVALID_PARAMETERS** (0x4D) Invalid certificate store (DTLSserver instance not initalized?).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-588">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-588">Allowed From</span></span>

<span data-ttu-id="1a36b-589">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-589">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-590">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-590">Example</span></span>

```C
/* Configure number of sessions per server. */
#define DTLS_SERVER_SESSIONS 3

/* Define parameters for X.509 client verification. */
#define MAX_CERT_SIZE         (2000)       /* 2KB expected maximum certificate size. */
#define CERTS_PER_SESSION (3)            /* Assume maximum chain length of 3 certificates. */
#define CERT_BUFFER_SIZE     (DTLS_SERVER_SESSIONS * CERTS_PER_SESSION * \
 (MAX_CERT_SIZE + sizeof(NX_SECURE_X509_CERT))

/* Define our incoming certificate buffer. */
UCHAR client_certs_buffer[CERT_BUFFER_SIZE];

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                    certificate_der_data,
                                    sizeof(certificate_der_data),
                                    NX_NULL, 0,
                                    NX_NULL, 0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                                &trusted_ca_certificate, 1);

    /* Configure client X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_configure(&dtls_server,
        CERTS_PER_SESSION,
        client_certs_buffer,
        sizeof(client_certs_buffer));

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-591">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-591">See Also</span></span>

- <span data-ttu-id="1a36b-592">nx_secure_dtls_server_x509_client_verify_disable,</span><span class="sxs-lookup"><span data-stu-id="1a36b-592">nx_secure_dtls_server_x509_client_verify_disable,</span></span>
- <span data-ttu-id="1a36b-593">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-593">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="1a36b-594">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-594">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="1a36b-595">nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="1a36b-595">nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="1a36b-596">nx_secure_dtls_server_trusted_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="1a36b-596">nx_secure_dtls_server_trusted_certificate_add,</span></span>
- <span data-ttu-id="1a36b-597">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1a36b-597">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_server_x509_client_verify_disable"></a><span data-ttu-id="1a36b-598">nx_secure_dtls_server_x509_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="1a36b-598">nx_secure_dtls_server_x509_client_verify_disable</span></span>

<span data-ttu-id="1a36b-599">Disabilita la verifica del certificato X. 509 client per un server DTLS protetto NetX</span><span class="sxs-lookup"><span data-stu-id="1a36b-599">Disables client X.509 certificate verification for a NetX Secure DTLS Server</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-600">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-600">Prototype</span></span>

```C
UINT nx_secure_dtls_server_x509_client_verify_disable(
                           NX_SECURE_DTLS_SERVER *server_ptr);
```

### <a name="description"></a><span data-ttu-id="1a36b-601">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-601">Description</span></span>

<span data-ttu-id="1a36b-602">Questo servizio Disabilita la verifica del certificato client X. 509 in un server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-602">This service disables X.509 Client certificate verification on a DTLS Server.</span></span> <span data-ttu-id="1a36b-603">Il servizio non ha alcun effetto se la verifica del certificato client X. 509 non è abilitata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-603">The service has no effect if X.509 Client certificate verification is not enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="1a36b-604">La disabilitazione dell'autenticazione client in un'istanza del server DTLS attiva può causare un comportamento imprevedibile.</span><span class="sxs-lookup"><span data-stu-id="1a36b-604">Disabling client authentication on an active DTLS Server instance may result in unpredictable behavior.</span></span> <span data-ttu-id="1a36b-605">Il servizio di nx_secure_dtls_server_stop deve essere chiamato prima di modificare lo stato del server.</span><span class="sxs-lookup"><span data-stu-id="1a36b-605">The nx_secure_dtls_server_stop service should be called before changing server state.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-606">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-606">Parameters</span></span>

- <span data-ttu-id="1a36b-607">**server_ptr** Puntatore a un'istanza del server DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-607">**server_ptr** Pointer to a previously created DTLS Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-608">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-608">Return Values</span></span>

- <span data-ttu-id="1a36b-609">**NX_SUCCESS** (0x00) la disabilitazione dell'autenticazione client X. 509 è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-609">**NX_SUCCESS** (0x00) Successful disabling of X.509 client authentication.</span></span>
- <span data-ttu-id="1a36b-610">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-610">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-611">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-611">Allowed From</span></span>

<span data-ttu-id="1a36b-612">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-612">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-613">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-613">Example</span></span>

```C
/* Configure number of sessions per server. */
#define DTLS_SERVER_SESSIONS 3

/* Define parameters for X.509 client verification. */
#define MAX_CERT_SIZE         (2000)       /* 2KB expected maximum certificate size. */
#define CERTS_PER_SESSION (3)            /* Assume maximum chain length of 3 certificates. */
#define CERT_BUFFER_SIZE     (DTLS_SERVER_SESSIONS * CERTS_PER_SESSION * \
 (MAX_CERT_SIZE + sizeof(NX_SECURE_X509_CERT))

/* Define our incoming certificate buffer. */
UCHAR client_certs_buffer[CERT_BUFFER_SIZE];

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Certificate control block and data. */
NX_SECURE_X509_CERT trusted_ca_certificate;
UCHAR certificate_der_data[] = { … };

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                    LOCAL_SERVER_PORT,
                                    NX_IP_PERIODIC_RATE,
                                    dtls_server_session_buffer,
                                    sizeof(dtls_server_session_buffer),
                                    &tls_crypto_table,
                                    crypto_metadata_buffer,
                                    sizeof(crypto_metadata_buffer),
                                    packet_buffer,
                                    sizeof(packet_buffer),
                                    dtls_server_connect_notify,
                                    dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize trusted certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&trusted_ca_certificate,
                                    certificate_der_data,
                        sizeof(certificate_der_data), NX_NULL, 0,
                        NX_NULL, 0, NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_trusted_certificate_add(&dtls_server,
                                            &trusted_ca_certificate, 1);

    /* Configure client X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_configure(&dtls_server,
        CERTS_PER_SESSION,
        client_certs_buffer,
        sizeof(client_certs_buffer));

    /* Start server. */
    status = nx_secure_dtls_server_start(&dtls_server);

    /* Process client requests, etc… */

    /* Stop the server before changing state. */
    status = nx_secure_dtls_server_stop(&dtls_server);

    /* Disable X.509 authentication and verification. */
    status = nx_secure_dtls_server_x509_client_verify_disable(&dtls_server);

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-614">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-614">See Also</span></span>

- <span data-ttu-id="1a36b-615">nx_secure_dtls_server_x509_client_verify_configure,</span><span class="sxs-lookup"><span data-stu-id="1a36b-615">nx_secure_dtls_server_x509_client_verify_configure,</span></span>
- <span data-ttu-id="1a36b-616">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span><span class="sxs-lookup"><span data-stu-id="1a36b-616">nx_secure_dtls_server_start, nx_secure_dtls_server_create,</span></span>
- <span data-ttu-id="1a36b-617">nx_secure_dtls_server_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-617">nx_secure_dtls_server_session_start,</span></span>
- <span data-ttu-id="1a36b-618">nx_secure_dtls_server_session_stop,</span><span class="sxs-lookup"><span data-stu-id="1a36b-618">nx_secure_dtls_server_session_stop,</span></span>
- <span data-ttu-id="1a36b-619">nx_secure_dtls_server_trusted_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="1a36b-619">nx_secure_dtls_server_trusted_certificate_add,</span></span>
- <span data-ttu-id="1a36b-620">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1a36b-620">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_session_client_info_get"></a><span data-ttu-id="1a36b-621">nx_secure_dtls_session_client_info_get</span><span class="sxs-lookup"><span data-stu-id="1a36b-621">nx_secure_dtls_session_client_info_get</span></span>

<span data-ttu-id="1a36b-622">Ottenere informazioni client Remote da una sessione del server DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-622">Get remote client information from a DTLS Server session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-623">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-623">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_client_info_get(
                                    NX_SECURE_DTLS_SESSION *session_ptr,
                                    NXD_ADDRESS *client_ip_address,
                                    UINT *client_port, UINT *local_port);

```

### <a name="description"></a><span data-ttu-id="1a36b-624">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-624">Description</span></span>

<span data-ttu-id="1a36b-625">Questo servizio restituisce le informazioni di rete relative a un client DTLS connesso a una determinata sessione del server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-625">This service returns the network information about a DTLS Client that is connected to a particular DTLS Server session.</span></span> <span data-ttu-id="1a36b-626">Le informazioni restituite sono costituite dall'indirizzo IP e dalla porta UDP del client remoto, nonché dalla porta locale del server a cui è connesso il client.</span><span class="sxs-lookup"><span data-stu-id="1a36b-626">The information returned consists of the remote client’s IP address and UDP port, as well as the local server port to which the client is connected.</span></span>

<span data-ttu-id="1a36b-627">In generale, l'istanza della sessione DTLS sarà quella ottenuta nella chiamata di una delle routine di callback di notifica DTLS (ad esempio, il connect_notify o receive_notify i callback passati in nx_secure_dtls_server_create).</span><span class="sxs-lookup"><span data-stu-id="1a36b-627">In general, the DTLS session instance will be the one obtained in the invocation of one of the DTLS notification callback routines (e.g. the connect_notify or receive_notify callbacks passed into nx_secure_dtls_server_create).</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-628">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-628">Parameters</span></span>

- <span data-ttu-id="1a36b-629">**session_ptr** Puntatore a un'istanza di sessione del server DTLS attiva.</span><span class="sxs-lookup"><span data-stu-id="1a36b-629">**session_ptr** Pointer to an active DTLS server session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-630">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-630">Return Values</span></span>

- <span data-ttu-id="1a36b-631">L'eliminazione del server è riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="1a36b-631">**NX_SUCCESS** (0x00) Successful deletion of server.</span></span>
- <span data-ttu-id="1a36b-632">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-632">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-633">**NX_INVALID_SOCKET** (0X13) il socket UDP associato non è valido (sessione non inizializzata?).</span><span class="sxs-lookup"><span data-stu-id="1a36b-633">**NX_INVALID_SOCKET** (0x13) The associated UDP socket is not valid (session not initialized?).</span></span>
- <span data-ttu-id="1a36b-634">Il socket UDP **NX_NOT_CONNECTED** (0x38) non è connesso: la connessione client è stata eliminata o non è ancora stata stabilita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-634">**NX_NOT_CONNECTED** (0x38) UDP socket is not connected – client connection dropped or not yet established.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-635">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-635">Allowed From</span></span>

<span data-ttu-id="1a36b-636">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-636">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-637">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-637">Example</span></span>

```C
#define DTLS_SERVER_SESSION (3)

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SERVER dtls_server;

/* Allocate space for DTLS sessions in the DTLS server. */
UCHAR dtls_server_session_buffer[sizeof(NX_SECURE_DTLS_SESSION)
                                        * DTLS_SERVER_SESSIONS];

/* Flag used to indicate that a DTLS Client has connected. */
UINT connect_flag = 0;

/* Flag used to indicate application data reception. */
UINT receive_flag = 0;

/* Pointer to newly-connected DTLS session.
   NOTE: In practice this should be an array
   or list in case a new connection is
   attempted while a previous session is being started. */
NX_SECURE_DTLS_SESSION *new_dtls_session;

/* Pointer to session for application data receive.
NOTE: Should be an array or list as
   with new_dtls_session */
NX_SECURE_DTLS_SESSION *receive_dtls_session;

/* Connect notify callback routine. */
UINT dtls_server_connect_notify(NX_SECURE_DTLS_SESSION *dtls_session, NXD_ADDRESS
                                                            *ip_address, UINT port)
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
    NXD_ADDRESS client_ip;
    UINT client_port, server_port;

    /* Get DTLS client information which can be used in filtering or associating
       the DTLS session with application data (e.g. a session pointer table). */
    status = nx_secure_dtls_session_client_info_get(dtls_session, &client_ip,
   &client_port, &server_port);

    /* Receive and process DTLS record.
       NOTE: Mutex handling omitted for clarity. */
    receive_flag = 1;
    receive_dtls_session = dtls_session;

    return(NX_SUCCESS);
}

/* Primary application thread for handling DTLS server operations. */
void dtls_server_thread(void)
{
    NX_PACKET *send_packet;
    NX_PACKET *receive_packet;
    UINT status;

    /* Setup DTLS Server instance. */
    status = nx_secure_dtls_server_create(&dtls_server, &ip_instance,
                                            LOCAL_SERVER_PORT,
                                            NX_IP_PERIODIC_RATE,
                                            dtls_server_session_buffer,
                                            sizeof(dtls_server_session_buffer),
                                            &tls_crypto_table,
                                            crypto_metadata_buffer,
                                            sizeof(crypto_metadata_buffer),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            dtls_server_connect_notify,
                                            dtls_server_receive_notify);

    /* Check for errors. */

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            device_cert_der,
                                            device_cert_der_len,
                                            NX_NULL, 0,
                                            device_cert_key_der,
                                            device_cert_key_der_len,
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_server_local_certificate_add(&dtls_server,
                                                        &certificate, 1);


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

            /* Check for errors. */
        }

        /* Check for received application data. */
        if(receive_flag)
        {
            /* We have received data over a previously-established DTLS session.
               Mutex handling omitted for clarity. */
            Status = nx_secure_dtls_session_receive(receive_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

            /* Process received data… */

            /* Prepare and send response to client. */
            status = nx_secure_dtls_packet_allocate(receive_dtls_session,
                                                &packet_pool,
                                                &send_packet,
                                                NX_IP_PERIODIC_RATE);

            /* Check for errors and prepare response data
            (e.g. nx_packet_data_append). */

            /* Send response to client. */
            status = nx_secure_dtls_server_session_send(receive_dtls_session,
                send_packet);
        }

        /* If not processing connections or received data, let the thread sleep. */
        if(!connect_flag && !receive_flag)
        {
            tx_thread_sleep(100);
        }
    }

    /* If we exit the processing loop, clean up the server. */
    status = nx_secure_dtls_server_delete(&dtls_server);
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-638">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-638">See Also</span></span>

- <span data-ttu-id="1a36b-639">nx_secure_dtls_server_start, nx_secure_dtls_server_stop,</span><span class="sxs-lookup"><span data-stu-id="1a36b-639">nx_secure_dtls_server_start, nx_secure_dtls_server_stop,</span></span>
- <span data-ttu-id="1a36b-640">nx_secure_dtls_server_create, nx_secure_dtls_server_delete,</span><span class="sxs-lookup"><span data-stu-id="1a36b-640">nx_secure_dtls_server_create, nx_secure_dtls_server_delete,</span></span>
- <span data-ttu-id="1a36b-641">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span><span class="sxs-lookup"><span data-stu-id="1a36b-641">nx_secure_dtls_session_receive, nx_secure_dtls_server_session_send,</span></span>
- <span data-ttu-id="1a36b-642">nx_secure_dtls_server_session_start</span><span class="sxs-lookup"><span data-stu-id="1a36b-642">nx_secure_dtls_server_session_start</span></span>

## <a name="nx_secure_dtls_session_create"></a><span data-ttu-id="1a36b-643">nx_secure_dtls_session_create</span><span class="sxs-lookup"><span data-stu-id="1a36b-643">nx_secure_dtls_session_create</span></span>

<span data-ttu-id="1a36b-644">Creare e configurare una sessione NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-644">Create and configure a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-645">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-645">Prototype</span></span>

```C
UINT nx_secure_dtls_session_create(
                        NX_SECURE_DTLS_SESSION *dtls_session,
                        const NX_SECURE_TLS_CRYPTO *crypto_table,
                        VOID *metadata_buffer, ULONG metadata_size,
                        UCHAR *packet_reassembly_buffer,
                        UINT packet_reassembly_buffer_size,
                        UINT certs_number,
                        UCHAR *remote_certificate_buffer,
                        ULONG remote_certificate_buffer_size));

```

### <a name="description"></a><span data-ttu-id="1a36b-646">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-646">Description</span></span>

<span data-ttu-id="1a36b-647">Questo servizio crea e configura una sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-647">This service creates and configures a DTLS session.</span></span> <span data-ttu-id="1a36b-648">In genere, questa operazione verrà utilizzata per creare sessioni client DTLS mentre le sessioni del server DTLS vengono gestite con il meccanismo server DTLS (vedere *nx_secure_dtls_server_create*), ma potrebbero essere presenti istanze in cui un'applicazione deve creare una singola istanza di sessione del server DTLS autonoma, nel qual caso il servizio può essere utilizzato <sup>7</sup>.</span><span class="sxs-lookup"><span data-stu-id="1a36b-648">Generally, this will be used to create DTLS Client sessions as DTLS Server sessions are managed with the DTLS Server mechanism (see *nx_secure_dtls_server_create*), but there may be instances where an application needs to create a single stand-alone DTLS Server session instance in which case this service may be used<sup>7</sup>.</span></span>

<span data-ttu-id="1a36b-649">I parametri consentono di configurare le informazioni e l'allocazione di memoria necessarie per creare un'istanza di una sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-649">The parameters configure the information and memory allocation needed to instantiate a DTLS session.</span></span> <span data-ttu-id="1a36b-650">Il parametro crypto_table è una tabella TLS contenente tutte le routine di crittografia necessarie per la crittografia e l'autenticazione TLS/DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-650">The crypto_table parameter is a TLS table containing all of the cryptographic routines needed for TLS/DTLS encryption and authentication.</span></span> <span data-ttu-id="1a36b-651">Il metadata_buffer viene usato per la crittografia caclulations (vedere nx_secure_tls_metadata_size_calculate nel manuale dell'utente di NetX Secure TLS) e il packet_reassembly_buffer viene usato per riassemblare i datagrammi UDP in un record DTLS completo per la decrittografia.</span><span class="sxs-lookup"><span data-stu-id="1a36b-651">The metadata_buffer is used for encryption caclulations (see nx_secure_tls_metadata_size_calculate in the NetX Secure TLS User Guide), and the packet_reassembly_buffer is used to reassemble UDP datagrams into a complete DTLS record for decryption.</span></span>

<span data-ttu-id="1a36b-652">I certs_number e remote_certificate_buffer sono necessari per i client DTLS che richiedono spazio per archiviare ed elaborare la catena di certificati del server DTLS in ingresso.</span><span class="sxs-lookup"><span data-stu-id="1a36b-652">The certs_number and remote_certificate_buffer are required for DTLS Clients which need space to store and process the incoming DTLS Server certificate chain.</span></span> <span data-ttu-id="1a36b-653">Il buffer deve essere in grado di contenere le dimensioni massime previste della catena di certificati per qualsiasi server a cui si connetterà.</span><span class="sxs-lookup"><span data-stu-id="1a36b-653">The buffer must be able to accommodate the maximum expected size of the certificate chain for any server to which it will connect.</span></span> <span data-ttu-id="1a36b-654">Il buffer è diviso per il numero di certificati previsti (certs_number parametro) e deve essere sufficientemente grande da contenere una NX_SECURE_X509_CERT struttura per ogni certificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-654">The buffer is divided up by the number of expected certificates (certs_number parameter) and must also be large enough to hold one NX_SECURE_X509_CERT structure per certificate.</span></span> <span data-ttu-id="1a36b-655">È possibile determinare le dimensioni del buffer utilizzando la formula seguente:</span><span class="sxs-lookup"><span data-stu-id="1a36b-655">The buffer size can be determined using the following formula:</span></span>

```C
remote_certificate_buffer_size = (certs_number) *
                 (maximum cert size + sizeof(NX_SECURE_X509_CERT))
```

- <span data-ttu-id="1a36b-656">certs_number è il numero massimo previsto di certificati nella catena di certificati del server</span><span class="sxs-lookup"><span data-stu-id="1a36b-656">certs_number is the expected maximum number of certificates in the server’s certificate chain</span></span>
- <span data-ttu-id="1a36b-657">Le dimensioni massime del certificato dipendono dalle dimensioni delle chiavi usate e dalle informazioni del certificato, ma 2 KB è in genere sufficiente.</span><span class="sxs-lookup"><span data-stu-id="1a36b-657">Maximum certificate size is dependent on the size of keys being used and the information in the certificate, but 2KB is generally sufficient.</span></span>

<span data-ttu-id="1a36b-658">**7** la creazione di sessioni del server DTLS con questa routine non è consigliata e presenta alcune limitazioni.</span><span class="sxs-lookup"><span data-stu-id="1a36b-658">**7** Creating DTLS Server sessions with this routine is not recommended and comes with some limitations.</span></span> <span data-ttu-id="1a36b-659">Il problema principale è che la sessione non gestirà le connessioni client aggiuntive in modo normale. Poiché UDP è senza connessione, un secondo client può inviare legalmente i dati alla porta UDP del server quando una sessione DTLS precedente è ancora attiva, causando la fine della sessione del server con un errore.</span><span class="sxs-lookup"><span data-stu-id="1a36b-659">The primary issue is that the session will not handle additional client connections gracefully – since UDP is connectionless a second client can legally send data to the server’s UDP port when a previous DTLS session is still active which would cause the server session to end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-660">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-660">Parameters</span></span>

- <span data-ttu-id="1a36b-661">**dtls_session** Puntatore a una struttura di sessione DTLS non inizializzata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-661">**dtls_session** Pointer to an uninitialized DTLS Session structure.</span></span>
- <span data-ttu-id="1a36b-662">**crypto_table** Puntatore a una struttura della tabella di crittografia TLS/DTLS utilizzata per tutte le operazioni di crittografia.</span><span class="sxs-lookup"><span data-stu-id="1a36b-662">**crypto_table** Pointer to a TLS/DTLS encryption table structure used for all cryptographic operations.</span></span>
- <span data-ttu-id="1a36b-663">**crypto_metadata_buffer** Spazio del buffer per i calcoli delle operazioni di crittografia e le informazioni sullo stato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-663">**crypto_metadata_buffer** Buffer space for cryptographic operation calculations and state information.</span></span>
- <span data-ttu-id="1a36b-664">**crypto_metadata_size** Dimensioni del buffer dei metadati.</span><span class="sxs-lookup"><span data-stu-id="1a36b-664">**crypto_metadata_size** Size of metadata buffer.</span></span>
- <span data-ttu-id="1a36b-665">**packet_reassembly_buffer** Buffer utilizzato da DTLS per riassemblare i dati UDP nei record DTLS per la decrittografia.</span><span class="sxs-lookup"><span data-stu-id="1a36b-665">**packet_reassembly_buffer** Buffer used by DTLS to reassemble UDP data into DTLS records for decryption.</span></span>
- <span data-ttu-id="1a36b-666">**packet_reassembly_buffer_size** Dimensioni del buffer di riassemblaggio.</span><span class="sxs-lookup"><span data-stu-id="1a36b-666">**packet_reassembly_buffer_size** Size of reassembly buffer.</span></span> <span data-ttu-id="1a36b-667">In genere deve essere maggiore di 16KB, ma può essere minore a seconda dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-667">Generally should be greater than 16KB but may be smaller depending on application.</span></span>
- <span data-ttu-id="1a36b-668">**certs_number** Numero massimo di certificati previsto nella catena di certificati del server remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-668">**certs_number** Maximum expected number of certificates in the remote server’s certificate chain.</span></span>
- <span data-ttu-id="1a36b-669">**remote_certificate_buffer** Spazio del buffer per i dati del certificato in ingresso.</span><span class="sxs-lookup"><span data-stu-id="1a36b-669">**remote_certificate_buffer** Buffer space for incoming certificate data.</span></span>
- <span data-ttu-id="1a36b-670">**remote_certificate_buffer_size** Dimensioni del buffer del certificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-670">**remote_certificate_buffer_size** Size of the certificate buffer.</span></span>


### <a name="return-values"></a><span data-ttu-id="1a36b-671">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-671">Return Values</span></span>

- <span data-ttu-id="1a36b-672">**NX_SUCCESS** (0x00) la creazione della sessione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-672">**NX_SUCCESS** (0x00) Successful creation of session.</span></span>
- <span data-ttu-id="1a36b-673">**NX_PTR_ERROR** (0x07) la sessione o il puntatore del buffer non valido.</span><span class="sxs-lookup"><span data-stu-id="1a36b-673">**NX_PTR_ERROR** (0x07) Invalid session or buffer pointer.</span></span>
- <span data-ttu-id="1a36b-674">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) non è sufficiente spazio del buffer per il riassemblaggio, i certificati o la crittografia dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1a36b-674">**NX_INVALID_PARAMETERS** (0x4D) Not enough buffer space for packet reassembly, certificates, or cryptography.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-675">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-675">Allowed From</span></span>

<span data-ttu-id="1a36b-676">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-676">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-677">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-677">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len,
                                    NX_NULL, 0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
    &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                            &udp_socket, &server_ip,
                                            4443,
                                            NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session,
                                                &send_packet,
                                                &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session,
                                            &receive_packet,
                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-678">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-678">See Also</span></span>

- <span data-ttu-id="1a36b-679">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-679">nx_secure_dtls_client_session_start,nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-680">nx_secure_dtls_session_send</span><span class="sxs-lookup"><span data-stu-id="1a36b-680">nx_secure_dtls_session_send</span></span>

## <a name="nx_secure_dtls_session_delete"></a><span data-ttu-id="1a36b-681">nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1a36b-681">nx_secure_dtls_session_delete</span></span>

<span data-ttu-id="1a36b-682">Liberare le risorse usate da una sessione NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-682">Free up resources used by a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-683">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-683">Prototype</span></span>

```C
UINT nx_secure_dtls_session_delete(
                        NX_SECURE_DTLS_SESSION *dtls_session);

```

### <a name="description"></a><span data-ttu-id="1a36b-684">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-684">Description</span></span>

<span data-ttu-id="1a36b-685">Questo servizio Elimina una sessione DTLS, liberando tutte le risorse allocate al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-685">This service deletes a DTLS session, freeing up any resources that were allocated when it was created.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-686">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-686">Parameters</span></span>

- <span data-ttu-id="1a36b-687">**dtls_session** Puntatore a una struttura di sessione DTLS inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-687">**dtls_session** Pointer to a DTLS Session structure that was initialized previously.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-688">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-688">Return Values</span></span>

- <span data-ttu-id="1a36b-689">L'eliminazione della sessione **NX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-689">**NX_SUCCESS** (0x00) Successful deletion of session.</span></span>
- <span data-ttu-id="1a36b-690">**NX_PTR_ERROR** (0x07) la sessione o il puntatore del buffer non valido.</span><span class="sxs-lookup"><span data-stu-id="1a36b-690">**NX_PTR_ERROR** (0x07) Invalid session or buffer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-691">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-691">Allowed From</span></span>

<span data-ttu-id="1a36b-692">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-692">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-693">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-693">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                        trusted_cert_der,
                                        trusted_cert_der_len,
                                        NX_NULL, 0, NX_NULL, 0,
                                        NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                                    &udp_socket,
                                                    &server_ip, 4443,
                                                    NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

        /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                &receive_packet,
                                                NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-694">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-694">See Also</span></span>

- <span data-ttu-id="1a36b-695">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-695">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-696">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1a36b-696">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span></span>

## <a name="nx_secure_dtls_session_end"></a><span data-ttu-id="1a36b-697">nx_secure_dtls_session_end</span><span class="sxs-lookup"><span data-stu-id="1a36b-697">nx_secure_dtls_session_end</span></span>

<span data-ttu-id="1a36b-698">Arrestare una sessione di DTLS sicura NetX attiva</span><span class="sxs-lookup"><span data-stu-id="1a36b-698">Shut down an active NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-699">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-699">Prototype</span></span>

```C
UINT nx_secure_dtls_session_end(NX_SECURE_DTLS_SESSION *dtls_session,
                                UINT wait_option);

```

### <a name="description"></a><span data-ttu-id="1a36b-700">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-700">Description</span></span>

<span data-ttu-id="1a36b-701">Questo servizio termina una sessione DTLS attiva inviando un avviso TLS/DTLS CloseNotify all'host remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-701">This service ends an active DTLS session by sending a TLS/DTLS CloseNotify alert to the remote host.</span></span> <span data-ttu-id="1a36b-702">L'indirizzo IP e la porta usati sono quelli usati nella chiamata precedente a nx_secure_dtls_session_send.</span><span class="sxs-lookup"><span data-stu-id="1a36b-702">The IP address and port used are those used in the previous call to nx_secure_dtls_session_send.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-703">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-703">Parameters</span></span>

- <span data-ttu-id="1a36b-704">**dtls_session** Puntatore a una struttura di sessione DTLS inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-704">**dtls_session** Pointer to a DTLS Session structure that was initialized previously.</span></span>
- <span data-ttu-id="1a36b-705">**WAIT_OPTION** Valore di attesa ThreadX da utilizzare per le operazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="1a36b-705">**wait_option** ThreadX wait value to use for network operations.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-706">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-706">Return Values</span></span>

- <span data-ttu-id="1a36b-707">L'eliminazione della sessione **NX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-707">**NX_SUCCESS** (0x00) Successful deletion of session.</span></span>
- <span data-ttu-id="1a36b-708">**NX_PTR_ERROR** (0x07) la sessione o il puntatore del buffer non valido.</span><span class="sxs-lookup"><span data-stu-id="1a36b-708">**NX_PTR_ERROR** (0x07) Invalid session or buffer pointer.</span></span>
- <span data-ttu-id="1a36b-709">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) non è stato in grado di allocare i pacchetti per l'avviso CloseNotify.</span><span class="sxs-lookup"><span data-stu-id="1a36b-709">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Could not allocate packet(s) for CloseNotify alert.</span></span>
- <span data-ttu-id="1a36b-710">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) errore interno probabile: la routine di crittografia non è stata riconosciuta.</span><span class="sxs-lookup"><span data-stu-id="1a36b-710">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) Likely internal error – cryptographic routine not recognized.</span></span>
- <span data-ttu-id="1a36b-711">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) invio UDP sottostante non riuscito.</span><span class="sxs-lookup"><span data-stu-id="1a36b-711">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Underlying UDP send failed.</span></span>
- <span data-ttu-id="1a36b-712">Errore **NX_IP_ADDRESS_ERROR** (0x21) con l'indirizzo IP dell'host remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-712">**NX_IP_ADDRESS_ERROR** (0x21) Error with remote host IP address.</span></span>
- <span data-ttu-id="1a36b-713">Il socket UDP sottostante **NX_NOT_BOUND** (0x24) non è associato a una porta.</span><span class="sxs-lookup"><span data-stu-id="1a36b-713">**NX_NOT_BOUND** (0x24) Underlying UDP socket not bound to port.</span></span>
- <span data-ttu-id="1a36b-714">**NX_INVALID_PORT** (0x46) porta UDP non valida.</span><span class="sxs-lookup"><span data-stu-id="1a36b-714">**NX_INVALID_PORT** (0x46) Invalid UDP port.</span></span>
- <span data-ttu-id="1a36b-715">La porta UDP **NX_PORT_UNAVAILABLE** (0x23) non è disponibile per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="1a36b-715">**NX_PORT_UNAVAILABLE** (0x23) UDP port not available for use.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-716">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-716">Allowed From</span></span>

<span data-ttu-id="1a36b-717">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-717">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-718">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-718">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session,
                                                &send_packet,
                                                &server_ip, 4443);

    /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session,
                                        NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

    }

```

### <a name="see-also"></a><span data-ttu-id="1a36b-719">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-719">See Also</span></span>

- <span data-ttu-id="1a36b-720">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-720">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-721">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1a36b-721">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span></span>

## <a name="nx_secure_dtls_session_local_certificate_add"></a><span data-ttu-id="1a36b-722">nx_secure_dtls_session_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-722">nx_secure_dtls_session_local_certificate_add</span></span>

<span data-ttu-id="1a36b-723">Aggiungere un certificato di identità locale a una sessione NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-723">Add a local identity certificate to a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-724">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-724">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_local_certificate_add(
                            NX_SECURE_DTLS_SESSION *session_ptr,
                            NX_SECURE_X509_CERT *certificate,
                            UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="1a36b-725">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-725">Description</span></span>

<span data-ttu-id="1a36b-726">Questo servizio aggiunge un certificato di identità locale a un'istanza di sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-726">This service adds a local identity certificate to a DTLS Session instance.</span></span> <span data-ttu-id="1a36b-727">In generale, questo servizio verrà usato quando una sessione client di DTLS deve fornire un certificato di identità a un host server remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-727">In general, this service will be used when a DTLS Client session needs to provide an identity certificate to a remote server host.</span></span> <span data-ttu-id="1a36b-728">Si tratta di una configurazione facoltativa per DTLS, quindi non è in genere necessario un certificato per i client DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-728">This is an optional configuration for DTLS so a certificate is not generally required for DTLS Clients.</span></span> <span data-ttu-id="1a36b-729">Un certificato di identità richiede una chiave privata associata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-729">An identity certificate requires an associated private key.</span></span>

<span data-ttu-id="1a36b-730">Il parametro cert_id è un identificatore numerico diverso da zero per il certificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-730">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="1a36b-731">Ciò consente di rimuovere facilmente il certificato o di trovarlo nell'evento in cui sono presenti più certificati di identità con lo stesso nome comune X. 509 presente nell'archivio certificati DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-731">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS certificate store.</span></span> <span data-ttu-id="1a36b-732">Per ulteriori informazioni sui certificati X. 509, vedere la guida dell'utente di NetX Secure TLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-732">See the NetX Secure TLS User Guide for more information about X.509 certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-733">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-733">Parameters</span></span>

- <span data-ttu-id="1a36b-734">**session_ptr** Puntatore a un'istanza di sessione DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-734">**session_ptr** Pointer to a previously created DTLS Session instance.</span></span>
- <span data-ttu-id="1a36b-735">**certificato** di Puntatore a una struttura di certificato X. 509 inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-735">**certificate** Pointer to a previously initialized X.509 certificate structure.</span></span>
- <span data-ttu-id="1a36b-736">**cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-736">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-737">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-737">Return Values</span></span>

- <span data-ttu-id="1a36b-738">**NX_SUCCESS** (0x00) aggiunta del certificato alla sessione DTLS completata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-738">**NX_SUCCESS** (0x00) Successful addition of certificate to DTLS session.</span></span>
- <span data-ttu-id="1a36b-739">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-739">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-740">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) è stato passato un ID certificato 0.</span><span class="sxs-lookup"><span data-stu-id="1a36b-740">**NX_INVALID_PARAMETERS** (0x4D) A certificate ID of 0 was passed in.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-741">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-741">Allowed From</span></span>

<span data-ttu-id="1a36b-742">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-742">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-743">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-743">Example</span></span>

<span data-ttu-id="1a36b-744">\* Per un esempio più completo, vedere informazioni di riferimento per *nx_secure_dtls_session_create* .</span><span class="sxs-lookup"><span data-stu-id="1a36b-744">\*See reference for *nx_secure_dtls_session_create* for a more complete example.</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data. Identity
certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

/* Create a TLS session for our socket. Ciphers and metadata defined
   elsewhere. See nx_secure_tls_session_create reference for more
   information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
{
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
}

/* Initialize our trusted certificate. See section “Importing X.509
   Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len,
                                    NX_NULL, 0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

/* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                              &certificate, 1);

    /* Initialize local server identity certificate with key and
    add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                        certificate_der_data,
                        sizeof(certificate_der_data),
                        NX_NULL, 0,
                        certificate_key_der_data,
                        sizeof(certificate_key_der_data),
                        NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                    &certificate, 1);

/* Set up IP address of remote host. */
server_ip.nxd_ip_version = NX_IP_VERSION_V4;
server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


/* Now we can start the DTLS session as normal. */
status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                    &udp_socket, &server_ip, 4443,
                                    NX_IP_PERIODIC_RATE);


    /* Process responses, etc…*/
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-745">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-745">See Also</span></span>

- <span data-ttu-id="1a36b-746">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-746">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-747">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-747">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span></span>
- <span data-ttu-id="1a36b-748">nx_secure_dtls_session_local_certificate_remove,</span><span class="sxs-lookup"><span data-stu-id="1a36b-748">nx_secure_dtls_session_local_certificate_remove,</span></span>
- <span data-ttu-id="1a36b-749">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1a36b-749">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_session_local_certificate_remove"></a><span data-ttu-id="1a36b-750">nx_secure_dtls_session_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1a36b-750">nx_secure_dtls_session_local_certificate_remove</span></span>

<span data-ttu-id="1a36b-751">Rimuovere un certificato di identità locale da una sessione NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-751">Remove a local identity certificate from a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-752">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-752">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_local_certificate_remove(
                                         NX_SECURE_DTLS_SESSION *session_ptr,
                                         UCHAR *common_name,
                                         UINT common_name_length, UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="1a36b-753">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-753">Description</span></span>

<span data-ttu-id="1a36b-754">Questo servizio rimuove un certificato di identità locale da un'istanza di sessione DTLS usando un numero di ID certificato (assegnato quando il certificato è stato aggiunto con nx_secure_dtls_session_local_certificate_add) o il campo CommonName X. 509.</span><span class="sxs-lookup"><span data-stu-id="1a36b-754">This service removes a local identity certificate from a DTLS Session instance using either a certificate ID number (assigned when the certificate was added with nx_secure_dtls_session_local_certificate_add) or the X.509 CommonName field.</span></span>

<span data-ttu-id="1a36b-755">Se il common_name viene usato per trovare la corrispondenza con il certificato, il parametro cert_id deve essere impostato su 0.</span><span class="sxs-lookup"><span data-stu-id="1a36b-755">If the common_name is used to match the certificate, the cert_id parameter should be set to 0.</span></span> <span data-ttu-id="1a36b-756">Se si utilizza cert_id, common_name deve essere passato un valore di NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="1a36b-756">If cert_id is used, common_name should be passed a value of NX_NULL.</span></span>

<span data-ttu-id="1a36b-757">Il parametro cert_id è un identificatore numerico diverso da zero per il certificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-757">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="1a36b-758">Ciò consente di rimuovere facilmente il certificato o di trovarlo nell'evento in cui sono presenti più certificati di identità con lo stesso nome comune X. 509 presente nell'archivio certificati DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-758">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS certificate store.</span></span> <span data-ttu-id="1a36b-759">Per ulteriori informazioni sui certificati X. 509, vedere la guida dell'utente di NetX Secure TLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-759">See the NetX Secure TLS User Guide for more information about X.509 certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-760">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-760">Parameters</span></span>

- <span data-ttu-id="1a36b-761">**session_ptr** Puntatore a un'istanza di sessione DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-761">**session_ptr** Pointer to a previously created DTLS Session instance.</span></span>
- <span data-ttu-id="1a36b-762">**common_name** Puntatore alla stringa comune di cui trovare la corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-762">**common_name** Pointer to the CommonName string to match.</span></span>
- <span data-ttu-id="1a36b-763">**common_name_length** Lunghezza della stringa di common_name.</span><span class="sxs-lookup"><span data-stu-id="1a36b-763">**common_name_length** Length of the common_name string.</span></span>
- <span data-ttu-id="1a36b-764">**cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-764">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-765">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-765">Return Values</span></span>

- <span data-ttu-id="1a36b-766">**NX_SUCCESS** (0x00) la rimozione del certificato dalla sessione DTLS è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-766">**NX_SUCCESS** (0x00) Successful removal of certificate from DTLS session.</span></span>
- <span data-ttu-id="1a36b-767">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-767">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-768">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0X119) non è stato trovato alcun certificato corrispondente al cert_id o common_name nella sessione DTLS specificata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-768">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate matching the cert_id or common_name was found in the given DTLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-769">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-769">Allowed From</span></span>

<span data-ttu-id="1a36b-770">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-770">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-771">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-771">Example</span></span>

<span data-ttu-id="1a36b-772">\* Per un esempio più completo, vedere informazioni di riferimento per *nx_secure_dtls_session_create* .</span><span class="sxs-lookup"><span data-stu-id="1a36b-772">\*See reference for *nx_secure_dtls_session_create* for a more complete example.</span></span>

```C

/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data.
Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
        nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                            &certificate, 1);

        /* Initialize local server identity certificate with key
        and add to server. */
        status = nx_secure_x509_certificate_initialize(&certificate,
                                certificate_der_data,
                                sizeof(certificate_der_data),
                                NX_NULL, 0,
                                certificate_key_der_data,
                                sizeof(certificate_key_der_data),
                                NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

        /* Add local server identity certificate to DTLS server with ID of 1. */
        status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                            &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
        &udp_socket, &server_ip, 4443,
        NX_IP_PERIODIC_RATE);

        /* Process responses, etc…*/

    /* At some point in the future,
    we decide to remove the certificate using the ID of 1
    when it was added to the session. */
        status = nx_secure_dtls_session_local_certificate_remove(&client_dtls_session,
                                                                NX_NULL, 0, 1);
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-773">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-773">See Also</span></span>

- <span data-ttu-id="1a36b-774">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-774">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-775">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-775">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span></span>
- <span data-ttu-id="1a36b-776">nx_secure_dtls_session_local_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="1a36b-776">nx_secure_dtls_session_local_certificate_add,</span></span>
- <span data-ttu-id="1a36b-777">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1a36b-777">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_session_receive"></a><span data-ttu-id="1a36b-778">nx_secure_dtls_session_receive</span><span class="sxs-lookup"><span data-stu-id="1a36b-778">nx_secure_dtls_session_receive</span></span>

<span data-ttu-id="1a36b-779">Ricevere i dati dell'applicazione in una sessione di DTLS sicura NetX stabilita</span><span class="sxs-lookup"><span data-stu-id="1a36b-779">Receive application data over an established NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-780">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-780">Prototype</span></span>

```C
UINT nx_secure_dtls_session_receive(
                                NX_SECURE_DTLS_SESSION *dtls_session,
                                NX_PACKET **packet_ptr_ptr,
                                UINT wait_option);

```

### <a name="description"></a><span data-ttu-id="1a36b-781">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-781">Description</span></span>

<span data-ttu-id="1a36b-782">Questo servizio restituisce i dati dell'applicazione ricevuti da una sessione DTLS attiva.</span><span class="sxs-lookup"><span data-stu-id="1a36b-782">This service returns application data received by an active DTLS Session.</span></span> <span data-ttu-id="1a36b-783">La sessione DTLS può essere una sessione del server DTLS (gestita da un'istanza del server DTLS) o una sessione client DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-783">The DTLS Session may be either a DTLS Server session (managed by a DTLS Server instance) or a DTLS Client session.</span></span> <span data-ttu-id="1a36b-784">Il pacchetto restituito può essere elaborato usando uno dei servizi API NX_PACKET (vedere la documentazione di NetX per altre informazioni).</span><span class="sxs-lookup"><span data-stu-id="1a36b-784">The returned packet may be processed using any of the NX_PACKET API services (see the NetX documentation for more information).</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-785">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-785">Parameters</span></span>

- <span data-ttu-id="1a36b-786">**dtls_session** Puntatore a una struttura di sessione DTLS inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-786">**dtls_session** Pointer to a DTLS Session structure that was initialized previously.</span></span>
- <span data-ttu-id="1a36b-787">**packet_ptr_ptr** Puntatore a un puntatore NX_PACKET per il pacchetto restituito.</span><span class="sxs-lookup"><span data-stu-id="1a36b-787">**packet_ptr_ptr** Pointer to an NX_PACKET pointer for the return packet.</span></span>
- <span data-ttu-id="1a36b-788">**WAIT_OPTION** Valore di attesa ThreadX da utilizzare per le operazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="1a36b-788">**wait_option** ThreadX wait value to use for network operations.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-789">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-789">Return Values</span></span>

- <span data-ttu-id="1a36b-790">**NX_SUCCESS** (0x00) ricevuta correttamente del pacchetto di dati dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-790">**NX_SUCCESS** (0x00) Successful receipt of application data packet.</span></span>
- <span data-ttu-id="1a36b-791">**NX_PTR_ERROR** (0x07) una sessione o un puntatore di pacchetto non valido.</span><span class="sxs-lookup"><span data-stu-id="1a36b-791">**NX_PTR_ERROR** (0x07) Invalid session or packet pointer.</span></span>
- <span data-ttu-id="1a36b-792">Il protocollo UDP **NX_NOT_ENABLED** (0x14) non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-792">**NX_NOT_ENABLED** (0x14) UDP is not enabled.</span></span>
- <span data-ttu-id="1a36b-793">Socket UDP **NX_NOT_BOUND** (0x24) non associato alla porta.</span><span class="sxs-lookup"><span data-stu-id="1a36b-793">**NX_NOT_BOUND** (0x24) UDP socket not bound to port.</span></span>
- <span data-ttu-id="1a36b-794">**NX_SECURE_TLS_INVALID_PACKET** (0X104) recevied dati che non sono record DTLS validi.</span><span class="sxs-lookup"><span data-stu-id="1a36b-794">**NX_SECURE_TLS_INVALID_PACKET** (0x104) Recevied data that was not a valid DTLS record.</span></span>
- <span data-ttu-id="1a36b-795">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) non è stato possibile eseguire correttamente l'hashing di un record DTLS (errore di crittografia).</span><span class="sxs-lookup"><span data-stu-id="1a36b-795">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A DTLS record failed to be properly hashed (encryption error).</span></span>
- <span data-ttu-id="1a36b-796">Verifica della riempimento della crittografia **NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12A) non riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-796">**NX_SECURE_TLS_PADDING_CHECK_FAILED** (0x12A) Encryption padding check failure.</span></span>
- <span data-ttu-id="1a36b-797">**NX_SECURE_TLS_ALERT_RECEIVED** (0X114) recevied un avviso dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-797">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Recevied an alert from the remote host.</span></span>
- <span data-ttu-id="1a36b-798">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE**    (0X102) ha ricevuto un messaggio non riconosciuto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-798">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE**    (0x102) Received an unrecognized message.</span></span>
- <span data-ttu-id="1a36b-799">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0X10A) recevied un record DTLS con una lunghezza non valida.</span><span class="sxs-lookup"><span data-stu-id="1a36b-799">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) Recevied a DTLS record with an invalid length.</span></span>
- <span data-ttu-id="1a36b-800">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) è stato rilevato un CIPHERSUITE sconosciuto (indica l'errore interno della crittografia).</span><span class="sxs-lookup"><span data-stu-id="1a36b-800">**NX_SECURE_TLS_UNKNOWN_CIPHERSUITE** (0x105) An unknown ciphersuite was encountered (indicates internal cryptography error).</span></span>
- <span data-ttu-id="1a36b-801">**NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0X12E) recevied un record DTLS con una versione di DTLS non corrispondente.</span><span class="sxs-lookup"><span data-stu-id="1a36b-801">**NX_SECURE_TLS_PROTOCOL_VERSION_CHANGED** (0x12E) Recevied a DTLS record with a mismatched DTLS version.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-802">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-802">Allowed From</span></span>

<span data-ttu-id="1a36b-803">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-803">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-804">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-804">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
    status = nx_secure_dtls_session_receive(&client_dtls_session, &receive_packet,
                                                            NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_end(&client_dtls_session, NX_IP_PERIODIC_RATE);

    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-805">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-805">See Also</span></span>

- <span data-ttu-id="1a36b-806">nx_secure_dtls_client_session_start, nx_secure_dtls_session_end,</span><span class="sxs-lookup"><span data-stu-id="1a36b-806">nx_secure_dtls_client_session_start, nx_secure_dtls_session_end,</span></span>
- <span data-ttu-id="1a36b-807">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1a36b-807">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span></span>

## <a name="nx_secure_dtls_session_reset"></a><span data-ttu-id="1a36b-808">nx_secure_dtls_session_reset</span><span class="sxs-lookup"><span data-stu-id="1a36b-808">nx_secure_dtls_session_reset</span></span>

<span data-ttu-id="1a36b-809">Cancellare i dati in un'istanza di sessione NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-809">Clear data in an NetX Secure DTLS Session instance</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-810">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-810">Prototype</span></span>

```C
UINT nx_secure_dtls_session_reset(NX_SECURE_DTLS_SESSION *dtls_session);
```

### <a name="description"></a><span data-ttu-id="1a36b-811">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-811">Description</span></span>

<span data-ttu-id="1a36b-812">Questo servizio Reimposta una sessione DTLS, cancellando tutti i dati di crittografia effimeri e consentendo di riutilizzare la struttura per una nuova sessione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-812">This service resets a DTLS session, clearing all ephemeral cryptographic data and allowing the structure to be re-used for a new session.</span></span> <span data-ttu-id="1a36b-813">I dati persistenti, ad esempio gli archivi certificati, vengono mantenuti in modo che non nx_secure_dtls_session_create necessario chiamare ripetutamente.</span><span class="sxs-lookup"><span data-stu-id="1a36b-813">Persistent data (e.g. certificate stores) are maintained so that nx_secure_dtls_session_create need not be called repeatedly.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-814">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-814">Parameters</span></span>

- <span data-ttu-id="1a36b-815">**dtls_session** Puntatore a una struttura di sessione DTLS inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-815">**dtls_session** Pointer to a DTLS Session structure that was initialized previously.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-816">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-816">Return Values</span></span>

- <span data-ttu-id="1a36b-817">**NX_SUCCESS** (0x00) reimpostazione della sessione completata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-817">**NX_SUCCESS** (0x00) Successful reset of session.</span></span>
- <span data-ttu-id="1a36b-818">**NX_PTR_ERROR** (0x07) la sessione o il puntatore del buffer non valido.</span><span class="sxs-lookup"><span data-stu-id="1a36b-818">**NX_PTR_ERROR** (0x07) Invalid session or buffer pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-819">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-819">Allowed From</span></span>

<span data-ttu-id="1a36b-820">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-820">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-821">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-821">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                        &nx_crypto_tls_ciphers,
                                        crypto_metadata,
                                        sizeof(crypto_metadata),
                                        packet_buffer,
                                        sizeof(packet_buffer),
                                        REMOTE_CERT_NUMBER,
                                        remote_certs_buffer,
                                        sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
    printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
            Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
        /* Error! */
        return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

    /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
    status = nx_secure_dtls_session_reset(&client_dtls_session);

    /* A new session can now be started using the same structure. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,



    /* Clean up. */
    status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-822">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-822">See Also</span></span>

- <span data-ttu-id="1a36b-823">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-823">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-824">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span><span class="sxs-lookup"><span data-stu-id="1a36b-824">nx_secure_dtls_session_send, nx_secure_dtls_session_delete</span></span>

## <a name="nx_secure_dtls_-session_send"></a><span data-ttu-id="1a36b-825">nx_secure_dtls_ session_send</span><span class="sxs-lookup"><span data-stu-id="1a36b-825">nx_secure_dtls_ session_send</span></span>

<span data-ttu-id="1a36b-826">Inviare dati tramite una sessione DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-826">Send data over a DTLS session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-827">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-827">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_send(NX_SECURE_DTLS_SESSION *session_ptr,
                                          NX_PACKET *packet_ptr,
                                          NXD_ADDRESS *ip_address, UINT port);

```

### <a name="description"></a><span data-ttu-id="1a36b-828">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-828">Description</span></span>

<span data-ttu-id="1a36b-829">Questo servizio invia un pacchetto di dati su una sessione DTLS stabilita a un host DTLS remoto presso la porta e l'indirizzo IP specificati.</span><span class="sxs-lookup"><span data-stu-id="1a36b-829">This service sends a packet of data over an established DTLS Session to a remote DTLS host at the given IP address and port.</span></span> <span data-ttu-id="1a36b-830">La sessione utilizzata è una sessione client DTLS attiva.</span><span class="sxs-lookup"><span data-stu-id="1a36b-830">The session used is an active DTLS Client session.</span></span> <span data-ttu-id="1a36b-831">Si noti che l'indirizzo IP e la porta sono forniti a causa della natura senza stato di UDP, ma in genere corrispondono all'indirizzo e alla porta usati per avviare la sessione in nx_secure_dtls_session_start.</span><span class="sxs-lookup"><span data-stu-id="1a36b-831">Note that the IP address and port are provided due to the stateless nature of UDP but should generally match the address and port used to start the session in nx_secure_dtls_session_start.</span></span>

<span data-ttu-id="1a36b-832">I dati forniti nel pacchetto, che devono essere allocati tramite *nx_secure_dtls_packet_allocate*, vengono crittografati usando le routine e i parametri crittografici della sessione DTLS e quindi inviati all'host remoto tramite il socket UDP della sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-832">The data provided in the packet, which must be allocated using *nx_secure_dtls_packet_allocate*, is encrypted using the DTLS session cryptographic parameters and routines and then sent to the remote host over the DTLS Session’s UDP socket.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-833">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-833">Parameters</span></span>

- <span data-ttu-id="1a36b-834">**session_ptr** Puntatore a un'istanza di sessione client DTLS attiva.</span><span class="sxs-lookup"><span data-stu-id="1a36b-834">**session_ptr** Pointer to an active DTLS client session instance.</span></span>
- <span data-ttu-id="1a36b-835">**packet_ptr** Puntatore a un'istanza di NX_PACKET allocata in precedenza e popolata con i dati dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a36b-835">**packet_ptr** Pointer to an NX_PACKET instance allocated previously and populated with application data.</span></span>
- <span data-ttu-id="1a36b-836">**ip_address** Puntatore a una struttura di NXD_ADDRESS contenente l'indirizzo IP dell'host remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-836">**ip_address** Pointer to an NXD_ADDRESS structure containing the IP address of the remote host.</span></span>
- <span data-ttu-id="1a36b-837">**porta** Porta UDP sull'host remoto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-837">**port** UDP port on the remote host.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-838">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-838">Return Values</span></span>

- <span data-ttu-id="1a36b-839">Il **NX_SUCCESS** (0x00) ha completato l'invio del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1a36b-839">**NX_SUCCESS** (0x00) Successful send of packet.</span></span>
- <span data-ttu-id="1a36b-840">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-840">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-841">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) si è verificato un errore nell'operazione di invio UDP sottostante.</span><span class="sxs-lookup"><span data-stu-id="1a36b-841">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) An error occurred in the underlying UDP send operation.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-842">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-842">Allowed From</span></span>

<span data-ttu-id="1a36b-843">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-843">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-844">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-844">Example</span></span>

```C
/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_DTLS_SESSION client_dtls_session;

/* Trusted certificate structure and raw data. */
NX_SECURE_X509_CERT trusted_cert;
const UCHAR trusted_cert_der = { … };

/* Cryptography routines and crypto work buffers. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;
UCHAR crypto_metadata[9000];

/* Packet reassembly buffer for decryption. */
UCHAR packet_buffer[4000];

/* Remote certificate buffer for incoming certificates. */
#define REMOTE_CERT_SIZE (sizeof(NX_SECURE_X509_CERT) + 2000)
#define REMOTE_CERT_NUMBER  (3)
UCHAR remote_certs_buffer[REMOTE_CERT_SIZE * REMOTE_CERT_NUMBER];

/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL,
                                    0, NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    if(status != NX_SUCCESS)
    {
    /* Error! */
    return(status);
    }

    /* Add data to send packet as usual for NX_PACKET and send to server.  */
    status = nx_secure_dtls_session_send(&client_dtls_session, &send_packet,
                                                        &server_ip, 4443);

        /* Receive response from server. */
        status = nx_secure_dtls_session_receive(&client_dtls_session,
                                                    &receive_packet,
                                                    NX_IP_PERIODIC_RATE);

    /* Process response. */

    /* Shut down DTLS session. */
        status = nx_secure_dtls_session_end(&client_dtls_session,
                                            NX_IP_PERIODIC_RATE);

    /* Clean up. */
        status = nx_secure_dtls_session_delete(&client_dtls_session);

}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-845">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-845">See Also</span></span>

- <span data-ttu-id="1a36b-846">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-846">nx_secure_dtls_client_session_start, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-847">nx_secure_dtls_session_create</span><span class="sxs-lookup"><span data-stu-id="1a36b-847">nx_secure_dtls_session_create</span></span>

## <a name="nx_secure_dtls_session_trusted_certificate_add"></a><span data-ttu-id="1a36b-848">nx_secure_dtls_session_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="1a36b-848">nx_secure_dtls_session_trusted_certificate_add</span></span>

<span data-ttu-id="1a36b-849">Aggiungere un certificato CA attendibile a una sessione NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-849">Add a trusted CA certificate to a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-850">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-850">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_trusted_certificate_add(
                                         NX_SECURE_DTLS_SESSION *session_ptr,
                                         NX_SECURE_X509_CERT *certificate,
                                         UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="1a36b-851">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-851">Description</span></span>

<span data-ttu-id="1a36b-852">Questo servizio aggiunge una CA attendibile o un certificato X. 509 CA attendibile a un'istanza di sessione DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-852">This service adds a trusted CA or intermediate CA X.509 certificate to a DTLS Session instance.</span></span> <span data-ttu-id="1a36b-853">Per convalidare i certificati del server remoto, un client DTLS richiede almeno un certificato attendibile, a meno che non venga usato un meccanismo di autenticazione alternativo (ad esempio, le chiavi precondivise).</span><span class="sxs-lookup"><span data-stu-id="1a36b-853">A DTLS Client requires at least one trusted certificate in order to validate remote server certificates unless an alternative authentication mechanism is used (e.g. Pre-Shared Keys).</span></span> <span data-ttu-id="1a36b-854">Un certificato attendibile non dispone in genere di una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-854">A trusted certificate does not usually have a private key.</span></span>

<span data-ttu-id="1a36b-855">Il parametro cert_id è un identificatore numerico diverso da zero per il certificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-855">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="1a36b-856">Ciò consente di rimuovere facilmente il certificato o di trovarlo nell'evento in cui sono presenti più certificati di identità con lo stesso nome comune X. 509 presente nell'archivio certificati DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-856">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS certificate store.</span></span> <span data-ttu-id="1a36b-857">Per ulteriori informazioni sui certificati X. 509, vedere la guida dell'utente di NetX Secure TLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-857">See the NetX Secure TLS User Guide for more information about X.509 certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-858">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-858">Parameters</span></span>

- <span data-ttu-id="1a36b-859">**session_ptr** Puntatore a un'istanza di sessione DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-859">**session_ptr** Pointer to a previously created DTLS Session instance.</span></span>
- <span data-ttu-id="1a36b-860">**certificato** di Puntatore a una struttura di certificato X. 509 inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-860">**certificate** Pointer to a previously initialized X.509 certificate structure.</span></span>
- <span data-ttu-id="1a36b-861">**cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-861">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>

### <a name="return-values"></a><span data-ttu-id="1a36b-862">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-862">Return Values</span></span>

- <span data-ttu-id="1a36b-863">**NX_SUCCESS** (0x00) aggiunta del certificato alla sessione DTLS completata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-863">**NX_SUCCESS** (0x00) Successful addition of certificate to DTLS session.</span></span>
- <span data-ttu-id="1a36b-864">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-864">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-865">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) è stato passato un ID certificato 0.</span><span class="sxs-lookup"><span data-stu-id="1a36b-865">**NX_INVALID_PARAMETERS** (0x4D) A certificate ID of 0 was passed in.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-866">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-866">Allowed From</span></span>

<span data-ttu-id="1a36b-867">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-867">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-868">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-868">Example</span></span>

<span data-ttu-id="1a36b-869">\* Per un esempio più completo, vedere informazioni di riferimento per *nx_secure_dtls_session_create* .</span><span class="sxs-lookup"><span data-stu-id="1a36b-869">\*See reference for *nx_secure_dtls_session_create* for a more complete example.</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data.
Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
   Certificates into NetX Secure” for more information. */
    nx_secure_x509_certificate_initialize(&trusted_certificate,
                                            trusted_cert_der,
                                            trusted_cert_der_len,
                                            NX_NULL, 0, NX_NULL, 0,
                                            NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the trusted store using a numeric ID. */
    nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                      &certificate, 1);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0,
                                            certificate_key_der_data,
                                            sizeof(certificate_key_der_data),
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);

    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
         &udp_socket, &server_ip, 4443,
         NX_IP_PERIODIC_RATE);


    /* Process responses, etc…*/
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-870">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-870">See Also</span></span>

- <span data-ttu-id="1a36b-871">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-871">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-872">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-872">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span></span>
- <span data-ttu-id="1a36b-873">nx_secure_dtls_session_trusted_certificate_remove,</span><span class="sxs-lookup"><span data-stu-id="1a36b-873">nx_secure_dtls_session_trusted_certificate_remove,</span></span>
- <span data-ttu-id="1a36b-874">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1a36b-874">nx_secure_x509_certificate_initialize</span></span>

## <a name="nx_secure_dtls_session_trusted_certificate_remove"></a><span data-ttu-id="1a36b-875">nx_secure_dtls_session_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="1a36b-875">nx_secure_dtls_session_trusted_certificate_remove</span></span>

<span data-ttu-id="1a36b-876">Rimuovere un certificato CA attendibile da una sessione NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="1a36b-876">Remove a trusted CA certificate from a NetX Secure DTLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="1a36b-877">Prototipo</span><span class="sxs-lookup"><span data-stu-id="1a36b-877">Prototype</span></span>

```C
UINT  nx_secure_dtls_session_trusted_certificate_remove(
                            NX_SECURE_DTLS_SESSION *session_ptr,
                            UCHAR *common_name,
                            UINT common_name_length, UINT cert_id);

```

### <a name="description"></a><span data-ttu-id="1a36b-878">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a36b-878">Description</span></span>

<span data-ttu-id="1a36b-879">Questo servizio rimuove un certificato CA attendibile da un'istanza di sessione DTLS usando un numero di ID certificato (assegnato quando il certificato è stato aggiunto con nx_secure_dtls_session_trusted_certificate_add) o il campo CommonName X. 509.</span><span class="sxs-lookup"><span data-stu-id="1a36b-879">This service removes a trusted CA certificate from a DTLS Session instance using either a certificate ID number (assigned when the certificate was added with nx_secure_dtls_session_trusted_certificate_add) or the X.509 CommonName field.</span></span>

<span data-ttu-id="1a36b-880">Se il common_name viene usato per trovare la corrispondenza con il certificato, il parametro cert_id deve essere impostato su 0.</span><span class="sxs-lookup"><span data-stu-id="1a36b-880">If the common_name is used to match the certificate, the cert_id parameter should be set to 0.</span></span> <span data-ttu-id="1a36b-881">Se si utilizza cert_id, common_name deve essere passato un valore di NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="1a36b-881">If cert_id is used, common_name should be passed a value of NX_NULL.</span></span>

<span data-ttu-id="1a36b-882">Il parametro cert_id è un identificatore numerico diverso da zero per il certificato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-882">The cert_id parameter is a numeric, non-zero identifier for the certificate.</span></span> <span data-ttu-id="1a36b-883">Ciò consente di rimuovere facilmente il certificato o di trovarlo nell'evento in cui sono presenti più certificati di identità con lo stesso nome comune X. 509 presente nell'archivio certificati DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-883">This enables the certificate to be easily removed or found in the event there are multiple identity certificates with the same X.509 Common Name present in the DTLS certificate store.</span></span> <span data-ttu-id="1a36b-884">Per ulteriori informazioni sui certificati X. 509, vedere la guida dell'utente di NetX Secure TLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-884">See the NetX Secure TLS User Guide for more information about X.509 certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="1a36b-885">Parametri</span><span class="sxs-lookup"><span data-stu-id="1a36b-885">Parameters</span></span>

- <span data-ttu-id="1a36b-886">**session_ptr** Puntatore a un'istanza di sessione DTLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-886">**session_ptr** Pointer to a previously created DTLS Session instance.</span></span>
- <span data-ttu-id="1a36b-887">**common_name** Puntatore alla stringa comune di cui trovare la corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="1a36b-887">**common_name** Pointer to the CommonName string to match.</span></span>
- <span data-ttu-id="1a36b-888">**common_name_length** Lunghezza della stringa di common_name.</span><span class="sxs-lookup"><span data-stu-id="1a36b-888">**common_name_length** Length of the common_name string.</span></span>
- <span data-ttu-id="1a36b-889">**cert_id** Identificatore univoco numerico diverso da zero per questo certificato in questo server DTLS.</span><span class="sxs-lookup"><span data-stu-id="1a36b-889">**cert_id** Numeric non-zero unique identifier for this certificate in this DTLS server.</span></span>


### <a name="return-values"></a><span data-ttu-id="1a36b-890">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="1a36b-890">Return Values</span></span>

- <span data-ttu-id="1a36b-891">**NX_SUCCESS** (0x00) la rimozione del certificato dalla sessione DTLS è riuscita.</span><span class="sxs-lookup"><span data-stu-id="1a36b-891">**NX_SUCCESS** (0x00) Successful removal of certificate from DTLS session.</span></span>
- <span data-ttu-id="1a36b-892">**NX_PTR_ERROR** puntatore non valido (0x07) passato.</span><span class="sxs-lookup"><span data-stu-id="1a36b-892">**NX_PTR_ERROR** (0x07) Invalid pointer passed.</span></span>
- <span data-ttu-id="1a36b-893">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0X119) non è stato trovato alcun certificato corrispondente al cert_id o common_name nella sessione DTLS specificata.</span><span class="sxs-lookup"><span data-stu-id="1a36b-893">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate matching the cert_id or common_name was found in the given DTLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="1a36b-894">Consentito da</span><span class="sxs-lookup"><span data-stu-id="1a36b-894">Allowed From</span></span>

<span data-ttu-id="1a36b-895">Thread</span><span class="sxs-lookup"><span data-stu-id="1a36b-895">Threads</span></span>

### <a name="example"></a><span data-ttu-id="1a36b-896">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a36b-896">Example</span></span>

<span data-ttu-id="1a36b-897">\* Per un esempio più completo, vedere informazioni di riferimento per *nx_secure_dtls_session_create* .</span><span class="sxs-lookup"><span data-stu-id="1a36b-897">\*See reference for *nx_secure_dtls_session_create* for a more complete example.</span></span>

```C
/* Our DTLS Server instance. */
NX_SECURE_DTLS_SESSION dtls_client;

/* Certificate control block and data. Identity certificates require a private key. */
NX_SECURE_X509_CERT certificate;
UCHAR certificate_der_data[] = { … };
UCHAR certificate_key_der_data[] = { … };


/* Application thread where TLS session is started. */
void application_thread()
{
    NXD_ADDRESS server_ip;

    /* Create a TLS session for our socket. Ciphers and metadata defined
    elsewhere. See nx_secure_tls_session_create reference for more
    information. */
        status =  nx_secure_dtls_session_create(&client_dtls_session,
                                            &nx_crypto_tls_ciphers,
                                            crypto_metadata,
                                            sizeof(crypto_metadata),
                                            packet_buffer,
                                            sizeof(packet_buffer),
                                            REMOTE_CERT_NUMBER,
                                            remote_certs_buffer,
                                            sizeof(remote_certs_buffer));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_dtls_session_create: 0x%x\n", status);
    }

    /* Initialize our trusted certificate. See section “Importing X.509
    Certificates into NetX Secure” for more information. */
        nx_secure_x509_certificate_initialize(&trusted_certificate,
                                    trusted_cert_der,
                                    trusted_cert_der_len, NX_NULL, 0,
                                    NX_NULL, 0,
                                    NX_SECURE_X509_KEY_TYPE_NONE);

    /* Add the certificate to the local store using a numeric ID. */
        nx_secure_dtls_session_trusted_certificate_add(&client_dtls_session,
                                                            &certificate, 1);

    /* Initialize local server identity certificate with key and add to server. */
    status = nx_secure_x509_certificate_initialize(&certificate,
                                            certificate_der_data,
                                            sizeof(certificate_der_data),
                                            NX_NULL, 0,
                                            certificate_key_der_data,
                                            sizeof(certificate_key_der_data),
                                            NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add local server identity certificate to DTLS server with ID of 1. */
    status = nx_secure_dtls_session_local_certificate_add(&dtls_client,
                                                        &certificate, 1);

    /* Set up IP address of remote host. */
    server_ip.nxd_ip_version = NX_IP_VERSION_V4;
    server_ip.nxd_ip_address.v4 = IP_ADDRESS(192, 168, 1, 150);


    /* Now we can start the DTLS session as normal. */
    status =  nx_secure_dtls_client_session_start(&client_dtls_session,
                                        &udp_socket, &server_ip, 4443,
                                        NX_IP_PERIODIC_RATE);

    /* Process responses, etc…*/

    /* At some point in the future,
    we decide to remove the certificate using the ID of 1
    when it was added to the session. */
    status = nx_secure_dtls_session_trusted_certificate_remove(&client_dtls_session,
                                                                    NX_NULL, 0, 1);
}

```

### <a name="see-also"></a><span data-ttu-id="1a36b-898">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a36b-898">See Also</span></span>

- <span data-ttu-id="1a36b-899">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span><span class="sxs-lookup"><span data-stu-id="1a36b-899">nx_secure_dtls_session_create, nx_secure_dtls_session_receive,</span></span>
- <span data-ttu-id="1a36b-900">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span><span class="sxs-lookup"><span data-stu-id="1a36b-900">nx_secure_dtls_session_send, nx_secure_dtls_session_start,</span></span>
- <span data-ttu-id="1a36b-901">nx_secure_dtls_session_trusted_certificate_add,</span><span class="sxs-lookup"><span data-stu-id="1a36b-901">nx_secure_dtls_session_trusted_certificate_add,</span></span>
- <span data-ttu-id="1a36b-902">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="1a36b-902">nx_secure_x509_certificate_initialize</span></span>
