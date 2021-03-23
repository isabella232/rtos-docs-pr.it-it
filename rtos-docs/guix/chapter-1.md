---
title: Capitolo 1-Introduzione a GUIX
description: GUIX è un'implementazione in tempo reale a prestazioni elevate di un'interfaccia utente progettata esclusivamente per applicazioni incorporate basate su Azure RTO ThreadX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b90da988a03d59b1bca3f5584164d641bef96454
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823108"
---
# <a name="chapter-1---introduction-to-azure-rtos-guix"></a><span data-ttu-id="577be-103">Capitolo 1-Introduzione ad Azure RTO GUIX</span><span class="sxs-lookup"><span data-stu-id="577be-103">Chapter 1 - Introduction to Azure RTOS GUIX</span></span>

<span data-ttu-id="577be-104">Azure RTO GUIX (GUIX) è un'implementazione in tempo reale a prestazioni elevate di un Framework di interfaccia grafica progettato esclusivamente per applicazioni incorporate basate su ThreadX.</span><span class="sxs-lookup"><span data-stu-id="577be-104">Azure RTOS GUIX (GUIX) is a high-performance real-time implementation of a graphical interface framework designed exclusively for embedded ThreadX-based applications.</span></span> <span data-ttu-id="577be-105">Questo capitolo contiene un'introduzione a GUIX e una descrizione delle relative applicazioni e vantaggi.</span><span class="sxs-lookup"><span data-stu-id="577be-105">This chapter contains an introduction to GUIX and a description of its applications and benefits.</span></span>

## <a name="guix-feature-overview"></a><span data-ttu-id="577be-106">Panoramica della funzionalità GUIX</span><span class="sxs-lookup"><span data-stu-id="577be-106">GUIX Feature Overview</span></span>

<span data-ttu-id="577be-107">A differenza di molte altre implementazioni GUI, GUIX è progettato per essere versatile, con scalabilità semplice da piccole applicazioni basate su micro-controller, a quelle che usano potenti processori RISC e DSP.</span><span class="sxs-lookup"><span data-stu-id="577be-107">Unlike many other GUI implementations, GUIX is designed to be versatile—easily scaling from small micro-controller-based applications to those that use powerful RISC and DSP processors.</span></span> <span data-ttu-id="577be-108">Si tratta di un contrasto netto rispetto a un dominio pubblico o ad altre implementazioni commerciali destinate originariamente agli ambienti di workstation, ma vengono quindi compresse in progettazioni incorporate.</span><span class="sxs-lookup"><span data-stu-id="577be-108">This is in sharp contrast to public domain or other commercial implementations originally intended for workstation environments but then squeezed into embedded designs.</span></span> <span data-ttu-id="577be-109">Di seguito viene riportata una panoramica delle funzionalità di GUIX:</span><span class="sxs-lookup"><span data-stu-id="577be-109">An overview of GUIX features follows:</span></span>

- <span data-ttu-id="577be-110">Facile da usare con lo strumento di progettazione basato su host GUIX Studio</span><span class="sxs-lookup"><span data-stu-id="577be-110">Easy to use with host-based design tool GUIX Studio</span></span>

- <span data-ttu-id="577be-111">Ambiente di runtime Win32 GUIX per la prototipazione host completa</span><span class="sxs-lookup"><span data-stu-id="577be-111">Win32 GUIX run-time environment for complete hosted prototyping</span></span>

- <span data-ttu-id="577be-112">Supporta la maggior parte dei processori supportati da ThreadX</span><span class="sxs-lookup"><span data-stu-id="577be-112">Supports most processors supported by ThreadX</span></span>

- <span data-ttu-id="577be-113">Scritto esclusivamente in ANSI C</span><span class="sxs-lookup"><span data-stu-id="577be-113">Written exclusively in ANSI C</span></span>

- <span data-ttu-id="577be-114">Endian neutro</span><span class="sxs-lookup"><span data-stu-id="577be-114">Endian neutral</span></span>

- <span data-ttu-id="577be-115">GUI incorporata più piccola e veloce</span><span class="sxs-lookup"><span data-stu-id="577be-115">Smallest, Fasted Embedded GUI</span></span>

- <span data-ttu-id="577be-116">Configurabile in fase di esecuzione, numero di oggetti, dimensioni dello schermo e così via.</span><span class="sxs-lookup"><span data-stu-id="577be-116">Run-time configurable, number of objects, screen size, etc.</span></span>

- <span data-ttu-id="577be-117">Interfaccia del driver di visualizzazione facile da scrivere</span><span class="sxs-lookup"><span data-stu-id="577be-117">Easy to write display driver interface</span></span>

- <span data-ttu-id="577be-118">Colore (fino alla profondità del colore di 32-BPP), supporto monocromatico e scala di grigi</span><span class="sxs-lookup"><span data-stu-id="577be-118">Color (up to 32-bpp color depth), monochrome, and grayscale support</span></span>

- <span data-ttu-id="577be-119">Supporto multilingue tramite codifica di stringhe UTF8 e risorse di stringa</span><span class="sxs-lookup"><span data-stu-id="577be-119">Multilingual support via UTF8 string encoding and string resources</span></span>

- <span data-ttu-id="577be-120">Tipi di carattere gratuiti predefiniti e facile aggiunta di nuovi tipi di carattere</span><span class="sxs-lookup"><span data-stu-id="577be-120">Default free fonts and easy to add new fonts</span></span>

- <span data-ttu-id="577be-121">Sono supportate più Canvas di disegno di diverse dimensioni</span><span class="sxs-lookup"><span data-stu-id="577be-121">Multiple drawing Canvases supported, of various sizes</span></span>

- <span data-ttu-id="577be-122">Sono supportate più visualizzazioni di dimensioni e profondità dei colori diverse</span><span class="sxs-lookup"><span data-stu-id="577be-122">Multiple displays of different sizes and color depths supported</span></span>

- <span data-ttu-id="577be-123">Supporto della transizione dello schermo (dissolvenza, dissolvenza, scorrimento e così via)</span><span class="sxs-lookup"><span data-stu-id="577be-123">Screen Transition support (fade in, fade out, swipe, etc.)</span></span>

- <span data-ttu-id="577be-124">Supporto per touchscreen, movimenti e tastiera virtuale</span><span class="sxs-lookup"><span data-stu-id="577be-124">Touch Screen, Gesture, and Virtual Keyboard Support</span></span>

- <span data-ttu-id="577be-125">Compressione bitmap</span><span class="sxs-lookup"><span data-stu-id="577be-125">Bitmap compression</span></span>

- <span data-ttu-id="577be-126">Supporto per la fusione alfa</span><span class="sxs-lookup"><span data-stu-id="577be-126">Alpha Blending Support</span></span>

- <span data-ttu-id="577be-127">Supporto del dithering</span><span class="sxs-lookup"><span data-stu-id="577be-127">Dither Support</span></span>

- <span data-ttu-id="577be-128">Supporto anti-aliasing</span><span class="sxs-lookup"><span data-stu-id="577be-128">Anti-Aliasing Support</span></span>

- <span data-ttu-id="577be-129">Personalizzazione e temi</span><span class="sxs-lookup"><span data-stu-id="577be-129">Skinning and Themes</span></span>

- <span data-ttu-id="577be-130">Blending Canvas</span><span class="sxs-lookup"><span data-stu-id="577be-130">Canvas Blending</span></span>

- <span data-ttu-id="577be-131">Gestione completa della finestra</span><span class="sxs-lookup"><span data-stu-id="577be-131">Complete Window Management</span></span>

  - <span data-ttu-id="577be-132">Relazione padre/figlio</span><span class="sxs-lookup"><span data-stu-id="577be-132">Parent/Child Relationship</span></span>

  - <span data-ttu-id="577be-133">Creazione dinamica, eliminazione, ridimensionamento, trasferimento</span><span class="sxs-lookup"><span data-stu-id="577be-133">Dynamic creation, deletion, resizing, moving</span></span>
  - <span data-ttu-id="577be-134">Creazione e gestione di eventi distinti</span><span class="sxs-lookup"><span data-stu-id="577be-134">Separate event handling and drawing</span></span> 
  - <span data-ttu-id="577be-135">Ordine Z</span><span class="sxs-lookup"><span data-stu-id="577be-135">Z-order</span></span>
  - <span data-ttu-id="577be-136">Ritaglio e visualizzazioni</span><span class="sxs-lookup"><span data-stu-id="577be-136">Clipping and views</span></span>

- <span data-ttu-id="577be-137">Set completo di widget</span><span class="sxs-lookup"><span data-stu-id="577be-137">Extensive Set of Widgets</span></span>

  - <span data-ttu-id="577be-138">Vari tipi di pulsanti, dispositivi di scorrimento e comparazioni</span><span class="sxs-lookup"><span data-stu-id="577be-138">Various button types, sliders, and dials</span></span>

  - <span data-ttu-id="577be-139">Elenco a discesa</span><span class="sxs-lookup"><span data-stu-id="577be-139">Drop Down List</span></span>
  
  - <span data-ttu-id="577be-140">Prompt</span><span class="sxs-lookup"><span data-stu-id="577be-140">Prompt</span></span>

  - <span data-ttu-id="577be-141">Visualizzazione di testo su più righe</span><span class="sxs-lookup"><span data-stu-id="577be-141">Multi-Line text view</span></span>
  
  - <span data-ttu-id="577be-142">Input di testo a riga singola e a più righe</span><span class="sxs-lookup"><span data-stu-id="577be-142">Single and Multi-Line text input</span></span>
  
  - <span data-ttu-id="577be-143">Rotellina di scorrimento numerica e testuale</span><span class="sxs-lookup"><span data-stu-id="577be-143">Numeric and Textual Scroll Wheels</span></span>
  
  - <span data-ttu-id="577be-144">Finestre e barre di scorrimento</span><span class="sxs-lookup"><span data-stu-id="577be-144">Windows and Scroll Bars</span></span>
  
  - <span data-ttu-id="577be-145">Indicatore di stato radiale</span><span class="sxs-lookup"><span data-stu-id="577be-145">Radial Progress Bar</span></span>
  
  - <span data-ttu-id="577be-146">Sprite</span><span class="sxs-lookup"><span data-stu-id="577be-146">Sprite</span></span>

### <a name="ansi-c-source-code"></a><span data-ttu-id="577be-147">Codice sorgente ANSI C</span><span class="sxs-lookup"><span data-stu-id="577be-147">ANSI C Source Code</span></span>

<span data-ttu-id="577be-148">GUIX è scritto completamente in ANSI C ed è immediatamente portabile in qualsiasi architettura del processore con un compilatore ANSI C e il supporto di ThreadX.</span><span class="sxs-lookup"><span data-stu-id="577be-148">GUIX is written completely in ANSI C and is portable immediately to virtually any processor architecture that has an ANSI C compiler and ThreadX support.</span></span> <span data-ttu-id="577be-149">Sebbene sia scritto in ANSI C, GUIX utilizza un modello orientato a oggetti ed ereditarietà.</span><span class="sxs-lookup"><span data-stu-id="577be-149">Although written in ANSI C, GUIX uses an object oriented model and inheritance.</span></span>

### <a name="not-a-black-box"></a><span data-ttu-id="577be-150">Non è una scatola nera</span><span class="sxs-lookup"><span data-stu-id="577be-150">Not A Black Box</span></span>

<span data-ttu-id="577be-151">La maggior parte delle distribuzioni di GUIX include il codice sorgente C completo.</span><span class="sxs-lookup"><span data-stu-id="577be-151">Most distributions of GUIX include the complete C source code.</span></span> <span data-ttu-id="577be-152">In questo modo si eliminano i problemi "black-box" che si verificano con molte implementazioni GUI commerciali.</span><span class="sxs-lookup"><span data-stu-id="577be-152">This eliminates the “black-box” problems that occur with many commercial GUI implementations.</span></span> <span data-ttu-id="577be-153">Con GUIX, gli sviluppatori di applicazioni possono vedere esattamente cosa sta facendo l'interfaccia utente grafica, ma non ci sono misteri.</span><span class="sxs-lookup"><span data-stu-id="577be-153">By using GUIX, applications developers can see exactly what the GUI is doing—there are no mysteries!</span></span>

<span data-ttu-id="577be-154">Il codice sorgente consente anche modifiche specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="577be-154">Having the source code also allows for application specific modifications.</span></span> <span data-ttu-id="577be-155">Sebbene non sia consigliato, è senz'altro utile avere la possibilità di modificare l'interfaccia utente grafica, se necessaria.</span><span class="sxs-lookup"><span data-stu-id="577be-155">Although not recommended, it is certainly beneficial to have the ability to modify the GUI if it is required.</span></span> <span data-ttu-id="577be-156">Queste funzionalità sono particolarmente confortanti per gli sviluppatori abituati a lavorare con prodotti di dominio interno o pubblico.</span><span class="sxs-lookup"><span data-stu-id="577be-156">These features are especially comforting to developers accustomed to working with in-house or public domain products.</span></span> <span data-ttu-id="577be-157">Si aspettano che il codice sorgente sia in grado di modificarlo.</span><span class="sxs-lookup"><span data-stu-id="577be-157">They expect to have source code and the ability to modify it.</span></span> <span data-ttu-id="577be-158">GUIX è il software GUI finale per tali sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="577be-158">GUIX is the ultimate GUI software for such developers.</span></span>

## <a name="embedded-gui-applications"></a><span data-ttu-id="577be-159">Applicazioni GUI incorporate</span><span class="sxs-lookup"><span data-stu-id="577be-159">Embedded GUI Applications</span></span>

<span data-ttu-id="577be-160">Le applicazioni GUI incorporate sono applicazioni con requisiti di interfaccia utente e vengono eseguite su microprocessori nascosti all'interno di prodotti quali telefoni cellulari, apparecchiature di comunicazione, motori automobilistici, stampanti laser, dispositivi medicali e così via.</span><span class="sxs-lookup"><span data-stu-id="577be-160">Embedded GUI applications are applications that have a user interface requirement and execute on microprocessors hidden inside products such as cellular phones, communication equipment, automotive engines, laser printers, medical devices, and so forth.</span></span> <span data-ttu-id="577be-161">Tali applicazioni presentano quasi sempre alcuni vincoli di memoria e di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="577be-161">Such applications almost always have some memory and performance constraints.</span></span> <span data-ttu-id="577be-162">Un'altra distinzione della GUI incorporata è che il software e l'hardware hanno uno scopo dedicato.</span><span class="sxs-lookup"><span data-stu-id="577be-162">Another distinction of embedded GUI is that their software and hardware have a dedicated purpose.</span></span>

### <a name="real-time-gui-software"></a><span data-ttu-id="577be-163">Software GUI in tempo reale</span><span class="sxs-lookup"><span data-stu-id="577be-163">Real-time GUI Software</span></span>

<span data-ttu-id="577be-164">In pratica, il software GUI che deve eseguire l'elaborazione in un periodo di tempo esatto viene chiamato software *GUI in tempo reale* e quando i vincoli temporali vengono applicati alle applicazioni GUI, vengono classificati come applicazioni in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="577be-164">Basically, GUI software that must perform its processing within an exact period of time is called *real-time GUI* software, and when time constraints are imposed on GUI applications, they are classified as realtime applications.</span></span> <span data-ttu-id="577be-165">Le applicazioni GUI incorporate sono quasi sempre in tempo reale a causa dell'interazione intrinseca con il mondo esterno.</span><span class="sxs-lookup"><span data-stu-id="577be-165">Embedded GUI applications are almost always real-time because of their inherent interaction with the external world.</span></span>

## <a name="guix-benefits"></a><span data-ttu-id="577be-166">Vantaggi di GUIX</span><span class="sxs-lookup"><span data-stu-id="577be-166">GUIX Benefits</span></span>

<span data-ttu-id="577be-167">I principali vantaggi derivanti dall'utilizzo di GUIX per le applicazioni incorporate sono i requisiti di memoria elevate, con funzionalità avanzate e molto ridotte.</span><span class="sxs-lookup"><span data-stu-id="577be-167">The primary benefits of using GUIX for embedded applications are high-performance, feature rich, and very small memory requirements.</span></span> <span data-ttu-id="577be-168">GUIX è anche completamente integrato con il sistema operativo in tempo reale multitasking di Azure RTO ThreadX per le prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="577be-168">GUIX is also completely integrated with the high-performance, multitasking Azure RTOS ThreadX real-time operating system.</span></span>

### <a name="improved-responsiveness"></a><span data-ttu-id="577be-169">Velocità di risposta migliorata</span><span class="sxs-lookup"><span data-stu-id="577be-169">Improved Responsiveness</span></span>

<span data-ttu-id="577be-170">Il prodotto GUIX a prestazioni elevate consente alle applicazioni di rispondere più rapidamente che mai.</span><span class="sxs-lookup"><span data-stu-id="577be-170">The high-performance GUIX product enables applications to respond faster than ever before.</span></span> <span data-ttu-id="577be-171">Questo è particolarmente importante per le applicazioni incorporate che hanno un volume significativo di informazioni visive o requisiti di temporizzazione rigidi per la visualizzazione di tali informazioni.</span><span class="sxs-lookup"><span data-stu-id="577be-171">This is especially important for embedded applications that either have a significant volume of visual information or strict timing requirements on displaying such information.</span></span>

### <a name="software-maintenance"></a><span data-ttu-id="577be-172">Manutenzione del software</span><span class="sxs-lookup"><span data-stu-id="577be-172">Software Maintenance</span></span>

<span data-ttu-id="577be-173">L'uso di GUIX consente agli sviluppatori di partizionare facilmente gli aspetti dell'interfaccia utente grafica dell'applicazione incorporata.</span><span class="sxs-lookup"><span data-stu-id="577be-173">Using GUIX allows developers to easily partition the GUI aspects of their embedded application.</span></span> <span data-ttu-id="577be-174">Questo partizionamento rende l'intero processo di sviluppo semplice e migliora significativamente la manutenzione futura del software.</span><span class="sxs-lookup"><span data-stu-id="577be-174">This partitioning makes the entire development process easy and significantly enhances future software maintenance.</span></span>

### <a name="increased-throughput"></a><span data-ttu-id="577be-175">Maggiore velocità effettiva</span><span class="sxs-lookup"><span data-stu-id="577be-175">Increased Throughput</span></span>

<span data-ttu-id="577be-176">GUIX fornisce l'interfaccia utente grafica a prestazioni elevate disponibile, che trasferisce direttamente all'applicazione incorporata.</span><span class="sxs-lookup"><span data-stu-id="577be-176">GUIX provides the highest-performance GUI available, which directly transfers to the embedded application.</span></span> <span data-ttu-id="577be-177">Le applicazioni GUIX sono in grado di elaborare le informazioni dell'interfaccia utente più velocemente di quelle non GUIX.</span><span class="sxs-lookup"><span data-stu-id="577be-177">GUIX applications are able to process user interface information faster than non-GUIX applications!</span></span>

### <a name="processor-isolation"></a><span data-ttu-id="577be-178">Isolamento processore</span><span class="sxs-lookup"><span data-stu-id="577be-178">Processor Isolation</span></span>

<span data-ttu-id="577be-179">GUIX fornisce un'interfaccia affidabile e indipendente dal processore tra l'applicazione e il processore sottostante e l'hardware di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="577be-179">GUIX provides a robust, processor-independent interface between the application and the underlying processor and display hardware.</span></span> <span data-ttu-id="577be-180">Ciò consente agli sviluppatori di concentrarsi sugli aspetti di alto livello dell'interfaccia utente piuttosto che spendere più tempo per la visualizzazione dei problemi hardware.</span><span class="sxs-lookup"><span data-stu-id="577be-180">This allows developers to concentrate on the high-level aspects of the user interface rather than spending extra time dealing with display hardware issues.</span></span>

### <a name="ease-of-use"></a><span data-ttu-id="577be-181">Semplicità d'uso</span><span class="sxs-lookup"><span data-stu-id="577be-181">Ease of Use</span></span>

<span data-ttu-id="577be-182">GUIX è progettato tenendo presente lo sviluppatore di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="577be-182">GUIX is designed with the application developer in mind.</span></span> <span data-ttu-id="577be-183">L'architettura GUIX e l'interfaccia di chiamata del servizio sono facili da comprendere.</span><span class="sxs-lookup"><span data-stu-id="577be-183">The GUIX architecture and service call interface are easy to understand.</span></span> <span data-ttu-id="577be-184">Di conseguenza, gli sviluppatori GUIX possono usare rapidamente le funzionalità avanzate.</span><span class="sxs-lookup"><span data-stu-id="577be-184">As a result, GUIX developers can quickly use its advanced features.</span></span>

### <a name="improve-time-to-market"></a><span data-ttu-id="577be-185">Miglioramento del time-to-Market</span><span class="sxs-lookup"><span data-stu-id="577be-185">Improve Time to Market</span></span>

<span data-ttu-id="577be-186">Le potenti funzionalità di GUIX accelerano il processo di sviluppo del software.</span><span class="sxs-lookup"><span data-stu-id="577be-186">The powerful features of GUIX accelerate the software development process.</span></span> <span data-ttu-id="577be-187">GUIX estrae la maggior parte del processore e visualizza problemi hardware, eliminando così questi problemi dalla maggior parte dell'implementazione dell'interfaccia utente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="577be-187">GUIX abstracts most processor and display hardware issues, thereby removing these concerns from a majority of application user interface implementation.</span></span> <span data-ttu-id="577be-188">Questa funzionalità, abbinata alla semplicità d'uso e al set di funzionalità avanzate, comporta tempi di immissione sul mercato più rapidi.</span><span class="sxs-lookup"><span data-stu-id="577be-188">This feature, coupled with the ease-of-use and advanced feature set, results in a faster time to market!</span></span>

### <a name="protecting-the-software-investment"></a><span data-ttu-id="577be-189">Protezione dell'investimento software</span><span class="sxs-lookup"><span data-stu-id="577be-189">Protecting the Software Investment</span></span>

<span data-ttu-id="577be-190">GUIX è scritto esclusivamente in ANSI C ed è completamente integrato con il sistema operativo Azure RTO ThreadX in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="577be-190">GUIX is written exclusively in ANSI C and is fully integrated with the Azure RTOS ThreadX real-time operating system.</span></span> <span data-ttu-id="577be-191">Ciò significa che le applicazioni GUIX sono immediatamente portabili a tutti i processori supportati da ThreadX.</span><span class="sxs-lookup"><span data-stu-id="577be-191">This means GUIX applications are instantly portable to all ThreadX supported processors.</span></span> <span data-ttu-id="577be-192">Meglio ancora, un'architettura del processore completamente nuova può essere supportata con ThreadX in poche settimane.</span><span class="sxs-lookup"><span data-stu-id="577be-192">Better yet, a completely new processor architecture can be supported with ThreadX in a matter of weeks.</span></span> <span data-ttu-id="577be-193">Di conseguenza, l'uso di GUIX garantisce il percorso di migrazione dell'applicazione e protegge l'investimento di sviluppo originale.</span><span class="sxs-lookup"><span data-stu-id="577be-193">As a result, using GUIX ensures the application’s migration path and protects the original development investment.</span></span>
