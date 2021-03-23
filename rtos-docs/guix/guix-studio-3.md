---
title: Descrizione di GUIX Studio
description: Questo capitolo contiene una descrizione dello strumento di analisi del sistema di GUIX Studio.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 89bbcd51c22dddef6e420750e8c8805a66344335
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822274"
---
# <a name="chapter-3-description-of-guix-studio"></a>Capitolo 3: Descrizione di GUIX Studio

Questo capitolo contiene una descrizione dello strumento di analisi del sistema di GUIX Studio. In questo capitolo è stata rilevata una descrizione della funzionalità complessiva della GUI. 

## <a name="guix-studio-views"></a>Viste di GUIX Studio

Sono disponibili cinque aree principali dell'interfaccia utente di GUIX studio, vale a dire la ***barra degli strumenti** _, la _*_visualizzazione del progetto_*_, la _*_visualizzazione delle proprietà_*_, la _*_visualizzazione di destinazione_*_ e _*_visualizzazione risorse_*_. _ *_Figura 2_** Mostra l'interfaccia utente di base di GUIX Studio. Ognuna delle viste viene descritta ulteriormente nelle sezioni secondarie seguenti.

![Screenshot dell'interfaccia utente di base di GUIX Studio.](./media/guix-studio/image_10.png)

**Figura 2**

### <a name="title"></a>Titolo

- GUIX studio 18: il ***titolo** _ Visualizza la versione di GUIX studio e il progetto attualmente aperto, come illustrato nella parte superiore di _ *_Figura 2_** in precedenza.

### <a name="toolbar"></a>Barra degli strumenti

La ***barra degli strumenti** _ Mostra i pulsanti disponibili per lo sviluppatore di GUIX studio, come illustrato nella _Figura 3_* *.

![Screenshot della barra degli strumenti di GUIX Studio.](./media/guix-studio/image11.jpg)

**Figura 3**

I pulsanti della barra degli strumenti sono definiti come segue:

![New button](./media/guix-studio/new-button.png) Consente di creare un nuovo progetto GUIX Studio

![Pulsante Apri](./media/guix-studio/open-button.png) Apre un progetto GUIX Studio esistente

![Pulsante per il salvataggio](./media/guix-studio/save-button.png) Salva il progetto

![Pulsante Taglia](./media/guix-studio/cut-button.png) Taglia widget selezionato, inclusi gli elementi figlio

![Pulsante Copia](./media/guix-studio/copy-button.png) Copia il widget selezionato, inclusi gli elementi figlio

![Pulsante Incolla](./media/guix-studio/paste-button.png) Incollare widget e elementi figlio

![Pulsante Allinea a sinistra](./media/guix-studio/left-align-button.png) Allinea a sinistra i widget selezionati

![Pulsante Allinea a destra](./media/guix-studio/right-align-button.png) Allinea a destra i widget selezionati

![Pulsante Allinea in alto](./media/guix-studio/top-align-button.png) Allinea in alto i widget selezionati

![Pulsante Allinea in basso](./media/guix-studio/bottom-align-button.png) Allinea in basso i widget selezionati

![Pulsante spazio verticale](./media/guix-studio/space-vertically-button.png) Ugualmente lo spazio di widget selezionati verticalmente

![Pulsante spazio orizzontale](./media/guix-studio/space-horizontally-button.png) Widget selezionati nello stesso spazio orizzontalmente

![Pulsante uguale larghezza](./media/guix-studio/equal-width-button.png) Rendi uguali i widget selezionati

![Pulsante uguale altezza](./media/guix-studio/equal-height-button.png) Fare in modo che il widget selezionato sia uguale all'altezza

![Pulsante Sposta in primo piano](./media/guix-studio/move-front-button.png) Sposta i widget selezionati in primo piano

![Pulsante Sposta indietro](./media/guix-studio/move-back-button.png) Sposta indietro i widget selezionati

![Pulsante dimensioni](./media/guix-studio/size-button.png) Ridimensiona la schermata di destinazione dello zoom indietro del widget selezionato per il contenuto

![Pulsante Zoom indietro](./media/guix-studio/zoom-out-button.png) Schermata di destinazione dello zoom indietro

![Pulsante zoom avanti](./media/guix-studio/zoom-in-button.png) Zoom nella schermata di destinazione

![Pulsante Registra](./media/guix-studio/record-button.png) Registra macro

![Pulsante riproduzione](./media/guix-studio/playback-button.png) Macro di riproduzione

![Pulsante Esegui](./media/guix-studio/run-button.png) Esegui applicazione

![Pulsante informazioni](./media/guix-studio/about-button.png) Informazioni su GUIX Studio

### <a name="project-view"></a>Project View

La ***visualizzazione progetto** _ Mostra gli oggetti elenco gerarchico GUIX che comprendono l'interfaccia utente incorporata. È possibile aggiungere nuovi oggetti GUIX facendo clic sull'oggetto padre, quindi selezionando un oggetto dal menu _*_Inserisci_*_ oppure facendo clic con il pulsante destro del mouse sull'oggetto e scegliendo dal menu di scelta rapida. _*_Nella figura 4_*_ riportata di seguito viene illustrata la _visualizzazione del progetto_ GUIX Studio _ * * *.

![Screenshot della visualizzazione del progetto GUIX Studio.](./media/guix-studio/image_35.png)

**Figura 4**

### <a name="properties-view"></a>Visualizzazione proprietà

La ***visualizzazione Proprietà _ Mostra** informazioni dettagliate sulle proprietà dell'oggetto GUIX attualmente selezionato, che può essere selezionato tramite la _*_visualizzazione del progetto_*_ o facendo clic direttamente sull'oggetto nella _*_visualizzazione di destinazione_*_. _*_Nella figura 5_*_ riportata di seguito viene illustrata la _visualizzazione delle proprietà_ di GUIX Studio _ * * *.

![Screenshot della visualizzazione delle proprietà di GUIX Studio.](./media/guix-studio/image36.jpg)

**Figura 5**

### <a name="target-view"></a>Visualizzazione di destinazione

La ***visualizzazione di destinazione** _ è la progettazione della schermata WYSIWYG e l'area di layout. Questa visualizzazione è destinata a rappresentare lo schermo fisico o le visualizzazioni disponibili nell'hardware di destinazione. Gli oggetti possono essere selezionati, spostati, ridimensionati e così via tramite semplici operazioni del mouse. Inoltre, le operazioni di allineamento e di ordinamento Z sono disponibili per gli oggetti selezionati nella visualizzazione di destinazione. La selezione di un oggetto nella _*_visualizzazione di destinazione_*_ comporterà anche la visualizzazione delle proprietà di tale oggetto nella _*_visualizzazione delle proprietà_*_. _*_Nella figura 6_*_ riportata di seguito viene illustrata la _visualizzazione di destinazione_ GUIX Studio _ * * *.

![Screenshot della visualizzazione di destinazione di GUIX Studio.](./media/guix-studio/image_37.png)

**Figura 6**

### <a name="resource-view"></a>Visualizzazione risorse

***Visualizzazione risorse** _ viene usato per gestire le risorse (colori, tipi di carattere, pixelmaps e stringhe) disponibili per le schermate delle applicazioni definite per ogni visualizzazione. È possibile fare clic sulle intestazioni del gruppo Visualizzazione risorse per espandere ogni gruppo ed esaminare il contenuto del gruppo. La _*_Figura 7_*_ seguente mostra GUIX Studio _ *_visualizzazione risorse_* *.

![Screenshot di GUIX Studio Visualizzazione risorse.](./media/guix-studio/image38.jpg)

**Figura 7**

Il titolo dei gruppi di risorse indica il nome del tema corrente. Se sono disponibili più temi, è possibile spostarsi tra i temi facendo clic sulla freccia su e giù.

Ogni gruppo di risorse nella vista precedente può essere espanso o compresso facendo clic sull'intestazione di gruppo. Una descrizione più dettagliata di ogni gruppo di risorse segue il capitolo successivo.

## <a name="the-guix-studio-project"></a>Progetto GUIX Studio

Un progetto di GUIX Studio mantiene le informazioni sulla progettazione della schermata dell'interfaccia utente e sulle risorse dell'interfaccia utente. I dati del progetto vengono salvati in un file di formato XML con estensione ". ***GXP***". Poiché il file di progetto è un file di XML Schema, è possibile controllarne la versione e condividerlo in modo analogo a qualsiasi altro file di origine.

Quando si inizia a usare GUIX Studio per la prima volta, sarà necessario aprire uno dei progetti di esempio forniti con la distribuzione o creare un nuovo progetto. Tutto il lavoro viene salvato nel file di dati del progetto.

GUIX studio produce anche file di origine ANSI C. Questi file di origine contengono le risorse dell'applicazione o le strutture dei dati che descrivono le schermate progettate. GUIX Studio scrive anche in queste funzioni API dei file di origine generate che sanno di usare le strutture di dati generate per creare dinamicamente le schermate delle applicazioni. Il software dell'applicazione richiamerà semplicemente le funzioni API fornite per creare le schermate progettate all'interno di GUIX Studio.

Con l'avanzamento della progettazione dell'interfaccia utente, si userà periodicamente GUIX Studio per generare i file di output compatibili con GUIX che consentono di compilare ed eseguire l'interfaccia progettata. È possibile compilare ed eseguire i file di origine generati per l'hardware di destinazione o sul desktop di Windows che simula ThreadX e GUIX.

## <a name="guix-studio-project-organization"></a>Organizzazione del progetto GUIX Studio

È utile avere una certa conoscenza dell'organizzazione di base di un progetto di GUIX Studio per comprendere come usare GUIX studio in modo efficace e per comprendere le informazioni presentate nella visualizzazione del progetto dell'IDE di GUIX Studio. La visualizzazione del progetto è una rappresentazione visiva di riepilogo di tutte le informazioni contenute nel progetto.

Prima di descrivere il progetto, è necessario definire alcuni termini. In primo luogo, viene usato il termine **display** per indicare un dispositivo di visualizzazione fisico. Si tratta in genere di un dispositivo di visualizzazione LCD, ma potrebbe usare altre tecnologie. Il termine successivo è **Screen**, che significa un oggetto GUIX di primo livello, in genere una finestra GUIX e tutti gli elementi figlio associati. Una schermata è un costrutto software che può essere definito e modificato in fase di esecuzione. Infine, un **tema** è una raccolta di risorse. Un tema include una tabella delle definizioni dei colori, le definizioni dei tipi di carattere e le definizioni Pixelmap progettate per funzionare in modo corretto e presentare all'utente finale un aspetto coerente.

Il progetto include innanzitutto un set di informazioni globali, ad esempio il nome del progetto, il numero di visualizzazioni supportate, il formato di risoluzione e colore di ogni visualizzazione, il numero di lingue supportate, il nome di ogni lingua supportata. Il nome del progetto è il primo nodo visualizzato nella visualizzazione del progetto.

Il progetto successivamente organizza tutte le informazioni necessarie per un massimo di 4 visualizzazioni fisiche e le schermate e le risorse disponibili per ogni visualizzazione. I nomi visualizzati sono i nodi di livello successivo nell'albero di visualizzazione del progetto.

Una funzionalità univoca dell'applicazione GUIX studio è il supporto predefinito per più schermi fisici, ognuno con una propria risoluzione x, y, formato colori, schermate e risorse. Sebbene la maggior parte delle applicazioni GUIX utilizzi un solo display fisico, questa funzionalità è importante per coloro che rendono un prodotto che deve supportare più visualizzazioni fisiche simultanee.

Sotto ogni definizione di visualizzazione sono presenti le finestre o le schermate di primo livello definite per la visualizzazione. Le definizioni dello schermo possono essere annidate a qualsiasi livello, a seconda del numero e dell'annidamento dei widget figlio in ogni schermata.

Questa schermata e l'organizzazione dei widget figlio vengono visualizzate in modo grafico nella visualizzazione del progetto.

Inoltre, associato a ogni visualizzazione sono i temi supportati dalla visualizzazione e il contenuto delle risorse che compongono ogni tema. Se il progetto include più visualizzazioni, si noterà che il Visualizzazione risorse ne modifica il contenuto quando si seleziona una visualizzazione e poi un'altra. Questo perché il contenuto della risorsa è collegato a ogni visualizzazione. Non solo il formato dei colori può essere diverso, ma il pixelmaps, i colori e i tipi di carattere che si sceglie di usare possono variare da uno schermo fisico a un altro.

Il componente finale gestito dal progetto è il dati della tabella di stringhe associato a ogni visualizzazione. Poiché le visualizzazioni possono essere di una risoluzione x, y molto diversa, i dati di stringa vengono mantenuti in modo indipendente per ogni visualizzazione definita nel progetto.
