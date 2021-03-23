---
title: Capitolo 2-installazione e uso di Azure RTO NetX Duo DHCPv6 client
description: Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client DHCPv6 di Azure RTO NetX Duo.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: a154dbeb91b46a2c8bd5f4585e168a6b62d042ff
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821998"
---
# <a name="chapter-2---installation-and-use-of-azure-rtos-netx-duo-dhcpv6-client"></a><span data-ttu-id="d4b8f-103">Capitolo 2-installazione e uso di Azure RTO NetX Duo DHCPv6 client</span><span class="sxs-lookup"><span data-stu-id="d4b8f-103">Chapter 2 - Installation and use of Azure RTOS NetX Duo DHCPv6 Client</span></span>

<span data-ttu-id="d4b8f-104">Questo capitolo contiene una descrizione dei vari problemi relativi all'installazione, alla configurazione e all'utilizzo del componente client DHCPv6 di Azure RTO NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-104">This chapter contains a description of various issues related to installation, setup, and usage of the Azure RTOS NetX Duo DHCPv6 Client component.</span></span>

## <a name="product-distribution"></a><span data-ttu-id="d4b8f-105">Distribuzione del prodotto</span><span class="sxs-lookup"><span data-stu-id="d4b8f-105">Product Distribution</span></span>

<span data-ttu-id="d4b8f-106">Il client NetX Duo DHCPv6 è disponibile all'indirizzo [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo) .</span><span class="sxs-lookup"><span data-stu-id="d4b8f-106">NetX Duo DHCPv6 Client is available at [https://github.com/azure-rtos/netxduo](https://github.com/azure-rtos/netxduo).</span></span> <span data-ttu-id="d4b8f-107">Il pacchetto include due file di origine e un file PDF che contiene questo documento, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d4b8f-107">The package includes two source files and a PDF file that contains this document, as follows:</span></span>

- <span data-ttu-id="d4b8f-108">**nxd_dhcpv6_client. h** File di intestazione per il client DuoDHCPv6 di NetX</span><span class="sxs-lookup"><span data-stu-id="d4b8f-108">**nxd_dhcpv6_client.h** Header file for NetX DuoDHCPv6 Client</span></span>

- <span data-ttu-id="d4b8f-109">**nxd_dhcpv6_client. c** File di codice sorgente per il client DHCPv6 NetX Duo</span><span class="sxs-lookup"><span data-stu-id="d4b8f-109">**nxd_dhcpv6_client.c** Source code file for NetX Duo DHCPv6 Client</span></span>

- <span data-ttu-id="d4b8f-110">**demo_netxduo_dhcpv6_client. c** Programma di esempio che illustra la configurazione del client DHCPv6 NetX Duo</span><span class="sxs-lookup"><span data-stu-id="d4b8f-110">**demo_netxduo_dhcpv6_client.c** Sample program demonstrating the setup of the NetX Duo DHCPv6 Client</span></span>

- <span data-ttu-id="d4b8f-111">**nxd_dhcpv6_client.pdf** Descrizione PDF di NetX Duo DHCPv6 client</span><span class="sxs-lookup"><span data-stu-id="d4b8f-111">**nxd_dhcpv6_client.pdf** PDF description of NetX Duo DHCPv6 Client</span></span>

## <a name="netx-duo-dhcpv6-client-installation"></a><span data-ttu-id="d4b8f-112">Installazione del client NetX Duo DHCPv6</span><span class="sxs-lookup"><span data-stu-id="d4b8f-112">NetX Duo DHCPv6 Client Installation</span></span>

<span data-ttu-id="d4b8f-113">Per usare l'API client di NetX Duo DHCPv6, l'intera distribuzione indicata in precedenza può essere copiata nella stessa directory in cui è installato NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-113">To use NetX Duo DHCPv6 Client API, the entire distribution mentioned above can be copied to the same directory where NetX Duo is installed.</span></span> <span data-ttu-id="d4b8f-114">Se, ad esempio, NetX Duo è installato nella directory "*\threadx\arm7\green*", i file *nxd_dhcpv6_client. h* e *nxd_dhpcv6_client. c* possono essere copiati in questa directory.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-114">For example, if NetX Duo is installed in the directory “*\threadx\arm7\green*” then the *nxd_dhcpv6_client.h* and *nxd_dhpcv6_client.c* files can be copied into this directory.</span></span>

## <a name="using-the-netx-duo-dhcpv6-client"></a><span data-ttu-id="d4b8f-115">Uso del client DHCPv6 NetX Duo</span><span class="sxs-lookup"><span data-stu-id="d4b8f-115">Using the NetX Duo DHCPv6 Client</span></span>

<span data-ttu-id="d4b8f-116">Il codice dell'applicazione deve includere *nxd_dhcpv6_client. h* dopo aver incluso *tx_api. h* e *nx_api. h*, per usare rispettivamente i servizi Dhcpv6 client, threadX e NETX Duo.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-116">The application code must include *nxd_dhcpv6_client.h* after it includes *tx_api.h* and *nx_api.h*, to use DHCPv6 Client, ThreadX and NetX Duo services, respectively.</span></span> <span data-ttu-id="d4b8f-117">*nxd_dhcpv6_client. c* deve essere compilato nel progetto nello stesso modo in cui sono presenti altri file dell'applicazione e il relativo form oggetto deve essere collegato insieme ai file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-117">*nxd_dhcpv6_client.c* must be compiled in the project in the same manner as other application files and its object form must be linked along with the files of the application.</span></span>

### <a name="span-classunderlineclient-dhcp-unique-identifier-duidspan"></a><span data-ttu-id="d4b8f-118"><span class="underline">Identificatore univoco DHCP client (DUID)</span></span><span class="sxs-lookup"><span data-stu-id="d4b8f-118"><span class="underline">Client DHCP Unique Identifier (DUID)</span></span></span>

<span data-ttu-id="d4b8f-119">Il client DUID definisce in modo univoco ogni client in una rete.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-119">The Client DUID uniquely defines each Client on a network.</span></span> <span data-ttu-id="d4b8f-120">Un'applicazione deve creare un DUID client prima di richiedere un indirizzo IPv6 da un server.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-120">An application must create a Client DUID prior to requesting an IPv6 address from a Server.</span></span> <span data-ttu-id="d4b8f-121">Il client DUID viene automaticamente incluso in tutti i messaggi al server.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-121">The Client DUID is automatically included in all messages to the Server.</span></span> <span data-ttu-id="d4b8f-122">Per creare un DUID, l'applicazione chiama il servizio *nx_dhcpv6_create_client_duid:*</span><span class="sxs-lookup"><span data-stu-id="d4b8f-122">To create a DUID, the application calls the service *nx_dhcpv6_create_client_duid:*</span></span>
```C
UINT nx_dhcpv6_create_client_duid(NX_DHCPV6 *dhcpv6_ptr, 
                                  UINT duid_type, 
                                  UINT hardware_type, ULONG time);
```

<span data-ttu-id="d4b8f-123">L'applicazione chiama questo servizio e specifica il tipo di DUID (solo livello di collegamento o del livello di collegamento più tempo.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-123">The application calls this service and specifies the type of DUID (link layer only, or link layer plus time.</span></span> <span data-ttu-id="d4b8f-124">Per link layer Plus Time Duid, questo servizio fornirà il campo time se l'input time non è specificato.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-124">For link layer plus time DUIDs, this service will provide the time field if the time input is not specified.</span></span>

<span data-ttu-id="d4b8f-125">Per il riavvio dei dispositivi e l'utilizzo di un lease di indirizzi IPv6 assegnato in precedenza, l'applicazione deve creare il client DUID come quello usato al momento dell'assegnazione dell'indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-125">For devices rebooting and wishing to use a previously assigned IPv6 address lease, the application must create the Client DUID as the one it used when assigned the IPv6 address.</span></span> <span data-ttu-id="d4b8f-126">L'indirizzo del livello di collegamento è sufficiente per creare un client del livello di collegamento DUID.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-126">The link layer address is all that is needed to create a link layer Client DUID.</span></span> <span data-ttu-id="d4b8f-127">Questa operazione non richiede l'archiviazione di memoria non volatile precedente se il dispositivo ha accesso all'indirizzo del livello di collegamento.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-127">This does not require previous non volatile memory storage if the device has access to the link layer address.</span></span> <span data-ttu-id="d4b8f-128">Per DUID di tipo time, l'applicazione deve avere accesso agli stessi dati temporali usati nella creazione di DUID precedente e questa operazione richiede memoria non volatile.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-128">For DUIDs of type time, the application must have access to the same time data used in the previous DUID creation and this does require non volatile memory.</span></span> <span data-ttu-id="d4b8f-129">I client che non dispongono di una risorsa di archiviazione stabile non devono utilizzare Duid di tipo time.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-129">Clients that do not have any stable storage must not use DUIDs of type time.</span></span>

### <a name="span-classunderlineclient-identity-association-for-non-temporary-addresses-ianaspan"></a><span data-ttu-id="d4b8f-130"><span class="underline">Associazione di identità client per indirizzi non temporanei (IANA)</span></span><span class="sxs-lookup"><span data-stu-id="d4b8f-130"><span class="underline">Client Identity Association for Non Temporary Addresses (IANA)</span></span></span>

<span data-ttu-id="d4b8f-131">L'applicazione deve creare una IANA e, facoltativamente, uno o più indirizzi IA prima di richiedere un indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-131">The application must create an IANA and optionally one or more IA addresses before requesting an IPv6 address.</span></span> <span data-ttu-id="d4b8f-132">A tale scopo, l'applicazione chiama il servizio *nx_dhcpv6_create_client_iana* .</span><span class="sxs-lookup"><span data-stu-id="d4b8f-132">To do so, the application calls the *nx_dhcpv6_create_client_iana* service.</span></span> <span data-ttu-id="d4b8f-133">Per creare un'opzione di indirizzo IA, l'applicazione chiama il servizio *nx_dhcpv6_add_client_ia* con un indirizzo IPv6 e i valori di durata richiesti come hint per il server.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-133">To create an IA address option, the application calls the *nx_dhcpv6_add_client_ia* service with a requested IPv6 address and lifetime values as a hint to the Server.</span></span>

<span data-ttu-id="d4b8f-134">IANA e i rispettivi IAs definiscono cumulativamente i parametri di assegnazione degli indirizzi IPv6 del client:</span><span class="sxs-lookup"><span data-stu-id="d4b8f-134">The IANA and its IAs cumulatively define the Client IPv6 address assignment parameters:</span></span>

<span data-ttu-id="d4b8f-135">Prima di avviare il client DHCPv6, l'applicazione client DHCPv6 crea una IANA usando il servizio *nx_dhcpv6_create_client_iana* :</span><span class="sxs-lookup"><span data-stu-id="d4b8f-135">Before starting the DHCPv6 Client, the DHCPv6 Client application creates an IANA using the *nx_dhcpv6_create_client_iana* service:</span></span>

```C
UINT    nx_dhcpv6_create_client_iana(NX_DHCPV6 *dhcpv6_ptr, 
                                     UINT IA_ident, ULONG T1, ULONG T2);
```

<span data-ttu-id="d4b8f-136">Deve inoltre creare uno o più IAs utilizzando il servizio *nx_dhcpv6_create_client_ia* e gli indirizzi IPv6 richiesti prima di avviare il client DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-136">It must also create one or more IAs using the *nx_dhcpv6_create_client_ia* service and requested IPv6 addresses before starting the DHCPv6 Client.</span></span>

```C
UINT    nx_dhcpv6_add_client_ia(NX_DHCPV6 *dhcpv6_ptr, 
                                NXD_ADDRESS *ipv6_address, 
                                ULONG preferred_lifetime, 
                                ULONG valid_lifetime);
```

> [!NOTE]
> <span data-ttu-id="d4b8f-137">Il numero di indirizzi IA creati dall'applicazione non può superare il NX_DHCPV6_MAX_IA_ADDRESS parametro il cui valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-137">The number of IA addresses the application creates cannot exceed the NX_DHCPV6_MAX_IA_ADDRESS parameter whose default value is 1.</span></span>

<span data-ttu-id="d4b8f-138">Il client DHCPv6 NetX Duo supporta *nx_dhcpv6_create_client_ia* per le applicazioni client DHCPv6 legacy e che è identico a *nx_dhcpv6_add_client_ia* ma gli sviluppatori sono invitati a usare il servizio *nx_dhcpv6_add_client_ia* .</span><span class="sxs-lookup"><span data-stu-id="d4b8f-138">The NetX Duo DHCPv6 Client supports *nx_dhcpv6_create_client_ia* for legacy DHCPv6 Client applications and which is identical to *nx_dhcpv6_add_client_ia* but developers are encouraged to use the *nx_dhcpv6_add_client_ia* service.</span></span>

<span data-ttu-id="d4b8f-139">Questi servizi vengono illustrati in "piccolo esempio di sistema" in altre sezioni di questo capitolo.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-139">These services are demonstrated in the “Small Example System” elsewhere in this chapter.</span></span>

### <a name="span-classunderlinenon-volatile-memory-considerations-to-reuse-ianas-and-iasspan"></a><span data-ttu-id="d4b8f-140"><span class="underline">Considerazioni sulla memoria non volatile per il riutilizzo di IANA e IAs</span></span><span class="sxs-lookup"><span data-stu-id="d4b8f-140"><span class="underline">Non Volatile Memory Considerations To Reuse IANAs and IAs</span></span></span>

<span data-ttu-id="d4b8f-141">L'applicazione deve salvare i parametri IANA T1, T2 e l'identificatore IANA nella memoria non volatile se si desidera utilizzare lo stesso indirizzo (es) per il riavvio.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-141">The application must save IANA parameters T1, T2, and the IANA identifier to non volatile memory if it wishes to use the same address(es) on rebooting.</span></span> <span data-ttu-id="d4b8f-142">L'applicazione deve anche salvare la relativa IA, che include l'indirizzo IPv6 nella memoria non volatile.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-142">The application must also save its IA which includes its IPv6 address to non volatile memory.</span></span>

<span data-ttu-id="d4b8f-143">L'applicazione deve inoltre archiviare il tempo trascorso dal momento in cui è stato associato ai lease degli indirizzi IPv6 assegnati alla memoria non volatile in caso di chiusura.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-143">The application must also store the time elapsed that it has been bound to its assigned IPv6 address lease(s) to non volatile memory if shutting down.</span></span> <span data-ttu-id="d4b8f-144">Questa operazione viene eseguita chiamando il servizio *nx_dhcpv6_get_time_accrued* prima di arrestare il client DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-144">It does this by calling the *nx_dhcpv6_get_time_accrued* service before it stops the DHCPv6 Client.</span></span>

```C
UINT nx_dhcpv6_get_time_accrued(NX_DHCPV6 *dhcpv6_ptr, 
                                ULONG *time_accrued);
```

<span data-ttu-id="d4b8f-145">Supponendo che l'applicazione disponga di un clock indipendente per tenere traccia dell'intervallo di tempo da quando è stato arrestato e riavviato il client DHCPv6 dopo un riavvio, aggiunge il tempo trascorso al tempo trascorso sul lease IPv6 prima dell'arresto.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-145">Assuming the application has an independent clock to track the time interval from when it stopped and restarted the DHCPv6 Client after a reboot, it adds to that elapsed time to the time accrued on the IPv6 lease before stopping.</span></span> <span data-ttu-id="d4b8f-146">Inizia ora l'attività thread del client con il tempo totale trascorso associato al lease IPv6 come input nv_time riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d4b8f-146">It now starts the Client thread task with the total elapsed time bound to the IPv6 lease as the nv_time input below:</span></span>

```C
UINT nx_dhcpv6_start(NX_DHCPV6 *dhcpv6_ptr, ULONG nv_time);
```

<span data-ttu-id="d4b8f-147">Da questo punto, l'attività thread client DHCPv6 assumerà il controllo del tempo accumulato nel lease IPv6 per il momento in cui rinnovare il lease.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-147">From this point, the DHCPv6 Client thread task will take over monitoring the time accrued on the IPv6 lease for when to renew the lease.</span></span>

### <a name="span-classunderlinesetting-dhcpv6-option-dataspan"></a><span data-ttu-id="d4b8f-148"><span class="underline">Impostazione dei dati dell'opzione DHCPv6</span></span><span class="sxs-lookup"><span data-stu-id="d4b8f-148"><span class="underline">Setting DHCPv6 Option Data</span></span></span>

<span data-ttu-id="d4b8f-149">Prima di richiedere un lease IPv6, l'applicazione può richiedere altri dati di parametri di rete, ad esempio server DNS e server di ora.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-149">Before requesting an IPv6 lease, the application can request other network parameter data such as DNS server and time server.</span></span> <span data-ttu-id="d4b8f-150">Alcuni di questi parametri includono servizi specifici.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-150">Some of these parameters have specific services.</span></span> <span data-ttu-id="d4b8f-151">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="d4b8f-151">A few are shown below:</span></span>

```C
UINT  nx_dhcpv6_request_option_DNS_server(NX_DHCPV6 *dhcpv6_ptr, 
                                          UINT enable)

UINT  nx_dhcpv6_request_option_time_server(NX_DHCPV6 *dhcpv6_ptr, 
                                           UINT enable);
```

### <a name="span-classunderlineinitiating-the-ipv6-address-requestspan"></a><span data-ttu-id="d4b8f-152"><span class="underline">Avvio della richiesta di indirizzo IPv6</span></span><span class="sxs-lookup"><span data-stu-id="d4b8f-152"><span class="underline">Initiating the IPv6 address Request</span></span></span>

<span data-ttu-id="d4b8f-153">L'applicazione avvia il thread del client DHCPv6 chiamando il servizio di *nx_dhcpv6_start* con un input di ora zero.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-153">The application starts the DHCPv6 Client thread by calling the *nx_dhcpv6_start* service with a zero time input.</span></span> <span data-ttu-id="d4b8f-154">Per avviare il protocollo DHCPv6 per richiedere un indirizzo IPv6, l'applicazione chiama *nx_dhcpv6_request_solicit.*</span><span class="sxs-lookup"><span data-stu-id="d4b8f-154">To initiate the DHCPv6 protocol to request an IPv6 address, the application calls *nx_dhcpv6_request_solicit.*</span></span>

<span data-ttu-id="d4b8f-155">Se l'applicazione vuole usare un lease IPv6 assegnato in precedenza, chiama *nx_dhcpv6_start* con un input di ora diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-155">If the application wishes to use a previously assigned IPv6 lease assigned, it calls *nx_dhcpv6_start* with a non zero time input.</span></span> <span data-ttu-id="d4b8f-156">Non deve chiamare *nx_dhcpv6_request_solicit*.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-156">It should not call *nx_dhcpv6_request_solicit*.</span></span>

<span data-ttu-id="d4b8f-157">Successivamente, l'applicazione non deve eseguire altre operazioni e il client DHCPv6 eseguirà automaticamente il monitoraggio quando è il momento di rinnovare o riassociare un indirizzo IPv6.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-157">Thereafter the application need do nothing more and the DHCPv6 Client will automatically monitor when it is time to renew or rebind an IPv6 address.</span></span>

## <a name="small-example-system"></a><span data-ttu-id="d4b8f-158">Sistema di esempio di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="d4b8f-158">Small Example System</span></span>

<span data-ttu-id="d4b8f-159">Un esempio di come è facile usare il client DHCPv6 NetX Duo è descritto nel piccolo esempio seguente usando un client DHCPv6 e un driver "RAM" virtuale.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-159">An example of how easy it is to use the NetX Duo DHCPv6 Client is described in the small example below using a DHCPv6 Client and a virtual “RAM” driver.</span></span> <span data-ttu-id="d4b8f-160">Questa demo presuppone un dispositivo con una sola interfaccia di rete fisica.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-160">This demo assumes a device with only a single physical network interface.</span></span>

<span data-ttu-id="d4b8f-161">*tx_application_define* crea un pool di pacchetti per il client DHCPv6 per inviare messaggi DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-161">*tx_application_define* creates packet pool for the DHCPv6 Client to send DHCPv6 messages.</span></span> <span data-ttu-id="d4b8f-162">Viene inoltre creato un thread dell'applicazione e un'istanza IP.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-162">It also creates an application thread and IP instance.</span></span> <span data-ttu-id="d4b8f-163">Abilita quindi UDP e ICMP sull'IP nelle righe 130-148.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-163">It then enables UDP and ICMP on IP in lines 130-148.</span></span> <span data-ttu-id="d4b8f-164">Il client DHCPv6 viene quindi creato con le funzioni di callback di modifica dello stato (*dhcpv6_state_change_notify* ) e di errore del server (*dhcpv6_server_error_handler*) in line151.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-164">Then the DHCPv6 Client is created with state change (*dhcpv6_state_change_notify* ) and server error (*dhcpv6_server_error_handler*) callback functions in line151.</span></span>

<span data-ttu-id="d4b8f-165">Nella funzione di immissione thread del client *thread_client_entry*, l'indirizzo IP del client viene configurato con un indirizzo locale collegamento e abilitato per i servizi IPv6 e ICMPv6 sulle righe 202-217.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-165">In the Client thread entry function, *thread_client_entry*, the Client IP is set up with a link local address and enabled for IPv6 and ICMPv6 services on lines 202-217.</span></span> <span data-ttu-id="d4b8f-166">Prima di avviare il client DHCPv6, l'applicazione crea un client DUID, un'opzione IANA e un'opzione di indirizzo IA in lines219-303.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-166">Before starting the DHCPv6 Client, the application creates a Client DUID, an IANA option and an IA address option on lines219-303.</span></span> <span data-ttu-id="d4b8f-167">L'opzione Indirizzo IA è facoltativa se il client desidera richiedere un indirizzo IPv6 e durate valide e preferite dal server.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-167">The IA address option is optional if the Client wishes to request an IPv6 address and valid and preferred lifetimes from the Server.</span></span> <span data-ttu-id="d4b8f-168">Il server è in grado o meno di concedere l'indirizzo IPv6 o i tempi di lease richiesti.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-168">The Server may or may not grant the requested IPv6 address or lease times.</span></span> <span data-ttu-id="d4b8f-169">L'applicazione può aggiungere più opzioni IA (fino a NX_DHCPV6_MAX_IA_ADDRESS) a cui assegnare più indirizzi globali.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-169">The application may add more IA options (up to NX_DHCPV6_MAX_IA_ADDRESS) to be assigned multiple global addresses.</span></span>

<span data-ttu-id="d4b8f-170">Infine, l'applicazione imposta diverse opzioni per richiedere i parametri di rete nei messaggi al server DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-170">Lastly, the application sets various options to request network parameters in its messages to the DHCPv6 Server.</span></span> <span data-ttu-id="d4b8f-171">L'attività client DHCPv6 viene avviata chiamando *nx_dhcpv6_start* in line306 e il protocollo DHCPv6 effettivo viene avviato nello stato sollecitazione con la chiamata a *nx_dhcpv6_request_solicit* alla riga 317.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-171">The DHCPv6 Client task is started by calling *nx_dhcpv6_start* in line306, and the actual DHCPv6 protocol is started in the SOLICIT state with the call to *nx_dhcpv6_request_solicit* in line 317.</span></span> <span data-ttu-id="d4b8f-172">Il client DHCPv6 gestisce automaticamente la promozione dello stato del client tramite il protocollo DHCPv6 fino a quando non viene associato a un indirizzo o si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-172">The DHCPv6 Client then automatically handles the promotion of the Client state through the DHCPv6 protocol until it is bound to an address or an error occurs.</span></span> <span data-ttu-id="d4b8f-173">Durante questo periodo di tempo, l'applicazione attende il completamento del protocollo, oltre al rilevamento degli indirizzi duplicati (DAD) per il completamento se l'istanza IP è configurata per il padre (ovvero la configurazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="d4b8f-173">During this time, the application waits for the protocol to complete, as well as the Duplicate Address Detection (DAD) to complete if the IP instance is configured for DAD (which is the default configuration).</span></span>

<span data-ttu-id="d4b8f-174">Dopo la chiamata di tx_thread_sleep, l'applicazione controlla i parametri globali impostati nel callback di modifica dello stato per determinare l'esito positivo dell'attività client DHCPv6 per ottenere un lease IPv6 e, in caso affermativo, che la verifica dell'univocità del padre sia riuscita.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-174">After the tx_thread_sleep call, the application checks on the global parameters set in the state change callback to determine the success of both the DHCPv6 Client task to get assigned an IPv6 lease and if so, that the DAD check for uniqueness succeeded.</span></span> <span data-ttu-id="d4b8f-175">Questa operazione viene eseguita utilizzando i contatori impostati nelle funzioni modifica stato e callback errore server.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-175">This is done using the counters set up in the state change and server error callback functions.</span></span> <span data-ttu-id="d4b8f-176">L'applicazione esegue il polling per conteggi diversi da zero di address_not_assigned, address_expired e server_errors per l'assegnazione di indirizzi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-176">The application polls for non zero counts of address_not_assigned, address_expired and server_errors for failed address assignment.</span></span> <span data-ttu-id="d4b8f-177">Se il conteggio di bound_addresses è diverso da zero (almeno un indirizzo assegnato correttamente), verifica la presenza di un address_failed_dad diverso da zero per un controllo padre non riuscito.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-177">If the count of bound_addresses is non zero (at least one address successfully assigned), it checks for a non zero address_failed_dad for a failed DAD check.</span></span> <span data-ttu-id="d4b8f-178">Segue una spiegazione della modifica dello stato e dei callback di errore del server:</span><span class="sxs-lookup"><span data-stu-id="d4b8f-178">An explanation of the state change and server error callbacks follows:</span></span>

<span data-ttu-id="d4b8f-179">Il callback di modifica dello stato, *dhcpv6_state_change_notify*, lo stato del client DHCPv6 precedente e corrente per determinare se il client ha ricevuto risposte server valide:</span><span class="sxs-lookup"><span data-stu-id="d4b8f-179">The state change callback, *dhcpv6_state_change_notify*, the previous and current DHCPv6 Client state to determine if the Client received any valid Server responses:</span></span>

  - <span data-ttu-id="d4b8f-180">*dhcpv6_state_change_notify* controlla le transizioni direttamente da sollecitazione a init e, in tal caso, incrementa un contatore per il client DHCPv6 che non riceve risposte dal server.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-180">*dhcpv6_state_change_notify* checks for transitions directly from SOLICIT to INIT and if so it increments a counter for the DHCPv6 Client receiving no responses from the Server.</span></span>

<span data-ttu-id="d4b8f-181">Successivamente *dhcpv6_state_change_notify* controlla se il client è stato assegnato (associato) a uno o più indirizzi IPv6:</span><span class="sxs-lookup"><span data-stu-id="d4b8f-181">Next *dhcpv6_state_change_notify* checks if the Client was assigned (bound) to one or more IPv6 addresses:</span></span>

  - <span data-ttu-id="d4b8f-182">Se il nuovo stato è associato, incrementa un contatore di indirizzi associati al client.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-182">If the new state is BOUND, it increments a counter of addresses bound to the Client.</span></span>
    
<span data-ttu-id="d4b8f-183">Il *dhcpv6_state_change_notify* controlla anche la presenza di un controllo padre non riuscito:</span><span class="sxs-lookup"><span data-stu-id="d4b8f-183">The *dhcpv6_state_change_notify* also checks for a failed DAD check:</span></span>

  - <span data-ttu-id="d4b8f-184">Se le transizioni di stato da si RIFIUTAno a INIT, il client DHCPv6 non ha superato il controllo padre su uno degli indirizzi assegnati e incrementa il numero di assegnazioni di indirizzi non riuscite.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-184">If the state transitions from DECLINE to INIT, the DHCPv6 Client has failed DAD check on one of its assigned addresses and increments the count of failed address assignments.</span></span>
    
<span data-ttu-id="d4b8f-185">L'ultimo controllo per *dhcpv6_state_change_notify* in questo esempio è per un indirizzo assegnato correttamente che ha superato il controllo padre perché non venga rinnovato o riassociato:</span><span class="sxs-lookup"><span data-stu-id="d4b8f-185">The last check by *dhcpv6_state_change_notify* in this example is for a successfully assigned address that passed the DAD check to fail to be renewed or rebind:</span></span>

  - <span data-ttu-id="d4b8f-186">Se lo stato cambia da riassocia a INIT, il client non ha ricevuto alcuna risposta alle richieste RENEW o rebind e *dhcpv6_state_change_notify* incrementa il numero di indirizzi scaduti.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-186">If the state changes from REBIND to INIT, the Client did not get any responses to either its RENEW or REBIND requests and *dhcpv6_state_change_notify* increments its count of expired addresses.</span></span>

<span data-ttu-id="d4b8f-187">Il *dhcpv6_server_error_handler* se notificato dall'attività client DHCPv6 di uno stato di errore ricevuto dal server incrementa il numero di errori del server.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-187">The *dhcpv6_server_error_handler* if notified by the DHCPv6 Client task of an error status received from the Server increments the count of server errors.</span></span>

<span data-ttu-id="d4b8f-188">Supponendo che tutto vada bene, l'applicazione interroga il client DHCPv6 per i dati di indirizzo, inclusi i tempi di lease.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-188">Assuming all goes well, the application queries the DHCPv6 Client for address data including lease times.</span></span> <span data-ttu-id="d4b8f-189">Ottiene un conteggio degli indirizzi validi (correttamente assegnati) chiamando il servizio *nx_dhcpv6_get_valid_ip_address_count* e l'ora di rinnovo nello IANA (si applica a tutti gli indirizzi Ia assegnati) chiamando *nx_dhcpv6_get_iana_lease_time* sulle righe 372-392.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-189">It gets a count of valid (successfully assigned) addresses by calling the *nx_dhcpv6_get_valid_ip_address_count* service and time to renew in the IANA (applies to all IA addresses assigned) by calling *nx_dhcpv6_get_iana_lease_time* on lines 372-392.</span></span> <span data-ttu-id="d4b8f-190">Viene quindi eseguita una query sul client DHCPv6 per ciascuna delle opzioni IA per l'indirizzo IPv6 e i tempi di lease in base all'indice dell'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-190">It then queries the DHCPv6 Client for each of its IA options for IPv6 address and lease times by address index.</span></span>

<span data-ttu-id="d4b8f-191">Alcuni servizi client DHCPv6 (*nx_dhcpv6_get_lease_time_data, nx_dhcpv6_get_IP_address*) non richiedono un indice di indirizzo come input e restituiscono parametri DHCPv6 per l'indirizzo globale del client primario.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-191">Some DHCPv6 Client services (*nx_dhcpv6_get_lease_time_data, nx_dhcpv6_get_IP_address*) do not require an address index as an input, and return DHCPv6 parameters for the primary Client global address.</span></span> <span data-ttu-id="d4b8f-192">Questa operazione è adatta ai client con un singolo indirizzo IPv6 globale quando chiama *nx_dhcpv6_get_valid_ip_address_lease_time* alla riga 384.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-192">This is suitable for Clients with a single global IPv6 address when it calls *nx_dhcpv6_get_valid_ip_address_lease_time* in line 384.</span></span>

<span data-ttu-id="d4b8f-193">La configurazione client DHCPv6, NX_DHCPV6_CLIENT_RESTORE_STATE, t consente a un sistema di ripristinare un client DHCPv6 creato in precedenza nello stato associato tra i riavvii del sistema.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-193">The DHCPv6 Client configuration, NX_DHCPV6_CLIENT_RESTORE_STATE, t allows a system to restore a previously created DHCPv6 Client in Bound state between system reboots.</span></span> <span data-ttu-id="d4b8f-194">Chiamando il *nx_dhcpv6_client_get_record* per ottenere il record client DHCPv6 tra i riavvii del sistema alla riga 434, chiamando il *nx_dhcpv6_client_restore_record* per archiviare il record client DHCPv6 dopo l'accensione del sistema alla riga 525.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-194">Calling the *nx_dhcpv6_client_get_record* to get the DHCPv6 Client record between system reboots on line 434, calling the *nx_dhcpv6_client_restore_record* to store the DHCPv6 Client record after system power up on line 525.</span></span>

<span data-ttu-id="d4b8f-195">L'applicazione rilascia quindi gli indirizzi assegnati usando il servizio *nx_dhcpv6_request_release* alla riga 552.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-195">The application then releases the assigned addresses using the *nx_dhcpv6_request_release* service in line 552.</span></span> <span data-ttu-id="d4b8f-196">Per riavviare l'applicazione, arresta il client DHCPv6 con il servizio *nx_dhcpv6_client_stop* alla riga 567 e cancella tutti gli indirizzi IPv6 registrati con l'istanza IP configurata durantequesti DHCPv6 client.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-196">To restart the application stops the DHCPv6 Client with the *nx_dhcpv6_client_stop* service in line 567 and clears all IPv6 addresses registered with the IP instance that were configured throughthe DHCPv6 Client.</span></span> <span data-ttu-id="d4b8f-197">Questa operazione viene eseguita chiamando *nx_dhcpv6_reinitialize* alla riga 578.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-197">It does this by calling *nx_dhcpv6_reinitialize* in line 578.</span></span> <span data-ttu-id="d4b8f-198">Riavvia quindi l'attività client DHCPv6 con *nx_dhcpv6_start* e *nx_dhcpv6_request_solicit* servizi come prima.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-198">Then it restarts the DHCPv6 Client task with *nx_dhcpv6_start* and *nx_dhcpv6_request_solicit* services as before.</span></span>

<span data-ttu-id="d4b8f-199">Il client DHCPv6 viene eliminato con la chiamata a *nx_dhcpv6_delete* in line626.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-199">The DHCPv6 Client is deleted with the call to *nx_dhcpv6_delete* in line626.</span></span> <span data-ttu-id="d4b8f-200">Si noti che non elimina il pool di pacchetti *e* creato per il client DHCPv6 perché questo pool di pacchetti viene usato anche dall'istanza di IP.</span><span class="sxs-lookup"><span data-stu-id="d4b8f-200">Note that it does not delete th *e* packet pool it created for the DHCPv6 Client because this packet pool is also used by the IP instance.</span></span> <span data-ttu-id="d4b8f-201">In caso contrario, è necessario eliminare il pool di pacchetti se non è possibile utilizzarlo con il servizio NetX Duo *nx_packet_pool_delete* .</span><span class="sxs-lookup"><span data-stu-id="d4b8f-201">Otherwise it should delete the packet pool if it has no further use for it using the NetX Duo *nx_packet_pool_delete* service.</span></span>

```C
/* This is a small demo of the NetX Duo DHCPv6 Client for the high-performance NetX Duo stack. */

#include    <stdio.h>
#include   "tx_api.h"
#include   "nx_api.h"
#include   "nxd_dhcpv6_client.h"

#ifdef FEATURE_NX_IPV6
#define     DEMO_STACK_SIZE         2048

/* Set the client address, and request these address from DHCPv6 Server. */
/*
#define     NX_DHCPV6_REQUEST_IA_ADDRESS
*/

/* Set the list of DHCPv6 option data (timezone, DNS server, timer server, domain name)to get from the DHCPv6 server. */

#define     NX_DHCPV6_REQUEST_OPTION


/* Add the fully qualified domain name to request whether the DHCPv6 server SHOULD or SHOULD NOT perform the AAAA RR or DNS updates. */

#define     NX_DHCPV6_REQUEST_FQDN_OPTION


/* Define the ThreadX and NetX object control blocks... */

NX_PACKET_POOL          pool_0;
TX_THREAD               thread_client;
NX_IP                   client_ip;

/* Define the Client and Server instances. */

NX_DHCPV6               dhcp_client;

/* Define the error counter used in the demo application... */
ULONG                   error_counter;
CHAR                    *pointer;

/* Define thread prototypes. */
void    thread_client_entry(ULONG thread_input);

/***** Substitute your ethernet driver entry function here *********/
extern VOID    _nx_ram_network_driver(NX_IP_DRIVER *driver_req_ptr);

/* Declare DHCPv6 Client callbacks */
VOID dhcpv6_state_change_notify(NX_DHCPV6 *dhcpv6_ptr, UINT old_state, UINT new_state);
VOID dhcpv6_server_error_handler(NX_DHCPV6 *dhcpv6_ptr, UINT op_code, UINT status_code, UINT message_type);

/* Set up globals for tracking changes to DHCPv6 Client from callback services. */
UINT state_changes = 0;
UINT address_expired = 0;
UINT address_failed_dad = 0;
UINT bound_addresses = 0;
UINT address_not_assigned = 0;
UINT server_errors = 0;

/* Define some DHCPv6 parameters. */

#define DHCPV6_IANA_ID      0xC0DEDBAD
#define DHCPV6_T1           NX_DHCPV6_INFINITE_LEASE
#define DHCPV6_T2           NX_DHCPV6_INFINITE_LEASE
#define DHCPV6_RENEW_TIME   NX_DHCPV6_INFINITE_LEASE
#define DHCPV6_REBIND_TIME  NX_DHCPV6_INFINITE_LEASE
#define PACKET_PAYLOAD      500
#define PACKET_POOL_SIZE    (5*PACKET_PAYLOAD)

/* Define main entry point. */

int main()
{

    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
}


/* Define what the initial system looks like. */

void    tx_application_define(void *first_unused_memory)
{

UINT    status;

    /* Setup the working pointer. */
    pointer =  (CHAR *) first_unused_memory;

    /* Create the Client thread. */
    status = tx_thread_create(&thread_client, "Client thread", thread_client_entry, 0,
                              pointer, DEMO_STACK_SIZE, 8, 8, TX_NO_TIME_SLICE, TX_AUTO_START);

    /* Check for IP create errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    pointer =  pointer + DEMO_STACK_SIZE;

    /* Initialize the NetX system. */
    nx_system_initialize();

    /* Create a packet pool. */
    status =  nx_packet_pool_create(&pool_0, "NetX Main Packet Pool", 1024,  pointer, PACKET_POOL_SIZE);

    pointer = pointer + PACKET_POOL_SIZE;

    /* Check for pool creation error. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Create a Client IP instance. */
    status = nx_ip_create(&client_ip, "Client IP", IP_ADDRESS(0, 0, 0, 0),
                          0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                          pointer, 2048, 1);

    pointer =  pointer + 2048;

    /* Check for IP create errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Enable UDP traffic for sending DHCPv6 messages. */
    status =  nx_udp_enable(&client_ip);

    /* Check for UDP enable errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Enable ICMP. */
    status =  nx_icmp_enable(&client_ip);

    /* Check for ICMP enable errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Create the DHCPv6 Client. */
    status =  nx_dhcpv6_client_create(&dhcp_client, &client_ip, "DHCPv6 Client",
                                      &pool_0, pointer, 2048, dhcpv6_state_change_notify,
                                      dhcpv6_server_error_handler);

    /* Check for errors. */
    if (status)
    {
        error_counter++;
        return;
    }

    /* Update the stack pointer because we need it again. */
    pointer = pointer + 2048;

    /* Yield control to DHCPv6 threads and ThreadX. */
    return;
}


/* Define the Client host application thread. */

void    thread_client_entry(ULONG thread_input)
{

UINT        status;
ULONG       T1, T2;
UINT        address_count;
UINT        address_index = 0;
NXD_ADDRESS valid_ipv6_address;
ULONG       preferred_lifetime;
ULONG       valid_lifetime;
UINT        ia_count = 1;

#ifdef NX_DHCPV6_REQUEST_IA_ADDRESS
NXD_ADDRESS ipv6_address;
#endif

#ifdef NX_DHCPV6_REQUEST_OPTION
UCHAR       buffer[200];
NXD_ADDRESS dns_server;
#endif

#ifdef NX_DHCPV6_CLIENT_RESTORE_STATE
ULONG       current_time;
ULONG       elapsed_time;
NX_DHCPV6_CLIENT_RECORD dhcpv6_client_record;
#endif


    state_changes = 0;

    /* Establish the link local address for the host. The RAM driver creates
       a virtual MAC address of 0x1122334456. */
    status = nxd_ipv6_address_set(&client_ip, 0, NX_NULL, 10, NULL);

    if (status)
    {
        error_counter++;
        return;
    }

    /* Let NetX Duo get initialized. */
    tx_thread_sleep(50);

    /* Enable the Client IP for IPv6 and ICMPv6 services. */
    nxd_ipv6_enable(&client_ip);
    nxd_icmp_enable(&client_ip);

    /* Create a Link Layer Plus Time DUID for the DHCPv6 Client. Set time ID field
       to NULL; the DHCPv6 Client API will supply one. */
    status = nx_dhcpv6_create_client_duid(&dhcp_client, NX_DHCPV6_DUID_TYPE_LINK_TIME,
                                          NX_DHCPV6_HW_TYPE_IEEE_802, 0);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* Create the DHCPv6 client's Identity Association (IA-NA) now.

       Note that if this host had already been assigned in IPv6 lease, it
       would have to use the assigned T1 and T2 values in loading the DHCPv6
       client with an IANA block.
    */
    status = nx_dhcpv6_create_client_iana(&dhcp_client, DHCPV6_IANA_ID, DHCPV6_T1,  DHCPV6_T2);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

#ifdef NX_DHCPV6_REQUEST_IA_ADDRESS
    memset(&ipv6_address,0x0, sizeof(NXD_ADDRESS));
    ipv6_address.nxd_ip_version = NX_IP_VERSION_V6;
    ipv6_address.nxd_ip_address.v6[0] = 0x3ffe0501;
    ipv6_address.nxd_ip_address.v6[1] = 0xffff0100;
    ipv6_address.nxd_ip_address.v6[2] = 0x00000000;
    ipv6_address.nxd_ip_address.v6[3] = 0x0000abcd;

    /* Create an IA address option.
        Note that if this host had already been assigned in IPv6 lease, it
        would have to use the assigned IPv6 address, preferred and valid lifetime
        values in loading the DHCPv6 Client with an IA block.
    */
    status = nx_dhcpv6_add_client_ia(&dhcp_client, &ipv6_address,DHCPV6_RENEW_TIME, DHCPV6_REBIND_TIME);

    if (status != NX_SUCCESS)
    {
        error_counter++;
        return;
    }

    /* If the DHCPv6 Client is configured for a maximum number of IA addresses
       greater than 1, we can add another IA address if the device requires
       multiple global IPv6 addresses. */
    if(NX_DHCPV6_MAX_IA_ADDRESS >= 2)
    {
        memset(&ipv6_address,0x0, sizeof(NXD_ADDRESS));
        ipv6_address.nxd_ip_version = NX_IP_VERSION_V6;
        ipv6_address.nxd_ip_address.v6[0] = 0x3ffe0501;
        ipv6_address.nxd_ip_address.v6[1] = 0xffff0100;
        ipv6_address.nxd_ip_address.v6[2] = 0x00000000;
        ipv6_address.nxd_ip_address.v6[3] = 0x00001234;

        /* Add another  IA address option. */
        status = nx_dhcpv6_add_client_ia(&dhcp_client, &ipv6_address, DHCPV6_RENEW_TIME, DHCPV6_REBIND_TIME);

        if (status != NX_SUCCESS)
        {
            error_counter++;
            return;
        }
    }
#endif /* NX_DHCPV6_REQUEST_IA_ADDRESS  */

#ifdef NX_DHCPV6_REQUEST_OPTION
    /* Set the list of DHCPv6 option data to get from the DHCPv6 server if needed. */
    nx_dhcpv6_request_option_timezone(&dhcp_client, NX_TRUE);
    nx_dhcpv6_request_option_DNS_server(&dhcp_client, NX_TRUE);
    nx_dhcpv6_request_option_time_server(&dhcp_client, NX_TRUE);
    nx_dhcpv6_request_option_domain_name(&dhcp_client, NX_TRUE);
#endif /* NX_DHCPV6_REQUEST_OPTION */


#ifdef NX_DHCPV6_REQUEST_FQDN_OPTION
    /* Set the DHCPv6 Client FQDN option.
       operation: NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR         DHCPv6 Client choose to updating the FQDN-to-IPv6 address mapping for FQDN and address(es) used by the client.
                  NX_DHCPV6_CLIENT_DESIRES_SERVER_DO_DNS_UPDATE   DHCPv6 Client choose to updating the FQDN-to-IPv6 address mapping for FQDN and address(es) used by the client to the server.
                  NX_DHCPV6_CLIENT_DESIRES_NO_SERVER_DNS_UPDATE   DHCPv6 Client choose to request that the server perform no DNS updatest on its behalf. */
    nx_dhcpv6_request_option_FQDN(&dhcp_client, "DHCPv6-Client", NX_DHCPV6_CLIENT_DESIRES_UPDATE_AAAA_RR);
#endif /* NX_DHCPV6_REQUEST_FQDN_OPTION */

    /* Start up the NetX DHCPv6 Client thread task. */
    status =  nx_dhcpv6_start(&dhcp_client);

    /* Check for errors. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Start the DHCPv6 by sending a Solicit message out on the network. */
    status = nx_dhcpv6_request_solicit(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Is the DHCPv6 Client request for address assignment successfully started? */
    if (status == NX_SUCCESS)
    {

        /* If Duplicate Address Detection (DAD) is enabled in NetX Duo, e.g. #NXDUO_DISABLE_DAD
           not defined, allow time for NetX Duo to verify the address is unique on our network.
         */
        tx_thread_sleep(500);

        /* Check the bound address. */
        if (bound_addresses != ia_count)
        {

            /* Attempt to find out why DHCPv6 failed, where...*/

            if (server_errors > 0)
            {
                /* Actually you would compare server_error count with number of IA's added
                   to determine if any addresses were assigned. */
                printf("Server error, not all address assigned\n");
            }

            if (address_not_assigned > 0)
            {
                /* Actually you would compare address not assigned count with number of IA's added
                   to determine if any addresses were assigned. */

                printf("No servers responded to some or all of our IAs\n");
            }

        }

        /* Regardless if the DHCPv6 Client achieved a bound state, check for DAD
           failures. */
        if (address_failed_dad > 0)
        {
            /* Actually you would compare failed dad count with number of IA's added
               to determine if any addresses were assigned. */

            printf("Some or all of our IAs failed DAD\n");

        }

        /* Successfully assigned IPv6 addresses! */

        /* Get the count of valid IPv6 address obtained by DHCPv6. */
        status = nx_dhcpv6_get_valid_ip_address_count(&dhcp_client, &address_count);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Get the IPv6 address and related lifetimes by address index. This index is the
           index into the DHCPv6 Client address table. Not to be confused with the IP
           instance address table! */
        status = nx_dhcpv6_get_valid_ip_address_lease_time(&dhcp_client, address_index,
                                                           &valid_ipv6_address, 
                                                               &preferred_lifetime,
                                                           &valid_lifetime);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Get the IANA options for when to start renew/rebind requests. These time
           parameters are the same for all IPv6 addresses assigned in the Client
           e.g. IANA returned from Server. */
        status = nx_dhcpv6_get_iana_lease_time(&dhcp_client, &T1, &T2);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /*****************************************************************************/
        /* These are 'legacy' DHCPv6 services and are for the most part identical to the services
           above except they default to the primary global IPv6 address regardless if the
           Client was assigned more than one global IPv6 address. */

        /* Now check the assigned lease times. */
        status = nx_dhcpv6_get_lease_time_data(&dhcp_client, &T1, &T2,
                                               &preferred_lifetime, &valid_lifetime);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Get the IP address. */
        status = nx_dhcpv6_get_IP_address(&dhcp_client, &valid_ipv6_address);

        /* Check status. */
        if (status != NX_SUCCESS)
        {
            error_counter++;
        }

        /* Bound state. */

#ifdef NX_DHCPV6_CLIENT_RESTORE_STATE

        /* Get the DHCPv6 Client record. */
        nx_dhcpv6_client_get_record(&dhcp_client, &dhcpv6_client_record);

        /* Delete DHCPv6 instance. */
        nx_dhcpv6_client_delete(&dhcp_client);

        /* Delete IP instance. */
        status = nx_ip_delete(&client_ip);

        /* Check for error. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Create a Client IP instance. */
        status = nx_ip_create(&client_ip, "Client IP", IP_ADDRESS(0, 0, 0, 0),
                              0xFFFFFF00UL, &pool_0, _nx_ram_network_driver,
                              pointer, 2048, 1);

        pointer =  pointer + 2048;

        /* Check for IP create errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Enable UDP traffic for sending DHCPv6 messages. */
        status =  nx_udp_enable(&client_ip);

        /* Check for UDP enable errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Enable ICMP. */
        status =  nx_icmp_enable(&client_ip);

        /* Check for ICMP enable errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Enable the Client IP for IPv6 and ICMPv6 services. */
        status = nxd_ipv6_enable(&client_ip);
        status += nxd_icmp_enable(&client_ip);

        /* Check for IPv6 and ICMPv6 enable errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Establish the link local address for the host. The RAM driver creates
           a virtual MAC address of 0x1122334456. */
        status = nxd_ipv6_address_set(&client_ip, 0, NX_NULL, 10, NULL);

        if (status)
        {
            error_counter++;
            return;
        }

        /* If Duplicate Address Detection (DAD) is enabled in NetX Duo, e.g. #NXDUO_DISABLE_DAD
           not defined, allow time for NetX Duo to verify the address is unique on our network.
         */
        tx_thread_sleep(500);

        /* Create the DHCPv6 Client. */
        status =  nx_dhcpv6_client_create(&dhcp_client, &client_ip, "DHCPv6 Client",
                                          &pool_0, pointer, 2048, dhcpv6_state_change_notify,
                                          dhcpv6_server_error_handler);

        /* Check for errors. */
        if (status)
        {
            error_counter++;
            return;
        }

        /* Update the stack pointer because we need it again. */
        pointer = pointer + 2048;

        /* Restore the DHCPv6 record. */
        nx_dhcpv6_client_restore_record(&dhcp_client, &dhcpv6_client_record, 5);

        /* Resume the DHCPv6 service. */
        nx_dhcpv6_resume(&dhcp_client);
#endif


#ifdef NX_DHCPV6_REQUEST_OPTION

        /* Get the DNS Server address. */
        nx_dhcpv6_get_DNS_server_address(&dhcp_client, 0, &dns_server);

        /* Get the domain name. */
        memset(buffer, 0, sizeof(buffer));

        nx_dhcpv6_get_other_option_data(&dhcp_client, NX_DHCPV6_DOMAIN_NAME_OPTION, buffer, 200); // Try to get DNS info got from DHCPv6 Server

        /* Get the domain name. */
        memset(buffer, 0, sizeof(buffer));

        /* Get the time zone. */
        nx_dhcpv6_get_other_option_data(&dhcp_client, NX_DHCPV6_NEW_POSIX_TIMEZONE_OPTION, buffer, 200); // Try to get DNS info got from DHCPv6 Server
#endif

        /* At some point, we may wish to release the IPv6 address lease e.g. the device
           is leaving the network or powering down. In that case we inform the
           DHCPv6 Server that we are releasing the address lease. */
        status = nx_dhcpv6_request_release(&dhcp_client);

        /* Check status. */
        if (status != NX_SUCCESS)
        {

            error_counter++;
            return;
        }

        /* Send the release message. */
        tx_thread_sleep(100);
    }

    /* Stopping the Client task. */
    status = nx_dhcpv6_stop(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Clear the previously assigned IPv6 addresses from the Client and IP address table. */
    status = nx_dhcpv6_reinitialize(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Start up the Client task again. */
    status = nx_dhcpv6_start(&dhcp_client);

    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Begin the request process by sending a Solicit message with the IA created above
       with our preferred IPv6 address. */
    status = nx_dhcpv6_request_solicit(&dhcp_client);
    /* Check status. */
    if (status != NX_SUCCESS)
    {

        error_counter++;
        return;
    }

    /* Wait a bit before releasing the IP address and terminating the client. */
    tx_thread_sleep(500);

    /* Ok, lets stop the application. Again we DO NOT plan
       to keep the IPv6 address we were assigned and need to release it
       back to the DHCPv6 server. */
    status = nx_dhcpv6_request_release(&dhcp_client);

    /* Check for error. */
    if (status != NX_SUCCESS)
    {
        error_counter++;
    }

    /* Now delete the DHCPv6 client and release ThreadX and
       NetX Duo resources back to the system. */
    nx_dhcpv6_client_delete(&dhcp_client);


    return;

}


/* This is the notification from the DHCPv6 Client task that it has changed
   state in the DHCPv6 protocol, for example getting assigned an IPv6 lease and
   achieving the bound state or an IPv6 lease expires and being reset to
   the init state.
*/
VOID dhcpv6_state_change_notify(NX_DHCPV6 *dhcpv6_ptr, UINT old_state, UINT new_state)
{


    /* Increment state change counter. */
    state_changes++;

    /* Check if the Client attempted to request an IPv6 lease but no servers
       responded. */
    if ((old_state == NX_DHCPV6_STATE_SENDING_SOLICIT) && (new_state == NX_DHCPV6_STATE_INIT))
    {

        /* Indication that either DAD failed or IP lease expired. */
        address_not_assigned++;
    }

    /* Check if the Client has been assigned an IPv6 lease. */
    if (new_state == NX_DHCPV6_STATE_BOUND_TO_ADDRESS)
    {
        bound_addresses++;
    }

   /* Check if the Client was bound, but failed the uniqueness check
       (Duplicate Address Detection) and was reset to the INIT state. */
    if ((old_state == NX_DHCPV6_STATE_SENDING_DECLINE) && (new_state == NX_DHCPV6_STATE_INIT))
    {

        /* Indication that DAD failed on Client IA. */
        address_failed_dad++;
    }

    /* Check if the Client was bound, attempted renew the lease but the
       IPv6 address renewal/rebinding failed. */
    if ((old_state == NX_DHCPV6_STATE_SENDING_REBIND) && (new_state == NX_DHCPV6_STATE_INIT))
    {

        /* Indication that the IP lease expired. */
        address_expired++;
    }



    /* Other checks are possible. */

}

/* This is the notification from the DHCPv6 Client task that it received an error
   from the server (status code) in response to the Client's last DHCPv6 message.
*/

VOID dhcpv6_server_error_handler(NX_DHCPV6 *dhcpv6_ptr, UINT op_code, UINT status_code, UINT message_type)
{

    /* Increment the server error count. */
    server_errors++;

    /* This should distinguish between receiving a server error and no server
       available to assign the Client an IPv6 address if the Client fails
       to get assigned an address. */
}

#endif /* FEATURE_NX_IPV6 */
```
