---
title: Capitolo 3 - Componenti funzionali di Azure RTOS ThreadX SMP
description: Questo capitolo contiene una descrizione delle prestazioni elevate Azure RTOS kernel SMP ThreadX dal punto di vista funzionale.
author: philmea
ms.author: philmea
ms.date: 06/04/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 04676491f8ccaa98fa9ad396c221c38901c188b420ed710da3c96d863b49e6c5
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116799254"
---
# <a name="chapter-3---functional-components-of-azure-rtos-threadx-smp"></a>Capitolo 3 - Componenti funzionali di Azure RTOS ThreadX SMP

Questo capitolo contiene una descrizione delle prestazioni elevate Azure RTOS kernel SMP ThreadX dal punto di vista funzionale. Ogni componente funzionale viene presentato in modo facile da comprendere.

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Esistono quattro tipi di esecuzione del programma all'interno di un'applicazione ThreadX SMP: inizializzazione, esecuzione di thread, routine del servizio di interruzione (ISR) e timer dell'applicazione.

La figura 1 a pagina 45 mostra ogni tipo diverso di esecuzione del programma. Informazioni più dettagliate su ognuno di questi tipi sono disponibili nelle sezioni successive di questo capitolo.

### <a name="initialization"></a>Inizializzazione
Come suggerisce il nome, si tratta del primo tipo di esecuzione del programma in un'applicazione ThreadX SMP. L'inizializzazione include tutta l'esecuzione del programma tra la reimpostazione del processore e il punto di ingresso del *ciclo di pianificazione dei thread.*

> [!IMPORTANT]
> L'inizializzazione viene eseguita da o avviata dal core 0, che è il core in esecuzione predefinito dopo la reimpostazione.

### <a name="thread-execution"></a>Esecuzione di thread
Al termine dell'inizializzazione, ogni core che esegue ThreadX SMP entra nel ciclo di pianificazione dei thread. Il ciclo di pianificazione cerca un thread dell'applicazione pronto per l'esecuzione in tale core. Quando viene trovato un thread pronto, ThreadX SMP trasferisce il controllo a esso. Al termine del thread (o quando un altro thread con priorità più alta diventa pronto), l'esecuzione viene tornata al ciclo di pianificazione dei thread per trovare il successivo thread pronto con priorità più alta in ogni core.

Questo processo di esecuzione continua e pianificazione dei thread è il tipo più comune di esecuzione del programma nelle applicazioni ThreadX SMP.

![Esecuzione di thread](media/image4.png)

**FIGURA 1. Tipi di esecuzione del programma**

### <a name="interrupt-service-routines-isr"></a>Routine di servizio di interrupt (ISR)
Gli interrupt sono il fondamento dei sistemi in tempo reale. Senza interruzioni sarebbe estremamente difficile rispondere ai cambiamenti nel mondo esterno in modo corretto. Al rilevamento di un interrupt, il processore salva le informazioni chiave sull'esecuzione corrente del programma (in genere nello stack), quindi trasferisce il controllo a un'area di programma predefinita. Questa area di programma predefinita è comunemente chiamata routine di servizio di interrupt.

Nella maggior parte dei casi, gli interrupt si verificano durante l'esecuzione del thread (o nel ciclo di pianificazione dei thread). Tuttavia, gli interrupt possono verificarsi anche all'interno di un ISR in esecuzione o di un timer dell'applicazione.

Tutti i core sono autorizzati a elaborare gli interrupt. Il mapping degli interrupt ai core è sotto il controllo diretto dell'applicazione. L'interrupt del timer SMP ThreadX viene assegnato per impostazione predefinita al core 0 per l'elaborazione. Vedere il codice in *tx_timer_interrupt. S* per l'implementazione di questa assegnazione.

### <a name="application-timers"></a>Timer dell'applicazione
I timer dell'applicazione sono simili agli ISR, ad eccezione del fatto che l'implementazione dell'hardware (in genere viene usato un singolo interrupt hardware periodico) è nascosta all'applicazione. Tali timer vengono usati dalle applicazioni per eseguire timeout, periodici e/o servizi watchdog. Proprio come gli ISR, i timer dell'applicazione spesso interrompno l'esecuzione del thread. A differenza degli ISR, tuttavia, i timer dell'applicazione non possono interrompersi a vicenda.

> [!NOTE]
> Come i thread, i timer dell'applicazione possono essere esclusi dall'esecuzione in qualsiasi core.

## <a name="memory-usage"></a>Utilizzo memoria

ThreadX SMP risiede insieme al programma dell'applicazione. Di conseguenza, l'utilizzo della memoria statica (o della memoria fissa) di ThreadX SMP è determinato dagli strumenti di sviluppo. ad esempio il compilatore, il linker e il localizzatore. L'utilizzo della memoria dinamica (o della memoria di run-time) è sotto il controllo diretto dell'applicazione.

> [!NOTE]
> Tutta la memoria a cui accede ThreadX SMP deve essere coerente con la cache e accessibile da tutti i core che eseguono ThreadX SMP.

### <a name="static-memory-usage"></a>Utilizzo della memoria statica
La maggior parte degli strumenti di sviluppo suddivide l'immagine del programma dell'applicazione in cinque aree di base: *istruzione*, *costante* *,* dati inizializzati, dati non *inizializzati* e *stack di sistema*. La figura 2 a pagina 47 illustra un esempio di queste aree di memoria.

![Utilizzo della memoria statica](media/image5.png)

**FIGURA 2. Esempio di area di memoria**

È importante comprendere che si tratta solo di un esempio. Il layout effettivo della memoria statica è specifico del processore, degli strumenti di sviluppo e dell'hardware sottostante.

L'area delle istruzioni contiene tutte le istruzioni del processore del programma. Questa area è in genere la più grande e si trova spesso nella ROM.

L'area costante contiene varie costanti compilate, incluse le stringhe definite o a cui si fa riferimento all'interno del programma. Questa area contiene anche la "copia iniziale" dell'area dati inizializzata. Durante il processo di inizializzazione del compilatore, questa parte dell'area costante viene usata per configurare l'area dati inizializzata nella RAM. L'area costante in genere segue l'area di istruzioni e si trova spesso nella ROM.

I dati inizializzati e le aree dati non inizializzate contengono tutte le variabili globali e statiche. Queste aree si trovano sempre nella RAM.

Lo stack di sistema viene in genere configurato immediatamente dopo le aree dati inizializzate e non inizializzate. Lo stack di sistema viene usato dal compilatore durante l'inizializzazione, quindi da ThreadX SMP durante l'inizializzazione e, successivamente, nell'elaborazione ISR.

### <a name="dynamic-memory-usage"></a>memoria dinamica utilizzo
Come accennato in precedenza, l'utilizzo dinamico della memoria è sotto il controllo diretto dell'applicazione. I blocchi di controllo e le aree di memoria associati a stack, code e pool di memoria possono essere posizionati in qualsiasi punto dello spazio di memoria della destinazione. Si tratta di una funzionalità importante perché facilita l'utilizzo facile di diversi tipi di memoria fisica.

Si supponga, ad esempio, che un ambiente hardware di destinazione abbia sia memoria veloce che memoria lenta. Se l'applicazione necessita di prestazioni aggiuntive per un thread ad alta priorità, il blocco di controllo (TX_THREAD) e lo stack possono essere inseriti nell'area di memoria veloce, che può migliorare notevolmente le prestazioni.

## <a name="initialization"></a>Inizializzazione 
Comprendere il processo di inizializzazione è importante. L'ambiente hardware iniziale è configurato qui. Questo è anche il punto in cui all'applicazione viene data la sua personalità iniziale.

> [!IMPORTANT]
> ThreadX SMP tenta di utilizzare (quando possibile) il processo di inizializzazione completo dello strumento di sviluppo. In questo modo sarà più semplice eseguire l'aggiornamento alle nuove versioni degli strumenti di sviluppo in futuro.

### <a name="system-reset-vector"></a>Vettore di reimpostazione del sistema 
Tutti i microprocessori hanno logica di reimpostazione. Quando si verifica una reimpostazione (hardware o software), l'indirizzo del punto di ingresso dell'applicazione viene recuperato da un percorso di memoria specifico. Dopo il recupero del punto di ingresso, il processore trasferisce il controllo a tale posizione. 

Il punto di ingresso dell'applicazione è spesso scritto nel linguaggio assembly nativo e viene in genere fornito dagli strumenti di sviluppo (almeno in formato modello). In alcuni casi, viene fornita una versione speciale del programma di ingresso con ThreadX SMP. 

### <a name="development-tool-initialization"></a>Inizializzazione dello strumento di sviluppo
Al termine dell'inizializzazione di basso livello, il controllo trasferisce all'inizializzazione di alto livello dello strumento di sviluppo. Questa è in genere la posizione in cui vengono impostate le variabili C statiche e globali inizializzate. Tenere presente che i valori iniziali vengono recuperati dall'area costante. L'elaborazione esatta dell'inizializzazione è specifica dello strumento di sviluppo.

### <a name="main-function"></a>Funzione main 
Al termine dell'inizializzazione dello strumento di sviluppo, il controllo trasferisce alla funzione main fornita *dall'utente.* A questo punto, l'applicazione controlla cosa accade dopo. Per la maggior parte delle applicazioni, la funzione main chiama *tx_kernel_enter*, che è la voce in ThreadX SMP. Tuttavia, le applicazioni possono eseguire l'elaborazione preliminare (in genere per l'inizializzazione hardware) prima di immettere ThreadX SMP.

> [!IMPORTANT]
> La chiamata a tx_kernel_enter non restituisce , pertanto non inserire alcuna elaborazione dopo di essa.

### <a name="tx_kernel_enter"></a>tx_kernel_enter 
La funzione entry coordina l'inizializzazione di varie strutture di dati SMP ThreadX interne e quindi chiama la funzione di definizione *dell'applicazione tx_application_define*.

Quando *tx_application_define* viene restituito, il controllo viene trasferito al ciclo di pianificazione dei thread. Questo contrassegna la fine dell'inizializzazione.

### <a name="application-definition-function"></a>Funzione di definizione dell'applicazione
La *tx_application_define* definisce tutti i thread iniziali dell'applicazione, le code, i semafori, i mutex, i flag di evento, i pool di memoria e i timer. È anche possibile creare ed eliminare risorse di sistema dai thread durante il normale funzionamento dell'applicazione. Tuttavia, tutte le risorse iniziali dell'applicazione sono definite qui.

La *tx_application_define* ha un singolo parametro di input ed è sicuramente opportuno menzionarla. Il *primo indirizzo* RAM disponibile è l'unico parametro di input per questa funzione. Viene in genere usato come punto di partenza per allocazioni iniziali di memoria in fase di esecuzione di stack di thread, code e pool di memoria.

> [!IMPORTANT]
> Al termine dell'inizializzazione, solo un thread in esecuzione può creare ed eliminare risorse di sistema, inclusi altri thread. È pertanto necessario creare almeno un thread durante l'inizializzazione.

### <a name="interrupts"></a>Interrompe 
Gli interrupt vengono lasciati disabilitati durante l'intero processo di inizializzazione. Se l'applicazione abilita in qualche modo gli interrupt, può verificarsi un comportamento imprevedibile. La figura 3 a pagina 52 illustra l'intero processo di inizializzazione, dalla reimpostazione del sistema all'inizializzazione specifica dell'applicazione.

## <a name="thread-execution"></a>Esecuzione di thread

La pianificazione e l'esecuzione di thread dell'applicazione è l'attività più importante di ThreadX SMP. Un thread viene in genere definito come segmento di programma semi-indipendente con uno scopo dedicato. L'elaborazione combinata di tutti i thread rende un'applicazione.

I thread vengono creati dinamicamente *chiamando* tx_thread_create durante l'inizializzazione o durante l'esecuzione del thread. I thread vengono creati in *uno stato pronto* o *sospeso.*

![Processo di inizializzazione SMP](media/image6.png)

**FIGURA 3. Processo di inizializzazione SMP**

### <a name="thread-execution-states"></a>Stati di esecuzione dei thread  
La comprensione dei diversi stati di elaborazione dei thread è un elemento chiave per comprendere l'intero ambiente multithreading. In ThreadX SMP sono presenti cinque stati di thread distinti: *ready*, *suspended*, *executing,* *terminated* e *completed*. La figura 4 illustra il diagramma di transizione dello stato del thread per ThreadX SMP.

![Stati di esecuzione dei thread](media/image7.png)

**FIGURA 4. Transizione dello stato del thread**

Un thread è in *uno stato pronto* quando è pronto per l'esecuzione. Un thread pronto non viene eseguito fino a quando non è il thread con priorità più alta nello stato pronto. In questo caso, ThreadX SMP esegue il thread, che ne modifica lo stato in *esecuzione.*

Se un thread con priorità più alta diventa pronto, il thread in esecuzione torna a *uno stato* pronto. Viene quindi eseguito il thread ad alta priorità appena pronto, che modifica lo stato logico in *esecuzione*. Questa transizione tra *stati pronti* *ed in* esecuzione si verifica ogni volta che si verifica la preemption del thread.

In un determinato momento, solo un thread si trova in *uno stato di esecuzione.* Ciò è dovuto al fatto che un thread nello *stato di* esecuzione ha il controllo del processore sottostante.

I thread in *stato sospeso* non sono idonei per l'esecuzione. I motivi per  cui lo stato è sospeso includono la sospensione per tempo, messaggi della coda, semafori, mutex, flag di evento, memoria e sospensione di thread di base. Dopo la rimozione della causa della sospensione, il thread viene riposto in *uno stato pronto.*

Un thread in stato *completato è* un thread che ha completato l'elaborazione e restituito dalla funzione di ingresso. La funzione entry viene specificata durante la creazione del thread. Un thread in stato *completato non può* essere eseguito di nuovo.

Un thread è in uno *stato terminato* perché un altro thread o il thread stesso ha chiamato il *tx_thread_terminate* servizio. Un thread in uno *stato terminato non può* essere eseguito di nuovo.

> [!IMPORTANT]
> Se si desidera avviare nuovamente un thread completato o terminato, l'applicazione deve prima eliminare il thread. Può quindi essere ri-creato e ri-avviato.

### <a name="thread-entryexit-notification"></a>Notifica di ingresso/uscita del thread  
Alcune applicazioni possono risultare vantaggiose ricevere una notifica quando un thread specifico viene immesso per la prima volta, quando viene completato o viene terminato. ThreadX SMP offre questa funzionalità tramite il *tx_thread_entry_exit_notify* di rete. Questo servizio registra una funzione di notifica dell'applicazione per un thread specifico, che viene chiamato da ThreadX SMP ogni volta che il thread viene avviato, completato o terminato. Dopo la chiamata, la funzione di notifica dell'applicazione può eseguire l'elaborazione specifica dell'applicazione. Ciò comporta in genere la notifica dell'evento a un altro thread dell'applicazione tramite una primitiva di sincronizzazione SMP ThreadX.

### <a name="thread-priorities"></a>Priorità dei thread  
Come accennato in precedenza, un thread è un segmento di programma semi-indipendente con uno scopo dedicato. Tuttavia, tutti i thread non vengono creati uguali. Lo scopo dedicato di alcuni thread è molto più importante di altri. Questo tipo eterogeneo di importanza dei thread è un segno distintivo delle applicazioni in tempo reale incorporate.

ThreadX SMP determina l'importanza di un thread quando viene creato assegnando un valore numerico che rappresenta la *priorità*. Il numero massimo di priorità SMP ThreadX è configurabile da 32 a 1024 in incrementi di 32. Il numero massimo effettivo di priorità è determinato dalla *costante TX_MAX_PRIORITIES* durante la compilazione della libreria ThreadX SMP. La presenza di un numero maggiore di priorità non aumenta significativamente il sovraccarico di elaborazione. Tuttavia, per ogni gruppo di 32 livelli di priorità sono necessari altri 128 byte di RAM per gestirli. Ad esempio, 32 livelli di priorità richiedono 128 byte di RAM, 64 livelli di priorità richiedono 256 byte di RAM e 96 livelli di priorità richiedono 384 byte di RAM.

Per impostazione predefinita, ThreadX SMP ha 32 livelli di priorità, che vanno dalla priorità 0 alla priorità 31.

I valori numericamente più piccoli implicano una priorità più alta. Di conseguenza, la priorità 0 rappresenta la priorità più alta, mentre la priorità *(TX_MAX_PRIORITIES*-1) rappresenta la priorità più bassa.

Più thread possono avere la stessa priorità basandosi sulla pianificazione cooperativa o sulla sezione temporale. Inoltre, le priorità dei thread possono essere modificate durante la fase di esecuzione.

### <a name="thread-scheduling"></a>Pianificazione dei thread 
ThreadX SMP pianifica i thread in base alla priorità. Il thread pronto con la priorità più alta viene eseguito per primo. Se sono pronti più thread con la stessa priorità, vengono eseguiti in modalità FIFO *(First-In-First-Out).*

Per impostazione predefinita, ThreadX SMP pianifica i thread con priorità più alta "n" nei processori disponibili "n". Se l'elaborazione simultanea è necessaria solo per i thread pronti con  la stessa priorità, la libreria SMP ThreadX deve essere compilata TX_THREAD_SMP_EQUAL_PRIORITY definita.

> [!NOTE]
> Per impostazione predefinita, tutti i thread possono essere eseguiti solo nel core 0, compilando la libreria ThreadX SMP **con** TX_THREAD_SMP_ONLY_CORE_0_DEFAULT definito.

### <a name="round-robin-scheduling"></a>Pianificazione round robin  
ThreadX SMP supporta la *pianificazione round robin* di più thread con la stessa priorità. Questa operazione viene eseguita tramite chiamate cooperativi *a tx_thread_relinquish*. Questo servizio offre a tutti gli altri thread pronti con la stessa priorità la possibilità di essere eseguiti *prima che* il tx_thread_relinquish chiamante venga eseguito di nuovo.

### <a name="time-slicing"></a>Time-Slicing 
*La sezione temporale è* un'altra forma di pianificazione round robin. Un intervallo di tempo specifica il numero massimo di tick timer (interrupt timer) che un thread può eseguire senza rinunciare al processore. In ThreadX SMP la sezione temporale è disponibile in base al perthreading. La sezione temporale del thread viene assegnata durante la creazione e può essere modificata durante la fase di esecuzione. Alla scadenza di un intervallo di tempo, tutti gli altri thread pronti dello stesso livello di priorità hanno la possibilità di essere eseguiti prima che il thread con intervallo di tempo venga eseguito di nuovo.

Un nuovo intervallo di tempo del thread viene assegnato a un thread dopo la sospensione, la rinuncia, la chiamata al servizio ThreadX SMP che causa la preemption o viene a sua volta suddiviso in più volte.

Quando un thread con intervallo di tempo viene preempted, riprende prima di altri thread pronti con uguale priorità per il resto della relativa sezione temporale.

> [!IMPORTANT]
> L'uso della sezione temporale comporta un leggero sovraccarico del sistema. Poiché la sezione temporale è utile solo nei casi in cui più thread condividono la stessa priorità, ai thread con una priorità univoca non deve essere assegnato un intervallo di tempo.

### <a name="preemption"></a>Precedenza 
La precedenza è il processo di interruzione temporanea di un thread in esecuzione a favore di un thread con priorità più alta. Questo processo non è visibile al thread in esecuzione. Al termine del thread con priorità più alta, il controllo viene trasferito di nuovo nella posizione esatta in cui si è verificata la precedenza.

Si tratta di una funzionalità molto importante nei sistemi in tempo reale perché facilita la risposta rapida agli eventi importanti dell'applicazione. Anche se una funzionalità molto importante, la precedenza può anche essere un'origine di un'ampia gamma di problemi, tra cui la carestia, l'overhead eccessivo e l'inversione della priorità.

### <a name="preemption-threshold"></a>Soglia di preemption™ 
Per facilitare alcuni dei problemi intrinseci di preemption, ThreadX SMP offre una funzionalità univoca e avanzata denominata *preemption-threshold.*

Una soglia di precedenza consente a un  thread di specificare un limite di priorità per la disabilitazione della precedenza. I thread con priorità più elevate rispetto al limite massimo possono comunque essere pre-autorizzati, mentre quelli inferiori al limite massimo non possono essere pre-autorizzati.

Si supponga, ad esempio, che un thread con priorità 20 interagisca solo con un gruppo di thread con priorità compresa tra 15 e 20. Durante le sezioni critiche, il thread con priorità 20 può impostare la soglia di precedenza su 15, impedendo così la precedenza da tutti i thread con cui interagisce. Ciò consente ancora ai thread molto importanti (priorità compresa tra 0 e 14) di predilire questo thread durante l'elaborazione della sezione critica, con un'elaborazione molto più reattiva.

Naturalmente, è comunque possibile che un thread disabiliti tutte le preemption impostandone la soglia di preemption su 0. Inoltre, è possibile modificare preemption-threshold durante la fase di esecuzione.

> [!IMPORTANT]
> L'uso di preemption-threshold disabilita la sezione temporale per il thread specificato.

### <a name="priority-inheritance"></a>Ereditarietà delle priorità 
ThreadX SMP supporta anche l'ereditarietà della priorità facoltativa all'interno dei servizi mutex descritti più avanti in questo capitolo. L'ereditarietà della priorità consente a un thread con priorità inferiore di presupporre temporaneamente la priorità di un thread con priorità alta in attesa di un mutex di proprietà del thread con priorità inferiore. Questa funzionalità consente all'applicazione di evitare l'inversione di priorità non deterministica eliminando la precedenza delle priorità intermedie dei thread. Naturalmente, *è possibile usare preemption-threshold* per ottenere un risultato simile.

### <a name="thread-creation"></a>Creazione di thread 
I thread dell'applicazione vengono creati durante l'inizializzazione o durante l'esecuzione di altri thread dell'applicazione. Non esiste alcun limite al numero di thread che possono essere creati da un'applicazione.

### <a name="thread-control-block-tx_thread"></a>Blocco di controllo thread TX_THREAD 
Le caratteristiche di ogni thread sono contenute nel relativo blocco di controllo. Questa struttura è definita nel file ***tx_api.h.***

Il blocco di controllo di un thread può trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione.

L'individuazione del blocco di controllo in altre aree richiede un po' più attenzione, proprio come tutta la memoria allocata dinamicamente. Se un blocco di controllo viene allocato all'interno di una funzione C, la memoria associata fa parte dello stack del thread chiamante. In generale, evitare di usare l'archiviazione locale per i blocchi di controllo perché, dopo il ritorno della funzione, viene rilasciato tutto lo spazio dello stack della variabile locale, indipendentemente dal fatto che sia in uso da un altro thread per un blocco di controllo.

Nella maggior parte dei casi, l'applicazione non è conforme al contenuto del blocco di controllo del thread. Esistono tuttavia alcune situazioni, in particolare durante il debug, in cui è utile guardare determinati membri. Di seguito sono riportati alcuni dei membri del blocco di controllo più utili:

- **tx_thread_run_count** contiene un contatore del numero di volte in cui il thread è stato pianificato. Un contatore crescente indica che il thread è in corso di pianificazione ed esecuzione.

- **tx_thread_state** contiene lo stato del thread associato. Di seguito sono elencati i possibili stati dei thread:

    - TX_READY(0x00)
    - TX_COMPLETED(0x01)
    - TX_TERMINATED(0x02)
    - TX_SUSPENDED(0x03)
    - TX_SLEEP(0x04)
    - TX_QUEUE_SUSP(0x05)
    - TX_SEMAPHORE_SUSP(0x06)
    - TX_EVENT_FLAG (0x07)
    - TX_BLOCK_MEMORY(0x08)
    - TX_BYTE_MEMORY (0x09)
    - TX_MUTEX_SUSP(0x0D)

> [!IMPORTANT]
> Naturalmente esistono molti altri campi interessanti nel blocco di controllo del thread, tra cui il puntatore dello stack, il valore dell'intervallo di tempo, le priorità e così via. Gli utenti sono invitati a esaminare i membri del blocco di controllo, ma le modifiche sono rigorosamente vietate.

> [!IMPORTANT]
> Lo stato di "esecuzione" indicato in precedenza in questa sezione non è lo stesso. Non è necessario perché è presente un solo thread in esecuzione in un determinato momento. Anche lo stato di un thread in esecuzione è ***TX_READY***.

### <a name="currently-executing-thread"></a>Thread attualmente in esecuzione 
Come accennato in precedenza, è presente un solo thread in esecuzione in un determinato momento. Esistono diversi modi per identificare il thread in esecuzione, a seconda del thread che effettua la richiesta.

Un segmento di programma può ottenere l'indirizzo del blocco di controllo del thread in ***esecuzione chiamando tx_thread_identify***. Ciò è utile nelle parti condivise del codice dell'applicazione eseguite da più thread.

Nelle sessioni di debug gli utenti possono esaminare la matrice di puntatori SMP ThreadX ***interna _tx_thread_current_ptr[core]***. Contiene l'indirizzo del blocco di controllo del thread attualmente in esecuzione. Se questo puntatore è NULL, non è in esecuzione alcun thread dell'applicazione; Ad esempio, ThreadX SMP è in attesa nel proprio ciclo di pianificazione che un thread diventi pronto.

### <a name="thread-stack-area"></a>Thread Stack Area 
Ogni thread deve avere un proprio stack per salvare il contesto dell'ultima esecuzione e dell'uso del compilatore. La maggior parte dei compilatori C usa lo stack per effettuare chiamate di funzione e allocare temporaneamente variabili locali. La figura 5 a pagina 61 mostra lo stack di un thread tipico.

![Thread Stack Area](media/image8.png)

**FIGURA 5. Stack di thread tipico**

Il punto in cui uno stack di thread si trova in memoria è l'applicazione. L'area dello stack viene specificata durante la creazione del thread e può trovarsi in qualsiasi punto dello spazio indirizzi della destinazione. Si tratta di una funzionalità importante perché consente alle applicazioni di migliorare le prestazioni dei thread importanti inserendo il proprio stack nella RAM ad alta velocità.

La dimensione di uno stack è una delle domande più frequenti sui thread. L'area dello stack di un thread deve essere sufficientemente grande da contenere l'annidamento delle chiamate di funzione nel peggiore dei casi, l'allocazione delle variabili locali e il salvataggio dell'ultimo contesto di esecuzione.

La dimensione minima dello stack, **TX_MINIMUM_STACK**, è definita da ThreadX SMP. Uno stack di queste dimensioni supporta il salvataggio del contesto di un thread e la quantità minima di chiamate di funzione e l'allocazione delle variabili locali.

Per la maggior parte dei thread, tuttavia, le dimensioni minime dello stack sono troppo ridotte e l'utente deve verificare il requisito delle dimensioni peggiori esaminando l'annidamento delle chiamate di funzione e l'allocazione delle variabili locali. Naturalmente, è sempre meglio iniziare con un'area dello stack più grande.

Dopo il debug dell'applicazione, è possibile ottimizzare le dimensioni dello stack di thread se la memoria è insufficiente. Uno dei preferiti è quello di impostare tutte le aree dello stack con un modello di dati facilmente identificabile, ad esempio (0xEFEF) prima di creare i thread. Dopo aver esaminato accuratamente l'applicazione, è possibile esaminare le aree dello stack per verificare la quantità di stack effettivamente usata individuando l'area dello stack in cui il modello di dati è ancora intatto. La figura 6 mostra un set di impostazioni dello stack da 0xEFEF dopo l'esecuzione completa dei thread.

> [!IMPORTANT]
> Per impostazione predefinita, ThreadX SMP inizializza ogni byte di ogni stack di thread con il valore 0xEF.

### <a name="memory-pitfalls"></a>Problemi di memoria 
I requisiti dello stack per i thread possono essere di grandi dimensioni. È quindi importante progettare l'applicazione in modo che abbia un numero ragionevole di thread. È inoltre necessario fare attenzione a evitare un utilizzo eccessivo dello stack all'interno dei thread. È consigliabile evitare algoritmi ricorsivi e strutture di dati locali di grandi dimensioni.

Nella maggior parte dei casi, uno stack in overflow causa il danneggiamento della memoria adiacente da parte dell'esecuzione del thread (in genere 

![Problemi di memoria](media/image9.png)

**FIGURA 6. Stack Preset su 0xEFEF**

prima) l'area dello stack. I risultati sono imprevedibili, ma nella maggior parte dei casi comportano una modifica non naturale del contatore del programma. Questa operazione viene spesso definita "salto nelle alci". Naturalmente, l'unico modo per evitare questo problema è garantire che tutti gli stack di thread siano sufficientemente grandi.

### <a name="optional-run-time-stack-checking"></a>Controllo dello stack di run-time facoltativo  
ThreadX SMP offre la possibilità di controllare il danneggiamento dello stack di ogni thread in fase di esecuzione. Per impostazione predefinita, ThreadX SMP riempie ogni byte di stack di thread con un modello 0xEF dati durante la creazione. Se l'applicazione compila la libreria ThreadX SMP con ***TX_ENABLE_STACK_CHECKING** _ definito, ThreadX SMP esaminerà lo stack di ogni thread per verificarne il danneggiamento quando viene sospeso o ripreso. Se viene rilevato un danneggiamento dello stack, ThreadX SMP chiamerà la routine di gestione degli errori dello stack dell'applicazione come specificato dalla chiamata a _tx_thread_stack_error_notify*. In caso contrario, se non è stato specificato alcun gestore degli errori dello stack, ThreadX SMP chiamerà la routine _tx_thread_stack_error_handler *interna.*

### <a name="reentrancy"></a>Rientranza 
Una delle realtà del multithreading è che la stessa funzione C può essere chiamata da più thread. Ciò offre una potenza eccezionale e consente anche di ridurre lo spazio del codice. Tuttavia, richiede che le funzioni C chiamate da più thread siano *rientranti.*

In pratica, una funzione rientrante archivia l'indirizzo del mittente del chiamante nello stack corrente e non si basa su variabili C globali o statiche impostate in precedenza. La maggior parte dei compilatori posiziona l'indirizzo del mittente nello stack. Di conseguenza, gli sviluppatori di applicazioni devono preoccuparsi solo dell'uso *di variabili globali* e *statiche.*

Un esempio di funzione non rientrante è la funzione token di stringa "strtok" disponibile nella libreria C standard. Questa funzione memorizza il puntatore di stringa precedente nelle chiamate successive. Esegue questa operazione con un puntatore di stringa statico. Se questa funzione viene chiamata da più thread, probabilmente restituirebbe un puntatore non valido.

### <a name="thread-priority-pitfalls"></a>Insidie della priorità dei thread 
La selezione delle priorità dei thread è uno degli aspetti più importanti del multithreading. Talvolta è molto allettante assegnare priorità in base a una nozione percepita di importanza dei thread anziché determinare cosa è esattamente necessario in fase di esecuzione. L'uso improprio delle priorità dei thread può affamare altri thread, creare inversione della priorità, ridurre la larghezza di banda di elaborazione e rendere difficile la comprensione del comportamento in fase di esecuzione dell'applicazione.

Come accennato in precedenza, ThreadX SMP fornisce un algoritmo di pianificazione preemptive basato sulla priorità. I thread con priorità più bassa non vengono eseguiti finché non sono disponibili thread con priorità più alta pronti per l'esecuzione. Se un thread con priorità più alta è sempre pronto, i thread con priorità più bassa non vengono mai eseguiti. Questa condizione è detta *thread starvation.*

La maggior parte dei problemi di affamazione di thread viene rilevata nelle prime fasi del debug e può essere risolta assicurando che i thread con priorità più alta non vengono eseguiti in modo continuo. In alternativa, è possibile aggiungere all'applicazione la logica che aumenta gradualmente la priorità dei thread senza utilizzo di dati fino a quando non hanno la possibilità di essere eseguiti.

Un altro insidie associato alle priorità dei thread è *l'inversione della priorità*. L'inversione della priorità si verifica quando un thread con priorità più alta viene sospeso perché un thread con priorità più bassa ha una risorsa necessaria. Naturalmente, in alcuni casi è necessario che due thread con priorità diversa convivino una risorsa comune. Se questi thread sono gli unici attivi, il tempo di inversione della priorità è delimitato dal tempo in cui il thread con priorità inferiore contiene la risorsa. Questa condizione è sia deterministica che piuttosto normale. Tuttavia, se i thread con priorità intermedia diventano attivi durante questa condizione di inversione della priorità, il tempo di inversione della priorità non è più deterministico e potrebbe causare un errore dell'applicazione.

Esistono principalmente tre metodi distinti per impedire l'inversione della priorità non deterministica in ThreadX SMP. In primo luogo, le selezioni della priorità dell'applicazione e il comportamento in fase di esecuzione possono essere progettati in modo da impedire il problema di inversione della priorità. In secondo momento, i thread con priorità più bassa possono usare *la* soglia di precedenza per bloccare la precedenza dai thread intermedi mentre condividono le risorse con thread con priorità più alta. Infine, i thread che usano oggetti mutex SMP ThreadX per proteggere le risorse di sistema possono usare l'ereditarietà della priorità *mutex* facoltativa per eliminare l'inversione della priorità non deterministica.

### <a name="priority-overhead"></a>Sovraccarico di priorità 
Uno dei modi più trascurati per ridurre il sovraccarico nel multithreading è ridurre il numero di commutatori di contesto. Come accennato in precedenza, un cambio di contesto si verifica quando l'esecuzione di un thread con priorità più alta è preferita rispetto a quella del thread in esecuzione. È opportuno ricordare che i thread con priorità più alta possono diventare pronti in seguito a eventi esterni (ad esempio interrupt) e da chiamate al servizio effettuate dal thread in esecuzione.

Per illustrare gli effetti delle priorità dei thread sull'overhead del cambio di contesto, si supponga un ambiente a tre thread con thread denominati *thread_1*, *thread_2* e *thread_3*. Si supponga inoltre che tutti i thread siano in uno stato di sospensione in attesa di un messaggio. Quando thread_1 riceve un messaggio, lo inoltra immediatamente thread_2. Thread_2 quindi inoltra il messaggio a thread_3. Thread_3 rimuove semplicemente il messaggio. Dopo che ogni thread elabora il messaggio, torna indietro e attende un altro messaggio.

L'elaborazione necessaria per eseguire questi tre thread varia notevolmente a seconda delle priorità. Se tutti i thread hanno la stessa priorità, si verifica un singolo cambio di contesto prima dell'esecuzione di ogni thread. Il cambio di contesto si verifica quando ogni thread viene sospeso in una coda di messaggi vuota.

Tuttavia, se thread_2 ha una priorità più alta rispetto thread_1 e thread_3 ha una priorità più alta rispetto thread_2, il numero di commutatori di contesto raddoppia. Ciò è dovuto al fatto che un altro cambio di contesto si verifica all'interno *del tx_queue_send* quando rileva che un thread con priorità più alta è pronto.

Il meccanismo di soglia di precedenza SMP ThreadX può evitare questi commutatori di contesto aggiuntivi e consentire comunque le selezioni di priorità indicate in precedenza. Si tratta di una funzionalità importante perché consente diverse priorità dei thread durante la pianificazione, eliminando al tempo stesso alcuni dei contesti indesiderati che passano da uno all'altro durante l'esecuzione del thread.

### <a name="run-time-thread-performance-information"></a>Informazioni sulle prestazioni dei thread di run-time 
ThreadX SMP fornisce informazioni facoltative sulle prestazioni dei thread di run-time. Se la libreria e l'applicazione ThreadX SMP vengono compilate ***TX_THREAD_ENABLE_PERFORMANCE_INFO,*** ThreadX SMP accumula le informazioni seguenti:

Numero totale per il sistema complessivo:

- ritorsioni di thread
- sospensioni di thread
- preemptions delle chiamate di servizio
- interrupt preemptions
- inversione di priorità
- time-slices
- relinquishes
- timeout dei thread
- sospensioni interrotte
- inattività del sistema
- restituisce un sistema non inattivo

Numero totale per ogni thread:

- Riprese
- Sospensioni
- preemptions delle chiamate di servizio
- interrupt preemptions
- inversione di priorità
- time-slices
- thread relinquishes
- timeout dei thread
- sospensioni interrotte

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi *tx_thread_performance_info_get* e *tx_thread_performance_system_info_get*. Le informazioni sulle prestazioni dei thread sono utili per determinare se l'applicazione funziona correttamente. È anche utile per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di preemption delle chiamate al servizio potrebbe suggerire che la priorità del thread e/o la soglia di precedenza sia troppo bassa. Inoltre, un numero relativamente basso di valori restituiti dal sistema inattivi potrebbe suggerire che i thread con priorità più bassa non vengono sospesi in modo sufficiente.

### <a name="debugging-pitfalls"></a>Problemi di debug 
Il debug di applicazioni multithreading è un po' più difficile perché lo stesso codice di programma può essere eseguito da più thread. In questi casi, un punto di interruzione da solo potrebbe non essere sufficiente. Il debugger deve anche visualizzare la matrice di puntatori del thread ***corrente _tx_thread_current_ptr[core]*** usando un punto di interruzione condizionale per verificare se il thread chiamante è quello di cui eseguire il debug.

Gran parte di questo processo viene gestito in pacchetti di supporto multithreading offerti da diversi fornitori di strumenti di sviluppo. Grazie alla progettazione semplice, l'integrazione di ThreadX SMP con diversi strumenti di sviluppo è relativamente semplice.

La dimensione dello stack è sempre un argomento di debug importante nel multithreading. Ogni volta che viene osservato un comportamento inspiegabile, è in genere una buona prima ipotesi aumentare le dimensioni dello stack per tutti i thread, in particolare le dimensioni dello stack dell'ultimo thread da eseguire.

> [!IMPORTANT]
> È anche una buona idea creare la libreria ThreadX SMP con TX_ENABLE_STACK_CHECKING definiti. Ciò consente di isolare i problemi di danneggiamento dello stack il prima possibile durante l'elaborazione.

## <a name="message-queues"></a>Code di messaggi

Le code di messaggi sono il mezzo principale per la comunicazione interthread in ThreadX SMP. Uno o più messaggi possono trovarsi in una coda di messaggi. Una coda di messaggi che contiene un singolo messaggio viene comunemente chiamata cassetta *postale.*

I messaggi vengono copiati in una *coda tx_queue_send* e vengono copiati da una coda *tx_queue_receive*. L'unica eccezione è quando un thread viene sospeso durante l'attesa di un messaggio in una coda vuota. In questo caso, il messaggio successivo inviato alla coda viene inserito direttamente nell'area di destinazione del thread.

Ogni coda di messaggi è una risorsa pubblica. ThreadX SMP non pone vincoli sulla modalità di utilizzo delle code di messaggi.

### <a name="creating-message-queues"></a>Creazione di code di messaggi 
Le code di messaggi vengono create durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. Non esiste alcun limite al numero di code di messaggi in un'applicazione. 

### <a name="message-size"></a>Dimensioni del messaggio 
Ogni coda di messaggi supporta una serie di messaggi a dimensione fissa. Le dimensioni dei messaggi disponibili sono comprese tra 1 e 16 parole a 32 bit incluse. Le dimensioni del messaggio vengono specificate al momento della creazione della coda. 

I messaggi dell'applicazione con più di 16 parole devono essere passati dal puntatore . Questa operazione viene eseguita creando una coda con una dimensione del messaggio di 1 parola (sufficiente per contenere un puntatore) e quindi inviando e ricevendo puntatori al messaggio anziché l'intero messaggio.

### <a name="message-queue-capacity"></a>Capacità della coda di messaggi 
Il numero di messaggi che una coda può contenere è una funzione delle dimensioni dei messaggi e delle dimensioni dell'area di memoria fornita durante la creazione. La capacità totale dei messaggi della coda viene calcolata dividendo il numero di byte in ogni messaggio nel numero totale di byte nell'area di memoria fornita.

Ad esempio, se una coda di messaggi che supporta una dimensione del messaggio di 1 parola a 32 bit (4 byte) viene creata con un'area di memoria di 100 byte, la capacità sarà di 25 messaggi.

### <a name="queue-memory-area"></a>Area di memoria della coda 
Come accennato in precedenza, l'area di memoria per il buffering dei messaggi viene specificata durante la creazione della coda. Analogamente ad altre aree di memoria in ThreadX SMP, può trovarsi in qualsiasi punto dello spazio degli indirizzi della destinazione.

Si tratta di una funzionalità importante perché offre all'applicazione una notevole flessibilità. Ad esempio, un'applicazione potrebbe individuare l'area di memoria di una coda importante nella RAM ad alta velocità per migliorare le prestazioni.

### <a name="thread-suspension"></a>Sospensione dei thread  
I thread dell'applicazione possono essere sospesi durante il tentativo di inviare o ricevere un messaggio da una coda. In genere, la sospensione dei thread comporta l'attesa di un messaggio da una coda vuota. Tuttavia, è anche possibile che un thread sospende il tentativo di inviare un messaggio a una coda completa. 

Dopo aver risolto la condizione di sospensione, il servizio richiesto viene completato e il thread in attesa viene ripreso. Se più thread vengono sospesi nella stessa coda, vengono ripresi nell'ordine in cui sono stati sospesi (FIFO).

Tuttavia, la ripresa della priorità è possibile anche se l'applicazione chiama tx_queue_prioritize ***prima*** del servizio di accodamento che revoca la sospensione dei thread. Il servizio di assegnazione della priorità della coda posiziona il thread con priorità più alta all'inizio dell'elenco di sospensione, lasciando tutti gli altri thread sospesi nello stesso ordine FIFO.

I timeout sono disponibili anche per tutte le sospensioni della coda. Fondamentalmente, un timeout specifica il numero massimo di tick timer che il thread rimarrà sospeso. Se si verifica un timeout, il thread viene ripreso e il servizio viene restituito con il codice di errore appropriato.

### <a name="queue-send-notification"></a>Notifica di invio coda  
Alcune applicazioni possono risultare vantaggiose ricevere una notifica ogni volta che un messaggio viene inserito in una coda. ThreadX SMP offre questa possibilità tramite il *tx_queue_send_notify* di lavoro. Questo servizio registra la funzione di notifica dell'applicazione fornita con la coda specificata. ThreadX SMP richiama successivamente questa funzione di notifica dell'applicazione ogni volta che viene inviato un messaggio alla coda. L'elaborazione esatta all'interno della funzione di notifica dell'applicazione è determinata dall'applicazione. tuttavia, in genere consiste nel riprendere il thread appropriato per l'elaborazione del nuovo messaggio.

### <a name="queue-event-chaining"></a>Concatenamento di eventi della coda™  
Le funzionalità di notifica in ThreadX SMP possono essere usate per concatenare vari eventi di sincronizzazione. Ciò è in genere utile quando un singolo thread deve elaborare più eventi di sincronizzazione.

Si supponga, ad esempio, che un singolo thread sia responsabile dell'elaborazione dei messaggi da cinque code diverse e che sia necessario sospendere anche quando non sono disponibili messaggi. Questa operazione viene eseguita facilmente registrando una funzione di notifica dell'applicazione per ogni coda e introducendo un semaforo di conteggio aggiuntivo. In particolare, la funzione di notifica dell'applicazione esegue un *tx_semaphore_put* ogni volta che viene chiamato (il conteggio dei semafori rappresenta il numero totale di messaggi in tutte e cinque le code). Il thread di elaborazione viene sospeso in questo semaforo tramite il *tx_semaphore_get* servizio. Quando il semaforo è disponibile (in questo caso, quando è disponibile un messaggio), il thread di elaborazione viene ripreso. Interroga quindi ogni coda per un messaggio, elabora il messaggio trovato *ed* esegue un altro tx_semaphore_get attesa del messaggio successivo. Questa operazione senza concatenamento di eventi è piuttosto difficile e probabilmente richiederebbe più thread e/o codice dell'applicazione aggiuntivo.

In generale, *il concatenamento di eventi* comporta un minor numero di thread, un minore sovraccarico e requisiti di RAM più piccoli. Offre anche un meccanismo altamente flessibile per gestire i requisiti di sincronizzazione di sistemi più complessi.

### <a name="run-time-queue-performance-information"></a>Informazioni sulle prestazioni della coda di run-time  
ThreadX SMP fornisce informazioni facoltative sulle prestazioni della coda di run-time. Se la libreria e l'applicazione  ThreadX SMP vengono compilate con TX_QUEUE_ENABLE_PERFORMANCE_INFO, ThreadX SMP accumula le informazioni seguenti:

Numero totale per il sistema complessivo:

- messaggi inviati
- messaggi ricevuti
- sospensioni vuote della coda
- sospensioni complete della coda
- Restituisce l'errore completo della coda (sospensione non specificata)
- timeout della coda

Numero totale per ogni coda:

- messaggi inviati
- messaggi ricevuti
- sospensioni vuote della coda
- sospensioni complete della coda
- Restituisce l'errore completo della coda (sospensione non specificata)
- timeout della coda

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi *tx_queue_performance_info_get* e *tx_queue_performance_system_info_get*. Le informazioni sulle prestazioni della coda sono utili per determinare se l'applicazione funziona correttamente. È anche utile per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di "sospensioni complete della coda" suggerisce che un aumento delle dimensioni della coda potrebbe essere vantaggioso.

### <a name="queue-control-block-tx_queue"></a>Blocco di controllo code TX_QUEUE 
Le caratteristiche di ogni coda di messaggi si trovano nel relativo blocco di controllo. Contiene informazioni interessanti, ad esempio il numero di messaggi nella coda. Questa struttura è definita nel file ***tx_api.h.***

I blocchi di controllo della coda di messaggi possono anche trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione.

### <a name="message-destination-pitfall"></a>Errore di destinazione del messaggio  
Come accennato in precedenza, i messaggi vengono copiati tra l'area della coda e le aree dati dell'applicazione. È importante assicurarsi che la destinazione di un messaggio ricevuto sia sufficientemente grande da contenere l'intero messaggio. In caso contrario, la memoria che segue la destinazione del messaggio sarà probabilmente danneggiata. 

> [!WARNING]
> Ciò è particolarmente letale quando una destinazione di messaggi troppo piccola si trova nello stack, niente di simile al danneggiamento dell'indirizzo mittente di una funzione.

## <a name="counting-semaphores"></a>Conteggio dei semafori

ThreadX SMP fornisce semafori di conteggio a 32 bit compresi tra 0 e 4.294.967.295. Esistono due operazioni per il conteggio  dei semafori: tx_semaphore_get e *tx_semaphore_put*. L'operazione get riduce il semaforo di uno. Se il semaforo è 0, l'operazione get non riesce. L'inverso dell'operazione get è l'operazione put. Aumenta il semaforo di uno.

Ogni semaforo di conteggio è una risorsa pubblica. ThreadX SMP non inserisce vincoli sul modo in cui vengono usati i semafori di conteggio.

I semafori di conteggio vengono in genere usati per *l'esclusione reciproca.* Tuttavia, il conteggio dei semafori può essere usato anche come metodo per la notifica degli eventi.

### <a name="mutual-exclusion"></a>Esclusione reciproca 
L'esclusione reciproca riguarda il controllo dell'accesso dei thread a determinate aree dell'applicazione (denominate anche *sezioni critiche* o *risorse dell'applicazione).* Se usato per l'esclusione reciproca, il "conteggio corrente" di un semaforo rappresenta il numero totale di thread a cui è consentito l'accesso. Nella maggior parte dei casi, il conteggio dei semafori usati per l'esclusione reciproca avrà un valore iniziale pari a 1, vale a dire che un solo thread può accedere alla risorsa associata alla volta. I semafori di conteggio che hanno solo valori 0 o 1 sono comunemente denominati *semafori binari.*

> [!IMPORTANT]
> Se viene usato un semaforo binario, l'utente deve impedire allo stesso thread di eseguire un'operazione get su un semaforo di cui è già proprietario. Un secondo get non riesce e potrebbe causare la sospensione indefinita del thread chiamante e l'invariabilità permanente della risorsa.

### <a name="event-notification"></a>Notifica dell'evento 
È anche possibile usare il conteggio dei semafori come notifica degli eventi, in modo producer-consumer. Il consumer tenta di ottenere il semaforo di conteggio mentre il producer aumenta il semaforo ogni volta che è disponibile qualcosa. Questi semafori hanno in genere un valore iniziale pari a 0 e non aumentano fino a quando il producer non ha qualcosa di pronto per il consumer. Anche i semafori usati per la notifica degli eventi possono trarre vantaggio dall'uso *della* tx_semaphore_ceiling_put di servizio. Questo servizio garantisce che il numero di semafori non superi mai il valore fornito nella chiamata.

### <a name="creating-counting-semaphores"></a>Creazione di semafori di conteggio 
I semafori di conteggio vengono creati durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. Il conteggio iniziale del semaforo viene specificato durante la creazione. Non esiste alcun limite al numero di semafori di conteggio in un'applicazione. 

### <a name="thread-suspension"></a>Sospensione dei thread  
I thread dell'applicazione possono essere sospesi durante il tentativo di eseguire un'operazione get su un semaforo con un conteggio corrente di 0. 

Dopo l'esecuzione di un'operazione put, viene eseguita l'operazione get del thread sospeso e il thread viene ripreso. Se più thread vengono sospesi nello stesso semaforo di conteggio, vengono ripresi nello stesso ordine in cui sono stati sospesi (FIFO).

Tuttavia, la ripresa della priorità è possibile  anche se l'applicazione chiama tx_semaphore_prioritize prima della chiamata put del semaforo che solleva la sospensione del thread. Il servizio di assegnazione delle priorità del semaforo posiziona il thread con la priorità più alta all'inizio dell'elenco di sospensione, lasciando tutti gli altri thread sospesi nello stesso ordine FIFO.

### <a name="semaphore-put-notification"></a>Notifica put del semaforo 
Alcune applicazioni possono risultare vantaggiose ricevere una notifica ogni volta che viene inserito un semaforo. ThreadX SMP offre questa possibilità tramite il *servizio tx_semaphore_put_notify* locale. Questo servizio registra la funzione di notifica dell'applicazione fornita con il semaforo specificato. ThreadX SMP richiama successivamente questa funzione di notifica dell'applicazione ogni volta che viene inserito il semaforo. L'elaborazione esatta all'interno della funzione di notifica dell'applicazione è determinata dall'applicazione. tuttavia, in genere consiste nel riprendere il thread appropriato per l'elaborazione del nuovo evento put del semaforo.

### <a name="semaphore-eventchaining"></a>Semaphore Eventchaining™ 
Le funzionalità di notifica in ThreadX SMP possono essere usate per concatenare vari eventi di sincronizzazione. Ciò è in genere utile quando un singolo thread deve elaborare più eventi di sincronizzazione.

Ad esempio, anziché sospendere thread separati per un messaggio della coda, i flag di evento e un semaforo, l'applicazione può registrare una routine di notifica per ogni oggetto. Quando viene richiamata, la routine di notifica dell'applicazione può quindi riprendere un singolo thread, che può interrogare ogni oggetto per trovare ed elaborare il nuovo evento.

In generale, *il concatenamento degli eventi* comporta un minor numero di thread, un minor sovraccarico e requisiti di RAM più piccoli. Offre anche un meccanismo altamente flessibile per gestire i requisiti di sincronizzazione di sistemi più complessi.

### <a name="run-time-semaphore-performance-information"></a>Informazioni sulle prestazioni del semaforo di run-time 
ThreadX SMP fornisce informazioni facoltative sulle prestazioni del semaforo di run-time. Se la libreria e l'applicazione ThreadX SMP vengono compilate ***TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO*** definite, ThreadX SMP accumula le informazioni seguenti. 

Numero totale per il sistema complessivo:

- semaphore puts
- semaphore gets
- semaforo ottenere le sospensioni
- semaphore get timeouts

Numero totale per ogni semaforo:

- semaphore puts
- semaphore gets
- semaforo ottenere le sospensioni
- semaphore get timeouts

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi *tx_semaphore_performance_info_get* e *tx_semaphore_performance_system_info_get*. Le informazioni sulle prestazioni del semaforo sono utili per determinare se l'applicazione funziona correttamente. È anche utile per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di "timeout get semaphore" potrebbe suggerire che gli altri thread magano le risorse troppo a lungo.

### <a name="semaphore-control-block-tx_semaphore"></a>Blocco di controllo semaforo TX_SEMAPHORE 
Le caratteristiche di ogni semaforo di conteggio si trovano nel relativo blocco di controllo. Contiene informazioni come il conteggio del semaforo corrente. Questa struttura è definita nel file ***tx_api.h.*** 

I blocchi di controllo del semaforo possono trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione. 

### <a name="deadly-embrace"></a>Deadly Embrace 
Una delle insidie più interessanti e pericolose associate ai semafori usati per l'esclusione reciproca è l'uso *di*. Un accettamento, o *deadlock,* è una condizione in cui due o più thread vengono sospesi per un periodo illimitato durante il tentativo di ottenere semafori già di proprietà reciproca.

Questa condizione è illustrata meglio da un esempio di due thread, due semafori. Si supponga che il primo thread sia proprietario del primo semaforo e che il secondo sia proprietario del secondo semaforo. Se il primo thread tenta di ottenere il secondo semaforo e contemporaneamente il secondo thread tenta di ottenere il primo semaforo, entrambi i thread entrano in una condizione di deadlock. Inoltre, se questi thread rimangono sospesi per sempre, anche le risorse associate vengono bloccate per sempre. La figura 7 a pagina 78 illustra questo esempio.

![Deadly Embrace](media/image10.png)

**FIGURA 7. Esempio di thread sospesi**

Per i sistemi in tempo reale, è possibile impedire l'inserimento di alcune restrizioni sul modo in cui i thread ottengono i semafori. I thread possono avere un solo semaforo alla volta. In alternativa, i thread possono essere proprietari di più semafori se li raccolgono nello stesso ordine. Nell'esempio precedente, se il primo e il secondo thread ottengono il primo e il secondo semaforo nell'ordine indicato, l'adottamento non è consentito.

> [!IMPORTANT]
> È anche possibile usare il timeout di sospensione associato all'operazione get per eseguire il ripristino da un'accettata.

### <a name="priority-inversion"></a>Inversione priorità 
Un altro insidie associato ai semafori di esclusione reciproca è l'inversione della priorità. Questo argomento viene illustrato in modo più completo in "Insidie della priorità dei thread" a pagina 64.

Il problema di base deriva da una situazione in cui un thread con priorità più bassa ha un semaforo necessario per un thread con priorità più alta. Questo è di per sé normale. Tuttavia, i thread con priorità tra di essi possono causare l'inversione della priorità per un periodo di tempo non deterministico. Questa operazione può essere gestita tramite un'attenta selezione delle priorità dei thread, usando la soglia di precedenza e aumentando temporaneamente la priorità del thread proprietario della risorsa a quella del thread con priorità alta.

## <a name="mutexes"></a>Mutex

Oltre ai semafori, ThreadX SMP fornisce anche un oggetto mutex. Un mutex è fondamentalmente un semaforo binario, il che significa che un solo thread può essere proprietario di un mutex alla volta. Inoltre, lo stesso thread può eseguire più volte un'operazione get mutex riuscita su un mutex di proprietà, 4.294.967.295 per essere esatto. Sono disponibili due operazioni sull'oggetto mutex: ***tx_mutex_get** _ e _*_tx_mutex_put_**. L'operazione get ottiene un mutex non di proprietà di un altro thread, mentre l'operazione put rilascia un mutex ottenuto in precedenza. Perché un thread rilasci un mutex, il numero di operazioni put deve essere uguale al numero di operazioni get precedenti.

Ogni mutex è una risorsa pubblica. ThreadX SMP non pone vincoli sulla modalità di utilizzo dei mutex.

I mutex ThreadX vengono usati esclusivamente per *l'esclusione reciproca.* A differenza del conteggio dei semafori, i mutex non possono essere utilizzati come metodo per la notifica degli eventi.

### <a name="mutex-mutual-exclusion"></a>Esclusione reciproca mutex 
Analogamente alla discussione nella sezione relativa al semaforo di conteggio, l'esclusione reciproca  riguarda il controllo dell'accesso dei thread a determinate aree dell'applicazione (denominate anche sezioni critiche o risorse *dell'applicazione).* Quando disponibile, un mutex SMP ThreadX avrà un numero di proprietà 0. Dopo che il mutex è stato ottenuto da un thread, il conteggio della proprietà viene incrementato una volta per ogni operazione get riuscita eseguita sul mutex e decrementato per ogni operazione put riuscita.

### <a name="creating-mutexes"></a>Creazione di mutex 
I mutex SMP ThreadX vengono creati durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. La condizione iniziale di un mutex è sempre "disponibile". È anche possibile creare un mutex con *l'ereditarietà della priorità* selezionata.

### <a name="thread-suspension"></a>Sospensione dei thread 
I thread dell'applicazione possono essere sospesi durante il tentativo di eseguire un'operazione get su un mutex già di proprietà di un altro thread.

Dopo che il thread proprietario ha eseguito lo stesso numero di operazioni put, viene eseguita l'operazione get del thread sospeso, con la proprietà del mutex e il thread viene ripreso. Se più thread vengono sospesi nello stesso mutex, vengono ripresi nello stesso ordine in cui sono stati sospesi (FIFO).

Tuttavia, la ripresa della priorità viene eseguita automaticamente se durante la creazione è stata selezionata l'ereditarietà della priorità mutex. La ripresa della priorità è possibile  anche se l'applicazione chiama tx_mutex_prioritize prima della chiamata put mutex che eleva la sospensione del thread. Il servizio di assegnazione delle priorità mutex posiziona il thread con priorità più alta all'inizio dell'elenco di sospensione, lasciando tutti gli altri thread sospesi nello stesso ordine FIFO.

### <a name="run-time-mutex-performance-information"></a>Informazioni sulle prestazioni del mutex di run-time 
ThreadX SMP fornisce informazioni facoltative sulle prestazioni del mutex di run-time. Se la libreria e l'applicazione ThreadX SMP vengono compilate ***TX_MUTEX_ENABLE_PERFORMANCE_INFO*** definite, ThreadX SMP accumula le informazioni seguenti.

Numero totale per il sistema complessivo:

- mutex puts
- mutex gets
- mutex get suspensions
- mutex get timeouts
- inversione della priorità mutex
- Ereditarietà della priorità mutex

Numero totale per ogni mutex:

- mutex puts
- mutex gets
- mutex get suspensions
- mutex get timeouts
- inversione della priorità mutex
- Ereditarietà della priorità mutex

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi *tx_mutex_performance_info_get* e *tx_mutex_performance_system_info_get*. Le informazioni sulle prestazioni mutex sono utili per determinare se l'applicazione funziona correttamente. È anche utile per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di "mutex get timeouts" potrebbe suggerire che altri thread marcino le risorse troppo a lungo.

### <a name="mutex-control-block-tx_mutex"></a>Blocco di controllo mutex TX_MUTEX 
Le caratteristiche di ogni mutex si trovano nel relativo blocco di controllo. Contiene informazioni quali il numero di proprietà del mutex corrente insieme al puntatore del thread proprietario del mutex. Questa struttura è definita nel file ***tx_api.h.***

I blocchi di controllo mutex possono trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione.

### <a name="deadly-embrace"></a>Deadly Embrace  
Una delle insidie più interessanti e pericolose associate alla proprietà del mutex è *l'adottamento di*. Un blocco indefinito, o *deadlock,* è una condizione in cui due o più thread vengono sospesi per un periodo illimitato durante il tentativo di ottenere un mutex già di proprietà degli altri thread. La discussione *sull'accetta e* sui rimedi trovati a pagina 77 è completamente valida anche per l'oggetto mutex.

### <a name="priority-inversion"></a>Inversione priorità 
Come accennato in precedenza, una delle principali insidie associate all'esclusione reciproca è l'inversione della priorità. Questo argomento viene illustrato in modo più completo in "Insidie della priorità dei thread" a pagina 64. 

Il problema di base deriva da una situazione in cui un thread con priorità più bassa ha un semaforo necessario per un thread con priorità più alta. Questo è di per sé normale. Tuttavia, i thread con priorità tra di essi possono causare l'inversione della priorità per un periodo di tempo non deterministico. A differenza dei semafori descritti in precedenza, l'oggetto mutex SMP ThreadX ha *ereditarietà della priorità facoltativa.* L'idea di base alla base dell'ereditarietà della priorità è che la priorità di un thread con priorità più bassa viene temporaneamente elevata alla priorità di un thread con priorità alta che vuole che lo stesso mutex sia di proprietà del thread con priorità inferiore. Quando il thread con priorità più bassa rilascia il mutex, viene ripristinata la priorità originale e al thread con priorità più alta viene data la proprietà del mutex. Questa funzionalità elimina l'inversione della priorità non deterministica delimitando la quantità di inversione al momento in cui il thread con priorità inferiore contiene il mutex. Naturalmente, le tecniche illustrate in precedenza in questo capitolo per gestire l'inversione di priorità non deterministica sono valide anche con i mutex.

## <a name="event-flags"></a>Flag di evento

I flag di evento offrono uno strumento potente per la sincronizzazione dei thread. Ogni flag di evento è rappresentato da un singolo bit. I flag di evento sono disposti in gruppi di 32.

I thread possono operare contemporaneamente su tutti i 32 flag di evento in un gruppo. Gli eventi vengono impostati *tx_event_flags_set* e recuperati da *tx_event_flags_get*.

L'impostazione dei flag di evento viene eseguita con un'operazione AND/OR logica tra i flag di evento correnti e i nuovi flag di evento. Il tipo di operazione logica (AND o OR) viene specificato nella *tx_event_flags_set* chiamata.

Sono disponibili opzioni logiche simili per il recupero dei flag di evento. Una richiesta get può specificare che sono necessari tutti i flag di evento specificati (AND logico). In alternativa, una richiesta get può specificare che uno qualsiasi dei flag di evento specificati soddisferà la richiesta (or logico). Il tipo di operazione logica associata al recupero dei flag di evento viene specificato nella *tx_event_flags_get* chiamata.

> [!IMPORTANT]
> I flag di evento che soddisfano una richiesta get vengono utilizzati, ad esempio, impostati su zero, se TX_OR_CLEAR **o** **TX_AND_CLEAR** vengono specificati dalla richiesta.

Ogni gruppo di flag di evento è una risorsa pubblica. ThreadX SMP non pone vincoli sul modo in cui vengono usati i gruppi di flag di evento.

### <a name="creating-event-flags-groups"></a>Creazione di gruppi di flag di evento
I gruppi di flag di evento vengono creati durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. Al momento della creazione, tutti i flag di evento nel gruppo vengono impostati su zero. Non esiste alcun limite al numero di gruppi di flag di evento in un'applicazione.

### <a name="thread-suspension"></a>Sospensione dei thread 
I thread dell'applicazione possono essere sospesi durante il tentativo di ottenere qualsiasi combinazione logica di flag di evento da un gruppo. Dopo aver impostato un flag di evento, vengono esaminate le richieste get di tutti i thread sospesi. Tutti i thread che ora hanno i flag di evento necessari vengono ripresi.

> [!IMPORTANT]
> Tutti i thread sospesi in un gruppo di flag di evento vengono esaminati quando vengono impostati i relativi flag di evento. Questo, naturalmente, introduce un sovraccarico aggiuntivo. È quindi consigliabile limitare il numero di thread che usano lo stesso gruppo di flag di evento a un numero ragionevole.

### <a name="event-flags-set-notification"></a>Notifica dell'impostazione dei flag di evento 
Alcune applicazioni possono risultare vantaggiose ricevere una notifica ogni volta che viene impostato un flag di evento. ThreadX SMP offre questa possibilità tramite il *tx_event_flags_set_notify* servizio. Questo servizio registra la funzione di notifica dell'applicazione fornita con il gruppo di flag di evento specificato. ThreadX SMP richiama successivamente questa funzione di notifica dell'applicazione ogni volta che viene impostato un flag di evento nel gruppo. L'elaborazione esatta all'interno della funzione di notifica dell'applicazione è determinata dall'applicazione, ma in genere consiste nel riprendere il thread appropriato per l'elaborazione del nuovo flag di evento. 

### <a name="event-flags-event-chaining"></a>Event Flags Event-chaining (Concatenamento di eventi™ 
Le funzionalità di notifica in ThreadX SMP possono essere usate per "concatenare" diversi eventi di sincronizzazione. Ciò è in genere utile quando un singolo thread deve elaborare più eventi di sincronizzazione. 

Ad esempio, anziché sospendere thread separati per un messaggio della coda, i flag di evento e un semaforo, l'applicazione può registrare una routine di notifica per ogni oggetto. Quando viene richiamata, la routine di notifica dell'applicazione può quindi riprendere un singolo thread, che può interrogare ogni oggetto per trovare ed elaborare il nuovo evento. 

In generale, *il concatenamento degli eventi* comporta un minor numero di thread, un minor sovraccarico e requisiti di RAM più piccoli. Offre anche un meccanismo altamente flessibile per gestire i requisiti di sincronizzazione di sistemi più complessi. 

### <a name="run-time-event-flags-performance-information"></a>Informazioni sulle prestazioni dei flag di eventi di run-time 
ThreadX SMP fornisce informazioni facoltative sulle prestazioni dei flag di eventi di run-time. Se la libreria e l'applicazione ThreadX SMP vengono compilate ***TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO,*** ThreadX SMP accumula le informazioni seguenti.

Numero totale per il sistema complessivo:

- set di flag di eventi
- event flags gets
- i flag di evento ottengono le sospensioni
- event flags get timeouts

Numero totale per ogni gruppo di flag di evento:

- set di flag di eventi
- event flags gets
- i flag di evento ottengono le sospensioni
- event flags get timeouts

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi *tx_event_flags_performance_info_get* e *tx_event_flags_performance_system_info_get*. Le informazioni sulle prestazioni dei flag di evento sono utili per determinare se l'applicazione funziona correttamente. È anche utile per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di timeout nel servizio tx_event_flags_get *potrebbe* suggerire che il timeout di sospensione dei flag di evento sia troppo breve.

### <a name="event-flags-group-control-block-tx_event_flags_group"></a>Blocco di controllo gruppo flag di TX_EVENT_FLAGS_GROUP
Le caratteristiche di ogni gruppo di flag di evento si trovano nel relativo blocco di controllo. Contiene informazioni quali le impostazioni dei flag di evento correnti e il numero di thread sospesi per gli eventi. Questa struttura è definita nel file ***tx_api.h.*** 

I blocchi di controllo del gruppo di eventi possono trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione.

## <a name="memory-block-pools"></a>Pool di blocchi di memoria  

L'allocazione della memoria in modo rapido e deterministico è sempre una sfida nelle applicazioni in tempo reale. A questo scopo, ThreadX SMP offre la possibilità di creare e gestire più pool di blocchi di memoria a dimensione fissa.

Poiché i pool di blocchi di memoria sono costituiti da blocchi a dimensione fissa, non si verificano mai problemi di frammentazione. Naturalmente, la frammentazione causa un comportamento intrinsecamente non deterministico. Inoltre, il tempo necessario per allocare e liberare un blocco di memoria a dimensione fissa è paragonabile a quello della semplice manipolazione dell'elenco collegato. Inoltre, l'allocazione e la deallocazione dei blocchi di memoria vengono eseguite all'inizio dell'elenco disponibile. In questo modo si garantisce la massima velocità di elaborazione dell'elenco collegato e può essere utile per mantenere il blocco di memoria effettivo nella cache.

La mancanza di flessibilità è lo svantaggio principale dei pool di memoria a dimensione fissa. Le dimensioni del blocco di un pool devono essere sufficientemente grandi da gestire i requisiti di memoria dei casi peggiori per gli utenti. Naturalmente, la memoria può essere sprecata se vengono effettuate molte richieste di memoria di dimensioni diverse allo stesso pool. Una possibile soluzione consiste nel creare diversi pool di blocchi di memoria che contengono blocchi di memoria di dimensioni diverse.

Ogni pool di blocchi di memoria è una risorsa pubblica. ThreadX SMP non pone vincoli sul modo in cui vengono usati i pool.

### <a name="creating-memory-block-pools"></a>Creazione di pool di blocchi di memoria  
I pool di blocchi di memoria vengono creati durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. Non esiste alcun limite al numero di pool di blocchi di memoria in un'applicazione.

### <a name="memory-block-size"></a>Dimensioni del blocco di memoria  
Come accennato in precedenza, i pool di blocchi di memoria contengono un numero di blocchi a dimensione fissa. Le dimensioni del blocco, in byte, vengono specificate durante la creazione del pool.

> [!IMPORTANT]
> ThreadX SMP aggiunge una piccola quantità di overhead, ovvero le dimensioni di un puntatore C, a ogni blocco di memoria nel pool. Inoltre, ThreadX SMP potrebbe dover riempire le dimensioni del blocco per mantenere l'inizio di ogni blocco di memoria allineato correttamente.

### <a name="pool-capacity"></a>Capacità del pool 
Il numero di blocchi di memoria in un pool è una funzione delle dimensioni del blocco e del numero totale di byte nell'area di memoria fornita durante la creazione. La capacità di un pool viene calcolata dividendo le dimensioni del blocco (inclusa la spaziatura interna e i byte di overhead del puntatore) nel numero totale di byte nell'area di memoria fornita.

### <a name="pools-memory-area"></a>Area di memoria del pool 
Come accennato in precedenza, l'area di memoria per il pool di blocchi viene specificata durante la creazione. Analogamente ad altre aree di memoria in ThreadX SMP, può trovarsi in qualsiasi punto dello spazio degli indirizzi della destinazione.

Si tratta di una funzionalità importante grazie alla notevole flessibilità che offre. Si supponga, ad esempio, che un prodotto di comunicazione abbia un'area di memoria a velocità elevata per l'I/O. Questa area di memoria è facilmente gestita rendendola in un pool di blocchi di memoria SMP ThreadX.

### <a name="thread-suspension"></a>Sospensione dei thread 
I thread dell'applicazione possono essere sospesi durante l'attesa di un blocco di memoria da un pool vuoto. Quando un blocco viene restituito al pool, al thread sospeso viene assegnato questo blocco e il thread viene ripreso.

Se più thread vengono sospesi nello stesso pool di blocchi di memoria, vengono ripresi nell'ordine in cui sono stati sospesi (FIFO).

Tuttavia, la ripresa della priorità è possibile anche se l'applicazione chiama tx_block_pool_prioritize prima della chiamata di rilascio ***del*** blocco che revoca la sospensione del thread. Il servizio di assegnazione della priorità del pool di blocchi posiziona il thread con priorità più alta all'inizio dell'elenco di sospensione, lasciando tutti gli altri thread sospesi nello stesso ordine FIFO.

### <a name="run-time-block-pool-performance-information"></a>Informazioni sulle prestazioni del pool a blocchi di run-time  
ThreadX SMP fornisce informazioni facoltative sulle prestazioni del pool a blocchi di run-time. Se la libreria e l'applicazione  ThreadX SMP vengono compilate con TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO, ThreadX SMP accumula le informazioni seguenti.

Numero totale per il sistema complessivo:

- blocchi allocati
- blocchi rilasciati
- sospensioni di allocazione
- timeout di allocazione

Numero totale per ogni pool di blocchi:

- blocchi allocati
- blocchi rilasciati
- sospensioni di allocazione
- timeout di allocazione

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi *tx_block_pool_performance_info_get* e *tx_block_pool_performance_system_info_get*. Le informazioni sulle prestazioni del pool di blocchi sono utili per determinare se l'applicazione funziona correttamente. È anche utile per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di "sospensioni di allocazione" potrebbe suggerire che il pool di blocchi sia troppo piccolo.

### <a name="memory-block-pool-control-block-tx_block_pool"></a>Blocco di controllo del pool di blocchi di memoria TX_BLOCK_POOL  
Le caratteristiche di ogni pool di blocchi di memoria si trovano nel relativo blocco di controllo. Contiene informazioni quali il numero di blocchi di memoria disponibili e le dimensioni del blocco del pool di memoria. Questa struttura è definita nel file ***tx_api.h.*** 

I blocchi di controllo del pool possono anche trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione. 

### <a name="overwriting-memory-blocks"></a>Sovrascrittura dei blocchi di memoria  
È importante assicurarsi che l'utente di un blocco di memoria allocato non scrivo al di fuori dei limiti. In questo caso, si verifica un danneggiamento in un'area di memoria adiacente (in genere successiva). I risultati sono imprevedibili e spesso fatali. 

## <a name="memory-byte-pools"></a>Pool di byte di memoria

I pool di byte di memoria SMP ThreadX sono simili a un heap C standard. A differenza dell'heap C standard, è possibile avere più pool di byte di memoria. Inoltre, i thread possono essere sospesi in un pool fino a quando la memoria richiesta non è disponibile.

Le allocazioni dai pool di byte di memoria sono simili alle chiamate *malloc* tradizionali, che includono la quantità di memoria desiderata (in byte). La memoria viene allocata dal pool in *modo appropriato.* Ad esempio, viene usato il primo blocco di memoria disponibile che soddisfa la richiesta. La memoria in eccesso da questo blocco viene convertita in un nuovo blocco e inserita nuovamente nell'elenco di memoria disponibile. Questo processo è denominato *frammentazione.*

I blocchi di memoria libera adiacenti *vengono uniti durante* una successiva ricerca di un blocco di memoria disponibile sufficientemente grande. Questo processo è denominato *de-frammentazione.*

Ogni pool di byte di memoria è una risorsa pubblica. ThreadX SMP non inserisce vincoli sulla modalità di utilizzo dei pool, ad eccezione del fatto che i servizi byte di memoria non possono essere chiamati da ISR.

### <a name="creating-memory-byte-pools"></a>Creazione di pool di byte di memoria 
I pool di byte di memoria vengono creati durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. Non esiste alcun limite al numero di pool di byte di memoria in un'applicazione.  

### <a name="pool-capacity"></a>Capacità del pool 
Il numero di byte allocatibili in un pool di byte di memoria è leggermente inferiore a quello specificato durante la creazione. Ciò è dovuto al fatto che la gestione dell'area di memoria disponibile introduce un sovraccarico. Ogni blocco di memoria disponibile nel pool richiede l'equivalente di due puntatori C di overhead. Inoltre, il pool viene creato con due blocchi, un blocco libero di grandi dimensioni e un piccolo blocco allocato in modo permanente alla fine dell'area di memoria. Questo blocco allocato viene usato per migliorare le prestazioni dell'algoritmo di allocazione. Elimina la necessità di controllare continuamente la fine dell'area del pool durante l'unione.  

Durante la fase di esecuzione, la quantità di overhead nel pool aumenta in genere. Le allocazioni di un numero dispari di byte vengono riempite per garantire l'allineamento corretto del blocco di memoria successivo. Inoltre, l'overhead aumenta quando il pool diventa più frammentato.

### <a name="pools-memory-area"></a>Area di memoria del pool  
L'area di memoria per un pool di byte di memoria viene specificata durante la creazione. Analogamente ad altre aree di memoria in ThreadX SMP, può trovarsi in qualsiasi punto dello spazio degli indirizzi della destinazione. 

Si tratta di una funzionalità importante grazie alla notevole flessibilità che offre. Ad esempio, se l'hardware di destinazione ha un'area di memoria ad alta velocità e un'area di memoria a bassa velocità, l'utente può gestire l'allocazione di memoria per entrambe le aree creando un pool in ognuna di esse. 

### <a name="thread-suspension"></a>Sospensione dei thread  
I thread dell'applicazione possono essere sospesi durante l'attesa dei byte di memoria da un pool. Quando la memoria contigua sufficiente diventa disponibile, ai thread sospesi viene data la memoria richiesta e i thread vengono ripresi. 

Se più thread vengono sospesi nello stesso pool di byte di memoria, viene loro data memoria (ripresa) nell'ordine in cui sono stati sospesi (FIFO). 

Tuttavia, la ripresa della priorità è possibile  anche se l'applicazione chiama tx_byte_pool_prioritize prima della chiamata di rilascio dei byte che solleva la sospensione del thread. Il servizio di assegnazione della priorità del pool di byte posiziona il thread con priorità più alta all'inizio dell'elenco di sospensione, lasciando tutti gli altri thread sospesi nello stesso ordine FIFO.

### <a name="run-time-byte-pool-performance-information"></a>Informazioni sulle prestazioni del pool di byte in fase di esecuzione  
ThreadX SMP fornisce informazioni facoltative sulle prestazioni del pool di byte in fase di esecuzione. Se la libreria e l'applicazione  ThreadX SMP vengono compilate con TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO, ThreadX SMP accumula le informazioni seguenti.

Numero totale per il sistema complessivo:

- Allocazioni
- versioni
- frammenti cercati
- frammenti uniti
- frammenti creati
- sospensioni di allocazione
- timeout di allocazione

Numero totale per ogni pool di byte:

- Allocazioni
- versioni
- frammenti cercati
- frammenti uniti
- frammenti creati
- sospensioni di allocazione
- timeout di allocazione

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi *tx_byte_pool_performance_info_get* e *tx_byte_pool_performance_system_info_get*. Le informazioni sulle prestazioni del pool di byte sono utili per determinare se l'applicazione funziona correttamente. È anche utile per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di "sospensioni di allocazione" potrebbe suggerire che il pool di byte sia troppo piccolo.

### <a name="memory-byte-pool-control-block-tx_byte_pool"></a>Blocco di controllo del pool di byte di memoria TX_BYTE_POOL  
Le caratteristiche di ogni pool di byte di memoria si trovano nel relativo blocco di controllo. Contiene informazioni utili, ad esempio il numero di byte disponibili nel pool. Questa struttura è definita nel file ***tx_api.h.*** 

I blocchi di controllo del pool possono anche trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione. 

### <a name="nondeterministic-behavior"></a>Comportamento non deterministico 
Anche se i pool di byte di memoria forniscono l'allocazione di memoria più flessibile, hanno anche un comportamento in qualche modo non deterministico. Ad esempio, un pool di byte di memoria può avere 2.000 byte di memoria disponibili, ma potrebbe non essere in grado di soddisfare una richiesta di allocazione di 1.000 byte. Ciò è dovuto al fatto che non esistono garanzie sul numero di byte liberi contigui. Anche se esiste un blocco libero da 1.000 byte, non esistono garanzie sul tempo necessario per trovare il blocco. È possibile che sia necessario cercare l'intero pool di memoria per trovare il blocco di 1.000 byte. 

> [!IMPORTANT]
> Per questo scopo, è in genere consigliabile evitare l'uso di servizi byte di memoria nelle aree in cui è necessario un comportamento deterministico in tempo reale. Molte applicazioni preallocare la memoria necessaria durante l'inizializzazione o la configurazione in fase di esecuzione.

### <a name="overwriting-memory-blocks"></a>Sovrascrittura dei blocchi di memoria 
È importante assicurarsi che l'utente della memoria allocata non scrivo al di fuori dei limiti. In questo caso, si verifica un danneggiamento in un'area di memoria adiacente (in genere successiva). I risultati sono imprevedibili e spesso fatali. 

## <a name="application-timers"></a>Timer dell'applicazione

La risposta rapida agli eventi esterni asincroni è la funzione più importante delle applicazioni incorporate in tempo reale. Tuttavia, molte di queste applicazioni devono anche eseguire determinate attività a intervalli di tempo predeterminato.

I timer dell'applicazione ThreadX SMP offrono alle applicazioni la possibilità di eseguire funzioni dell'applicazione C a intervalli di tempo specifici. È anche possibile che un timer dell'applicazione scada una sola volta. Questo tipo di timer è detto *timer* a un solo colpo, mentre i timer a intervalli ripetuti sono detti *timer periodici.*

Ogni timer dell'applicazione è una risorsa pubblica. ThreadX SMP non pone vincoli sul modo in cui vengono usati i timer dell'applicazione.

> [!IMPORTANT]
> I timer dell'applicazione possono essere esclusi dall'esecuzione in qualsiasi core tramite l tx_timer_smp_core_exclude API.

### <a name="timer-intervals"></a>Intervalli timer 
In ThreadX gli intervalli di tempo SMP vengono misurati da interrupt timer periodici. Ogni interrupt timer è denominato timer *tick*. Il tempo effettivo tra i tick del timer viene specificato dall'applicazione, ma 10 ms è la norma per la maggior parte delle implementazioni. La configurazione periodica del timer si trova in genere nel file ***tx_initialize_low_level*** assembly.

Vale la pena ricordare che l'hardware sottostante deve avere la possibilità di generare interrupt periodici per il funzionamento dei timer dell'applicazione. In alcuni casi, il processore ha una funzionalità di interrupt periodico incorporata. Se il processore non ha questa capacità, la scheda dell'utente deve avere un dispositivo periferico in grado di generare interrupt periodici.

> [!IMPORTANT]
> ThreadX SMP può comunque funzionare anche senza un'origine di interrupt periodica. Tuttavia, tutta l'elaborazione correlata al timer viene quindi disabilitata. Sono inclusi il timelicing, i timeout di sospensione e i servizi timer.

### <a name="timer-accuracy"></a>Accuratezza timer 
Le scadenze del timer vengono specificate in termini di tick. Il valore di scadenza specificato viene ridotto di uno per ogni tick del timer. Poiché un timer dell'applicazione può essere abilitato subito prima di un interrupt timer (o tick timer), l'ora di scadenza effettiva potrebbe essere fino a un tick in anticipo.

Se la frequenza di tick del timer è di 10 ms, i timer dell'applicazione potrebbero scadere in anticipo fino a 10 ms. Si tratta di un valore più significativo per i timer di 10 ms rispetto a 1 secondo. Naturalmente, l'aumento della frequenza di interrupt del timer riduce questo margine di errore.

### <a name="timer-execution"></a>Esecuzione del timer 
I timer dell'applicazione vengono eseguiti nell'ordine in cui diventano attivi. Ad esempio, se tre timer vengono creati con lo stesso valore di scadenza e attivati, le funzioni di scadenza corrispondenti verranno eseguite nell'ordine in cui sono stati attivati. 

### <a name="creating-application-timers"></a>Creazione di timer dell'applicazione 
I timer dell'applicazione vengono creati durante l'inizializzazione o in fase di esecuzione dai thread dell'applicazione. Non esiste alcun limite al numero di timer dell'applicazione in un'applicazione. 

### <a name="run-time-application-timer-performance-information"></a>Informazioni sulle prestazioni del timer dell'applicazione in fase di esecuzione  
ThreadX SMP fornisce informazioni facoltative sulle prestazioni del timer dell'applicazione in fase di esecuzione. Se la libreria e l'applicazione  ThreadX SMP vengono compilate con TX_TIMER_ENABLE_PERFORMANCE_INFO, ThreadX SMP accumula le informazioni seguenti. 

Numero totale per il sistema complessivo:

- Attivazioni
- disattivazioni
- riattivazioni (timer periodici)
- expirations
- rettifiche di scadenza

Numero totale per ogni timer dell'applicazione:

- Attivazioni
- disattivazioni
- riattivazioni (timer periodici)
- expirations
- rettifiche di scadenza

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi *tx_timer_performance_info_get* e *tx_timer_performance_system_info_get*. Le informazioni sulle prestazioni del timer dell'applicazione sono utili per determinare se l'applicazione funziona correttamente. È anche utile per ottimizzare l'applicazione.

### <a name="application-timer-control-block-tx_timer"></a>Blocco di controllo timer applicazione TX_TIMER 
Le caratteristiche di ogni timer dell'applicazione si trovano nel relativo blocco di controllo. Contiene informazioni utili, ad esempio il valore di identificazione della scadenza a 32 bit. Questa struttura è definita nel file ***tx_api.h.***

I blocchi di controllo del timer dell'applicazione possono trovarsi in qualsiasi punto della memoria, ma è più comune rendere il blocco di controllo una struttura globale definendo il blocco all'esterno dell'ambito di qualsiasi funzione. 

### <a name="excessive-timers"></a>Timer eccessivi 
Per impostazione predefinita, i timer dell'applicazione vengono eseguiti dall'interno di un thread di sistema nascosto che viene eseguito con priorità zero, che in genere è superiore a qualsiasi thread dell'applicazione. Per questo, l'elaborazione all'interno dei timer dell'applicazione deve essere mantenuta al minimo. 

È anche importante evitare, quando possibile, i timer che scadono ogni tick del timer. Una situazione di questo tipo potrebbe provocare un sovraccarico eccessivo nell'applicazione.

> [!WARNING]
> Come accennato in precedenza, i timer dell'applicazione vengono eseguiti da un thread di sistema nascosto. È quindi importante non selezionare la sospensione in tutte le chiamate al servizio ThreadX SMP effettuate dall'interno della funzione di scadenza del timer dell'applicazione.

## <a name="relative-time"></a>Ora relativa

Oltre ai timer dell'applicazione menzionati in precedenza, ThreadX SMP fornisce un singolo contatore tick a 32 bit a incremento continuo. Il contatore di tick o *il tempo* viene aumentato di uno per ogni interrupt del timer.

L'applicazione può leggere o impostare questo contatore a 32 bit tramite chiamate tx_time_get *e* *tx_time_set*, rispettivamente. L'uso di questo contatore tick è determinato completamente dall'applicazione. Non viene usato internamente da ThreadX SMP.

### <a name="interrupts"></a>Interrompe 
La risposta rapida agli eventi asincroni è la funzione principale delle applicazioni incorporate in tempo reale. L'applicazione sa che tale evento è presente tramite interrupt hardware. 

Un interrupt è una modifica asincrona nell'esecuzione del processore. In genere, quando si verifica un interrupt, il processore salva una piccola parte dell'esecuzione corrente nello stack e trasferisce il controllo al vettore di interrupt appropriato. Il vettore di interrupt è fondamentalmente solo l'indirizzo della routine responsabile della gestione dell'interrupt di tipo specifico. La procedura di gestione esatta degli interrupt è specifica del processore. 

### <a name="interrupt-control"></a>Controllo interrupt 
Il *tx_interrupt_control* consente alle applicazioni di abilitare e disabilitare gli interrupt. La posizione di abilitazione/disabilitazione dell'interrupt precedente viene restituita da questo servizio. È importante ricordare che il controllo delle interruzioni influisce solo sul segmento di programma attualmente in esecuzione. Ad esempio, se un thread disabilita gli interrupt, rimangono disabilitati solo durante l'esecuzione di tale thread. 

> [!WARNING]
> Un interrupt non mascherabile (NMI) è un interrupt che non può essere disabilitato dall'hardware. Tale interrupt può essere usato dalle applicazioni ThreadX SMP. Tuttavia, la routine di gestione NMI dell'applicazione non può usare la gestione del contesto SMP ThreadX o i servizi API. Interrupt gestiti SMP ThreadX

ThreadX SMP offre alle applicazioni la gestione completa degli interrupt. Questa gestione include il salvataggio e il ripristino del contesto dell'esecuzione interrotta. ThreadX SMP consente inoltre di chiamare determinati servizi dall'interno di routine del servizio interrupt (ISR). Di seguito è riportato un elenco di servizi SmP di ThreadX consentiti dagli ISR dell'applicazione:

- tx_block_allocate 
- tx_block_pool_info_get 
- tx_block_pool_prioritize 
- tx_block_pool_performance_info_get 
- tx_block_pool_performance_system_info_get 
- tx_block_release 
- tx_byte_pool_info_get 
- tx_byte_pool_performance_info_get 
- tx_byte_pool_performance_system_info_get 
- tx_byte_pool_prioritize 
- tx_event_flags_info_get 
- tx_event_flags_get 
- tx_event_flags_set 
- tx_event_flags_performance_info_get 
- tx_event_flags_performance_system_info_get 
- tx_event_flags_set_notify 
- tx_interrupt_control 
- tx_mutex_performance_info_get 
- tx_mutex_performance_system_info_get 
- tx_queue_front_send 
- tx_queue_info_get 
- tx_queue_performance_info_get 
- tx_queue_performance_system_info_get 
- tx_queue_prioritize 
- tx_queue_receive 
- tx_queue_send 
- tx_semaphore_get 
- tx_queue_send_notify 
- tx_semaphore_ceiling_put 
- tx_semaphore_info_get 
- tx_semaphore_performance_info_get 
- tx_semaphore_performance_system_info_get 
- tx_semaphore_prioritize 
- tx_semaphore_put 
- tx_thread_identify 
- tx_semaphore_put_notify 
- tx_thread_entry_exit_notify 
- tx_thread_info_get 
- tx_thread_resume 
- tx_thread_performance_info_get 
- tx_thread_performance_system_info_get 
- tx_thread_stack_error_notify 
- tx_thread_wait_abort 
- tx_time_get 
- tx_time_set 
- tx_timer_activate 
- tx_timer_change 
- tx_timer_deactivate 
- tx_timer_info_get 
- tx_timer_performance_info_get 
- tx_timer_performance_system_info_get

> [!WARNING]
> La sospensione non è consentita dagli ISR. Pertanto, il **wait_option** per tutte le chiamate al servizio ThreadX SMP effettuate da un ISR deve essere impostato **su TX_NO_WAIT**.

### <a name="isr-template"></a>Modello ISR 
Per gestire gli interrupt dell'applicazione, è necessario chiamare diverse utilità ThreadX SMP all'inizio e alla fine degli ISR dell'applicazione. Il formato esatto per la gestione degli interrupt varia tra le porte. Esaminare il ***filereadme_threadx.txt*** sul disco di distribuzione per istruzioni specifiche sulla gestione degli ISR.

Il segmento di codice seguente è tipico della maggior parte degli ISR gestiti da ThreadX SMP. Nella maggior parte dei casi, questa elaborazione è in linguaggio assembly.

**_application_ISR_vector_entry**:  
; Salvare il contesto e prepararsi per  
; Uso di ThreadX SMP chiamando l'ISR  
; Funzione entry.  
Chiamare **_tx_thread_context_save**  

; L'ISR può ora chiamare ThreadX SMP  
; servizi e funzioni C proprie  

; Al termine dell'ISR, contesto  
; viene ripristinato (o la preemption del thread)  
; chiamando il ripristino del contesto  
; Funzione. Il controllo non viene restituito.  
Jump **_tx_thread_context_restore**

### <a name="high-frequency-interrupts"></a>Interrupt ad alta frequenza  
Alcune interruzioni si verificano a una frequenza tale che il salvataggio e il ripristino del contesto completo a ogni interrupt consumano una larghezza di banda di elaborazione eccessiva. In questi casi, è comune che l'applicazione abbia un ISR in linguaggio assembly di piccole dimensioni che esegue una quantità limitata di elaborazione per la maggior parte di questi interrupt ad altafrequenza. 

Dopo un determinato momento, l'ISR di piccole dimensioni potrebbe dover interagire con ThreadX SMP. Questa operazione viene eseguita chiamando le funzioni di ingresso e di uscita descritte nel modello precedente. 

### <a name="interrupt-latency"></a>Latenza di interrupt  
ThreadX SMP blocca gli interrupt in brevi periodi di tempo. La quantità massima di tempo in cui gli interrupt vengono disabilitati è nell'ordine del tempo necessario per salvare o ripristinare il contesto di un thread. 