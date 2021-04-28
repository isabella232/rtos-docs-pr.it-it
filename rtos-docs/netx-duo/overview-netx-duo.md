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
# <a name="overview-of-azure-rtos-netx-duo"></a>Panoramica di Azure RTOS NetX Duo

Azure RTOS stack di rete TCP/IP incorporato di NetX Duo è lo stack di rete TCP/IP avanzato di livello industriale di Microsoft, dual IPv4 e IPv6, progettato specificamente per applicazioni IoT, in tempo reale e con incorporamento avanzato. NetX Duo offre applicazioni incorporate con protocolli di rete di base come IPv4, IPv6, TCP e UDP, nonché una suite completa di protocolli aggiuntivi aggiuntivi di livello superiore. Azure RTOS NetX Duo offre sicurezza tramite altri prodotti di sicurezza aggiuntivi, tra cui Azure RTOS NetX Secure IPsec e Azure RTOS NetX Secure SSL/TLS/DTLS. Il tutto combinato con un footprint ridotto, un'esecuzione rapida e una maggiore facilità d'uso rendono Azure RTOS NetX Duo la scelta ideale per le applicazioni IoT incorporate più complesse.

## <a name="api-protocols"></a>Protocolli API

### <a name="mqtt"></a>MQTT

* Trasporto dei dati di telemetria della coda di messaggistica (MQTT)
* MEMORIA FLASH minima di 2,7 KB

### <a name="auto-ip"></a>IP automatico

* Assegnazione automatica di indirizzi IPv4
* Minimo 1,2 KB, 300 byte di RAM

### <a name="http-https"></a>HTTP, HTTPS

#### <a name="http-10"></a>HTTP 1.0

* Hypertext Transfer Protocol(HTTP)
* Memoria FLASH minima da 2,8 KB a 4,8 KB/ da 0,4 KB a 1,0 KB di RAM
* Supporto client e server

#### <a name="httphttps-11"></a>HTTP/HTTPS 1.1

* Hypertext Transfer Protocol(HTTP)
* Memoria FLASH minima da 3,0 KB a 9,5 KB/ da 0,5 KB a 2 KB di RAM
* Supporto client e server
* Più sessioni client in ingresso
* Testo normale e HTTPS crittografato
* Supporto delle connessioni permanenti
* Caricamento di file multipart
* Completamente integrato con Azure RTOS NetX Secure TLS

### <a name="smtp"></a>SMTP

* Simple Mall Transfer Protocol (SMTP)
* Footprint minimo di 4,1 KB e 0,6 KB di RAM
* Supporto client

### <a name="dhcp"></a>DHCP

* Dynamic Host Configuration Protocol (DHCP)
* Footprint minimo da 3,6 KB a 4,6 KB FLASH, 2,7 KB di RAM
* Supporto client e server
* Supporto per IPv4 e IPv6

### <a name="nat"></a>NAT

* Network Address Translation (NAT)
* Footprint minimo di 3,5 K6 e 0,6 KB di RAM
* Supporto degli indirizzi IPv4
* NAT è disponibile solo con Azure RTOS NetX Duo

### <a name="snmp"></a>SNMP

* Simple Network Management Protocol (SNMP)
* Footprint minimo di 10,9 KB e 2,6 KB di RAM
* Supporto dell'agente per VI, V2 e V3

### <a name="dns-mdns-dns-sd"></a>DNS, mDNS, DNS-SD

* Domain Name System (DNS)
* Multicast Domain Name System (mDNS)
* Individuazione dei servizi basati su DNS (DNS-SD)
* DNS minimo da 2,4 KB a 3 KB FLASH, footprint ram da 1 KB
* Supporto client
* mDNS e DNS-SD sono disponibili solo con Azure RTOS NetX Duo

### <a name="p0p3"></a>P0P3

* Post Office Protocol versione 3 (POP3)
* Footprint minimo di 8,1 KB e 1,4 KB di RAM
* Supporto client

### <a name="telnet"></a>Telnet

* Footprint minimo di 0,5 KB e 0,3 KB di RAM
* Supporto client e server
* API Telnet intuitive: *nx_telnet_ \**

### <a name="ftp-tftp"></a>FTP, TFTP

* File Transfer Protocol (FTP)
* Trivial File Transfer Protocol (TFTP)
* FTP minimo da 1,8 KB a 7,2 KB FLASH, footprint di RAM da 0,6 a 2,1 KB
* Memoria flash TFTP minima da 1,7 KB a 2,4 KB, footprint di RAM da 0,3 a 1,8 KB
* Supporto client e server
* API FTP e TFTP *intuitive: \** nx_ftp_ o *\* nx_tftp_*

### <a name="ppp-pppoe"></a>PPP, PPPoE

* Protocollo PPP (Polnt-to-PoInt)
* Point-to-Point Protocol over Ethernet(PPPoE)
* Footprint minimo di 7,1 KB e 3,8 KB di RAM
* API PPP intuitive: *nx_ppp_ \**

* PPPoE è disponibile solo con Azure RTOS NetX Duo

### <a name="sntp"></a>SNTP

* Simple Network Time Protocol (SNTP)
* Minimo 4 KB e 0,5 KB di RAM
* Supporto client
* API SNTP intuitive: *nx_sntp_ \**

### <a name="azure-rtos-netx-duo-api"></a>Azure RTOS NetX Duo API

* API intuitiva e coerente
* Convenzione di denominazione sostantivo-verbo
* Implementazione rapida dell'API a copia zero
* Tutte le API hanno <i>nx_* per</i> identificarsi facilmente come Azure RTOS NetX
* Le API di blocco hanno un timeout del thread facoltativo
* Vedere [Azure RTOS per l'utente di NetX Duo](about-this-guide.md) per altri dettagli
* Livello BSD facoltativo per la portabilità del codice socket legacy

### <a name="igmp"></a>Igmp

* IGMP (Internet Group Management Protocol)
* Flash minimo da 2,5 KB
* Supporto dei gruppi multicast IPv4
* IXIA IxANVL convalidato
* Statistiche IGMP facoltative
* Traccia a livello di sistema tramite Azure RTOS ThreadX
* API IGMP intuitive: *nx_igmp_ \**

### <a name="azure-rtos-netx-secure-dtls"></a>Azure RTOS NetX Secure DTLS

* Datagram Transport Layer Security (DTLS) 1.0 e 1.2
* MEMORIA FLASH minima di 11 KB
* Chiave RSA a 2048 bit veloce e software di dimensioni ~1 secondo @120MHz
* Implementazione semplificata di X.509
* Completamente integrato con i Azure RTOS UDP di NetX Duo
* Supporto della crittografia hardware
* Supporto della crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)
* Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse le curve P 192/224/256/384/521
* Supporto delle chiavi crittografate (dipendente dall'hardware)

### <a name="azure-rtos-netx-secure-tls"></a>Azure RTOS NetX Secure TLS

* Transport Layer Security (TLS) 1.0, 1.1 e 1.2
* MEMORIA FLASH minima di 8,8 KB
* Chiave RSA a 2048 bit veloce e software di dimensioni ~1 secondo @120MHz
* Implementazione semplificata di X.509
* Completamente integrato con Azure RTOS TCP NetX Duo
* Supporto della crittografia hardware
* Supporto della crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)
* Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse le curve P 192/224/256/384/521
* Supporto delle chiavi crittografate (dipendente dall'hardware)

### <a name="icmp"></a>ICMP

* Internet Control Message Protocol (ICMP)
* Flash minimo da 2,5 KB
* Supporto per IPv4 e IPv6
* IXIA IxANVL convalidato
* Richiesta ping e risposta ping
* Sospensione facoltativa dei thread nelle richieste ping
* Timeout facoltativo per tutte le sospensioni
* Statistiche ICMP facoltative
* Traccia a livello di sistema tramite Azure RTOS TraceX
* API ICMP intuitive: *nx_icmp_ \**

### <a name="udp"></a>UDP

* Udp (User Datagram Protocol)
* MINIMO FLASH da 2,5 KB, 124 socket di RAM per socket
* Elaborazione rapida dei pacchetti TCP in prossimità di wirespeed:
    * RX 95 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 14%
    * TX 94 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 10%
* Tecnologia udp Fast Path™
* Nessun limite al numero di UDP
* IXIA IxANVL convalidato
* Sospensione facoltativa alla ricezione del socket
* Timeout facoltativo per tutte le sospensioni
* Statistiche UDP facoltative
* Traccia a livello di sistema tramite Azure RTOS TraceX
* API UDP intuitive: *nx_udp_ \**

### <a name="tcp"></a>TCP

* Transmission Control Protocol (TCP)
* Memoria flash minima da 10,5K8 a 12,5 KB, 280 byte di RAM per socket
* Elaborazione rapida dei pacchetti TCP da vicino:
    * RX 93 Mbps su Ethernet a 100 Mbps, @100MHz MCU, utilizzo MCU del 20%
    * TX 94 Mbps su Ethernet a 100 Mbps, @100MHz MCU, utilizzo MCU del 27%
* Connessione affidabile
* Nessun limite al numero di socket TCP
* IXIA IxANVL convalidato
* Sospensione facoltativa su ricezione/trasmissione socket
* Timeout facoltativo per tutte le sospensioni
* Statistiche TCP facoltative
* Traccia a livello di sistema tramite Azure RTOS TraceX
* API TCP intuitive: *nx_tcp_ \**

### <a name="arprarp"></a>ARP/RARP

* ARP (Address Resolution Protocol)
* RaRP (Reverse Address Resolution Protocol)
* Minimo 1,7 KB FLASH, dimensioni della RAM
* Risoluzione dinamica di indirizzi MAC da 32 blt IPv4 e 48 blt
* IXIA IxANVL convalidato
* Cache ARP flessibile e definita dall'utente
* Supporto gratuito ARP
* Statistiche ARP/RARP facoltative determinate dall'applicazione
* Traccia a livello di sistema tramite Azure RTOS TraceX
* API ARP/RARP intuitive: *nx_arp_ \**, *nx_rarp_ \**

### <a name="ipv4-amp-ipv6"></a>IPv4 &amp; IPv6

* Ip (Internet Protocol)
* Footprint minimo da 3,5 KB a 8,5 KB FLASH, da 2 KB a 3 KB di RAM
* Architettura di Piconet™
* Prestazioni veloci e near wirespeed
* Supporto di più interfacce
* Supporto multihomed
* Supporto del routing statico
* Supporto della frammentazione/riassemblaggio IP
* Supporto degli indirizzi IPv4 e IPv6
* IXIA IxANVL convalidato
* Certificazione del logo pronto per IPv6 fase II
* Statistiche IP facoltative
* Interfaccia del driver di livello fisico ben definita e intuitiva
* Traccia a livello di sistema tramite Azure RTOS TraceX
* API intuitive del livello IP: *\* nx_ip_*, *nxd_ip_ \** *\** , nxd_ipv6_
* Precertificato da TUV e UL a IEC 61508 SIL 4, IEC 62304 Classe C, ISO 26262 ASIL D e EN 50128 SW-SIL4

### <a name="azure-rtos-netx-secure-ipsec"></a>Azure RTOS IPSEC sicuro di NetX

* IPSEC (Internet Protocol Security)
* Livello IP
* Supporto della crittografia hardware
* Supporto della crittografia software, tra cui:
    * DES, 3DES
    * AES
    * HMAC-MD5
    * HMAC-SHA1
* Internet Key Exchange (IKE) versione 2
* API IPsec intuitive: *nx_ipsec_ \**
* IPsec è disponibile solo con Azure RTOS NetX Duo

## <a name="safe-and-secure"></a>Sicurezza e sicurezza

Azure RTOS NetX Duo è sicuro. Questa sicurezza viene fornita tramite prodotti di sicurezza aggiuntivi, tra cui IPsec, SSL, TLS e DTLS. Inoltre, l'applicazione ha il controllo completo su tutti gli accessi esterni Azure RTOS NetX Duo, rendendo molto più semplice la determinazione dei rischi di sicurezza.

Microsoft Azure RTOS fornisce agli OEM componenti per proteggere la comunicazione e creare codice e isolamento dei dati usando meccanismi di protezione hardware MCU/MPU sottostanti. È in definitiva responsabilità del generatore di dispositivi garantire che il dispositivo soddisfi pienamente i requisiti di sicurezza in evoluzione associati al caso d'uso specifico.


## <a name="interoperability-verification"></a>Verifica dell'interoperabilità

NetX Duo è conforme agli standard RFC e offre interoperabilità completa con i dispositivi per la maggior parte dei fornitori.

![Logo pronto per IPv6](./media/overview-netx-duo/ipv6-ready-logo.png)

Azure RTOS NetX Duo è uno degli unici stack TCP/IP incorporati per ottenere la rigorosa certificazione del logo IPv6-Ready, dimostrando di aver superato i test di conformità e interoperabilità, amministrati e convalidati dal forum IPv6. NetX Duo usa anche lo standard di settore IxANVL (Automated Network Validation Library) per l'implementazione del protocollo TCP/IP core di NetX Duo.

## <a name="comprehensive-iot-solution"></a>Soluzione IoT completa

NetX Duo offre una delle reti TCP/IP più complete per applicazioni IoT con un'incorporata approfondita. Questo supporto include i prodotti del protocollo aggiuntivo seguenti.

MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPsec, AutoIP, DHCP, DNS, mDNS, DNS-SD, FTP, HTTP, IPsec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP

## <a name="advanced-technology"></a>Tecnologia avanzata

Azure RTOS NetX Duo è una tecnologia avanzata che include:

* Architettura di Piconet™
* Scalabilità automatica
* Tecnologia Fast-Path UDP™
* Gestione flessibile dei pacchetti
* API e implementazione in copia zero
* Supporto multihomed
* Timeout facoltativo per tutte le sospensioni
* Supporto del routing statico
* IPsec
* SSL/TLS/DTLS
* Azure RTOS di analisi del sistema TraceX

## <a name="related-services"></a>Servizi correlati

Il Centro sicurezza di Azure per la sicurezza RTOS IoT offre una soluzione di sicurezza completa per Azure RTOS dispositivi. Il modulo di sicurezza per Azure RTOS rilevamento di attività di rete dannose, la base del comportamento dei dispositivi basato su avvisi personalizzati e contribuisce a migliorare la protezione della sicurezza dei dispositivi. Altre informazioni sul modulo [di sicurezza per Azure RTOS](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) [](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) guida introduttiva alla configurazione del modulo Azure RTOS sicurezza.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su NetX Duo, iniziare con il manuale [Azure RTOS'utente di NetX Duo.](about-this-guide.md)
