---
title: Capitolo 3-Descrizione dei servizi server DHCP NetX di Azure RTO
description: Questo capitolo contiene una descrizione di tutti i servizi server DHCP NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: d24c69cf6b8c2bb84b7155e49a54e8296ee662f0
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822688"
---
# <a name="chapter-3---description-of-azure-rtos-netx-dhcp-server-services"></a><span data-ttu-id="73076-103">Capitolo 3-Descrizione dei servizi server DHCP NetX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="73076-103">Chapter 3 - Description of Azure RTOS NetX DHCP Server services</span></span>

<span data-ttu-id="73076-104">Questo capitolo contiene una descrizione di tutti i servizi server DHCP di NetX.</span><span class="sxs-lookup"><span data-stu-id="73076-104">This chapter contains a description of all NetX DHCP Server services.</span></span>

<span data-ttu-id="73076-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="73076-105">In the "Return Values" section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="73076-106">**nx_dhcp_server_create**: *creare un'istanza del server DHCP*</span><span class="sxs-lookup"><span data-stu-id="73076-106">**nx_dhcp_server_create**: *Create a DHCP Server instance*</span></span>
- <span data-ttu-id="73076-107">**nx_dhcp_set_interface_network_parameters**: *impostare le opzioni del server DHCP per i parametri di rete critici per l'interfaccia specificata*</span><span class="sxs-lookup"><span data-stu-id="73076-107">**nx_dhcp_set_interface_network_parameters**: *Set DHCP Server options for critical network parameters for specified interface*</span></span>
- <span data-ttu-id="73076-108">**nx_dhcp_create_server_ip_address_list**: *creare un pool di indirizzi IP disponibili da assegnare all'interfaccia dei client DHCP*</span><span class="sxs-lookup"><span data-stu-id="73076-108">**nx_dhcp_create_server_ip_address_list**: *Create pool of available IP addresses to assign to DHCP Clients interface*</span></span>
- <span data-ttu-id="73076-109">**nx_dhcp_clear_client_record**: *rimuovere il record client nel database del server*</span><span class="sxs-lookup"><span data-stu-id="73076-109">**nx_dhcp_clear_client_record**: *Remove Client record in the Server database*</span></span>
- <span data-ttu-id="73076-110">**nx_dhcp_server_delete**: *eliminare un'istanza di dhcpserver*</span><span class="sxs-lookup"><span data-stu-id="73076-110">**nx_dhcp_server_delete**: *Delete a DHCPServer instance*</span></span>
- <span data-ttu-id="73076-111">**nx_dhcp_server_start**: *avviare o riprendere l'elaborazione del server DHCP*</span><span class="sxs-lookup"><span data-stu-id="73076-111">**nx_dhcp_server_start**: *Start or resume DHCP Server processing*</span></span>
- <span data-ttu-id="73076-112">**nx_dhcp_server_stop**: *arrestare l'elaborazione del server DHCP*</span><span class="sxs-lookup"><span data-stu-id="73076-112">**nx_dhcp_server_stop**: *Stop DHCP server processing*</span></span>

## <a name="nx_dhcp_server_create"></a><span data-ttu-id="73076-113">nx_dhcp_server_create</span><span class="sxs-lookup"><span data-stu-id="73076-113">nx_dhcp_server_create</span></span>

<span data-ttu-id="73076-114">Creare un'istanza del server DHCP</span><span class="sxs-lookup"><span data-stu-id="73076-114">Create a DHCP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="73076-115">Prototipo</span><span class="sxs-lookup"><span data-stu-id="73076-115">Prototype</span></span>

```c
UINT nx_dhcp_server_create(NX_DHCP_SERVER *dhcp_ptr, NX_IP *ip_ptr,
                        VOID *stack_ptr, ULONG stack_size,
                        CHAR *input_address_list, CHAR *name_ptr,
                        NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a><span data-ttu-id="73076-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73076-116">Description</span></span>

<span data-ttu-id="73076-117">Questo servizio crea un'istanza del server DHCP con un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="73076-117">This service creates a DHCP Server instance with a previously created IP instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73076-118">L'applicazione deve verificare che il pool di pacchetti creato per il servizio di creazione IP disponga di un payload di byte minimum548, escluso le intestazioni UDP, IP e Ethernet.</span><span class="sxs-lookup"><span data-stu-id="73076-118">The application must make sure the packet pool created for the IP create service has a minimum548 byte payload, not including the UDP, IP and Ethernet headers.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="73076-119">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="73076-119">Input Parameters</span></span>

- <span data-ttu-id="73076-120">**dhcp_ptr**: puntatore al blocco di controllo server DHCP.</span><span class="sxs-lookup"><span data-stu-id="73076-120">**dhcp_ptr**: Pointer to DHCP Server control block.</span></span>  
- <span data-ttu-id="73076-121">**ip_ptr**: puntatore all'istanza IP del server DHCP.</span><span class="sxs-lookup"><span data-stu-id="73076-121">**ip_ptr**: Pointer to DHCP Server IP instance.</span></span>
- <span data-ttu-id="73076-122">**stack_ptr**: posizione dello stack del server DHCP del puntatore.</span><span class="sxs-lookup"><span data-stu-id="73076-122">**stack_ptr**: Pointer DHCP Server stack location.</span></span>
- <span data-ttu-id="73076-123">**stack_size**: dimensioni dello stack di server DHCP</span><span class="sxs-lookup"><span data-stu-id="73076-123">**stack_size**: Size of DHCP Server stack</span></span>
- <span data-ttu-id="73076-124">**input_address_list**: puntatore all'elenco di indirizzi IP del server</span><span class="sxs-lookup"><span data-stu-id="73076-124">**input_address_list**: Pointer to Server's list of IP addresses</span></span>
- <span data-ttu-id="73076-125">**name_ptr**: puntatore al nome del server DHCP</span><span class="sxs-lookup"><span data-stu-id="73076-125">**name_ptr**: Pointer to DHCP Server name</span></span>
- <span data-ttu-id="73076-126">**packet_pool_ptr**: puntatore al pool di pacchetti del server DHCP</span><span class="sxs-lookup"><span data-stu-id="73076-126">**packet_pool_ptr**: Pointer to DHCP Server packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="73076-127">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="73076-127">Return Values</span></span>

- <span data-ttu-id="73076-128">**NX_SUCCESS**: (0x00) la creazione del server DHCP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="73076-128">**NX_SUCCESS**: (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="73076-129">**NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD**: (0xA9) payload del pacchetto troppo piccolo errore</span><span class="sxs-lookup"><span data-stu-id="73076-129">**NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD**: (0xA9) Packet payload too small error</span></span>
- <span data-ttu-id="73076-130">**NX_DHCP_NO_SERVER_OPTION_LIST**: l'elenco di opzioni del server (0x96) è vuoto</span><span class="sxs-lookup"><span data-stu-id="73076-130">**NX_DHCP_NO_SERVER_OPTION_LIST**: (0x96) Server option list is empty</span></span>
- <span data-ttu-id="73076-131">NX_DHCP_PARAMETER_ERROR: (0x92) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="73076-131">NX_DHCP_PARAMETER_ERROR: (0x92) Invalid non pointer input</span></span>
- <span data-ttu-id="73076-132">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="73076-132">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="73076-133">NX_PTR_ERROR: (0x16) input puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="73076-133">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="73076-134">Consentito da</span><span class="sxs-lookup"><span data-stu-id="73076-134">Allowed From</span></span>

<span data-ttu-id="73076-135">Applicazione</span><span class="sxs-lookup"><span data-stu-id="73076-135">Application</span></span>

### <a name="example"></a><span data-ttu-id="73076-136">Esempio</span><span class="sxs-lookup"><span data-stu-id="73076-136">Example</span></span>

```c
/* Create a DHCP Server instance. */
status = nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
                    DEMO_SERVER_STACK_SIZE, SERVER_IP_ADDRESS_LIST,
                    "DHCP server", &server_pool);

/* If status is NX_SUCCESS a DHCP Server instance was successfully created. */
```

## <a name="nx_dhcp_create_server_ip_address_list"></a><span data-ttu-id="73076-137">nx_dhcp_create_server_ip_address_list</span><span class="sxs-lookup"><span data-stu-id="73076-137">nx_dhcp_create_server_ip_address_list</span></span>

<span data-ttu-id="73076-138">Creare un pool di indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="73076-138">Create a IP address pool</span></span>

### <a name="prototype"></a><span data-ttu-id="73076-139">Prototipo</span><span class="sxs-lookup"><span data-stu-id="73076-139">Prototype</span></span>

```c
UINT nx_dhcp_create_server_ip_address_list(NX_DHCP_SERVER *dhcp_ptr,
                            UINT iface_index, ULONG start_ip_address,
                            ULONG end_ip_address, UINT *addresses_added);
```

### <a name="description"></a><span data-ttu-id="73076-140">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73076-140">Description</span></span>

<span data-ttu-id="73076-141">Questo servizio crea un pool specifico di interfaccia di indirizzi IP disponibili per il server DHCP specificato da assegnare.</span><span class="sxs-lookup"><span data-stu-id="73076-141">This service creates a networkinterface specific pool of available IP addresses for the specified DHCP server to assign.</span></span> <span data-ttu-id="73076-142">Gli indirizzi IP di inizio e di fine devono corrispondere all'interfaccia di rete specificata.</span><span class="sxs-lookup"><span data-stu-id="73076-142">The start and end IP addresses must match the specified network interface.</span></span> <span data-ttu-id="73076-143">Il numero effettivo di indirizzi IP aggiunti può essere inferiore al totale degli indirizzi se l'elenco di indirizzi IP non è sufficientemente grande (impostazione configurabile dall'utente *NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* parametro).</span><span class="sxs-lookup"><span data-stu-id="73076-143">The actual number of IP addresses added may be less than the total addresses if the IP address list is not large enough (which is set in the user configurable *NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* parameter).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="73076-144">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="73076-144">Input Parameters</span></span>

- <span data-ttu-id="73076-145">**dhcp_ptr** Puntatore al blocco di controllo server DHCP.</span><span class="sxs-lookup"><span data-stu-id="73076-145">**dhcp_ptr** Pointer to DHCP Server control block.</span></span>  
- <span data-ttu-id="73076-146">**iface_index**: indice corrispondente all'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="73076-146">**iface_index**: Index corresponding to network interface</span></span>
- <span data-ttu-id="73076-147">**start_ip_address**: primo indirizzo IP disponibile</span><span class="sxs-lookup"><span data-stu-id="73076-147">**start_ip_address**: First available IP address</span></span>
- <span data-ttu-id="73076-148">**end_ip_address**: ultimo indirizzo IP disponibile</span><span class="sxs-lookup"><span data-stu-id="73076-148">**end_ip_address**: Last of the available IP address</span></span>
- <span data-ttu-id="73076-149">**addresses_added**: numero di indirizzi IP aggiunti all'elenco</span><span class="sxs-lookup"><span data-stu-id="73076-149">**addresses_added**: Number of IP addresses added to list</span></span>

### <a name="return-values"></a><span data-ttu-id="73076-150">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="73076-150">Return Values</span></span>

- <span data-ttu-id="73076-151">**NX_SUCCESS**: (0x00) la creazione del server DHCP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="73076-151">**NX_SUCCESS**: (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="73076-152">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: l'indice (0xA1) non corrisponde agli indirizzi</span><span class="sxs-lookup"><span data-stu-id="73076-152">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: (0xA1) Index does not match addresses</span></span>
- <span data-ttu-id="73076-153">**NX_DHCP_INVALID_IP_ADDRESS_LIST**: (0x99) input dell'indirizzo non valido</span><span class="sxs-lookup"><span data-stu-id="73076-153">**NX_DHCP_INVALID_IP_ADDRESS_LIST**: (0x99) Invalid address input</span></span>
- <span data-ttu-id="73076-154">NX_DHCP_INVALID_IP_ADDRESS: (0x9B) indirizzi di inizio/fine illogici</span><span class="sxs-lookup"><span data-stu-id="73076-154">NX_DHCP_INVALID_IP_ADDRESS: (0x9B) Illogical start/end addresses</span></span>
- <span data-ttu-id="73076-155">NX_PTR_ERROR: (0x16) input puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="73076-155">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="73076-156">Consentito da</span><span class="sxs-lookup"><span data-stu-id="73076-156">Allowed From</span></span>

<span data-ttu-id="73076-157">Applicazione</span><span class="sxs-lookup"><span data-stu-id="73076-157">Application</span></span>

### <a name="example"></a><span data-ttu-id="73076-158">Esempio</span><span class="sxs-lookup"><span data-stu-id="73076-158">Example</span></span>

```c
/* Create a pool of available IP addresses to assign. */
status = nx_dhcp_create_server_ip_list (&dhcp_server, iface_index,
                START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);

/* If status is NX_SUCCESS aIP address list was successfully created. 
addresses_added indicates how many IP addresses were actually added to the list. */
```

## <a name="nx_dhcp_clear_client_record"></a><span data-ttu-id="73076-159">nx_dhcp_clear_client_record</span><span class="sxs-lookup"><span data-stu-id="73076-159">nx_dhcp_clear_client_record</span></span>

<span data-ttu-id="73076-160">Rimuovi record client dal database del server</span><span class="sxs-lookup"><span data-stu-id="73076-160">Remove Client record from Server database</span></span>

### <a name="prototype"></a><span data-ttu-id="73076-161">Prototipo</span><span class="sxs-lookup"><span data-stu-id="73076-161">Prototype</span></span>

```c
UINT nx_dhcp_clear_client_record (NX_DHCP_SERVER *dhcp_ptr,
                                NX_DHCP_CLIENT *dhcp_client_ptr);
```

### <a name="description"></a><span data-ttu-id="73076-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73076-162">Description</span></span>

<span data-ttu-id="73076-163">Questo servizio Cancella il record client dal database del server.</span><span class="sxs-lookup"><span data-stu-id="73076-163">This service clears the Client record from the Server database.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="73076-164">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="73076-164">Input Parameters</span></span>

- <span data-ttu-id="73076-165">**dhcp_ptr**: puntatore al blocco di controllo server DHCP.</span><span class="sxs-lookup"><span data-stu-id="73076-165">**dhcp_ptr**: Pointer to DHCP Server control block.</span></span>  
- <span data-ttu-id="73076-166">**dhcp_client_ptr**: puntatore al client DHCP da rimuovere</span><span class="sxs-lookup"><span data-stu-id="73076-166">**dhcp_client_ptr**: Pointer to DHCP Client to remove</span></span>

### <a name="return-values"></a><span data-ttu-id="73076-167">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="73076-167">Return Values</span></span>

- <span data-ttu-id="73076-168">**NX_SUCCESS**: (0x00) la creazione del server DHCP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="73076-168">**NX_SUCCESS**: (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="73076-169">NX_PTR_ERROR: (0x16) input puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="73076-169">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="73076-170">NX_CALLER_ERROR: (0x11) chiamante non thread del servizio</span><span class="sxs-lookup"><span data-stu-id="73076-170">NX_CALLER_ERROR: (0x11) Non thread caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="73076-171">Consentito da</span><span class="sxs-lookup"><span data-stu-id="73076-171">Allowed From</span></span>

<span data-ttu-id="73076-172">Applicazione</span><span class="sxs-lookup"><span data-stu-id="73076-172">Application</span></span>

### <a name="example"></a><span data-ttu-id="73076-173">Esempio</span><span class="sxs-lookup"><span data-stu-id="73076-173">Example</span></span>

```c
/* Remove Client record from the server database. */
status = nx_dhcp_clear_client_record (&dhcp_server, &dhcp_client_ptr);

/* If status is NX_SUCCESS the specified Client was removed from the database. */
```

## <a name="nx_dhcp_set_interface_network_parameters"></a><span data-ttu-id="73076-174">nx_dhcp_set_interface_network_parameters</span><span class="sxs-lookup"><span data-stu-id="73076-174">nx_dhcp_set_interface_network_parameters</span></span>

<span data-ttu-id="73076-175">Impostare i parametri di rete per le opzioni DHCP</span><span class="sxs-lookup"><span data-stu-id="73076-175">Set network parameters for DHCP options</span></span>

### <a name="prototype"></a><span data-ttu-id="73076-176">Prototipo</span><span class="sxs-lookup"><span data-stu-id="73076-176">Prototype</span></span>

```c
UINT nx_dhcp_set_interface_network_parameters(NX_DHCP_SERVER *dhcp_ptr,
                                    UINT iface_index, ULONG subnet_mask,
                                    ULONG default_gateway_address,
                                    ULONG dns_server_address);
```

### <a name="description"></a><span data-ttu-id="73076-177">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73076-177">Description</span></span>

<span data-ttu-id="73076-178">Questo servizio imposta i valori predefiniti per i parametri critici della rete per l'interfaccia specificata.</span><span class="sxs-lookup"><span data-stu-id="73076-178">This service sets default values for network critical parameters for the specified interface.</span></span> <span data-ttu-id="73076-179">Il server DHCP includerà queste opzioni nell'offerta e le risposte ACK al client DHCP.</span><span class="sxs-lookup"><span data-stu-id="73076-179">The DHCP server will include these options in its OFFER and ACK replies to the DHCP Client.</span></span> <span data-ttu-id="73076-180">Se i parametri dell'interfaccia del set di host in cui è in esecuzione un server DHCP, i parametri vengono impostati come predefiniti come indicato di seguito: il router impostato sul gateway di interfaccia principale per il server DHCP stesso, l'indirizzo del server DNS per il server DHCP stesso e il subnet mask allo stesso modo in cui è configurata l'interfaccia server DHCP.</span><span class="sxs-lookup"><span data-stu-id="73076-180">If the host set interface parameters on which a DHCP server is running, the parameters will defaulted as follows: the router set to the primary interface gateway for the DHCP server itself, the DNS server address to the DHCP server itself, and the subnet mask to the same as the DHCP server interface is configured with.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="73076-181">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="73076-181">Input Parameters</span></span>

- <span data-ttu-id="73076-182">**dhcp_ptr**: puntatore al blocco di controllo server DHCP.</span><span class="sxs-lookup"><span data-stu-id="73076-182">**dhcp_ptr**: Pointer to DHCP Server control block.</span></span>  
- <span data-ttu-id="73076-183">**iface_index**: indice corrispondente all'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="73076-183">**iface_index**: Index corresponding to network interface</span></span>
- <span data-ttu-id="73076-184">**subnet_mask**: subnet mask per la rete client</span><span class="sxs-lookup"><span data-stu-id="73076-184">**subnet_mask**: Subnet mask for Client network</span></span>
- <span data-ttu-id="73076-185">**default_gateway_address**: indirizzo IP del router del client</span><span class="sxs-lookup"><span data-stu-id="73076-185">**default_gateway_address**: Client's router IP address</span></span>
- <span data-ttu-id="73076-186">**dns_server_address**: server DNS per la rete del client</span><span class="sxs-lookup"><span data-stu-id="73076-186">**dns_server_address**: DNS server for Client's network</span></span>

### <a name="return-values"></a><span data-ttu-id="73076-187">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="73076-187">Return Values</span></span>

- <span data-ttu-id="73076-188">**NX_SUCCESS**: (0x00) la creazione del server DHCP è riuscita.</span><span class="sxs-lookup"><span data-stu-id="73076-188">**NX_SUCCESS**: (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="73076-189">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: l'indice (0xA1) non corrisponde agli indirizzi</span><span class="sxs-lookup"><span data-stu-id="73076-189">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX**: (0xA1) Index does not match addresses</span></span>
- <span data-ttu-id="73076-190">**NX_DHCP_INVALID_NETWORK_PARAMETERS**: (0xA3) parametri di rete non validi</span><span class="sxs-lookup"><span data-stu-id="73076-190">**NX_DHCP_INVALID_NETWORK_PARAMETERS**: (0xA3) Invalid network parameters</span></span>
- <span data-ttu-id="73076-191">NX_PTR_ERROR: (0x16) input puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="73076-191">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="73076-192">Consentito da</span><span class="sxs-lookup"><span data-stu-id="73076-192">Allowed From</span></span>

<span data-ttu-id="73076-193">Applicazione</span><span class="sxs-lookup"><span data-stu-id="73076-193">Application</span></span>

### <a name="example"></a><span data-ttu-id="73076-194">Esempio</span><span class="sxs-lookup"><span data-stu-id="73076-194">Example</span></span>

```c
/* Set network parameters for a specific interface. */
status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
                                    NX_DHCP_SUBNET_MASK, IP_ADDRESS(10,0,0,1),
                                    IP_ADDRESS(10,0,0,1));

/* If status is NX_SUCCESS network parameters were successfully set. */
```

## <a name="nx_dhcp_server_delete"></a><span data-ttu-id="73076-195">nx_dhcp_server_delete</span><span class="sxs-lookup"><span data-stu-id="73076-195">nx_dhcp_server_delete</span></span>

<span data-ttu-id="73076-196">Eliminare un'istanza del server DHCP</span><span class="sxs-lookup"><span data-stu-id="73076-196">Delete a DHCP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="73076-197">Prototipo</span><span class="sxs-lookup"><span data-stu-id="73076-197">Prototype</span></span>

```c
UINT nx_dhcp_server_delete(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="73076-198">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73076-198">Description</span></span>

<span data-ttu-id="73076-199">Questo servizio Elimina un'istanza del server DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="73076-199">This service deletes a previously created DHCP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="73076-200">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="73076-200">Input Parameters</span></span>

- <span data-ttu-id="73076-201">**dhcp_ptr**: puntatore a un'istanza del server DHCP.</span><span class="sxs-lookup"><span data-stu-id="73076-201">**dhcp_ptr**: Pointer to a DHCP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="73076-202">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="73076-202">Return Values</span></span>

- <span data-ttu-id="73076-203">**NX_SUCCESS**: (0x00) eliminazione del server DHCP riuscita.</span><span class="sxs-lookup"><span data-stu-id="73076-203">**NX_SUCCESS**: (0x00) Successful DHCP Server delete.</span></span>
- <span data-ttu-id="73076-204">NX_PTR_ERROR: (0x16) input puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="73076-204">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="73076-205">NX_DHCP_PARAMETER_ERROR: (0x92) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="73076-205">NX_DHCP_PARAMETER_ERROR: (0x92) Invalid non pointer input</span></span>
- <span data-ttu-id="73076-206">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="73076-206">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="73076-207">Consentito da</span><span class="sxs-lookup"><span data-stu-id="73076-207">Allowed From</span></span>

<span data-ttu-id="73076-208">Thread</span><span class="sxs-lookup"><span data-stu-id="73076-208">Threads</span></span>

### <a name="example"></a><span data-ttu-id="73076-209">Esempio</span><span class="sxs-lookup"><span data-stu-id="73076-209">Example</span></span>

```c
/* Delete a DHCP Server instance. */
status = nx_dhcp_server_delete(&dhcp_server);  
  
/* If status is NX_SUCCESS the DHCP Server instance was successfully deleted. */
```

## <a name="nx_dhcp_server_start"></a><span data-ttu-id="73076-210">nx_dhcp_server_start</span><span class="sxs-lookup"><span data-stu-id="73076-210">nx_dhcp_server_start</span></span>

<span data-ttu-id="73076-211">Avviare l'elaborazione del server DHCP</span><span class="sxs-lookup"><span data-stu-id="73076-211">Start DHCP Server processing</span></span>

### <a name="prototype"></a><span data-ttu-id="73076-212">Prototipo</span><span class="sxs-lookup"><span data-stu-id="73076-212">Prototype</span></span>

```c
UINT nx_dhcp_server_start(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="73076-213">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73076-213">Description</span></span>

<span data-ttu-id="73076-214">Questo servizio avvia l'elaborazione del server DHCP, che include la creazione di un socket UDP del server, l'associazione della porta DHCP e l'attesa per la ricezione delle richieste DHCP del client.</span><span class="sxs-lookup"><span data-stu-id="73076-214">This service starts DHCP Server processing, which includes creating a server UDP socket, binding the DHCP port and waiting to receive Client DHCP requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="73076-215">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="73076-215">Input Parameters</span></span>

- <span data-ttu-id="73076-216">**dhcp_ptr**: puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="73076-216">**dhcp_ptr**: Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="73076-217">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="73076-217">Return Values</span></span>

- <span data-ttu-id="73076-218">**NX_SUCCESS**: (0x00) l'avvio del server è riuscito.</span><span class="sxs-lookup"><span data-stu-id="73076-218">**NX_SUCCESS**: (0x00) Successful Server start.</span></span>  
- <span data-ttu-id="73076-219">**NX_DHCP_ALREADY_STARTED**: (0X93) DHCP è già avviato.</span><span class="sxs-lookup"><span data-stu-id="73076-219">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP already started.</span></span>
- <span data-ttu-id="73076-220">NX_PTR_ERROR: (0x16) input puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="73076-220">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="73076-221">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="73076-221">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="73076-222">NX_DHCP_PARAMETER_ERROR: (0x92) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="73076-222">NX_DHCP_PARAMETER_ERROR: (0x92) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="73076-223">Consentito da</span><span class="sxs-lookup"><span data-stu-id="73076-223">Allowed From</span></span>

<span data-ttu-id="73076-224">Thread</span><span class="sxs-lookup"><span data-stu-id="73076-224">Threads</span></span>

### <a name="example"></a><span data-ttu-id="73076-225">Esempio</span><span class="sxs-lookup"><span data-stu-id="73076-225">Example</span></span>

```c
/* Start the DHCP Server processing for this IP instance. */
status = nx_dhcp_server_start(&dhcp_server);  

/* If status is NX_SUCCESS the DHCP Server was successfully started. */
```

### <a name="see-also"></a><span data-ttu-id="73076-226">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="73076-226">See Also</span></span>

<span data-ttu-id="73076-227">nx_dhcp_create, nx_dhcp_delete, nx_dhcp_release, nx_dhcp_state_change_notify, nx_dhcp_stop, nx_dhcp_user_option_retrieve, nx_dhcp_user_option_convert</span><span class="sxs-lookup"><span data-stu-id="73076-227">nx_dhcp_create, nx_dhcp_delete, nx_dhcp_release, nx_dhcp_state_change_notify, nx_dhcp_stop, nx_dhcp_user_option_retrieve, nx_dhcp_user_option_convert</span></span>

## <a name="nx_dhcp_server_stop"></a><span data-ttu-id="73076-228">nx_dhcp_server_stop</span><span class="sxs-lookup"><span data-stu-id="73076-228">nx_dhcp_server_stop</span></span>

<span data-ttu-id="73076-229">Arresta l'elaborazione del server DHCP</span><span class="sxs-lookup"><span data-stu-id="73076-229">Stops DHCP Server processing</span></span>

### <a name="prototype"></a><span data-ttu-id="73076-230">Prototipo</span><span class="sxs-lookup"><span data-stu-id="73076-230">Prototype</span></span>

```c
UINT nx_dhcp_server_stop(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="73076-231">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73076-231">Description</span></span>

<span data-ttu-id="73076-232">Questo servizio interrompe l'elaborazione del server DHCP, che include la ricezione di richieste client DHCP.</span><span class="sxs-lookup"><span data-stu-id="73076-232">This service stops DHCP Server processing, which includes of receiving DHCP Client requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="73076-233">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="73076-233">Input Parameters</span></span>

- <span data-ttu-id="73076-234">**dhcp_ptr**: puntatore all'istanza del server DHCP.</span><span class="sxs-lookup"><span data-stu-id="73076-234">**dhcp_ptr**: Pointer to DHCP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="73076-235">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="73076-235">Return Values</span></span>

- <span data-ttu-id="73076-236">**NX_SUCCESS**: (0x00) l'arresto DHCP è riuscito.</span><span class="sxs-lookup"><span data-stu-id="73076-236">**NX_SUCCESS**: (0x00) Successful DHCP stop.</span></span>
- <span data-ttu-id="73076-237">**NX_DHCP_ALREADY_STARTED**: (0X93) DHCP è già avviato.</span><span class="sxs-lookup"><span data-stu-id="73076-237">**NX_DHCP_ALREADY_STARTED**: (0x93) DHCP already started.</span></span>
- <span data-ttu-id="73076-238">NX_PTR_ERROR: (0x16) input puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="73076-238">NX_PTR_ERROR: (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="73076-239">NX_CALLER_ERROR: (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="73076-239">NX_CALLER_ERROR: (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="73076-240">NX_DHCP_PARAMETER_ERROR: (0x92) non è stato inserito alcun puntatore non valido.</span><span class="sxs-lookup"><span data-stu-id="73076-240">NX_DHCP_PARAMETER_ERROR: (0x92) Invalid non pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="73076-241">Consentito da</span><span class="sxs-lookup"><span data-stu-id="73076-241">Allowed From</span></span>

<span data-ttu-id="73076-242">Thread</span><span class="sxs-lookup"><span data-stu-id="73076-242">Threads</span></span>

### <a name="example"></a><span data-ttu-id="73076-243">Esempio</span><span class="sxs-lookup"><span data-stu-id="73076-243">Example</span></span>

```c
/* Stop the DHCP Server processing for this IP instance. */
status = nx_dhcp_server_stop(&dhcp_server);  

/* If status is NX_SUCCESS the DHCP Server was successfully stopped. */
```
