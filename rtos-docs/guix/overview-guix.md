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
# <a name="overview-of-azure-rtos-guix-and-azure-rtos-guix-studio"></a>Panoramica di Azure RTO GUIX e Azure RTO GUIX Studio

L'interfaccia utente grafica di Azure GUIX Embedded è una soluzione GUI avanzata e industriale di Microsoft progettata appositamente per applicazioni molto incorporate e in tempo reale. Microsoft offre anche uno strumento di progettazione desktop WYSIWYG completo denominato Azure RTO GUIX studio, che consente agli sviluppatori di progettare l'interfaccia utente grafica sul desktop e generare codice GUI incorporato GUIX di Azure RTO che può quindi essere esportato nella destinazione. Azure RTO GUIX è completamente integrato con Azure RTO ThreadX RTO ed è disponibile per molti degli stessi processori supportati da Azure RTO ThreadX. Tutti questi componenti, combinati con un footprint estremamente ridotto, un'esecuzione rapida e una maggiore facilità d'uso, rendono Azure RTO GUIX la scelta ideale per le applicazioni per le cose incorporate più complesse che richiedono un'interfaccia utente. 

## <a name="azure-rtos-guix-api"></a>API GUIX di Azure RTO

### <a name="intuitive-and-consistent-api"></a>API intuitiva e coerente

* Sostantivo-convenzione di denominazione dei verbi

* Tutte le API hanno *gx_* principali per identificare facilmente come Azure RTO GUIX

* Modello di programmazione basato sugli eventi (API)

* Supporto completo per il disegno Canvas diretto quando necessario

* Semplice interazione con il codice generato da Azure RTO GUIX Studio

* API per line, Rectangle, Polygon e così via.

* API per Circle, Arc, Pie, Chord, ellisse e così via.

* API per il disegno e il posizionamento del testo

* Anti-aliasing, riempimenti di trama e riempimenti a tinta unita

* API per la creazione e la modifica di schermate e widget

### <a name="azure-rtos-guix-studio-generated-files"></a>File generati da Azure RTO GUIX Studio

* File di origine ANSI C generati automaticamente

* Isola il software dell'applicazione dai dettagli del layout

* Include i tipi di carattere e le immagini richiesti dalla progettazione dell'interfaccia utente

* File generati compilati con il codice dell'applicazione

* Il layout della schermata può essere aggiornato senza influire sulla logica dell'applicazione

* ID risorsa creare la lingua e l'indipendenza del tema

* Funzioni di elaborazione di eventi e disegno personalizzato fornite dall'utente

### <a name="widget-library"></a>Libreria widget

* Set predefinito ma personalizzabile di elementi di interfaccia comuni

* Estremamente piccola, compatta ed efficiente

* La libreria include pulsante, misuratore, elenco, finestra, scorrimento, dispositivo di scorrimento, indicatore di stato, messaggio di richiesta e molto altro

* Disegno e aspetto completamente personalizzabili

* Operazioni completamente personalizzabili e gestione degli eventi

* Solo i widget usati sono collegati al software dell'applicazione

### <a name="math-and-utilities"></a>Matematica e utilità

* Funzioni per sin, cos, arcsin, ARccOS, tangente, radice quadrata

* Funzioni per la modifica delle aree dello schermo

* Configurazione e avvio del sistema

* Definizione del pool di memoria (facoltativo)

* Gestione timer

* Gestione delle animazioni

* Manutenzione elenco Dirty

### <a name="image-processing"></a>Elaborazione di immagini

* Funzioni per la decodifica di runtime di immagini JPEG e png

* Applicare la conversione dello spazio colore e del rethering

* Rotazione dell'immagine

* Ridimensionamento delle immagini

* Blending immagini

### <a name="event-processing"></a>Elaborazione di eventi

* Sospende automaticamente il thread GUIX di Azure RTO quando è inattivo

* Modello di programmazione basato sugli eventi popolare nella progettazione dell'interfaccia utente

* Isola i driver di input dal thread di disegno GUIX di Azure RTO

* Funzioni per l'invio e la ricezione di eventi

* Tipi di evento predefiniti per tutti i tipi di widget GUIX di Azure RTO

* Eventi personalizzati definiti dall'utente supportati

### <a name="canvas-processing"></a>Elaborazione Canvas

* Ritaglio e manutenzione degli ordini Z

* Isola la libreria widget dai dettagli hardware

* Isola l'applicazione dai dettagli dell'hardware

* Aggiornamento automatico in background di aree dirty

* Più Canvas con livelli e blending supportati

* Può essere richiamato direttamente dal software dell'applicazione

### <a name="input-device-drivers"></a>Driver/i dispositivo di input

* Supporto specifico dell'hardware, Azure RTO GUIX e applicazione isolata da dettagli hardware

* Tocco resistivo, perno sensibile e tastiera supportati

* Eventi di input passati alla coda degli eventi di Azure RTO GUIX

### <a name="display-drivers"></a>Visualizza driver

* Supporto specifico dell'hardware

* Driver generici forniti per tutti i formati e la profondità di colore

* Personalizzata per l'utilizzo di acceleratori grafici disponibili

### <a name="target-hardware"></a>Hardware di destinazione

* Quasi tutti i componenti hardware che supportano l'output grafico sono compatibili con GUIX

* Sono supportate più visualizzazioni fisiche

* Requisiti minimi di RAM e Flash

## <a name="create-elegant-user-interfaces"></a>Creare interfacce utente eleganti

Azure RTO GUIX e Azure RTO GUIX studio forniscono tutte le funzionalità necessarie per creare interfacce utente univocamente eleganti. Il pacchetto standard Azure RTO GUIX include varie interfacce utente di esempio, tra cui un riferimento ai dispositivi medici, un riferimento a Smart Watch, un riferimento per l'automazione della casa, un riferimento al controllo industriale, un riferimento per l'automotive e diversi esempi di sprite e animazione. Fare clic sugli esempi di riferimento illustrati di seguito.

### <a name="home-automation"></a>Automazione domestica

<img alt="Screenshot of the GUIX home automation" class="img-responsive" src="./media/overview/guix_home_automation.png"/>

### <a name="medical"></a>Medicina

<img alt="Screenshot of the GUIX medical device" class="img-responsive" src="./media/overview/demo_guix_medical.png"/>

### <a name="consumer"></a>Consumer

<img alt="Screenshot of the GUIX Consumer smart watch" class="img-responsive" src="./media/overview/demo_guix_smart_watch.png"/>

### <a name="white-goods"></a>Beni bianchi

<img alt="Screenshot of the GUIX white goods exaample" class="img-responsive" src="./media/overview/demo_guix_white_goods.png"/>

### <a name="automotive"></a>Automobilistico

<img alt="Screenshot of the GUIX automotive" class="img-responsive" src="./media/overview/demo_guix_infotainment.png"/>

### <a name="industrial"></a>Industriale

<img alt="Screenshot of the GUIX industrial control" class="img-responsive" src="./media/overview/demo_guix_industrial.png"/>

Ogni riferimento GUIX di Azure RTO include un progetto di Azure RTO GUIX Studio corrispondente che definisce tutti gli elementi grafici della progettazione di riferimento. Modificare una progettazione di riferimento è facile. È sufficiente aprire il progetto RTO GUIX di Azure corrispondente, apportare le modifiche desiderate, salvare il progetto e quindi selezionare *Project*.

Generare tutti i file di output per generare il codice C per Azure RTO GUIX. Quindi, è sufficiente ricompilare l'applicazione di destinazione ed eseguire per osservare la progettazione di riferimento modificata.

### <a name="small-footprint"></a>Footprint ridotto

Azure RTO GUIX ha un footprint minimo ristretto di 13,2 KB di RAM FLASH e 4KB per il supporto di base, senza includere la memoria necessaria per un'area di disegno.

Per una visualizzazione con la tecnologia di aggiornamento automatico e del grammo interno, non è necessaria alcuna memoria Canvas. Tuttavia, per migliorare le prestazioni di disegno o per una configurazione di visualizzazione che non utilizza la lingua locale per la visualizzazione, un'area di memoria Canvas viene definita dall'applicazione.

I requisiti di memoria di Canvas sono una funzione delle dimensioni dell'area di disegno, oltre alla profondità del colore, e sono definiti dalla formula:

<i>RAM Canvas (byte) = (x * y * (BPP/8))</i>

Dove "x" e "y" sono le dimensioni dell'area di disegno (visualizzazione).

La maggior parte delle applicazioni usa anche risorse grafiche, che non sono incluse nei requisiti principali di archiviazione della libreria GUIX di Azure RTO. Queste risorse includono tipi di carattere, icone grafiche (pixelmaps) e stringhe statiche. Questi dati possono essere archiviati nella sezione memoria const (ad esempio, FLASH).

Le dimensioni di questa area di memoria dipendono da diversi fattori, tra cui il numero e le dimensioni dei tipi di carattere univoci usati, il numero e le dimensioni delle icone grafiche usate, il formato del colore di output e se ogni risorsa usa dati compressi, poiché Azure RTO GUIX supporta la compressione RLE dei dati di tipo carattere e Pixelmap. I requisiti di archiviazione per ogni risorsa vengono visualizzati nell'applicazione Azure RTO GUIX studio, consentendo all'utente di tenere traccia e monitorare la quantità di memoria flash che verrà usata dalle risorse dell'applicazione.

Come Azure RTO ThreadX, le dimensioni di Azure RTO GUIX vengono ridimensionate automaticamente in base ai servizi effettivamente usati dall'applicazione. In questo modo si eliminano praticamente la necessità di complicati parametri di configurazione e di compilazione, semplificando le operazioni per lo sviluppatore.

### <a name="fast-execution"></a>Esecuzione rapida

Azure RTO GUIX è scritto esclusivamente in C ed è progettato per la velocità. Azure RTO GUIX ha un livello minimo di chiamata di funzione interna.

Inoltre, Azure RTO GUIX offre funzionalità ottimizzate di ritaglio, disegno e gestione degli eventi. Tutti questi e una filosofia di progettazione orientata alle prestazioni generale consentono ad Azure RTO GUIX di ottenere le prestazioni più veloci possibile.

### <a name="pre-certified--by-tuv-to-many-safety-standards"></a>Pre-certificati da TUV a molti standard di sicurezza

Azure RTO GUIX è stato certificato da SGS-TUV Saar per l'uso nei sistemi critici per la sicurezza, secondo IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 ASIL D e EN 50128. La certificazione conferma che Azure RTO GUIX può essere usato per lo sviluppo di software correlato alla sicurezza per i livelli di integrità di sicurezza più elevati di IEC-61508, IEC-62304, ISO 26262 e EN 50128 per la "protezione funzionale dei sistemi elettronici di sicurezza elettronica, elettronici e programmabili". SGS-TUV Saar, formato da una joint venture del SGS-Group e del TUV della Germania, è diventato la società leader accreditata e indipendente per il test, il controllo, la verifica e la certificazione del software incorporato per i sistemi correlati alla sicurezza in tutto il mondo. Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, tra cui IEC-62304, ISO 26262 e EN 50128, vengono usati per garantire la protezione funzionale di dispositivi medicali elettrici, elettronici e programmabili per la sicurezza elettronica, sistemi di controllo dei processi, macchinari industriali, automobili e sistemi di controllo ferroviario.

<img alt="SGS-TUV Saar" class="img-responsive" src="https://rtos.com/wp-content/uploads/2017/10/partener-logo-sgs-tuv-saar-2.png"/>

#### <a name="simple-easy-to-use"></a>Semplice e facile da usare

Azure RTO GUIX è molto semplice da usare e Azure RTO GUIX studio lo rende ancora più semplice consentendo agli sviluppatori di progettare visivamente sul desktop e generare codice C eseguito sulla destinazione effettiva. Le applicazioni possono quindi aggiungere le proprie funzioni personalizzate di gestione e creazione degli eventi per completare l'interfaccia utente grafica.

L'uso dell'API GUIX di Azure RTO è semplice. L'API GUIX di Azure RTO è intuitiva e altamente funzionale. I nomi delle API sono costituiti da parole reali e non dalla "zuppa alfabetica" e/o dai nomi molto abbreviati che sono così comuni in altri prodotti file system. Tutte le API GUIX di Azure RTO hanno un *gx_* leader e seguono una convenzione di denominazione sostantivo-verbo. Inoltre, esiste una coerenza funzionale nell'API. Ad esempio, tutte le API che inizializzano un blocco di controllo widget sono denominate &lt; widget_type &gt; _create e i parametri create function per ogni tipo di widget sono sempre definiti nello stesso ordine.

### <a name="comprehensive-set-of-built-in-widgets"></a>Set completo di widget predefiniti

* Azure RTO GUIX offre un set completo di widget predefiniti, tra cui:

* Menu Accordion

* Pulsante

* Casella di controllo

* Misuratore circolare

* Elenco a discesa

* Elenco orizzontale

* Finestra barra di scorrimento orizzontale

* Icona

* Pulsante icona

* Grafico a linee

* Menu

* Pulsante testo su più righe

* Input di testo multilinea

* Visualizzazione testo su più righe

* Richiesta Pixelmap numerica

* Prompt numerico

* Rotellina di scorrimento numerica

* Pulsante pixelmap

* Prompt pixelmap

* Dispositivo di scorrimento pixelmap

* Sprite pixelmap

* ProgressBar

* Prompt

* Indicatore di stato radiale

* RadioButton

* Rotellina di scorrimento

* Input di testo a riga singola

* Slider

* Rotellina di scorrimento stringa

* Pulsante testo

* Visualizzazione ad albero

* Elenco verticale

* Barra di scorrimento verticale

È facile per l'applicazione creare anche i propri widget dei clienti.

### <a name="complete-low-level-drawing-api"></a>API di disegno di basso livello completa

Azure RTO GUIX offre un'affidabile API di disegno Canvas, che consente all'applicazione di eseguire il rendering di forme grafiche complesse.

Tutte le funzioni supportano l'anti-aliasing su destinazioni di profondità dei colori elevate e tutte le forme possono essere riempite con la struttura, inclusi i riempimenti a tinta unita e Pixelmap. Tutte le primitive di disegno supportano il pennello alfa quando viene eseguito a 16 BPP e una profondità di colore superiore. Le funzioni di disegno includono:

* Arco di estrazione

* Cerchio disegnato

* Linea di estrazione

* Grafico a torta

* Pixelmap Blend

* Riquadro pixelmap

* Poligono di disegni

* Testo disegnato

* Accordo di estrazione

* Disegni ellissi

* Pixel di estrazione

* Pixelmap-disegni

* Pixelmap ruota

* Rettangolo di estrazione

* Blend di testo

### <a name="default-free-fonts-and-easy-to-add-more"></a>Tipi di carattere gratuiti predefiniti e semplicità di aggiunta

Azure RTO GUIX offre un set gratuito di tipi di carattere TrueType. Gli sviluppatori possono aggiungere altri tipi di carattere TrueType nel modo desiderato.

Il formato del tipo di carattere GUIX di Azure RTO supporta l'anti-aliasing 8bpp, l'anti-aliasing di 4bpp e i tipi di carattere monocromatico 1bpp. Per la maggior parte delle applicazioni con vincoli di risorse, Azure RTO GUIX pre-esegue il rendering dei tipi di carattere TrueType in un formato bitmap compresso usando lo strumento desktop di GUIX Studio.

### <a name="custom-jpg-and-png-decoder-implementation"></a>Implementazione del decodificatore JPG personalizzato e PNG

Implementazione del decodificatore jpg e png del decodificatore JPG e PNG personalizzato. Questa implementazione supporta la conversione dello spazio colore, la dithering e la creazione di runtime di immagini in formato Pixelmap compatibili con GUIX di Azure RTO.

### <a name="extensive-display-and-touchscreen-support"></a>Supporto completo per schermo e touchscreen

Azure RTO GUIX offre driver di visualizzazione generici per quasi tutti i formati di colore, tra cui 1bpp monocromatico, 8 BPP tavolozza, 8 BPP 3:3:2 formato

16 BPP 565, formato RGB, 16 BPP 4:4:4:4, 32 BPP x:r: g:b format e 32 BPP a:r: g:b format. Inoltre, Azure RTO GUIX è integrato con molti dei più diffusi controller LCD e acceleratori hardware (ST ChromeArt, Renesas Synergy e così via).

Azure RTO GUIX supporta completamente il touchscreen (incluso il supporto per il movimento), la penna e i dispositivi di input della tastiera virtuale.

### <a name="azure-rtos-guix-studio-desktop-wysiwyg-tool"></a>Strumento WYSIWYG di Azure RTO GUIX Studio Desktop

Azure RTO GUIX Studio fornisce un ambiente di progettazione della schermata WYSIWYG completo che consente all'utente di trascinare e rilasciare elementi grafici usati per creare le schermate dell'interfaccia utente grafica. Azure RTO GUIX Studio genera automaticamente il codice C compatibile con la libreria RTO GUIX di Azure, pronto per essere compilato ed eseguito nella destinazione. Gli sviluppatori possono produrre tipi di carattere pre-rendering da usare all'interno di un'applicazione usando lo strumento integrato di generazione dei caratteri di Azure RTO GUIX Studio. I tipi di carattere possono essere generati in formati monocromatici o anti-alias e sono ottimizzati per risparmiare spazio nella destinazione. I tipi di carattere possono includere qualsiasi set di caratteri, inclusi i caratteri Unicode per le applicazioni multilingue.

<img alt="Diagram of SGS-TUV Saar certification logo" class="alignnone size-full wp-image-1500" height="341" sizes="(max-width: 535px) 100vw, 535px" src="./media/overview/studio_screen_shot.png"/>

Azure RTO GUIX Studio semplifica l'importazione di elementi grafici da file PNG o JPG con conversione in Azure RTO GUIX compresso da usare nel sistema di destinazione. Molti dei tipi di widget GUIX di Azure RTO sono progettati per incorporare grafica utente per un aspetto personalizzato. Inoltre, Azure RTO GUIX Studio consente la personalizzazione dei colori predefiniti e degli stili di disegno usati dai widget GUIX di Azure RTO, consentendo agli sviluppatori di ottimizzare l'aspetto di Azure RTO GUIX in modo molto semplice. La generazione e la gestione delle stringhe dell'applicazione sono un'altra funzionalità incorporata di Azure RTO GUIX Studio. Ciò consente agli sviluppatori di progettare un'applicazione usando un linguaggio per lo sviluppo e di aggiungere in modo rapido e semplice il supporto per altre lingue dopo il rilascio del prodotto. Un'applicazione Azure RTO GUIX completa può essere eseguita su un desktop PC all'interno dell'ambiente Azure RTO GUIX studio, consentendo una generazione rapida e semplice di concetti di GUI, test dei flussi dello schermo e osservazione delle transizioni e delle animazioni dello schermo. Al termine, una progettazione può essere esportata come strutture di dati C pronte per la destinazione, pronta per essere compilata e collegata con le librerie di Azure RTO GUIX e Azure RTO ThreadX.

Azure RTO GUIX e Azure RTO GUIX Studio supportano più temi di risorse, consentendo a un'applicazione di essere facilmente Riskin in fase di esecuzione. I tipi di carattere, i colori e pixelmaps possono essere modificati in fase di esecuzione con una semplice API.

Scopri di più su GUIX Studio

### <a name="complete-win32-simulation"></a>Completa simulazione Win32

Azure RTO GUIX viene eseguito in un PC Windows, usando esattamente la stessa libreria di disegno eseguita sulla lavagna di destinazione. Con Azure RTO GUIX è possibile compilare ed eseguire un'applicazione GUI sul PC e usare lo stesso codice dell'applicazione nella destinazione per il debug, la creazione rapida di prototipi, la dimostrazione e l'operazione di destinazione WYSIWYG.

### <a name="advanced-technology"></a>Tecnologia avanzata

* La tecnologia avanzata di Azure RTO GUIX è incorporata:

* Fusione alfa

* Anti-aliasing

* Scalabilità automatica

* Compressione bitmap

* Blending Canvas

* Supporto widget personalizzato

* Supporto per disegno posticipato

* Supporto di rethering

* Programmazione neutra endian

* Supporto dell'acceleratore hardware

* Supporto multilingue e codifica UTF-8

* Supporto per più visualizzazioni e Canvas

* Ritaglio ottimizzato, disegno e gestione degli eventi

* Runtime JPEG e PNG Decoder

* Personalizzazione e temi

* Supporta la monocromia tramite il colore reale a 32 bit con formati di grafica Alpha

* Transizioni, sprite e supporto per animazioni

* Simulazione Win32

* Gestione delle finestre, inclusi i viewport e la manutenzione degli ordini Z

### <a name="fastest-time-to-market"></a>Time-to-market più veloce

Azure RTO GUIX è facile da installare, apprendere, usare, eseguire il debug, verificare, certificare e gestire. Azure RTO GUIX Studio consente anche di semplificare la progettazione e l'implementazione di GUI embedded. Di conseguenza, Azure RTO GUIX è una delle soluzioni GUI più diffuse per i dispositivi it incorporati. Il nostro vantaggio di time-to-Market coerente è basato su:

* Documentazione sulla qualità: esaminare la [Guida dell'utente di Azure RTO GUIX](about-guix.md) e vedere per se stessi.

* Disponibilità del codice sorgente completa

* API di facile utilizzo

* Set di funzionalità completo e avanzato

## <a name="one-simple-license"></a>Una licenza semplice

Non è previsto alcun costo per l'uso e il test del codice sorgente e nessun costo per le licenze di produzione quando viene distribuito in dispositivi con licenza preliminare, tutti gli altri dispositivi necessitano di una licenza annuale semplice.

## <a name="full-highest-quality-source-code"></a>Codice sorgente completo di qualità elevata

Nel corso degli anni, il codice sorgente NetX di Azure RTO ha impostato la qualità e la facilità di comprensione. Inoltre, la convenzione relativa alla presenza di una funzione per ogni file fornisce una semplice navigazione all'origine.

## <a name="supports-most-popular-architectures"></a>Supporta le architetture più diffuse

Azure RTO GUIX viene eseguito sui microprocessori più diffusi a 32/64 bit, predefiniti, completamente testati e completamente supportati, inclusi i seguenti:

Architetture avanzate:

**Dispositivi analoghi**: SHARC, Blackfin, CM4xx

**Andina Core**: RISC-V

**Ambiqmicro**: Apollo MCU

**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/a15/a5/A7/A8/A9/A5x 64-bi/A7X a 64 bit/R4/R5, TrustZone ARMv8-M

**Cadenza**: Xtensa, diamante

**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WICED WiFi

**Cypress**: RISC-V

**Silice**: ESI-RISC

**Infineon**: XMC1000, XMC4000, Tricore

**Intel; Intel FPGA**: x36/Pentium, XScale, Nios II, Cyclone, Arria 10

**Microchip**: avr32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32

**Microsemi**: RISC-V

**NXP**: LPC, ARM7, ARM9, PowerPC, 68K, I.MX, ColdFire, Kinetis Cortex-M3/M4

**Renesas**: SH, HS, V850, RX, RZ, Synergy

**Laboratori siliconici**: EFM32

**Synopsys**: Arc 600, 700, Arc em, Arc HS

**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7

**TL**: C5xxx, C6xxx, Stellaris, Sitara, tiva-C

**Elaborazione Wave**: MIPS32 4K, 24K, 34K, 1004K, MIPS64 5K, MicroAptiv, InterAptiv, ProAptiv, M-Class

**Xilinx**: Microblaze, PowerPC 405, ZYNQ, Zynq UltraSCALE
