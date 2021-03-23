---
title: Progettazione schermata di GUIX Studio
description: La progettazione delle schermate delle applicazioni è lo scopo principale di GUIX Studio.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 318e68ab5ab7d841057d65565dfda263597d03e4
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822235"
---
# <a name="chapter-5-guix-studio-screen-designer"></a>Capitolo 5: Progettazione schermata di GUIX Studio

La progettazione delle schermate delle applicazioni è lo scopo principale di GUIX Studio. La progettazione dello schermo viene eseguita con tutte le varie visualizzazioni descritte in precedenza nel capitolo 3. Tuttavia, l'elemento principale della progettazione dello schermo in GUIX studio è la ***visualizzazione di destinazione***, ovvero la posizione in cui tutti gli elementi dello schermo sono visualizzati visivamente e esattamente allo stesso modo in cui verranno visualizzati nella visualizzazione di destinazione incorporata. Questi elementi della schermata possono essere selezionati, spostati, ridimensionati e così via tramite semplici operazioni del mouse e dei pulsanti. Inoltre, gli oggetti selezionati sono disponibili per le operazioni relative all'allineamento e al pulsante dell'ordine Z. Le sottosezioni seguenti descrivono diverse funzionalità della progettazione della schermata di GUIX Studio. 

## <a name="creatingconfiguring-projects"></a>Creazione/configurazione di progetti

La creazione di progetti in GUIX studio è semplice: è sufficiente selezionare il pulsante ***nuovo progetto** _ o il progetto selezione menu _*_, nuovo progetto_*_. GUIX studio presenta quindi la finestra di dialogo _ *_Configura progetto_**. Da questa finestra di dialogo vengono specificate le impostazioni di base di visualizzazione, nonché le informazioni sul percorso in cui si trova il codice generato da GUIX Studio.

Quando viene creato un nuovo progetto, viene visualizzata la finestra di dialogo Configura progetto. Questo è il punto in cui lo sviluppatore specifica il numero di visualizzazioni hardware disponibili nella destinazione e le proprietà visualizzate in ogni visualizzazione. Le proprietà includono il nome logico, la risoluzione x/y, la profondità e il formato dei colori e altre proprietà di visualizzazione. GUIX Studio supporta più visualizzazioni nello stesso progetto. Se sono necessarie altre visualizzazioni, è necessario modificare il campo ***Number of Displays** _ in modo che corrisponda al numero di visualizzazioni nel dispositivo incorporato. Il numero massimo di visualizzazioni in un progetto è 4. _ *_Figura 21_** Mostra la finestra di dialogo Configura progetto.

Per modificare il progetto e/o le impostazioni di visualizzazione, è possibile usare l'opzione di menu ***configure, Project/display** _ oppure selezionando il progetto o la visualizzazione, facendo clic con il pulsante destro del mouse e scegliendo _*_Configura, progetto/visualizzazione_*_. In entrambi i casi, viene visualizzata la finestra di dialogo _ *_Configura progetto_** che semplifica le modifiche apportate alle impostazioni e/o alle visualizzazioni del progetto.

![Screenshot della finestra di dialogo Configura progetto.](./media/guix-studio/config_project.png)

**Figura 21**

Il gruppo Directory è il punto in cui è possibile specificare le directory di output predefinite per i file di origine e di intestazione C prodotti da studio. Queste directory vengono in genere salvate in relazione al percorso del progetto per facilitare lo spostamento dei progetti da un computer a un altro o da un file System a un altro.

Il campo intestazioni aggiuntive è il punto in cui è possibile specificare file di intestazione personalizzati. Se è necessario più di un file di intestazione, utilizzare un punto e virgola per delimitare l'elenco.

Quando si richiamano i comandi "genera applicazione" o "genera risorse" di studio, queste sono le directory predefinite in cui verranno scritti i file di origine. Naturalmente, è possibile eseguire l'override di questi percorsi di directory in qualsiasi momento immettendo nuove posizioni nella finestra di dialogo Directory di output.

## <a name="selecting-widgets"></a>Selezione di widget

La selezione dei widget viene eseguita facendo clic sul widget nell'albero del widget ***visualizzazione progetto** _ oppure facendo clic sul widget visibile nell'area di _*_visualizzazione destinazione_*_ . Quando si seleziona un singolo widget, le relative proprietà vengono visualizzate nell'area di _*_visualizzazione delle proprietà_*_ . _*_Nella figura 22_*_ è indicato il widget "_ *_Button_* *" selezionato.

![Screenshot del widget selezionato.](./media/guix-studio/select_button.png)

**Figura 22**

## <a name="using-properties"></a>Utilizzo delle proprietà

Come indicato in precedenza, le proprietà di un widget selezionato vengono visualizzate nella **visualizzazione delle proprietà***. Tutti i widget hanno un insieme comune di proprietà, oltre ad alcune proprietà specifiche del tipo di widget specifico. Un widget Button, ad esempio, ha una proprietà _ *_pushed_** mentre un widget della finestra non lo è. Di seguito è riportato il set comune di proprietà widget:

| Proprietà         | Significato                                                                               |
| ---------------- | ------------------------------------------------------------------------------------- |
| Tipo di widget    | Tipo di widget, per riferimento                                                                               |
| Nome widget      | Nome del widget, passato alla funzione di creazione widget e usato per la denominazione delle variabili nei file di origine generati.               |
| ID widget        | ID del widget. Questo valore ID viene usato per generare segnali dai widget figlio nelle schermate padre.                            |
| Sinistra             | Coordinata più a sinistra del widget                                                                                                 |
| Inizio              | Coordinata superiore del widget                                                                                                  |
| Larghezza            | Larghezza del widget in pixel                                                                                                      |
| Altezza           | Altezza del widget in pixel                                                                                                     |
| Bordo           | Tipo di bordo del widget                                                                                                          |
| Modalità trasparente      | Controllare se il widget è parzialmente trasparente                                                                       |
| Estrai selezionato    | Verificare che il widget venga inizialmente disegnato nello stato selezionato.                                            |
| Abilita           | Controllare se il widget può essere selezionato o scelto dall'utente finale.                                                    |
| Accetta lo stato attivo    | Controllare se il widget accetta lo stato attivo.                                                                                 |
| Allocazione Runtime | Controllare se il blocco di controllo widget deve essere allocato dinamicamente.                                                 |
| Riempimento normale      | ID risorsa colore riempimento normale                                                                                                  |
| Riempimento selezionato    | ID risorsa colore riempimento selezionato                                                                                                |
| Funzione di progetto    | Nome della funzione di disegno personalizzata definita dall'utente. Se questo campo è vuoto, viene utilizzata la funzione di disegno standard per quel tipo di widget. |
| Funzione Event   | Nome della funzione di gestione degli eventi personalizzata definita dall'utente. Se vuota, viene utilizzata la gestione degli eventi standard per questo tipo di widget.          |

La ***Figura 23*** Mostra le proprietà di un semplice widget di finestra.

![Screenshot delle proprietà di un semplice widget della finestra.](./media/guix-studio/image57.jpg)

**Figura 23**

Molti tipi di widget hanno proprietà aggiuntive specifiche per ogni tipo di widget.

Nella figura 23 precedente, ad esempio, il tipo di widget Window supporta un ID Pixelmap di sfondo e un'impostazione di stile che indica se lo sfondo deve essere centrato o affiancato.

I widget di testo supportano un campo ID stringa, insieme agli stili di allineamento del testo e una specifica del tipo di carattere. Le proprietà del widget aggiuntive sono in genere molto intuitive dopo aver letto la descrizione di ogni tipo di widget e gli stili disponibili e creare i parametri della funzione per quel tipo di widget.

## <a name="manipulating-widgets"></a>Manipolazione di widget

Per modificare un widget, è necessario innanzitutto selezionarlo. Questa operazione viene eseguita facendo clic direttamente sul widget nella **visualizzazione * destinazione** _ oppure selezionandola nell'albero dei widget _ *_visualizzazione progetto_**. Una volta selezionato, il widget avrà un contorno tratteggiato. In questo stato, è possibile spostarlo semplicemente facendo clic sul widget e trascinandolo nella posizione desiderata nell'elemento padre. Se il widget è un widget di primo livello, il trascinamento del widget sta impostando in modo efficace la posizione iniziale del widget sulla visualizzazione di destinazione. Naturalmente, è sempre possibile spostare o ridimensionare qualsiasi widget in qualsiasi momento usando l'API GUIX.

Per ridimensionare l'altezza del widget, posizionare il mouse sul bordo superiore del widget e attendere che il puntatore del mouse venga modificato in una freccia verso il basso. A questo punto è possibile modificare l'altezza del widget semplicemente spostando il mouse mentre viene premuto il pulsante destro del mouse. La larghezza del mouse può essere ridimensionata in modo simile posizionando il puntatore del mouse sul bordo sinistro del widget. ***Figura 24** _ Mostra il widget "_ *_Button_* *" ridimensionato e spostato nell'area sinistra/superiore della finestra padre.

![Screenshot del widget dei pulsanti.](./media/guix-studio/resize_button.png)

**Figura 24**

## <a name="manipulating-multiple-widgets"></a>Manipolazione di più widget

La selezione di più widget viene eseguita facendo clic su più widget nella visualizzazione di destinazione tenendo premuto il tasto ***CTRL*** . Questa operazione indicherà ogni widget selezionato con un contorno tratteggiato. Si noti che quando si selezionano più widget ogni widget del gruppo di selezione deve essere figlio dello stesso elemento padre.

Dopo aver selezionato più widget, è possibile spostarli simultaneamente facendo clic all'interno di uno dei widget selezionati e spostando il mouse con il pulsante destro del mouse. Inoltre, per allineare il gruppo di widget selezionati, è possibile usare i pulsanti di allineamento della **barra degli strumenti**. La _*_Figura 25_*_ Mostra i widget "_*_Button_*_" e "_*_New Button_*_" selezionati e la _*_Figura 26_*_ Mostra il risultato della selezione del pulsante _ *_align-left_** mentre questi widget sono selezionati.

![Screenshot dei widget Button e New Button selezionati](./media/guix-studio/multiple_select.png)

**Figura 25**

![Screenshot del risultato della selezione del pulsante Align-Left.](./media/guix-studio/align_left.png)

**Figura 26**

## <a name="cutcopypaste-operations"></a>Operazioni Taglia/copia/incolla

Un widget selezionato nella visualizzazione di **destinazione*** può essere tagliato, copiato e incollato in modalità standard. I widget e le schermate possono essere copiati all'interno di un progetto o copiati da un progetto e incollati in un altro progetto. La _*_barra degli strumenti_*_ contiene pulsanti per taglia, copia e incolla. Sono inoltre disponibili le stesse opzioni nell'opzione di menu Modifica. Si noti che quando si incolla un widget, è necessario selezionare il widget padre prima di incollare il nuovo widget. La _*_Figura 27_*_ Mostra il risultato della selezione del widget "_ *_Button_* *", della copia e della copia nella stessa finestra.

![Screenshot delle operazioni Taglia/copia/incolla.](./media/guix-studio/copy_paste_button.png)

**Figura 27**

La copia e incolla all'interno di un progetto è in genere semplice perché le risorse che potrebbero essere richieste dai widget copiati sono sempre presenti quando si lavora all'interno di un progetto. Tuttavia, se si copia un widget da Project A e lo si incolla in Project B, possono verificarsi problemi con le dipendenze delle risorse.

Quando si copiano i widget in studio, l'applicazione Studio crea un elenco delle risorse richieste dai widget copiati e genera una tabella di dipendenza delle risorse portabile nel formato XML, che viene copiato negli Appunti di Windows, insieme alle informazioni effettive del widget copiato. Quando si incollano i widget in un progetto diverso, studio esamina prima di tutto l'elenco di dipendenze delle risorse e aggiunge le risorse necessarie al progetto aperto, se non esistono già. Studio identifica le risorse corrispondenti in base ai nomi degli ID di risorsa e per le risorse di stringa studio confronta anche il contenuto della stringa. Se vengono trovate risorse corrispondenti, Studio aggiorna gli ID risorsa dei widget incollati per usare correttamente le risorse nel nuovo progetto. Se le risorse non vengono trovate, verranno aggiunte.

Quando Studio aggiunge una risorsa al progetto come parte di un'operazione Incolla widget, in studio viene effettivamente aggiunto un collegamento alla risorsa nel caso di risorse del tipo di carattere e di Pixelmap. Questo collegamento viene generato dal progetto di origine e verranno visualizzati messaggi di avviso se non è possibile trovare tali risorse relative al percorso del progetto in cui si sta incollando. I collegamenti alle risorse verranno aggiunti al progetto indipendentemente, ma potrebbe essere necessario copiare manualmente i tipi di carattere e i file di immagine nei percorsi appropriati nel nuovo albero del progetto per eliminare gli errori di caricamento delle risorse. Studio non copia i file. ttf,. png o. jpg da un percorso a un altro.

Il modo più semplice per evitare problemi in questo senso consiste nel tenere una struttura di directory coerente tra i progetti che si desidera condividere. Se si desidera spostare facilmente gli elementi dal progetto A al progetto B, è possibile lasciare le immagini grafiche e i tipi di carattere utilizzati da entrambi i progetti in una sottodirectory coerente di ogni cartella del progetto.

## <a name="changing-z-order"></a>Modifica dell'ordine Z

È possibile spostare facilmente i widget davanti o dietro altri widget. Questa operazione viene eseguita selezionando il widget e selezionando i pulsanti ***Sposta in primo piano** o _*_Sposta a indietro_*_ sulla _*_barra degli strumenti_*_. _ *_Figure 28_** Mostra lo spostato del secondo pulsante sullo sfondo.

![Screenshot del pulsante z-order.](./media/guix-studio/change_z_order.png)

**Figura 28**

## <a name="assigning-colors-fonts-and-pixelmaps"></a>Assegnazione di colori, tipi di carattere e pixelmaps

Oltre a selezionare i colori, i tipi di carattere e pixelmaps nella visualizzazione proprietà per un widget selezionato, è supportato anche un metodo di trascinamento della selezione a sintassi abbreviata per l'assegnazione di risorse ai widget. Per usare questa funzionalità, è sufficiente fare clic su una risorsa, ad esempio un colore del tipo di carattere nella visualizzazione risorse, e trascinare la risorsa sul widget desiderato nella visualizzazione di destinazione. Rilasciare la risorsa rilasciando il pulsante sinistro del mouse sul widget.

Quando si usa il metodo di trascinamento della selezione, le risorse di colore vengono sempre assegnate al colore di sfondo normale del widget. Con la visualizzazione proprietà è necessario assegnare altri colori, ad esempio il colore selezionato o il colore del testo selezionato.

Analogamente, le risorse Pixelmap vengono assegnate al campo Pixelmap "normale" o "riempimento" di un widget che supporta la visualizzazione di Pixelmap. Per assegnare altri campi a un widget che supporta più pixelmaps, è necessario usare la visualizzazione delle proprietà.

## <a name="using-templates"></a>Uso di modelli

Qualsiasi schermata o raccolta di widget figlio progettati in studio può essere usata come modello per nuove schermate e nuovi controlli figlio. L'uso di un modello è simile alla copia e incolla di un widget, ad eccezione di qualsiasi elemento derivato da un modello che viene modificato automaticamente quando il modello su cui si basa è stato modificato. Non è consentito modificare le proprietà del widget modello quando si utilizza una schermata derivata o un'istanza ereditata del modello. Tuttavia, quando si modificano le proprietà del modello in qualsiasi modo, tutte le istanze che fanno riferimento a tale modello vengono aggiornate automaticamente, poiché sono derivate da tale modello.

Un altro vantaggio derivante dall'utilizzo di modelli per gli elementi ripetuti è che le dimensioni del file delle specifiche generate in studio in genere risulteranno inferiori rispetto a quando si ricreano gli elementi ripetuti ogni volta che vengono utilizzati.

Per indicare che una schermata o una raccolta di widget figlio deve essere usata come modello, è possibile attivare la casella di controllo "template" nella visualizzazione delle proprietà del widget. Una volta accesa la casella di controllo "template" (modello), il widget del modello verrà visualizzato nell'istruzione ***Insert |*** Menu a discesa modello/i.

Come esempio di utilizzo di un modello, è possibile definire una finestra utilizzata come barra dei pulsanti. Questa finestra può contenere diversi pulsanti figlio e questa barra del pulsante viene usata di frequente in varie schermate. È possibile definire una piccola finestra autonoma all'interno del progetto studio che include i pulsanti figlio obbligatori e assegnare a questa finestra il nome "button_bar". Selezionare quindi questa finestra e attivare la proprietà "template". Selezionare quindi una schermata su cui si desidera aggiungere la barra dei pulsanti. Usare l'istruzione INSERT | Template | button_bar comando di menu per inserire un'istanza della finestra di button_bar sullo schermo. Si noti che è possibile riposizionare la barra dei pulsanti, ma non è consentito modificare la maggior parte delle proprietà. Tuttavia, è possibile usare il widget button_bar (e qualsiasi elemento figlio) come qualsiasi altro tipo di widget GUIX predefinito. Per modificare il button_bar, è necessario selezionare il modello button_bar per apportare le modifiche.

Un altro esempio di utilizzo tipico di un modello è costituito da un'applicazione che include molte schermate simili. Ad esempio, l'applicazione potrebbe avere 10 schermate diverse che condividono la barra del titolo comune, il colore di riempimento, le dimensioni e così via. In questo caso, è possibile definire una schermata modello che includa i widget figlio della barra del titolo e configurare le dimensioni dello schermo, il colore di riempimento e altre proprietà. Una volta definita questa schermata modello, è possibile derivare le 10 schermate diverse da questo modello. Quando si usa l'istruzione INSERT | Modello | \<base_screen> il comando di menu, lo schermo inizierà con tutti i widget figlio e le impostazioni della schermata del modello. Si noti che ogni schermata derivata dalla schermata modello non è una copia del modello, ma è effettivamente un'istanza derivata della schermata modello. È quindi possibile personalizzare ogni schermata derivata in modo che contenga tutti i contenuti aggiuntivi richiesti.

Si noti che oltre a salvare le dimensioni del file delle specifiche generate, l'uso dei modelli può semplificare la gestione delle modifiche apportate all'aspetto dell'applicazione. Nell'esempio precedente, si supponga che sia necessario modificare il colore di sfondo delle 10 schermate simili. Anziché essere necessari per selezionare ogni schermata e modificare le impostazioni del colore di riempimento, è sufficiente selezionare il modello di base e modificarne il colore di riempimento. questa modifica verrà immediatamente riflessa in tutte le schermate derivate.

Un ulteriore commento relativo ai modelli: è necessario assicurarsi che il flusso di elaborazione degli eventi venga mantenuto, vale a dire che se si specifica un gestore eventi per una schermata di base (per la gestione degli eventi del widget comune) e per una schermata derivata, il gestore eventi della schermata derivata deve chiamare il gestore eventi base_screen nel caso predefinito. Questo consentirà al gestore eventi della schermata di base di elaborare gli eventi generati dai widget comuni a tutte le schermate derivate da questo modello di base.

## <a name="record-and-playback-macro"></a>Macro di record e riproduzione

Le funzioni di record e riproduzione macro consentono di registrare e riprodurre le sequenze di tasti e gli eventi del mouse.

La registrazione in un file di macro viene eseguita selezionando il pulsante della barra degli strumenti ***Registra macro** _ oppure il menu selezionando _*_modifica, Registra macro_*_. GUIX Studio Visualizza la finestra di dialogo _*_Registra macro_*_ che consente di specificare il percorso per il file di macro. Dopo aver selezionato questa opzione, fare clic sul pulsante _*_registra_*_ per avviare la registrazione. Al termine della registrazione, selezionare di nuovo il pulsante della barra degli strumenti di _*_registrazione macro_*_ oppure utilizzare il menu a discesa selezionando _ *_modifica, fine macro_** per terminare la registrazione delle macro.

La riproduzione di un file di macro viene eseguita selezionando il pulsante della barra degli strumenti ***macro di riproduzione** usando il menu a discesa principale per selezionare il comando _*_modifica, riproduzione macro_*_ . GUIX studio presenta la finestra di dialogo _ *_riproduzione macro_** che consente di specificare il file di macro registrato in precedenza da eseguire.

Quando si registrano macro che scelgono file di input o di output, ad esempio l'aggiunta di un tipo di carattere o di un'immagine, è importante usare la tastiera per digitare il nome del file, anziché usare il mouse per selezionare dal browser file. Poiché il registratore di macro registra gli eventi del mouse e della tastiera e, poiché il browser del file può cambiare nel tempo, è più affidabile digitare il nome file anziché selezionare il file graficamente.

## <a name="zooming-target-view"></a>Visualizzazione di destinazione zoom

La funzione zoom avanti consente di ottenere una visualizzazione di chiusura della schermata di destinazione.

È possibile scegliere l'impostazione di zoom percentuale desiderata in ***Configure | Visualizzazione di destinazione |** Opzione di menu Zoom _. La *_barra degli strumenti_* _ * include anche pulsanti per lo zoom avanti e indietro.

## <a name="gridsnap-settings"></a>Impostazioni griglia/blocca

La finestra di dialogo ***Impostazioni griglia e snap** contiene alcune impostazioni e opzioni per griglia e snap. _*_Nella Figura 29_*_ viene visualizzata la finestra _*_di dialogo Impostazioni griglia e di allineamento_*_ quando il menu _ *_Configura | Visualizzazione di destinazione | Grid/snap_** è selezionato.

![Screenshot delle impostazioni della griglia e dello snap.](./media/guix-studio/image63.jpg)

**Figura 29**

Attiva ***Mostra griglia** _ Visualizza griglia nella schermata destinazione. è possibile specificare l'incremento della griglia (in pixel) nel campo _*_Spaziatura griglia_*_ . L'opzione _ *_Blocca sulla griglia_** consente di ottenere la posizione corretta di un widget. l'attivazione di questa opzione attiverà gli snap attivi.

Quando è abilitata l'opzione ***griglia e blocca*** :

- Se si trascina un oggetto con il mouse nella visualizzazione di destinazione, l'oggetto verrà spostato in base all'incremento della griglia.
- Se si trascina il bordo di un oggetto per ridimensionare, il bordo trascinato potrebbe bloccarsi sulla posizione della griglia.
- Se si seleziona un oggetto e si usano i tasti freccia su/sinistra/giù/destra, il widget selezionato verrà spostato in base all'incremento dello snap, sarà possibile specificare l'incremento dello snap (in pixel) nel campo ***spaziatura*** .
