---
title: Capitolo 2-installazione e uso del server DHCP NetX di Azure RTO
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente server DHCP NetX di Azure RTO.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 034a4d74c566fbfe94981a42b7e06e7f2ee79d25
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822694"
---
# <a name="chapter-2---installation-and-use-of-the-azure-rtos-netx-dhcp-server"></a><span data-ttu-id="bc66a-103">Capitolo 2-installazione e uso del server DHCP NetX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="bc66a-103">Chapter 2 - Installation and use of the Azure RTOS NetX DHCP Server</span></span>

<span data-ttu-id="bc66a-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente DHCP NetX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="bc66a-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX DHCP component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="bc66a-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="bc66a-105">Product Distribution</span></span>

<span data-ttu-id="bc66a-106">Il server DHCP NetX di Azure RTO può essere ottenuto dal repository del codice sorgente pubblico all'indirizzo [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/) .</span><span class="sxs-lookup"><span data-stu-id="bc66a-106">Azure RTOS NetX DHCP Server can be obtained from our public source code repository at [https://github.com/azure-rtos/netx/](https://github.com/azure-rtos/netx/).</span></span> <span data-ttu-id="bc66a-107">Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="bc66a-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="bc66a-108">**nx_dhcp_server. h**: file di intestazione per il server DHCP NETX</span><span class="sxs-lookup"><span data-stu-id="bc66a-108">**nx_dhcp_server.h**: Header file for NetX DHCP Server</span></span>
- <span data-ttu-id="bc66a-109">**nx_dhcp_server. c**: file di origine c per il server DHCP NETX</span><span class="sxs-lookup"><span data-stu-id="bc66a-109">**nx_dhcp_server.c**: C Source file for NetX DHCP Server</span></span>
- <span data-ttu-id="bc66a-110">**nx_dhcp_server.pdf**: Descrizione PDF del server DHCP NETX</span><span class="sxs-lookup"><span data-stu-id="bc66a-110">**nx_dhcp_server.pdf**: PDF description of NetX DHCP Server</span></span>
- <span data-ttu-id="bc66a-111">**demo_netx_dhcp_server. c**: NETX server DHCP demo</span><span class="sxs-lookup"><span data-stu-id="bc66a-111">**demo_netx_dhcp_server.c**: NetX DHCP Server demonstration</span></span>

## <a name="dhcp-installation"></a><span data-ttu-id="bc66a-112">Installazione DHCP</span><span class="sxs-lookup"><span data-stu-id="bc66a-112">DHCP Installation</span></span>

<span data-ttu-id="bc66a-113">Per usare il server DHCP NetX, l'intera distribuzione indicata in precedenza deve essere copiata nella stessa directory in cui è installato NetX.</span><span class="sxs-lookup"><span data-stu-id="bc66a-113">In order to use NetX DHCP Server, the entire distribution mentioned previously should be copied to the same directory where NetX is installed.</span></span> <span data-ttu-id="bc66a-114">Se, ad esempio, NetX è installato nella directory "*\threadx\arm7\green*", i file *nx_dhcp_server. h* e *nx_dhpc_server. c* devono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="bc66a-114">For example, if NetX is installed in the directory "*\threadx\arm7\green*" then the *nx_dhcp_server.h* and *nx_dhpc_server.c* files should be copied into this directory.</span></span>

## <a name="using-netx-dhcp-server"></a><span data-ttu-id="bc66a-115">Uso del server DHCP NetX</span><span class="sxs-lookup"><span data-stu-id="bc66a-115">Using NetX DHCP Server</span></span>

<span data-ttu-id="bc66a-116">L'uso del server DHCP NetX è facile.</span><span class="sxs-lookup"><span data-stu-id="bc66a-116">Using NetX DHCP Server is easy.</span></span> <span data-ttu-id="bc66a-117">In pratica, il codice dell'applicazione deve includere *nx_dhcp_server. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per poter utilizzare rispettivamente threadX e NETX.</span><span class="sxs-lookup"><span data-stu-id="bc66a-117">Basically, the application code must include *nx_dhcp_server.h* after it includes *tx_api.h* and *nx_api.h*, in order to use ThreadX and NetX, respectively.</span></span> <span data-ttu-id="bc66a-118">Una volta incluso *nx_dhcp_server. h* , il codice dell'applicazione è in grado di eseguire le chiamate di funzione DHCP specificate più avanti in questa guida.</span><span class="sxs-lookup"><span data-stu-id="bc66a-118">Once *nx_dhcp_server.h* is included, the application code is then able to make the DHCP function calls specified later in this guide.</span></span> <span data-ttu-id="bc66a-119">Nell'applicazione deve inoltre essere incluso *nx_dhcp_server. c* nel processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="bc66a-119">The application must also include *nx_dhcp_server.c* in the build process.</span></span> <span data-ttu-id="bc66a-120">Questo file deve essere compilato in modo analogo a quello di altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bc66a-120">This file must be compiled in the same manner as other application files and its object form must be linked along with the files of the application.</span></span> <span data-ttu-id="bc66a-121">Per ulteriori informazioni sull'utilizzo del server DHCP NetX, vedere le sezioni seguenti [requisiti del dhcpserver NETX](#requirements-of-the-netx-dhcp-server) e [vincoli del server DHCP NETX](#constraints-of-the-netx-dhcp-server).</span><span class="sxs-lookup"><span data-stu-id="bc66a-121">For more details on using NetX DHCP Server, see the following sections [Requirements of the NetX DHCPServer](#requirements-of-the-netx-dhcp-server) and [Constraints of the NetX DHCP Server](#constraints-of-the-netx-dhcp-server).</span></span>

> [!NOTE]
> <span data-ttu-id="bc66a-122">Poiché DHCP usa i servizi UDP NetX, è necessario abilitare UDP con la chiamata *nx_udp_enable* prima di usare DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-122">Since DHCP utilizes NetX UDP services, UDP must be enabled with the *nx_udp_enable* call prior to using DHCP.</span></span>

## <a name="requirements-of-the-netx-dhcp-server"></a><span data-ttu-id="bc66a-123">Requisiti del server DHCP NetX</span><span class="sxs-lookup"><span data-stu-id="bc66a-123">Requirements of the NetX DHCP Server</span></span>

<span data-ttu-id="bc66a-124">Il server DHCP NetX richiede una porta del socket UDP assegnata alla porta DHCP 67 ben nota.</span><span class="sxs-lookup"><span data-stu-id="bc66a-124">The NetX DHCP Server requires a UDP socket port assigned to the well known DHCP port 67.</span></span> <span data-ttu-id="bc66a-125">Per creare il server DHCP, l'applicazione deve creare un pool di pacchetti con payload di pacchetti di almeno 548 byte più le intestazioni IP, UDP e Ethernet (con un totale di 44 byte con allineamento a 4 byte).</span><span class="sxs-lookup"><span data-stu-id="bc66a-125">To create the DHCP Server, the application must create a packet pool with packet payload at least 548 bytes plus IP, UDP and Ethernet headers (which total 44 bytes with 4 byte alignment).</span></span>

<span data-ttu-id="bc66a-126">Si presuppone che il server e il client utilizzino entrambe le impostazioni degli indirizzi hardware Ethernet:</span><span class="sxs-lookup"><span data-stu-id="bc66a-126">It is assumed that the Server and Client are both using Ethernet hardware address settings:</span></span>

- <span data-ttu-id="bc66a-127">**Tipo di hardware**: 1</span><span class="sxs-lookup"><span data-stu-id="bc66a-127">**Hardware type**: 1</span></span>
- <span data-ttu-id="bc66a-128">**Lunghezza hardware**: 6</span><span class="sxs-lookup"><span data-stu-id="bc66a-128">**Hardware length**: 6</span></span>
- <span data-ttu-id="bc66a-129">**Hop**: 0</span><span class="sxs-lookup"><span data-stu-id="bc66a-129">**Hops**: 0</span></span>

### <a name="multiple-client-sessions"></a><span data-ttu-id="bc66a-130">Più sessioni client</span><span class="sxs-lookup"><span data-stu-id="bc66a-130">Multiple Client Sessions</span></span>

<span data-ttu-id="bc66a-131">Il server DHCP di NetX è in grado di gestire più sessioni client mantenendo una tabella dei client DHCP attivi e lo stato del client, ad esempio gli Stati DHCP INIT, BOOT, SELECTing, REQUESTing, RINNOVAting e così via. Se il timeout della sessione scade prima di ricevere il messaggio client successivo, a meno che il client non sia associato a un lease IP, il server cancellerà i dati della sessione client e restituirà l'indirizzo IP assegnato nuovamente al pool disponibile.</span><span class="sxs-lookup"><span data-stu-id="bc66a-131">The NetX DHCP Server can handles multiple Client sessions by keeping a table of active DHCP clients and what 'state' the Client is in e.g. DHCP states INIT, BOOT, SELECTING, REQUESTING, RENEWING etc. If the session time out expires before receiving the next Client message, unless that Client is bound to an IP lease, the Server will clear the Client session data and return the assigned IP address back to the available pool.</span></span> <span data-ttu-id="bc66a-132">Se il server riceve più messaggi di individuazione dallo stesso client, il server reimposta il timeout della sessione e mantiene l'indirizzo IP riservato affinché il client accetti in un messaggio di richiesta successivo.</span><span class="sxs-lookup"><span data-stu-id="bc66a-132">If the Server receives multiple DISCOVER messages from the same Client the Server resets the session time out and keeps the IP address reserved for the Client to accept in a subsequent REQUEST message.</span></span>

<span data-ttu-id="bc66a-133">Il server DHCP NetX accetta anche la richiesta DHCP a stato singolo, ad esempio il client invia solo un messaggio di richiesta.</span><span class="sxs-lookup"><span data-stu-id="bc66a-133">The NetX DHCP Server also accepts the single state Client DHCP request e.g. the Client only sends a REQUEST message.</span></span> <span data-ttu-id="bc66a-134">Si presuppone che al client sia stato precedentemente assegnato un lease IP dal server DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-134">This assumes the Client has been previously assigned an IP lease from the DHCP server.</span></span>

### <a name="setting-interface-specific-network-parameters-server-responses"></a><span data-ttu-id="bc66a-135">Impostazione delle risposte del server dei parametri di rete specifici dell'interfaccia</span><span class="sxs-lookup"><span data-stu-id="bc66a-135">Setting Interface Specific Network Parameters Server Responses</span></span>

<span data-ttu-id="bc66a-136">L'applicazione può impostare i parametri del router, subnet mask e del server DNS per ogni interfaccia che gestisce le richieste dei client DHCP, usando il servizio *nx_dhcp_set_interface_network_parameters* .</span><span class="sxs-lookup"><span data-stu-id="bc66a-136">The application can set the router, subnet mask and DNS server parameters for each interface it handles DHCP Client requests, using the *nx_dhcp_set_interface_network_parameters* service.</span></span> <span data-ttu-id="bc66a-137">In caso contrario, questi parametri vengono impostati rispettivamente sul gateway IP sull'interfaccia principale del server, sulla subnet di rete DHCP e sull'indirizzo IP del server DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-137">Otherwise these parameters are defaulted to the IP gateway on the Server's primary interface, its DHCP network subnet, and DHCP Server IP address, respectively.</span></span>

<span data-ttu-id="bc66a-138">Il server DHCP include questi parametri nei dati delle opzioni dei messaggi DHCP inviati ai client DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-138">The DHCP Server includes these parameters in the option data of DHCP messages it sends to DHCP clients.</span></span>

### <a name="assigning-ip-addresses-to-the-client"></a><span data-ttu-id="bc66a-139">Assegnazione di indirizzi IP al client</span><span class="sxs-lookup"><span data-stu-id="bc66a-139">Assigning IP addresses to the Client</span></span>

<span data-ttu-id="bc66a-140">Se il messaggio di individuazione del client non specifica un indirizzo IP richiesto, il server DHCP può utilizzarne uno dal proprio pool.</span><span class="sxs-lookup"><span data-stu-id="bc66a-140">If the Client DISCOVER message does not specify a requested IP address, the DHCP Server can use one from its own pool.</span></span> <span data-ttu-id="bc66a-141">Se il server non dispone di indirizzi IP disponibili, invierà al client un messaggio NACK.</span><span class="sxs-lookup"><span data-stu-id="bc66a-141">If the Server has no available IP addresses it will send the Client a NACK message.</span></span>

<span data-ttu-id="bc66a-142">Il server DHCP NetX concederà l'indirizzo IP richiesto nel messaggio di richiesta client purché l'indirizzo IP sia disponibile e si trovi nel database degli indirizzi IP del server.</span><span class="sxs-lookup"><span data-stu-id="bc66a-142">The NetX DHCP Server will grant the requested IP address in the Client REQUEST message as long as the IP address is available and can be found in the Server IP address database.</span></span> <span data-ttu-id="bc66a-143">L'applicazione crea l'elenco di indirizzi IP disponibili per l'assegnazione ai client DHCP utilizzando il servizio *nx_dhcp_create_server_ip_address_list* .</span><span class="sxs-lookup"><span data-stu-id="bc66a-143">The application creates the Server's list of available IP addresses for assigning to DHCP Clients using the *nx_dhcp_create_server_ip_address_list* service.</span></span> <span data-ttu-id="bc66a-144">Se il server non dispone degli indirizzi IP richiesti oppure viene assegnato a un altro host, invierà al client un messaggio NACK.</span><span class="sxs-lookup"><span data-stu-id="bc66a-144">If the Server does not have the requested IP addresses or it is assigned to another host it will send the Client a NACK message.</span></span>

<span data-ttu-id="bc66a-145">Quando il server DHCP riceve una richiesta client, identifica il client in modo univoco utilizzando l'indirizzo MAC del client nel campo indirizzo MAC client del messaggio DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-145">When the DHCP Server receives a Client request, it identifies that Client uniquely using the Client MAC address in the Client MAC address field in the DHCP message.</span></span> <span data-ttu-id="bc66a-146">Se il client modifica l'indirizzo MAC o viene spostato altrove su un'altra subnet, deve inviare un messaggio di rilascio al server per restituire l'indirizzo IP al pool disponibile e richiedere un nuovo indirizzo IP nello stato INIT.</span><span class="sxs-lookup"><span data-stu-id="bc66a-146">If the Client changes it's MAC address or is moved elsewhere onto another subnet it should send a RELEASE message to the Server to return the IP address back to the available pool, and request a new IP address in the INIT state.</span></span>

<span data-ttu-id="bc66a-147">Per informazioni dettagliate, vedere la figura 1,1 della sezione **sistema di esempio di piccole dimensioni** .</span><span class="sxs-lookup"><span data-stu-id="bc66a-147">See Figure 1.1 of the **Small Example System** section for details.</span></span> <span data-ttu-id="bc66a-148">Il numero di indirizzi IP salvati nell'istanza del server DHCP è limitato alle dimensioni della matrice di indirizzi del server nel blocco di controllo server DHCP e viene definito dall'opzione configurabile NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE.</span><span class="sxs-lookup"><span data-stu-id="bc66a-148">The number of IP addresses saved to the DHCP Server instance is limited to the size of the server address array in the DHCP Server control block, and defined by the configurable option NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE.</span></span>

### <a name="ip-address-lease-times"></a><span data-ttu-id="bc66a-149">Tempi di lease degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="bc66a-149">IP Address Lease Times</span></span>

<span data-ttu-id="bc66a-150">Il server DHCP accetterà anche il tempo di lease del client di richiesta se tale tempo di lease è inferiore al tempo di lease predefinito del server, definito nell'opzione configurabile NX_DHCP_DEFAULT_LEASE_TIME.</span><span class="sxs-lookup"><span data-stu-id="bc66a-150">The DHCP Server will also accept the request Client lease time if that lease time is less than the Server default lease time which is defined in configurable option NX_DHCP_DEFAULT_LEASE_TIME.</span></span> <span data-ttu-id="bc66a-151">I tempi di rinnovo e di riassociazione assegnati al client sono rispettivamente del 50% e del 85% del tempo di lease, a meno che il tempo di lease non sia infinito (0xFFFFFFFF), nel qual caso i tempi di rinnovo e di riassociazione vengono impostati anche su infinito.</span><span class="sxs-lookup"><span data-stu-id="bc66a-151">Renewal and rebind times assigned to the Client are 50% and 85% of the lease time, respectively, unless the lease time is infinity (0xFFFFFFFF), in which case renewal and rebind times are also set to infinity.</span></span>

### <a name="dhcp-server-timeouts"></a><span data-ttu-id="bc66a-152">Timeout server DHCP</span><span class="sxs-lookup"><span data-stu-id="bc66a-152">DHCP Server Timeouts</span></span>

<span data-ttu-id="bc66a-153">Il server DHCP dispone di un timeout di sessione configurabile dall'utente, NX_DHCP_CLIENT_SESSION_TIMEOUT, per attendere il successivo messaggio del client DHCP, a meno che la sessione non venga completata.</span><span class="sxs-lookup"><span data-stu-id="bc66a-153">The DHCP Server has a user configurable session timeout, NX_DHCP_CLIENT_SESSION_TIMEOUT, for waiting for the next DHCP Client message unless the session is completed.</span></span> <span data-ttu-id="bc66a-154">Il timeout viene reimpostato quando il server riceve il messaggio successivo dal client indipendentemente dal fatto che sia lo stesso messaggio inviato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bc66a-154">The time out is reset when the Server receives the next message from the Client regardless if is the same message previously sent.</span></span>

### <a name="internal-error-handling"></a><span data-ttu-id="bc66a-155">Gestione interna degli errori</span><span class="sxs-lookup"><span data-stu-id="bc66a-155">Internal error handling</span></span>

<span data-ttu-id="bc66a-156">Il server DHCP riceve ed elabora i pacchetti client DHCP nella funzione *nx_dhcp_listen_for_messages* .</span><span class="sxs-lookup"><span data-stu-id="bc66a-156">The DHCP Server receives and processes DHCP Client packets in the *nx_dhcp_listen_for_messages* function.</span></span> <span data-ttu-id="bc66a-157">Questa funzione interrompe l'elaborazione del pacchetto client DHCP corrente se il pacchetto non è valido o se il server DHCP rileva un errore interno. n *x_dhcp_listen_for_messages* restituisce uno stato di errore.</span><span class="sxs-lookup"><span data-stu-id="bc66a-157">This function will discontinue processing the current DHCP Client packet if the packet is invalid, or the DHCP Server encounters an internal error.n *x_dhcp_listen_for_messages* returns an error status.</span></span> <span data-ttu-id="bc66a-158">Il thread del server DHCP cede il controllo brevemente all'utilità di pianificazione di ThreadX prima di chiamare questa funzione per ricevere il successivo messaggio del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-158">The DHCP Server thread relinquishes control briefly of the ThreadX scheduler before calling this function to receive the next DHCP Client message.</span></span> <span data-ttu-id="bc66a-159">Nella versione corrente non è disponibile alcun supporto per la registrazione per lo stato di errore restituito da *nx_dhcp_listen_for_messages.*</span><span class="sxs-lookup"><span data-stu-id="bc66a-159">In the current release there is no logging support for error status returns from *nx_dhcp_listen_for_messages.*</span></span>

### <a name="option-55-parameter-request-list"></a><span data-ttu-id="bc66a-160">Opzione 55: elenco di richieste di parametri</span><span class="sxs-lookup"><span data-stu-id="bc66a-160">Option 55: Parameter Request List</span></span>

<span data-ttu-id="bc66a-161">Il server DHCP di NetX deve essere configurato con un set di opzioni per caricare nell'elenco di opzioni di richiesta parametro (55) nell'offerta e i messaggi DHCPACK trasmessi al client.</span><span class="sxs-lookup"><span data-stu-id="bc66a-161">The NetX DHCP Server must be configured with a set of options to load to Parameter Request Option (55) list in the OFFER and DHCPACK messages it transmits back to the Client.</span></span> <span data-ttu-id="bc66a-162">Queste opzioni includono i dati di configurazione di rete critici per la rete client e per impostazione predefinita è definito come indirizzo IP del router, subnet mask e server DNS.</span><span class="sxs-lookup"><span data-stu-id="bc66a-162">These options should include network critical configuration data for the Client network and by default is defined to be router IP address, subnet mask, and DNS server.</span></span> <span data-ttu-id="bc66a-163">L'elenco di opzioni è un elenco delimitato da spazi e definito nell'NX_DHCP_DEFAULT_SERVER_OPTION_LIST configurabile dall'utente.</span><span class="sxs-lookup"><span data-stu-id="bc66a-163">The option list is a space delimited list and defined in the user configurable NX_DHCP_DEFAULT_SERVER_OPTION_LIST.</span></span> <span data-ttu-id="bc66a-164">Si noti che il numero di opzioni specificato in questo elenco deve essere uguale NX_DHCP_DEFAULT_OPTION_LIST_SIZE anche definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="bc66a-164">Note the number of options specified in this list must equal NX_DHCP_DEFAULT_OPTION_LIST_SIZE which is also user defined.</span></span>

## <a name="constraints-of-the-netx-dhcp-server"></a><span data-ttu-id="bc66a-165">Vincoli del server DHCP NetX</span><span class="sxs-lookup"><span data-stu-id="bc66a-165">Constraints of the NetX DHCP Server</span></span>

### <a name="dhcp-messages"></a><span data-ttu-id="bc66a-166">Messaggi DHCP</span><span class="sxs-lookup"><span data-stu-id="bc66a-166">DHCP Messages</span></span>

<span data-ttu-id="bc66a-167">Il server DHCP NetX non verifica che un indirizzo IP sia stato assegnato altrove sulla rete prima di concedere l'indirizzo IP al client.</span><span class="sxs-lookup"><span data-stu-id="bc66a-167">The NetX DHCP Server does not verify that an IP address has not been assigned elsewhere on the network before granting the IP address to the Client.</span></span> <span data-ttu-id="bc66a-168">Se sono presenti più server DHCP, è possibile che questo sia il caso.</span><span class="sxs-lookup"><span data-stu-id="bc66a-168">If there are multiple DHCP servers, this can indeed be the case.</span></span> <span data-ttu-id="bc66a-169">*In base allo standard RFC 2131, è responsabilità del cliente verificare che l'indirizzo IP sia univoco sulla propria rete,* ad esempio eseguendo il ping dell'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="bc66a-169">*As per RFC 2131, it is the Client's responsibility to verify the IP address is unique on its network* (e.g. pinging the address).</span></span> <span data-ttu-id="bc66a-170">In caso contrario, il server deve ricevere un messaggio di rifiuto con l'indirizzo IP per aggiornare il relativo database dal client.</span><span class="sxs-lookup"><span data-stu-id="bc66a-170">If it is not, the Server should receive a DECLINE message with the IP address to update its database from the Client.</span></span>

<span data-ttu-id="bc66a-171">Il server DHCP NetX non emette messaggi di FORCE_RENEW.</span><span class="sxs-lookup"><span data-stu-id="bc66a-171">The NetX DHCP Server does not issue FORCE_RENEW messages.</span></span> <span data-ttu-id="bc66a-172">È il client DHCP a rinnovare il lease di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-172">It is up to the DHCP Client to renew its IP address lease.</span></span> <span data-ttu-id="bc66a-173">Tuttavia, il server DHCP monitora il tempo rimanente per tutti gli indirizzi IP assegnati nel database.</span><span class="sxs-lookup"><span data-stu-id="bc66a-173">However, the DHCP Server monitors the time remaining on all the assigned IP addresses in its database.</span></span> <span data-ttu-id="bc66a-174">Quando un lease di indirizzi IP scade, l'indirizzo IP viene restituito al pool di indirizzi IP disponibili.</span><span class="sxs-lookup"><span data-stu-id="bc66a-174">When an IP address lease expires, that IP address is returned to the pool of available IP addresses.</span></span> <span data-ttu-id="bc66a-175">Quindi spetta al client rinnovare/riassociare attivamente il lease degli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-175">Hence it is up to the Client to actively renew/rebind its IP address lease.</span></span>

<span data-ttu-id="bc66a-176">I dati della sessione vengono cancellati non appena il client viene concesso ("associato") a un lease IP (o uno esistente viene rinnovato).</span><span class="sxs-lookup"><span data-stu-id="bc66a-176">Session data is cleared as soon as the Client either is granted ("bound") to an IP lease (or an existing one is renewed).</span></span> <span data-ttu-id="bc66a-177">Se un pacchetto client dimostra un falso o si verifica il timeout del client tra le risposte, i dati della sessione vengono cancellati.</span><span class="sxs-lookup"><span data-stu-id="bc66a-177">If a Client packet proves bogus, or the Client times out between responses, session data is cleared.</span></span>

### <a name="saving-data-between-reboots"></a><span data-ttu-id="bc66a-178">Salvataggio dei dati tra i riavvii</span><span class="sxs-lookup"><span data-stu-id="bc66a-178">Saving Data Between Reboots</span></span>

<span data-ttu-id="bc66a-179">Il server DHCP NetX Salva i dati client inclusi i parametri di richiesta DHCP in una tabella di record client.</span><span class="sxs-lookup"><span data-stu-id="bc66a-179">The NetX DHCP Server saves Client data including DHCP request parameters in a Client record table.</span></span> <span data-ttu-id="bc66a-180">Questa tabella non è archiviata nella memoria non volatile, pertanto se l'host del server DHCP deve riavviare tali informazioni non vengono salvate tra i riavvii.</span><span class="sxs-lookup"><span data-stu-id="bc66a-180">This table is not stored in non volatile memory, so if the DHCP Server host must reboot that information is not saved between reboots.</span></span>

<span data-ttu-id="bc66a-181">Il server DHCP NetX Salva i dati di lease degli indirizzi IP in una tabella di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-181">The NetX DHCP Server saves IP address lease data in a IP address table.</span></span> <span data-ttu-id="bc66a-182">Questa tabella non è archiviata nella memoria non volatile, pertanto se l'host del server DHCP deve riavviare tali informazioni non vengono salvate tra i riavvii.</span><span class="sxs-lookup"><span data-stu-id="bc66a-182">This table is not stored in non volatile memory, so if the DHCP Server host must reboot that information is not saved between reboots.</span></span>

### <a name="relay-agents"></a><span data-ttu-id="bc66a-183">Agenti di inoltro</span><span class="sxs-lookup"><span data-stu-id="bc66a-183">Relay Agents</span></span>

<span data-ttu-id="bc66a-184">Il server DHCP NetX è configurato con un indirizzo IP zero per il campo "agente di inoltro" perché non supporta le richieste DHCP di rete.</span><span class="sxs-lookup"><span data-stu-id="bc66a-184">The NetX DHCP Server is configured with a zero IP address for the 'Relay agent' field because it does not support out of network DHCP requests.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="bc66a-185">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="bc66a-185">Small Example System</span></span>

<span data-ttu-id="bc66a-186">Un esempio di come è facile usare il server DHCP NetX è descritto nella figura 1,1 riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="bc66a-186">An example of how easy it is to use the NetX DHCP Server is described in Figure 1.1 that appears below.</span></span> <span data-ttu-id="bc66a-187">In questo esempio il file di inclusione DHCP *nx_dhcp_server. h* viene portato nella riga 5.</span><span class="sxs-lookup"><span data-stu-id="bc66a-187">In this example, the DHCP include file *nx_dhcp_server.h* is brought in at line 5.</span></span> <span data-ttu-id="bc66a-188">Dimensioni dello stack di thread del server DHCP, dimensioni dello stack del thread IP e dimensioni dello stack del thread di test sono tutte definite nelle righe 7-13.</span><span class="sxs-lookup"><span data-stu-id="bc66a-188">DHCP Server thread stack size, IP thread stack size and test thread stack size are all defined in lines 7-13.</span></span>

<span data-ttu-id="bc66a-189">Per prima cosa, un'attività del thread di test facoltativa per l'arresto, il riavvio e la fine dell'eliminazione del server DHCP viene creata con la funzione "*test_thread_entry*" alla riga 57.</span><span class="sxs-lookup"><span data-stu-id="bc66a-189">First, an optional test thread task for stopping, restarting and eventually deleting the DHCP server is created with the "*test_thread_entry*" function at line 57.</span></span> <span data-ttu-id="bc66a-190">Un blocco di controllo server DHCP "*dhcp_server*" viene definito come variabile globale alla riga 20.</span><span class="sxs-lookup"><span data-stu-id="bc66a-190">A DHCP Server control block "*dhcp_server*" is defined as a global variable at line 20.</span></span> <span data-ttu-id="bc66a-191">Si noti che il pool di pacchetti del server viene creato con i pacchetti con un payload almeno pari al messaggio DHCP standard (548 byte più i byte di intestazione IP e UDP).</span><span class="sxs-lookup"><span data-stu-id="bc66a-191">Note that the server packet pool is created with packets having a payload at least as large as the standard DHCP message (548 bytes plus IP and UDP header bytes).</span></span> <span data-ttu-id="bc66a-192">Dopo aver creato un'istanza IP per il server DHCP, l'applicazione crea il server DHCP alla riga 96.</span><span class="sxs-lookup"><span data-stu-id="bc66a-192">After successfully creating an IP instance for the DHCP Server, the application creates the DHCP Server in line 96.</span></span> <span data-ttu-id="bc66a-193">Successivamente, l'applicazione consente all'istanza IP del server di essere abilitata per UDP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-193">Next, the application enables the Server IP instance to be UDP enabled.</span></span> <span data-ttu-id="bc66a-194">Prima di avviare il server DHCP, l'elenco di indirizzi IP disponibili viene creato nella riga 137 usando il servizio *nx_dhcp_create_server_ip_address_list* .</span><span class="sxs-lookup"><span data-stu-id="bc66a-194">Before starting the DHCP Server, the available IP address list is created in line 137 using the *nx_dhcp_create_server_ip_address_list* service.</span></span> <span data-ttu-id="bc66a-195">I parametri di configurazione di rete vengono impostati nella riga 138 seguente utilizzando il servizio *nx_dhcp_set_interface_network_parameters* , i servizi server DHCP diventano disponibili quando l'applicazione chiama il *nx_dhcp_server_start* alla riga 141.</span><span class="sxs-lookup"><span data-stu-id="bc66a-195">The network configuration parameters are set in the following line 138 using the *nx_dhcp_set_interface_network_parameters* service, DHCP Server services become available when the application calls the *nx_dhcp_server_start* at line 141.</span></span> <span data-ttu-id="bc66a-196">Nell'attività Test thread viene illustrato l'utilizzo dell'arresto e del riavvio del server DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-196">The test thread task demonstrates the use of stopping and restarting the DHCP server.</span></span>

```c
/* This is a small demo of NetX DHCP Server for the high-performance NetX TCP/IP stack. */

#include     "tx_api.h"
#include     "nx_api.h"
#include     "nx_dhcp_server.h"

#define     DEMO_TEST_STACK_SIZE       2048
#define     DEMO_SERVER_STACK_SIZE     2048
#define     SERVER_IP_ADDRESS_LIST     "192.168.2.10 192.168.2.11 192.168.2.12"
#define     PACKET_PAYLOAD             1000
#define     PACKET_POOL_SIZE           (PACKET_PAYLOAD * 10)
#define     SERVER_IP_THREAD_STACK     2048

/* Define the ThreadX and NetX object control blocks... */

TX_THREAD          test_thread;
NX_PACKET_POOL     server_pool;
NX_IP              server_ip;
NX_DHCP_SERVER     dhcp_server;

/* Define the counters used in the demo application... */

ULONG             state_changes;

/* Define thread prototypes. */

void     test_thread_entry(ULONG thread_input);
void     nx_etherDriver_mcf5485(struct NX_IP_DRIVER_STRUCT *driver_req);

/* Define main entry point. */

intmain()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}

/* Define what the initial system looks like. */

void     tx_application_define(void *first_unused_memory)
{

CHAR     *pointer;
UINT     status;

    /* Setup the working pointer. */
    pointer = (CHAR *) first_unused_memory;

    /* Create the test thread. */
    status = tx_thread_create(&test_thread, "test thread", test_thread_entry, 0,
                pointer, TEST_STACK_SIZE, 1, 1, TX_NO_TIME_SLICE, TX_DONT_START);

    if (status)
    {
        printf("Error with DHCP test thread create. Status 0x%x\r\n", status);
        return;
    }

    pointer = pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create the DHCP Server packet pool. */
    status = nx_packet_pool_create(&server_pool, "NetX Main Packet Pool",
                                PACKET_PAYLOAD, pointer, PACKET_POOL_SIZE);
                                pointer = pointer + PACKET_POOL_SIZE;

    /* Check for pool creation error. */
    if (status)
    {
        printf("Error with DHCP server packet pool create. Status 0x%x\r\n", status);
        return;
    }

    /* Create the DHCP Server IP instance. */
    status = nx_ip_create(&server_ip, "NetX DHCP Server IP", NX_DHCP_SERVER_IP_ADDRESS,
                        0xFFFFFF00UL, &server_pool, nx_etherDriver_mcf5485, pointer,
                        SERVER_IP_THREAD_STACK, 1);

    pointer = pointer + DEMO_IP_THREAD_STACK;

    /* Check for IP create errors. */
    if (status)
    {
        printf("Error with DHCP server IP task create. Status 0x%x\r\n", status);
        return;
    }

    /* Create the DHCP Server instance. */
    status = nx_dhcp_server_create(&dhcp_server, &server_ip, pointer,
                    DEMO_SERVER_STACK_SIZE,"DHCP Server", &server_pool);

    if (status)
    {
        printf("Error with DHCP server create. Status 0x%x\r\n", status);
        return;
    }

    pointer = pointer + DEMO_SERVER_STACK_SIZE;

    /* Enable ARP and supply ARP cache memory for IP Instance 0. */
    status = nx_arp_enable(&server_ip, (void *) pointer, 1024);
    pointer = pointer + 1024;

    /* Check for ARP enable errors. */
    if (status)
    {
        printf("Error with ARP enable. Status 0x%x\r\n", status);
        return;
    }

    /* Enable UDP traffic. */
    status = nx_udp_enable(&server_ip);

    /* Check for UDP enable errors. */
    if (status)
    {
        printf("Error with ICMP enable. Status 0x%x\r\n", status);
        return;
    }

    /* Enable ICMP to enable the ping utility. */
    status = nx_icmp_enable(&server_ip);

    /* Check for errors. */
    if (status)
    {
        printf("Error with ICMP enable. Status 0x%x\r\n", status);
    }

    status = nx_dhcp_create_server_ip_address_list(&dhcp_server, iface_index,
                START_IP_ADDRESS_LIST, END_IP_ADDRESS_LIST, &addresses_added);
    status = nx_dhcp_set_interface_network_parameters(&dhcp_server, iface_index,
                                        NX_DHCP_SUBNET_MASK, IP_ADDRESS(10,0,0,1),
                                        IP_ADDRESS(10,0,0,1));

    /* Start the DHCP Server. */
    status = nx_dhcp_server_start(&dhcp_server);

    tx_thread_resume(&test_thread);
}

/* Define the test thread. */
void     test_thread_entry(ULONG thread_input)
{

UINT     status;
UINT     keep_spinning;

    /* Just let the test thread be idle till we're ready to shut things down. */
    keep_spinning = 1;
    while(keep_spinning)
    {
        tx_thread_sleep(300);
    }

    printf("Stopping the server...\n");
    status = nx_dhcp_server_stop(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server stop. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(500);

    printf("Starting the server...\n");
    status = nx_dhcp_server_start(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server start. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(600);

    printf("Stopping the server for good...\n");
    status = nx_dhcp_server_stop(&dhcp_server);
    if (status)
    {
        printf("Error with DHPC server stop. Status 0x%x\r\n", status);
        return;
    }

    tx_thread_sleep(200);

    printf("Deleting the server...\n");
    status = nx_dhcp_server_delete(&dhcp_server);
    if (status)
    {
        printf("Error with DHCP server delete. Status 0x%x\r\n", status);
        return;
    }
}
```

<span data-ttu-id="bc66a-197">Figura 1,1 esempio di applicazione server DHCP NetX</span><span class="sxs-lookup"><span data-stu-id="bc66a-197">Figure 1.1 Example NetX DHCP Server application</span></span>

## <a name="configuration-options"></a><span data-ttu-id="bc66a-198">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="bc66a-198">Configuration Options</span></span>

<span data-ttu-id="bc66a-199">Sono disponibili diverse opzioni di configurazione per la compilazione del server DHCP NetX.</span><span class="sxs-lookup"><span data-stu-id="bc66a-199">There are several configuration options for building NetX DHCP Server.</span></span> <span data-ttu-id="bc66a-200">L'elenco seguente descrive tutti i dettagli:</span><span class="sxs-lookup"><span data-stu-id="bc66a-200">The following list describes each in detail:</span></span>  
  
- <span data-ttu-id="bc66a-201">**NX_DISABLE_ERROR_CHECKING**: questa opzione rimuove il controllo degli errori DHCP di base.</span><span class="sxs-lookup"><span data-stu-id="bc66a-201">**NX_DISABLE_ERROR_CHECKING**: This option removes the basic DHCP error checking.</span></span> <span data-ttu-id="bc66a-202">Viene in genere usato dopo il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bc66a-202">It is typically used after the application is debugged.</span></span>  
- <span data-ttu-id="bc66a-203">**NX_DHCP_SERVER_THREAD_PRIORITY**: questa opzione specifica la priorità del thread del server DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-203">**NX_DHCP_SERVER_THREAD_PRIORITY**: This option specifies the priority of the DHCP Server thread.</span></span> <span data-ttu-id="bc66a-204">Per impostazione predefinita, questo valore specifica che il thread DHCP viene eseguito con priorità 2.</span><span class="sxs-lookup"><span data-stu-id="bc66a-204">By default, this value specifies that the DHCP thread runs at priority 2.</span></span>
- <span data-ttu-id="bc66a-205">**NX_DHCP_TYPE_OF_SERVICE**: questa opzione specifica il tipo di servizio necessario per le richieste UDP DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-205">**NX_DHCP_TYPE_OF_SERVICE**: This option specifies the type of service required for the DHCP UDP requests.</span></span> <span data-ttu-id="bc66a-206">Per impostazione predefinita, questo valore viene definito come NX_IP_NORMAL per indicare il normale servizio pacchetti IP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-206">By default, this value is defined as NX_IP_NORMAL to indicate normal IP packet service.</span></span>
- <span data-ttu-id="bc66a-207">**NX_DHCP_FRAGMENT_OPTION**: abilitazione del frammento per le richieste UDP DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-207">**NX_DHCP_FRAGMENT_OPTION**: Fragment enable for DHCP UDP requests.</span></span> <span data-ttu-id="bc66a-208">Per impostazione predefinita, questo valore è impostato su NX_DONT_FRAGMENT per disabilitare la frammentazione UDP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-208">By default, this value is set to NX_DONT_FRAGMENT to disable UDP fragmenting.</span></span>
- <span data-ttu-id="bc66a-209">**NX_DHCP_TIME_TO_LIVE**: specifica il numero di router che il pacchetto può superare prima che venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="bc66a-209">**NX_DHCP_TIME_TO_LIVE**: Specifies the number of routers the packet can pass before it is discarded.</span></span> <span data-ttu-id="bc66a-210">Il valore predefinito è 0x80.</span><span class="sxs-lookup"><span data-stu-id="bc66a-210">The default value is 0x80.</span></span>
- <span data-ttu-id="bc66a-211">**NX_DHCP_QUEUE_DEPTH** Specifica il numero di pacchetti che il socket del server DHCP mantiene prima di scaricare la coda.</span><span class="sxs-lookup"><span data-stu-id="bc66a-211">**NX_DHCP_QUEUE_DEPTH** Specifies the number of packets that the DHCP Server socket keeps before flushing the queue.</span></span> <span data-ttu-id="bc66a-212">Il valore predefinito è 5.</span><span class="sxs-lookup"><span data-stu-id="bc66a-212">The default value is 5.</span></span>
- <span data-ttu-id="bc66a-213">**NX_DHCP_PACKET_ALLOCATE_TIMEOUT**: specifica il timeout nei cicli del timer in modo che il server DHCP NETX attenda l'allocazione di un pacchetto dal relativo pool di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="bc66a-213">**NX_DHCP_PACKET_ALLOCATE_TIMEOUT**: Specifies the timeout in timer ticks for the NetX DHCP Server to wait for allocate a packet from its packet pool.</span></span> <span data-ttu-id="bc66a-214">Il valore predefinito è impostato su NX_IP_PERIODIC_RATE.</span><span class="sxs-lookup"><span data-stu-id="bc66a-214">The default value is set to NX_IP_PERIODIC_RATE.</span></span>
- <span data-ttu-id="bc66a-215">**NX_DHCP_SUBNET_MASK**: subnet mask il client DHCP deve essere configurato con.</span><span class="sxs-lookup"><span data-stu-id="bc66a-215">**NX_DHCP_SUBNET_MASK**: This is the subnet mask the DHCP Client should be configured with.</span></span> <span data-ttu-id="bc66a-216">Il valore predefinito è impostato su 0xFFFFFF00.</span><span class="sxs-lookup"><span data-stu-id="bc66a-216">The default value is set to 0xFFFFFF00.</span></span>
- <span data-ttu-id="bc66a-217">**NX_DHCP_FAST_PERIODIC_TIME_INTERVAL**: periodo di timeout nei cicli del timer per il timer rapido del server DHCP per il controllo del tempo di sessione rimanente e per la gestione delle sessioni scadute.</span><span class="sxs-lookup"><span data-stu-id="bc66a-217">**NX_DHCP_FAST_PERIODIC_TIME_INTERVAL**: This is timeout period in timer ticks for the DHCP Server fast timer to check on session time remaining and handle sessions that have timed out.</span></span>
- <span data-ttu-id="bc66a-218">**NX_DHCP_SLOW_PERIODIC_TIME_INTERVAL**: periodo di timeout nei segni di graduazione del timer per il timer del server DHCP lento per verificare il tempo di lease degli indirizzi IP rimanente e gestire il lease scaduto.</span><span class="sxs-lookup"><span data-stu-id="bc66a-218">**NX_DHCP_SLOW_PERIODIC_TIME_INTERVAL**: This is timeout period in timer ticks for the DHCP Server slow timer to check on IP address lease time remaining and handle lease that have timed out.</span></span>
- <span data-ttu-id="bc66a-219">**NX_DHCP_CLIENT_SESSION_TIMEOUT**: periodo di timeout nei cicli del timer il server DHCP attenderà di ricevere il successivo messaggio del client DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-219">**NX_DHCP_CLIENT_SESSION_TIMEOUT**: This is timeout period in timer ticks the DHCP Server will wait to receive the next DHCP Client message.</span></span>
- <span data-ttu-id="bc66a-220">**NX_DHCP_DEFAULT_LEASE_TIME**: tempo di lease degli indirizzi IP in secondi assegnato al client DHCP e la base per calcolare il rinnovo e i tempi di riassociazione assegnati anche al client.</span><span class="sxs-lookup"><span data-stu-id="bc66a-220">**NX_DHCP_DEFAULT_LEASE_TIME**: This is IP Address lease time in seconds assigned to the DHCP Client, and the basis for computing the renewal and rebind times also assigned to the Client.</span></span> <span data-ttu-id="bc66a-221">Il valore predefinito è impostato su 0xFFFFFFFF (Infinity).</span><span class="sxs-lookup"><span data-stu-id="bc66a-221">The default value is set to 0xFFFFFFFF (infinity).</span></span>
- <span data-ttu-id="bc66a-222">**NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE**: dimensione della matrice di server DHCP per l'assegnazione di indirizzi IP disponibili per l'assegnazione al client.</span><span class="sxs-lookup"><span data-stu-id="bc66a-222">**NX_DHCP_IP_ADDRESS_MAX_LIST_SIZE**: This is size of the DHCP Server array for holding available IP addresses for assigning to the Client.</span></span> <span data-ttu-id="bc66a-223">Il valore predefinito è 20.</span><span class="sxs-lookup"><span data-stu-id="bc66a-223">The default value is 20.</span></span>
- <span data-ttu-id="bc66a-224">**NX_DHCP_CLIENT_RECORD_TABLE_SIZE**: dimensione dell'array di server DHCP per la conservazione dei record client.</span><span class="sxs-lookup"><span data-stu-id="bc66a-224">**NX_DHCP_CLIENT_RECORD_TABLE_SIZE**: This is size of the DHCP Server array for holding Client records.</span></span> <span data-ttu-id="bc66a-225">Il valore predefinito è 50.</span><span class="sxs-lookup"><span data-stu-id="bc66a-225">The default value is 50.</span></span>
- <span data-ttu-id="bc66a-226">**NX_DHCP_CLIENT_OPTIONS_MAX**: dimensione della matrice nell'istanza del client DHCP per contenere tutte le opzioni richieste nell'elenco di richieste di parametri nella sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="bc66a-226">**NX_DHCP_CLIENT_OPTIONS_MAX**: This is size of the array in the DHCP Client instance for holding the all the requested options in the parameter request list in the current session.</span></span> <span data-ttu-id="bc66a-227">Il valore predefinito è 12.</span><span class="sxs-lookup"><span data-stu-id="bc66a-227">The default value is 12.</span></span>
- <span data-ttu-id="bc66a-228">**NX_DHCP_OPTIONAL_SERVER_OPTION_LIST**: si tratta del buffer che contiene l'elenco predefinito di opzioni del server DHCP da fornire al client DHCP corrente nell'elenco di richieste di parametri.</span><span class="sxs-lookup"><span data-stu-id="bc66a-228">**NX_DHCP_OPTIONAL_SERVER_OPTION_LIST**: This is the buffer holding the DHCP Server's default list of options to supply to the current DHCP Client in the parameter request list.</span></span> <span data-ttu-id="bc66a-229">Il valore predefinito è "1 3 6".</span><span class="sxs-lookup"><span data-stu-id="bc66a-229">The default is "1 3 6."</span></span>
- <span data-ttu-id="bc66a-230">**NX_DHCP_OPTIONAL_SERVER_OPTION_SIZE**: dimensione della matrice in cui è contenuto l'elenco predefinito di opzioni del server DHCP.</span><span class="sxs-lookup"><span data-stu-id="bc66a-230">**NX_DHCP_OPTIONAL_SERVER_OPTION_SIZE**: This is the size of the array to hold the DHCP Server's default list of options.</span></span> <span data-ttu-id="bc66a-231">Il valore predefinito è 3.</span><span class="sxs-lookup"><span data-stu-id="bc66a-231">The default value is 3.</span></span>
- <span data-ttu-id="bc66a-232">**NX_DHCP_SERVER_HOSTNAME_MAX**: dimensione del buffer per contenere il nome host del server.</span><span class="sxs-lookup"><span data-stu-id="bc66a-232">**NX_DHCP_SERVER_HOSTNAME_MAX**: This is size of the buffer for holding the Server host name.</span></span> <span data-ttu-id="bc66a-233">Il valore predefinito è (32).</span><span class="sxs-lookup"><span data-stu-id="bc66a-233">The default value is 32.</span></span>
- <span data-ttu-id="bc66a-234">**NX_DHCP_CLIENT_HOSTNAME_MAX**: dimensione del buffer per contenere il nome host del client nella sessione client del server DHCP corrente.</span><span class="sxs-lookup"><span data-stu-id="bc66a-234">**NX_DHCP_CLIENT_HOSTNAME_MAX**: This is size of the buffer for holding the Client host name in the current DHCP Server Client session.</span></span> <span data-ttu-id="bc66a-235">Il valore predefinito è (32).</span><span class="sxs-lookup"><span data-stu-id="bc66a-235">The default value is 32.</span></span>
