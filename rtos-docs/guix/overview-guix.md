---
title: Informazioni Azure RTOS GUIX e Azure RTOS GUIX Studio
description: Azure RTOS GUIX è un pacchetto di qualità professionale, creato per soddisfare le esigenze degli sviluppatori di sistemi incorporati.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: faa1bc0d4697a7b5e79430097c2921fd4dde4be9e6390398befc0b89074f2fe6
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116790755"
---
# <a name="overview-of-azure-rtos-guix-and-azure-rtos-guix-studio"></a>Panoramica di Azure RTOS GUIX e Azure RTOS GUIX Studio

L'interfaccia utente grafica incorporata di GuiX di Azure è la soluzione GUI avanzata di livello industriale di Microsoft progettata specificamente per applicazioni IoT e deep embedded, in tempo reale. Microsoft offre anche uno strumento di progettazione desktop WYSIWYG completo denominato Azure RTOS GUIX Studio, che consente agli sviluppatori di progettare l'interfaccia utente grafica sul desktop e generare codice GUIX incorporato Azure RTOS GUIX che può quindi essere esportato nella destinazione. Azure RTOS GUIX è completamente integrato con Azure RTOS ThreadX RTOS ed è disponibile per molti degli stessi processori supportati da Azure RTOS ThreadX. Tutto questo combinato con un footprint estremamente ridotto, un'esecuzione rapida e una maggiore facilità d'uso, rendono Azure RTOS GUIX la scelta ideale per le applicazioni IoT incorporate più complesse che richiedono un'interfaccia utente. 

## <a name="azure-rtos-guix-api"></a>Azure RTOS GUIX API

### <a name="powerful-apis"></a>API potenti

* Supporto completo per il disegno canvas diretto quando necessario
* Semplice interazione con Azure RTOS codice generato da GUIX Studio
* API per linea, rettangolo, poligono e così via.
* API per cerchio, arco, torta, accordo, ellisse e così via.
* API per il disegno e il posizionamento del testo
* Anti-aliasing, riempimenti a trama e riempimenti a tinta unita
* API per la creazione e la modifica di schermate e widget

### <a name="azure-rtos-guix-studio-generated-files"></a>Azure RTOS file generati da GUIX Studio

* File di origine ANSI C generati automaticamente
* Isola il software dell'applicazione dai dettagli del layout
* Include tipi di carattere e immagini richiesti dalla progettazione dell'interfaccia utente
* File generati compilati con il codice dell'applicazione
* Il layout dello schermo può essere aggiornato senza influire sulla logica dell'applicazione
* Gli ID risorsa creano l'indipendenza della lingua e del tema
* Funzioni di disegno ed elaborazione eventi personalizzate fornite dall'utente

### <a name="widget-library"></a>Libreria widget

* Set predefinito ma personalizzabile di elementi di interfaccia comuni
* Estremamente piccola, compatta ed efficiente
* La libreria include pulsante, misuratore, elenco, finestra, scorrimento, dispositivo di scorrimento, indicatore di stato, richiesta e altro ancora
* Disegno e aspetto completamente personalizzabili
* Gestione di operazioni e eventi completamente personalizzabile
* Solo i widget usati sono collegati al software dell'applicazione

### <a name="math-and-utilities"></a>Matematica e utilità

* Funzioni per sin, cos, arcsin, arccos, tangente, radice quadrata
* Funzioni per la modifica delle aree dello schermo
* Configurazione e avvio del sistema
* Definizione del pool di memoria (facoltativo)
* Gestione timer
* Gestione delle animazioni
* Manutenzione degli elenchi dirty

### <a name="image-processing"></a>Elaborazione di immagini

* Funzioni per la decodifica di runtime di immagini jpeg e png
* Applicare il dithering e la conversione dello spazio colore
* Rotazione delle immagini
* Ridimensionamento delle immagini
* Fusione di immagini

### <a name="event-processing"></a>Elaborazione di eventi

* Sospende automaticamente Azure RTOS thread GUIX in caso di inattività
* Modello di programmazione basato su eventi comune nella progettazione dell'interfaccia utente
* Isola i driver di input Azure RTOS thread di disegno GUIX
* Funzioni per l'invio e la ricezione di eventi
* Tipi di evento predefiniti per tutti i Azure RTOS di widget GUIX
* Eventi personalizzati definiti dall'utente supportati

### <a name="canvas-processing"></a>Elaborazione dell'area di disegno

* Manutenzione del ritaglio e dell'ordine Z
* Isola la libreria di widget dai dettagli hardware
* Isola l'applicazione dai dettagli hardware
* Aggiornamento automatico in background delle aree dirty
* Più canvas con la strating e la fusione supportate
* Può essere richiamato direttamente dal software dell'applicazione

### <a name="input-device-drivers"></a>Driver di dispositivo di input

* Supporto specifico dell'hardware, Azure RTOS GUIX e applicazione isolata dai dettagli hardware
* Supporto di touch, tappi e tastierino di resistenza
* Eventi di input passati alla coda Azure RTOS eventi GUIX

### <a name="display-drivers"></a>Visualizzare i driver

* Supporto specifico dell'hardware
* Driver generici forniti per tutti i formati e la profondità del colore
* Personalizzato per usare gli acceleratori di grafica disponibili

### <a name="target-hardware"></a>Hardware di destinazione

* Quasi tutti i componenti hardware in grado di eseguire l'output grafico sono compatibili con GUIX
* Più schermi fisici supportati
* Requisiti minimi di RAM e Flash

## <a name="create-elegant-user-interfaces"></a>Creare interfacce utente eleganti

Azure RTOS GUIX e Azure RTOS GUIX Studio offrono tutte le funzionalità necessarie per creare interfacce utente univoche ed eleganti. Il pacchetto GUIX Azure RTOS standard include varie interfacce utente di esempio, tra cui un riferimento per dispositivi medici, un riferimento smart watch, un riferimento di automazione domestica, un riferimento di controllo industriale, un riferimento automobilistico e vari esempi di sprite e animazione. Fare clic sugli esempi di riferimento illustrati di seguito.

### <a name="home-automation"></a>Automazione domestica

<img alt="Screenshot of the GUIX home automation" class="img-responsive" src="./media/overview/guix_home_automation.png"/>

### <a name="medical"></a>Medicina

<img alt="Screenshot of the GUIX medical device" class="img-responsive" src="./media/overview/demo_guix_medical.png"/>

### <a name="consumer"></a>Consumer

<img alt="Screenshot of the GUIX Consumer smart watch" class="img-responsive" src="./media/overview/demo_guix_smart_watch.png"/>

### <a name="white-goods"></a>White Goods

<img alt="Screenshot of the GUIX white goods exaample" class="img-responsive" src="./media/overview/demo_guix_white_goods.png"/>

### <a name="automotive"></a>Automobilistico

<img alt="Screenshot of the GUIX automotive" class="img-responsive" src="./media/overview/demo_guix_infotainment.png"/>

### <a name="industrial"></a>Industriale

<img alt="Screenshot of the GUIX industrial control" class="img-responsive" src="./media/overview/demo_guix_industrial.png"/>

Ogni Azure RTOS riferimento GUIX ha un progetto AZURE RTOS GUIX Studio corrispondente che definisce tutti gli elementi grafici della progettazione di riferimento. La modifica di una progettazione di riferimento è semplice. È sufficiente aprire il Azure RTOS progetto GUIX corrispondente, apportare le modifiche desiderate, salvare il progetto e quindi *selezionare Project*.

Generare tutti i file di output per generare il codice C per Azure RTOS GUIX. È quindi sufficiente ricompilare l'applicazione di destinazione ed eseguire per osservare la progettazione dei riferimenti modificata.

### <a name="guix-memory-footprint"></a>Footprint di memoria GUIX

Azure RTOS GUIX ha un footprint minimo notevolmente ridotto di 13,2 KB di FLASH e 4 KB di RAM per il supporto di base, senza includere la memoria necessaria per un canvas.

Per una visualizzazione con GRAM interno e tecnologia di aggiornamento automatico, non è necessaria memoria canvas. Tuttavia, per migliorare le prestazioni di disegno o per una configurazione di visualizzazione che non usa GRAM locale per la visualizzazione, un'area di memoria canvas viene definita dall'applicazione.

I requisiti di memoria dell'area di disegno sono una funzione delle dimensioni dell'area di disegno e della profondità del colore e sono definiti dalla formula:

<i>RAM canvas (byte) = (x * y * (bpp/8))</i>

Dove "x" e "y" sono le dimensioni dell'area di disegno (visualizzazione).

La maggior parte delle applicazioni usa anche risorse grafiche, che non sono incluse nel core Azure RTOS di archiviazione della libreria GUIX. Queste risorse includono tipi di carattere, icone grafiche (pixelmap) e stringhe statiche. Questi dati possono essere archiviati nella sezione const memory (ad esempio FLASH).

Le dimensioni di questa area di memoria dipendono da diversi fattori, tra cui il numero e le dimensioni dei tipi di carattere univoci usati, il numero e le dimensioni delle icone grafiche usate, il formato del colore di output e se ogni risorsa usa o meno dati compressi, poiché Azure RTOS GUIX supporta la compressione RLE sia dei dati di tipo di carattere che di pixelmap. I requisiti di archiviazione per ogni risorsa vengono visualizzati all'interno dell'applicazione GUIX Studio di Azure RTOS, consentendo all'utente di tenere traccia e monitorare la quantità di memoria flash che verrà utilizzata dalle risorse dell'applicazione.

Come Azure RTOS ThreadX, le dimensioni di Azure RTOS GUIX vengono ridimensionate automaticamente in base ai servizi effettivamente usati dall'applicazione. Questo elimina virtualmente la necessità di parametri di configurazione e compilazione complessi, semplificando le operazioni per lo sviluppatore.

#### <a name="simple-easy-to-use"></a>Semplice, facile da usare

Azure RTOS GUIX è molto semplice da usare e Azure RTOS GUIX Studio lo rende ancora più semplice consentendo agli sviluppatori di progettare visivamente sul desktop e generare codice C che viene eseguito nella destinazione effettiva. Le applicazioni possono quindi aggiungere funzioni personalizzate di gestione e disegno degli eventi per completare l'interfaccia utente grafica.

L'uso Azure RTOS'API GUIX è semplice. L Azure RTOS API GUIX è intuitiva e altamente funzionale. I nomi delle API sono fatti di parole reali e non di "zuppe dell'alfabeto" e/o dei nomi altamente abbreviati così comuni in altri file system prodotti. Tutte Azure RTOS API GUIX hanno un gx_ *e* seguono una convenzione di denominazione sostantivo-verbo. Inoltre, esiste una coerenza funzionale in tutta l'API. Ad esempio, tutte le API che inizializzano un blocco di controllo widget sono denominate widget_type _create e i parametri della funzione create per ogni tipo di widget sono sempre definiti &lt; &gt; nello stesso ordine.

### <a name="comprehensive-set-of-built-in-widgets"></a>Set completo di widget predefiniti

* Azure RTOS GUIX offre un set di widget predefiniti, tra cui:
* Accordion Menu
* Button
* Casella di controllo
* Misuratore circolare
* Elenco a discesa
* Elenco orizzontale
* Finestra barra di scorrimento orizzontale
* Icona
* Pulsante Icona
* Grafico a linee
* Menu
* Pulsante Testo su più righe
* Input di testo su più righe
* Visualizzazione testo su più righe
* Richiesta mappa pixel numerica
* Richiesta numerica
* Rotellina di scorrimento numerica
* Pulsante Mappa pixel
* Richiesta mappa pixel
* Dispositivo di scorrimento mappa pixel
* Pixelmap Sprite
* ProgressBar
* Prompt
* Indicatore di stato radiale
* RadioButton
* Rotellina
* Input di testo a riga singola
* Slider
* Rotellina di scorrimento delle stringhe
* Pulsante Testo
* Visualizzazione ad albero
* Elenco verticale
* Barra di scorrimento verticale

È facile per l'applicazione creare anche i propri widget dei clienti.

### <a name="complete-low-level-drawing-api"></a>COMPLETARE l'API di disegno di basso livello

Azure RTOS GUIX offre un'API di disegno canvas affidabile che consente all'applicazione di eseguire il rendering di forme grafiche complesse.

Tutte le funzioni supportano l'antialiasing su destinazioni con profondità di colore elevata e tutte le forme possono essere riempite con il contorno, inclusi i riempimenti a tinta unita e a motivi mappa pixel. Tutte le primitive di disegno supportano l'alfa del pennello quando vengono eseguite a 16 bpp e una profondità di colore superiore. Le funzioni di disegno includono:

* Disegno ad arco
* Disegno di cerchi
* Disegno di linee
* Disegno a torta
* Fusione di mappe pixel
* Riquadro mappa pixel
* Disegno poligono
* Disegno di testo
* Chord Draw
* Disegno ellisse
* Disegno in pixel
* Disegno mappa pixel
* Rotazione mappa pixel
* Disegno rettangolo
* Combinazione di testo

### <a name="default-free-fonts-and-easy-to-add-more"></a>Tipi di carattere gratuiti predefiniti e facile da aggiungere

Azure RTOS GUIX offre un set gratuito di tipi di carattere TrueType. Gli sviluppatori possono aggiungere altri tipi di carattere TrueType in base alle esigenze.

Il Azure RTOS tipo di carattere GUIX supporta l'anti-aliasing 8bpp, l'anti-aliasing 4bpp e i tipi di carattere monocromatici 1bpp. Per le applicazioni più vincolate alle risorse, Azure RTOS GUIX esegue il pre-rendering dei tipi di carattere TrueType in un formato bitmap compresso usando lo strumento desktop GUIX Studio.

### <a name="custom-jpg-and-png-decoder-implementation"></a>Implementazione personalizzata del decodificatore JPG e PNG

Implementazione personalizzata del decodificatore JPG e PNG jpg e del decodificatore di file PNG. Questa implementazione supporta la conversione dello spazio dei colori, il dithering e la creazione di runtime Azure RTOS immagini in formato pixelmap compatibili con GUIX.

### <a name="extensive-display-and-touchscreen-support"></a>Supporto completo dello schermo e del touchscreen

Azure RTOS GUIX fornisce driver di visualizzazione generici per quasi tutti i formati di colore, tra cui 1bpp monocromatico, tavolozza 8 bpp, 8 bpp 3:3:2 formato,

Formato 16 bpp 565 rgb, 16 bpp 4:4:4:4, 32 bpp x:r:g:b e formato 32 bpp a:r:g:b. Inoltre, Azure RTOS GUIX è integrato con molti dei più diffusi controller LCD e acceleratori hardware (ST ChromeArt, Renesas Synergy e così via).

Azure RTOS GUIX supporta completamente il touchscreen (incluso il supporto dei movimenti), la penna e i dispositivi di input della tastiera virtuale.

### <a name="azure-rtos-guix-studio-desktop-wysiwyg-tool"></a>Azure RTOS strumento WYSIWYG desktop GUIX Studio

Azure RTOS GUIX Studio offre un ambiente di progettazione dello schermo WYSIWYG completo che consente all'utente di trascinare e rilasciare elementi grafici usati per compilare le schermate GUI. Azure RTOS GUIX Studio genera automaticamente codice C compatibile con la libreria GUIX Azure RTOS, pronta per essere compilata ed eseguita nella destinazione. Gli sviluppatori possono produrre tipi di carattere di cui è stato eseguito il rendering preliminare per l'uso all'interno di un'applicazione usando lo strumento Azure RTOS di generazione dei caratteri di GUIX Studio. I tipi di carattere possono essere generati in formati monocromatici o con antialiasing e sono ottimizzati per risparmiare spazio nella destinazione. I tipi di carattere possono includere qualsiasi set di caratteri, inclusi i caratteri Unicode per applicazioni multilingue.

<img alt="Diagram of SGS-TUV Saar certification logo" class="alignnone size-full wp-image-1500" height="341" sizes="(max-width: 535px) 100vw, 535px" src="./media/overview/studio_screen_shot.png"/>

Azure RTOS GUIX Studio facilita l'importazione di grafica da file PNG o JPG con conversione Azure RTOS pixelmap GUIX compresse per l'uso nel sistema di destinazione. Molti dei tipi Azure RTOS widget GUIX sono progettati per incorporare grafica utente per un aspetto personalizzato. Inoltre, Azure RTOS GUIX Studio consente la personalizzazione dei colori predefiniti e degli stili di disegno usati dai widget GUIX di Azure RTOS, consentendo agli sviluppatori di ottimizzare molto facilmente l'aspetto di Azure RTOS GUIX. La generazione e la manutenzione delle stringhe dell'applicazione è un'altra funzionalità incorporata di Azure RTOS GUIX Studio. In questo modo gli sviluppatori possono progettare un'applicazione usando un linguaggio per lo sviluppo e aggiungere rapidamente e facilmente il supporto per altri linguaggi dopo il rilascio del prodotto. Un'applicazione GUIX Azure RTOS completa può essere eseguita in un desktop pc all'interno dell'ambiente GUIX Studio di Azure RTOS, consentendo una generazione e una dimostrazione rapida e semplice dei concetti relativi all'interfaccia utente grafica, al test dei flussi dello schermo e all'osservazione delle transizioni dello schermo e delle animazioni. Al termine, una progettazione può essere esportata come strutture di dati C pronte per la destinazione, pronte per essere compilate e collegate con le librerie GUIX e threadX Azure RTOS Azure RTOS.

Azure RTOS GUIX e Azure RTOS GUIX Studio supportano più temi di risorse, consentendo di riasserire facilmente un'applicazione in fase di esecuzione. I tipi di carattere, i colori e le mappe pixel possono essere modificati in fase di esecuzione con una semplice API.

Altre informazioni su GUIX Studio

### <a name="complete-win32-simulation"></a>Completare la simulazione Win32

Azure RTOS GUIX viene eseguito in un PC Windows, usando esattamente la stessa libreria di disegno eseguita sulla scheda di destinazione. Con Azure RTOS GUIX, è possibile compilare ed eseguire un'applicazione GUI nel PC e usare lo stesso codice dell'applicazione nella destinazione per il debug, la creazione rapida di prototipi, la dimostrazione e l'operazione di destinazione WYSIWYG.

### <a name="advanced-technology"></a>Tecnologia avanzata

* Azure RTOS tecnologia avanzata di GUIX incorpora:
* Fusione alfa
* Antialiasing
* Scalabilità automatica
* Compressione bitmap
* Fusione dell'area di disegno
* Supporto dei widget personalizzati
* Supporto del disegno posticipato
* Supporto del dithering
* Programmazione neutra endiana
* Supporto dell'acceleratore hardware
* Supporto multilingue e codifica UTF-8
* Supporto di più display e canvas
* Ritaglio, disegno e gestione degli eventi ottimizzati
* Decodificatore JPEG e PNG di runtime
* Interfaccia e temi
* Supporta il colore reale monocromatico a 32 bit con formati di grafica alfa
* Supporto di transizioni, Sprite e animazioni
* Simulazione Win32
* Gestione delle finestre, inclusi i viewport e la manutenzione dell'ordine Z
