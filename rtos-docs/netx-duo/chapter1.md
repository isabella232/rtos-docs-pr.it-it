---
title: Capitolo 1-Introduzione ad Azure RTO NetX Duo
description: Questo capitolo contiene un'introduzione ad Azure RTO NetX Duo e una descrizione delle relative applicazioni e vantaggi.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 91dfd0e62cb565f677faa7d52fe22abc1f0e19a1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822127"
---
# <a name="chapter-1---introduction-to-azure-rtos-netx-duo"></a>Capitolo 1-Introduzione ad Azure RTO NetX Duo

Azure RTO NetX Duo è un'implementazione in tempo reale a prestazioni elevate degli standard TCP/IP progettati esclusivamente per applicazioni incorporate basate su Azure RTO ThreadX. Questo capitolo contiene un'introduzione a NetX Duo e una descrizione delle relative applicazioni e vantaggi. 

## <a name="netx-duo-unique-features"></a>Funzionalità univoche di NetX Duo

A differenza di altre implementazioni di TCP/IP, NetX Duo è progettato per essere versatile e facilmente scalabile da piccole applicazioni basate su micro-controller a quelle che usano processori RISC e DSP avanzati. Si tratta di un contrasto netto rispetto a un dominio pubblico o ad altre implementazioni commerciali destinate originariamente agli ambienti di workstation, ma vengono quindi compresse in progettazioni incorporate.

### <a name="piconettrade-architecture"></a>&trade;Architettura piconet

Sottostanti la scalabilità e le prestazioni superiori di NetX Duo sono <em>piconet</em>, un'architettura software appositamente progettata per i sistemi incorporati. L'architettura piconet ottimizza la scalabilità implementando NetX Duo Services come libreria C. In questo modo, solo i servizi usati dall'applicazione vengono inseriti nell'immagine finale del runtime. Di conseguenza, le dimensioni effettive di NetX Duo sono determinate dall'applicazione. Per la maggior parte delle applicazioni, i requisiti dell'immagine di istruzione di NetX Duo variano da 5 Kbyte a 30 Kbyte di dimensioni. Con IPv6 e ICMPv6 abilitati per la configurazione degli indirizzi IPv6 e i protocolli di individuazione adiacenti, NetX Duo è compreso tra 30 Kbyte e 45 kByte.

NetX Duo raggiunge prestazioni di rete superiori mediante la sovrapposizione di chiamate di funzione componente interne solo quando è necessario. Inoltre, la maggior parte dell'elaborazione di NetX Duo viene eseguita direttamente in linea, con conseguente miglioramento delle prestazioni per il software di rete workstation utilizzato in passato nelle progettazioni incorporate.

### <a name="zero-copy-implementation"></a>Implementazione di copia zero

NetX Duo fornisce un'implementazione basata su pacchetti con copia zero di TCP/IP. La copia zero indica che i dati nel buffer di pacchetti dell'applicazione non vengono mai copiati all'interno di NetX Duo. Questo consente di migliorare notevolmente le prestazioni e di liberare i cicli di elaborazione importanti per l'applicazione, che è importante nelle applicazioni incorporate.

### <a name="udp-fast-pathtrade-technology"></a>Tecnologia di percorso veloce UDP &trade;

Con la <em>tecnologia di percorso rapido UDP</em>, NETX Duo fornisce l'elaborazione UDP più veloce possibile. Sul lato di invio, l'elaborazione UDP, incluso il checksum UDP facoltativo, è contenuta all'interno del servizio <em>**nx_udp_socket_send**</em> . Non viene effettuata alcuna chiamata di funzione aggiuntiva finché il pacchetto non è pronto per essere inviato tramite la routine di invio IP di NetX Duo interna. Questa routine è anche Flat, ovvero la nidificazione delle chiamate di funzione è minima, quindi il pacchetto viene rapidamente inviato al driver di rete dell'applicazione. Quando viene ricevuto il pacchetto UDP, l'elaborazione di ricezione di pacchetti NetX Duo inserisce il pacchetto direttamente nella coda di ricezione del socket UDP appropriato o lo assegna al primo thread sospeso in attesa di un pacchetto di ricezione dalla coda di ricezione del socket UDP. Non sono necessarie opzioni di contesto ThreadX aggiuntive.

### <a name="ansi-c-source-cod"></a>Cod origine ANSI C

NetX Duo è scritto completamente in ANSI C ed è immediatamente portabile a qualsiasi architettura del processore con un compilatore ANSI C e il supporto di ThreadX. 

### <a name="not-a-black-box"></a>Non è una scatola nera

La maggior parte delle distribuzioni di NetX Duo include il codice sorgente C completo. In questo modo si eliminano i problemi "black-box" che si verificano con molti stack di rete commerciali. Con NetX Duo, gli sviluppatori di applicazioni possono vedere esattamente cosa sta facendo lo stack di rete, senza mistero!

Il codice sorgente consente anche modifiche specifiche dell'applicazione. Sebbene non sia consigliato, è utile avere la possibilità di modificare lo stack di rete, se necessario.

Queste funzionalità sono particolarmente confortanti per gli sviluppatori abituati a lavorare con stack di rete interni o pubblici. Si aspettano che il codice sorgente sia in grado di modificarlo. NetX Duo è il software di rete finale per tali sviluppatori.

### <a name="bsd-compatible-socket-api"></a>API socket BSD-Compatible

Per le applicazioni legacy, NetX Duo fornisce anche un'interfaccia socket compatibile con BSD che effettua chiamate all'API NetX Duo a prestazioni elevate sotto. Questo consente di eseguire la migrazione del codice dell'applicazione di rete esistente a NetX Duo.

## <a name="rfcs-supported-by-netx-duo"></a>RFC supportate da NetX Duo

Il supporto di NetX duo di RFC che descrivono i protocolli di rete di base include ma non è limitato ai protocolli di rete seguenti. NetX Duo segue tutti i consigli generali e i requisiti di base entro i vincoli di un sistema operativo in tempo reale con un footprint di memoria ridotto e un'esecuzione efficiente.

| **RFC**  | **Descrizione**                                        |
| -------- | ------------------------------------------------------ |
|RFC 1112 | Estensioni host per multicast IP (IGMPv1)           |
|RFC 1122 | Requisiti per gli host Internet-livelli di comunicazione |
|RFC 2236 | Protocollo di gestione dei gruppi Internet, versione 2          |
|RFC 768  | UDP (User Datagram Protocol)                           |
|RFC 791  | Protocollo IP (Internet Protocol)                                 |
|RFC 792  | Internet Control Message Protocol (ICMP)               |
|RFC 793  | Transmission Control Protocol (TCP)                    |
|RFC 826  | ARP (Ethernet Address Resolution Protocol) |
|RFC 903  | Protocollo RARP (Reverse Address Resolution Protocol) |
|RFC 5681 | Controllo di congestione TCP                     |

Di seguito sono elencate le RFC correlate a IPv6 supportate da NetX Duo.

|**RFC** |**Descrizione**|
-------- | ------------------------------------------ |
|RFC 1981 |Percorso MTU Discovery per Internet Protocol V6 (IPv6)|
|RFC 2460 | Specifica IPv6 (Internet Protocol V6)|
|RFC 2464 |Trasmissione di pacchetti IPv6 su reti Ethernet|
|RFC 4291 |Architettura di indirizzamento IPv6 (Internet Protocol V6)|
|RFC 4443 |Internet Control Message Protocol (ICMPv6) per la specifica IPv6 (Internet Protocol V6)|
|RFC 4861 |Individuazione router adiacenti per IP V6|
|RFC 4862 |Configurazione automatica degli indirizzi senza stato IPv6|

## <a name="embedded-network-applications"></a>Applicazioni di rete incorporate

Le applicazioni di rete incorporate sono applicazioni che necessitano di accesso alla rete ed eseguite su microprocessori nascosti all'interno di prodotti quali telefoni cellulari, apparecchiature di comunicazione, motori automobilistici, stampanti laser, dispositivi medicali e così via. Tali applicazioni presentano quasi sempre alcuni vincoli di memoria e di prestazioni. Un'altra distinzione delle applicazioni di rete incorporate è che il software e l'hardware hanno uno scopo dedicato.

Il software di rete che deve eseguire l'elaborazione in un periodo di tempo esatto viene chiamato software di *rete* in *tempo reale* e quando i vincoli temporali vengono imposti sulle applicazioni di rete, vengono classificati come applicazioni in tempo reale. Le applicazioni di rete incorporate sono quasi sempre in tempo reale a causa dell'interazione intrinseca con il mondo esterno.

## <a name="netx-duo-benefits"></a>Vantaggi di NetX Duo

I principali vantaggi dell'uso di NetX Duo per le applicazioni incorporate sono la connettività Internet ad alta velocità e requisiti di memoria ridotti. NetX Duo è inoltre integrato con il sistema operativo multitasking ThreadX in tempo reale a prestazioni elevate.

### <a name="improved-responsiveness"></a>Velocità di risposta migliorata

Lo stack del protocollo NetX Duo a prestazioni elevate consente alle applicazioni di rete incorporate di rispondere più rapidamente che mai. Questo è particolarmente importante per le applicazioni incorporate che hanno un volume significativo di traffico di rete o requisiti di elaborazione rigorosi in un singolo pacchetto.

### <a name="software-maintenance"></a>Manutenzione del software

L'uso di NetX Duo consente agli sviluppatori di partizionare facilmente gli aspetti della rete dell'applicazione incorporata. Questo partizionamento rende l'intero processo di sviluppo semplice e migliora significativamente la manutenzione futura del software.

### <a name="increased-throughput"></a>Maggiore velocità effettiva

NetX Duo fornisce la rete a prestazioni elevate disponibile, che è possibile ottenere con un sovraccarico minimo di elaborazione dei pacchetti. Questa operazione consente inoltre una maggiore velocità effettiva.

### <a name="processor-isolation"></a>Isolamento processore

NetX Duo fornisce un'interfaccia affidabile e indipendente dal processore tra l'applicazione e il processore e l'hardware di rete sottostanti. Ciò consente agli sviluppatori di concentrarsi sugli aspetti della rete dell'applicazione anziché spendere più tempo per risolvere i problemi hardware che influiscono direttamente sulla rete.

### <a name="ease-of-use"></a>Semplicità d'uso

NetX Duo è stato progettato tenendo presente lo sviluppatore di applicazioni. L'architettura di NetX Duo e l'interfaccia di chiamata del servizio sono facili da comprendere. Di conseguenza, gli sviluppatori di NetX Duo possono usare rapidamente le funzionalità avanzate.

### <a name="improve-time-to-market"></a>Miglioramento del time-to-Market

Le potenti funzionalità di NetX Duo accelerano il processo di sviluppo del software. NetX Duo estrae la maggior parte dei problemi hardware di rete e del processore, eliminando così questi problemi dalla maggior parte delle aree specifiche della rete dell'applicazione. Questo, associato alla semplicità d'uso e al set di funzionalità avanzate, comporta tempi di immissione sul mercato più rapidi.

### <a name="protecting-the-software-investment"></a>Protezione dell'investimento software

NetX Duo è scritto esclusivamente in ANSI C ed è completamente integrato con il sistema operativo ThreadX in tempo reale. Ciò significa che le applicazioni NetX Duo sono immediatamente portabili a tutti i processori supportati da ThreadX. Meglio ancora, una nuova architettura del processore può essere supportata con ThreadX in poche settimane. Di conseguenza, l'uso di NetX duo garantisce il percorso di migrazione dell'applicazione e protegge l'investimento di sviluppo originale.

## <a name="ipv6-ready-logo-certification"></a>Certificazione del logo pronto per IPv6

La certificazione "IPv6 ready" di NetX Duo è stata ottenuta tramite il pacchetto "IPv6 Core Protocol (fase 2) self test" disponibile nell'organizzazione IPv6 Ready. Per ulteriori informazioni sulla piattaforma di test e i test case, fare riferimento ai siti Web di IPv6-Ready del progetto seguenti:[**https://www.ipv6ready.org/**](https://www.ipv6ready.org/)

La fase 2 IPv6 Core Protocol self test suite verifica che uno stack IPv6 osservi i requisiti definiti nei seguenti RFC con test completi:  
Sezione 1: RFC 2460  
Sezione 2: RFC 4861  
Sezione 3: RFC 4862  
Sezione 4: RFC 1981  
Sezione 5: RFC 4443  

## <a name="ixanvl-test"></a>Test di IxANVL

NetX Duo viene testato con IxANVL da IXIA. IxANVL è lo standard di settore per la convalida automatica di reti e protocolli. Altre informazioni su IxANVL sono disponibili in: [**https://www.ixiacom.com/products/ixanvl**](https://www.ipv6ready.org/)

In particolare, i moduli NetX Duo seguenti sono testati con IxANVL:

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

NetX Duo è stato certificato da SGS-TÜV Saar per l'uso nei sistemi critici per la sicurezza, in base a IEC61508 e IEC-62304. La certificazione conferma che NetX Duo può essere usato nello sviluppo di software correlato alla protezione per i livelli di integrità di sicurezza più elevati dei International Electrotechnical Commission (IEC) 61508 e IEC 62304, per la "protezione funzionale dei sistemi elettronici di sicurezza elettrica, elettronici e programmabili". SGS-TÜV Saar, formato da una joint venture di SGSGroup di Germania e TÜV Saarland, è diventato la società leader accreditata e indipendente per il test, il controllo, la verifica e la certificazione del software incorporato per i sistemi correlati alla sicurezza in tutto il mondo. Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, incluso IEC 62304, vengono utilizzati per garantire la sicurezza funzionale di dispositivi medicali, sistemi di controllo dei processi, macchinari industriali e sistemi di controllo ferroviari. 

SGS-TÜV Saar ha certificato NetX Duo da usare nei sistemi autonomi per la sicurezza, in base allo standard ISO 26262. Inoltre, NetX Duo è certificato per il livello di integrità di sicurezza (ASIL) di Automotive, che rappresenta il livello più elevato di certificazione ISO 26262. 

Inoltre, SGS-TÜV Saar ha certificato NetX Duo da usare nelle applicazioni ferroviari critiche per la sicurezza, che soddisfano lo standard EN 50128 fino a SW-SIL 4.

![Diagramma del logo di certificazione SGS-TÜV Saar.](./media/user-guide/sgs-tuv-saar-logo.png)

IEC 61508 fino a SIL 4  
IEC 62304 fino a SW Safety Class C ISO 26262 ASIL D EN 50128 SW-SIL 4

> [!IMPORTANT]
> *Per ulteriori informazioni sulle versioni di NetX Duo certificate da TÜV o sulla disponibilità di report di test, certificati e documentazione associata, contattare Microsoft.*

### <a name="ul-certification"></a>Certificazione UL

NetX Duo è stato certificato da UL per conformità con UL 60730-1 allegato H, CSA E60730-1 allegato H, IEC 60730-1 allegato H, UL 60335-1 allegato R, IEC 60335-1 allegato R e UL 1998 standard di sicurezza per il software in componenti programmabili. Insieme a IEC/UL 60730-1, che presenta i requisiti per "controlli che usano software" nell'allegato H, lo standard IEC 60335-1 descrive i requisiti per "circuiti elettronici programmabili" nell'allegato R. IEC 60730 allegato H e IEC 60335-1 allegato R, indirizzare la sicurezza dell'hardware e del software MCU usati in Appliance, ad esempio macchine di lavaggio, lavastoviglie, essiccatori, frigoriferi, freezer e forni.

![Diagramma del logo di certificazione UL.](./media/user-guide/c-ru-us-logo.png)

*UL/IEC 60730, UL/IEC 60335, UL 1998*

> [!IMPORTANT]  
> *Per ulteriori informazioni sulle versioni di NetX Duo certificate da UL o sulla disponibilità di report di test, certificati e documentazione associata, contattare Microsoft.*