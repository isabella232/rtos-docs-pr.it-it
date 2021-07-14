---
title: Informazioni Azure RTOS NetX Duo
description: Azure RTOS NetX Duo è uno stack di rete TCP/IP avanzato di livello industriale progettato specificamente per applicazioni IoT e in tempo reale con deep embedded.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: b40a57bf385ddcf623ff7cbe0d2e798c547227d7
ms.sourcegitcommit: dbbec3ba6a7eb6097c7888b235c433a2efd6e5b9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2021
ms.locfileid: "113754897"
---
# <a name="overview-of-azure-rtos-netx-duo"></a><span data-ttu-id="6c2c8-103">Panoramica di Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="6c2c8-103">Overview of Azure RTOS NetX Duo</span></span>

<span data-ttu-id="6c2c8-104">Azure RTOS stack di rete TCP/IP incorporato di NetX Duo è lo stack di rete TCP/IP avanzato e di livello industriale di Microsoft, progettato appositamente per le applicazioni IoT e IPv4 avanzate di livello industriale.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-104">Azure RTOS NetX Duo embedded TCP/IP network stack is Microsoft's advanced, industrial grade dual IPv4 and IPv6 TCP/IP network stack that is designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="6c2c8-105">NetX Duo offre applicazioni incorporate con protocolli di rete di base come IPv4, IPv6, TCP e UDP, nonché una suite completa di protocolli aggiuntivi aggiuntivi di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-105">NetX Duo provides embedded applications with core network protocols such as IPv4, IPv6, TCP, and UDP as well as a complete suite of additional, higher-level add-on protocols.</span></span> <span data-ttu-id="6c2c8-106">Azure RTOS NetX Duo offre sicurezza tramite altri prodotti di sicurezza aggiuntivi, tra cui Azure RTOS NetX Secure IPsec e Azure RTOS NetX Secure SSL/TLS/DTLS.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-106">Azure RTOS NetX Duo offers security via additional add-on security products, including Azure RTOS NetX Secure IPsec and Azure RTOS NetX Secure SSL/TLS/DTLS.</span></span> <span data-ttu-id="6c2c8-107">Tutto questo in combinazione con un footprint ridotto, un'esecuzione rapida e una maggiore facilità d'uso rendono Azure RTOS NetX Duo la scelta ideale per le applicazioni IoT incorporate più complesse.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-107">All of this combined with an small footprint, fast execution, and superior ease-of-use make Azure RTOS NetX Duo the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="6c2c8-108">Protocolli API</span><span class="sxs-lookup"><span data-stu-id="6c2c8-108">API protocols</span></span>

### <a name="mqtt"></a><span data-ttu-id="6c2c8-109">MQTT</span><span class="sxs-lookup"><span data-stu-id="6c2c8-109">MQTT</span></span>

* <span data-ttu-id="6c2c8-110">Trasporto di telemetria della coda di messaggistica (MQTT)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-110">Messaging Queue Telemetry Transport (MQTT)</span></span>
* <span data-ttu-id="6c2c8-111">Flash minimo da 2,7 KB</span><span class="sxs-lookup"><span data-stu-id="6c2c8-111">Minimal 2.7 KB FLASH</span></span>

### <a name="auto-ip"></a><span data-ttu-id="6c2c8-112">IP automatico</span><span class="sxs-lookup"><span data-stu-id="6c2c8-112">Auto IP</span></span>

* <span data-ttu-id="6c2c8-113">Assegnazione automatica di indirizzi IPv4</span><span class="sxs-lookup"><span data-stu-id="6c2c8-113">Automatic IPv4 address assignment</span></span>
* <span data-ttu-id="6c2c8-114">Minimo 1,2 KB, 300 byte di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-114">Minimal 1.2 KB, 300 bytes of RAM</span></span>

### <a name="http-https"></a><span data-ttu-id="6c2c8-115">HTTP, HTTPS</span><span class="sxs-lookup"><span data-stu-id="6c2c8-115">HTTP, HTTPS</span></span>
<span data-ttu-id="6c2c8-116">NetX Duo supporta i protocolli HTTP/HTTPS seguenti.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-116">NetX Duo supports the following HTTP/HTTPS protocols.</span></span>

#### <a name="http-10"></a><span data-ttu-id="6c2c8-117">HTTP 1.0</span><span class="sxs-lookup"><span data-stu-id="6c2c8-117">HTTP 1.0</span></span>

* <span data-ttu-id="6c2c8-118">Hypertext Transfer Protocol(HTTP)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-118">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="6c2c8-119">Memoria FLASH minima da 2,8 KB a 4,8 KB/ da 0,4 KB a 1,0 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-119">Minimal 2.8 KB to 4.8 KB FLASH / 0.4 KB to 1.0 KB RAM</span></span>
* <span data-ttu-id="6c2c8-120">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="6c2c8-120">Client and server support</span></span>

#### <a name="httphttps-11"></a><span data-ttu-id="6c2c8-121">HTTP/HTTPS 1.1</span><span class="sxs-lookup"><span data-stu-id="6c2c8-121">HTTP/HTTPS 1.1</span></span>

* <span data-ttu-id="6c2c8-122">Hypertext Transfer Protocol(HTTP)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-122">Hypertext Transfer Protocol(HTTP)</span></span>
* <span data-ttu-id="6c2c8-123">Memoria FLASH minima da 3,0 KB a 9,5 KB/ da 0,5 KB a 2 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-123">Minimal 3.0 KB to 9.5 KB FLASH / 0.5 KB to 2 KB RAM</span></span>
* <span data-ttu-id="6c2c8-124">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="6c2c8-124">Client and server support</span></span>
* <span data-ttu-id="6c2c8-125">Più sessioni client in ingresso</span><span class="sxs-lookup"><span data-stu-id="6c2c8-125">Multiple incoming client sessions</span></span>
* <span data-ttu-id="6c2c8-126">Testo normale e HTTPS crittografato</span><span class="sxs-lookup"><span data-stu-id="6c2c8-126">Plain text and encrypted HTTPS</span></span>
* <span data-ttu-id="6c2c8-127">Supporto delle connessioni permanenti</span><span class="sxs-lookup"><span data-stu-id="6c2c8-127">Persistent connection support</span></span>
* <span data-ttu-id="6c2c8-128">Caricamento di file multipart</span><span class="sxs-lookup"><span data-stu-id="6c2c8-128">Multipart file upload</span></span>
* <span data-ttu-id="6c2c8-129">Completamente integrato con Azure RTOS NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="6c2c8-129">Fully integrated with Azure RTOS NetX Secure TLS</span></span>

### <a name="smtp"></a><span data-ttu-id="6c2c8-130">SMTP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-130">SMTP</span></span>

* <span data-ttu-id="6c2c8-131">Simple Mall Transfer Protocol (SMTP)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-131">Simple Mall Transfer Protocol (SMTP)</span></span>
* <span data-ttu-id="6c2c8-132">Footprint minimo di 4,1 KB e 0,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-132">Minimal 4.1 KB and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="6c2c8-133">Supporto client</span><span class="sxs-lookup"><span data-stu-id="6c2c8-133">Client support</span></span>

### <a name="dhcp"></a><span data-ttu-id="6c2c8-134">DHCP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-134">DHCP</span></span>

* <span data-ttu-id="6c2c8-135">Dynamic Host Configuration Protocol (DHCP)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-135">Dynamic Host Configuration Protocol (DHCP)</span></span>
* <span data-ttu-id="6c2c8-136">Footprint minimo da 3,6 KB a 4,6 KB FLASH, 2,7 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-136">Minimal 3.6 KB to 4.6 KB FLASH, 2.7 KB RAM footprint</span></span>
* <span data-ttu-id="6c2c8-137">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="6c2c8-137">Client and server support</span></span>
* <span data-ttu-id="6c2c8-138">Supporto per IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="6c2c8-138">IPv4 and IPv6 support</span></span>

### <a name="nat"></a><span data-ttu-id="6c2c8-139">NAT</span><span class="sxs-lookup"><span data-stu-id="6c2c8-139">NAT</span></span>

* <span data-ttu-id="6c2c8-140">Network Address Translation (NAT)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-140">Network Address Translation (NAT)</span></span>
* <span data-ttu-id="6c2c8-141">Footprint minimo di 3,5 K6 e 0,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-141">Minimal 3.5K6 and 0.6 KB RAM footprint</span></span>
* <span data-ttu-id="6c2c8-142">Supporto degli indirizzi IPv4</span><span class="sxs-lookup"><span data-stu-id="6c2c8-142">IPv4 address support</span></span>
* <span data-ttu-id="6c2c8-143">NAT è disponibile solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="6c2c8-143">NAT is only available with Azure RTOS NetX Duo</span></span>

### <a name="snmp"></a><span data-ttu-id="6c2c8-144">SNMP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-144">SNMP</span></span>

* <span data-ttu-id="6c2c8-145">Simple Network Management Protocol (SNMP)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-145">Simple Network Management Protocol (SNMP)</span></span>
* <span data-ttu-id="6c2c8-146">Footprint minimo di 10,9 KB e 2,6 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-146">Minimal 10.9 KB and 2.6 KB RAM footprint</span></span>
* <span data-ttu-id="6c2c8-147">Supporto dell'agente per VI, V2 e V3</span><span class="sxs-lookup"><span data-stu-id="6c2c8-147">Agent support for VI, V2, and V3</span></span>

### <a name="dns-mdns-dns-sd"></a><span data-ttu-id="6c2c8-148">DNS, mDNS, DNS-SD</span><span class="sxs-lookup"><span data-stu-id="6c2c8-148">DNS, mDNS, DNS-SD</span></span>

* <span data-ttu-id="6c2c8-149">Domain Name System (DNS)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-149">Domain Name System (DNS)</span></span>
* <span data-ttu-id="6c2c8-150">Multicast Domain Name System (mDNS)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-150">Multicast Domain Name System (mDNS)</span></span>
* <span data-ttu-id="6c2c8-151">Individuazione dei servizi basati su DNS (DNS-SD)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-151">DNS-based service discovery (DNS-SD)</span></span>
* <span data-ttu-id="6c2c8-152">DNS minimo da 2,4 KB a 3 KB FLASH, footprint ram da 1 KB</span><span class="sxs-lookup"><span data-stu-id="6c2c8-152">DNS Minimal 2.4 KB to 3 KB FLASH, 1 KB RAM footprint</span></span>
* <span data-ttu-id="6c2c8-153">Supporto client</span><span class="sxs-lookup"><span data-stu-id="6c2c8-153">Client support</span></span>
* <span data-ttu-id="6c2c8-154">mDNS e DNS-SD sono disponibili solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="6c2c8-154">mDNS and DNS-SD are only available with Azure RTOS NetX Duo</span></span>

### <a name="pop3"></a><span data-ttu-id="6c2c8-155">POP3</span><span class="sxs-lookup"><span data-stu-id="6c2c8-155">POP3</span></span>

* <span data-ttu-id="6c2c8-156">Post Office Protocol versione 3 (POP3)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-156">Post Office Protocol Version 3 (POP3)</span></span>
* <span data-ttu-id="6c2c8-157">Footprint minimo di 8,1 KB e 1,4 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-157">Minimal 8.1 KB and 1.4 KB RAM footprint</span></span>
* <span data-ttu-id="6c2c8-158">Supporto client</span><span class="sxs-lookup"><span data-stu-id="6c2c8-158">Client support</span></span>

### <a name="telnet"></a><span data-ttu-id="6c2c8-159">Telnet</span><span class="sxs-lookup"><span data-stu-id="6c2c8-159">TELNET</span></span>

* <span data-ttu-id="6c2c8-160">Footprint minimo di 0,5 KB e 0,3 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-160">Minimal 0.5 KB and 0.3 KB RAM footprint</span></span>
* <span data-ttu-id="6c2c8-161">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="6c2c8-161">Client and server support</span></span>
* <span data-ttu-id="6c2c8-162">API Telnet intuitive: *nx_telnet_ \**</span><span class="sxs-lookup"><span data-stu-id="6c2c8-162">Intuitive Telnet APIs: *nx_telnet_\**</span></span>

### <a name="ftp-tftp"></a><span data-ttu-id="6c2c8-163">FTP, TFTP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-163">FTP, TFTP</span></span>

* <span data-ttu-id="6c2c8-164">File Transfer Protocol (FTP)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-164">File Transfer Protocol (FTP)</span></span>
* <span data-ttu-id="6c2c8-165">Trivial File Transfer Protocol (TFTP)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-165">Trivial File Transfer Protocol (TFTP)</span></span>
* <span data-ttu-id="6c2c8-166">FTP minimo da 1,8 KB a 7,2 KB FLASH, da 0,6 KB a 2,1 KB ram footprint</span><span class="sxs-lookup"><span data-stu-id="6c2c8-166">FTP Minimal 1.8 KB to 7.2 KB FLASH, 0.6 KB to 2.1 KB RAM footprint</span></span>
* <span data-ttu-id="6c2c8-167">TFTP minimo da 1,7 KB a 2,4 KB FLASH, da 0,3 KB a 1,8 KB ram footprint</span><span class="sxs-lookup"><span data-stu-id="6c2c8-167">TFTP Minimal 1.7 KB to 2.4 KB FLASH, 0.3 KB to 1.8 KB RAM footprint</span></span>
* <span data-ttu-id="6c2c8-168">Supporto client e server</span><span class="sxs-lookup"><span data-stu-id="6c2c8-168">Client and server support</span></span>
* <span data-ttu-id="6c2c8-169">API FTP e TFTP *intuitive: nx_ftp_ \** o *nx_tftp_ \**</span><span class="sxs-lookup"><span data-stu-id="6c2c8-169">Intuitive FTP and TFTP APIs: *nx_ftp_\** or *nx_tftp_\**</span></span>

### <a name="ppp-pppoe"></a><span data-ttu-id="6c2c8-170">PPP, PPPoE</span><span class="sxs-lookup"><span data-stu-id="6c2c8-170">PPP, PPPoE</span></span>

* <span data-ttu-id="6c2c8-171">Protocollo PPP (Polnt-to-PoInt)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-171">Polnt-to-PoInt Protocol (PPP)</span></span>
* <span data-ttu-id="6c2c8-172">Point-to-Point Protocol over Ethernet(PPPoE)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-172">Point-to-Point Protocol over Ethernet(PPPoE)</span></span>
* <span data-ttu-id="6c2c8-173">Footprint minimo di 7,1 KB e 3,8 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-173">Minimal 7.1 KB and 3.8 KB RAM footprint</span></span>
* <span data-ttu-id="6c2c8-174">API PPP intuitive: *nx_ppp_ \**</span><span class="sxs-lookup"><span data-stu-id="6c2c8-174">Intuitive PPP APIs: *nx_ppp_\**</span></span>

* <span data-ttu-id="6c2c8-175">PPPoE è disponibile solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="6c2c8-175">PPPoE is only available with Azure RTOS NetX Duo</span></span>

### <a name="sntp"></a><span data-ttu-id="6c2c8-176">SNTP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-176">SNTP</span></span>

* <span data-ttu-id="6c2c8-177">Simple Network Time Protocol (SNTP)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-177">Simple Network Time Protocol (SNTP)</span></span>
* <span data-ttu-id="6c2c8-178">Minimo 4 KB e 0,5 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-178">Minimal 4 KB and 0.5 KB RAM</span></span>
* <span data-ttu-id="6c2c8-179">Supporto client</span><span class="sxs-lookup"><span data-stu-id="6c2c8-179">Client support</span></span>
* <span data-ttu-id="6c2c8-180">API SNTP intuitive: *nx_sntp_ \**</span><span class="sxs-lookup"><span data-stu-id="6c2c8-180">Intuitive SNTP APIs: *nx_sntp_\**</span></span>

### <a name="legacy-code-support"></a><span data-ttu-id="6c2c8-181">Supporto del codice legacy</span><span class="sxs-lookup"><span data-stu-id="6c2c8-181">Legacy code support</span></span>

* <span data-ttu-id="6c2c8-182">Livello BSD facoltativo per la portabilità del codice socket legacy</span><span class="sxs-lookup"><span data-stu-id="6c2c8-182">Optional BSD layer for porting legacy socket code</span></span>

### <a name="igmp"></a><span data-ttu-id="6c2c8-183">Igmp</span><span class="sxs-lookup"><span data-stu-id="6c2c8-183">IGMP</span></span>

* <span data-ttu-id="6c2c8-184">IGMP (Internet Group Management Protocol)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-184">Internet Group Management Protocol (IGMP)</span></span>
* <span data-ttu-id="6c2c8-185">Flash minimo da 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="6c2c8-185">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="6c2c8-186">Supporto dei gruppi multicast IPv4</span><span class="sxs-lookup"><span data-stu-id="6c2c8-186">IPv4 multicast group support</span></span>
* <span data-ttu-id="6c2c8-187">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="6c2c8-187">IXIA IxANVL validated</span></span>
* <span data-ttu-id="6c2c8-188">Statistiche IGMP facoltative</span><span class="sxs-lookup"><span data-stu-id="6c2c8-188">Optional IGMP statistics</span></span>
* <span data-ttu-id="6c2c8-189">Traccia a livello di sistema tramite Azure RTOS ThreadX</span><span class="sxs-lookup"><span data-stu-id="6c2c8-189">System-level trace via Azure RTOS ThreadX</span></span>
* <span data-ttu-id="6c2c8-190">API IGMP intuitive: *nx_igmp_ \**</span><span class="sxs-lookup"><span data-stu-id="6c2c8-190">Intuitive IGMP APIs: *nx_igmp_\**</span></span>

### <a name="azure-rtos-netx-secure-dtls"></a><span data-ttu-id="6c2c8-191">Azure RTOS DTLS sicuri di NetX</span><span class="sxs-lookup"><span data-stu-id="6c2c8-191">Azure RTOS NetX Secure DTLS</span></span>

* <span data-ttu-id="6c2c8-192">Datagram Transport Layer Security (DTLS) 1.0 e 1.2</span><span class="sxs-lookup"><span data-stu-id="6c2c8-192">Datagram Transport Layer Security (DTLS) 1.0 and 1.2</span></span>
* <span data-ttu-id="6c2c8-193">FLASH minimo di 11 KB</span><span class="sxs-lookup"><span data-stu-id="6c2c8-193">Minimal 11 KB FLASH</span></span>
* <span data-ttu-id="6c2c8-194">Fast, software RSA 2048-bit key size ~1-second @120MHz</span><span class="sxs-lookup"><span data-stu-id="6c2c8-194">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="6c2c8-195">Implementazione semplificata di X.509</span><span class="sxs-lookup"><span data-stu-id="6c2c8-195">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="6c2c8-196">Completamente integrato con i Azure RTOS UDP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="6c2c8-196">Fully integrated with Azure RTOS NetX Duo UDP sockets</span></span>
* <span data-ttu-id="6c2c8-197">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="6c2c8-197">Hardware Crypto Support</span></span>
* <span data-ttu-id="6c2c8-198">Supporto della crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-198">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="6c2c8-199">Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse le curve P 192/224/256/384/521</span><span class="sxs-lookup"><span data-stu-id="6c2c8-199">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="6c2c8-200">Supporto delle chiavi crittografate (dipendente dall'hardware)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-200">Encrypted Key Support (hardware dependent)</span></span>

### <a name="azure-rtos-netx-secure-tls"></a><span data-ttu-id="6c2c8-201">Azure RTOS NetX Secure TLS</span><span class="sxs-lookup"><span data-stu-id="6c2c8-201">Azure RTOS NetX Secure TLS</span></span>

* <span data-ttu-id="6c2c8-202">Transport Layer Security (TLS) 1.0, 1.1 e 1.2</span><span class="sxs-lookup"><span data-stu-id="6c2c8-202">Transport Layer Security (TLS) 1.0, 1.1, and 1.2</span></span>
* <span data-ttu-id="6c2c8-203">Flash minimo da 8,8 KB</span><span class="sxs-lookup"><span data-stu-id="6c2c8-203">Minimal 8.8 KB FLASH</span></span>
* <span data-ttu-id="6c2c8-204">Fast, software RSA 2048-bit key size ~1-second @120MHz</span><span class="sxs-lookup"><span data-stu-id="6c2c8-204">Fast, software RSA 2048-bit key size ~1-second @120MHz</span></span>
* <span data-ttu-id="6c2c8-205">Implementazione semplificata di X.509</span><span class="sxs-lookup"><span data-stu-id="6c2c8-205">Streamlined X.509 Implementation</span></span>
* <span data-ttu-id="6c2c8-206">Completamente integrato con Azure RTOS TCP NetX Duo</span><span class="sxs-lookup"><span data-stu-id="6c2c8-206">Fully integrated with Azure RTOS NetX Duo TCP sockets</span></span>
* <span data-ttu-id="6c2c8-207">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="6c2c8-207">Hardware Crypto Support</span></span>
* <span data-ttu-id="6c2c8-208">Supporto della crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-208">Software Crypto Support: RSA (all key sizes), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)</span></span>
* <span data-ttu-id="6c2c8-209">Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse le curve P 192/224/256/384/521</span><span class="sxs-lookup"><span data-stu-id="6c2c8-209">Elliptic Curve Cryptography (ECC) with ECDSA (signing) and ECDH (encryption), including P-curves 192/224/256/384/521</span></span>
* <span data-ttu-id="6c2c8-210">Supporto delle chiavi crittografate (dipendente dall'hardware)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-210">Encrypted Key Support (hardware dependent)</span></span>

### <a name="icmp"></a><span data-ttu-id="6c2c8-211">ICMP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-211">ICMP</span></span>

* <span data-ttu-id="6c2c8-212">Internet Control Message Protocol (ICMP)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-212">Internet Control Message Protocol (ICMP)</span></span>
* <span data-ttu-id="6c2c8-213">Flash minimo da 2,5 KB</span><span class="sxs-lookup"><span data-stu-id="6c2c8-213">Minimal 2.5 KB FLASH</span></span>
* <span data-ttu-id="6c2c8-214">Supporto per IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="6c2c8-214">IPv4 and IPv6 support</span></span>
* <span data-ttu-id="6c2c8-215">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="6c2c8-215">IXIA IxANVL validated</span></span>
* <span data-ttu-id="6c2c8-216">Richiesta ping e risposta ping</span><span class="sxs-lookup"><span data-stu-id="6c2c8-216">Ping request and ping response</span></span>
* <span data-ttu-id="6c2c8-217">Sospensione facoltativa dei thread nelle richieste ping</span><span class="sxs-lookup"><span data-stu-id="6c2c8-217">Optional thread suspension on ping requests</span></span>
* <span data-ttu-id="6c2c8-218">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="6c2c8-218">Optional timeout on all suspension</span></span>
* <span data-ttu-id="6c2c8-219">Statistiche ICMP facoltative</span><span class="sxs-lookup"><span data-stu-id="6c2c8-219">Optional ICMP statistics</span></span>
* <span data-ttu-id="6c2c8-220">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="6c2c8-220">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="6c2c8-221">API ICMP intuitive: *nx_icmp_ \**</span><span class="sxs-lookup"><span data-stu-id="6c2c8-221">Intuitive ICMP APIs: *nx_icmp_\**</span></span>

### <a name="udp"></a><span data-ttu-id="6c2c8-222">UDP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-222">UDP</span></span>

* <span data-ttu-id="6c2c8-223">Udp (User Datagram Protocol)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-223">User Datagram Protocol (UDP)</span></span>
* <span data-ttu-id="6c2c8-224">MINIMO FLASH da 2,5 KB, 124 socket di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="6c2c8-224">Minimal 2.5 KB FLASH, 124 sockets bytes of RAM per socket</span></span>
* <span data-ttu-id="6c2c8-225">Elaborazione rapida dei pacchetti TCP in prossimità di wirespeed:</span><span class="sxs-lookup"><span data-stu-id="6c2c8-225">Fast, near wirespeed TCP packet processing:</span></span>
    * <span data-ttu-id="6c2c8-226">RX 95 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 14%</span><span class="sxs-lookup"><span data-stu-id="6c2c8-226">RX 95 Mbps on 100 Mbps Ethernet, MCU @100MHz, 14% MCU utilization</span></span>
    * <span data-ttu-id="6c2c8-227">TX 94 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 10%</span><span class="sxs-lookup"><span data-stu-id="6c2c8-227">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 10% MCU utilization</span></span>
* <span data-ttu-id="6c2c8-228">Tecnologia udp Fast Path™</span><span class="sxs-lookup"><span data-stu-id="6c2c8-228">UDP Fast Path™ technology</span></span>
* <span data-ttu-id="6c2c8-229">Nessun limite al numero di UDP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-229">No limits on the number of UDP</span></span>
* <span data-ttu-id="6c2c8-230">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="6c2c8-230">IXIA IxANVL validated</span></span>
* <span data-ttu-id="6c2c8-231">Sospensione facoltativa alla ricezione socket</span><span class="sxs-lookup"><span data-stu-id="6c2c8-231">Optional suspension on socket receive</span></span>
* <span data-ttu-id="6c2c8-232">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="6c2c8-232">Optional timeout on all suspension</span></span>
* <span data-ttu-id="6c2c8-233">Statistiche UDP facoltative</span><span class="sxs-lookup"><span data-stu-id="6c2c8-233">Optional UDP statistics</span></span>
* <span data-ttu-id="6c2c8-234">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="6c2c8-234">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="6c2c8-235">API UDP intuitive: *nx_udp_ \**</span><span class="sxs-lookup"><span data-stu-id="6c2c8-235">Intuitive UDP APIs: *nx_udp_\**</span></span>

### <a name="tcp"></a><span data-ttu-id="6c2c8-236">TCP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-236">TCP</span></span>

* <span data-ttu-id="6c2c8-237">TCP (Transmission Control Protocol)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-237">Transmission Control Protocol (TCP)</span></span>
* <span data-ttu-id="6c2c8-238">Flash minimo da 10,5 KB a 12,5 KB, 280 byte di RAM per socket</span><span class="sxs-lookup"><span data-stu-id="6c2c8-238">Minimal 10.5K8 to 12.5 KB FLASH, 280 bytes of RAM per socket</span></span>
* <span data-ttu-id="6c2c8-239">Elaborazione rapida dei pacchetti TCP in prossimità di wlrespeed:</span><span class="sxs-lookup"><span data-stu-id="6c2c8-239">Fast, near wlrespeed TCP packet processing:</span></span>
    * <span data-ttu-id="6c2c8-240">RX 93 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 20%</span><span class="sxs-lookup"><span data-stu-id="6c2c8-240">RX 93 Mbps on 100 Mbps Ethernet, MCU @100MHz, 20% MCU utilization</span></span>
    * <span data-ttu-id="6c2c8-241">TX 94 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 27%</span><span class="sxs-lookup"><span data-stu-id="6c2c8-241">TX 94 Mbps on 100 Mbps Ethernet, MCU @100MHz, 27% MCU utilization</span></span>
* <span data-ttu-id="6c2c8-242">Connessione affidabile</span><span class="sxs-lookup"><span data-stu-id="6c2c8-242">Reliable connection</span></span>
* <span data-ttu-id="6c2c8-243">Nessun limite al numero di socket TCP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-243">No limits on the number of TCP sockets</span></span>
* <span data-ttu-id="6c2c8-244">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="6c2c8-244">IXIA IxANVL validated</span></span>
* <span data-ttu-id="6c2c8-245">Sospensione facoltativa nella ricezione/trasmissione socket</span><span class="sxs-lookup"><span data-stu-id="6c2c8-245">Optional suspension on socket receive/transmit</span></span>
* <span data-ttu-id="6c2c8-246">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="6c2c8-246">Optional timeout on all suspension</span></span>
* <span data-ttu-id="6c2c8-247">Statistiche TCP facoltative</span><span class="sxs-lookup"><span data-stu-id="6c2c8-247">Optional TCP statistics</span></span>
* <span data-ttu-id="6c2c8-248">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="6c2c8-248">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="6c2c8-249">API TCP intuitive: *nx_tcp_ \**</span><span class="sxs-lookup"><span data-stu-id="6c2c8-249">Intuitive TCP APIs: *nx_tcp_\**</span></span>

### <a name="arprarp"></a><span data-ttu-id="6c2c8-250">ARP/RARP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-250">ARP/RARP</span></span>

* <span data-ttu-id="6c2c8-251">ARP (Address Resolution Protocol)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-251">Address Resolution Protocol (ARP)</span></span>
* <span data-ttu-id="6c2c8-252">RaRP (Reverse Address Resolution Protocol)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-252">Reverse Address Resolution Protocol (RARP)</span></span>
* <span data-ttu-id="6c2c8-253">Minimo 1,7 KB FLASH, dimensioni della RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-253">Minimal 1.7 KB FLASH, RAM size</span></span>
* <span data-ttu-id="6c2c8-254">Risoluzione dinamica di indirizzi MAC da 32 blt IPv4 e 48 blt</span><span class="sxs-lookup"><span data-stu-id="6c2c8-254">Dynamic resolution of 32-blt IPv4 and 48-blt MAC addresses</span></span>
* <span data-ttu-id="6c2c8-255">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="6c2c8-255">IXIA IxANVL validated</span></span>
* <span data-ttu-id="6c2c8-256">Cache ARP flessibile e definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="6c2c8-256">Flexible, user-defined ARP cache</span></span>
* <span data-ttu-id="6c2c8-257">Supporto gratuito ARP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-257">Gratuitous ARP support</span></span>
* <span data-ttu-id="6c2c8-258">Statistiche ARP/RARP facoltative determinate dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="6c2c8-258">Optional ARP/RARP statistics determined by application</span></span>
* <span data-ttu-id="6c2c8-259">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="6c2c8-259">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="6c2c8-260">API ARP/RARP intuitive: *nx_arp_ \**, *nx_rarp_ \**</span><span class="sxs-lookup"><span data-stu-id="6c2c8-260">Intuitive ARP/RARP APIs: *nx_arp_\**, *nx_rarp_\**</span></span>

### <a name="ipv4-amp-ipv6"></a><span data-ttu-id="6c2c8-261">IPv4 &amp; IPv6</span><span class="sxs-lookup"><span data-stu-id="6c2c8-261">IPv4 &amp; IPv6</span></span>

* <span data-ttu-id="6c2c8-262">Ip (Internet Protocol)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-262">Internet Protocol (IP)</span></span>
* <span data-ttu-id="6c2c8-263">Footprint minimo da 3,5 KB a 8,5 KB FLASH, da 2 KB a 3 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="6c2c8-263">Minimal 3.5 KB to 8.5 KB FLASH, 2 KB to 3 KB RAM footprint</span></span>
* <span data-ttu-id="6c2c8-264">Architettura di Piconet™</span><span class="sxs-lookup"><span data-stu-id="6c2c8-264">Piconet™ architecture</span></span>
* <span data-ttu-id="6c2c8-265">Prestazioni veloci e near wirespeed</span><span class="sxs-lookup"><span data-stu-id="6c2c8-265">Fast, near wirespeed performance</span></span>
* <span data-ttu-id="6c2c8-266">Supporto di più interfacce</span><span class="sxs-lookup"><span data-stu-id="6c2c8-266">Multiple interface support</span></span>
* <span data-ttu-id="6c2c8-267">Supporto multihomed</span><span class="sxs-lookup"><span data-stu-id="6c2c8-267">Multihomed support</span></span>
* <span data-ttu-id="6c2c8-268">Supporto del routing statico</span><span class="sxs-lookup"><span data-stu-id="6c2c8-268">Static routing support</span></span>
* <span data-ttu-id="6c2c8-269">Supporto della frammentazione/riassemblaggio IP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-269">IP fragmentation/reassembly support</span></span>
* <span data-ttu-id="6c2c8-270">Supporto degli indirizzi IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="6c2c8-270">IPv4 and IPv6 address support</span></span>
* <span data-ttu-id="6c2c8-271">IXIA IxANVL convalidato</span><span class="sxs-lookup"><span data-stu-id="6c2c8-271">IXIA IxANVL validated</span></span>
* <span data-ttu-id="6c2c8-272">Certificazione del logo pronto per IPv6 di fase II</span><span class="sxs-lookup"><span data-stu-id="6c2c8-272">Phase II IPv6 Ready Logo Certification</span></span>
* <span data-ttu-id="6c2c8-273">Statistiche IP facoltative</span><span class="sxs-lookup"><span data-stu-id="6c2c8-273">Optional IP statistics</span></span>
* <span data-ttu-id="6c2c8-274">Interfaccia del driver del livello fisico ben definita e intuitiva</span><span class="sxs-lookup"><span data-stu-id="6c2c8-274">Well defined, intuitive physical layer driver interface</span></span>
* <span data-ttu-id="6c2c8-275">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="6c2c8-275">System-level trace via Azure RTOS TraceX</span></span>
* <span data-ttu-id="6c2c8-276">API del livello IP intuitive: *\* nx_ip_*, *nxd_ip_ \** *\** , nxd_ipv6_</span><span class="sxs-lookup"><span data-stu-id="6c2c8-276">Intuitive IP layer APIs: *nx_ip_\**, *nxd_ip_\**, *nxd_ipv6_\**</span></span>
* <span data-ttu-id="6c2c8-277">Precertificato da TUV e UL a IEC 61508 SIL 4, IEC 62304 Classe C, ISO 26262 ASIL D e EN 50128 SW-SIL4</span><span class="sxs-lookup"><span data-stu-id="6c2c8-277">Pre-certified by TUV and UL to IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D, and EN 50128 SW-SIL4</span></span>

### <a name="azure-rtos-netx-secure-ipsec"></a><span data-ttu-id="6c2c8-278">Azure RTOS IPSEC sicuro di NetX</span><span class="sxs-lookup"><span data-stu-id="6c2c8-278">Azure RTOS NetX Secure IPSEC</span></span>

* <span data-ttu-id="6c2c8-279">IpSec (Internet Protocol Security)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-279">Internet Protocol Security (IPSEC)</span></span>
* <span data-ttu-id="6c2c8-280">Livello IP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-280">IP layer</span></span>
* <span data-ttu-id="6c2c8-281">Supporto della crittografia hardware</span><span class="sxs-lookup"><span data-stu-id="6c2c8-281">Hardware crypto support</span></span>
* <span data-ttu-id="6c2c8-282">Supporto della crittografia software, tra cui:</span><span class="sxs-lookup"><span data-stu-id="6c2c8-282">Software crypto support, including:</span></span>
    * <span data-ttu-id="6c2c8-283">DES, 3DES</span><span class="sxs-lookup"><span data-stu-id="6c2c8-283">DES, 3DES</span></span>
    * <span data-ttu-id="6c2c8-284">AES</span><span class="sxs-lookup"><span data-stu-id="6c2c8-284">AES</span></span>
    * <span data-ttu-id="6c2c8-285">HMAC-MD5</span><span class="sxs-lookup"><span data-stu-id="6c2c8-285">HMAC-MD5</span></span>
    * <span data-ttu-id="6c2c8-286">HMAC-SHA1</span><span class="sxs-lookup"><span data-stu-id="6c2c8-286">HMAC-SHA1</span></span>
* <span data-ttu-id="6c2c8-287">Supporto di Internet Key Exchange (IKE) versione 2</span><span class="sxs-lookup"><span data-stu-id="6c2c8-287">Internet Key Exchange (IKE) Version 2 support</span></span>
* <span data-ttu-id="6c2c8-288">API IPsec intuitive: *nx_ipsec_ \**</span><span class="sxs-lookup"><span data-stu-id="6c2c8-288">Intuitive IPsec APIs: *nx_ipsec_\**</span></span>
* <span data-ttu-id="6c2c8-289">IPsec è disponibile solo con Azure RTOS NetX Duo</span><span class="sxs-lookup"><span data-stu-id="6c2c8-289">IPsec is only available with Azure RTOS NetX Duo</span></span>

## <a name="safe-and-secure"></a><span data-ttu-id="6c2c8-290">Cassaforte e sicuro</span><span class="sxs-lookup"><span data-stu-id="6c2c8-290">Safe and secure</span></span>

<span data-ttu-id="6c2c8-291">Azure RTOS NetX Duo è sicuro.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-291">Azure RTOS NetX Duo is secure.</span></span> <span data-ttu-id="6c2c8-292">Questa sicurezza viene fornita tramite prodotti di sicurezza aggiuntivi, tra cui IPsec, SSL, TLS e DTLS.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-292">This security is provided through add-on security products, including IPsec, SSL, TLS, and DTLS.</span></span> <span data-ttu-id="6c2c8-293">Inoltre, l'applicazione ha il controllo completo su tutti gli accessi esterni Azure RTOS NetX Duo, rendendo molto più semplice la determinazione dei rischi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-293">Also, the application has complete control over all external access to Azure RTOS NetX Duo, making security risk determination much easier.</span></span>

<span data-ttu-id="6c2c8-294">Microsoft Azure RTOS fornisce agli OEM componenti per proteggere la comunicazione e creare codice e isolamento dei dati usando i meccanismi di protezione hardware MCU/MPU sottostanti.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-294">Microsoft Azure RTOS provides OEMs with components to secure communication and to create code and data isolation using underlying MCU/MPU hardware protection mechanisms.</span></span> <span data-ttu-id="6c2c8-295">È in definitiva responsabilità del generatore di dispositivi garantire che il dispositivo soddisfi pienamente i requisiti di sicurezza in evoluzione associati al caso d'uso specifico.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-295">It is ultimately the responsibility of the device builder to ensure the device fully meets the evolving security requirements associated with its specific use case.</span></span>

## <a name="interoperability-verification"></a><span data-ttu-id="6c2c8-296">Verifica dell'interoperabilità</span><span class="sxs-lookup"><span data-stu-id="6c2c8-296">Interoperability verification</span></span>

<span data-ttu-id="6c2c8-297">NetX Duo è conforme agli standard RFC e offre interoperabilità completa con i dispositivi per la maggior parte dei fornitori.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-297">NetX Duo conforms to RFC standards and offers complete interoperability with devices for most vendors.</span></span>

![Logo pronto per IPv6](./media/overview-netx-duo/ipv6-ready-logo.png)

<span data-ttu-id="6c2c8-299">Azure RTOS NetX Duo è uno degli unici stack TCP/IP incorporati per ottenere la rigorosa certificazione del logo IPv6-Ready, dimostrando di aver superato i test di conformità e interoperabilità, amministrati e convalidati dal forum IPv6.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-299">Azure RTOS NetX Duo is one of the only embedded TCP/IP stacks to achieve the rigorous IPv6-Ready Logo certification, evidence that it has passed conformance and interoperability tests, administered and validated by the IPv6 Forum.</span></span> <span data-ttu-id="6c2c8-300">NetX Duo usa anche lo standard di settore IxANVL (Automated Network Validation Library) per l'implementazione del protocollo TCP/IP core di NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-300">NetX Duo also utilizes the industry standard IxANVL (Automated Network Validation Library) for the NetX Duo core TCP/IP protocol implementation.</span></span>

## <a name="comprehensive-iot-solution"></a><span data-ttu-id="6c2c8-301">Soluzione IoT completa</span><span class="sxs-lookup"><span data-stu-id="6c2c8-301">Comprehensive IoT solution</span></span>

<span data-ttu-id="6c2c8-302">NetX Duo offre una delle reti TCP/IP più complete per applicazioni IoT con un'incorporata approfondita.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-302">NetX Duo has one of the most comprehensive TCP/IP networking for deeply embedded IoT applications.</span></span> <span data-ttu-id="6c2c8-303">Questo supporto include i prodotti del protocollo aggiuntivo seguenti.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-303">This support includes the following add-on protocol products.</span></span>

* <span data-ttu-id="6c2c8-304">MQTT</span><span class="sxs-lookup"><span data-stu-id="6c2c8-304">MQTT</span></span>
* <span data-ttu-id="6c2c8-305">CoAP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-305">CoAP</span></span>
* <span data-ttu-id="6c2c8-306">LWM2M</span><span class="sxs-lookup"><span data-stu-id="6c2c8-306">LWM2M</span></span>
* <span data-ttu-id="6c2c8-307">6LoWPAN</span><span class="sxs-lookup"><span data-stu-id="6c2c8-307">6LoWPAN</span></span>
* <span data-ttu-id="6c2c8-308">SSL/TLS/DTLS</span><span class="sxs-lookup"><span data-stu-id="6c2c8-308">SSL/TLS/DTLS</span></span>
* <span data-ttu-id="6c2c8-309">IPsec</span><span class="sxs-lookup"><span data-stu-id="6c2c8-309">IPsec</span></span>
* <span data-ttu-id="6c2c8-310">AutoIP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-310">AutoIP</span></span>
* <span data-ttu-id="6c2c8-311">DHCP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-311">DHCP</span></span>
* <span data-ttu-id="6c2c8-312">DNS</span><span class="sxs-lookup"><span data-stu-id="6c2c8-312">DNS</span></span>
* <span data-ttu-id="6c2c8-313">Mdns</span><span class="sxs-lookup"><span data-stu-id="6c2c8-313">mDNS</span></span>
* <span data-ttu-id="6c2c8-314">DNS-SD</span><span class="sxs-lookup"><span data-stu-id="6c2c8-314">DNS-SD</span></span>
* <span data-ttu-id="6c2c8-315">FTP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-315">FTP</span></span>
* <span data-ttu-id="6c2c8-316">HTTP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-316">HTTP</span></span>
* <span data-ttu-id="6c2c8-317">IPsec</span><span class="sxs-lookup"><span data-stu-id="6c2c8-317">IPsec</span></span>
* <span data-ttu-id="6c2c8-318">NAT</span><span class="sxs-lookup"><span data-stu-id="6c2c8-318">NAT</span></span>
* <span data-ttu-id="6c2c8-319">POP3</span><span class="sxs-lookup"><span data-stu-id="6c2c8-319">POP3</span></span>
* <span data-ttu-id="6c2c8-320">Ppp</span><span class="sxs-lookup"><span data-stu-id="6c2c8-320">PPP</span></span>
* <span data-ttu-id="6c2c8-321">Pppoe</span><span class="sxs-lookup"><span data-stu-id="6c2c8-321">PPPoE</span></span>
* <span data-ttu-id="6c2c8-322">SMTP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-322">SMTP</span></span>
* <span data-ttu-id="6c2c8-323">SNMP v1/2/3</span><span class="sxs-lookup"><span data-stu-id="6c2c8-323">SNMP v1/2/3</span></span>
* <span data-ttu-id="6c2c8-324">Telnet</span><span class="sxs-lookup"><span data-stu-id="6c2c8-324">Telnet</span></span>
* <span data-ttu-id="6c2c8-325">TFTP</span><span class="sxs-lookup"><span data-stu-id="6c2c8-325">TFTP</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="6c2c8-326">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="6c2c8-326">Advanced technology</span></span>

<span data-ttu-id="6c2c8-327">Azure RTOS NetX Duo è una tecnologia avanzata che include quanto segue.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-327">Azure RTOS NetX Duo is advanced technology that includes the following.</span></span>

* <span data-ttu-id="6c2c8-328">Architettura di Piconet™</span><span class="sxs-lookup"><span data-stu-id="6c2c8-328">Piconet™ architecture</span></span>
* <span data-ttu-id="6c2c8-329">Scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="6c2c8-329">Automatic scaling</span></span>
* <span data-ttu-id="6c2c8-330">Tecnologia Fast-Path UDP™</span><span class="sxs-lookup"><span data-stu-id="6c2c8-330">UDP Fast-Path Technology™</span></span>
* <span data-ttu-id="6c2c8-331">Gestione flessibile dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="6c2c8-331">Flexible packet management</span></span>
* <span data-ttu-id="6c2c8-332">API e implementazione in copia zero</span><span class="sxs-lookup"><span data-stu-id="6c2c8-332">Zero-copy API and implementation</span></span>
* <span data-ttu-id="6c2c8-333">Supporto multihomed</span><span class="sxs-lookup"><span data-stu-id="6c2c8-333">Multihomed support</span></span>
* <span data-ttu-id="6c2c8-334">Timeout facoltativo per tutte le sospensioni</span><span class="sxs-lookup"><span data-stu-id="6c2c8-334">Optional timeout on all suspension</span></span>
* <span data-ttu-id="6c2c8-335">Supporto del routing statico</span><span class="sxs-lookup"><span data-stu-id="6c2c8-335">Static routing support</span></span>
* <span data-ttu-id="6c2c8-336">IPsec</span><span class="sxs-lookup"><span data-stu-id="6c2c8-336">IPsec</span></span>
* <span data-ttu-id="6c2c8-337">SSL/TLS/DTLS</span><span class="sxs-lookup"><span data-stu-id="6c2c8-337">SSL/TLS/DTLS</span></span>
* <span data-ttu-id="6c2c8-338">Azure RTOS di analisi del sistema TraceX</span><span class="sxs-lookup"><span data-stu-id="6c2c8-338">Azure RTOS TraceX system analysis support</span></span>

## <a name="related-services"></a><span data-ttu-id="6c2c8-339">Servizi correlati</span><span class="sxs-lookup"><span data-stu-id="6c2c8-339">Related services</span></span>

<span data-ttu-id="6c2c8-340">NetX Duo offre i servizi aggiuntivi seguenti.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-340">NetX Duo provides the following additional services.</span></span>

* <span data-ttu-id="6c2c8-341">Azure IoT Middleware</span><span class="sxs-lookup"><span data-stu-id="6c2c8-341">Azure IoT Middleware</span></span>
* <span data-ttu-id="6c2c8-342">Azure Defender</span><span class="sxs-lookup"><span data-stu-id="6c2c8-342">Azure Defender</span></span>
* <span data-ttu-id="6c2c8-343">Aggiornamento del dispositivo per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-343">Device update for IoT Hub.</span></span>

### <a name="azure-iot-middleware"></a><span data-ttu-id="6c2c8-344">Azure IoT Middleware</span><span class="sxs-lookup"><span data-stu-id="6c2c8-344">Azure IoT Middleware</span></span>

<span data-ttu-id="6c2c8-345">NetX Duo include [Azure IoT Middleware](https://github.com/azure-rtos/netxduo/blob/master/addons/azure_iot/docs/README.md)per Azure RTOS , una libreria specifica della piattaforma che funge da livello di associazione tra Azure RTOS e Azure SDK per Embedded C per facilitare la connettività ai servizi Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-345">NetX Duo includes [Azure IoT Middleware for Azure RTOS](https://github.com/azure-rtos/netxduo/blob/master/addons/azure_iot/docs/README.md), a platform-specific library that acts as a binding layer between the Azure RTOS and the Azure SDK for Embedded C to facilitate connectivity to Azure IoT services.</span></span> <span data-ttu-id="6c2c8-346">Gli obiettivi del Azure IoT middleware sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-346">The goals of Azure IoT Middleware are the following.</span></span>
* <span data-ttu-id="6c2c8-347">Fornire le interfacce client intelligenti (IoTHub_Client, DeviceProvisioning_Client) necessarie agli sviluppatori per le proprie applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-347">Provide the smart client interfaces (IoTHub_Client, DeviceProvisioning_Client) that developers need for their applications.</span></span>
* <span data-ttu-id="6c2c8-348">Orchestrare l'interazione tra Embedded C SDK e la piattaforma.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-348">Orchestrate the interaction between the Embedded C SDK and the platform.</span></span>
* <span data-ttu-id="6c2c8-349">Specificare Azure RTOS'inizializzazione della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-349">Provide Azure RTOS platform initialization.</span></span>
* <span data-ttu-id="6c2c8-350">IoT Plug and Play supporto.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-350">IoT Plug and Play support.</span></span>
* <span data-ttu-id="6c2c8-351">Funzionalità di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-351">Security capabilities.</span></span>
* <span data-ttu-id="6c2c8-352">Limitazione delle risorse in grado di riconoscere.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-352">Resource limitation aware.</span></span>
* <span data-ttu-id="6c2c8-353">Supporto del protocollo.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-353">Protocol support.</span></span>

![Azure RTOS servizi correlati a NetX Duo](./media/overview-netx-duo/related-services.png)

### <a name="azure-defender"></a><span data-ttu-id="6c2c8-355">Azure Defender</span><span class="sxs-lookup"><span data-stu-id="6c2c8-355">Azure Defender</span></span>

<span data-ttu-id="6c2c8-356">Il Azure Defender per IoT di sicurezza fornisce una soluzione di sicurezza completa per Azure RTOS dispositivi.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-356">The Azure Defender for IoT security module provides a comprehensive security solution for Azure RTOS devices.</span></span> <span data-ttu-id="6c2c8-357">Il modulo di sicurezza per Azure RTOS rilevamento delle attività di rete dannose, la base del comportamento dei dispositivi basata su avvisi personalizzati e contribuisce a migliorare l'pulizia della sicurezza dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-357">The Security Module for Azure RTOS offers malicious network activity detection, custom alert based device behavior baselining, and helps improve device security hygiene.</span></span> <span data-ttu-id="6c2c8-358">Altre informazioni sul modulo [di sicurezza per Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) guida introduttiva alla configurazione del modulo Azure RTOS sicurezza. [](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-358">Learn more about the [Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) or get started with the [Configure Security Module for Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) quickstart.</span></span>

### <a name="device-update-for-iot-hub"></a><span data-ttu-id="6c2c8-359">Aggiornamento dei dispositivi per l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="6c2c8-359">Device Update for IoT Hub</span></span>

<span data-ttu-id="6c2c8-360">Aggiornamento dei dispositivi di Azure per [l'hub IoT](https://docs.microsoft.com/azure/iot-hub-device-update/understand-device-update) è un servizio che consente di distribuire aggiornamenti over-the-air (OTA) per i dispositivi IoT.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-360">The [Azure Device Update for IoT Hub](https://docs.microsoft.com/azure/iot-hub-device-update/understand-device-update) is a service that enables you to deploy over-the-air updates (OTA) for your IoT devices.</span></span> <span data-ttu-id="6c2c8-361">Il modulo Device Update for IoT Hub è l'implementazione di Device Update for IoT Hub Agent in Azure RTOS NetX Duo.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-361">The Device Update for IoT Hub module is the implementation of Device Update for IoT Hub Agent in Azure RTOS NetX Duo.</span></span> <span data-ttu-id="6c2c8-362">Fornisce API semplici per i generatori di dispositivi per integrare la funzionalità Aggiornamento dispositivi nella propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-362">It provides simple APIs for device builders to integrate the Device Update capability in their application.</span></span>

<span data-ttu-id="6c2c8-363">Vedere gli esempi di schede di valutazione dei semiconduttori chiave che includono le guide introduttive per informazioni su come configurare, compilare e distribuire gli aggiornamenti over-the-air (OTA) nei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="6c2c8-363">See the samples of key semiconductors evaluation boards that include the get started guides to learn configure, build and deploy the over-the-air (OTA) updates to the devices.</span></span>

<span data-ttu-id="6c2c8-364">Altre informazioni sull'uso di Aggiornamento dispositivi per [l'hub IoT con Azure RTOS](https://docs.microsoft.com/azure/iot-hub-device-update/device-update-azure-real-time-operating-system).</span><span class="sxs-lookup"><span data-stu-id="6c2c8-364">And you can learn more details about use [Device Update for IoT Hub with Azure RTOS](https://docs.microsoft.com/azure/iot-hub-device-update/device-update-azure-real-time-operating-system).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c2c8-365">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c2c8-365">Next steps</span></span>

<span data-ttu-id="6c2c8-366">Per altre informazioni su NetX Duo, iniziare con la guida [Azure RTOS'utente di NetX Duo.](about-this-guide.md)</span><span class="sxs-lookup"><span data-stu-id="6c2c8-366">To learn more about NetX Duo, start with the [Azure RTOS NetX Duo User Guide](about-this-guide.md).</span></span>
