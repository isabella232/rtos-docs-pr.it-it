---
title: Informazioni Azure RTOS NetX Duo
description: Azure RTOS NetX Duo è uno stack di rete TCP/IP avanzato di livello industriale progettato specificamente per applicazioni IoT e in tempo reale con deep embedded.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 6112ab5cb711ca1a5c83fd5cd4b43abc0302c6c5
ms.sourcegitcommit: f9d8cf23becf96d5bd6d31dd54f89c48962fd09b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549332"
---
# <a name="overview-of-azure-rtos-netx-duo"></a><span data-ttu-id="d19e3-103">Panoramica di Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="d19e3-103">Overview of Azure RTOS NetX Duo</span></span>

<span data-ttu-id="d19e3-104">Azure RTOS stack di rete TCP/IP incorporato di NetX Duo è lo stack di rete TCP/IP avanzato e di livello industriale di Microsoft, progettato appositamente per le applicazioni IoT e IPv4 avanzate di livello industriale.</span><span class="sxs-lookup"><span data-stu-id="d19e3-104">Azure RTOS NetX Duo embedded TCP/IP network stack is Microsoft's advanced, industrial grade dual IPv4 and IPv6 TCP/IP network stack that is designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="d19e3-105">NetX Duo offre applicazioni incorporate con protocolli di rete di base come IPv4, IPv6, TCP e UDP, nonché una suite completa di protocolli aggiuntivi aggiuntivi di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="d19e3-105">NetX Duo provides embedded applications with core network protocols such as IPv4, IPv6, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="d19e3-106">Azure RTOS NetX Duo offre sicurezza tramite altri prodotti di sicurezza aggiuntivi, tra cui Azure RTOS NetX Secure IPsec e Azure RTOS NetX Secure SSL/TLS/DTLS.</span><span class="sxs-lookup"><span data-stu-id="d19e3-106">Azure RTOS NetX Duo offers security via additional add-on security products, including Azure RTOS NetX Secure IPsec and Azure RTOS NetX Secure SSL/TLS/DTLS.</span></span> <span data-ttu-id="d19e3-107">Tutto questo in combinazione con un footprint ridotto, un'esecuzione rapida e una maggiore facilità d'uso rendono Azure RTOS NetX Duo la scelta ideale per le applicazioni IoT incorporate più complesse.</span><span class="sxs-lookup"><span data-stu-id="d19e3-107">All of this combined with an small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX Duo the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="d19e3-108">Protocolli API</span><span class="sxs-lookup"><span data-stu-id="d19e3-108">API protocols</span></span>

### <a name="mqtt"></a><span data-ttu-id="d19e3-109">MQTT</span><span class="sxs-lookup"><span data-stu-id="d19e3-109">MQTT</span></span>

* <span data-ttu-id="d19e3-110">Trasporto di telemetria della coda di messaggistica (MQTT)</span><span class="sxs-lookup"><span data-stu-id="d19e3-110">Messaging Queue Telemetry Transport (MQTT)</span></span>
* <span data-ttu-id="d19e3-111">Flash minimo da 2,7 KB</span><span class="sxs-lookup"><span data-stu-id="d19e3-111">Minimal 2.7 KB FLASH</span></span>

### <a name="auto-ip"></a><span data-ttu-id="d19e3-112">IP automatico</span><span class="sxs-lookup"><span data-stu-id="d19e3-112">Auto IP</span></span>

* <span data-ttu-id="d19e3-113">Assegnazione automatica di indirizzi IPv4</span><span class="sxs-lookup"><span data-stu-id="d19e3-113">Automatic IPv4 address assignment</span></span>
* <span data-ttu-id="d19e3-114">Minimo 1,2 KB, 300 byte di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-114">Minimal 1.2 KB, 300 bytes of RAM</span></span>

### <a name="http-https"></a><span data-ttu-id="d19e3-115">HTTP, HTTPS</span><span class="sxs-lookup"><span data-stu-id="d19e3-115">HTTP, HTTPS</span></span>

#### <a name="http-10"></a><span data-ttu-id="d19e3-116">HTTP 1.0</span><span class="sxs-lookup"><span data-stu-id="d19e3-116">HTTP 1.0</span></span>

* <span data-ttu-id="d19e3-117">Hypertext Transfer Protocol(HTTP)</span><span class="sxs-lookup"><span data-stu-id="d19e3-117">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="d19e3-118">Memoria FLASH minima da 2,8 KB a 4,8 KB/ da 0,4 KB a 1,0 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-118">Minimal 2.8 KB to 4.8 KB FLASH / 0.4 KB to 1.0 KB RAM</span></span>
* <span data-ttu-id="d19e3-119">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="d19e3-119">Client and server support</span></span>

#### <a name="httphttps-11"></a><span data-ttu-id="d19e3-120">HTTP/HTTPS 1.1</span><span class="sxs-lookup"><span data-stu-id="d19e3-120">HTTP/HTTPS 1.1</span></span>

* <span data-ttu-id="d19e3-121">Hypertext Transfer Protocol(HTTP)</span><span class="sxs-lookup"><span data-stu-id="d19e3-121">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="d19e3-122">Memoria FLASH minima da 3,0 KB a 9,5 KB/ da 0,5 KB a 2 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-122">Minimal 3.0 KB to 9.5 KB FLASH / 0.5 KB to 2 KB RAM</span></span>
* <span data-ttu-id="d19e3-123">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="d19e3-123">Client and server support</span></span>
* <span data-ttu-id="d19e3-124">Più sessioni client in ingresso</span><span class="sxs-lookup"><span data-stu-id="d19e3-124">Multiple incoming client sessions</span></span>
* <span data-ttu-id="d19e3-125">Testo normale e HTTPS crittografato</span><span class="sxs-lookup"><span data-stu-id="d19e3-125">Plain text and encrypted HTTPS</span></span>
* <span data-ttu-id="d19e3-126">Supporto delle connessioni permanenti</span><span class="sxs-lookup"><span data-stu-id="d19e3-126">Persistent connection support</span></span>
* <span data-ttu-id="d19e3-127">Caricamento di file multipart</span><span class="sxs-lookup"><span data-stu-id="d19e3-127">Multipart file upload</span></span>
* <span data-ttu-id="d19e3-128">Completamente integrato con Azure RTOS NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="d19e3-128">Fully integrated with Azure RTOS NetX Secure TLS</span></span>

### <a name="smtp"></a><span data-ttu-id="d19e3-129">SMTP</span><span class="sxs-lookup"><span data-stu-id="d19e3-129">SMTP</span></span>

* <span data-ttu-id="d19e3-130">Simple Mall Transfer Protocol (SMTP)</span><span class="sxs-lookup"><span data-stu-id="d19e3-130">Simple Mall Transfer Protocol (SMTP)</span></span>
* <span data-ttu-id="d19e3-131">Footprint minimo di 4,1 KB e 0,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-131">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="d19e3-132">Supporto client</span><span class="sxs-lookup"><span data-stu-id="d19e3-132">Client support</span></span>

### <a name="dhcp"></a><span data-ttu-id="d19e3-133">DHCP</span><span class="sxs-lookup"><span data-stu-id="d19e3-133">DHCP</span></span>

* <span data-ttu-id="d19e3-134">Dynamic Host Configuration Protocol (DHCP)</span><span class="sxs-lookup"><span data-stu-id="d19e3-134">Dynamic Host Configuration Protocol (DHCP)</span></span>
* <span data-ttu-id="d19e3-135">Footprint minimo da 3,6 KB a 4,6 KB FLASH, 2,7 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-135">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="d19e3-136">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="d19e3-136">Client and server support</span></span>
* <span data-ttu-id="d19e3-137">Supporto per IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="d19e3-137">IPv4 and IPv6 support</span></span>

### <a name="nat"></a><span data-ttu-id="d19e3-138">NAT</span><span class="sxs-lookup"><span data-stu-id="d19e3-138">NAT</span></span>

* <span data-ttu-id="d19e3-139">Network Address Translation (NAT)</span><span class="sxs-lookup"><span data-stu-id="d19e3-139">Network Address Translation (NAT)</span></span>
* <span data-ttu-id="d19e3-140">Footprint minimo di 3,5 K6 e 0,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-140">Minimal 3.5K6 and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="d19e3-141">Supporto degli indirizzi IPv4</span><span class="sxs-lookup"><span data-stu-id="d19e3-141">IPv4 address support</span></span>
* <span data-ttu-id="d19e3-142">NAT è disponibile solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="d19e3-142">NAT is only available with Azure RTOS NetX Duo</span></span>

### <a name="snmp"></a><span data-ttu-id="d19e3-143">SNMP</span><span class="sxs-lookup"><span data-stu-id="d19e3-143">SNMP</span></span>

* <span data-ttu-id="d19e3-144">Simple Network Management Protocol (SNMP)</span><span class="sxs-lookup"><span data-stu-id="d19e3-144">Simple Network Management Protocol (SNMP)</span></span>
* <span data-ttu-id="d19e3-145">Footprint minimo di 10,9 KB e 2,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-145">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="d19e3-146">Supporto dell'agente per VI, V2 e V3</span><span class="sxs-lookup"><span data-stu-id="d19e3-146">Agent support for VI, V2, and V3</span></span>

### <a name="dns-mdns-dns-sd"></a><span data-ttu-id="d19e3-147">DNS, mDNS, DNS-SD</span><span class="sxs-lookup"><span data-stu-id="d19e3-147">DNS, mDNS, DNS-SD</span></span>

* <span data-ttu-id="d19e3-148">Domain Name System (DNS)</span><span class="sxs-lookup"><span data-stu-id="d19e3-148">Domain Name System (DNS)</span></span>
* <span data-ttu-id="d19e3-149">Multicast Domain Name System (mDNS)</span><span class="sxs-lookup"><span data-stu-id="d19e3-149">Multicast Domain Name System (mDNS)</span></span>
* <span data-ttu-id="d19e3-150">Individuazione dei servizi basati su DNS (DNS-SD)</span><span class="sxs-lookup"><span data-stu-id="d19e3-150">DNS-based service discovery (DNS-SD)</span></span>
* <span data-ttu-id="d19e3-151">DNS minimo da 2,4 KB a 3 KB FLASH, footprint di RAM da 1 KB</span><span class="sxs-lookup"><span data-stu-id="d19e3-151">DNS Minimal 2.4 KB to 3 KB FLASH, 1 KB RAM footprint</span></span>
* <span data-ttu-id="d19e3-152">Supporto client</span><span class="sxs-lookup"><span data-stu-id="d19e3-152">Client support</span></span>
* <span data-ttu-id="d19e3-153">mDNS e DNS-SD sono disponibili solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="d19e3-153">mDNS and DNS-SD are only available with Azure RTOS NetX Duo</span></span>

### <a name="pop3"></a><span data-ttu-id="d19e3-154">POP3</span><span class="sxs-lookup"><span data-stu-id="d19e3-154">POP3</span></span>

* <span data-ttu-id="d19e3-155">Post Office Protocol versione 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="d19e3-155">Post Office Protocol Version 3 (POP3)</span></span>
* <span data-ttu-id="d19e3-156">Footprint minimo di 8,1 KB e 1,4 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-156">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="d19e3-157">Supporto client</span><span class="sxs-lookup"><span data-stu-id="d19e3-157">Client support</span></span>

### <a name="telnet"></a><span data-ttu-id="d19e3-158">Telnet</span><span class="sxs-lookup"><span data-stu-id="d19e3-158">TELNET</span></span>

* <span data-ttu-id="d19e3-159">Footprint minimo di 0,5 KB e 0,3 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-159">Minimal 0.5 KB and 0.3 KB RAM footprint</span></span>
* <span data-ttu-id="d19e3-160">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="d19e3-160">Client and server support</span></span>
* <span data-ttu-id="d19e3-161">API Telnet intuitive: *nx_telnet_ \**</span><span class="sxs-lookup"><span data-stu-id="d19e3-161">Intuitive Telnet APIs: *nx_telnet_\**</span></span>

### <a name="ftp-tftp"></a><span data-ttu-id="d19e3-162">FTP, TFTP</span><span class="sxs-lookup"><span data-stu-id="d19e3-162">FTP, TFTP</span></span>

* <span data-ttu-id="d19e3-163">File Transfer Protocol (FTP)</span><span class="sxs-lookup"><span data-stu-id="d19e3-163">File Transfer Protocol (FTP)</span></span>
* <span data-ttu-id="d19e3-164">Trivial File Transfer Protocol (TFTP)</span><span class="sxs-lookup"><span data-stu-id="d19e3-164">Trivial File Transfer Protocol (TFTP)</span></span>
* <span data-ttu-id="d19e3-165">FTP minimo da 1,8 KB a 7,2 KB FLASH, da 0,6 KB a 2,1 KB ram footprint</span><span class="sxs-lookup"><span data-stu-id="d19e3-165">FTP Minimal 1.8 KB to 7.2 KB FLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="d19e3-166">TFTP minimo da 1,7 KB a 2,4 KB FLASH, da 0,3 KB a 1,8 KB ram footprint</span><span class="sxs-lookup"><span data-stu-id="d19e3-166">TFTP Minimal 1.7 KB to 2.4 KB FLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="d19e3-167">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="d19e3-167">Client and server support</span></span>
* <span data-ttu-id="d19e3-168">API FTP e TFTP *intuitive: \** nx_ftp_ o *\* nx_tftp_*</span><span class="sxs-lookup"><span data-stu-id="d19e3-168">Intuitive FTP and TFTP APIs: *nx_ftp_\** or *nx_tftp_\**</span></span>

### <a name="ppp-pppoe"></a><span data-ttu-id="d19e3-169">PPP, PPPoE</span><span class="sxs-lookup"><span data-stu-id="d19e3-169">PPP, PPPoE</span></span>

* <span data-ttu-id="d19e3-170">Protocollo PPP (Polnt-to-PoInt)</span><span class="sxs-lookup"><span data-stu-id="d19e3-170">Polnt-to-PoInt Protocol (PPP)</span></span>
* <span data-ttu-id="d19e3-171">Point-to-Point Protocol over Ethernet(PPPoE)</span><span class="sxs-lookup"><span data-stu-id="d19e3-171">Point-to-Point Protocol over Ethernet(PPPoE)</span></span>
* <span data-ttu-id="d19e3-172">Footprint minimo di 7,1 KB e 3,8 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-172">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="d19e3-173">API PPP intuitive: *nx_ppp_ \**</span><span class="sxs-lookup"><span data-stu-id="d19e3-173">Intuitive PPP APIs: *nx_ppp_\**</span></span>

* <span data-ttu-id="d19e3-174">PPPoE è disponibile solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="d19e3-174">PPPoE is only available with Azure RTOS NetX Duo</span></span>

### <a name="sntp"></a><span data-ttu-id="d19e3-175">SNTP</span><span class="sxs-lookup"><span data-stu-id="d19e3-175">SNTP</span></span>

* <span data-ttu-id="d19e3-176">Simple Network Time Protocol (SNTP)</span><span class="sxs-lookup"><span data-stu-id="d19e3-176">Simple Network Time Protocol (SNTP)</span></span>
* <span data-ttu-id="d19e3-177">Minimo 4 KB e 0,5 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-177">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="d19e3-178">Supporto client</span><span class="sxs-lookup"><span data-stu-id="d19e3-178">Client support</span></span>
* <span data-ttu-id="d19e3-179">API SNTP intuitive: *nx_sntp_ \**</span><span class="sxs-lookup"><span data-stu-id="d19e3-179">Intuitive SNTP APIs: *nx_sntp_\**</span></span>

### <a name="azure-rtos-netx-duo-api"></a><span data-ttu-id="d19e3-180">Azure RTOS NetX Duo API</span><span class="sxs-lookup"><span data-stu-id="d19e3-180">Azure RTOS NetX Duo API</span></span>

* <span data-ttu-id="d19e3-181">API intuitiva e coerente</span><span class="sxs-lookup"><span data-stu-id="d19e3-181">Intuitive and consistent API</span></span>
* <span data-ttu-id="d19e3-182">Convenzione di denominazione sostantivo-verbo</span><span class="sxs-lookup"><span data-stu-id="d19e3-182">Noun-verb naming convention</span></span>
* <span data-ttu-id="d19e3-183">Implementazione rapida dell'API a copia zero</span><span class="sxs-lookup"><span data-stu-id="d19e3-183">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="d19e3-184">Tutte le API hanno <i>nx_\* per</i> identificarsi facilmente come Azure RTOS NetX</span><span class="sxs-lookup"><span data-stu-id="d19e3-184">All APIs have leading <i>nx_\*</i> to easily identify as Azure RTOS NetX</span></span>
* <span data-ttu-id="d19e3-185">Le API di blocco hanno un timeout del thread facoltativo</span><span class="sxs-lookup"><span data-stu-id="d19e3-185">Blocking APIs have optional thread timeout</span></span>
* <span data-ttu-id="d19e3-186">Vedere [Azure RTOS per l'utente di NetX Duo](about-this-guide.md) per altri dettagli</span><span class="sxs-lookup"><span data-stu-id="d19e3-186">See [Azure RTOS NetX Duo User Guide](about-this-guide.md) for more details</span></span>
* <span data-ttu-id="d19e3-187">Livello BSD facoltativo per la portabilità del codice socket legacy</span><span class="sxs-lookup"><span data-stu-id="d19e3-187">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp"></a><span data-ttu-id="d19e3-188">Igmp</span><span class="sxs-lookup"><span data-stu-id="d19e3-188">IGMP</span></span>

* <span data-ttu-id="d19e3-189">IGMP (Internet Group Management Protocol)</span><span class="sxs-lookup"><span data-stu-id="d19e3-189">Internet Group Management Protocol (IGMP)</span></span>
* <span data-ttu-id="d19e3-190">Flash minimo da 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="d19e3-190">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="d19e3-191">Supporto dei gruppi multicast IPv4</span><span class="sxs-lookup"><span data-stu-id="d19e3-191">IPv4 multicast group support</span></span>
* <span data-ttu-id="d19e3-192">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="d19e3-192">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d19e3-193">Statistiche IGMP facoltative</span><span class="sxs-lookup"><span data-stu-id="d19e3-193">Optional IGMP statistics</span></span>
* <span data-ttu-id="d19e3-194">Traccia a livello di sistema tramite Azure RTOS ThreadX</span><span class="sxs-lookup"><span data-stu-id="d19e3-194">System-level trace via Azure RTOS ThreadX</span></span>
* <span data-ttu-id="d19e3-195">API IGMP intuitive: *nx_igmp_ \**</span><span class="sxs-lookup"><span data-stu-id="d19e3-195">Intuitive IGMP APIs: *nx_igmp_\**</span></span>

### <a name="azure-rtos-netx-secure-dtls"></a><span data-ttu-id="d19e3-196">Azure RTOS DTLS sicuri di NetX</span><span class="sxs-lookup"><span data-stu-id="d19e3-196">Azure RTOS NetX Secure DTLS</span></span>

* <span data-ttu-id="d19e3-197">Datagram Transport Layer Security (DTLS) 1.0 e 1.2</span><span class="sxs-lookup"><span data-stu-id="d19e3-197">Datagram Transport Layer Security (DTLS) 1.0 and 1.2</span></span>
* <span data-ttu-id="d19e3-198">FLASH minimo di 11 KB</span><span class="sxs-lookup"><span data-stu-id="d19e3-198">Minimal 11 KB FLASH</span></span>
* <span data-ttu-id="d19e3-199">Fast, software RSA 2048-bit key size ~1-second @120MHz</span><span class="sxs-lookup"><span data-stu-id="d19e3-199">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="d19e3-200">Implementazione semplificata di X.509</span><span class="sxs-lookup"><span data-stu-id="d19e3-200">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="d19e3-201">Completamente integrato con i Azure RTOS UDP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="d19e3-201">Fully integrated with Azure RTOS NetX Duo UDP sockets</span></span>
* <span data-ttu-id="d19e3-202">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="d19e3-202">Hardware Crypto Support</span></span>
* <span data-ttu-id="d19e3-203">Supporto della crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="d19e3-203">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="d19e3-204">Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse le curve P 192/224/256/384/521</span><span class="sxs-lookup"><span data-stu-id="d19e3-204">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="d19e3-205">Supporto delle chiavi crittografate (dipendente dall'hardware)</span><span class="sxs-lookup"><span data-stu-id="d19e3-205">Encrypted Key Support (hardware dependent)</span></span>

### <a name="azure-rtos-netx-secure-tls"></a><span data-ttu-id="d19e3-206">Azure RTOS NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="d19e3-206">Azure RTOS NetX Secure TLS</span></span>

* <span data-ttu-id="d19e3-207">Transport Layer Security (TLS) 1.0, 1.1 e 1.2</span><span class="sxs-lookup"><span data-stu-id="d19e3-207">Transport Layer Security (TLS) 1.0, 1.1, and 1.2</span></span>
* <span data-ttu-id="d19e3-208">Flash minimo da 8,8 KB</span><span class="sxs-lookup"><span data-stu-id="d19e3-208">Minimal 8.8 KB FLASH</span></span>
* <span data-ttu-id="d19e3-209">Fast, software RSA 2048-bit key size ~1-second @120MHz</span><span class="sxs-lookup"><span data-stu-id="d19e3-209">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="d19e3-210">Implementazione semplificata di X.509</span><span class="sxs-lookup"><span data-stu-id="d19e3-210">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="d19e3-211">Completamente integrato con Azure RTOS TCP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="d19e3-211">Fully integrated with Azure RTOS NetX Duo TCP sockets</span></span>
* <span data-ttu-id="d19e3-212">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="d19e3-212">Hardware Crypto Support</span></span>
* <span data-ttu-id="d19e3-213">Supporto della crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="d19e3-213">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="d19e3-214">Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse le curve P 192/224/256/384/521</span><span class="sxs-lookup"><span data-stu-id="d19e3-214">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="d19e3-215">Supporto delle chiavi crittografate (dipendente dall'hardware)</span><span class="sxs-lookup"><span data-stu-id="d19e3-215">Encrypted Key Support (hardware dependent)</span></span>

### <a name="icmp"></a><span data-ttu-id="d19e3-216">ICMP</span><span class="sxs-lookup"><span data-stu-id="d19e3-216">ICMP</span></span>

* <span data-ttu-id="d19e3-217">Internet Control Message Protocol (ICMP)</span><span class="sxs-lookup"><span data-stu-id="d19e3-217">Internet Control Message Protocol (ICMP)</span></span>
* <span data-ttu-id="d19e3-218">Flash minimo da 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="d19e3-218">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="d19e3-219">Supporto per IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="d19e3-219">IPv4 and IPv6 support</span></span>
* <span data-ttu-id="d19e3-220">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="d19e3-220">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d19e3-221">Richiesta ping e risposta ping</span><span class="sxs-lookup"><span data-stu-id="d19e3-221">Ping request and ping response</span></span>
* <span data-ttu-id="d19e3-222">Sospensione facoltativa dei thread nelle richieste ping</span><span class="sxs-lookup"><span data-stu-id="d19e3-222">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="d19e3-223">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="d19e3-223">Optional timeout on all suspension</span></span>
* <span data-ttu-id="d19e3-224">Statistiche ICMP facoltative</span><span class="sxs-lookup"><span data-stu-id="d19e3-224">Optional ICMP statistics</span></span>
* <span data-ttu-id="d19e3-225">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="d19e3-225">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="d19e3-226">API ICMP intuitive: *nx_icmp_ \**</span><span class="sxs-lookup"><span data-stu-id="d19e3-226">Intuitive ICMP APIs: *nx_icmp_\**</span></span>

### <a name="udp"></a><span data-ttu-id="d19e3-227">UDP</span><span class="sxs-lookup"><span data-stu-id="d19e3-227">UDP</span></span>

* <span data-ttu-id="d19e3-228">Udp (User Datagram Protocol)</span><span class="sxs-lookup"><span data-stu-id="d19e3-228">User Datagram Protocol (UDP)</span></span>
* <span data-ttu-id="d19e3-229">MINIMO FLASH da 2,5 KB, 124 socket di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="d19e3-229">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="d19e3-230">Elaborazione rapida dei pacchetti TCP in prossimità di wirespeed:</span><span class="sxs-lookup"><span data-stu-id="d19e3-230">Fast, near wirespeed TCP packet processing:</span></span>
    * <span data-ttu-id="d19e3-231">RX 95 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 14%</span><span class="sxs-lookup"><span data-stu-id="d19e3-231">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU utilization</span></span>
    * <span data-ttu-id="d19e3-232">TX 94 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 10%</span><span class="sxs-lookup"><span data-stu-id="d19e3-232">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU utilization</span></span>
* <span data-ttu-id="d19e3-233">Tecnologia udp Fast Path™</span><span class="sxs-lookup"><span data-stu-id="d19e3-233">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="d19e3-234">Nessun limite al numero di UDP</span><span class="sxs-lookup"><span data-stu-id="d19e3-234">No limits on the number of UDP</span></span>
* <span data-ttu-id="d19e3-235">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="d19e3-235">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d19e3-236">Sospensione facoltativa alla ricezione socket</span><span class="sxs-lookup"><span data-stu-id="d19e3-236">Optional suspension on socket receive</span></span>
* <span data-ttu-id="d19e3-237">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="d19e3-237">Optional timeout on all suspension</span></span>
* <span data-ttu-id="d19e3-238">Statistiche UDP facoltative</span><span class="sxs-lookup"><span data-stu-id="d19e3-238">Optional UDP statistics</span></span>
* <span data-ttu-id="d19e3-239">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="d19e3-239">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="d19e3-240">API UDP intuitive: *nx_udp_ \**</span><span class="sxs-lookup"><span data-stu-id="d19e3-240">Intuitive UDP APIs: *nx_udp_\**</span></span>

### <a name="tcp"></a><span data-ttu-id="d19e3-241">TCP</span><span class="sxs-lookup"><span data-stu-id="d19e3-241">TCP</span></span>

* <span data-ttu-id="d19e3-242">TCP (Transmission Control Protocol)</span><span class="sxs-lookup"><span data-stu-id="d19e3-242">Transmission Control Protocol (TCP)</span></span>
* <span data-ttu-id="d19e3-243">Flash minimo da 10,5 KB a 12,5 KB, 280 byte di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="d19e3-243">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="d19e3-244">Elaborazione rapida dei pacchetti TCP in prossimità di wlrespeed:</span><span class="sxs-lookup"><span data-stu-id="d19e3-244">Fast, near wlrespeed TCP packet processing:</span></span>
    * <span data-ttu-id="d19e3-245">RX 93 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 20%</span><span class="sxs-lookup"><span data-stu-id="d19e3-245">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU utilization</span></span>
    * <span data-ttu-id="d19e3-246">TX 94 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 27%</span><span class="sxs-lookup"><span data-stu-id="d19e3-246">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU utilization</span></span>
* <span data-ttu-id="d19e3-247">Connessione affidabile</span><span class="sxs-lookup"><span data-stu-id="d19e3-247">Reliable connection</span></span>
* <span data-ttu-id="d19e3-248">Nessun limite al numero di socket TCP</span><span class="sxs-lookup"><span data-stu-id="d19e3-248">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="d19e3-249">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="d19e3-249">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d19e3-250">Sospensione facoltativa nella ricezione/trasmissione socket</span><span class="sxs-lookup"><span data-stu-id="d19e3-250">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="d19e3-251">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="d19e3-251">Optional timeout on all suspension</span></span>
* <span data-ttu-id="d19e3-252">Statistiche TCP facoltative</span><span class="sxs-lookup"><span data-stu-id="d19e3-252">Optional TCP statistics</span></span>
* <span data-ttu-id="d19e3-253">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="d19e3-253">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="d19e3-254">API TCP intuitive: *nx_tcp_ \**</span><span class="sxs-lookup"><span data-stu-id="d19e3-254">Intuitive TCP APIs: *nx_tcp_\**</span></span>

### <a name="arprarp"></a><span data-ttu-id="d19e3-255">ARP/RARP</span><span class="sxs-lookup"><span data-stu-id="d19e3-255">ARP/RARP</span></span>

* <span data-ttu-id="d19e3-256">ARP (Address Resolution Protocol)</span><span class="sxs-lookup"><span data-stu-id="d19e3-256">Address Resolution Protocol (ARP)</span></span>
* <span data-ttu-id="d19e3-257">RaRP (Reverse Address Resolution Protocol)</span><span class="sxs-lookup"><span data-stu-id="d19e3-257">Reverse Address Resolution Protocol (RARP)</span></span>
* <span data-ttu-id="d19e3-258">Minimo 1,7 KB FLASH, dimensioni della RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-258">Minimal 1.7 KB FLASH, RAM size</span></span>
* <span data-ttu-id="d19e3-259">Risoluzione dinamica di indirizzi MAC da 32 blt IPv4 e 48 blt</span><span class="sxs-lookup"><span data-stu-id="d19e3-259">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses</span></span>
* <span data-ttu-id="d19e3-260">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="d19e3-260">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d19e3-261">Cache ARP flessibile e definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="d19e3-261">Flexible, user-defined ARP cache</span></span>
* <span data-ttu-id="d19e3-262">Supporto gratuito ARP</span><span class="sxs-lookup"><span data-stu-id="d19e3-262">Gratuitous ARP support</span></span>
* <span data-ttu-id="d19e3-263">Statistiche ARP/RARP facoltative determinate dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="d19e3-263">Optional ARP/RARP statistics determined by application</span></span>
* <span data-ttu-id="d19e3-264">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="d19e3-264">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="d19e3-265">API ARP/RARP intuitive: *nx_arp_ \**, *nx_rarp_ \**</span><span class="sxs-lookup"><span data-stu-id="d19e3-265">Intuitive ARP/RARP APIs: *nx_arp_\**, *nx_rarp_\**</span></span>

### <a name="ipv4-amp-ipv6"></a><span data-ttu-id="d19e3-266">IPv4 &amp; IPv6</span><span class="sxs-lookup"><span data-stu-id="d19e3-266">IPv4 &amp; IPv6</span></span>

* <span data-ttu-id="d19e3-267">Ip (Internet Protocol)</span><span class="sxs-lookup"><span data-stu-id="d19e3-267">Internet Protocol (IP)</span></span>
* <span data-ttu-id="d19e3-268">Footprint minimo da 3,5 KB a 8,5 KB FLASH, da 2 KB a 3 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d19e3-268">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint</span></span>
* <span data-ttu-id="d19e3-269">Architettura di Piconet™</span><span class="sxs-lookup"><span data-stu-id="d19e3-269">Piconet™ architecture</span></span>
* <span data-ttu-id="d19e3-270">Prestazioni veloci e near wirespeed</span><span class="sxs-lookup"><span data-stu-id="d19e3-270">Fast, near wirespeed performance</span></span>
* <span data-ttu-id="d19e3-271">Supporto di più interfacce</span><span class="sxs-lookup"><span data-stu-id="d19e3-271">Multiple interface support</span></span>
* <span data-ttu-id="d19e3-272">Supporto multihomed</span><span class="sxs-lookup"><span data-stu-id="d19e3-272">Multihomed support</span></span>
* <span data-ttu-id="d19e3-273">Supporto del routing statico</span><span class="sxs-lookup"><span data-stu-id="d19e3-273">Static routing support</span></span>
* <span data-ttu-id="d19e3-274">Supporto della frammentazione/riassemblaggio IP</span><span class="sxs-lookup"><span data-stu-id="d19e3-274">IP fragmentation/reassembly support</span></span>
* <span data-ttu-id="d19e3-275">Supporto degli indirizzi IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="d19e3-275">IPv4 and IPv6 address support</span></span>
* <span data-ttu-id="d19e3-276">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="d19e3-276">IXIA IxANVL validated</span></span>
* <span data-ttu-id="d19e3-277">Certificazione del logo pronto per IPv6 di fase II</span><span class="sxs-lookup"><span data-stu-id="d19e3-277">Phase II IPv6 Ready Logo Certification</span></span>
* <span data-ttu-id="d19e3-278">Statistiche IP facoltative</span><span class="sxs-lookup"><span data-stu-id="d19e3-278">Optional IP statistics</span></span>
* <span data-ttu-id="d19e3-279">Interfaccia del driver del livello fisico ben definita e intuitiva</span><span class="sxs-lookup"><span data-stu-id="d19e3-279">Well defined, intuitive physical layer driver interface</span></span>
* <span data-ttu-id="d19e3-280">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="d19e3-280">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="d19e3-281">API del livello IP intuitive: *\* nx_ip_*, *nxd_ip_ \** *\** , nxd_ipv6_</span><span class="sxs-lookup"><span data-stu-id="d19e3-281">Intuitive IP layer APIs: *nx_ip_\**, *nxd_ip_\**, *nxd_ipv6_\**</span></span>
* <span data-ttu-id="d19e3-282">Precertificato da TUV e UL a IEC 61508 SIL 4, IEC 62304 Classe C, ISO 26262 ASIL D e EN 50128 SW-SIL4</span><span class="sxs-lookup"><span data-stu-id="d19e3-282">Pre-certified by TUV and UL to IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D, and EN 50128 SW-SIL4</span></span>

### <a name="azure-rtos-netx-secure-ipsec"></a><span data-ttu-id="d19e3-283">Azure RTOS IPSEC sicuro di NetX</span><span class="sxs-lookup"><span data-stu-id="d19e3-283">Azure RTOS NetX Secure IPSEC</span></span>

* <span data-ttu-id="d19e3-284">IpSec (Internet Protocol Security)</span><span class="sxs-lookup"><span data-stu-id="d19e3-284">Internet Protocol Security (IPSEC)</span></span>
* <span data-ttu-id="d19e3-285">Livello IP</span><span class="sxs-lookup"><span data-stu-id="d19e3-285">IP layer</span></span>
* <span data-ttu-id="d19e3-286">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="d19e3-286">Hardware crypto support</span></span>
* <span data-ttu-id="d19e3-287">Supporto della crittografia software, tra cui:</span><span class="sxs-lookup"><span data-stu-id="d19e3-287">Software crypto support, including:</span></span>
    * <span data-ttu-id="d19e3-288">DES, 3DES</span><span class="sxs-lookup"><span data-stu-id="d19e3-288">DES, 3DES</span></span>
    * <span data-ttu-id="d19e3-289">AES</span><span class="sxs-lookup"><span data-stu-id="d19e3-289">AES</span></span>
    * <span data-ttu-id="d19e3-290">HMAC-MD5</span><span class="sxs-lookup"><span data-stu-id="d19e3-290">HMAC-MD5</span></span>
    * <span data-ttu-id="d19e3-291">HMAC-SHA1</span><span class="sxs-lookup"><span data-stu-id="d19e3-291">HMAC-SHA1</span></span>
* <span data-ttu-id="d19e3-292">Supporto di Internet Key Exchange (IKE) versione 2</span><span class="sxs-lookup"><span data-stu-id="d19e3-292">Internet Key Exchange (IKE) Version 2 support</span></span>
* <span data-ttu-id="d19e3-293">API IPsec intuitive: *nx_ipsec_ \**</span><span class="sxs-lookup"><span data-stu-id="d19e3-293">Intuitive IPsec APIs: *nx_ipsec_\**</span></span>
* <span data-ttu-id="d19e3-294">IPsec è disponibile solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="d19e3-294">IPsec is only available with Azure RTOS NetX Duo</span></span>

## <a name="safe-and-secure"></a><span data-ttu-id="d19e3-295">Cassaforte e sicuro</span><span class="sxs-lookup"><span data-stu-id="d19e3-295">Safe and secure</span></span>

<span data-ttu-id="d19e3-296">Azure RTOS NetX Duo è sicuro.</span><span class="sxs-lookup"><span data-stu-id="d19e3-296">Azure RTOS NetX Duo is secure.</span></span> <span data-ttu-id="d19e3-297">Questa sicurezza viene fornita tramite prodotti di sicurezza aggiuntivi, tra cui IPsec, SSL, TLS e DTLS.</span><span class="sxs-lookup"><span data-stu-id="d19e3-297">This security is provided through add-on security products, including IPsec, SSL, TLS, and DTLS.</span></span> <span data-ttu-id="d19e3-298">Inoltre, l'applicazione ha il controllo completo su tutti gli accessi esterni Azure RTOS NetX Duo, rendendo molto più semplice la determinazione dei rischi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d19e3-298">Also, the application has complete control over all external access to Azure RTOS NetX Duo, making security risk determination much easier.</span></span>

<span data-ttu-id="d19e3-299">Microsoft Azure RTOS fornisce agli OEM componenti per proteggere la comunicazione e creare codice e isolamento dei dati usando i meccanismi di protezione hardware MCU/MPU sottostanti.</span><span class="sxs-lookup"><span data-stu-id="d19e3-299">Microsoft Azure RTOS provides OEMs with components to secure communication and to create code and data isolation using underlying MCU/MPU hardware protection mechanisms.</span></span> <span data-ttu-id="d19e3-300">È in definitiva responsabilità del generatore di dispositivi garantire che il dispositivo soddisfi pienamente i requisiti di sicurezza in evoluzione associati al caso d'uso specifico.</span><span class="sxs-lookup"><span data-stu-id="d19e3-300">It is ultimately the responsibility of the device builder to ensure the device fully meets the evolving security requirements associated with its specific use case.</span></span>


## <a name="interoperability-verification"></a><span data-ttu-id="d19e3-301">Verifica dell'interoperabilità</span><span class="sxs-lookup"><span data-stu-id="d19e3-301">Interoperability verification</span></span>

<span data-ttu-id="d19e3-302">NetX Duo è conforme agli standard RFC e offre interoperabilità completa con i dispositivi per la maggior parte dei fornitori.</span><span class="sxs-lookup"><span data-stu-id="d19e3-302">NetX Duo conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span>

![Logo pronto per IPv6](./media/overview-netx-duo/ipv6-ready-logo.png)

<span data-ttu-id="d19e3-304">Azure RTOS NetX Duo è uno degli unici stack TCP/IP incorporati per ottenere la rigorosa certificazione del logo IPv6-Ready, dimostrando che ha superato i test di conformità e interoperabilità, amministrati e convalidati dal forum IPv6.</span><span class="sxs-lookup"><span data-stu-id="d19e3-304">Azure RTOS NetX Duo is one of the only embedded TCP/IP stacks to achieve the rigorous IPv6-Ready Logo certification, evidence that it has passed conformance and interoperability tests, administered and validated by the IPv6 Forum.</span></span> <span data-ttu-id="d19e3-305">NetX Duo usa anche lo standard di settore IxANVL (Automated Network Validation Library) per l'implementazione del protocollo TCP/IP core di NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="d19e3-305">NetX Duo also utilizes the industry standard IxANVL (Automated Network Validation Library) for the NetX Duo core TCP/IP protocol implementation.</span></span>

## <a name="comprehensive-iot-solution"></a><span data-ttu-id="d19e3-306">Soluzione IoT completa</span><span class="sxs-lookup"><span data-stu-id="d19e3-306">Comprehensive IoT solution</span></span>

<span data-ttu-id="d19e3-307">NetX Duo offre una delle reti TCP/IP più complete per le applicazioni IoT con un'ampia incorporata.</span><span class="sxs-lookup"><span data-stu-id="d19e3-307">NetX Duo has one of the most comprehensive TCP/IP networking for deeply embedded IoT applications.</span></span> <span data-ttu-id="d19e3-308">Questo supporto include i seguenti prodotti del protocollo aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="d19e3-308">This support includes the following add-on protocol products.</span></span>

<span data-ttu-id="d19e3-309">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPsec, AutoIP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPsec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span><span class="sxs-lookup"><span data-stu-id="d19e3-309">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPsec, AutoIP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPsec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="d19e3-310">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="d19e3-310">Advanced technology</span></span>

<span data-ttu-id="d19e3-311">Azure RTOS NetX Duo è una tecnologia avanzata che include:</span><span class="sxs-lookup"><span data-stu-id="d19e3-311">Azure RTOS NetX Duo is advanced technology that includes:</span></span>

* <span data-ttu-id="d19e3-312">Architettura ™ Piconet</span><span class="sxs-lookup"><span data-stu-id="d19e3-312">Piconet™ architecture</span></span>
* <span data-ttu-id="d19e3-313">Scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="d19e3-313">Automatic scaling</span></span>
* <span data-ttu-id="d19e3-314">UDP Fast-Path Technology™</span><span class="sxs-lookup"><span data-stu-id="d19e3-314">UDP Fast-Path Technology™</span></span>
* <span data-ttu-id="d19e3-315">Gestione flessibile dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="d19e3-315">Flexible packet management</span></span>
* <span data-ttu-id="d19e3-316">API e implementazione a copia zero</span><span class="sxs-lookup"><span data-stu-id="d19e3-316">Zero-copy API and implementation</span></span>
* <span data-ttu-id="d19e3-317">Supporto multihomed</span><span class="sxs-lookup"><span data-stu-id="d19e3-317">Multihomed support</span></span>
* <span data-ttu-id="d19e3-318">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="d19e3-318">Optional timeout on all suspension</span></span>
* <span data-ttu-id="d19e3-319">Supporto del routing statico</span><span class="sxs-lookup"><span data-stu-id="d19e3-319">Static routing support</span></span>
* <span data-ttu-id="d19e3-320">IPsec</span><span class="sxs-lookup"><span data-stu-id="d19e3-320">IPsec</span></span>
* <span data-ttu-id="d19e3-321">SSL/TLS/DTLS</span><span class="sxs-lookup"><span data-stu-id="d19e3-321">SSL/TLS/DTLS</span></span>
* <span data-ttu-id="d19e3-322">Azure RTOS di analisi del sistema TraceX</span><span class="sxs-lookup"><span data-stu-id="d19e3-322">Azure RTOS TraceX system analysis support</span></span>

## <a name="related-services"></a><span data-ttu-id="d19e3-323">Servizi correlati</span><span class="sxs-lookup"><span data-stu-id="d19e3-323">Related services</span></span>

### <a name="azure-iot"></a><span data-ttu-id="d19e3-324">Azure IoT</span><span class="sxs-lookup"><span data-stu-id="d19e3-324">Azure IoT</span></span>

<span data-ttu-id="d19e3-325">NetX Duo include [Azure IoT Middleware](https://github.com/azure-rtos/netxduo/blob/master/addons/azure_iot/docs/README.md)per Azure RTOS, una libreria specifica della piattaforma che funge da livello di binding tra il Azure RTOS e Azure SDK per Embedded C per facilitare la connettività ai servizi Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="d19e3-325">NetX Duo includes [Azure IoT Middleware for Azure RTOS](https://github.com/azure-rtos/netxduo/blob/master/addons/azure_iot/docs/README.md), a platform-specific library that acts as a binding layer between the Azure RTOS and the Azure SDK for Embedded C to facilitate connectivity to Azure IoT services.</span></span> <span data-ttu-id="d19e3-326">Gli obiettivi del Azure IoT middleware sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="d19e3-326">The goals of Azure IoT Middleware are the following.</span></span>
* <span data-ttu-id="d19e3-327">Fornire le interfacce smart client (IoTHub_Client, DeviceProvisioning_Client) necessarie agli sviluppatori per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d19e3-327">Provide the smart client interfaces (IoTHub_Client, DeviceProvisioning_Client) that developers need for their applications.</span></span>
* <span data-ttu-id="d19e3-328">Orchestrare l'interazione tra Embedded C SDK e la piattaforma.</span><span class="sxs-lookup"><span data-stu-id="d19e3-328">Orchestrate the interaction between the Embedded C SDK and the platform.</span></span>
* <span data-ttu-id="d19e3-329">Specificare Azure RTOS inizializzazione della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="d19e3-329">Provide Azure RTOS platform initialization.</span></span>
* <span data-ttu-id="d19e3-330">IoT Plug and Play supporto.</span><span class="sxs-lookup"><span data-stu-id="d19e3-330">IoT Plug and Play support.</span></span>
* <span data-ttu-id="d19e3-331">Funzionalità di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d19e3-331">Security capabilities.</span></span>
* <span data-ttu-id="d19e3-332">Informazioni sulle limitazioni delle risorse.</span><span class="sxs-lookup"><span data-stu-id="d19e3-332">Resource limitation aware.</span></span>
* <span data-ttu-id="d19e3-333">Supporto del protocollo.</span><span class="sxs-lookup"><span data-stu-id="d19e3-333">Protocol support.</span></span>

![Azure RTOS correlati a NetX Duo](./media/overview-netx-duo/related-services.png)

### <a name="azure-defender"></a><span data-ttu-id="d19e3-335">Azure Defender</span><span class="sxs-lookup"><span data-stu-id="d19e3-335">Azure Defender</span></span>

<span data-ttu-id="d19e3-336">Il modulo Azure Defender per IoT sicurezza offre una soluzione di sicurezza completa per Azure RTOS dispositivi.</span><span class="sxs-lookup"><span data-stu-id="d19e3-336">The Azure Defender for IoT security module provides a comprehensive security solution for Azure RTOS devices.</span></span> <span data-ttu-id="d19e3-337">Il modulo di sicurezza per Azure RTOS rilevamento di attività di rete dannose, la base del comportamento dei dispositivi basato su avvisi personalizzati e contribuisce a migliorare la protezione della sicurezza dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="d19e3-337">The Security Module for Azure RTOS offers malicious network activity detection, custom alert based device behavior baselining, and helps improve device security hygiene.</span></span> <span data-ttu-id="d19e3-338">Altre informazioni sul modulo [di sicurezza per Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) [](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) guida introduttiva alla configurazione del modulo Azure RTOS sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d19e3-338">Learn more about the [Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) or get started with the [Configure Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) quickstart.</span></span>

### <a name="device-update-for-iot-hub"></a><span data-ttu-id="d19e3-339">Aggiornamento del dispositivo per l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="d19e3-339">Device Update for IoT Hub</span></span>

<span data-ttu-id="d19e3-340">L'aggiornamento dei dispositivi di Azure per l'hub [IoT](https://docs.microsoft.com/azure/iot-hub-device-update/understand-device-update) è un servizio che consente di distribuire aggiornamenti over-the-air (OTA) per i dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="d19e3-340">The [Azure Device Update for IoT Hub](https://docs.microsoft.com/azure/iot-hub-device-update/understand-device-update) is a service that enables you to deploy over-the-air updates (OTA) for your IoT devices.</span></span> <span data-ttu-id="d19e3-341">Il modulo Device Update for IoT Hub (Aggiornamento dispositivo per hub IoT) è l'implementazione dell'aggiornamento del dispositivo per l'agente dell'hub IoT in Azure RTOS NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="d19e3-341">The Device Update for IoT Hub module is the implementation of Device Update for IoT Hub Agent in Azure RTOS NetX Duo.</span></span> <span data-ttu-id="d19e3-342">Fornisce semplici API per i generatori di dispositivi per integrare la funzionalità Aggiornamento dispositivo nella propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="d19e3-342">It provides simple APIs for device builders to integrate the Device Update capability in their application.</span></span>

<span data-ttu-id="d19e3-343">Vedere gli esempi di schede di valutazione dei semiconduttori chiave che includono le guide introduttive per informazioni su come configurare, compilare e distribuire gli aggiornamenti over-the-air (OTA) nei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="d19e3-343">See the samples of key semiconductors evaluation boards that include the get started guides to learn configure, build and deploy the over-the-air (OTA) updates to the devices.</span></span>

<span data-ttu-id="d19e3-344">Altre informazioni sull'uso dell'aggiornamento dei [dispositivi per l'hub IoT con Azure RTOS](https://docs.microsoft.com/azure/iot-hub-device-update/device-update-azure-real-time-operating-system).</span><span class="sxs-lookup"><span data-stu-id="d19e3-344">And you can learn more details about use [Device Update for IoT Hub with Azure RTOS](https://docs.microsoft.com/azure/iot-hub-device-update/device-update-azure-real-time-operating-system).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d19e3-345">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d19e3-345">Next steps</span></span>

<span data-ttu-id="d19e3-346">Per altre informazioni su NetX Duo, iniziare con il manuale [Azure RTOS'utente di NetX Duo.](about-this-guide.md)</span><span class="sxs-lookup"><span data-stu-id="d19e3-346">To learn more about NetX Duo, start with the [Azure RTOS NetX Duo User Guide](about-this-guide.md).</span></span>
