---
title: Informazioni Azure RTOS ThreadX
description: Azure ThreadX è un sistema operativo avanzato in tempo reale (RTOS) progettato specificamente per applicazioni con integrazione avanzata.
author: philmea
ms.author: philmea
ms.date: 6/9/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: e786e5bf1f434ec9543823dee8784b677a2b371f
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171387"
---
# <a name="overview-of-azure-rtos-threadx"></a>Panoramica di Azure RTOS ThreadX

Azure RTOS ThreadX è il sistema operativo RTOS (Advanced Industrial Grade Real-Time Operating System) di Microsoft progettato specificamente per applicazioni IoT, real-time e deep embedded. Azure RTOS ThreadX offre funzionalità avanzate di pianificazione, comunicazione, sincronizzazione, timer, gestione della memoria e gestione degli interrupt. Inoltre, Azure RTOS ThreadX ha molte funzionalità avanzate, tra cui il picokernel™ l'architettura, la soglia di preemption™ la pianificazione, il concatenamento di eventi, la profilatura dell'esecuzione ™, le metriche delle prestazioni e la traccia degli eventi di sistema. Insieme alla semplicità d'uso superiore, Azure RTOS ThreadX è la scelta ideale per le applicazioni incorporate più complesse. Dal 2017, Azure RTOS ThreadX ha oltre 6,2 miliardi di distribuzioni, in un'ampia gamma di prodotti, tra cui dispositivi consumer, elettronica medicale e apparecchiature di controllo industriale.

## <a name="api-protocols"></a>Protocolli API

### <a name="azure-rtos-threadx-services"></a>Azure RTOS ThreadX Services

* Creazione dinamica di thread
* Nessun limite al numero di thread
* Le API del thread principale includono:
  * tx_thread_create
  * tx_thread_delete
  * tx_thread_preemption_change
  * tx_thread_priority_change
  * tx_thread_relinquish
  * tx_thread_reset
  * tx_thread_resume
  * tx_thread_sleep
  * tx_thread_suspend
  * tx_thread_terminate
  * tx_thread_wait_abort
* Informazioni aggiuntive e API per le prestazioni

### <a name="message-queues"></a>Code di messaggi

* Creazione dinamica della coda
* Nessun limite al numero di code
* Messaggi copiati per valore (o per riferimento tramite puntatore)
* Dimensioni dei messaggi da 1 a 16 parole a 32 bit
* Sospensione di thread facoltativa in modalità vuota e completa
* Timeout facoltativo per tutte le sospensioni
* Le API principali della coda di messaggi includono:
  * tx_queue_create
  * tx_queue_delete
  * tx_queue_flush
  * tx_queue_front_send
  * tx_queue_receive
  * tx_queue_send_notify
* Informazioni aggiuntive e API per le prestazioni

### <a name="counting-semaphores"></a>Conteggio dei semafori

* Creazione dinamica del semaforo
* Nessun limite al numero di semafori
* Semafori di conteggio a 32 bit (da 0 a 4.294.967.295)
* Supporta la protezione dei consumer-producer o delle risorse
* Sospensione del thread facoltativa quando il semaforo non è disponibile
* Timeout facoltativo per tutte le sospensioni
* Le PRINCIPALI API del semaforo includono:
  * tx_semaphore_create
  * tx_semaphore_delete
  * tx_semaphore_get
  * tx_semaphore_put
  * tx_semaphore_put_notify
* Informazioni aggiuntive e API per le prestazioni

### <a name="mutexes"></a>Mutex

* Creazione dinamica di mutex
* Nessun limite al numero di mutex
* Protezione delle risorse annidate supportata
* Ereditarietà della priorità facoltativa supportata
* Sospensione del thread facoltativa quando mutex non disponibile
* Timeout facoltativo per tutte le sospensioni
* Le PRINCIPALI API mutex includono:
  * tx_mutex_create
  * tx_mutex_delete
  * tx_mutex_get
  * tx_mutex_put
* Informazioni aggiuntive e API per le prestazioni

### <a name="event-flags"></a>Flag di evento

* Creazione di gruppi di flag di eventi dinamici
* Nessun limite al numero di gruppi di flag di eventi
* Sincronizzazione di uno o più thread
* Supporto di operazioni get e clear atomiche
* Sospensione multithread facoltativa nel set di eventi AND/OR
* Timeout facoltativo per tutte le sospensioni
* Le API dei flag di eventi principali includono:
  * tx_event_flags_create
  * tx_event_flags_delete
  * tx_event_flags_get
  * tx_event_flags_set
  * tx_event_flags_set_notify
* Informazioni aggiuntive e API per le prestazioni

### <a name="block-memory-pools"></a>Bloccare i pool di memoria

* Creazione dinamica del pool a blocchi
* Nessun limite al numero di pool di blocchi
* Nessun limite alle dimensioni dei blocchi di dimensioni fisse o delle dimensioni del pool
* Più veloce possibile allocazione di memoria/deal-location
* Sospensione facoltativa dei thread nel pool vuoto
* Timeout facoltativo per tutte le sospensioni
* Le API principali del pool di blocchi includono:
  * tx_block_pool_create
  * tx_block_pool_delete
  * tx_block_allocate
  * tx_block_release
* Informazioni aggiuntive e API per le prestazioni

### <a name="byte-memory-pools"></a>Pool di memoria di byte

* Creazione dinamica del pool di byte
* Nessun limite al numero di pool di byte
* Nessun limite alle dimensioni del pool di byte
* Allocazione/deallocazione di memoria a lunghezza variabile più flessibile
* Località delle dimensioni di allocazione supportata
* Sospensione facoltativa dei thread in un pool vuoto
* Timeout facoltativo per tutte le sospensioni
* Le API principali del pool di byte includono:
  * tx_byte_pool_create
  * tx_byte_pool_delete
  * tx_byte_allocate
  * tx_byte_release
* Informazioni aggiuntive e API per le prestazioni

### <a name="application-timers"></a>Timer dell'applicazione

* Creazione dinamica del timer
* Nessun limite al numero di timer
* Timer periodici o one-shot supportati
* I timer periodici possono avere un valore di scadenza iniziale diverso
* Nessuna ricerca nell'attivazione o disattivazione del timer
* Tutti i timer guidati da un interrupt timer hardware
* Le API principali del timer includono:
  * tx_timer_create
  * tx_timer_delete
  * tx_timer_activate
  * tx_timer_change
  * tx_timer_deactivate
* Informazioni aggiuntive e API per le prestazioni

### <a name="azure-rtos-threadx-core-scheduler"></a>Azure RTOS ThreadX Core Scheduler

* Footprint minimo di RAM da 2 KB FLASH, 1 KB
* Cambio di contesto rapido e secondario
* Completamente deterministico indipendentemente dal numero di thread
* Pianificazione preventiva basata sulla priorità
* 32 livelli di priorità predefiniti, facoltativamente fino a 1024 livelli
* Pianificazione cooperativa entro il livello di priorità (FIFO)
* Tecnologia preemption-threshold
* Servizi timer facoltativi, tra cui:
  * Intervallo di tempo facoltativo per thread
  * Timeout facoltativo per tutti i blocchi
  * LE API richiedono l'interrupt del timer hardware
* Profilatura dell'esecuzione
* Traccia a livello di sistema
* Sicurezza certificata per molti standard

## <a name="most-deployed-rtos"></a>RTOS più distribuito

Azure RTOS ThreadX ha oltre 6,2 miliardi di distribuzioni in tutto il mondo, secondo la società leader di intelligence di mercato M2M, VDC Research. La popolarità di Azure RTOS ThreadX è un esempio di affidabilità, qualità, dimensioni, prestazioni, funzionalità avanzate, facilità d'uso e vantaggi complessivi del time-to-market.

> *"Abbiamo seguito la crescita di THREADX nei mercati wireless e IoT fin dalla sua creazione e siamo sempre più impressionati dall'adozione diffusa di THREADX nel settore".* – Chris Rommel, Executive Vice President, VDC Research

## <a name="small-footprint"></a>Ingombro

Azure RTOS ThreadX richiede un'area di istruzioni di 2 KB notevolmente ridotta e 1 KB di RAM per il footprint minimo. Ciò è dovuto in gran parte all'architettura a ™ a più livelli e alla scalabilità automatica. Il ridimensionamento automatico significa che solo i servizi (e l'infrastruttura di supporto) usati dall'applicazione vengono inclusi nell'immagine finale in fase di collegamento.

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

## <a name="fast-execution"></a>Esecuzione rapida

Azure RTOS ThreadX ottiene un cambio di contesto di sottosecondo nei processori più diffusi ed è notevolmente più veloce rispetto ad altri RTOS commerciali. Oltre a essere veloce, Azure RTOS ThreadX è altamente deterministico. Consente di ottenere le stesse prestazioni veloci, sia che siano disponibili 200 thread o solo uno.

Ecco alcune caratteristiche tipiche delle prestazioni di Azure RTOS ThreadX:

* Avvio rapido: Azure RTOS ThreadX viene avviato in meno di 120 cicli.
* Rimozione facoltativa del controllo degli errori di base: è Azure RTOS controllo degli errori ThreadX di base può essere ignorato in fase di compilazione. Ciò può essere utile quando il codice dell'applicazione viene verificato e non richiede più il controllo degli errori per ogni parametro. Si noti che questa operazione può essere eseguita su un'unità di compilazione, anziché a livello di sistema.
* Picokernel™ Progettazione: i servizi non sono a livelli l'uno sull'altro, eliminando così l'overhead delle chiamate di funzione non necessarie.
* *Elaborazione interrupt ottimizzata: solo i registri scratch vengono salvati/ripristinati al momento dell'ingresso/uscita di ISR, a meno che non sia necessaria la precedenza.
* Elaborazione API ottimizzata:

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

Azure RTOS ThreadX è una tecnologia avanzata la cui funzionalità più importante è la pianificazione della soglia di priorità. Questa funzionalità è univoca per Azure RTOS ThreadX ed è stata oggetto di ricerche accademiche approfondite. Ad esempio, vedere [Scheduling Fixed-Priority Tasks with Preemption Threshold](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf)(Pianificazione di attività di Fixed-Priority con soglia di preemption), di Yun Wang, Concordia University e Manas Sakslde, University of University of Bayh.

Considerare le funzionalità di Azure RTOS ThreadX.

* Funzionalità complete e complete per il multitasking
  * Thread, timer dell'applicazione, code di messaggi, semafori di conteggio, mutex, flag di eventi, pool di memoria di blocchi e byte
* Priority-Based preemptive
* Flessibilità di priorità: fino a 1024 livelli di priorità
* Pianificazione cooperativa
* Preemption-Threshold™: univoco per Azure RTOS ThreadX, consente di ridurre i commutatori di contesto e di garantire la pianificazione (in base alla ricerca accademica)
* Protezione della memoria tramite Azure RTOS ThreadX MODULES
* Completamente deterministico
* Traccia eventi: acquisisce gli ultimi *n* eventi di sistema/applicazione
* Concatenamento di ™: registrare una funzione di callback di notifica specifica dell'applicazione per ogni Azure RTOS di comunicazione ThreadX o di sincronizzazione
* Azure RTOS ThreadX MODULES con protezione della memoria facoltativa
* Run-Time delle prestazioni
  * Numero di ripresi di thread
  * Numero di sospensioni dei thread
  * Numero di preemption di thread su cui si è richiesto
  * Numero di interruzioni di thread asincrone
  * Numero di inversione della priorità dei thread
  * Numero di richieste di thread
* Execution Profile Kit (EPK)
* Separare lo stack di interrupt
* Run-Time'analisi dello stack
* Elaborazione ottimizzata degli interrupt del timer

## <a name="multicore-support-amp--smp"></a>Supporto multicore (AMP & SMP)

ThreadX Azure RTOS standard viene spesso usato in modalità Asimmetrica multiprocessing (AMP), in cui una copia separata di Azure RTOS ThreadX e l'applicazione (o Linux) vengono eseguite in ogni core e comunicano tra loro tramite memoria condivisa o un meccanismo di comunicazione tra processori, ad esempio OpenAMP (Azure RTOS ThreadX supporta OpenAMP). Si tratta della configurazione multicore più tipica che usa Azure RTOS ThreadX e può essere la più efficiente se l'applicazione è in grado di caricare in modo efficace i processori.

Per gli ambienti in cui il caricamento dei processori è altamente dinamico, Azure RTOS ThreadX Symetric Multiprocessing (SMP) è disponibile per le famiglie di processori seguenti:

* Arm Cortex-Ax
* Arm Cortex-Rx
* ARM Cortex-A5x a 64 bit
* MIPS 34K, 1004K e interAptiv
* PowerPC
* Synopsys ARC HS
* x86

Azure RTOS ThreadX SMP esegue il bilanciamento del carico dinamico tra *n* processori e consente a tutte le risorse threadX di Azure RTOS (code, semafori, flag di eventi, pool di memoria e così via) di essere accessibili da qualsiasi thread in qualsiasi core. Azure RTOS ThreadX SMP abilita l'API ThreadX Azure RTOS completa in tutti i core e introduce la nuova API seguente applicabile all'operazione SMP:

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a>Protezione della memoria tramite Azure RTOS ThreadX

Un prodotto aggiuntivo denominato Azure RTOS ThreadX MODULES consente di aggregare uno o più thread dell'applicazione in un "modulo" che può essere caricato ed eseguito dinamicamente (o eseguito sul posto) nella destinazione.

I moduli consentono l'aggiornamento dei campi, la correzione di bug e il partizionamento dei programmi per consentire alle applicazioni di grandi dimensioni di occupare solo la memoria necessaria per i thread attivi.

I moduli hanno anche uno spazio di indirizzi completamente separato Azure RTOS ThreadX stesso. Ciò consente Azure RTOS ThreadX di posizionare la protezione della memoria (tramite MPU o MMU) intorno al modulo in modo che l'accesso accidentale all'esterno del modulo non sia in grado di danneggiare altri componenti software.


## <a name="misra-compliant"></a>Conforme a MISRA

Azure RTOS threadx e Azure RTOS codice SMP ThreadX è conforme a MISRA-C:2004 e MISRA C:2012. MISRA C è un set di linee guida per la programmazione per sistemi critici che usano il linguaggio di programmazione C. Le linee guida originali di MISRA C erano destinate principalmente alle applicazioni per il settore automobilistico; Tuttavia, MISRA C è ora ampiamente riconosciuto come applicabile a qualsiasi applicazione critica per la sicurezza. Azure RTOS ThreadX è conforme a tutte le regole obbligatorie e obbligatorie di MISRA-C:2004 e MISRA C:2012.

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Certificazione errata":::

## <a name="supports-most-popular-architectures"></a>Supporta le architetture più comuni

Azure RTOS ThreadX viene eseguito nei microprocessori a 32/64 bit più diffusi, preimpresciati, completamente testati e completamente supportati, inclusi i seguenti:

* Dispositivi analoghi: SHARC, Blackfin, CM4xx
* Andes Core: RISC-V
* Ambiqmicro: Cpu avi
* ARM: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x a 64 bit/R4/R5, TrustZone ARMv8-M
* Cadenza: Xtensa, Diamond
* CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi
* Cypress: RISC-V
* EnSilica: eSi-RISC
* Infineon: XMC1000, XMC4000, TriCore
* Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Kpine, Arria 10
* Microchip: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32
* Microsemi: RISC-V
* NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4
* Renesas: SH, HS, V850, RX, RZ, Synergy
* Silicon Labs: EFM32
* Synopsys: ARC 600, 700, ARC EM, ARC HS
* ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7
* Tl: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C
* Wave Computing: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class
* Xilinx: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE

## <a name="supports-most-popular-tools"></a>Supporta gli strumenti più diffusi

Azure RTOS ThreadX supporta la maggior parte degli strumenti di sviluppo incorporati più diffusi, tra cui Embedded Workbench™ di IAR, che offre anche la conoscenza del kernel ThreadX Azure RTOS più completa disponibile. L'integrazione aggiuntiva degli strumenti include GNU (GCC), ARM DS-5/uVision®, Green Hudson MULTI®, Wind River Workbench™, Imagination Codescape, Renesas e2studio, Metaware SeeCode™, NXP CodeWarrior, Lauterrbac TRACE32®, TI Code-Composer Studio, CrossCore e tutti i dispositivi analogici.
