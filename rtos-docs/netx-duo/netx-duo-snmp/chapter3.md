---
title: Capitolo 3-Descrizione dei servizi dell'agente SNMP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi dell'agente SNMP NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: cf4c4cb0edb7deb7bd0f257f48949b5c7355426b
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821671"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-snmp-agent-services"></a><span data-ttu-id="06882-103">Capitolo 3-Descrizione dei servizi dell'agente SNMP di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="06882-103">Chapter 3 - Description of Azure RTOS NetX Duo SNMP agent services</span></span>

<span data-ttu-id="06882-104">Questo capitolo contiene una descrizione di tutti i servizi dell'agente SNMP di Azure RTO NetX Duo (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="06882-104">This chapter contains a description of all Azure RTOS NetX Duo SNMP agent services (listed below) in alphabetical order.</span></span>

<span data-ttu-id="06882-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="06882-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- [<span data-ttu-id="06882-106">nx_snmp_agent_auth_trap_key_use</span><span class="sxs-lookup"><span data-stu-id="06882-106">nx_snmp_agent_auth_trap_key_use</span></span>](#nx_snmp_agent_auth_trap_key_use)
   - <span data-ttu-id="06882-107">*Specificare la chiave di autenticazione (solo SNMP v3) per i messaggi trap*</span><span class="sxs-lookup"><span data-stu-id="06882-107">*Specify authentication key (SNMP v3 only) for trap messages*</span></span>
- [<span data-ttu-id="06882-108">nx_snmp_agent_authenticate_key_use</span><span class="sxs-lookup"><span data-stu-id="06882-108">nx_snmp_agent_authenticate_key_use</span></span>](#nx_snmp_agent_authenticate_key_use)
   - <span data-ttu-id="06882-109">*Specificare la chiave di autenticazione (solo SNMP v3) per i messaggi di risposta*</span><span class="sxs-lookup"><span data-stu-id="06882-109">*Specify authentication key (SNMP v3 only) for response messages*</span></span>
- [<span data-ttu-id="06882-110">nx_snmp_agent_community_get</span><span class="sxs-lookup"><span data-stu-id="06882-110">nx_snmp_agent_community_get</span></span>](#nx_snmp_agent_community_get)
   - <span data-ttu-id="06882-111">*Recupera nome comunità*</span><span class="sxs-lookup"><span data-stu-id="06882-111">*Retrieve community name*</span></span>
- [<span data-ttu-id="06882-112">nx_snmp_agent_context_engine_set</span><span class="sxs-lookup"><span data-stu-id="06882-112">nx_snmp_agent_context_engine_set</span></span>](#nx_snmp_agent_context_engine_set)
   - <span data-ttu-id="06882-113">*Imposta motore di contesto (solo SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="06882-113">*Set context engine (SNMP v3 only)*</span></span>
- [<span data-ttu-id="06882-114">nx_snmp_agent_context_name_set</span><span class="sxs-lookup"><span data-stu-id="06882-114">nx_snmp_agent_context_name_set</span></span>](#nx_snmp_agent_context_name_set)
   - <span data-ttu-id="06882-115">*Imposta nome contesto (solo SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="06882-115">*Set context name (SNMP v3 only)*</span></span>
- [<span data-ttu-id="06882-116">nx_snmp_agent_create</span><span class="sxs-lookup"><span data-stu-id="06882-116">nx_snmp_agent_create</span></span>](#nx_snmp_agent_create)
   - <span data-ttu-id="06882-117">*Crea agente SNMP*</span><span class="sxs-lookup"><span data-stu-id="06882-117">*Create SNMP agent*</span></span>
- [<span data-ttu-id="06882-118">nx_snmp_agent_current_version_get</span><span class="sxs-lookup"><span data-stu-id="06882-118">nx_snmp_agent_current_version_get</span></span>](#nx_snmp_agent_current_version_get)
   - <span data-ttu-id="06882-119">*Ottenere la versione SNMP del pacchetto ricevuto*</span><span class="sxs-lookup"><span data-stu-id="06882-119">*Get the SNMP version of received packet*</span></span>
- [<span data-ttu-id="06882-120">nx_snmp_agent_request_get_type_test</span><span class="sxs-lookup"><span data-stu-id="06882-120">nx_snmp_agent_request_get_type_test</span></span>](#nx_snmp_agent_request_get_type_test)
   - <span data-ttu-id="06882-121">*Indica se l'ultima richiesta SNMP è GET o SET Type*</span><span class="sxs-lookup"><span data-stu-id="06882-121">*Indicate if last SNMP request is GET or SET type*</span></span>
- [<span data-ttu-id="06882-122">nx_snmp_agent_private_string_test</span><span class="sxs-lookup"><span data-stu-id="06882-122">nx_snmp_agent_private_string_test</span></span>](#nx_snmp_agent_private_string_test)
   - <span data-ttu-id="06882-123">*Determinare se la stringa corrisponde alla stringa privata dell'agente*</span><span class="sxs-lookup"><span data-stu-id="06882-123">*Determine if string matches agent private string*</span></span>
- [<span data-ttu-id="06882-124">nx_snmp_agent_public_string_test</span><span class="sxs-lookup"><span data-stu-id="06882-124">nx_snmp_agent_public_string_test</span></span>](#nx_snmp_agent_public_string_test)
   - <span data-ttu-id="06882-125">*Determinare se la stringa corrisponde alla stringa pubblica dell'agente*</span><span class="sxs-lookup"><span data-stu-id="06882-125">*Determine if string matches agent public string*</span></span>
- [<span data-ttu-id="06882-126">nx_snmp_agent_set_interface</span><span class="sxs-lookup"><span data-stu-id="06882-126">nx_snmp_agent_set_interface</span></span>](#nx_snmp_agent_set_interface)
   - <span data-ttu-id="06882-127">*Impostare l'interfaccia di rete per la messaggistica SNMP*</span><span class="sxs-lookup"><span data-stu-id="06882-127">*Set network interface for SNMP messaging*</span></span>
- [<span data-ttu-id="06882-128">nx_snmp_agent_private_string_set</span><span class="sxs-lookup"><span data-stu-id="06882-128">nx_snmp_agent_private_string_set</span></span>](#nx_snmp_agent_private_string_set)
   - <span data-ttu-id="06882-129">*Imposta la stringa della comunità privata dell'agente SNMP*</span><span class="sxs-lookup"><span data-stu-id="06882-129">*Set the SNMP agent private community string*</span></span>
- [<span data-ttu-id="06882-130">nx_snmp_agent_public_string_set</span><span class="sxs-lookup"><span data-stu-id="06882-130">nx_snmp_agent_public_string_set</span></span>](#nx_snmp_agent_public_string_set)
   - <span data-ttu-id="06882-131">*Imposta la stringa della comunità pubblica dell'agente SNMP*</span><span class="sxs-lookup"><span data-stu-id="06882-131">*Set the SNMP agent public community string*</span></span>
- [<span data-ttu-id="06882-132">nx_snmp_agent_version_set</span><span class="sxs-lookup"><span data-stu-id="06882-132">nx_snmp_agent_version_set</span></span>](#nx_snmp_agent_version_set)
   - <span data-ttu-id="06882-133">*Impostare lo stato dell'agente SNMP per tutte le versioni SNMP*</span><span class="sxs-lookup"><span data-stu-id="06882-133">*Set the SNMP agent status for all SNMP versions*</span></span>
- [<span data-ttu-id="06882-134">nx_snmp_agent_delete</span><span class="sxs-lookup"><span data-stu-id="06882-134">nx_snmp_agent_delete</span></span>](#nx_snmp_agent_delete)
   - <span data-ttu-id="06882-135">*Elimina agente SNMP*</span><span class="sxs-lookup"><span data-stu-id="06882-135">*Delete SNMP agent*</span></span>
- [<span data-ttu-id="06882-136">nx_snmp_agent_md5_key_create</span><span class="sxs-lookup"><span data-stu-id="06882-136">nx_snmp_agent_md5_key_create</span></span>](#nx_snmp_agent_md5_key_create)
   - <span data-ttu-id="06882-137">*Crea chiave MD5 (solo SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="06882-137">*Create md5 key (SNMP v3 only)*</span></span>
- [<span data-ttu-id="06882-138">nx_snmp_agent_md5_key_create_extended</span><span class="sxs-lookup"><span data-stu-id="06882-138">nx_snmp_agent_md5_key_create_extended</span></span>](#nx_snmp_agent_md5_key_create_extended)
   - <span data-ttu-id="06882-139">*Crea chiave MD5 (solo SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="06882-139">*Create md5 key (SNMP v3 only)*</span></span>
- [<span data-ttu-id="06882-140">nx_snmp_agent_priv_trap_key_use</span><span class="sxs-lookup"><span data-stu-id="06882-140">nx_snmp_agent_priv_trap_key_use</span></span>](#nx_snmp_agent_priv_trap_key_use)
   - <span data-ttu-id="06882-141">*Specificare la chiave di crittografia (solo SNMP v3) per i messaggi trap*</span><span class="sxs-lookup"><span data-stu-id="06882-141">*Specify encryption key (SNMP v3 only) for trap messages*</span></span>
- [<span data-ttu-id="06882-142">nx_snmp_agent_privacy_key_use</span><span class="sxs-lookup"><span data-stu-id="06882-142">nx_snmp_agent_privacy_key_use</span></span>](#nx_snmp_agent_privacy_key_use)
   - <span data-ttu-id="06882-143">*Specificare la chiave di crittografia (solo SNMP v3) per i messaggi di risposta*</span><span class="sxs-lookup"><span data-stu-id="06882-143">*Specify encryption key (SNMP v3 only) for response messages*</span></span>
- [<span data-ttu-id="06882-144">nx_snmp_agent_sha_key_create</span><span class="sxs-lookup"><span data-stu-id="06882-144">nx_snmp_agent_sha_key_create</span></span>](#nx_snmp_agent_sha_key_create)
   - <span data-ttu-id="06882-145">*Crea chiave SHA (solo SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="06882-145">*Create sha key (SNMP v3 only)*</span></span>
- [<span data-ttu-id="06882-146">nx_snmp_agent_sha_key_create_extended</span><span class="sxs-lookup"><span data-stu-id="06882-146">nx_snmp_agent_sha_key_create_extended</span></span>](#nx_snmp_agent_sha_key_create_extended)
   - <span data-ttu-id="06882-147">*Crea chiave SHA (solo SNMP v3)*</span><span class="sxs-lookup"><span data-stu-id="06882-147">*Create sha key (SNMP v3 only)*</span></span>
- [<span data-ttu-id="06882-148">nx_snmp_agent_start</span><span class="sxs-lookup"><span data-stu-id="06882-148">nx_snmp_agent_start</span></span>](#nx_snmp_agent_start)
   - <span data-ttu-id="06882-149">*Avvia agente SNMP*</span><span class="sxs-lookup"><span data-stu-id="06882-149">*Start SNMP agent*</span></span>
- [<span data-ttu-id="06882-150">nx_snmp_agent_stop</span><span class="sxs-lookup"><span data-stu-id="06882-150">nx_snmp_agent_stop</span></span>](#nx_snmp_agent_stop)
   - <span data-ttu-id="06882-151">*Arrestare l'agente SNMP*</span><span class="sxs-lookup"><span data-stu-id="06882-151">*Stop SNMP agent*</span></span>
- [<span data-ttu-id="06882-152">nx_snmp_agent_trap_send</span><span class="sxs-lookup"><span data-stu-id="06882-152">nx_snmp_agent_trap_send</span></span>](#nx_snmp_agent_trap_send)
   - <span data-ttu-id="06882-153">*Invia trap SNMP v1 (solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="06882-153">*Send SNMP v1 trap (IPv4 only)*</span></span>
- [<span data-ttu-id="06882-154">nx_snmp_agent_trapv2_send</span><span class="sxs-lookup"><span data-stu-id="06882-154">nx_snmp_agent_trapv2_send</span></span>](#nx_snmp_agent_trapv2_send)
   - <span data-ttu-id="06882-155">*Invia trap SNMP v2 (solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="06882-155">*Send SNMP v2 trap (IPv4 only)*</span></span>
- [<span data-ttu-id="06882-156">nx_snmp_agent_trapv2_oid_send</span><span class="sxs-lookup"><span data-stu-id="06882-156">nx_snmp_agent_trapv2_oid_send</span></span>](#nx_snmp_agent_trapv2_oid_send)
   - <span data-ttu-id="06882-157">*Invia trap SNMP v2 (solo IPv4) specificando l'OID*</span><span class="sxs-lookup"><span data-stu-id="06882-157">*Send SNMP v2 trap (IPv4 only) specifying the OID*</span></span>
- [<span data-ttu-id="06882-158">nx_snmp_agent_trapv3_send</span><span class="sxs-lookup"><span data-stu-id="06882-158">nx_snmp_agent_trapv3_send</span></span>](#nx_snmp_agent_trapv3_send)
   - <span data-ttu-id="06882-159">*Invia trap SNMP v3 (solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="06882-159">*Send SNMP v3 trap (IPv4 only)*</span></span>
- [<span data-ttu-id="06882-160">nx_snmp_agent_trapv3_oid_send</span><span class="sxs-lookup"><span data-stu-id="06882-160">nx_snmp_agent_trapv3_oid_send</span></span>](#nx_snmp_agent_trapv3_oid_send)
   - <span data-ttu-id="06882-161">*Invia trap SNMP v2 (solo IPv4) specificando l'OID*</span><span class="sxs-lookup"><span data-stu-id="06882-161">*Send SNMP v2 trap (IPv4 only) specifying the OID*</span></span>
- [<span data-ttu-id="06882-162">nxd_snmp_agent_trap_send</span><span class="sxs-lookup"><span data-stu-id="06882-162">nxd_snmp_agent_trap_send</span></span>](#nxd_snmp_agent_trap_send)
   - <span data-ttu-id="06882-163">*Invia trap SNMP v1 (IPv4 e IPv6)*</span><span class="sxs-lookup"><span data-stu-id="06882-163">*Send SNMP v1 trap (IPv4 and IPv6)*</span></span>
- [<span data-ttu-id="06882-164">nxd_snmp_agent_trapv2_send</span><span class="sxs-lookup"><span data-stu-id="06882-164">nxd_snmp_agent_trapv2_send</span></span>](#nxd_snmp_agent_trapv2_send)
   - <span data-ttu-id="06882-165">*Invia trap SNMP v2 (IPv4 e IPv6)*</span><span class="sxs-lookup"><span data-stu-id="06882-165">*Send SNMP v2 trap (IPv4 and IPv6)*</span></span>
- [<span data-ttu-id="06882-166">nxd_snmp_agent_trapv2_oid_send</span><span class="sxs-lookup"><span data-stu-id="06882-166">nxd_snmp_agent_trapv2_oid_send</span></span>](#nxd_snmp_agent_trapv2_oid_send)
   - <span data-ttu-id="06882-167">*Invia trap SNMP v2 (IPv4/IPv6) che specifica l'OID*</span><span class="sxs-lookup"><span data-stu-id="06882-167">*Send SNMP v2 trap (IPv4/IPv6) specifying the OID*</span></span>
- [<span data-ttu-id="06882-168">nxd_snmp_agent_trapv3_send</span><span class="sxs-lookup"><span data-stu-id="06882-168">nxd_snmp_agent_trapv3_send</span></span>](#nxd_snmp_agent_trapv3_send)
   - <span data-ttu-id="06882-169">*Invia trap SNMP v3 (IPv4 e IPv6)*</span><span class="sxs-lookup"><span data-stu-id="06882-169">*Send SNMP v3 trap (IPv4 and IPv6)*</span></span>
- [<span data-ttu-id="06882-170">nxd_snmp_agent_trapv3_oid_send</span><span class="sxs-lookup"><span data-stu-id="06882-170">nxd_snmp_agent_trapv3_oid_send</span></span>](#nxd_snmp_agent_trapv3_oid_send)
   - <span data-ttu-id="06882-171">*Invia trap SNMP v2 (IPv4/IPv6) che specifica l'OID*</span><span class="sxs-lookup"><span data-stu-id="06882-171">*Send SNMP v2 trap (IPv4/IPv6) specifying the OID*</span></span>
- [<span data-ttu-id="06882-172">nx_snmp_agent_v3_context_boots_set</span><span class="sxs-lookup"><span data-stu-id="06882-172">nx_snmp_agent_v3_context_boots_set</span></span>](#nx_snmp_agent_v3_context_boots_set)
   - <span data-ttu-id="06882-173">*Impostare il numero di riavvii*</span><span class="sxs-lookup"><span data-stu-id="06882-173">*Set the number of reboots*</span></span>
- [<span data-ttu-id="06882-174">nx_snmp_object_compare</span><span class="sxs-lookup"><span data-stu-id="06882-174">nx_snmp_object_compare</span></span>](#nx_snmp_object_compare)
   - <span data-ttu-id="06882-175">*Confrontare due oggetti*</span><span class="sxs-lookup"><span data-stu-id="06882-175">*Compare two objects*</span></span>
- [<span data-ttu-id="06882-176">nx_snmp_object_compare_extended</span><span class="sxs-lookup"><span data-stu-id="06882-176">nx_snmp_object_compare_extended</span></span>](#nx_snmp_object_compare_extended)
   - <span data-ttu-id="06882-177">*Confrontare due oggetti*</span><span class="sxs-lookup"><span data-stu-id="06882-177">*Compare two objects*</span></span>
- [<span data-ttu-id="06882-178">nx_snmp_object_copy</span><span class="sxs-lookup"><span data-stu-id="06882-178">nx_snmp_object_copy</span></span>](#nx_snmp_object_copy)
   - <span data-ttu-id="06882-179">*Copia di un oggetto*</span><span class="sxs-lookup"><span data-stu-id="06882-179">*Copy an object*</span></span>
- [<span data-ttu-id="06882-180">nx_snmp_object_copy_extended</span><span class="sxs-lookup"><span data-stu-id="06882-180">nx_snmp_object_copy_extended</span></span>](#nx_snmp_object_copy_extended)
   - <span data-ttu-id="06882-181">*Copia di un oggetto*</span><span class="sxs-lookup"><span data-stu-id="06882-181">*Copy an object*</span></span>
- [<span data-ttu-id="06882-182">nx_snmp_object_counter_get</span><span class="sxs-lookup"><span data-stu-id="06882-182">nx_snmp_object_counter_get</span></span>](#nx_snmp_object_counter_get)
   - <span data-ttu-id="06882-183">*Ottenere un oggetto contatore*</span><span class="sxs-lookup"><span data-stu-id="06882-183">*Get counter object*</span></span>
- [<span data-ttu-id="06882-184">nx_snmp_object_counter_set</span><span class="sxs-lookup"><span data-stu-id="06882-184">nx_snmp_object_counter_set</span></span>](#nx_snmp_object_counter_set)
   - <span data-ttu-id="06882-185">*Imposta oggetto contatore*</span><span class="sxs-lookup"><span data-stu-id="06882-185">*Set counter object*</span></span>
- [<span data-ttu-id="06882-186">nx_snmp_object_counter64_get</span><span class="sxs-lookup"><span data-stu-id="06882-186">nx_snmp_object_counter64_get</span></span>](#nx_snmp_object_counter64_get)
   - <span data-ttu-id="06882-187">*Ottenere un oggetto contatore a 64 bit*</span><span class="sxs-lookup"><span data-stu-id="06882-187">*Get 64-bit counter object*</span></span>
- [<span data-ttu-id="06882-188">nx_snmp_object_counter64_set</span><span class="sxs-lookup"><span data-stu-id="06882-188">nx_snmp_object_counter64_set</span></span>](#nx_snmp_object_counter64_set)
   - <span data-ttu-id="06882-189">*Imposta oggetto contatore a 64 bit*</span><span class="sxs-lookup"><span data-stu-id="06882-189">*Set 64-bit counter object*</span></span>
- [<span data-ttu-id="06882-190">nx_snmp_object_end_of_mib</span><span class="sxs-lookup"><span data-stu-id="06882-190">nx_snmp_object_end_of_mib</span></span>](#nx_snmp_object_end_of_mib)
   - <span data-ttu-id="06882-191">*Impostare il valore di fine del MIB*</span><span class="sxs-lookup"><span data-stu-id="06882-191">*Set end-of-mib value*</span></span>
- [<span data-ttu-id="06882-192">nx_snmp_object_gauge_get</span><span class="sxs-lookup"><span data-stu-id="06882-192">nx_snmp_object_gauge_get</span></span>](#nx_snmp_object_gauge_get)
   - <span data-ttu-id="06882-193">*Ottenere un oggetto misuratore*</span><span class="sxs-lookup"><span data-stu-id="06882-193">*Get gauge object*</span></span>
- [<span data-ttu-id="06882-194">nx_snmp_object_gauge_set</span><span class="sxs-lookup"><span data-stu-id="06882-194">nx_snmp_object_gauge_set</span></span>](#nx_snmp_object_gauge_set)
   - <span data-ttu-id="06882-195">*Imposta oggetto misuratore*</span><span class="sxs-lookup"><span data-stu-id="06882-195">*Set gauge object*</span></span>
- [<span data-ttu-id="06882-196">nx_snmp_object_id_get</span><span class="sxs-lookup"><span data-stu-id="06882-196">nx_snmp_object_id_get</span></span>](#nx_snmp_object_id_get)
   - <span data-ttu-id="06882-197">*Ottieni ID oggetto*</span><span class="sxs-lookup"><span data-stu-id="06882-197">*Get object id*</span></span>
- [<span data-ttu-id="06882-198">nx_snmp_object_id_set</span><span class="sxs-lookup"><span data-stu-id="06882-198">nx_snmp_object_id_set</span></span>](#nx_snmp_object_id_set)
   - <span data-ttu-id="06882-199">*Imposta ID oggetto*</span><span class="sxs-lookup"><span data-stu-id="06882-199">*Set object id*</span></span>
- [<span data-ttu-id="06882-200">nx_snmp_object_integer_get</span><span class="sxs-lookup"><span data-stu-id="06882-200">nx_snmp_object_integer_get</span></span>](#nx_snmp_object_integer_get)
   - <span data-ttu-id="06882-201">*Ottenere un oggetto Integer*</span><span class="sxs-lookup"><span data-stu-id="06882-201">*Get integer object*</span></span>
- [<span data-ttu-id="06882-202">nx_snmp_object_integer_set</span><span class="sxs-lookup"><span data-stu-id="06882-202">nx_snmp_object_integer_set</span></span>](#nx_snmp_object_integer_set)
   - <span data-ttu-id="06882-203">*Imposta oggetto Integer*</span><span class="sxs-lookup"><span data-stu-id="06882-203">*Set integer object*</span></span>
- [<span data-ttu-id="06882-204">nx_snmp_object_ip_address_get</span><span class="sxs-lookup"><span data-stu-id="06882-204">nx_snmp_object_ip_address_get</span></span>](#nx_snmp_object_ip_address_get)
   - <span data-ttu-id="06882-205">*Ottenere l'oggetto indirizzo IP (solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="06882-205">*Get IP address object (IPv4 only)*</span></span>
- [<span data-ttu-id="06882-206">nx_snmp_object_ip_address_set</span><span class="sxs-lookup"><span data-stu-id="06882-206">nx_snmp_object_ip_address_set</span></span>](#nx_snmp_object_ip_address_set)
   - <span data-ttu-id="06882-207">*Imposta oggetto indirizzo IP (solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="06882-207">*Set IP address object (IPv4 only)*</span></span>
- [<span data-ttu-id="06882-208">nx_snmp_object_ipv6_address_get</span><span class="sxs-lookup"><span data-stu-id="06882-208">nx_snmp_object_ipv6_address_get</span></span>](#nx_snmp_object_ipv6_address_get)
   - <span data-ttu-id="06882-209">*Ottenere l'oggetto indirizzo IP (solo IPv6)*</span><span class="sxs-lookup"><span data-stu-id="06882-209">*Get IP address object (IPv6 only)*</span></span>
- [<span data-ttu-id="06882-210">nx_snmp_object_ipv6_address_set</span><span class="sxs-lookup"><span data-stu-id="06882-210">nx_snmp_object_ipv6_address_set</span></span>](#nx_snmp_object_ipv6_address_set)
   - <span data-ttu-id="06882-211">*Imposta oggetto indirizzo IP (solo IPv6)*</span><span class="sxs-lookup"><span data-stu-id="06882-211">*Set IP address object (IPv6 only)*</span></span>
- [<span data-ttu-id="06882-212">nx_snmp_object_no_instance</span><span class="sxs-lookup"><span data-stu-id="06882-212">nx_snmp_object_no_instance</span></span>](#nx_snmp_object_no_instance)
   - <span data-ttu-id="06882-213">*Imposta valore senza istanza*</span><span class="sxs-lookup"><span data-stu-id="06882-213">*Set no-instance value*</span></span>
- [<span data-ttu-id="06882-214">nx_snmp_object_not_found</span><span class="sxs-lookup"><span data-stu-id="06882-214">nx_snmp_object_not_found</span></span>](#nx_snmp_object_not_found)
   - <span data-ttu-id="06882-215">*Imposta valore non trovato*</span><span class="sxs-lookup"><span data-stu-id="06882-215">*Set not-found value*</span></span>
- [<span data-ttu-id="06882-216">nx_snmp_object_octet_string_get</span><span class="sxs-lookup"><span data-stu-id="06882-216">nx_snmp_object_octet_string_get</span></span>](#nx_snmp_object_octet_string_get)
   - <span data-ttu-id="06882-217">*Ottenere un oggetto stringa ottetto*</span><span class="sxs-lookup"><span data-stu-id="06882-217">*Get octet string object*</span></span>
- [<span data-ttu-id="06882-218">nx_snmp_object_octet_string_set</span><span class="sxs-lookup"><span data-stu-id="06882-218">nx_snmp_object_octet_string_set</span></span>](#nx_snmp_object_octet_string_set)
   - <span data-ttu-id="06882-219">*Imposta oggetto stringa ottetto*</span><span class="sxs-lookup"><span data-stu-id="06882-219">*Set octet string object*</span></span>
- [<span data-ttu-id="06882-220">nx_snmp_object_string_get</span><span class="sxs-lookup"><span data-stu-id="06882-220">nx_snmp_object_string_get</span></span>](#nx_snmp_object_string_get)
   - <span data-ttu-id="06882-221">*Ottenere un oggetto stringa ASCII*</span><span class="sxs-lookup"><span data-stu-id="06882-221">*Get ASCII string object*</span></span>
- [<span data-ttu-id="06882-222">nx_snmp_object_string_set</span><span class="sxs-lookup"><span data-stu-id="06882-222">nx_snmp_object_string_set</span></span>](#nx_snmp_object_string_set)
   - <span data-ttu-id="06882-223">*Imposta oggetto stringa ASCII*</span><span class="sxs-lookup"><span data-stu-id="06882-223">*Set ASCII string object*</span></span>
- [<span data-ttu-id="06882-224">nx_snmp_object_timetics_get</span><span class="sxs-lookup"><span data-stu-id="06882-224">nx_snmp_object_timetics_get</span></span>](#nx_snmp_object_timetics_get)
   - <span data-ttu-id="06882-225">*Ottenere l'oggetto timetics*</span><span class="sxs-lookup"><span data-stu-id="06882-225">*Get timetics object*</span></span>
- [<span data-ttu-id="06882-226">nx_snmp_object_timetics_set</span><span class="sxs-lookup"><span data-stu-id="06882-226">nx_snmp_object_timetics_set</span></span>](#nx_snmp_object_timetics_set)
   - <span data-ttu-id="06882-227">*Imposta oggetto timetics*</span><span class="sxs-lookup"><span data-stu-id="06882-227">*Set timetics object*</span></span>

## <a name="nx_snmp_agent_auth_trap_key_use"></a><span data-ttu-id="06882-228">nx_snmp_agent_auth_trap_key_use</span><span class="sxs-lookup"><span data-stu-id="06882-228">nx_snmp_agent_auth_trap_key_use</span></span>
<span data-ttu-id="06882-229">Specificare la chiave di autenticazione per i messaggi trap</span><span class="sxs-lookup"><span data-stu-id="06882-229">Specify authentication key for trap messages</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-230">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-230">Prototype</span></span>

```c
UINT nx_snmp_agent_auth_trap_key_use(NX_SNMP_AGENT *agent_ptr, 
                                     NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a><span data-ttu-id="06882-231">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-231">Description</span></span>

<span data-ttu-id="06882-232">Questo servizio specifica la chiave da utilizzare per l'impostazione dei parametri di autenticazione nell'intestazione di sicurezza SNMPv3 nei messaggi trap.</span><span class="sxs-lookup"><span data-stu-id="06882-232">This service specifies the key to be used for setting authentication parameters in the SNMPv3 security header in trap messages.</span></span> <span data-ttu-id="06882-233">Se si specifica un valore NX_NULL per la chiave, l'autenticazione viene disabilitata.</span><span class="sxs-lookup"><span data-stu-id="06882-233">Supplying a NX_NULL value for the key disables authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="06882-234">La chiave deve essere creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06882-234">The key must be previously created.</span></span> <span data-ttu-id="06882-235">Vedere nx_snmp_agent_md5_key_create o nx_snmp_agent_sha_key_create.</span><span class="sxs-lookup"><span data-stu-id="06882-235">See nx_snmp_agent_md5_key_create or nx_snmp_agent_sha_key_create.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-236">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-236">Input Parameters</span></span>

- <span data-ttu-id="06882-237">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-237">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-238">**chiave** di Puntatore a una chiave MD5 o SHA creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06882-238">**key** Pointer to a previously created MD5 or SHA key.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-239">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-239">Return Values</span></span>

- <span data-ttu-id="06882-240">Il set di chiavi di autenticazione **NX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="06882-240">**NX_SUCCESS** (0x00) Successful authentication key set.</span></span>
- <span data-ttu-id="06882-241">Sicurezza SNMP **NX_NOT_ENABLED** (0x14) disabilitata</span><span class="sxs-lookup"><span data-stu-id="06882-241">**NX_NOT_ENABLED** (0x14) SNMP Security disabled</span></span> 
- <span data-ttu-id="06882-242">**NX_PTR_ERROR** (0x07) puntatore a agente SNMP non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-242">**NX_PTR_ERROR** (0x07) Invalid SNMP Agent pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-243">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-243">Allowed From</span></span>

<span data-ttu-id="06882-244">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-244">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-245">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-245">Example</span></span>

```c
/* Use previously created “my_key” for SNMPv3 trap message authentication.  */
status =  nx_snmp_agent_auth_trap_key_use(&my_agent, &my_key);


/* If status is NX_SUCCESS the SNMP Agent will use “my_key” for
   for authentication parameters in trap messages.  */
```

## <a name="nx_snmp_agent_authenticate_key_use"></a><span data-ttu-id="06882-246">nx_snmp_agent_authenticate_key_use</span><span class="sxs-lookup"><span data-stu-id="06882-246">nx_snmp_agent_authenticate_key_use</span></span>
<span data-ttu-id="06882-247">Specificare la chiave di autenticazione per i messaggi di risposta</span><span class="sxs-lookup"><span data-stu-id="06882-247">Specify authentication key for response messages</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-248">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-248">Prototype</span></span>

```c
UINT nx_snmp_agent_authenticate_key_use(NX_SNMP_AGENT *agent_ptr, 
                                        NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a><span data-ttu-id="06882-249">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-249">Description</span></span>

<span data-ttu-id="06882-250">Questo servizio specifica la chiave da utilizzare per i parametri di autenticazione nel parametro di sicurezza SNMPv3 per tutte le richieste effettuate dopo l'impostazione.</span><span class="sxs-lookup"><span data-stu-id="06882-250">This service specifies the key to be used for authentication parameters in the SNMPv3 security parameter for all requests made after it is set.</span></span> <span data-ttu-id="06882-251">Se si specifica un valore NX_NULL per la chiave, l'autenticazione viene disabilitata.</span><span class="sxs-lookup"><span data-stu-id="06882-251">Supplying a NX_NULL value for the key disables authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="06882-252">La chiave deve essere creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06882-252">The key must be previously created.</span></span> <span data-ttu-id="06882-253">Vedere nx_snmp_agent_md5_key_create o nx_snmp_agent_sha_key_create.</span><span class="sxs-lookup"><span data-stu-id="06882-253">See nx_snmp_agent_md5_key_create or nx_snmp_agent_sha_key_create.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-254">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-254">Input Parameters</span></span>

- <span data-ttu-id="06882-255">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-255">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-256">**chiave** di Puntatore a una chiave MD5 o SHA creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06882-256">**key** Pointer to a previously created MD5 or SHA key.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-257">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-257">Return Values</span></span>

- <span data-ttu-id="06882-258">Il set di chiavi SNMP **NX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="06882-258">**NX_SUCCESS** (0x00) Successful SNMP key set.</span></span>
- <span data-ttu-id="06882-259">Sicurezza SNMP **NX_NOT_ENABLED** (0x14) disabilitata</span><span class="sxs-lookup"><span data-stu-id="06882-259">**NX_NOT_ENABLED** (0x14) SNMP Security disabled</span></span>
- <span data-ttu-id="06882-260">**NX_PTR_ERROR** (0x07) puntatore a agente SNMP non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-260">**NX_PTR_ERROR** (0x07) Invalid SNMP Agent pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-261">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-261">Allowed From</span></span>

<span data-ttu-id="06882-262">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-262">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-263">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-263">Example</span></span>

```c
/* Use previously created “my_key” for SNMPv3 authentication.  */
status =  nx_snmp_agent_authenticate_key_use(&my_agent, &my_key);


/* If status is NX_SUCCESS the SNMP Agent will use “my_key” for
   for setting the authentication parameters of SNMPv3 requests.  */
```

## <a name="nx_snmp_agent_community_get"></a><span data-ttu-id="06882-264">nx_snmp_agent_community_get</span><span class="sxs-lookup"><span data-stu-id="06882-264">nx_snmp_agent_community_get</span></span>
<span data-ttu-id="06882-265">Recupera nome comunità</span><span class="sxs-lookup"><span data-stu-id="06882-265">Retrieve community name</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-266">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-266">Prototype</span></span>

```c
UINT nx_snmp_agent_community_get(NX_SNMP_AGENT *agent_ptr, 
                                 UCHAR **community_string_ptr);
```

### <a name="description"></a><span data-ttu-id="06882-267">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-267">Description</span></span>

<span data-ttu-id="06882-268">Questo servizio recupera il nome della community dalla richiesta SNMP più recente ricevuta dall'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-268">This service retrieves the community name from the most recent SNMP request received by the SNMP Agent.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-269">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-269">Input Parameters</span></span>

- <span data-ttu-id="06882-270">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-270">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-271">**community_string_ptr** Puntatore a un puntatore di stringa per restituire la stringa della community dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-271">**community_string_ptr** Pointer to a string pointer to return the SNMP Agent community string.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-272">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-272">Return Values</span></span>

- <span data-ttu-id="06882-273">**NX_SUCCESS** (0x00) riuscita community SNMP Get.</span><span class="sxs-lookup"><span data-stu-id="06882-273">**NX_SUCCESS** (0x00) Successful SNMP community get.</span></span>
- <span data-ttu-id="06882-274">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-274">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-275">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-275">Allowed From</span></span>

<span data-ttu-id="06882-276">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-276">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-277">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-277">Example</span></span>

```c
UCHAR *string_ptr;

/* Pickup the community string pointer for my_agent.  */
status =  nx_snmp_agent_community_get(&my_agent, &string_ptr);


/* If status is NX_SUCCESS the pointer “string_ptr” points to the
   last community name supplied to the SNMP agent.  */
```

## <a name="nx_snmp_agent_request_get_type_test"></a><span data-ttu-id="06882-278">nx_snmp_agent_request_get_type_test</span><span class="sxs-lookup"><span data-stu-id="06882-278">nx_snmp_agent_request_get_type_test</span></span>
<span data-ttu-id="06882-279">Indica se l'ultima richiesta SNMP è GET o SET Type</span><span class="sxs-lookup"><span data-stu-id="06882-279">Indicate if last SNMP request is GET or SET type</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-280">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-280">Prototype</span></span>

```c
UINT nx_snmp_agent_request_get_type_test(NX_SNMP_AGENT *agent_ptr,
                                         UINT *is_get_type);
```

### <a name="description"></a><span data-ttu-id="06882-281">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-281">Description</span></span>

<span data-ttu-id="06882-282">Questo servizio indica se la richiesta più recente dal gestore SNMP è GET (GET, GetNext o GetBulk) o un tipo di SET.</span><span class="sxs-lookup"><span data-stu-id="06882-282">This service indicates if the most recent request from the SNMP Manager is a GET (GET, GETNEXT, or GETBULK) or SET type.</span></span> <span data-ttu-id="06882-283">È destinato all'uso con il callback del nome utente in cui l'applicazione SNMPv1 o SNMPv2 desidera confrontare la stringa della community ricevuta con la stringa pubblica dell'agente SNMP se la richiesta è un tipo GET o la stringa privata dell'agente SNMP se la richiesta è un tipo di SET.</span><span class="sxs-lookup"><span data-stu-id="06882-283">It is intended for use with the username callback where the SNMPv1 or SNMPv2 application will want to compare the received community string to the SNMP Agent public string if the request is a GET type, or to the SNMP Agent private string if the request is a SET type.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-284">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-284">Input Parameters</span></span>

- <span data-ttu-id="06882-285">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-285">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-286">**is_get_type** Puntatore allo stato del tipo di richiesta:</span><span class="sxs-lookup"><span data-stu-id="06882-286">**is_get_type** Pointer to request type status:</span></span>  
<span data-ttu-id="06882-287">NX_TRUE se GET Type</span><span class="sxs-lookup"><span data-stu-id="06882-287">NX_TRUE if GET type</span></span>  
<span data-ttu-id="06882-288">NX_FALSE se il tipo è impostato</span><span class="sxs-lookup"><span data-stu-id="06882-288">NX_FALSE if SET type</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-289">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-289">Return Values</span></span>

- <span data-ttu-id="06882-290">Il tipo restituito da **NX_SUCCESS** (0x00) è riuscito</span><span class="sxs-lookup"><span data-stu-id="06882-290">**NX_SUCCESS** (0x00) Successfully returned type</span></span>
- <span data-ttu-id="06882-291">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-291">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-292">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-292">Allowed From</span></span>

<span data-ttu-id="06882-293">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-293">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-294">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-294">Example</span></span>

```c
UINT is_get_type;

/* Determine if the current SNMP request is a GET or SET type.  */
status =  nx_snmp_agent_request_get_type_test(&my_agent, &is_get_type);


/* If status is NX_SUCCESS, is_get_type will indicate the request type.  */
```

## <a name="nx_snmp_agent_context_engine_set"></a><span data-ttu-id="06882-295">nx_snmp_agent_context_engine_set</span><span class="sxs-lookup"><span data-stu-id="06882-295">nx_snmp_agent_context_engine_set</span></span>
<span data-ttu-id="06882-296">Imposta motore di contesto (solo SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="06882-296">Set context engine (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-297">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-297">Prototype</span></span>

```c
UINT nx_snmp_agent_context_engine_set(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *context_engine, 
                                      UINT context_engine_size);
```
### <a name="description"></a><span data-ttu-id="06882-298">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-298">Description</span></span>

<span data-ttu-id="06882-299">Questo servizio imposta il motore di contesto dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-299">This service sets the context engine of the SNMP Agent.</span></span> <span data-ttu-id="06882-300">È applicabile solo per l'elaborazione SNMPv3.</span><span class="sxs-lookup"><span data-stu-id="06882-300">It is only applicable for SNMPv3 processing.</span></span> <span data-ttu-id="06882-301">Questa operazione deve essere chiamata prima di creare chiavi di sicurezza se l'applicazione usa l'autenticazione e la crittografia, perché l'ID del motore di contesto viene usato nel processo di creazione della chiave.</span><span class="sxs-lookup"><span data-stu-id="06882-301">This should be called before creating security keys if the application is using authentication and encryption, since the context engine ID is used in the key creation process.</span></span> <span data-ttu-id="06882-302">In caso contrario, NetX Duo SNMP fornisce un ID del motore di contesto predefinito nella parte superiore di *nxd_snmp. c:*</span><span class="sxs-lookup"><span data-stu-id="06882-302">If not, NetX Duo SNMP provides a default context engine id at the top of *nxd_snmp.c:*</span></span>

```c
UCHAR _nx_snmp_default_context_engine[NX_SNMP_MAX_CONTEXT_STRING] =  
                {0x80, 0x00, 0x03, 0x10, 0x01, 0xc0, 0xa8, 0x64, 0xaf};

```

### <a name="input-parameters"></a><span data-ttu-id="06882-303">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-303">Input Parameters</span></span>

- <span data-ttu-id="06882-304">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-304">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-305">**context_engine** Puntatore alla stringa del motore di contesto.</span><span class="sxs-lookup"><span data-stu-id="06882-305">**context_engine** Pointer to the context engine string.</span></span>
- <span data-ttu-id="06882-306">**context_engine_size** Dimensione della stringa del motore di contesto.</span><span class="sxs-lookup"><span data-stu-id="06882-306">**context_engine_size** Size of context engine string.</span></span> <span data-ttu-id="06882-307">Si noti che il numero massimo di byte in un motore di contesto è definito da NX_SNMP_MAX_CONTEXT_STRING.</span><span class="sxs-lookup"><span data-stu-id="06882-307">Note that the maximum number of bytes in a context engine is defined by NX_SNMP_MAX_CONTEXT_STRING.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-308">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-308">Return Values</span></span>

- <span data-ttu-id="06882-309">**NX_SUCCESS** (0x00) set di motori di contesto SNMP riusciti.</span><span class="sxs-lookup"><span data-stu-id="06882-309">**NX_SUCCESS** (0x00) Successful SNMP context engine set.</span></span>
- <span data-ttu-id="06882-310">**NX_NOT_ENABLED** (0X14) SNMPv3 non è abilitato</span><span class="sxs-lookup"><span data-stu-id="06882-310">**NX_NOT_ENABLED** (0x14) SNMPv3 is not enabled</span></span>
- <span data-ttu-id="06882-311">Errore di dimensioni del motore di contesto **NX_SNMP_ERROR** (0x100).</span><span class="sxs-lookup"><span data-stu-id="06882-311">**NX_SNMP_ERROR** (0x100) Context engine size error.</span></span>
- <span data-ttu-id="06882-312">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-312">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-313">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-313">Allowed From</span></span>

<span data-ttu-id="06882-314">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-314">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-315">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-315">Example</span></span>

```c
UCHAR my_engine[] = {0x80, 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07};

/* Set the context engine for my_agent.  */
status =  nx_snmp_agent_context_engine_set(&my_agent, my_engine, 9);


/* If status is NX_SUCCESS the context engine has been set.  */
```
## <a name="nx_snmp_agent_context_name_set"></a><span data-ttu-id="06882-316">nx_snmp_agent_context_name_set</span><span class="sxs-lookup"><span data-stu-id="06882-316">nx_snmp_agent_context_name_set</span></span>
<span data-ttu-id="06882-317">Imposta nome contesto (solo SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="06882-317">Set context name (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-318">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-318">Prototype</span></span>

```c
UINT nx_snmp_agent_context_name_set(NX_SNMP_AGENT *agent_ptr, 
                                    UCHAR *context_name, 
                                    UINT context_name_size);
```

### <a name="description"></a><span data-ttu-id="06882-319">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-319">Description</span></span>

<span data-ttu-id="06882-320">Questo servizio imposta il nome del contesto dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-320">This service sets the context name of the SNMP Agent.</span></span> <span data-ttu-id="06882-321">È applicabile solo per l'elaborazione SNMPv3.</span><span class="sxs-lookup"><span data-stu-id="06882-321">It is only applicable for SNMPv3 processing.</span></span> <span data-ttu-id="06882-322">Se non viene chiamato, NetX Duo SNMP Agent lascerà vuoto il nome del contesto.</span><span class="sxs-lookup"><span data-stu-id="06882-322">If not called, NetX Duo SNMP Agent will leave the context name blank.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-323">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-323">Input Parameters</span></span>

- <span data-ttu-id="06882-324">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-324">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-325">**context_name** Puntatore alla stringa del nome del contesto.</span><span class="sxs-lookup"><span data-stu-id="06882-325">**context_name** Pointer to the context name string.</span></span>
- <span data-ttu-id="06882-326">**context_name_size** Dimensione della stringa del nome del contesto.</span><span class="sxs-lookup"><span data-stu-id="06882-326">**context_name_size** Size of context name string.</span></span> <span data-ttu-id="06882-327">Si noti che il numero massimo di byte in un nome di contesto è definito da NX_SNMP_MAX_CONTEXT_STRING.</span><span class="sxs-lookup"><span data-stu-id="06882-327">Note that the maximum number of bytes in a context name is defined by NX_SNMP_MAX_CONTEXT_STRING.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-328">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-328">Return Values</span></span>

- <span data-ttu-id="06882-329">È stato impostato il nome del contesto SNMP **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="06882-329">**NX_SUCCESS** (0x00) Successful SNMP context name set.</span></span>
- <span data-ttu-id="06882-330">Errore nella dimensione del nome del contesto **NX_SNMP_ERROR** (0x100).</span><span class="sxs-lookup"><span data-stu-id="06882-330">**NX_SNMP_ERROR** (0x100) Context name size error.</span></span>
- <span data-ttu-id="06882-331">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-331">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-332">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-332">Allowed From</span></span>

<span data-ttu-id="06882-333">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-333">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-334">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-334">Example</span></span>

```c
/* Set the context name for my_agent.  */
status =  nx_snmp_agent_context_name_set(&my_agent, “my_context_name”, 15);


/* If status is NX_SUCCESS the context name has been set.  */
```

## <a name="nx_snmp_agent_create"></a><span data-ttu-id="06882-335">nx_snmp_agent_create</span><span class="sxs-lookup"><span data-stu-id="06882-335">nx_snmp_agent_create</span></span>
<span data-ttu-id="06882-336">Crea agente SNMP</span><span class="sxs-lookup"><span data-stu-id="06882-336">Create SNMP agent</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-337">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-337">Prototype</span></span>

```c
UINT nx_snmp_agent_create(NX_SNMP_AGENT *agent_ptr, 
      CHAR *snmp_agent_name, NX_IP *ip_ptr, VOID *stack_ptr, 
      ULONG stack_size, NX_PACKET_POOL *pool_ptr,
      UINT (*snmp_agent_username_process)(struct NX_SNMP_AGENT_STRUCT 
                                    *agent_ptr, UCHAR *username),
      UINT (*snmp_agent_get_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data),
      UINT (*snmp_agent_getnext_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data),
      UINT (*snmp_agent_set_process)(struct NX_SNMP_AGENT_STRUCT 
                  *agent_ptr, UCHAR *object_requested, 
                  NX_SNMP_OBJECT_DATA *object_data));
```
### <a name="description"></a><span data-ttu-id="06882-338">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-338">Description</span></span>

<span data-ttu-id="06882-339">Questo servizio crea un agente SNMP nell'istanza IP specificata.</span><span class="sxs-lookup"><span data-stu-id="06882-339">This service creates a SNMP Agent on the specified IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-340">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-340">Input Parameters</span></span>

- <span data-ttu-id="06882-341">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-341">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-342">**snmp_agent_name** Puntatore alla stringa del nome dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-342">**snmp_agent_name** Pointer to the SNMP Agent name string.</span></span>
- <span data-ttu-id="06882-343">**ip_ptr** Puntatore all'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="06882-343">**ip_ptr** Pointer to IP instance.</span></span>
- <span data-ttu-id="06882-344">**stack_ptr** Puntatore al puntatore dello stack del thread dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-344">**stack_ptr** Pointer to SNMP Agent thread stack pointer.</span></span>
- <span data-ttu-id="06882-345">**stack_size** Dimensioni dello stack in byte.</span><span class="sxs-lookup"><span data-stu-id="06882-345">**stack_size** Stack size in bytes.</span></span>
- <span data-ttu-id="06882-346">**pool_ptr** Puntatore al pool di pacchetti predefinito per l'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-346">**pool_ptr** Pointer the default packet pool for this SNMP Agent.</span></span>
- <span data-ttu-id="06882-347">**snmp_agent_username_process** Puntatore a funzione per la routine di gestione del nome utente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06882-347">**snmp_agent_username_process** Function pointer to application’s username handling routine.</span></span>
- <span data-ttu-id="06882-348">**snmp_agent_get_process** Puntatore a funzione per la routine di gestione delle richieste GET dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06882-348">**snmp_agent_get_process** Function pointer to application’s GET request handling routine.</span></span>
- <span data-ttu-id="06882-349">**snmp_agent_getnext_process** Puntatore della funzione alla routine di gestione delle richieste GetNext dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06882-349">**snmp_agent_getnext_process** Function pointer to application’s GETNEXT request handling routine.</span></span>
- <span data-ttu-id="06882-350">**snmp_agent_set_process** Puntatore a funzione per la routine di gestione delle richieste SET dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="06882-350">**snmp_agent_set_process** Function pointer to application’s SET request handling routine.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-351">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-351">Return Values</span></span>

- <span data-ttu-id="06882-352">Creazione dell'agente SNMP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="06882-352">**NX_SUCCESS** (0x00) Successful SNMP Agent create.</span></span>
- <span data-ttu-id="06882-353">Errore di creazione dell'agente SNMP **NX_SNMP_ERROR** (0x100).</span><span class="sxs-lookup"><span data-stu-id="06882-353">**NX_SNMP_ERROR** (0x100) SNMP Agent create error.</span></span>
- <span data-ttu-id="06882-354">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-354">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-355">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-355">Allowed From</span></span>

<span data-ttu-id="06882-356">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-356">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-357">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-357">Example</span></span>

```c
NX_SNMP_AGENT my_agent;

/* Create the SNMP Agent “my_agent.”  */
status =  nx_snmp_agent_create(&my_agent, "My SNMP Agent", &ip_0, stack_start_ptr,
                4096, &pool_0, my_username_processing, my_get_processing, 
                my_getnext_processing, my_set_processing);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been created.  */
```

## <a name="nx_snmp_agent_current_version_get"></a><span data-ttu-id="06882-358">nx_snmp_agent_current_version_get</span><span class="sxs-lookup"><span data-stu-id="06882-358">nx_snmp_agent_current_version_get</span></span>
<span data-ttu-id="06882-359">Ottenere la versione del pacchetto SNMP</span><span class="sxs-lookup"><span data-stu-id="06882-359">Get the SNMP packet version</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-360">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-360">Prototype</span></span>

```c
UINT nx_snmp_agent_current_version_get(NX_SNMP_AGENT *agent_ptr, 
                                       UINT *version);
```

### <a name="description"></a><span data-ttu-id="06882-361">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-361">Description</span></span>

<span data-ttu-id="06882-362">Questo servizio recupera la versione SNMP analizzata dal pacchetto SNMP più recente ricevuto.</span><span class="sxs-lookup"><span data-stu-id="06882-362">This service retrieves the SNMP version parsed from the most recent SNMP packet received.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-363">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-363">Input Parameters</span></span>

- <span data-ttu-id="06882-364">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-364">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-365">**versione** di Puntatore alla versione SNMP analizzata dal pacchetto SNMP ricevuto</span><span class="sxs-lookup"><span data-stu-id="06882-365">**version** Pointer to the SNMP version parsed from received SNMP packet</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-366">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-366">Return Values</span></span>

- <span data-ttu-id="06882-367">**NX_SUCCESS** (0x00) versione SNMP riuscita Get</span><span class="sxs-lookup"><span data-stu-id="06882-367">**NX_SUCCESS** (0x00) Successful SNMP version get</span></span>
- <span data-ttu-id="06882-368">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="06882-368">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-369">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-369">Allowed From</span></span>

<span data-ttu-id="06882-370">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-370">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-371">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-371">Example</span></span>

```c
UINT          snmp_version;
NX_SNMP_AGENT my_agent;

/* Get the version of the last received SNMP packet. */
status =  nx_snmp_agent_current_version_get (&my_agent, &snmp_version);


/* If status is NX_SUCCESS, snmp_version contains 
   the received packet SNMP version.  */
```

## <a name="nx_snmp_agent_private_string_test"></a><span data-ttu-id="06882-372">nx_snmp_agent_private_string_test</span><span class="sxs-lookup"><span data-stu-id="06882-372">nx_snmp_agent_private_string_test</span></span>
<span data-ttu-id="06882-373">Verificare che la stringa privata corrisponda alla stringa privata dell'agente</span><span class="sxs-lookup"><span data-stu-id="06882-373">Verify private string matches Agent private string</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-374">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-374">Prototype</span></span>

```c
UINT nx_snmp_agent_private_string_test(NX_SNMP_AGENT *agent_ptr, 
                                       UCHAR *community_string,          
                                       UINT *is_private);
```

### <a name="description"></a><span data-ttu-id="06882-375">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-375">Description</span></span>

<span data-ttu-id="06882-376">Questo servizio confronta la stringa della comunità di input con terminazione null con la stringa privata dell'agente SNMP e indica se corrispondono.</span><span class="sxs-lookup"><span data-stu-id="06882-376">This service compares the null terminated input community string with the SNMP agent private string and indicates if they match.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-377">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-377">Input Parameters</span></span>

- <span data-ttu-id="06882-378">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-378">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-379">**community_string** Puntatore alla stringa da confrontare</span><span class="sxs-lookup"><span data-stu-id="06882-379">**community_string** Pointer to string to compare</span></span>
- <span data-ttu-id="06882-380">**is_private** Puntatore al risultato del confronto</span><span class="sxs-lookup"><span data-stu-id="06882-380">**is_private** Pointer to result of comparison</span></span>  
<span data-ttu-id="06882-381">Corrispondenze NX_TRUE-stringa</span><span class="sxs-lookup"><span data-stu-id="06882-381">NX_TRUE - string matches</span></span>  
<span data-ttu-id="06882-382">NX_FALSE stringa non corrisponde</span><span class="sxs-lookup"><span data-stu-id="06882-382">NX_FALSE - string does not match</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-383">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-383">Return Values</span></span>

- <span data-ttu-id="06882-384">Confronto tra **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="06882-384">**NX_SUCCESS** (0x00) Successful comparison</span></span>
- <span data-ttu-id="06882-385">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="06882-385">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-386">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-386">Allowed From</span></span>

<span data-ttu-id="06882-387">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-387">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-388">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-388">Example</span></span>

```c
UINT        is_private;
UCHAR       *community_string_ptr;
NX_SNMP_AGENT   my_agent;

/* Determine if the community string matches the agent private string */
status =  nx_snmp_agent_private_string_test(&my_agent, community_string_ptr,  
                                            &is_private);


/* If status is NX_SUCCESS, is_private will indicate if there is a match. 
   If is_private is NX_TRUE, they match.  */
```

## <a name="nx_snmp_agent_public_string_test"></a><span data-ttu-id="06882-389">nx_snmp_agent_public_string_test</span><span class="sxs-lookup"><span data-stu-id="06882-389">nx_snmp_agent_public_string_test</span></span>
<span data-ttu-id="06882-390">Verificare che la stringa pubblica ricevuta corrisponda alla stringa pubblica dell'agente</span><span class="sxs-lookup"><span data-stu-id="06882-390">Verify received public string matches Agent’s public string</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-391">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-391">Prototype</span></span>

```c
UINT nx_snmp_agent_public_string_test(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *community_string,          
                                      UINT *is_public);
```
### <a name="description"></a><span data-ttu-id="06882-392">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-392">Description</span></span>

<span data-ttu-id="06882-393">Questo servizio confronta una stringa della community di input con terminazione null con la stringa pubblica dell'agente SNMP e indica se corrispondono.</span><span class="sxs-lookup"><span data-stu-id="06882-393">This service compares a null terminated input community string with the SNMP agent public string and indicates if they match.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-394">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-394">Input Parameters</span></span>

- <span data-ttu-id="06882-395">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-395">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-396">**community_string** Puntatore alla stringa da confrontare</span><span class="sxs-lookup"><span data-stu-id="06882-396">**community_string** Pointer to string to compare</span></span>
- <span data-ttu-id="06882-397">**is_public** Puntatore al risultato del confronto</span><span class="sxs-lookup"><span data-stu-id="06882-397">**is_public** Pointer to result of comparison</span></span>  
<span data-ttu-id="06882-398">Corrispondenze NX_TRUE-stringa</span><span class="sxs-lookup"><span data-stu-id="06882-398">NX_TRUE - string matches</span></span>  
<span data-ttu-id="06882-399">NX_FALSE stringa non corrisponde</span><span class="sxs-lookup"><span data-stu-id="06882-399">NX_FALSE - string does not match</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-400">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-400">Return Values</span></span>

- <span data-ttu-id="06882-401">Confronto tra **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="06882-401">**NX_SUCCESS** (0x00) Successful comparison</span></span>
- <span data-ttu-id="06882-402">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="06882-402">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-403">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-403">Allowed From</span></span>

<span data-ttu-id="06882-404">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-404">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-405">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-405">Example</span></span>

```c
UINT        is_public;
UCHAR       *community_string_ptr;
NX_SNMP_AGENT   my_agent;


/* Determine if the community string matches the agent public string */
status =  nx_snmp_agent_public_string_test(&my_agent, community_string_ptr,  
                                           &is_public);


/* If status is NX_SUCCESS, is_public will indicate if there is a match. 
   If is_public is true they match.  */
```

## <a name="nx_snmp_agent_version_set"></a><span data-ttu-id="06882-406">nx_snmp_agent_version_set</span><span class="sxs-lookup"><span data-stu-id="06882-406">nx_snmp_agent_version_set</span></span>
<span data-ttu-id="06882-407">Impostare lo stato dell'agente SNMP per ogni versione SNMP</span><span class="sxs-lookup"><span data-stu-id="06882-407">Set the SNMP agent status for each SNMP version</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-408">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-408">Prototype</span></span>

```c
UINT nx_snmp_agent_version_set(NX_SNMP_AGENT *agent_ptr, 
                               UINT enabled_v1, UINT enable_v2, 
                               UINT enable_v3);
```

### <a name="description"></a><span data-ttu-id="06882-409">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-409">Description</span></span>

<span data-ttu-id="06882-410">Questo servizio imposta lo stato (abilitato/disabilitato) per ogni versione di SNMP, V1, V2 e V3 nell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-410">This service sets the status (enabled/disabled) for each of the SNMP versions, V1, V2 and V3 on the SNMP agent.</span></span> <span data-ttu-id="06882-411">Si noti che le opzioni configurabili dall'utente, NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2 e NX_SNMP_DISABLE_V3, sostituiranno le impostazioni di Runtime.</span><span class="sxs-lookup"><span data-stu-id="06882-411">Note that the user configurable options, NX_SNMP_DISABLE_V1, NX_SNMP_DISABLE_V2, and NX_SNMP_DISABLE_V3, will override these run time settings.</span></span> <span data-ttu-id="06882-412">Per impostazione predefinita, l'agente SNMP è abilitato per tutte e tre le versioni.</span><span class="sxs-lookup"><span data-stu-id="06882-412">By default, the SNMP agent is enabled for all three versions.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-413">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-413">Input Parameters</span></span>

- <span data-ttu-id="06882-414">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-414">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-415">**enabled_v1** Imposta lo stato abilitato per SNMP v1 su on/off.</span><span class="sxs-lookup"><span data-stu-id="06882-415">**enabled_v1** Sets enabled status for SNMP V1 to on/off.</span></span>
- <span data-ttu-id="06882-416">**enabled_v2** Imposta lo stato abilitato per SNMP v2 su on/off.</span><span class="sxs-lookup"><span data-stu-id="06882-416">**enabled_v2** Sets enabled status for SNMP V2 to on/off.</span></span>
- <span data-ttu-id="06882-417">**enabled_v3** Imposta lo stato abilitato per SNMP v3 su on/off.</span><span class="sxs-lookup"><span data-stu-id="06882-417">**enabled_v3** Sets enabled status for SNMP V3 to on/off.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-418">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-418">Return Values</span></span>

- <span data-ttu-id="06882-419">Set di versioni SNMP **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="06882-419">**NX_SUCCESS** (0x00) Successful SNMP version set</span></span>
- <span data-ttu-id="06882-420">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="06882-420">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-421">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-421">Allowed From</span></span>

<span data-ttu-id="06882-422">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-422">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-423">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-423">Example</span></span>

```c
UINT          v1_on = NX_TRUE;
UINT          v2_on = NX_TRUE;
UINT          v3_on = NX_FALSE;

NX_SNMP_AGENT my_agent;

/* Enable/Disable each SNMP protocol (version) for the SNMP Agent) */
status =  nx_snmp_agent_version_set(&my_agent, v1_on, v2_on, v3_on);


/* If status is NX_SUCCESS, my_agent is enabled only for V1 and V2 assuming 
   NX_SNMP_DISABLE_V1 and NX_SNMP_DISABLE_V2 are not defined. */
```

## <a name="nx_snmp_agent_private_string_set"></a><span data-ttu-id="06882-424">nx_snmp_agent_private_string_set</span><span class="sxs-lookup"><span data-stu-id="06882-424">nx_snmp_agent_private_string_set</span></span>
<span data-ttu-id="06882-425">Imposta la stringa privata dell'agente SNMP</span><span class="sxs-lookup"><span data-stu-id="06882-425">Set the SNMP agent private string</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-426">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-426">Prototype</span></span>

```c
UINT nx_snmp_agent_private_string_set(NX_SNMP_AGENT *agent_ptr, 
                                      UCHAR *community_string);
```

### <a name="description"></a><span data-ttu-id="06882-427">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-427">Description</span></span>

<span data-ttu-id="06882-428">Questo servizio imposta la stringa della comunità privata dell'agente SNMP con la stringa con terminazione null di input.</span><span class="sxs-lookup"><span data-stu-id="06882-428">This service sets the SNMP agent private community string with the input null terminated string.</span></span> <span data-ttu-id="06882-429">Il valore predefinito è NULL (nessuna stringa privata impostata), in modo che qualsiasi pacchetto SNMP ricevuto con una stringa della community "privata" non verrà accettato dall'agente SNMP per l'accesso in lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="06882-429">The default value is NULL (no private string set), such that any SNMP packet received with a “private” community string will not be accepted by the SNMP agent for read/write access.</span></span> <span data-ttu-id="06882-430">La stringa di input deve essere minore o uguale a quella configurabile dall'utente NX_SNMP_MAX_USER_NAME-1 (per consentire la risoluzione di spazio per la terminazione null).</span><span class="sxs-lookup"><span data-stu-id="06882-430">The input string must be less than or equal to the user configurable NX_SNMP_MAX_USER_NAME-1 (to allow room for null termination) size.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-431">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-431">Input Parameters</span></span>

- <span data-ttu-id="06882-432">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-432">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-433">**community_string** Puntatore alla stringa privata da assegnare</span><span class="sxs-lookup"><span data-stu-id="06882-433">**community_string** Pointer to the private string to assign</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-434">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-434">Return Values</span></span>

- <span data-ttu-id="06882-435">**NX_SUCCESS** (0x00) ha impostato correttamente una stringa privata</span><span class="sxs-lookup"><span data-stu-id="06882-435">**NX_SUCCESS** (0x00) Successfully set private string</span></span>
- <span data-ttu-id="06882-436">Dimensioni stringa **NX_SNMP_ERROR_TOOBIG** (0x01) troppo grandi</span><span class="sxs-lookup"><span data-stu-id="06882-436">**NX_SNMP_ERROR_TOOBIG** (0x01) String size too large</span></span> 
- <span data-ttu-id="06882-437">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="06882-437">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-438">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-438">Allowed From</span></span>

<span data-ttu-id="06882-439">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-439">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-440">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-440">Example</span></span>

```c
NX_SNMP_AGENT my_agent;

/* Set the SNMP agent’s private community string */
status =  nx_snmp_agent_private_string_set(&my_agent, “private”));


/* If status is NX_SUCCESS, the SNMP agent private string is set.  */
```

## <a name="nx_snmp_agent_public_string_set"></a><span data-ttu-id="06882-441">nx_snmp_agent_public_string_set</span><span class="sxs-lookup"><span data-stu-id="06882-441">nx_snmp_agent_public_string_set</span></span>
<span data-ttu-id="06882-442">Imposta la stringa pubblica dell'agente SNMP</span><span class="sxs-lookup"><span data-stu-id="06882-442">Set the SNMP agent public string</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-443">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-443">Prototype</span></span>

```c
UINT nx_snmp_agent_public_string_set(NX_SNMP_AGENT *agent_ptr, 
                                     UCHAR *community_string);
```

### <a name="description"></a><span data-ttu-id="06882-444">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-444">Description</span></span>

<span data-ttu-id="06882-445">Questo servizio imposta la stringa della comunità pubblica dell'agente SNMP con la stringa con terminazione null di input.</span><span class="sxs-lookup"><span data-stu-id="06882-445">This service sets the SNMP agent public community string with the input null terminated string.</span></span> <span data-ttu-id="06882-446">La stringa community deve essere minore o uguale a quella configurabile dall'utente NX_SNMP_MAX_USER_NAME-1 (per consentire la risoluzione di spazio per la terminazione null).</span><span class="sxs-lookup"><span data-stu-id="06882-446">The community string must be less than or equal to the user configurable NX_SNMP_MAX_USER_NAME-1 (to allow room for null termination) size.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-447">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-447">Input Parameters</span></span>

- <span data-ttu-id="06882-448">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-448">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-449">**community_string** Puntatore alla stringa pubblica da assegnare</span><span class="sxs-lookup"><span data-stu-id="06882-449">**community_string** Pointer to the public string to assign</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-450">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-450">Return Values</span></span>

- <span data-ttu-id="06882-451">**NX_SUCCESS** (0x00) ha impostato correttamente una stringa pubblica</span><span class="sxs-lookup"><span data-stu-id="06882-451">**NX_SUCCESS** (0x00) Successfully set public string</span></span>
- <span data-ttu-id="06882-452">Dimensioni stringa **NX_SNMP_ERROR_TOOBIG** (0x01) troppo grandi</span><span class="sxs-lookup"><span data-stu-id="06882-452">**NX_SNMP_ERROR_TOOBIG** (0x01) String size too large</span></span>
- <span data-ttu-id="06882-453">**NX_PTR_ERROR** (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="06882-453">**NX_PTR_ERROR** (0x07) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-454">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-454">Allowed From</span></span>

<span data-ttu-id="06882-455">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-455">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-456">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-456">Example</span></span>

```c
NX_SNMP_AGENT my_agent;

/* Set the SNMP agent’s public string. */
nx_snmp_agent_public_string_set(&my_agent, “my_public”));


/* If status is NX_SUCCESS, the SNMP agent public string is set.  */
```

## <a name="nx_snmp_agent_delete"></a><span data-ttu-id="06882-457">nx_snmp_agent_delete</span><span class="sxs-lookup"><span data-stu-id="06882-457">nx_snmp_agent_delete</span></span>
<span data-ttu-id="06882-458">Elimina agente SNMP</span><span class="sxs-lookup"><span data-stu-id="06882-458">Delete SNMP agent</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-459">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-459">Prototype</span></span>

```C
UINT nx_snmp_agent_delete(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a><span data-ttu-id="06882-460">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-460">Description</span></span>

<span data-ttu-id="06882-461">Questo servizio Elimina un agente SNMP creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06882-461">This service deletes a previously created SNMP Agent.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-462">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-462">Input Parameters</span></span>

- <span data-ttu-id="06882-463">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-463">**agent_ptr** Pointer to SNMP Agent control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-464">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-464">Return Values</span></span>

- <span data-ttu-id="06882-465">Eliminazione dell'agente SNMP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="06882-465">**NX_SUCCESS** (0x00) Successful SNMP Agent delete.</span></span>
- <span data-ttu-id="06882-466">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-466">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-467">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-467">Allowed From</span></span>

<span data-ttu-id="06882-468">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-468">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-469">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-469">Example</span></span>

```c
/* Delete the SNMP Agent “my_agent.”  */
status =  nx_snmp_agent_delete(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been deleted.  */
```

## <a name="nx_snmp_agent_set_interface"></a><span data-ttu-id="06882-470">nx_snmp_agent_set_interface</span><span class="sxs-lookup"><span data-stu-id="06882-470">nx_snmp_agent_set_interface</span></span>
<span data-ttu-id="06882-471">Impostazione dell'interfaccia di rete dell'agente SNMP</span><span class="sxs-lookup"><span data-stu-id="06882-471">Set the SNMP agent network interface</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-472">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-472">Prototype</span></span>

```c
UINT nx_snmp_agent_set_interface(NX_SNMP_AGENT *agent_ptr,  
                                 UINT if_index);
```

### <a name="description"></a><span data-ttu-id="06882-473">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-473">Description</span></span>

<span data-ttu-id="06882-474">Questo servizio imposta l'interfaccia di rete SNMP per l'agente SNMP come specificato dall'indice dell'interfaccia di input.</span><span class="sxs-lookup"><span data-stu-id="06882-474">This service sets the SNMP network interface for the SNMP Agent as specified by the input interface index.</span></span> <span data-ttu-id="06882-475">Questa opzione è utile solo per le applicazioni host SNMP con NetX Duo 5,6 o versioni successive che supportano più interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="06882-475">This is only useful for SNMP host applications with NetX Duo 5.6 or higher which support multiple network interfaces.</span></span> <span data-ttu-id="06882-476">Il valore predefinito se non è specificato dall'host è zero, per l'interfaccia primaria.</span><span class="sxs-lookup"><span data-stu-id="06882-476">The default value if not specified by the host is zero, for the primary interface.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-477">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-477">Input Parameters</span></span>

- <span data-ttu-id="06882-478">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-478">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-479">**If_index** Indice che specifica l'interfaccia SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-479">**If_index** Index specifying the SNMP interface.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-480">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-480">Return Values</span></span>

- <span data-ttu-id="06882-481">Il set di interfacce SNMP **NX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="06882-481">**NX_SUCCESS** (0x00) Successful SNMP interface set.</span></span>
- <span data-ttu-id="06882-482">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-482">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-483">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-483">Allowed From</span></span>

<span data-ttu-id="06882-484">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-484">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-485">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-485">Example</span></span>

```c
/* Set the SNMP Agent “my_agent” to the secondary interface.  */
if_index = 1;
status =  nx_snmp_agent_set_interface(&my_agent, if_index);


/* If status is NX_SUCCESS the SNMP agent interface is set.  */
```

## <a name="nx_snmp_agent_md5_key_create"></a><span data-ttu-id="06882-486">nx_snmp_agent_md5_key_create</span><span class="sxs-lookup"><span data-stu-id="06882-486">nx_snmp_agent_md5_key_create</span></span>
<span data-ttu-id="06882-487">Crea chiave MD5 (solo SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="06882-487">Create md5 key (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-488">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-488">Prototype</span></span>

```c
UINT nx_snmp_agent_md5_key_create(NX_SNMP_AGENT *agent_ptr, 
                                  UCHAR *password, 
                                  NX_SNMP_SECURITY_KEY 
                                       *destination_key);
```
### <a name="description"></a><span data-ttu-id="06882-489">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-489">Description</span></span>

<span data-ttu-id="06882-490">Questo servizio crea una chiave MD5 che può essere usata per l'autenticazione e la crittografia.</span><span class="sxs-lookup"><span data-stu-id="06882-490">This service creates a MD5 key that can be used for authentication and encryption.</span></span>

<span data-ttu-id="06882-491">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="06882-491">This service is deprecated.</span></span> <span data-ttu-id="06882-492">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_snmp_agent_md5_key_create_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="06882-492">Developers are encouraged to migrate to *nx_snmp_agent_md5_key_create_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-493">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-493">Input Parameters</span></span>

- <span data-ttu-id="06882-494">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-494">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-495">**password** di Puntatore alla stringa della password.</span><span class="sxs-lookup"><span data-stu-id="06882-495">**password** Pointer to password string.</span></span>
- <span data-ttu-id="06882-496">**destination_key** Puntatore alla struttura dei dati della chiave SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-496">**destination_key** Pointer to SNMP key data structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-497">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-497">Return Values</span></span>

- <span data-ttu-id="06882-498">Creazione chiave riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="06882-498">**NX_SUCCESS** (0x00) Successful key create.</span></span>
- <span data-ttu-id="06882-499">Sicurezza **NX_NOT_ENABLED** (0x14) non abilitata.</span><span class="sxs-lookup"><span data-stu-id="06882-499">**NX_NOT_ENABLED** (0x14) Security not enabled.</span></span>
- <span data-ttu-id="06882-500">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-500">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-501">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-501">Allowed From</span></span>

<span data-ttu-id="06882-502">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-502">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-503">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-503">Example</span></span>

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the MD5 key for “my_agent.”   */
status =  nx_snmp_agent_md5_key_create(&my_agent, “authpw”, &my_key);


/* If status is NX_SUCCESS an MD5 key has been created.  */
```

## <a name="nx_snmp_agent_md5_key_create_extended"></a><span data-ttu-id="06882-504">nx_snmp_agent_md5_key_create_extended</span><span class="sxs-lookup"><span data-stu-id="06882-504">nx_snmp_agent_md5_key_create_extended</span></span>
<span data-ttu-id="06882-505">Crea chiave MD5 (solo SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="06882-505">Create md5 key (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-506">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-506">Prototype</span></span>

```c
UINT nx_snmp_agent_md5_key_create_extended(NX_SNMP_AGENT *agent_ptr, 
                                           UCHAR *password, 
                                           UINT password_length,
                                           NX_SNMP_SECURITY_KEY 
                                           *destination_key);
```
### <a name="description"></a><span data-ttu-id="06882-507">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-507">Description</span></span>

<span data-ttu-id="06882-508">Questo servizio crea una chiave MD5 che può essere usata per l'autenticazione e la crittografia.</span><span class="sxs-lookup"><span data-stu-id="06882-508">This service creates a MD5 key that can be used for authentication and encryption.</span></span>

<span data-ttu-id="06882-509">Questo servizio sostituisce *nx_snmp_agent_md5_key_create ().*</span><span class="sxs-lookup"><span data-stu-id="06882-509">This service replaces *nx_snmp_agent_md5_key_create().*</span></span> <span data-ttu-id="06882-510">Per questa versione è necessario che il chiamante fornisca la lunghezza della password.</span><span class="sxs-lookup"><span data-stu-id="06882-510">This version requires caller to supply password length.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-511">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-511">Input Parameters</span></span>

- <span data-ttu-id="06882-512">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-512">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-513">**password** di Puntatore alla stringa della password.</span><span class="sxs-lookup"><span data-stu-id="06882-513">**password** Pointer to password string.</span></span>
- <span data-ttu-id="06882-514">**password_length** Lunghezza della stringa della password.</span><span class="sxs-lookup"><span data-stu-id="06882-514">**password_length** Length of password string.</span></span>
- <span data-ttu-id="06882-515">**destination_key** Puntatore alla struttura dei dati della chiave SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-515">**destination_key** Pointer to SNMP key data structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-516">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-516">Return Values</span></span>

- <span data-ttu-id="06882-517">Creazione chiave riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="06882-517">**NX_SUCCESS** (0x00) Successful key create.</span></span>
- <span data-ttu-id="06882-518">Sicurezza **NX_NOT_ENABLED** (0x14) non abilitata.</span><span class="sxs-lookup"><span data-stu-id="06882-518">**NX_NOT_ENABLED** (0x14) Security not enabled.</span></span>
- <span data-ttu-id="06882-519">SNMP **NX_SNMP_FAILED** (0x102) non riuscito.</span><span class="sxs-lookup"><span data-stu-id="06882-519">**NX_SNMP_FAILED** (0x102) SNMP failed.</span></span>
- <span data-ttu-id="06882-520">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-520">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-521">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-521">Allowed From</span></span>

<span data-ttu-id="06882-522">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-522">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-523">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-523">Example</span></span>

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the MD5 key for “my_agent.”   */
status =  nx_snmp_agent_md5_key_create_extended(&my_agent, “authpw”, 6, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_priv_trap_key_use"></a><span data-ttu-id="06882-524">nx_snmp_agent_priv_trap_key_use</span><span class="sxs-lookup"><span data-stu-id="06882-524">nx_snmp_agent_priv_trap_key_use</span></span>
<span data-ttu-id="06882-525">Specificare la chiave di crittografia per i messaggi trap</span><span class="sxs-lookup"><span data-stu-id="06882-525">Specify encryption key for trap messages</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-526">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-526">Prototype</span></span>

```c
UINT nx_snmp_agent_priv_trap_key_use(NX_SNMP_AGENT *agent_ptr, 
                                     NX_SNMP_SECURITY_KEY *key);
```

### <a name="description"></a><span data-ttu-id="06882-527">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-527">Description</span></span>

<span data-ttu-id="06882-528">Questo servizio specifica che è necessario usare una chiave per la privacy creata in precedenza per la crittografia e la decrittografia dei messaggi trap SNMPv3.</span><span class="sxs-lookup"><span data-stu-id="06882-528">This service specifies that a previously created privacy key is to be used for encryption and decryption of SNMPv3 trap messages.</span></span>

> [!NOTE]
> <span data-ttu-id="06882-529">*È necessario creare una chiave authentictation in precedenza. Per la privacy SNMP v3 (crittografia) è richiesta l'autenticazione. Per informazioni dettagliate, vedere nx_snmp_agent_auth_trap_key_use.*</span><span class="sxs-lookup"><span data-stu-id="06882-529">*An authentictation key must be previously created. SNMP v3 privacy (encryption) requires authentication. See nx_snmp_agent_auth_trap_key_use for details.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-530">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-530">Input Parameters</span></span>

- <span data-ttu-id="06882-531">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-531">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-532">**chiave** di Puntatore alla chiave create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06882-532">**key** Pointer to previously create key.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-533">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-533">Return Values</span></span>

- <span data-ttu-id="06882-534">Il set di chiavi per la privacy **NX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="06882-534">**NX_SUCCESS** (0x00) Successful privacy key set.</span></span>
- <span data-ttu-id="06882-535">Sicurezza **NX_NOT_ENABLED** (0x14) non abilitata.</span><span class="sxs-lookup"><span data-stu-id="06882-535">**NX_NOT_ENABLED** (0x14) Security not enabled.</span></span>
- <span data-ttu-id="06882-536">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-536">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-537">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-537">Allowed From</span></span>

<span data-ttu-id="06882-538">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-538">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-539">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-539">Example</span></span>

```c
/* Use the “my_privacy_key” for the SNMP Agent “my_agent” trap messages.   */
status =  nx_snmp_agent_priv_trap_key_use(&my_agent, &my_privacy_key);


/* If status is NX_SUCCESS the privacy key is registered with the SNMP agent.  */
```

## <a name="nx_snmp_agent_privacy_key_use"></a><span data-ttu-id="06882-540">nx_snmp_agent_privacy_key_use</span><span class="sxs-lookup"><span data-stu-id="06882-540">nx_snmp_agent_privacy_key_use</span></span>
<span data-ttu-id="06882-541">Specificare la chiave di crittografia per i messaggi di risposta</span><span class="sxs-lookup"><span data-stu-id="06882-541">Specify encryption key for response messages</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-542">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-542">Prototype</span></span>

```c
UINT nx_snmp_agent_privacy_key_use(NX_SNMP_AGENT *agent_ptr, 
                                   NX_SNMP_SECURITY_KEY *key);
```
### <a name="description"></a><span data-ttu-id="06882-543">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-543">Description</span></span>

<span data-ttu-id="06882-544">Questo servizio specifica che la chiave creata in precedenza deve essere utilizzata per la crittografia e la decrittografia dei messaggi di risposta SNMPv3.</span><span class="sxs-lookup"><span data-stu-id="06882-544">This service specifies that the previously created key is to be used for encryption and decryption of SNMPv3 response messages.</span></span>

> [!NOTE]
> <span data-ttu-id="06882-545">*È necessario che sia stata specificata in precedenza una chiave di autenticazione. La crittografia SNMP V3 richiede anche la creazione di una chiave di autenticazione. Per informazioni dettagliate, vedere nx_snmp_agent_authentiation_key_use.*</span><span class="sxs-lookup"><span data-stu-id="06882-545">*An authentication key must have previously been specified. SNMP v3 encryption requires creation of an authentication key as well. See nx_snmp_agent_authentiation_key_use for details.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-546">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-546">Input Parameters</span></span>

- <span data-ttu-id="06882-547">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-547">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-548">**chiave** di Puntatore alla chiave create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06882-548">**key** Pointer to previously create key.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-549">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-549">Return Values</span></span>

- <span data-ttu-id="06882-550">Il set di chiavi per la privacy **NX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="06882-550">**NX_SUCCESS** (0x00) Successful privacy key set.</span></span>
- <span data-ttu-id="06882-551">Sicurezza **NX_NOT_ENABLED** (0x14) non abilitata.</span><span class="sxs-lookup"><span data-stu-id="06882-551">**NX_NOT_ENABLED** (0x14) Security not enabled.</span></span>
- <span data-ttu-id="06882-552">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-552">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-553">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-553">Allowed From</span></span>

<span data-ttu-id="06882-554">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-554">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-555">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-555">Example</span></span>

```c
/* Use the “my_privacy_key” for the SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_privacy_key_use(&my_agent, &my_privacy_key);


/* If status is NX_SUCCESS the privacy key is registered with the SNMP agent.  */
```

## <a name="nx_snmp_agent_sha_key_create"></a><span data-ttu-id="06882-556">nx_snmp_agent_sha_key_create</span><span class="sxs-lookup"><span data-stu-id="06882-556">nx_snmp_agent_sha_key_create</span></span>
<span data-ttu-id="06882-557">Crea chiave SHA (solo SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="06882-557">Create SHA key (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-558">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-558">Prototype</span></span>

```c
UINT nx_snmp_agent_sha_key_create(NX_SNMP_AGENT *agent_ptr, 
                                  UCHAR *password, 
                                  NX_SNMP_SECURITY_KEY  
                                  *destination_key);
```
### <a name="description"></a><span data-ttu-id="06882-559">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-559">Description</span></span>

<span data-ttu-id="06882-560">Questo servizio crea una chiave SHA che può essere usata per l'autenticazione e la crittografia.</span><span class="sxs-lookup"><span data-stu-id="06882-560">This service creates a SHA key that can be used for authentication and encryption.</span></span>

<span data-ttu-id="06882-561">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="06882-561">This service is deprecated.</span></span> <span data-ttu-id="06882-562">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_snmp_agent_sha_key_create_extended ()*.</span><span class="sxs-lookup"><span data-stu-id="06882-562">Developers are encouraged to migrate to *nx_snmp_agent_sha_key_create_extended()*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-563">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-563">Input Parameters</span></span>

- <span data-ttu-id="06882-564">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-564">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-565">**password** di Puntatore alla stringa della password.</span><span class="sxs-lookup"><span data-stu-id="06882-565">**password** Pointer to password string.</span></span>
- <span data-ttu-id="06882-566">**destination_key** Puntatore alla struttura dei dati della chiave SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-566">**destination_key** Pointer to SNMP key data structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-567">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-567">Return Values</span></span>

- <span data-ttu-id="06882-568">Creazione chiave riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="06882-568">**NX_SUCCESS** (0x00) Successful key create.</span></span>
- <span data-ttu-id="06882-569">Errore di creazione della chiave **NX_SNMP_ERROR** (0x100).</span><span class="sxs-lookup"><span data-stu-id="06882-569">**NX_SNMP_ERROR** (0x100) Key create error.</span></span>
- <span data-ttu-id="06882-570">**NX_PTR_ERROR** (0x07) un agente SNMP o un puntatore a chiave non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-570">**NX_PTR_ERROR** (0x07) Invalid SNMP Agent or key pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-571">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-571">Allowed From</span></span>

<span data-ttu-id="06882-572">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-572">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-573">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-573">Example</span></span>

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the SHA key for “my_agent.”   */
status =  nx_snmp_agent_sha_key_create(&my_agent, “authpw”, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_sha_key_create_extended"></a><span data-ttu-id="06882-574">nx_snmp_agent_sha_key_create_extended</span><span class="sxs-lookup"><span data-stu-id="06882-574">nx_snmp_agent_sha_key_create_extended</span></span>
<span data-ttu-id="06882-575">Crea chiave SHA (solo SNMP v3)</span><span class="sxs-lookup"><span data-stu-id="06882-575">Create SHA key (SNMP v3 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-576">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-576">Prototype</span></span>

```c
UINT nx_snmp_agent_sha_key_create_extended(NX_SNMP_AGENT *agent_ptr, 
                                           UCHAR *password, 
                                           UINT password_length,
                                           NX_SNMP_SECURITY_KEY  
                                           *destination_key);
```
### <a name="description"></a><span data-ttu-id="06882-577">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-577">Description</span></span>

<span data-ttu-id="06882-578">Questo servizio crea una chiave SHA che può essere usata per l'autenticazione e la crittografia.</span><span class="sxs-lookup"><span data-stu-id="06882-578">This service creates a SHA key that can be used for authentication and encryption.</span></span>

<span data-ttu-id="06882-579">Questo servizio sostituisce *nx_snmp_agent_sha_key_create ().*</span><span class="sxs-lookup"><span data-stu-id="06882-579">This service replaces *nx_snmp_agent_sha_key_create().*</span></span> <span data-ttu-id="06882-580">Per questa versione è necessario che il chiamante fornisca la lunghezza della password.</span><span class="sxs-lookup"><span data-stu-id="06882-580">This version requires caller to supply password length.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-581">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-581">Input Parameters</span></span>

- <span data-ttu-id="06882-582">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-582">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-583">**password** di Puntatore alla stringa della password.</span><span class="sxs-lookup"><span data-stu-id="06882-583">**password** Pointer to password string.</span></span>
- <span data-ttu-id="06882-584">**password_length** Lunghezza della stringa della password.</span><span class="sxs-lookup"><span data-stu-id="06882-584">**password_length** Length of password string.</span></span>
- <span data-ttu-id="06882-585">**destination_key** Puntatore alla struttura dei dati della chiave SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-585">**destination_key** Pointer to SNMP key data structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-586">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-586">Return Values</span></span>

- <span data-ttu-id="06882-587">Creazione chiave riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="06882-587">**NX_SUCCESS** (0x00) Successful key create.</span></span>
- <span data-ttu-id="06882-588">Errore di creazione della chiave **NX_SNMP_ERROR** (0x100).</span><span class="sxs-lookup"><span data-stu-id="06882-588">**NX_SNMP_ERROR** (0x100) Key create error.</span></span>
- <span data-ttu-id="06882-589">Creazione della chiave di **NX_SNMP_FAILED** (0x102) non riuscita.</span><span class="sxs-lookup"><span data-stu-id="06882-589">**NX_SNMP_FAILED** (0x102) Key create failed.</span></span>
- <span data-ttu-id="06882-590">**NX_PTR_ERROR** (0x07) un agente SNMP o un puntatore a chiave non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-590">**NX_PTR_ERROR** (0x07) Invalid SNMP Agent or key pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-591">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-591">Allowed From</span></span>

<span data-ttu-id="06882-592">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-592">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-593">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-593">Example</span></span>

```c
NX_SNMP_SECURITY_KEY my_key;

/* Create the SHA key for “my_agent.”   */
status =  nx_snmp_agent_sha_key_create_extended(&my_agent, “authpw”, 6, &my_key);


/* If status is NX_SUCCESS the key for the password “authpw” has been created.  */
```

## <a name="nx_snmp_agent_start"></a><span data-ttu-id="06882-594">nx_snmp_agent_start</span><span class="sxs-lookup"><span data-stu-id="06882-594">nx_snmp_agent_start</span></span>
<span data-ttu-id="06882-595">Avvia agente SNMP</span><span class="sxs-lookup"><span data-stu-id="06882-595">Start SNMP agent</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-596">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-596">Prototype</span></span>

```c
UINT nx_snmp_agent_start(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a><span data-ttu-id="06882-597">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-597">Description</span></span>

<span data-ttu-id="06882-598">Questo servizio associa il socket UDP alla porta SNMP 161 e avvia l'attività thread agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-598">This service binds the UDP socket to the SNMP port 161 and starts the SNMP Agent thread task.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-599">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-599">Input Parameters</span></span>

- <span data-ttu-id="06882-600">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-600">**agent_ptr** Pointer to SNMP Agent control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-601">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-601">Return Values</span></span>

- <span data-ttu-id="06882-602">**NX_SUCCESS** (0x00) avvio dell'agente SNMP riuscito.</span><span class="sxs-lookup"><span data-stu-id="06882-602">**NX_SUCCESS** (0x00) Successful start of SNMP Agent.</span></span>
- <span data-ttu-id="06882-603">Errore di avvio dell'agente SNMP **NX_SNMP_ERROR** (0x100).</span><span class="sxs-lookup"><span data-stu-id="06882-603">**NX_SNMP_ERROR** (0x100) SNMP Agent start error.</span></span>
- <span data-ttu-id="06882-604">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-604">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-605">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-605">Allowed From</span></span>

<span data-ttu-id="06882-606">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-606">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-607">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-607">Example</span></span>

```c
/* Start the previously created SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_start(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been started.  */
```
## <a name="nx_snmp_agent_stop"></a><span data-ttu-id="06882-608">nx_snmp_agent_stop</span><span class="sxs-lookup"><span data-stu-id="06882-608">nx_snmp_agent_stop</span></span>
<span data-ttu-id="06882-609">Arrestare l'agente SNMP</span><span class="sxs-lookup"><span data-stu-id="06882-609">Stop SNMP agent</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-610">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-610">Prototype</span></span>

```c
UINT nx_snmp_agent_stop(NX_SNMP_AGENT *agent_ptr);
```
### <a name="description"></a><span data-ttu-id="06882-611">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-611">Description</span></span>

<span data-ttu-id="06882-612">Questo servizio arresta l'attività thread agente SNMP e Annulla il binding del socket UDP alla porta SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-612">This service stops the SNMP Agent thread task and unbinds the UDP socket to the SNMP port.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-613">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-613">Input Parameters</span></span>

- <span data-ttu-id="06882-614">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-614">**agent_ptr** Pointer to SNMP Agent control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-615">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-615">Return Values</span></span>

- <span data-ttu-id="06882-616">L'arresto dell'agente SNMP **NX_SUCCESS** (0x00) è riuscito.</span><span class="sxs-lookup"><span data-stu-id="06882-616">**NX_SUCCESS** (0x00) Successful stop of SNMP Agent.</span></span>
- <span data-ttu-id="06882-617">**NX_PTR_ERROR** (0x07) puntatore a agente SNMP non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-617">**NX_PTR_ERROR** (0x07) Invalid SNMP Agent pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-618">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-618">Allowed From</span></span>

<span data-ttu-id="06882-619">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-619">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-620">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-620">Example</span></span>

```c
/* Stop the previously created and started SNMP Agent “my_agent.”   */
status =  nx_snmp_agent_stop(&my_agent);


/* If status is NX_SUCCESS the SNMP Agent “my_agent” has been stopped.  */
```
## <a name="nx_snmp_agent_trap_send"></a><span data-ttu-id="06882-621">nx_snmp_agent_trap_send</span><span class="sxs-lookup"><span data-stu-id="06882-621">nx_snmp_agent_trap_send</span></span>
<span data-ttu-id="06882-622">Invia trap SNMPv1 *(solo IPv4)*</span><span class="sxs-lookup"><span data-stu-id="06882-622">Send SNMPv1 trap *(IPv4 only)*</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-623">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-623">Prototype</span></span>

```c
UINT nx_snmp_agent_trap_send(NX_SNMP_AGENT *agent_ptr, 
                             ULONG ip_address, UCHAR *enterprise, 
                             UINT trap_type, UINT trap_code, 
                             ULONG elapsed_time, 
                             NX_SNMP_TRAP_OBJECT *object_list_ptr);
```

### <a name="description"></a><span data-ttu-id="06882-624">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-624">Description</span></span>

<span data-ttu-id="06882-625">Questo servizio invia una trap SNMP al gestore SNMP all'indirizzo IPv4 specificato.</span><span class="sxs-lookup"><span data-stu-id="06882-625">This service sends an SNMP trap to the SNMP Manager at the specified IPv4 address.</span></span> <span data-ttu-id="06882-626">Il metodo preferito per l'invio di un trap SNMP in NetX duo consiste nell'usare il servizio *nxd_snmp_agent_trap_send* .</span><span class="sxs-lookup"><span data-stu-id="06882-626">The preferred method for sending an SNMP trap in NetX Duo is to use the *nxd_snmp_agent_trap_send* service.</span></span> <span data-ttu-id="06882-627">*nx_snmp_agent_trap_send* è incluso in NETX Duo per supportare le applicazioni agente SNMP NETX esistenti.</span><span class="sxs-lookup"><span data-stu-id="06882-627">*nx_snmp_agent_trap_send* is included in NetX Duo to support existing NetX SNMP Agent applications.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-628">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-628">Input Parameters</span></span>

- <span data-ttu-id="06882-629">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-629">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-630">**ip_address** Indirizzo IPv4 della gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-630">**ip_address** IPv4 address of the SNMP Manager.</span></span>
- <span data-ttu-id="06882-631">**Enterprise** Stringa ID oggetto aziendale (sysObectID).</span><span class="sxs-lookup"><span data-stu-id="06882-631">**enterprise** Enterprise object ID string (sysObectID).</span></span>
- <span data-ttu-id="06882-632">**trap_type** Tipo di trap richiesto, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="06882-632">**trap_type** Type of trap requested, as follows:</span></span>  
   - <span data-ttu-id="06882-633">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="06882-633">NX_SNMP_TRAP_COLDSTART (0)</span></span>  
   - <span data-ttu-id="06882-634">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="06882-634">NX_SNMP_TRAP_WARMSTART (1)</span></span>  
   - <span data-ttu-id="06882-635">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="06882-635">NX_SNMP_TRAP_LINKDOWN (2)</span></span>  
   - <span data-ttu-id="06882-636">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="06882-636">NX_SNMP_TRAP_LINKUP (3)</span></span>  
   - <span data-ttu-id="06882-637">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="06882-637">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>  
   - <span data-ttu-id="06882-638">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="06882-638">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>  

- <span data-ttu-id="06882-639">**trap_code** Codice trap specifico.</span><span class="sxs-lookup"><span data-stu-id="06882-639">**trap_code** Specific trap code.</span></span>
- <span data-ttu-id="06882-640">**elapsed_time** Il sistema temporale è stato aggiornato (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="06882-640">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="06882-641">**object_list_ptr** Matrice di oggetti e i relativi valori associati da includere nel trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-641">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="06882-642">L'elenco è NX_NULL terminato.</span><span class="sxs-lookup"><span data-stu-id="06882-642">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-643">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-643">Return Values</span></span>

- <span data-ttu-id="06882-644">**NX_SUCCESS** (0x00) la trasmissione trap SNMP riuscita.</span><span class="sxs-lookup"><span data-stu-id="06882-644">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="06882-645">Errore di **NX_SNMP_ERROR** (0X100) durante l'invio del trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-645">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="06882-646">Il **NX_NOT_ENABLED** (0X14) SNMPv1 non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="06882-646">**NX_NOT_ENABLED** (0x14) SNMPv1 not enabled.</span></span>
- <span data-ttu-id="06882-647">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-647">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-648">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-648">Allowed From</span></span>

<span data-ttu-id="06882-649">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-649">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-650">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-650">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

ULONG dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build list of objects to supply in the trap.  */
trap_list[0].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.2.2.1.1.0";
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_INTEGER;
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_msw =   counter;
trap_list[1].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.1.3.0";
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_TIME_TICS;
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_msw =   tx_time_get();
trap_list[2].nx_snmp_object_string_ptr =  NX_NULL; /* Terminate list!  */

/* Send trap to SNMP manager at 193.2.2.61.  */
status =  nx_snmp_agent_trap_send(&my_agent,dest_ip_address,
                                   "1.3.6.7.7.7", NX_SNMP_TRAP_LINKUP, counter++, 
                                  tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nxd_snmp_agent_trap_send"></a><span data-ttu-id="06882-651">nxd_snmp_agent_trap_send</span><span class="sxs-lookup"><span data-stu-id="06882-651">nxd_snmp_agent_trap_send</span></span>
<span data-ttu-id="06882-652">Invia trap SNMPv1 *(IPv4 e IPv6)*</span><span class="sxs-lookup"><span data-stu-id="06882-652">Send SNMPv1 trap *(IPv4 and IPv6)*</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-653">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-653">Prototype</span></span>

```c
UINT nxd_snmp_agent_trap_send(NX_SNMP_AGENT *agent_ptr, 
            ULONG ip_address, UCHAR *enterprise, UINT trap_type, 
            UINT trap_code, ULONG elapsed_time, 
            NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="06882-654">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-654">Description</span></span>

<span data-ttu-id="06882-655">Questo servizio invia una trap SNMP al gestore SNMP all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="06882-655">This service sends an SNMP trap to the SNMP Manager at the specified IP address.</span></span> <span data-ttu-id="06882-656">Il metodo equivalente per l'invio di un trap SNMP in NetX è il servizio *nxd_snmp_agent_trap_send* .</span><span class="sxs-lookup"><span data-stu-id="06882-656">The equivalent method for sending an SNMP trap in NetX is the *nxd_snmp_agent_trap_send* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-657">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-657">Input Parameters</span></span>

- <span data-ttu-id="06882-658">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-658">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-659">**ip_address** Indirizzo IPv4 o IPv6 della gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-659">**ip_address** IPv4 or IPv6 address of the SNMP Manager.</span></span>
- <span data-ttu-id="06882-660">**Enterprise** Stringa ID oggetto aziendale (sysObectID).</span><span class="sxs-lookup"><span data-stu-id="06882-660">**enterprise** Enterprise object ID string (sysObectID).</span></span>
- <span data-ttu-id="06882-661">**trap_type** Tipo di trap richiesto, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="06882-661">**trap_type** Type of trap requested, as follows:</span></span>  
   - <span data-ttu-id="06882-662">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="06882-662">NX_SNMP_TRAP_COLDSTART (0)</span></span>
   - <span data-ttu-id="06882-663">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="06882-663">NX_SNMP_TRAP_WARMSTART (1)</span></span>
   - <span data-ttu-id="06882-664">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="06882-664">NX_SNMP_TRAP_LINKDOWN (2)</span></span>
   - <span data-ttu-id="06882-665">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="06882-665">NX_SNMP_TRAP_LINKUP (3)</span></span>
   - <span data-ttu-id="06882-666">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="06882-666">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>
   - <span data-ttu-id="06882-667">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="06882-667">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>

- <span data-ttu-id="06882-668">**trap_code** Codice trap specifico.</span><span class="sxs-lookup"><span data-stu-id="06882-668">**trap_code** Specific trap code.</span></span>
- <span data-ttu-id="06882-669">**elapsed_time** Il sistema temporale è stato aggiornato (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="06882-669">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="06882-670">**object_list_ptr** Matrice di oggetti e i relativi valori associati da includere nel trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-670">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="06882-671">L'elenco è NX_NULL terminato.</span><span class="sxs-lookup"><span data-stu-id="06882-671">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-672">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-672">Return Values</span></span>

- <span data-ttu-id="06882-673">**NX_SUCCESS** (0x00) la trasmissione trap SNMP riuscita.</span><span class="sxs-lookup"><span data-stu-id="06882-673">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="06882-674">Errore di **NX_SNMP_ERROR** (0X100) durante l'invio del trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-674">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="06882-675">Il **NX_NOT_ENABLED** (0X14) SNMPv1 non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="06882-675">**NX_NOT_ENABLED** (0x14) SNMPv1 not enabled.</span></span>
- <span data-ttu-id="06882-676">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-676">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-677">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-677">Allowed From</span></span>

<span data-ttu-id="06882-678">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-678">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-679">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-679">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build list of objects to supply in the trap.  */
trap_list[0].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.2.2.1.1.0";
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_INTEGER;
trap_list[0].nx_snmp_object_data.nx_snmp_object_data_msw =   counter;
trap_list[1].nx_snmp_object_string_ptr =  "1.3.6.1.2.1.1.3.0";
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_type =  NX_SNMP_TIME_TICS;
trap_list[1].nx_snmp_object_data.nx_snmp_object_data_msw =   tx_time_get();
trap_list[2].nx_snmp_object_string_ptr =  NX_NULL; /* Terminate list!  */

/* Send trap to SNMP manager at 193.2.2.61.  */
status =  nxd_snmp_agent_trap_send(&my_agent,&dest_ip_address,
                 "1.3.6.7.7.7", NX_SNMP_TRAP_LINKUP, counter++, tx_time_get(), 
               trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv2_send"></a><span data-ttu-id="06882-680">nx_snmp_agent_trapv2_send</span><span class="sxs-lookup"><span data-stu-id="06882-680">nx_snmp_agent_trapv2_send</span></span>
<span data-ttu-id="06882-681">Invia trap SNMPv2 (solo IPv4)</span><span class="sxs-lookup"><span data-stu-id="06882-681">Send SNMPv2 trap (IPv4 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-682">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-682">Prototype</span></span>

```c
UINT nx_snmp_agent_trapv2_send(NX_SNMP_AGENT *agent_ptr, 
            NXD_ADDRESS *ip_address, UCHAR *community, UINT trap_type, 
            ULONG elapsed_time, NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="06882-683">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-683">Description</span></span>

<span data-ttu-id="06882-684">Questo servizio invia una trap SNMPv2 al gestore SNMP all'indirizzo IPv4 specificato.</span><span class="sxs-lookup"><span data-stu-id="06882-684">This service sends an SNMPv2 trap to the SNMP Manager at the specified IPv4 address.</span></span> <span data-ttu-id="06882-685">Il metodo preferito per l'invio di un trap SNMP in NetX duo consiste nell'usare il servizio *nxd_snmp_agent_trapv2_send* .</span><span class="sxs-lookup"><span data-stu-id="06882-685">The preferred method for sending an SNMP trap in NetX Duo is to use the *nxd_snmp_agent_trapv2_send* service.</span></span> <span data-ttu-id="06882-686">*nx_snmp_agent_trapv2_send* è incluso in NETX Duo per supportare le applicazioni agente SNMP NETX esistenti.</span><span class="sxs-lookup"><span data-stu-id="06882-686">*nx_snmp_agent_trapv2_send* is included in NetX Duo to support existing NetX SNMP Agent applications.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-687">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-687">Input Parameters</span></span>

- <span data-ttu-id="06882-688">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-688">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-689">**ip_address** Indirizzo IPv4 della gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-689">**ip_address** IPv4 address of the SNMP Manager.</span></span>
- <span data-ttu-id="06882-690">**community** di Nome della community (username).</span><span class="sxs-lookup"><span data-stu-id="06882-690">**community** Community name (username).</span></span>
- <span data-ttu-id="06882-691">**trap_type**</span><span class="sxs-lookup"><span data-stu-id="06882-691">**trap_type**</span></span>  
   <span data-ttu-id="06882-692">Tipo di trap richiesto.</span><span class="sxs-lookup"><span data-stu-id="06882-692">Type of trap requested.</span></span> <span data-ttu-id="06882-693">Gli eventi standard sono:</span><span class="sxs-lookup"><span data-stu-id="06882-693">The standard events are:</span></span>  
   - <span data-ttu-id="06882-694">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="06882-694">NX_SNMP_TRAP_COLDSTART (0)</span></span>
   - <span data-ttu-id="06882-695">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="06882-695">NX_SNMP_TRAP_WARMSTART (1)</span></span>
   - <span data-ttu-id="06882-696">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="06882-696">NX_SNMP_TRAP_LINKDOWN (2)</span></span>
   - <span data-ttu-id="06882-697">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="06882-697">NX_SNMP_TRAP_LINKUP (3)</span></span>
   - <span data-ttu-id="06882-698">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="06882-698">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>
   - <span data-ttu-id="06882-699">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="06882-699">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>

   <span data-ttu-id="06882-700">Per i dati proprietari:</span><span class="sxs-lookup"><span data-stu-id="06882-700">For proprietary data:</span></span>  
   - <span data-ttu-id="06882-701">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (definito in *nxd_snmp. h*)</span><span class="sxs-lookup"><span data-stu-id="06882-701">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (defined in *nxd_snmp.h*)</span></span>
   
- <span data-ttu-id="06882-702">**elapsed_time** Il sistema temporale è stato aggiornato (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="06882-702">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="06882-703">**object_list_ptr** Matrice di oggetti e i relativi valori associati da includere nel trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-703">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="06882-704">L'elenco è NX_NULL terminato.</span><span class="sxs-lookup"><span data-stu-id="06882-704">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-705">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-705">Return Values</span></span>

- <span data-ttu-id="06882-706">**NX_SUCCESS** (0x00) la trasmissione trap SNMP riuscita.</span><span class="sxs-lookup"><span data-stu-id="06882-706">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="06882-707">Errore di **NX_SNMP_ERROR** (0X100) durante l'invio del trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-707">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="06882-708">Il **NX_NOT_ENABLED** (0X14) SNMPv2 non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="06882-708">**NX_NOT_ENABLED** (0x14) SNMPv2 not enabled.</span></span>
- <span data-ttu-id="06882-709">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-709">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-710">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-710">Allowed From</span></span>

<span data-ttu-id="06882-711">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-711">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-712">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-712">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
ULONG  dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv2_send(&my_agent,dest_ip_address, "public",
               NX_SNMP_TRAP_COLDSTART, tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv2_oid_send"></a><span data-ttu-id="06882-713">nx_snmp_agent_trapv2_oid_send</span><span class="sxs-lookup"><span data-stu-id="06882-713">nx_snmp_agent_trapv2_oid_send</span></span>
<span data-ttu-id="06882-714">Invia trap SNMPv2 specificando OID direttamente</span><span class="sxs-lookup"><span data-stu-id="06882-714">Send SNMPv2 trap specifying OID directly</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-715">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-715">Prototype</span></span>

```c
UINT nx_snmp_agent_trapv2_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                   ULONG ip_address, UCHAR *community,        
                                   UCHAR *oid, ULONG elapsed_time,   
                                   NX_SNMP_TRAP_OBJECT 
                                            *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="06882-716">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-716">Description</span></span>

<span data-ttu-id="06882-717">Questo servizio invia una trap SNMPv2 al gestore SNMP all'indirizzo IP specificato (solo IPv4) e consente al chiamante di specificare direttamente l'OID.</span><span class="sxs-lookup"><span data-stu-id="06882-717">This service sends an SNMPv2 trap to the SNMP Manager at the specified IP address (IPv4 only) and allows the caller to specify the OID directly.</span></span> <span data-ttu-id="06882-718">Il metodo preferito per l'invio di un trap SNMP con l'OID specificato in NetX duo consiste nell'usare il servizio *nxd_snmp_agent_trapv2_oid_send* .</span><span class="sxs-lookup"><span data-stu-id="06882-718">The preferred method for sending an SNMP trap with specified OID in NetX Duo is to use the *nxd_snmp_agent_trapv2_oid_send* service.</span></span> <span data-ttu-id="06882-719">*nx_snmp_agent_trapv2_oid_ Send* è incluso in NETX Duo per supportare le applicazioni agente SNMP NETX esistenti.</span><span class="sxs-lookup"><span data-stu-id="06882-719">*nx_snmp_agent_trapv2_oid_ send* is included in NetX Duo to support existing NetX SNMP Agent applications.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-720">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-720">Input Parameters</span></span>

- <span data-ttu-id="06882-721">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-721">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-722">**ip_address** Indirizzo IP di gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-722">**ip_address** IP address of SNMP Manager.</span></span>
- <span data-ttu-id="06882-723">**community** di Nome della community (username).</span><span class="sxs-lookup"><span data-stu-id="06882-723">**community** Community name (username).</span></span>
- <span data-ttu-id="06882-724">**OID** Puntatore al buffer contenente l'OID.</span><span class="sxs-lookup"><span data-stu-id="06882-724">**oid** Pointer to buffer containing OID.</span></span>
- <span data-ttu-id="06882-725">**elapsed_time** Il sistema temporale è stato aggiornato (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="06882-725">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="06882-726">**object_list_ptr** Matrice di oggetti e i relativi valori associati da includere nel trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-726">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="06882-727">L'elenco è NX_NULL terminato.</span><span class="sxs-lookup"><span data-stu-id="06882-727">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-728">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-728">Return Values</span></span>

- <span data-ttu-id="06882-729">**NX_SUCCESS** (0x00) la trasmissione trap SNMP riuscita.</span><span class="sxs-lookup"><span data-stu-id="06882-729">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="06882-730">Errore di **NX_SNMP_ERROR** (0X100) durante l'invio del trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-730">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="06882-731">**NX_PTR_ERROR** (0x16) un agente SNMP o un puntatore a parametro non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-731">**NX_PTR_ERROR** (0x16) Invalid SNMP Agent or parameter pointer.</span></span>
- <span data-ttu-id="06882-732">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP di destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-732">**NX_IP_ADDRESS_ERROR** (0x21) Invalid destination IP address.</span></span>
- <span data-ttu-id="06882-733">Il parametro **NX_OPTION_ERROR** (0X0a) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-733">**NX_OPTION_ERROR** (0x0a) Invalid parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-734">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-734">Allowed From</span></span>

<span data-ttu-id="06882-735">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-735">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-736">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-736">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv2_oid_send(&my_agent, IP_ADDRESS(193,2,2,61), 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv2_send"></a><span data-ttu-id="06882-737">nxd_snmp_agent_trapv2_send</span><span class="sxs-lookup"><span data-stu-id="06882-737">nxd_snmp_agent_trapv2_send</span></span>
<span data-ttu-id="06882-738">Invia trap SNMPv2 (IPv4 e IPv6)</span><span class="sxs-lookup"><span data-stu-id="06882-738">Send SNMPv2 trap (IPv4 and IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-739">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-739">Prototype</span></span>

```c
UINT nxd_snmp_agent_trapv2_send(NX_SNMP_AGENT *agent_ptr, 
                                NXD_ADDRESS *ip_address, 
                                UCHAR *community, UINT trap_type, 
                                ULONG elapsed_time, 
                                NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="06882-740">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-740">Description</span></span>

<span data-ttu-id="06882-741">Questo servizio invia una trap SNMP v2 al gestore SNMP all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="06882-741">This service sends an SNMP V2 trap to the SNMP Manager at the specified IP address.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-742">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-742">Input Parameters</span></span>

- <span data-ttu-id="06882-743">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-743">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-744">**ip_address** Indirizzo IP (IPv4 o IPv6) di gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-744">**ip_address** IP (IPv4 or IPv6) address of the SNMP Manager.</span></span>
- <span data-ttu-id="06882-745">**community** di Nome della community (username).</span><span class="sxs-lookup"><span data-stu-id="06882-745">**community** Community name (username).</span></span>
- <span data-ttu-id="06882-746">**trap_type**</span><span class="sxs-lookup"><span data-stu-id="06882-746">**trap_type**</span></span>  
   <span data-ttu-id="06882-747">Tipo di trap richiesto.</span><span class="sxs-lookup"><span data-stu-id="06882-747">Type of trap requested.</span></span> <span data-ttu-id="06882-748">Gli eventi standard sono:</span><span class="sxs-lookup"><span data-stu-id="06882-748">The standard events are:</span></span>  
   - <span data-ttu-id="06882-749">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="06882-749">NX_SNMP_TRAP_COLDSTART (0)</span></span>
   - <span data-ttu-id="06882-750">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="06882-750">NX_SNMP_TRAP_WARMSTART (1)</span></span>
   - <span data-ttu-id="06882-751">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="06882-751">NX_SNMP_TRAP_LINKDOWN (2)</span></span>
   - <span data-ttu-id="06882-752">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="06882-752">NX_SNMP_TRAP_LINKUP (3)</span></span>
   - <span data-ttu-id="06882-753">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="06882-753">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>
   - <span data-ttu-id="06882-754">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="06882-754">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>

   <span data-ttu-id="06882-755">Per i dati proprietari:</span><span class="sxs-lookup"><span data-stu-id="06882-755">For proprietary data:</span></span>

   - <span data-ttu-id="06882-756">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (definito in *nxd_snmp. h*)</span><span class="sxs-lookup"><span data-stu-id="06882-756">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (defined in *nxd_snmp.h*)</span></span>

- <span data-ttu-id="06882-757">**elapsed_time** Il sistema temporale è stato aggiornato (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="06882-757">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="06882-758">**object_list_ptr** Matrice di oggetti e i relativi valori associati da includere nel trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-758">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="06882-759">L'elenco è NX_NULL terminato.</span><span class="sxs-lookup"><span data-stu-id="06882-759">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-760">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-760">Return Values</span></span>

- <span data-ttu-id="06882-761">**NX_SUCCESS** (0x00) la trasmissione trap SNMP riuscita.</span><span class="sxs-lookup"><span data-stu-id="06882-761">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="06882-762">Errore di **NX_SNMP_ERROR** (0X100) durante l'invio del trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-762">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="06882-763">Il **NX_NOT_ENABLED** (0X14) SNMPv2 non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="06882-763">**NX_NOT_ENABLED** (0x14) SNMPv2 not enabled.</span></span>
- <span data-ttu-id="06882-764">**NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) versione IP non supportata</span><span class="sxs-lookup"><span data-stu-id="06882-764">**NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) Unsupported IP version</span></span>
- <span data-ttu-id="06882-765">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-765">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-766">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-766">Allowed From</span></span>

<span data-ttu-id="06882-767">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-767">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-768">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-768">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send a standard event trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv2_send(&my_agent,&dest_ip_address, "public",
                                    NX_SNMP_TRAP_COLDSTART, tx_time_get(),  
                                    trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv2_oid_send"></a><span data-ttu-id="06882-769">nxd_snmp_agent_trapv2_oid_send</span><span class="sxs-lookup"><span data-stu-id="06882-769">nxd_snmp_agent_trapv2_oid_send</span></span>
<span data-ttu-id="06882-770">Invia trap SNMPv2 specificando OID direttamente</span><span class="sxs-lookup"><span data-stu-id="06882-770">Send SNMPv2 trap specifying OID directly</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-771">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-771">Prototype</span></span>

```c
UINT nxd_snmp_agent_trapv2_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                    NXD_ADDRESS *ip_address, 
                                    UCHAR *community,        
                                    UCHAR *oid, ULONG elapsed_time,   
                                    NX_SNMP_TRAP_OBJECT 
                                    *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="06882-772">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-772">Description</span></span>

<span data-ttu-id="06882-773">Questo servizio invia una trap SNMP v2 al gestore SNMP all'indirizzo IP specificato (IPv4/IPv6) e consente al chiamante di specificare direttamente l'OID.</span><span class="sxs-lookup"><span data-stu-id="06882-773">This service sends an SNMP v2 trap to the SNMP Manager at the specified IP address (IPv4/IPv6) and allows the caller to specify the OID directly.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-774">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-774">Input Parameters</span></span>

- <span data-ttu-id="06882-775">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-775">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-776">**ip_address** Indirizzo IP di gestione SNMP (IPv4/IPv6).</span><span class="sxs-lookup"><span data-stu-id="06882-776">**ip_address** IP address of SNMP Manager (IPv4/IPv6).</span></span>
- <span data-ttu-id="06882-777">**community** di Nome della community (username).</span><span class="sxs-lookup"><span data-stu-id="06882-777">**community** Community name (username).</span></span>
- <span data-ttu-id="06882-778">**OID** Puntatore al buffer contenente l'OID.</span><span class="sxs-lookup"><span data-stu-id="06882-778">**oid** Pointer to buffer containing OID.</span></span>
- <span data-ttu-id="06882-779">**elapsed_time** Il sistema temporale è stato aggiornato (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="06882-779">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="06882-780">**object_list_ptr** Matrice di oggetti e i relativi valori associati da includere nel trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-780">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="06882-781">L'elenco è NX_NULL terminato.</span><span class="sxs-lookup"><span data-stu-id="06882-781">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-782">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-782">Return Values</span></span>

- <span data-ttu-id="06882-783">**NX_SUCCESS** (0x00) la trasmissione trap SNMP riuscita.</span><span class="sxs-lookup"><span data-stu-id="06882-783">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="06882-784">Errore di **NX_SNMP_ERROR** (0X100) durante l'invio del trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-784">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="06882-785">**NX_PTR_ERROR** (0x16) un agente SNMP o un puntatore a parametro non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-785">**NX_PTR_ERROR** (0x16) Invalid SNMP Agent or parameter pointer.</span></span>
- <span data-ttu-id="06882-786">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP di destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-786">**NX_IP_ADDRESS_ERROR** (0x21) Invalid destination IP address.</span></span>
- <span data-ttu-id="06882-787">Il parametro **NX_OPTION_ERROR** (0X0a) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-787">**NX_OPTION_ERROR** (0x0a) Invalid parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-788">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-788">Allowed From</span></span>

<span data-ttu-id="06882-789">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-789">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-790">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-790">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS         address;


/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

address.nxd_ip_version = NX_IP_VERSION_V4;
address.nxd_ip_address.v4 = IP_ADDRESS(193,2,2,61)

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv2_oid_send(&my_agent, &address, 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nx_snmp_agent_trapv3_send"></a><span data-ttu-id="06882-791">nx_snmp_agent_trapv3_send</span><span class="sxs-lookup"><span data-stu-id="06882-791">nx_snmp_agent_trapv3_send</span></span>
<span data-ttu-id="06882-792">Invia trap SNMPv3 (solo IPv4)</span><span class="sxs-lookup"><span data-stu-id="06882-792">Send SNMPv3 trap (IPv4 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-793">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-793">Prototype</span></span>

```c
UINT nx_snmp_agent_trapv3_send(NX_SNMP_AGENT *agent_ptr, 
            ULONG ip_address, UCHAR *username, UINT trap_type, 
            ULONG elapsed_time, NX_SNMP_TRAP_OBJECT *object_list_ptr);
```

### <a name="description"></a><span data-ttu-id="06882-794">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-794">Description</span></span>

<span data-ttu-id="06882-795">Questo servizio invia una trap SNMPv3 al gestore SNMP all'indirizzo IPv4 specificato.</span><span class="sxs-lookup"><span data-stu-id="06882-795">This service sends an SNMPv3 trap to the SNMP Manager at the specified IPv4 address.</span></span> <span data-ttu-id="06882-796">Il metodo preferito per l'invio di un trap SNMP in NetX duo consiste nell'usare il servizio *nxd_snmp_agent_trapv3_send* .</span><span class="sxs-lookup"><span data-stu-id="06882-796">The preferred method for sending an SNMP trap in NetX Duo is to use the *nxd_snmp_agent_trapv3_send* service.</span></span> <span data-ttu-id="06882-797">*nx_snmp_agent_trapv3_send* è incluso in NETX Duo per supportare le applicazioni agente SNMP NETX esistenti.</span><span class="sxs-lookup"><span data-stu-id="06882-797">*nx_snmp_agent_trapv3_send* is included in NetX Duo to support existing NetX SNMP Agent applications.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-798">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-798">Input Parameters</span></span>

- <span data-ttu-id="06882-799">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-799">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-800">**ip_address** Indirizzo IPv4 della gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-800">**ip_address** IPv4 address of the SNMP Manager.</span></span>
- <span data-ttu-id="06882-801">**nome utente** Nome della community (username).</span><span class="sxs-lookup"><span data-stu-id="06882-801">**username** Community name (username).</span></span>
- <span data-ttu-id="06882-802">**trap_type**</span><span class="sxs-lookup"><span data-stu-id="06882-802">**trap_type**</span></span>  
   <span data-ttu-id="06882-803">Tipo di trap richiesto.</span><span class="sxs-lookup"><span data-stu-id="06882-803">Type of trap requested.</span></span> <span data-ttu-id="06882-804">Gli eventi standard sono:</span><span class="sxs-lookup"><span data-stu-id="06882-804">The standard events are:</span></span>  
   - <span data-ttu-id="06882-805">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="06882-805">NX_SNMP_TRAP_COLDSTART (0)</span></span>
   - <span data-ttu-id="06882-806">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="06882-806">NX_SNMP_TRAP_WARMSTART (1)</span></span>
   - <span data-ttu-id="06882-807">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="06882-807">NX_SNMP_TRAP_LINKDOWN (2)</span></span>
   - <span data-ttu-id="06882-808">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="06882-808">NX_SNMP_TRAP_LINKUP (3)</span></span>
   - <span data-ttu-id="06882-809">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="06882-809">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>
   - <span data-ttu-id="06882-810">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="06882-810">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>

   <span data-ttu-id="06882-811">Per i dati proprietari:</span><span class="sxs-lookup"><span data-stu-id="06882-811">For proprietary data:</span></span>
   - <span data-ttu-id="06882-812">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (definito in *nxd_snmp. h*)</span><span class="sxs-lookup"><span data-stu-id="06882-812">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (defined in *nxd_snmp.h*)</span></span>

- <span data-ttu-id="06882-813">**elapsed_time** Il sistema temporale è stato aggiornato (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="06882-813">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="06882-814">**object_list_ptr** Matrice di oggetti e i relativi valori associati da includere nel trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-814">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="06882-815">L'elenco è NX_NULL terminato.</span><span class="sxs-lookup"><span data-stu-id="06882-815">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-816">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-816">Return Values</span></span>

- <span data-ttu-id="06882-817">**NX_SUCCESS** (0x00) la trasmissione trap SNMP riuscita.</span><span class="sxs-lookup"><span data-stu-id="06882-817">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="06882-818">Errore di **NX_SNMP_ERROR** (0X100) durante l'invio del trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-818">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="06882-819">Il **NX_NOT_ENABLED** (0X14) SNMPv3 non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="06882-819">**NX_NOT_ENABLED** (0x14) SNMPv3 not enabled.</span></span>
- <span data-ttu-id="06882-820">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-820">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-821">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-821">Allowed From</span></span>

<span data-ttu-id="06882-822">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-822">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-823">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-823">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
ULONG dest_ip_address = IP_ADDRESS(1,2,3,4);

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv3_send(&my_agent, dest_ip_address, "public",
               NX_SNMP_TRAP_COLDSTART, tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nx_snmp_agent_trapv3_oid_send"></a><span data-ttu-id="06882-824">nx_snmp_agent_trapv3_oid_send</span><span class="sxs-lookup"><span data-stu-id="06882-824">nx_snmp_agent_trapv3_oid_send</span></span>
<span data-ttu-id="06882-825">Invia trap SNMPv3 specificando OID direttamente</span><span class="sxs-lookup"><span data-stu-id="06882-825">Send SNMPv3 trap specifying OID directly</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-826">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-826">Prototype</span></span>

```c
UINT nx_snmp_agent_trapv3_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                   ULONG ip_address, UCHAR *username,        
                                   UCHAR *oid, ULONG elapsed_time,   
                                   NX_SNMP_TRAP_OBJECT 
                                   *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="06882-827">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-827">Description</span></span>

<span data-ttu-id="06882-828">Questo servizio invia una trap SNMPv3 al gestore SNMP all'indirizzo IP specificato (solo IPv4) e consente al chiamante di specificare direttamente l'OID.</span><span class="sxs-lookup"><span data-stu-id="06882-828">This service sends an SNMPv3 trap to the SNMP Manager at the specified IP address (IPv4 only) and allows the caller to specify the OID directly.</span></span> <span data-ttu-id="06882-829">Il metodo preferito per l'invio di un trap SNMP con l'OID specificato in NetX duo consiste nell'usare il servizio *nxd_snmp_agent_trapv3_oid_send* .</span><span class="sxs-lookup"><span data-stu-id="06882-829">The preferred method for sending an SNMP trap with specified OID in NetX Duo is to use the *nxd_snmp_agent_trapv3_oid_send* service.</span></span> <span data-ttu-id="06882-830">*nx_snmp_agent_trapv3_oid_ Send* è incluso in NETX Duo per supportare le applicazioni agente SNMP NETX esistenti.</span><span class="sxs-lookup"><span data-stu-id="06882-830">*nx_snmp_agent_trapv3_oid_ send* is included in NetX Duo to support existing NetX SNMP Agent applications.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-831">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-831">Input Parameters</span></span>

- <span data-ttu-id="06882-832">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-832">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-833">**ip_address** Indirizzo IP di gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-833">**ip_address** IP address of SNMP Manager.</span></span>
- <span data-ttu-id="06882-834">**nome utente** Nome della community (username).</span><span class="sxs-lookup"><span data-stu-id="06882-834">**username** Community name (username).</span></span>
- <span data-ttu-id="06882-835">**OID** Puntatore al buffer contenente l'OID.</span><span class="sxs-lookup"><span data-stu-id="06882-835">**oid** Pointer to buffer containing OID.</span></span>
- <span data-ttu-id="06882-836">**elapsed_time** Il sistema temporale è stato aggiornato (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="06882-836">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="06882-837">**object_list_ptr** Matrice di oggetti e i relativi valori associati da includere nel trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-837">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="06882-838">L'elenco è NX_NULL terminato.</span><span class="sxs-lookup"><span data-stu-id="06882-838">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-839">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-839">Return Values</span></span>

- <span data-ttu-id="06882-840">**NX_SUCCESS** (0x00) la trasmissione trap SNMP riuscita.</span><span class="sxs-lookup"><span data-stu-id="06882-840">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="06882-841">Errore di **NX_SNMP_ERROR** (0X100) durante l'invio del trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-841">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="06882-842">**NX_PTR_ERROR** (0x16) un agente SNMP o un puntatore a parametro non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-842">**NX_PTR_ERROR** (0x16) Invalid SNMP Agent or parameter pointer.</span></span>
- <span data-ttu-id="06882-843">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP di destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-843">**NX_IP_ADDRESS_ERROR** (0x21) Invalid destination IP address.</span></span>
- <span data-ttu-id="06882-844">Il parametro **NX_OPTION_ERROR** (0X0a) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-844">**NX_OPTION_ERROR** (0x0a) Invalid parameter.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-845">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-845">Allowed From</span></span>

<span data-ttu-id="06882-846">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-846">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-847">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-847">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nx_snmp_agent_trapv3_oid_send(&my_agent, IP_ADDRESS(193,2,2,61), 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nxd_snmp_agent_trapv3_send"></a><span data-ttu-id="06882-848">nxd_snmp_agent_trapv3_send</span><span class="sxs-lookup"><span data-stu-id="06882-848">nxd_snmp_agent_trapv3_send</span></span>
<span data-ttu-id="06882-849">Invia trap SNMPv3 (IPv4 e IPv6)</span><span class="sxs-lookup"><span data-stu-id="06882-849">Send SNMPv3 trap (IPv4 and IPv6)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-850">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-850">Prototype</span></span>

```c
UINT nxd_snmp_agent_trapv3_send(NX_SNMP_AGENT *agent_ptr, 
                                NXD_ADDRESS *ip_address, 
                                UCHAR *username, UINT trap_type, 
                                ULONG elapsed_time, 
                                NX_SNMP_TRAP_OBJECT *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="06882-851">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-851">Description</span></span>

<span data-ttu-id="06882-852">Questo servizio invia una trap SNMP al gestore SNMP all'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="06882-852">This service sends an SNMP trap to the SNMP Manager at the specified IP address.</span></span> <span data-ttu-id="06882-853">Questo trap è fondamentalmente lo stesso di SNMP v2 trap, ad eccezione del formato del messaggio trap incluso in SNMP v3 PDU.</span><span class="sxs-lookup"><span data-stu-id="06882-853">This trap is basically the same as the SNMP v2 trap, except the trap message format is contained in the SNMP v3 PDU.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-854">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-854">Input Parameters</span></span>

- <span data-ttu-id="06882-855">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-855">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-856">**ip_address** Indirizzo IP (IPv4 o IPv6) di gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-856">**ip_address** IP (IPv4 or IPv6) address of the SNMP Manager.</span></span>
- <span data-ttu-id="06882-857">**nome utente** Nome della community (username).</span><span class="sxs-lookup"><span data-stu-id="06882-857">**username** Community name (username).</span></span>
- <span data-ttu-id="06882-858">**trap_type**</span><span class="sxs-lookup"><span data-stu-id="06882-858">**trap_type**</span></span>  
   <span data-ttu-id="06882-859">Tipo di trap richiesto.</span><span class="sxs-lookup"><span data-stu-id="06882-859">Type of trap requested.</span></span> <span data-ttu-id="06882-860">Gli eventi standard sono:</span><span class="sxs-lookup"><span data-stu-id="06882-860">The standard events are:</span></span>
   - <span data-ttu-id="06882-861">NX_SNMP_TRAP_COLDSTART (0)</span><span class="sxs-lookup"><span data-stu-id="06882-861">NX_SNMP_TRAP_COLDSTART (0)</span></span>
   - <span data-ttu-id="06882-862">NX_SNMP_TRAP_WARMSTART (1)</span><span class="sxs-lookup"><span data-stu-id="06882-862">NX_SNMP_TRAP_WARMSTART (1)</span></span>
   - <span data-ttu-id="06882-863">NX_SNMP_TRAP_LINKDOWN (2)</span><span class="sxs-lookup"><span data-stu-id="06882-863">NX_SNMP_TRAP_LINKDOWN (2)</span></span>
   - <span data-ttu-id="06882-864">NX_SNMP_TRAP_LINKUP (3)</span><span class="sxs-lookup"><span data-stu-id="06882-864">NX_SNMP_TRAP_LINKUP (3)</span></span>
   - <span data-ttu-id="06882-865">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span><span class="sxs-lookup"><span data-stu-id="06882-865">NX_SNMP_TRAP_AUTHENTICATE_FAILURE (4)</span></span>
   - <span data-ttu-id="06882-866">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span><span class="sxs-lookup"><span data-stu-id="06882-866">NX_SNMP_TRAP_EGPNEIGHBORLOSS (5)</span></span>  
   <span data-ttu-id="06882-867">Per i dati proprietari:</span><span class="sxs-lookup"><span data-stu-id="06882-867">For proprietary data:</span></span>
   - <span data-ttu-id="06882-868">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (definito in *nxd_snmp. h*)</span><span class="sxs-lookup"><span data-stu-id="06882-868">NX_SNMP_TRAP_CUSTOM (0xFFFFFFFF) (defined in *nxd_snmp.h*)</span></span>

- <span data-ttu-id="06882-869">**elapsed_time** Il sistema temporale è stato aggiornato (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="06882-869">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="06882-870">**object_list_ptr** Matrice di oggetti e i relativi valori associati da includere nel trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-870">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="06882-871">L'elenco è NX_NULL terminato.</span><span class="sxs-lookup"><span data-stu-id="06882-871">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-872">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-872">Return Values</span></span>

- <span data-ttu-id="06882-873">**NX_SUCCESS** (0x00) la trasmissione trap SNMP riuscita.</span><span class="sxs-lookup"><span data-stu-id="06882-873">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="06882-874">Errore di **NX_SNMP_ERROR** (0X100) durante l'invio del trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-874">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="06882-875">Il **NX_NOT_ENABLED** (0X14) SNMPv3 non è abilitato.</span><span class="sxs-lookup"><span data-stu-id="06882-875">**NX_NOT_ENABLED** (0x14) SNMPv3 not enabled.</span></span>
- <span data-ttu-id="06882-876">**NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) versione IP non supportata</span><span class="sxs-lookup"><span data-stu-id="06882-876">**NX_SNMP_INVALID_IP_PROTOCOL_ERROR** (0x104) Unsupported IP version</span></span>
- <span data-ttu-id="06882-877">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-877">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-878">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-878">Allowed From</span></span>

<span data-ttu-id="06882-879">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-879">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-880">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-880">Example</span></span>

```c
NX_SNMP_TRAP_OBJECT trap_list[5];
NXD_ADDRESS dest_ip_address;

    dest_ip_address.nxd_ip_version = NX_IP_VERSION_V6 ;
    dest_ip_address.nxd_ip_address.v6[0] = 0x20010db8;
    dest_ip_address.nxd_ip_address.v6[1] = 0xf101;
    dest_ip_address.nxd_ip_address.v6[2] = 0x00000000;
    dest_ip_address.nxd_ip_address.v6[3] = 0x00000101;

/* Build an empty object list, since it is not needed for the 
   NX_SNMP_TRAP_COLDSTART trap.  */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv3_send(&my_agent, &dest_ip_address, "public",
                                    NX_SNMP_TRAP_COLDSTART, tx_time_get(),  
                                    trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```

## <a name="nxd_snmp_agent_trapv3_oid_send"></a><span data-ttu-id="06882-881">nxd_snmp_agent_trapv3_oid_send</span><span class="sxs-lookup"><span data-stu-id="06882-881">nxd_snmp_agent_trapv3_oid_send</span></span>
<span data-ttu-id="06882-882">Invia trap SNMPv3 specificando OID direttamente</span><span class="sxs-lookup"><span data-stu-id="06882-882">Send SNMPv3 trap specifying OID directly</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-883">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-883">Prototype</span></span>

```c
UINT nxd_snmp_agent_trapv3_oid_send(NX_SNMP_AGENT *agent_ptr, 
                                    NXD_ADDRESS *ip_address, 
                                    UCHAR *username,        
                                    UCHAR *oid, ULONG elapsed_time,   
                                    NX_SNMP_TRAP_OBJECT 
                                            *object_list_ptr);
```
### <a name="description"></a><span data-ttu-id="06882-884">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-884">Description</span></span>

<span data-ttu-id="06882-885">Questo servizio invia una trap SNMPv3 al gestore SNMP all'indirizzo IP specificato (IPv4/IPv6) e consente al chiamante di specificare direttamente l'OID.</span><span class="sxs-lookup"><span data-stu-id="06882-885">This service sends an SNMPv3 trap to the SNMP Manager at the specified IP address (IPv4/IPv6) and allows the caller to specify the OID directly.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-886">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-886">Input Parameters</span></span>

- <span data-ttu-id="06882-887">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-887">**agent_ptr** Pointer to SNMP Agent control block.</span></span>
- <span data-ttu-id="06882-888">**ip_address** Puntatore all'indirizzo IP della gestione SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-888">**ip_address** Pointer to IP address of SNMP Manager.</span></span>
- <span data-ttu-id="06882-889">**nome utente** Nome utente (nome community).</span><span class="sxs-lookup"><span data-stu-id="06882-889">**username** Username (community name).</span></span>
- <span data-ttu-id="06882-890">**OID** Puntatore al buffer contenente l'OID.</span><span class="sxs-lookup"><span data-stu-id="06882-890">**oid** Pointer to buffer containing OID.</span></span>
- <span data-ttu-id="06882-891">**elapsed_time** Il sistema temporale è stato aggiornato (sysUpTime).</span><span class="sxs-lookup"><span data-stu-id="06882-891">**elapsed_time** Time system has been up (sysUpTime).</span></span>
- <span data-ttu-id="06882-892">**object_list_ptr** Matrice di oggetti e i relativi valori associati da includere nel trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-892">**object_list_ptr** Array of objects and their associated values to be included in the SNMP trap.</span></span> <span data-ttu-id="06882-893">L'elenco è NX_NULL terminato.</span><span class="sxs-lookup"><span data-stu-id="06882-893">The list is NX_NULL terminated.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-894">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-894">Return Values</span></span>

- <span data-ttu-id="06882-895">**NX_SUCCESS** (0x00) la trasmissione trap SNMP riuscita.</span><span class="sxs-lookup"><span data-stu-id="06882-895">**NX_SUCCESS** (0x00) Successful SNMP trap send.</span></span>
- <span data-ttu-id="06882-896">Errore di **NX_SNMP_ERROR** (0X100) durante l'invio del trap SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-896">**NX_SNMP_ERROR** (0x100) Error sending SNMP trap.</span></span>
- <span data-ttu-id="06882-897">**NX_PTR_ERROR** (0x16) un agente SNMP o un puntatore a parametro non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-897">**NX_PTR_ERROR** (0x16) Invalid SNMP Agent or parameter pointer.</span></span>
- <span data-ttu-id="06882-898">**NX_IP_ADDRESS_ERROR** (0x21) indirizzo IP di destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-898">**NX_IP_ADDRESS_ERROR** (0x21) Invalid destination IP address.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-899">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-899">Allowed From</span></span>

<span data-ttu-id="06882-900">Thread</span><span class="sxs-lookup"><span data-stu-id="06882-900">Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-901">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-901">Example</span></span>

```c
NXD_ADDRESS         ip_address;
NX_SNMP_TRAP_OBJECT trap_list[5];

/* Build an empty object list */
trap_list[0].nx_snmp_object_string_ptr =  NX_NULL;

ip_address.nxd_ip_version = NX_IP_VERSION_V4;
ip_address.nxd_ip_address.v4 = IP_ADDRESS(193,2,2,61);

/* Send trap to SNMP manager at 193.2.2.61.  */
Status =  nxd_snmp_agent_trapv3_oid_send(&my_agent, &ip_address, 
                                       "public", (UCHAR *)"0.9.9.9.9.9.9.9.9.9",  
                                       tx_time_get(), trap_list);

/* If status is NX_SUCCESS the SNMP trap has been sent.  */
```
## <a name="nx_snmp_agent_v3_context_boots_set"></a><span data-ttu-id="06882-902">nx_snmp_agent_v3_context_boots_set</span><span class="sxs-lookup"><span data-stu-id="06882-902">nx_snmp_agent_v3_context_boots_set</span></span>
<span data-ttu-id="06882-903">Imposta il numero di riavvii (se SNMPv3 è abilitato)</span><span class="sxs-lookup"><span data-stu-id="06882-903">Set the number of reboots (if SNMPv3 enabled)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-904">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-904">Prototype</span></span>

```c
UINT nx_snmp_agent_v3_context_boots_set(NX_SNMP_AGENT *agent_ptr, 
                                        UINT boots);
```

### <a name="description"></a><span data-ttu-id="06882-905">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-905">Description</span></span>

<span data-ttu-id="06882-906">Questo servizio imposta il numero di riavvii registrati dall'agente SNMP.</span><span class="sxs-lookup"><span data-stu-id="06882-906">This service sets the number of reboots recorded by the SNMP agent.</span></span> <span data-ttu-id="06882-907">Questo servizio è disponibile solo se SNMPv3 è abilitato per l'agente SNMP perché il numero di avvio viene usato solo nel protocollo SNMPv3.</span><span class="sxs-lookup"><span data-stu-id="06882-907">This service is only available if SNMPv3 is enabled for the SNMP agent because boot count is only used in the SNMPv3 protocol.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-908">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-908">Input Parameters</span></span>

- <span data-ttu-id="06882-909">**agent_ptr** Puntatore al blocco di controllo dell'agente SNMP</span><span class="sxs-lookup"><span data-stu-id="06882-909">**agent_ptr** Pointer to SNMP Agent control block</span></span>
- <span data-ttu-id="06882-910">**Avvia** Valore su cui impostare il numero di avvio dell'agente SNMP</span><span class="sxs-lookup"><span data-stu-id="06882-910">**boots** The value to set SNMP Agent boot count to</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-911">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-911">Return Values</span></span>

- <span data-ttu-id="06882-912">**NX_SUCCESS** (0x00) ha impostato correttamente il conteggio di avvio</span><span class="sxs-lookup"><span data-stu-id="06882-912">**NX_SUCCESS** (0x00) Successfully set boot count</span></span>
- <span data-ttu-id="06882-913">**NX_SNMP_ERROR** (0X100) errore durante l'impostazione del numero di avvio</span><span class="sxs-lookup"><span data-stu-id="06882-913">**NX_SNMP_ERROR** (0x100) Error setting boot count</span></span>
- <span data-ttu-id="06882-914">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-914">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-915">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-915">Allowed From</span></span>

<span data-ttu-id="06882-916">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-916">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-917">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-917">Example</span></span>

```c
UINT my_boots = 4;

if (my_agent.nx_snmp_agent_v3_enabled == NX_TRUE)
{
   status = nx_snmp_agent_v3_context_boots_set(&my_agent, my_boots);
}


/* If status is NX_SUCCESS the SNMP boot count is set.  */
```

## <a name="nx_snmp_object_compare"></a><span data-ttu-id="06882-918">nx_snmp_object_compare</span><span class="sxs-lookup"><span data-stu-id="06882-918">nx_snmp_object_compare</span></span>
<span data-ttu-id="06882-919">Confrontare due oggetti</span><span class="sxs-lookup"><span data-stu-id="06882-919">Compare two objects</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-920">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-920">Prototype</span></span>

```c
UINT nx_snmp_object_compare(UCHAR *object, UCHAR *reference_object);
```

### <a name="description"></a><span data-ttu-id="06882-921">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-921">Description</span></span>

<span data-ttu-id="06882-922">Questo servizio confronta l'ID oggetto fornito con l'ID dell'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06882-922">This service compares the supplied object ID with the reference object ID.</span></span> <span data-ttu-id="06882-923">Entrambi gli ID oggetto si trovano nella notazione SMI ASCII, ad esempio, entrambi gli oggetti devono iniziare con la stringa ASCII "1.3.6".</span><span class="sxs-lookup"><span data-stu-id="06882-923">Both object IDs are in the ASCII SMI notation, e.g., both object must start with the ASCII string “1.3.6”.</span></span>

<span data-ttu-id="06882-924">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="06882-924">This service is deprecated.</span></span> <span data-ttu-id="06882-925">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_snmp_object_compare_extended ().*</span><span class="sxs-lookup"><span data-stu-id="06882-925">Developers are encouraged to migrate to *nx_snmp_object_compare_extended().*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-926">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-926">Input Parameters</span></span>

- <span data-ttu-id="06882-927">**oggetto** di Puntatore all'ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="06882-927">**object** Pointer to object ID.</span></span>
- <span data-ttu-id="06882-928">**reference_object** Puntatore all'ID dell'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06882-928">**reference_object** Pointer to the reference object ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-929">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-929">Return Values</span></span>

- <span data-ttu-id="06882-930">**NX_SUCCESS** (0x00) l'oggetto corrisponde all'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06882-930">**NX_SUCCESS** (0x00) The object matches the reference object.</span></span>
- <span data-ttu-id="06882-931">**NX_SNMP_NEXT_ENTRY** (0X101) l'oggetto è minore dell'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06882-931">**NX_SNMP_NEXT_ENTRY** (0x101) The object is less than the reference object.</span></span>
- <span data-ttu-id="06882-932">**NX_SNMP_ERROR** (0X100) l'oggetto è maggiore dell'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06882-932">**NX_SNMP_ERROR** (0x100) The object is greater than the reference object.</span></span>
- <span data-ttu-id="06882-933">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-933">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-934">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-934">Allowed From</span></span>

<span data-ttu-id="06882-935">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-935">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-936">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-936">Example</span></span>

```c
/* Compare “requested_object” with the sysDescr object ID of 
   "1.3.6.1.2.1.1.1.0".  */
Status =  nx_snmp_object_compare(requested_object, "1.3.6.1.2.1.1.1.0");

/* If status is NX_SUCCESS, requested_object is the sysDescr object. 
   Otherwise, if status is NX_SNMP_NEXT_ENTRY, the requested object is
   less than the sysDescr. If status is NX_SNMP_ERROR, the object is 
   greater than sysDescr. */
```

## <a name="nx_snmp_object_compare_extended"></a><span data-ttu-id="06882-937">nx_snmp_object_compare_extended</span><span class="sxs-lookup"><span data-stu-id="06882-937">nx_snmp_object_compare_extended</span></span>
<span data-ttu-id="06882-938">Confrontare due oggetti</span><span class="sxs-lookup"><span data-stu-id="06882-938">Compare two objects</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-939">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-939">Prototype</span></span>

```c
UINT nx_snmp_object_compare_extended(UCHAR *request_object, 
                                     UINT requested_object_length,
                                     UCHAR *reference_object
                                     UINT reference_object_length);
```
### <a name="description"></a><span data-ttu-id="06882-940">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-940">Description</span></span>

<span data-ttu-id="06882-941">Questo servizio confronta l'ID oggetto fornito con l'ID dell'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06882-941">This service compares the supplied object ID with the reference object ID.</span></span> <span data-ttu-id="06882-942">Entrambi gli ID oggetto si trovano nella notazione SMI ASCII, ad esempio, entrambi gli oggetti devono iniziare con la stringa ASCII "1.3.6".</span><span class="sxs-lookup"><span data-stu-id="06882-942">Both object IDs are in the ASCII SMI notation, e.g., both object must start with the ASCII string “1.3.6”.</span></span>

<span data-ttu-id="06882-943">Questo servizio sostituisce *nx_snmp_object_compare ().*</span><span class="sxs-lookup"><span data-stu-id="06882-943">This service replaces *nx_snmp_object_compare().*</span></span> <span data-ttu-id="06882-944">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza.</span><span class="sxs-lookup"><span data-stu-id="06882-944">This version requires callers to supply length information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-945">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-945">Input Parameters</span></span>

- <span data-ttu-id="06882-946">**Request_Object** Puntatore all'ID oggetto della richiesta.</span><span class="sxs-lookup"><span data-stu-id="06882-946">**request_object** Pointer to request object ID.</span></span>
- <span data-ttu-id="06882-947">**request_object_length** Lunghezza dell'ID dell'oggetto della richiesta.</span><span class="sxs-lookup"><span data-stu-id="06882-947">**request_object_length** Length of the request object ID.</span></span>
- <span data-ttu-id="06882-948">**reference_object** Puntatore all'ID dell'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06882-948">**reference_object** Pointer to the reference object ID.</span></span>
- <span data-ttu-id="06882-949">**reference_object_length** Lunghezza dell'ID dell'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06882-949">**reference_object_length** Length of the reference object ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-950">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-950">Return Values</span></span>

- <span data-ttu-id="06882-951">**NX_SUCCESS** (0x00) l'oggetto corrisponde all'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06882-951">**NX_SUCCESS** (0x00) The object matches the reference object.</span></span>
- <span data-ttu-id="06882-952">**NX_SNMP_NEXT_ENTRY** (0X101) l'oggetto è minore dell'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06882-952">**NX_SNMP_NEXT_ENTRY** (0x101) The object is less than the reference object.</span></span>
- <span data-ttu-id="06882-953">**NX_SNMP_ERROR** (0X100) l'oggetto è maggiore dell'oggetto di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06882-953">**NX_SNMP_ERROR** (0x100) The object is greater than the reference object.</span></span>
- <span data-ttu-id="06882-954">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-954">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-955">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-955">Allowed From</span></span>

<span data-ttu-id="06882-956">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-956">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-957">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-957">Example</span></span>

```c
/* Compare “requested_object” with the sysDescr object ID of 
   "1.3.6.1.2.1.1.1.0".  */
Status =  nx_snmp_object_compare_extended(requested_object, 17,
                                          "1.3.6.1.2.1.1.1.0", 17);

/* If status is NX_SUCCESS, requested_object is the sysDescr object. 
   Otherwise, if status is NX_SNMP_NEXT_ENTRY, the requested object is
   less than the sysDescr. If status is NX_SNMP_ERROR, the object is 
   greater than sysDescr. */
```

## <a name="nx_snmp_object_copy"></a><span data-ttu-id="06882-958">nx_snmp_object_copy</span><span class="sxs-lookup"><span data-stu-id="06882-958">nx_snmp_object_copy</span></span>
<span data-ttu-id="06882-959">Copia di un oggetto</span><span class="sxs-lookup"><span data-stu-id="06882-959">Copy an object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-960">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-960">Prototype</span></span>

```c
UINT  nx_snmp_object_copy(UCHAR *source_object_name, 
                          UCHAR *destination_object_name);
```
### <a name="description"></a><span data-ttu-id="06882-961">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-961">Description</span></span>

<span data-ttu-id="06882-962">Questo servizio Copia l'oggetto di origine nella notazione SIM ASCII nell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-962">This service copies the source object in ASCII SIM notation to the destination object.</span></span>

<span data-ttu-id="06882-963">questo servizio è deprecato.</span><span class="sxs-lookup"><span data-stu-id="06882-963">This service is deprecated.</span></span> <span data-ttu-id="06882-964">Gli sviluppatori sono invitati a eseguire la migrazione a *nx_snmp_object_copy_extended ().*</span><span class="sxs-lookup"><span data-stu-id="06882-964">Developers are encouraged to migrate to *nx_snmp_object_copy_extended().*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-965">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-965">Input Parameters</span></span>

- <span data-ttu-id="06882-966">**source_object_name** Puntatore all'ID dell'oggetto di origine.</span><span class="sxs-lookup"><span data-stu-id="06882-966">**source_object_name** Pointer to source object ID.</span></span>
- <span data-ttu-id="06882-967">**destination_object_name** Puntatore all'ID dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-967">**destination_object_name** Pointer to destination object ID.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-968">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-968">Return Values</span></span>

- <span data-ttu-id="06882-969">**dimensioni** Numero di byte copiati nel nome di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-969">**size** Number of bytes copied to destination name.</span></span> <span data-ttu-id="06882-970">Se Error, viene restituito zero.</span><span class="sxs-lookup"><span data-stu-id="06882-970">If error, zero is returned.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-971">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-971">Allowed From</span></span>

<span data-ttu-id="06882-972">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-972">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-973">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-973">Example</span></span>

```c
/* Copy “my_object” to “my_new_object”.  */
size =  nx_snmp_object_copy(my_object, my_new_object);

/* Size contains the number of bytes copied. */
```

## <a name="nx_snmp_object_copy_extended"></a><span data-ttu-id="06882-974">nx_snmp_object_copy_extended</span><span class="sxs-lookup"><span data-stu-id="06882-974">nx_snmp_object_copy_extended</span></span>
<span data-ttu-id="06882-975">Copia di un oggetto</span><span class="sxs-lookup"><span data-stu-id="06882-975">Copy an object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-976">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-976">Prototype</span></span>

```c
UINT  nx_snmp_object_copy_extended(UCHAR *source_object_name, 
                             UINT source_object_name_length,
                             UCHAR *destination_object_name_buffer,
                             UINT destination_object_name_buffer_size);
```

### <a name="description"></a><span data-ttu-id="06882-977">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-977">Description</span></span>

<span data-ttu-id="06882-978">Questo servizio Copia l'oggetto di origine nella notazione SIM ASCII nell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-978">This service copies the source object in ASCII SIM notation to the destination object.</span></span>

<span data-ttu-id="06882-979">Questo servizio sostituisce *nx_snmp_object_copy ().*</span><span class="sxs-lookup"><span data-stu-id="06882-979">This service replaces *nx_snmp_object_copy().*</span></span> <span data-ttu-id="06882-980">Questa versione richiede che i chiamanti forniscano informazioni sulla lunghezza.</span><span class="sxs-lookup"><span data-stu-id="06882-980">This version requires callers to supply length information.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-981">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-981">Input Parameters</span></span>

- <span data-ttu-id="06882-982">**source_object_name** Puntatore all'ID dell'oggetto di origine.</span><span class="sxs-lookup"><span data-stu-id="06882-982">**source_object_name** Pointer to source object ID.</span></span>
- <span data-ttu-id="06882-983">**source_object_name_length** Lunghezza dell'ID dell'oggetto di origine.</span><span class="sxs-lookup"><span data-stu-id="06882-983">**source_object_name_length** Length of source object ID.</span></span>
- <span data-ttu-id="06882-984">**destination_object_name_buffer** Puntatore al buffer dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-984">**destination_object_name_buffer** Pointer to destination object buffer.</span></span>
- <span data-ttu-id="06882-985">**destination_object_name_buffer_size** Dimensioni del buffer dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-985">**destination_object_name_buffer_size** Size of destination object buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-986">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-986">Return Values</span></span>

- <span data-ttu-id="06882-987">**dimensioni** Numero di byte copiati nel nome di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-987">**size** Number of bytes copied to destination name.</span></span> <span data-ttu-id="06882-988">Se Error, viene restituito zero.</span><span class="sxs-lookup"><span data-stu-id="06882-988">If error, zero is returned.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-989">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-989">Allowed From</span></span>

<span data-ttu-id="06882-990">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-990">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-991">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-991">Example</span></span>

```c
UCHAR   my_object = "1.3.6.1.2.1.1.1.0";
UCHAR   my_new_object[32];


/* Copy “my_object” to “my_new_object”.  */
size =  nx_snmp_object_copy(my_object, 17, my_new_object, sizeof(my_new_object));

/* Size contains the number of bytes copied. */
```

## <a name="nx_snmp_object_counter_get"></a><span data-ttu-id="06882-992">nx_snmp_object_counter_get</span><span class="sxs-lookup"><span data-stu-id="06882-992">nx_snmp_object_counter_get</span></span>
<span data-ttu-id="06882-993">Ottenere un oggetto contatore</span><span class="sxs-lookup"><span data-stu-id="06882-993">Get counter object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-994">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-994">Prototype</span></span>

```c
UINT  nx_snmp_object_counter_get(VOID *source_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```
### <a name="description"></a><span data-ttu-id="06882-995">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-995">Description</span></span>

<span data-ttu-id="06882-996">Questo servizio recupera l'oggetto contatore in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-996">This service retrieves the counter object at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="06882-997">Questa routine viene in genere chiamata dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-997">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-998">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-998">Input Parameters</span></span>

- <span data-ttu-id="06882-999">**source_ptr** Puntatore all'origine del contatore.</span><span class="sxs-lookup"><span data-stu-id="06882-999">**source_ptr** Pointer to counter source.</span></span>
- <span data-ttu-id="06882-1000">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1000">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1001">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1001">Return Values</span></span>

- <span data-ttu-id="06882-1002">**NX_SUCCESS** (0x00) è stato recuperato correttamente l'oggetto contatore.</span><span class="sxs-lookup"><span data-stu-id="06882-1002">**NX_SUCCESS** (0x00) The counter object has be successfully retrieved.</span></span>
- <span data-ttu-id="06882-1003">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1003">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1004">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1004">Allowed From</span></span>

<span data-ttu-id="06882-1005">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1005">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1006">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1006">Example</span></span>

```c
/* Get the ifInOctets (1.3.6.1.2.1.2.2.1.10.0) MIB-2 object.  */
status =  nx_snmp_object_counter_get(&ifInOctets, my_object);

/* If status is NX_SUCCESS, the ifInOctets object has been 
   retrieved and is ready to be returned. */
```

## <a name="nx_snmp_object_counter_set"></a><span data-ttu-id="06882-1007">nx_snmp_object_counter_set</span><span class="sxs-lookup"><span data-stu-id="06882-1007">nx_snmp_object_counter_set</span></span>
<span data-ttu-id="06882-1008">Imposta oggetto contatore</span><span class="sxs-lookup"><span data-stu-id="06882-1008">Set counter object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1009">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1009">Prototype</span></span>

```c
UINT  nx_snmp_object_counter_set(VOID *destination_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1010">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1010">Description</span></span>

<span data-ttu-id="06882-1011">Questo servizio imposta il contatore in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con il valore del contatore nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1011">This service sets the counter at the address specified by the destination pointer with the counter value in the NetX object data structure.</span></span> <span data-ttu-id="06882-1012">Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.</span><span class="sxs-lookup"><span data-stu-id="06882-1012">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1013">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1013">Input Parameters</span></span>

- <span data-ttu-id="06882-1014">**destination_ptr** Puntatore alla destinazione del contatore.</span><span class="sxs-lookup"><span data-stu-id="06882-1014">**destination_ptr** Pointer to counter destination.</span></span>
- <span data-ttu-id="06882-1015">**object_data** Puntatore alla struttura dell'oggetto di origine del contatore.</span><span class="sxs-lookup"><span data-stu-id="06882-1015">**object_data** Pointer to counter source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1016">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1016">Return Values</span></span>

- <span data-ttu-id="06882-1017">**NX_SUCCESS** (0x00) l'oggetto contatore è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1017">**NX_SUCCESS** (0x00) The counter object has be successfully set.</span></span>
- <span data-ttu-id="06882-1018">Il tipo di oggetto **NX_SNMP_ERROR_WRONGTYPE** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1018">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="06882-1019">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1019">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1020">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1020">Allowed From</span></span>

<span data-ttu-id="06882-1021">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1021">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1022">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1022">Example</span></span>

```c
/* Set the ifInOctets (1.3.6.1.2.1.2.2.1.10.0) MIB-2 object with
   the counter object value contained in my_object.  */
status =  nx_snmp_object_counter_set(&ifInOctets, my_object);

/* If status is NX_SUCCESS, the ifInOctets object has been 
   set. */
```

## <a name="nx_snmp_object_counter64_get"></a><span data-ttu-id="06882-1023">nx_snmp_object_counter64_get</span><span class="sxs-lookup"><span data-stu-id="06882-1023">nx_snmp_object_counter64_get</span></span>
<span data-ttu-id="06882-1024">Ottenere un oggetto contatore a 64 bit</span><span class="sxs-lookup"><span data-stu-id="06882-1024">Get 64-bit counter object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1025">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1025">Prototype</span></span>

```c
UINT  nx_snmp_object_counter64_get(VOID *source_ptr, 
                                   NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1026">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1026">Description</span></span>

<span data-ttu-id="06882-1027">Questo servizio recupera l'oggetto contatore a 64 bit in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1027">This service retrieves the 64-bit counter object at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="06882-1028">Questa routine viene in genere chiamata dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1028">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1029">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1029">Input Parameters</span></span>

- <span data-ttu-id="06882-1030">**source_ptr** Puntatore all'origine del contatore.</span><span class="sxs-lookup"><span data-stu-id="06882-1030">**source_ptr** Pointer to counter source.</span></span>
- <span data-ttu-id="06882-1031">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1031">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1032">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1032">Return Values</span></span>

- <span data-ttu-id="06882-1033">**NX_SUCCESS** (0x00) è stato recuperato correttamente l'oggetto contatore.</span><span class="sxs-lookup"><span data-stu-id="06882-1033">**NX_SUCCESS** (0x00) The counter object has be successfully retrieved.</span></span>
- <span data-ttu-id="06882-1034">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1034">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1035">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1035">Allowed From</span></span>

<span data-ttu-id="06882-1036">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1036">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1037">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1037">Example</span></span>

```c
/* Get the value of my_64_bit_counter and place it into my_object
   for return.  */
status =  nx_snmp_object_counter64_get(&my_64_bit_counter, my_object);

/* If status is NX_SUCCESS, the my_64_bit_counter object has been 
   retrieved and is ready to be returned. */
```

## <a name="nx_snmp_object_counter64_set"></a><span data-ttu-id="06882-1038">nx_snmp_object_counter64_set</span><span class="sxs-lookup"><span data-stu-id="06882-1038">nx_snmp_object_counter64_set</span></span>
<span data-ttu-id="06882-1039">Imposta oggetto contatore a 64 bit</span><span class="sxs-lookup"><span data-stu-id="06882-1039">Set 64-bit counter object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1040">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1040">Prototype</span></span>

```c
UINT  nx_snmp_object_counter64_set(VOID *destination_ptr, 
                                   NX_SNMP_OBJECT_DATA *object_data);
```
### <a name="description"></a><span data-ttu-id="06882-1041">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1041">Description</span></span>

<span data-ttu-id="06882-1042">Questo servizio imposta il contatore a 64 bit in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con il valore del contatore nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1042">This service sets the 64-bit counter at the address specified by the destination pointer with the counter value in the NetX object data structure.</span></span> <span data-ttu-id="06882-1043">Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.</span><span class="sxs-lookup"><span data-stu-id="06882-1043">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1044">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1044">Input Parameters</span></span>

- <span data-ttu-id="06882-1045">**destination_ptr** Puntatore alla destinazione del contatore.</span><span class="sxs-lookup"><span data-stu-id="06882-1045">**destination_ptr** Pointer to counter destination.</span></span>
- <span data-ttu-id="06882-1046">**object_data** Puntatore alla struttura dell'oggetto di origine del contatore.</span><span class="sxs-lookup"><span data-stu-id="06882-1046">**object_data** Pointer to counter source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1047">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1047">Return Values</span></span>

- <span data-ttu-id="06882-1048">**NX_SUCCESS** (0x00) l'oggetto contatore è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1048">**NX_SUCCESS** (0x00) The counter object has be successfully set.</span></span>
- <span data-ttu-id="06882-1049">Il tipo di oggetto **NX_SNMP_ERROR_WRONGTYPE** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1049">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="06882-1050">**NX_PTR_ERROR** (0x07) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1050">**NX_PTR_ERROR** (0x07) Invalid input pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1051">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1051">Allowed From</span></span>

<span data-ttu-id="06882-1052">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1052">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1053">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1053">Example</span></span>

```c
/* Set the value of my_64_bit_counter with the value in my_object.  */
status =  nx_snmp_object_counter64_set(&my_64_bit_counter, my_object);

/* If status is NX_SUCCESS, the my_64_bit_counter object has been 
   set. */
```

## <a name="nx_snmp_object_end_of_mib"></a><span data-ttu-id="06882-1054">nx_snmp_object_end_of_mib</span><span class="sxs-lookup"><span data-stu-id="06882-1054">nx_snmp_object_end_of_mib</span></span>
<span data-ttu-id="06882-1055">Impostare il valore di fine del MIB</span><span class="sxs-lookup"><span data-stu-id="06882-1055">Set end-of-mib value</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1056">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1056">Prototype</span></span>

```c
UINT  nx_snmp_object_end_of_mib(VOID *not_used_ptr, 
                              NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1057">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1057">Description</span></span>

<span data-ttu-id="06882-1058">Questo servizio crea un oggetto che segnala la fine del MIB e viene in genere chiamato dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1058">This service creates an object signaling the end of the MIB and is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1059">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1059">Input Parameters</span></span>

- <span data-ttu-id="06882-1060">**not_used_ptr** Puntatore non utilizzato: deve essere NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="06882-1060">**not_used_ptr** Pointer not used – should be NX_NULL.</span></span>
- <span data-ttu-id="06882-1061">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1061">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1062">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1062">Return Values</span></span>

- <span data-ttu-id="06882-1063">**NX_SUCCESS** (0x00) l'oggetto End-of-MIB è stato compilato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1063">**NX_SUCCESS** (0x00) The end-of-mib object has be successfully built.</span></span>
- <span data-ttu-id="06882-1064">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1064">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1065">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1065">Allowed From</span></span>

<span data-ttu-id="06882-1066">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1066">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1067">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1067">Example</span></span>

```c
/* Place an end-of-mib value in my_object.  */
status =  nx_snmp_object_end_of_mib(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now an end-of-mib object. */
```

## <a name="nx_snmp_object_gauge_get"></a><span data-ttu-id="06882-1068">nx_snmp_object_gauge_get</span><span class="sxs-lookup"><span data-stu-id="06882-1068">nx_snmp_object_gauge_get</span></span>
<span data-ttu-id="06882-1069">Ottenere un oggetto misuratore</span><span class="sxs-lookup"><span data-stu-id="06882-1069">Get gauge object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1070">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1070">Prototype</span></span>

```c
UINT  nx_snmp_object_gauge_get(VOID *source_ptr, 
                               NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1071">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1071">Description</span></span>

<span data-ttu-id="06882-1072">Questo servizio recupera l'oggetto misuratore in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1072">This service retrieves the gauge object at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="06882-1073">Questa routine viene in genere chiamata dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1073">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1074">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1074">Input Parameters</span></span>

- <span data-ttu-id="06882-1075">**source_ptr** Puntatore all'origine del misuratore.</span><span class="sxs-lookup"><span data-stu-id="06882-1075">**source_ptr** Pointer to gauge source.</span></span>
- <span data-ttu-id="06882-1076">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1076">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1077">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1077">Return Values</span></span>

- <span data-ttu-id="06882-1078">**NX_SUCCESS** (0x00) è stato recuperato correttamente l'oggetto misuratore.</span><span class="sxs-lookup"><span data-stu-id="06882-1078">**NX_SUCCESS** (0x00) The gauge object has be successfully retrieved.</span></span>
- <span data-ttu-id="06882-1079">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1079">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1080">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1080">Allowed From</span></span>

<span data-ttu-id="06882-1081">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1081">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1082">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1082">Example</span></span>

```c
/* Get the value of ifSpeed (1.3.6.1.2.1.2.2.1.5.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_gauge_get(&ifSpeed, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ifSpeed gauge value. */
```

## <a name="nx_snmp_object_gauge_set"></a><span data-ttu-id="06882-1083">nx_snmp_object_gauge_set</span><span class="sxs-lookup"><span data-stu-id="06882-1083">nx_snmp_object_gauge_set</span></span>
<span data-ttu-id="06882-1084">Imposta oggetto misuratore</span><span class="sxs-lookup"><span data-stu-id="06882-1084">Set gauge object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1085">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1085">Prototype</span></span>

```c
UINT  nx_snmp_object_gauge_set(VOID *destination_ptr,
                                     NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1086">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1086">Description</span></span>

<span data-ttu-id="06882-1087">Questo servizio imposta il misuratore in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con il valore del misuratore nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1087">This service sets the gauge at the address specified by the destination pointer with the gauge value in the NetX object data structure.</span></span> <span data-ttu-id="06882-1088">Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.</span><span class="sxs-lookup"><span data-stu-id="06882-1088">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1089">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1089">Input Parameters</span></span>

- <span data-ttu-id="06882-1090">**destination_ptr** Puntatore alla destinazione del misuratore.</span><span class="sxs-lookup"><span data-stu-id="06882-1090">**destination_ptr** Pointer to gauge destination.</span></span>
- <span data-ttu-id="06882-1091">**object_data** Puntatore alla struttura dell'oggetto di origine del misuratore.</span><span class="sxs-lookup"><span data-stu-id="06882-1091">**object_data** Pointer to gauge source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1092">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1092">Return Values</span></span>

- <span data-ttu-id="06882-1093">**NX_SUCCESS** (0x00) l'oggetto misuratore è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1093">**NX_SUCCESS** (0x00) The gauge object has be successfully set.</span></span>
- <span data-ttu-id="06882-1094">Il tipo di oggetto **NX_SNMP_ERROR_WRONGTYPE** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1094">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="06882-1095">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1095">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1096">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1096">Allowed From</span></span>

<span data-ttu-id="06882-1097">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1097">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1098">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1098">Example</span></span>

```c
/* Set the value of “my_gauge” from the gauge value in my_object.  */
status =  nx_snmp_object_gauge_set(&my_gauge, my_object);

/* If status is NX_SUCCESS, the my_gauge now contains the new gauge value. */
```

## <a name="nx_snmp_object_id_get"></a><span data-ttu-id="06882-1099">nx_snmp_object_id_get</span><span class="sxs-lookup"><span data-stu-id="06882-1099">nx_snmp_object_id_get</span></span>
<span data-ttu-id="06882-1100">Ottieni ID oggetto</span><span class="sxs-lookup"><span data-stu-id="06882-1100">Get object id</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1101">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1101">Prototype</span></span>

```c
UINT  nx_snmp_object_id_get(VOID *source_ptr, 
                            NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1102">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1102">Description</span></span>

<span data-ttu-id="06882-1103">Questo servizio recupera l'ID oggetto (nella notazione ASCII SIM) all'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1103">This service retrieves the object ID (in ASCII SIM notation) at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="06882-1104">Questa routine viene in genere chiamata dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1104">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1105">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1105">Input Parameters</span></span>

- <span data-ttu-id="06882-1106">**source_ptr** Puntatore all'origine dell'ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="06882-1106">**source_ptr** Pointer to object ID source.</span></span>
- <span data-ttu-id="06882-1107">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1107">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1108">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1108">Return Values</span></span>

- <span data-ttu-id="06882-1109">**NX_SUCCESS** (0x00) l'ID oggetto è stato recuperato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1109">**NX_SUCCESS** (0x00) The object ID has be successfully retrieved.</span></span>
- <span data-ttu-id="06882-1110">Lunghezza dell'oggetto **NX_SNMP_ERROR** (0X100) non valida</span><span class="sxs-lookup"><span data-stu-id="06882-1110">**NX_SNMP_ERROR** (0x100) Invalid length of object</span></span>
- <span data-ttu-id="06882-1111">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1111">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1112">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1112">Allowed From</span></span>

<span data-ttu-id="06882-1113">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1113">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1114">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1114">Example</span></span>

```c
/* Get the value of sysObjectID(1.3.6.1.2.1.1.2.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_id_get(&sysObjectID, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysObjectID value. */
```

## <a name="nx_snmp_object_id_set"></a><span data-ttu-id="06882-1115">nx_snmp_object_id_set</span><span class="sxs-lookup"><span data-stu-id="06882-1115">nx_snmp_object_id_set</span></span>
<span data-ttu-id="06882-1116">Imposta ID oggetto</span><span class="sxs-lookup"><span data-stu-id="06882-1116">Set object id</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1117">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1117">Prototype</span></span>

```c
UINT  nx_snmp_object_id_set(VOID *destination_ptr, 
                             NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1118">Description</span></span>

<span data-ttu-id="06882-1119">Questo servizio imposta l'ID oggetto (nella notazione ASCII SIM) nell'indirizzo specificato dal puntatore di destinazione con l'ID oggetto nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1119">This service sets the object ID (in ASCII SIM notation) at the address specified by the destination pointer with the object ID in the NetX object data structure.</span></span> <span data-ttu-id="06882-1120">Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.</span><span class="sxs-lookup"><span data-stu-id="06882-1120">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1121">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1121">Input Parameters</span></span>

- <span data-ttu-id="06882-1122">**destination_ptr** Puntatore alla destinazione ID oggetto.</span><span class="sxs-lookup"><span data-stu-id="06882-1122">**destination_ptr** Pointer to object ID destination.</span></span>
- <span data-ttu-id="06882-1123">**object_data** Puntatore alla struttura dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="06882-1123">**object_data** Pointer to object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1124">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1124">Return Values</span></span>

- <span data-ttu-id="06882-1125">**NX_SUCCESS** (0x00) l'ID oggetto è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1125">**NX_SUCCESS** (0x00) The object ID has been successfully set.</span></span>
- <span data-ttu-id="06882-1126">Il tipo di oggetto **NX_SNMP_ERROR_WRONGTYPE** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1126">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="06882-1127">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1127">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1128">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1128">Allowed From</span></span>

<span data-ttu-id="06882-1129">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1129">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1130">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1130">Example</span></span>

```c
/* Set the string “my_object_id” with the object ID value contained 
   in my_object.  */
status =  nx_snmp_object_id_set(my_object_id, my_object);

/* If status is NX_SUCCESS, the my_object_id now contains the object ID value. */
```

## <a name="nx_snmp_object_integer_get"></a><span data-ttu-id="06882-1131">nx_snmp_object_integer_get</span><span class="sxs-lookup"><span data-stu-id="06882-1131">nx_snmp_object_integer_get</span></span>
<span data-ttu-id="06882-1132">Ottenere un oggetto Integer</span><span class="sxs-lookup"><span data-stu-id="06882-1132">Get integer object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1133">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1133">Prototype</span></span>

```c
UINT  nx_snmp_object_integer_get(VOID *source_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1134">Description</span></span>

<span data-ttu-id="06882-1135">Questo servizio recupera l'oggetto Integer in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1135">This service retrieves the integer object at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="06882-1136">Questa routine viene in genere chiamata dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1136">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1137">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1137">Input Parameters</span></span>

- <span data-ttu-id="06882-1138">**source_ptr** Puntatore all'origine Integer.</span><span class="sxs-lookup"><span data-stu-id="06882-1138">**source_ptr** Pointer to integer source.</span></span>
- <span data-ttu-id="06882-1139">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1139">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1140">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1140">Return Values</span></span>

- <span data-ttu-id="06882-1141">**NX_SUCCESS** (0x00) l'oggetto Integer è stato recuperato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1141">**NX_SUCCESS** (0x00) The integer object has been successfully retrieved.</span></span>
- <span data-ttu-id="06882-1142">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1142">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1143">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1143">Allowed From</span></span>

<span data-ttu-id="06882-1144">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1144">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1145">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1145">Example</span></span>

```c
/* Get the value of sysServices (1.3.6.1.2.1.1.7.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_integer_get(&sysServices, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysServices value. */
```

## <a name="nx_snmp_object_integer_set"></a><span data-ttu-id="06882-1146">nx_snmp_object_integer_set</span><span class="sxs-lookup"><span data-stu-id="06882-1146">nx_snmp_object_integer_set</span></span>
<span data-ttu-id="06882-1147">Imposta oggetto Integer</span><span class="sxs-lookup"><span data-stu-id="06882-1147">Set integer object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1148">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1148">Prototype</span></span>

```c
UINT  nx_snmp_object_integer_set(VOID *destination_ptr,
                                      NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1149">Description</span></span>

<span data-ttu-id="06882-1150">Questo servizio imposta il numero intero all'indirizzo specificato dal puntatore di destinazione con il valore integer nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1150">This service sets the integer at the address specified by the destination pointer with the integer value in the NetX object data structure.</span></span> <span data-ttu-id="06882-1151">Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.</span><span class="sxs-lookup"><span data-stu-id="06882-1151">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1152">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1152">Input Parameters</span></span>

- <span data-ttu-id="06882-1153">**destination_ptr** Puntatore alla destinazione Integer.</span><span class="sxs-lookup"><span data-stu-id="06882-1153">**destination_ptr** Pointer to integer destination.</span></span>
- <span data-ttu-id="06882-1154">**object_data** Puntatore alla struttura dell'oggetto di origine di tipo Integer.</span><span class="sxs-lookup"><span data-stu-id="06882-1154">**object_data** Pointer to integer source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1155">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1155">Return Values</span></span>

- <span data-ttu-id="06882-1156">**NX_SUCCESS** (0x00) l'oggetto Integer è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1156">**NX_SUCCESS** (0x00) The integer object has been successfully set.</span></span>
- <span data-ttu-id="06882-1157">Il tipo di oggetto **NX_SNMP_ERROR_WRONGTYPE** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1157">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="06882-1158">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1158">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1159">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1159">Allowed From</span></span>

<span data-ttu-id="06882-1160">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1160">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1161">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1161">Example</span></span>

```c
/* Set the value of ifAdminStatus from the integer value in my_object.  */
status =  nx_snmp_object_integer_set(&ifAdminStatus, my_object);

/* If status is NX_SUCCESS, ifAdnminStatus now contains the new integer value. */
```

## <a name="nx_snmp_object_ip_address_get"></a><span data-ttu-id="06882-1162">nx_snmp_object_ip_address_get</span><span class="sxs-lookup"><span data-stu-id="06882-1162">nx_snmp_object_ip_address_get</span></span>
<span data-ttu-id="06882-1163">Ottenere l'oggetto indirizzo IP (solo IPv4)</span><span class="sxs-lookup"><span data-stu-id="06882-1163">Get IP address object (IPv4 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-1164">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1164">Prototype</span></span>

```c
UINT  nx_snmp_object_ip_address_get(VOID *source_ptr,
                                          NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1165">Description</span></span>

<span data-ttu-id="06882-1166">Questo servizio recupera l'oggetto indirizzo IP in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1166">This service retrieves the IP address object at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="06882-1167">Questa routine viene in genere chiamata dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1167">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1168">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1168">Input Parameters</span></span>

- <span data-ttu-id="06882-1169">**source_ptr** Puntatore all'origine dell'indirizzo IPv4.</span><span class="sxs-lookup"><span data-stu-id="06882-1169">**source_ptr** Pointer to IPv4 address source.</span></span>
- <span data-ttu-id="06882-1170">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1170">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1171">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1171">Return Values</span></span>

- <span data-ttu-id="06882-1172">**NX_SUCCESS** (0x00) l'oggetto indirizzo IP è stato recuperato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1172">**NX_SUCCESS** (0x00) The IP address object has been successfully retrieved.</span></span>
- <span data-ttu-id="06882-1173">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1173">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1174">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1174">Allowed From</span></span>

<span data-ttu-id="06882-1175">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1175">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1176">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1176">Example</span></span>

```c
/* Get the value of ipAdEntAddr (1.3.6.1.2.1.4.20.1.1.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_ip_address_get(&ipAdEntAddr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ipAdEntAddr value. */
```

## <a name="nx_snmp_object_ipv6_address_get"></a><span data-ttu-id="06882-1177">nx_snmp_object_ipv6_address_get</span><span class="sxs-lookup"><span data-stu-id="06882-1177">nx_snmp_object_ipv6_address_get</span></span>
<span data-ttu-id="06882-1178">Ottenere l'oggetto indirizzo IP (solo IPv6)</span><span class="sxs-lookup"><span data-stu-id="06882-1178">Get IP address object (IPv6 only)</span></span>

### <a name="prototype"></a><span data-ttu-id="06882-1179">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1179">Prototype</span></span>

```c
UINT  nx_snmp_object_ipv6_address_get(VOID *source_ptr,
                                          NX_SNMP_OBJECT_DATA 
                                      *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1180">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1180">Description</span></span>

<span data-ttu-id="06882-1181">Questo servizio recupera l'oggetto indirizzo IPv6 in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1181">This service retrieves the IPv6 address object at the address specified by the source pointer and places it in the NetX object data structure.</span></span>
<span data-ttu-id="06882-1182">Questa routine viene in genere chiamata dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1182">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1183">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1183">Input Parameters</span></span>

- <span data-ttu-id="06882-1184">**source_ptr** Puntatore all'origine dell'indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="06882-1184">**source_ptr** Pointer to IPv6 address source.</span></span>
- <span data-ttu-id="06882-1185">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1185">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1186">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1186">Return Values</span></span>

- <span data-ttu-id="06882-1187">**NX_SUCCESS** (0x00) l'oggetto indirizzo IP è stato recuperato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1187">**NX_SUCCESS** (0x00) The IP address object has been successfully retrieved.</span></span>
- <span data-ttu-id="06882-1188">**NX_SNMP_ERROR_WRONGTYPE** (0x07) codice oggetto SNMP di input errato</span><span class="sxs-lookup"><span data-stu-id="06882-1188">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Incorrect input SNMP object code</span></span>
- <span data-ttu-id="06882-1189">IPv6 **NX_NOT_ENABLED** (0x14) non abilitato</span><span class="sxs-lookup"><span data-stu-id="06882-1189">**NX_NOT_ENABLED** (0x14) IPv6 not enabled</span></span>
- <span data-ttu-id="06882-1190">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1190">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1191">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1191">Allowed From</span></span>

<span data-ttu-id="06882-1192">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1192">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1193">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1193">Example</span></span>

```c
/* Get the value of ipAdEntAddr (1.3.6.1.2.1.4.20.1.1.0) and place it in my_object
   for return.  */
status =  nx_snmp_object_ipv6_address_get(&ipAdEntAddr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the ipAdEntAddr value. */
```

## <a name="nx_snmp_object_ip_address_set"></a><span data-ttu-id="06882-1194">nx_snmp_object_ip_address_set</span><span class="sxs-lookup"><span data-stu-id="06882-1194">nx_snmp_object_ip_address_set</span></span>
<span data-ttu-id="06882-1195">Imposta oggetto indirizzo IPv4</span><span class="sxs-lookup"><span data-stu-id="06882-1195">Set IPv4 address object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1196">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1196">Prototype</span></span>

```c
UINT  nx_snmp_object_ip_address_set(VOID *destination_ptr, 
                                    NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1197">Description</span></span>

<span data-ttu-id="06882-1198">Questo servizio imposta l'indirizzo IPv4 in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con l'indirizzo IP nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1198">This service sets the IPv4 address at the address specified by the destination pointer with the IP address in the NetX object data structure.</span></span> <span data-ttu-id="06882-1199">Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.</span><span class="sxs-lookup"><span data-stu-id="06882-1199">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1200">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1200">Input Parameters</span></span>

- <span data-ttu-id="06882-1201">**destination_ptr** Puntatore all'indirizzo IP da impostare.</span><span class="sxs-lookup"><span data-stu-id="06882-1201">**destination_ptr** Pointer to IP address to set.</span></span>
- <span data-ttu-id="06882-1202">**object_data** Puntatore alla struttura dell'oggetto indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="06882-1202">**object_data** Pointer to IP address object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1203">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1203">Return Values</span></span>

- <span data-ttu-id="06882-1204">**NX_SUCCESS** (0x00) l'oggetto indirizzo IP è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1204">**NX_SUCCESS** (0x00) The IP address object has been successfully set.</span></span>
- <span data-ttu-id="06882-1205">Il tipo di oggetto **NX_SNMP_ERROR_WRONGTYPE** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1205">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="06882-1206">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1206">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1207">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1207">Allowed From</span></span>

<span data-ttu-id="06882-1208">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1208">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1209">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1209">Example</span></span>

```c
/* Set the value of atNetworkAddress to the IP address in my_object.  */
status =  nx_snmp_object_ip_address_set(&atNetworkAddress, my_object);

/* If status is NX_SUCCESS, atNetWorkAddress now contains the new IP address. */
```

## <a name="nx_snmp_object_ipv6_address_set"></a><span data-ttu-id="06882-1210">nx_snmp_object_ipv6_address_set</span><span class="sxs-lookup"><span data-stu-id="06882-1210">nx_snmp_object_ipv6_address_set</span></span>
<span data-ttu-id="06882-1211">Imposta oggetto indirizzo IPv6</span><span class="sxs-lookup"><span data-stu-id="06882-1211">Set IPv6 address object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1212">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1212">Prototype</span></span>

```c
UINT  nx_snmp_object_ipv6_address_set(VOID *destination_ptr, 
                                      NX_SNMP_OBJECT_DATA  
                                      *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1213">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1213">Description</span></span>

<span data-ttu-id="06882-1214">Questo servizio imposta l'indirizzo IPv6 in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con l'indirizzo IP nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1214">This service sets the IPv6 address at the address specified by the destination pointer with the IP address in the NetX object data structure.</span></span> <span data-ttu-id="06882-1215">Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.</span><span class="sxs-lookup"><span data-stu-id="06882-1215">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1216">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1216">Input Parameters</span></span>

- <span data-ttu-id="06882-1217">**destination_ptr** Puntatore all'indirizzo IP da impostare.</span><span class="sxs-lookup"><span data-stu-id="06882-1217">**destination_ptr** Pointer to IP address to set.</span></span>
- <span data-ttu-id="06882-1218">**object_data** Puntatore alla struttura dell'oggetto indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="06882-1218">**object_data** Pointer to IP address object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1219">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1219">Return Values</span></span>

- <span data-ttu-id="06882-1220">**NX_SUCCESS** (0x00) l'indirizzo IPv6 è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1220">**NX_SUCCESS** (0x00) The IPv6 address has been successfully set.</span></span>
- <span data-ttu-id="06882-1221">Il tipo di oggetto **NX_SNMP_ERROR_WRONGTYPE** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1221">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="06882-1222">IPv6 **NX_NOT_ENABLED** (0x14) non abilitato</span><span class="sxs-lookup"><span data-stu-id="06882-1222">**NX_NOT_ENABLED** (0x14) IPv6 not enabled</span></span>
- <span data-ttu-id="06882-1223">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1223">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1224">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1224">Allowed From</span></span>

<span data-ttu-id="06882-1225">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1225">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1226">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1226">Example</span></span>

```c
/* Set the value of atNetworkAddress to the IP address in my_object.  */
status =  nx_snmp_object_ipv6_address_set(&atNetworkAddress, my_object);

/* If status is NX_SUCCESS, atNetWorkAddress now contains the new IP address. */
```

## <a name="nx_snmp_object_no_instance"></a><span data-ttu-id="06882-1227">nx_snmp_object_no_instance</span><span class="sxs-lookup"><span data-stu-id="06882-1227">nx_snmp_object_no_instance</span></span>
<span data-ttu-id="06882-1228">Imposta oggetto senza istanza</span><span class="sxs-lookup"><span data-stu-id="06882-1228">Set no-instance object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1229">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1229">Prototype</span></span>

```c
UINT  nx_snmp_object_no_instance(VOID *not_used_ptr, 
                                 NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1230">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1230">Description</span></span>

<span data-ttu-id="06882-1231">Questo servizio crea un oggetto che segnala che non è presente alcuna istanza dell'oggetto specificato e viene in genere chiamato dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1231">This service creates an object signaling that there was no instance of the specified object and is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1232">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1232">Input Parameters</span></span>

- <span data-ttu-id="06882-1233">**not_used_ptr** Puntatore non utilizzato: deve essere NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="06882-1233">**not_used_ptr** Pointer not used – should be NX_NULL.</span></span>
- <span data-ttu-id="06882-1234">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1234">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1235">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1235">Return Values</span></span>

- <span data-ttu-id="06882-1236">**NX_SUCCESS** (0x00) l'oggetto senza istanza è stato compilato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1236">**NX_SUCCESS** (0x00) The no-instance object has been successfully built.</span></span>
- <span data-ttu-id="06882-1237">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1237">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1238">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1238">Allowed From</span></span>

<span data-ttu-id="06882-1239">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1239">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1240">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1240">Example</span></span>

```c
/* Place no-instance value in my_object.  */
status =  nx_snmp_object_no_instance(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now a no-instance object. */
```

## <a name="nx_snmp_object_not_found"></a><span data-ttu-id="06882-1241">nx_snmp_object_not_found</span><span class="sxs-lookup"><span data-stu-id="06882-1241">nx_snmp_object_not_found</span></span>
<span data-ttu-id="06882-1242">Impostazione oggetto non trovato</span><span class="sxs-lookup"><span data-stu-id="06882-1242">Set not-found object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1243">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1243">Prototype</span></span>

```c
UINT  nx_snmp_object_not_found(VOID *not_used_ptr, 
                               NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1244">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1244">Description</span></span>

<span data-ttu-id="06882-1245">Questo servizio crea un oggetto che segnala che l'oggetto non è stato trovato e viene in genere chiamato dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1245">This service creates an object signaling the object was not found and is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1246">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1246">Input Parameters</span></span>

- <span data-ttu-id="06882-1247">**not_used_ptr** Puntatore non utilizzato: deve essere NX_NULL.</span><span class="sxs-lookup"><span data-stu-id="06882-1247">**not_used_ptr** Pointer not used – should be NX_NULL.</span></span>
- <span data-ttu-id="06882-1248">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1248">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1249">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1249">Return Values</span></span>

- <span data-ttu-id="06882-1250">**NX_SUCCESS** (0x00) l'oggetto non trovato è stato compilato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1250">**NX_SUCCESS** (0x00) The not-found object has been successfully built.</span></span>
- <span data-ttu-id="06882-1251">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1251">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1252">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1252">Allowed From</span></span>

<span data-ttu-id="06882-1253">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1253">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1254">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1254">Example</span></span>

```c
/* Place not-found value in my_object.  */
status =  nx_snmp_object_not_found(NX_NULL, my_object);

/* If status is NX_SUCCESS, the my_object is now a not-found object. */
```

## <a name="nx_snmp_object_octet_string_get"></a><span data-ttu-id="06882-1255">nx_snmp_object_octet_string_get</span><span class="sxs-lookup"><span data-stu-id="06882-1255">nx_snmp_object_octet_string_get</span></span>
<span data-ttu-id="06882-1256">Ottenere un oggetto stringa ottetto</span><span class="sxs-lookup"><span data-stu-id="06882-1256">Get octet string object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1257">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1257">Prototype</span></span>

```c
UINT  nx_snmp_object_octet_string_get(VOID *source_ptr,
                                            NX_SNMP_OBJECT_DATA *object_data, 
                                      UINT length);
```
### <a name="description"></a><span data-ttu-id="06882-1258">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1258">Description</span></span>

<span data-ttu-id="06882-1259">Questo servizio recupera la stringa di ottetto in corrispondenza dell'indirizzo specificato dal puntatore di origine e la inserisce nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1259">This service retrieves the octet string at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="06882-1260">Questa routine viene in genere chiamata dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1260">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1261">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1261">Input Parameters</span></span>

- <span data-ttu-id="06882-1262">**source_ptr** Puntatore all'origine della stringa di ottetti.</span><span class="sxs-lookup"><span data-stu-id="06882-1262">**source_ptr** Pointer to octet string source.</span></span>
- <span data-ttu-id="06882-1263">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1263">**object_data** Pointer to destination object structure.</span></span>
- <span data-ttu-id="06882-1264">**lunghezza** Numero di byte nella stringa ottetto.</span><span class="sxs-lookup"><span data-stu-id="06882-1264">**length** Number of bytes in octet string.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1265">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1265">Return Values</span></span>

- <span data-ttu-id="06882-1266">**NX_SUCCESS** (0x00) l'oggetto stringa ottetto è stato recuperato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1266">**NX_SUCCESS** (0x00) The octet string object has been successfully retrieved.</span></span>
- <span data-ttu-id="06882-1267">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1267">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1268">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1268">Allowed From</span></span>

<span data-ttu-id="06882-1269">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1269">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1270">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1270">Example</span></span>

```c
/* Get the value of the 6-byte ifPhysAddress (1.3.6.1.2.1.2.2.1.6.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_octet_string_get(ifPhysAddress, my_object, 6);

/* If status is NX_SUCCESS, the my_object now contains the ifPhysAddress value. */
```

## <a name="nx_snmp_object_octet_string_set"></a><span data-ttu-id="06882-1271">nx_snmp_object_octet_string_set</span><span class="sxs-lookup"><span data-stu-id="06882-1271">nx_snmp_object_octet_string_set</span></span>
<span data-ttu-id="06882-1272">Imposta oggetto stringa ottetto</span><span class="sxs-lookup"><span data-stu-id="06882-1272">Set octet string object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1273">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1273">Prototype</span></span>

```c
UINT  nx_snmp_object_octet_string_set(VOID *destination_ptr, 
                                      NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1274">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1274">Description</span></span>

<span data-ttu-id="06882-1275">Questo servizio imposta la stringa di ottetto in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con la stringa di ottetto nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1275">This service sets the octet string at the address specified by the destination pointer with the octet string in the NetX object data structure.</span></span> <span data-ttu-id="06882-1276">Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.</span><span class="sxs-lookup"><span data-stu-id="06882-1276">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1277">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1277">Input Parameters</span></span>

- <span data-ttu-id="06882-1278">**destination_ptr** Puntatore alla destinazione della stringa ottetto.</span><span class="sxs-lookup"><span data-stu-id="06882-1278">**destination_ptr** Pointer to octet string destination.</span></span>
- <span data-ttu-id="06882-1279">**object_data** Puntatore alla struttura dell'oggetto di origine della stringa ottetto.</span><span class="sxs-lookup"><span data-stu-id="06882-1279">**object_data** Pointer to octet string source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1280">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1280">Return Values</span></span>

- <span data-ttu-id="06882-1281">**NX_SUCCESS** (0x00) l'oggetto stringa ottetto è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1281">**NX_SUCCESS** (0x00) The octet string object has been successfully set.</span></span>
- <span data-ttu-id="06882-1282">Il tipo di oggetto **NX_SNMP_ERROR_WRONGTYPE** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1282">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="06882-1283">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1283">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1284">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1284">Allowed From</span></span>

<span data-ttu-id="06882-1285">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1285">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1286">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1286">Example</span></span>

```c
/* Set the value of sysContact (1.3.6.1.2.1.1.4.0) from the 
   octet string in my_object.  */
status =  nx_snmp_object_octet_string_set(sysContact, my_object);

/* If status is NX_SUCCESS, sysContact now contains the new octet string. */
```

## <a name="nx_snmp_object_string_get"></a><span data-ttu-id="06882-1287">nx_snmp_object_string_get</span><span class="sxs-lookup"><span data-stu-id="06882-1287">nx_snmp_object_string_get</span></span>
<span data-ttu-id="06882-1288">Ottenere un oggetto stringa ASCII</span><span class="sxs-lookup"><span data-stu-id="06882-1288">Get ASCII string object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1289">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1289">Prototype</span></span>

```c
UINT  nx_snmp_object_string_get(VOID *source_ptr, 
                                NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1290">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1290">Description</span></span>

<span data-ttu-id="06882-1291">Questo servizio recupera la stringa ASCII in corrispondenza dell'indirizzo specificato dal puntatore di origine e la inserisce nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1291">This service retrieves the ASCII string at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="06882-1292">Questa routine viene in genere chiamata dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1292">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1293">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1293">Input Parameters</span></span>

- <span data-ttu-id="06882-1294">**source_ptr** Puntatore all'origine stringa ASCII.</span><span class="sxs-lookup"><span data-stu-id="06882-1294">**source_ptr** Pointer to ASCII string source.</span></span>
- <span data-ttu-id="06882-1295">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1295">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1296">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1296">Return Values</span></span>

- <span data-ttu-id="06882-1297">**NX_SUCCESS** (0x00) l'oggetto stringa ASCII è stato recuperato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1297">**NX_SUCCESS** (0x00) The ASCII string object has been successfully retrieved.</span></span>
- <span data-ttu-id="06882-1298">La stringa **NX_SNMP_ERROR** (0x100) è troppo grande</span><span class="sxs-lookup"><span data-stu-id="06882-1298">**NX_SNMP_ERROR** (0x100) String is too big</span></span>  
- <span data-ttu-id="06882-1299">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1299">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1300">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1300">Allowed From</span></span>

<span data-ttu-id="06882-1301">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1301">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1302">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1302">Example</span></span>

```c
/* Get the value of the sysDescr (1.3.6.1.2.1.1.1.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_string_get(sysDescr, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysDescr string. */
```

## <a name="nx_snmp_object_string_set"></a><span data-ttu-id="06882-1303">nx_snmp_object_string_set</span><span class="sxs-lookup"><span data-stu-id="06882-1303">nx_snmp_object_string_set</span></span>
<span data-ttu-id="06882-1304">Imposta oggetto stringa ASCII</span><span class="sxs-lookup"><span data-stu-id="06882-1304">Set ASCII string object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1305">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1305">Prototype</span></span>

```c
UINT  nx_snmp_object_string_set(VOID *destination_ptr, 
                                NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1306">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1306">Description</span></span>

<span data-ttu-id="06882-1307">Questo servizio imposta la stringa ASCII in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con la stringa ASCII nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1307">This service sets the ASCII string at the address specified by the destination pointer with the ASCII string in the NetX object data structure.</span></span> <span data-ttu-id="06882-1308">Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.</span><span class="sxs-lookup"><span data-stu-id="06882-1308">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1309">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1309">Input Parameters</span></span>

- <span data-ttu-id="06882-1310">**destination_ptr** Puntatore alla destinazione stringa ASCII.</span><span class="sxs-lookup"><span data-stu-id="06882-1310">**destination_ptr** Pointer to ASCII string destination.</span></span>
- <span data-ttu-id="06882-1311">**object_data** Puntatore alla struttura dell'oggetto di origine stringa ASCII.</span><span class="sxs-lookup"><span data-stu-id="06882-1311">**object_data** Pointer to ASCII string source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1312">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1312">Return Values</span></span>

- <span data-ttu-id="06882-1313">**NX_SUCCESS** (0x00) l'oggetto stringa ASCII è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1313">**NX_SUCCESS** (0x00) The ASCII string object has been successfully set.</span></span>
- <span data-ttu-id="06882-1314">La stringa **NX_SNMP_ERROR** (0x100) è troppo grande.</span><span class="sxs-lookup"><span data-stu-id="06882-1314">**NX_SNMP_ERROR** (0x100) String too large.</span></span>
- <span data-ttu-id="06882-1315">**NX_SNMP_ERROR_BADVALUE** (0x03) carattere non valido nella stringa</span><span class="sxs-lookup"><span data-stu-id="06882-1315">**NX_SNMP_ERROR_BADVALUE** (0x03) Invalid character in string</span></span>
- <span data-ttu-id="06882-1316">Il tipo di oggetto **NX_SNMP_ERROR_WRONGTYPE** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1316">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="06882-1317">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1317">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1318">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1318">Allowed From</span></span>

<span data-ttu-id="06882-1319">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1319">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1320">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1320">Example</span></span>

```c
/* Set the value of sysContact (1.3.6.1.2.1.1.4.0) from the 
   ASCII string in my_object.  */
status =  nx_snmp_object_string_set(sysContact, my_object);

/* If status is NX_SUCCESS, sysContact now contains the new ASCII string. */
```

## <a name="nx_snmp_object_timetics_get"></a><span data-ttu-id="06882-1321">nx_snmp_object_timetics_get</span><span class="sxs-lookup"><span data-stu-id="06882-1321">nx_snmp_object_timetics_get</span></span>
<span data-ttu-id="06882-1322">Ottenere l'oggetto timetics</span><span class="sxs-lookup"><span data-stu-id="06882-1322">Get timetics object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1323">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1323">Prototype</span></span>

```c
UINT  nx_snmp_object_timetics_get(VOID *source_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1324">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1324">Description</span></span>

<span data-ttu-id="06882-1325">Questo servizio recupera il timetics in corrispondenza dell'indirizzo specificato dal puntatore di origine e lo inserisce nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1325">This service retrieves the timetics at the address specified by the source pointer and places it in the NetX object data structure.</span></span> <span data-ttu-id="06882-1326">Questa routine viene in genere chiamata dalla routine di callback GET o GetNext Application.</span><span class="sxs-lookup"><span data-stu-id="06882-1326">This routine is typically called from the GET or GETNEXT application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1327">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1327">Input Parameters</span></span>

- <span data-ttu-id="06882-1328">**source_ptr** Puntatore all'origine timetics.</span><span class="sxs-lookup"><span data-stu-id="06882-1328">**source_ptr** Pointer to timetics source.</span></span>
- <span data-ttu-id="06882-1329">**object_data** Puntatore alla struttura dell'oggetto di destinazione.</span><span class="sxs-lookup"><span data-stu-id="06882-1329">**object_data** Pointer to destination object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1330">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1330">Return Values</span></span>

- <span data-ttu-id="06882-1331">**NX_SUCCESS** (0x00) l'oggetto timetics è stato recuperato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1331">**NX_SUCCESS** (0x00) The timetics object has been successfully retrieved.</span></span>
- <span data-ttu-id="06882-1332">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1332">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1333">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1333">Allowed From</span></span>

<span data-ttu-id="06882-1334">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1334">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1335">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1335">Example</span></span>

```c
/* Get the value of the sysUpTime (1.3.6.1.2.1.1.3.0) and place 
   it in my_object for return.  */
status =  nx_snmp_object_timetics_get(sysUpTime, my_object);

/* If status is NX_SUCCESS, the my_object now contains the sysUpTime value. */
```

## <a name="nx_snmp_object_timetics_set"></a><span data-ttu-id="06882-1336">nx_snmp_object_timetics_set</span><span class="sxs-lookup"><span data-stu-id="06882-1336">nx_snmp_object_timetics_set</span></span>
<span data-ttu-id="06882-1337">Imposta oggetto timetics</span><span class="sxs-lookup"><span data-stu-id="06882-1337">Set timetics object</span></span> 

### <a name="prototype"></a><span data-ttu-id="06882-1338">Prototipo</span><span class="sxs-lookup"><span data-stu-id="06882-1338">Prototype</span></span>

```c
UINT  nx_snmp_object_timetics_set(VOID *destination_ptr, 
                                  NX_SNMP_OBJECT_DATA *object_data);
```

### <a name="description"></a><span data-ttu-id="06882-1339">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06882-1339">Description</span></span>

<span data-ttu-id="06882-1340">Questo servizio imposta la variabile timetics in corrispondenza dell'indirizzo specificato dal puntatore di destinazione con timetics nella struttura dei dati dell'oggetto NetX.</span><span class="sxs-lookup"><span data-stu-id="06882-1340">This service sets the timetics variable at the address specified by the destination pointer with the timetics in the NetX object data structure.</span></span>
<span data-ttu-id="06882-1341">Questa routine viene in genere chiamata dalla routine di callback dell'applicazione SET.</span><span class="sxs-lookup"><span data-stu-id="06882-1341">This routine is typically called from the SET application callback routine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="06882-1342">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="06882-1342">Input Parameters</span></span>

- <span data-ttu-id="06882-1343">**destination_ptr** Puntatore alla destinazione timetics.</span><span class="sxs-lookup"><span data-stu-id="06882-1343">**destination_ptr** Pointer to timetics destination.</span></span>
- <span data-ttu-id="06882-1344">**object_data** Puntatore alla struttura dell'oggetto di origine timetics.</span><span class="sxs-lookup"><span data-stu-id="06882-1344">**object_data** Pointer to timetics source object structure.</span></span>

### <a name="return-values"></a><span data-ttu-id="06882-1345">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="06882-1345">Return Values</span></span>

- <span data-ttu-id="06882-1346">**NX_SUCCESS** (0x00) l'oggetto timetics è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06882-1346">**NX_SUCCESS** (0x00) The timetics object has been successfully set.</span></span>
- <span data-ttu-id="06882-1347">Il tipo di oggetto **NX_SNMP_ERROR_WRONGTYPE** (0x07) non è valido.</span><span class="sxs-lookup"><span data-stu-id="06882-1347">**NX_SNMP_ERROR_WRONGTYPE** (0x07) Invalid object type.</span></span>
- <span data-ttu-id="06882-1348">Puntatore di input **NX_PTR_ERROR** (0x07) non valido</span><span class="sxs-lookup"><span data-stu-id="06882-1348">**NX_PTR_ERROR** (0x07) Invalid input pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="06882-1349">Consentito da</span><span class="sxs-lookup"><span data-stu-id="06882-1349">Allowed From</span></span>

<span data-ttu-id="06882-1350">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="06882-1350">Initialization, Threads</span></span>

### <a name="example"></a><span data-ttu-id="06882-1351">Esempio</span><span class="sxs-lookup"><span data-stu-id="06882-1351">Example</span></span>

```c
/* Set the value of “my_time” from the timetics value in my_object.  */
status =  nx_snmp_object_timetics_set(&my_time, my_object);

/* If status is NX_SUCCESS, my_time now contains the new timetics. */
```