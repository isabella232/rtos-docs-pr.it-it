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
# <a name="overview-of-azure-rtos-netx"></a>Panoramica di Azure RTOS NetX

Azure RTOS NetX è uno stack di rete incorporato TCP/IP IPv4 di livello industriale, progettato specificamente per applicazioni IoT, real-time e deep embedded. Azure RTOS NetX è lo stack di rete IPv4 originale di Microsoft ed è essenzialmente un subset di Azure RTOS. NetX offre applicazioni incorporate con protocolli di rete di base, ad esempio IPv4, TCP e UDP, nonché una suite completa di protocolli aggiuntivi aggiuntivi di livello superiore. Un footprint ridotto, un'esecuzione rapida e una maggiore facilità d'uso rendono Azure RTOS NetX una scelta ideale per le applicazioni IoT incorporate più complesse.

## <a name="api-protocols"></a>Protocolli API

### <a name="telnet"></a>Telnet

* Footprint minimo di 0,5 KB e 0,3 KB di RAM.
* Supporto client e server.

### <a name="auto-ip"></a>IP automatico

* Assegnazione automatica degli indirizzi IPv4.
* Minimo 1,2 KB, 300 byte di RAM.

### <a name="http---hypertext-transfer-protocolhttp"></a>HTTP - Hypertext Transfer Protocol(HTTP)

* Footprint minimo da 2,8 KB a 4,8 KBBFLASH, da 0,4 KB a 1,0 KB di RAM.
* Supporto client e server.

### <a name="smtp---simple-mail-transfer-protocol-smtp"></a>SMTP - Simple Mail Transfer Protocol (SMTP)

* Footprint minimo di 4,1 KB e 0,6 KB di RAM
* Supporto client

### <a name="dhcp---dynamic-host-configuration-protocol-dhcp"></a>DHCP - Dynamic Host Configuration Protocol (DHCP)

* Memoria FLASH minima da 3,6 KB a 4,6 KB, footprint della RAM di 2,7 KB
* Supporto client e server
* Supporto IPv4

### <a name="p0p3---post-office-protocol-version-3-pop3"></a>P0P3 - Post Office Protocol versione 3 (POP3)

* Footprint minimo di 8,1 KB e 1,4 KB di RAM
* Supporto client

### <a name="snmp---simple-network-management-protocol-snmp"></a>SNMP - Simple Network Management Protocol (SNMP)

* Footprint minimo di 10,9 KB e 2,6 KB di RAM
* Supporto dell'agente per VI, V2 e V3

### <a name="ftp-tftp---file-transfer-protocol-ftp-trivial-file-transfer-protocol-tftp"></a>FTP, TFTP - File Transfer Protocol (FTP), Trivial File Transfer Protocol (TFTP)

* FTP minimo da 1,8 KB a 7,2 KBBFLASH, da 0,6 KB a 2,1 KB di footprint della RAM
* TFTP minimo da 1,7 KB a 2,4 KBBFLASH, da 0,3 KB a 1,8 KB di footprint della RAM
* Supporto client e server

### <a name="ppp---polnt-to-point-protocol-ppp"></a>PPP - Protocollo PPP (Polnt-to-PoInt)

* Footprint minimo di 7,1 KB e 3,8 KB di RAM
* Affidabilità e affidabilità.

### <a name="sntp---simple-network-time-protocol-sntp"></a>SNTP - Simple Network Time Protocol (SNTP)

* Minimo 4 KB e 0,5 KB di RAM
* Supporto client

### <a name="azure-rtos-netx-api"></a>Azure RTOS NetX API

* Implementazione rapida dell'API a copia zero
* Livello BSD facoltativo per la portabilità del codice socket legacy

### <a name="igmp---internet-group-management-protocol-igmp"></a>IGMP - Internet Group Management Protocol (IGMP)

* Flash minimo da 2,5 KB
* Supporto dei gruppi multicast IPv4
* IXIA IxANVL convalidato
* Statistiche IGMP facoltative
* Traccia a livello di sistema tramite Azure RTOS TraceX

### <a name="udp---user-datagram-protocol-udp"></a>UDP - User Datagram Protocol (UDP)

* Minimo 2,5 KB FLASH, 124 byte di RAM per socket
* Elaborazione rapida dei pacchetti TCP in prossimità di wirespeed:
* RX 95 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 14%
* TX 94 Mbps su 100 Mbps Ethernet, @100MHz MCU, utilizzo MCU del 10%
* Tecnologia udp Fast Path™
* Nessun limite al numero di UDP
* IXIA IxANVL convalidato
* Sospensione facoltativa alla ricezione socket
* Timeout facoltativo per tutte le sospensioni
* Statistiche UDP facoltative
* Traccia a livello di sistema tramite Azure RTOS TraceX

### <a name="tcp---transmission-control-protocol-tcp"></a>TCP - Transmission Control Protocol (TCP)

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

### <a name="icmp---internet-control-message-protocol-icmp"></a>ICMP - Internet Control Message Protocol (ICMP)

* MEMORIA FLASH minima di 2,5 KB
* Supporto IPv4
* IXIA IxANVL convalidato
* Richiesta ping e risposta ping
* Sospensione del thread facoltativa nelle richieste ping
* Timeout facoltativo per tutte le sospensioni
* Statistiche ICMP facoltative
* Traccia a livello di sistema tramite Azure RTOS TraceX

### <a name="ipv4---internet-protocol-ip"></a>IPv4 - Ip (Internet Protocol)

* Footprint minimo da 3,5 KB a 8,5 KB FLASH, da 2 KB a 3 KB di RAM.
* Architettura di Piconet™.
* Prestazioni veloci e near wirespeed.
* Supporto di più interfacce.
* Supporto multi-homed.
* Supporto del routing statico.
* Supporto della frammentazione/riassemblaggio IP.
* Supporto IPv4.
* IXIA IxANVL convalidato.
* Certificazione del logo pronta per la fase II.
* Statistiche IP facoltative.
* Interfaccia del driver del livello fisico ben definita e intuitiva.
* Traccia a livello di sistema tramite Azure RTOS TraceX.

### <a name="arprarp---address-resolution-protocol-arp-reverse-address-resolution-protocol-rarp"></a>ARP/RARP - Address Resolution Protocol (ARP), Reverse Address Resolution Protocol (RARP)

* Dimensioni minime di 1,7 KB di MEMORIA FLASH e RAM.
* Risoluzione dinamica di indirizzi MAC da 32 blt IPv4 e 48 blt.
* IXIA IxANVL convalidato.
* Cache ARP flessibile e definita dall'utente.
* Supporto gratuito ARP.
* Statistiche ARP/RARP facoltative determinate dall'applicazione.
* Traccia a livello di sistema tramite Azure RTOS TraceX.

### <a name="ethernet-wifi-bluetooth-le-154-etc"></a>ETHERNET, WiFi, BLUETOOTH LE, 15.4 e così via.

## <a name="interoperability-verification"></a>Verifica dell'interoperabilità

Azure RTOS NetX è conforme agli standard RFC e offre interoperabilità completa con i dispositivi per la maggior parte dei fornitori. Azure RTOS NetX usa anche lo standard di settore IxANVL (Automated Network Validation Library) per l'implementazione del protocollo TCP/IP Azure RTOS NetX Core.

## <a name="advanced-technology"></a>Tecnologia avanzata

Azure RTOS NetX è una tecnologia avanzata che include quanto segue.
* Architettura ™ Piconet.
* Ridimensionamento automatico.
* UDP Fast-Path Technology™.
* Gestione flessibile dei pacchetti.
* API e implementazione a copia zero.
* Supporto multi-homed.
* Timeout facoltativo per tutte le sospensioni.
* Supporto del routing statico.
* Azure RTOS di analisi del sistema TraceX.
