---
title: Capitolo 4-servizi client di Azure RTO NetX Duo DHCPv6
description: Questo capitolo contiene una descrizione di tutti i servizi client di Azure RTO NetX Duo DHCPv6 (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 40fbfa7319ca95af65c92b12582d4bbb05005dc0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821977"
---
# <a name="chapter-4---azure-rtos-netx-duo-dhcpv6-client-services"></a><span data-ttu-id="5ab65-103">Capitolo 4-servizi client di Azure RTO NetX Duo DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-103">Chapter 4 - Azure RTOS NetX Duo DHCPv6 Client services</span></span>

<span data-ttu-id="5ab65-104">Questo capitolo contiene una descrizione di tutti i servizi client di Azure RTO NetX Duo DHCPv6 (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="5ab65-104">This chapter contains a description of all Azure RTOS NetX Duo DHCPv6 Client services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="5ab65-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="5ab65-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="5ab65-106">**nx_dhcpv6_client_create:** *creare un'istanza del client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-106">**nx_dhcpv6_client_create:** *Create a DHCPv6 Client instance*</span></span> 

- <span data-ttu-id="5ab65-107">**nx_dhcpv6_client_delete:** *eliminare un'istanza del client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-107">**nx_dhcpv6_client_delete:** *Delete a DHCPv6 Client instance*</span></span> 

- <span data-ttu-id="5ab65-108">**nx_dhcpv6_create_ client_duid:** *creare un client DHCPv6 Duid*</span><span class="sxs-lookup"><span data-stu-id="5ab65-108">**nx_dhcpv6_create_ client_duid:** *Create a DHCPv6 Client DUID*</span></span> 

- <span data-ttu-id="5ab65-109">**nx_dhcpv6 _add_client_ia:** *aggiungere un indirizzo di identità del client DHCPv6 (IA)*</span><span class="sxs-lookup"><span data-stu-id="5ab65-109">**nx_dhcpv6 _add_client_ia:** *Add a DHCPv6 Client Identity Address (IA)*</span></span> 

- <span data-ttu-id="5ab65-110">**nx_dhcpv6 _create_client_ia:** (*legacy aggiungere un indirizzo di identità client DHCPv6 (IA))*</span><span class="sxs-lookup"><span data-stu-id="5ab65-110">**nx_dhcpv6 _create_client_ia:** (*Legacy Add a DHCPv6 Client Identity Address (IA))*</span></span> 

- <span data-ttu-id="5ab65-111">**nx_dhcpv6_create_client_iana:** *creare un'associazione di identità client Dhcpv6 per indirizzi non temporanei (IANA)*</span><span class="sxs-lookup"><span data-stu-id="5ab65-111">**nx_dhcpv6_create_client_iana:** *Create a DHCPv6 Client Identity Association for Non Temporary Addresses (IANA)*</span></span> 

- <span data-ttu-id="5ab65-112">**nx_dhcpv6_get_client_duid_time_id:** *ottenere l'ID ora dal client DHCPv6 Duid*</span><span class="sxs-lookup"><span data-stu-id="5ab65-112">**nx_dhcpv6_get_client_duid_time_id:** *Get the time ID from DHCPv6 Client DUID*</span></span> 

- <span data-ttu-id="5ab65-113">**nx_dhcpv6_client_set_interface:** *impostare l'interfaccia di rete client per le comunicazioni con il server DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-113">**nx_dhcpv6_client_set_interface:** *Set the Client network interface for communications with the DHCPv6 Server*</span></span> 

- <span data-ttu-id="5ab65-114">**nx_dhcpv6_get_IP_address:** *ottenere l'indirizzo IPv6 globale assegnato al client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-114">**nx_dhcpv6_get_IP_address:** *Get the global IPv6 address assigned to the DHCPv6 client*</span></span> 

- <span data-ttu-id="5ab65-115">**nx_dhcpv6_get_lease_time_data:** *ottiene T1, T2, durata valida e preferita per l'indirizzo IPv6 globale del client*</span><span class="sxs-lookup"><span data-stu-id="5ab65-115">**nx_dhcpv6_get_lease_time_data:** *Get T1, T2, valid and preferred lifetimes for the Client global IPv6 address*</span></span>

- <span data-ttu-id="5ab65-116">**nx_dhcpv6_get_valid_ip_address_lease_time:** *ottiene T1, T2, durate e le durate preferite per l'indirizzo IPv6 del client DHCPv6 in base all'indice dell'indirizzo*</span><span class="sxs-lookup"><span data-stu-id="5ab65-116">**nx_dhcpv6_get_valid_ip_address_lease_time:** *Get T1, T2, valid and preferred lifetimes for the DHCPv6 Client IPv6 address by address index*</span></span> 

- <span data-ttu-id="5ab65-117">**nx_dhcpv6_get_iana_lease_time:** *ottenere T1 e T2 nell'associazione di identità (IANA) con lease per il client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-117">**nx_dhcpv6_get_iana_lease_time:** *Get T1 and T2 in the Identity Association (IANA) leased to the DHCPv6 Client*</span></span> 

- <span data-ttu-id="5ab65-118">**nx_dhcpv6_get_other_option_data:** *ottenere i dati delle opzioni specificati, ad esempio il nome di dominio o il server del fuso orario*</span><span class="sxs-lookup"><span data-stu-id="5ab65-118">**nx_dhcpv6_get_other_option_data:** *Get the specified option data e.g. domain name or time zone server*</span></span> 

- <span data-ttu-id="5ab65-119">**nx_dhcpv6_get_DNS_server_address:** *ottenere l'indirizzo del server DNS in corrispondenza dell'indice specificato nell'elenco dei server DNS del client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-119">**nx_dhcpv6_get_DNS_server_address:** *Get DNS Server address at the specified index into the DHCPv6 Client DNS server list*</span></span> 

- <span data-ttu-id="5ab65-120">**nx_dhcpv6_get_time_accrued:** *ottenere l'ora in cui il lease dell'indirizzo IPv6 globale è stato associato al client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-120">**nx_dhcpv6_get_time_accrued:** *Get the time accrued the global IPv6 address lease has been bound to the DHCPv6 Client*</span></span> 

- <span data-ttu-id="5ab65-121">**nx_dhcpv6_get_time_server_address:** *ottenere l'indirizzo del server in corrispondenza dell'indice specificato nell'elenco dei server di tempo client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-121">**nx_dhcpv6_get_time_server_address:** *Get Time Server address at the specified index into the DHCPv6 Client Time server list*</span></span>

- <span data-ttu-id="5ab65-122">**nx_dhcpv6_get_valid_ip_address_count:** *ottenere il numero di indirizzi IPv6 assegnati al client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-122">**nx_dhcpv6_get_valid_ip_address_count:** *Get the number of IPv6 addresses assigned to the DHCPv6 Client*</span></span> 

- <span data-ttu-id="5ab65-123">**nx_dhcpv6_reinitialize:** *reinizializzare DHCPv6 per riavviare la macchina a Stati del client DHCPv6 e rieseguire il protocollo DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-123">**nx_dhcpv6_reinitialize:** *Reinitialize the DHCPv6 for restarting the DHCPv6 Client state machine and rerunning the DHCPv6 protocol*</span></span> 

- <span data-ttu-id="5ab65-124">**nx_dhcpv6_request_confirm:** *inviare una richiesta di conferma al server*</span><span class="sxs-lookup"><span data-stu-id="5ab65-124">**nx_dhcpv6_request_confirm:** *Send a CONFIRM request to the Server*</span></span> 

- <span data-ttu-id="5ab65-125">**nx_dhcpv6_request_inform_request:** *Termina un messaggio di richiesta di notifica al server*</span><span class="sxs-lookup"><span data-stu-id="5ab65-125">**nx_dhcpv6_request_inform_request:** S *end an INFORM REQUEST message to the Server*</span></span> 

- <span data-ttu-id="5ab65-126">**nx_dhcpv6_request_release:** *inviare una richiesta di rilascio al server*</span><span class="sxs-lookup"><span data-stu-id="5ab65-126">**nx_dhcpv6_request_release:** *Send a RELEASE request to the Server*</span></span> 

- <span data-ttu-id="5ab65-127">**nx_dhcpv6_request_option_DNS_server:** *aggiungere l'opzione del server DNS all'opzione client Richiedi i dati nei messaggi di richiesta al server*</span><span class="sxs-lookup"><span data-stu-id="5ab65-127">**nx_dhcpv6_request_option_DNS_server:** *Add the DNS server option to the Client option request data in request messages to the Server*</span></span> 

- <span data-ttu-id="5ab65-128">**nx_dhcpv6_request_option_FQDN:** *aggiungere l'opzione FQDN all'opzione client Richiedi i dati nei messaggi di richiesta al server*</span><span class="sxs-lookup"><span data-stu-id="5ab65-128">**nx_dhcpv6_request_option_FQDN:** *Add the FQDN option to the Client option request data in request messages to the Server*</span></span> 

- <span data-ttu-id="5ab65-129">**nx_dhcpv6_request_option_domain_name:** *aggiungere l'opzione nome dominio all'opzione client Richiedi i dati nei messaggi di richiesta al server*</span><span class="sxs-lookup"><span data-stu-id="5ab65-129">**nx_dhcpv6_request_option_domain_name:** *Add the domain name option to the Client option request data in request messages to the Server*</span></span> 

- <span data-ttu-id="5ab65-130">**nx_dhcpv6_request_option_time_server:** *aggiungere l'opzione Time Server all'opzione client Richiedi i dati nei messaggi di richiesta al server*</span><span class="sxs-lookup"><span data-stu-id="5ab65-130">**nx_dhcpv6_request_option_time_server:** *Add the time server option to the Client option request data in request messages to the Server*</span></span> 

- <span data-ttu-id="5ab65-131">**nx_dhcpv6_request_option_timezone:** *aggiungere l'opzione fuso orario all'opzione client Richiedi i dati nei messaggi di richiesta al server*</span><span class="sxs-lookup"><span data-stu-id="5ab65-131">**nx_dhcpv6_request_option_timezone:** *Add the time zone option to the Client option request data in request messages to the Server*</span></span> 

- <span data-ttu-id="5ab65-132">**nx_dhcpv6_request_solicit:** *inviare una richiesta di sollecitazione Dhcpv6 a qualsiasi server nella rete client (broadcast)*</span><span class="sxs-lookup"><span data-stu-id="5ab65-132">**nx_dhcpv6_request_solicit:** *Send a DHCPv6 SOLICIT request to any Server on the Client network (broadcast)*</span></span> 

- <span data-ttu-id="5ab65-133">**nx_dhcpv6_request_solicit_rapid:** *inviare una richiesta di sollecitazione Dhcpv6 a qualsiasi server nella rete client (broadcast) con il set di opzioni di commit rapido*</span><span class="sxs-lookup"><span data-stu-id="5ab65-133">**nx_dhcpv6_request_solicit_rapid:** *Send a DHCPv6 SOLICIT request to any Server on the Client network (broadcast) with the Rapid Commit option set*</span></span> 

- <span data-ttu-id="5ab65-134">**nx_dhcpv6_resume:** *riprendere l'elaborazione del client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-134">**nx_dhcpv6_resume:** *Resume DHCPv6 Client processing*</span></span> 

- <span data-ttu-id="5ab65-135">**nx_dhcpv6_start:** *avviare l'attività thread del client DHCPv6. Si noti che questo non è equivalente all'avvio della macchina a stati DHCPv6 e non invia una richiesta di SOLLECITAzione*</span><span class="sxs-lookup"><span data-stu-id="5ab65-135">**nx_dhcpv6_start:** *Start the DHCPv6 Client thread task. Note this is not equivalent to starting the DHCPv6 state machine and does not send a SOLICIT request*</span></span> 

- <span data-ttu-id="5ab65-136">**nx_dhcpv6_stop:** *arrestare l'attività thread del client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-136">**nx_dhcpv6_stop:** *Stop the DHCPv6 Client thread task*</span></span> 

- <span data-ttu-id="5ab65-137">**nx_dhcpv6_suspend:** *sospendere l'attività thread client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="5ab65-137">**nx_dhcpv6_suspend:** *Suspend the DHCPv6 Client thread task*</span></span> 

- <span data-ttu-id="5ab65-138">**nx_dhcpv6_set_time_accrued:** *impostare l'ora accumulata sul lease di indirizzi IPv6 del client globale nel record client.*</span><span class="sxs-lookup"><span data-stu-id="5ab65-138">**nx_dhcpv6_set_time_accrued:** *Set the time accrued on the global Client IPv6 address lease in the Client record.*</span></span>

## <a name="nx_dhcpv6_client_create"></a><span data-ttu-id="5ab65-139">nx_dhcpv6_client_create</span><span class="sxs-lookup"><span data-stu-id="5ab65-139">nx_dhcpv6_client_create</span></span>

<span data-ttu-id="5ab65-140">Creare un'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-140">Create a DHCPv6 client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-141">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-141">Prototype</span></span>

```C
UINT  nx_dhcpv6_client_create(NX_DHCPV6 *dhcpv6_ptr, 
                        NX_IP *ip_ptr, CHAR *name_ptr, 
                        NX_PACKET_POOL *packet_pool_ptr, 
                        VOID *stack_ptr, ULONG stack_size,
                        VOID (*dhcpv6_state_change_notify)
                                 (struct NX_DHCPV6_STRUCT *dhcpv6_ptr, 
                                  UINT old_state, UINT new_state), 
                        VOID (*dhcpv6_server_error_handler)
                                 (struct NX_DHCPV6_STRUCT *dhcpv6_ptr, 
                                 UINT op_code, UINT status_code, 
                                 UINT message_type));
```

### <a name="description"></a><span data-ttu-id="5ab65-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-142">Description</span></span>

<span data-ttu-id="5ab65-143">Questo servizio crea un'istanza del client DHCPv6, incluse le funzioni di callback.</span><span class="sxs-lookup"><span data-stu-id="5ab65-143">This service creates a DHCPv6 client instance including callback functions.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-144">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-144">Input Parameters</span></span>

- <span data-ttu-id="5ab65-145">**dhcpv6_ptr** Puntatore al blocco di controllo DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-145">**dhcpv6_ptr** Pointer to DHCPv6 control block</span></span>  

- <span data-ttu-id="5ab65-146">**ip_ptr** Puntatore a istanza IP client</span><span class="sxs-lookup"><span data-stu-id="5ab65-146">**ip_ptr** Pointer to Client IP instance</span></span>  

- <span data-ttu-id="5ab65-147">**name_ptr** Puntatore al nome per l'istanza di DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-147">**name_ptr** Pointer to name for DHCPv6 instance</span></span>

- <span data-ttu-id="5ab65-148">**packet_pool_ptr** Puntatore al pool di pacchetti client</span><span class="sxs-lookup"><span data-stu-id="5ab65-148">**packet_pool_ptr** Pointer to Client packet pool</span></span>

- <span data-ttu-id="5ab65-149">**stack_ptr** Puntatore alla memoria dello stack client</span><span class="sxs-lookup"><span data-stu-id="5ab65-149">**stack_ptr** Pointer to Client stack memory</span></span>

- <span data-ttu-id="5ab65-150">**stack_size** Dimensioni della memoria dello stack client</span><span class="sxs-lookup"><span data-stu-id="5ab65-150">**stack_size** Size of Client stack memory</span></span>

- <span data-ttu-id="5ab65-151">**dhcpv6_state_change_notify** Puntatore alla funzione di callback richiamata quando il client avvia una nuova richiesta DHCPv6 al server</span><span class="sxs-lookup"><span data-stu-id="5ab65-151">**dhcpv6_state_change_notify** Pointer to callback function invoked when the Client initiates a new DHCPv6 request to the server</span></span>

- <span data-ttu-id="5ab65-152">**dhcpv6_server_error_handler** Puntatore alla funzione di callback richiamata quando il client riceve uno stato di errore dal server</span><span class="sxs-lookup"><span data-stu-id="5ab65-152">**dhcpv6_server_error_handler** Pointer to callback function invoked when the Client receives an error status from the server</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-153">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-153">Return Values</span></span>

- <span data-ttu-id="5ab65-154">Creazione client riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="5ab65-154">**NX_SUCCESS** (0x00) Successful Client create</span></span>

- <span data-ttu-id="5ab65-155">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-155">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-156">NX_DHCPV6_PARAM_ERROR (0xE93) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-156">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-157">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-157">Allowed From</span></span>

<span data-ttu-id="5ab65-158">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-158">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-159">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-159">Example</span></span>

```C
/* Create a DHCPv6 client instance without specifying link local or preferred
   global IP address.  */
status =  nx_dhcpv6_client_create(&dhcp_0, &ip_0, "DHCPv6 Client", &pool_0,
                                  NULL, NULL, pointer, 2048,        
                                  dhcpv6_state_change_notify, 
                                  dhcpv6_server_error_handler);

/* If status is NX_SUCCESS a DHCPv6 client instance was successfully
   created.  */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-160">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-160">See Also</span></span>

- <span data-ttu-id="5ab65-161">nx_dhcpv6_client_delete</span><span class="sxs-lookup"><span data-stu-id="5ab65-161">nx_dhcpv6_client_delete</span></span>

## <a name="nx_dhcpv6_client_delete"></a><span data-ttu-id="5ab65-162">nx_dhcpv6_client_delete</span><span class="sxs-lookup"><span data-stu-id="5ab65-162">nx_dhcpv6_client_delete</span></span>

<span data-ttu-id="5ab65-163">Eliminare un'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-163">Delete a DHCPv6 Client instance</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-164">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-164">Prototype</span></span>

```C
UINT nx_dhcpv6_client_delete(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-165">Description</span></span>

<span data-ttu-id="5ab65-166">Questo servizio Elimina un'istanza del client DHCPv6 creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5ab65-166">This service deletes a previously created DHCPv6 client instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-167">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-167">Input Parameters</span></span>

- <span data-ttu-id="5ab65-168">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-168">**dhcpv6_ptr** Pointer to DHCPv6 client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-169">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-169">Return Values</span></span>

- <span data-ttu-id="5ab65-170">Eliminazione di DHCPv6 riuscita **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="5ab65-170">**NX_SUCCESS** (0x00) Successful DHCPv6 deletion</span></span>

- <span data-ttu-id="5ab65-171">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-171">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-172">NX_DHCPV6_PARAM_ERROR (0xE93) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-172">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-173">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-173">Allowed From</span></span>

<span data-ttu-id="5ab65-174">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-174">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-175">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-175">Example</span></span>

```C
/* Delete a DHCPv6 client instance.  */
status =  nx_dhcpv6_client_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCPv6 client instance was successfully
   deleted.  */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-176">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-176">See Also</span></span>

- <span data-ttu-id="5ab65-177">nx_dhcpv6_client_create</span><span class="sxs-lookup"><span data-stu-id="5ab65-177">nx_dhcpv6_client_create</span></span>

## <a name="nx_dhcpv6_client_set_interface"></a><span data-ttu-id="5ab65-178">nx_dhcpv6_client_set_interface</span><span class="sxs-lookup"><span data-stu-id="5ab65-178">nx_dhcpv6_client_set_interface</span></span>

<span data-ttu-id="5ab65-179">Imposta l'interfaccia di rete del client per DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-179">Sets Client’s Network Interface for DHCPv6</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-180">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-180">Prototype</span></span>

```C
UINT    nx_dhcpv6_client_set_interface(NX_DHCPV6 *dhcpv6_ptr, 
                                       UINT *interface_index);
```

### <a name="description"></a><span data-ttu-id="5ab65-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-181">Description</span></span>

<span data-ttu-id="5ab65-182">Questo servizio imposta l'interfaccia di rete del client per la comunicazione con i server DHCPv6 all'indice dell'interfaccia di input specificato.</span><span class="sxs-lookup"><span data-stu-id="5ab65-182">This service sets the Client’s network interface for communicating with the DHCPv6 Server(s) to the specified input interface index.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-183">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-183">Input Parameters</span></span>

- <span data-ttu-id="5ab65-184">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-184">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-185">**interface_index** Indice che indica l'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="5ab65-185">**interface_index** Index indicating network interface</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-186">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-186">Return Values</span></span>

- <span data-ttu-id="5ab65-187">Interfaccia **NX_SUCCESS** (0x00) impostata correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-187">**NX_SUCCESS** (0x00) Interface successfully set</span></span>

- <span data-ttu-id="5ab65-188">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-188">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-189">Input di indice dell'interfaccia NX_INVALID_INTERFACE (0x4C) non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-189">NX_INVALID_INTERFACE (0x4C) Invalid interface index input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-190">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-190">Allowed From</span></span>

<span data-ttu-id="5ab65-191">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-192">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-192">Example</span></span>

```C
/* Set the client interface for DHCPv6 communication with the Server to 
   the secondary interface (1). */

UINT index = 1;
status = nx_dhcpv6_client_set_interface(&dhcp_0, index);

/* If status is NX_SUCCESS, the Client successfully set 
   the DHCPv6 network interface.  */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-193">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-193">See Also</span></span>

- <span data-ttu-id="5ab65-194">nx_dhcpv6_client _create</span><span class="sxs-lookup"><span data-stu-id="5ab65-194">nx_dhcpv6_client _create</span></span>
- <span data-ttu-id="5ab65-195">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="5ab65-195">nx_dhcpv6_start</span></span>

## <a name="nx_dhcpv6_client_set_destination_address"></a><span data-ttu-id="5ab65-196">nx_dhcpv6_client_set_destination_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-196">nx_dhcpv6_client_set_destination_address</span></span>

<span data-ttu-id="5ab65-197">Imposta l'indirizzo di destinazione a cui deve essere inviato il messaggio DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-197">Sets the destination address where DHCPv6 message should be sent to</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-198">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-198">Prototype</span></span>

```C
UINT nx_dhcpv6_client_set_destination_address(NX_DHCPV6 *dhcpv6_ptr,
                                              NXD_ADDRESS *destination_address);
```

### <a name="description"></a><span data-ttu-id="5ab65-199">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-199">Description</span></span>

<span data-ttu-id="5ab65-200">Questo servizio imposta l'indirizzo di destinazione a cui deve essere inviato il messaggio DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-200">This service sets the destination address where DHCPv6 message should be sent to.</span></span> <span data-ttu-id="5ab65-201">Per impostazione predefinita, è ALL_DHCP_Relay_Agents_and_Servers (FF02:: 1:2).</span><span class="sxs-lookup"><span data-stu-id="5ab65-201">By default is ALL_DHCP_Relay_Agents_and_Servers(FF02::1:2).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-202">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-202">Input Parameters</span></span>

- <span data-ttu-id="5ab65-203">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-203">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-204">**destination_address** Indirizzo di destinazione</span><span class="sxs-lookup"><span data-stu-id="5ab65-204">**destination_address** Destination address</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-205">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-205">Return Values</span></span>

- <span data-ttu-id="5ab65-206">Interfaccia **NX_SUCCESS** (0x00) impostata correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-206">**NX_SUCCESS** (0x00) Interface successfully set</span></span>

- <span data-ttu-id="5ab65-207">NX_PTR_ERROR (0x07) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-207">NX_PTR_ERROR (0x07) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-208">Errore di parazione NX_DHCPV6_PARAM_ERROR (0xE93)</span><span class="sxs-lookup"><span data-stu-id="5ab65-208">NX_DHCPV6_PARAM_ERROR (0xE93) Parament error</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-209">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-209">Allowed From</span></span>

<span data-ttu-id="5ab65-210">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-210">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-211">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-211">Example</span></span>

```C
/* Set the destination address where DHCPv6 message should be sent to. */

NXD_ADDRESS dest_address; /* Set the destination address.  */

status = nx_dhcpv6_client_set_destination_address(&dhcp_0, &dest_address);

/* If status is NX_SUCCESS, the Client successfully set the destination address. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-212">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-212">See Also</span></span>

- <span data-ttu-id="5ab65-213">nx_dhcpv6_client _create</span><span class="sxs-lookup"><span data-stu-id="5ab65-213">nx_dhcpv6_client _create</span></span>
- <span data-ttu-id="5ab65-214">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="5ab65-214">nx_dhcpv6_start</span></span>

## <a name="nx_dhcpv6_create_client_duid"></a><span data-ttu-id="5ab65-215">nx_dhcpv6_create_client_duid</span><span class="sxs-lookup"><span data-stu-id="5ab65-215">nx_dhcpv6_create_client_duid</span></span>

<span data-ttu-id="5ab65-216">Crea oggetto DUID client</span><span class="sxs-lookup"><span data-stu-id="5ab65-216">Create Client DUID object</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-217">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-217">Prototype</span></span>

```C
UINT nx_dhcpv6_create_client_duid(NX_DHCPV6 *dhcpv6_ptr,
                                  UINT duid_type, UINT hardware_type,
                                  ULONG time);
```

### <a name="description"></a><span data-ttu-id="5ab65-218">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-218">Description</span></span>

<span data-ttu-id="5ab65-219">Questo servizio crea il client DUID con i parametri di input.</span><span class="sxs-lookup"><span data-stu-id="5ab65-219">This service creates the Client DUID with the input parameters.</span></span> <span data-ttu-id="5ab65-220">Se l'input dell'ora non viene specificato e il tipo Duid indica il livello di collegamento con il tempo, questa funzione fornirà un'ora che include un fattore casuale per l'univocità.</span><span class="sxs-lookup"><span data-stu-id="5ab65-220">If the time input is not supplied and the duid type indicates link layer with time, this function will supply a time which includes a randomizing factor for uniqueness.</span></span> <span data-ttu-id="5ab65-221">I tipi Duid assegnati al fornitore (Enterprise) non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="5ab65-221">Vendor assigned (enterprise) duid types are not supported.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-222">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-222">Input Parameters</span></span>

- <span data-ttu-id="5ab65-223">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-223">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-224">**duid_type** Tipo di DUID (hardware, Enterprise e così via)</span><span class="sxs-lookup"><span data-stu-id="5ab65-224">**duid_type** Type of DUID (hardware, enterprise etc)</span></span>

- <span data-ttu-id="5ab65-225">**hardware_type** Hardware di rete, ad esempio IEEE 802</span><span class="sxs-lookup"><span data-stu-id="5ab65-225">**hardware_type** Network hardware e.g. IEEE 802</span></span>

- <span data-ttu-id="5ab65-226">**ora** di Valore utilizzato per la creazione di un identificatore univoco</span><span class="sxs-lookup"><span data-stu-id="5ab65-226">**time** Value used in creating unique identifier</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-227">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-227">Return Values</span></span>

- <span data-ttu-id="5ab65-228">**NX_SUCCESS** (0x00) client Duid riusciti creati</span><span class="sxs-lookup"><span data-stu-id="5ab65-228">**NX_SUCCESS** (0x00) Successful Client DUID created</span></span>

- <span data-ttu-id="5ab65-229">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-229">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-230">NX_DHCPV6_PARAM_ERROR (0xE93) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-230">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

- <span data-ttu-id="5ab65-231">NX_DHCPV6_UNSUPPORTED_DUID_TYPE (0xE98) DUID tipo sconosciuto o non supportato</span><span class="sxs-lookup"><span data-stu-id="5ab65-231">NX_DHCPV6_UNSUPPORTED_DUID_TYPE (0xE98) DUID type unknown or not supported</span></span> 

- <span data-ttu-id="5ab65-232">NX_DHCPV6_UNSUPPORTED_DUID_HW_TYPE (0xE99) DUID tipo di hardware sconosciuto o non supportato</span><span class="sxs-lookup"><span data-stu-id="5ab65-232">NX_DHCPV6_UNSUPPORTED_DUID_HW_TYPE (0xE99) DUID hardware type unknown or not supported</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-233">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-233">Allowed From</span></span>

<span data-ttu-id="5ab65-234">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-234">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-235">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-235">Example</span></span>

```C
/* Create the Client DUID from the supplied input.
   The time field is left NULL so the DHCPv6 client will provide one.  */
status = nx_dhcpv6_create_client_duid(&dhcp_0, NX_DHCPV6_DUID_TYPE_LINK_TIME,
                                      NX_DHCPV6_HW_TYPE_IEEE_802, 0)

/* If status is NX_SUCCESS the client DUID was successfully created.  */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-236">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-236">See Also</span></span>

- <span data-ttu-id="5ab65-237">nx_dhcpv6_create_client_ia</span><span class="sxs-lookup"><span data-stu-id="5ab65-237">nx_dhcpv6_create_client_ia</span></span>
- <span data-ttu-id="5ab65-238">nx_dhcpv6_create_client_iana</span><span class="sxs-lookup"><span data-stu-id="5ab65-238">nx_dhcpv6_create_client_iana</span></span>
- <span data-ttu-id="5ab65-239">nx_dhcpv6_create_server_duid</span><span class="sxs-lookup"><span data-stu-id="5ab65-239">nx_dhcpv6_create_server_duid</span></span>

## <a name="nx_dhcpv6_create_client_ia"></a><span data-ttu-id="5ab65-240">nx_dhcpv6_create_client_ia</span><span class="sxs-lookup"><span data-stu-id="5ab65-240">nx_dhcpv6_create_client_ia</span></span>

<span data-ttu-id="5ab65-241">Aggiungere un'associazione di identità al client</span><span class="sxs-lookup"><span data-stu-id="5ab65-241">Add an Identity Association to the Client</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-242">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-242">Prototype</span></span>

```C
UINT nx_dhcpv6_create_client_ia(NX_DHCPV6 *dhcpv6_ptr,
                                NXD_ADDRESS *ipv6_address,
                                ULONG preferred_lifetime,
                                ULONG valid_lifetime);
```

### <a name="description"></a><span data-ttu-id="5ab65-243">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-243">Description</span></span>

<span data-ttu-id="5ab65-244">Questo servizio è identico a quello del servizio *nx_dhcpv6_add_client_ia* .</span><span class="sxs-lookup"><span data-stu-id="5ab65-244">This service is identical to the *nx_dhcpv6_add_client_ia* service.</span></span> <span data-ttu-id="5ab65-245">Viene aggiunta un'associazione di identità client compilando il record client con i parametri forniti.</span><span class="sxs-lookup"><span data-stu-id="5ab65-245">It adds a Client Identity Association by filling in the Client record with the supplied parameters.</span></span> <span data-ttu-id="5ab65-246">Per richiedere le durate massime preferite e valide, impostare questi parametri su infinito.</span><span class="sxs-lookup"><span data-stu-id="5ab65-246">To request the maximum preferred and valid lifetimes, set these parameters to infinity.</span></span> <span data-ttu-id="5ab65-247">Per aggiungere più di un IA a un client DHCPv6, impostare il NX_DHCPV6_MAX_IA_ADDRESS su un valore superiore al valore predefinito 1.</span><span class="sxs-lookup"><span data-stu-id="5ab65-247">To add more than one IA to a DHCPv6 Client, set the NX_DHCPV6_MAX_IA_ADDRESS to a value higher than the default value of 1.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-248">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-248">Input Parameters</span></span>

- <span data-ttu-id="5ab65-249">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-249">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-250">**Ipv6_address** Puntatore al blocco di indirizzi IP di NetX Duo</span><span class="sxs-lookup"><span data-stu-id="5ab65-250">**ipv6_address** Pointer to NetX Duo IP address block</span></span>

- <span data-ttu-id="5ab65-251">**preferred_lifetime** Intervallo di tempo prima che l'indirizzo IP sia deprecato</span><span class="sxs-lookup"><span data-stu-id="5ab65-251">**preferred_lifetime** Length of time before IP address is deprecated</span></span>

- <span data-ttu-id="5ab65-252">**valid_lifetime** Periodo di tempo prima della scadenza dell'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="5ab65-252">**valid_lifetime** Length of time before IP address is expired</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-253">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-253">Return Values</span></span>

- <span data-ttu-id="5ab65-254">**NX_SUCCESS** (0x00) client con esito positivo aggiunto</span><span class="sxs-lookup"><span data-stu-id="5ab65-254">**NX_SUCCESS** (0x00) Successful Client IA added</span></span>

- <span data-ttu-id="5ab65-255">Indirizzo IA duplicato **NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xEAF)</span><span class="sxs-lookup"><span data-stu-id="5ab65-255">**NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xEAF) Duplicate IA address</span></span> 

- <span data-ttu-id="5ab65-256">**NX_DHCPV6_REACHED_MAX_IA_ADDRESS** (0XEAE) Ia supera il numero massimo di client IAS che è in grado di archiviare</span><span class="sxs-lookup"><span data-stu-id="5ab65-256">**NX_DHCPV6_REACHED_MAX_IA_ADDRESS** (0xEAE) IA exceeds the max IAs Client can store</span></span>

- <span data-ttu-id="5ab65-257">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-257">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-258">NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) non valido (ad esempio, null) indirizzo IA in IA</span><span class="sxs-lookup"><span data-stu-id="5ab65-258">NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) Invalid (e.g. null) IA address in IA</span></span>

- <span data-ttu-id="5ab65-259">NX_DHCPV6_PARAM_ERROR (0xE93) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-259">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>


### <a name="allowed-from"></a><span data-ttu-id="5ab65-260">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-260">Allowed From</span></span>

<span data-ttu-id="5ab65-261">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-261">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-262">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-262">Example</span></span>

```C
/* Add an Client IA using the supplied input.   */
status = nx_dhcpv6_create_client_ia(&dhcp_0, &ipv6_address, 
NX_DHCPV6_PREFERRED_LIFETIME, NX_DHCPV6_VALID_LIFETIME);

/* If status is NX_SUCCESS the client IA was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-263">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-263">See Also</span></span>

- <span data-ttu-id="5ab65-264">nx_dhcpv6_add_client_duid</span><span class="sxs-lookup"><span data-stu-id="5ab65-264">nx_dhcpv6_add_client_duid</span></span>
- <span data-ttu-id="5ab65-265">nx_dhcpv6_create_server_duid</span><span class="sxs-lookup"><span data-stu-id="5ab65-265">nx_dhcpv6_create_server_duid</span></span>
- <span data-ttu-id="5ab65-266">nx_dhcpv6_create_client_iana</span><span class="sxs-lookup"><span data-stu-id="5ab65-266">nx_dhcpv6_create_client_iana</span></span>

## <a name="nx_dhcpv6_create_client_iana"></a><span data-ttu-id="5ab65-267">nx_dhcpv6_create_client_iana</span><span class="sxs-lookup"><span data-stu-id="5ab65-267">nx_dhcpv6_create_client_iana</span></span>

<span data-ttu-id="5ab65-268">Creare un'associazione di identità (non temporanea) per il client</span><span class="sxs-lookup"><span data-stu-id="5ab65-268">Create an Identity Association (Non Temporary) for the Client</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-269">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-269">Prototype</span></span>

```C
UINT nx_dhcpv6_create_client_iana(NX_DHCPV6 *dhcpv6_ptr, 
                                  UINT IA_ident, ULONG T1, ULONG T2);
```

### <a name="description"></a><span data-ttu-id="5ab65-270">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-270">Description</span></span>

<span data-ttu-id="5ab65-271">Questo servizio crea un'associazione di identità (IANA) client non temporanea dai parametri forniti.</span><span class="sxs-lookup"><span data-stu-id="5ab65-271">This service creates a Client Non Temporary Identity Association (IANA) from the supplied parameters.</span></span> <span data-ttu-id="5ab65-272">Per impostare i tempi T1 e T2 su massimo (infinito) nelle richieste del client DHCPv6, impostare questi parametri su NX_DHCPV6_INFINITE_LEASE.</span><span class="sxs-lookup"><span data-stu-id="5ab65-272">To set the T1 and T2 times to maximum (infinity) in the DHCPv6 Client requests, set these parameters to NX_DHCPV6_INFINITE_LEASE.</span></span> 

> [!NOTE]
> <span data-ttu-id="5ab65-273">Un client dispone di un solo IANA.</span><span class="sxs-lookup"><span data-stu-id="5ab65-273">A Client has only one IANA.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-274">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-274">Input Parameters</span></span>

- <span data-ttu-id="5ab65-275">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-275">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-276">**IA_ident** Identificatore univoco dell'associazione di identità</span><span class="sxs-lookup"><span data-stu-id="5ab65-276">**IA_ident** Identity Association unique identifier</span></span>

- <span data-ttu-id="5ab65-277">**T1** Quando il client deve avviare il rinnovo degli indirizzi IPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-277">**T1** When the Client must start the IPv6 address renewal</span></span>

- <span data-ttu-id="5ab65-278">**T2** Quando il client deve avviare la riassociazione degli indirizzi theIPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-278">**T2** When the Client must start theIPv6 address rebinding</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-279">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-279">Return Values</span></span>

- <span data-ttu-id="5ab65-280">Il **NX_SUCCESS** (0x00) ha creato correttamente IANA</span><span class="sxs-lookup"><span data-stu-id="5ab65-280">**NX_SUCCESS** (0x00) Successfully created the IANA</span></span>

- <span data-ttu-id="5ab65-281">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-281">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-282">NX_DHCPV6_PARAM_ERROR (0xE93) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-282">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-283">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-283">Allowed From</span></span>

<span data-ttu-id="5ab65-284">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-284">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-285">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-285">Example</span></span>

```C
/* Create the Client IANA from the supplied input.  */
status = nx_dhcpv6_create_client_iana(&dhcp_0, DHCPV6_IA_ID, DHCPV6_T1,   
                                      DHCPV6_T2);

/* If status is NX_SUCCESS the client IANA was successfully created.  */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-286">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-286">See Also</span></span>

- <span data-ttu-id="5ab65-287">nx_dhcpv6_create_client_duid</span><span class="sxs-lookup"><span data-stu-id="5ab65-287">nx_dhcpv6_create_client_duid</span></span>
- <span data-ttu-id="5ab65-288">nx_dhcpv6_create_server_duid</span><span class="sxs-lookup"><span data-stu-id="5ab65-288">nx_dhcpv6_create_server_duid</span></span>
- <span data-ttu-id="5ab65-289">nx_dhcpv6_add_client_ia</span><span class="sxs-lookup"><span data-stu-id="5ab65-289">nx_dhcpv6_add_client_ia</span></span>

## <a name="nx_dhcpv6_add_client_ia"></a><span data-ttu-id="5ab65-290">nx_dhcpv6_add_client_ia</span><span class="sxs-lookup"><span data-stu-id="5ab65-290">nx_dhcpv6_add_client_ia</span></span> 

<span data-ttu-id="5ab65-291">Aggiungere un'associazione di identità al client</span><span class="sxs-lookup"><span data-stu-id="5ab65-291">Add an Identity Association to the Client</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-292">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-292">Prototype</span></span>

```C
UINT nx_dhcpv6_add_client_ia(NX_DHCPV6 *dhcpv6_ptr, 
                             NXD_ADDRESS *ipv6_address, 
                             ULONG preferred_lifetime, 
                             ULONG valid_lifetime);
```

### <a name="description"></a><span data-ttu-id="5ab65-293">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-293">Description</span></span>

<span data-ttu-id="5ab65-294">Questo servizio aggiunge un'associazione di identità client compilando il record client con i parametri forniti.</span><span class="sxs-lookup"><span data-stu-id="5ab65-294">This service adds a Client Identity Association by filling in the Client record with the supplied parameters.</span></span> <span data-ttu-id="5ab65-295">Per richiedere le durate massime preferite e valide, impostare questi parametri su infinito.</span><span class="sxs-lookup"><span data-stu-id="5ab65-295">To request the maximum preferred and valid lifetimes, set these parameters to infinity.</span></span> <span data-ttu-id="5ab65-296">Per aggiungere più di un IA a un client DHCPv6, impostare il NX_DHCPV6_MAX_IA_ADDRESS su un valore superiore al valore predefinito 1.</span><span class="sxs-lookup"><span data-stu-id="5ab65-296">To add more than one IA to a DHCPv6 Client, set the NX_DHCPV6_MAX_IA_ADDRESS to a value higher than the default value of 1.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-297">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-297">Input Parameters</span></span>

- <span data-ttu-id="5ab65-298">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-298">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-299">**Ipv6_address** Puntatore al blocco di indirizzi IP di NetX Duo</span><span class="sxs-lookup"><span data-stu-id="5ab65-299">**ipv6_address** Pointer to NetX Duo IP address block</span></span>

- <span data-ttu-id="5ab65-300">**preferred_lifetime** Intervallo di tempo prima che l'indirizzo IP sia deprecato</span><span class="sxs-lookup"><span data-stu-id="5ab65-300">**preferred_lifetime** Length of time before IP address is deprecated</span></span>

- <span data-ttu-id="5ab65-301">**valid_lifetime** Periodo di tempo prima della scadenza dell'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="5ab65-301">**valid_lifetime** Length of time before IP address is expired</span></span> 

### <a name="return-values"></a><span data-ttu-id="5ab65-302">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-302">Return Values</span></span>

- <span data-ttu-id="5ab65-303">**NX_SUCCESS** (0x00) client con esito positivo aggiunto</span><span class="sxs-lookup"><span data-stu-id="5ab65-303">**NX_SUCCESS** (0x00) Successful Client IA added</span></span>

- <span data-ttu-id="5ab65-304">Indirizzo IA duplicato **NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xEAF)</span><span class="sxs-lookup"><span data-stu-id="5ab65-304">**NX_DHCPV6_IA_ADDRESS_ALREADY_EXIST** (0xEAF) Duplicate IA address</span></span> 

- <span data-ttu-id="5ab65-305">**NX_DHCPV6_REACHED_MAX_IA_ADDRESS** (0XEAE) Ia supera il numero massimo di client IAS che è in grado di archiviare</span><span class="sxs-lookup"><span data-stu-id="5ab65-305">**NX_DHCPV6_REACHED_MAX_IA_ADDRESS** (0xEAE) IA exceeds the max IAs Client can store</span></span>

- <span data-ttu-id="5ab65-306">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-306">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-307">NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) non valido (ad esempio, null) indirizzo IA in IA</span><span class="sxs-lookup"><span data-stu-id="5ab65-307">NX_DHCPV6_INVALID_IA_ADDRESS (0xEA4) Invalid (e.g. null) IA address in IA</span></span>

- <span data-ttu-id="5ab65-308">NX_DHCPV6_PARAM_ERROR (0xE93) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-308">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

 
### <a name="allowed-from"></a><span data-ttu-id="5ab65-309">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-309">Allowed From</span></span>

<span data-ttu-id="5ab65-310">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-310">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-311">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-311">Example</span></span>

```C
/* Add an Client IA using the supplied input.   */
status = nx_dhcpv6_add_client_ia(&dhcp_0, &ipv6_address, 
                                 NX_DHCPV6_PREFERRED_LIFETIME,
                                 NX_DHCPV6_VALID_LIFETIME);

/* If status is NX_SUCCESS the client IA was successfully added.  */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-312">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-312">See Also</span></span>

- <span data-ttu-id="5ab65-313">nx_dhcpv6_create_client_duid</span><span class="sxs-lookup"><span data-stu-id="5ab65-313">nx_dhcpv6_create_client_duid</span></span>
- <span data-ttu-id="5ab65-314">nx_dhcpv6_create_server_duid</span><span class="sxs-lookup"><span data-stu-id="5ab65-314">nx_dhcpv6_create_server_duid</span></span>
- <span data-ttu-id="5ab65-315">nx_dhcpv6_create_client_iana</span><span class="sxs-lookup"><span data-stu-id="5ab65-315">nx_dhcpv6_create_client_iana</span></span>

## <a name="nx_dhcpv6_get_client_duid_time_id"></a><span data-ttu-id="5ab65-316">nx_dhcpv6_get_client_duid_time_id</span><span class="sxs-lookup"><span data-stu-id="5ab65-316">nx_dhcpv6_get_client_duid_time_id</span></span>

<span data-ttu-id="5ab65-317">Recupera l'ID ora dal client DUID</span><span class="sxs-lookup"><span data-stu-id="5ab65-317">Retrieves time ID from Client DUID</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-318">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-318">Prototype</span></span>

```C
UINT nx_dhcpv6_get_client_duid_time_id(NX_DHCPV6 *dhcpv6_ptr, ULONG *time_id);
```

### <a name="description"></a><span data-ttu-id="5ab65-319">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-319">Description</span></span>

<span data-ttu-id="5ab65-320">Questo servizio recupera il campo ID ora dal client DUID.</span><span class="sxs-lookup"><span data-stu-id="5ab65-320">This service retrieves the time ID field from the Client DUID.</span></span> <span data-ttu-id="5ab65-321">Se l'applicazione deve prima chiamare *nx_dhcpv6_create_client_duid*, per compilare il Duid client nell'istanza del client DHCPv6 oppure avrà un valore null per questo campo.</span><span class="sxs-lookup"><span data-stu-id="5ab65-321">If the application must first call *nx_dhcpv6_create_client_duid*, to fill in the Client DUID in the DHCPv6 Client instance or it will have a null value for this field.</span></span> <span data-ttu-id="5ab65-322">Lo scopo è quello di salvare i dati e presentare lo stesso DUID client al server, incluso il campo relativo all'ora, tra i riavvii.</span><span class="sxs-lookup"><span data-stu-id="5ab65-322">The intent is for the application to save this data and present the same Client DUID to the server, including the time field, across reboots.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-323">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-323">Input Parameters</span></span>

- <span data-ttu-id="5ab65-324">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-324">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-325">**TIME_ID** Puntatore al campo ora DUID client</span><span class="sxs-lookup"><span data-stu-id="5ab65-325">**time_id** Pointer to Client DUID time field</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-326">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-326">Return Values</span></span>

- <span data-ttu-id="5ab65-327">Sono stati recuperati i dati di lease IP **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="5ab65-327">**NX_SUCCESS** (0x00) IP lease data successfully retrieved</span></span>

- <span data-ttu-id="5ab65-328">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-328">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-329">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-329">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-330">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-330">Allowed From</span></span>

<span data-ttu-id="5ab65-331">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-331">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-332">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-332">Example</span></span>

```C
/* Retrieve the time ID from the Client DUID.  */
status = nx_dhcpv6_get_client_duid_time_id(&dhcp_0, &time_ID);

/* If status is NX_SUCCESS the time ID was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-333">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-333">See Also</span></span>

- <span data-ttu-id="5ab65-334">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-334">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="5ab65-335">nx_dhcpv6_get_time_lease_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-335">nx_dhcpv6_get_time_lease_data</span></span>
- <span data-ttu-id="5ab65-336">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-336">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="5ab65-337">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="5ab65-337">nx_dhcpv6_get_time_accrued</span></span>

## <a name="nx_dhcpv6_get_ip_address"></a><span data-ttu-id="5ab65-338">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-338">nx_dhcpv6_get_IP_address</span></span>

<span data-ttu-id="5ab65-339">Recupera l'indirizzo IPv6 globale del client</span><span class="sxs-lookup"><span data-stu-id="5ab65-339">Retrieves Client’s global IPv6 address</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-340">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-340">Prototype</span></span>

```C
UINT nx_dhcpv6_get_IP_address(NX_DHCPV6 *dhcpv6_ptr, 
                              NXD_ADDRESS *ip_address);
```

### <a name="description"></a><span data-ttu-id="5ab65-341">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-341">Description</span></span>

<span data-ttu-id="5ab65-342">Questo servizio recupera l'indirizzo IPv6 globale del client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-342">This service retrieves the Client’s global IPv6 address.</span></span> <span data-ttu-id="5ab65-343">Se il client non dispone di un indirizzo valido, viene restituito lo stato di errore.</span><span class="sxs-lookup"><span data-stu-id="5ab65-343">If the Client does not have a valid address, an error status is returned.</span></span> <span data-ttu-id="5ab65-344">Se un client dispone di più di un indirizzo IPv6 globale, viene restituito l'indirizzo IPv6 primario.</span><span class="sxs-lookup"><span data-stu-id="5ab65-344">If a Client has more than one global IPv6 address, the primary IPv6 address is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-345">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-345">Input Parameters</span></span>

- <span data-ttu-id="5ab65-346">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-346">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-347">**ip_address** Puntatore a indirizzo IPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-347">**ip_address** Pointer to IPv6 address</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-348">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-348">Return Values</span></span>

- <span data-ttu-id="5ab65-349">Indirizzo IPv6 **NX_SUCCESS** (0x00) assegnato correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-349">**NX_SUCCESS** (0x00) IPv6 address successfully assigned</span></span>

- <span data-ttu-id="5ab65-350">Indirizzo IPv6 **NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-350">**NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) IPv6 address is not valid</span></span>

- <span data-ttu-id="5ab65-351">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-351">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-352">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-352">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-353">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-353">Allowed From</span></span>

<span data-ttu-id="5ab65-354">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-354">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-355">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-355">Example</span></span>

```C
UINT address_status;
UINT address_index;

/* Retrieve the client’s assigned IP address.  */
status = nx_dhcpv6_get_IP_address(&dhcp_0, &ipv6_address);

/* If status is NX_SUCCESS the client IP address was assigned.
   Now register it with NetX Duo on the primary interface (index zero). 
   The address index is returned in the address_index field*/
status = nxd_ipv6_address_set(&ip_0, 0, &ipv6_address, 64, &address_index);
```

### <a name="see-also"></a><span data-ttu-id="5ab65-356">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-356">See Also</span></span>

- <span data-ttu-id="5ab65-357">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-357">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="5ab65-358">nx_dhcpv6_get_client_duid_time_id</span><span class="sxs-lookup"><span data-stu-id="5ab65-358">nx_dhcpv6_get_client_duid_time_id</span></span>
- <span data-ttu-id="5ab65-359">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-359">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="5ab65-360">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="5ab65-360">nx_dhcpv6_get_time_accrued</span></span>

## <a name="nx_dhcpv6_get_lease_time_data"></a><span data-ttu-id="5ab65-361">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-361">nx_dhcpv6_get_lease_time_data</span></span>

<span data-ttu-id="5ab65-362">Recupera i dati relativi alla durata del lease dell'indirizzo del client</span><span class="sxs-lookup"><span data-stu-id="5ab65-362">Retrieves Client’s IA address lease time data</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-363">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-363">Prototype</span></span>

```C
UINT nx_dhcpv6_get_lease_time_data(NX_DHCPV6 *dhcpv6_ptr, ULONG *T1, 
                                   ULONG *T2, ULONG *preferred_lifetime, 
                                   ULONG *valid_lifetime);
```

### <a name="description"></a><span data-ttu-id="5ab65-364">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-364">Description</span></span>

<span data-ttu-id="5ab65-365">Questo servizio recupera i dati relativi all'ora di indirizzi globali del client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-365">This service retrieves the Client’s global IA address time data.</span></span> <span data-ttu-id="5ab65-366">Se lo stato dell'indirizzo del client IA non è valido, i dati relativi all'ora vengono impostati su zero e viene restituito uno stato di completamento corretto.</span><span class="sxs-lookup"><span data-stu-id="5ab65-366">If the Client IA address status is invalid, time data is set to zero and a successful completion status is returned.</span></span> <span data-ttu-id="5ab65-367">Se un client ha più di un indirizzo IPv6 globale, vengono restituiti i dati dell'indirizzo IA primario.</span><span class="sxs-lookup"><span data-stu-id="5ab65-367">If a Client has more than one global IPv6 address, the primary IA address data is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-368">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-368">Input Parameters</span></span>

- <span data-ttu-id="5ab65-369">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-369">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-370">**T1** Puntatore al tempo di rinnovo dell'indirizzo IA</span><span class="sxs-lookup"><span data-stu-id="5ab65-370">**T1** Pointer to IA address renew time</span></span>

- <span data-ttu-id="5ab65-371">**T2** Puntatore a tempo di riassociazione indirizzo IA</span><span class="sxs-lookup"><span data-stu-id="5ab65-371">**T2** Pointer to IA address rebind time</span></span>

- <span data-ttu-id="5ab65-372">**preferred_lifetime** Puntatore all'ora in cui l'indirizzo IA è deprecato</span><span class="sxs-lookup"><span data-stu-id="5ab65-372">**preferred_lifetime** Pointer to time when IA address is deprecated</span></span>

- <span data-ttu-id="5ab65-373">**valid_lifetime** Puntatore all'ora in cui l'indirizzo IA è scaduto</span><span class="sxs-lookup"><span data-stu-id="5ab65-373">**valid_lifetime** Pointer to time when IA address is expired</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-374">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-374">Return Values</span></span>

- <span data-ttu-id="5ab65-375">Sono stati recuperati i dati di lease di **NX_SUCCESS** (0x00) Ia</span><span class="sxs-lookup"><span data-stu-id="5ab65-375">**NX_SUCCESS** (0x00) IA lease data successfully retrieved</span></span>

- <span data-ttu-id="5ab65-376">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-376">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-377">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-377">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-378">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-378">Allowed From</span></span>

<span data-ttu-id="5ab65-379">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-379">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-380">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-380">Example</span></span>

```C
/* Retrieve the client’s assigned IA lease data.  */
status = nx_dhcpv6_get_lease_time_data(&dhcp_0, &T1, &T2, &preferred_lifetime, 
                                       &valid_lifetime);

/* If status is NX_SUCCESS the client IA address lease data was retrieved.  */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-381">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-381">See Also</span></span>

- <span data-ttu-id="5ab65-382">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-382">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="5ab65-383">nx_dhcpv6_get_client_duid_time_id</span><span class="sxs-lookup"><span data-stu-id="5ab65-383">nx_dhcpv6_get_client_duid_time_id</span></span>
- <span data-ttu-id="5ab65-384">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-384">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="5ab65-385">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="5ab65-385">nx_dhcpv6_get_time_accrued</span></span>
- <span data-ttu-id="5ab65-386">nx_dhcpv6_get_iana_lease_time</span><span class="sxs-lookup"><span data-stu-id="5ab65-386">nx_dhcpv6_get_iana_lease_time</span></span>

## <a name="nx_dhcpv6_get_iana-lease_time"></a><span data-ttu-id="5ab65-387">nx_dhcpv6_get_iana lease_time</span><span class="sxs-lookup"><span data-stu-id="5ab65-387">nx_dhcpv6_get_iana lease_time</span></span>

<span data-ttu-id="5ab65-388">Recuperare i dati relativi al tempo di lease IANA del client</span><span class="sxs-lookup"><span data-stu-id="5ab65-388">Retrieve the Client’s IANA lease time data</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-389">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-389">Prototype</span></span>

```C
UINT nx_dhcpv6_get_iana_lease_time(NX_DHCPV6 *dhcpv6_ptr, ULONG *T1, 
                                    ULONG *T2);
```

### <a name="description"></a><span data-ttu-id="5ab65-390">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-390">Description</span></span>

<span data-ttu-id="5ab65-391">Questo servizio recupera i dati temporali di lease IA-NA globali del client (T1 e T2).</span><span class="sxs-lookup"><span data-stu-id="5ab65-391">This service retrieves the Client’s global IA-NA lease time data (T1 and T2).</span></span> <span data-ttu-id="5ab65-392">Se nessuno degli indirizzi client IA-NA ha uno stato di indirizzo valido, i dati relativi all'ora vengono impostati su zero e viene restituito uno stato di completamento corretto.</span><span class="sxs-lookup"><span data-stu-id="5ab65-392">If none of the Client IA-NA addresses have a valid address status, time data is set to zero and a successful completion status is returned.</span></span> <span data-ttu-id="5ab65-393">Se un client ha più di un indirizzo IPv6 globale, vengono restituiti i dati dell'indirizzo IA primario.</span><span class="sxs-lookup"><span data-stu-id="5ab65-393">If a Client has more than one global IPv6 address, the primary IA address data is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-394">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-394">Input Parameters</span></span>

- <span data-ttu-id="5ab65-395">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-395">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-396">**T1** Puntatore a tempo per l'avvio del rinnovo del lease</span><span class="sxs-lookup"><span data-stu-id="5ab65-396">**T1** Pointer to time for starting lease renewal</span></span>

- <span data-ttu-id="5ab65-397">**T2** Puntatore a tempo per l'avvio della riassociazione del lease</span><span class="sxs-lookup"><span data-stu-id="5ab65-397">**T2** Pointer to time for starting lease rebinding</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-398">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-398">Return Values</span></span>

- <span data-ttu-id="5ab65-399">**NX_SUCCESS** (0x00) dati di lease IANA recuperati correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-399">**NX_SUCCESS** (0x00) IANA lease data successfully retrieved</span></span>

- <span data-ttu-id="5ab65-400">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-400">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-401">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-401">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-402">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-402">Allowed From</span></span>

<span data-ttu-id="5ab65-403">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-403">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-404">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-404">Example</span></span>

```C
/* Retrieve the client’s assigned IANA lease data.  */
status = nx_dhcpv6_get_iana_lease_time(&dhcp_0, &T1, &T2);

/* If status is NX_SUCCESS the client IA address lease data was retrieved.  */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-405">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-405">See Also</span></span>

- <span data-ttu-id="5ab65-406">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-406">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="5ab65-407">nx_dhcpv6_get_client_duid_time_id</span><span class="sxs-lookup"><span data-stu-id="5ab65-407">nx_dhcpv6_get_client_duid_time_id</span></span>
- <span data-ttu-id="5ab65-408">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-408">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="5ab65-409">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="5ab65-409">nx_dhcpv6_get_time_accrued</span></span>
- <span data-ttu-id="5ab65-410">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-410">nx_dhcpv6_get_lease_time_data</span></span>

## <a name="nx_dhcpv6_get_valid_ip_address_count"></a><span data-ttu-id="5ab65-411">nx_dhcpv6_get_valid_ip_address_count</span><span class="sxs-lookup"><span data-stu-id="5ab65-411">nx_dhcpv6_get_valid_ip_address_count</span></span>

<span data-ttu-id="5ab65-412">Recuperare un numero di indirizzi IA validi del client</span><span class="sxs-lookup"><span data-stu-id="5ab65-412">Retrieve a count of Client’s valid IA addresses</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-413">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-413">Prototype</span></span>

```C
UINT nx_dhcpv6_get_valid_ip_address_count(NX_DHCPV6 *dhcpv6_ptr, 
                                          UINT *address_count);
```

### <a name="description"></a><span data-ttu-id="5ab65-414">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-414">Description</span></span>

<span data-ttu-id="5ab65-415">Questo servizio recupera il conteggio degli indirizzi IPv6 validi del client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-415">This service retrieves the count of the Client’s valid IPv6 addresses.</span></span> <span data-ttu-id="5ab65-416">Un indirizzo IPv6 valido viene associato (assegnato) al client e registrato con l'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="5ab65-416">A valid IPv6 address is bound (assigned) to the Client and registered with the IP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-417">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-417">Input Parameters</span></span>

- <span data-ttu-id="5ab65-418">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-418">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-419">**address_count** Puntatore al conteggio indirizzi da restituire</span><span class="sxs-lookup"><span data-stu-id="5ab65-419">**address_count** Pointer to address count to return</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-420">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-420">Return Values</span></span>

- <span data-ttu-id="5ab65-421">**NX_SUCCESS** (0x00) dati di lease IANA recuperati correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-421">**NX_SUCCESS** (0x00) IANA lease data successfully retrieved</span></span>

- <span data-ttu-id="5ab65-422">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-422">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-423">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-423">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-424">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-424">Allowed From</span></span>

<span data-ttu-id="5ab65-425">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-425">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-426">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-426">Example</span></span>

```C
UINT address_count; 

/* Retrieve the count of valid IA-NA addresses.  */
status = nx_dhcpv6_get_valid_ip_address_count(&dhcp_0, &address_count);

/* If status is NX_SUCCESS the client IA address count was retrieved.  */
```

## <a name="nx_dhcpv6_get_valid_ip_address_lease_time"></a><span data-ttu-id="5ab65-427">nx_dhcpv6_get_valid_ip_address_lease_time</span><span class="sxs-lookup"><span data-stu-id="5ab65-427">nx_dhcpv6_get_valid_ip_address_lease_time</span></span>

<span data-ttu-id="5ab65-428">Recuperare i dati client IA per indice dell'indirizzo</span><span class="sxs-lookup"><span data-stu-id="5ab65-428">Retrieve the Client IA data by address index</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-429">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-429">Prototype</span></span>

```C
UINT nx_dhcpv6_get_valid_ip_address_lease_time(NX_DHCPV6 *dhcpv6_ptr, 
                                               UINT address_index,
                                               NXD_ADDRESS *ip_address,
                                               ULONG *preferred_lifetime,
                                               ULONG *valid_lifetime);
```

### <a name="description"></a><span data-ttu-id="5ab65-430">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-430">Description</span></span>

<span data-ttu-id="5ab65-431">Questo servizio recupera l'indirizzo del client e i dati di lease in base all'indice dell'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="5ab65-431">This service retrieves the Client’s IA address and lease data by address index.</span></span> <span data-ttu-id="5ab65-432">Se viene fornito un indice non valido o l'indirizzo IPv6 in tale indice non è valido, il servizio restituisce uno stato di errore NX_DHCPV6_IA_ADDRESS_NOT_VALID.</span><span class="sxs-lookup"><span data-stu-id="5ab65-432">If an invalid index is supplied, or the IPv6 address at that index is not valid, the service returns an NX_DHCPV6_IA_ADDRESS_NOT_VALID error status.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-433">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-433">Input Parameters</span></span>

- <span data-ttu-id="5ab65-434">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-434">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-435">**address_index** Indicizzare in DHCPv6 IA Table</span><span class="sxs-lookup"><span data-stu-id="5ab65-435">**address_index** Index into DHCPv6 IA table</span></span>

- <span data-ttu-id="5ab65-436">**ip_address** Puntatore all'indirizzo IPv6 da recuperare</span><span class="sxs-lookup"><span data-stu-id="5ab65-436">**ip_address** Pointer to IPv6 address to retrieve</span></span>

- <span data-ttu-id="5ab65-437">**preferred_lifetime** Puntatore all'ora in cui l'indirizzo IA è deprecato</span><span class="sxs-lookup"><span data-stu-id="5ab65-437">**preferred_lifetime** Pointer to time when IA address is deprecated</span></span>

- <span data-ttu-id="5ab65-438">**valid_lifetime** Puntatore all'ora in cui l'indirizzo IA è scaduto</span><span class="sxs-lookup"><span data-stu-id="5ab65-438">**valid_lifetime** Pointer to time when IA address is expired</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-439">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-439">Return Values</span></span>

- <span data-ttu-id="5ab65-440">**NX_SUCCESS** (0x00) dati IANA recuperati correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-440">**NX_SUCCESS** (0x00) IANA data successfully retrieved</span></span>

- <span data-ttu-id="5ab65-441">**NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0XEAD) un indice non valido o nessun indirizzo IPv6 valido in corrispondenza dell'indice fornito</span><span class="sxs-lookup"><span data-stu-id="5ab65-441">**NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) An invalid index or no valid IPv6 address at the supplied index</span></span> 

- <span data-ttu-id="5ab65-442">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-442">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-443">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-443">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-444">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-444">Allowed From</span></span>

<span data-ttu-id="5ab65-445">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-445">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-446">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-446">Example</span></span>

```C
UINT address_index = 1; 
NXD_ADDRESS *ip_address;

/* Retrieve the IPv6 address, and valid and preferred lifetime for the IA record
   Saved at index 1 in the DHCPv6 table.  */
status = nx_dhcpv6_get_valid_ip_address_lease_time(&dhcp_0, address_index, 
                                                   &ip_address, 
                                                   &preferred_lifetime,  
                                                   &valid_lifetime);

/* If status is NX_SUCCESS the client IA address and lease data were retrieved.  */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-447">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-447">See Also</span></span>

- <span data-ttu-id="5ab65-448">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-448">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="5ab65-449">nx_dhcpv6_get_iana_lease_time</span><span class="sxs-lookup"><span data-stu-id="5ab65-449">nx_dhcpv6_get_iana_lease_time</span></span>
- <span data-ttu-id="5ab65-450">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-450">nx_dhcpv6_get_lease_time_data</span></span>

## <a name="nx_dhcpv6_get_dns_server_address"></a><span data-ttu-id="5ab65-451">nx_dhcpv6_get_DNS_server_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-451">nx_dhcpv6_get_DNS_server_address</span></span>

<span data-ttu-id="5ab65-452">Recupera l'indirizzo del server DNS</span><span class="sxs-lookup"><span data-stu-id="5ab65-452">Retrieves DNS Server address</span></span> 

### <a name="prototype"></a><span data-ttu-id="5ab65-453">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-453">Prototype</span></span>

```C
UINT nx_dhcpv6_get_DNS_server_address(NX_DHCPV6 *dhcpv6_ptr, UINT index,
                                      NXD_ADDRESS *server_address);
```

### <a name="description"></a><span data-ttu-id="5ab65-454">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-454">Description</span></span>

<span data-ttu-id="5ab65-455">Questo servizio recupera i dati dell'indirizzo IPv6 del server DNS in corrispondenza dell'indice specificato nell'elenco client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-455">This service retrieves the DNS server IPv6 address data at the specified index in the Client list.</span></span> <span data-ttu-id="5ab65-456">Se l'elenco non contiene un indirizzo del server in corrispondenza dell'indice, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="5ab65-456">If the list does not contain a server address at the index, an error is returned.</span></span> <span data-ttu-id="5ab65-457">L'indice non può superare le dimensioni dell'elenco di server DNS specificato dall'opzione configurabile dall'utente NX_DHCPV6_NUM_DNS_SERVERS.</span><span class="sxs-lookup"><span data-stu-id="5ab65-457">The index may not exceed the size of the DNS Server list is specified by the user configurable option NX_DHCPV6_NUM_DNS_SERVERS.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-458">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-458">Input Parameters</span></span>

- <span data-ttu-id="5ab65-459">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-459">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-460">**Indice** di Indicizzare nell'elenco dei server DNS</span><span class="sxs-lookup"><span data-stu-id="5ab65-460">**index** Index into the DNS Server list</span></span>

- <span data-ttu-id="5ab65-461">**server_address** Puntatore al buffer di indirizzi del server</span><span class="sxs-lookup"><span data-stu-id="5ab65-461">**server_address** Pointer to Server address buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-462">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-462">Return Values</span></span>

- <span data-ttu-id="5ab65-463">Indirizzo **NX_SUCCESS** (0x00) recuperato correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-463">**NX_SUCCESS** (0x00) Address successfully retrieved</span></span>

- <span data-ttu-id="5ab65-464">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-464">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-465">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-465">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-466">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-466">Allowed From</span></span>

<span data-ttu-id="5ab65-467">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-467">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-468">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-468">Example</span></span>

```C
/* Retrieve the DNS server at the specified index in the list. */

UINT index = 0;
NXD_ADDRESS server_address;


        status = nx_dhcpv6_get_DNS_server_address(&dhcp_0, index, &server_address);

/* If status == NX_SUCCESS, the DNS server IP address successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-469">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-469">See Also</span></span>

- <span data-ttu-id="5ab65-470">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-470">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="5ab65-471">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-471">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="5ab65-472">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="5ab65-472">nx_dhcpv6_get_time_accrued</span></span>

## <a name="nx_dhcpv6_get_other_option_data"></a><span data-ttu-id="5ab65-473">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-473">nx_dhcpv6_get_other_option_data</span></span>

<span data-ttu-id="5ab65-474">Recupera i dati dell'opzione DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-474">Retrieves DHCPv6 option data</span></span> 

### <a name="prototype"></a><span data-ttu-id="5ab65-475">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-475">Prototype</span></span>

```C
UINT  nx_dhcpv6_get_other_option_data(NX_DHCPV6 *dhcpv6_ptr, 
                                      UINT option_code, UCHAR *buffer);
```

### <a name="description"></a><span data-ttu-id="5ab65-476">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-476">Description</span></span>

<span data-ttu-id="5ab65-477">Questo servizio recupera i dati dell'opzione DHCPv6 da un messaggio DHCPv6 per il codice di opzione specificato.</span><span class="sxs-lookup"><span data-stu-id="5ab65-477">This service retrieves DHCPv6 option data from a DHCPv6 message for the specified option code.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-478">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-478">Input Parameters</span></span>

- <span data-ttu-id="5ab65-479">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-479">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-480">**opzione** codice opzione codice per i dati da recuperare</span><span class="sxs-lookup"><span data-stu-id="5ab65-480">**option** code Option code for which data to retrieve</span></span>

- <span data-ttu-id="5ab65-481">**buffer** Puntatore al buffer in cui copiare i dati</span><span class="sxs-lookup"><span data-stu-id="5ab65-481">**buffer** Pointer to buffer to copy data to</span></span> 

### <a name="return-values"></a><span data-ttu-id="5ab65-482">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-482">Return Values</span></span>

- <span data-ttu-id="5ab65-483">Sono stati recuperati i dati dell'opzione **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="5ab65-483">**NX_SUCCESS** (0x00) Option data successfully retrieved</span></span>

- <span data-ttu-id="5ab65-484">**NX_DHCPV6_UNKNOWN_OPTION** (0xEAB) codice opzione sconosciuto/non supportato</span><span class="sxs-lookup"><span data-stu-id="5ab65-484">**NX_DHCPV6_UNKNOWN_OPTION** (0xEAB) Unknown/unsupported option code</span></span>

- <span data-ttu-id="5ab65-485">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-485">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-486">NX_DHCPV6_PARAM_ERROR (0xE93) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-486">NX_DHCPV6_PARAM_ERROR (0xE93) Invalid non pointer input</span></span>

- <span data-ttu-id="5ab65-487">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-487">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-488">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-488">Allowed From</span></span>

<span data-ttu-id="5ab65-489">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-489">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-490">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-490">Example</span></span>

```C
/* Retrieve the option data specified by the input option code. */
status = nx_dhcpv6_get_other_option_data(&dhcp_0, option_code, buffer);

/* If status is NX_SUCCESS the option data was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-491">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-491">See Also</span></span>

- <span data-ttu-id="5ab65-492">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-492">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="5ab65-493">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-493">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="5ab65-494">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="5ab65-494">nx_dhcpv6_get_time_accrued</span></span>

## <a name="nx_dhcpv6_get_time_accrued"></a><span data-ttu-id="5ab65-495">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="5ab65-495">nx_dhcpv6_get_time_accrued</span></span>

<span data-ttu-id="5ab65-496">Recupera l'ora accumulata nel lease di indirizzi IP del client</span><span class="sxs-lookup"><span data-stu-id="5ab65-496">Retrieves time accrued on Client’s IP address lease</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-497">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-497">Prototype</span></span>

```C
UINT nx_dhcpv6_get_time_accrued(NX_DHCPV6 *dhcpv6_ptr, ULONG *time_accrued);
```

### <a name="description"></a><span data-ttu-id="5ab65-498">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-498">Description</span></span>

<span data-ttu-id="5ab65-499">Questo servizio recupera il tempo accumulato per il lease di indirizzi IPv6 del client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-499">This service retrieves the time accrued on the Client’s IPv6 address lease.</span></span> <span data-ttu-id="5ab65-500">La funzione controlla tutti gli indirizzi IPv6 assegnati al client per il primo indirizzo valido.</span><span class="sxs-lookup"><span data-stu-id="5ab65-500">The function checks all the IPv6 addresses assigned to the Client for the first valid address.</span></span> <span data-ttu-id="5ab65-501">Se non vengono trovati indirizzi validi, viene restituito un valore pari a zero per l'ora.</span><span class="sxs-lookup"><span data-stu-id="5ab65-501">If no valid addresses are found, a zero value for time accrued is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-502">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-502">Input Parameters</span></span>

- <span data-ttu-id="5ab65-503">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-503">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-504">**time_accrued** Puntatore a tempo accumulato nel lease IP</span><span class="sxs-lookup"><span data-stu-id="5ab65-504">**time_accrued** Pointer to time accrued in IP lease</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-505">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-505">Return Values</span></span>

- <span data-ttu-id="5ab65-506">Il tempo di maturazione **NX_SUCCESS** (0x00) è stato recuperato</span><span class="sxs-lookup"><span data-stu-id="5ab65-506">**NX_SUCCESS** (0x00) Accrued time successfully retrieved</span></span>

- <span data-ttu-id="5ab65-507">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-507">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-508">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-508">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-509">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-509">Allowed From</span></span>

<span data-ttu-id="5ab65-510">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-510">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-511">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-511">Example</span></span>

```C
/* Retrieve time accrued time on the Client address lease. */
status = nx_dhcpv6_get_time_accrued(&dhcp_0, &time_accrued);

/* If status is NX_SUCCESS the time accrued on the client IP address 
   lease was retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-512">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-512">See Also</span></span>

- <span data-ttu-id="5ab65-513">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-513">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="5ab65-514">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-514">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="5ab65-515">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-515">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="5ab65-516">nx_dhcpv6_set_time_accrued</span><span class="sxs-lookup"><span data-stu-id="5ab65-516">nx_dhcpv6_set_time_accrued</span></span>

## <a name="nx_dhcpv6_get_time_server_address"></a><span data-ttu-id="5ab65-517">nx_dhcpv6_get_time_server_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-517">nx_dhcpv6_get_time_server_address</span></span>

<span data-ttu-id="5ab65-518">Recupera l'indirizzo del server ora</span><span class="sxs-lookup"><span data-stu-id="5ab65-518">Retrieves Time Server address</span></span> 

### <a name="prototype"></a><span data-ttu-id="5ab65-519">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-519">Prototype</span></span>

```C
UINT  nx_dhcpv6_get_time_server_address(NX_DHCPV6 *dhcpv6_ptr, UINT index, 
                                        NXD_ADDRESS *server_address);
```

### <a name="description"></a><span data-ttu-id="5ab65-520">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-520">Description</span></span>

<span data-ttu-id="5ab65-521">Questo servizio recupera i dati dell'indirizzo IPv6 del server di tempo in corrispondenza dell'indice specificato nell'elenco client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-521">This service retrieves the Time server IPv6 address data at the specified index in the Client list.</span></span> <span data-ttu-id="5ab65-522">Se l'elenco non contiene un indirizzo del server in corrispondenza dell'indice, viene restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="5ab65-522">If the list does not contain a server address at the index, an error is returned.</span></span> <span data-ttu-id="5ab65-523">L'indice non può superare le dimensioni dell'elenco di server di tempo specificato dall'opzione configurabile dall'utente NX_DHCPV6_NUM_TIME_SERVERS.</span><span class="sxs-lookup"><span data-stu-id="5ab65-523">The index may not exceed the size of the Time Server list is specified by the user configurable option NX_DHCPV6_NUM_TIME_SERVERS.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-524">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-524">Input Parameters</span></span>

- <span data-ttu-id="5ab65-525">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-525">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-526">**Indice** di Indicizza nell'elenco dei server di tempo</span><span class="sxs-lookup"><span data-stu-id="5ab65-526">**index** Index into the Time Server list</span></span>

- <span data-ttu-id="5ab65-527">**server_address** Puntatore al buffer di indirizzi del server</span><span class="sxs-lookup"><span data-stu-id="5ab65-527">**server_address** Pointer to Server address buffer</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-528">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-528">Return Values</span></span>

- <span data-ttu-id="5ab65-529">Indirizzo **NX_SUCCESS** (0x00) recuperato correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-529">**NX_SUCCESS** (0x00) Address successfully retrieved</span></span>

- <span data-ttu-id="5ab65-530">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-530">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-531">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-531">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-532">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-532">Allowed From</span></span>

<span data-ttu-id="5ab65-533">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-533">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-534">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-534">Example</span></span>

```C
/* Retrieve the Time server at the specified index in the list. */

UINT index = 0;
NXD_ADDRESS server_address;


      status = nx_dhcpv6_get_time_server_address(&dhcp_0, index, &server_address);

/* If status == NX_SUCCESS, the Time server IP address successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-535">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-535">See Also</span></span>

- <span data-ttu-id="5ab65-536">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-536">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="5ab65-537">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-537">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="5ab65-538">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="5ab65-538">nx_dhcpv6_get_time_accrued</span></span>
- <span data-ttu-id="5ab65-539">nx_dhcpv6_get_DNS_server_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-539">nx_dhcpv6_get_DNS_server_address</span></span>

## <a name="nx_dhcpv6_reinitialize"></a><span data-ttu-id="5ab65-540">nx_dhcpv6_reinitialize</span><span class="sxs-lookup"><span data-stu-id="5ab65-540">nx_dhcpv6_reinitialize</span></span>

<span data-ttu-id="5ab65-541">Rimuovere l'indirizzo IP del client dalla tabella IP</span><span class="sxs-lookup"><span data-stu-id="5ab65-541">Remove the Client IP address from the IP table</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-542">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-542">Prototype</span></span>

```C
UINT nx_dhcpv6_reinitialize(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-543">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-543">Description</span></span>

<span data-ttu-id="5ab65-544">Questo servizio reinizializza il client per il riavvio della macchina a stati DHCPv6 ed esegue nuovamente il protocollo DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-544">This service reinitializes the Client for restarting the DHCPv6 state machine and re-running the DHCPv6 protocol.</span></span> <span data-ttu-id="5ab65-545">Questa operazione non è necessaria se il client non ha avviato in precedenza la macchina a stati DHPCv6 o non è stato assegnato alcun indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-545">This is not necessary if the Client has not previously started the DHPCv6 state machine or been assigned any IPv6 addresses.</span></span> <span data-ttu-id="5ab65-546">Gli indirizzi salvati nel client DHCPv6 e registrati con l'istanza IP vengono cancellati.</span><span class="sxs-lookup"><span data-stu-id="5ab65-546">The addresses saved to the DHCPv6 Client as well as registered with the IP instance are both cleared.</span></span>

> [!NOTE]
> <span data-ttu-id="5ab65-547">L'applicazione deve ancora avviare il client DHCPv6 utilizzando il *servizio nx_dhcpv6_start* e iniziare la richiesta di assegnazione di indirizzi IPv6 chiamando *nx_dhcpv6_request_solicit*.</span><span class="sxs-lookup"><span data-stu-id="5ab65-547">The application must still start the DHCPv6 Client using the *nx_dhcpv6_start service* and begin the request for IPv6 address assignment by calling *nx_dhcpv6_request_solicit*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-548">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-548">Input Parameters</span></span>

- <span data-ttu-id="5ab65-549">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-549">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-550">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-550">Return Values</span></span>

- <span data-ttu-id="5ab65-551">L'indirizzo **NX_SUCCESS** (0x00) è stato rimosso</span><span class="sxs-lookup"><span data-stu-id="5ab65-551">**NX_SUCCESS** (0x00) Address successfully removed</span></span>

- <span data-ttu-id="5ab65-552">Il client DHCPv6 **NX_DHCPV6_ALREADY_STARTED** (0xE91) è già in esecuzione</span><span class="sxs-lookup"><span data-stu-id="5ab65-552">**NX_DHCPV6_ALREADY_STARTED** (0xE91) DHCPv6 Client is already running</span></span>

- <span data-ttu-id="5ab65-553">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-553">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-554">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-554">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-555">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-555">Allowed From</span></span>

<span data-ttu-id="5ab65-556">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-556">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-557">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-557">Example</span></span>

```C
/* Clear the assigned IP address(es) from the Client and the IP instance */
status = nx_dhcpv6_reinitialize(&dhcp_0);

/* If status is NX_SUCCESS the Client IP address was successfully removed. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-558">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-558">See Also</span></span>

- <span data-ttu-id="5ab65-559">nx_dhcpv6_stop</span><span class="sxs-lookup"><span data-stu-id="5ab65-559">nx_dhcpv6_stop</span></span>
- <span data-ttu-id="5ab65-560">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="5ab65-560">nx_dhcpv6_start</span></span>

## <a name="nx_dhcpv6_request_confirm"></a><span data-ttu-id="5ab65-561">nx_dhcpv6_request_confirm</span><span class="sxs-lookup"><span data-stu-id="5ab65-561">nx_dhcpv6_request_confirm</span></span>

<span data-ttu-id="5ab65-562">Elaborare lo stato di conferma del client</span><span class="sxs-lookup"><span data-stu-id="5ab65-562">Process the Client’s CONFIRM state</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-563">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-563">Prototype</span></span>

```C
UINT nx_dhcpv6_request_confirm(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-564">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-564">Description</span></span>

<span data-ttu-id="5ab65-565">Questo servizio invia una richiesta di conferma.</span><span class="sxs-lookup"><span data-stu-id="5ab65-565">This service sends a CONFIRM request.</span></span> <span data-ttu-id="5ab65-566">Se viene ricevuta una risposta dal server, il client DHCPv6 aggiorna i relativi parametri di lease con i dati ricevuti.</span><span class="sxs-lookup"><span data-stu-id="5ab65-566">If a reply is received from the Server, the DHCPv6 Client updates its lease parameters with the received data.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-567">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-567">Input Parameters</span></span>

- <span data-ttu-id="5ab65-568">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-568">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-569">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-569">Return Values</span></span>

- <span data-ttu-id="5ab65-570">**NX_SUCCESS** (0x00) confermare che il messaggio è stato inviato ed elaborato correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-570">**NX_SUCCESS** (0x00) CONFIRM message successfully sent and processed</span></span>

- <span data-ttu-id="5ab65-571">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-571">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-572">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-572">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-573">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-573">Allowed From</span></span>

<span data-ttu-id="5ab65-574">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-574">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-575">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-575">Example</span></span>

```C
/* Send a CONFIRM message to the Server. */
status = nx_dhcpv6_request_confirm(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the CONFIRM message. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-576">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-576">See Also</span></span>

- <span data-ttu-id="5ab65-577">nx_dhcpv6_request_inform_request</span><span class="sxs-lookup"><span data-stu-id="5ab65-577">nx_dhcpv6_request_inform_request</span></span>
- <span data-ttu-id="5ab65-578">nx_dhcpv6_request_release</span><span class="sxs-lookup"><span data-stu-id="5ab65-578">nx_dhcpv6_request_release</span></span>
- <span data-ttu-id="5ab65-579">nx_dhcpv6_request_solicit</span><span class="sxs-lookup"><span data-stu-id="5ab65-579">nx_dhcpv6_request_solicit</span></span>


## <a name="nx_dhcpv6_request_inform_request"></a><span data-ttu-id="5ab65-580">nx_dhcpv6_request_inform_request</span><span class="sxs-lookup"><span data-stu-id="5ab65-580">nx_dhcpv6_request_inform_request</span></span>

<span data-ttu-id="5ab65-581">Elabora lo stato di richiesta di informazioni del client</span><span class="sxs-lookup"><span data-stu-id="5ab65-581">Process the Client’s INFORM REQUEST state</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-582">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-582">Prototype</span></span>

```C
UINT nx_dhcpv6_request_inform_request(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-583">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-583">Description</span></span>

<span data-ttu-id="5ab65-584">Questo servizio invia un messaggio di richiesta di notifica.</span><span class="sxs-lookup"><span data-stu-id="5ab65-584">This service sends an INFORM REQUEST message.</span></span> <span data-ttu-id="5ab65-585">Se viene ricevuta una risposta, quando ne viene ricevuta una, la risposta viene elaborata per determinare se è valida e il server ha concesso la richiesta.</span><span class="sxs-lookup"><span data-stu-id="5ab65-585">If a reply is received, When one is received, the reply is processed to determine it is valid and the server granted the request.</span></span> <span data-ttu-id="5ab65-586">L'istanza del client viene quindi aggiornata con le informazioni sul server in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="5ab65-586">The Client instance is then updated with the server information as needed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-587">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-587">Input Parameters</span></span>

- <span data-ttu-id="5ab65-588">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-588">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-589">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-589">Return Values</span></span>

- <span data-ttu-id="5ab65-590">**NX_SUCCESS** (0x00) informa che il messaggio di richiesta è stato creato ed elaborato correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-590">**NX_SUCCESS** (0x00) INFORM REQUEST message successfully created and processed</span></span>

- <span data-ttu-id="5ab65-591">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-591">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-592">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-592">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-593">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-593">Allowed From</span></span>

<span data-ttu-id="5ab65-594">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-594">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-595">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-595">Example</span></span>

```C
/* Send an INFORM REQUEST message to the server. */
status = nx_dhcpv6_request_inform_request(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the INFORM REQUEST 
   message and processed the reply. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-596">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-596">See Also</span></span>

- <span data-ttu-id="5ab65-597">nx_dhcpv6_request_confirm</span><span class="sxs-lookup"><span data-stu-id="5ab65-597">nx_dhcpv6_request_confirm</span></span>

## <a name="nx_dhcpv6_request_option_dns_server"></a><span data-ttu-id="5ab65-598">nx_dhcpv6_request_option_DNS_server</span><span class="sxs-lookup"><span data-stu-id="5ab65-598">nx_dhcpv6_request_option_DNS_server</span></span>

<span data-ttu-id="5ab65-599">Aggiungi server DNS alla richiesta di opzione DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-599">Add DNS Server to DHCPv6 Option request</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-600">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-600">Prototype</span></span>

```C
UINT nx_dhcpv6_request_option_DNS_server(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-601">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-601">Description</span></span>

<span data-ttu-id="5ab65-602">Questo servizio aggiunge l'opzione per richiedere le informazioni sul server DNS alla richiesta di opzione DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-602">This service adds the option for requesting DNS server information to the DHCPv6 option request.</span></span> <span data-ttu-id="5ab65-603">Se la risposta del server include i dati del server DNS, il client memorizzerà il server DNS se è presente spazio a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="5ab65-603">If the Server reply includes DNS server data, the Client will store the DNS server if it has room to do so.</span></span> <span data-ttu-id="5ab65-604">Il numero di server DNS che il client può archiviare è determinato dall'opzione configurabile NX_DHCPV6_NUM_DNS_SERVERS il cui valore predefinito è 2.</span><span class="sxs-lookup"><span data-stu-id="5ab65-604">The number of DNS servers the Client can store is determined by the configurable option NX_DHCPV6_NUM_DNS_SERVERS whose default value is 2.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-605">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-605">Input Parameters</span></span>

- <span data-ttu-id="5ab65-606">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-606">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-607">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-607">Return Values</span></span>

- <span data-ttu-id="5ab65-608">È inclusa l'opzione del server DNS **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="5ab65-608">**NX_SUCCESS** (0x00) DNS server option is included</span></span>

- <span data-ttu-id="5ab65-609">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-609">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-610">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-610">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-611">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-611">Allowed From</span></span>

<span data-ttu-id="5ab65-612">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-612">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-613">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-613">Example</span></span>

```C
/* Set the DNS server option in Client requests. */
nx_dhcpv6_request_option_DNS_server(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a><span data-ttu-id="5ab65-614">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-614">See Also</span></span>

- <span data-ttu-id="5ab65-615">nx_dhcpv6_request_option_domain_name</span><span class="sxs-lookup"><span data-stu-id="5ab65-615">nx_dhcpv6_request_option_domain_name</span></span>
- <span data-ttu-id="5ab65-616">nx_dhcpv6_request_option_time_server</span><span class="sxs-lookup"><span data-stu-id="5ab65-616">nx_dhcpv6_request_option_time_server</span></span>
- <span data-ttu-id="5ab65-617">nx_dhcpv6_request_option_timezone</span><span class="sxs-lookup"><span data-stu-id="5ab65-617">nx_dhcpv6_request_option_timezone</span></span>

## <a name="nx_dhcpv6_request_option_fqdn"></a><span data-ttu-id="5ab65-618">nx_dhcpv6_request_option_FQDN</span><span class="sxs-lookup"><span data-stu-id="5ab65-618">nx_dhcpv6_request_option_FQDN</span></span>

<span data-ttu-id="5ab65-619">Aggiungere l'opzione nome di dominio completo all'elenco di richieste di opzioni</span><span class="sxs-lookup"><span data-stu-id="5ab65-619">Add Fully Qualified Domain Name option to Option request list</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-620">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-620">Prototype</span></span>

```C
UINT nx_dhcpv6_request_option_FQDN(NX_DHCPV6 *dhcpv6_ptr, UCHAR *domain_name, 
UINT op);
```

### <a name="description"></a><span data-ttu-id="5ab65-621">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-621">Description</span></span>

<span data-ttu-id="5ab65-622">Questo servizio aggiunge l'opzione per l'aggiunta del nome di dominio completo del client alla richiesta di opzione DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-622">This service adds the option for adding the Client Fully Qualified Domain Name to the DHCPv6 option request.</span></span> <span data-ttu-id="5ab65-623">Sono disponibili tre opzioni per l'opzione FQDN:</span><span class="sxs-lookup"><span data-stu-id="5ab65-623">There are three options for the FQDN option:</span></span>

- <span data-ttu-id="5ab65-624">NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR 0 aggiornare il mapping degli indirizzi FQDN a IPv6 per il nome di dominio completo e l'indirizzo (es) usati dal client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-624">NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR 0 Update the FQDN-to-IPv6 address mapping for FQDN and address(es) used by the Client.</span></span>

- <span data-ttu-id="5ab65-625">NX_DHCPV6_CLIENT_DESIRES_SERVER_DO_DNS_UPDATE 1 aggiornare il mapping degli indirizzi FQDN a IPv6 per il nome di dominio completo e l'indirizzo (es) usati dal client al server.</span><span class="sxs-lookup"><span data-stu-id="5ab65-625">NX_DHCPV6_CLIENT_DESIRES_SERVER_DO_DNS_UPDATE 1 Update the FQDN-to-IPv6 address mapping for FQDN and address(es) used by the Client to the server.</span></span>

- <span data-ttu-id="5ab65-626">NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE 2 richiedere che il server non esegua aggiornamenti DNS per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5ab65-626">NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE 2 Request the server perform no DNS updates on the Client’s behalf.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-627">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-627">Input Parameters</span></span>

- <span data-ttu-id="5ab65-628">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-628">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-629">**Domain_name** Stringa che contiene il nome di dominio</span><span class="sxs-lookup"><span data-stu-id="5ab65-629">**domain_name** String holding the domain name</span></span>

- <span data-ttu-id="5ab65-630">**operazione operativa** Tipo di opzione FQDN da applicare (vedere l'elenco precedente)</span><span class="sxs-lookup"><span data-stu-id="5ab65-630">**op** Type of FQDN option to apply (see list above)</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-631">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-631">Return Values</span></span>

- <span data-ttu-id="5ab65-632">È inclusa l'opzione FQDN **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="5ab65-632">**NX_SUCCESS** (0x00) FQDN option is included</span></span>

- <span data-ttu-id="5ab65-633">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-633">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-634">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-634">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-635">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-635">Allowed From</span></span>

<span data-ttu-id="5ab65-636">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-636">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-637">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-637">Example</span></span>

```C
/* Set the FQDN option in Client DHCPv6 request. */
nx_dhcpv6_request_option_FQDN(&dhcp_0, “DHCPv6_Client”, 
                              NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE);
```

### <a name="see-also"></a><span data-ttu-id="5ab65-638">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-638">See Also</span></span>

- <span data-ttu-id="5ab65-639">nx_dhcpv6_request_option_domain_name</span><span class="sxs-lookup"><span data-stu-id="5ab65-639">nx_dhcpv6_request_option_domain_name</span></span>
- <span data-ttu-id="5ab65-640">nx_dhcpv6_request_option_time_server</span><span class="sxs-lookup"><span data-stu-id="5ab65-640">nx_dhcpv6_request_option_time_server</span></span>
- <span data-ttu-id="5ab65-641">nx_dhcpv6_request_option_timezone</span><span class="sxs-lookup"><span data-stu-id="5ab65-641">nx_dhcpv6_request_option_timezone</span></span>

## <a name="nx_dhcpv6_request_option_domain_name"></a><span data-ttu-id="5ab65-642">nx_dhcpv6_request_option_domain_name</span><span class="sxs-lookup"><span data-stu-id="5ab65-642">nx_dhcpv6_request_option_domain_name</span></span>

<span data-ttu-id="5ab65-643">Aggiunta dell'opzione nome dominio alla richiesta di opzione DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-643">Add domain name option to DHCPv6 option request</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-644">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-644">Prototype</span></span>

```C
UINT nx_dhcpv6_request_option_domain_name(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-645">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-645">Description</span></span>

<span data-ttu-id="5ab65-646">Questo servizio aggiunge l'opzione nome di dominio alla richiesta di opzione nei messaggi di richiesta client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-646">This service adds the domain name option to the option request in Client request messages.</span></span> <span data-ttu-id="5ab65-647">Se la risposta del server include i dati del nome di dominio, il client archivia le informazioni sul nome di dominio se le dimensioni del nome di dominio sono comprese nelle dimensioni del buffer per contenere il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="5ab65-647">If the Server reply includes domain name data, the Client will store the domain name information if the size of the domain name is within the buffer size for holding the domain name.</span></span> <span data-ttu-id="5ab65-648">Questa dimensione del buffer è un'opzione configurabile (NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE) con un valore predefinito di 30 byte.</span><span class="sxs-lookup"><span data-stu-id="5ab65-648">This buffer size is a configurable option (NX_DHCPV6_DOMAIN_NAME_BUFFER_SIZE) with a default value of 30 bytes.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-649">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-649">Input Parameters</span></span>

- <span data-ttu-id="5ab65-650">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-650">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-651">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-651">Return Values</span></span>

- <span data-ttu-id="5ab65-652">Set di opzioni del nome di dominio **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="5ab65-652">**NX_SUCCESS** (0x00) Domain name option set</span></span>

- <span data-ttu-id="5ab65-653">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-653">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-654">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-654">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-655">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-655">Allowed From</span></span>

<span data-ttu-id="5ab65-656">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-656">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-657">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-657">Example</span></span>

```C
/* Set the domain name option in Client requests. */
nx_dhcpv6_request_option_domain_name(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a><span data-ttu-id="5ab65-658">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-658">See Also</span></span>

- <span data-ttu-id="5ab65-659">nx_dhcpv6_request_option_DNS_server</span><span class="sxs-lookup"><span data-stu-id="5ab65-659">nx_dhcpv6_request_option_DNS_server</span></span>
- <span data-ttu-id="5ab65-660">nx_dhcpv6_request_option_time_server</span><span class="sxs-lookup"><span data-stu-id="5ab65-660">nx_dhcpv6_request_option_time_server</span></span>
- <span data-ttu-id="5ab65-661">nx_dhcpv6_request_option_timezone</span><span class="sxs-lookup"><span data-stu-id="5ab65-661">nx_dhcpv6_request_option_timezone</span></span>

## <a name="nx_dhcpv6_request_option_time_server"></a><span data-ttu-id="5ab65-662">nx_dhcpv6_request_option_time_server</span><span class="sxs-lookup"><span data-stu-id="5ab65-662">nx_dhcpv6_request_option_time_server</span></span>

<span data-ttu-id="5ab65-663">Imposta i dati del server di ora come richiesta facoltativa</span><span class="sxs-lookup"><span data-stu-id="5ab65-663">Set time server data as optional request</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-664">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-664">Prototype</span></span>

```C
UINT nx_dhcpv6_request_option_time_server(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-665">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-665">Description</span></span>

<span data-ttu-id="5ab65-666">Questo servizio aggiunge l'opzione per le informazioni sul server di tempo alla richiesta di opzione dei messaggi di richiesta client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-666">This service adds the option for time server information to the option request of Client request messages.</span></span> <span data-ttu-id="5ab65-667">Se la risposta del server include i dati di Tim server, il client archivia il server di ora se è presente spazio a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="5ab65-667">If the Server reply includes tim server data, the Client will store the time server if it has room to do so.</span></span> <span data-ttu-id="5ab65-668">Il numero di server di tempo che il client può archiviare è determinato dall'opzione configurabile</span><span class="sxs-lookup"><span data-stu-id="5ab65-668">The number of time servers the Client can store is determined by the configurable option</span></span>

<span data-ttu-id="5ab65-669">NX_DHCPV6_NUM_TIME _SERVERS il cui valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="5ab65-669">NX_DHCPV6_NUM_TIME _SERVERS whose default value is 1.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-670">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-670">Input Parameters</span></span>

- <span data-ttu-id="5ab65-671">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-671">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-672">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-672">Return Values</span></span>

- <span data-ttu-id="5ab65-673">Aggiunta l'opzione del server **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="5ab65-673">**NX_SUCCESS** (0x00) Time server option added</span></span>

- <span data-ttu-id="5ab65-674">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-674">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-675">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-675">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-676">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-676">Allowed From</span></span>

<span data-ttu-id="5ab65-677">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-677">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-678">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-678">Example</span></span>

```C
/* Set the time server option in Client request messages. */
nx_dhcpv6_request_option_time_server(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a><span data-ttu-id="5ab65-679">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-679">See Also</span></span>

- <span data-ttu-id="5ab65-680">nx_dhcpv6_request_option_DNS_server</span><span class="sxs-lookup"><span data-stu-id="5ab65-680">nx_dhcpv6_request_option_DNS_server</span></span>
- <span data-ttu-id="5ab65-681">nx_dhcpv6_request_option_domain_name</span><span class="sxs-lookup"><span data-stu-id="5ab65-681">nx_dhcpv6_request_option_domain_name</span></span>
- <span data-ttu-id="5ab65-682">nx_dhcpv6_request_option_timezone</span><span class="sxs-lookup"><span data-stu-id="5ab65-682">nx_dhcpv6_request_option_timezone</span></span>

## <a name="nx_dhcpv6_request_option_timezone"></a><span data-ttu-id="5ab65-683">nx_dhcpv6_request_option_timezone</span><span class="sxs-lookup"><span data-stu-id="5ab65-683">nx_dhcpv6_request_option_timezone</span></span>

<span data-ttu-id="5ab65-684">Imposta i dati del fuso orario come richiesta facoltativa</span><span class="sxs-lookup"><span data-stu-id="5ab65-684">Set time zone data as optional request</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-685">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-685">Prototype</span></span>

```C
UINT nx_dhcpv6_request_option_timezone(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-686">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-686">Description</span></span>

<span data-ttu-id="5ab65-687">Questo servizio aggiunge l'opzione per la richiesta di informazioni sul fuso orario alla richiesta di opzione client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-687">This service adds the option for requesting time zone information to the Client option request.</span></span> <span data-ttu-id="5ab65-688">Se la risposta del server include i dati del fuso orario, il client archivia le informazioni sul fuso orario se le dimensioni del fuso orario sono comprese nella dimensione del buffer per la conservazione del fuso orario.</span><span class="sxs-lookup"><span data-stu-id="5ab65-688">If the Server reply includes time zone data, the Client will store the time zone information if the size of the time zone is within the buffer size for holding the time zone.</span></span> <span data-ttu-id="5ab65-689">Questa dimensione del buffer è un'opzione configurabile (NX_DHCPV6_ TIME_ZONE _BUFFER_SIZE) con un valore predefinito di 10 byte.</span><span class="sxs-lookup"><span data-stu-id="5ab65-689">This buffer size is a configurable option (NX_DHCPV6_ TIME_ZONE _BUFFER_SIZE) with a default value of 10 bytes.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-690">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-690">Input Parameters</span></span>

- <span data-ttu-id="5ab65-691">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-691">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-692">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-692">Return Values</span></span>

- <span data-ttu-id="5ab65-693">Aggiunta l'opzione del fuso orario **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="5ab65-693">**NX_SUCCESS** (0x00) Time zone option added</span></span>

- <span data-ttu-id="5ab65-694">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-694">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-695">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-695">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-696">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-696">Allowed From</span></span>

<span data-ttu-id="5ab65-697">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-697">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-698">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-698">Example</span></span>

```C
/* Set time zone option in Client request messages. */
nx_dhcpv6_request_option_timezone(&dhcp_0, NX_TRUE);
```

### <a name="see-also"></a><span data-ttu-id="5ab65-699">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-699">See Also</span></span>

- <span data-ttu-id="5ab65-700">nx_dhcpv6_request_option_DNS_server</span><span class="sxs-lookup"><span data-stu-id="5ab65-700">nx_dhcpv6_request_option_DNS_server</span></span>
- <span data-ttu-id="5ab65-701">nx_dhcpv6_request_option_domain_name</span><span class="sxs-lookup"><span data-stu-id="5ab65-701">nx_dhcpv6_request_option_domain_name</span></span>
- <span data-ttu-id="5ab65-702">nx_dhcpv6_request_option_time_server</span><span class="sxs-lookup"><span data-stu-id="5ab65-702">nx_dhcpv6_request_option_time_server</span></span>

## <a name="nx_dhcpv6_request_release"></a><span data-ttu-id="5ab65-703">nx_dhcpv6_request_release</span><span class="sxs-lookup"><span data-stu-id="5ab65-703">nx_dhcpv6_request_release</span></span>

<span data-ttu-id="5ab65-704">Invia un messaggio di rilascio di DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-704">Send a DHCPv6 RELEASE message</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-705">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-705">Prototype</span></span>

```C
UINT nx_dhcpv6_request_release(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-706">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-706">Description</span></span>

<span data-ttu-id="5ab65-707">Questo servizio invia un messaggio di rilascio sulla rete client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-707">This service sends a RELEASE message on the Client network.</span></span> <span data-ttu-id="5ab65-708">Se il messaggio viene inviato correttamente, viene restituito un stato di esito positivo.</span><span class="sxs-lookup"><span data-stu-id="5ab65-708">If the message is successfully sent, a successful status is returned.</span></span> <span data-ttu-id="5ab65-709">Un completamento corretto non significa che il client ha ricevuto una risposta o che è stato ancora concesso un indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-709">A successful completion does not mean the Client received a response or has been granted an IPv6 address yet.</span></span> <span data-ttu-id="5ab65-710">L'attività thread del client DHCPv6 attende una risposta da un server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-710">The DHCPv6 Client thread task waits for a reply from a DHCPv6 Server.</span></span> <span data-ttu-id="5ab65-711">Se ne viene ricevuta una, verifica che la risposta sia valida e archivia i dati nel record client.</span><span class="sxs-lookup"><span data-stu-id="5ab65-711">If one is received, it checks the reply is valid and stores the data to the Client record.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-712">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-712">Input Parameters</span></span>

- <span data-ttu-id="5ab65-713">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-713">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-714">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-714">Return Values</span></span>

- <span data-ttu-id="5ab65-715">Messaggio di rilascio di **NX_SUCCESS** (0x00) inviato correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-715">**NX_SUCCESS** (0x00) RELEASE message successfully sent</span></span>

- <span data-ttu-id="5ab65-716">Attività client di **NX_DHCPV6_NOT_STARTED** (0XE92) DHCPV6 non avviata</span><span class="sxs-lookup"><span data-stu-id="5ab65-716">**NX_DHCPV6_NOT_STARTED** (0xE92) DHCPv6 Client task not started</span></span>

- <span data-ttu-id="5ab65-717">Indirizzo **NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) non associato al client</span><span class="sxs-lookup"><span data-stu-id="5ab65-717">**NX_DHCPV6_IA_ADDRESS_NOT_VALID** (0xEAD) Address not bound to Client</span></span>

- <span data-ttu-id="5ab65-718">**NX_INVALID_INTERFACE** (0X4C) non trovato nella tabella degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="5ab65-718">**NX_INVALID_INTERFACE** (0x4C) Not found in IP address table</span></span>

- <span data-ttu-id="5ab65-719">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-719">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-720">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-720">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-721">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-721">Allowed From</span></span>

<span data-ttu-id="5ab65-722">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-722">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-723">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-723">Example</span></span>

```C
/* Send an RELEASE message to the Server. */
status = nx_dhcpv6_request_release(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the RELEASE message. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-724">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-724">See Also</span></span>

- <span data-ttu-id="5ab65-725">nx_dhcpv6_request_confirm</span><span class="sxs-lookup"><span data-stu-id="5ab65-725">nx_dhcpv6_request_confirm</span></span>
- <span data-ttu-id="5ab65-726">nx_dhcpv6_request_inform_request</span><span class="sxs-lookup"><span data-stu-id="5ab65-726">nx_dhcpv6_request_inform_request</span></span>
- <span data-ttu-id="5ab65-727">nx_dhcpv6_request_solicit</span><span class="sxs-lookup"><span data-stu-id="5ab65-727">nx_dhcpv6_request_solicit</span></span>

## <a name="nx_dhcpv6_request_solicit"></a><span data-ttu-id="5ab65-728">nx_dhcpv6_request_solicit</span><span class="sxs-lookup"><span data-stu-id="5ab65-728">nx_dhcpv6_request_solicit</span></span>

<span data-ttu-id="5ab65-729">Invia un messaggio di SOLLECITAzione</span><span class="sxs-lookup"><span data-stu-id="5ab65-729">Send a SOLICIT message</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-730">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-730">Prototype</span></span>

```C
UINT nx_dhcpv6_request_solicit(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-731">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-731">Description</span></span>

<span data-ttu-id="5ab65-732">Questo servizio invia un messaggio di SOLLECITAzione sulla rete.</span><span class="sxs-lookup"><span data-stu-id="5ab65-732">This service sends a SOLICIT message out on the network.</span></span> <span data-ttu-id="5ab65-733">Se il messaggio viene inviato correttamente, viene restituito un stato di esito positivo.</span><span class="sxs-lookup"><span data-stu-id="5ab65-733">If the message is successfully sent, a successful status is returned.</span></span> <span data-ttu-id="5ab65-734">Un completamento corretto non significa che il client ha ricevuto una risposta o che è stato ancora concesso un indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-734">A successful completion does not mean the Client received a response or has been granted an IPv6 address yet.</span></span> <span data-ttu-id="5ab65-735">L'attività thread del client DHCPv6 è in attesa di una risposta (un messaggio di annuncio) da un server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-735">The DHCPv6 Client thread task waits for a reply (an ADVERTISE message) from a DHCPv6 Server.</span></span> <span data-ttu-id="5ab65-736">Se ne viene ricevuta una, verifica che la risposta sia valida, archivia i dati nel record client e promuove il client allo stato della richiesta.</span><span class="sxs-lookup"><span data-stu-id="5ab65-736">If one is received, it checks the reply is valid, stores the data to the Client record and promotes the Client to the REQUEST state.</span></span>

> [!NOTE] 
> <span data-ttu-id="5ab65-737">Se è impostata l'opzione di commit rapido, il client DHCPv6 passerà direttamente allo stato associato se riceve un messaggio di annuncio server valido.</span><span class="sxs-lookup"><span data-stu-id="5ab65-737">If the Rapid Commit option is set, the DHCPv6 Client will go directly to the Bound state if it receives a valid Server ADVERTISE message.</span></span> <span data-ttu-id="5ab65-738">Per ulteriori informazioni, vedere la descrizione del servizio per *nx_dhcpv6_request_solicit_rapid* .</span><span class="sxs-lookup"><span data-stu-id="5ab65-738">See the service description for *nx_dhcpv6_request_solicit_rapid* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-739">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-739">Input Parameters</span></span>

- <span data-ttu-id="5ab65-740">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-740">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-741">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-741">Return Values</span></span>

- <span data-ttu-id="5ab65-742">Messaggio di SOLLECITAzione **NX_SUCCESS** (0x00) inviato correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-742">**NX_SUCCESS** (0x00) SOLICIT message successfully sent</span></span>

- <span data-ttu-id="5ab65-743">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-743">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-744">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-744">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-745">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-745">Allowed From</span></span>

<span data-ttu-id="5ab65-746">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-746">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-747">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-747">Example</span></span>

```C
/* Send an SOLICIT message to the server. */
status = nx_dhcpv6_request_solicit(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the SOLICIT message. */
```

## <a name="nx_dhcpv6_request_solicit_rapid"></a><span data-ttu-id="5ab65-748">nx_dhcpv6_request_solicit_rapid</span><span class="sxs-lookup"><span data-stu-id="5ab65-748">nx_dhcpv6_request_solicit_rapid</span></span>

<span data-ttu-id="5ab65-749">Inviare un messaggio di SOLLECITAzione con l'opzione di commit rapido</span><span class="sxs-lookup"><span data-stu-id="5ab65-749">Send a SOLICIT message with the Rapid Commit option</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-750">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-750">Prototype</span></span>

```C
UINT nx_dhcpv6_request_solicit_rapid(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-751">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-751">Description</span></span>

<span data-ttu-id="5ab65-752">Questo servizio invia un messaggio di SOLLECITAzione in rete con il set di opzioni di commit rapido.</span><span class="sxs-lookup"><span data-stu-id="5ab65-752">This service sends a SOLICIT message out on the network with the Rapid Commit option set.</span></span> <span data-ttu-id="5ab65-753">Se il messaggio viene inviato correttamente, viene restituito un stato di esito positivo.</span><span class="sxs-lookup"><span data-stu-id="5ab65-753">If the message is successfully sent, a successful status is returned.</span></span> <span data-ttu-id="5ab65-754">Un completamento corretto non significa che il client ha ricevuto una risposta o che è stato ancora concesso un indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-754">A successful completion does not mean the Client received a response or has been granted an IPv6 address yet.</span></span> <span data-ttu-id="5ab65-755">L'attività thread del client DHCPv6 è in attesa di una risposta (un messaggio di annuncio) da un server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-755">The DHCPv6 Client thread task waits for a reply (an ADVERTISE message) from a DHCPv6 Server.</span></span> <span data-ttu-id="5ab65-756">Se ne viene ricevuta una, verifica che la risposta sia valida, archivia i dati nel record client e promuove il client allo stato associato.</span><span class="sxs-lookup"><span data-stu-id="5ab65-756">If one is received, it checks the reply is valid, stores the data to the Client record and promotes the Client to the BOUND state.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-757">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-757">Input Parameters</span></span>

- <span data-ttu-id="5ab65-758">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-758">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-759">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-759">Return Values</span></span>

- <span data-ttu-id="5ab65-760">Messaggio di SOLLECITAzione **NX_SUCCESS** (0x00) inviato correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-760">**NX_SUCCESS** (0x00) SOLICIT message successfully sent</span></span>

- <span data-ttu-id="5ab65-761">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-761">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-762">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-762">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-763">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-763">Allowed From</span></span>

<span data-ttu-id="5ab65-764">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-764">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-765">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-765">Example</span></span>

```C
/* Send an SOLICIT message to the server. */
status = nx_dhcpv6_request_solicit_rapid(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully sent the SOLICIT message. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-766">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-766">See Also</span></span>

- <span data-ttu-id="5ab65-767">nx_dhcpv6_request_solicit</span><span class="sxs-lookup"><span data-stu-id="5ab65-767">nx_dhcpv6_request_solicit</span></span>
- <span data-ttu-id="5ab65-768">nx_dhcpv6_request_confirm</span><span class="sxs-lookup"><span data-stu-id="5ab65-768">nx_dhcpv6_request_confirm</span></span>
- <span data-ttu-id="5ab65-769">nx_dhcpv6_request_inform_request</span><span class="sxs-lookup"><span data-stu-id="5ab65-769">nx_dhcpv6_request_inform_request</span></span>
- <span data-ttu-id="5ab65-770">nx_dhcpv6_request_release</span><span class="sxs-lookup"><span data-stu-id="5ab65-770">nx_dhcpv6_request_release</span></span>

## <a name="nx_dhcpv6_resume"></a><span data-ttu-id="5ab65-771">nx_dhcpv6_resume</span><span class="sxs-lookup"><span data-stu-id="5ab65-771">nx_dhcpv6_resume</span></span>

<span data-ttu-id="5ab65-772">Riavvia attività client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-772">Resume DHCPv6 Client task</span></span> 

### <a name="prototype"></a><span data-ttu-id="5ab65-773">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-773">Prototype</span></span>

```C
UINT nx_dhcpv6_resume(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-774">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-774">Description</span></span>

<span data-ttu-id="5ab65-775">Questo servizio riprende l'attività thread del client DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-775">This service resumes the DHCPv6 Client thread task.</span></span> <span data-ttu-id="5ab65-776">Lo stato corrente del client DHCPv6 verrà elaborato (ad esempio, con binding, sollecitazione)</span><span class="sxs-lookup"><span data-stu-id="5ab65-776">The current DHCPv6 Client state will be processed (e.g. Bound, Solicit)</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-777">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-777">Input Parameters</span></span>

- <span data-ttu-id="5ab65-778">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-778">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-779">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-779">Return Values</span></span>

- <span data-ttu-id="5ab65-780">Il client **NX_SUCCESS** (0x00) è stato ripreso</span><span class="sxs-lookup"><span data-stu-id="5ab65-780">**NX_SUCCESS** (0x00) Client successfully resumed</span></span>

- <span data-ttu-id="5ab65-781">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-781">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-782">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-782">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-783">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-783">Allowed From</span></span>

<span data-ttu-id="5ab65-784">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-784">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-785">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-785">Example</span></span>

```C
/* Resume the DHCPv6 Client task. */
status = nx_dhcpv6_resume(&dhcp_0);

/* If status is NX_SUCCESS the Client thread task successfully resumed. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-786">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-786">See Also</span></span>

- <span data-ttu-id="5ab65-787">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="5ab65-787">nx_dhcpv6_start</span></span>
- <span data-ttu-id="5ab65-788">nx_dhcpv6_stop</span><span class="sxs-lookup"><span data-stu-id="5ab65-788">nx_dhcpv6_stop</span></span>
- <span data-ttu-id="5ab65-789">nx_dhcpv6_suspend</span><span class="sxs-lookup"><span data-stu-id="5ab65-789">nx_dhcpv6_suspend</span></span>

## <a name="nx_dhcpv6_set_-time_accrued"></a><span data-ttu-id="5ab65-790">nx_dhcpv6_set_ time_accrued</span><span class="sxs-lookup"><span data-stu-id="5ab65-790">nx_dhcpv6_set_ time_accrued</span></span>

<span data-ttu-id="5ab65-791">Imposta il tempo accumulato per il lease degli indirizzi IP del client</span><span class="sxs-lookup"><span data-stu-id="5ab65-791">Sets time accrued on Client’s IP address lease</span></span>

### <a name="prototype"></a><span data-ttu-id="5ab65-792">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-792">Prototype</span></span>

```C
UINT nx_dhcpv6_set_time_accrued(NX_DHCPV6 *dhcpv6_ptr,
                                ULONG time_accrued);
```

### <a name="description"></a><span data-ttu-id="5ab65-793">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-793">Description</span></span>

<span data-ttu-id="5ab65-794">Questo servizio imposta il tempo accumulato per l'indirizzo IP globale del client poiché è stato assegnato dal server.</span><span class="sxs-lookup"><span data-stu-id="5ab65-794">This service sets the time accrued on the Client’s global IP address since it was assigned by the server.</span></span> <span data-ttu-id="5ab65-795">Questa operazione deve essere utilizzata solo se un client è attualmente associato a un indirizzo IPv6 assegnato.</span><span class="sxs-lookup"><span data-stu-id="5ab65-795">This should only be used if a Client is currently bound to an assigned IPv6 address.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-796">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-796">Input Parameters</span></span>

- <span data-ttu-id="5ab65-797">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-797">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

- <span data-ttu-id="5ab65-798">**time_accrued** Tempo accumulato nel lease IP</span><span class="sxs-lookup"><span data-stu-id="5ab65-798">**time_accrued** Time accrued in IP lease</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-799">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-799">Return Values</span></span>

- <span data-ttu-id="5ab65-800">Il tempo di **NX_SUCCESS** (0x00) è stato impostato correttamente</span><span class="sxs-lookup"><span data-stu-id="5ab65-800">**NX_SUCCESS** (0x00) Time accrued successfully set</span></span>

- <span data-ttu-id="5ab65-801">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-801">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-802">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-802">Allowed From</span></span>

<span data-ttu-id="5ab65-803">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-803">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-804">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-804">Example</span></span>

```C
/* Set time accrued since client’s assigned IP address was assigned. */
status = nx_dhcpv6_set_time_accrued(&dhcp_0, time_accrued);

/* If status is NX_SUCCESS the time accrued on the client IP address lease was 
   successfully set. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-805">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-805">See Also</span></span>

- <span data-ttu-id="5ab65-806">nx_dhcpv6_get_IP_address</span><span class="sxs-lookup"><span data-stu-id="5ab65-806">nx_dhcpv6_get_IP_address</span></span>
- <span data-ttu-id="5ab65-807">nx_dhcpv6_get_other_option_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-807">nx_dhcpv6_get_other_option_data</span></span>
- <span data-ttu-id="5ab65-808">nx_dhcpv6_get_lease_time_data</span><span class="sxs-lookup"><span data-stu-id="5ab65-808">nx_dhcpv6_get_lease_time_data</span></span>
- <span data-ttu-id="5ab65-809">nx_dhcpv6_get_time_accrued</span><span class="sxs-lookup"><span data-stu-id="5ab65-809">nx_dhcpv6_get_time_accrued</span></span>

## <a name="nx_dhcpv6_start"></a><span data-ttu-id="5ab65-810">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="5ab65-810">nx_dhcpv6_start</span></span>

<span data-ttu-id="5ab65-811">Avviare l'attività client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-811">Start the DHCPv6 Client task</span></span> 

### <a name="prototype"></a><span data-ttu-id="5ab65-812">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-812">Prototype</span></span>

```C
UINT nx_dhcpv6_start(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-813">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-813">Description</span></span>

<span data-ttu-id="5ab65-814">Questo servizio avvia l'attività client DHCPv6 e prepara il client per l'esecuzione del protocollo DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-814">This service starts the DHCPv6 Client task and prepares the Client for running the DHCPv6 protocol.</span></span> <span data-ttu-id="5ab65-815">Verifica che l'istanza del client disponga di informazioni sufficienti, ad esempio un client DUID, crea e associa il socket UDP per l'invio e la ricezione di messaggi DHCPv6 e attiva i timer per tenere traccia del tempo di sessione e quando il lease IPv6 corrente scade.</span><span class="sxs-lookup"><span data-stu-id="5ab65-815">It verifies the Client instance has sufficient information (such as a Client DUID), creates and binds the UDP socket for sending and receiving DHCPv6 messages and activates timers for keeping track of session time and when the current IPv6 lease expires.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-816">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-816">Input Parameters</span></span>

- <span data-ttu-id="5ab65-817">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-817">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-818">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-818">Return Values</span></span>

- <span data-ttu-id="5ab65-819">Il client **NX_SUCCESS** (0x00) è stato avviato</span><span class="sxs-lookup"><span data-stu-id="5ab65-819">**NX_SUCCESS** (0x00) Client successfully started</span></span>

- <span data-ttu-id="5ab65-820">Mancano le opzioni necessarie per il client **NX_DHCPV6_MISSING_REQUIRED_OPTIONS** (0xEA9)</span><span class="sxs-lookup"><span data-stu-id="5ab65-820">**NX_DHCPV6_MISSING_REQUIRED_OPTIONS** (0xEA9) Client missing required options</span></span>

- <span data-ttu-id="5ab65-821">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-821">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-822">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-822">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-823">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-823">Allowed From</span></span>

<span data-ttu-id="5ab65-824">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-824">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-825">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-825">Example</span></span>

```C
/* Start the DHCPv6 Client task. */
status = nx_dhcpv6_start(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully started. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-826">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-826">See Also</span></span>

- <span data-ttu-id="5ab65-827">nx_dhcpv6_resume</span><span class="sxs-lookup"><span data-stu-id="5ab65-827">nx_dhcpv6_resume</span></span>
- <span data-ttu-id="5ab65-828">nx_dhcpv6_suspend</span><span class="sxs-lookup"><span data-stu-id="5ab65-828">nx_dhcpv6_suspend</span></span>
- <span data-ttu-id="5ab65-829">nx_dhcpv6_stop</span><span class="sxs-lookup"><span data-stu-id="5ab65-829">nx_dhcpv6_stop</span></span>
- <span data-ttu-id="5ab65-830">nx_dhcpv6_reinitialize</span><span class="sxs-lookup"><span data-stu-id="5ab65-830">nx_dhcpv6_reinitialize</span></span>

## <a name="nx_dhcpv6_stop"></a><span data-ttu-id="5ab65-831">nx_dhcpv6_stop</span><span class="sxs-lookup"><span data-stu-id="5ab65-831">nx_dhcpv6_stop</span></span>

<span data-ttu-id="5ab65-832">Arrestare l'attività client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-832">Stop the DHCPv6 Client task</span></span> 

### <a name="prototype"></a><span data-ttu-id="5ab65-833">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-833">Prototype</span></span>

```C
UINT nx_dhcpv6_stop(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-834">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-834">Description</span></span>

<span data-ttu-id="5ab65-835">Questo servizio arresta l'attività client DHCPv6 e cancella i conteggi di ritrasmissione, l'intervallo massimo di ritrasmissione, disattiva i timer di scadenza della sessione e del lease e Annulla l'associazione della porta del socket client DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-835">This service stops the DHCPv6 Client task, and clears retransmission counts, maximum retransmission intervals, deactivates the session and lease expiration timers, and unbinds the DHCPv6 Client socket port.</span></span> <span data-ttu-id="5ab65-836">Per riavviare il client, è necessario prima arrestare ed eventualmente reinizializzare il client prima di avviare un'altra sessione con un server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="5ab65-836">To restart the Client, one must first stop and optionally reinitialize the Client before starting another session with any DHCPv6 server.</span></span> <span data-ttu-id="5ab65-837">Per ulteriori informazioni, vedere la sezione di esempio di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="5ab65-837">See the Small Example section for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-838">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-838">Input Parameters</span></span>

- <span data-ttu-id="5ab65-839">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-839">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-840">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-840">Return Values</span></span>

- <span data-ttu-id="5ab65-841">Il client **NX_SUCCESS** (0x00) è stato arrestato</span><span class="sxs-lookup"><span data-stu-id="5ab65-841">**NX_SUCCESS** (0x00) Client successfully stopped</span></span>

- <span data-ttu-id="5ab65-842">Thread client di **NX_DHCPV6_NOT_STARTED** (0xE92) non avviato</span><span class="sxs-lookup"><span data-stu-id="5ab65-842">**NX_DHCPV6_NOT_STARTED** (0xE92) Client thread not started</span></span>

- <span data-ttu-id="5ab65-843">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-843">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-844">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-844">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>


### <a name="allowed-from"></a><span data-ttu-id="5ab65-845">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-845">Allowed From</span></span>

<span data-ttu-id="5ab65-846">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-846">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-847">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-847">Example</span></span>

```C
/* Stop the DHCPv6 Client task. */
status = nx_dhcpv6_start(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully stopped. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-848">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-848">See Also</span></span>

- <span data-ttu-id="5ab65-849">nx_dhcpv6_resume</span><span class="sxs-lookup"><span data-stu-id="5ab65-849">nx_dhcpv6_resume</span></span>
- <span data-ttu-id="5ab65-850">nx_dhcpv6_suspend</span><span class="sxs-lookup"><span data-stu-id="5ab65-850">nx_dhcpv6_suspend</span></span>
- <span data-ttu-id="5ab65-851">nx_dhcpv6_reinitialize</span><span class="sxs-lookup"><span data-stu-id="5ab65-851">nx_dhcpv6_reinitialize</span></span>
- <span data-ttu-id="5ab65-852">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="5ab65-852">nx_dhcpv6_start</span></span>

## <a name="nx_dhcpv6_suspend"></a><span data-ttu-id="5ab65-853">nx_dhcpv6_suspend</span><span class="sxs-lookup"><span data-stu-id="5ab65-853">nx_dhcpv6_suspend</span></span>

<span data-ttu-id="5ab65-854">Sospendere l'attività del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-854">Suspend the DHCPv6 Client task</span></span> 

### <a name="prototype"></a><span data-ttu-id="5ab65-855">Prototipo</span><span class="sxs-lookup"><span data-stu-id="5ab65-855">Prototype</span></span>

```C
UINT nx_dhcpv6_suspend(NX_DHCPV6 *dhcpv6_ptr);
```

### <a name="description"></a><span data-ttu-id="5ab65-856">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ab65-856">Description</span></span>

<span data-ttu-id="5ab65-857">Questo servizio sospende l'attività del client DHCPv6 e tutte le richieste in corso di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5ab65-857">This service suspends the DHCPv6 client task and any request it was in the middle of processing.</span></span> <span data-ttu-id="5ab65-858">I timer vengono disattivati e lo stato del client è impostato su non in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5ab65-858">Timers are deactivated and the Client state is set to non-running.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="5ab65-859">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="5ab65-859">Input Parameters</span></span>

- <span data-ttu-id="5ab65-860">**dhcpv6_ptr** Puntatore all'istanza del client DHCPv6</span><span class="sxs-lookup"><span data-stu-id="5ab65-860">**dhcpv6_ptr** Pointer to DHCPv6 Client instance</span></span>

### <a name="return-values"></a><span data-ttu-id="5ab65-861">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="5ab65-861">Return Values</span></span>

- <span data-ttu-id="5ab65-862">Il client **NX_SUCCESS** (0x00) è stato sospeso</span><span class="sxs-lookup"><span data-stu-id="5ab65-862">**NX_SUCCESS** (0x00) Client successfully suspended</span></span>

- <span data-ttu-id="5ab65-863">Il client **NX_DHCPV6_NOT_STARTED** (0XE92) non è in esecuzione e non può essere sospeso</span><span class="sxs-lookup"><span data-stu-id="5ab65-863">**NX_DHCPV6_NOT_STARTED** (0XE92) Client not running so cannot be suspended</span></span>

- <span data-ttu-id="5ab65-864">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="5ab65-864">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

- <span data-ttu-id="5ab65-865">NX_CALLER_ERROR (0x11) deve essere chiamato dal thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-865">NX_CALLER_ERROR (0x11) Must be called from thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="5ab65-866">Consentito da</span><span class="sxs-lookup"><span data-stu-id="5ab65-866">Allowed From</span></span>

<span data-ttu-id="5ab65-867">Thread</span><span class="sxs-lookup"><span data-stu-id="5ab65-867">Threads</span></span>

### <a name="example"></a><span data-ttu-id="5ab65-868">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ab65-868">Example</span></span>

```C
/* Suspend the DHCPv6 Client task. */
status = nx_dhcpv6_suspend(&dhcp_0);

/* If status is NX_SUCCESS the Client successfully suspended. */
```

### <a name="see-also"></a><span data-ttu-id="5ab65-869">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5ab65-869">See Also</span></span>

- <span data-ttu-id="5ab65-870">nx_dhcpv6_resume</span><span class="sxs-lookup"><span data-stu-id="5ab65-870">nx_dhcpv6_resume</span></span>
- <span data-ttu-id="5ab65-871">nx_dhcpv6_start</span><span class="sxs-lookup"><span data-stu-id="5ab65-871">nx_dhcpv6_start</span></span>
- <span data-ttu-id="5ab65-872">nx_dhcpv6_reinitialize</span><span class="sxs-lookup"><span data-stu-id="5ab65-872">nx_dhcpv6_reinitialize</span></span>
- <span data-ttu-id="5ab65-873">nx_dhcpv6_stop</span><span class="sxs-lookup"><span data-stu-id="5ab65-873">nx_dhcpv6_stop</span></span>
