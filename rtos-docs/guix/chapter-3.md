---
title: Capitolo 3-Panoramica funzionale di GUIX
description: Questo capitolo contiene una panoramica funzionale del prodotto con interfaccia utente GUIX a prestazioni elevate.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2057b86e6f44912fe8ca349cdf0ad2cc10f5c4cd
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823105"
---
# <a name="chapter-3---functional-overview-of-guix"></a>Capitolo 3-Panoramica funzionale di GUIX

Questo capitolo contiene una panoramica funzionale del prodotto con interfaccia utente GUIX a prestazioni elevate. 

## <a name="execution-overview"></a>Panoramica dell'esecuzione

GUIX implementa un modello di programmazione basato sugli eventi. Ciò significa che il Framework GUIX viene principalmente gestito dalla ricezione degli eventi inseriti nella coda degli eventi di GUIX. L'elaborazione di questi eventi viene eseguita nel contesto del thread GUIX, che è un thread ThreadX creato durante l'inizializzazione del sistema GUIX.

Le applicazioni GUIX definiscono l'interfaccia utente chiamando le funzioni dell'API GUIX per creare widget Windows e figlio e personalizzare l'aspetto di questi widget chiamando funzioni API aggiuntive usate per definire i colori, gli stili, i tipi di carattere e diversi altri attributi di ogni tipo di finestra o widget. Se si usa GUIX Studio per creare l'aspetto delle schermate dell'interfaccia utente, la maggior parte di queste operazioni di chiamata delle funzioni API di GUIX per creare la visualizzazione viene eseguita dall'applicazione GUIX Studio.

Le applicazioni GUIX interagiscono con l'utente di sistema e con la logica di business esterna gestendo gli eventi recuperati dalla coda degli eventi di GUIX.
Questi eventi vengono in genere prodotti da widget GUIX, ma possono anche essere creati da thread esterni. Quando viene eseguito il push di un tipico pulsante GUIX, il pulsante Invia un evento alla finestra padre del pulsante. Il programma dell'applicazione agirà sul push del pulsante fornendo un gestore per l'evento push del pulsante.

I thread GUIX aggiuntivi vengono spesso creati per elementi quali i driver di input. Un driver di input della schermata di tocco tipico viene eseguito come thread autonomo esterno al thread principale GUIX. Il driver di input tocco Invia le informazioni sul tocco al thread GUIX inviando gli eventi nella coda degli eventi di GUIX.

Poiché molte operazioni dell'interfaccia utente, ad esempio le animazioni, richiedono informazioni accurate sugli intervalli, GUIX implementa anche un'interfaccia timer semplice e semplice da usare. Questa interfaccia del timer si basa sul servizio timer ThreadX e viene configurata automaticamente all'avvio del sistema.

La maggior parte del software GUIX è indipendente dalle dipendenze hardware. Il Framework richiede driver di input specifici dell'hardware e driver grafici specifici dell'hardware. I dettagli del modo in cui vengono implementati questi driver specifici dell'hardware vengono rinviati al capitolo 5.

## <a name="initialization"></a>Inizializzazione 

Il ***gx_system_initialize*** del servizio deve essere chiamato prima di chiamare qualsiasi altro servizio GUIX. L'inizializzazione del sistema GUIX può essere chiamata dalla routine di ***Tx_application_define*** threadX (contesto di inizializzazione) o dai thread dell'applicazione. La funzione ***gx_system_initialize*** crea la coda degli eventi GUIX, Inizializza la funzionalità del timer GUIX, crea il thread di sistema GUIX principale e inizializza varie strutture di dati gestite da GUIX durante l'esecuzione dell'applicazione.

Una volta restituito ***gx_system_initialize*** , l'applicazione è pronta per creare visualizzazioni, Canvas, finestre, widget e personalizzare le proprietà di tutti gli oggetti GUIX. Gran parte dell'API per la creazione di oggetti GUIX può essere chiamata da ***tx_application_define*** o dai thread dell'applicazione.

## <a name="application-interface-calls"></a>Chiamate dell'interfaccia dell'applicazione 

Le chiamate dall'applicazione vengono eseguite in gran parte dal ***tx_application_define*** (contesto di inizializzazione) o dai thread dell'applicazione. Vedere la sezione "consentito da" di ogni API GUIX descritta nel capitolo 4 per determinare il contesto dal quale può essere chiamato.

Nella maggior parte dei casi, le attività a elevato utilizzo di elaborazione vengono posticipate al thread GUIX interno, inclusi tutti i processi di elaborazione degli eventi e di finestra.

Le funzioni API GUIX possono essere chiamate da qualsiasi thread in qualsiasi momento.
Tuttavia, viene in genere considerata un'architettura migliore per separare la logica di business critica per il tempo dalla logica dell'interfaccia utente. Poiché le operazioni di disegno dell'interfaccia utente possono richiedere molto tempo a seconda delle dimensioni di visualizzazione e delle prestazioni della CPU, in genere non si desidera che i thread critici per il tempo attendano un ritardo per il completamento di un'operazione di disegno.

## <a name="internal-guix-thread"></a>Thread GUIX interno 

Come indicato in precedenza, GUIX dispone di un thread interno che esegue la maggior parte dell'elaborazione dell'interfaccia utente grafica. Questo thread viene creato dal software dell'applicazione chiamando ***gx_system_initialize** _ seguito da _ *_gx_system_start_* *.

La priorità del thread GUIX interno è determinata da `#define GX_SYSTEM_THREAD_PRIORITY` . Per impostazione predefinita, questo valore è 16 (priorità intermedia), ma può essere modificato specificando questo valore nel file di intestazione gx_port. h o gx_user. h, eseguendo l'override del valore predefinito.

L'intervallo di tempo del thread GUIX viene definito in modo analogo da `#define GX_SYSTEM_THREAD_TIMESLICE` , che per impostazione predefinita corrisponde al valore 10 ms.

Lo stack sie del thread di sistema è determinato dall'oggetto `#define GX_THREAD_STACK_SIZE` , che si trova nel file di intestazione ***gx_port. h*** , ma può anche essere sottoposto a override specificando questo valore nel file di intestazione gx_user. h.

Il ciclo di esecuzione del thread GUIX interno è costituito da tre azioni.
In primo luogo, GUIX recupera gli eventi dalla coda degli eventi di GUIX e li invia per l'elaborazione da parte di GUIX Windows and widgets. Gli eventi vengono in genere inseriti nella coda degli eventi di GUIX per timer periodici, dispositivi di input come uno schermo touchscreen o una tastiera e da widget GUIX quando elaborano l'input dell'utente. Successivamente, dopo l'elaborazione di tutti gli eventi, GUIX determina se è necessario un aggiornamento dello schermo e, in tal caso, esegue l'elaborazione necessaria per aggiornare i dati grafici di visualizzazione, soprattutto chiamando le funzioni di disegno di tali finestre e widget che sono stati contrassegnati come dirty. Infine, GUIX sospende il thread GUIX fino a quando non arriva un nuovo evento di input o gli eventi.

## <a name="event-processing"></a>Elaborazione di eventi 

Gli eventi di input tocco o penna vengono elaborati determinando la finestra o il widget in primo piano sotto la posizione del pixel di input del tocco o della penna e chiamando la funzione di elaborazione degli eventi della finestra/widget. Se il widget riconosce gli eventi di input penna, l'evento verrà elaborato come appropriato per il tipo di widget. In caso contrario, il widget di primo livello passerà l'evento di input tocco o penna al padre del widget per l'elaborazione. Questo passaggio dell'evento fino alla catena continua fino a quando non viene gestito l'evento o l'evento arriva alla finestra radice, nel qual caso l'evento viene ignorato.

Gli eventi di tastiera vengono inviati alla finestra/widget con lo stato attivo per l'input. Lo stato dello stato attivo per l'input viene gestito dal componente gx_system di GUIX.

Gli eventi timer vengono sempre inviati alla finestra o al widget proprietario del timer per l'elaborazione.

Gli eventi generati internamente, ad esempio eventi click del pulsante o eventi di modifica del valore del dispositivo di scorrimento, vengono sempre inviati all'elemento padre del widget che genera l'evento. Se l'elemento padre non elabora l'evento, viene passato alla catena simile agli eventi di input tocco o penna.

## <a name="drawing"></a>Disegno 

Una volta completata l'elaborazione di tutti gli eventi, il thread interno di GUIX determina se è necessario un aggiornamento dello schermo e in tal caso vengono chiamate le funzioni di disegno finestra/widget appropriate. Al termine del disegno, il thread interno di GUIX attende semplicemente la coda degli eventi per l'elaborazione del successivo evento GUIX.

GUIX implementa il concetto di *aree dirty*, ovvero aree che devono essere ridisegnate, per ogni widget e Canvas. Un widget può essere disegnato solo in aree precedentemente contrassegnate come dirty. Quando viene chiamata una funzione di disegno di widget, tutte le operazioni di disegno vengono ritagliate internamente nel rettangolo modificato precedentemente definito.
I tentativi di estrazione al di fuori di quest'area verranno ignorati.

I widget e Windows si contrassegnano come Dirty chiamando la funzione API ***gx_system_dirty_mark***. Questa funzione contrassegna l'intero widget o finestra come necessario per essere ridisegnato. Una seconda funzione, ***gx_system_dirty_partial_add***, può essere richiamata come alternativa per contrassegnare come Dirty solo una parte di una finestra o un widget.

Questo modello di contrassegnare i widget come Dirty e quindi ridisegnare tali widget solo quando tutti gli eventi di input sono stati elaborati viene definito *disegno posticipato*. L'algoritmo di disegno posticipato di GUIX e la manutenzione degli elenchi Dirty sono progettati per migliorare l'efficienza del disegno. Poiché le operazioni di disegno sono in genere costose, GUIX funziona duramente per impedire il disegno non necessario.

Il disegno viene eseguito in un' *area* di disegno GUIX. Un'area di disegno è un'area di memoria riservata per conservare i dati grafici. Un'area di disegno può essere collegata direttamente al buffer dei frame hardware, a seconda dell'architettura di sistema e dei vincoli di memoria. Prima di poter eseguire qualsiasi disegno, è necessario innanzitutto aprire un'area di disegno per il disegno chiamando la funzione API ***gx_canvas_drawing_initiate*** . Questa API prepara un'area di disegno per il disegno e stabilisce il *contesto di disegno* corrente. Quando GUIX esegue un aggiornamento Canvas di sistema, l'area di disegno viene aperta per il disegno e il contesto di disegno stabilito prima che vengano richiamate le API di disegno a livello di widget. Di conseguenza, non è necessario che i widget avviino il disegno in un'area di disegno all'interno della funzione di disegno widget.

Tuttavia, se un'applicazione desidera eseguire il disegno immediato su un'area di disegno, all'esterno del flusso dell'algoritmo di disegno posticipato GUIX standard, l'applicazione deve richiamare direttamente il ***gx_canvas_drawing_initiate*** prima di chiamare qualsiasi altra funzione API di disegno e deve chiamare ***gx_canvas_drawing_complete*** una volta completato il disegno immediato.

## <a name="user-input"></a>Input utente 

GUIX supporta i dispositivi touch screen, mouse e tastiera con tipi di eventi predefiniti. I dispositivi di input aggiuntivi possono essere usati definendo tipi di evento personalizzati o eseguendo il mapping del dispositivo di input personalizzato ai tipi di evento predefiniti.

Le azioni associate a questi dispositivi vengono convertite in eventi elaborati dal thread interno di GUIX. Il software a livello di driver scritto per supportare un touch screen deve prepararsi e inviare agli eventi della coda di eventi GUIX per le operazioni di penna, penna e penna. Analogamente, un driver di input della tastiera deve generare eventi per l'input della chiave e della versione della chiave.

## <a name="modal-dialog-execution"></a>Esecuzione modale della finestra di dialogo 

L'esecuzione modale della finestra di dialogo si riferisce alla presentazione di una finestra all'utente che deve essere chiusa in qualche modo prima che qualsiasi altra finestra o widget GUIX possa ricevere l'input dell'utente. Le finestre di dialogo modali acquisiscono tutti gli input utente mentre viene visualizzata la finestra di dialogo, indipendentemente dalla posizione x, y degli eventi di input tocco o del mouse.

Le finestre di dialogo modali vengono attivate dal software dell'applicazione creando prima di tutto la finestra in modo normale chiamando ***gx_window_create*** e chiamando quindi la funzione API GUIX ***gx_window_execute.***

Quando viene chiamata la funzione ***gx_window_execute*** , GUIX immette un ciclo di elaborazione di eventi locali. La funzione ***gx_window_execute*** non torna al chiamante finché la finestra di dialogo non viene chiusa, dall'input dell'utente o chiamando ***gx_window_close***. Per questo motivo, è molto importante non chiamare mai la funzione ***gx_window_execute*** da un thread diverso dal thread interno di GUIX.

## <a name="periodic-processing"></a>Elaborazione periodica 

Per fornire gli effetti di visualizzazione, l'animazione sprite e il supporto per le richieste periodiche dell'applicazione, GUIX usa un timer ThreadX. Questo singolo timer viene usato per gestire tutte le esigenze relative al tempo di GUIX. Per impostazione predefinita, la frequenza per l'elaborazione del timer interno GUIX è impostata su 20ms tramite la costante **GX_SYSTEM_TIMER_MS**, definita in **_gx_api. h_**, a meno che la costante non sia stata definita in precedenza nell'intestazione gx_port. h o gx_user. h. La frequenza predefinita può essere modificata dall'applicazione tramite un'opzione di compilazione quando si compila la libreria GUIX o ridefine in modo esplicito in ***gx_user. h***.

> [!IMPORTANT]
> Si noti che la frequenza del timer GUIX è espressa nei cicli del timer RTO ed è definita dalla costante **GX_SYSTEM_TIMER_TICKS**. Il valore di **GX_SYSTEM_TIMER_TICKS** viene calcolato utilizzando **GX_SYSTEM_TIMER_MS** e **TX_TIMER_TICKS_PER_SECOND**. Per modificare la frequenza e la risoluzione del timer GUIX, l'utente può ridefinire uno di questi valori in ***gx_port. h** _ o _ *_gx_user. h_**.

## <a name="display-driver"></a>Visualizza driver 

I driver di visualizzazione sono responsabili di fornire un set di funzioni di disegno al codice GUIX di base. L'implementazione di ciascuna di queste funzioni di disegno è determinata dal driver e, quando possibile, l'implementazione utilizzerà il supporto dell'accelerazione hardware. In generale, la funzione di disegno funziona scrivendo i dati dei pixel in un buffer di memoria, che può essere il buffer di frame fisico o un buffer secondario, a seconda dell'architettura del driver. Molti driver implementano il doppio buffer con due buffer di frame e questi buffer vengono disconnessi richiamando la funzione di attivazione/disinserimento del buffer. GUIX chiama queste funzioni internamente nei momenti appropriati. Per i sistemi con vincoli di memoria, le funzioni di disegno possono scrivere solo in un singolo buffer del frame di memoria.

GUIX fornisce implementazioni software predefinite di ogni funzione di disegno di basso livello a ogni profondità e formato dei colori del supporto. Queste funzioni vengono richiamate tramite puntatori a funzione mantenuti all'interno della struttura **GX_DISPLAY** . Quando vengono creati driver specifici dell'hardware, in genere sovrascriveranno un certo numero di puntatori a funzione con funzioni specifiche per l'hardware di destinazione.

Un driver di visualizzazione hardware tipico viene implementato creando prima il driver di visualizzazione GUIX predefinito per la profondità e il formato di colore richiesti.
Il driver hardware sostituirà quindi le funzioni che devono essere ottimizzate o personalizzate per l'implementazione hardware specifica.

GUIX supporta formati di colore pixel compresi tra 1-BPP monocromatico e 32-BPP a:r: g:b formato. GUIX supporta anche molte varianti all'interno di ogni ampia categoria di profondità del colore, ad esempio r:g: b rispetto a b:g: r ordine byte, pixel compresso rispetto a formati pixel allineati a Word e canali alfa. Attualmente sono supportati 25 formati di colore distinti, ma questo elenco cresce man mano che i fornitori di hardware offrono nuove varianti.

## <a name="display-memory-architectures"></a>Visualizzare le architetture di memoria

Varie destinazioni hardware e visualizzazioni usano un'ampia gamma di architetture di memoria di visualizzazione diverse, a seconda dei vincoli di memoria della destinazione e dei requisiti di funzionalità dell'applicazione. Di seguito vengono descritte alcune delle architetture di memoria comuni con una breve descrizione di ciascuna di esse.

Modello 1) nessun buffer di frame, dati grafici contenuti in un grammo esterno:

![Nessun buffer frame, dati grafici contenuti in un grammo esterno](./media/guix/user-guide/no-frame-buffer.png)

Nel modello precedente, nessuna memoria per un buffer di frame esiste in memoria locale per la CPU. Tutti i dati grafici vengono archiviati in un grammo esterno incorporato nella visualizzazione stessa. L'interfaccia per il grammo esterno può essere parallela o seriale. Questo tipo di architettura ha un costo molto basso; Tuttavia può presentare un effetto di strappo indesiderato quando i dati grafici vengono aggiornati.

Modello 2) un buffer di frame locale:

![Un buffer frame locale](./media/guix/user-guide/one-local-frame-buffer.png)

In questo modello, la memoria per i dati grafici viene allocata da una memoria ad accesso casuale che è direttamente accessibile alla CPU. È necessario che sia presente hardware dedicato per trasmettere ripetutamente i dati grafici (insieme ai segnali di temporizzazione) dalla memoria locale alla visualizzazione. Questo modello è diverso dal modello 1 perché la memoria grafica è un blocco della SRAM locale o della DRAM disponibile per la CPU. Potrebbe trattarsi della stessa memoria in cui si trovano le variabili dello stack e del programma.

Modello 3) buffer frame locale + grammo esterno:

![Buffer frame locale + grammo esterno](./media/guix/user-guide/local-frame-buffer-external-gram.png)

Il modello 3 è una combinazione dei primi due. In questo modello è disponibile una quantità di memoria locale sufficiente per mantenere un buffer del frame. Inoltre, il dispositivo di visualizzazione fornisce un grammo esterno e viene aggiornato automaticamente usando i dati forniti nel grammo. Questa architettura trae vantaggio dall'efficienza degli aggiornamenti migliorata perché è possibile trasferire la parte modificata del buffer dei frame locale al grammo esterno in un unico trasferimento a blocchi, spesso utilizzando canali DMA di onboarding. Questo modello Elimina inoltre lo strappo e lo sfarfallio che possono essere presenti in uno dei primi due modelli, perché solo i contenuti grafici completati vengono copiati nel grammo esterno.

Modello 4) buffer dei frame ping-pong:

![Buffer dei frame ping-pong](./media/guix/user-guide/ping-pong-frame-buffers.png)

Nel modello 4 è presente memoria sufficiente per fornire due buffer di frame locali. In questo caso, GUIX considera un buffer di frame come il buffer del frame attivo e l'altro come buffer del frame di lavoro. Quando è in corso un'operazione di creazione o aggiornamento dello schermo, viene eseguita nel buffer di lavoro. Al termine dell'operazione di disegno, i buffer vengono attivati e il buffer di lavoro diventa il buffer attivo e il buffer attivo diventa il buffer di lavoro. Questo modello Elimina inoltre lo sfarfallio dello schermo e lo strappo che possono essere osservati in un singolo sistema memorizzato nel buffer.

Modello 5) buffer ping-pong con composizione Canvas:

![Buffer ping-pong con composizione Canvas](./media/guix/user-guide/ping-pong-buffers-canvas-composting.png)

Nel modello 5 è possibile creare un numero qualsiasi di Canvas, fino ai limiti della memoria disponibile. Le area di disegno possono essere sovrapposte o combinate come definito dall'applicazione per creare il composito Canvas. Quando viene creata una nuova composizione dopo un'operazione di aggiornamento dello schermo, i buffer compositi attivi e di lavoro vengono attivati o disattivati in un'operazione identica all'architettura del buffer ping-pong standard. Il modello 5 aggiunge la possibilità di eseguire operazioni di dissolvenza dello schermo e di fusione combinando le Canvas nell'output finale composito.

Modello 6) composizione Canvas con grammo esterno:

![Composizione Canvas con grammo esterno](./media/guix/user-guide/canvas-compositing-external-gram.png)

Il modello 6 è una lieve variazione sul modello 5, in cui è necessario un solo buffer composito e il buffer composito viene quindi trasferito al grammo esterno. Questo modello supporta inoltre la fusione a schermo intero e le sovrimpressioni.

## <a name="string-encoding"></a>Codifica di stringhe 

Per impostazione predefinita, GUIX supporta la codifica della stringa di formato UTF8. Il supporto per la codifica di stringhe UTF8 può essere disabilitato definendo **GX_DISABLE_UTF8_SUPPORT** nel file di intestazione ***gx_user. h*** . Se la codifica UTF8 è disabilitata, GUIX utilizzerà internamente solo la codifica di caratteri ASCII a 8 bit standard più latino-1. La disabilitazione della codifica di stringhe UTF8 produce un footprint della libreria GUIX leggermente più piccolo e un'esecuzione di runtime leggermente più veloce delle funzioni di gestione delle stringhe e di disegno del testo.

La codifica di stringhe UTF8 presenta i tratti seguenti:

  - Le stringhe ASCII non accettano più spazio di archiviazione rispetto alla codifica ASCII a 7 bit standard.

  - La maggior parte delle funzioni di stringa ANSI-C funziona con la codifica di stringhe UTF8 senza modifiche.

Tutti i set di caratteri attivi nel mondo, inclusi i set di caratteri kanji, possono essere rappresentati con la codifica di stringhe UTF8.

### <a name="static-and-dynamic-strings"></a>Stringhe statiche e dinamiche 

Le stringhe assegnate ai widget GUIX che supportano la visualizzazione di testo possono essere costanti definite in modo statico, che in genere vengono inserite nell'archivio costante come parte della tabella di stringhe GUIX descritta di seguito e stringhe definite in modo dinamico, ovvero stringhe generate in fase di esecuzione usando servizi quali ***sprintf** _ o _ *_gx_utility_ltoa_* *.

Esempi di stringhe dinamiche possono includere un valore visualizzato sotto forma di numero in un widget della richiesta di GUIX o una stringa "Time/date", formattata dinamicamente in base alla posizione e alle preferenze di formato dell'utente. Se si creano stringhe in fase di esecuzione che verranno assegnate ai widget GUIX, ad esempio **GX_PROMPT** o **GX_TEXT_BUTTON widget**, è necessario scegliere di allocare in modo statico lo spazio di archiviazione per queste stringhe generate in fase di esecuzione, ad esempio
matrici di caratteri globali, oppure è possibile definire e installare una funzione di allocatore di memoria dinamica e usare lo stile **GX_STYLE_TEXT_COPY** , che indica a tali widget di creare una copia privata delle stringhe di testo assegnate.

Si tratta di un errore di programmazione per usare l'archiviazione temporanea, ad esempio una matrice di caratteri automatica, per contenere una stringa generata dinamicamente e quindi assegnare questa stringa a un widget senza lo stile **GX_STYLE_TEXT_COPY** . Quando questo stile non è abilitato, il widget copia semplicemente il puntatore di stringa fornito e i dati di stringa devono essere allocati in modo statico oppure il puntatore della stringa del widget probabilmente finirà puntando ai dati di Garbage Collection che producono risultati imprevedibili.

### <a name="passing-gx_string-arguments"></a>Passaggio di argomenti GX_STRING 

Le funzioni API GUIX che accettano un parametro GX_STRING verificano sempre che la lunghezza della stringa a cui punta il campo **GX_STRING. gx_string_ptr** corrisponda al valore del campo **GX_STRING. gx_string_length** . Se i due campi non sono coerenti, viene restituito un errore di **GX_INVALID_STRING_LENGTH** e l'API chiamata restituisce senza accettare l'assegnazione di stringa.

Per motivi di sicurezza, il software GUIX non usa mai internamente le funzioni stringa C standard, ad esempio ***strlen** _ o _ *_strcpy_* *. Queste funzioni sono note a essere suscettibili ad attacchi dannosi quando i dati di stringa vengono acquisiti dinamicamente, come spesso accade con le applicazioni connesse.

Le versioni della libreria GUIX precedenti alla versione 5,6 hanno definito funzioni API che accettano ( `GX_CONST GX_CHAR *text` ) come parametro. Queste funzioni, sebbene ancora supportate per la compatibilità con le versioni precedenti, sono state obsolete e sostituite dalle funzioni API preferite che accettano ( `GX_CONST GX_STRING *string` ) come parametro di input.

Per impostazione predefinita, l'API di gestione del testo deprecata è abilitata per consentire a tutte le applicazioni precedentemente scritte di compilare con gli aggiornamenti più recenti della libreria GUIX. Per disabilitare l'API di gestione del testo deprecata, è necessario aggiungere la definizione **GX_DISABLE_DEPRECATED_STRING_API** al **file di intestazione _gx_user. h_*_. Tutte le nuove applicazioni devono definire _* GX_DISABLE_DEPRECATED_STRING_API** e utilizzare solo le funzioni API di sostituzione. Tutti i file di output generati da GUIX Studio per la versione della libreria GUIX versione 5,6 o successiva utilizzeranno solo le funzioni API di sostituzione.

Nella tabella seguente sono elencati i nomi delle funzioni API di sostituzione deprecate e appena definite:

| **Nome della funzione deprecata**              | **Sostituito con**                              |
| ------------------------------------------ | ----------------------------------------------- |
| gx_binres_language_table_load          | gx_binres_language_table_load_ext          |
| gx_canvas_rotated_text_draw            | gx_canvas_rotated_text_draw_ext            |
| gx_canvas_text_draw                     | gx_canvas_text_draw_ext                     |
| gx_context_string_get                   | gx_context_string_get_ext                   |
| gx_display_language_table_get          | gx_display_language_table_get_ext          |
| gx_display_language_table_set          | gx_display_language_table_set_ext          |
| gx_display_string_get                   | gx_display_string_get_ext                   |
| gx_display_string_table_get            | gx_display_string_table_get_ext            |
| gx_multi_line_text_button_text_set   | gx_multi_line_text_button_text_set_ext   |
| gx_multi_line_text_input_char_insert | gx_multi_line_text_input_char_insert_ext |
| gx_multi_line_text_input_text_set    | gx_multi_line_text_input_text_set_ext    |
| gx_multi_line_text_view_text_set     | gx_multi_line_text_view_text_set_ext     |
| gx_prompt_text_get                      | gx_prompt_text_get_ext                      |
| gx_prompt_text_set                      | gx_prompt_text_set_ext                      |
| gx_single_line_text_input_text_set   | gx_single_line_text_input_text_set_ext   |
| gx_system_string_width_get             | gx_system_string_width_get_ext             |
| gx_system_version_string_get           | gx_system_version_string_get_ext           |
| gx_text_button_text_get                | gx_text_button_text_get_ext                |
| gx_text_button_text_set                | gx_text_button_text_set_ext                |
| gx_text_scroll_wheel_callback_set     | gx_text_scroll_wheel_callback_set_ext     |
| gx_utility_string_to_alphamap          | gx_utility_string_to_alphamap_ext          |
| gx_widget_string_get                    | gx_widget_string_get_ext                    |
| gx_widget_text_blend                    | gx_widget_text_blend_ext                    |
| gx_widget_text_draw                     | gx_widget_text_draw_ext                     |

### <a name="guix-string-table"></a>Tabella di stringhe GUIX 

La tabella di stringhe GUIX e le risorse di stringa sono registrate con un'istanza di visualizzazione GUIX.

Ogni visualizzazione in un sistema a più schermi ha una propria tabella di stringhe e ogni visualizzazione può essere eseguita nella propria lingua selezionata. Gli altri tipi di risorse GUIX (colori, tipi di carattere e pixelmaps) vengono gestiti anche dal componente di visualizzazione GUIX, in quanto questi tipi di risorse sono specifici per ogni formato di colore di visualizzazione e profondità dei colori.

Sebbene sia possibile creare manualmente la tabella delle stringhe dell'applicazione, nella maggior parte dei casi la tabella delle stringhe di visualizzazione viene definita dall'applicazione GUIX Studio come parte del file di risorse del progetto. Le lingue disponibili sono definite anche nel file di intestazione della risorsa. La tabella della stringa di visualizzazione è una tabella a più colonne di puntatori alle stringhe dell'applicazione. Ogni colonna della tabella di stringhe rappresenta una lingua supportata dall'applicazione.
Se l'applicazione supporta solo una lingua, ad esempio l'inglese, nella tabella delle stringhe sarà presente una sola colonna. È comunque possibile aggiungere il supporto per lingue aggiuntive in qualsiasi momento senza modificare il software dell'applicazione.

La tabella delle stringhe attive viene assegnata chiamando la funzione API ***gx_display_string_table_set*** . Questa funzione viene chiamata automaticamente dal codice di avvio generato da GUIX studio, ma può anche essere chiamata direttamente dall'applicazione per modificare la tabella delle stringhe attive.

La lingua attiva viene assegnata chiamando la funzione API ***gx_display_active_language_set*** . Questa funzione determina la colonna della tabella delle stringhe di visualizzazione attiva.

Quando questa funzione viene richiamata, un evento **GX_EVENT_LANGUAGE_CHANGE** viene inviato a tutti i widget GUIX visibili, consentendo loro di eseguire l'aggiornamento per visualizzare i dati della stringa appena attiva.

I widget e il software applicativo risolvono le stringhe definite in modo statico usando i valori ID di stringa e le funzioni API ***gx_display_string_get_ext*** o ***gx_widget_string_get_ext*** . Queste funzioni restituiscono il **GX_STRING** associato a un ID di stringa specificato e al linguaggio attualmente attivo.

### <a name="bi-directional-text-display"></a>Visualizzazione del testo bidirezionale 

GUIX forniscono due strategie per il supporto di testo bidirezionale.

Un'opzione consiste nell'eseguire il riordino del testo bidi nell'applicazione GUIX Studio. L'uso di questa opzione GUIX studio è responsabile della generazione del testo bidi nel file di output nell'ordine di visualizzazione. Questa soluzione ha un effetto zero sulle prestazioni di runtime e non richiede alcuna aggiunta alla libreria di runtime GUIX. Per consentire a GUIX studio di generare stringhe di testo bidi displayorder, è necessario selezionare la casella di controllo **genera testo bidi in ordine di visualizzazione** nella finestra di dialogo di configurazione della lingua di GUIX Studio:

![Configurare le lingue](./media/guix/user-guide/configure-languages.png)

Con queste opzioni selezionate, il file di risorse generato conterrà le stringhe BiDi generate in ordine di visualizzazione e non è richiesta alcuna elaborazione aggiuntiva all'interno della libreria di runtime GUIX.

La seconda opzione consiste nell'eseguire il riordino del testo bidi in fase di esecuzione. Questa opzione è supportata per le applicazioni che devono gestire la stringa di testo bidi che sono definite in modo dinamico e non vengono generate dall'applicazione GUIX Studio. In questo caso la libreria di runtime GUIX è responsabile del riordinamento del testo bidi prima di disegnare ogni stringa di testo. Questa soluzione ha un effetto di prestazioni e memoria in fase di esecuzione. Per il processo di riordinamento del testo bidi è necessario che sia disponibile memoria dinamica sufficiente. Questa soluzione richiede che il GX_DYNAMIC_BIDI_TEXT_SUPPORT condizionale venga definito durante la compilazione della libreria GUIX. Vengono fornite due funzioni API ***gx_system_bidi_text_enable*** e ***gx_system_bidi_text_disable*** per abilitare o disabilitare il supporto del testo bidi in fase di esecuzione.

Non usare entrambi **GX_DYNAMIC_BIDI_TEXT_SUPPORT** e configurare GUIX Studio per generare il testo bidi in ordine di visualizzazione. È necessario selezionare una strategia o l'altra per la gestione delle stringhe di testo bidi.

## <a name="memory-usage"></a>Utilizzo memoria 

GUIX si trova insieme al programma applicativo. Di conseguenza, l'utilizzo della memoria statica (o della memoria fissa) di GUIX è determinato dagli strumenti di sviluppo; ad esempio, il compilatore, il linker e il localizzatore. L'utilizzo della memoria dinamica (o della memoria di run-time) è sotto il controllo diretto dell'applicazione.

### <a name="static-memory-usage"></a>Utilizzo memoria statica 

La maggior parte degli strumenti di sviluppo divide l'immagine del programma applicativa in cinque aree di base: *istruzione*, *costante*, *dati inizializzati*, *dati non inizializzati* e *stack di thread GUIX*. Nella figura X della pagina X viene illustrato un esempio di queste aree di memoria.

È importante comprendere che questo è solo un esempio. Il layout di memoria statica effettivo è specifico del processore, degli strumenti di sviluppo, dell'hardware sottostante e dell'applicazione stessa.

L'area di istruzioni contiene tutte le istruzioni del processore del programma. Questa area è spesso situata in ROM.

L'area costante contiene varie costanti compilate, che in GUIX contiene le impostazioni predefinite e tutte le risorse dell'applicazione (immagini, stringhe, tipi di carattere e colori). Inoltre, quest'area contiene la "copia iniziale" dell'area dati inizializzata. Durante il processo di inizializzazione del compilatore, questa parte dell'area costante viene utilizzata per configurare i dati globali inizializzati in RAM. L'area costante è in genere il più grande e in genere segue l'area di istruzioni e spesso si trova nella ROM.

GUIX pixelmaps e i tipi di carattere richiedono in genere grandi quantità di dati di archiviazione costanti. Queste aree dati statiche di grandi dimensioni vengono normalmente mantenute in ROM o FLASH.

Lo stack di thread GUIX viene definito all'interno dell'area dati non inizializzata, come variabile globale, nel file ***gx_system. h*** , come indicato di seguito:

```C
_gx_system_thread_stack[GX_THREAD_STACK_SIZE];
```

**GX_THREAD_STACK_SIZE** è definito in **_gx_port. h_**, ma è possibile eseguirne l'override dall'applicazione definendo questo simbolo nel file di intestazione ***gx_user. h*** oppure tramite le opzioni del progetto o i parametri della riga di comando. La dimensione dello stack deve essere sufficientemente grande da consentire la gestione degli eventi peggiori e le chiamate di disegno nidificate.

### <a name="dynamic-memory-usage"></a>Utilizzo memoria dinamica 

Come indicato in precedenza, l'utilizzo della memoria dinamica è sotto il controllo diretto dell'applicazione. I blocchi di controllo e la memoria associati alle Canvas e così via possono essere posizionati in qualsiasi punto dello spazio di memoria della destinazione. Si tratta di una funzionalità importante perché facilita l'utilizzo di diversi tipi di memoria fisica, in fase di esecuzione.

Si supponga, ad esempio, che un ambiente hardware di destinazione disponga sia di memoria veloce che di memoria lenta. Se l'applicazione richiede prestazioni aggiuntive per il disegno, è possibile inserire in modo esplicito nell'area di memoria ad alta velocità la memoria di Canvas per ottenere prestazioni ottimali.

Diverse funzionalità e servizi GUIX facoltativi richiedono un meccanismo di allocazione della memoria dinamica in fase di esecuzione, noto come heap. Questi servizi e funzionalità sono completamente facoltativi e molte applicazioni GUIX non utilizzano heap e non definiscono un meccanismo di allocazione della memoria di Runtime.

Se si utilizzeranno servizi che richiedono l'allocazione della memoria di runtime, è necessario installare le funzioni che GUIX chiamerà quando la memoria deve essere allocata o liberata in modo dinamico. È possibile implementare queste funzioni come si preferisce, in modo che anche in questo caso il percorso del pool di memoria dinamica sia sotto il controllo dell'applicazione. Per installare il supporto per l'allocazione di memoria dinamica, l'applicazione deve richiamare il servizio API ***gx_system_memory_allocator_set*** durante l'avvio del programma per definire l'allocazione di memoria e i servizi di memoria libera. Per un esempio completo, vedere la documentazione di questa API.

I servizi GUIX che richiedono un servizio di allocazione e deallocazione della memoria di Runtime includono:

  - Caricamento di risorse binarie dall'archiviazione esterna all'ambiente di runtime GUIX.

  - Il decodificatore di immagini JPEG di runtime software.

  - Il decodificatore di immagini PNG di runtime software.

  - Uso di widget di testo con GX_STYLE_TEXT_COPY.

  - Funzioni di utilità di ridimensionamento e rotazione del runtime pixemap.
  - Schermata di runtime e l'allocazione di blocchi di controllo widget.

Per le applicazioni più piccole, le risorse GUIX vengono in genere compilate e collegate in modo statico come parte dell'immagine dell'applicazione e l'installazione delle risorse binarie non è necessaria. Le risorse binarie consentono a un'applicazione di installare le risorse (tipi di carattere, immagini, lingue) in fase di esecuzione caricate da un percorso di archiviazione, ad esempio un'unità flash o un URL.

I decodificatori JPEG e PNG di runtime sono componenti facoltativi. La maggior parte delle applicazioni GUIX consente allo strumento GUIX studio di pre-decodificare tutti i file di immagine necessari e di archiviarli come risorse di dati GUIX Pixemap proprietarie. Questi servizi vengono forniti per completezza per le applicazioni che richiedono la conversione del runtime di immagini JPEG e/o PNG nel formato Pixelmap.

**GX_STYLE_TEXT_COPY** consente all'utente di specificare che uno specifico widget o widget manterrà la propria copia privata del testo assegnato dinamicamente. Per usare questa opzione è necessario che il meccanismo di allocazione della memoria sia installato prima di usare. Se questo flag di stile **<span class="underline">non</span>** viene specificato quando viene creato un widget di tipo testo, l'applicazione deve allocare le aree di archiviazione statiche per tutte le stringhe di testo create dinamicamente e assegnate. Le variabili automatiche non devono essere usate in questo caso per contenere dati di stringa generati in fase di esecuzione. Se lo stile del **GX_STYLE_TEXT_COPY** è abilitato, le variabili automatiche possono essere usate per contenere i dati stringa assegnati ai widget GUIX, perché ogni widget creerà una propria copia del testo assegnato.

Le funzioni di utilità di ridimensionamento e rotazione Pixelmap restituiscono il Pixelmap convertito risultante come nuovo Pixelmap disponibile per l'applicazione.
Se vengono usati questi servizi, è necessario che sia disponibile memoria dinamica sufficiente per contenere questi blocchi di dati Pixelmap generati dal runtime.

Infine, i blocchi di controllo per le schermate e i widget GUIX possono essere allocati in modo statico o dinamico. Per le applicazioni più piccole, è comune creare tutte le schermate dell'applicazione durante l'avvio del programma e utilizzare blocchi di controllo allocati in modo statico. Per le applicazioni di grandi dimensioni, è normale creare i controlli widget schermata e figlio in modo dinamico in base alle esigenze. I blocchi di controllo allocati dinamicamente vengono specificati selezionando la casella di controllo **Runtime allocate** nella visualizzazione delle proprietà di GUIX Studio oppure passando il flag di stile **GX_STYLE_DYNAMICALLY_ALLOCATED** quando si crea un widget tramite l'API standard. L'uso di blocchi di controllo widget allocati dinamicamente richiede che i servizi di allocazione e deallocazione della memoria siano definiti come descritto in precedenza.

## <a name="guix-components"></a>Componenti di GUIX 

Le API GUIX sono divise e organizzate in diversi gruppi di base che corrispondono ai componenti fondamentali del sistema GUIX. I componenti fondamentali includono:

| <!-- -->    | <!-- -->    |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GX_SYSTEM  | Componente di sistema GUIX, responsabile di inizializzazione, eventi, timer, tabelle di stringhe e gestione della gerarchia dei widget visibile.                                                                                                                                                                                                                                                                      |
| GX_CANVAS  | Area di disegno. Un'area di disegno può essere un'astrazione sottile del buffer dei frame hardware oppure può anche essere un'area di disegno della memoria pura. Il tipo di area di disegno è determinato dai parametri passati alla funzione API gx_canvas_create.                                                                                                                                                                                   |
| GX_CONTEXT | Componente del contesto del disegno. Il contesto di disegno contiene informazioni sulla schermata, l'area di disegno, il pennello e l'area di ridimensionamento per le operazioni di disegno correnti.                                                                                                                                                                                                                                      |
| GX_DISPLAY | Fornisce le API e le implementazioni a livello di driver per consentire all'applicazione e ai widget GUIX di eseguire il disegno su un'area di disegno. GX_DISPLAY viene implementato per eseguire correttamente il rendering della grafica in ogni area di disegno usando il formato di colore richiesto dell'area di disegno. Il componente GX_DISPLAY gestisce anche le risorse (colori, tipi di carattere e pixelmaps) disponibili per i widget che disegnano in canvas collegati a ogni visualizzazione. |
| GX_WIDGET  | Oggetto widget visibile di base e API associate. Tutti i tipi di widget GUIX sono basati su o derivati dal tipo di GX_WIDGET di base.                                                                                                                                                                                                                                                                      |
| GX_UTILITY | In questo gruppo sono incluse funzioni di utilità per l'utilizzo di rettangoli, funzioni per la conversione di stringhe e funzioni matematiche non ANSI.                                                                                                                                                                                                                                                         |

Oltre a questi componenti di base, GUIX include le API univoche per ogni tipo di widget fornito nella libreria. Queste API sono descritte nel capitolo 4 di questo manuale dell'utente, "Descrizione dei servizi GUIX".

## <a name="guix-system-component"></a>Componente di sistema GUIX

Il componente di sistema GUIX offre diversi servizi globali per l'applicazione dell'interfaccia utente. Questi servizi includono: *inizializzazione, gestione degli eventi, gestione dello schermo, gestione delle risorse, gestione del timer* e *gestione dei widget*. Ogni servizio è essenziale per l'organizzazione del programma dell'applicazione e questi servizi vengono descritti in modo più dettagliato nelle sezioni secondarie seguenti.

### <a name="initialization"></a>Inizializzazione 

L'inizializzazione di GUIX viene eseguita dall'applicazione che chiama il servizio ***gx_system_initialize***, che può essere chiamato dall'applicazione dalla routine ***tx_application_define*** threadX (contesto di inizializzazione) o dai thread dell'applicazione. La funzione ***gx_system_initialize*** Inizializza tutte le strutture di dati globali GUIX e crea il mutex di sistema GUIX, la coda degli eventi, il timer e il thread. Una volta che ***gx_system_initialize*** restituisce, l'applicazione può usare GUIX.

### <a name="thread-processing"></a>Elaborazione thread 

Il thread interno di GUIX, creato durante l'inizializzazione, è responsabile della maggior parte dell'elaborazione in GUIX. L'elaborazione in questo thread completa innanzitutto qualsiasi inizializzazione aggiuntiva richiesta dal driver di visualizzazione sottostante. Al termine dell'operazione, il thread GUIX entra in un ciclo che elabora tutti gli eventi presenti nella coda degli eventi di GUIX e quindi aggiorna la schermata, se necessario. L'aggiornamento dello schermo esegue le funzioni di disegno GUIX necessarie in base a ciò che è visibile ed è stato contrassegnato come Dirty significa che deve essere ridisegnato. Quando non sono presenti eventi e non è rimasto alcun elemento da aggiornare sullo schermo, il thread GUIX verrà sospeso, in attesa dell'arrivo del successivo evento GUIX.

### <a name="rtos-binding"></a>Binding RTO 

Il componente di sistema GUIX è configurato per impostazione predefinita in modo da utilizzare il sistema operativo ThreadX in tempo reale per servizi quali servizi thread, servizi di Accodamento eventi e servizi timer. GUIX può essere facilmente trasferito ad altri sistemi operativi usando la direttiva per il preprocessore GX_DISABLE_THREADX_BINDING e ricompilando la libreria GUIX. Questa operazione rimuove le dipendenze ThreadX dal codice sorgente GUIX e consente allo sviluppatore di applicazioni di implementare i servizi del sistema operativo richiesti usando qualsiasi RTO fornito dal sistema di destinazione. [Appendice F-GUIX RTO binding Services](appendix-f.md) descrive i servizi che devono essere implementati per la porta GUIX in un sistema operativo diverso dal sistema operativo threadX.

### <a name="multithread-safety"></a>Sicurezza multithread 

L'API GUIX è disponibile dal contesto del thread GUIX e da altri thread dell'applicazione. I thread dell'applicazione possono interagire con il thread GUIX inviando e ricevendo eventi, accedendo a variabili condivise e usando le funzioni dell'API GUIX. GUIX usa un mutex ThreadX interno per la protezione delle risorse multithread. Inoltre, GUIX impedisce la modifica della struttura interna dei widget visibili dopo l'inizio di un'operazione di aggiornamento dello schermo. Le API che modificano l'albero degli oggetti visibili vengono bloccate durante l'esecuzione delle operazioni di disegno e rilasciate al termine dell'aggiornamento dello schermo.

### <a name="system-timers"></a>Timer di sistema 

GUIX fornisce l'applicazione con timer periodici, che vengono spesso usati per l'aggiornamento periodico dei dati visualizzati nelle finestre di GUIX. Questa operazione viene eseguita tramite un timer periodico ThreadX, che viene usato anche per eseguire gli effetti a livello di sistema GUIX, ad esempio la dissolvenza dello schermo in entrata/in uscita e così via.

L'applicazione può creare timer e utilizzare la stessa funzionalità del timer utilizzata internamente da GUIX. Naturalmente, l'applicazione può anche creare e usare direttamente i timer ThreadX, se necessario. Il vantaggio dei timer GUIX è che sono molto facili da usare e sono preconfigurati per funzionare all'interno del sistema di elaborazione basato su eventi di GUIX.

Per creare e avviare un timer GUIX, l'applicazione deve richiamare la funzione ***gx_system_timer_start***. I parametri di questa funzione includono un puntatore al widget chiamante, l'ID del timer, che consente a un widget di avviare molti timer, e i valori di timeout iniziali e di ripianificazione. Se il valore di timeout della ripianificazione è 0, il timer verrà eseguito una sola volta e verrà eliminato dall'elenco dei timer attivi una volta scaduto.

Una volta avviata, il timer GUIX invierà GX_EVENT_TIMEOUT eventi al proprietario del timer, una volta o periodicamente, a seconda del valore della ripianificazione del timer. Un timer GUIX può essere arrestato chiamando la funzione API ***gx_system_timer_stop***.

### <a name="pen-speed-configuration"></a>Configurazione della velocità della penna 

Il componente di sistema GUIX include informazioni di configurazione correlate al rilevamento della velocità della penna. GUIX generato internamente **GX_EVENT_VERTICAL_FLICK** e **GX_EVENT_HORIZONTAL_FLICK** eventi in base alla velocità e alla distanza degli eventi PEN_DOWN generati dal driver di input tocco, se presenti. L'applicazione può configurare la distanza e la velocità minime necessarie per attivare questi eventi generati internamente usando la funzione API **_gx_system_pen_configure_** .

### <a name="screen-stack"></a>Stack di schermate 

Il componente di sistema GUIX fornisce servizi correlati allo stack dello schermo GUIX, una funzionalità facoltativa che supporta uno stack di widget virtuali in cui è possibile eseguire il push, il pop e il recupero delle schermate in fase di esecuzione da parte dell'applicazione. Lo stack di schermate è utile per la gestione di sistemi di menu complessi, in cui la route in base alla quale l'utente può arrivare a diversi Stati del sistema di menu è variata. Il ritorno allo stato precedente nel sistema di menu può essere facilmente eseguito inserendo prima lo stato della schermata precedente, visualizzando la nuova schermata e consentendo alla nuova schermata di estrarre lo stato precedente dallo stack dello schermo quando lo schermo corrente viene chiuso.

### <a name="clipboard-maintenance"></a>Manutenzione degli Appunti 

GUIX supporta gli Appunti per copiare e incollare testo durante l'esecuzione del runtime. Questo supporto viene fornito dal componente di sistema GUIX.

### <a name="dirty-list-maintenance"></a>Manutenzione elenco Dirty 

GUIX gestisce un elenco di widget Dirty, ovvero i widget visibili e che devono essere ridisegnato a causa di modifiche dello stato o di essere resi appena visibili. Questo elenco Dirty migliora le prestazioni di disegno consentendo a GUIX di eseguire un'operazione di aggiornamento Canvas per riflettere tutte le modifiche correnti apportate allo stato dell'interfaccia utente, anziché eseguire un aggiornamento Canvas quando viene apportata una modifica dell'interfaccia utente.
Questo elenco Dirty viene inoltre gestito dal componente di sistema GUIX.

### <a name="animation-control-block-pool"></a>Pool di blocchi di controllo animazione 

Le applicazioni spesso desiderano eseguire più sequenze di animazione, spesso in parallelo. GUIX gestisce un pool di blocchi di controllo di animazione da cui l'applicazione può allocare e usare. In questo modo l'applicazione può definire staticamente questi blocchi di controllo e consente di riutilizzarli in momenti diversi, anziché definire un blocco di controllo dell'animazione univoco per ogni animazione che l'applicazione potrebbe definire. Il pool di blocchi di controllo animazione viene inoltre gestito dal componente di sistema GUIX.

### <a name="system-error-handling"></a>Gestione degli errori di sistema 

Il gestore degli errori di sistema GUIX è progettato per consentire all'applicazione di individuare gli errori interni del sistema in GUIX che potrebbero risultare più difficili da determinare dal punto di vista dell'API. Ogni volta che si verifica un errore di sistema all'interno di GUIX, viene chiamata la funzione interna ***_gx_system_error_process*** . Questa funzione Salva il codice di errore fornito e incrementa il numero totale di errori di sistema rilevati. Le variabili di errore di sistema sono definite come segue:

UINT **_gx_system_last_error**;

**_GX_SYSTEM_ERROR_COUNT** ULONG;

Se l'applicazione GUIX funziona in modo anomalo, è utile esaminare la variabile Count degli errori nel debugger. Se è impostata, un modo efficace per risolvere il problema consiste nell'impostare un punto di interruzione nella funzione ***_gx_system_error_process*** e vedere quando/dove viene chiamato.

## <a name="guix-canvas-component"></a>Componente Canvas GUIX

Il componente Canvas è responsabile di tutte le operazioni di elaborazione correlate all'area di disegno. Un'area di disegno è effettivamente un buffer di frame virtuale. Per produrre output grafico, l'applicazione deve creare almeno un'area di disegno.
In genere, è necessario creare almeno un'area di disegno per ogni schermo fisico supportato dal sistema.

Tutto il disegno GUIX viene inserito in un'area di disegno. Nei sistemi più semplici o con vincoli di memoria, è probabile che sia presente solo un'area di disegno che potrebbe essere collegata direttamente al buffer dei frame visibile, mentre i sistemi con una maggiore quantità di memoria e requisiti grafici più avanzati potrebbero richiedere più Canvas. L'esecuzione di più Canvas disponibili per uno schermo Abilita funzionalità come gli effetti di dissolvenza dello schermo e della finestra.
I Canvas possono essere uno dei due tipi principali, semplice o gestito.

Una semplice area di disegno è un'area di disegno fuori schermo usata dall'applicazione.
GUIX non esegue alcuna operazione direttamente con un'area di disegno semplice, ma l'applicazione può utilizzare un'area di disegno semplice per eseguire il rendering del disegno complesso in un buffer fuori schermo, quindi utilizzare questo buffer fuori schermo per aggiornare l'area di disegno visibile quando necessario.

Un'area di disegno gestita viene automaticamente visualizzata all'interno del buffer dei frame hardware di GUIX. Un'area di disegno gestita è inclusa nella creazione di un'area di disegno composta per i sistemi con memoria sufficiente per supportare più Canvas gestite. Le Canvas gestite hanno un ordine Z gestito da GUIX e il ritaglio delle visualizzazioni viene applicato a tutte le Canvas gestite.

Un'area di disegno è diversa da un buffer di frame perché è più generica. Nei sistemi con vincoli di memoria può essere presente una sola area di disegno e la memoria per questa area di disegno potrebbe essere la memoria del buffer dei frame visibile. Tuttavia, per i sistemi più complessi che supportano sovrimpressioni grafiche più avanzate e più Canvas, le aree di disegno gestite sono allocate in ogni area di memoria, che sono distinte dalla memoria buffer dei frame hardware.
Questi Canvas gestiti vengono sottoposti a rendering nel buffer del frame visibile durante l'operazione di aggiornamento o di attivazione del buffer dei frame.

Per l'hardware che supporta più livelli grafici, ad esempio più buffer di frame sovrapposti, l'applicazione può associare una o più Canvas ai livelli grafici hardware usando l'API ***gx_canvas_hardware_layer_bind*** . Questo servizio informa l'area di disegno che è collegata a un particolare livello di grafica hardware e, una volta collegato, l'area di disegno tenterà di usare il supporto hardware per la visibilità dell'area di disegno, ad esempio gx_canvas_show, gx_canvas_hide), la fusione alfa di Canvas (ad esempio ***gx_canvas_alpha_set***) e l'offset dell'area di disegno all'interno della visualizzazione (***gx_canvas_offset_set***).

Per le architetture diverse dalla più semplice organizzazione del buffer a frame singolo/singolo, le dimensioni di un'area di disegno sono determinate dall'applicazione e possono essere diverse dalla dimensione fissa di un buffer di frame.
Può anche trovarsi in corrispondenza di un offset selezionato dall'applicazione. Altre informazioni, ad esempio l'ordine Z, vengono mantenute all'interno dell'area di disegno. Quando il disegno dell'area di disegno è completo, il contenuto dell'area di disegno viene trasferito alla visualizzazione fisica dal driver di visualizzazione. In alcuni sistemi che non dispongono di memoria sufficiente per le aree di memoria del buffer del frame e dell'area di disegno separate, l'aggiornamento dell'area di disegno viene effettivamente eseguito direttamente sullo schermo fisico tramite il driver di visualizzazione.

### <a name="canvas-creation"></a>Creazione Canvas 

È possibile creare un oggetto Canvas durante l'inizializzazione o in qualsiasi momento durante l'esecuzione dei thread dell'applicazione. Non esiste alcun limite al numero di oggetti Canvas che possono essere creati da un'applicazione. La maggior parte delle applicazioni, tuttavia, creerà un solo oggetto Canvas per tutto il disegno GUIX.

### <a name="canvas-control-block"></a>Blocco di controllo Canvas 

Le caratteristiche di ogni oggetto Canvas si trovano nel blocco di controllo **GX_CANVAS** ed è definito in **_gx_api. h_**. La memoria necessaria per un oggetto Canvas viene fornita dall'applicazione e può trovarsi in qualsiasi punto della memoria. Tuttavia, è più comune fare in modo che il blocco di controllo dell'oggetto Canvas e l'area di disegno siano una struttura globale definendoli al di fuori dell'ambito di qualsiasi funzione.

### <a name="canvas-alpha-channel"></a>Canale alfa Canvas

GUIX supporta la fusione alfa dei colori di primo piano e di sfondo su molti livelli, incluso il canale alfa bitmap che specifica un rapporto di fusione per pixel, il pennello alfa che specifica il rapporto di fusione per un pennello a 16 BPP e profondità del colore superiore e l'oggetto Canvas Alpha che specifica il rapporto di fusione per un'area di disegno sovrapposta.

Il valore alfa di un'area di disegno viene utilizzato quando sono presenti più Canvas composte insieme per la visualizzazione all'interno del buffer del frame. Se l'ordine Z dell'area di disegno è tale che un'area di disegno è sopra altre Canvas, il valore alfa dell'area di disegno può essere impostato in modo da fondere l'area di disegno con quelli che si trovano dietro. La modifica rapida del valore alfa di un'area di disegno viene utilizzata per fornire effetti di transizione dello schermo "dissolvenza", ma è possibile utilizzare in molti modi l'elemento Canvas Alpha.

Se un'area di disegno è associata a un livello grafico hardware usando gx_canvas_hardware_layer_bind (), GUIX tenterà di implementare la fusione alfa di Canvas utilizzando il supporto hardware, riducendo al minimo l'overhead software associato alla fusione di un'area di disegno sovrapposta.

I valori alfa variano da 0 a 255, dove un valore pari a 0 indica che il pixel è completamente trasparente e i valori maggiori di 0 aumentano se il valore alfa di Canvas trasparente può essere supportato solo per i driver dello schermo in esecuzione a 16 BPP e superiori, a meno che non venga fornita l'assistenza hardware per la fusione con Canvas.

### <a name="canvas-offset"></a>Offset Canvas 

È possibile sfalsare un'area di disegno all'interno del buffer di frame visibile richiamando il servizio API ***gx_canvas_offset_set*** . Gli offset Canvas vengono in genere usati per implementare animazioni sprite. Se un'area di disegno è associata a un livello grafico hardware richiamando la funzione API ***gx_canvas_hardware_layer_bind*** , GUIX tenterà di implementare le modifiche dell'offset Canvas utilizzando il supporto hardware, riducendo al minimo l'overhead del software associato allo spostamento della posizione dell'area di disegno.

### <a name="canvas-drawing"></a>Disegno Canvas 

Il componente Canvas GUIX fornisce un'API di disegno completa per l'applicazione. Prima di poter richiamare le API di disegno, ad esempio ***gx_canvas_line_draw*** o ***gx_canvas_pixelmap_draw*** , è necessario aprire l'area di disegno di destinazione per il disegno richiamando la funzione API ***gx_canvas_drawing_initiate*** . Questa funzione prepara un'area di disegno per il disegno e crea un ***contesto di disegno***.

Le API di disegno che eseguono il rendering nell'area di disegno, ad esempio ***gx_canvas_line_draw** _ o _*_gx_canvas_text_draw_*_, usano parametri trovati nel pennello del contesto di disegno corrente per definire lo stile, la larghezza e i colori della linea. Questi parametri del pennello vengono modificati chiamando il _*_gx_context_brush_define_*_, _* _gx_context_brush_set_* *, ***gx_context_brush_style_set**_ e funzioni API simili dopo che è stato stabilito un contesto di disegno chiamando _ *_gx_canvas_drawing_initiate_* *.

Quando GUIX richiama le funzioni finestra e disegno widget come parte di un'operazione di aggiornamento Canvas posticipata, l'area di disegno di destinazione viene aperta per il disegno prima di chiamare le funzioni di disegno del widget. Per questo motivo, non è necessario che le funzioni di disegno dei widget standard aprano l'area di disegno di destinazione.

In alcuni casi, l'applicazione potrebbe voler forzare il disegno immediato su un'area di disegno. In questo caso, l'applicazione può eseguire i passaggi seguenti.

1. Chiamare la funzione API ***gx_canvas_drawing_initiate*** , passando l'area di disegno di destinazione e il rettangolo all'interno dell'area di disegno in cui l'applicazione vuole creare. 

2. Per eseguire il disegno desiderato, chiamare un numero qualsiasi di API di disegno Canvas.

3. Chiamare la funzione API ***gx_canvas_drawing_complete*** per segnalare che il disegno è stato completato. In questo modo l'area di disegno viene scaricata nel buffer di frame visibile e/o viene attivata un'operazione di attivazione/disattivazione del buffer, a seconda dell'architettura della memoria di sistema.

### <a name="drawing-apis"></a>Disegno di API 

Esistono diverse primitive di disegno principali richieste da GUIX per disegnare tutti gli elementi visivi sullo schermo. Queste API di disegno possono anche essere richiamate dal software applicativo, in genere come parte di una funzione di disegno widget personalizzata. Queste API di disegno di Canvas GUIX eseguono la convalida e il ritaglio dei parametri, quindi passano le coordinate di disegno ritagliate fino al driver di visualizzazione per le implementazioni del disegno specifiche per l'hardware e il formato colori. Queste funzioni dell'API di disegno sono definite come segue.

- gx_canvas_alpha_set
- gx_canvas_arc_draw
- gx_canvas_block_move
- gx_canvas_circle_draw
- gx_canvas_ellipse_draw
- gx_canvas_glyphs_draw
- gx_canvas_hardware_layer_bind
- gx_canvas_hide
- gx_canvas_line_draw
- gx_canvas_offset_set
- gx_canvas_pie_draw
- gx_canvas_pixel_draw
- gx_canvas_pixelmap_blend
- gx_canvas_pixelmap_rotate
- gx_canvas_pixelmap_tile
- gx_canvas_polygon_draw
- gx_canvas_rectangle_draw
- gx_canvas_rotated_text_draw
- gx_canvas_shift
- gx_canvas_show
- gx_canvas_text_draw

L'API Drawing viene richiamata tramite l'API Canvas GUIX e tutto il disegno viene eseguito usando gx_canvas_ * funzioni API. Il disegno viene eseguito utilizzando il pennello corrente nel contesto di disegno corrente. Qualsiasi funzione di disegno di forme precedente può essere delineata, colorata a tinta unita o Pixelmap riempita come definito dal pennello corrente. Per modificare la larghezza, il colore o il riempimento del contorno della forma, utilizzare le funzioni API gx_context_brush_ * per definire il pennello all'interno del contesto di disegno corrente.

Le API di disegno a livello di applicazione precedenti non eseguono il disegno effettivo nell'area di disegno, ma verificano invece i parametri del chiamante prima di richiamare la funzione di disegno del livello driver di visualizzazione. La funzione di disegno a livello di driver scrive effettivamente i dati pixel nella memoria Canvas.

GUIX fornisce funzioni di disegno di driver di visualizzazione generiche o predefinite per varie profondità dei colori, tra cui 1, 2, 4, 8, 16, 24 e 32 bit per pixel (BPP). In alcuni casi, l'implementazione predefinita del disegno software viene sostituita da implementazioni con accelerazione hardware per le destinazioni hardware che forniscono un acceleratore di disegno 2D.

### <a name="color-depth"></a>Profondità colore 

GUIX supporta le profondità di colore fino a 32-BPP, oltre a monocromatico e scala di grigi. Il tipo di supporto per la profondità dei colori dipende in gran parte dalle funzionalità dello schermo fisico sottostante e ha anche un effetto sulla quantità di memoria necessaria per l'area di disegno dell'area di disegno. Di seguito è riportato un elenco del supporto per la profondità dei colori insieme a una breve descrizione delle variazioni all'interno di tale profondità.

| &nbsp;Formato colori       | Descrizione                                                                                                   |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| monocromatico a 1 bit   | formato a 1 bit per pixel compresso.                                                                                                   |
| scala di grigi a 2 bit    | 4 livelli di grigio, compressi quattro pixel per byte.                                                                                      |
| scala di grigi a 4 bit    | 16 livelli di grigio, compressi due pixel per byte.                                                                                      |
| colore a 4 bit        | Un'organizzazione di memoria Planar in formato VGA.                                                                                         |
| scala di grigi a 8 bit    | 256 livelli di grigio                                                                                                                  |
| modalità tavolozza a 8 bit | 1 byte per pixel usato come indice della tavolozza                                                                                           |
| modalità r:g: b a 8 bit   | Un formato di 2:3:2 r:g: b meno comunemente utilizzato.                                                                                         |
| 16 bit             | Ogni pixel richiede due byte. Può essere r:g: b o b:g: r byte order. In genere, la struttura 5:6:5, ma può anche essere la struttura 5:5:5 o 4:4:4:4 a:r: g:b. |
| a 24 bit             | Ogni pixel richiede 3 (formato compresso) o 4 (formato decompresso) byte. Può trovarsi in r:g: b o b:g: r byte order come richiesto dall'hardware. |
| 32 bit             | Ogni pixel richiede 4 byte con un canale alfa. Può essere a:r: g:b o b:g: r:a byte order e determinato dall'hardware.              |

### <a name="mouse-support"></a>Supporto del mouse 

GUIX supporta la creazione di un cursore del mouse su un'area di disegno desiderata. Il cursore del mouse può essere disegnato nel software o potrebbe essere supportato dalla sovrimpressione del cursore hardware. In entrambi i casi, l'API fornita all'applicazione correlata al supporto del cursore del mouse è la stessa, indipendentemente dal fatto che venga utilizzato il disegno del cursore del mouse.

Il supporto del mouse GUIX è abilitato solo se `#define GX_MOUSE_SUPPORT` è definito nel file di intestazione gx_user. h prima di compilare la libreria GUIX.

L'applicazione deve definire il cursore del mouse e l'area sensibile usando la funzione API ***gx_canvas_mouse_define*** . Questa API accetta un puntatore all'area di disegno in cui deve essere disegnata l'immagine del cursore e un puntatore a una struttura **GX_MOUSE_CURSOR_INFO** , che definisce l'immagine del cursore del mouse e l'area sensibile dell'immagine del mouse rispetto all'angolo superiore sinistro dell'immagine.

## <a name="guix-display-component"></a>Componente di visualizzazione GUIX 

Il componente di visualizzazione è fondamentale in GUIX, perché gestisce l'elaborazione di tutti gli oggetti visualizzati, che in loro volta contengono uno o più Canvas, widget e finestre. Il componente di visualizzazione interagisce anche con il driver dello schermo hardware sottostante associato a ogni visualizzazione tramite una serie di puntatori a funzione.

### <a name="display-creation"></a>Creazione della visualizzazione 

È possibile creare un oggetto di visualizzazione durante l'inizializzazione o in qualsiasi momento durante l'esecuzione dei thread dell'applicazione. In genere, un'applicazione crea un oggetto di visualizzazione per gestire ogni schermata fisica. Se è stato usato GUIX Studio per definire l'applicazione e le visualizzazioni fisiche sono disponibili, si userà la funzione API gx_studio_display_configure per creare e inizializzare ogni visualizzazione.

### <a name="display-control-block"></a>Visualizzazione del blocco di controllo 

Le caratteristiche di ogni oggetto visualizzato si trovano nel blocco di controllo ***GX_DISPLAY** _ e sono definite in _ *_gx_api. h_* *. La memoria necessaria per un oggetto visualizzato viene fornita dall'applicazione e può trovarsi in qualsiasi punto della memoria. Tuttavia, è più comune fare in modo che il controllo di visualizzazione blocchi una struttura globale definendolo al di fuori dell'ambito di qualsiasi funzione.

### <a name="resource-management"></a>Gestione delle risorse 

Le risorse sono componenti dell'interfaccia utente necessari per l'applicazione, ma non sono codice dell'applicazione. Le risorse sono dati dell'applicazione e in genere sono definite in modo statico. I tipi di risorsa includono pixelmaps, fonts, Colors e Strings. Queste risorse possono essere modificate in qualsiasi momento, in genere senza modificare alcun software applicativo. È importante tenere l'archiviazione di e i riferimenti alle risorse separate dal software applicativo per consentire la modifica dell'aspetto dell'interfaccia utente senza modificare il codice dell'applicazione, in quanto le modifiche apportate al software applicativo richiedono in genere il ritesting e la verifica associati al software.

Il modulo di ***visualizzazione*** GUIX fornisce le funzionalità di gestione delle risorse per tutte le risorse che dipendono dalla profondità di colore e dal formato dello schermo. Tali funzionalità includono la manutenzione della tabella Pixelmap attiva, della tabella dei tipi di carattere attiva e della tabella dei colori attiva. La risorsa della tabella di stringhe viene gestita dal modulo di sistema GUIX, poiché in genere le risorse di stringa non devono essere modificate in base alla profondità e al formato dei colori.

Il software dell'applicazione fa riferimento alle risorse in base all'ID risorsa, che è un indice nella tabella delle risorse corrispondente. Ciò consente di modificare la tabella, ad esempio la tabella dei colori potrebbe essere modificata quando un prodotto passa da "modalità giorno" a "modalità notte", ma i valori dell'ID colore rimangono invariati.

Le risorse dell'applicazione vengono scritte in un file di risorse o in un set di file di risorse dall'applicazione GUIX Studio. I colori predefiniti, pixelmaps e i tipi di carattere vengono forniti automaticamente quando si crea un nuovo progetto GUIX studio, ma queste impostazioni predefinite sono facilmente sostituite quando si definisce l'aspetto dell'applicazione.

È importante notare che gli ID di risorsa per i colori, i tipi di carattere e pixelmaps non possono essere risolti nei valori effettivi di colore, tipo di carattere o Pixelmap fino a quando il componente di visualizzazione attivo non è noto. Poiché l'architettura GUIX supporta più visualizzazioni attive, gli ID delle risorse possono essere risolti solo in valori di risorse quando un widget e l'ID di risorsa associato possono essere risolti in una visualizzazione specifica. Questa proprietà è nota come associazione dinamica. L'ID di risorsa per una proprietà, ad esempio un colore del testo, ad esempio l'ID di risorsa **GX_COLOR_ID_TEXT,** potrebbe risolversi in un valore R:G: B a 16 bit per il bianco se usato in uno schermo, ma lo stesso ID colore potrebbe risolversi in un valore di colore nero monocromatico quando viene usato in un'altra visualizzazione.

In pratica, questa associazione dinamica di ID risorse ai valori delle risorse significa che il software dell'applicazione e i componenti interni di GUIX dovrebbero spesso risolvere solo gli ID risorsa in valori di risorse all'interno di un contesto di disegno attivo. Un contesto di disegno attivo specifica lo schermo attualmente attivo, che consente a GUIX di risolvere ogni ID di risorsa in un valore di risorsa specifico. Se il software dell'applicazione è necessario per trovare un valore specifico di risorsa all'esterno di un contesto di disegno, questa operazione può essere eseguita anche per i widget visibili. I widget visibili sono collegati a una finestra radice che può essere usata anche per risolvere l'area di disegno attiva e visualizzare per tale widget.

Se un widget è stato creato ma non ancora visualizzato (ad esempio, non è stato collegato ad alcuna finestra radice o ad altro elemento padre visibile), qualsiasi ID di risorsa associato a tale widget non può essere risolto in un valore di risorsa specifico, ad eccezione di indicizzazione diretta nella tabella delle risorse assegnata a una visualizzazione specifica. Questo accesso diretto a una tabella delle risorse specifica può essere eseguito in modo sicuro dal software applicativo, ma non viene mai eseguito nel software della libreria GUIX interna.

### <a name="widget-defaults"></a>Impostazioni predefinite widget 

Il componente di visualizzazione GUIX fornisce anche le definizioni predefinite per diversi attributi widget. Se non diversamente specificato dall'applicazione, i widget/Windows vengono creati con questi attributi di sistema. Questi attributi di sistema sono costituiti principalmente da tipi di carattere, colori e bitmap mantenuti nelle tabelle delle risorse di sistema. Gli attributi aggiuntivi per l'aspetto della barra di scorrimento predefinito vengono gestiti anche dal componente di visualizzazione GUIX.

Le impostazioni predefinite dei colori sono definite dalla tabella dei colori assegnata a ogni visualizzazione e dagli ID colore predefiniti predefiniti. Gli ID colore predefiniti includono i seguenti.

| ID colore | Descrizione |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| GX_COLOR_ID_CANVAS | Colore predefinito Canvas (ovvero sfondo schermo) |
| GX_COLOR_ID_WIDGET_FILL | Colore riempimento widget predefinito |
| GX_COLOR_ID_WINDOW_FILL | Colore riempimento finestra predefinito |
| GX_COLOR_ID_DISABLED_FILL | Colore di riempimento del widget disabilitato predefinito |
| GX_COLOR_ID_DEFAULT_BORDER | Colore del bordo del widget predefinito |
| GX_COLOR_ID_WINDOW_BORDER | Colore del bordo predefinito della finestra |
| GX_COLOR_ID_TEXT | Colore del testo predefinito |
| GX_COLOR_ID_SELECTED_TEXT | Colore del testo selezionato predefinito |
| GX_COLOR_ID_DISABLED_TEXT | Colore del testo disabilitato predefinito |
| GX_COLOR_ID_SELECTED_TEXT_FILL | Colore riempimento testo selezionato predefinito |
| GX_COLOR_ID_READONLY_TEXT | Colore del testo ReadOnly predefinito |
| GX_COLOR_ID_READONLY_FILL | Colore di riempimento testo di sola lettura predefinito |
| GX_COLOR_ID_SCROLL_FILL |    Colore riempimento barra di scorrimento |
| GX_COLOR_ID_SCROLL_BUTTON | Colore riempimento pulsante barra di scorrimento |
| GX_COLOR_ID_SHADOW | Colore ombreggiatura predefinito |
| GX_COLOR_ID_SHINE | Colore di evidenziazione predefinito |
| GX_COLOR_ID_BUTTON_BORDER | Colore bordo widget pulsante |
| GX_COLOR_ID_BUTTON_UPPER | Colore riempimento superiore widget pulsante |
| GX_COLOR_ID_BUTTON_LOWER | Colore di riempimento inferiore del widget pulsante |
| GX_COLOR_ID_BUTTON_TEXT | Colore del testo del widget pulsante |
| GX_COLOR_ID_TEXT_INPUT_TEXT | Colore del testo del widget input di testo |
| GX_COLOR_ID_TEXT_INPUT_FILL | Colore riempimento input di testo |
| GX_COLOR_ID_SLIDER_TICK | Colore utilizzato per creare segni di graduazione del dispositivo di scorrimento. |
| GX_COLOR_ID_SLIDER_GROOVE_BOTTOM | Colore usato per creare il Groove del dispositivo di scorrimento |
| GX_COLOR_ID_SLIDER_NEEDLE_OUTLINE | Colore utilizzato per disegnare il contorno dell'ago |
| GX_COLOR_ID_SLIDER_NEEDLE_FILL | Colore usato per riempire la lancetta del dispositivo di scorrimento |
| GX_COLOR_ID_SLIDER_NEEDLE_LINE1 | Colore usato per l'evidenziazione della lancetta |
| GX_COLOR_ID_SLIDER_NEEDLE_LINE2 | Colore utilizzato per creare l'ombreggiatura della lancetta |

Per questi valori di ID colore viene eseguito il mapping a un valore di colore specifico definito dalla tabella dei colori assegnata a ogni visualizzazione. Queste impostazioni predefinite possono essere modificate come un gruppo per una visualizzazione chiamando la funzione API ***gx_display_color_table_set*** . Se si usa GUIX studio, la tabella dei colori di visualizzazione viene automaticamente inizializzata quando l'applicazione chiama la funzione ***gx_studio_display_configure*** .

Il componente di visualizzazione GUIX gestisce inoltre una tabella dei caratteri predefinita. La tabella dei tipi di carattere predefinita definisce il tipo di carattere utilizzato da ogni tipo di widget, a meno che non sia specificato specificamente dall'applicazione. Gli ID tabella dei tipi di carattere visualizzati predefiniti includono i valori seguenti.

| &nbsp;ID carattere | Descrizione |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------|
| GX_FONT_ID_DEFAULT | Tipo di carattere predefinito utilizzato quando non è definito alcun tipo di carattere specifico |
| GX_FONT_ID_BUTTON | Carattere predefinito usato per tutto il testo sui pulsanti |
| GX_FONT_ID_TEXT_INPUT | Tipo di carattere predefinito usato per i campi di modifica del testo |

L'ID del tipo di carattere usato da qualsiasi widget di tipo testo può essere riassegnato usando il **gx_<widget_type API>_font_set** fornita per ogni tipo di widget relativo al testo. L'intera tabella dei tipi di carattere può essere riassegnata chiamando la funzione API **gx_display_font_table_set** .

### <a name="scrollbar-appearance"></a>Aspetto barra di scorrimento 

GUIX display gestisce anche le impostazioni predefinite per l'aspetto della barra di scorrimento per tale visualizzazione. Queste impostazioni sono definite dalla struttura **GX_SCROLLBAR_APPEARANCE** definita di seguito. GUIX display mantiene una struttura di aspetto della barra di scorrimento per le barre di scorrimento verticali e una seconda struttura per le barre di scorrimento orizzontali. L'applicazione può modificare l'aspetto predefinito della barra di scorrimento per qualsiasi visualizzazione inizializzando una struttura di **GX_SCROLLBAR_APPEARANCE** e richiamando la funzione API ***gx_display_scroll_appearance_set***.

```c
typedef struct GX_SCROLLBAR_APPEARANCE_STRUCT
{
    GX_VALUE       gx_scroll_width;
    GX_VALUE       gx_scroll_thumb_width;
    GX_VALUE       gx_scroll_thumb_travel_min;
    GX_VALUE       gx_scroll_thumb_travel_max;
    GX_UBYTE       gx_scroll_thumb_border_style;
    GX_RESOURCE_ID gx_scroll_fill_pixelmap;
    GX_RESOURCE_ID gx_scroll_thumb_pixelmap;
    GX_RESOURCE_ID gx_scroll_up_pixelmap;
    GX_RESOURCE_ID gx_scroll_down_pixelmap;
    GX_RESOURCE_ID gx_scroll_thumb_color;
    GX_RESOURCE_ID gx_scroll_thumb_border_color;
    GX_RESOURCE_ID gx_scroll_button_color;
} GX_SCROLLBAR_APPEARANCE;
```
| Membro della struttura GX_SCROLLBAR_APPEARANCE | Descrizione |
| --- | --- |
| gx_scroll_width | Larghezza di una barra di scorrimento verticale o di un'altezza di una barra di scorrimento orizzontale, in pixel. |
| gx_scroll_thumb_width | Larghezza dei pulsanti Elevator e end, in pixel. |
| gx_scroll_thumb_travel_max | Offset dalla fine della barra di scorrimento al punto di partenza del pulsante Thumb massimo. |
| gx_scroll_fill_pixelmap | Pixelmap utilizzato per riempire lo sfondo dello scorrimento. |
| gx_scroll_thumb_pixelmap | Pixelmap utilizzato per creare il pulsante del cursore di scorrimento. |
| gx_scroll_up_pixelmap | Pixelmap utilizzato per creare il pulsante di scorrimento verso l'alto. |
| gx_scroll_down_pixelmap | Pixelmap usato per creare il pulsante di scorrimento verso il basso. |
| gx_scroll_fill_color | ID colore del colore utilizzato per riempire lo sfondo della barra di scorrimento. |
| gx_scroll_button_color | ID colore del colore utilizzato per riempire il pulsante Thumb della barra di scorrimento. |

Oltre a queste impostazioni predefinite per i tipi di carattere, il colore e gli stili, l'applicazione può specificare uno qualsiasi dei parametri in base alla distinzione tra maiuscole e minuscole, se necessario, usando l'API fornita da ogni tipo di widget.

### <a name="skinning-and-themes"></a>Personalizzazione e temi

La scuoiatura consente ai widget GUIX e alle finestre di modificare facilmente l'aspetto di base, ovvero la modifica dell'aspetto di base in un'unica posizione modifica l'aspetto di base di tutti i widget e finestre associati.

Per ricreare l'applicazione GUIX, è necessario specificare una nuova tabella color, font e Pixelmap per le tabelle delle risorse di visualizzazione GUIX. Poiché tutti i widget di GUIX fanno riferimento al colore, alla bitmap o al tipo di carattere per ID di risorsa, se si specifica una nuova tabella delle risorse, tutti i widget GUIX iniziano a usare i nuovi colori e pixelmaps quando si attraggono sulla visualizzazione desiderata.

Un nuovo set di tipi di carattere, colori e pixelmaps progettati per collaborare per offrire un aspetto interessante è denominato *tema*. Un tema definisce un set di tabelle delle risorse e le dimensioni di ogni tabella delle risorse. È possibile definire qualsiasi numero di temi per qualsiasi visualizzazione con l'applicazione GUIX Studio. È necessario passare l'indice del tema iniziale alla funzione generata da GUIX Studio ***gx_studio_display_configure***, che installa il tema iniziale nella visualizzazione creata. Il tema attivo per qualsiasi visualizzazione può essere modificato in qualsiasi momento chiamando la funzione ***gx_display_theme_install***.

### <a name="root-window"></a>Finestra radice

Per ogni area di disegno visibile creata da un'applicazione, l'applicazione deve anche creare una finestra radice per l'area di disegno. Questa finestra speciale essenzialmente funge da contenitore per tutti i widget e le finestre dell'applicazione di primo livello. La finestra radice disegna lo sfondo dell'area di disegno e, dal momento che la finestra radice è derivata dalla classe **GX_WINDOW** la finestra radice può avere anche lo sfondo. Per modificare il colore di sfondo della visualizzazione o dell'area di disegno, è sufficiente modificare il colore di riempimento della finestra radice collegata a tale area di disegno.

Se si usa la funzione generata da GUIX Studio denominata ***gx_studio_display_configure*** per configurare gli schermi, l'area di disegno e la finestra radice per ogni visualizzazione vengono creati automaticamente come parte di questa funzione di inizializzazione.

### <a name="anti-aliasing"></a>Anti-aliasing 

L'anti-aliasing è una funzionalità facoltativa di GUIX che viene usata per smussare linee, curve e tipi di carattere. L'anti-aliasing è supportato solo quando si esegue con un driver di visualizzazione che utilizza una profondità di colore di 16 BPP o superiore.

Il disegno a linee con aliasing viene abilitato impostando il **GX_BRUSH_ALIAS** Flash nel pennello attivo. Questo vale per le linee disegnate direttamente e per le linee disegnate come bordo di un poligono o di un cerchio.

Il disegno di testo con anti-aliasing viene abilitato tramite un tipo di carattere anti-aliasing prodotto dall'applicazione GUIX Studio. Quando si crea il tipo di carattere, si specifica se un tipo di carattere deve essere generato come antialiasing o binario.
I tipi di carattere con anti-aliasing in GUIX utilizzano 16 livelli di trasparenza per ogni pixel.

### <a name="clipping"></a>Ritaglio 

Il ritaglio è supportato internamente dal componente di visualizzazione GUIX e dai livelli di finestra e widget dall'architettura padre-figlio gestita dai widget GUIX. Non è mai possibile creare una finestra o un widget al di fuori dell'area del widget e non è mai consentito creare un widget al di fuori dell'area dell'elemento padre del widget.

In questo modo si impedisce anche che i widget vengano disegnati a coordinate di pixel che si trovino all'esterno della memoria Canvas, causando probabilmente un errore di memoria o un errore di sistema. I widget non possono essere disegnati all'esterno dell'area del widget, dell'area padre del widget o oltre l'extent dell'area di disegno.

Inoltre, i widget possono essere creati solo in aree contrassegnate in precedenza come dirty. In questo modo si impedisce che venga disegnata un'intera finestra, ad esempio quando è stato rivelato solo un angolo della finestra. Solo la parte della finestra che è effettivamente necessario aggiornare è contrassegnata come Dirty, quindi la funzione di disegno della finestra Aggiorna effettivamente solo i pixel nell'area dirty.

Il componente di visualizzazione GUIX impone questi algoritmi di ritaglio prima di richiamare le funzioni di disegno a livello di driver.

### <a name="views"></a>Viste 

GUIX mantiene sempre un set di visualizzazioni per ogni finestra radice e ogni finestra figlio della finestra radice. Le visualizzazioni sono un'area di ritaglio dinamica e determinata in fase di esecuzione che viene modificata in base alla posizione della finestra e all'ordine Z.
GUIX usa le visualizzazioni per evitare che una finestra o un widget in background venga disegnato sopra una finestra o un widget in primo piano. Le visualizzazioni applicano la disciplina dell'ordine Z. Inoltre, le visualizzazioni sono importanti per garantire l'efficienza, in quanto impediscono a una finestra in background di disegnare in un'area dell'area di disegno che non può essere visualizzata. Se una finestra è completamente coperta da un'altra finestra, la finestra coperta non sarà consentita per il disegno nell'area di disegno, anche se tenta di eseguire questa operazione.

### <a name="display-driver-interface"></a>Visualizza interfaccia driver 

I driver di visualizzazione GUIX sono responsabili di tutte le interazioni con lo schermo fisico sottostante. I driver di visualizzazione dispongono di tre funzioni di base: inizializzazione, disegno e visualizzazione del buffer dei frame.
L'inizializzazione è responsabile della preparazione dell'hardware di visualizzazione fisico, dell'informativa di GUIX delle proprietà dell'hardware di visualizzazione fisico e della creazione di un modulo di GUIX per l'utilizzo di funzioni di disegno specifiche. L'inizializzazione del driver di visualizzazione principale viene chiamata dalla funzione GUIX ***gx_display_create*** . Inoltre, il thread GUIX chiamerà anche un'inizializzazione di driver di visualizzazione secondaria dal contesto del thread. Questo driver di visualizzazione secondario è necessario solo se il driver richiede i servizi di RTO durante l'inizializzazione, ad esempio, interruzioni del dispositivo o ***tx_thread_sleep*** richieste di ritardo tra i passaggi del processo di inizializzazione.

Al termine dell'inizializzazione, il driver di visualizzazione è responsabile di qualsiasi disegno diretto che può essere eseguito nell'hardware di visualizzazione fisico.
Infine, il driver di visualizzazione è responsabile della visualizzazione del buffer dei frame.

## <a name="guix-widget-component"></a>Componente widget GUIX

Un widget GUIX è un elemento grafico visibile. Sono presenti componenti GUIX che non sono visibili, ad esempio timer e funzioni di utilità Math.
Tuttavia tutti i componenti visibili sono derivati dal componente widget GUIX di base. Un widget GUIX è il blocco predefinito principale della visualizzazione GUIX: tutti gli altri elementi grafici sono derivati dalla funzionalità del widget di base.

I widget GUIX vengono implementati in modo orientato agli oggetti con supporto completo dell'ereditarietà. Questa operazione viene eseguita utilizzando ANSI C, il che comporta i requisiti di memoria e di elaborazione più piccoli possibili. Quando si parla di un particolare widget, ad esempio **GX_BUTTON**, che *deriva da* un altro widget, ad esempio il **GX_WIDGET** di base, significa che la struttura di controllo **GX_BUTTON** contiene tutte le variabili membro e i puntatori a funzione di **GX_WIDGET**, con alcune variabili aggiuntive specifiche per **GX_BUTTON**. GUIX crea livelli di widget in questo modo, in modo che i widget più complessi siano sempre basati su un widget più semplice prima di essi. Questo modello gerarchico di derivazione consente di apprendere più facilmente le API usate per modificare i parametri dei widget. Se si desidera modificare il colore di un pulsante, utilizzare la stessa API utilizzata per modificare il colore di un widget, ovvero ***gx_widget_fill_color_set***.

L'organizzazione dei widget visibili viene gestita in modo padre-figlio utilizzando elenchi strutturati ad albero che collegano i widget figlio agli elementi padre. Gli elementi figlio ereditano le caratteristiche dagli elementi padre, ad esempio le visualizzazioni in cui è possibile disegnarli e l'area di disegno in cui disegnano.
I widget figlio possono avere i propri widget figlio, ereditando di nuovo le varie caratteristiche dell'elemento padre. Le caratteristiche di qualsiasi widget possono essere ridefinite in modo esplicito tramite varie chiamate API GUIX.

### <a name="widget-creation"></a>Creazione widget 

Un oggetto widget può essere creato durante l'inizializzazione o in qualsiasi momento durante l'esecuzione dei thread dell'applicazione. Non esiste alcun limite al numero di oggetti widget che possono essere creati da un'applicazione. Non è inoltre previsto alcun limite al numero di elementi figlio che possono essere presenti nei widget, entro i limiti di memoria dell'hardware di destinazione.

Ogni tipo di widget ha una propria funzione di creazione, ad esempio ***gx_button_create** _ o _ *_gx_prompt_create_* *. I primi tre parametri per queste funzioni sono sempre gli stessi, ovvero un puntatore alla struttura del controllo widget, un puntatore di stringa al nome del widget e un puntatore all'elemento padre del widget. Ogni funzione create può avere un numero qualsiasi di parametri aggiuntivi a seconda dei requisiti di quel particolare tipo di widget.

### <a name="widget-control-block"></a>Blocco di controllo widget 

Le caratteristiche di ogni oggetto widget sono disponibili nel relativo blocco di controllo **GX_WIDGET** e sono definite in **_gx_api. h_**. La memoria necessaria per un oggetto widget viene fornita dall'applicazione e può trovarsi in qualsiasi punto della memoria. Tuttavia, è più comune fare in modo che il controllo oggetto widget blocchi una struttura globale definendola al di fuori dell'ambito di qualsiasi funzione. Se si usa GUIX studio, i blocchi di controllo widget possono essere allocati staticamente all'interno del file delle specifiche generate in studio oppure possono essere allocati in modo dinamico dall'applicazione.

### <a name="dynamic-widget-control-block-allocation-and-de-allocation"></a>Allocazione e deallocazione di blocchi di controllo widget dinamici 

Se si usa l'allocazione dei blocchi di controllo dinamici, sarà necessario definire due funzioni che GUIX userà per allocare e liberare la memoria necessaria per i blocchi di controllo widget. Le funzioni per la gestione della memoria vengono passate al componente di sistema GUIX tramite la funzione API ***gx_system_memory_allocator_set*** . Questa funzione consente di passare due puntatori a funzione in GUIX: il primo è un puntatore a una funzione di allocazione della memoria e il secondo è un puntatore a una funzione di memoria libera. In genere, queste funzioni vengono implementate usando i pool di byte ThreadX, ma la progettazione di GUIX consente di implementare la gestione dinamica della memoria nel modo preferito.

L'allocazione dinamica dei widget viene spesso usata all'interno del file delle specifiche dell'applicazione generato da studio, quando si seleziona l'opzione "allocata dinamicamente" nel campo proprietà widget di studio. Tuttavia, è anche possibile usare l'allocazione dei blocchi di controllo dinamici all'interno dell'applicazione. Se si usa l'allocazione dei blocchi di controllo dinamici all'interno dell'applicazione, è necessario richiamare la funzione API ***gx_widget_allocate** _ per allocare il blocco di controllo widget. Successivamente, quando si crea il widget, assicurarsi di passare il flag di stile _ *GX_WIDGET_STYLE_DYNAMICALLY_ALLOCATED** (insieme a qualsiasi altro flag di stile necessario) alla funzione di creazione widget. Questo flag viene usato per contrassegnare il widget come allocato in modo dinamico nel campo stato widget. Quando e se il widget viene eliminato in un secondo momento usando **_gx_widget_delete_**, GUIX controllerà questo campo di stato e chiamerà automaticamente la funzione deallocator della memoria per assicurarsi che non vi siano perdite di memoria.

> [!IMPORTANT]
> Per evitare la perdita di memoria, è necessario creare un widget creato con un blocco di controllo allocato in modo dinamico con il flag di stile **GX_WIDGET_STYLE_DYNAMICALLY_ALLOCATED** .

### <a name="types"></a>Tipi

GUIX offre un set completo di widget predefiniti. Come indicato in precedenza, tutti i widget specializzati sono derivati dal widget di base. Di seguito è riportato un elenco dei widget predefiniti in GUIX:

**GX_TYPE_WIDGET**

**GX_TYPE_BUTTON**

**GX_TYPE_TEXT_BUTTON**

**GX_TYPE_MULTI_LINE_TEXT_BUTTON**

**GX_TYPE_RADIO_BUTTON**

**GX_TYPE_CHECKBOX**

**GX_TYPE_PIXELMAP_BUTTON**

**GX_TYPE_ICON_BUTTON**

**GX_TYPE_ICON**

**GX_TYPE_SPRITE**

**GX_TYPE_SLIDER**

**GX_TYPE_PIXELMAP_SLIDER**

**GX_TYPE_VERTICAL_SCROLL**

**GX_TYPE_HORIZONTAL_SCROLL**

**GX_TYPE_PROGRESS_BAR**

**GX_TYPE_PROMPT**

**GX_TYPE_NUMERIC_PROMPT**

**GX_TYPE_PIXELMAP_PROMPT**

**GX_TYPE_NUMERIC_PIXELMAP_PROMPT**

**GX_TYPE_SINGLE_LINE_TEXT_INPUT**

**GX_TYPE_MULTI_LINE_TEXT_VIEW**

**GX_TYPE_MULTI_LINE_TEXT_INPUT**

**GX_TYPE_WINDOW**

**GX_TYPE_ROOT_WINDOW**

**GX_TYPE_VERTICAL_LIST**

**GX_TYPE_HORIZONTAL_LIST**

**GX_TYPE_POPUP_LIST**

**GX_TYPE_DROP_LIST**

**GX_TYPE_LINE_CHART**

**GX_TYPE_DIALOG**

**GX_TYPE_KEYBOARD**

**GX_TYPE_SCROLL_WHEEL**

**GX_TYPE_TEXT_SCROLL_WHEEL**

**GX_TYPE_STRING_SCROLL_WHEEL**

**GX_TYPE_NUMERIC_SCROLL_WHEEL**

**GX_TYPE_CIRCULAR_GAUGE**

**GX_TYPE_RADIAL_PROGRESS_BAR**

**GX_TYPE_RADIAL_SLIDER**

**GX_TYPE_MENU_LIST**

**GX_TYPE_MENU**

**GX_TYPE_ACCORDION_MENU**

**GX_TYPE_TREE_VIEW**


### <a name="styles"></a>Stili

Gli stili dei widget sono costituiti da elementi come le proprietà del bordo (elevate, a nicchia, sottili, spesse o senza bordo), nonché proprietà per tipi di widget specifici, come elencato in precedenza. I flag di stile del widget offrono il metodo più semplice per modificare l'aspetto di qualsiasi widget.
Lo stile iniziale del widget è sempre un parametro passato alla funzione di creazione specifica del tipo di widget.

### <a name="colors"></a>Colori 

I widget si attraggono usando i colori definiti nella tabella dei colori di sistema.
Gli ID colore sono definiti per lo sfondo dell'area di disegno, il colore di riempimento del widget predefinito, il colore di riempimento del pulsante, il colore di riempimento del widget di testo, il colore di riempimento della finestra e altri valori Inoltre, gli oggetti **GX_WINDOW** supportano la visualizzazione di una bitmap o di uno sfondo quando il client della finestra viene riempito.

Il metodo più semplice per modificare la combinazione di colori predefinita è l'uso di GUIX studio e la creazione o la definizione di una combinazione di colori che soddisfi i requisiti.
È anche possibile definire manualmente la combinazione di colori creando una matrice di valori GX_COLOR e richiamando la funzione API gx_system_color_table_set.

### <a name="event-notification"></a>Notifica dell'evento 

Gli eventi GUIX sono richieste effettuate a uno o più widget per eseguire un'azione e notifiche specifiche per notificare i widget dell'input utente e le modifiche dello stato del sistema interno. Ad esempio, quando un widget acquisisce lo stato attivo, il **GX_EVENT_FOCUS_GAINED** viene inviato al widget tramite il servizio API ***gx_system_event_send*** .

Gli eventi vengono passati attraverso la coda degli eventi GUIX e ogni evento è un'istanza della struttura di dati **GX_EVENT** . La struttura dei dati **GX_EVENT** è definita in ***gx_api. h***, tuttavia i campi più importanti della struttura sono **gx_event_type**, **gx_event_sender**, **gx_event_target** e **gx_event_payload**.

Il campo **gx_event_type** viene usato per identificare la classe di evento particolare. Il tipo di evento indica se è, ad esempio, un evento **GX_EVENT_PEN_DOWN** o un evento di **GX_EVENT_TIMER** . Il **gx_event_payload** è un'Unione di diversi campi dati e non sono tutti validi per ogni tipo di evento.
Usare prima di tutto il campo tipo di evento, prima di esaminare gli altri campi dati degli eventi.

Il campo **gx_event_sender** contiene l'ID del widget che ha generato l'evento se l'evento è una notifica del widget figlio.

Il campo **gx_event_target** può essere usato per indirizzare gli eventi definiti dall'utente a una particolare finestra o widget. Se si vuole inviare un evento a una determinata finestra, è necessario assegnare alla finestra un valore ID univoco (in modo che possa essere identificato in modo positivo) e quando si compila l'evento, inserire il valore ID della finestra nel campo **gx_event_target** . Se non si conosce l'ID di destinazione o si desidera che l'evento venga indirizzato al widget con lo stato attivo per l'input, assicurarsi di impostare il campo **gx_event_target** su 0.

Infine, il campo **gx_event_payload** è un'Unione di diversi tipi di dati. Per gli eventi **GX_EVENT_PEN_DOWN** e **GX_EVENT_PEN_UP** , il campo **gx_event_pointdata** contiene il pixel x, y che coordina la posizione della penna. Per gli eventi del timer, il campo **gx_event_timer_id** contiene l'ID del timer scaduto. Altri campi dati di payload vengono utilizzati per altri tipi di evento. L'elenco completo dei tipi di evento predefiniti e dei rispettivi campi payload è definito nelle [descrizioni degli eventi Appendice E-GUIX](appendix-e.md).

L'applicazione può anche aggiungere eventi personalizzati, a partire da numericamente dopo la costante **GX_FIRST_APP_EVENT**. Tutti i numeri di evento dopo questa costante sono riservati per l'utilizzo da parte dell'applicazione. Naturalmente, il gestore eventi dell'applicazione deve disporre dell'elaborazione per tali eventi dell'applicazione.

### <a name="event-processing"></a>Elaborazione di eventi 

È disponibile una funzione di elaborazione di eventi widget predefinita per ogni widget, denominato ***gx_<>_event_process di tipo widget***. Nella maggior parte dei casi, l'applicazione non deve preoccuparsi della gestione degli eventi di un determinato widget. Tuttavia, nelle situazioni in cui l'applicazione richiede l'elaborazione di eventi personalizzata o supplementare, è possibile che l'applicazione esegua l'override della funzione di elaborazione predefinita con la propria tramite l'API GUIX ***gx_widget_event_process_set***. Questa funzione esegue l'override della funzione di elaborazione degli eventi predefinita con la funzione di elaborazione della funzione evento specificata nell'API.

> [!IMPORTANT]
> Le funzioni di elaborazione degli eventi dell'applicazione possono sfruttare i vantaggi, ovvero non duplicare l'elaborazione, dell'elaborazione predefinita semplicemente chiamando direttamente il ***gx_widget_event_process*** elaborazione predefinita.

L'elaborazione degli eventi viene chiamata esclusivamente dal contesto del thread di sistema GUIX interno. In questo modo, i requisiti dello stack per elaborare la gestione degli eventi si applicano solo al thread GUIX.

### <a name="implementing-custom-event-processing-example"></a>Implementazione dell'elaborazione di eventi personalizzati (esempio) 

È possibile fornire la propria funzione di elaborazione degli eventi per qualsiasi widget o finestra nel sistema GUIX. Se si crea un tipo di widget personalizzato, in genere verrà installato il gestore eventi personalizzato nella funzione di creazione del widget. Se si sta semplicemente estendendo o modificando il funzionamento di un widget o di una finestra esistente, è possibile chiamare la funzione API gx_widget_event_process_set dopo la creazione del widget o della finestra. Per elaborare gli eventi generati dai controlli figlio, si fornirà quasi sempre la gestione degli eventi per le finestre di primo livello, denominate anche schermate. L'evento di elaborazione generato dai controlli figlio di una schermata è il modo principale per aggiungere funzionalità all'applicazione GUIX.

Si supponga, ad esempio, di definire una schermata di primo livello denominata "main_menu".
Questa schermata può essere definita usando GUIX Studio oppure è possibile creare questa schermata nel codice dell'applicazione. Se si definisce lo schermo all'interno di GUIX studio, è sufficiente digitare il nome del gestore eventi nel campo proprietà di studio per la schermata e il codice delle specifiche generate da studio installerà automaticamente il gestore eventi. In questo caso, il gestore eventi personalizzato verrà chiamato ***main_menu_event_handler*** e dovrebbe essere codificato come segue:

```C
int main_menu_item; /* example: variable to keep track of selected item */

UINT main_menu_event_handler(GX_WINDOW *main_screen, GX_EVENT *event_ptr)
{
    UINT status = GX_SUCCESS;

    switch(event_ptr->gx_event_type)
    {
    /* this is an example for catching events from a child button */
    case GX_SIGNAL(IDB_CHILD_BUTTON, GX_EVENT_CLICKED):
        /* insert your button handler code here */
        break;

    case GX_EVENT_SHOW:
        /* add functionality to the show event handler */
        /* first, do default processing */
        status = gx_window_event_process(main_screen, event_ptr); /* note 1 */

        /* now add my own processing */
        main_menu_item = 0;
        break;

    default:
        /* pass all other events to base processing function */
        status = gx_window_event_process(main_screen, event_ptr); /* note 1 */
        break;
    }
    return status;
}
```

Nell'esempio precedente, è importante notare che per gli eventi di sistema come **GX_EVENT_SHOW** (gli eventi generati internamente per inviare una notifica a un widget di una modifica dello stato), l'applicazione deve passare tali eventi alla funzione di elaborazione degli eventi del widget di base per assicurarsi che venga eseguita la normale elaborazione. L'applicazione può quindi aggiungere la logica aggiuntiva desiderata. Tutti gli eventi che non sono gestiti dall'applicazione (il case predefinito precedente) devono essere passati anche alla funzione di elaborazione degli eventi di base. Poiché questo esempio è stato per una schermata di primo livello basata su **GX_WINDOW**, la funzione di elaborazione degli eventi predefinita è gx_window_event_process.

### <a name="drawing-function"></a>Funzione Drawing 

Tutto il disegno dei widget viene eseguito separatamente dalla gestione degli eventi. Questa operazione è più efficiente perché il disegno è in genere costoso in termini di cicli della CPU. Implementando un algoritmo di disegno posticipato, è possibile completare tutti gli eventi in attesa e le modifiche di visualizzazione associate prima di eseguire qualsiasi disegno, eliminando così il disegno sprecato. Analogamente all'elaborazione di eventi, esiste una funzione di disegno widget predefinita per la maggior parte dei widget, denominata ***gx_<tipo di widget>_draw***, dove xxx è il tipo di widget. Nella maggior parte dei casi, l'applicazione non deve preoccuparsi della funzione di disegno di un determinato widget. Tuttavia, nelle situazioni in cui l'applicazione richiede un disegno personalizzato o supplementare, è possibile che l'applicazione esegua l'override della funzione di disegno predefinita con la propria tramite l'API GUIX ***gx_widget_draw_set***. Questa funzione consente all'applicazione di fornire la propria funzione di disegno personalizzata per qualsiasi widget. Ciò consente all'applicazione di definire tutti i nuovi tipi di widget.

> [!IMPORTANT]
> Le funzioni di disegno delle applicazioni possono trarre vantaggio (ovvero non duplicare il codice) del disegno predefinito semplicemente chiamandolo direttamente dalla funzione di disegno sottoposta a override.

Il disegno del widget viene chiamato esclusivamente dal contesto del thread di sistema GUIX interno. In questo modo, i requisiti di intervallo e stack per eseguire il disegno si applicano solo al thread GUIX.

### <a name="implementing-custom-drawing-example"></a>Implementazione del disegno personalizzato (esempio) 

Viene fatto riferimento alla funzione di disegno per qualsiasi widget tramite un puntatore a funzione indiretto che è un membro del blocco di controllo GX_WIDGET. Se si usa GUIX Studio per definire il widget, è possibile installare il puntatore a funzione personalizzato semplicemente digitando il nome della funzione nel parametro "Drawing Function" delle proprietà del widget e studio installerà automaticamente il puntatore a funzione quando viene creato il widget. Se si crea il widget nel codice dell'applicazione, è necessario usare la funzione API ***gx_widget_draw_set*** per installare la funzione di disegno personalizzata dopo che il widget è stato creato.

Per questo esempio, si supponga di voler personalizzare l'aspetto di un pulsante. Il pulsante sarà simile a un **GX_TEXT_BUTTON**, ma verrà aggiunto il disegno di una piccola bitmap "Led_on" verde nella parte centrale destra del pulsante quando si preme il pulsante e una piccola bitmap "Led_off" quando il pulsante non viene premuto. Si desidera creare un pulsante simile a quello illustrato di seguito.

![Screenshot del pulsante verde per il.](./media/guix/image4.jpg) pulsante personalizzato "on"

![Screenshot del pulsante rosso per disattivato.](./media/guix/image5.jpg) pulsante personalizzato "disattivato"

In questo caso, si scriverebbe una funzione di disegno di un pulsante che avrà un aspetto simile al seguente.

```C
UINT my_button_draw(GX_TEXT_BUTTON *button)
{
    GX_PIXELMAP *map;
    ULONG button_style;
    INT xpos;
    INT ypos;

    /* first, do the normal text button drawing */
    gx_text_button_draw(button);

    /* now add our extra pixelmap */

    gx_widget_style_get(button, &button_style);

    if (button_style & GX_STYLE_BUTTON_PUSHED)
    {
        /* use the ON pixelmap */
        gx_context_pixelmap_get(GX_PIXELMAP_ID_LED_ON, &map);
    }
    else
    {
        /* use the OFF pixelmap */
        gx_context_pixelmap_get(GX_PIXELMAP_ID_LED_OFF, &map);
    }
    if (map)
    {
        /* draw it 20 pixels in from right edge */
        xpos = button->gx_widget_size.gx_rectangle_right;
        xpos -= map->gx_pixelmap_width + 20;

        /* and draw 10 pixels from the top edge */
        ypos = button->gx_widget_size.gx_rectangle_top + 10;

        /* draw the extra pixelmap on top of the button */
        gx_canvas_pixelmap_draw(xpos, ypos, map);
    }
}
```

## <a name="guix-drawing-context-component"></a>Componente del contesto di disegno GUIX 

Il contesto di disegno viene creato dinamicamente, in fase di esecuzione, mentre GUIX esegue ogni operazione di aggiornamento Canvas. Il contesto di disegno unisce l'area di disegno, il driver dello schermo e il pennello usati per eseguire le operazioni di disegno correnti.

Il contesto di disegno è definito dalla struttura **GX_DRAW_CONTEXT** .
Questa struttura contiene variabili che definiscono il ritaglio e la visualizzazione dell'operazione di disegno corrente, definiscono l'area di disegno corrente e definiscono il driver della schermata corrente in uso. La struttura di **GX_DRAW_CONTEXT** include anche il pennello utilizzato per il disegno. Il pennello del contesto di disegno è il membro che verrà usato direttamente nelle funzioni di disegno personalizzate. La struttura del pennello viene definita come illustrato nel codice riportato di seguito.

```C
typedef struct GX_BRUSH_STRUCT
{
    GX_PIXELMAP *gx_brush_pixelmap;
    GX_FONT     *gx_brush_font;
    ULONG        gx_brush_line_pattern;
    ULONG        gx_brush_pattern_mask;
    GX_COLOR     gx_brush_fill_color;  
    GX_COLOR     gx_brush_line_color;  
    UINT         gx_brush_style;
    GX_VALUE     gx_brush_width;
    UCHAR        gx_brush_alpha;  
} GX_BRUSH;
```

Il campo **gx_brush_pixelmap** definisce un Pixelmap da utilizzare per le compilazioni di rettangoli e poligoni. Questo membro non viene utilizzato a meno che l' **gx_brush_style** non includa lo stile **GX_BRUSH_PIXELMAP** .

Il membro **gx_brush_font** definisce il tipo di carattere utilizzato per il disegno del testo.
Il membro **gx_brush_line_pattern** definisce il modello utilizzato per le linee tratteggiate.
Il **gx_brush_style** membro è un set di flag di stile che possono essere o insieme per definire completamente gli attributi del pennello. I flag di stile del pennello disponibili includono quanto segue.

**GX_BRUSH_OUTLINE**  
**GX_BRUSH_SOLID_FILL**  
**GX_BRUSH_PIXELMAP_FILL**  
**GX_BRUSH_ALIAS**  
**GX_BRUSH_UNDERLINE**  
**GX_BRUSH_ROUND**

Il membro **gx_brush_width** definisce la riga con il disegno di linee o la larghezza del contorno per il disegno di forme con contorno.

Il membro **gx_brush_line_color** definisce il colore di primo piano per il disegno a linee e per il disegno del testo.

Il membro **gx_brush_fill_color** definisce il colore di riempimento a tinta unita usato per il riempimento della forma. Il componente del contesto GUIX fornisce un set di API progettate per semplificare la modifica del pennello corrente all'interno del contesto attivo. Queste API includono **gx_context_brush_define**, **gx_context_line_color_set**, **gx_context_fill_color_set**, **gx_context_font_set** e molte altre.

Il contesto di estrazione di un oggetto padre viene ereditato dagli oggetti figlio. In realtà, un clone del contesto di disegno padre viene ereditato dagli oggetti figlio quando vengono richiamate le funzioni di disegno. L'elemento figlio può modificare il contesto senza influire sul disegno padre, ma può anche ereditare informazioni dall'elemento padre, ad esempio il colore e lo stile del pennello, se lo si desidera.

## <a name="guix-window-component"></a>Componente finestra GUIX 

Il componente finestra è responsabile di tutte le operazioni di elaborazione della finestra in GUIX. Una finestra GUIX è fondamentalmente un'area di visualizzazione distinta che può contenere uno o più widget figlio. In GUIX, la finestra è in realtà solo un tipo speciale di oggetto widget fondamentale.

Le finestre GUIX vengono implementate in modo orientato a oggetti con supporto completo dell'ereditarietà. Questa operazione viene eseguita utilizzando ANSI C, il che comporta i requisiti di memoria e di elaborazione più piccoli possibili.

GUIX Windows amplia la funzionalità del widget GUIX principalmente aggiungendo il supporto per lo scorrimento orizzontale e verticale. Gli oggetti finestra GUIX possono creare e visualizzare automaticamente le barre di scorrimento e rispondere all'input della barra di scorrimento. Le finestre mobili hanno anche incorporato la gestione degli eventi per consentire lo spostamento o il trascinamento della finestra in base agli eventi di input penna.
Infine, la finestra GUIX risponde alla ricezione dello stato attivo per l'input spostando la finestra nella parte anteriore della finestra Z-order.

La finestra GUIX gestisce il concetto di *area client*, ovvero la parte interna della finestra dopo che i bordi della finestra e gli oggetti non client quali le barre di scorrimento vengono rimossi dall'area disponibile. I widget figlio dell'area client vengono ritagliati nell'area client della finestra, mentre gli elementi figlio non client, ad esempio le barre di scorrimento, possono essere disegnato all'esterno dell'area client, ma vengono comunque ritagliati nelle dimensioni esterne della finestra.

Le finestre vengono gestite in modo padre-figlio, dove gli elementi figlio ereditano le caratteristiche dal rispettivo elemento padre. Le finestre figlio possono avere le proprie finestre figlio, ereditando di nuovo le varie caratteristiche dell'elemento padre. Le caratteristiche di qualsiasi finestra possono essere ridefinite in modo esplicito tramite varie chiamate API GUIX.

### <a name="window-creation"></a>Creazione finestra 

È possibile creare un oggetto finestra durante l'inizializzazione o in qualsiasi momento durante l'esecuzione dei thread dell'applicazione. Non esiste alcun limite al numero di oggetti finestra che possono essere creati da un'applicazione. Non è inoltre previsto alcun limite per il numero di elementi figlio che possono essere presenti in qualsiasi finestra.

### <a name="window-control-block"></a>Blocco di controllo finestra 

Le caratteristiche di ogni oggetto finestra sono disponibili nel relativo blocco di controllo **GX_WINDOW** e sono definite in **_gx_api. h_**. La memoria necessaria per un oggetto finestra viene fornita dall'applicazione e può trovarsi in qualsiasi punto della memoria. Tuttavia, è più comune fare in modo che il controllo oggetto finestra blocchi una struttura globale definendola al di fuori dell'ambito di qualsiasi funzione.

### <a name="root-window"></a>Finestra radice 

GUIX richiede la cosiddetta finestra radice per ogni area di disegno. La finestra radice è senza bordi e ha le stesse dimensioni dell'area di disegno a cui è collegata. Viene usato principalmente come contenitore per tutti i widget e le finestre di primo livello. La finestra radice viene in genere creata dall'applicazione tramite la funzione API ***gx_window_root_create***, subito dopo la creazione dello schermo e dell'area di disegno. Se si usa la funzione generata da studio gx_studio_display_configure, l'indirizzo della finestra radice può essere restituito nella posizione passata come ultimo parametro a questa funzione.

Per impostazione predefinita, una finestra radice non può essere spostata e, nel caso più semplice, la finestra radice corrisponde alla dimensione dell'area di disegno. La finestra radice attiva lo sfondo dello schermo, quindi per modificare il colore di sfondo dello schermo o per visualizzare lo sfondo è necessario assegnare un colore o uno sfondo alla finestra radice.

Se una finestra radice è mobile, viene spostata in modo non modificando la relativa posizione nell'area di disegno come una finestra figlio, ma spostando l'area di disegno.
Questa funzionalità consente alla finestra radice di GUIX di sfruttare l'hardware che supporta più buffer di frame con registri di offset hardware.

### <a name="background"></a>Sfondo 

Gli sfondi della finestra sono colori a tinta unita o immagini bitmap. È disponibile uno sfondo della finestra predefinito a livello di sistema che fornisce il valore predefinito per il set iniziale di finestre. Naturalmente, qualsiasi sfondo della finestra può essere modificato tramite l'API GUIX.

Per modificare lo sfondo a tinta unita di una finestra, usare l'API ***gx_widget_fill_color_set*** . Per assegnare uno sfondo a una finestra, usare l'API ***gx_window_wallpaper_set*** .

### <a name="scrolling"></a>Scorrimento 

GUIX supporta lo scorrimento della finestra standard quando l'area necessaria per visualizzare gli elementi figlio della finestra supera le dimensioni correnti della finestra, orizzontalmente e/o verticalmente. Per abilitare lo scorrimento, l'applicazione deve creare le barre di scorrimento desiderate e collegarle alla finestra.

Il componente della finestra GUIX fornisce un'implementazione di scorrimento predefinita in base alle dimensioni dell'area client della finestra e all'extent di tutti i widget figlio. Le applicazioni possono inoltre fornire un'implementazione e un'interpretazione di scorrimento personalizzate eseguendo l'override della funzione ***gx_window_scroll_info_get*** per una particolare finestra.

### <a name="event-notification"></a>Notifica dell'evento 

La funzione di elaborazione degli eventi della finestra predefinita differisce dall'elaborazione di eventi GX_WIDGET principalmente nella gestione degli eventi di scorrimento e di ridimensionamento. GX_WINDOW forniti gestori determinare per gli eventi di scorrimento e di ridimensionamento.

L'applicazione può anche aggiungere eventi personalizzati, a partire da numericamente dopo la costante **GX_FIRST_APP_EVENT**. Tutti i numeri di evento dopo questa costante sono riservati per l'utilizzo da parte dell'applicazione. Naturalmente, il gestore eventi della finestra dell'applicazione deve disporre dell'elaborazione per tali eventi dell'applicazione.

### <a name="event-processing"></a>Elaborazione di eventi 

Analogamente a tutti gli altri tipi di widget, esiste una funzione di elaborazione di eventi finestra predefinita per ogni finestra, denominata ***gx_window_event_process***. Questa funzione di gestione degli eventi viene in genere sostituita con il proprio gestore eventi nelle finestre create. Questo è il modo in cui si risponde agli eventi ed è necessario eseguire azioni in base agli eventi generati dai controlli figlio della finestra.

È importante ricordare di richiamare la funzione di base ***gx_window_event_process*** per gli eventi di sistema GUIX se si esegue l'override del gestore eventi, in modo da consentire la gestione degli eventi predefiniti, oltre a qualsiasi azione che si sta aggiungendo al gestore dell'evento. Se, ad esempio, si specifica un gestore personalizzato per l'evento **GX_EVENT_SHOW** e non si passa questo evento al ***gx_window_event_process***, la finestra non verrà mai visualizzata.
Per fornire un gestore eventi personalizzato per una finestra, utilizzare la funzione ***gx_widget_event_process_set*** per definire l'indirizzo del gestore eventi. Questa funzione esegue l'override della funzione di elaborazione degli eventi predefinita con la funzione di elaborazione della funzione evento specificata nell'API.

> [!IMPORTANT]
> Le funzioni di elaborazione degli eventi dell'applicazione possono sfruttare i vantaggi, ovvero non duplicare l'elaborazione, dell'elaborazione predefinita semplicemente chiamando direttamente il ***gx_window_event_process*** predefinito.

L'elaborazione degli eventi viene chiamata esclusivamente dal contesto del thread di sistema GUIX interno. In questo modo, i requisiti dello stack per elaborare la gestione degli eventi si applicano solo al thread GUIX.

## <a name="guix-image-reader-component"></a>Componente lettore immagini GUIX 

Il componente lettore di immagini fornisce utilità e funzioni API per decomprimere immagini compresse non elaborate nel formato GUIX Pixelmap. Sono supportati i dati dell'immagine RAW del formato JPEG e PNG, con formati aggiuntivi riservati per le versioni future.

Si noti che per la maggior parte delle applicazioni GUIX, il componente lettore di immagini GUIX non è necessario. La maggior parte delle applicazioni si basa sull'applicazione GUIX Studio per convertire gli asset grafici in formato JPEG e PNG in risorse **GX_PIXELMAP** compatibili con GUIX. Il componente lettore di immagini GUIX viene usato quando le risorse grafiche non elaborate sono note solo in fase di esecuzione o quando i vincoli di archiviazione del sistema impediscono l'archiviazione delle risorse nel formato **GX_PIXELMAP** . I dati delle immagini in formato JPEG e PNG sono in genere più compatti rispetto al formato **GX_PIXELMAP** , tuttavia si verifica un notevole sovraccarico di runtime associato all'esecuzione dinamica della decompressione e della conversione dello spazio colore di questi tipi di immagine.

Se vengono passate immagini JPEG o PNG con formato RAW alla funzione API gx_canvas_pixelmap_draw, GUIX decomprime e disegna i dati JPEG o PNG in modo dinamico. Si noti che questo avrà un impatto negativo significativo sulla velocità di disegno del runtime e il passaggio di dati di immagini in formato RAW alla funzione gx_canvas_pixelmap_draw non è consigliabile, a meno che non si usi una destinazione hardware che supporta la decompressione JPEG o PNG assistita da hardware.

> [!IMPORTANT]
> Il passaggio di immagini JPEG o PNG non elaborate all'API gx_canvas_pixelmap_draw comporta un sovraccarico di runtime significativo per la maggior parte dell'hardware di destinazione.

In alternativa, i dati JPEG e PNG non elaborati possono essere convertiti nel formato GX_PIXELMAP in fase di esecuzione usando il componente lettore di immagini.
Il pixelmaps prodotto in questo modo può essere usato e disegnato proprio come pixelmaps prodotto da studio e contenuto nel file di risorse. Ciò consente all'applicazione di eseguire la decompressione dell'immagine, la dithering e la conversione dello spazio colore una volta, in genere durante l'avvio del programma, anziché eseguire queste operazioni ogni volta che viene disegnata l'immagine.

Le funzioni del componente lettore di immagini includono:

***gx_image_reader_create***  
***gx_image_reader_palette_set***  
***gx_image_reader_start***

## <a name="guix-animation-component"></a>Componente animazione GUIX 

Il componente GUIX Animation è un set di funzioni e servizi usati per automatizzare le automazioni di transizione di schermate e widget. Il componente animazione GUIX supporta le animazioni di dissolvenza, dissolvenza e spostamento o scorrimento dei tipi di widget.

È possibile supportare le animazioni di tipo dissolvenza variando il valore alfa interno dei widget di dissolvenza (se **GX_BRUSH_ALPHA_SUPPORT** è abilitato) o disegnando qualsiasi raccolta di widget in un'area di disegno di memoria separata quando viene mescolato con lo sfondo. Per le destinazioni hardware che supportano più livelli grafici hardware, il supporto per gli effetti di dissolvenza uniforme viene eseguito in modo ottimale usando questo approccio di blending Canvas, spesso con una larghezza di banda Core minima necessaria. Per le destinazioni hardware che non supportano più livelli grafici, la fusione usando il valore alfa del pennello GUIX è supportata quando l'esecuzione è a 16 BPP e profondità del colore superiore.

Se un'animazione deve usare un'area di disegno distinta, il componente di animazione GUIX fornisce al servizio API gx_animation_canvas_define a questo scopo. Per altri tipi di animazione non è necessaria un'area di disegno separata, che verrà utilizzata se disponibile. Questo consente di utilizzare al meglio qualsiasi supporto hardware sottostante per più superfici hardware.

Le variabili che controllano un'animazione sono definite da due blocchi di controllo. Innanzitutto, il blocco di controllo **GX_ANIMATION** che definisce il controller di animazione. Il controller di animazione è il motore di guida che esegue la sequenza di animazione definita. Un singolo controller di animazione può essere riutilizzato più volte per eseguire molte sequenze di animazione diverse. Se è necessario eseguire contemporaneamente più sequenze di animazione, è possibile creare più controller di animazione **GX_ANIMATION** .

Il componente di sistema GUIX può fornire un blocco riutilizzabile di strutture di controllo **GX_ANIMATION** , che possono essere richieste dall'applicazione quando e l'animazione sono necessarie e vengono automaticamente restituite al pool di sistema al termine della sequenza di animazione. In questo modo l'applicazione definisce in modo statico una struttura di **GX_ANIMATION** per ogni animazione che può essere implementata. Le dimensioni del pool di **GX_ANIMATION** strutture sono definite dalla costante **GX_ANIMATION_POOL_SIZE**, che per impostazione predefinita è 6, ovvero per impostazione predefinita 6 animazioni simultanee possono essere allocate dal pool di sistema. Questa costante può naturalmente essere ridefinita nel file di intestazione gx_user. h è necessario eseguire animazioni più simultanee. Se **GX_ANIMATION_POOL_SIZE** è impostato su zero, il componente di sistema GUIX non fornisce un pool di animazioni o servizi correlati.

Il secondo blocco o struttura di controllo utilizzato per definire un'animazione è la struttura **GX_ANIMATION_INFO** . Questa struttura viene utilizzata per definire una particolare sequenza di animazione. Questa struttura di informazioni viene passata al controller di animazione per avviare una sequenza di animazione usando il servizio API gx_animation_start. La struttura **GX_ANIMATION_INFO** contiene i campi seguenti:

```C
typedef struct GX_ANIMATION_INFO_STRUCT
{
    GX_WIDGET *gx_animation_target;
    GX_WIDGET *gx_animation_parent;
    GX_WIDGET *gx_animation_screen_list;
    USHORT gx_animation_style;
    USHORT gx_animation_id;
    USHORT gx_animation_start_delay;
    USHORT gx_animation_frame_interval;
    GX_POINT gx_animation_start_position;
    GX_POINT gx_animation_end_position;
    GX_UBYTE gx_animation_start_alpha;
    GX_UBYTE gx_animation_end_alpha;
    GX_UBYTE gx_animation_steps;
} GX_ANIMATION_INFO;
```

Il membro **gx_animation_target** definisce il widget di destinazione su cui agirà il controller di animazione.

Il membro **gx_animation_parent** definisce il widget padre, se presente, a cui verrà collegato il widget di destinazione al termine della sequenza di animazione. Il gx_animation_parent è anche il destinatario dell'evento GX_ANIMATION_COMPLETE che viene generato al completamento di un'animazione.

Il membro **gx_animation_screen_list** definisce un elenco di widget per le animazioni della diapositiva dello schermo basate sull'input penna. L'elenco Widge deve terminare con GX_NULL puntatore e ogni widget nell'elenco deve avere le stesse dimensioni x, y del gx_animation_parent.

Il **gx_animation_style** è una maschera di maschera che definisce il tipo di animazione da eseguire e le opzioni associate. I flag di stile dell'animazione includono quanto segue.

| &nbsp;Flag stile &nbsp; animazione | Descrizione |
| --- | --- |
| GX_ANIMATION_TRANSLATE | Richiedere un'animazione di tipo diapositiva o dissolvenza. |
| GX_ANIMATION_SCREEN_DRAG | Richiedere un'animazione per il trascinamento dello schermo guidato dall'input penna. |

I flag seguenti possono essere utilizzati in combinazione con le animazioni di tipo **SCREEN_DRAG** .

| &nbsp;Flag di trascinamento dello schermo &nbsp; | Descrizione |
| --- | --- |
| GX_ANIMATION_WRAP | L'elenco delle schermate deve essere ripartito dall'inizio alla fine. |
| GX_ANIMATION_HORIZONTAL | Il trascinamento dello schermo è consentito in direzione orizzontale.  |
| GX_ANIMATION_VERTICAL | Il trascinamento della schermata è consentito nella direzione verticale. |

Il flag seguente può essere usato in combinazione con animazioni translate.

| Converti &nbsp; &nbsp; flag animazioni | Descrizione |
| --- | --- |
| GX_ANIMATION_DETACH | Scollega la destinazione dell'animazione dall'elemento padre dell'animazione quando l'animazione viene completata. Se la destinazione è stata allocata in modo dinamico e creata dalla gestione automatica degli eventi di GUIX studio, la destinazione verrà eliminata dopo la disconnessione. |
| GX_ANIMATION_TRANSLATE | I tipi di animazione sono animazioni basate su timer. L'applicazione definisce la posizione iniziale e finale e il valore alfa iniziale e finale per il widget di destinazione e il gestore delle animazioni crea un timer da gestire e come forza motrice per eseguire l'animazione.
| GX_ANIMATION_SCREEN_DRAG | Si differenzia dalle animazioni di **traduzione** in quanto questo tipo di animazione è basato sugli eventi di input penna. Questo tipo di animazione tiene traccia con l'input dello schermo touchscreen per scorrere il widget di destinazione quando l'utente trascina una penna o uno stilo attraverso lo schermo touchscreen di input. Per usare questo tipo di animazione, l'applicazione deve chiamare l'API **_gx_animation_drag_enable_** per abilitare questa animazione. |

Il valore **gx_animation_id** viene passato nuovamente all'elemento padre dell'animazione nel campo Event.gx_event_sender dell'evento **GX_ANIMATION_COMPLETE** . Questo valore viene usato dall'elemento padre dell'animazione per determinare quale delle diverse animazioni figlio sta segnalando il completamento. Questo valore può essere 0 e un'animazione con ID valore 0 non genererà un evento **ANIMATION_COMPLETE** .

Il valore **gx_animation_start_delay** è un conteggio GUIX che indica il numero di cicli del timer da ritardare dopo la chiamata di **_gx_animation_start_*_ prima di eseguire effettivamente l'animazione. Il valore può essere 0 per avviare immediatamente l'animazione quando si chiama _*_gx_animation_start_**.

Il campo **gx_animation_frame_interval** definisce il numero di cicli del timer GUIX (un multiplo della frequenza del battito del sistema operativo sottostante) per ritardare tra ogni frame della sequenza di animazione. Il valore minimo è 1.

Il **gx_animation_start_position** definisce il punto di partenza superiore sinistro per il widget di destinazione per le animazioni di traduzione.

Il **gx_animation_end_position** definisce la posizione finale superiore sinistra per il widget di destinazione per le animazioni del tipo di conversione.

Il campo **gx_animation_start_alpha** definisce il valore alfa dell'area di disegno iniziale per le animazioni del tipo di traduzione.

Il campo **gx_animation_end_alpha** definisce il valore alfa dell'area di disegno finale per le animazioni del tipo di traduzione.

Il campo **gx_animation_steps** definisce il numero di passaggi o frame che il controller deve eseguire per le animazioni di traduzione. Un numero maggiore di passaggi produce un aspetto più scorrevole e/o una dissolvenza, ma richiede anche una maggiore larghezza di banda di sistema.

Per implementare gli effetti di animazione nell'applicazione, è prima necessario chiamare ***gx_animation_create*** per inizializzare il controller di animazione. Se l'animazione usa un'area di disegno secondaria, inizializzare l'area di disegno chiamando gx_animation_canvas_define. Successivamente, è necessario inizializzare la struttura di **GX_ANIMATION_INFO** per definire il tipo specifico di animazione da eseguire e gli altri parametri di animazione. Infine, chiamare gx_animation_start per attivare la sequenza di animazione.

Quando il controller di animazione completa una sequenza di animazione, invia un evento **GX_ANIMATION_COMPLETE** al widget padre, consentendo l'esecuzione di tutte le operazioni di pulizia desiderate dell'area di disegno dell'animazione.

## <a name="guix-utility-component"></a>Componente utilità GUIX 

Il componente utilità è responsabile di tutte le funzioni di utilità comuni in GUIX. Si tratta di funzioni comuni che sono utilità utili e possono essere richiamate da qualsiasi punto dell'applicazione o dal codice GUIX interno. Di seguito sono riportate le funzioni del componente utilità.

***gx_utility_canvas_to_bmp***

***gx_utility_circle_point_get***

***gx_utility_alphamap_create***

***gx_utility_gradient_create***

***gx_utility_gradient_delete***

***gx_utlity_ltoa***

***gx_utility_math_acos***

***gx_utility_math_asin***

***gx_utility_math_cos***

***gx_utility_math_sin***

***gx_utility_math_sqrt***

***gx_utility_pixelmap_resize***

***gx_utility_pixelmap_rotate***

***gx_utility_pixelmap_simple_rotate***

***gx_utility_rectangle_center***

***gx_utility_rectangle_center_find***

***gx_utility_rectangle_combine***

***gx_utility_rectangle_compare***

***gx_utility_rectangle_define***

***gx_utility_rectangle_overlap_detect***

***gx_utility_rectangle_point_detect***

***gx_utility_rectangle_resize***

***gx_utility_rectangle_shift***

***gx_utility_string_to_alphamap***
