---
title: Descrizione di GUIX Studio
description: Questo capitolo contiene una descrizione dello strumento di analisi del sistema GUIX Studio.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 843106aa67d2a978c7f271954e028b32ba4dd007fe35a36b7c17ba0f5f80e4a9
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116787031"
---
# <a name="chapter-3-description-of-guix-studio"></a>Capitolo 3: Descrizione di GUIX Studio

Questo capitolo contiene una descrizione dello strumento di analisi del sistema GUIX Studio. In questo capitolo è disponibile una descrizione delle funzionalità generali dell'interfaccia utente grafica. 

## <a name="guix-studio-views"></a>Visualizzazioni di GUIX Studio

Esistono cinque aree principali dell'interfaccia utente di GUIX Studio, in cui ***Toolbar** _, _*_Project View_*_, _*_Properties View_*_, Target _*_View_*_ _*_e Visualizzazione risorse_*_. _ *_Figura 2_** mostra l'interfaccia utente di base di GUIX Studio. Ognuna delle visualizzazioni viene discussa ulteriormente nelle sottose sezioni seguenti.

![Screenshot dell'interfaccia utente di base di GUIX Studio.](./media/guix-studio/image_10.png)

**Figura 2**

### <a name="title"></a>Titolo

- GUIX Studio 18: ***Title** _ visualizza la versione di GUIX Studio e il progetto attualmente aperto, come illustrato nella parte superiore di _ *_Figura 2_** in precedenza.

### <a name="toolbar"></a>Barra degli strumenti

La barra **degli strumenti*** mostra i pulsanti disponibili per lo sviluppatore GUIX Studio, come illustrato nella figura _3_**.

![Screenshot della barra degli strumenti di GUIX Studio.](./media/guix-studio/image11.jpg)

**Figura 3**

I pulsanti della barra degli strumenti sono definiti come segue:

![New button](./media/guix-studio/new-button.png) Crea un nuovo progetto GUIX Studio

![Pulsante Apri](./media/guix-studio/open-button.png) Apre un progetto GUIX Studio esistente

![Pulsante Salva](./media/guix-studio/save-button.png) Salva il progetto

![Pulsante Taglia](./media/guix-studio/cut-button.png) Widget Taglia selezionato, inclusi gli elementi figlio

![Pulsante Copia](./media/guix-studio/copy-button.png) Copiare il widget selezionato, inclusi gli elementi figlio

![Pulsante Incolla](./media/guix-studio/paste-button.png) Incollare il widget e gli elementi figlio

![Pulsante allinea a sinistra](./media/guix-studio/left-align-button.png) Allinea a sinistra i widget selezionati

![Pulsante allinea a destra](./media/guix-studio/right-align-button.png) Allinea a destra i widget selezionati

![Pulsante allinea in alto](./media/guix-studio/top-align-button.png) Allinea in alto i widget selezionati

![Pulsante allinea in basso](./media/guix-studio/bottom-align-button.png) Allinea in basso i widget selezionati

![Pulsante Spazi verticalmente](./media/guix-studio/space-vertically-button.png) Spazio uniforme dei widget selezionati verticalmente

![Pulsante Spazi orizzontalmente](./media/guix-studio/space-horizontally-button.png) Spazia uniformemente orizzontalmente i widget selezionati

![Pulsante Larghezza uguale](./media/guix-studio/equal-width-button.png) Rendere uguali i widget selezionati

![Pulsante Altezza uguale](./media/guix-studio/equal-height-button.png) Rendere i widget selezionati uguali all'altezza

![Pulsante Sposta in primo piano](./media/guix-studio/move-front-button.png) Spostare i widget selezionati in primo piano

![Pulsante Sposta indietro](./media/guix-studio/move-back-button.png) Sposta i widget selezionati in avanti

![Pulsante Dimensioni](./media/guix-studio/size-button.png) Ridimensionare il widget selezionato per il contenuto Zoom indietro della schermata di destinazione

![Pulsante Zoom indietro](./media/guix-studio/zoom-out-button.png) Schermata di destinazione zoom indietro

![Pulsante Zoom avanti](./media/guix-studio/zoom-in-button.png) Zoom avanti nella schermata di destinazione

![Pulsante Registra](./media/guix-studio/record-button.png) Registra macro

![Pulsante Di riproduzione](./media/guix-studio/playback-button.png) Macro di riproduzione

![Pulsante Esegui](./media/guix-studio/run-button.png) Eseguire l'applicazione

![Pulsante Informazioni su](./media/guix-studio/about-button.png) Informazioni su GUIX Studio

### <a name="project-view"></a>Project View

Il simbolo ***Project visualizzazione** _ mostra gli oggetti GUIX dell'elenco gerarchico che costituiscono l'interfaccia utente incorporata. È possibile aggiungere nuovi oggetti GUIX facendo clic sull'oggetto padre e quindi selezionando un oggetto dal _*_menu_*_ Inserisci oppure facendo clic con il pulsante destro del mouse sull'oggetto e scegliendo dal menu di scelta rapida. _*_La figura 4_*_ seguente illustra GUIX Studio _*_Project visualizzazione_**.

![Screenshot della visualizzazione Project GUIX Studio.](./media/guix-studio/image_35.png)

**Figura 4**

### <a name="properties-view"></a>Visualizzazione Proprietà

***Properties View** _ visualizza informazioni dettagliate sulle proprietà dell'oggetto GUIX attualmente selezionato, che possono essere selezionate tramite la visualizzazione _*_Project_*_ o facendo clic direttamente sull'oggetto nella Visualizzazione _*_di destinazione._*_ _*_La figura 5_*_ seguente illustra la visualizzazione Proprietà di GUIX Studio __*_**.

![Screenshot della visualizzazione proprietà di GUIX Studio.](./media/guix-studio/image36.jpg)

**Figura 5**

### <a name="target-view"></a>Visualizzazione di destinazione

***Target View** _ è l'area di layout e progettazione dello schermo WYSIWYG. Questa visualizzazione è concepita per rappresentare la visualizzazione fisica o gli schermi disponibili nell'hardware di destinazione. Gli oggetti possono essere selezionati, spostati, ridimensionati e così via tramite semplici operazioni del mouse. Inoltre, le operazioni sui pulsanti allineamento e ordine Z sono disponibili per gli oggetti selezionati nella visualizzazione di destinazione. La selezione di un oggetto nella _*_visualizzazione_*_ di destinazione comporta anche la visualizzazione delle proprietà di tale oggetto nella _*_visualizzazione Proprietà_*_. _*_La figura 6_*_ seguente illustra GUIX Studio _*_Target View_**.

![Screenshot della visualizzazione di destinazione di GUIX Studio.](./media/guix-studio/image_37.png)

**Figura 6**

### <a name="resource-view"></a>Visualizzazione risorse

Il simbolo *** Visualizzazione risorse** _ viene usato per gestire le risorse (colori, tipi di carattere, mappe pixel e stringhe) disponibili per le schermate delle applicazioni definite per ogni visualizzazione. È possibile fare clic sulle intestazioni del gruppo di visualizzazione delle risorse per espandere ogni gruppo ed esaminare il contenuto del gruppo. _*_La figura 7_*_ seguente illustra GUIX Studio _*_Visualizzazione risorse_**.

![Screenshot di GUIX Studio Visualizzazione risorse.](./media/guix-studio/image38.jpg)

**Figura 7**

Il titolo dei gruppi di risorse indica il nome del tema corrente. Se sono disponibili più temi, è possibile passare da un tema all'altro facendo clic sulla freccia su e giù.

Ogni gruppo di risorse nella visualizzazione precedente può essere espanso o compresso facendo clic sull'intestazione del gruppo. Nel capitolo successivo viene fornita una descrizione più dettagliata di ogni gruppo di risorse.

## <a name="the-guix-studio-project"></a>GuiX Studio Project

Un progetto GUIX Studio gestisce informazioni sulla progettazione dello schermo dell'interfaccia utente e sulle risorse dell'interfaccia utente. I dati del progetto vengono salvati in un file di formato XML con estensione ". ***gxp***". Poiché il file di progetto è un file di XML Schema, può essere controllato e condiviso in modo analogo a qualsiasi altro file di origine.

Quando si inizia a usare GUIX Studio per la prima volta, è necessario aprire uno dei progetti di esempio forniti con la distribuzione o creare un nuovo progetto. Tutto il lavoro viene salvato nel file di dati del progetto.

GUIX Studio produce anche file di origine ANSI C. Questi file di origine contengono le risorse dell'applicazione o le strutture di dati che descrivono le schermate progettate. GUIX Studio scrive anche in queste funzioni API dei file di origine generati che sanno di usare le strutture di dati generate per creare dinamicamente le schermate dell'applicazione. Il software dell'applicazione richiama semplicemente le funzioni API fornite per creare le schermate progettate in GUIX Studio.

Durante la progettazione dell'interfaccia utente, è necessario usare periodicamente GUIX Studio per generare i file di output compatibili con GUIX che consentono di compilare ed eseguire l'interfaccia progettata. È possibile compilare ed eseguire i file di origine generati per l'hardware di destinazione o sul desktop Windows che simula ThreadX e GUIX.

## <a name="guix-studio-project-organization"></a>GUIX Studio Project Organization

È utile conoscere l'organizzazione di base di un progetto GUIX Studio per comprendere come usare GUIX Studio in modo efficace e per comprendere le informazioni presentate nella visualizzazione Project dell'IDE di GUIX Studio. La Project è una rappresentazione visiva di riepilogo di tutte le informazioni contenute nel progetto.

Prima di descrivere il progetto, è necessario definire alcuni termini. In primo luogo, si usa il **termine Display** per indicare un dispositivo di visualizzazione fisico. Si tratta più spesso di un dispositivo display LCD, ma potrebbe usare altre tecnologie. Il termine successivo è **Screen**, che indica un oggetto GUIX di primo livello, in genere una finestra GUIX e tutti gli elementi figlio associati. Una schermata è un costrutto software che può essere definito e modificato in fase di esecuzione. Infine, **un tema** è una raccolta di risorse. Un tema include una tabella di definizioni dei colori, definizioni dei tipi di carattere e definizioni di pixelmap progettate per funzionare bene insieme e presentare all'utente finale un aspetto coerente.

Il progetto include innanzitutto un set di informazioni globali, ad esempio il nome del progetto, il numero di schermi supportati, la risoluzione e il formato dei colori di ogni visualizzazione, il numero di lingue supportate, il nome di ogni lingua supportata. Il nome del progetto è il primo nodo visualizzato nella Project visualizzazione.

Il progetto organizza quindi tutte le informazioni necessarie per un massimo di 4 schermi fisici e le schermate e le risorse disponibili per ogni visualizzazione. I nomi visualizzati sono i nodi di livello successivo nell'Project di visualizzazione.

Una funzionalità unica dell'applicazione GUIX Studio è il supporto predefinito per più schermi fisici, ognuno con la propria risoluzione x,y, il formato dei colori, le schermate e le risorse. Anche se la maggior parte delle applicazioni GUIX usa un solo display fisico, questa funzionalità è importante per chi effettua un prodotto che deve supportare più schermi fisici simultanei.

Sotto ogni definizione di visualizzazione sono presenti le finestre o le schermate di primo livello definite per tale visualizzazione. Le definizioni dello schermo possono essere annidate a qualsiasi livello a seconda del numero e dell'annidamento dei widget figlio in ogni schermata.

Questa schermata e l'organizzazione di widget figlio vengono visualizzati in modo grafico nella Project visualizzazione.

A ogni visualizzazione sono associati anche i temi supportati dalla visualizzazione e il contenuto della risorsa che compone ogni tema. Se il progetto include più schermi, si noterà che il Visualizzazione risorse ne modifica il contenuto quando si seleziona una visualizzazione e quindi un'altra. Questo perché il contenuto della risorsa è collegato a ogni visualizzazione. Non solo il formato dei colori può essere diverso, ma le mappe pixel, i colori e i tipi di carattere che si sceglie di usare possono variare da uno schermo fisico a un altro.

Il componente finale gestito dal progetto sono i dati della tabella di stringhe associati a ogni visualizzazione. Poiché i display possono avere risoluzioni x,y molto diverse, i dati stringa vengono mantenuti in modo indipendente per ogni visualizzazione definita nel progetto.
