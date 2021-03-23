---
title: Informazioni su Azure RTO NetX
description: Azure RTO NetX è un'implementazione ad alte prestazioni di standard di protocollo TCP/IP, completamente integrato con Azure RTO ThreadX e disponibile per tutti i processori supportati.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 029f73b755d5c40279125fb010ec35baaaf7f38d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104821488"
---
# <a name="overview-of-azure-rtos-netx"></a><span data-ttu-id="2fd82-103">Panoramica di Azure RTO NetX</span><span class="sxs-lookup"><span data-stu-id="2fd82-103">Overview of Azure RTOS NetX</span></span>

<span data-ttu-id="2fd82-104">Azure RTO NetX è uno stack di rete incorporato TCP/IP IPv4 di livello industriale, progettato in modo specifico per applicazioni incorporate, in tempo reale e in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="2fd82-104">Azure RTOS NetX is an industrial grade TCP/IP IPv4 embedded network stack, designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="2fd82-105">Azure RTO NetX è lo stack di rete IPv4 originale di Microsoft ed è essenzialmente un subset di RTO di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd82-105">Azure RTOS NetX is Microsoft's original IPv4 network stack, and is essentially a subset of Azure RTOS.</span></span> <span data-ttu-id="2fd82-106">NetX fornisce applicazioni incorporate con protocolli di rete principali, ad esempio IPv4, TCP e UDP, nonché una suite completa di protocolli aggiuntivi di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="2fd82-106">NetX provides embedded applications with core network protocols such as IPv4, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="2fd82-107">Un footprint ridotto, un'esecuzione rapida e una semplicità di utilizzo superiore rendono Azure RTO NetX la scelta ideale per le applicazioni di Internet delle cose più complesse.</span><span class="sxs-lookup"><span data-stu-id="2fd82-107">A small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX an ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="2fd82-108">Protocolli API</span><span class="sxs-lookup"><span data-stu-id="2fd82-108">API protocols</span></span>

### <a name="telnet"></a><span data-ttu-id="2fd82-109">TELNET</span><span class="sxs-lookup"><span data-stu-id="2fd82-109">TELNET</span></span>

* <span data-ttu-id="2fd82-110">Ingombro minimo 0,5 KB e 0,3 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-110">Minimal 0.5 KB and 0.3 KB RAM footprint</span></span>
* <span data-ttu-id="2fd82-111">Supporto per client e server</span><span class="sxs-lookup"><span data-stu-id="2fd82-111">Client and server support</span></span>
* <span data-ttu-id="2fd82-112">API Telnet intuitive *: \* nx_telnet_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-112">Intuitive Telnet APIs: *nx_telnet_\**</span></span>

### <a name="auto-ip"></a><span data-ttu-id="2fd82-113">IP automatico</span><span class="sxs-lookup"><span data-stu-id="2fd82-113">Auto IP</span></span>

* <span data-ttu-id="2fd82-114">Assegnazione automatica di indirizzi IPv4</span><span class="sxs-lookup"><span data-stu-id="2fd82-114">Automatic IPv4 address assignment</span></span>
* <span data-ttu-id="2fd82-115">Minimo 1,2 KB, 300 byte di RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-115">Minimal 1.2 KB, 300 bytes of RAM</span></span>
* <span data-ttu-id="2fd82-116">API AutoIP intuitive *: \* nx_autoip_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-116">Intuitive AutoIP APIs: *nx_autoip_\**</span></span>

### <a name="http---hypertext-transfer-protocolhttp"></a><span data-ttu-id="2fd82-117">HTTP-Hypertext Transfer Protocol (HTTP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-117">HTTP - Hypertext Transfer Protocol(HTTP)</span></span>

* <span data-ttu-id="2fd82-118">Minimo 2,8 KB a 4.8 KBFLASH, da 0,4 KB a 1,0 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-118">Minimal 2.8 KB to 4.8KBFLASH, 0.4 KB to 1.0 KB RAM footprint</span></span>
* <span data-ttu-id="2fd82-119">Supporto per client e server</span><span class="sxs-lookup"><span data-stu-id="2fd82-119">Client and server support</span></span>
* <span data-ttu-id="2fd82-120">API HTTP intuitive *: \* nx_http_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-120">Intuitive HTTP APIs: *nx_http_\**</span></span>

### <a name="smtp---simple-mail-transfer-protocol-smtp"></a><span data-ttu-id="2fd82-121">SMTP-Simple Mail Transfer Protocol (SMTP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-121">SMTP - Simple Mail Transfer Protocol (SMTP)</span></span>

* <span data-ttu-id="2fd82-122">Ingombro minimo 4,1 KB e 0,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-122">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="2fd82-123">Supporto client</span><span class="sxs-lookup"><span data-stu-id="2fd82-123">Client support</span></span>
* <span data-ttu-id="2fd82-124">API SMTP intuitive *: \* nx_smtp_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-124">Intuitive SMTP APIs: *nx_smtp_\**</span></span>

### <a name="dhcp---dynamic-host-configuration-protocol-dhcp"></a><span data-ttu-id="2fd82-125">DHCP-Dynamic Host Configuration Protocol (DHCP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-125">DHCP - Dynamic Host Configuration Protocol (DHCP)</span></span>

* <span data-ttu-id="2fd82-126">Minimo 3,6 KB a 4,6 KB FLASH, 2,7 KB di impronta RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-126">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="2fd82-127">Supporto per client e server</span><span class="sxs-lookup"><span data-stu-id="2fd82-127">Client and server support</span></span>
* <span data-ttu-id="2fd82-128">Supporto per IPv4</span><span class="sxs-lookup"><span data-stu-id="2fd82-128">IPv4 support</span></span>
* <span data-ttu-id="2fd82-129">API DHCP intuitive *: \* nx_dhcp_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-129">Intuitive DHCP APIs: *nx_dhcp_\**</span></span>

### <a name="p0p3---post-office-protocol-version-3-pop3"></a><span data-ttu-id="2fd82-130">P0P3-Post Office Protocol versione 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="2fd82-130">P0P3 - Post Office Protocol Version 3 (POP3)</span></span>

* <span data-ttu-id="2fd82-131">Ingombro minimo 8,1 KB e 1,4 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-131">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="2fd82-132">Supporto client</span><span class="sxs-lookup"><span data-stu-id="2fd82-132">Client support</span></span>
* <span data-ttu-id="2fd82-133">API P0P3 intuitive *: \* nx_pop3_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-133">Intuitive P0P3 APIs: *nx_pop3_\**</span></span>

### <a name="snmp---simple-network-management-protocol-snmp"></a><span data-ttu-id="2fd82-134">SNMP-Simple Network Management Protocol (SNMP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-134">SNMP - Simple Network Management Protocol (SNMP)</span></span>

* <span data-ttu-id="2fd82-135">Ingombro minimo 10,9 KB e 2,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-135">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="2fd82-136">Supporto degli agenti per VI, V2 e V3</span><span class="sxs-lookup"><span data-stu-id="2fd82-136">Agent support for VI, V2, and V3</span></span>
* <span data-ttu-id="2fd82-137">API SNMP intuitive *: \* nx_snmp_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-137">Intuitive SNMP APIs: *nx_snmp_\**</span></span>

### <a name="ftp-tftp---file-transfer-protocol-ftp-trivial-file-transfer-protocol-tftp"></a><span data-ttu-id="2fd82-138">FTP, TFTP-File Transfer Protocol (FTP), Trivial File Transfer Protocol (TFTP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-138">FTP, TFTP - File Transfer Protocol (FTP), Trivial File Transfer Protocol (TFTP)</span></span>

* <span data-ttu-id="2fd82-139">FTP minimo 1,8 KB a 7,2 KBFLASH, da 0,6 KB a 2,1 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-139">FTP Minimal 1.8 KB to 7.2KBFLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="2fd82-140">TFTP minimo 1,7 KB a 2,4 KBFLASH, da 0,3 KB a 1,8 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-140">TFTP Minimal 1.7 KB to 2.4KBFLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="2fd82-141">Supporto per client e server</span><span class="sxs-lookup"><span data-stu-id="2fd82-141">Client and server support</span></span>
* <span data-ttu-id="2fd82-142">API FTP e TFTP intuitive: <i>nx_ftp_ *</i> o <i>nx_tftp_*</i></span><span class="sxs-lookup"><span data-stu-id="2fd82-142">Intuitive FTP and TFTP APIs: <i>nx_ftp_ *</i> or <i>nx_tftp_*</i></span></span>

### <a name="ppp---polnt-to-point-protocol-ppp"></a><span data-ttu-id="2fd82-143">PPP-bravo-to-PoInt Protocol (PPP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-143">PPP - Polnt-to-PoInt Protocol (PPP)</span></span>

* <span data-ttu-id="2fd82-144">Ingombro minimo 7,1 KB e 3,8 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-144">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="2fd82-145">API PPP intuitive *: \* nx_ppp_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-145">Intuitive PPP APIs: *nx_ppp_\**</span></span>

### <a name="sntp---simple-network-time-protocol-sntp"></a><span data-ttu-id="2fd82-146">SNTP-Simple Network Time Protocol (SNTP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-146">SNTP - Simple Network Time Protocol (SNTP)</span></span>

* <span data-ttu-id="2fd82-147">Minimo 4 KB e 0,5 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-147">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="2fd82-148">Supporto client</span><span class="sxs-lookup"><span data-stu-id="2fd82-148">Client support</span></span>
* <span data-ttu-id="2fd82-149">API SNTP intuitive *: \* nx_sntp_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-149">Intuitive SNTP APIs: *nx_sntp_\**</span></span>

### <a name="azure-rtos-netx-api"></a><span data-ttu-id="2fd82-150">API NetX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="2fd82-150">Azure RTOS NetX API</span></span>

* <span data-ttu-id="2fd82-151">API intuitiva e coerente</span><span class="sxs-lookup"><span data-stu-id="2fd82-151">Intuitive and consistent API</span></span>
* <span data-ttu-id="2fd82-152">Sostantivo-convenzione di denominazione dei verbi</span><span class="sxs-lookup"><span data-stu-id="2fd82-152">Noun-verb naming convention</span></span>
* <span data-ttu-id="2fd82-153">Implementazione API veloce, copia zero</span><span class="sxs-lookup"><span data-stu-id="2fd82-153">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="2fd82-154">Tutte le funzioni API hanno <i>nx_ \*</i> per identificare facilmente come Azure RTO NETX</span><span class="sxs-lookup"><span data-stu-id="2fd82-154">All API functions have leading <i>nx_\*</i> to easily identify as Azure RTOS NetX</span></span>
* <span data-ttu-id="2fd82-155">Le funzioni API di blocco hanno un timeout thread facoltativo</span><span class="sxs-lookup"><span data-stu-id="2fd82-155">Blocking API functions have an optional thread timeout</span></span>
* <span data-ttu-id="2fd82-156">Livello BSD facoltativo per il porting del codice socket legacy</span><span class="sxs-lookup"><span data-stu-id="2fd82-156">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp---internet-group-management-protocol-igmp"></a><span data-ttu-id="2fd82-157">IGMP (Internet Group Management Protocol)</span><span class="sxs-lookup"><span data-stu-id="2fd82-157">IGMP - Internet Group Management Protocol (IGMP)</span></span>

* <span data-ttu-id="2fd82-158">FLASH minimo 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="2fd82-158">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="2fd82-159">Supporto del gruppo multicast IPv4</span><span class="sxs-lookup"><span data-stu-id="2fd82-159">IPv4 multicast group support</span></span>
* <span data-ttu-id="2fd82-160">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="2fd82-160">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="2fd82-161">Statistiche IGMP facoltative</span><span class="sxs-lookup"><span data-stu-id="2fd82-161">Optional IGMP statistics</span></span>
* <span data-ttu-id="2fd82-162">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="2fd82-162">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="2fd82-163">API IGMP intuitive *: \* nx_igmp_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-163">Intuitive IGMP APIs: *nx_igmp_\**</span></span>

### <a name="udp---user-datagram-protocol-udp"></a><span data-ttu-id="2fd82-164">UDP-User Datagram Protocol (UDP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-164">UDP - User Datagram Protocol (UDP)</span></span>

* <span data-ttu-id="2fd82-165">Minimo 2,5 KB di FLASH, 124 socket byte di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="2fd82-165">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="2fd82-166">Elaborazione di pacchetti TCP veloce, near wirespeed:</span><span class="sxs-lookup"><span data-stu-id="2fd82-166">Fast, near wirespeed TCP packet processing:</span></span>
* <span data-ttu-id="2fd82-167">RX 95 Mbps su Ethernet a 100 Mbps, MCU @100MHz , 14% di utilizzo di MCU</span><span class="sxs-lookup"><span data-stu-id="2fd82-167">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU Utilization</span></span>
* <span data-ttu-id="2fd82-168">TX 94 Mbps a 100 Mbps Ethernet, MCU @100MHz , 10% di utilizzo di MCU</span><span class="sxs-lookup"><span data-stu-id="2fd82-168">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU Utilization</span></span>
* <span data-ttu-id="2fd82-169">Percorso rapido UDP™ tecnologia</span><span class="sxs-lookup"><span data-stu-id="2fd82-169">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="2fd82-170">Nessun limite al numero di UDP</span><span class="sxs-lookup"><span data-stu-id="2fd82-170">No limits on the number of UDP</span></span>
* <span data-ttu-id="2fd82-171">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="2fd82-171">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="2fd82-172">Sospensione facoltativa per ricezione socket</span><span class="sxs-lookup"><span data-stu-id="2fd82-172">Optional suspension on socket receive</span></span>
* <span data-ttu-id="2fd82-173">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="2fd82-173">Optional timeout on all suspension</span></span>
* <span data-ttu-id="2fd82-174">Statistiche UDP facoltative</span><span class="sxs-lookup"><span data-stu-id="2fd82-174">Optional UDP statistics</span></span>
* <span data-ttu-id="2fd82-175">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="2fd82-175">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="2fd82-176">API UDP intuitive *: \* nx_udp_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-176">Intuitive UDP APIs: *nx_udp_\**</span></span>

### <a name="tcp---transmission-control-protocol-tcp"></a><span data-ttu-id="2fd82-177">TCP-Transmission Control Protocol (TCP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-177">TCP - Transmission Control Protocol (TCP)</span></span>

* <span data-ttu-id="2fd82-178">Minimo da 10.5 K8 a 12,5 KB di FLASH, 280 byte di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="2fd82-178">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="2fd82-179">Elaborazione di pacchetti TCP veloce, near wlrespeed:</span><span class="sxs-lookup"><span data-stu-id="2fd82-179">Fast, near wlrespeed TCP packet processing:</span></span>
* <span data-ttu-id="2fd82-180">RX 93 Mbps su Ethernet a 100 Mbps, MCU @100MHz , utilizzo di MCU del 20%</span><span class="sxs-lookup"><span data-stu-id="2fd82-180">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU Utilization</span></span>
* <span data-ttu-id="2fd82-181">TX 94 Mbps su Ethernet a 100 Mbps, MCU @100MHz , utilizzo di MCU del 27%</span><span class="sxs-lookup"><span data-stu-id="2fd82-181">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU Utilization</span></span>
* <span data-ttu-id="2fd82-182">Connessione affidabile</span><span class="sxs-lookup"><span data-stu-id="2fd82-182">Reliable connection</span></span>
* <span data-ttu-id="2fd82-183">Nessun limite al numero di socket TCP</span><span class="sxs-lookup"><span data-stu-id="2fd82-183">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="2fd82-184">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="2fd82-184">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="2fd82-185">Sospensione facoltativa per ricezione/trasmissione socket</span><span class="sxs-lookup"><span data-stu-id="2fd82-185">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="2fd82-186">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="2fd82-186">Optional timeout on all suspension</span></span>
* <span data-ttu-id="2fd82-187">Statistiche TCP facoltative</span><span class="sxs-lookup"><span data-stu-id="2fd82-187">Optional TCP statistics</span></span>
* <span data-ttu-id="2fd82-188">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="2fd82-188">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="2fd82-189">API TCP intuitive *: \* nx_tcp_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-189">Intuitive TCP APIs:  *nx_tcp_\**</span></span>

### <a name="icmp---internet-control-message-protocol-icmp"></a><span data-ttu-id="2fd82-190">ICMP-Internet Control Message Protocol (ICMP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-190">ICMP - Internet Control Message Protocol (ICMP)</span></span>

* <span data-ttu-id="2fd82-191">FLASH minimo 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="2fd82-191">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="2fd82-192">Supporto per IPv4</span><span class="sxs-lookup"><span data-stu-id="2fd82-192">IPv4 support</span></span>
* <span data-ttu-id="2fd82-193">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="2fd82-193">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="2fd82-194">Ping richiesta e risposta ping</span><span class="sxs-lookup"><span data-stu-id="2fd82-194">Ping request and ping response</span></span>
* <span data-ttu-id="2fd82-195">Sospensione thread facoltativa sulle richieste ping</span><span class="sxs-lookup"><span data-stu-id="2fd82-195">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="2fd82-196">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="2fd82-196">Optional timeout on all suspension</span></span>
* <span data-ttu-id="2fd82-197">Statistiche ICMP facoltative</span><span class="sxs-lookup"><span data-stu-id="2fd82-197">Optional ICMP statistics</span></span>
* <span data-ttu-id="2fd82-198">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="2fd82-198">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="2fd82-199">API ICMP intuitive *: \* nx_icmp_*</span><span class="sxs-lookup"><span data-stu-id="2fd82-199">Intuitive ICMP APIs: *nx_icmp_\**</span></span>

### <a name="ipv4---internet-protocol-ip"></a><span data-ttu-id="2fd82-200">IPv4-Internet Protocol (IP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-200">IPv4 - Internet Protocol (IP)</span></span>

* <span data-ttu-id="2fd82-201">Minimo 3,5 KB a 8,5 KB FLASH, da 2 KB a 3 KB di impronta RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-201">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint</span></span>
* <span data-ttu-id="2fd82-202">Architettura™ piconet</span><span class="sxs-lookup"><span data-stu-id="2fd82-202">Piconet™ Architecture</span></span>
* <span data-ttu-id="2fd82-203">Prestazioni veloci, near wirespeed</span><span class="sxs-lookup"><span data-stu-id="2fd82-203">Fast, near wirespeed performance</span></span>
* <span data-ttu-id="2fd82-204">Supporto di più interfacce</span><span class="sxs-lookup"><span data-stu-id="2fd82-204">Multiple interface support</span></span>
* <span data-ttu-id="2fd82-205">Supporto multihomed</span><span class="sxs-lookup"><span data-stu-id="2fd82-205">Multihomed support</span></span>
* <span data-ttu-id="2fd82-206">Supporto del routing statico</span><span class="sxs-lookup"><span data-stu-id="2fd82-206">Static routing support</span></span>
* <span data-ttu-id="2fd82-207">Supporto per la frammentazione e il riassemblaggio IP</span><span class="sxs-lookup"><span data-stu-id="2fd82-207">IP fragmentation/reassembly support</span></span>
* <span data-ttu-id="2fd82-208">Supporto per IPv4</span><span class="sxs-lookup"><span data-stu-id="2fd82-208">IPv4 Support</span></span>
* <span data-ttu-id="2fd82-209">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="2fd82-209">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="2fd82-210">Certificazione del logo per la fase II pronta</span><span class="sxs-lookup"><span data-stu-id="2fd82-210">Phase II Ready Logo Certification</span></span>
* <span data-ttu-id="2fd82-211">Statistiche IP facoltative</span><span class="sxs-lookup"><span data-stu-id="2fd82-211">Optional IP statistics</span></span>
* <span data-ttu-id="2fd82-212">Interfaccia del driver del livello fisico intuitiva e ben definita</span><span class="sxs-lookup"><span data-stu-id="2fd82-212">Well defined, intuitive physical layer driver interface</span></span>
* <span data-ttu-id="2fd82-213">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="2fd82-213">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="2fd82-214">API del livello IP intuitive: *nx_ip_ \**, *nxd_ip_ \**</span><span class="sxs-lookup"><span data-stu-id="2fd82-214">Intuitive IP layer APIs: *nx_ip_\**, *nxd_ip_\**</span></span>
* <span data-ttu-id="2fd82-215">Pre-certificati da TUV e UL a IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D e EN 50128 SW-SIL4</span><span class="sxs-lookup"><span data-stu-id="2fd82-215">Pre-certified by TUV and UL to IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D, and EN 50128 SW-SIL4</span></span>

### <a name="arprarp---address-resolution-protocol-arp-reverse-address-resolution-protocol-rarp"></a><span data-ttu-id="2fd82-216">ARP/RARP-Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP)</span><span class="sxs-lookup"><span data-stu-id="2fd82-216">ARP/RARP - Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP)</span></span>

* <span data-ttu-id="2fd82-217">Minimo 1,7 KB di memoria, dimensioni RAM</span><span class="sxs-lookup"><span data-stu-id="2fd82-217">Minimal 1.7 KB FLASH, RAM size</span></span>
* <span data-ttu-id="2fd82-218">Risoluzione dinamica degli indirizzi MAC 32-BLT IPv4 e 48-BLT</span><span class="sxs-lookup"><span data-stu-id="2fd82-218">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses</span></span>
* <span data-ttu-id="2fd82-219">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="2fd82-219">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="2fd82-220">Cache ARP flessibile definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="2fd82-220">Flexible, user-defined ARP cache</span></span>
* <span data-ttu-id="2fd82-221">Supporto ARP gratuito</span><span class="sxs-lookup"><span data-stu-id="2fd82-221">Gratuitous ARP support</span></span>
* <span data-ttu-id="2fd82-222">Statistiche ARP/RARP facoltative determinate dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="2fd82-222">Optional ARP/RARP statistics determined by application</span></span>
* <span data-ttu-id="2fd82-223">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="2fd82-223">System-level Trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="2fd82-224">API ARP/RARP intuitive *: \* nx_arp_*, *nx_rarp_ \**</span><span class="sxs-lookup"><span data-stu-id="2fd82-224">Intuitive ARP/RARP APIs: *nx_arp_\**, *nx_rarp_\**</span></span>

### <a name="ethernet-wifi-bluetooth-le-154-etc"></a><span data-ttu-id="2fd82-225">ETHERNET, Wi-Fi, BLUETOOTH LE, 15,4 e così via.</span><span class="sxs-lookup"><span data-stu-id="2fd82-225">ETHERNET, WiFi, BLUETOOTH LE, 15.4, etc.</span></span>

## <a name="small-footprint"></a><span data-ttu-id="2fd82-226">Footprint ridotto</span><span class="sxs-lookup"><span data-stu-id="2fd82-226">Small-footprint</span></span>

<span data-ttu-id="2fd82-227">Azure RTO NetX ha un footprint notevolmente ridotto da 9 KB a 15 KB per il supporto IP e UDP di base.</span><span class="sxs-lookup"><span data-stu-id="2fd82-227">Azure RTOS NetX has a remarkably small footprint of 9 KB to 15 KB for basic IP and UDP support.</span></span> <span data-ttu-id="2fd82-228">Per la funzionalità TCP sono necessari altri 10 KB a 13 KB di memoria per l'area di istruzione.</span><span class="sxs-lookup"><span data-stu-id="2fd82-228">An additional 10 KB to 13 KB of instruction area memory is needed for TCP functionality.</span></span> <span data-ttu-id="2fd82-229">L'utilizzo della RAM NetX di Azure RTO in genere varia da 2,6 KB a 3,6 KB oltre alla memoria del pool di pacchetti, definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2fd82-229">Azure RTOS NetX RAM usage typically ranges from 2.6 KB to 3.6 KB plus the packet pool memory, which is defined by the application.</span></span> <span data-ttu-id="2fd82-230">Come Azure RTO ThreadX, le dimensioni di Azure RTO NetX vengono ridimensionate automaticamente in base ai servizi usati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2fd82-230">Like Azure RTOS ThreadX, the size of Azure RTOS NetX automatically scales based on the services used by the application.</span></span> <span data-ttu-id="2fd82-231">In questo modo si eliminano praticamente la necessità di complicati parametri di configurazione e di compilazione, semplificando le operazioni per lo sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="2fd82-231">This virtually eliminates the need for complicated configuration and build parameters, making things easier for the developer.</span></span>

## <a name="fast-execution"></a><span data-ttu-id="2fd82-232">Esecuzione rapida</span><span class="sxs-lookup"><span data-stu-id="2fd82-232">Fast execution</span></span>

<span data-ttu-id="2fd82-233">Azure RTO NetX offre un'implementazione di invio/ricezione di pacchetti con copia zero ed è altamente integrato con Azure RTO ThreadX per ottenere le prestazioni più rapide possibile.</span><span class="sxs-lookup"><span data-stu-id="2fd82-233">Azure RTOS NetX provides a zero-copy packet send/receive implementation and is highly integrated with Azure RTOS ThreadX to achieve the fastest possible performance.</span></span> <span data-ttu-id="2fd82-234">Ad esempio, Azure RTO NetX può in genere ottenere trasferimenti di dati near wirespeed su un processore 80 MHz (o meno), usando solo una piccola percentuale dei cicli del processore.</span><span class="sxs-lookup"><span data-stu-id="2fd82-234">For example, Azure RTOS NetX can typically achieve near wirespeed data transfers on an 80-MHz processor (or less), while using only a small percentage of the processor cycles.</span></span>

## <a name="simple-easy-to-use"></a><span data-ttu-id="2fd82-235">Semplice e facile da usare</span><span class="sxs-lookup"><span data-stu-id="2fd82-235">Simple, easy-to-use</span></span>

<span data-ttu-id="2fd82-236">Azure RTO NetX è semplice da usare.</span><span class="sxs-lookup"><span data-stu-id="2fd82-236">Azure RTOS NetX is simple to use.</span></span> <span data-ttu-id="2fd82-237">L'API NetX di Azure RTO è intuitiva e altamente funzionale.</span><span class="sxs-lookup"><span data-stu-id="2fd82-237">The Azure RTOS NetX API is both intuitive and highly functional.</span></span> <span data-ttu-id="2fd82-238">I nomi delle API sono costituiti da parole reali e non da "zuppa alfabetica" o nomi altamente abbreviati, così comuni in altri prodotti di rete.</span><span class="sxs-lookup"><span data-stu-id="2fd82-238">The API names are made of real words and not “alphabet soup” or highly abbreviated names that are so common in other networking products.</span></span> <span data-ttu-id="2fd82-239">Tutte le API NetX di Azure RTO hanno un *nx_* leader e seguono una convenzione di denominazione sostantivo-verbo.</span><span class="sxs-lookup"><span data-stu-id="2fd82-239">All Azure RTOS NetX APIs have a leading *nx_* and follow a noun-verb naming convention.</span></span> <span data-ttu-id="2fd82-240">Inoltre, esiste una coerenza funzionale nell'API.</span><span class="sxs-lookup"><span data-stu-id="2fd82-240">Furthermore, there is a functional consistency throughout the API.</span></span> <span data-ttu-id="2fd82-241">Tutte le funzioni API che sospendono, ad esempio, hanno un timeout facoltativo che funziona in modo identico.</span><span class="sxs-lookup"><span data-stu-id="2fd82-241">For example, all API functions that suspend have an optional timeout that functions in an identical manner.</span></span> <span data-ttu-id="2fd82-242">Per le applicazioni legacy, Azure RTO NetX offre un ulteriore livello compatibile con socket BSD.</span><span class="sxs-lookup"><span data-stu-id="2fd82-242">For legacy applications, Azure RTOS NetX offers an additional BSD socket compatible layer.</span></span> <span data-ttu-id="2fd82-243">Questo livello consente agli sviluppatori di eseguire facilmente la migrazione di applicazioni di rete di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="2fd82-243">This layer helps developers migrate large networking applications with ease.</span></span>

## <a name="interoperability-verification"></a><span data-ttu-id="2fd82-244">Verifica dell'interoperabilità</span><span class="sxs-lookup"><span data-stu-id="2fd82-244">Interoperability verification</span></span>

<span data-ttu-id="2fd82-245">Azure RTO NetX è conforme agli standard RFC e offre un'interoperabilità completa con i dispositivi per la maggior parte dei fornitori.</span><span class="sxs-lookup"><span data-stu-id="2fd82-245">Azure RTOS NetX conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span> <span data-ttu-id="2fd82-246">Azure RTO NetX usa anche lo standard di settore IxANVL (Automatic Network Validation Library) per l'implementazione del protocollo TCP/IP di Azure RTO NetX core.</span><span class="sxs-lookup"><span data-stu-id="2fd82-246">Azure RTOS NetX also utilizes the industry standard IxANVL (Automated Network Validation Library) for the Azure RTOS NetX core TCP/IP protocol implementation.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="2fd82-247">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="2fd82-247">Advanced technology</span></span>

<span data-ttu-id="2fd82-248">Azure RTO NetX è una tecnologia avanzata che include:</span><span class="sxs-lookup"><span data-stu-id="2fd82-248">Azure RTOS NetX is advanced technology that includes:</span></span>

* <span data-ttu-id="2fd82-249">Architettura™ piconet</span><span class="sxs-lookup"><span data-stu-id="2fd82-249">Piconet™ architecture</span></span>
* <span data-ttu-id="2fd82-250">ridimensionamento automatico</span><span class="sxs-lookup"><span data-stu-id="2fd82-250">automatic scaling</span></span>
* <span data-ttu-id="2fd82-251">Tecnologia Fast-Path UDP™</span><span class="sxs-lookup"><span data-stu-id="2fd82-251">UDP Fast-Path Technology™</span></span>
* <span data-ttu-id="2fd82-252">gestione flessibile dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="2fd82-252">flexible packet management</span></span>
* <span data-ttu-id="2fd82-253">API di copia zero e implementazione</span><span class="sxs-lookup"><span data-stu-id="2fd82-253">zero-copy API and implementation</span></span>
* <span data-ttu-id="2fd82-254">supporto multihomed</span><span class="sxs-lookup"><span data-stu-id="2fd82-254">multihomed support</span></span>
* <span data-ttu-id="2fd82-255">timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="2fd82-255">optional timeout on all suspension</span></span>
* <span data-ttu-id="2fd82-256">supporto del routing statico</span><span class="sxs-lookup"><span data-stu-id="2fd82-256">static routing support</span></span>
* <span data-ttu-id="2fd82-257">Supporto per l'analisi del sistema TraceX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="2fd82-257">Azure RTOS TraceX system analysis support</span></span>

## <a name="fastest-time-to-market"></a><span data-ttu-id="2fd82-258">Time-to-market più veloce</span><span class="sxs-lookup"><span data-stu-id="2fd82-258">Fastest time-to-market</span></span>

<span data-ttu-id="2fd82-259">Azure RTO NetX è facile da installare, apprendere, usare, eseguire il debug, verificare, certificare e gestire.</span><span class="sxs-lookup"><span data-stu-id="2fd82-259">Azure RTOS NetX is easy to install, learn, use, debug, verify, certify, and maintain.</span></span> <span data-ttu-id="2fd82-260">Di conseguenza, Azure RTO NetX è uno degli stack TCP/IP più diffusi per i dispositivi di Internet delle cose incorporate, inclusi molti SoC da Broadcom, GainSpan e così via.</span><span class="sxs-lookup"><span data-stu-id="2fd82-260">As a result, Azure RTOS NetX is one of the most popular TCP/IP stacks for embedded IoT devices, including many SoCs from Broadcom, Gainspan, and so forth.</span></span> <span data-ttu-id="2fd82-261">Il nostro vantaggio di time-to-Market coerente è basato su:</span><span class="sxs-lookup"><span data-stu-id="2fd82-261">Our consistent time-to-market advantage is built on:</span></span>

* <span data-ttu-id="2fd82-262">documentazione sulla qualità: esaminare la [Guida dell'utente di Azure RTO NETX](about-this-guide.md) e vedere per se stessi.</span><span class="sxs-lookup"><span data-stu-id="2fd82-262">quality documentation – please review our [Azure RTOS NetX User Guide](about-this-guide.md) and see for yourself!</span></span>
* <span data-ttu-id="2fd82-263">disponibilità del codice sorgente completa</span><span class="sxs-lookup"><span data-stu-id="2fd82-263">complete source code availability</span></span>
* <span data-ttu-id="2fd82-264">API di facile utilizzo</span><span class="sxs-lookup"><span data-stu-id="2fd82-264">easy-to-use API</span></span>
* <span data-ttu-id="2fd82-265">set di funzionalità completo e avanzato</span><span class="sxs-lookup"><span data-stu-id="2fd82-265">comprehensive and advanced feature set</span></span>

## <a name="one-simple-license"></a><span data-ttu-id="2fd82-266">Una licenza semplice</span><span class="sxs-lookup"><span data-stu-id="2fd82-266">One Simple License</span></span>

<span data-ttu-id="2fd82-267">Non è previsto alcun costo per l'uso e il test del codice sorgente e nessun costo per le licenze di produzione quando viene distribuito in dispositivi con licenza preliminare, tutti gli altri dispositivi necessitano di una licenza annuale semplice.</span><span class="sxs-lookup"><span data-stu-id="2fd82-267">There is no cost to use and test the source code and no cost for production licenses when deployed to pre-licensed devices, all other devices need a simple annual license.</span></span>

## <a name="full-highest-quality-source-code"></a><span data-ttu-id="2fd82-268">Codice sorgente completo di qualità elevata</span><span class="sxs-lookup"><span data-stu-id="2fd82-268">Full, highest-quality source code</span></span>

<span data-ttu-id="2fd82-269">Nel corso degli anni, il codice sorgente NetX di Azure RTO ha impostato la qualità e la facilità di comprensione.</span><span class="sxs-lookup"><span data-stu-id="2fd82-269">Throughout the years, Azure RTOS NetX source code has set the bar in quality and ease of understanding.</span></span> <span data-ttu-id="2fd82-270">Inoltre, la convenzione relativa alla presenza di una funzione per ogni file fornisce una semplice navigazione all'origine.</span><span class="sxs-lookup"><span data-stu-id="2fd82-270">In addition, the convention of having one function per file provides for easy source navigation.</span></span>

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="2fd82-271">Supporta le architetture più diffuse</span><span class="sxs-lookup"><span data-stu-id="2fd82-271">Supports most popular architectures</span></span>

<span data-ttu-id="2fd82-272">Azure RTO NetX viene eseguito sui microprocessori più diffusi a 32/64 bit, predefiniti, completamente testati e completamente supportati, incluse le seguenti architetture avanzate:</span><span class="sxs-lookup"><span data-stu-id="2fd82-272">Azure RTOS NetX runs on most popular 32/64-bit microprocessors, out-of-the-box, fully tested and fully supported, including the following advanced architectures:</span></span>

<span data-ttu-id="2fd82-273">**Dispositivi analoghi**: SHARC, Blackfin, CM4xx</span><span class="sxs-lookup"><span data-stu-id="2fd82-273">**Analog Devices**: SHARC, Blackfin, CM4xx</span></span>

<span data-ttu-id="2fd82-274">**Andina Core**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="2fd82-274">**Andes Core**: RISC-V</span></span>

<span data-ttu-id="2fd82-275">**Ambiqmicro**: Apollo MCU</span><span class="sxs-lookup"><span data-stu-id="2fd82-275">**Ambiqmicro**: Apollo MCUs</span></span>

<span data-ttu-id="2fd82-276">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/a15/a5/A7/A8/A9/A5x 64-bi/A7X a 64 bit/R4/R5, TrustZone ARMv8-M</span><span class="sxs-lookup"><span data-stu-id="2fd82-276">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>

<span data-ttu-id="2fd82-277">**Cadenza**: Xtensa, diamante</span><span class="sxs-lookup"><span data-stu-id="2fd82-277">**Cadence**: Xtensa, Diamond</span></span>

<span data-ttu-id="2fd82-278">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WICED WiFi</span><span class="sxs-lookup"><span data-stu-id="2fd82-278">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>

<span data-ttu-id="2fd82-279">**Cypress**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="2fd82-279">**Cypress**: RISC-V</span></span>

<span data-ttu-id="2fd82-280">**Silice**: ESI-RISC</span><span class="sxs-lookup"><span data-stu-id="2fd82-280">**EnSilica**: eSi-RISC</span></span>

<span data-ttu-id="2fd82-281">**Infineon**: XMC1000, XMC4000, Tricore</span><span class="sxs-lookup"><span data-stu-id="2fd82-281">**Infineon**: XMC1000, XMC4000, TriCore</span></span>

<span data-ttu-id="2fd82-282">**Intel; Intel FPGA**: x36/Pentium, XScale, Nios II, Cyclone, Arria 10</span><span class="sxs-lookup"><span data-stu-id="2fd82-282">**Intel; Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>

<span data-ttu-id="2fd82-283">**Microchip**: avr32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="2fd82-283">**Microchip**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>

<span data-ttu-id="2fd82-284">**Microsemi**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="2fd82-284">**Microsemi**: RISC-V</span></span>

<span data-ttu-id="2fd82-285">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="2fd82-285">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>

<span data-ttu-id="2fd82-286">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span><span class="sxs-lookup"><span data-stu-id="2fd82-286">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span></span>

<span data-ttu-id="2fd82-287">**Laboratori siliconici**: EFM32</span><span class="sxs-lookup"><span data-stu-id="2fd82-287">**Silicon Labs**: EFM32</span></span>

<span data-ttu-id="2fd82-288">**Synopsys**: Arc 600, 700, Arc em, Arc HS</span><span class="sxs-lookup"><span data-stu-id="2fd82-288">**Synopsys**: ARC 600, 700, ARC EM, ARC HS</span></span>

<span data-ttu-id="2fd82-289">**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="2fd82-289">**ST**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>

<span data-ttu-id="2fd82-290">**TL**: C5xxx, C6xxx, Stellaris, Sitara, tiva-C</span><span class="sxs-lookup"><span data-stu-id="2fd82-290">**Tl**: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>

<span data-ttu-id="2fd82-291">**Elaborazione Wave**: MIPS32 4K, 24 k, 34 k, 1004 k, MIPS64 5K, MicroAptiv, InterAptiv, ProAptiv, M-Class</span><span class="sxs-lookup"><span data-stu-id="2fd82-291">**Wave Computing**: MIPS32 4K, 24 K, 34 K, 1004 K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>

<span data-ttu-id="2fd82-292">**Xilinx**: Microblaze, PowerPC 405, ZYNQ, Zynq UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="2fd82-292">**Xilinx**: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>

<span data-ttu-id="2fd82-293">*Tutte le cifre relative a tempistiche e dimensioni elencate sono stime e possono essere diverse nella piattaforma di sviluppo.*</span><span class="sxs-lookup"><span data-stu-id="2fd82-293">*All timing and size figures listed are estimates and may be different on your development platform.*</span></span>
