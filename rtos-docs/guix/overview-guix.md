---
title: Informazioni su Azure RTO GUIX e Azure RTO GUIX Studio
description: Azure RTO GUIX è un pacchetto di qualità professionale, creato per soddisfare le esigenze degli sviluppatori di sistemi embedded.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 0d0ff37784673f851ab918e20b255d19ddf98b0f
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822997"
---
# <a name="overview-of-azure-rtos-guix-and-azure-rtos-guix-studio"></a><span data-ttu-id="a3479-103">Panoramica di Azure RTO GUIX e Azure RTO GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="a3479-103">Overview of Azure RTOS GUIX and Azure RTOS GUIX Studio</span></span>

<span data-ttu-id="a3479-104">L'interfaccia utente grafica di Azure GUIX Embedded è una soluzione GUI avanzata e industriale di Microsoft progettata appositamente per applicazioni molto incorporate e in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="a3479-104">Azure GUIX embedded GUI is Microsoft’s advanced, industrial grade GUI solution designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="a3479-105">Microsoft offre anche uno strumento di progettazione desktop WYSIWYG completo denominato Azure RTO GUIX studio, che consente agli sviluppatori di progettare l'interfaccia utente grafica sul desktop e generare codice GUI incorporato GUIX di Azure RTO che può quindi essere esportato nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="a3479-105">Microsoft also provides a full-featured WYSIWYG desktop design tool named Azure RTOS GUIX Studio, which allows developers to design their GUI on the desktop and generate Azure RTOS GUIX embedded GUI code that can then be exported to the target.</span></span> <span data-ttu-id="a3479-106">Azure RTO GUIX è completamente integrato con Azure RTO ThreadX RTO ed è disponibile per molti degli stessi processori supportati da Azure RTO ThreadX.</span><span class="sxs-lookup"><span data-stu-id="a3479-106">Azure RTOS GUIX is fully integrated with Azure RTOS ThreadX RTOS and is available for many of the same processors supported by Azure RTOS ThreadX.</span></span> <span data-ttu-id="a3479-107">Tutti questi componenti, combinati con un footprint estremamente ridotto, un'esecuzione rapida e una maggiore facilità d'uso, rendono Azure RTO GUIX la scelta ideale per le applicazioni per le cose incorporate più complesse che richiedono un'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="a3479-107">All of this combined with an extremely small footprint, fast execution, and superior ease-of-use, make Azure RTOS GUIX the ideal choice for the most demanding embedded IoT applications requiring a user interface.</span></span> 

## <a name="azure-rtos-guix-api"></a><span data-ttu-id="a3479-108">API GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="a3479-108">Azure RTOS GUIX API</span></span>

### <a name="intuitive-and-consistent-api"></a><span data-ttu-id="a3479-109">API intuitiva e coerente</span><span class="sxs-lookup"><span data-stu-id="a3479-109">Intuitive and consistent API</span></span>

* <span data-ttu-id="a3479-110">Sostantivo-convenzione di denominazione dei verbi</span><span class="sxs-lookup"><span data-stu-id="a3479-110">Noun-verb naming convention</span></span>

* <span data-ttu-id="a3479-111">Tutte le API hanno *gx_* principali per identificare facilmente come Azure RTO GUIX</span><span class="sxs-lookup"><span data-stu-id="a3479-111">All APIs have leading *gx_* to easily identify as Azure RTOS GUIX</span></span>

* <span data-ttu-id="a3479-112">Modello di programmazione basato sugli eventi (API)</span><span class="sxs-lookup"><span data-stu-id="a3479-112">Event-driven programming model (API)</span></span>

* <span data-ttu-id="a3479-113">Supporto completo per il disegno Canvas diretto quando necessario</span><span class="sxs-lookup"><span data-stu-id="a3479-113">Full support for direct canvas drawing when needed</span></span>

* <span data-ttu-id="a3479-114">Semplice interazione con il codice generato da Azure RTO GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="a3479-114">Simple to interact with Azure RTOS GUIX Studio generated code</span></span>

* <span data-ttu-id="a3479-115">API per line, Rectangle, Polygon e così via.</span><span class="sxs-lookup"><span data-stu-id="a3479-115">APIs for line, rectangle, polygon, etc.</span></span>

* <span data-ttu-id="a3479-116">API per Circle, Arc, Pie, Chord, ellisse e così via.</span><span class="sxs-lookup"><span data-stu-id="a3479-116">APIs for circle, arc, pie, chord, ellipse, etc.</span></span>

* <span data-ttu-id="a3479-117">API per il disegno e il posizionamento del testo</span><span class="sxs-lookup"><span data-stu-id="a3479-117">APIs for text drawing and positioning</span></span>

* <span data-ttu-id="a3479-118">Anti-aliasing, riempimenti di trama e riempimenti a tinta unita</span><span class="sxs-lookup"><span data-stu-id="a3479-118">Anti-aliasing, texture fills, and solid fills</span></span>

* <span data-ttu-id="a3479-119">API per la creazione e la modifica di schermate e widget</span><span class="sxs-lookup"><span data-stu-id="a3479-119">APIs for creating and modifing screens and widgets</span></span>

### <a name="azure-rtos-guix-studio-generated-files"></a><span data-ttu-id="a3479-120">File generati da Azure RTO GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="a3479-120">Azure RTOS GUIX Studio Generated Files</span></span>

* <span data-ttu-id="a3479-121">File di origine ANSI C generati automaticamente</span><span class="sxs-lookup"><span data-stu-id="a3479-121">Automatically generated ANSI C source files</span></span>

* <span data-ttu-id="a3479-122">Isola il software dell'applicazione dai dettagli del layout</span><span class="sxs-lookup"><span data-stu-id="a3479-122">Insulates application software from layout details</span></span>

* <span data-ttu-id="a3479-123">Include i tipi di carattere e le immagini richiesti dalla progettazione dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="a3479-123">Includes fonts and images required by UI design</span></span>

* <span data-ttu-id="a3479-124">File generati compilati con il codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a3479-124">Generated files compiled with application code</span></span>

* <span data-ttu-id="a3479-125">Il layout della schermata può essere aggiornato senza influire sulla logica dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a3479-125">Screen layout can be updated without affecting application logic</span></span>

* <span data-ttu-id="a3479-126">ID risorsa creare la lingua e l'indipendenza del tema</span><span class="sxs-lookup"><span data-stu-id="a3479-126">Resource IDs create language and theme independence</span></span>

* <span data-ttu-id="a3479-127">Funzioni di elaborazione di eventi e disegno personalizzato fornite dall'utente</span><span class="sxs-lookup"><span data-stu-id="a3479-127">User-supplied custom drawing and event processing functions</span></span>

### <a name="widget-library"></a><span data-ttu-id="a3479-128">Libreria widget</span><span class="sxs-lookup"><span data-stu-id="a3479-128">Widget library</span></span>

* <span data-ttu-id="a3479-129">Set predefinito ma personalizzabile di elementi di interfaccia comuni</span><span class="sxs-lookup"><span data-stu-id="a3479-129">Pre-defined but customizable set of common interface elements</span></span>

* <span data-ttu-id="a3479-130">Estremamente piccola, compatta ed efficiente</span><span class="sxs-lookup"><span data-stu-id="a3479-130">Extremely small, compact, and efficient</span></span>

* <span data-ttu-id="a3479-131">La libreria include pulsante, misuratore, elenco, finestra, scorrimento, dispositivo di scorrimento, indicatore di stato, messaggio di richiesta e molto altro</span><span class="sxs-lookup"><span data-stu-id="a3479-131">Library includes button, gauge, list, window, scroll, slider, progress bar, prompt and many more</span></span>

* <span data-ttu-id="a3479-132">Disegno e aspetto completamente personalizzabili</span><span class="sxs-lookup"><span data-stu-id="a3479-132">Fully customizable drawing and appearance</span></span>

* <span data-ttu-id="a3479-133">Operazioni completamente personalizzabili e gestione degli eventi</span><span class="sxs-lookup"><span data-stu-id="a3479-133">Fully customizable operation and event handling</span></span>

* <span data-ttu-id="a3479-134">Solo i widget usati sono collegati al software dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a3479-134">Only the widgets used are linked with application software</span></span>

### <a name="math-and-utilities"></a><span data-ttu-id="a3479-135">Matematica e utilità</span><span class="sxs-lookup"><span data-stu-id="a3479-135">Math and utilities</span></span>

* <span data-ttu-id="a3479-136">Funzioni per sin, cos, arcsin, ARccOS, tangente, radice quadrata</span><span class="sxs-lookup"><span data-stu-id="a3479-136">Functions for sin, cos, arcsin, arccos, tangent, square root</span></span>

* <span data-ttu-id="a3479-137">Funzioni per la modifica delle aree dello schermo</span><span class="sxs-lookup"><span data-stu-id="a3479-137">Functions for manipulating screen regions</span></span>

* <span data-ttu-id="a3479-138">Configurazione e avvio del sistema</span><span class="sxs-lookup"><span data-stu-id="a3479-138">System configuration and startup</span></span>

* <span data-ttu-id="a3479-139">Definizione del pool di memoria (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="a3479-139">Memory pool definition (optional)</span></span>

* <span data-ttu-id="a3479-140">Gestione timer</span><span class="sxs-lookup"><span data-stu-id="a3479-140">Timer Management</span></span>

* <span data-ttu-id="a3479-141">Gestione delle animazioni</span><span class="sxs-lookup"><span data-stu-id="a3479-141">Animation Management</span></span>

* <span data-ttu-id="a3479-142">Manutenzione elenco Dirty</span><span class="sxs-lookup"><span data-stu-id="a3479-142">Dirty list maintenance</span></span>

### <a name="image-processing"></a><span data-ttu-id="a3479-143">Elaborazione di immagini</span><span class="sxs-lookup"><span data-stu-id="a3479-143">Image processing</span></span>

* <span data-ttu-id="a3479-144">Funzioni per la decodifica di runtime di immagini JPEG e png</span><span class="sxs-lookup"><span data-stu-id="a3479-144">Functions for runtime decode of jpeg and png images</span></span>

* <span data-ttu-id="a3479-145">Applicare la conversione dello spazio colore e del rethering</span><span class="sxs-lookup"><span data-stu-id="a3479-145">Apply dithering and color space conversion</span></span>

* <span data-ttu-id="a3479-146">Rotazione dell'immagine</span><span class="sxs-lookup"><span data-stu-id="a3479-146">Image rotation</span></span>

* <span data-ttu-id="a3479-147">Ridimensionamento delle immagini</span><span class="sxs-lookup"><span data-stu-id="a3479-147">Image scaling</span></span>

* <span data-ttu-id="a3479-148">Blending immagini</span><span class="sxs-lookup"><span data-stu-id="a3479-148">Image blending</span></span>

### <a name="event-processing"></a><span data-ttu-id="a3479-149">Elaborazione di eventi</span><span class="sxs-lookup"><span data-stu-id="a3479-149">Event processing</span></span>

* <span data-ttu-id="a3479-150">Sospende automaticamente il thread GUIX di Azure RTO quando è inattivo</span><span class="sxs-lookup"><span data-stu-id="a3479-150">Automatically suspends Azure RTOS GUIX thread when idle</span></span>

* <span data-ttu-id="a3479-151">Modello di programmazione basato sugli eventi popolare nella progettazione dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="a3479-151">Event-driven programming model popular in UI design</span></span>

* <span data-ttu-id="a3479-152">Isola i driver di input dal thread di disegno GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="a3479-152">Insulates input drivers from Azure RTOS GUIX drawing thread</span></span>

* <span data-ttu-id="a3479-153">Funzioni per l'invio e la ricezione di eventi</span><span class="sxs-lookup"><span data-stu-id="a3479-153">Functions for sending and receiving events</span></span>

* <span data-ttu-id="a3479-154">Tipi di evento predefiniti per tutti i tipi di widget GUIX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="a3479-154">Pre-defined event types for all Azure RTOS GUIX widget types</span></span>

* <span data-ttu-id="a3479-155">Eventi personalizzati definiti dall'utente supportati</span><span class="sxs-lookup"><span data-stu-id="a3479-155">User-defined custom events supported</span></span>

### <a name="canvas-processing"></a><span data-ttu-id="a3479-156">Elaborazione Canvas</span><span class="sxs-lookup"><span data-stu-id="a3479-156">Canvas processing</span></span>

* <span data-ttu-id="a3479-157">Ritaglio e manutenzione degli ordini Z</span><span class="sxs-lookup"><span data-stu-id="a3479-157">Clipping and Z-Order maintenance</span></span>

* <span data-ttu-id="a3479-158">Isola la libreria widget dai dettagli hardware</span><span class="sxs-lookup"><span data-stu-id="a3479-158">Insulates widget library from hardware details</span></span>

* <span data-ttu-id="a3479-159">Isola l'applicazione dai dettagli dell'hardware</span><span class="sxs-lookup"><span data-stu-id="a3479-159">Insulates application from hardware details</span></span>

* <span data-ttu-id="a3479-160">Aggiornamento automatico in background di aree dirty</span><span class="sxs-lookup"><span data-stu-id="a3479-160">Automatic background refresh of dirty areas</span></span>

* <span data-ttu-id="a3479-161">Più Canvas con livelli e blending supportati</span><span class="sxs-lookup"><span data-stu-id="a3479-161">Multiple canvases with layering and blending supported</span></span>

* <span data-ttu-id="a3479-162">Può essere richiamato direttamente dal software dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a3479-162">Can be invoked directly by the application software</span></span>

### <a name="input-device-drivers"></a><span data-ttu-id="a3479-163">Driver/i dispositivo di input</span><span class="sxs-lookup"><span data-stu-id="a3479-163">Input device driver(s)</span></span>

* <span data-ttu-id="a3479-164">Supporto specifico dell'hardware, Azure RTO GUIX e applicazione isolata da dettagli hardware</span><span class="sxs-lookup"><span data-stu-id="a3479-164">Hardware-specific support, Azure RTOS GUIX and application insulated from hardware details</span></span>

* <span data-ttu-id="a3479-165">Tocco resistivo, perno sensibile e tastiera supportati</span><span class="sxs-lookup"><span data-stu-id="a3479-165">Resistive Touch, Cap Touch, and keypad supported</span></span>

* <span data-ttu-id="a3479-166">Eventi di input passati alla coda degli eventi di Azure RTO GUIX</span><span class="sxs-lookup"><span data-stu-id="a3479-166">Input events passed to Azure RTOS GUIX event queue</span></span>

### <a name="display-drivers"></a><span data-ttu-id="a3479-167">Visualizza driver</span><span class="sxs-lookup"><span data-stu-id="a3479-167">Display drivers</span></span>

* <span data-ttu-id="a3479-168">Supporto specifico dell'hardware</span><span class="sxs-lookup"><span data-stu-id="a3479-168">Hardware-specific support</span></span>

* <span data-ttu-id="a3479-169">Driver generici forniti per tutti i formati e la profondità di colore</span><span class="sxs-lookup"><span data-stu-id="a3479-169">Generic drivers provided for all color depth and formats</span></span>

* <span data-ttu-id="a3479-170">Personalizzata per l'utilizzo di acceleratori grafici disponibili</span><span class="sxs-lookup"><span data-stu-id="a3479-170">Customized to utilize available graphics accelerators</span></span>

### <a name="target-hardware"></a><span data-ttu-id="a3479-171">Hardware di destinazione</span><span class="sxs-lookup"><span data-stu-id="a3479-171">Target hardware</span></span>

* <span data-ttu-id="a3479-172">Quasi tutti i componenti hardware che supportano l'output grafico sono compatibili con GUIX</span><span class="sxs-lookup"><span data-stu-id="a3479-172">Nearly any hardware capable of graphical output Is compatible with GUIX</span></span>

* <span data-ttu-id="a3479-173">Sono supportate più visualizzazioni fisiche</span><span class="sxs-lookup"><span data-stu-id="a3479-173">Multiple physical displays supported</span></span>

* <span data-ttu-id="a3479-174">Requisiti minimi di RAM e Flash</span><span class="sxs-lookup"><span data-stu-id="a3479-174">Minimal RAM and Flash requirements</span></span>

## <a name="create-elegant-user-interfaces"></a><span data-ttu-id="a3479-175">Creare interfacce utente eleganti</span><span class="sxs-lookup"><span data-stu-id="a3479-175">Create Elegant User Interfaces</span></span>

<span data-ttu-id="a3479-176">Azure RTO GUIX e Azure RTO GUIX studio forniscono tutte le funzionalità necessarie per creare interfacce utente univocamente eleganti.</span><span class="sxs-lookup"><span data-stu-id="a3479-176">Azure RTOS GUIX and Azure RTOS GUIX Studio provide all the features necessary to create uniquely elegant user interfaces.</span></span> <span data-ttu-id="a3479-177">Il pacchetto standard Azure RTO GUIX include varie interfacce utente di esempio, tra cui un riferimento ai dispositivi medici, un riferimento a Smart Watch, un riferimento per l'automazione della casa, un riferimento al controllo industriale, un riferimento per l'automotive e diversi esempi di sprite e animazione.</span><span class="sxs-lookup"><span data-stu-id="a3479-177">The standard Azure RTOS GUIX package includes various sample user interfaces, including a medical device reference, a smart watch reference, a home automation reference, an industrial control reference, an automotive reference, and various sprite and animation examples.</span></span> <span data-ttu-id="a3479-178">Fare clic sugli esempi di riferimento illustrati di seguito.</span><span class="sxs-lookup"><span data-stu-id="a3479-178">Please click on the reference examples shown below.</span></span>

### <a name="home-automation"></a><span data-ttu-id="a3479-179">Automazione domestica</span><span class="sxs-lookup"><span data-stu-id="a3479-179">Home Automation</span></span>

<img alt="Screenshot of the GUIX home automation" class="img-responsive" src="./media/overview/guix_home_automation.png"/>

### <a name="medical"></a><span data-ttu-id="a3479-180">Medicina</span><span class="sxs-lookup"><span data-stu-id="a3479-180">Medical</span></span>

<img alt="Screenshot of the GUIX medical device" class="img-responsive" src="./media/overview/demo_guix_medical.png"/>

### <a name="consumer"></a><span data-ttu-id="a3479-181">Consumer</span><span class="sxs-lookup"><span data-stu-id="a3479-181">Consumer</span></span>

<img alt="Screenshot of the GUIX Consumer smart watch" class="img-responsive" src="./media/overview/demo_guix_smart_watch.png"/>

### <a name="white-goods"></a><span data-ttu-id="a3479-182">Beni bianchi</span><span class="sxs-lookup"><span data-stu-id="a3479-182">White Goods</span></span>

<img alt="Screenshot of the GUIX white goods exaample" class="img-responsive" src="./media/overview/demo_guix_white_goods.png"/>

### <a name="automotive"></a><span data-ttu-id="a3479-183">Automobilistico</span><span class="sxs-lookup"><span data-stu-id="a3479-183">Automotive</span></span>

<img alt="Screenshot of the GUIX automotive" class="img-responsive" src="./media/overview/demo_guix_infotainment.png"/>

### <a name="industrial"></a><span data-ttu-id="a3479-184">Industriale</span><span class="sxs-lookup"><span data-stu-id="a3479-184">Industrial</span></span>

<img alt="Screenshot of the GUIX industrial control" class="img-responsive" src="./media/overview/demo_guix_industrial.png"/>

<span data-ttu-id="a3479-185">Ogni riferimento GUIX di Azure RTO include un progetto di Azure RTO GUIX Studio corrispondente che definisce tutti gli elementi grafici della progettazione di riferimento.</span><span class="sxs-lookup"><span data-stu-id="a3479-185">Each Azure RTOS GUIX reference has a corresponding Azure RTOS GUIX Studio project that defines all the graphical elements of the reference design.</span></span> <span data-ttu-id="a3479-186">Modificare una progettazione di riferimento è facile.</span><span class="sxs-lookup"><span data-stu-id="a3479-186">Changing a reference design is easy.</span></span> <span data-ttu-id="a3479-187">È sufficiente aprire il progetto RTO GUIX di Azure corrispondente, apportare le modifiche desiderate, salvare il progetto e quindi selezionare *Project*.</span><span class="sxs-lookup"><span data-stu-id="a3479-187">Simply open the corresponding Azure RTOS GUIX project, make the desired changes, save the project, and then select *Project*.</span></span>

<span data-ttu-id="a3479-188">Generare tutti i file di output per generare il codice C per Azure RTO GUIX.</span><span class="sxs-lookup"><span data-stu-id="a3479-188">Generate All Output Files to generate the C code for Azure RTOS GUIX.</span></span> <span data-ttu-id="a3479-189">Quindi, è sufficiente ricompilare l'applicazione di destinazione ed eseguire per osservare la progettazione di riferimento modificata.</span><span class="sxs-lookup"><span data-stu-id="a3479-189">Then simply rebuild the target application and run to observe the modified reference design.</span></span>

### <a name="small-footprint"></a><span data-ttu-id="a3479-190">Footprint ridotto</span><span class="sxs-lookup"><span data-stu-id="a3479-190">Small-footprint</span></span>

<span data-ttu-id="a3479-191">Azure RTO GUIX ha un footprint minimo ristretto di 13,2 KB di RAM FLASH e 4KB per il supporto di base, senza includere la memoria necessaria per un'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="a3479-191">Azure RTOS GUIX has a remarkably small minimal footprint of 13.2KB of FLASH and 4KB RAM for basic support, not including the memory required for a canvas.</span></span>

<span data-ttu-id="a3479-192">Per una visualizzazione con la tecnologia di aggiornamento automatico e del grammo interno, non è necessaria alcuna memoria Canvas.</span><span class="sxs-lookup"><span data-stu-id="a3479-192">For a display with internal GRAM and self-refresh technology, no canvas memory is required.</span></span> <span data-ttu-id="a3479-193">Tuttavia, per migliorare le prestazioni di disegno o per una configurazione di visualizzazione che non utilizza la lingua locale per la visualizzazione, un'area di memoria Canvas viene definita dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a3479-193">However, to improve drawing performance, or for a display configuration that does not utilize GRAM local to the display, a canvas memory area is defined by the application.</span></span>

<span data-ttu-id="a3479-194">I requisiti di memoria di Canvas sono una funzione delle dimensioni dell'area di disegno, oltre alla profondità del colore, e sono definiti dalla formula:</span><span class="sxs-lookup"><span data-stu-id="a3479-194">Canvas memory requirements are a function of the canvas size as well as the color depth, and are defined by the formula:</span></span>

<span data-ttu-id="a3479-195"><i>RAM Canvas (byte) = (x \* y \* (BPP/8))</i></span><span class="sxs-lookup"><span data-stu-id="a3479-195"><i>Canvas RAM (bytes) = (x \* y \* (bpp/8))</i></span></span>

<span data-ttu-id="a3479-196">Dove "x" e "y" sono le dimensioni dell'area di disegno (visualizzazione).</span><span class="sxs-lookup"><span data-stu-id="a3479-196">Where “x” and “y” are the dimensions of the canvas (display).</span></span>

<span data-ttu-id="a3479-197">La maggior parte delle applicazioni usa anche risorse grafiche, che non sono incluse nei requisiti principali di archiviazione della libreria GUIX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="a3479-197">Most applications also utilize graphical resources, which are not included in the core Azure RTOS GUIX library storage requirements.</span></span> <span data-ttu-id="a3479-198">Queste risorse includono tipi di carattere, icone grafiche (pixelmaps) e stringhe statiche.</span><span class="sxs-lookup"><span data-stu-id="a3479-198">These resources include fonts, graphical icons (pixelmaps), and static strings.</span></span> <span data-ttu-id="a3479-199">Questi dati possono essere archiviati nella sezione memoria const (ad esempio, FLASH).</span><span class="sxs-lookup"><span data-stu-id="a3479-199">This data can be stored in the const memory section (i.e. FLASH).</span></span>

<span data-ttu-id="a3479-200">Le dimensioni di questa area di memoria dipendono da diversi fattori, tra cui il numero e le dimensioni dei tipi di carattere univoci usati, il numero e le dimensioni delle icone grafiche usate, il formato del colore di output e se ogni risorsa usa dati compressi, poiché Azure RTO GUIX supporta la compressione RLE dei dati di tipo carattere e Pixelmap.</span><span class="sxs-lookup"><span data-stu-id="a3479-200">The size of this memory area is dependent on a number of factors, including the number and size of unique fonts used, the number and size of the graphical icons used, the output color format, and whether or not each resource is using compressed data, since Azure RTOS GUIX supports RLE compression of both font and pixelmap data.</span></span> <span data-ttu-id="a3479-201">I requisiti di archiviazione per ogni risorsa vengono visualizzati nell'applicazione Azure RTO GUIX studio, consentendo all'utente di tenere traccia e monitorare la quantità di memoria flash che verrà usata dalle risorse dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a3479-201">The storage requirements for each resource are displayed within the Azure RTOS GUIX Studio application, allowing the user to track and monitor the amount of flash memory that will be consumed by the application resources.</span></span>

<span data-ttu-id="a3479-202">Come Azure RTO ThreadX, le dimensioni di Azure RTO GUIX vengono ridimensionate automaticamente in base ai servizi effettivamente usati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a3479-202">Like Azure RTOS ThreadX, the size of Azure RTOS GUIX automatically scales based on the services actually used by the application.</span></span> <span data-ttu-id="a3479-203">In questo modo si eliminano praticamente la necessità di complicati parametri di configurazione e di compilazione, semplificando le operazioni per lo sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="a3479-203">This virtually eliminates the need for complicated configuration and build parameters, making things easier for the developer.</span></span>

### <a name="fast-execution"></a><span data-ttu-id="a3479-204">Esecuzione rapida</span><span class="sxs-lookup"><span data-stu-id="a3479-204">Fast execution</span></span>

<span data-ttu-id="a3479-205">Azure RTO GUIX è scritto esclusivamente in C ed è progettato per la velocità.</span><span class="sxs-lookup"><span data-stu-id="a3479-205">Azure RTOS GUIX is written exclusively in C and is designed for speed.</span></span> <span data-ttu-id="a3479-206">Azure RTO GUIX ha un livello minimo di chiamata di funzione interna.</span><span class="sxs-lookup"><span data-stu-id="a3479-206">Azure RTOS GUIX has minimal internal function call layering.</span></span>

<span data-ttu-id="a3479-207">Inoltre, Azure RTO GUIX offre funzionalità ottimizzate di ritaglio, disegno e gestione degli eventi.</span><span class="sxs-lookup"><span data-stu-id="a3479-207">In addition, Azure RTOS GUIX provides optimized clipping, drawing, and event handling.</span></span> <span data-ttu-id="a3479-208">Tutti questi e una filosofia di progettazione orientata alle prestazioni generale consentono ad Azure RTO GUIX di ottenere le prestazioni più veloci possibile.</span><span class="sxs-lookup"><span data-stu-id="a3479-208">All of this and a general performance-oriented design philosophy help Azure RTOS GUIX achieve the fastest possible performance.</span></span>

### <a name="pre-certified--by-tuv-to-many-safety-standards"></a><span data-ttu-id="a3479-209">Pre-certificati da TUV a molti standard di sicurezza</span><span class="sxs-lookup"><span data-stu-id="a3479-209">Pre-certified  by TUV to many safety standards</span></span>

<span data-ttu-id="a3479-210">Azure RTO GUIX è stato certificato da SGS-TUV Saar per l'uso nei sistemi critici per la sicurezza, secondo IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 ASIL D e EN 50128.</span><span class="sxs-lookup"><span data-stu-id="a3479-210">Azure RTOS GUIX has been certified by SGS-TUV  Saar for use in safety-critical systems, according to IEC-61508 SIL 4, IEC-62304  SW Safety Class C, ISO 26262 ASIL D and EN 50128.</span></span> <span data-ttu-id="a3479-211">La certificazione conferma che Azure RTO GUIX può essere usato per lo sviluppo di software correlato alla sicurezza per i livelli di integrità di sicurezza più elevati di IEC-61508, IEC-62304, ISO 26262 e EN 50128 per la "protezione funzionale dei sistemi elettronici di sicurezza elettronica, elettronici e programmabili".</span><span class="sxs-lookup"><span data-stu-id="a3479-211">The certification confirms that Azure RTOS GUIX can be used in the development of safety-related software for the highest safety integrity levels of IEC-61508, IEC-62304, ISO 26262 and EN 50128 for the “Functional Safety of electrical, electronic, and programmable electronic safety-related systems.”</span></span> <span data-ttu-id="a3479-212">SGS-TUV Saar, formato da una joint venture del SGS-Group e del TUV della Germania, è diventato la società leader accreditata e indipendente per il test, il controllo, la verifica e la certificazione del software incorporato per i sistemi correlati alla sicurezza in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="a3479-212">SGS-TUV Saar, formed through a joint venture of Germany’s SGS-Group and TUV Saarland, has become the leading accredited, independent company for testing, auditing, verifying and certifying embedded software for safety-related systems worldwide.</span></span> <span data-ttu-id="a3479-213">Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, tra cui IEC-62304, ISO 26262 e EN 50128, vengono usati per garantire la protezione funzionale di dispositivi medicali elettrici, elettronici e programmabili per la sicurezza elettronica, sistemi di controllo dei processi, macchinari industriali, automobili e sistemi di controllo ferroviario.</span><span class="sxs-lookup"><span data-stu-id="a3479-213">The industrial safety standard IEC 61508, and all standards that are derived from it, including IEC-62304, ISO 26262 and EN 50128, are used to assure the functional safety of electrical, electronic, and programmable electronic safety-related medical devices, process control systems, industrial machinery, automobiles and railway control systems.</span></span>

<img alt="SGS-TUV Saar" class="img-responsive" src="https://rtos.com/wp-content/uploads/2017/10/partener-logo-sgs-tuv-saar-2.png"/>

#### <a name="simple-easy-to-use"></a><span data-ttu-id="a3479-214">Semplice e facile da usare</span><span class="sxs-lookup"><span data-stu-id="a3479-214">Simple, easy-to-use</span></span>

<span data-ttu-id="a3479-215">Azure RTO GUIX è molto semplice da usare e Azure RTO GUIX studio lo rende ancora più semplice consentendo agli sviluppatori di progettare visivamente sul desktop e generare codice C eseguito sulla destinazione effettiva.</span><span class="sxs-lookup"><span data-stu-id="a3479-215">Azure RTOS GUIX is very simple to use and Azure RTOS GUIX Studio makes it even easier by allowing developers to visually design on the desktop and generate C code that runs on the actual target.</span></span> <span data-ttu-id="a3479-216">Le applicazioni possono quindi aggiungere le proprie funzioni personalizzate di gestione e creazione degli eventi per completare l'interfaccia utente grafica.</span><span class="sxs-lookup"><span data-stu-id="a3479-216">Applications can then add their own custom event handling and drawing functions to complete their GUI.</span></span>

<span data-ttu-id="a3479-217">L'uso dell'API GUIX di Azure RTO è semplice.</span><span class="sxs-lookup"><span data-stu-id="a3479-217">Using the Azure RTOS GUIX API is straightforward.</span></span> <span data-ttu-id="a3479-218">L'API GUIX di Azure RTO è intuitiva e altamente funzionale.</span><span class="sxs-lookup"><span data-stu-id="a3479-218">The Azure RTOS GUIX API is both intuitive and highly functional.</span></span> <span data-ttu-id="a3479-219">I nomi delle API sono costituiti da parole reali e non dalla "zuppa alfabetica" e/o dai nomi molto abbreviati che sono così comuni in altri prodotti file system.</span><span class="sxs-lookup"><span data-stu-id="a3479-219">The API names are made of real words and not the “alphabet soup” and/or the highly abbreviated names that are so common in other file system products.</span></span> <span data-ttu-id="a3479-220">Tutte le API GUIX di Azure RTO hanno un *gx_* leader e seguono una convenzione di denominazione sostantivo-verbo.</span><span class="sxs-lookup"><span data-stu-id="a3479-220">All Azure RTOS GUIX APIs have a leading *gx_* and follow a noun-verb naming convention.</span></span> <span data-ttu-id="a3479-221">Inoltre, esiste una coerenza funzionale nell'API.</span><span class="sxs-lookup"><span data-stu-id="a3479-221">Furthermore, there is a functional consistency throughout the API.</span></span> <span data-ttu-id="a3479-222">Ad esempio, tutte le API che inizializzano un blocco di controllo widget sono denominate &lt; widget_type &gt; _create e i parametri create function per ogni tipo di widget sono sempre definiti nello stesso ordine.</span><span class="sxs-lookup"><span data-stu-id="a3479-222">For example, all APIs that initialize a widget control block are named &lt; widget_type&gt;_create, and the create function parameters for each widget type are always defined in the same order.</span></span>

### <a name="comprehensive-set-of-built-in-widgets"></a><span data-ttu-id="a3479-223">Set completo di widget predefiniti</span><span class="sxs-lookup"><span data-stu-id="a3479-223">Comprehensive set of built-in widgets</span></span>

* <span data-ttu-id="a3479-224">Azure RTO GUIX offre un set completo di widget predefiniti, tra cui:</span><span class="sxs-lookup"><span data-stu-id="a3479-224">Azure RTOS GUIX provides a rich set of built-in widgets, including:</span></span>

* <span data-ttu-id="a3479-225">Menu Accordion</span><span class="sxs-lookup"><span data-stu-id="a3479-225">Accordion Menu</span></span>

* <span data-ttu-id="a3479-226">Pulsante</span><span class="sxs-lookup"><span data-stu-id="a3479-226">Button</span></span>

* <span data-ttu-id="a3479-227">Casella di controllo</span><span class="sxs-lookup"><span data-stu-id="a3479-227">Checkbox</span></span>

* <span data-ttu-id="a3479-228">Misuratore circolare</span><span class="sxs-lookup"><span data-stu-id="a3479-228">Circular Gauge</span></span>

* <span data-ttu-id="a3479-229">Elenco a discesa</span><span class="sxs-lookup"><span data-stu-id="a3479-229">Drop Down List</span></span>

* <span data-ttu-id="a3479-230">Elenco orizzontale</span><span class="sxs-lookup"><span data-stu-id="a3479-230">Horizontal List</span></span>

* <span data-ttu-id="a3479-231">Finestra barra di scorrimento orizzontale</span><span class="sxs-lookup"><span data-stu-id="a3479-231">Horizontal Scrollbar Window</span></span>

* <span data-ttu-id="a3479-232">Icona</span><span class="sxs-lookup"><span data-stu-id="a3479-232">Icon</span></span>

* <span data-ttu-id="a3479-233">Pulsante icona</span><span class="sxs-lookup"><span data-stu-id="a3479-233">Icon Button</span></span>

* <span data-ttu-id="a3479-234">Grafico a linee</span><span class="sxs-lookup"><span data-stu-id="a3479-234">Line Chart</span></span>

* <span data-ttu-id="a3479-235">Menu</span><span class="sxs-lookup"><span data-stu-id="a3479-235">Menu</span></span>

* <span data-ttu-id="a3479-236">Pulsante testo su più righe</span><span class="sxs-lookup"><span data-stu-id="a3479-236">Multi Line Text Button</span></span>

* <span data-ttu-id="a3479-237">Input di testo multilinea</span><span class="sxs-lookup"><span data-stu-id="a3479-237">Multi Line Text Input</span></span>

* <span data-ttu-id="a3479-238">Visualizzazione testo su più righe</span><span class="sxs-lookup"><span data-stu-id="a3479-238">Multi Line Text View</span></span>

* <span data-ttu-id="a3479-239">Richiesta Pixelmap numerica</span><span class="sxs-lookup"><span data-stu-id="a3479-239">Numeric Pixelmap Prompt</span></span>

* <span data-ttu-id="a3479-240">Prompt numerico</span><span class="sxs-lookup"><span data-stu-id="a3479-240">Numeric Prompt</span></span>

* <span data-ttu-id="a3479-241">Rotellina di scorrimento numerica</span><span class="sxs-lookup"><span data-stu-id="a3479-241">Numeric Scroll Wheel</span></span>

* <span data-ttu-id="a3479-242">Pulsante pixelmap</span><span class="sxs-lookup"><span data-stu-id="a3479-242">Pixelmap Button</span></span>

* <span data-ttu-id="a3479-243">Prompt pixelmap</span><span class="sxs-lookup"><span data-stu-id="a3479-243">Pixelmap Prompt</span></span>

* <span data-ttu-id="a3479-244">Dispositivo di scorrimento pixelmap</span><span class="sxs-lookup"><span data-stu-id="a3479-244">Pixelmap Slider</span></span>

* <span data-ttu-id="a3479-245">Sprite pixelmap</span><span class="sxs-lookup"><span data-stu-id="a3479-245">Pixelmap Sprite</span></span>

* <span data-ttu-id="a3479-246">ProgressBar</span><span class="sxs-lookup"><span data-stu-id="a3479-246">Progress Bar</span></span>

* <span data-ttu-id="a3479-247">Prompt</span><span class="sxs-lookup"><span data-stu-id="a3479-247">Prompt</span></span>

* <span data-ttu-id="a3479-248">Indicatore di stato radiale</span><span class="sxs-lookup"><span data-stu-id="a3479-248">Radial Progress Bar</span></span>

* <span data-ttu-id="a3479-249">RadioButton</span><span class="sxs-lookup"><span data-stu-id="a3479-249">Radio Button</span></span>

* <span data-ttu-id="a3479-250">Rotellina di scorrimento</span><span class="sxs-lookup"><span data-stu-id="a3479-250">Scroll Wheel</span></span>

* <span data-ttu-id="a3479-251">Input di testo a riga singola</span><span class="sxs-lookup"><span data-stu-id="a3479-251">Single Line Text Input</span></span>

* <span data-ttu-id="a3479-252">Slider</span><span class="sxs-lookup"><span data-stu-id="a3479-252">Slider</span></span>

* <span data-ttu-id="a3479-253">Rotellina di scorrimento stringa</span><span class="sxs-lookup"><span data-stu-id="a3479-253">String Scroll Wheel</span></span>

* <span data-ttu-id="a3479-254">Pulsante testo</span><span class="sxs-lookup"><span data-stu-id="a3479-254">Text Button</span></span>

* <span data-ttu-id="a3479-255">Visualizzazione ad albero</span><span class="sxs-lookup"><span data-stu-id="a3479-255">Tree View</span></span>

* <span data-ttu-id="a3479-256">Elenco verticale</span><span class="sxs-lookup"><span data-stu-id="a3479-256">Vertical List</span></span>

* <span data-ttu-id="a3479-257">Barra di scorrimento verticale</span><span class="sxs-lookup"><span data-stu-id="a3479-257">Vertical Scrollbar</span></span>

<span data-ttu-id="a3479-258">È facile per l'applicazione creare anche i propri widget dei clienti.</span><span class="sxs-lookup"><span data-stu-id="a3479-258">It’s easy for the application to create its own customer widgets as well.</span></span>

### <a name="complete-low-level-drawing-api"></a><span data-ttu-id="a3479-259">API di disegno di basso livello completa</span><span class="sxs-lookup"><span data-stu-id="a3479-259">Complete low-level drawing API</span></span>

<span data-ttu-id="a3479-260">Azure RTO GUIX offre un'affidabile API di disegno Canvas, che consente all'applicazione di eseguire il rendering di forme grafiche complesse.</span><span class="sxs-lookup"><span data-stu-id="a3479-260">Azure RTOS GUIX provides a robust canvas drawing API, allowing the application to render complex graphical shapes.</span></span>

<span data-ttu-id="a3479-261">Tutte le funzioni supportano l'anti-aliasing su destinazioni di profondità dei colori elevate e tutte le forme possono essere riempite con la struttura, inclusi i riempimenti a tinta unita e Pixelmap.</span><span class="sxs-lookup"><span data-stu-id="a3479-261">All functions support anti-aliasing on high color depth targets, and all shapes can be filled our outlined, including solid and pixelmap pattern fills.</span></span> <span data-ttu-id="a3479-262">Tutte le primitive di disegno supportano il pennello alfa quando viene eseguito a 16 BPP e una profondità di colore superiore.</span><span class="sxs-lookup"><span data-stu-id="a3479-262">All drawing primitives support brush alpha when running at 16 bpp and higher color depth.</span></span> <span data-ttu-id="a3479-263">Le funzioni di disegno includono:</span><span class="sxs-lookup"><span data-stu-id="a3479-263">Drawing functions include:</span></span>

* <span data-ttu-id="a3479-264">Arco di estrazione</span><span class="sxs-lookup"><span data-stu-id="a3479-264">Arc Draw</span></span>

* <span data-ttu-id="a3479-265">Cerchio disegnato</span><span class="sxs-lookup"><span data-stu-id="a3479-265">Circle Draw</span></span>

* <span data-ttu-id="a3479-266">Linea di estrazione</span><span class="sxs-lookup"><span data-stu-id="a3479-266">Line Draw</span></span>

* <span data-ttu-id="a3479-267">Grafico a torta</span><span class="sxs-lookup"><span data-stu-id="a3479-267">Pie Draw</span></span>

* <span data-ttu-id="a3479-268">Pixelmap Blend</span><span class="sxs-lookup"><span data-stu-id="a3479-268">Pixelmap Blend</span></span>

* <span data-ttu-id="a3479-269">Riquadro pixelmap</span><span class="sxs-lookup"><span data-stu-id="a3479-269">Pixelmap Tile</span></span>

* <span data-ttu-id="a3479-270">Poligono di disegni</span><span class="sxs-lookup"><span data-stu-id="a3479-270">Polygon Draw</span></span>

* <span data-ttu-id="a3479-271">Testo disegnato</span><span class="sxs-lookup"><span data-stu-id="a3479-271">Text Draw</span></span>

* <span data-ttu-id="a3479-272">Accordo di estrazione</span><span class="sxs-lookup"><span data-stu-id="a3479-272">Chord Draw</span></span>

* <span data-ttu-id="a3479-273">Disegni ellissi</span><span class="sxs-lookup"><span data-stu-id="a3479-273">Ellipse Draw</span></span>

* <span data-ttu-id="a3479-274">Pixel di estrazione</span><span class="sxs-lookup"><span data-stu-id="a3479-274">Pixel Draw</span></span>

* <span data-ttu-id="a3479-275">Pixelmap-disegni</span><span class="sxs-lookup"><span data-stu-id="a3479-275">Pixelmap Draw</span></span>

* <span data-ttu-id="a3479-276">Pixelmap ruota</span><span class="sxs-lookup"><span data-stu-id="a3479-276">Pixelmap Rotate</span></span>

* <span data-ttu-id="a3479-277">Rettangolo di estrazione</span><span class="sxs-lookup"><span data-stu-id="a3479-277">Rectangle Draw</span></span>

* <span data-ttu-id="a3479-278">Blend di testo</span><span class="sxs-lookup"><span data-stu-id="a3479-278">Text Blend</span></span>

### <a name="default-free-fonts-and-easy-to-add-more"></a><span data-ttu-id="a3479-279">Tipi di carattere gratuiti predefiniti e semplicità di aggiunta</span><span class="sxs-lookup"><span data-stu-id="a3479-279">Default free fonts and easy to add more</span></span>

<span data-ttu-id="a3479-280">Azure RTO GUIX offre un set gratuito di tipi di carattere TrueType.</span><span class="sxs-lookup"><span data-stu-id="a3479-280">Azure RTOS GUIX provides a free set of TrueType fonts.</span></span> <span data-ttu-id="a3479-281">Gli sviluppatori possono aggiungere altri tipi di carattere TrueType nel modo desiderato.</span><span class="sxs-lookup"><span data-stu-id="a3479-281">Developers can add additional TrueType fonts as desired.</span></span>

<span data-ttu-id="a3479-282">Il formato del tipo di carattere GUIX di Azure RTO supporta l'anti-aliasing 8bpp, l'anti-aliasing di 4bpp e i tipi di carattere monocromatico 1bpp.</span><span class="sxs-lookup"><span data-stu-id="a3479-282">The Azure RTOS GUIX font format supports 8bpp anti-aliasing, 4bpp anti-aliasing, and 1bpp monochrome fonts.</span></span> <span data-ttu-id="a3479-283">Per la maggior parte delle applicazioni con vincoli di risorse, Azure RTO GUIX pre-esegue il rendering dei tipi di carattere TrueType in un formato bitmap compresso usando lo strumento desktop di GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="a3479-283">For the most resource-constrained applications, Azure RTOS GUIX pre-renders the TrueType fonts to a compressed bitmap format using our GUIX Studio desktop tool.</span></span>

### <a name="custom-jpg-and-png-decoder-implementation"></a><span data-ttu-id="a3479-284">Implementazione del decodificatore JPG personalizzato e PNG</span><span class="sxs-lookup"><span data-stu-id="a3479-284">Custom JPG and PNG decoder implementation</span></span>

<span data-ttu-id="a3479-285">Implementazione del decodificatore jpg e png del decodificatore JPG e PNG personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a3479-285">Custom JPG and PNG decoder implementation JPG and PNG file decoder implementation.</span></span> <span data-ttu-id="a3479-286">Questa implementazione supporta la conversione dello spazio colore, la dithering e la creazione di runtime di immagini in formato Pixelmap compatibili con GUIX di Azure RTO.</span><span class="sxs-lookup"><span data-stu-id="a3479-286">This implementation supports color space conversion, dithering, and runtime creation of Azure RTOS GUIX-compatible pixelmap format images.</span></span>

### <a name="extensive-display-and-touchscreen-support"></a><span data-ttu-id="a3479-287">Supporto completo per schermo e touchscreen</span><span class="sxs-lookup"><span data-stu-id="a3479-287">Extensive display and touchscreen support</span></span>

<span data-ttu-id="a3479-288">Azure RTO GUIX offre driver di visualizzazione generici per quasi tutti i formati di colore, tra cui 1bpp monocromatico, 8 BPP tavolozza, 8 BPP 3:3:2 formato</span><span class="sxs-lookup"><span data-stu-id="a3479-288">Azure RTOS GUIX provides generic display drivers for nearly all color formats, including 1bpp monochrome, 8 bpp palette, 8 bpp 3:3:2 format,</span></span>

<span data-ttu-id="a3479-289">16 BPP 565, formato RGB, 16 BPP 4:4:4:4, 32 BPP x:r: g:b format e 32 BPP a:r: g:b format.</span><span class="sxs-lookup"><span data-stu-id="a3479-289">16 bpp 565 rgb format, 16 bpp 4:4:4:4 format, 32 bpp x:r:g:b format, and 32 bpp a:r:g:b format.</span></span> <span data-ttu-id="a3479-290">Inoltre, Azure RTO GUIX è integrato con molti dei più diffusi controller LCD e acceleratori hardware (ST ChromeArt, Renesas Synergy e così via).</span><span class="sxs-lookup"><span data-stu-id="a3479-290">In addition, Azure RTOS GUIX is integrated with many of the most popular LCD controllers and hardware accelerators (ST ChromeArt, Renesas Synergy, etc.).</span></span>

<span data-ttu-id="a3479-291">Azure RTO GUIX supporta completamente il touchscreen (incluso il supporto per il movimento), la penna e i dispositivi di input della tastiera virtuale.</span><span class="sxs-lookup"><span data-stu-id="a3479-291">Azure RTOS GUIX fully supports touchscreen (including gesture support), pen, and virtual keyboard input devices.</span></span>

### <a name="azure-rtos-guix-studio-desktop-wysiwyg-tool"></a><span data-ttu-id="a3479-292">Strumento WYSIWYG di Azure RTO GUIX Studio Desktop</span><span class="sxs-lookup"><span data-stu-id="a3479-292">Azure RTOS GUIX Studio desktop WYSIWYG tool</span></span>

<span data-ttu-id="a3479-293">Azure RTO GUIX Studio fornisce un ambiente di progettazione della schermata WYSIWYG completo che consente all'utente di trascinare e rilasciare elementi grafici usati per creare le schermate dell'interfaccia utente grafica.</span><span class="sxs-lookup"><span data-stu-id="a3479-293">Azure RTOS GUIX Studio provides a complete WYSIWYG screen design environment which allows the user to drag-and-drop graphical elements used to build the GUI screens.</span></span> <span data-ttu-id="a3479-294">Azure RTO GUIX Studio genera automaticamente il codice C compatibile con la libreria RTO GUIX di Azure, pronto per essere compilato ed eseguito nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="a3479-294">Azure RTOS GUIX Studio automatically generates C code compatible with the Azure RTOS GUIX library, ready to be compiled and run on the target.</span></span> <span data-ttu-id="a3479-295">Gli sviluppatori possono produrre tipi di carattere pre-rendering da usare all'interno di un'applicazione usando lo strumento integrato di generazione dei caratteri di Azure RTO GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="a3479-295">Developers can produce pre-rendered fonts for use within an application using the integrated Azure RTOS GUIX Studio font generation tool.</span></span> <span data-ttu-id="a3479-296">I tipi di carattere possono essere generati in formati monocromatici o anti-alias e sono ottimizzati per risparmiare spazio nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="a3479-296">Fonts can be generated in monochrome or anti-aliased formats, and are optimized to save space on the target.</span></span> <span data-ttu-id="a3479-297">I tipi di carattere possono includere qualsiasi set di caratteri, inclusi i caratteri Unicode per le applicazioni multilingue.</span><span class="sxs-lookup"><span data-stu-id="a3479-297">Fonts can include any set of characters, including Unicode characters for multi-lingual applications.</span></span>

<img alt="Diagram of SGS-TUV Saar certification logo" class="alignnone size-full wp-image-1500" height="341" sizes="(max-width: 535px) 100vw, 535px" src="./media/overview/studio_screen_shot.png"/>

<span data-ttu-id="a3479-298">Azure RTO GUIX Studio semplifica l'importazione di elementi grafici da file PNG o JPG con conversione in Azure RTO GUIX compresso da usare nel sistema di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a3479-298">Azure RTOS GUIX Studio facilitates the import of graphics from PNG or JPG files with conversion to compressed Azure RTOS GUIX Pixelmaps for use on the target system.</span></span> <span data-ttu-id="a3479-299">Molti dei tipi di widget GUIX di Azure RTO sono progettati per incorporare grafica utente per un aspetto personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a3479-299">Many of the Azure RTOS GUIX widget types are designed to incorporate user graphics for a custom look and feel.</span></span> <span data-ttu-id="a3479-300">Inoltre, Azure RTO GUIX Studio consente la personalizzazione dei colori predefiniti e degli stili di disegno usati dai widget GUIX di Azure RTO, consentendo agli sviluppatori di ottimizzare l'aspetto di Azure RTO GUIX in modo molto semplice.</span><span class="sxs-lookup"><span data-stu-id="a3479-300">In addition, Azure RTOS GUIX Studio allows customization of the default colors and drawing styles used by the Azure RTOS GUIX widgets, allowing developers to tune the appearance of Azure RTOS GUIX very easily.</span></span> <span data-ttu-id="a3479-301">La generazione e la gestione delle stringhe dell'applicazione sono un'altra funzionalità incorporata di Azure RTO GUIX Studio.</span><span class="sxs-lookup"><span data-stu-id="a3479-301">Generation and maintenance of application strings is another built-in facility of Azure RTOS GUIX Studio.</span></span> <span data-ttu-id="a3479-302">Ciò consente agli sviluppatori di progettare un'applicazione usando un linguaggio per lo sviluppo e di aggiungere in modo rapido e semplice il supporto per altre lingue dopo il rilascio del prodotto.</span><span class="sxs-lookup"><span data-stu-id="a3479-302">This enables developers to design an application using one language for developing, and quickly and easily add support for additional languages after the product is released.</span></span> <span data-ttu-id="a3479-303">Un'applicazione Azure RTO GUIX completa può essere eseguita su un desktop PC all'interno dell'ambiente Azure RTO GUIX studio, consentendo una generazione rapida e semplice di concetti di GUI, test dei flussi dello schermo e osservazione delle transizioni e delle animazioni dello schermo.</span><span class="sxs-lookup"><span data-stu-id="a3479-303">A complete Azure RTOS GUIX application can be executed on a PC desktop within the Azure RTOS GUIX Studio environment, allowing a quick and easy generation and demonstration of GUI concepts, testing of screen flows, and observation of screen transitions and animations.</span></span> <span data-ttu-id="a3479-304">Al termine, una progettazione può essere esportata come strutture di dati C pronte per la destinazione, pronta per essere compilata e collegata con le librerie di Azure RTO GUIX e Azure RTO ThreadX.</span><span class="sxs-lookup"><span data-stu-id="a3479-304">When completed, a design can be exported as target-ready C data structures, ready to be compiled and linked with the Azure RTOS GUIX and Azure RTOS ThreadX libraries.</span></span>

<span data-ttu-id="a3479-305">Azure RTO GUIX e Azure RTO GUIX Studio supportano più temi di risorse, consentendo a un'applicazione di essere facilmente Riskin in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a3479-305">Azure RTOS GUIX and Azure RTOS GUIX Studio support multiple resource themes, allowing an application to be easily reskinned at run-time.</span></span> <span data-ttu-id="a3479-306">I tipi di carattere, i colori e pixelmaps possono essere modificati in fase di esecuzione con una semplice API.</span><span class="sxs-lookup"><span data-stu-id="a3479-306">Fonts, colors, and pixelmaps can be changed at run-time with one simple API.</span></span>

<span data-ttu-id="a3479-307">Scopri di più su GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="a3479-307">Learn more about GUIX Studio</span></span>

### <a name="complete-win32-simulation"></a><span data-ttu-id="a3479-308">Completa simulazione Win32</span><span class="sxs-lookup"><span data-stu-id="a3479-308">Complete Win32 simulation</span></span>

<span data-ttu-id="a3479-309">Azure RTO GUIX viene eseguito in un PC Windows, usando esattamente la stessa libreria di disegno eseguita sulla lavagna di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a3479-309">Azure RTOS GUIX runs on a Windows PC, using exactly the same drawing library that runs on the target board.</span></span> <span data-ttu-id="a3479-310">Con Azure RTO GUIX è possibile compilare ed eseguire un'applicazione GUI sul PC e usare lo stesso codice dell'applicazione nella destinazione per il debug, la creazione rapida di prototipi, la dimostrazione e l'operazione di destinazione WYSIWYG.</span><span class="sxs-lookup"><span data-stu-id="a3479-310">With Azure RTOS GUIX, you can build and run a GUI application on the PC, and use the same application code on your target for debugging, rapid prototyping, demonstration, and WYSIWYG target operation.</span></span>

### <a name="advanced-technology"></a><span data-ttu-id="a3479-311">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="a3479-311">Advanced technology</span></span>

* <span data-ttu-id="a3479-312">La tecnologia avanzata di Azure RTO GUIX è incorporata:</span><span class="sxs-lookup"><span data-stu-id="a3479-312">Azure RTOS GUIX's advanced technology incorporates:</span></span>

* <span data-ttu-id="a3479-313">Fusione alfa</span><span class="sxs-lookup"><span data-stu-id="a3479-313">Alpha blending</span></span>

* <span data-ttu-id="a3479-314">Anti-aliasing</span><span class="sxs-lookup"><span data-stu-id="a3479-314">Anti-Aliasing</span></span>

* <span data-ttu-id="a3479-315">Scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="a3479-315">Automatic scaling</span></span>

* <span data-ttu-id="a3479-316">Compressione bitmap</span><span class="sxs-lookup"><span data-stu-id="a3479-316">Bitmap compression</span></span>

* <span data-ttu-id="a3479-317">Blending Canvas</span><span class="sxs-lookup"><span data-stu-id="a3479-317">Canvas blending</span></span>

* <span data-ttu-id="a3479-318">Supporto widget personalizzato</span><span class="sxs-lookup"><span data-stu-id="a3479-318">Custom widget support</span></span>

* <span data-ttu-id="a3479-319">Supporto per disegno posticipato</span><span class="sxs-lookup"><span data-stu-id="a3479-319">Deferred drawing support</span></span>

* <span data-ttu-id="a3479-320">Supporto di rethering</span><span class="sxs-lookup"><span data-stu-id="a3479-320">Dithering support</span></span>

* <span data-ttu-id="a3479-321">Programmazione neutra endian</span><span class="sxs-lookup"><span data-stu-id="a3479-321">Endian neutral programming</span></span>

* <span data-ttu-id="a3479-322">Supporto dell'acceleratore hardware</span><span class="sxs-lookup"><span data-stu-id="a3479-322">Hardware accelerator support</span></span>

* <span data-ttu-id="a3479-323">Supporto multilingue e codifica UTF-8</span><span class="sxs-lookup"><span data-stu-id="a3479-323">Multilingual support and UTF-8 encoding</span></span>

* <span data-ttu-id="a3479-324">Supporto per più visualizzazioni e Canvas</span><span class="sxs-lookup"><span data-stu-id="a3479-324">Multiple display and canvas support</span></span>

* <span data-ttu-id="a3479-325">Ritaglio ottimizzato, disegno e gestione degli eventi</span><span class="sxs-lookup"><span data-stu-id="a3479-325">Optimized clipping, drawing, and event handling</span></span>

* <span data-ttu-id="a3479-326">Runtime JPEG e PNG Decoder</span><span class="sxs-lookup"><span data-stu-id="a3479-326">Runtime JPEG and PNG decoder</span></span>

* <span data-ttu-id="a3479-327">Personalizzazione e temi</span><span class="sxs-lookup"><span data-stu-id="a3479-327">Skinning and Themes</span></span>

* <span data-ttu-id="a3479-328">Supporta la monocromia tramite il colore reale a 32 bit con formati di grafica Alpha</span><span class="sxs-lookup"><span data-stu-id="a3479-328">Supports monochrome through 32-bit true-color with alpha graphics formats</span></span>

* <span data-ttu-id="a3479-329">Transizioni, sprite e supporto per animazioni</span><span class="sxs-lookup"><span data-stu-id="a3479-329">Transitions, Sprites, and Animation support</span></span>

* <span data-ttu-id="a3479-330">Simulazione Win32</span><span class="sxs-lookup"><span data-stu-id="a3479-330">Win32 simulation</span></span>

* <span data-ttu-id="a3479-331">Gestione delle finestre, inclusi i viewport e la manutenzione degli ordini Z</span><span class="sxs-lookup"><span data-stu-id="a3479-331">Window management including Viewports and Z-order maintenance</span></span>

### <a name="fastest-time-to-market"></a><span data-ttu-id="a3479-332">Time-to-market più veloce</span><span class="sxs-lookup"><span data-stu-id="a3479-332">Fastest time-to-market</span></span>

<span data-ttu-id="a3479-333">Azure RTO GUIX è facile da installare, apprendere, usare, eseguire il debug, verificare, certificare e gestire.</span><span class="sxs-lookup"><span data-stu-id="a3479-333">Azure RTOS GUIX is easy to install, learn, use, debug, verify, certify and maintain.</span></span> <span data-ttu-id="a3479-334">Azure RTO GUIX Studio consente anche di semplificare la progettazione e l'implementazione di GUI embedded.</span><span class="sxs-lookup"><span data-stu-id="a3479-334">Azure RTOS GUIX Studio also helps making embedded GUI design and implementation easier.</span></span> <span data-ttu-id="a3479-335">Di conseguenza, Azure RTO GUIX è una delle soluzioni GUI più diffuse per i dispositivi it incorporati.</span><span class="sxs-lookup"><span data-stu-id="a3479-335">As a result, Azure RTOS GUIX is one of the most popular GUI solutions for embedded IoT devices.</span></span> <span data-ttu-id="a3479-336">Il nostro vantaggio di time-to-Market coerente è basato su:</span><span class="sxs-lookup"><span data-stu-id="a3479-336">Our consistent time-to-market advantage is built on:</span></span>

* <span data-ttu-id="a3479-337">Documentazione sulla qualità: esaminare la [Guida dell'utente di Azure RTO GUIX](about-guix.md) e vedere per se stessi.</span><span class="sxs-lookup"><span data-stu-id="a3479-337">Quality Documentation – please review our [Azure RTOS GUIX User Guide](about-guix.md) and see for yourself!</span></span>

* <span data-ttu-id="a3479-338">Disponibilità del codice sorgente completa</span><span class="sxs-lookup"><span data-stu-id="a3479-338">Complete Source Code Availability</span></span>

* <span data-ttu-id="a3479-339">API di facile utilizzo</span><span class="sxs-lookup"><span data-stu-id="a3479-339">Easy-to-use API</span></span>

* <span data-ttu-id="a3479-340">Set di funzionalità completo e avanzato</span><span class="sxs-lookup"><span data-stu-id="a3479-340">Comprehensive and Advanced Feature Set</span></span>

## <a name="one-simple-license"></a><span data-ttu-id="a3479-341">Una licenza semplice</span><span class="sxs-lookup"><span data-stu-id="a3479-341">One Simple License</span></span>

<span data-ttu-id="a3479-342">Non è previsto alcun costo per l'uso e il test del codice sorgente e nessun costo per le licenze di produzione quando viene distribuito in dispositivi con licenza preliminare, tutti gli altri dispositivi necessitano di una licenza annuale semplice.</span><span class="sxs-lookup"><span data-stu-id="a3479-342">There is no cost to use and test the source code and no cost for production licenses when deployed to pre-licensed devices, all other devices need a simple annual license.</span></span>

## <a name="full-highest-quality-source-code"></a><span data-ttu-id="a3479-343">Codice sorgente completo di qualità elevata</span><span class="sxs-lookup"><span data-stu-id="a3479-343">Full, highest-quality source code</span></span>

<span data-ttu-id="a3479-344">Nel corso degli anni, il codice sorgente NetX di Azure RTO ha impostato la qualità e la facilità di comprensione.</span><span class="sxs-lookup"><span data-stu-id="a3479-344">Throughout the years, Azure RTOS NetX source code has set the bar in quality and ease of understanding.</span></span> <span data-ttu-id="a3479-345">Inoltre, la convenzione relativa alla presenza di una funzione per ogni file fornisce una semplice navigazione all'origine.</span><span class="sxs-lookup"><span data-stu-id="a3479-345">In addition, the convention of having one function per file provides for easy source navigation.</span></span>

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="a3479-346">Supporta le architetture più diffuse</span><span class="sxs-lookup"><span data-stu-id="a3479-346">Supports most popular architectures</span></span>

<span data-ttu-id="a3479-347">Azure RTO GUIX viene eseguito sui microprocessori più diffusi a 32/64 bit, predefiniti, completamente testati e completamente supportati, inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="a3479-347">Azure RTOS GUIX runs on most popular 32/64-bit microprocessors, out-of-the-box, fully tested and fully supported, including the following:</span></span>

<span data-ttu-id="a3479-348">Architetture avanzate:</span><span class="sxs-lookup"><span data-stu-id="a3479-348">Advanced Architectures:</span></span>

<span data-ttu-id="a3479-349">**Dispositivi analoghi**: SHARC, Blackfin, CM4xx</span><span class="sxs-lookup"><span data-stu-id="a3479-349">**Analog Devices**: SHARC, Blackfin, CM4xx</span></span>

<span data-ttu-id="a3479-350">**Andina Core**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="a3479-350">**Andes Core**: RISC-V</span></span>

<span data-ttu-id="a3479-351">**Ambiqmicro**: Apollo MCU</span><span class="sxs-lookup"><span data-stu-id="a3479-351">**Ambiqmicro**: Apollo MCUs</span></span>

<span data-ttu-id="a3479-352">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/a15/a5/A7/A8/A9/A5x 64-bi/A7X a 64 bit/R4/R5, TrustZone ARMv8-M</span><span class="sxs-lookup"><span data-stu-id="a3479-352">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>

<span data-ttu-id="a3479-353">**Cadenza**: Xtensa, diamante</span><span class="sxs-lookup"><span data-stu-id="a3479-353">**Cadence**: Xtensa, Diamond</span></span>

<span data-ttu-id="a3479-354">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WICED WiFi</span><span class="sxs-lookup"><span data-stu-id="a3479-354">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>

<span data-ttu-id="a3479-355">**Cypress**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="a3479-355">**Cypress**: RISC-V</span></span>

<span data-ttu-id="a3479-356">**Silice**: ESI-RISC</span><span class="sxs-lookup"><span data-stu-id="a3479-356">**EnSilica**: eSi-RISC</span></span>

<span data-ttu-id="a3479-357">**Infineon**: XMC1000, XMC4000, Tricore</span><span class="sxs-lookup"><span data-stu-id="a3479-357">**Infineon**: XMC1000, XMC4000, TriCore</span></span>

<span data-ttu-id="a3479-358">**Intel; Intel FPGA**: x36/Pentium, XScale, Nios II, Cyclone, Arria 10</span><span class="sxs-lookup"><span data-stu-id="a3479-358">**Intel; Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>

<span data-ttu-id="a3479-359">**Microchip**: avr32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="a3479-359">**Microchip**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>

<span data-ttu-id="a3479-360">**Microsemi**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="a3479-360">**Microsemi**: RISC-V</span></span>

<span data-ttu-id="a3479-361">**NXP**: LPC, ARM7, ARM9, PowerPC, 68K, I.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="a3479-361">**NXP**: LPC, ARM7, ARM9, PowerPC, 68K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>

<span data-ttu-id="a3479-362">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span><span class="sxs-lookup"><span data-stu-id="a3479-362">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span></span>

<span data-ttu-id="a3479-363">**Laboratori siliconici**: EFM32</span><span class="sxs-lookup"><span data-stu-id="a3479-363">**Silicon Labs**: EFM32</span></span>

<span data-ttu-id="a3479-364">**Synopsys**: Arc 600, 700, Arc em, Arc HS</span><span class="sxs-lookup"><span data-stu-id="a3479-364">**Synopsys**: ARC 600, 700, ARC EM, ARC HS</span></span>

<span data-ttu-id="a3479-365">**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="a3479-365">**ST**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>

<span data-ttu-id="a3479-366">**TL**: C5xxx, C6xxx, Stellaris, Sitara, tiva-C</span><span class="sxs-lookup"><span data-stu-id="a3479-366">**Tl**: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>

<span data-ttu-id="a3479-367">**Elaborazione Wave**: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, MicroAptiv, InterAptiv, ProAptiv, M-Class</span><span class="sxs-lookup"><span data-stu-id="a3479-367">**Wave Computing**: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>

<span data-ttu-id="a3479-368">**Xilinx**: Microblaze, PowerPC 405, ZYNQ, Zynq UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="a3479-368">**Xilinx**: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>
