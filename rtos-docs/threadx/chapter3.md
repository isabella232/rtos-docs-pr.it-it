---
title: Capitolo 3-componenti funzionali di Azure RTO ThreadX
description: Questo capitolo contiene una descrizione del kernel ThreadX di Azure RTO ad alte prestazioni dal punto di vista funzionale.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: aa66ad392171958e5d2cc765992fd1a9e41250a6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823276"
---
# <a name="chapter-3---functional-components-of-azure-rtos-threadx"></a>Capitolo 3-componenti funzionali di Azure RTO ThreadX

Questo capitolo contiene una descrizione del kernel ThreadX di Azure RTO ad alte prestazioni dal punto di vista funzionale. Ogni componente funzionale viene presentato in modo facile da comprendere.

## <a name="execution-overview"></a>Panoramica dell'esecuzione

Sono disponibili quattro tipi di esecuzione del programma all'interno di un'applicazione ThreadX: inizializzazione, esecuzione dei thread, routine del servizio di interrupt (ISRs) e timer dell'applicazione.

Nella figura 2 sono illustrati i diversi tipi di esecuzione del programma. Le informazioni più dettagliate su ognuno di questi tipi sono disponibili nelle sezioni successive di questo capitolo.

### <a name="initialization"></a>Inizializzazione

Come suggerisce il nome, questo è il primo tipo di esecuzione del programma in un'applicazione ThreadX. L'inizializzazione include l'esecuzione del programma tra la reimpostazione del processore e il punto di ingresso del *ciclo di pianificazione dei thread.*

### <a name="thread-execution"></a>Esecuzione thread

Al termine dell'inizializzazione, ThreadX immette il ciclo di pianificazione dei thread. Il ciclo di pianificazione cerca un thread dell'applicazione pronto per l'esecuzione. Quando viene trovato un thread pronto, ThreadX trasferisce il controllo a tale thread. Al termine del thread (o un altro thread con priorità più alta), l'esecuzione viene ritrasferita al ciclo di pianificazione dei thread per individuare il successivo thread pronto per la priorità più alta.

Questo processo di esecuzione continua e pianificazione dei thread è il tipo più comune di esecuzione di programmi nelle applicazioni ThreadX.

### <a name="interrupt-service-routines-isr"></a>Routine del servizio di interrupt (ISR)

Gli interrupt sono l'elemento fondamentale dei sistemi in tempo reale. Senza interruzioni, sarebbe molto difficile rispondere alle modifiche nel mondo esterno in modo tempestivo. Al rilevamento di un interrupt, il processore salva le informazioni chiave sull'esecuzione del programma corrente (in genere nello stack), quindi trasferisce il controllo a un'area del programma predefinita. Questa area del programma predefinita è comunemente denominata routine del servizio di interrupt. Nella maggior parte dei casi, gli interrupt si verificano durante l'esecuzione del thread o nel ciclo di pianificazione dei thread. Tuttavia, gli interrupt possono verificarsi anche all'interno di un ISR in esecuzione o di un timer dell'applicazione.

![Tipi di esecuzione del programma](./media/user-guide/types-program-execution.png)

**FIGURA 2. Tipi di esecuzione del programma**

### <a name="application-timers"></a>Timer applicazione

I timer dell'applicazione sono simili a ISRs, con l'eccezione che l'implementazione dell'hardware (in genere viene usato un singolo interrupt hardware periodico) viene nascosta dall'applicazione. Tali timer vengono usati dalle applicazioni per eseguire i servizi di timeout, Periodics e/o watchdog. Analogamente a ISRs, i timer dell'applicazione interrompono più spesso l'esecuzione del thread. A differenza di ISRs, tuttavia, i timer dell'applicazione non possono interrompersi tra loro.

## <a name="memory-usage"></a>Utilizzo memoria

ThreadX si trova insieme al programma applicativo. Di conseguenza, l'utilizzo della memoria statica (o della memoria fissa) di ThreadX è determinato dagli strumenti di sviluppo; ad esempio, il compilatore, il linker e il localizzatore. L'utilizzo della memoria dinamica (o della memoria di run-time) è sotto il controllo diretto dell'applicazione.

### <a name="static-memory-usage"></a>Utilizzo memoria statica

La maggior parte degli strumenti di sviluppo divide l'immagine del programma applicativa in cinque aree di base: *istruzione*, *costante*, *dati inizializzati*, *dati non inizializzati* e *stack di sistema*. Nella figura 3 viene illustrato un esempio di queste aree di memoria.

È importante comprendere che questo è solo un esempio. Il layout di memoria statica effettivo è specifico del processore, degli strumenti di sviluppo e dell'hardware sottostante.

L'area di istruzioni contiene tutte le istruzioni del processore del programma. Questa area è in genere la più grande e spesso si trova in ROM.

L'area costante contiene varie costanti compilate, incluse le stringhe definite o a cui viene fatto riferimento all'interno del programma. Inoltre, quest'area contiene la "copia iniziale" dell'area dati inizializzata. Durante il processo di inizializzazione del compilatore *utilizzo memoria* , questa parte dell'area costante viene utilizzata per configurare l'area dati inizializzata in RAM. L'area costante segue in genere l'area di istruzioni e spesso si trova nella ROM.

I dati inizializzati e le aree dati non inizializzate contengono tutte le variabili globali e statiche. Queste aree sono sempre situate in RAM.

Lo stack di sistema viene in genere configurato immediatamente dopo le aree dati inizializzate e non inizializzate.

Lo stack di sistema viene usato dal compilatore durante l'inizializzazione, quindi da ThreadX durante l'inizializzazione e, successivamente, nell'elaborazione ISR.

![Esempio di area di memoria](./media/user-guide/memory-area-example.png)

**FIGURA 3. Esempio di area di memoria**

### <a name="dynamic-memory-usage"></a>Utilizzo memoria dinamica

Come indicato in precedenza, l'utilizzo della memoria dinamica è sotto il controllo diretto dell'applicazione. I blocchi di controllo e le aree di memoria associati a stack, code e pool di memoria possono essere posizionati in qualsiasi punto dello spazio di memoria della destinazione. Si tratta di una funzionalità importante perché semplifica l'utilizzo di diversi tipi di memoria fisica.

Si supponga, ad esempio, che un ambiente hardware di destinazione disponga sia di memoria veloce che di memoria lenta. Se l'applicazione richiede prestazioni aggiuntive per un thread con priorità alta, il blocco di controllo (TX_THREAD) e lo stack possono essere inseriti nell'area di memoria veloce, che può migliorare significativamente le prestazioni.

## <a name="initialization"></a>Inizializzazione

La comprensione del processo di inizializzazione è importante. L'ambiente hardware iniziale è configurato qui. Inoltre, è il punto in cui l'applicazione riceve la personalità iniziale.

> [!NOTE]
> *ThreadX tenta di utilizzare (laddove possibile) il processo di inizializzazione completo dello strumento di sviluppo. In questo modo sarà più semplice eseguire l'aggiornamento a nuove versioni degli strumenti di sviluppo in futuro.*

### <a name="system-reset-vector"></a>Vettore di ripristino del sistema

Tutti i microprocessori hanno una logica di reimpostazione. Quando si verifica una reimpostazione, ovvero hardware o software, l'indirizzo del punto di ingresso dell'applicazione viene recuperato da una posizione di memoria specifica. Una volta recuperato il punto di ingresso, il processore trasferisce il controllo a tale posizione. Il punto di ingresso dell'applicazione è spesso scritto nel linguaggio degli assembly nativi e viene in genere fornito dagli strumenti di sviluppo (almeno in formato modello). In alcuni casi, viene fornita una versione speciale del programma entry con ThreadX.

### <a name="development-tool-initialization"></a>Inizializzazione dello strumento di sviluppo

Al termine dell'inizializzazione di basso livello, il controllo viene trasferito all'inizializzazione di alto livello dello strumento di sviluppo. Si tratta in genere della posizione in cui sono impostate le variabili C globali e statiche inizializzate. Tenere presente che i valori iniziali vengono recuperati dall'area costante. L'elaborazione dell'inizializzazione esatta è specifica dello strumento di sviluppo.

### <a name="main-function"></a>Main (funzione)

Al termine dell'inizializzazione dello strumento di sviluppo, il controllo viene trasferito alla funzione *principale* fornita dall'utente. A questo punto, l'applicazione controlla cosa accade successivamente. Per la maggior parte delle applicazioni, la funzione Main chiama semplicemente *tx_kernel_enter*, che è la voce in threadX. Tuttavia, le applicazioni possono eseguire l'elaborazione preliminare, in genere per l'inizializzazione dell'hardware, prima di immettere ThreadX.

> [!IMPORTANT]
> *La chiamata a tx_kernel_enter non restituisce, quindi non inserire alcuna elaborazione dopo di essa.*

### <a name="tx_kernel_enter"></a>tx_kernel_enter

La funzione entry coordina l'inizializzazione di varie strutture di dati ThreadX interne, quindi chiama la funzione di definizione dell'applicazione ***tx_application_define***.

Quando ***tx_application_define*** restituisce, il controllo viene trasferito al ciclo di pianificazione dei thread. Questa operazione contrassegna la fine dell'inizializzazione.

### <a name="application-definition-function"></a>Funzione definizione applicazione

La funzione ***tx_application_define*** definisce tutti i thread dell'applicazione, le code, i semafori, i mutex, i flag di evento, i pool di memoria e i timer iniziali. È anche possibile creare ed eliminare le risorse di sistema dai thread durante il normale funzionamento dell'applicazione. Tuttavia, tutte le risorse dell'applicazione iniziale sono definite qui.

La funzione ***tx_application_define** _ ha un solo parametro di input e certamente vale la pena citare. L'indirizzo di RAM * disponibile _first è l'unico parametro di input per questa funzione. Viene in genere utilizzato come punto di partenza per le allocazioni di memoria di runtime iniziali di stack di thread, code e pool di memoria.

> [!NOTE]
> *Al termine dell'inizializzazione, solo un thread in esecuzione può creare ed eliminare le risorse di sistema, inclusi gli altri thread. Per questo motivo, durante l'inizializzazione deve essere creato almeno un thread.*

### <a name="interrupts"></a>Interrompe

Gli interrupt vengono lasciati disabilitati durante l'intero processo di inizializzazione. Se l'applicazione è in grado di consentire interruzioni, potrebbe verificarsi un comportamento imprevedibile. Nella figura 4 viene illustrato l'intero processo di inizializzazione, dal ripristino del sistema tramite l'inizializzazione specifica dell'applicazione.

## <a name="thread-execution"></a>Esecuzione thread

La pianificazione e l'esecuzione dei thread dell'applicazione sono l'attività più importante di ThreadX. Un thread viene in genere definito come segmento di programma parzialmente indipendente con uno scopo dedicato. L'elaborazione combinata di tutti i thread crea un'applicazione.

I thread vengono creati dinamicamente chiamando ***tx_thread_create** _ durante l'inizializzazione o durante l'esecuzione del thread. I thread vengono creati in uno stato _ready * o *sospeso* .

![Processo di inizializzazione](./media/user-guide/initialization-process.png)

**FIGURA 4. Processo di inizializzazione**

### <a name="thread-execution-states"></a>Stati di esecuzione thread

Comprendere i diversi Stati di elaborazione dei thread è un ingrediente chiave per comprendere l'intero ambiente multithread. In ThreadX sono presenti cinque Stati di thread distinti: *pronto*, *sospeso*, in *esecuzione*, *terminato* e *completato*. Nella figura 5 viene illustrato il diagramma di transizione dello stato del thread per ThreadX.

![Transizione dello stato del thread](./media/user-guide/thread-state-transition.png)

**FIGURA 5. Transizione dello stato del thread**

Un thread si trova in uno stato *pronto* quando è pronto per l'esecuzione. Un thread pronto non viene eseguito fino a quando non è il thread con priorità più elevata nello stato Ready. In questo caso, ThreadX esegue il thread, che quindi modifica lo stato in in *esecuzione*.

Se un thread con priorità più alta diventa pronto, il thread in esecuzione torna a uno stato *pronto* . Viene quindi eseguito il thread ad alta priorità appena pronto, che modifica lo stato logico in *esecuzione*. Questa transizione tra gli stati *pronto* ed *esecuzione* si verifica ogni volta che si verifica l'interruzione del thread.

In un momento specifico, solo un thread è in *esecuzione* . Questo perché un thread nello stato in *esecuzione* ha il controllo del processore sottostante.

I thread in stato *sospeso* non sono idonei per l'esecuzione. I motivi per essere *sospesi* includono la sospensione per il tempo, i messaggi della coda, i semafori, i mutex, i flag di evento, la memoria e la sospensione di thread di base. Una volta rimossa la provocazione della sospensione, il thread viene nuovamente inserito in uno stato *pronto* .

Un thread in stato *completato* è un thread che ha completato l'elaborazione e restituito dalla relativa funzione entry. La funzione entry viene specificata durante la creazione del thread. Un thread in stato *completato* non può essere eseguito nuovamente.

Un thread è in uno stato *terminato* perché un altro thread o il thread stesso ha chiamato il servizio *tx_thread_terminate* . Un thread in uno stato *terminato* non può essere eseguito nuovamente.

> [!IMPORTANT]
> *Se si desidera riavviare un thread completato o terminato, l'applicazione deve innanzitutto eliminare il thread. Può quindi essere ricreato e riavviato.*

### <a name="thread-entryexit-notification"></a>Notifica voce/uscita thread

Per alcune applicazioni può risultare vantaggioso ricevere una notifica quando viene immesso un thread specifico per la prima volta, quando viene completato o terminato. ThreadX offre questa possibilità tramite il servizio ***tx_thread_entry_exit_notify*** . Questo servizio registra una funzione di notifica dell'applicazione per un thread specifico, che viene chiamato da ThreadX ogni volta che il thread inizia l'esecuzione, viene completato o viene terminato. Dopo essere stato richiamato, la funzione di notifica dell'applicazione può eseguire l'elaborazione specifica dell'applicazione. Ciò comporta in genere l'informazione di un altro thread dell'evento tramite una primitiva di sincronizzazione ThreadX.

### <a name="thread-priorities"></a>Priorità dei thread

Come indicato in precedenza, un thread è un segmento di programma parzialmente indipendente con uno scopo dedicato. Tuttavia, tutti i thread non vengono creati uguali. Lo scopo dedicato di alcuni thread è molto più importante di altri. Questo tipo eterogeneo di importanza dei thread è una caratteristica delle applicazioni incorporate in tempo reale.

ThreadX determina l'importanza di un thread quando il thread viene creato assegnando un valore numerico che rappresenta la *priorità*. Il numero massimo di priorità di ThreadX è configurabile da 32 a 1024 con incrementi di 32. Il numero massimo effettivo di priorità è determinato dalla costante **TX_MAX_PRIORITIES** durante la compilazione della libreria threadX. La presenza di un numero maggiore di priorità non comporta un aumento significativo del sovraccarico di elaborazione. Tuttavia, per ogni gruppo di 32 livelli di priorità, per gestirli sono necessari 128 byte aggiuntivi di RAM. Ad esempio, 32 livelli di priorità richiedono 128 byte di RAM, 64 livelli di priorità richiedono 256 byte di RAM e i livelli di priorità 96 richiedono 384 byte di RAM.

Per impostazione predefinita, ThreadX dispone di 32 livelli di priorità, che vanno dalla priorità 0 alla priorità 31. Valori numericamente inferiori implicano una priorità più elevata. Di conseguenza, Priority 0 rappresenta la priorità più alta, mentre Priority (**TX_MAX_PRIORITIES**-1) rappresenta la priorità più bassa.

Più thread possono avere la stessa priorità basandosi sulla pianificazione cooperativa o sul sezionamento dei tempi. Inoltre, le priorità del thread possono essere modificate in fase di esecuzione.

### <a name="thread-scheduling"></a>Pianificazione di thread

ThreadX Pianifica i thread in base alla priorità. Il thread pronto con la priorità più alta viene eseguito per primo. Se sono pronti più thread con la stessa priorità, vengono eseguiti in modalità FIFO ( *First-in-First-out* ).

### <a name="round-robin-scheduling"></a>Pianificazione Round Robin

ThreadX supporta la pianificazione *Round Robin* di più thread con la stessa priorità. Questa operazione viene eseguita tramite chiamate cooperative a ***tx_thread_relinquish** _. Questo servizio fornisce a tutti gli altri thread pronti con la stessa priorità la possibilità di eseguire prima che il chiamante _ *_tx_thread_relinquish_** venga eseguito nuovamente.

### <a name="time-slicing"></a>Time-Slicing

Il *sezionamento del tempo* è un altro tipo di pianificazione Round Robin. Una sezione di tempo specifica il numero massimo di cicli timer (interrupt timer) che un thread può eseguire senza rinunciare al processore. In ThreadX, il sezionamento del tempo è disponibile in base ai singoli thread. La sezione relativa al tempo del thread viene assegnata durante la creazione e può essere modificata in fase di esecuzione. Alla scadenza di un intervallo di tempo, tutti gli altri thread pronti con lo stesso livello di priorità hanno la possibilità di eseguire prima di eseguire di nuovo il thread con sezionamento del tempo.

Una sezione del tempo del thread aggiornata viene assegnata a un thread dopo la sospensione, cede, effettua una chiamata al servizio ThreadX che causa la precedenza o è a sua volta sezionata.

Quando un thread con sezionamento temporale viene interrotto, riprenderà prima di altri thread pronti con uguale priorità per il resto della relativa sezione di tempo.

> [!NOTE]
> *L'uso del sezionamento del tempo comporta una lieve quantità di overhead del sistema. Poiché il sezionamento del tempo è utile solo nei casi in cui più thread condividono la stessa priorità, non è necessario assegnare un intervallo di tempo ai thread con una priorità univoca.*

### <a name="preemption"></a>Precedenza

La precedenza è il processo di interruzione temporanea di un thread in esecuzione a favore di un thread con priorità più alta. Questo processo è invisibile al thread in esecuzione. Quando il thread con priorità più alta è terminato, il controllo viene trasferito di nuovo alla posizione esatta in cui è avvenuta la precedenza. Si tratta di una funzionalità molto importante nei sistemi in tempo reale perché semplifica la risposta rapida a eventi importanti dell'applicazione. Sebbene una funzionalità molto importante, la precedenza può anche costituire un'origine di diversi problemi, tra cui inedia, sovraccarico eccessivo e inversione con priorità.

### <a name="preemption-thresholdtrade"></a>Soglia di precedenza&trade;

Per semplificare alcuni dei problemi intrinseci di precedenza, ThreadX offre una funzionalità univoca e avanzata denominata *precedenza-soglia*.

Una soglia di precedenza consente a un thread di specificare un *limite* di priorità per la disabilitazione della precedenza. I thread con priorità più elevata rispetto al limite massimo possono comunque essere interrotti, mentre quelli inferiori al limite massimo non sono consentiti per l'interruzione.

Si supponga, ad esempio, che un thread con priorità 20 interagisca solo con un gruppo di thread con priorità compresa tra 15 e 20. Durante le sezioni critiche, il thread della priorità 20 può impostare la soglia di precedenza su 15, impedendo in tal modo la precedenza da tutti i thread con cui interagisce. Questo consente comunque ai thread molto importanti (priorità tra 0 e 14) di precedere questo thread durante la relativa elaborazione della sezione critica, che comporta un'elaborazione molto più reattiva.

Naturalmente, è ancora possibile per un thread disabilitare la precedenza impostando la relativa soglia di precedenza su 0. Inoltre, la soglia di precedenza può essere modificata in fase di esecuzione.

> [!NOTE]
> *Con la soglia di precedenza viene disabilitato il sezionamento del tempo per il thread specificato.*

### <a name="priority-inheritance"></a>Ereditarietà priorità

ThreadX supporta anche l'ereditarietà della priorità facoltativa nei servizi mutex descritti più avanti in questo capitolo. L'ereditarietà della priorità consente a un thread con priorità inferiore di assumere temporaneamente la priorità di un thread con priorità alta in attesa di un mutex di proprietà del thread con priorità inferiore. Questa funzionalità consente all'applicazione di evitare l'inversione di priorità non deterministica eliminando la precedenza delle priorità del thread intermedio. Naturalmente, è possibile usare la *soglia di precedenza* per ottenere un risultato simile.

### <a name="thread-creation"></a>Creazione di thread

I thread dell'applicazione vengono creati durante l'inizializzazione o durante l'esecuzione di altri thread dell'applicazione. Non esiste alcun limite al numero di thread che possono essere creati da un'applicazione.

### <a name="thread-control-block-tx_thread"></a>TX_THREAD blocchi di controllo thread

Le caratteristiche di ogni thread sono contenute nel relativo blocco di controllo. Questa struttura viene definita nel file ***tx_api. h*** .

Il blocco di controllo di un thread può trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendolo al di fuori dell'ambito di qualsiasi funzione.

Per individuare il blocco di controllo in altre aree, è necessario prestare maggiore attenzione, come per tutta la memoria allocata in modo dinamico. Se un blocco di controllo viene allocato all'interno di una funzione C, la memoria associata è parte dello stack del thread chiamante. In generale, evitare di usare l'archiviazione locale per i blocchi di controllo perché, dopo la restituzione della funzione, viene rilasciato tutto lo spazio dello stack della variabile locale, indipendentemente dal fatto che venga usato da un altro thread per un blocco di controllo.

Nella maggior parte dei casi, l'applicazione è ignara del contenuto del blocco di controllo del thread. Tuttavia, esistono alcune situazioni, soprattutto durante il debug, in cui è utile esaminare alcuni membri. Di seguito sono riportati alcuni dei più utili membri del blocco di controllo.

**tx_thread_run_count** contiene un contatore del numero di volte in cui il thread è stato pianificato. Un contatore crescente indica che è in corso la pianificazione e l'esecuzione del thread.

**tx_thread_state** contiene lo stato del thread associato. Di seguito sono elencati i possibili stati dei thread.

|  Stato thread   | Valore |
| --------------- | ------ |
| TX_READY       | 0x00 |
| TX_COMPLETED   | 0x01 |
| TX_TERMINATED  | 0x02 |
| TX_SUSPENDED   | 0x03 |
| TX_SLEEP       | 0x04 |
| TX_QUEUE_SUSP | 0x05 |
| TX_SEMAPHORE_SUSP | 0x06 |
| TX_EVENT_FLAG   | 0x07 |
| TX_BLOCK_MEMORY | 0x08 |
| TX_BYTE_MEMORY  | 0x09 |
| TX_MUTEX_SUSP   | 0X0D |

> [!NOTE]
> *Naturalmente, esistono molti altri campi interessanti nel blocco di controllo dei thread, tra cui il puntatore dello stack, il valore della sezione temporale, le priorità e così via. Gli utenti sono invitati a esaminare i membri del blocco di controllo, ma le modifiche sono rigorosamente proibite.*

> [!IMPORTANT]
> Non *esiste alcuna uguaglianza per lo stato "in esecuzione" indicato in precedenza in questa sezione. Non è necessario perché esiste solo un thread in esecuzione in un determinato momento. Anche lo stato di un thread in esecuzione è* **TX_READY**.

### <a name="currently-executing-thread"></a>Thread attualmente in esecuzione

Come indicato in precedenza, è in esecuzione un solo thread in un determinato momento. Esistono diversi modi per identificare il thread in esecuzione, a seconda del thread che sta effettuando la richiesta.
Un segmento di programma può ottenere l'indirizzo del blocco di controllo del thread in esecuzione chiamando ***tx_thread_identify***. Questa operazione è utile nelle parti condivise del codice dell'applicazione eseguite da più thread.

Nelle sessioni di debug gli utenti possono esaminare il puntatore ThreadX interno ***_tx_thread_current_ptr***. Contiene l'indirizzo del blocco di controllo del thread attualmente in esecuzione. Se questo puntatore è NULL, non è in esecuzione alcun thread dell'applicazione; ovvero, ThreadX è in attesa nel ciclo di pianificazione affinché un thread diventi pronto.

### <a name="thread-stack-area"></a>Area stack di thread

Ogni thread deve avere un proprio stack per salvare il contesto dell'ultima esecuzione e l'utilizzo del compilatore. La maggior parte dei compilatori C usa lo stack per eseguire chiamate di funzione e allocare temporaneamente le variabili locali. Nella figura 6 viene illustrato lo stack di un thread tipico.

Quando uno stack di thread si trova in memoria è all'interno dell'applicazione. L'area dello stack viene specificata durante la creazione del thread e può trovarsi in qualsiasi punto dello spazio degli indirizzi della destinazione. Si tratta di una funzionalità importante perché consente alle applicazioni di migliorare le prestazioni dei thread importanti inserendo lo stack in RAM ad alta velocità.

**Area memoria dello stack** (esempio)

![Stack di thread tipico](./media/user-guide/typical-thread-stack.png)

**FIGURA 6. Stack di thread tipico**

La dimensione di uno stack è una delle domande più frequenti sui thread. L'area dello stack di un thread deve essere sufficientemente grande da contenere la nidificazione della chiamata di funzione peggiore, l'allocazione delle variabili locali e il salvataggio dell'ultimo contesto di esecuzione.

La dimensione minima dello stack, **TX_MINIMUM_STACK**, è definita da threadX. Uno stack di queste dimensioni supporta il salvataggio del contesto di un thread e la quantità minima di chiamate di funzione e l'allocazione delle variabili locali.

Per la maggior parte dei thread, tuttavia, la dimensione minima dello stack è troppo piccola e l'utente deve verificare il requisito delle dimensioni peggiori esaminando la nidificazione delle chiamate di funzione e l'allocazione delle variabili locali. Naturalmente, è sempre preferibile iniziare con un'area dello stack più ampia.

Quando l'applicazione viene sottoposta a debug, è possibile ottimizzare le dimensioni dello stack di thread se la memoria è limitata. Un trucco preferito consiste nel preimpostare tutte le aree dello stack con un modello di dati facilmente identificabile, ad esempio (0xEFEF) prima della creazione dei thread. Dopo aver completato l'applicazione, è possibile esaminare le aree dello stack per verificare la quantità di stack effettivamente utilizzata individuando l'area dello stack in cui il modello di dati è ancora intatto. La figura 7 Mostra un set di impostazioni dello stack da 0xEFEF dopo l'esecuzione completa del thread.

**Area memoria dello stack** (un altro esempio)

![Imposta lo stack su 0xEFEF *](./media/user-guide/stack-preset.png)

**FIGURA 7. Imposta lo stack su 0xEFEF**

> [!IMPORTANT]
> *Per impostazione predefinita, ThreadX Inizializza ogni byte di ogni stack di thread con un valore di 0xEF.*

### <a name="memory-pitfalls"></a>Problemi di memoria

I requisiti dello stack per i thread possono essere di grandi dimensioni. Pertanto, è importante progettare l'applicazione in modo che disponga di un numero ragionevole di thread. Inoltre, è necessario prestare attenzione per evitare un utilizzo eccessivo dello stack nei thread. Gli algoritmi ricorsivi e le strutture di dati locali di grandi dimensioni devono essere evitati.

Nella maggior parte dei casi, uno stack con overflow causa la danneggiamento della memoria adiacente (in genere prima) dell'area dello stack da parte dell'esecuzione del thread. I risultati sono imprevedibili, ma la maggior parte delle volte comporta una modifica non naturale del contatore del programma. Questa operazione viene spesso definita "passaggio alle erbacce". Naturalmente, l'unico modo per evitare questo problema è garantire che tutti gli stack di thread siano sufficientemente grandi.

### <a name="optional-run-time-stack-checking"></a>Controllo dello stack di run-time facoltativo

ThreadX consente di controllare il danneggiamento dello stack di ogni thread durante la fase di esecuzione. Per impostazione predefinita, ThreadX riempie ogni byte di stack di thread con un modello di dati 0xEF durante la creazione. Se l'applicazione compila la libreria ThreadX con **TX_ENABLE_STACK_CHECKING** definito, threadX esaminerà lo stack di ogni thread per danneggiarlo mentre viene sospeso o ripreso. Se viene rilevato un danneggiamento dello stack, ThreadX chiamerà la routine di gestione degli errori dello stack dell'applicazione come specificato dalla chiamata a **_tx_thread_stack_error_notify_*_. In caso contrario, se non è stato specificato alcun gestore di errori dello stack, ThreadX chiamerà la routine interna _* _ _tx_thread_stack_error_handler_** .

### <a name="reentrancy"></a>Rientranza

Una delle bellezze reali del multithreading è che la stessa funzione C può essere chiamata da più thread. Ciò garantisce grande potenza e contribuisce inoltre a ridurre lo spazio di codice. Tuttavia, richiede che le funzioni C chiamate da più thread siano *rientranti*.

In sostanza, una funzione rientrante archivia l'indirizzo mittente del chiamante nello stack corrente e non si basa sulle variabili C globali o statiche impostate in precedenza. La maggior parte dei compilatori inserisce l'indirizzo mittente nello stack. Di conseguenza, gli sviluppatori di applicazioni devono preoccuparsi solo dell'utilizzo di *Globals* e *static*.

Un esempio di funzione non rientrante è la funzione token di stringa ***strtok*** trovata nella libreria C standard. Questa funzione "ricorda" il puntatore di stringa precedente nelle chiamate successive. Questa operazione viene eseguita con un puntatore di stringa statico. Se questa funzione viene chiamata da più thread, è molto probabile che restituisca un puntatore non valido.

### <a name="thread-priority-pitfalls"></a>Problemi relativi alla priorità del thread

La selezione delle priorità dei thread è uno degli aspetti più importanti del multithreading. Talvolta è molto difficile assegnare le priorità in base a una nozione percepita di importanza dei thread, anziché determinare cosa è esattamente necessario durante la fase di esecuzione. L'utilizzo improprio delle priorità dei thread può infame altri thread, creare inversione con priorità, ridurre la larghezza di banda di elaborazione e rendere difficile la comprensione del comportamento in fase di esecuzione dell'applicazione.

Come indicato in precedenza, ThreadX fornisce un algoritmo di pianificazione preemptive basato sulla priorità. I thread con priorità inferiore non vengono eseguiti fino a quando non sono presenti thread con priorità più elevata pronti per l'esecuzione. Se un thread con priorità più alta è sempre pronto, i thread con priorità inferiore non vengono mai eseguiti. Questa condizione è detta *inedia del thread*.

La maggior parte dei problemi di inedia dei thread viene rilevata all'inizio del debug e può essere risolta garantendo che i thread con priorità più alta non vengano In alternativa, è possibile aggiungere la logica all'applicazione che aumenta gradualmente la priorità dei thread affamati fino a quando non avranno la possibilità di eseguire.

Un altro trabocchetto associato alle priorità dei thread è l' *inversione della priorità*. L'inversione della priorità avviene quando un thread con priorità più alta viene sospeso perché un thread con priorità inferiore ha una risorsa necessaria. Naturalmente, in alcuni casi è necessario che due thread con priorità diversa condividano una risorsa comune. Se questi thread sono gli unici attivi, il tempo di inversione della priorità è limitato dal tempo in cui il thread con priorità inferiore include la risorsa. Questa condizione è deterministica e abbastanza normale. Tuttavia, se i thread della priorità intermedia diventano attivi durante questa condizione di inversione della priorità, il tempo di inversione della priorità non è più deterministico e potrebbe causare un errore dell'applicazione.

Esistono principalmente tre metodi distinti per impedire l'inversione di priorità non deterministica in ThreadX. In primo luogo, le selezioni per la priorità dell'applicazione e il comportamento in fase di esecuzione possono essere progettate in modo da evitare il problema di inversione della priorità. In secondo luogo, i thread con priorità più bassa possono utilizzare la *soglia di precedenza* per bloccare la precedenza dai thread intermedi mentre condividono risorse con thread con priorità più elevata. Infine, i thread che usano gli oggetti mutex ThreadX per proteggere le risorse di sistema possono usare l' *ereditarietà della priorità* mutex facoltativa per eliminare l'inversione della priorità non deterministica.

### <a name="priority-overhead"></a>Overhead priorità

Uno dei modi più trascurati per ridurre l'overhead nel multithreading consiste nel ridurre il numero di cambi di contesto. Come indicato in precedenza, un cambio di contesto si verifica quando l'esecuzione di un thread con priorità più alta è favorita rispetto a quella del thread in esecuzione. È opportuno ricordare che i thread con priorità più elevata possono diventare pronti a causa di eventi esterni (ad esempio, interrupt) e di chiamate al servizio eseguite dal thread in esecuzione.

Per illustrare le priorità dei thread degli effetti sul sovraccarico del cambio di contesto, si supponga un ambiente a tre thread con thread denominati *Thread_1*, *Thread_2* e *Thread_3*. Si supponga inoltre che tutti i thread siano in uno stato di sospensione in attesa di un messaggio. Quando thread_1 riceve un messaggio, lo inoltra immediatamente a thread_2. Thread_2 quindi trasmette il messaggio al thread_3. Thread_3 semplicemente Elimina il messaggio. Dopo l'elaborazione del messaggio da parte di ogni thread, viene riattivato e rimane in attesa di un altro messaggio.

L'elaborazione necessaria per eseguire questi tre thread varia notevolmente a seconda delle priorità. Se tutti i thread hanno la stessa priorità, prima dell'esecuzione di ogni thread viene eseguito un singolo cambio di contesto. Il cambio di contesto si verifica quando ogni thread viene sospeso in una coda di messaggi vuota.

Tuttavia, se thread_2 ha una priorità più elevata rispetto a thread_1 e thread_3 ha una priorità più elevata rispetto a thread_2, il numero di cambi di contesto raddoppia. Questo è dovuto al fatto che un'altra opzione di contesto si verifica all'interno del servizio *tx_queue_send* quando rileva che un thread con priorità più alta è ora pronto.

Il meccanismo di soglia di precedenza ThreadX può evitare questi cambi di contesto aggiuntivi e consentire comunque le selezioni di priorità indicate in precedenza. Si tratta di una funzionalità importante perché consente numerose priorità dei thread durante la pianificazione, eliminando allo stesso tempo parte del contesto indesiderato che passa tra di essi durante l'esecuzione del thread.

### <a name="run-time-thread-performance-information"></a>Informazioni sulle prestazioni del thread in fase di esecuzione

ThreadX fornisce informazioni facoltative sulle prestazioni del thread in fase di esecuzione. Se la libreria e l'applicazione ThreadX sono compilate con **TX_THREAD_ENABLE_PERFORMANCE_INFO** definito, threadX accumula le informazioni seguenti.

Numero totale per il sistema globale:

  - riprese di thread

  - sospensioni di thread

  - prelazioni delle chiamate al servizio

  - interruzioni di interrupt

  - inversioni di priorità

  - sezioni temporali

  - cede

  - Timeout thread

  - interruzioni di sospensione

  - il sistema inattivo restituisce

  - Restituisce il sistema non inattivo

Numero totale per ogni thread:

  - delle riprese

  - sospensioni

  - prelazioni delle chiamate al servizio

  - interruzioni di interrupt

  - inversioni di priorità

  - sezioni temporali

  - il thread cede

  - Timeout thread

  - interruzioni di sospensione

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi ***tx_thread_performance_info_get** _ e _ *_tx_thread_performance_system_info_get_* *. Le informazioni sulle prestazioni dei thread sono utili per determinare se l'applicazione funziona correttamente. È utile anche per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di prelazioni della chiamata al servizio potrebbe indicare che la priorità e/o la soglia di precedenza del thread è troppo bassa. Inoltre, un numero relativamente basso di ritorni di sistema inattivi potrebbe indicare che i thread con priorità inferiore non sono sufficientemente sospesi.

### <a name="debugging-pitfalls"></a>Problemi di debug

Il debug di applicazioni multithread è un po' più difficile perché lo stesso codice programma può essere eseguito da più thread. In questi casi, un punto di rottura da solo potrebbe non essere sufficiente. Il debugger deve anche visualizzare il puntatore al thread corrente **_tx_thread_current_ptr** usando un punto di interruzione condizionale per verificare se il thread chiamante è quello di cui eseguire il debug.

Molti di questi vengono gestiti nei pacchetti di supporto per il multithreading offerti attraverso diversi fornitori di strumenti di sviluppo. Grazie alla progettazione semplice, l'integrazione di ThreadX con diversi strumenti di sviluppo è relativamente semplice.

La dimensione dello stack è sempre un argomento di debug importante nel multithreading. Ogni volta che viene osservato un comportamento inspiegabile, in genere è opportuno aumentare le dimensioni dello stack per tutti i thread, in particolare le dimensioni dello stack dell'ultimo thread da eseguire.

> [!TIP]
> *È inoltre consigliabile compilare la libreria ThreadX con **TX_ENABLE_STACK_CHECKING** definito. Questo consente di isolare i problemi di danneggiamento dello stack nel minor tempo possibile nell'elaborazione.*

## <a name="message-queues"></a>Code di messaggi

Le code di messaggi sono il mezzo principale per la comunicazione tra thread in ThreadX. Uno o più messaggi possono risiedere in una coda di messaggi. Una coda di messaggi che include un singolo messaggio è comunemente denominata *cassetta postale*.

I messaggi vengono copiati in una coda per ***tx_queue_send** _ e vengono copiati da una coda di _ *_tx_queue_receive_* *. L'unica eccezione è rappresentata dal momento in cui un thread viene sospeso in attesa di un messaggio in una coda vuota. In questo caso, il messaggio successivo inviato alla coda viene inserito direttamente nell'area di destinazione del thread.

Ogni coda di messaggi è una risorsa pubblica. ThreadX non impone vincoli sulla modalità di utilizzo delle code di messaggi.

### <a name="creating-message-queues"></a>Creazione di code di messaggi

Le code di messaggi vengono create durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Non esiste alcun limite al numero di code di messaggi in un'applicazione.

### <a name="message-size"></a>Dimensioni del messaggio

Ogni coda di messaggi supporta una serie di messaggi a dimensione fissa. Le dimensioni dei messaggi disponibili sono comprese tra 1 e 16 32 bit. La dimensione del messaggio viene specificata quando viene creata la coda. I messaggi dell'applicazione con dimensioni maggiori di 16 parole devono essere passati dal puntatore. Questa operazione viene eseguita tramite la creazione di una coda con una dimensione del messaggio di 1 parola (sufficiente per mantenere un puntatore) e quindi l'invio e la ricezione di puntatori ai messaggi anziché dell'intero messaggio.

### <a name="message-queue-capacity"></a>Capacità coda messaggi

Il numero di messaggi che una coda può mantenere è una funzione delle dimensioni del messaggio e le dimensioni dell'area di memoria fornita durante la creazione. La capacità totale dei messaggi della coda viene calcolata dividendo il numero di byte in ogni messaggio nel numero totale di byte nell'area di memoria specificata.

Se, ad esempio, viene creata una coda di messaggi che supporta una dimensione del messaggio di Word a 1 32 bit (4 byte) con un'area di memoria di 100 byte, la relativa capacità è di 25 messaggi.

### <a name="queue-memory-area"></a>Area memoria coda

Come indicato in precedenza, l'area di memoria per i messaggi di buffering viene specificata durante la creazione della coda. Analogamente ad altre aree di memoria in ThreadX, può trovarsi in qualsiasi punto dello spazio degli indirizzi della destinazione.

Si tratta di una funzionalità importante perché garantisce una notevole flessibilità all'applicazione. Ad esempio, un'applicazione potrebbe individuare l'area di memoria di una coda importante in RAM ad alta velocità per migliorare le prestazioni.

### <a name="thread-suspension"></a>Sospensione thread

I thread dell'applicazione possono essere sospesi durante il tentativo di inviare o ricevere un messaggio da una coda. In genere, la sospensione dei thread prevede l'attesa di un messaggio da una coda vuota. Tuttavia, è anche possibile che un thread sospenda il tentativo di inviare un messaggio a una coda completa.

Una volta risolta la condizione per la sospensione, il servizio richiesto viene completato e il thread in attesa viene ripreso. Se più thread sono sospesi nella stessa coda, vengono ripresi nell'ordine in cui sono stati sospesi (FIFO).

Tuttavia, la ripresa della priorità è possibile anche se l'applicazione chiama ***tx_queue_prioritize*** prima del servizio di accodamento che solleva la sospensione del thread. Il servizio accoda priorità posiziona il thread con priorità più alta all'inizio dell'elenco di sospensioni, lasciando tutti gli altri thread sospesi nello stesso ordine FIFO.

I timeout sono disponibili anche per tutte le sospensioni della coda. In sostanza, un timeout specifica il numero massimo di cicli del timer che il thread resterà sospeso. Se si verifica un timeout, il thread viene ripreso e il servizio restituisce con il codice di errore appropriato.

### <a name="queue-send-notification"></a>Notifica di invio della coda

Alcune applicazioni potrebbero risultare vantaggioso ricevere notifiche ogni volta che un messaggio viene inserito in una coda. ThreadX offre questa possibilità tramite il servizio ***tx_queue_send_notify*** . Questo servizio registra la funzione di notifica dell'applicazione fornita con la coda specificata. ThreadX richiamerà successivamente questa funzione di notifica dell'applicazione ogni volta che un messaggio viene inviato alla coda. L'elaborazione esatta all'interno della funzione di notifica dell'applicazione è determinata dall'applicazione; Tuttavia, in genere è costituito dalla ripresa del thread appropriato per l'elaborazione del nuovo messaggio.

### <a name="queue-event-chainingtrade"></a>Concatenamento di eventi in coda&trade;

Le funzionalità di notifica in ThreadX possono essere usate per concatenare diversi eventi di sincronizzazione. Questa operazione è in genere utile quando un singolo thread deve elaborare più eventi di sincronizzazione.

Si supponga, ad esempio, che un singolo thread sia responsabile dell'elaborazione dei messaggi da cinque code diverse ed è necessario sospenderlo anche quando non sono disponibili messaggi. Questa operazione viene eseguita facilmente registrando una funzione di notifica dell'applicazione per ogni coda e introducendo un semaforo di conteggio aggiuntivo. In particolare, la funzione di notifica dell'applicazione esegue un *tx_semaphore_put* ogni volta che viene chiamato (il conteggio dei semafori rappresenta il numero totale di messaggi in tutte e cinque le code). Il thread di elaborazione sospende in questo semaforo tramite il servizio *tx_semaphore_get* . Quando il semaforo è disponibile (in questo caso, quando è disponibile un messaggio), il thread di elaborazione viene ripreso. Interroga quindi ogni coda per un messaggio, elabora il messaggio trovato ed esegue un'altra ***tx_semaphore_get*** per attendere il messaggio successivo. Eseguire questa operazione senza concatenamento di eventi è piuttosto difficile e probabilmente richiederebbe più thread e/o codice dell'applicazione aggiuntivo.

In generale, il *concatenamento degli eventi* comporta un minor numero di thread, minore overhead e requisiti di RAM inferiori. Fornisce inoltre un meccanismo estremamente flessibile per gestire i requisiti di sincronizzazione di sistemi più complessi.

### <a name="run-time-queue-performance-information"></a>Informazioni sulle prestazioni della coda di runtime
ThreadX fornisce informazioni sulle prestazioni della coda di runtime facoltative. Se la libreria e l'applicazione ThreadX sono compilate con ***TX_QUEUE_ENABLE_PERFORMANCE_INFO*** definito, threadX accumula le informazioni seguenti.

Numero totale per il sistema globale:

  - messaggi inviati

  - messaggi ricevuti

  - sospendere le sospensioni vuote

  - sospensione completa della coda

  - ritorni errore coda completa (sospensione non specificata)

  - timeout della coda

Numero totale per ogni coda:

  - messaggi inviati

  - messaggi ricevuti

  - sospendere le sospensioni vuote

  - sospensione completa della coda

  - ritorni errore coda completa (sospensione non specificata)

  - timeout della coda

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi ***tx_queue_performance_info_get** _ e _ *_tx_queue_performance_system_info_get_* *. Le informazioni sulle prestazioni della coda sono utili per determinare se l'applicazione funziona correttamente. È utile anche per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di "sospensioni complete della coda" suggerisce un aumento delle dimensioni della coda può risultare vantaggioso.

### <a name="queue-control-block-tx_queue"></a>TX_QUEUE blocchi di controllo della coda

Le caratteristiche di ogni coda di messaggi sono disponibili nel relativo blocco di controllo. Contiene informazioni interessanti, ad esempio il numero di messaggi nella coda. Questa struttura viene definita nel file ***tx_api. h*** .

I blocchi di controllo della coda di messaggi possono anche trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendola al di fuori dell'ambito di qualsiasi funzione.

### <a name="message-destination-pitfall"></a>Insidia destinazione messaggio

Come indicato in precedenza, i messaggi vengono copiati tra l'area della coda e le aree dati dell'applicazione. È importante assicurarsi che la destinazione di un messaggio ricevuto sia sufficientemente grande da poter conservare l'intero messaggio. In caso contrario, la memoria che segue la destinazione del messaggio sarà probabilmente danneggiata.

> [!NOTE]
> *Questa operazione è particolarmente letale quando una destinazione di messaggio troppo piccola è nello stack, nulla come il danneggiamento dell'indirizzo di ritorno di una funzione.*

## <a name="counting-semaphores"></a>Conteggio dei semafori

ThreadX fornisce semaforo di conteggio a 32 bit che variano in valore compreso tra 0 e 4.294.967.295. Per il conteggio dei semafori sono disponibili due operazioni: *tx_semaphore_get* e *tx_semaphore_put*. L'operazione Get riduce il semaforo di uno. Se il semaforo è 0, l'operazione get ha esito negativo. L'inverso dell'operazione get è l'operazione Put.
Il semaforo aumenta di uno.

Ogni semaforo di conteggio è una risorsa pubblica. ThreadX non impone vincoli sul conteggio dei semafori utilizzati.

Il conteggio dei semafori viene in genere usato per l' *esclusione reciproca*. Tuttavia, il conteggio dei semafori può essere usato anche come metodo per la notifica degli eventi.

### <a name="mutual-exclusion"></a>Esclusione reciproca

 L'esclusione reciproca riguarda il controllo dell'accesso dei thread a determinate aree dell'applicazione, denominate anche *sezioni critiche* o *risorse dell'applicazione*. Quando viene usato per l'esclusione reciproca, il "conteggio corrente" di un semaforo rappresenta il numero totale di thread a cui è consentito l'accesso. Nella maggior parte dei casi, il conteggio dei semafori usati per l'esclusione reciproca avrà un valore iniziale pari a 1, ovvero un solo thread può accedere alla risorsa associata alla volta. Il conteggio dei semafori che hanno solo valori 0 o 1 viene comunemente chiamato *semaforo binario*.

> [!IMPORTANT]
> *Se viene usato un semaforo binario, l'utente deve impedire allo stesso thread di eseguire un'operazione get su un semaforo di cui è già proprietario. Un secondo Get non ha avuto esito positivo e potrebbe causare una sospensione indefinita del thread chiamante e l'indisponibilità permanente della risorsa.*

### <a name="event-notification"></a>Notifica dell'evento

È anche possibile usare il conteggio dei semafori come notifica degli eventi, in modo da producer-consumer. Il consumer tenta di ottenere il semaforo di conteggio mentre il produttore aumenta il semaforo ogni volta che è disponibile qualcosa. Questi semafori hanno in genere un valore iniziale pari a 0 e non aumentano fino a quando il produttore non ha qualcosa di pronto per l'utente. I semafori usati per la notifica degli eventi possono anche trarre vantaggio dall'uso della chiamata al servizio ***tx_semaphore_ceiling_put*** . Questo servizio garantisce che il numero di semafori non superi mai il valore specificato nella chiamata.

### <a name="creating-counting-semaphores"></a>Creazione di semafori di conteggio

Il conteggio dei semafori viene creato durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Il numero iniziale del semaforo viene specificato durante la creazione. Non esiste alcun limite al numero di semafori in un'applicazione.

### <a name="thread-suspension"></a>Sospensione thread

I thread dell'applicazione possono essere sospesi durante il tentativo di eseguire un'operazione get su un semaforo con un conteggio corrente pari a 0.

Dopo l'esecuzione di un'operazione Put, viene eseguita l'operazione Get del thread sospeso e il thread viene ripreso. Se più thread vengono sospesi nello stesso semaforo di conteggio, vengono ripresi nello stesso ordine in cui sono stati sospesi (FIFO).

Tuttavia, la ripresa della priorità è possibile anche se l'applicazione chiama ***tx_semaphore_prioritize*** prima della chiamata di put del semaforo che solleva la sospensione del thread. Il servizio semaforo priorità posiziona il thread con priorità più alta all'inizio dell'elenco di sospensioni, lasciando tutti gli altri thread sospesi nello stesso ordine FIFO.

### <a name="semaphore-put-notification"></a>Notifica put semaforo

Alcune applicazioni potrebbero risultare vantaggioso ricevere notifiche ogni volta che viene inserito un semaforo. ThreadX offre questa possibilità tramite il servizio ***tx_semaphore_put_notify*** . Questo servizio registra la funzione di notifica dell'applicazione fornita con il semaforo specificato. ThreadX richiamerà successivamente questa funzione di notifica dell'applicazione ogni volta che viene inserito il semaforo. L'elaborazione esatta all'interno della funzione di notifica dell'applicazione è determinata dall'applicazione; Tuttavia, in genere è costituito dalla ripresa del thread appropriato per l'elaborazione del nuovo evento Semaphore put.

### <a name="semaphore-event-chainingtrade"></a>Concatenamento di eventi Semaphore&trade;

Le funzionalità di notifica in ThreadX possono essere usate per concatenare diversi eventi di sincronizzazione. Questa operazione è in genere utile quando un singolo thread deve elaborare più eventi di sincronizzazione.

Ad esempio, anziché avere thread separati sospesi per un messaggio della coda, i flag di evento e un semaforo, l'applicazione può registrare una routine di notifica per ogni oggetto. Quando viene richiamato, la routine di notifica dell'applicazione può riprendere un singolo thread, che può interrogare ogni oggetto per trovare ed elaborare il nuovo evento.

In generale, il *concatenamento degli eventi* comporta un minor numero di thread, minore overhead e requisiti di RAM inferiori. Fornisce inoltre un meccanismo estremamente flessibile per gestire i requisiti di sincronizzazione di sistemi più complessi.

### <a name="run-time-semaphore-performance-information"></a>Informazioni sulle prestazioni del semaforo in fase di esecuzione

ThreadX fornisce informazioni sulle prestazioni del semaforo di run-time facoltative. Se la libreria e l'applicazione ThreadX sono compilate con **TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO** definito, threadX accumula le informazioni seguenti.

Numero totale per il sistema globale:

  - semaforo inserito

  - semaforo ottenuto

  - sospensioni semaforo Get

  - Timeout get semaforo

Numero totale per ogni semaforo:

  - semaforo inserito

  - semaforo ottenuto

  - sospensioni semaforo Get

  - Timeout get semaforo

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi ***tx_semaphore_performance_info_get** _ e _ *_tx_semaphore_performance_system_info_get_* *. Le informazioni sulle prestazioni del semaforo sono utili per determinare se l'applicazione funziona correttamente. È utile anche per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di "Timeout get Semaphore" potrebbe suggerire che altri thread mantengono risorse troppo lunghe.

### <a name="semaphore-control-block-tx_semaphore"></a>TX_SEMAPHORE del blocco di controllo Semaphore

Le caratteristiche di ogni semaforo di conteggio si trovano nel blocco di controllo. Contiene informazioni come il numero corrente di semafori. Questa struttura viene definita nel file ***tx_api. h*** .

I blocchi di controllo Semaphore possono trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendolo al di fuori dell'ambito di qualsiasi funzione.

### <a name="deadly-embrace"></a>Abbraccio mortale

Uno degli ostacoli più interessanti e pericolosi associati ai semafori usati per l'esclusione reciproca è il *mortale* abbandono. Un abbraccio mortale, o un *deadlock*, è una condizione in cui due o più thread vengono sospesi a tempo indefinito durante il tentativo di ottenere i semafori già posseduti l'uno dall'altro.

Questa condizione è illustrata in modo ottimale da un due thread, un esempio di semaforo. Si supponga che il primo thread sia proprietario del primo semaforo e che il secondo thread appartenga al secondo semaforo. Se il primo thread tenta di ottenere il secondo semaforo e allo stesso tempo il secondo thread tenta di ottenere il primo semaforo, entrambi i thread entrano in una condizione di deadlock. Inoltre, se questi thread rimarranno sospesi per sempre, anche le risorse associate vengono bloccate per sempre. Questo esempio è illustrato nella figura 8.

**Abbraccio mortale** (esempio)

![Esempio di thread sospesi](./media/user-guide/example-suspended-threads.png)

**FIGURA 8. Esempio di thread sospesi**

Per i sistemi in tempo reale, gli abbracci letali possono essere evitati inserendo alcune restrizioni sul modo in cui i thread ottengono i semafori. I thread possono avere un solo semaforo alla volta. In alternativa, i thread possono essere proprietari di più semafori se li raccolgono nello stesso ordine. Nell'esempio precedente, se il primo e il secondo thread ottengono il primo e il secondo semaforo nell'ordine, l'abbraccio mortale viene impedito.

> [!TIP]
> *È anche possibile usare il timeout di sospensione associato all'operazione get per il ripristino da un abbraccio mortale.*

### <a name="priority-inversion"></a>Inversione priorità

Un altro trabocchetto associato ai semafori di esclusione reciproca è la priorità Inversion. Questo argomento viene descritto più in dettaglio in "problemi relativi alla[priorità del thread](#thread-priority-pitfalls)".

Il problema di base è dovuto a una situazione in cui un thread con priorità più bassa ha un semaforo che richiede un thread con priorità più elevata. Si tratta di un comportamento normale. Tuttavia, i thread con le priorità tra di essi possono causare l'inversione della priorità per l'ultimo periodo di tempo non deterministico. Questo può essere gestito tramite un'attenta selezione delle priorità dei thread, usando la soglia di precedenza e aumentando temporaneamente la priorità del thread che possiede la risorsa a quello del thread con priorità alta.

## <a name="mutexes"></a>Mutex

Oltre ai semafori, ThreadX fornisce anche un oggetto mutex. Un mutex è fondamentalmente un semaforo binario, il che significa che un solo thread può essere proprietario di un mutex alla volta. Inoltre, lo stesso thread può eseguire un'operazione mutex Get riuscita su un mutex di proprietà più volte, 4.294.967.295 come Exact. Nell'oggetto mutex sono presenti due operazioni: ***tx_mutex_get** _ e _ *_tx_mutex_put_* *. L'operazione get ottiene un mutex non di proprietà di un altro thread, mentre l'operazione Put rilascia un mutex ottenuto in precedenza. Affinché un thread rilasci un mutex, il numero di operazioni Put deve essere uguale al numero di operazioni get precedenti.

Ogni mutex è una risorsa pubblica. ThreadX non impone vincoli sulla modalità di utilizzo di mutex.

I mutex ThreadX vengono usati esclusivamente per l' *esclusione reciproca*. Diversamente dal conteggio dei semafori, i mutex non sono usati come metodo per la notifica degli eventi.

### <a name="mutex-mutual-exclusion"></a>Esclusione reciproca mutex

Analogamente a quanto descritto nella sezione Counting Semaphore, l'esclusione reciproca riguarda il controllo dell'accesso dei thread a determinate aree dell'applicazione, denominate anche *sezioni critiche* o *risorse dell'applicazione*. Se disponibile, un mutex ThreadX avrà un numero di proprietà pari a 0. Dopo che il mutex è stato ottenuto da un thread, il numero di proprietà viene incrementato una volta per ogni operazione Get riuscita eseguita sul mutex e decrementa per ogni operazione Put riuscita.

### <a name="creating-mutexes"></a>Creazione di mutex

I mutex ThreadX vengono creati durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. La condizione iniziale di un mutex è sempre "disponibile". È possibile creare anche un mutex con l' *ereditarietà prioritaria* selezionata.

### <a name="thread-suspension"></a>Sospensione thread

I thread dell'applicazione possono essere sospesi durante il tentativo di eseguire un'operazione get su un mutex già di proprietà di un altro thread.

Quando il thread proprietario esegue lo stesso numero di operazioni Put, viene eseguita l'operazione Get del thread sospeso, assegnando la proprietà del mutex e il thread viene ripreso. Se più thread vengono sospesi nello stesso mutex, vengono ripresi nello stesso ordine in cui sono stati sospesi (FIFO).

Tuttavia, la ripresa della priorità viene eseguita automaticamente se l'ereditarietà della priorità mutex è stata selezionata durante la creazione. La ripresa della priorità è inoltre possibile se l'applicazione chiama ***tx_mutex_prioritize*** prima della chiamata put mutex che solleva la sospensione del thread. Il servizio di assegnazione delle priorità di mutex posiziona il thread con priorità più elevata all'inizio dell'elenco di sospensioni, lasciando tutti gli altri thread sospesi nello stesso ordine FIFO.

### <a name="run-time-mutex-performance-information"></a>Informazioni sulle prestazioni del mutex in fase di esecuzione

ThreadX fornisce informazioni sulle prestazioni di mutex in fase di esecuzione facoltative. Se la libreria e l'applicazione ThreadX sono compilate con **TX_MUTEX_ENABLE_PERFORMANCE_INFO** definito, threadX accumula le informazioni seguenti.

Numero totale per il sistema globale:

- mutex put

- mutex ottiene

- sospensioni mutex Get

- Timeout get mutex

- inversioni di priorità mutex

- ereditarietà priorità mutex

Numero totale per ogni mutex:

  - mutex put

  - mutex ottiene

  - sospensioni mutex Get

  - Timeout get mutex

  - inversioni di priorità mutex

  - ereditarietà priorità mutex

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi ***tx_mutex_performance_info_get** _ e _ *_tx_mutex_performance_system_info_get_* *. Le informazioni sulle prestazioni di mutex sono utili per determinare se l'applicazione funziona correttamente. È utile anche per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di "Timeout get mutex" potrebbe suggerire che altri thread mantengono risorse troppo lunghe.

### <a name="mutex-control-block-tx_mutex"></a>TX_MUTEX del blocco di controllo mutex

Le caratteristiche di ogni mutex sono disponibili nel relativo blocco di controllo. Contiene informazioni come il conteggio di proprietà Mutex corrente insieme al puntatore del thread proprietario del mutex. Questa struttura viene definita nel file ***tx_api. h*** . I blocchi di controllo mutex possono trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendolo al di fuori dell'ambito di qualsiasi funzione.

### <a name="deadly-embrace"></a>Abbraccio mortale

Uno degli errori più interessanti e pericolosi associati alla proprietà di mutex è l' *abbraccio mortale*. Un abbraccio mortale, o un *deadlock*, è una condizione in cui due o più thread vengono sospesi a tempo indefinito durante il tentativo di ottenere un mutex già di proprietà degli altri thread. La discussione sull' *abbraccio mortale* e sui relativi rimedi è completamente valida anche per l'oggetto mutex.

### <a name="priority-inversion"></a>Inversione priorità

Come indicato in precedenza, un grave problema associato all'esclusione reciproca è la priorità Inversion. Questo argomento viene descritto più in dettaglio in "problemi relativi alla[priorità del thread](#thread-priority-pitfalls)".

Il problema di base è dovuto a una situazione in cui un thread con priorità più bassa ha un semaforo che richiede un thread con priorità più elevata. Si tratta di un comportamento normale. Tuttavia, i thread con le priorità tra di essi possono causare l'inversione della priorità per l'ultimo periodo di tempo non deterministico. A differenza dei semafori descritti in precedenza, l'oggetto mutex ThreadX ha un' *ereditarietà prioritaria* facoltativa. La priorità di base dell'ereditarietà è che un thread con priorità inferiore ha la priorità generata temporaneamente alla priorità di un thread con priorità alta che desidera lo stesso mutex di proprietà del thread con priorità inferiore. Quando il thread con priorità più bassa rilascia il mutex, viene ripristinata la priorità originale e al thread con priorità superiore viene assegnata la proprietà del mutex. Questa funzionalità Elimina l'inversione di priorità non deterministica deselezionando la quantità di inversione fino al momento in cui il thread con priorità inferiore include il mutex. Naturalmente, le tecniche descritte in precedenza in questo capitolo per gestire l'inversione di priorità non deterministica sono valide anche per i mutex.

## <a name="event-flags"></a>Flag evento

I flag di evento forniscono uno strumento potente per la sincronizzazione dei thread. Ogni flag di evento è rappresentato da un solo bit. I flag di evento sono disposti in gruppi di 32. I thread possono operare su tutti i flag di evento 32 in un gruppo nello stesso momento. Gli eventi vengono impostati da ***tx_event_flags_set** _ e vengono recuperati da _ *_tx_event_flags_get_* *.

L'impostazione dei flag di evento viene eseguita con un'operazione AND/OR logica tra i flag di evento correnti e i nuovi flag di evento. Il tipo di operazione logica (AND o OR) viene specificato nella chiamata ***tx_event_flags_set*** .

Sono disponibili opzioni logiche simili per il recupero dei flag di evento. Una richiesta GET può specificare che tutti i flag di evento specificati sono obbligatori (AND logico).

In alternativa, una richiesta GET può specificare che uno dei flag evento specificati soddisferà la richiesta (un OR logico). Il tipo di operazione logica associata al recupero dei flag di evento è specificato nella chiamata ***tx_event_flags_get*** .

> [!IMPORTANT]
> *I flag di evento che soddisfano una richiesta GET vengono utilizzati, ovvero impostati su zero, se* **TX_OR_CLEAR** *o* **TX_AND_CLEAR** *sono specificati dalla richiesta.*

Ogni gruppo di flag di evento è una risorsa pubblica. ThreadX non impone vincoli sul modo in cui vengono usati i gruppi di flag evento.

### <a name="creating-event-flags-groups"></a>Creazione di gruppi di flag di evento

I gruppi di flag di evento vengono creati durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Al momento della creazione, tutti i flag di evento nel gruppo vengono impostati su zero. Non esiste alcun limite al numero di gruppi di flag di evento in un'applicazione.

### <a name="thread-suspension"></a>Sospensione thread

I thread dell'applicazione possono essere sospesi durante il tentativo di ottenere qualsiasi combinazione logica di flag evento da un gruppo. Dopo l'impostazione di un flag di evento, vengono esaminate le richieste Get di tutti i thread sospesi. Vengono ripresi tutti i thread che ora hanno i flag di evento richiesti.

> [!NOTE]
> *Tutti i thread sospesi in un gruppo di flag di evento vengono esaminati quando vengono impostati i flag evento. Questo, ovviamente, introduce un sovraccarico aggiuntivo. È pertanto consigliabile limitare il numero di thread che utilizzano lo stesso gruppo di flag di evento a un numero ragionevole.*

### <a name="event-flags-set-notification"></a>Notifica set di flag evento

Alcune applicazioni potrebbero risultare vantaggioso ricevere una notifica ogni volta che viene impostato un flag di evento. ThreadX offre questa possibilità tramite il servizio ***tx_event_flags_set_notify*** . Questo servizio registra la funzione di notifica dell'applicazione fornita con il gruppo di flag di evento specificato. ThreadX richiamerà successivamente questa funzione di notifica dell'applicazione ogni volta che viene impostato un flag di evento nel gruppo. L'elaborazione esatta all'interno della funzione di notifica dell'applicazione è determinata dall'applicazione, ma in genere è costituita dalla ripresa del thread appropriato per l'elaborazione del nuovo flag di evento.

### <a name="event-flags-event-chainingtrade"></a>Concatenamento di eventi flag di evento&trade;

Le funzionalità di notifica in ThreadX possono essere usate per "concatenare" vari eventi di sincronizzazione. Questa operazione è in genere utile quando un singolo thread deve elaborare più eventi di sincronizzazione.

Ad esempio, anziché avere thread separati sospesi per un messaggio della coda, i flag di evento e un semaforo, l'applicazione può registrare una routine di notifica per ogni oggetto. Quando viene richiamato, la routine di notifica dell'applicazione può riprendere un singolo thread, che può interrogare ogni oggetto per trovare ed elaborare il nuovo evento.

In generale, il *concatenamento degli eventi* comporta un minor numero di thread, minore overhead e requisiti di RAM inferiori. Fornisce inoltre un meccanismo estremamente flessibile per gestire i requisiti di sincronizzazione di sistemi più complessi.

### <a name="run-time-event-flags-performance-information"></a>Informazioni sulle prestazioni di flag di runtime

ThreadX fornisce informazioni sulle prestazioni di flag di runtime facoltativi. Se la libreria e l'applicazione ThreadX sono compilate con **TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO** definito, threadX accumula le informazioni seguenti.

Numero totale per il sistema globale:

  - set di flag evento

  - Flag evento ottenuti

  - i flag evento ottengono sospensioni

  - timeout di Get dei flag evento

Numero totale per ogni gruppo di flag di evento:

  - set di flag evento

  - Flag evento ottenuti

  - i flag evento ottengono sospensioni

  - timeout di Get dei flag evento

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi ***tx_event_flags_performance_info_get** _ e _*_tx_event_flags_performance_system_info_get_*_. Le informazioni sulle prestazioni dei flag di evento sono utili per determinare se l'applicazione funziona correttamente. È utile anche per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di timeout nel servizio _ *_tx_event_flags_get_** potrebbe indicare che il timeout di sospensione dei flag di evento è troppo breve.

### <a name="event-flags-group-control-block-tx_event_flags_group"></a>Blocco di controllo gruppo flag di evento TX_EVENT_FLAGS_GROUP

Le caratteristiche di ogni gruppo di flag di evento sono disponibili nel relativo blocco di controllo. Contiene informazioni quali le impostazioni dei flag di evento correnti e il numero di thread sospesi per gli eventi. Questa struttura viene definita nel file ***tx_api. h*** .

I blocchi di controllo del gruppo di eventi possono trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendola al di fuori dell'ambito di qualsiasi funzione.

### <a name="memory-block-pools"></a>Pool di blocchi di memoria

L'allocazione della memoria in modo rapido e deterministico è sempre un problema in applicazioni in tempo reale. Tenendo presente questo aspetto, ThreadX offre la possibilità di creare e gestire più pool di blocchi di memoria di dimensioni fisse.

Poiché i pool di blocchi di memoria sono costituiti da blocchi di dimensioni fisse, non si verificano mai problemi di frammentazione. Naturalmente, la frammentazione causa comportamenti intrinsecamente non deterministici. Inoltre, il tempo necessario per allocare e liberare un blocco di memoria di dimensioni fisse è paragonabile a quello della semplice manipolazione di elenchi collegati. Inoltre, l'allocazione e la deallocazione dei blocchi di memoria vengono eseguite all'inizio dell'elenco disponibile. Questa operazione fornisce l'elaborazione dell'elenco collegato più veloce possibile e potrebbe contribuire a tenere il blocco di memoria effettivo nella cache.

La mancanza di flessibilità è lo svantaggio principale dei pool di memoria a dimensione fissa. Le dimensioni del blocco di un pool devono essere sufficienti per gestire i requisiti di memoria del caso peggiori degli utenti. Naturalmente, la memoria può essere sprecata se vengono apportate molte richieste di memoria di dimensioni diverse allo stesso pool. Una possibile soluzione consiste nel creare diversi pool di blocchi di memoria diversi che contengono blocchi di memoria di dimensioni diverse.

Ogni pool di blocchi di memoria è una risorsa pubblica. ThreadX non impone vincoli per la modalità di utilizzo del pool.

### <a name="creating-memory-block-pools"></a>Creazione di pool di blocchi di memoria

I pool di blocchi di memoria vengono creati durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Non esiste alcun limite al numero di pool di blocchi di memoria in un'applicazione.

### <a name="memory-block-size"></a>Dimensioni blocco di memoria

Come indicato in precedenza, i pool di blocchi di memoria contengono un numero di blocchi di dimensioni fisse. Le dimensioni del blocco, in byte, vengono specificate durante la creazione del pool.

> [!NOTE]
> *ThreadX aggiunge una piccola quantità di overhead, ovvero la dimensione di un puntatore C, a ogni blocco di memoria nel pool. Inoltre, ThreadX potrebbe dover riempire le dimensioni del blocco per evitare l'inizio di ogni blocco di memoria nell'allineamento appropriato.*

### <a name="pool-capacity"></a>Capacità pool

Il numero di blocchi di memoria in un pool è una funzione delle dimensioni del blocco e il numero totale di byte nell'area di memoria fornita durante la creazione. La capacità di un pool viene calcolata dividendo le dimensioni del blocco (inclusa la spaziatura interna e i byte di overhead del puntatore) nel numero totale di byte nell'area di memoria specificata.

### <a name="pools-memory-area"></a>Area di memoria del pool

Come indicato in precedenza, l'area di memoria per il pool di blocchi viene specificata durante la creazione. Analogamente ad altre aree di memoria in ThreadX, può trovarsi in qualsiasi punto dello spazio degli indirizzi della destinazione.

Si tratta di una funzionalità importante grazie alla notevole flessibilità offerta. Si supponga, ad esempio, che un prodotto di comunicazione disponga di un'area di memoria ad alta velocità per l'I/O. Questa area di memoria è facilmente gestibile rendendola in un pool di blocchi di memoria ThreadX.

### <a name="thread-suspension"></a>Sospensione thread

I thread dell'applicazione possono essere sospesi in attesa di un blocco di memoria da un pool vuoto. Quando un blocco viene restituito al pool, al thread sospeso viene assegnato questo blocco e il thread viene ripreso.

Se più thread vengono sospesi nello stesso pool di blocchi di memoria, verranno ripresi nell'ordine in cui sono stati sospesi (FIFO).

Tuttavia, la ripresa della priorità è possibile anche se l'applicazione chiama ***tx_block_pool_prioritize*** prima della chiamata di rilascio del blocco che solleva la sospensione del thread. Il servizio di assegnazione delle priorità del pool di blocchi posiziona il thread con priorità più elevata all'inizio dell'elenco di sospensioni, lasciando tutti gli altri thread sospesi nello stesso ordine FIFO.

### <a name="run-time-block-pool-performance-information"></a>Informazioni sulle prestazioni del pool di blocchi in fase di esecuzione

ThreadX fornisce informazioni sulle prestazioni del pool di blocchi in fase di esecuzione facoltative. Se la libreria e l'applicazione ThreadX sono compilate con **TX_BLOCK_POOL_ENABLE_PERFORMANCE_INFO** definito, threadX accumula le informazioni seguenti.

Numero totale per il sistema globale:

  - blocchi allocati

  - blocchi rilasciati

  - sospensioni di allocazione

  - timeout di allocazione

Numero totale per ogni pool di blocchi:

  - blocchi allocati

  - blocchi rilasciati

  - sospensioni di allocazione

  - timeout di allocazione

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi ***tx_block_pool_performance_info_get** _ e _ *_tx_block_pool_performance_system_info_get_* *. Le informazioni sulle prestazioni del pool di blocchi sono utili per determinare se l'applicazione funziona correttamente. È utile anche per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di "sospensioni di allocazione" potrebbe indicare che il pool di blocchi è troppo piccolo.

### <a name="memory-block-pool-control-block-tx_block_pool"></a>Blocco di controllo del pool di blocchi di memoria TX_BLOCK_POOL

Le caratteristiche di ogni pool di blocchi di memoria si trovano nel blocco di controllo. Contiene informazioni quali il numero di blocchi di memoria disponibili e le dimensioni del blocco del pool di memoria. Questa struttura viene definita nel file ***tx_api. h*** .

I blocchi di controllo del pool possono anche trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendola al di fuori dell'ambito di qualsiasi funzione.

### <a name="overwriting-memory-blocks"></a>Sovrascrittura di blocchi di memoria

È importante assicurarsi che l'utente di un blocco di memoria allocato non scriva al di fuori dei limiti. In tal caso, il danneggiamento si verifica in un'area di memoria adiacente (in genere successiva). I risultati sono imprevedibili e spesso fatali per l'applicazione.

## <a name="memory-byte-pools"></a>Pool di byte di memoria

I pool di byte di memoria ThreadX sono simili a un heap C standard. Diversamente dall'heap C standard, è possibile avere più pool di byte di memoria. Inoltre, i thread possono sospendere in un pool fino a quando non è disponibile la memoria richiesta.

Le allocazioni dai pool di byte di memoria sono simili alle chiamate tradizionali ***malloc** _, che includono la quantità di memoria desiderata (in byte). La memoria viene allocata dal pool in modo _first ovvero, viene utilizzato il primo blocco di memoria libera che soddisfa la richiesta. Una quantità eccessiva di memoria da questo blocco viene convertita in un nuovo blocco e inserita nuovamente nell'elenco di memoria libera. Questo processo è denominato *frammentazione*.

I blocchi di memoria liberi adiacenti vengono *Uniti* durante una ricerca di allocazione successiva per un blocco di memoria disponibile sufficientemente grande. Questo processo è denominato *deframmentazione*.

Ogni pool di byte di memoria è una risorsa pubblica. ThreadX non impone vincoli per la modalità di utilizzo dei pool, ad eccezione del fatto che non è possibile chiamare i servizi byte di memoria da ISRs.

### <a name="creating-memory-byte-pools"></a>Creazione di pool di byte di memoria

I pool di byte di memoria vengono creati durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Non esiste alcun limite al numero di pool di byte di memoria in un'applicazione.

### <a name="pool-capacity"></a>Capacità pool

Il numero di byte allocabili in un pool di byte di memoria è leggermente inferiore a quello specificato durante la creazione. Ciò è dovuto al fatto che la gestione dell'area di memoria libera introduce un sovraccarico. Ogni blocco di memoria disponibile nel pool richiede l'equivalente di due puntatori C di overhead. Il pool viene inoltre creato con due blocchi, un blocco libero di grandi dimensioni e un piccolo blocco allocato in modo permanente alla fine dell'area di memoria. Questo blocco allocato viene utilizzato per migliorare le prestazioni dell'algoritmo di allocazione. Elimina la necessità di verificare continuamente la fine dell'area del pool durante l'Unione.

Durante la fase di esecuzione, la quantità di overhead nel pool aumenta in genere. Le allocazioni di un numero dispari di byte vengono riempite per garantire un corretto allineamento del blocco di memoria successivo. Inoltre, l'overhead aumenta quando il pool diventa più frammentato.

### <a name="pools-memory-area"></a>Area di memoria del pool

L'area di memoria per un pool di byte di memoria viene specificata durante la creazione. Analogamente ad altre aree di memoria in ThreadX, può trovarsi in qualsiasi punto dello spazio degli indirizzi della destinazione. Si tratta di una funzionalità importante grazie alla notevole flessibilità offerta. Se, ad esempio, l'hardware di destinazione ha un'area di memoria ad alta velocità e un'area di memoria a bassa velocità, l'utente può gestire l'allocazione di memoria per entrambe le aree creando un pool in ognuno di essi.

### <a name="thread-suspension"></a>Sospensione thread

I thread dell'applicazione possono essere sospesi in attesa di byte di memoria da un pool. Quando è disponibile una quantità di memoria contigua sufficiente, ai thread sospesi viene assegnata la memoria richiesta e i thread vengono ripresi.

Se più thread vengono sospesi nello stesso pool di byte di memoria, vengono assegnati alla memoria (ripresa) nell'ordine in cui sono stati sospesi (FIFO).

Tuttavia, la ripresa della priorità è possibile anche se l'applicazione chiama ***tx_byte_pool_prioritize*** prima della chiamata di rilascio di byte che solleva la sospensione del thread. Il servizio di assegnazione delle priorità del pool di byte inserisce il thread con priorità più elevata all'inizio dell'elenco di sospensioni, lasciando tutti gli altri thread sospesi nello stesso ordine FIFO.

### <a name="run-time-byte-pool-performance-information"></a>Informazioni sulle prestazioni del pool di byte in fase di esecuzione

ThreadX fornisce informazioni sulle prestazioni del pool di byte in fase di esecuzione facoltative. Se la libreria e l'applicazione ThreadX sono compilate con ***TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO*** definito, threadX accumula le informazioni seguenti.

Numero totale per il sistema globale:

  - allocazioni

  - versioni

  - frammenti cercati

  - frammenti Uniti

  - frammenti creati

  - sospensioni di allocazione

  - timeout di allocazione

Numero totale per ogni pool di byte:

  - allocazioni

  - versioni

  - frammenti cercati

  - frammenti Uniti

  - frammenti creati

  - sospensioni di allocazione

  - timeout di allocazione

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi ***tx_byte_pool_performance_info_get** _ e _ *_tx_byte_pool_performance_system_info_get_* *. Le informazioni sulle prestazioni del pool di byte sono utili per determinare se l'applicazione funziona correttamente. È utile anche per ottimizzare l'applicazione. Ad esempio, un numero relativamente elevato di "sospensioni di allocazione" potrebbe indicare che il pool di byte è troppo piccolo.

### <a name="memory-byte-pool-control-block-tx_byte_pool"></a>TX_BYTE_POOL blocco di controllo pool di byte di memoria

Le caratteristiche di ogni pool di byte di memoria si trovano nel blocco di controllo. Contiene informazioni utili, ad esempio il numero di byte disponibili nel pool. Questa struttura viene definita nel file ***tx_api. h*** .

I blocchi di controllo del pool possono anche trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendola al di fuori dell'ambito di qualsiasi funzione.

### <a name="nondeterministic-behavior"></a>Comportamento non deterministico

Sebbene i pool di byte di memoria forniscano l'allocazione di memoria più flessibile, soffrono anche di un comportamento non deterministico. Ad esempio, un pool di byte di memoria potrebbe avere 2.000 byte di memoria disponibile, ma potrebbe non essere in grado di soddisfare una richiesta di allocazione di 1.000 byte. Questo perché non esistono garanzie sul numero di byte liberi contigui. Anche se esiste un blocco libero a 1.000 byte, non sono previste garanzie sul tempo necessario per trovare il blocco. È possibile che l'intero pool di memoria debba eseguire la ricerca per trovare il blocco di 1.000 byte.

> [!TIP]
> *A causa del comportamento non deterministico dei pool di byte di memoria, è in genere consigliabile evitare l'utilizzo di servizi byte di memoria nelle aree in cui è necessario il comportamento deterministico e in tempo reale. Molte applicazioni preallocano la memoria necessaria durante l'inizializzazione o la configurazione in fase di esecuzione.*

### <a name="overwriting-memory-blocks"></a>Sovrascrittura di blocchi di memoria

È importante assicurarsi che l'utente della memoria allocata non scriva al di fuori dei limiti. In tal caso, il danneggiamento si verifica in un'area di memoria adiacente (in genere successiva). I risultati sono imprevedibili e spesso catastrofici per l'esecuzione del programma.

## <a name="application-timers"></a>Timer applicazione

Una risposta rapida a eventi esterni asincroni è la funzione più importante delle applicazioni incorporate in tempo reale. Tuttavia, molte di queste applicazioni devono anche eseguire determinate attività a intervalli di tempo prestabiliti.

I timer dell'applicazione ThreadX offrono alle applicazioni la possibilità di eseguire le funzioni C dell'applicazione a intervalli di tempo specifici. È anche possibile che un timer dell'applicazione SCADA una sola volta. Questo tipo di timer è denominato *timer* monouso, mentre i timer per intervalli ripetuti vengono chiamati timer *periodici*.

Ogni timer dell'applicazione è una risorsa pubblica. ThreadX non impone vincoli sul modo in cui vengono usati i timer applicazione.

### <a name="timer-intervals"></a>Intervalli timer

Negli intervalli di tempo ThreadX sono misurati in base a interrupt timer periodici. Ogni interrupt del timer viene chiamato *ciclo* del timer. Il tempo effettivo tra i cicli del timer viene specificato dall'applicazione, ma 10 ms è la norma per la maggior parte delle implementazioni. La configurazione del timer periodico si trova in genere nel file di assembly ***tx_initialize_low_level*** .

Vale la pena ricordare che l'hardware sottostante deve avere la possibilità di generare interruzioni periodiche per il funzionamento dei timer dell'applicazione. In alcuni casi, il processore ha una funzionalità di interrupt periodica incorporata. Se il processore non è in grado di eseguire questa operazione, è necessario che la lavagna dell'utente disponga di un dispositivo periferico in grado di generare interruzioni periodiche.

> [!IMPORTANT]
> *ThreadX può comunque funzionare anche senza un'origine interrupt periodica. Tuttavia, tutte le operazioni di elaborazione correlate al timer vengono disabilitate. Sono inclusi timeslicing, i timeout di sospensione e i servizi timer.*

### <a name="timer-accuracy"></a>Accuratezza timer

Le scadenze del timer vengono specificate in termini di cicli. Il valore di scadenza specificato viene diminuito di uno per ogni ciclo del timer. Poiché un timer dell'applicazione può essere abilitato immediatamente prima di un interrupt del timer (o un segno di timer), l'ora di scadenza effettiva potrebbe essere fino a un segno di prima.

Se la frequenza di battito del timer è 10 ms, i timer dell'applicazione possono scadere prima di 10 ms. Questa operazione è più significativa per i timer 10 ms di 1 secondo. Naturalmente, l'aumento della frequenza di interrupt del timer diminuisce questo margine di errore.

### <a name="timer-execution"></a>Esecuzione del timer

I timer dell'applicazione vengono eseguiti nell'ordine in cui diventano attivi. Se, ad esempio, vengono creati tre timer con lo stesso valore di scadenza e attivato, l'esecuzione delle funzioni di scadenza corrispondenti verrà garantita nell'ordine in cui sono state attivate.

### <a name="creating-application-timers"></a>Creazione di timer applicazione

I timer dell'applicazione vengono creati durante l'inizializzazione o durante la fase di esecuzione dai thread dell'applicazione. Non esiste alcun limite al numero di timer applicazione in un'applicazione.

### <a name="run-time-application-timer-performance-information"></a>Informazioni sulle prestazioni del timer dell'applicazione in fase di esecuzione

ThreadX fornisce informazioni sulle prestazioni del timer dell'applicazione in fase di esecuzione. Se la libreria e l'applicazione ThreadX sono compilate con **TX_TIMER_ENABLE_PERFORMANCE_INFO** definito, threadX accumula le informazioni seguenti.

Numero totale per il sistema globale:

- attivazioni

- disattivazioni

- Riattivazioni (timer periodici)

- expirations

- rettifiche di scadenza

Numero totale per ogni timer applicazione:

- attivazioni

- disattivazioni

- Riattivazioni (timer periodici)

- expirations

- rettifiche di scadenza

Queste informazioni sono disponibili in fase di esecuzione tramite i servizi ***tx_timer_performance_info_get** _ e _ *_tx_timer_performance_system_info_get_* *. Le informazioni sulle prestazioni del timer applicazione sono utili per determinare se l'applicazione funziona correttamente. È utile anche per ottimizzare l'applicazione.

### <a name="application-timer-control-block-tx_timer"></a>TX_TIMER blocco di controllo timer applicazione

Le caratteristiche di ogni timer dell'applicazione si trovano nel relativo blocco di controllo. Contiene informazioni utili, ad esempio il valore di identificazione della scadenza a 32 bit. Questa struttura viene definita nel file ***tx_api. h*** .

I blocchi di controllo del timer applicazione possono trovarsi in qualsiasi punto della memoria, ma è più comune fare in modo che il controllo blocchi una struttura globale definendolo al di fuori dell'ambito di qualsiasi funzione.

### <a name="excessive-timers"></a>Timer eccessivi

Per impostazione predefinita, i timer dell'applicazione vengono eseguiti da un thread di sistema nascosto eseguito con priorità zero, che in genere è superiore a qualsiasi thread dell'applicazione. Per questo motivo, l'elaborazione all'interno dei timer dell'applicazione deve essere mantenuta al minimo.

È inoltre importante evitare, quando possibile, i timer che scadono ogni ciclo del timer. Una situazione di questo tipo può causare un sovraccarico eccessivo nell'applicazione.

> [!IMPORTANT]
> *Come indicato in precedenza, i timer dell'applicazione vengono eseguiti da un thread di sistema nascosto. È pertanto importante non selezionare la sospensione per le chiamate al servizio ThreadX effettuate dall'interno della funzione di scadenza del timer dell'applicazione.*

## <a name="relative-time"></a>Ora relativa

Oltre ai timer dell'applicazione citati in precedenza, ThreadX fornisce un singolo contatore di cicli a 32 bit a incremento continuo. Il contatore o l' *ora* del segno di verifica viene aumentato di uno per ogni interrupt del timer.

L'applicazione può leggere o impostare questo contatore a 32 bit tramite chiamate a ***tx_time_get** _ e _ *_tx_time_set_* * rispettivamente. L'uso di questo contatore di cicli è determinato completamente dall'applicazione. Non viene utilizzato internamente da ThreadX.

## <a name="interrupts"></a>Interrompe

Una risposta rapida agli eventi asincroni è la funzione principale di applicazioni incorporate in tempo reale. L'applicazione sa che tale evento è presente attraverso gli interrupt hardware.

Un interrupt è una modifica asincrona nell'esecuzione del processore. In genere, quando si verifica un interrupt, il processore di *interrupt* salva una piccola parte dell'esecuzione corrente nello stack e trasferisce il controllo al vettore di interrupt appropriato. Il vettore di interrupt è fondamentalmente solo l'indirizzo della routine responsabile della gestione dell'interrupt del tipo specifico. La procedura di gestione degli interrupt esatta è specifica del processore.

### <a name="interrupt-control"></a>Interrompi controllo

Il servizio ***tx_interrupt_control*** consente alle applicazioni di abilitare e disabilitare gli interrupt. Questo servizio restituisce la postura di abilitazione/disabilitazione dell'interrupt precedente. È importante ricordare che il controllo interrupt influisca solo sul segmento di programma attualmente in esecuzione. Ad esempio, se un thread Disabilita gli interrupt, restano disabilitati solo durante l'esecuzione del thread.

> [!NOTE]
> *Un interrupt non mascherabile (NMI) è un interrupt che non può essere disabilitato dall'hardware. Tale interrupt può essere utilizzato dalle applicazioni ThreadX. Tuttavia, la routine di gestione NMI dell'applicazione non è autorizzata a usare la gestione del contesto ThreadX o qualsiasi servizio API.*

### <a name="threadx-managed-interrupts"></a>Interrupt gestiti di ThreadX

ThreadX fornisce applicazioni con gestione completa degli interrupt. Questa gestione include il salvataggio e il ripristino del contesto dell'esecuzione interrotta. Inoltre, ThreadX consente la chiamata di determinati servizi dall'interno di routine del servizio di interrupt (ISRs). Di seguito è riportato un elenco di servizi ThreadX consentiti dall'applicazione ISRs.

```c
tx_block_allocate
tx_block_pool_info_get tx_block_pool_prioritize
tx_block_pool_performance_info_get
tx_block_pool_performance_system_info_get tx_block_release
tx_byte_pool_info_get tx_byte_pool_performance_info_get
tx_byte_pool_performance_system_info_get
tx_byte_pool_prioritize tx_event_flags_info_get
tx_event_flags_get tx_event_flags_set
tx_event_flags_performance_info_get
tx_event_flags_performance_system_info_get
tx_event_flags_set_notify tx_interrupt_control
tx_mutex_performance_info_get
tx_mutex_performance_system_info_get tx_queue_front_send
tx_queue_info_get tx_queue_performance_info_get
tx_queue_performance_system_info_get tx_queue_prioritize
tx_queue_receive tx_queue_send tx_semaphore_get
tx_queue_send_notify tx_semaphore_ceiling_put
tx_semaphore_info_get tx_semaphore_performance_info_get
tx_semaphore_performance_system_info_get
tx_semaphore_prioritize tx_semaphore_put tx_thread_identify
tx_semaphore_put_notify tx_thread_entry_exit_notify
tx_thread_info_get tx_thread_resume
tx_thread_performance_info_get
tx_thread_performance_system_info_get
tx_thread_stack_error_notify tx_thread_wait_abort tx_time_get
tx_time_set tx_timer_activate tx_timer_change
tx_timer_deactivate tx_timer_info_get
tx_timer_performance_info_get
tx_timer_performance_system_info_get
```

> [!IMPORTANT]
> *La sospensione non è consentita da ISRs. Pertanto, il parametro **WAIT_OPTION** per tutte le chiamate al servizio threadX effettuate da un ISR deve essere impostato su **TX_NO_WAIT**.*

### <a name="isr-template"></a>Modello ISR

Per gestire gli interrupt dell'applicazione, è necessario chiamare diverse utilità ThreadX all'inizio e alla fine dell'applicazione ISRs. Il formato esatto per la gestione degli interrupt varia a seconda delle porte.

Il piccolo segmento di codice seguente è tipico della maggior parte degli ISRs gestiti ThreadX. Nella maggior parte dei casi, questa elaborazione è in linguaggio assembly.

```c
_application_ISR_vector_entry:

; Save context and prepare for

; ThreadX use by calling the ISR

; entry function.

CALL _tx_thread_context_save

; The ISR can now call ThreadX

; services and its own C functions

; When the ISR is finished, context

; is restored (or thread preemption)

; by calling the context restore ; function. Control does not return!

JUMP _tx_thread_context_restore
```

### <a name="high-frequency-interrupts"></a>Interrupt ad alta frequenza

Alcuni interrupt si verificano a una frequenza elevata che il salvataggio e il ripristino del contesto completo su ogni interrupt utilizzeranno una larghezza di banda di elaborazione eccessiva. In questi casi, è normale che l'applicazione disponga di un linguaggio ISR (Small assembly language) che esegue una quantità limitata di elaborazione per la maggior parte degli interrupt ad alta frequenza.

Dopo un certo periodo di tempo, il piccolo ISR potrebbe dover interagire con ThreadX. Questa operazione viene eseguita chiamando le funzioni di ingresso e di uscita descritte nel modello precedente.

### <a name="interrupt-latency"></a>Latenza interrupt

ThreadX blocca gli interrupt per brevi periodi di tempo. L'intervallo di tempo massimo di interrupt è disabilitato nell'ordine del tempo necessario per salvare o ripristinare il contesto di un thread.
