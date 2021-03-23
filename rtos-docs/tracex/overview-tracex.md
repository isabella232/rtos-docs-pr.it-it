---
title: Informazioni su Azure RTO TraceX
description: Azure RTO TraceX è uno strumento di analisi basato su host Microsoft che offre agli sviluppatori una visualizzazione grafica degli eventi di sistema in tempo reale e consente loro di visualizzare e comprendere meglio il comportamento dei sistemi in tempo reale.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 9fd33eec6da69e6dda421a125a2dde5eae93b46d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104824530"
---
# <a name="overview-of-azure-rtos-tracex"></a>Panoramica di Azure RTO TraceX

Azure RTO TraceX è uno strumento di analisi basato su host Microsoft che offre agli sviluppatori una visualizzazione grafica degli eventi di sistema in tempo reale e consente loro di visualizzare e comprendere meglio il comportamento dei sistemi in tempo reale. Con Azure RTO TraceX, gli sviluppatori possono vedere chiaramente l'occorrenza di eventi di sistema come gli interrupt e i cambi di contesto che si verificano con gli strumenti di debug standard. La possibilità di identificare e studiare questi eventi e di individuare la tempistica dell'occorrenza nel contesto dell'operazione complessiva del sistema consente agli sviluppatori di risolvere i problemi di programmazione cercando un comportamento imprevisto e consentendo loro di esaminare aree specifiche. le informazioni di traccia aggiuntive vengono archiviate in un buffer nel sistema di destinazione, con la posizione e le dimensioni del buffer determinate dall'applicazione in fase di esecuzione. Azure RTO TraceX può elaborare qualsiasi buffer costruito nel modo appropriato, non solo da Azure RTO ThreadX, ma da qualsiasi applicazione o RTO. Le informazioni di traccia possono essere caricate nell'host per l'analisi in qualsiasi momento, ovvero post mortem o su un punto di interruzione. Azure RTO ThreadX implementa un buffer circolare, che consente agli eventi "N" più recenti di essere disponibili per l'ispezione in caso di malfunzionamento del sistema o un altro evento significativo.

![Visualizzazione Single-Core di Azure RTO TraceX](./media/user-guide/screen_shot_33.png)

**Visualizzazione Single-Core TraceX**

## <a name="key-capabilites"></a>Funzionalità chiave

### <a name="azure-rtos-tracex-built-in-system-analysis"></a>Analisi del sistema incorporata in Azure RTO TraceX

Azure RTO TraceX fornisce report di analisi di sistema incorporati disponibili tramite un solo clic del pulsante sulla barra degli strumenti di TraceX. Questi pulsanti e report includono:

![Genera rapporto del profilo di esecuzione](./media/overview-tracex/execution-profile-report-button.jpg) Genera rapporto del profilo di esecuzione

![Genera rapporto statistiche prestazioni](./media/overview-tracex/performance-statistics-report-button.jpg) Genera rapporto statistiche prestazioni

![Genera report sull'utilizzo dello stack di thread](./media/overview-tracex/thread-stack-usage-report-button.jpg) Genera report sull'utilizzo dello stack di thread

### <a name="trace-data-collected-by-azure-rtos-threadx"></a>Traccia dati raccolti da Azure RTO ThreadX

Azure RTO TraceX è progettato per funzionare con Azure RTO ThreadX, che crea un database di eventi di sistema e di applicazione nel sistema di destinazione durante la fase di esecuzione. Questi eventi includono:

* commutazioni di contesto del thread
* precedenza
* sospensioni
* terminazioni
* interruzioni di sistema
* eventi specifici dell'applicazione
* tutte le chiamate all'API ThreadX di Azure RTO
* tutte le chiamate all'API NetX di Azure RTO
* tutte le chiamate all'API FileX di Azure RTO
* tutte le chiamate all'API USBX di Azure RTO
* Icone e informazioni definite dall'applicazione

Gli eventi vengono registrati sotto controllo del programma, con timestamp e identificazione dei thread attivi, in modo che possano essere visualizzati in un secondo momento nella sequenza temporale appropriata e associati al thread appropriato. La registrazione degli eventi può essere arrestata e riavviata in modo dinamico dal programma dell'applicazione, ad esempio quando viene rilevata un'area di interesse. In questo modo si evita di ingombrare il database e si utilizza la memoria di destinazione quando il sistema funziona correttamente.

### <a name="azure-rtos-tracex-is-like-a-software-logic-analyzer"></a>Azure RTO TraceX è come un analizzatore della logica software

Una volta che il registro eventi è stato caricato dalla memoria di destinazione all'host, Azure RTO TraceX Visualizza gli eventi graficamente su un asse orizzontale che rappresenta il tempo, con i vari thread dell'applicazione e le routine di sistema a cui gli eventi sono correlati elencati lungo l'asse verticale. Azure RTO TraceX crea un "Analizzatore della logica software" nell'host, rendendo visibili gli eventi di sistema. Gli eventi sono rappresentati da icone con codifica a colori, situate in corrispondenza del punto di occorrenza lungo la sequenza temporale orizzontale, a destra del thread o routine di sistema pertinente. Quando si seleziona un'icona di evento, vengono visualizzate le informazioni corrispondenti per tale evento, nonché le informazioni per i due eventi precedenti e due successivi. Questo consente di accedere rapidamente a un singolo clic alle informazioni più immediate sull'evento e sui relativi eventi immediatamente circostanti. Azure RTO TraceX offre una visualizzazione di riepilogo che Mostra tutti gli eventi di sistema su una singola linea orizzontale per semplificare l'analisi dei sistemi con molti thread.

### <a name="sequential-view-mode"></a>Modalità di visualizzazione sequenziale

Per selezionare la modalità di visualizzazione sequenziale, fare clic sulla scheda "visualizzazione sequenziale". Questa è la modalità predefinita. In questa modalità, gli eventi vengono visualizzati immediatamente dopo l'altro, indipendentemente dal tempo trascorso tra di essi. Si noti anche il righello sopra l'area di visualizzazione. Viene visualizzato il numero di evento relativo dall'inizio della traccia. Questa modalità è la modalità predefinita ed è particolarmente utile per ottenere una panoramica di ciò che accade nel sistema.

![Modalità di visualizzazione sequenziale](./media/user-guide/screen_shot_10.png)

**Modalità di visualizzazione sequenziale**

### <a name="time-view-mode"></a>Modalità di visualizzazione dell'ora

In questa modalità, gli eventi vengono visualizzati in un momento relativo, con una barra verde uniforme utilizzata per visualizzare l'esecuzione tra gli eventi. Questa modalità è particolarmente utile per vedere dove si verifica la maggior parte dell'elaborazione nel sistema, che consente agli sviluppatori di ottimizzare il sistema per migliorare le prestazioni e/o la velocità di risposta.

Si noti anche il righello sopra la visualizzazione dell'evento. Questo righello Mostra i cicli relativi dall'inizio della traccia, come derivati dal timestamp instrumentato nella registrazione della traccia eventi all'interno di Azure RTO ThreadX. Se i timestamp sono troppo vicini (timer a bassa frequenza), gli eventi verranno eseguiti insieme. Viceversa, se i timestamp sono troppo distanti (timer ad alta frequenza), gli eventi saranno troppo lontani. La scelta del timestamp di frequenza appropriato è una considerazione importante per rendere significativo la visualizzazione relativa del tempo.

![Modalità di visualizzazione dell'ora](./media/user-guide/screen_shot_31.png)

### <a name="system-summary-line"></a>Riga di riepilogo sistema

Azure RTO TraceX fornisce anche una singola riga di riepilogo che include tutti gli eventi nella stessa riga. La riga di riepilogo contiene un riepilogo del contesto, nonché il riepilogo degli eventi corrispondente sotto. Questo semplifica la visualizzazione di una panoramica di un sistema complesso. La barra di riepilogo è particolarmente utile nei sistemi con un numero elevato di thread. Senza tale linea di riepilogo, l'utente dovrà seguire le interazioni di sistema complesse usando la barra di scorrimento verticale per seguire il contesto di esecuzione.

Azure RTO TraceX elenca i contesti di sistema sul lato sinistro dello schermo.
Gli eventi che si verificano in un determinato contesto vengono visualizzati sulla linea orizzontale a destra del contesto. In questo modo, l'utente può facilmente determinare il contesto in cui si è verificato l'evento e seguire la riga del contesto per visualizzare tutti gli eventi che si sono verificati in un determinato contesto.

![Riga di riepilogo sistema](./media/user-guide/screen_shot_32.png)

**Riga di riepilogo sistema**

Le prime due voci di contesto sono sempre i contesti "interrupt" e "Initialize/Idle". Il contesto "interrupt" rappresenta tutti gli eventi di sistema effettuati dalle routine del servizio di interrupt (ISRs). Il contesto di "inizializzazione/inattività" rappresenta due contesti in Azure RTO ThreadX. Gli eventi che si verificano durante tx_application_define sono eventi di inizializzazione e vengono visualizzati nel contesto di inizializzazione/inattività. Se il sistema è inattivo e pertanto non si verificano eventi, la barra verde che rappresenta "in esecuzione" nella visualizzazione ora viene disegnata nel contesto "Inizializza/inattiva".

## <a name="methods-of-navigation"></a>Metodi di navigazione

Azure RTO TraceX consente allo sviluppatore di specificare come funzionano i pulsanti di navigazione "Avanti" e "precedente".

![Pulsanti di spostamento](./media/user-guide/event.png)

Se si seleziona "Event", la navigazione viene eseguita nell'evento successivo o precedente. Se si seleziona "context", la navigazione viene eseguita nell'evento successivo o precedente nello stesso contesto. Se si seleziona "oggetto", la navigazione viene eseguita nell'evento successivo o precedente dell'oggetto corrente, ad esempio, gli eventi associati a una coda specifica. Se l'opzione "Switches" è selezionata, la navigazione viene eseguita sul cambio di contesto successivo o precedente. Se si seleziona "stesso ID", la navigazione viene eseguita nell'evento successivo o precedente per lo stesso ID evento.

### <a name="event-information-display"></a>Visualizzazione delle informazioni sugli eventi

Azure RTO TraceX fornisce informazioni dettagliate su alcuni eventi 300. Sono inclusi sei eventi interni ThreadX di Azure RTO, due eventi ISR (immissione ed uscita), 14 eventi FileX di Azure RTO interni, 42 eventi interni di Azure RTO NETX e un evento definito dall'utente. Gli eventi rimanenti corrispondono direttamente ad Azure RTO ThreadX, Azure RTO FileX e Azure RTO NetX API Services.
Indipendentemente dal fatto che sia selezionata la modalità di visualizzazione sequenziale o temporale, un passaggio del mouse su qualsiasi evento nell'area di visualizzazione genera informazioni dettagliate sugli eventi visualizzati in prossimità dell'evento. Il passaggio del mouse sull'evento 494 nel file di traccia demo demo_threadx. trx è illustrato di seguito:

![Mouse-Over Visualizza altre informazioni](./media/user-guide/screen_shot_37.png)

**Ulteriori informazioni vengono visualizzate tramite il pulsante del mouse**

Ogni evento visualizzato contiene informazioni standard sul contesto e sull'ora e sul timestamp relativi. Il campo contesto indica il contesto in cui si è verificata l'evento. Sono presenti esattamente quattro contesti: thread, Idle, ISR e inizializzazione. Quando si verifica un evento in un contesto di thread, il nome del thread e la relativa priorità in quel momento vengono raccolti e visualizzati come illustrato in precedenza. L'ora relativa indica il numero relativo di cicli del timer dall'inizio della traccia. L'indicatore di ora RAW Visualizza l'origine dell'ora non elaborata dell'evento. Infine, vengono visualizzate tutte le informazioni specifiche dell'evento.

### <a name="zooming-in-and-out"></a>Zoom avanti e indietro

Per impostazione predefinita, Azure RTO TraceX Visualizza gli eventi in una dimensione di facile visualizzazione con un mapping di 1:1 pixel: segno di graduazione. L'utente può ingrandire o ridurre le impostazioni desiderate. Lo zoom indietro al 100% è utile per visualizzare l'intera traccia nella visualizzazione corrente, mentre lo zoom avanti è utile nelle condizioni in cui gli eventi si sovrappongono a causa della risoluzione dell'origine del timestamp.

![Zoom-Out al 100% di visualizzazione o zoom avanti per i dettagli](./media/user-guide/screen_shot_41.png)

**Zoom indietro alla visualizzazione 100% o zoom avanti per i dettagli**

Quando si esegue lo zoom indietro al 100%, mostrando l'intera traccia all'interno della pagina di visualizzazione corrente, è facile vedere tutte le esecuzioni del contesto acquisite nella traccia e gli eventi generali che si verificano all'interno di tali contesti. Si noti che "thread 1" e "thread 2" vengono eseguiti più spesso. La colorazione blu per gli eventi suggerisce anche che questi thread stanno effettuando chiamate al servizio di Accodamento (gli eventi della coda sono di colore blu).

Il ripristino in una visualizzazione icone completa è altrettanto semplice; Il pulsante zoom avanti può essere selezionato ripetutamente oppure è possibile che venga immesso un fattore pari a 100.

### <a name="delta-ticks-between-events"></a>Cicli Delta tra gli eventi

Determinare il numero di cicli tra i vari eventi in Azure RTO TraceX è semplice: è sufficiente fare clic sull'evento iniziale e trascinare il mouse sull'evento finale.
Il numero Delta di cicli tra gli eventi viene visualizzato nell'angolo superiore destro dello schermo.

![Cicli Delta](./media/user-guide/screen_shot_42.png)

**Cicli Delta**

I cicli Delta indicano che sono trascorsi 5032 cicli tra l'evento 494 e l'evento 496. Questa operazione può anche essere calcolata manualmente esaminando i timestamp relativi di ogni evento e sottraendo, ma l'uso dell'interfaccia utente grafica è facile e immediato.

### <a name="priority-inversions"></a>Inversioni di priorità

Azure RTO TraceX Visualizza automaticamente le inversioni di priorità rilevate nel file di traccia. Le inversioni con priorità sono definite come condizioni in cui un thread con priorità più alta è bloccato tentando di ottenere un mutex attualmente di proprietà di un thread con priorità inferiore. Questa condizione viene definita "deterministica" perché il sistema è stato configurato per funzionare in questo modo. Per informare l'utente, Azure RTO TraceX Mostra gli intervalli di inversione della priorità "deterministico" come colore del salmone chiaro.

Azure RTO TraceX Visualizza anche le inversioni di priorità "non deterministiche". Queste inversioni con priorità sono diverse dalle inversioni di priorità "deterministiche", in quanto un altro thread di un livello di priorità diverso è stato eseguito in una "deterministica" inversione di priorità, rendendo quindi il tempo entro l'inversione di priorità alquanto "non deterministica". Questa condizione è spesso sconosciuta all'utente e può essere molto grave. Per avvertire l'utente di questa condizione, Azure RTO TraceX Mostra inversioni di priorità "non deterministiche" come colore del salmone più luminoso.

![Inversione di priorità deterministica e non deterministica](./media/user-guide/screen_shot_43.png)

**Inversione di priorità deterministica e non deterministica**

### <a name="execution-profile"></a>Profilo di esecuzione

Azure RTO TraceX fornisce un report del profilo di esecuzione predefinito per tutti i contesti di esecuzione all'interno del file di traccia attualmente caricato.

![Profilo di esecuzione](./media/user-guide/execution_profile.png)

### <a name="performance-statistics"></a>Performance statistics

Azure RTO TraceX fornisce un report di statistiche sulle prestazioni predefinito per il file di traccia attualmente caricato.

![Performance statistics](./media/user-guide/performance_statistics.png)

### <a name="thread-stack-usage"></a>Utilizzo dello stack di thread

Azure RTO TraceX fornisce un report di utilizzo dello stack predefinito per tutti i thread in esecuzione all'interno del file di traccia attualmente caricato.

![Utilizzo dello stack](./media/user-guide/thread_stack_usage.png)

Azure RTO TraceX presenta le statistiche sulle prestazioni di Azure RTO FileX del file di traccia attualmente caricato. Queste informazioni vengono visualizzate per l'intero sistema, in tutti gli oggetti multimediali aperti.

![Statistiche FileX](./media/user-guide/filex_statistics.png)

### <a name="azure-rtos-netx-statistics"></a>Statistiche NetX di Azure RTO

Azure RTO TraceX presenta anche le statistiche sulle prestazioni di NetX del file di traccia attualmente caricato. Queste informazioni vengono visualizzate per l'intero sistema.

![Statistiche NetX](./media/user-guide/netx_statistics.png)

### <a name="raw-trace-dump"></a>Dump traccia RAW

Azure RTO TraceX può creare un file di traccia non elaborato in formato testo e avviare il blocco note per visualizzarlo.

![Dump traccia RAW](./media/user-guide/raw_trace_dump.png)

Si noti che tutte le cifre relative a tempistiche e dimensioni elencate sono stime e possono essere diverse nella piattaforma di sviluppo
