---
title: Informazioni Azure RTOS ThreadX
description: Altre informazioni su Azure ThreadX, un sistema operativo avanzato in tempo reale (RTOS) progettato specificamente per applicazioni con integrazione avanzata.
author: philmea
ms.author: philmea
ms.date: 6/9/2021
ms.service: rtos
ms.topic: overview
ms.custom: contperf-fy21q4
ms.openlocfilehash: 300307a82cfde9c74ec0a2499528898b384076676f75bd592fa2840bc5ac53a8
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116796302"
---
# <a name="overview-of-azure-rtos-threadx"></a>Panoramica di Azure RTOS ThreadX

Azure RTOS ThreadX è il sistema operativo RTOS (Advanced Industrial Grade Real-Time Operating System) di Microsoft. È progettato specificamente per applicazioni IoT, in tempo reale e con un'incorporata profonda. Azure RTOS ThreadX offre funzionalità avanzate di pianificazione, comunicazione, sincronizzazione, timer, gestione della memoria e gestione degli interrupt. Inoltre, Azure RTOS ThreadX ha molte funzionalità avanzate: tra cui il picokernel™ l'architettura, la soglia di preemption™ la pianificazione, il concatenamento di eventi, la profilatura dell'esecuzione ™, le metriche delle prestazioni e la traccia degli eventi di sistema. Insieme alla semplicità d'uso superiore, Azure RTOS ThreadX è la scelta ideale per le applicazioni incorporate più complesse. Azure RTOS ThreadX ha miliardi di distribuzioni in un'ampia gamma di prodotti, tra cui dispositivi consumer, elettronica medicale e apparecchiature di controllo industriale.

## <a name="threadx-footprint"></a>Footprint ThreadX

Azure RTOS ThreadX ha un'area di istruzioni di 2 KB notevolmente ridotta e un footprint minimo di 1 KB di RAM. Queste dimensioni ridotte sono in gran parte dovute all'architettura a picokernel non a più livelli e al ridimensionamento automatico. Il ridimensionamento automatico significa che solo i servizi (e l'infrastruttura di supporto) usati dall'applicazione vengono inclusi nell'immagine finale in fase di collegamento.

Ecco alcune caratteristiche tipiche delle Azure RTOS ThreadX.

|Azure RTOS servizio ThreadX  |Dimensioni tipiche in byte  |
|---------|---------|
|Servizi di base (richiesta) |2.000  |
|Servizi code  |900  |
|Servizi flag di eventi  |900  |
|Servizi di semaforo  |450  |
|Servizi Mutex  |1.200  |
|Bloccare i servizi di memoria  |550  |
|Servizi di memoria byte  |900  |

## <a name="threadx-execution-speed"></a>Velocità di esecuzione ThreadX

Azure RTOS ThreadX ottiene un commutatore di contesto di sottosecondi nei processori più diffusi ed è più veloce complessivamente rispetto ad altri RTOS commerciali. Oltre a essere veloce, Azure RTOS ThreadX è altamente deterministico. Ottiene le stesse prestazioni veloci indipendentemente dal fatto che siano pronti 200 thread o solo uno.

Ecco alcune caratteristiche di prestazioni tipiche di Azure RTOS ThreadX:

* Avvio rapido: Azure RTOS ThreadX viene avviato in meno di 120 cicli.
* Rimozione facoltativa del controllo degli errori di base: è Azure RTOS controllo degli errori ThreadX di base può essere ignorato in fase di compilazione. Ciò può essere utile quando il codice dell'applicazione viene verificato e non richiede più il controllo degli errori per ogni parametro. Il controllo degli errori può essere eseguito su un'unità di compilazione, anziché a livello di sistema.
* Progettazione di picokernel: i servizi non sono a livelli l'uno sull'altro, eliminando l'overhead delle chiamate di funzione non necessarie.
* Elaborazione di interrupt ottimizzata: solo i registri scratch vengono salvati/ripristinati al momento dell'ingresso/uscita di ISR, a meno che non sia necessaria la precedenza.
* Elaborazione api ottimizzata:

    |Azure RTOS servizio ThreadX  |Tempo di servizio in microsecondi*  |
    |---------|---------|
    |Sospensione dei thread  |0,6  |
    |Ripresa di thread  |0,6  |
    |Invio in coda  |0,3  |
    |Ricezione coda  |0,3  |
    |Ottenere un semaforo  |0,2  |
    |Inserire un semaforo  |0,2  |
    |Cambio di contesto  |0,4  |
    |Risposta di interrupt  |0.0 – 0.6  |

    **Dati sulle prestazioni basati sul processore tipico in esecuzione a 200 MHz.*

## <a name="advanced-technology"></a>Tecnologia avanzata

Azure RTOS ThreadX è importante per la pianificazione della soglia di priorità. Questa funzionalità è univoca per Azure RTOS ThreadX ed è stata oggetto di ricerche accademiche approfondite. Per altre informazioni, vedere il documento [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://ieeexplore.ieee.org/document/811269)(Pianificazione delle attività Fixed-Priority con soglia di preemption), di Yun Wang (Concordia University) e Manas Saksena (University of Pittsburgh).

Funzionalità chiave di Azure RTOS ThreadX:

* Funzionalità multitasking complete e complete
  * Thread, timer dell'applicazione, code di messaggi, semafori di conteggio, mutex, flag di eventi, blocchi e pool di memoria di byte
* Priority-Based pianificazione preventiva
* Flessibilità di priorità: fino a 1024 livelli di priorità
* Pianificazione cooperativa
* Preemption-Threshold: univoco per Azure RTOS ThreadX, consente di ridurre i commutatori di contesto e di garantire la pianificazione (per ricerca accademica)
* Protezione della memoria tramite Azure RTOS ThreadX MODULES
* Completamente deterministico
* Traccia eventi: acquisisci gli ultimi *n eventi* di sistema/applicazione
* Concatenamento di eventi: registrare una funzione di callback "notify" specifica dell'applicazione per ogni Azure RTOS di comunicazione o sincronizzazione ThreadX
* Azure RTOS moduli ThreadX con protezione della memoria facoltativa
* Run-Time metriche delle prestazioni
  * Numero di rievazioni di thread
  * Numero di sospensioni dei thread
  * Numero di pre-svuotari di thread richiesto
  * Numero di pre-svuotaoni di interrupt di thread asincroni
  * Numero di inversioni di priorità dei thread
  * Numero di richieste di thread
* Kit del profilo di esecuzione (EPK)
* Separare lo stack di interrupt
* Run-Time'analisi dello stack
* Ottimizzazione dell'elaborazione degli interrupt del timer

## <a name="multicore-support-amp--smp"></a>Supporto multicore (AMP & SMP)

ThreadX Azure RTOS standard viene spesso usato in modalità Asimmetrica multiprocessing (AMP), in cui una copia separata di Azure RTOS ThreadX e l'applicazione (o Linux) viene eseguita in ogni core e comunicano tra loro tramite memoria condivisa o un meccanismo di comunicazione tra processori come OpenAMP (Azure RTOS ThreadX supporta OpenAMP).

Negli ambienti in cui il caricamento dei processori è altamente dinamico, Azure RTOS multiprocessing simmetrico ThreadX (SMP) è disponibile per le famiglie di processori seguenti:

* Arm Cortex-Ax
* Arm Cortex-Rx
* ARM Cortex-A5x a 64 bit
* MIPS 34 K, 1004 K e interAptiv
* PowerPC
* Synopsys ARC HS
* x86

Azure RTOS ThreadX SMP esegue il bilanciamento del carico dinamico tra *n* processori. Consente a tutte Azure RTOS threadX (code, semafori, flag di eventi, pool di memoria e così via) di accedere a qualsiasi thread in qualsiasi core. Azure RTOS ThreadX SMP abilita l'API ThreadX Azure RTOS completa in tutti i core e introduce le nuove API seguenti applicabili all'operazione SMP:

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