---
title: Informazioni Azure RTOS NetX
description: Azure RTOS NetX è un'implementazione ad alte prestazioni degli standard del protocollo TCP/IP, completamente integrata con Azure RTOS ThreadX e disponibile per tutti i processori supportati.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 63fd212249da6154926684f9bc844d2c2a78e84e
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754846"
---
# <a name="overview-of-azure-rtos-netx"></a><span data-ttu-id="3c047-103">Panoramica di Azure RTOS NetX</span><span class="sxs-lookup"><span data-stu-id="3c047-103">Overview of Azure RTOS NetX</span></span>

<span data-ttu-id="3c047-104">Azure RTOS NetX è uno stack di rete incorporato TCP/IP IPv4 di livello industriale, progettato specificamente per applicazioni IoT, in tempo reale e con deep embedded.</span><span class="sxs-lookup"><span data-stu-id="3c047-104">Azure RTOS NetX is an industrial grade TCP/IP IPv4 embedded network stack, designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="3c047-105">Azure RTOS NetX è lo stack di rete IPv4 originale di Microsoft ed è essenzialmente un subset di Azure RTOS.</span><span class="sxs-lookup"><span data-stu-id="3c047-105">Azure RTOS NetX is Microsoft's original IPv4 network stack, and is essentially a subset of Azure RTOS.</span></span> <span data-ttu-id="3c047-106">NetX fornisce applicazioni incorporate con protocolli di rete di base come IPv4, TCP e UDP, nonché una suite completa di protocolli aggiuntivi di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="3c047-106">NetX provides embedded applications with core network protocols such as IPv4, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="3c047-107">Un footprint ridotto, un'esecuzione rapida e una maggiore facilità d'uso rendono NetX Azure RTOS la scelta ideale per le applicazioni IoT incorporate più complesse.</span><span class="sxs-lookup"><span data-stu-id="3c047-107">A small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX an ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="3c047-108">Protocolli API</span><span class="sxs-lookup"><span data-stu-id="3c047-108">API protocols</span></span>
<span data-ttu-id="3c047-109">Azure RTOS NetX offre il supporto per gli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="3c047-109">Azure RTOS NetX provides support for the following.</span></span>

### <a name="telnet"></a><span data-ttu-id="3c047-110">Telnet</span><span class="sxs-lookup"><span data-stu-id="3c047-110">TELNET</span></span>

* <span data-ttu-id="3c047-111">Footprint minimo di 0,5 KB e 0,3 KB di RAM.</span><span class="sxs-lookup"><span data-stu-id="3c047-111">Minimal 0.5 KB and 0.3 KB RAM footprint.</span></span>
* <span data-ttu-id="3c047-112">Supporto client e server.</span><span class="sxs-lookup"><span data-stu-id="3c047-112">Client and server support.</span></span>

### <a name="auto-ip"></a><span data-ttu-id="3c047-113">IP automatico</span><span class="sxs-lookup"><span data-stu-id="3c047-113">Auto IP</span></span>

* <span data-ttu-id="3c047-114">Assegnazione automatica degli indirizzi IPv4.</span><span class="sxs-lookup"><span data-stu-id="3c047-114">Automatic IPv4 address assignment.</span></span>
* <span data-ttu-id="3c047-115">Minimo 1,2 KB, 300 byte di RAM.</span><span class="sxs-lookup"><span data-stu-id="3c047-115">Minimal 1.2 KB, 300 bytes of RAM.</span></span>

### <a name="http---hypertext-transfer-protocolhttp"></a><span data-ttu-id="3c047-116">HTTP - Hypertext Transfer Protocol(HTTP)</span><span class="sxs-lookup"><span data-stu-id="3c047-116">HTTP - Hypertext Transfer Protocol(HTTP)</span></span>

* <span data-ttu-id="3c047-117">Minimo da 2,8 KB a 4,8 KBBFLASH, da 0,4 KB a 1,0 KB di footprint della RAM.</span><span class="sxs-lookup"><span data-stu-id="3c047-117">Minimal 2.8 KB to 4.8KBFLASH, 0.4 KB to 1.0 KB RAM footprint.</span></span>
* <span data-ttu-id="3c047-118">Supporto client e server.</span><span class="sxs-lookup"><span data-stu-id="3c047-118">Client and server support.</span></span>

### <a name="smtp---simple-mail-transfer-protocol-smtp"></a><span data-ttu-id="3c047-119">SMTP - Simple Mail Transfer Protocol (SMTP)</span><span class="sxs-lookup"><span data-stu-id="3c047-119">SMTP - Simple Mail Transfer Protocol (SMTP)</span></span>

* <span data-ttu-id="3c047-120">Footprint minimo di 4,1 KB e 0,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="3c047-120">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="3c047-121">Supporto client</span><span class="sxs-lookup"><span data-stu-id="3c047-121">Client support</span></span>

### <a name="dhcp---dynamic-host-configuration-protocol-dhcp"></a><span data-ttu-id="3c047-122">DHCP - Dynamic Host Configuration Protocol (DHCP)</span><span class="sxs-lookup"><span data-stu-id="3c047-122">DHCP - Dynamic Host Configuration Protocol (DHCP)</span></span>

* <span data-ttu-id="3c047-123">Memoria FLASH minima da 3,6 KB a 4,6 KB, footprint della RAM di 2,7 KB</span><span class="sxs-lookup"><span data-stu-id="3c047-123">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="3c047-124">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="3c047-124">Client and server support</span></span>
* <span data-ttu-id="3c047-125">Supporto IPv4</span><span class="sxs-lookup"><span data-stu-id="3c047-125">IPv4 support</span></span>

### <a name="p0p3---post-office-protocol-version-3-pop3"></a><span data-ttu-id="3c047-126">P0P3 - Post Office Protocol versione 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="3c047-126">P0P3 - Post Office Protocol Version 3 (POP3)</span></span>

* <span data-ttu-id="3c047-127">Footprint minimo di 8,1 KB e 1,4 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="3c047-127">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="3c047-128">Supporto client</span><span class="sxs-lookup"><span data-stu-id="3c047-128">Client support</span></span>

### <a name="snmp---simple-network-management-protocol-snmp"></a><span data-ttu-id="3c047-129">SNMP - Simple Network Management Protocol (SNMP)</span><span class="sxs-lookup"><span data-stu-id="3c047-129">SNMP - Simple Network Management Protocol (SNMP)</span></span>

* <span data-ttu-id="3c047-130">Footprint minimo di 10,9 KB e 2,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="3c047-130">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="3c047-131">Supporto dell'agente per VI, V2 e V3</span><span class="sxs-lookup"><span data-stu-id="3c047-131">Agent support for VI, V2, and V3</span></span>

### <a name="ftp-tftp---file-transfer-protocol-ftp-trivial-file-transfer-protocol-tftp"></a><span data-ttu-id="3c047-132">FTP, TFTP - File Transfer Protocol (FTP), Trivial File Transfer Protocol (TFTP)</span><span class="sxs-lookup"><span data-stu-id="3c047-132">FTP, TFTP - File Transfer Protocol (FTP), Trivial File Transfer Protocol (TFTP)</span></span>

* <span data-ttu-id="3c047-133">FTP minimo da 1,8 KB a 7,2 KBBFLASH, da 0,6 KB a 2,1 KB di footprint della RAM</span><span class="sxs-lookup"><span data-stu-id="3c047-133">FTP Minimal 1.8 KB to 7.2KBFLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="3c047-134">TFTP minimo da 1,7 KB a 2,4 KBBFLASH, da 0,3 KB a 1,8 KB di footprint della RAM</span><span class="sxs-lookup"><span data-stu-id="3c047-134">TFTP Minimal 1.7 KB to 2.4KBFLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="3c047-135">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="3c047-135">Client and server support</span></span>

### <a name="ppp---polnt-to-point-protocol-ppp"></a><span data-ttu-id="3c047-136">PPP - Protocollo PPP (Polnt-to-PoInt)</span><span class="sxs-lookup"><span data-stu-id="3c047-136">PPP - Polnt-to-PoInt Protocol (PPP)</span></span>

* <span data-ttu-id="3c047-137">Footprint minimo di 7,1 KB e 3,8 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="3c047-137">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="3c047-138">Affidabilità e affidabilità.</span><span class="sxs-lookup"><span data-stu-id="3c047-138">Dependable and reliable.</span></span>

### <a name="sntp---simple-network-time-protocol-sntp"></a><span data-ttu-id="3c047-139">SNTP - Simple Network Time Protocol (SNTP)</span><span class="sxs-lookup"><span data-stu-id="3c047-139">SNTP - Simple Network Time Protocol (SNTP)</span></span>

* <span data-ttu-id="3c047-140">Minimo 4 KB e 0,5 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="3c047-140">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="3c047-141">Supporto client</span><span class="sxs-lookup"><span data-stu-id="3c047-141">Client support</span></span>

### <a name="azure-rtos-netx-api"></a><span data-ttu-id="3c047-142">Azure RTOS API NetX</span><span class="sxs-lookup"><span data-stu-id="3c047-142">Azure RTOS NetX API</span></span>

* <span data-ttu-id="3c047-143">Implementazione rapida e senza copia dell'API</span><span class="sxs-lookup"><span data-stu-id="3c047-143">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="3c047-144">Livello BSD facoltativo per la portabilità del codice socket legacy</span><span class="sxs-lookup"><span data-stu-id="3c047-144">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp---internet-group-management-protocol-igmp"></a><span data-ttu-id="3c047-145">IGMP - Internet Group Management Protocol (IGMP)</span><span class="sxs-lookup"><span data-stu-id="3c047-145">IGMP - Internet Group Management Protocol (IGMP)</span></span>

* <span data-ttu-id="3c047-146">MEMORIA FLASH minima di 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="3c047-146">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="3c047-147">Supporto di gruppi multicast IPv4</span><span class="sxs-lookup"><span data-stu-id="3c047-147">IPv4 multicast group support</span></span>
* <span data-ttu-id="3c047-148">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="3c047-148">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="3c047-149">Statistiche IGMP facoltative</span><span class="sxs-lookup"><span data-stu-id="3c047-149">Optional IGMP statistics</span></span>
* <span data-ttu-id="3c047-150">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="3c047-150">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="udp---user-datagram-protocol-udp"></a><span data-ttu-id="3c047-151">UDP - User Datagram Protocol (UDP)</span><span class="sxs-lookup"><span data-stu-id="3c047-151">UDP - User Datagram Protocol (UDP)</span></span>

* <span data-ttu-id="3c047-152">MEMORIA FLASH minima di 2,5 KB, 124 byte di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="3c047-152">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="3c047-153">Elaborazione rapida e quasi in transito dei pacchetti TCP:</span><span class="sxs-lookup"><span data-stu-id="3c047-153">Fast, near wirespeed TCP packet processing:</span></span>
* <span data-ttu-id="3c047-154">RX 95 Mbps su Ethernet a 100 Mbps, @100MHz MCU, utilizzo MCU del 14%</span><span class="sxs-lookup"><span data-stu-id="3c047-154">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU Utilization</span></span>
* <span data-ttu-id="3c047-155">TX 94 Mbps su Ethernet a 100 Mbps, @100MHz MCU, utilizzo MCU del 10%</span><span class="sxs-lookup"><span data-stu-id="3c047-155">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU Utilization</span></span>
* <span data-ttu-id="3c047-156">Tecnologia fast path™ UDP</span><span class="sxs-lookup"><span data-stu-id="3c047-156">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="3c047-157">Nessun limite al numero di UDP</span><span class="sxs-lookup"><span data-stu-id="3c047-157">No limits on the number of UDP</span></span>
* <span data-ttu-id="3c047-158">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="3c047-158">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="3c047-159">Sospensione facoltativa alla ricezione del socket</span><span class="sxs-lookup"><span data-stu-id="3c047-159">Optional suspension on socket receive</span></span>
* <span data-ttu-id="3c047-160">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="3c047-160">Optional timeout on all suspension</span></span>
* <span data-ttu-id="3c047-161">Statistiche UDP facoltative</span><span class="sxs-lookup"><span data-stu-id="3c047-161">Optional UDP statistics</span></span>
* <span data-ttu-id="3c047-162">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="3c047-162">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="tcp---transmission-control-protocol-tcp"></a><span data-ttu-id="3c047-163">TCP - Transmission Control Protocol (TCP)</span><span class="sxs-lookup"><span data-stu-id="3c047-163">TCP - Transmission Control Protocol (TCP)</span></span>

* <span data-ttu-id="3c047-164">Memoria flash minima da 10,5K8 a 12,5 KB, 280 byte di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="3c047-164">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="3c047-165">Elaborazione rapida dei pacchetti TCP da vicino:</span><span class="sxs-lookup"><span data-stu-id="3c047-165">Fast, near wlrespeed TCP packet processing:</span></span>
* <span data-ttu-id="3c047-166">RX 93 Mbps su Ethernet a 100 Mbps, @100MHz MCU, utilizzo MCU del 20%</span><span class="sxs-lookup"><span data-stu-id="3c047-166">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU Utilization</span></span>
* <span data-ttu-id="3c047-167">TX 94 Mbps su Ethernet a 100 Mbps, @100MHz MCU, utilizzo MCU del 27%</span><span class="sxs-lookup"><span data-stu-id="3c047-167">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU Utilization</span></span>
* <span data-ttu-id="3c047-168">Connessione affidabile</span><span class="sxs-lookup"><span data-stu-id="3c047-168">Reliable connection</span></span>
* <span data-ttu-id="3c047-169">Nessun limite al numero di socket TCP</span><span class="sxs-lookup"><span data-stu-id="3c047-169">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="3c047-170">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="3c047-170">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="3c047-171">Sospensione facoltativa su ricezione/trasmissione socket</span><span class="sxs-lookup"><span data-stu-id="3c047-171">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="3c047-172">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="3c047-172">Optional timeout on all suspension</span></span>
* <span data-ttu-id="3c047-173">Statistiche TCP facoltative</span><span class="sxs-lookup"><span data-stu-id="3c047-173">Optional TCP statistics</span></span>
* <span data-ttu-id="3c047-174">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="3c047-174">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="icmp---internet-control-message-protocol-icmp"></a><span data-ttu-id="3c047-175">ICMP - Internet Control Message Protocol (ICMP)</span><span class="sxs-lookup"><span data-stu-id="3c047-175">ICMP - Internet Control Message Protocol (ICMP)</span></span>

* <span data-ttu-id="3c047-176">MEMORIA FLASH minima di 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="3c047-176">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="3c047-177">Supporto IPv4</span><span class="sxs-lookup"><span data-stu-id="3c047-177">IPv4 support</span></span>
* <span data-ttu-id="3c047-178">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="3c047-178">IXIA IxANVL Validated</span></span>
* <span data-ttu-id="3c047-179">Richiesta ping e risposta ping</span><span class="sxs-lookup"><span data-stu-id="3c047-179">Ping request and ping response</span></span>
* <span data-ttu-id="3c047-180">Sospensione del thread facoltativa nelle richieste ping</span><span class="sxs-lookup"><span data-stu-id="3c047-180">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="3c047-181">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="3c047-181">Optional timeout on all suspension</span></span>
* <span data-ttu-id="3c047-182">Statistiche ICMP facoltative</span><span class="sxs-lookup"><span data-stu-id="3c047-182">Optional ICMP statistics</span></span>
* <span data-ttu-id="3c047-183">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="3c047-183">System-level Trace via Azure RTOS TraceX</span></span>

### <a name="ipv4---internet-protocol-ip"></a><span data-ttu-id="3c047-184">IPv4 - Ip (Internet Protocol)</span><span class="sxs-lookup"><span data-stu-id="3c047-184">IPv4 - Internet Protocol (IP)</span></span>

* <span data-ttu-id="3c047-185">Memoria FLASH minima da 3,5 KB a 8,5 KB, footprint di RAM da 2 KB a 3 KB.</span><span class="sxs-lookup"><span data-stu-id="3c047-185">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint.</span></span>
* <span data-ttu-id="3c047-186">Architettura ™ Piconet.</span><span class="sxs-lookup"><span data-stu-id="3c047-186">Piconet™ Architecture.</span></span>
* <span data-ttu-id="3c047-187">Prestazioni veloci e near wirespeed.</span><span class="sxs-lookup"><span data-stu-id="3c047-187">Fast, near wirespeed performance.</span></span>
* <span data-ttu-id="3c047-188">Supporto di più interfacce.</span><span class="sxs-lookup"><span data-stu-id="3c047-188">Multiple interface support.</span></span>
* <span data-ttu-id="3c047-189">Supporto multi-homed.</span><span class="sxs-lookup"><span data-stu-id="3c047-189">Multi-homed support.</span></span>
* <span data-ttu-id="3c047-190">Supporto del routing statico.</span><span class="sxs-lookup"><span data-stu-id="3c047-190">Static routing support.</span></span>
* <span data-ttu-id="3c047-191">Supporto della frammentazione/riassemblaggio IP.</span><span class="sxs-lookup"><span data-stu-id="3c047-191">IP fragmentation/reassembly support.</span></span>
* <span data-ttu-id="3c047-192">Supporto IPv4.</span><span class="sxs-lookup"><span data-stu-id="3c047-192">IPv4 Support.</span></span>
* <span data-ttu-id="3c047-193">IXIA IxANVL convalidato.</span><span class="sxs-lookup"><span data-stu-id="3c047-193">IXIA IxANVL Validated.</span></span>
* <span data-ttu-id="3c047-194">Certificazione del logo pronta per la fase II.</span><span class="sxs-lookup"><span data-stu-id="3c047-194">Phase II Ready Logo Certification.</span></span>
* <span data-ttu-id="3c047-195">Statistiche IP facoltative.</span><span class="sxs-lookup"><span data-stu-id="3c047-195">Optional IP statistics.</span></span>
* <span data-ttu-id="3c047-196">Interfaccia del driver di livello fisico ben definita e intuitiva.</span><span class="sxs-lookup"><span data-stu-id="3c047-196">Well defined, intuitive physical layer driver interface.</span></span>
* <span data-ttu-id="3c047-197">Traccia a livello di sistema tramite Azure RTOS TraceX.</span><span class="sxs-lookup"><span data-stu-id="3c047-197">System-level Trace via Azure RTOS TraceX.</span></span>

### <a name="arprarp---address-resolution-protocol-arp-reverse-address-resolution-protocol-rarp"></a><span data-ttu-id="3c047-198">ARP/RARP - Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP)</span><span class="sxs-lookup"><span data-stu-id="3c047-198">ARP/RARP - Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP)</span></span>

* <span data-ttu-id="3c047-199">Memoria FLASH minima di 1,7 KB, dimensioni della RAM.</span><span class="sxs-lookup"><span data-stu-id="3c047-199">Minimal 1.7 KB FLASH, RAM size.</span></span>
* <span data-ttu-id="3c047-200">Risoluzione dinamica di indirizzi MAC IPv4 e 48 blt a 32 blt.</span><span class="sxs-lookup"><span data-stu-id="3c047-200">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses.</span></span>
* <span data-ttu-id="3c047-201">IXIA IxANVL convalidato.</span><span class="sxs-lookup"><span data-stu-id="3c047-201">IXIA IxANVL Validated.</span></span>
* <span data-ttu-id="3c047-202">Cache ARP flessibile e definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="3c047-202">Flexible, user-defined ARP cache.</span></span>
* <span data-ttu-id="3c047-203">Supporto gratuito ARP.</span><span class="sxs-lookup"><span data-stu-id="3c047-203">Gratuitous ARP support.</span></span>
* <span data-ttu-id="3c047-204">Statistiche ARP/RARP facoltative determinate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3c047-204">Optional ARP/RARP statistics determined by application.</span></span>
* <span data-ttu-id="3c047-205">Traccia a livello di sistema tramite Azure RTOS TraceX.</span><span class="sxs-lookup"><span data-stu-id="3c047-205">System-level Trace via Azure RTOS TraceX.</span></span>

### <a name="ethernet-wifi-bluetooth-le-154-etc"></a><span data-ttu-id="3c047-206">ETHERNET, WiFi, BLUETOOTH LE, 15.4 e così via.</span><span class="sxs-lookup"><span data-stu-id="3c047-206">ETHERNET, WiFi, BLUETOOTH LE, 15.4, etc.</span></span>

## <a name="interoperability-verification"></a><span data-ttu-id="3c047-207">Verifica dell'interoperabilità</span><span class="sxs-lookup"><span data-stu-id="3c047-207">Interoperability verification</span></span>

<span data-ttu-id="3c047-208">Azure RTOS NetX è conforme agli standard RFC e offre interoperabilità completa con i dispositivi della maggior parte dei fornitori.</span><span class="sxs-lookup"><span data-stu-id="3c047-208">Azure RTOS NetX conforms to RFC standards and offers complete interoperability with devices from most vendors.</span></span> <span data-ttu-id="3c047-209">Azure RTOS NetX usa anche lo standard di settore IxANVL (Automated Network Validation Library) per l'implementazione del protocollo TCP/IP Azure RTOS NetX Core.</span><span class="sxs-lookup"><span data-stu-id="3c047-209">Azure RTOS NetX also utilizes the industry standard IxANVL (Automated Network Validation Library) for the Azure RTOS NetX core TCP/IP protocol implementation.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="3c047-210">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="3c047-210">Advanced technology</span></span>

<span data-ttu-id="3c047-211">Azure RTOS NetX è una tecnologia avanzata che include quanto segue.</span><span class="sxs-lookup"><span data-stu-id="3c047-211">Azure RTOS NetX is advanced technology that includes the following.</span></span>
* <span data-ttu-id="3c047-212">Architettura ™ Piconet.</span><span class="sxs-lookup"><span data-stu-id="3c047-212">Piconet™ architecture.</span></span>
* <span data-ttu-id="3c047-213">Scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="3c047-213">Automatic scaling.</span></span>
* <span data-ttu-id="3c047-214">UDP Fast-Path Technology™.</span><span class="sxs-lookup"><span data-stu-id="3c047-214">UDP Fast-Path Technology™.</span></span>
* <span data-ttu-id="3c047-215">Gestione flessibile dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="3c047-215">Flexible packet management.</span></span>
* <span data-ttu-id="3c047-216">API e implementazione in copia zero.</span><span class="sxs-lookup"><span data-stu-id="3c047-216">Zero-copy API and implementation.</span></span>
* <span data-ttu-id="3c047-217">Supporto multi-homed.</span><span class="sxs-lookup"><span data-stu-id="3c047-217">Multi-homed support.</span></span>
* <span data-ttu-id="3c047-218">Timeout facoltativo per tutte le sospensioni.</span><span class="sxs-lookup"><span data-stu-id="3c047-218">Optional timeout on all suspension.</span></span>
* <span data-ttu-id="3c047-219">Supporto del routing statico.</span><span class="sxs-lookup"><span data-stu-id="3c047-219">Static routing support.</span></span>
* <span data-ttu-id="3c047-220">Azure RTOS di analisi del sistema TraceX.</span><span class="sxs-lookup"><span data-stu-id="3c047-220">Azure RTOS TraceX system analysis support.</span></span>
