---
title: Informazioni Azure RTOS GUIX e Azure RTOS GUIX Studio
description: Azure RTOS GUIX è un pacchetto di qualità professionale, creato per soddisfare le esigenze degli sviluppatori di sistemi incorporati.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 8f4a1578fcabdabfb213ced9c6593f6cffc964aa
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171404"
---
# <a name="overview-of-azure-rtos-guix-and-azure-rtos-guix-studio"></a><span data-ttu-id="9d873-103">Panoramica di Azure RTOS GUIX e Azure RTOS GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="9d873-103">Overview of Azure RTOS GUIX and Azure RTOS GUIX Studio</span></span>

<span data-ttu-id="9d873-104">L'interfaccia utente grafica incorporata GUIX di Azure è la soluzione GUI avanzata di livello industriale di Microsoft progettata specificamente per applicazioni IoT, in tempo reale e con deep embedded.</span><span class="sxs-lookup"><span data-stu-id="9d873-104">Azure GUIX embedded GUI is Microsoft’s advanced, industrial grade GUI solution designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="9d873-105">Microsoft offre anche uno strumento di progettazione desktop WYSIWYG completo denominato Azure RTOS GUIX Studio, che consente agli sviluppatori di progettare la gui sul desktop e generare codice GUIX incorporato Azure RTOS che può quindi essere esportato nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="9d873-105">Microsoft also provides a full-featured WYSIWYG desktop design tool named Azure RTOS GUIX Studio, which allows developers to design their GUI on the desktop and generate Azure RTOS GUIX embedded GUI code that can then be exported to the target.</span></span> <span data-ttu-id="9d873-106">Azure RTOS GUIX è completamente integrato con Azure RTOS ThreadX RTOS ed è disponibile per molti degli stessi processori supportati da Azure RTOS ThreadX.</span><span class="sxs-lookup"><span data-stu-id="9d873-106">Azure RTOS GUIX is fully integrated with Azure RTOS ThreadX RTOS and is available for many of the same processors supported by Azure RTOS ThreadX.</span></span> <span data-ttu-id="9d873-107">Il tutto combinato con un footprint estremamente ridotto, un'esecuzione rapida e una maggiore facilità d'uso, rende Azure RTOS GUIX la scelta ideale per le applicazioni IoT incorporate più complesse che richiedono un'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="9d873-107">All of this combined with an extremely small footprint, fast execution, and superior ease-of-use, make Azure RTOS GUIX the ideal choice for the most demanding embedded IoT applications requiring a user interface.</span></span> 

## <a name="azure-rtos-guix-api"></a><span data-ttu-id="9d873-108">Azure RTOS aPI GUIX</span><span class="sxs-lookup"><span data-stu-id="9d873-108">Azure RTOS GUIX API</span></span>

### <a name="powerful-apis"></a><span data-ttu-id="9d873-109">API potenti</span><span class="sxs-lookup"><span data-stu-id="9d873-109">Powerful APIs</span></span>

* <span data-ttu-id="9d873-110">Supporto completo per il disegno diretto nell'area di disegno quando necessario</span><span class="sxs-lookup"><span data-stu-id="9d873-110">Full support for direct canvas drawing when needed</span></span>
* <span data-ttu-id="9d873-111">Semplice interazione con Azure RTOS codice generato da GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="9d873-111">Simple to interact with Azure RTOS GUIX Studio generated code</span></span>
* <span data-ttu-id="9d873-112">API per linee, rettangoli, poligoni e così via.</span><span class="sxs-lookup"><span data-stu-id="9d873-112">APIs for line, rectangle, polygon, etc.</span></span>
* <span data-ttu-id="9d873-113">API per circle, arc, pie, chord, ellipse e così via.</span><span class="sxs-lookup"><span data-stu-id="9d873-113">APIs for circle, arc, pie, chord, ellipse, etc.</span></span>
* <span data-ttu-id="9d873-114">API per il disegno e il posizionamento del testo</span><span class="sxs-lookup"><span data-stu-id="9d873-114">APIs for text drawing and positioning</span></span>
* <span data-ttu-id="9d873-115">Anti-aliasing, riempimenti di trama e riempimenti a tinta unita</span><span class="sxs-lookup"><span data-stu-id="9d873-115">Anti-aliasing, texture fills, and solid fills</span></span>
* <span data-ttu-id="9d873-116">API per la creazione e la modifica di schermate e widget</span><span class="sxs-lookup"><span data-stu-id="9d873-116">APIs for creating and modifing screens and widgets</span></span>

### <a name="azure-rtos-guix-studio-generated-files"></a><span data-ttu-id="9d873-117">Azure RTOS file generati da GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="9d873-117">Azure RTOS GUIX Studio Generated Files</span></span>

* <span data-ttu-id="9d873-118">File di origine ANSI C generati automaticamente</span><span class="sxs-lookup"><span data-stu-id="9d873-118">Automatically generated ANSI C source files</span></span>
* <span data-ttu-id="9d873-119">Isola il software applicativo dai dettagli del layout</span><span class="sxs-lookup"><span data-stu-id="9d873-119">Insulates application software from layout details</span></span>
* <span data-ttu-id="9d873-120">Include i tipi di carattere e le immagini richiesti dalla progettazione dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="9d873-120">Includes fonts and images required by UI design</span></span>
* <span data-ttu-id="9d873-121">File generati compilati con il codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9d873-121">Generated files compiled with application code</span></span>
* <span data-ttu-id="9d873-122">Il layout dello schermo può essere aggiornato senza influire sulla logica dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9d873-122">Screen layout can be updated without affecting application logic</span></span>
* <span data-ttu-id="9d873-123">Gli ID risorsa creano l'indipendenza della lingua e del tema</span><span class="sxs-lookup"><span data-stu-id="9d873-123">Resource IDs create language and theme independence</span></span>
* <span data-ttu-id="9d873-124">Funzioni di disegno ed elaborazione eventi personalizzate fornite dall'utente</span><span class="sxs-lookup"><span data-stu-id="9d873-124">User-supplied custom drawing and event processing functions</span></span>

### <a name="widget-library"></a><span data-ttu-id="9d873-125">Libreria widget</span><span class="sxs-lookup"><span data-stu-id="9d873-125">Widget library</span></span>

* <span data-ttu-id="9d873-126">Set predefinito ma personalizzabile di elementi di interfaccia comuni</span><span class="sxs-lookup"><span data-stu-id="9d873-126">Pre-defined but customizable set of common interface elements</span></span>
* <span data-ttu-id="9d873-127">Estremamente piccola, compatta ed efficiente</span><span class="sxs-lookup"><span data-stu-id="9d873-127">Extremely small, compact, and efficient</span></span>
* <span data-ttu-id="9d873-128">La libreria include pulsante, misuratore, elenco, finestra, scorrimento, dispositivo di scorrimento, indicatore di stato, richiesta e altro ancora</span><span class="sxs-lookup"><span data-stu-id="9d873-128">Library includes button, gauge, list, window, scroll, slider, progress bar, prompt and many more</span></span>
* <span data-ttu-id="9d873-129">Disegno e aspetto completamente personalizzabili</span><span class="sxs-lookup"><span data-stu-id="9d873-129">Fully customizable drawing and appearance</span></span>
* <span data-ttu-id="9d873-130">Gestione di operazioni e eventi completamente personalizzabili</span><span class="sxs-lookup"><span data-stu-id="9d873-130">Fully customizable operation and event handling</span></span>
* <span data-ttu-id="9d873-131">Solo i widget usati sono collegati al software dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9d873-131">Only the widgets used are linked with application software</span></span>

### <a name="math-and-utilities"></a><span data-ttu-id="9d873-132">Matematica e utilità</span><span class="sxs-lookup"><span data-stu-id="9d873-132">Math and utilities</span></span>

* <span data-ttu-id="9d873-133">Funzioni per sin, cos, arcsin, arccos, tangente, radice quadrata</span><span class="sxs-lookup"><span data-stu-id="9d873-133">Functions for sin, cos, arcsin, arccos, tangent, square root</span></span>
* <span data-ttu-id="9d873-134">Funzioni per la modifica delle aree dello schermo</span><span class="sxs-lookup"><span data-stu-id="9d873-134">Functions for manipulating screen regions</span></span>
* <span data-ttu-id="9d873-135">Configurazione e avvio del sistema</span><span class="sxs-lookup"><span data-stu-id="9d873-135">System configuration and startup</span></span>
* <span data-ttu-id="9d873-136">Definizione del pool di memoria (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="9d873-136">Memory pool definition (optional)</span></span>
* <span data-ttu-id="9d873-137">Gestione timer</span><span class="sxs-lookup"><span data-stu-id="9d873-137">Timer Management</span></span>
* <span data-ttu-id="9d873-138">Gestione delle animazioni</span><span class="sxs-lookup"><span data-stu-id="9d873-138">Animation Management</span></span>
* <span data-ttu-id="9d873-139">Manutenzione degli elenchi dirty</span><span class="sxs-lookup"><span data-stu-id="9d873-139">Dirty list maintenance</span></span>

### <a name="image-processing"></a><span data-ttu-id="9d873-140">Elaborazione di immagini</span><span class="sxs-lookup"><span data-stu-id="9d873-140">Image processing</span></span>

* <span data-ttu-id="9d873-141">Funzioni per la decodifica di runtime di immagini jpeg e png</span><span class="sxs-lookup"><span data-stu-id="9d873-141">Functions for runtime decode of jpeg and png images</span></span>
* <span data-ttu-id="9d873-142">Applicare il dithering e la conversione dello spazio colore</span><span class="sxs-lookup"><span data-stu-id="9d873-142">Apply dithering and color space conversion</span></span>
* <span data-ttu-id="9d873-143">Rotazione delle immagini</span><span class="sxs-lookup"><span data-stu-id="9d873-143">Image rotation</span></span>
* <span data-ttu-id="9d873-144">Ridimensionamento delle immagini</span><span class="sxs-lookup"><span data-stu-id="9d873-144">Image scaling</span></span>
* <span data-ttu-id="9d873-145">Fusione di immagini</span><span class="sxs-lookup"><span data-stu-id="9d873-145">Image blending</span></span>

### <a name="event-processing"></a><span data-ttu-id="9d873-146">Elaborazione di eventi</span><span class="sxs-lookup"><span data-stu-id="9d873-146">Event processing</span></span>

* <span data-ttu-id="9d873-147">Sospende automaticamente Azure RTOS thread GUIX quando è inattivo</span><span class="sxs-lookup"><span data-stu-id="9d873-147">Automatically suspends Azure RTOS GUIX thread when idle</span></span>
* <span data-ttu-id="9d873-148">Modello di programmazione basato su eventi molto diffuso nella progettazione dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="9d873-148">Event-driven programming model popular in UI design</span></span>
* <span data-ttu-id="9d873-149">Isola i driver di input Azure RTOS thread di disegno GUIX</span><span class="sxs-lookup"><span data-stu-id="9d873-149">Insulates input drivers from Azure RTOS GUIX drawing thread</span></span>
* <span data-ttu-id="9d873-150">Funzioni per l'invio e la ricezione di eventi</span><span class="sxs-lookup"><span data-stu-id="9d873-150">Functions for sending and receiving events</span></span>
* <span data-ttu-id="9d873-151">Tipi di evento predefiniti per tutti i Azure RTOS di widget GUIX</span><span class="sxs-lookup"><span data-stu-id="9d873-151">Pre-defined event types for all Azure RTOS GUIX widget types</span></span>
* <span data-ttu-id="9d873-152">Eventi personalizzati definiti dall'utente supportati</span><span class="sxs-lookup"><span data-stu-id="9d873-152">User-defined custom events supported</span></span>

### <a name="canvas-processing"></a><span data-ttu-id="9d873-153">Elaborazione di canvas</span><span class="sxs-lookup"><span data-stu-id="9d873-153">Canvas processing</span></span>

* <span data-ttu-id="9d873-154">Manutenzione di ritaglio e ordine Z</span><span class="sxs-lookup"><span data-stu-id="9d873-154">Clipping and Z-Order maintenance</span></span>
* <span data-ttu-id="9d873-155">Isola la libreria di widget dai dettagli dell'hardware</span><span class="sxs-lookup"><span data-stu-id="9d873-155">Insulates widget library from hardware details</span></span>
* <span data-ttu-id="9d873-156">Isola l'applicazione dai dettagli dell'hardware</span><span class="sxs-lookup"><span data-stu-id="9d873-156">Insulates application from hardware details</span></span>
* <span data-ttu-id="9d873-157">Aggiornamento automatico in background delle aree dirty</span><span class="sxs-lookup"><span data-stu-id="9d873-157">Automatic background refresh of dirty areas</span></span>
* <span data-ttu-id="9d873-158">Più canvas con livelli e fusione supportati</span><span class="sxs-lookup"><span data-stu-id="9d873-158">Multiple canvases with layering and blending supported</span></span>
* <span data-ttu-id="9d873-159">Può essere richiamato direttamente dal software dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="9d873-159">Can be invoked directly by the application software</span></span>

### <a name="input-device-drivers"></a><span data-ttu-id="9d873-160">Driver di dispositivo di input</span><span class="sxs-lookup"><span data-stu-id="9d873-160">Input device driver(s)</span></span>

* <span data-ttu-id="9d873-161">Supporto specifico dell'hardware, Azure RTOS GUIX e applicazione isolata dai dettagli dell'hardware</span><span class="sxs-lookup"><span data-stu-id="9d873-161">Hardware-specific support, Azure RTOS GUIX and application insulated from hardware details</span></span>
* <span data-ttu-id="9d873-162">Supporto di touch, tappo e tastierino di resistenza</span><span class="sxs-lookup"><span data-stu-id="9d873-162">Resistive Touch, Cap Touch, and keypad supported</span></span>
* <span data-ttu-id="9d873-163">Eventi di input passati alla coda Azure RTOS eventi GUIX</span><span class="sxs-lookup"><span data-stu-id="9d873-163">Input events passed to Azure RTOS GUIX event queue</span></span>

### <a name="display-drivers"></a><span data-ttu-id="9d873-164">Visualizzare i driver</span><span class="sxs-lookup"><span data-stu-id="9d873-164">Display drivers</span></span>

* <span data-ttu-id="9d873-165">Supporto specifico dell'hardware</span><span class="sxs-lookup"><span data-stu-id="9d873-165">Hardware-specific support</span></span>
* <span data-ttu-id="9d873-166">Driver generici forniti per tutti i formati e la profondità del colore</span><span class="sxs-lookup"><span data-stu-id="9d873-166">Generic drivers provided for all color depth and formats</span></span>
* <span data-ttu-id="9d873-167">Personalizzato per usare gli acceleratori di grafica disponibili</span><span class="sxs-lookup"><span data-stu-id="9d873-167">Customized to utilize available graphics accelerators</span></span>

### <a name="target-hardware"></a><span data-ttu-id="9d873-168">Hardware di destinazione</span><span class="sxs-lookup"><span data-stu-id="9d873-168">Target hardware</span></span>

* <span data-ttu-id="9d873-169">Quasi tutti i componenti hardware in grado di eseguire l'output grafico sono compatibili con GUIX</span><span class="sxs-lookup"><span data-stu-id="9d873-169">Nearly any hardware capable of graphical output Is compatible with GUIX</span></span>
* <span data-ttu-id="9d873-170">Più schermi fisici supportati</span><span class="sxs-lookup"><span data-stu-id="9d873-170">Multiple physical displays supported</span></span>
* <span data-ttu-id="9d873-171">Requisiti minimi di RAM e Flash</span><span class="sxs-lookup"><span data-stu-id="9d873-171">Minimal RAM and Flash requirements</span></span>

## <a name="create-elegant-user-interfaces"></a><span data-ttu-id="9d873-172">Creare interfacce utente eleganti</span><span class="sxs-lookup"><span data-stu-id="9d873-172">Create Elegant User Interfaces</span></span>

<span data-ttu-id="9d873-173">Azure RTOS GUIX e Azure RTOS GUIX Studio offrono tutte le funzionalità necessarie per creare interfacce utente univoche ed eleganti.</span><span class="sxs-lookup"><span data-stu-id="9d873-173">Azure RTOS GUIX and Azure RTOS GUIX Studio provide all the features necessary to create uniquely elegant user interfaces.</span></span> <span data-ttu-id="9d873-174">Il pacchetto GUIX Azure RTOS standard include varie interfacce utente di esempio, tra cui un riferimento per dispositivi medici, un riferimento smart watch, un riferimento di automazione domestica, un riferimento di controllo industriale, un riferimento automobilistico e vari esempi di sprite e animazione.</span><span class="sxs-lookup"><span data-stu-id="9d873-174">The standard Azure RTOS GUIX package includes various sample user interfaces, including a medical device reference, a smart watch reference, a home automation reference, an industrial control reference, an automotive reference, and various sprite and animation examples.</span></span> <span data-ttu-id="9d873-175">Fare clic sugli esempi di riferimento illustrati di seguito.</span><span class="sxs-lookup"><span data-stu-id="9d873-175">Please click on the reference examples shown below.</span></span>

### <a name="home-automation"></a><span data-ttu-id="9d873-176">Automazione domestica</span><span class="sxs-lookup"><span data-stu-id="9d873-176">Home Automation</span></span>

<img alt="Screenshot of the GUIX home automation" class="img-responsive" src="./media/overview/guix_home_automation.png"/>

### <a name="medical"></a><span data-ttu-id="9d873-177">Medicina</span><span class="sxs-lookup"><span data-stu-id="9d873-177">Medical</span></span>

<img alt="Screenshot of the GUIX medical device" class="img-responsive" src="./media/overview/demo_guix_medical.png"/>

### <a name="consumer"></a><span data-ttu-id="9d873-178">Consumer</span><span class="sxs-lookup"><span data-stu-id="9d873-178">Consumer</span></span>

<img alt="Screenshot of the GUIX Consumer smart watch" class="img-responsive" src="./media/overview/demo_guix_smart_watch.png"/>

### <a name="white-goods"></a><span data-ttu-id="9d873-179">White Goods</span><span class="sxs-lookup"><span data-stu-id="9d873-179">White Goods</span></span>

<img alt="Screenshot of the GUIX white goods exaample" class="img-responsive" src="./media/overview/demo_guix_white_goods.png"/>

### <a name="automotive"></a><span data-ttu-id="9d873-180">Automobilistico</span><span class="sxs-lookup"><span data-stu-id="9d873-180">Automotive</span></span>

<img alt="Screenshot of the GUIX automotive" class="img-responsive" src="./media/overview/demo_guix_infotainment.png"/>

### <a name="industrial"></a><span data-ttu-id="9d873-181">Industriale</span><span class="sxs-lookup"><span data-stu-id="9d873-181">Industrial</span></span>

<img alt="Screenshot of the GUIX industrial control" class="img-responsive" src="./media/overview/demo_guix_industrial.png"/>

<span data-ttu-id="9d873-182">Ogni Azure RTOS riferimento GUIX ha un progetto AZURE RTOS GUIX Studio corrispondente che definisce tutti gli elementi grafici della progettazione di riferimento.</span><span class="sxs-lookup"><span data-stu-id="9d873-182">Each Azure RTOS GUIX reference has a corresponding Azure RTOS GUIX Studio project that defines all the graphical elements of the reference design.</span></span> <span data-ttu-id="9d873-183">La modifica di una progettazione di riferimento è semplice.</span><span class="sxs-lookup"><span data-stu-id="9d873-183">Changing a reference design is easy.</span></span> <span data-ttu-id="9d873-184">È sufficiente aprire il Azure RTOS progetto GUIX corrispondente, apportare le modifiche desiderate, salvare il progetto e quindi selezionare *Progetto*.</span><span class="sxs-lookup"><span data-stu-id="9d873-184">Simply open the corresponding Azure RTOS GUIX project, make the desired changes, save the project, and then select *Project*.</span></span>

<span data-ttu-id="9d873-185">Generare tutti i file di output per generare il codice C per Azure RTOS GUIX.</span><span class="sxs-lookup"><span data-stu-id="9d873-185">Generate All Output Files to generate the C code for Azure RTOS GUIX.</span></span> <span data-ttu-id="9d873-186">È quindi sufficiente ricompilare l'applicazione di destinazione ed eseguire per osservare la progettazione dei riferimenti modificata.</span><span class="sxs-lookup"><span data-stu-id="9d873-186">Then simply rebuild the target application and run to observe the modified reference design.</span></span>

### <a name="memory-footprint"></a><span data-ttu-id="9d873-187">Footprint della memoria</span><span class="sxs-lookup"><span data-stu-id="9d873-187">Memory footprint</span></span>

<span data-ttu-id="9d873-188">Azure RTOS GUIX ha un footprint minimo notevolmente ridotto di 13,2 KB di FLASH e 4 KB di RAM per il supporto di base, senza includere la memoria necessaria per un'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="9d873-188">Azure RTOS GUIX has a remarkably small minimal footprint of 13.2KB of FLASH and 4KB RAM for basic support, not including the memory required for a canvas.</span></span>

<span data-ttu-id="9d873-189">Per una visualizzazione con GRAM interno e tecnologia di aggiornamento automatico, non è necessaria alcuna memoria canvas.</span><span class="sxs-lookup"><span data-stu-id="9d873-189">For a display with internal GRAM and self-refresh technology, no canvas memory is required.</span></span> <span data-ttu-id="9d873-190">Tuttavia, per migliorare le prestazioni di disegno o per una configurazione di visualizzazione che non utilizza GRAM locale per la visualizzazione, viene definita dall'applicazione un'area di memoria canvas.</span><span class="sxs-lookup"><span data-stu-id="9d873-190">However, to improve drawing performance, or for a display configuration that does not utilize GRAM local to the display, a canvas memory area is defined by the application.</span></span>

<span data-ttu-id="9d873-191">I requisiti di memoria dell'area di disegno sono una funzione delle dimensioni dell'area di disegno e della profondità del colore e sono definiti dalla formula:</span><span class="sxs-lookup"><span data-stu-id="9d873-191">Canvas memory requirements are a function of the canvas size as well as the color depth, and are defined by the formula:</span></span>

<span data-ttu-id="9d873-192"><i>RAM canvas (byte) = (x \* y \* (bpp/8))</i></span><span class="sxs-lookup"><span data-stu-id="9d873-192"><i>Canvas RAM (bytes) = (x \* y \* (bpp/8))</i></span></span>

<span data-ttu-id="9d873-193">Dove "x" e "y" sono le dimensioni dell'area di disegno (visualizzazione).</span><span class="sxs-lookup"><span data-stu-id="9d873-193">Where “x” and “y” are the dimensions of the canvas (display).</span></span>

<span data-ttu-id="9d873-194">La maggior parte delle applicazioni usa anche risorse grafiche, che non sono incluse nei requisiti di Azure RTOS di archiviazione della libreria GUIX.</span><span class="sxs-lookup"><span data-stu-id="9d873-194">Most applications also utilize graphical resources, which are not included in the core Azure RTOS GUIX library storage requirements.</span></span> <span data-ttu-id="9d873-195">Queste risorse includono tipi di carattere, icone grafiche (mappe pixel) e stringhe statiche.</span><span class="sxs-lookup"><span data-stu-id="9d873-195">These resources include fonts, graphical icons (pixelmaps), and static strings.</span></span> <span data-ttu-id="9d873-196">Questi dati possono essere archiviati nella sezione const memory (ad esempio FLASH).</span><span class="sxs-lookup"><span data-stu-id="9d873-196">This data can be stored in the const memory section (i.e. FLASH).</span></span>

<span data-ttu-id="9d873-197">Le dimensioni di questa area di memoria dipendono da diversi fattori, tra cui il numero e le dimensioni dei tipi di carattere univoci usati, il numero e le dimensioni delle icone grafiche usate, il formato del colore di output e se ogni risorsa usa o meno dati compressi, poiché Azure RTOS GUIX supporta la compressione RLE dei dati sia del tipo di carattere che della mappa pixel.</span><span class="sxs-lookup"><span data-stu-id="9d873-197">The size of this memory area is dependent on a number of factors, including the number and size of unique fonts used, the number and size of the graphical icons used, the output color format, and whether or not each resource is using compressed data, since Azure RTOS GUIX supports RLE compression of both font and pixelmap data.</span></span> <span data-ttu-id="9d873-198">I requisiti di archiviazione per ogni risorsa vengono visualizzati all'interno dell'applicazione guiX Studio di Azure RTOS, consentendo all'utente di tenere traccia e monitorare la quantità di memoria flash che verrà utilizzata dalle risorse dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9d873-198">The storage requirements for each resource are displayed within the Azure RTOS GUIX Studio application, allowing the user to track and monitor the amount of flash memory that will be consumed by the application resources.</span></span>

<span data-ttu-id="9d873-199">Come Azure RTOS ThreadX, le dimensioni di Azure RTOS GUIX vengono ridimensionate automaticamente in base ai servizi effettivamente usati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9d873-199">Like Azure RTOS ThreadX, the size of Azure RTOS GUIX automatically scales based on the services actually used by the application.</span></span> <span data-ttu-id="9d873-200">Questo elimina virtualmente la necessità di parametri di configurazione e compilazione complessi, semplificando le operazioni per lo sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="9d873-200">This virtually eliminates the need for complicated configuration and build parameters, making things easier for the developer.</span></span>

#### <a name="simple-easy-to-use"></a><span data-ttu-id="9d873-201">Semplice e facile da usare</span><span class="sxs-lookup"><span data-stu-id="9d873-201">Simple, easy-to-use</span></span>

<span data-ttu-id="9d873-202">Azure RTOS GUIX è molto semplice da usare e Azure RTOS GUIX Studio lo rende ancora più semplice consentendo agli sviluppatori di progettare visivamente sul desktop e generare codice C che viene eseguito nella destinazione effettiva.</span><span class="sxs-lookup"><span data-stu-id="9d873-202">Azure RTOS GUIX is very simple to use and Azure RTOS GUIX Studio makes it even easier by allowing developers to visually design on the desktop and generate C code that runs on the actual target.</span></span> <span data-ttu-id="9d873-203">Le applicazioni possono quindi aggiungere funzioni personalizzate di gestione e disegno degli eventi per completare l'interfaccia utente grafica.</span><span class="sxs-lookup"><span data-stu-id="9d873-203">Applications can then add their own custom event handling and drawing functions to complete their GUI.</span></span>

<span data-ttu-id="9d873-204">L'uso Azure RTOS'API GUIX è semplice.</span><span class="sxs-lookup"><span data-stu-id="9d873-204">Using the Azure RTOS GUIX API is straightforward.</span></span> <span data-ttu-id="9d873-205">L Azure RTOS API GUIX è intuitiva e altamente funzionale.</span><span class="sxs-lookup"><span data-stu-id="9d873-205">The Azure RTOS GUIX API is both intuitive and highly functional.</span></span> <span data-ttu-id="9d873-206">I nomi delle API sono fatti di parole reali e non di "zuppe dell'alfabeto" e/o dei nomi altamente abbreviati così comuni in altri file system prodotti.</span><span class="sxs-lookup"><span data-stu-id="9d873-206">The API names are made of real words and not the “alphabet soup” and/or the highly abbreviated names that are so common in other file system products.</span></span> <span data-ttu-id="9d873-207">Tutte Azure RTOS API GUIX hanno un'gx_ *e* seguono una convenzione di denominazione sostantivo-verbo.</span><span class="sxs-lookup"><span data-stu-id="9d873-207">All Azure RTOS GUIX APIs have a leading *gx_* and follow a noun-verb naming convention.</span></span> <span data-ttu-id="9d873-208">Inoltre, esiste una coerenza funzionale in tutta l'API.</span><span class="sxs-lookup"><span data-stu-id="9d873-208">Furthermore, there is a functional consistency throughout the API.</span></span> <span data-ttu-id="9d873-209">Ad esempio, tutte le API che inizializzano un blocco di controllo widget sono denominate widget_type _create e i parametri della funzione create per ogni tipo di widget sono sempre definiti &lt; &gt; nello stesso ordine.</span><span class="sxs-lookup"><span data-stu-id="9d873-209">For example, all APIs that initialize a widget control block are named &lt; widget_type&gt;_create, and the create function parameters for each widget type are always defined in the same order.</span></span>

### <a name="comprehensive-set-of-built-in-widgets"></a><span data-ttu-id="9d873-210">Set completo di widget predefiniti</span><span class="sxs-lookup"><span data-stu-id="9d873-210">Comprehensive set of built-in widgets</span></span>

* <span data-ttu-id="9d873-211">Azure RTOS GUIX offre un set di widget predefiniti, tra cui:</span><span class="sxs-lookup"><span data-stu-id="9d873-211">Azure RTOS GUIX provides a rich set of built-in widgets, including:</span></span>
* <span data-ttu-id="9d873-212">Accordion Menu</span><span class="sxs-lookup"><span data-stu-id="9d873-212">Accordion Menu</span></span>
* <span data-ttu-id="9d873-213">Pulsante</span><span class="sxs-lookup"><span data-stu-id="9d873-213">Button</span></span>
* <span data-ttu-id="9d873-214">Casella di controllo</span><span class="sxs-lookup"><span data-stu-id="9d873-214">Checkbox</span></span>
* <span data-ttu-id="9d873-215">Misuratore circolare</span><span class="sxs-lookup"><span data-stu-id="9d873-215">Circular Gauge</span></span>
* <span data-ttu-id="9d873-216">Elenco a discesa</span><span class="sxs-lookup"><span data-stu-id="9d873-216">Drop Down List</span></span>
* <span data-ttu-id="9d873-217">Elenco orizzontale</span><span class="sxs-lookup"><span data-stu-id="9d873-217">Horizontal List</span></span>
* <span data-ttu-id="9d873-218">Finestra barra di scorrimento orizzontale</span><span class="sxs-lookup"><span data-stu-id="9d873-218">Horizontal Scrollbar Window</span></span>
* <span data-ttu-id="9d873-219">Icona</span><span class="sxs-lookup"><span data-stu-id="9d873-219">Icon</span></span>
* <span data-ttu-id="9d873-220">Pulsante Icona</span><span class="sxs-lookup"><span data-stu-id="9d873-220">Icon Button</span></span>
* <span data-ttu-id="9d873-221">Grafico a linee</span><span class="sxs-lookup"><span data-stu-id="9d873-221">Line Chart</span></span>
* <span data-ttu-id="9d873-222">Menu</span><span class="sxs-lookup"><span data-stu-id="9d873-222">Menu</span></span>
* <span data-ttu-id="9d873-223">Pulsante Testo su più righe</span><span class="sxs-lookup"><span data-stu-id="9d873-223">Multi Line Text Button</span></span>
* <span data-ttu-id="9d873-224">Input di testo su più righe</span><span class="sxs-lookup"><span data-stu-id="9d873-224">Multi Line Text Input</span></span>
* <span data-ttu-id="9d873-225">Visualizzazione testo su più righe</span><span class="sxs-lookup"><span data-stu-id="9d873-225">Multi Line Text View</span></span>
* <span data-ttu-id="9d873-226">Richiesta di mappa pixel numerica</span><span class="sxs-lookup"><span data-stu-id="9d873-226">Numeric Pixelmap Prompt</span></span>
* <span data-ttu-id="9d873-227">Richiesta numerica</span><span class="sxs-lookup"><span data-stu-id="9d873-227">Numeric Prompt</span></span>
* <span data-ttu-id="9d873-228">Rotellina di scorrimento numerica</span><span class="sxs-lookup"><span data-stu-id="9d873-228">Numeric Scroll Wheel</span></span>
* <span data-ttu-id="9d873-229">Pulsante Mappa pixel</span><span class="sxs-lookup"><span data-stu-id="9d873-229">Pixelmap Button</span></span>
* <span data-ttu-id="9d873-230">Richiesta mappa pixel</span><span class="sxs-lookup"><span data-stu-id="9d873-230">Pixelmap Prompt</span></span>
* <span data-ttu-id="9d873-231">Dispositivo di scorrimento mappa pixel</span><span class="sxs-lookup"><span data-stu-id="9d873-231">Pixelmap Slider</span></span>
* <span data-ttu-id="9d873-232">Pixelmap Sprite</span><span class="sxs-lookup"><span data-stu-id="9d873-232">Pixelmap Sprite</span></span>
* <span data-ttu-id="9d873-233">ProgressBar</span><span class="sxs-lookup"><span data-stu-id="9d873-233">Progress Bar</span></span>
* <span data-ttu-id="9d873-234">Prompt</span><span class="sxs-lookup"><span data-stu-id="9d873-234">Prompt</span></span>
* <span data-ttu-id="9d873-235">Indicatore di stato radiale</span><span class="sxs-lookup"><span data-stu-id="9d873-235">Radial Progress Bar</span></span>
* <span data-ttu-id="9d873-236">RadioButton</span><span class="sxs-lookup"><span data-stu-id="9d873-236">Radio Button</span></span>
* <span data-ttu-id="9d873-237">Rotellina</span><span class="sxs-lookup"><span data-stu-id="9d873-237">Scroll Wheel</span></span>
* <span data-ttu-id="9d873-238">Input di testo a riga singola</span><span class="sxs-lookup"><span data-stu-id="9d873-238">Single Line Text Input</span></span>
* <span data-ttu-id="9d873-239">Slider</span><span class="sxs-lookup"><span data-stu-id="9d873-239">Slider</span></span>
* <span data-ttu-id="9d873-240">String Scroll Wheel</span><span class="sxs-lookup"><span data-stu-id="9d873-240">String Scroll Wheel</span></span>
* <span data-ttu-id="9d873-241">Pulsante Testo</span><span class="sxs-lookup"><span data-stu-id="9d873-241">Text Button</span></span>
* <span data-ttu-id="9d873-242">Visualizzazione ad albero</span><span class="sxs-lookup"><span data-stu-id="9d873-242">Tree View</span></span>
* <span data-ttu-id="9d873-243">Elenco verticale</span><span class="sxs-lookup"><span data-stu-id="9d873-243">Vertical List</span></span>
* <span data-ttu-id="9d873-244">Barra di scorrimento verticale</span><span class="sxs-lookup"><span data-stu-id="9d873-244">Vertical Scrollbar</span></span>

<span data-ttu-id="9d873-245">È facile per l'applicazione creare anche i propri widget dei clienti.</span><span class="sxs-lookup"><span data-stu-id="9d873-245">It’s easy for the application to create its own customer widgets as well.</span></span>

### <a name="complete-low-level-drawing-api"></a><span data-ttu-id="9d873-246">COMPLETARE l'API di disegno di basso livello</span><span class="sxs-lookup"><span data-stu-id="9d873-246">Complete low-level drawing API</span></span>

<span data-ttu-id="9d873-247">Azure RTOS GUIX offre un'API di disegno canvas affidabile, che consente all'applicazione di eseguire il rendering di forme grafiche complesse.</span><span class="sxs-lookup"><span data-stu-id="9d873-247">Azure RTOS GUIX provides a robust canvas drawing API, allowing the application to render complex graphical shapes.</span></span>

<span data-ttu-id="9d873-248">Tutte le funzioni supportano l'anti-aliasing su destinazioni con profondità di colore elevata e tutte le forme possono essere riempite dal contorno, inclusi i riempimenti a tinta unita e i riempimenti con motivo mappa pixel.</span><span class="sxs-lookup"><span data-stu-id="9d873-248">All functions support anti-aliasing on high color depth targets, and all shapes can be filled our outlined, including solid and pixelmap pattern fills.</span></span> <span data-ttu-id="9d873-249">Tutte le primitive di disegno supportano il pennello alfa quando l'esecuzione è a 16 bpp e una profondità di colore superiore.</span><span class="sxs-lookup"><span data-stu-id="9d873-249">All drawing primitives support brush alpha when running at 16 bpp and higher color depth.</span></span> <span data-ttu-id="9d873-250">Le funzioni di disegno includono:</span><span class="sxs-lookup"><span data-stu-id="9d873-250">Drawing functions include:</span></span>

* <span data-ttu-id="9d873-251">Arc Draw</span><span class="sxs-lookup"><span data-stu-id="9d873-251">Arc Draw</span></span>
* <span data-ttu-id="9d873-252">Circle Draw</span><span class="sxs-lookup"><span data-stu-id="9d873-252">Circle Draw</span></span>
* <span data-ttu-id="9d873-253">Disegno di linee</span><span class="sxs-lookup"><span data-stu-id="9d873-253">Line Draw</span></span>
* <span data-ttu-id="9d873-254">Disegno a torta</span><span class="sxs-lookup"><span data-stu-id="9d873-254">Pie Draw</span></span>
* <span data-ttu-id="9d873-255">Fusione di mappe pixel</span><span class="sxs-lookup"><span data-stu-id="9d873-255">Pixelmap Blend</span></span>
* <span data-ttu-id="9d873-256">Riquadro mappa pixel</span><span class="sxs-lookup"><span data-stu-id="9d873-256">Pixelmap Tile</span></span>
* <span data-ttu-id="9d873-257">Disegno poligono</span><span class="sxs-lookup"><span data-stu-id="9d873-257">Polygon Draw</span></span>
* <span data-ttu-id="9d873-258">Disegno di testo</span><span class="sxs-lookup"><span data-stu-id="9d873-258">Text Draw</span></span>
* <span data-ttu-id="9d873-259">Chord Draw</span><span class="sxs-lookup"><span data-stu-id="9d873-259">Chord Draw</span></span>
* <span data-ttu-id="9d873-260">Disegno ellisse</span><span class="sxs-lookup"><span data-stu-id="9d873-260">Ellipse Draw</span></span>
* <span data-ttu-id="9d873-261">Disegno in pixel</span><span class="sxs-lookup"><span data-stu-id="9d873-261">Pixel Draw</span></span>
* <span data-ttu-id="9d873-262">Disegno mappa pixel</span><span class="sxs-lookup"><span data-stu-id="9d873-262">Pixelmap Draw</span></span>
* <span data-ttu-id="9d873-263">Rotazione mappa pixel</span><span class="sxs-lookup"><span data-stu-id="9d873-263">Pixelmap Rotate</span></span>
* <span data-ttu-id="9d873-264">Disegno rettangolo</span><span class="sxs-lookup"><span data-stu-id="9d873-264">Rectangle Draw</span></span>
* <span data-ttu-id="9d873-265">Combinazione di testo</span><span class="sxs-lookup"><span data-stu-id="9d873-265">Text Blend</span></span>

### <a name="default-free-fonts-and-easy-to-add-more"></a><span data-ttu-id="9d873-266">Tipi di carattere gratuiti predefiniti e facile da aggiungere</span><span class="sxs-lookup"><span data-stu-id="9d873-266">Default free fonts and easy to add more</span></span>

<span data-ttu-id="9d873-267">Azure RTOS GUIX offre un set gratuito di tipi di carattere TrueType.</span><span class="sxs-lookup"><span data-stu-id="9d873-267">Azure RTOS GUIX provides a free set of TrueType fonts.</span></span> <span data-ttu-id="9d873-268">Gli sviluppatori possono aggiungere altri tipi di carattere TrueType in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="9d873-268">Developers can add additional TrueType fonts as desired.</span></span>

<span data-ttu-id="9d873-269">Il Azure RTOS tipo di carattere GUIX supporta l'anti-aliasing 8bpp, l'anti-aliasing 4bpp e i tipi di carattere monocromatici 1bpp.</span><span class="sxs-lookup"><span data-stu-id="9d873-269">The Azure RTOS GUIX font format supports 8bpp anti-aliasing, 4bpp anti-aliasing, and 1bpp monochrome fonts.</span></span> <span data-ttu-id="9d873-270">Per le applicazioni più vincolate alle risorse, Azure RTOS GUIX esegue il pre-rendering dei tipi di carattere TrueType in un formato bitmap compresso usando lo strumento desktop GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="9d873-270">For the most resource-constrained applications, Azure RTOS GUIX pre-renders the TrueType fonts to a compressed bitmap format using our GUIX Studio desktop tool.</span></span>

### <a name="custom-jpg-and-png-decoder-implementation"></a><span data-ttu-id="9d873-271">Implementazione personalizzata del decodificatore JPG e PNG</span><span class="sxs-lookup"><span data-stu-id="9d873-271">Custom JPG and PNG decoder implementation</span></span>

<span data-ttu-id="9d873-272">Implementazione personalizzata del decodificatore JPG e PNG jpg e del decodificatore di file PNG.</span><span class="sxs-lookup"><span data-stu-id="9d873-272">Custom JPG and PNG decoder implementation JPG and PNG file decoder implementation.</span></span> <span data-ttu-id="9d873-273">Questa implementazione supporta la conversione dello spazio colore, il dithering e la creazione di runtime Azure RTOS immagini in formato pixelmap compatibile con GUIX.</span><span class="sxs-lookup"><span data-stu-id="9d873-273">This implementation supports color space conversion, dithering, and runtime creation of Azure RTOS GUIX-compatible pixelmap format images.</span></span>

### <a name="extensive-display-and-touchscreen-support"></a><span data-ttu-id="9d873-274">Supporto completo dello schermo e del touchscreen</span><span class="sxs-lookup"><span data-stu-id="9d873-274">Extensive display and touchscreen support</span></span>

<span data-ttu-id="9d873-275">Azure RTOS GUIX fornisce driver di visualizzazione generici per quasi tutti i formati di colore, tra cui 1bpp monocromatico, 8 bpp palette, 8 bpp 3:3:2 format,</span><span class="sxs-lookup"><span data-stu-id="9d873-275">Azure RTOS GUIX provides generic display drivers for nearly all color formats, including 1bpp monochrome, 8 bpp palette, 8 bpp 3:3:2 format,</span></span>

<span data-ttu-id="9d873-276">Formato 16 bpp 565 rgb, 16 bpp 4:4:4, 32 bpp x:r:g:b e formato 32 bpp a:r:g:b.</span><span class="sxs-lookup"><span data-stu-id="9d873-276">16 bpp 565 rgb format, 16 bpp 4:4:4:4 format, 32 bpp x:r:g:b format, and 32 bpp a:r:g:b format.</span></span> <span data-ttu-id="9d873-277">Inoltre, Azure RTOS GUIX è integrato con molti dei controller LCD e degli acceleratori hardware più diffusi (ST ChromeArt, Renesas Synergy e così via).</span><span class="sxs-lookup"><span data-stu-id="9d873-277">In addition, Azure RTOS GUIX is integrated with many of the most popular LCD controllers and hardware accelerators (ST ChromeArt, Renesas Synergy, etc.).</span></span>

<span data-ttu-id="9d873-278">Azure RTOS GUIX supporta completamente il touchscreen (incluso il supporto movimenti), la penna e i dispositivi di input della tastiera virtuale.</span><span class="sxs-lookup"><span data-stu-id="9d873-278">Azure RTOS GUIX fully supports touchscreen (including gesture support), pen, and virtual keyboard input devices.</span></span>

### <a name="azure-rtos-guix-studio-desktop-wysiwyg-tool"></a><span data-ttu-id="9d873-279">Azure RTOS STRUMENTO WYSIWYG desktop DI GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="9d873-279">Azure RTOS GUIX Studio desktop WYSIWYG tool</span></span>

<span data-ttu-id="9d873-280">Azure RTOS GUIX Studio offre un ambiente di progettazione schermo WYSIWYG completo che consente all'utente di trascinare gli elementi grafici usati per compilare le schermate gui.</span><span class="sxs-lookup"><span data-stu-id="9d873-280">Azure RTOS GUIX Studio provides a complete WYSIWYG screen design environment which allows the user to drag-and-drop graphical elements used to build the GUI screens.</span></span> <span data-ttu-id="9d873-281">Azure RTOS GUIX Studio genera automaticamente codice C compatibile con la libreria GUIX di Azure RTOS, pronto per essere compilato ed eseguito nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="9d873-281">Azure RTOS GUIX Studio automatically generates C code compatible with the Azure RTOS GUIX library, ready to be compiled and run on the target.</span></span> <span data-ttu-id="9d873-282">Gli sviluppatori possono produrre tipi di carattere di cui è stato eseguito il rendering preliminare da usare all'interno di un'applicazione usando lo strumento Azure RTOS di generazione dei tipi di carattere di GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="9d873-282">Developers can produce pre-rendered fonts for use within an application using the integrated Azure RTOS GUIX Studio font generation tool.</span></span> <span data-ttu-id="9d873-283">I tipi di carattere possono essere generati in formati monocromatici o con anti-aliasing e sono ottimizzati per risparmiare spazio nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="9d873-283">Fonts can be generated in monochrome or anti-aliased formats, and are optimized to save space on the target.</span></span> <span data-ttu-id="9d873-284">I tipi di carattere possono includere qualsiasi set di caratteri, inclusi i caratteri Unicode per le applicazioni multilingue.</span><span class="sxs-lookup"><span data-stu-id="9d873-284">Fonts can include any set of characters, including Unicode characters for multi-lingual applications.</span></span>

<img alt="Diagram of SGS-TUV Saar certification logo" class="alignnone size-full wp-image-1500" height="341" sizes="(max-width: 535px) 100vw, 535px" src="./media/overview/studio_screen_shot.png"/>

<span data-ttu-id="9d873-285">Azure RTOS GUIX Studio facilita l'importazione di grafica da file PNG o JPG con la conversione Azure RTOS pixelmap GUIX compresse per l'uso nel sistema di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9d873-285">Azure RTOS GUIX Studio facilitates the import of graphics from PNG or JPG files with conversion to compressed Azure RTOS GUIX Pixelmaps for use on the target system.</span></span> <span data-ttu-id="9d873-286">Molti dei tipi Azure RTOS widget GUIX sono progettati per incorporare grafica utente per un aspetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9d873-286">Many of the Azure RTOS GUIX widget types are designed to incorporate user graphics for a custom look and feel.</span></span> <span data-ttu-id="9d873-287">Inoltre, Azure RTOS GUIX Studio consente la personalizzazione dei colori predefiniti e degli stili di disegno usati dai widget GUIX di Azure RTOS, consentendo agli sviluppatori di ottimizzare molto facilmente l'aspetto di Azure RTOS GUIX.</span><span class="sxs-lookup"><span data-stu-id="9d873-287">In addition, Azure RTOS GUIX Studio allows customization of the default colors and drawing styles used by the Azure RTOS GUIX widgets, allowing developers to tune the appearance of Azure RTOS GUIX very easily.</span></span> <span data-ttu-id="9d873-288">La generazione e la manutenzione delle stringhe dell'applicazione sono un'altra funzionalità incorporata di Azure RTOS GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="9d873-288">Generation and maintenance of application strings is another built-in facility of Azure RTOS GUIX Studio.</span></span> <span data-ttu-id="9d873-289">In questo modo gli sviluppatori possono progettare un'applicazione usando un linguaggio per lo sviluppo e aggiungere rapidamente e facilmente il supporto per altri linguaggi dopo il rilascio del prodotto.</span><span class="sxs-lookup"><span data-stu-id="9d873-289">This enables developers to design an application using one language for developing, and quickly and easily add support for additional languages after the product is released.</span></span> <span data-ttu-id="9d873-290">Un'applicazione GUIX di Azure RTOS completa può essere eseguita in un pc desktop all'interno dell'ambiente GUIX Studio di Azure RTOS, consentendo una generazione e una dimostrazione rapida e semplice dei concetti relativi all'interfaccia utente grafica, al test dei flussi dello schermo e all'osservazione delle transizioni dello schermo e delle animazioni.</span><span class="sxs-lookup"><span data-stu-id="9d873-290">A complete Azure RTOS GUIX application can be executed on a PC desktop within the Azure RTOS GUIX Studio environment, allowing a quick and easy generation and demonstration of GUI concepts, testing of screen flows, and observation of screen transitions and animations.</span></span> <span data-ttu-id="9d873-291">Al termine, una progettazione può essere esportata come strutture di dati C pronte per la destinazione, pronte per essere compilate e collegate con le librerie GUIX e threadX Azure RTOS Azure RTOS.</span><span class="sxs-lookup"><span data-stu-id="9d873-291">When completed, a design can be exported as target-ready C data structures, ready to be compiled and linked with the Azure RTOS GUIX and Azure RTOS ThreadX libraries.</span></span>

<span data-ttu-id="9d873-292">Azure RTOS GUIX e Azure RTOS GUIX Studio supportano più temi di risorse, consentendo di riassalvare facilmente un'applicazione in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9d873-292">Azure RTOS GUIX and Azure RTOS GUIX Studio support multiple resource themes, allowing an application to be easily reskinned at run-time.</span></span> <span data-ttu-id="9d873-293">I tipi di carattere, i colori e le mappe pixel possono essere modificati in fase di esecuzione con una semplice API.</span><span class="sxs-lookup"><span data-stu-id="9d873-293">Fonts, colors, and pixelmaps can be changed at run-time with one simple API.</span></span>

<span data-ttu-id="9d873-294">Altre informazioni su GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="9d873-294">Learn more about GUIX Studio</span></span>

### <a name="complete-win32-simulation"></a><span data-ttu-id="9d873-295">Completare la simulazione Win32</span><span class="sxs-lookup"><span data-stu-id="9d873-295">Complete Win32 simulation</span></span>

<span data-ttu-id="9d873-296">Azure RTOS GUIX viene eseguito in un PC Windows, usando esattamente la stessa libreria di disegno eseguita sulla scheda di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9d873-296">Azure RTOS GUIX runs on a Windows PC, using exactly the same drawing library that runs on the target board.</span></span> <span data-ttu-id="9d873-297">Con Azure RTOS GUIX, è possibile compilare ed eseguire un'applicazione GUI nel PC e usare lo stesso codice dell'applicazione nella destinazione per il debug, la creazione rapida di prototipi, la dimostrazione e l'operazione di destinazione WYSIWYG.</span><span class="sxs-lookup"><span data-stu-id="9d873-297">With Azure RTOS GUIX, you can build and run a GUI application on the PC, and use the same application code on your target for debugging, rapid prototyping, demonstration, and WYSIWYG target operation.</span></span>

### <a name="advanced-technology"></a><span data-ttu-id="9d873-298">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="9d873-298">Advanced technology</span></span>

* <span data-ttu-id="9d873-299">Azure RTOS tecnologia avanzata di GUIX incorpora:</span><span class="sxs-lookup"><span data-stu-id="9d873-299">Azure RTOS GUIX's advanced technology incorporates:</span></span>
* <span data-ttu-id="9d873-300">Fusione alfa</span><span class="sxs-lookup"><span data-stu-id="9d873-300">Alpha blending</span></span>
* <span data-ttu-id="9d873-301">Antialiasing</span><span class="sxs-lookup"><span data-stu-id="9d873-301">Anti-Aliasing</span></span>
* <span data-ttu-id="9d873-302">Scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="9d873-302">Automatic scaling</span></span>
* <span data-ttu-id="9d873-303">Compressione bitmap</span><span class="sxs-lookup"><span data-stu-id="9d873-303">Bitmap compression</span></span>
* <span data-ttu-id="9d873-304">Fusione dell'area di disegno</span><span class="sxs-lookup"><span data-stu-id="9d873-304">Canvas blending</span></span>
* <span data-ttu-id="9d873-305">Supporto dei widget personalizzati</span><span class="sxs-lookup"><span data-stu-id="9d873-305">Custom widget support</span></span>
* <span data-ttu-id="9d873-306">Supporto del disegno posticipato</span><span class="sxs-lookup"><span data-stu-id="9d873-306">Deferred drawing support</span></span>
* <span data-ttu-id="9d873-307">Supporto del dithering</span><span class="sxs-lookup"><span data-stu-id="9d873-307">Dithering support</span></span>
* <span data-ttu-id="9d873-308">Programmazione neutra endiana</span><span class="sxs-lookup"><span data-stu-id="9d873-308">Endian neutral programming</span></span>
* <span data-ttu-id="9d873-309">Supporto dell'acceleratore hardware</span><span class="sxs-lookup"><span data-stu-id="9d873-309">Hardware accelerator support</span></span>
* <span data-ttu-id="9d873-310">Supporto multilingue e codifica UTF-8</span><span class="sxs-lookup"><span data-stu-id="9d873-310">Multilingual support and UTF-8 encoding</span></span>
* <span data-ttu-id="9d873-311">Supporto di più display e canvas</span><span class="sxs-lookup"><span data-stu-id="9d873-311">Multiple display and canvas support</span></span>
* <span data-ttu-id="9d873-312">Gestione ottimizzata di ritaglio, disegno e eventi</span><span class="sxs-lookup"><span data-stu-id="9d873-312">Optimized clipping, drawing, and event handling</span></span>
* <span data-ttu-id="9d873-313">Decodificatore JPEG e PNG di runtime</span><span class="sxs-lookup"><span data-stu-id="9d873-313">Runtime JPEG and PNG decoder</span></span>
* <span data-ttu-id="9d873-314">Interfaccia e temi</span><span class="sxs-lookup"><span data-stu-id="9d873-314">Skinning and Themes</span></span>
* <span data-ttu-id="9d873-315">Supporta il colore reale monocromatico a 32 bit con formati di grafica alfa</span><span class="sxs-lookup"><span data-stu-id="9d873-315">Supports monochrome through 32-bit true-color with alpha graphics formats</span></span>
* <span data-ttu-id="9d873-316">Transizioni, Sprite e supporto dell'animazione</span><span class="sxs-lookup"><span data-stu-id="9d873-316">Transitions, Sprites, and Animation support</span></span>
* <span data-ttu-id="9d873-317">Simulazione Win32</span><span class="sxs-lookup"><span data-stu-id="9d873-317">Win32 simulation</span></span>
* <span data-ttu-id="9d873-318">Gestione delle finestre, inclusi viewport e manutenzione dell'ordine Z</span><span class="sxs-lookup"><span data-stu-id="9d873-318">Window management including Viewports and Z-order maintenance</span></span>
