---
title: Capitolo 1-Introduzione ad Azure RTO NetX
description: Questo capitolo contiene un'introduzione ad Azure RTO NetX e una descrizione delle relative applicazioni e vantaggi.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 48be6a7ecddc53b36b3cc1a9ecfb50a11e285881
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822796"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx"></a>Capitolo 1-Introduzione ad Azure RTO NetX

Azure RTO NetX è un'implementazione in tempo reale a prestazioni elevate degli standard TCP/IP progettati esclusivamente per applicazioni incorporate basate su ThreadX. Questo capitolo contiene un'introduzione a NetX e una descrizione delle relative applicazioni e vantaggi.

## <a name="netx-unique-features"></a>Funzionalità univoche di NetX

A differenza di altre implementazioni di TCP/IP, NetX è progettato per essere versatile, con scalabilità semplice da piccole applicazioni basate su microcontroller, a quelle che usano processori RISC e DSP avanzati. Si tratta di un contrasto netto rispetto a un dominio pubblico o ad altre implementazioni commerciali destinate originariamente agli ambienti di workstation, ma vengono quindi compresse in progettazioni incorporate.

### <a name="piconettrade-architecture"></a>&trade;Architettura piconet

Sottostanti la scalabilità e le prestazioni superiori di NetX sono *piconet*, un'architettura software appositamente progettata per sistemi incorporati. L'architettura piconet ottimizza la scalabilità implementando i servizi NetX come libreria C. In questo modo, solo i servizi effettivamente utilizzati dall'applicazione vengono inseriti nell'immagine finale del runtime. Di conseguenza, le dimensioni effettive di NetX sono completamente determinate dall'applicazione. Per la maggior parte delle applicazioni, i requisiti delle dimensioni dell'immagine di NetX sono compresi tra 5 Kbyte e 30 Kbyte di dimensioni.

NetX consente di ottenere prestazioni di rete superiori mediante la sovrapposizione delle chiamate di funzione componente interne solo quando è assolutamente necessario. Inoltre, la maggior parte dell'elaborazione di NetX viene eseguita direttamente in linea, con conseguente miglioramento delle prestazioni rispetto al software di rete workstation spesso usato nelle progettazioni incorporate in passato.</th>

### <a name="zero-copy-implementation"></a>Implementazione di copia zero

NetX fornisce un'implementazione di *copia zero* basata su pacchetti di TCP/IP. La copia zero indica che i dati nel buffer di pacchetti dell'applicazione non vengono mai copiati all'interno di NetX. Questo consente di migliorare notevolmente le prestazioni e di liberare i cicli di elaborazione preziosi per l'applicazione, estremamente importante per le applicazioni incorporate.

### <a name="udp-fast-pathtrade-technology"></a>Tecnologia di percorso veloce UDP &trade;

Con la *tecnologia di percorso rapido UDP*, NETX fornisce l'elaborazione UDP più veloce possibile. Sul lato di invio, l'elaborazione UDP, incluso il checksum UDP facoltativo, è completamente inclusa nel servizio ***nx_udp_socket_send*** . Non viene effettuata alcuna chiamata di funzione aggiuntiva finché il pacchetto non è pronto per essere inviato tramite la routine di invio IP NetX interna. Questa routine è anche piatta (ad esempio, la nidificazione delle chiamate di funzione è minima), quindi il pacchetto viene rapidamente inviato al driver di rete dell'applicazione. Quando viene ricevuto il pacchetto UDP, l'elaborazione di ricezione di pacchetti NetX inserisce il pacchetto direttamente nella coda di ricezione del socket UDP appropriato o lo assegna al primo thread sospeso in attesa di un pacchetto di ricezione dalla coda di ricezione del socket UDP. Non sono necessarie opzioni di contesto ThreadX aggiuntive.

### <a name="ansi-c-source-code"></a>Codice sorgente ANSI C

NetX è scritto completamente in ANSI C ed è immediatamente portabile in qualsiasi architettura del processore con un compilatore ANSI C e il supporto di ThreadX.

### <a name="not-a-black-box"></a>Non è una scatola nera

La maggior parte delle distribuzioni di NetX include il codice sorgente C completo. In questo modo si eliminano i problemi "black-box" che si verificano con molti stack di rete commerciali. Con NetX, gli sviluppatori di applicazioni possono vedere esattamente cosa sta facendo lo stack di rete, senza alcun mistero!
  
Il codice sorgente consente anche modifiche specifiche dell'applicazione. Sebbene non sia consigliato, è senz'altro utile avere la possibilità di modificare lo stack di rete, se necessario.  

Queste funzionalità sono particolarmente confortanti per gli sviluppatori abituati a lavorare con stack di rete interni o pubblici. Si aspettano che il codice sorgente sia in grado di modificarlo. NetX è il software di rete finale per tali sviluppatori.

### <a name="bsd-compatible-socket-api"></a>API socket BSD-Compatible

Per le applicazioni legacy, NetX offre un'interfaccia socket compatibile con BSD che effettua chiamate all'API NetX a prestazioni elevate sotto. Questo consente di eseguire la migrazione del codice dell'applicazione di rete esistente a NetX.

## <a name="rfcs-supported-by-netx"></a>RFC supportate da NetX

Il supporto NetX di RFC che descrivono i protocolli di rete di base include ma non è limitato ai protocolli di rete seguenti. NetX segue tutti i requisiti generali e i requisiti di base nei vincoli di un sistema operativo in tempo reale con un footprint di memoria ridotto e un'esecuzione efficiente.

| RFC      | Descrizione                                            |
|----------|--------------------------------------------------------|
| RFC 1112 | Estensioni host per multicast IP (IGMPv1)           |
| RFC 1122 | Requisiti per gli host Internet-livelli di comunicazione |
| RFC 2236 | Protocollo di gestione dei gruppi Internet, versione 2          |
| RFC 768  | UDP (User Datagram Protocol)                           |
| RFC 791  | Protocollo IP (Internet Protocol)                                 |
| RFC 792  | Internet Control Message Protocol (ICMP)               |
| RFC 793  | Transmission Control Protocol (TCP)                    |
| RFC 826  | ARP (Ethernet Address Resolution Protocol)             |
| RFC 903  | Protocollo RARP (Reverse Address Resolution Protocol)             |
|          |                                                        |

## <a name="embedded-network-applications"></a>Applicazioni di rete incorporate

Le applicazioni di rete incorporate sono applicazioni che necessitano di accesso alla rete ed eseguite su microprocessori nascosti all'interno di prodotti quali telefoni cellulari, apparecchiature di comunicazione, motori automobilistici, stampanti laser, dispositivi medicali e così via. Tali applicazioni presentano quasi sempre alcuni vincoli di memoria e di prestazioni. Un'altra distinzione delle applicazioni di rete incorporate è che il software e l'hardware hanno uno scopo dedicato.

### <a name="real-time-network-software"></a>Software di rete in tempo reale  

In pratica, il software di rete che deve eseguire l'elaborazione in un periodo di tempo esatto viene chiamato software di *rete* in *tempo reale* e quando i vincoli temporali vengono applicati alle applicazioni di rete, vengono classificati come applicazioni in tempo reale. Le applicazioni di rete incorporate sono quasi sempre in tempo reale a causa dell'interazione intrinseca con il mondo esterno.

## <a name="netx-benefits"></a>Vantaggi di NetX

I principali vantaggi dell'uso di NetX per le applicazioni incorporate sono la connettività Internet ad alta velocità e requisiti di memoria molto ridotti. NetX è inoltre completamente integrato con il sistema operativo multitasking ThreadX in tempo reale a prestazioni elevate.

### <a name="improved-responsiveness"></a>Velocità di risposta migliorata  

Lo stack di protocolli NetX a prestazioni elevate consente alle applicazioni di rete incorporate di rispondere più rapidamente che mai. Questo è particolarmente importante per le applicazioni incorporate che hanno un volume significativo di traffico di rete o requisiti di elaborazione rigorosi in un singolo pacchetto.

### <a name="software-maintenance"></a>Manutenzione del software

L'uso di NetX consente agli sviluppatori di partizionare facilmente gli aspetti della rete dell'applicazione incorporata. Questo partizionamento rende l'intero processo di sviluppo semplice e migliora significativamente la manutenzione futura del software.

### <a name="increased-throughput"></a>Maggiore velocità effettiva

NetX offre la rete a prestazioni elevate disponibile, che è possibile ottenere con un sovraccarico minimo di elaborazione dei pacchetti. Questa operazione consente inoltre una maggiore velocità effettiva.

### <a name="processor-isolation"></a>Isolamento processore

NetX fornisce un'interfaccia affidabile e indipendente dal processore tra l'applicazione e il processore e l'hardware di rete sottostanti. Ciò consente agli sviluppatori di concentrarsi sugli aspetti della rete dell'applicazione anziché spendere più tempo per risolvere i problemi hardware che influiscono direttamente sulla rete.

### <a name="ease-of-use"></a>Semplicità d'uso

NetX è progettato tenendo presente lo sviluppatore di applicazioni. L'architettura NetX e l'interfaccia di chiamata del servizio sono facili da comprendere. Di conseguenza, gli sviluppatori NetX possono usare rapidamente le funzionalità avanzate.

### <a name="improve-time-to-market"></a>Miglioramento del time-to-Market

Le potenti funzionalità di NetX accelerano il processo di sviluppo del software. NetX estrae la maggior parte dei problemi hardware di rete e del processore, eliminando così questi problemi dalla maggior parte delle aree specifiche della rete dell'applicazione. Questo, associato alla semplicità d'uso e al set di funzionalità avanzate, comporta tempi di immissione sul mercato più rapidi.

### <a name="protecting-the-software-investment"></a>Protezione dell'investimento software

NetX è scritto esclusivamente in ANSI C ed è completamente integrato con il sistema operativo ThreadX in tempo reale. Ciò significa che le applicazioni NetX sono immediatamente portabili a tutti i processori supportati da ThreadX. Meglio ancora, un'architettura del processore completamente nuova può essere supportata con ThreadX in poche settimane. Di conseguenza, l'uso di NetX garantisce il percorso di migrazione dell'applicazione e protegge l'investimento di sviluppo originale.
