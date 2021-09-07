---
title: Capitolo 1 - Introduzione a Azure RTOS NetX Duo
description: Questo capitolo contiene un'introduzione Azure RTOS NetX Duo e una descrizione delle applicazioni e dei vantaggi.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8f45d32afcc2edbd5b851f1b7fb03e7fa2430ebc
ms.sourcegitcommit: 20a136b06a25e31bbde718b4d12a03ddd8db9051
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2021
ms.locfileid: "123552365"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo"></a>Capitolo 1 - Introduzione a Azure RTOS NetX Duo

Azure RTOS NetX Duo è un'implementazione in tempo reale ad alte prestazioni degli standard TCP/IP progettata esclusivamente per applicazioni Azure RTOS basate su ThreadX. Questo capitolo contiene un'introduzione a NetX Duo e una descrizione delle applicazioni e dei vantaggi. 

## <a name="netx-duo-unique-features"></a>Funzionalità univoche di NetX Duo

A differenza di altre implementazioni TCP/IP, NetX Duo è progettato per essere versatile e passare facilmente da piccole applicazioni basate su micro controller a quelle che usano potenti processori RISC e DSP. Questo è in netto contrasto con il dominio pubblico o altre implementazioni commerciali originariamente destinate agli ambienti workstation, ma poi compresse in progettazioni incorporate.

### <a name="piconettrade-architecture"></a>Architettura di &trade; Piconet

Alla base della scalabilità e delle prestazioni superiori di NetX Duo c'è <em>Piconet,</em>un'architettura software appositamente progettata per i sistemi incorporati. L'architettura di Piconet ottimizza la scalabilità implementando i servizi NetX Duo come libreria C. In questo modo, solo i servizi usati dall'applicazione vengono portati nell'immagine di runtime finale. Di conseguenza, le dimensioni effettive di NetX Duo sono determinate dall'applicazione. Per la maggior parte delle applicazioni, i requisiti dell'immagine di istruzione di NetX Duo sono compresi tra 5 KByte e 30 KByte. Con IPv6 e ICMPv6 abilitati per la configurazione degli indirizzi IPv6 e i protocolli di individuazione adiacente, NetX Duo ha dimensioni da 30 kbyte a 45 kbyte.

NetX Duo ottiene prestazioni di rete superiori tramite l'applicazione di più livelli alle chiamate di funzione dei componenti interni solo quando è necessario. Inoltre, gran parte dell'elaborazione NetX Duo viene eseguita direttamente in linea, con conseguenti vantaggi in termini di prestazioni eccezionali rispetto al software di rete della workstation usato in progetti incorporati in passato.

### <a name="zero-copy-implementation"></a>Implementazione in copia zero

NetX Duo offre un'implementazione di TCP/IP a copia zero basata su pacchetti. Zero copy significa che i dati nel buffer di pacchetti dell'applicazione non vengono mai copiati all'interno di NetX Duo. Ciò migliora notevolmente le prestazioni e libera preziosi cicli del processore per l'applicazione, che è importante nelle applicazioni incorporate.

### <a name="udp-fast-pathtrade-technology"></a>Tecnologia del percorso rapido &trade; UDP

Con <em>la tecnologia UDP Fast Path,</em>NetX Duo offre l'elaborazione UDP più veloce possibile. Sul lato dell'invio, l'elaborazione UDP, incluso il checksum UDP facoltativo, è contenuta nel <em>**nx_udp_socket_send**</em> servizio. Non vengono effettuate chiamate di funzione aggiuntive fino a quando il pacchetto non è pronto per l'invio tramite la routine di invio IP interna di NetX Duo. Anche questa routine è semplice, ovvero l'annidamento delle chiamate di funzione è minimo, quindi il pacchetto viene inviato rapidamente al driver di rete dell'applicazione. Quando viene ricevuto il pacchetto UDP, l'elaborazione di ricezione pacchetti NetX Duo inserisce il pacchetto direttamente nella coda di ricezione del socket UDP appropriato o lo assegna al primo thread sospeso in attesa di un pacchetto di ricezione dalla coda di ricezione del socket UDP. Non sono necessari altri commutatori di contesto ThreadX.

### <a name="ansi-c-source-code"></a>Codice sorgente ANSI C

NetX Duo è scritto completamente in ANSI C ed è immediatamente portabile in qualsiasi architettura del processore con un compilatore ANSI C e il supporto ThreadX. 

### <a name="not-a-black-box"></a>Non una scatola nera

La maggior parte delle distribuzioni di NetX Duo include il codice sorgente C completo. In questo modo si eliminano i problemi di "black box" che si verificano con molti stack di rete commerciali. Usando NetX Duo, gli sviluppatori di applicazioni possono vedere esattamente cosa sta facendo lo stack di rete, senza problemi.

La presenza del codice sorgente consente anche modifiche specifiche dell'applicazione. Anche se non è consigliabile, è utile avere la possibilità di modificare lo stack di rete, se necessario.

Queste funzionalità sono particolarmente confortanti per gli sviluppatori abituati a lavorare con stack di rete di dominio pubblico o interno. Si prevede di avere codice sorgente e la possibilità di modificarlo. NetX Duo è il software di rete finale per tali sviluppatori.

### <a name="bsd-compatible-socket-api"></a>BSD-Compatible'API Socket

Per le applicazioni legacy, NetX Duo offre anche un'interfaccia socket compatibile con BSD che effettua chiamate all'API NetX Duo ad alte prestazioni sottostante. Ciò consente di eseguire la migrazione del codice dell'applicazione di rete esistente a NetX Duo.

## <a name="rfcs-supported-by-netx-duo"></a>RFC supportate da NetX Duo

Il supporto netX Duo delle RFC che descrivono i protocolli di rete di base include, ma non è limitato ai protocolli di rete seguenti. NetX Duo segue tutte le raccomandazioni generali e i requisiti di base entro i vincoli di un sistema operativo in tempo reale con footprint di memoria ridotto ed esecuzione efficiente.

| **RFC**  | **Descrizione**                                        |
| -------- | ------------------------------------------------------ |
|RFC 1112 | Estensioni host per il multicasting IP (IGMPv1)           |
|RFC 1122 | Requisiti per gli host Internet - Livelli di comunicazione |
|RFC 2236 | Internet Group Management Protocol, versione 2          |
|RFC 768  | Udp (User Datagram Protocol)                           |
|RFC 791  | Ip (Internet Protocol)                                 |
|RFC 792  | Internet Control Message Protocol (ICMP)               |
|RFC 793  | TCP (Transmission Control Protocol)                    |
|RFC 826  | Ethernet Address Resolution Protocol (ARP) |
|RFC 903  | RaRP (Reverse Address Resolution Protocol) |
|RFC 5681 | Controllo della congestione TCP                     |

Di seguito sono riportate le RFC correlate a IPv6 supportate da NetX Duo.

|**RFC** |**Descrizione**|
-------- | ------------------------------------------ |
|RFC 1981 |Individuazione MTU percorso per Internet Protocol v6 (IPv6)|
|RFC 2460 | Specifica IPv6 (Internet Protocol v6)|
|RFC 2464 |Trasmissione di pacchetti IPv6 su reti Ethernet|
|RFC 4291 |Architettura degli indirizzi IPv6 (Internet Protocol v6)|
|RFC 4443 |Internet Control Message Protocol (ICMPv6) per la specifica IPv6 (Internet Protocol v6)|
|RFC 4861 |Individuazione adiacente per IP v6|
|RFC 4862 |Configurazione automatica degli indirizzi senza stato IPv6|

## <a name="embedded-network-applications"></a>Applicazioni di rete incorporate

Le applicazioni di rete incorporate sono applicazioni che necessitano dell'accesso alla rete ed eseguono su microprocessori nascosti all'interno di prodotti come telefoni cellulari, apparecchiature di comunicazione, motori automobilistici, stampanti laser, dispositivi medici e così via. Tali applicazioni hanno quasi sempre alcuni vincoli di memoria e prestazioni. Un'altra distinzione delle applicazioni di rete incorporate è che il software e l'hardware hanno uno scopo dedicato.

Il software di rete che deve eseguire l'elaborazione entro un periodo di tempo esatto è detto  *software* di rete in tempo reale e quando vengono imposti vincoli di tempo alle applicazioni di rete, vengono classificati come applicazioni in tempo reale. Le applicazioni di rete incorporate sono quasi sempre in tempo reale a causa dell'interazione intrinseca con il mondo esterno.

## <a name="netx-duo-benefits"></a>Vantaggi di NetX Duo

I vantaggi principali dell'uso di NetX Duo per le applicazioni incorporate sono la connettività Internet ad alta velocità e i requisiti di memoria di piccole dimensioni. NetX Duo è integrato anche con il sistema operativo threadX in tempo reale ad alte prestazioni e multitasking.

### <a name="improved-responsiveness"></a>Velocità di risposta migliorata

Lo stack di protocolli NetX Duo ad alte prestazioni consente alle applicazioni di rete incorporate di rispondere più velocemente che mai. Ciò è particolarmente importante per le applicazioni incorporate che hanno un volume significativo di traffico di rete o requisiti di elaborazione stringenti in un singolo pacchetto.

### <a name="software-maintenance"></a>Manutenzione del software

L'uso di NetX Duo consente agli sviluppatori di partizionare facilmente gli aspetti di rete dell'applicazione incorporata. Questo partizionamento semplifica l'intero processo di sviluppo e migliora in modo significativo la manutenzione futura del software.

### <a name="increased-throughput"></a>Maggiore velocità effettiva

NetX Duo offre la rete con le prestazioni più elevate disponibili, che si ottiene con un sovraccarico minimo per l'elaborazione dei pacchetti. Ciò consente anche una maggiore velocità effettiva.

### <a name="processor-isolation"></a>Isolamento del processore

NetX Duo offre un'interfaccia affidabile e indipendente dal processore tra l'applicazione e il processore e l'hardware di rete sottostanti. In questo modo gli sviluppatori possono concentrarsi sugli aspetti di rete dell'applicazione anziché dedicarsi più tempo alla gestione dei problemi hardware che interessano direttamente la rete.

### <a name="ease-of-use"></a>Facilità d'uso

NetX Duo è progettato in base allo sviluppatore di applicazioni. L'architettura di NetX Duo e l'interfaccia delle chiamate di servizio sono facili da comprendere. Di conseguenza, gli sviluppatori NetX Duo possono usare rapidamente le funzionalità avanzate.

### <a name="improve-time-to-market"></a>Migliorare il time-to-market

Le potenti funzionalità di NetX Duo accelerano il processo di sviluppo del software. NetX Duo astrae la maggior parte dei problemi relativi al processore e all'hardware di rete, rimuovendo quindi questi problemi dalla maggior parte delle aree specifiche della rete applicativa. Questo, insieme alla facilità d'uso e al set di funzionalità avanzate, comporta un time-to-market più rapido.

### <a name="protecting-the-software-investment"></a>Protezione dell'investimento software

NetX Duo è scritto esclusivamente in ANSI C ed è completamente integrato con il sistema operativo threadX in tempo reale. Ciò significa che le applicazioni NetX Duo sono immediatamente portabili a tutti i processori supportati da ThreadX. Meglio ancora, una nuova architettura del processore può essere supportata con ThreadX in poche settimane. Di conseguenza, l'uso di NetX Duo garantisce il percorso di migrazione dell'applicazione e protegge l'investimento di sviluppo originale.

## <a name="ipv6-ready-logo-certification"></a>Certificazione del logo pronto per IPv6

La certificazione "IPv6 Ready" di NetX Duo è stata ottenuta tramite il pacchetto "IPv6 Core Protocol (Fase 2) Self Test" disponibile dall'organizzazione pronta per IPv6. Per altre informazioni sulla piattaforma di test e sui test caseIPv6-Ready vedere i siti Web del progetto di test seguenti:[**https://www.ipv6ready.org/**](https://www.ipv6ready.org/)

Phase 2 IPv6 Core Protocol Self Test Suite verifica che uno stack IPv6 osservi i requisiti definiti nelle RFC seguenti con test approfonditi:  
Sezione 1: RFC 2460  
Sezione 2: RFC 4861  
Sezione 3: RFC 4862  
Sezione 4: RFC 1981  
Sezione 5: RFC 4443  

## <a name="ixanvl-test"></a>IxANVL Test

NetX Duo viene testato con IxANVL da IXIA. IxANVL è lo standard di settore per la convalida automatica di rete e protocollo. Altre informazioni su IxANVL sono disponibili all'indirizzo: [**https://www.ixiacom.com/products/ixanvl**](https://www.ipv6ready.org/)

In particolare, i moduli NetX Duo seguenti vengono testati con IxANVL:

|**Modulo** | **Standard** |
| --------- | ------------ |
|IP | RFC791 </br> RFC1122 </br> RFC894|
|ICMP | RFC792 </br> RFC1122 </br> RFC1812|
|UDP | RFC768 </br> RFC1122|
|TCP-Core| RFC793 </br> RFC1122 </br> RFC2460|
|TCP-Advanced| RFC1981</br>RFC2001</br>RFC2385</br>RFC2463</br>RFC813</br>RFC896|
|TCP-Performance| RFC793</br>RFC1323</br>RFC2018|

## <a name="safety-certifications"></a>Certificazioni di sicurezza

### <a name="tv-certification"></a>Certificazione TÜV  

NetX Duo è stato certificato da SGS-TÜV Saar per l'uso in sistemi critici per la sicurezza, in base a IEC61508 e IEC-62304. La certificazione conferma che NetX Duo può essere usato nello sviluppo di software correlato alla sicurezza per i più elevati livelli di integrità della sicurezza dei sistemi International Electrotechnical Commission (IEC) 61508 e IEC 62304, per "Sicurezza funzionale dei sistemi elettrici, elettronici e programmabili correlati alla sicurezza elettronica". SGS-TÜV Saar, formata da una joint-venture di SGSGroup e TÜV Saarland, è diventata la società leader indipendente e accreditata per il test, il controllo, la verifica e la certificazione di software incorporato per sistemi correlati alla sicurezza in tutto il mondo. Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, incluso IEC 62304, vengono usati per garantire la sicurezza funzionale dei dispositivi medici elettrici, elettronici e programmabili correlati alla sicurezza elettronica, sistemi di controllo dei processi, macchinari industriali e sistemi di controllo delle linee di trasporto. 

SGS-TÜV Saar ha certificato NetX Duo da usare nei sistemi automobilistici critici per la sicurezza, in base allo standard ISO 26262. NetX Duo è inoltre certificato per il livello di integrità della sicurezza del settore automobilistico (ASIL) D, che rappresenta il livello più alto di certificazione ISO 26262. 

Inoltre, SGS-TÜV Saar ha certificato NetX Duo per l'uso in applicazioni critiche per la sicurezza, in base allo standard EN 50128 fino a SW-SIL 4.

![Diagramma del logo di certificazione Saar SGS-TÜV.](./media/user-guide/sgs-tuv-saar-logo.png)

IEC 61508 fino a SIL 4  
IEC 62304 fino alla classe di sicurezza SW C ISO 26262 ASIL D EN 50128 SW-SIL 4

> [!IMPORTANT]
> *Per altre informazioni sulle versioni di NetX Duo certificate da TÜV o per la disponibilità di report di test, certificati e documentazione associata, contattare Microsoft.*

### <a name="ul-certification"></a>Certificazione UL

NetX Duo è stato certificato da UL per la conformità agli standard di sicurezza UL 60730-1 Annex H, CSA E60730-1 Annex H, IEC 60730-1 Annex H, UL 60335-1 Annex R, IEC 60335-1 Annex R e UL 1998 standard di sicurezza per il software in componenti programmabili. Insieme a IEC/UL 60730-1, che ha i requisiti per "Controlli che usano software" nell'allegato H, Lo standard IEC 60335-1 descrive i requisiti per "Circuiti elettronici programmabili" nell'allegato R. IEC 60730 Annex H e IEC 60335-1 Annex R per la sicurezza dell'hardware e del software MCU usati in elettrodomestici, lavastoviglie, lavastoviglie, essiccatori, refrigeratori, refrigeratori e forni.

![Diagramma del logo di certificazione UL.](./media/user-guide/c-ru-us-logo.png)

*UL/IEC 60730, UL/IEC 60335, UL 1998*

> [!IMPORTANT]  
> *Per altre informazioni sulle versioni di NetX Duo certificate da UL o per la disponibilità di report di test, certificati e documentazione associata, contattare Microsoft.*