---
title: Capitolo 1 - Introduzione a Azure RTOS NetX
description: Questo capitolo contiene un'introduzione Azure RTOS NetX e una descrizione delle applicazioni e dei vantaggi.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 207aaec18f020e8cc3534a9ef55ed338df487fd95b22b5021f691ea63ba62b8b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116782863"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx"></a>Capitolo 1 - Introduzione a Azure RTOS NetX

Azure RTOS NetX è un'implementazione ad alte prestazioni in tempo reale degli standard TCP/IP progettata esclusivamente per le applicazioni incorporate basate su ThreadX. Questo capitolo contiene un'introduzione a NetX e una descrizione delle applicazioni e dei vantaggi.

## <a name="netx-unique-features"></a>Funzionalità univoche di NetX

A differenza di altre implementazioni TCP/IP, NetX è progettato per essere versatile, facilmente scalabile da piccole applicazioni basate su microcontroller a quelle che usano potenti processori RISC e DSP. Questo è in netto contrasto con il dominio pubblico o altre implementazioni commerciali originariamente destinate agli ambienti workstation, ma poi suddivise in progettazioni incorporate.

### <a name="piconettrade-architecture"></a>Architettura di &trade; Piconet

Alla base della scalabilità e delle prestazioni superiori di NetX *c'è Piconet,* un'architettura software progettata appositamente per i sistemi incorporati. L'architettura di Piconet ottimizza la scalabilità implementando i servizi NetX come libreria C. In questo modo, solo i servizi effettivamente usati dall'applicazione vengono portati nell'immagine di runtime finale. Di conseguenza, le dimensioni effettive di NetX sono completamente determinate dall'applicazione. Per la maggior parte delle applicazioni, i requisiti relativi alle dimensioni delle immagini di NetX sono compresi tra 5 kByte e 30 KByte.

NetX ottiene prestazioni di rete superiori tramite il layering delle chiamate di funzione dei componenti interni solo quando è assolutamente necessario. Inoltre, gran parte dell'elaborazione NetX viene eseguita direttamente in linea, con conseguenti notevoli vantaggi in termini di prestazioni rispetto al software di rete delle workstation spesso usato in progetti incorporati in passato.</th>

### <a name="zero-copy-implementation"></a>Implementazione con copia zero

NetX fornisce un'implementazione di TCP/IP *a copia zero* basata su pacchetti. Zero copy significa che i dati nel buffer di pacchetti dell'applicazione non vengono mai copiati all'interno di NetX. In questo modo si migliorano notevolmente le prestazioni e si liberano importanti cicli del processore per l'applicazione, che è estremamente importante nelle applicazioni incorporate.

### <a name="udp-fast-pathtrade-technology"></a>Tecnologia fast path &trade; UDP

Con *la tecnologia UDP Fast Path,* NetX offre la massima velocità di elaborazione UDP possibile. Sul lato di invio, l'elaborazione UDP, incluso il checksum UDP facoltativo, è completamente contenuta all'interno ***nx_udp_socket_send*** servizio. Non vengono effettuate chiamate di funzione aggiuntive fino a quando il pacchetto non è pronto per essere inviato tramite la routine di invio IP NetX interna. Anche questa routine è semplice(ad esempio, l'annidamento delle chiamate di funzione è minimo), quindi il pacchetto viene inviato rapidamente al driver di rete dell'applicazione. Quando viene ricevuto il pacchetto UDP, l'elaborazione di ricezione pacchetti NetX inserisce il pacchetto direttamente nella coda di ricezione del socket UDP appropriato o lo concede al primo thread sospeso in attesa di un pacchetto di ricezione dalla coda di ricezione del socket UDP. Non sono necessari altri commutatori di contesto ThreadX.

### <a name="ansi-c-source-code"></a>Codice sorgente C ANSI

NetX è scritto completamente in ANSI C ed è portabile immediatamente in qualsiasi architettura del processore con un compilatore ANSI C e il supporto ThreadX.

### <a name="not-a-black-box"></a>Non una scatola nera

La maggior parte delle distribuzioni di NetX include il codice sorgente C completo. In questo modo si eliminano i problemi di "black box" che si verificano con molti stack di reti commerciali. Con NetX, gli sviluppatori di applicazioni possono vedere esattamente le prestazioni dello stack di rete, senza problemi.
  
La presenza del codice sorgente consente anche modifiche specifiche dell'applicazione. Sebbene non sia consigliabile, è certamente vantaggioso avere la possibilità di modificare lo stack di rete, se necessario.  

Queste funzionalità sono particolarmente confortevoli per gli sviluppatori abituati a lavorare con stack di rete di dominio pubblico o interno. Si aspettano di avere codice sorgente e la possibilità di modificarlo. NetX è il software di rete finale per tali sviluppatori.

### <a name="bsd-compatible-socket-api"></a>API socket BSD-Compatible

Per le applicazioni legacy, NetX fornisce un'interfaccia socket compatibile con BSD che effettua chiamate all'API NetX ad alte prestazioni sottostante. Ciò consente di eseguire la migrazione del codice dell'applicazione di rete esistente a NetX.

## <a name="rfcs-supported-by-netx"></a>RFC supportate da NetX

Il supporto NetX delle RFC che descrivono i protocolli di rete di base include, ma non è limitato ai protocolli di rete seguenti. NetX segue tutte le raccomandazioni generali e i requisiti di base entro i vincoli di un sistema operativo in tempo reale con footprint di memoria ridotto ed esecuzione efficiente.

| RFC      | Descrizione                                            |
|----------|--------------------------------------------------------|
| RFC 1112 | Estensioni host per ip multicasting (IGMPv1)           |
| RFC 1122 | Requisiti per gli host Internet - Livelli di comunicazione |
| RFC 2236 | Internet Group Management Protocol, versione 2          |
| RFC 768  | User Datagram Protocol (UDP)                           |
| RFC 791  | Ip (Internet Protocol)                                 |
| RFC 792  | Internet Control Message Protocol (ICMP)               |
| RFC 793  | TCP (Transmission Control Protocol)                    |
| RFC 826  | ARP (Address Resolution Protocol) Ethernet             |
| RFC 903  | RaRP (Reverse Address Resolution Protocol)             |
|          |                                                        |

## <a name="embedded-network-applications"></a>Applicazioni di rete incorporate

Le applicazioni di rete incorporate sono applicazioni che necessitano dell'accesso alla rete e che vengono eseguite su microprocessori nascosti all'interno di prodotti come telefoni cellulari, apparecchiature di comunicazione, motori automobilistici, stampanti bluetooth, dispositivi medici e così via. Tali applicazioni hanno quasi sempre alcuni vincoli di memoria e prestazioni. Un'altra distinzione tra le applicazioni di rete incorporate è che il software e l'hardware hanno uno scopo dedicato.

### <a name="real-time-network-software"></a>Software di rete in tempo reale  

Fondamentalmente, il software di rete che deve eseguire  l'elaborazione entro un periodo di tempo esatto è detto *software* di rete in tempo reale e, quando vengono imposti vincoli di tempo alle applicazioni di rete, vengono classificati come applicazioni in tempo reale. Le applicazioni di rete incorporate sono quasi sempre in tempo reale a causa dell'interazione intrinseca con il mondo esterno.

## <a name="netx-benefits"></a>Vantaggi di NetX

I vantaggi principali dell'uso di NetX per le applicazioni incorporate sono la connettività Internet ad alta velocità e i requisiti di memoria molto piccoli. NetX è anche completamente integrato con il sistema operativo threadX in tempo reale ad alte prestazioni e multitasking.

### <a name="improved-responsiveness"></a>Velocità di risposta migliorata  

Lo stack di protocolli NetX ad alte prestazioni consente alle applicazioni di rete incorporate di rispondere più velocemente che mai. Ciò è particolarmente importante per le applicazioni incorporate che hanno un volume significativo di traffico di rete o requisiti di elaborazione stringenti per un singolo pacchetto.

### <a name="software-maintenance"></a>Manutenzione del software

L'uso di NetX consente agli sviluppatori di partizionare facilmente gli aspetti di rete dell'applicazione incorporata. Questo partizionamento semplifica l'intero processo di sviluppo e migliora significativamente la manutenzione futura del software.

### <a name="increased-throughput"></a>Maggiore velocità effettiva

NetX offre le migliori prestazioni di rete disponibili, che si ottiene con un sovraccarico minimo per l'elaborazione dei pacchetti. Ciò consente anche una maggiore velocità effettiva.

### <a name="processor-isolation"></a>Isolamento del processore

NetX offre un'interfaccia affidabile e indipendente dal processore tra l'applicazione e il processore sottostante e l'hardware di rete. In questo modo gli sviluppatori possono concentrarsi sugli aspetti di rete dell'applicazione anziché dedicarsi più tempo alla gestione dei problemi hardware che interessano direttamente la rete.

### <a name="ease-of-use"></a>Facilità d'uso

NetX è progettato per lo sviluppatore di applicazioni. L'architettura NetX e l'interfaccia delle chiamate di servizio sono facili da comprendere. Di conseguenza, gli sviluppatori NetX possono usare rapidamente le funzionalità avanzate.

### <a name="improve-time-to-market"></a>Migliorare il time-to-market

Le potenti funzionalità di NetX accelerano il processo di sviluppo del software. NetX astrae la maggior parte dei problemi hardware del processore e della rete, rimuovendo così questi problemi dalla maggior parte delle aree specifiche della rete dell'applicazione. Questo, insieme alla facilità d'uso e al set di funzionalità avanzate, consente di ottenere un time-to-market più veloce.

### <a name="protecting-the-software-investment"></a>Protezione dell'investimento software

NetX è scritto esclusivamente in ANSI C ed è completamente integrato con il sistema operativo ThreadX in tempo reale. Ciò significa che le applicazioni NetX sono immediatamente portabili in tutti i processori supportati da ThreadX. Meglio ancora, un'architettura del processore completamente nuova può essere supportata con ThreadX in poche settimane. Di conseguenza, l'uso di NetX garantisce il percorso di migrazione dell'applicazione e protegge l'investimento di sviluppo originale.
