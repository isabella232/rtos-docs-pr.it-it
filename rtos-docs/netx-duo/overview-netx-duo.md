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
# <a name="overview-of-azure-rtos-netx-duo"></a>Panoramica di Azure RTO NetX Duo

Lo stack di rete TCP/IP di Azure RTO NetX Duo Embedded è uno stack di rete TCP/IP avanzato e di livello industriale di Microsoft, progettato in modo specifico per applicazioni molto incorporate e in tempo reale. NetX Duo fornisce applicazioni incorporate con protocolli di rete principali, ad esempio IPv4, IPv6, TCP e UDP, oltre a una suite completa di altri protocolli aggiuntivi di livello superiore. Azure RTO NetX Duo offre sicurezza tramite altri prodotti per la sicurezza aggiuntivi, tra cui Azure RTO NetX Secure IPsec e Azure RTO NetX secure SSL/TLS/DTLS. Tutti questi combinati con un footprint ridotto, un'esecuzione rapida e una semplicità di utilizzo superiore rendono Azure RTO NetX Duo la scelta ideale per le applicazioni di Internet delle cose incorporate più complesse.

## <a name="api-protocols"></a>Protocolli API

### <a name="mqtt"></a>MQTT

* Trasporto di telemetria della coda di messaggistica (MQTT)
* FLASH minimo 2,7 KB
* API MQTT intuitive: *nx_mqtt_*\*

### <a name="auto-ip"></a>IP automatico

* Assegnazione automatica di indirizzi IPv4
* Minimo 1,2 KB, 300 byte di RAM
* API AutoIP intuitive *: \* nx_autoip_*

### <a name="http-https"></a>HTTP, HTTPS

#### <a name="http-10"></a>HTTP 1,0

* Hypertext Transfer Protocol (HTTP)
* Minimo 2,8 KB a 4,8 KB FLASH/0,4 KB a 1,0 KB di RAM
* Supporto per client e server
* API intuitive *: \* nx_http_*

#### <a name="httphttps-11"></a>HTTP/HTTPS 1,1

* Hypertext Transfer Protocol (HTTP)
* Minimo 3,0 KB a 9,5 KB FLASH/0,5 KB a 2 KB di RAM
* Supporto per client e server
* Più sessioni client in ingresso
* Testo normale e HTTPS crittografato
* Supporto per connessioni permanenti
* Caricamento file multipart
* Completamente integrato con Azure RTO NetX Secure TLS
* API intuitive *: \* nx_web_http*

### <a name="smtp"></a>SMTP

* Simple Mall Transfer Protocol (SMTP)
* Ingombro minimo 4,1 KB e 0,6 KB di RAM
* Supporto client
* API SMTP intuitive *: \* nx_smtp_*

### <a name="dhcp"></a>DHCP

* Dynamic Host Configuration Protocol (DHCP)
* Minimo 3,6 KB a 4,6 KB FLASH, 2,7 KB di impronta RAM
* Supporto per client e server
* Supporto per IPv4 e IPv6
* API DHCP intuitive *: \* nx_dhcp_*

### <a name="nat"></a>NAT

* Network Address Translation (NAT)
* Ingombro minimo 3.5 K6 e 0,6 KB di RAM
* Supporto degli indirizzi IPv4
* API NAT intuitive *: \* nx_nat_*
* NAT è disponibile solo con Azure RTO NetX Duo

### <a name="snmp"></a>SNMP

* Simple Network Management Protocol (SNMP)
* Ingombro minimo 10,9 KB e 2,6 KB di RAM
* Supporto degli agenti per VI, V2 e V3
* API SNMP intuitive *: \* nx_snmp_*

### <a name="dns-mdns-dns-sd"></a>DNS, MDN, DNS-SD

* Domain Name System (DNS)
* Domain Name System multicast (MDN)
* Individuazione del servizio basato su DNS (DNS-SD)
* DNS minimo 2,4 KB a 3 KB di FLASH, 1 KB di impronta RAM
* Supporto client
* API intuitive *: \* nx_dns_*
* MDN e DNS-SD sono disponibili solo con Azure RTO NetX Duo

### <a name="p0p3"></a>P0P3

* Post Office Protocol versione 3 (POP3)
* Ingombro minimo 8,1 KB e 1,4 KB di RAM
* Supporto client
* API P0P3 intuitive *: \* nx_pop3_*

### <a name="telnet"></a>TELNET

* Ingombro minimo 0,5 KB e 0,3 KB di RAM
* Supporto per client e server
* API Telnet intuitive *: \* nx_telnet_*

### <a name="ftp-tftp"></a>FTP, TFTP

* File Transfer Protocol (FTP)
* Trivial File Transfer Protocol (TFTP)
* FTP minimo 1,8 KB a 7,2 KB FLASH, da 0,6 KB a 2,1 KB di impronta RAM
* TFTP minimo 1,7 KB a 2,4 KB FLASH, 0,3 KB a 1,8 KB di RAM footprint
* Supporto per client e server
* API FTP e TFTP intuitive *: \* nx_ftp_* o *nx_tftp_ \**

### <a name="ppp-pppoe"></a>PPP, PPPoE

* Protocollo bravo-to-PoInt (PPP)
* Point-to-Point Protocol su Ethernet (PPPoE)
* Ingombro minimo 7,1 KB e 3,8 KB di RAM
* API PPP intuitive *: \* nx_ppp_*

* PPPoE è disponibile solo con Azure RTO NetX Duo

### <a name="sntp"></a>SNTP

* Simple Network Time Protocol (SNTP)
* Minimo 4 KB e 0,5 KB di RAM
* Supporto client
* API SNTP intuitive *: \* nx_sntp_*

### <a name="azure-rtos-netx-duo-api"></a>API di Azure RTO NetX Duo

* API intuitiva e coerente
* Sostantivo-convenzione di denominazione dei verbi
* Implementazione API veloce, copia zero
* Tutte le API hanno <i>nx_ *</i> per identificare facilmente come Azure RTO NETX
* Le API di blocco hanno un timeout thread facoltativo
* Per altri dettagli, vedere la [Guida dell'utente di Azure RTO NETX Duo](about-this-guide.md)
* Livello BSD facoltativo per il porting del codice socket legacy

### <a name="igmp"></a>IGMP

* IGMP (Internet Group Management Protocol)
* FLASH minimo 2,5 KB
* Supporto del gruppo multicast IPv4
* IxANVL di IXIA convalidati
* Statistiche IGMP facoltative
* Traccia a livello di sistema tramite Azure RTO ThreadX
* API IGMP intuitive *: \* nx_igmp_*

### <a name="azure-rtos-netx-secure-dtls"></a>Azure RTO NetX Secure DTLS

* Datagramma Transport Layer Security (DTLS) 1,0 e 1,2
* FLASH minimo 11 KB
* Fast, software RSA 2048 bit key size ~ 1 secondo @120MHz
* Implementazione X. 509 semplificata
* Completamente integrato con i socket UDP di Azure RTO NetX Duo
* Supporto della crittografia hardware
* Supporto per la crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)
* Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse P-curve 192/224/256/384/521
* Supporto della chiave crittografata (dipendente dall'hardware)

### <a name="azure-rtos-netx-secure-tls"></a>Azure RTO NetX Secure TLS

* Transport Layer Security (TLS) 1,0, 1,1 e 1,2
* FLASH minimo 8,8 KB
* Fast, software RSA 2048 bit key size ~ 1 secondo @120MHz
* Implementazione X. 509 semplificata
* Completamente integrato con i socket TCP RTO NetX duo di Azure
* Supporto della crittografia hardware
* Supporto per la crittografia software: RSA (tutte le dimensioni delle chiavi), AES, DES/3DES, ECC, HMAC, MD5, SHA-1, SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512)
* Crittografia a curva ellittica (ECC) con ECDSA (firma) e ECDH (crittografia), incluse P-curve 192/224/256/384/521
* Supporto della chiave crittografata (dipendente dall'hardware)

### <a name="icmp"></a>ICMP

* Internet Control Message Protocol (ICMP)
* FLASH minimo 2,5 KB
* Supporto per IPv4 e IPv6
* IxANVL di IXIA convalidati
* Ping richiesta e risposta ping
* Sospensione thread facoltativa sulle richieste ping
* Timeout facoltativo per tutte le sospensioni
* Statistiche ICMP facoltative
* Traccia a livello di sistema tramite Azure RTO TraceX
* API ICMP intuitive *: \* nx_icmp_*

### <a name="udp"></a>UDP

* UDP (User Datagram Protocol)
* Minimo 2,5 KB di FLASH, 124 socket byte di RAM per socket
* Elaborazione di pacchetti TCP veloce, near wirespeed:
    * RX 95 Mbps su Ethernet a 100 Mbps, MCU @100MHz , 14% di utilizzo di MCU
    * TX 94 Mbps a 100 Mbps Ethernet, MCU @100MHz , 10% di utilizzo di MCU
* Percorso rapido UDP™ tecnologia
* Nessun limite al numero di UDP
* IxANVL di IXIA convalidati
* Sospensione facoltativa per ricezione socket
* Timeout facoltativo per tutte le sospensioni
* Statistiche UDP facoltative
* Traccia a livello di sistema tramite Azure RTO TraceX
* API UDP intuitive *: \* nx_udp_*

### <a name="tcp"></a>TCP

* Transmission Control Protocol (TCP)
* Minimo da 10.5 K8 a 12,5 KB di FLASH, 280 byte di RAM per socket
* Elaborazione di pacchetti TCP veloce, near wlrespeed:
    * RX 93 Mbps su Ethernet a 100 Mbps, MCU @100MHz , utilizzo di MCU del 20%
    * TX 94 Mbps su Ethernet a 100 Mbps, MCU @100MHz , utilizzo di MCU del 27%
* Connessione affidabile
* Nessun limite al numero di socket TCP
* IxANVL di IXIA convalidati
* Sospensione facoltativa per ricezione/trasmissione socket
* Timeout facoltativo per tutte le sospensioni
* Statistiche TCP facoltative
* Traccia a livello di sistema tramite Azure RTO TraceX
* API TCP intuitive *: \* nx_tcp_*

### <a name="arprarp"></a>ARP/RARP

* ARP (Address Resolution Protocol)
* Protocollo RARP (Reverse Address Resolution Protocol)
* Minimo 1,7 KB di memoria, dimensioni RAM
* Risoluzione dinamica degli indirizzi MAC 32-BLT IPv4 e 48-BLT
* IxANVL di IXIA convalidati
* Cache ARP flessibile definita dall'utente
* Supporto ARP gratuito
* Statistiche ARP/RARP facoltative determinate dall'applicazione
* Traccia a livello di sistema tramite Azure RTO TraceX
* API ARP/RARP intuitive *: \* nx_arp_*, *nx_rarp_ \**

### <a name="ipv4-amp-ipv6"></a>&amp;IPv6 IPv4

* Protocollo IP (Internet Protocol)
* Minimo 3,5 KB a 8,5 KB FLASH, da 2 KB a 3 KB di impronta RAM
* Architettura™ piconet
* Prestazioni veloci, near wirespeed
* Supporto di più interfacce
* Supporto multihomed
* Supporto del routing statico
* Supporto per la frammentazione e il riassemblaggio IP
* Supporto degli indirizzi IPv4 e IPv6
* IxANVL di IXIA convalidati
* Certificazione del logo pronto per la fase II IPv6
* Statistiche IP facoltative
* Interfaccia del driver del livello fisico intuitiva e ben definita
* Traccia a livello di sistema tramite Azure RTO TraceX
* API del livello IP intuitive: *\* nx_ip_*, *nxd_ip_ \**, *nxd_ipv6_ \**
* Pre-certificati da TUV e UL a IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D e EN 50128 SW-SIL4

### <a name="azure-rtos-netx-secure-ipsec"></a>IPSEC protetto da Azure RTO NetX

* IPSEC (Internet Protocol Security)
* Livello IP
* Supporto della crittografia hardware
* Supporto per la crittografia software, tra cui:
    * DES, 3DES
    * AES
    * HMAC-MD5
    * HMAC-SHA1
* Supporto di protocollo IKE (IKE) versione 2
* API IPsec intuitive *: \* nx_ipsec_*
* IPsec è disponibile solo con Azure RTO NetX Duo

## <a name="small-footprint"></a>Footprint ridotto

Azure RTO NetX Duo presenta un footprint notevolmente ridotto da 9 KB a 15 KB per il supporto di base per IP e UDP. Per la funzionalità TCP sono necessari altri 10 KB a 13 KB di memoria per l'area di istruzione. L'utilizzo della RAM di Azure RTO NetX Duo è generalmente compreso tra 2,6 KB e 3,6 KB oltre alla memoria del pool di pacchetti, definita dall'applicazione. Come Azure RTO ThreadX, le dimensioni di Azure RTO NetX Duo vengono ridimensionate automaticamente in base ai servizi usati dall'applicazione. In questo modo si eliminano praticamente la necessità di complicati parametri di configurazione e di compilazione, semplificando le operazioni per lo sviluppatore.

## <a name="fast-execution"></a>Esecuzione rapida

Azure RTO NetX Duo fornisce un'implementazione di invio/ricezione di pacchetti con copia zero, altamente integrata con Azure RTO ThreadX, per ottenere le prestazioni più rapide possibile. Ad esempio, Azure RTO NetX Duo può in genere ottenere trasferimenti di dati near wirespeed su un processore 80 MHz (o meno), usando solo una piccola percentuale dei cicli del processore.

## <a name="simple-easy-to-use"></a>Semplice e facile da usare

L'API di Azure RTO NetX Duo è intuitiva, semplice e altamente funzionale.

I nomi delle API sono costituiti da parole reali e non da "zuppa alfabetica" o nomi altamente abbreviati, così comuni in altri prodotti di rete. Tutte le API di Azure RTO NetX Duo hanno un *nx_* leader e seguono una convenzione di denominazione sostantivo-verbo. Inoltre, esiste una coerenza funzionale nell'API. Tutte le funzioni API che sospendono, ad esempio, hanno un timeout facoltativo che funziona in modo identico.

Per le applicazioni legacy, Azure RTO NetX Duo offre un ulteriore livello compatibile con socket BSD. Questo livello consente agli sviluppatori di eseguire facilmente la migrazione di applicazioni di rete di grandi dimensioni.

## <a name="safe-and-secure"></a>Sicuro e sicuro

Azure RTO NetX Duo è sicuro. Questa sicurezza viene fornita tramite i prodotti per la sicurezza dei componenti aggiuntivi, tra cui IPsec, SSL, TLS e DTLS. Inoltre, l'applicazione ha il controllo completo su tutti gli accessi esterni ad Azure RTO NetX Duo, rendendo molto più semplice la determinazione dei rischi per la sicurezza.

Microsoft Azure RTO fornisce agli OEM i componenti per proteggere le comunicazioni e creare codice e isolamento dei dati utilizzando meccanismi di protezione hardware MCU/MPU sottostanti. È in definitiva responsabilità del generatore di dispositivi verificare che il dispositivo soddisfi pienamente i requisiti di sicurezza in evoluzione associati al caso d'uso specifico.

## <a name="pre-certified--by-tuv-and-ul-to-many-safety-standards"></a>Pre-certificati da TUV e UL a molti standard di sicurezza

Azure RTO NetX Duo è stato certificato da SGS-TUV Saar per l'uso nei sistemi critici per la sicurezza, in base alla classe IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 ASIL D e EN 50128. La certificazione conferma che è possibile usare Azure RTO NetX Duo per lo sviluppo di software correlati alla sicurezza per i livelli di integrità di sicurezza più elevati di IEC-61508, IEC-62304, ISO 26262 e EN 50128 per la "protezione funzionale dei sistemi elettronici di sicurezza elettronica, elettronici e programmabili". SGS-TUV Saar, costituito da una joint venture del SGS-Group e del TUV del Regno Unito, è diventato la società leader accreditata e indipendente per il test, il controllo, la verifica e la certificazione del software incorporato per i sistemi correlati alla sicurezza in tutto il mondo. Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, tra cui IEC-62304, ISO 26262 e EN 50128, vengono usati per garantire la protezione funzionale di dispositivi medicali elettrici, elettronici e programmabili per la sicurezza elettronica, sistemi di controllo dei processi, macchinari industriali, automobili e sistemi di controllo ferroviario.

:::image type="content" source="media/overview-netx-duo/partener-logo-sgs-tuv-saar.png" alt-text="SGS-certificazione TUV":::

Azure RTO NetX Duo è stato riconosciuto da UL per conformità con UL 60730-1 allegato H, CSA E60730-1 allegato H, IEC 60730-1 allegato H, UL 60335-1 allegato R, IEC 60335-1 allegato R e UL 1998 sicurezza standard per il software in componenti programmabili. UL è una società globale, indipendente e scientifica per la sicurezza, con più di un secolo di competenze innovative per l'innovazione delle soluzioni di sicurezza, che vanno dall'adozione pubblica di energia elettrica ai progressi della sostenibilità, dell'energia rinnovabile e della nanotecnologia.

:::image type="content" source="media/overview-netx-duo/cru-logo-certification.png" alt-text="Certificazione CRU UL":::

Gli artefatti (certificato, manuale di sicurezza, report di test e così via) associati alle certificazioni TUV e UL sono disponibili per la vendita.

Nei casi in cui l'applicazione necessita di ulteriore certificazione, un servizio di certificazione è disponibile tramite Microsoft per fornire la certificazione chiavi in volta a diversi standard usando la piattaforma hardware effettiva e persino coprendo il codice dell'applicazione. Per ulteriori informazioni sul servizio di certificazione, contattare Microsoft.

## <a name="eal4-common-criteria-security-certification"></a>EAL4 + criteri comuni certificazione di sicurezza

Azure RTO ha raggiunto la certificazione di sicurezza EAL4 + Common Criteria. La destinazione di valutazione (TOE) copre Azure RTO ThreadX, Azure RTO NetX Duo, Azure RTO NetX Secure TLS e Azure RTO NETX MQTT. Questo rappresenta i protocolli più tipici necessari per i sensori, i dispositivi, i router perimetrali e i gateway con incorporate profondità.

:::image type="content" source="media/overview-netx-duo/eal-logo-certification.png" alt-text="Certificazione EAL":::

La funzionalità di valutazione della sicurezza IT utilizzata per la Microsoft Azure certificazione di sicurezza RTO SC è BrightSight BV e l'autorità di certificazione è SERTIT.

## <a name="fips-140-2-validated"></a>FIPS 140-2 convalidato

Le librerie di crittografia NetX di Azure RTO hanno avuto la certificazione Federal Information Processing Standard 140-2 (FIPS 140-2) per il software, che specifica i requisiti per i moduli di crittografia. FIPS 140-2 richiede che tutti gli enti governativi federali e i reparti che utilizzano la sicurezza basata su crittografia siano in grado di soddisfare standard specifici relativi alla forza e alle funzionalità di crittografia. Questi standard di sicurezza basati su crittografia sono riconosciuti anche in Canada e nell'Unione europea.

Il Lab di valutazione della sicurezza delle informazioni usato per le librerie di crittografia NetX di Azure RTO è atsec e l'autorità di certificazione è il National Institute of Standards and Technology (NIST). Per ulteriori informazioni, vedere il [sito Web del NIST](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3394) .

## <a name="interoperability-verification"></a>Verifica dell'interoperabilità

NetX Duo è conforme agli standard RFC e offre un'interoperabilità completa con i dispositivi per la maggior parte dei fornitori.

![Logo pronto per IPv6](./media/overview-netx-duo/ipv6-ready-logo.png)

Azure RTO NetX Duo è uno degli unici stack TCP/IP incorporati per ottenere la rigorosa certificazione del logo IPv6-Ready, prova che ha superato i test di conformità e interoperabilità, gestiti e convalidati dal forum di IPv6. NetX Duo usa anche il IxANVL (Automatic Network Validation Library) standard del settore per l'implementazione del protocollo TCP/IP di NetX Duo Core.

## <a name="comprehensive-iot-solution"></a>Soluzione completa

Azure RTO NetX Duo presenta un footprint notevolmente ridotto da 9 KB a 15 KB per il supporto di base per IP e UDP. NetX duo ha una delle reti TCP/IP più complete per le applicazioni per le cose estremamente incorporate. Questo supporto include i prodotti del protocollo aggiuntivo seguenti:

MQTT, CoAP, LWM2M, 6LoWPAN, SSL/TLS/DTLS, IPsec, AutoIP, DHCP, DNS, MDN, DNS-SD, FTP, HTTP, IPsec, NAT, POP3, PPP, PPPoE, SMTP, SNMP v1/2/3, Telnet, TFTP

## <a name="advanced-technology"></a>Tecnologia avanzata

Azure RTO NetX Duo è una tecnologia avanzata che include:

* Architettura™ piconet
* Scalabilità automatica
* Tecnologia Fast-Path UDP™
* Gestione flessibile dei pacchetti
* API di copia zero e implementazione
* Supporto multihomed
* Timeout facoltativo per tutte le sospensioni
* Supporto del routing statico
* IPsec
* SSL/TLS/DTLS
* Supporto per l'analisi del sistema TraceX di Azure RTO

## <a name="fastest-time-to-market"></a>Time-to-market più veloce

Azure RTO NetX Duo è facile da installare, apprendere, usare, eseguire il debug, verificare, certificare e gestire. Di conseguenza, NetX Duo è uno degli stack TCP/IP più diffusi per i dispositivi di Internet delle cose incorporate, inclusi molti SoC da Broadcom, GainSpan e così via. Il nostro vantaggio di time-to-Market coerente è basato su:

* Documentazione relativa alla qualità: esaminare la guida per l' [utente di Azure RTO NETX Duo](about-this-guide.md) e vedere per se stessi.
* Disponibilità del codice sorgente completa
* API di facile utilizzo
* Set di funzionalità completo e avanzato

## <a name="one-simple-license"></a>Una licenza semplice

Non è previsto alcun costo per l'uso e il test del codice sorgente e nessun costo per le licenze di produzione quando viene distribuito in dispositivi con licenza preliminare, tutti gli altri dispositivi necessitano di una licenza annuale semplice.

## <a name="full-highest-quality-source-code"></a>Codice sorgente completo di qualità elevata

Nel corso degli anni, il codice sorgente di Azure RTO NetX duo ha impostato la qualità e la facilità di comprensione. Inoltre, la convenzione relativa alla presenza di una funzione per ogni file fornisce una semplice navigazione all'origine.

## <a name="supports-most-popular-architectures"></a>Supporta le architetture più diffuse

Azure RTO NetX Duo viene eseguito sui microprocessori più diffusi a 32/64 bit predefiniti, completamente testato e completamente supportato, incluse le seguenti architetture avanzate:

**Dispositivi analoghi**: SHARC, Blackfin, CM4xx

**Andina Core**: RISC-V

**Ambiqmicro**: pollo MCU

**ARM**: RM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/a15/a5/A7/A8/A9/A5x 64-bi/A7X a 64 bit/R4/R5, TrustZone ARMv8-M

**Cadenza**: Xtensa, diamante

**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WICED WiFi

**Cypress**: RISC-V

**Silice**: ESI-RISC

**Infineon**: XMC1000, XMC4000, Tricore

**Intel & Intel FPGA**: x36/Pentium, XScale, Nios II, Cyclone, Arria 10

**Microchip**: avr32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32

**Microsemi**: RISC-V

**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4

**Renesas**: SH, HS, V850, RX, RZ, Synergy

**Silicone** Lab: EFM32

**Synopsys**: Arc 600, 700, Arc em, Arc HS

**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7

**TL**: C5xxx, C6xxx, Stellaris, Sitara, tiva-C

**Elaborazione Wave**: MIPS32 4K, 24 k, 34 k, 1004 k, MIPS64 5K, MicroAptiv, InterAptiv, ProAptiv, M-Class

**Xilinx**: Microblaze, PowerPC 405, ZYNQ, Zynq UltraSCALE

*Tutte le cifre relative a tempistiche e dimensioni elencate sono stime e possono essere diverse nella piattaforma di sviluppo.*

## <a name="related-services"></a>Servizi correlati

Il modulo di sicurezza del Centro sicurezza di Azure per RTO offre una soluzione di sicurezza completa per i dispositivi RTO di Azure. Il modulo di sicurezza per Azure RTO offre rilevamento di attività di rete dannose, linea di base del comportamento dei dispositivi basati su avvisi personalizzati e consente di migliorare l'igiene della sicurezza del dispositivo. Scopri di più sul [modulo di sicurezza per Azure RTO](https://docs.microsoft.com/azure/asc-for-iot/iot-security-azure-rtos) o inizia a usare la Guida introduttiva alla [configurazione del modulo di sicurezza per RTO di Azure](https://docs.microsoft.com/azure/asc-for-iot/quickstart-azure-rtos-security-module) .

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su NetX Duo, vedere il [manuale dell'utente di Azure RTO NETX Duo](about-this-guide.md).
