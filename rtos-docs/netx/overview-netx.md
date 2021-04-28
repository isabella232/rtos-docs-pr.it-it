---
title: Informazioni Azure RTOS NetX
description: Azure RTOS NetX è un'implementazione ad alte prestazioni degli standard del protocollo TCP/IP, completamente integrata con Azure RTOS ThreadX e disponibile per tutti i processori supportati.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 7c864c23f019e4841ddb3096fde663c8039baf44
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171319"
---
# <a name="overview-of-azure-rtos-netx"></a><span data-ttu-id="7143a-103">Panoramica di Azure RTOS NetX</span><span class="sxs-lookup"><span data-stu-id="7143a-103">Overview of Azure RTOS NetX</span></span>

<span data-ttu-id="7143a-104">Azure RTOS NetX è uno stack di rete incorporato TCP/IP IPv4 di livello industriale, progettato specificamente per applicazioni IoT, real-time e deep embedded.</span><span class="sxs-lookup"><span data-stu-id="7143a-104">Azure RTOS NetX is an industrial grade TCP/IP IPv4 embedded network stack, designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="7143a-105">Azure RTOS NetX è lo stack di rete IPv4 originale di Microsoft ed è essenzialmente un subset di Azure RTOS.</span><span class="sxs-lookup"><span data-stu-id="7143a-105">Azure RTOS NetX is Microsoft's original IPv4 network stack, and is essentially a subset of Azure RTOS.</span></span> <span data-ttu-id="7143a-106">NetX offre applicazioni incorporate con protocolli di rete di base, ad esempio IPv4, TCP e UDP, nonché una suite completa di protocolli aggiuntivi aggiuntivi di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="7143a-106">NetX provides embedded applications with core network protocols such as IPv4, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="7143a-107">Un footprint ridotto, un'esecuzione rapida e una maggiore facilità d'uso rendono Azure RTOS NetX una scelta ideale per le applicazioni IoT incorporate più complesse.</span><span class="sxs-lookup"><span data-stu-id="7143a-107">A small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX an ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="7143a-108">Protocolli API</span><span class="sxs-lookup"><span data-stu-id="7143a-108">API protocols</span></span>

### <a name="telnet"></a><span data-ttu-id="7143a-109">Telnet</span><span class="sxs-lookup"><span data-stu-id="7143a-109">TELNET</span></span>

* <span data-ttu-id="7143a-110">Footprint minimo di 0,5 KB e 0,3 KB di RAM.</span><span class="sxs-lookup"><span data-stu-id="7143a-110">Minimal 0.5 KB and 0.3 KB RAM footprint.</span></span>
* <span data-ttu-id="7143a-111">Supporto client e server.</span><span class="sxs-lookup"><span data-stu-id="7143a-111">Client and server support.</span></span>

### <a name="auto-ip"></a><span data-ttu-id="7143a-112">IP automatico</span><span class="sxs-lookup"><span data-stu-id="7143a-112">Auto IP</span></span>

* <span data-ttu-id="7143a-113">Assegnazione automatica degli indirizzi IPv4.</span><span class="sxs-lookup"><span data-stu-id="7143a-113">Automatic IPv4 address assignment.</span></span>
* <span data-ttu-id="7143a-114">Minimo 1,2 KB, 300 byte di RAM.</span><span class="sxs-lookup"><span data-stu-id="7143a-114">Minimal 1.2 KB, 300 bytes of RAM.</span></span>

### <a name="http---hypertext-transfer-protocolhttp"></a><span data-ttu-id="7143a-115">HTTP - Hypertext Transfer Protocol(HTTP)</span><span class="sxs-lookup"><span data-stu-id="7143a-115">HTTP - Hypertext Transfer Protocol(HTTP)</span></span>

* <span data-ttu-id="7143a-116">Footprint minimo da 2,8 KB a 4,8 KBBFLASH, da 0,4 KB a 1,0 KB di RAM.</span><span class="sxs-lookup"><span data-stu-id="7143a-116">Minimal 2.8 KB to 4.8KBFLASH, 0.4 KB to 1.0 KB RAM footprint.</span></span>
* <span data-ttu-id="7143a-117">Supporto client e server.</span><span class="sxs-lookup"><span data-stu-id="7143a-117">Client and server support.</span></span>

### <a name="smtp---simple-mail-transfer-protocol-smtp"></a><span data-ttu-id="7143a-118">SMTP - Simple Mail Transfer Protocol (SMTP)</span><span class="sxs-lookup"><span data-stu-id="7143a-118">SMTP - Simple Mail Transfer Protocol (SMTP)</span></span>

* <span data-ttu-id="7143a-119">Footprint minimo di 4,1 KB e 0,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="7143a-119">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="7143a-120">Supporto client</span><span class="sxs-lookup"><span data-stu-id="7143a-120">Client support</span></span>

### <a name="dhcp---dynamic-host-configuration-protocol-dhcp"></a><span data-ttu-id="7143a-121">DHCP - Dynamic Host Configuration Protocol (DHCP)</span><span class="sxs-lookup"><span data-stu-id="7143a-121">DHCP - Dynamic Host Configuration Protocol (DHCP)</span></span>

* <span data-ttu-id="7143a-122">Memoria FLASH minima da 3,6 KB a 4,6 KB, footprint della RAM di 2,7 KB</span><span class="sxs-lookup"><span data-stu-id="7143a-122">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="7143a-123">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="7143a-123">Client and server support</span></span>
* <span data-ttu-id="7143a-124">Supporto IPv4</span><span class="sxs-lookup"><span data-stu-id="7143a-124">IPv4 support</span></span>

### <a name="p0p3---post-office-protocol-version-3-pop3"></a><span data-ttu-id="7143a-125">P0P3 - Post Office Protocol versione 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="7143a-125">P0P3 - Post Office Protocol Version 3 (POP3)</span></span>

* <span data-ttu-id="7143a-126">Footprint minimo di 8,1 KB e 1,4 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="7143a-126">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="7143a-127">Supporto client</span><span class="sxs-lookup"><span data-stu-id="7143a-127">Client support</span></span>

### <a name="snmp---simple-network-management-protocol-snmp"></a><span data-ttu-id="7143a-128">SNMP - Simple Network Management Protocol (SNMP)</span><span class="sxs-lookup"><span data-stu-id="7143a-128">SNMP - Simple Network Management Protocol (SNMP)</span></span>

* <span data-ttu-id="7143a-129">Footprint minimo di 10,9 KB e 2,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="7143a-129">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="7143a-130">Supporto dell'agente per VI, V2 e V3</span><span class="sxs-lookup"><span data-stu-id="7143a-130">Agent support for VI, V2, and V3</span></span>

### <a name="ftp-tftp---file-transfer-protocol-ftp-trivial-file-transfer-protocol-tftp"></a><span data-ttu-id="7143a-131">FTP, TFTP - File Transfer Protocol (FTP), Trivial File Transfer Protocol (TFTP)</span><span class="sxs-lookup"><span data-stu-id="7143a-131">FTP, TFTP - File Transfer Protocol (FTP), Trivial File Transfer Protocol (TFTP)</span></span>

* <span data-ttu-id="7143a-132">FTP minimo da 1,8 KB a 7,2 KBBFLASH, da 0,6 KB a 2,1 KB di footprint della RAM</span><span class="sxs-lookup"><span data-stu-id="7143a-132">FTP Minimal 1.8 KB to 7.2KBFLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="7143a-133">TFTP minimo da 1,7 KB a 2,4 KBBFLASH, da 0,3 KB a 1,8 KB di footprint della RAM</span><span class="sxs-lookup"><span data-stu-id="7143a-133">TFTP Minimal 1.7 KB to 2.4KBFLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="7143a-134">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="7143a-134">Client and server support</span></span>

### <a name="ppp---polnt-to-point-protocol-ppp"></a><span data-ttu-id="7143a-135">PPP - Protocollo PPP (Polnt-to-PoInt)</span><span class="sxs-lookup"><span data-stu-id="7143a-135">PPP - Polnt-to-PoInt Protocol (PPP)</span></span>

* <span data-ttu-id="7143a-136">Footprint minimo di 7,1 KB e 3,8 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="7143a-136">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="7143a-137">Affidabilità e affidabilità.</span><span class="sxs-lookup"><span data-stu-id="7143a-137">Dependable and reliable.</span></span>

### <a name="sntp---simple-network-time-protocol-sntp"></a><span data-ttu-id="7143a-138">SNTP - Simple Network Time Protocol (SNTP)</span><span class="sxs-lookup"><span data-stu-id="7143a-138">SNTP - Simple Network Time Protocol (SNTP)</span></span>

* <span data-ttu-id="7143a-139">Minimo 4 KB e 0,5 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="7143a-139">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="7143a-140">Supporto client</span><span class="sxs-lookup"><span data-stu-id="7143a-140">Client support</span></span>

### <a name="azure-rtos-netx-api"></a><span data-ttu-id="7143a-141">Azure RTOS NetX API</span><span class="sxs-lookup"><span data-stu-id="7143a-141">Azure RTOS NetX API</span></span>

* <span data-ttu-id="7143a-142">Implementazione rapida dell'API a copia zero</span><span class="sxs-lookup"><span data-stu-id="7143a-142">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="7143a-143">Livello BSD facoltativo per la portabilità del codice socket legacy</span><span class="sxs-lookup"><span data-stu-id="7143a-143">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp---internet-group-management-protocol-igmp"></a><span data-ttu-id="7143a-144">IGMP - Internet Group Management Protocol (IGMP)</span><span class="sxs-lookup"><span data-stu-id="7143a-144">IGMP - Internet Group Management Protocol (IGMP)</span></span>

* <span data-ttu-id="7143a-145">Flash minimo da 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="7143a-145">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="7143a-146">Supporto dei gruppi multicast IPv4</span><span class="sxs-lookup"><span data-stu-id="7143a-146">IPv4 multicast group support</span></span>
* <span data-ttu-id="7143a-147">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="7143a-147">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="7143a-148">Statistiche IGMP facoltative</span><span class="sxs-lookup"><span data-stu-id="7143a-148">Optional IGMP statistics</span></span>
* <span data-ttu-id="7143a-149">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="7143a-149">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="udp---user-datagram-protocol-udp"></a><span data-ttu-id="7143a-150">UDP - User Datagram Protocol (UDP)</span><span class="sxs-lookup"><span data-stu-id="7143a-150">UDP - User Datagram Protocol (UDP)</span></span>

* <span data-ttu-id="7143a-151">Minimo 2,5 KB FLASH, 124 byte di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="7143a-151">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="7143a-152">Elaborazione rapida dei pacchetti TCP in prossimità di wirespeed:</span><span class="sxs-lookup"><span data-stu-id="7143a-152">Fast, near wirespeed TCP packet processing:</span></span>
* <span data-ttu-id="7143a-153">RX 95 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 14%</span><span class="sxs-lookup"><span data-stu-id="7143a-153">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU Utilization</span></span>
* <span data-ttu-id="7143a-154">TX 94 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 10%</span><span class="sxs-lookup"><span data-stu-id="7143a-154">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU Utilization</span></span>
* <span data-ttu-id="7143a-155">Tecnologia udp Fast Path™</span><span class="sxs-lookup"><span data-stu-id="7143a-155">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="7143a-156">Nessun limite al numero di UDP</span><span class="sxs-lookup"><span data-stu-id="7143a-156">No limits on the number of UDP</span></span>
* <span data-ttu-id="7143a-157">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="7143a-157">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="7143a-158">Sospensione facoltativa alla ricezione socket</span><span class="sxs-lookup"><span data-stu-id="7143a-158">Optional suspension on socket receive</span></span>
* <span data-ttu-id="7143a-159">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="7143a-159">Optional timeout on all suspension</span></span>
* <span data-ttu-id="7143a-160">Statistiche UDP facoltative</span><span class="sxs-lookup"><span data-stu-id="7143a-160">Optional UDP statistics</span></span>
* <span data-ttu-id="7143a-161">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="7143a-161">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="tcp---transmission-control-protocol-tcp"></a><span data-ttu-id="7143a-162">TCP - Transmission Control Protocol (TCP)</span><span class="sxs-lookup"><span data-stu-id="7143a-162">TCP - Transmission Control Protocol (TCP)</span></span>

* <span data-ttu-id="7143a-163">Memoria flash minima da 10,5K8 a 12,5 KB, 280 byte di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="7143a-163">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="7143a-164">Elaborazione rapida dei pacchetti TCP da vicino:</span><span class="sxs-lookup"><span data-stu-id="7143a-164">Fast, near wlrespeed TCP packet processing:</span></span>
* <span data-ttu-id="7143a-165">RX 93 Mbps su Ethernet a 100 Mbps, @100MHz MCU, utilizzo MCU del 20%</span><span class="sxs-lookup"><span data-stu-id="7143a-165">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU Utilization</span></span>
* <span data-ttu-id="7143a-166">TX 94 Mbps su Ethernet a 100 Mbps, @100MHz MCU, utilizzo MCU del 27%</span><span class="sxs-lookup"><span data-stu-id="7143a-166">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU Utilization</span></span>
* <span data-ttu-id="7143a-167">Connessione affidabile</span><span class="sxs-lookup"><span data-stu-id="7143a-167">Reliable connection</span></span>
* <span data-ttu-id="7143a-168">Nessun limite al numero di socket TCP</span><span class="sxs-lookup"><span data-stu-id="7143a-168">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="7143a-169">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="7143a-169">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="7143a-170">Sospensione facoltativa su ricezione/trasmissione socket</span><span class="sxs-lookup"><span data-stu-id="7143a-170">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="7143a-171">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="7143a-171">Optional timeout on all suspension</span></span>
* <span data-ttu-id="7143a-172">Statistiche TCP facoltative</span><span class="sxs-lookup"><span data-stu-id="7143a-172">Optional TCP statistics</span></span>
* <span data-ttu-id="7143a-173">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="7143a-173">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="icmp---internet-control-message-protocol-icmp"></a><span data-ttu-id="7143a-174">ICMP - Internet Control Message Protocol (ICMP)</span><span class="sxs-lookup"><span data-stu-id="7143a-174">ICMP - Internet Control Message Protocol (ICMP)</span></span>

* <span data-ttu-id="7143a-175">MEMORIA FLASH minima di 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="7143a-175">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="7143a-176">Supporto IPv4</span><span class="sxs-lookup"><span data-stu-id="7143a-176">IPv4 support</span></span>
* <span data-ttu-id="7143a-177">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="7143a-177">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="7143a-178">Richiesta ping e risposta ping</span><span class="sxs-lookup"><span data-stu-id="7143a-178">Ping request and ping response</span></span>
* <span data-ttu-id="7143a-179">Sospensione del thread facoltativa nelle richieste ping</span><span class="sxs-lookup"><span data-stu-id="7143a-179">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="7143a-180">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="7143a-180">Optional timeout on all suspension</span></span>
* <span data-ttu-id="7143a-181">Statistiche ICMP facoltative</span><span class="sxs-lookup"><span data-stu-id="7143a-181">Optional ICMP statistics</span></span>
* <span data-ttu-id="7143a-182">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="7143a-182">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="ipv4---internet-protocol-ip"></a><span data-ttu-id="7143a-183">IPv4 - Ip (Internet Protocol)</span><span class="sxs-lookup"><span data-stu-id="7143a-183">IPv4 - Internet Protocol (IP)</span></span>

* <span data-ttu-id="7143a-184">Footprint minimo da 3,5 KB a 8,5 KB FLASH, da 2 KB a 3 KB di RAM.</span><span class="sxs-lookup"><span data-stu-id="7143a-184">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint.</span></span>
* <span data-ttu-id="7143a-185">Architettura di Piconet™.</span><span class="sxs-lookup"><span data-stu-id="7143a-185">Piconet™ Architecture.</span></span>
* <span data-ttu-id="7143a-186">Prestazioni veloci e near wirespeed.</span><span class="sxs-lookup"><span data-stu-id="7143a-186">Fast, near wirespeed performance.</span></span>
* <span data-ttu-id="7143a-187">Supporto di più interfacce.</span><span class="sxs-lookup"><span data-stu-id="7143a-187">Multiple interface support.</span></span>
* <span data-ttu-id="7143a-188">Supporto multi-homed.</span><span class="sxs-lookup"><span data-stu-id="7143a-188">Multi-homed support.</span></span>
* <span data-ttu-id="7143a-189">Supporto del routing statico.</span><span class="sxs-lookup"><span data-stu-id="7143a-189">Static routing support.</span></span>
* <span data-ttu-id="7143a-190">Supporto della frammentazione/riassemblaggio IP.</span><span class="sxs-lookup"><span data-stu-id="7143a-190">IP fragmentation/reassembly support.</span></span>
* <span data-ttu-id="7143a-191">Supporto IPv4.</span><span class="sxs-lookup"><span data-stu-id="7143a-191">IPv4 Support.</span></span>
* <span data-ttu-id="7143a-192">IXIA IxANVL convalidato.</span><span class="sxs-lookup"><span data-stu-id="7143a-192">IXIA IxANVL Validated.</span></span>
* <span data-ttu-id="7143a-193">Certificazione del logo pronta per la fase II.</span><span class="sxs-lookup"><span data-stu-id="7143a-193">Phase II Ready Logo Certification.</span></span>
* <span data-ttu-id="7143a-194">Statistiche IP facoltative.</span><span class="sxs-lookup"><span data-stu-id="7143a-194">Optional IP statistics.</span></span>
* <span data-ttu-id="7143a-195">Interfaccia del driver del livello fisico ben definita e intuitiva.</span><span class="sxs-lookup"><span data-stu-id="7143a-195">Well defined, intuitive physical layer driver interface.</span></span>
* <span data-ttu-id="7143a-196">Traccia a livello di sistema tramite Azure RTOS TraceX.</span><span class="sxs-lookup"><span data-stu-id="7143a-196">System-level Trace via Azure RTOS TraceX.</span></span>

### <a name="arprarp---address-resolution-protocol-arp-reverse-address-resolution-protocol-rarp"></a><span data-ttu-id="7143a-197">ARP/RARP - Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP)</span><span class="sxs-lookup"><span data-stu-id="7143a-197">ARP/RARP - Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP)</span></span>

* <span data-ttu-id="7143a-198">Dimensioni minime di 1,7 KB di MEMORIA FLASH e RAM.</span><span class="sxs-lookup"><span data-stu-id="7143a-198">Minimal 1.7 KB FLASH, RAM size.</span></span>
* <span data-ttu-id="7143a-199">Risoluzione dinamica di indirizzi MAC da 32 blt IPv4 e 48 blt.</span><span class="sxs-lookup"><span data-stu-id="7143a-199">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses.</span></span>
* <span data-ttu-id="7143a-200">IXIA IxANVL convalidato.</span><span class="sxs-lookup"><span data-stu-id="7143a-200">IXIA IxANVL Validated.</span></span>
* <span data-ttu-id="7143a-201">Cache ARP flessibile e definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="7143a-201">Flexible, user-defined ARP cache.</span></span>
* <span data-ttu-id="7143a-202">Supporto gratuito ARP.</span><span class="sxs-lookup"><span data-stu-id="7143a-202">Gratuitous ARP support.</span></span>
* <span data-ttu-id="7143a-203">Statistiche ARP/RARP facoltative determinate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7143a-203">Optional ARP/RARP statistics determined by application.</span></span>
* <span data-ttu-id="7143a-204">Traccia a livello di sistema tramite Azure RTOS TraceX.</span><span class="sxs-lookup"><span data-stu-id="7143a-204">System-level Trace via Azure RTOS TraceX.</span></span>

### <a name="ethernet-wifi-bluetooth-le-154-etc"></a><span data-ttu-id="7143a-205">ETHERNET, WiFi, BLUETOOTH LE, 15.4 e così via.</span><span class="sxs-lookup"><span data-stu-id="7143a-205">ETHERNET, WiFi, BLUETOOTH LE, 15.4, etc.</span></span>

## <a name="interoperability-verification"></a><span data-ttu-id="7143a-206">Verifica dell'interoperabilità</span><span class="sxs-lookup"><span data-stu-id="7143a-206">Interoperability verification</span></span>

<span data-ttu-id="7143a-207">Azure RTOS NetX è conforme agli standard RFC e offre interoperabilità completa con i dispositivi per la maggior parte dei fornitori.</span><span class="sxs-lookup"><span data-stu-id="7143a-207">Azure RTOS NetX conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span> <span data-ttu-id="7143a-208">Azure RTOS NetX usa anche lo standard di settore IxANVL (Automated Network Validation Library) per l'implementazione del protocollo TCP/IP Azure RTOS NetX Core.</span><span class="sxs-lookup"><span data-stu-id="7143a-208">Azure RTOS NetX also utilizes the industry standard IxANVL (Automated Network Validation Library) for the Azure RTOS NetX core TCP/IP protocol implementation.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="7143a-209">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="7143a-209">Advanced technology</span></span>

<span data-ttu-id="7143a-210">Azure RTOS NetX è una tecnologia avanzata che include quanto segue.</span><span class="sxs-lookup"><span data-stu-id="7143a-210">Azure RTOS NetX is advanced technology that includes the following.</span></span>
* <span data-ttu-id="7143a-211">Architettura ™ Piconet.</span><span class="sxs-lookup"><span data-stu-id="7143a-211">Piconet™ architecture.</span></span>
* <span data-ttu-id="7143a-212">Ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="7143a-212">Automatic scaling.</span></span>
* <span data-ttu-id="7143a-213">UDP Fast-Path Technology™.</span><span class="sxs-lookup"><span data-stu-id="7143a-213">UDP Fast-Path Technology™.</span></span>
* <span data-ttu-id="7143a-214">Gestione flessibile dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="7143a-214">Flexible packet management.</span></span>
* <span data-ttu-id="7143a-215">API e implementazione a copia zero.</span><span class="sxs-lookup"><span data-stu-id="7143a-215">Zero-copy API and implementation.</span></span>
* <span data-ttu-id="7143a-216">Supporto multi-homed.</span><span class="sxs-lookup"><span data-stu-id="7143a-216">Multi-homed support.</span></span>
* <span data-ttu-id="7143a-217">Timeout facoltativo per tutte le sospensioni.</span><span class="sxs-lookup"><span data-stu-id="7143a-217">Optional timeout on all suspension.</span></span>
* <span data-ttu-id="7143a-218">Supporto del routing statico.</span><span class="sxs-lookup"><span data-stu-id="7143a-218">Static routing support.</span></span>
* <span data-ttu-id="7143a-219">Azure RTOS di analisi del sistema TraceX.</span><span class="sxs-lookup"><span data-stu-id="7143a-219">Azure RTOS TraceX system analysis support.</span></span>
