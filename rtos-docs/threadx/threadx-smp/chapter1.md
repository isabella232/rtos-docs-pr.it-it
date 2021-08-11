---
title: Capitolo 1 - Introduzione all'Azure RTOS ThreadX SMP
description: Questo capitolo contiene un'introduzione al prodotto e una descrizione delle applicazioni e dei vantaggi.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9b9fb7b08691930abcf57df77fff27e619bb7a554a6235d4e234889b7c80945e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116802243"
---
# <a name="chapter-1-introduction-to-azure-rtos-threadx-smp"></a>Capitolo 1: Introduzione all'Azure RTOS ThreadX SMP

Azure RTOS ThreadX SMP è un kernel SMP in tempo reale ad alte prestazioni progettato specificamente per le applicazioni incorporate. Questo capitolo contiene un'introduzione al prodotto e una descrizione delle applicazioni e dei vantaggi.

## <a name="threadx-smp-unique-features"></a>Funzionalità univoche di ThreadX SMP

ThreadX SMP introduce la tecnologia SMP (Symmetric Multi-Processing) per le applicazioni incorporate. I thread dell'applicazione SMP ThreadX (con priorità variabile) che sono "PRONTI" per l'esecuzione vengono allocati dinamicamente ai core del processore disponibili durante la pianificazione. Ciò comporta una vera elaborazione SMP, incluso il bilanciamento del carico automatico dell'esecuzione dei thread dell'applicazione in tutti i core del processore disponibili.

A differenza di altri kernel in tempo reale, ThreadX SMP è progettato per essere versatile, facilmente scalabile tra piccole applicazioni basate su micro-controller tramite quelle che usano potenti processori CISC, RISC e DSP.

ThreadX SMP è scalabile in base all'architettura sottostante. Poiché i servizi SMP ThreadX vengono implementati come libreria C, solo i servizi effettivamente usati dall'applicazione vengono inserito nell'immagine di runtime. Di conseguenza, le dimensioni effettive di ThreadX SMP sono completamente determinate dall'applicazione. Per la maggior parte delle applicazioni, l'immagine dell'istruzione di ThreadX SMP ha una dimensione compresa tra 5 kByte e 20 KByte.

### <a name="picokernel-architecture"></a>Architettura di ™ picokernel 
Invece di creare livelli di funzioni kernel l'una sull'altra, ad esempio le architetture *a microkernel* tradizionali, i servizi ThreadX SMP si collegano direttamente al core. Ciò comporta il cambio di contesto più veloce possibile e le prestazioni delle chiamate al servizio. Questa progettazione non a livelli è *un'architettura a 360* bit.

### <a name="ansi-c-source-code"></a>Codice sorgente C ANSI 
ThreadX SMP è scritto principalmente in ANSI C. È necessaria una piccola quantità di linguaggio assembly per adattare il kernel al processore di destinazione sottostante. Questa progettazione consente di eseguire la portabilità di ThreadX SMP in una nuova famiglia di processori in tempi molto brevi, in genere entro settimane.

### <a name="advanced-technology"></a>Tecnologia avanzata 
Di seguito sono riportati i principali elementi della tecnologia avanzata ThreadX SMP:

  - Semplice *architettura a takernel*
  - Bilanciamento del carico automatico
  - Esclusione del processore per thread
  - Ridimensionamento automatico (footprint ridotto)
  - Elaborazione deterministica
  - Prestazioni veloci in tempo reale
  - Pianificazione preemptive e cooperativa
  - Supporto flessibile della priorità dei thread (32-1024)
  - Creazione dinamica di oggetti di sistema
  - Numero illimitato di oggetti di sistema
  - Gestione ottimizzata degli interrupt
  - Soglia di preemption™
  - Ereditarietà della priorità
  - Concatenamento di eventi™
  - Timer software veloci
  - Gestione della memoria di run-time
  - Monitoraggio delle prestazioni in fase di esecuzione
  - Analisi dello stack in fase di esecuzione
  - Traccia di sistema incorporata
  - Supporto di processori vasti
  - Supporto di vasti strumenti di sviluppo
  - Completamente neutro endian

### <a name="not-a-black-box"></a>Non una scatola nera
La maggior parte delle distribuzioni di ThreadX SMP include il codice sorgente C completo e il linguaggio di assembly specifico del processore. In questo modo si eliminano i problemi di "black box" che si verificano con molti kernel commerciali. Con ThreadX SMP, gli sviluppatori di applicazioni possono vedere esattamente cosa sta facendo il kernel, senza problemi.

Il codice sorgente consente anche modifiche specifiche dell'applicazione. Sebbene non sia consigliabile, è certamente vantaggioso avere la possibilità di modificare il kernel se è assolutamente necessario.

Queste funzionalità sono particolarmente confortanti per gli sviluppatori abituati a lavorare con *i propri kernel inhouse.* Si aspettano di avere codice sorgente e la possibilità di modificare il kernel. ThreadX SMP è il kernel finale per tali sviluppatori.

### <a name="the-rtos-standard"></a>The RTOS Standard
Grazie alla versatilità, all'architettura *a takernel* ad alte prestazioni, alla tecnologia avanzata e alla portabilità dimostrata, ThreadX SMP è attualmente distribuito in più di due miliardi di dispositivi. In questo modo ThreadX SMP è lo standard RTOS per le applicazioni con incorporamenti approfonditi.

## <a name="safety-certifications"></a>Certificazioni di sicurezza

### <a name="tv-certification"></a>Certificazione TÜV  
ThreadX SMP è stato certificato da SGS-TÜV Saar per l'uso in sistemi critici per la sicurezza, in base a IEC61508 e IEC-62304. La certificazione conferma che ThreadX SMP può essere usato nello sviluppo di software correlato alla sicurezza per i livelli di integrità di sicurezza più elevati di International Electrotechnical Commission (IEC) 61508 e IEC 62304, per la "Sicurezza funzionale dei sistemi elettronici, elettronici e programmabili correlati alla sicurezza elettronica". SGS-TÜV Saar, formato da un comune gruppo di SGS-Group e TÜV Saarland della Germania, è diventato la principale società indipendente e accreditata per test, controllo, verifica e certificazione di software incorporato per sistemi correlati alla sicurezza in tutto il mondo. Lo standard di sicurezza industriale IEC 61508 e tutti gli standard che ne derivano, incluso lo standard IEC 62304, vengono usati per garantire la sicurezza funzionale dei dispositivi medici elettronici, elettronici e programmabili correlati alla sicurezza elettronica, ai sistemi di controllo dei processi, ai macchinari industriali e ai sistemi di controllo delle apparecchiature.

SGS-TÜV Saar ha certificato ThreadX SMP da usare nei sistemi automobilistici critici per la sicurezza, in base allo standard ISO 26262. Inoltre, ThreadX SMP è certificato per Il livello di integrità della sicurezza automobilistica (ASIL) D, che rappresenta il livello più alto di certificazione ISO 26262.

Inoltre, SGS-TÜV Saar ha certificato ThreadX SMP da usare in applicazioni critiche per la sicurezza, in base allo standard EN 50128 fino a SW-SIL 4.

![Certificazione TÜV](media/image2.png)

IEC 61508 fino a SIL 4  
IEC 62304 fino alla classe di sicurezza SW C  
ISO 26262 ASIL D  
EN 50128 SW-SIL 4  

> [!IMPORTANT]
> Contattare per altre informazioni sulle versioni di ThreadX SMP certificate da TÜV o per la disponibilità di report di test, certificati e [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) documentazione associata.

### <a name="misra-c-compliant"></a>Conforme a MISRA C 
MISRA C è un set di linee guida per la programmazione per sistemi critici che usano il linguaggio di programmazione C. Le linee guida originali di MISRA C erano destinate principalmente alle applicazioni per il settore automobilistico; Tuttavia, MISRA C è ora ampiamente riconosciuto come applicabile a qualsiasi applicazione critica per la sicurezza. ThreadX SMP è conforme a tutte le regole "obbligatorie" e "obbligatorie" di MISRA-C:2004 e MISRA C:2012. ThreadX SMP è anche conforme a tutte e tre le regole di "consulenza". Per altri ***dettagliThreadX_MISRA_Compliance.pdf*** vedere il documento sulla gestione dei dati.

### <a name="ul-certification"></a>Certificazione UL 
ThreadX SMP è stato certificato da UL per la conformità con UL 60730-1 Annex H, CSA E607301 Annex H, IEC 60730-1 Annex H, UL 60335-1 Annex R, IEC 60335-1 Annex R e UL 1998 standard di sicurezza per il software in componenti programmabili. Insieme a IEC/UL 60730-1, che presenta i requisiti per "Controlli che usano software" nell'allegato H, Lo standard IEC 60335-1 descrive i requisiti per "Circuiti elettronici programmabili" nell'allegato R. IEC 60730 Annex H e IEC 60335-1 Allegato R per la sicurezza dell'hardware e del software MCU usati in appliance come macchine per la lavastoviglie, lavastoviglie, refrigeratori, refrigeratori, refrigeratori e apparecchiature.

![Certificazione UL](media/image3.png) 

*UL/IEC 60730, UL/IEC 60335, UL 1998*

> [!IMPORTANT]
> Contattare per altre informazioni sulle versioni di ThreadX SMP certificate da TÜV o per la disponibilità di report di test, certificati e [azure-rtos-support@microsoft.com](https://azure-rtos-support@microsoft.com) documentazione associata.

### <a name="certification-pack"></a>Pacchetto di certificazione

Il pacchetto di certificazione ThreadX SMP™ è un pacchetto autonomo completo, chiavi in porta, specifico del settore che fornisce tutte le prove di ThreadX SMP necessarie per certificare o inviare correttamente il prodotto basato su ThreadX SMP ai livelli di affidabilità e criticità più elevati richiesti per i sistemi Medical, Medical e Industrial critici per la sicurezza. Le certificazioni supportate includono DO-178B, ED-12B, DO-278, KPI510(k), IEC-62304, IEC-60601, ISO- 14971, UL-1998, IEC-61508, CENELEC EN50128, BS50128 e 49CFR236. Per altre sales@expresslogic.com informazioni sul Pacchetto di certificazione, contattare .

## <a name="embedded-applications"></a>Applicazioni incorporate

Le applicazioni incorporate vengono eseguite su microprocessori all'interno di prodotti come dispositivi di comunicazione wireless, motori di automobili, stampanti bluetooth, dispositivi medici e così via. Un'altra distinzione delle applicazioni incorporate è che il software e l'hardware hanno uno scopo dedicato.

### <a name="real-time-software"></a>Software in tempo reale 
Quando al software applicativo vengono imposti vincoli di tempo, si tratta del software *in tempo* reale. In pratica, il software che deve eseguire l'elaborazione entro un periodo di tempo esatto è detto software *in tempo* reale. Le applicazioni incorporate sono quasi sempre in tempo reale a causa dell'interazione intrinseca con gli eventi esterni.

### <a name="multitasking"></a>Multitasking  
Come accennato, le applicazioni incorporate hanno uno scopo dedicato. Per soddisfare questo scopo, il software deve eseguire un'ampia gamma di *attività.* Un'attività è una parte semi-indipendente dell'applicazione che svolge un compito specifico. È anche il caso in cui alcune attività sono più importanti di altre. Una delle principali difficoltà in un'applicazione incorporata è l'allocazione del processore tra le varie attività dell'applicazione. Questa allocazione dell'elaborazione tra attività concorrenti è lo scopo principale di ThreadX SMP.

### <a name="tasks-vs-threads"></a>Attività e thread 
È necessario fare un'altra distinzione sulle attività. Il termine attività viene usato in diversi modi. A volte significa un programma caricabile separatamente. In altri casi, può fare riferimento a un segmento di programma interno.

Nella discussione contemporanea sul sistema operativo, esistono due termini che sostituiscono più o meno l'uso dell'attività: *process* e *thread*. Un *processo* è un programma completamente indipendente con un proprio spazio di indirizzi, mentre un *thread* è un segmento di programma semi-indipendente che viene eseguito all'interno di un processo. I thread condividono lo stesso spazio di indirizzi del processo. L'overhead associato alla gestione dei thread è minimo.

La maggior parte delle applicazioni incorporate non può permettersi l'overhead (memoria e prestazioni) associato a un sistema operativo completamente orientato ai processi. Inoltre, i microprocessori più piccoli non hanno l'architettura hardware per supportare un vero sistema operativo orientato ai processi. Per questi motivi, ThreadX SMP implementa un modello di thread, estremamente efficiente e pratico per la maggior parte delle applicazioni incorporate in tempo reale.

Per evitare confusione, ThreadX SMP non usa il termine *attività*. Viene invece usato il *thread* dei nomi più descrittivo e contemporaneo.

## <a name="threadx-smp-benefits"></a>Vantaggi di ThreadX SMP

L'uso di ThreadX SMP offre molti vantaggi alle applicazioni incorporate. Naturalmente, il vantaggio principale è il tempo di elaborazione allocato ai thread dell'applicazione incorporati.

### <a name="automatic-load-balancing"></a>Bilanciamento del carico automatico  
ThreadX SMP offre il bilanciamento del carico automatico (esecuzione di thread tra core disponibili), che semplifica il più possibile l'uso di processori multicore. 

### <a name="improved-responsiveness"></a>Velocità di risposta migliorata  
Prima dei kernel in tempo reale come ThreadX SMP, la maggior parte delle applicazioni incorporate ha allocato il tempo di elaborazione con un ciclo di controllo semplice, in genere dall'interno della *funzione* principale C. Questo approccio viene ancora usato in applicazioni molto piccole o semplici. Tuttavia, nelle applicazioni di grandi dimensioni o complesse, non è pratico perché il tempo di risposta a qualsiasi evento è una funzione del tempo di elaborazione peggiore di un passaggio attraverso il ciclo di controllo.

Peggiorando le cose, le caratteristiche di temporizzazione dell'applicazione cambiano ogni volta che vengono apportate modifiche al ciclo di controllo. Ciò rende l'applicazione intrinsecamente instabile e difficile da gestire e migliorare.

ThreadX SMP offre tempi di risposta rapidi e deterministici a eventi esterni importanti. ThreadX SMP esegue questa operazione tramite l'algoritmo di pianificazione preemptive basato sulla priorità, che consente a un thread con priorità più alta di pre-eseguire un thread con priorità inferiore in esecuzione. Di conseguenza, il tempo di risposta peggiore si avvicina al tempo necessario per eseguire un cambio di contesto. Questo non è solo deterministico, ma è anche estremamente veloce.

### <a name="software-maintenance"></a>Manutenzione del software  
Il kernel SMP ThreadX consente agli sviluppatori di applicazioni di concentrarsi sui requisiti specifici dei thread dell'applicazione senza doversi preoccupare di modificare la tempistica di altre aree dell'applicazione. Questa funzionalità rende anche molto più semplice ripristinare o migliorare un'applicazione che usa ThreadX SMP.

### <a name="increased-throughput"></a>Maggiore velocità effettiva  
Un possibile soluzione al problema del tempo di risposta del ciclo di controllo è l'aggiunta di un altro polling. Ciò migliora la velocità di risposta, ma non garantisce comunque un tempo di risposta costante nel peggiore dei casi e non fa nulla per migliorare le modifiche future dell'applicazione. Inoltre, il processore sta ora eseguendo un'elaborazione ancora più superflua a causa del polling aggiuntivo. Tutte queste elaborazioni non necessarie riducono la velocità effettiva complessiva del sistema.

Un aspetto interessante per quanto riguarda l'overhead è che molti sviluppatori presuppongono che ambienti multithreading come ThreadX SMP aumentino il sovraccarico e hanno un impatto negativo sulla velocità effettiva totale del sistema. In alcuni casi, tuttavia, il multithreading riduce effettivamente il sovraccarico eliminando tutti i polling ridondanti che si verificano negli ambienti del ciclo di controllo. L'overhead associato ai kernel multithreading è in genere una funzione del tempo necessario per il cambio di contesto. Se il tempo di cambio di contesto è inferiore al processo di polling, ThreadX SMP offre una soluzione con il potenziale di un minore sovraccarico e una maggiore velocità effettiva. Ciò rende ThreadX SMP una scelta ovvia per le applicazioni con qualsiasi grado di complessità o dimensione.

### <a name="processor-isolation"></a>Isolamento del processore  
ThreadX SMP offre un'interfaccia processorindependent affidabile tra l'applicazione e il processore sottostante. In questo modo gli sviluppatori possono concentrarsi sull'applicazione anziché dedicarsi a una quantità significativa di tempo per l'apprendimento dei dettagli hardware. 

### <a name="dividing-the-application"></a>Divisione dell'applicazione  
Nelle applicazioni basate su cicli di controllo, ogni sviluppatore deve avere una conoscenza approfondita del comportamento e dei requisiti dell'intera applicazione in fase di esecuzione. Ciò è dovuto al fatto che la logica di allocazione del processore viene dispersa nell'intera applicazione. Con l'aumentare delle dimensioni o della complessità di un'applicazione, diventa impossibile per tutti gli sviluppatori ricordare i requisiti di elaborazione precisi dell'intera applicazione.

ThreadX SMP libera ogni sviluppatore dalle preoccupazioni associate all'allocazione del processore e consente di concentrarsi sulla parte specifica dell'applicazione incorporata. ThreadX SMP forza inoltre la dividizione dell'applicazione in thread chiaramente definiti. Questa divisione dell'applicazione in thread semplifica di per sé lo sviluppo.

### <a name="ease-of-use"></a>Facilità d'uso  
ThreadX SMP è progettato in base allo sviluppatore di applicazioni. L'architettura ThreadX SMP e l'interfaccia delle chiamate di servizio sono progettate per essere facilmente comprensibili. Di conseguenza, gli sviluppatori SMP ThreadX possono usare rapidamente le funzionalità avanzate.  

### <a name="improve-time-to-market"></a>Migliorare il time-to-market  
Tutti i vantaggi di ThreadX SMP accelerano il processo di sviluppo software. ThreadX SMP si occupa della maggior parte dei problemi del processore e delle certificazioni di sicurezza più comuni, rimuovendo questo impegno dalla pianificazione dello sviluppo. Tutto questo comporta un time-to-market più rapido.  

### <a name="protecting-the-software-investment"></a>Protezione dell'investimento software  
Grazie all'architettura, ThreadX SMP viene facilmente connessa a nuovi ambienti di processori e/o strumenti di sviluppo. Questo, insieme al fatto che ThreadX SMP isola le applicazioni dai dettagli dei processori sottostanti, rende le applicazioni SMP ThreadX altamente portabili. Di conseguenza, il percorso di migrazione dell'applicazione è garantito e l'investimento di sviluppo originale è protetto.