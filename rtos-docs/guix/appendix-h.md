---
title: Appendice H - Flag di configurazione Build-Time GUIX
description: Informazioni sui flag di configurazione della fase di compilazione GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: ecd4d86fbc6fb1ebaa002675e66492758edaf14ed90aa03fc9f4cf4abb87e661
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784207"
---
# <a name="appendix-h---guix-build-time-configuration-flags"></a>Appendice H - Flag di configurazione Build-Time GUIX

GUIX supporta diverse opzioni di compilazione condizionale e valori di configurazione. È possibile eseguire l'override dell'impostazione predefinita per questi valori condizionali e di configurazione definendo il valore nel file di intestazione gx_user.h o nella riga di comando del compilatore.

**GX_DISABLE_THREADX_BINDING**
- Impostazione predefinita: Non definito
- Descrizione: questa condizione condizionale può essere usata per disabilitare l'associazione RTOS ThreadX predefinita. Se si vuole eseguire GUIX con un RTOS diverso da ThreadX, è necessario #define GX_DISABLE_THREADX_BINDING e fornire i propri servizi di associazione RTOS.

GX_SYSTEM_TIMER_MS
- Impostazione predefinita: 20
- Descrizione: questo valore definisce l'intervallo o la precisione del timer GUIX desiderato.

TX_TIMER_TICKS_PER_SECOND
- Predefinito: 100
- Descrizione: questo valore definisce il numero di frequenze di interrupt del timer TX. Poiché il timer predefinito per l'intervallo ThreadX è 10 ms, questo valore viene impostato su una frequenza di 100 Hz.

GX_DISABLE_MULTITHREAD_SUPPORT
- Impostazione predefinita: non definita
- Descrizione: questo condizionale in fase di compilazione può essere usato per disabilitare il supporto dell'API GUIX per più thread che richiamano contemporaneamente l'API GUIX. Se solo un thread dell'applicazione utilizzerà l'API GUIX, è necessario definire questo flag per ridurre l'overhead di sistema associato alla protezione delle sezioni di codice critiche.

GX_DISABLE_UTF8_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: questo condizionale in fase di compilazione può essere usato per rimuovere il supporto interno GUIX per la codifica della stringa di formato UTF8. Se si usano solo valori di carattere M- 0xff nell'applicazione, l'attivazione di questo #define ridurrà le dimensioni del codice e il sovraccarico associati al supporto della codifica della stringa di formato UTF8.

GX_DISABLE_ARC_DRAWING_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: questa condizione condizionale può essere usata per ridurre le dimensioni del codice della libreria GUIX e le dimensioni della struttura GX_DISPLAY rimuovendo il supporto per le funzioni di disegno ad arco circle, arc, pie ed ellipse. Queste funzioni non sono richieste dal set di widget GUIX predefinito.

GX_DISABLE_SOFTWARE_DECODER_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: questa condizione condizionale può essere definita per rimuovere il supporto del decodificatore software JPEG e PNG del runtime della libreria GUIX. Se l'applicazione non richiede la decodifica di runtime di file jpg o png, ovvero l'applicazione non usa pixelmap in formato RAW prodotte da Studio e non legge i file di immagine da un file system esterno, è possibile attivare questo #define per ridurre il footprint della libreria GUIX.

GX_DISABLE_BINARY_RESOURCE_SUPPORT
- Impostazione predefinita: non definita
- Descrizione: questa condizione condizionale può essere usata per rimuovere il supporto della libreria GUIX per il caricamento di dati di risorse binarie. Le risorse binarie possono essere usate per eseguire il binding di runtime dei dati delle risorse con l'applicazione GUIX. Se si usano solo file di risorse in formato codice sorgente C, è possibile definire questa condizione condizionale per ridurre il footprint della libreria GUIX.

GX_DISABLE_BRUSH_ALPHA_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: quando si esegue a 16 bpp e a profondità di colore superiori, GUIX supporta facoltativamente il disegno di grafica non ad arco, mappe pixel e tipi di carattere con un valore alfa definito dal pennello del contesto di disegno. Il supporto di questa modalità di disegno introduce un piccolo sovraccarico di runtime e un aumento del footprint della libreria, che può essere eliminato definendo questo flag se non è necessario il supporto per il disegno con alpha blending. Si noti che le mappe pixel con canale alfa, tipi di carattere con anti-aliasing e altre modalità di disegno anti-aliasing sono ancora supportate indipendentemente da questa impostazione condizionale.

GX_DISABLE_THREADX_TIMER_SOURCE
- Impostazione predefinita: non definita.
- Descrizione: questa condizione condizionale può essere usata per disabilitare l'origine timer ThreadX. È necessario definire GX_DISABLE_THREADX_TIMER_SOURCE se si vuole usare un'origine timer diversa.

GX_REPEAT_BUTTON_INITIAL_TICS
- Predefinito: 10.
- Descrizione: se a un pulsante è applicato GX_STYLE_BUTTON_REPEAT stile, questo valore definisce il tempo di attesa del pulsante prima di iniziare a inviare eventi GX_EVENT_CLICKED ripetuti.

GX_MAX_QUEUE_EVENTS
- Impostazione predefinita: 48.
- Descrizione: definisce le dimensioni della coda di eventi GUIX in unità di voci della struttura di eventi. Se si verifica un overflow della coda di eventi, gli eventi inseriti nella coda vengono eliminati e GX_SYSTEM_ERROR viene restituito dalla funzione gx_system_event_send().

GX_MAX_DIRTY_AREAS
- Impostazione predefinita: 64.
- Descrizione: definisce il numero massimo di voci di elenco dirty univoche che possono essere gestite da un'area di disegno. Quando si verifica un overflow dell'elenco dirty, GUIX contrassegna per impostazione predefinita la finestra radice dell'area di disegno come dirty, il che è meno efficiente rispetto al disegno di singoli widget figlio.

GX_MAX_CONTEXT_NESTING
- Impostazione predefinita: 8.
- Descrizione: definisce l'annidamento massimo dello stack del contesto di disegno. Equivale all'annidamento massimo dei widget padre/figlio/figlio/figlio all'interno della definizione dell'interfaccia utente.

GX_MAX_INPUT_CAPTURE_NESTING
- Impostazione predefinita: 4.
- Descrizione: definisce le dimensioni dello stack usato per gestire l'elenco dei widget che hanno l'input dell'utente (mouse e tastiera).

GX_SYSTEM_THREAD_PRIORITY
- Impostazione predefinita: 16.
- Descrizione: definisce la priorità del thread GUIX creato durante gx_system_initialize().

GX_SYSTEM_THREAD_TIMESLICE
- Predefinito: 10.
- Descrizione: definisce il tempo del thread GUIX in termini di tick del timer RTOS. Se altri thread vengono definiti con la stessa priorità del thread GUIX, questo valore determina la frequenza con cui ai thread concorrenti viene concesso il controllo della CPU.

GX_CURSOR_BLINK_INTERVAL
- Valore predefinito: 20.
- Descrizione: definisce la frequenza con cui il cursore di input lampeggia per i widget di input di testo. Questo valore è in termini di tick del timer GUIX, che per impostazione predefinita è definito come 50 ms, quindi un valore pari a 20 indica che il cursore di input lampeggia una volta al secondo.

GX_MULTI_LINE_INDEX_CACHE_SIZE
- Impostazione predefinita: 32.
- Descrizione: definisce le dimensioni della cache dell'indice list-start gestita dalla visualizzazione testo su più righe e dai widget di input di testo su più righe. Questa cache viene usata per eseguire rapidamente lo scorrimento verticale dei widget di testo su più righe. Per prestazioni ottimali, le dimensioni della cache devono essere impostate su un numero maggiore di righe visibili del widget di testo su più righe più grande definito dall'applicazione. Ad esempio, se le righe più visibili per qualsiasi widget di testo sono 20 righe, l'applicazione potrebbe definire una dimensione della cache di 32 (impostazione predefinita), che consente a GUIX di scorrere verticalmente senza ricalcolare tutti gli indici di inizio riga.

GX_MULTI_LINE_TEXT_BUTTON_MAX_LINES
- Impostazione predefinita: 4.
- Descrizione: il blocco di controllo pulsante di testo su più righe mantiene un puntatore a ogni riga di testo che deve essere visualizzata dal pulsante. Questo valore determina il numero di puntatori di testo necessari per il pulsante di testo su più righe con il caso peggiore.

GX_POLYGON_MAX_EDGE_NUM
- Predefinito: 10.
- Descrizione: questo valore determina il poligono più complesso che può essere disegnato da GUIX. L'algoritmo di disegno poligono determina le linee necessarie per definire i bordi dei poligoni e questa definizione definisce il numero massimo di bordi che possono essere supportati.

GX_NUMERIC_SCROLL_WHEEL_STRING_BUFFER_SIZE
- Impostazione predefinita: 16.
- Descrizione: per una rotellina di scorrimento numerica, il widget della rotellina di scorrimento converte i valori integer in stringhe ascii. Questo valore determina la lunghezza massima della stringa necessaria per visualizzare i valori integer assegnati.

GX_DEFAULT_CIRCULAR_GAUGE_ANIMATION_DELAY
- Impostazione predefinita: 5.
- Descrizione: definisce il numero di tick del timer GUIX (50 ms) tra gli aggiornamenti di un misuratore circolare configurato per animare il movimento della lancetta tra l'ultima e la posizione angolare corrente.

GX_NUMERIC_PROMPT_BUFFER_SIZE
- Impostazione predefinita: 16.
- Descrizione: un prompt numerico alloca un buffer per convertire un valore intero assegnato al prompt in una stringa ascii. Questa definizione definisce le dimensioni di questo buffer di caratteri.

GX_ANIMATION_POOL_SIZE
- Impostazione predefinita: 6.
- Descrizione: GUIX definisce un pool di animazioni da cui le strutture di informazioni sull'animazione possono essere allocate e restituite dinamicamente, usando le API gx_system_animation_get e gx_system_animation_free(). Questa definizione definisce le dimensioni del pool di blocchi di controllo dell'animazione.

GX_MOUSE_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: questa definizione abilita il supporto per l'input del mouse. Il mouse software richiede che il driver di visualizzazione diseeni e tieni traccia del cursore del mouse, con un sovraccarico aggiuntivo per il driver di visualizzazione. Questa definizione deve essere definita solo quando è necessario il supporto di un mouse (non di un touchscreen).

GX_HARDWARE_MOUSE_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: quando questa definizione viene definita, il driver di visualizzazione GUIX utilizza il supporto per il disegno del cursore del mouse hardware. In questo modo si riduce la memoria necessaria per acquisire la memoria canvas sotto il cursore del mouse e si migliorano le prestazioni di sistema per tali destinazioni hardware che supportano un livello grafico di sovrapposizione del mouse.

GX_FONT_KERNING_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: questa definizione può essere definita per abilitare il supporto della crenatura dei caratteri. La crenatura dei caratteri migliora la spaziatura dei glifi per determinate combinazioni di glifi. Questo supporto aggiunge una piccola quantità di overhead alle funzioni di disegno della stringa di runtime e aggiunge anche una piccola quantità di dimensioni alle strutture dei dati del tipo di carattere.

GX_WIDGET_USER_DATA
- Impostazione predefinita: non definita.
- Descrizione: se definito, viene aggiunto un campo dati definito dall'utente al blocco GX_WIDGET controllo. Questo campo dati può essere assegnato usando la visualizzazione delle proprietà all'interno di GUIX Studio. Questo campo dati viene ignorato internamente da GUIX, ma può essere usato dal software applicativo per molti scopi.

GUIX_5_4_0_COMPATIBILITY
- Impostazione predefinita: non definita.
- Descrizione: alcune API GUI sono state modificate dopo la versione 5.4.0 per aggiungere il supporto per i colori del testo disabilitati e per migliorare l'accuratezza di determinate funzioni matematiche usando parametri di corrispondenza a virgola fissa. Queste modifiche rendono le versioni della libreria GUIX successive alla 5.4.0 incompatibili con le versioni precedenti. Tuttavia, attivando questo #define, la libreria può essere compilata in modo che le API siano completamente compatibili con le versioni <= 5.4.0, vale a dire che non sono necessarie modifiche nelle applicazioni esistenti per la compilazione con la versione più recente della libreria GUIX.

GX_MAX_STRING_LENGTH
- Impostazione predefinita: 102400
- Descrizione: definisce la lunghezza massima di una stringa, usata per testare le stringhe non valide. Se la stringa di input supera la lunghezza massima della stringa, verrà considerata non valida.