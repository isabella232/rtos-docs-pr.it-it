---
title: Capitolo 3-Descrizione dei servizi client DHCP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi client DHCP di Azure RTO NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f143a443221ae08848316a458a630a0790108198
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822022"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-dhcp-client-services"></a><span data-ttu-id="9c44a-103">Capitolo 3-Descrizione dei servizi client DHCP di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="9c44a-103">Chapter 3 - Description of Azure RTOS NetX Duo DHCP Client services</span></span>

<span data-ttu-id="9c44a-104">Questo capitolo contiene una descrizione di tutti i servizi client DHCP di Azure RTO NetX Duo (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="9c44a-104">This chapter contains a description of all Azure RTOS NetX Duo DHCP Client services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="9c44a-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="9c44a-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="9c44a-106">**nx_dhcp_create**: *creare un'istanza DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-106">**nx_dhcp_create**: *Create a DHCP instance*</span></span>
- <span data-ttu-id="9c44a-107">**nx_dhcp_clear_broadcast_flag**: *Cancella flag broadcast nei messaggi client*</span><span class="sxs-lookup"><span data-stu-id="9c44a-107">**nx_dhcp_clear_broadcast_flag**: *Clear broadcast flag on Client messages*</span></span>
- <span data-ttu-id="9c44a-108">**nx_dhcp_delete**: *eliminare un'istanza DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-108">**nx_dhcp_delete**: *Delete a DHCP instance*</span></span>
- <span data-ttu-id="9c44a-109">**nx_dhcp_force_renew**: *inviare un messaggio di rinnovo forzato*</span><span class="sxs-lookup"><span data-stu-id="9c44a-109">**nx_dhcp_force_renew**: *Send a force renew message*</span></span>
- <span data-ttu-id="9c44a-110">**nx_dhcp_packet_pool_set**: *impostare il pool di pacchetti client DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-110">**nx_dhcp_packet_pool_set**: *Set the DHCP Client packet pool*</span></span>
- <span data-ttu-id="9c44a-111">**nx_dhcp_decline**: inviare un *messaggio di rifiuto al server*</span><span class="sxs-lookup"><span data-stu-id="9c44a-111">**nx_dhcp_decline**: Send *Decline message to server*</span></span>
- <span data-ttu-id="9c44a-112">**nx_dhcp_release**: inviare un *messaggio di rilascio al server*</span><span class="sxs-lookup"><span data-stu-id="9c44a-112">**nx_dhcp_release**: Send *Release message to server*</span></span>
- <span data-ttu-id="9c44a-113">**nx_dhcp_reinitialize**: *Cancella parametri della rete client DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-113">**nx_dhcp_reinitialize**: *Clear DHCP client network parameters*</span></span>
- <span data-ttu-id="9c44a-114">**nx_dhcp_request_client_ip**: *specificare un indirizzo IP specifico*</span><span class="sxs-lookup"><span data-stu-id="9c44a-114">**nx_dhcp_request_client_ip**: *Specify a specific IP address*</span></span>
- <span data-ttu-id="9c44a-115">**nx_dhcp_send_request**: *inviare un messaggio DHCP al server*</span><span class="sxs-lookup"><span data-stu-id="9c44a-115">**nx_dhcp_send_request**: *Send DHCP message to server*</span></span>
- <span data-ttu-id="9c44a-116">**nx_dhcp_start**: *avviare l'elaborazione del client DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-116">**nx_dhcp_start**: *Start the DHCP Client processing*</span></span>
- <span data-ttu-id="9c44a-117">**nx_dhcp_stop**: *arrestare l'elaborazione del client DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-117">**nx_dhcp_stop**: *Stop the DHCP Client processing*</span></span>
- <span data-ttu-id="9c44a-118">**nx_dhcp_set_interface_index**: *impostare l'interfaccia per l'esecuzione del client DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-118">**nx_dhcp_set_interface_index**: *Set the interface to run DHCP Client*</span></span>
- <span data-ttu-id="9c44a-119">**nx_dhcp_server_address_get**: *ottenere l'indirizzo IP del server DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-119">**nx_dhcp_server_address_get**: *Get the DHCP server IP address*</span></span>
- <span data-ttu-id="9c44a-120">**nx_dhcp_state_change_notify**: *impostare la funzione di callback quando viene modificato lo stato DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-120">**nx_dhcp_state_change_notify**: *Set the callback function when DHCP state changes*</span></span>
- <span data-ttu-id="9c44a-121">**nx_dhcp_user_option_retrieve**: *recuperare l'opzione DHCP specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-121">**nx_dhcp_user_option_retrieve**: *Retrieve the specified DHCP option*</span></span>
- <span data-ttu-id="9c44a-122">**nx_dhcp_user_option_convert**: *conversione di quattro byte in ULONG*</span><span class="sxs-lookup"><span data-stu-id="9c44a-122">**nx_dhcp_user_option_convert**: *Convert four bytes to ULONG*</span></span>

<span data-ttu-id="9c44a-123">Servizi client DHCP specifici dell'interfaccia:</span><span class="sxs-lookup"><span data-stu-id="9c44a-123">Interface specific DHCP Client services:</span></span>
 
- <span data-ttu-id="9c44a-124">**nx_dhcp_interface_clear_broadcast_flag**: *Cancella il flag broadcast nei messaggi client sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-124">**nx_dhcp_interface_clear_broadcast_flag**: *Clear broadcast flag on Client messages on specified interface*</span></span>
- <span data-ttu-id="9c44a-125">**nx_dhcp_interface_enable**: *Abilita l'interfaccia per l'esecuzione di DHCP sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-125">**nx_dhcp_interface_enable**: *Enable interface to run DHCP on the specified interface*</span></span>
- <span data-ttu-id="9c44a-126">**nx_dhcp_interface_disable**: *disabilitare l'interfaccia per l'esecuzione di DHCP sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-126">**nx_dhcp_interface_disable**: *Disable interface to run DHCP on the specified interface*</span></span>
- <span data-ttu-id="9c44a-127">**nx_dhcp_interface_decline**: *inviare il messaggio di rifiuto al server sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-127">**nx_dhcp_interface_decline**: *Send Decline message to server on the specified interface*</span></span>
- <span data-ttu-id="9c44a-128">**nx_dhcp_interface_force_renew**: *inviare un messaggio Force Renew sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-128">**nx_dhcp_interface_force_renew**: *Send a force renew message on the specified interface*</span></span>
- <span data-ttu-id="9c44a-129">**nx_dhcp_interface_reinitialize**: *Cancella i parametri di rete del client DHCP nell'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-129">**nx_dhcp_interface_reinitialize**: *Clear DHCP client network parameters on the specified interface*</span></span>
- <span data-ttu-id="9c44a-130">**nx_dhcp_interface_release**: *inviare un messaggio di rilascio al server sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-130">**nx_dhcp_interface_release**: *Send Release message to server on the specified interface*</span></span>
- <span data-ttu-id="9c44a-131">**nx_dhcp_interface_request_client_ip**: *specificare un indirizzo IP specifico nell'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-131">**nx_dhcp_interface_request_client_ip**: *Specify a specific IP address on the specified interface*</span></span>
- <span data-ttu-id="9c44a-132">**nx_dhcp_interface_send_request**: *inviare un messaggio DHCP al server sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-132">**nx_dhcp_interface_send_request**: *Send DHCP message to server on the specified interface*</span></span>
- <span data-ttu-id="9c44a-133">**nx_dhcp_interface_server_address_get**: *ottenere l'indirizzo IP del server DHCP nell'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-133">**nx_dhcp_interface_server_address_get**: *Get the DHCP server IP address on the specified interface*</span></span>
- <span data-ttu-id="9c44a-134">**nx_dhcp_interface_start**: *avviare l'elaborazione del client DHCP sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-134">**nx_dhcp_interface_start**: *Start the DHCP Client processing on the specified interface*</span></span>
- <span data-ttu-id="9c44a-135">**nx_dhcp_interface_stop**: *arrestare l'elaborazione del client DHCP sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-135">**nx_dhcp_interface_stop**: *Stop the DHCP Client processing on the specified interface*</span></span>
- <span data-ttu-id="9c44a-136">**nx_dhcp_interface_state_change_notify**: *impostare la funzione di callback quando lo stato DHCP viene modificato sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-136">**nx_dhcp_interface_state_change_notify**: *Set the callback function when DHCP state changes on the specified interface*</span></span>
- <span data-ttu-id="9c44a-137">**nx_dhcp_interface_user_option_retrieve**: *recuperare l'opzione DHCP specificata nell'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-137">**nx_dhcp_interface_user_option_retrieve**: *Retrieve the specified DHCP option on the specified interface*</span></span>

<span data-ttu-id="9c44a-138">Servizi client DHCP se è stato definito NX_DHCP_CLIENT_RESORE_STATE:</span><span class="sxs-lookup"><span data-stu-id="9c44a-138">DHCP Client Services if NX_DHCP_CLIENT_RESORE_STATE is defined:</span></span>

- <span data-ttu-id="9c44a-139">**nx_dhcp_resume**: *Riprendi stato client DHCP stabilito in precedenza*</span><span class="sxs-lookup"><span data-stu-id="9c44a-139">**nx_dhcp_resume**: *Resume previously established DHCP Client state*</span></span>
- <span data-ttu-id="9c44a-140">**nx_dhcp_suspend**: *sospendere l'elaborazione dello stato del client DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-140">**nx_dhcp_suspend**: *Suspend processing the DHCP Client state*</span></span>
- <span data-ttu-id="9c44a-141">**nx_dhcp_client_get_record**: *creare un record dello stato del client DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-141">**nx_dhcp_client_get_record**: *Create a record of the DHCP Client state*</span></span>
- <span data-ttu-id="9c44a-142">**nx_dhcp_client_restore_record**: *ripristinare un record salvato in precedenza nel client DHCP*</span><span class="sxs-lookup"><span data-stu-id="9c44a-142">**nx_dhcp_client_restore_record**: *Restore a previously saved record to the DHCP Client*</span></span>
- <span data-ttu-id="9c44a-143">**nx_dhcp_client_update_time_remaining**: *aggiornare il tempo rimanente nello stato DHCP corrente*</span><span class="sxs-lookup"><span data-stu-id="9c44a-143">**nx_dhcp_client_update_time_remaining**: *Update the time remaining in the current DHCP state*</span></span>

<span data-ttu-id="9c44a-144">Servizi client DHCP specifici dell'interfaccia se NX_DHCP_CLIENT_RESORE_STATE è definito:</span><span class="sxs-lookup"><span data-stu-id="9c44a-144">Interface Specific DHCP Client Services if NX_DHCP_CLIENT_RESORE_STATE is defined:</span></span>

- <span data-ttu-id="9c44a-145">**nx_dhcp_client_interface_get_record**: *creare un record dello stato del client DHCP nell'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-145">**nx_dhcp_client_interface_get_record**: *Create a record of the DHCP Client state on the specified interface*</span></span>
- <span data-ttu-id="9c44a-146">**nx_dhcp_client_interface_restore_record**: *ripristinare un record salvato in precedenza nel client DHCP sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-146">**nx_dhcp_client_interface_restore_record**: *Restore a previously saved record to the DHCP Client on the specified interface*</span></span>
- <span data-ttu-id="9c44a-147">**nx_dhcp_client_interface_update_time_remaining**: *aggiornare l'ora rimanente nello stato DHCP corrente sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="9c44a-147">**nx_dhcp_client_interface_update_time_remaining**: *Update the time remaining in the current DHCP state on the specified interface*</span></span>

## <a name="nx_dhcp_create"></a><span data-ttu-id="9c44a-148">nx_dhcp_create</span><span class="sxs-lookup"><span data-stu-id="9c44a-148">nx_dhcp_create</span></span>

<span data-ttu-id="9c44a-149">Creare un'istanza DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-149">Create a DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-150">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-150">Prototype</span></span>

```c
UINT nx_dhcp_create(NX_DHCP *dhcp_ptr, NX_IP *ip_ptr, CHAR *name_ptr);
```

### <a name="description"></a><span data-ttu-id="9c44a-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-151">Description</span></span>

<span data-ttu-id="9c44a-152">Questo servizio crea un'istanza DHCP per l'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-152">This service creates a DHCP instance for the previously created IP instance.</span></span> <span data-ttu-id="9c44a-153">Per impostazione predefinita, l'interfaccia primaria è abilitata per l'esecuzione di DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-153">By default the primary interface is enabled for running DHCP.</span></span> <span data-ttu-id="9c44a-154">L'input del nome, sebbene non usato nell'implementazione di NetX duo del client DHCP, deve rispettare i criteri RFC 1035 per i nomi host.</span><span class="sxs-lookup"><span data-stu-id="9c44a-154">The name input, while not used in the NetX Duo implementation of DHCP Client, must follow RFC 1035 criteria for host names.</span></span> <span data-ttu-id="9c44a-155">La lunghezza totale non deve superare i 255 caratteri, le etichette separate da punti devono iniziare con una lettera e terminare con una lettera o un numero e possono contenere trattini ma nessun altro carattere non alfanumerico.</span><span class="sxs-lookup"><span data-stu-id="9c44a-155">The total length must not exceed 255 characters, the labels separate by dots must begin with a letter, and end with a letter or number, and may contain hyphens but no other non-alphanumeric character.</span></span>

<span data-ttu-id="9c44a-156">Se l'applicazione desidera eseguire un'altra interfaccia DHCP registrata con l'istanza IP (usando *nx_ip_interface_attach*), l'applicazione può chiamare *NX_DHCP_SET_INTERFACE_INDEX* per eseguire DHCP solo su tale interfaccia oppure *nx_dhcp_interface_enable* per eseguire DHCP su tale interfaccia.</span><span class="sxs-lookup"><span data-stu-id="9c44a-156">If the application would like to run DHCP another interface registered with the IP instance, (using *nx_ip_interface_attach*), the application can call *nx_dhcp_set_interface_index* to run DHCP on just that interface, or *nx_dhcp_interface_enable* to run DHCP on that interface as well.</span></span> <span data-ttu-id="9c44a-157">Per ulteriori informazioni, vedere la descrizione di questi servizi.</span><span class="sxs-lookup"><span data-stu-id="9c44a-157">See description of these services for more details.</span></span>

>[!NOTE]
> <span data-ttu-id="9c44a-158">L'applicazione deve verificare che il payload del pool di pacchetti client DHCP sia in grado di supportare la dimensione minima dei messaggi DHCP specificata dalla RFC 2131 sezione 2 (548 byte di dati del messaggio DHCP più le intestazioni UDP, IP e frame di rete fisica).</span><span class="sxs-lookup"><span data-stu-id="9c44a-158">The application must make sure the DHCP Client packet pool payload can support the minimum DHCP message size specified by the RFC 2131 Section 2 (548 bytes of DHCP message data plus UDP, IP and physical network frame headers).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-159">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-159">Input Parameters</span></span>

- <span data-ttu-id="9c44a-160">**dhcp_ptr**: puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-160">**dhcp_ptr**: Pointer to DHCP control block.</span></span> 
- <span data-ttu-id="9c44a-161">**ip_ptr**: puntatore all'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-161">**ip_ptr**: Pointer to previously created IP instance.</span></span>  
- <span data-ttu-id="9c44a-162">**name_ptr**: puntatore al nome host per l'istanza DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-162">**name_ptr**: Pointer to host name for DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-163">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-163">Return Values</span></span>

- <span data-ttu-id="9c44a-164">**NX_SUCCESS**: (0x00) creazione DHCP riuscita</span><span class="sxs-lookup"><span data-stu-id="9c44a-164">**NX_SUCCESS**: (0x00) Successful DHCP create</span></span>
- <span data-ttu-id="9c44a-165">**NX_DHCP_INVALID_NAME**: (0xA8) nome host non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-165">**NX_DHCP_INVALID_NAME**: (0xA8) Invalid host name</span></span>
- <span data-ttu-id="9c44a-166">**NX_DHCP_INVALID_PAYLOAD**: payload (0x9C) troppo piccolo per il messaggio DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-166">**NX_DHCP_INVALID_PAYLOAD**: (0x9C) Payload too small for DHCP message</span></span>
- <span data-ttu-id="9c44a-167">NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-167">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-168">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-168">Allowed From</span></span>

<span data-ttu-id="9c44a-169">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="9c44a-169">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-170">Example</span></span>

```c
/* Create a DHCP instance.  */
status =  nx_dhcp_create(&my_dhcp, &my_ip, "My-DHCP");

/* If status is NX_SUCCESS a DHCP instance was successfully created.  */
```

## <a name="nx_dhcp_interface_enable"></a><span data-ttu-id="9c44a-171">nx_dhcp_interface_enable</span><span class="sxs-lookup"><span data-stu-id="9c44a-171">nx_dhcp_interface_enable</span></span>

<span data-ttu-id="9c44a-172">Abilitare l'interfaccia specificata per l'esecuzione di DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-172">Enable the specified interface to run DHCP</span></span> 

### <a name="prototype"></a><span data-ttu-id="9c44a-173">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-173">Prototype</span></span>

```c
UINT nx_dhcp_interface_enable(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="9c44a-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-174">Description</span></span>

<span data-ttu-id="9c44a-175">Questo servizio Abilita l'interfaccia specificata per l'esecuzione di DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-175">This service enables the specified interface for running DHCP.</span></span> <span data-ttu-id="9c44a-176">Per impostazione predefinita, l'interfaccia primaria è abilitata per il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-176">By default the primary interface is enabled for DHCP Client.</span></span> <span data-ttu-id="9c44a-177">A questo punto, è possibile avviare DHCP su questa interfaccia chiamando *nx_dhcp_interface_start* o per avviare DHCP in tutte le interfacce abilitate *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="9c44a-177">At this point, DHCP can be started on this interface either by calling *nx_dhcp_interface_start* or to start DHCP on all enabled interfaces *nx_dhcp_start*.</span></span>

>[!NOTE] 
> <span data-ttu-id="9c44a-178">L'applicazione deve prima registrare questa interfaccia con l'istanza IP, usando *nx_ip_interface_attach.*</span><span class="sxs-lookup"><span data-stu-id="9c44a-178">The application must first register this interface with the IP instance, using *nx_ip_interface_attach.*</span></span>

<span data-ttu-id="9c44a-179">Per aggiungere questa interfaccia all'elenco delle interfacce abilitate, è inoltre necessario che sia disponibile un'interfaccia client DHCP "record".</span><span class="sxs-lookup"><span data-stu-id="9c44a-179">Further, there must be an available DHCP Client interface ‘record’ to add this interface to the list of enabled interfaces.</span></span> <span data-ttu-id="9c44a-180">Per impostazione predefinita NX_DHCP_CLIENT_MAX_RECORDS viene definito su 1.</span><span class="sxs-lookup"><span data-stu-id="9c44a-180">By default NX_DHCP_CLIENT_MAX_RECORDS is defined to 1.</span></span> <span data-ttu-id="9c44a-181">Impostare questa opzione sul numero massimo di interfacce previste per eseguire simultaneamente il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-181">Set this option to the maximum number of interfaces expected to run DHCP Client simultaneously.</span></span> <span data-ttu-id="9c44a-182">In genere NX_DHCP_CLIENT_MAX_RECORDS corrisponderà NX_MAX_PHYSICAL_INTERFACES; Tuttavia, se un dispositivo ha più interfacce fisiche rispetto a quanto previsto per l'esecuzione del client DHCP, può risparmiare memoria impostando NX_DHCP_CLIENT_MAX_RECORDS su un valore inferiore a quello specificato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-182">Typically NX_DHCP_CLIENT_MAX_RECORDS will equal NX_MAX_PHYSICAL_INTERFACES; however, if a device has more physical interfaces than it expects to run DHCP Client, it can save memory by setting NX_DHCP_CLIENT_MAX_RECORDS to less than that number.</span></span> <span data-ttu-id="9c44a-183">Non esiste un mapping uno-a-uno delle interfacce fisiche con i record dell'interfaccia client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-183">There is not a one to one mapping of physical interfaces with DHCP Client interface records.</span></span>

<span data-ttu-id="9c44a-184">La differenza tra questo servizio e *nx_dhcp_set_interface_index* è la seconda che imposta una sola interfaccia per eseguire DHCP, mentre questo servizio aggiunge semplicemente l'interfaccia specificata all'elenco di interfacce client abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-184">The difference between this service and *nx_dhcp_set_interface_index* is the latter sets only a single interface to run DHCP whereas this service simply adds the specified interface to the list of Client interfaces enabled for DHCP.</span></span>

<span data-ttu-id="9c44a-185">Per disabilitare un'interfaccia per DHCP, l'applicazione può chiamare il</span><span class="sxs-lookup"><span data-stu-id="9c44a-185">To disable an interface for DHCP, the application can call the</span></span>

<span data-ttu-id="9c44a-186">servizio *nx_dhcp_interface_disable* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-186">*nx_dhcp_interface_disable* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-187">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-187">Input Parameters</span></span>

- <span data-ttu-id="9c44a-188">**dhcp_ptr**: puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-188">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="9c44a-189">**interface_index**: Indice dell'interfaccia per abilitare DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-189">**interface_index**: Index of interface to enable DHCP on</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-190">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-190">Return Values</span></span>

- <span data-ttu-id="9c44a-191">**NX_SUCCESS**: (0x00) Abilitazione DHCP riuscita</span><span class="sxs-lookup"><span data-stu-id="9c44a-191">**NX_SUCCESS**: (0x00) Successful DHCP enable</span></span>
- <span data-ttu-id="9c44a-192">**NX_DHCP_NO_RECORDS_AVAILABLE**: (0XA7) non sono disponibili record per un'altra interfaccia da abilitare per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-192">**NX_DHCP_NO_RECORDS_AVAILABLE**: (0xA7) No record available for another Interface to be enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-193">Interfaccia **NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-193">**NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) Interface enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-194">NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-194">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>
- <span data-ttu-id="9c44a-195">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-195">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-196">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-196">Allowed From</span></span>

<span data-ttu-id="9c44a-197">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="9c44a-197">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-198">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-198">Example</span></span>

```c
/* Enable DHCP on a secondary interface. It is already enabled on the primary 
   interface.  NX_DHCP_CLIENT_MAX_RECORDS is set to 2. */

status =  nx_dhcp_interface_enable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface was successfully enabled.  */


status = nx_dhcp_start(&my_dhcp);
/* If status is NX_SUCCESS DHCP is running on interface 0 and 1.  */
```

## <a name="nx_dhcp_interface_disable"></a><span data-ttu-id="9c44a-199">nx_dhcp_interface_disable</span><span class="sxs-lookup"><span data-stu-id="9c44a-199">nx_dhcp_interface_disable</span></span>

<span data-ttu-id="9c44a-200">Disabilitare l'interfaccia specificata per eseguire DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-200">Disable the specified interface to run DHCP</span></span> 

### <a name="prototype"></a><span data-ttu-id="9c44a-201">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-201">Prototype</span></span>

```c

UINT nx_dhcp_interface_disable(NX_DHCP *dhcp_ptr, 
                               UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="9c44a-202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-202">Description</span></span>

<span data-ttu-id="9c44a-203">Questo servizio Disabilita l'interfaccia specificata per l'esecuzione di DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-203">This service disables the specified interface for running DHCP.</span></span> <span data-ttu-id="9c44a-204">Reinizializza il client DHCP su questa interfaccia.</span><span class="sxs-lookup"><span data-stu-id="9c44a-204">It reinitializes the DHCP Client on this interface.</span></span>

<span data-ttu-id="9c44a-205">Per riavviare il client DHCP, l'applicazione deve riabilitare l'interfaccia utilizzando *nx_dhcp_interface_enable* e riavviare DHCP chiamando *nx_dhcp_interface_start*.</span><span class="sxs-lookup"><span data-stu-id="9c44a-205">To restart the DHCP Client the application must re-enable the interface using *nx_dhcp_interface_enable* and restart DHCP by calling *nx_dhcp_interface_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-206">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-206">Input Parameters</span></span>

- <span data-ttu-id="9c44a-207">**dhcp_ptr**: puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-207">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="9c44a-208">**interface_index**: Indice dell'interfaccia in cui disabilitare DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-208">**interface_index**: Index of interface to disable DHCP on</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-209">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-209">Return Values</span></span>

- <span data-ttu-id="9c44a-210">**NX_SUCCESS**: (0x00) creazione DHCP riuscita</span><span class="sxs-lookup"><span data-stu-id="9c44a-210">**NX_SUCCESS**: (0x00) Successful DHCP create</span></span>
- <span data-ttu-id="9c44a-211">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-211">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-212">NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-212">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>
- <span data-ttu-id="9c44a-213">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-213">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>
- <span data-ttu-id="9c44a-214">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-214">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-215">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-215">Allowed From</span></span>

<span data-ttu-id="9c44a-216">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-216">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-217">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-217">Example</span></span>

```c
/* Disable DHCP on a secondary interface. */

status =  nx_dhcp_interface_disable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface is successfully disabled.  */
```
## <a name="nx_dhcp_clear_broadcast_flag"></a><span data-ttu-id="9c44a-218">nx_dhcp_clear_broadcast_flag</span><span class="sxs-lookup"><span data-stu-id="9c44a-218">nx_dhcp_clear_broadcast_flag</span></span>

<span data-ttu-id="9c44a-219">Imposta il flag di trasmissione DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-219">Set the DHCP broadcast flag</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-220">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-220">Prototype</span></span>

```c
UINT nx_dhcp_clear_broadcast_flag(NX_DHCP *dhcp_ptr, UINT clear_flag);
```

### <a name="description"></a><span data-ttu-id="9c44a-221">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-221">Description</span></span>

<span data-ttu-id="9c44a-222">Questo servizio imposta o cancella il flag di trasmissione l'intestazione del messaggio DHCP per tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-222">This service sets or clears the broadcast flag the DHCP message header for all interfaces enabled for DHCP.</span></span> <span data-ttu-id="9c44a-223">Per alcuni messaggi DHCP, ad esempio DISCOVER, il flag broadcast è impostato su broadcast perché il client non dispone di un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-223">For some DHCP messages (e.g. DISCOVER) the broadcast flag is set to broadcast because the Client does not have an IP address.</span></span>

<span data-ttu-id="9c44a-224">valori clear_flag:</span><span class="sxs-lookup"><span data-stu-id="9c44a-224">clear_flag values:</span></span> 

- <span data-ttu-id="9c44a-225">**NX_TRUE**: il flag broadcast è cancellato (richiesta unicast risposta)</span><span class="sxs-lookup"><span data-stu-id="9c44a-225">**NX_TRUE**: broadcast flag is cleared (request unicast response)</span></span>
- <span data-ttu-id="9c44a-226">**NX_FALSE**: flag broadcast impostato (risposta broadcast richiesta)</span><span class="sxs-lookup"><span data-stu-id="9c44a-226">**NX_FALSE**: broadcast flag is set (request broadcast response)</span></span>

<span data-ttu-id="9c44a-227">Questo servizio è destinato ai client DHCP che devono passare attraverso un router per accedere al server DHCP, in cui il router rifiuta l'invio di messaggi broadcast.</span><span class="sxs-lookup"><span data-stu-id="9c44a-227">This service is intended for DHCP Clients that must go through a router to get to the DHCP Server, where the router rejects forwarding broadcast messages.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-228">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-228">Input Parameters</span></span>

- <span data-ttu-id="9c44a-229">**dhcp_ptr**: puntatore al blocco di controllo DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-229">**dhcp_ptr**: Pointer to DHCP control block</span></span>  
- <span data-ttu-id="9c44a-230">**clear_flag**: valore su cui impostare il flag di trasmissione</span><span class="sxs-lookup"><span data-stu-id="9c44a-230">**clear_flag**: Value to set the broadcast flag to</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-231">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-231">Return Values</span></span>

- <span data-ttu-id="9c44a-232">**NX_SUCCESS**: (0x00) impostazione del flag completata</span><span class="sxs-lookup"><span data-stu-id="9c44a-232">**NX_SUCCESS**: (0x00) Successfully set flag</span></span>
- <span data-ttu-id="9c44a-233">NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-233">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-234">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-234">Allowed From</span></span>

<span data-ttu-id="9c44a-235">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="9c44a-235">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-236">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-236">Example</span></span>

```c
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a  
    unicast response).  */
status =  nx_dhcp_clear_broadcast_flag(&my_dhcp, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated.  */
```

## <a name="nx_dhcp_interface_clear_broadcast_flag"></a><span data-ttu-id="9c44a-237">nx_dhcp_interface_clear_broadcast_flag</span><span class="sxs-lookup"><span data-stu-id="9c44a-237">nx_dhcp_interface_clear_broadcast_flag</span></span>

<span data-ttu-id="9c44a-238">Imposta o deseleziona il flag broadcast sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-238">Set or clear the broadcast flag on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-239">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-239">Prototype</span></span>

```c
UINT nx_dhcp_interface_clear_broadcast_flag(NX_DHCP *dhcp_ptr, 
                                            UINT interface_index, 
                                            UINT clear_flag);
```

### <a name="description"></a><span data-ttu-id="9c44a-240">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-240">Description</span></span>

<span data-ttu-id="9c44a-241">Questo servizio consente all'applicazione host client DHCP di impostare o deselezionare il flag di trasmissione nei messaggi client DHCP per il server DHCP sull'interfaccia specificata.</span><span class="sxs-lookup"><span data-stu-id="9c44a-241">This service enables the DHCP Client host application to set or clear the broadcast flag in DHCP Client messages to the DHCP Server on the specified interface.</span></span> <span data-ttu-id="9c44a-242">Per ulteriori informazioni, vedere **nx_dhcp_clear_broadcast_flag**.</span><span class="sxs-lookup"><span data-stu-id="9c44a-242">For more details see **nx_dhcp_clear_broadcast_flag**.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-243">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-243">Input Parameters</span></span>

- <span data-ttu-id="9c44a-244">**dhcp_ptr**: puntatore al blocco di controllo DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-244">**dhcp_ptr**: Pointer to DHCP control block</span></span>
- <span data-ttu-id="9c44a-245">**interface_index**: Indice dell'interfaccia per impostare il flag di trasmissione</span><span class="sxs-lookup"><span data-stu-id="9c44a-245">**interface_index**: Index of interface to set the broadcast flag</span></span>
- <span data-ttu-id="9c44a-246">**clear_flag**: valore su cui impostare il flag di trasmissione</span><span class="sxs-lookup"><span data-stu-id="9c44a-246">**clear_flag**: Value to set the broadcast flag to</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-247">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-247">Return Values</span></span>

- <span data-ttu-id="9c44a-248">**NX_SUCCESS**: (0x00) impostazione del flag completata</span><span class="sxs-lookup"><span data-stu-id="9c44a-248">**NX_SUCCESS**: (0x00) Successfully set flag</span></span>
- <span data-ttu-id="9c44a-249">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-249">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-250">NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-250">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>
- <span data-ttu-id="9c44a-251">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-251">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-252">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-252">Allowed From</span></span>

<span data-ttu-id="9c44a-253">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="9c44a-253">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-254">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-254">Example</span></span>

```c
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a 
   unicast response) on a previously attached secondary interface.  */

iface_index = 1;

status =  nx_dhcp_interface_clear_broadcast_flag(&my_dhcp, iface_index, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated.  */
```

## <a name="nx_dhcp_delete"></a><span data-ttu-id="9c44a-255">nx_dhcp_delete</span><span class="sxs-lookup"><span data-stu-id="9c44a-255">nx_dhcp_delete</span></span>

<span data-ttu-id="9c44a-256">Eliminare un'istanza DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-256">Delete a DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-257">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-257">Prototype</span></span>

```c
UINT nx_dhcp_delete(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="9c44a-258">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-258">Description</span></span>

<span data-ttu-id="9c44a-259">Questo servizio Elimina un'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-259">This service deletes a previously created DHCP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-260">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-260">Input Parameters</span></span>

- <span data-ttu-id="9c44a-261">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-261">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-262">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-262">Return Values</span></span>

- <span data-ttu-id="9c44a-263">**NX_SUCCESS**: (0x00) l'eliminazione DHCP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="9c44a-263">**NX_SUCCESS**: (0x00) Successful DHCP delete.</span></span>
- <span data-ttu-id="9c44a-264">NX_PTR_ERROR: (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-264">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="9c44a-265">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-265">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-266">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-266">Allowed From</span></span>

<span data-ttu-id="9c44a-267">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-267">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-268">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-268">Example</span></span>

```c
/* Delete a DHCP instance.  */
status =  nx_dhcp_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCP instance was successfully deleted.  */
```

## <a name="nx_dhcp_-force_renew"></a><span data-ttu-id="9c44a-269">nx_dhcp_ force_renew</span><span class="sxs-lookup"><span data-stu-id="9c44a-269">nx_dhcp_ force_renew</span></span>

<span data-ttu-id="9c44a-270">Invia un messaggio di rinnovo forzato</span><span class="sxs-lookup"><span data-stu-id="9c44a-270">Send a force renew message</span></span> 

### <a name="prototype"></a><span data-ttu-id="9c44a-271">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-271">Prototype</span></span>

```c
UINT nx_dhcp force_renew(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="9c44a-272">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-272">Description</span></span>

<span data-ttu-id="9c44a-273">Questo servizio consente all'applicazione host di inviare un messaggio di rinnovo forzato su tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-273">This service enables the host application to send a force renew message on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="9c44a-274">Il client DHCP deve trovarsi in uno stato associato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-274">The DHCP Client must be in a BOUND state.</span></span> <span data-ttu-id="9c44a-275">Questa funzione imposta lo stato su RENEW, in modo che il client DHCP tenterà di eseguire il rinnovo prima della scadenza del timeout T1.</span><span class="sxs-lookup"><span data-stu-id="9c44a-275">This function sets the state to RENEW such that the DHCP Client will try to renew before the T1 timeout expires.</span></span>

<span data-ttu-id="9c44a-276">Per inviare un rinnovo forzato a un'interfaccia specifica quando più interfacce sono abilitate per DHCP, usare *nx_dhcp_interface_force_renew*.</span><span class="sxs-lookup"><span data-stu-id="9c44a-276">To send a force renew on a specific interface when multiple interfaces are DHCP-enabled, use *nx_dhcp_interface_force_renew*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-277">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-277">Input Parameters</span></span>

- <span data-ttu-id="9c44a-278">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-278">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-279">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-279">Return Values</span></span>

- <span data-ttu-id="9c44a-280">**NX_SUCCESS**: (0x00) ha inviato il rinnovo forzato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-280">**NX_SUCCESS**: (0x00) Successfully sent force renew.</span></span>
- <span data-ttu-id="9c44a-281">**NX_DHCP_NOT_BOUND**: (0x94) indirizzo IP client non associato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-281">**NX_DHCP_NOT_BOUND**: (0x94) Client IP address not bound.</span></span>  
- <span data-ttu-id="9c44a-282">NX_PTR_ERROR: (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-282">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="9c44a-283">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-283">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-284">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-284">Allowed From</span></span>

<span data-ttu-id="9c44a-285">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-285">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-286">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-286">Example</span></span>

```c
/* Send a force renew message from the Client.  */
status =  nx_dhcp_force_renew(&my_dhcp);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired.  */
```

## <a name="nx_dhcp_interface_force_renew"></a><span data-ttu-id="9c44a-287">nx_dhcp_interface_force_renew</span><span class="sxs-lookup"><span data-stu-id="9c44a-287">nx_dhcp_interface_force_renew</span></span>

<span data-ttu-id="9c44a-288">Invia un messaggio Force Renew sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-288">Send a force renew message on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-289">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-289">Prototype</span></span>

```c
UINT nx_dhcp_interface_force_renew(NX_DHCP *dhcp_ptr, 
                                   UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="9c44a-290">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-290">Description</span></span>

<span data-ttu-id="9c44a-291">Questo servizio consente all'applicazione host di inviare un messaggio Force Renew sull'interfaccia di input purché tale interfaccia sia stata abilitata per DHCP (vedere *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="9c44a-291">This service enables the host application to send a force renew message on the input interface as long as that interface has been enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="9c44a-292">Il client DHCP nell'interfaccia specificata deve essere in uno stato associato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-292">The DHCP Client on the specified interface must be in a BOUND state.</span></span> <span data-ttu-id="9c44a-293">Questa funzione imposta lo stato su RENEW, in modo che il client DHCP tenterà di eseguire il rinnovo prima della scadenza del timeout T1.</span><span class="sxs-lookup"><span data-stu-id="9c44a-293">This function sets the state to RENEW such that the DHCP Client will try to renew before the T1 timeout expires.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-294">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-294">Input Parameters</span></span>

- <span data-ttu-id="9c44a-295">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-295">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-296">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-296">Return Values</span></span>

- <span data-ttu-id="9c44a-297">**NX_SUCCESS**: (0x00) ha inviato il rinnovo forzato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-297">**NX_SUCCESS**: (0x00) Successfully sent force renew.</span></span>  
- <span data-ttu-id="9c44a-298">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-298">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-299">NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-299">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>
- <span data-ttu-id="9c44a-300">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-300">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-301">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-301">Allowed From</span></span>

<span data-ttu-id="9c44a-302">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-302">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-303">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-303">Example</span></span>

```c
/* Send a force renew message to the server on interface 1.  */
status =  nx_dhcp_interface_force_renew(&my_dhcp, 1);


/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired.  */
```

## <a name="nx_dhcp_packet_pool_set"></a><span data-ttu-id="9c44a-304">nx_dhcp_packet_pool_set</span><span class="sxs-lookup"><span data-stu-id="9c44a-304">nx_dhcp_packet_pool_set</span></span>

<span data-ttu-id="9c44a-305">Impostare il pool di pacchetti client DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-305">Set the DHCP Client packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-306">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-306">Prototype</span></span>

```c
UINT nx_dhcp_packet_pool_set(NX_DHCP *dhcp_ptr, NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a><span data-ttu-id="9c44a-307">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-307">Description</span></span>

<span data-ttu-id="9c44a-308">Questo servizio consente all'applicazione di creare il pool di pacchetti client DHCP passando un puntatore a un pool di pacchetti creato in precedenza in questa chiamata al servizio.</span><span class="sxs-lookup"><span data-stu-id="9c44a-308">This service allows the application to create the DHCP Client packet pool by passing in a pointer to a previously created packet pool in this service call.</span></span> <span data-ttu-id="9c44a-309">Per utilizzare questa funzionalità, l'applicazione host deve definire NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL.</span><span class="sxs-lookup"><span data-stu-id="9c44a-309">To use this feature, the host application must define NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL.</span></span> <span data-ttu-id="9c44a-310">Una volta definito, il servizio *nx_dhcp_create* non creerà il pool di pacchetti del client.</span><span class="sxs-lookup"><span data-stu-id="9c44a-310">When defined, the *nx_dhcp_create* service will not create the Client’s packet pool.</span></span> 

>[!NOTE] 
> <span data-ttu-id="9c44a-311">Per l'applicazione è consigliabile utilizzare i valori predefiniti per il payload del pool di pacchetti client DHCP, definito come NX_DHCP_PACKET_PAYLOAD in *nxd_dhcp_client. h* quando si crea il pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9c44a-311">The application is recommended to use the default values for the DHCP client packet pool payload, defined as NX_DHCP_PACKET_PAYLOAD in *nxd_dhcp_client.h* when creating the packet pool.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-312">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-312">Input Parameters</span></span>

- <span data-ttu-id="9c44a-313">**dhcp_ptr**: puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-313">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="9c44a-314">**packet_pool_ptr**: puntatore al pool di pacchetti creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="9c44a-314">**packet_pool_ptr**: Pointer to previously created packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-315">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-315">Return Values</span></span>

- <span data-ttu-id="9c44a-316">**NX_SUCCESS**: (0x00) il pool di pacchetti client DHCP è impostato</span><span class="sxs-lookup"><span data-stu-id="9c44a-316">**NX_SUCCESS**: (0x00) DHCP Client packet pool is set</span></span>
- <span data-ttu-id="9c44a-317">**NX_NOT_ENABLED**: il servizio (0x14) non è abilitato</span><span class="sxs-lookup"><span data-stu-id="9c44a-317">**NX_NOT_ENABLED**: (0x14) Service is not enabled</span></span>
- <span data-ttu-id="9c44a-318">NX_PTR_ERROR: (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-318">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="9c44a-319">NX_DHCP_INVALID_PAYLOAD: il payload (0x9C) è troppo piccolo</span><span class="sxs-lookup"><span data-stu-id="9c44a-319">NX_DHCP_INVALID_PAYLOAD: (0x9C) Payload is too small</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-320">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-320">Allowed From</span></span>

<span data-ttu-id="9c44a-321">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9c44a-321">Application code</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-322">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-322">Example</span></span>

```c
/* Create the packet pool. */
status =  nx_packet_pool_create(&dhcp_pool, "DHCP Client Packet Pool", 
                                 NX_DHCP_PACKET_PAYLOAD, pointer, 
                                 (15 * NX_DHCP_PACKET_PAYLOAD));

/* Create the DHCP Client. */
status =  nx_dhcp_create(&dhcp_0, &ip_0, "janetsdhcp1");

/* Set the DHCP Client packet pool.  */
status =  nx_dhcp_packet_pool_set(&my_dhcp, packet_pool_ptr);
/* If status is NX_SUCCESS packet pool was successfully set.  */

```

## <a name="nx_dhcp_request_client_ip"></a><span data-ttu-id="9c44a-323">nx_dhcp_request_client_ip</span><span class="sxs-lookup"><span data-stu-id="9c44a-323">nx_dhcp_request_client_ip</span></span>

<span data-ttu-id="9c44a-324">Imposta l'indirizzo IP richiesto per l'istanza DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-324">Set requested IP address for DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-325">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-325">Prototype</span></span>

```c
UINT nx_dhcp_request_client_ip(NX_DHCP *dhcp_ptr, 
                               ULONG client_ip_address, 
                               UINT skip_discover_message);
```

### <a name="description"></a><span data-ttu-id="9c44a-326">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-326">Description</span></span>

<span data-ttu-id="9c44a-327">Questo servizio imposta l'indirizzo IP per il client DHCP da richiedere dal server DHCP sulla prima interfaccia abilitata per DHCP nel record client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-327">This service sets the IP address for the DHCP Client to request from the DHCP Server on the first interface enabled for DHCP in the DHCP Client record.</span></span> <span data-ttu-id="9c44a-328">Se viene impostato il flag di *skip_discover_message* , il client DHCP Ignora il messaggio di individuazione e invia un messaggio di richiesta.</span><span class="sxs-lookup"><span data-stu-id="9c44a-328">If the *skip_discover_message* flag is set, the DHCP Client skips the Discover message and sends a Request message.</span></span>

<span data-ttu-id="9c44a-329">Per impostare la richiesta per un indirizzo IP specifico per i messaggi DHCP in un'interfaccia specifica, usare il servizio *nx_dhcp_interface_request_client_ip* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-329">To set the request for a specific IP for DHCP messages on a specific interface, use the *nx_dhcp_interface_request_client_ip* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-330">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-330">Input Parameters</span></span>

- <span data-ttu-id="9c44a-331">**dhcp_ptr**: puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-331">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="9c44a-332">**client_ip_address**: indirizzo IP da richiedere dal server DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-332">**client_ip_address**: IP address to request from DHCP server</span></span>
- <span data-ttu-id="9c44a-333">**skip_discover_message**:</span><span class="sxs-lookup"><span data-stu-id="9c44a-333">**skip_discover_message**:</span></span> 
    - <span data-ttu-id="9c44a-334">Se true, il client DHCP invia un messaggio di richiesta</span><span class="sxs-lookup"><span data-stu-id="9c44a-334">If true, DHCP Client sends Request message</span></span>
    - <span data-ttu-id="9c44a-335">Se false, invia il messaggio di individuazione.</span><span class="sxs-lookup"><span data-stu-id="9c44a-335">If false, it sends the Discover message.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-336">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-336">Return Values</span></span>

- <span data-ttu-id="9c44a-337">**NX_SUCCESS**: (0x00) l'indirizzo IP richiesto è impostato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-337">**NX_SUCCESS**: (0x00) Requested IP address is set.</span></span>
- <span data-ttu-id="9c44a-338">NX_PTR_ERROR: (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-338">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="9c44a-339">NX_DHCP_INVALID_IP_REQUEST: (0x9D) indirizzo IP NULL richiesto</span><span class="sxs-lookup"><span data-stu-id="9c44a-339">NX_DHCP_INVALID_IP_REQUEST: (0x9D) NULL IP address requested</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-340">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-340">Allowed From</span></span>

<span data-ttu-id="9c44a-341">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-341">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-342">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-342">Example</span></span>

```c
/* Set the DHCP Client requested IP address and skip the discover message.  */

status =  nx_dhcp_request_client_ip(&my_dhcp, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set.  */

```

## <a name="nx_dhcp_interface_request_client_ip"></a><span data-ttu-id="9c44a-343">nx_dhcp_interface_request_client_ip</span><span class="sxs-lookup"><span data-stu-id="9c44a-343">nx_dhcp_interface_request_client_ip</span></span>

<span data-ttu-id="9c44a-344">Imposta l'indirizzo IP richiesto per l'istanza DHCP nell'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-344">Set requested IP address for DHCP instance on specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-345">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-345">Prototype</span></span>

```c
UINT nx_dhcp_interface_request_client_ip(NX_DHCP *dhcp_ptr, UINT  interface_index, 
                                         ULONG client_ip_address, UINT skip_discover_message);
```

### <a name="description"></a><span data-ttu-id="9c44a-346">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-346">Description</span></span>

<span data-ttu-id="9c44a-347">Questo servizio imposta l'indirizzo IP per il client DHCP da richiedere dal server DHCP sull'interfaccia specificata, se tale interfaccia è abilitata per DHCP (vedere *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="9c44a-347">This service sets the IP address for the DHCP Client to request from the DHCP Server on the specified interface, if that interface is enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="9c44a-348">Se viene impostato il flag di *skip_discover_message* , il client DHCP Ignora il messaggio di individuazione e invia un messaggio di richiesta.</span><span class="sxs-lookup"><span data-stu-id="9c44a-348">If the *skip_discover_message* flag is set, the DHCP Client skips the Discover message and sends a Request message.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-349">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-349">Input Parameters</span></span>

- <span data-ttu-id="9c44a-350">**dhcp_ptr**: puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-350">**dhcp_ptr**: Pointer to DHCP control block.</span></span>
- <span data-ttu-id="9c44a-351">**Interface_index**: Indice dell'interfaccia su cui richiedere l'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="9c44a-351">**Interface_index**: Index of interface to request IP address on</span></span>
- <span data-ttu-id="9c44a-352">**client_ip_address**: indirizzo IP da richiedere dal server DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-352">**client_ip_address**: IP address to request from DHCP server</span></span>
- <span data-ttu-id="9c44a-353">**skip_discover_message**: Se true, il client DHCP invia un messaggio di richiesta; in caso contrario, invia il messaggio di individuazione.</span><span class="sxs-lookup"><span data-stu-id="9c44a-353">**skip_discover_message**: If true, DHCP Client sends Request message; else it sends the Discover message.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-354">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-354">Return Values</span></span>

- <span data-ttu-id="9c44a-355">**NX_SUCCESS**: (0x00) l'indirizzo IP richiesto è impostato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-355">**NX_SUCCESS**: (0x00) Requested IP address is set.</span></span>
- <span data-ttu-id="9c44a-356">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-356">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-357">NX_PTR_ERROR: (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-357">NX_PTR_ERROR: (0x16) Invalid IP or DHCP pointer</span></span>
- <span data-ttu-id="9c44a-358">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-358">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-359">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-359">Allowed From</span></span>

<span data-ttu-id="9c44a-360">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-360">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-361">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-361">Example</span></span>

```c
/* Set the DHCP Client requested IP address and skip the discover message on  
   interface 0.  */
status =  nx_dhcp_interface_request_client_ip(&my_dhcp, 0, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set.  */
```

## <a name="nx_dhcp_reinitialize"></a><span data-ttu-id="9c44a-362">nx_dhcp_reinitialize</span><span class="sxs-lookup"><span data-stu-id="9c44a-362">nx_dhcp_reinitialize</span></span>

<span data-ttu-id="9c44a-363">Cancella i parametri della rete client DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-363">Clear the DHCP client network parameters</span></span> 

### <a name="prototype"></a><span data-ttu-id="9c44a-364">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-364">Prototype</span></span>

```c
UINT nx_dhcp_reinitialize(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="9c44a-365">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-365">Description</span></span>

<span data-ttu-id="9c44a-366">Questo servizio Cancella i parametri della rete dell'applicazione host (indirizzo IP, indirizzo di rete e network mask) e cancella lo stato del client DHCP in tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-366">This service clears the host application network parameters (IP address, network address and network mask), and clears the DHCP Client state on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="9c44a-367">Viene usato in combinazione con *nx_dhcp_stop* e *nx_dhcp_start* per "riavviare" la macchina a stati DHCP:</span><span class="sxs-lookup"><span data-stu-id="9c44a-367">It is used in combination with *nx_dhcp_stop* and *nx_dhcp_start* to ‘restart’ the DHCP state machine:</span></span>

```c
nx_dhcp_stop(&my_dhcp);
nx_dhcp_reinitialize(&my_dhcp);
nx_dhcp_start(&my_dhcp);
```

<span data-ttu-id="9c44a-368">Per reinizializzare il client DHCP in un'interfaccia specifica quando sono abilitate più interfacce per DHCP, usare il servizio *nx_dhcp_interface_reinitialize* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-368">To reinitialize the DHCP Client on a specific interface when multiple interfaces are enabled for DHCP, use the *nx_dhcp_interface_reinitialize* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-369">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-369">Input Parameters</span></span>

- <span data-ttu-id="9c44a-370">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-370">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-371">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-371">Return Values</span></span>

- <span data-ttu-id="9c44a-372">**NX_SUCCESS**: (0x00) il protocollo DHCP è stato reinizializzato</span><span class="sxs-lookup"><span data-stu-id="9c44a-372">**NX_SUCCESS**: (0x00) DHCP successfully reinitialized</span></span> 
- <span data-ttu-id="9c44a-373">NX_PTR_ERROR: (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-373">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-374">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-374">Allowed From</span></span>

<span data-ttu-id="9c44a-375">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-375">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-376">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-376">Example</span></span>

```c
/* Reinitialize the previously started DHCP client.  */
status =  nx_dhcp_reinitialize(&my_dhcp);

/* If status is NX_SUCCESS the host application successfully reinitialized its network parameters and DHCP client state. */
```

## <a name="nx_dhcp_interface_reinitialize"></a><span data-ttu-id="9c44a-377">nx_dhcp_interface_reinitialize</span><span class="sxs-lookup"><span data-stu-id="9c44a-377">nx_dhcp_interface_reinitialize</span></span>

<span data-ttu-id="9c44a-378">Cancella i parametri di rete del client DHCP nell'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-378">Clear the DHCP client network parameters on the specified interface</span></span> 

### <a name="prototype"></a><span data-ttu-id="9c44a-379">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-379">Prototype</span></span>

```c
UINT nx_dhcp_interface_reinitialize(NX_DHCP *dhcp_ptr, 
                                     UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="9c44a-380">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-380">Description</span></span>

<span data-ttu-id="9c44a-381">Questo servizio Cancella i parametri di rete (indirizzo IP, indirizzo di rete e network mask) nell'interfaccia specificata se tale interfaccia è abilitata per DHCP (vedere *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="9c44a-381">This service clears the network parameters (IP address, network address and network mask) on the specified interface if that interface is enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="9c44a-382">Per ulteriori informazioni, vedere *nx_dhcp_reinitialize* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-382">See *nx_dhcp_reinitialize* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-383">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-383">Input Parameters</span></span>

- <span data-ttu-id="9c44a-384">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza</span><span class="sxs-lookup"><span data-stu-id="9c44a-384">**dhcp_ptr**: Pointer to previously created DHCP instance</span></span>
- <span data-ttu-id="9c44a-385">**interface_index**: Indice dell'interfaccia da reinizializzare</span><span class="sxs-lookup"><span data-stu-id="9c44a-385">**interface_index**: Index of interface to reinitialize</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-386">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-386">Return Values</span></span>

- <span data-ttu-id="9c44a-387">**NX_SUCCESS**: (0x00) l'interfaccia è stata reinizializzata</span><span class="sxs-lookup"><span data-stu-id="9c44a-387">**NX_SUCCESS**: (0x00) Interface successfully reinitialized</span></span>
- <span data-ttu-id="9c44a-388">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-388">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-389">NX_PTR_ERROR: (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-389">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="9c44a-390">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-390">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="9c44a-391">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-391">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-392">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-392">Allowed From</span></span>

<span data-ttu-id="9c44a-393">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-393">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-394">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-394">Example</span></span>

```c
/* Reinitialize the previously started DHCP client on interface 1.  */
status =  nx_dhcp_interface_reinitialize(&my_dhcp, 1);

/* If status is NX_SUCCESS the host application successfully reinitialized its network parameters and DHCP client state. */
```

## <a name="nx_dhcp_release"></a><span data-ttu-id="9c44a-395">nx_dhcp_release</span><span class="sxs-lookup"><span data-stu-id="9c44a-395">nx_dhcp_release</span></span>

<span data-ttu-id="9c44a-396">Rilascia indirizzo IP con lease</span><span class="sxs-lookup"><span data-stu-id="9c44a-396">Release Leased IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-397">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-397">Prototype</span></span>

```c
UINT nx_dhcp_release(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="9c44a-398">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-398">Description</span></span>

<span data-ttu-id="9c44a-399">Questo servizio rilascia l'indirizzo IP ottenuto da un server DHCP inviando il messaggio di rilascio a tale server.</span><span class="sxs-lookup"><span data-stu-id="9c44a-399">This service releases the IP address obtained from a DHCP server by sending the RELEASE message to that server.</span></span> <span data-ttu-id="9c44a-400">Quindi reinizializza il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-400">It then reinitializes the DHCP Client.</span></span> <span data-ttu-id="9c44a-401">Questo servizio viene applicato a tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-401">This service is applied to all interfaces enabled for DHCP.</span></span>

<span data-ttu-id="9c44a-402">L'applicazione può riavviare il client DHCP chiamando *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="9c44a-402">The application can restart the DHCP Client by calling *nx_dhcp_start*.</span></span>

<span data-ttu-id="9c44a-403">Per rilasciare un indirizzo al server DHCP in un'interfaccia specifica, usare il servizio *nx_dhcp_interface_release*</span><span class="sxs-lookup"><span data-stu-id="9c44a-403">To release an address back to the DHCP server on a specific interface, use the *nx_dhcp_interface_release* service</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-404">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-404">Input Parameters</span></span>

- <span data-ttu-id="9c44a-405">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-405">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-406">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-406">Return Values</span></span>

- <span data-ttu-id="9c44a-407">**NX_SUCCESS**: (0x00) versione DHCP riuscita.</span><span class="sxs-lookup"><span data-stu-id="9c44a-407">**NX_SUCCESS**: (0x00) Successful DHCP release.</span></span>  
- <span data-ttu-id="9c44a-408">**NX_DHCP_NOT_BOUND**: (0X94) l'indirizzo IP non è stato concesso in lease, quindi non può essere rilasciato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-408">**NX_DHCP_NOT_BOUND**: (0x94) The IP address has not been leased so it can’t be released.</span></span>
- <span data-ttu-id="9c44a-409">NX_PTR_ERROR: (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-409">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="9c44a-410">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-410">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-411">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-411">Allowed From</span></span>

<span data-ttu-id="9c44a-412">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-412">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-413">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-413">Example</span></span>

```c
/* Release the previously leased IP address.  */
status =  nx_dhcp_release(&my_dhcp);

/* If status is NX_SUCCESS the previous IP lease was successfully released.  */
```

## <a name="nx_dhcp_interface_release"></a><span data-ttu-id="9c44a-414">nx_dhcp_interface_release</span><span class="sxs-lookup"><span data-stu-id="9c44a-414">nx_dhcp_interface_release</span></span>

<span data-ttu-id="9c44a-415">Rilasciare l'indirizzo IP sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-415">Release IP address on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-416">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-416">Prototype</span></span>

```c
UINT nx_dhcp_interface_release(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="9c44a-417">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-417">Description</span></span>

<span data-ttu-id="9c44a-418">Questo servizio rilascia l'indirizzo IP ottenuto da un server DHCP sull'interfaccia specificata e reinizializza il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-418">This service releases the IP address obtained from a DHCP server on the specified interface and reinitializes the DHCP Client.</span></span> <span data-ttu-id="9c44a-419">Il client DHCP può essere riavviato chiamando *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="9c44a-419">The DHCP Client can be restarted by calling *nx_dhcp_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-420">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-420">Input Parameters</span></span>

- <span data-ttu-id="9c44a-421">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-421">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-422">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-422">Return Values</span></span>

- <span data-ttu-id="9c44a-423">**NX_SUCCESS**: (0x00) versione DHCP riuscita.</span><span class="sxs-lookup"><span data-stu-id="9c44a-423">**NX_SUCCESS**: (0x00) Successful DHCP release.</span></span>
- <span data-ttu-id="9c44a-424">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-424">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-425">**NX_DHCP_NOT_BOUND**: (0X94) l'indirizzo IP non è stato concesso in lease, quindi non può essere rilasciato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-425">**NX_DHCP_NOT_BOUND**: (0x94) The IP address has not been leased so it can’t be released.</span></span>
- <span data-ttu-id="9c44a-426">NX_PTR_ERROR: (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-426">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="9c44a-427">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-427">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="9c44a-428">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-428">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-429">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-429">Allowed From</span></span>

<span data-ttu-id="9c44a-430">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-430">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-431">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-431">Example</span></span>

```c
/* Release the previously leased IP address on interface 1.  */
status =  nx_dhcp_interface_release(&my_dhcp, 1);

/* If status is NX_SUCCESS the previous IP lease was successfully released.  */
```

## <a name="nx_dhcp_decline"></a><span data-ttu-id="9c44a-432">nx_dhcp_decline</span><span class="sxs-lookup"><span data-stu-id="9c44a-432">nx_dhcp_decline</span></span>

<span data-ttu-id="9c44a-433">Rifiuta indirizzo IP dal server DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-433">Decline IP address from DHCP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-434">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-434">Prototype</span></span>

```c
UINT nx_dhcp_decline(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="9c44a-435">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-435">Description</span></span>

<span data-ttu-id="9c44a-436">Questo servizio rifiuta un indirizzo IP con lease dal server DHCP in tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-436">This service declines an IP address leased from the DHCP server on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="9c44a-437">Se viene definito NX_DHCP_CLIENT_ SEND_ ARP_PROBE, il client DHCP invierà un messaggio di rifiuto se rileva che l'indirizzo IP è già in uso.</span><span class="sxs-lookup"><span data-stu-id="9c44a-437">If NX_DHCP_CLIENT_ SEND_ ARP_PROBE is defined, the DHCP Client will send a DECLINE message if it detects that the IP address is already in use.</span></span> <span data-ttu-id="9c44a-438">Per ulteriori informazioni sulla configurazione del probe ARP nel client DHCP NetX Duo, vedere **Probe ARP** nel capitolo 1.</span><span class="sxs-lookup"><span data-stu-id="9c44a-438">See **ARP Probes** in Chapter One for more information on ARP probe configuration in the NetX Duo DHCP Client.</span></span>

<span data-ttu-id="9c44a-439">L'applicazione può utilizzare questo servizio per rifiutare il proprio indirizzo IP se rileva che l'indirizzo è in uso in altri modi.</span><span class="sxs-lookup"><span data-stu-id="9c44a-439">The application can use this service to decline its IP address if it discovers the address is in use by other means.</span></span>

<span data-ttu-id="9c44a-440">Questo servizio reinizializza il client DHCP in modo che possa essere riavviato chiamando *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="9c44a-440">This service reinitializes the DHCP Client to that it can be restarted by calling *nx_dhcp_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-441">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-441">Input Parameters</span></span>

- <span data-ttu-id="9c44a-442">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-442">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-443">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-443">Return Values</span></span>

- <span data-ttu-id="9c44a-444">**NX_SUCCESS**: (0x00) il rifiuto è stato inviato</span><span class="sxs-lookup"><span data-stu-id="9c44a-444">**NX_SUCCESS**: (0x00) Decline successfully sent</span></span>  
- <span data-ttu-id="9c44a-445">**NX_DHCP_NOT_BOUND**: (0X94) client DHCP non associato</span><span class="sxs-lookup"><span data-stu-id="9c44a-445">**NX_DHCP_NOT_BOUND**: (0x94) DHCP Client not bound</span></span>
- <span data-ttu-id="9c44a-446">NX_PTR_ERROR: (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-446">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="9c44a-447">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-447">NX_CALLER_ERROR: (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-448">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-448">Allowed From</span></span>

<span data-ttu-id="9c44a-449">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-449">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-450">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-450">Example</span></span>

```c

/* Decline the IP address offered by the DHCP server.  */
status =  nx_dhcp_decline(&my_dhcp);

/* If status is NX_SUCCESS the previous IP address decline message was successfully trasnmitted.  */
```

## <a name="nx_dhcp_interface_decline"></a><span data-ttu-id="9c44a-451">nx_dhcp_interface_decline</span><span class="sxs-lookup"><span data-stu-id="9c44a-451">nx_dhcp_interface_decline</span></span>

<span data-ttu-id="9c44a-452">Rifiutare l'indirizzo IP dal server DHCP sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-452">Decline IP address from DHCP Server on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-453">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-453">Prototype</span></span>

```c
UINT nx_dhcp_interface_decline(NX_DHCP *dhcp_ptr, 
                               UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="9c44a-454">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-454">Description</span></span>

<span data-ttu-id="9c44a-455">Questo servizio invia il messaggio di rifiuto al server per rifiutare un indirizzo IP assegnato dal server DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-455">This service sends the DECLINE message to the server to decline an IP address assigned by the DHCP server.</span></span> <span data-ttu-id="9c44a-456">Reinizializza inoltre il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-456">It also reinitializes the DHCP Client.</span></span> <span data-ttu-id="9c44a-457">Per ulteriori informazioni, vedere *nx_dhcp_decline* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-457">See *nx_dhcp_decline* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-458">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-458">Input Parameters</span></span>

- <span data-ttu-id="9c44a-459">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-459">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="9c44a-460">**Interface_index**: Indice dell'interfaccia per rifiutare l'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="9c44a-460">**Interface_index**: Index of interface to decline IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-461">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-461">Return Values</span></span>

- <span data-ttu-id="9c44a-462">**NX_SUCCESS**: (0x00) messaggio di rifiuto DHCP inviato</span><span class="sxs-lookup"><span data-stu-id="9c44a-462">**NX_SUCCESS**: (0x00) DHCP decline message sent</span></span>  
- <span data-ttu-id="9c44a-463">**NX_DHCP_NOT_BOUND**: (0X94) client DHCP non associato</span><span class="sxs-lookup"><span data-stu-id="9c44a-463">**NX_DHCP_NOT_BOUND**: (0x94) DHCP Client not bound</span></span>
- <span data-ttu-id="9c44a-464">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-464">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-465">NX_PTR_ERROR: (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-465">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="9c44a-466">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-466">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="9c44a-467">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-467">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-468">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-468">Allowed From</span></span>

<span data-ttu-id="9c44a-469">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-469">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-470">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-470">Example</span></span>

```c
/* Decline the IP address offered by the DHCP server on interface 2.  */
status =  nx_dhcp_interface_decline(&my_dhcp, 2);

/* If status is NX_SUCCESS the previous IP address decline message was successfully trasnmitted.  */
```
## <a name="nx_dhcp_send_request"></a><span data-ttu-id="9c44a-471">nx_dhcp_send_request</span><span class="sxs-lookup"><span data-stu-id="9c44a-471">nx_dhcp_send_request</span></span>

<span data-ttu-id="9c44a-472">Invia messaggio DHCP al server</span><span class="sxs-lookup"><span data-stu-id="9c44a-472">Send DHCP message to Server</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-473">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-473">Prototype</span></span>

```c
UINT nx_dhcp_send_request(NX_DHCP *dhcp_ptr, UINT dhcp_message_type);

```

### <a name="description"></a><span data-ttu-id="9c44a-474">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-474">Description</span></span>

<span data-ttu-id="9c44a-475">Questo servizio invia il messaggio DHCP specificato al server DHCP nella prima interfaccia abilitata per DHCP trovato nel record client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-475">This service sends the specified DHCP message to the DHCP server on the first interface enabled for DHCP found in the DHCP Client record.</span></span> <span data-ttu-id="9c44a-476">Per inviare un messaggio di rilascio o di rifiuto, l'applicazione deve utilizzare rispettivamente i servizi di *nx_dhcp [_interface] _Release*() o *nx_dhcp_interface_decline ()* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-476">To send a RELEASE or DECLINE message, the application must use the *nx_dhcp[_interface]_release*() or *nx_dhcp_interface_decline()* services respectively.</span></span>

<span data-ttu-id="9c44a-477">È necessario avviare il client DHCP per l'utilizzo di questo servizio, ad eccezione dell'invio del INFORM_REQUEST tipo di messaggio.</span><span class="sxs-lookup"><span data-stu-id="9c44a-477">The DHCP Client must be started to use this service except for sending the INFORM_REQUEST message type.</span></span>

>[!NOTE]
> <span data-ttu-id="9c44a-478">Questo servizio non è destinato all'applicazione host a "unità" della macchina a stati client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-478">This service is not intended for the host application to ‘drive’ the DHCP Client state machine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-479">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-479">Input Parameters</span></span>

- <span data-ttu-id="9c44a-480">**dhcp_ptr**: puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-480">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="9c44a-481">**dhcp_message_type**: richiesta messaggio (definita in *nxd_dhcp_client. h*)</span><span class="sxs-lookup"><span data-stu-id="9c44a-481">**dhcp_message_type**: Message request (defined in *nxd_dhcp_client.h*)</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-482">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-482">Return Values</span></span>

- <span data-ttu-id="9c44a-483">**NX_SUCCESS**: (0x00) messaggio DHCP inviato</span><span class="sxs-lookup"><span data-stu-id="9c44a-483">**NX_SUCCESS**: (0x00) DHCP message sent</span></span>  
- <span data-ttu-id="9c44a-484">**NX_DHCP_NOT_STARTED**: (0x96) indice di interfaccia non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-484">**NX_DHCP_NOT_STARTED**: (0x96) Invalid interface index</span></span>
- <span data-ttu-id="9c44a-485">**NX_DHCP_INVALID_MESSAGE**: (0x9B) tipo di messaggio non valido da inviare</span><span class="sxs-lookup"><span data-stu-id="9c44a-485">**NX_DHCP_INVALID_MESSAGE**: (0x9B) Invalid message type to send</span></span>
- <span data-ttu-id="9c44a-486">NX_PTR_ERROR: (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-486">NX_PTR_ERROR: (0x16) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-487">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-487">Allowed From</span></span>

<span data-ttu-id="9c44a-488">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-488">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-489">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-489">Example</span></span>

```c
/* Send the DHCP INFORM REQUEST message to the server.  */

status =  nx_dhcp_send_request(&my_dhcp, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent.  */
```

## <a name="nx_dhcp_interface_send_request"></a><span data-ttu-id="9c44a-490">nx_dhcp_interface_send_request</span><span class="sxs-lookup"><span data-stu-id="9c44a-490">nx_dhcp_interface_send_request</span></span>

<span data-ttu-id="9c44a-491">Invia messaggio DHCP al server in un'interfaccia specifica</span><span class="sxs-lookup"><span data-stu-id="9c44a-491">Send DHCP message to Server on a specific interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-492">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-492">Prototype</span></span>

```c
UINT nx_dhcp_interface_send_request(NX_DHCP *dhcp_ptr, 
                                    UINT interface_index, 
                                    UINT dhcp_message_type);
```

### <a name="description"></a><span data-ttu-id="9c44a-493">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-493">Description</span></span>

<span data-ttu-id="9c44a-494">Questo servizio invia un messaggio al server DHCP sull'interfaccia specificata se tale interfaccia è abilitata per DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-494">This service sends a message to the DHCP server on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="9c44a-495">Per inviare un messaggio di rilascio o di rifiuto, l'applicazione deve utilizzare rispettivamente i servizi di *nx_dhcp [_interface] _Release*() o *nx_dhcp_interface_decline ()* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-495">To send a RELEASE or DECLINE message, the application must use the *nx_dhcp[_interface]_release*() or *nx_dhcp_interface_decline()* services respectively.</span></span>

<span data-ttu-id="9c44a-496">È necessario avviare il client DHCP per l'utilizzo di questo servizio, ad eccezione dell'invio del tipo di messaggio di richiesta di comunicazione DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-496">The DHCP Client must be started to use this service except for sending the DHCP INFORM REQUEST message type.</span></span>

<span data-ttu-id="9c44a-497">Questo servizio non è destinato all'applicazione host a "unità" della macchina a stati client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-497">This service is not intended for the host application to ‘drive’ the DHCP Client state machine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-498">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-498">Input Parameters</span></span>

- <span data-ttu-id="9c44a-499">**dhcp_ptr**: puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-499">**dhcp_ptr**: Pointer to DHCP control block.</span></span>
- <span data-ttu-id="9c44a-500">**Interface_index**: Indice dell'interfaccia su cui inviare il messaggio</span><span class="sxs-lookup"><span data-stu-id="9c44a-500">**Interface_index**: Index of interface to send message on</span></span>
- <span data-ttu-id="9c44a-501">**dhcp_message_type**: richiesta messaggio (definita in nxd_dhcp_client. h)</span><span class="sxs-lookup"><span data-stu-id="9c44a-501">**dhcp_message_type**: Message request (defined in nxd_dhcp_client.h)</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-502">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-502">Return Values</span></span>

- <span data-ttu-id="9c44a-503">**NX_SUCCESS**: (0x00) messaggio DHCP inviato</span><span class="sxs-lookup"><span data-stu-id="9c44a-503">**NX_SUCCESS**: (0x00) DHCP message sent</span></span>  
- <span data-ttu-id="9c44a-504">**NX_DHCP_NOT_STARTED**: (0x96) indice di interfaccia non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-504">**NX_DHCP_NOT_STARTED**: (0x96) Invalid interface index</span></span>
- <span data-ttu-id="9c44a-505">**NX_DHCP_INVALID_MESSAGE**: (0x9B) tipo di messaggio non valido da inviare</span><span class="sxs-lookup"><span data-stu-id="9c44a-505">**NX_DHCP_INVALID_MESSAGE**: (0x9B) Invalid message type to send</span></span>
- <span data-ttu-id="9c44a-506">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED**: (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-506">**NX_DHCP_INTERFACE_NOT_ENABLED**: (0xA4) Interface not enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-507">NX_PTR_ERROR: (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-507">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="9c44a-508">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-508">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="9c44a-509">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-509">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-510">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-510">Allowed From</span></span>

<span data-ttu-id="9c44a-511">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-511">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-512">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-512">Example</span></span>

```c
/* Send the INFORM REQUEST message to the server on the primary interface.  */

status =  nx_dhcp_interface_send_request(&my_dhcp, 0, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent.  */
```

## <a name="nx_dhcp_server_address_get"></a><span data-ttu-id="9c44a-513">nx_dhcp_server_address_get</span><span class="sxs-lookup"><span data-stu-id="9c44a-513">nx_dhcp_server_address_get</span></span>

<span data-ttu-id="9c44a-514">Ottenere l'indirizzo IP del server DHCP del client DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-514">Get the DHCP Client’s DHCP server IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-515">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-515">Prototype</span></span>

```c
UINT nx_dhcp_server_address_get(NX_DHCP *dhcp_ptr, 
                                ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="9c44a-516">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-516">Description</span></span>

<span data-ttu-id="9c44a-517">Questo servizio recupera l'indirizzo IP del server DHCP client DHCP nella prima interfaccia abilitata per DHCP trovato nel record client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-517">This service retrieves the DHCP Client DHCP server IP address on the first interface enabled for DHCP found in the DHCP Client record.</span></span> <span data-ttu-id="9c44a-518">Il chiamante può utilizzare questo servizio solo dopo che il client DHCP è associato a un indirizzo IP assegnato dal server DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-518">The caller can only use this service after the DHCP Client is bound to an IP address assigned by the DHCP Server.</span></span> <span data-ttu-id="9c44a-519">L'applicazione host può usare il servizio *nx_ip_status_check* per verificare che l'indirizzo IP sia impostato oppure è possibile usare il *_dhcp_state_change_notify* NX ed eseguire query sullo stato del client DHCP NX_DHCP_STATE_BOUND.</span><span class="sxs-lookup"><span data-stu-id="9c44a-519">The host application can use the *nx_ip_status_check* service to verify IP address is set, or it can use the nx *_dhcp_state_change_notify* and query the DHCP Client state is NX_DHCP_STATE_BOUND.</span></span> <span data-ttu-id="9c44a-520">Per ulteriori informazioni sull'impostazione della funzione di callback di modifica dello stato, vedere *nx_dhcp_state_change_notify* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-520">See *nx_dhcp_state_change_notify* for more details about setting the state change callback function.</span></span>

<span data-ttu-id="9c44a-521">Per trovare il server DHCP in un'interfaccia specifica quando sono abilitate più interfacce per il client DHCP, usare il servizio *nx_dhcp_interface_server_address_get*</span><span class="sxs-lookup"><span data-stu-id="9c44a-521">To find the DHCP server on a specific interface when multiple interfaces are enabled for DHCP Client, use the *nx_dhcp_interface_server_address_get* service</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-522">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-522">Input Parameters</span></span>

- <span data-ttu-id="9c44a-523">**dhcp_ptr**: puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-523">**dhcp_ptr**: Pointer to DHCP control block.</span></span>
- <span data-ttu-id="9c44a-524">**server_address**: puntatore all'indirizzo IP del server</span><span class="sxs-lookup"><span data-stu-id="9c44a-524">**server_address**: Pointer to server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-525">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-525">Return Values</span></span>

- <span data-ttu-id="9c44a-526">**NX_SUCCESS**: (0x00) indirizzo server DHCP restituito</span><span class="sxs-lookup"><span data-stu-id="9c44a-526">**NX_SUCCESS**: (0x00) DHCP server address returned</span></span>
- <span data-ttu-id="9c44a-527">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) non sono abilitate interfacce per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-527">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) No interfaces enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-528">NX_PTR_ERROR: (0x16) puntatore di input non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-528">NX_PTR_ERROR: (0x16) Invalid input pointer</span></span>
- <span data-ttu-id="9c44a-529">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-529">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-530">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-530">Allowed From</span></span>

<span data-ttu-id="9c44a-531">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-531">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-532">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-532">Example</span></span>

```c
/* Use the state change notify service to determine the Client transition to the bound state and get its DHCP server IP address.*/

void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{
ULONG server_address;
UINT  status;

/* Increment state changes counter.  */
state_changes++;

if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
        {
            status = nx_dhcp_server_address_get(&dhcp_0, &server_address);
        }

}
```

## <a name="nx_dhcp_interface_server_address_get"></a><span data-ttu-id="9c44a-533">nx_dhcp_interface_server_address_get</span><span class="sxs-lookup"><span data-stu-id="9c44a-533">nx_dhcp_interface_server_address_get</span></span>

<span data-ttu-id="9c44a-534">Ottenere l'indirizzo IP del server DHCP del client DHCP nell'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-534">Get the DHCP Client’s DHCP server IP address on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-535">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-535">Prototype</span></span>

```c
UINT nx_dhcp_interface_server_address_get(NX_DHCP *dhcp_ptr, 
                                          UINT interface_index,
                                          ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="9c44a-536">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-536">Description</span></span>

<span data-ttu-id="9c44a-537">Questo servizio recupera l'indirizzo IP del server DHCP client DHCP nell'interfaccia specificata se tale interfaccia è abilitata per DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-537">This service retrieves the DHCP Client DHCP server IP address on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="9c44a-538">Il client DHCP deve essere nello stato associato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-538">The DHCP Client must be in the Bound state.</span></span> <span data-ttu-id="9c44a-539">Dopo l'avvio del client DHCP su tale interfaccia, l'applicazione host può utilizzare il servizio *nx_ip_status_check* per verificare che l'indirizzo IP sia impostato oppure utilizzare il callback di modifica dello stato del client DHCP ed eseguire una query sullo stato del client DHCP NX_DHCP_STATE_BOUND.</span><span class="sxs-lookup"><span data-stu-id="9c44a-539">After starting the DHCP Client on that interface, the host application can either use the *nx_ip_status_check* service to verify the IP address is set, or it can use the DHCP Client state change callback and query the DHCP Client state is NX_DHCP_STATE_BOUND.</span></span> <span data-ttu-id="9c44a-540">Per ulteriori informazioni sull'impostazione della funzione di callback di modifica dello stato, vedere *nx_dhcp_state_change_notify* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-540">See *nx_dhcp_state_change_notify* for more details about setting the state change callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-541">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-541">Input Parameters</span></span>

- <span data-ttu-id="9c44a-542">**dhcp_ptr**: puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-542">**dhcp_ptr**: Pointer to DHCP control block.</span></span>
- <span data-ttu-id="9c44a-543">**Interface_index**: Indice dell'interfaccia per ottenere l'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="9c44a-543">**Interface_index**: Index of interface to obtain IP address</span></span>
- <span data-ttu-id="9c44a-544">**server_address**: puntatore all'indirizzo IP del server</span><span class="sxs-lookup"><span data-stu-id="9c44a-544">**server_address**: Pointer to server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-545">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-545">Return Values</span></span>

- <span data-ttu-id="9c44a-546">**NX_SUCCESS**: (0x00) indirizzo server DHCP restituito</span><span class="sxs-lookup"><span data-stu-id="9c44a-546">**NX_SUCCESS**: (0x00) DHCP server address returned</span></span>
- <span data-ttu-id="9c44a-547">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) non sono abilitate interfacce per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-547">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) No interfaces enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-548">**NX_DHCP_NOT_BOUND**: (0X94) client DHCP non associato</span><span class="sxs-lookup"><span data-stu-id="9c44a-548">**NX_DHCP_NOT_BOUND**: (0x94) DHCP Client not bound</span></span>
- <span data-ttu-id="9c44a-549">NX_PTR_ERROR: (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-549">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>
- <span data-ttu-id="9c44a-550">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-550">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>
- <span data-ttu-id="9c44a-551">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-551">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-552">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-552">Allowed From</span></span>

<span data-ttu-id="9c44a-553">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-553">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-554">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-554">Example</span></span>

```c
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. */

void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter.  */
state_changes++;

/* Get the DHCP server IP address on interface 1 */
if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
        {
         status = nx_dhcp_interface_server_address_get(&dhcp_0, 1, 
                                                       &server_address);
        }
}
```

## <a name="nx_dhcp_set_interface_index"></a><span data-ttu-id="9c44a-555">nx_dhcp_set_interface_index</span><span class="sxs-lookup"><span data-stu-id="9c44a-555">nx_dhcp_set_interface_index</span></span>

<span data-ttu-id="9c44a-556">Impostare l'interfaccia di rete per l'istanza DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-556">Set network interface for DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-557">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-557">Prototype</span></span>

```c
UINT nx_dhcp_set_interface_index(NX_DHCP *dhcp_ptr, UINT index);
```

### <a name="description"></a><span data-ttu-id="9c44a-558">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-558">Description</span></span>

<span data-ttu-id="9c44a-559">Questo servizio imposta l'interfaccia di rete per l'istanza DHCP per la connessione al server DHCP in quando viene eseguito il client DHCP configurato per una singola interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="9c44a-559">This service sets the network interface for the DHCP instance to connect to the DHCP Server on when running DHCP Client configured for a single network interface.</span></span>

<span data-ttu-id="9c44a-560">Per impostazione predefinita, il client DHCP viene eseguito sull'interfaccia principale.</span><span class="sxs-lookup"><span data-stu-id="9c44a-560">By default the DHCP Client runs on the primary interface.</span></span> <span data-ttu-id="9c44a-561">Per eseguire DHCP in un servizio secondario, utilizzare questo servizio per impostare l'interfaccia secondaria come interfaccia client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-561">To run DHCP on a secondary service, use this service to set the secondary interface as the DHCP Client interface.</span></span> <span data-ttu-id="9c44a-562">In precedenza, l'applicazione deve registrare l'interfaccia specificata nell'istanza IP utilizzando il servizio *nx_ip_interface_attach* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-562">The application must previously register the specified interface to the IP instance using the *nx_ip_interface_attach* service.</span></span>

>[!NOTE]
> <span data-ttu-id="9c44a-563">Questo servizio è destinato alle applicazioni che intendono eseguire il client DHCP su una sola interfaccia.</span><span class="sxs-lookup"><span data-stu-id="9c44a-563">This service is intended for applications that intend to run the DHCP Client on only one interface.</span></span> <span data-ttu-id="9c44a-564">Per eseguire DHCP su più interfacce, vedere *nx_dhcp_interface_enable* per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="9c44a-564">To run DHCP on multiple interfaces see *nx_dhcp_interface_enable* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-565">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-565">Input Parameters</span></span>

- <span data-ttu-id="9c44a-566">**dhcp_ptr**: puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-566">**dhcp_ptr**: Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="9c44a-567">**index**: Indice dell'interfaccia di rete del dispositivo</span><span class="sxs-lookup"><span data-stu-id="9c44a-567">**index**: Index of device network interface</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-568">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-568">Return Values</span></span>

- <span data-ttu-id="9c44a-569">L'interfaccia **NX_SUCCESS**: (0x00) è stata impostata correttamente.</span><span class="sxs-lookup"><span data-stu-id="9c44a-569">**NX_SUCCESS**: (0x00) Interface is successfully set.</span></span>
- <span data-ttu-id="9c44a-570">**NX_INVALID_INTERFACE**: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-570">**NX_INVALID_INTERFACE**: (0x4C) Invalid network interface</span></span>
- <span data-ttu-id="9c44a-571">Interfaccia **NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-571">**NX_DHCP_INTERFACE_ALREADY_ENABLED**: (0xA3) Interface enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-572">**NX_DHCP_NO_RECORDS_AVAILABLE**: (0XA7) nessun record disponibile per un altro</span><span class="sxs-lookup"><span data-stu-id="9c44a-572">**NX_DHCP_NO_RECORDS_AVAILABLE**: (0xA7) No record available for another</span></span> 
- <span data-ttu-id="9c44a-573">NX_PTR_ERROR: (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="9c44a-573">NX_PTR_ERROR: (0x16) Invalid DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-574">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-574">Allowed From</span></span>

<span data-ttu-id="9c44a-575">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-575">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-576">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-576">Example</span></span>

```c
/* Set the DHCP Client interface to the secondary interface (index 1).  */
status =  nx_dhcp_set_interface_index(&my_dhcp, 1);
/* If status is NX_SUCCESS a DHCP interface was successfully set.  */
```

## <a name="nx_dhcp_start"></a><span data-ttu-id="9c44a-577">nx_dhcp_start</span><span class="sxs-lookup"><span data-stu-id="9c44a-577">nx_dhcp_start</span></span>

<span data-ttu-id="9c44a-578">Avviare l'elaborazione DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-578">Start DHCP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-579">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-579">Prototype</span></span>

```c
UINT nx_dhcp_start(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="9c44a-580">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-580">Description</span></span>

<span data-ttu-id="9c44a-581">Questo servizio avvia l'elaborazione DHCP su tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-581">This service starts DHCP processing on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="9c44a-582">Per impostazione predefinita, l'interfaccia primaria è abilitata per DHCP quando l'applicazione chiama *nx_dhcp_create.*</span><span class="sxs-lookup"><span data-stu-id="9c44a-582">By default the primary interface is enabled for DHCP when the application calls *nx_dhcp_create.*</span></span>

<span data-ttu-id="9c44a-583">Per verificare quando l'istanza IP è associata a un indirizzo IP sull'interfaccia client DHCP, usare *nx_ip_status_check* per vedere Verificare che l'indirizzo IP sia valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-583">To verify when the IP instance is bound to an IP address on the DHCP Client interface, use *nx_ip_status_check* to see confirm the IP address is valid.</span></span>

<span data-ttu-id="9c44a-584">Se sono presenti altre interfacce che eseguono già DHCP, il servizio non le influirà.</span><span class="sxs-lookup"><span data-stu-id="9c44a-584">If there are other interfaces already running DHCP, this service will not affect them.</span></span>

<span data-ttu-id="9c44a-585">Per avviare DHCP in un'interfaccia specifica quando sono abilitate più interfacce, usare il servizio *nx_dhcp_interface_start* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-585">To start DHCP on a specific interface when multiple interfaces are enabled, use the *nx_dhcp_interface_start* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-586">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-586">Input Parameters</span></span>

- <span data-ttu-id="9c44a-587">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-587">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-588">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-588">Return Values</span></span>

- <span data-ttu-id="9c44a-589">**NX_SUCCESS**: (0x00) avvio DHCP riuscito.</span><span class="sxs-lookup"><span data-stu-id="9c44a-589">**NX_SUCCESS**: (0x00) Successful DHCP start.</span></span>  
- <span data-ttu-id="9c44a-590">**NX_DHCP_ALREADY_STARTED**: (0X93) DHCP è già avviato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-590">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP already started.</span></span>
- <span data-ttu-id="9c44a-591">NX_PTR_ERROR: (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-591">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="9c44a-592">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-592">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-593">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-593">Allowed From</span></span>

<span data-ttu-id="9c44a-594">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-594">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-595">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-595">Example</span></span>

```c
/* Start the DHCP processing for this IP instance.  */
status =  nx_dhcp_start(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully started.  */
```

## <a name="nx_dhcp_interface_start"></a><span data-ttu-id="9c44a-596">nx_dhcp_interface_start</span><span class="sxs-lookup"><span data-stu-id="9c44a-596">nx_dhcp_interface_start</span></span>

<span data-ttu-id="9c44a-597">Avvia elaborazione DHCP sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-597">Start DHCP processing on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-598">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-598">Prototype</span></span>

```c
UINT nx_dhcp_interface_start(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="9c44a-599">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-599">Description</span></span>

<span data-ttu-id="9c44a-600">Questo servizio avvia l'elaborazione DHCP sull'interfaccia specificata se tale interfaccia è abilitata per DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-600">This service starts DHCP processing on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="9c44a-601">Per ulteriori informazioni sull'abilitazione di un'interfaccia per DHCP, vedere *nx_dhcp_interface_enable*().</span><span class="sxs-lookup"><span data-stu-id="9c44a-601">See *nx_dhcp_interface_enable*() for more details about enabling an interface for DHCP.</span></span> <span data-ttu-id="9c44a-602">Per impostazione predefinita, l'interfaccia primaria è abilitata per DHCP quando l'applicazione chiama *nx_dhcp_create.*</span><span class="sxs-lookup"><span data-stu-id="9c44a-602">By default the primary interface is enabled for DHCP when the application calls *nx_dhcp_create.*</span></span>

<span data-ttu-id="9c44a-603">Se non sono presenti altre interfacce che eseguono il client DHCP, il servizio avvierà/riprenderà il thread del client DHCP e (ri) attiverà il timer del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-603">If there are no other interfaces running DHCP Client this service will start/resume the DHCP Client thread and (re)activate the DHCP Client timer.</span></span>  
  
<span data-ttu-id="9c44a-604">L'applicazione deve usare *nx_ip_status_check* per verificare se è stato ottenuto un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-604">The application should use *nx_ip_status_check* to verify if an IP address is obtained.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-605">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-605">Input Parameters</span></span>

- <span data-ttu-id="9c44a-606">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-606">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="9c44a-607">**Interface_index**: Indice in cui avviare il client DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-607">**Interface_index**: Index on which to start the DHCP Client</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-608">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-608">Return Values</span></span>

- <span data-ttu-id="9c44a-609">**NX_SUCCESS**: (0x00) avvio DHCP riuscito.</span><span class="sxs-lookup"><span data-stu-id="9c44a-609">**NX_SUCCESS**: (0x00) Successful DHCP start.</span></span> 
- <span data-ttu-id="9c44a-610">**NX_DHCP_ALREADY_STARTED**: (0X93) DHCP è già avviato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-610">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP already started.</span></span>
- <span data-ttu-id="9c44a-611">NX_PTR_ERROR: (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-611">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="9c44a-612">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-612">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="9c44a-613">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-613">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-614">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-614">Allowed From</span></span>

<span data-ttu-id="9c44a-615">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-615">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-616">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-616">Example</span></span>

```c
/* Start the DHCP processing for this IP instance on interface 1.  */
status =  nx_dhcp_interface_start(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully started.  */
```

## <a name="nx_dhcp_state_change_notify"></a><span data-ttu-id="9c44a-617">nx_dhcp_state_change_notify</span><span class="sxs-lookup"><span data-stu-id="9c44a-617">nx_dhcp_state_change_notify</span></span>

<span data-ttu-id="9c44a-618">Imposta funzione di callback modifica stato DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-618">Set DHCP state change callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-619">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-619">Prototype</span></span>

```c
UINT nx_dhcp_state_change_notify(NX_DHCP *dhcp_ptr, 
                                 VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, UCHAR new_state));
```

### <a name="description"></a><span data-ttu-id="9c44a-620">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-620">Description</span></span>

<span data-ttu-id="9c44a-621">Questo servizio registra la funzione di callback specificata dhcp_state_change_notify per notificare a un'applicazione le modifiche dello stato DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-621">This service registers the specified callback function dhcp_state_change_notify for notifying an application of DHCP state changes.</span></span> <span data-ttu-id="9c44a-622">La funzione di callback fornisce lo stato di transizione del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-622">The callback function supplies the state the DHCP Client has transitioned into.</span></span>

<span data-ttu-id="9c44a-623">Di seguito sono riportati i valori associati ai vari Stati DHCP:</span><span class="sxs-lookup"><span data-stu-id="9c44a-623">Following are values associated with the various DHCP states:</span></span>

- <span data-ttu-id="9c44a-624">NX_DHCP_STATE_BOOT: 1</span><span class="sxs-lookup"><span data-stu-id="9c44a-624">NX_DHCP_STATE_BOOT: 1</span></span>
- <span data-ttu-id="9c44a-625">NX_DHCP_STATE_INIT: 2</span><span class="sxs-lookup"><span data-stu-id="9c44a-625">NX_DHCP_STATE_INIT: 2</span></span>
- <span data-ttu-id="9c44a-626">NX_DHCP_STATE_SELECTING: 3</span><span class="sxs-lookup"><span data-stu-id="9c44a-626">NX_DHCP_STATE_SELECTING: 3</span></span>
- <span data-ttu-id="9c44a-627">NX_DHCP_STATE_REQUESTING: 4</span><span class="sxs-lookup"><span data-stu-id="9c44a-627">NX_DHCP_STATE_REQUESTING: 4</span></span>
- <span data-ttu-id="9c44a-628">NX_DHCP_STATE_BOUND: 5</span><span class="sxs-lookup"><span data-stu-id="9c44a-628">NX_DHCP_STATE_BOUND: 5</span></span>
- <span data-ttu-id="9c44a-629">NX_DHCP_STATE_RENEWING: 6</span><span class="sxs-lookup"><span data-stu-id="9c44a-629">NX_DHCP_STATE_RENEWING: 6</span></span>
- <span data-ttu-id="9c44a-630">NX_DHCP_STATE_REBINDING: 7</span><span class="sxs-lookup"><span data-stu-id="9c44a-630">NX_DHCP_STATE_REBINDING: 7</span></span>
- <span data-ttu-id="9c44a-631">NX_DHCP_STATE_FORCERENEW: 8</span><span class="sxs-lookup"><span data-stu-id="9c44a-631">NX_DHCP_STATE_FORCERENEW: 8</span></span>
- <span data-ttu-id="9c44a-632">NX_DHCP_STATE_ADDRESS_PROBING: 9</span><span class="sxs-lookup"><span data-stu-id="9c44a-632">NX_DHCP_STATE_ADDRESS_PROBING: 9</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-633">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-633">Input Parameters</span></span>

- <span data-ttu-id="9c44a-634">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-634">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="9c44a-635">**dhcp_state_change_notify**: puntatore alla funzione di callback modifica stato</span><span class="sxs-lookup"><span data-stu-id="9c44a-635">**dhcp_state_change_notify**: State change callback function pointer</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-636">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-636">Return Values</span></span>

- <span data-ttu-id="9c44a-637">**NX_SUCCESS**: (0x00) set di callback riuscito.</span><span class="sxs-lookup"><span data-stu-id="9c44a-637">**NX_SUCCESS**: (0x00) Successful callback set.</span></span>  
- <span data-ttu-id="9c44a-638">NX_PTR_ERROR: (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-638">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="9c44a-639">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-639">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-640">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-640">Allowed From</span></span>

<span data-ttu-id="9c44a-641">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="9c44a-641">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-642">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-642">Example</span></span>

```c
/* Register the “my_state_change” function to be called on any DHCP state change, assuming DHCP has alreadybeen created.  */
status =  nx_dhcp_state_change_notify(&my_dhcp, my_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered.  */
```

## <a name="nx_dhcp_interface_state_change_notify"></a><span data-ttu-id="9c44a-643">nx_dhcp_interface_state_change_notify</span><span class="sxs-lookup"><span data-stu-id="9c44a-643">nx_dhcp_interface_state_change_notify</span></span>

<span data-ttu-id="9c44a-644">Imposta la funzione di callback della modifica dello stato DHCP sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-644">Set DHCP state change callback function on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-645">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-645">Prototype</span></span>

```c
UINT nx_dhcp_interface_state_change_notify(NX_DHCP *dhcp_ptr, UINT interface_index,
                                           VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                                                            UINT interface_index,
                                                                            UCHAR new_state));
```

### <a name="description"></a><span data-ttu-id="9c44a-646">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-646">Description</span></span>

<span data-ttu-id="9c44a-647">Questo servizio registra la funzione di callback specificata per notificare a un'applicazione le modifiche dello stato DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-647">This service registers the specified callback function for notifying an application of DHCP state changes.</span></span> <span data-ttu-id="9c44a-648">Gli argomenti di input funciton di callback sono l'indice dell'interfaccia e lo stato di transizione del client DHCP a tale interfaccia.</span><span class="sxs-lookup"><span data-stu-id="9c44a-648">The callback funciton input arguments are the interface index and the state the DHCP Client has transitioned to on that interface.</span></span>

<span data-ttu-id="9c44a-649">Per ulteriori informazioni sulle funzioni di modifica dello stato, vedere *nx_dhcp_state_change_notify*().</span><span class="sxs-lookup"><span data-stu-id="9c44a-649">For more information about state change functions, see *nx_dhcp_state_change_notify*().</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-650">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-650">Input Parameters</span></span>

- <span data-ttu-id="9c44a-651">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-651">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="9c44a-652">**dhcp_interface_state_change_notify**: puntatore alla funzione di callback dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9c44a-652">**dhcp_interface_state_change_notify**: Application callback function pointer</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-653">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-653">Return Values</span></span>

- <span data-ttu-id="9c44a-654">**NX_SUCCESS**: (0x00) set di callback riuscito.</span><span class="sxs-lookup"><span data-stu-id="9c44a-654">**NX_SUCCESS**: (0x00) Successful callback set.</span></span>  
- <span data-ttu-id="9c44a-655">NX_PTR_ERROR: (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-655">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-656">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-656">Allowed From</span></span>

<span data-ttu-id="9c44a-657">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="9c44a-657">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-658">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-658">Example</span></span>

```c
/* Register the “my_state_change” function to be called on any DHCP state change,   
   assuming DHCP has alreadybeen created.  */

void dhcp_interstate_state_change(NX_DHCP *dhcp_ptr, UINT iface_index, 
                                  UCHAR new_state);


status =  nx_dhcp_interstate_state_change_notify(&my_dhcp,  
                                                 dhcp_interstate_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered.  */
```

## <a name="nx_dhcp_stop"></a><span data-ttu-id="9c44a-659">nx_dhcp_stop</span><span class="sxs-lookup"><span data-stu-id="9c44a-659">nx_dhcp_stop</span></span>

<span data-ttu-id="9c44a-660">Arresta l'elaborazione DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-660">Stops DHCP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-661">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-661">Prototype</span></span>

```c
UINT nx_dhcp_stop(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="9c44a-662">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-662">Description</span></span>

<span data-ttu-id="9c44a-663">Questo servizio interrompe l'elaborazione DHCP su tutte le interfacce che hanno avviato l'elaborazione DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-663">This service stops DHCP processing on all interfaces that have started DHCP processing.</span></span> <span data-ttu-id="9c44a-664">Se non sono presenti interfacce che elaborano DHCP, il servizio sospende il thread del client DHCP e disattiva il timer del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-664">If there are no interfaces processing DHCP, this service will suspend the DHCP Client thread, and inactivate the DHCP Client timer.</span></span>

<span data-ttu-id="9c44a-665">Per arrestare DHCP in un'interfaccia specifica se sono abilitate più interfacce per DHCP, usare il servizio *nx_dhcp_interface_stop* .</span><span class="sxs-lookup"><span data-stu-id="9c44a-665">To stop DHCP on a specific interface if multiple interfaces are enabled for DHCP, use the *nx_dhcp_interface_stop* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-666">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-666">Input Parameters</span></span>

- <span data-ttu-id="9c44a-667">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-667">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-668">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-668">Return Values</span></span>

- <span data-ttu-id="9c44a-669">**NX_SUCCESS**: (0x00) arresto DHCP riuscito</span><span class="sxs-lookup"><span data-stu-id="9c44a-669">**NX_SUCCESS**: (0x00) Successful DHCP stop</span></span>
- <span data-ttu-id="9c44a-670">**NX_DHCP_NOT_STARTED**: (0X96) l'istanza DHCP non è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="9c44a-670">**NX_DHCP_NOT_STARTED**: (0x96) The DHCP instance not started.</span></span>
- <span data-ttu-id="9c44a-671">NX_PTR_ERROR: (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-671">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="9c44a-672">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-672">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-673">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-673">Allowed From</span></span>

<span data-ttu-id="9c44a-674">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-674">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-675">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-675">Example</span></span>

```c
/* Stop the DHCP processing for this IP instance.  */
status =  nx_dhcp_stop(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully stopped.  */
```

## <a name="nx_dhcp_interface_stop"></a><span data-ttu-id="9c44a-676">nx_dhcp_interface_stop</span><span class="sxs-lookup"><span data-stu-id="9c44a-676">nx_dhcp_interface_stop</span></span>

<span data-ttu-id="9c44a-677">Arresta l'elaborazione DHCP sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-677">Stop DHCP processing on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-678">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-678">Prototype</span></span>

```c
UINT nx_dhcp_interface_stop(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="9c44a-679">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-679">Description</span></span>

<span data-ttu-id="9c44a-680">Questo servizio interrompe l'elaborazione DHCP sull'interfaccia specificata se DHCP è già avviato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-680">This service stops DHCP processing on the specified interface if DHCP is already started.</span></span> <span data-ttu-id="9c44a-681">Se non sono presenti altre interfacce che eseguono DHCP, il thread e il timer DHCP verranno sospesi.</span><span class="sxs-lookup"><span data-stu-id="9c44a-681">If there are no other interfaces running DHCP, the DHCP thread and timer are suspended.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-682">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-682">Input Parameters</span></span>

- <span data-ttu-id="9c44a-683">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-683">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="9c44a-684">**Interface_index**: interfaccia in cui arrestare l'elaborazione DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-684">**Interface_index**: Interface on which to stop DHCP processing</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-685">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-685">Return Values</span></span>

- <span data-ttu-id="9c44a-686">**NX_SUCCESS**: (0x00) arresto DHCP riuscito</span><span class="sxs-lookup"><span data-stu-id="9c44a-686">**NX_SUCCESS**: (0x00) Successful DHCP stop</span></span>
- <span data-ttu-id="9c44a-687">**NX_DHCP_NOT_STARTED**: (0X96) DHCP non avviato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-687">**NX_DHCP_NOT_STARTED**: (0x96) DHCP not started.</span></span>
- <span data-ttu-id="9c44a-688">NX_PTR_ERROR: (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-688">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="9c44a-689">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-689">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="9c44a-690">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-690">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-691">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-691">Allowed From</span></span>

<span data-ttu-id="9c44a-692">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-692">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-693">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-693">Example</span></span>

```c
/* Stop DHCP processing for this IP instance on interface 1.  */
status =  nx_dhcp_interface_stop(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully stopped.  */
```

## <a name="nx_dhcp_user_option_retrieve"></a><span data-ttu-id="9c44a-694">nx_dhcp_user_option_retrieve</span><span class="sxs-lookup"><span data-stu-id="9c44a-694">nx_dhcp_user_option_retrieve</span></span>

<span data-ttu-id="9c44a-695">Recupera un'opzione DHCP dall'ultima risposta server</span><span class="sxs-lookup"><span data-stu-id="9c44a-695">Retrieve a DHCP option from last server response</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-696">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-696">Prototype</span></span>

```c
UINT nx_dhcp_user_option_retrieve(NX_DHCP *dhcp_ptr, UINT request_option, 
                                  UCHAR *destination_ptr, UINT *destination_size);
```

### <a name="description"></a><span data-ttu-id="9c44a-697">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-697">Description</span></span>

<span data-ttu-id="9c44a-698">Questo servizio recupera l'opzione DHCP specificata dal buffer delle opzioni DHCP nella prima interfaccia abilitata per DHCP trovato nel record client DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-698">This service retrieves the specified DHCP option from the DHCP options buffer on the first interface enabled for DHCP found on the DHCP Client record.</span></span> <span data-ttu-id="9c44a-699">In caso di esito positivo, i dati dell'opzione vengono copiati nel buffer specificato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-699">If successful, the option data is copied into the specified buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-700">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-700">Input Parameters</span></span>

- <span data-ttu-id="9c44a-701">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-701">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>  
- <span data-ttu-id="9c44a-702">**request_option**: opzione DHCP, come specificato dalle RFC.</span><span class="sxs-lookup"><span data-stu-id="9c44a-702">**request_option**: DHCP option, as specified by the RFCs.</span></span> <span data-ttu-id="9c44a-703">Vedere l'opzione NX_DHCP_OPTION in *nxd_dhcp_client. h*.</span><span class="sxs-lookup"><span data-stu-id="9c44a-703">See the NX_DHCP_OPTION option in *nxd_dhcp_client.h*.</span></span>
- <span data-ttu-id="9c44a-704">**destination_ptr**: puntatore alla destinazione per la stringa di risposta.</span><span class="sxs-lookup"><span data-stu-id="9c44a-704">**destination_ptr**: Pointer to the destination for the response string.</span></span>  
- <span data-ttu-id="9c44a-705">**destination_size**: puntatore alla dimensione della destinazione e al ritorno, la destinazione in cui inserire il numero di byte restituiti.</span><span class="sxs-lookup"><span data-stu-id="9c44a-705">**destination_size**: Pointer to the size of the destination and on return, the destination to place the number of bytes returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-706">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-706">Return Values</span></span>

- <span data-ttu-id="9c44a-707">**NX_SUCCESS**: (0x00) il recupero delle opzioni è riuscito.</span><span class="sxs-lookup"><span data-stu-id="9c44a-707">**NX_SUCCESS**: (0x00) Successful option retrieval.</span></span>  
- <span data-ttu-id="9c44a-708">**NX_DHCP_NOT_BOUND**: (0X94) client DHCP non associato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-708">**NX_DHCP_NOT_BOUND**: (0x94) DHCP Client not bound.</span></span>
- <span data-ttu-id="9c44a-709">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) non sono abilitate interfacce per DHCP</span><span class="sxs-lookup"><span data-stu-id="9c44a-709">**NX_DHCP_NO_INTERFACES_ENABLED**: (0xA5) No interfaces enabled for DHCP</span></span>
- <span data-ttu-id="9c44a-710">**NX_DHCP_DEST_TO_SMALL**: (0x95) la destinazione è troppo piccola per mantenere la risposta.</span><span class="sxs-lookup"><span data-stu-id="9c44a-710">**NX_DHCP_DEST_TO_SMALL**: (0x95) Destination is too small to hold response.</span></span>
- <span data-ttu-id="9c44a-711">Impossibile trovare l'opzione **NX_DHCP_PARSE_ERROR**: (0x97) nella risposta del server.</span><span class="sxs-lookup"><span data-stu-id="9c44a-711">**NX_DHCP_PARSE_ERROR**: (0x97) Option not found in Server response.</span></span>
- <span data-ttu-id="9c44a-712">NX_PTR_ERROR: (0x16) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-712">NX_PTR_ERROR: (0x16) Invalid input pointer.</span></span>
- <span data-ttu-id="9c44a-713">NX_CALLER_ERROR: (0x11) il chiamante di questo servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-713">NX_CALLER_ERROR: (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-714">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-714">Allowed From</span></span>

<span data-ttu-id="9c44a-715">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-715">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-716">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-716">Example</span></span>

```c
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server.  */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_user_option_retrieve(&my_dhcp, NX_DHCP_OPTION_DNS_SVR,
                                        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string.  */
```

## <a name="nx_dhcp_interface_user_option_retrieve"></a><span data-ttu-id="9c44a-717">nx_dhcp_interface_user_option_retrieve</span><span class="sxs-lookup"><span data-stu-id="9c44a-717">nx_dhcp_interface_user_option_retrieve</span></span>

<span data-ttu-id="9c44a-718">Recupera un'opzione DHCP dall'ultima risposta server sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-718">Retrieve a DHCP option from last server response on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-719">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-719">Prototype</span></span>

```c
UINT nx_dhcp_interface_user_option_retrieve(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            UINT request_option, UCHAR *destination_ptr,
                                            UINT *destination_size);
```

### <a name="description"></a><span data-ttu-id="9c44a-720">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-720">Description</span></span>

<span data-ttu-id="9c44a-721">Questo servizio recupera l'opzione DHCP specificata dal buffer delle opzioni DHCP nell'interfaccia specificata, se tale interfaccia è abilitata per DHCP.</span><span class="sxs-lookup"><span data-stu-id="9c44a-721">This service retrieves the specified DHCP option from the DHCP options buffer on the specified interface, if that interface is enabled for DHCP.</span></span> <span data-ttu-id="9c44a-722">In caso di esito positivo, i dati dell'opzione vengono copiati nel buffer specificato.</span><span class="sxs-lookup"><span data-stu-id="9c44a-722">If successful, the option data is copied into the specified buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-723">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-723">Input Parameters</span></span>

- <span data-ttu-id="9c44a-724">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-724">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="9c44a-725">**Interface_index**: Indice in cui recuperare l'opzione specificata</span><span class="sxs-lookup"><span data-stu-id="9c44a-725">**Interface_index**: Index on which to retrieve the specified option</span></span>
- <span data-ttu-id="9c44a-726">**request_option**: opzione DHCP, come specificato dalle RFC.</span><span class="sxs-lookup"><span data-stu-id="9c44a-726">**request_option**: DHCP option, as specified by the RFCs.</span></span> <span data-ttu-id="9c44a-727">Vedere l'opzione NX_DHCP_OPTION: in *nxd_dhcp_client. h*.</span><span class="sxs-lookup"><span data-stu-id="9c44a-727">See the NX_DHCP_OPTION option: in *nxd_dhcp_client.h*.</span></span>  
- <span data-ttu-id="9c44a-728">**destination_ptr**: puntatore alla destinazione per la stringa di risposta.</span><span class="sxs-lookup"><span data-stu-id="9c44a-728">**destination_ptr**: Pointer to the destination for the response string.</span></span>  
- <span data-ttu-id="9c44a-729">**destination_size**: puntatore alla dimensione della destinazione e al ritorno, la destinazione in cui inserire il numero di byte restituiti.</span><span class="sxs-lookup"><span data-stu-id="9c44a-729">**destination_size**: Pointer to the size of the destination and on return, the destination to place the number of bytes returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-730">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-730">Return Values</span></span>

- <span data-ttu-id="9c44a-731">**NX_SUCCESS**: (0x00) il recupero delle opzioni è riuscito.</span><span class="sxs-lookup"><span data-stu-id="9c44a-731">**NX_SUCCESS**: (0x00) Successful option retrieval.</span></span>  
- <span data-ttu-id="9c44a-732">**NX_DHCP_NOT_BOUND**: (0x94) indirizzo IP non assegnato</span><span class="sxs-lookup"><span data-stu-id="9c44a-732">**NX_DHCP_NOT_BOUND**: (0x94) IP address not assigned</span></span>
- <span data-ttu-id="9c44a-733">**NX_DHCP_DEST_TO_SMALL**: il buffer (0x95) è troppo piccolo</span><span class="sxs-lookup"><span data-stu-id="9c44a-733">**NX_DHCP_DEST_TO_SMALL**: (0x95) Buffer is too small</span></span>
- <span data-ttu-id="9c44a-734">**NX_DHCP_PARSE_ERROR**: (0x97) l'opzione DHCP non è stata trovata nella risposta del server.</span><span class="sxs-lookup"><span data-stu-id="9c44a-734">**NX_DHCP_PARSE_ERROR**: (0x97) DHCP Option not found in Server response.</span></span>
- <span data-ttu-id="9c44a-735">NX_PTR_ERROR: (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-735">NX_PTR_ERROR: (0x16) Invalid DHCP pointer.</span></span>
- <span data-ttu-id="9c44a-736">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-736">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="9c44a-737">NX_INVALID_INTERFACE: (0x4C) interfaccia di rete non valida</span><span class="sxs-lookup"><span data-stu-id="9c44a-737">NX_INVALID_INTERFACE: (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-738">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-738">Allowed From</span></span>

<span data-ttu-id="9c44a-739">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-739">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-740">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-740">Example</span></span>

```c
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server on the prmary interface.  */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_interface_user_option_retrieve(&my_dhcp, 0, NX_DHCP_OPTION_DNS_SVR,
                                                  dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string.  */
```

## <a name="nx_dhcp_user_option_convert"></a><span data-ttu-id="9c44a-741">nx_dhcp_user_option_convert</span><span class="sxs-lookup"><span data-stu-id="9c44a-741">nx_dhcp_user_option_convert</span></span>

<span data-ttu-id="9c44a-742">Converte quattro byte in ULONG</span><span class="sxs-lookup"><span data-stu-id="9c44a-742">Convert four bytes to ULONG</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-743">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-743">Prototype</span></span>

```c
ULONG nx_dhcp_user_option_convert(UCHAR *option_string_ptr);
```

### <a name="description"></a><span data-ttu-id="9c44a-744">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-744">Description</span></span>

<span data-ttu-id="9c44a-745">Questo servizio converte i quattro caratteri a cui punta "option_string_ptr" in un valore long senza segno.</span><span class="sxs-lookup"><span data-stu-id="9c44a-745">This service converts the four characters pointed to by “option_string_ptr” into an unsigned long value.</span></span> <span data-ttu-id="9c44a-746">È particolarmente utile quando gli indirizzi IP sono</span><span class="sxs-lookup"><span data-stu-id="9c44a-746">It is especially useful when IP addresses are</span></span>  
<span data-ttu-id="9c44a-747">presente.</span><span class="sxs-lookup"><span data-stu-id="9c44a-747">present.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-748">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-748">Input Parameters</span></span>

- <span data-ttu-id="9c44a-749">**option_string_ptr**: puntatore a una stringa di opzione recuperata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-749">**option_string_ptr**: Pointer to previously retrieved option string.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-750">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-750">Return Values</span></span>

- <span data-ttu-id="9c44a-751">**Valore**: valore dei primi quattro byte.</span><span class="sxs-lookup"><span data-stu-id="9c44a-751">**Value**: Value of first four bytes.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-752">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-752">Allowed From</span></span>

<span data-ttu-id="9c44a-753">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-753">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-754">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-754">Example</span></span>

```c
UCHAR  dns_ip_string[4];
ULONG  dns_ip;

/* Convert the first four bytes of “dns_ip_string” to an actual IP
address in “dns_ip.”  */
dns_ip=  nx_dhcp_user_option_convert(dns_ip_string);

/* If status is NX_SUCCESS the DNS IP address is in “dns_ip.”  */
```

## <a name="nx_dhcp_user_option_add_callback_set"></a><span data-ttu-id="9c44a-755">nx_dhcp_user_option_add_callback_set</span><span class="sxs-lookup"><span data-stu-id="9c44a-755">nx_dhcp_user_option_add_callback_set</span></span>

<span data-ttu-id="9c44a-756">Imposta la funzione di callback per l'aggiunta di opzioni fornite dall'utente</span><span class="sxs-lookup"><span data-stu-id="9c44a-756">Set callback function for adding user supplied options</span></span>

### <a name="prototype"></a><span data-ttu-id="9c44a-757">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9c44a-757">Prototype</span></span>

```c
ULONG nx_dhcp_user_option_add_callbcak_set(NX_DHCP *dhcp_ptr, 
                                           UINT (*dhcp_user_option_add)(NX_DHCP *dhcp_ptr, 
                                                                        UINT iface_index, 
                                                                        UINT message_type, 
                                                                        UCHAR *user_option_ptr, 
                                                                        UINT *user_option_length));
```

### <a name="description"></a><span data-ttu-id="9c44a-758">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c44a-758">Description</span></span>

<span data-ttu-id="9c44a-759">Questo servizio registra la funzione di callback specificata per aggiungere opzioni fornite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="9c44a-759">This service registers the specified callback function for adding user supplied options.</span></span>

<span data-ttu-id="9c44a-760">Se la funzione di callback specificata, le applicazioni possono aggiungere opzioni fornite dall'utente nel pacchetto per iface_index e message_type.</span><span class="sxs-lookup"><span data-stu-id="9c44a-760">If the callback function specified, the applications can add user supplied options into the packet by iface_index and message_type.</span></span>

>[!NOTE] 
> <span data-ttu-id="9c44a-761">Nella routine dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9c44a-761">In user’s routine.</span></span> <span data-ttu-id="9c44a-762">Le applicazioni devono seguire il formato delle opzioni DHCP quando si aggiungono le opzioni fornite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="9c44a-762">Applications must follow the DHCP options format when add user supplied options.</span></span> <span data-ttu-id="9c44a-763">La dimensione totale delle opzioni utente deve essere minore o uguale a user_option_length e aggiornare la user_option_length come lunghezza delle opzioni reali.</span><span class="sxs-lookup"><span data-stu-id="9c44a-763">The total size of user options must be less or equal to user_option_length, and update the user_option_length as real options length.</span></span> <span data-ttu-id="9c44a-764">Restituisce NX_TRUE se le opzioni di aggiunta sono state completate, in caso contrario restituire NX_FALSE.</span><span class="sxs-lookup"><span data-stu-id="9c44a-764">Return NX_TRUE if add options successfully, else return NX_FALSE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9c44a-765">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9c44a-765">Input Parameters</span></span>

- <span data-ttu-id="9c44a-766">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c44a-766">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>
- <span data-ttu-id="9c44a-767">**dhcp_user_option_add**: puntatore alla funzione di aggiunta dell'opzione User.</span><span class="sxs-lookup"><span data-stu-id="9c44a-767">**dhcp_user_option_add**: Pointer to user option add function.</span></span>

### <a name="return-values"></a><span data-ttu-id="9c44a-768">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9c44a-768">Return Values</span></span>

- <span data-ttu-id="9c44a-769">**NX_SUCCESS**: (0x00) set di callback riuscito.</span><span class="sxs-lookup"><span data-stu-id="9c44a-769">**NX_SUCCESS**: (0x00) Successful callback set.</span></span>
- <span data-ttu-id="9c44a-770">NX_PTR_ERROR: (0x16) puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="9c44a-770">NX_PTR_ERROR: (0x16) Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9c44a-771">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9c44a-771">Allowed From</span></span>

<span data-ttu-id="9c44a-772">Thread</span><span class="sxs-lookup"><span data-stu-id="9c44a-772">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9c44a-773">Esempio</span><span class="sxs-lookup"><span data-stu-id="9c44a-773">Example</span></span>

```c
/* Register the “my_dhcp_user_option_add” function to be called when add DHCP
options, assuming DHCP has already been created.  */

status =  nx_dhcp_user_option_add_callback_set(&my_dhcp, my_dhcp_user_option_add);

/* If status is NX_SUCCESS the callback function was successfully registered.  */

```

