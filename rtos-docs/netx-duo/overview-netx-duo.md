---
title: Informazioni Azure RTOS NetX Duo
description: Azure RTOS NetX Duo è uno stack di rete TCP/IP avanzato di livello industriale progettato specificamente per applicazioni IoT e in tempo reale con deep embedded.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: e3fe3bcc602f409cc76f3be47aca865bf8116697
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171336"
---
# <a name="overview-of-azure-rtos-netx-duo"></a><span data-ttu-id="419a7-103">Panoramica di Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="419a7-103">Overview of Azure RTOS NetX Duo</span></span>

<span data-ttu-id="419a7-104">Azure RTOS stack di rete TCP/IP incorporato di NetX Duo è lo stack di rete TCP/IP avanzato di livello industriale di Microsoft, dual IPv4 e IPv6, progettato specificamente per applicazioni IoT, in tempo reale e con incorporamento avanzato.</span><span class="sxs-lookup"><span data-stu-id="419a7-104">Azure RTOS NetX Duo embedded TCP/IP network stack is Microsoft's advanced, industrial grade dual IPv4 and IPv6 TCP/IP network stack that is designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="419a7-105">NetX Duo offre applicazioni incorporate con protocolli di rete di base come IPv4, IPv6, TCP e UDP, nonché una suite completa di protocolli aggiuntivi aggiuntivi di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="419a7-105">NetX Duo provides embedded applications with core network protocols such as IPv4, IPv6, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="419a7-106">Azure RTOS NetX Duo offre sicurezza tramite altri prodotti di sicurezza aggiuntivi, tra cui Azure RTOS NetX Secure IPsec e Azure RTOS NetX Secure SSL/TLS/DTLS.</span><span class="sxs-lookup"><span data-stu-id="419a7-106">Azure RTOS NetX Duo offers security via additional add-on security products, including Azure RTOS NetX Secure IPsec and Azure RTOS NetX Secure SSL/TLS/DTLS.</span></span> <span data-ttu-id="419a7-107">Il tutto combinato con un footprint ridotto, un'esecuzione rapida e una maggiore facilità d'uso rendono Azure RTOS NetX Duo la scelta ideale per le applicazioni IoT incorporate più complesse.</span><span class="sxs-lookup"><span data-stu-id="419a7-107">All of this combined with an small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX Duo the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="419a7-108">Protocolli API</span><span class="sxs-lookup"><span data-stu-id="419a7-108">API protocols</span></span>

### <a name="mqtt"></a><span data-ttu-id="419a7-109">MQTT</span><span class="sxs-lookup"><span data-stu-id="419a7-109">MQTT</span></span>

* <span data-ttu-id="419a7-110">Trasporto dei dati di telemetria della coda di messaggistica (MQTT)</span><span class="sxs-lookup"><span data-stu-id="419a7-110">Messaging Queue Telemetry Transport (MQTT)</span></span>
* <span data-ttu-id="419a7-111">MEMORIA FLASH minima di 2,7 KB</span><span class="sxs-lookup"><span data-stu-id="419a7-111">Minimal 2.7 KB FLASH</span></span>

### <a name="auto-ip"></a><span data-ttu-id="419a7-112">IP automatico</span><span class="sxs-lookup"><span data-stu-id="419a7-112">Auto IP</span></span>

* <span data-ttu-id="419a7-113">Assegnazione automatica di indirizzi IPv4</span><span class="sxs-lookup"><span data-stu-id="419a7-113">Automatic IPv4 address assignment</span></span>
* <span data-ttu-id="419a7-114">Minimo 1,2 KB, 300 byte di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-114">Minimal 1.2 KB, 300 bytes of RAM</span></span>

### <a name="http-https"></a><span data-ttu-id="419a7-115">HTTP, HTTPS</span><span class="sxs-lookup"><span data-stu-id="419a7-115">HTTP, HTTPS</span></span>

#### <a name="http-10"></a><span data-ttu-id="419a7-116">HTTP 1.0</span><span class="sxs-lookup"><span data-stu-id="419a7-116">HTTP 1.0</span></span>

* <span data-ttu-id="419a7-117">Hypertext Transfer Protocol(HTTP)</span><span class="sxs-lookup"><span data-stu-id="419a7-117">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="419a7-118">Memoria FLASH minima da 2,8 KB a 4,8 KB/ da 0,4 KB a 1,0 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-118">Minimal 2.8 KB to 4.8 KB FLASH / 0.4 KB to 1.0 KB RAM</span></span>
* <span data-ttu-id="419a7-119">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="419a7-119">Client and server support</span></span>

#### <a name="httphttps-11"></a><span data-ttu-id="419a7-120">HTTP/HTTPS 1.1</span><span class="sxs-lookup"><span data-stu-id="419a7-120">HTTP/HTTPS 1.1</span></span>

* <span data-ttu-id="419a7-121">Hypertext Transfer Protocol(HTTP)</span><span class="sxs-lookup"><span data-stu-id="419a7-121">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="419a7-122">Memoria FLASH minima da 3,0 KB a 9,5 KB/ da 0,5 KB a 2 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-122">Minimal 3.0 KB to 9.5 KB FLASH / 0.5 KB to 2 KB RAM</span></span>
* <span data-ttu-id="419a7-123">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="419a7-123">Client and server support</span></span>
* <span data-ttu-id="419a7-124">Più sessioni client in ingresso</span><span class="sxs-lookup"><span data-stu-id="419a7-124">Multiple incoming client sessions</span></span>
* <span data-ttu-id="419a7-125">Testo normale e HTTPS crittografato</span><span class="sxs-lookup"><span data-stu-id="419a7-125">Plain text and encrypted HTTPS</span></span>
* <span data-ttu-id="419a7-126">Supporto delle connessioni permanenti</span><span class="sxs-lookup"><span data-stu-id="419a7-126">Persistent connection support</span></span>
* <span data-ttu-id="419a7-127">Caricamento di file multipart</span><span class="sxs-lookup"><span data-stu-id="419a7-127">Multipart file upload</span></span>
* <span data-ttu-id="419a7-128">Completamente integrato con Azure RTOS NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="419a7-128">Fully integrated with Azure RTOS NetX Secure TLS</span></span>

### <a name="smtp"></a><span data-ttu-id="419a7-129">SMTP</span><span class="sxs-lookup"><span data-stu-id="419a7-129">SMTP</span></span>

* <span data-ttu-id="419a7-130">Simple Mall Transfer Protocol (SMTP)</span><span class="sxs-lookup"><span data-stu-id="419a7-130">Simple Mall Transfer Protocol (SMTP)</span></span>
* <span data-ttu-id="419a7-131">Footprint minimo di 4,1 KB e 0,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-131">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="419a7-132">Supporto client</span><span class="sxs-lookup"><span data-stu-id="419a7-132">Client support</span></span>

### <a name="dhcp"></a><span data-ttu-id="419a7-133">DHCP</span><span class="sxs-lookup"><span data-stu-id="419a7-133">DHCP</span></span>

* <span data-ttu-id="419a7-134">Dynamic Host Configuration Protocol (DHCP)</span><span class="sxs-lookup"><span data-stu-id="419a7-134">Dynamic Host Configuration Protocol (DHCP)</span></span>
* <span data-ttu-id="419a7-135">Footprint minimo da 3,6 KB a 4,6 KB FLASH, 2,7 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-135">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="419a7-136">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="419a7-136">Client and server support</span></span>
* <span data-ttu-id="419a7-137">Supporto per IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="419a7-137">IPv4 and IPv6 support</span></span>

### <a name="nat"></a><span data-ttu-id="419a7-138">NAT</span><span class="sxs-lookup"><span data-stu-id="419a7-138">NAT</span></span>

* <span data-ttu-id="419a7-139">Network Address Translation (NAT)</span><span class="sxs-lookup"><span data-stu-id="419a7-139">Network Address Translation (NAT)</span></span>
* <span data-ttu-id="419a7-140">Footprint minimo di 3,5 K6 e 0,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-140">Minimal 3.5K6 and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="419a7-141">Supporto degli indirizzi IPv4</span><span class="sxs-lookup"><span data-stu-id="419a7-141">IPv4 address support</span></span>
* <span data-ttu-id="419a7-142">NAT è disponibile solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="419a7-142">NAT is only available with Azure RTOS NetX Duo</span></span>

### <a name="snmp"></a><span data-ttu-id="419a7-143">SNMP</span><span class="sxs-lookup"><span data-stu-id="419a7-143">SNMP</span></span>

* <span data-ttu-id="419a7-144">Simple Network Management Protocol (SNMP)</span><span class="sxs-lookup"><span data-stu-id="419a7-144">Simple Network Management Protocol (SNMP)</span></span>
* <span data-ttu-id="419a7-145">Footprint minimo di 10,9 KB e 2,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-145">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="419a7-146">Supporto dell'agente per VI, V2 e V3</span><span class="sxs-lookup"><span data-stu-id="419a7-146">Agent support for VI, V2, and V3</span></span>

### <a name="dns-mdns-dns-sd"></a><span data-ttu-id="419a7-147">DNS, mDNS, DNS-SD</span><span class="sxs-lookup"><span data-stu-id="419a7-147">DNS, mDNS, DNS-SD</span></span>

* <span data-ttu-id="419a7-148">Domain Name System (DNS)</span><span class="sxs-lookup"><span data-stu-id="419a7-148">Domain Name System (DNS)</span></span>
* <span data-ttu-id="419a7-149">Multicast Domain Name System (mDNS)</span><span class="sxs-lookup"><span data-stu-id="419a7-149">Multicast Domain Name System (mDNS)</span></span>
* <span data-ttu-id="419a7-150">Individuazione dei servizi basati su DNS (DNS-SD)</span><span class="sxs-lookup"><span data-stu-id="419a7-150">DNS-based service discovery (DNS-SD)</span></span>
* <span data-ttu-id="419a7-151">DNS minimo da 2,4 KB a 3 KB FLASH, footprint ram da 1 KB</span><span class="sxs-lookup"><span data-stu-id="419a7-151">DNS Minimal 2.4 KB to 3 KB FLASH, 1 KB RAM footprint</span></span>
* <span data-ttu-id="419a7-152">Supporto client</span><span class="sxs-lookup"><span data-stu-id="419a7-152">Client support</span></span>
* <span data-ttu-id="419a7-153">mDNS e DNS-SD sono disponibili solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="419a7-153">mDNS and DNS-SD are only available with Azure RTOS NetX Duo</span></span>

### <a name="p0p3"></a><span data-ttu-id="419a7-154">P0P3</span><span class="sxs-lookup"><span data-stu-id="419a7-154">P0P3</span></span>

* <span data-ttu-id="419a7-155">Post Office Protocol versione 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="419a7-155">Post Office Protocol Version 3 (POP3)</span></span>
* <span data-ttu-id="419a7-156">Footprint minimo di 8,1 KB e 1,4 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-156">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="419a7-157">Supporto client</span><span class="sxs-lookup"><span data-stu-id="419a7-157">Client support</span></span>

### <a name="telnet"></a><span data-ttu-id="419a7-158">Telnet</span><span class="sxs-lookup"><span data-stu-id="419a7-158">TELNET</span></span>

* <span data-ttu-id="419a7-159">Footprint minimo di 0,5 KB e 0,3 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-159">Minimal 0.5 KB and 0.3 KB RAM footprint</span></span>
* <span data-ttu-id="419a7-160">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="419a7-160">Client and server support</span></span>
* <span data-ttu-id="419a7-161">API Telnet intuitive: *nx_telnet_ \**</span><span class="sxs-lookup"><span data-stu-id="419a7-161">Intuitive Telnet APIs: *nx_telnet_\**</span></span>

### <a name="ftp-tftp"></a><span data-ttu-id="419a7-162">FTP, TFTP</span><span class="sxs-lookup"><span data-stu-id="419a7-162">FTP, TFTP</span></span>

* <span data-ttu-id="419a7-163">File Transfer Protocol (FTP)</span><span class="sxs-lookup"><span data-stu-id="419a7-163">File Transfer Protocol (FTP)</span></span>
* <span data-ttu-id="419a7-164">Trivial File Transfer Protocol (TFTP)</span><span class="sxs-lookup"><span data-stu-id="419a7-164">Trivial File Transfer Protocol (TFTP)</span></span>
* <span data-ttu-id="419a7-165">FTP minimo da 1,8 KB a 7,2 KB FLASH, footprint di RAM da 0,6 a 2,1 KB</span><span class="sxs-lookup"><span data-stu-id="419a7-165">FTP Minimal 1.8 KB to 7.2 KB FLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="419a7-166">Memoria flash TFTP minima da 1,7 KB a 2,4 KB, footprint di RAM da 0,3 a 1,8 KB</span><span class="sxs-lookup"><span data-stu-id="419a7-166">TFTP Minimal 1.7 KB to 2.4 KB FLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="419a7-167">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="419a7-167">Client and server support</span></span>
* <span data-ttu-id="419a7-168">API FTP e TFTP *intuitive: \** nx_ftp_ o *\* nx_tftp_*</span><span class="sxs-lookup"><span data-stu-id="419a7-168">Intuitive FTP and TFTP APIs: *nx_ftp_\** or *nx_tftp_\**</span></span>

### <a name="ppp-pppoe"></a><span data-ttu-id="419a7-169">PPP, PPPoE</span><span class="sxs-lookup"><span data-stu-id="419a7-169">PPP, PPPoE</span></span>

* <span data-ttu-id="419a7-170">Protocollo PPP (Polnt-to-PoInt)</span><span class="sxs-lookup"><span data-stu-id="419a7-170">Polnt-to-PoInt Protocol (PPP)</span></span>
* <span data-ttu-id="419a7-171">Point-to-Point Protocol over Ethernet(PPPoE)</span><span class="sxs-lookup"><span data-stu-id="419a7-171">Point-to-Point Protocol over Ethernet(PPPoE)</span></span>
* <span data-ttu-id="419a7-172">Footprint minimo di 7,1 KB e 3,8 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-172">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="419a7-173">API PPP intuitive: *nx_ppp_ \**</span><span class="sxs-lookup"><span data-stu-id="419a7-173">Intuitive PPP APIs: *nx_ppp_\**</span></span>

* <span data-ttu-id="419a7-174">PPPoE è disponibile solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="419a7-174">PPPoE is only available with Azure RTOS NetX Duo</span></span>

### <a name="sntp"></a><span data-ttu-id="419a7-175">SNTP</span><span class="sxs-lookup"><span data-stu-id="419a7-175">SNTP</span></span>

* <span data-ttu-id="419a7-176">Simple Network Time Protocol (SNTP)</span><span class="sxs-lookup"><span data-stu-id="419a7-176">Simple Network Time Protocol (SNTP)</span></span>
* <span data-ttu-id="419a7-177">Minimo 4 KB e 0,5 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-177">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="419a7-178">Supporto client</span><span class="sxs-lookup"><span data-stu-id="419a7-178">Client support</span></span>
* <span data-ttu-id="419a7-179">API SNTP intuitive: *nx_sntp_ \**</span><span class="sxs-lookup"><span data-stu-id="419a7-179">Intuitive SNTP APIs: *nx_sntp_\**</span></span>

### <a name="azure-rtos-netx-duo-api"></a><span data-ttu-id="419a7-180">Azure RTOS NetX Duo API</span><span class="sxs-lookup"><span data-stu-id="419a7-180">Azure RTOS NetX Duo API</span></span>

* <span data-ttu-id="419a7-181">API intuitiva e coerente</span><span class="sxs-lookup"><span data-stu-id="419a7-181">Intuitive and consistent API</span></span>
* <span data-ttu-id="419a7-182">Convenzione di denominazione sostantivo-verbo</span><span class="sxs-lookup"><span data-stu-id="419a7-182">Noun-verb naming convention</span></span>
* <span data-ttu-id="419a7-183">Implementazione rapida dell'API a copia zero</span><span class="sxs-lookup"><span data-stu-id="419a7-183">Fast, zero-copy API implementation</span></span>
* <span data-ttu-id="419a7-184">Tutte le API hanno <i>nx_\* per</i> identificarsi facilmente come Azure RTOS NetX</span><span class="sxs-lookup"><span data-stu-id="419a7-184">All APIs have leading <i>nx_\*</i> to easily identify as Azure RTOS NetX</span></span>
* <span data-ttu-id="419a7-185">Le API di blocco hanno un timeout del thread facoltativo</span><span class="sxs-lookup"><span data-stu-id="419a7-185">Blocking APIs have optional thread timeout</span></span>
* <span data-ttu-id="419a7-186">Vedere [Azure RTOS per l'utente di NetX Duo](about-this-guide.md) per altri dettagli</span><span class="sxs-lookup"><span data-stu-id="419a7-186">See [Azure RTOS NetX Duo User Guide](about-this-guide.md) for more details</span></span>
* <span data-ttu-id="419a7-187">Livello BSD facoltativo per la portabilità del codice socket legacy</span><span class="sxs-lookup"><span data-stu-id="419a7-187">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp"></a><span data-ttu-id="419a7-188">Igmp</span><span class="sxs-lookup"><span data-stu-id="419a7-188">IGMP</span></span>

* <span data-ttu-id="419a7-189">IGMP (Internet Group Management Protocol)</span><span class="sxs-lookup"><span data-stu-id="419a7-189">Internet Group Management Protocol (IGMP)</span></span>
* <span data-ttu-id="419a7-190">Flash minimo da 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="419a7-190">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="419a7-191">Supporto dei gruppi multicast IPv4</span><span class="sxs-lookup"><span data-stu-id="419a7-191">IPv4 multicast group support</span></span>
* <span data-ttu-id="419a7-192">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="419a7-192">IXIA IxANVL validated</span></span>
* <span data-ttu-id="419a7-193">Statistiche IGMP facoltative</span><span class="sxs-lookup"><span data-stu-id="419a7-193">Optional IGMP statistics</span></span>
* <span data-ttu-id="419a7-194">Traccia a livello di sistema tramite Azure RTOS ThreadX</span><span class="sxs-lookup"><span data-stu-id="419a7-194">System-level trace via Azure RTOS ThreadX</span></span>
* <span data-ttu-id="419a7-195">API IGMP intuitive: *nx_igmp_ \**</span><span class="sxs-lookup"><span data-stu-id="419a7-195">Intuitive IGMP APIs: *nx_igmp_\**</span></span>

### <a name="azure-rtos-netx-secure-dtls"></a><span data-ttu-id="419a7-196">Azure RTOS NetX Secure DTLS</span><span class="sxs-lookup"><span data-stu-id="419a7-196">Azure RTOS NetX Secure DTLS</span></span>

* <span data-ttu-id="419a7-197">Datagram Transport Layer Security (DTLS) 1.0 e 1.2</span><span class="sxs-lookup"><span data-stu-id="419a7-197">Datagram Transport Layer Security (DTLS) 1.0 and 1.2</span></span>
* <span data-ttu-id="419a7-198">MEMORIA FLASH minima di 11 KB</span><span class="sxs-lookup"><span data-stu-id="419a7-198">Minimal 11 KB FLASH</span></span>
* <span data-ttu-id="419a7-199">Chiave RSA a 2048 bit veloce e software di dimensioni ~1 secondo @120MHz</span><span class="sxs-lookup"><span data-stu-id="419a7-199">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="419a7-200">Implementazione semplificata di X.509</span><span class="sxs-lookup"><span data-stu-id="419a7-200">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="419a7-201">Completamente integrato con i Azure RTOS UDP di NetX Duo</span><span class="sxs-lookup"><span data-stu-id="419a7-201">Fully integrated with Azure RTOS NetX Duo UDP sockets</span></span>
* <span data-ttu-id="419a7-202">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="419a7-202">Hardware Crypto Support</span></span>
* <span data-ttu-id="419a7-203">Supporto della crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="419a7-203">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="419a7-204">Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse le curve P 192/224/256/384/521</span><span class="sxs-lookup"><span data-stu-id="419a7-204">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="419a7-205">Supporto delle chiavi crittografate (dipendente dall'hardware)</span><span class="sxs-lookup"><span data-stu-id="419a7-205">Encrypted Key Support (hardware dependent)</span></span>

### <a name="azure-rtos-netx-secure-tls"></a><span data-ttu-id="419a7-206">Azure RTOS NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="419a7-206">Azure RTOS NetX Secure TLS</span></span>

* <span data-ttu-id="419a7-207">Transport Layer Security (TLS) 1.0, 1.1 e 1.2</span><span class="sxs-lookup"><span data-stu-id="419a7-207">Transport Layer Security (TLS) 1.0, 1.1, and 1.2</span></span>
* <span data-ttu-id="419a7-208">MEMORIA FLASH minima di 8,8 KB</span><span class="sxs-lookup"><span data-stu-id="419a7-208">Minimal 8.8 KB FLASH</span></span>
* <span data-ttu-id="419a7-209">Chiave RSA a 2048 bit veloce e software di dimensioni ~1 secondo @120MHz</span><span class="sxs-lookup"><span data-stu-id="419a7-209">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="419a7-210">Implementazione semplificata di X.509</span><span class="sxs-lookup"><span data-stu-id="419a7-210">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="419a7-211">Completamente integrato con Azure RTOS TCP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="419a7-211">Fully integrated with Azure RTOS NetX Duo TCP sockets</span></span>
* <span data-ttu-id="419a7-212">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="419a7-212">Hardware Crypto Support</span></span>
* <span data-ttu-id="419a7-213">Supporto della crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="419a7-213">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="419a7-214">Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse le curve P 192/224/256/384/521</span><span class="sxs-lookup"><span data-stu-id="419a7-214">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="419a7-215">Supporto delle chiavi crittografate (dipendente dall'hardware)</span><span class="sxs-lookup"><span data-stu-id="419a7-215">Encrypted Key Support (hardware dependent)</span></span>

### <a name="icmp"></a><span data-ttu-id="419a7-216">ICMP</span><span class="sxs-lookup"><span data-stu-id="419a7-216">ICMP</span></span>

* <span data-ttu-id="419a7-217">Internet Control Message Protocol (ICMP)</span><span class="sxs-lookup"><span data-stu-id="419a7-217">Internet Control Message Protocol (ICMP)</span></span>
* <span data-ttu-id="419a7-218">Flash minimo da 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="419a7-218">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="419a7-219">Supporto per IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="419a7-219">IPv4 and IPv6 support</span></span>
* <span data-ttu-id="419a7-220">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="419a7-220">IXIA IxANVL validated</span></span>
* <span data-ttu-id="419a7-221">Richiesta ping e risposta ping</span><span class="sxs-lookup"><span data-stu-id="419a7-221">Ping request and ping response</span></span>
* <span data-ttu-id="419a7-222">Sospensione facoltativa dei thread nelle richieste ping</span><span class="sxs-lookup"><span data-stu-id="419a7-222">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="419a7-223">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="419a7-223">Optional timeout on all suspension</span></span>
* <span data-ttu-id="419a7-224">Statistiche ICMP facoltative</span><span class="sxs-lookup"><span data-stu-id="419a7-224">Optional ICMP statistics</span></span>
* <span data-ttu-id="419a7-225">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="419a7-225">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="419a7-226">API ICMP intuitive: *nx_icmp_ \**</span><span class="sxs-lookup"><span data-stu-id="419a7-226">Intuitive ICMP APIs: *nx_icmp_\**</span></span>

### <a name="udp"></a><span data-ttu-id="419a7-227">UDP</span><span class="sxs-lookup"><span data-stu-id="419a7-227">UDP</span></span>

* <span data-ttu-id="419a7-228">Udp (User Datagram Protocol)</span><span class="sxs-lookup"><span data-stu-id="419a7-228">User Datagram Protocol (UDP)</span></span>
* <span data-ttu-id="419a7-229">MINIMO FLASH da 2,5 KB, 124 socket di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="419a7-229">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="419a7-230">Elaborazione rapida dei pacchetti TCP in prossimità di wirespeed:</span><span class="sxs-lookup"><span data-stu-id="419a7-230">Fast, near wirespeed TCP packet processing:</span></span>
    * <span data-ttu-id="419a7-231">RX 95 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 14%</span><span class="sxs-lookup"><span data-stu-id="419a7-231">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU utilization</span></span>
    * <span data-ttu-id="419a7-232">TX 94 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 10%</span><span class="sxs-lookup"><span data-stu-id="419a7-232">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU utilization</span></span>
* <span data-ttu-id="419a7-233">Tecnologia udp Fast Path™</span><span class="sxs-lookup"><span data-stu-id="419a7-233">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="419a7-234">Nessun limite al numero di UDP</span><span class="sxs-lookup"><span data-stu-id="419a7-234">No limits on the number of UDP</span></span>
* <span data-ttu-id="419a7-235">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="419a7-235">IXIA IxANVL validated</span></span>
* <span data-ttu-id="419a7-236">Sospensione facoltativa alla ricezione del socket</span><span class="sxs-lookup"><span data-stu-id="419a7-236">Optional suspension on socket receive</span></span>
* <span data-ttu-id="419a7-237">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="419a7-237">Optional timeout on all suspension</span></span>
* <span data-ttu-id="419a7-238">Statistiche UDP facoltative</span><span class="sxs-lookup"><span data-stu-id="419a7-238">Optional UDP statistics</span></span>
* <span data-ttu-id="419a7-239">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="419a7-239">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="419a7-240">API UDP intuitive: *nx_udp_ \**</span><span class="sxs-lookup"><span data-stu-id="419a7-240">Intuitive UDP APIs: *nx_udp_\**</span></span>

### <a name="tcp"></a><span data-ttu-id="419a7-241">TCP</span><span class="sxs-lookup"><span data-stu-id="419a7-241">TCP</span></span>

* <span data-ttu-id="419a7-242">Transmission Control Protocol (TCP)</span><span class="sxs-lookup"><span data-stu-id="419a7-242">Transmission Control Protocol (TCP)</span></span>
* <span data-ttu-id="419a7-243">Memoria flash minima da 10,5K8 a 12,5 KB, 280 byte di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="419a7-243">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="419a7-244">Elaborazione rapida dei pacchetti TCP da vicino:</span><span class="sxs-lookup"><span data-stu-id="419a7-244">Fast, near wlrespeed TCP packet processing:</span></span>
    * <span data-ttu-id="419a7-245">RX 93 Mbps su Ethernet a 100 Mbps, @100MHz MCU, utilizzo MCU del 20%</span><span class="sxs-lookup"><span data-stu-id="419a7-245">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU utilization</span></span>
    * <span data-ttu-id="419a7-246">TX 94 Mbps su Ethernet a 100 Mbps, @100MHz MCU, utilizzo MCU del 27%</span><span class="sxs-lookup"><span data-stu-id="419a7-246">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU utilization</span></span>
* <span data-ttu-id="419a7-247">Connessione affidabile</span><span class="sxs-lookup"><span data-stu-id="419a7-247">Reliable connection</span></span>
* <span data-ttu-id="419a7-248">Nessun limite al numero di socket TCP</span><span class="sxs-lookup"><span data-stu-id="419a7-248">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="419a7-249">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="419a7-249">IXIA IxANVL validated</span></span>
* <span data-ttu-id="419a7-250">Sospensione facoltativa su ricezione/trasmissione socket</span><span class="sxs-lookup"><span data-stu-id="419a7-250">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="419a7-251">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="419a7-251">Optional timeout on all suspension</span></span>
* <span data-ttu-id="419a7-252">Statistiche TCP facoltative</span><span class="sxs-lookup"><span data-stu-id="419a7-252">Optional TCP statistics</span></span>
* <span data-ttu-id="419a7-253">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="419a7-253">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="419a7-254">API TCP intuitive: *nx_tcp_ \**</span><span class="sxs-lookup"><span data-stu-id="419a7-254">Intuitive TCP APIs: *nx_tcp_\**</span></span>

### <a name="arprarp"></a><span data-ttu-id="419a7-255">ARP/RARP</span><span class="sxs-lookup"><span data-stu-id="419a7-255">ARP/RARP</span></span>

* <span data-ttu-id="419a7-256">ARP (Address Resolution Protocol)</span><span class="sxs-lookup"><span data-stu-id="419a7-256">Address Resolution Protocol (ARP)</span></span>
* <span data-ttu-id="419a7-257">RaRP (Reverse Address Resolution Protocol)</span><span class="sxs-lookup"><span data-stu-id="419a7-257">Reverse Address Resolution Protocol (RARP)</span></span>
* <span data-ttu-id="419a7-258">Minimo 1,7 KB FLASH, dimensioni della RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-258">Minimal 1.7 KB FLASH, RAM size</span></span>
* <span data-ttu-id="419a7-259">Risoluzione dinamica di indirizzi MAC da 32 blt IPv4 e 48 blt</span><span class="sxs-lookup"><span data-stu-id="419a7-259">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses</span></span>
* <span data-ttu-id="419a7-260">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="419a7-260">IXIA IxANVL validated</span></span>
* <span data-ttu-id="419a7-261">Cache ARP flessibile e definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="419a7-261">Flexible, user-defined ARP cache</span></span>
* <span data-ttu-id="419a7-262">Supporto gratuito ARP</span><span class="sxs-lookup"><span data-stu-id="419a7-262">Gratuitous ARP support</span></span>
* <span data-ttu-id="419a7-263">Statistiche ARP/RARP facoltative determinate dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="419a7-263">Optional ARP/RARP statistics determined by application</span></span>
* <span data-ttu-id="419a7-264">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="419a7-264">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="419a7-265">API ARP/RARP intuitive: *nx_arp_ \**, *nx_rarp_ \**</span><span class="sxs-lookup"><span data-stu-id="419a7-265">Intuitive ARP/RARP APIs: *nx_arp_\**, *nx_rarp_\**</span></span>

### <a name="ipv4-amp-ipv6"></a><span data-ttu-id="419a7-266">IPv4 &amp; IPv6</span><span class="sxs-lookup"><span data-stu-id="419a7-266">IPv4 &amp; IPv6</span></span>

* <span data-ttu-id="419a7-267">Ip (Internet Protocol)</span><span class="sxs-lookup"><span data-stu-id="419a7-267">Internet Protocol (IP)</span></span>
* <span data-ttu-id="419a7-268">Footprint minimo da 3,5 KB a 8,5 KB FLASH, da 2 KB a 3 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="419a7-268">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint</span></span>
* <span data-ttu-id="419a7-269">Architettura di Piconet™</span><span class="sxs-lookup"><span data-stu-id="419a7-269">Piconet™ architecture</span></span>
* <span data-ttu-id="419a7-270">Prestazioni veloci e near wirespeed</span><span class="sxs-lookup"><span data-stu-id="419a7-270">Fast, near wirespeed performance</span></span>
* <span data-ttu-id="419a7-271">Supporto di più interfacce</span><span class="sxs-lookup"><span data-stu-id="419a7-271">Multiple interface support</span></span>
* <span data-ttu-id="419a7-272">Supporto multihomed</span><span class="sxs-lookup"><span data-stu-id="419a7-272">Multihomed support</span></span>
* <span data-ttu-id="419a7-273">Supporto del routing statico</span><span class="sxs-lookup"><span data-stu-id="419a7-273">Static routing support</span></span>
* <span data-ttu-id="419a7-274">Supporto della frammentazione/riassemblaggio IP</span><span class="sxs-lookup"><span data-stu-id="419a7-274">IP fragmentation/reassembly support</span></span>
* <span data-ttu-id="419a7-275">Supporto degli indirizzi IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="419a7-275">IPv4 and IPv6 address support</span></span>
* <span data-ttu-id="419a7-276">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="419a7-276">IXIA IxANVL validated</span></span>
* <span data-ttu-id="419a7-277">Certificazione del logo pronto per IPv6 fase II</span><span class="sxs-lookup"><span data-stu-id="419a7-277">Phase II IPv6 Ready Logo Certification</span></span>
* <span data-ttu-id="419a7-278">Statistiche IP facoltative</span><span class="sxs-lookup"><span data-stu-id="419a7-278">Optional IP statistics</span></span>
* <span data-ttu-id="419a7-279">Interfaccia del driver di livello fisico ben definita e intuitiva</span><span class="sxs-lookup"><span data-stu-id="419a7-279">Well defined, intuitive physical layer driver interface</span></span>
* <span data-ttu-id="419a7-280">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="419a7-280">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="419a7-281">API intuitive del livello IP: *\* nx_ip_*, *nxd_ip_ \** *\** , nxd_ipv6_</span><span class="sxs-lookup"><span data-stu-id="419a7-281">Intuitive IP layer APIs: *nx_ip_\**, *nxd_ip_\**, *nxd_ipv6_\**</span></span>
* <span data-ttu-id="419a7-282">Precertificato da TUV e UL a IEC 61508 SIL 4, IEC 62304 Classe C, ISO 26262 ASIL D e EN 50128 SW-SIL4</span><span class="sxs-lookup"><span data-stu-id="419a7-282">Pre-certified by TUV and UL to IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D, and EN 50128 SW-SIL4</span></span>

### <a name="azure-rtos-netx-secure-ipsec"></a><span data-ttu-id="419a7-283">Azure RTOS IPSEC sicuro di NetX</span><span class="sxs-lookup"><span data-stu-id="419a7-283">Azure RTOS NetX Secure IPSEC</span></span>

* <span data-ttu-id="419a7-284">IPSEC (Internet Protocol Security)</span><span class="sxs-lookup"><span data-stu-id="419a7-284">Internet Protocol Security (IPSEC)</span></span>
* <span data-ttu-id="419a7-285">Livello IP</span><span class="sxs-lookup"><span data-stu-id="419a7-285">IP layer</span></span>
* <span data-ttu-id="419a7-286">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="419a7-286">Hardware crypto support</span></span>
* <span data-ttu-id="419a7-287">Supporto della crittografia software, tra cui:</span><span class="sxs-lookup"><span data-stu-id="419a7-287">Software crypto support, including:</span></span>
    * <span data-ttu-id="419a7-288">DES, 3DES</span><span class="sxs-lookup"><span data-stu-id="419a7-288">DES, 3DES</span></span>
    * <span data-ttu-id="419a7-289">AES</span><span class="sxs-lookup"><span data-stu-id="419a7-289">AES</span></span>
    * <span data-ttu-id="419a7-290">HMAC-MD5</span><span class="sxs-lookup"><span data-stu-id="419a7-290">HMAC-MD5</span></span>
    * <span data-ttu-id="419a7-291">HMAC-SHA1</span><span class="sxs-lookup"><span data-stu-id="419a7-291">HMAC-SHA1</span></span>
* <span data-ttu-id="419a7-292">Internet Key Exchange (IKE) versione 2</span><span class="sxs-lookup"><span data-stu-id="419a7-292">Internet Key Exchange (IKE) Version 2 support</span></span>
* <span data-ttu-id="419a7-293">API IPsec intuitive: *nx_ipsec_ \**</span><span class="sxs-lookup"><span data-stu-id="419a7-293">Intuitive IPsec APIs: *nx_ipsec_\**</span></span>
* <span data-ttu-id="419a7-294">IPsec è disponibile solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="419a7-294">IPsec is only available with Azure RTOS NetX Duo</span></span>

## <a name="safe-and-secure"></a><span data-ttu-id="419a7-295">Sicurezza e sicurezza</span><span class="sxs-lookup"><span data-stu-id="419a7-295">Safe and secure</span></span>

<span data-ttu-id="419a7-296">Azure RTOS NetX Duo è sicuro.</span><span class="sxs-lookup"><span data-stu-id="419a7-296">Azure RTOS NetX Duo is secure.</span></span> <span data-ttu-id="419a7-297">Questa sicurezza viene fornita tramite prodotti di sicurezza aggiuntivi, tra cui IPsec, SSL, TLS e DTLS.</span><span class="sxs-lookup"><span data-stu-id="419a7-297">This security is provided through add-on security products, including IPsec, SSL, TLS, and DTLS.</span></span> <span data-ttu-id="419a7-298">Inoltre, l'applicazione ha il controllo completo su tutti gli accessi esterni Azure RTOS NetX Duo, rendendo molto più semplice la determinazione dei rischi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="419a7-298">Also, the application has complete control over all external access to Azure RTOS NetX Duo, making security risk determination much easier.</span></span>

<span data-ttu-id="419a7-299">Microsoft Azure RTOS fornisce agli OEM componenti per proteggere la comunicazione e creare codice e isolamento dei dati usando meccanismi di protezione hardware MCU/MPU sottostanti.</span><span class="sxs-lookup"><span data-stu-id="419a7-299">Microsoft Azure RTOS provides OEMs with components to secure communication and to create code and data isolation using underlying MCU/MPU hardware protection mechanisms.</span></span> <span data-ttu-id="419a7-300">È in definitiva responsabilità del generatore di dispositivi garantire che il dispositivo soddisfi pienamente i requisiti di sicurezza in evoluzione associati al caso d'uso specifico.</span><span class="sxs-lookup"><span data-stu-id="419a7-300">It is ultimately the responsibility of the device builder to ensure the device fully meets the evolving security requirements associated with its specific use case.</span></span>


## <a name="interoperability-verification"></a><span data-ttu-id="419a7-301">Verifica dell'interoperabilità</span><span class="sxs-lookup"><span data-stu-id="419a7-301">Interoperability verification</span></span>

<span data-ttu-id="419a7-302">NetX Duo è conforme agli standard RFC e offre interoperabilità completa con i dispositivi per la maggior parte dei fornitori.</span><span class="sxs-lookup"><span data-stu-id="419a7-302">NetX Duo conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span>

![Logo pronto per IPv6](./media/overview-netx-duo/ipv6-ready-logo.png)

<span data-ttu-id="419a7-304">Azure RTOS NetX Duo è uno degli unici stack TCP/IP incorporati per ottenere la rigorosa certificazione del logo IPv6-Ready, dimostrando di aver superato i test di conformità e interoperabilità, amministrati e convalidati dal forum IPv6.</span><span class="sxs-lookup"><span data-stu-id="419a7-304">Azure RTOS NetX Duo is one of the only embedded TCP/IP stacks to achieve the rigorous IPv6-Ready Logo certification, evidence that it has passed conformance and interoperability tests, administered and validated by the IPv6 Forum.</span></span> <span data-ttu-id="419a7-305">NetX Duo usa anche lo standard di settore IxANVL (Automated Network Validation Library) per l'implementazione del protocollo TCP/IP core di NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="419a7-305">NetX Duo also utilizes the industry standard IxANVL (Automated Network Validation Library) for the NetX Duo core TCP/IP protocol implementation.</span></span>

## <a name="comprehensive-iot-solution"></a><span data-ttu-id="419a7-306">Soluzione IoT completa</span><span class="sxs-lookup"><span data-stu-id="419a7-306">Comprehensive IoT solution</span></span>

<span data-ttu-id="419a7-307">NetX Duo offre una delle reti TCP/IP più complete per applicazioni IoT con un'incorporata approfondita.</span><span class="sxs-lookup"><span data-stu-id="419a7-307">NetX Duo has one of the most comprehensive TCP/IP networking for deeply embedded IoT applications.</span></span> <span data-ttu-id="419a7-308">Questo supporto include i prodotti del protocollo aggiuntivo seguenti.</span><span class="sxs-lookup"><span data-stu-id="419a7-308">This support includes the following add-on protocol products.</span></span>

<span data-ttu-id="419a7-309">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPsec, AutoIP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPsec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span><span class="sxs-lookup"><span data-stu-id="419a7-309">MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPsec, AutoIP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPsec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="419a7-310">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="419a7-310">Advanced technology</span></span>

<span data-ttu-id="419a7-311">Azure RTOS NetX Duo è una tecnologia avanzata che include:</span><span class="sxs-lookup"><span data-stu-id="419a7-311">Azure RTOS NetX Duo is advanced technology that includes:</span></span>

* <span data-ttu-id="419a7-312">Architettura di Piconet™</span><span class="sxs-lookup"><span data-stu-id="419a7-312">Piconet™ architecture</span></span>
* <span data-ttu-id="419a7-313">Scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="419a7-313">Automatic scaling</span></span>
* <span data-ttu-id="419a7-314">Tecnologia Fast-Path UDP™</span><span class="sxs-lookup"><span data-stu-id="419a7-314">UDP Fast-Path Technology™</span></span>
* <span data-ttu-id="419a7-315">Gestione flessibile dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="419a7-315">Flexible packet management</span></span>
* <span data-ttu-id="419a7-316">API e implementazione in copia zero</span><span class="sxs-lookup"><span data-stu-id="419a7-316">Zero-copy API and implementation</span></span>
* <span data-ttu-id="419a7-317">Supporto multihomed</span><span class="sxs-lookup"><span data-stu-id="419a7-317">Multihomed support</span></span>
* <span data-ttu-id="419a7-318">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="419a7-318">Optional timeout on all suspension</span></span>
* <span data-ttu-id="419a7-319">Supporto del routing statico</span><span class="sxs-lookup"><span data-stu-id="419a7-319">Static routing support</span></span>
* <span data-ttu-id="419a7-320">IPsec</span><span class="sxs-lookup"><span data-stu-id="419a7-320">IPsec</span></span>
* <span data-ttu-id="419a7-321">SSL/TLS/DTLS</span><span class="sxs-lookup"><span data-stu-id="419a7-321">SSL/TLS/DTLS</span></span>
* <span data-ttu-id="419a7-322">Azure RTOS di analisi del sistema TraceX</span><span class="sxs-lookup"><span data-stu-id="419a7-322">Azure RTOS TraceX system analysis support</span></span>

## <a name="related-services"></a><span data-ttu-id="419a7-323">Servizi correlati</span><span class="sxs-lookup"><span data-stu-id="419a7-323">Related services</span></span>

<span data-ttu-id="419a7-324">Il Centro sicurezza di Azure per la sicurezza RTOS IoT offre una soluzione di sicurezza completa per Azure RTOS dispositivi.</span><span class="sxs-lookup"><span data-stu-id="419a7-324">The Azure Security Center for IoT RTOS security module provides a comprehensive security solution for Azure RTOS devices.</span></span> <span data-ttu-id="419a7-325">Il modulo di sicurezza per Azure RTOS rilevamento di attività di rete dannose, la base del comportamento dei dispositivi basato su avvisi personalizzati e contribuisce a migliorare la protezione della sicurezza dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="419a7-325">The Security Module for Azure RTOS offers malicious network activity detection, custom alert based device behavior baselining, and helps improve device security hygiene.</span></span> <span data-ttu-id="419a7-326">Altre informazioni sul modulo [di sicurezza per Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) [](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) guida introduttiva alla configurazione del modulo Azure RTOS sicurezza.</span><span class="sxs-lookup"><span data-stu-id="419a7-326">Learn more about the [Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) or get started with the [Configure Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) quickstart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="419a7-327">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="419a7-327">Next steps</span></span>

<span data-ttu-id="419a7-328">Per altre informazioni su NetX Duo, iniziare con il manuale [Azure RTOS'utente di NetX Duo.](about-this-guide.md)</span><span class="sxs-lookup"><span data-stu-id="419a7-328">To learn more about NetX Duo, start with the [Azure RTOS NetX Duo User Guide](about-this-guide.md).</span></span>
