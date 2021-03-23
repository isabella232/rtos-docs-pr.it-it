---
title: Informazioni su Azure RTO ThreadX
description: Azure ThreadX è un sistema operativo in tempo reale avanzato (RTO), progettato specificamente per applicazioni con Deep embedded.
author: philmea
ms.author: philmea
ms.date: 6/9/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: acee58d9c48cb7a66993aaa5dc4a565dfe96234d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823249"
---
# <a name="overview-of-azure-rtos-threadx"></a>Panoramica di Azure RTO ThreadX

Azure RTO ThreadX è il sistema operativo Microsoft Advanced Industrial Real-Time (RTO), progettato in modo specifico per applicazioni molto incorporate e in tempo reale. Azure RTO ThreadX offre funzionalità avanzate di pianificazione, comunicazione, sincronizzazione, timer, gestione della memoria e gestione delle interruzioni. Inoltre, Azure RTO ThreadX offre molte funzionalità avanzate, tra cui l'architettura picokernel™, la soglia di precedenza™ la pianificazione, la concatenazione di eventi, la profilatura™ esecuzione, le metriche delle prestazioni e la traccia eventi di sistema. Insieme alla relativa semplicità di utilizzo, Azure RTO ThreadX è la scelta ideale per le applicazioni incorporate più complesse. A partire da 2017, Azure RTO ThreadX ha oltre 6,2 miliardi distribuzioni, in un'ampia gamma di prodotti, tra cui dispositivi consumer, elettronica medica e apparecchiature di controllo industriale.

## <a name="api-protocols"></a>Protocolli API

### <a name="azure-rtos-threadx-api"></a>API ThreadX di Azure RTO

* API intuitiva e coerente
* Sostantivo-convenzione di denominazione dei verbi
* Tutte le API hanno *tx_* principali per identificare facilmente come Azure RTO threadX
* Le API di blocco hanno un timeout thread facoltativo
* Molte API sono direttamente disponibili dall'applicazione ISRs

### <a name="azure-rtos-threadx-services"></a>Servizi ThreadX di Azure RTO

* Creazione di thread dinamici
* Nessun limite per il numero di thread
* Le API thread principali includono:
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
* Altre informazioni e API per le prestazioni

### <a name="message-queues"></a>Code di messaggi

* Creazione coda dinamica
* Nessun limite al numero di code
* Messaggi copiati per valore (o per riferimento tramite puntatore)
* Dimensioni dei messaggi dalle parole da 1 a 16 32 bit
* Sospensione thread facoltativa su vuota e piena
* Timeout facoltativo per tutte le sospensioni
* Le principali API della coda di messaggi includono:
  * tx_queue_create
  * tx_queue_delete
  * tx_queue_flush
  * tx_queue_front_send
  * tx_queue_receive
  * tx_queue_send_notify
* Altre informazioni e API per le prestazioni

### <a name="counting-semaphores"></a>Conteggio dei semafori

* Creazione dinamica del semaforo
* Nessun limite per il numero di semafori
* semafori di conteggio a 32 bit (da 0 a 4.294.967.295)
* Supporta la protezione delle risorse e dei producer
* Sospensione thread facoltativa quando semaforo non disponibile
* Timeout facoltativo per tutte le sospensioni
* Le API principali del semaforo includono:
  * tx_semaphore_create
  * tx_semaphore_delete
  * tx_semaphore_get
  * tx_semaphore_put
  * tx_semaphore_put_notify
* Altre informazioni e API per le prestazioni

### <a name="mutexes"></a>Mutex

* Creazione di mutex dinamici
* Nessun limite al numero di mutex
* Protezione delle risorse nidificata supportata
* Ereditarietà priorità facoltativa supportata
* Sospensione thread facoltativa quando mutex non disponibile
* Timeout facoltativo per tutte le sospensioni
* Le principali API mutex includono:
  * tx_mutex_create
  * tx_mutex_delete
  * tx_mutex_get
  * tx_mutex_put
* Altre informazioni e API per le prestazioni

### <a name="event-flags"></a>Flag evento

* Creazione di gruppi di flag di evento dinamici
* Nessun limite al numero di gruppi di flag di evento
* Sincronizzazione di un thread o di più thread
* Supporto per Atomic Get e Clear
* Sospensione multithread facoltativa su e/o set di eventi
* Timeout facoltativo per tutte le sospensioni
* Le API principali del flag di evento includono:
  * tx_event_flags_create
  * tx_event_flags_delete
  * tx_event_flags_get
  * tx_event_flags_set
  * tx_event_flags_set_notify
* Altre informazioni e API per le prestazioni

### <a name="block-memory-pools"></a>Blocca pool di memoria

* Creazione di pool di blocchi dinamici
* Nessun limite al numero di pool di blocchi
* Nessun limite per le dimensioni dei blocchi a dimensione fissa o delle dimensioni del pool
* Allocazione di memoria/Deal-location più veloce possibile
* Sospensione thread facoltativa nel pool vuoto
* Timeout facoltativo per tutte le sospensioni
* Le API principali del pool di blocchi includono:
  * tx_block_pool_create
  * tx_block_pool_delete
  * tx_block_allocate
  * tx_block_release
* Altre informazioni e API per le prestazioni

### <a name="byte-memory-pools"></a>Pool di memoria byte

* Creazione di pool di byte dinamici
* Nessun limite al numero di pool di byte
* Nessun limite per le dimensioni del pool di byte
* Allocazione/deallocazione di memoria a lunghezza variabile più flessibile
* Impostazioni locali per le dimensioni di allocazione supportate
* Sospensione thread facoltativa nel pool vuoto
* Timeout facoltativo per tutte le sospensioni
* Le principali API del pool di byte includono:
  * tx_byte_pool_create
  * tx_byte_pool_delete
  * tx_byte_allocate
  * tx_byte_release
* Altre informazioni e API per le prestazioni

### <a name="application-timers"></a>Timer applicazione

* Creazione di timer dinamici
* Nessun limite al numero di timer
* Timer periodici o monouso supportati
* I timer periodici possono avere un valore di scadenza iniziale diverso
* Nessuna ricerca sull'attivazione o la disattivazione del timer
* Tutti i timer basati su un interrupt del timer hardware
* Le API del timer principale includono:
  * tx_timer_create
  * tx_timer_delete
  * tx_timer_activate
  * tx_timer_change
  * tx_timer_deactivate
* Altre informazioni e API per le prestazioni

### <a name="azure-rtos-threadx-core-scheduler"></a>Utilità di pianificazione principale di Azure RTO ThreadX

* FLASH 2 KB minimo, impronta RAM 1 KB
* Cambio di contesto veloce, Sub-microsecondo
* Completamente deterministico indipendentemente dal numero di thread
* Pianificazione in base alla priorità e piena di PreEmptive
* 32 livelli di priorità predefiniti, facoltativamente fino a 1024 livelli
* Pianificazione cooperativa all'interno del livello di priorità (FIFO)
* Tecnologia di soglia di precedenza
* Servizi timer facoltativi, tra cui:
  * Intervallo di tempo facoltativo per thread
  * Timeout facoltativo per tutti i blocchi
  * API richiede nell'interrupt del timer hardware
* Profilatura esecuzione
* Traccia a livello di sistema
* Sicurezza certificata per molti standard

## <a name="most-deployed-rtos"></a>RTO più distribuiti

Azure RTO ThreadX ha più di 6,2 miliardi distribuzioni in tutto il mondo, in base alla principale azienda di marketing di M2M, Data Center Research. La popolarità di Azure RTO ThreadX è un testamento per l'affidabilità, la qualità, le dimensioni, le prestazioni, le funzionalità avanzate, la facilità d'uso e i vantaggi complessivi di time-to-Market.

> *"Abbiamo seguito la traiettoria di crescita di THREADX nei mercati wireless e di tutto il mondo, dal momento che la società è stata trovata e sono sempre più impressionati dall'adozione generalizzata di THREADX".* – Chris Rommel, Executive Vice President, DC Research

## <a name="small-footprint"></a>Footprint ridotto

Azure RTO ThreadX richiede un'area di istruzioni 2 KB molto piccola e 1 KB di RAM per il footprint minimo. Questa operazione è in gran parte dovuta all'architettura™ non a più livelli di picokernel e alla scalabilità automatica. La scalabilità automatica indica che solo i servizi (e l'infrastruttura di supporto) usati dall'applicazione sono inclusi nell'immagine finale in fase di collegamento.

Di seguito sono riportate alcune caratteristiche tipiche delle dimensioni ThreadX di Azure RTO:

|Servizio ThreadX di Azure RTO  |Dimensioni tipiche in byte  |
|---------|---------|
|Servizi di base (obbligatorio) |2\.000  |
|Servizi di Accodamento  |900  |
|Servizi flag di evento  |900  |
|Servizi semaforo  |450  |
|Servizi mutex  |1.200  |
|Blocca servizi di memoria  |550  |
|Servizi di memoria byte  |900  |

## <a name="fast-execution"></a>Esecuzione rapida

Azure RTO threadX ottiene un cambio di contesto di microsecondo nei processori più diffusi ed è significativamente più veloce rispetto ad altri RTOSes commerciali. Oltre a essere veloce, Azure RTO ThreadX è anche estremamente deterministico. Ottiene le stesse prestazioni veloci se sono presenti 200 thread pronti o solo uno.

Di seguito sono riportate alcune caratteristiche tipiche delle prestazioni di Azure RTO ThreadX:

* Avvio rapido: Azure RTO ThreadX avvia in meno di 120 cicli.
* Rimozione facoltativa del controllo degli errori di base: il controllo degli errori di base di Azure RTO ThreadX può essere ignorato in fase di compilazione. Questa operazione può essere utile quando il codice dell'applicazione viene verificato e non richiede più il controllo degli errori per ogni parametro. Si noti che questa operazione può essere eseguita in un'unità di compilazione, anziché a livello di sistema.
* Picokernel™ progettazione: i servizi non sono sovrapposti tra loro, eliminando così un sovraccarico di chiamate di funzione non necessario.
* * Elaborazione interrupt ottimizzata: solo i registri Scratch vengono salvati/ripristinati in caso di immissione/uscita ISR, a meno che non sia necessaria la precedenza.
* Elaborazione API ottimizzata:

    |Servizio ThreadX di Azure RTO  |Tempo di servizio in microsecondi *  |
    |---------|---------|
    |Sospensione thread  |0,6  |
    |Ripresa thread  |0,6  |
    |Coda Invio  |0,3  |
    |Ricezione coda  |0,3  |
    |Ottieni semaforo  |0,2  |
    |Inserisci semaforo  |0,2  |
    |Cambio di contesto  |0,4  |
    |Risposta di interrupt  |0,0 – 0,6  |

    **Cifre sulle prestazioni basate sul processore tipico in esecuzione in 200MHz*.

## <a name="pre-certified-by-tuv-and-ul-to-many-safety-standards"></a>Pre-certificati da TUV e UL a molti standard di sicurezza

Azure RTO ThreadX e Azure RTO ThreadX SMP sono stati certificati da SGS-TUV Saar per l'uso nei sistemi critici per la sicurezza, secondo IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 ASIL D e EN 50128. La certificazione conferma che è possibile usare Azure RTO ThreadX e Azure RTO ThreadX SMP nello sviluppo di software correlati alla sicurezza per i livelli di integrità di sicurezza più elevati di IEC-61508, IEC-62304, ISO 26262 e EN 50128 per la "protezione funzionale dei sistemi elettronici, elettrici, elettronici e programmabili relativi alla sicurezza elettronica". SGS-TUV Saar, formato da una joint venture del SGS-Group e del TUV della Germania, è diventato la società leader accreditata e indipendente per il test, il controllo, la verifica e la certificazione del software incorporato per i sistemi correlati alla sicurezza in tutto il mondo. Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, tra cui IEC-62304, ISO 26262 e EN 50128, vengono usati per garantire la protezione funzionale di dispositivi medicali elettrici, elettronici e programmabili per la sicurezza elettronica, sistemi di controllo dei processi, macchinari industriali, automobili e sistemi di controllo ferroviario.

:::image type="content" source="media/overview-threadx/partener-logo-sgs-tuv-saar-2.png" alt-text="Certificazione SGS TUV SAAR":::

Azure RTO ThreadX e Azure RTO ThreadX SMP sono stati riconosciuti da UL per garantire la conformità con UL 60730-1 allegato H, CSA E60730-1 allegato H, IEC 60730-1 allegato H, UL 60335-1 allegato R, IEC 60335-1 allegato R e UL 1998 standard di sicurezza per il software in componenti programmabili. UL è una società globale, indipendente e scientifica per la sicurezza, con più di un secolo di competenze innovative per l'innovazione delle soluzioni di sicurezza, che vanno dall'adozione pubblica di energia elettrica ai progressi della sostenibilità, dell'energia rinnovabile e della nanotecnologia.

:::image type="content" source="media/overview-threadx/cru-logo-certification.png" alt-text="Certificazione UL":::

Gli artefatti (certificato, manuale di sicurezza, report di test e così via) associati alle certificazioni TUV e UL sono disponibili per la vendita.

## <a name="eal4-common-criteria-security-certification"></a>EAL4 + criteri comuni certificazione di sicurezza

Azure RTO ha raggiunto la certificazione di sicurezza EAL4 + Common Criteria. La destinazione di valutazione (TOE) copre Azure RTO ThreadX, Azure RTO NetX-Duo, Azure RTO NetX Secure TLS e Azure RTO NETX MQTT. Questo rappresenta i protocolli più tipici necessari per i sensori, i dispositivi, i router perimetrali e i gateway con incorporate profondità.

:::image type="content" border="false" source="media/overview-threadx/eal-logo-certification.png" alt-text="Certificazione EAL":::

La funzionalità di valutazione della sicurezza IT usata per la certificazione di sicurezza di Azure RTO è BrightSight BV e l'autorità di certificazione è SERTIT.

## <a name="simple-easy-to-use"></a>Semplice e facile da usare

Azure RTO ThreadX è molto semplice da usare. L'API ThreadX di Azure RTO è intuitiva e altamente funzionale. I nomi delle API sono costituiti da parole reali e non dalla zuppa alfabetica dei nomi molto abbreviati che sono così comuni in altri prodotti RTO. Tutte le API ThreadX di Azure RTO hanno un leader `tx_` e seguono una convenzione di denominazione dei verbi sostantivi. Inoltre, esiste una coerenza funzionale nell'API. Tutte le API che sospendono, ad esempio, hanno un timeout facoltativo che funziona in modo identico per le API.

La creazione di un'applicazione ThreadX di Azure RTO è facile. L'applicazione deve includere *tx_api. h*, chiamare `tx_kernel_enter` da Main, definire la `tx_application_define` funzione e creare un thread, definire la funzione del punto di ingresso del thread e collegarsi alla libreria threadX di Azure RTO (in genere *TX. a*).

Azure RTO ThreadX vanta anche il maggior calibro di documentazione disponibile. 

## <a name="advanced-technology"></a>Tecnologia avanzata

Azure RTO ThreadX è una tecnologia avanzata la cui caratteristica più rilevante è la pianificazione della soglia di precedenza. Questa funzionalità è univoca per Azure RTO ThreadX ed è stata l'oggetto di una ricerca accademica completa. Vedere ad esempio [pianificazione Fixed-Priority attività con soglia di precedenza](https://www.cs.utah.edu/~regehr/reading/open_papers/preempt_thresh.pdf), di Yun Wang, Concordia University e Manas Siviglia, University of Pittsburgh.

Prendere in considerazione le funzionalità di Azure RTO ThreadX:

* Funzionalità complete e complete per il multitasking
  * Thread, timer applicazione, code di messaggi, semafori di conteggio, mutex, flag di evento, pool di memoria a blocchi e byte
* Priority-Based la pianificazione di tipo preemptive
* Flessibilità prioritaria: fino a 1024 livelli di priorità
* Pianificazione cooperativa
* ™ Della soglia di precedenza: univoco per Azure RTO ThreadX, consente di ridurre i cambi di contesto e contribuire a garantire la pianificazione (per ricerca accademica)
* Protezione della memoria tramite i moduli ThreadX di Azure RTO
* Completamente deterministica
* Traccia eventi-Acquisisci gli ultimi *n* eventi di sistema/applicazione
* Concatenamento di eventi™: registrare una funzione di callback "notify" specifica dell'applicazione per ogni comunicazione o oggetto di sincronizzazione ThreadX di RTO di Azure
* MODULI ThreadX di Azure RTO con protezione della memoria facoltativa
* Metriche delle prestazioni Run-Time
  * Numero di riprese dei thread
  * Numero di sospensioni di thread
  * Numero di prelazioni dei thread richieste
  * Numero di interruzioni di interrupt del thread asincrono
  * Numero di inversioni di priorità thread
  * Numero di thread abbandonati
* Kit del profilo di esecuzione (EPK)
* Stack di interrupt separato
* Analisi dello stack Run-Time
* Elaborazione interrupt timer ottimizzata

## <a name="multicore-support-amp--smp"></a>Supporto multicore (AMP & SMP)

Il ThreadX standard di Azure RTO viene spesso usato in modo multiprocessore asimmetrico, in cui una copia separata di Azure RTO ThreadX e l'applicazione (o Linux) viene eseguita in ogni core e comunicano tra loro tramite memoria condivisa o un meccanismo di comunicazione tra processori come OpenAMP (Azure RTO ThreadX supporta OpenAMP). Questa è la configurazione multicore più tipica con Azure RTO ThreadX e può essere il più efficiente se l'applicazione è in grado di caricare effettivamente i processori.

Per gli ambienti in cui il caricamento dei processori è altamente dinamico, Azure RTO ThreadX simmetrica multiprocessing (SMP) è disponibile per le famiglie di processori seguenti:

* Cortex-Ax ARM
* Cortex-Rx ARM
* ARM Cortex-A5x a 64 bit
* MIPS 34K, 1004K e interAptiv
* PowerPC
* Synopsys ARC HS
* x86

Azure RTO ThreadX SMP esegue il bilanciamento del carico dinamico tra *n* processori e consente a tutte le risorse di Azure RTO threadX (code, semafori, flag di evento, pool di memoria e così via) di accedere a qualsiasi thread in qualsiasi core. Azure RTO ThreadX SMP consente l'intera API RTO ThreadX di Azure in tutti i core e introduce le nuove API seguenti applicabili all'operazione SMP:

* `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
* `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
* `UINT tx_thread_smp_core_get(void);`
* `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
* `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## <a name="memory-protection-via-azure-rtos-threadx-modules"></a>Protezione della memoria tramite i moduli ThreadX di Azure RTO

Un prodotto aggiuntivo denominato moduli ThreadX di Azure RTO consente di aggregare uno o più thread dell'applicazione in un "modulo", che può essere caricato e eseguito in modo dinamico (o eseguito sul posto) nella destinazione.

I moduli consentono l'aggiornamento dei campi, la correzione di bug e il partizionamento del programma per consentire alle applicazioni di grandi dimensioni di occupare solo la memoria necessaria per i thread attivi.

I moduli hanno anche uno spazio degli indirizzi completamente separato da Azure RTO ThreadX. In questo modo, Azure RTO ThreadX può inserire la protezione della memoria (tramite MPU o MMU) intorno al modulo, in modo che l'accesso accidentale esterno al modulo non sia in grado di danneggiare altri componenti software.

## <a name="fastest-time-to-market"></a>Time-to-market più veloce

Azure RTO ThreadX è facile da installare, apprendere, usare, eseguire il debug, verificare, certificare e gestire. Di conseguenza, Azure RTO ThreadX è stato il leader di RTO time-to-market per gli ultimi sette anni consecutivi, in base ai sondaggi relativi alle previsioni di mercato incorporate (EMF). I sondaggi mostrano costantemente che il 70% delle progettazioni che usano Azure RTO ThreadX per raggiungere il mercato nel tempo, superando tutte le altre RTOSes.

Di seguito sono riportati i motivi per i vantaggi del time-to-Market coerenti:

* Documentazione sulla qualità
* Disponibilità del codice sorgente completa
* API di facile utilizzo
* Set di funzionalità completo e avanzato
* Integrazione di strumenti di terze parti di ampio respiro, in particolare il Workbench incorporato di IAR™

## <a name="royalty-free"></a>Royalty gratuito

Non è previsto alcun costo per l'uso e il test del codice sorgente e nessun costo per le licenze di produzione quando viene distribuito in dispositivi con licenza preliminare, tutti gli altri dispositivi necessitano di una licenza annuale semplice.

## <a name="full-highest-quality-source-code"></a>Codice sorgente completo di qualità elevata

Fin dall'inizio, Azure RTO ThreadX è stato progettato per essere un livello industriale RTO, distribuito con codice sorgente C completo. Il codice sorgente ThreadX di Azure RTO ha impostato la qualità e la facilità di comprensione. Inoltre, la convenzione relativa alla presenza di una funzione per ogni file fornisce una semplice navigazione all'origine.

Azure RTO ThreadX è conforme alle convenzioni di codifica rigide, incluso il requisito che ogni riga di codice C abbia un commento significativo. Inoltre, l'origine ThreadX di Azure RTO è stata certificata per gli standard più elevati.

## <a name="misra-compliant"></a>Conforme a MISRA

Azure RTO ThreadX e Azure RTO ThreadX SMP origine code sono MISRA-C:2004 e MISRA C:2012 conformi. MISRA C è un set di linee guida per la programmazione per i sistemi critici che usano il linguaggio di programmazione C. Le linee guida originali di MISRA C erano destinate principalmente alle applicazioni automobilistiche; Tuttavia, MISRA C è ora ampiamente riconosciuto come applicabile a qualsiasi applicazione critica per la sicurezza. ThreadX RTO di Azure è conforme a tutte le regole obbligatorie e obbligatorie di MISRA-C:2004 e MISRA C:2012.

:::image type="content" source="media/overview-threadx/misra-logo-certification.png" alt-text="Certificazione MISRA":::

## <a name="supports-most-popular-architectures"></a>Supporta le architetture più diffuse

Azure RTO ThreadX viene eseguito sui microprocessori più diffusi a 32/64 bit, predefiniti, completamente testati e completamente supportati, inclusi i seguenti:

* Dispositivi analoghi: SHARC, Blackfin, CM4xx
* Andina Core: RISC-V
* Ambiqmicro: Apollo MCU
* ARM: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/a15/a5/A7/A8/A9/A5x 64-bi/A7X a 64 bit/R4/R5, TrustZone ARMv8-M
* Cadenza: Xtensa, diamante
* CEVA: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WICED WiFi
* Cypress: RISC-V
* Silice: eSi-RISC
* Infineon: XMC1000, XMC4000, Tricore
* Intel & Intel FPGA: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10
* Microchip: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32
* Microsemi: RISC-V
* NXP: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4
* Renesas: SH, HS, V850, RX, RZ, Synergy
* Laboratori siliconici: EFM32
* Synopsys: ARC 600, 700, ARC EM, ARC HS
* ST: STM32, ARM7, ARM9, Cortex-M3/M4/M7
* TL: C5xxx, C6xxx, Stellaris, Sitara, tiva-C
* Elaborazione Wave: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class
* Xilinx: Microblaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE

## <a name="supports-most-popular-tools"></a>Supporta gli strumenti più diffusi

Azure RTO ThreadX supporta gli strumenti di sviluppo embedded più diffusi, tra cui il™ Embedded Workbench di IAR, che include anche la maggior parte delle funzionalità di riconoscimento del kernel Azure RTO ThreadX più complete. L'integrazione di strumenti aggiuntivi include GNU (GCC), ARM DS-5/uVision®, Green Hills multi®, Wind River Workbench™, Imagine codescape, Renesas e2studio, Metaware As™, NXP CodeWarrior, Lauterbach TRACE32®, TI Code-Composer studio, CrossCore e tutti i dispositivi analoghi.
