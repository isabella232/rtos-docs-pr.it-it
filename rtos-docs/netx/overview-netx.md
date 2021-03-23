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
# <a name="overview-of-azure-rtos-netx"></a>Panoramica di Azure RTO NetX

Azure RTO NetX è uno stack di rete incorporato TCP/IP IPv4 di livello industriale, progettato in modo specifico per applicazioni incorporate, in tempo reale e in tempo reale. Azure RTO NetX è lo stack di rete IPv4 originale di Microsoft ed è essenzialmente un subset di RTO di Azure. NetX fornisce applicazioni incorporate con protocolli di rete principali, ad esempio IPv4, TCP e UDP, nonché una suite completa di protocolli aggiuntivi di livello superiore. Un footprint ridotto, un'esecuzione rapida e una semplicità di utilizzo superiore rendono Azure RTO NetX la scelta ideale per le applicazioni di Internet delle cose più complesse.

## <a name="api-protocols"></a>Protocolli API

### <a name="telnet"></a>TELNET

* Ingombro minimo 0,5 KB e 0,3 KB di RAM
* Supporto per client e server
* API Telnet intuitive *: \* nx_telnet_*

### <a name="auto-ip"></a>IP automatico

* Assegnazione automatica di indirizzi IPv4
* Minimo 1,2 KB, 300 byte di RAM
* API AutoIP intuitive *: \* nx_autoip_*

### <a name="http---hypertext-transfer-protocolhttp"></a>HTTP-Hypertext Transfer Protocol (HTTP)

* Minimo 2,8 KB a 4.8 KBFLASH, da 0,4 KB a 1,0 KB di RAM
* Supporto per client e server
* API HTTP intuitive *: \* nx_http_*

### <a name="smtp---simple-mail-transfer-protocol-smtp"></a>SMTP-Simple Mail Transfer Protocol (SMTP)

* Ingombro minimo 4,1 KB e 0,6 KB di RAM
* Supporto client
* API SMTP intuitive *: \* nx_smtp_*

### <a name="dhcp---dynamic-host-configuration-protocol-dhcp"></a>DHCP-Dynamic Host Configuration Protocol (DHCP)

* Minimo 3,6 KB a 4,6 KB FLASH, 2,7 KB di impronta RAM
* Supporto per client e server
* Supporto per IPv4
* API DHCP intuitive *: \* nx_dhcp_*

### <a name="p0p3---post-office-protocol-version-3-pop3"></a>P0P3-Post Office Protocol versione 3 (POP3)

* Ingombro minimo 8,1 KB e 1,4 KB di RAM
* Supporto client
* API P0P3 intuitive *: \* nx_pop3_*

### <a name="snmp---simple-network-management-protocol-snmp"></a>SNMP-Simple Network Management Protocol (SNMP)

* Ingombro minimo 10,9 KB e 2,6 KB di RAM
* Supporto degli agenti per VI, V2 e V3
* API SNMP intuitive *: \* nx_snmp_*

### <a name="ftp-tftp---file-transfer-protocol-ftp-trivial-file-transfer-protocol-tftp"></a>FTP, TFTP-File Transfer Protocol (FTP), Trivial File Transfer Protocol (TFTP)

* FTP minimo 1,8 KB a 7,2 KBFLASH, da 0,6 KB a 2,1 KB di RAM
* TFTP minimo 1,7 KB a 2,4 KBFLASH, da 0,3 KB a 1,8 KB di RAM
* Supporto per client e server
* API FTP e TFTP intuitive: <i>nx_ftp_ *</i> o <i>nx_tftp_*</i>

### <a name="ppp---polnt-to-point-protocol-ppp"></a>PPP-bravo-to-PoInt Protocol (PPP)

* Ingombro minimo 7,1 KB e 3,8 KB di RAM
* API PPP intuitive *: \* nx_ppp_*

### <a name="sntp---simple-network-time-protocol-sntp"></a>SNTP-Simple Network Time Protocol (SNTP)

* Minimo 4 KB e 0,5 KB di RAM
* Supporto client
* API SNTP intuitive *: \* nx_sntp_*

### <a name="azure-rtos-netx-api"></a>API NetX di Azure RTO

* API intuitiva e coerente
* Sostantivo-convenzione di denominazione dei verbi
* Implementazione API veloce, copia zero
* Tutte le funzioni API hanno <i>nx_ *</i> per identificare facilmente come Azure RTO NETX
* Le funzioni API di blocco hanno un timeout thread facoltativo
* Livello BSD facoltativo per il porting del codice socket legacy

### <a name="igmp---internet-group-management-protocol-igmp"></a>IGMP (Internet Group Management Protocol)

* FLASH minimo 2,5 KB
* Supporto del gruppo multicast IPv4
* IxANVL di IXIA convalidati
* Statistiche IGMP facoltative
* Traccia a livello di sistema tramite Azure RTO TraceX
* API IGMP intuitive *: \* nx_igmp_*

### <a name="udp---user-datagram-protocol-udp"></a>UDP-User Datagram Protocol (UDP)

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

### <a name="tcp---transmission-control-protocol-tcp"></a>TCP-Transmission Control Protocol (TCP)

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

### <a name="icmp---internet-control-message-protocol-icmp"></a>ICMP-Internet Control Message Protocol (ICMP)

* FLASH minimo 2,5 KB
* Supporto per IPv4
* IxANVL di IXIA convalidati
* Ping richiesta e risposta ping
* Sospensione thread facoltativa sulle richieste ping
* Timeout facoltativo per tutte le sospensioni
* Statistiche ICMP facoltative
* Traccia a livello di sistema tramite Azure RTO TraceX
* API ICMP intuitive *: \* nx_icmp_*

### <a name="ipv4---internet-protocol-ip"></a>IPv4-Internet Protocol (IP)

* Minimo 3,5 KB a 8,5 KB FLASH, da 2 KB a 3 KB di impronta RAM
* Architettura™ piconet
* Prestazioni veloci, near wirespeed
* Supporto di più interfacce
* Supporto multihomed
* Supporto del routing statico
* Supporto per la frammentazione e il riassemblaggio IP
* Supporto per IPv4
* IxANVL di IXIA convalidati
* Certificazione del logo per la fase II pronta
* Statistiche IP facoltative
* Interfaccia del driver del livello fisico intuitiva e ben definita
* Traccia a livello di sistema tramite Azure RTO TraceX
* API del livello IP intuitive: *nx_ip_ \**, *nxd_ip_ \**
* Pre-certificati da TUV e UL a IEC 61508 SIL 4, IEC 62304 Class C, ISO 26262 ASIL D e EN 50128 SW-SIL4

### <a name="arprarp---address-resolution-protocol-arp-reverse-address-resolution-protocol-rarp"></a>ARP/RARP-Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP)

* Minimo 1,7 KB di memoria, dimensioni RAM
* Risoluzione dinamica degli indirizzi MAC 32-BLT IPv4 e 48-BLT
* IxANVL di IXIA convalidati
* Cache ARP flessibile definita dall'utente
* Supporto ARP gratuito
* Statistiche ARP/RARP facoltative determinate dall'applicazione
* Traccia a livello di sistema tramite Azure RTO TraceX
* API ARP/RARP intuitive *: \* nx_arp_*, *nx_rarp_ \**

### <a name="ethernet-wifi-bluetooth-le-154-etc"></a>ETHERNET, Wi-Fi, BLUETOOTH LE, 15,4 e così via.

## <a name="small-footprint"></a>Footprint ridotto

Azure RTO NetX ha un footprint notevolmente ridotto da 9 KB a 15 KB per il supporto IP e UDP di base. Per la funzionalità TCP sono necessari altri 10 KB a 13 KB di memoria per l'area di istruzione. L'utilizzo della RAM NetX di Azure RTO in genere varia da 2,6 KB a 3,6 KB oltre alla memoria del pool di pacchetti, definita dall'applicazione. Come Azure RTO ThreadX, le dimensioni di Azure RTO NetX vengono ridimensionate automaticamente in base ai servizi usati dall'applicazione. In questo modo si eliminano praticamente la necessità di complicati parametri di configurazione e di compilazione, semplificando le operazioni per lo sviluppatore.

## <a name="fast-execution"></a>Esecuzione rapida

Azure RTO NetX offre un'implementazione di invio/ricezione di pacchetti con copia zero ed è altamente integrato con Azure RTO ThreadX per ottenere le prestazioni più rapide possibile. Ad esempio, Azure RTO NetX può in genere ottenere trasferimenti di dati near wirespeed su un processore 80 MHz (o meno), usando solo una piccola percentuale dei cicli del processore.

## <a name="simple-easy-to-use"></a>Semplice e facile da usare

Azure RTO NetX è semplice da usare. L'API NetX di Azure RTO è intuitiva e altamente funzionale. I nomi delle API sono costituiti da parole reali e non da "zuppa alfabetica" o nomi altamente abbreviati, così comuni in altri prodotti di rete. Tutte le API NetX di Azure RTO hanno un *nx_* leader e seguono una convenzione di denominazione sostantivo-verbo. Inoltre, esiste una coerenza funzionale nell'API. Tutte le funzioni API che sospendono, ad esempio, hanno un timeout facoltativo che funziona in modo identico. Per le applicazioni legacy, Azure RTO NetX offre un ulteriore livello compatibile con socket BSD. Questo livello consente agli sviluppatori di eseguire facilmente la migrazione di applicazioni di rete di grandi dimensioni.

## <a name="interoperability-verification"></a>Verifica dell'interoperabilità

Azure RTO NetX è conforme agli standard RFC e offre un'interoperabilità completa con i dispositivi per la maggior parte dei fornitori. Azure RTO NetX usa anche lo standard di settore IxANVL (Automatic Network Validation Library) per l'implementazione del protocollo TCP/IP di Azure RTO NetX core.

## <a name="advanced-technology"></a>Tecnologia avanzata

Azure RTO NetX è una tecnologia avanzata che include:

* Architettura™ piconet
* ridimensionamento automatico
* Tecnologia Fast-Path UDP™
* gestione flessibile dei pacchetti
* API di copia zero e implementazione
* supporto multihomed
* timeout facoltativo per tutte le sospensioni
* supporto del routing statico
* Supporto per l'analisi del sistema TraceX di Azure RTO

## <a name="fastest-time-to-market"></a>Time-to-market più veloce

Azure RTO NetX è facile da installare, apprendere, usare, eseguire il debug, verificare, certificare e gestire. Di conseguenza, Azure RTO NetX è uno degli stack TCP/IP più diffusi per i dispositivi di Internet delle cose incorporate, inclusi molti SoC da Broadcom, GainSpan e così via. Il nostro vantaggio di time-to-Market coerente è basato su:

* documentazione sulla qualità: esaminare la [Guida dell'utente di Azure RTO NETX](about-this-guide.md) e vedere per se stessi.
* disponibilità del codice sorgente completa
* API di facile utilizzo
* set di funzionalità completo e avanzato

## <a name="one-simple-license"></a>Una licenza semplice

Non è previsto alcun costo per l'uso e il test del codice sorgente e nessun costo per le licenze di produzione quando viene distribuito in dispositivi con licenza preliminare, tutti gli altri dispositivi necessitano di una licenza annuale semplice.

## <a name="full-highest-quality-source-code"></a>Codice sorgente completo di qualità elevata

Nel corso degli anni, il codice sorgente NetX di Azure RTO ha impostato la qualità e la facilità di comprensione. Inoltre, la convenzione relativa alla presenza di una funzione per ogni file fornisce una semplice navigazione all'origine.

## <a name="supports-most-popular-architectures"></a>Supporta le architetture più diffuse

Azure RTO NetX viene eseguito sui microprocessori più diffusi a 32/64 bit, predefiniti, completamente testati e completamente supportati, incluse le seguenti architetture avanzate:

**Dispositivi analoghi**: SHARC, Blackfin, CM4xx

**Andina Core**: RISC-V

**Ambiqmicro**: Apollo MCU

**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/a15/a5/A7/A8/A9/A5x 64-bi/A7X a 64 bit/R4/R5, TrustZone ARMv8-M

**Cadenza**: Xtensa, diamante

**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WICED WiFi

**Cypress**: RISC-V

**Silice**: ESI-RISC

**Infineon**: XMC1000, XMC4000, Tricore

**Intel; Intel FPGA**: x36/Pentium, XScale, Nios II, Cyclone, Arria 10

**Microchip**: avr32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32

**Microsemi**: RISC-V

**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4

**Renesas**: SH, HS, V850, RX, RZ, Synergy

**Laboratori siliconici**: EFM32

**Synopsys**: Arc 600, 700, Arc em, Arc HS

**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7

**TL**: C5xxx, C6xxx, Stellaris, Sitara, tiva-C

**Elaborazione Wave**: MIPS32 4K, 24 k, 34 k, 1004 k, MIPS64 5K, MicroAptiv, InterAptiv, ProAptiv, M-Class

**Xilinx**: Microblaze, PowerPC 405, ZYNQ, Zynq UltraSCALE

*Tutte le cifre relative a tempistiche e dimensioni elencate sono stime e possono essere diverse nella piattaforma di sviluppo.*
