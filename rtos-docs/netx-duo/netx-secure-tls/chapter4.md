---
title: Capitolo 4 - Descrizione dei Azure RTOS NetX Secure
description: Questo capitolo contiene una descrizione di tutti i servizi NetX Secure (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 80ec22058ab64ed0c6258bb3d9364ec44f9a741b
ms.sourcegitcommit: 4ebe7c51ba850951c6a9d0f15e22d07bb752bc28
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2021
ms.locfileid: "110223393"
---
# <a name="chapter-4---description-of-azure-rtos-netx-secure-services"></a><span data-ttu-id="c7c64-103">Capitolo 4 - Descrizione dei Azure RTOS NetX Secure</span><span class="sxs-lookup"><span data-stu-id="c7c64-103">Chapter 4 - Description of Azure RTOS NetX Secure services</span></span>

<span data-ttu-id="c7c64-104">Questo capitolo contiene una descrizione di tutti i Azure RTOS NetX Secure (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="c7c64-104">This chapter contains a description of all Azure RTOS NetX Secure services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="c7c64-105">Nella sezione "Valori restituiti" nelle descrizioni api seguenti, i valori in **GRASSETTO** non sono interessati dalla macro **NX_SECURE_DISABLE_ERROR_CHECKING** usata per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_SECURE_DISABLE_ERROR_CHECKING** macro that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- [<span data-ttu-id="c7c64-106">nx_secure_crypto_table_self_test</span><span class="sxs-lookup"><span data-stu-id="c7c64-106">nx_secure_crypto_table_self_test</span></span>](#nx_secure_crypto_table_self_test)
  - <span data-ttu-id="c7c64-107">Eseguire self_test sui metodi di crittografia</span><span class="sxs-lookup"><span data-stu-id="c7c64-107">Perform self_test on the crypto methods</span></span>
- [<span data-ttu-id="c7c64-108">nx_secure_module_hash_compute</span><span class="sxs-lookup"><span data-stu-id="c7c64-108">nx_secure_module_hash_compute</span></span>](#nx_secure_module_hash_compute)
  - <span data-ttu-id="c7c64-109">Calcola il valore hash usando user_supplied funzione hash</span><span class="sxs-lookup"><span data-stu-id="c7c64-109">Computes hash value using user_supplied hash function</span></span>
- [<span data-ttu-id="c7c64-110">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-110">nx_secure_tls_active_certificate_set</span></span>](#nx_secure_tls_active_certificate_set)
  - <span data-ttu-id="c7c64-111">Impostare il certificato di identità attivo per una sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-111">Set the active identity certificate for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-112">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-112">nx_secure_tls_client_psk_set</span></span>](#nx_secure_tls_client_psk_set)
  - <span data-ttu-id="c7c64-113">Impostare una chiave Pre_Shared per una sessione del client TLS sicuro NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-113">Set a Pre_Shared Key for a NetX Secure TLS Client Session</span></span>
- [<span data-ttu-id="c7c64-114">nx_secure_tls_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-114">nx_secure_tls_initialize</span></span>](#nx_secure_tls_initialize)
  - <span data-ttu-id="c7c64-115">Inizializza il modulo NETX Secure TLS]</span><span class="sxs-lookup"><span data-stu-id="c7c64-115">Initializes the NetX Secure TLS module]</span></span>
- [<span data-ttu-id="c7c64-116">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-116">nx_secure_tls_local_certificate_add</span></span>](#nx_secure_tls_local_certificate_add)
  - <span data-ttu-id="c7c64-117">Aggiungere un certificato locale alla sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-117">Add a local certificate to NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-118">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-118">nx_secure_tls_local_certificate_find</span></span>](#nx_secure_tls_local_certificate_find)
  - <span data-ttu-id="c7c64-119">Trovare un certificato locale in una sessione TLS sicura netx in base al nome comune</span><span class="sxs-lookup"><span data-stu-id="c7c64-119">Find a local certificate in a NetX Secure TLS Session by Common Name</span></span>
- [<span data-ttu-id="c7c64-120">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-120">nx_secure_tls_local_certificate_remove</span></span>](#nx_secure_tls_local_certificate_remove)
  - <span data-ttu-id="c7c64-121">Rimuovere il certificato locale dalla sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-121">Remove local certificate from NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-122">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="c7c64-122">nx_secure_tls_metadata_size_calculate</span></span>](#nx_secure_tls_metadata_size_calculate)
  - <span data-ttu-id="c7c64-123">Calcolare le dimensioni dei metadati crittografici per una sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-123">Calculate size of cryptographic metadata for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-124">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-124">nx_secure_tls_packet_allocate</span></span>](#nx_secure_tls_packet_allocate)
  - <span data-ttu-id="c7c64-125">Allocare un pacchetto per una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-125">Allocate a packet for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-126">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-126">nx_secure_tls_psk_add</span></span>](#nx_secure_tls_psk_add)
  - <span data-ttu-id="c7c64-127">Aggiungere una Pre_Shared chiave a una sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-127">Add a Pre_Shared Key to a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-128">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-128">nx_secure_tls_remote_certificate_allocate</span></span>](#nx_secure_tls_remote_certificate_allocate)
  - <span data-ttu-id="c7c64-129">Allocare spazio per il certificato fornito da un host TLS remoto</span><span class="sxs-lookup"><span data-stu-id="c7c64-129">Allocate space for the certificate provided by a remote TLS host</span></span>
- [<span data-ttu-id="c7c64-130">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-130">nx_secure_tls_remote_certificate_buffer_allocate</span></span>](#nx_secure_tls_remote_certificate_buffer_allocate)
  - <span data-ttu-id="c7c64-131">Allocare spazio per tutti i certificati forniti da un host TLS remoto</span><span class="sxs-lookup"><span data-stu-id="c7c64-131">Allocate space for all certificates provided by a remote TLS host</span></span>
- [<span data-ttu-id="c7c64-132">nx_secure_tls_remote_certificate_free_all</span><span class="sxs-lookup"><span data-stu-id="c7c64-132">nx_secure_tls_remote_certificate_free_all</span></span>](#nx_secure_tls_remote_certificate_free_all)
  - <span data-ttu-id="c7c64-133">Spazio disponibile allocato per i certificati in ingresso</span><span class="sxs-lookup"><span data-stu-id="c7c64-133">Free space allocated for incoming certificates</span></span>
- [<span data-ttu-id="c7c64-134">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-134">nx_secure_tls_server_certificate_add</span></span>](#nx_secure_tls_server_certificate_add)
  - <span data-ttu-id="c7c64-135">Aggiungere un certificato specifico per i server TLS usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="c7c64-135">Add a certificate specifically for TLS servers using a numeric identifier</span></span>
- [<span data-ttu-id="c7c64-136">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-136">nx_secure_tls_server_certificate_find</span></span>](#nx_secure_tls_server_certificate_find)
  - <span data-ttu-id="c7c64-137">Trovare un certificato usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="c7c64-137">Find a certificate using a numeric identifier</span></span>
- [<span data-ttu-id="c7c64-138">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-138">nx_secure_tls_server_certificate_remove</span></span>](#nx_secure_tls_server_certificate_remove)
  - <span data-ttu-id="c7c64-139">Rimuovere un certificato del server locale usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="c7c64-139">Remove a local server certificate using a numeric identifier</span></span>
- [<span data-ttu-id="c7c64-140">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-140">nx_secure_tls_session_certificate_callback_set</span></span>](#nx_secure_tls_session_certificate_callback_set)
  - <span data-ttu-id="c7c64-141">Configurare un callback per TLS da usare per la convalida aggiuntiva del certificato</span><span class="sxs-lookup"><span data-stu-id="c7c64-141">Set up a callback for TLS to use for additional certificate validation</span></span>
- [<span data-ttu-id="c7c64-142">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-142">nx_secure_tls_session_client_callback_set</span></span>](#nx_secure_tls_session_client_callback_set)
  - <span data-ttu-id="c7c64-143">Configurare un callback per TLS da richiamare all'inizio di un handshake client TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-143">Set up a callback for TLS to invoke at the beginning of a TLS Client handshake</span></span>
- [<span data-ttu-id="c7c64-144">nx_secure_tls_session_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="c7c64-144">nx_secure_tls_session_x509_client_verify_configure</span></span>](#nx_secure_tls_session_x509_client_verify_configure)
  - <span data-ttu-id="c7c64-145">Abilitare la verifica X.509 del client e allocare spazio per i certificati client</span><span class="sxs-lookup"><span data-stu-id="c7c64-145">Enable client X.509 verification and allocate space for client certificates</span></span>
- [<span data-ttu-id="c7c64-146">nx_secure_tls_session_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="c7c64-146">nx_secure_tls_session_client_verify_disable</span></span>](#nx_secure_tls_session_client_verify_disable)
  - <span data-ttu-id="c7c64-147">Disabilitare l'autenticazione del certificato client per una sessione TLS sicura netx</span><span class="sxs-lookup"><span data-stu-id="c7c64-147">Disable Client Certificate Authentication for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-148">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="c7c64-148">nx_secure_tls_session_client_verify_enable</span></span>](#nx_secure_tls_session_client_verify_enable)
  - <span data-ttu-id="c7c64-149">Abilitare l'autenticazione del certificato client per una sessione TLS sicura netx</span><span class="sxs-lookup"><span data-stu-id="c7c64-149">Enable Client Certificate Authentication for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-150">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-150">nx_secure_tls_session_create</span></span>](#nx_secure_tls_session_create)
  - <span data-ttu-id="c7c64-151">Creare una sessione TLS sicura netx per le comunicazioni sicure</span><span class="sxs-lookup"><span data-stu-id="c7c64-151">Create a NetX Secure TLS Session for secure communications</span></span>
- [<span data-ttu-id="c7c64-152">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-152">nx_secure_tls_session_delete</span></span>](#nx_secure_tls_session_delete)
  - <span data-ttu-id="c7c64-153">Eliminare una sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-153">Delete a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-154">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="c7c64-154">nx_secure_tls_session_end</span></span>](#nx_secure_tls_session_end)
  - <span data-ttu-id="c7c64-155">Terminare una sessione TLS sicura di NetX attiva</span><span class="sxs-lookup"><span data-stu-id="c7c64-155">End an active NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-156">nx_secure_tls_session_packet_buffer_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-156">nx_secure_tls_session_packet_buffer_set</span></span>](#nx_secure_tls_session_packet_buffer_set)
  - <span data-ttu-id="c7c64-157">Impostare il buffer di riassemblaggio dei pacchetti per una sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-157">Set the packet reassembly buffer for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-158">nx_secure_tls_session_protocol_version_override</span><span class="sxs-lookup"><span data-stu-id="c7c64-158">nx_secure_tls_session_protocol_version_override</span></span>](#nx_secure_tls_session_protocol_version_override)
  - <span data-ttu-id="c7c64-159">Eseguire l'override della versione predefinita del protocollo TLS per una sessione TLS sicura netx</span><span class="sxs-lookup"><span data-stu-id="c7c64-159">Override the default TLS protocol version for a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-160">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-160">nx_secure_tls_session_receive</span></span>](#nx_secure_tls_session_receive)
  - <span data-ttu-id="c7c64-161">Ricevere dati da una sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-161">Receive data from a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-162">nx_secure_tls_session_renegotiate_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-162">nx_secure_tls_session_renegotiate_callback_set</span></span>](#nx_secure_tls_session_renegotiate_callback_set)
  - <span data-ttu-id="c7c64-163">Assegnare un callback che verrà richiamato all'inizio di una rinegoziazione della sessione</span><span class="sxs-lookup"><span data-stu-id="c7c64-163">Assign a callback that will be invoked at the beginning of a session renegotiation</span></span>
- [<span data-ttu-id="c7c64-164">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="c7c64-164">nx_secure_tls_session_renegotiate</span></span>](#nx_secure_tls_session_renegotiate)
  - <span data-ttu-id="c7c64-165">Avviare un handshake di rinegoziazione della sessione con l'host remoto</span><span class="sxs-lookup"><span data-stu-id="c7c64-165">Initiate a session renegotiation handshake with the remote host</span></span>
- [<span data-ttu-id="c7c64-166">nx_secure_tls_session_reset</span><span class="sxs-lookup"><span data-stu-id="c7c64-166">nx_secure_tls_session_reset</span></span>](#nx_secure_tls_session_reset)
  - <span data-ttu-id="c7c64-167">Cancellare e reimpostare una sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-167">Clear out and reset a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-168">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-168">nx_secure_tls_session_send</span></span>](#nx_secure_tls_session_send)
  - <span data-ttu-id="c7c64-169">Inviare dati tramite una sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-169">Send data through a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-170">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-170">nx_secure_tls_session_server_callback_set</span></span>](#nx_secure_tls_session_server_callback_set)
  - <span data-ttu-id="c7c64-171">Configurare un callback per TLS da richiamare all'inizio di un handshake del server TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-171">Set up a callback for TLS to invoke at the beginning of a TLS Server handshake</span></span>
- [<span data-ttu-id="c7c64-172">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-172">nx_secure_tls_session_sni_extension_parse</span></span>](#nx_secure_tls_session_sni_extension_parse)
  - <span data-ttu-id="c7c64-173">Analizzare un'Indicazione nome server (SNI) ricevuta da un client TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-173">Parse a Server Name Indication (SNI) extension received from a TLS Client</span></span>
- [<span data-ttu-id="c7c64-174">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-174">nx_secure_tls_session_sni_extension_set</span></span>](#nx_secure_tls_session_sni_extension_set)
  - <span data-ttu-id="c7c64-175">Impostare un nome DNS Indicazione nome server (SNI) per l'invio a un server remoto</span><span class="sxs-lookup"><span data-stu-id="c7c64-175">Set a Server Name Indication (SNI) extension DNS name to send to a remote Server</span></span>
- [<span data-ttu-id="c7c64-176">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-176">nx_secure_tls_session_start</span></span>](#nx_secure_tls_session_start)
  - <span data-ttu-id="c7c64-177">Avviare una sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-177">Start a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-178">nx_secure_tls_session_time_function_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-178">nx_secure_tls_session_time_function_set</span></span>](#nx_secure_tls_session_time_function_set)
  - <span data-ttu-id="c7c64-179">Assegnare una funzione timestamp a una sessione TLS protetta netx</span><span class="sxs-lookup"><span data-stu-id="c7c64-179">Assign a timestamp function to a NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-180">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-180">nx_secure_tls_trusted_certificate_add</span></span>](#nx_secure_tls_trusted_certificate_add)
  - <span data-ttu-id="c7c64-181">Aggiungere un certificato attendibile alla sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-181">Add trusted certificate to NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-182">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-182">nx_secure_tls_trusted_certificate_remove</span></span>](#nx_secure_tls_trusted_certificate_remove)
  - <span data-ttu-id="c7c64-183">Rimuovere un certificato attendibile dalla sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-183">Remove trusted certificate from NetX Secure TLS Session</span></span>
- [<span data-ttu-id="c7c64-184">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-184">nx_secure_x509_certificate_initialize</span></span>](#nx_secure_x509_certificate_initialize)
  - <span data-ttu-id="c7c64-185">Inizializzare il certificato X.509 per NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-185">Initialize X.509 Certificate for NetX Secure TLS</span></span>
- [<span data-ttu-id="c7c64-186">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-186">nx_secure_x509_common_name_dns_check</span></span>](#nx_secure_x509_common_name_dns_check)
  - <span data-ttu-id="c7c64-187">Controllare il nome DNS rispetto al certificato X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-187">Check DNS name against X.509 Certificate</span></span>
- [<span data-ttu-id="c7c64-188">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-188">nx_secure_x509_crl_revocation_check</span></span>](#nx_secure_x509_crl_revocation_check)
  - <span data-ttu-id="c7c64-189">Controllare il certificato X.509 rispetto a un elenco di revoche di certificati (CRL)]</span><span class="sxs-lookup"><span data-stu-id="c7c64-189">Check X.509 Certificate against a supplied Certificate Revocation List (CRL)]</span></span>
- [<span data-ttu-id="c7c64-190">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-190">nx_secure_x509_dns_name_initialize</span></span>](#nx_secure_x509_dns_name_initialize)
  - <span data-ttu-id="c7c64-191">Inizializzare una struttura di nomi DNS X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-191">Initialize an X.509 DNS name structure</span></span>
- [<span data-ttu-id="c7c64-192">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-192">nx_secure_x509_extended_key_usage_extension_parse</span></span>](#nx_secure_x509_extended_key_usage_extension_parse)
  - <span data-ttu-id="c7c64-193">Trovare e analizzare un'estensione per l'utilizzo chiavi estesa X.509 in un certificato X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-193">Find and parse an X.509 extended key usage extension in an X.509 certificate</span></span>
- [<span data-ttu-id="c7c64-194">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-194">nx_secure_x509_extension_find</span></span>](#nx_secure_x509_extension_find)
  - <span data-ttu-id="c7c64-195">Trovare e restituire un'estensione X.509 in un certificato X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-195">Find and return an X.509 extension in an X.509 certificate</span></span>
- [<span data-ttu-id="c7c64-196">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-196">nx_secure_x509_key_usage_extension_parse</span></span>](#nx_secure_x509_key_usage_extension_parse)
  - <span data-ttu-id="c7c64-197">Trovare e analizzare un'estensione Utilizzo chiavi X.509 in un certificato X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-197">Find and parse an X.509 Key Usage extension in an X.509 certificate</span></span>

## <a name="nx_secure_crypto_table_self_test"></a><span data-ttu-id="c7c64-198">nx_secure_crypto_table_self_test</span><span class="sxs-lookup"><span data-stu-id="c7c64-198">nx_secure_crypto_table_self_test</span></span>

<span data-ttu-id="c7c64-199">Eseguire il test self-test sui metodi di crittografia</span><span class="sxs-lookup"><span data-stu-id="c7c64-199">Perform self-test on the crypto methods</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-200">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-200">Prototype</span></span>

```C
UINT nx_secure_crypto_table_self_test(
                                  const NX_SECURE_TLS_CRYPTO *crypto_table,
                                  VOID *metadata, UINT metadata_size);
```

### <a name="description"></a><span data-ttu-id="c7c64-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-201">Description</span></span>

<span data-ttu-id="c7c64-202">Questo servizio viene eseguito tramite i test self-test del metodo di crittografia per la convalida.</span><span class="sxs-lookup"><span data-stu-id="c7c64-202">This service runs through the crypto method self tests to validate.</span></span> <span data-ttu-id="c7c64-203">Il test self-service è disponibile solo se la libreria NetX Secure viene compilata con il simbolo NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK definito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-203">The self test is available only if NetX Secure library is built with the symbol NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK defined.</span></span>

<span data-ttu-id="c7c64-204">Per ogni metodo di crittografia supportato, il test self-service fornisce dati di input predefiniti e verifica che l'output corrisponda al valore previsto predefinito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-204">For each supported crypto method, the self test provides pre-defined input data, and verified the output matches the pre-defined expected value.</span></span>

<span data-ttu-id="c7c64-205">NetX Secure Crypto Self Test supporta gli algoritmi e le dimensioni delle chiavi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7c64-205">NetX Secure crypto self test supports the following algorithms and key sizes:</span></span>

- <span data-ttu-id="c7c64-206">DES: crittografia e decrittografia</span><span class="sxs-lookup"><span data-stu-id="c7c64-206">DES: encryption and decryption</span></span>
- <span data-ttu-id="c7c64-207">Triple DES (3DES): crittografia e decrittografia</span><span class="sxs-lookup"><span data-stu-id="c7c64-207">Triple DES (3DES): encryption and decryption</span></span>
- <span data-ttu-id="c7c64-208">AES: 128, 192, dimensioni della chiave a 256 bit, crittografia e decrittografia, in modalità CBC e modalità contatore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-208">AES: 128-, 192-, 256-bit key size, encryption and decryption, in CBC mode and counter mode.</span></span>
- <span data-ttu-id="c7c64-209">HMAC-MD5: autenticazione e calcolo hash</span><span class="sxs-lookup"><span data-stu-id="c7c64-209">HMAC-MD5: authentication and hash computation</span></span>
- <span data-ttu-id="c7c64-210">HMAC-SHA: SHA1-96, SHA1-160, SHA2-256, SHA2-384, SHA2- 512, autenticazione e calcolo hash</span><span class="sxs-lookup"><span data-stu-id="c7c64-210">HMAC-SHA: SHA1-96, SHA1-160, SHA2-256, SHA2-384, SHA2- 512, authentication and hash computation</span></span>
- <span data-ttu-id="c7c64-211">MD5: autenticazione</span><span class="sxs-lookup"><span data-stu-id="c7c64-211">MD5: authentication</span></span>
- <span data-ttu-id="c7c64-212">Funzione pseudo-casuale (PRF): PRF_HMAC_SHA1 e PRF_HMAC_SHA2-256</span><span class="sxs-lookup"><span data-stu-id="c7c64-212">Pseudo-random Function (PRF): PRF_HMAC_SHA1 and PRF_HMAC_SHA2-256</span></span>
- <span data-ttu-id="c7c64-213">RSA: operazione power-modulus RSA a 1024, 2048 e 4096 bit</span><span class="sxs-lookup"><span data-stu-id="c7c64-213">RSA: 1024-, 2048-, 4096-bit RSA power-modulus operation</span></span>
- <span data-ttu-id="c7c64-214">SHA: autenticazione SHA1 (96 e 160 bit), SHA2 (256 bit, 384 bit, 512 bit)</span><span class="sxs-lookup"><span data-stu-id="c7c64-214">SHA: SHA1 (96- and 160-bit), SHA2 (256bit, 384bit, 512bit) authentication</span></span>

<span data-ttu-id="c7c64-215">Questa funzione include i vettori predefiniti per gli algoritmi di crittografia elencati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-215">This function has the built-in vectors for the crypto algorithms listed above.</span></span> <span data-ttu-id="c7c64-216">Tuttavia, verifica solo quelli elencati nella *cipher_table* passati a questa funzione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-216">However it only tests the ones listed in the *cipher_table* passed into this function.</span></span> <span data-ttu-id="c7c64-217">Ad esempio, per una sessione TLS usa solo il TLS_RSA_WITH_AES_128_CBC_SHA ciphersuite, questa funzione eseguirà test self-service su RSA (1024, 2048, 4096 bit), AES-CBC (128 bit) e SHA1.</span><span class="sxs-lookup"><span data-stu-id="c7c64-217">For example, for a TLS session uses only the ciphersuite TLS_RSA_WITH_AES_128_CBC_SHA, this function will perform self test on the RSA (1024-, 2048-, 4096-bit), AES-CBC (128-bit) and SHA1.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-218">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-218">Parameters</span></span>

- <span data-ttu-id="c7c64-219">**crypto_table** Puntatore alla tabella di crittografia usata dalla sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-219">**crypto_table** Pointer to the crypto table being used by the TLS session.</span></span> <span data-ttu-id="c7c64-220">Si tratta dello stesso crypto_table passato alla **_chiamata nx_secure_tls_session_create()._**</span><span class="sxs-lookup"><span data-stu-id="c7c64-220">This is the same crypto_table being passed into the **_nx_secure_tls_session_create()_** call.</span></span>
- <span data-ttu-id="c7c64-221">**metadati** Puntatore allo spazio per l'area dei metadati di crittografia.</span><span class="sxs-lookup"><span data-stu-id="c7c64-221">**metadata** Pointer to space for cryptography metadata area.</span></span> <span data-ttu-id="c7c64-222">.</span><span class="sxs-lookup"><span data-stu-id="c7c64-222">.</span></span>
- <span data-ttu-id="c7c64-223">**metadata_size** Dimensioni del buffer dei metadati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-223">**metadata_size** Size of the metadata buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-224">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-224">Return Values</span></span>

- <span data-ttu-id="c7c64-225">**NX_SECURE_TLS_SUCCESS** (0x00) Sono stati testati correttamente i metodi di crittografia forniti.</span><span class="sxs-lookup"><span data-stu-id="c7c64-225">**NX_SECURE_TLS_SUCCESS** (0x00) Successfully tested the crypto methods provided.</span></span>
- <span data-ttu-id="c7c64-226">**NX_PTR_ERROR** (0x07) Struttura del metodo di crittografia non valida</span><span class="sxs-lookup"><span data-stu-id="c7c64-226">**NX_PTR_ERROR** (0x07) Invalid crypto method structure</span></span>
- <span data-ttu-id="c7c64-227">**NX_NOT_SUCCESSFUL** (0x43) il test self-test della crittografia ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="c7c64-227">**NX_NOT_SUCCESSFUL** (0x43) Crypto self test fails.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-228">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-228">Allowed From</span></span>

<span data-ttu-id="c7c64-229">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-229">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-230">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-230">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-231">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-231">See Also</span></span>

- <span data-ttu-id="c7c64-232">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-232">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_module_hash_compute"></a><span data-ttu-id="c7c64-233">nx_secure_module_hash_compute</span><span class="sxs-lookup"><span data-stu-id="c7c64-233">nx_secure_module_hash_compute</span></span>

<span data-ttu-id="c7c64-234">Calcola il valore hash usando la funzione hash fornita dall'utente</span><span class="sxs-lookup"><span data-stu-id="c7c64-234">Computes hash value using user-supplied hash function</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-235">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-235">Prototype</span></span>

```C
UINT nx_secure_module_hash_compute(
                      NX_CRYPTO_METHOD *hamc_ptr,
                      UINT start_address, UINT end_address,
                      UCHAR *key, UINT key_length,
                      VOID *metadata, UINT metadata_size,
                      UCHAR *output_buffer, UINT output_buffer_size,
                      UINT *actual_size);
```

### <a name="description"></a><span data-ttu-id="c7c64-236">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-236">Description</span></span>

<span data-ttu-id="c7c64-237">Questa funzione calcola il valore hash del flusso di dati nell'area di memoria specificata, usando il metodo di crittografia HMAC fornito e la stringa della chiave.</span><span class="sxs-lookup"><span data-stu-id="c7c64-237">This function computes the hash value of the data stream in the specified memory area, using supplied HMAC crypto method and the key string.</span></span> <span data-ttu-id="c7c64-238">La funzione di calcolo hash del modulo è disponibile solo se la libreria NetX Secure viene compilata con il simbolo seguente definito: NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK</span><span class="sxs-lookup"><span data-stu-id="c7c64-238">The module hash compute function is available only if NetX Secure library is built with the following symbol being defined: NX_SECURE_POWER_ON_SELF_TEST_MODULE_INTEGRITY_CHECK</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-239">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-239">Parameters</span></span>

- <span data-ttu-id="c7c64-240">**hmac_ptr** Puntatore al metodo di crittografia HMAC usato per il calcolo del valore hash.</span><span class="sxs-lookup"><span data-stu-id="c7c64-240">**hmac_ptr** Pointer to the HMAC crypto method being used for the hash value computation.</span></span>
- <span data-ttu-id="c7c64-241">**start_address** Indirizzo iniziale del buffer di dati</span><span class="sxs-lookup"><span data-stu-id="c7c64-241">**start_address** The starting address of the data buffer</span></span>
- <span data-ttu-id="c7c64-242">**end_address** Indirizzo finale del buffer di dati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-242">**end_address** The ending address of the data buffer.</span></span> <span data-ttu-id="c7c64-243">Si noti che il calcolo hash non copre i dati in questa end_address.</span><span class="sxs-lookup"><span data-stu-id="c7c64-243">Note that hash computation does not cover the data at this end_address.</span></span>
- <span data-ttu-id="c7c64-244">**chiave** Stringa chiave usata nel calcolo HMAC.</span><span class="sxs-lookup"><span data-stu-id="c7c64-244">**key** The key string being used in the HMAC computation.</span></span>
- <span data-ttu-id="c7c64-245">**key_length** Dimensioni della stringa di chiave, in byte</span><span class="sxs-lookup"><span data-stu-id="c7c64-245">**key_length** The size of the key string, in bytes</span></span>
- <span data-ttu-id="c7c64-246">**metadati** Puntatore allo spazio utilizzato dall'algoritmo HMAC.</span><span class="sxs-lookup"><span data-stu-id="c7c64-246">**metadata** Pointer to space used by the HMAC algorithm.</span></span>
- <span data-ttu-id="c7c64-247">**metadata_size** Dimensioni del buffer dei metadati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-247">**metadata_size** Size of the metadata buffer.</span></span>
- <span data-ttu-id="c7c64-248">**output_buffer** Posizione di memoria in cui viene archiviato l'output hash.</span><span class="sxs-lookup"><span data-stu-id="c7c64-248">**output_buffer** The memory location where the hash output is being stored at.</span></span>
- <span data-ttu-id="c7c64-249">**output_buffer_size** Spazio disponibile del buffer di output, in byte</span><span class="sxs-lookup"><span data-stu-id="c7c64-249">**output_buffer_size** The available space of the output buffer, in bytes</span></span>
- <span data-ttu-id="c7c64-250">**actual_size** Restituito dalla funzione che indica il numero effettivo di byte scritti nel output_buffer.</span><span class="sxs-lookup"><span data-stu-id="c7c64-250">**actual_size** Returned by the function indicating the actual number of bytes being written into the output_buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-251">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-251">Return Values</span></span>

- <span data-ttu-id="c7c64-252">**0 Il** valore hash è stato calcolato correttamente.</span><span class="sxs-lookup"><span data-stu-id="c7c64-252">**0** Successfully computed the hash value.</span></span>
- <span data-ttu-id="c7c64-253">**1 Il** calcolo dell'hash non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-253">**1** The hash computation failed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-254">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-254">Allowed From</span></span>

<span data-ttu-id="c7c64-255">inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-255">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-256">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-256">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-257">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-257">See Also</span></span>

- <span data-ttu-id="c7c64-258">nx_secure_crypto_method_self_test</span><span class="sxs-lookup"><span data-stu-id="c7c64-258">nx_secure_crypto_method_self_test</span></span>

## <a name="nx_secure_tls_active_certificate_set"></a><span data-ttu-id="c7c64-259">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-259">nx_secure_tls_active_certificate_set</span></span>

<span data-ttu-id="c7c64-260">Impostare il certificato di identità attivo per una sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-260">Set the active identity certificate for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-261">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-261">Prototype</span></span>

```C
UINT  nx_secure_tls_active_certificate_set(
                   NX_SECURE_TLS_SESSION *tls_session,
                   NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a><span data-ttu-id="c7c64-262">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-262">Description</span></span>

<span data-ttu-id="c7c64-263">Questo servizio deve essere chiamato dall'interno di un callback di sessione (vedere nx_secure_tls_session_client_callback_set e nx_secure_tls_session_server_callback_set).</span><span class="sxs-lookup"><span data-stu-id="c7c64-263">This service is intended to be called from within a session callback (see nx_secure_tls_session_client_callback_set and nx_secure_tls_session_server_callback_set).</span></span> <span data-ttu-id="c7c64-264">Quando viene chiamato con una struttura NX_SECURE_X509_CERT inizializzata in precedenza, tale certificato verrà usato al posto del certificato di identità predefinito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-264">When called with a previously-initialized NX_SECURE_X509_CERT structure, that certificate will be used instead of the default identity certificate.</span></span> <span data-ttu-id="c7c64-265">Nella maggior parte dei casi, il certificato deve essere stato aggiunto all'archivio locale (vedere nx_secure_tls_local_certificate_add) o l'handshake TLS potrebbe non riuscire.</span><span class="sxs-lookup"><span data-stu-id="c7c64-265">In most cases, the certificate must have been added to the local store (see nx_secure_tls_local_certificate_add) or the TLS handshake may fail.</span></span>

<span data-ttu-id="c7c64-266">Questo servizio è progettato per consentire a TLS di supportare più certificati di identità.</span><span class="sxs-lookup"><span data-stu-id="c7c64-266">This service is intended to allow TLS to support multiple identity certificates.</span></span> <span data-ttu-id="c7c64-267">Ciò è utile per un server TLS che fornisce più indirizzi di rete in modo che il server possa scegliere un certificato appropriato da fornire al client remoto a seconda del punto di ingresso del client.</span><span class="sxs-lookup"><span data-stu-id="c7c64-267">This is useful for a TLS server that services multiple network addresses so the server can pick an appropriate certificate to provide to the remote client depending on the client's entrypoint.</span></span> <span data-ttu-id="c7c64-268">Per un client TLS, questa routine può essere usata per modificare il certificato inviato a un server remoto in fase di esecuzione dopo che il server si è identificato nell'handshake TLS (questo caso è più raro del caso d'uso del server TLS).</span><span class="sxs-lookup"><span data-stu-id="c7c64-268">For a TLS client, this routine may be used to change the certificate sent to a remote server at runtime after the server has identified itself in the TLS handshake (this is more rare than the TLS server use-case).</span></span>

<span data-ttu-id="c7c64-269">Nel caso in cui più certificati possano condividere lo stesso nome distinto X.509, i certificati dovranno essere aggiunti usando nx_secure_tls_server_certificate_add, che introduce un identificatore numerico separato dal certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-269">In the case where multiple certificates may share the same X.509 distinguished name, certificates will need to be added using nx_secure_tls_server_certificate_add, which introduces a numeric identifier separate from the certificate.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-270">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-270">Parameters</span></span>

- <span data-ttu-id="c7c64-271">**session_ptr** Puntatore a un'istanza di sessione TLS passata nel callback di sessione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-271">**session_ptr** Pointer to a TLS Session instance passed into the session callback.</span></span>
- <span data-ttu-id="c7c64-272">**certificato** Puntatore a un certificato X.509 inizializzato che deve essere usato per la sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="c7c64-272">**certificate** Pointer to an initialized X.509 certificate that is to be used for the current session.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-273">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-273">Return Values</span></span>

- <span data-ttu-id="c7c64-274">**NX_SUCCESS** (0x00) Assegnazione del certificato alla sessione completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-274">**NX_SUCCESS** (0x00) Successful assignment of certificate to session.</span></span>
- <span data-ttu-id="c7c64-275">**NX_PTR_ERROR** (0x07) Puntatore di certificato o sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-275">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-276">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-276">Allowed From</span></span>

<span data-ttu-id="c7c64-277">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-277">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-278">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-278">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-279">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-279">See Also</span></span>

- <span data-ttu-id="c7c64-280">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-280">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-281">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-281">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="c7c64-282">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-282">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="c7c64-283">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-283">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="c7c64-284">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-284">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="c7c64-285">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-285">nx_secure_tls_server_certificate_find</span></span>
- <span data-ttu-id="c7c64-286">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-286">nx_secure_tls_server_certificate_remove</span></span>

## <a name="nx_secure_tls_client_psk_set"></a><span data-ttu-id="c7c64-287">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-287">nx_secure_tls_client_psk_set</span></span>

<span data-ttu-id="c7c64-288">Impostare una chiave precondi condivisa per una sessione del client TLS sicuro netx</span><span class="sxs-lookup"><span data-stu-id="c7c64-288">Set a Pre-Shared Key for a NetX Secure TLS Client Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-289">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-289">Prototype</span></span>

```C
UINT  nx_secure_tls_client_psk_set(NX_SECURE_TLS_SESSION *session_ptr,
                              UCHAR *pre_shared_key, UINT psk_length,
                              UCHAR *psk_identity, UINT identity_length,
                              UCHAR *hint, UINT hint_length);
```

### <a name="description"></a><span data-ttu-id="c7c64-290">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-290">Description</span></span>

<span data-ttu-id="c7c64-291">Questo servizio aggiunge una chiave precondi shared (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo della sessione TLS e imposta tale chiave PSK da usare nelle connessioni client TLS successive.</span><span class="sxs-lookup"><span data-stu-id="c7c64-291">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a TLS Session control block, and sets that PSK to be used in subsequent TLS Client connections.</span></span> <span data-ttu-id="c7c64-292">La chiave PSK viene usata al posto di un certificato digitale quando i ciphersuit PSK sono abilitati e usati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-292">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

<span data-ttu-id="c7c64-293">In questo caso, la chiave PSK è associata a un server TLS remoto specifico con cui il client TLS vuole comunicare.</span><span class="sxs-lookup"><span data-stu-id="c7c64-293">In this case, the PSK is associated with a specific remote TLS Server with which the TLS Client wishes to communicate.</span></span> <span data-ttu-id="c7c64-294">La chiave PSK impostata tramite questa API verrà fornita all'host remoto del server TLS durante il successivo handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-294">The PSK set through this API will be provided to the remote TLS Server host during the next TLS handshake.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-295">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-295">Parameters</span></span>

- <span data-ttu-id="c7c64-296">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-296">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-297">**pre_shared_key** Valore PSK effettivo.</span><span class="sxs-lookup"><span data-stu-id="c7c64-297">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="c7c64-298">**psk_length** Lunghezza del valore PSK.</span><span class="sxs-lookup"><span data-stu-id="c7c64-298">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="c7c64-299">**psk_identity** Stringa utilizzata per identificare questo valore PSK.</span><span class="sxs-lookup"><span data-stu-id="c7c64-299">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="c7c64-300">**identity_length** Lunghezza dell'identità PSK.</span><span class="sxs-lookup"><span data-stu-id="c7c64-300">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="c7c64-301">**hint** Stringa usata per indicare il gruppo di chiavi psk tra cui scegliere in un server TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-301">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="c7c64-302">**hint_length** Lunghezza della stringa dell'hint.</span><span class="sxs-lookup"><span data-stu-id="c7c64-302">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-303">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-303">Return Values</span></span>

- <span data-ttu-id="c7c64-304">**NX_SUCCESS** (0x00) Aggiunta corretta di PSK.</span><span class="sxs-lookup"><span data-stu-id="c7c64-304">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="c7c64-305">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-305">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="c7c64-306">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Impossibile aggiungere un'altra chiave PSK.</span><span class="sxs-lookup"><span data-stu-id="c7c64-306">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-307">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-307">Allowed From</span></span>

<span data-ttu-id="c7c64-308">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-308">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-309">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-309">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_client_psk_set(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-310">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-310">See Also</span></span>

- <span data-ttu-id="c7c64-311">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-311">nx_secure_tls_psk_add</span></span>
- <span data-ttu-id="c7c64-312">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-312">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-313">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-313">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-314">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-314">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-315">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-315">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_initialize"></a><span data-ttu-id="c7c64-316">nx_secure_tls_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-316">nx_secure_tls_initialize</span></span>

<span data-ttu-id="c7c64-317">Inizializza il modulo NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-317">Initializes the NetX Secure TLS module</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-318">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-318">Prototype</span></span>

```C
VOID nx_secure_tls_initialize(VOID);
```

### <a name="description"></a><span data-ttu-id="c7c64-319">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-319">Description</span></span>

<span data-ttu-id="c7c64-320">Questo servizio inizializza il modulo NetX Secure TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-320">This service initializes the NetX Secure TLS module.</span></span> <span data-ttu-id="c7c64-321">Deve essere chiamato prima che sia possibile accedere ad altri servizi NetX Secure.</span><span class="sxs-lookup"><span data-stu-id="c7c64-321">It must be called before other NetX Secure services can be accessed.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-322">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-322">Parameters</span></span>

<span data-ttu-id="c7c64-323">nessuno</span><span class="sxs-lookup"><span data-stu-id="c7c64-323">None</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-324">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-324">Return Values</span></span>

<span data-ttu-id="c7c64-325">nessuno</span><span class="sxs-lookup"><span data-stu-id="c7c64-325">None</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-326">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-326">Allowed From</span></span>

<span data-ttu-id="c7c64-327">inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-327">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-328">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-328">Example</span></span>

```C
/* Initializes the TLS module. */
Nx_secure_tls_initialize();
```

### <a name="see-also"></a><span data-ttu-id="c7c64-329">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-329">See Also</span></span>

- <span data-ttu-id="c7c64-330">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-330">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_local_certificate_add"></a><span data-ttu-id="c7c64-331">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-331">nx_secure_tls_local_certificate_add</span></span>

<span data-ttu-id="c7c64-332">Aggiungere un certificato locale alla sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-332">Add a local certificate to NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-333">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-333">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_add(
              NX_SECURE_TLS_SESSION *session_ptr,
              NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a><span data-ttu-id="c7c64-334">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-334">Description</span></span>

<span data-ttu-id="c7c64-335">Questo servizio aggiunge un'istanza inizializzata NX_SECURE_X509_CERT struttura all'archivio locale di una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-335">This service adds an initialized NX_SECURE_X509_CERT structure instance to the local store of a TLS session.</span></span> <span data-ttu-id="c7c64-336">Questo certificato può essere usato dallo stack TLS per identificare il dispositivo durante l'handshake TLS (se è stato contrassegnato come certificato di identità durante l'inizializzazione della struttura del certificato usando nx_secure_x509_certificate_initialize) o come autorità di certificazione come parte di una catena di certificati fornita all'host remoto durante l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-336">This certificate may used by the TLS stack to identify the device during the TLS handshake (if it was marked as an identity certificate during initialization of the certificate structure using nx_secure_x509_certificate_initialize), or as an issuer as part of a certificate chain provided to the remote host during the TLS handshake.</span></span>

<span data-ttu-id="c7c64-337">Se sono necessari più certificati locali con lo stesso nome comune, è possibile aggiungere certificati usando il *servizio nx_secure_tls_server_certificate_add* (vedere l'avviso seguente).</span><span class="sxs-lookup"><span data-stu-id="c7c64-337">If multiple local certificates with the same Common Name are needed, certificates may be added using the *nx_secure_tls_server_certificate_add* service (see warning below).</span></span>

<span data-ttu-id="c7c64-338">Per la **modalità** server TLS è necessario un certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-338">A certificate is **required** for TLS Server mode.</span></span>

<span data-ttu-id="c7c64-339">Un certificato è *facoltativo* per la modalità client TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-339">A certificate is *optional* for TLS Client mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7c64-340">*Questa API non deve essere usata con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API del certificato server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add indici basati sul nome comune X.509. I servizi certificati locali offrono un'alternativa pratica all'identificatore numerico per le applicazioni che usano un solo certificato di identità. Usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-340">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-341">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-341">Parameters</span></span>

- <span data-ttu-id="c7c64-342">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-342">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-343">**certificate_ptr** Puntatore a un'istanza del certificato TLS inizializzata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-343">**certificate_ptr** Pointer to an initialized TLS Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-344">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-344">Return Values</span></span>

- <span data-ttu-id="c7c64-345">**NX_SUCCESS** (0x00) Aggiunta del certificato completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-345">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="c7c64-346">**NX_INVALID_PARAMETERS** (0x4D) Si è tentato di aggiungere un certificato non valido o duplicato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-346">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid or duplicate certificate.</span></span>
- <span data-ttu-id="c7c64-347">**NX_PTR_ERROR** (0x07) Sessione TLS o puntatore al certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-347">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-348">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-348">Allowed From</span></span>

<span data-ttu-id="c7c64-349">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-349">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-350">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-350">Example</span></span>

```C
/* Initialize certificate structure. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, private_key, 64);

/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_add(&tls_session, &certificate);


/* If status is NX_SUCCESS the certificate was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-351">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-351">See Also</span></span>

- <span data-ttu-id="c7c64-352">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-352">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-353">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-353">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-354">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-354">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-355">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-355">nx_secure_tls_local_certificate_remove</span></span>
- <span data-ttu-id="c7c64-356">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-356">nx_secure_tls_local_certificate_find</span></span>

## <a name="nx_secure_tls_local_certificate_find"></a><span data-ttu-id="c7c64-357">nx_secure_tls_local_certificate_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-357">nx_secure_tls_local_certificate_find</span></span>

<span data-ttu-id="c7c64-358">Trovare un certificato locale in una sessione TLS sicura netx in base al nome comune</span><span class="sxs-lookup"><span data-stu-id="c7c64-358">Find a local certificate in a NetX Secure TLS Session by Common Name</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-359">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-359">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_find(NX_SECURE_TLS_SESSION
                        *session_ptr, NX_SECURE_X509_CERT
                        **certificate, UCHAR *common_name, UINT
                        name_length);
```

### <a name="description"></a><span data-ttu-id="c7c64-360">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-360">Description</span></span>

<span data-ttu-id="c7c64-361">Questo servizio trova un certificato nell'archivio certificati del dispositivo locale di una sessione TLS e restituisce un puntatore alla struttura NX_SECURE_X509_CERT nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="c7c64-361">This service finds a certificate in the local device certificate store of a TLS session and returns a pointer to the NX_SECURE_X509_CERT structure in the store.</span></span> <span data-ttu-id="c7c64-362">Il common_name e la sua lunghezza (name_length) vengono usati per identificare il certificato nell'archivio abbinando il campo Nome comune soggetto X.509 del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-362">The common_name parameter and it's length (name_length) are used to identify the certificate in the store by matching the certificate's X.509 Subject Common Name field.</span></span>

<span data-ttu-id="c7c64-363">Se sono presenti più certificati con lo stesso nome comune, verrà restituito solo il primo. Usare *invece* nx_secure_tls_server_certificate_find.</span><span class="sxs-lookup"><span data-stu-id="c7c64-363">If more than one certificate with the same Common Name is present, only the first one will be returned – use *nx_secure_tls_server_certificate_find* instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7c64-364">*Questa API non deve essere usata con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API del certificato server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add indici basati sul nome comune X.509. I servizi certificati locali offrono un'alternativa pratica all'identificatore numerico per le applicazioni che usano un solo certificato di identità. Usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-364">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-365">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-365">Parameters</span></span>

- <span data-ttu-id="c7c64-366">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-366">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-367">**certificato** Restituisce Puntatore al certificato corrispondente.</span><span class="sxs-lookup"><span data-stu-id="c7c64-367">**certificate** Return Pointer to matched certificate.</span></span>
- <span data-ttu-id="c7c64-368">**common_name** Stringa del nome comune di cui trovare la corrispondenza (nome DNS).</span><span class="sxs-lookup"><span data-stu-id="c7c64-368">**common_name** Common Name string to match (DNS name).</span></span>
- <span data-ttu-id="c7c64-369">**name_length** Lunghezza dei common_name stringa.</span><span class="sxs-lookup"><span data-stu-id="c7c64-369">**name_length** Length of common_name string data.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-370">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-370">Return Values</span></span>

- <span data-ttu-id="c7c64-371">**NX_SUCCESS** certificato (0x00) trovato e puntatore restituito nel parametro "certificate".</span><span class="sxs-lookup"><span data-stu-id="c7c64-371">**NX_SUCCESS** (0x00) Certificate was found and pointer returned in "certificate" parameter.</span></span>
- <span data-ttu-id="c7c64-372">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Non è stato trovato alcun certificato con il nome comune specificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-372">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) No certificate with the supplied Common Name was found.</span></span>
- <span data-ttu-id="c7c64-373">**NX_PTR_ERROR** (0x07) Sessione TLS, puntatore al certificato o stringa di nome comune non valida.</span><span class="sxs-lookup"><span data-stu-id="c7c64-373">**NX_PTR_ERROR** (0x07) Invalid TLS session, certificate pointer, or common name string.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-374">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-374">Allowed From</span></span>

<span data-ttu-id="c7c64-375">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-375">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-376">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-376">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-377">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-377">See Also</span></span>

- <span data-ttu-id="c7c64-378">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-378">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-379">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-379">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-380">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-380">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-381">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-381">nx_secure_tls_local_certificate_remove</span></span>
- <span data-ttu-id="c7c64-382">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-382">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_local_certificate_remove"></a><span data-ttu-id="c7c64-383">nx_secure_tls_local_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-383">nx_secure_tls_local_certificate_remove</span></span>

<span data-ttu-id="c7c64-384">Rimuovere il certificato locale dalla sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-384">Remove local certificate from NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-385">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-385">Prototype</span></span>

```C
UINT  nx_secure_tls_local_certificate_remove(NX_SECURE_TLS_SESSION
                  *session_ptr, UCHAR *common_name, UINT
                  common_name_length);
```

### <a name="description"></a><span data-ttu-id="c7c64-386">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-386">Description</span></span>

<span data-ttu-id="c7c64-387">Questo servizio rimuove un'istanza del certificato locale da una sessione TLS, con chiave nel campo Nome comune nel certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-387">This service removes a local certificate instance from a TLS session, keyed on the Common Name field in the certificate.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7c64-388">*Questa API non deve essere usata con la stessa sessione TLS quando si usa nx_secure_tls_server_certificate_add. L'API del certificato server usa un identificatore numerico univoco per ogni certificato e nx_secure_tls_local_certificate_add indici basati sul nome comune X.509. I servizi certificati locali offrono un'alternativa pratica all'identificatore numerico per le applicazioni che usano un solo certificato di identità. Usando il nome comune, l'applicazione non deve tenere traccia degli identificatori numerici.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-388">*This API should not be used with the same TLS session when using nx_secure_tls_server_certificate_add. The server certificate API uses a unique numeric identifier for each certificate, and nx_secure_tls_local_certificate_add indexes based on the X.509 Common Name. The local certificate services provide a convenient alternative to the numeric identifier for applications that use only a single identity certificate – by using the Common Name, the application need not keep track of numeric identifiers.*</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-389">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-389">Parameters</span></span>

- <span data-ttu-id="c7c64-390">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-390">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-391">**common_name** Valore nome comune del certificato da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="c7c64-391">**common_name** The Common Name value of the certificate to be removed.</span></span>
- <span data-ttu-id="c7c64-392">**common_name_length** Lunghezza della stringa del nome comune.</span><span class="sxs-lookup"><span data-stu-id="c7c64-392">**common_name_length** The length of the Common Name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-393">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-393">Return Values</span></span>

- <span data-ttu-id="c7c64-394">**NX_SUCCESS** (0x00) Aggiunta del certificato completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-394">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="c7c64-395">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-395">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="c7c64-396">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-396">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Certificate was not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-397">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-397">Allowed From</span></span>

<span data-ttu-id="c7c64-398">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-398">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-399">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-399">Example</span></span>

```C
/* Add certificate to TLS session.  */
status =  nx_secure_tls_local_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-400">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-400">See Also</span></span>

- <span data-ttu-id="c7c64-401">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-401">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-402">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-402">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-403">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-403">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-404">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-404">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_metadata_size_calculate"></a><span data-ttu-id="c7c64-405">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="c7c64-405">nx_secure_tls_metadata_size_calculate</span></span>

<span data-ttu-id="c7c64-406">Calcolare le dimensioni dei metadati crittografici per una sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-406">Calculate size of cryptographic metadata for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-407">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-407">Prototype</span></span>

```C
UINT  nx_secure_tls_metadata_size_calculate(
                        const NX_SECURE_TLS_CRYPTO *crypto_table,
                        ULONG *metadata_size);
```

### <a name="description"></a><span data-ttu-id="c7c64-408">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-408">Description</span></span>

<span data-ttu-id="c7c64-409">Questo servizio calcola e restituisce le dimensioni dei metadati crittografici necessari per una determinata sessione TLS e la tabella di crittografia TLS. Per altre informazioni sulla tabella di crittografia crittografica, vedere la sezione "Inizializzazione di TLS con metodi di crittografia".</span><span class="sxs-lookup"><span data-stu-id="c7c64-409">This service calculates and returns the size of the cryptographic metadata needed for a particular TLS session and TLS cryptography table (see the section "Initializing TLS with Cryptographic Methods" for more information on the cryptographic cipher table).</span></span>

<span data-ttu-id="c7c64-410">Questo servizio deve essere chiamato con la tabella crittografica desiderata per calcolare le dimensioni del buffer dei metadati passato in nx_secure_tls_session_create.</span><span class="sxs-lookup"><span data-stu-id="c7c64-410">This service should be called with the desired cryptographic table to calculate the size of the metadata buffer passed into nx_secure_tls_session_create.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-411">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-411">Parameters</span></span>

- <span data-ttu-id="c7c64-412">**crypto_table** Puntatore a una tabella di crittografia NETX Secure TLS completa.</span><span class="sxs-lookup"><span data-stu-id="c7c64-412">**crypto_table** Pointer to a complete NetX Secure TLS cryptography table.</span></span>
- <span data-ttu-id="c7c64-413">**metadata_size** Output del calcolo delle dimensioni in byte.</span><span class="sxs-lookup"><span data-stu-id="c7c64-413">**metadata_size** The output of the size calculation in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-414">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-414">Return Values</span></span>

- <span data-ttu-id="c7c64-415">**NX_SUCCESS** (0x00) Calcolo delle dimensioni dei metadati riuscito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-415">**NX_SUCCESS** (0x00) Successful calculation of metadata size.</span></span>
- <span data-ttu-id="c7c64-416">**NX_PTR_ERROR** (0x07) Tabella di crittografia o puntatore di dimensione restituito non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-416">**NX_PTR_ERROR** (0x07) Invalid crypto table or return size pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-417">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-417">Allowed From</span></span>

<span data-ttu-id="c7c64-418">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-418">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-419">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-419">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-420">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-420">See Also</span></span>

- <span data-ttu-id="c7c64-421">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-421">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_packet_allocate"></a><span data-ttu-id="c7c64-422">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-422">nx_secure_tls_packet_allocate</span></span>

<span data-ttu-id="c7c64-423">Allocare un pacchetto per una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-423">Allocate a packet for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-424">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-424">Prototype</span></span>

```C
UINT  nx_secure_tls_packet_allocate(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET_POOL *pool_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c7c64-425">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-425">Description</span></span>

<span data-ttu-id="c7c64-426">Questo servizio alloca un NX_PACKET per la sessione TLS attiva specificata dal NX_PACKET_POOL.</span><span class="sxs-lookup"><span data-stu-id="c7c64-426">This service allocates an NX_PACKET for the specified active TLS session from the specified NX_PACKET_POOL.</span></span> <span data-ttu-id="c7c64-427">Questo servizio deve essere chiamato dall'applicazione per allocare pacchetti di dati da inviare tramite una connessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-427">This service should be called by the application to allocate data packets to be sent over a TLS connection.</span></span> <span data-ttu-id="c7c64-428">La sessione TLS deve essere inizializzata prima di chiamare questo servizio.</span><span class="sxs-lookup"><span data-stu-id="c7c64-428">The TLS session must be initialized before calling this service.</span></span>

<span data-ttu-id="c7c64-429">Il pacchetto allocato viene inizializzato correttamente in modo che i dati di intestazione e piè di pagina TLS possano essere aggiunti dopo che i dati del pacchetto sono stati popolati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-429">The allocated packet is properly initialized so that TLS header and footer data may be added after the packet data is populated.</span></span> <span data-ttu-id="c7c64-430">In caso contrario, il comportamento è identico *nx_packet_allocate*.</span><span class="sxs-lookup"><span data-stu-id="c7c64-430">The behavior is otherwise identical to *nx_packet_allocate*.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-431">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-431">Parameters</span></span>

- <span data-ttu-id="c7c64-432">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-432">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-433">**pool_ptr** Puntatore a un NX_PACKET_POOL da cui allocare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-433">**pool_ptr** Pointer to an NX_PACKET_POOL from which to allocate the packet.</span></span>
- <span data-ttu-id="c7c64-434">**packet_ptr** Puntatore di output al pacchetto appena allocato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-434">**packet_ptr** Output pointer to the newly-allocated packet.</span></span>
- <span data-ttu-id="c7c64-435">**wait_option** Opzione di sospensione per l'allocazione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c7c64-435">**wait_option** Suspension option for packet allocation.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-436">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-436">Return Values</span></span>

- <span data-ttu-id="c7c64-437">**NX_SUCCESS** (0x00) L'allocazione dei pacchetti è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-437">**NX_SUCCESS** (0x00) Successful packet allocate.</span></span>
- <span data-ttu-id="c7c64-438">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) L'allocazione dei pacchetti sottostante non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-438">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Underlying packet allocation failed.</span></span>
- <span data-ttu-id="c7c64-439">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) La sessione TLS fornita non è stata inizializzata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-439">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-440">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-440">Allowed From</span></span>

<span data-ttu-id="c7c64-441">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-441">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-442">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-442">Example</span></span>

```C
/* Allocate a new TLS packet from the previously created packet pool and
previously initialized TLS session.   */

status = nx_secure_tls_packet_allocate(&tls_session, &pool_0, &packet_ptr,
                                       NX_WAIT_FOREVER);

/* If status is NX_SUCCESS, the newly allocated packet pointer is found in the
variable packet_ptr.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-443">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-443">See Also</span></span>

- <span data-ttu-id="c7c64-444">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-444">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="c7c64-445">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-445">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-446">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-446">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-447">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-447">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-448">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-448">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="c7c64-449">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-449">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="c7c64-450">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-450">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="c7c64-451">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="c7c64-451">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="c7c64-452">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-452">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_psk_add"></a><span data-ttu-id="c7c64-453">nx_secure_tls_psk_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-453">nx_secure_tls_psk_add</span></span>

<span data-ttu-id="c7c64-454">Aggiungere una chiave precondinessa a una sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-454">Add a Pre-Shared Key to a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-455">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-455">Prototype</span></span>

```C
UINT  nx_secure_tls_psk_add(NX_SECURE_TLS_SESSION *session_ptr,
                            UCHAR *pre_shared_key, UINT psk_length,
                            UCHAR *psk_identity, UINT
                            identity_length, UCHAR *hint, UINT
                            hint_length);
```

### <a name="description"></a><span data-ttu-id="c7c64-456">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-456">Description</span></span>

<span data-ttu-id="c7c64-457">Questo servizio aggiunge una chiave precondi condivisa (PSK), la relativa stringa di identità e un hint di identità a un blocco di controllo della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-457">This service adds a Pre-Shared Key (PSK), its identity string, and an identity hint to a TLS Session control block.</span></span> <span data-ttu-id="c7c64-458">La chiave PSK viene usata al posto di un certificato digitale quando i ciphersuit PSK sono abilitati e usati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-458">The PSK is used in place of a digital certificate when PSK ciphersuites are enabled and used.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-459">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-459">Parameters</span></span>

- <span data-ttu-id="c7c64-460">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-460">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-461">**pre_shared_key** Valore PSK effettivo.</span><span class="sxs-lookup"><span data-stu-id="c7c64-461">**pre_shared_key** The actual PSK value.</span></span>
- <span data-ttu-id="c7c64-462">**psk_length** Lunghezza del valore PSK.</span><span class="sxs-lookup"><span data-stu-id="c7c64-462">**psk_length** The length of the PSK value.</span></span>
- <span data-ttu-id="c7c64-463">**psk_identity** Stringa utilizzata per identificare questo valore PSK.</span><span class="sxs-lookup"><span data-stu-id="c7c64-463">**psk_identity** A string used to identify this PSK value.</span></span>
- <span data-ttu-id="c7c64-464">**identity_length** Lunghezza dell'identità PSK.</span><span class="sxs-lookup"><span data-stu-id="c7c64-464">**identity_length** The length of the PSK identity.</span></span>
- <span data-ttu-id="c7c64-465">**hint** Stringa usata per indicare il gruppo di chiavi psk tra cui scegliere in un server TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-465">**hint** A string used to indicate which group of PSKs to choose from on a TLS server.</span></span>
- <span data-ttu-id="c7c64-466">**hint_length** Lunghezza della stringa dell'hint.</span><span class="sxs-lookup"><span data-stu-id="c7c64-466">**hint_length** The length of the hint string.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-467">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-467">Return Values</span></span>

- <span data-ttu-id="c7c64-468">**NX_SUCCESS** (0x00) Aggiunta corretta di PSK.</span><span class="sxs-lookup"><span data-stu-id="c7c64-468">**NX_SUCCESS** (0x00) Successful addition of PSK.</span></span>
- <span data-ttu-id="c7c64-469">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-469">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="c7c64-470">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125) Impossibile aggiungere un'altra chiave PSK.</span><span class="sxs-lookup"><span data-stu-id="c7c64-470">**NX_SECURE_TLS_NO_MORE_PSK_SPACE** (0x125)  Cannot add another PSK.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-471">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-471">Allowed From</span></span>

<span data-ttu-id="c7c64-472">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-472">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-473">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-473">Example</span></span>

```C
/* PSK value.  */
UCHAR psk[] = { 0x1a, 0x2b, 0x3c, 0x4d };

/* Add PSK to TLS session.  */
status =  nx_secure_tls_psk_add(&tls_session, psk, sizeof(psk), “psk_1”, 4,
“Client_identity”, 15);


/* If status is NX_SUCCESS the PSK was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-474">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-474">See Also</span></span>

- <span data-ttu-id="c7c64-475">nx_secure_tls_client_psk_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-475">nx_secure_tls_client_psk_set</span></span>
- <span data-ttu-id="c7c64-476">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-476">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-477">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-477">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-478">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-478">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-479">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-479">nx_secure_tls_local_certificate_add</span></span>

## <a name="nx_secure_tls_remote_certificate_allocate"></a><span data-ttu-id="c7c64-480">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-480">nx_secure_tls_remote_certificate_allocate</span></span>

<span data-ttu-id="c7c64-481">Allocare spazio per il certificato fornito da un host TLS remoto</span><span class="sxs-lookup"><span data-stu-id="c7c64-481">Allocate space for the certificate provided by a remote TLS host</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-482">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-482">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_allocate(
                 NX_SECURE_TLS_SESSION *session_ptr,
                 NX_SECURE_X509_CERT *certificate_ptr,
                 UCHAR *raw_certificate_buffer,
                 UINT raw_buffer_size);
```

### <a name="description"></a><span data-ttu-id="c7c64-483">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-483">Description</span></span>

<span data-ttu-id="c7c64-484">Questo servizio aggiunge un'istanza della NX_SECURE_X509_CERT non inizializzata a una sessione TLS allo scopo di allocare spazio per i certificati forniti da un host remoto durante una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-484">This service adds an uninitialized NX_SECURE_X509_CERT structure instance to a TLS session for the purpose of allocating space for certificates provided by a remote host during a TLS session.</span></span> <span data-ttu-id="c7c64-485">I dati del certificato remoto vengono analizzati da NetX Secure TLS e tali informazioni vengono usate per popolare l'istanza della struttura di certificati fornita a questa funzione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-485">The remote certificate data is parsed by NetX Secure TLS and that information is used to populate the certificate structure instance provided to this function.</span></span> <span data-ttu-id="c7c64-486">I certificati aggiunti in questo modo vengono inseriti in un elenco collegato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-486">Certificates added in this manner are placed in a linked list.</span></span>

<span data-ttu-id="c7c64-487">Se si prevede che l'host remoto fornirà più certificati, questa funzione deve essere chiamata ripetutamente per allocare spazio per tutti i certificati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-487">If it is expected that the remote host will provide multiple certificates, this function should be called repeatedly to allocate space for all certificates.</span></span> <span data-ttu-id="c7c64-488">I certificati aggiuntivi vengono aggiunti alla fine dell'elenco di certificati collegati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-488">The additional certificates are added to the end of the certificate linked list.</span></span>

<span data-ttu-id="c7c64-489">Se non si alloca un certificato remoto, la modalità client TLS avrà esito negativo durante l'handshake TLS, a meno che non sia in uso una crittografia PSK (Pre-Shared Key).</span><span class="sxs-lookup"><span data-stu-id="c7c64-489">Failure to allocate a remote certificate will cause TLS Client mode to fail during the TLS handshake unless a Pre-Shared Key (PSK) ciphersuite is in use.</span></span>

<span data-ttu-id="c7c64-490">Il *raw_certificate_buffer* punta allo spazio allocato per archiviare il certificato remoto in ingresso.</span><span class="sxs-lookup"><span data-stu-id="c7c64-490">The *raw_certificate_buffer* parameter points to space allocated to store the incoming remote certificate.</span></span> <span data-ttu-id="c7c64-491">I certificati tipici con chiavi RSA a 2048 bit che usano SHA-256 per le firme sono nell'intervallo tra 1000 e 2000 byte.</span><span class="sxs-lookup"><span data-stu-id="c7c64-491">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="c7c64-492">Il buffer deve essere sufficientemente grande da contenere almeno tale dimensione, ma a seconda dei certificati host remoti può essere notevolmente più piccolo o più grande.</span><span class="sxs-lookup"><span data-stu-id="c7c64-492">The buffer should be large enough to at least hold that size, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="c7c64-493">Si noti che se il buffer è troppo piccolo per contenere il certificato in ingresso, l'handshake TLS terminerà con un errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-493">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

<span data-ttu-id="c7c64-494">Per la modalità server TLS, è necessaria un'allocazione remota del certificato solo se è abilitata l'autenticazione del certificato client.</span><span class="sxs-lookup"><span data-stu-id="c7c64-494">For TLS Server mode, a remote certificate allocation is needed only if client certificate authentication is enabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-495">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-495">Parameters</span></span>

- <span data-ttu-id="c7c64-496">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-496">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-497">**certificate_ptr** Puntatore a un'istanza del certificato X.509 non inizializzata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-497">**certificate_ptr** Pointer to an uninitialized X.509 Certificate instance.</span></span>
- <span data-ttu-id="c7c64-498">**raw_certificate_buffer** Puntatore a un buffer per contenere il certificato non analizzato ricevuto dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-498">**raw_certificate_buffer** Pointer to a buffer to hold the un-parsed certificate received from the remote host.</span></span>
- <span data-ttu-id="c7c64-499">**raw_buffer_size** Dimensioni del buffer del certificato non elaborato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-499">**raw_buffer_size** Size of the raw certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-500">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-500">Return Values</span></span>

- <span data-ttu-id="c7c64-501">**NX_SUCCESS** (0x00) Corretta allocazione del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-501">**NX_SUCCESS** (0x00) Successful allocation of certificate.</span></span>
- <span data-ttu-id="c7c64-502">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-502">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="c7c64-503">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) Il buffer fornito era troppo piccolo.</span><span class="sxs-lookup"><span data-stu-id="c7c64-503">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="c7c64-504">**NX_INVALID_PARAMETERS** (0x4D) Si è tentato di aggiungere un certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-504">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid certificate.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-505">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-505">Allowed From</span></span>

<span data-ttu-id="c7c64-506">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-506">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-507">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-507">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-508">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-508">See Also</span></span>

- <span data-ttu-id="c7c64-509">nx_secure_x509_certificate_initialize,</span><span class="sxs-lookup"><span data-stu-id="c7c64-509">nx_secure_x509_certificate_initialize,</span></span>
- <span data-ttu-id="c7c64-510">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-510">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_remote_certificate_buffer_allocate"></a><span data-ttu-id="c7c64-511">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-511">nx_secure_tls_remote_certificate_buffer_allocate</span></span>

<span data-ttu-id="c7c64-512">Allocare spazio per tutti i certificati forniti da un host TLS remoto</span><span class="sxs-lookup"><span data-stu-id="c7c64-512">Allocate space for all certificates provided by a remote TLS host</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-513">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-513">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_buffer_allocate(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="c7c64-514">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-514">Description</span></span>

<span data-ttu-id="c7c64-515">Questo servizio alloca spazio per elaborare le catene di certificati in ingresso da host server remoti per eseguire l'autenticazione e la verifica X.509 in un'istanza del client TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-515">This service allocates space to process incoming certificate chains from remote server hosts in order to perform X.509 authentication and verification in a TLS Client instance.</span></span> <span data-ttu-id="c7c64-516">Per la modalità server TLS, l'allocazione remota dei certificati è necessaria solo se  è abilitata l'autenticazione del certificato X.509 client. Per le istanze del server TLS è invece necessario usare il nx_secure_tls_session_x509_client_verify_configure servizio.</span><span class="sxs-lookup"><span data-stu-id="c7c64-516">For TLS Server mode, remote certificate allocation is needed only if client X.509 certificate authentication is enabled – for TLS Server instances the service *nx_secure_tls_session_x509_client_verify_configure* should be used instead.</span></span>

<span data-ttu-id="c7c64-517">Se non si allocano certificati remoti, la modalità client TLS avrà esito negativo durante l'handshake TLS, a meno che non sia in uso una crittografia PSK (Pre-Shared Key).</span><span class="sxs-lookup"><span data-stu-id="c7c64-517">Failure to allocate remote certificates will cause TLS Client mode to fail during the TLS handshake unless a Pre-Shared Key (PSK) ciphersuite is in use.</span></span>

<span data-ttu-id="c7c64-518">Il *certificate_buffer* punta allo spazio allocato per archiviare i certificati remoti in ingresso e i blocchi di controllo necessari per tali certificati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-518">The *certificate_buffer* parameter points to space allocated to store the incoming remote certificates and the control blocks needed for those certificates.</span></span> <span data-ttu-id="c7c64-519">Il buffer verrà diviso per il numero di certificati (*certs_number*) con una parte uguale a ogni certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-519">The buffer will be divided by the number of certificates (*certs_number*) with an equal portion given to each certificate.</span></span> <span data-ttu-id="c7c64-520">Il *buffer_size*  parametro indica le dimensioni del buffer.</span><span class="sxs-lookup"><span data-stu-id="c7c64-520">The *buffer_size*  parameter indicates the size of the buffer.</span></span> <span data-ttu-id="c7c64-521">Lo spazio necessario è disponibile con la formula seguente:</span><span class="sxs-lookup"><span data-stu-id="c7c64-521">The space needed can be found with the following formula:</span></span>

```C
buffer_size = (<expected max number of certificates in chain>) *
                 (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

<span data-ttu-id="c7c64-522">I certificati tipici con chiavi RSA a 2048 bit che usano SHA-256 per le firme sono nell'intervallo di 1000-2000 byte.</span><span class="sxs-lookup"><span data-stu-id="c7c64-522">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="c7c64-523">Il buffer deve essere sufficientemente grande da contenere almeno tale dimensione per ogni certificato, ma a seconda dei certificati host remoti può essere notevolmente più piccolo o più grande.</span><span class="sxs-lookup"><span data-stu-id="c7c64-523">The buffer should be large enough to at least hold that size for each certificate, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="c7c64-524">Si noti che se il buffer è troppo piccolo per contenere il certificato in ingresso, l'handshake TLS terminerà con un errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-524">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-525">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-525">Parameters</span></span>

- <span data-ttu-id="c7c64-526">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-526">**session_ptr** Pointer to a previously created TLS Session  instance.</span></span>
- <span data-ttu-id="c7c64-527">**certs_number** Numero di certificati da allocare dal buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-527">**certs_number** Number of certificates to allocate from the  provided buffer.</span></span>
- <span data-ttu-id="c7c64-528">**certificate_buffer** Puntatore a un buffer per contenere i certificati ricevuti da un host remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-528">**certificate_buffer** Pointer to a buffer to hold certificates received  from a remote host.</span></span>
- <span data-ttu-id="c7c64-529">**buffer_size** Dimensioni del buffer del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-529">**buffer_size** Size of the certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-530">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-530">Return Values</span></span>

- <span data-ttu-id="c7c64-531">**NX_SUCCESS** (0x00) Corretta allocazione del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-531">**NX_SUCCESS** (0x00) Successful allocation of certificate.</span></span>
- <span data-ttu-id="c7c64-532">**NX_PTR_ERROR** (0x07) Sessione TLS o puntatore al buffer non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-532">**NX_PTR_ERROR** (0x07) Invalid TLS session or buffer pointer.</span></span>
- <span data-ttu-id="c7c64-533">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) Il buffer fornito era troppo piccolo.</span><span class="sxs-lookup"><span data-stu-id="c7c64-533">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="c7c64-534">**NX_INVALID_PARAMETERS** (0x4D) Il buffer era troppo piccolo per contenere il numero desiderato di certificati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-534">**NX_INVALID_PARAMETERS** (0x4D) The buffer was too small to hold  the desired number of certificates.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-535">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-535">Allowed From</span></span>

<span data-ttu-id="c7c64-536">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-536">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-537">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-537">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-538">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-538">See Also</span></span>

- <span data-ttu-id="c7c64-539">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-539">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-540">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-540">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_remote_certificate_free_all"></a><span data-ttu-id="c7c64-541">nx_secure_tls_remote_certificate_free_all</span><span class="sxs-lookup"><span data-stu-id="c7c64-541">nx_secure_tls_remote_certificate_free_all</span></span>

<span data-ttu-id="c7c64-542">Spazio disponibile allocato per i certificati in ingresso</span><span class="sxs-lookup"><span data-stu-id="c7c64-542">Free space allocated for incoming certificates</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-543">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-543">Prototype</span></span>

```C
UINT  nx_secure_tls_remote_certificate_free_all(
                  NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="c7c64-544">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-544">Description</span></span>

<span data-ttu-id="c7c64-545">Questo servizio viene usato per liberare tutti i buffer del certificato allocati a una sessione TLS specifica nx_secure_tls_remote_certificate_allocated tramite la restituzione nello spazio del certificato disponibile della sessione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-545">This service is used to free all of the certificate buffers allocated to a particular TLS Session by nx_secure_tls_remote_certificate_allocated by returning them to that session's free certificate space.</span></span> <span data-ttu-id="c7c64-546">Questa operazione può essere necessaria se un'applicazione riutilizza un oggetto sessione TLS senza eliminarlo e ricrearlo con nx_secure_tls_session_delete e nx_secure_tls_session_create.</span><span class="sxs-lookup"><span data-stu-id="c7c64-546">This may be necessary if an application reuses a TLS session object without deleting it and recreating it with nx_secure_tls_session_delete and nx_secure_tls_session_create.</span></span>

<span data-ttu-id="c7c64-547">Si noti che lo spazio del certificato remoto viene recuperato automaticamente quando la sessione TLS viene reimpostata come accade nx_secure_tls_session_end quindi la maggior parte delle applicazioni non deve chiamare questo servizio.</span><span class="sxs-lookup"><span data-stu-id="c7c64-547">Note that the remote certificate space is recovered automatically when the TLS session is reset as happens in nx_secure_tls_session_end so most applications should not need to call this service.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-548">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-548">Parameters</span></span>

- <span data-ttu-id="c7c64-549">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-549">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-550">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-550">Return Values</span></span>

- <span data-ttu-id="c7c64-551">**NX_SUCCESS** (0x00) Operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-551">**NX_SUCCESS** (0x00) Successful operation.</span></span>
- <span data-ttu-id="c7c64-552">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-552">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="c7c64-553">**NX_INVALID_PARAMETERS** (0x4D) Errore interno: è probabile che l'archivio certificati sia danneggiato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-553">**NX_INVALID_PARAMETERS** (0x4D) Internal error – certificate store likely corrupt.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-554">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-554">Allowed From</span></span>

<span data-ttu-id="c7c64-555">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-555">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-556">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-556">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-557">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-557">See Also</span></span>

- <span data-ttu-id="c7c64-558">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-558">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-559">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-559">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-560">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-560">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-561">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="c7c64-561">nx_secure_tls_session_end</span></span>

## <a name="nx_secure_tls_server_certificate_add"></a><span data-ttu-id="c7c64-562">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-562">nx_secure_tls_server_certificate_add</span></span>

<span data-ttu-id="c7c64-563">Aggiungere un certificato specifico per i server TLS usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="c7c64-563">Add a certificate specifically for TLS servers using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-564">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-564">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_add(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT *certificate, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="c7c64-565">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-565">Description</span></span>

<span data-ttu-id="c7c64-566">Questo servizio viene usato per aggiungere un certificato all'archivio locale di una sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico anziché indicizzare l'archivio usando il soggetto X.509 (nome comune) all'interno del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-566">This service is used to add a certificate to a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span> <span data-ttu-id="c7c64-567">L'identificatore numerico è separato dal certificato e consente di aggiungere più certificati come certificati di identità a un server TLS, oltre a consentire l'aggiunta di più certificati con lo stesso nome comune allo stesso archivio locale della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-567">The numeric identifier is separate from the certificate and allows multiple certificates to be added as identity certificates to a TLS server, as well as allowing multiple certificates with the same Common Name to be added to the same TLS session local store.</span></span> <span data-ttu-id="c7c64-568">Questo stesso servizio può essere usato per i certificati client, ma è raro che un client TLS abbia più certificati di identità.</span><span class="sxs-lookup"><span data-stu-id="c7c64-568">This same service can be used for client certificates, but it is rare for a TLS client to have multiple identity certificates.</span></span>

<span data-ttu-id="c7c64-569">Il cert_id parametro è un numero intero positivo diverso da zero assegnato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-569">The cert_id parameter is a non-zero positive integer assigned by the application.</span></span> <span data-ttu-id="c7c64-570">Il valore effettivo non è importante (diverso da zero), ma deve essere univoco nell'archivio per la sessione TLS fornita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-570">The actual value does not matter (other than zero) but it must be unique in the store for the provided TLS session.</span></span> <span data-ttu-id="c7c64-571">Il cert_id può essere usato per trovare e rimuovere certificati dall'archivio locale usando nx_secure_tls_server_certificate_find e nx_secure_tls_server_certificate_remove, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="c7c64-571">The cert_id value can be used to find and remove certificates from the local store using nx_secure_tls_server_certificate_find and nx_secure_tls_server_certificate_remove, respectively.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7c64-572">*Questa API non deve essere usata con la stessa sessione TLS quando si usa nx_secure_tls_local_certificate_add. L nx_secure_tls_server_certificate_add API usa un identificatore numerico univoco per ogni certificato e l'indice dei servizi certificati locali in base al nome comune X.509. I servizi certificati del server consentono l'esistenza di più certificati con dati condivisi (in particolare nome comune) nello stesso archivio locale. Ciò è utile per un server con più identità.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-572">*This API should not be used with the same TLS session when using nx_secure_tls_local_certificate_add. The nx_secure_tls_server_certificate_add API uses a unique numeric identifier for each certificate, and local certificate services index based on the X.509 Common Name. The server certificate services allow multiple certificates with shared data (especially Common Name) to exist in the same local store – this is useful for a server with multiple identities.*</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-573">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-573">Parameters</span></span>

- <span data-ttu-id="c7c64-574">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-574">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-575">**certificato** Puntatore a un'istanza del certificato X.509 inizializzata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-575">**certificate** Pointer to a previously initialized X.509 certificate instance.</span></span>
- <span data-ttu-id="c7c64-576">**cert_id** Numero DI ID certificato positivo, diverso da zero e relativamente univoco.</span><span class="sxs-lookup"><span data-stu-id="c7c64-576">**cert_id** Positive, non-zero, relatively unique certificate ID number.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-577">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-577">Return Values</span></span>

- <span data-ttu-id="c7c64-578">**NX_SUCCESS** (0x00)Operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-578">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="c7c64-579">**NX_PTR_ERROR** (0x07) Sessione TLS o puntatore di certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-579">**NX_PTR_ERROR** (0x07) Invalid TLS session orcertificate pointer.</span></span>
- <span data-ttu-id="c7c64-580">**NX_SECURE_TLS_CERT_ID_INVALID** (0x138) L'ID certificato specificato ha un valore non valido (probabilmente 0).</span><span class="sxs-lookup"><span data-stu-id="c7c64-580">**NX_SECURE_TLS_CERT_ID_INVALID** (0x138) The provided certificate ID had An invalid value (likely 0).</span></span>
- <span data-ttu-id="c7c64-581">**NX_SECURE_TLS_CERT_ID_DUPLICATE** (0x139) L'ID certificato specificato era già presente nell'archivio locale.</span><span class="sxs-lookup"><span data-stu-id="c7c64-581">**NX_SECURE_TLS_CERT_ID_DUPLICATE** (0x139) The provided certificate ID was already present in the local store.</span></span>
- <span data-ttu-id="c7c64-582">**NX_INVALID_PARAMETERS(0x4D)** Errore interno: è probabile che l'archivio certificati sia danneggiato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-582">**NX_INVALID_PARAMETERS(0x4D)** Internal error – certificate store likely corrupt.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-583">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-583">Allowed From</span></span>

<span data-ttu-id="c7c64-584">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-584">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-585">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-585">Example</span></span>

```C
/* Certificate control block. */
NX_SECURE_X509_CERT certificate;


/* Add certificate to TLS session.  */
status =  nx_secure_tls_server_certificate_add(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully added with the ID
0x12.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-586">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-586">See Also</span></span>

- <span data-ttu-id="c7c64-587">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-587">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-588">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-588">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="c7c64-589">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-589">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="c7c64-590">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-590">nx_secure_tls_server_certificate_find</span></span>
- <span data-ttu-id="c7c64-591">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-591">nx_secure_tls_server_certificate_remove</span></span>

## <a name="nx_secure_tls_server_certificate_find"></a><span data-ttu-id="c7c64-592">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-592">nx_secure_tls_server_certificate_find</span></span>

<span data-ttu-id="c7c64-593">Trovare un certificato usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="c7c64-593">Find a certificate using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-594">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-594">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_find(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  NX_SECURE_X509_CERT **certificate, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="c7c64-595">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-595">Description</span></span>

<span data-ttu-id="c7c64-596">Questo servizio viene usato per trovare un certificato nell'archivio locale di una sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico invece di indicizzare l'archivio usando il soggetto X.509 (nome comune) all'interno del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-596">This service is used to find a certificate in a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span>

<span data-ttu-id="c7c64-597">Il cert_id è un numero intero positivo diverso da zero assegnato dall'applicazione quando il certificato viene aggiunto all'archivio locale della sessione TLS usando nx_secure_tls_server_certificate_add.</span><span class="sxs-lookup"><span data-stu-id="c7c64-597">The cert_id parameter is a non-zero positive integer assigned by the application when the certificate is added to the TLS session local store using nx_secure_tls_server_certificate_add.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7c64-598">*Questa API non deve essere usata con la stessa sessione TLS quando si usa nx_secure_tls_local_certificate_add. L nx_secure_tls_server_certificate_add API usa un identificatore numerico univoco per ogni certificato e l'indice dei servizi certificati locali in base al nome comune X.509. I servizi certificati server consentono l'esistenza di più certificati con dati condivisi (in particolare nome comune) nello stesso archivio locale. Ciò è utile per un server con più identità.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-598">*This API should not be used with the same TLS session when using nx_secure_tls_local_certificate_add. The nx_secure_tls_server_certificate_add API uses a unique numeric identifier for each certificate, and local certificate services index based on the X.509 Common Name. The server certificate services allow multiple certificates with shared data (especially Common Name) to exist in the same local store – this is useful for a server with multiple identities.*</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-599">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-599">Parameters</span></span>

- <span data-ttu-id="c7c64-600">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-600">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-601">**certificato** Puntatore a un puntatore al certificato X.509 per restituire un riferimento al certificato trovato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-601">**certificate** Pointer to an X.509 certificate pointer to return a reference to the found certificate.</span></span>
- <span data-ttu-id="c7c64-602">**cert_id** Valore ID certificato positivo diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="c7c64-602">**cert_id** Non-zero positive certificate ID value.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-603">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-603">Return Values</span></span>

- <span data-ttu-id="c7c64-604">**NX_SUCCESS** (0x00)Operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-604">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="c7c64-605">**NX_PTR_ERROR** (0x07) Sessione TLS o puntatore al certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-605">**NX_PTR_ERROR** (0x07) Invalid TLS session or certificate pointer.</span></span>
- <span data-ttu-id="c7c64-606">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) L'ID certificato specificato non corrisponde ad alcun id nell'archivio locale della sessione TLS fornita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-606">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) The provided certificate ID did not match any in the local store of the provided TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-607">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-607">Allowed From</span></span>

<span data-ttu-id="c7c64-608">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-608">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-609">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-609">Example</span></span>

```C
NX_SECURE_X509_CERT *certificate;


/* Find certificate in TLS session.  */
status =  nx_secure_tls_server_certificate_find(&tls_session, &certificate, 0x12);


/* If status is NX_SUCCESS the certificate was successfully found and a reference
returned in the certificate parameter.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-610">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-610">See Also</span></span>

- <span data-ttu-id="c7c64-611">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-611">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-612">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-612">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="c7c64-613">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-613">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="c7c64-614">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-614">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="c7c64-615">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-615">nx_secure_tls_server_certificate_remove</span></span>

##  <a name="nx_secure_tls_server_certificate_remove"></a><span data-ttu-id="c7c64-616">nx_secure_tls_server_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-616">nx_secure_tls_server_certificate_remove</span></span>

<span data-ttu-id="c7c64-617">Rimuovere un certificato del server locale usando un identificatore numerico</span><span class="sxs-lookup"><span data-stu-id="c7c64-617">Remove a local server certificate using a numeric identifier</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-618">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-618">Prototype</span></span>

```C
UINT  nx_secure_tls_server_certificate_remove(
                  NX_SECURE_TLS_SESSION *session_ptr, UINT cert_id);
```

### <a name="description"></a><span data-ttu-id="c7c64-619">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-619">Description</span></span>

<span data-ttu-id="c7c64-620">Questo servizio viene usato per rimuovere un certificato dall'archivio locale di una sessione TLS (vedere nx_secure_tls_local_certificate_add) usando un identificatore numerico anziché indicizzare l'archivio usando il soggetto X.509 (nome comune) all'interno del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-620">This service is used to remove a certificate from a TLS session's local store (see nx_secure_tls_local_certificate_add) using a numeric identifier instead of indexing the store using the X.509 Subject (Common Name) within the certificate.</span></span>

<span data-ttu-id="c7c64-621">Il cert_id è un numero intero positivo diverso da zero assegnato dall'applicazione quando il certificato viene aggiunto all'archivio locale della sessione TLS usando nx_secure_tls_server_certificate_add.</span><span class="sxs-lookup"><span data-stu-id="c7c64-621">The cert_id parameter is a non-zero positive integer assigned by the application when the certificate is added to the TLS session local store using nx_secure_tls_server_certificate_add.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-622">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-622">Parameters</span></span>

- <span data-ttu-id="c7c64-623">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-623">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-624">**cert_id** Valore ID certificato positivo diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="c7c64-624">**cert_id** Non-zero positive certificate ID value.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-625">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-625">Return Values</span></span>

- <span data-ttu-id="c7c64-626">**NX_SUCCESS** (0x00)Operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-626">**NX_SUCCESS** (0x00)Successful operation.</span></span>
- <span data-ttu-id="c7c64-627">**NX_PTR_ERROR** (0x07) Sessione TLS non valida.</span><span class="sxs-lookup"><span data-stu-id="c7c64-627">**NX_PTR_ERROR** (0x07) Invalid TLS session.</span></span>
- <span data-ttu-id="c7c64-628">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) L'ID certificato specificato non corrisponde ad alcun id nell'archivio locale della sessione TLS fornita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-628">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) The provided certificate ID did not match any in the local store of the provided TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-629">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-629">Allowed From</span></span>

<span data-ttu-id="c7c64-630">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-630">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-631">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-631">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-632">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-632">See Also</span></span>

- <span data-ttu-id="c7c64-633">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-633">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-634">nx_secure_tls_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-634">nx_secure_tls_local_certificate_add</span></span>
- <span data-ttu-id="c7c64-635">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-635">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="c7c64-636">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-636">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="c7c64-637">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-637">nx_secure_tls_server_certificate_find</span></span>

## <a name="nx_secure_tls_session_alert_value_get"></a><span data-ttu-id="c7c64-638">nx_secure_tls_session_alert_value_get</span><span class="sxs-lookup"><span data-stu-id="c7c64-638">nx_secure_tls_session_alert_value_get</span></span>

<span data-ttu-id="c7c64-639">Ottenere il valore e il livello di avviso TLS inviati dall'host remoto</span><span class="sxs-lookup"><span data-stu-id="c7c64-639">Get the TLS alert value and level sent by the remote host</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-640">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-640">Prototype</span></span>

```C
UINT  nx_secure_tls_session_alert_value_get(
                   NX_SECURE_TLS_SESSION *session_ptr,
                   UINT *alert_level, UINT *alert_value);
```

### <a name="description"></a><span data-ttu-id="c7c64-641">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-641">Description</span></span>

<span data-ttu-id="c7c64-642">Questo servizio viene usato per recuperare il livello e il valore di avviso TLS quando l'host remoto invia un avviso in risposta a un problema o a un errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-642">This service is used to retrieve the TLS alert level and value when the remote host sends an alert in response to some problem or error.</span></span>

<span data-ttu-id="c7c64-643">I valori dei parametri alert_level e alert_value sono validi solo se questa funzione viene chiamata immediatamente dopo una chiamata API TLS che ha restituito lo stato NX_SECURE_TLS_ALERT_RECEIVED (0x114) che indica che è stato ricevuto un avviso dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-643">The values of the alert_level and alert_value parameters are only valid if this function is called immediately following a TLS API call that returned a status of NX_SECURE_TLS_ALERT_RECEIVED (0x114) indicating that an alert was received from the remote host.</span></span>

<span data-ttu-id="c7c64-644">Si noti che se l'host locale TLS invia un avviso, i codici di errore restituiti sono molto più descrittivi dell'errore effettivo rispetto all'avviso TLS stesso perché i valori di avviso TLS vengono intenzionalmente lasciati ambigui per impedire determinati tipi di attacco ,ad esempio un attacco "oracolo di riempimento" o simili.</span><span class="sxs-lookup"><span data-stu-id="c7c64-644">Note that if the local host TLS sends an alert, the returned error codes are far more descriptive of the actual error than the TLS alert itself because TLS alert values are intentionally left ambiguous to prevent certain types of attack (such as a "padding oracle" attack or similar).</span></span>

<span data-ttu-id="c7c64-645">Il livello di avviso accetta solo uno dei due valori seguenti: NX_SECURE_TLS_ALERT_LEVEL_WARNING (0x1) o NX_SECURE_TLS_ALERT_LEVEL_FATAL (0x2).</span><span class="sxs-lookup"><span data-stu-id="c7c64-645">The alert level only takes one of two values: NX_SECURE_TLS_ALERT_LEVEL_WARNING (0x1) or NX_SECURE_TLS_ALERT_LEVEL_FATAL (0x2).</span></span> <span data-ttu-id="c7c64-646">In generale, solo l'avviso CloseNotify (usato per indicare un esito positivo di una sessione TLS) riceverà un livello di "Avviso", anche se alcune situazioni di configurazione dell'estensione possono anche essere considerate avvisi.</span><span class="sxs-lookup"><span data-stu-id="c7c64-646">In general, only the CloseNotify Alert (used to indicate a successful end to a TLS session) will be given a level of "Warning" though some extension configuration situations may also be considered warnings.</span></span> <span data-ttu-id="c7c64-647">La maggior parte degli avvisi sarà "Fatal" che indica un potenziale errore di sicurezza e determina la chiusura immediata della connessione TLS (handshake o sessione).</span><span class="sxs-lookup"><span data-stu-id="c7c64-647">The vast majority of alerts will be "Fatal" indicating a potential security failure and resulting in immediate closure of the TLS connection (handshake or session).</span></span>

<span data-ttu-id="c7c64-648">I valori di avviso TLS sono definiti nelle RFC TLS, di seguito è riportato l'elenco di RFC 5246 (TLSv1.2) per riferimento:</span><span class="sxs-lookup"><span data-stu-id="c7c64-648">The TLS alert values are defined in the TLS RFCs, here is the list from RFC 5246 (TLSv1.2) for reference:</span></span>

| <span data-ttu-id="c7c64-649">Nome avviso</span><span class="sxs-lookup"><span data-stu-id="c7c64-649">Alert Name</span></span>                     | <span data-ttu-id="c7c64-650">Valore</span><span class="sxs-lookup"><span data-stu-id="c7c64-650">Value</span></span> | <span data-ttu-id="c7c64-651">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-651">Description</span></span>                                                                                                                                                  |
| ---------------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="c7c64-652">close_notify</span><span class="sxs-lookup"><span data-stu-id="c7c64-652">close_notify</span></span>                  | <span data-ttu-id="c7c64-653">0</span><span class="sxs-lookup"><span data-stu-id="c7c64-653">0</span></span>     | <span data-ttu-id="c7c64-654">Nessun errore, indica l'esito positivo della sessione</span><span class="sxs-lookup"><span data-stu-id="c7c64-654">No error, indicates successful session end</span></span>                                                                                                                   |
| <span data-ttu-id="c7c64-655">unexpected_message</span><span class="sxs-lookup"><span data-stu-id="c7c64-655">unexpected_message</span></span>            | <span data-ttu-id="c7c64-656">10</span><span class="sxs-lookup"><span data-stu-id="c7c64-656">10</span></span>    | <span data-ttu-id="c7c64-657">TLS ha ricevuto un messaggio imprevisto o non in ordine</span><span class="sxs-lookup"><span data-stu-id="c7c64-657">TLS received an unexpected or out-of-order message</span></span>                                                                                                           |
| <span data-ttu-id="c7c64-658">bad_record_mac</span><span class="sxs-lookup"><span data-stu-id="c7c64-658">bad_record_mac</span></span>               | <span data-ttu-id="c7c64-659">20</span><span class="sxs-lookup"><span data-stu-id="c7c64-659">20</span></span>    | <span data-ttu-id="c7c64-660">Decrittografia e/o verifica MAC non riuscita</span><span class="sxs-lookup"><span data-stu-id="c7c64-660">Decryption and/or MAC verification failed</span></span>                                                                                                                    |
| <span data-ttu-id="c7c64-661">decryption_failed_RESERVED</span><span class="sxs-lookup"><span data-stu-id="c7c64-661">decryption_failed_RESERVED</span></span>   | <span data-ttu-id="c7c64-662">21</span><span class="sxs-lookup"><span data-stu-id="c7c64-662">21</span></span>    | <span data-ttu-id="c7c64-663">**DEPRECATO** Decrittografia non riuscita (deprecata a causa di attacchi di oracolo di riempimento)</span><span class="sxs-lookup"><span data-stu-id="c7c64-663">**DEPRECATED** Decryption failed (deprecated due to padding oracle attacks)</span></span>                                                                                      |
| <span data-ttu-id="c7c64-664">record_overflow</span><span class="sxs-lookup"><span data-stu-id="c7c64-664">record_overflow</span></span>               | <span data-ttu-id="c7c64-665">22</span><span class="sxs-lookup"><span data-stu-id="c7c64-665">22</span></span>    | <span data-ttu-id="c7c64-666">È stato ricevuto un record maggiore delle dimensioni massime del record TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-666">A record was received that is larger than the TLS maximum record size</span></span>                                                                                        |
| <span data-ttu-id="c7c64-667">decompression_failure</span><span class="sxs-lookup"><span data-stu-id="c7c64-667">decompression_failure</span></span>         | <span data-ttu-id="c7c64-668">30</span><span class="sxs-lookup"><span data-stu-id="c7c64-668">30</span></span>    | <span data-ttu-id="c7c64-669">Si è verificato un problema durante la compressione/decompressione di un record TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-669">A problem was encountered in compression/decompression of a TLS record</span></span>                                                                                       |
| <span data-ttu-id="c7c64-670">handshake_failure</span><span class="sxs-lookup"><span data-stu-id="c7c64-670">handshake_failure</span></span>             | <span data-ttu-id="c7c64-671">40</span><span class="sxs-lookup"><span data-stu-id="c7c64-671">40</span></span>    | <span data-ttu-id="c7c64-672">Si è verificato un errore di handshake non specificato che non è coperto da un avviso diverso</span><span class="sxs-lookup"><span data-stu-id="c7c64-672">Some unspecified handshake error occurred that isn't covered by a different alert</span></span>                                                                            |
| <span data-ttu-id="c7c64-673">no_certificate_RESERVED</span><span class="sxs-lookup"><span data-stu-id="c7c64-673">no_certificate_RESERVED</span></span>      | <span data-ttu-id="c7c64-674">41</span><span class="sxs-lookup"><span data-stu-id="c7c64-674">41</span></span>    | <span data-ttu-id="c7c64-675">**DEPRECATO** in TLS (solo SSL)</span><span class="sxs-lookup"><span data-stu-id="c7c64-675">**DEPRECATED** in TLS (SSL only)</span></span>                                                                                                                                 |
| <span data-ttu-id="c7c64-676">bad_certificate</span><span class="sxs-lookup"><span data-stu-id="c7c64-676">bad_certificate</span></span>               | <span data-ttu-id="c7c64-677">42</span><span class="sxs-lookup"><span data-stu-id="c7c64-677">42</span></span>    | <span data-ttu-id="c7c64-678">Un certificato ricevuto contiene firme o formattazioni non valide</span><span class="sxs-lookup"><span data-stu-id="c7c64-678">A certificate that was received contained invalid formatting or signatures</span></span>                                                                                   |
| <span data-ttu-id="c7c64-679">unsupported_certificate</span><span class="sxs-lookup"><span data-stu-id="c7c64-679">unsupported_certificate</span></span>       | <span data-ttu-id="c7c64-680">43</span><span class="sxs-lookup"><span data-stu-id="c7c64-680">43</span></span>    | <span data-ttu-id="c7c64-681">È stato ricevuto un certificato di tipo non valido, ad esempio un certificato di sola firma usato per l'autenticazione server TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-681">A certificate was received that was of an invalid type (e.g. signing-only certificate used for TLS server authentication)</span></span>                                    |
| <span data-ttu-id="c7c64-682">certificate_revoked</span><span class="sxs-lookup"><span data-stu-id="c7c64-682">certificate_revoked</span></span>           | <span data-ttu-id="c7c64-683">44</span><span class="sxs-lookup"><span data-stu-id="c7c64-683">44</span></span>    | <span data-ttu-id="c7c64-684">Lo stato del certificato (fornito da un CRL o OCSP) è stato indicato come "revocato"</span><span class="sxs-lookup"><span data-stu-id="c7c64-684">The certificate status (as provided by a CRL or OCSP) was indicated as being "revoked"</span></span>                                                                       |
| <span data-ttu-id="c7c64-685">certificate_expired</span><span class="sxs-lookup"><span data-stu-id="c7c64-685">certificate_expired</span></span>           | <span data-ttu-id="c7c64-686">45</span><span class="sxs-lookup"><span data-stu-id="c7c64-686">45</span></span>    | <span data-ttu-id="c7c64-687">Il certificato ricevuto non è compreso nell'intervallo di date valido (non ancora valido o scaduto)</span><span class="sxs-lookup"><span data-stu-id="c7c64-687">The received certificate was outside it's valid date range (either not valid yet or expired)</span></span>                                                                 |
| <span data-ttu-id="c7c64-688">certificate_unknown</span><span class="sxs-lookup"><span data-stu-id="c7c64-688">certificate_unknown</span></span>           | <span data-ttu-id="c7c64-689">46</span><span class="sxs-lookup"><span data-stu-id="c7c64-689">46</span></span>    | <span data-ttu-id="c7c64-690">È stato rilevato un problema di certificato sconosciuto non coperto da altri avvisi</span><span class="sxs-lookup"><span data-stu-id="c7c64-690">Some unknown certificate issue was encountered that was not covered by other alerts</span></span>                                                                          |
| <span data-ttu-id="c7c64-691">illegal_parameter</span><span class="sxs-lookup"><span data-stu-id="c7c64-691">illegal_parameter</span></span>             | <span data-ttu-id="c7c64-692">47</span><span class="sxs-lookup"><span data-stu-id="c7c64-692">47</span></span>    | <span data-ttu-id="c7c64-693">Una configurazione o un valore negoziato nell'handshake TLS non è valido o non è compreso nell'intervallo</span><span class="sxs-lookup"><span data-stu-id="c7c64-693">Some configuration or negotiated value in the TLS handshake was invalid or out of range</span></span>                                                                      |
| <span data-ttu-id="c7c64-694">unknown_ca</span><span class="sxs-lookup"><span data-stu-id="c7c64-694">unknown_ca</span></span>                    | <span data-ttu-id="c7c64-695">48</span><span class="sxs-lookup"><span data-stu-id="c7c64-695">48</span></span>    | <span data-ttu-id="c7c64-696">Non è stato possibile tracciare il certificato di identità ricevuto tramite una catena di certificati in un certificato ca radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="c7c64-696">The received identity certificate could not be traced via a certificate chain to a trusted root CA certificate.</span></span>                                              |
| <span data-ttu-id="c7c64-697">access_denied</span><span class="sxs-lookup"><span data-stu-id="c7c64-697">access_denied</span></span>                 | <span data-ttu-id="c7c64-698">49</span><span class="sxs-lookup"><span data-stu-id="c7c64-698">49</span></span>    | <span data-ttu-id="c7c64-699">Indica che è stato ricevuto un certificato valido, ma il controllo di accesso dell'applicazione ha indicato che il certificato non era valido per le risorse richieste.</span><span class="sxs-lookup"><span data-stu-id="c7c64-699">Indicates a valid certificate was received but application access control indicated that the certificate was invalid for the requested resources.</span></span>            |
| <span data-ttu-id="c7c64-700">decode_error</span><span class="sxs-lookup"><span data-stu-id="c7c64-700">decode_error</span></span>                  | <span data-ttu-id="c7c64-701">50</span><span class="sxs-lookup"><span data-stu-id="c7c64-701">50</span></span>    | <span data-ttu-id="c7c64-702">Un campo o un valore in un'intestazione TLS o un messaggio di handshake non è compreso nell'intervallo o non è valido, causando un errore nella decodifica di un record TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-702">Some field or value in a TLS header or handshake message was out of range or invalid, leading to a failure in decoding of a TLS record.</span></span>                      |
| <span data-ttu-id="c7c64-703">decrypt_error</span><span class="sxs-lookup"><span data-stu-id="c7c64-703">decrypt_error</span></span>                 | <span data-ttu-id="c7c64-704">51</span><span class="sxs-lookup"><span data-stu-id="c7c64-704">51</span></span>    | <span data-ttu-id="c7c64-705">Impossibile verificare la firma o l'hash del messaggio completato durante l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-705">A signature or Finished message hash during the TLS handshake could not be verified.</span></span>                                                                         |
| <span data-ttu-id="c7c64-706">export_restriction_RESERVED</span><span class="sxs-lookup"><span data-stu-id="c7c64-706">export_restriction_RESERVED</span></span>  | <span data-ttu-id="c7c64-707">60</span><span class="sxs-lookup"><span data-stu-id="c7c64-707">60</span></span>    | <span data-ttu-id="c7c64-708">DEPRECATO in TLSv1.2</span><span class="sxs-lookup"><span data-stu-id="c7c64-708">DEPRECATED in TLSv1.2</span></span>                                                                                                                                        |
| <span data-ttu-id="c7c64-709">protocol_version</span><span class="sxs-lookup"><span data-stu-id="c7c64-709">protocol_version</span></span>              | <span data-ttu-id="c7c64-710">70</span><span class="sxs-lookup"><span data-stu-id="c7c64-710">70</span></span>    | <span data-ttu-id="c7c64-711">La versione del protocollo TLS negoziata durante l'handshake è riconosciuta ma non supportata (ad esempio TLSv1.0 è stata presentata ma non abilitata).</span><span class="sxs-lookup"><span data-stu-id="c7c64-711">The TLS protocol version negotiated during the handshake is recognized but not supported (e.g. TLSv1.0 was presented but not enabled).</span></span>                       |
| <span data-ttu-id="c7c64-712">insufficient_security</span><span class="sxs-lookup"><span data-stu-id="c7c64-712">insufficient_security</span></span>         | <span data-ttu-id="c7c64-713">71</span><span class="sxs-lookup"><span data-stu-id="c7c64-713">71</span></span>    | <span data-ttu-id="c7c64-714">Inviato ogni volta che un handshake ha esito negativo a causa della mancanza di crittografia sicura (ad esempio, le dimensioni della chiave sono troppo piccole per i requisiti dell'applicazione)</span><span class="sxs-lookup"><span data-stu-id="c7c64-714">Sent whenever a handshake fails due to a lack of secure ciphers (e.g. key size is too small for the application requirements)</span></span>                                |
| <span data-ttu-id="c7c64-715">internal_error</span><span class="sxs-lookup"><span data-stu-id="c7c64-715">internal_error</span></span>                | <span data-ttu-id="c7c64-716">80</span><span class="sxs-lookup"><span data-stu-id="c7c64-716">80</span></span>    | <span data-ttu-id="c7c64-717">Si è verificato un errore non TLS (ad esempio problemi di allocazione della memoria, problemi dell'applicazione) che ha generato una sessione TLS interrotta.</span><span class="sxs-lookup"><span data-stu-id="c7c64-717">Some non-TLS error (e.g. memory allocation problems, application issues) occurred resulting in a broken TLS session.</span></span>                                         |
| <span data-ttu-id="c7c64-718">user_canceled</span><span class="sxs-lookup"><span data-stu-id="c7c64-718">user_canceled</span></span>                 | <span data-ttu-id="c7c64-719">90</span><span class="sxs-lookup"><span data-stu-id="c7c64-719">90</span></span>    | <span data-ttu-id="c7c64-720">Restituito se la sessione TLS viene annullata da un utente o un'applicazione prima del completamento dell'handshake (simile a CloseNotify).</span><span class="sxs-lookup"><span data-stu-id="c7c64-720">Returned if the TLS session is cancelled by a user or application before the handshake is complete (similar to CloseNotify).</span></span>                                 |
| <span data-ttu-id="c7c64-721">no_renegotiation</span><span class="sxs-lookup"><span data-stu-id="c7c64-721">no_renegotiation</span></span>              | <span data-ttu-id="c7c64-722">100</span><span class="sxs-lookup"><span data-stu-id="c7c64-722">100</span></span>   | <span data-ttu-id="c7c64-723">Indica che l'host remoto non è disposto a eseguire handshake di rinegoziazione TLS in risposta a una richiesta di rinegoziazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-723">Indiates that the remote host is not willing to perform TLS renegotiation handshakes in response to a renegotiation request.</span></span>                                 |
| <span data-ttu-id="c7c64-724">unsupported_extension</span><span class="sxs-lookup"><span data-stu-id="c7c64-724">unsupported_extension</span></span>         | <span data-ttu-id="c7c64-725">110</span><span class="sxs-lookup"><span data-stu-id="c7c64-725">110</span></span>   | <span data-ttu-id="c7c64-726">Inviato se un client TLS riceve un serverHello contenente estensioni non richieste in modo esplicito nel ClientHello iniziale (che indica che il server ha un problema).</span><span class="sxs-lookup"><span data-stu-id="c7c64-726">Sent if a TLS Client receives a ServerHello containing extensions not explicitly asked for in the initial ClientHello (indicating the server has a problem).</span></span> |

### <a name="parameters"></a><span data-ttu-id="c7c64-727">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-727">Parameters</span></span>

- <span data-ttu-id="c7c64-728">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-728">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-729">**alert_level** Restituisce il livello dell'avviso ricevuto (avviso o irreversibile).</span><span class="sxs-lookup"><span data-stu-id="c7c64-729">**alert_level** Return the level of the received alert (warning or fatal).</span></span>
- <span data-ttu-id="c7c64-730">**alert_value** Restituisce il valore dell'avviso ricevuto (vedere la tabella).</span><span class="sxs-lookup"><span data-stu-id="c7c64-730">**alert_value** Return the value of the received alert (see table).</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-731">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-731">Return Values</span></span>

- <span data-ttu-id="c7c64-732">**NX_SUCCESS** (0x00) Operazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-732">**NX_SUCCESS** (0x00) Successful operation.</span></span>
- <span data-ttu-id="c7c64-733">**NX_PTR_ERROR** (0x07) Sessione TLS non valida.</span><span class="sxs-lookup"><span data-stu-id="c7c64-733">**NX_PTR_ERROR** (0x07) Invalid TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-734">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-734">Allowed From</span></span>

<span data-ttu-id="c7c64-735">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-735">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-736">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-736">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-737">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-737">See Also</span></span>

- <span data-ttu-id="c7c64-738">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-738">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-739">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-739">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="c7c64-740">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-740">nx_secure_tls_session_receive</span></span>

## <a name="nx_secure_tls_session_certificate_callback_set"></a><span data-ttu-id="c7c64-741">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-741">nx_secure_tls_session_certificate_callback_set</span></span>

<span data-ttu-id="c7c64-742">Configurare un callback per TLS da usare per la convalida aggiuntiva del certificato</span><span class="sxs-lookup"><span data-stu-id="c7c64-742">Set up a callback for TLS to use for additional certificate validation</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-743">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-743">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_certificate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *session,
                                    NX_SECURE_X509_CERT *certificate));
```

### <a name="description"></a><span data-ttu-id="c7c64-744">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-744">Description</span></span>

<span data-ttu-id="c7c64-745">Questo servizio assegna un puntatore a funzione a una sessione TLS che TLS richiama quando viene ricevuto un certificato da un host remoto, consentendo all'applicazione di eseguire controlli di convalida, ad esempio la convalida DNS, la revoca del certificato e l'applicazione dei criteri dei certificati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-745">This service assigns a function pointer to a TLS session that TLS will invoke when a certificate is received from a remote host, allowing the application to perform validation checks such as DNS validation, certificate revocation, and certificate policy enforcement.</span></span>

<span data-ttu-id="c7c64-746">NetX Secure TLS eseguirà la convalida del percorso X.509 di base sul certificato prima di richiamare il callback per garantire che il certificato possa essere tracciato in un certificato nell'archivio certificati attendibili TLS, ma tutte le altre convalide verranno gestite da questo callback.</span><span class="sxs-lookup"><span data-stu-id="c7c64-746">NetX Secure TLS will perform basic X.509 path validation on the certificate before invoking the callback to assure that the certificate can be traced to a certificate in the TLS trusted certificate store, but all other validation will be handled by this callback.</span></span>

<span data-ttu-id="c7c64-747">Il callback fornisce il puntatore di sessione TLS e un puntatore al certificato di identità dell'host remoto (la foglia nella catena di certificati).</span><span class="sxs-lookup"><span data-stu-id="c7c64-747">The callback provides the TLS session pointer and a pointer to the remote host identity certificate (the leaf in the certificate chain).</span></span> <span data-ttu-id="c7c64-748">Il callback deve restituire NX_SUCCESS se la convalida ha esito positivo; in caso contrario, deve restituire un codice di errore che indica l'errore di convalida.</span><span class="sxs-lookup"><span data-stu-id="c7c64-748">The callback should return NX_SUCCESS if all validation is successful, otherwise it should return an error code indicating the validation failure.</span></span> <span data-ttu-id="c7c64-749">Qualsiasi valore diverso da NX_SUCCESS causerà l'interruzione immediata dell'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-749">Any value other than NX_SUCCESS will cause the TLS handshake to immediately abort.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-750">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-750">Parameters</span></span>

- <span data-ttu-id="c7c64-751">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-751">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-752">**func_ptr** Puntatore alla funzione di callback di convalida del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-752">**func_ptr** Pointer to the certificate validation callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-753">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-753">Return Values</span></span>

- <span data-ttu-id="c7c64-754">**NX_SUCCESS** (0x00) Corretta allocazione del puntatore a funzione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-754">**NX_SUCCESS** (0x00) Successful allocation of Function pointer.</span></span>
- <span data-ttu-id="c7c64-755">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-755">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-756">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-756">Allowed From</span></span>

<span data-ttu-id="c7c64-757">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-757">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-758">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-758">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-759">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-759">See Also</span></span>

- <span data-ttu-id="c7c64-760">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-760">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-761">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-761">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="c7c64-762">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-762">nx_secure_x509_crl_revocation_check</span></span>

## <a name="nx_secure_tls_session_client_callback_set"></a><span data-ttu-id="c7c64-763">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-763">nx_secure_tls_session_client_callback_set</span></span>

<span data-ttu-id="c7c64-764">Configurare un callback per TLS da richiamare all'inizio di un handshake client TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-764">Set up a callback for TLS to invoke at the beginning of a TLS Client handshake</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-765">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-765">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_client_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions, UINT num_extensions));
```

### <a name="description"></a><span data-ttu-id="c7c64-766">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-766">Description</span></span>

<span data-ttu-id="c7c64-767">Questo servizio assegna un puntatore a funzione a una sessione TLS che TLS richiama quando un handshake client TLS ha ricevuto un messaggio ServerHelloDone.</span><span class="sxs-lookup"><span data-stu-id="c7c64-767">This service assigns a function pointer to a TLS session that TLS will invoke when a TLS Client handshake has received a ServerHelloDone message.</span></span> <span data-ttu-id="c7c64-768">La funzione di callback consente a un'applicazione di elaborare tutte le estensioni TLS dal messaggio ServerHello ricevuto che richiedono input o decisioni.</span><span class="sxs-lookup"><span data-stu-id="c7c64-768">The callback function allows an application to process any TLS extensions from the received ServerHello message that require input or decision making.</span></span>

<span data-ttu-id="c7c64-769">Il callback viene eseguito con il blocco di controllo sessione TLS richiamato e una matrice di NX_SECURE_TLS_HELLO_EXTENSION oggetti .</span><span class="sxs-lookup"><span data-stu-id="c7c64-769">The callback is executed with the invoking TLS session control block and an array of NX_SECURE_TLS_HELLO_EXTENSION objects.</span></span> <span data-ttu-id="c7c64-770">La matrice di oggetti di estensione deve essere passata a una funzione helper che troverà e an parserà un'estensione specifica.</span><span class="sxs-lookup"><span data-stu-id="c7c64-770">The array of extension objects is intended to be passed into a helper function that will find and parse a specific extension.</span></span> <span data-ttu-id="c7c64-771">Attualmente non sono supportate estensioni specifiche in NetX Secure che richiedono l'input del client TLS, ma il callback è disponibile per i progettisti di applicazioni per gestire estensioni personalizzate o nuove che potrebbero diventare disponibili.</span><span class="sxs-lookup"><span data-stu-id="c7c64-771">Currently, there are no specific extensions supported in NetX Secure that require TLS Client input, but the callback is available for application designers to handle custom or new extensions that may become available.</span></span> <span data-ttu-id="c7c64-772">Per una funzione helper di esempio che analizza le estensioni TLS fornite nei messaggi hello, vedere *nx_secure_tls_session_sni_extension_parse*.</span><span class="sxs-lookup"><span data-stu-id="c7c64-772">For an example helper function that parses TLS extensions provided in hello messages, see *nx_secure_tls_session_sni_extension_parse*.</span></span>

<span data-ttu-id="c7c64-773">Il callback client può essere usato anche per selezionare il certificato di identità attivo usando *nx_secure_tls_active_certificate_set* per il client TLS nel caso in cui il server remoto abbia richiesto un certificato e fornito informazioni per consentire al client TLS di selezionare un certificato specifico.</span><span class="sxs-lookup"><span data-stu-id="c7c64-773">The client callback may also be used to select the active identity certificate using *nx_secure_tls_active_certificate_set* for the TLS Client in the event that the remote server has requested a certificate and provided information to allow the TLS Client to select a specific certificate.</span></span> <span data-ttu-id="c7c64-774">Per altre informazioni, vedere le informazioni nx_secure_tls_active_certificate_set riferimento.</span><span class="sxs-lookup"><span data-stu-id="c7c64-774">See the reference for nx_secure_tls_active_certificate_set for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-775">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-775">Parameters</span></span>

- <span data-ttu-id="c7c64-776">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-776">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-777">**func_ptr** Puntatore alla funzione di callback client TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-777">**func_ptr** Pointer to the TLS Client callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-778">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-778">Return Values</span></span>

- <span data-ttu-id="c7c64-779">**NX_SUCCESS** (0x00) Corretta allocazione del puntatore a funzione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-779">**NX_SUCCESS** (0x00) Successful allocation of function pointer.</span></span>
- <span data-ttu-id="c7c64-780">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-780">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-781">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-781">Allowed From</span></span>

<span data-ttu-id="c7c64-782">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-782">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-783">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-783">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-784">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-784">See Also</span></span>

- <span data-ttu-id="c7c64-785">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-785">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-786">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-786">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="c7c64-787">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-787">nx_secure_tls_active_certificate_set</span></span>

## <a name="nx_secure_tls_session_x509_client_verify_configure"></a><span data-ttu-id="c7c64-788">nx_secure_tls_session_x509_client_verify_configure</span><span class="sxs-lookup"><span data-stu-id="c7c64-788">nx_secure_tls_session_x509_client_verify_configure</span></span>

<span data-ttu-id="c7c64-789">Abilitare la verifica X.509 del client e allocare spazio per i certificati client</span><span class="sxs-lookup"><span data-stu-id="c7c64-789">Enable client X.509 verification and allocate space for client certificates</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-790">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-790">Prototype</span></span>

```C
UINT  nx_secure_tls_session_x509_client_verify_configure(
                  NX_SECURE_TLS_SESSION *session_ptr,
                  UINT certs_number, VOID *certificate_buffer,
                  ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="c7c64-791">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-791">Description</span></span>

<span data-ttu-id="c7c64-792">Questo servizio abilita l'autenticazione client X.509 facoltativa per un'istanza del server TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-792">This service enables the optional X.509 Client Authentication for a TLS Server instance.</span></span> <span data-ttu-id="c7c64-793">Alloca anche lo spazio necessario per elaborare le catene di certificati in ingresso dall'host client remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-793">It also allocates the space needed to process incoming certificate chains from the remote client host.</span></span> <span data-ttu-id="c7c64-794">I certificati forniti dal client remoto verranno verificati in base ai certificati attendibili dell'istanza del server TLS, assegnati al servizio *nx_secure_tls_trusted_certificate_add.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-794">The certificates supplied by the remote client will be verified against the TLS server instance's trusted certificates, assigned with the service *nx_secure_tls_trusted_certificate_add.*</span></span>

<span data-ttu-id="c7c64-795">Per la modalità client TLS, è necessaria l'allocazione remota dei certificati e deve *essere* nx_secure_tls_remote_certificate_buffer_allocate servizio.</span><span class="sxs-lookup"><span data-stu-id="c7c64-795">For TLS Client mode, remote certificate allocation is required and the service *nx_secure_tls_remote_certificate_buffer_allocate* should be used instead.</span></span> <span data-ttu-id="c7c64-796">L'abilitazione dell'autenticazione client X.509 in un'istanza del client TLS non avrà alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-796">Enabling X.509 Client Authentication on a TLS Client instance will have no effect.</span></span>

<span data-ttu-id="c7c64-797">Il *certificate_buffer* punta allo spazio allocato per archiviare i certificati remoti in ingresso e i blocchi di controllo necessari per tali certificati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-797">The *certificate_buffer* parameter points to space allocated to store the incoming remote certificates and the control blocks needed for those certificates.</span></span> <span data-ttu-id="c7c64-798">Il buffer verrà diviso per il numero di certificati (*certs_number*) con una parte uguale a ogni certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-798">The buffer will be divided by the number of certificates (*certs_number*) with an equal portion given to each certificate.</span></span> <span data-ttu-id="c7c64-799">Il *buffer_size* parametro indica le dimensioni del buffer.</span><span class="sxs-lookup"><span data-stu-id="c7c64-799">The *buffer_size* parameter indicates the size of the buffer.</span></span> <span data-ttu-id="c7c64-800">Lo spazio necessario è disponibile con la formula seguente:</span><span class="sxs-lookup"><span data-stu-id="c7c64-800">The space needed can be found with the following formula:</span></span>

```C
buffer_size = (<expected max number of certificates in chain>) *
             (sizeof(NX_SECURE_X509_CERT) + <max cert size>)
```

<span data-ttu-id="c7c64-801">I certificati tipici con chiavi RSA a 2048 bit che usano SHA-256 per le firme sono nell'intervallo di 1000-2000 byte.</span><span class="sxs-lookup"><span data-stu-id="c7c64-801">Typical certificates with RSA keys of 2048 bits using SHA-256 for signatures are in the range of 1000-2000 bytes.</span></span> <span data-ttu-id="c7c64-802">Il buffer deve essere sufficientemente grande da contenere almeno tale dimensione per ogni certificato, ma a seconda dei certificati host remoti può essere notevolmente più piccolo o più grande.</span><span class="sxs-lookup"><span data-stu-id="c7c64-802">The buffer should be large enough to at least hold that size for each certificate, but depending on the remote host certificates may be significantly smaller or larger.</span></span> <span data-ttu-id="c7c64-803">Si noti che se il buffer è troppo piccolo per contenere il certificato in ingresso, l'handshake TLS terminerà con un errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-803">Note that if the buffer is too small to hold the incoming certificate, the TLS handshake will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-804">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-804">Parameters</span></span>

- <span data-ttu-id="c7c64-805">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-805">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-806">**certs_number** Numero di certificati da allocare dal buffer specificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-806">**certs_number** Number of certificates to allocate from the provided buffer.</span></span>
- <span data-ttu-id="c7c64-807">**certificate_buffer** Puntatore a un buffer per contenere i certificati ricevuti da un host remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-807">**certificate_buffer** Pointer to a buffer to hold certificates received from a remote host.</span></span>
- <span data-ttu-id="c7c64-808">**buffer_size** Dimensioni del buffer del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-808">**buffer_size** Size of the certificate buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-809">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-809">Return Values</span></span>

- <span data-ttu-id="c7c64-810">**NX_SUCCESS** (0x00)Allocazione del certificato completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-810">**NX_SUCCESS** (0x00)Successful allocation of certificate.</span></span>
- <span data-ttu-id="c7c64-811">**NX_PTR_ERROR** (0x07) Sessione TLS o puntatore al buffer non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-811">**NX_PTR_ERROR** (0x07) Invalid TLS session or buffer pointer.</span></span>
- <span data-ttu-id="c7c64-812">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) Il buffer fornito era troppo piccolo.</span><span class="sxs-lookup"><span data-stu-id="c7c64-812">**NX_SECURE_TLS_INSUFFICIENT_CERT_SPACE** (0x12D) The supplied buffer was too small.</span></span>
- <span data-ttu-id="c7c64-813">**NX_INVALID_PARAMETERS** (0x4D) Il buffer era troppo piccolo per contenere il numero desiderato di certificati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-813">**NX_INVALID_PARAMETERS** (0x4D) The buffer was too small to hold the desired number of certificates.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-814">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-814">Allowed From</span></span>

<span data-ttu-id="c7c64-815">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-815">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-816">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-816">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-817">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-817">See Also</span></span>

- <span data-ttu-id="c7c64-818">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-818">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-819">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-819">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-820">nx_secure_tls_remote_certificate_buffer_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-820">nx_secure_tls_remote_certificate_buffer_allocate</span></span>

## <a name="nx_secure_tls_session_client_verify_disable"></a><span data-ttu-id="c7c64-821">nx_secure_tls_session_client_verify_disable</span><span class="sxs-lookup"><span data-stu-id="c7c64-821">nx_secure_tls_session_client_verify_disable</span></span>

<span data-ttu-id="c7c64-822">Disabilitare l'autenticazione del certificato client per una sessione TLS protetta NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-822">Disable Client Certificate Authentication for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-823">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-823">Prototype</span></span>

```C
UINT  nx_secure_tls_session_client_verify_disable(
                              NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="c7c64-824">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-824">Description</span></span>

<span data-ttu-id="c7c64-825">Questo servizio disabilita l'autenticazione del certificato client per una sessione TLS specifica.</span><span class="sxs-lookup"><span data-stu-id="c7c64-825">This service disables Client Certificate Authentication for a specific TLS session.</span></span> <span data-ttu-id="c7c64-826">Vedere nx_secure_tls_session_client_verify_enable per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="c7c64-826">See nx_secure_tls_session_client_verify_enable for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-827">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-827">Parameters</span></span>

- <span data-ttu-id="c7c64-828">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-828">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-829">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-829">Return Values</span></span>

- <span data-ttu-id="c7c64-830">**NX_SUCCESS** (0x00) Modifica dello stato riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-830">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="c7c64-831">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-831">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-832">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-832">Allowed From</span></span>

<span data-ttu-id="c7c64-833">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-833">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-834">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-834">Example</span></span>

```C
/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_disable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will not
request certificates from the remote TLS client.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-835">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-835">See Also</span></span>

- <span data-ttu-id="c7c64-836">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="c7c64-836">nx_secure_tls_session_client_verify_enable</span></span>
- <span data-ttu-id="c7c64-837">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-837">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-838">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-838">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_client_verify_enable"></a><span data-ttu-id="c7c64-839">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="c7c64-839">nx_secure_tls_session_client_verify_enable</span></span>

<span data-ttu-id="c7c64-840">Abilitare l'autenticazione del certificato client per una sessione TLS sicura netx</span><span class="sxs-lookup"><span data-stu-id="c7c64-840">Enable Client Certificate Authentication for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-841">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-841">Prototype</span></span>

```C
UINT  nx_secure_tls_session_client_verify_enable(
                                NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="c7c64-842">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-842">Description</span></span>

<span data-ttu-id="c7c64-843">Questo servizio abilita l'autenticazione del certificato client per una sessione TLS specifica.</span><span class="sxs-lookup"><span data-stu-id="c7c64-843">This service enables Client Certificate Authentication for a specific TLS session.</span></span> <span data-ttu-id="c7c64-844">Se si abilita l'autenticazione del certificato client per un'istanza del server TLS, il server TLS richiederà un certificato da qualsiasi client TLS remoto durante l'handshake TLS iniziale.</span><span class="sxs-lookup"><span data-stu-id="c7c64-844">Enabling Client Certificate Authentication for a TLS Server instance will cause the TLS Server to request a certificate from any remote TLS Client during the initial TLS handshake.</span></span> <span data-ttu-id="c7c64-845">Il certificato ricevuto dal client TLS remoto è accompagnato da un messaggio CertificateVerify, che il server TLS usa per verificare che il client sia proprietario del certificato (ha accesso alla chiave privata associata a tale certificato).</span><span class="sxs-lookup"><span data-stu-id="c7c64-845">The certificate received from the remote TLS Client is accompanied by a CertificateVerify message, which the TLS Server uses to verify that the Client owns the certificate (has access to the private key associated with that certificate).</span></span>

<span data-ttu-id="c7c64-846">Se il certificato fornito può essere verificato e tracciato di nuovo in un certificato nell'archivio certificati attendibili del server TLS tramite una catena di certificati X.509, il client TLS remoto viene autenticato e l'handshake continua.</span><span class="sxs-lookup"><span data-stu-id="c7c64-846">If the provided certificate can be verified and traced back to a certificate in the TLS Server trusted certificate store via an X.509 certificate chain, the remote TLS Client is authenticated and the handshake proceeds.</span></span> <span data-ttu-id="c7c64-847">In caso di errori durante l'elaborazione del certificato o del messaggio CertificateVerify, l'handshake TLS termina con un errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-847">In case of any errors in processing the certificate or CertificateVerify message, the TLS handshake ends with an error.</span></span>

> [!NOTE]
> <span data-ttu-id="c7c64-848">*Il server TLS deve avere almeno un certificato nell'archivio attendibile aggiunto con nx_secure_tls_trusted_certificate_add l'autenticazione avrà sempre esito negativo.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-848">*The TLS Server must have at least one certificate in its trusted store added with nx_secure_tls_trusted_certificate_add or authentication will always fail.*</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-849">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-849">Parameters</span></span>

- <span data-ttu-id="c7c64-850">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-850">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-851">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-851">Return Values</span></span>

- <span data-ttu-id="c7c64-852">**NX_SUCCESS** (0x00) Modifica dello stato riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-852">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="c7c64-853">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-853">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-854">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-854">Allowed From</span></span>

<span data-ttu-id="c7c64-855">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-855">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-856">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-856">Example</span></span>

```C
/* Add a trusted certificate so the TLS Server has something to verify against. */
status = nx_secure_tls_trusted_certificate_add(&tls_session,
                                               &trusted_certificate);

/* Disable client certificate authentication for this TLS session.   */
status = nx_secure_tls_session_client_verify_enable(&tls_session);

/* Any new TLS Server sessions using the tls_session control block will now
request and verify certificates from the remote TLS client.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-857">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-857">See Also</span></span>

- <span data-ttu-id="c7c64-858">nx_secure_tls_session_client_verify_enable</span><span class="sxs-lookup"><span data-stu-id="c7c64-858">nx_secure_tls_session_client_verify_enable</span></span>
- <span data-ttu-id="c7c64-859">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-859">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-860">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-860">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-861">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-861">nx_secure_tls_trusted_certificate_add</span></span>

## <a name="nx_secure_tls_session_create"></a><span data-ttu-id="c7c64-862">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-862">nx_secure_tls_session_create</span></span>

<span data-ttu-id="c7c64-863">Creare una sessione TLS sicura netx per le comunicazioni sicure</span><span class="sxs-lookup"><span data-stu-id="c7c64-863">Create a NetX Secure TLS Session for secure communications</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-864">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-864">Prototype</span></span>

```C
UINT  nx_secure_tls_session_create(NX_SECURE_TLS_SESSION *session_ptr
                                   NX_SECURE_TLS_CRYPTO *cipher_table,
                                   VOID *encryption_metadata_area,
                                   ULONG encryption_metadata_size);
```

### <a name="description"></a><span data-ttu-id="c7c64-865">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-865">Description</span></span>

<span data-ttu-id="c7c64-866">Questo servizio inizializza un'istanza NX_SECURE_TLS_SESSION struttura da usare per stabilire comunicazioni TLS sicure su una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="c7c64-866">This service initializes an NX_SECURE_TLS_SESSION structure instance for use in establishing secure TLS communications over a network connection.</span></span>

<span data-ttu-id="c7c64-867">Il metodo accetta un NX_SECURE_TLS_CRYPTO oggetto popolato con i metodi di crittografia disponibili da usare per TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-867">The method takes a NX_SECURE_TLS_CRYPTO object that is populated with the available cryptographic methods to be used for TLS.</span></span> <span data-ttu-id="c7c64-868">*L encryption_metadata_area* punta a un buffer allocato per l'uso da parte di TLS per i "metadati" usati dai metodi di crittografia nella tabella NX_SECURE_TLS_CRYPTO per i calcoli.</span><span class="sxs-lookup"><span data-stu-id="c7c64-868">The *encryption_metadata_area* points to a buffer allocated for use by TLS for the "metadata" used by the cryptographic methods in the NX_SECURE_TLS_CRYPTO table for calculations.</span></span> <span data-ttu-id="c7c64-869">Le dimensioni della tabella possono essere determinate usando il nx_secure_tls_metadata_size_calculate dati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-869">The size of the table can be determined by using the nx_secure_tls_metadata_size_calculate service.</span></span> <span data-ttu-id="c7c64-870">Per altri dettagli, vedere la sezione "Crittografia in NetX Secure TLS" nel capitolo 3.</span><span class="sxs-lookup"><span data-stu-id="c7c64-870">See the section "Cryptography in NetX Secure TLS" in Chapter 3 for more details.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-871">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-871">Parameters</span></span>

- <span data-ttu-id="c7c64-872">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-872">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-873">**cipher_table** Puntatore ai metodi di crittografia TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-873">**cipher_table** Pointer to TLS cryptographic methods.</span></span>
- <span data-ttu-id="c7c64-874">**encryption_metadata_area** Puntatore allo spazio per i metadati di crittografia.</span><span class="sxs-lookup"><span data-stu-id="c7c64-874">**encryption_metadata_area** Pointer to space for cryptography metadata.</span></span>
- <span data-ttu-id="c7c64-875">**encryption_metadata_size** Dimensioni del buffer dei metadati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-875">**encryption_metadata_size** Size of the metadata buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-876">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-876">Return Values</span></span>

- <span data-ttu-id="c7c64-877">**NX_SUCCESS** (0x00)Inizializzazione della sessione TLS completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-877">**NX_SUCCESS** (0x00)Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="c7c64-878">**NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-878">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="c7c64-879">**NX_INVALID_PARAMETERS** (0x4D) Il buffer dei metadati era troppo piccolo per i metodi specificati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-879">**NX_INVALID_PARAMETERS** (0x4D) The metadata buffer was too small for the given methods.</span></span>
- <span data-ttu-id="c7c64-880">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) Nella tabella di crittografia non è stato fornito un metodo di crittografia obbligatorio per la versione abilitata di TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-880">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A required cipher method for the enabled version of TLS was not supplied in the cipher table.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-881">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-881">Allowed From</span></span>

<span data-ttu-id="c7c64-882">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-882">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-883">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-883">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-884">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-884">See Also</span></span>

- <span data-ttu-id="c7c64-885">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-885">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-886">nx_secure_tls_metadata_size_calculate</span><span class="sxs-lookup"><span data-stu-id="c7c64-886">nx_secure_tls_metadata_size_calculate</span></span>
- <span data-ttu-id="c7c64-887">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-887">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-888">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-888">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-889">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="c7c64-889">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="c7c64-890">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-890">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="c7c64-891">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-891">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="c7c64-892">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-892">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="c7c64-893">Crittografia in NetX Secure TLS nel capitolo 3</span><span class="sxs-lookup"><span data-stu-id="c7c64-893">Cryptography in NetX Secure TLS in Chapter 3</span></span>

## <a name="nx_secure_tls_session_delete"></a><span data-ttu-id="c7c64-894">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-894">nx_secure_tls_session_delete</span></span>

<span data-ttu-id="c7c64-895">Eliminare una sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-895">Delete a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-896">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-896">Prototype</span></span>

```C
UINT  nx_secure_tls_session_delete(NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="c7c64-897">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-897">Description</span></span>

<span data-ttu-id="c7c64-898">Questo servizio elimina una sessione TLS rappresentata da un'istanza NX_SECURE_TLS_SESSION e rilascia tutte le risorse di sistema di proprietà di tale istanza di sessione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-898">This service deletes a TLS session represented by an NX_SECURE_TLS_SESSION structure instance and releases all system resources owned by that session instance.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-899">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-899">Parameters</span></span>

- <span data-ttu-id="c7c64-900">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-900">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-901">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-901">Return Values</span></span>

- <span data-ttu-id="c7c64-902">**NX_SUCCESS** (0x00) Inizializzazione riuscita della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-902">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="c7c64-903">**NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-903">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-904">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-904">Allowed From</span></span>

<span data-ttu-id="c7c64-905">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-905">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-906">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-906">Example</span></span>

```C
/* Delete TLS session.  */
status =  nx_secure_tls_session_delete(&tls_session);


/* If status is NX_SUCCESS the TLS Session was successfully deleted.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-907">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-907">See Also</span></span>

- <span data-ttu-id="c7c64-908">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-908">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-909">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-909">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-910">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-910">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-911">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="c7c64-911">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="c7c64-912">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-912">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="c7c64-913">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-913">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="c7c64-914">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-914">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_end"></a><span data-ttu-id="c7c64-915">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="c7c64-915">nx_secure_tls_session_end</span></span>

<span data-ttu-id="c7c64-916">Terminare una sessione TLS sicura di NetX attiva</span><span class="sxs-lookup"><span data-stu-id="c7c64-916">End an active NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-917">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-917">Prototype</span></span>

```C
UINT  nx_secure_tls_session_end(NX_SECURE_TLS_SESSION *session_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c7c64-918">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-918">Description</span></span>

<span data-ttu-id="c7c64-919">Questo servizio termina una sessione TLS rappresentata da un'istanza NX_SECURE_TLS_SESSION di sicurezza inviando il messaggio CLOSENotify TLS all'host remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-919">This service ends a TLS session represented by an NX_SECURE_TLS_SESSION structure instance by sending the TLS CloseNotify message to the remote host.</span></span> <span data-ttu-id="c7c64-920">Il servizio attende quindi che l'host remoto risponda con il proprio messaggio CloseNotify.</span><span class="sxs-lookup"><span data-stu-id="c7c64-920">The service then waits for the remote host to respond with its own CloseNotify message.</span></span>

<span data-ttu-id="c7c64-921">Se l'host remoto non invia un messaggio CloseNotify, TLS considera questo errore e una possibile violazione della sicurezza, quindi controllare il valore restituito è importante per una connessione sicura.</span><span class="sxs-lookup"><span data-stu-id="c7c64-921">If the remote host does not send a CloseNotify message, TLS considers this an error and a possible security breach, so checking the return value is important for a secure connection.</span></span> <span data-ttu-id="c7c64-922">Il **wait_option** può essere usato per controllare per quanto tempo il servizio deve attendere la risposta prima di restituire il controllo al thread chiamante.</span><span class="sxs-lookup"><span data-stu-id="c7c64-922">The **wait_option** parameter can be used to control how long the service should wait for the response before returning control to the calling thread.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-923">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-923">Parameters</span></span>

- <span data-ttu-id="c7c64-924">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-924">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-925">**wait_option** Indica per quanto tempo il servizio deve attendere la risposta dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-925">**wait_option** Indicates how long the service should wait for the response from the remote host.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-926">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-926">Return Values</span></span>

- <span data-ttu-id="c7c64-927">**NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-927">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="c7c64-928">**NX_SECURE_TLS_NO_CLOSE_RESPONSE** (0x113) Non ha ricevuto una risposta dall'host remoto prima del timeout.</span><span class="sxs-lookup"><span data-stu-id="c7c64-928">**NX_SECURE_TLS_NO_CLOSE_RESPONSE** (0x113) Did not receive a response from the remote host before timing out.</span></span>
- <span data-ttu-id="c7c64-929">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Impossibile allocare un pacchetto per inviare il messaggio CloseNotify.</span><span class="sxs-lookup"><span data-stu-id="c7c64-929">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Could not allocate a packet to send the CloseNotify message.</span></span>
- <span data-ttu-id="c7c64-930">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Impossibile inviare il messaggio CloseNotify sul socket TCP.</span><span class="sxs-lookup"><span data-stu-id="c7c64-930">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Could not send the CloseNotify message over the TCP socket.</span></span>
- <span data-ttu-id="c7c64-931">**NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-931">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-932">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-932">Allowed From</span></span>

<span data-ttu-id="c7c64-933">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-933">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-934">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-934">Example</span></span>

```C
/* End TLS session.  */
status =  nx_secure_tls_session_end(&tls_session, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the TLS Session was successfully ended.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-935">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-935">See Also</span></span>

- <span data-ttu-id="c7c64-936">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-936">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-937">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-937">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-938">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-938">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-939">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-939">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="c7c64-940">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-940">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="c7c64-941">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-941">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="c7c64-942">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-942">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_packet_buffer_set"></a><span data-ttu-id="c7c64-943">nx_secure_tls_session_packet_buffer_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-943">nx_secure_tls_session_packet_buffer_set</span></span>

<span data-ttu-id="c7c64-944">Impostare il buffer di riassemblaggio dei pacchetti per una sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-944">Set the packet reassembly buffer for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-945">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-945">Prototype</span></span>

```C
UINT  nx_secure_tls_session_packet_buffer_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *buffer_ptr,
                                    ULONG buffer_size);
```

### <a name="description"></a><span data-ttu-id="c7c64-946">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-946">Description</span></span>

<span data-ttu-id="c7c64-947">Questo servizio associa un buffer di riassemblaggio di pacchetti a una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-947">This service associates a packet reassembly buffer to a TLS session.</span></span> <span data-ttu-id="c7c64-948">Per decrittografare e analizzare i record TLS in ingresso, i dati in ogni record devono essere assemblati dai pacchetti TCP sottostanti.</span><span class="sxs-lookup"><span data-stu-id="c7c64-948">In order to decrypt and parse incoming TLS records, the data in each record must be assembled from the underlying TCP packets.</span></span> <span data-ttu-id="c7c64-949">I record TLS possono avere dimensioni massime di 16 KB (anche se in genere sono molto più piccoli), quindi potrebbero non rientrare in un singolo pacchetto TCP.</span><span class="sxs-lookup"><span data-stu-id="c7c64-949">TLS records can be up to 16KB in size (though typically are much smaller) so may not fit into a single TCP packet.</span></span>

<span data-ttu-id="c7c64-950">Se si sa che le dimensioni dei messaggi in ingresso saranno inferiori al limite di record TLS di 16 KB, le dimensioni del buffer possono essere ridotte, ma per gestire i dati in ingresso sconosciuti il buffer deve essere reso il più grande possibile.</span><span class="sxs-lookup"><span data-stu-id="c7c64-950">If you know the incoming message size will be smaller than the TLS record limit of 16KB, the buffer size can be made smaller, but in order to handle unknown incoming data the buffer should be made as large as possible.</span></span> <span data-ttu-id="c7c64-951">Se un record in ingresso è più grande del buffer fornito, la sessione TLS terminerà con un errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-951">If an incoming record is larger than the supplied buffer, the TLS session will end with an error.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-952">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-952">Parameters</span></span>

- <span data-ttu-id="c7c64-953">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-953">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-954">**buffer_ptr** Puntatore al buffer per TLS da usare per il riassemblaggio dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c7c64-954">**buffer_ptr** Pointer to buffer for TLS to use for packet reassembly.</span></span>
- <span data-ttu-id="c7c64-955">**buffer_size** Dimensioni del buffer fornito in byte.</span><span class="sxs-lookup"><span data-stu-id="c7c64-955">**buffer_size** Size of the supplied buffer in bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-956">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-956">Return Values</span></span>

- <span data-ttu-id="c7c64-957">**NX_SUCCESS** (0x00) Inizializzazione riuscita della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-957">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="c7c64-958">**NX_INVALID_PARAMETERS** (0x4D) Buffer o puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-958">**NX_INVALID_PARAMETERS** (0x4D) Invalid buffer or TLS session pointer.</span></span>
- <span data-ttu-id="c7c64-959">**NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-959">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-960">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-960">Allowed From</span></span>

<span data-ttu-id="c7c64-961">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-961">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-962">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-962">Example</span></span>

```C
/* Buffer for TLS packet reassembly. */
UCHAR tls_packet_buffer[16384];
/* Assign buffer to TLS session.  */
status =  nx_secure_tls_session_packet_buffer_set(&tls_session, tls_packet_buffer,
                                                  sizeof(tls_packet_buffer));


/* If status is NX_SUCCESS the buffer was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-963">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-963">See Also</span></span>

- <span data-ttu-id="c7c64-964">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-964">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-965">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-965">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-966">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-966">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-967">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-967">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="c7c64-968">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-968">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="c7c64-969">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-969">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="c7c64-970">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-970">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_protocol_version_override"></a><span data-ttu-id="c7c64-971">nx_secure_tls_session_protocol_version_override</span><span class="sxs-lookup"><span data-stu-id="c7c64-971">nx_secure_tls_session_protocol_version_override</span></span>

<span data-ttu-id="c7c64-972">Eseguire l'override della versione predefinita del protocollo TLS per una sessione TLS sicura netx</span><span class="sxs-lookup"><span data-stu-id="c7c64-972">Override the default TLS protocol version for a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-973">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-973">Prototype</span></span>

```C
UINT  nx_secure_tls_session_protocol_version_override(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              USHORT protocol_version);
```

### <a name="description"></a><span data-ttu-id="c7c64-974">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-974">Description</span></span>

<span data-ttu-id="c7c64-975">Questo servizio esegue l'override della versione predefinita (più recente) del protocollo TLS usata da una sessione specifica.</span><span class="sxs-lookup"><span data-stu-id="c7c64-975">This service overrides the default (newest) TLS protocol version used by a particular session.</span></span> <span data-ttu-id="c7c64-976">Ciò consente a NetX Secure TLS di usare una versione precedente di TLS per una sessione TLS specifica senza disabilitare le versioni più recenti di TLS in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-976">This enables NetX Secure TLS to use an older version of TLS for a specific TLS Session without disabling newer TLS versions at compile time.</span></span> <span data-ttu-id="c7c64-977">Questo può essere utile nelle applicazioni che potrebbero dover comunicare con un host meno recente che non supporta la versione più recente di TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-977">This may be useful in applications that may need to communicate with an older host that does not support the newest version of TLS.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7c64-978">*A causa della versione 5.11SP3, NetX Secure TLS supporta RFC 7507 (vedere la nota seguente) e qualsiasi override di una versione precedente con questa API comporta l'invio di un scsv di fallback in ClientHello. Se il server supporta una versione più recente di TLS e il fallback SCSV è incluso in ClientHello, tale server interromperà l'handshake TLS con un avviso di fallback non appropriato. ScSV viene inviato solo quando l'override della versione è una versione precedente di TLS di quella abilitata (ad esempio, se si esegue l'override della versione a TLS 1.2, non verrà inviato alcun SCSV).*</span><span class="sxs-lookup"><span data-stu-id="c7c64-978">*As of version 5.11SP3, NetX Secure TLS supports RFC 7507 (see note below) and any override to an older version with this API will result in a fallback SCSV being sent in the ClientHello. If the server supports a newer version of TLS and the fallback SCSV is included in the ClientHello, that server will abort the TLS handshake with an "Inappropriate Fallback" alert. The SCSV is only sent when the version override is an older version of TLS than is enabled (e.g. if you override the version to TLS 1.2, no SCSV will be sent).*</span></span>

<span data-ttu-id="c7c64-979">I valori validi per il protocol_version sono le macro seguenti: NX_SECURE_TLS_VERSION_TLS_1_0, NX_SECURE_TLS_VERSION_TLS_1_1 e NX_SECURE_TLS_VERSION_TLS_1_2.</span><span class="sxs-lookup"><span data-stu-id="c7c64-979">Valid values for the protocol_version parameter are the following macros: NX_SECURE_TLS_VERSION_TLS_1_0, NX_SECURE_TLS_VERSION_TLS_1_1, and NX_SECURE_TLS_VERSION_TLS_1_2.</span></span>

<span data-ttu-id="c7c64-980">Le macro NX_SECURE_TLS_DISABLE_TLS_1_1 e NX_SECURE_TLS_ENABLE_TLS_1_0 possono essere usate per controllare le versioni di TLS compilate nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-980">The macros NX_SECURE_TLS_DISABLE_TLS_1_1 and NX_SECURE_TLS_ENABLE_TLS_1_0 can be used to control the versions of TLS that are compiled into the application.</span></span> <span data-ttu-id="c7c64-981">TLS versione 1.2 è sempre abilitato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-981">TLS version 1.2 is always enabled.</span></span>

<span data-ttu-id="c7c64-982">Si noti che se l'host remoto non supporta la versione fornita, la connessione avrà esito negativo. Solo la versione di sostituzione fornita verrà negoziata da NetX Secure TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-982">Note that if the remote host does not support the supplied version, the connection will fail – only the supplied override version will be negotiated by NetX Secure TLS.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7c64-983">RFC 7507: SCSV di fallback TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-983">RFC 7507: TLS Fallback SCSV.</span></span> <span data-ttu-id="c7c64-984">Questa RFC è stata introdotta per attenuare un problema di sicurezza causato originariamente da server che gestivano in modo non corretto la negoziazione di downgrade del protocollo e rifiutavano invece messaggi ClientHello altrimenti validi.</span><span class="sxs-lookup"><span data-stu-id="c7c64-984">This RFC was introduced to mitigate a security problem that was originally caused by servers that improperly handled protocol downgrade negotiation and instead rejected otherwise valid ClientHello messages.</span></span> <span data-ttu-id="c7c64-985">Nel tentativo di mantenere la compatibilità con questi server precedenti, alcune applicazioni client TLS hanno iniziato a ripetere gli handshake non riusciti con e la versione precedente di TLS (ad esempio TLS 1.2 non è riuscito, quindi provare TLS 1.1).</span><span class="sxs-lookup"><span data-stu-id="c7c64-985">In an attempt to remain compatible with these old servers, some TLS client applications started to retry failed handshakes with and older TLS version (e.g. TLS 1.2 failed so try TLS 1.1).</span></span> <span data-ttu-id="c7c64-986">Questa soluzione alternativa ha tuttavia introdotto un nuovo problema: un utente malintenzionato potrebbe forzare il downgrade di un client introducendo artificialmente un errore di rete o di pacchetto che causa l'esito negativo della connessione al server, anche quando il server supporta la versione più recente di TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-986">This workaround however introduced a new problem – an attacker could force a client to downgrade by artificially introducing a network or packet error causing the server connection to fail – even when the server supported the newer TLS version.</span></span> <span data-ttu-id="c7c64-987">Effettuando il downgrade a una versione precedente, l'utente malintenzionato potrebbe sfruttare i punti deboli di tale versione (SSLv3<sup>21</sup> in particolare è debole per l'attacco POODLE).</span><span class="sxs-lookup"><span data-stu-id="c7c64-987">By downgrading to an older version the attacker could exploit weaknesses in that version (SSLv3<sup>21</sup> in particular is weak to the POODLE attack).</span></span> <span data-ttu-id="c7c64-988">Per evitare questa situazione, RFC 7507 ha presentato la "scSV di fallback", una pseudo-crittografia<sup>22</sup> inviata in ClientHello che invia una notifica a un server TLS quando un client TLS usa una versione TLS non supportata dalla versione più recente.</span><span class="sxs-lookup"><span data-stu-id="c7c64-988">To prevent this situation, RFC 7507 introdued the "fallback SCSV," a pseudo-ciphersuite<sup>22</sup> sent in the ClientHello that notifies a TLS server when a TLS client is using a TLS version that is not the newest version it supports.</span></span> <span data-ttu-id="c7c64-989">In questo modo, un server che supporta una versione più recente può rifiutare un ClientHello contenente la versione scSV di fallback e impedire il successo dell'attacco di downgrade.</span><span class="sxs-lookup"><span data-stu-id="c7c64-989">This way, a server that supports a newer version can reject a ClientHello containing the fallback SCSV and prevent the downgrade attack from succeeding.</span></span>

21. <span data-ttu-id="c7c64-990">NetX Secure non implementa SSLv3 a causa dell'esistenza di gravi punti deboli noti, ad esempio POODLE.</span><span class="sxs-lookup"><span data-stu-id="c7c64-990">NetX Secure does not implement SSLv3 due to the existence of known serious weaknesses such as POODLE.</span></span>

22. <span data-ttu-id="c7c64-991">Uno pseudo-ciphersuite, o SCSV (Signaling Cipher Suite Value), è un numero di ciphersuite riservato usato per segnalare le implementazioni TLS abilitate sulle funzionalità che non erano disponibili nelle versioni precedenti di TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-991">A pseudo-ciphersuite, or SCSV (Signaling Cipher Suite Value), is a reserved ciphersuite number that is used to signal enabled TLS implementations about features that were not available in older TLS versions.</span></span> <span data-ttu-id="c7c64-992">ScSV di fallback e TLS_EMPTY_RENEGOTIATION_INFO_SCSV (RFC 5746) sono esempi.</span><span class="sxs-lookup"><span data-stu-id="c7c64-992">The fallback SCSV and the TLS_EMPTY_RENEGOTIATION_INFO_SCSV (RFC 5746) are examples.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-993">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-993">Parameters</span></span>

- <span data-ttu-id="c7c64-994">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-994">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-995">**protocol_version** Macro della versione di TLS per la versione specifica di TLS da usare.</span><span class="sxs-lookup"><span data-stu-id="c7c64-995">**protocol_version** TLS version macro for the specific TLS version to use.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-996">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-996">Return Values</span></span>

- <span data-ttu-id="c7c64-997">**NX_SUCCESS** (0x00) Modifica dello stato riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-997">**NX_SUCCESS** (0x00) Successful state change.</span></span>
- <span data-ttu-id="c7c64-998">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-998">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="c7c64-999">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) Versione TLS nota ma non supportata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-999">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) Known but unsupported TLS version.</span></span>
- <span data-ttu-id="c7c64-1000">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Versione del protocollo non valida.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1000">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Invalid protocol version.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1001">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1001">Allowed From</span></span>

<span data-ttu-id="c7c64-1002">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1002">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1003">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1003">Example</span></span>

```C
/* Set the protocol version to be used to TLSv1.1. */
status = nx_secure_tls_session_protocol_version_override(&tls_session,
                                              NX_SECURE_TLS_VERSION_TLS_1_1);

/* This TLS Session will use TLSv1.1 for the handshake and TLS session. */
status = nx_secure_tls_session_start(&tls_session, &tcp_socket, NX_WAIT_FOREVER);
```

### <a name="see-also"></a><span data-ttu-id="c7c64-1004">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1004">See Also</span></span>

- <span data-ttu-id="c7c64-1005">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-1005">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-1006">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1006">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_receive"></a><span data-ttu-id="c7c64-1007">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-1007">nx_secure_tls_session_receive</span></span>

<span data-ttu-id="c7c64-1008">Ricevere dati da una sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-1008">Receive data from a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1009">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1009">Prototype</span></span>

```C
UINT  nx_secure_tls_session_receive(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET **packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c7c64-1010">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1010">Description</span></span>

<span data-ttu-id="c7c64-1011">Questo servizio riceve i dati dalla sessione TLS attiva specificata, gestendo la decrittografia dei dati prima di fornirla al chiamante nel parametro NX_PACKET.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1011">This service receives data from the specified active TLS session, handling the decryption of that data before providing it to the caller in the NX_PACKET parameter.</span></span> <span data-ttu-id="c7c64-1012">Se nella sessione specificata non viene accodato alcun dato, la chiamata viene sospesa in base all'opzione di attesa fornita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1012">If no data is queued in the specified session, the call suspends based on the supplied wait option.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7c64-1013">*Se NX_SUCCESS restituito, l'applicazione è responsabile del rilascio del pacchetto ricevuto quando non è più necessario.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-1013">*If NX_SUCCESS is returned, the application is responsible for releasing the received packet when it is no longer needed.*</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1014">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1014">Parameters</span></span>

- <span data-ttu-id="c7c64-1015">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1015">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-1016">**packet_ptr** Puntatore a un puntatore a pacchetto TLS allocato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1016">**packet_ptr** Pointer to an allocated TLS packet pointer.</span></span>
- <span data-ttu-id="c7c64-1017">**wait_option** Indica per quanto tempo il servizio deve attendere un pacchetto dall'host remoto prima della restituzione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1017">**wait_option** Indicates how long the service should wait for a packet from the remote host before returning.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1018">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1018">Return Values</span></span>

- <span data-ttu-id="c7c64-1019">**NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1019">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="c7c64-1020">**NX_NO_PACKET** (0x01) Nessun dato ricevuto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1020">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="c7c64-1021">**NX_NOT_CONNECTED** (0x38) Il socket TCP sottostante non è più connesso.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1021">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="c7c64-1022">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Un messaggio ricevuto non è riuscito a eseguire un controllo hash di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1022">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A received message failed an authentication hash check.</span></span>
- <span data-ttu-id="c7c64-1023">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Un messaggio ricevuto conteneva una versione del protocollo sconosciuta nella relativa intestazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1023">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received message contained an unknown protocol version in its header.</span></span>
- <span data-ttu-id="c7c64-1024">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Ha ricevuto un avviso TLS dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1024">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Received a TLS alert from the remote host.</span></span>
- <span data-ttu-id="c7c64-1025">**NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1025">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="c7c64-1026">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) La sessione TLS fornita non è stata inizializzata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1026">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1027">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1027">Allowed From</span></span>

<span data-ttu-id="c7c64-1028">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1028">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1029">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1029">Example</span></span>

```C
/* Receive a packet from an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is received, blocking otherwise.
*/
status =  nx_secure_tls_session_receive(&tls_session, &packet_ptr,
NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the received packet is pointed to by  "packet_ptr". */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-1030">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1030">See Also</span></span>

- <span data-ttu-id="c7c64-1031">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-1031">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="c7c64-1032">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-1032">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-1033">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1033">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-1034">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-1034">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-1035">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-1035">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="c7c64-1036">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-1036">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="c7c64-1037">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="c7c64-1037">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="c7c64-1038">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1038">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_renegotiate_callback_set"></a><span data-ttu-id="c7c64-1039">nx_secure_tls_session_renegotiate_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1039">nx_secure_tls_session_renegotiate_callback_set</span></span>

<span data-ttu-id="c7c64-1040">Assegnare un callback che verrà richiamato all'inizio di una rinegoziazione della sessione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1040">Assign a callback that will be invoked at the beginning of a session renegotiation</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1041">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1041">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_renegotiate_callback_set (
                  NX_SECURE_TLS_SESSION *tls_session,
                  ULONG (*func_ptr)(struct NX_SECURE_TLS_SESSION_struct
                  *session));
```

### <a name="description"></a><span data-ttu-id="c7c64-1042">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1042">Description</span></span>

<span data-ttu-id="c7c64-1043">Questo servizio assegna un callback a una sessione TLS che verrà richiamata ogni volta che dall'host remoto viene ricevuto il primo messaggio di un handshake di rinegoziazione della sessione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1043">This service assigns a callback to a TLS session that will be invoked whenever the first message of a session renegotiation handshake is received from the remote host.</span></span>

<span data-ttu-id="c7c64-1044">La funzione di callback è concepita come notifica all'applicazione dell'inizio di un handshake di rinegoziazione. L'applicazione può scegliere di terminare la sessione TLS restituisce qualsiasi valore diverso da zero dal callback che causerà la chiusura della sessione TLS da parte di TLS con un errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1044">The callback function is intended as a notification to the application that a renegotiation handshake is beginning – the application may choose to terminate the TLS session by returning any non-zero value from the callback which will cause TLS to end the TLS session with an error.</span></span> <span data-ttu-id="c7c64-1045">Se l'applicazione vuole procedere con la rinegoziazione, il callback deve restituire NX_SUCCESS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1045">If the application wishes to proceed with the renegotiation, the callback should return NX_SUCCESS.</span></span>

> [!NOTE]
> <span data-ttu-id="c7c64-1046">*A causa della semantica di rinegoziazione TLS, il callback verrà richiamato per i client TLS sicuri NetX ogni volta che viene ricevuto un HelloRequest dal server remoto, ma non quando il client avvia la rinegoziazione. Nei server NETX Secure TLS, il callback verrà richiamato ogni volta che viene ricevuto un ClientHello di rinegoziazione (qualsiasi ClientHello ricevuto nel contesto di una sessione TLS attiva). Ciò significa che il callback verrà richiamato se l'host remoto o l'applicazione locale ha avviato la rinegoziazione perché il server TLS invierà un HelloRequest a cui risponderà il client remoto.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-1046">*Due to the semantics of TLS renegotiation, the callback will be invoked for NetX Secure TLS Clients whenever a HelloRequest is received from the remote server, but not when the client initiates the renegotiation. On NetX Secure TLS Servers, the callback will be invoked whenever a renegotiation ClientHello is received (any ClientHello received in the context of an active TLS session). This means that the callback will be invoked whether the remote host or the local application has initiated the renegotiation because the TLS server will send a HelloRequest to which the remote client will respond.*</span></span>

<span data-ttu-id="c7c64-1047">NetX Secure TLS implementa l'estensione Secure Renegotiation Inidication da RFC 5746 per garantire che gli handshake di rinegoziazione non siano soggetti ad attacchi man-in-the-middle.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1047">NetX Secure TLS implements the Secure Renegotiation Inidication Extension from RFC 5746 to ensure that renegotiation handshakes are not subject to man-in-the-middle attacks.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1048">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1048">Parameters</span></span>

- <span data-ttu-id="c7c64-1049">**session_ptr** Puntatore all'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1049">**session_ptr** Pointer to TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-1050">**func_ptr** Puntatore alla funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1050">**func_ptr** Pointer to callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1051">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1051">Return Values</span></span>

- <span data-ttu-id="c7c64-1052">**NX_SUCCESS** (0x00) Assegnazione riuscita del callback.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1052">**NX_SUCCESS** (0x00) Successful assignment of callback.</span></span>
- <span data-ttu-id="c7c64-1053">**NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido per la funzione di callback o la sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1053">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer for the callback function or TLS session.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1054">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1054">Allowed From</span></span>

<span data-ttu-id="c7c64-1055">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1055">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1056">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1056">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1057">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1057">See Also</span></span>

- <span data-ttu-id="c7c64-1058">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1058">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-1059">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-1059">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-1060">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-1060">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="c7c64-1061">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-1061">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="c7c64-1062">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1062">nx_secure_tls_session_renegotiate</span></span>

## <a name="nx_secure_tls_session_renegotiate"></a><span data-ttu-id="c7c64-1063">nx_secure_tls_session_renegotiate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1063">nx_secure_tls_session_renegotiate</span></span>

<span data-ttu-id="c7c64-1064">Avviare un handshake di rinegoziazione della sessione con l'host remoto</span><span class="sxs-lookup"><span data-stu-id="c7c64-1064">Initiate a session renegotiation handshake with the remote host</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1065">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1065">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_renegotiate (
                  NX_SECURE_TLS_SESSION *tls_session,
                  UINT wait_option);
```

### <a name="description"></a><span data-ttu-id="c7c64-1066">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1066">Description</span></span>

<span data-ttu-id="c7c64-1067">Questo servizio avvia un handshake di *rinegoziazione* della sessione con un host TLS remoto connesso.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1067">This service initiates a session *renegotiation* handshake with a connected remote TLS host.</span></span> <span data-ttu-id="c7c64-1068">Una rinegoziazione è costituita da un secondo handshake TLS nel contesto di una sessione TLS stabilita in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1068">A renegotiation consists of a second TLS handshake within the context of a previously-established TLS session.</span></span> <span data-ttu-id="c7c64-1069">Ognuno dei nuovi messaggi di handshake viene crittografato usando la sessione TLS fino a quando non vengono generate nuove chiavi di sessione e non vengono sfrallati i messaggi ChangeCipherSpec, in cui le nuove chiavi vengono usate per crittografare tutti i messaggi.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1069">Each of the new handshake messages is encrypted using the TLS session until new session keys are generated and ChangeCipherSpec messages are exchanged, at which time the new keys are used to encrypt all messages.</span></span>

<span data-ttu-id="c7c64-1070">Una rinegoziazione può essere avviata in qualsiasi momento dopo aver stabilito una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1070">A renegotiation can be initiated at any time once a TLS session is established.</span></span> <span data-ttu-id="c7c64-1071">Se viene tentata una rinegoziazione durante un handshake TLS o prima che venga stabilita una sessione TLS, non verrà eseguita alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1071">If a renegotiation is attempted during a TLS handshake or before a TLS session is established no action will be taken.</span></span>

> [!NOTE]
> <span data-ttu-id="c7c64-1072">*Un intero handshake TLS verrà eseguito quando questo servizio viene richiamato, quindi il tempo di completamento e lo stato restituito variano a seconda delle impostazioni TLS correnti e dei parametri di sessione.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-1072">*An entire TLS handshake will be performed when this service is invoked so the time to completion and returned status will vary depending on the current TLS settings and session parameters.*</span></span>

<span data-ttu-id="c7c64-1073">NetX Secure TLS implementa l'estensione secure renegotiation Inidication di RFC 5746 per garantire che gli handshake di rinegoziazione non siano soggetti ad attacchi man-in-the-middle.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1073">NetX Secure TLS implements the Secure Renegotiation Inidication Extension from RFC 5746 to ensure that renegotiation handshakes are not subject to man-in-the-middle attacks.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1074">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1074">Parameters</span></span>

- <span data-ttu-id="c7c64-1075">**session_ptr** Puntatore all'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1075">**session_ptr** Pointer to TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-1076">**wait_option** Indica per quanto tempo il servizio deve attendere un pacchetto dall'host remoto prima della restituzione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1076">**wait_option** Indicates how long the service should wait for a packet from the remote host before returning.</span></span> <span data-ttu-id="c7c64-1077">Viene passato a tutti i servizi NetX all'interno di TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1077">This is passed to all NetX services within TLS.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1078">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1078">Return Values</span></span>

- <span data-ttu-id="c7c64-1079">**NX_SUCCESS** (0x00) Rinegoziazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1079">**NX_SUCCESS** (0x00) Successful renegotiation.</span></span>
- <span data-ttu-id="c7c64-1080">**NX_NO_PACKET** (0x01) Nessun dato ricevuto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1080">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="c7c64-1081">**NX_NOT_CONNECTED** (0x38) Il socket TCP sottostante non è più connesso.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1081">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="c7c64-1082">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Un messaggio ricevuto non è riuscito a eseguire un controllo hash di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1082">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) A received message failed an authentication hash check.</span></span>
- <span data-ttu-id="c7c64-1083">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Un messaggio ricevuto conteneva una versione del protocollo sconosciuta nella relativa intestazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1083">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received message contained an unknown protocol version in its header.</span></span>
- <span data-ttu-id="c7c64-1084">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Ha ricevuto un avviso TLS dall'host remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1084">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) Received a TLS alert from the remote host.</span></span>
- <span data-ttu-id="c7c64-1085">**NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE** (0x134) La sessione TLS locale o remota è inattiva, rendendo impossibile la rinegoziazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1085">**NX_SECURE_TLS_RENEGOTIATION_SESSION_INACTIVE** (0x134) The local or remote TLS session is inactive, making renegotiation impossible.</span></span>
- <span data-ttu-id="c7c64-1086">**NX_SECURE_TLS_RENEGOTIATION_FAILURE** (0x13A) L'host remoto non ha fornito l'estensione SCSV o Secure Renegotiation e pertanto non è possibile eseguire la rinegoziazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1086">**NX_SECURE_TLS_RENEGOTIATION_FAILURE** (0x13A) The remote host did not provide either the SCSV or Secure Renegotiation Extension and thus renegotiation cannot be performed.</span></span>
- <span data-ttu-id="c7c64-1087">**NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1087">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="c7c64-1088">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) La sessione TLS fornita non è stata inizializzata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1088">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>
- <span data-ttu-id="c7c64-1089">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED(0x111)** Allocazione pacchetti sottostante non riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1089">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Underlying packet allocation failed.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1090">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1090">Allowed From</span></span>

<span data-ttu-id="c7c64-1091">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1091">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1092">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1092">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1093">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1093">See Also</span></span>

- <span data-ttu-id="c7c64-1094">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1094">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-1095">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-1095">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-1096">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-1096">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="c7c64-1097">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-1097">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="c7c64-1098">nx_secure_tls_session_renegotiation_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1098">nx_secure_tls_session_renegotiation_callback_set</span></span>

## <a name="nx_secure_tls_session_reset"></a><span data-ttu-id="c7c64-1099">nx_secure_tls_session_reset</span><span class="sxs-lookup"><span data-stu-id="c7c64-1099">nx_secure_tls_session_reset</span></span>

<span data-ttu-id="c7c64-1100">Cancellare e reimpostare una sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-1100">Clear out and reset a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1101">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1101">Prototype</span></span>

```C
UINT  nx_secure_tls_session_reset (NX_SECURE_TLS_SESSION *session_ptr);
```

### <a name="description"></a><span data-ttu-id="c7c64-1102">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1102">Description</span></span>

<span data-ttu-id="c7c64-1103">Questo servizio cancella una sessione TLS e reimposta lo stato come se la sessione fosse stata appena creata in modo da poter usare nuovamente un oggetto sessione TLS esistente per una nuova sessione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1103">This service clears out a TLS session and resets the state as if the session had just been created so an existing TLS session object can be re-used for a new session.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1104">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1104">Parameters</span></span>

- <span data-ttu-id="c7c64-1105">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1105">**session_ptr** Pointer to a TLS Session instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1106">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1106">Return Values</span></span>

- <span data-ttu-id="c7c64-1107">**NX_SUCCESS** (0x00) Inizializzazione riuscita della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1107">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="c7c64-1108">**NX_INVALID_PARAMETERS** (0x4D) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1108">**NX_INVALID_PARAMETERS** (0x4D) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="c7c64-1109">**NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1109">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1110">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1110">Allowed From</span></span>

<span data-ttu-id="c7c64-1111">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1111">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1112">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1112">Example</span></span>

```C
/* Reset a TLS session.  */
status =  nx_secure_tls_session_reset(&tls_session);


/* If status is NX_SUCCESS the session was successfully reset and may be reused.*/
```

### <a name="see-also"></a><span data-ttu-id="c7c64-1113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1113">See Also</span></span>

- <span data-ttu-id="c7c64-1114">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-1114">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-1115">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1115">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-1116">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-1116">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-1117">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-1117">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="c7c64-1118">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-1118">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="c7c64-1119">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-1119">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="c7c64-1120">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1120">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_send"></a><span data-ttu-id="c7c64-1121">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-1121">nx_secure_tls_session_send</span></span>

<span data-ttu-id="c7c64-1122">Inviare dati tramite una sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-1122">Send data through a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1123">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1123">Prototype</span></span>

```C
UINT  nx_secure_tls_session_send(NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_PACKET *packet_ptr,
                                    ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c7c64-1124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1124">Description</span></span>

<span data-ttu-id="c7c64-1125">Questo servizio invia i dati nel NX_PACKET fornito, usando la sessione TLS attiva specificata e gestendo la crittografia di tali dati prima di inviarli all'host remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1125">This service sends data in the supplied NX_PACKET, using the specified active TLS session, and handling the encryption of that data before sending it to the remote host.</span></span> <span data-ttu-id="c7c64-1126">Se le dimensioni dell'ultima finestra annunciata del ricevitore sono inferiori a questa richiesta, il servizio viene sospeso facoltativamente in base alle opzioni di attesa specificate.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1126">If the receiver's last advertised window size is less than this request, the service optionally suspends based on the wait options specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7c64-1127">*A meno che non venga restituito un errore, l'applicazione non deve rilasciare il pacchetto dopo questa chiamata. Questa operazione causerà risultati imprevedibili perché il driver di rete rilascerà il pacchetto dopo la trasmissione.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-1127">*Unless an error is returned, the application should not release the packet after this call. Doing so will cause unpredictable results because the network driver will release the packet after transmission.*</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1128">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1128">Parameters</span></span>

- <span data-ttu-id="c7c64-1129">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1129">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-1130">**packet_ptr** Puntatore a un pacchetto TLS contenente i dati da inviare.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1130">**packet_ptr** Pointer to a TLS packet containing data to be sent.</span></span>
- <span data-ttu-id="c7c64-1131">**wait_option** Definisce il comportamento del servizio se la richiesta è maggiore delle dimensioni della finestra del ricevitore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1131">**wait_option** Defines how the service behaves if the request is greater than the window size of the receiver.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1132">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1132">Return Values</span></span>

- <span data-ttu-id="c7c64-1133">**NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1133">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="c7c64-1134">**NX_NO_PACKET** (0x01) Nessun dato ricevuto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1134">**NX_NO_PACKET** (0x01) No data received.</span></span>
- <span data-ttu-id="c7c64-1135">**NX_NOT_CONNECTED** (0x38) Il socket TCP sottostante non è più connesso.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1135">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="c7c64-1136">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) L'invio del socket TCP sottostante non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1136">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) The underlying TCP socket send failed.</span></span>
- <span data-ttu-id="c7c64-1137">**NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1137">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="c7c64-1138">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) La sessione TLS fornita non è stata inizializzata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1138">**NX_SECURE_TLS_SESSION_UNINITIALIZED** (0x101) The supplied TLS session was not initialized.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1139">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1139">Allowed From</span></span>

<span data-ttu-id="c7c64-1140">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1140">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1141">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1141">Example</span></span>

```C
/* Send a packet using an active TLS session previously created and started with
nx_secure_tls_session_start. Wait until a packet is sent, blocking otherwise.   */
status =  nx_secure_tls_session_send(&tls_session, &packet_ptr, NX_WAIT_FOREVER);


/* If status is NX_SUCCESS the packet has been sent. */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-1142">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1142">See Also</span></span>

- <span data-ttu-id="c7c64-1143">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-1143">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="c7c64-1144">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-1144">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-1145">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1145">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-1146">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1146">nx_secure_tls_packet_allocate</span></span>
- <span data-ttu-id="c7c64-1147">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-1147">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-1148">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-1148">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="c7c64-1149">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-1149">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="c7c64-1150">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="c7c64-1150">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="c7c64-1151">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1151">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_session_server_callback_set"></a><span data-ttu-id="c7c64-1152">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1152">nx_secure_tls_session_server_callback_set</span></span>

<span data-ttu-id="c7c64-1153">Configurare un callback per TLS da richiamare all'inizio di un handshake del server TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-1153">Set up a callback for TLS to invoke at the beginning of a TLS Server handshake</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1154">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1154">Prototype</span></span>

```C
UINT  nx_secure_tls_ session_server_callback_set (
                 NX_SECURE_TLS_SESSION *tls_session,
                 ULONG (*func_ptr)(NX_SECURE_TLS_SESSION *tls_session,
                                   NX_SECURE_TLS_HELLO_EXTENSION
                                   *extensions, UINT num_extensions));
```

### <a name="description"></a><span data-ttu-id="c7c64-1155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1155">Description</span></span>

<span data-ttu-id="c7c64-1156">Questo servizio assegna un puntatore a funzione a una sessione TLS che TLS richiama quando un handshake del server TLS ha ricevuto un messaggio ClientHello.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1156">This service assigns a function pointer to a TLS session that TLS will invoke when a TLS Server handshake has received a ClientHello message.</span></span> <span data-ttu-id="c7c64-1157">La funzione di callback consente a un'applicazione di elaborare tutte le estensioni TLS dal messaggio ClientHello ricevuto che richiedono input o processo decisionale.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1157">The callback function allows an application to process any TLS extensions from the received ClientHello message that require input or decision making.</span></span>

<span data-ttu-id="c7c64-1158">Il callback viene eseguito con il blocco di controllo della sessione TLS richiamato e una matrice NX_SECURE_TLS_HELLO_EXTENSION oggetti .</span><span class="sxs-lookup"><span data-stu-id="c7c64-1158">The callback is executed with the invoking TLS session control block and an array of NX_SECURE_TLS_HELLO_EXTENSION objects.</span></span> <span data-ttu-id="c7c64-1159">La matrice di oggetti estensione deve essere passata in una funzione helper che troverà e analerà un'estensione specifica.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1159">The array of extension objects is intended to be passed into a helper function that will find and parse a specific extension.</span></span> <span data-ttu-id="c7c64-1160">Per una funzione helper di esempio che analizza le estensioni TLS fornite nei messaggi hello, *vedere nx_secure_tls_session_sni_extension_parse*.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1160">For an example helper function that parses TLS extensions provided in hello messages, see *nx_secure_tls_session_sni_extension_parse*.</span></span>

<span data-ttu-id="c7c64-1161">Il callback del server può essere usato anche per selezionare il certificato di identità attivo *usando nx_secure_tls_active_certificate_set* per il server TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1161">The server callback may also be used to select the active identity certificate using *nx_secure_tls_active_certificate_set* for the TLS Server.</span></span> <span data-ttu-id="c7c64-1162">Ciò si verifica più spesso in risposta a un'estensione Indicazione nome server (SNI) che consente a un client TLS di indicare il server che sta tentando di contattare.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1162">This will most often occur in response to a Server Name Indication (SNI) extension which allows a TLS Client to indicate which server it is attempting to contact.</span></span> <span data-ttu-id="c7c64-1163">Per altre informazioni, *vedere nx_secure_tls_session_sni_extension_parse* e *nx_secure_tls_active_certificate_set* informazioni.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1163">See the references for *nx_secure_tls_session_sni_extension_parse* and *nx_secure_tls_active_certificate_set* for more information.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1164">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1164">Parameters</span></span>

- <span data-ttu-id="c7c64-1165">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1165">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-1166">**func_ptr** Puntatore alla funzione di callback del server TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1166">**func_ptr** Pointer to the TLS Server callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1167">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1167">Return Values</span></span>

- <span data-ttu-id="c7c64-1168">**NX_SUCCESS** (0x00) Corretta allocazione del puntatore a funzione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1168">**NX_SUCCESS** (0x00) Successful allocation of Function pointer.</span></span>
- <span data-ttu-id="c7c64-1169">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1169">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1170">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1170">Allowed From</span></span>

<span data-ttu-id="c7c64-1171">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1171">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1172">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1172">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1173">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1173">See Also</span></span>

- <span data-ttu-id="c7c64-1174">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1174">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-1175">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1175">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="c7c64-1176">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1176">nx_secure_tls_active_certificate_set</span></span>
- <span data-ttu-id="c7c64-1177">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-1177">nx_secure_tls_session_sni_extension_parse</span></span>
- <span data-ttu-id="c7c64-1178">nx_secure_tls_server_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-1178">nx_secure_tls_server_certificate_add</span></span>
- <span data-ttu-id="c7c64-1179">nx_secure_tls_server_certificate_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-1179">nx_secure_tls_server_certificate_find</span></span>

## <a name="nx_secure_tls_session_sni_extension_parse"></a><span data-ttu-id="c7c64-1180">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-1180">nx_secure_tls_session_sni_extension_parse</span></span>

<span data-ttu-id="c7c64-1181">Analizzare un'Indicazione nome server (SNI) ricevuta da un client TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-1181">Parse a Server Name Indication (SNI) extension received from a TLS Client</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1182">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1182">Prototype</span></span>

```C
UINT  nx_secure_tls_session_sni_extension_parse(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_TLS_HELLO_EXTENSION
                                    *extensions,
                                    UINT num_extensions,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a><span data-ttu-id="c7c64-1183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1183">Description</span></span>

<span data-ttu-id="c7c64-1184">Questo servizio deve essere chiamato dall'interno di un callback di sessione del server TLS, aggiunto a una sessione TLS usando nx_secure_tls_session_server_callback_set.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1184">This service is intended to be called from within a TLS Server session callback, added to a TLS session using nx_secure_tls_session_server_callback_set.</span></span> <span data-ttu-id="c7c64-1185">Il callback viene richiamato dopo la ricezione di un messaggio ClientHello da un client TLS remoto e viene fornita una matrice di estensioni disponibili (e il numero di estensioni nella matrice).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1185">The callback is invoked following the reception of a ClientHello message from a remote TLS client and is supplied an array of available extensions (and the number of extensions in the array).</span></span> <span data-ttu-id="c7c64-1186">Tale matrice e la relativa lunghezza possono essere passate direttamente a questa routine per determinare se è presente un'estensione SNI. In caso contrario, viene restituito NX_SECURE_TLS_EXTENSION_NOT_FOUND che indica semplicemente che il client ha scelto di non determinare l'estensione SNI (non si tratta di un errore).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1186">That array and its length can be passed directly to this routine to determine if there is an SNI extension present – if not, NX_SECURE_TLS_EXTENSION_NOT_FOUND is returned indicating simply that the client opted not to provice the SNI extension (this is not an error).</span></span>

<span data-ttu-id="c7c64-1187">Se viene trovata l'estensione SNI, il nome DNS X.509 fornito dal client TLS viene restituito nella dns_name struttura.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1187">If the SNI extension is found, the X.509 DNS name supplied by the TLS client is returned in the dns_name structure.</span></span> <span data-ttu-id="c7c64-1188">Attualmente, l'estensione SNI fornisce solo una singola voce di nome DNS, che può essere usata dal server TLS per determinare quale certificato di identità inviare al client remoto.\*\*</span><span class="sxs-lookup"><span data-stu-id="c7c64-1188">Currently, the SNI extension only supplies a single DNS name entry, which may be used by the TLS server to determine which identity certificate to send to the remote client.\*\*</span></span>

<span data-ttu-id="c7c64-1189">La NX_SECURE_X509_DNS_NAME contiene semplicemente il nome DNS come stringa UCHAR nel campo nx_secure_x509_dns_name e la lunghezza della stringa del nome in *nx_secure_x509_dns_name_length*. </span><span class="sxs-lookup"><span data-stu-id="c7c64-1189">The NX_SECURE_X509_DNS_NAME structure simply contains the DNS name as a UCHAR string in the field *nx_secure_x509_dns_name* and the length of the name string in *nx_secure_x509_dns_name_length*.</span></span> <span data-ttu-id="c7c64-1190">La macro NX_SECURE_X509_DNS_NAME_MAX le dimensioni del buffer nx_secure_x509_dns_name dati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1190">The macro NX_SECURE_X509_DNS_NAME_MAX controls the size of the nx_secure_x509_dns_name buffer.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1191">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1191">Parameters</span></span>

- <span data-ttu-id="c7c64-1192">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1192">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-1193">**estensioni** Puntatore a una matrice di estensioni Hello TLS (dal callback di sessione).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1193">**extensions** Pointer to an array of TLS Hello extensions (from session callback).</span></span>
- <span data-ttu-id="c7c64-1194">**num_extensions** Numero di estensioni nella matrice (dal callback di sessione).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1194">**num_extensions** Number of extensions in array (from session callback).</span></span>
- <span data-ttu-id="c7c64-1195">**dns_name** Restituisce il nome DNS fornito nell'estensione SNI.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1195">**dns_name** Return DNS name supplied in the SNI extension.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1196">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1196">Return Values</span></span>

- <span data-ttu-id="c7c64-1197">**NX_SUCCESS** (0x00) Analisi dell'estensione completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1197">**NX_SUCCESS** (0x00) Successful parsing of the extension.</span></span>
- <span data-ttu-id="c7c64-1198">**NX_PTR_ERROR** (0x07) Matrice di estensioni non valida o puntatore di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1198">**NX_PTR_ERROR** (0x07) Invalid extensions array or TLS session pointer.</span></span>
- <span data-ttu-id="c7c64-1199">**NX_SECURE_TLS_EXTENSION_NOT_FOUND'estensione** SNI 0x136 (0x136) non trovata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1199">**NX_SECURE_TLS_EXTENSION_NOT_FOUND** (0x136) SNI extension not found.</span></span>
- <span data-ttu-id="c7c64-1200">**NX_SECURE_TLS_SNI_EXTENSION_INVALID** formato dell'estensione SNI 0x137 (0x137) non è valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1200">**NX_SECURE_TLS_SNI_EXTENSION_INVALID** (0x137) SNI extension format was invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1201">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1201">Allowed From</span></span>

<span data-ttu-id="c7c64-1202">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1202">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1203">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1203">Example</span></span>

### <a name="see-also"></a><span data-ttu-id="c7c64-1204">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1204">See Also</span></span>

- <span data-ttu-id="c7c64-1205">nx_secure_tls_session_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1205">nx_secure_tls_session_server_callback_set</span></span>
- <span data-ttu-id="c7c64-1206">nx_secure_tls_session_client_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1206">nx_secure_tls_session_client_callback_set</span></span>
- <span data-ttu-id="c7c64-1207">nx_secure_tls_server_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1207">nx_secure_tls_server_callback_set</span></span>
- <span data-ttu-id="c7c64-1208">nx_secure_tls_active_certificate_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1208">nx_secure_tls_active_certificate_set</span></span>

## <a name="nx_secure_tls_session_sni_extension_set"></a><span data-ttu-id="c7c64-1209">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1209">nx_secure_tls_session_sni_extension_set</span></span>

<span data-ttu-id="c7c64-1210">Impostare un nome DNS Indicazione nome server estensione SNI da inviare a un server remoto</span><span class="sxs-lookup"><span data-stu-id="c7c64-1210">Set a Server Name Indication (SNI) extension DNS name to send to a remote Server</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1211">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1211">Prototype</span></span>

```C
UINT  nx_secure_tls_session_sni_extension_set(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    NX_SECURE_X509_DNS_NAME *dns_name);
```

### <a name="description"></a><span data-ttu-id="c7c64-1212">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1212">Description</span></span>

<span data-ttu-id="c7c64-1213">Questo servizio consente a un'applicazione client TLS di fornire un nome DNS del server preferito a un server TLS remoto usando l'estensione TLS Indicazione nome server (SNI).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1213">This service allows a TLS Client application to provide a preferred server DNS name to a remote TLS server using the Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="c7c64-1214">L'estensione SNI consente al server di selezionare il certificato di identità e i parametri corretti in base alle preferenze del server indicate dal client.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1214">The SNI extension allows the server to select the proper identity certificate and parameters based on the client's indicated server preference.</span></span> <span data-ttu-id="c7c64-1215">L'estensione SNI supporta attualmente solo un singolo nome DNS da inviare, quindi il parametro del nome singolare.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1215">The SNI extension currently only supports a single DNS name to be sent, hence the singular name parameter.</span></span> <span data-ttu-id="c7c64-1216">Il dns_name deve essere inizializzato con *nx_secure_x509_dns_name_initialize* e conterrà il server preferito del client.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1216">The dns_name parameter must be initialized with *nx_secure_x509_dns_name_initialize* and will contain the client's preferred server.</span></span> <span data-ttu-id="c7c64-1217">Per annullare l'impostazione del nome dell'estensione, è sufficiente chiamare questo servizio con un valore di parametro "dns_name" di NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1217">To unset the extension name, simply call this service with a "dns_name" parameter value of NX_NULL.</span></span>

<span data-ttu-id="c7c64-1218">La NX_SECURE_X509_DNS_NAME contiene semplicemente il nome DNS come stringa UCHAR nel campo nx_secure_x509_dns_name e la lunghezza della stringa del nome in *nx_secure_x509_dns_name_length*. </span><span class="sxs-lookup"><span data-stu-id="c7c64-1218">The NX_SECURE_X509_DNS_NAME structure simply contains the DNS name as a UCHAR string in the field  *nx_secure_x509_dns_name* and the length of the name string in *nx_secure_x509_dns_name_length*.</span></span> <span data-ttu-id="c7c64-1219">La macro NX_SECURE_X509_DNS_NAME_MAX le dimensioni del buffer nx_secure_x509_dns_name dati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1219">The macro  NX_SECURE_X509_DNS_NAME_MAX controls the size of the nx_secure_x509_dns_name buffer.</span></span>

> [!NOTE]
> <span data-ttu-id="c7c64-1220">*Questa routine deve essere chiamata prima nx_secure_tls_session_start richiamata o clientHello non conterrà l'estensione SNI.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-1220">*This routine must be called before nx_secure_tls_session_start is invoked or the ClientHello will not contain the SNI extension.*</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1221">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1221">Parameters</span></span>

- <span data-ttu-id="c7c64-1222">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1222">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-1223">**dns_name** Nome DNS fornito dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1223">**dns_name** DNS name supplied by the application.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1224">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1224">Return Values</span></span>

- <span data-ttu-id="c7c64-1225">**NX_SUCCESS** (0x00) Aggiunta riuscita del nome del server DNS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1225">**NX_SUCCESS** (0x00) Successful addition of DNS server name.</span></span>
- <span data-ttu-id="c7c64-1226">**NX_PTR_ERROR** (0x07) Nome DNS o puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1226">**NX_PTR_ERROR** (0x07) Invalid DNS name or TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1227">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1227">Allowed From</span></span>

<span data-ttu-id="c7c64-1228">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1228">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1229">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1229">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1230">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1230">See Also</span></span>

- <span data-ttu-id="c7c64-1231">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-1231">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-1232">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-1232">nx_secure_x509_dns_name_initialize</span></span>

## <a name="nx_secure_tls_session_start"></a><span data-ttu-id="c7c64-1233">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-1233">nx_secure_tls_session_start</span></span>

<span data-ttu-id="c7c64-1234">Avviare una sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-1234">Start a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1235">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1235">Prototype</span></span>

```C
UINT  nx_secure_tls_session_start(NX_SECURE_TLS_SESSION *session_ptr,
                                  NX_TCP_SOCKET *tcp_socket_ptr,
                                  ULONG wait_option);
```

### <a name="description"></a><span data-ttu-id="c7c64-1236">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1236">Description</span></span>

<span data-ttu-id="c7c64-1237">Questo servizio avvia una sessione TLS usando il blocco di controllo della sessione TLS fornito e un socket TCP connesso.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1237">This service starts a TLS session using the supplied TLS session control block and a connected TCP socket.</span></span> <span data-ttu-id="c7c64-1238">La connessione TCP deve essere già completata dopo una chiamata riuscita a nx_tcp_client_socket_connect o nx_tcp_server_socket_accept.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1238">The TCP connection must already be complete following a successful call to either nx_tcp_client_socket_connect or nx_tcp_server_socket_accept.</span></span>

<span data-ttu-id="c7c64-1239">Questo servizio determinerà il tipo di sessione TLS (client o server) dal socket TCP.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1239">This service will determine the type of TLS session (Client or Server) from the TCP socket.</span></span>

<span data-ttu-id="c7c64-1240">L'opzione wait definisce il comportamento del servizio mentre è in corso l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1240">The wait option defines how the service behaves while the TLS handshake is in progress.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1241">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1241">Parameters</span></span>

- <span data-ttu-id="c7c64-1242">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1242">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-1243">**tcp_socket_ptr** Puntatore a un socket TCP connesso.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1243">**tcp_socket_ptr** Pointer to a connected TCP socket.</span></span>
- <span data-ttu-id="c7c64-1244">**wait_option** Definisce il comportamento del servizio mentre è in corso l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1244">**wait_option** Defines how the service behaves while the TLS handshake is in progress.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1245">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1245">Return Values</span></span>

- <span data-ttu-id="c7c64-1246">**NX_SUCCESS** (0x00) Inizializzazione della sessione TLS completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1246">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="c7c64-1247">**NX_NOT_CONNECTED** (0x38) Il socket TCP sottostante non è più connesso.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1247">**NX_NOT_CONNECTED** (0x38) The underlying TCP socket is no longer connected.</span></span>
- <span data-ttu-id="c7c64-1248">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) Un tipo di messaggio TLS ricevuto non è corretto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1248">**NX_SECURE_TLS_UNRECOGNIZED_MESSAGE_TYPE** (0x102) A received TLS message type is incorrect.</span></span>
- <span data-ttu-id="c7c64-1249">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) Una crittografia fornita dall'host remoto non è supportata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1249">**NX_SECURE_TLS_UNSUPPORTED_CIPHER** (0x106) A cipher provided by the remote host is not supported.</span></span>
- <span data-ttu-id="c7c64-1250">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) L'elaborazione dei messaggi durante l'handshake TLS non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1250">**NX_SECURE_TLS_HANDSHAKE_FAILURE** (0x107) Message processing during the TLS handshake has failed.</span></span>
- <span data-ttu-id="c7c64-1251">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) Un messaggio in arrivo non ha superato un controllo MAC hash.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1251">**NX_SECURE_TLS_HASH_MAC_VERIFY_FAILURE** (0x108) An incoming message failed a hash MAC check.</span></span>
- <span data-ttu-id="c7c64-1252">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) Un invio di socket TCP sottostante non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1252">**NX_SECURE_TLS_TCP_SEND_FAILED** (0x109) An underlying TCP socket send failed.</span></span>
- <span data-ttu-id="c7c64-1253">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) Un messaggio in arrivo ha un campo di lunghezza non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1253">**NX_SECURE_TLS_INCORRECT_MESSAGE_LENGTH** (0x10A) An incoming message had an invalid length field.</span></span>
- <span data-ttu-id="c7c64-1254">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10B) Un messaggio ChangeCipherSpec in ingresso non è corretto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1254">**NX_SECURE_TLS_BAD_CIPHERSPEC** (0x10B) An incoming ChangeCipherSpec message was incorrect.</span></span>
- <span data-ttu-id="c7c64-1255">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10C) Un certificato TLS in ingresso non è utilizzabile per identificare il server TLS remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1255">**NX_SECURE_TLS_INVALID_SERVER_CERT** (0x10C) An incoming TLS certificate is unusable for identifying the remote TLS server.</span></span>
- <span data-ttu-id="c7c64-1256">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) La crittografia a chiave pubblica fornita dall'host remoto non è supportata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1256">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) The public-key cipher provided by the remote host is unsupported.</span></span>
- <span data-ttu-id="c7c64-1257">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) L'host remoto non ha indicato alcun ciphersuit supportato dallo stack TLS sicuro NetX.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1257">**NX_SECURE_TLS_NO_SUPPORTED_CIPHERS** (0x10E) The remote host has indicated no ciphersuites that are supported by the NetX Secure TLS stack.</span></span>
- <span data-ttu-id="c7c64-1258">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) Un messaggio TLS ricevuto aveva una versione tls sconosciuta nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1258">**NX_SECURE_TLS_UNKNOWN_TLS_VERSION** (0x10F) A received TLS message had an unknown TLS version in its header.</span></span>
- <span data-ttu-id="c7c64-1259">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) Un messaggio TLS ricevuto aveva una versione tls nota ma non supportata nell'intestazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1259">**NX_SECURE_TLS_UNSUPPORTED_TLS_VERSION** (0x110) A received TLS message had a known but unsupported TLS version in its header.</span></span>
- <span data-ttu-id="c7c64-1260">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) Un'allocazione interna di pacchetti TLS non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1260">**NX_SECURE_TLS_ALLOCATE_PACKET_FAILED** (0x111) An internal TLS packet allocation failed.</span></span>
- <span data-ttu-id="c7c64-1261">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) L'host remoto ha fornito un certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1261">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) The remote host provided an invalid certificate.</span></span>
- <span data-ttu-id="c7c64-1262">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) L'host remoto ha inviato un avviso che indica un errore e termina la sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1262">**NX_SECURE_TLS_ALERT_RECEIVED** (0x114) The remote host sent an alert indicating an error and ending the TLS session.</span></span>
- <span data-ttu-id="c7c64-1263">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13B) Una voce nella tabella ciphersuite contiene un puntatore a funzione NULL.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1263">**NX_SECURE_TLS_MISSING_CRYPTO_ROUTINE** (0x13B) An entry in the ciphersuite table had a NULL function pointer.</span></span>
- <span data-ttu-id="c7c64-1264">**NX_SECURE_TLS_INAPPROPRIATE_FALLBACK** (0x146) Un client TLS remotoHello include lo scSV di fallback e tenta un fallback della versione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1264">**NX_SECURE_TLS_INAPPROPRIATE_FALLBACK** (0x146) A remote TLS ClientHello included the fallback SCSV andattempted a version fallback.</span></span>
- <span data-ttu-id="c7c64-1265">**NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1265">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1266">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1266">Allowed From</span></span>

<span data-ttu-id="c7c64-1267">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1267">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1268">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1268">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1269">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1269">See Also</span></span>

- <span data-ttu-id="c7c64-1270">nx_tcp_socket_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-1270">nx_tcp_socket_receive</span></span>
- <span data-ttu-id="c7c64-1271">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-1271">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-1272">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1272">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-1273">nx_secure_tls_session_send</span><span class="sxs-lookup"><span data-stu-id="c7c64-1273">nx_secure_tls_session_send</span></span>
- <span data-ttu-id="c7c64-1274">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-1274">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="c7c64-1275">nx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-1275">nx_secure_tls_session_receive</span></span>
- <span data-ttu-id="c7c64-1276">nx_secure_tls_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1276">nx_secure_tls_packet_allocate</span></span>
- <span data-ttu-id="c7c64-1277">nx_secure_tls_session_end</span><span class="sxs-lookup"><span data-stu-id="c7c64-1277">nx_secure_tls_session_end</span></span>
- <span data-ttu-id="c7c64-1278">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1278">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-1279">nx_tcp_socket_accept</span><span class="sxs-lookup"><span data-stu-id="c7c64-1279">nx_tcp_socket_accept</span></span>
- <span data-ttu-id="c7c64-1280">nx_tcp_socket_listen</span><span class="sxs-lookup"><span data-stu-id="c7c64-1280">nx_tcp_socket_listen</span></span>
- <span data-ttu-id="c7c64-1281">nx_tcp_socket_disconnect</span><span class="sxs-lookup"><span data-stu-id="c7c64-1281">nx_tcp_socket_disconnect</span></span>
- <span data-ttu-id="c7c64-1282">nx_tcp_socket_unaccept</span><span class="sxs-lookup"><span data-stu-id="c7c64-1282">nx_tcp_socket_unaccept</span></span>
- <span data-ttu-id="c7c64-1283">nx_tcp_socket_relisten</span><span class="sxs-lookup"><span data-stu-id="c7c64-1283">nx_tcp_socket_relisten</span></span>
- <span data-ttu-id="c7c64-1284">nx_tcp_socket_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-1284">nx_tcp_socket_delete</span></span>
- <span data-ttu-id="c7c64-1285">nx_packet_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1285">nx_packet_allocate</span></span>
- <span data-ttu-id="c7c64-1286">nx_packet_data_append</span><span class="sxs-lookup"><span data-stu-id="c7c64-1286">nx_packet_data_append</span></span>
- <span data-ttu-id="c7c64-1287">nx_packet_data_extract_offset</span><span class="sxs-lookup"><span data-stu-id="c7c64-1287">nx_packet_data_extract_offset</span></span>

## <a name="nx_secure_tls_session_time_function_set"></a><span data-ttu-id="c7c64-1288">nx_secure_tls_session_time_function_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1288">nx_secure_tls_session_time_function_set</span></span>

<span data-ttu-id="c7c64-1289">Assegnare una funzione timestamp a una sessione TLS sicura netx</span><span class="sxs-lookup"><span data-stu-id="c7c64-1289">Assign a timestamp function to a NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1290">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1290">Prototype</span></span>

```C
UINT  nx_secure_tls_time_function_set(
                              NX_SECURE_TLS_SESSION *session_ptr,
                              ULONG (*time_func_ptr)(void));
```

### <a name="description"></a><span data-ttu-id="c7c64-1291">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1291">Description</span></span>

<span data-ttu-id="c7c64-1292">Questa funzione configura un puntatore a funzione che TLS richiama quando deve ottenere l'ora corrente, usata in vari messaggi di handshake TLS e per la verifica dei certificati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1292">This function sets up a function pointer that TLS will invoke when it needs to get the current time, which is used in various TLS handshake messages and for verification of certificates.</span></span>

<span data-ttu-id="c7c64-1293">È previsto che la funzione restituisca il GMT corrente in formato UNIX a 32 bit (secondi a partire dalla mezzanotte del 1° gennaio 1970 UTC, ignorando i secondi intercalare), in base ai requisiti clientHello nella RFC 5246 tls.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1293">The function is expected to return the current GMT in UNIX 32-bit format (seconds since the midnight starting Jan 1, 1970, UTC, ignoring leap seconds), as per the ClientHello requirements in the TLS RFC 5246.</span></span>

<span data-ttu-id="c7c64-1294">Se non viene assegnata alcuna funzione timestamp, verrà usato il valore 0 per il timestamp nell'handshake TLS e il controllo della scadenza del certificato non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1294">If no timestamp function is assigned, a value of 0 for the timestamp in the TLS handshake will be used and certificate expiration checking will not work.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1295">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1295">Parameters</span></span>

- <span data-ttu-id="c7c64-1296">**session_ptr** Puntatore a un'istanza di sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1296">**session_ptr** Pointer to a TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-1297">**time_func_ptr** Puntatore a una funzione che restituisce l'ora corrente (GMT) in formato UNIX a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1297">**time_func_ptr** Pointer to a function that returns the current time (GMT) in UNIX 32-bit format.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1298">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1298">Return Values</span></span>

- <span data-ttu-id="c7c64-1299">**NX_SUCCESS** (0x00) Inizializzazione riuscita della sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1299">**NX_SUCCESS** (0x00) Successful initialization of the TLS session.</span></span>
- <span data-ttu-id="c7c64-1300">**NX_INVALID_PARAMETERS** (0x4D) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1300">**NX_INVALID_PARAMETERS** (0x4D) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="c7c64-1301">**NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1301">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1302">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1302">Allowed From</span></span>

<span data-ttu-id="c7c64-1303">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1303">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1304">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1304">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1305">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1305">See Also</span></span>

- <span data-ttu-id="c7c64-1306">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-1306">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-1307">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1307">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-1308">nx_secure_tls_session_start</span><span class="sxs-lookup"><span data-stu-id="c7c64-1308">nx_secure_tls_session_start</span></span>
- <span data-ttu-id="c7c64-1309">nx_secure_tls_session_delete</span><span class="sxs-lookup"><span data-stu-id="c7c64-1309">nx_secure_tls_session_delete</span></span>
- <span data-ttu-id="c7c64-1310">nx_secure_tls_session_sendnx_secure_tls_session_receive</span><span class="sxs-lookup"><span data-stu-id="c7c64-1310">nx_secure_tls_session_sendnx_secure_tls_session_receive</span></span>
- <span data-ttu-id="c7c64-1311">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1311">nx_secure_tls_session_create</span></span>

## <a name="nx_secure_tls_trusted_certificate_add"></a><span data-ttu-id="c7c64-1312">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-1312">nx_secure_tls_trusted_certificate_add</span></span>

<span data-ttu-id="c7c64-1313">Aggiungere un certificato attendibile alla sessione TLS sicura di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-1313">Add trusted certificate to NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1314">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1314">Prototype</span></span>

```C
UINT  nx_secure_tls_trusted_certificate_add(NX_SECURE_TLS_SESSION
                            *session_ptr, NX_SECURE_X509_CERT *certificate_ptr);
```

### <a name="description"></a><span data-ttu-id="c7c64-1315">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1315">Description</span></span>

<span data-ttu-id="c7c64-1316">Questo servizio aggiunge un'istanza NX_SECURE_X509_CERT a una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1316">This service adds an initialized NX_SECURE_X509_CERT structure instance to a TLS session.</span></span> <span data-ttu-id="c7c64-1317">Questo certificato viene usato dallo stack TLS per verificare i certificati forniti dall'host remoto durante l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1317">This certificate is used by the TLS stack to verify certificates supplied by the remote host during the TLS handshake.</span></span>

<span data-ttu-id="c7c64-1318">I certificati attendibili sono necessari per la modalità client TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1318">Trusted certificates are required for TLS Client mode.</span></span>

<span data-ttu-id="c7c64-1319">I certificati attendibili sono necessari solo per la modalità server TLS se è abilitata l'autenticazione del certificato client.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1319">Trusted certificates are only required for TLS Server mode if client certificate authentication is enabled.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1320">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1320">Parameters</span></span>

- <span data-ttu-id="c7c64-1321">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1321">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-1322">**certificate_ptr** Puntatore a un'istanza del certificato TLS inizializzata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1322">**certificate_ptr** Pointer to an initialized TLS Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1323">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1323">Return Values</span></span>

- <span data-ttu-id="c7c64-1324">**NX_SUCCESS** (0x00) Aggiunta del certificato completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1324">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="c7c64-1325">**NX_INVALID_PARAMETERS** (0x4D) Tentativo di aggiungere un certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1325">**NX_INVALID_PARAMETERS** (0x4D) Tried to add an invalid certificate.</span></span>
- <span data-ttu-id="c7c64-1326">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1326">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1327">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1327">Allowed From</span></span>

<span data-ttu-id="c7c64-1328">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1328">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1329">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1329">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1330">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1330">See Also</span></span>

- <span data-ttu-id="c7c64-1331">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-1331">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-1332">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1332">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-1333">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1333">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-1334">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-1334">nx_secure_tls_trusted_certificate_remove</span></span>

## <a name="nx_secure_tls_trusted_certificate_remove"></a><span data-ttu-id="c7c64-1335">nx_secure_tls_trusted_certificate_remove</span><span class="sxs-lookup"><span data-stu-id="c7c64-1335">nx_secure_tls_trusted_certificate_remove</span></span>

<span data-ttu-id="c7c64-1336">Rimuovere un certificato attendibile dalla sessione TLS protetta di NetX</span><span class="sxs-lookup"><span data-stu-id="c7c64-1336">Remove trusted certificate from NetX Secure TLS Session</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1337">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1337">Prototype</span></span>

```C
UINT  nx_secure_tls_trusted_certificate_remove(
                                    NX_SECURE_TLS_SESSION *session_ptr,
                                    UCHAR *common_name,
                                    UINT common_name_length);
```

### <a name="description"></a><span data-ttu-id="c7c64-1338">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1338">Description</span></span>

<span data-ttu-id="c7c64-1339">Questo servizio rimuove un certificato attendibile da una sessione TLS, con chiave nel campo Nome comune nel certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1339">This service removes a trusted certificate from a TLS session, keyed on the Common Name field in the certificate.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1340">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1340">Parameters</span></span>

- <span data-ttu-id="c7c64-1341">**session_ptr** Puntatore a un'istanza di sessione TLS creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1341">**session_ptr** Pointer to a previously created TLS Session instance.</span></span>
- <span data-ttu-id="c7c64-1342">**common_name** Valore common name del certificato da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1342">**common_name** The Common Name value of the certificate to be removed.</span></span>
- <span data-ttu-id="c7c64-1343">**common_name_length** Lunghezza della stringa Common Name.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1343">**common_name_length** The length of the Common Name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1344">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1344">Return Values</span></span>

- <span data-ttu-id="c7c64-1345">**NX_SUCCESS** (0x00) Aggiunta del certificato completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1345">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="c7c64-1346">**NX_PTR_ERROR** (0x07) Puntatore di sessione TLS non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1346">**NX_PTR_ERROR** (0x07) Invalid TLS session pointer.</span></span>
- <span data-ttu-id="c7c64-1347">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** certificato (0x119) non trovato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1347">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) Certificate was not found.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1348">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1348">Allowed From</span></span>

<span data-ttu-id="c7c64-1349">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1349">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1350">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1350">Example</span></span>

```C
/* Remove certificate from TLS session.  */
status =  nx_secure_tls_trusted_certificate_remove(&tls_session,
                                                “www.example.com”, 15);


/* If status is NX_SUCCESS the certificate was successfully removed.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-1351">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1351">See Also</span></span>

- <span data-ttu-id="c7c64-1352">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-1352">nx_secure_x509_certificate_initialize</span></span>
- <span data-ttu-id="c7c64-1353">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1353">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-1354">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1354">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-1355">nx_secure_tls_trusted_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-1355">nx_secure_tls_trusted_certificate_add</span></span>

## <a name="nx_secure_x509_certificate_initialize"></a><span data-ttu-id="c7c64-1356">nx_secure_x509_certificate_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-1356">nx_secure_x509_certificate_initialize</span></span>

<span data-ttu-id="c7c64-1357">Inizializzare il certificato X.509 per NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-1357">Initialize X.509 Certificate for NetX Secure TLS</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1358">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1358">Prototype</span></span>

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

### <a name="description"></a><span data-ttu-id="c7c64-1359">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1359">Description</span></span>

<span data-ttu-id="c7c64-1360">Questo servizio inizializza una struttura NX_SECURE_X509_CERT da un certificato digitale X.509 con codifica binaria da usare in una sessione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1360">This service initializes an NX_SECURE_X509_CERT structure from a binary-encoded X.509 digital certificate for use in a TLS session.</span></span>

<span data-ttu-id="c7c64-1361">I dati del **certificato devono** essere un certificato digitale X.509 valido in formato binario con codifica DER.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1361">The certificate data **must** be a valid X.509 digital certificate in DER-encoded binary format.</span></span> <span data-ttu-id="c7c64-1362">I dati possono essere da qualsiasi origine (ad esempio, file system, buffer costante compilato e così via) purché sia fornito un puntatore UCHAR a tale dati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1362">The data can some from any source (e.g. file system, compiled constant buffer, etc.) as long as a UCHAR pointer to that data is provided.</span></span>

<span data-ttu-id="c7c64-1363">Il *raw_data_buffer* e le relative dimensioni sono parametri facoltativi che specificano un buffer dedicato in cui i dati del certificato vengono copiati prima dell'analisi.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1363">The *raw_data_buffer* parameter and its size are optional parameters that specify a dedicated buffer into which the certificate data is copied before parsing.</span></span> <span data-ttu-id="c7c64-1364">Se raw_data_buffer viene passato come NX_NULL, la struttura NX_SECURE_X509_CERT punti direttamente alla matrice certificate_data (in questo caso buffer_size viene ignorata).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1364">If raw_data_buffer is passed as NX_NULL then the NX_SECURE_X509_CERT structure will point directly into the certificate_data array (buffer_size is ignored in this case).</span></span> <span data-ttu-id="c7c64-1365">Se raw_data_buffer viene passato come ***NX_NULL,*** non modificare i dati a cui punta il puntatore certificate_data o l'elaborazione del certificato avrà probabilmente esito negativo.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1365">If raw_data_buffer is passed as NX_NULL, ***do not*** modify the data pointed to by the certificate_data pointer or certificate processing will likely fail!</span></span>

<span data-ttu-id="c7c64-1366">Il parametro della chiave privata è per i certificati di identità locali: la chiave privata viene usata dai server per decrittografare i dati della chiave in ingresso da un client (crittografati con la chiave pubblica del server) e dai client per verificare la propria identità a un server quando il server richiede un certificato client.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1366">The private key parameter is for local identity certificates – the private key is used by servers to decrypt the incoming key data from a client (encrypted using the server's public key) and by clients to verify their identity to a server when the server requests a client certificate.</span></span> <span data-ttu-id="c7c64-1367">L'aggiunta di una chiave privata con questa API contrassegnerà automaticamente il certificato associato come certificato di identità per un'applicazione TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1367">Adding a private key with this API will automatically mark the associated certificate as being an identity certificate for a TLS application.</span></span> <span data-ttu-id="c7c64-1368">Quando si inizializzano i certificati per altri scopi (ad esempio, l'archivio attendibile), il parametro *private_key_data* deve essere passato come NULL, il *private_key_data_length* come 0 e il *private_key_type* deve essere passato come NX_SECURE_X509_KEY_TYPE_NONE.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1368">When initializing certificates for other purposes (e.g. the trusted store), the *private_key_data* parameter should be passed as NULL, the *private_key_data_length* as 0, and the *private_key_type* should be passed as NX_SECURE_X509_KEY_TYPE_NONE.</span></span>

<span data-ttu-id="c7c64-1369">Il *private_key_type* parametro indica la formattazione della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1369">The *private_key_type* parameter indicates the formatting of the private key.</span></span> <span data-ttu-id="c7c64-1370">Ad esempio, se la chiave privata è una chiave privata RSA in formato PKCS#1 con codifica DER, il private_key_type deve essere passato come NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER, un tipo noto a NetX Secure che verrà analizzato immediatamente e salvato per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1370">For example, if the private key is a DER-encoded PKCS#1-format RSA private key, the private_key_type should be passed as NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER, a type known to NetX Secure which will be parsed immediately and saved for later use.</span></span>

<span data-ttu-id="c7c64-1371">Il private_key_type supporta anche i tipi di chiave definiti dall'utente<sup>23</sup> per piattaforme e applicazioni con formati di chiave specifici o altre esigenze.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1371">The private_key_type also supports user-defined key types<sup>23</sup> for platforms and applications that have specific key formats or other needs.</span></span> <span data-ttu-id="c7c64-1372">Ad esempio, un motore di crittografia basato su hardware può usare un formato specifico non riconosciuto dal software NetX Secure oppure una chiave privata può essere crittografata o rappresentata da un token di crittografia, come nel caso di un hardware crittografico Trusted Platform Module (TPM) o PKCS#11.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1372">For example, a hardware-based encryption engine may use a specific format not understood by the NetX Secure software, or a private key may be encrypted or represented by a cryptographic token as might be the case with a Trusted Platform Module (TPM) or PKCS#11 cryptographic hardware.</span></span> <span data-ttu-id="c7c64-1373">Quando si usa un tipo di chiave definito dall'utente, i dati della chiave vengono passati verbatim alla routine crittografica appropriata, ad esempio una chiave privata RSA verrebbe passata, senza alcuna analisi o elaborazione, direttamente alla routine crittografica RSA fornita a TLS nella tabella ciphersuite.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1373">When a user-defined key type is used, the key data is passed verbatim to the appropriate cryptographic routine - for example, an RSA private key would be passed, without any parsing or processing, directly to the RSA cryptographic routine provided to TLS in the ciphersuite table.</span></span> <span data-ttu-id="c7c64-1374">Il tipo di chiave definito dall'utente viene passato anche alla routine crittografica (nel caso di RSA, questo è il parametro "op").</span><span class="sxs-lookup"><span data-stu-id="c7c64-1374">The user-defined key type is also passed to the cryptographic routine (in the case of RSA, this is the "op" parameter).</span></span>

<span data-ttu-id="c7c64-1375">L'intervallo di chiavi definite dall'utente copre la metà superiore di un intero senza segno a 32 bit, 0x0001 0000-0xFFFF FFFF.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1375">The range of user-defined keys covers the top half of a 32-bit unsigned integer, from 0x0001 0000-0xFFFF FFFF.</span></span> <span data-ttu-id="c7c64-1376">I valori inferiori 0x0001 0000 sono riservati per l'uso di NetX Secure.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1376">Values less than 0x0001 0000 are reserved for NetX Secure use.</span></span>

<span data-ttu-id="c7c64-1377">I tipi di chiave definiti dall'utente sono una funzionalità avanzata che richiede routine crittografiche personalizzate per gestire i dati della chiave privata non elaborati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1377">User-defined key types are an advanced feature that requires custom cryptographic routines to handle the raw private key data.</span></span> <span data-ttu-id="c7c64-1378">Per informazioni su questa funzionalità, contattare il rappresentante di Express Logic.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1378">Please contact your Express Logic representative if you have need of this feature.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1379">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1379">Parameters</span></span>

- <span data-ttu-id="c7c64-1380">**certificate_ptr** Puntatore a un'istanza del certificato X.509 non inizializzata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1380">**certificate_ptr** Pointer to an uninitialized X.509 Certificate instance.</span></span>
- <span data-ttu-id="c7c64-1381">**certificate_data** Puntatore ai dati binari X.509 con codifica DER.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1381">**certificate_data** Pointer to DER-encoded X.509 binary data.</span></span>
- <span data-ttu-id="c7c64-1382">**raw_data_buffer** Puntatore al buffer dei dati del certificato dedicato facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1382">**raw_data_buffer** Pointer to optional dedicated certificate data buffer.</span></span>
- <span data-ttu-id="c7c64-1383">**buffer_size** Dimensioni del buffer dei dati del certificato dedicato facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1383">**buffer_size** Size of optional dedicated certificate data buffer.</span></span>
- <span data-ttu-id="c7c64-1384">**certificate_data_length** Lunghezza in byte dei dati binari del certificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1384">**certificate_data_length** Length of certificate binary data in bytes.</span></span>
- <span data-ttu-id="c7c64-1385">**private_key_data** Puntatore ai dati facoltativi della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1385">**private_key_data** Pointer to optional private key data.</span></span>
- <span data-ttu-id="c7c64-1386">**private_key_data_length** Lunghezza dei dati della chiave privata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1386">**private_key_data_length** Length of private key data.</span></span>
- <span data-ttu-id="c7c64-1387">**private_key_type** Identificatore del tipo di chiave.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1387">**private_key_type** Key type identifier.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1388">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1388">Return Values</span></span>

- <span data-ttu-id="c7c64-1389">**NX_SUCCESS** (0x00) Aggiunta del certificato completata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1389">**NX_SUCCESS** (0x00) Successful addition of certificate.</span></span>
- <span data-ttu-id="c7c64-1390">**NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1390">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>
- <span data-ttu-id="c7c64-1391">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) I dati del certificato non contengono un certificato X.509 con codifica DER.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1391">**NX_SECURE_TLS_INVALID_CERTIFICATE** (0x112) Certificate data did not contain a DER-encoded X.509 certificate.</span></span>
- <span data-ttu-id="c7c64-1392">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** certificato (0x10D) non dispone di una crittografia a chiave pubblica supportata da NetX Secure.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1392">**NX_SECURE_TLS_UNSUPPORTED_PUBLIC_CIPHER** (0x10D) Certificate did not have a public-key cipher that is supported by NetX Secure.</span></span>
- <span data-ttu-id="c7c64-1393">**NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE** chiave privata (0x186) o certificato non contiene una sequenza ASN.1 valida.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1393">**NX_SECURE_X509_INVALID_CERTIFICATE_SEQUENCE** (0x186) Private key or certificate did not contain a valid ASN.1 sequence.</span></span>
- <span data-ttu-id="c7c64-1394">**NX_SECURE_PKCS1_INVALID_PRIVATE_KEY** (0x18A) La chiave privata specificata non è una chiave RSA PKCS#1 valida.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1394">**NX_SECURE_PKCS1_INVALID_PRIVATE_KEY** (0x18A) The provided private key was not a valid PKCS#1 RSA key.</span></span>
- <span data-ttu-id="c7c64-1395">**NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE** (0x19D) Il tipo di chiave privata specificato non è definito dall'utente e non corrisponde ad alcun tipo noto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1395">**NX_SECURE_X509_INVALID_PRIVATE_KEY_TYPE** (0x19D) The private key type provided was not user-defined and did not match any known type.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1396">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1396">Allowed From</span></span>

<span data-ttu-id="c7c64-1397">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1397">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1398">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1398">Example</span></span>

```C
/* Initialize certificate structure. The certificate structure will point directly
   into the certificate_data array since we are passing the raw_data_buffer as
   NX_NULL. This certificate has a private key so it will be used to identify this
   device. */
status =  nx_secure_x509_certificate_initialize(&certificate, certificate_data,
500, NX_NULL, 0, private_key, 64, NX_SECURE_X509_KEY_TYPE_RSA_PKCS1_DER);


/* If status is NX_SUCCESS the certificate was successfully initialized.  */
```

### <a name="see-also"></a><span data-ttu-id="c7c64-1399">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1399">See Also</span></span>

- <span data-ttu-id="c7c64-1400">nx_secure_local_certificate_add</span><span class="sxs-lookup"><span data-stu-id="c7c64-1400">nx_secure_local_certificate_add</span></span>
- <span data-ttu-id="c7c64-1401">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1401">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-1402">nx_secure_tls_remote_certificate_allocate</span><span class="sxs-lookup"><span data-stu-id="c7c64-1402">nx_secure_tls_remote_certificate_allocate</span></span>
- <span data-ttu-id="c7c64-1403">Importazione di certificati X.509 in NetX Secure nel capitolo 3.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1403">Importing X.509 Certificates into NetX Secure in Chapter 3.</span></span>

## <a name="nx_secure_x509_common_name_dns_check"></a><span data-ttu-id="c7c64-1404">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-1404">nx_secure_x509_common_name_dns_check</span></span>

<span data-ttu-id="c7c64-1405">Controllare il nome DNS rispetto al certificato X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-1405">Check DNS name against X.509 Certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1406">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1406">Prototype</span></span>

```C
UINT  nx_secure_x509_common_name_dns_check(
                        NX_SECURE_X509_CERT *certificate,
                        const UCHAR *dns_tld, UINT dns_tld_length);
```

### <a name="description"></a><span data-ttu-id="c7c64-1407">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1407">Description</span></span>

<span data-ttu-id="c7c64-1408">Questo servizio controlla il nome comune di un certificato rispetto a un nome di dominio principale (TLD) fornito dal chiamante ai fini della convalida DNS di un host remoto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1408">This service checks a certificate's Common Name against a Top- Domain name (TLD) provided by the caller for the purposes of DNS validation of a remote host.</span></span> <span data-ttu-id="c7c64-1409">Questa funzione di utilità deve essere chiamata dall'interno di una routine di callback di convalida del certificato fornita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1409">This utility function is intended to be called from within a certificate validation callback routine provided by the application.</span></span> <span data-ttu-id="c7c64-1410">Il nome TLD deve essere la parte superiore dell'URL usato per accedere all'host remoto (il "." -separated string before the first slash).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1410">The TLD name should be the top part of the URL used to access the remote host (the "."-separated string before the first slash).</span></span> <span data-ttu-id="c7c64-1411">Se il nome comune contiene un carattere jolly , ad esempio .example.com, il carattere jolly corrisponderà a qualsiasi con *lo stesso suffisso. Si* noti che solo il primo carattere jolly (" ") rilevato (lettura da destra a sinistra) verrà considerato  per la corrispondenza con caratteri jolly, ad esempio abc.\*.example.com corrisponderà a qualsiasi nome che termina con ".example.com".</span><span class="sxs-lookup"><span data-stu-id="c7c64-1411">If the Common Name contains a wildcard (such as *.example.com), the wildcard will match any with the same suffix. Note that only the first wildcard ("*") encountered (reading right-to-left) will be considered for wildcard matching – for example, abc.\*.example.com will match *any* name ending in ".example.com".</span></span>

<span data-ttu-id="c7c64-1412">Se il nome comune non corrisponde alla stringa fornita, viene analizzata l'estensione "subjectAltName" (se presente nel certificato) e vengono confrontate anche le voci DNSName.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1412">If the Common Name does not match the provided string, the "subjectAltName" extension is parsed (if it exists in the certificate) and any DNSName entries are also compared.</span></span> <span data-ttu-id="c7c64-1413">Se nessuna di queste voci corrisponde, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1413">If none of those entries match, an error is returned.</span></span>

<span data-ttu-id="c7c64-1414">È importante comprendere il formato del nome comune (e delle voci subjectAltName) nei certificati previsti.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1414">It is important to understand the format of the common name (and subjectAltName entries) in expected certificates.</span></span> <span data-ttu-id="c7c64-1415">Ad esempio, alcuni certificati possono usare un indirizzo IP non elaborato o un carattere jolly.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1415">For example, some certificates may use a raw IP address or a wild card.</span></span> <span data-ttu-id="c7c64-1416">La stringa DNS TLD deve essere formattata in modo che corrisponda ai valori previsti nei certificati ricevuti.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1416">The DNS TLD string must be formatted such that it will match the expected values in received certificates.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1417">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1417">Parameters</span></span>

- <span data-ttu-id="c7c64-1418">**certificate_ptr** Puntatore a un'istanza del certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1418">**certificate_ptr** Pointer to an X.509 Certificate instance.</span></span>
- <span data-ttu-id="c7c64-1419">**dns_tld** Top-Level nome di dominio con cui eseguire il confronto.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1419">**dns_tld** Top-Level Domain name to compare against.</span></span>
- <span data-ttu-id="c7c64-1420">**dns_tld_length** Lunghezza della stringa TLD.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1420">**dns_tld_length** Length of TLD string.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1421">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1421">Return Values</span></span>

- <span data-ttu-id="c7c64-1422">**NX_SUCCESS** (0x00) Confronto riuscito con nome comune o subjectAltName.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1422">**NX_SUCCESS** (0x00) Successful comparison with Common Name or subjectAltName.</span></span>
- <span data-ttu-id="c7c64-1423">**NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH** (0x195) Nessun nome corrispondente trovato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1423">**NX_SECURE_X509_CERTIFICATE_DNS_MISMATCH** (0x195) No matching name found.</span></span>
- <span data-ttu-id="c7c64-1424">**NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1424">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1425">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1425">Allowed From</span></span>

<span data-ttu-id="c7c64-1426">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1426">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1427">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1427">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1428">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1428">See Also</span></span>

- <span data-ttu-id="c7c64-1429">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1429">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-1430">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1430">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="c7c64-1431">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-1431">nx_secure_x509_crl_revocation_check</span></span>

## <a name="nx_secure_x509_crl_revocation_check"></a><span data-ttu-id="c7c64-1432">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-1432">nx_secure_x509_crl_revocation_check</span></span>

<span data-ttu-id="c7c64-1433">Controllare il certificato X.509 rispetto a un elenco di revoche di certificati (CRL) fornito</span><span class="sxs-lookup"><span data-stu-id="c7c64-1433">Check X.509 Certificate against a supplied Certificate Revocation List (CRL)</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1434">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1434">Prototype</span></span>

```C
UINT  nx_secure_x509_crl_revocation_check(const UCHAR *crl_data,
                              UINT crl_length,
                              NX_SECURE_X509_CERTIFICATE_STORE *store,
                              NX_SECURE_X509_CERT *certificate);
```

### <a name="description"></a><span data-ttu-id="c7c64-1435">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1435">Description</span></span>

<span data-ttu-id="c7c64-1436">Questo servizio accetta un elenco di revoche di certificati con codifica DER e cerca un certificato specifico in tale elenco.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1436">This service takes a DER-encoded Certificate Revocation List and searches for a specific certificate in that list.</span></span> <span data-ttu-id="c7c64-1437">L'autorità di certificazione del CRL viene convalidata rispetto a un archivio certificati fornito, l'autorità di certificazione CRL viene convalidata in modo che sia uguale a quella per il certificato controllato e il numero di serie del certificato in questione viene usato per cercare l'elenco di certificati revocati.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1437">The issuer of the CRL is validated against a supplied certificate store, the CRL issuer is validated to be the same as the one for the certificate being checked, and the serial number of the certificate in question is used to search the revoked certificates list.</span></span> <span data-ttu-id="c7c64-1438">Se le autorità di certificazione corrispondono, la  firma viene esere e il certificato non è presente nell'elenco, la chiamata ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1438">If the issuers match, the signature checks out, and the certificate is **not** present in the list, the call is successful.</span></span> <span data-ttu-id="c7c64-1439">In tutti gli altri casi viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1439">All other cases cause an error to be returned.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1440">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1440">Parameters</span></span>

- <span data-ttu-id="c7c64-1441">**crl_data** Puntatore a un CRL con codifica DER.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1441">**crl_data** Pointer to a DER-encoded CRL.</span></span>
- <span data-ttu-id="c7c64-1442">**crl_length** Lunghezza in byte dei dati CRL.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1442">**crl_length** Length in bytes of CRL data.</span></span>
- <span data-ttu-id="c7c64-1443">**store** Puntatore a un archivio certificati X.509.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1443">**store** Pointer to an X.509 Certificate store.</span></span>
- <span data-ttu-id="c7c64-1444">**certificate_ptr** Puntatore a un'istanza del certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1444">**certificate_ptr** Pointer to an X.509 Certificate instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1445">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1445">Return Values</span></span>

- <span data-ttu-id="c7c64-1446">**NX_SUCCESS** (0x00) Convalida riuscita che il certificato non è stato revocato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1446">**NX_SUCCESS** (0x00) Successful validation that the certificate was not revoked.</span></span>
- <span data-ttu-id="c7c64-1447">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** certificato dell'autorità di certificazione CRL (0x119) non trovato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1447">**NX_SECURE_TLS_CERTIFICATE_NOT_FOUND** (0x119) CRL issuer certificate not found.</span></span>
- <span data-ttu-id="c7c64-1448">**NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND** 0x11B) Certificato dell'autorità di certificazione non trovato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1448">**NX_SECURE_TLS_ISSUER_CERTIFICATE_NOT_FOUND** 0x11B) Certificate issuer certificate not found.</span></span>
- <span data-ttu-id="c7c64-1449">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) L'ASN.1 CRL contiene un campo di lunghezza non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1449">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) The CRL ASN.1 contained an invalid length field.</span></span>
- <span data-ttu-id="c7c64-1450">**NX_SECURE_X509_UNEXPECTED_ASN1_TAG(0x189)** L'elenco CRL contiene un ASN.1 non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1450">**NX_SECURE_X509_UNEXPECTED_ASN1_TAG(0x189)** The CRL contained invalid ASN.1.</span></span>
- <span data-ttu-id="c7c64-1451">**NX_SECURE_X509_CHAIN_VERIFY_FAILURE** (0x18C) Verifica della catena di certificati non riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1451">**NX_SECURE_X509_CHAIN_VERIFY_FAILURE** (0x18C) A certificate chain verification failed.</span></span>
- <span data-ttu-id="c7c64-1452">**NX_SECURE_X509_CRL_ISSUER_MISMATCH(0x197)** CRL e autorità di certificazione non corrispondono.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1452">**NX_SECURE_X509_CRL_ISSUER_MISMATCH** (0x197) CRL and certificate issuers did not match.</span></span>
- <span data-ttu-id="c7c64-1453">**NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED** 0x198) La firma CRL non è valida.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1453">**NX_SECURE_X509_CRL_SIGNATURE_CHECK_FAILED** 0x198) The CRL signature was invalid.</span></span>
- <span data-ttu-id="c7c64-1454">**NX_SECURE_X509_CRL_CERTIFICATE_REVOKED** (0x199) Il certificato controllato è stato trovato nell'elenco CRL e pertanto viene revocato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1454">**NX_SECURE_X509_CRL_CERTIFICATE_REVOKED** (0x199) The certificate being checked was found in the CRL and is therefore revoked.</span></span>
- <span data-ttu-id="c7c64-1455">**NX_PTR_ERROR** (0x07) Ha tentato di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1455">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1456">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1456">Allowed From</span></span>

<span data-ttu-id="c7c64-1457">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1457">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1458">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1458">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1459">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1459">See Also</span></span>

- <span data-ttu-id="c7c64-1460">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1460">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-1461">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1461">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="c7c64-1462">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-1462">nx_secure_x509_common_name_dns_check</span></span>

## <a name="nx_secure_x509_dns_name_initialize"></a><span data-ttu-id="c7c64-1463">nx_secure_x509_dns_name_initialize</span><span class="sxs-lookup"><span data-stu-id="c7c64-1463">nx_secure_x509_dns_name_initialize</span></span>

<span data-ttu-id="c7c64-1464">Inizializzare una struttura di nomi DNS X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-1464">Initialize an X.509 DNS name structure</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1465">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1465">Prototype</span></span>

```C
UINT  nx_secure_x509_dns_name_initialize(
                        NX_SECURE_X509_DNS_NAME *dns_name,
                        const UCHAR *name_string, UINT length);
```

### <a name="description"></a><span data-ttu-id="c7c64-1466">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1466">Description</span></span>

<span data-ttu-id="c7c64-1467">Questo servizio inizializza un nome DNS X.509 da usare con determinati servizi API che richiedono un formato di nome specifico.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1467">This service initializes an X.509 DNS name for use with certain API services requiring a specific name format.</span></span> <span data-ttu-id="c7c64-1468">Ad esempio, il *servizio nx_secure_tls_sni_extension_parse* prevede che un oggetto NX_SECURE_X509_DNS_NAME corrisponda al nome fornito da un host remoto nell'estensione Indicazione nome server durante l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1468">For example, the *nx_secure_tls_sni_extension_parse* service expects an NX_SECURE_X509_DNS_NAME object in order to match the name provided by a remote host in the Server Name Indication extension during the TLS handshake.</span></span> <span data-ttu-id="c7c64-1469">Un nome DNS è semplicemente una stringa di caratteri con una lunghezza: la lunghezza massima consentita di un nome DNS (e le dimensioni del buffer interno in NX_SECURE_X509_DNS_NAME) è controllata dalla macro NX_SECURE_X509_DNS_NAME_MAX (100 byte predefiniti).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1469">A DNS name is simply a charater string with a length – the maximum allowed length of a DNS name (and the size of the internal buffer in NX_SECURE_X509_DNS_NAME) is controlled by the macro NX_SECURE_X509_DNS_NAME_MAX (default 100 bytes).</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1470">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1470">Parameters</span></span>

- <span data-ttu-id="c7c64-1471">**dns_name** Struttura dei nomi DNS da inizializzare.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1471">**dns_name** DNS name structure to initialize.</span></span>
- <span data-ttu-id="c7c64-1472">**name_string** Dati di stringa del nome DNS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1472">**name_string** DNS name string data.</span></span>
- <span data-ttu-id="c7c64-1473">**lunghezza** Lunghezza della stringa del nome.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1473">**length** Length of name string.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1474">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1474">Return Values</span></span>

- <span data-ttu-id="c7c64-1475">**NX_SUCCESS** (0x00) Inizializzazione riuscita.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1475">**NX_SUCCESS** (0x00) Successful initialization.</span></span>
- <span data-ttu-id="c7c64-1476">**NX_SECURE_X509_NAME_STRING_TOO_LONG** (0x19E) La stringa del nome specificata ha superato NX_SECURE_X509_DNS_NAME_MAX.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1476">**NX_SECURE_X509_NAME_STRING_TOO_LONG** (0x19E) The given name string exceeded NX_SECURE_X509_DNS_NAME_MAX.</span></span>
- <span data-ttu-id="c7c64-1477">**NX_PTR_ERROR** (0x07) Tentativo di usare un puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1477">**NX_PTR_ERROR** (0x07) Tried to use an invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1478">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1478">Allowed From</span></span>

<span data-ttu-id="c7c64-1479">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1479">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1480">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1480">Example</span></span>

```C
NX_SECURE_X509_DNS_NAME dns_name;

/* Initialize DNS name. */
status = nx_secure_x509_dns_name_initialize(&dns_name, “www.example.com”,
                                            strlen(“www.example.com”);

/* Use initialized DNS name to send the Server Name Indication extension to the
   remote TLS server. */
status = nx_secure_tls_session_sni_extension_set(&tls_session, &dns_name);
```

### <a name="see-also"></a><span data-ttu-id="c7c64-1481">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1481">See Also</span></span>

- <span data-ttu-id="c7c64-1482">nx_secure_tls_session_create</span><span class="sxs-lookup"><span data-stu-id="c7c64-1482">nx_secure_tls_session_create</span></span>
- <span data-ttu-id="c7c64-1483">nx_secure_tls_session_sni_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-1483">nx_secure_tls_session_sni_extension_parse</span></span>
- <span data-ttu-id="c7c64-1484">nx_secure_tls_session_sni_extension_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1484">nx_secure_tls_session_sni_extension_set</span></span>

## <a name="nx_secure_x509_extended_key_usage_extension_parse"></a><span data-ttu-id="c7c64-1485">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-1485">nx_secure_x509_extended_key_usage_extension_parse</span></span>

<span data-ttu-id="c7c64-1486">Trovare e analizzare un'estensione X.509 estesa per l'utilizzo delle chiavi in un certificato X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-1486">Find and parse an X.509 extended key usage extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1487">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1487">Prototype</span></span>

```C
UINT  nx_secure_x509_extended_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        UINT key_usage);
```

### <a name="description"></a><span data-ttu-id="c7c64-1488">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1488">Description</span></span>

<span data-ttu-id="c7c64-1489">Questo servizio deve essere chiamato dall'interno di un callback di verifica del certificato (vedere *nx_secure_tls_session_certificate_callback_set)*.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1489">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)*.</span></span> <span data-ttu-id="c7c64-1490">Cerca un OID di utilizzo della chiave estesa specifico all'interno di un certificato X.509 e restituisce se l'OID è presente.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1490">It will search for a specific extended key usage OID within an X.509 certificate and return whether the OID is present.</span></span> <span data-ttu-id="c7c64-1491">Il key_usage è un mapping integer degli OID usato internamente da NetX Secure X.509 e TLS per evitare di passare le stringhe OID a lunghezza variabile come parametri.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1491">The key_usage parameter is an integer mapping of the OIDs which is used internally by NetX Secure X.509 and TLS to avoid passing the variable-length OID strings as parameters.</span></span>

<span data-ttu-id="c7c64-1492">Gli OID pertinenti per l'estensione per l'utilizzo della chiave estesa sono indicati nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1492">The relevant OIDs for the extended key usage extension are given in the table below.</span></span> <span data-ttu-id="c7c64-1493">Un'implementazione tipica del client TLS che vuole controllare l'utilizzo della chiave estesa in un certificato del server TLS ricevuto verificherebbe l'esistenza del NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH OID: se l'estensione è presente ma tale OID non lo è, il certificato verrebbe considerato non valido per l'identificazione dell'host come server TLS e il callback di verifica del certificato dovrebbe restituire un errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1493">A typical TLS Client implementation wishing to check extended key usage in a received TLS server certificate would check for the existence of the OID NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH – if the extension is present but that OID is not, then the certificate would be considered invalid for identifiying the host as a TLS server and the certificate verification callback should return an error.</span></span> <span data-ttu-id="c7c64-1494">Se l'estensione stessa non è presente, è l'applicazione a decidere se procedere o meno con l'handshake TLS.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1494">If the extension itself is missing, then it is up to the application whether or not to proceed with the TLS handshake.</span></span>

<span data-ttu-id="c7c64-1495">Nel callback di verifica del certificato, il codice restituito di errore NX_SECURE_X509_KEY_USAGE_ERROR è riservato per l'uso da parte dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1495">In the certificate verification callback, the error return code NX_SECURE_X509_KEY_USAGE_ERROR is reserved for application use.</span></span> <span data-ttu-id="c7c64-1496">Se si verifica un errore durante la verifica dell'utilizzo della chiave, questo valore può essere restituito dal callback per indicare il motivo dell'errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1496">If there is an error in checking key usage, this value may be returned from the callback to indicate the reason for failure.</span></span>

| <span data-ttu-id="c7c64-1497">NetX Secure Identifier</span><span class="sxs-lookup"><span data-stu-id="c7c64-1497">NetX Secure Identifier</span></span>                                | <span data-ttu-id="c7c64-1498">Valore OID</span><span class="sxs-lookup"><span data-stu-id="c7c64-1498">OID Value</span></span>         | <span data-ttu-id="c7c64-1499">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1499">Description</span></span>                                      |
| --------------------------------------------------------- | --------------------- | ---------------------------------------------------- |
| <span data-ttu-id="c7c64-1500">NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH</span><span class="sxs-lookup"><span data-stu-id="c7c64-1500">NX_SECURE_TLS_X509_TYPE_PKIX_KP_SERVER_AUTH</span></span>   | <span data-ttu-id="c7c64-1501">1.3.6.1.5.5.7.3.1</span><span class="sxs-lookup"><span data-stu-id="c7c64-1501">1.3.6.1.5.5.7.3.1</span></span> | <span data-ttu-id="c7c64-1502">Il certificato può essere usato per identificare un server TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-1502">Certificate can be used to identify a TLS server</span></span> |
| <span data-ttu-id="c7c64-1503">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CLIENT_AUTH</span><span class="sxs-lookup"><span data-stu-id="c7c64-1503">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CLIENT_AUTH</span></span>   | <span data-ttu-id="c7c64-1504">1.3.6.1.5.5.7.3.2</span><span class="sxs-lookup"><span data-stu-id="c7c64-1504">1.3.6.1.5.5.7.3.2</span></span> | <span data-ttu-id="c7c64-1505">Il certificato può essere usato per identificare un client TLS</span><span class="sxs-lookup"><span data-stu-id="c7c64-1505">Certificate can be used to identify a TLS client</span></span> |
| <span data-ttu-id="c7c64-1506">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CODE_SIGNING</span><span class="sxs-lookup"><span data-stu-id="c7c64-1506">NX_SECURE_TLS_X509_TYPE_PKIX_KP_CODE_SIGNING</span></span>  | <span data-ttu-id="c7c64-1507">1.3.6.1.5.5.7.3.3</span><span class="sxs-lookup"><span data-stu-id="c7c64-1507">1.3.6.1.5.5.7.3.3</span></span> | <span data-ttu-id="c7c64-1508">Il certificato può essere usato per firmare il codice</span><span class="sxs-lookup"><span data-stu-id="c7c64-1508">Certificate can be used to sign code</span></span>             |
| <span data-ttu-id="c7c64-1509">NX_SECURE_TLS_X509_TYPE_PKIX_KP_EMAIL_PROTECT</span><span class="sxs-lookup"><span data-stu-id="c7c64-1509">NX_SECURE_TLS_X509_TYPE_PKIX_KP_EMAIL_PROTECT</span></span> | <span data-ttu-id="c7c64-1510">1.3.6.1.5.5.7.3.4</span><span class="sxs-lookup"><span data-stu-id="c7c64-1510">1.3.6.1.5.5.7.3.4</span></span> | <span data-ttu-id="c7c64-1511">Il certificato può essere usato per firmare i messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="c7c64-1511">Certificate can be used to sign emails</span></span>           |
| <span data-ttu-id="c7c64-1512">NX_SECURE_TLS_X509_TYPE_PKIX_KP_TIME_STAMPING</span><span class="sxs-lookup"><span data-stu-id="c7c64-1512">NX_SECURE_TLS_X509_TYPE_PKIX_KP_TIME_STAMPING</span></span> | <span data-ttu-id="c7c64-1513">1.3.6.1.5.5.7.3.8</span><span class="sxs-lookup"><span data-stu-id="c7c64-1513">1.3.6.1.5.5.7.3.8</span></span> | <span data-ttu-id="c7c64-1514">Il certificato può essere usato per firmare i timestamp</span><span class="sxs-lookup"><span data-stu-id="c7c64-1514">Certificate can be used to sign timestamps</span></span>       |
| <span data-ttu-id="c7c64-1515">NX_SECURE_TLS_X509_TYPE_PKIX_KP_OCSP_SIGNING</span><span class="sxs-lookup"><span data-stu-id="c7c64-1515">NX_SECURE_TLS_X509_TYPE_PKIX_KP_OCSP_SIGNING</span></span>  | <span data-ttu-id="c7c64-1516">1.3.6.1.5.5.7.3.9</span><span class="sxs-lookup"><span data-stu-id="c7c64-1516">1.3.6.1.5.5.7.3.9</span></span> | <span data-ttu-id="c7c64-1517">Il certificato può essere usato per firmare le risposte OCSP</span><span class="sxs-lookup"><span data-stu-id="c7c64-1517">Certificate can be used to sign OCSP responses</span></span>   |

<span data-ttu-id="c7c64-1518">OID e mapping per l'estensione X.509 Extended Key Usage</span><span class="sxs-lookup"><span data-stu-id="c7c64-1518">OIDs and mappings for X.509 Extended Key Usage Extension</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1519">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1519">Parameters</span></span>

- <span data-ttu-id="c7c64-1520">**certificato** Puntatore al certificato da verificare.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1520">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="c7c64-1521">**key_usage** Mapping di interi OID dalla tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1521">**key_usage** OID integer mapping from table above.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1522">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1522">Return Values</span></span>

- <span data-ttu-id="c7c64-1523">**NX_SUCCESS** (0x00) OID di utilizzo della chiave specificato trovato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1523">**NX_SUCCESS** (0x00) Specified key usage OID found.</span></span>
- <span data-ttu-id="c7c64-1524">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) Rilevato tag multi byte ASN.1 (certificato non supportato).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1524">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="c7c64-1525">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Rilevato campo ASN.1 invaild (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1525">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="c7c64-1526">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Classe di tag ASN.1 non valida rilevata (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1526">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="c7c64-1527">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Rilevata estensione non valida (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1527">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered (invalid certificate).</span></span>
- <span data-ttu-id="c7c64-1528">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) L'estensione Utilizzo chiavi esteso non è stata trovata nel certificato fornito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1528">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) The Extended Key Usage extension was not found in the provided certificate.</span></span>
- <span data-ttu-id="c7c64-1529">**NX_PTR_ERROR** (0x07) Puntatore certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1529">**NX_PTR_ERROR** (0x07) Invalid certificate pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1530">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1530">Allowed From</span></span>

<span data-ttu-id="c7c64-1531">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1531">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1532">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1532">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1533">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1533">See Also</span></span>

- <span data-ttu-id="c7c64-1534">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1534">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="c7c64-1535">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-1535">nx_secure_x509_key_usage_extension_parse</span></span>
- <span data-ttu-id="c7c64-1536">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-1536">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="c7c64-1537">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-1537">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="c7c64-1538">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-1538">nx_secure_x509_extension_find</span></span>

## <a name="nx_secure_x509_extension_find"></a><span data-ttu-id="c7c64-1539">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-1539">nx_secure_x509_extension_find</span></span>

<span data-ttu-id="c7c64-1540">Trovare e restituire un'estensione X.509 in un certificato X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-1540">Find and return an X.509 extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1541">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1541">Prototype</span></span>

```C
UINT  nx_secure_x509_extension_find(
                        NX_SECURE_X509_CERT *certificate,
                        NX_SECURE_X509_EXTENSION *extension,
                        USHORT extension_id);
```

### <a name="description"></a><span data-ttu-id="c7c64-1542">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1542">Description</span></span>

<span data-ttu-id="c7c64-1543">Questo servizio deve essere chiamato dall'interno di un callback di verifica del certificato (vedere *nx_secure_tls_session_certificate_callback_set)* ed è un servizio X.509 avanzato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1543">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)* and is an advanced X.509 service.</span></span>

<span data-ttu-id="c7c64-1544">La funzione cerca un'estensione specifica all'interno di un certificato X.509 in base a un OID e restituisce se l'OID è presente, insieme a una struttura contenente riferimenti ai dati di estensione non elaborati pertinenti.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1544">The function will search for a specific extension within an X.509 certificate based on an OID and return whether the OID is present, along with a structure containing references to the relevant raw extension data.</span></span> <span data-ttu-id="c7c64-1545">Il extension_id è un mapping di interi degli OID usato internamente da NetX Secure X.509 e TLS per evitare di passare le stringhe OID a lunghezza variabile come parametri.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1545">The extension_id parameter is an integer mapping of the OIDs which is used internally by NetX Secure X.509 and TLS to avoid passing the variable-length OID strings as parameters.</span></span>

<span data-ttu-id="c7c64-1546">Le funzioni helper fornite per estensioni specifiche (ad esempio *nx_secure_x509_key_usage_extension_parse*) chiamano nx_secure_x509_extension_find internamente per ottenere i dati dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1546">The helper functions provided for specific extensions (such as *nx_secure_x509_key_usage_extension_parse*) call nx_secure_x509_extension_find internally to obtain the extension data.</span></span>

<span data-ttu-id="c7c64-1547">Gli OID pertinenti per le estensioni X.509 note sono indicati nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1547">The relevant OIDs for known X.509 extensions are given in the table below.</span></span>

<span data-ttu-id="c7c64-1548">La NX_SECURE_X509_EXTENSION contiene puntatori al certificato X.509 che consentono alle funzioni helper come *nx_secure_x509_key_usage_extension_parse* di decodificare rapidamente i dati ASN.1 con codifica DER dell'estensione non elaborata.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1548">The NX_SECURE_X509_EXTENSION structure contains pointers into the X.509 certificate that allow helper functions such as *nx_secure_x509_key_usage_extension_parse* to quickly decode the raw extension DER-encoded ASN.1 data.</span></span>

<span data-ttu-id="c7c64-1549">Per informazioni su estensioni specifiche, vedere RFC 5280 (specifica X.509) o il riferimento per le funzioni helper appropriate, se disponibili.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1549">For information on specific extensions, see RFC 5280 (X.509 specification) or the reference for the appropriate helper functions if available.</span></span>

<span data-ttu-id="c7c64-1550">La versione corrente di NetX Secure X.509 ha un supporto limitato per le estensioni X.509.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1550">The current version of NetX Secure X.509 has limited support for X.509 extensions.</span></span> <span data-ttu-id="c7c64-1551">In futuro verranno aggiunte altre funzioni helper.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1551">More helper functions will be added in the future.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7c64-1552">*Questo servizio è una funzionalità avanzata per gli utenti che hanno familiarità con le estensioni X.509 e con codifica DER ASN.1. Viene fornito per consentire agli utenti di accedere alle estensioni per le quali NetX Secure X.509 attualmente non fornisce funzioni helper. Per tali estensioni senza funzioni helper, sarà necessario analizzare manualmente l'ASN.1 con codifica DER non elaborato.*</span><span class="sxs-lookup"><span data-stu-id="c7c64-1552">*This service is an advanced feature for users familiar with X.509 extensions and DER-encoded ASN.1. It is provided to enable those users to access extensions for which NetX Secure X.509 does not currently provide helper functions. For those extensions without helper functions, you will have to parse the raw DER-encoded ASN.1 yourself.*</span></span>

| <span data-ttu-id="c7c64-1553">NetX Secure Identifier</span><span class="sxs-lookup"><span data-stu-id="c7c64-1553">NetX Secure Identifier</span></span>                              | <span data-ttu-id="c7c64-1554">Valore OID</span><span class="sxs-lookup"><span data-stu-id="c7c64-1554">OID Value</span></span> | <span data-ttu-id="c7c64-1555">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1555">Description</span></span>                                                                    | <span data-ttu-id="c7c64-1556">Funzione helper?</span><span class="sxs-lookup"><span data-stu-id="c7c64-1556">Helper function?</span></span> |
| ------------------------------------------------------- | ------------- | ---------------------------------------------------------------------------------- | -------------------- |
| <span data-ttu-id="c7c64-1557">NX_SECURE_TLS_X509_TYPE_DIRECTORY_ATTRIBUTES</span><span class="sxs-lookup"><span data-stu-id="c7c64-1557">NX_SECURE_TLS_X509_TYPE_DIRECTORY_ATTRIBUTES</span></span>  | <span data-ttu-id="c7c64-1558">2.5.29.9</span><span class="sxs-lookup"><span data-stu-id="c7c64-1558">2.5.29.9</span></span>  | <span data-ttu-id="c7c64-1559">Attributi della directory: attributi di informazioni di base sul soggetto del certificato</span><span class="sxs-lookup"><span data-stu-id="c7c64-1559">Directory Attributes – basic information attributes about certificate subject</span></span>  | <span data-ttu-id="c7c64-1560">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1560">No</span></span>               |
| <span data-ttu-id="c7c64-1561">NX_SECURE_TLS_X509_TYPE_SUBJECT_KEY_ID</span><span class="sxs-lookup"><span data-stu-id="c7c64-1561">NX_SECURE_TLS_X509_TYPE_SUBJECT_KEY_ID</span></span>       | <span data-ttu-id="c7c64-1562">2.5.29.14</span><span class="sxs-lookup"><span data-stu-id="c7c64-1562">2.5.29.14</span></span> | <span data-ttu-id="c7c64-1563">Usato per identificare una chiave pubblica specifica</span><span class="sxs-lookup"><span data-stu-id="c7c64-1563">Used to identify a specific public key</span></span>                                         | <span data-ttu-id="c7c64-1564">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1564">No</span></span>               |
| <span data-ttu-id="c7c64-1565">NX_SECURE_TLS_X509_TYPE_KEY_USAGE</span><span class="sxs-lookup"><span data-stu-id="c7c64-1565">NX_SECURE_TLS_X509_TYPE_KEY_USAGE</span></span>             | <span data-ttu-id="c7c64-1566">2.5.29.15</span><span class="sxs-lookup"><span data-stu-id="c7c64-1566">2.5.29.15</span></span> | <span data-ttu-id="c7c64-1567">Fornisce informazioni sugli usi validi per la chiave pubblica del certificato</span><span class="sxs-lookup"><span data-stu-id="c7c64-1567">Provides information on valid uses for the certificate public key</span></span>              | <span data-ttu-id="c7c64-1568">Sì</span><span class="sxs-lookup"><span data-stu-id="c7c64-1568">Yes</span></span>              |
| <span data-ttu-id="c7c64-1569">NX_SECURE_TLS_X509_TYPE_SUBJECT_ALT_NAME</span><span class="sxs-lookup"><span data-stu-id="c7c64-1569">NX_SECURE_TLS_X509_TYPE_SUBJECT_ALT_NAME</span></span>     | <span data-ttu-id="c7c64-1570">2.5.29.17</span><span class="sxs-lookup"><span data-stu-id="c7c64-1570">2.5.29.17</span></span> | <span data-ttu-id="c7c64-1571">Fornisce nomi DNS alternativi per identificare il certificato</span><span class="sxs-lookup"><span data-stu-id="c7c64-1571">Provides alternative DNS names to identify the certificate</span></span>                     | <span data-ttu-id="c7c64-1572">Sì<sup>24</sup></span><span class="sxs-lookup"><span data-stu-id="c7c64-1572">Yes<sup>24</sup></span></span>        |
| <span data-ttu-id="c7c64-1573">NX_SECURE_TLS_X509_TYPE_ISSUER_ALT_NAME</span><span class="sxs-lookup"><span data-stu-id="c7c64-1573">NX_SECURE_TLS_X509_TYPE_ISSUER_ALT_NAME</span></span>      | <span data-ttu-id="c7c64-1574">2.5.29.18</span><span class="sxs-lookup"><span data-stu-id="c7c64-1574">2.5.29.18</span></span> | <span data-ttu-id="c7c64-1575">Fornisce nomi DNS alternativi per identificare l'autorità emittente del certificato</span><span class="sxs-lookup"><span data-stu-id="c7c64-1575">Provides alternative DNS names to identify the certificate's issuer</span></span>            | <span data-ttu-id="c7c64-1576">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1576">No</span></span>               |
| <span data-ttu-id="c7c64-1577">NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="c7c64-1577">NX_SECURE_TLS_X509_TYPE_BASIC_CONSTRAINTS</span></span>     | <span data-ttu-id="c7c64-1578">2.5.29.19</span><span class="sxs-lookup"><span data-stu-id="c7c64-1578">2.5.29.19</span></span> | <span data-ttu-id="c7c64-1579">Fornisce informazioni di base sui vincoli di utilizzo dei certificati</span><span class="sxs-lookup"><span data-stu-id="c7c64-1579">Provides basic certificate usage constraint information</span></span>                        | <span data-ttu-id="c7c64-1580">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1580">No</span></span>               |
| <span data-ttu-id="c7c64-1581">NX_SECURE_TLS_X509_TYPE_NAME_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="c7c64-1581">NX_SECURE_TLS_X509_TYPE_NAME_CONSTRAINTS</span></span>      | <span data-ttu-id="c7c64-1582">2.5.29.30</span><span class="sxs-lookup"><span data-stu-id="c7c64-1582">2.5.29.30</span></span> | <span data-ttu-id="c7c64-1583">Usato per vincolare i nomi dei certificati a domini specifici</span><span class="sxs-lookup"><span data-stu-id="c7c64-1583">Used to constrain certificate names to specific domains</span></span>                        | <span data-ttu-id="c7c64-1584">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1584">No</span></span>               |
| <span data-ttu-id="c7c64-1585">NX_SECURE_TLS_X509_TYPE_CRL_DISTRIBUTION</span><span class="sxs-lookup"><span data-stu-id="c7c64-1585">NX_SECURE_TLS_X509_TYPE_CRL_DISTRIBUTION</span></span>      | <span data-ttu-id="c7c64-1586">2.5.29.31</span><span class="sxs-lookup"><span data-stu-id="c7c64-1586">2.5.29.31</span></span> | <span data-ttu-id="c7c64-1587">Fornisce gli URI per la distribuzione CRL</span><span class="sxs-lookup"><span data-stu-id="c7c64-1587">Provides URIs for CRL distribution</span></span>                                             | <span data-ttu-id="c7c64-1588">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1588">No</span></span>               |
| <span data-ttu-id="c7c64-1589">NX_SECURE_TLS_X509_TYPE_CERTIFICATE_POLICIES</span><span class="sxs-lookup"><span data-stu-id="c7c64-1589">NX_SECURE_TLS_X509_TYPE_CERTIFICATE_POLICIES</span></span>  | <span data-ttu-id="c7c64-1590">2.5.29.32</span><span class="sxs-lookup"><span data-stu-id="c7c64-1590">2.5.29.32</span></span> | <span data-ttu-id="c7c64-1591">Elenco di criteri certificato per sistemi PKI di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="c7c64-1591">List of certificate policies for large PKI systems</span></span>                             | <span data-ttu-id="c7c64-1592">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1592">No</span></span>               |
| <span data-ttu-id="c7c64-1593">NX_SECURE_TLS_X509_TYPE_CERT_POLICY_MAPPINGS</span><span class="sxs-lookup"><span data-stu-id="c7c64-1593">NX_SECURE_TLS_X509_TYPE_CERT_POLICY_MAPPINGS</span></span> | <span data-ttu-id="c7c64-1594">2.5.29.33</span><span class="sxs-lookup"><span data-stu-id="c7c64-1594">2.5.29.33</span></span> | <span data-ttu-id="c7c64-1595">Elenco dei criteri dei certificati della CA</span><span class="sxs-lookup"><span data-stu-id="c7c64-1595">List of CA certificate policies</span></span>                                                | <span data-ttu-id="c7c64-1596">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1596">No</span></span>               |
| <span data-ttu-id="c7c64-1597">NX_SECURE_TLS_X509_TYPE_AUTHORITY_KEY_ID</span><span class="sxs-lookup"><span data-stu-id="c7c64-1597">NX_SECURE_TLS_X509_TYPE_AUTHORITY_KEY_ID</span></span>     | <span data-ttu-id="c7c64-1598">2.5.29.35</span><span class="sxs-lookup"><span data-stu-id="c7c64-1598">2.5.29.35</span></span> | <span data-ttu-id="c7c64-1599">Usato per identificare una chiave pubblica specifica associata a una firma del certificato</span><span class="sxs-lookup"><span data-stu-id="c7c64-1599">Used to identify a specific public key associated with a certificate signature</span></span> | <span data-ttu-id="c7c64-1600">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1600">No</span></span>               |
| <span data-ttu-id="c7c64-1601">NX_SECURE_TLS_X509_TYPE_POLICY_CONSTRAINTS</span><span class="sxs-lookup"><span data-stu-id="c7c64-1601">NX_SECURE_TLS_X509_TYPE_POLICY_CONSTRAINTS</span></span>    | <span data-ttu-id="c7c64-1602">2.5.29.36</span><span class="sxs-lookup"><span data-stu-id="c7c64-1602">2.5.29.36</span></span> | <span data-ttu-id="c7c64-1603">Vincoli dei criteri dell'autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1603">CA policy constraints</span></span>                                                          | <span data-ttu-id="c7c64-1604">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1604">No</span></span>               |
| <span data-ttu-id="c7c64-1605">NX_SECURE_TLS_X509_TYPE_EXTENDED_KEY_USAGE</span><span class="sxs-lookup"><span data-stu-id="c7c64-1605">NX_SECURE_TLS_X509_TYPE_EXTENDED_KEY_USAGE</span></span>   | <span data-ttu-id="c7c64-1606">2.5.29.37</span><span class="sxs-lookup"><span data-stu-id="c7c64-1606">2.5.29.37</span></span> | <span data-ttu-id="c7c64-1607">Informazioni aggiuntive sull'utilizzo delle chiavi basate su OID</span><span class="sxs-lookup"><span data-stu-id="c7c64-1607">Additional OID-based key usage information</span></span>                                     | <span data-ttu-id="c7c64-1608">Sì</span><span class="sxs-lookup"><span data-stu-id="c7c64-1608">Yes</span></span>              |
| <span data-ttu-id="c7c64-1609">NX_SECURE_TLS_X509_TYPE_FRESHEST_CRL</span><span class="sxs-lookup"><span data-stu-id="c7c64-1609">NX_SECURE_TLS_X509_TYPE_FRESHEST_CRL</span></span>          | <span data-ttu-id="c7c64-1610">2.5.29.46</span><span class="sxs-lookup"><span data-stu-id="c7c64-1610">2.5.29.46</span></span> | <span data-ttu-id="c7c64-1611">Fornisce informazioni per ottenere i delta CRL</span><span class="sxs-lookup"><span data-stu-id="c7c64-1611">Provides information for obtaining delta CRLs</span></span>                                  | <span data-ttu-id="c7c64-1612">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1612">No</span></span>               |
| <span data-ttu-id="c7c64-1613">NX_SECURE_TLS_X509_TYPE_INHIBIT_ANYPOLICY</span><span class="sxs-lookup"><span data-stu-id="c7c64-1613">NX_SECURE_TLS_X509_TYPE_INHIBIT_ANYPOLICY</span></span>     | <span data-ttu-id="c7c64-1614">2.5.29.54</span><span class="sxs-lookup"><span data-stu-id="c7c64-1614">2.5.29.54</span></span> | <span data-ttu-id="c7c64-1615">Campo del certificato della CA che indica che non è possibile usare AnyPolicy</span><span class="sxs-lookup"><span data-stu-id="c7c64-1615">CA certificate field indicating that AnyPolicy cannot be used</span></span>                  | <span data-ttu-id="c7c64-1616">No</span><span class="sxs-lookup"><span data-stu-id="c7c64-1616">No</span></span>               |

<span data-ttu-id="c7c64-1617">OID e mapping per le estensioni X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-1617">OIDs and mappings for X.509 Extensions</span></span>

24. <span data-ttu-id="c7c64-1618">L'estensione SubjectAltName viene analizzata come parte del controllo dei nomi DNS nel servizio nx_secure_x509_common_name_dns_check.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1618">The SubjectAltName extension is parsed as part of the DNS name check in the service nx_secure_x509_common_name_dns_check.</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1619">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1619">Parameters</span></span>

- <span data-ttu-id="c7c64-1620">**certificato** Puntatore al certificato da verificare.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1620">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="c7c64-1621">**estensione** Struttura restituita contenente il puntatore ai dati di estensione e la lunghezza.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1621">**extension** Return structure containing extension data pointer and length.</span></span>
- <span data-ttu-id="c7c64-1622">**extension_id** Mapping di interi OID dalla tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1622">**extension_id** OID integer mapping from table above.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1623">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1623">Return Values</span></span>

- <span data-ttu-id="c7c64-1624">**NX_SUCCESS** (0x00) OID dell'estensione specificato trovato e dati restituiti.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1624">**NX_SUCCESS** (0x00) Specified extension OID found and data returned.</span></span>
- <span data-ttu-id="c7c64-1625">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) Rilevato tag multi byte ASN.1 (certificato non supportato).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1625">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="c7c64-1626">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Rilevato campo ASN.1 invaild (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1626">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="c7c64-1627">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Classe di tag ASN.1 non valida rilevata (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1627">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="c7c64-1628">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Rilevata estensione non valida</span><span class="sxs-lookup"><span data-stu-id="c7c64-1628">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered</span></span>
- <span data-ttu-id="c7c64-1629">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) L'OID dell'estensione specificato non è stato trovato nel certificato fornito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1629">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B) The given extension OID was not found in the provided certificate.</span></span>
- <span data-ttu-id="c7c64-1630">**NX_PTR_ERROR** (0x07) Puntatore di estensione o certificato non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1630">**NX_PTR_ERROR** (0x07) Invalid certificate or extension pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1631">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1631">Allowed From</span></span>

<span data-ttu-id="c7c64-1632">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1632">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1633">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1633">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1634">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1634">See Also</span></span>

- <span data-ttu-id="c7c64-1635">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1635">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="c7c64-1636">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-1636">nx_secure_x509_key_usage_extension_parse</span></span>
- <span data-ttu-id="c7c64-1637">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-1637">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="c7c64-1638">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-1638">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="c7c64-1639">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-1639">nx_secure_x509_extended_key_usage_extension_parse</span></span>

## <a name="nx_secure_x509_key_usage_extension_parse"></a><span data-ttu-id="c7c64-1640">nx_secure_x509_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-1640">nx_secure_x509_key_usage_extension_parse</span></span>

<span data-ttu-id="c7c64-1641">Trovare e analizzare un'estensione X.509 Key Usage in un certificato X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-1641">Find and parse an X.509 Key Usage extension in an X.509 certificate</span></span>

### <a name="prototype"></a><span data-ttu-id="c7c64-1642">Prototipo</span><span class="sxs-lookup"><span data-stu-id="c7c64-1642">Prototype</span></span>

```C
UINT  nx_secure_x509_key_usage_extension_parse(
                        NX_SECURE_X509_CERT *certificate,
                        USHORT *bitfield);
```

### <a name="description"></a><span data-ttu-id="c7c64-1643">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1643">Description</span></span>

<span data-ttu-id="c7c64-1644">Questo servizio deve essere chiamato dall'interno di un callback di verifica del certificato *(vedere nx_secure_tls_session_certificate_callback_set).*</span><span class="sxs-lookup"><span data-stu-id="c7c64-1644">This service is intended to be called from within a certificate verification callback (see *nx_secure_tls_session_certificate_callback_set)*.</span></span> <span data-ttu-id="c7c64-1645">Verrà cercata l'estensione Utilizzo chiavi e, se trovata, restituirà il campo di bit Utilizzo chiavi nel parametro "bitfield".</span><span class="sxs-lookup"><span data-stu-id="c7c64-1645">It will search for the Key Usage extension and if found, will return the Key Usage bitfield in the "bitfield" parameter.</span></span>

<span data-ttu-id="c7c64-1646">I bit, come definito dalla specifica X.509 (RFC 5280), sono indicati nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1646">The bits, as defined by the X.509 specification (RFC 5280) are given in the table below.</span></span> <span data-ttu-id="c7c64-1647">Un'operazione AND bit per bit con la maschera di bit appropriata (e il controllo della presenza di valori non zero) offrirà il valore di ogni bit.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1647">A bitwise AND with the appropriate bitmask (and checking for non-zero) will give the value of each bit.</span></span>

<span data-ttu-id="c7c64-1648">Si noti che la codifica DER del campo di bit elimina gli zeri aggiuntivi, quindi la posizione effettiva dei bit nei dati del certificato non elaborati sarà probabilmente diversa dalle relative posizioni nel campo di bit decodificato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1648">Note that the DER-encoding of the bitfield eliminates extra zeroes so the actual position of the bits in the raw certificate data will likely be different from their positions in the decoded bitfield.</span></span> <span data-ttu-id="c7c64-1649">Le maschera di bit fornite devono essere usate solo sul campo di bit decodificato restituito da *nx_secure_x509_key_usage_extension_parse* e non con i dati non elaborati del certificato con codifica DER.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1649">The supplied bitmasks are only intended to be used on the decoded bitfield returned by *nx_secure_x509_key_usage_extension_parse* and not with the raw DER-encoded certificate data.</span></span>

<span data-ttu-id="c7c64-1650">Nel callback di verifica del certificato, il codice restituito di errore NX_SECURE_X509_KEY_USAGE_ERROR è riservato per l'uso da parte dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1650">In the certificate verification callback, the error return code NX_SECURE_X509_KEY_USAGE_ERROR is reserved for application use.</span></span> <span data-ttu-id="c7c64-1651">Se si verifica un errore durante la verifica dell'utilizzo della chiave, questo valore può essere restituito dal callback per indicare il motivo dell'errore.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1651">If there is an error in checking key usage, this value may be returned from the callback to indicate the reason for failure.</span></span>

| <span data-ttu-id="c7c64-1652">NetX Secure Identifier</span><span class="sxs-lookup"><span data-stu-id="c7c64-1652">NetX Secure Identifier</span></span>                            | <span data-ttu-id="c7c64-1653">Posizione del bit</span><span class="sxs-lookup"><span data-stu-id="c7c64-1653">Bit position</span></span> | <span data-ttu-id="c7c64-1654">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c7c64-1654">Description</span></span>                                                                                                                                                  |
| ----------------------------------------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="c7c64-1655">NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE</span><span class="sxs-lookup"><span data-stu-id="c7c64-1655">NX_SECURE_X509_KEY_USAGE_DIGITAL_SIGNATURE</span></span>  | <span data-ttu-id="c7c64-1656">0</span><span class="sxs-lookup"><span data-stu-id="c7c64-1656">0</span></span>            | <span data-ttu-id="c7c64-1657">Il certificato può essere usato per le firme digitali</span><span class="sxs-lookup"><span data-stu-id="c7c64-1657">Certificate can be used for digital signatures</span></span>                                                                                                               |
| <span data-ttu-id="c7c64-1658">NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION</span><span class="sxs-lookup"><span data-stu-id="c7c64-1658">NX_SECURE_X509_KEY_USAGE_NON_REPUDIATION</span></span>    | <span data-ttu-id="c7c64-1659">1</span><span class="sxs-lookup"><span data-stu-id="c7c64-1659">1</span></span>            | <span data-ttu-id="c7c64-1660">Il certificato può essere usato per verificare firme digitali diverse da quelle per certificati e CRL</span><span class="sxs-lookup"><span data-stu-id="c7c64-1660">Certificate can be used to verify digital signatures other than those for certificates and CRLs</span></span>                                                              |
| <span data-ttu-id="c7c64-1661">NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT</span><span class="sxs-lookup"><span data-stu-id="c7c64-1661">NX_SECURE_X509_KEY_USAGE_KEY_ENCIPHERMENT</span></span>   | <span data-ttu-id="c7c64-1662">2</span><span class="sxs-lookup"><span data-stu-id="c7c64-1662">2</span></span>            | <span data-ttu-id="c7c64-1663">Il certificato può essere usato per crittografare le chiavi simmetriche (trasporto delle chiavi)</span><span class="sxs-lookup"><span data-stu-id="c7c64-1663">Certificate can be used to encrypt symmetric keys (key transport)</span></span>                                                                                            |
| <span data-ttu-id="c7c64-1664">NX_SECURE_X509_KEY_USAGE_DATA_ENCIPHERMENT</span><span class="sxs-lookup"><span data-stu-id="c7c64-1664">NX_SECURE_X509_KEY_USAGE_DATA_ENCIPHERMENT</span></span>  | <span data-ttu-id="c7c64-1665">3</span><span class="sxs-lookup"><span data-stu-id="c7c64-1665">3</span></span>            | <span data-ttu-id="c7c64-1666">Il certificato può essere usato per crittografare direttamente i dati utente non elaborati (non comune)</span><span class="sxs-lookup"><span data-stu-id="c7c64-1666">Certificate can be used to directly encrypt raw user data (uncommon)</span></span>                                                                                         |
| <span data-ttu-id="c7c64-1667">NX_SECURE_X509_KEY_USAGE_KEY_AGREEMENT</span><span class="sxs-lookup"><span data-stu-id="c7c64-1667">NX_SECURE_X509_KEY_USAGE_KEY_AGREEMENT</span></span>      | <span data-ttu-id="c7c64-1668">4</span><span class="sxs-lookup"><span data-stu-id="c7c64-1668">4</span></span>            | <span data-ttu-id="c7c64-1669">Il certificato può essere usato per il contratto di chiave (come con Diffie-Hellman)</span><span class="sxs-lookup"><span data-stu-id="c7c64-1669">Certificate can be used for key agreement (as with Diffie-Hellman)</span></span>                                                                                           |
| <span data-ttu-id="c7c64-1670">NX_SECURE_X509_KEY_USAGE_KEY_CERT_SIGN</span><span class="sxs-lookup"><span data-stu-id="c7c64-1670">NX_SECURE_X509_KEY_USAGE_KEY_CERT_SIGN</span></span>     | <span data-ttu-id="c7c64-1671">5</span><span class="sxs-lookup"><span data-stu-id="c7c64-1671">5</span></span>            | <span data-ttu-id="c7c64-1672">Il certificato può essere usato per firmare e verificare altri certificati (il certificato è un certificato CA o ICA).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1672">Certificate can be used to sign and verify other certificates (the certificate is a CA or ICA certificate).</span></span>                                                  |
| <span data-ttu-id="c7c64-1673">NX_SECURE_X509_KEY_USAGE_CRL_SIGN</span><span class="sxs-lookup"><span data-stu-id="c7c64-1673">NX_SECURE_X509_KEY_USAGE_CRL_SIGN</span></span>           | <span data-ttu-id="c7c64-1674">6</span><span class="sxs-lookup"><span data-stu-id="c7c64-1674">6</span></span>            | <span data-ttu-id="c7c64-1675">La chiave pubblica del certificato viene usata per verificare le firme nei CRL</span><span class="sxs-lookup"><span data-stu-id="c7c64-1675">Certificate public key is used to verify signatures on CRLs</span></span>                                                                                                  |
| <span data-ttu-id="c7c64-1676">NX_SECURE_X509_KEY_USAGE_ENCIPHER_ONLY</span><span class="sxs-lookup"><span data-stu-id="c7c64-1676">NX_SECURE_X509_KEY_USAGE_ENCIPHER_ONLY</span></span>      | <span data-ttu-id="c7c64-1677">7</span><span class="sxs-lookup"><span data-stu-id="c7c64-1677">7</span></span>            | <span data-ttu-id="c7c64-1678">Usato con il bit key agreement (bit 4): se impostato, la chiave del certificato può essere usata solo per crittografare durante l'accordo di chiave.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1678">Used with Key Agreement bit (bit 4) – when set, certificate key can only be used to encrypt during key agreement.</span></span> <span data-ttu-id="c7c64-1679">Non definito se il bit dell'accordo di chiave non è impostato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1679">Undefined if Key Agreement bit is not set.</span></span> |
| <span data-ttu-id="c7c64-1680">NX_SECURE_X509_KEY_USAGE_DECIPHER_ONLY</span><span class="sxs-lookup"><span data-stu-id="c7c64-1680">NX_SECURE_X509_KEY_USAGE_DECIPHER_ONLY</span></span>      | <span data-ttu-id="c7c64-1681">8</span><span class="sxs-lookup"><span data-stu-id="c7c64-1681">8</span></span>            | <span data-ttu-id="c7c64-1682">Usato con il bit key agreement (bit 4): se impostato, la chiave del certificato può essere usata solo per decrittografare durante l'accordo di chiave.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1682">Used with Key Agreement bit (bit 4) – when set, certificate key can only be used to decrypt during key agreement.</span></span> <span data-ttu-id="c7c64-1683">Non definito se il bit dell'accordo di chiave non è impostato.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1683">Undefined if Key Agreement bit is not set.</span></span> |

<span data-ttu-id="c7c64-1684">Maschera di bit e valori per l'estensione per l'utilizzo delle chiavi X.509</span><span class="sxs-lookup"><span data-stu-id="c7c64-1684">Bitmasks and values for X.509 Key Usage Extension</span></span>

### <a name="parameters"></a><span data-ttu-id="c7c64-1685">Parametri</span><span class="sxs-lookup"><span data-stu-id="c7c64-1685">Parameters</span></span>

- <span data-ttu-id="c7c64-1686">**certificato** Puntatore al certificato da verificare.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1686">**certificate** Pointer to certificate being verified.</span></span>
- <span data-ttu-id="c7c64-1687">**bitfield** Restituisce l'intero campo di bit dall'estensione.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1687">**bitfield** Return the entire bitfield from the extension.</span></span>

### <a name="return-values"></a><span data-ttu-id="c7c64-1688">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="c7c64-1688">Return Values</span></span>

- <span data-ttu-id="c7c64-1689">**NX_SUCCESS** (0x00) L'estensione per l'utilizzo della chiave è stata trovata e il campo di bit restituito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1689">**NX_SUCCESS** (0x00) Key usage extension found and bitfield returned.</span></span>
- <span data-ttu-id="c7c64-1690">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) Rilevato tag multi byte ASN.1 (certificato non supportato).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1690">**NX_SECURE_X509_MULTIBYTE_TAG_UNSUPPORTED** (0x181) ASN.1 multi-byte tag encountered (unsupported certificate).</span></span>
- <span data-ttu-id="c7c64-1691">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Rilevato campo ASN.1 invaild (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1691">**NX_SECURE_X509_ASN1_LENGTH_TOO_LONG** (0x182) Invaild ASN.1 field encountered (invalid certificate).</span></span>
- <span data-ttu-id="c7c64-1692">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Classe di tag ASN.1 non valida rilevata (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1692">**NX_SECURE_X509_INVALID_TAG_CLASS** (0x190) Invalid ASN.1 tag class encountered (invalid certificate).</span></span>
- <span data-ttu-id="c7c64-1693">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Rilevata estensione non valida (certificato non valido).</span><span class="sxs-lookup"><span data-stu-id="c7c64-1693">**NX_SECURE_X509_INVALID_EXTENSION_SEQUENCE** (0x192) Invalid extension encountered (invalid certificate).</span></span>
- <span data-ttu-id="c7c64-1694">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B)L'estensione Utilizzo chiavi non è stata trovata nel certificato fornito.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1694">**NX_SECURE_X509_EXTENSION_NOT_FOUND** (0x19B)The Key Usage extension was not found in the provided certificate.</span></span>
- <span data-ttu-id="c7c64-1695">**NX_PTR_ERROR** (0x07) Certificato o puntatore di campo di bit non valido.</span><span class="sxs-lookup"><span data-stu-id="c7c64-1695">**NX_PTR_ERROR** (0x07) Invalid certificate or bitfield pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="c7c64-1696">Consentito da</span><span class="sxs-lookup"><span data-stu-id="c7c64-1696">Allowed From</span></span>

<span data-ttu-id="c7c64-1697">Thread</span><span class="sxs-lookup"><span data-stu-id="c7c64-1697">Threads</span></span>

### <a name="example"></a><span data-ttu-id="c7c64-1698">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7c64-1698">Example</span></span>

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

### <a name="see-also"></a><span data-ttu-id="c7c64-1699">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c7c64-1699">See Also</span></span>

- <span data-ttu-id="c7c64-1700">nx_secure_tls_session_certificate_callback_set</span><span class="sxs-lookup"><span data-stu-id="c7c64-1700">nx_secure_tls_session_certificate_callback_set</span></span>
- <span data-ttu-id="c7c64-1701">nx_secure_x509_extended_key_usage_extension_parse</span><span class="sxs-lookup"><span data-stu-id="c7c64-1701">nx_secure_x509_extended_key_usage_extension_parse</span></span>
- <span data-ttu-id="c7c64-1702">nx_secure_x509_crl_revocation_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-1702">nx_secure_x509_crl_revocation_check</span></span>
- <span data-ttu-id="c7c64-1703">nx_secure_x509_common_name_dns_check</span><span class="sxs-lookup"><span data-stu-id="c7c64-1703">nx_secure_x509_common_name_dns_check</span></span>
- <span data-ttu-id="c7c64-1704">nx_secure_x509_extension_find</span><span class="sxs-lookup"><span data-stu-id="c7c64-1704">nx_secure_x509_extension_find</span></span>
