---
title: Appendice H-GUIX Build-Time flag di configurazione
description: Informazioni sui flag di configurazione in fase di compilazione GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 65095e326bc6809eba6e9472e2d74325351354ca
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822319"
---
# <a name="appendix-h---guix-build-time-configuration-flags"></a>Appendice H-GUIX Build-Time flag di configurazione

GUIX supportano diverse opzioni di compilazione condizionale e valori di configurazione. È possibile eseguire l'override dell'impostazione predefinita per le condizioni e i valori di configurazione predefinendo il valore nel file di intestazione gx_user. h o nella riga di comando del compilatore.

**GX_DISABLE_THREADX_BINDING**
- Valore predefinito: non definito
- Descrizione: questo condizionale può essere usato per disabilitare l'associazione RTO ThreadX predefinita. Se si vuole eseguire GUIX con un RTO diverso da ThreadX, è necessario #define GX_DISABLE_THREADX_BINDING e fornire i propri servizi di associazione RTO.

GX_SYSTEM_TIMER_MS
- Valore predefinito: 20
- Descrizione: questo valore definisce l'intervallo o la precisione del timer GUIX desiderato.

TX_TIMER_TICKS_PER_SECOND
- Predefinito: 100
- Descrizione: questo valore definisce il numero di frequenze di interrupt del timer TX. Poiché il timer di intervallo ThreadX predefinito è 10 ms, questo valore viene impostato su una frequenza di 100 Hz.

GX_SYSTEM_TIMER_TICKS
- Impostazione predefinita: ((GX_SYSTEM_TIMER_MS * TX_TIMER_TICKS_PER_SECOND)/1000)
- Descrizione: questo valore definisce il numero di cicli del timer RTO sottostanti per ogni segno di timer di GUIX. Il valore predefinito è 2, ovvero l'intervallo del timer GUIX è 2 intervalli di interrupt del timer ThreadX o 20 ms per impostazione predefinita.

GX_DISABLE_MULTITHREAD_SUPPORT
- Impostazione predefinita: non definita
- Descrizione: questa condizione condizionale in fase di compilazione può essere usata per disabilitare il supporto dell'API GUIX per più thread che richiamano l'API GUIX simultaneamente. Se un solo thread dell'applicazione utilizzerà mai l'API GUIX, è necessario definire questo flag per ridurre l'overhead del sistema associato alla protezione delle sezioni di codice critiche.

GX_DISABLE_UTF8_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: questa condizione condizionale in fase di compilazione può essere usata per rimuovere il supporto interno di GUIX per la codifica della stringa di formato UTF8. Se nell'applicazione si utilizzano solo i valori di carattere M-0xFF, l'attivazione di questa #define ridurrà le dimensioni del codice e l'overhead associato al supporto della codifica della stringa di formato UTF8.

GX_DISABLE_ARC_DRAWING_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: questa condizione condizionale può essere usata per ridurre le dimensioni del codice della libreria GUIX e GX_DISPLAY la dimensione della struttura rimuovendo il supporto per le funzioni di disegno arco, arco, torta ed ellisse. Queste funzioni non sono richieste dal set di widget GUIX predefinito.

GX_DISABLE_SOFTWARE_DECODER_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: questo condizionale può essere definito per rimuovere il supporto del decodificatore del software PNG e JPEG di runtime della libreria GUIX. Se l'applicazione non richiede la decodifica del runtime dei file jpg o PNG, che significa che l'applicazione non usa il formato RAW pixelmaps prodotto da studio e non legge i file di immagine da un file System esterno, è possibile attivare questa #define per ridurre il footprint della libreria GUIX.

GX_DISABLE_BINARY_RESOURCE_SUPPORT
- Impostazione predefinita: non definita
- Descrizione: questa condizione condizionale può essere usata per rimuovere il supporto della libreria GUIX per il caricamento dei dati delle risorse binarie. È possibile usare le risorse binarie per eseguire l'associazione di runtime dei dati delle risorse con l'applicazione GUIX. Se si usano solo file di risorse in formato codice sorgente C, è possibile definire questa condizione condizionale per ridurre il footprint della libreria GUIX.

GX_DISABLE_BRUSH_ALPHA_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: quando viene eseguito a 16 BPP e profondità di colore superiore, GUIX supporta facoltativamente il disegno di elementi grafici non Arc, pixelmaps e tipi di carattere con un valore alfa definito dal pennello del contesto di disegno. Il supporto di questa modalità di disegno introduce un lieve sovraccarico in fase di esecuzione e un aumento del footprint della libreria, che può essere eliminato definendo questo flag se non è necessario il supporto per il disegno con alpha blending. Si noti che pixelmaps con il canale alfa, i tipi di carattere con alias e altre modalità di disegno con anti-aliasing sono ancora supportati indipendentemente da questa impostazione condizionale.

GX_DISABLE_THREADX_TIMER_SOURCE
- Impostazione predefinita: non definita.
- Descrizione: questa condizione condizionale può essere usata per disabilitare l'origine del timer ThreadX. È necessario definire GX_DISABLE_THREADX_TIMER_SOURCE se si desidera utilizzare un'origine del timer diversa.

GX_REPEAT_BUTTON_INITIAL_TICS
- Predefinito: 10.
- Descrizione: se un pulsante presenta lo stile GX_STYLE_BUTTON_REPEAT, questo valore definisce il tempo di attesa del pulsante prima di iniziare a inviare eventi GX_EVENT_CLICKED ripetuti.

GX_MAX_QUEUE_EVENTS
- Valore predefinito: 48.
- Descrizione: definisce la dimensione della coda di eventi GUIX in unità di voci della struttura evento. Se si verifica un overflow della coda degli eventi, gli eventi inseriti nella coda vengono eliminati e GX_SYSTEM_ERROR viene restituito dalla funzione gx_system_event_send ().

GX_MAX_DIRTY_AREAS
- Valore predefinito: 64.
- Descrizione: definisce il numero massimo di voci di elenco Dirty univoche che possono essere gestite da un'area di disegno. Quando si verifica un overflow dell'elenco Dirty, per impostazione predefinita GUIX verrà contrassegnato come Dirty la finestra radice Canvas, che risulta meno efficiente rispetto al disegno di singoli widget figlio.

GX_MAX_CONTEXT_NESTING
- Impostazione predefinita: 8.
- Descrizione: definisce l'annidamento massimo dello stack del contesto del disegno. Equivale alla nidificazione massima dei widget padre/figlio/figlio/figlio all'interno della definizione dell'interfaccia utente.

GX_MAX_INPUT_CAPTURE_NESTING
- Impostazione predefinita: 4.
- Descrizione: definisce la dimensione dello stack usato per gestire l'elenco dei widget che hanno acquisito l'input dell'utente (mouse e tastiera).

GX_SYSTEM_THREAD_PRIORITY
- Impostazione predefinita: 16.
- Descrizione: definisce la priorità del thread GUIX creato durante gx_system_initialize ().

GX_SYSTEM_THREAD_TIMESLICE
- Predefinito: 10.
- Descrizione: definisce il TimeSlice del thread GUIX in termini di cicli del timer RTO. Se altri thread sono definiti con la stessa priorità del thread GUIX, questo valore determina la frequenza con cui i thread in conflitto ricevono il controllo della CPU.

GX_CURSOR_BLINK_INTERVAL
- Valore predefinito: 20.
- Descrizione: definisce la velocità con cui il cursore di input lampeggia per i widget di input di testo. Questo valore è in termini di cicli del timer GUIX, che per impostazione predefinita è definito come 50 ms, quindi un valore pari a 20 indica che il cursore di input lampeggia una volta al secondo.

GX_MULTI_LINE_INDEX_CACHE_SIZE
- Valore predefinito: 32.
- Descrizione: definisce la dimensione della cache degli indici di inizio elenco gestita dai widget visualizzazione testo su più righe e input di testo multiriga. Questa cache viene utilizzata per eseguire lo scorrimento verticale rapido dei widget di testo multilinea. Per prestazioni ottimali, le dimensioni della cache devono essere impostate su un valore maggiore del numero di righe visibili del più grande widget di testo multilinea definito dall'applicazione. Se, ad esempio, le righe più visibili per qualsiasi widget di testo sono pari a 20 righe, l'applicazione potrebbe definire una dimensione della cache di 32 (impostazione predefinita), che consente a GUIX di scorrere verticalmente senza ricalcolare tutti gli indici di avvio della riga.

GX_MULTI_LINE_TEXT_BUTTON_MAX_LINES
- Impostazione predefinita: 4.
- Descrizione: il blocco di controllo del pulsante di testo su più righe mantiene un puntatore a ogni riga di testo che deve essere visualizzata dal pulsante. Questo valore determina il numero di puntatori di testo necessari per il pulsante testo a più righe del caso peggiore.

GX_POLYGON_MAX_EDGE_NUM
- Predefinito: 10.
- Descrizione: questo valore determina il poligono più complesso che può essere disegnato da GUIX. L'algoritmo di disegno poligono determina le righe necessarie per definire i bordi del poligono e questa definizione definisce il numero massimo di spigoli che possono essere supportati.

GX_NUMERIC_SCROLL_WHEEL_STRING_BUFFER_SIZE
- Impostazione predefinita: 16.
- Descrizione: per una rotellina di scorrimento dei numeri, il widget della rotellina di scorrimento converte i valori integer in stringhe ASCII. Questo valore determina la lunghezza massima della stringa necessaria per visualizzare i valori integer assegnati.

GX_DEFAULT_CIRCULAR_GAUGE_ANIMATION_DELAY
- Impostazione predefinita: 5.
- Descrizione: definisce il numero di segni di graduazione del timer GUIX (50 ms) tra gli aggiornamenti di un misuratore circolare configurato per animare il movimento della lancetta tra l'ultima e la posizione angolare corrente.

GX_NUMERIC_PROMPT_BUFFER_SIZE
- Impostazione predefinita: 16.
- Descrizione: una richiesta numerica alloca un buffer per convertire un valore integer assegnato al prompt in una stringa ASCII. Questa definizione definisce la dimensione del buffer di caratteri.

GX_ANIMATION_POOL_SIZE
- Valore predefinito: 6.
- Descrizione: GUIX definisce un pool di animazioni da cui le strutture delle informazioni di animazione possono essere allocate e restituite dinamicamente, usando le API gx_system_animation_get e gx_system_animation_free (). Questa definizione definisce le dimensioni del pool di blocchi di controllo dell'animazione.

GX_MOUSE_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: questa definizione Abilita il supporto per l'input del mouse. Il mouse software richiede che il driver di visualizzazione disegni e tenga traccia del cursore del mouse, che aggiunge un sovraccarico aggiuntivo al driver di visualizzazione. Questa definizione deve essere definita solo quando è necessario supportare un mouse (non un touchscreen).

GX_HARDWARE_MOUSE_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: quando si definisce questa definizione, il driver di visualizzazione GUIX utilizza il supporto per il disegno del cursore del mouse. In questo modo si riduce la memoria necessaria per acquisire la memoria Canvas sotto il cursore del mouse e migliorare le prestazioni del sistema per tali destinazioni hardware che supportano un livello grafico sovrapposto al mouse.

GX_FONT_KERNING_SUPPORT
- Impostazione predefinita: non definita.
- Descrizione: questa definizione può essere definita per abilitare il supporto della crenatura dei tipi di carattere. La crenatura dei tipi di carattere migliora la spaziatura del glifo per determinate combinazioni di glifi. Questo supporto aggiunge una piccola quantità di overhead alle funzioni di disegno della stringa di runtime e aggiunge anche una piccola quantità di dimensioni alle strutture di dati del tipo di carattere.

GX_WIDGET_USER_DATA
- Impostazione predefinita: non definita.
- Descrizione: se definito, aggiunge un campo dati definito dall'utente al blocco di controllo GX_WIDGET. Questo campo dati può essere assegnato usando la visualizzazione proprietà in GUIX Studio. Questo campo dati viene ignorato da GUIX internamente, ma può essere utilizzato dal software applicativo per molti scopi.

GUIX_5_4_0_COMPATIBILITY
- Impostazione predefinita: non definita.
- Descrizione: alcune API GUI sono state modificate dopo la versione 5.4.0 per aggiungere il supporto per i colori del testo disabilitato e per migliorare l'accuratezza di determinate funzioni matematiche utilizzando parametri di corrispondenza a virgola fissa. Queste modifiche rendono le versioni della libreria GUIX dopo 5.4.0 incompatibili con le versioni precedenti. Tuttavia, se si accende questa #define, la libreria può essere compilata in modo che le API siano completamente compatibili con le versioni <= 5.4.0, vale a dire che non sono necessarie modifiche nelle applicazioni esistenti per la compilazione con la versione più recente della libreria GUIX.

GX_MAX_STRING_LENGTH
- Valore predefinito: 102400
- Descrizione: definisce la lunghezza massima di una stringa usata per testare le stringhe non valide. Se la stringa di input supera la lunghezza massima consentita per la stringa, sarà considerata non valida.