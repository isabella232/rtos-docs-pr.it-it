---
title: Capitolo 4-servizi server DHCPv6 di Azure RTO NetX Duo
description: Questo capitolo contiene una descrizione di tutti i servizi NetX Duo DHCPv6Server
author: philmea
ms.author: philmea
ms.date: 06/08/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 1d45139031b5a687baacf86c7a2e0a53c90533be
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821932"
---
# <a name="chapter-4---azure-rtos-netx-duo-dhcpv6-server-services"></a><span data-ttu-id="da103-103">Capitolo 4-servizi server DHCPv6 di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="da103-103">Chapter 4 - Azure RTOS NetX Duo DHCPv6 server services</span></span>

<span data-ttu-id="da103-104">Questo capitolo contiene una descrizione di tutti i servizi NetX Duo DHCPv6Server (elencati di seguito).</span><span class="sxs-lookup"><span data-stu-id="da103-104">This chapter contains a description of all NetX Duo DHCPv6Server services (listed below).</span></span>

<span data-ttu-id="da103-105">Nella sezione "valori restituiti" nelle descrizioni dell'API seguenti, i valori in **grassetto** non sono interessati dal **NX_DISABLE_ERROR_CHECKING** definire usato per disabilitare il controllo degli errori dell'API, mentre i valori non in grassetto sono completamente disabilitati.</span><span class="sxs-lookup"><span data-stu-id="da103-105">In the “Return Values” section in the following API descriptions, values in **BOLD** are not affected by the **NX_DISABLE_ERROR_CHECKING** define that is used to disable API error checking, while non-bold values are completely disabled.</span></span>

- <span data-ttu-id="da103-106">nx_dhcpv6_server_create *creare un ServerInstance DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="da103-106">nx_dhcpv6_server_create *Create a DHCPv6 serverinstance*</span></span>
- <span data-ttu-id="da103-107">nx_dhcpv6_server_delete *eliminare un ServerInstance DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="da103-107">nx_dhcpv6_server_delete *Delete a DHCPv6 serverinstance*</span></span>
- <span data-ttu-id="da103-108">nx_dhcpv6_server_start *avviare l'attività server DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="da103-108">nx_dhcpv6_server_start *Start the DHCPv6 server task*</span></span>
- <span data-ttu-id="da103-109">nx_dhcpv6_server_suspend *sospendere l'attività del server DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="da103-109">nx_dhcpv6_server_suspend *Suspend the DHCPv6 server task*</span></span>
- <span data-ttu-id="da103-110">nx_dhcpv6_server_resume *riprendere l'elaborazione del client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="da103-110">nx_dhcpv6_server_resume *Resume DHCPv6 client processing*</span></span>
- <span data-ttu-id="da103-111">nx_dhcpv6_server_suspend *sospendere l'elaborazione del client DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="da103-111">nx_dhcpv6_server_suspend *Suspend DHCPv6 client processing*</span></span>
- <span data-ttu-id="da103-112">nx_dhcpv6_create_dns_address *impostare il server DNS per le richieste di opzioni*</span><span class="sxs-lookup"><span data-stu-id="da103-112">nx_dhcpv6_create_dns_address *Set the DNS server for option requests*</span></span>
- <span data-ttu-id="da103-113">nx_dhcpv6_create_ip_address_range *creare l'intervallo di indirizzi IP da affittare*</span><span class="sxs-lookup"><span data-stu-id="da103-113">nx_dhcpv6_create_ip_address_range *Create the range of IP addresses to lease*</span></span>
- <span data-ttu-id="da103-114">nx_dhcpv6_reserve_ip_address_range *intervallo di riserva degli indirizzi IP nell'elenco dei server*</span><span class="sxs-lookup"><span data-stu-id="da103-114">nx_dhcpv6_reserve_ip_address_range *Reserve range of IP addresses in server list*</span></span>
- <span data-ttu-id="da103-115">nx_dhcpv6_set_server_duid *impostare il server Duid per i pacchetti DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="da103-115">nx_dhcpv6_set_server_duid *Set the Server DUID for DHCPv6 packets*</span></span>
- <span data-ttu-id="da103-116">nx_dhcpv6_add_ip_address_lease *aggiungere un record di lease alla tabella del server DHCPv6*</span><span class="sxs-lookup"><span data-stu-id="da103-116">nx_dhcpv6_add_ip_address_lease *Add a lease record to the DHCPv6 server table*</span></span>
- <span data-ttu-id="da103-117">Nx_dhcpv6_retrieve_ip_address_lease *recuperare un record di lease IP dalla tabella server*</span><span class="sxs-lookup"><span data-stu-id="da103-117">Nx_dhcpv6_retrieve_ip_address_lease *Retrieve an IP lease record from the Server table*</span></span>
- <span data-ttu-id="da103-118">nx_dhcpv6_add_client_record *aggiungere un record client DHCPv6 alla tabella server*</span><span class="sxs-lookup"><span data-stu-id="da103-118">nx_dhcpv6_add_client_record *Add a DHCPv6 Client record to the Server table*</span></span>
- <span data-ttu-id="da103-119">nx_dhcpv6_retrieve_client_record *recuperare un record client dalla tabella server*</span><span class="sxs-lookup"><span data-stu-id="da103-119">nx_dhcpv6_retrieve_client_record *Retrieve a client record from the Server table*</span></span>
- <span data-ttu-id="da103-120">nx_dhcpv6_server_interface_set *impostare l'indice dell'interfaccia per i servizi DHCPv6 del server*</span><span class="sxs-lookup"><span data-stu-id="da103-120">nx_dhcpv6_server_interface_set *Set the interface index for Server DHCPv6 services*</span></span>
- <span data-ttu-id="da103-121">nx_dhcpv6_server_option_request_handler_set *impostare il gestore della richiesta di opzione*</span><span class="sxs-lookup"><span data-stu-id="da103-121">nx_dhcpv6_server_option_request_handler_set *Set the option request handler*</span></span>

## <a name="nx_dhcpv6_create_dns_address"></a><span data-ttu-id="da103-122">nx_dhcpv6_create_dns_address</span><span class="sxs-lookup"><span data-stu-id="da103-122">nx_dhcpv6_create_dns_address</span></span>

### <a name="set-the-network-dns-server"></a><span data-ttu-id="da103-123">Impostare il server DNS di rete</span><span class="sxs-lookup"><span data-stu-id="da103-123">Set the network DNS server</span></span>

<span data-ttu-id="da103-124">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-124">**Prototype**</span></span>

```
UINT nx_dhcpv6_create_dns_address(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *dns_ipv6_address);
```

<span data-ttu-id="da103-125">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-125">**Description**</span></span>

<span data-ttu-id="da103-126">Questo servizio carica il server DHCPv6 con l'indirizzo del server DNS per l'interfaccia di rete del server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-126">This service loads the DHCPv6 Server with the DNS server address for the Server DHCPv6 network interface.</span></span>

<span data-ttu-id="da103-127">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-127">**Input Parameters**</span></span>

- <span data-ttu-id="da103-128">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-128">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-129">**dns_ipv6_address** Puntatore al server DNS</span><span class="sxs-lookup"><span data-stu-id="da103-129">**dns_ipv6_address** Pointer to the DNS server</span></span>

<span data-ttu-id="da103-130">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-130">**Return Values**</span></span>

- <span data-ttu-id="da103-131">**NX_SUCCESS** (0x00) DNS Serversaved all'istanza del server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-131">**NX_SUCCESS** (0x00) DNS Serversaved to DHCPv6 Server instance</span></span>
- <span data-ttu-id="da103-132">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) viene fornito un indirizzo non valido</span><span class="sxs-lookup"><span data-stu-id="da103-132">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) An invalid address is supplied</span></span>
- <span data-ttu-id="da103-133">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-133">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-134">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-134">**Allowed From**</span></span>

<span data-ttu-id="da103-135">codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da103-135">Application Code</span></span>

<span data-ttu-id="da103-136">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-136">**Example**</span></span>

```
/* Set the network DNS server with the input address for the Server DHCPv6interface. */
status = nx_dhcpv6_create__dns_address(&dhcp_server_0, &dns_ipv6_address);
/* If this service returns NX_SUCCESS the DNS server data was accepted. */
```

## <a name="nx_dhcpv6_create_ip_address_range"></a><span data-ttu-id="da103-137">nx_dhcpv6_create_ip_address_range</span><span class="sxs-lookup"><span data-stu-id="da103-137">nx_dhcpv6_create_ip_address_range</span></span>

### <a name="create-the-server-ip-address-list"></a><span data-ttu-id="da103-138">Creare l'elenco di indirizzi IP del server</span><span class="sxs-lookup"><span data-stu-id="da103-138">Create the Server IP address list</span></span>

<span data-ttu-id="da103-139">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-139">**Prototype**</span></span>

```
UINT _nx_dhcpv6_create_ip_address_range(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *start_ipv6_address, NXD_ADDRESS *end_ipv6_address, 
     UINT *addresses_added)
```

<span data-ttu-id="da103-140">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-140">**Description**</span></span>

<span data-ttu-id="da103-141">Questo servizio crea l'elenco di indirizzi IP specificato dagli indirizzi iniziale e finale dell'intervallo di indirizzi assegnabile del server.</span><span class="sxs-lookup"><span data-stu-id="da103-141">This service creates the IP address list specified by the start and end addresses of the Server’s assignable address range.</span></span> <span data-ttu-id="da103-142">Gli indirizzi iniziale e finale devono corrispondere al prefisso dell'indirizzo di interfaccia server (deve trovarsi nello stesso collegamento dell'interfaccia DHCPv6 del server).</span><span class="sxs-lookup"><span data-stu-id="da103-142">The start and end addresses must match the Server interface address prefix (must be on the same link as the Server DHCPv6 interface).</span></span> <span data-ttu-id="da103-143">Viene restituito il numero di indirizzi effettivamente aggiunti.</span><span class="sxs-lookup"><span data-stu-id="da103-143">The number of addresses actually added is returned.</span></span>

<span data-ttu-id="da103-144">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-144">**Input Parameters**</span></span>

- <span data-ttu-id="da103-145">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-145">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-146">**start_ipv6_address** Inizio degli indirizzi da aggiungere</span><span class="sxs-lookup"><span data-stu-id="da103-146">**start_ipv6_address** Start of addresses to add</span></span>
- <span data-ttu-id="da103-147">**end_ipv6_address** Fine degli indirizzi da aggiungere</span><span class="sxs-lookup"><span data-stu-id="da103-147">**end_ipv6_address** End of addresses to add</span></span>
- <span data-ttu-id="da103-148">\***addresses_added** Output degli indirizzi aggiunti</span><span class="sxs-lookup"><span data-stu-id="da103-148">\***addresses_added** Output of addresses added</span></span>

<span data-ttu-id="da103-149">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-149">**Return Values**</span></span>

- <span data-ttu-id="da103-150">Elenco di indirizzi IP **NX_SUCCESS** (0x00) creato correttamente</span><span class="sxs-lookup"><span data-stu-id="da103-150">**NX_SUCCESS** (0x00) IP address list successfully created</span></span>
- <span data-ttu-id="da103-151">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) viene fornito un indirizzo non valido</span><span class="sxs-lookup"><span data-stu-id="da103-151">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) An invalid address is supplied</span></span>
- <span data-ttu-id="da103-152">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-152">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-153">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-153">**Allowed From**</span></span>

<span data-ttu-id="da103-154">codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da103-154">Application Code</span></span>

<span data-ttu-id="da103-155">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-155">**Example**</span></span>

```
/* Create the Server IP address list for the server DHCPv6 interface. */
status = nx_dhcpv6_create_ip_address_range(&dhcp_server_0,
         &start_ipv6_address, &end_ipv6_address, &addresses_reserved);
/* If status is NX_SUCCESS one or more addresses were successfully added. */
```

## <a name="nx_dhcpv6_reserve_ip_address_range"></a><span data-ttu-id="da103-156">nx_dhcpv6_reserve_ip_address_range</span><span class="sxs-lookup"><span data-stu-id="da103-156">nx_dhcpv6_reserve_ip_address_range</span></span>

### <a name="reserve-specified-range-of-ip-addresses"></a><span data-ttu-id="da103-157">Riserva l'intervallo specificato di indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="da103-157">Reserve specified range of IP addresses</span></span>

<span data-ttu-id="da103-158">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-158">**Prototype**</span></span>

```
UINT _nx_dhcpv6_reserve_ip_address_range(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     NXD_ADDRESS *start_ipv6_address, NXD_ADDRESS *end_ipv6_address, 
     UINT *addresses_reserved)
```

<span data-ttu-id="da103-159">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-159">**Description**</span></span>

<span data-ttu-id="da103-160">Questo servizio riserva l'intervallo di indirizzi IP specificato dagli indirizzi iniziale e finale.</span><span class="sxs-lookup"><span data-stu-id="da103-160">This service reserves the IP address range specified by the start and end addresses.</span></span> <span data-ttu-id="da103-161">Questi indirizzi devono essere compresi nell'intervallo di indirizzi IP del server creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="da103-161">These addresses must be within in the previously created server IP address range.</span></span> <span data-ttu-id="da103-162">Questi indirizzi non verranno assegnati ad alcun client dal server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-162">These addresses will not be assigned to any Clients by the DHCPv6 Server.</span></span> <span data-ttu-id="da103-163">Gli indirizzi iniziale e finale devono corrispondere al prefisso dell'indirizzo di interfaccia server (deve trovarsi nello stesso collegamento dell'interfaccia di rete del server DHCPv6).</span><span class="sxs-lookup"><span data-stu-id="da103-163">The start and end addresses must match the Server interface address prefix (must be on the same link as the Server DHCPv6 network interface).</span></span> <span data-ttu-id="da103-164">Viene restituito il numero di indirizzi effettivamente riservati.</span><span class="sxs-lookup"><span data-stu-id="da103-164">The number of addresses actually reserved is returned.</span></span>

<span data-ttu-id="da103-165">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-165">**Input Parameters**</span></span>

- <span data-ttu-id="da103-166">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-166">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-167">**start_ipv6_address** Inizio degli indirizzi da riservare</span><span class="sxs-lookup"><span data-stu-id="da103-167">**start_ipv6_address** Start of addresses to reserve</span></span>
- <span data-ttu-id="da103-168">**end_ipv6_address** Fine degli indirizzi da riservare</span><span class="sxs-lookup"><span data-stu-id="da103-168">**end_ipv6_address** End of addresses to reserve</span></span>
- <span data-ttu-id="da103-169">\***addresses_reserved** Numero di indirizzi riservati</span><span class="sxs-lookup"><span data-stu-id="da103-169">\***addresses_reserved** Number of addresses reserved</span></span>

<span data-ttu-id="da103-170">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-170">**Return Values**</span></span>

- <span data-ttu-id="da103-171">Creazione ed elaborazione del messaggio di rilascio di **NX_SUCCESS** (0x00) completato</span><span class="sxs-lookup"><span data-stu-id="da103-171">**NX_SUCCESS** (0x00) RELEASE message successfully created and processed</span></span>
- <span data-ttu-id="da103-172">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) viene fornito un indirizzo non valido</span><span class="sxs-lookup"><span data-stu-id="da103-172">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) An invalid address is supplied</span></span>
- <span data-ttu-id="da103-173">Impossibile trovare l'indirizzo di avvio **NX_DHCPV6_INVALID_IP_ADDRESS** (0xED1) nell'elenco degli indirizzi del server.</span><span class="sxs-lookup"><span data-stu-id="da103-173">**NX_DHCPV6_INVALID_IP_ADDRESS** (0xED1) Starting address not found in Server address list.</span></span>
- <span data-ttu-id="da103-174">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-174">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-175">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-175">**Allowed From**</span></span>

<span data-ttu-id="da103-176">codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da103-176">Application Code</span></span>

<span data-ttu-id="da103-177">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-177">**Example**</span></span>

```
/* Reserve a range of ip addresses in the Server address table for the server DHCPv6 
network interface. */

status = nx_dhcpv6_reserve_ip_address_range(&dhcp_server_0,
         &start_ipv6_address, &end_ipv6_address, &addresses_reserved);

/* If status is NX_SUCCESS one or more addresses were successfully reserved. */
```

## <a name="nx_dhcpv6_server_create"></a><span data-ttu-id="da103-178">nx_dhcpv6_server_create</span><span class="sxs-lookup"><span data-stu-id="da103-178">nx_dhcpv6_server_create</span></span>

### <a name="create-the-dhcpv6-server-instance"></a><span data-ttu-id="da103-179">Creazione dell'istanza del server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-179">Create the DHCPv6 Server instance</span></span> 

<span data-ttu-id="da103-180">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-180">**Prototype**</span></span>

```
UINT nx_dhcpv6_server_create(NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
        NX_IP *ip_ptr, CHAR *name_ptr, 
        NX_PACKET_POOL *packet_pool_ptr, 
        VOID *stack_ptr,ULONG stack_size,
    VOID (*dhcpv6_address_declined_handler)(struct 
        NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
        NX_DHCPV6_CLIENT *dhcpv6_client_ptr, 
        UINT message),
    VOID (*dhcpv6_option_request_handler)(
        struct NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
        UINT option_request, UCHAR *buffer_ptr, UINT *index));
```

<span data-ttu-id="da103-181">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-181">**Description**</span></span>

<span data-ttu-id="da103-182">Questo servizio crea l'attività server DHCPv6 con l'input specificato.</span><span class="sxs-lookup"><span data-stu-id="da103-182">This service creates the DHCPv6 Server task with the specified input.</span></span> <span data-ttu-id="da103-183">I gestori di callback sono input facoltativo.</span><span class="sxs-lookup"><span data-stu-id="da103-183">The callback handlers are optional input.</span></span> <span data-ttu-id="da103-184">Il puntatore dello stack, l'istanza IP e l'input del pool di pacchetti sono obbligatori.</span><span class="sxs-lookup"><span data-stu-id="da103-184">The stack pointer, IP instance and packet pool input are required.</span></span> <span data-ttu-id="da103-185">L'istanza IP e il pool di pacchetti devono essere già stati creati.</span><span class="sxs-lookup"><span data-stu-id="da103-185">The IP instance and packet pool must already be created.</span></span>

<span data-ttu-id="da103-186">L'utente è invitato a chiamare nx_dhcpv6_server_option_request_handler_set per impostare il gestore della richiesta di opzione.</span><span class="sxs-lookup"><span data-stu-id="da103-186">User is encouraged to call nx_dhcpv6_server_option_request_handler_set to set the option request handler.</span></span>

<span data-ttu-id="da103-187">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-187">**Input Parameters**</span></span>

- <span data-ttu-id="da103-188">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-188">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-189">**ip_ptr** Puntatore all'istanza IP</span><span class="sxs-lookup"><span data-stu-id="da103-189">**ip_ptr** Pointer to the IP instance</span></span>
- <span data-ttu-id="da103-190">**name_str** Puntatore al nome del server</span><span class="sxs-lookup"><span data-stu-id="da103-190">**name_str** Pointer to Server name</span></span>
- <span data-ttu-id="da103-191">**packet_pool_ptr** Puntatore al pool di pacchetti del server</span><span class="sxs-lookup"><span data-stu-id="da103-191">**packet_pool_ptr** Pointer to Server packet pool</span></span>
- <span data-ttu-id="da103-192">**stack_ptr** Puntatore alla memoria dello stack del server</span><span class="sxs-lookup"><span data-stu-id="da103-192">**stack_ptr** Pointer to Server stack memory</span></span>
- <span data-ttu-id="da103-193">**stack_size** Dimensione della memoria dello stack del server</span><span class="sxs-lookup"><span data-stu-id="da103-193">**stack_size** Size of Server stack memory</span></span>
- <span data-ttu-id="da103-194">**dhcpv6_address_declined_handler** Puntatore al gestore di messaggi di rifiuto o rilascio del client</span><span class="sxs-lookup"><span data-stu-id="da103-194">**dhcpv6_address_declined_handler** Pointer to Client Decline or Release message handler</span></span>
- <span data-ttu-id="da103-195">**dhcpv6_option_request_handler** Gestore opzioni di richiesta puntatore a opzioni</span><span class="sxs-lookup"><span data-stu-id="da103-195">**dhcpv6_option_request_handler** Pointer to options request option handler</span></span>

<span data-ttu-id="da103-196">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-196">**Return Values**</span></span>

- <span data-ttu-id="da103-197">Riattivazione del server **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="da103-197">**NX_SUCCESS** (0x00) Server successfully resumed</span></span>
- <span data-ttu-id="da103-198">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-198">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>
- <span data-ttu-id="da103-199">NX_DHCPV6_PARAM_ERROR input non valido del puntatore</span><span class="sxs-lookup"><span data-stu-id="da103-199">NX_DHCPV6_PARAM_ERROR Invalid non pointer input</span></span>

<span data-ttu-id="da103-200">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-200">**Allowed From**</span></span>

<span data-ttu-id="da103-201">codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da103-201">Application Code</span></span>

<span data-ttu-id="da103-202">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-202">**Example**</span></span>

```
/* Create the DHCPv6 Server. */
status = nx_dhcpv6_server_create(&dhcp_server_0, &ip_0, "DHCPv6 Server",
         &pool_0, stack_pointer,2048, dhcpv6_decline_handler,
         dhcpv6_get_time_handler);
/* If status is NX_SUCCESS the Server successfully created. */
```

## <a name="nx_dhcpv6_server_delete"></a><span data-ttu-id="da103-203">nx_dhcpv6_server_delete</span><span class="sxs-lookup"><span data-stu-id="da103-203">nx_dhcpv6_server_delete</span></span>

### <a name="delete-the-dhcpv6-server"></a><span data-ttu-id="da103-204">Eliminare il server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-204">Delete the DHCPv6 Server</span></span>

<span data-ttu-id="da103-205">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-205">**Prototype**</span></span>

```
UINT _nx_dhcpv6_server_delee(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

<span data-ttu-id="da103-206">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-206">**Description**</span></span>

<span data-ttu-id="da103-207">Questo servizio Elimina l'attività server DHCPv6 e qualsiasi richiesta elaborata dal server.</span><span class="sxs-lookup"><span data-stu-id="da103-207">This service deletes the DHCPv6 Server task and any request that the Server was processing.</span></span>

<span data-ttu-id="da103-208">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-208">**Input Parameters**</span></span>

- <span data-ttu-id="da103-209">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-209">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="da103-210">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-210">**Return Values**</span></span>

- <span data-ttu-id="da103-211">Eliminazione del server **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="da103-211">**NX_SUCCESS** (0x00) Server successfully deleted</span></span>
- <span data-ttu-id="da103-212">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-212">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-213">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-213">**Allowed From**</span></span>

<span data-ttu-id="da103-214">Thread</span><span class="sxs-lookup"><span data-stu-id="da103-214">Threads</span></span>

<span data-ttu-id="da103-215">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-215">**Example**</span></span>

```
/* Delete the DHCPv6 Serve. */
status = nx_dhcpv6_server_delete(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully deleted. */
```

## <a name="nx_dhcpv6_server_resume"></a><span data-ttu-id="da103-216">nx_dhcpv6_server_resume</span><span class="sxs-lookup"><span data-stu-id="da103-216">nx_dhcpv6_server_resume</span></span>

### <a name="resume-dhcpv6-server-task"></a><span data-ttu-id="da103-217">Riavvia attività server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-217">Resume DHCPv6 Server task</span></span> 

<span data-ttu-id="da103-218">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-218">**Prototype**</span></span>

```
UINT _nx_dhcpv6_server_resume(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

<span data-ttu-id="da103-219">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-219">**Description**</span></span>

<span data-ttu-id="da103-220">Questo servizio riprende l'attività del server DHCPv6 e qualsiasi richiesta elaborata dal server.</span><span class="sxs-lookup"><span data-stu-id="da103-220">This service resumes the DHCPv6 Server task and any request that the Server was processing.</span></span>

<span data-ttu-id="da103-221">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-221">**Input Parameters**</span></span>

- <span data-ttu-id="da103-222">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-222">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="da103-223">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-223">**Return Values**</span></span>

- <span data-ttu-id="da103-224">Riattivazione del server **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="da103-224">**NX_SUCCESS** (0x00) Server successfully resumed</span></span>
- <span data-ttu-id="da103-225">Il server **NX_DHCPV6_ALREADY_STARTED** (0xE91) è già in esecuzione</span><span class="sxs-lookup"><span data-stu-id="da103-225">**NX_DHCPV6_ALREADY_STARTED** (0xE91) Server is running already</span></span>
- <span data-ttu-id="da103-226">**stato (variabile** ) threadX e stato di errore di NETX Duo</span><span class="sxs-lookup"><span data-stu-id="da103-226">**status** (variable) ThreadX and NetX Duo error status</span></span>
- <span data-ttu-id="da103-227">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-227">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-228">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-228">**Allowed From**</span></span>

<span data-ttu-id="da103-229">Thread</span><span class="sxs-lookup"><span data-stu-id="da103-229">Threads</span></span>

<span data-ttu-id="da103-230">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-230">**Example**</span></span>

```
/* Resume the DHCPv6 Server task. */
status = nx_dhcpv6_server_resume(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully resumed. */
```

## <a name="nx_dhcpv6_server_suspend"></a><span data-ttu-id="da103-231">nx_dhcpv6_server_suspend</span><span class="sxs-lookup"><span data-stu-id="da103-231">nx_dhcpv6_server_suspend</span></span>

### <a name="suspend-dhcpv6-server-task"></a><span data-ttu-id="da103-232">Sospendi attività server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-232">Suspend DHCPv6 Server task</span></span> 

<span data-ttu-id="da103-233">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-233">**Prototype**</span></span>

```
UINT _nx_dhcpv6_server_suspend(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

<span data-ttu-id="da103-234">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-234">**Description**</span></span>

<span data-ttu-id="da103-235">Questo servizio sospende l'attività del server DHCPv6 e qualsiasi richiesta elaborata dal server.</span><span class="sxs-lookup"><span data-stu-id="da103-235">This service suspends the DHCPv6 Server task and any request that the Server was processing.</span></span>

<span data-ttu-id="da103-236">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-236">**Input Parameters**</span></span>

- <span data-ttu-id="da103-237">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-237">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="da103-238">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-238">**Return Values**</span></span>

- <span data-ttu-id="da103-239">Riattivazione del server **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="da103-239">**NX_SUCCESS** (0x00) Server successfully resumed</span></span>
- <span data-ttu-id="da103-240">Il server **NX_DHCPV6_NOT_STARTED** (0xE92) non è stato avviato</span><span class="sxs-lookup"><span data-stu-id="da103-240">**NX_DHCPV6_NOT_STARTED** (0xE92) Server is not started</span></span> 
- <span data-ttu-id="da103-241">**Stato (variabile** ) threadX e stato di errore di NETX Duo</span><span class="sxs-lookup"><span data-stu-id="da103-241">**Status** (variable) ThreadX and NetX Duo error status</span></span>
- <span data-ttu-id="da103-242">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-242">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-243">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-243">**Allowed From**</span></span>

<span data-ttu-id="da103-244">Thread</span><span class="sxs-lookup"><span data-stu-id="da103-244">Threads</span></span>

<span data-ttu-id="da103-245">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-245">**Example**</span></span>

```
/* Suspend the DHCPv6 Server task. */
status = nx_dhcpv6_server_suspend(&dhcp_server_0);

/* If status is NX_SUCCESS the Server successfully suspended. */
```

## <a name="nx_dhcpv6_server_start"></a><span data-ttu-id="da103-246">nx_dhcpv6_server_start</span><span class="sxs-lookup"><span data-stu-id="da103-246">nx_dhcpv6_server_start</span></span>

### <a name="start-the-dhcpv6-server-task"></a><span data-ttu-id="da103-247">Avviare l'attività server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-247">Start the DHCPv6 Server task</span></span> 

<span data-ttu-id="da103-248">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-248">**Prototype**</span></span>

```
UINT _nx_dhcpv6_server_start(NX_DHCPV6_SERVER *dhcpv6_server_ptr)
```

<span data-ttu-id="da103-249">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-249">**Description**</span></span>

<span data-ttu-id="da103-250">Questo servizio avvia l'attività server DHCPv6 e legge il server per elaborare le richieste dell'applicazione per la ricezione di messaggi client DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-250">This service starts the DHCPv6 Server task and readies the Server to process application requests for receiving DHCPv6 Client messages.</span></span> <span data-ttu-id="da103-251">Verifica che l'istanza del server disponga di informazioni sufficienti (server DUID), crea e associa il socket UDP per l'invio e la ricezione di messaggi DHCPv6 e attiva i timer per tenere traccia dell'ora della sessione e della scadenza del lease IP.</span><span class="sxs-lookup"><span data-stu-id="da103-251">It verifies the Server instance has sufficient information (Server DUID), creates and binds the UDP socket for sending and receiving DHCPv6 messages, and activates timers for keeping track of session time and IP lease expiration.</span></span>

>[!NOTE] 
> <span data-ttu-id="da103-252">Prima di poter eseguire il server DHCPv6, l'applicazione host è responsabile della creazione dell'intervallo di indirizzi IP da cui il server può assegnare gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="da103-252">Before the DHCPv6 Server can run, the host application is responsible for creating the IP address range from which the Server can assign IP addresses.</span></span> <span data-ttu-id="da103-253">È anche responsabile dell'impostazione del server DUID e dell'interfaccia DHCPv6 (vedere rispettivamente *nx_dhcpv6_server_duid_set* e *nx_dhcpv6_server_interface_set* .</span><span class="sxs-lookup"><span data-stu-id="da103-253">It is also responsible for setting the Server DUID and DHCPv6 interface (see *nx_dhcpv6_server_duid_set* and *nx_dhcpv6_server_interface_set* respectively.</span></span>

<span data-ttu-id="da103-254">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-254">**Input Parameters**</span></span>

- <span data-ttu-id="da103-255">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-255">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="da103-256">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-256">**Return Values**</span></span>

- <span data-ttu-id="da103-257">Server **NX_SUCCESS** (0x00) avviato correttamente</span><span class="sxs-lookup"><span data-stu-id="da103-257">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="da103-258">Il server **NX_DHCPV6_ALREADY_STARTED** (0xE91) è già in esecuzione</span><span class="sxs-lookup"><span data-stu-id="da103-258">**NX_DHCPV6_ALREADY_STARTED** (0xE91) Server is running already</span></span>
- <span data-ttu-id="da103-259">Il server **NX_DHCPV6_NO_ASSIGNABLE_ADDRESSES** (0xEA7) non dispone di indirizzi assegnabili per il lease</span><span class="sxs-lookup"><span data-stu-id="da103-259">**NX_DHCPV6_NO_ASSIGNABLE_ADDRESSES** (0xEA7) Server has no assignable addresses to lease</span></span>
- <span data-ttu-id="da103-260">Indice indirizzo globale **NX_DHCPV6_INVALID_GLOBAL_INDEX** (0xE97) non impostato</span><span class="sxs-lookup"><span data-stu-id="da103-260">**NX_DHCPV6_INVALID_GLOBAL_INDEX** (0xE97) Global address index not set</span></span>
- <span data-ttu-id="da103-261">**NX_DHCPV6_NO_SERVER_DUID** (0XE92) senza Duid server creato</span><span class="sxs-lookup"><span data-stu-id="da103-261">**NX_DHCPV6_NO_SERVER_DUID** (0xE92) No Server DUID created</span></span> 
- <span data-ttu-id="da103-262">**stato (variabile** ) threadX e stato di errore di NETX Duo</span><span class="sxs-lookup"><span data-stu-id="da103-262">**status** (variable) ThreadX and NetX Duo error status</span></span>
- <span data-ttu-id="da103-263">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-263">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-264">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-264">**Allowed From**</span></span>

<span data-ttu-id="da103-265">Thread</span><span class="sxs-lookup"><span data-stu-id="da103-265">Threads</span></span>

<span data-ttu-id="da103-266">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-266">**Example**</span></span>

```
/* Start the DHCPv6 Server task. */
status = nx_dhcpv6_server_start(&dhcp_server_0);
/* If status is NX_SUCCESS the Server successfully started. */
```

## <a name="nx_dhcpv6_retrieve_ip_address_lease"></a><span data-ttu-id="da103-267">nx_dhcpv6_retrieve_ip_address_lease</span><span class="sxs-lookup"><span data-stu-id="da103-267">nx_dhcpv6_retrieve_ip_address_lease</span></span>

### <a name="get-an-ip-address-lease-from-the-server-table"></a><span data-ttu-id="da103-268">Ottenere un lease di indirizzi IP dalla tabella server</span><span class="sxs-lookup"><span data-stu-id="da103-268">Get an IP address lease from the Server table</span></span>

<span data-ttu-id="da103-269">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-269">**Prototype**</span></span>

```
UINT _nx_dhcpv6_retrieve_ip_address_lease(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, UINT table_index, 
     NXD_ADDRESS *lease_IP_address, ULONG *T1, ULONG *T2, 
     ULONG *valid_lifetime, ULONG *preferred_lifetime)
```

<span data-ttu-id="da103-270">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-270">**Description**</span></span>

<span data-ttu-id="da103-271">Questo servizio recupera un record di lease di indirizzi IP dalla tabella server in corrispondenza della posizione di indice della tabella specificata.</span><span class="sxs-lookup"><span data-stu-id="da103-271">This service retrieves an IP address lease record from the Server table at the specified table index location.</span></span> <span data-ttu-id="da103-272">Questa operazione può essere eseguita prima o dopo il recupero dei dati del record client.</span><span class="sxs-lookup"><span data-stu-id="da103-272">This can be done before or after retrieving Client record data.</span></span>

<span data-ttu-id="da103-273">La capacità di archiviare e recuperare i dati tra il server DHCPv6 e la memoria non volatile è un requisito del protocollo DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-273">The capability of storing and retrieving data between the DHCPv6 Server and non volatile memory is a requirement of the DHCPv6 protocol.</span></span> <span data-ttu-id="da103-274">Non fa alcuna differenza per quanto riguarda l'ordine in cui i dati di lease IP e i dati dei record client vengono salvati nella memoria non volatile.</span><span class="sxs-lookup"><span data-stu-id="da103-274">It makes no difference in what order IP lease data and Client record data is saved to nonvolatile memory.</span></span>

>[!NOTE] 
> <span data-ttu-id="da103-275">Non è consigliabile copiare dati in o da tabelle server senza arrestare o sospendere prima il server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-275">It is not recommended to copy data to or from Server tables without stopping or suspending the DHCPv6 Server first.</span></span>

<span data-ttu-id="da103-276">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-276">**Input Parameters**</span></span>

- <span data-ttu-id="da103-277">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-277">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-278">**table_index** Indice tabella in cui archiviare il lease</span><span class="sxs-lookup"><span data-stu-id="da103-278">**table_index** Table index to store lease at</span></span>
- <span data-ttu-id="da103-279">**lease_IP_address** Puntatore a indirizzo IP con lease per il client</span><span class="sxs-lookup"><span data-stu-id="da103-279">**lease_IP_address** Pointer to IP address leased to the Client</span></span>
- <span data-ttu-id="da103-280">**T1** Tempo di rinnovo richiesto dal client</span><span class="sxs-lookup"><span data-stu-id="da103-280">**T1** Client requested renew time</span></span>
- <span data-ttu-id="da103-281">**T2** Tempo di riassociazione richiesto dal client</span><span class="sxs-lookup"><span data-stu-id="da103-281">**T2** Client requested rebind time</span></span>
- <span data-ttu-id="da103-282">**valid_lifetime** Il lease client diventa deprecato</span><span class="sxs-lookup"><span data-stu-id="da103-282">**valid_lifetime** Client lease becomes deprecated</span></span>
- <span data-ttu-id="da103-283">**preferred_lifetime** Lease client non valido</span><span class="sxs-lookup"><span data-stu-id="da103-283">**preferred_lifetime** Client lease becomes invalid</span></span>

<span data-ttu-id="da103-284">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-284">**Return Values**</span></span>

- <span data-ttu-id="da103-285">Server **NX_SUCCESS** (0x00) avviato correttamente</span><span class="sxs-lookup"><span data-stu-id="da103-285">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="da103-286">Input di dati di lease IP di **NX_DHCPV6_PARAMETER_ERROR** (0XE93) non valido</span><span class="sxs-lookup"><span data-stu-id="da103-286">**NX_DHCPV6_PARAMETER_ERROR** (0xE93) Invalid IP lease data input</span></span>
- <span data-ttu-id="da103-287">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-287">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-288">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-288">**Allowed From**</span></span>

<span data-ttu-id="da103-289">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da103-289">Application code</span></span>

<span data-ttu-id="da103-290">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-290">**Example**</span></span>

```
/* Retrieve the DHCPv6 Server lease data. */
For (I = 0; I < NX_DHCPV6_MAX_LEASES; i++)
{
    /* Get the next lease record. */
    status = nx_dhcpv6_server_startdhcpv6_server_ptr, i, &next_ipv6_address, &T1,
             &T2, &preferred_lifetime, &valid_lifetime);
    /* The host application then saves this record to memory.
}
/* If status is NX_SUCCESS the Server data is successfully downloaded. */
```

## <a name="nx_dhcpv6_add_ip_address_lease"></a><span data-ttu-id="da103-291">nx_dhcpv6_add_ip_address_lease</span><span class="sxs-lookup"><span data-stu-id="da103-291">nx_dhcpv6_add_ip_address_lease</span></span>

### <a name="add-an-ip-address-lease-to-the-server-table"></a><span data-ttu-id="da103-292">Aggiungere un lease di indirizzi IP alla tabella del server</span><span class="sxs-lookup"><span data-stu-id="da103-292">Add an IP address lease to the Server table</span></span>

<span data-ttu-id="da103-293">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-293">**Prototype**</span></span>

```
UINT _nx_dhcpv6_add_ip_address_lease(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, UINT table_index, NXD_ADDRESS *lease_IP_address, ULONG T1, ULONG T2, 
     ULONG valid_lifetime, ULONG preferred_lifetime)
```

<span data-ttu-id="da103-294">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-294">**Description**</span></span>

<span data-ttu-id="da103-295">Questo servizio carica i dati di lease IP da una sessione del server DHCPv6 precedente dalla memoria non volatile alla tabella dei lease del server.</span><span class="sxs-lookup"><span data-stu-id="da103-295">This service loads IP lease data from a previous DHCPv6 Server session from non volatile memory to the Server lease table.</span></span> <span data-ttu-id="da103-296">Questa operazione non è necessaria se il server viene eseguito per la prima volta e non ha dati di lease precedenti.</span><span class="sxs-lookup"><span data-stu-id="da103-296">This is not necessary if the Server is running for the first time and has no previous lease data.</span></span> <span data-ttu-id="da103-297">In tal caso, l'applicazione host deve creare un intervallo di indirizzi IP per l'assegnazione di indirizzi IP, usando il servizio *nx_dhcpv6_create_ip_address_range*.</span><span class="sxs-lookup"><span data-stu-id="da103-297">If this is the case the host application must create an IP address range for assigning IP addresses, using the *nx_dhcpv6_create_ip_address_range* service.</span></span> <span data-ttu-id="da103-298">I dati sono sufficienti per ricostruire un record di lease DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-298">The data is sufficient to reconstruct a DHCPv6 lease record.</span></span> <span data-ttu-id="da103-299">Non è necessario specificare l'indice della tabella.</span><span class="sxs-lookup"><span data-stu-id="da103-299">The table index need not be specified.</span></span> <span data-ttu-id="da103-300">Se impostato su 0xFFFFFFFF (Infinity), il server DHCPv6 troverà il successivo slot disponibile in cui copiare i dati.</span><span class="sxs-lookup"><span data-stu-id="da103-300">If set to 0xFFFFFFFF (infinity) the DHCPv6 Server will find the next available slot to copy the data to.</span></span>

>[!NOTE] 
> <span data-ttu-id="da103-301">Il caricamento dei dati di lease IP deve essere eseguito prima di caricare i record client; è necessario eseguire entrambe le operazioni prima di avviare (re) il server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-301">Uploading IP lease data MUST be done before uploading Client records; both MUST be done before (re)starting the DHCPv6 Server.</span></span>

<span data-ttu-id="da103-302">La capacità di archiviare e recuperare i dati tra il server DHCPv6 e la memoria non volatile è un requisito del protocollo DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-302">The capability of storing and retrieving data between the DHCPv6 Server and non volatile memory is a requirement of the DHCPv6 protocol.</span></span>

<span data-ttu-id="da103-303">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-303">**Input Parameters**</span></span>

- <span data-ttu-id="da103-304">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-304">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-305">**table_index** Indice tabella in cui archiviare il lease</span><span class="sxs-lookup"><span data-stu-id="da103-305">**table_index** Table index to store lease at</span></span>
- <span data-ttu-id="da103-306">**lease_IP_address** Puntatore a indirizzo IP con lease per il client</span><span class="sxs-lookup"><span data-stu-id="da103-306">**lease_IP_address** Pointer to IP address leased to the Client</span></span>
- <span data-ttu-id="da103-307">**T1** Tempo di rinnovo richiesto dal client</span><span class="sxs-lookup"><span data-stu-id="da103-307">**T1** Client requested renew time</span></span>
- <span data-ttu-id="da103-308">**T2** Tempo di riassociazione richiesto dal client</span><span class="sxs-lookup"><span data-stu-id="da103-308">**T2** Client requested rebind time</span></span>
- <span data-ttu-id="da103-309">**valid_lifetime** Il lease client diventa deprecato</span><span class="sxs-lookup"><span data-stu-id="da103-309">**valid_lifetime** Client lease becomes deprecated</span></span>
- <span data-ttu-id="da103-310">**preferred_lifetime** Lease client non valido</span><span class="sxs-lookup"><span data-stu-id="da103-310">**preferred_lifetime** Client lease becomes invalid</span></span>

<span data-ttu-id="da103-311">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-311">**Return Values**</span></span>

- <span data-ttu-id="da103-312">Server **NX_SUCCESS** (0x00) avviato correttamente</span><span class="sxs-lookup"><span data-stu-id="da103-312">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="da103-313">**NX_DHCPV6_TABLE_FULL** (0XEC4) senza spazio per altri dati di lease \* \*</span><span class="sxs-lookup"><span data-stu-id="da103-313">**NX_DHCPV6_TABLE_FULL** (0xEC4) No room for more lease data\*\*</span></span>
- <span data-ttu-id="da103-314">I dati di lease **NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) non sembrano trovarsi sul collegamento con l'interfaccia DHCPV6 del server</span><span class="sxs-lookup"><span data-stu-id="da103-314">**NX_DHCPV6_INVALID_INTERFACE_IP_ADDRESS** (0xE95) Lease data does not appear to be on link with Server DHCPv6 interface</span></span>
- <span data-ttu-id="da103-315">Input di dati di lease IP di **NX_DHCPV6_PARAM_ERROR** (0XE93) non valido</span><span class="sxs-lookup"><span data-stu-id="da103-315">**NX_DHCPV6_PARAM_ERROR** (0xE93) Invalid IP lease data input</span></span>
- <span data-ttu-id="da103-316">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-316">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-317">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-317">**Allowed From**</span></span>

<span data-ttu-id="da103-318">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da103-318">Application code</span></span>

<span data-ttu-id="da103-319">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-319">**Example**</span></span>

```
/* Copy the IP lease data to the Server address table. Note that the table index
is defaulted to 0xFFFFFFFF meaning the DHCPv6 Server will find an empty slot 
for each lease. */

    For(I = 0; I < NX_DHCPV6_MAX_LEASES; i++)
    {
        status = nx_dhcpv6_add_ip_address_lease(dhcpv6_server_ptr, 0xFFFFFFFF,
                 &next_ipv6_address, &T1, &T2, &preferred_lifetime, &valid_lifetime);
        /* Get the next lease address from memory… */
    }
    
    /* If status is NX_SUCCESS the lease data was successfully uploaded. It is opk
    to add the Client records to the Server table now. */
```

## <a name="nx_dhcpv6_add_client_record"></a><span data-ttu-id="da103-320">nx_dhcpv6_add_client_record</span><span class="sxs-lookup"><span data-stu-id="da103-320">nx_dhcpv6_add_client_record</span></span>

### <a name="add-a-client-record-to-the-server-table"></a><span data-ttu-id="da103-321">Aggiungere un record client alla tabella del server</span><span class="sxs-lookup"><span data-stu-id="da103-321">Add a Client record to the Server table</span></span>

<span data-ttu-id="da103-322">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-322">**Prototype**</span></span>

```
UINT _nx_dhcpv6_add_client_record(NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT table_index, ULONG message_xid, 
     NXD_ADDRESS *client_address, UINT client_state, 
     ULONG IP_lease_time_accrued, ULONG valid_lifetime, UINT duid_type, UINTduid_hardware, 
     ULONG physical_address_msw, ULONG physical_address_lsw, ULONG duid_time, 
     ULONG duid_vendor_number, UCHAR *duid_vendor_private, UINT duid_private_length)
```

<span data-ttu-id="da103-323">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-323">**Description**</span></span>

<span data-ttu-id="da103-324">Questo servizio copia i dati client dalla memoria non volatile alla tabella del server un record alla volta.</span><span class="sxs-lookup"><span data-stu-id="da103-324">This service copies Client data from non volatile memory to the Server table one record at a time.</span></span> <span data-ttu-id="da103-325">Questa operazione è necessaria solo se il server viene riavviato e contiene i dati client di una sessione precedente per il ripristino dalla memoria.</span><span class="sxs-lookup"><span data-stu-id="da103-325">This is only necessary if the Server is being rebooted and has Client data from a previous session to restore from memory.</span></span> <span data-ttu-id="da103-326">Se un server non ha dati precedenti, il server DHCPv6 Inizializza la tabella client in modo da poter aggiungere i record client.</span><span class="sxs-lookup"><span data-stu-id="da103-326">If a Server has no previous data, the DHCPv6 Server will initialize the Client table to be able for adding Client records.</span></span>

<span data-ttu-id="da103-327">Non è necessario specificare l'indice della tabella.</span><span class="sxs-lookup"><span data-stu-id="da103-327">It is not necessary to specify the table index.</span></span> <span data-ttu-id="da103-328">Se impostato su 0xFFFFFFFF (Infinity), il server DHCPv6 troverà lo slot successivo disponibile.</span><span class="sxs-lookup"><span data-stu-id="da103-328">If set to 0xFFFFFFFF (infinity) the DHCPv6 Server will locate the next available slot.</span></span> <span data-ttu-id="da103-329">Il server DHCPv6 può ricostruire un record client da questi dati.</span><span class="sxs-lookup"><span data-stu-id="da103-329">The DHCPv6 Server can reconstruct a Client record from this data.</span></span>

>[!NOTE] 
> <span data-ttu-id="da103-330">L'applicazione host deve caricare i dati di lease IP prima che i dati del record client.</span><span class="sxs-lookup"><span data-stu-id="da103-330">The host application MUST upload the IP lease data BEFORE the Client record data.</span></span> <span data-ttu-id="da103-331">In questo modo, internamente il server DHCPv6 può collegare le tabelle in modo che ogni record client venga unito al record di lease IP corrispondente nelle rispettive tabelle.</span><span class="sxs-lookup"><span data-stu-id="da103-331">This is so that internally the DHCPv6 Server can cross link the tables so that each Client record is joined with its corresponding IP lease record in their respective tables.</span></span> <span data-ttu-id="da103-332">Per informazioni dettagliate sul caricamento dei dati di lease IP dalla memoria, vedere *nx_dhcpv6_add_ip_address_lease* .</span><span class="sxs-lookup"><span data-stu-id="da103-332">See *nx_dhcpv6_add_ip_address_lease* for details on uploading IP lease data from memory.</span></span>

>[!NOTE] 
> <span data-ttu-id="da103-333">A seconda del tipo DUID, non è necessario specificare tutti i dati.</span><span class="sxs-lookup"><span data-stu-id="da103-333">Depending on DUID type, not all data must be supplied.</span></span> <span data-ttu-id="da103-334">Se ad esempio un client dispone di un tipo DUID assegnato dal fornitore, può inviare zero per i parametri del livello di collegamento DUID (indirizzo MAC, tipo di hardware, ora DUID).</span><span class="sxs-lookup"><span data-stu-id="da103-334">For example if a Client has a vendor assigned DUID type, it can send in zero for DUID Link Layer parameters (MAC address, hardware type, DUID time).</span></span>

<span data-ttu-id="da103-335">La capacità di archiviare e recuperare i dati tra il server DHCPv6 e la memoria non volatile è un requisito del protocollo DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-335">The capability of storing and retrieving data between the DHCPv6 Server and non volatile memory is a requirement of the DHCPv6 protocol.</span></span>

<span data-ttu-id="da103-336">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-336">**Input Parameters**</span></span>

- <span data-ttu-id="da103-337">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-337">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="da103-338">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-338">**Return Values**</span></span>

- <span data-ttu-id="da103-339">Server **NX_SUCCESS** (0x00) avviato correttamente</span><span class="sxs-lookup"><span data-stu-id="da103-339">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="da103-340">**NX_ INVALID_PARAMETERS** (irreversibile 0x4D) non è stato inserito un puntatore non valido \* \*</span><span class="sxs-lookup"><span data-stu-id="da103-340">**NX_ INVALID_PARAMETERS** (0x4D) Invalid non pointer input\*\*</span></span>
- <span data-ttu-id="da103-341">**NX_DHCPV6_TABLE_FULL** (0XEC4) non sono stati lasciati slot vuoti per l'aggiunta di un altro record client</span><span class="sxs-lookup"><span data-stu-id="da103-341">**NX_DHCPV6_TABLE_FULL** (0xEC4) No empty slots left for adding another Client record</span></span>
- <span data-ttu-id="da103-342">Impossibile trovare l'indirizzo assegnato del client **NX_DHCPV6_ADDRESS_NOT_FOUND** (0xEA8) nella tabella di lease del server.</span><span class="sxs-lookup"><span data-stu-id="da103-342">**NX_DHCPV6_ADDRESS_NOT_FOUND** (0xEA8) Client assigned address not found in Server lease table.</span></span>
- <span data-ttu-id="da103-343">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-343">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-344">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-344">**Allowed From**</span></span>

<span data-ttu-id="da103-345">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da103-345">Application code</span></span>

<span data-ttu-id="da103-346">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-346">**Example**</span></span>

```
/*Add the IP lease data and Client records back to the server before starting
theServer. */
    /* Copy the 'lease data' to the server table FIRST. */
for (i = 0; i< NX_DHCPV6_MAX_LEASES; i++)
    {

        /* Add the next lease record. Let the server find the next
        available slot. */
        status = nx_dhcpv6_add_ip_address_lease(dhcpv6_server_ptr,
                 0xFFFFFFFF,,&next_ipv6_address, NX_DHCPV6_DEFAULT_T1_TIME, 
                 NX_DHCPV6_DEFAULT_T2_TIME, NX_DHCPV6_DEFAULT_PREFERRED_TIME, 
                 NX_DHCPV6_DEFAULT_VALID_TIME);
if (status != NX_SUCCESS)
return status;
        /* Get the next IP lease record from memory. */
        …
    }
    /* Copy the client records to the Server table NEXT.
    for (i = 0; i< NX_DHCPV6_MAX_LEASES; i++)
    {
        /* Add the next client record. Let the server find the next
        available slot. */
        status = nx_dhcpv6_add_client_record(dhcpv6_server_ptr, 0xFFFFFFFF,
                 message_xid, &client_ipv6_address, NX_DHCPV6_STATE_BOUND,
                 IP_lifetime_time_accrued, valid_lifetime, duid_type, 
                 duid_hardware, physical_address_msw, physical_address_lsw, 
                 duid_time, 0, NX_NULL, 0);
if (status != NX_SUCCESS)
return status;
        /* Get the next Client record from memory. */
        …
    }

/* If status is NX_SUCCESS the Server data was successfully restored and 
it is ok to start the DHCPv6 server now. */
```

## <a name="nx_dhcpv6_retrieve_client_record"></a><span data-ttu-id="da103-347">nx_dhcpv6_retrieve_client_record</span><span class="sxs-lookup"><span data-stu-id="da103-347">nx_dhcpv6_retrieve_client_record</span></span>

### <a name="retrieve-a-client-record-from-the-server-table"></a><span data-ttu-id="da103-348">Recuperare un record client dalla tabella server</span><span class="sxs-lookup"><span data-stu-id="da103-348">Retrieve a Client record from the Server table</span></span>

<span data-ttu-id="da103-349">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-349">**Prototype**</span></span>

```
UINT _nx_dhcpv6_retrieve_client_record(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT table_index, ULONG *message_xid, 
     NXD_ADDRESS *client_address, UINT *client_state, 
     ULONG IP_lease_time_accrued, 
     ULONG *valid_lifetime, UINT *duid_type, 
     UINT *duid_hardware, ULONG *physical_address_msw, 
     ULONG *physical_address_lsw, ULONG *duid_time, 
     ULONG *duid_vendor_number, 
     UCHAR *duid_vendor_private, 
     UINT *duid_private_length)
```

<span data-ttu-id="da103-350">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-350">**Description**</span></span>

<span data-ttu-id="da103-351">Questo servizio copia i dati essenziali dalla tabella dei record client del server per l'archiviazione in memoria non volatile.</span><span class="sxs-lookup"><span data-stu-id="da103-351">This service copies the essential data from the Server’s Client record table for storage to non-volatile memory.</span></span> <span data-ttu-id="da103-352">Il server può ricostruire un record client adeguato da tali dati nel processo inverso (caricando i dati nella tabella server).</span><span class="sxs-lookup"><span data-stu-id="da103-352">The Server can reconstruct an adequate Client record from such data in the reverse process (uploading data to the Server table).</span></span> <span data-ttu-id="da103-353">Indipendentemente dal tipo DUID, nessuno dei puntatori può essere puntatori NULL; i dati vengono inizializzati su zero per tutti i parametri.</span><span class="sxs-lookup"><span data-stu-id="da103-353">Regardless of the DUID type, none of the pointers can be NULL pointers; data is initialized to zero for all parameters.</span></span> <span data-ttu-id="da103-354">Se, ad esempio, il tipo di DUID client è link layer Plus Time, il numero del fornitore viene restituito come zero e l'ID privato è una stringa vuota.</span><span class="sxs-lookup"><span data-stu-id="da103-354">For example, if the Client DUID type is Link Layer Plus Time, the vendor number is returned as zero and the private ID is an empty string.</span></span>

<span data-ttu-id="da103-355">La capacità di archiviare e recuperare i dati tra il server DHCPv6 e la memoria non volatile è un requisito del protocollo DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-355">The capability of storing and retrieving data between the DHCPv6 Server and non volatile memory is a requirement of the DHCPv6 protocol.</span></span> <span data-ttu-id="da103-356">Non fa alcuna differenza per quanto riguarda l'ordine in cui i dati di lease IP e i dati dei record client vengono salvati nella memoria non volatile.</span><span class="sxs-lookup"><span data-stu-id="da103-356">It makes no difference in what order IP lease data and Client record data is saved to nonvolatile memory.</span></span>

>[!NOTE] 
> <span data-ttu-id="da103-357">Non è consigliabile copiare dati in o da tabelle server senza arrestare o sospendere prima il server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-357">It is not recommended to copy data to or from Server tables without stopping or suspending the DHCPv6 Server first.</span></span>

<span data-ttu-id="da103-358">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-358">**Input Parameters**</span></span>

- <span data-ttu-id="da103-359">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-359">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-360">**table_index** Indice nella tabella client del server</span><span class="sxs-lookup"><span data-stu-id="da103-360">**table_index** Index into Server’s client table</span></span>
- <span data-ttu-id="da103-361">**message_xid** ID transazione server client</span><span class="sxs-lookup"><span data-stu-id="da103-361">**message_xid** Client Server Transaction ID</span></span>
- <span data-ttu-id="da103-362">**CLIENT_ADDRESS** Indirizzo IPv6 concesso in lease al client</span><span class="sxs-lookup"><span data-stu-id="da103-362">**client_address** IPv6 address leased to Client</span></span>
- <span data-ttu-id="da103-363">**client_state** Stato DHCPv6 client (ad esempio associato)</span><span class="sxs-lookup"><span data-stu-id="da103-363">**client_state** Client DHCPv6 state (e.g. bound)</span></span>
- <span data-ttu-id="da103-364">**IP_lease_time_accrued** L'ora di scadenza del lease è già **dhcpv6_server_ptr** puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-364">**IP_lease_time_accrued** Time expired on lease already **dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-365">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-365">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>

<span data-ttu-id="da103-366">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-366">**Return Values**</span></span>

- <span data-ttu-id="da103-367">Server **NX_SUCCESS** (0x00) avviato correttamente</span><span class="sxs-lookup"><span data-stu-id="da103-367">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="da103-368">**NX_DHCPV6_INVALID_DUID** (0xECC) dati Duid non validi o incoerenti</span><span class="sxs-lookup"><span data-stu-id="da103-368">**NX_DHCPV6_INVALID_DUID** (0xECC) Invalid or inconsistent DUID data</span></span>
- <span data-ttu-id="da103-369">**NX_PTR_ERROR** (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-369">**NX_PTR_ERROR** (0x16) Invalid pointer input</span></span>
- <span data-ttu-id="da103-370">NX_INVALID_PARAMETERS (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-370">NX_INVALID_PARAMETERS (0x4D) Invalid non pointer input</span></span>

<span data-ttu-id="da103-371">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-371">**Allowed From**</span></span>

<span data-ttu-id="da103-372">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da103-372">Application code</span></span>

<span data-ttu-id="da103-373">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-373">**Example**</span></span>

```
/* Retrieve the Client records from the DHCPv6 Server table. */
For (i = 0; i< NX_MAX_DHCPV6_CLIENTS; i++)
{
    status = nx_dhcpv6_retrieve_client_recorddhcpv6_server_ptr, i, &message_xid,
             &client_ipv6_address, &client_state, &IP_lifetime_time_accrued, 
             valid_lifetime, &duid_type, &duid_hardware, &physical_address_msw,
             &physical_address_lsw, &duid_time, &duid_vendor_number, &private_id[0], 
             &length);
    /* The host application can save this data to memory now.
}
/* If status is NX_SUCCESS the Server successfully started. */
```

## <a name="nx_dhcpv6_server_interface_set"></a><span data-ttu-id="da103-374">nx_dhcpv6_server_interface_set</span><span class="sxs-lookup"><span data-stu-id="da103-374">nx_dhcpv6_server_interface_set</span></span>

### <a name="setthe-interface-index-for-server-dhcpv6-interface"></a><span data-ttu-id="da103-375">SetThe Interface index per server DHCPv6 Interface</span><span class="sxs-lookup"><span data-stu-id="da103-375">Setthe interface index for Server DHCPv6 interface</span></span>

<span data-ttu-id="da103-376">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-376">**Prototype**</span></span>

```
UINT _nx_dhcpv6_server_interface_set(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     UINT iface_index, UINT ga_address_index)
```

<span data-ttu-id="da103-377">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-377">**Description**</span></span>

<span data-ttu-id="da103-378">Questo servizio imposta l'interfaccia di rete su cui il server DHCPv6 gestisce le richieste del client DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-378">This service sets the network interface on which the DHCPv6 Server handles DHCPv6 Client requests.</span></span> <span data-ttu-id="da103-379">Non per le versioni di NetX duo che non supportano la multihome, il valore dell'interfaccia viene impostato su zero.</span><span class="sxs-lookup"><span data-stu-id="da103-379">Not that for versions of NetX Duo that do not support multihome, the interface value is defaulted to zero.</span></span> <span data-ttu-id="da103-380">L'indice globale degli indirizzi è necessario per ottenere l'indirizzo globale del server sull'interfaccia DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-380">The global address index is necessary to obtain the Server global address on its DHCPv6 interface.</span></span> <span data-ttu-id="da103-381">Viene usato dalla logica DHCPv6 per assicurarsi che gli indirizzi di lease e altri dati DHCPv6 siano collegati al server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-381">This is used by the DHCPv6 logic to ensure that lease addresses and other DHCPv6 data is on link with the DHCPv6 Server.</span></span>

<span data-ttu-id="da103-382">Questo metodo deve essere chiamato prima che il server DHCPv6 venga avviato, anche per le applicazioni in dispositivi singoli o senza supporto multihome.</span><span class="sxs-lookup"><span data-stu-id="da103-382">This must be called before the DHCPv6 server is started, even for applications on single homed devices or without multihome support.</span></span>

<span data-ttu-id="da103-383">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-383">**Input Parameters**</span></span>

- <span data-ttu-id="da103-384">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-384">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-385">**iface_index** Interfaccia server DHCPv6 server</span><span class="sxs-lookup"><span data-stu-id="da103-385">**iface_index** Server DHCPv6 Server interface</span></span>
- <span data-ttu-id="da103-386">**ga_address_index** Indice dell'indirizzo globale del server nella tabella degli indirizzi dell'istanza IP del server</span><span class="sxs-lookup"><span data-stu-id="da103-386">**ga_address_index** Index of Server global address in the Server IP instance address table</span></span>

<span data-ttu-id="da103-387">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-387">**Return Values**</span></span>

- <span data-ttu-id="da103-388">Server **NX_SUCCESS** (0x00) avviato correttamente</span><span class="sxs-lookup"><span data-stu-id="da103-388">**NX_SUCCESS** (0x00) Server successfully started</span></span>
- <span data-ttu-id="da103-389">L'interfaccia **NX_INVALID_INTERFACE** (0x4C) non esiste</span><span class="sxs-lookup"><span data-stu-id="da103-389">**NX_INVALID_INTERFACE** (0x4C) Interface does not exist</span></span>
- <span data-ttu-id="da103-390">NX_NO_INTERFACE_ADDRESS indice globale (0x50) supera il numero massimo di indirizzi IPv6 per l'istanza IP (NX_MAX_IPV6_ADDRESSES)</span><span class="sxs-lookup"><span data-stu-id="da103-390">NX_NO_INTERFACE_ADDRESS (0x50) Global index exceeds the IP instance maximum IPv6 addresses (NX_MAX_IPV6_ADDRESSES)</span></span>
- <span data-ttu-id="da103-391">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-391">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-392">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-392">**Allowed From**</span></span>

<span data-ttu-id="da103-393">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da103-393">Application code</span></span>

<span data-ttu-id="da103-394">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-394">**Example**</span></span>

```
/* Set the Server DHCPv6 interface to the primary interface. The global IP 
address is at the index 1 in the IP address table. */
status = nx_dhcpv6_server_interface_set(&dhcp_server_0, 0, 1);

/* If status is NX_SUCCESS the Server interface is successfully set. */
```
## <a name="nx_dhcpv6_set_server_duid"></a><span data-ttu-id="da103-395">nx_dhcpv6_set_server_duid</span><span class="sxs-lookup"><span data-stu-id="da103-395">nx_dhcpv6_set_server_duid</span></span>

### <a name="set-the-server-duid-for-dhcpv6-packets"></a><span data-ttu-id="da103-396">Impostare il server DUID per i pacchetti DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-396">Set the Server DUID for DHCPv6 packets</span></span>

<span data-ttu-id="da103-397">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-397">**Prototype**</span></span>

```
UINT _nx_dhcpv6_set_server_duid(NX_DHCPV6_SERVER *dhcpv6_server_ptr,
     UINT duid_type, UINT hardware_type, 
     ULONG mac_address_msw, ULONG mac_address_lsw, 
     ULONG time)
```

<span data-ttu-id="da103-398">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-398">**Description**</span></span>

<span data-ttu-id="da103-399">Questo servizio imposta il server DUID e deve essere chiamato prima che l'applicazione host avvii il server.</span><span class="sxs-lookup"><span data-stu-id="da103-399">This service sets the Server DUID and must be called before the host application starts the Server.</span></span> <span data-ttu-id="da103-400">Per i tipi di DUID a livello di collegamento e di collegamento ora, l'applicazione host deve fornire i dati di tipo hardware e indirizzo MAC.</span><span class="sxs-lookup"><span data-stu-id="da103-400">For link layer and link layer time DUID types, the host application must supply the hardware type and MAC address data.</span></span> <span data-ttu-id="da103-401">Per l'ora del livello di collegamento Duid, il puntatore all'ora deve puntare a un momento valido.</span><span class="sxs-lookup"><span data-stu-id="da103-401">For link layer time DUIDs, the time pointer must point to a valid time.</span></span> <span data-ttu-id="da103-402">Il numero di secondi trascorsi dal 1 ° gennaio 2000 è un valore di inizializzazione tipico.</span><span class="sxs-lookup"><span data-stu-id="da103-402">The number of seconds since Jan 1, 2000 is a typical seed value.</span></span> <span data-ttu-id="da103-403">Se il tipo di DUID del server è Enterprise, fornitore assegnato, il DUID verrà creato dalle opzioni configurabili dall'utente NX_DHCPV6_SERVER_DUID_VENDOR_PRIVATE_ID e NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_ID e i valori dell'ora e degli indirizzi MAC possono essere impostati su NULL.</span><span class="sxs-lookup"><span data-stu-id="da103-403">If the Server DUID type is the enterprise, vendor assigned type, the DUID will be created from the user configurable options NX_DHCPV6_SERVER_DUID_VENDOR_PRIVATE_ID and NX_DHCPV6_SERVER_DUID_VENDOR_ASSIGNED_ID, and the time and MAC address values can be set to NULL.</span></span>

>[!NOTE] 
> <span data-ttu-id="da103-404">È responsabilità dell'applicazione host salvare i parametri del server DUID nella memoria non volatile in modo che usi lo stesso DUID nei messaggi ai client tra i riavvii.</span><span class="sxs-lookup"><span data-stu-id="da103-404">It is the host application’s responsibility to save the Server DUID parameters to nonvolatile memory such that it uses the same DUID in messages to Clients between reboots.</span></span> <span data-ttu-id="da103-405">Si tratta di un requisito del protocollo DHCPv6 (RFC 3315).</span><span class="sxs-lookup"><span data-stu-id="da103-405">This is a requirement of the DHCPv6 protocol (RFC 3315).</span></span>

<span data-ttu-id="da103-406">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-406">**Input Parameters**</span></span>

- <span data-ttu-id="da103-407">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-407">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-408">**duid_type** Tipo DUID del server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-408">**duid_type** DHCPv6 Server DUID type</span></span>
- <span data-ttu-id="da103-409">**hardware_type** Tipo di hardware (ad esempio, Ethernet)</span><span class="sxs-lookup"><span data-stu-id="da103-409">**hardware_type** Hardware type (e.g. Ethernet)</span></span>
- <span data-ttu-id="da103-410">**mac_address_msw** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-410">**mac_address_msw** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-411">**mac_address_lsw** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-411">**mac_address_lsw** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-412">**ora** di Valore di ora per DUID</span><span class="sxs-lookup"><span data-stu-id="da103-412">**time** Time value for DUID</span></span>

<span data-ttu-id="da103-413">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-413">**Return Values**</span></span>

- <span data-ttu-id="da103-414">Il server **NX_SUCCESS** (0x00) è stato sospeso</span><span class="sxs-lookup"><span data-stu-id="da103-414">**NX_SUCCESS** (0x00) Server successfully suspended</span></span>
- <span data-ttu-id="da103-415">**NX_DHCPV6_INVALID_SERVER_DUID** (0XE98) tipo Duid sconosciuto o non supportato</span><span class="sxs-lookup"><span data-stu-id="da103-415">**NX_DHCPV6_INVALID_SERVER_DUID** (0XE98) Unknown or unsupported DUID type</span></span>
- <span data-ttu-id="da103-416">**NX_INVALID_PARAMETERS** (irreversibile 0x4D) non è stato inserito alcun puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-416">**NX_INVALID_PARAMETERS** (0x4D) Invalid non pointer input</span></span>
- <span data-ttu-id="da103-417">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-417">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-418">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-418">**Allowed From**</span></span>

<span data-ttu-id="da103-419">Codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da103-419">Application code</span></span>

<span data-ttu-id="da103-420">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-420">**Example**</span></span>

```
/* Set the DHCPv6 ServerDUID as Link layer plus time, over Ethernet hardware. */
duid_time = SECONDS_SINCE_JAN_1_2000_MOD_32 + rand();

status = nx_dhcpv6_set_server_duid(&dhcp_server_0,1, 0x6,
         physical_address_msw,physical_address_lsw,duid_time);

/* If status is NX_SUCCESS the ServerDUID is successfully set. */
```

## <a name="nx_dhcpv6_server_option_request_handler_set"></a><span data-ttu-id="da103-421">nx_dhcpv6_server_option_request_handler_set</span><span class="sxs-lookup"><span data-stu-id="da103-421">nx_dhcpv6_server_option_request_handler_set</span></span>

### <a name="set-the-option-request-handler-for-dhcpv6-server-instance"></a><span data-ttu-id="da103-422">Impostare il gestore della richiesta di opzione per l'istanza del server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-422">Set the option request handler for DHCPv6 Server instance</span></span> 

<span data-ttu-id="da103-423">**Prototipo**</span><span class="sxs-lookup"><span data-stu-id="da103-423">**Prototype**</span></span>

```
UINT nx_dhcpv6_server_option_request_handler_set(
     NX_DHCPV6_SERVER *dhcpv6_server_ptr, 
     VOID (*dhcpv6_option_request_handler_extended)(
          struct NX_DHCPV6_SERVER_STRUCT *dhcpv6_server_ptr, 
          UINT option_request, UCHAR *buffer_ptr, 
          UINT *index, UINT available_payload));
```

<span data-ttu-id="da103-424">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="da103-424">**Description**</span></span>

<span data-ttu-id="da103-425">Questo servizio imposta il gestore di richieste di opzioni estese del server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="da103-425">This service sets the DHCPv6 Server extended option request handler.</span></span>

<span data-ttu-id="da103-426">**Parametri di input**</span><span class="sxs-lookup"><span data-stu-id="da103-426">**Input Parameters**</span></span>

- <span data-ttu-id="da103-427">**dhcpv6_server_ptr** Puntatore al server DHCPv6</span><span class="sxs-lookup"><span data-stu-id="da103-427">**dhcpv6_server_ptr** Pointer to DHCPv6 Server</span></span>
- <span data-ttu-id="da103-428">**dhcpv6_option_request_handler_extended** Puntatore al gestore di richieste di opzioni estese</span><span class="sxs-lookup"><span data-stu-id="da103-428">**dhcpv6_option_request_handler_extended** Pointer to extended options request handler</span></span>

<span data-ttu-id="da103-429">**Valori restituiti**</span><span class="sxs-lookup"><span data-stu-id="da103-429">**Return Values**</span></span>

- <span data-ttu-id="da103-430">Riattivazione del server **NX_SUCCESS** (0x00) completata</span><span class="sxs-lookup"><span data-stu-id="da103-430">**NX_SUCCESS** (0x00) Server successfully resumed</span></span>
- <span data-ttu-id="da103-431">NX_PTR_ERROR (0x16) input puntatore non valido</span><span class="sxs-lookup"><span data-stu-id="da103-431">NX_PTR_ERROR (0x16) Invalid pointer input</span></span>

<span data-ttu-id="da103-432">**Consentito da**</span><span class="sxs-lookup"><span data-stu-id="da103-432">**Allowed From**</span></span>

<span data-ttu-id="da103-433">codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="da103-433">Application Code</span></span>

<span data-ttu-id="da103-434">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="da103-434">**Example**</span></span>

```
/* Set the option request handler for DHCPv6 Server. */
status = nx_dhcpv6_server_option_request_handler_set(&dhcp_server_0,
         dhcpv6_option_request_handler_extended);

/* If status is NX_SUCCESS the extended handler successfully set. */
```