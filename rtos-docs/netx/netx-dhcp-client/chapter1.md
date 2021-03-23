---
title: Capitolo 1-Introduzione ad Azure RTO NetX client DHCP
description: In NetX, l'indirizzo IP dell'applicazione è uno dei parametri specificati per la chiamata al servizio nx_ip_create.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 44eb764c84a15a1bc96cf94bcbc8f81be7b41eef
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822709"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-dhcp-client"></a><span data-ttu-id="71191-103">Capitolo 1-Introduzione ad Azure RTO NetX client DHCP</span><span class="sxs-lookup"><span data-stu-id="71191-103">Chapter 1 - Introduction to Azure RTOS NetX DHCP Client</span></span>

<span data-ttu-id="71191-104">In NetX, l'indirizzo IP dell'applicazione è uno dei parametri specificati per la chiamata al servizio *nx_ip_create* .</span><span class="sxs-lookup"><span data-stu-id="71191-104">In NetX, the application’s IP address is one of the supplied parameters to the *nx_ip_create* service call.</span></span> <span data-ttu-id="71191-105">La fornitura dell'indirizzo IP non costituisce un problema se l'indirizzo IP è noto all'applicazione, in modo statico o tramite la configurazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="71191-105">Supplying the IP address poses no problem if the IP address is known to the application, either statically or through user configuration.</span></span> <span data-ttu-id="71191-106">Tuttavia, esistono alcuni casi in cui l'applicazione non è in grado di conoscere il proprio indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="71191-106">However, there are some instances where the application doesn’t know or care what its IP address is.</span></span> <span data-ttu-id="71191-107">In tali situazioni, è necessario specificare un indirizzo IP zero per la funzione *nx_ip_create* e usare il protocollo client DHCP di Azure RTO per ottenere dinamicamente un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="71191-107">In such situations, a zero IP address should be supplied to the *nx_ip_create* function and the Azure RTOS DHCP Client protocol should be used to dynamically obtain an IP address.</span></span>

## <a name="dynamic-ip-address-assignment"></a><span data-ttu-id="71191-108">Assegnazione di indirizzi IP dinamici</span><span class="sxs-lookup"><span data-stu-id="71191-108">Dynamic IP Address Assignment</span></span>

<span data-ttu-id="71191-109">Il servizio di base usato per ottenere un indirizzo IP dinamico dalla rete è il protocollo RARP (Reverse Address Resolution Protocol).</span><span class="sxs-lookup"><span data-stu-id="71191-109">The basic service used to obtain a dynamic IP address from the network is the Reverse Address Resolution Protocol (RARP).</span></span> <span data-ttu-id="71191-110">Questo protocollo è simile a ARP, ad eccezione del fatto che è stato progettato per ottenere un indirizzo IP per se stesso anziché per trovare l'indirizzo MAC per un altro nodo di rete.</span><span class="sxs-lookup"><span data-stu-id="71191-110">This protocol is similar to ARP, except it is designed to obtain an IP address for itself instead of finding the MAC address for another network node.</span></span> <span data-ttu-id="71191-111">Il messaggio RARP di basso livello viene trasmesso sulla rete locale ed è responsabilità di un server nella rete rispondere con una risposta RARP, che contiene un indirizzo IP allocato dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="71191-111">The low-level RARP message is broadcast on the local network and it is the responsibility of a server on the network to respond with an RARP response, which contains a dynamically allocated IP address.</span></span>

<span data-ttu-id="71191-112">Sebbene RARP fornisca un servizio per l'allocazione dinamica di indirizzi IP, presenta diversi difetti.</span><span class="sxs-lookup"><span data-stu-id="71191-112">Although RARP provides a service for dynamic allocation of IP addresses, it has several shortcomings.</span></span> <span data-ttu-id="71191-113">Il difetto più evidente è che il RARP fornisce solo l'allocazione dinamica dell'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="71191-113">The most glaring deficiency is that RARP only provides dynamic allocation of the IP address.</span></span> <span data-ttu-id="71191-114">Nella maggior parte dei casi, è necessario disporre di altre informazioni per consentire a un dispositivo di partecipare correttamente a una rete.</span><span class="sxs-lookup"><span data-stu-id="71191-114">In most situations, more information is necessary in order for a device to properly participate on a network.</span></span> <span data-ttu-id="71191-115">Oltre a un indirizzo IP, per la maggior parte dei dispositivi sono necessari il network mask e l'indirizzo IP del gateway.</span><span class="sxs-lookup"><span data-stu-id="71191-115">In addition to an IP address, most devices need the network mask and the gateway IP address.</span></span> <span data-ttu-id="71191-116">Potrebbe essere necessario anche l'indirizzo IP di un server DNS e altre informazioni sulla rete.</span><span class="sxs-lookup"><span data-stu-id="71191-116">The IP address of a DNS server and other network information may also be needed.</span></span> <span data-ttu-id="71191-117">RARP non è in grado di fornire queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="71191-117">RARP does not have the ability to provide this information.</span></span>

## <a name="rarp-alternatives"></a><span data-ttu-id="71191-118">Alternative RARP</span><span class="sxs-lookup"><span data-stu-id="71191-118">RARP Alternatives</span></span>

<span data-ttu-id="71191-119">Per ovviare alle carenze di RARP, i ricercatori hanno sviluppato un meccanismo di allocazione indirizzi IP più completo denominato BOOTP (Bootstrap Protocol).</span><span class="sxs-lookup"><span data-stu-id="71191-119">In order to overcome the deficiencies of RARP, researchers developed a more comprehensive IP address allocation mechanism called the Bootstrap Protocol (BOOTP).</span></span> <span data-ttu-id="71191-120">Questo protocollo è in grado di allocare dinamicamente un indirizzo IP e di fornire altre informazioni importanti sulla rete.</span><span class="sxs-lookup"><span data-stu-id="71191-120">This protocol has the ability to dynamically allocate an IP address and also provide additional important network information.</span></span> <span data-ttu-id="71191-121">Tuttavia, BOOTP presenta lo svantaggio di essere progettato per le configurazioni di rete statiche.</span><span class="sxs-lookup"><span data-stu-id="71191-121">However, BOOTP has the drawback of being designed for static network configurations.</span></span> <span data-ttu-id="71191-122">Non consente l'assegnazione di indirizzi rapidi o automatici.</span><span class="sxs-lookup"><span data-stu-id="71191-122">It does not allow for quick or automated address assignment.</span></span>

<span data-ttu-id="71191-123">Questo è il punto in cui il Dynamic Host Configuration Protocol (DHCP) è estremamente utile.</span><span class="sxs-lookup"><span data-stu-id="71191-123">This is where the Dynamic Host Configuration Protocol (DHCP) is extremely useful.</span></span> <span data-ttu-id="71191-124">DHCP è progettato per estendere le funzionalità di base di BOOTP per includere l'allocazione del server IP completamente automatizzata e l'allocazione di indirizzi IP completamente dinamica tramite il "leasing" di un indirizzo IP a un client per un periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="71191-124">DHCP is designed to extend the basic functionality of BOOTP to include completely automated IP server allocation and completely dynamic IP address allocation through “leasing” an IP address to a client for a specified period of time.</span></span> <span data-ttu-id="71191-125">DHCP può inoltre essere configurato in modo da allocare gli indirizzi IP in modo statico, ad esempio BOOTP.</span><span class="sxs-lookup"><span data-stu-id="71191-125">DHCP can also be configured to allocate IP addresses in a static manner like BOOTP.</span></span>

## <a name="dhcp-messages"></a><span data-ttu-id="71191-126">Messaggi DHCP</span><span class="sxs-lookup"><span data-stu-id="71191-126">DHCP Messages</span></span>

<span data-ttu-id="71191-127">Sebbene DHCP migliori significativamente la funzionalità di BOOTP, DHCP usa lo stesso formato di messaggio BOOTP e supporta le stesse opzioni del fornitore di BOOTP.</span><span class="sxs-lookup"><span data-stu-id="71191-127">Although DHCP greatly enhances the functionality of BOOTP, DHCP uses the same message format as BOOTP and supports the same vendor options as BOOTP.</span></span> <span data-ttu-id="71191-128">Per eseguire la funzione, DHCP introduce sette nuove opzioni specifiche di DHCP, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="71191-128">In order to perform its function, DHCP introduces seven new DHCP-specific options, as follows:</span></span>

- <span data-ttu-id="71191-129">DISCOVER (1) (inviato dal client DHCP)</span><span class="sxs-lookup"><span data-stu-id="71191-129">DISCOVER (1) (sent by DHCP Client)</span></span>

- <span data-ttu-id="71191-130">OFFERTA (2) (inviata dal server DHCP)</span><span class="sxs-lookup"><span data-stu-id="71191-130">OFFER (2) (sent by DHCP Server)</span></span>

- <span data-ttu-id="71191-131">REQUEST (3) (inviato dal client DHCP)</span><span class="sxs-lookup"><span data-stu-id="71191-131">REQUEST (3) (sent by DHCP Client)</span></span>

- <span data-ttu-id="71191-132">RIFIUTARE (4) (inviato dal client DHCP)</span><span class="sxs-lookup"><span data-stu-id="71191-132">DECLINE (4) (sent by DHCP Client)</span></span>

- <span data-ttu-id="71191-133">ACK (5) (inviato dal server DHCP)</span><span class="sxs-lookup"><span data-stu-id="71191-133">ACK (5) (sent by DHCP Server)</span></span>

- <span data-ttu-id="71191-134">NACK (6) (inviato dal server DHCP)</span><span class="sxs-lookup"><span data-stu-id="71191-134">NACK (6) (sent by DHCP Server)</span></span>

- <span data-ttu-id="71191-135">VERSIONE (7) (inviata dal client DHCP)</span><span class="sxs-lookup"><span data-stu-id="71191-135">RELEASE (7) (sent by DHCP Client)</span></span>

- <span data-ttu-id="71191-136">INFORMA (8) (inviato dal client DHCP)</span><span class="sxs-lookup"><span data-stu-id="71191-136">INFORM (8) (sent by DHCP Client)</span></span>

- <span data-ttu-id="71191-137">FORCERENEW (9) (inviato dal client DHCP)</span><span class="sxs-lookup"><span data-stu-id="71191-137">FORCERENEW (9) (sent by DHCP Client)</span></span>

## <a name="dhcp-communication"></a><span data-ttu-id="71191-138">Comunicazione DHCP</span><span class="sxs-lookup"><span data-stu-id="71191-138">DHCP Communication</span></span>

<span data-ttu-id="71191-139">DHCP utilizza il protocollo UDP per inviare richieste e risposte di campo.</span><span class="sxs-lookup"><span data-stu-id="71191-139">DHCP utilizes the UDP protocol to send requests and field responses.</span></span> <span data-ttu-id="71191-140">Prima di avere un indirizzo IP, i messaggi UDP che contengono le informazioni DHCP vengono inviati e ricevuti tramite l'indirizzo di trasmissione IP di 255.255.255.255.</span><span class="sxs-lookup"><span data-stu-id="71191-140">Prior to having an IP address, UDP messages carrying the DHCP information are sent and received by utilizing the IP broadcast address of 255.255.255.255.</span></span>

## <a name="dhcp-client-state-machine"></a><span data-ttu-id="71191-141">Macchina a stati client DHCP</span><span class="sxs-lookup"><span data-stu-id="71191-141">DHCP Client State Machine</span></span>

<span data-ttu-id="71191-142">Il client DHCP viene implementato come macchina a Stati.</span><span class="sxs-lookup"><span data-stu-id="71191-142">The DHCP Client is implemented as a state machine.</span></span> <span data-ttu-id="71191-143">La macchina a stati viene elaborata da un thread DHCP interno creato durante *nx_dhcp_create* elaborazione.</span><span class="sxs-lookup"><span data-stu-id="71191-143">The state machine is processed by an internal DHCP thread that is created during *nx_dhcp_create* processing.</span></span> <span data-ttu-id="71191-144">Gli stati principali del client DHCP sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="71191-144">The main states of DHCP Client are as follows:</span></span>


- <span data-ttu-id="71191-145">**NX_DHCP_STATE_BOOT** A partire da un indirizzo IP precedente</span><span class="sxs-lookup"><span data-stu-id="71191-145">**NX_DHCP_STATE_BOOT** Starting with a previous IP address</span></span>

- <span data-ttu-id="71191-146">**NX_DHCP_STATE_INIT** A partire da nessun valore dell'indirizzo IP precedente</span><span class="sxs-lookup"><span data-stu-id="71191-146">**NX_DHCP_STATE_INIT** Starting with no previous   IP address value</span></span>

- <span data-ttu-id="71191-147">**NX_DHCP_STATE_SELECTING** In attesa di una risposta da un server DHCP</span><span class="sxs-lookup"><span data-stu-id="71191-147">**NX_DHCP_STATE_SELECTING** Waiting for a response from any DHCP server</span></span>

- <span data-ttu-id="71191-148">**NX_DHCP_STATE_REQUESTING** Server DHCP identificato, richiesta indirizzo IP inviata</span><span class="sxs-lookup"><span data-stu-id="71191-148">**NX_DHCP_STATE_REQUESTING** DHCP Server identified, IP address request sent</span></span>

- <span data-ttu-id="71191-149">**NX_DHCP_STATE_BOUND** Lease indirizzi IP DHCP stabilito</span><span class="sxs-lookup"><span data-stu-id="71191-149">**NX_DHCP_STATE_BOUND** DHCP IP Address lease established</span></span>

- <span data-ttu-id="71191-150">**NX_DHCP_STATE_RENEWING** Tempo di rinnovo del lease di indirizzi IP DHCP scaduto, rinnovo richiesto</span><span class="sxs-lookup"><span data-stu-id="71191-150">**NX_DHCP_STATE_RENEWING** DHCP IP Address lease renewal time elapsed, renewal requested</span></span>

- <span data-ttu-id="71191-151">**NX_DHCP_STATE_REBINDING** Tempo di riassociazione lease indirizzi IP DHCP scaduto, rinnovo richiesto</span><span class="sxs-lookup"><span data-stu-id="71191-151">**NX_DHCP_STATE_REBINDING** DHCP IP Address lease rebind time elapsed, renewal requested</span></span>

- <span data-ttu-id="71191-152">**NX_DHCP_STATE_FORCERENEW** Lease di indirizzi IP DHCP stabilito, forzare il rinnovo dal server (attualmente non supportato) o dall'applicazione che chiama nx_dhcp_force_renew</span><span class="sxs-lookup"><span data-stu-id="71191-152">**NX_DHCP_STATE_FORCERENEW** DHCP IP Address lease established, force renewal by server (currently not supported) or by the application calling nx_dhcp_force_renew</span></span>

- <span data-ttu-id="71191-153">**NX_DHCP_STATE_ADDRESS_PROBING** Sondaggio di indirizzi IP DHCP, inviare il probe ARP per rilevare il conflitto di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="71191-153">**NX_DHCP_STATE_ADDRESS_PROBING** DHCP IP Address probing, send the ARP probe to detect IP address conflict.</span></span>

## <a name="dhcp-client-multiple-interface-support"></a><span data-ttu-id="71191-154">Supporto per più interfacce del client DHCP</span><span class="sxs-lookup"><span data-stu-id="71191-154">DHCP Client Multiple Interface Support</span></span>

<span data-ttu-id="71191-155">Il client DHCP è stato precedentemente implementato per l'esecuzione su una sola interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="71191-155">The DHCP Client was previously implemented to run on only a single network interface.</span></span> <span data-ttu-id="71191-156">Il comportamento predefinito era (ed è ancora) per l'esecuzione del client DHCP sull'interfaccia primaria.</span><span class="sxs-lookup"><span data-stu-id="71191-156">The default behavior was (and still is) for the DHCP Client to run on the primary interface.</span></span> <span data-ttu-id="71191-157">Chiamando *nx_dhcp_set_interface_index*, l'applicazione può (e ancora possibile) eseguire DHCP su un'interfaccia di rete secondaria anziché sull'interfaccia primaria.</span><span class="sxs-lookup"><span data-stu-id="71191-157">By calling *nx_dhcp_set_interface_index*, the application could (and still can) run DHCP on a secondary network interface instead of the primary interface.</span></span>

<span data-ttu-id="71191-158">Supporta ora DHCP in esecuzione su più interfacce in parallelo.</span><span class="sxs-lookup"><span data-stu-id="71191-158">It now supports DHCP running on multiple interfaces in parallel.</span></span> <span data-ttu-id="71191-159">Vedere **il client DHCP su più interfacce simultaneamente** nel capitolo due per informazioni dettagliate su come eseguire simultaneamente il client DHCP in più di un'interfaccia fisica.</span><span class="sxs-lookup"><span data-stu-id="71191-159">See **DHCP Client on Multiple Interfaces Simultaneously** in Chapter Two for specific details how to run DHCP Client on more than one physical interface simultaneously.</span></span>

## <a name="dhcp-user-request"></a><span data-ttu-id="71191-160">Richiesta utente DHCP</span><span class="sxs-lookup"><span data-stu-id="71191-160">DHCP User Request</span></span>

<span data-ttu-id="71191-161">Una volta che il server DHCP concede un indirizzo IP, l'elaborazione del client DHCP può richiedere parametri aggiuntivi, uno alla volta, usando il servizio *nx_dhcp_user_option_request* .</span><span class="sxs-lookup"><span data-stu-id="71191-161">Once the DHCP server grants an IP address, the DHCP client processing can request additional parameters — one at a time — by using the *nx_dhcp_user_option_request* service.</span></span>

## <a name="dhcp-client-socket-queue"></a><span data-ttu-id="71191-162">Coda socket client DHCP</span><span class="sxs-lookup"><span data-stu-id="71191-162">DHCP Client Socket Queue</span></span> 

<span data-ttu-id="71191-163">Il client DHCP cancella automaticamente i pacchetti broadcast dai server DHCP destinati ad altri client DHCP dalla coda di ricezione del socket in attesa che il server risponda a se stesso.</span><span class="sxs-lookup"><span data-stu-id="71191-163">The DHCP Client automatically clears broadcast packets from DHCP Servers intended for other DHCP Clients from its socket receive queue while waiting for Server to respond to itself.</span></span> <span data-ttu-id="71191-164">In una rete occupata, questa operazione potrebbe causare l'eliminazione dei pacchetti destinati al client.</span><span class="sxs-lookup"><span data-stu-id="71191-164">In a busy network, not doing so could cause packets intended for the Client to be dropped.</span></span>

## <a name="dhcp-rfcs"></a><span data-ttu-id="71191-165">RFC DHCP</span><span class="sxs-lookup"><span data-stu-id="71191-165">DHCP RFCs</span></span>

<span data-ttu-id="71191-166">NetX DHCP è conforme a RFC2132, RFC2131 e RFC correlati.</span><span class="sxs-lookup"><span data-stu-id="71191-166">NetX DHCP is compliant with RFC2132, RFC2131, and related RFCs.</span></span>

