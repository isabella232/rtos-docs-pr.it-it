---
title: Informazioni Azure RTOS ThreadX
description: Altre informazioni su Azure ThreadX, un sistema operativo avanzato in tempo reale (RTOS) progettato specificamente per applicazioni con deep embedded.
author: philmea
ms.author: philmea
ms.date: 6/9/2021
ms.service: rtos
ms.topic: overview
ms.custom: contperf-fy21q4
ms.openlocfilehash: 8c0bec2bb3b699b3a8d39d85eb322f3bbd95515a
ms.sourcegitcommit: 8b03df42920bdd544fb4195ab818043f6c71969e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2021
ms.locfileid: "114436747"
---
# <a name="overview-of-azure-rtos-threadx"></a>Panoramica di Azure RTOS ThreadX

Azure RTOS ThreadX è il sistema operativo Real-Time (RTOS) avanzato di Microsoft. È progettato specificamente per applicazioni IoT, in tempo reale e con deep embedded. Azure RTOS ThreadX offre funzionalità avanzate di pianificazione, comunicazione, sincronizzazione, timer, gestione della memoria e gestione degli interrupt. Inoltre, Azure RTOS ThreadX offre molte funzionalità avanzate, tra cui il relativo grafico™ l'architettura, la soglia di preemption™ la pianificazione, il concatenamento degli eventi, la profilatura dell'esecuzione del ™, le metriche delle prestazioni e la traccia degli eventi di sistema. In combinazione con la sua maggiore facilità d'uso, Azure RTOS ThreadX è la scelta ideale per le applicazioni incorporate più complesse. Azure RTOS ThreadX ha miliardi di distribuzioni in un'ampia gamma di prodotti, tra cui dispositivi consumer, componenti elettronici medici e apparecchiature di controllo industriale.

## <a name="threadx-footprint"></a>Footprint ThreadX

Azure RTOS ThreadX ha un'area di istruzioni di 2 KB notevolmente ridotta e un footprint minimo di 1 KB di RAM. Queste dimensioni ridotte sono in gran parte dovute all'architettura non a più livelli del picokernel e alla scalabilità automatica. Il ridimensionamento automatico significa che solo i servizi (e l'infrastruttura di supporto) usati dall'applicazione vengono inclusi nell'immagine finale in fase di collegamento.

Ecco alcune caratteristiche tipiche delle Azure RTOS ThreadX.

|Azure RTOS ThreadX Service  |Dimensioni tipiche in byte  |
|---------|---------|
|Servizi di base (richiesta) |2.000  |
|Servizi di accodamento  |900  |
|Servizi flag di evento  |900  |
|Servizi semafori  |450  |
|Servizi mutex  |1.200  |
|Servizi di memoria a blocchi  |550  |
|Servizi byte memory  |900  |

## <a name="threadx-execution-speed"></a>Velocità di esecuzione di ThreadX

Azure RTOS ThreadX ottiene un cambio di contesto di submicrosecondo nei processori più diffusi ed è complessivamente più veloce rispetto ad altri RTOS commerciali. Oltre a essere veloce, Azure RTOS ThreadX è altamente deterministico. Consente di ottenere le stesse prestazioni rapide, sia che siano disponibili 200 thread o solo uno.

Ecco alcune caratteristiche tipiche delle prestazioni di Azure RTOS ThreadX:

* Avvio rapido: Azure RTOS ThreadX viene avviato in meno di 120 cicli.
* Rimozione facoltativa del controllo degli errori di base: è Azure RTOS controllo degli errori ThreadX di base può essere ignorato in fase di compilazione. Ciò può essere utile quando il codice dell'applicazione viene verificato e non richiede più il controllo degli errori per ogni parametro. Il controllo degli errori può essere ignorato in un'unità di compilazione, anziché a livello di sistema.
* Progettazione di immagini: i servizi non sono a livelli l'uno sull'altro, eliminando il sovraccarico delle chiamate di funzione non necessarie.
* Elaborazione ottimizzata degli interrupt: solo i registri scratch vengono salvati/ripristinati all'ingresso/uscita da ISR, a meno che non sia necessaria la precedenza.
* Elaborazione API ottimizzata:

    |Azure RTOS ThreadX Service  |Tempo del servizio in microsecondi*  |
    |---------|---------|
    |Thread Suspend  |0,6  |
    |Thread Resume  |0,6  |
    |Invio in coda  |0,3  |
    |Ricezione coda  |0,3  |
    |Ottenere un semaforo  |0,2  |
    |Put Semaphore  |0,2  |
    |Cambio di contesto  |0,4  |
    |Risposta di interrupt  |0.0 – 0.6  |

    **Dati sulle prestazioni basati sul processore tipico in esecuzione a 200 MHz.*

## <a name="advanced-technology"></a>Tecnologia avanzata

Azure RTOS ThreadX è importante per la pianificazione della soglia di preemption. Questa funzionalità è univoca per Azure RTOS ThreadX ed è stata oggetto di ricerche accademiche approfondite. Per altre informazioni, vedere il documento [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf)(Pianificazione delle attività di Fixed-Priority con soglia di preemption), di Yun Wang (Concordia University) e Manas Sakslde (University of University).

Funzionalità principali di Azure RTOS ThreadX:

* Funzionalità complete e complete per il multitasking
  * Thread, timer dell'applicazione, code di messaggi, semafori di conteggio, mutex, flag di eventi, blocchi e pool di memoria di byte
* Priority-Based pianificazione preemptive
* Flessibilità di priorità: fino a 1024 livelli di priorità
* Pianificazione cooperativa
* Preemption-Threshold: univoco per Azure RTOS ThreadX, consente di ridurre i commutatori di contesto e di garantire la pianificazione (in base alla ricerca accademica)
* Protezione della memoria tramite Azure RTOS ThreadX MODULES
* Completamente deterministico
* Traccia eventi : acquisisce gli ultimi *n* eventi di sistema/applicazione
* Concatenamento di eventi: registrare una funzione di callback di notifica specifica dell'applicazione per ogni Azure RTOS di comunicazione o sincronizzazione ThreadX
* Azure RTOS ThreadX MODULES con protezione della memoria facoltativa
* Run-Time delle prestazioni
  * Numero di ripresi di thread
  * Numero di sospensioni dei thread
  * Numero di preventivi dei thread su cui si è richiesto
  * Numero di preventivi di interrupt di thread asincroni
  * Numero di inversione della priorità dei thread
  * Numero di richieste di thread
* Execution Profile Kit (EPK)
* Separare lo stack di interrupt
* Run-Time Stack Analysis
* Elaborazione ottimizzata degli interrupt timer

## <a name="multicore-support-amp--smp"></a>Supporto multicore (AMP & SMP)

ThreadX Azure RTOS Standard viene spesso usato in modalità Asimmetrica multiprocessing (AMP), in cui una copia separata di Azure RTOS ThreadX e l'applicazione (o Linux) viene eseguita in ogni core e comunicano tra loro tramite memoria condivisa o un meccanismo di comunicazione tra processori, ad esempio OpenAMP (Azure RTOS ThreadX supporta OpenAMP).

Negli ambienti in cui il caricamento dei processori è altamente dinamico, Azure RTOS SMP (ThreadX Symmetric Multiprocessing) è disponibile per le famiglie di processori seguenti:

* Arm Cortex-Ax
* Arm Cortex-Rx
* ARM Cortex-A5x a 64 bit
* MIPS 34 K, 1004 K e interAptiv
* PowerPC
* Synopsys ARC HS
* x86

Azure RTOS ThreadX SMP esegue il bilanciamento del carico dinamico *tra n* processori. Consente a tutte le Azure RTOS ThreadX (code, semafori, flag di eventi, pool di memoria e così via) di essere accessibili da qualsiasi thread in qualsiasi core. Azure RTOS ThreadX SMP abilita l'API ThreadX Azure RTOS completa in tutti i core e introduce le nuove API seguenti applicabili all'operazione SMP:

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a>Protezione della memoria tramite Azure RTOS ThreadX

Un prodotto aggiuntivo denominato moduli threadX Azure RTOS consente di aggregare uno o più thread dell'applicazione in un "modulo" che può essere caricato ed eseguito dinamicamente (o eseguito sul posto) nella destinazione.

I moduli consentono l'aggiornamento dei campi, la correzione di bug e il partizionamento dei programmi per consentire alle applicazioni di grandi dimensioni di occupare solo la memoria necessaria per i thread attivi.

I moduli hanno anche uno spazio di indirizzi separato Azure RTOS ThreadX stesso. Ciò consente Azure RTOS ThreadX di posizionare la protezione della memoria (tramite MPU o MMU) intorno al modulo in modo che l'accesso accidentale all'esterno del modulo non sia in grado di danneggiare qualsiasi altro componente software.

## <a name="misra-compliant"></a>Conforme a MISRA

Azure RTOS codice sorgente ThreadX e Azure RTOS ThreadX SMP sono conformi a MISRA-C: 2004 e MISRA C:2012. MISRA C è un set di linee guida di programmazione per i sistemi critici che usano il linguaggio di programmazione C. Le linee guida originali di MISRA C erano destinate principalmente alle applicazioni automobilistiche; Tuttavia, MISRA C è ora ampiamente riconosciuto come applicabile a qualsiasi applicazione critica per la sicurezza. Azure RTOS ThreadX è conforme a tutte le regole obbligatorie e obbligatorie di MISRA-C: 2004 e MISRA C:2012.

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Certificazione misra":::

## <a name="supports-most-popular-tools"></a>Supporta gli strumenti più diffusi

Azure RTOS ThreadX supporta gli strumenti di sviluppo incorporati più diffusi, tra cui Embedded Workbench di IAR, che offre anche il riconoscimento del kernel threadX Azure RTOS più completo disponibile. Altri strumenti di integrazione includono GNU (GCC), ARM DS-5/uVision®, Green Hudson MULTI®, Wind River Workbench, Imagination Codescape, Renesas e2studio, Metaware SeeCode, NXP CodeWarrior, Lauterbach TRACE32®, TI Code-Composer Studio, CrossCore e tutti i dispositivi analogici.

## <a name="adaptation-layer-for-threadx"></a>Livello di adattamento per ThreadX

È possibile semplificare i problemi di migrazione delle applicazioni Azure RTOS usando i livelli di adattamento [ThreadX](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers) per varie API RTOS legacy (FreeRTOS, POSIX, OSEK e così via)

> [!div class="nextstepaction"]
> [Introduzione a Azure RTOS ThreadX](chapter1.md)