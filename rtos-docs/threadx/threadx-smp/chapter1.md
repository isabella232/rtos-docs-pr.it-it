---
title: Capitolo 1-Introduzione ad Azure RTO ThreadX SMP
description: Questo capitolo contiene un'introduzione al prodotto e una descrizione delle relative applicazioni e vantaggi.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 67bdb9076272fa3671ec9321baec609b291c04b8
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822475"
---
# <a name="chapter-1-introduction-to-azure-rtos-threadx-smp"></a>Capitolo 1: introduzione ad Azure RTO ThreadX SMP

Azure RTO ThreadX SMP è un kernel SMP in tempo reale a prestazioni elevate progettato appositamente per le applicazioni incorporate. Questo capitolo contiene un'introduzione al prodotto e una descrizione delle relative applicazioni e vantaggi.

## <a name="threadx-smp-unique-features"></a>Funzionalità univoche di ThreadX SMP

ThreadX SMP offre la tecnologia SMP (symmetric multiprocessing) per le applicazioni incorporate. I thread dell'applicazione SMP di ThreadX (di priorità variabile) che sono "pronti" per l'esecuzione vengono allocati in modo dinamico ai core del processore disponibili durante la pianificazione. In questo modo si ottiene una vera e propria elaborazione SMP, incluso il bilanciamento automatico del carico dell'esecuzione del thread dell'applicazione in tutti i core del processore disponibili.

A differenza di altri kernel in tempo reale, ThreadX SMP è progettato per essere versatile, semplificando il ridimensionamento tra piccole applicazioni basate su micro-controller tramite quelle che usano processori CISC, RISC e DSP avanzati.

ThreadX SMP è scalabile in base all'architettura sottostante. Poiché i servizi SMP di ThreadX vengono implementati come libreria C, solo i servizi effettivamente utilizzati dall'applicazione vengono inseriti nell'immagine di run-time. Di conseguenza, le dimensioni effettive di ThreadX SMP sono completamente determinate dall'applicazione. Per la maggior parte delle applicazioni, l'immagine di istruzione di ThreadX SMP è compresa tra 5 Kbyte e 20 KByte di dimensioni.

### <a name="picokernel-architecture"></a>Architettura™ picokernel 
Invece di sovrapporre le funzioni del kernel su altre, come le architetture tradizionali del *microkernel* , i servizi SMP di threadX si collegano direttamente al suo nucleo. Ciò comporta il cambio del contesto più rapido possibile e le prestazioni delle chiamate di servizio. Questa progettazione non a livelli viene chiamata architettura *picokernel* .

### <a name="ansi-c-source-code"></a>Codice sorgente ANSI C 
ThreadX SMP è scritto principalmente in ANSI C. Per adattare il kernel al processore di destinazione sottostante è necessaria una piccola quantità di linguaggio assembly. Questa progettazione consente di trasferire ThreadX SMP a una nuova famiglia di processori in un intervallo di tempo molto breve, in genere entro settimane.

### <a name="advanced-technology"></a>Tecnologia avanzata 
Di seguito sono riportate le caratteristiche principali della tecnologia avanzata SMP di ThreadX:

  - Architettura *picokernel* semplice
  - Bilanciamento del carico automatico
  - Esclusione processore per thread
  - Ridimensionamento automatico (footprint ridotto)
  - Elaborazione deterministica
  - Prestazioni veloci in tempo reale
  - Pianificazione di tipo preemptive e cooperativa
  - Supporto per priorità thread flessibili (32-1024)
  - Creazione dinamica di oggetti di sistema
  - Numero illimitato di oggetti di sistema
  - Gestione degli interrupt ottimizzata
  - ™ Della soglia di precedenza
  - Ereditarietà priorità
  - ™ Di concatenamento degli eventi
  - Timer software veloci
  - Gestione della memoria in fase di esecuzione
  - Monitoraggio delle prestazioni in fase di esecuzione
  - Analisi dello stack della fase di esecuzione
  - Traccia di sistema incorporata
  - Supporto del processore esteso
  - Supporto per strumenti di sviluppo vast
  - Completamente endian neutro

### <a name="not-a-black-box"></a>Non è una scatola nera
La maggior parte delle distribuzioni di ThreadX SMP include il codice sorgente C completo, nonché il linguaggio dell'assembly processorspecific. In questo modo si eliminano i problemi "black-box" che si verificano con molti kernel commerciali. Con ThreadX SMP, gli sviluppatori di applicazioni possono vedere esattamente cosa sta facendo il kernel, ma non ci sono misteri.

Il codice sorgente consente anche modifiche specifiche dell'applicazione. Sebbene non sia consigliato, è senz'altro utile avere la possibilità di modificare il kernel se è assolutamente necessario.

Queste funzionalità sono particolarmente confortanti per gli sviluppatori abituati a lavorare con i propri *kernel inhouse*. Si aspettano che il codice sorgente e la possibilità di modificare il kernel. ThreadX SMP è il kernel finale per tali sviluppatori.

### <a name="the-rtos-standard"></a>Standard RTO
Grazie alla versatilità, all'architettura *picokernel* a prestazioni elevate, alla tecnologia avanzata e alla portabilità dimostrata, threadX SMP è attualmente distribuito in più di 2 miliardi dispositivi. In questo modo si rende ThreadX SMP lo standard RTO per applicazioni con Deep embedded.

## <a name="safety-certifications"></a>Certificazioni di sicurezza

### <a name="tv-certification"></a>Certificazione TÜV  
ThreadX SMP è stato certificato da SGS-TÜV Saar per l'uso nei sistemi critici per la sicurezza, in base a IEC61508 e IEC-62304. La certificazione conferma che è possibile usare ThreadX SMP nello sviluppo di software correlati alla sicurezza per i livelli di integrità di sicurezza più elevati dei International Electrotechnical Commission (IEC) 61508 e IEC 62304, per la "protezione funzionale dei sistemi elettronici di sicurezza elettrica, elettronici e programmabili". SGS-TÜV Saar, costituito da una joint venture di SGS-Group della Germania e TÜV Saarland, è diventato la società leader accreditata e indipendente per il test, il controllo, la verifica e la certificazione del software incorporato per i sistemi correlati alla sicurezza in tutto il mondo. Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, incluso IEC 62304, vengono utilizzati per garantire la sicurezza funzionale di dispositivi medicali, sistemi di controllo dei processi, macchinari industriali e sistemi di controllo ferroviari.

SGS-TÜV Saar ha certificato SMP di ThreadX da usare nei sistemi autonomi per la sicurezza, in base allo standard ISO 26262. Inoltre, ThreadX SMP è certificato per il livello di integrità di sicurezza (ASIL) di Automotive, che rappresenta il livello più elevato di certificazione ISO 26262.

Inoltre, SGS-TÜV Saar ha certificato ThreadX SMP da usare nelle applicazioni ferroviari critiche per la sicurezza, che soddisfano lo standard EN 50128 fino a SW-SIL 4.

![Certificazione TÜV](media/image2.png)

IEC 61508 fino a SIL 4  
IEC 62304 fino alla classe di sicurezza SW C  
ISO 26262 ASIL D  
EN 50128 SW-SIL 4  

> [!IMPORTANT]
> Contattare [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) per ulteriori informazioni sulle versioni di THREADX SMP certificate da TÜV o per la disponibilità di report di test, certificati e documentazione associata.

### <a name="misra-c-compliant"></a>Conformità C MISRA 
MISRA C è un set di linee guida per la programmazione per i sistemi critici che usano il linguaggio di programmazione C. Le linee guida originali di MISRA C erano destinate principalmente alle applicazioni automobilistiche; Tuttavia, MISRA C è ora ampiamente riconosciuto come applicabile a qualsiasi applicazione di sicurezza critica. ThreadX SMP è conforme a tutte le regole "obbligatoria" e "obbligatoria" di MISRA-C:2004 e MISRA C:2012. ThreadX SMP è inoltre conforme a tutte e tre le regole "consultive". Per ulteriori informazioni, fare riferimento al documento ***ThreadX_MISRA_Compliance.pdf*** .

### <a name="ul-certification"></a>Certificazione UL 
ThreadX SMP è stato certificato da UL per conformità con UL 60730-1 allegato H, CSA E607301 allegato H, IEC 60730-1 allegato H, UL 60335-1 allegato R, IEC 60335-1 allegato R e UL 1998 standard di sicurezza per il software in componenti programmabili. Insieme a IEC/UL 60730-1, che presenta i requisiti per "controlli che usano software" nell'allegato H, lo standard IEC 60335-1 descrive i requisiti per "circuiti elettronici programmabili" nell'allegato R. IEC 60730 allegato H e IEC 60335-1 allegato R, indirizzare la sicurezza dell'hardware e del software MCU usati in Appliance, ad esempio macchine di lavaggio, lavastoviglie, essiccatori, frigoriferi, freezer e forni.

![Certificazione UL](media/image3.png) 

*UL/IEC 60730, UL/IEC 60335, UL 1998*

> [!IMPORTANT]
> Contattare [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) per ulteriori informazioni sulle versioni di THREADX SMP certificate da TÜV o per la disponibilità di report di test, certificati e documentazione associata.

### <a name="certification-pack"></a>Pacchetto di certificazione

Il ThreadX SMP Certification Pack™ è un pacchetto autonomo 100% completo, chiavi in mano, specifico per il settore, che fornisce tutte le prove SMP ThreadX necessarie per certificare o inviare correttamente il prodotto basato su SMP ThreadX ai livelli più elevati di affidabilità e criticità necessari per i sistemi aeronautici, medici e industriali critici per la sicurezza. Le certificazioni supportate includono DO-178B, ED-12B, DO-278, FDA510 (k), IEC-62304, IEC-60601, ISO-14971, UL-1998, IEC-61508, CENELEC EN50128, BS50128 e 49CFR236. sales@expresslogic.comPer ulteriori informazioni, contattare il pacchetto di certificazione.

## <a name="embedded-applications"></a>Applicazioni incorporate

Le applicazioni incorporate vengono eseguite su microprocessori nascosti all'interno di prodotti come dispositivi di comunicazione wireless, motori di automobili, stampanti laser, dispositivi medici e così via. Un'altra distinzione delle applicazioni incorporate è che il software e l'hardware hanno uno scopo dedicato.

### <a name="real-time-software"></a>Software in tempo reale 
Quando si impostano vincoli temporali sul software applicativo, questo viene chiamato software in *tempo reale* . Fondamentalmente, il software che deve eseguire l'elaborazione in un periodo di tempo esatto viene chiamato software in *tempo reale* . Le applicazioni incorporate sono quasi sempre in tempo reale a causa dell'interazione intrinseca con gli eventi esterni.

### <a name="multitasking"></a>Multitasking  
Come indicato in precedenza, le applicazioni incorporate hanno uno scopo dedicato. Per soddisfare questo scopo, il software deve eseguire una serie di *attività*. Un'attività è una parte parzialmente indipendente dell'applicazione che esegue un compito specifico. È anche vero che alcune attività sono più importanti di altre. Una delle principali difficoltà in un'applicazione incorporata è l'allocazione del processore tra le varie attività dell'applicazione. Questa allocazione dell'elaborazione tra attività in competizione è lo scopo principale di ThreadX SMP.

### <a name="tasks-vs-threads"></a>Confronto tra attività e thread 
È necessario fare un'altra distinzione sulle attività. Il termine attività viene utilizzato in diversi modi. Talvolta significa un programma scaricabile separatamente. In altri casi, può fare riferimento a un segmento di programma interno.

Nella discussione contemporanea sul sistema operativo, esistono due termini che sostituiscono più o meno l'uso dell'attività: *processo* e *thread*. Un *processo* è un programma completamente indipendente con lo spazio degli indirizzi, mentre un *thread* è un segmento di programma parzialmente indipendente eseguito all'interno di un processo. I thread condividono lo stesso spazio degli indirizzi del processo. Il sovraccarico associato alla gestione dei thread è minimo.

La maggior parte delle applicazioni incorporate non può permettersi l'overhead (sia di memoria che di prestazioni) associato a un sistema operativo completo orientato ai processi. Inoltre, i microprocessori più piccoli non hanno l'architettura hardware per supportare un vero sistema operativo orientato ai processi. Per questi motivi, ThreadX SMP implementa un modello di thread, che è estremamente efficiente e pratico per la maggior parte delle applicazioni incorporate in tempo reale.

Per evitare confusione, ThreadX SMP non usa il termine *attività*. Viene invece utilizzato il *thread* del nome più descrittivo e contemporaneo.

## <a name="threadx-smp-benefits"></a>Vantaggi di ThreadX SMP

L'uso di ThreadX SMP offre molti vantaggi alle applicazioni incorporate. Naturalmente, il vantaggio principale è il modo in cui vengono allocati i tempi di elaborazione dei thread dell'applicazione incorporati.

### <a name="automatic-load-balancing"></a>Bilanciamento del carico automatico  
ThreadX SMP fornisce bilanciamento del carico automatico (esecuzione dei thread tra i core disponibili), che semplifica il più possibile l'utilizzo di processori multicore. 

### <a name="improved-responsiveness"></a>Velocità di risposta migliorata  
Prima di kernel in tempo reale come ThreadX SMP, la maggior parte delle applicazioni incorporate ha allocato tempi di elaborazione con un semplice ciclo di controllo, in genere all'interno della funzione *principale* C. Questo approccio viene comunque utilizzato in applicazioni molto piccole o semplici. Tuttavia, in applicazioni complesse o di grandi dimensioni non è pratico perché il tempo di risposta a un evento è una funzione del tempo di elaborazione worstcase di un passaggio attraverso il ciclo di controllo.

Rendendo le cose peggiori, le caratteristiche temporali dell'applicazione cambiano ogni volta che vengono apportate modifiche al ciclo di controllo. In questo modo l'applicazione è intrinsecamente instabile e difficile da gestire e migliorare.

ThreadX SMP fornisce tempi di risposta rapidi e deterministici a eventi esterni importanti. ThreadX SMP esegue questa operazione tramite l'algoritmo di pianificazione preemptive basato sulla priorità, che consente a un thread con priorità più alta di precedere un thread con priorità più bassa. Di conseguenza, il tempo di risposta del caso peggiore si avvicina al tempo necessario per l'esecuzione di un cambio di contesto. Questo non è solo deterministico, ma è anche estremamente veloce.

### <a name="software-maintenance"></a>Manutenzione del software  
Il kernel SMP di ThreadX consente agli sviluppatori di applicazioni di concentrarsi su requisiti specifici dei thread dell'applicazione senza doversi preoccupare di modificare la tempistica di altre aree dell'applicazione. Questa funzionalità rende inoltre molto più semplice riparare o migliorare un'applicazione che utilizza ThreadX SMP.

### <a name="increased-throughput"></a>Maggiore velocità effettiva  
Per risolvere il problema del tempo di risposta del ciclo di controllo è possibile aggiungere altro polling. Ciò migliora la velocità di risposta, ma non garantisce comunque un tempo di risposta costante peggiore e non esegue alcuna operazione per migliorare la modifica futura dell'applicazione. Inoltre, il processore sta ora eseguendo un'elaborazione ancora più superflua a causa del polling aggiuntivo. Questa elaborazione non necessaria riduce la velocità effettiva complessiva del sistema.

Un aspetto interessante del sovraccarico è che molti sviluppatori presumono che gli ambienti multithreading come ThreadX SMP aumentino il sovraccarico e abbiano un impatto negativo sulla velocità effettiva totale del sistema. In alcuni casi, tuttavia, il multithreading riduce effettivamente il sovraccarico eliminando tutti i polling ridondanti che si verificano negli ambienti del ciclo di controllo. Il sovraccarico associato ai kernel multithreading è in genere una funzione del tempo necessario per il cambio di contesto. Se il tempo di cambio del contesto è inferiore rispetto al processo di polling, ThreadX SMP fornisce una soluzione con il potenziale di minore overhead e una maggiore velocità effettiva. Questo rende ThreadX SMP una scelta ovvia per le applicazioni con un livello di complessità o dimensione.

### <a name="processor-isolation"></a>Isolamento processore  
ThreadX SMP fornisce un'interfaccia processorindependent affidabile tra l'applicazione e il processore sottostante. Ciò consente agli sviluppatori di concentrarsi sull'applicazione invece di spendere una quantità significativa di informazioni sull'hardware per l'apprendimento. 

### <a name="dividing-the-application"></a>Divisione dell'applicazione  
Nelle applicazioni basate su ciclo di controllo ogni sviluppatore deve avere una conoscenza approfondita del comportamento e dei requisiti del runtime dell'applicazione. Questo perché la logica di allocazione del processore viene distribuita nell'intera applicazione. Con l'aumentare delle dimensioni o della complessità di un'applicazione, diventa impossibile per tutti gli sviluppatori ricordare i requisiti di elaborazione esatti dell'intera applicazione.

ThreadX SMP libera ogni sviluppatore dalle preoccupazioni associate all'allocazione del processore e consente loro di concentrarsi sulla parte specifica dell'applicazione incorporata. ThreadX SMP impone inoltre che l'applicazione venga divisa in thread chiaramente definiti. Di per sé, questa divisione dell'applicazione nei thread rende lo sviluppo molto più semplice.

### <a name="ease-of-use"></a>Semplicità d'uso  
ThreadX SMP è stato progettato tenendo presente lo sviluppatore di applicazioni. L'architettura SMP di ThreadX e l'interfaccia di chiamata del servizio sono progettate per essere facilmente comprensibili. Di conseguenza, gli sviluppatori di ThreadX SMP possono usare rapidamente le funzionalità avanzate.  

### <a name="improve-time-to-market"></a>Miglioramento del time-to-Market  
Tutti i vantaggi di ThreadX SMP accelerano il processo di sviluppo del software. ThreadX SMP si occupa della maggior parte dei problemi del processore e delle certificazioni di sicurezza più comuni, rimuovendo così questa operazione dalla pianificazione dello sviluppo. Tutti questi risultati hanno un tempo di immissione sul mercato più rapido.  

### <a name="protecting-the-software-investment"></a>Protezione dell'investimento software  
Grazie alla relativa architettura, ThreadX SMP è facilmente trasportato in nuovi ambienti di sviluppo e/o di processore. Questo, associato al fatto che ThreadX SMP isola le applicazioni dai dettagli dei processori sottostanti, rende le applicazioni SMP ThreadX altamente portabili. Di conseguenza, viene garantito il percorso di migrazione dell'applicazione e l'investimento di sviluppo originale è protetto.