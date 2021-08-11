---
title: GuiX Studio del sistema operativo Real-Time (RTOS) di Azure Guida introduttiva
description: Questa guida offre una breve introduzione all'uso dell'applicazione GUIX Studio di Azure RTOS, l'ambiente di sviluppo rapido dell'interfaccia utente basato su Microsoft Windows appositamente progettato per la libreria di runtime GUIX di Azure RTOS di Microsoft.
author: philmea
ms.author: philmea
ms.date: 7/20/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 9ab4dfb2edd8990692ee3dc134207f43e4c757538dbc738f6f406bf40864bfb3
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785422"
---
# <a name="azure-rtos-guix-studio-quick-start-guide"></a>Azure RTOS GUIX Studio Guida introduttiva

Questa guida offre una breve introduzione all'uso di Azure RTOS GUIX Studio. GUIX Studio è un'Windows di progettazione dell'interfaccia utente basata Azure RTOS di Microsoft. 

È destinato allo sviluppatore di software in tempo reale incorporato usando il sistema operativo ThreadX Real-Time (RTOS) e la libreria di runtime dell'interfaccia utente GUIX di Azure RTOS. Lo sviluppatore deve avere familiarità con i concetti standard Azure RTOS ThreadX e Azure RTOS GUIX.

## <a name="summary"></a>Riepilogo

Azure RTOS GUIX Studio include tutto il necessario per creare, compilare ed eseguire una progettazione di interfaccia grafica personalizzata. Se si sta valutando GUIX Studio, il kit di valutazione è progettato per consentire di compilare ed eseguire la progettazione GUIX come applicazione desktop Windows autonoma a scopo di test e valutazione. Poiché GUIX è progettato per l'uso in quasi qualsiasi destinazione incorporata in grado di eseguire l'output grafico, le operazioni eseguite e le progettazioni create sul desktop possono sempre essere compilate ed eseguite nella destinazione incorporata senza modificare il software dell'applicazione.
Il programma di installazione di GUIX Studio inserisce diversi componenti nel sistema di sviluppo:

- Applicazione GUIX Studio.
- Diversi progetti di esempio GUIX.
- Tutte le risorse grafiche e i tipi di carattere usati nei progetti di esempio.
- File di soluzione e file di progetto per la compilazione in un ambiente desktop Windows usando l Microsoft Visual Studio IDE.
- Librerie GUIX e ThreadX predefinite per Win32, che consentono di compilare ed eseguire applicazioni personalizzate nel PC.
- File di intestazione dell'API GUIX e ThreadX.

## <a name="prerequisites"></a>Prerequisiti

Il Azure RTOS del programma di installazione di GUIX Studio include diversi semplici progetti di esempio e si prevede di iniziare modificando, compilando ed eseguendo questi esempi mentre si apprenderà come usare l'applicazione GUIX Studio. Per compilare ed eseguire gli esempi sul desktop Windows, è necessario un Microsoft Visual Studio di compilazione. Questi strumenti possono essere scaricati dal percorso seguente:

https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs#DownloadFamilies_4

Se gli strumenti di sviluppo Microsoft non sono installati, è comunque possibile usare l'applicazione GUIX Studio per creare una progettazione personalizzata dell'interfaccia ed esaminare il codice sorgente prodotto. Non sarà tuttavia possibile compilare ed eseguire la progettazione come applicazione autonoma.

## <a name="running-the-examples"></a>Esecuzione degli esempi

Dopo aver eseguito il programma di installazione di GUIX Studio, nel contenuto installato sono inclusi diversi file di progetto e di compilazione di Studio di esempio. Per verificare che gli strumenti desktop siano installati e funzionino correttamente, è consigliabile iniziare compilando ed eseguendo ognuno degli esempi forniti così com'è. Si farà riferimento alla directory di installazione come , nel qual caso è necessario usare il browser di file e passare a \<root> \<root> /GUIX_Studio_6.x/examples. All'interno di questa directory dovrebbero essere visualizzati diversi semplici programmi di esempio, ad esempio demo_guix_calculator, demo_guix_car_infotainment, demo_guix__home_automation, demo_guix_widget_types e altri.

## <a name="building-an-example"></a>Compilazione di un esempio

È necessario trovare una sottodirectory denominata *build all'interno* di ogni cartella di esempio. Questa direzione include progetti preconfigurato per ogni toolchain supportato. Ad esempio, è possibile passare a /GUIX_Studio_6.x/examples/thermometer/build/vs_2019 ed è possibile trovare un file di soluzione Microsoft Visual Studio preconfigurato e un file di progetto pronti per essere caricati ed eseguiti \<root> nell'IDE Visual Studio. Se si vuole usare una toolchain diversa, contattare [azure_rtos_support](https://docs.microsoft.com/azure/azure-portal/supportability/how-to-create-azure-support-request#create-a-support-request).

È consigliabile avviare l'ide Microsoft Visual C++ e aprire almeno uno di questi esempi. Premere il tasto per compilare il progetto di esempio e premere il tasto per eseguire il programma dopo \<F7> \<F5> la corretta compilazione. Verrà ora visualizzata un'interfaccia utente GUIX in esecuzione all'interno di una finestra Windows Microsoft.

## <a name="designing-and-running-your-own-user-interface"></a>Progettazione ed esecuzione di applicazioni Interfaccia utente

Questa guida introduttiva non è una sostituzione della Guida utente di GUIX Studio o della Guida dell'utente guiX, ma verrà illustrato un numero sufficiente per iniziare e consigliare di continuare facendo riferimento alla Guida per l'utente di GUIX Studio per informazioni più dettagliate.

Esistono due metodi per creare e modificare la propria interfaccia utente. È possibile studiare il manuale di programmazione della libreria GUIX e usare l'API GUIX direttamente dal software dell'applicazione per implementare completamente la progettazione. Più spesso si userà l'applicazione GUIX Studio per eseguire la maggior parte del lavoro di progettazione e layout degli elementi dello schermo e quindi si completerà la gestione degli eventi e altre logica dell'applicazione necessarie per rendere l'interfaccia utente realmente utile.

Ognuno degli esempi forniti è stato creato usando l'applicazione di progettazione dell'interfaccia GUIX Studio. Dopo aver eseguito il programma di installazione di GUIX Studio, sul desktop dovrebbe essere visualizzata un'icona per GUIX Studio 6.x.x.x.  Avviare GUIX Studio ora e aprire il progetto denominato "demo_guix_widget_types\guix_widget_types.gxp". La *widget_types* demo è un progetto di esempio che illustra diverse varianti dei tipi di widget GUIX più comuni.

Dopo aver aperto un progetto, fare clic su "+" per aprire il nodo della struttura ad albero denominato "Primary" nella visualizzazione Project nell'angolo superiore sinistro dell'IDE e fare clic sulla finestra di primo livello all'interno di questa cartella denominata "Menu_Screen". Il progetto non dovrebbe essere visualizzato come illustrato di seguito:

![Screenshot di Studio con il progetto aperto.](./media/guix-studio/qs_project_open.png)

## <a name="guix-studio-views"></a>Visualizzazioni di GUIX Studio

L'IDE di GUIX Studio è costituito da diverse ***visualizzazioni***. Ogni visualizzazione è progettata per facilitare l'esplorazione della progettazione e apportare modifiche a tale progettazione.

### <a name="project-view"></a>Project View

La visualizzazione in alto a sinistra è denominata Project visualizzazione. Questa visualizzazione mostra ognuno degli schermi fisici inclusi nel progetto (la maggior parte dei progetti ha una sola visualizzazione) e le schermate e i widget figlio progettati per l'esecuzione in tale visualizzazione.

### <a name="properties-view"></a>Visualizzazione Proprietà

Sotto la Project è disponibile la visualizzazione Proprietà. Come suggerisce il nome Visualizzazione proprietà, questa vista consente di modificare i widget modificando varie proprietà associate.

### <a name="target-view"></a>Visualizzazione di destinazione

L'area di visualizzazione centrale è denominata Visualizzazione di destinazione. Questa visualizzazione è una visualizzazione WYSIWYG dell'interfaccia utente. Poiché la libreria GUIX disegna all'interno della visualizzazione di destinazione, questa visualizzazione è una rappresentazione accurata dei pixel dell'aspetto della progettazione durante l'esecuzione nella destinazione incorporata. Se si fa clic su widget diversi nella visualizzazione Project o nella visualizzazione di destinazione centrale, i valori visualizzati nella visualizzazione Proprietà cambiano per visualizzare le proprietà del widget selezionato.

### <a name="resource-view"></a>Visualizzazione risorse

Infine, a destra si può vedere ciò che viene chiamato Visualizzazione risorse. Questa visualizzazione consente di selezionare, aggiungere, eliminare e modificare colori, tipi di carattere, pixelmap e stringhe inclusi nel progetto.

## <a name="modifying-the-example"></a>Modifica dell'esempio

GUIX Studio è progettato per essere intuitivo. Per spostare uno dei widget mostrati in precedenza, è sufficiente fare clic sul widget nella visualizzazione di destinazione e trascinarlo in una nuova posizione. Per modificare i colori del widget, fare clic sul widget desiderato e modificare i colori visualizzati nella visualizzazione Proprietà. Per modificare il tipo di carattere usato da un widget di visualizzazione del testo, è sufficiente fare clic sul tipo di carattere desiderato all'interno del Visualizzazione risorse e trascinare il tipo di carattere nel widget di destinazione desiderato. Spostare il mouse lungo i pulsanti della barra degli strumenti per visualizzare informazioni rapide sull'operazione eseguita da ogni pulsante.

Sperimentare e apportare alcune modifiche secondarie all'esempio. Ad esempio, è possibile trascinare un widget in una nuova posizione, modificare il colore di sfondo di una finestra o ridimensionare un pulsante. Non è consigliabile eliminare i widget dall'esempio fino a quando non si acquisisce maggiore esperienza nell'uso di GUIX perché l'eliminazione dei widget potrebbe richiedere modifiche associate al codice sorgente dell'applicazione.

## <a name="running-the-application-within-studio"></a>Esecuzione dell'applicazione all'interno di Studio

È possibile usare il comando | Eseguire il comando di menu Applicazione (o il pulsante Esegui applicazione sulla barra dei pulsanti) per eseguire l'applicazione immediatamente all'interno di una nuova finestra del desktop. Le funzioni di disegno personalizzate e altro codice dell'applicazione non verranno richiamate usando questo metodo, ma consentono di esplorare rapidamente la progettazione dell'interfaccia utente e ottenere un'idea generale dell'aspetto dell'applicazione, inclusa la navigazione da una schermata a quella successiva.

## <a name="generating-source-files"></a>Generazione di file di origine

Dopo aver apportato le modifiche, è necessario richiamare i comandi di menu di GUIX Studio per generare nuovi file di origine per il progetto. È quindi possibile ricompilare il programma di esempio per visualizzare le modifiche in azione. Per generare i file di origine, usare i comandi di menu di GUIX Studio Project| Generare file di risorse e Project| Genera file di specifica (è anche possibile fare clic con il pulsante destro del mouse sulla visualizzazione nella Project per eseguire questi comandi).

Quando si generano questi nuovi file di origine, è necessario osservare un messaggio di conferma che informa che i file di origine associati al progetto sono stati aggiornati. Se non si osserva questo messaggio di conferma, verificare di disporre delle autorizzazioni di scrittura per la directory in cui si trova il progetto. È ora possibile chiudere l'applicazione GUIX Studio. Se sono state apportate modifiche al progetto, GUIX Studio chiederà se si desidera salvare tali modifiche. Procedere e salvare le modifiche. Questi esempi sono destinati all'uso e all'sperimentazione durante l'apprendimento dell'uso di GUIX Studio.

### <a name="building-and-running-the-application"></a>Compilazione ed esecuzione dell'applicazione

Ora che GUIX Studio ha generato i file di output del progetto, è possibile compilare e collegare per creare un eseguibile Win32 autonomo. Inoltre, per incorporare qualsiasi disegno personalizzato o gestione degli eventi definita nell'applicazione, è necessario compilare e collegare i file di output generati da GUIX Studio con il proprio software applicativo. Verrà usata la toolchain Microsoft Visual C++ come esempio, ma viene usata esattamente la stessa procedura se si sta compilando ed eseguendo per la destinazione prevista.

- Avviare l MSVC IDE e aprire la soluzione \<root> /GUIX_Studio_5.x/examples/demo_guix_widget_types/build/vs_2019/guix_widget_types.sln.

- Usare la \<F7> chiave per ricompilare la soluzione.
- Usare la \<F5> chiave per eseguire il programma.
 
Verrà ora visualizzato il programma in esecuzione, con le modifiche apportate all'interno di Studio.

### <a name="learning-more"></a>Altre informazioni

La **Guida dell'utente di GUIX Studio** è disponibile in [azrtos-guix-studio-user-guide](https://docs.microsoft.com/azure/rtos/guix/about-guix-studio). La Guida dell'utente di GUIX Studio è una guida molto più approfondita all'uso di GUIX Studio.

Inoltre, la **Guida utente GUIX** è disponibile in [azrtos-guix-user-guide](https://docs.microsoft.com/azure/rtos/guix/about-guix).  Questa guida offre informazioni molto più dettagliate su ciò che accade "Under the Hood" quando viene eseguita l'applicazione GUIX. È necessario fare riferimento a entrambe queste guide per sfruttare appieno le funzionalità della libreria di runtime GUIX e di GUIX Studio.

## <a name="customer-support-center"></a>Centro supporto clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza usando la procedura qui. Fornire le informazioni seguenti in un messaggio di posta elettronica per risolvere in modo più efficiente la richiesta di supporto:

- Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e il modo in cui può essere riprodotto in modo affidabile.
- Allegare il file di traccia che causa il problema.
- La versione di Azure RTOS GUIX Studio in uso (visualizzata in alto a sinistra dello schermo).
- La versione di Azure RTOS GUIX in uso, incluse le variabili _gx_version_idstring **e _gx_build_options.** 
