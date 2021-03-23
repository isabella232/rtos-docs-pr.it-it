---
title: Sistema operativo Azure Real-Time (RTO) GUIX Studio Guida introduttiva
description: Questa guida fornisce una breve introduzione all'utilizzo dell'applicazione Azure RTO GUIX studio, l'ambiente di sviluppo dell'interfaccia utente rapido basato su Microsoft Windows appositamente progettato per la libreria di runtime GUIX di Azure RTO da Microsoft.
author: philmea
ms.author: philmea
ms.date: 7/20/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: eedd53867b56312b53f4e9509136ee856acabfd7
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823015"
---
# <a name="azure-rtos-guix-studio-quick-start-guide"></a>Guida introduttiva di Azure RTO GUIX Studio

Questa guida fornisce una breve introduzione all'uso di Azure RTO GUIX Studio. GUIX studio è un'applicazione di progettazione dell'interfaccia utente basata su Windows progettata per l'uso con la libreria di runtime GUIX di Azure RTO di Microsoft. 

È concepito per lo sviluppatore di software in tempo reale incorporato che usa il sistema operativo ThreadX Real-Time (RTO) e la libreria di runtime dell'interfaccia utente GUIX di Azure RTO. Lo sviluppatore deve avere familiarità con i concetti standard di Azure RTO ThreadX e Azure RTO GUIX.

## <a name="summary"></a>Riepilogo

Azure RTO GUIX Studio include tutto il necessario per creare, compilare ed eseguire la propria progettazione di interfaccia grafica. Se si sta valutando GUIX studio, il kit di valutazione è progettato per consentire di compilare ed eseguire il progetto GUIX come applicazione desktop di Windows autonoma a scopo di test e valutazione. Poiché GUIX è progettato per l'uso in quasi tutte le destinazioni incorporate in grado di produrre output grafico, le operazioni da eseguire e le progettazioni create sul desktop possono essere sempre compilate ed eseguite nella destinazione incorporata senza modificare il software dell'applicazione.
Il programma di installazione di GUIX Studio inserisce diversi componenti nel sistema di sviluppo:

- Applicazione GUIX Studio.
- Diversi progetti di esempio di GUIX.
- Tutte le risorse grafiche e i tipi di carattere usati nei progetti di esempio.
- File di soluzione e file di progetto per la compilazione in un ambiente desktop Windows utilizzando l'IDE di Microsoft Visual Studio.
- Librerie GUIX e ThreadX predefinite per Win32, che consentono di compilare ed eseguire le proprie applicazioni nel computer.
- File di intestazione dell'API GUIX e ThreadX.

## <a name="prerequisites"></a>Prerequisiti

Il programma di installazione di Azure RTO GUIX Studio include diversi semplici progetti di esempio e si prevede di iniziare modificando, compilando ed eseguendo questi esempi quando si apprenderà come usare l'applicazione GUIX Studio. Per compilare ed eseguire gli esempi sul desktop di Windows, è necessario un compilatore Microsoft Visual Studio. Questi strumenti possono essere scaricati dal percorso seguente:

https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs#DownloadFamilies_4

Se non sono installati gli strumenti di sviluppo Microsoft, è comunque possibile avviare i pneumatici e usare l'applicazione GUIX Studio per creare una struttura di interfaccia personalizzata ed esaminare il codice sorgente prodotto. Tuttavia, non sarà possibile compilare ed eseguire la progettazione come applicazione autonoma.

## <a name="running-the-examples"></a>Esecuzione degli esempi

Dopo aver eseguito il programma di installazione di GUIX studio, nel contenuto installato sono inclusi diversi file di progetto e di compilazione di esempio di studio. Per verificare che gli strumenti desktop siano installati e funzionanti correttamente, è consigliabile iniziare compilando ed eseguendo tutti gli esempi forniti così come sono. Si fa riferimento alla directory di installazione come \<root> , nel qual caso è necessario usare il browser file e passare a \<root> /GUIX_Studio_6. x/examples. In questa directory dovrebbero essere visualizzati diversi semplici programmi di esempio, ad esempio demo_guix_calculator, demo_guix_car_infotainment, demo_guix__home_automation, demo_guix_widget_types e altri.

## <a name="building-an-example"></a>Compilazione di un esempio

Dovrebbe essere presente una sottodirectory denominata *Build* all'interno di ogni cartella di esempio. Questa direzione include progetti preconfigurati per ogni programma di produzione supportato. Ad esempio, è possibile passare a \<root> /GUIX_Studio_6. x/examples/termometro/Build/vs_2019 e si troverà un file di soluzione Microsoft Visual Studio preconfigurato e un file di progetto pronto per essere caricato ed eseguito nell'IDE di Visual Studio. Se si desidera utilizzare un altro oggetto, contattare [azure_rtos_support](https://docs.microsoft.com/azure/azure-portal/supportability/how-to-create-azure-support-request#create-a-support-request).

È consigliabile avviare l'IDE Microsoft Visual C++ e aprire almeno uno di questi esempi. Premere il \<F7> tasto per compilare il progetto di esempio e premere il \<F5> tasto per eseguire il programma dopo che è stato compilato correttamente. Verrà ora visualizzata un'interfaccia utente di GUIX in esecuzione in una finestra di Microsoft Windows.

## <a name="designing-and-running-your-own-user-interface"></a>Progettazione ed esecuzione di un'interfaccia utente personalizzata

Questa Guida introduttiva non è una sostituzione del manuale dell'utente di GUIX Studio o del manuale dell'utente di GUIX, ma verrà illustrato un numero sufficiente per iniziare e si consiglia di continuare facendo riferimento al manuale dell'utente di GUIX Studio per informazioni più dettagliate.

Esistono due metodi per la creazione e la modifica dell'interfaccia utente. È possibile studiare il manuale di programmazione della libreria GUIX e usare l'API GUIX direttamente dall'interno del software dell'applicazione per implementare completamente il progetto. Più spesso, si userà l'applicazione GUIX Studio per eseguire la maggior parte delle operazioni di progettazione e layout degli elementi dello schermo, quindi completare la gestione degli eventi e la logica dell'applicazione necessaria per far funzionare l'interfaccia utente.

Ognuno degli esempi forniti è stato creato con l'applicazione di progettazione dell'interfaccia GUIX Studio. È necessario disporre di un'icona sul desktop per GUIX Studio 6. x.x. x dopo aver eseguito il programma di installazione di GUIX Studio.  Avviare GUIX Studio ora e aprire il progetto denominato "demo_guix_widget_types \ guix_widget_types. GXP". La demo *widget_types* è un progetto di esempio che illustra diverse varianti dei tipi di widget GUIX più comuni.

Ora che è aperto un progetto, fare clic su "+" per aprire il nodo della struttura ad albero denominato "Primary" nella visualizzazione progetto nell'angolo superiore sinistro dell'IDE e fare clic sulla finestra di primo livello all'interno di questa cartella denominata "Menu_Screen". Il progetto non deve apparire come illustrato di seguito:

![Screenshot di studio con progetto aperto.](./media/guix-studio/qs_project_open.png)

## <a name="guix-studio-views"></a>Viste di GUIX Studio

L'IDE di GUIX studio è costituito da diverse ***visualizzazioni***. Ogni visualizzazione è progettata per facilitare l'esplorazione della progettazione e apportare modifiche a tale progettazione.

### <a name="project-view"></a>Project View

La visualizzazione in alto a sinistra è denominata visualizzazione progetto. Questa visualizzazione Mostra ogni visualizzazione fisica inclusa nel progetto (la maggior parte dei progetti dispone di una sola visualizzazione) e le schermate e i widget figlio progettati per l'esecuzione in tale visualizzazione.

### <a name="properties-view"></a>Visualizzazione proprietà

Sotto la visualizzazione del progetto è presente la visualizzazione delle proprietà. Come implica la visualizzazione delle proprietà del nome, questa visualizzazione consente di modificare i widget modificando varie proprietà associate.

### <a name="target-view"></a>Visualizzazione di destinazione

L'area di visualizzazione centrale viene chiamata visualizzazione di destinazione. Questa visualizzazione è una visualizzazione WYSIWYG dell'interfaccia utente. Poiché la libreria GUIX viene disegnata nella visualizzazione di destinazione, questa visualizzazione è una rappresentazione con precisione in pixel della modalità di visualizzazione della progettazione durante l'esecuzione nella destinazione incorporata. Se si fa clic su widget diversi nella visualizzazione del progetto o nella vista di destinazione centrale, i valori visualizzati nella visualizzazione delle proprietà cambiano per visualizzare le proprietà del widget selezionato.

### <a name="resource-view"></a>Visualizzazione risorse

Infine, a destra, verrà visualizzato il nome Visualizzazione risorse. Questa visualizzazione consente di selezionare, aggiungere, eliminare e modificare i colori, i tipi di carattere, pixelmaps e le stringhe inclusi nel progetto.

## <a name="modifying-the-example"></a>Modifica dell'esempio

GUIX studio è progettato per essere intuitivo. Per spostare uno dei widget indicati in precedenza, è sufficiente fare clic su tale widget nella visualizzazione di destinazione e trascinarlo in una nuova posizione. Per modificare i colori dei widget, fare clic sul widget desiderato e modificare i colori visualizzati nella visualizzazione delle proprietà. Per modificare il tipo di carattere usato da un widget di visualizzazione del testo, è sufficiente fare clic sul tipo di carattere desiderato all'interno del Visualizzazione risorse e trascinare il tipo di carattere sul widget di destinazione desiderato. Galleggiare il mouse lungo i pulsanti della barra degli strumenti per visualizzare la Guida rapida relativa all'operazione eseguita da ciascun pulsante.

Sperimentare manualmente e apportare alcune piccole modifiche all'esempio. Ad esempio, è possibile trascinare un widget in una nuova posizione, modificare il colore di sfondo di una finestra o ridimensionare un pulsante. Non è consigliabile eliminare alcun widget dall'esempio fino a quando non si acquisisce maggiore esperienza nell'uso di GUIX, poiché l'eliminazione dei widget potrebbe richiedere modifiche associate al codice sorgente dell'applicazione.

## <a name="running-the-application-within-studio"></a>Esecuzione dell'applicazione in studio

È possibile utilizzare la modifica | Eseguire il comando di menu dell'applicazione (o eseguire il pulsante applica sulla barra dei pulsanti) per eseguire l'applicazione immediatamente all'interno di una nuova finestra del desktop. Le funzioni di disegno personalizzate e il codice dell'applicazione non verranno richiamati utilizzando questo metodo, ma consentono di spostarsi rapidamente nella progettazione dell'interfaccia utente e di ottenere un'idea complessiva dell'aspetto dell'applicazione, inclusa la navigazione da una schermata a quella successiva.

## <a name="generating-source-files"></a>Generazione di file di origine

Dopo aver apportato le modifiche, è necessario richiamare i comandi di menu di GUIX Studio per generare nuovi file di origine per il progetto. È quindi possibile ricompilare il programma di esempio per visualizzare le modifiche in azione. Per generare file di origine, usare il progetto comandi di menu di GUIX Studio | Generare file di risorse e progetto | Genera file di specifica (è anche possibile fare clic con il pulsante destro del mouse sulla visualizzazione nella visualizzazione del progetto per eseguire questi comandi).

Quando si generano i nuovi file di origine, è necessario osservare un messaggio di conferma che informa che i file di origine associati al progetto sono stati aggiornati. Se non si osserva questo messaggio di conferma, verificare di disporre delle autorizzazioni di scrittura per la directory in cui risiede il progetto. È ora possibile chiudere l'applicazione GUIX Studio. Se sono state apportate modifiche al progetto, GUIX Studio chiederà se si desidera salvare le modifiche. Procedere e salvare le modifiche. questi esempi sono progettati per l'uso e la sperimentazione con l'apprendimento dell'uso di GUIX Studio.

### <a name="building-and-running-the-application"></a>Compilazione ed esecuzione dell'applicazione

Ora che GUIX studio ha generato i file di output del progetto, è possibile compilare e creare un collegamento per creare un eseguibile Win32 autonomo. Inoltre, per incorporare un disegno personalizzato o la gestione degli eventi definiti nell'applicazione, è necessario compilare e collegare i file di output generati da GUIX studio con il software dell'applicazione. Come esempio, verrà usato il Microsoft Visual C++ la gestione dei componenti, ma viene usata esattamente la stessa procedura se si compila e si esegue per la destinazione desiderata.

- Avviare l'IDE MSVC e aprire la soluzione \<root> /GUIX_Studio_5. x/examples/demo_guix_widget_types/build/vs_2019/guix_widget_types. sln.

- Usare la \<F7> chiave per ricompilare la soluzione.
- Usare la \<F5> chiave per eseguire il programma.
 
A questo punto dovrebbe essere visualizzato il programma in esecuzione, con le modifiche apportate all'interno di studio.

### <a name="learning-more"></a>Altre informazioni

La **Guida per l'utente di GUIX Studio** è disponibile in [azrtos-GUIX-Studio-User-Guide](https://docs.microsoft.com/azure/rtos/guix/about-guix-studio). La guida per l'utente di GUIX studio è una guida molto più completa all'uso di GUIX Studio.

Inoltre, la **Guida dell'utente di GUIX** è disponibile in [azrtos-GUIX-user-guide](https://docs.microsoft.com/azure/rtos/guix/about-guix).  Questa guida offre informazioni molto più dettagliate su ciò che accade "dietro le quinte" quando viene eseguita l'applicazione GUIX. È necessario fare riferimento a entrambe le guide per sfruttare completamente le funzionalità della libreria di runtime GUIX e di GUIX Studio.

## <a name="customer-support-center"></a>Centro assistenza clienti

Inviare un ticket di supporto tramite il portale di Azure per domande o assistenza seguendo questa procedura. Fornire le informazioni riportate di seguito in un messaggio di posta elettronica per risolvere in modo più efficiente la richiesta di supporto:

- Descrizione dettagliata del problema, inclusa la frequenza di occorrenza e il modo in cui può essere riprodotta in modo affidabile.
- Alleghi il file di traccia che causa il problema.
- La versione di Azure RTO GUIX studio in uso (visualizzata nella parte superiore sinistra dello schermo).
- La versione di Azure RTO GUIX in uso che include la variabile **_gx_version_idstring** e **_gx_build_options** .
