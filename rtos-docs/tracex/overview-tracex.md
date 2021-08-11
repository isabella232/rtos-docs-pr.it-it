---
title: Informazioni Azure RTOS TraceX
description: Azure RTOS TraceX è lo strumento di analisi basato su host di Microsoft che offre agli sviluppatori una visualizzazione grafica degli eventi di sistema in tempo reale e consente loro di visualizzare e comprendere meglio il comportamento dei sistemi in tempo reale.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 966f3be5ebe34e006067175e422480fbf1ab664bb0ff627d7b01e71036dc5e82
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116792181"
---
# <a name="overview-of-azure-rtos-tracex"></a>Panoramica di Azure RTOS TraceX

Azure RTOS TraceX è lo strumento di analisi basato su host di Microsoft che offre agli sviluppatori una visualizzazione grafica degli eventi di sistema in tempo reale e consente loro di visualizzare e comprendere meglio il comportamento dei sistemi in tempo reale. Con Azure RTOS TraceX, gli sviluppatori possono vedere chiaramente l'occorrenza di eventi di sistema come interrupt e commutatori di contesto che si verificano fuori dalla visualizzazione degli strumenti di debug standard. La possibilità di identificare e studiare questi eventi e di individuare la tempistica dell'occorrenza nel contesto dell'operazione complessiva del sistema consente agli sviluppatori di risolvere i problemi di programmazione individuando un comportamento imprevisto e consentendo loro di analizzare aree specifiche in cui ulteriori informazioni di traccia vengono archiviate in un buffer nel sistema di destinazione, con la posizione e le dimensioni del buffer determinate dall'applicazione in fase di esecuzione. Azure RTOS TraceX può elaborare qualsiasi buffer costruito nel modo corretto, non solo da Azure RTOS ThreadX, ma da qualsiasi applicazione o RTOS. Le informazioni di traccia possono essere caricate nell'host per l'analisi in qualsiasi momento, post-mortem o in corrispondenza di un punto di interruzione. Azure RTOS ThreadX implementa un buffer circolare, che consente agli eventi "N" più recenti di essere disponibili per l'ispezione in caso di malfunzionamento del sistema o di altri eventi significativi.

![Azure RTOS visualizzazione Single-Core TraceX](./media/user-guide/screen_shot_33.png)

**Visualizzazione Single-Core TraceX**

## <a name="key-capabilites"></a>Funzionalità chiave

### <a name="azure-rtos-tracex-built-in-system-analysis"></a>Azure RTOS'analisi di sistema incorporata di TraceX

Azure RTOS TraceX offre report di analisi di sistema predefiniti disponibili tramite un singolo clic del pulsante sulla barra degli strumenti di TraceX. Questi pulsanti e report includono:

![Generare il report del profilo di esecuzione](./media/overview-tracex/execution-profile-report-button.jpg) Generare il report del profilo di esecuzione

![Generare un report sulle statistiche delle prestazioni](./media/overview-tracex/performance-statistics-report-button.jpg) Generare un report sulle statistiche delle prestazioni

![Generare un report sull'utilizzo dello stack di thread](./media/overview-tracex/thread-stack-usage-report-button.jpg) Generare un report sull'utilizzo dello stack di thread

### <a name="trace-data-collected-by-azure-rtos-threadx"></a>Dati di traccia raccolti da Azure RTOS ThreadX

Azure RTOS TraceX è progettato per funzionare con Azure RTOS ThreadX, che costruisce un database di "eventi" del sistema e dell'applicazione nel sistema di destinazione durante la fase di esecuzione. Questi eventi includono:

* commutatori di contesto del thread
* preemptions
* Sospensioni
* Terminazioni
* interrupt di sistema
* eventi specifici dell'applicazione
* tutte Azure RTOS di API ThreadX
* tutte Azure RTOS chiamate API NetX
* tutte le Azure RTOS api FileX
* tutte Azure RTOS chiamate API USBX
* icone e informazioni definite dall'applicazione

Gli eventi vengono registrati sotto il controllo del programma, con timestamp e identificazione del thread attivo, in modo che possano essere visualizzati in un secondo momento nella sequenza temporale appropriata e associati al thread appropriato. La registrazione degli eventi può essere arrestata e riavviata dinamicamente dal programma dell'applicazione, ad esempio quando viene rilevata un'area di interesse. In questo modo si evita di ingombrare il database e di usare la memoria di destinazione quando il sistema funziona correttamente.

### <a name="azure-rtos-tracex-is-like-a-software-logic-analyzer"></a>Azure RTOS TraceX è simile a un analizzatore di logica software

Dopo il caricamento del log eventi dalla memoria di destinazione all'host, Azure RTOS TraceX visualizza gli eventi graficamente su un asse orizzontale che rappresenta l'ora, con i vari thread dell'applicazione e le routine di sistema a cui gli eventi sono correlati elencati lungo l'asse verticale. Azure RTOS TraceX crea un "analizzatore della logica software" nell'host, rendendo gli eventi di sistema chiaramente visibili. Gli eventi sono rappresentati da icone codificate a colori, che si trovano nel punto dell'occorrenza lungo la sequenza temporale orizzontale, a destra del thread o della routine di sistema pertinente. Quando si seleziona un'icona di evento, vengono visualizzate le informazioni corrispondenti per tale evento, nonché le informazioni per i due eventi precedenti e successivi. In questo modo è possibile accedere rapidamente con un solo clic alle informazioni più immediate sull'evento e sugli eventi immediatamente circostanti. Azure RTOS TraceX offre una visualizzazione "Riepilogo" che mostra tutti gli eventi di sistema su una singola linea orizzontale per semplificare l'analisi dei sistemi con molti thread.

### <a name="sequential-view-mode"></a>Modalità di visualizzazione sequenziale

La modalità di visualizzazione sequenziale viene selezionata facendo clic sulla scheda "Visualizzazione sequenziale". Questa è la modalità predefinita. In questa modalità, gli eventi vengono visualizzati immediatamente l'uno dopo l'altro, indipendentemente dal tempo trascorso tra di essi. Si noti anche il righello sopra l'area di visualizzazione. Mostra il numero di evento relativo dall'inizio della traccia. Questa modalità è la modalità predefinita ed è particolarmente utile per ottenere una buona panoramica di ciò che succede nel sistema.

![Modalità di visualizzazione sequenziale](./media/user-guide/screen_shot_10.png)

**Modalità di visualizzazione sequenziale**

### <a name="time-view-mode"></a>Modalità di visualizzazione dell'ora

In questa modalità, gli eventi vengono visualizzati in modo relativo al tempo, con una barra verde continua usata per mostrare l'esecuzione tra gli eventi. Questa modalità è particolarmente utile per vedere dove avviene la maggior parte dell'elaborazione nel sistema, che può aiutare gli sviluppatori a ottimizzare il sistema per migliorare le prestazioni e/o la velocità di risposta.

Si noti anche il righello sopra la visualizzazione dell'evento. Questo righello mostra i segni di graduazione relativi dall'inizio della traccia, come derivato dal timestamp instrumentato nella registrazione della traccia eventi all'interno di Azure RTOS ThreadX. Se i timestamp sono troppo vicini (timer a bassa frequenza), gli eventi verranno eseguiti insieme. Al contrario, se i timestamp sono troppo distanti (timer a frequenza elevata), gli eventi saranno troppo distanti. La scelta del timestamp di frequenza giusto è una considerazione importante per rendere significativa la visualizzazione relativa all'ora.

![Modalità di visualizzazione temporale](./media/user-guide/screen_shot_31.png)

### <a name="system-summary-line"></a>Riga di riepilogo del sistema

Azure RTOS TraceX fornisce anche una singola riga di riepilogo che include tutti gli eventi nella stessa riga. La riga di riepilogo contiene un riepilogo del contesto e il riepilogo dell'evento corrispondente sottostante. In questo modo è facile visualizzare una panoramica di un sistema complesso. La barra di riepilogo è particolarmente utile nei sistemi con un numero elevato di thread. Senza tale riga di riepilogo, l'utente deve seguire interazioni di sistema complesse usando la barra di scorrimento verticale per seguire il contesto di esecuzione.

Azure RTOS TraceX elenca i contesti di sistema sul lato sinistro dello schermo.
Gli eventi che si verificano in un contesto specifico vengono visualizzati sulla linea orizzontale a destra di tale contesto. In questo modo, l'utente può facilmente determinare il contesto in cui si è verificato l'evento e seguire tale riga di contesto per visualizzare tutti gli eventi che si sono verificati in un contesto specifico.

![Riga di riepilogo del sistema](./media/user-guide/screen_shot_32.png)

**Riga di riepilogo del sistema**

Le prime due voci di contesto sono sempre i contesti "Interrupt" e "Initialize/Idle". Il contesto "Interrupt" rappresenta tutti gli eventi di sistema generati dalle routine di servizio di interrupt (ISR). Il contesto "Initialize/Idle" rappresenta due contesti in Azure RTOS ThreadX. Gli eventi che si verificano tx_application_define, sono eventi "Initialize" e vengono visualizzati nel contesto "Initialize/Idle". Se il sistema è inattivo e quindi non si verifica alcun evento, la barra verde che rappresenta "Running" nella visualizzazione temporale viene disegnata nel contesto "Initialize/Idle".

## <a name="methods-of-navigation"></a>Metodi di navigazione

Azure RTOS TraceX consente allo sviluppatore di specificare il funzionamento dei pulsanti di spostamento "Avanti" e "Indietro".

![Pulsanti di spostamento](./media/user-guide/event.png)

Se si seleziona "Evento", la navigazione viene eseguita nell'evento successivo/precedente. Se si seleziona "Contesto", lo spostamento viene eseguito sull'evento successivo/precedente nello stesso contesto. Se si seleziona "Object", lo spostamento viene eseguito sull'evento successivo/precedente dell'oggetto corrente, ad esempio gli eventi associati a una coda specifica. Se è selezionata l'opzione "Commutatori", la navigazione viene eseguita nel passaggio di contesto successivo/precedente. Se si seleziona "Stesso ID", la navigazione viene eseguita nell'evento successivo/precedente per lo stesso ID evento.

### <a name="event-information-display"></a>Visualizzazione delle informazioni sugli eventi

Azure RTOS TraceX fornisce informazioni dettagliate su circa 300 eventi. Sono inclusi sei eventi ThreadX Azure RTOS interni, due eventi ISR (enter ed exit), 14 eventi FileX Azure RTOS interni, 42 eventi NetX Azure RTOS interni e un evento definito dall'utente. Gli eventi rimanenti corrispondono direttamente Azure RTOS ThreadX, Azure RTOS FileX e Azure RTOS servizi API NetX.
Indipendentemente dal fatto che sia selezionata la modalità di visualizzazione sequenziale o temporale, un passaggio del mouse su qualsiasi evento nell'area di visualizzazione comporta la visualizzazione di informazioni dettagliate sull'evento vicino all'evento. Il passaggio del mouse sull'evento 494 nel file di traccia demo_threadx.trx dimostrativo è illustrato di seguito:

![Mouse-Over visualizza altre informazioni](./media/user-guide/screen_shot_37.png)

**Il passaggio del mouse visualizza altre informazioni**

Ogni evento visualizzato contiene informazioni standard sul contesto e sia l'ora relativa che il timestamp. Il campo Contesto mostra il contesto in cui si è verificata l'evento. Esistono esattamente quattro contesti: thread, inattività, ISR e inizializzazione. Quando un evento si verifica in un contesto di thread, il nome del thread e la relativa priorità in quel momento vengono raccolti e visualizzati come illustrato in precedenza. L'ora relativa mostra il numero relativo di tick del timer dall'inizio della traccia. Il timestamp non elaborato visualizza l'origine dell'ora non elaborata dell'evento. Infine, vengono visualizzate tutte le informazioni specifiche dell'evento.

### <a name="zooming-in-and-out"></a>Zoom avanti e indietro

Per impostazione predefinita, Azure RTOS TraceX visualizza gli eventi in dimensioni facilmente visualizzabili, con un mapping di 1:1 pixel:tick. L'utente può eseguire lo zoom avanti o indietro in base alle esigenze. Lo zoom indietro al 100% è utile per visualizzare l'intera traccia nella visualizzazione corrente, mentre lo zoom avanti è utile nelle condizioni in cui gli eventi si sovrappongono a causa della risoluzione dell'origine timestamp.

![Zoom-Out visualizzazione al 100% o zoom avanti per i dettagli](./media/user-guide/screen_shot_41.png)

**Zoom indietro per visualizzare al 100% o zoom avanti per i dettagli**

Quando si esegue lo zoom indietro al 100%, visualizzando l'intera traccia all'interno della pagina di visualizzazione corrente, è facile visualizzare tutte le esecuzioni del contesto acquisite nella traccia, nonché gli eventi generali che si verificano all'interno di tali contesti. Si noti che "thread 1" e "thread 2" vengono eseguiti più spesso. La colorazione blu per i relativi eventi suggerisce anche che questi thread effettuano chiamate al servizio di accodamento (gli eventi della coda sono di colore blu).

Il ripristino in una visualizzazione icona completa è altrettanto semplice. Il pulsante di zoom avanti può essere selezionato ripetutamente o è possibile immettere un fattore di 100.

### <a name="delta-ticks-between-events"></a>Tick differenziali tra gli eventi

Determinare il numero di tick tra i vari eventi in Azure RTOS TraceX è semplice: è sufficiente fare clic sull'evento iniziale e trascinare il mouse sull'evento finale.
Il numero delta di tick tra gli eventi verrà visualizzato nell'angolo superiore destro dello schermo.

![Tick delta](./media/user-guide/screen_shot_42.png)

**Tick delta**

I tick delta indicano che sono trascorsi 5032 tick tra l'evento 494 e l'evento 496. Questo può anche essere calcolato manualmente esaminando i timestamp relativi in ogni evento e sottraendo, ma l'uso dell'interfaccia utente grafica è semplice e istantaneo.

### <a name="priority-inversions"></a>Inversione di priorità

Azure RTOS TraceX visualizza automaticamente le inversione di priorità rilevate nel file di traccia. Le inversioni di priorità sono definite come condizioni in cui un thread con priorità più alta viene bloccato tentando di ottenere un mutex attualmente di proprietà di un thread con priorità più bassa. Questa condizione è stata specificata come "deterministica", perché il sistema è stato programmato per funzionare in questo modo. Per informare l'utente, Azure RTOS TraceX mostra gli intervalli di inversione della priorità "deterministici" come colore blu chiaro.

Azure RTOS TraceX visualizza anche le inversione di priorità "non deterministiche". Queste inversione di priorità differiscono dalle inversioni di priorità "deterministiche" perché un altro thread di un livello di priorità diverso è stato eseguito nel mezzo di quella che era un'inversione di priorità "deterministica", rendendo il tempo entro l'inversione della priorità un po' "non deterministico". Questa condizione è spesso sconosciuta all'utente e può essere molto grave. Per avvisare l'utente di questa condizione, Azure RTOS TraceX mostra le inversioni di priorità "non deterministiche" come colore color più chiaro.

![Inversione di priorità deterministica e non deterministica](./media/user-guide/screen_shot_43.png)

**Inversione di priorità deterministica e non deterministica**

### <a name="execution-profile"></a>Profilo di esecuzione

Azure RTOS TraceX fornisce un report del profilo di esecuzione predefinito per tutti i contesti di esecuzione all'interno di nel file di traccia attualmente caricato.

![Profilo di esecuzione](./media/user-guide/execution_profile.png)

### <a name="performance-statistics"></a>Performance statistics

Azure RTOS TraceX fornisce un report delle statistiche sulle prestazioni incorporato per il file di traccia attualmente caricato.

![Performance statistics](./media/user-guide/performance_statistics.png)

### <a name="thread-stack-usage"></a>Utilizzo dello stack di thread

Azure RTOS TraceX fornisce un report sull'utilizzo dello stack incorporato per tutti i thread in esecuzione all'interno del file di traccia attualmente caricato.

![Utilizzo dello stack](./media/user-guide/thread_stack_usage.png)

Azure RTOS TraceX presenta le Azure RTOS delle prestazioni fileX del file di traccia attualmente caricato. Queste informazioni vengono visualizzate per l'intero sistema in tutti gli oggetti multimediali aperti.

![Statistiche FileX](./media/user-guide/filex_statistics.png)

### <a name="azure-rtos-netx-statistics"></a>Azure RTOS statistiche NetX

Azure RTOS TraceX presenta anche le statistiche sulle prestazioni NetX del file di traccia attualmente caricato. Queste informazioni vengono visualizzate per l'intero sistema.

![Statistiche NetX](./media/user-guide/netx_statistics.png)

### <a name="raw-trace-dump"></a>Dump di traccia non elaborato

Azure RTOS TraceX può compilare un file di traccia non elaborato in formato testo e avviare il Blocco note per visualizzarlo.

![Dump di traccia non elaborato](./media/user-guide/raw_trace_dump.png)

Si noti che tutte le cifre relative a tempi e dimensioni elencate sono stime e possono essere diverse nella piattaforma di sviluppo
