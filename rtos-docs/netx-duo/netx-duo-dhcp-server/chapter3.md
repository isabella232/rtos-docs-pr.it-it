---
title: Capitolo 3-Descrizione dei servizi server DHCP di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi server DHCP di NetX Duo (elencati di seguito) in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 33eb0b4bd98f808124b9a6a1f01950639243d612
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822010"
---
# <a name="chapter-3---description-of-azure-rtos-netx-duo-dhcp-server-services"></a><span data-ttu-id="57164-103">Capitolo 3-Descrizione dei servizi server DHCP di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="57164-103">Chapter 3 - Description of Azure RTOS NetX Duo DHCP Server Services</span></span>

<span data-ttu-id="57164-104">Questo capitolo contiene una descrizione di tutti i servizi server DHCP di NetX Duo (elencati di seguito) in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="57164-104">This chapter contains a description of all NetX Duo DHCP Server services (listed below) in alphabetic order.</span></span>

> [!NOTE]
> <span data-ttu-id="57164-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="57164-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

## <a name="nx_dhcp_server-create"></a><span data-ttu-id="57164-106">creazione nx_dhcp_server</span><span class="sxs-lookup"><span data-stu-id="57164-106">nx_dhcp_server create</span></span>

<span data-ttu-id="57164-107">Creare un'istanza del server DHCP</span><span class="sxs-lookup"><span data-stu-id="57164-107">Create a DHCP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="57164-108">Prototipo</span><span class="sxs-lookup"><span data-stu-id="57164-108">Prototype</span></span>

```C
UINT nx_dhcp_server_create(NX_DHCP_SERVER *dhcp_ptr, NX_IP *ip_ptr,
    VOID *stack_ptr, ULONG stack_size,
    CHAR *input_address_list, CHAR *name_ptr, NX_PACKET_POOL *packet_pool_ptr);
```

### <a name="description"></a><span data-ttu-id="57164-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57164-109">Description</span></span>

<span data-ttu-id="57164-110">Questo servizio crea un'istanza del server DHCP con un'istanza IP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="57164-110">This service creates a DHCP Server instance with a previously created IP instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57164-111">L'applicazione deve verificare che il pool di pacchetti creato per il servizio di creazione IP disponga di un payload di 548 byte minimo, esclusi le intestazioni UDP, IP e Ethernet.</span><span class="sxs-lookup"><span data-stu-id="57164-111">The application must make sure the packet pool created for the IP create service has a minimum 548 byte payload, not including the UDP, IP and Ethernet headers.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="57164-112">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="57164-112">Input Parameters</span></span>

- <span data-ttu-id="57164-113">**dhcp_ptr** Puntatore al blocco di controllo server DHCP.</span><span class="sxs-lookup"><span data-stu-id="57164-113">**dhcp_ptr** Pointer to DHCP Server control block.</span></span>
- <span data-ttu-id="57164-114">**ip_ptr** Puntatore all'istanza IP del server DHCP.</span><span class="sxs-lookup"><span data-stu-id="57164-114">**ip_ptr** Pointer to DHCP Server IP instance.</span></span>
- <span data-ttu-id="57164-115">**stack_ptr** Posizione dello stack del server DHCP del puntatore.</span><span class="sxs-lookup"><span data-stu-id="57164-115">**stack_ptr** Pointer DHCP Server stack location.</span></span>
- <span data-ttu-id="57164-116">**Stack_size dimensioni dello stack server DHCP** input_address_list puntatore all'elenco di indirizzi IP del server</span><span class="sxs-lookup"><span data-stu-id="57164-116">**stack_size Size of DHCP Server stack** input_address_list Pointer to Server’s list of IP addresses</span></span>
- <span data-ttu-id="57164-117">puntatore **name_ptr al nome del server dhcp** packet_pool_ptr puntatore al pool di pacchetti del server DHCP</span><span class="sxs-lookup"><span data-stu-id="57164-117">**name_ptr Pointer to DHCP Server name** packet_pool_ptr Pointer to DHCP Server packet pool</span></span>

### <a name="return-values"></a><span data-ttu-id="57164-118">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="57164-118">Return Values</span></span>

- <span data-ttu-id="57164-119">**NX_SUCCESS** (0x00) il server DHCP è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="57164-119">**NX_SUCCESS** (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="57164-120">Errore del payload del pacchetto **NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD** (0xA9) troppo piccolo</span><span class="sxs-lookup"><span data-stu-id="57164-120">**NX_DHCP_INADEQUATE_PACKET_POOL_PAYLOAD** (0xA9) Packet payload too small error</span></span>
- <span data-ttu-id="57164-121">L'elenco di opzioni del server **NX_DHCP_NO_SERVER_OPTION_LIST** (0x96) è vuoto</span><span class="sxs-lookup"><span data-stu-id="57164-121">**NX_DHCP_NO_SERVER_OPTION_LIST** (0x96) Server option list is empty</span></span>
- <span data-ttu-id="57164-122">NX_DHCP_PARAMETER_ERROR (0x92) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="57164-122">NX_DHCP_PARAMETER_ERROR (0x92) Invalid non pointer input</span></span>
- <span data-ttu-id="57164-123">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="57164-123">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="57164-124">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="57164-124">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="57164-125">Consentito da</span><span class="sxs-lookup"><span data-stu-id="57164-125">Allowed From</span></span>

<span data-ttu-id="57164-126">Applicazione</span><span class="sxs-lookup"><span data-stu-id="57164-126">Application</span></span>

### <a name="example"></a><span data-ttu-id="57164-127">Esempio</span><span class="sxs-lookup"><span data-stu-id="57164-127">Example</span></span>

```C
/* Create a DHCP Server instance. */

status = nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
    DEMO_SERVER_STACK_SIZE, SERVER_IP_ADDRESS_LIST, "DHCP server", &server_pool);

/* If status is NX_SUCCESS a DHCP Server instance was successfully created. */
```

## <a name="nx_dhcp_create_server_ip_address_list"></a><span data-ttu-id="57164-128">nx_dhcp_create_server_ip_address_list</span><span class="sxs-lookup"><span data-stu-id="57164-128">nx_dhcp_create_server_ip_address_list</span></span>

<span data-ttu-id="57164-129">Creare un pool di indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="57164-129">Create a IP address pool</span></span>

### <a name="prototype"></a><span data-ttu-id="57164-130">Prototipo</span><span class="sxs-lookup"><span data-stu-id="57164-130">Prototype</span></span>

```C
UINT nx_dhcp_create_server_ip_address_list(NX_DHCP_SERVER *dhcp_ptr,
    UINT iface_index, ULONG start_ip_address,
    ULONG end_ip_address, UINT *addresses_added);
```

### <a name="description"></a><span data-ttu-id="57164-131">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57164-131">Description</span></span>

<span data-ttu-id="57164-132">Questo servizio crea un pool specifico dell'interfaccia di rete di indirizzi IP disponibili per il server DHCP specificato da assegnare.</span><span class="sxs-lookup"><span data-stu-id="57164-132">This service creates a network interface specific pool of available IP addresses for the specified DHCP server to assign.</span></span> <span data-ttu-id="57164-133">Gli indirizzi IP di inizio e di fine devono corrispondere all'interfaccia di rete specificata.</span><span class="sxs-lookup"><span data-stu-id="57164-133">The start and end IP addresses must match the specified network interface.</span></span> <span data-ttu-id="57164-134">Il numero effettivo di indirizzi IP aggiunti può essere inferiore al totale degli indirizzi se l'elenco di indirizzi IP non è sufficientemente grande (impostazione configurabile dall'utente *NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* parametro).</span><span class="sxs-lookup"><span data-stu-id="57164-134">The actual number of IP addresses added may be less than the total addresses if the IP address list is not large enough (which is set in the user configurable *NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE* parameter).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="57164-135">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="57164-135">Input Parameters</span></span>

- <span data-ttu-id="57164-136">**dhcp_ptr** Puntatore al blocco di controllo server DHCP.</span><span class="sxs-lookup"><span data-stu-id="57164-136">**dhcp_ptr** Pointer to DHCP Server control block.</span></span>
- <span data-ttu-id="57164-137">**iface_index** Indice corrispondente all'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="57164-137">**iface_index** Index corresponding to network interface</span></span>
- <span data-ttu-id="57164-138">**start_ip_address** Primo indirizzo IP disponibile</span><span class="sxs-lookup"><span data-stu-id="57164-138">**start_ip_address** First available IP address</span></span>
- <span data-ttu-id="57164-139">**end_ip_address** Ultimo indirizzo IP disponibile</span><span class="sxs-lookup"><span data-stu-id="57164-139">**end_ip_address** Last of the available IP address</span></span>
- <span data-ttu-id="57164-140">**addresses_added** Numero di indirizzi IP aggiunti all'elenco</span><span class="sxs-lookup"><span data-stu-id="57164-140">**addresses_added** Number of IP addresses added to list</span></span>

### <a name="return-values"></a><span data-ttu-id="57164-141">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="57164-141">Return Values</span></span>

- <span data-ttu-id="57164-142">**NX_SUCCESS** (0x00) il server DHCP è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="57164-142">**NX_SUCCESS** (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="57164-143">L'indice **NX_DHCP_SERVER_BAD_INTERFACE_INDEX** (0xA1) non corrisponde agli indirizzi</span><span class="sxs-lookup"><span data-stu-id="57164-143">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX** (0xA1) Index does not match addresses</span></span>
- <span data-ttu-id="57164-144">Input dell'indirizzo di **NX_DHCP_INVALID_IP_ADDRESS_LIST** (0X99) non valido</span><span class="sxs-lookup"><span data-stu-id="57164-144">**NX_DHCP_INVALID_IP_ADDRESS_LIST** (0x99) Invalid address input</span></span>
- <span data-ttu-id="57164-145">Indirizzi di inizio/fine illogici NX_DHCP_INVALID_IP_ADDRESS (0x9B)</span><span class="sxs-lookup"><span data-stu-id="57164-145">NX_DHCP_INVALID_IP_ADDRESS (0x9B) Illogical start/end addresses</span></span>
- <span data-ttu-id="57164-146">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="57164-146">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="57164-147">Consentito da</span><span class="sxs-lookup"><span data-stu-id="57164-147">Allowed From</span></span>

<span data-ttu-id="57164-148">Applicazione</span><span class="sxs-lookup"><span data-stu-id="57164-148">Application</span></span>

### <a name="example"></a><span data-ttu-id="57164-149">Esempio</span><span class="sxs-lookup"><span data-stu-id="57164-149">Example</span></span>

```C
/* Create a pool of available IP addresses to assign. */

status = nx_dhcp_create_server_ip_list(&dhcp_server, iface_index,
    START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);

/* If status is NX_SUCCESS a IP address list was successfully created.
    addresses_added indicates how many IP addresses were actually added to the
    list. */
```

## <a name="nx_dhcp_clear_client_record"></a><span data-ttu-id="57164-150">nx_dhcp_clear_client_record</span><span class="sxs-lookup"><span data-stu-id="57164-150">nx_dhcp_clear_client_record</span></span>

<span data-ttu-id="57164-151">Rimuovi record client dal database del server</span><span class="sxs-lookup"><span data-stu-id="57164-151">Remove Client record from Server database</span></span>

### <a name="prototype"></a><span data-ttu-id="57164-152">Prototipo</span><span class="sxs-lookup"><span data-stu-id="57164-152">Prototype</span></span>

```C
UINT nx_dhcp_clear_client_record(NX_DHCP_SERVER *dhcp_ptr,
    NX_DHCP_CLIENT *dhcp_client_ptr);
```

### <a name="description"></a><span data-ttu-id="57164-153">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57164-153">Description</span></span>

<span data-ttu-id="57164-154">Questo servizio Cancella il record client dal database del server.</span><span class="sxs-lookup"><span data-stu-id="57164-154">This service clears the Client record from the Server database.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="57164-155">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="57164-155">Input Parameters</span></span>

- <span data-ttu-id="57164-156">**dhcp_ptr** Puntatore al blocco di controllo server DHCP.</span><span class="sxs-lookup"><span data-stu-id="57164-156">**dhcp_ptr** Pointer to DHCP Server control block.</span></span>
- <span data-ttu-id="57164-157">**dhcp_client_ptr puntatore al client DHCP da rimuovere**</span><span class="sxs-lookup"><span data-stu-id="57164-157">**dhcp_client_ptr Pointer to DHCP Client to remove**</span></span>

### <a name="return-values"></a><span data-ttu-id="57164-158">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="57164-158">Return Values</span></span>

- <span data-ttu-id="57164-159">**NX_SUCCESS** (0x00) il server DHCP è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="57164-159">**NX_SUCCESS** (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="57164-160">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="57164-160">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="57164-161">NX_CALLER_ERROR (0x11) chiamante non thread del servizio</span><span class="sxs-lookup"><span data-stu-id="57164-161">NX_CALLER_ERROR (0x11) Non thread caller of service</span></span>

### <a name="allowed-from"></a><span data-ttu-id="57164-162">Consentito da</span><span class="sxs-lookup"><span data-stu-id="57164-162">Allowed From</span></span>

<span data-ttu-id="57164-163">Applicazione</span><span class="sxs-lookup"><span data-stu-id="57164-163">Application</span></span>

### <a name="example"></a><span data-ttu-id="57164-164">Esempio</span><span class="sxs-lookup"><span data-stu-id="57164-164">Example</span></span>

```C
/* Remove Client record from the server database. */
status = nx_dhcp_clear_client_record(&dhcp_server, &dhcp_client_ptr);

/* If status is NX_SUCCESS the specified Client was removed from the database. */
```

## <a name="nx_dhcp_set_interface_network_parameters"></a><span data-ttu-id="57164-165">nx_dhcp_set_interface_network_parameters</span><span class="sxs-lookup"><span data-stu-id="57164-165">nx_dhcp_set_interface_network_parameters</span></span>

<span data-ttu-id="57164-166">Impostare i parametri di rete per le opzioni DHCP</span><span class="sxs-lookup"><span data-stu-id="57164-166">Set network parameters for DHCP options</span></span>

### <a name="prototype"></a><span data-ttu-id="57164-167">Prototipo</span><span class="sxs-lookup"><span data-stu-id="57164-167">Prototype</span></span>

```C
UINT nx_dhcp_set_interface_network_parameters(NX_DHCP_SERVER *dhcp_ptr,
    UINT iface_index, ULONG subnet_mask,
    ULONG default_gateway_address,
    ULONG dns_server_address);
```

### <a name="description"></a><span data-ttu-id="57164-168">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57164-168">Description</span></span>

<span data-ttu-id="57164-169">Questo servizio imposta i valori predefiniti per i parametri critici della rete per l'interfaccia specificata.</span><span class="sxs-lookup"><span data-stu-id="57164-169">This service sets default values for network critical parameters for the specified interface.</span></span> <span data-ttu-id="57164-170">Il server DHCP includerà queste opzioni nell'offerta e le risposte ACK al client DHCP.</span><span class="sxs-lookup"><span data-stu-id="57164-170">The DHCP server will include these options in its OFFER and ACK replies to the DHCP Client.</span></span> <span data-ttu-id="57164-171">Se i parametri dell'interfaccia del set di host in cui è in esecuzione un server DHCP, i parametri vengono impostati come predefiniti come indicato di seguito: il router impostato sul gateway di interfaccia principale per il server DHCP stesso, l'indirizzo del server DNS per il server DHCP stesso e il subnet mask allo stesso modo in cui è configurata l'interfaccia server DHCP.</span><span class="sxs-lookup"><span data-stu-id="57164-171">If the host set interface parameters on which a DHCP server is running, the parameters will defaulted as follows: the router set to the primary interface gateway for the DHCP server itself, the DNS server address to the DHCP server itself, and the subnet mask to the same as the DHCP server interface is configured with.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="57164-172">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="57164-172">Input Parameters</span></span>

- <span data-ttu-id="57164-173">**dhcp_ptr** Puntatore al blocco di controllo server DHCP.</span><span class="sxs-lookup"><span data-stu-id="57164-173">**dhcp_ptr** Pointer to DHCP Server control block.</span></span>
- <span data-ttu-id="57164-174">**iface_index** Indice corrispondente all'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="57164-174">**iface_index** Index corresponding to network interface</span></span>
- <span data-ttu-id="57164-175">**subnet_mask** Subnet mask per rete client</span><span class="sxs-lookup"><span data-stu-id="57164-175">**subnet_mask** Subnet mask for Client network</span></span>
- <span data-ttu-id="57164-176">**default_gateway_address** Indirizzo IP del router del client</span><span class="sxs-lookup"><span data-stu-id="57164-176">**default_gateway_address** Client’s router IP address</span></span>
- <span data-ttu-id="57164-177">**dns_server_address** Server DNS per la rete del client</span><span class="sxs-lookup"><span data-stu-id="57164-177">**dns_server_address** DNS server for Client’s network</span></span>

### <a name="return-values"></a><span data-ttu-id="57164-178">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="57164-178">Return Values</span></span>

- <span data-ttu-id="57164-179">**NX_SUCCESS** (0x00) il server DHCP è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="57164-179">**NX_SUCCESS** (0x00) Successful DHCP Server create.</span></span>
- <span data-ttu-id="57164-180">L'indice **NX_DHCP_SERVER_BAD_INTERFACE_INDEX** (0xA1) non corrisponde agli indirizzi</span><span class="sxs-lookup"><span data-stu-id="57164-180">**NX_DHCP_SERVER_BAD_INTERFACE_INDEX** (0xA1) Index does not match addresses</span></span>
- <span data-ttu-id="57164-181">Parametri di rete non validi per **NX_DHCP_INVALID_NETWORK_PARAMETERS** (0xA3)</span><span class="sxs-lookup"><span data-stu-id="57164-181">**NX_DHCP_INVALID_NETWORK_PARAMETERS** (0xA3) Invalid network parameters</span></span>
- <span data-ttu-id="57164-182">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="57164-182">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="57164-183">Consentito da</span><span class="sxs-lookup"><span data-stu-id="57164-183">Allowed From</span></span>

<span data-ttu-id="57164-184">Applicazione</span><span class="sxs-lookup"><span data-stu-id="57164-184">Application</span></span>

### <a name="example"></a><span data-ttu-id="57164-185">Esempio</span><span class="sxs-lookup"><span data-stu-id="57164-185">Example</span></span>

```C
/* Set network parameters for a specific interface. */

status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
    NX_DHCP_SUBNET_MASK, NX_DHCP_DEFAULT_GATEWAY,
    NX_DHCP_DNS_SERVER);

/* If status is NX_SUCCESS network parameters were successfully set. */
```

## <a name="nx_dhcp_server_delete"></a><span data-ttu-id="57164-186">nx_dhcp_server_delete</span><span class="sxs-lookup"><span data-stu-id="57164-186">nx_dhcp_server_delete</span></span>

<span data-ttu-id="57164-187">Eliminare un'istanza del server DHCP</span><span class="sxs-lookup"><span data-stu-id="57164-187">Delete a DHCP Server instance</span></span>

### <a name="prototype"></a><span data-ttu-id="57164-188">Prototipo</span><span class="sxs-lookup"><span data-stu-id="57164-188">Prototype</span></span>

```C
UINT nx_dhcp_server_delete(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="57164-189">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57164-189">Description</span></span>

<span data-ttu-id="57164-190">Questo servizio Elimina un'istanza del server DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="57164-190">This service deletes a previously created DHCP Server instance.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="57164-191">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="57164-191">Input Parameters</span></span>

- <span data-ttu-id="57164-192">**dhcp_ptr** Puntatore a un'istanza del server DHCP.</span><span class="sxs-lookup"><span data-stu-id="57164-192">**dhcp_ptr** Pointer to a DHCP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="57164-193">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="57164-193">Return Values</span></span>

- <span data-ttu-id="57164-194">Eliminazione del server DHCP riuscita **NX_SUCCESS** (0x00).</span><span class="sxs-lookup"><span data-stu-id="57164-194">**NX_SUCCESS** (0x00) Successful DHCP Server delete.</span></span>
- <span data-ttu-id="57164-195">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="57164-195">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="57164-196">NX_DHCP_PARAMETER_ERROR (0x92) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="57164-196">NX_DHCP_PARAMETER_ERROR (0x92) Invalid non pointer input</span></span>
- <span data-ttu-id="57164-197">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="57164-197">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="57164-198">Consentito da</span><span class="sxs-lookup"><span data-stu-id="57164-198">Allowed From</span></span>

<span data-ttu-id="57164-199">Thread</span><span class="sxs-lookup"><span data-stu-id="57164-199">Threads</span></span>

### <a name="example"></a><span data-ttu-id="57164-200">Esempio</span><span class="sxs-lookup"><span data-stu-id="57164-200">Example</span></span>

```C
/* Delete a DHCP Server instance. */

status = nx_dhcp_server_delete(&dhcp_server);

/* If status is NX_SUCCESS the DHCP Server instance was successfully deleted. */
```

## <a name="nx_dhcp_server_start"></a><span data-ttu-id="57164-201">nx_dhcp_server_start</span><span class="sxs-lookup"><span data-stu-id="57164-201">nx_dhcp_server_start</span></span>

<span data-ttu-id="57164-202">Avviare l'elaborazione del server DHCP</span><span class="sxs-lookup"><span data-stu-id="57164-202">Start DHCP Server processing</span></span>

### <a name="prototype"></a><span data-ttu-id="57164-203">Prototipo</span><span class="sxs-lookup"><span data-stu-id="57164-203">Prototype</span></span>

```C
UINT nx_dhcp_server_start(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="57164-204">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57164-204">Description</span></span>

<span data-ttu-id="57164-205">Questo servizio avvia l'elaborazione del server DHCP, che include la creazione di un socket UDP del server, l'associazione della porta DHCP e l'attesa per la ricezione delle richieste DHCP del client.</span><span class="sxs-lookup"><span data-stu-id="57164-205">This service starts DHCP Server processing, which includes creating a server UDP socket, binding the DHCP port and waiting to receive Client DHCP requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="57164-206">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="57164-206">Input Parameters</span></span>

- <span data-ttu-id="57164-207">**dhcp_ptr** Puntatore all'istanza DHCP creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="57164-207">**dhcp_ptr** Pointer to previously created DHCP instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="57164-208">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="57164-208">Return Values</span></span>

- <span data-ttu-id="57164-209">Inizio del server **NX_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="57164-209">**NX_SUCCESS** (0x00) Successful Server start.</span></span>
- <span data-ttu-id="57164-210">**NX_DHCP_ALREADY_STARTED** DHCP (0x93) già avviato.</span><span class="sxs-lookup"><span data-stu-id="57164-210">**NX_DHCP_ALREADY_STARTED** (0x93) DHCP already started.</span></span>
- <span data-ttu-id="57164-211">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="57164-211">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="57164-212">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="57164-212">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="57164-213">NX_DHCP_PARAMETER_ERROR (0x92) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="57164-213">NX_DHCP_PARAMETER_ERROR (0x92) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="57164-214">Consentito da</span><span class="sxs-lookup"><span data-stu-id="57164-214">Allowed From</span></span>

<span data-ttu-id="57164-215">Thread</span><span class="sxs-lookup"><span data-stu-id="57164-215">Threads</span></span>

### <a name="example"></a><span data-ttu-id="57164-216">Esempio</span><span class="sxs-lookup"><span data-stu-id="57164-216">Example</span></span>

```C
/* Start the DHCP Server processing for this IP instance. */

status = nx_dhcp_server_start(&dhcp_server);

/* If status is NX_SUCCESS the DHCP Server was successfully started. */
```

## <a name="nx_dhcp_server_stop"></a><span data-ttu-id="57164-217">nx_dhcp_server_stop</span><span class="sxs-lookup"><span data-stu-id="57164-217">nx_dhcp_server_stop</span></span>

<span data-ttu-id="57164-218">Arresta l'elaborazione del server DHCP</span><span class="sxs-lookup"><span data-stu-id="57164-218">Stops DHCP Server processing</span></span>

### <a name="prototype"></a><span data-ttu-id="57164-219">Prototipo</span><span class="sxs-lookup"><span data-stu-id="57164-219">Prototype</span></span>

```C
UINT nx_dhcp_server_stop(NX_DHCP_SERVER *dhcp_ptr);
```

### <a name="description"></a><span data-ttu-id="57164-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="57164-220">Description</span></span>

<span data-ttu-id="57164-221">Questo servizio interrompe l'elaborazione del server DHCP, che include la ricezione di richieste client DHCP.</span><span class="sxs-lookup"><span data-stu-id="57164-221">This service stops DHCP Server processing, which includes of receiving DHCP Client requests.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="57164-222">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="57164-222">Input Parameters</span></span>

- <span data-ttu-id="57164-223">**dhcp_ptr** Puntatore all'istanza del server DHCP.</span><span class="sxs-lookup"><span data-stu-id="57164-223">**dhcp_ptr** Pointer to DHCP Server instance.</span></span>

### <a name="return-values"></a><span data-ttu-id="57164-224">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="57164-224">Return Values</span></span>

- <span data-ttu-id="57164-225">Arresto DHCP **NX_SUCCESS** (0x00) riuscito.</span><span class="sxs-lookup"><span data-stu-id="57164-225">**NX_SUCCESS** (0x00) Successful DHCP stop.</span></span>
- <span data-ttu-id="57164-226">**NX_DHCP_ALREADY_STARTED** DHCP (0x93) già avviato.</span><span class="sxs-lookup"><span data-stu-id="57164-226">**NX_DHCP_ALREADY_STARTED** (0x93) DHCP already started.</span></span>
- <span data-ttu-id="57164-227">L'input del puntatore NX_PTR_ERROR (0x16) non è valido.</span><span class="sxs-lookup"><span data-stu-id="57164-227">NX_PTR_ERROR (0x16) Invalid pointer input.</span></span>
- <span data-ttu-id="57164-228">NX_CALLER_ERROR (0x11) il chiamante del servizio non è valido.</span><span class="sxs-lookup"><span data-stu-id="57164-228">NX_CALLER_ERROR (0x11) Invalid caller of service.</span></span>
- <span data-ttu-id="57164-229">NX_DHCP_PARAMETER_ERROR (0x92) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="57164-229">NX_DHCP_PARAMETER_ERROR (0x92) Invalid non pointer input</span></span>

### <a name="allowed-from"></a><span data-ttu-id="57164-230">Consentito da</span><span class="sxs-lookup"><span data-stu-id="57164-230">Allowed From</span></span>

<span data-ttu-id="57164-231">Thread</span><span class="sxs-lookup"><span data-stu-id="57164-231">Threads</span></span>

### <a name="example"></a><span data-ttu-id="57164-232">Esempio</span><span class="sxs-lookup"><span data-stu-id="57164-232">Example</span></span>

```C
/* Stop the DHCP Server processing for this IP instance. */

status = nx_dhcp_server_stop(&dhcp_server);

/* If status is NX_SUCCESS the DHCP Server was successfully stopped. */
```
