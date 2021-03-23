---
title: Progetto di esempio semplice
description: Questo capitolo descrive come creare un progetto di esempio in GUIX studio ed eseguire l'esempio in GUIX.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 3661396f097e0ed7bd872fae01a7bec9212001b9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822331"
---
# <a name="chapter-10-example-project"></a><span data-ttu-id="6f351-103">Capitolo 10: progetto di esempio</span><span class="sxs-lookup"><span data-stu-id="6f351-103">Chapter 10: Example Project</span></span>

<span data-ttu-id="6f351-104">Questo capitolo descrive come creare un progetto di esempio in GUIX studio ed eseguire l'esempio in GUIX.</span><span class="sxs-lookup"><span data-stu-id="6f351-104">This chapter describes how to create an example project in GUIX Studio and execute the example on GUIX.</span></span>

## <a name="create-new-project"></a><span data-ttu-id="6f351-105">Creare un nuovo progetto</span><span class="sxs-lookup"><span data-stu-id="6f351-105">Create New Project</span></span>

<span data-ttu-id="6f351-106">Il primo passaggio consiste nel creare un nuovo progetto e configurare le visualizzazioni e le lingue supportate dal progetto.</span><span class="sxs-lookup"><span data-stu-id="6f351-106">The first step is creating a new project and configuring the displays and languages that the project will support.</span></span> <span data-ttu-id="6f351-107">Quando si avvia GUIX Studio per la prima volta, viene visualizzata la schermata ***progetti recenti*** :</span><span class="sxs-lookup"><span data-stu-id="6f351-107">When you first start GUIX Studio, you will see the ***Recent Projects*** screen:</span></span>

![Screenshot della finestra di dialogo progetti recenti di GUIX Studio.](./media/guix-studio/recent_projects.png)

<span data-ttu-id="6f351-109">**Figura 10,1**</span><span class="sxs-lookup"><span data-stu-id="6f351-109">**Figure 10.1**</span></span>

<span data-ttu-id="6f351-110">Fare clic sul pulsante \***Crea nuovo progetto** _...</span><span class="sxs-lookup"><span data-stu-id="6f351-110">Click on the \***Create New Project** _…</span></span> <span data-ttu-id="6f351-111">pulsante per avviare un nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="6f351-111">button to begin a new project.</span></span> <span data-ttu-id="6f351-112">Verrà visualizzata la finestra di dialogo _ \*_nuovo progetto GUIX_\*\*, mostrata di seguito:</span><span class="sxs-lookup"><span data-stu-id="6f351-112">You will be presented with the _ *_New GUIX Project_*\* dialog, shown here:</span></span>

![Screenshot della finestra di dialogo Crea nuovo progetto di GUIX Studio.](./media/guix-studio/create_new_project.png)

<span data-ttu-id="6f351-114">**Figura 10,2**</span><span class="sxs-lookup"><span data-stu-id="6f351-114">**Figure 10.2**</span></span>

<span data-ttu-id="6f351-115">Digitare il nome "***new_example***" come nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="6f351-115">Type the name "***new_example***" as the project name.</span></span> <span data-ttu-id="6f351-116">I nomi dei progetti devono usare le regole di denominazione delle variabili C standard, ovvero non caratteri speciali o riservati.</span><span class="sxs-lookup"><span data-stu-id="6f351-116">Project names should use standard C variable naming rules, that is, no special or reserved characters.</span></span> <span data-ttu-id="6f351-117">Digitare il percorso della posizione in cui salvare il progetto.</span><span class="sxs-lookup"><span data-stu-id="6f351-117">Type the path to the location where the project should be saved.</span></span> <span data-ttu-id="6f351-118">Il percorso deve essere una directory file system valida, ovvero GUIX Studio non creerà la directory se non esiste.</span><span class="sxs-lookup"><span data-stu-id="6f351-118">The path must be a valid file system directory, that is, GUIX Studio will not create the directory if it does not exist.</span></span> <span data-ttu-id="6f351-119">Fare clic su "OK" per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="6f351-119">Click "OK" to create the project.</span></span>

<span data-ttu-id="6f351-120">La schermata successiva mostra la schermata di configurazione del progetto, mostrata di seguito:</span><span class="sxs-lookup"><span data-stu-id="6f351-120">The next screen shown is the Project Configuration screen, shown here:</span></span>

![Screenshot della finestra di dialogo Configura progetto di GUIX Studio.](./media/guix-studio/config_new_project.png)

<span data-ttu-id="6f351-122">**Figura 10,3**</span><span class="sxs-lookup"><span data-stu-id="6f351-122">**Figure 10.3**</span></span>

<span data-ttu-id="6f351-123">Questa finestra di dialogo consente di specificare il numero di visualizzazioni che saranno supportate dal progetto e assegnare un nome a ogni visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="6f351-123">This dialog allows you to specify how many displays your project will support, and give a name to each display.</span></span> <span data-ttu-id="6f351-124">È necessario specificare il formato di colore supportato da ogni visualizzazione e, facoltativamente, digitare un percorso per i file di output generati da studio per ogni visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="6f351-124">You must specify the color format supported by each display, and optionally type a pathname for the output files generated by Studio for each display.</span></span> <span data-ttu-id="6f351-125">La directory predefinita per i file di output è ***" \\ .***", ovvero i file di output C vengono scritti nella stessa directory del progetto stesso.</span><span class="sxs-lookup"><span data-stu-id="6f351-125">The default directory for the output files is "***.\\***", meaning the C output files are written to the same directory as the project itself.</span></span>

<span data-ttu-id="6f351-126">Per questo esempio, lasciare il segno ***Number of Displays** _ impostato su "1", digitare il nome "_*_main_display_*_" nel campo Display Name e selezionare "_*_allocate Canvas Memory_\*_".</span><span class="sxs-lookup"><span data-stu-id="6f351-126">For this example, leave the ***Number of Displays** _ set to "1", type the name "_*_main_display_*_" in the display name field, and check "_*_allocate canvas memory_\*_".</span></span> <span data-ttu-id="6f351-127">Lasciare i valori predefiniti per la risoluzione, il formato di colore e i campi directory, quindi fare clic su _ *_OK_* \*.</span><span class="sxs-lookup"><span data-stu-id="6f351-127">Leave the resolution, color format, and directory fields at their default values, and click _\*_OK_\*\*.</span></span>

<span data-ttu-id="6f351-128">A questo punto si noterà che il progetto è aperto con l'IDE di studio, come illustrato nella figura 10,4:</span><span class="sxs-lookup"><span data-stu-id="6f351-128">You should now see your project open with the Studio IDE, as shown in figure 10.4:</span></span>

![Screenshot di un progetto aperto con l'IDE di studio.](./media/guix-studio/initial_screen.png)

<span data-ttu-id="6f351-130">**Figura 10,4**</span><span class="sxs-lookup"><span data-stu-id="6f351-130">**Figure 10.4**</span></span>

<span data-ttu-id="6f351-131">Quando si crea un nuovo progetto, GUIX Studio crea automaticamente una finestra predefinita come punto di partenza per il progetto.</span><span class="sxs-lookup"><span data-stu-id="6f351-131">When you create a new project, GUIX Studio automatically creates a default window as the starting point for your project.</span></span> <span data-ttu-id="6f351-132">Questa casella grigia è la finestra predefinita creata per l'utente, centrata all'interno della *visualizzazione di destinazione*.</span><span class="sxs-lookup"><span data-stu-id="6f351-132">This gray box is the default window created for you, centered within the *Target View*.</span></span>

<span data-ttu-id="6f351-133">Se questa finestra non è selezionata, fare clic sulla finestra in modo da disegnare la casella di selezione tratteggiata intorno alla finestra.</span><span class="sxs-lookup"><span data-stu-id="6f351-133">If this window is not selected, click on the window so that the dashed selection box is drawn around the window.</span></span> <span data-ttu-id="6f351-134">A questo punto, nella \**visualizzazione delle proprietà\*\*\*, modificare il nome del _*_widget_*_, l' _*_ID widget_*_, _*_Left_*_, _*_Top_*_, _*_Width_*_, _*_Height_*_ e _ *_Border_** in modo che corrispondano alle impostazioni indicate di seguito.</span><span class="sxs-lookup"><span data-stu-id="6f351-134">Now in the ***Properties View** _, change the _*_Widget Name_*_, _*_Widget Id_*_, _*_Left_*_, _*_Top_*_, _*_Width_*_, _*_Height_*_, and _ *_Border_** to match those settings shown below.</span></span> <span data-ttu-id="6f351-135">Quando si apportano queste modifiche, le modifiche verranno applicate immediatamente all'interno della visualizzazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6f351-135">As you make these changes, you should see your changes immediately taking effect within the Target View.</span></span>

![Screenshot della finestra di dialogo Visualizzazione proprietà.](./media/guix-studio/initial_window_properties.png)

<span data-ttu-id="6f351-137">**Figura 10,5**</span><span class="sxs-lookup"><span data-stu-id="6f351-137">**Figure 10.5**</span></span>

<span data-ttu-id="6f351-138">Si aggiungerà quindi una risorsa Pixelmap da usare all'interno di un widget \***GX_ICON** _.</span><span class="sxs-lookup"><span data-stu-id="6f351-138">Next we will add a pixelmap resource to be used within a \***GX_ICON** _ widget.</span></span> <span data-ttu-id="6f351-139">Con la distribuzione di GUIX studio sono disponibili diverse icone che funzioneranno correttamente per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="6f351-139">Several icons are provided with your GUIX Studio distribution that will work fine for this example.</span></span> <span data-ttu-id="6f351-140">Espandere il Visualizzazione risorse _*_pixelmaps_*_ e fare clic sul pulsante _ \*_Aggiungi nuovo Pixelmap_\*\*:</span><span class="sxs-lookup"><span data-stu-id="6f351-140">Expand your _*_Pixelmaps_*_ Resource View and click the _ *_Add New Pixelmap_*\* button:</span></span>

![Screenshot del pulsante Aggiungi nuovo Pixelmap.](./media/guix-studio/image74.jpg)

<span data-ttu-id="6f351-142">Passare alla cartella di installazione di GUIX studio e nella cartella ***./graphics/icons** _ selezionare il file denominato _*_i_history_lg.png_\*_.</span><span class="sxs-lookup"><span data-stu-id="6f351-142">Browse to your GUIX Studio installation folder, and within the ***./graphics/icons** _ folder select the file named _*_i_history_lg.png_\*_.</span></span> <span data-ttu-id="6f351-143">Fare clic su _*_Apri_*_ per aggiungere la risorsa al progetto.</span><span class="sxs-lookup"><span data-stu-id="6f351-143">Click _*_Open_*_ to add this resource to your project.</span></span> <span data-ttu-id="6f351-144">Il Visualizzazione risorse _ *_pixelmaps_*\* dovrebbe ora visualizzare un'anteprima dell'immagine dell'icona appena aggiunta:</span><span class="sxs-lookup"><span data-stu-id="6f351-144">Your _ *_Pixelmaps_*\* Resource View should now show a preview of the newly added icon image:</span></span>

![Screenshot del Visualizzazione risorse pixelmaps.](./media/guix-studio/example_add_pixelmap.png)

<span data-ttu-id="6f351-146">**Figura 10,6**</span><span class="sxs-lookup"><span data-stu-id="6f351-146">**Figure 10.6**</span></span>

<span data-ttu-id="6f351-147">Questa nuova risorsa immagine verrà usata in un secondo momento nell'ambito della progettazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="6f351-147">We will use this new image resource later as part of our UI design.</span></span>

<span data-ttu-id="6f351-148">Analogamente all'aggiunta di una risorsa Pixelmap, verrà aggiunta una nuova risorsa di tipo carattere alla casella degli strumenti in modo che sia possibile utilizzare questo tipo di carattere in un secondo momento nella progettazione.</span><span class="sxs-lookup"><span data-stu-id="6f351-148">Similar to adding a pixelmap resource, we will add a new font resource to our toolbox so that we can use this font later in our design.</span></span> <span data-ttu-id="6f351-149">Espandere ***font** _ visualizzazione risorse e fare clic sul pulsante _*_Aggiungi nuovo tipo di carattere_\*_ .</span><span class="sxs-lookup"><span data-stu-id="6f351-149">Expand the ***Fonts** _ Resource View and click on the _*_Add New Font_\*_ button.</span></span> <span data-ttu-id="6f351-150">Questa azione richiama la finestra di dialogo _*_Aggiungi/modifica_*_ carattere.</span><span class="sxs-lookup"><span data-stu-id="6f351-150">This action will invoke the _*_Add/Edit_*_ font dialog.</span></span> <span data-ttu-id="6f351-151">Passare quindi ai tipi di carattere GUIX specificati nella cartella di installazione di GUIX studio, _\*_ . \\ \\i tipi di carattere verasans_ *_ e selezionare il file del tipo di carattere TrueType denominato _*_VeraIt. ttf_*_. Digitare il tipo di carattere "_*_MEDIUM_ITALIC_*_" nel campo nome carattere e digitare "_*_30_\* \*" nel campo altezza.</span><span class="sxs-lookup"><span data-stu-id="6f351-151">Next, browse to the supplied GUIX fonts in the GUIX Studio installation folder, _\*_.\\fonts\\verasans_ *_, and select the TrueType font file named _*_VeraIt.ttf_*_. Type font the font name "_*_MEDIUM_ITALIC_*_" in the font name field, and type "_*_30_\*\*" in the height field.</span></span> <span data-ttu-id="6f351-152">La finestra di dialogo dovrebbe ora essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="6f351-152">Your dialog should now look like this:</span></span>

![Screenshot della finestra di dialogo Modifica carattere.](./media/guix-studio/example_add_font.png)

<span data-ttu-id="6f351-154">**Figura 10,7**</span><span class="sxs-lookup"><span data-stu-id="6f351-154">**Figure 10.7**</span></span>

<span data-ttu-id="6f351-155">Fare clic su ***OK*** per aggiungere questo tipo di carattere al progetto.</span><span class="sxs-lookup"><span data-stu-id="6f351-155">Click ***OK*** to add this font to your project.</span></span> <span data-ttu-id="6f351-156">A questo punto il tipo di carattere dovrebbe essere visualizzato nel Visualizzazione risorse:</span><span class="sxs-lookup"><span data-stu-id="6f351-156">You should now see the font in your Resource View:</span></span>

![Screenshot dei tipi di carattere nel Visualizzazione risorse.](./media/guix-studio/example_font_added.png)

<span data-ttu-id="6f351-158">**Figura 10,8**</span><span class="sxs-lookup"><span data-stu-id="6f351-158">**Figure 10.8**</span></span>

<span data-ttu-id="6f351-159">Questo nuovo tipo di carattere verrà usato in un secondo momento nella progettazione dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="6f351-159">We will use this new font later in our UI design.</span></span>

<span data-ttu-id="6f351-160">Ora che sono disponibili alcune nuove risorse, è necessario aggiungere alcuni widget figlio alla schermata che può usare queste risorse.</span><span class="sxs-lookup"><span data-stu-id="6f351-160">Now that we have some new resources available, we need to add some child widgets to our screen that can utilize these resources.</span></span> <span data-ttu-id="6f351-161">Selezionare la finestra creata in precedenza denominata "\***hello_world** _" facendo clic con il pulsante destro del mouse sulla finestra nella visualizzazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6f351-161">Select the previously created window named "\***hello_world** _" by right-clicking on the window in the Target View.</span></span> <span data-ttu-id="6f351-162">Nel menu a comparsa visualizzato, selezionare il comando di menu _*_Inserisci, testo, prompt_*_ per inserire un nuovo widget _ *_GX_PROMPT_*\* e collegare il widget alla finestra di sfondo.</span><span class="sxs-lookup"><span data-stu-id="6f351-162">In the pop-up menu that is now displayed, select the menu command _*_Insert, Text, Prompt_*_ to insert a new _ *_GX_PROMPT_*\* widget and attach the widget to the background window.</span></span> <span data-ttu-id="6f351-163">La finestra dovrebbe ora essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="6f351-163">Your window should now look like this:</span></span>

![Screenshot di un menu a comparsa con la selezione del prompt](./media/guix-studio/image78.jpg)

<span data-ttu-id="6f351-165">**Figura 10,9**</span><span class="sxs-lookup"><span data-stu-id="6f351-165">**Figure 10.9**</span></span>

<span data-ttu-id="6f351-166">Fare clic sul carattere denominato "***MEDIUM_ITALIC** _" in _ *_fonts_** visualizzazione risorse, quindi trascinare e rilasciare il tipo di carattere nel widget della richiesta.</span><span class="sxs-lookup"><span data-stu-id="6f351-166">Click on the font named "***MEDIUM_ITALIC** _" in the _ *_Fonts_** Resource View, and drag and drop the font on the prompt widget.</span></span> <span data-ttu-id="6f351-167">Modificare quindi le proprietà del prompt come illustrato nella figura 10,10 per ridimensionare la richiesta, impostare la trasparenza della richiesta e modificare il testo e lo stile della richiesta:</span><span class="sxs-lookup"><span data-stu-id="6f351-167">Next, edit the prompt properties as shown in figure 10.10 to resize the prompt, set the prompt transparency, and change the prompt text and style:</span></span>

![Screenshot della visualizzazione delle proprietà per la richiesta.](./media/guix-studio/image79.jpg)

<span data-ttu-id="6f351-169">**Figura 10,10**</span><span class="sxs-lookup"><span data-stu-id="6f351-169">**Figure 10.10**</span></span>

<span data-ttu-id="6f351-170">Potrebbe essere necessario scorrere verticalmente nella visualizzazione proprietà per visualizzare ognuna di queste impostazioni, a seconda della risoluzione dello schermo.</span><span class="sxs-lookup"><span data-stu-id="6f351-170">You may need to scroll vertically in the Properties View to see each of these settings depending on your screen resolution.</span></span> <span data-ttu-id="6f351-171">Dopo avere apportato queste modifiche, la visualizzazione di destinazione dovrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="6f351-171">After making these changes, your Target View should now look like this:</span></span>

![Screenshot di un menu a comparsa con la selezione del Hello World.](./media/guix-studio/image80.jpg)

<span data-ttu-id="6f351-173">**Figura 10,11**</span><span class="sxs-lookup"><span data-stu-id="6f351-173">**Figure 10.11**</span></span>

<span data-ttu-id="6f351-174">A questo punto verrà inserito il widget icona stile pulsante icona sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="6f351-174">Next we will place an Icon Button style widget on the screen.</span></span> <span data-ttu-id="6f351-175">Selezionare la finestra in background facendo clic su di essa e usare il menu di primo livello o il menu a comparsa con il pulsante destro del mouse per selezionare ***Inserisci, pulsante, icona pulsante** _ per aggiungere una nuova _*_GX_ICON_BUTTON_\*_ alla finestra.</span><span class="sxs-lookup"><span data-stu-id="6f351-175">Select the background window by clicking on it, and use either the top-level menu or the right-click pop-up menu to select ***Insert, Button, Icon Button** _ to add a new _*_GX_ICON_BUTTON_\*_ to the window.</span></span> <span data-ttu-id="6f351-176">Fare clic sull'icona denominata _ *_I_HISTORY_LG_*\* aggiunta in precedenza e trascinarla sul pulsante icona.</span><span class="sxs-lookup"><span data-stu-id="6f351-176">Click on the Icon named _ *_I_HISTORY_LG_*\* that we added earlier and drag it to the icon button.</span></span> <span data-ttu-id="6f351-177">Utilizzando la visualizzazione proprietà, modificare la posizione e le dimensioni dell'icona come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6f351-177">Using the properties view, adjust the icon position and size as show below:</span></span>

![Screenshot della visualizzazione delle proprietà per il widget stile pulsante icona.](./media/guix-studio/image81.jpg)

<span data-ttu-id="6f351-179">**Figura 10,12**</span><span class="sxs-lookup"><span data-stu-id="6f351-179">**Figure 10.12**</span></span>

<span data-ttu-id="6f351-180">A questo punto la schermata dovrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="6f351-180">Your screen should now look like this:</span></span>

![Screenshot di un menu a comparsa con il Hello World e l'icona degli Appunti.](./media/guix-studio/image82.jpg)

<span data-ttu-id="6f351-182">**Figura 10,13**</span><span class="sxs-lookup"><span data-stu-id="6f351-182">**Figure 10.13**</span></span>

<span data-ttu-id="6f351-183">Questa operazione verrà chiamata completa per la semplice progettazione della schermata di esempio.</span><span class="sxs-lookup"><span data-stu-id="6f351-183">We will call this complete for the simple example screen design.</span></span> <span data-ttu-id="6f351-184">È probabile che le schermate dell'applicazione siano molto più sofisticate, ma ciò è sufficiente per illustrare come usare GUIX Studio per creare schermate delle applicazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="6f351-184">Your actual application screens will likely be much more sophisticated, but this is enough to show you how to use GUIX Studio to create your own application screens.</span></span>

## <a name="generate-resource-and-application-code"></a><span data-ttu-id="6f351-185">Generare codice di risorse e applicazioni</span><span class="sxs-lookup"><span data-stu-id="6f351-185">Generate Resource and Application Code</span></span>

<span data-ttu-id="6f351-186">Il passaggio successivo consiste nel generare il file di risorse e il file di specifica che definiscono l'interfaccia utente di run-time GUIX incorporata.</span><span class="sxs-lookup"><span data-stu-id="6f351-186">The next step is to generate the resource file and specification file that define the embedded GUIX run-time UI.</span></span> <span data-ttu-id="6f351-187">Per generare i file di output, è necessario fare clic con il pulsante destro del mouse sul nodo \***main_display** _ nella visualizzazione del progetto e selezionare il comando _ \*_genera file di risorse_\*\*.</span><span class="sxs-lookup"><span data-stu-id="6f351-187">To generate your output files you will need right-click on the ***main_display** _ node in the Project View, and select the _ *_Generate Resource Files_** command.</span></span> <span data-ttu-id="6f351-188">Si osserverà una finestra informativa che indica che i file di risorse sono stati generati, come illustrato nella figura 10,14:</span><span class="sxs-lookup"><span data-stu-id="6f351-188">You will observe an information window that indicates your resource files have been generated, as shown in figure 10.14:</span></span>

![Screenshot di una finestra di dialogo di notifica.](./media/guix-studio/image83.jpg)

<span data-ttu-id="6f351-190">**Figura 10,14**</span><span class="sxs-lookup"><span data-stu-id="6f351-190">**Figure 10.14**</span></span>

<span data-ttu-id="6f351-191">Fare clic su ***OK** per chiudere la notifica e utilizzare la stessa procedura per fare clic con il pulsante destro del mouse sul nodo _*_main_display_\*_ e selezionare il comando _ \*_genera file di specifica_\*\*.</span><span class="sxs-lookup"><span data-stu-id="6f351-191">Click ***OK** _ to dismiss this notification, and use the same procedure to right-click on the _*_main_display_*_ node and select the _ *_Generate Specification Files_** command.</span></span> <span data-ttu-id="6f351-192">È necessario osservare una finestra di notifica simile.</span><span class="sxs-lookup"><span data-stu-id="6f351-192">You should observe a similar notification window.</span></span> <span data-ttu-id="6f351-193">A questo punto sono stati generati i file dell'applicazione dell'interfaccia utente semplici.</span><span class="sxs-lookup"><span data-stu-id="6f351-193">You have now generated your simple UI application files.</span></span>

## <a name="create-user-supplied-code"></a><span data-ttu-id="6f351-194">Crea codice fornito dall'utente</span><span class="sxs-lookup"><span data-stu-id="6f351-194">Create User Supplied Code</span></span>

<span data-ttu-id="6f351-195">Il passaggio successivo consiste nel creare il file dell'applicazione che richiama la progettazione della schermata generata da GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="6f351-195">The next step is to create your own application file that will invoke the GUIX Studio-generated screen design.</span></span> <span data-ttu-id="6f351-196">Usando l'editor preferito, creare un file di origine denominato ***new_example. c*** e immettere il codice sorgente seguente nel file:</span><span class="sxs-lookup"><span data-stu-id="6f351-196">Using your preferred editor, create a source file named ***new_example.c***, and enter the following source code into this file:</span></span>

```C

/* This is an example of the GUIX graphics framework in Win32. */
/* Include system files. */

#include <stdio.h>
#include "tx_api.h"
#include "gx_api.h"

/* Include GUIX resource and specification files for example. */

#include "new_example_resources.h"
#include "new_example_specifications.h"

/* Define the new example thread control block and stack. */

TX_THREAD new_example_thread;
UCHAR new_example_thread_stack[4096];

/* Define the root window pointer. */

GX_WINDOW_ROOT *root_window;

/* Define function prototypes. */

VOID new_example_thread_entry(ULONG thread_input);
UINT win32_graphics_driver_setup_24bpp(GX_DISPLAY *display);

int main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
    return(0);
}

VOID tx_application_define(void *first_unused_memory)
{
    /* Create the new example thread. */
    tx_thread_create(&new_example_thread, "GUIX New Example Thread", 
                      new_example_thread_entry, 0, 
                      new_example_thread_stack, sizeof(new_example_thread_stack),
                      1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);
}

VOID new_example_thread_entry(ULONG thread_input)
{

    /* Initialize the GUIX library */
    gx_system_initialize();

    /* Configure the main display. */
    gx_studio_display_configure(MAIN_DISPLAY,                      /* Display to configure*/
                                win32_graphics_driver_setup_24bpp, /* Driver to use */
                                LANGUAGE_ENGLISH,                  /* Language to install */
                                MAIN_DISPLAY_DEFAULT_THEME,        /* Theme to install */
                                &root_window);                     /* Root window pointer */

    /* Create the screen - attached to root window. */

    gx_studio_named_widget_create("hello_world", (GX_WIDGET *) root_window, GX_NULL);

    /* Show the root window to make it visible. */
    gx_widget_show(root_window);

    /* Let GUIX run. */
    gx_system_start();

}
```

<span data-ttu-id="6f351-197">Il codice sorgente precedente crea un tipico thread ThreadX denominato `GUIX New Example Thread` con una dimensione dello stack di 4K byte.</span><span class="sxs-lookup"><span data-stu-id="6f351-197">The source code above creates a typical ThreadX thread named `GUIX New Example Thread` with a stack size of 4K bytes.</span></span> <span data-ttu-id="6f351-198">Il lavoro interessante inizia nella funzione denominata ***new_example_thread_entry***.</span><span class="sxs-lookup"><span data-stu-id="6f351-198">The interesting work begins in the function named ***new_example_thread_entry***.</span></span> <span data-ttu-id="6f351-199">Questa funzione è la posizione in cui inizia l'esecuzione del thread specifico di GUIX.</span><span class="sxs-lookup"><span data-stu-id="6f351-199">This function is where the GUIX specific thread begins to run.</span></span>

<span data-ttu-id="6f351-200">La prima chiamata è alla funzione denominata ***gx_system_initialize***.</span><span class="sxs-lookup"><span data-stu-id="6f351-200">The first call is to the function named ***gx_system_initialize***.</span></span> <span data-ttu-id="6f351-201">Questa chiamata è sempre obbligatoria prima che vengano richiamate altre API GUIX per preparare la libreria GUIX per il primo utilizzo.</span><span class="sxs-lookup"><span data-stu-id="6f351-201">This call is always required before any other GUIX APIs are invoked to prepare the GUIX library for first use.</span></span>

<span data-ttu-id="6f351-202">Nell'esempio viene quindi chiamata la funzione ***gx_studio_display_configure***.</span><span class="sxs-lookup"><span data-stu-id="6f351-202">Next, the example calls the function ***gx_studio_display_configure***.</span></span> <span data-ttu-id="6f351-203">Questa funzione crea l'istanza di visualizzazione GUIX, installa la lingua richiesta della tabella delle stringhe dell'applicazione, installa il tema richiesto dalle risorse di visualizzazione e restituisce un puntatore alla finestra radice creata per questa visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="6f351-203">This function creates the GUIX display instance, installs the requested language of the application string table, installs the requested theme from the display resources, and returns a pointer to the root window that has been created for this display.</span></span> <span data-ttu-id="6f351-204">La finestra radice viene usata come elemento padre di tutte le schermate di primo livello che l'applicazione visualizzerà.</span><span class="sxs-lookup"><span data-stu-id="6f351-204">The root window is used as the parent of all top-level screens that our application will display.</span></span>

<span data-ttu-id="6f351-205">Successivamente, l'esempio chiama \***gx_studio_named_widget_create** _ per creare un'istanza della schermata _ \*_hello_world_\*\*.</span><span class="sxs-lookup"><span data-stu-id="6f351-205">Next the example calls ***gx_studio_named_widget_create** _ to create an instance of our _ *_hello_world_** screen.</span></span> <span data-ttu-id="6f351-206">Questa funzione usa le strutture di dati e le risorse generate da GUIX Studio per creare un'istanza della schermata come è stata definita.</span><span class="sxs-lookup"><span data-stu-id="6f351-206">This function uses the data structures and resource produces by GUIX Studio to create an instance of the screen as we have defined it.</span></span> <span data-ttu-id="6f351-207">Il puntatore della finestra radice viene passato come secondo parametro a questa chiamata di funzione, ovvero si vuole che la schermata venga collegata immediatamente alla finestra radice.</span><span class="sxs-lookup"><span data-stu-id="6f351-207">We pass the root window pointer as the second parameter to this function call, meaning we want the screen to be immediately attached to the root window.</span></span> <span data-ttu-id="6f351-208">L'ultimo parametro è un puntatore restituito facoltativo che può essere usato se si vuole tenere un puntatore alla schermata creata.</span><span class="sxs-lookup"><span data-stu-id="6f351-208">The last parameter is an optional return pointer that can be used if we want to keep a pointer to the created screen.</span></span>

<span data-ttu-id="6f351-209">Viene chiamato Next \***gx_widget_show** _, che rende visibile la finestra radice e tutti i relativi elementi figlio, inclusa la schermata _ \*_hello_world_\*\*.</span><span class="sxs-lookup"><span data-stu-id="6f351-209">Next ***gx_widget_show** _ is called, which makes the root window and all of its children, including the _ *_hello_world_** screen, visible.</span></span>

<span data-ttu-id="6f351-210">Infine, nell'esempio viene chiamato ***gx_system_start***.</span><span class="sxs-lookup"><span data-stu-id="6f351-210">Finally, the example calls ***gx_system_start***.</span></span> <span data-ttu-id="6f351-211">Questa funzione inizia l'esecuzione del ciclo di elaborazione degli eventi di sistema GUIX.</span><span class="sxs-lookup"><span data-stu-id="6f351-211">This function begins executing the GUIX system event processing loop.</span></span>

## <a name="build-and-run-the-example"></a><span data-ttu-id="6f351-212">Compilare ed eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="6f351-212">Build and Run the Example</span></span>

<span data-ttu-id="6f351-213">Compilare ed eseguire l'esempio è specifico per gli strumenti e l'ambiente di compilazione.</span><span class="sxs-lookup"><span data-stu-id="6f351-213">Building and running the example is specific to your build tools and environment.</span></span> <span data-ttu-id="6f351-214">Tuttavia è possibile definire il processo generale:</span><span class="sxs-lookup"><span data-stu-id="6f351-214">However we can define the general process:</span></span>

1. <span data-ttu-id="6f351-215">Creare una nuova directory e un nuovo progetto di applicazione</span><span class="sxs-lookup"><span data-stu-id="6f351-215">Create a new directory and application project</span></span>
1. <span data-ttu-id="6f351-216">Aggiungere questi file al progetto:</span><span class="sxs-lookup"><span data-stu-id="6f351-216">Add these files to the project:</span></span>

    <span data-ttu-id="6f351-217">**new_example_resources. c**</span><span class="sxs-lookup"><span data-stu-id="6f351-217">**new_example_resources.c**</span></span>

    <span data-ttu-id="6f351-218">**new_example_specification. c**</span><span class="sxs-lookup"><span data-stu-id="6f351-218">**new_example_specification.c**</span></span>

    <span data-ttu-id="6f351-219">**new_example. c**</span><span class="sxs-lookup"><span data-stu-id="6f351-219">**new_example.c**</span></span>

1. <span data-ttu-id="6f351-220">Aggiungere i file di supporto della fase di esecuzione Win32 dal percorso di installazione di GUIX Studio ***./win32_runtime***.</span><span class="sxs-lookup"><span data-stu-id="6f351-220">Add the Win32 run-time support files from the GUIX Studio installation path ***./win32_runtime***.</span></span> <span data-ttu-id="6f351-221">Sono inclusi i file di intestazione Win32 ThreadX e GUIX e la libreria di Runtime.</span><span class="sxs-lookup"><span data-stu-id="6f351-221">This includes the ThreadX and GUIX Win32 header and run-time library files.</span></span>
1. <span data-ttu-id="6f351-222">Aggiungere la libreria Win32 GUIX (***GX. lib***) al progetto</span><span class="sxs-lookup"><span data-stu-id="6f351-222">Add the GUIX Win32 library (***gx.lib***) to the project</span></span>
1. <span data-ttu-id="6f351-223">Aggiungere la libreria Win32 ThreadX (***TX. lib***) al progetto</span><span class="sxs-lookup"><span data-stu-id="6f351-223">Add the ThreadX Win32 library (***tx.lib***) to the project</span></span>
1. <span data-ttu-id="6f351-224">Compilare, collegare ed eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6f351-224">Compile, Link, and Run the application!</span></span>
