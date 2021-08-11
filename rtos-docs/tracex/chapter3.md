---
title: Capitolo 3 - Descrizione di Azure RTOS TraceX
description: Questo capitolo descrive la funzionalità complessiva dello strumento di analisi Azure RTOS di sistema TraceX, inclusa la funzionalità complessiva della relativa interfaccia utente grafica.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: bb466427374659027bf91c7bb46c74e7d2ff561d200db9dab1a2bddbe6635ef4
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116789348"
---
# <a name="chapter-3---description-of-azure-rtos-tracex"></a>Capitolo 3 - Descrizione di Azure RTOS TraceX

Questo capitolo descrive la funzionalità complessiva dello strumento di analisi Azure RTOS di sistema TraceX, inclusa la funzionalità complessiva della relativa interfaccia utente grafica. 

## <a name="display-overview"></a>Panoramica della visualizzazione

**La figura 4** mostra la finestra di visualizzazione principale dello strumento di analisi del sistema TraceX. Il layout è semplice: i contesti di esecuzione sono rappresentati dagli elementi verticali sul lato sinistro; ad esempio inizializzazione, interrupt, inattività e le varie voci del thread. Gli eventi che si verificano in ogni contesto vengono visualizzati orizzontalmente sulla stessa riga di contesto. Ad esempio, gli **eventi A QR** mostrati di seguito mostrano che il **_thread 2_*_ sta effettuando chiamate successive a _*_tx_queue_receive_**.

![Screenshot della finestra di visualizzazione principale dello strumento di analisi del sistema TraceX.](./media/user-guide/screen_shot_10.png)


**FIGURA 5**

Le modifiche al contesto sono rappresentate dalle linee nere verticali che connettono le linee di contesto. L'evento attualmente selezionato è rappresentato da una linea verticale rossa continua. In questo esempio viene selezionato l'evento 494.

## <a name="title-bar"></a>TitleBar

La barra del titolo di TraceX fornisce diverse informazioni utili. Il primo è la versione corrente di TraceX. Il secondo è il percorso completo del file di traccia attualmente aperto. L'esempio nella figura **6** illustra **_TraceX_*_ version _*_6.0.0_ _ visualizza il file di traccia *_*_demo_threadx.trx._**

![Screenshot della barra del titolo di TraceX.](./media/user-guide/screen_shot_11.png)

**FIGURA 6**

## <a name="tool-bar"></a>ToolBar

La barra degli strumenti TraceX fornisce diversi pulsanti per aprire i file di traccia e controllare gli elementi della relativa visualizzazione.

![Screenshot della barra degli strumenti di TraceX.](./media/user-guide/screen_shot_12.png)


**FIGURA 7**

I pulsanti della barra degli strumenti di TraceX, da sinistra a destra, sono definiti come segue:
                                             
| **Button**                         | **Funzione** |
| ---------------------------------- | ----------------------------------------------------------------------------------------------- |
| ![Pulsante Apri file di traccia](./media/user-guide/screen_shot_13.png)      | Aprire un file di traccia |
| ![Pulsante Apri guida utente](./media/user-guide/screen_shot_14.png)      | Aprire questo Manuale dell'utente |
| ![Pulsante Genera profilo di esecuzione](./media/user-guide/screen_shot_15.png)       | Generare il profilo di esecuzione |
| ![ Pulsante Genera statistiche prestazioni](./media/user-guide/screen_shot_16.png)       | Generare statistiche sulle prestazioni |
| ![Pulsante Genera utilizzo stack di thread](./media/user-guide/screen_shot_17.png)       | Generare l'utilizzo dello stack di thread |
| ![Pulsante Visualizza evento selezionato](./media/user-guide/screen_shot_18.png)       | Visualizzare l'evento attualmente selezionato |
| ![Cercare pulsante](./media/user-guide/screen_shot_19.png)      | Cercare eventi |
| ![Pulsante Zoom avanti](./media/user-guide/screen_shot_20.png)      | Eseguire lo zoom avanti. |
| ![Pulsante Visualizza zoom](./media/user-guide/screen_shot_21.png)      | Selezionare la percentuale di zoom dello schermo, dove 100% indica che l'intero file di traccia viene visualizzato all'interno della visualizzazione corrente. |
| ![Pulsante Zoom indietro](./media/user-guide/screen_shot_22.png)      | Eseguire lo zoom indietro. |
| ![Selezionare il primo pulsante dell'evento](./media/user-guide/screen_shot_23.png)      | Selezionare il primo evento. |
| ![Pulsante Visualizza pagina evento precedente](./media/user-guide/screen_shot_24.png)      | Visualizzare la pagina dell'evento precedente. |
| ![Pulsante Visualizza evento precedente](./media/user-guide/screen_shot_25.png)      | Visualizzare l'evento precedente. |
| ![Pulsante di spostamento successivo/precedente](./media/user-guide/screen_shot_26.png)      | Determinare il funzionamento dei pulsanti di spostamento successivo/precedente. Se **l'opzione*** Evento _ è selezionata, la navigazione viene eseguita nell'evento successivo/precedente. Se _*_l'opzione_*_ Contesto è selezionata, la navigazione viene eseguita sull'evento successivo/precedente nel contesto specificato. Se _*_l'opzione_*_ Oggetto è selezionata, la navigazione viene eseguita sull'evento successivo/precedente dell'oggetto specificato. ad esempio eventi associati a una coda specifica. Se _*_l'opzione_*_ Opzioni è selezionata, lo spostamento viene eseguito alla modifica successiva/precedente nel contesto. Se si seleziona _ *_ID_**, la navigazione viene eseguita sull'evento successivo/precedente dell'ID evento specificato. |
| ![Pulsante Visualizza evento successivo](./media/user-guide/screen_shot_27.png)      | Visualizzare l'evento successivo. |
| ![Pulsante Visualizza pagina evento successiva](./media/user-guide/screen_shot_28.png)      | Visualizzare la pagina dell'evento successiva. |
| ![Pulsante Seleziona ultimo evento](./media/user-guide/screen_shot_29.png)      | Selezionare l'ultimo evento. |

## <a name="display-mode-tabs"></a>Schede della modalità di visualizzazione

TraceX visualizza gli eventi di sistema in due modi diversi: *sequenziale e* *relativo all'ora.* La modalità predefinita è sequenziale e questa è la modalità illustrata nella **figura 8.**

La modifica della modalità è semplice come la selezione delle schede ***Visualizzazione** sequenziale _ o _*_Visualizzazione_*_ temporale nella finestra TraceX. _*La figura 8** mostra le schede **_Visualizzazione sequenziale_*_ e _ *_Visualizzazione temporale_** .

![Screenshot delle schede Visualizzazione sequenziale e Visualizzazione temporale.](./media/user-guide/screen_shot_30.png)

**FIGURA 8**

## <a name="sequential-view-mode"></a>Modalità di visualizzazione sequenziale

La modalità di visualizzazione sequenziale viene selezionata dalla scheda ***Visualizzazione sequenziale** _ illustrata nella _*Figura 8**. Si tratta della modalità predefinita. In questa modalità, gli eventi vengono visualizzati im.. /mediamente l'uno dopo l'altro, indipendentemente dal tempo trascorso tra di essi. Si noti anche il righello sopra l'area di visualizzazione **nella figura 8.** Mostra il numero di evento relativo dall'inizio della traccia.

Questa modalità è la modalità predefinita ed è utile per ottenere una buona panoramica di ciò che sta succedendo nel sistema.

## <a name="time-view-mode"></a>Modalità di visualizzazione temporale

La modalità di visualizzazione dell'ora viene selezionata dal pulsante ***Visualizzazione temporale** _ . _ *Figura 9** mostra la stessa traccia eventi della **figura 8,** ad eccezione della modalità di visualizzazione temporale. In questa modalità, gli eventi vengono visualizzati in modo relativo temporale, con la barra verde continua usata per mostrare l'esecuzione tra gli eventi. Questa modalità è utile per vedere dove avviene la maggior parte dell'elaborazione nel sistema, che può aiutare gli sviluppatori a ottimizzare il sistema per migliorare le prestazioni e/o la velocità di risposta.

![Screenshot della scheda Visualizzazione temporale.](./media/user-guide/screen_shot_31.png)

**FIGURA 9**

Si noti anche il righello sopra la visualizzazione dell'evento **nella figura 9.** Questo righello mostra i segni di graduazione relativi dall'inizio della traccia, come derivato dal timestamp instrumentato nella registrazione della traccia eventi all'interno di ThreadX. Se i timestamp sono troppo vicini (timer a bassa frequenza), gli eventi verranno eseguiti insieme. Al contrario, se i timestamp sono troppo distanti (timer a frequenza elevata), gli eventi saranno troppo distanti. La scelta del timestamp di frequenza giusto è una considerazione importante per rendere significativa la visualizzazione relativa all'ora.

## <a name="system-summary-line"></a>Riga di riepilogo del sistema

TraceX fornisce anche una singola riga di riepilogo (il contesto principale nella **figura 10)** che include tutti gli eventi nella stessa riga. In questo modo è facile visualizzare una panoramica di un sistema complesso. La barra di riepilogo è particolarmente utile nei sistemi con molti thread. Senza tale riga di riepilogo, è necessario seguire interazioni di sistema complesse usando la barra di scorrimento verticale per seguire il contesto di esecuzione.

![Screenshot della riga di riepilogo del sistema nella scheda Visualizzazione sequenziale.](./media/user-guide/screen_shot_32.png)


**FIGURA 10**

La riga di riepilogo contiene un riepilogo del contesto e il riepilogo dell'evento corrispondente sottostante. Nell'esempio illustrato **nella figura 10 è** facile vedere che il thread **_2_ _ è in esecuzione *e interrotto. L'interrupt* comporta la preemption di _ _thread 3_**, ***thread 6** _, _*_thread 4_*_ e _*_thread 7_*_, dopo il quale _ *_thread 2_** riprende l'esecuzione.

## <a name="system-contexts"></a>Contesti di sistema

TraceX elenca i contesti di sistema sul lato sinistro della visualizzazione, come illustrato nella **figura 11.** Gli eventi che si verificano in un contesto specifico vengono visualizzati sulla linea orizzontale a destra di tale contesto. In questo modo, è possibile determinare facilmente il contesto in cui si è verificato l'evento e seguire tale riga di contesto per visualizzare tutti gli eventi che si sono verificati in un contesto specifico.

Le prime voci di contesto di traino sono sempre i contesti ***Interrupt** _ e _*_Initialize/Idle._*_ _*_Il contesto_*_ di interrupt rappresenta tutti gli eventi di sistema generati da Interrupt Service Routines (IRS). _*_Il contesto Initialize/Idle_*_ rappresenta due contesti in ThreadX. Gli eventi che si _*_verificano tx_application_define_*_, sono _*_il contesto Initialize/Idle._*_ Se il sistema è inattivo e quindi non si verifica alcun evento, la barra verde che rappresenta _*_In_*_ esecuzione nella visualizzazione temporale viene disegnata nel contesto _ *_Initialize/Idle_**.

![Screenshot dei contesti di sistema sul lato sinistro dello schermo.](./media/user-guide/screen_shot_33.png)

**FIGURA 11**

Nell'esempio nella **Figura 11** sono presenti nove contesti di thread, a partire dal thread del **_timer_*di sistema _ context. Altre informazioni su un singolo contesto sono disponibili posizionando il mouse su tale contesto. Le informazioni aggiuntive includono l'indirizzo dello stack iniziale del thread, l'indirizzo dello stack finale, le dimensioni totali, la percentuale usata, la percentuale di esecuzione relativa, il numero di sospensioni, i ripresi e la priorità più alta e più bassa durante la traccia. _* La figura 12** mostra le informazioni per **_il thread 0._**

![Screenshot delle informazioni per il thread 0.](./media/user-guide/screen_shot_34.png)


**FIGURA 12**

I contesti possono anche essere spostati per raggruppare quelli di maggiore interesse. Questa operazione viene eseguita trascinando e rilasciando il contesto o facendo clic con il pulsante destro del mouse sul contesto. Facendo clic con il pulsante destro del mouse sul contesto viene visualizzata una finestra di dialogo per spostare il contesto nella parte superiore o inferiore. 

Se si seleziona ***Sposta** in alto _ il contesto del _*_thread 3_*_ viene spostato all'inizio dell'elenco dei contesti, come illustrato nella _*Figura 13**.

![Screenshot del contesto spostato all'inizio dell'elenco dei contesti.](./media/user-guide/screen_shot_35.png)


**FIGURA 13**

## <a name="thread-status-information"></a>Informazioni sullo stato del thread

Se abilitata, TraceX visualizza lo stato di ogni thread tramite una linea colorata nel contesto del thread. Una linea verde indica che il thread è in uno stato "pronto", mentre una riga di qualsiasi altro colore indica che il thread è sospeso. Per i thread sospesi, il colore della linea indica il tipo di oggetto ThreadX su cui è sospeso il thread. Ad esempio, nella figura **13** la linea verde nel contesto _ del thread del timer di sistema a partire **_dall'evento_*147 mostra* che _ Thread _timer_ di sistema _ è *pronto. Prima dell'evento 147* e dopo l'evento 154, l'assenza della linea verde indica che _ _Thread timer_ di sistema _ *è pronto. Prima dell'evento 147*** e dopo l'evento 154, l'assenza della linea verde indica che _ Thread timer di sistema è sospeso.

![Screenshot dello stato di ogni thread tramite una linea colorata nel contesto del thread.](./media/user-guide/screen_shot_36.png)

**FIGURA 14**

Sono disponibili tre modalità di visualizzazione dello stato del thread tramite il menu ***Opzioni -> righe di stato** _ . _*_L'opzione Solo_*_ pronto mostra solo le righe di stato pronte (verdi), ma non le righe di stato di sospensione. Si tratta dell'opzione predefinita per TraceX. L'opzione _ *_All On_** consente la visualizzazione di tutte le righe di stato (pronto e sospeso).

Infine, ***l'opzione All Off*** disabilita la visualizzazione di tutte le righe di stato.

## <a name="event-information-display"></a>Visualizzazione delle informazioni sull'evento

TraceX fornisce informazioni dettagliate su circa 600 eventi di run-time, tra cui threadX, FileX, NetX, NetX Duo e chiamate API USBX ed eventi interni. TraceX supporta anche fino a 61.439 eventi univoci definiti dall'utente.

Indipendentemente dal fatto che sia selezionata la modalità di visualizzazione sequenziale o temporale, un passaggio del mouse su qualsiasi evento nell'area di visualizzazione comporta la visualizzazione di informazioni dettagliate sull'evento vicino all'evento. Il passaggio del mouse sull'evento 143 nella dimostrazione ***demo_threadx.trx** _ file di traccia è illustrato nella _*Figura 15**:

![Screenshot del passaggio del mouse sull'evento 143 in un file di traccia di esempio](./media/user-guide/screen_shot_37.png)

**FIGURA 15**

Ogni evento visualizzato contiene informazioni standard su ***Context** _ e su _*_Relative Time e_*_ Time _*_Stamp_*_. Il campo Contesto mostra il contesto in cui si è verificata l'evento. Esistono esattamente quattro contesti: thread, inattività, ISR e inizializzazione. Quando un evento si verifica in un contesto di thread, il nome del thread e la relativa priorità in quel momento vengono raccolti e visualizzati come illustrato in precedenza. _*_L'ora_*_ relativa mostra il numero relativo di tick del timer dall'inizio della traccia. _ *_Timestamp non elaborato_** visualizza l'origine dell'ora non elaborata dell'evento. Infine, vengono visualizzate tutte le informazioni specifiche dell'evento. Queste informazioni sono dettagliate nella parte restante di questo capitolo.

Informazioni dettagliate sull'evento sono disponibili anche facendo doppio clic su qualsiasi evento. Fare doppio clic sull'evento 143 è illustrato nella **figura 16:**

![Screenshot delle informazioni dettagliate sull'evento quando si fa doppio clic su un evento.](./media/user-guide/screen_shot_38.png)

**FIGURA 16**

La possibilità di visualizzare più eventi contemporaneamente offre all'utente una visualizzazione molto più ricca di ciò che è successo. La visualizzazione affiancata è molto utile perché molti eventi sono correlati tra loro. A tale scopo, fare doppio clic su più eventi.

## <a name="current-event-display"></a>Visualizzazione dell'evento corrente

TraceX visualizza l'evento corrente, in una finestra separata, quando viene selezionato dall'utente tramite Visualizza ***-> Evento*** corrente o facendo clic sul pulsante dell'evento corrente sulla barra degli strumenti. Dopo la selezione, TraceX visualizza l'evento attualmente selezionato in una finestra autonoma e la aggiorna ogni volta che viene selezionato un altro evento.

## <a name="event-searching"></a>Ricerca di eventi

TraceX offre una funzionalità di ricerca di eventi completa. L'ID evento e i campi di informazioni di ogni evento sono i parametri di ricerca principali. La non specifica di un valore per un parametro di ricerca indica che il parametro rimuove in modo efficace tale parametro dalla ricerca. Inoltre, la ricerca può essere eseguita in modo che qualsiasi parametro trovato soddisfi la ricerca o che tutti i parametri siano trovati per soddisfare la ricerca. La ricerca può anche essere limitata a un contesto specifico o coprire tutti i contesti nella traccia. Per richiamare la ricerca di eventi, selezionare il pulsante ***Cerca** per valore _ sulla barra degli strumenti, come illustrato nella _figura 17**. Se selezionata, viene visualizzata la finestra di dialogo di ricerca, che specifica tutti i parametri per la ricerca. I pulsanti **_Avanti_*_ _*_e_*_ Indietro nella finestra di dialogo di ricerca possono quindi essere usati per trovare gli eventi successivi e precedenti che corrispondono ai criteri di ricerca specificati. _ *Figura 17** mostra la finestra di dialogo di ricerca.

![Screenshot della ricerca di eventi.](./media/user-guide/screen_shot_39.png)

**FIGURA 17**

![Screenshot della finestra di dialogo di ricerca.](./media/user-guide/screen_shot_40.png)

**FIGURA 18**

## <a name="zooming-in-and-out"></a>Zoom avanti e indietro

Per impostazione predefinita, TraceX visualizza gli eventi con le dimensioni complete. È possibile eseguire lo zoom avanti o indietro in base alle esigenze. Lo zoom indietro è utile per visualizzare gli eventi complessivi acquisiti nella traccia, mentre lo zoom avanti è utile nelle condizioni in cui gli eventi si sovrappongono a causa della risoluzione dell'origine timestamp. **La figura 19** mostra il file **_demo_threadx.trx_** ingrandito in modo da visualizzare il 100% del file di traccia.

![Screenshot di un file di esempio ingrandito in modo da visualizzare il 100% del file di traccia.](./media/user-guide/screen_shot_41.png)

**FIGURA 19**

Quando si esegue lo zoom indietro al 100% per visualizzare l'intera traccia all'interno della pagina di visualizzazione corrente, è facile visualizzare tutte le esecuzioni del contesto acquisite nella traccia, nonché gli eventi generali che si verificano all'interno di tali contesti. Si noti **nella figura 16 che** il thread **_1_ _ e *_*_thread 2_** vengono eseguiti più spesso. La colorazione blu per i relativi eventi suggerisce anche che questi thread effettuano chiamate al servizio di coda (gli eventi della coda sono di colore blu).

Il ripristino in una visualizzazione icona completa è altrettanto semplice; Il pulsante di zoom avanti può essere selezionato ripetutamente o può essere immesso un fattore di 100.

## <a name="delta-ticks-between-events"></a>Tick differenziali tra gli eventi

Determinare il numero di tick tra i vari eventi in TraceX è semplice: fare clic sull'evento iniziale e trascinare il mouse sull'evento finale. Il numero delta di tick tra gli eventi viene visualizzato nell'angolo superiore destro della visualizzazione, come illustrato **nella figura 17.**

![Screenshot del numero differenziale di tick tra gli eventi.](./media/user-guide/screen_shot_42.png)

**FIGURA 17**

I tick differenziali mostrati nella figura **17** mostrano che sono trascorsi 5032 tick tra l'evento 125 e l'evento 154. Questo può anche essere calcolato manualmente esaminando i timestamp relativi in ogni evento e sottraendo, ma l'uso dell'interfaccia utente grafica è semplice e istantaneo.

## <a name="actual-time-display"></a>Visualizzazione dell'ora effettiva

Se abilitata, TraceX visualizza il tempo effettivo in microsecondi in ***Visualizzazione** ora _ e per le varie informazioni sull'ora delta visualizzate da TraceX. Per impostazione predefinita, la visualizzazione dell'ora effettiva è disabilitata. Per abilitare la visualizzazione dell'ora effettiva, è necessario immettere il numero di tick per microsecondo tramite la selezione del menu _ *_Opzioni -> Ticks per Microsecond_** (il valore da immettere è determinato dall'origine timer hardware usata per la registrazione degli eventi TraceX nella destinazione).

## <a name="priority-inversions"></a>Inversioni di priorità

TraceX visualizza automaticamente le inversioni di priorità rilevate nel file di traccia. Le inversioni di priorità sono definite come condizioni in cui un thread con priorità più alta viene bloccato durante il tentativo di ottenere un mutex attualmente di proprietà di un thread con priorità inferiore. Questa condizione è stata specificata *come deterministica* perché il sistema è stato configurato per funzionare in questo modo. Per informare l'utente, TraceX mostra gli *intervalli di* inversione della priorità deterministica come colore chiaro del salmone.

TraceX visualizza anche *le inversioni di* priorità non deterministiche. Queste inversioni di priorità differiscono dalle inversioni di priorità *deterministiche* in quanto un altro thread di un livello di priorità diverso è stato eseguito nel mezzo di quella che era un'inversione di priorità *deterministica,* rendendo così il tempo all'interno dell'inversione di priorità un po' non *deterministica.* Questa condizione è spesso sconosciuta all'utente e può essere molto grave. Per avvisare l'utente di questa condizione, TraceX mostra le inversioni di priorità *non deterministiche* come colore del salmone più chiaro. **La figura 18** illustra le *inversioni di priorità deterministiche* e *non deterministiche.*

![Screenshot dell'inversione della priorità in un file di traccia.](./media/user-guide/screen_shot_43.png)

**FIGURA 18**

**La figura 18** illustra *un'inversione di* priorità deterministica dall'evento 398 all'evento 402. In questo intervallo, il thread * con priorità più alta **0** _ si blocca in un mutex di proprietà di un thread con _*_priorità inferiore 1._*_ All'evento 402 , _ *_thread 1_** rilascia il mutex e termina quindi l'inversione di priorità.

L'area ombreggiata più chiara mostra *un'inversione di* priorità non deterministica tra l'evento 408 e l'evento 420. Ciò che rende questo comportamento *non deterministico* è che, mentre ***thread 1** _ contiene il mutex su cui è bloccato il thread con priorità più alta _*_0,_*_ si verifica un'interruzione che riprende il thread _*_2_**, che quindi esegue e allunga il tempo di inversione della priorità del sistema. Questa condizione può essere piuttosto grave e difficile da identificare. Tuttavia, con TraceX è facilmente identificabile.
