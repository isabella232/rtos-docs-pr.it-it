---
title: Capitolo 3-Descrizione di Azure RTO TraceX
description: Questo capitolo descrive la funzionalità complessiva dello strumento di analisi del sistema TraceX di Azure RTO, inclusa la funzionalità complessiva della GUI.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 1c974b353c92e0a3cf51c92818794197cf999582
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823528"
---
# <a name="chapter-3---description-of-azure-rtos-tracex"></a>Capitolo 3-Descrizione di Azure RTO TraceX

Questo capitolo descrive la funzionalità complessiva dello strumento di analisi del sistema TraceX di Azure RTO, inclusa la funzionalità complessiva della GUI. 

## <a name="display-overview"></a>Visualizza panoramica

**Nella figura 4** è illustrata la finestra di visualizzazione principale dello strumento di analisi del sistema TraceX. Il layout è semplice: i contesti di esecuzione sono rappresentati dagli elementi verticali sul lato sinistro; ad esempio, inizializzazione, interrupt, inattività e le varie voci di thread. Gli eventi che si verificano in ogni contesto vengono visualizzati orizzontalmente nella stessa riga di contesto. Ad esempio, gli eventi **QR** indicati di seguito mostrano che **_thread 2_*_ sta effettuando chiamate successive a _*_tx_queue_receive_**.

![Screenshot della finestra di visualizzazione principale dello strumento di analisi del sistema TraceX.](./media/user-guide/screen_shot_10.png)


**FIGURA 5**

Le modifiche al contesto sono rappresentate dalle linee nere verticali che connettono le linee del contesto. L'evento attualmente selezionato è rappresentato da una linea rossa verticale a tinta unita. In questo esempio è selezionato l'evento 494.

## <a name="title-bar"></a>TitleBar

La barra del titolo TraceX fornisce diverse informazioni utili. Prima è la versione corrente di TraceX. Il secondo è il percorso completo del file di traccia attualmente aperto. L'esempio nella **Figura 6** Mostra **_TraceX_*_ version _*_6.0.0_*_ Visualizza il file di traccia _*_demo_threadx. TRX_** .

![Screenshot della barra del titolo TraceX.](./media/user-guide/screen_shot_11.png)

**FIGURA 6**

## <a name="tool-bar"></a>ToolBar

La barra degli strumenti di TraceX offre diversi pulsanti per aprire i file di traccia e controllare gli elementi della relativa visualizzazione.

![Screenshot della barra degli strumenti TraceX.](./media/user-guide/screen_shot_12.png)


**FIGURA 7**

I pulsanti della barra degli strumenti di TraceX, da sinistra a destra, sono definiti come segue:
                                             
| **Button**                         | **Funzione** |
| ---------------------------------- | ----------------------------------------------------------------------------------------------- |
| ![Pulsante Apri file di traccia](./media/user-guide/screen_shot_13.png)      | Aprire un file di traccia |
| ![Pulsante Apri Guida utente](./media/user-guide/screen_shot_14.png)      | Apri questo manuale dell'utente |
| ![Pulsante Genera profilo di esecuzione](./media/user-guide/screen_shot_15.png)       | Genera profilo di esecuzione |
| ![ Pulsante genera statistiche prestazioni](./media/user-guide/screen_shot_16.png)       | Genera statistiche sulle prestazioni |
| ![Pulsante genera utilizzo stack thread](./media/user-guide/screen_shot_17.png)       | Genera utilizzo stack di thread |
| ![Pulsante Visualizza evento selezionato](./media/user-guide/screen_shot_18.png)       | Visualizza evento attualmente selezionato |
| ![Cercare pulsante](./media/user-guide/screen_shot_19.png)      | Cerca eventi |
| ![Pulsante zoom avanti](./media/user-guide/screen_shot_20.png)      | Eseguire lo zoom avanti. |
| ![Pulsante Zoom Visualizza](./media/user-guide/screen_shot_21.png)      | Selezionare percentuale di zoom schermo, dove 100% indica che l'intero file di traccia viene visualizzato nella visualizzazione corrente. |
| ![Pulsante Zoom indietro](./media/user-guide/screen_shot_22.png)      | Eseguire lo zoom indietro. |
| ![Pulsante Seleziona primo evento](./media/user-guide/screen_shot_23.png)      | Selezionare il primo evento. |
| ![Pulsante Visualizza pagina evento precedente](./media/user-guide/screen_shot_24.png)      | Visualizza la pagina dell'evento precedente. |
| ![Pulsante Visualizza evento precedente](./media/user-guide/screen_shot_25.png)      | Visualizza l'evento precedente. |
| ![Pulsante di spostamento successivo/precedente](./media/user-guide/screen_shot_26.png)      | Determinare come operano i pulsanti di navigazione successivi/precedenti. Se ***Event** _ è selezionato, la navigazione viene eseguita nell'evento successivo o precedente. Se il _*_contesto_*_ è selezionato, la navigazione viene eseguita nell'evento successivo o precedente nel contesto specificato. Se l' _*_oggetto_*_ è selezionato, la navigazione viene eseguita nell'evento successivo o precedente dell'oggetto specificato. ad esempio, eventi associati a una coda specifica. Se è selezionata l'opzione _*_Opzioni_*_ , la navigazione viene eseguita sulla modifica successiva o precedente nel contesto. Se è selezionata l'opzione _ *_ID_**, la navigazione viene eseguita nell'evento successivo o precedente dell'ID evento specificato. |
| ![Pulsante Mostra evento successivo](./media/user-guide/screen_shot_27.png)      | Visualizza l'evento successivo. |
| ![Pulsante Visualizza pagina evento successivo](./media/user-guide/screen_shot_28.png)      | Visualizza la pagina di evento successiva. |
| ![Pulsante Seleziona ultimo evento](./media/user-guide/screen_shot_29.png)      | Selezionare ultimo evento. |

## <a name="display-mode-tabs"></a>Schede modalità di visualizzazione

TraceX Visualizza gli eventi di sistema in due modi diversi: *sequenziale* e *temporale relativo*. La modalità predefinita è sequenziale e corrisponde alla modalità mostrata nella **Figura 8**.

Per modificare la modalità è sufficiente selezionare le schede ***visualizzazione sequenziale** _ o _*_visualizzazione ora_*_ nella finestra TraceX. _*Figura 8** Visualizza le schede **_visualizzazione sequenziale_*_ e *_visualizzazione ora_**.

![Screenshot delle schede visualizzazione sequenziale e visualizzazione ora.](./media/user-guide/screen_shot_30.png)

**FIGURA 8**

## <a name="sequential-view-mode"></a>Modalità di visualizzazione sequenziale

La modalità di visualizzazione sequenziale è selezionata dalla scheda ***visualizzazione sequenziale** visualizzata in _ * figura 8 * *. Si tratta della modalità predefinita. In questa modalità vengono visualizzati gli eventi im. /mediately l'uno dopo l'altro, indipendentemente dal tempo trascorso tra di essi. Si noti anche il righello sopra l'area di visualizzazione nella **Figura 8**. Viene visualizzato il numero di evento relativo dall'inizio della traccia.

Questa modalità è la modalità predefinita ed è utile per ottenere una panoramica corretta di ciò che accade nel sistema.

## <a name="time-view-mode"></a>Modalità di visualizzazione dell'ora

La modalità di visualizzazione ora è selezionata dal pulsante ***visualizzazione ora** _. _ *Figura 9** Mostra la stessa traccia eventi della **Figura 8** eccetto la modalità di visualizzazione tempo. In questa modalità, gli eventi vengono visualizzati in un momento relativo, con la barra verde uniforme utilizzata per visualizzare l'esecuzione tra gli eventi. Questa modalità è utile per vedere dove si verifica la maggior parte dell'elaborazione nel sistema, che consente agli sviluppatori di ottimizzare il sistema per migliorare le prestazioni e/o la velocità di risposta.

![Screenshot della scheda visualizzazione tempo.](./media/user-guide/screen_shot_31.png)

**FIGURA 9**

Si noti anche il righello sopra la visualizzazione dell'evento nella **Figura 9**. Questo righello Mostra i cicli relativi dall'inizio della traccia, come derivati dal timestamp instrumentato nella registrazione della traccia eventi all'interno di ThreadX. Se gli indicatori timestamp sono troppo vicini (timer a bassa frequenza), gli eventi verranno eseguiti insieme. Viceversa, se i timestamp sono troppo distanti (timer ad alta frequenza), gli eventi saranno troppo lontani. La scelta del timestamp di frequenza appropriato è una considerazione importante per rendere significativo la visualizzazione relativa del tempo.

## <a name="system-summary-line"></a>Riga di riepilogo sistema

TraceX fornisce anche una singola riga di riepilogo (il contesto superiore nella **Figura 10**) che include tutti gli eventi nella stessa riga. Questo semplifica la visualizzazione di una panoramica di un sistema complesso. La barra di riepilogo è particolarmente utile nei sistemi con molti thread. Senza questa linea di riepilogo, è necessario seguire le interazioni di sistema complesse usando la barra di scorrimento verticale per seguire il contesto di esecuzione.

![Screenshot della riga di riepilogo sistema nella scheda visualizzazione sequenziale.](./media/user-guide/screen_shot_32.png)


**FIGURA 10**

La riga di riepilogo contiene un riepilogo del contesto, nonché il riepilogo degli eventi corrispondente sotto. Nell'esempio illustrato nella **Figura 10,** è facile vedere che il **_thread 2_*_ è in esecuzione e interrotto. L'interrupt genera la precedenza di _*_thread 3_**, ***thread 6** _, _*_thread 4_*_ e _*_thread 7_*_, dopo il quale _ *_thread 2_** riprende l'esecuzione.

## <a name="system-contexts"></a>Contesti di sistema

TraceX elenca i contesti di sistema sul lato sinistro dello schermo, come illustrato nella **Figura 11**. Gli eventi che si verificano in un determinato contesto vengono visualizzati sulla linea orizzontale a destra del contesto. In questo modo, è possibile verificare facilmente il contesto in cui si è verificato l'evento e seguire la riga del contesto per visualizzare tutti gli eventi che si sono verificati in un determinato contesto.

Le prime voci di contesto di traino sono sempre i contesti ***interrupt** _ e _*_Inizializza/inattività_*_ . Il contesto di _*_interrupt_*_ rappresenta tutti gli eventi di sistema effettuati dalle routine del servizio di interrupt (IRS). Il contesto di _*_inizializzazione/inattività_*_ rappresenta due contesti in threadX. Gli eventi che si verificano durante _*_tx_application_define_*_ sono il contesto di _*_inizializzazione/inattività_*_ . Se il sistema è inattivo e pertanto non si verificano eventi, la barra verde che rappresenta l' _*_esecuzione_*_ nella visualizzazione ora viene disegnata nel contesto _ *_Initialize/Idle_**.

![Screenshot dei contesti di sistema sul lato sinistro dello schermo.](./media/user-guide/screen_shot_33.png)

**FIGURA 11**

Nell'esempio della **Figura 11** sono presenti nove contesti di thread, a partire dal contesto del **_thread del timer di sistema_*. Ulteriori informazioni su un singolo contesto sono disponibili posizionando il mouse su tale contesto. Le informazioni aggiuntive includono l'indirizzo dello stack iniziale del thread, l'indirizzo dello stack finale, le dimensioni totali, la percentuale utilizzata, la percentuale di esecuzione relativa, il numero di sospensioni, le riprese e la priorità più alta e minima durante la traccia. _* La figura 12** Mostra le informazioni per il **_thread 0_**.

![Screenshot delle informazioni per il thread 0.](./media/user-guide/screen_shot_34.png)


**FIGURA 12**

È anche possibile spostare i contesti per raggruppare quelli di maggiore interesse. Questa operazione viene eseguita trascinando il contesto o facendo clic con il pulsante destro del mouse sul contesto. Facendo clic con il pulsante destro del mouse sul contesto, viene visualizzata una finestra di dialogo che consente di trasferire il contesto nella parte superiore o inferiore. 

Se si seleziona ***sposta all'inizio**, il contesto del _*_thread 3_*_ verrà spostato nella parte superiore dell'elenco di contesti, come illustrato nella figura 13 * *.

![Screenshot del contesto spostato nella parte superiore dell'elenco di contesti.](./media/user-guide/screen_shot_35.png)


**FIGURA 13**

## <a name="thread-status-information"></a>Informazioni sullo stato del thread

Se abilitata, TraceX Visualizza lo stato di ogni thread tramite una linea colorata sul contesto del thread. Una linea verde indica che il thread è in uno stato "pronto", mentre una riga di qualsiasi altro colore indica che il thread è sospeso. Per i thread sospesi, il colore della riga indica il tipo di oggetto ThreadX su cui il thread è sospeso. Ad esempio, nella **Figura 13** la linea verde sul **contesto _ del _thread timer di sistema_*a partire dall'evento 147 indica che il thread del*_timer di sistema_ _ *è pronto. Prima dell'evento 147 e dopo l'evento 154, l'assenza della linea verde indica che il thread del*_timer di sistema_ _ *è pronto. Prima dell'evento 147 e dopo l'evento 154, l'assenza della linea verde indica che il thread del*_timer di sistema_** è sospeso.

![Screenshot dello stato di ogni thread tramite una linea colorata sul contesto del thread.](./media/user-guide/screen_shot_36.png)

**FIGURA 14**

Sono disponibili tre modalità di visualizzazione dello stato dei thread, disponibile tramite il menu ***Opzioni-> stato _ righe**. L'opzione _*_solo pronto_*_ Mostra solo le linee di stato (verde) pronte, ma non visualizza alcuna riga di stato di sospensione. Questa è l'opzione predefinita per TraceX. L'opzione _ *_All on_** consente di visualizzare tutte le righe di stato (pronte e sospese).

Infine, l'opzione ***All Off disattiva*** la visualizzazione di tutte le righe di stato.

## <a name="event-information-display"></a>Visualizzazione delle informazioni sugli eventi

TraceX fornisce informazioni dettagliate su alcuni eventi di run-time 600, tra cui ThreadX, FileX, NetX, NetX Duo e chiamate API USBX ed eventi interni. TraceX supporta anche fino a altri 61.439 eventi univoci definiti dall'utente.

Indipendentemente dal fatto che sia selezionata la modalità di visualizzazione sequenziale o temporale, un passaggio del mouse su qualsiasi evento nell'area di visualizzazione genera informazioni dettagliate sugli eventi visualizzati in prossimità dell'evento. Il passaggio del mouse sull'evento 143 nel file di traccia demo ***demo_threadx. TRX** _ è illustrato nella figura 15 * *:

![Screenshot del passaggio del mouse sull'evento 143 in un file di traccia di esempio](./media/user-guide/screen_shot_37.png)

**FIGURA 15**

Ogni evento visualizzato contiene informazioni standard sul ***contesto** _ e sull'ora e sul _*_timestamp_*_ _*_relativi_*_ . Il campo contesto indica il contesto in cui si è verificata l'evento. Sono presenti esattamente quattro contesti: thread, Idle, ISR e inizializzazione. Quando si verifica un evento in un contesto di thread, il nome del thread e la relativa priorità in quel momento vengono raccolti e visualizzati come illustrato in precedenza. L' _*_ora relativa_*_ indica il numero relativo di cicli del timer dall'inizio della traccia. _ *_Timestamp RAW_** Visualizza l'origine dell'ora non elaborata dell'evento. Infine, vengono visualizzate tutte le informazioni specifiche dell'evento. Queste informazioni sono descritte in dettaglio nel resto di questo capitolo.

Per informazioni dettagliate sugli eventi è anche possibile fare doppio clic su qualsiasi evento. Il doppio clic sull'evento 143 è illustrato nella **Figura 16**:

![Screenshot delle informazioni dettagliate sull'evento quando si fa doppio clic su un evento.](./media/user-guide/screen_shot_38.png)

**FIGURA 16**

La possibilità di visualizzare più eventi in una sola volta fornisce all'utente una visualizzazione più dettagliata di ciò che si è verificato. La visualizzazione affiancata è molto utile poiché molti eventi sono correlati tra loro. Questa operazione viene eseguita facendo doppio clic su più eventi.

## <a name="current-event-display"></a>Visualizzazione evento corrente

TraceX Visualizza l'evento corrente, in una finestra separata, quando viene selezionato dall'utente tramite ***visualizza > evento corrente*** o facendo clic sul pulsante evento corrente sulla barra degli strumenti. Dopo la selezione, TraceX Visualizza l'evento attualmente selezionato in una finestra autonoma e aggiorna questa finestra ogni volta che viene selezionato un altro evento.

## <a name="event-searching"></a>Ricerca di eventi

TraceX offre una funzionalità di ricerca di eventi completa. I campi ID evento e informazioni di ogni evento sono i parametri di ricerca principali. Se non si specifica un valore per un parametro di ricerca, il parametro verrà rimosso in modo efficace dal parametro search. Inoltre, la ricerca può essere eseguita in modo che tutti i parametri trovati soddisfino la ricerca o che tutti i parametri siano disponibili per soddisfare la ricerca. Anche la ricerca può essere limitata a un particolare contesto o coprire tutti i contesti nella traccia. La chiamata alla ricerca di eventi viene eseguita selezionando il pulsante ***Cerca per valore** _ sulla barra degli strumenti, come illustrato nella _Figura 17 * *. Quando viene selezionata, viene visualizzata la finestra di dialogo di ricerca che specifica tutti i parametri per la ricerca. I pulsanti *_Avanti_*_ e _*_indietro_*_ nella finestra di dialogo di ricerca possono essere usati per trovare gli eventi successivi e precedenti che corrispondono ai criteri di ricerca specificati. _ *Figura 17** Visualizza la finestra di dialogo di ricerca.

![Screenshot della ricerca di eventi.](./media/user-guide/screen_shot_39.png)

**FIGURA 17**

![Screenshot della finestra di dialogo di ricerca.](./media/user-guide/screen_shot_40.png)

**FIGURA 18**

## <a name="zooming-in-and-out"></a>Zoom avanti e indietro

Per impostazione predefinita, TraceX Visualizza gli eventi con le dimensioni massime. È possibile ingrandire o ridurre le esigenze. Lo zoom indietro è utile per visualizzare gli eventi complessivi acquisiti nella traccia, mentre lo zoom avanti è utile nelle condizioni in cui gli eventi si sovrappongono a causa della risoluzione dell'origine del timestamp. **Nella figura 19** viene illustrato il file **_demo_threadx. TRX_** , in modo che venga visualizzato il 100% del file di traccia.

![Screenshot di un file di esempio ingrandito in modo da visualizzare il 100% del file di traccia.](./media/user-guide/screen_shot_41.png)

**FIGURA 19**

Quando si esegue lo zoom indietro al 100% per visualizzare l'intera traccia all'interno della pagina di visualizzazione corrente, è facile vedere tutto l'esecuzione del contesto acquisita nella traccia e gli eventi generali che si verificano all'interno di tali contesti. Si noti nella **Figura 16** che il thread **_1_*_ e _*_thread 2_** vengono eseguiti più spesso. La colorazione blu per gli eventi suggerisce anche che questi thread stanno effettuando chiamate al servizio di Accodamento (gli eventi della coda sono di colore blu).

Il ripristino in una visualizzazione icone completa è altrettanto semplice; Il pulsante zoom avanti può essere selezionato ripetutamente oppure è possibile che venga immesso un fattore pari a 100.

## <a name="delta-ticks-between-events"></a>Cicli Delta tra gli eventi

Determinare il numero di cicli tra i vari eventi in TraceX è semplice: fare clic sull'evento iniziale e trascinare il mouse sull'evento finale. Il numero Delta di cicli tra gli eventi viene visualizzato nell'angolo superiore destro dello schermo, come illustrato nella **Figura 17**.

![Screenshot del numero Delta di cicli tra gli eventi.](./media/user-guide/screen_shot_42.png)

**FIGURA 17**

I cicli Delta mostrati nella **Figura 17** mostrano che sono trascorsi 5032 cicli tra l'evento 125 e l'evento 154. Questa operazione può anche essere calcolata manualmente esaminando i timestamp relativi di ogni evento e sottraendo, ma l'uso dell'interfaccia utente grafica è facile e immediato.

## <a name="actual-time-display"></a>Visualizzazione dell'ora effettiva

Se abilitata, TraceX Visualizza l'ora effettiva in microsecondi nella **visualizzazione temporale** _ e per le varie informazioni sul tempo Delta visualizzate da TraceX. Per impostazione predefinita, la visualizzazione dell'ora effettiva è disabilitata. Per abilitare la visualizzazione dell'ora effettiva, il numero di cicli per microsecondo deve essere immesso tramite la selezione di menu _ *_Opzioni-> cicli per microsecondi_** (il valore da immettere è determinato dall'origine del timer hardware utilizzata per la registrazione degli eventi TraceX nella destinazione).

## <a name="priority-inversions"></a>Inversioni di priorità

TraceX Visualizza automaticamente le inversioni prioritarie rilevate nel file di traccia. Le inversioni con priorità sono definite come condizioni in cui un thread con priorità più alta è bloccato tentando di ottenere un mutex attualmente di proprietà di un thread con priorità inferiore. Questa condizione è definita *deterministica*, perché il sistema è stato configurato per funzionare in questo modo. Per informare l'utente, TraceX Mostra gli intervalli di inversione con priorità *deterministica* come colore del salmone chiaro.

TraceX Visualizza anche le inversioni *di priorità non deterministiche* . Queste inversioni con priorità sono diverse dalle inversioni con priorità *deterministica* , in quanto un altro thread di un livello di priorità diverso è stato eseguito nella parte centrale di un'inversione di priorità *deterministica* , rendendo quindi il tempo entro l'inversione di priorità alquanto *non deterministica*. Questa condizione è spesso sconosciuta all'utente e può essere molto grave. Per avvertire l'utente di questa condizione, TraceX Mostra inversioni di priorità *non deterministiche* come colore del salmone più luminoso. **Nella figura 18** sono illustrate le inversioni di priorità *deterministiche* e *non deterministiche* .

![Screenshot della priorità inversione in un file di traccia.](./media/user-guide/screen_shot_43.png)

**FIGURA 18**

La **Figura 18** Mostra un'inversione di priorità *deterministica* dall'evento 398 all'evento 402. In questo intervallo, il **thread 0** _ con priorità più alta viene bloccato su un mutex di proprietà di un thread con priorità inferiore _*_1_*_. All'evento 402, _ *_thread 1_** rilascia il mutex e pertanto termina l'inversione della priorità.

L'area ombreggiata più luminosa Mostra un'inversione di priorità *non deterministica* tra l'evento 408 e l'evento 420. Ciò che rende questa operazione *non deterministica* è che, mentre ***thread 1** _ contiene il mutex a cui è bloccato il _*_thread_*_ con priorità più elevata, si verifica un interrupt che riprende _ *_thread 2_* *, che viene quindi eseguito e prolungato il tempo per cui il sistema è in inversione con priorità. Questa condizione può essere piuttosto complessa e difficile da identificare; Tuttavia, con TraceX è facilmente identificabile.
