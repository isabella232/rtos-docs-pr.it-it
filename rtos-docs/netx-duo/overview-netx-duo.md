---
title: Informazioni su Azure RTO NetX Duo
description: Azure RTO NetX Duo è uno stack di rete TCP/IP avanzato e di livello industriale, progettato in modo specifico per le applicazioni in tempo reale e in tempo reale incorporate.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 2339da391e52b437a2111ae439cccf41e038bdcf
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822829"
---
# <a name="overview-of-azure-rtos-netx-duo"></a><span data-ttu-id="69128-103">Panoramica di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="69128-103">Overview of Azure RTOS NetX Duo</span></span>

<span data-ttu-id="69128-104">Lo stack di rete TCP/IP di Azure RTO NetX Duo Embedded è uno stack di rete TCP/IP avanzato e di livello industriale di Microsoft, progettato in modo specifico per applicazioni molto incorporate e in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="69128-104">Azure RTOS NetX Duo embedded TCP/IP network stack is Microsoft's advanced, industrial grade dual IPv4 and IPv6 TCP/IP network stack that is designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="69128-105">NetX Duo fornisce applicazioni incorporate con protocolli di rete principali, ad esempio IPv4, IPv6, TCP e UDP, oltre a una suite completa di altri protocolli aggiuntivi di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="69128-105">NetX Duo provides embedded applications with core network protocols such as IPv4, IPv6, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="69128-106">Azure RTO NetX Duo offre sicurezza tramite altri prodotti per la sicurezza aggiuntivi, tra cui Azure RTO NetX Secure IPsec e Azure RTO NetX secure SSL/TLS/DTLS.</span><span class="sxs-lookup"><span data-stu-id="69128-106">Azure RTOS NetX Duo offers security via additional add-on security products, including Azure RTOS NetX Secure IPsec and Azure RTOS NetX Secure SSL/TLS/DTLS.</span></span> <span data-ttu-id="69128-107">Tutti questi combinati con un footprint ridotto, un'esecuzione rapida e una semplicità di utilizzo superiore rendono Azure RTO NetX Duo la scelta ideale per le applicazioni di Internet delle cose incorporate più complesse.</span><span class="sxs-lookup"><span data-stu-id="69128-107">All of this combined with an small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX Duo the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="69128-108">Protocolli API</span><span class="sxs-lookup"><span data-stu-id="69128-108">API protocols</span></span>

### <a name="mqtt"></a><span data-ttu-id="69128-109">MQTT</span><span class="sxs-lookup"><span data-stu-id="69128-109">MQTT</span></span>

* <span data-ttu-id="69128-110">Trasporto di telemetria della coda di messaggistica (MQTT)</span><span class="sxs-lookup"><span data-stu-id="69128-110">Messaging Queue Telemetry Transport (MQTT)</span></span>
* <span data-ttu-id="69128-111">FLASH minimo 2,7 KB</span><span class="sxs-lookup"><span data-stu-id="69128-111">Minimal 2.7 KB FLASH</span></span>
* <span data-ttu-id="69128-112">API MQTT intuitive: *nx_mqtt_*\*</span><span class="sxs-lookup"><span data-stu-id="69128-112">Intuitive MQTT APIs: *nx_mqtt_*\*</span></span>

### <a name="auto-ip"></a><span data-ttu-id="69128-113">IP automatico</span><span class="sxs-lookup"><span data-stu-id="69128-113">Auto IP</span></span>

* <span data-ttu-id="69128-114">Assegnazione automatica di indirizzi IPv4</span><span class="sxs-lookup"><span data-stu-id="69128-114">Automatic IPv4 address assignment</span></span>
* <span data-ttu-id="69128-115">Minimo 1,2 KB, 300 byte di RAM</span><span class="sxs-lookup"><span data-stu-id="69128-115">Minimal 1.2 KB, 300 bytes of RAM</span></span>
* <span data-ttu-id="69128-116">API AutoIP intuitive *: \* nx_autoip_*</span><span class="sxs-lookup"><span data-stu-id="69128-116">Intuitive AutoIP APIs: *nx_autoip_\**</span></span>

### <a name="http-https"></a><span data-ttu-id="69128-117">HTTP, HTTPS</span><span class="sxs-lookup"><span data-stu-id="69128-117">HTTP, HTTPS</span></span>

#### <a name="http-10"></a><span data-ttu-id="69128-118">HTTP 1,0</span><span class="sxs-lookup"><span data-stu-id="69128-118">HTTP 1.0</span></span>

* <span data-ttu-id="69128-119">Hypertext Transfer Protocol (HTTP)</span><span class="sxs-lookup"><span data-stu-id="69128-119">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="69128-120">Minimo 2,8 KB a 4,8 KB FLASH/0,4 KB a 1,0 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="69128-120">Minimal 2.8 KB to 4.8 KB FLASH / 0.4 KB to 1.0 KB RAM</span></span>
* <span data-ttu-id="69128-121">Supporto per client e server</span><span class="sxs-lookup"><span data-stu-id="69128-121">Client and server support</span></span>
* <span data-ttu-id="69128-122">API intuitive *: \* nx_http_*</span><span class="sxs-lookup"><span data-stu-id="69128-122">Intuitive APIs: *nx_http_\**</span></span>

#### <a name="httphttps-11"></a><span data-ttu-id="69128-123">HTTP/HTTPS 1,1</span><span class="sxs-lookup"><span data-stu-id="69128-123">HTTP/HTTPS 1.1</span></span>

* <span data-ttu-id="69128-124">Hypertext Transfer Protocol (HTTP)</span><span class="sxs-lookup"><span data-stu-id="69128-124">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="69128-125">Minimo 3,0 KB a 9,5 KB FLASH/0,5 KB a 2 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="69128-125">Minimal 3.0 KB to 9.5 KB FLASH / 0.5 KB to 2 KB RAM</span></span>
* <span data-ttu-id="69128-126">Supporto per client e server</span><span class="sxs-lookup"><span data-stu-id="69128-126">Client and server support</span></span>
* <span data-ttu-id="69128-127">Più sessioni client in ingresso</span><span class="sxs-lookup"><span data-stu-id="69128-127">Multiple incoming client sessions</span></span>
* <span data-ttu-id="69128-128">Testo normale e HTTPS crittografato</span><span class="sxs-lookup"><span data-stu-id="69128-128">Plain text and encrypted HTTPS</span></span>
* <span data-ttu-id="69128-129">Supporto per connessioni permanenti</span><span class="sxs-lookup"><span data-stu-id="69128-129">Persistent connection support</span></span>
* <span data-ttu-id="69128-130">Caricamento file multipart</span><span class="sxs-lookup"><span data-stu-id="69128-130">Multipart file upload</span></span>
* <span data-ttu-id="69128-131">Completamente integrato con Azure RTO NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="69128-131">Fully integrated with Azure RTOS NetX Secure TLS</span></span>
* <span data-ttu-id="69128-132">API intuitive *: \* nx_web_http*</span><span class="sxs-lookup"><span data-stu-id="69128-132">Intuitive APIs: *nx_web_http\**</span></span>

### <a name="smtp"></a><span data-ttu-id="69128-133">SMTP</span><span class="sxs-lookup"><span data-stu-id="69128-133">SMTP</span></span>

* <span data-ttu-id="69128-134">Simple Mall Transfer Protocol (SMTP)</span><span class="sxs-lookup"><span data-stu-id="69128-134">Simple Mall Transfer Protocol (SMTP)</span></span>
* <span data-ttu-id="69128-135">Ingombro minimo 4,1 KB e 0,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="69128-135">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="69128-136">Supporto client</span><span class="sxs-lookup"><span data-stu-id="69128-136">Client support</span></span>
* <span data-ttu-id="69128-137">API SMTP intuitive *: \* nx_smtp_*</span><span class="sxs-lookup"><span data-stu-id="69128-137">Intuitive SMTP APIs: *nx_smtp_\**</span></span>

### <a name="dhcp"></a><span data-ttu-id="69128-138">DHCP</span><span class="sxs-lookup"><span data-stu-id="69128-138">DHCP</span></span>

* <span data-ttu-id="69128-139">Dynamic Host Configuration Protocol (DHCP)</span><span class="sxs-lookup"><span data-stu-id="69128-139">Dynamic Host Configuration Protocol (DHCP)</span></span>
* <span data-ttu-id="69128-140">Minimo 3,6 KB a 4,6 KB FLASH, 2,7 KB di impronta RAM</span><span class="sxs-lookup"><span data-stu-id="69128-140">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="69128-141">Supporto per client e server</span><span class="sxs-lookup"><span data-stu-id="69128-141">Client and server support</span></span>
* <span data-ttu-id="69128-142">Supporto per IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="69128-142">IPv4 and IPv6 support</span></span>
* <span data-ttu-id="69128-143">API DHCP intuitive *: \* nx_dhcp_*</span><span class="sxs-lookup"><span data-stu-id="69128-143">Intuitive DHCP APIs: *nx_dhcp_\**</span></span>

### <a name="nat"></a><span data-ttu-id="69128-144">NAT</span><span class="sxs-lookup"><span data-stu-id="69128-144">NAT</span></span>

* <span data-ttu-id="69128-145">Network Address Translation (NAT)</span><span class="sxs-lookup"><span data-stu-id="69128-145">Network Address Translation (NAT)</span></span>
* <span data-ttu-id="69128-146">Ingombro minimo 3.5 K6 e 0,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="69128-146">Minimal 3.5K6 and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="69128-147">Supporto degli indirizzi IPv4</span><span class="sxs-lookup"><span data-stu-id="69128-147">IPv4 address support</span></span>
* <span data-ttu-id="69128-148">API NAT intuitive *: \* nx_nat_*</span><span class="sxs-lookup"><span data-stu-id="69128-148">Intuitive NAT APIs: *nx_nat_\**</span></span>
* <span data-ttu-id="69128-149">NAT è disponibile solo con Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="69128-149">NAT is only available with Azure RTOS NetX Duo</span></span>

### <a name="snmp"></a><span data-ttu-id="69128-150">SNMP</span><span class="sxs-lookup"><span data-stu-id="69128-150">SNMP</span></span>

* <span data-ttu-id="69128-151">Simple Network Management Protocol (SNMP)</span><span class="sxs-lookup"><span data-stu-id="69128-151">Simple Network Management Protocol (SNMP)</span></span>
* <span data-ttu-id="69128-152">Ingombro minimo 10,9 KB e 2,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="69128-152">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="69128-153">Supporto degli agenti per VI, V2 e V3</span><span class="sxs-lookup"><span data-stu-id="69128-153">Agent support for VI, V2, and V3</span></span>
* <span data-ttu-id="69128-154">API SNMP intuitive *: \* nx_snmp_*</span><span class="sxs-lookup"><span data-stu-id="69128-154">Intuitive SNMP APIs: *nx_snmp_\**</span></span>

### <a name="dns-mdns-dns-sd"></a><span data-ttu-id="69128-155">DNS, MDN, DNS-SD</span><span class="sxs-lookup"><span data-stu-id="69128-155">DNS, mDNS, DNS-SD</span></span>

* <span data-ttu-id="69128-156">Domain Name System (DNS)</span><span class="sxs-lookup"><span data-stu-id="69128-156">Domain Name System (DNS)</span></span>
* <span data-ttu-id="69128-157">Domain Name System multicast (MDN)</span><span class="sxs-lookup"><span data-stu-id="69128-157">Multicast Domain Name System (mDNS)</span></span>
* <span data-ttu-id="69128-158">Individuazione del servizio basato su DNS (DNS-SD)</span><span class="sxs-lookup"><span data-stu-id="69128-158">DNS-based service discovery (DNS-SD)</span></span>
* <span data-ttu-id="69128-159">DNS minimo 2,4 KB a 3 KB di FLASH, 1 KB di impronta RAM</span><span class="sxs-lookup"><span data-stu-id="69128-159">DNS Minimal 2.4 KB to 3 KB FLASH, 1 KB RAM footprint</span></span>
* <span data-ttu-id="69128-160">Supporto client</span><span class="sxs-lookup"><span data-stu-id="69128-160">Client support</span></span>
* <span data-ttu-id="69128-161">API intuitive *: \* nx_dns_*</span><span class="sxs-lookup"><span data-stu-id="69128-161">Intuitive APIs: *nx_dns_\**</span></span>
* <span data-ttu-id="69128-162">MDN e DNS-SD sono disponibili solo con Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="69128-162">mDNS and DNS-SD are only available with Azure RTOS NetX Duo</span></span>

### <a name="p0p3"></a><span data-ttu-id="69128-163">P0P3</span><span class="sxs-lookup"><span data-stu-id="69128-163">P0P3</span></span>

* <span data-ttu-id="69128-164">Post Office Protocol versione 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="69128-164">Post Office Protocol Version 3 (POP3)</span></span>
* <span data-ttu-id="69128-165">Ingombro minimo 8,1 KB e 1,4 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="69128-165">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="69128-166">Supporto client</span><span class="sxs-lookup"><span data-stu-id="69128-166">Client support</span></span>
* <span data-ttu-id="69128-167">API P0P3 intuitive *: \* nx_pop3_*</span><span class="sxs-lookup"><span data-stu-id="69128-167">Intuitive P0P3 APIs: *nx_pop3_\**</span></span>

### <a name="telnet"></a><span data-ttu-id="69128-168">TELNET</span><span class="sxs-lookup"><span data-stu-id="69128-168">TELNET</span></span>

* <span data-ttu-id="69128-169">Ingombro minimo 0,5 KB e 0,3 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="69128-169">Minimal 0.5 KB and 0.3 KB RAM footprint</span></span>
* <span data-ttu-id="69128-170">Supporto per client e server</span><span class="sxs-lookup"><span data-stu-id="69128-170">Client and server support</span></span>
* <span data-ttu-id="69128-171">API Telnet intuitive *: \* nx_telnet_*</span><span class="sxs-lookup"><span data-stu-id="69128-171">Intuitive Telnet APIs: *nx_telnet_\**</span></span>

### <a name="ftp-tftp"></a><span data-ttu-id="69128-172">FTP, TFTP</span><span class="sxs-lookup"><span data-stu-id="69128-172">FTP, TFTP</span></span>

* <span data-ttu-id="69128-173">File Transfer Protocol (FTP)</span><span class="sxs-lookup"><span data-stu-id="69128-173">File Transfer Protocol (FTP)</span></span>
* <span data-ttu-id="69128-174">Trivial File Transfer Protocol (TFTP)</span><span class="sxs-lookup"><span data-stu-id="69128-174">Trivial File Transfer Protocol (TFTP)</span></span>
* <span data-ttu-id="69128-175">FTP minimo 1,8 KB a 7,2 KB FLASH, da 0,6 KB a 2,1 KB di impronta RAM</span><span class="sxs-lookup"><span data-stu-id="69128-175">FTP Minimal 1.8 KB to 7.2 KB FLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="69128-176">TFTP minimo 1,7 KB a 2,4 KB FLASH, 0,3 KB a 1,8 KB di RAM footprint</span><span class="sxs-lookup"><span data-stu-id="69128-176">TFTP Minimal 1.7 KB to 2.4 KB FLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="69128-177">Supporto per client e server</span><span class="sxs-lookup"><span data-stu-id="69128-177">Client and server support</span></span>
* <span data-ttu-id="69128-178">API FTP e TFTP intuitive *: \* nx_ftp_* o *nx_tftp_ \**</span><span class="sxs-lookup"><span data-stu-id="69128-178">Intuitive FTP and TFTP APIs: *nx_ftp_\** or *nx_tftp_\**</span></span>

### <a name="ppp-pppoe"></a><span data-ttu-id="69128-179">PPP, PPPoE</span><span class="sxs-lookup"><span data-stu-id="69128-179">PPP, PPPoE</span></span>

* <span data-ttu-id="69128-180">Protocollo bravo-to-PoInt (PPP)</span><span class="sxs-lookup"><span data-stu-id="69128-180">Polnt-to-PoInt Protocol (PPP)</span></span>
* <span data-ttu-id="69128-181">Point-to-Point Protocol su Ethernet (PPPoE)</span><span class="sxs-lookup"><span data-stu-id="69128-181">Point-to-Point Protocol over Ethernet(PPPoE)</span></span>
* <span data-ttu-id="69128-182">Ingombro minimo 7,1 KB e 3,8 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="69128-182">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="69128-183">API PPP intuitive *: \* nx_ppp_*</span><span class="sxs-lookup"><span data-stu-id="69128-183">Intuitive PPP APIs: *nx_ppp_\**</span></span>

* <span data-ttu-id="69128-184">PPPoE è disponibile solo con Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="69128-184">PPPoE is only available with Azure RTOS NetX Duo</span></span>

### <a name="sntp"></a><span data-ttu-id="69128-185">SNTP</span><span class="sxs-lookup"><span data-stu-id="69128-185">SNTP</span></span>

* <span data-ttu-id="69128-186">Simple Network Time Protocol (SNTP)</span><span class="sxs-lookup"><span data-stu-id="69128-186">Simple Network Time Protocol (SNTP)</span></span>
* <span data-ttu-id="69128-187">Minimo 4 KB e 0,5 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="69128-187">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="69128-188">Supporto client</span><span class="sxs-lookup"><span data-stu-id="69128-188">Client support</span></span>
* <span data-ttu-id="69128-189">API SNTP intuitive *: \* nx_sntp_*</span><span class="sxs-lookup"><span data-stu-id="69128-189">Intuitive SNTP APIs: *nx_sntp_\**</span></span>

### <a name="azure-rtos-netx-duo-api"></a><span data-ttu-id="69128-190">API di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="69128-190">Azure RTOS NetX Duo API</span></span>

* <span data-ttu-id="69128-191">API intuitiva e coerente</span><span class="sxs-lookup"><span data-stu-id="69128-191">Intuitive and consistent API</span></span>
* <span data-ttu-id="69128-192">Sostantivo-convenzione di denominazione dei verbi</span><span class="sxs-lookup"><span data-stu-id="69128-192">Noun-verb naming convention</span></span>
* <span data-ttu-id="69128-193">Implementazione API veloce, copia zero</span><span class="sxs-lookup"><span data-stu-id="69128-193">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="69128-194">Tutte le API hanno <i>nx_ \*</i> per identificare facilmente come Azure RTO NETX</span><span class="sxs-lookup"><span data-stu-id="69128-194">All APIs have leading <i>nx_\*</i> to easily identify as Azure RTOS NetX</span></span>
* <span data-ttu-id="69128-195">Le API di blocco hanno un timeout thread facoltativo</span><span class="sxs-lookup"><span data-stu-id="69128-195">Blocking APIs have optional thread timeout</span></span>
* <span data-ttu-id="69128-196">Per altri dettagli, vedere la [Guida dell'utente di Azure RTO NETX Duo](about-this-guide.md)</span><span class="sxs-lookup"><span data-stu-id="69128-196">See [Azure RTOS NetX Duo User Guide](about-this-guide.md) for more details</span></span>
* <span data-ttu-id="69128-197">Livello BSD facoltativo per il porting del codice socket legacy</span><span class="sxs-lookup"><span data-stu-id="69128-197">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp"></a><span data-ttu-id="69128-198">IGMP</span><span class="sxs-lookup"><span data-stu-id="69128-198">IGMP</span></span>

* <span data-ttu-id="69128-199">IGMP (Internet Group Management Protocol)</span><span class="sxs-lookup"><span data-stu-id="69128-199">Internet Group Management Protocol (IGMP)</span></span>
* <span data-ttu-id="69128-200">FLASH minimo 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="69128-200">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="69128-201">Supporto del gruppo multicast IPv4</span><span class="sxs-lookup"><span data-stu-id="69128-201">IPv4 multicast group support</span></span>
* <span data-ttu-id="69128-202">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="69128-202">IXIA IxANVL validated</span></span>
* <span data-ttu-id="69128-203">Statistiche IGMP facoltative</span><span class="sxs-lookup"><span data-stu-id="69128-203">Optional IGMP statistics</span></span>
* <span data-ttu-id="69128-204">Traccia a livello di sistema tramite Azure RTO ThreadX</span><span class="sxs-lookup"><span data-stu-id="69128-204">System-level trace via Azure RTOS ThreadX</span></span>
* <span data-ttu-id="69128-205">API IGMP intuitive *: \* nx_igmp_*</span><span class="sxs-lookup"><span data-stu-id="69128-205">Intuitive IGMP APIs: *nx_igmp_\**</span></span>

### <a name="azure-rtos-netx-secure-dtls"></a><span data-ttu-id="69128-206">Azure RTO NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="69128-206">Azure RTOS NetX Secure DTLS</span></span>

* <span data-ttu-id="69128-207">Datagramma Transport Layer Security (DTLS) 1,0 e 1,2</span><span class="sxs-lookup"><span data-stu-id="69128-207">Datagram Transport Layer Security (DTLS) 1.0 and 1.2</span></span>
* <span data-ttu-id="69128-208">FLASH minimo 11 KB</span><span class="sxs-lookup"><span data-stu-id="69128-208">Minimal 11 KB FLASH</span></span>
* <span data-ttu-id="69128-209">Fast, software RSA 2048 bit key size ~ 1 secondo @120MHz</span><span class="sxs-lookup"><span data-stu-id="69128-209">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="69128-210">Implementazione X. 509 semplificata</span><span class="sxs-lookup"><span data-stu-id="69128-210">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="69128-211">Completamente integrato con i socket UDP di Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="69128-211">Fully integrated with Azure RTOS NetX Duo UDP sockets</span></span>
* <span data-ttu-id="69128-212">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="69128-212">Hardware Crypto Support</span></span>
* <span data-ttu-id="69128-213">Supporto per la crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="69128-213">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="69128-214">Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse P-curve 192/224/256/384/521</span><span class="sxs-lookup"><span data-stu-id="69128-214">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="69128-215">Supporto della chiave crittografata (dipendente dall'hardware)</span><span class="sxs-lookup"><span data-stu-id="69128-215">Encrypted Key Support (hardware dependent)</span></span>

### <a name="azure-rtos-netx-secure-tls"></a><span data-ttu-id="69128-216">Azure RTO NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="69128-216">Azure RTOS NetX Secure TLS</span></span>

* <span data-ttu-id="69128-217">Transport Layer Security (TLS) 1,0, 1,1 e 1,2</span><span class="sxs-lookup"><span data-stu-id="69128-217">Transport Layer Security (TLS) 1.0, 1.1, and 1.2</span></span>
* <span data-ttu-id="69128-218">FLASH minimo 8,8 KB</span><span class="sxs-lookup"><span data-stu-id="69128-218">Minimal 8.8 KB FLASH</span></span>
* <span data-ttu-id="69128-219">Fast, software RSA 2048 bit key size ~ 1 secondo @120MHz</span><span class="sxs-lookup"><span data-stu-id="69128-219">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="69128-220">Implementazione X. 509 semplificata</span><span class="sxs-lookup"><span data-stu-id="69128-220">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="69128-221">Completamente integrato con i socket TCP RTO NetX duo di Azure</span><span class="sxs-lookup"><span data-stu-id="69128-221">Fully integrated with Azure RTOS NetX Duo TCP sockets</span></span>
* <span data-ttu-id="69128-222">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="69128-222">Hardware Crypto Support</span></span>
* <span data-ttu-id="69128-223">Supporto per la crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="69128-223">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="69128-224">Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse P-curve 192/224/256/384/521</span><span class="sxs-lookup"><span data-stu-id="69128-224">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="69128-225">Supporto della chiave crittografata (dipendente dall'hardware)</span><span class="sxs-lookup"><span data-stu-id="69128-225">Encrypted Key Support (hardware dependent)</span></span>

### <a name="icmp"></a><span data-ttu-id="69128-226">ICMP</span><span class="sxs-lookup"><span data-stu-id="69128-226">ICMP</span></span>

* <span data-ttu-id="69128-227">Internet Control Message Protocol (ICMP)</span><span class="sxs-lookup"><span data-stu-id="69128-227">Internet Control Message Protocol (ICMP)</span></span>
* <span data-ttu-id="69128-228">FLASH minimo 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="69128-228">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="69128-229">Supporto per IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="69128-229">IPv4 and IPv6 support</span></span>
* <span data-ttu-id="69128-230">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="69128-230">IXIA IxANVL validated</span></span>
* <span data-ttu-id="69128-231">Ping richiesta e risposta ping</span><span class="sxs-lookup"><span data-stu-id="69128-231">Ping request and ping response</span></span>
* <span data-ttu-id="69128-232">Sospensione thread facoltativa sulle richieste ping</span><span class="sxs-lookup"><span data-stu-id="69128-232">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="69128-233">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="69128-233">Optional timeout on all suspension</span></span>
* <span data-ttu-id="69128-234">Statistiche ICMP facoltative</span><span class="sxs-lookup"><span data-stu-id="69128-234">Optional ICMP statistics</span></span>
* <span data-ttu-id="69128-235">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="69128-235">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="69128-236">API ICMP intuitive *: \* nx_icmp_*</span><span class="sxs-lookup"><span data-stu-id="69128-236">Intuitive ICMP APIs: *nx_icmp_\**</span></span>

### <a name="udp"></a><span data-ttu-id="69128-237">UDP</span><span class="sxs-lookup"><span data-stu-id="69128-237">UDP</span></span>

* <span data-ttu-id="69128-238">UDP (User Datagram Protocol)</span><span class="sxs-lookup"><span data-stu-id="69128-238">User Datagram Protocol (UDP)</span></span>
* <span data-ttu-id="69128-239">Minimo 2,5 KB di FLASH, 124 socket byte di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="69128-239">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="69128-240">Elaborazione di pacchetti TCP veloce, near wirespeed:</span><span class="sxs-lookup"><span data-stu-id="69128-240">Fast, near wirespeed TCP packet processing:</span></span>
    * <span data-ttu-id="69128-241">RX 95 Mbps su Ethernet a 100 Mbps, MCU @100MHz , 14% di utilizzo di MCU</span><span class="sxs-lookup"><span data-stu-id="69128-241">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU utilization</span></span>
    * <span data-ttu-id="69128-242">TX 94 Mbps a 100 Mbps Ethernet, MCU @100MHz , 10% di utilizzo di MCU</span><span class="sxs-lookup"><span data-stu-id="69128-242">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU utilization</span></span>
* <span data-ttu-id="69128-243">Percorso rapido UDP™ tecnologia</span><span class="sxs-lookup"><span data-stu-id="69128-243">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="69128-244">Nessun limite al numero di UDP</span><span class="sxs-lookup"><span data-stu-id="69128-244">No limits on the number of UDP</span></span>
* <span data-ttu-id="69128-245">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="69128-245">IXIA IxANVL validated</span></span>
* <span data-ttu-id="69128-246">Sospensione facoltativa per ricezione socket</span><span class="sxs-lookup"><span data-stu-id="69128-246">Optional suspension on socket receive</span></span>
* <span data-ttu-id="69128-247">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="69128-247">Optional timeout on all suspension</span></span>
* <span data-ttu-id="69128-248">Statistiche UDP facoltative</span><span class="sxs-lookup"><span data-stu-id="69128-248">Optional UDP statistics</span></span>
* <span data-ttu-id="69128-249">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="69128-249">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="69128-250">API UDP intuitive *: \* nx_udp_*</span><span class="sxs-lookup"><span data-stu-id="69128-250">Intuitive UDP APIs: *nx_udp_\**</span></span>

### <a name="tcp"></a><span data-ttu-id="69128-251">TCP</span><span class="sxs-lookup"><span data-stu-id="69128-251">TCP</span></span>

* <span data-ttu-id="69128-252">Transmission Control Protocol (TCP)</span><span class="sxs-lookup"><span data-stu-id="69128-252">Transmission Control Protocol (TCP)</span></span>
* <span data-ttu-id="69128-253">Minimo da 10.5 K8 a 12,5 KB di FLASH, 280 byte di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="69128-253">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="69128-254">Elaborazione di pacchetti TCP veloce, near wlrespeed:</span><span class="sxs-lookup"><span data-stu-id="69128-254">Fast, near wlrespeed TCP packet processing:</span></span>
    * <span data-ttu-id="69128-255">RX 93 Mbps su Ethernet a 100 Mbps, MCU @100MHz , utilizzo di MCU del 20%</span><span class="sxs-lookup"><span data-stu-id="69128-255">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU utilization</span></span>
    * <span data-ttu-id="69128-256">TX 94 Mbps su Ethernet a 100 Mbps, MCU @100MHz , utilizzo di MCU del 27%</span><span class="sxs-lookup"><span data-stu-id="69128-256">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU utilization</span></span>
* <span data-ttu-id="69128-257">Connessione affidabile</span><span class="sxs-lookup"><span data-stu-id="69128-257">Reliable connection</span></span>
* <span data-ttu-id="69128-258">Nessun limite al numero di socket TCP</span><span class="sxs-lookup"><span data-stu-id="69128-258">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="69128-259">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="69128-259">IXIA IxANVL validated</span></span>
* <span data-ttu-id="69128-260">Sospensione facoltativa per ricezione/trasmissione socket</span><span class="sxs-lookup"><span data-stu-id="69128-260">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="69128-261">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="69128-261">Optional timeout on all suspension</span></span>
* <span data-ttu-id="69128-262">Statistiche TCP facoltative</span><span class="sxs-lookup"><span data-stu-id="69128-262">Optional TCP statistics</span></span>
* <span data-ttu-id="69128-263">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="69128-263">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="69128-264">API TCP intuitive *: \* nx_tcp_*</span><span class="sxs-lookup"><span data-stu-id="69128-264">Intuitive TCP APIs: *nx_tcp_\**</span></span>

### <a name="arprarp"></a><span data-ttu-id="69128-265">ARP/RARP</span><span class="sxs-lookup"><span data-stu-id="69128-265">ARP/RARP</span></span>

* <span data-ttu-id="69128-266">ARP (Address Resolution Protocol)</span><span class="sxs-lookup"><span data-stu-id="69128-266">Address Resolution Protocol (ARP)</span></span>
* <span data-ttu-id="69128-267">Protocollo RARP (Reverse Address Resolution Protocol)</span><span class="sxs-lookup"><span data-stu-id="69128-267">Reverse Address Resolution Protocol (RARP)</span></span>
* <span data-ttu-id="69128-268">Minimo 1,7 KB di memoria, dimensioni RAM</span><span class="sxs-lookup"><span data-stu-id="69128-268">Minimal 1.7 KB FLASH, RAM size</span></span>
* <span data-ttu-id="69128-269">Risoluzione dinamica degli indirizzi MAC 32-BLT IPv4 e 48-BLT</span><span class="sxs-lookup"><span data-stu-id="69128-269">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses</span></span>
* <span data-ttu-id="69128-270">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="69128-270">IXIA IxANVL validated</span></span>
* <span data-ttu-id="69128-271">Cache ARP flessibile definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="69128-271">Flexible, user-defined ARP cache</span></span>
* <span data-ttu-id="69128-272">Supporto ARP gratuito</span><span class="sxs-lookup"><span data-stu-id="69128-272">Gratuitous ARP support</span></span>
* <span data-ttu-id="69128-273">Statistiche ARP/RARP facoltative determinate dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="69128-273">Optional ARP/RARP statistics determined by application</span></span>
* <span data-ttu-id="69128-274">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="69128-274">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="69128-275">API ARP/RARP intuitive *: \* nx_arp_*, *nx_rarp_ \**</span><span class="sxs-lookup"><span data-stu-id="69128-275">Intuitive ARP/RARP APIs: *nx_arp_\**, *nx_rarp_\**</span></span>

### <a name="ipv4-amp-ipv6"></a><span data-ttu-id="69128-276">&amp;IPv6 IPv4</span><span class="sxs-lookup"><span data-stu-id="69128-276">IPv4 &amp; IPv6</span></span>

* <span data-ttu-id="69128-277">Protocollo IP (Internet Protocol)</span><span class="sxs-lookup"><span data-stu-id="69128-277">Internet Protocol (IP)</span></span>
* <span data-ttu-id="69128-278">Minimo 3,5 KB a 8,5 KB FLASH, da 2 KB a 3 KB di impronta RAM</span><span class="sxs-lookup"><span data-stu-id="69128-278">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint</span></span>
* <span data-ttu-id="69128-279">Architettura™ piconet</span><span class="sxs-lookup"><span data-stu-id="69128-279">Piconet™ architecture</span></span>
* <span data-ttu-id="69128-280">Prestazioni veloci, near wirespeed</span><span class="sxs-lookup"><span data-stu-id="69128-280">Fast, near wirespeed performance</span></span>
* <span data-ttu-id="69128-281">Supporto di più interfacce</span><span class="sxs-lookup"><span data-stu-id="69128-281">Multiple interface support</span></span>
* <span data-ttu-id="69128-282">Supporto multihomed</span><span class="sxs-lookup"><span data-stu-id="69128-282">Multihomed support</span></span>
* <span data-ttu-id="69128-283">Supporto del routing statico</span><span class="sxs-lookup"><span data-stu-id="69128-283">Static routing support</span></span>
* <span data-ttu-id="69128-284">Supporto per la frammentazione e il riassemblaggio IP</span><span class="sxs-lookup"><span data-stu-id="69128-284">IP fragmentation/reassembly support</span></span>
* <span data-ttu-id="69128-285">Supporto degli indirizzi IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="69128-285">IPv4 and IPv6 address support</span></span>
* <span data-ttu-id="69128-286">IxANVL di IXIA convalidati</span><span class="sxs-lookup"><span data-stu-id="69128-286">IXIA IxANVL validated</span></span>
* <span data-ttu-id="69128-287">Certificazione del logo pronto per la fase II IPv6</span><span class="sxs-lookup"><span data-stu-id="69128-287">Phase II IPv6 Ready Logo Certification</span></span>
* <span data-ttu-id="69128-288">Statistiche IP facoltative</span><span class="sxs-lookup"><span data-stu-id="69128-288">Optional IP statistics</span></span>
* <span data-ttu-id="69128-289">Interfaccia del driver del livello fisico intuitiva e ben definita</span><span class="sxs-lookup"><span data-stu-id="69128-289">Well defined, intuitive physical layer driver interface</span></span>
* <span data-ttu-id="69128-290">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="69128-290">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="69128-291">API del livello IP intuitive: *\* nx_ip_*, *nxd_ip_ \**, *nxd_ipv6_ \**</span><span class="sxs-lookup"><span data-stu-id="69128-291">Intuitive IP layer APIs: *nx_ip_\**, *nxd_ip_\**, *nxd_ipv6_\**</span></span>
* <span data-ttu-id="69128-292">Pre-certificati da TUV e UL a IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D e EN 50128 SW-SIL4</span><span class="sxs-lookup"><span data-stu-id="69128-292">Pre-certified by TUV and UL to IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D, and EN 50128 SW-SIL4</span></span>

### <a name="azure-rtos-netx-secure-ipsec"></a><span data-ttu-id="69128-293">IPSEC protetto da Azure RTO NetX</span><span class="sxs-lookup"><span data-stu-id="69128-293">Azure RTOS NetX Secure IPSEC</span></span>

* <span data-ttu-id="69128-294">IPSEC (Internet Protocol Security)</span><span class="sxs-lookup"><span data-stu-id="69128-294">Internet Protocol Security (IPSEC)</span></span>
* <span data-ttu-id="69128-295">Livello IP</span><span class="sxs-lookup"><span data-stu-id="69128-295">IP layer</span></span>
* <span data-ttu-id="69128-296">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="69128-296">Hardware crypto support</span></span>
* <span data-ttu-id="69128-297">Supporto per la crittografia software, tra cui:</span><span class="sxs-lookup"><span data-stu-id="69128-297">Software crypto support, including:</span></span>
    * <span data-ttu-id="69128-298">DES, 3DES</span><span class="sxs-lookup"><span data-stu-id="69128-298">DES, 3DES</span></span>
    * <span data-ttu-id="69128-299">AES</span><span class="sxs-lookup"><span data-stu-id="69128-299">AES</span></span>
    * <span data-ttu-id="69128-300">HMAC-MD5</span><span class="sxs-lookup"><span data-stu-id="69128-300">HMAC-MD5</span></span>
    * <span data-ttu-id="69128-301">HMAC-SHA1</span><span class="sxs-lookup"><span data-stu-id="69128-301">HMAC-SHA1</span></span>
* <span data-ttu-id="69128-302">Supporto di protocollo IKE (IKE) versione 2</span><span class="sxs-lookup"><span data-stu-id="69128-302">Internet Key Exchange (IKE) Version 2 support</span></span>
* <span data-ttu-id="69128-303">API IPsec intuitive *: \* nx_ipsec_*</span><span class="sxs-lookup"><span data-stu-id="69128-303">Intuitive IPsec APIs: *nx_ipsec_\**</span></span>
* <span data-ttu-id="69128-304">IPsec è disponibile solo con Azure RTO NetX Duo</span><span class="sxs-lookup"><span data-stu-id="69128-304">IPsec is only available with Azure RTOS NetX Duo</span></span>

## <a name="small-footprint"></a><span data-ttu-id="69128-305">Footprint ridotto</span><span class="sxs-lookup"><span data-stu-id="69128-305">Small-footprint</span></span>

<span data-ttu-id="69128-306">Azure RTO NetX Duo presenta un footprint notevolmente ridotto da 9 KB a 15 KB per il supporto di base per IP e UDP.</span><span class="sxs-lookup"><span data-stu-id="69128-306">Azure RTOS NetX Duo has a remarkably small footprint of 9 KB to 15 KB for basic IP and UDP support.</span></span> <span data-ttu-id="69128-307">Per la funzionalità TCP sono necessari altri 10 KB a 13 KB di memoria per l'area di istruzione.</span><span class="sxs-lookup"><span data-stu-id="69128-307">An additional 10 KB to 13 KB of instruction area memory is needed for TCP functionality.</span></span> <span data-ttu-id="69128-308">L'utilizzo della RAM di Azure RTO NetX Duo è generalmente compreso tra 2,6 KB e 3,6 KB oltre alla memoria del pool di pacchetti, definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="69128-308">Azure RTOS NetX Duo RAM usage typically ranges from 2.6 KB to 3.6 KB plus the packet pool memory, which is defined by the application.</span></span> <span data-ttu-id="69128-309">Come Azure RTO ThreadX, le dimensioni di Azure RTO NetX Duo vengono ridimensionate automaticamente in base ai servizi usati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="69128-309">Like Azure RTOS ThreadX, the size of Azure RTOS NetX Duo automatically scales based on the services used by the application.</span></span> <span data-ttu-id="69128-310">In questo modo si eliminano praticamente la necessità di complicati parametri di configurazione e di compilazione, semplificando le operazioni per lo sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="69128-310">This virtually eliminates the need for complicated configuration and build parameters, making things easier for the developer.</span></span>

## <a name="fast-execution"></a><span data-ttu-id="69128-311">Esecuzione rapida</span><span class="sxs-lookup"><span data-stu-id="69128-311">Fast execution</span></span>

<span data-ttu-id="69128-312">Azure RTO NetX Duo fornisce un'implementazione di invio/ricezione di pacchetti con copia zero, altamente integrata con Azure RTO ThreadX, per ottenere le prestazioni più rapide possibile.</span><span class="sxs-lookup"><span data-stu-id="69128-312">Azure RTOS NetX Duo provides a zero-copy packet send/receive implementation, highly integrated with Azure RTOS ThreadX, to achieve the fastest possible performance.</span></span> <span data-ttu-id="69128-313">Ad esempio, Azure RTO NetX Duo può in genere ottenere trasferimenti di dati near wirespeed su un processore 80 MHz (o meno), usando solo una piccola percentuale dei cicli del processore.</span><span class="sxs-lookup"><span data-stu-id="69128-313">For example, Azure RTOS NetX Duo can typically achieve near wirespeed data transfers on an 80 MHz (or less) processor, while using only a small percentage of the processor cycles.</span></span>

## <a name="simple-easy-to-use"></a><span data-ttu-id="69128-314">Semplice e facile da usare</span><span class="sxs-lookup"><span data-stu-id="69128-314">Simple, easy-to-use</span></span>

<span data-ttu-id="69128-315">L'API di Azure RTO NetX Duo è intuitiva, semplice e altamente funzionale.</span><span class="sxs-lookup"><span data-stu-id="69128-315">The Azure RTOS NetX Duo API is intuitive, straightforward,  and highly functional.</span></span>

<span data-ttu-id="69128-316">I nomi delle API sono costituiti da parole reali e non da "zuppa alfabetica" o nomi altamente abbreviati, così comuni in altri prodotti di rete.</span><span class="sxs-lookup"><span data-stu-id="69128-316">The API names are made of real words and not the “alphabet soup” or highly abbreviated names that are so common in other networking products.</span></span> <span data-ttu-id="69128-317">Tutte le API di Azure RTO NetX Duo hanno un *nx_* leader e seguono una convenzione di denominazione sostantivo-verbo.</span><span class="sxs-lookup"><span data-stu-id="69128-317">All Azure RTOS NetX Duo APIs have a leading *nx_* and follow a noun-verb naming convention.</span></span> <span data-ttu-id="69128-318">Inoltre, esiste una coerenza funzionale nell'API.</span><span class="sxs-lookup"><span data-stu-id="69128-318">Furthermore, there is a functional consistency throughout the API.</span></span> <span data-ttu-id="69128-319">Tutte le funzioni API che sospendono, ad esempio, hanno un timeout facoltativo che funziona in modo identico.</span><span class="sxs-lookup"><span data-stu-id="69128-319">For example, all API functions that suspend have an optional timeout that operates in an identical manner.</span></span>

<span data-ttu-id="69128-320">Per le applicazioni legacy, Azure RTO NetX Duo offre un ulteriore livello compatibile con socket BSD.</span><span class="sxs-lookup"><span data-stu-id="69128-320">For legacy applications, Azure RTOS NetX Duo offers an additional BSD socket compatible layer.</span></span> <span data-ttu-id="69128-321">Questo livello consente agli sviluppatori di eseguire facilmente la migrazione di applicazioni di rete di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="69128-321">This layer helps developers migrate large networking applications with ease.</span></span>

## <a name="safe-and-secure"></a><span data-ttu-id="69128-322">Sicuro e sicuro</span><span class="sxs-lookup"><span data-stu-id="69128-322">Safe and secure</span></span>

<span data-ttu-id="69128-323">Azure RTO NetX Duo è sicuro.</span><span class="sxs-lookup"><span data-stu-id="69128-323">Azure RTOS NetX Duo is secure.</span></span> <span data-ttu-id="69128-324">Questa sicurezza viene fornita tramite i prodotti per la sicurezza dei componenti aggiuntivi, tra cui IPsec, SSL, TLS e DTLS.</span><span class="sxs-lookup"><span data-stu-id="69128-324">This security is provided through add-on security products, including IPsec, SSL, TLS, and DTLS.</span></span> <span data-ttu-id="69128-325">Inoltre, l'applicazione ha il controllo completo su tutti gli accessi esterni ad Azure RTO NetX Duo, rendendo molto più semplice la determinazione dei rischi per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="69128-325">Also, the application has complete control over all external access to Azure RTOS NetX Duo, making security risk determination much easier.</span></span>

<span data-ttu-id="69128-326">Microsoft Azure RTO fornisce agli OEM i componenti per proteggere le comunicazioni e creare codice e isolamento dei dati utilizzando meccanismi di protezione hardware MCU/MPU sottostanti.</span><span class="sxs-lookup"><span data-stu-id="69128-326">Microsoft Azure RTOS provides OEMs with components to secure communication and to create code and data isolation using underlying MCU/MPU hardware protection mechanisms.</span></span> <span data-ttu-id="69128-327">È in definitiva responsabilità del generatore di dispositivi verificare che il dispositivo soddisfi pienamente i requisiti di sicurezza in evoluzione associati al caso d'uso specifico.</span><span class="sxs-lookup"><span data-stu-id="69128-327">It is ultimately the responsibility of the device builder to ensure the device fully meets the evolving security requirements associated with its specific use case.</span></span>

## <a name="pre-certified--by-tuv-and-ul-to-many-safety-standards"></a><span data-ttu-id="69128-328">Pre-certificati da TUV e UL a molti standard di sicurezza</span><span class="sxs-lookup"><span data-stu-id="69128-328">Pre-certified  by TUV and UL to many safety standards</span></span>

<span data-ttu-id="69128-329">Azure RTO NetX Duo è stato certificato da SGS-TUV Saar per l'uso nei sistemi critici per la sicurezza, in base alla classe IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 ASIL D e EN 50128.</span><span class="sxs-lookup"><span data-stu-id="69128-329">Azure RTOS NetX Duo has been certified by SGS-TUV  Saar for use in safety-critical systems, according to IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 ASIL D and EN 50128.</span></span> <span data-ttu-id="69128-330">La certificazione conferma che è possibile usare Azure RTO NetX Duo per lo sviluppo di software correlati alla sicurezza per i livelli di integrità di sicurezza più elevati di IEC-61508, IEC-62304, ISO 26262 e EN 50128 per la "protezione funzionale dei sistemi elettronici di sicurezza elettronica, elettronici e programmabili".</span><span class="sxs-lookup"><span data-stu-id="69128-330">The certification confirms that Azure RTOS NetX Duo can be used in the development of safety-related software for the highest safety integrity levels of IEC-61508, IEC-62304, ISO 26262 and EN 50128 for the “Functional Safety of electrical, electronic, and programmable electronic safety-related systems.”</span></span> <span data-ttu-id="69128-331">SGS-TUV Saar, costituito da una joint venture del SGS-Group e del TUV del Regno Unito, è diventato la società leader accreditata e indipendente per il test, il controllo, la verifica e la certificazione del software incorporato per i sistemi correlati alla sicurezza in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="69128-331">SGS-TUV Saar, formed through a joint venture of Germany’s SGS-Group and TUV Saarland, has become the leading accredited, independent company for testing, auditing, verifying, and certifying embedded software for safety-related systems worldwide.</span></span> <span data-ttu-id="69128-332">Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, tra cui IEC-62304, ISO 26262 e EN 50128, vengono usati per garantire la protezione funzionale di dispositivi medicali elettrici, elettronici e programmabili per la sicurezza elettronica, sistemi di controllo dei processi, macchinari industriali, automobili e sistemi di controllo ferroviario.</span><span class="sxs-lookup"><span data-stu-id="69128-332">The industrial safety standard IEC 61508, and all standards that are derived from it, including IEC-62304, ISO 26262 and EN 50128, are used to assure the functional safety of electrical, electronic, and programmable electronic safety-related medical devices, process control systems, industrial machinery, automobiles and railway control systems.</span></span>

:::image type="content" source="media/overview-netx-duo/partener-logo-sgs-tuv-saar.png" alt-text="SGS-certificazione TUV":::

<span data-ttu-id="69128-334">Azure RTO NetX Duo è stato riconosciuto da UL per conformità con UL 60730-1 allegato H, CSA E60730-1 allegato H, IEC 60730-1 allegato H, UL 60335-1 allegato R, IEC 60335-1 allegato R e UL 1998 sicurezza standard per il software in componenti programmabili.</span><span class="sxs-lookup"><span data-stu-id="69128-334">Azure RTOS NetX Duo has been recognized by UL for compliance with UL 60730-1 Annex H, CSA E60730-1 Annex H, IEC 60730-1 Annex H, UL 60335-1 Annex R, IEC 60335-1 Annex R, and UL 1998 safety standards for software in programmable components.</span></span> <span data-ttu-id="69128-335">UL è una società globale, indipendente e scientifica per la sicurezza, con più di un secolo di competenze innovative per l'innovazione delle soluzioni di sicurezza, che vanno dall'adozione pubblica di energia elettrica ai progressi della sostenibilità, dell'energia rinnovabile e della nanotecnologia.</span><span class="sxs-lookup"><span data-stu-id="69128-335">UL is a global, independent, safety-science company with more than a century of expertise innovating safety solutions, ranging from the public adoption of electricity to breakthroughs in sustainability, renewable energy, and nanotechnology.</span></span>

:::image type="content" source="media/overview-netx-duo/cru-logo-certification.png" alt-text="Certificazione CRU UL":::

<span data-ttu-id="69128-337">Gli artefatti (certificato, manuale di sicurezza, report di test e così via) associati alle certificazioni TUV e UL sono disponibili per la vendita.</span><span class="sxs-lookup"><span data-stu-id="69128-337">Artifacts (Certificate, Safety Manual, Test Report, etc.) associated with the TUV and UL certifications are available for sale.</span></span>

<span data-ttu-id="69128-338">Nei casi in cui l'applicazione necessita di ulteriore certificazione, un servizio di certificazione è disponibile tramite Microsoft per fornire la certificazione chiavi in volta a diversi standard usando la piattaforma hardware effettiva e persino coprendo il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="69128-338">In cases where the application needs additional certification, a certification service is available through Microsoft for providing turn-key certification to various standards using the actual hardware platform and even covering the application code.</span></span> <span data-ttu-id="69128-339">Per ulteriori informazioni sul servizio di certificazione, contattare Microsoft.</span><span class="sxs-lookup"><span data-stu-id="69128-339">Contact us for more details on our certification service.</span></span>

## <a name="eal4-common-criteria-security-certification"></a><span data-ttu-id="69128-340">EAL4 + criteri comuni certificazione di sicurezza</span><span class="sxs-lookup"><span data-stu-id="69128-340">EAL4+ Common Criteria security certification</span></span>

<span data-ttu-id="69128-341">Azure RTO ha raggiunto la certificazione di sicurezza EAL4 + Common Criteria.</span><span class="sxs-lookup"><span data-stu-id="69128-341">Azure RTOS has achieved EAL4+ Common Criteria security certification.</span></span> <span data-ttu-id="69128-342">La destinazione di valutazione (TOE) copre Azure RTO ThreadX, Azure RTO NetX Duo, Azure RTO NetX Secure TLS e Azure RTO NETX MQTT.</span><span class="sxs-lookup"><span data-stu-id="69128-342">The Target of Evalution (TOE) covers Azure RTOS ThreadX, Azure RTOS NetX Duo, Azure RTOS NetX Secure TLS, and Azure RTOS NetX MQTT.</span></span> <span data-ttu-id="69128-343">Questo rappresenta i protocolli più tipici necessari per i sensori, i dispositivi, i router perimetrali e i gateway con incorporate profondità.</span><span class="sxs-lookup"><span data-stu-id="69128-343">This represents the most typical IoT protocols required by deeply embedded sensors, devices, edge routers, and gateways.</span></span>

:::image type="content" source="media/overview-netx-duo/eal-logo-certification.png" alt-text="Certificazione EAL":::

<span data-ttu-id="69128-345">La funzionalità di valutazione della sicurezza IT utilizzata per la Microsoft Azure certificazione di sicurezza RTO SC è BrightSight BV e l'autorità di certificazione è SERTIT.</span><span class="sxs-lookup"><span data-stu-id="69128-345">The IT Security Evaluation Facility used for the Microsoft Azure RTOS SC security certification is Brightsight BV and the Certification Authority is SERTIT.</span></span>

## <a name="fips-140-2-validated"></a><span data-ttu-id="69128-346">FIPS 140-2 convalidato</span><span class="sxs-lookup"><span data-stu-id="69128-346">FIPS 140-2 Validated</span></span>

<span data-ttu-id="69128-347">Le librerie di crittografia NetX di Azure RTO hanno avuto la certificazione Federal Information Processing Standard 140-2 (FIPS 140-2) per il software, che specifica i requisiti per i moduli di crittografia.</span><span class="sxs-lookup"><span data-stu-id="69128-347">Azure RTOS NetX Crypto libraries have achieved Federal Information Processing Standardization 140-2 (FIPS 140-2) Certification for software, which specifies requirements for cryptography modules.</span></span> <span data-ttu-id="69128-348">FIPS 140-2 richiede che tutti gli enti governativi federali e i reparti che utilizzano la sicurezza basata su crittografia siano in grado di soddisfare standard specifici relativi alla forza e alle funzionalità di crittografia.</span><span class="sxs-lookup"><span data-stu-id="69128-348">FIPS 140-2 requires all federal government agencies and departments that use cryptographic-based security to meet specific standards related to encryption strength and capabilities.</span></span> <span data-ttu-id="69128-349">Questi standard di sicurezza basati su crittografia sono riconosciuti anche in Canada e nell'Unione europea.</span><span class="sxs-lookup"><span data-stu-id="69128-349">These cryptographic-based security standards are also recognized in Canada and the European Union.</span></span>

<span data-ttu-id="69128-350">Il Lab di valutazione della sicurezza delle informazioni usato per le librerie di crittografia NetX di Azure RTO è atsec e l'autorità di certificazione è il National Institute of Standards and Technology (NIST).</span><span class="sxs-lookup"><span data-stu-id="69128-350">The Information Security evaluation lab used for Azure RTOS NetX Crypto libraries was atsec and the certification authority is The National Institute of Standards and Technology (NIST).</span></span> <span data-ttu-id="69128-351">Per ulteriori informazioni, vedere il [sito Web del NIST](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3394) .</span><span class="sxs-lookup"><span data-stu-id="69128-351">Review the [NIST website](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3394) for additional details.</span></span>

## <a name="interoperability-verification"></a><span data-ttu-id="69128-352">Verifica dell'interoperabilità</span><span class="sxs-lookup"><span data-stu-id="69128-352">Interoperability verification</span></span>

<span data-ttu-id="69128-353">NetX Duo è conforme agli standard RFC e offre un'interoperabilità completa con i dispositivi per la maggior parte dei fornitori.</span><span class="sxs-lookup"><span data-stu-id="69128-353">NetX Duo conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span>

![Logo pronto per IPv6](./media/overview-netx-duo/ipv6-ready-logo.png)

<span data-ttu-id="69128-355">Azure RTO NetX Duo è uno degli unici stack TCP/IP incorporati per ottenere la rigorosa certificazione del logo IPv6-Ready, prova che ha superato i test di conformità e interoperabilità, gestiti e convalidati dal forum di IPv6.</span><span class="sxs-lookup"><span data-stu-id="69128-355">Azure RTOS NetX Duo is one of the only embedded TCP/IP stacks to achieve the rigorous IPv6-Ready Logo certification, evidence that it has passed conformance and interoperability tests, administered and validated by the IPv6 Forum.</span></span> <span data-ttu-id="69128-356">NetX Duo usa anche il IxANVL (Automatic Network Validation Library) standard del settore per l'implementazione del protocollo TCP/IP di NetX Duo Core.</span><span class="sxs-lookup"><span data-stu-id="69128-356">NetX Duo also utilizes the industry standard IxANVL (Automated Network Validation Library) for the NetX Duo core TCP/IP protocol implementation.</span></span>

## <a name="comprehensive-iot-solution"></a><span data-ttu-id="69128-357">Soluzione completa</span><span class="sxs-lookup"><span data-stu-id="69128-357">Comprehensive IoT solution</span></span>

<span data-ttu-id="69128-358">Azure RTO NetX Duo presenta un footprint notevolmente ridotto da 9 KB a 15 KB per il supporto di base per IP e UDP.</span><span class="sxs-lookup"><span data-stu-id="69128-358">Azure RTOS NetX Duo has a remarkably small footprint of 9 KB to 15 KB for basic IP and UDP support.</span></span> <span data-ttu-id="69128-359">NetX duo ha una delle reti TCP/IP più complete per le applicazioni per le cose estremamente incorporate.</span><span class="sxs-lookup"><span data-stu-id="69128-359">NetX Duo has one of the most comprehensive TCP/IP networking for deeply embedded IoT applications.</span></span> <span data-ttu-id="69128-360">Questo supporto include i prodotti del protocollo aggiuntivo seguenti:</span><span class="sxs-lookup"><span data-stu-id="69128-360">This support includes the following add-on protocol products:</span></span>

<span data-ttu-id="69128-361">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPsec, AutoIP, DHCP, DNS, MDN, DNS-SD, FTP, HTTP, IPsec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span><span class="sxs-lookup"><span data-stu-id="69128-361">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPsec, AutoIP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPsec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="69128-362">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="69128-362">Advanced technology</span></span>

<span data-ttu-id="69128-363">Azure RTO NetX Duo è una tecnologia avanzata che include:</span><span class="sxs-lookup"><span data-stu-id="69128-363">Azure RTOS NetX Duo is advanced technology that includes:</span></span>

* <span data-ttu-id="69128-364">Architettura™ piconet</span><span class="sxs-lookup"><span data-stu-id="69128-364">Piconet™ architecture</span></span>
* <span data-ttu-id="69128-365">Scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="69128-365">Automatic scaling</span></span>
* <span data-ttu-id="69128-366">Tecnologia Fast-Path UDP™</span><span class="sxs-lookup"><span data-stu-id="69128-366">UDP Fast-Path Technology™</span></span>
* <span data-ttu-id="69128-367">Gestione flessibile dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="69128-367">Flexible packet management</span></span>
* <span data-ttu-id="69128-368">API di copia zero e implementazione</span><span class="sxs-lookup"><span data-stu-id="69128-368">Zero-copy API and implementation</span></span>
* <span data-ttu-id="69128-369">Supporto multihomed</span><span class="sxs-lookup"><span data-stu-id="69128-369">Multihomed support</span></span>
* <span data-ttu-id="69128-370">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="69128-370">Optional timeout on all suspension</span></span>
* <span data-ttu-id="69128-371">Supporto del routing statico</span><span class="sxs-lookup"><span data-stu-id="69128-371">Static routing support</span></span>
* <span data-ttu-id="69128-372">IPsec</span><span class="sxs-lookup"><span data-stu-id="69128-372">IPsec</span></span>
* <span data-ttu-id="69128-373">SSL/TLS/DTLS</span><span class="sxs-lookup"><span data-stu-id="69128-373">SSL/TLS/DTLS</span></span>
* <span data-ttu-id="69128-374">Supporto per l'analisi del sistema TraceX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="69128-374">Azure RTOS TraceX system analysis support</span></span>

## <a name="fastest-time-to-market"></a><span data-ttu-id="69128-375">Time-to-market più veloce</span><span class="sxs-lookup"><span data-stu-id="69128-375">Fastest time-to-market</span></span>

<span data-ttu-id="69128-376">Azure RTO NetX Duo è facile da installare, apprendere, usare, eseguire il debug, verificare, certificare e gestire.</span><span class="sxs-lookup"><span data-stu-id="69128-376">Azure RTOS NetX Duo is easy to install, learn, use, debug, verify, certify and maintain.</span></span> <span data-ttu-id="69128-377">Di conseguenza, NetX Duo è uno degli stack TCP/IP più diffusi per i dispositivi di Internet delle cose incorporate, inclusi molti SoC da Broadcom, GainSpan e così via. Il nostro vantaggio di time-to-Market coerente è basato su:</span><span class="sxs-lookup"><span data-stu-id="69128-377">As a result, NetX Duo is one of the most popular TCP/IP stacks for embedded IoT devices, including many SoCs from Broadcom, Gainspan, etc. Our consistent time-to-market advantage is built on:</span></span>

* <span data-ttu-id="69128-378">Documentazione relativa alla qualità: esaminare la guida per l' [utente di Azure RTO NETX Duo](about-this-guide.md) e vedere per se stessi.</span><span class="sxs-lookup"><span data-stu-id="69128-378">Quality documentation – please review our [Azure RTOS NetX Duo User Guide](about-this-guide.md) and see for yourself!</span></span>
* <span data-ttu-id="69128-379">Disponibilità del codice sorgente completa</span><span class="sxs-lookup"><span data-stu-id="69128-379">Complete source code availability</span></span>
* <span data-ttu-id="69128-380">API di facile utilizzo</span><span class="sxs-lookup"><span data-stu-id="69128-380">Easy-to-use API</span></span>
* <span data-ttu-id="69128-381">Set di funzionalità completo e avanzato</span><span class="sxs-lookup"><span data-stu-id="69128-381">Comprehensive and advanced feature set</span></span>

## <a name="one-simple-license"></a><span data-ttu-id="69128-382">Una licenza semplice</span><span class="sxs-lookup"><span data-stu-id="69128-382">One Simple License</span></span>

<span data-ttu-id="69128-383">Non è previsto alcun costo per l'uso e il test del codice sorgente e nessun costo per le licenze di produzione quando viene distribuito in dispositivi con licenza preliminare, tutti gli altri dispositivi necessitano di una licenza annuale semplice.</span><span class="sxs-lookup"><span data-stu-id="69128-383">There is no cost to use and test the source code and no cost for production licenses when deployed to pre-licensed devices, all other devices need a simple annual license.</span></span>

## <a name="full-highest-quality-source-code"></a><span data-ttu-id="69128-384">Codice sorgente completo di qualità elevata</span><span class="sxs-lookup"><span data-stu-id="69128-384">Full, highest-quality source code</span></span>

<span data-ttu-id="69128-385">Nel corso degli anni, il codice sorgente di Azure RTO NetX duo ha impostato la qualità e la facilità di comprensione.</span><span class="sxs-lookup"><span data-stu-id="69128-385">Throughout the years, Azure RTOS NetX Duo source code has set the bar in quality and ease of understanding.</span></span> <span data-ttu-id="69128-386">Inoltre, la convenzione relativa alla presenza di una funzione per ogni file fornisce una semplice navigazione all'origine.</span><span class="sxs-lookup"><span data-stu-id="69128-386">In addition, the convention of having one function per file provides for easy source navigation.</span></span>

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="69128-387">Supporta le architetture più diffuse</span><span class="sxs-lookup"><span data-stu-id="69128-387">Supports most popular architectures</span></span>

<span data-ttu-id="69128-388">Azure RTO NetX Duo viene eseguito sui microprocessori più diffusi a 32/64 bit predefiniti, completamente testato e completamente supportato, incluse le seguenti architetture avanzate:</span><span class="sxs-lookup"><span data-stu-id="69128-388">Azure RTOS NetX Duo runs on most popular 32/64-bit microprocessors out-of-the-box, fully tested and fully supported, including the following advanced architectures:</span></span>

<span data-ttu-id="69128-389">**Dispositivi analoghi**: SHARC, Blackfin, CM4xx</span><span class="sxs-lookup"><span data-stu-id="69128-389">**Analog Devices**: SHARC, Blackfin, CM4xx</span></span>

<span data-ttu-id="69128-390">**Andina Core**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="69128-390">**Andes Core**: RISC-V</span></span>

<span data-ttu-id="69128-391">**Ambiqmicro**: pollo MCU</span><span class="sxs-lookup"><span data-stu-id="69128-391">**Ambiqmicro**: pollo MCUs</span></span>

<span data-ttu-id="69128-392">**ARM**: RM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/a15/a5/A7/A8/A9/A5x 64-bi/A7X a 64 bit/R4/R5, TrustZone ARMv8-M</span><span class="sxs-lookup"><span data-stu-id="69128-392">**ARM**: RM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>

<span data-ttu-id="69128-393">**Cadenza**: Xtensa, diamante</span><span class="sxs-lookup"><span data-stu-id="69128-393">**Cadence**: Xtensa, Diamond</span></span>

<span data-ttu-id="69128-394">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WICED WiFi</span><span class="sxs-lookup"><span data-stu-id="69128-394">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>

<span data-ttu-id="69128-395">**Cypress**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="69128-395">**Cypress**: RISC-V</span></span>

<span data-ttu-id="69128-396">**Silice**: ESI-RISC</span><span class="sxs-lookup"><span data-stu-id="69128-396">**EnSilica**: eSi-RISC</span></span>

<span data-ttu-id="69128-397">**Infineon**: XMC1000, XMC4000, Tricore</span><span class="sxs-lookup"><span data-stu-id="69128-397">**Infineon**: XMC1000, XMC4000, TriCore</span></span>

<span data-ttu-id="69128-398">**Intel & Intel FPGA**: x36/Pentium, XScale, Nios II, Cyclone, Arria 10</span><span class="sxs-lookup"><span data-stu-id="69128-398">**Intel & Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>

<span data-ttu-id="69128-399">**Microchip**: avr32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="69128-399">**Microchip**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>

<span data-ttu-id="69128-400">**Microsemi**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="69128-400">**Microsemi**: RISC-V</span></span>

<span data-ttu-id="69128-401">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="69128-401">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>

<span data-ttu-id="69128-402">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span><span class="sxs-lookup"><span data-stu-id="69128-402">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span></span>

<span data-ttu-id="69128-403">**Silicone** Lab: EFM32</span><span class="sxs-lookup"><span data-stu-id="69128-403">**Silicon** Labs: EFM32</span></span>

<span data-ttu-id="69128-404">**Synopsys**: Arc 600, 700, Arc em, Arc HS</span><span class="sxs-lookup"><span data-stu-id="69128-404">**Synopsys**: ARC 600, 700, ARC EM, ARC HS</span></span>

<span data-ttu-id="69128-405">**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="69128-405">**ST**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>

<span data-ttu-id="69128-406">**TL**: C5xxx, C6xxx, Stellaris, Sitara, tiva-C</span><span class="sxs-lookup"><span data-stu-id="69128-406">**Tl**: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>

<span data-ttu-id="69128-407">**Elaborazione Wave**: MIPS32 4K, 24 k, 34 k, 1004 k, MIPS64 5K, MicroAptiv, InterAptiv, ProAptiv, M-Class</span><span class="sxs-lookup"><span data-stu-id="69128-407">**Wave Computing**: MIPS32 4K, 24 K, 34 K, 1004 K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>

<span data-ttu-id="69128-408">**Xilinx**: Microblaze, PowerPC 405, ZYNQ, Zynq UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="69128-408">**Xilinx**: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>

<span data-ttu-id="69128-409">*Tutte le cifre relative a tempistiche e dimensioni elencate sono stime e possono essere diverse nella piattaforma di sviluppo.*</span><span class="sxs-lookup"><span data-stu-id="69128-409">*All timing and size figures listed are estimates and may be different on your development platform.*</span></span>

## <a name="related-services"></a><span data-ttu-id="69128-410">Servizi correlati</span><span class="sxs-lookup"><span data-stu-id="69128-410">Related services</span></span>

<span data-ttu-id="69128-411">Il modulo di sicurezza del Centro sicurezza di Azure per RTO offre una soluzione di sicurezza completa per i dispositivi RTO di Azure.</span><span class="sxs-lookup"><span data-stu-id="69128-411">The Azure Security Center for IoT RTOS security module provides a comprehensive security solution for Azure RTOS devices.</span></span> <span data-ttu-id="69128-412">Il modulo di sicurezza per Azure RTO offre rilevamento di attività di rete dannose, linea di base del comportamento dei dispositivi basati su avvisi personalizzati e consente di migliorare l'igiene della sicurezza del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69128-412">The Security Module for Azure RTOS offers malicious network activity detection, custom alert based device behavior baselining, and helps improve device security hygiene.</span></span> <span data-ttu-id="69128-413">Scopri di più sul [modulo di sicurezza per Azure RTO](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) o inizia a usare la Guida introduttiva alla [configurazione del modulo di sicurezza per RTO di Azure](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) .</span><span class="sxs-lookup"><span data-stu-id="69128-413">Learn more about the [Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) or get started with the [Configure Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) quickstart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69128-414">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69128-414">Next steps</span></span>

<span data-ttu-id="69128-415">Per altre informazioni su NetX Duo, vedere il [manuale dell'utente di Azure RTO NETX Duo](about-this-guide.md).</span><span class="sxs-lookup"><span data-stu-id="69128-415">To learn more about NetX Duo, start with the [Azure RTOS NetX Duo User Guide](about-this-guide.md).</span></span>
