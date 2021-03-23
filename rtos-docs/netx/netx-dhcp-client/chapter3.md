---
title: Capitolo 3-Descrizione dei servizi client DHCP di Azure RTO NetX
description: Questo capitolo contiene una descrizione di tutti i servizi DHCP di Azure RTO NetX (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8a614d22eca4fe693209751d72958b7d975c64c2
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822700"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dhcp-client-services"></a><span data-ttu-id="df421-103">Capitolo 3-Descrizione dei servizi client DHCP di Azure RTO NetX</span><span class="sxs-lookup"><span data-stu-id="df421-103">Chapter 3 - Description of Azure RTOS NetX DHCP Client services</span></span>

<span data-ttu-id="df421-104">Questo capitolo contiene una descrizione di tutti i servizi DHCP di Azure RTO NetX (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="df421-104">This chapter contains a description of all Azure RTOS NetX DHCP services (listed below) in alphabetic order.</span></span>

<span data-ttu-id="df421-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="df421-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="df421-106">**nx_dhcp_create**: *creare un'istanza DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-106">**nx_dhcp_create**: *Create a DHCP instance*</span></span>

- <span data-ttu-id="df421-107">**nx_dhcp_clear_broadcast_flag**: Cancella flag broadcast nei messaggi client</span><span class="sxs-lookup"><span data-stu-id="df421-107">**nx_dhcp_clear_broadcast_flag**: Clear broadcast flag on Client messages</span></span>

- <span data-ttu-id="df421-108">**nx_dhcp_delete**: *eliminare un'istanza DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-108">**nx_dhcp_delete**: *Delete a DHCP instance*</span></span>

- <span data-ttu-id="df421-109">**nx_dhcp_decline**: inviare un *messaggio di rifiuto al server*</span><span class="sxs-lookup"><span data-stu-id="df421-109">**nx_dhcp_decline**: Send *Decline message to server*</span></span>

- <span data-ttu-id="df421-110">**nx_dhcp_force_renew**: *Invia messaggio di rinnovo forzato*</span><span class="sxs-lookup"><span data-stu-id="df421-110">**nx_dhcp_force_renew**: *Send force renew message*</span></span>

- <span data-ttu-id="df421-111">**nx_dhcp_packet_pool_set**: *impostare il pool di pacchetti client DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-111">**nx_dhcp_packet_pool_set**: *Set the DHCP Client packet pool*</span></span>

- <span data-ttu-id="df421-112">**nx_dhcp_release**: inviare un *messaggio di rilascio al server*</span><span class="sxs-lookup"><span data-stu-id="df421-112">**nx_dhcp_release**: Send *Release message to server*</span></span>

- <span data-ttu-id="df421-113">**nx_dhcp_reinitialize**: *Cancella parametri della rete client DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-113">**nx_dhcp_reinitialize**: *Clear DHCP client network parameters*</span></span>

- <span data-ttu-id="df421-114">**nx_dhcp_request_client_ip**: *specificare un indirizzo IP specifico*</span><span class="sxs-lookup"><span data-stu-id="df421-114">**nx_dhcp_request_client_ip**: *Specify a specific IP address*</span></span>

- <span data-ttu-id="df421-115">**nx_dhcp_send_request**: *inviare un messaggio DHCP al server*</span><span class="sxs-lookup"><span data-stu-id="df421-115">**nx_dhcp_send_request**: *Send DHCP message to server*</span></span>

- <span data-ttu-id="df421-116">**nx_dhcp_server_address_get**: *recuperare l'indirizzo del server DHCP del client DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-116">**nx_dhcp_server_address_get**: *Retrieve DHCP Client’s DHCP server address*</span></span>

- <span data-ttu-id="df421-117">**nx_dhcp_set_interface_index**: *specificare l'interfaccia di rete del client*</span><span class="sxs-lookup"><span data-stu-id="df421-117">**nx_dhcp_set_interface_index**: *Specify the Client network interface*</span></span>

- <span data-ttu-id="df421-118">**nx_dhcp_start**: *avviare l'elaborazione DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-118">**nx_dhcp_start**: *Start DHCP processing*</span></span>

- <span data-ttu-id="df421-119">**nx_dhcp_state_change_notify**: *notifica l'applicazione della modifica dello stato DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-119">**nx_dhcp_state_change_notify**: *Notify application of DHCP state change*</span></span>

- <span data-ttu-id="df421-120">**nx_dhcp_stop**: *arrestare l'elaborazione DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-120">**nx_dhcp_stop**: *Stop DHCP processing*</span></span>

- <span data-ttu-id="df421-121">**nx_dhcp_user_option_retrieve**: *recuperare l'opzione DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-121">**nx_dhcp_user_option_retrieve**: *Retrieve DHCP option*</span></span>

- <span data-ttu-id="df421-122">**nx_dhcp_user_option_convert**: *conversione di quattro byte in ULONG*</span><span class="sxs-lookup"><span data-stu-id="df421-122">**nx_dhcp_user_option_convert**: *Convert four bytes to ULONG*</span></span>

<span data-ttu-id="df421-123">Servizi client DHCP specifici dell'interfaccia:</span><span class="sxs-lookup"><span data-stu-id="df421-123">Interface specific DHCP Client services:</span></span>

- <span data-ttu-id="df421-124">**nx_dhcp_interface_clear_broadcast_flag**: *Cancella il flag broadcast nei messaggi client sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-124">**nx_dhcp_interface_clear_broadcast_flag**: *Clear broadcast flag on Client messages on specified interface*</span></span>

- <span data-ttu-id="df421-125">**nx_dhcp_interface_enable**: *Abilita l'interfaccia per l'esecuzione di DHCP sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-125">**nx_dhcp_interface_enable**: *Enable interface to run DHCP on the specified interface*</span></span>

- <span data-ttu-id="df421-126">**nx_dhcp_interface_disable**: *disabilitare l'interfaccia per l'esecuzione di DHCP sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-126">**nx_dhcp_interface_disable**: *Disable interface to run DHCP on the specified interface*</span></span>

- <span data-ttu-id="df421-127">**nx_dhcp_interface_decline**: *inviare il messaggio di rifiuto al server sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-127">**nx_dhcp_interface_decline**: *Send Decline message to server on the specified interface*</span></span>

- <span data-ttu-id="df421-128">**nx_dhcp_interface_force_renew**: *inviare un messaggio Force Renew sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-128">**nx_dhcp_interface_force_renew**: *Send a force renew message on the specified interface*</span></span>

- <span data-ttu-id="df421-129">**nx_dhcp_interface_reinitialize**: *Cancella i parametri di rete del client DHCP nell'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-129">**nx_dhcp_interface_reinitialize**: *Clear DHCP client network parameters on the specified interface*</span></span>

- <span data-ttu-id="df421-130">**nx_dhcp_interface_release**: *inviare un messaggio di rilascio al server sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-130">**nx_dhcp_interface_release**: *Send Release message to server  on the specified interface*</span></span>

- <span data-ttu-id="df421-131">**nx_dhcp_interface_request_client_ip**: *specificare un indirizzo IP specifico nell'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-131">**nx_dhcp_interface_request_client_ip**: *Specify a specific IP address on the specified interface*</span></span>

- <span data-ttu-id="df421-132">**nx_dhcp_interface_send_request**: *inviare un messaggio DHCP al server sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-132">**nx_dhcp_interface_send_request**: *Send DHCP message to server on the specified interface*</span></span>

- <span data-ttu-id="df421-133">**nx_dhcp_interface_server_address_get**: *ottenere l'indirizzo IP del server DHCP nell'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-133">**nx_dhcp_interface_server_address_get**: *Get the DHCP server IP address on the specified interface*</span></span>

- <span data-ttu-id="df421-134">**nx_dhcp_interface_start**: *avviare l'elaborazione del client DHCP sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-134">**nx_dhcp_interface_start**: *Start the DHCP Client processing on the specified interface*</span></span>

- <span data-ttu-id="df421-135">**nx_dhcp_interface_stop**: *arrestare l'elaborazione del client DHCP sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-135">**nx_dhcp_interface_stop**: *Stop the DHCP Client processing on the specified interface*</span></span>

- <span data-ttu-id="df421-136">**nx_dhcp_interface_state_change_notify**: *impostare la funzione di callback quando lo stato DHCP viene modificato sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-136">**nx_dhcp_interface_state_change_notify**: *Set the callback function when DHCP state changes on the specified interface*</span></span>

- <span data-ttu-id="df421-137">**nx_dhcp_interface_user_option_retrieve**: *recuperare l'opzione DHCP specificata nell'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-137">**nx_dhcp_interface_user_option_retrieve**: *Retrieve the specified DHCP option on the specified interface*</span></span>

<span data-ttu-id="df421-138">Servizi client DHCP se è stato definito NX_DHCP_CLIENT_RESORE_STATE:</span><span class="sxs-lookup"><span data-stu-id="df421-138">DHCP Client Services if NX_DHCP_CLIENT_RESORE_STATE is defined:</span></span>

- <span data-ttu-id="df421-139">**nx_dhcp_resume**: *Riprendi stato client DHCP stabilito in precedenza*</span><span class="sxs-lookup"><span data-stu-id="df421-139">**nx_dhcp_resume**: *Resume previously established DHCP Client state*</span></span>

- <span data-ttu-id="df421-140">**nx_dhcp_suspend**: *sospendere l'elaborazione dello stato del client DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-140">**nx_dhcp_suspend**: *Suspend processing the DHCP Client state*</span></span>

- <span data-ttu-id="df421-141">**nx_dhcp_client_get_record**: *creare un record dello stato del client DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-141">**nx_dhcp_client_get_record**: *Create a record of the DHCP Client state*</span></span>

- <span data-ttu-id="df421-142">**nx_dhcp_client_restore_record**: *ripristinare un record salvato in precedenza nel client DHCP*</span><span class="sxs-lookup"><span data-stu-id="df421-142">**nx_dhcp_client_restore_record**: *Restore a previously saved record to the DHCP Client*</span></span>

- <span data-ttu-id="df421-143">**nx_dhcp_client_update_time_remaining**: *aggiornare il tempo rimanente nello stato DHCP corrente*</span><span class="sxs-lookup"><span data-stu-id="df421-143">**nx_dhcp_client_update_time_remaining**: *Update the time remaining in the current DHCP state*</span></span>

<span data-ttu-id="df421-144">Servizi client DHCP specifici dell'interfaccia se NX_DHCP_CLIENT_RESORE_STATE è definito:</span><span class="sxs-lookup"><span data-stu-id="df421-144">Interface Specific DHCP Client Services if NX_DHCP_CLIENT_RESORE_STATE is defined:</span></span>

- <span data-ttu-id="df421-145">**nx_dhcp_client_interface_get_record**: *creare un record dello stato del client DHCP nell'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-145">**nx_dhcp_client_interface_get_record**: *Create a record of the DHCP Client state on the specified interface*</span></span>

- <span data-ttu-id="df421-146">**nx_dhcp_client_interface_restore_record**: *ripristinare un record salvato in precedenza nel client DHCP sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-146">**nx_dhcp_client_interface_restore_record**: *Restore a previously saved record to the DHCP Client on the specified interface*</span></span>

- <span data-ttu-id="df421-147">**nx_dhcp_client_interface_update_time_remaining**: *aggiornare l'ora rimanente nello stato DHCP corrente sull'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="df421-147">**nx_dhcp_client_interface_update_time_remaining**: *Update the time remaining in the current DHCP state on the specified interface*</span></span>

## <a name="nx_dhcp_create"></a><span data-ttu-id="df421-148">nx_dhcp_create</span><span class="sxs-lookup"><span data-stu-id="df421-148">nx_dhcp_create</span></span>

<span data-ttu-id="df421-149">Creare un'istanza DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-149">Create a DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-150">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-150">Prototype</span></span>

```C
UINT nx_dhcp_create(NX_DHCP *dhcp_ptr, NX_IP *ip_ptr, CHAR *name_ptr);
```

### <a name="description"></a><span data-ttu-id="df421-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-151">Description</span></span>

<span data-ttu-id="df421-152">Questo servizio crea un'istanza DHCP per l'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-152">This service creates a DHCP instance for the previously created IP instance.</span></span> <span data-ttu-id="df421-153">Per impostazione predefinita, l'interfaccia primaria è abilitata per l'esecuzione di DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-153">By default the primary interface is enabled for running DHCP.</span></span> <span data-ttu-id="df421-154">L'input del nome, sebbene non usato nell'implementazione NetX del client DHCP, deve seguire i criteri RFC 1035 per i nomi host.</span><span class="sxs-lookup"><span data-stu-id="df421-154">The name input, while not used in the NetX implementation of DHCP Client, must follow RFC 1035 criteria for host names.</span></span> <span data-ttu-id="df421-155">La lunghezza totale non deve superare i 255 caratteri, le etichette separate da punti devono iniziare con una lettera e terminare con una lettera o un numero e possono contenere trattini ma nessun altro carattere non alfanumerico.</span><span class="sxs-lookup"><span data-stu-id="df421-155">The total length must not exceed 255 characters, the labels separate by dots must begin with a letter, and end with a letter or number, and may contain hyphens but no other non-alphanumeric character.</span></span>

<span data-ttu-id="df421-156">Se l'applicazione desidera eseguire un'altra interfaccia DHCP registrata con l'istanza IP (usando *nx_ip_interface_attach*), l'applicazione può chiamare *NX_DHCP_SET_INTERFACE_INDEX* per eseguire DHCP solo su tale interfaccia oppure *nx_dhcp_interface_enable* per eseguire DHCP su tale interfaccia.</span><span class="sxs-lookup"><span data-stu-id="df421-156">If the application would like to run DHCP another interface registered with the IP instance, (using *nx_ip_interface_attach*), the application can call *nx_dhcp_set_interface_index* to run DHCP on just that interface, or *nx_dhcp_interface_enable* to run DHCP on that interface as well.</span></span> <span data-ttu-id="df421-157">Per ulteriori informazioni, vedere la descrizione di questi servizi.</span><span class="sxs-lookup"><span data-stu-id="df421-157">See description of these services for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="df421-158">L'applicazione deve verificare che il payload del pool di pacchetti client DHCP sia in grado di supportare la dimensione minima dei messaggi DHCP specificata dalla RFC 2131 sezione 2 (548 byte di dati del messaggio DHCP più le intestazioni UDP, IP e frame di rete fisica).</span><span class="sxs-lookup"><span data-stu-id="df421-158">The application must make sure the DHCP Client packet pool payload can support the minimum DHCP message size specified by the RFC 2131 Section 2 (548 bytes of DHCP message data plus UDP, IP and physical network frame headers).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-159">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-159">Input Parameters</span></span>

- <span data-ttu-id="df421-160">**dhcp_ptr** Puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-160">**dhcp_ptr** Pointer to DHCP control block.</span></span>  
- <span data-ttu-id="df421-161">**ip_ptr** Puntatore a un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-161">**ip_ptr** Pointer to previously created IP instance.</span></span>  
- <span data-ttu-id="df421-162">**name_ptr** Puntatore al nome host per l'istanza DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-162">**name_ptr** Pointer to host name for DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-163">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-163">Return Values</span></span>

- <span data-ttu-id="df421-164">Creazione di DHCP **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="df421-164">**NX_SUCCESS** (0x00) Successful DHCP create</span></span>

- <span data-ttu-id="df421-165">**NX_DHCP_INVALID_NAME** (0xA8) nome host non valido</span><span class="sxs-lookup"><span data-stu-id="df421-165">**NX_DHCP_INVALID_NAME** (0xA8) Invalid host name</span></span>

- <span data-ttu-id="df421-166">Payload **NX_DHCP_INVALID_PAYLOAD** (0x9C) troppo piccolo per il messaggio DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-166">**NX_DHCP_INVALID_PAYLOAD** (0x9C) Payload too small for DHCP message</span></span>

- <span data-ttu-id="df421-167">NX_PTR_ERROR (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-167">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-168">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-168">Allowed From</span></span>

<span data-ttu-id="df421-169">**Thread,** Inizializzazione</span><span class="sxs-lookup"><span data-stu-id="df421-169">**Threads,** Initialization</span></span>

### <a name="example"></a><span data-ttu-id="df421-170">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-170">Example</span></span>

```C
/* Create a DHCP instance. */
status =  nx_dhcp_create(&my_dhcp, &my_ip, "My-DHCP");

/* If status is NX_SUCCESS a DHCP instance was successfully created. */
```

## <a name="nx_dhcp_interface_enable"></a><span data-ttu-id="df421-171">nx_dhcp_interface_enable</span><span class="sxs-lookup"><span data-stu-id="df421-171">nx_dhcp_interface_enable</span></span>

<span data-ttu-id="df421-172">Abilitare l'interfaccia specificata per l'esecuzione di DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-172">Enable the specified interface to run DHCP</span></span> 

### <a name="prototype"></a><span data-ttu-id="df421-173">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-173">Prototype</span></span>

```C
UINT nx_dhcp_interface_enable(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="df421-174">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-174">Description</span></span>

<span data-ttu-id="df421-175">Questo servizio Abilita l'interfaccia specificata per l'esecuzione di DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-175">This service enables the specified interface for running DHCP.</span></span> <span data-ttu-id="df421-176">Per impostazione predefinita, l'interfaccia primaria è abilitata per il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-176">By default the primary interface is enabled for DHCP Client.</span></span> <span data-ttu-id="df421-177">A questo punto, è possibile avviare DHCP su questa interfaccia chiamando *nx_dhcp_interface_start* o per avviare DHCP in tutte le interfacce abilitate *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="df421-177">At this point, DHCP can be started on this interface either by calling *nx_dhcp_interface_start* or to start DHCP on all enabled interfaces *nx_dhcp_start*.</span></span>

<span data-ttu-id="df421-178">Si noti che l'applicazione deve prima registrare questa interfaccia con l'istanza IP, usando *nx_ip_interface_attach.*</span><span class="sxs-lookup"><span data-stu-id="df421-178">Note the application must first register this interface with the IP instance, using *nx_ip_interface_attach.*</span></span>

<span data-ttu-id="df421-179">Per aggiungere questa interfaccia all'elenco delle interfacce abilitate, è inoltre necessario che sia disponibile un'interfaccia client DHCP "record".</span><span class="sxs-lookup"><span data-stu-id="df421-179">Further, there must be an available DHCP Client interface ‘record’ to add this interface to the list of enabled interfaces.</span></span> <span data-ttu-id="df421-180">Per impostazione predefinita NX_DHCP_CLIENT_MAX_RECORDS viene definito su 1.</span><span class="sxs-lookup"><span data-stu-id="df421-180">By default NX_DHCP_CLIENT_MAX_RECORDS is defined to 1.</span></span> <span data-ttu-id="df421-181">Impostare questa opzione sul numero massimo di interfacce previste per eseguire simultaneamente il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-181">Set this option to the maximum number of interfaces expected to run DHCP Client simultaneously.</span></span> <span data-ttu-id="df421-182">In genere NX_DHCP_CLIENT_MAX_RECORDS corrisponderà NX_MAX_PHYSICAL_INTERFACES; Tuttavia, se un dispositivo ha più interfacce fisiche rispetto a quanto previsto per l'esecuzione del client DHCP, può risparmiare memoria impostando NX_DHCP_CLIENT_MAX_RECORDS su un valore inferiore a quello specificato.</span><span class="sxs-lookup"><span data-stu-id="df421-182">Typically NX_DHCP_CLIENT_MAX_RECORDS will equal NX_MAX_PHYSICAL_INTERFACES; however, if a device has more physical interfaces than it expects to run DHCP Client, it can save memory by setting NX_DHCP_CLIENT_MAX_RECORDS to less than that number.</span></span> <span data-ttu-id="df421-183">Non esiste un mapping uno-a-uno delle interfacce fisiche con i record dell'interfaccia client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-183">There is not a one to one mapping of physical interfaces with DHCP Client interface records.</span></span>

<span data-ttu-id="df421-184">La differenza tra questo servizio e *nx_dhcp_set_interface_index* è la seconda che imposta una sola interfaccia per eseguire DHCP, mentre questo servizio aggiunge semplicemente l'interfaccia specificata all'elenco di interfacce client abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-184">The difference between this service and *nx_dhcp_set_interface_index* is the latter sets only a single interface to run DHCP whereas this service simply adds the specified interface to the list of Client interfaces enabled for DHCP.</span></span>

<span data-ttu-id="df421-185">Per disabilitare un'interfaccia per DHCP, l'applicazione può chiamare il servizio *nx_dhcp_interface_disable* .</span><span class="sxs-lookup"><span data-stu-id="df421-185">To disable an interface for DHCP, the application can call the *nx_dhcp_interface_disable* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-186">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-186">Input Parameters</span></span>

- <span data-ttu-id="df421-187">**dhcp_ptr** Puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-187">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="df421-188">**interface_index** Indice dell'interfaccia per abilitare DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-188">**interface_index** Index of interface to enable DHCP on</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-189">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-189">Return Values</span></span>

- <span data-ttu-id="df421-190">Abilitazione DHCP **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="df421-190">**NX_SUCCESS** (0x00) Successful DHCP enable</span></span>

- <span data-ttu-id="df421-191">**NX_DHCP_NO_RECORDS_AVAILABLE** (0XA7) non è disponibile alcun record per l'abilitazione di un'altra interfaccia per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-191">**NX_DHCP_NO_RECORDS_AVAILABLE** (0xA7) No record available for another Interface to be enabled for DHCP</span></span>

- <span data-ttu-id="df421-192">Interfaccia **NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-192">**NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) Interface enabled for DHCP</span></span>

- <span data-ttu-id="df421-193">NX_PTR_ERROR (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-193">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="df421-194">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-194">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-195">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-195">Allowed From</span></span>

<span data-ttu-id="df421-196">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="df421-196">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="df421-197">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-197">Example</span></span>

```C
/* Enable DHCP on a secondary interface. It is already enabled on the primary 
   interface. NX_DHCP_CLIENT_MAX_RECORDS is set to 2. */

status =  nx_dhcp_interface_enable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface was successfully enabled. */


status = nx_dhcp_start(&my_dhcp);
/* If status is NX_SUCCESS DHCP is running on interface 0 and 1. */
```

## <a name="nx_dhcp_interface_disable"></a><span data-ttu-id="df421-198">nx_dhcp_interface_disable</span><span class="sxs-lookup"><span data-stu-id="df421-198">nx_dhcp_interface_disable</span></span>

<span data-ttu-id="df421-199">Disabilitare l'interfaccia specificata per eseguire DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-199">Disable the specified interface to run DHCP</span></span> 

### <a name="prototype"></a><span data-ttu-id="df421-200">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-200">Prototype</span></span>

```C
UINT nx_dhcp_interface_disable(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="df421-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-201">Description</span></span>

<span data-ttu-id="df421-202">Questo servizio Disabilita l'interfaccia specificata per l'esecuzione di DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-202">This service disables the specified interface for running DHCP.</span></span> <span data-ttu-id="df421-203">Reinizializza il client DHCP su questa interfaccia.</span><span class="sxs-lookup"><span data-stu-id="df421-203">It reinitializes the DHCP Client on this interface.</span></span>

<span data-ttu-id="df421-204">Per riavviare il client DHCP, l'applicazione deve riabilitare l'interfaccia utilizzando *nx_dhcp_interface_enable* e riavviare DHCP chiamando *nx_dhcp_interface_start*.</span><span class="sxs-lookup"><span data-stu-id="df421-204">To restart the DHCP Client the application must re-enable the interface using *nx_dhcp_interface_enable* and restart DHCP by calling *nx_dhcp_interface_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-205">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-205">Input Parameters</span></span>

- <span data-ttu-id="df421-206">**dhcp_ptr** Puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-206">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="df421-207">**interface_index** Indice dell'interfaccia in cui disabilitare DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-207">**interface_index** Index of interface to disable DHCP on</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-208">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-208">Return Values</span></span>

- <span data-ttu-id="df421-209">Creazione di DHCP **NX_SUCCESS** (0x00) riuscita</span><span class="sxs-lookup"><span data-stu-id="df421-209">**NX_SUCCESS** (0x00) Successful DHCP create</span></span>

- <span data-ttu-id="df421-210">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-210">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="df421-211">NX_PTR_ERROR (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-211">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="df421-212">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="df421-212">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

- <span data-ttu-id="df421-213">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-213">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-214">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-214">Allowed From</span></span>

<span data-ttu-id="df421-215">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-215">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-216">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-216">Example</span></span>

```C
/* Disable DHCP on a secondary interface.
. */

status = nx_dhcp_interface_disable(&my_dhcp, 1);
/* If status is NX_SUCCESS the interface is successfully disabled. */
```

## <a name="nx_dhcp_clear_broadcast_flag"></a><span data-ttu-id="df421-217">nx_dhcp_clear_broadcast_flag</span><span class="sxs-lookup"><span data-stu-id="df421-217">nx_dhcp_clear_broadcast_flag</span></span>

<span data-ttu-id="df421-218">Imposta il flag di trasmissione DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-218">Set the DHCP broadcast flag</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-219">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-219">Prototype</span></span>

```C
UINT nx_dhcp_clear_broadcast_flag(NX_DHCP *dhcp_ptr, UINT clear_flag);
```

### <a name="description"></a><span data-ttu-id="df421-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-220">Description</span></span>

<span data-ttu-id="df421-221">Questo servizio imposta o cancella il flag di trasmissione l'intestazione del messaggio DHCP per tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-221">This service sets or clears the broadcast flag the DHCP message header for all interfaces enabled for DHCP.</span></span> <span data-ttu-id="df421-222">Per alcuni messaggi DHCP, ad esempio DISCOVER, il flag broadcast è impostato su broadcast perché il client non dispone di un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="df421-222">For some DHCP messages (e.g. DISCOVER) the broadcast flag is set to broadcast because the Client does not have an IP address.</span></span>

<span data-ttu-id="df421-223">__clear_flag__</span><span class="sxs-lookup"><span data-stu-id="df421-223">__clear_flag__</span></span>


- <span data-ttu-id="df421-224">**NX_TRUE** flag broadcast è deselezionata (richiesta unicast risposta)</span><span class="sxs-lookup"><span data-stu-id="df421-224">**NX_TRUE** broadcast flag is cleared (request unicast response)</span></span>

- <span data-ttu-id="df421-225">Flag di broadcast **NX_FALSE** impostato (risposta broadcast richiesta)</span><span class="sxs-lookup"><span data-stu-id="df421-225">**NX_FALSE** broadcast flag is set (request broadcast response)</span></span>

<span data-ttu-id="df421-226">Questo servizio è destinato ai client DHCP che devono passare attraverso un router per accedere al server DHCP, in cui il router rifiuta l'invio di messaggi broadcast.</span><span class="sxs-lookup"><span data-stu-id="df421-226">This service is intended for DHCP Clients that must go through a router to get to the DHCP Server, where the router rejects forwarding broadcast messages.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-227">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-227">Input Parameters</span></span>

- <span data-ttu-id="df421-228">**dhcp_ptr** Puntatore al blocco di controllo DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-228">**dhcp_ptr** Pointer to DHCP control block</span></span>  

- <span data-ttu-id="df421-229">**clear_flag** Valore per cui impostare il flag di trasmissione</span><span class="sxs-lookup"><span data-stu-id="df421-229">**clear_flag** Value to set the broadcast flag to</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-230">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-230">Return Values</span></span>

- <span data-ttu-id="df421-231">Il flag di broadcast è stato aggiornato **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="df421-231">**NX_SUCCESS** (0x00) Successfully updated the broadcast flag</span></span>

- <span data-ttu-id="df421-232">NX_PTR_ERROR (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-232">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="df421-233">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="df421-233">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-234">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-234">Allowed From</span></span>

<span data-ttu-id="df421-235">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="df421-235">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="df421-236">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-236">Example</span></span>

```C
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a  
    unicast response). */
status =  nx_dhcp_clear_broadcast_flag(&my_dhcp, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated. */
```

## <a name="nx_dhcp_interface_clear_broadcast_flag"></a><span data-ttu-id="df421-237">nx_dhcp_interface_clear_broadcast_flag</span><span class="sxs-lookup"><span data-stu-id="df421-237">nx_dhcp_interface_clear_broadcast_flag</span></span>

<span data-ttu-id="df421-238">Imposta o deseleziona il flag broadcast sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="df421-238">Set or clear the broadcast flag on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-239">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-239">Prototype</span></span>

```C
UINT nx_dhcp_interface_clear_broadcast_flag(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            UINT clear_flag);
```

### <a name="description"></a><span data-ttu-id="df421-240">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-240">Description</span></span>

<span data-ttu-id="df421-241">Questo servizio consente all'applicazione host client DHCP di impostare o deselezionare il flag di trasmissione nei messaggi client DHCP per il server DHCP sull'interfaccia specificata.</span><span class="sxs-lookup"><span data-stu-id="df421-241">This service enables the DHCP Client host application to set or clear the broadcast flag in DHCP Client messages to the DHCP Server on the specified interface.</span></span> <span data-ttu-id="df421-242">Per altri dettagli, vedere **nx_dhcp_clear_broadcast_flag**</span><span class="sxs-lookup"><span data-stu-id="df421-242">For more details see **nx_dhcp_clear_broadcast_flag**</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-243">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-243">Input Parameters</span></span>

- <span data-ttu-id="df421-244">**dhcp_ptr** Puntatore al blocco di controllo DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-244">**dhcp_ptr** Pointer to DHCP control block</span></span>

- <span data-ttu-id="df421-245">**interface_index** Indice dell'interfaccia per impostare il flag di trasmissione</span><span class="sxs-lookup"><span data-stu-id="df421-245">**interface_index** Index of interface to set the broadcast flag</span></span>  

- <span data-ttu-id="df421-246">**clear_flag** Valore per cui impostare il flag di trasmissione</span><span class="sxs-lookup"><span data-stu-id="df421-246">**clear_flag** Value to set the broadcast flag to</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-247">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-247">Return Values</span></span>

- <span data-ttu-id="df421-248">Il flag di broadcast è stato aggiornato **NX_SUCCESS** (0x00)</span><span class="sxs-lookup"><span data-stu-id="df421-248">**NX_SUCCESS** (0x00) Successfully updated the broadcast flag</span></span>

- <span data-ttu-id="df421-249">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-249">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="df421-250">NX_PTR_ERROR (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-250">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="df421-251">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-251">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-252">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-252">Allowed From</span></span>

<span data-ttu-id="df421-253">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="df421-253">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="df421-254">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-254">Example</span></span>

```C
/* Send DHCP Client messages with the broadcast flag cleared (e.g. request a 
   unicast response) on a previously attached secondary interface. */

iface_index = 1;

status =  nx_dhcp_interface_clear_broadcast_flag(&my_dhcp, iface_index, NX_TRUE);

/* If status is NX_SUCCESS the DHCP Client broadcast flag is updated. */
```

## <a name="nx_dhcp_delete"></a><span data-ttu-id="df421-255">nx_dhcp_delete</span><span class="sxs-lookup"><span data-stu-id="df421-255">nx_dhcp_delete</span></span>

<span data-ttu-id="df421-256">Eliminare un'istanza DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-256">Delete a DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-257">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-257">Prototype</span></span>

```C
UINT nx_dhcp_delete(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="df421-258">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-258">Description</span></span>

<span data-ttu-id="df421-259">Questo servizio Elimina un'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-259">This service deletes a previously created DHCP instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-260">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-260">Input Parameters</span></span>

- <span data-ttu-id="df421-261">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-261">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-262">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-262">Return Values</span></span>

- <span data-ttu-id="df421-263">L'eliminazione DHCP è riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="df421-263">**NX_SUCCESS** (0x00) Successful DHCP delete.</span></span>

- <span data-ttu-id="df421-264">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-264">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="df421-265">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="df421-265">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-266">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-266">Allowed From</span></span>

<span data-ttu-id="df421-267">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-267">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-268">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-268">Example</span></span>

```C
/* Delete a DHCP instance. */
status =  nx_dhcp_delete(&my_dhcp);

/* If status is NX_SUCCESS the DHCP instance was successfully deleted. */
```

## <a name="nx_dhcp_-force_renew"></a><span data-ttu-id="df421-269">nx_dhcp_ force_renew</span><span class="sxs-lookup"><span data-stu-id="df421-269">nx_dhcp_ force_renew</span></span>

<span data-ttu-id="df421-270">Invia un messaggio di rinnovo forzato</span><span class="sxs-lookup"><span data-stu-id="df421-270">Send a force renew message</span></span> 

### <a name="prototype"></a><span data-ttu-id="df421-271">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-271">Prototype</span></span>

```C
UINT nx_dhcp force_renew(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="df421-272">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-272">Description</span></span>

<span data-ttu-id="df421-273">Questo servizio consente all'applicazione host di inviare un messaggio di rinnovo forzato su tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-273">This service enables the host application to send a force renew message on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="df421-274">Il client DHCP deve trovarsi in uno stato associato.</span><span class="sxs-lookup"><span data-stu-id="df421-274">The DHCP Client must be in a BOUND state.</span></span> <span data-ttu-id="df421-275">Questa funzione imposta lo stato su RENEW, in modo che il client DHCP tenterà di eseguire il rinnovo prima della scadenza del timeout T1.</span><span class="sxs-lookup"><span data-stu-id="df421-275">This function sets the state to RENEW such that the DHCP Client will try to renew before the T1 timeout expires.</span></span>

<span data-ttu-id="df421-276">Per inviare un rinnovo forzato a un'interfaccia specifica quando più interfacce sono abilitate per DHCP, usare *nx_dhcp_interface_force_renew*.</span><span class="sxs-lookup"><span data-stu-id="df421-276">To send a force renew on a specific interface when multiple interfaces are DHCP-enabled, use *nx_dhcp_interface_force_renew*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-277">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-277">Input Parameters</span></span>

- <span data-ttu-id="df421-278">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-278">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-279">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-279">Return Values</span></span>

- <span data-ttu-id="df421-280">**NX_SUCCESS** (0x00) ha inviato il rinnovo forzato.</span><span class="sxs-lookup"><span data-stu-id="df421-280">**NX_SUCCESS** (0x00) Successfully sent force renew.</span></span>  

- <span data-ttu-id="df421-281">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-281">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="df421-282">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="df421-282">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-283">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-283">Allowed From</span></span>

<span data-ttu-id="df421-284">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-284">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-285">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-285">Example</span></span>

```C
/* Send a force renew message from the Client. */
status =  nx_dhcp_force_renew(&my_dhcp);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired. */
```

## <a name="nx_dhcp_interface_force_renew"></a><span data-ttu-id="df421-286">nx_dhcp_interface_force_renew</span><span class="sxs-lookup"><span data-stu-id="df421-286">nx_dhcp_interface_force_renew</span></span>

<span data-ttu-id="df421-287">Invia un messaggio Force Renew sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="df421-287">Send a force renew message on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-288">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-288">Prototype</span></span>

```C
UINT nx_dhcp_interface_force_renew(NX_DHCP *dhcp_ptr,
                                    UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="df421-289">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-289">Description</span></span>

<span data-ttu-id="df421-290">Questo servizio consente all'applicazione host di inviare un messaggio Force Renew sull'interfaccia di input purché tale interfaccia sia stata abilitata per DHCP (vedere *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="df421-290">This service enables the host application to send a force renew message on the input interface as long as that interface has been enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="df421-291">Il client DHCP nell'interfaccia specificata deve essere in uno stato associato.</span><span class="sxs-lookup"><span data-stu-id="df421-291">The DHCP Client on the specified interface must be in a BOUND state.</span></span> <span data-ttu-id="df421-292">Questa funzione imposta lo stato su RENEW, in modo che il client DHCP tenterà di eseguire il rinnovo prima della scadenza del timeout T1.</span><span class="sxs-lookup"><span data-stu-id="df421-292">This function sets the state to RENEW such that the DHCP Client will try to renew before the T1 timeout expires.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-293">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-293">Input Parameters</span></span>

- <span data-ttu-id="df421-294">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-294">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-295">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-295">Return Values</span></span>

- <span data-ttu-id="df421-296">**NX_SUCCESS** (0x00) ha inviato il rinnovo forzato.</span><span class="sxs-lookup"><span data-stu-id="df421-296">**NX_SUCCESS** (0x00) Successfully sent force renew.</span></span>  

- <span data-ttu-id="df421-297">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-297">**NX_DHCP_INTERFACE_NOT_ENABLED**  (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="df421-298">NX_PTR_ERROR (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-298">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="df421-299">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-299">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-300">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-300">Allowed From</span></span>

<span data-ttu-id="df421-301">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-301">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-302">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-302">Example</span></span>

```C
/* Send a force renew message to the server on interface 1. */
status =  nx_dhcp_interface_force_renew(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP client state is the RENEWING state and the    
   DHCP Client thread task will begin renewing before T1 is expired. */
```

## <a name="nx_dhcp_packet_pool_set"></a><span data-ttu-id="df421-303">nx_dhcp_packet_pool_set</span><span class="sxs-lookup"><span data-stu-id="df421-303">nx_dhcp_packet_pool_set</span></span>

<span data-ttu-id="df421-304">Impostare il pool di pacchetti client DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-304">Set the DHCP Client packet pool</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-305">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-305">Prototype</span></span>

```C
UINT nx_dhcp_packet_pool_set(NX_DHCP *dhcp_ptr,
                            NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a><span data-ttu-id="df421-306">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-306">Description</span></span>

<span data-ttu-id="df421-307">Questo servizio consente all'applicazione di creare il pool di pacchetti client DHCP passando un puntatore a un pool di pacchetti creato in precedenza in questa chiamata al servizio.</span><span class="sxs-lookup"><span data-stu-id="df421-307">This service allows the application to create the DHCP Client packet pool by passing in a pointer to a previously created packet pool in this service call.</span></span> <span data-ttu-id="df421-308">Per utilizzare questa funzionalità, l'applicazione host deve definire NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL.</span><span class="sxs-lookup"><span data-stu-id="df421-308">To use this feature, the host application must define NX_DHCP_CLIENT_USER_CREATE_PACKET_POOL.</span></span> <span data-ttu-id="df421-309">Una volta definito, il servizio *nx_dhcp_create* non creerà il pool di pacchetti del client.</span><span class="sxs-lookup"><span data-stu-id="df421-309">When defined, the *nx_dhcp_create* service will not create the Client’s packet pool.</span></span> <span data-ttu-id="df421-310">Si noti che è consigliabile utilizzare i valori predefiniti per il payload del pool di pacchetti client DHCP, definito come NX_DHCP_PACKET_PAYLOAD in *nx_dhcp. h* quando si crea il pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="df421-310">Note that the application is recommended to use the default values for the DHCP client packet pool payload, defined as NX_DHCP_PACKET_PAYLOAD in *nx_dhcp.h* when creating the packet pool.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-311">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-311">Input Parameters</span></span>

- <span data-ttu-id="df421-312">**dhcp_ptr** Puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-312">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="df421-313">**packet_pool_ptr** Puntatore al pool di pacchetti creato in precedenza</span><span class="sxs-lookup"><span data-stu-id="df421-313">**packet_pool_ptr** Pointer to previously created packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-314">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-314">Return Values</span></span>

- <span data-ttu-id="df421-315">Il pool di pacchetti client DHCP **NX_SUCCESS** (0x00) è impostato</span><span class="sxs-lookup"><span data-stu-id="df421-315">**NX_SUCCESS** (0x00) DHCP Client packet pool is set</span></span>

- <span data-ttu-id="df421-316">Il servizio **NX_NOT_ENABLED** (0x14) non è abilitato</span><span class="sxs-lookup"><span data-stu-id="df421-316">**NX_NOT_ENABLED** (0x14) Service is not enabled</span></span>

- <span data-ttu-id="df421-317">NX_PTR_ERROR (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-317">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="df421-318">Il payload di NX_DHCP_INVALID_PAYLOAD (0x9C) è troppo piccolo</span><span class="sxs-lookup"><span data-stu-id="df421-318">NX_DHCP_INVALID_PAYLOAD (0x9C) Payload is too small</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-319">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-319">Allowed From</span></span>

<span data-ttu-id="df421-320">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="df421-320">Application code</span></span>

### <a name="example"></a><span data-ttu-id="df421-321">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-321">Example</span></span>

```C
/* Create the packet pool. */
status =  nx_packet_pool_create(&dhcp_pool, "DHCP Client Packet Pool", 
        NX_DHCP_PACKET_PAYLOAD, pointer, (15 * NX_DHCP_PACKET_PAYLOAD));

/* Create the DHCP Client. */
status =  nx_dhcp_create(&dhcp_0, &ip_0, "janetsdhcp1");

/* Set the DHCP Client packet pool. */
status =  nx_dhcp_packet_pool_set(&my_dhcp, packet_pool_ptr);
/* If status is NX_SUCCESS packet pool was successfully set. */
```

## <a name="nx_dhcp_request_client_ip"></a><span data-ttu-id="df421-322">nx_dhcp_request_client_ip</span><span class="sxs-lookup"><span data-stu-id="df421-322">nx_dhcp_request_client_ip</span></span>

<span data-ttu-id="df421-323">Imposta l'indirizzo IP richiesto per l'istanza DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-323">Set requested IP address for DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-324">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-324">Prototype</span></span>

```C
UINT nx_dhcp_request_client_ip(NX_DHCP *dhcp_ptr,
                                ULONG client_ip_address,
                                UINT skip_discover_message);
```

### <a name="description"></a><span data-ttu-id="df421-325">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-325">Description</span></span>

<span data-ttu-id="df421-326">Questo servizio imposta l'indirizzo IP per il client DHCP da richiedere dal server DHCP sulla prima interfaccia abilitata per DHCP nel record client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-326">This service sets the IP address for the DHCP Client to request from the DHCP Server on the first interface enabled for DHCP in the DHCP Client record.</span></span> <span data-ttu-id="df421-327">Se viene impostato il flag di *skip_discover_message* , il client DHCP Ignora il messaggio di individuazione e invia un messaggio di richiesta.</span><span class="sxs-lookup"><span data-stu-id="df421-327">If the *skip_discover_message* flag is set, the DHCP Client skips the Discover message and sends a Request message.</span></span>

<span data-ttu-id="df421-328">Per impostare la richiesta per un indirizzo IP specifico per i messaggi DHCP in un'interfaccia specifica, usare il servizio *nx_dhcp_interface_request_client_ip* .</span><span class="sxs-lookup"><span data-stu-id="df421-328">To set the request for a specific IP for DHCP messages on a specific interface, use the *nx_dhcp_interface_request_client_ip* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-329">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-329">Input Parameters</span></span>

- <span data-ttu-id="df421-330">**dhcp_ptr** Puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-330">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="df421-331">**client_ip_address** Indirizzo IP da richiedere dal server DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-331">**client_ip_address** IP address to request from DHCP server</span></span>

- <span data-ttu-id="df421-332">**skip_discover_message** Se true, il client DHCP invia un messaggio di richiesta</span><span class="sxs-lookup"><span data-stu-id="df421-332">**skip_discover_message** If true, DHCP Client sends Request message</span></span>  
<span data-ttu-id="df421-333">Se false, invia il messaggio di individuazione.</span><span class="sxs-lookup"><span data-stu-id="df421-333">If false, it sends the Discover message.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-334">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-334">Return Values</span></span>

- <span data-ttu-id="df421-335">È stato impostato l'indirizzo IP richiesto **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="df421-335">**NX_SUCCESS** (0x00) Requested IP address is set.</span></span>

- <span data-ttu-id="df421-336">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-336">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="df421-337">NX_PTR_ERROR (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-337">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="df421-338">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-338">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>
 
### <a name="allowed-from"></a><span data-ttu-id="df421-339">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-339">Allowed From</span></span>

<span data-ttu-id="df421-340">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-340">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-341">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-341">Example</span></span>

```C
/* Set the DHCP Client requested IP address and skip the discover message. */

status =  nx_dhcp_request_client_ip(&my_dhcp, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set. */
```

## <a name="nx_dhcp_interface_request_client_ip"></a><span data-ttu-id="df421-342">nx_dhcp_interface_request_client_ip</span><span class="sxs-lookup"><span data-stu-id="df421-342">nx_dhcp_interface_request_client_ip</span></span>

<span data-ttu-id="df421-343">Imposta l'indirizzo IP richiesto per l'istanza DHCP nell'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="df421-343">Set requested IP address for DHCP instance on specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-344">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-344">Prototype</span></span>

```C
UINT nx_dhcp_interface_request_client_ip(NX_DHCP *dhcp_ptr,
                                        UINT interface_index,
                                        ULONG client_ip_address,
                                        UINT skip_discover_message);
```

### <a name="description"></a><span data-ttu-id="df421-345">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-345">Description</span></span>

<span data-ttu-id="df421-346">Questo servizio imposta l'indirizzo IP per il client DHCP da richiedere dal server DHCP sull'interfaccia specificata, se tale interfaccia è abilitata per DHCP (vedere *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="df421-346">This service sets the IP address for the DHCP Client to request from the DHCP Server on the specified interface, if that interface is enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="df421-347">Se viene impostato il flag di *skip_discover_message* , il client DHCP Ignora il messaggio di individuazione e invia un messaggio di richiesta.</span><span class="sxs-lookup"><span data-stu-id="df421-347">If the *skip_discover_message* flag is set, the DHCP Client skips the Discover message and sends a Request message.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-348">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-348">Input Parameters</span></span>

- <span data-ttu-id="df421-349">**dhcp_ptr** Puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-349">**dhcp_ptr** Pointer to DHCP control block.</span></span>

- <span data-ttu-id="df421-350">**Interface_index** Indice dell'interfaccia su cui richiedere l'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="df421-350">**Interface_index** Index of interface to request IP address on</span></span>

- <span data-ttu-id="df421-351">**client_ip_address** Indirizzo IP da richiedere dal server DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-351">**client_ip_address** IP address to request from DHCP server</span></span>

- <span data-ttu-id="df421-352">**skip_discover_message** Se true, il client DHCP invia un messaggio di richiesta; in caso contrario, invia il messaggio di individuazione.</span><span class="sxs-lookup"><span data-stu-id="df421-352">**skip_discover_message** If true, DHCP Client sends Request message; else it sends the Discover message.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-353">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-353">Return Values</span></span>

- <span data-ttu-id="df421-354">È stato impostato l'indirizzo IP richiesto **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="df421-354">**NX_SUCCESS** (0x00) Requested IP address is set.</span></span>

- <span data-ttu-id="df421-355">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-355">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="df421-356">NX_PTR_ERROR (0x16) puntatore IP o DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-356">NX_PTR_ERROR (0x16) Invalid IP or DHCP pointer</span></span>

- <span data-ttu-id="df421-357">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-357">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>


### <a name="allowed-from"></a><span data-ttu-id="df421-358">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-358">Allowed From</span></span>

<span data-ttu-id="df421-359">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-359">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-360">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-360">Example</span></span>

```C
/* Set the DHCP Client requested IP address and skip the discover message on  
   interface 0. */
status =  nx_dhcp_interface_request_client_ip(&my_dhcp, 0, IP(192,168,0,6), NX_TRUE);

/* If status is NX_SUCCESS requested IP address was successfully set. */
```

## <a name="nx_dhcp_reinitialize"></a><span data-ttu-id="df421-361">nx_dhcp_reinitialize</span><span class="sxs-lookup"><span data-stu-id="df421-361">nx_dhcp_reinitialize</span></span>

<span data-ttu-id="df421-362">Cancella i parametri della rete client DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-362">Clear the DHCP client network parameters</span></span> 

### <a name="prototype"></a><span data-ttu-id="df421-363">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-363">Prototype</span></span>

```C
UINT nx_dhcp_reinitialize(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="df421-364">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-364">Description</span></span>

<span data-ttu-id="df421-365">Questo servizio Cancella i parametri della rete dell'applicazione host (indirizzo IP, indirizzo di rete e network mask) e cancella lo stato del client DHCP in tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-365">This service clears the host application network parameters (IP address, network address and network mask), and clears the DHCP Client state on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="df421-366">Viene usato in combinazione con *nx_dhcp_stop* e *nx_dhcp_start* per "riavviare" la macchina a stati DHCP:</span><span class="sxs-lookup"><span data-stu-id="df421-366">It is used in combination with *nx_dhcp_stop* and *nx_dhcp_start* to ‘restart’ the DHCP state machine:</span></span> 

<span data-ttu-id="df421-367">nx_dhcp_stop (&my_dhcp);</span><span class="sxs-lookup"><span data-stu-id="df421-367">nx_dhcp_stop(&my_dhcp);</span></span>  
<span data-ttu-id="df421-368">nx_dhcp_reinitialize (&my_dhcp);</span><span class="sxs-lookup"><span data-stu-id="df421-368">nx_dhcp_reinitialize(&my_dhcp);</span></span>  
<span data-ttu-id="df421-369">nx_dhcp_start (&my_dhcp);</span><span class="sxs-lookup"><span data-stu-id="df421-369">nx_dhcp_start(&my_dhcp);</span></span>


<span data-ttu-id="df421-370">Per reinizializzare il client DHCP in un'interfaccia specifica quando sono abilitate più interfacce per DHCP, usare il servizio *nx_dhcp_interface_reinitialize* .</span><span class="sxs-lookup"><span data-stu-id="df421-370">To reinitialize the DHCP Client on a specific interface when multiple interfaces are enabled for DHCP, use the *nx_dhcp_interface_reinitialize* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-371">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-371">Input Parameters</span></span>

- <span data-ttu-id="df421-372">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-372">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-373">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-373">Return Values</span></span>

- <span data-ttu-id="df421-374">Reinizializzazione del DHCP **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="df421-374">**NX_SUCCESS** (0x00) DHCP successfully reinitialized</span></span> 

- <span data-ttu-id="df421-375">NX_PTR_ERROR (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-375">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-376">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-376">Allowed From</span></span>

<span data-ttu-id="df421-377">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-377">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-378">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-378">Example</span></span>

```C
/* Reinitialize the previously started DHCP client. */
status =  nx_dhcp_reinitialize(&my_dhcp);

/* If status is NX_SUCCESS the host application successfully reinitialized its 
network parameters and DHCP client state. */
```

## <a name="nx_dhcp_interface_reinitialize"></a><span data-ttu-id="df421-379">nx_dhcp_interface_reinitialize</span><span class="sxs-lookup"><span data-stu-id="df421-379">nx_dhcp_interface_reinitialize</span></span>

<span data-ttu-id="df421-380">Cancella i parametri di rete del client DHCP nell'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="df421-380">Clear the DHCP client network parameters on the specified interface</span></span> 

### <a name="prototype"></a><span data-ttu-id="df421-381">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-381">Prototype</span></span>

```C
UINT nx_dhcp_interface_reinitialize(NX_DHCP *dhcp_ptr,
                                    UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="df421-382">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-382">Description</span></span>

<span data-ttu-id="df421-383">Questo servizio Cancella i parametri di rete (indirizzo IP, indirizzo di rete e network mask) nell'interfaccia specificata se tale interfaccia è abilitata per DHCP (vedere *nx_dhcp_interface_enable*).</span><span class="sxs-lookup"><span data-stu-id="df421-383">This service clears the network parameters (IP address, network address and network mask) on the specified interface if that interface is enabled for DHCP (see *nx_dhcp_interface_enable*).</span></span> <span data-ttu-id="df421-384">Per ulteriori informazioni, vedere *nx_dhcp_reinitialize* .</span><span class="sxs-lookup"><span data-stu-id="df421-384">See *nx_dhcp_reinitialize* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-385">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-385">Input Parameters</span></span>

- <span data-ttu-id="df421-386">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza</span><span class="sxs-lookup"><span data-stu-id="df421-386">**dhcp_ptr** Pointer to previously created DHCP instance</span></span>

- <span data-ttu-id="df421-387">**interface_index** Indice dell'interfaccia da reinizializzare.</span><span class="sxs-lookup"><span data-stu-id="df421-387">**interface_index** Index of interface to reinitialize.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-388">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-388">Return Values</span></span>

- <span data-ttu-id="df421-389">L'interfaccia **NX_SUCCESS** (0x00) è stata reinizializzata</span><span class="sxs-lookup"><span data-stu-id="df421-389">**NX_SUCCESS** (0x00) Interface successfully reinitialized</span></span>

- <span data-ttu-id="df421-390">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-390">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="df421-391">NX_PTR_ERROR (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-391">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="df421-392">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="df421-392">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="df421-393">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-393">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-394">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-394">Allowed From</span></span>

<span data-ttu-id="df421-395">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-395">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-396">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-396">Example</span></span>

```C
/* Reinitialize the previously started DHCP client on interface 1. */
status =  nx_dhcp_interface_reinitialize(&my_dhcp, 1);

/* If status is NX_SUCCESS the host application successfully reinitialized its 
network parameters and DHCP client state. */
```

## <a name="nx_dhcp_release"></a><span data-ttu-id="df421-397">nx_dhcp_release</span><span class="sxs-lookup"><span data-stu-id="df421-397">nx_dhcp_release</span></span>

<span data-ttu-id="df421-398">Rilascia indirizzo IP con lease</span><span class="sxs-lookup"><span data-stu-id="df421-398">Release Leased IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-399">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-399">Prototype</span></span>

```C
UINT nx_dhcp_release(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="df421-400">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-400">Description</span></span>

<span data-ttu-id="df421-401">Questo servizio rilascia l'indirizzo IP ottenuto da un server DHCP inviando il messaggio di rilascio a tale server.</span><span class="sxs-lookup"><span data-stu-id="df421-401">This service releases the IP address obtained from a DHCP server by sending the RELEASE message to that server.</span></span> <span data-ttu-id="df421-402">Quindi reinizializza il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-402">It then reinitializes the DHCP Client.</span></span> <span data-ttu-id="df421-403">Questo servizio viene applicato a tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-403">This service is applied to all interfaces enabled for DHCP.</span></span>

<span data-ttu-id="df421-404">L'applicazione può riavviare il client DHCP chiamando *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="df421-404">The application can restart the DHCP Client by calling *nx_dhcp_start*.</span></span>

<span data-ttu-id="df421-405">Per rilasciare un indirizzo al server DHCP in un'interfaccia specifica, usare il servizio *nx_dhcp_interface_release*</span><span class="sxs-lookup"><span data-stu-id="df421-405">To release an address back to the DHCP server on a specific interface, use the *nx_dhcp_interface_release* service</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-406">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-406">Input Parameters</span></span>

- <span data-ttu-id="df421-407">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-407">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-408">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-408">Return Values</span></span>

- <span data-ttu-id="df421-409">**NX_SUCCESS** (0x00) versione DHCP riuscita.</span><span class="sxs-lookup"><span data-stu-id="df421-409">**NX_SUCCESS** (0x00) Successful DHCP release.</span></span>  

- <span data-ttu-id="df421-410">**NX_DHCP_NOT_BOUND** (0X94) l'indirizzo IP non è stato concesso in lease, quindi non può essere rilasciato.</span><span class="sxs-lookup"><span data-stu-id="df421-410">**NX_DHCP_NOT_BOUND** (0x94) The IP address has not been leased so it can’t be released.</span></span>

- <span data-ttu-id="df421-411">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-411">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="df421-412">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="df421-412">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-413">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-413">Allowed From</span></span>

<span data-ttu-id="df421-414">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-414">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-415">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-415">Example</span></span>

```C
/* Release the previously leased IP address. */
status =  nx_dhcp_release(&my_dhcp);

/* If status is NX_SUCCESS the previous IP lease was successfully released. */
```

## <a name="nx_dhcp_interface_release"></a><span data-ttu-id="df421-416">nx_dhcp_interface_release</span><span class="sxs-lookup"><span data-stu-id="df421-416">nx_dhcp_interface_release</span></span>

<span data-ttu-id="df421-417">Rilasciare l'indirizzo IP sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="df421-417">Release IP address on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-418">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-418">Prototype</span></span>

```C
UINT nx_dhcp_interface_release(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="df421-419">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-419">Description</span></span>

<span data-ttu-id="df421-420">Questo servizio rilascia l'indirizzo IP ottenuto da un server DHCP sull'interfaccia specificata e reinizializza il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-420">This service releases the IP address obtained from a DHCP server on the specified interface and reinitializes the DHCP Client.</span></span> <span data-ttu-id="df421-421">Il client DHCP può essere riavviato chiamando *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="df421-421">The DHCP Client can be restarted by calling *nx_dhcp_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-422">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-422">Input Parameters</span></span>

- <span data-ttu-id="df421-423">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-423">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-424">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-424">Return Values</span></span>

- <span data-ttu-id="df421-425">**NX_SUCCESS** (0x00) versione DHCP riuscita.</span><span class="sxs-lookup"><span data-stu-id="df421-425">**NX_SUCCESS** (0x00) Successful DHCP release.</span></span>

- <span data-ttu-id="df421-426">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-426">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="df421-427">**NX_DHCP_NOT_BOUND** (0X94) l'indirizzo IP non è stato concesso in lease, quindi non può essere rilasciato.</span><span class="sxs-lookup"><span data-stu-id="df421-427">**NX_DHCP_NOT_BOUND** (0x94) The IP address has not been leased so it can’t be released.</span></span>

- <span data-ttu-id="df421-428">NX_PTR_ERROR (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-428">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="df421-429">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="df421-429">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="df421-430">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-430">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-431">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-431">Allowed From</span></span>

<span data-ttu-id="df421-432">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-432">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-433">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-433">Example</span></span>

```C
/* Release the previously leased IP address on interface 1. */
status =  nx_dhcp_interface_release(&my_dhcp, 1);

/* If status is NX_SUCCESS the previous IP lease was successfully released. */
```

## <a name="nx_dhcp_decline"></a><span data-ttu-id="df421-434">nx_dhcp_decline</span><span class="sxs-lookup"><span data-stu-id="df421-434">nx_dhcp_decline</span></span>

<span data-ttu-id="df421-435">Rifiuta indirizzo IP dal server DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-435">Decline IP address from DHCP Server</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-436">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-436">Prototype</span></span>

```C
UINT nx_dhcp_decline(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="df421-437">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-437">Description</span></span>

<span data-ttu-id="df421-438">Questo servizio rifiuta un indirizzo IP con lease dal server DHCP in tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-438">This service declines an IP address leased from the DHCP server on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="df421-439">Se viene definito NX_DHCP_CLIENT_ SEND_ ARP_PROBE, il client DHCP invierà un messaggio di rifiuto se rileva che l'indirizzo IP è già in uso.</span><span class="sxs-lookup"><span data-stu-id="df421-439">If NX_DHCP_CLIENT_ SEND_ ARP_PROBE is defined, the DHCP Client will send a DECLINE message if it detects that the IP address is already in use.</span></span> <span data-ttu-id="df421-440">Per ulteriori informazioni sulla configurazione del probe ARP nel client DHCP NetX, vedere **Probe ARP** nel capitolo 1.</span><span class="sxs-lookup"><span data-stu-id="df421-440">See **ARP Probes** in Chapter One for more information on ARP probe configuration in the NetX DHCP Client.</span></span>

<span data-ttu-id="df421-441">L'applicazione può utilizzare questo servizio per rifiutare il proprio indirizzo IP se rileva che l'indirizzo è in uso in altri modi.</span><span class="sxs-lookup"><span data-stu-id="df421-441">The application can use this service to decline its IP address if it discovers the address is in use by other means.</span></span>

<span data-ttu-id="df421-442">Questo servizio reinizializza il client DHCP in modo che possa essere riavviato chiamando *nx_dhcp_start*.</span><span class="sxs-lookup"><span data-stu-id="df421-442">This service reinitializes the DHCP Client to that it can be restarted by calling *nx_dhcp_start*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-443">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-443">Input Parameters</span></span>

- <span data-ttu-id="df421-444">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-444">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-445">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-445">Return Values</span></span>

- <span data-ttu-id="df421-446">Il rifiuto di **NX_SUCCESS** (0x00) è stato inviato</span><span class="sxs-lookup"><span data-stu-id="df421-446">**NX_SUCCESS** (0x00) Decline successfully sent</span></span>  

- <span data-ttu-id="df421-447">**NX_DHCP_NOT_STARTED** (0X96) l'istanza DHCP non è stata avviata</span><span class="sxs-lookup"><span data-stu-id="df421-447">**NX_DHCP_NOT_STARTED** (0x96) The DHCP instance not started</span></span>

- <span data-ttu-id="df421-448">NX_PTR_ERROR (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-448">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="df421-449">NX_CALLER_ERROR (0x11) chiamante non valido di questo servizio</span><span class="sxs-lookup"><span data-stu-id="df421-449">NX_CALLER_ERROR (0x11) Invalid caller of this service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-450">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-450">Allowed From</span></span>

<span data-ttu-id="df421-451">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-451">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-452">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-452">Example</span></span>

```C
/* Decline the IP address offered by the DHCP server. */
status =  nx_dhcp_decline(&my_dhcp);

/* If status is NX_SUCCESS the previous IP address decline message was 
   successfully trasnmitted. */
```

## <a name="nx_dhcp_interface_decline"></a><span data-ttu-id="df421-453">nx_dhcp_interface_decline</span><span class="sxs-lookup"><span data-stu-id="df421-453">nx_dhcp_interface_decline</span></span>

<span data-ttu-id="df421-454">Rifiutare l'indirizzo IP dal server DHCP sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="df421-454">Decline IP address from DHCP Server on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-455">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-455">Prototype</span></span>

```C
UINT nx_dhcp_interface_decline(NX_DHCP *dhcp_ptr,
                                UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="df421-456">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-456">Description</span></span>

<span data-ttu-id="df421-457">Questo servizio invia il messaggio di rifiuto al server per rifiutare un indirizzo IP assegnato dal server DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-457">This service sends the DECLINE message to the server to decline an IP address assigned by the DHCP server.</span></span> <span data-ttu-id="df421-458">Reinizializza inoltre il client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-458">It also reinitializes the DHCP Client.</span></span> <span data-ttu-id="df421-459">Per ulteriori informazioni, vedere *nx_dhcp_decline* .</span><span class="sxs-lookup"><span data-stu-id="df421-459">See *nx_dhcp_decline* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-460">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-460">Input Parameters</span></span>

- <span data-ttu-id="df421-461">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-461">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="df421-462">**Interface_index** Indice dell'interfaccia per rifiutare l'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="df421-462">**Interface_index** Index of interface to decline IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-463">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-463">Return Values</span></span>

- <span data-ttu-id="df421-464">**NX_SUCCESS** (0x00) messaggio di rifiuto DHCP inviato</span><span class="sxs-lookup"><span data-stu-id="df421-464">**NX_SUCCESS** (0x00) DHCP decline message sent</span></span>  

- <span data-ttu-id="df421-465">Client DHCP **NX_DHCP_NOT_BOUND** (0x94) non associato</span><span class="sxs-lookup"><span data-stu-id="df421-465">**NX_DHCP_NOT_BOUND** (0x94) DHCP Client not bound</span></span>

- <span data-ttu-id="df421-466">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-466">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="df421-467">NX_PTR_ERROR (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-467">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="df421-468">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="df421-468">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="df421-469">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-469">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-470">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-470">Allowed From</span></span>

<span data-ttu-id="df421-471">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-471">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-472">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-472">Example</span></span>
```C
/* Decline the IP address offered by the DHCP server on interface 2. */
status =  nx_dhcp_interface_decline(&my_dhcp, 2);

/* If status is NX_SUCCESS the previous IP address decline message was
   successfully trasnmitted. */
```

## <a name="nx_dhcp_send_request"></a><span data-ttu-id="df421-473">nx_dhcp_send_request</span><span class="sxs-lookup"><span data-stu-id="df421-473">nx_dhcp_send_request</span></span>

<span data-ttu-id="df421-474">Invia messaggio DHCP al server</span><span class="sxs-lookup"><span data-stu-id="df421-474">Send DHCP message to Server</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-475">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-475">Prototype</span></span>

```C
UINT nx_dhcp_send_request(NX_DHCP *dhcp_ptr, UINT dhcp_message_type);
```

### <a name="description"></a><span data-ttu-id="df421-476">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-476">Description</span></span>

<span data-ttu-id="df421-477">Questo servizio invia il messaggio DHCP specificato al server DHCP nella prima interfaccia abilitata per DHCP trovato nel record client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-477">This service sends the specified DHCP message to the DHCP server on the first interface enabled for DHCP found in the DHCP Client record.</span></span> <span data-ttu-id="df421-478">Per inviare un messaggio di rilascio o di rifiuto, l'applicazione deve utilizzare rispettivamente i servizi di *nx_dhcp [_interface] _Release*() o *nx_dhcp_interface_decline ()* .</span><span class="sxs-lookup"><span data-stu-id="df421-478">To send a RELEASE or DECLINE message, the application must use the *nx_dhcp[_interface]_release*() or *nx_dhcp_interface_decline()* services respectively.</span></span>

<span data-ttu-id="df421-479">È necessario avviare il client DHCP per l'utilizzo di questo servizio, ad eccezione dell'invio del INFORM_REQUEST tipo di messaggio.</span><span class="sxs-lookup"><span data-stu-id="df421-479">The DHCP Client must be started to use this service except for sending the INFORM_REQUEST message type.</span></span>

> [!NOTE] 
> <span data-ttu-id="df421-480">Questo servizio non è destinato all'applicazione host a "unità" della macchina a stati client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-480">This service is not intended for the host application to ‘drive’ the DHCP Client state machine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-481">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-481">Input Parameters</span></span>

- <span data-ttu-id="df421-482">**dhcp_ptr** Puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-482">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="df421-483">**dhcp_message_type** Richiesta messaggio (definita in *nx_dhcp. h*)</span><span class="sxs-lookup"><span data-stu-id="df421-483">**dhcp_message_type** Message request (defined in *nx_dhcp.h*)</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-484">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-484">Return Values</span></span>

- <span data-ttu-id="df421-485">**NX_SUCCESS** (0x00) messaggio DHCP inviato</span><span class="sxs-lookup"><span data-stu-id="df421-485">**NX_SUCCESS** (0x00) DHCP message sent</span></span>  

- <span data-ttu-id="df421-486">Indice di interfaccia **NX_DHCP_NOT_STARTED** (0X96) non valido</span><span class="sxs-lookup"><span data-stu-id="df421-486">**NX_DHCP_NOT_STARTED** (0x96) Invalid interface index</span></span>

- <span data-ttu-id="df421-487">**NX_DHCP_INVALID_MESSAGE** (0x9B) tipo di messaggio non valido da inviare</span><span class="sxs-lookup"><span data-stu-id="df421-487">**NX_DHCP_INVALID_MESSAGE** (0x9B) Invalid message type to send</span></span>

- <span data-ttu-id="df421-488">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="df421-488">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-489">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-489">Allowed From</span></span>

<span data-ttu-id="df421-490">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-490">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-491">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-491">Example</span></span>

```C
/* Send the DHCP INFORM REQUEST message to the server. */

status =  nx_dhcp_send_request(&my_dhcp, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent. */
```

## <a name="nx_dhcp_interface_send_request"></a><span data-ttu-id="df421-492">nx_dhcp_interface_send_request</span><span class="sxs-lookup"><span data-stu-id="df421-492">nx_dhcp_interface_send_request</span></span>

<span data-ttu-id="df421-493">Invia messaggio DHCP al server in un'interfaccia specifica</span><span class="sxs-lookup"><span data-stu-id="df421-493">Send DHCP message to Server on a specific interface</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-494">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-494">Prototype</span></span>

```C
UINT nx_dhcp_interface_send_request(NX_DHCP *dhcp_ptr,
                                    UINT interface_index,
                                    UINT dhcp_message_type);
```

### <a name="description"></a><span data-ttu-id="df421-495">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-495">Description</span></span>

<span data-ttu-id="df421-496">Questo servizio invia un messaggio al server DHCP sull'interfaccia specificata se tale interfaccia è abilitata per DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-496">This service sends a message to the DHCP server on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="df421-497">Per inviare un messaggio di rilascio o di rifiuto, l'applicazione deve utilizzare rispettivamente i servizi di *nx_dhcp [_interface] _Release*() o *nx_dhcp_interface_decline ()* .</span><span class="sxs-lookup"><span data-stu-id="df421-497">To send a RELEASE or DECLINE message, the application must use the *nx_dhcp[_interface]_release*() or *nx_dhcp_interface_decline()* services respectively.</span></span>

<span data-ttu-id="df421-498">È necessario avviare il client DHCP per l'utilizzo di questo servizio, ad eccezione dell'invio del tipo di messaggio di richiesta di comunicazione DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-498">The DHCP Client must be started to use this service except for sending the DHCP INFORM REQUEST message type.</span></span>

<span data-ttu-id="df421-499">Questo servizio non è destinato all'applicazione host a "unità" della macchina a stati client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-499">This service is not intended for the host application to ‘drive’ the DHCP Client state machine.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-500">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-500">Input Parameters</span></span>

- <span data-ttu-id="df421-501">**dhcp_ptr** Puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-501">**dhcp_ptr** Pointer to DHCP control block.</span></span>

- <span data-ttu-id="df421-502">**Interface_index** Indice dell'interfaccia su cui inviare il messaggio</span><span class="sxs-lookup"><span data-stu-id="df421-502">**Interface_index** Index of interface to send message on</span></span>  

- <span data-ttu-id="df421-503">**dhcp_message_type** Richiesta messaggio (definita in *nx_dhcp. h*)</span><span class="sxs-lookup"><span data-stu-id="df421-503">**dhcp_message_type** Message request (defined in *nx_dhcp.h*)</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-504">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-504">Return Values</span></span>

- <span data-ttu-id="df421-505">**NX_SUCCESS** (0x00) messaggio DHCP inviato</span><span class="sxs-lookup"><span data-stu-id="df421-505">**NX_SUCCESS** (0x00) DHCP message sent</span></span>  

- <span data-ttu-id="df421-506">Indice di interfaccia **NX_DHCP_NOT_STARTED** (0X96) non valido</span><span class="sxs-lookup"><span data-stu-id="df421-506">**NX_DHCP_NOT_STARTED** (0x96) Invalid interface index</span></span>

- <span data-ttu-id="df421-507">**NX_DHCP_INVALID_MESSAGE** (0x9B) tipo di messaggio non valido da inviare</span><span class="sxs-lookup"><span data-stu-id="df421-507">**NX_DHCP_INVALID_MESSAGE** (0x9B) Invalid message type to send</span></span>

- <span data-ttu-id="df421-508">Interfaccia **NX_DHCP_INTERFACE_NOT_ENABLED** (0xa4) non abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-508">**NX_DHCP_INTERFACE_NOT_ENABLED** (0xA4) Interface not enabled for DHCP</span></span>

- <span data-ttu-id="df421-509">NX_PTR_ERROR (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-509">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="df421-510">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="df421-510">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="df421-511">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-511">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-512">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-512">Allowed From</span></span>

<span data-ttu-id="df421-513">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-513">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-514">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-514">Example</span></span>

```C
/* Send the INFORM REQUEST message to the server on the primary interface. */

status =  nx_dhcp_interface_send_request(&my_dhcp, 0, NX_DHCP_TYPE_DHCPINFORM);
/* If status is NX_SUCCESS a DHCP message was successfully sent. */
```

## <a name="nx_dhcp_server_address_get"></a><span data-ttu-id="df421-515">nx_dhcp_server_address_get</span><span class="sxs-lookup"><span data-stu-id="df421-515">nx_dhcp_server_address_get</span></span>

<span data-ttu-id="df421-516">Ottenere l'indirizzo IP del server DHCP del client DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-516">Get the DHCP Client’s DHCP server IP address</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-517">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-517">Prototype</span></span>

```C
UINT nx_dhcp_server_address_get(NX_DHCP *dhcp_ptr,
                                ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="df421-518">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-518">Description</span></span>

<span data-ttu-id="df421-519">Questo servizio recupera l'indirizzo IP del server DHCP client DHCP nella prima interfaccia abilitata per DHCP trovato nel record client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-519">This service retrieves the DHCP Client DHCP server IP address on the first interface enabled for DHCP found in the DHCP Client record.</span></span> <span data-ttu-id="df421-520">Il chiamante può utilizzare questo servizio solo dopo che il client DHCP è associato a un indirizzo IP assegnato dal server DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-520">The caller can only use this service after the DHCP Client is bound to an IP address assigned by the DHCP Server.</span></span> <span data-ttu-id="df421-521">L'applicazione host può utilizzare il servizio *nx_ip_status_check* per verificare che l'indirizzo IP sia impostato oppure utilizzare l' *nx_dhcp_state_change_notify* ed eseguire una query sullo stato del client DHCP NX_DHCP_STATE_BOUND.</span><span class="sxs-lookup"><span data-stu-id="df421-521">The host application can use the *nx_ip_status_check* service to verify IP address is set, or it can use the *nx_dhcp_state_change_notify* and query the DHCP Client state is NX_DHCP_STATE_BOUND.</span></span> <span data-ttu-id="df421-522">Per ulteriori informazioni sull'impostazione della funzione di callback di modifica dello stato, vedere *nx_dhcp_state_change_notify* .</span><span class="sxs-lookup"><span data-stu-id="df421-522">See *nx_dhcp_state_change_notify* for more details about setting the state change callback function.</span></span>

<span data-ttu-id="df421-523">Per trovare il server DHCP in un'interfaccia specifica quando sono abilitate più interfacce per il client DHCP, usare il servizio *nx_dhcp_interface_server_address_get*</span><span class="sxs-lookup"><span data-stu-id="df421-523">To find the DHCP server on a specific interface when multiple interfaces are enabled for DHCP Client, use the *nx_dhcp_interface_server_address_get* service</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-524">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-524">Input Parameters</span></span>

- <span data-ttu-id="df421-525">**dhcp_ptr** Puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-525">**dhcp_ptr** Pointer to DHCP control block.</span></span>

- <span data-ttu-id="df421-526">**server_address** Puntatore all'indirizzo IP del server</span><span class="sxs-lookup"><span data-stu-id="df421-526">**server_address** Pointer to server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-527">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-527">Return Values</span></span>

- <span data-ttu-id="df421-528">Indirizzo server DHCP **NX_SUCCESS** (0x00) restituito</span><span class="sxs-lookup"><span data-stu-id="df421-528">**NX_SUCCESS** (0x00) DHCP server address returned</span></span>

- <span data-ttu-id="df421-529">Puntatore di input NX_PTR_ERROR (0x16) non valido</span><span class="sxs-lookup"><span data-stu-id="df421-529">NX_PTR_ERROR (0x16) Invalid input pointer</span></span>

- <span data-ttu-id="df421-530">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="df421-530">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-531">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-531">Allowed From</span></span>

<span data-ttu-id="df421-532">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-532">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-533">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-533">Example</span></span>

```C
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. 
/* void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter. */
    state_changes++;

    if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
    {
            status = nx_dhcp_server_address_get(&dhcp_0, &server_address);
    }
```

## <a name="nx_dhcp_interface_server_address_get"></a><span data-ttu-id="df421-534">nx_dhcp_interface_server_address_get</span><span class="sxs-lookup"><span data-stu-id="df421-534">nx_dhcp_interface_server_address_get</span></span>

<span data-ttu-id="df421-535">Ottenere l'indirizzo IP del server DHCP del client DHCP nell'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="df421-535">Get the DHCP Client’s DHCP server IP address on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-536">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-536">Prototype</span></span>

```C
UINT nx_dhcp_interface_server_address_get(NX_DHCP *dhcp_ptr,
                                            UINT interface_index,
                                            ULONG server_address);
```

### <a name="description"></a><span data-ttu-id="df421-537">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-537">Description</span></span>

<span data-ttu-id="df421-538">Questo servizio recupera l'indirizzo IP del server DHCP client DHCP nell'interfaccia specificata se tale interfaccia è abilitata per DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-538">This service retrieves the DHCP Client DHCP server IP address on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="df421-539">Il client DHCP deve essere nello stato associato.</span><span class="sxs-lookup"><span data-stu-id="df421-539">The DHCP Client must be in the Bound state.</span></span> <span data-ttu-id="df421-540">Dopo l'avvio del client DHCP su tale interfaccia, l'applicazione host può utilizzare il servizio *nx_ip_status_check* per verificare che l'indirizzo IP sia impostato oppure utilizzare il callback di modifica dello stato del client DHCP ed eseguire una query sullo stato del client DHCP NX_DHCP_STATE_BOUND.</span><span class="sxs-lookup"><span data-stu-id="df421-540">After starting the DHCP Client on that interface, the host application can either use the *nx_ip_status_check* service to verify the IP address is set, or it can use the DHCP Client state change callback and query the DHCP Client state is NX_DHCP_STATE_BOUND.</span></span> <span data-ttu-id="df421-541">Per ulteriori informazioni sull'impostazione della funzione di callback di modifica dello stato, vedere *nx_dhcp_state_change_notify* .</span><span class="sxs-lookup"><span data-stu-id="df421-541">See *nx_dhcp_state_change_notify* for more details about setting the state change callback function.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-542">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-542">Input Parameters</span></span>

- <span data-ttu-id="df421-543">**dhcp_ptr** Puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-543">**dhcp_ptr** Pointer to DHCP control block.</span></span>

- <span data-ttu-id="df421-544">**Interface_index** Indice dell'interfaccia per ottenere l'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="df421-544">**Interface_index** Index of interface to obtain IP address</span></span>  

- <span data-ttu-id="df421-545">**server_address** Puntatore all'indirizzo IP del server</span><span class="sxs-lookup"><span data-stu-id="df421-545">**server_address** Pointer to server IP address</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-546">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-546">Return Values</span></span>

- <span data-ttu-id="df421-547">Indirizzo server DHCP **NX_SUCCESS** (0x00) restituito</span><span class="sxs-lookup"><span data-stu-id="df421-547">**NX_SUCCESS** (0x00) DHCP server address returned</span></span>

- <span data-ttu-id="df421-548">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) non sono abilitate interfacce per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-548">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) No interfaces enabled for DHCP</span></span>

- <span data-ttu-id="df421-549">Client DHCP **NX_DHCP_NOT_BOUND** (0x94) non associato</span><span class="sxs-lookup"><span data-stu-id="df421-549">**NX_DHCP_NOT_BOUND** (0x94) DHCP Client not bound</span></span>

- <span data-ttu-id="df421-550">NX_PTR_ERROR (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-550">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

- <span data-ttu-id="df421-551">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="df421-551">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

- <span data-ttu-id="df421-552">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-552">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-553">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-553">Allowed From</span></span>

<span data-ttu-id="df421-554">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-554">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-555">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-555">Example</span></span>

```C
/* Use the state change notify service to determine the Client transition to the 
bound state and get its DHCP server IP address. 
/* void dhcp_state_change(NX_DHCP *dhcp_ptr, UCHAR new_state)
{

ULONG server_address;
UINT  status;

/* Increment state changes counter. */
    state_changes++;

    /* Get the DHCP server IP address on interface 1 */
    if (dhcp_0.nx_dhcp_state == NX_DHCP_STATE_BOUND)
    {
            status = nx_dhcp_interface_server_address_get(&dhcp_0, 1, 
                                                    &server_address);
    }
```

## <a name="nx_dhcp_set_interface_index"></a><span data-ttu-id="df421-556">nx_dhcp_set_interface_index</span><span class="sxs-lookup"><span data-stu-id="df421-556">nx_dhcp_set_interface_index</span></span>

<span data-ttu-id="df421-557">Impostare l'interfaccia di rete per l'istanza DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-557">Set network interface for DHCP instance</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-558">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-558">Prototype</span></span>

```C
UINT nx_dhcp_set_interface_index(NX_DHCP *dhcp_ptr, UINT index);
```

### <a name="description"></a><span data-ttu-id="df421-559">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-559">Description</span></span>

<span data-ttu-id="df421-560">Questo servizio imposta l'interfaccia di rete per l'istanza DHCP per la connessione al server DHCP in quando viene eseguito il client DHCP configurato per una singola interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="df421-560">This service sets the network interface for the DHCP instance to connect to the DHCP Server on when running DHCP Client configured for a single network interface.</span></span>

<span data-ttu-id="df421-561">Per impostazione predefinita, il client DHCP viene eseguito sull'interfaccia principale.</span><span class="sxs-lookup"><span data-stu-id="df421-561">By default the DHCP Client runs on the primary interface.</span></span> <span data-ttu-id="df421-562">Per eseguire DHCP in un servizio secondario, utilizzare questo servizio per impostare l'interfaccia secondaria come interfaccia client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-562">To run DHCP on a secondary service, use this service to set the secondary interface as the DHCP Client interface.</span></span> <span data-ttu-id="df421-563">In precedenza, l'applicazione deve registrare l'interfaccia specificata nell'istanza IP utilizzando il servizio *nx_ip_interface_attach* .</span><span class="sxs-lookup"><span data-stu-id="df421-563">The application must previously register the specified interface to the IP instance using the *nx_ip_interface_attach* service.</span></span>

<span data-ttu-id="df421-564">Si noti che questo servizio è destinato alle applicazioni che intendono eseguire il client DHCP su una sola interfaccia.</span><span class="sxs-lookup"><span data-stu-id="df421-564">Note that this service is intended for applications that intend to run the DHCP Client on only one interface.</span></span> <span data-ttu-id="df421-565">Per eseguire DHCP su più interfacce, vedere *nx_dhcp_interface_enable* per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="df421-565">To run DHCP on multiple interfaces see *nx_dhcp_interface_enable* for more details.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-566">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-566">Input Parameters</span></span>

- <span data-ttu-id="df421-567">**dhcp_ptr** Puntatore al blocco di controllo DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-567">**dhcp_ptr** Pointer to DHCP control block.</span></span>  

- <span data-ttu-id="df421-568">**Indice** di Indice dell'interfaccia di rete del dispositivo</span><span class="sxs-lookup"><span data-stu-id="df421-568">**index** Index of device network interface</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-569">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-569">Return Values</span></span>

- <span data-ttu-id="df421-570">L'interfaccia **NX_SUCCESS** (0x00) è stata impostata correttamente.</span><span class="sxs-lookup"><span data-stu-id="df421-570">**NX_SUCCESS** (0x00) Interface is successfully set.</span></span>

- <span data-ttu-id="df421-571">L'interfaccia di rete **NX_INVALID_INTERFACE** (0X4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-571">**NX_INVALID_INTERFACE** (0x4C) Invalid network interface</span></span>

- <span data-ttu-id="df421-572">Interfaccia **NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) abilitata per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-572">**NX_DHCP_INTERFACE_ALREADY_ENABLED** (0xA3) Interface enabled for DHCP</span></span>

- <span data-ttu-id="df421-573">**NX_DHCP_NO_RECORDS_AVAILABLE** (0XA7) nessun record disponibile per un altro</span><span class="sxs-lookup"><span data-stu-id="df421-573">**NX_DHCP_NO_RECORDS_AVAILABLE** (0xA7) No record available for another</span></span>

- <span data-ttu-id="df421-574">NX_PTR_ERROR (0x16) puntatore DHCP non valido</span><span class="sxs-lookup"><span data-stu-id="df421-574">NX_PTR_ERROR (0x16) Invalid DHCP pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-575">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-575">Allowed From</span></span>

<span data-ttu-id="df421-576">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-576">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-577">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-577">Example</span></span>

```C
/* Set the DHCP Client interface to the secondary interface (index 1). */
status =  nx_dhcp_set_interface_index(&my_dhcp, 1);
/* If status is NX_SUCCESS a DHCP interface was successfully set. */
```

## <a name="nx_dhcp_start"></a><span data-ttu-id="df421-578">nx_dhcp_start</span><span class="sxs-lookup"><span data-stu-id="df421-578">nx_dhcp_start</span></span>

<span data-ttu-id="df421-579">Avviare l'elaborazione DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-579">Start DHCP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-580">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-580">Prototype</span></span>

```C
UINT nx_dhcp_start(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="df421-581">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-581">Description</span></span>

<span data-ttu-id="df421-582">Questo servizio avvia l'elaborazione DHCP su tutte le interfacce abilitate per DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-582">This service starts DHCP processing on all interfaces enabled for DHCP.</span></span> <span data-ttu-id="df421-583">Per impostazione predefinita, l'interfaccia primaria è abilitata per DHCP quando l'applicazione chiama *nx_dhcp_create.*</span><span class="sxs-lookup"><span data-stu-id="df421-583">By default the primary interface is enabled for DHCP when the application calls *nx_dhcp_create.*</span></span>

<span data-ttu-id="df421-584">Per verificare quando l'istanza IP è associata a un indirizzo IP sull'interfaccia client DHCP, usare *nx_ip_status_check* per vedere Verificare che l'indirizzo IP sia valido.</span><span class="sxs-lookup"><span data-stu-id="df421-584">To verify when the IP instance is bound to an IP address on the DHCP Client interface, use *nx_ip_status_check* to see confirm the IP address is valid.</span></span>

<span data-ttu-id="df421-585">Se sono presenti altre interfacce che eseguono già DHCP, il servizio non le influirà.</span><span class="sxs-lookup"><span data-stu-id="df421-585">If there are other interfaces already running DHCP, this service will not affect them.</span></span>

<span data-ttu-id="df421-586">Per avviare DHCP in un'interfaccia specifica quando sono abilitate più interfacce, usare il servizio *nx_dhcp_interface_start* .</span><span class="sxs-lookup"><span data-stu-id="df421-586">To start DHCP on a specific interface when multiple interfaces are enabled, use the *nx_dhcp_interface_start* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-587">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-587">Input Parameters</span></span>

- <span data-ttu-id="df421-588">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-588">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-589">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-589">Return Values</span></span>

- <span data-ttu-id="df421-590">Avvio DHCP **NX_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="df421-590">**NX_SUCCESS** (0x00) Successful DHCP start.</span></span>  

- <span data-ttu-id="df421-591">**NX_DHCP_ALREADY_STARTED** DHCP (0x93) già avviato.</span><span class="sxs-lookup"><span data-stu-id="df421-591">**NX_DHCP_ALREADY_STARTED** (0x93) DHCP already started.</span></span>

- <span data-ttu-id="df421-592">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-592">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="df421-593">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="df421-593">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-594">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-594">Allowed From</span></span>

<span data-ttu-id="df421-595">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-595">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-596">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-596">Example</span></span>

```C
/* Start the DHCP processing for this IP instance. */
status =  nx_dhcp_start(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully started. */
```

## <a name="nx_dhcp_interface_start"></a><span data-ttu-id="df421-597">nx_dhcp_interface_start</span><span class="sxs-lookup"><span data-stu-id="df421-597">nx_dhcp_interface_start</span></span>

<span data-ttu-id="df421-598">Avvia elaborazione DHCP sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="df421-598">Start DHCP processing on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-599">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-599">Prototype</span></span>

```C
UINT nx_dhcp_interface_start(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="df421-600">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-600">Description</span></span>

<span data-ttu-id="df421-601">Questo servizio avvia l'elaborazione DHCP sull'interfaccia specificata se tale interfaccia è abilitata per DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-601">This service starts DHCP processing on the specified interface if that interface is enabled for DHCP.</span></span> <span data-ttu-id="df421-602">Per ulteriori informazioni sull'abilitazione di un'interfaccia per DHCP, vedere *nx_dhcp_interface_enable*().</span><span class="sxs-lookup"><span data-stu-id="df421-602">See *nx_dhcp_interface_enable*() for more details about enabling an interface for DHCP.</span></span> <span data-ttu-id="df421-603">Per impostazione predefinita, l'interfaccia primaria è abilitata per DHCP quando l'applicazione chiama *nx_dhcp_create.*</span><span class="sxs-lookup"><span data-stu-id="df421-603">By default the primary interface is enabled for DHCP when the application calls *nx_dhcp_create.*</span></span>

<span data-ttu-id="df421-604">Se non sono presenti altre interfacce che eseguono il client DHCP, il servizio avvierà/riprenderà il thread del client DHCP e (ri) attiverà il timer del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-604">If there are no other interfaces running DHCP Client this service will start/resume the DHCP Client thread and (re)activate the DHCP Client timer.</span></span>  
  
<span data-ttu-id="df421-605">L'applicazione deve usare *nx_ip_status_check* per verificare se è stato ottenuto un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="df421-605">The application should use *nx_ip_status_check* to verify if an IP address is obtained.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-606">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-606">Input Parameters</span></span>

- <span data-ttu-id="df421-607">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-607">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="df421-608">**Interface_index** Indice in cui avviare il client DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-608">**Interface_index** Index on which to start the DHCP Client</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-609">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-609">Return Values</span></span>

- <span data-ttu-id="df421-610">Avvio DHCP **NX_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="df421-610">**NX_SUCCESS** (0x00) Successful DHCP start.</span></span>  

- <span data-ttu-id="df421-611">**NX_DHCP_ALREADY_STARTED** (0X93) l'istanza DHCP è già stata avviata.</span><span class="sxs-lookup"><span data-stu-id="df421-611">**NX_DHCP_ALREADY_STARTED** (0x93) The DHCP instance has already been started.</span></span>

- <span data-ttu-id="df421-612">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-612">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="df421-613">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="df421-613">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

- <span data-ttu-id="df421-614">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-614">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-615">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-615">Allowed From</span></span>

<span data-ttu-id="df421-616">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-616">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-617">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-617">Example</span></span>

```C
/* Start the DHCP processing for this IP instance on interface 1. */
status =  nx_dhcp_interface_start(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully started. */
```

## <a name="nx_dhcp_state_change_notify"></a><span data-ttu-id="df421-618">nx_dhcp_state_change_notify</span><span class="sxs-lookup"><span data-stu-id="df421-618">nx_dhcp_state_change_notify</span></span>

<span data-ttu-id="df421-619">Imposta funzione di callback modifica stato DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-619">Set DHCP state change callback function</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-620">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-620">Prototype</span></span>

```C
UINT nx_dhcp_state_change_notify(
          NX_DHCP *dhcp_ptr, 
          VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                           UCHAR new_state));
```

### <a name="description"></a><span data-ttu-id="df421-621">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-621">Description</span></span>

<span data-ttu-id="df421-622">Questo servizio registra la funzione di callback specificata dhcp_state_change_notify per notificare a un'applicazione le modifiche dello stato DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-622">This service registers the specified callback function dhcp_state_change_notify for notifying an application of DHCP state changes.</span></span> <span data-ttu-id="df421-623">La funzione di callback fornisce lo stato di transizione del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-623">The callback function supplies the state the DHCP Client has transitioned into.</span></span>

<span data-ttu-id="df421-624">Di seguito sono riportati i valori associati ai vari Stati DHCP:</span><span class="sxs-lookup"><span data-stu-id="df421-624">Following are values associated with the various DHCP states:</span></span>

| <span data-ttu-id="df421-625">State</span><span class="sxs-lookup"><span data-stu-id="df421-625">State</span></span>                             | <span data-ttu-id="df421-626">Valore</span><span class="sxs-lookup"><span data-stu-id="df421-626">Value</span></span> |
|-----------------------------------|-------|
| <span data-ttu-id="df421-627">\_ \_ avvio stato DHCP \_ NX</span><span class="sxs-lookup"><span data-stu-id="df421-627">NX\_DHCP\_STATE\_BOOT</span></span>             | <span data-ttu-id="df421-628">1</span><span class="sxs-lookup"><span data-stu-id="df421-628">1</span></span>     |
| <span data-ttu-id="df421-629">\_ \_ init stato DHCP \_ NX</span><span class="sxs-lookup"><span data-stu-id="df421-629">NX\_DHCP\_STATE\_INIT</span></span>             | <span data-ttu-id="df421-630">2</span><span class="sxs-lookup"><span data-stu-id="df421-630">2</span></span>     |
| <span data-ttu-id="df421-631">\_ \_ selezione stato DHCP \_ NX</span><span class="sxs-lookup"><span data-stu-id="df421-631">NX\_DHCP\_STATE\_SELECTING</span></span>        | <span data-ttu-id="df421-632">3</span><span class="sxs-lookup"><span data-stu-id="df421-632">3</span></span>     |
| <span data-ttu-id="df421-633">\_ \_ richiesta stato DHCP \_ NX</span><span class="sxs-lookup"><span data-stu-id="df421-633">NX\_DHCP\_STATE\_REQUESTING</span></span>       | <span data-ttu-id="df421-634">4</span><span class="sxs-lookup"><span data-stu-id="df421-634">4</span></span>     |
| <span data-ttu-id="df421-635">\_ \_ limite stato DHCP \_ NX</span><span class="sxs-lookup"><span data-stu-id="df421-635">NX\_DHCP\_STATE\_BOUND</span></span>            | <span data-ttu-id="df421-636">5</span><span class="sxs-lookup"><span data-stu-id="df421-636">5</span></span>     |
| <span data-ttu-id="df421-637">\_ \_ rinnovo stato DHCP \_ NX</span><span class="sxs-lookup"><span data-stu-id="df421-637">NX\_DHCP\_STATE\_RENEWING</span></span>         | <span data-ttu-id="df421-638">6</span><span class="sxs-lookup"><span data-stu-id="df421-638">6</span></span>     |
| <span data-ttu-id="df421-639">\_riassociazione \_ dello stato DHCP NX \_</span><span class="sxs-lookup"><span data-stu-id="df421-639">NX\_DHCP\_STATE\_REBINDING</span></span>        | <span data-ttu-id="df421-640">7</span><span class="sxs-lookup"><span data-stu-id="df421-640">7</span></span>     |
| <span data-ttu-id="df421-641">NX_DHCP_STATE_FORCERENEW</span><span class="sxs-lookup"><span data-stu-id="df421-641">NX_DHCP_STATE_FORCERENEW</span></span>          | <span data-ttu-id="df421-642">8</span><span class="sxs-lookup"><span data-stu-id="df421-642">8</span></span>     |
| <span data-ttu-id="df421-643">\_ \_ \_ probe degli indirizzi di stato DHCP NX \_</span><span class="sxs-lookup"><span data-stu-id="df421-643">NX\_DHCP\_STATE\_ADDRESS\_PROBING</span></span> | <span data-ttu-id="df421-644">9</span><span class="sxs-lookup"><span data-stu-id="df421-644">9</span></span>     |


### <a name="input-parameters"></a><span data-ttu-id="df421-645">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-645">Input Parameters</span></span>

- <span data-ttu-id="df421-646">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-646">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="df421-647">**dhcp_state_change_notify** Puntatore alla funzione di callback modifica stato</span><span class="sxs-lookup"><span data-stu-id="df421-647">**dhcp_state_change_notify** State change callback function pointer</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-648">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-648">Return Values</span></span>

- <span data-ttu-id="df421-649">**NX_SUCCESS** (0x00) set di callback riuscito.</span><span class="sxs-lookup"><span data-stu-id="df421-649">**NX_SUCCESS** (0x00) Successful callback set.</span></span>  

- <span data-ttu-id="df421-650">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-650">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="df421-651">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="df421-651">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-652">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-652">Allowed From</span></span>

<span data-ttu-id="df421-653">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="df421-653">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="df421-654">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-654">Example</span></span>

```C
/* Register the “my_state_change” function to be called on any DHCP state change, 
   assuming DHCP has alreadybeen created. */
status =  nx_dhcp_state_change_notify(&my_dhcp, my_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered. */
```

## <a name="nx_dhcp_interface_state_change_notify"></a><span data-ttu-id="df421-655">nx_dhcp_interface_state_change_notify</span><span class="sxs-lookup"><span data-stu-id="df421-655">nx_dhcp_interface_state_change_notify</span></span>

<span data-ttu-id="df421-656">Imposta la funzione di callback della modifica dello stato DHCP sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="df421-656">Set DHCP state change callback function on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-657">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-657">Prototype</span></span>

```C
UINT nx_dhcp_interface_state_change_notify(
              NX_DHCP *dhcp_ptr, 
              UINT interface_index,
              VOID (*dhcp_state_change_notify)(NX_DHCP *dhcp_ptr, 
                                               UINT interface_index,
                                               UCHAR new_state));
```

### <a name="description"></a><span data-ttu-id="df421-658">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-658">Description</span></span>

<span data-ttu-id="df421-659">Questo servizio registra la funzione di callback specificata per notificare a un'applicazione le modifiche dello stato DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-659">This service registers the specified callback function for notifying an application of DHCP state changes.</span></span> <span data-ttu-id="df421-660">Gli argomenti di input funciton di callback sono l'indice dell'interfaccia e lo stato di transizione del client DHCP a tale interfaccia.</span><span class="sxs-lookup"><span data-stu-id="df421-660">The callback funciton input arguments are the interface index and the state the DHCP Client has transitioned to on that interface.</span></span>

<span data-ttu-id="df421-661">Per ulteriori informazioni sulle funzioni di modifica dello stato, vedere *nx_dhcp_state_change_notify*().</span><span class="sxs-lookup"><span data-stu-id="df421-661">For more information about state change functions, see *nx_dhcp_state_change_notify*().</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-662">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-662">Input Parameters</span></span>

- <span data-ttu-id="df421-663">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-663">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="df421-664">**dhcp_interface_state_change_notify** Puntatore alla funzione di callback dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="df421-664">**dhcp_interface_state_change_notify** Application callback function pointer</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-665">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-665">Return Values</span></span>

- <span data-ttu-id="df421-666">**NX_SUCCESS** (0x00) set di callback riuscito.</span><span class="sxs-lookup"><span data-stu-id="df421-666">**NX_SUCCESS** (0x00) Successful callback set.</span></span>  

- <span data-ttu-id="df421-667">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-667">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-668">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-668">Allowed From</span></span>

<span data-ttu-id="df421-669">Thread, inizializzazione</span><span class="sxs-lookup"><span data-stu-id="df421-669">Threads, Initialization</span></span>

### <a name="example"></a><span data-ttu-id="df421-670">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-670">Example</span></span>

```C
/* Register the “my_state_change” function to be called on any DHCP state 
   change, assuming DHCP has alreadybeen created. */

void dhcp_interstate_state_change(NX_DHCP *dhcp_ptr, UINT iface_index, 
                                 UCHAR new_state);


status =  nx_dhcp_interstate_state_change_notify(&my_dhcp,  
                                                 dhcp_interstate_state_change);

/* If status is NX_SUCCESS the callback function was successfully
   registered. */
```

## <a name="nx_dhcp_stop"></a><span data-ttu-id="df421-671">nx_dhcp_stop</span><span class="sxs-lookup"><span data-stu-id="df421-671">nx_dhcp_stop</span></span>

<span data-ttu-id="df421-672">Arresta l'elaborazione DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-672">Stops DHCP processing</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-673">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-673">Prototype</span></span>

```C
UINT nx_dhcp_stop(NX_DHCP *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="df421-674">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-674">Description</span></span>

<span data-ttu-id="df421-675">Questo servizio interrompe l'elaborazione DHCP su tutte le interfacce che hanno avviato l'elaborazione DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-675">This service stops DHCP processing on all interfaces that have started DHCP processing.</span></span> <span data-ttu-id="df421-676">Se non sono presenti interfacce che elaborano DHCP, il servizio sospende il thread del client DHCP e disattiva il timer del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-676">If there are no interfaces processing DHCP, this service will suspend the DHCP Client thread, and inactivate the DHCP Client timer.</span></span>

<span data-ttu-id="df421-677">Per arrestare DHCP in un'interfaccia specifica se sono abilitate più interfacce per DHCP, usare il servizio *nx_dhcp_interface_stop* .</span><span class="sxs-lookup"><span data-stu-id="df421-677">To stop DHCP on a specific interface if multiple interfaces are enabled for DHCP, use the *nx_dhcp_interface_stop* service.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-678">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-678">Input Parameters</span></span>

- <span data-ttu-id="df421-679">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-679">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-680">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-680">Return Values</span></span>

- <span data-ttu-id="df421-681">Arresto DHCP **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="df421-681">**NX_SUCCESS** (0x00) Successful DHCP stop</span></span>

- <span data-ttu-id="df421-682">**NX_DHCP_NOT_STARTED** (0X96) l'istanza DHCP non è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="df421-682">**NX_DHCP_NOT_STARTED** (0x96) The DHCP instance not started.</span></span>

- <span data-ttu-id="df421-683">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-683">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="df421-684">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="df421-684">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-685">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-685">Allowed From</span></span>

<span data-ttu-id="df421-686">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-686">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-687">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-687">Example</span></span>

```C
/* Stop the DHCP processing for this IP instance. */
status =  nx_dhcp_stop(&my_dhcp);

/* If status is NX_SUCCESS the DHCP was successfully stopped. */
```

## <a name="nx_dhcp_interface_stop"></a><span data-ttu-id="df421-688">nx_dhcp_interface_stop</span><span class="sxs-lookup"><span data-stu-id="df421-688">nx_dhcp_interface_stop</span></span>

<span data-ttu-id="df421-689">Arresta l'elaborazione DHCP sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="df421-689">Stop DHCP processing on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-690">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-690">Prototype</span></span>

```C
UINT nx_dhcp_interface_stop(NX_DHCP *dhcp_ptr, UINT interface_index);
```

### <a name="description"></a><span data-ttu-id="df421-691">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-691">Description</span></span>

<span data-ttu-id="df421-692">Questo servizio interrompe l'elaborazione DHCP sull'interfaccia specificata se DHCP è già avviato.</span><span class="sxs-lookup"><span data-stu-id="df421-692">This service stops DHCP processing on the specified interface if DHCP is already started.</span></span> <span data-ttu-id="df421-693">Se non sono presenti altre interfacce che eseguono DHCP, il thread e il timer DHCP verranno sospesi.</span><span class="sxs-lookup"><span data-stu-id="df421-693">If there are no other interfaces running DHCP, the DHCP thread and timer are suspended.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-694">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-694">Input Parameters</span></span>

- <span data-ttu-id="df421-695">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-695">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="df421-696">**Interface_index** Interfaccia su cui arrestare l'elaborazione DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-696">**Interface_index** Interface on which to stop DHCP processing</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-697">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-697">Return Values</span></span>

- <span data-ttu-id="df421-698">Arresto DHCP **NX_SUCCESS** (0x00) riuscito</span><span class="sxs-lookup"><span data-stu-id="df421-698">**NX_SUCCESS** (0x00) Successful DHCP stop</span></span>

- <span data-ttu-id="df421-699">**NX_DHCP_NOT_STARTED** DHCP (0x96) non avviato.</span><span class="sxs-lookup"><span data-stu-id="df421-699">**NX_DHCP_NOT_STARTED** (0x96) DHCP not started.</span></span>

- <span data-ttu-id="df421-700">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-700">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="df421-701">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="df421-701">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

- <span data-ttu-id="df421-702">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-702">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-703">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-703">Allowed From</span></span>

<span data-ttu-id="df421-704">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-704">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-705">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-705">Example</span></span>

```C
/* Stop DHCP processing for this IP instance on interface 1. */
status =  nx_dhcp_interface_stop(&my_dhcp, 1);

/* If status is NX_SUCCESS the DHCP was successfully stopped. */
```

## <a name="nx_dhcp_user_option_retrieve"></a><span data-ttu-id="df421-706">nx_dhcp_user_option_retrieve</span><span class="sxs-lookup"><span data-stu-id="df421-706">nx_dhcp_user_option_retrieve</span></span>

<span data-ttu-id="df421-707">Recupera un'opzione DHCP dall'ultima risposta server</span><span class="sxs-lookup"><span data-stu-id="df421-707">Retrieve a DHCP option from last server response</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-708">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-708">Prototype</span></span>

```C
UINT nx_dhcp_user_option_retrieve(NX_DHCP *dhcp_ptr, 
            UINT request_option, UCHAR *destination_ptr, 
            UINT *destination_size);
```

### <a name="description"></a><span data-ttu-id="df421-709">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-709">Description</span></span>

<span data-ttu-id="df421-710">Questo servizio recupera l'opzione DHCP specificata dal buffer delle opzioni DHCP nella prima interfaccia abilitata per DHCP trovato nel record client DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-710">This service retrieves the specified DHCP option from the DHCP options buffer on the first interface enabled for DHCP found on the DHCP Client record.</span></span> <span data-ttu-id="df421-711">In caso di esito positivo, i dati dell'opzione vengono copiati nel buffer specificato.</span><span class="sxs-lookup"><span data-stu-id="df421-711">If successful, the option data is copied into the specified buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-712">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-712">Input Parameters</span></span>

- <span data-ttu-id="df421-713">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-713">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>  

- <span data-ttu-id="df421-714">**request_option** Opzione DHCP, come specificato dalle RFC.</span><span class="sxs-lookup"><span data-stu-id="df421-714">**request_option** DHCP option, as specified by the RFCs.</span></span> <span data-ttu-id="df421-715">Vedere l'opzione NX_DHCP_OPTION in *nx_dhcp. h*.</span><span class="sxs-lookup"><span data-stu-id="df421-715">See the NX_DHCP_OPTION option in *nx_dhcp.h*.</span></span>

- <span data-ttu-id="df421-716">**destination_ptr** Puntatore alla destinazione per la stringa di risposta.</span><span class="sxs-lookup"><span data-stu-id="df421-716">**destination_ptr** Pointer to the destination for the response string.</span></span>  

- <span data-ttu-id="df421-717">**destination_size** Puntatore alla dimensione della destinazione e all'oggetto restituito, la destinazione in cui inserire il numero di byte restituiti.</span><span class="sxs-lookup"><span data-stu-id="df421-717">**destination_size** Pointer to the size of the destination and on return, the destination to place the number of bytes returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-718">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-718">Return Values</span></span>

- <span data-ttu-id="df421-719">Il recupero delle opzioni riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="df421-719">**NX_SUCCESS** (0x00) Successful option retrieval.</span></span>  

- <span data-ttu-id="df421-720">Client DHCP **NX_DHCP_NOT_BOUND** (0x94) non associato.</span><span class="sxs-lookup"><span data-stu-id="df421-720">**NX_DHCP_NOT_BOUND** (0x94) DHCP Client not bound.</span></span>

- <span data-ttu-id="df421-721">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) non sono abilitate interfacce per DHCP</span><span class="sxs-lookup"><span data-stu-id="df421-721">**NX_DHCP_NO_INTERFACES_ENABLED** (0xA5) No interfaces enabled for DHCP</span></span>

- <span data-ttu-id="df421-722">La destinazione **NX_DHCP_DEST_TO_SMALL** (0x95) è troppo piccola per mantenere la risposta.</span><span class="sxs-lookup"><span data-stu-id="df421-722">**NX_DHCP_DEST_TO_SMALL** (0x95) Destination is too small to hold response.</span></span>

- <span data-ttu-id="df421-723">Impossibile trovare l'opzione DHCP **NX_DHCP_PARSE_ERROR** (0x97) nella risposta del server.</span><span class="sxs-lookup"><span data-stu-id="df421-723">**NX_DHCP_PARSE_ERROR** (0x97) DHCP Option not found in Server response.</span></span>

- <span data-ttu-id="df421-724">NX_PTR_ERROR (0x16) puntatore di input non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-724">NX_PTR_ERROR (0x16) Invalid input pointer.</span></span>

- <span data-ttu-id="df421-725">Il chiamante NX_CALLER_ERROR (0x11) non è valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="df421-725">NX_CALLER_ERROR (0x11) Invalid caller of this service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-726">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-726">Allowed From</span></span>

<span data-ttu-id="df421-727">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-727">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-728">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-728">Example</span></span>

```C
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server. */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_user_option_retrieve(&my_dhcp, NX_DHCP_OPTION_DNS_SVR,
        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string. */
```

## <a name="nx_dhcp_interface_user_option_retrieve"></a><span data-ttu-id="df421-729">nx_dhcp_interface_user_option_retrieve</span><span class="sxs-lookup"><span data-stu-id="df421-729">nx_dhcp_interface_user_option_retrieve</span></span>

<span data-ttu-id="df421-730">Recupera un'opzione DHCP dall'ultima risposta server sull'interfaccia specificata</span><span class="sxs-lookup"><span data-stu-id="df421-730">Retrieve a DHCP option from last server response on the specified interface</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-731">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-731">Prototype</span></span>

```C
UINT nx_dhcp_interface_user_option_retrieve(NX_DHCP *dhcp_ptr,
                  UINT interface_index, 
            UINT request_option, UCHAR *destination_ptr, 
            UINT *destination_size);
```

### <a name="description"></a><span data-ttu-id="df421-732">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-732">Description</span></span>

<span data-ttu-id="df421-733">Questo servizio recupera l'opzione DHCP specificata dal buffer delle opzioni DHCP nell'interfaccia specificata, se tale interfaccia è abilitata per DHCP.</span><span class="sxs-lookup"><span data-stu-id="df421-733">This service retrieves the specified DHCP option from the DHCP options buffer on the specified interface, if that interface is enabled for DHCP.</span></span> <span data-ttu-id="df421-734">In caso di esito positivo, i dati dell'opzione vengono copiati nel buffer specificato.</span><span class="sxs-lookup"><span data-stu-id="df421-734">If successful, the option data is copied into the specified buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-735">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-735">Input Parameters</span></span>

- <span data-ttu-id="df421-736">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-736">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="df421-737">**Interface_index** Indice in cui recuperare l'opzione specificata</span><span class="sxs-lookup"><span data-stu-id="df421-737">**Interface_index** Index on which to retrieve the specified option</span></span>  

- <span data-ttu-id="df421-738">**request_option** Opzione DHCP, come specificato dalle RFC.</span><span class="sxs-lookup"><span data-stu-id="df421-738">**request_option** DHCP option, as specified by the RFCs.</span></span> <span data-ttu-id="df421-739">Vedere l'opzione NX_DHCP_OPTION in *nx_dhcp. h*.</span><span class="sxs-lookup"><span data-stu-id="df421-739">See the NX_DHCP_OPTION option in *nx_dhcp.h*.</span></span>  

- <span data-ttu-id="df421-740">**destination_ptr** Puntatore alla destinazione per la stringa di risposta.</span><span class="sxs-lookup"><span data-stu-id="df421-740">**destination_ptr** Pointer to the destination for the response string.</span></span>  

- <span data-ttu-id="df421-741">**destination_size** Puntatore alla dimensione della destinazione e all'oggetto restituito, la destinazione in cui inserire il numero di byte restituiti.</span><span class="sxs-lookup"><span data-stu-id="df421-741">**destination_size** Pointer to the size of the destination and on return, the destination to place the number of bytes returned.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-742">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-742">Return Values</span></span>

- <span data-ttu-id="df421-743">Il recupero delle opzioni riuscite **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="df421-743">**NX_SUCCESS** (0x00) Successful option retrieval.</span></span>  

- <span data-ttu-id="df421-744">Indirizzo IP **NX_DHCP_NOT_BOUND** (0x94) non assegnato</span><span class="sxs-lookup"><span data-stu-id="df421-744">**NX_DHCP_NOT_BOUND** (0x94) IP address not assigned</span></span>

- <span data-ttu-id="df421-745">Il buffer di **NX_DHCP_DEST_TO_SMALL** (0x95) è troppo piccolo</span><span class="sxs-lookup"><span data-stu-id="df421-745">**NX_DHCP_DEST_TO_SMALL** (0x95) Buffer is too small</span></span>

- <span data-ttu-id="df421-746">Impossibile trovare l'opzione DHCP **NX_DHCP_PARSE_ERROR** (0x97) nella risposta del server.</span><span class="sxs-lookup"><span data-stu-id="df421-746">**NX_DHCP_PARSE_ERROR** (0x97) DHCP Option not found in Server response.</span></span>

- <span data-ttu-id="df421-747">NX_PTR_ERROR (0x16) puntatore DHCP non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-747">NX_PTR_ERROR (0x16) Invalid DHCP pointer.</span></span>

- <span data-ttu-id="df421-748">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="df421-748">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

- <span data-ttu-id="df421-749">L'interfaccia di rete NX_INVALID_INTERFACE (0x4C) non è valida</span><span class="sxs-lookup"><span data-stu-id="df421-749">NX_INVALID_INTERFACE (0x4C) Invalid network interface</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-750">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-750">Allowed From</span></span>

<span data-ttu-id="df421-751">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-751">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-752">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-752">Example</span></span>

```C
UCHAR  dns_ip_string[4];
ULONG  size;

/* Obtain the IP address of the DNS server on the prmary interface. */
size =    sizeof(dnx_ip_string);
status =  nx_dhcp_interface_user_option_retrieve(&my_dhcp, 0, NX_DHCP_OPTION_DNS_SVR,
        dns_ip_string, &size);

/* If status is NX_SUCCESS the DNS IP address is in dns_ip_string. */
```

## <a name="nx_dhcp_user_option_convert"></a><span data-ttu-id="df421-753">nx_dhcp_user_option_convert</span><span class="sxs-lookup"><span data-stu-id="df421-753">nx_dhcp_user_option_convert</span></span>

<span data-ttu-id="df421-754">Converte quattro byte in ULONG</span><span class="sxs-lookup"><span data-stu-id="df421-754">Convert four bytes to ULONG</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-755">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-755">Prototype</span></span>

```C
ULONG nx_dhcp_user_option_convert(UCHAR *option_string_ptr);
```

### <a name="description"></a><span data-ttu-id="df421-756">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-756">Description</span></span>

<span data-ttu-id="df421-757">Questo servizio converte i quattro caratteri a cui punta "option_string_ptr" in un valore long senza segno.</span><span class="sxs-lookup"><span data-stu-id="df421-757">This service converts the four characters pointed to by “option_string_ptr” into an unsigned long value.</span></span> <span data-ttu-id="df421-758">È particolarmente utile quando sono presenti indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="df421-758">It is especially useful when IP addresses are present.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-759">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-759">Input Parameters</span></span>

- <span data-ttu-id="df421-760">**option_string_ptr** Puntatore alla stringa di opzione recuperata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-760">**option_string_ptr** Pointer to previously retrieved option string.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-761">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-761">Return Values</span></span>

- <span data-ttu-id="df421-762">**Valore** di Valore dei primi quattro byte.</span><span class="sxs-lookup"><span data-stu-id="df421-762">**Value** Value of first four bytes.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-763">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-763">Allowed From</span></span>

<span data-ttu-id="df421-764">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-764">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-765">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-765">Example</span></span>

```C
UCHAR  dns_ip_string[4];
ULONG  dns_ip;

/* Convert the first four bytes of “dns_ip_string” to an actual IP
address in “dns_ip.”  */
dns_ip=  nx_dhcp_user_option_convert(dns_ip_string);

/* If status is NX_SUCCESS the DNS IP address is in “dns_ip.”  */
```

## <a name="nx_dhcp_user_option_add_callback_set"></a><span data-ttu-id="df421-766">nx_dhcp_user_option_add_callback_set</span><span class="sxs-lookup"><span data-stu-id="df421-766">nx_dhcp_user_option_add_callback_set</span></span>

<span data-ttu-id="df421-767">Imposta la funzione di callback per l'aggiunta di opzioni fornite dall'utente</span><span class="sxs-lookup"><span data-stu-id="df421-767">Set callback function for adding user supplied options</span></span>

### <a name="prototype"></a><span data-ttu-id="df421-768">Prototipo</span><span class="sxs-lookup"><span data-stu-id="df421-768">Prototype</span></span>

```C
ULONG nx_dhcp_user_option_add_callbcak_set(NX_DHCP *dhcp_ptr, 
    UINT (*dhcp_user_option_add)(NX_DHCP *dhcp_ptr, 
                                 UINT iface_index, 
                                 UINT message_type, 
                                 UCHAR *user_option_ptr, 
                                 UINT *user_option_length));
```

### <a name="description"></a><span data-ttu-id="df421-769">Descrizione</span><span class="sxs-lookup"><span data-stu-id="df421-769">Description</span></span>

<span data-ttu-id="df421-770">Questo servizio registra la funzione di callback specificata per aggiungere opzioni fornite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="df421-770">This service registers the specified callback function for adding user supplied options.</span></span>

<span data-ttu-id="df421-771">Se la funzione di callback specificata, le applicazioni possono aggiungere opzioni fornite dall'utente nel pacchetto per iface_index e message_type.</span><span class="sxs-lookup"><span data-stu-id="df421-771">If the callback function specified, the applications can add user supplied options into the packet by iface_index and message_type.</span></span>

> [!NOTE]
> <span data-ttu-id="df421-772">Nella routine dell'utente.</span><span class="sxs-lookup"><span data-stu-id="df421-772">In user’s routine.</span></span> <span data-ttu-id="df421-773">Le applicazioni devono seguire il formato delle opzioni DHCP quando si aggiungono le opzioni fornite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="df421-773">Applications must follow the DHCP options format when add user supplied options.</span></span> <span data-ttu-id="df421-774">La dimensione totale delle opzioni utente deve essere minore o uguale a user_option_length e aggiornare la user_option_length come lunghezza delle opzioni reali.</span><span class="sxs-lookup"><span data-stu-id="df421-774">The total size of user options must be less or equal to user_option_length, and update the user_option_length as real options length.</span></span> <span data-ttu-id="df421-775">Restituisce NX_TRUE se le opzioni di aggiunta sono state completate, in caso contrario restituire NX_FALSE.</span><span class="sxs-lookup"><span data-stu-id="df421-775">Return NX_TRUE if add options successfully, else return NX_FALSE.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="df421-776">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="df421-776">Input Parameters</span></span>

- <span data-ttu-id="df421-777">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df421-777">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

- <span data-ttu-id="df421-778">**dhcp_user_option_add** Puntatore alla funzione di aggiunta dell'opzione User.</span><span class="sxs-lookup"><span data-stu-id="df421-778">**dhcp_user_option_add** Pointer to user option add function.</span></span>

### <a name="return-values"></a><span data-ttu-id="df421-779">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="df421-779">Return Values</span></span>

- <span data-ttu-id="df421-780">**NX_SUCCESS** (0x00) set di callback riuscito.</span><span class="sxs-lookup"><span data-stu-id="df421-780">**NX_SUCCESS** (0x00) Successful callback set.</span></span>

- <span data-ttu-id="df421-781">NX_PTR_ERROR (0x16) puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="df421-781">NX_PTR_ERROR (0x16) Invalid pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="df421-782">Consentito da</span><span class="sxs-lookup"><span data-stu-id="df421-782">Allowed From</span></span>

<span data-ttu-id="df421-783">Thread</span><span class="sxs-lookup"><span data-stu-id="df421-783">Threads</span></span>

### <a name="example"></a><span data-ttu-id="df421-784">Esempio</span><span class="sxs-lookup"><span data-stu-id="df421-784">Example</span></span>

```C
/* Register the “my_dhcp_user_option_add” function to be called when add DHCP
options, assuming DHCP has already been created. */

status =  nx_dhcp_user_option_add_callback_set(&my_dhcp, my_dhcp_user_option_add);

/* If status is NX_SUCCESS the callback function was successfully registered. */
```
