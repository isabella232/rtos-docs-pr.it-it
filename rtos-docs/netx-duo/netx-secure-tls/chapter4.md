---
title: Capitolo 4-Descrizione dei servizi sicuri di Azure RTO NetX
description: Questo capitolo contiene una descrizione di tutti i servizi protetti NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 89761ec3438b1b16c1a603764bf7d4e1eac1b4ea
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822853"
---
# <a name="chapter-4---description-of-azure-rtos-netx-secure-services"></a><span data-ttu-id="2f02e-103">Capitolo 4-Descrizione dei servizi sicuri di Azure RTO NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-103">Chapter 4 - Description of Azure RTOS NetX Secure services</span></span>

<span data-ttu-id="2f02e-104">Questo capitolo contiene una descrizione di tutti i servizi protetti di Azure RTO NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="2f02e-104">This chapter contains a description of all Azure RTOS NetX Secure services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="2f02e-105">Nella sezione "valori restituiti" nelle descrizioni API seguenti i valori in **grassetto** non sono interessati dalla macro **NX_SECURE_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_SECURE_DISABLE_ERROR_CHECKING** macro that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- [<span data-ttu-id="2f02e-106">nx_secure_crypto_table_self_test</span><span class="sxs-lookup"><span data-stu-id="2f02e-106">nx_secure_crypto_table_self_test</span></span>](#nx_secure_crypto_table_self_test)
  - <span data-ttu-id="2f02e-107">Eseguire self_test sui metodi di crittografia</span><span class="sxs-lookup"><span data-stu-id="2f02e-107">Perform self_test on the crypto methods</span></span>
- [<span data-ttu-id="2f02e-108">nx_secure_module_hash_compute</span><span class="sxs-lookup"><span data-stu-id="2f02e-108">nx_secure_module_hash_compute</span></span>](#nx_secure_module_hash_compute)
  - <span data-ttu-id="2f02e-109">Calcola il valore hash utilizzando user_supplied funzione hash</span><span class="sxs-lookup"><span data-stu-id="2f02e-109">Computes hash value using user_supplied hash function</span></span>
- [<span data-ttu-id="2f02e-110">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-110">nx_secure_tls_active_certificate_set</span></span>](#nx_secure_tls_active_certificate_set)
  - <span data-ttu-id="2f02e-111">Impostare il certificato di identità attivo per una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-111">Set the active identity certificate for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-112">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-112">nx_secure_tls_client_psk_set</span></span>](#nx_secure_tls_client_psk_set)
  - <span data-ttu-id="2f02e-113">Impostare una chiave di Pre_Shared per una sessione client TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-113">Set a Pre_Shared Key for a NetX Secure TLS Client Session</span></span>
- [<span data-ttu-id="2f02e-114">nx_secure_tls_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-114">nx_secure_tls_initialize</span></span>](#nx_secure_tls_initialize)
  - <span data-ttu-id="2f02e-115">Inizializza il modulo TLS sicuro NetX]</span><span class="sxs-lookup"><span data-stu-id="2f02e-115">Initializes the NetX Secure TLS module]</span></span>
- [<span data-ttu-id="2f02e-116">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-116">nx_secure_tls_local_certificate_add</span></span>](#nx_secure_tls_local_certificate_add)
  - <span data-ttu-id="2f02e-117">Aggiungere un certificato locale a una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-117">Add a local certificate to NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-118">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-118">nx_secure_tls_local_certificate_find</span></span>](#nx_secure_tls_local_certificate_find)
  - <span data-ttu-id="2f02e-119">Trovare un certificato locale in una sessione TLS sicura NetX per nome comune</span><span class="sxs-lookup"><span data-stu-id="2f02e-119">Find a local certificate in a NetX Secure TLS Session by Common Name</span></span>
- [<span data-ttu-id="2f02e-120">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-120">nx_secure_tls_local_certificate_remove</span></span>](#nx_secure_tls_local_certificate_remove)
  - <span data-ttu-id="2f02e-121">Rimuovere il certificato locale dalla sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-121">Remove local certificate from NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-122">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="2f02e-122">nx_secure_tls_metadata_size_calculate</span></span>](#nx_secure_tls_metadata_size_calculate)
  - <span data-ttu-id="2f02e-123">Calcolo delle dimensioni dei metadati crittografici per una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-123">Calculate size of cryptographic metadata for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-124">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-124">nx_secure_tls_packet_allocate</span></span>](#nx_secure_tls_packet_allocate)
  - <span data-ttu-id="2f02e-125">Allocare un pacchetto per una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-125">Allocate a packet for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-126">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-126">nx_secure_tls_psk_add</span></span>](#nx_secure_tls_psk_add)
  - <span data-ttu-id="2f02e-127">Aggiungere una chiave di Pre_Shared a una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-127">Add a Pre_Shared Key to a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-128">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-128">nx_secure_tls_remote_certificate_allocate</span></span>](#nx_secure_tls_remote_certificate_allocate)
  - <span data-ttu-id="2f02e-129">Alloca spazio per il certificato fornito da un host TLS remoto</span><span class="sxs-lookup"><span data-stu-id="2f02e-129">Allocate space for the certificate provided by a remote TLS host</span></span>
- [<span data-ttu-id="2f02e-130">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-130">nx_secure_tls_remote_certificate_buffer_allocate</span></span>](#nx_secure_tls_remote_certificate_buffer_allocate)
  - <span data-ttu-id="2f02e-131">Alloca spazio per tutti i certificati forniti da un host TLS remoto</span><span class="sxs-lookup"><span data-stu-id="2f02e-131">Allocate space for all certificates provided by a remote TLS host</span></span>
- [<span data-ttu-id="2f02e-132">nx_secure_tls_remote_certificate_free_all</span><span class="sxs-lookup"><span data-stu-id="2f02e-132">nx_secure_tls_remote_certificate_free_all</span></span>](#nx_secure_tls_remote_certificate_free_all)
  - <span data-ttu-id="2f02e-133">Spazio disponibile allocato per i certificati in ingresso</span><span class="sxs-lookup"><span data-stu-id="2f02e-133">Free space allocated for incoming certificates</span></span>
- [<span data-ttu-id="2f02e-134">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-134">nx_secure_tls_server_certificate_add</span></span>](#nx_secure_tls_server_certificate_add)
  - <span data-ttu-id="2f02e-135">Aggiungere un certificato in modo specifico per i server TLS usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="2f02e-135">Add a certificate specifically for TLS servers using a numeric identifier</span></span>
- [<span data-ttu-id="2f02e-136">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-136">nx_secure_tls_server_certificate_find</span></span>](#nx_secure_tls_server_certificate_find)
  - <span data-ttu-id="2f02e-137">Trovare un certificato usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="2f02e-137">Find a certificate using a numeric identifier</span></span>
- [<span data-ttu-id="2f02e-138">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-138">nx_secure_tls_server_certificate_remove</span></span>](#nx_secure_tls_server_certificate_remove)
  - <span data-ttu-id="2f02e-139">Rimuovere un certificato del server locale usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="2f02e-139">Remove a local server certificate using a numeric identifier</span></span>
- [<span data-ttu-id="2f02e-140">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-140">nx_secure_tls_session_certificate_callback_set</span></span>](#nx_secure_tls_session_certificate_callback_set)
  - <span data-ttu-id="2f02e-141">Configurare un callback per TLS da usare per la convalida aggiuntiva dei certificati</span><span class="sxs-lookup"><span data-stu-id="2f02e-141">Set up a callback for TLS to use for additional certificate validation</span></span>
- [<span data-ttu-id="2f02e-142">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-142">nx_secure_tls_session_client_callback_set</span></span>](#nx_secure_tls_session_client_callback_set)
  - <span data-ttu-id="2f02e-143">Configurare un callback per TLS da richiamare all'inizio di un handshake client TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-143">Set up a callback for TLS to invoke at the beginning of a TLS Client handshake</span></span>
- [<span data-ttu-id="2f02e-144">nx_secure_tls_session_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="2f02e-144">nx_secure_tls_session_x509_client_verify_configure</span></span>](#nx_secure_tls_session_x509_client_verify_configure)
  - <span data-ttu-id="2f02e-145">Abilitare la verifica del client X. 509 e allocare spazio per i certificati client</span><span class="sxs-lookup"><span data-stu-id="2f02e-145">Enable client X.509 verification and allocate space for client certificates</span></span>
- [<span data-ttu-id="2f02e-146">nx_secure_tls_session_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="2f02e-146">nx_secure_tls_session_client_verify_disable</span></span>](#nx_secure_tls_session_client_verify_disable)
  - <span data-ttu-id="2f02e-147">Disabilitare l'autenticazione del certificato client per una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-147">Disable Client Certificate Authentication for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-148">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="2f02e-148">nx_secure_tls_session_client_verify_enable</span></span>](#nx_secure_tls_session_client_verify_enable)
  - <span data-ttu-id="2f02e-149">Abilitare l'autenticazione del certificato client per una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-149">Enable Client Certificate Authentication for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-150">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-150">nx_secure_tls_session_create</span></span>](#nx_secure_tls_session_create)
  - <span data-ttu-id="2f02e-151">Creare una sessione TLS sicura NetX per le comunicazioni sicure</span><span class="sxs-lookup"><span data-stu-id="2f02e-151">Create a NetX Secure TLS Session for secure communications</span></span>
- [<span data-ttu-id="2f02e-152">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-152">nx_secure_tls_session_delete</span></span>](#nx_secure_tls_session_delete)
  - <span data-ttu-id="2f02e-153">Eliminare una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-153">Delete a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-154">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="2f02e-154">nx_secure_tls_session_end</span></span>](#nx_secure_tls_session_end)
  - <span data-ttu-id="2f02e-155">Terminare una sessione TLS protetta NetX attiva</span><span class="sxs-lookup"><span data-stu-id="2f02e-155">End an active NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-156">nx_secure_tls_session_packet_buffer_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-156">nx_secure_tls_session_packet_buffer_set</span></span>](#nx_secure_tls_session_packet_buffer_set)
  - <span data-ttu-id="2f02e-157">Impostare il buffer di riassemblaggio dei pacchetti per una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-157">Set the packet reassembly buffer for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-158">nx_secure_tls_session_protocol_version_override</span><span class="sxs-lookup"><span data-stu-id="2f02e-158">nx_secure_tls_session_protocol_version_override</span></span>](#nx_secure_tls_session_protocol_version_override)
  - <span data-ttu-id="2f02e-159">Eseguire l'override della versione del protocollo TLS predefinita per una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-159">Override the default TLS protocol version for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-160">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-160">nx_secure_tls_session_receive</span></span>](#nx_secure_tls_session_receive)
  - <span data-ttu-id="2f02e-161">Ricevere dati da una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-161">Receive data from a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-162">nx_secure_tls_session_renegotiate_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-162">nx_secure_tls_session_renegotiate_callback_set</span></span>](#nx_secure_tls_session_renegotiate_callback_set)
  - <span data-ttu-id="2f02e-163">Assegnare un callback che verrà richiamato all'inizio di una rinegoziazione della sessione</span><span class="sxs-lookup"><span data-stu-id="2f02e-163">Assign a callback that will be invoked at the beginning of a session renegotiation</span></span>
- [<span data-ttu-id="2f02e-164">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="2f02e-164">nx_secure_tls_session_renegotiate</span></span>](#nx_secure_tls_session_renegotiate)
  - <span data-ttu-id="2f02e-165">Avviare un handshake di rinegoziazione della sessione con l'host remoto</span><span class="sxs-lookup"><span data-stu-id="2f02e-165">Initiate a session renegotiation handshake with the remote host</span></span>
- [<span data-ttu-id="2f02e-166">nx_secure_tls_session_reset</span><span class="sxs-lookup"><span data-stu-id="2f02e-166">nx_secure_tls_session_reset</span></span>](#nx_secure_tls_session_reset)
  - <span data-ttu-id="2f02e-167">Cancellare e reimpostare una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-167">Clear out and reset a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-168">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-168">nx_secure_tls_session_send</span></span>](#nx_secure_tls_session_send)
  - <span data-ttu-id="2f02e-169">Inviare dati tramite una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-169">Send data through a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-170">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-170">nx_secure_tls_session_server_callback_set</span></span>](#nx_secure_tls_session_server_callback_set)
  - <span data-ttu-id="2f02e-171">Configurare un callback per TLS da richiamare all'inizio di un handshake del server TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-171">Set up a callback for TLS to invoke at the beginning of a TLS Server handshake</span></span>
- [<span data-ttu-id="2f02e-172">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-172">nx_secure_tls_session_sni_extension_parse</span></span>](#nx_secure_tls_session_sni_extension_parse)
  - <span data-ttu-id="2f02e-173">Analizzare un'estensione di Indicazione nome server (SNI) ricevuta da un client TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-173">Parse a Server Name Indication (SNI) extension received from a TLS Client</span></span>
- [<span data-ttu-id="2f02e-174">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-174">nx_secure_tls_session_sni_extension_set</span></span>](#nx_secure_tls_session_sni_extension_set)
  - <span data-ttu-id="2f02e-175">Impostare un nome DNS dell'estensione Indicazione nome server (SNI) da inviare a un server remoto</span><span class="sxs-lookup"><span data-stu-id="2f02e-175">Set a Server Name Indication (SNI) extension DNS name to send to a remote Server</span></span>
- [<span data-ttu-id="2f02e-176">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-176">nx_secure_tls_session_start</span></span>](#nx_secure_tls_session_start)
  - <span data-ttu-id="2f02e-177">Avviare una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-177">Start a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-178">nx_secure_tls_session_time_function_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-178">nx_secure_tls_session_time_function_set</span></span>](#nx_secure_tls_session_time_function_set)
  - <span data-ttu-id="2f02e-179">Assegnare una funzione timestamp a una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-179">Assign a timestamp function to a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-180">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-180">nx_secure_tls_trusted_certificate_add</span></span>](#nx_secure_tls_trusted_certificate_add)
  - <span data-ttu-id="2f02e-181">Aggiungere un certificato attendibile alla sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-181">Add trusted certificate to NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-182">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-182">nx_secure_tls_trusted_certificate_remove</span></span>](#nx_secure_tls_trusted_certificate_remove)
  - <span data-ttu-id="2f02e-183">Rimuovere il certificato attendibile dalla sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-183">Remove trusted certificate from NetX Secure TLS Session</span></span>
- [<span data-ttu-id="2f02e-184">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-184">nx_secure_x509_certificate_initialize</span></span>](#nx_secure_x509_certificate_initialize)
  - <span data-ttu-id="2f02e-185">Inizializzare il certificato X. 509 per NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-185">Initialize X.509 Certificate for NetX Secure TLS</span></span>
- [<span data-ttu-id="2f02e-186">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-186">nx_secure_x509_common_name_dns_check</span></span>](#nx_secure_x509_common_name_dns_check)
  - <span data-ttu-id="2f02e-187">Verificare il nome DNS rispetto al certificato X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-187">Check DNS name against X.509 Certificate</span></span>
- [<span data-ttu-id="2f02e-188">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-188">nx_secure_x509_crl_revocation_check</span></span>](#nx_secure_x509_crl_revocation_check)
  - <span data-ttu-id="2f02e-189">Controllare il certificato X. 509 in base a un elenco di revoche di certificati (CRL) specificato]</span><span class="sxs-lookup"><span data-stu-id="2f02e-189">Check X.509 Certificate against a supplied Certificate Revocation List (CRL)]</span></span>
- [<span data-ttu-id="2f02e-190">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-190">nx_secure_x509_dns_name_initialize</span></span>](#nx_secure_x509_dns_name_initialize)
  - <span data-ttu-id="2f02e-191">Inizializzare una struttura del nome DNS X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-191">Initialize an X.509 DNS name structure</span></span>
- [<span data-ttu-id="2f02e-192">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-192">nx_secure_x509_extended_key_usage_extension_parse</span></span>](#nx_secure_x509_extended_key_usage_extension_parse)
  - <span data-ttu-id="2f02e-193">Trovare e analizzare un'estensione per l'utilizzo delle chiavi estese X. 509 in un certificato X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-193">Find and parse an X.509 extended key usage extension in an X.509 certificate</span></span>
- [<span data-ttu-id="2f02e-194">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-194">nx_secure_x509_extension_find</span></span>](#nx_secure_x509_extension_find)
  - <span data-ttu-id="2f02e-195">Trovare e restituire un'estensione X. 509 in un certificato X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-195">Find and return an X.509 extension in an X.509 certificate</span></span>
- [<span data-ttu-id="2f02e-196">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-196">nx_secure_x509_key_usage_extension_parse</span></span>](#nx_secure_x509_key_usage_extension_parse)
  - <span data-ttu-id="2f02e-197">Trovare e analizzare un'estensione per l'utilizzo della chiave X. 509 in un certificato X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-197">Find and parse an X.509 Key Usage extension in an X.509 certificate</span></span>

## <a name="nx_secure_crypto_table_self_test"></a><span data-ttu-id="2f02e-198">nx_secure_crypto_table_self_test</span><span class="sxs-lookup"><span data-stu-id="2f02e-198">nx_secure_crypto_table_self_test</span></span>

<span data-ttu-id="2f02e-199">Eseguire test autonomi sui metodi di crittografia</span><span class="sxs-lookup"><span data-stu-id="2f02e-199">Perform self-test on the crypto methods</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-200">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-200">Prototype</span></span>

```C
UINT nx_secure_crypto_table_self_test(
                                  const NX_SECURE_TLS_CRYPTO *crypto_table,
                                  VOID *metadata, UINT metadata_size);
```

### <a name="description"></a><span data-ttu-id="2f02e-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-201">Description</span></span>

<span data-ttu-id="2f02e-202">Questo servizio esegue gli autotest del metodo Crypto per la convalida.</span><span class="sxs-lookup"><span data-stu-id="2f02e-202">This service runs through the crypto method self tests to validate.</span></span> <span data-ttu-id="2f02e-203">Il test automatico è disponibile solo se la libreria protetta NetX è compilata con il simbolo NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK definito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-203">The self test is available only if NetX Secure library is built with the symbol NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK defined.</span></span>

<span data-ttu-id="2f02e-204">Per ogni metodo Crypto supportato, il test automatico fornisce dati di input predefiniti e verifica che l'output corrisponda al valore previsto predefinito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-204">For each supported crypto method, the self test provides pre-defined input data, and verified the output matches the pre-defined expected value.</span></span>

<span data-ttu-id="2f02e-205">NetX Secure Crypto self test supporta gli algoritmi e le dimensioni delle chiavi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f02e-205">NetX Secure crypto self test supports the following algorithms and key sizes:</span></span>

- <span data-ttu-id="2f02e-206">DES: crittografia e decrittografia</span><span class="sxs-lookup"><span data-stu-id="2f02e-206">DES: encryption and decryption</span></span>
- <span data-ttu-id="2f02e-207">Triple DES (3DES): crittografia e decrittografia</span><span class="sxs-lookup"><span data-stu-id="2f02e-207">Triple DES (3DES): encryption and decryption</span></span>
- <span data-ttu-id="2f02e-208">AES: 128-, 192-, dimensioni della chiave a 256 bit, crittografia e decrittografia, in modalità CBC e in modalità contatore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-208">AES: 128-, 192-, 256-bit key size, encryption and decryption, in CBC mode and counter mode.</span></span>
- <span data-ttu-id="2f02e-209">HMAC-MD5: autenticazione e calcolo hash</span><span class="sxs-lookup"><span data-stu-id="2f02e-209">HMAC-MD5: authentication and hash computation</span></span>
- <span data-ttu-id="2f02e-210">HMAC-SHA: SHA1-96, SHA1-160, SHA2-256, SHA2-384, SHA2-512, autenticazione e calcolo hash</span><span class="sxs-lookup"><span data-stu-id="2f02e-210">HMAC-SHA: SHA1-96, SHA1-160, SHA2-256, SHA2-384, SHA2- 512, authentication and hash computation</span></span>
- <span data-ttu-id="2f02e-211">MD5: autenticazione</span><span class="sxs-lookup"><span data-stu-id="2f02e-211">MD5: authentication</span></span>
- <span data-ttu-id="2f02e-212">Funzione pseudo-random (PRF): PRF_HMAC_SHA1 e PRF_HMAC_SHA2-256</span><span class="sxs-lookup"><span data-stu-id="2f02e-212">Pseudo-random Function (PRF): PRF_HMAC_SHA1 and PRF_HMAC_SHA2-256</span></span>
- <span data-ttu-id="2f02e-213">RSA: 1024-, 2048-, operazione RSA di Power-Modul a 4096 bit</span><span class="sxs-lookup"><span data-stu-id="2f02e-213">RSA: 1024-, 2048-, 4096-bit RSA power-modulus operation</span></span>
- <span data-ttu-id="2f02e-214">SHA: SHA1 (96-and 160-bit), SHA2 (256bit, 384bit, 512bit) Authentication</span><span class="sxs-lookup"><span data-stu-id="2f02e-214">SHA: SHA1 (96- and 160-bit), SHA2 (256bit, 384bit, 512bit) authentication</span></span>

<span data-ttu-id="2f02e-215">Questa funzione include i vettori predefiniti per gli algoritmi di crittografia elencati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-215">This function has the built-in vectors for the crypto algorithms listed above.</span></span> <span data-ttu-id="2f02e-216">Tuttavia, verifica solo quelli elencati nell' *cipher_table* passati a questa funzione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-216">However it only tests the ones listed in the *cipher_table* passed into this function.</span></span> <span data-ttu-id="2f02e-217">Ad esempio, per una sessione TLS usa solo la TLS_RSA_WITH_AES_128_CBC_SHA ciphersuite, questa funzione eseguirà il test automatico su RSA (1024-, 2048-, 4096-bit), AES-CBC (128 bit) e SHA1.</span><span class="sxs-lookup"><span data-stu-id="2f02e-217">For example, for a TLS session uses only the ciphersuite TLS_RSA_WITH_AES_128_CBC_SHA, this function will perform self test on the RSA (1024-, 2048-, 4096-bit), AES-CBC (128-bit) and SHA1.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-218">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-218">Parameters</span></span>

- <span data-ttu-id="2f02e-219">**crypto_table** Puntatore alla tabella Crypto utilizzata dalla sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-219">**crypto_table** Pointer to the crypto table being used by the TLS session.</span></span> <span data-ttu-id="2f02e-220">Si tratta dello stesso crypto_table passato nella chiamata **_nx_secure_tls_session_create ()_** .</span><span class="sxs-lookup"><span data-stu-id="2f02e-220">This is the same crypto_table being passed into the **_nx_secure_tls_session_create()_** call.</span></span>
- <span data-ttu-id="2f02e-221">**metadati** di Puntatore allo spazio per l'area dei metadati di crittografia.</span><span class="sxs-lookup"><span data-stu-id="2f02e-221">**metadata** Pointer to space for cryptography metadata area.</span></span> <span data-ttu-id="2f02e-222">.</span><span class="sxs-lookup"><span data-stu-id="2f02e-222">.</span></span>
- <span data-ttu-id="2f02e-223">**metadata_size** Dimensioni del buffer dei metadati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-223">**metadata_size** Size of the metadata buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-224">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-224">Return Values</span></span>

- <span data-ttu-id="2f02e-225">**NX_SECURE_TLS_SUCCESS** (0x00) ha testato correttamente i metodi di crittografia forniti.</span><span class="sxs-lookup"><span data-stu-id="2f02e-225">**NX_SECURE_TLS_SUCCESS** (0x00) Successfully tested the crypto methods provided.</span></span>
- <span data-ttu-id="2f02e-226">Struttura del metodo Crypto **NX_PTR_ERROR** (0x07) non valida</span><span class="sxs-lookup"><span data-stu-id="2f02e-226">**NX_PTR_ERROR** (0x07) Invalid crypto method structure</span></span>
- <span data-ttu-id="2f02e-227">**NX_NOT_SUCCESSFUL** (0X43) Crypto self test ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="2f02e-227">**NX_NOT_SUCCESSFUL** (0x43) Crypto self test fails.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-228">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-228">Allowed From</span></span>

<span data-ttu-id="2f02e-229">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-229">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-230">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-230">Example</span></span>

```C
/* crypto_tls_ciphers is the cipher table for the TLS session. */
/* metadata_buffer is the memory area used by the cipher functions. */

/* The following function verifies the supplied ciphersuties using the built-in
   self test. */

if (nx_secure_crypto_table_self_test(&crypto_tls_ciphers, metadata_buffer,
    sizeof(metadata_buffer)))
{
    printf("Crypto self test failed!\r\n");
    exit(0);
}
else
{
    printf("Crypto self test succeed!\r\n");
}

/* Now the ciphersuites are successfully test, it can be used in
   nx_secure_tls_session_create() */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-231">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-231">See Also</span></span>

- <span data-ttu-id="2f02e-232">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-232">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_module_hash_compute"></a><span data-ttu-id="2f02e-233">nx_secure_module_hash_compute</span><span class="sxs-lookup"><span data-stu-id="2f02e-233">nx_secure_module_hash_compute</span></span>

<span data-ttu-id="2f02e-234">Calcola il valore hash utilizzando la funzione hash fornita dall'utente</span><span class="sxs-lookup"><span data-stu-id="2f02e-234">Computes hash value using user-supplied hash function</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-235">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-235">Prototype</span></span>

```C
UINT nx_secure_module_hash_compute(
                      NX_CRYPTO_METHOD *hamc_ptr,
                      UINT start_address, UINT end_address,
                      UCHAR *key, UINT key_length,
                      VOID *metadata, UINT metadata_size,
                      UCHAR *output_buffer, UINT output_buffer_size,
                      UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="2f02e-236">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-236">Description</span></span>

<span data-ttu-id="2f02e-237">Questa funzione calcola il valore hash del flusso di dati nell'area di memoria specificata, usando il metodo crittografico HMAC fornito e la stringa chiave.</span><span class="sxs-lookup"><span data-stu-id="2f02e-237">This function computes the hash value of the data stream in the specified memory area, using supplied HMAC crypto method and the key string.</span></span> <span data-ttu-id="2f02e-238">La funzione di calcolo hash del modulo è disponibile solo se la libreria protetta NetX viene compilata con il simbolo seguente definito: NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK</span><span class="sxs-lookup"><span data-stu-id="2f02e-238">The module hash compute function is available only if NetX Secure library is built with the following symbol being defined: NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-239">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-239">Parameters</span></span>

- <span data-ttu-id="2f02e-240">**hmac_ptr** Puntatore al metodo crittografico HMAC utilizzato per il calcolo del valore hash.</span><span class="sxs-lookup"><span data-stu-id="2f02e-240">**hmac_ptr** Pointer to the HMAC crypto method being used for the hash value computation.</span></span>
- <span data-ttu-id="2f02e-241">**start_address** Indirizzo iniziale del buffer di dati</span><span class="sxs-lookup"><span data-stu-id="2f02e-241">**start_address** The starting address of the data buffer</span></span>
- <span data-ttu-id="2f02e-242">**end_address** Indirizzo finale del buffer di dati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-242">**end_address** The ending address of the data buffer.</span></span> <span data-ttu-id="2f02e-243">Si noti che il calcolo hash non copre i dati in questo end_address.</span><span class="sxs-lookup"><span data-stu-id="2f02e-243">Note that hash computation does not cover the data at this end_address.</span></span>
- <span data-ttu-id="2f02e-244">**chiave** di Stringa chiave utilizzata nel calcolo HMAC.</span><span class="sxs-lookup"><span data-stu-id="2f02e-244">**key** The key string being used in the HMAC computation.</span></span>
- <span data-ttu-id="2f02e-245">**Key_Length** Dimensione della stringa di chiave, in byte</span><span class="sxs-lookup"><span data-stu-id="2f02e-245">**key_length** The size of the key string, in bytes</span></span>
- <span data-ttu-id="2f02e-246">**metadati** di Puntatore allo spazio utilizzato dall'algoritmo HMAC.</span><span class="sxs-lookup"><span data-stu-id="2f02e-246">**metadata** Pointer to space used by the HMAC algorithm.</span></span>
- <span data-ttu-id="2f02e-247">**metadata_size** Dimensioni del buffer dei metadati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-247">**metadata_size** Size of the metadata buffer.</span></span>
- <span data-ttu-id="2f02e-248">**output_buffer** Posizione di memoria in cui viene archiviato l'output hash.</span><span class="sxs-lookup"><span data-stu-id="2f02e-248">**output_buffer** The memory location where the hash output is being stored at.</span></span>
- <span data-ttu-id="2f02e-249">**output_buffer_size** Spazio disponibile del buffer di output, in byte</span><span class="sxs-lookup"><span data-stu-id="2f02e-249">**output_buffer_size** The available space of the output buffer, in bytes</span></span>
- <span data-ttu-id="2f02e-250">**actual_size** Restituito dalla funzione che indica il numero effettivo di byte scritti nell'output_buffer.</span><span class="sxs-lookup"><span data-stu-id="2f02e-250">**actual_size** Returned by the function indicating the actual number of bytes being written into the output_buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-251">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-251">Return Values</span></span>

- <span data-ttu-id="2f02e-252">**0** ha calcolato correttamente il valore hash.</span><span class="sxs-lookup"><span data-stu-id="2f02e-252">**0** Successfully computed the hash value.</span></span>
- <span data-ttu-id="2f02e-253">**1** il calcolo hash non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-253">**1** The hash computation failed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-254">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-254">Allowed From</span></span>

<span data-ttu-id="2f02e-255">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-255">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-256">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-256">Example</span></span>

```C
/* Define the HMAC SHA256 method */
NX_CRYPTO_METHOD hmac_sha256 =
{
    NX_CRYPTO_AUTHENTICATION_HMAC_SHA2_256,    /* HMAC SHA256 algorithm  */
    0,                                         /* Key size, not used     */
    0,                                         /* IV size, not used      */
    NX_CRYPTO_HMAC_SHA256_ICV_FULL_LEN_IN_BITS,/* Transmitted ICV size   */
    NX_CRYPTO_SHA2_BLOCK_SIZE_IN_BYTES,        /* Block size in bytes    */
    sizeof(NX_CRYPTO_SHA256_HMAC),             /* Metadata size in bytes */
    _nx_crypto_method_hmac_sha256_init,        /* HMAC SHA256 init       */
    _nx_crypto_method_hmac_sha256_cleanup,     /* HMAC SHA256 cleanup    */
    _nx_crypto_method_hmac_sha256_operation    /* HMAC SHA256 operation  */
};

/* Define the hash key being used. */
const CHAR hash_key = “my hash key”;

/* Define starting address. */
UINT starting_address = 0x10000;

/* Define the ending address.
   Note that the hash computation covers the memory location
   before the ending address. */
UINT ending_address = 0x11000;

/* Declare the output buffer. */
#define OUTPUT_BUFFER_SIZE
UCHAR output_buffer[OUTPUT_BUFFER_SIZE];

UINT actual_size;

/* Declare 1K bytes of metadata buffer area. */
UCHAR metadata_buffer[1024];

/* Compute the hash value of the data between 0x10000 – 0x10FFF */
nx_secure_module_hash_compute(&hmac_sha256,
                              starting_address, ending_address,
                              hash_key, strlen(hash_key),
                              metadata_buffer, sizeof(metadata_buffer),
                              output_buffer, OUTPUT_BUFFER_SIZE, &actual_size);

/* If this function returns “0”, the hash value has been computed and is stored
   in output_buffer. */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-257">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-257">See Also</span></span>

- <span data-ttu-id="2f02e-258">nx_secure_crypto_method_self_test</span><span class="sxs-lookup"><span data-stu-id="2f02e-258">nx_secure_crypto_method_self_test</span></span>

## <a name="nx_secure_tls_active_certificate_set"></a><span data-ttu-id="2f02e-259">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-259">nx_secure_tls_active_certificate_set</span></span>

<span data-ttu-id="2f02e-260">Impostare il certificato di identità attivo per una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-260">Set the active identity certificate for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-261">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-261">Prototype</span></span>

```C
UINT  nx_secure_tls_active_certificate_set(
                   NX_SECURE_TLS_SESSION *tls_session,
                   NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a><span data-ttu-id="2f02e-262">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-262">Description</span></span>

<span data-ttu-id="2f02e-263">Questo servizio è destinato a essere chiamato dall'interno di un callback di sessione (vedere nx_secure_tls_session_client_callback_set e nx_secure_tls_session_server_callback_set).</span><span class="sxs-lookup"><span data-stu-id="2f02e-263">This service is intended to be called from within a session callback (see nx_secure_tls_session_client_callback_set and nx_secure_tls_session_server_callback_set).</span></span> <span data-ttu-id="2f02e-264">Quando viene chiamato con una struttura di NX_SECURE_X509_CERT inizializzata in precedenza, il certificato verrà usato al posto del certificato di identità predefinito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-264">When called with a previously-initialized NX_SECURE_X509_CERT structure, that certificate will be used instead of the default identity certificate.</span></span> <span data-ttu-id="2f02e-265">Nella maggior parte dei casi, il certificato deve essere stato aggiunto all'archivio locale (vedere nx_secure_tls_local_certificate_add) o l'handshake TLS potrebbe non riuscire.</span><span class="sxs-lookup"><span data-stu-id="2f02e-265">In most cases, the certificate must have been added to the local store (see nx_secure_tls_local_certificate_add) or the TLS handshake may fail.</span></span>

<span data-ttu-id="2f02e-266">Questo servizio è progettato per consentire a TLS di supportare più certificati di identità.</span><span class="sxs-lookup"><span data-stu-id="2f02e-266">This service is intended to allow TLS to support multiple identity certificates.</span></span> <span data-ttu-id="2f02e-267">Questa operazione è utile per un server TLS che fornisce servizi a più indirizzi di rete in modo che il server possa scegliere un certificato appropriato da fornire al client remoto a seconda del EntryPoint del client.</span><span class="sxs-lookup"><span data-stu-id="2f02e-267">This is useful for a TLS server that services multiple network addresses so the server can pick an appropriate certificate to provide to the remote client depending on the client's entrypoint.</span></span> <span data-ttu-id="2f02e-268">Per un client TLS, questa routine può essere usata per modificare il certificato inviato a un server remoto in fase di esecuzione dopo che il server è stato identificato nell'handshake TLS (questo è più raro del caso d'uso del server TLS).</span><span class="sxs-lookup"><span data-stu-id="2f02e-268">For a TLS client, this routine may be used to change the certificate sent to a remote server at runtime after the server has identified itself in the TLS handshake (this is more rare than the TLS server use-case).</span></span>

<span data-ttu-id="2f02e-269">Nel caso in cui più certificati possano condividere lo stesso nome distinto X. 509, è necessario aggiungere i certificati utilizzando nx_secure_tls_server_certificate_add, che introduce un identificatore numerico separato dal certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-269">In the case where multiple certificates may share the same X.509 distinguished name, certificates will need to be added using nx_secure_tls_server_certificate_add, which introduces a numeric identifier separate from the certificate.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-270">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-270">Parameters</span></span>

- <span data-ttu-id="2f02e-271">**session_ptr** Puntatore a un'istanza della sessione TLS passata al callback della sessione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-271">**session_ptr** Pointer to a TLS Session instance passed into the session callback.</span></span>
- <span data-ttu-id="2f02e-272">**certificato** di Puntatore a un certificato X. 509 inizializzato da utilizzare per la sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="2f02e-272">**certificate** Pointer to an initialized X.509 certificate that is to be used for the current session.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-273">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-273">Return Values</span></span>

- <span data-ttu-id="2f02e-274">**NX_SUCCESS** (0x00) assegnazione del certificato alla sessione completata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-274">**NX_SUCCESS** (0x00) Successful assignment of certificate to session.</span></span>
- <span data-ttu-id="2f02e-275">**NX_PTR_ERROR** (0x07) la sessione TLS o il puntatore al certificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-275">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-276">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-276">Allowed From</span></span>

<span data-ttu-id="2f02e-277">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-277">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-278">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-278">Example</span></span>

```C
#define TLS_SNI_SERVER_NAME “www.example.com”
#define TLS_DEFAULT_SERVER_CERT_ID 2
#define TLS_EXAMPLE_CERT_ID 3


/* Callback for ClientHello extensions processing. */
static ULONG tls_server_callback(NX_SECURE_TLS_SESSION *tls_session,
                                 NX_SECURE_TLS_HELLO_EXTENSION *extensions,
                                 UINT num_extensions)
{
NX_SECURE_X509_DNS_NAME dns_name;
INT compare_value;
UINT status;
NX_SECURE_X509_CERT *cert_ptr;

    /* Grab a pointer to our default certificate in case the SNI extension is not
       available or the specified server name is unknown. */
    nx_secure_tls_server_certificate_find(tls_session, &cert_ptr,
                                     TLS_DEFAULT_SERVER_CERT_ID);


    /* Process Server Name Indication extension. */
    status = _nx_secure_tls_session_sni_extension_parse(tls_session, extensions,
                                                    num_extensions, &dns_name);

    /* If no extension found, that is OK. Use default certificate. */
    if(status == NX_SUCCESS)
    {
          /* SNI extension found, select an active certificate based on the server
             name. */

          /* Make sure our SNI name matches. */
          compare_value = memcmp(dns_name.nx_secure_x509_dns_name,
                                TLS_SNI_SERVER_NAME, strlen(TLS_SNI_SERVER_NAME));

          if(compare_value == 0 && dns_name.nx_secure_x509_dns_name_length !=
             strlen(TLS_SNI_SERVER_NAME))
          {
             /* Found a match, find the certificate we want to use. */
             _nx_secure_tls_server_certificate_find(tls_session, &cert_ptr,
                                                      TLS_EXAMPLE_CERT_ID);
          }
          else
          {
             /* No matching server name found. The application may choose to simply
                provide the default certificate (and probably resulting in an error
                in the remote client) or returning an error here to end the
                handshake. A user-defined non-zero error code will be sufficient –
                the error code will abort the TLS handshake and be returned to the
                caller that started the server. */
                return(0x500);
          }
      }
      else
      {
      }
      /* Set the certificate we want to use. */
      nx_secure_tls_active_certificate_set(tls_session, cert_ptr);

      /* Return success to continue TLS handshake. */
      return(NX_SUCCESS);
}

/* Sockets, sessions, certificates defined in global static space to preserve
   application stack. */
NX_SECURE_TLS_SESSION server_tls_session;

/* Application where TLS session is started. */
void main()
{
    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_tls_session_create(&server_tls_session,
                                           &nx_crypto_tls_ciphers,
                                           server_crypto_metadata,
                                           sizeof(server_crypto_metadata));

    /* Check for error.  */
    if(status)
    {
        printf("Error in function nx_secure_tls_session_create: 0x%x\n", status);
    }

    /* Setup our packet reassembly buffer. See
       nx_secure_tls_session_packet_buffer_set for more information. */
    nx_secure_tls_session_packet_buffer_set(&server_tls_session,
                                      server_packet_buffer,
                                      sizeof(server_packet_buffer));


    /* Set callback for server TLS extension handling. */
    _nx_secure_tls_session_server_callback_set(&server_tls_session,
                                              tls_server_callback);

    /* Initialize our certificates – certificate data defined elsewhere. See
       section “Importing X.509 Certificates into NetX Secure” for more
       information. */
    nx_secure_x509_certificate_initialize(&default_certificate,
                                      default_cert_der,
                                      default _cert_der_len, NX_NULL, 0,
                                      default_cert_key_der,
                                      default_cert_key_der_len,
                                      NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_tls_server_certificate_add(&server_tls_session,
                                         &default_certificate,
                                         TLS_DEFAULT_SERVER_CERT_ID);

    /* Alternative identity certificate, needs to have a private key! */
    nx_secure_x509_certificate_initialize(&example_certificate,
                                      example_cert_der,
                                      example cert_der_len, NX_NULL, 0,
                                      example_cert_key_der,
                                      example_cert_key_der_len,
                                      NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);

    /* Add the certificate to the local store using a numeric ID. */
    nx_secure_tls_server_certificate_add(&server_tls_session,
                                         &example_certificate,
                                         TLS_EXAMPLE_CERT_ID);

    /* Now we can start the TLS session as normal. */
       …
}
```

### <a name="see-also"></a><span data-ttu-id="2f02e-279">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-279">See Also</span></span>

- <span data-ttu-id="2f02e-280">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-280">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-281">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-281">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="2f02e-282">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-282">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="2f02e-283">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-283">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="2f02e-284">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-284">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="2f02e-285">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-285">nx_secure_tls_server_certificate_find</span></span>
- <span data-ttu-id="2f02e-286">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-286">nx_secure_tls_server_certificate_remove</span></span>

## <a name="nx_secure_tls_client_psk_set"></a><span data-ttu-id="2f02e-287">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-287">nx_secure_tls_client_psk_set</span></span>

<span data-ttu-id="2f02e-288">Impostare una chiave precondivisa per una sessione client TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-288">Set a Pre-Shared Key for a NetX Secure TLS Client Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-289">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-289">Prototype</span></span>

```C
UINT  nx_secure_tls_client_psk_set(NX_SECURE_TLS_SESSION *session_ptr,
                              UCHAR *pre_shared_key, UINT psk_length,
                              UCHAR *psk_identity, UINT identity_length,
                              UCHAR *hint, UINT hint_length);
```

### <a name="description"></a><span data-ttu-id="2f02e-290">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-290">Description</span></span>

<span data-ttu-id="2f02e-291">Questo servizio aggiunge una chiave precondivisa (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo della sessione TLS e imposta tale PSK da usare nelle connessioni client TLS successive.</span><span class="sxs-lookup"><span data-stu-id="2f02e-291">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a TLS Session control block, and sets that PSK to be used in subsequent TLS Client connections.</span></span> <span data-ttu-id="2f02e-292">Il valore PSK viene usato al posto di un certificato digitale quando si Abilita e si usa PSK ciphersuites.</span><span class="sxs-lookup"><span data-stu-id="2f02e-292">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

<span data-ttu-id="2f02e-293">In questo caso, la PSK è associata a un server TLS remoto specifico con cui il client TLS desidera comunicare.</span><span class="sxs-lookup"><span data-stu-id="2f02e-293">In this case, the PSK is associated with a specific remote TLS Server with which the TLS Client wishes to communicate.</span></span> <span data-ttu-id="2f02e-294">Il set di PSK tramite questa API verrà fornito all'host del server TLS remoto durante il successivo handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-294">The PSK set through this API will be provided to the remote TLS Server host during the next TLS handshake.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-295">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-295">Parameters</span></span>

- <span data-ttu-id="2f02e-296">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-296">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-297">**pre_shared_key** Valore PSK effettivo.</span><span class="sxs-lookup"><span data-stu-id="2f02e-297">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="2f02e-298">**psk_length** Lunghezza del valore PSK.</span><span class="sxs-lookup"><span data-stu-id="2f02e-298">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="2f02e-299">**psk_identity** Stringa utilizzata per identificare il valore PSK.</span><span class="sxs-lookup"><span data-stu-id="2f02e-299">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="2f02e-300">**identity_length** Lunghezza dell'identità PSK.</span><span class="sxs-lookup"><span data-stu-id="2f02e-300">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="2f02e-301">**hint** Stringa utilizzata per indicare il gruppo di precondivise da scegliere in un server TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-301">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="2f02e-302">**hint_length** Lunghezza della stringa del suggerimento.</span><span class="sxs-lookup"><span data-stu-id="2f02e-302">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-303">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-303">Return Values</span></span>

- <span data-ttu-id="2f02e-304">L'aggiunta di PSK è stata completata **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="2f02e-304">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="2f02e-305">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-305">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="2f02e-306">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0X125) non è in grado di aggiungere un'altra PSK.</span><span class="sxs-lookup"><span data-stu-id="2f02e-306">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-307">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-307">Allowed From</span></span>

<span data-ttu-id="2f02e-308">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-308">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-309">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-309">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_client_psk_set(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-310">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-310">See Also</span></span>

- <span data-ttu-id="2f02e-311">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-311">nx_secure_tls_psk_add</span></span>
- <span data-ttu-id="2f02e-312">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-312">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-313">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-313">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-314">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-314">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-315">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-315">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_initialize"></a><span data-ttu-id="2f02e-316">nx_secure_tls_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-316">nx_secure_tls_initialize</span></span>

<span data-ttu-id="2f02e-317">Inizializza il modulo TLS sicuro NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-317">Initializes the NetX Secure TLS module</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-318">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-318">Prototype</span></span>

```C
VOID nx_secure_tls_initialize(VOID);
```

### <a name="description"></a><span data-ttu-id="2f02e-319">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-319">Description</span></span>

<span data-ttu-id="2f02e-320">Questo servizio Inizializza il modulo TLS sicuro NetX.</span><span class="sxs-lookup"><span data-stu-id="2f02e-320">This service initializes the NetX Secure TLS module.</span></span> <span data-ttu-id="2f02e-321">Deve essere chiamato prima che sia possibile accedere ad altri servizi NetX Secure.</span><span class="sxs-lookup"><span data-stu-id="2f02e-321">It must be called before other NetX Secure services can be accessed.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-322">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-322">Parameters</span></span>

<span data-ttu-id="2f02e-323">nessuno</span><span class="sxs-lookup"><span data-stu-id="2f02e-323">None</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-324">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-324">Return Values</span></span>

<span data-ttu-id="2f02e-325">nessuno</span><span class="sxs-lookup"><span data-stu-id="2f02e-325">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-326">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-326">Allowed From</span></span>

<span data-ttu-id="2f02e-327">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-327">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-328">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-328">Example</span></span>

```C
/* Initializes the TLS module. */
Nx_secure_tls_initialize();
```

### <a name="see-also"></a><span data-ttu-id="2f02e-329">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-329">See Also</span></span>

- <span data-ttu-id="2f02e-330">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-330">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_local_certificate_add"></a><span data-ttu-id="2f02e-331">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-331">nx_secure_tls_local_certificate_add</span></span>

<span data-ttu-id="2f02e-332">Aggiungere un certificato locale a una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-332">Add a local certificate to NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-333">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-333">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_add(
              NX_SECURE_TLS_SESSION *session_ptr,
              NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a><span data-ttu-id="2f02e-334">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-334">Description</span></span>

<span data-ttu-id="2f02e-335">Questo servizio aggiunge un'istanza della struttura NX_SECURE_X509_CERT inizializzata all'archivio locale di una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-335">This service adds an initialized NX_SECURE_X509_CERT structure instance to the local store of a TLS session.</span></span> <span data-ttu-id="2f02e-336">Questo certificato può essere usato dallo stack TLS per identificare il dispositivo durante l'handshake TLS (se è stato contrassegnato come certificato di identità durante l'inizializzazione della struttura del certificato usando nx_secure_x509_certificate_initialize) o come emittente come parte di una catena di certificati fornita all'host remoto durante l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-336">This certificate may used by the TLS stack to identify the device during the TLS handshake (if it was marked as an identity certificate during initialization of the certificate structure using nx_secure_x509_certificate_initialize), or as an issuer as part of a certificate chain provided to the remote host during the TLS handshake.</span></span>

<span data-ttu-id="2f02e-337">Se sono necessari più certificati locali con lo stesso nome comune, i certificati possono essere aggiunti usando il servizio *nx_secure_tls_server_certificate_add* (vedere l'avviso riportato di seguito).</span><span class="sxs-lookup"><span data-stu-id="2f02e-337">If multiple local certificates with the same Common Name are needed, certificates may be added using the *nx_secure_tls_server_certificate_add* service (see warning below).</span></span>

<span data-ttu-id="2f02e-338">Per la modalità server TLS è **necessario** un certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-338">A certificate is **required** for TLS Server mode.</span></span>

<span data-ttu-id="2f02e-339">Un certificato è *facoltativo* per la modalità client TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-339">A certificate is *optional* for TLS Client mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f02e-340">*Non usare questa API con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API Certificate Server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add gli indici in base al nome comune X. 509. I servizi certificati locali forniscono una comoda alternativa all'identificatore numerico per le applicazioni che usano solo un singolo certificato di identità: usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-340">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-341">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-341">Parameters</span></span>

- <span data-ttu-id="2f02e-342">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-342">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-343">**certificate_ptr** Puntatore a un'istanza di certificato TLS inizializzata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-343">**certificate_ptr** Pointer to an initialized TLS Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-344">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-344">Return Values</span></span>

- <span data-ttu-id="2f02e-345">Aggiunta del certificato **NX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-345">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="2f02e-346">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) ha tentato di aggiungere un certificato non valido o duplicato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-346">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid or duplicate certificate.</span></span>
- <span data-ttu-id="2f02e-347">**NX_PTR_ERROR** (0x07) la sessione TLS o il puntatore al certificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-347">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-348">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-348">Allowed From</span></span>

<span data-ttu-id="2f02e-349">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-349">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-350">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-350">Example</span></span>

```C
/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-351">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-351">See Also</span></span>

- <span data-ttu-id="2f02e-352">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-352">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-353">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-353">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-354">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-354">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-355">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-355">nx_secure_tls_local_certificate_remove</span></span>
- <span data-ttu-id="2f02e-356">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-356">nx_secure_tls_local_certificate_find</span></span>

## <a name="nx_secure_tls_local_certificate_find"></a><span data-ttu-id="2f02e-357">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-357">nx_secure_tls_local_certificate_find</span></span>

<span data-ttu-id="2f02e-358">Trovare un certificato locale in una sessione TLS sicura NetX per nome comune</span><span class="sxs-lookup"><span data-stu-id="2f02e-358">Find a local certificate in a NetX Secure TLS Session by Common Name</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-359">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-359">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_find(NX_SECURE_TLS_SESSION
                        *session_ptr, NX_SECURE_X509_CERT
                        **certificate, UCHAR *common_name, UINT
                        name_length);
```

### <a name="description"></a><span data-ttu-id="2f02e-360">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-360">Description</span></span>

<span data-ttu-id="2f02e-361">Questo servizio trova un certificato nell'archivio certificati del dispositivo locale di una sessione TLS e restituisce un puntatore alla struttura NX_SECURE_X509_CERT nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="2f02e-361">This service finds a certificate in the local device certificate store of a TLS session and returns a pointer to the NX_SECURE_X509_CERT structure in the store.</span></span> <span data-ttu-id="2f02e-362">Il parametro common_name e la lunghezza (name_length) vengono usati per identificare il certificato nell'archivio corrispondente al campo del nome comune del soggetto X. 509 del certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-362">The common_name parameter and it's length (name_length) are used to identify the certificate in the store by matching the certificate's X.509 Subject Common Name field.</span></span>

<span data-ttu-id="2f02e-363">Se è presente più di un certificato con lo stesso nome comune, viene restituito solo il primo: usare *nx_secure_tls_server_certificate_find* .</span><span class="sxs-lookup"><span data-stu-id="2f02e-363">If more than one certificate with the same Common Name is present, only the first one will be returned – use *nx_secure_tls_server_certificate_find* instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f02e-364">*Non usare questa API con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API Certificate Server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add gli indici in base al nome comune X. 509. I servizi certificati locali forniscono una comoda alternativa all'identificatore numerico per le applicazioni che usano solo un singolo certificato di identità: usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-364">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-365">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-365">Parameters</span></span>

- <span data-ttu-id="2f02e-366">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-366">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-367">**certificato** di Restituisce il puntatore al certificato corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2f02e-367">**certificate** Return Pointer to matched certificate.</span></span>
- <span data-ttu-id="2f02e-368">**common_name** Stringa del nome comune da confrontare (nome DNS).</span><span class="sxs-lookup"><span data-stu-id="2f02e-368">**common_name** Common Name string to match (DNS name).</span></span>
- <span data-ttu-id="2f02e-369">**name_length** Lunghezza dei dati della stringa common_name.</span><span class="sxs-lookup"><span data-stu-id="2f02e-369">**name_length** Length of common_name string data.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-370">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-370">Return Values</span></span>

- <span data-ttu-id="2f02e-371">È stato trovato il certificato **NX_SUCCESS** (0x00) e il puntatore è stato restituito nel parametro "Certificate".</span><span class="sxs-lookup"><span data-stu-id="2f02e-371">**NX_SUCCESS** (0x00) Certificate was found and pointer returned in "certificate" parameter.</span></span>
- <span data-ttu-id="2f02e-372">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0X119) non è stato trovato alcun certificato con il nome comune fornito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-372">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate with the supplied Common Name was found.</span></span>
- <span data-ttu-id="2f02e-373">**NX_PTR_ERROR** (0x07) una sessione TLS non valida, un puntatore al certificato o una stringa del nome comune.</span><span class="sxs-lookup"><span data-stu-id="2f02e-373">**NX_PTR_ERROR** (0x07) Invalid TLS session, certificate pointer, or common name string.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-374">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-374">Allowed From</span></span>

<span data-ttu-id="2f02e-375">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-375">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-376">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-376">Example</span></span>

```C
NX_SECURE_X509_CERT *certificate_ptr;

/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */

status = nx_secure_tls_local_certificate_find(&tls_session, &certificate_ptr,
                                      “common name”, strlen(“common name”));

/* If status is NX_SUCCESS the variable “certificate_ptr” points to a certificate
   structure containing a certificate with the Common Name “common name”. */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-377">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-377">See Also</span></span>

- <span data-ttu-id="2f02e-378">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-378">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-379">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-379">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-380">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-380">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-381">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-381">nx_secure_tls_local_certificate_remove</span></span>
- <span data-ttu-id="2f02e-382">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-382">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_local_certificate_remove"></a><span data-ttu-id="2f02e-383">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-383">nx_secure_tls_local_certificate_remove</span></span>

<span data-ttu-id="2f02e-384">Rimuovere il certificato locale dalla sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-384">Remove local certificate from NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-385">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-385">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_remove(NX_SECURE_TLS_SESSION
                  *session_ptr, UCHAR *common_name, UINT
                  common_name_length);
```

### <a name="description"></a><span data-ttu-id="2f02e-386">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-386">Description</span></span>

<span data-ttu-id="2f02e-387">Questo servizio rimuove un'istanza del certificato locale da una sessione TLS, con chiave nel campo del nome comune nel certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-387">This service removes a local certificate instance from a TLS session, keyed on the Common Name field in the certificate.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f02e-388">*Non usare questa API con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API Certificate Server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add gli indici in base al nome comune X. 509. I servizi certificati locali forniscono una comoda alternativa all'identificatore numerico per le applicazioni che usano solo un singolo certificato di identità: usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-388">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-389">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-389">Parameters</span></span>

- <span data-ttu-id="2f02e-390">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-390">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-391">**common_name** Valore del nome comune del certificato da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="2f02e-391">**common_name** The Common Name value of the certificate to be removed.</span></span>
- <span data-ttu-id="2f02e-392">**common_name_length** Lunghezza della stringa del nome comune.</span><span class="sxs-lookup"><span data-stu-id="2f02e-392">**common_name_length** The length of the Common Name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-393">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-393">Return Values</span></span>

- <span data-ttu-id="2f02e-394">Aggiunta del certificato **NX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-394">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="2f02e-395">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-395">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="2f02e-396">Il certificato **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-396">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Certificate was not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-397">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-397">Allowed From</span></span>

<span data-ttu-id="2f02e-398">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-398">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-399">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-399">Example</span></span>

```C
/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-400">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-400">See Also</span></span>

- <span data-ttu-id="2f02e-401">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-401">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-402">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-402">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-403">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-403">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-404">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-404">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_metadata_size_calculate"></a><span data-ttu-id="2f02e-405">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="2f02e-405">nx_secure_tls_metadata_size_calculate</span></span>

<span data-ttu-id="2f02e-406">Calcolo delle dimensioni dei metadati crittografici per una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-406">Calculate size of cryptographic metadata for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-407">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-407">Prototype</span></span>

```C
UINT  nx_secure_tls_metadata_size_calculate(
                        const NX_SECURE_TLS_CRYPTO *crypto_table,
                        ULONG *metadata_size);
```

### <a name="description"></a><span data-ttu-id="2f02e-408">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-408">Description</span></span>

<span data-ttu-id="2f02e-409">Questo servizio calcola e restituisce le dimensioni dei metadati di crittografia necessari per una determinata sessione TLS e una tabella di crittografia TLS (vedere la sezione "inizializzazione di TLS con i metodi di crittografia" per ulteriori informazioni sulla tabella di crittografia crittografica).</span><span class="sxs-lookup"><span data-stu-id="2f02e-409">This service calculates and returns the size of the cryptographic metadata needed for a particular TLS session and TLS cryptography table (see the section "Initializing TLS with Cryptographic Methods" for more information on the cryptographic cipher table).</span></span>

<span data-ttu-id="2f02e-410">Questo servizio deve essere chiamato con la tabella di crittografia desiderata per calcolare le dimensioni del buffer dei metadati passato in nx_secure_tls_session_create.</span><span class="sxs-lookup"><span data-stu-id="2f02e-410">This service should be called with the desired cryptographic table to calculate the size of the metadata buffer passed into nx_secure_tls_session_create.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-411">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-411">Parameters</span></span>

- <span data-ttu-id="2f02e-412">**crypto_table** Puntatore a una tabella di crittografia TLS protetta NetX completa.</span><span class="sxs-lookup"><span data-stu-id="2f02e-412">**crypto_table** Pointer to a complete NetX Secure TLS cryptography table.</span></span>
- <span data-ttu-id="2f02e-413">**metadata_size** Output del calcolo delle dimensioni in byte.</span><span class="sxs-lookup"><span data-stu-id="2f02e-413">**metadata_size** The output of the size calculation in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-414">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-414">Return Values</span></span>

- <span data-ttu-id="2f02e-415">**NX_SUCCESS** (0x00) il calcolo delle dimensioni dei metadati è riuscito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-415">**NX_SUCCESS** (0x00) Successful calculation of metadata size.</span></span>
- <span data-ttu-id="2f02e-416">**NX_PTR_ERROR** (0x07) tabella di crittografia o puntatore alla dimensione restituito non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-416">**NX_PTR_ERROR** (0x07) Invalid crypto table or return size pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-417">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-417">Allowed From</span></span>

<span data-ttu-id="2f02e-418">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-418">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-419">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-419">Example</span></span>

```C
/* Pointer to the platform-specific cipher table. */
extern nx_crypto_tls_ciphers;

/* Return variable for metadata size. */
ULONG crypto_metadata_size;

/* Calculate metadata size.  */
status =  nx_secure_tls_metadata_size_calculate(&nx_crypto_tls_ciphers,
                                                &crypto_metadata_size);


/* If status is NX_SUCCESS then crypto_metadata_size contains the size of the
   metadata buffer for the table nx_crypto_tls_ciphers.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-420">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-420">See Also</span></span>

- <span data-ttu-id="2f02e-421">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-421">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_module_hash_compute"></a><span data-ttu-id="2f02e-422">nx_secure_module_hash_compute</span><span class="sxs-lookup"><span data-stu-id="2f02e-422">nx_secure_module_hash_compute</span></span>

<span data-ttu-id="2f02e-423">Calcola il valore hash delle routine della libreria protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-423">Compute the hash value of the NetX Secure library routines</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-424">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-424">Prototype</span></span>

```C
VOID nx_secure_module_hash_compute(VOID);
```

### <a name="description"></a><span data-ttu-id="2f02e-425">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-425">Description</span></span>

<span data-ttu-id="2f02e-426">Questo servizio Inizializza il modulo TLS sicuro NetX.</span><span class="sxs-lookup"><span data-stu-id="2f02e-426">This service initializes the NetX Secure TLS module.</span></span> <span data-ttu-id="2f02e-427">Deve essere chiamato prima che sia possibile accedere ad altri servizi NetX Secure.</span><span class="sxs-lookup"><span data-stu-id="2f02e-427">It must be called before other NetX Secure services can be accessed.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-428">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-428">Parameters</span></span>

<span data-ttu-id="2f02e-429">nessuno</span><span class="sxs-lookup"><span data-stu-id="2f02e-429">None</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-430">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-430">Return Values</span></span>

<span data-ttu-id="2f02e-431">nessuno</span><span class="sxs-lookup"><span data-stu-id="2f02e-431">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-432">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-432">Allowed From</span></span>

<span data-ttu-id="2f02e-433">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-433">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-434">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-434">Example</span></span>

```C
/* Initializes the TLS module. */
Nx_secure_tls_initialize();
```

### <a name="see-also"></a><span data-ttu-id="2f02e-435">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-435">See Also</span></span>

- <span data-ttu-id="2f02e-436">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-436">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_packet_allocate"></a><span data-ttu-id="2f02e-437">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-437">nx_secure_tls_packet_allocate</span></span>

<span data-ttu-id="2f02e-438">Allocare un pacchetto per una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-438">Allocate a packet for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-439">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-439">Prototype</span></span>

```C
UINT  nx_secure_tls_packet_allocate(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET_POOL *pool_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="2f02e-440">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-440">Description</span></span>

<span data-ttu-id="2f02e-441">Questo servizio alloca un NX_PACKET per la sessione TLS attiva specificata dalla NX_PACKET_POOL specificata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-441">This service allocates an NX_PACKET for the specified active TLS session from the specified NX_PACKET_POOL.</span></span> <span data-ttu-id="2f02e-442">Questo servizio deve essere chiamato dall'applicazione per allocare i pacchetti di dati da inviare tramite una connessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-442">This service should be called by the application to allocate data packets to be sent over a TLS connection.</span></span> <span data-ttu-id="2f02e-443">È necessario inizializzare la sessione TLS prima di chiamare il servizio.</span><span class="sxs-lookup"><span data-stu-id="2f02e-443">The TLS session must be initialized before calling this service.</span></span>

<span data-ttu-id="2f02e-444">Il pacchetto allocato è stato inizializzato correttamente in modo che i dati di intestazione e piè di pagina TLS possano essere aggiunti dopo il popolamento dei dati del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-444">The allocated packet is properly initialized so that TLS header and footer data may be added after the packet data is populated.</span></span> <span data-ttu-id="2f02e-445">In caso contrario, il comportamento è identico a *nx_packet_allocate*.</span><span class="sxs-lookup"><span data-stu-id="2f02e-445">The behavior is otherwise identical to *nx_packet_allocate*.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-446">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-446">Parameters</span></span>

- <span data-ttu-id="2f02e-447">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-447">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-448">**pool_ptr** Puntatore a un NX_PACKET_POOL da cui allocare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-448">**pool_ptr** Pointer to an NX_PACKET_POOL from which to allocate the packet.</span></span>
- <span data-ttu-id="2f02e-449">**packet_ptr** Puntatore di output al pacchetto appena allocato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-449">**packet_ptr** Output pointer to the newly-allocated packet.</span></span>
- <span data-ttu-id="2f02e-450">**WAIT_OPTION** Opzione di sospensione per l'allocazione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2f02e-450">**wait_option** Suspension option for packet allocation.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-451">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-451">Return Values</span></span>

- <span data-ttu-id="2f02e-452">**NX_SUCCESS** (0x00) allocare il pacchetto correttamente.</span><span class="sxs-lookup"><span data-stu-id="2f02e-452">**NX_SUCCESS** (0x00) Successful packet allocate.</span></span>
- <span data-ttu-id="2f02e-453">L'allocazione del pacchetto sottostante **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-453">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Underlying packet allocation failed.</span></span>
- <span data-ttu-id="2f02e-454">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0X101) la sessione TLS specificata non è stata inizializzata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-454">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-455">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-455">Allowed From</span></span>

<span data-ttu-id="2f02e-456">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-456">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-457">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-457">Example</span></span>

```C
/* Allocate a new TLS packet from the previously created packet pool and
previously initialized TLS session.   */

status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &packet_ptr,
                                       NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
variable packet_ptr.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-458">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-458">See Also</span></span>

- <span data-ttu-id="2f02e-459">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-459">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="2f02e-460">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-460">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-461">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-461">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-462">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-462">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-463">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-463">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="2f02e-464">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-464">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="2f02e-465">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-465">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="2f02e-466">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="2f02e-466">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="2f02e-467">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-467">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_psk_add"></a><span data-ttu-id="2f02e-468">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-468">nx_secure_tls_psk_add</span></span>

<span data-ttu-id="2f02e-469">Aggiungere una chiave precondivisa a una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-469">Add a Pre-Shared Key to a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-470">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-470">Prototype</span></span>

```C
UINT  nx_secure_tls_psk_add(NX_SECURE_TLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a><span data-ttu-id="2f02e-471">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-471">Description</span></span>

<span data-ttu-id="2f02e-472">Questo servizio aggiunge una chiave precondivisa (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-472">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a TLS Session control block.</span></span> <span data-ttu-id="2f02e-473">Il valore PSK viene usato al posto di un certificato digitale quando si Abilita e si usa PSK ciphersuites.</span><span class="sxs-lookup"><span data-stu-id="2f02e-473">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-474">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-474">Parameters</span></span>

- <span data-ttu-id="2f02e-475">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-475">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-476">**pre_shared_key** Valore PSK effettivo.</span><span class="sxs-lookup"><span data-stu-id="2f02e-476">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="2f02e-477">**psk_length** Lunghezza del valore PSK.</span><span class="sxs-lookup"><span data-stu-id="2f02e-477">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="2f02e-478">**psk_identity** Stringa utilizzata per identificare il valore PSK.</span><span class="sxs-lookup"><span data-stu-id="2f02e-478">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="2f02e-479">**identity_length** Lunghezza dell'identità PSK.</span><span class="sxs-lookup"><span data-stu-id="2f02e-479">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="2f02e-480">**hint** Stringa utilizzata per indicare il gruppo di precondivise da scegliere in un server TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-480">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="2f02e-481">**hint_length** Lunghezza della stringa del suggerimento.</span><span class="sxs-lookup"><span data-stu-id="2f02e-481">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-482">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-482">Return Values</span></span>

- <span data-ttu-id="2f02e-483">L'aggiunta di PSK è stata completata **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="2f02e-483">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="2f02e-484">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-484">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="2f02e-485">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0X125) non è in grado di aggiungere un'altra PSK.</span><span class="sxs-lookup"><span data-stu-id="2f02e-485">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125)  Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-486">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-486">Allowed From</span></span>

<span data-ttu-id="2f02e-487">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-487">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-488">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-488">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_psk_add(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-489">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-489">See Also</span></span>

- <span data-ttu-id="2f02e-490">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-490">nx_secure_tls_client_psk_set</span></span>
- <span data-ttu-id="2f02e-491">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-491">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-492">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-492">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-493">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-493">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-494">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-494">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_remote_certificate_allocate"></a><span data-ttu-id="2f02e-495">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-495">nx_secure_tls_remote_certificate_allocate</span></span>

<span data-ttu-id="2f02e-496">Alloca spazio per il certificato fornito da un host TLS remoto</span><span class="sxs-lookup"><span data-stu-id="2f02e-496">Allocate space for the certificate provided by a remote TLS host</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-497">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-497">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_allocate(
                 NX_SECURE_TLS_SESSION *session_ptr,
                 NX_SECURE_X509_CERT *certificate_ptr,
                 UCHAR *raw_certificate_buffer,
                 UINT raw_buffer_size);
```

### <a name="description"></a><span data-ttu-id="2f02e-498">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-498">Description</span></span>

<span data-ttu-id="2f02e-499">Questo servizio aggiunge un'istanza di struttura di NX_SECURE_X509_CERT non inizializzata a una sessione TLS allo scopo di allocare spazio per i certificati forniti da un host remoto durante una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-499">This service adds an uninitialized NX_SECURE_X509_CERT structure instance to a TLS session for the purpose of allocating space for certificates provided by a remote host during a TLS session.</span></span> <span data-ttu-id="2f02e-500">I dati del certificato remoto vengono analizzati da NetX Secure TLS e tali informazioni vengono utilizzate per popolare l'istanza della struttura del certificato fornita a questa funzione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-500">The remote certificate data is parsed by NetX Secure TLS and that information is used to populate the certificate structure instance provided to this function.</span></span> <span data-ttu-id="2f02e-501">I certificati aggiunti in questo modo vengono inseriti in un elenco collegato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-501">Certificates added in this manner are placed in a linked list.</span></span>

<span data-ttu-id="2f02e-502">Se si prevede che l'host remoto fornirà più certificati, è necessario chiamare ripetutamente questa funzione per allocare spazio per tutti i certificati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-502">If it is expected that the remote host will provide multiple certificates, this function should be called repeatedly to allocate space for all certificates.</span></span> <span data-ttu-id="2f02e-503">I certificati aggiuntivi vengono aggiunti alla fine dell'elenco collegato al certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-503">The additional certificates are added to the end of the certificate linked list.</span></span>

<span data-ttu-id="2f02e-504">Se non si alloca un certificato remoto, la modalità client TLS avrà esito negativo durante l'handshake TLS a meno che non sia in uso una chiave precondivisa (PSK) ciphersuite.</span><span class="sxs-lookup"><span data-stu-id="2f02e-504">Failure to allocate a remote certificate will cause TLS Client mode to fail during the TLS handshake unless a Pre-Shared Key (PSK) ciphersuite is in use.</span></span>

<span data-ttu-id="2f02e-505">Il parametro *raw_certificate_buffer* punta allo spazio allocato per archiviare il certificato remoto in ingresso.</span><span class="sxs-lookup"><span data-stu-id="2f02e-505">The *raw_certificate_buffer* parameter points to space allocated to store the incoming remote certificate.</span></span> <span data-ttu-id="2f02e-506">I certificati tipici con chiavi RSA di 2048 bit che usano SHA-256 per le firme sono compresi nell'intervallo da 1000-2000 byte.</span><span class="sxs-lookup"><span data-stu-id="2f02e-506">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="2f02e-507">Il buffer deve essere sufficientemente grande da contenere almeno questa dimensione, ma a seconda dei certificati dell'host remoto può essere significativamente più piccolo o più grande.</span><span class="sxs-lookup"><span data-stu-id="2f02e-507">The buffer should be large enough to at least hold that size, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="2f02e-508">Si noti che se il buffer è troppo piccolo per conservare il certificato in ingresso, l'handshake TLS termina con un errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-508">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

<span data-ttu-id="2f02e-509">Per la modalità server TLS, è necessaria un'allocazione di certificati remota solo se è abilitata l'autenticazione del certificato client.</span><span class="sxs-lookup"><span data-stu-id="2f02e-509">For TLS Server mode, a remote certificate allocation is needed only if client certificate authentication is enabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-510">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-510">Parameters</span></span>

- <span data-ttu-id="2f02e-511">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-511">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-512">**certificate_ptr** Puntatore a un'istanza di un certificato X. 509 non inizializzato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-512">**certificate_ptr** Pointer to an uninitialized X.509 Certificate instance.</span></span>
- <span data-ttu-id="2f02e-513">**raw_certificate_buffer** Puntatore a un buffer per contenere il certificato non analizzato ricevuto dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-513">**raw_certificate_buffer** Pointer to a buffer to hold the un-parsed certificate received from the remote host.</span></span>
- <span data-ttu-id="2f02e-514">**raw_buffer_size** Dimensioni del buffer del certificato non elaborato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-514">**raw_buffer_size** Size of the raw certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-515">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-515">Return Values</span></span>

- <span data-ttu-id="2f02e-516">**NX_SUCCESS** (0x00) l'allocazione del certificato è riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-516">**NX_SUCCESS** (0x00) Successful allocation of certificate.</span></span>
- <span data-ttu-id="2f02e-517">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-517">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="2f02e-518">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0X12D) il buffer fornito è troppo piccolo.</span><span class="sxs-lookup"><span data-stu-id="2f02e-518">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="2f02e-519">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) ha tentato di aggiungere un certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-519">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid certificate.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-520">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-520">Allowed From</span></span>

<span data-ttu-id="2f02e-521">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-521">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-522">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-522">Example</span></span>

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;

/* Buffer space to hold the incoming certificate. */
UCHAR certificate_buffer[2000];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_allocate(&tls_session, &certificate,
                                                    certificate_buffer,
                                                    sizeof(certificate_buffer));


/* If status is NX_SUCCESS the certificate was successfully allocated.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-523">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-523">See Also</span></span>

- <span data-ttu-id="2f02e-524">nx_secure_x509_certificate_initialize,</span><span class="sxs-lookup"><span data-stu-id="2f02e-524">nx_secure_x509_certificate_initialize,</span></span>
- <span data-ttu-id="2f02e-525">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-525">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_remote_certificate_buffer_allocate"></a><span data-ttu-id="2f02e-526">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-526">nx_secure_tls_remote_certificate_buffer_allocate</span></span>

<span data-ttu-id="2f02e-527">Alloca spazio per tutti i certificati forniti da un host TLS remoto</span><span class="sxs-lookup"><span data-stu-id="2f02e-527">Allocate space for all certificates provided by a remote TLS host</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-528">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-528">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_buffer_allocate(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="2f02e-529">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-529">Description</span></span>

<span data-ttu-id="2f02e-530">Questo servizio alloca spazio per elaborare le catene di certificati in ingresso dagli host server remoti per eseguire l'autenticazione e la verifica X. 509 in un'istanza client TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-530">This service allocates space to process incoming certificate chains from remote server hosts in order to perform X.509 authentication and verification in a TLS Client instance.</span></span> <span data-ttu-id="2f02e-531">Per la modalità server TLS, l'allocazione di certificati remoti è necessaria solo se è abilitata l'autenticazione del certificato X. 509 del client: per le istanze del server TLS è necessario usare invece il *nx_secure_tls_session_x509_client_verify_configure* di servizio.</span><span class="sxs-lookup"><span data-stu-id="2f02e-531">For TLS Server mode, remote certificate allocation is needed only if client X.509 certificate authentication is enabled – for TLS Server instances the service *nx_secure_tls_session_x509_client_verify_configure* should be used instead.</span></span>

<span data-ttu-id="2f02e-532">Se non si allocano certificati remoti, la modalità client TLS avrà esito negativo durante l'handshake TLS a meno che non sia in uso una chiave precondivisa (PSK) ciphersuite.</span><span class="sxs-lookup"><span data-stu-id="2f02e-532">Failure to allocate remote certificates will cause TLS Client mode to fail during the TLS handshake unless a Pre-Shared Key (PSK) ciphersuite is in use.</span></span>

<span data-ttu-id="2f02e-533">Il parametro *certificate_buffer* punta allo spazio allocato per archiviare i certificati remoti in ingresso e i blocchi di controllo necessari per tali certificati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-533">The *certificate_buffer* parameter points to space allocated to store the incoming remote certificates and the control blocks needed for those certificates.</span></span> <span data-ttu-id="2f02e-534">Il buffer verrà diviso per il numero di certificati (*certs_number*) con una parte uguale assegnata a ogni certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-534">The buffer will be divided by the number of certificates (*certs_number*) with an equal portion given to each certificate.</span></span> <span data-ttu-id="2f02e-535">Il parametro *BUFFER_SIZE*  indica le dimensioni del buffer.</span><span class="sxs-lookup"><span data-stu-id="2f02e-535">The *buffer_size*  parameter indicates the size of the buffer.</span></span> <span data-ttu-id="2f02e-536">È possibile trovare lo spazio necessario con la formula seguente:</span><span class="sxs-lookup"><span data-stu-id="2f02e-536">The space needed can be found with the following formula:</span></span>

```C
buffer_size = (<expected max number of certificates in chain>) *
                 (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

<span data-ttu-id="2f02e-537">I certificati tipici con chiavi RSA di 2048 bit che usano SHA-256 per le firme sono compresi nell'intervallo da 1000-2000 byte.</span><span class="sxs-lookup"><span data-stu-id="2f02e-537">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="2f02e-538">Il buffer deve essere sufficientemente grande da contenere almeno tali dimensioni per ogni certificato, ma a seconda dei certificati dell'host remoto può essere significativamente più piccolo o più grande.</span><span class="sxs-lookup"><span data-stu-id="2f02e-538">The buffer should be large enough to at least hold that size for each certificate, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="2f02e-539">Si noti che se il buffer è troppo piccolo per conservare il certificato in ingresso, l'handshake TLS termina con un errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-539">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-540">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-540">Parameters</span></span>

- <span data-ttu-id="2f02e-541">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-541">**session_ptr** Pointer to a previously created TLS Session  instance.</span></span>
- <span data-ttu-id="2f02e-542">**certs_number** Numero di certificati da allocare dal buffer specificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-542">**certs_number** Number of certificates to allocate from the  provided buffer.</span></span>
- <span data-ttu-id="2f02e-543">**certificate_buffer** Puntatore a un buffer per contenere i certificati ricevuti da un host remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-543">**certificate_buffer** Pointer to a buffer to hold certificates received  from a remote host.</span></span>
- <span data-ttu-id="2f02e-544">**BUFFER_SIZE** Dimensioni del buffer del certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-544">**buffer_size** Size of the certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-545">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-545">Return Values</span></span>

- <span data-ttu-id="2f02e-546">**NX_SUCCESS** (0x00) l'allocazione del certificato è riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-546">**NX_SUCCESS** (0x00) Successful allocation of certificate.</span></span>
- <span data-ttu-id="2f02e-547">**NX_PTR_ERROR** (0x07) la sessione TLS o il puntatore del buffer non è valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-547">**NX_PTR_ERROR** (0x07) Invalid TLS session or buffer pointer.</span></span>
- <span data-ttu-id="2f02e-548">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0X12D) il buffer fornito è troppo piccolo.</span><span class="sxs-lookup"><span data-stu-id="2f02e-548">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="2f02e-549">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) il buffer era troppo piccolo per conservare il numero desiderato di certificati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-549">**NX_INVALID_PARAMETERS** (0x4D) The buffer was too small to hold  the desired number of certificates.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-550">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-550">Allowed From</span></span>

<span data-ttu-id="2f02e-551">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-551">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-552">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-552">Example</span></span>

```C
/* Buffer space to hold the incoming certificates. */
#define CERTIFICATE_NUMBER    (2)
#define CERTIFICATE_SIZE      (2000)
#define BUFFER_SIZE           (CERTIFICATE_NUMBER * \
                              (sizeof(NX_SECURE_X509_CERT) + CERTIFICATE_SIZE))
UCHAR certificate_buffer[BUFFER_SIZE];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_buffer_allocate(&tls_session,
                                                      CERTIFICATE_NUMBER,
                                                      certificate_buffer,
                                                      BUFFER_SIZE);


/* If status is NX_SUCCESS the buffer was successfully allocated.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-553">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-553">See Also</span></span>

- <span data-ttu-id="2f02e-554">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-554">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-555">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-555">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_remote_certificate_free_all"></a><span data-ttu-id="2f02e-556">nx_secure_tls_remote_certificate_free_all</span><span class="sxs-lookup"><span data-stu-id="2f02e-556">nx_secure_tls_remote_certificate_free_all</span></span>

<span data-ttu-id="2f02e-557">Spazio disponibile allocato per i certificati in ingresso</span><span class="sxs-lookup"><span data-stu-id="2f02e-557">Free space allocated for incoming certificates</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-558">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-558">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_free_all(
                  NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="2f02e-559">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-559">Description</span></span>

<span data-ttu-id="2f02e-560">Questo servizio viene usato per liberare tutti i buffer di certificato allocati a una determinata sessione TLS da nx_secure_tls_remote_certificate_allocated restituendo tali buffer allo spazio dei certificati libero della sessione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-560">This service is used to free all of the certificate buffers allocated to a particular TLS Session by nx_secure_tls_remote_certificate_allocated by returning them to that session's free certificate space.</span></span> <span data-ttu-id="2f02e-561">Questa operazione può essere necessaria se un'applicazione riutilizza un oggetto sessione TLS senza eliminarlo e ricrearlo con nx_secure_tls_session_delete e nx_secure_tls_session_create.</span><span class="sxs-lookup"><span data-stu-id="2f02e-561">This may be necessary if an application reuses a TLS session object without deleting it and recreating it with nx_secure_tls_session_delete and nx_secure_tls_session_create.</span></span>

<span data-ttu-id="2f02e-562">Si noti che lo spazio del certificato remoto viene recuperato automaticamente quando la sessione TLS viene reimpostata come avviene in nx_secure_tls_session_end, quindi la maggior parte delle applicazioni non deve chiamare questo servizio.</span><span class="sxs-lookup"><span data-stu-id="2f02e-562">Note that the remote certificate space is recovered automatically when the TLS session is reset as happens in nx_secure_tls_session_end so most applications should not need to call this service.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-563">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-563">Parameters</span></span>

- <span data-ttu-id="2f02e-564">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-564">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-565">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-565">Return Values</span></span>

- <span data-ttu-id="2f02e-566">**NX_SUCCESS** (0x00) operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-566">**NX_SUCCESS** (0x00) Successful operation.</span></span>
- <span data-ttu-id="2f02e-567">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-567">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="2f02e-568">Errore interno **NX_INVALID_PARAMETERS** (irreversibile 0x4D): probabilmente danneggiato nell'archivio certificati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-568">**NX_INVALID_PARAMETERS** (0x4D) Internal error – certificate store likely corrupt.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-569">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-569">Allowed From</span></span>

<span data-ttu-id="2f02e-570">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-570">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-571">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-571">Example</span></span>

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;

/* Buffer space to hold the incoming certificate. */
UCHAR certificate_buffer[2000];

/* Add certificate to TLS session.  */
status =  nx_secure_tls_remote_certificate_allocate(&tls_session, &certificate,
                                                    certificate_buffer,
                                                    sizeof(certificate_buffer));


/* If status is NX_SUCCESS the certificate was successfully allocated.  */

/* … TLS session setup, TCP connection, etc… */

/* End TLS session. */
nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);

/* Free up certificate buffers for next connection. */
nx_secure_tls_remote_certificate_free_all(&tls_session);
```

### <a name="see-also"></a><span data-ttu-id="2f02e-572">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-572">See Also</span></span>

- <span data-ttu-id="2f02e-573">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-573">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-574">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-574">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-575">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-575">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-576">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="2f02e-576">nx_secure_tls_session_end</span></span>

## <a name="nx_secure_tls_server_certificate_add"></a><span data-ttu-id="2f02e-577">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-577">nx_secure_tls_server_certificate_add</span></span>

<span data-ttu-id="2f02e-578">Aggiungere un certificato in modo specifico per i server TLS usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="2f02e-578">Add a certificate specifically for TLS servers using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-579">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-579">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_add(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT *certificate, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="2f02e-580">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-580">Description</span></span>

<span data-ttu-id="2f02e-581">Questo servizio viene usato per aggiungere un certificato a un archivio locale della sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico anziché indicizzare l'archivio usando il soggetto X. 509 (nome comune) all'interno del certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-581">This service is used to add a certificate to a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span> <span data-ttu-id="2f02e-582">L'identificatore numerico è separato dal certificato e consente l'aggiunta di più certificati come certificati di identità a un server TLS, oltre a consentire l'aggiunta di più certificati con lo stesso nome comune allo stesso archivio locale della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-582">The numeric identifier is separate from the certificate and allows multiple certificates to be added as identity certificates to a TLS server, as well as allowing multiple certificates with the same Common Name to be added to the same TLS session local store.</span></span> <span data-ttu-id="2f02e-583">Questo stesso servizio può essere usato per i certificati client, ma è raro che un client TLS disponga di più certificati di identità.</span><span class="sxs-lookup"><span data-stu-id="2f02e-583">This same service can be used for client certificates, but it is rare for a TLS client to have multiple identity certificates.</span></span>

<span data-ttu-id="2f02e-584">Il parametro cert_id è un numero intero positivo diverso da zero assegnato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-584">The cert_id parameter is a non-zero positive integer assigned by the application.</span></span> <span data-ttu-id="2f02e-585">Il valore effettivo non è rilevante (diverso da zero), ma deve essere univoco nell'archivio per la sessione TLS specificata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-585">The actual value does not matter (other than zero) but it must be unique in the store for the provided TLS session.</span></span> <span data-ttu-id="2f02e-586">Il valore cert_id può essere usato per trovare e rimuovere i certificati dall'archivio locale usando rispettivamente nx_secure_tls_server_certificate_find e nx_secure_tls_server_certificate_remove.</span><span class="sxs-lookup"><span data-stu-id="2f02e-586">The cert_id value can be used to find and remove certificates from the local store using nx_secure_tls_server_certificate_find and nx_secure_tls_server_certificate_remove, respectively.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f02e-587">*Non usare questa API con la stessa sessione TLS quando si usa nx_secure_tls_local_certificate_add. L'API nx_secure_tls_server_certificate_add usa un identificatore numerico univoco per ogni certificato e l'indice locale di Servizi certificati in base al nome comune X. 509. I servizi certificati server consentono di esistere più certificati con dati condivisi (in particolare il nome comune) nello stesso archivio locale. questa operazione è utile per un server con più identità.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-587">*This API should not be used with the same TLS session when using nx_secure_tls_local_certificate_add. The nx_secure_tls_server_certificate_add API uses a unique numeric identifier for each certificate, and local certificate services index based on the X.509 Common Name. The server certificate services allow multiple certificates with shared data (especially Common Name) to exist in the same local store – this is useful for a server with multiple identities.*</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-588">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-588">Parameters</span></span>

- <span data-ttu-id="2f02e-589">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-589">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-590">**certificato** di Puntatore a un'istanza di certificato X. 509 inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-590">**certificate** Pointer to a previously initialized X.509 certificate instance.</span></span>
- <span data-ttu-id="2f02e-591">**cert_id** Numero ID certificato positivo, diverso da zero, relativamente univoco.</span><span class="sxs-lookup"><span data-stu-id="2f02e-591">**cert_id** Positive, non-zero, relatively unique certificate ID number.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-592">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-592">Return Values</span></span>

- <span data-ttu-id="2f02e-593">**NX_SUCCESS** (0x00) operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-593">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="2f02e-594">Il puntatore orcertificate della sessione TLS **NX_PTR_ERROR** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-594">**NX_PTR_ERROR** (0x07) Invalid TLS session orcertificate pointer.</span></span>
- <span data-ttu-id="2f02e-595">**NX_SECURE_TLS_CERT_ID_INVALID** (0X138) l'ID certificato specificato presenta un valore non valido (probabilmente 0).</span><span class="sxs-lookup"><span data-stu-id="2f02e-595">**NX_SECURE_TLS_CERT_ID_INVALID** (0x138) The provided certificate ID had An invalid value (likely 0).</span></span>
- <span data-ttu-id="2f02e-596">**NX_SECURE_TLS_CERT_ID_DUPLICATE** (0X139) l'ID certificato specificato è già presente nell'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="2f02e-596">**NX_SECURE_TLS_CERT_ID_DUPLICATE** (0x139) The provided certificate ID was already present in the local store.</span></span>
- <span data-ttu-id="2f02e-597">**NX_INVALID_PARAMETERS (irreversibile 0x4D)** Errore interno: l'archivio certificati probabilmente è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-597">**NX_INVALID_PARAMETERS(0x4D)** Internal error – certificate store likely corrupt.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-598">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-598">Allowed From</span></span>

<span data-ttu-id="2f02e-599">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-599">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-600">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-600">Example</span></span>

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully added with the ID
0x12.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-601">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-601">See Also</span></span>

- <span data-ttu-id="2f02e-602">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-602">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-603">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-603">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="2f02e-604">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-604">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="2f02e-605">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-605">nx_secure_tls_server_certificate_find</span></span>
- <span data-ttu-id="2f02e-606">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-606">nx_secure_tls_server_certificate_remove</span></span>

## <a name="nx_secure_tls_server_certificate_find"></a><span data-ttu-id="2f02e-607">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-607">nx_secure_tls_server_certificate_find</span></span>

<span data-ttu-id="2f02e-608">Trovare un certificato usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="2f02e-608">Find a certificate using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-609">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-609">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_find(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT **certificate, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="2f02e-610">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-610">Description</span></span>

<span data-ttu-id="2f02e-611">Questo servizio viene usato per trovare un certificato nell'archivio locale di una sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico anziché indicizzare l'archivio usando il soggetto X. 509 (nome comune) all'interno del certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-611">This service is used to find a certificate in a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span>

<span data-ttu-id="2f02e-612">Il parametro cert_id è un numero intero positivo diverso da zero assegnato dall'applicazione quando il certificato viene aggiunto all'archivio locale della sessione TLS utilizzando nx_secure_tls_server_certificate_add.</span><span class="sxs-lookup"><span data-stu-id="2f02e-612">The cert_id parameter is a non-zero positive integer assigned by the application when the certificate is added to the TLS session local store using nx_secure_tls_server_certificate_add.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f02e-613">*Non usare questa API con la stessa sessione TLS quando si usa nx_secure_tls_local_certificate_add. L'API nx_secure_tls_server_certificate_add usa un identificatore numerico univoco per ogni certificato e l'indice locale di Servizi certificati in base al nome comune X. 509. I servizi certificati server consentono di esistere più certificati con dati condivisi (in particolare il nome comune) nello stesso archivio locale. questa operazione è utile per un server con più identità.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-613">*This API should not be used with the same TLS session when using nx_secure_tls_local_certificate_add. The nx_secure_tls_server_certificate_add API uses a unique numeric identifier for each certificate, and local certificate services index based on the X.509 Common Name. The server certificate services allow multiple certificates with shared data (especially Common Name) to exist in the same local store – this is useful for a server with multiple identities.*</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-614">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-614">Parameters</span></span>

- <span data-ttu-id="2f02e-615">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-615">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-616">**certificato** di Puntatore a un puntatore al certificato X. 509 per restituire un riferimento al certificato trovato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-616">**certificate** Pointer to an X.509 certificate pointer to return a reference to the found certificate.</span></span>
- <span data-ttu-id="2f02e-617">**cert_id** Valore ID certificato positivo diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="2f02e-617">**cert_id** Non-zero positive certificate ID value.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-618">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-618">Return Values</span></span>

- <span data-ttu-id="2f02e-619">**NX_SUCCESS** (0x00) operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-619">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="2f02e-620">**NX_PTR_ERROR** (0x07) la sessione TLS o il puntatore al certificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-620">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>
- <span data-ttu-id="2f02e-621">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0X119) l'ID certificato specificato non corrisponde a nessuno nell'archivio locale della sessione TLS specificata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-621">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) The provided certificate ID did not match any in the local store of the provided TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-622">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-622">Allowed From</span></span>

<span data-ttu-id="2f02e-623">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-623">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-624">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-624">Example</span></span>

```C
NX_SECURE_X509_CERT *certificate;


/* Find certificate in TLS session.  */
status =  nx_secure_tls_server_certificate_find(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully found and a reference
returned in the certificate parameter.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-625">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-625">See Also</span></span>

- <span data-ttu-id="2f02e-626">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-626">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-627">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-627">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="2f02e-628">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-628">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="2f02e-629">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-629">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="2f02e-630">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-630">nx_secure_tls_server_certificate_remove</span></span>

##  <a name="nx_secure_tls_server_certificate_remove"></a><span data-ttu-id="2f02e-631">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-631">nx_secure_tls_server_certificate_remove</span></span>

<span data-ttu-id="2f02e-632">Rimuovere un certificato del server locale usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="2f02e-632">Remove a local server certificate using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-633">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-633">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_remove(
                  NX_SECURE_TLS_SESSION *session_ptr, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="2f02e-634">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-634">Description</span></span>

<span data-ttu-id="2f02e-635">Questo servizio viene usato per rimuovere un certificato da un archivio locale della sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico anziché indicizzare l'archivio usando il soggetto X. 509 (nome comune) all'interno del certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-635">This service is used to remove a certificate from a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span>

<span data-ttu-id="2f02e-636">Il parametro cert_id è un numero intero positivo diverso da zero assegnato dall'applicazione quando il certificato viene aggiunto all'archivio locale della sessione TLS utilizzando nx_secure_tls_server_certificate_add.</span><span class="sxs-lookup"><span data-stu-id="2f02e-636">The cert_id parameter is a non-zero positive integer assigned by the application when the certificate is added to the TLS session local store using nx_secure_tls_server_certificate_add.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-637">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-637">Parameters</span></span>

- <span data-ttu-id="2f02e-638">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-638">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-639">**cert_id** Valore ID certificato positivo diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="2f02e-639">**cert_id** Non-zero positive certificate ID value.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-640">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-640">Return Values</span></span>

- <span data-ttu-id="2f02e-641">**NX_SUCCESS** (0x00) operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-641">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="2f02e-642">**NX_PTR_ERROR** sessione TLS non valida (0x07).</span><span class="sxs-lookup"><span data-stu-id="2f02e-642">**NX_PTR_ERROR** (0x07) Invalid TLS session.</span></span>
- <span data-ttu-id="2f02e-643">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0X119) l'ID certificato specificato non corrisponde a nessuno nell'archivio locale della sessione TLS specificata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-643">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) The provided certificate ID did not match any in the local store of the provided TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-644">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-644">Allowed From</span></span>

<span data-ttu-id="2f02e-645">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-645">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-646">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-646">Example</span></span>

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session with id 0x12.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);
/* Use certificate in TLS session, etc… */

/* Remove certificate from TLS session with id 0x12.  */
status =  nx_secure_tls_server_certificate_remove(&tls_session, 0x12);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-647">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-647">See Also</span></span>

- <span data-ttu-id="2f02e-648">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-648">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-649">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-649">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="2f02e-650">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-650">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="2f02e-651">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-651">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="2f02e-652">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-652">nx_secure_tls_server_certificate_find</span></span>

## <a name="nx_secure_tls_session_alert_value_get"></a><span data-ttu-id="2f02e-653">nx_secure_tls_session_alert_value_get</span><span class="sxs-lookup"><span data-stu-id="2f02e-653">nx_secure_tls_session_alert_value_get</span></span>

<span data-ttu-id="2f02e-654">Ottenere il livello e il valore di avviso TLS inviati dall'host remoto</span><span class="sxs-lookup"><span data-stu-id="2f02e-654">Get the TLS alert value and level sent by the remote host</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-655">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-655">Prototype</span></span>

```C
UINT  nx_secure_tls_session_alert_value_get(
                   NX_SECURE_TLS_SESSION *session_ptr,
                   UINT *alert_level, UINT *alert_value);
```

### <a name="description"></a><span data-ttu-id="2f02e-656">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-656">Description</span></span>

<span data-ttu-id="2f02e-657">Questo servizio viene usato per recuperare il livello e il valore di avviso TLS quando l'host remoto invia un avviso in risposta a un problema o a un errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-657">This service is used to retrieve the TLS alert level and value when the remote host sends an alert in response to some problem or error.</span></span>

<span data-ttu-id="2f02e-658">I valori dei parametri alert_level e alert_value sono validi solo se questa funzione viene chiamata immediatamente dopo una chiamata API TLS che ha restituito lo stato NX_SECURE_TLS_ALERT_RECEIVED (0x114) che indica che è stato ricevuto un avviso dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-658">The values of the alert_level and alert_value parameters are only valid if this function is called immediately following a TLS API call that returned a status of NX_SECURE_TLS_ALERT_RECEIVED (0x114) indicating that an alert was received from the remote host.</span></span>

<span data-ttu-id="2f02e-659">Si noti che se l'host locale TLS Invia un avviso, i codici di errore restituiti sono molto più descrittivi dell'errore effettivo rispetto all'avviso TLS stesso perché i valori di avviso TLS sono intenzionalmente lasciati ambigui per evitare determinati tipi di attacco (ad esempio, un attacco "riempimento Oracle" o simile).</span><span class="sxs-lookup"><span data-stu-id="2f02e-659">Note that if the local host TLS sends an alert, the returned error codes are far more descriptive of the actual error than the TLS alert itself because TLS alert values are intentionally left ambiguous to prevent certain types of attack (such as a "padding oracle" attack or similar).</span></span>

<span data-ttu-id="2f02e-660">Il livello di avviso accetta solo uno dei due valori seguenti: NX_SECURE_TLS_ALERT_LEVEL_WARNING (0x1) o NX_SECURE_TLS_ALERT_LEVEL_FATAL (0x2).</span><span class="sxs-lookup"><span data-stu-id="2f02e-660">The alert level only takes one of two values: NX_SECURE_TLS_ALERT_LEVEL_WARNING (0x1) or NX_SECURE_TLS_ALERT_LEVEL_FATAL (0x2).</span></span> <span data-ttu-id="2f02e-661">In generale, viene fornito un livello di "avviso" solo per l'avviso CloseNotify (usato per indicare un esito positivo di una sessione TLS), anche se alcune situazioni di configurazione dell'estensione possono essere considerate avvisi.</span><span class="sxs-lookup"><span data-stu-id="2f02e-661">In general, only the CloseNotify Alert (used to indicate a successful end to a TLS session) will be given a level of "Warning" though some extension configuration situations may also be considered warnings.</span></span> <span data-ttu-id="2f02e-662">La maggior parte degli avvisi sarà "irreversibile", che indica un potenziale errore di sicurezza e con conseguente chiusura immediata della connessione TLS (handshake o Session).</span><span class="sxs-lookup"><span data-stu-id="2f02e-662">The vast majority of alerts will be "Fatal" indicating a potential security failure and resulting in immediate closure of the TLS connection (handshake or session).</span></span>

<span data-ttu-id="2f02e-663">I valori di avviso TLS sono definiti nelle RFC di TLS. di seguito è riportato l'elenco di RFC 5246 (TLSv 1.2) per riferimento:</span><span class="sxs-lookup"><span data-stu-id="2f02e-663">The TLS alert values are defined in the TLS RFCs, here is the list from RFC 5246 (TLSv1.2) for reference:</span></span>

| <span data-ttu-id="2f02e-664">Nome avviso</span><span class="sxs-lookup"><span data-stu-id="2f02e-664">Alert Name</span></span>                     | <span data-ttu-id="2f02e-665">Valore</span><span class="sxs-lookup"><span data-stu-id="2f02e-665">Value</span></span> | <span data-ttu-id="2f02e-666">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-666">Description</span></span>                                                                                                                                                  |
| ---------------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="2f02e-667">close_notify</span><span class="sxs-lookup"><span data-stu-id="2f02e-667">close_notify</span></span>                  | <span data-ttu-id="2f02e-668">0</span><span class="sxs-lookup"><span data-stu-id="2f02e-668">0</span></span>     | <span data-ttu-id="2f02e-669">Nessun errore, indica la fine della sessione completata</span><span class="sxs-lookup"><span data-stu-id="2f02e-669">No error, indicates successful session end</span></span>                                                                                                                   |
| <span data-ttu-id="2f02e-670">unexpected_message</span><span class="sxs-lookup"><span data-stu-id="2f02e-670">unexpected_message</span></span>            | <span data-ttu-id="2f02e-671">10</span><span class="sxs-lookup"><span data-stu-id="2f02e-671">10</span></span>    | <span data-ttu-id="2f02e-672">Un messaggio imprevisto o non ordinato è stato ricevuto da TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-672">TLS received an unexpected or out-of-order message</span></span>                                                                                                           |
| <span data-ttu-id="2f02e-673">bad_record_mac</span><span class="sxs-lookup"><span data-stu-id="2f02e-673">bad_record_mac</span></span>               | <span data-ttu-id="2f02e-674">20</span><span class="sxs-lookup"><span data-stu-id="2f02e-674">20</span></span>    | <span data-ttu-id="2f02e-675">Verifica decrittografia e/o MAC non riuscita</span><span class="sxs-lookup"><span data-stu-id="2f02e-675">Decryption and/or MAC verification failed</span></span>                                                                                                                    |
| <span data-ttu-id="2f02e-676">decryption_failed_RESERVED</span><span class="sxs-lookup"><span data-stu-id="2f02e-676">decryption_failed_RESERVED</span></span>   | <span data-ttu-id="2f02e-677">21</span><span class="sxs-lookup"><span data-stu-id="2f02e-677">21</span></span>    | <span data-ttu-id="2f02e-678">**Obsoleto** Decrittografia non riuscita (deprecata a causa di attacchi Oracle di riempimento)</span><span class="sxs-lookup"><span data-stu-id="2f02e-678">**DEPRECATED** Decryption failed (deprecated due to padding oracle attacks)</span></span>                                                                                      |
| <span data-ttu-id="2f02e-679">record_overflow</span><span class="sxs-lookup"><span data-stu-id="2f02e-679">record_overflow</span></span>               | <span data-ttu-id="2f02e-680">22</span><span class="sxs-lookup"><span data-stu-id="2f02e-680">22</span></span>    | <span data-ttu-id="2f02e-681">È stato ricevuto un record maggiore della dimensione massima del record TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-681">A record was received that is larger than the TLS maximum record size</span></span>                                                                                        |
| <span data-ttu-id="2f02e-682">decompression_failure</span><span class="sxs-lookup"><span data-stu-id="2f02e-682">decompression_failure</span></span>         | <span data-ttu-id="2f02e-683">30</span><span class="sxs-lookup"><span data-stu-id="2f02e-683">30</span></span>    | <span data-ttu-id="2f02e-684">Si è verificato un problema durante la compressione/decompressione di un record TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-684">A problem was encountered in compression/decompression of a TLS record</span></span>                                                                                       |
| <span data-ttu-id="2f02e-685">handshake_failure</span><span class="sxs-lookup"><span data-stu-id="2f02e-685">handshake_failure</span></span>             | <span data-ttu-id="2f02e-686">40</span><span class="sxs-lookup"><span data-stu-id="2f02e-686">40</span></span>    | <span data-ttu-id="2f02e-687">Si è verificato un errore di handshake non specificato che non è coperto da un avviso diverso</span><span class="sxs-lookup"><span data-stu-id="2f02e-687">Some unspecified handshake error occurred that isn't covered by a different alert</span></span>                                                                            |
| <span data-ttu-id="2f02e-688">no_certificate_RESERVED</span><span class="sxs-lookup"><span data-stu-id="2f02e-688">no_certificate_RESERVED</span></span>      | <span data-ttu-id="2f02e-689">41</span><span class="sxs-lookup"><span data-stu-id="2f02e-689">41</span></span>    | <span data-ttu-id="2f02e-690">**Deprecato** in TLS (solo SSL)</span><span class="sxs-lookup"><span data-stu-id="2f02e-690">**DEPRECATED** in TLS (SSL only)</span></span>                                                                                                                                 |
| <span data-ttu-id="2f02e-691">bad_certificate</span><span class="sxs-lookup"><span data-stu-id="2f02e-691">bad_certificate</span></span>               | <span data-ttu-id="2f02e-692">42</span><span class="sxs-lookup"><span data-stu-id="2f02e-692">42</span></span>    | <span data-ttu-id="2f02e-693">Un certificato ricevuto contiene una formattazione o una firma non valida</span><span class="sxs-lookup"><span data-stu-id="2f02e-693">A certificate that was received contained invalid formatting or signatures</span></span>                                                                                   |
| <span data-ttu-id="2f02e-694">unsupported_certificate</span><span class="sxs-lookup"><span data-stu-id="2f02e-694">unsupported_certificate</span></span>       | <span data-ttu-id="2f02e-695">43</span><span class="sxs-lookup"><span data-stu-id="2f02e-695">43</span></span>    | <span data-ttu-id="2f02e-696">È stato ricevuto un certificato di tipo non valido (ad esempio, il certificato di sola firma usato per l'autenticazione del server TLS)</span><span class="sxs-lookup"><span data-stu-id="2f02e-696">A certificate was received that was of an invalid type (e.g. signing-only certificate used for TLS server authentication)</span></span>                                    |
| <span data-ttu-id="2f02e-697">certificate_revoked</span><span class="sxs-lookup"><span data-stu-id="2f02e-697">certificate_revoked</span></span>           | <span data-ttu-id="2f02e-698">44</span><span class="sxs-lookup"><span data-stu-id="2f02e-698">44</span></span>    | <span data-ttu-id="2f02e-699">Lo stato del certificato (come fornito da un CRL o OCSP) è stato indicato come "revocato"</span><span class="sxs-lookup"><span data-stu-id="2f02e-699">The certificate status (as provided by a CRL or OCSP) was indicated as being "revoked"</span></span>                                                                       |
| <span data-ttu-id="2f02e-700">certificate_expired</span><span class="sxs-lookup"><span data-stu-id="2f02e-700">certificate_expired</span></span>           | <span data-ttu-id="2f02e-701">45</span><span class="sxs-lookup"><span data-stu-id="2f02e-701">45</span></span>    | <span data-ttu-id="2f02e-702">Il certificato ricevuto non è compreso nell'intervallo di date valido, ovvero non è ancora valido o è scaduto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-702">The received certificate was outside it's valid date range (either not valid yet or expired)</span></span>                                                                 |
| <span data-ttu-id="2f02e-703">certificate_unknown</span><span class="sxs-lookup"><span data-stu-id="2f02e-703">certificate_unknown</span></span>           | <span data-ttu-id="2f02e-704">46</span><span class="sxs-lookup"><span data-stu-id="2f02e-704">46</span></span>    | <span data-ttu-id="2f02e-705">Si è verificato un problema di certificato sconosciuto non coperto da altri avvisi</span><span class="sxs-lookup"><span data-stu-id="2f02e-705">Some unknown certificate issue was encountered that was not covered by other alerts</span></span>                                                                          |
| <span data-ttu-id="2f02e-706">illegal_parameter</span><span class="sxs-lookup"><span data-stu-id="2f02e-706">illegal_parameter</span></span>             | <span data-ttu-id="2f02e-707">47</span><span class="sxs-lookup"><span data-stu-id="2f02e-707">47</span></span>    | <span data-ttu-id="2f02e-708">Una configurazione o un valore negoziato nell'handshake TLS non è valido o non è compreso nell'intervallo</span><span class="sxs-lookup"><span data-stu-id="2f02e-708">Some configuration or negotiated value in the TLS handshake was invalid or out of range</span></span>                                                                      |
| <span data-ttu-id="2f02e-709">unknown_ca</span><span class="sxs-lookup"><span data-stu-id="2f02e-709">unknown_ca</span></span>                    | <span data-ttu-id="2f02e-710">48</span><span class="sxs-lookup"><span data-stu-id="2f02e-710">48</span></span>    | <span data-ttu-id="2f02e-711">Non è stato possibile tracciare il certificato di identità ricevuto tramite una catena di certificati a un certificato CA radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="2f02e-711">The received identity certificate could not be traced via a certificate chain to a trusted root CA certificate.</span></span>                                              |
| <span data-ttu-id="2f02e-712">access_denied</span><span class="sxs-lookup"><span data-stu-id="2f02e-712">access_denied</span></span>                 | <span data-ttu-id="2f02e-713">49</span><span class="sxs-lookup"><span data-stu-id="2f02e-713">49</span></span>    | <span data-ttu-id="2f02e-714">Indica che è stato ricevuto un certificato valido, ma il controllo di accesso dell'applicazione ha indicato che il certificato non è valido per le risorse richieste.</span><span class="sxs-lookup"><span data-stu-id="2f02e-714">Indicates a valid certificate was received but application access control indicated that the certificate was invalid for the requested resources.</span></span>            |
| <span data-ttu-id="2f02e-715">decode_error</span><span class="sxs-lookup"><span data-stu-id="2f02e-715">decode_error</span></span>                  | <span data-ttu-id="2f02e-716">50</span><span class="sxs-lookup"><span data-stu-id="2f02e-716">50</span></span>    | <span data-ttu-id="2f02e-717">Alcuni campi o valori in un messaggio di intestazione o di handshake TLS non sono compresi nell'intervallo o non sono validi, causando un errore nella decodifica di un record TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-717">Some field or value in a TLS header or handshake message was out of range or invalid, leading to a failure in decoding of a TLS record.</span></span>                      |
| <span data-ttu-id="2f02e-718">decrypt_error</span><span class="sxs-lookup"><span data-stu-id="2f02e-718">decrypt_error</span></span>                 | <span data-ttu-id="2f02e-719">51</span><span class="sxs-lookup"><span data-stu-id="2f02e-719">51</span></span>    | <span data-ttu-id="2f02e-720">Non è stato possibile verificare una firma o un hash del messaggio terminato durante l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-720">A signature or Finished message hash during the TLS handshake could not be verified.</span></span>                                                                         |
| <span data-ttu-id="2f02e-721">export_restriction_RESERVED</span><span class="sxs-lookup"><span data-stu-id="2f02e-721">export_restriction_RESERVED</span></span>  | <span data-ttu-id="2f02e-722">60</span><span class="sxs-lookup"><span data-stu-id="2f02e-722">60</span></span>    | <span data-ttu-id="2f02e-723">DEPRECAto in TLSv 1.2</span><span class="sxs-lookup"><span data-stu-id="2f02e-723">DEPRECATED in TLSv1.2</span></span>                                                                                                                                        |
| <span data-ttu-id="2f02e-724">protocol_version</span><span class="sxs-lookup"><span data-stu-id="2f02e-724">protocol_version</span></span>              | <span data-ttu-id="2f02e-725">70</span><span class="sxs-lookup"><span data-stu-id="2f02e-725">70</span></span>    | <span data-ttu-id="2f02e-726">La versione del protocollo TLS negoziata durante l'handshake è riconosciuta ma non supportata (ad esempio, TLSv 1.0 è stato presentato ma non è abilitato).</span><span class="sxs-lookup"><span data-stu-id="2f02e-726">The TLS protocol version negotiated during the handshake is recognized but not supported (e.g. TLSv1.0 was presented but not enabled).</span></span>                       |
| <span data-ttu-id="2f02e-727">insufficient_security</span><span class="sxs-lookup"><span data-stu-id="2f02e-727">insufficient_security</span></span>         | <span data-ttu-id="2f02e-728">71</span><span class="sxs-lookup"><span data-stu-id="2f02e-728">71</span></span>    | <span data-ttu-id="2f02e-729">Inviato ogni volta che l'handshake ha esito negativo a causa della mancanza di crittografie sicure (ad esempio, la dimensione della chiave è troppo piccola per i requisiti dell'applicazione)</span><span class="sxs-lookup"><span data-stu-id="2f02e-729">Sent whenever a handshake fails due to a lack of secure ciphers (e.g. key size is too small for the application requirements)</span></span>                                |
| <span data-ttu-id="2f02e-730">internal_error</span><span class="sxs-lookup"><span data-stu-id="2f02e-730">internal_error</span></span>                | <span data-ttu-id="2f02e-731">80</span><span class="sxs-lookup"><span data-stu-id="2f02e-731">80</span></span>    | <span data-ttu-id="2f02e-732">Si è verificato un errore non TLS, ad esempio problemi di allocazione della memoria e problemi dell'applicazione, causando una sessione TLS interruppe.</span><span class="sxs-lookup"><span data-stu-id="2f02e-732">Some non-TLS error (e.g. memory allocation problems, application issues) occurred resulting in a broken TLS session.</span></span>                                         |
| <span data-ttu-id="2f02e-733">user_canceled</span><span class="sxs-lookup"><span data-stu-id="2f02e-733">user_canceled</span></span>                 | <span data-ttu-id="2f02e-734">90</span><span class="sxs-lookup"><span data-stu-id="2f02e-734">90</span></span>    | <span data-ttu-id="2f02e-735">Restituito se la sessione TLS viene annullata da un utente o da un'applicazione prima del completamento dell'handshake (simile a CloseNotify).</span><span class="sxs-lookup"><span data-stu-id="2f02e-735">Returned if the TLS session is cancelled by a user or application before the handshake is complete (similar to CloseNotify).</span></span>                                 |
| <span data-ttu-id="2f02e-736">no_renegotiation</span><span class="sxs-lookup"><span data-stu-id="2f02e-736">no_renegotiation</span></span>              | <span data-ttu-id="2f02e-737">100</span><span class="sxs-lookup"><span data-stu-id="2f02e-737">100</span></span>   | <span data-ttu-id="2f02e-738">Indiates che l'host remoto non è disposto a eseguire handshake di rinegoziazione TLS in risposta a una richiesta di rinegoziazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-738">Indiates that the remote host is not willing to perform TLS renegotiation handshakes in response to a renegotiation request.</span></span>                                 |
| <span data-ttu-id="2f02e-739">unsupported_extension</span><span class="sxs-lookup"><span data-stu-id="2f02e-739">unsupported_extension</span></span>         | <span data-ttu-id="2f02e-740">110</span><span class="sxs-lookup"><span data-stu-id="2f02e-740">110</span></span>   | <span data-ttu-id="2f02e-741">Inviato se un client TLS riceve un ServerHello contenente le estensioni non richieste in modo esplicito nel ClientHello iniziale (indicante che si è verificato un problema nel server).</span><span class="sxs-lookup"><span data-stu-id="2f02e-741">Sent if a TLS Client receives a ServerHello containing extensions not explicitly asked for in the initial ClientHello (indicating the server has a problem).</span></span> |

### <a name="parameters"></a><span data-ttu-id="2f02e-742">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-742">Parameters</span></span>

- <span data-ttu-id="2f02e-743">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-743">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-744">**alert_level** Restituisce il livello dell'avviso ricevuto (avviso o irreversibile).</span><span class="sxs-lookup"><span data-stu-id="2f02e-744">**alert_level** Return the level of the received alert (warning or fatal).</span></span>
- <span data-ttu-id="2f02e-745">**alert_value** Restituisce il valore dell'avviso ricevuto (vedere la tabella).</span><span class="sxs-lookup"><span data-stu-id="2f02e-745">**alert_value** Return the value of the received alert (see table).</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-746">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-746">Return Values</span></span>

- <span data-ttu-id="2f02e-747">**NX_SUCCESS** (0x00) operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-747">**NX_SUCCESS** (0x00) Successful operation.</span></span>
- <span data-ttu-id="2f02e-748">**NX_PTR_ERROR** sessione TLS non valida (0x07).</span><span class="sxs-lookup"><span data-stu-id="2f02e-748">**NX_PTR_ERROR** (0x07) Invalid TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-749">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-749">Allowed From</span></span>

<span data-ttu-id="2f02e-750">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-750">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-751">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-751">Example</span></span>

```C
/* Return values. */
UINT status, alert_level, alert_value;


/* Start a TLS session.  */
status =  nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);

/* Check for “alert received” error. */
if(status == NX_SECURE_TLS_ALERT_RECEIVED)
{

        /* Get the alert level and value. */
        status =  nx_secure_tls_session_alert_value_get(&tls_session,
                                             &alert_level, &alert_value);

        /* Print out the received alert level and value. */
        printf("Alert recieved. Value: %d, Level: %d\n", alert_value,
                alert_level);
}
else if(status != NX_SUCCESS)
{
    /* Additional error handling. */
}
```

### <a name="see-also"></a><span data-ttu-id="2f02e-752">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-752">See Also</span></span>

- <span data-ttu-id="2f02e-753">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-753">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-754">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-754">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="2f02e-755">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-755">nx_secure_tls_session_receive</span></span>

## <a name="nx_secure_tls_session_certificate_callback_set"></a><span data-ttu-id="2f02e-756">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-756">nx_secure_tls_session_certificate_callback_set</span></span>

<span data-ttu-id="2f02e-757">Configurare un callback per TLS da usare per la convalida aggiuntiva dei certificati</span><span class="sxs-lookup"><span data-stu-id="2f02e-757">Set up a callback for TLS to use for additional certificate validation</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-758">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-758">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_certificate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *session,
                                    NX_SECURE_X509_CERT *certificate));
```

### <a name="description"></a><span data-ttu-id="2f02e-759">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-759">Description</span></span>

<span data-ttu-id="2f02e-760">Questo servizio assegna un puntatore a funzione a una sessione TLS che verrà richiamata da TLS quando un certificato viene ricevuto da un host remoto, consentendo all'applicazione di eseguire controlli di convalida, ad esempio la convalida DNS, la revoca dei certificati e l'applicazione dei criteri dei certificati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-760">This service assigns a function pointer to a TLS session that TLS will invoke when a certificate is received from a remote host, allowing the application to perform validation checks such as DNS validation, certificate revocation, and certificate policy enforcement.</span></span>

<span data-ttu-id="2f02e-761">NetX Secure TLS eseguirà la convalida di base del percorso X. 509 sul certificato prima di richiamare il callback per garantire che il certificato possa essere tracciato a un certificato nell'archivio certificati trusted TLS, ma tutte le altre convalide verranno gestite da questo callback.</span><span class="sxs-lookup"><span data-stu-id="2f02e-761">NetX Secure TLS will perform basic X.509 path validation on the certificate before invoking the callback to assure that the certificate can be traced to a certificate in the TLS trusted certificate store, but all other validation will be handled by this callback.</span></span>

<span data-ttu-id="2f02e-762">Il callback fornisce il puntatore della sessione TLS e un puntatore al certificato di identità dell'host remoto (foglia nella catena di certificati).</span><span class="sxs-lookup"><span data-stu-id="2f02e-762">The callback provides the TLS session pointer and a pointer to the remote host identity certificate (the leaf in the certificate chain).</span></span> <span data-ttu-id="2f02e-763">Il callback deve restituire NX_SUCCESS se la convalida ha esito positivo; in caso contrario, deve restituire un codice di errore che indica l'errore di convalida.</span><span class="sxs-lookup"><span data-stu-id="2f02e-763">The callback should return NX_SUCCESS if all validation is successful, otherwise it should return an error code indicating the validation failure.</span></span> <span data-ttu-id="2f02e-764">Qualsiasi valore diverso da NX_SUCCESS farà sì che l'handshake TLS venga interrotto immediatamente.</span><span class="sxs-lookup"><span data-stu-id="2f02e-764">Any value other than NX_SUCCESS will cause the TLS handshake to immediately abort.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-765">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-765">Parameters</span></span>

- <span data-ttu-id="2f02e-766">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-766">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-767">**func_ptr** Puntatore alla funzione di callback di convalida del certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-767">**func_ptr** Pointer to the certificate validation callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-768">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-768">Return Values</span></span>

- <span data-ttu-id="2f02e-769">**NX_SUCCESS** (0x00) allocazione riuscita del puntatore a funzione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-769">**NX_SUCCESS** (0x00) Successful allocation of Function pointer.</span></span>
- <span data-ttu-id="2f02e-770">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-770">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-771">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-771">Allowed From</span></span>

<span data-ttu-id="2f02e-772">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-772">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-773">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-773">Example</span></span>

```C
/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
    /* Certificate validation checking goes here. */
    return(NX_SUCCESS);
}

/* In TLS setup routine. */
{
        /* Add callback to TLS session.  */
        status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                            certificate_callback);

        /* If status is NX_SUCCESS the certificate callback was added.  */
}
```

### <a name="see-also"></a><span data-ttu-id="2f02e-774">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-774">See Also</span></span>

- <span data-ttu-id="2f02e-775">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-775">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-776">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-776">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="2f02e-777">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-777">nx_secure_x509_crl_revocation_check</span></span>

## <a name="nx_secure_tls_session_client_callback_set"></a><span data-ttu-id="2f02e-778">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-778">nx_secure_tls_session_client_callback_set</span></span>

<span data-ttu-id="2f02e-779">Configurare un callback per TLS da richiamare all'inizio di un handshake client TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-779">Set up a callback for TLS to invoke at the beginning of a TLS Client handshake</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-780">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-780">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_client_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions, UINT num_extensions));
```

### <a name="description"></a><span data-ttu-id="2f02e-781">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-781">Description</span></span>

<span data-ttu-id="2f02e-782">Questo servizio assegna un puntatore a funzione a una sessione TLS che verrà richiamata da TLS quando un handshake del client TLS riceve un messaggio ServerHelloDone.</span><span class="sxs-lookup"><span data-stu-id="2f02e-782">This service assigns a function pointer to a TLS session that TLS will invoke when a TLS Client handshake has received a ServerHelloDone message.</span></span> <span data-ttu-id="2f02e-783">La funzione di callback consente a un'applicazione di elaborare tutte le estensioni TLS dal messaggio ServerHello ricevuto che richiede l'input o il processo decisionale.</span><span class="sxs-lookup"><span data-stu-id="2f02e-783">The callback function allows an application to process any TLS extensions from the received ServerHello message that require input or decision making.</span></span>

<span data-ttu-id="2f02e-784">Il callback viene eseguito con il blocco di controllo della sessione TLS chiamante e una matrice di oggetti NX_SECURE_TLS_HELLO_EXTENSION.</span><span class="sxs-lookup"><span data-stu-id="2f02e-784">The callback is executed with the invoking TLS session control block and an array of NX_SECURE_TLS_HELLO_EXTENSION objects.</span></span> <span data-ttu-id="2f02e-785">La matrice di oggetti estensione deve essere passata in una funzione helper che troverà e analizzerà un'estensione specifica.</span><span class="sxs-lookup"><span data-stu-id="2f02e-785">The array of extension objects is intended to be passed into a helper function that will find and parse a specific extension.</span></span> <span data-ttu-id="2f02e-786">Attualmente non sono presenti estensioni specifiche supportate in NetX Secure che richiedono l'input del client TLS, ma il callback è disponibile per le finestre di progettazione delle applicazioni per gestire le estensioni personalizzate o nuove che potrebbero diventare disponibili.</span><span class="sxs-lookup"><span data-stu-id="2f02e-786">Currently, there are no specific extensions supported in NetX Secure that require TLS Client input, but the callback is available for application designers to handle custom or new extensions that may become available.</span></span> <span data-ttu-id="2f02e-787">Per una funzione helper di esempio che analizza le estensioni TLS fornite nei messaggi Hello, vedere *nx_secure_tls_session_sni_extension_parse*.</span><span class="sxs-lookup"><span data-stu-id="2f02e-787">For an example helper function that parses TLS extensions provided in hello messages, see *nx_secure_tls_session_sni_extension_parse*.</span></span>

<span data-ttu-id="2f02e-788">Il callback del client può essere usato anche per selezionare il certificato di identità attivo usando *nx_secure_tls_active_certificate_set* per il client TLS nel caso in cui il server remoto abbia richiesto un certificato e abbia fornito informazioni per consentire al client TLS di selezionare un certificato specifico.</span><span class="sxs-lookup"><span data-stu-id="2f02e-788">The client callback may also be used to select the active identity certificate using *nx_secure_tls_active_certificate_set* for the TLS Client in the event that the remote server has requested a certificate and provided information to allow the TLS Client to select a specific certificate.</span></span> <span data-ttu-id="2f02e-789">Per ulteriori informazioni, vedere il riferimento per nx_secure_tls_active_certificate_set.</span><span class="sxs-lookup"><span data-stu-id="2f02e-789">See the reference for nx_secure_tls_active_certificate_set for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-790">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-790">Parameters</span></span>

- <span data-ttu-id="2f02e-791">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-791">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-792">**func_ptr** Puntatore alla funzione di callback del client TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-792">**func_ptr** Pointer to the TLS Client callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-793">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-793">Return Values</span></span>

- <span data-ttu-id="2f02e-794">**NX_SUCCESS** (0x00) allocazione riuscita del puntatore a funzione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-794">**NX_SUCCESS** (0x00) Successful allocation of function pointer.</span></span>
- <span data-ttu-id="2f02e-795">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-795">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-796">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-796">Allowed From</span></span>

<span data-ttu-id="2f02e-797">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-797">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-798">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-798">Example</span></span>

```C
/* Callback routine used to process ServerHello extensions and perform other
   runtime actions at the beginning of a TLS handshake (such as selecting an
   identify certificate to provide to the server). */

ULONG tls_client_callback(NX_SECURE_TLS_SESSION *session,
                          NX_SECURE_TLS_HELLO_EXTENSION *extensions, UINT
                          num_extensions)
{

    /* Extension parsing would go here. */

    /* Set an active identity certificate – the certificate should have been added
       to the local store at application start with
       nx_secure_tls_local_certificate_add. */
    nx_secure_tls_active_certificate_set(session, &global_identity_certificate);

    return(NX_SUCCESS);
}

/* TLS setup routine. */
UINT tls_setup(NX_SECURE_TLS_SESSION *tls_session)
{
    /* Add callback to TLS session.  */
    status =  nx_secure_tls_session_client_callback_set(tls_session,
                                                        client_callback);

    /* If status is NX_SUCCESS the callback was added and will be invoked once
       a ServerHelloDone message is received. */

    return(status);
}
```

### <a name="see-also"></a><span data-ttu-id="2f02e-799">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-799">See Also</span></span>

- <span data-ttu-id="2f02e-800">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-800">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-801">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-801">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="2f02e-802">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-802">nx_secure_tls_active_certificate_set</span></span>

## <a name="nx_secure_tls_session_x509_client_verify_configure"></a><span data-ttu-id="2f02e-803">nx_secure_tls_session_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="2f02e-803">nx_secure_tls_session_x509_client_verify_configure</span></span>

<span data-ttu-id="2f02e-804">Abilitare la verifica del client X. 509 e allocare spazio per i certificati client</span><span class="sxs-lookup"><span data-stu-id="2f02e-804">Enable client X.509 verification and allocate space for client certificates</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-805">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-805">Prototype</span></span>

```C
UINT  nx_secure_tls_session_x509_client_verify_configure(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="2f02e-806">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-806">Description</span></span>

<span data-ttu-id="2f02e-807">Questo servizio Abilita l'autenticazione client X. 509 facoltativa per un'istanza del server TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-807">This service enables the optional X.509 Client Authentication for a TLS Server instance.</span></span> <span data-ttu-id="2f02e-808">Alloca inoltre lo spazio necessario per elaborare le catene di certificati in ingresso dall'host client remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-808">It also allocates the space needed to process incoming certificate chains from the remote client host.</span></span> <span data-ttu-id="2f02e-809">I certificati forniti dal client remoto verranno verificati in base ai certificati attendibili dell'istanza del server TLS, assegnati con il nx_secure_tls_trusted_certificate_add del servizio *.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-809">The certificates supplied by the remote client will be verified against the TLS server instance's trusted certificates, assigned with the service *nx_secure_tls_trusted_certificate_add.*</span></span>

<span data-ttu-id="2f02e-810">Per la modalità client TLS, è necessaria l'allocazione di certificati remoti ed è invece necessario usare il *nx_secure_tls_remote_certificate_buffer_allocate* di servizio.</span><span class="sxs-lookup"><span data-stu-id="2f02e-810">For TLS Client mode, remote certificate allocation is required and the service *nx_secure_tls_remote_certificate_buffer_allocate* should be used instead.</span></span> <span data-ttu-id="2f02e-811">L'abilitazione dell'autenticazione client X. 509 su un'istanza del client TLS non avrà alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-811">Enabling X.509 Client Authentication on a TLS Client instance will have no effect.</span></span>

<span data-ttu-id="2f02e-812">Il parametro *certificate_buffer* punta allo spazio allocato per archiviare i certificati remoti in ingresso e i blocchi di controllo necessari per tali certificati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-812">The *certificate_buffer* parameter points to space allocated to store the incoming remote certificates and the control blocks needed for those certificates.</span></span> <span data-ttu-id="2f02e-813">Il buffer verrà diviso per il numero di certificati (*certs_number*) con una parte uguale assegnata a ogni certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-813">The buffer will be divided by the number of certificates (*certs_number*) with an equal portion given to each certificate.</span></span> <span data-ttu-id="2f02e-814">Il parametro *BUFFER_SIZE* indica le dimensioni del buffer.</span><span class="sxs-lookup"><span data-stu-id="2f02e-814">The *buffer_size* parameter indicates the size of the buffer.</span></span> <span data-ttu-id="2f02e-815">È possibile trovare lo spazio necessario con la formula seguente:</span><span class="sxs-lookup"><span data-stu-id="2f02e-815">The space needed can be found with the following formula:</span></span>

```C
buffer_size = (<expected max number of certificates in chain>) *
             (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

<span data-ttu-id="2f02e-816">I certificati tipici con chiavi RSA di 2048 bit che usano SHA-256 per le firme sono compresi nell'intervallo da 1000-2000 byte.</span><span class="sxs-lookup"><span data-stu-id="2f02e-816">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="2f02e-817">Il buffer deve essere sufficientemente grande da contenere almeno tali dimensioni per ogni certificato, ma a seconda dei certificati dell'host remoto può essere significativamente più piccolo o più grande.</span><span class="sxs-lookup"><span data-stu-id="2f02e-817">The buffer should be large enough to at least hold that size for each certificate, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="2f02e-818">Si noti che se il buffer è troppo piccolo per conservare il certificato in ingresso, l'handshake TLS termina con un errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-818">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-819">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-819">Parameters</span></span>

- <span data-ttu-id="2f02e-820">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-820">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-821">**certs_number** Numero di certificati da allocare dal buffer specificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-821">**certs_number** Number of certificates to allocate from the provided buffer.</span></span>
- <span data-ttu-id="2f02e-822">**certificate_buffer** Puntatore a un buffer per contenere i certificati ricevuti da un host remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-822">**certificate_buffer** Pointer to a buffer to hold certificates received from a remote host.</span></span>
- <span data-ttu-id="2f02e-823">**BUFFER_SIZE** Dimensioni del buffer del certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-823">**buffer_size** Size of the certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-824">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-824">Return Values</span></span>

- <span data-ttu-id="2f02e-825">**NX_SUCCESS** (0x00) l'allocazione del certificato è riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-825">**NX_SUCCESS** (0x00)Successful allocation of certificate.</span></span>
- <span data-ttu-id="2f02e-826">**NX_PTR_ERROR** (0x07) la sessione TLS o il puntatore del buffer non è valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-826">**NX_PTR_ERROR** (0x07) Invalid TLS session or buffer pointer.</span></span>
- <span data-ttu-id="2f02e-827">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0X12D) il buffer fornito è troppo piccolo.</span><span class="sxs-lookup"><span data-stu-id="2f02e-827">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="2f02e-828">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) il buffer era troppo piccolo per conservare il numero desiderato di certificati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-828">**NX_INVALID_PARAMETERS** (0x4D) The buffer was too small to hold the desired number of certificates.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-829">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-829">Allowed From</span></span>

<span data-ttu-id="2f02e-830">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-830">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-831">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-831">Example</span></span>

```C
/* Buffer space to hold the incoming certificates. */
#define CERTIFICATE_NUMBER    (2)
#define CERTIFICATE_SIZE      (2000)
#define BUFFER_SIZE          (CERTIFICATE_NUMBER * \
                                (sizeof(NX_SECURE_X509_CERT) + CERTIFICATE_SIZE))
UCHAR certificate_buffer[BUFFER_SIZE];

/* Enable X.509 Client verification and allocate certificate space in our TLS
   Server session.  */
status =  nx_secure_tls_session_x509_client_verify_configure(&tls_session,
                                                    CERTIFICATE_NUMBER,
                                                    certificate_buffer,
                                                    BUFFER_SIZE);


/* If status is NX_SUCCESS the buffer was successfully allocated.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-832">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-832">See Also</span></span>

- <span data-ttu-id="2f02e-833">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-833">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-834">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-834">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-835">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-835">nx_secure_tls_remote_certificate_buffer_allocate</span></span>

## <a name="nx_secure_tls_session_client_verify_disable"></a><span data-ttu-id="2f02e-836">nx_secure_tls_session_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="2f02e-836">nx_secure_tls_session_client_verify_disable</span></span>

<span data-ttu-id="2f02e-837">Disabilitare l'autenticazione del certificato client per una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-837">Disable Client Certificate Authentication for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-838">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-838">Prototype</span></span>

```C
UINT  nx_secure_tls_session_client_verify_disable(
                              NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="2f02e-839">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-839">Description</span></span>

<span data-ttu-id="2f02e-840">Questo servizio Disabilita l'autenticazione del certificato client per una sessione TLS specifica.</span><span class="sxs-lookup"><span data-stu-id="2f02e-840">This service disables Client Certificate Authentication for a specific TLS session.</span></span> <span data-ttu-id="2f02e-841">Per ulteriori informazioni, vedere nx_secure_tls_session_client_verify_enable.</span><span class="sxs-lookup"><span data-stu-id="2f02e-841">See nx_secure_tls_session_client_verify_enable for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-842">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-842">Parameters</span></span>

- <span data-ttu-id="2f02e-843">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-843">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-844">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-844">Return Values</span></span>

- <span data-ttu-id="2f02e-845">Modifica dello stato **NX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-845">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="2f02e-846">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-846">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-847">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-847">Allowed From</span></span>

<span data-ttu-id="2f02e-848">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-848">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-849">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-849">Example</span></span>

```C
/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_disable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will not
request certificates from the remote TLS client.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-850">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-850">See Also</span></span>

- <span data-ttu-id="2f02e-851">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="2f02e-851">nx_secure_tls_session_client_verify_enable</span></span>
- <span data-ttu-id="2f02e-852">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-852">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-853">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-853">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_client_verify_enable"></a><span data-ttu-id="2f02e-854">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="2f02e-854">nx_secure_tls_session_client_verify_enable</span></span>

<span data-ttu-id="2f02e-855">Abilitare l'autenticazione del certificato client per una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-855">Enable Client Certificate Authentication for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-856">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-856">Prototype</span></span>

```C
UINT  nx_secure_tls_session_client_verify_enable(
                                NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="2f02e-857">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-857">Description</span></span>

<span data-ttu-id="2f02e-858">Questo servizio Abilita l'autenticazione del certificato client per una sessione TLS specifica.</span><span class="sxs-lookup"><span data-stu-id="2f02e-858">This service enables Client Certificate Authentication for a specific TLS session.</span></span> <span data-ttu-id="2f02e-859">L'abilitazione dell'autenticazione del certificato client per un'istanza del server TLS farà sì che il server TLS richieda un certificato da qualsiasi client TLS remoto durante l'handshake TLS iniziale.</span><span class="sxs-lookup"><span data-stu-id="2f02e-859">Enabling Client Certificate Authentication for a TLS Server instance will cause the TLS Server to request a certificate from any remote TLS Client during the initial TLS handshake.</span></span> <span data-ttu-id="2f02e-860">Il certificato ricevuto dal client TLS remoto è accompagnato da un messaggio CertificateVerify, che il server TLS usa per verificare che il client sia proprietario del certificato (ha accesso alla chiave privata associata al certificato).</span><span class="sxs-lookup"><span data-stu-id="2f02e-860">The certificate received from the remote TLS Client is accompanied by a CertificateVerify message, which the TLS Server uses to verify that the Client owns the certificate (has access to the private key associated with that certificate).</span></span>

<span data-ttu-id="2f02e-861">Se il certificato fornito può essere verificato e ritracciato a un certificato nell'archivio certificati attendibili del server TLS tramite una catena di certificati X. 509, il client TLS remoto viene autenticato e l'handshake continua.</span><span class="sxs-lookup"><span data-stu-id="2f02e-861">If the provided certificate can be verified and traced back to a certificate in the TLS Server trusted certificate store via an X.509 certificate chain, the remote TLS Client is authenticated and the handshake proceeds.</span></span> <span data-ttu-id="2f02e-862">In caso di errori durante l'elaborazione del certificato o del messaggio CertificateVerify, l'handshake TLS termina con un errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-862">In case of any errors in processing the certificate or CertificateVerify message, the TLS handshake ends with an error.</span></span>

> [!NOTE]
> <span data-ttu-id="2f02e-863">*Il server TLS deve avere almeno un certificato nell'archivio attendibile aggiunto con nx_secure_tls_trusted_certificate_add o l'autenticazione avrà sempre esito negativo.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-863">*The TLS Server must have at least one certificate in its trusted store added with nx_secure_tls_trusted_certificate_add or authentication will always fail.*</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-864">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-864">Parameters</span></span>

- <span data-ttu-id="2f02e-865">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-865">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-866">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-866">Return Values</span></span>

- <span data-ttu-id="2f02e-867">Modifica dello stato **NX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-867">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="2f02e-868">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-868">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-869">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-869">Allowed From</span></span>

<span data-ttu-id="2f02e-870">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-870">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-871">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-871">Example</span></span>

```C
/* Add a trusted certificate so the TLS Server has something to verify against. */
status = nx_secure_tls_trusted_certificate_add(&tls_session,
                                               &trusted_certificate);

/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_enable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will now
request and verify certificates from the remote TLS client.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-872">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-872">See Also</span></span>

- <span data-ttu-id="2f02e-873">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="2f02e-873">nx_secure_tls_session_client_verify_enable</span></span>
- <span data-ttu-id="2f02e-874">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-874">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-875">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-875">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-876">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-876">nx_secure_tls_trusted_certificate_add</span></span>

## <a name="nx_secure_tls_session_create"></a><span data-ttu-id="2f02e-877">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-877">nx_secure_tls_session_create</span></span>

<span data-ttu-id="2f02e-878">Creare una sessione TLS sicura NetX per le comunicazioni sicure</span><span class="sxs-lookup"><span data-stu-id="2f02e-878">Create a NetX Secure TLS Session for secure communications</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-879">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-879">Prototype</span></span>

```C
UINT  nx_secure_tls_session_create(NX_SECURE_TLS_SESSION *session_ptr
                                   NX_SECURE_TLS_CRYPTO *cipher_table,
                                   VOID *encryption_metadata_area,
                                   ULONG encryption_metadata_size);
```

### <a name="description"></a><span data-ttu-id="2f02e-880">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-880">Description</span></span>

<span data-ttu-id="2f02e-881">Questo servizio Inizializza un'istanza della struttura NX_SECURE_TLS_SESSION da usare per stabilire comunicazioni TLS sicure su una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="2f02e-881">This service initializes an NX_SECURE_TLS_SESSION structure instance for use in establishing secure TLS communications over a network connection.</span></span>

<span data-ttu-id="2f02e-882">Il metodo accetta un oggetto NX_SECURE_TLS_CRYPTO popolato con i metodi di crittografia disponibili da usare per TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-882">The method takes a NX_SECURE_TLS_CRYPTO object that is populated with the available cryptographic methods to be used for TLS.</span></span> <span data-ttu-id="2f02e-883">Il *encryption_metadata_area* punta a un buffer allocato per l'uso da parte di TLS per i "metadati" usati dai metodi crittografici nella tabella NX_SECURE_TLS_CRYPTO per i calcoli.</span><span class="sxs-lookup"><span data-stu-id="2f02e-883">The *encryption_metadata_area* points to a buffer allocated for use by TLS for the "metadata" used by the cryptographic methods in the NX_SECURE_TLS_CRYPTO table for calculations.</span></span> <span data-ttu-id="2f02e-884">È possibile determinare le dimensioni della tabella utilizzando il servizio nx_secure_tls_metadata_size_calculate.</span><span class="sxs-lookup"><span data-stu-id="2f02e-884">The size of the table can be determined by using the nx_secure_tls_metadata_size_calculate service.</span></span> <span data-ttu-id="2f02e-885">Per altri dettagli, vedere la sezione "crittografia in NetX Secure TLS" nel capitolo 3.</span><span class="sxs-lookup"><span data-stu-id="2f02e-885">See the section "Cryptography in NetX Secure TLS" in Chapter 3 for more details.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-886">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-886">Parameters</span></span>

- <span data-ttu-id="2f02e-887">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-887">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-888">**cipher_table** Puntatore ai metodi di crittografia TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-888">**cipher_table** Pointer to TLS cryptographic methods.</span></span>
- <span data-ttu-id="2f02e-889">**encryption_metadata_area** Puntatore allo spazio per i metadati di crittografia.</span><span class="sxs-lookup"><span data-stu-id="2f02e-889">**encryption_metadata_area** Pointer to space for cryptography metadata.</span></span>
- <span data-ttu-id="2f02e-890">**encryption_metadata_size** Dimensioni del buffer dei metadati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-890">**encryption_metadata_size** Size of the metadata buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-891">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-891">Return Values</span></span>

- <span data-ttu-id="2f02e-892">**NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-892">**NX_SUCCESS** (0x00)Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="2f02e-893">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-893">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="2f02e-894">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) il buffer dei metadati è troppo piccolo per i metodi specificati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-894">**NX_INVALID_PARAMETERS** (0x4D) The metadata buffer was too small for the given methods.</span></span>
- <span data-ttu-id="2f02e-895">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0X106) un metodo di crittografia obbligatorio per la versione abilitata di TLS non è stato fornito nella tabella di crittografia.</span><span class="sxs-lookup"><span data-stu-id="2f02e-895">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A required cipher method for the enabled version of TLS was not supplied in the cipher table.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-896">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-896">Allowed From</span></span>

<span data-ttu-id="2f02e-897">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-897">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-898">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-898">Example</span></span>

```C
/* Reference the platform-specific TLS cryptographic method table. */
extern const NX_SECURE_TLS_CRYPTO nx_crypto_tls_ciphers;

/* Declare a buffer for the cryptographic metadata. The size should be calculated
   using nx_secure_tls_metadata_size_calculate. */
UCHAR crypto_metadata[4500];

/* Initialize TLS session.  */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* If status is NX_SUCCESS the TLS Session was successfully initialized.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-899">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-899">See Also</span></span>

- <span data-ttu-id="2f02e-900">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-900">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-901">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="2f02e-901">nx_secure_tls_metadata_size_calculate</span></span>
- <span data-ttu-id="2f02e-902">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-902">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-903">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-903">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-904">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="2f02e-904">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="2f02e-905">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-905">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="2f02e-906">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-906">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="2f02e-907">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-907">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="2f02e-908">Crittografia in NetX Secure TLS nel capitolo 3</span><span class="sxs-lookup"><span data-stu-id="2f02e-908">Cryptography in NetX Secure TLS in Chapter 3</span></span>

## <a name="nx_secure_tls_session_delete"></a><span data-ttu-id="2f02e-909">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-909">nx_secure_tls_session_delete</span></span>

<span data-ttu-id="2f02e-910">Eliminare una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-910">Delete a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-911">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-911">Prototype</span></span>

```C
UINT  nx_secure_tls_session_delete(NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="2f02e-912">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-912">Description</span></span>

<span data-ttu-id="2f02e-913">Questo servizio Elimina una sessione TLS rappresentata da un'istanza della struttura NX_SECURE_TLS_SESSION e rilascia tutte le risorse di sistema di proprietà di tale istanza di sessione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-913">This service deletes a TLS session represented by an NX_SECURE_TLS_SESSION structure instance and releases all system resources owned by that session instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-914">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-914">Parameters</span></span>

- <span data-ttu-id="2f02e-915">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-915">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-916">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-916">Return Values</span></span>

- <span data-ttu-id="2f02e-917">**NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-917">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="2f02e-918">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-918">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-919">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-919">Allowed From</span></span>

<span data-ttu-id="2f02e-920">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-920">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-921">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-921">Example</span></span>

```C
/* Delete TLS session.  */
status =  nx_secure_tls_session_delete(&tls_session);


/* If status is NX_SUCCESS the TLS Session was successfully deleted.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-922">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-922">See Also</span></span>

- <span data-ttu-id="2f02e-923">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-923">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-924">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-924">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-925">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-925">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-926">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="2f02e-926">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="2f02e-927">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-927">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="2f02e-928">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-928">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="2f02e-929">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-929">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_end"></a><span data-ttu-id="2f02e-930">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="2f02e-930">nx_secure_tls_session_end</span></span>

<span data-ttu-id="2f02e-931">Terminare una sessione TLS protetta NetX attiva</span><span class="sxs-lookup"><span data-stu-id="2f02e-931">End an active NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-932">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-932">Prototype</span></span>

```C
UINT  nx_secure_tls_session_end(NX_SECURE_TLS_SESSION *session_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="2f02e-933">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-933">Description</span></span>

<span data-ttu-id="2f02e-934">Questo servizio termina una sessione TLS rappresentata da un'istanza della struttura NX_SECURE_TLS_SESSION inviando il messaggio TLS CloseNotify all'host remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-934">This service ends a TLS session represented by an NX_SECURE_TLS_SESSION structure instance by sending the TLS CloseNotify message to the remote host.</span></span> <span data-ttu-id="2f02e-935">Il servizio attende quindi che l'host remoto risponda con il proprio messaggio CloseNotify.</span><span class="sxs-lookup"><span data-stu-id="2f02e-935">The service then waits for the remote host to respond with its own CloseNotify message.</span></span>

<span data-ttu-id="2f02e-936">Se l'host remoto non invia un messaggio CloseNotify, TLS considera un errore e una possibile violazione della sicurezza, quindi il controllo del valore restituito è importante per una connessione protetta.</span><span class="sxs-lookup"><span data-stu-id="2f02e-936">If the remote host does not send a CloseNotify message, TLS considers this an error and a possible security breach, so checking the return value is important for a secure connection.</span></span> <span data-ttu-id="2f02e-937">Il parametro **WAIT_OPTION** può essere utilizzato per controllare per quanto tempo il servizio deve attendere la risposta prima di restituire il controllo al thread chiamante.</span><span class="sxs-lookup"><span data-stu-id="2f02e-937">The **wait_option** parameter can be used to control how long the service should wait for the response before returning control to the calling thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-938">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-938">Parameters</span></span>

- <span data-ttu-id="2f02e-939">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-939">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-940">**WAIT_OPTION** Indica per quanto tempo il servizio deve attendere la risposta dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-940">**wait_option** Indicates how long the service should wait for the response from the remote host.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-941">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-941">Return Values</span></span>

- <span data-ttu-id="2f02e-942">**NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-942">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="2f02e-943">**NX_SECURE_TLS_NO_CLOSE_RESPONSE** (0x113) non ha ricevuto una risposta dall'host remoto prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="2f02e-943">**NX_SECURE_TLS_NO_CLOSE_RESPONSE** (0x113) Did not receive a response from the remote host before timing out.</span></span>
- <span data-ttu-id="2f02e-944">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) non è in grado di allocare un pacchetto per l'invio del messaggio CloseNotify.</span><span class="sxs-lookup"><span data-stu-id="2f02e-944">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Could not allocate a packet to send the CloseNotify message.</span></span>
- <span data-ttu-id="2f02e-945">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) non è in grado di inviare il messaggio CloseNotify sul socket TCP.</span><span class="sxs-lookup"><span data-stu-id="2f02e-945">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Could not send the CloseNotify message over the TCP socket.</span></span>
- <span data-ttu-id="2f02e-946">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-946">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-947">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-947">Allowed From</span></span>

<span data-ttu-id="2f02e-948">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-948">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-949">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-949">Example</span></span>

```C
/* End TLS session.  */
status =  nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the TLS Session was successfully ended.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-950">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-950">See Also</span></span>

- <span data-ttu-id="2f02e-951">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-951">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-952">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-952">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-953">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-953">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-954">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-954">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="2f02e-955">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-955">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="2f02e-956">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-956">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="2f02e-957">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-957">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_packet_buffer_set"></a><span data-ttu-id="2f02e-958">nx_secure_tls_session_packet_buffer_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-958">nx_secure_tls_session_packet_buffer_set</span></span>

<span data-ttu-id="2f02e-959">Impostare il buffer di riassemblaggio dei pacchetti per una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-959">Set the packet reassembly buffer for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-960">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-960">Prototype</span></span>

```C
UINT  nx_secure_tls_session_packet_buffer_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *buffer_ptr,
                                    ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="2f02e-961">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-961">Description</span></span>

<span data-ttu-id="2f02e-962">Questo servizio associa un buffer di riassemblaggio del pacchetto a una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-962">This service associates a packet reassembly buffer to a TLS session.</span></span> <span data-ttu-id="2f02e-963">Per decrittografare e analizzare i record TLS in ingresso, è necessario assemblare i dati in ogni record dai pacchetti TCP sottostanti.</span><span class="sxs-lookup"><span data-stu-id="2f02e-963">In order to decrypt and parse incoming TLS records, the data in each record must be assembled from the underlying TCP packets.</span></span> <span data-ttu-id="2f02e-964">I record TLS possono avere dimensioni fino a 16KB, anche se in genere sono molto più piccoli, quindi potrebbero non rientrare in un singolo pacchetto TCP.</span><span class="sxs-lookup"><span data-stu-id="2f02e-964">TLS records can be up to 16KB in size (though typically are much smaller) so may not fit into a single TCP packet.</span></span>

<span data-ttu-id="2f02e-965">Se si è certi che le dimensioni del messaggio in ingresso saranno inferiori al limite dei record TLS di 16KB, le dimensioni del buffer possono essere rese più piccole, ma per gestire i dati in ingresso sconosciuti il buffer deve essere reso il più grande possibile.</span><span class="sxs-lookup"><span data-stu-id="2f02e-965">If you know the incoming message size will be smaller than the TLS record limit of 16KB, the buffer size can be made smaller, but in order to handle unknown incoming data the buffer should be made as large as possible.</span></span> <span data-ttu-id="2f02e-966">Se un record in ingresso è più grande del buffer fornito, la sessione TLS termina con un errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-966">If an incoming record is larger than the supplied buffer, the TLS session will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-967">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-967">Parameters</span></span>

- <span data-ttu-id="2f02e-968">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-968">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-969">**buffer_ptr** Puntatore al buffer usato da TLS per il riassemblaggio dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="2f02e-969">**buffer_ptr** Pointer to buffer for TLS to use for packet reassembly.</span></span>
- <span data-ttu-id="2f02e-970">**BUFFER_SIZE** Dimensioni in byte del buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-970">**buffer_size** Size of the supplied buffer in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-971">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-971">Return Values</span></span>

- <span data-ttu-id="2f02e-972">**NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-972">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="2f02e-973">Il puntatore della sessione TLS o il buffer di **NX_INVALID_PARAMETERS** (irreversibile 0x4D) non è valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-973">**NX_INVALID_PARAMETERS** (0x4D) Invalid buffer or TLS session pointer.</span></span>
- <span data-ttu-id="2f02e-974">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-974">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-975">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-975">Allowed From</span></span>

<span data-ttu-id="2f02e-976">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-976">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-977">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-977">Example</span></span>

```C
/* Buffer for TLS packet reassembly. */
UCHAR tls_packet_buffer[16384];
/* Assign buffer to TLS session.  */
status =  nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                  sizeof(tls_packet_buffer));


/* If status is NX_SUCCESS the buffer was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-978">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-978">See Also</span></span>

- <span data-ttu-id="2f02e-979">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-979">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-980">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-980">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-981">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-981">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-982">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-982">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="2f02e-983">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-983">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="2f02e-984">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-984">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="2f02e-985">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-985">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_protocol_version_override"></a><span data-ttu-id="2f02e-986">nx_secure_tls_session_protocol_version_override</span><span class="sxs-lookup"><span data-stu-id="2f02e-986">nx_secure_tls_session_protocol_version_override</span></span>

<span data-ttu-id="2f02e-987">Eseguire l'override della versione del protocollo TLS predefinita per una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-987">Override the default TLS protocol version for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-988">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-988">Prototype</span></span>

```C
UINT  nx_secure_tls_session_protocol_version_override(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              USHORT protocol_version);
```

### <a name="description"></a><span data-ttu-id="2f02e-989">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-989">Description</span></span>

<span data-ttu-id="2f02e-990">Questo servizio esegue l'override della versione del protocollo TLS predefinita (più recente) utilizzata da una determinata sessione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-990">This service overrides the default (newest) TLS protocol version used by a particular session.</span></span> <span data-ttu-id="2f02e-991">Questo consente a NetX Secure TLS di usare una versione precedente di TLS per una sessione TLS specifica senza disabilitare le versioni più recenti di TLS in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-991">This enables NetX Secure TLS to use an older version of TLS for a specific TLS Session without disabling newer TLS versions at compile time.</span></span> <span data-ttu-id="2f02e-992">Questa operazione può essere utile nelle applicazioni che possono avere la necessità di comunicare con un host precedente che non supporta la versione più recente di TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-992">This may be useful in applications that may need to communicate with an older host that does not support the newest version of TLS.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f02e-993">*A partire dalla versione 5.11 SP3, NetX Secure TLS supporta RFC 7507 (vedere la nota di seguito) e qualsiasi override a una versione precedente con questa API determinerà l'invio di un SCSV di fallback in ClientHello. Se il server supporta una versione più recente di TLS e il SCSV di fallback è incluso in ClientHello, il server interromperà l'handshake TLS con un avviso "fallback non appropriato". SCSV viene inviato solo quando l'override della versione è una versione precedente di TLS rispetto a quella abilitata (ad esempio, se si sostituisce la versione a TLS 1,2, non verrà inviato alcun SCSV).*</span><span class="sxs-lookup"><span data-stu-id="2f02e-993">*As of version 5.11SP3, NetX Secure TLS supports RFC 7507 (see note below) and any override to an older version with this API will result in a fallback SCSV being sent in the ClientHello. If the server supports a newer version of TLS and the fallback SCSV is included in the ClientHello, that server will abort the TLS handshake with an "Inappropriate Fallback" alert. The SCSV is only sent when the version override is an older version of TLS than is enabled (e.g. if you override the version to TLS 1.2, no SCSV will be sent).*</span></span>

<span data-ttu-id="2f02e-994">I valori validi per il parametro protocol_version sono le macro seguenti: NX_SECURE_TLS_VERSION_TLS_1_0, NX_SECURE_TLS_VERSION_TLS_1_1 e NX_SECURE_TLS_VERSION_TLS_1_2.</span><span class="sxs-lookup"><span data-stu-id="2f02e-994">Valid values for the protocol_version parameter are the following macros: NX_SECURE_TLS_VERSION_TLS_1_0, NX_SECURE_TLS_VERSION_TLS_1_1, and NX_SECURE_TLS_VERSION_TLS_1_2.</span></span>

<span data-ttu-id="2f02e-995">Le macro NX_SECURE_TLS_DISABLE_TLS_1_1 e NX_SECURE_TLS_ENABLE_TLS_1_0 possono essere usate per controllare le versioni di TLS compilate nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-995">The macros NX_SECURE_TLS_DISABLE_TLS_1_1 and NX_SECURE_TLS_ENABLE_TLS_1_0 can be used to control the versions of TLS that are compiled into the application.</span></span> <span data-ttu-id="2f02e-996">La versione 1,2 di TLS è sempre abilitata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-996">TLS version 1.2 is always enabled.</span></span>

<span data-ttu-id="2f02e-997">Si noti che se l'host remoto non supporta la versione fornita, la connessione avrà esito negativo. solo la versione di sostituzione fornita verrà negoziata da NetX Secure TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-997">Note that if the remote host does not support the supplied version, the connection will fail – only the supplied override version will be negotiated by NetX Secure TLS.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f02e-998">RFC 7507: SCSV di fallback TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-998">RFC 7507: TLS Fallback SCSV.</span></span> <span data-ttu-id="2f02e-999">Questa RFC è stata introdotta per attenuare un problema di sicurezza che era originariamente causato da server che gestivano in modo errato la negoziazione del downgrade del protocollo e che invece rifiutavano messaggi ClientHello validi.</span><span class="sxs-lookup"><span data-stu-id="2f02e-999">This RFC was introduced to mitigate a security problem that was originally caused by servers that improperly handled protocol downgrade negotiation and instead rejected otherwise valid ClientHello messages.</span></span> <span data-ttu-id="2f02e-1000">Nel tentativo di mantenere la compatibilità con questi server obsoleti, alcune applicazioni client TLS hanno iniziato a ritentare gli handshake non riusciti con una versione precedente di TLS (ad esempio, TLS 1,2 non è riuscita, quindi provare TLS 1,1).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1000">In an attempt to remain compatible with these old servers, some TLS client applications started to retry failed handshakes with and older TLS version (e.g. TLS 1.2 failed so try TLS 1.1).</span></span> <span data-ttu-id="2f02e-1001">Questa soluzione ha tuttavia introdotto un nuovo problema: un utente malintenzionato potrebbe forzare il downgrade di un client introducendo artificialmente un errore di rete o di pacchetto che causa la mancata connessione del server, anche quando il server supporta la versione più recente di TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1001">This workaround however introduced a new problem – an attacker could force a client to downgrade by artificially introducing a network or packet error causing the server connection to fail – even when the server supported the newer TLS version.</span></span> <span data-ttu-id="2f02e-1002">Effettuando il downgrade a una versione precedente, l'autore dell'attacco potrebbe sfruttare i punti deboli in tale versione (SSLv3<sup>21</sup> in particolare è debole per l'attacco Poodle).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1002">By downgrading to an older version the attacker could exploit weaknesses in that version (SSLv3<sup>21</sup> in particular is weak to the POODLE attack).</span></span> <span data-ttu-id="2f02e-1003">Per evitare questa situazione, RFC 7507 introdued "fallback SCSV", uno pseudo-ciphersuite<sup>22</sup> inviato nel ClientHello che notifica a un server TLS quando un client TLS usa una versione di TLS che non è la versione più recente supportata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1003">To prevent this situation, RFC 7507 introdued the "fallback SCSV," a pseudo-ciphersuite<sup>22</sup> sent in the ClientHello that notifies a TLS server when a TLS client is using a TLS version that is not the newest version it supports.</span></span> <span data-ttu-id="2f02e-1004">In questo modo, un server che supporta una versione più recente può rifiutare un ClientHello contenente il SCSV di fallback e impedire che il downgrade venga eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1004">This way, a server that supports a newer version can reject a ClientHello containing the fallback SCSV and prevent the downgrade attack from succeeding.</span></span>

21. <span data-ttu-id="2f02e-1005">NetX Secure non implementa SSLv3 a causa dell'esistenza di debolezze gravi note, ad esempio POODLE.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1005">NetX Secure does not implement SSLv3 due to the existence of known serious weaknesses such as POODLE.</span></span>

22. <span data-ttu-id="2f02e-1006">Un ciphersuite, o SCSV (signaling Cipher Suite value), è un numero ciphersuite riservato usato per segnalare le implementazioni TLS abilitate sulle funzionalità non disponibili nelle versioni precedenti di TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1006">A pseudo-ciphersuite, or SCSV (Signaling Cipher Suite Value), is a reserved ciphersuite number that is used to signal enabled TLS implementations about features that were not available in older TLS versions.</span></span> <span data-ttu-id="2f02e-1007">I SCSV di fallback e i TLS_EMPTY_RENEGOTIATION_INFO_SCSV (RFC 5746) sono esempi.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1007">The fallback SCSV and the TLS_EMPTY_RENEGOTIATION_INFO_SCSV (RFC 5746) are examples.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1008">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1008">Parameters</span></span>

- <span data-ttu-id="2f02e-1009">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1009">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1010">**protocol_version** Macro della versione TLS per la versione specifica di TLS da usare.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1010">**protocol_version** TLS version macro for the specific TLS version to use.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1011">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1011">Return Values</span></span>

- <span data-ttu-id="2f02e-1012">Modifica dello stato **NX_SUCCESS** (0x00) riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1012">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="2f02e-1013">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1013">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="2f02e-1014">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) versione TLS nota ma non supportata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1014">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) Known but unsupported TLS version.</span></span>
- <span data-ttu-id="2f02e-1015">La versione del protocollo **NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0X10F) non è valida.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1015">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Invalid protocol version.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1016">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1016">Allowed From</span></span>

<span data-ttu-id="2f02e-1017">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1017">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1018">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1018">Example</span></span>

```C
/* Set the protocol version to be used to TLSv1.1. */
status = nx_secure_tls_session_protocol_version_override(&tls_session,
                                              NX_SECURE_TLS_VERSION_TLS_1_1);

/* This TLS Session will use TLSv1.1 for the handshake and TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1019">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1019">See Also</span></span>

- <span data-ttu-id="2f02e-1020">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-1020">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-1021">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1021">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_receive"></a><span data-ttu-id="2f02e-1022">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-1022">nx_secure_tls_session_receive</span></span>

<span data-ttu-id="2f02e-1023">Ricevere dati da una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-1023">Receive data from a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1024">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1024">Prototype</span></span>

```C
UINT  nx_secure_tls_session_receive(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="2f02e-1025">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1025">Description</span></span>

<span data-ttu-id="2f02e-1026">Questo servizio riceve i dati dalla sessione TLS attiva specificata, gestendo la decrittografia dei dati prima di fornirli al chiamante nel parametro NX_PACKET.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1026">This service receives data from the specified active TLS session, handling the decryption of that data before providing it to the caller in the NX_PACKET parameter.</span></span> <span data-ttu-id="2f02e-1027">Se nella sessione specificata non viene accodato alcun dato, la chiamata viene sospesa in base all'opzione wait fornita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1027">If no data is queued in the specified session, the call suspends based on the supplied wait option.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f02e-1028">*Se viene restituito NX_SUCCESS, l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-1028">*If NX_SUCCESS is returned, the application is responsible for releasing the received packet when it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1029">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1029">Parameters</span></span>

- <span data-ttu-id="2f02e-1030">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1030">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1031">**packet_ptr** Puntatore a un puntatore di pacchetto TLS allocato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1031">**packet_ptr** Pointer to an allocated TLS packet pointer.</span></span>
- <span data-ttu-id="2f02e-1032">**WAIT_OPTION** Indica per quanto tempo il servizio deve attendere un pacchetto dall'host remoto prima della restituzione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1032">**wait_option** Indicates how long the service should wait for a packet from the remote host before returning.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1033">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1033">Return Values</span></span>

- <span data-ttu-id="2f02e-1034">**NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1034">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="2f02e-1035">**NX_NO_PACKET** (0x01) non sono stati ricevuti dati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1035">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="2f02e-1036">**NX_NOT_CONNECTED** (0X38) il socket TCP sottostante non è più connesso.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1036">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="2f02e-1037">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0X108) un messaggio ricevuto non ha superato un controllo hash di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1037">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A received message failed an authentication hash check.</span></span>
- <span data-ttu-id="2f02e-1038">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0X10F) un messaggio ricevuto contiene una versione del protocollo sconosciuta nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1038">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received message contained an unknown protocol version in its header.</span></span>
- <span data-ttu-id="2f02e-1039">**NX_SECURE_TLS_ALERT_RECEIVED** (0X114) ha ricevuto un avviso TLS dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1039">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Received a TLS alert from the remote host.</span></span>
- <span data-ttu-id="2f02e-1040">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1040">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="2f02e-1041">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0X101) la sessione TLS specificata non è stata inizializzata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1041">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1042">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1042">Allowed From</span></span>

<span data-ttu-id="2f02e-1043">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1043">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1044">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1044">Example</span></span>

```C
/* Receive a packet from an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is received, blocking otherwise.
*/
status =  nx_secure_tls_session_receive(&tls_session, &packet_ptr,
NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the received packet is pointed to by  "packet_ptr". */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1045">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1045">See Also</span></span>

- <span data-ttu-id="2f02e-1046">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-1046">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="2f02e-1047">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-1047">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-1048">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1048">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-1049">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-1049">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-1050">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-1050">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="2f02e-1051">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-1051">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="2f02e-1052">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="2f02e-1052">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="2f02e-1053">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1053">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_renegotiate_callback_set"></a><span data-ttu-id="2f02e-1054">nx_secure_tls_session_renegotiate_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1054">nx_secure_tls_session_renegotiate_callback_set</span></span>

<span data-ttu-id="2f02e-1055">Assegnare un callback che verrà richiamato all'inizio di una rinegoziazione della sessione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1055">Assign a callback that will be invoked at the beginning of a session renegotiation</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1056">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1056">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_renegotiate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(struct NX_SECURE_TLS_SESSION_struct
                  *session));
```

### <a name="description"></a><span data-ttu-id="2f02e-1057">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1057">Description</span></span>

<span data-ttu-id="2f02e-1058">Questo servizio assegna un callback a una sessione TLS che verrà richiamata ogni volta che il primo messaggio di handshake di rinegoziazione della sessione viene ricevuto dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1058">This service assigns a callback to a TLS session that will be invoked whenever the first message of a session renegotiation handshake is received from the remote host.</span></span>

<span data-ttu-id="2f02e-1059">La funzione di callback è concepita come una notifica all'applicazione a partire dall'inizio di un handshake di rinegoziazione. l'applicazione può scegliere di terminare la sessione TLS restituendo qualsiasi valore diverso da zero dal callback, in modo che TLS concluda la sessione TLS con un errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1059">The callback function is intended as a notification to the application that a renegotiation handshake is beginning – the application may choose to terminate the TLS session by returning any non-zero value from the callback which will cause TLS to end the TLS session with an error.</span></span> <span data-ttu-id="2f02e-1060">Se l'applicazione desidera procedere con la rinegoziazione, il callback deve restituire NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1060">If the application wishes to proceed with the renegotiation, the callback should return NX_SUCCESS.</span></span>

> [!NOTE]
> <span data-ttu-id="2f02e-1061">*A causa della semantica di rinegoziazione TLS, viene richiamato il callback per i client TLS sicuri NetX ogni volta che un HelloRequest viene ricevuto dal server remoto, ma non quando il client avvia la rinegoziazione. In NetX Secure TLS Servers, il callback verrà richiamato ogni volta che viene ricevuta una rinegoziazione ClientHello (qualsiasi ClientHello ricevuto nel contesto di una sessione TLS attiva). Ciò significa che il callback verrà richiamato se l'host remoto o l'applicazione locale ha avviato la rinegoziazione perché il server TLS invierà una HelloRequest a cui il client remoto risponderà.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-1061">*Due to the semantics of TLS renegotiation, the callback will be invoked for NetX Secure TLS Clients whenever a HelloRequest is received from the remote server, but not when the client initiates the renegotiation. On NetX Secure TLS Servers, the callback will be invoked whenever a renegotiation ClientHello is received (any ClientHello received in the context of an active TLS session). This means that the callback will be invoked whether the remote host or the local application has initiated the renegotiation because the TLS server will send a HelloRequest to which the remote client will respond.*</span></span>

<span data-ttu-id="2f02e-1062">NetX Secure TLS implementa l'estensione Inidication di rinegoziazione sicura da RFC 5746 per assicurarsi che gli handshake di rinegoziazione non siano soggetti a attacchi man-in-the-Middle.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1062">NetX Secure TLS implements the Secure Renegotiation Inidication Extension from RFC 5746 to ensure that renegotiation handshakes are not subject to man-in-the-middle attacks.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1063">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1063">Parameters</span></span>

- <span data-ttu-id="2f02e-1064">**session_ptr** Puntatore all'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1064">**session_ptr** Pointer to TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1065">**func_ptr** Puntatore alla funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1065">**func_ptr** Pointer to callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1066">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1066">Return Values</span></span>

- <span data-ttu-id="2f02e-1067">**NX_SUCCESS** (0x00) assegnazione riuscita del callback.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1067">**NX_SUCCESS** (0x00) Successful assignment of callback.</span></span>
- <span data-ttu-id="2f02e-1068">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido per la funzione di callback o la sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1068">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer for the callback function or TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1069">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1069">Allowed From</span></span>

<span data-ttu-id="2f02e-1070">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1070">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1071">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1071">Example</span></span>

```C
/* Simple callback notifying the user that a renegotiation is starting. */
ULONG tls_renegotiation_callback(NX_SECURE_TLS_SESSION *session)
{
    printf("Renegotiation initiated by remote host\n");

    return(NX_SUCCESS);
}

/* Establish a TLS session with a remote host (TLS Client) */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* Set callback for renegotiation notification. */
status = nx_secure_tls_session_renegotiate_callback_set(&tls_session,
                                                tls_renegotiation_callback);
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1072">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1072">See Also</span></span>

- <span data-ttu-id="2f02e-1073">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1073">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-1074">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-1074">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-1075">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-1075">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="2f02e-1076">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-1076">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="2f02e-1077">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1077">nx_secure_tls_session_renegotiate</span></span>

## <a name="nx_secure_tls_session_renegotiate"></a><span data-ttu-id="2f02e-1078">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1078">nx_secure_tls_session_renegotiate</span></span>

<span data-ttu-id="2f02e-1079">Avviare un handshake di rinegoziazione della sessione con l'host remoto</span><span class="sxs-lookup"><span data-stu-id="2f02e-1079">Initiate a session renegotiation handshake with the remote host</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1080">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1080">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_renegotiate (
                  NX_SECURE_TLS_SESSION *tls_session,
                  UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="2f02e-1081">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1081">Description</span></span>

<span data-ttu-id="2f02e-1082">Questo servizio avvia un handshake di *rinegoziazione* della sessione con un host TLS remoto connesso.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1082">This service initiates a session *renegotiation* handshake with a connected remote TLS host.</span></span> <span data-ttu-id="2f02e-1083">Una rinegoziazione è costituita da un secondo handshake TLS all'interno del contesto di una sessione TLS stabilita in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1083">A renegotiation consists of a second TLS handshake within the context of a previously-established TLS session.</span></span> <span data-ttu-id="2f02e-1084">Ogni nuovo messaggio di handshake viene crittografato usando la sessione TLS finché non vengono generate nuove chiavi di sessione e vengono scambiati i messaggi ChangeCipherSpec, a quel punto le nuove chiavi vengono usate per crittografare tutti i messaggi.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1084">Each of the new handshake messages is encrypted using the TLS session until new session keys are generated and ChangeCipherSpec messages are exchanged, at which time the new keys are used to encrypt all messages.</span></span>

<span data-ttu-id="2f02e-1085">Una rinegoziazione può essere avviata in qualsiasi momento dopo che è stata stabilita una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1085">A renegotiation can be initiated at any time once a TLS session is established.</span></span> <span data-ttu-id="2f02e-1086">Se viene effettuato un tentativo di rinegoziazione durante un handshake TLS o prima che venga stabilita una sessione TLS, non verrà eseguita alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1086">If a renegotiation is attempted during a TLS handshake or before a TLS session is established no action will be taken.</span></span>

> [!NOTE]
> <span data-ttu-id="2f02e-1087">*Quando il servizio viene richiamato, viene eseguito un handshake TLS intero, quindi il tempo per il completamento e lo stato restituito variano a seconda delle impostazioni TLS correnti e dei parametri di sessione.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-1087">*An entire TLS handshake will be performed when this service is invoked so the time to completion and returned status will vary depending on the current TLS settings and session parameters.*</span></span>

<span data-ttu-id="2f02e-1088">NetX Secure TLS implementa l'estensione Inidication di rinegoziazione sicura da RFC 5746 per assicurarsi che gli handshake di rinegoziazione non siano soggetti a attacchi man-in-the-Middle.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1088">NetX Secure TLS implements the Secure Renegotiation Inidication Extension from RFC 5746 to ensure that renegotiation handshakes are not subject to man-in-the-middle attacks.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1089">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1089">Parameters</span></span>

- <span data-ttu-id="2f02e-1090">**session_ptr** Puntatore all'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1090">**session_ptr** Pointer to TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1091">**WAIT_OPTION** Indica per quanto tempo il servizio deve attendere un pacchetto dall'host remoto prima della restituzione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1091">**wait_option** Indicates how long the service should wait for a packet from the remote host before returning.</span></span> <span data-ttu-id="2f02e-1092">Viene passato a tutti i servizi NetX in TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1092">This is passed to all NetX services within TLS.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1093">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1093">Return Values</span></span>

- <span data-ttu-id="2f02e-1094">**NX_SUCCESS** (0x00) rinegoziazioni riuscite.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1094">**NX_SUCCESS** (0x00) Successful renegotiation.</span></span>
- <span data-ttu-id="2f02e-1095">**NX_NO_PACKET** (0x01) non sono stati ricevuti dati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1095">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="2f02e-1096">**NX_NOT_CONNECTED** (0X38) il socket TCP sottostante non è più connesso.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1096">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="2f02e-1097">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0X108) un messaggio ricevuto non ha superato un controllo hash di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1097">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A received message failed an authentication hash check.</span></span>
- <span data-ttu-id="2f02e-1098">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0X10F) un messaggio ricevuto contiene una versione del protocollo sconosciuta nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1098">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received message contained an unknown protocol version in its header.</span></span>
- <span data-ttu-id="2f02e-1099">**NX_SECURE_TLS_ALERT_RECEIVED** (0X114) ha ricevuto un avviso TLS dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1099">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Received a TLS alert from the remote host.</span></span>
- <span data-ttu-id="2f02e-1100">**NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE** (0X134) la sessione TLS locale o remota è inattiva, rendendo impossibile la rinegoziazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1100">**NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE** (0x134) The local or remote TLS session is inactive, making renegotiation impossible.</span></span>
- <span data-ttu-id="2f02e-1101">**NX_SECURE_TLS_RENEGOTIATION_FAILURE** (0X13A) l'host remoto non ha fornito l'estensione SCSV o di rinegoziazione sicura e pertanto non è possibile eseguire la rinegoziazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1101">**NX_SECURE_TLS_RENEGOTIATION_FAILURE** (0x13A) The remote host did not provide either the SCSV or Secure Renegotiation Extension and thus renegotiation cannot be performed.</span></span>
- <span data-ttu-id="2f02e-1102">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1102">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="2f02e-1103">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0X101) la sessione TLS specificata non è stata inizializzata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1103">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>
- <span data-ttu-id="2f02e-1104">L'allocazione del pacchetto sottostante **NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1104">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Underlying packet allocation failed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1105">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1105">Allowed From</span></span>

<span data-ttu-id="2f02e-1106">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1106">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1107">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1107">Example</span></span>

```C
/* Establish a TLS session with a remote host (TLS Client) */
status =  nx_secure_tls_session_create(&tls_session,
                                       &nx_crypto_tls_ciphers,
                                       crypto_metadata,
                                       sizeof(crypto_metadata));


/* Setup a client socket connection.  */
status = nx_tcp_client_socket_connect(&tcp_socket, server_ipv4_address,
REMOTE_SERVER_PORT, NX_WAIT_FOREVER);

/* Start the TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);

/* Send some data in the first TLS session. (Check “status” for errors…)*/
status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                       NX_WAIT_FOREVER);
status = nx_packet_data_append(send_packet, "Hello there!\r\n", 14, &pool_0,
                               NX_WAIT_FOREVER);
status = nx_secure_tls_session_send(&tls_session, send_packet,
                                    NX_IP_PERIODIC_RATE);

/* Now renegotiate the session. */
status  = nx_secure_tls_session_renegotiate(&tls_session, NX_WAIT_FOREVER);

/* If status == NX_SUCCESS, new TLS session keys have been generated. */

/* Send some data in the new TLS session. This will be encrypted using the new
   keys. */
status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &send_packet,
                                       NX_WAIT_FOREVER);
status = nx_packet_data_append(send_packet, "Another message…\r\n", 18, &pool_0,
                               NX_WAIT_FOREVER);
status = nx_secure_tls_session_send(&tls_session, send_packet,
                                    NX_IP_PERIODIC_RATE);
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1108">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1108">See Also</span></span>

- <span data-ttu-id="2f02e-1109">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1109">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-1110">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-1110">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-1111">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-1111">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="2f02e-1112">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-1112">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="2f02e-1113">nx_secure_tls_session_renegotiation_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1113">nx_secure_tls_session_renegotiation_callback_set</span></span>

## <a name="nx_secure_tls_session_reset"></a><span data-ttu-id="2f02e-1114">nx_secure_tls_session_reset</span><span class="sxs-lookup"><span data-stu-id="2f02e-1114">nx_secure_tls_session_reset</span></span>

<span data-ttu-id="2f02e-1115">Cancellare e reimpostare una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-1115">Clear out and reset a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1116">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1116">Prototype</span></span>

```C
UINT  nx_secure_tls_session_reset (NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="2f02e-1117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1117">Description</span></span>

<span data-ttu-id="2f02e-1118">Questo servizio Cancella una sessione TLS e Reimposta lo stato come se la sessione fosse stata appena creata in modo che un oggetto sessione TLS esistente possa essere riutilizzato per una nuova sessione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1118">This service clears out a TLS session and resets the state as if the session had just been created so an existing TLS session object can be re-used for a new session.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1119">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1119">Parameters</span></span>

- <span data-ttu-id="2f02e-1120">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1120">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1121">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1121">Return Values</span></span>

- <span data-ttu-id="2f02e-1122">**NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1122">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="2f02e-1123">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1123">**NX_INVALID_PARAMETERS** (0x4D) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="2f02e-1124">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1124">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1125">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1125">Allowed From</span></span>

<span data-ttu-id="2f02e-1126">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1126">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1127">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1127">Example</span></span>

```C
/* Reset a TLS session.  */
status =  nx_secure_tls_session_reset(&tls_session);


/* If status is NX_SUCCESS the session was successfully reset and may be reused.*/
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1128">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1128">See Also</span></span>

- <span data-ttu-id="2f02e-1129">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-1129">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-1130">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1130">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-1131">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-1131">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-1132">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-1132">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="2f02e-1133">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-1133">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="2f02e-1134">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-1134">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="2f02e-1135">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1135">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_send"></a><span data-ttu-id="2f02e-1136">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-1136">nx_secure_tls_session_send</span></span>

<span data-ttu-id="2f02e-1137">Inviare dati tramite una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-1137">Send data through a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1138">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1138">Prototype</span></span>

```C
UINT  nx_secure_tls_session_send(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET *packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="2f02e-1139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1139">Description</span></span>

<span data-ttu-id="2f02e-1140">Questo servizio invia i dati nel NX_PACKET fornito, usando la sessione TLS attiva specificata e gestendo la crittografia dei dati prima di inviarli all'host remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1140">This service sends data in the supplied NX_PACKET, using the specified active TLS session, and handling the encryption of that data before sending it to the remote host.</span></span> <span data-ttu-id="2f02e-1141">Se le ultime dimensioni della finestra annunciata del ricevitore sono inferiori a questa richiesta, il servizio sospende facoltativamente in base alle opzioni di attesa specificate.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1141">If the receiver's last advertised window size is less than this request, the service optionally suspends based on the wait options specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f02e-1142">*A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché il driver di rete rilascerà il pacchetto dopo la trasmissione.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-1142">*Unless an error is returned, the application should not release the packet after this call. Doing so will cause unpredictable results because the network driver will release the packet after transmission.*</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1143">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1143">Parameters</span></span>

- <span data-ttu-id="2f02e-1144">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1144">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1145">**packet_ptr** Puntatore a un pacchetto TLS contenente i dati da inviare.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1145">**packet_ptr** Pointer to a TLS packet containing data to be sent.</span></span>
- <span data-ttu-id="2f02e-1146">**WAIT_OPTION** Definisce il comportamento del servizio se la richiesta è maggiore delle dimensioni della finestra del destinatario.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1146">**wait_option** Defines how the service behaves if the request is greater than the window size of the receiver.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1147">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1147">Return Values</span></span>

- <span data-ttu-id="2f02e-1148">**NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1148">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="2f02e-1149">**NX_NO_PACKET** (0x01) non sono stati ricevuti dati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1149">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="2f02e-1150">**NX_NOT_CONNECTED** (0X38) il socket TCP sottostante non è più connesso.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1150">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="2f02e-1151">**NX_SECURE_TLS_TCP_SEND_FAILED** (0X109) l'invio del socket TCP sottostante non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1151">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) The underlying TCP socket send failed.</span></span>
- <span data-ttu-id="2f02e-1152">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1152">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="2f02e-1153">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0X101) la sessione TLS specificata non è stata inizializzata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1153">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1154">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1154">Allowed From</span></span>

<span data-ttu-id="2f02e-1155">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1155">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1156">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1156">Example</span></span>

```C
/* Send a packet using an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is sent, blocking otherwise.   */
status =  nx_secure_tls_session_send(&tls_session, &packet_ptr, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the packet has been sent. */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1157">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1157">See Also</span></span>

- <span data-ttu-id="2f02e-1158">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-1158">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="2f02e-1159">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-1159">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-1160">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1160">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-1161">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1161">nx_secure_tls_packet_allocate</span></span>
- <span data-ttu-id="2f02e-1162">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-1162">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-1163">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-1163">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="2f02e-1164">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-1164">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="2f02e-1165">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="2f02e-1165">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="2f02e-1166">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1166">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_server_callback_set"></a><span data-ttu-id="2f02e-1167">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1167">nx_secure_tls_session_server_callback_set</span></span>

<span data-ttu-id="2f02e-1168">Configurare un callback per TLS da richiamare all'inizio di un handshake del server TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-1168">Set up a callback for TLS to invoke at the beginning of a TLS Server handshake</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1169">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1169">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_server_callback_set (
                 NX_SECURE_TLS_SESSION *tls_session,
                 ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                   NX_SECURE_TLS_HELLO_EXTENSION
                                   *extensions, UINT num_extensions));
```

### <a name="description"></a><span data-ttu-id="2f02e-1170">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1170">Description</span></span>

<span data-ttu-id="2f02e-1171">Questo servizio assegna un puntatore a funzione a una sessione TLS che verrà richiamata da TLS quando un handshake del server TLS riceve un messaggio ClientHello.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1171">This service assigns a function pointer to a TLS session that TLS will invoke when a TLS Server handshake has received a ClientHello message.</span></span> <span data-ttu-id="2f02e-1172">La funzione di callback consente a un'applicazione di elaborare tutte le estensioni TLS dal messaggio ClientHello ricevuto che richiede l'input o il processo decisionale.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1172">The callback function allows an application to process any TLS extensions from the received ClientHello message that require input or decision making.</span></span>

<span data-ttu-id="2f02e-1173">Il callback viene eseguito con il blocco di controllo della sessione TLS chiamante e una matrice di oggetti NX_SECURE_TLS_HELLO_EXTENSION.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1173">The callback is executed with the invoking TLS session control block and an array of NX_SECURE_TLS_HELLO_EXTENSION objects.</span></span> <span data-ttu-id="2f02e-1174">La matrice di oggetti estensione deve essere passata in una funzione helper che troverà e analizzerà un'estensione specifica.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1174">The array of extension objects is intended to be passed into a helper function that will find and parse a specific extension.</span></span> <span data-ttu-id="2f02e-1175">Per una funzione helper di esempio che analizza le estensioni TLS fornite nei messaggi Hello, vedere *nx_secure_tls_session_sni_extension_parse*.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1175">For an example helper function that parses TLS extensions provided in hello messages, see *nx_secure_tls_session_sni_extension_parse*.</span></span>

<span data-ttu-id="2f02e-1176">Il callback del server può essere usato anche per selezionare il certificato di identità attivo usando *nx_secure_tls_active_certificate_set* per il server TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1176">The server callback may also be used to select the active identity certificate using *nx_secure_tls_active_certificate_set* for the TLS Server.</span></span> <span data-ttu-id="2f02e-1177">Questo problema si verifica più spesso in risposta a un'estensione Indicazione nome server (SNI) che consente a un client TLS di indicare quale server si sta tentando di contattare.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1177">This will most often occur in response to a Server Name Indication (SNI) extension which allows a TLS Client to indicate which server it is attempting to contact.</span></span> <span data-ttu-id="2f02e-1178">Per ulteriori informazioni, vedere i riferimenti per *nx_secure_tls_session_sni_extension_parse* e *nx_secure_tls_active_certificate_set* .</span><span class="sxs-lookup"><span data-stu-id="2f02e-1178">See the references for *nx_secure_tls_session_sni_extension_parse* and *nx_secure_tls_active_certificate_set* for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1179">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1179">Parameters</span></span>

- <span data-ttu-id="2f02e-1180">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1180">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1181">**func_ptr** Puntatore alla funzione di callback del server TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1181">**func_ptr** Pointer to the TLS Server callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1182">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1182">Return Values</span></span>

- <span data-ttu-id="2f02e-1183">**NX_SUCCESS** (0x00) allocazione riuscita del puntatore a funzione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1183">**NX_SUCCESS** (0x00) Successful allocation of Function pointer.</span></span>
- <span data-ttu-id="2f02e-1184">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1184">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1185">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1185">Allowed From</span></span>

<span data-ttu-id="2f02e-1186">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1186">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1187">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1187">Example</span></span>

```C
/* Application-supplied function to map server DNS name to a specific certificate
   ID. The certificate ID is supplied by the application when the certificate is
   added with nx_secure_tls_server_certificate_add. */
UINT application_find_id_by_dns_name(NX_SECURE_X509_DNS_NAME *dns_name)
{
    if(strncmp(dns_name->nx_secure_x509_dns_name, “server_name”,
               dns_name->nx_secure_x509_dns_name_length) == 0)
    {
        /* DNS name matches one we know, return it’s ID. */
        return(0x12);
    }

    /* Unknown DNS name, return 0 to indicate no matching ID found. */
    return(0);
}

/* Callback routine used to process ClientHello extensions and perform other
   runtime actions at the beginning of a TLS handshake (such as selecting an
   identify certificate to provide to the client). */
ULONG tls_server_callback(NX_SECURE_TLS_SESSION *session,
                          NX_SECURE_TLS_HELLO_EXTENSION *extensions, UINT
                          num_extensions)
{
UINT status;
NX_SECURE_X509_DNS_NAME dns_name;
UINT cert_id;
NX_SECURE_X509_CERT *certificate;


    /* Find and parse a Server Name Indication (SNI) extension. */
    status = nx_secure_tls_session_sni_extension_parse(session, extensions,
                                                       num_extensions, &dns_name);

    if(status != NX_SUCCESS && status != NX_SECURE_TLS_EXTENSION_NOT_FOUND)
    {
        /* Parsed an invalid extension, return the error. */
        return(status);
    }

    if(status == NX_SECURE_TLS_EXTENSION_NOT_FOUND)
    {
            /* SNI extension not found, just return success to use the default
               certificate. */
            return(NX_SUCCESS);
    }

    /* Find the application-supplied numeric identifier for the specified DNS
       name provided by the remote client. */
    cert_id = application_find_id_by_dns_name(&dns_name);

    /* If cert_id is 0, just use the default identity certificate added with
       nx_secure_tls_local_certificate_add. */
    if(cert_id != 0)
    {
        /* Application found a matching name, find the certificate in our
           store. */
        status = nx_secure_tls_server_certificate_find(tls_session, &certificate,
                                                       cert_id);

        if(status != NX_SUCCESS)
        {
            /* Didn’t find a valid certificate with the supplied ID. Return an
               error so TLS can shut down the handshake. */
            return(NX_SECURE_TLS_CERTIFICATE_NOT_FOUND);
        }

        /* Set the active identity certificate – the certificate should have been
           added to the local store at application start with
           nx_secure_tls_local_certificate_add. */
        nx_secure_tls_active_certificate_set(session, certificate);
    }

    return(NX_SUCCESS);
}

/* TLS setup routine. */
UINT tls_setup(NX_SECURE_TLS_SESSION *tls_session)
{
        /* Add callback to TLS session.  */
        status =  nx_secure_tls_session_server_callback_set(tls_session,
                                                            server_callback);

        /* If status is NX_SUCCESS the callback was added and will be invoked
           immediately after a ClientHello message is received. */

        return(status);
}
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1188">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1188">See Also</span></span>

- <span data-ttu-id="2f02e-1189">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1189">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-1190">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1190">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="2f02e-1191">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1191">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="2f02e-1192">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-1192">nx_secure_tls_session_sni_extension_parse</span></span>
- <span data-ttu-id="2f02e-1193">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-1193">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="2f02e-1194">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-1194">nx_secure_tls_server_certificate_find</span></span>

## <a name="nx_secure_tls_session_sni_extension_parse"></a><span data-ttu-id="2f02e-1195">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-1195">nx_secure_tls_session_sni_extension_parse</span></span>

<span data-ttu-id="2f02e-1196">Analizzare un'estensione di Indicazione nome server (SNI) ricevuta da un client TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-1196">Parse a Server Name Indication (SNI) extension received from a TLS Client</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1197">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1197">Prototype</span></span>

```C
UINT  nx_secure_tls_session_sni_extension_parse(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions,
                                    UINT num_extensions,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a><span data-ttu-id="2f02e-1198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1198">Description</span></span>

<span data-ttu-id="2f02e-1199">Questo servizio è destinato a essere chiamato dall'interno di un callback di sessione del server TLS, aggiunto a una sessione TLS utilizzando nx_secure_tls_session_server_callback_set.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1199">This service is intended to be called from within a TLS Server session callback, added to a TLS session using nx_secure_tls_session_server_callback_set.</span></span> <span data-ttu-id="2f02e-1200">Il callback viene richiamato dopo la ricezione di un messaggio ClientHello da un client TLS remoto e viene fornita una matrice di estensioni disponibili (e il numero di estensioni nella matrice).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1200">The callback is invoked following the reception of a ClientHello message from a remote TLS client and is supplied an array of available extensions (and the number of extensions in the array).</span></span> <span data-ttu-id="2f02e-1201">Tale matrice e la relativa lunghezza possono essere passate direttamente a questa routine per determinare se è presente un'estensione SNI. in caso contrario, viene restituito NX_SECURE_TLS_EXTENSION_NOT_FOUND che indica semplicemente che il client ha scelto di non proviceare l'estensione SNI (questo non è un errore).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1201">That array and its length can be passed directly to this routine to determine if there is an SNI extension present – if not, NX_SECURE_TLS_EXTENSION_NOT_FOUND is returned indicating simply that the client opted not to provice the SNI extension (this is not an error).</span></span>

<span data-ttu-id="2f02e-1202">Se viene rilevata l'estensione SNI, il nome DNS X. 509 fornito dal client TLS viene restituito nella struttura dns_name.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1202">If the SNI extension is found, the X.509 DNS name supplied by the TLS client is returned in the dns_name structure.</span></span> <span data-ttu-id="2f02e-1203">Attualmente, l'estensione SNI fornisce solo una voce di nome DNS singola, che può essere usata dal server TLS per determinare quale certificato di identità inviare al client remoto. \* \*</span><span class="sxs-lookup"><span data-stu-id="2f02e-1203">Currently, the SNI extension only supplies a single DNS name entry, which may be used by the TLS server to determine which identity certificate to send to the remote client.\*\*</span></span>

<span data-ttu-id="2f02e-1204">La struttura NX_SECURE_X509_DNS_NAME contiene semplicemente il nome DNS come stringa UCHAR nel campo *nx_secure_x509_dns_name* e la lunghezza della stringa del nome in *nx_secure_x509_dns_name_length*.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1204">The NX_SECURE_X509_DNS_NAME structure simply contains the DNS name as a UCHAR string in the field *nx_secure_x509_dns_name* and the length of the name string in *nx_secure_x509_dns_name_length*.</span></span> <span data-ttu-id="2f02e-1205">La macro NX_SECURE_X509_DNS_NAME_MAX controlla la dimensione del buffer di nx_secure_x509_dns_name.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1205">The macro NX_SECURE_X509_DNS_NAME_MAX controls the size of the nx_secure_x509_dns_name buffer.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1206">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1206">Parameters</span></span>

- <span data-ttu-id="2f02e-1207">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1207">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1208">**estensioni** di Puntatore a una matrice di estensioni di TLS Hello (dal callback della sessione).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1208">**extensions** Pointer to an array of TLS Hello extensions (from session callback).</span></span>
- <span data-ttu-id="2f02e-1209">**num_extensions** Numero di estensioni nella matrice (dal callback della sessione).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1209">**num_extensions** Number of extensions in array (from session callback).</span></span>
- <span data-ttu-id="2f02e-1210">**dns_name** Restituisce il nome DNS specificato nell'estensione SNI.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1210">**dns_name** Return DNS name supplied in the SNI extension.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1211">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1211">Return Values</span></span>

- <span data-ttu-id="2f02e-1212">**NX_SUCCESS** (0x00) l'analisi dell'estensione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1212">**NX_SUCCESS** (0x00) Successful parsing of the extension.</span></span>
- <span data-ttu-id="2f02e-1213">**NX_PTR_ERROR** (0x07) estensioni non valide per array o puntatore di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1213">**NX_PTR_ERROR** (0x07) Invalid extensions array or TLS session pointer.</span></span>
- <span data-ttu-id="2f02e-1214">Impossibile trovare l'estensione SNI **NX_SECURE_TLS_EXTENSION_NOT_FOUND** (0x136).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1214">**NX_SECURE_TLS_EXTENSION_NOT_FOUND** (0x136) SNI extension not found.</span></span>
- <span data-ttu-id="2f02e-1215">Il formato dell'estensione SNI **NX_SECURE_TLS_SNI_EXTENSION_INVALID** (0x137) non è valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1215">**NX_SECURE_TLS_SNI_EXTENSION_INVALID** (0x137) SNI extension format was invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1216">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1216">Allowed From</span></span>

<span data-ttu-id="2f02e-1217">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1217">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1218">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1218">Example</span></span>

### <a name="see-also"></a><span data-ttu-id="2f02e-1219">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1219">See Also</span></span>

- <span data-ttu-id="2f02e-1220">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1220">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="2f02e-1221">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1221">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="2f02e-1222">nx_secure_tls_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1222">nx_secure_tls_server_callback_set</span></span>
- <span data-ttu-id="2f02e-1223">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1223">nx_secure_tls_active_certificate_set</span></span>

## <a name="nx_secure_tls_session_sni_extension_set"></a><span data-ttu-id="2f02e-1224">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1224">nx_secure_tls_session_sni_extension_set</span></span>

<span data-ttu-id="2f02e-1225">Impostare un nome DNS dell'estensione Indicazione nome server (SNI) da inviare a un server remoto</span><span class="sxs-lookup"><span data-stu-id="2f02e-1225">Set a Server Name Indication (SNI) extension DNS name to send to a remote Server</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1226">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1226">Prototype</span></span>

```C
UINT  nx_secure_tls_session_sni_extension_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a><span data-ttu-id="2f02e-1227">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1227">Description</span></span>

<span data-ttu-id="2f02e-1228">Questo servizio consente a un'applicazione client TLS di fornire un nome DNS del server preferito a un server TLS remoto usando l'estensione TLS Indicazione nome server (SNI).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1228">This service allows a TLS Client application to provide a preferred server DNS name to a remote TLS server using the Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="2f02e-1229">L'estensione SNI consente al server di selezionare il certificato di identità e i parametri appropriati in base alle preferenze del server indicate dal client.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1229">The SNI extension allows the server to select the proper identity certificate and parameters based on the client's indicated server preference.</span></span> <span data-ttu-id="2f02e-1230">L'estensione SNI supporta attualmente solo un singolo nome DNS da inviare, quindi il parametro del nome singolare.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1230">The SNI extension currently only supports a single DNS name to be sent, hence the singular name parameter.</span></span> <span data-ttu-id="2f02e-1231">Il parametro dns_name deve essere inizializzato con *nx_secure_x509_dns_name_initialize* e conterrà il server preferito del client.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1231">The dns_name parameter must be initialized with *nx_secure_x509_dns_name_initialize* and will contain the client's preferred server.</span></span> <span data-ttu-id="2f02e-1232">Per annullare il nome dell'estensione, è sufficiente chiamare questo servizio con un valore di parametro "dns_name" di NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1232">To unset the extension name, simply call this service with a "dns_name" parameter value of NX_NULL.</span></span>

<span data-ttu-id="2f02e-1233">La struttura NX_SECURE_X509_DNS_NAME contiene semplicemente il nome DNS come stringa UCHAR nel campo  *nx_secure_x509_dns_name* e la lunghezza della stringa del nome in *nx_secure_x509_dns_name_length*.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1233">The NX_SECURE_X509_DNS_NAME structure simply contains the DNS name as a UCHAR string in the field  *nx_secure_x509_dns_name* and the length of the name string in *nx_secure_x509_dns_name_length*.</span></span> <span data-ttu-id="2f02e-1234">La macro NX_SECURE_X509_DNS_NAME_MAX controlla la dimensione del buffer di nx_secure_x509_dns_name.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1234">The macro  NX_SECURE_X509_DNS_NAME_MAX controls the size of the nx_secure_x509_dns_name buffer.</span></span>

> [!NOTE]
> <span data-ttu-id="2f02e-1235">*Questa routine deve essere chiamata prima che venga richiamato nx_secure_tls_session_start o ClientHello non conterrà l'estensione SNI.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-1235">*This routine must be called before nx_secure_tls_session_start is invoked or the ClientHello will not contain the SNI extension.*</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1236">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1236">Parameters</span></span>

- <span data-ttu-id="2f02e-1237">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1237">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1238">**dns_name** Nome DNS fornito dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1238">**dns_name** DNS name supplied by the application.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1239">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1239">Return Values</span></span>

- <span data-ttu-id="2f02e-1240">**NX_SUCCESS** (0x00) aggiunta del nome del server DNS completata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1240">**NX_SUCCESS** (0x00) Successful addition of DNS server name.</span></span>
- <span data-ttu-id="2f02e-1241">**NX_PTR_ERROR** (0x07) nome DNS o puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1241">**NX_PTR_ERROR** (0x07) Invalid DNS name or TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1242">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1242">Allowed From</span></span>

<span data-ttu-id="2f02e-1243">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1243">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1244">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1244">Example</span></span>

```C
#define TLS_SNI_SERVER_NAME “www.example.com”

NX_SECURE_X509_DNS_NAME dns_name;
NX_SECURE_TLS_SESSION client_tls_session;

/* Application where TLS session is started. */
void main()
{
    /* Create a TLS session for our socket. Ciphers and metadata defined
       elsewhere. See nx_secure_tls_session_create reference for more
       information. */
    status =  nx_secure_tls_session_create(&client_tls_session,
                                           &nx_crypto_tls_ciphers,
                                           server_crypto_metadata,
                                           sizeof(server_crypto_metadata));


    /* Initialize the DNS server name we want to send in the SNI extension. */
    nx_secure_x509_dns_name_initialize(&dns_name, TLS_SNI_SERVER_NAME,
                                    strlen(TLS_SNI_SERVER_NAME));

    /* The SNI server name needs to be set prior to starting the TLS session. */
    nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);

   /* Start TLS session as normal. */
}
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1245">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1245">See Also</span></span>

- <span data-ttu-id="2f02e-1246">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-1246">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-1247">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-1247">nx_secure_x509_dns_name_initialize</span></span>

## <a name="nx_secure_tls_session_start"></a><span data-ttu-id="2f02e-1248">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-1248">nx_secure_tls_session_start</span></span>

<span data-ttu-id="2f02e-1249">Avviare una sessione TLS sicura NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-1249">Start a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1250">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1250">Prototype</span></span>

```C
UINT  nx_secure_tls_session_start(NX_SECURE_TLS_SESSION *session_ptr,
                                  NX_TCP_SOCKET *tcp_socket_ptr,
                                  ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="2f02e-1251">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1251">Description</span></span>

<span data-ttu-id="2f02e-1252">Questo servizio avvia una sessione TLS utilizzando il blocco di controllo della sessione TLS fornito e un socket TCP connesso.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1252">This service starts a TLS session using the supplied TLS session control block and a connected TCP socket.</span></span> <span data-ttu-id="2f02e-1253">È necessario che la connessione TCP sia già stata completata in seguito a una chiamata riuscita a nx_tcp_client_socket_connect o nx_tcp_server_socket_accept.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1253">The TCP connection must already be complete following a successful call to either nx_tcp_client_socket_connect or nx_tcp_server_socket_accept.</span></span>

<span data-ttu-id="2f02e-1254">Questo servizio determinerà il tipo di sessione TLS (client o server) dal socket TCP.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1254">This service will determine the type of TLS session (Client or Server) from the TCP socket.</span></span>

<span data-ttu-id="2f02e-1255">L'opzione wait definisce il comportamento del servizio mentre l'handshake TLS è in corso.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1255">The wait option defines how the service behaves while the TLS handshake is in progress.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1256">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1256">Parameters</span></span>

- <span data-ttu-id="2f02e-1257">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1257">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1258">**tcp_socket_ptr** Puntatore a un socket TCP connesso.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1258">**tcp_socket_ptr** Pointer to a connected TCP socket.</span></span>
- <span data-ttu-id="2f02e-1259">**WAIT_OPTION** Definisce il comportamento del servizio mentre è in corso l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1259">**wait_option** Defines how the service behaves while the TLS handshake is in progress.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1260">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1260">Return Values</span></span>

- <span data-ttu-id="2f02e-1261">**NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1261">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="2f02e-1262">**NX_NOT_CONNECTED** (0X38) il socket TCP sottostante non è più connesso.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1262">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="2f02e-1263">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0X102) un tipo di messaggio TLS ricevuto non è corretto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1263">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) A received TLS message type is incorrect.</span></span>
- <span data-ttu-id="2f02e-1264">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0X106) una crittografia fornita dall'host remoto non è supportata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1264">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A cipher provided by the remote host is not supported.</span></span>
- <span data-ttu-id="2f02e-1265">L'elaborazione del messaggio **NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) durante l'handshake TLS non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1265">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) Message processing during the TLS handshake has failed.</span></span>
- <span data-ttu-id="2f02e-1266">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0X108) un messaggio in arrivo non ha superato un controllo Mac hash.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1266">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) An incoming message failed a hash MAC check.</span></span>
- <span data-ttu-id="2f02e-1267">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) non è stato possibile inviare un socket TCP sottostante.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1267">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) An underlying TCP socket send failed.</span></span>
- <span data-ttu-id="2f02e-1268">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0X10A) un messaggio in ingresso ha un campo di lunghezza non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1268">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) An incoming message had an invalid length field.</span></span>
- <span data-ttu-id="2f02e-1269">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0X10B) un messaggio ChangeCipherSpec in ingresso non è corretto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1269">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10B) An incoming ChangeCipherSpec message was incorrect.</span></span>
- <span data-ttu-id="2f02e-1270">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0X10C) un certificato TLS in ingresso è inutilizzabile per l'identificazione del server TLS remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1270">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10C) An incoming TLS certificate is unusable for identifying the remote TLS server.</span></span>
- <span data-ttu-id="2f02e-1271">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0X10D) la crittografia a chiave pubblica fornita dall'host remoto non è supportata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1271">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) The public-key cipher provided by the remote host is unsupported.</span></span>
- <span data-ttu-id="2f02e-1272">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0X10E) l'host remoto non ha indicato ciphersuites supportati dallo stack TLS sicuro NETX.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1272">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) The remote host has indicated no ciphersuites that are supported by the NetX Secure TLS stack.</span></span>
- <span data-ttu-id="2f02e-1273">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0X10F) un messaggio TLS ricevuto ha una versione di TLS sconosciuta nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1273">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received TLS message had an unknown TLS version in its header.</span></span>
- <span data-ttu-id="2f02e-1274">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) un messaggio TLS ricevuto ha una versione di TLS nota ma non supportata nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1274">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) A received TLS message had a known but unsupported TLS version in its header.</span></span>
- <span data-ttu-id="2f02e-1275">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0X111) l'allocazione di pacchetti TLS interna non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1275">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) An internal TLS packet allocation failed.</span></span>
- <span data-ttu-id="2f02e-1276">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0X112) l'host remoto ha fornito un certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1276">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) The remote host provided an invalid certificate.</span></span>
- <span data-ttu-id="2f02e-1277">**NX_SECURE_TLS_ALERT_RECEIVED** (0X114) l'host remoto ha inviato un avviso che indica un errore e termina la sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1277">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) The remote host sent an alert indicating an error and ending the TLS session.</span></span>
- <span data-ttu-id="2f02e-1278">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0X13B) una voce nella tabella ciphersuite include un puntatore a funzione null.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1278">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13B) An entry in the ciphersuite table had a NULL function pointer.</span></span>
- <span data-ttu-id="2f02e-1279">**NX_SECURE_TLS_INAPPROPRIATE_FALLBACK** (0X146) un ClientHello TLS remoto includeva il fallback SCSV andattempted un fallback della versione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1279">**NX_SECURE_TLS_INAPPROPRIATE_FALLBACK** (0x146) A remote TLS ClientHello included the fallback SCSV andattempted a version fallback.</span></span>
- <span data-ttu-id="2f02e-1280">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1280">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1281">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1281">Allowed From</span></span>

<span data-ttu-id="2f02e-1282">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1282">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1283">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1283">Example</span></span>

```C
NX_TCP_SOCKET tcp_socket;
NX_SECURE_TLS_SESSION tls_session;
NX_SECURE_X509_CERT certificate;

/* Initialize the TLS session structure. */
nx_secure_tls_session_create(&tls_session,
                              &nx_crypto_tls_ciphers,
                              crypto_metadata,
                              sizeof(crypto_metadata));

/* Setup the TLS packet reassembly buffer. */
status = nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                 sizeof(tls_packet_buffer));

/* Initialize a certificate for the TLS server. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data, 500,
NX_NULL, 0, private_key, 64);

/* If status is NX_SUCCESS, certificate is initialized. */

/* Add the certificate a local certificate to identify this TLS server. */
status = nx_secure_tls_add_local_certificate(&tls_session, &certificate);

/* If status is NX_SUCCESS, certificate was added successfully. */

/* Create and start a TCP socket as a server. */
/* NOTE: This assumes an IP instance called “ip_0” has already been created. */

/* Create a TCP server socket on the previously created IP instance, with normal
   delivery, IP fragmentation enabled, default time to live, a 8192-byte receive
   window, no urgent callback routine, and the "client_disconnect" routine to
   handle disconnection initiated from the other end of the connection.  */
status =  nx_tcp_socket_create(&ip_0, &tcp_socket, "TLS Server Socket", NX_IP_NORMAL,
                               NX_FRAGMENT_OKAY, NX_IP_TIME_TO_LIVE, 8192, NX_NULL,
                               NX_NULL);

/* If status is NX_SUCCESS, the TCP socket was created successfully. */

/* Start up a TCP server socket by listening on port 443 with a listen queue of
   size 5. */
status =  nx_tcp_server_socket_listen(&ip_0, 443, &tcp_socket, 5, NX_NULL);

/* Application main loop. */
while(1)
{
        /* Accept incoming requests on the TCP socket. */
        status =  nx_tcp_server_socket_accept(&tcp_socket, NX_WAIT_FOREVER);

        /* At this point, the TCP socket should be established (but not the TLS
        session yet). */

        /* Start the TLS session on our active TCP socket. */
        status = nx_secure_tls_session_start(&tls_session, &tcp_socket,
                                             NX_WAIT_FOREVER);

        /* At this point, if status is NX_SUCCESS, the TLS session has been
           established.  Application may now send/receive data through this
           channel. */

        /* Send and receive data using the TLS session. */
        /* Allocate TLS packets using nx_secure_tls_packet_allocate, write data with
           nx_packet_data_append, read data with nx_packet_data_extract_offset. */

        /* Send TLS data. */
        nx_secure_tls_session_send(&tls_session, &send_packet, NX_WAIT_FOREVER);

        nx_secure_tls_session_receive(&tls_session, &receive_packet_ptr,
        NX_WAIT_FOREVER);


        /* Once all application data is sent/received, end the TLS session. */
        status = nx_secure_tls_session_end(&tls_session);

        /* If status is NX_SUCCESS, the TLS session has been closed properly. */

        /* Now disconnect the TCP server socket from the client.  */
        nx_tcp_socket_disconnect(&tcp_socket, 200);

        /* Unaccept the TCP server socket.  Note that unaccept is called even if
           disconnect or accept fails.  */
        nx_tcp_server_socket_unaccept(&tcp_socket);

        /* Setup server socket for listening with this socket again.  */
        nx_tcp_server_socket_relisten(&ip_0, 443, &tcp_socket);
}

/* When the server application is shut down, clean up the TLS session. */
nx_secure_tls_session_delete(&tls_session);

/* Finally, clean up the TCP socket as well. */
nx_tcp_socket_delete(&tcp_socket);
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1284">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1284">See Also</span></span>

- <span data-ttu-id="2f02e-1285">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-1285">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="2f02e-1286">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-1286">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-1287">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1287">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-1288">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="2f02e-1288">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="2f02e-1289">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-1289">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="2f02e-1290">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-1290">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="2f02e-1291">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1291">nx_secure_tls_packet_allocate</span></span>
- <span data-ttu-id="2f02e-1292">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="2f02e-1292">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="2f02e-1293">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1293">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-1294">nx_tcp_socket_accept</span><span class="sxs-lookup"><span data-stu-id="2f02e-1294">nx_tcp_socket_accept</span></span>
- <span data-ttu-id="2f02e-1295">nx_tcp_socket_listen</span><span class="sxs-lookup"><span data-stu-id="2f02e-1295">nx_tcp_socket_listen</span></span>
- <span data-ttu-id="2f02e-1296">nx_tcp_socket_disconnect</span><span class="sxs-lookup"><span data-stu-id="2f02e-1296">nx_tcp_socket_disconnect</span></span>
- <span data-ttu-id="2f02e-1297">nx_tcp_socket_unaccept</span><span class="sxs-lookup"><span data-stu-id="2f02e-1297">nx_tcp_socket_unaccept</span></span>
- <span data-ttu-id="2f02e-1298">nx_tcp_socket_relisten</span><span class="sxs-lookup"><span data-stu-id="2f02e-1298">nx_tcp_socket_relisten</span></span>
- <span data-ttu-id="2f02e-1299">nx_tcp_socket_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-1299">nx_tcp_socket_delete</span></span>
- <span data-ttu-id="2f02e-1300">nx_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1300">nx_packet_allocate</span></span>
- <span data-ttu-id="2f02e-1301">nx_packet_data_append</span><span class="sxs-lookup"><span data-stu-id="2f02e-1301">nx_packet_data_append</span></span>
- <span data-ttu-id="2f02e-1302">nx_packet_data_extract_offset</span><span class="sxs-lookup"><span data-stu-id="2f02e-1302">nx_packet_data_extract_offset</span></span>

## <a name="nx_secure_tls_session_time_function_set"></a><span data-ttu-id="2f02e-1303">nx_secure_tls_session_time_function_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1303">nx_secure_tls_session_time_function_set</span></span>

<span data-ttu-id="2f02e-1304">Assegnare una funzione timestamp a una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-1304">Assign a timestamp function to a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1305">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1305">Prototype</span></span>

```C
UINT  nx_secure_tls_time_function_set(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              ULONG (*time_func_ptr)(void));
```

### <a name="description"></a><span data-ttu-id="2f02e-1306">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1306">Description</span></span>

<span data-ttu-id="2f02e-1307">Questa funzione configura un puntatore a funzione che TLS richiamerà quando deve ottenere l'ora corrente, che viene utilizzata in vari messaggi di handshake TLS e per la verifica dei certificati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1307">This function sets up a function pointer that TLS will invoke when it needs to get the current time, which is used in various TLS handshake messages and for verification of certificates.</span></span>

<span data-ttu-id="2f02e-1308">Si prevede che la funzione restituisca il GMT corrente nel formato UNIX a 32 bit (secondi dalla mezzanotte del 1 ° gennaio 1970, UTC, ignorando i secondi intercalari), in base ai requisiti di ClientHello in TLS RFC 5246.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1308">The function is expected to return the current GMT in UNIX 32-bit format (seconds since the midnight starting Jan 1, 1970, UTC, ignoring leap seconds), as per the ClientHello requirements in the TLS RFC 5246.</span></span>

<span data-ttu-id="2f02e-1309">Se non viene assegnata alcuna funzione timestamp, verrà usato il valore 0 per il timestamp nell'handshake TLS e il controllo della scadenza del certificato non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1309">If no timestamp function is assigned, a value of 0 for the timestamp in the TLS handshake will be used and certificate expiration checking will not work.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1310">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1310">Parameters</span></span>

- <span data-ttu-id="2f02e-1311">**session_ptr** Puntatore a un'istanza della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1311">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1312">**time_func_ptr** Puntatore a una funzione che restituisce l'ora corrente (GMT) nel formato UNIX 32 bit.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1312">**time_func_ptr** Pointer to a function that returns the current time (GMT) in UNIX 32-bit format.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1313">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1313">Return Values</span></span>

- <span data-ttu-id="2f02e-1314">**NX_SUCCESS** (0x00) inizializzazione corretta della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1314">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="2f02e-1315">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1315">**NX_INVALID_PARAMETERS** (0x4D) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="2f02e-1316">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1316">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1317">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1317">Allowed From</span></span>

<span data-ttu-id="2f02e-1318">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1318">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1319">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1319">Example</span></span>

```C
/* This function returns a 32-bit UNIX-style representation of the current GMT
   time. */
ULONG get_gmt_time(void)
{
ULONG time_value;

   /* Platform-specific time calculation goes here… */

   return(time_value);
}

/* Reset a TLS session.  */
status =  nx_secure_tls_timestamp_function_set(&tls_session, get_gmt_time);


/* If status is NX_SUCCESS the function was successfully added.*/
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1320">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1320">See Also</span></span>

- <span data-ttu-id="2f02e-1321">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-1321">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-1322">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1322">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-1323">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="2f02e-1323">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="2f02e-1324">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="2f02e-1324">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="2f02e-1325">nx_secure_tls_session_sendnx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="2f02e-1325">nx_secure_tls_session_sendnx_secure_tls_session_receive</span></span>
- <span data-ttu-id="2f02e-1326">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1326">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_trusted_certificate_add"></a><span data-ttu-id="2f02e-1327">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-1327">nx_secure_tls_trusted_certificate_add</span></span>

<span data-ttu-id="2f02e-1328">Aggiungere un certificato attendibile alla sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-1328">Add trusted certificate to NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1329">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1329">Prototype</span></span>

```C
UINT  nx_secure_tls_trusted_certificate_add(NX_SECURE_TLS_SESSION
                            *session_ptr, NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a><span data-ttu-id="2f02e-1330">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1330">Description</span></span>

<span data-ttu-id="2f02e-1331">Questo servizio aggiunge un'istanza di struttura NX_SECURE_X509_CERT inizializzata a una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1331">This service adds an initialized NX_SECURE_X509_CERT structure instance to a TLS session.</span></span> <span data-ttu-id="2f02e-1332">Questo certificato viene usato dallo stack TLS per verificare i certificati forniti dall'host remoto durante l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1332">This certificate is used by the TLS stack to verify certificates supplied by the remote host during the TLS handshake.</span></span>

<span data-ttu-id="2f02e-1333">Per la modalità client TLS sono necessari certificati attendibili.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1333">Trusted certificates are required for TLS Client mode.</span></span>

<span data-ttu-id="2f02e-1334">I certificati attendibili sono necessari solo per la modalità server TLS se è abilitata l'autenticazione del certificato client.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1334">Trusted certificates are only required for TLS Server mode if client certificate authentication is enabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1335">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1335">Parameters</span></span>

- <span data-ttu-id="2f02e-1336">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1336">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1337">**certificate_ptr** Puntatore a un'istanza di certificato TLS inizializzata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1337">**certificate_ptr** Pointer to an initialized TLS Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1338">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1338">Return Values</span></span>

- <span data-ttu-id="2f02e-1339">Aggiunta del certificato **NX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1339">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="2f02e-1340">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) ha tentato di aggiungere un certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1340">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid certificate.</span></span>
- <span data-ttu-id="2f02e-1341">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1341">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1342">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1342">Allowed From</span></span>

<span data-ttu-id="2f02e-1343">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1343">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1344">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1344">Example</span></span>

```C
/* Initialize certificate structure. */
status = nx_secure_x509_certificate_initialize(&certificate, certificate_data,
                                               certificate_buffer,
                                               sizeof(certificate_buffer), 500,
                                               private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_trusted_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1345">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1345">See Also</span></span>

- <span data-ttu-id="2f02e-1346">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-1346">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-1347">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1347">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-1348">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1348">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-1349">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-1349">nx_secure_tls_trusted_certificate_remove</span></span>

## <a name="nx_secure_tls_trusted_certificate_remove"></a><span data-ttu-id="2f02e-1350">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="2f02e-1350">nx_secure_tls_trusted_certificate_remove</span></span>

<span data-ttu-id="2f02e-1351">Rimuovere il certificato attendibile dalla sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-1351">Remove trusted certificate from NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1352">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1352">Prototype</span></span>

```C
UINT  nx_secure_tls_trusted_certificate_remove(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *common_name,
                                    UINT common_name_length);
```

### <a name="description"></a><span data-ttu-id="2f02e-1353">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1353">Description</span></span>

<span data-ttu-id="2f02e-1354">Questo servizio rimuove un certificato attendibile da una sessione TLS, con chiave nel campo nome comune nel certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1354">This service removes a trusted certificate from a TLS session, keyed on the Common Name field in the certificate.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1355">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1355">Parameters</span></span>

- <span data-ttu-id="2f02e-1356">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1356">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="2f02e-1357">**common_name** Valore del nome comune del certificato da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1357">**common_name** The Common Name value of the certificate to be removed.</span></span>
- <span data-ttu-id="2f02e-1358">**common_name_length** Lunghezza della stringa del nome comune.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1358">**common_name_length** The length of the Common Name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1359">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1359">Return Values</span></span>

- <span data-ttu-id="2f02e-1360">Aggiunta del certificato **NX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1360">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="2f02e-1361">**NX_PTR_ERROR** (0x07) puntatore a sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1361">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="2f02e-1362">Il certificato **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1362">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Certificate was not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1363">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1363">Allowed From</span></span>

<span data-ttu-id="2f02e-1364">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1364">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1365">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1365">Example</span></span>

```C
/* Remove certificate from TLS session.  */
status =  nx_secure_tls_trusted_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1366">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1366">See Also</span></span>

- <span data-ttu-id="2f02e-1367">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-1367">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="2f02e-1368">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1368">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-1369">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1369">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-1370">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-1370">nx_secure_tls_trusted_certificate_add</span></span>

## <a name="nx_secure_x509_certificate_initialize"></a><span data-ttu-id="2f02e-1371">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-1371">nx_secure_x509_certificate_initialize</span></span>

<span data-ttu-id="2f02e-1372">Inizializzare il certificato X. 509 per NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-1372">Initialize X.509 Certificate for NetX Secure TLS</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1373">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1373">Prototype</span></span>

```C
UINT  nx_secure_x509_certificate_initialize(
                  NX_SECURE_X509_CERT *certificate_ptr,
                  const UCHAR *certificate_data,
                  USHORT certificate_data_length,
                  UCHAR *raw_data_buffer,
                  USHORT buffer_size,
                  const UCHAR *private_key_data,
                  USHORT private_key_data_length,
                  UINT private_key_type);
```

### <a name="description"></a><span data-ttu-id="2f02e-1374">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1374">Description</span></span>

<span data-ttu-id="2f02e-1375">Questo servizio Inizializza una struttura di NX_SECURE_X509_CERT da un certificato digitale X. 509 con codifica binaria da usare in una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1375">This service initializes an NX_SECURE_X509_CERT structure from a binary-encoded X.509 digital certificate for use in a TLS session.</span></span>

<span data-ttu-id="2f02e-1376">I dati del certificato **devono** essere un certificato digitale X. 509 valido nel formato binario con codifica der.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1376">The certificate data **must** be a valid X.509 digital certificate in DER-encoded binary format.</span></span> <span data-ttu-id="2f02e-1377">I dati possono essere determinati da qualsiasi origine (ad esempio file system, buffer costante compilato e così via), purché venga fornito un puntatore UCHAR a tali dati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1377">The data can some from any source (e.g. file system, compiled constant buffer, etc.) as long as a UCHAR pointer to that data is provided.</span></span>

<span data-ttu-id="2f02e-1378">Il parametro *raw_data_buffer* e le relative dimensioni sono parametri facoltativi che specificano un buffer dedicato in cui i dati del certificato vengono copiati prima dell'analisi.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1378">The *raw_data_buffer* parameter and its size are optional parameters that specify a dedicated buffer into which the certificate data is copied before parsing.</span></span> <span data-ttu-id="2f02e-1379">Se raw_data_buffer viene passato come NX_NULL, la struttura NX_SECURE_X509_CERT punterà direttamente nella matrice di certificate_data (in questo caso buffer_size viene ignorato).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1379">If raw_data_buffer is passed as NX_NULL then the NX_SECURE_X509_CERT structure will point directly into the certificate_data array (buffer_size is ignored in this case).</span></span> <span data-ttu-id="2f02e-1380">Se raw_data_buffer viene passato come NX_NULL, ***non*** modificare i dati a cui punta il certificate_data puntatore o l'elaborazione del certificato probabilmente avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1380">If raw_data_buffer is passed as NX_NULL, ***do not*** modify the data pointed to by the certificate_data pointer or certificate processing will likely fail!</span></span>

<span data-ttu-id="2f02e-1381">Il parametro della chiave privata è per i certificati di identità locali: la chiave privata viene usata dai server per decrittografare i dati delle chiavi in ingresso da un client (crittografato con la chiave pubblica del server) e dai client per verificarne l'identità a un server quando il server richiede un certificato client.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1381">The private key parameter is for local identity certificates – the private key is used by servers to decrypt the incoming key data from a client (encrypted using the server's public key) and by clients to verify their identity to a server when the server requests a client certificate.</span></span> <span data-ttu-id="2f02e-1382">Se si aggiunge una chiave privata con questa API, il certificato associato verrà automaticamente contrassegnato come certificato di identità per un'applicazione TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1382">Adding a private key with this API will automatically mark the associated certificate as being an identity certificate for a TLS application.</span></span> <span data-ttu-id="2f02e-1383">Quando si inizializzano i certificati per altri scopi (ad esempio, l'archivio attendibile), il *private_key_data* parametro deve essere passato come null, il *private_key_data_length* come 0 e il *private_key_type* deve essere passato come NX_SECURE_X509_KEY_TYPE_NONE.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1383">When initializing certificates for other purposes (e.g. the trusted store), the *private_key_data* parameter should be passed as NULL, the *private_key_data_length* as 0, and the *private_key_type* should be passed as NX_SECURE_X509_KEY_TYPE_NONE.</span></span>

<span data-ttu-id="2f02e-1384">Il parametro *private_key_type* indica la formattazione della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1384">The *private_key_type* parameter indicates the formatting of the private key.</span></span> <span data-ttu-id="2f02e-1385">Se ad esempio la chiave privata è una chiave privata RSA con codifica DER PKCS # 1, il private_key_type deve essere passato come NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER, un tipo noto a NetX Secure che verrà analizzato immediatamente e salvato per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1385">For example, if the private key is a DER-encoded PKCS#1-format RSA private key, the private_key_type should be passed as NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER, a type known to NetX Secure which will be parsed immediately and saved for later use.</span></span>

<span data-ttu-id="2f02e-1386">Il private_key_type supporta anche i tipi di chiave definiti dall'utente<sup>23</sup> per le piattaforme e le applicazioni con formati chiave specifici o altre esigenze.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1386">The private_key_type also supports user-defined key types<sup>23</sup> for platforms and applications that have specific key formats or other needs.</span></span> <span data-ttu-id="2f02e-1387">Un motore di crittografia basato su hardware, ad esempio, può utilizzare un formato specifico non riconosciuto dal software NetX Secure, oppure una chiave privata può essere crittografata o rappresentata da un token crittografico come se si trattasse di un hardware di crittografia Trusted Platform Module (TPM) o PKCS # 11.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1387">For example, a hardware-based encryption engine may use a specific format not understood by the NetX Secure software, or a private key may be encrypted or represented by a cryptographic token as might be the case with a Trusted Platform Module (TPM) or PKCS#11 cryptographic hardware.</span></span> <span data-ttu-id="2f02e-1388">Quando si usa un tipo di chiave definito dall'utente, i dati della chiave vengono passati Verbatim alla routine di crittografia appropriata. ad esempio, viene passata una chiave privata RSA, senza analisi o elaborazione, direttamente alla routine di crittografia RSA fornita a TLS nella tabella ciphersuite.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1388">When a user-defined key type is used, the key data is passed verbatim to the appropriate cryptographic routine - for example, an RSA private key would be passed, without any parsing or processing, directly to the RSA cryptographic routine provided to TLS in the ciphersuite table.</span></span> <span data-ttu-id="2f02e-1389">Il tipo di chiave definito dall'utente viene inoltre passato alla routine di crittografia (nel caso di RSA, questo è il parametro "op").</span><span class="sxs-lookup"><span data-stu-id="2f02e-1389">The user-defined key type is also passed to the cryptographic routine (in the case of RSA, this is the "op" parameter).</span></span>

<span data-ttu-id="2f02e-1390">L'intervallo di chiavi definite dall'utente copre la metà superiore di un Unsigned Integer a 32 bit, da 0x0001 0000-0xFFFF FFFF.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1390">The range of user-defined keys covers the top half of a 32-bit unsigned integer, from 0x0001 0000-0xFFFF FFFF.</span></span> <span data-ttu-id="2f02e-1391">I valori minori di 0x0001 0000 sono riservati per l'uso sicuro di NetX.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1391">Values less than 0x0001 0000 are reserved for NetX Secure use.</span></span>

<span data-ttu-id="2f02e-1392">I tipi di chiave definiti dall'utente sono una funzionalità avanzata che richiede routine di crittografia personalizzate per gestire i dati della chiave privata non elaborata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1392">User-defined key types are an advanced feature that requires custom cryptographic routines to handle the raw private key data.</span></span> <span data-ttu-id="2f02e-1393">Se questa funzionalità è necessaria, contattare il rappresentante della logica Express.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1393">Please contact your Express Logic representative if you have need of this feature.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1394">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1394">Parameters</span></span>

- <span data-ttu-id="2f02e-1395">**certificate_ptr** Puntatore a un'istanza di un certificato X. 509 non inizializzato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1395">**certificate_ptr** Pointer to an uninitialized X.509 Certificate instance.</span></span>
- <span data-ttu-id="2f02e-1396">**certificate_data** Puntatore ai dati binari X. 509 con codifica DER.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1396">**certificate_data** Pointer to DER-encoded X.509 binary data.</span></span>
- <span data-ttu-id="2f02e-1397">**raw_data_buffer** Puntatore al buffer di dati del certificato dedicato facoltativo.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1397">**raw_data_buffer** Pointer to optional dedicated certificate data buffer.</span></span>
- <span data-ttu-id="2f02e-1398">**BUFFER_SIZE** Dimensioni del buffer di dati del certificato dedicato facoltativo.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1398">**buffer_size** Size of optional dedicated certificate data buffer.</span></span>
- <span data-ttu-id="2f02e-1399">**certificate_data_length** Lunghezza in byte dei dati binari del certificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1399">**certificate_data_length** Length of certificate binary data in bytes.</span></span>
- <span data-ttu-id="2f02e-1400">**private_key_data** Puntatore ai dati facoltativi della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1400">**private_key_data** Pointer to optional private key data.</span></span>
- <span data-ttu-id="2f02e-1401">**private_key_data_length** Lunghezza dei dati della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1401">**private_key_data_length** Length of private key data.</span></span>
- <span data-ttu-id="2f02e-1402">**private_key_type** Identificatore del tipo di chiave.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1402">**private_key_type** Key type identifier.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1403">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1403">Return Values</span></span>

- <span data-ttu-id="2f02e-1404">Aggiunta del certificato **NX_SUCCESS** (0x00) completata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1404">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="2f02e-1405">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1405">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="2f02e-1406">I dati del certificato **NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) non contengono un certificato X. 509 con codifica der.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1406">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) Certificate data did not contain a DER-encoded X.509 certificate.</span></span>
- <span data-ttu-id="2f02e-1407">Il certificato **NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) non dispone di una crittografia a chiave pubblica supportata da NETX Secure.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1407">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) Certificate did not have a public-key cipher that is supported by NetX Secure.</span></span>
- <span data-ttu-id="2f02e-1408">Il certificato o la chiave privata **NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE** (0x186) non contiene una sequenza ASN. 1 valida.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1408">**NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE** (0x186) Private key or certificate did not contain a valid ASN.1 sequence.</span></span>
- <span data-ttu-id="2f02e-1409">**NX_SECURE_PKCS1_INVALID_PRIVATE_KEY** (0X18A) la chiave privata specificata non era una chiave RSA PKCS # 1 valida.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1409">**NX_SECURE_PKCS1_INVALID_PRIVATE_KEY** (0x18A) The provided private key was not a valid PKCS#1 RSA key.</span></span>
- <span data-ttu-id="2f02e-1410">**NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE** (0X19D) il tipo di chiave privata fornito non è stato definito dall'utente e non corrisponde ad alcun tipo noto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1410">**NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE** (0x19D) The private key type provided was not user-defined and did not match any known type.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1411">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1411">Allowed From</span></span>

<span data-ttu-id="2f02e-1412">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1412">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1413">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1413">Example</span></span>

```C
/* Initialize certificate structure. The certificate structure will point directly
   into the certificate_data array since we are passing the raw_data_buffer as
   NX_NULL. This certificate has a private key so it will be used to identify this
   device. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, NX_NULL, 0, private_key, 64, NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);


/* If status is NX_SUCCESS the certificate was successfully initialized.  */
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1414">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1414">See Also</span></span>

- <span data-ttu-id="2f02e-1415">nx_secure_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="2f02e-1415">nx_secure_local_certificate_add</span></span>
- <span data-ttu-id="2f02e-1416">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1416">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-1417">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="2f02e-1417">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="2f02e-1418">Importazione di certificati X. 509 in NetX Secure nel capitolo 3.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1418">Importing X.509 Certificates into NetX Secure in Chapter 3.</span></span>

## <a name="nx_secure_x509_common_name_dns_check"></a><span data-ttu-id="2f02e-1419">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-1419">nx_secure_x509_common_name_dns_check</span></span>

<span data-ttu-id="2f02e-1420">Verificare il nome DNS rispetto al certificato X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-1420">Check DNS name against X.509 Certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1421">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1421">Prototype</span></span>

```C
UINT  nx_secure_x509_common_name_dns_check(
                        NX_SECURE_X509_CERT *certificate,
                        const UCHAR *dns_tld, UINT dns_tld_length);
```

### <a name="description"></a><span data-ttu-id="2f02e-1422">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1422">Description</span></span>

<span data-ttu-id="2f02e-1423">Questo servizio controlla il nome comune di un certificato rispetto a un nome di dominio principale (TLD) fornito dal chiamante ai fini della convalida DNS di un host remoto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1423">This service checks a certificate's Common Name against a Top- Domain name (TLD) provided by the caller for the purposes of DNS validation of a remote host.</span></span> <span data-ttu-id="2f02e-1424">Questa funzione di utilità è progettata per essere chiamata dall'interno di una routine di callback di convalida del certificato fornita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1424">This utility function is intended to be called from within a certificate validation callback routine provided by the application.</span></span> <span data-ttu-id="2f02e-1425">Il nome TLD deve essere la parte superiore dell'URL usato per accedere all'host remoto (il "." -stringa separata prima della prima barra).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1425">The TLD name should be the top part of the URL used to access the remote host (the "."-separated string before the first slash).</span></span> <span data-ttu-id="2f02e-1426">Se il nome comune contiene un carattere jolly, ad esempio *. example.com, il carattere jolly corrisponderà a qualsiasi con lo stesso suffisso. Si noti che viene considerato solo il primo carattere jolly ("*") rilevato (lettura da destra a sinistra) per la corrispondenza con caratteri jolly, ad esempio ABC. \*. example. com corrisponderà a *qualsiasi* nome che termina con ". example.com".</span><span class="sxs-lookup"><span data-stu-id="2f02e-1426">If the Common Name contains a wildcard (such as *.example.com), the wildcard will match any with the same suffix. Note that only the first wildcard ("*") encountered (reading right-to-left) will be considered for wildcard matching – for example, abc.\*.example.com will match *any* name ending in ".example.com".</span></span>

<span data-ttu-id="2f02e-1427">Se il nome comune non corrisponde alla stringa specificata, l'estensione "subjectAltName" viene analizzata (se presente nel certificato) e vengono confrontate anche le voci di DNSName.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1427">If the Common Name does not match the provided string, the "subjectAltName" extension is parsed (if it exists in the certificate) and any DNSName entries are also compared.</span></span> <span data-ttu-id="2f02e-1428">Se nessuna di queste voci corrisponde, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1428">If none of those entries match, an error is returned.</span></span>

<span data-ttu-id="2f02e-1429">È importante comprendere il formato del nome comune (e le voci subjectAltName) nei certificati previsti.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1429">It is important to understand the format of the common name (and subjectAltName entries) in expected certificates.</span></span> <span data-ttu-id="2f02e-1430">Ad esempio, alcuni certificati possono utilizzare un indirizzo IP non elaborato o un carattere jolly.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1430">For example, some certificates may use a raw IP address or a wild card.</span></span> <span data-ttu-id="2f02e-1431">La stringa TLD DNS deve essere formattata in modo che corrisponda ai valori previsti nei certificati ricevuti.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1431">The DNS TLD string must be formatted such that it will match the expected values in received certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1432">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1432">Parameters</span></span>

- <span data-ttu-id="2f02e-1433">**certificate_ptr** Puntatore a un'istanza del certificato X. 509.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1433">**certificate_ptr** Pointer to an X.509 Certificate instance.</span></span>
- <span data-ttu-id="2f02e-1434">**dns_tld** Top-Level nome di dominio rispetto al quale eseguire il confronto.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1434">**dns_tld** Top-Level Domain name to compare against.</span></span>
- <span data-ttu-id="2f02e-1435">**dns_tld_length** Lunghezza della stringa TLD.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1435">**dns_tld_length** Length of TLD string.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1436">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1436">Return Values</span></span>

- <span data-ttu-id="2f02e-1437">Il confronto tra **NX_SUCCESS** (0x00) ha esito positivo con il nome comune o SubjectAltName.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1437">**NX_SUCCESS** (0x00) Successful comparison with Common Name or subjectAltName.</span></span>
- <span data-ttu-id="2f02e-1438">**NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH** (0X195) non è stato trovato alcun nome corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1438">**NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH** (0x195) No matching name found.</span></span>
- <span data-ttu-id="2f02e-1439">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1439">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1440">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1440">Allowed From</span></span>

<span data-ttu-id="2f02e-1441">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1441">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1442">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1442">Example</span></span>

```C
/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
ULONG status;
UCHAR *tld = “www.example.com”;

    /* Check our DNS TLD against the certificate provided by the
       remote TLS host. */
    status = nx_secure_x509_common_name_dns_check(certificate, tld, strlen(tld));

        if(status != NX_SUCCESS)
        {
            /* TLD did not match any names in the certificate. */
            return(status);
        }

        /* DNS validation and any other checks were successful. */
        return(NX_SUCCESS);
}

…

/* Add callback to TLS session in TLS setup routine.  */
status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                         certificate_callback);
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1443">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1443">See Also</span></span>

- <span data-ttu-id="2f02e-1444">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1444">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-1445">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1445">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="2f02e-1446">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-1446">nx_secure_x509_crl_revocation_check</span></span>

## <a name="nx_secure_x509_crl_revocation_check"></a><span data-ttu-id="2f02e-1447">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-1447">nx_secure_x509_crl_revocation_check</span></span>

<span data-ttu-id="2f02e-1448">Controllare il certificato X. 509 in base a un elenco di revoche di certificati (CRL) fornito</span><span class="sxs-lookup"><span data-stu-id="2f02e-1448">Check X.509 Certificate against a supplied Certificate Revocation List (CRL)</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1449">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1449">Prototype</span></span>

```C
UINT  nx_secure_x509_crl_revocation_check(const UCHAR *crl_data,
                              UINT crl_length,
                              NX_SECURE_X509_CERTIFICATE_STORE *store,
                              NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a><span data-ttu-id="2f02e-1450">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1450">Description</span></span>

<span data-ttu-id="2f02e-1451">Questo servizio accetta un elenco di revoche di certificati con codifica DER e cerca un certificato specifico in tale elenco.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1451">This service takes a DER-encoded Certificate Revocation List and searches for a specific certificate in that list.</span></span> <span data-ttu-id="2f02e-1452">L'emittente del CRL viene convalidato in base a un archivio certificati fornito, l'emittente CRL viene convalidato in modo che corrisponda a quello per il certificato sottoposto a verifica e il numero di serie del certificato in questione viene usato per la ricerca nell'elenco dei certificati revocati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1452">The issuer of the CRL is validated against a supplied certificate store, the CRL issuer is validated to be the same as the one for the certificate being checked, and the serial number of the certificate in question is used to search the revoked certificates list.</span></span> <span data-ttu-id="2f02e-1453">Se le autorità emittenti corrispondono, la firma si estrae e il certificato **non** è presente nell'elenco, la chiamata ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1453">If the issuers match, the signature checks out, and the certificate is **not** present in the list, the call is successful.</span></span> <span data-ttu-id="2f02e-1454">Tutti gli altri casi provocano la restituzione di un errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1454">All other cases cause an error to be returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1455">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1455">Parameters</span></span>

- <span data-ttu-id="2f02e-1456">**crl_data** Puntatore a un CRL con codifica DER.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1456">**crl_data** Pointer to a DER-encoded CRL.</span></span>
- <span data-ttu-id="2f02e-1457">**crl_length** Lunghezza in byte dei dati CRL.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1457">**crl_length** Length in bytes of CRL data.</span></span>
- <span data-ttu-id="2f02e-1458">**Archivio** di Puntatore a un archivio certificati X. 509.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1458">**store** Pointer to an X.509 Certificate store.</span></span>
- <span data-ttu-id="2f02e-1459">**certificate_ptr** Puntatore a un'istanza del certificato X. 509.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1459">**certificate_ptr** Pointer to an X.509 Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1460">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1460">Return Values</span></span>

- <span data-ttu-id="2f02e-1461">**NX_SUCCESS** (0x00) la convalida ha esito positivo che il certificato non è stato revocato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1461">**NX_SUCCESS** (0x00) Successful validation that the certificate was not revoked.</span></span>
- <span data-ttu-id="2f02e-1462">Impossibile trovare il certificato dell'autorità emittente CRL **NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1462">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) CRL issuer certificate not found.</span></span>
- <span data-ttu-id="2f02e-1463">Il certificato dell'autorità emittente del certificato **NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND** 0x11B) non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1463">**NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND** 0x11B) Certificate issuer certificate not found.</span></span>
- <span data-ttu-id="2f02e-1464">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0X182) il CRL ASN. 1 conteneva un campo di lunghezza non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1464">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) The CRL ASN.1 contained an invalid length field.</span></span>
- <span data-ttu-id="2f02e-1465">**NX_SECURE_X509_UNEXPECTED_ASN1_TAG (0x189)** Il CRL contiene ASN. 1 non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1465">**NX_SECURE_X509_UNEXPECTED_ASN1_TAG(0x189)** The CRL contained invalid ASN.1.</span></span>
- <span data-ttu-id="2f02e-1466">**NX_SECURE_X509_CHAIN_VERIFY_FAILURE** (0X18C) la verifica della catena di certificati non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1466">**NX_SECURE_X509_CHAIN_VERIFY_FAILURE** (0x18C) A certificate chain verification failed.</span></span>
- <span data-ttu-id="2f02e-1467">**NX_SECURE_X509_CRL_ISSUER_MISMATCH** (0X197) CRL e le autorità emittenti di certificati non corrispondono.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1467">**NX_SECURE_X509_CRL_ISSUER_MISMATCH** (0x197) CRL and certificate issuers did not match.</span></span>
- <span data-ttu-id="2f02e-1468">**NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED** 0X198) la firma CRL non è valida.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1468">**NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED** 0x198) The CRL signature was invalid.</span></span>
- <span data-ttu-id="2f02e-1469">**NX_SECURE_X509_CRL_CERTIFICATE_REVOKED** (0X199) il certificato verificato è stato trovato nel CRL ed è quindi revocato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1469">**NX_SECURE_X509_CRL_CERTIFICATE_REVOKED** (0x199) The certificate being checked was found in the CRL and is therefore revoked.</span></span>
- <span data-ttu-id="2f02e-1470">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1470">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1471">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1471">Allowed From</span></span>

<span data-ttu-id="2f02e-1472">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1472">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1473">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1473">Example</span></span>

```C
/* CRL obtained for the expected certificate issuer through some means (downloaded
   from server manually, obtained from CRL endpoint, etc…) */
const UCHAR *crl_data;
UINT crl_length = 300;

/* Callback routine used to perform additional checks on a certificate. */
ULONG certificate_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT
*certificate)
{
ULONG status;
NX_SECURE_X509_CERTIFICATE_STORE *store;

    /* Obtain a certificate store to check against. In the certificate callback,
       it usually makes the most sense to use the store associated with the TLS
       session. */
    store = &session -> nx_secure_tls_credentials.nx_secure_tls_certificate_store;

    /* Check our certificate against the CRL and TLS certificate store. */
    status = nx_secure_x509_crl_revocation_check(crl, crl_length, store,
                                                 certificate);

        if(status != NX_SUCCESS)
        {
            if(status == NX_SECURE_X509_CRL_CERTIFICATE_REVOKED)
            {
                /* Certificate was revoked. */
               return(status);
            }
            else
            {
               /* CRL was invalid or some other issue. In this case the certificate
                  may still be valid since the CRL itself was a problem. At this
                  point it is up to the application to decide whether to continue
                  with the TLS handshake. For this example, assume certificate is
                  valid (faulty CRL is a possible Denial-of-Service attack).*/
               status = NX_SUCCESS;
        }

    /* Other certificate checking can go here. */

    /* Return status of certificate checks. */
    return(status);
}

…

/* Add callback to TLS session in TLS setup routine.  */
status =  nx_secure_tls_session_certificate_callback_set(&tls_session,
                                                         certificate_callback);
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1474">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1474">See Also</span></span>

- <span data-ttu-id="2f02e-1475">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1475">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-1476">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1476">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="2f02e-1477">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-1477">nx_secure_x509_common_name_dns_check</span></span>

## <a name="nx_secure_x509_dns_name_initialize"></a><span data-ttu-id="2f02e-1478">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="2f02e-1478">nx_secure_x509_dns_name_initialize</span></span>

<span data-ttu-id="2f02e-1479">Inizializzare una struttura del nome DNS X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-1479">Initialize an X.509 DNS name structure</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1480">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1480">Prototype</span></span>

```C
UINT  nx_secure_x509_dns_name_initialize(
                        NX_SECURE_X509_DNS_NAME *dns_name,
                        const UCHAR *name_string, UINT length);
```

### <a name="description"></a><span data-ttu-id="2f02e-1481">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1481">Description</span></span>

<span data-ttu-id="2f02e-1482">Questo servizio Inizializza un nome DNS X. 509 da usare con determinati servizi API che richiedono un formato di nome specifico.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1482">This service initializes an X.509 DNS name for use with certain API services requiring a specific name format.</span></span> <span data-ttu-id="2f02e-1483">Ad esempio, il servizio *nx_secure_tls_sni_extension_parse* prevede un oggetto NX_SECURE_X509_DNS_NAME in modo che corrisponda al nome fornito da un host remoto nell'estensione indicazione nome server durante l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1483">For example, the *nx_secure_tls_sni_extension_parse* service expects an NX_SECURE_X509_DNS_NAME object in order to match the name provided by a remote host in the Server Name Indication extension during the TLS handshake.</span></span> <span data-ttu-id="2f02e-1484">Un nome DNS è semplicemente una stringa charater con lunghezza, ovvero la lunghezza massima consentita di un nome DNS (e la dimensione del buffer interno in NX_SECURE_X509_DNS_NAME) è controllata dalla macro NX_SECURE_X509_DNS_NAME_MAX (valore predefinito 100 byte).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1484">A DNS name is simply a charater string with a length – the maximum allowed length of a DNS name (and the size of the internal buffer in NX_SECURE_X509_DNS_NAME) is controlled by the macro NX_SECURE_X509_DNS_NAME_MAX (default 100 bytes).</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1485">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1485">Parameters</span></span>

- <span data-ttu-id="2f02e-1486">**dns_name** Struttura del nome DNS da inizializzare.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1486">**dns_name** DNS name structure to initialize.</span></span>
- <span data-ttu-id="2f02e-1487">**name_string** Dati della stringa del nome DNS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1487">**name_string** DNS name string data.</span></span>
- <span data-ttu-id="2f02e-1488">**lunghezza** Lunghezza della stringa del nome.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1488">**length** Length of name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1489">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1489">Return Values</span></span>

- <span data-ttu-id="2f02e-1490">**NX_SUCCESS** (0x00) inizializzazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1490">**NX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="2f02e-1491">**NX_SECURE_X509_NAME_STRING_TOO_LONG** (0x19E) è stata superata la stringa del nome specificata NX_SECURE_X509_DNS_NAME_MAX.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1491">**NX_SECURE_X509_NAME_STRING_TOO_LONG** (0x19E) The given name string exceeded NX_SECURE_X509_DNS_NAME_MAX.</span></span>
- <span data-ttu-id="2f02e-1492">**NX_PTR_ERROR** (0x07) ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1492">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1493">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1493">Allowed From</span></span>

<span data-ttu-id="2f02e-1494">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1494">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1495">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1495">Example</span></span>

```C
NX_SECURE_X509_DNS_NAME dns_name;

/* Initialize DNS name. */
status = nx_secure_x509_dns_name_initialize(&dns_name, “www.example.com”,
                                            strlen(“www.example.com”);

/* Use initialized DNS name to send the Server Name Indication extension to the
   remote TLS server. */
status = nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1496">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1496">See Also</span></span>

- <span data-ttu-id="2f02e-1497">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="2f02e-1497">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="2f02e-1498">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-1498">nx_secure_tls_session_sni_extension_parse</span></span>
- <span data-ttu-id="2f02e-1499">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1499">nx_secure_tls_session_sni_extension_set</span></span>

## <a name="nx_secure_x509_extended_key_usage_extension_parse"></a><span data-ttu-id="2f02e-1500">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-1500">nx_secure_x509_extended_key_usage_extension_parse</span></span>

<span data-ttu-id="2f02e-1501">Trovare e analizzare un'estensione per l'utilizzo delle chiavi estese X. 509 in un certificato X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-1501">Find and parse an X.509 extended key usage extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1502">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1502">Prototype</span></span>

```C
UINT  nx_secure_x509_extended_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        UINT key_usage);
```

### <a name="description"></a><span data-ttu-id="2f02e-1503">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1503">Description</span></span>

<span data-ttu-id="2f02e-1504">Questo servizio è destinato a essere chiamato dall'interno di un callback di verifica del certificato (vedere *nx_secure_tls_session_certificate_callback_set)*.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1504">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)*.</span></span> <span data-ttu-id="2f02e-1505">Eseguirà la ricerca di un OID di utilizzo chiave esteso specifico all'interno di un certificato X. 509 e restituirà se l'OID è presente.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1505">It will search for a specific extended key usage OID within an X.509 certificate and return whether the OID is present.</span></span> <span data-ttu-id="2f02e-1506">Il key_usage parametro è un mapping di tipo Integer di OID che viene utilizzato internamente da NetX Secure X. 509 e TLS per evitare di passare le stringhe OID a lunghezza variabile come parametri.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1506">The key_usage parameter is an integer mapping of the OIDs which is used internally by NetX Secure X.509 and TLS to avoid passing the variable-length OID strings as parameters.</span></span>

<span data-ttu-id="2f02e-1507">Nella tabella seguente vengono forniti i OID rilevanti per l'estensione utilizzo chiavi avanzato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1507">The relevant OIDs for the extended key usage extension are given in the table below.</span></span> <span data-ttu-id="2f02e-1508">Una tipica implementazione del client TLS che desidera controllare l'utilizzo della chiave estesa in un certificato del server TLS ricevuto verificherebbe l'esistenza dell'OID NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH: se l'estensione è presente, ma tale OID non lo è, il certificato verrebbe considerato non valido per identifiying l'host come server TLS e il callback di verifica del certificato dovrebbe restituire un errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1508">A typical TLS Client implementation wishing to check extended key usage in a received TLS server certificate would check for the existence of the OID NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH – if the extension is present but that OID is not, then the certificate would be considered invalid for identifiying the host as a TLS server and the certificate verification callback should return an error.</span></span> <span data-ttu-id="2f02e-1509">Se non è presente l'estensione, è possibile che l'applicazione proceda o meno con l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1509">If the extension itself is missing, then it is up to the application whether or not to proceed with the TLS handshake.</span></span>

<span data-ttu-id="2f02e-1510">Nel callback di verifica del certificato, il codice restituito dall'errore NX_SECURE_X509_KEY_USAGE_ERROR è riservato per l'utilizzo da parte dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1510">In the certificate verification callback, the error return code NX_SECURE_X509_KEY_USAGE_ERROR is reserved for application use.</span></span> <span data-ttu-id="2f02e-1511">Se si verifica un errore durante il controllo dell'utilizzo della chiave, questo valore può essere restituito dal callback per indicare la causa dell'errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1511">If there is an error in checking key usage, this value may be returned from the callback to indicate the reason for failure.</span></span>

| <span data-ttu-id="2f02e-1512">Identificatore sicuro NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-1512">NetX Secure Identifier</span></span>                                | <span data-ttu-id="2f02e-1513">Valore OID</span><span class="sxs-lookup"><span data-stu-id="2f02e-1513">OID Value</span></span>         | <span data-ttu-id="2f02e-1514">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1514">Description</span></span>                                      |
| --------------------------------------------------------- | --------------------- | ---------------------------------------------------- |
| <span data-ttu-id="2f02e-1515">NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH</span><span class="sxs-lookup"><span data-stu-id="2f02e-1515">NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH</span></span>   | <span data-ttu-id="2f02e-1516">1.3.6.1.5.5.7.3.1</span><span class="sxs-lookup"><span data-stu-id="2f02e-1516">1.3.6.1.5.5.7.3.1</span></span> | <span data-ttu-id="2f02e-1517">Il certificato può essere usato per identificare un server TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-1517">Certificate can be used to identify a TLS server</span></span> |
| <span data-ttu-id="2f02e-1518">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CLIENT_AUTH</span><span class="sxs-lookup"><span data-stu-id="2f02e-1518">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CLIENT_AUTH</span></span>   | <span data-ttu-id="2f02e-1519">1.3.6.1.5.5.7.3.2</span><span class="sxs-lookup"><span data-stu-id="2f02e-1519">1.3.6.1.5.5.7.3.2</span></span> | <span data-ttu-id="2f02e-1520">Il certificato può essere usato per identificare un client TLS</span><span class="sxs-lookup"><span data-stu-id="2f02e-1520">Certificate can be used to identify a TLS client</span></span> |
| <span data-ttu-id="2f02e-1521">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CODE_SIGNING</span><span class="sxs-lookup"><span data-stu-id="2f02e-1521">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CODE_SIGNING</span></span>  | <span data-ttu-id="2f02e-1522">1.3.6.1.5.5.7.3.3</span><span class="sxs-lookup"><span data-stu-id="2f02e-1522">1.3.6.1.5.5.7.3.3</span></span> | <span data-ttu-id="2f02e-1523">Il certificato può essere usato per firmare il codice</span><span class="sxs-lookup"><span data-stu-id="2f02e-1523">Certificate can be used to sign code</span></span>             |
| <span data-ttu-id="2f02e-1524">NX_SECURE_TLS_X509_TYPE_PKIX_KP_EMAIL_PROTECT</span><span class="sxs-lookup"><span data-stu-id="2f02e-1524">NX_SECURE_TLS_X509_TYPE_PKIX_KP_EMAIL_PROTECT</span></span> | <span data-ttu-id="2f02e-1525">1.3.6.1.5.5.7.3.4</span><span class="sxs-lookup"><span data-stu-id="2f02e-1525">1.3.6.1.5.5.7.3.4</span></span> | <span data-ttu-id="2f02e-1526">Il certificato può essere usato per firmare i messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="2f02e-1526">Certificate can be used to sign emails</span></span>           |
| <span data-ttu-id="2f02e-1527">NX_SECURE_TLS_X509_TYPE_PKIX_KP_TIME_STAMPING</span><span class="sxs-lookup"><span data-stu-id="2f02e-1527">NX_SECURE_TLS_X509_TYPE_PKIX_KP_TIME_STAMPING</span></span> | <span data-ttu-id="2f02e-1528">1.3.6.1.5.5.7.3.8</span><span class="sxs-lookup"><span data-stu-id="2f02e-1528">1.3.6.1.5.5.7.3.8</span></span> | <span data-ttu-id="2f02e-1529">Il certificato può essere usato per firmare i timestamp</span><span class="sxs-lookup"><span data-stu-id="2f02e-1529">Certificate can be used to sign timestamps</span></span>       |
| <span data-ttu-id="2f02e-1530">NX_SECURE_TLS_X509_TYPE_PKIX_KP_OCSP_SIGNING</span><span class="sxs-lookup"><span data-stu-id="2f02e-1530">NX_SECURE_TLS_X509_TYPE_PKIX_KP_OCSP_SIGNING</span></span>  | <span data-ttu-id="2f02e-1531">1.3.6.1.5.5.7.3.9</span><span class="sxs-lookup"><span data-stu-id="2f02e-1531">1.3.6.1.5.5.7.3.9</span></span> | <span data-ttu-id="2f02e-1532">Il certificato può essere usato per firmare le risposte OCSP</span><span class="sxs-lookup"><span data-stu-id="2f02e-1532">Certificate can be used to sign OCSP responses</span></span>   |

<span data-ttu-id="2f02e-1533">OID e mapping per l'estensione utilizzo chiavi esteso X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-1533">OIDs and mappings for X.509 Extended Key Usage Extension</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1534">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1534">Parameters</span></span>

- <span data-ttu-id="2f02e-1535">**certificato** di Puntatore al certificato da verificare.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1535">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="2f02e-1536">**KEY_USAGE** Mapping Integer OID dalla tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1536">**key_usage** OID integer mapping from table above.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1537">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1537">Return Values</span></span>

- <span data-ttu-id="2f02e-1538">È stato trovato l'OID di utilizzo della chiave specificato **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1538">**NX_SUCCESS** (0x00) Specified key usage OID found.</span></span>
- <span data-ttu-id="2f02e-1539">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) è stato rilevato un tag a più byte ASN. 1 (certificato non supportato).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1539">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="2f02e-1540">È stato rilevato il campo ASN. 1 **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) invaild (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1540">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="2f02e-1541">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) classe di tag ASN. 1 non valida rilevata (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1541">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="2f02e-1542">È stata rilevata un'estensione di **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0X192) non valida. certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1542">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered (invalid certificate).</span></span>
- <span data-ttu-id="2f02e-1543">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) Impossibile trovare l'estensione utilizzo chiavi avanzato nel certificato fornito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1543">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) The Extended Key Usage extension was not found in the provided certificate.</span></span>
- <span data-ttu-id="2f02e-1544">Puntatore al certificato **NX_PTR_ERROR** (0x07) non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1544">**NX_PTR_ERROR** (0x07) Invalid certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1545">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1545">Allowed From</span></span>

<span data-ttu-id="2f02e-1546">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1546">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1547">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1547">Example</span></span>

```C
ULONG certificate_verification_callback(NX_SECURE_TLS_SESSION *session, NX_SECURE_X509_CERT* certificate)
{
UINT status;

    /* Extended key usage - look for specific OIDs. */
    status = nx_secure_x509_extended_key_usage_extension_parse(certificate,
                        NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH);

    if(status != NX_SUCCESS)
    {
        if(NX_SECURE_X509_EXT_KEY_USAGE_NOT_FOUND)
        {
            printf("Extended key usage extension not found or specified key usage OID not
                    provided in extension.\n");
            /* The certificate was valid but the specified OID was not found. The
               application can decide whether to continue or abort the TLS handshake. */
            return(NX_SECURE_X509_KEY_USAGE_ERROR);
        }
        else
        {
            /* The extension or certificate was invalid. */
            return(status);
        }
    }

    /* The specified OID was found, return success! */
    return(NX_SUCCESS);
}
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1548">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1548">See Also</span></span>

- <span data-ttu-id="2f02e-1549">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1549">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="2f02e-1550">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-1550">nx_secure_x509_key_usage_extension_parse</span></span>
- <span data-ttu-id="2f02e-1551">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-1551">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="2f02e-1552">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-1552">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="2f02e-1553">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-1553">nx_secure_x509_extension_find</span></span>

## <a name="nx_secure_x509_extension_find"></a><span data-ttu-id="2f02e-1554">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-1554">nx_secure_x509_extension_find</span></span>

<span data-ttu-id="2f02e-1555">Trovare e restituire un'estensione X. 509 in un certificato X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-1555">Find and return an X.509 extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1556">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1556">Prototype</span></span>

```C
UINT  nx_secure_x509_extension_find(
                        NX_SECURE_X509_CERT *certificate,
                        NX_SECURE_X509_EXTENSION *extension,
                        USHORT extension_id);
```

### <a name="description"></a><span data-ttu-id="2f02e-1557">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1557">Description</span></span>

<span data-ttu-id="2f02e-1558">Questo servizio è destinato a essere chiamato dall'interno di un callback di verifica del certificato (vedere *nx_secure_tls_session_certificate_callback_set)* ed è un servizio X. 509 avanzato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1558">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)* and is an advanced X.509 service.</span></span>

<span data-ttu-id="2f02e-1559">La funzione eseguirà la ricerca di un'estensione specifica all'interno di un certificato X. 509 in base a un OID e restituirà se l'OID è presente, insieme a una struttura che contiene riferimenti ai dati di estensione non elaborati pertinenti.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1559">The function will search for a specific extension within an X.509 certificate based on an OID and return whether the OID is present, along with a structure containing references to the relevant raw extension data.</span></span> <span data-ttu-id="2f02e-1560">Il extension_id parametro è un mapping di tipo Integer di OID che viene utilizzato internamente da NetX Secure X. 509 e TLS per evitare di passare le stringhe OID a lunghezza variabile come parametri.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1560">The extension_id parameter is an integer mapping of the OIDs which is used internally by NetX Secure X.509 and TLS to avoid passing the variable-length OID strings as parameters.</span></span>

<span data-ttu-id="2f02e-1561">Le funzioni di supporto fornite per estensioni specifiche (ad esempio *nx_secure_x509_key_usage_extension_parse*) chiamano nx_secure_x509_extension_find internamente per ottenere i dati dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1561">The helper functions provided for specific extensions (such as *nx_secure_x509_key_usage_extension_parse*) call nx_secure_x509_extension_find internally to obtain the extension data.</span></span>

<span data-ttu-id="2f02e-1562">Nella tabella seguente vengono forniti i OID rilevanti per le estensioni X. 509 note.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1562">The relevant OIDs for known X.509 extensions are given in the table below.</span></span>

<span data-ttu-id="2f02e-1563">La struttura NX_SECURE_X509_EXTENSION contiene puntatori al certificato X. 509 che consentono alle funzioni di supporto, ad esempio *nx_secure_x509_key_usage_extension_parse* di decodificare rapidamente i dati ASN. 1 con codifica der di estensione non elaborata.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1563">The NX_SECURE_X509_EXTENSION structure contains pointers into the X.509 certificate that allow helper functions such as *nx_secure_x509_key_usage_extension_parse* to quickly decode the raw extension DER-encoded ASN.1 data.</span></span>

<span data-ttu-id="2f02e-1564">Per informazioni sulle estensioni specifiche, vedere RFC 5280 (specifica X. 509) o il riferimento per le funzioni di supporto appropriate, se disponibili.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1564">For information on specific extensions, see RFC 5280 (X.509 specification) or the reference for the appropriate helper functions if available.</span></span>

<span data-ttu-id="2f02e-1565">La versione corrente di NetX Secure X. 509 ha un supporto limitato per le estensioni X. 509.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1565">The current version of NetX Secure X.509 has limited support for X.509 extensions.</span></span> <span data-ttu-id="2f02e-1566">In futuro verranno aggiunte altre funzioni helper.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1566">More helper functions will be added in the future.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f02e-1567">*Questo servizio è una funzionalità avanzata per gli utenti che hanno familiarità con le estensioni X. 509 e la codifica DER ASN. 1. Viene fornito per consentire a tali utenti di accedere alle estensioni per le quali NetX Secure X. 509 attualmente non fornisce funzioni di supporto. Per tali estensioni senza funzioni di supporto, sarà necessario analizzare il file ASN. 1 con codifica DER non elaborato.*</span><span class="sxs-lookup"><span data-stu-id="2f02e-1567">*This service is an advanced feature for users familiar with X.509 extensions and DER-encoded ASN.1. It is provided to enable those users to access extensions for which NetX Secure X.509 does not currently provide helper functions. For those extensions without helper functions, you will have to parse the raw DER-encoded ASN.1 yourself.*</span></span>

| <span data-ttu-id="2f02e-1568">Identificatore sicuro NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-1568">NetX Secure Identifier</span></span>                              | <span data-ttu-id="2f02e-1569">Valore OID</span><span class="sxs-lookup"><span data-stu-id="2f02e-1569">OID Value</span></span> | <span data-ttu-id="2f02e-1570">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1570">Description</span></span>                                                                    | <span data-ttu-id="2f02e-1571">Funzione helper?</span><span class="sxs-lookup"><span data-stu-id="2f02e-1571">Helper function?</span></span> |
| ------------------------------------------------------- | ------------- | ---------------------------------------------------------------------------------- | -------------------- |
| <span data-ttu-id="2f02e-1572">NX_SECURE_TLS_X509_TYPE_DIRECTORY_ATTRIBUTES</span><span class="sxs-lookup"><span data-stu-id="2f02e-1572">NX_SECURE_TLS_X509_TYPE_DIRECTORY_ATTRIBUTES</span></span>  | <span data-ttu-id="2f02e-1573">2.5.29.9</span><span class="sxs-lookup"><span data-stu-id="2f02e-1573">2.5.29.9</span></span>  | <span data-ttu-id="2f02e-1574">Attributi di directory: attributi di informazioni di base sul soggetto del certificato</span><span class="sxs-lookup"><span data-stu-id="2f02e-1574">Directory Attributes – basic information attributes about certificate subject</span></span>  | <span data-ttu-id="2f02e-1575">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1575">No</span></span>               |
| <span data-ttu-id="2f02e-1576">NX_SECURE_TLS_X509_TYPE_SUBJECT_KEY_ID</span><span class="sxs-lookup"><span data-stu-id="2f02e-1576">NX_SECURE_TLS_X509_TYPE_SUBJECT_KEY_ID</span></span>       | <span data-ttu-id="2f02e-1577">2.5.29.14</span><span class="sxs-lookup"><span data-stu-id="2f02e-1577">2.5.29.14</span></span> | <span data-ttu-id="2f02e-1578">Usato per identificare una chiave pubblica specifica</span><span class="sxs-lookup"><span data-stu-id="2f02e-1578">Used to identify a specific public key</span></span>                                         | <span data-ttu-id="2f02e-1579">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1579">No</span></span>               |
| <span data-ttu-id="2f02e-1580">NX_SECURE_TLS_X509_TYPE_KEY_USAGE</span><span class="sxs-lookup"><span data-stu-id="2f02e-1580">NX_SECURE_TLS_X509_TYPE_KEY_USAGE</span></span>             | <span data-ttu-id="2f02e-1581">2.5.29.15</span><span class="sxs-lookup"><span data-stu-id="2f02e-1581">2.5.29.15</span></span> | <span data-ttu-id="2f02e-1582">Fornisce informazioni sugli utilizzi validi per la chiave pubblica del certificato</span><span class="sxs-lookup"><span data-stu-id="2f02e-1582">Provides information on valid uses for the certificate public key</span></span>              | <span data-ttu-id="2f02e-1583">Sì</span><span class="sxs-lookup"><span data-stu-id="2f02e-1583">Yes</span></span>              |
| <span data-ttu-id="2f02e-1584">NX_SECURE_TLS_X509_TYPE_SUBJECT_ALT_NAME</span><span class="sxs-lookup"><span data-stu-id="2f02e-1584">NX_SECURE_TLS_X509_TYPE_SUBJECT_ALT_NAME</span></span>     | <span data-ttu-id="2f02e-1585">2.5.29.17</span><span class="sxs-lookup"><span data-stu-id="2f02e-1585">2.5.29.17</span></span> | <span data-ttu-id="2f02e-1586">Fornisce nomi DNS alternativi per identificare il certificato</span><span class="sxs-lookup"><span data-stu-id="2f02e-1586">Provides alternative DNS names to identify the certificate</span></span>                     | <span data-ttu-id="2f02e-1587">Sì<sup>24</sup></span><span class="sxs-lookup"><span data-stu-id="2f02e-1587">Yes<sup>24</sup></span></span>        |
| <span data-ttu-id="2f02e-1588">NX_SECURE_TLS_X509_TYPE_ISSUER_ALT_NAME</span><span class="sxs-lookup"><span data-stu-id="2f02e-1588">NX_SECURE_TLS_X509_TYPE_ISSUER_ALT_NAME</span></span>      | <span data-ttu-id="2f02e-1589">2.5.29.18</span><span class="sxs-lookup"><span data-stu-id="2f02e-1589">2.5.29.18</span></span> | <span data-ttu-id="2f02e-1590">Fornisce nomi DNS alternativi per identificare l'emittente del certificato</span><span class="sxs-lookup"><span data-stu-id="2f02e-1590">Provides alternative DNS names to identify the certificate's issuer</span></span>            | <span data-ttu-id="2f02e-1591">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1591">No</span></span>               |
| <span data-ttu-id="2f02e-1592">NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="2f02e-1592">NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS</span></span>     | <span data-ttu-id="2f02e-1593">2.5.29.19</span><span class="sxs-lookup"><span data-stu-id="2f02e-1593">2.5.29.19</span></span> | <span data-ttu-id="2f02e-1594">Fornisce informazioni di base sui vincoli di utilizzo del certificato</span><span class="sxs-lookup"><span data-stu-id="2f02e-1594">Provides basic certificate usage constraint information</span></span>                        | <span data-ttu-id="2f02e-1595">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1595">No</span></span>               |
| <span data-ttu-id="2f02e-1596">NX_SECURE_TLS_X509_TYPE_NAME_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="2f02e-1596">NX_SECURE_TLS_X509_TYPE_NAME_CONSTRAINTS</span></span>      | <span data-ttu-id="2f02e-1597">2.5.29.30</span><span class="sxs-lookup"><span data-stu-id="2f02e-1597">2.5.29.30</span></span> | <span data-ttu-id="2f02e-1598">Usato per vincolare i nomi dei certificati a domini specifici</span><span class="sxs-lookup"><span data-stu-id="2f02e-1598">Used to constrain certificate names to specific domains</span></span>                        | <span data-ttu-id="2f02e-1599">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1599">No</span></span>               |
| <span data-ttu-id="2f02e-1600">NX_SECURE_TLS_X509_TYPE_CRL_DISTRIBUTION</span><span class="sxs-lookup"><span data-stu-id="2f02e-1600">NX_SECURE_TLS_X509_TYPE_CRL_DISTRIBUTION</span></span>      | <span data-ttu-id="2f02e-1601">2.5.29.31</span><span class="sxs-lookup"><span data-stu-id="2f02e-1601">2.5.29.31</span></span> | <span data-ttu-id="2f02e-1602">Fornisce gli URI per la distribuzione CRL</span><span class="sxs-lookup"><span data-stu-id="2f02e-1602">Provides URIs for CRL distribution</span></span>                                             | <span data-ttu-id="2f02e-1603">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1603">No</span></span>               |
| <span data-ttu-id="2f02e-1604">NX_SECURE_TLS_X509_TYPE_CERTIFICATE_POLICIES</span><span class="sxs-lookup"><span data-stu-id="2f02e-1604">NX_SECURE_TLS_X509_TYPE_CERTIFICATE_POLICIES</span></span>  | <span data-ttu-id="2f02e-1605">2.5.29.32</span><span class="sxs-lookup"><span data-stu-id="2f02e-1605">2.5.29.32</span></span> | <span data-ttu-id="2f02e-1606">Elenco dei criteri di certificato per i sistemi PKI di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="2f02e-1606">List of certificate policies for large PKI systems</span></span>                             | <span data-ttu-id="2f02e-1607">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1607">No</span></span>               |
| <span data-ttu-id="2f02e-1608">NX_SECURE_TLS_X509_TYPE_CERT_POLICY_MAPPINGS</span><span class="sxs-lookup"><span data-stu-id="2f02e-1608">NX_SECURE_TLS_X509_TYPE_CERT_POLICY_MAPPINGS</span></span> | <span data-ttu-id="2f02e-1609">2.5.29.33</span><span class="sxs-lookup"><span data-stu-id="2f02e-1609">2.5.29.33</span></span> | <span data-ttu-id="2f02e-1610">Elenco dei criteri del certificato della CA</span><span class="sxs-lookup"><span data-stu-id="2f02e-1610">List of CA certificate policies</span></span>                                                | <span data-ttu-id="2f02e-1611">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1611">No</span></span>               |
| <span data-ttu-id="2f02e-1612">NX_SECURE_TLS_X509_TYPE_AUTHORITY_KEY_ID</span><span class="sxs-lookup"><span data-stu-id="2f02e-1612">NX_SECURE_TLS_X509_TYPE_AUTHORITY_KEY_ID</span></span>     | <span data-ttu-id="2f02e-1613">2.5.29.35</span><span class="sxs-lookup"><span data-stu-id="2f02e-1613">2.5.29.35</span></span> | <span data-ttu-id="2f02e-1614">Usato per identificare una chiave pubblica specifica associata a una firma del certificato</span><span class="sxs-lookup"><span data-stu-id="2f02e-1614">Used to identify a specific public key associated with a certificate signature</span></span> | <span data-ttu-id="2f02e-1615">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1615">No</span></span>               |
| <span data-ttu-id="2f02e-1616">NX_SECURE_TLS_X509_TYPE_POLICY_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="2f02e-1616">NX_SECURE_TLS_X509_TYPE_POLICY_CONSTRAINTS</span></span>    | <span data-ttu-id="2f02e-1617">2.5.29.36</span><span class="sxs-lookup"><span data-stu-id="2f02e-1617">2.5.29.36</span></span> | <span data-ttu-id="2f02e-1618">Vincoli dei criteri della CA</span><span class="sxs-lookup"><span data-stu-id="2f02e-1618">CA policy constraints</span></span>                                                          | <span data-ttu-id="2f02e-1619">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1619">No</span></span>               |
| <span data-ttu-id="2f02e-1620">NX_SECURE_TLS_X509_TYPE_EXTENDED_KEY_USAGE</span><span class="sxs-lookup"><span data-stu-id="2f02e-1620">NX_SECURE_TLS_X509_TYPE_EXTENDED_KEY_USAGE</span></span>   | <span data-ttu-id="2f02e-1621">2.5.29.37</span><span class="sxs-lookup"><span data-stu-id="2f02e-1621">2.5.29.37</span></span> | <span data-ttu-id="2f02e-1622">Informazioni aggiuntive sull'utilizzo della chiave basato su OID</span><span class="sxs-lookup"><span data-stu-id="2f02e-1622">Additional OID-based key usage information</span></span>                                     | <span data-ttu-id="2f02e-1623">Sì</span><span class="sxs-lookup"><span data-stu-id="2f02e-1623">Yes</span></span>              |
| <span data-ttu-id="2f02e-1624">NX_SECURE_TLS_X509_TYPE_FRESHEST_CRL</span><span class="sxs-lookup"><span data-stu-id="2f02e-1624">NX_SECURE_TLS_X509_TYPE_FRESHEST_CRL</span></span>          | <span data-ttu-id="2f02e-1625">2.5.29.46</span><span class="sxs-lookup"><span data-stu-id="2f02e-1625">2.5.29.46</span></span> | <span data-ttu-id="2f02e-1626">Fornisce informazioni per ottenere Delta CRL</span><span class="sxs-lookup"><span data-stu-id="2f02e-1626">Provides information for obtaining delta CRLs</span></span>                                  | <span data-ttu-id="2f02e-1627">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1627">No</span></span>               |
| <span data-ttu-id="2f02e-1628">NX_SECURE_TLS_X509_TYPE_INHIBIT_ANYPOLICY</span><span class="sxs-lookup"><span data-stu-id="2f02e-1628">NX_SECURE_TLS_X509_TYPE_INHIBIT_ANYPOLICY</span></span>     | <span data-ttu-id="2f02e-1629">2.5.29.54</span><span class="sxs-lookup"><span data-stu-id="2f02e-1629">2.5.29.54</span></span> | <span data-ttu-id="2f02e-1630">Campo certificato CA che indica che non è possibile usare AnyPolicy</span><span class="sxs-lookup"><span data-stu-id="2f02e-1630">CA certificate field indicating that AnyPolicy cannot be used</span></span>                  | <span data-ttu-id="2f02e-1631">No</span><span class="sxs-lookup"><span data-stu-id="2f02e-1631">No</span></span>               |

<span data-ttu-id="2f02e-1632">OID e mapping per le estensioni X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-1632">OIDs and mappings for X.509 Extensions</span></span>

24. <span data-ttu-id="2f02e-1633">L'estensione SubjectAltName viene analizzata come parte del controllo del nome DNS nel servizio nx_secure_x509_common_name_dns_check.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1633">The SubjectAltName extension is parsed as part of the DNS name check in the service nx_secure_x509_common_name_dns_check.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1634">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1634">Parameters</span></span>

- <span data-ttu-id="2f02e-1635">**certificato** di Puntatore al certificato da verificare.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1635">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="2f02e-1636">**estensione** di Struttura restituita contenente il puntatore e la lunghezza dei dati di estensione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1636">**extension** Return structure containing extension data pointer and length.</span></span>
- <span data-ttu-id="2f02e-1637">**extension_id** Mapping Integer OID dalla tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1637">**extension_id** OID integer mapping from table above.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1638">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1638">Return Values</span></span>

- <span data-ttu-id="2f02e-1639">È stato trovato un OID di estensione specificato **NX_SUCCESS** (0x00) e i dati restituiti.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1639">**NX_SUCCESS** (0x00) Specified extension OID found and data returned.</span></span>
- <span data-ttu-id="2f02e-1640">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) è stato rilevato un tag a più byte ASN. 1 (certificato non supportato).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1640">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="2f02e-1641">È stato rilevato il campo ASN. 1 **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) invaild (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1641">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="2f02e-1642">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) classe di tag ASN. 1 non valida rilevata (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1642">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="2f02e-1643">Rilevata estensione **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0X192) non valida</span><span class="sxs-lookup"><span data-stu-id="2f02e-1643">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered</span></span>
- <span data-ttu-id="2f02e-1644">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0X19B) l'OID di estensione specificato non è stato trovato nel certificato fornito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1644">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) The given extension OID was not found in the provided certificate.</span></span>
- <span data-ttu-id="2f02e-1645">**NX_PTR_ERROR** (0x07) o un puntatore di estensione non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1645">**NX_PTR_ERROR** (0x07) Invalid certificate or extension pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1646">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1646">Allowed From</span></span>

<span data-ttu-id="2f02e-1647">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1647">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1648">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1648">Example</span></span>

```C
/* Function to parse a Basic Constraints X.509 extension. */
UINT _basic_constraints_extension_parse(NX_SECURE_X509_CERT *certificate)
{
const UCHAR             *current_buffer;
ULONG                    length;
UINT                     status;
NX_SECURE_X509_EXTENSION extension_data;

    /* Find the Basic Constraints extension in the certificate. */
    status = _nx_secure_x509_extension_find(certificate, &extension_data,
                              NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS);

    /* See if extension present - it might be OK if not present! */
    if (status != NX_SUCCESS)
    {
        return(status);
    }

    /* The extension_data structure now points to the raw extension ASN.1
      (DER-encoded). */
    current_buffer = extension_data.nx_secure_x509_extension_data;
    length = extension_data.nx_secure_x509_extension_data_length;

   /* Extension ASN.1 parsing… */

   return(NX_SUCCESS);
}
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1649">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1649">See Also</span></span>

- <span data-ttu-id="2f02e-1650">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1650">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="2f02e-1651">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-1651">nx_secure_x509_key_usage_extension_parse</span></span>
- <span data-ttu-id="2f02e-1652">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-1652">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="2f02e-1653">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-1653">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="2f02e-1654">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-1654">nx_secure_x509_extended_key_usage_extension_parse</span></span>

## <a name="nx_secure_x509_key_usage_extension_parse"></a><span data-ttu-id="2f02e-1655">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-1655">nx_secure_x509_key_usage_extension_parse</span></span>

<span data-ttu-id="2f02e-1656">Trovare e analizzare un'estensione per l'utilizzo della chiave X. 509 in un certificato X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-1656">Find and parse an X.509 Key Usage extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="2f02e-1657">Prototipo</span><span class="sxs-lookup"><span data-stu-id="2f02e-1657">Prototype</span></span>

```C
UINT  nx_secure_x509_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        USHORT *bitfield);
```

### <a name="description"></a><span data-ttu-id="2f02e-1658">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1658">Description</span></span>

<span data-ttu-id="2f02e-1659">Questo servizio è destinato a essere chiamato dall'interno di un callback di verifica del certificato (vedere *nx_secure_tls_session_certificate_callback_set)*.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1659">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)*.</span></span> <span data-ttu-id="2f02e-1660">Eseguirà la ricerca dell'estensione per l'utilizzo delle chiavi e, se presente, restituirà l'utilizzo della chiave bit nel parametro "bit".</span><span class="sxs-lookup"><span data-stu-id="2f02e-1660">It will search for the Key Usage extension and if found, will return the Key Usage bitfield in the "bitfield" parameter.</span></span>

<span data-ttu-id="2f02e-1661">I bit, come definito dalla specifica X. 509 (RFC 5280) sono forniti nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1661">The bits, as defined by the X.509 specification (RFC 5280) are given in the table below.</span></span> <span data-ttu-id="2f02e-1662">Un operatore AND bit per bit con la maschera di bit appropriata (e il controllo di un valore diverso da zero) fornirà il valore di ogni bit.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1662">A bitwise AND with the appropriate bitmask (and checking for non-zero) will give the value of each bit.</span></span>

<span data-ttu-id="2f02e-1663">Si noti che la codifica DER del bit Elimina gli zeri aggiuntivi, in modo che la posizione effettiva dei bit nei dati del certificato non elaborato sarà probabilmente diversa dalle rispettive posizioni nel bit decodificato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1663">Note that the DER-encoding of the bitfield eliminates extra zeroes so the actual position of the bits in the raw certificate data will likely be different from their positions in the decoded bitfield.</span></span> <span data-ttu-id="2f02e-1664">Le maschere di bit fornite sono destinate solo all'uso nei bit decodificati restituiti da *nx_secure_x509_key_usage_extension_parse* e non con i dati del certificato con codifica der non elaborati.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1664">The supplied bitmasks are only intended to be used on the decoded bitfield returned by *nx_secure_x509_key_usage_extension_parse* and not with the raw DER-encoded certificate data.</span></span>

<span data-ttu-id="2f02e-1665">Nel callback di verifica del certificato, il codice restituito dall'errore NX_SECURE_X509_KEY_USAGE_ERROR è riservato per l'utilizzo da parte dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1665">In the certificate verification callback, the error return code NX_SECURE_X509_KEY_USAGE_ERROR is reserved for application use.</span></span> <span data-ttu-id="2f02e-1666">Se si verifica un errore durante il controllo dell'utilizzo della chiave, questo valore può essere restituito dal callback per indicare la causa dell'errore.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1666">If there is an error in checking key usage, this value may be returned from the callback to indicate the reason for failure.</span></span>

| <span data-ttu-id="2f02e-1667">Identificatore sicuro NetX</span><span class="sxs-lookup"><span data-stu-id="2f02e-1667">NetX Secure Identifier</span></span>                            | <span data-ttu-id="2f02e-1668">Posizione del bit</span><span class="sxs-lookup"><span data-stu-id="2f02e-1668">Bit position</span></span> | <span data-ttu-id="2f02e-1669">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2f02e-1669">Description</span></span>                                                                                                                                                  |
| ----------------------------------------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="2f02e-1670">NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE</span><span class="sxs-lookup"><span data-stu-id="2f02e-1670">NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE</span></span>  | <span data-ttu-id="2f02e-1671">0</span><span class="sxs-lookup"><span data-stu-id="2f02e-1671">0</span></span>            | <span data-ttu-id="2f02e-1672">Il certificato può essere usato per le firme digitali</span><span class="sxs-lookup"><span data-stu-id="2f02e-1672">Certificate can be used for digital signatures</span></span>                                                                                                               |
| <span data-ttu-id="2f02e-1673">NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION</span><span class="sxs-lookup"><span data-stu-id="2f02e-1673">NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION</span></span>    | <span data-ttu-id="2f02e-1674">1</span><span class="sxs-lookup"><span data-stu-id="2f02e-1674">1</span></span>            | <span data-ttu-id="2f02e-1675">Il certificato può essere usato per verificare le firme digitali diverse da quelle per i certificati e i CRL</span><span class="sxs-lookup"><span data-stu-id="2f02e-1675">Certificate can be used to verify digital signatures other than those for certificates and CRLs</span></span>                                                              |
| <span data-ttu-id="2f02e-1676">NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT</span><span class="sxs-lookup"><span data-stu-id="2f02e-1676">NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT</span></span>   | <span data-ttu-id="2f02e-1677">2</span><span class="sxs-lookup"><span data-stu-id="2f02e-1677">2</span></span>            | <span data-ttu-id="2f02e-1678">Il certificato può essere usato per crittografare le chiavi simmetriche (trasporto chiavi)</span><span class="sxs-lookup"><span data-stu-id="2f02e-1678">Certificate can be used to encrypt symmetric keys (key transport)</span></span>                                                                                            |
| <span data-ttu-id="2f02e-1679">NX_SECURE_X509_KEY_USAGE_DATA_ENCIPHERMENT</span><span class="sxs-lookup"><span data-stu-id="2f02e-1679">NX_SECURE_X509_KEY_USAGE_DATA_ENCIPHERMENT</span></span>  | <span data-ttu-id="2f02e-1680">3</span><span class="sxs-lookup"><span data-stu-id="2f02e-1680">3</span></span>            | <span data-ttu-id="2f02e-1681">Il certificato può essere usato per crittografare direttamente i dati utente non elaborati (non comune)</span><span class="sxs-lookup"><span data-stu-id="2f02e-1681">Certificate can be used to directly encrypt raw user data (uncommon)</span></span>                                                                                         |
| <span data-ttu-id="2f02e-1682">NX_SECURE_X509_KEY_USAGE_KEY_AGREEMENT</span><span class="sxs-lookup"><span data-stu-id="2f02e-1682">NX_SECURE_X509_KEY_USAGE_KEY_AGREEMENT</span></span>      | <span data-ttu-id="2f02e-1683">4</span><span class="sxs-lookup"><span data-stu-id="2f02e-1683">4</span></span>            | <span data-ttu-id="2f02e-1684">Il certificato può essere usato per il contratto chiave (come con Diffie-Hellman)</span><span class="sxs-lookup"><span data-stu-id="2f02e-1684">Certificate can be used for key agreement (as with Diffie-Hellman)</span></span>                                                                                           |
| <span data-ttu-id="2f02e-1685">NX_SECURE_X509_KEY_USAGE_KEY_CERT_SIGN</span><span class="sxs-lookup"><span data-stu-id="2f02e-1685">NX_SECURE_X509_KEY_USAGE_KEY_CERT_SIGN</span></span>     | <span data-ttu-id="2f02e-1686">5</span><span class="sxs-lookup"><span data-stu-id="2f02e-1686">5</span></span>            | <span data-ttu-id="2f02e-1687">Il certificato può essere usato per firmare e verificare altri certificati (il certificato è un certificato CA o ICA).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1687">Certificate can be used to sign and verify other certificates (the certificate is a CA or ICA certificate).</span></span>                                                  |
| <span data-ttu-id="2f02e-1688">NX_SECURE_X509_KEY_USAGE_CRL_SIGN</span><span class="sxs-lookup"><span data-stu-id="2f02e-1688">NX_SECURE_X509_KEY_USAGE_CRL_SIGN</span></span>           | <span data-ttu-id="2f02e-1689">6</span><span class="sxs-lookup"><span data-stu-id="2f02e-1689">6</span></span>            | <span data-ttu-id="2f02e-1690">Chiave pubblica del certificato usata per verificare le firme nei CRL</span><span class="sxs-lookup"><span data-stu-id="2f02e-1690">Certificate public key is used to verify signatures on CRLs</span></span>                                                                                                  |
| <span data-ttu-id="2f02e-1691">NX_SECURE_X509_KEY_USAGE_ENCIPHER_ONLY</span><span class="sxs-lookup"><span data-stu-id="2f02e-1691">NX_SECURE_X509_KEY_USAGE_ENCIPHER_ONLY</span></span>      | <span data-ttu-id="2f02e-1692">7</span><span class="sxs-lookup"><span data-stu-id="2f02e-1692">7</span></span>            | <span data-ttu-id="2f02e-1693">Utilizzato con il bit del contratto chiave (bit 4): quando è impostato, la chiave del certificato può essere utilizzata solo per la crittografia durante il contratto di chiave.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1693">Used with Key Agreement bit (bit 4) – when set, certificate key can only be used to encrypt during key agreement.</span></span> <span data-ttu-id="2f02e-1694">Non definito se il bit del contratto chiave non è impostato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1694">Undefined if Key Agreement bit is not set.</span></span> |
| <span data-ttu-id="2f02e-1695">NX_SECURE_X509_KEY_USAGE_DECIPHER_ONLY</span><span class="sxs-lookup"><span data-stu-id="2f02e-1695">NX_SECURE_X509_KEY_USAGE_DECIPHER_ONLY</span></span>      | <span data-ttu-id="2f02e-1696">8</span><span class="sxs-lookup"><span data-stu-id="2f02e-1696">8</span></span>            | <span data-ttu-id="2f02e-1697">Utilizzato con il bit del contratto chiave (bit 4): quando è impostato, la chiave del certificato può essere utilizzata solo per la decrittografia durante il contratto di chiave.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1697">Used with Key Agreement bit (bit 4) – when set, certificate key can only be used to decrypt during key agreement.</span></span> <span data-ttu-id="2f02e-1698">Non definito se il bit del contratto chiave non è impostato.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1698">Undefined if Key Agreement bit is not set.</span></span> |

<span data-ttu-id="2f02e-1699">Maschere di maschera e valori per l'estensione utilizzo chiavi X. 509</span><span class="sxs-lookup"><span data-stu-id="2f02e-1699">Bitmasks and values for X.509 Key Usage Extension</span></span>

### <a name="parameters"></a><span data-ttu-id="2f02e-1700">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f02e-1700">Parameters</span></span>

- <span data-ttu-id="2f02e-1701">**certificato** di Puntatore al certificato da verificare.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1701">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="2f02e-1702">**bit** Restituisce l'intero bit dall'estensione.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1702">**bitfield** Return the entire bitfield from the extension.</span></span>

### <a name="return-values"></a><span data-ttu-id="2f02e-1703">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="2f02e-1703">Return Values</span></span>

- <span data-ttu-id="2f02e-1704">È stata rilevata l'estensione utilizzo chiavi **NX_SUCCESS** (0x00) e bit restituito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1704">**NX_SUCCESS** (0x00) Key usage extension found and bitfield returned.</span></span>
- <span data-ttu-id="2f02e-1705">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) è stato rilevato un tag a più byte ASN. 1 (certificato non supportato).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1705">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="2f02e-1706">È stato rilevato il campo ASN. 1 **NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) invaild (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1706">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="2f02e-1707">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) classe di tag ASN. 1 non valida rilevata (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="2f02e-1707">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="2f02e-1708">È stata rilevata un'estensione di **NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0X192) non valida. certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1708">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered (invalid certificate).</span></span>
- <span data-ttu-id="2f02e-1709">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) Impossibile trovare l'estensione utilizzo chiavi nel certificato fornito.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1709">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B)The Key Usage extension was not found in the provided certificate.</span></span>
- <span data-ttu-id="2f02e-1710">**NX_PTR_ERROR** (0x07) certificato non valido o puntatore bit.</span><span class="sxs-lookup"><span data-stu-id="2f02e-1710">**NX_PTR_ERROR** (0x07) Invalid certificate or bitfield pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="2f02e-1711">Consentito da</span><span class="sxs-lookup"><span data-stu-id="2f02e-1711">Allowed From</span></span>

<span data-ttu-id="2f02e-1712">Thread</span><span class="sxs-lookup"><span data-stu-id="2f02e-1712">Threads</span></span>

### <a name="example"></a><span data-ttu-id="2f02e-1713">Esempio</span><span class="sxs-lookup"><span data-stu-id="2f02e-1713">Example</span></span>

```C
ULONG certificate_verification_callback(NX_SECURE_TLS_SESSION *session,
  NX_SECURE_X509_CERT* certificate)
{
UINT status;
USHORT key_usage_bitfield;

    /* Key usage – extract key usage bitfield. */
    status = nx_secure_x509_key_usage_extension_parse(certificate, &key_usage_bitfield);

   /* Check certificate for a few specific key usage bits. */
   if((key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE) == 0 ||
      (key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION)   == 0 ||
      (key_usage_bitfield & NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT)  == 0)
    {
        printf("Expected key usage bitfield bits not set!\n");
        return(NX_SECURE_X509_KEY_USAGE_ERROR);
    }

    /* The specified bits were set, return success! */
    return(NX_SUCCESS);
}
```

### <a name="see-also"></a><span data-ttu-id="2f02e-1714">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f02e-1714">See Also</span></span>

- <span data-ttu-id="2f02e-1715">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="2f02e-1715">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="2f02e-1716">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="2f02e-1716">nx_secure_x509_extended_key_usage_extension_parse</span></span>
- <span data-ttu-id="2f02e-1717">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-1717">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="2f02e-1718">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="2f02e-1718">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="2f02e-1719">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="2f02e-1719">nx_secure_x509_extension_find</span></span>
