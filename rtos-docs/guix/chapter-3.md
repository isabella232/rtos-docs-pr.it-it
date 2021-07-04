---
title: Capitolo 3 - Panoramica funzionale di GUIX
description: Questo capitolo contiene una panoramica funzionale del prodotto dell'interfaccia utente GUIX ad alte prestazioni.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 2a53da048b18d35b6b15a4ad8d4138e1a2acd4e8
ms.sourcegitcommit: 95f4ae0842a486fec8f10d1480203695faa9592d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2021
ms.locfileid: "111875248"
---
# <a name="chapter-3---functional-overview-of-guix"></a>Capitolo 3 - Panoramica funzionale di GUIX

Questo capitolo contiene una panoramica funzionale del prodotto dell'interfaccia utente GUIX ad alte prestazioni. 

## <a name="execution-overview"></a>Panoramica dell'esecuzione

GUIX implementa un modello di programmazione basato su eventi. Ciò significa che il framework GUIX è basato principalmente sulla ricezione di eventi inseriti nella coda di eventi GUIX. L'elaborazione di questi eventi avviene nel contesto del thread GUIX, ovvero un thread ThreadX creato durante l'inizializzazione del sistema GUIX.

Le applicazioni GUIX definiscono l'interfaccia utente chiamando le funzioni API GUIX per creare finestre e widget figlio e personalizzano l'aspetto di questi widget chiamando funzioni API aggiuntive usate per definire colori, stili, tipi di carattere e vari altri attributi di ogni finestra o tipo di widget. Se si usa GUIX Studio per creare l'aspetto delle schermate dell'interfaccia utente, gran parte di questa operazione di chiamata delle funzioni API GUIX per creare la visualizzazione viene eseguita automaticamente dall'applicazione GUIX Studio.

Le applicazioni GUIX interagiscono con l'utente del sistema e con la logica di business esterna gestendo gli eventi recuperati dalla coda di eventi GUIX.
Questi eventi vengono in genere generati da widget GUIX, ma possono anche essere creati da thread esterni. Quando viene premuto un pulsante GUIX tipico, il pulsante invia un evento alla finestra padre del pulsante. Il programma dell'applicazione agirà sulla pressione del pulsante fornendo un gestore per l'evento di push del pulsante.

Vengono spesso creati thread GUIX aggiuntivi per elementi come i driver di input. Un tipico driver di input del touchscreen viene eseguito come thread autonomo esterno al thread GUIX principale. Il driver di input tocco invia informazioni di tocco nel thread GUIX inviando eventi nella coda di eventi GUIX.

Poiché molte operazioni dell'interfaccia utente, ad esempio le animazioni, richiedono informazioni temporali accurate, GUIX implementa anche un'interfaccia timer semplice e facile da usare. Questa interfaccia timer si basa sul servizio timer ThreadX e viene configurata automaticamente all'avvio del sistema.

La maggior parte del software GUIX è indipendente da eventuali dipendenze hardware. Il framework richiede driver di input specifici dell'hardware e driver di grafica specifici dell'hardware. I dettagli della modalità di implementazione di questi driver specifici dell'hardware vengono rinviati al capitolo 5.

## <a name="initialization"></a>Inizializzazione 

Il servizio ***gx_system_initialize*** deve essere chiamato prima di qualsiasi altro servizio GUIX. L'inizializzazione del sistema GUIX può essere chiamata dalla routine threadX ***tx_application_define*** (contesto di inizializzazione) o dai thread dell'applicazione. La ***funzione gx_system_initialize*** crea la coda di eventi GUIX, inizializza la funzionalità timer GUIX, crea il thread di sistema GUIX principale e inizializza varie strutture di dati gestite da GUIX durante l'esecuzione dell'applicazione.

Dopo ***gx_system_initialize,*** l'applicazione è pronta per creare schermi, canvas, finestre, widget e personalizzare le proprietà di tutti gli oggetti GUIX. Gran parte dell'API di creazione di oggetti GUIX può essere chiamata ***tx_application_define*** o dai thread dell'applicazione.

## <a name="application-interface-calls"></a>Chiamate all'interfaccia dell'applicazione 

Le chiamate dall'applicazione vengono in gran parte effettuate da ***tx_application_define*** (contesto di inizializzazione) o dai thread dell'applicazione. Vedere la sezione "Allowed From" (Consentito da) di ogni API GUIX descritta nel capitolo 4 per determinare il contesto da cui può essere chiamata.

Nella maggior parte dei casi, le attività a elevato utilizzo di elaborazione vengono posticipate al thread GUIX interno, inclusa l'elaborazione di tutti gli eventi e il disegno di widget/finestre.

Le funzioni API GUIX possono essere chiamate da qualsiasi thread in qualsiasi momento.
Tuttavia, in genere è considerata un'architettura migliore per separare la logica di business critica per il tempo dalla logica dell'interfaccia utente. Poiché le operazioni di disegno dell'interfaccia utente possono talvolta richiedere molto tempo a seconda delle dimensioni di visualizzazione e delle prestazioni della CPU, in genere non è necessario che i thread critici per il tempo ritardino l'attesa del completamento di un'operazione di disegno.

## <a name="internal-guix-thread"></a>Thread GUIX interno 

Come accennato, GUIX ha un thread interno che esegue la maggior parte dell'elaborazione dell'interfaccia utente grafica. Questo thread viene creato dal software dell'applicazione chiamando ***gx_system_initialize** _ seguito da _*_gx_system_start_**.

La priorità del thread GUIX interno è determinata da `#define GX_SYSTEM_THREAD_PRIORITY` . Il valore predefinito è 16 (priorità intermedia), ma può essere modificato specificando questo valore nel file di intestazione gx_port.h o gx_user.h, eseguendo l'override del valore predefinito.

L'intervallo di tempo del thread GUIX è definito in modo analogo da , il cui valore predefinito `#define GX_SYSTEM_THREAD_TIMESLICE` è 10 ms.

Il sie dello stack del thread di sistema è determinato da , che si trova nel file di intestazione gx_port.h, ma può anche essere sottoposto a override specificando questo valore nel file di intestazione `#define GX_THREAD_STACK_SIZE` gx_user.h. 

Il ciclo di esecuzione del thread GUIX interno è costituito da tre azioni.
In primo luogo, GUIX recupera gli eventi dalla coda di eventi GUIX e invia tali eventi per l'elaborazione da parte delle finestre e dei widget GUIX. Gli eventi vengono in genere inseriti nella coda di eventi GUIX da timer periodici, dispositivi di input come un touchscreen o un tastierino e dai widget GUIX stessi durante l'elaborazione dell'input dell'utente. Successivamente, dopo l'elaborazione di tutti gli eventi, GUIX determina se è necessario un aggiornamento dello schermo e, in tal caso, esegue l'elaborazione necessaria per aggiornare i dati grafici visualizzati, principalmente chiamando le funzioni di disegno di tali finestre e widget contrassegnati come dirty. GuiX sospende infine il thread GUIX fino all'arrivo di un nuovo evento o di un nuovo evento di input.

## <a name="event-processing"></a>Elaborazione di eventi 

Gli eventi di input tocco o penna vengono elaborati determinando la finestra o il widget più in alto sotto la posizione del pixel di input tocco o penna e chiamando la funzione di elaborazione degli eventi della finestra o del widget. Se il widget comprende gli eventi di input penna, ela processerà l'evento nel modo appropriato per quel tipo di widget. In caso contrario, il widget in primo piano passerà l'evento di input tocco o penna all'elemento padre del widget per l'elaborazione. Questo passaggio dell'evento nella catena continua fino a quando l'evento non viene gestito o l'evento arriva alla finestra radice, nel qual caso l'evento viene eliminato.

Gli eventi del tastierino vengono inviati alla finestra o al widget con lo stato attivo per l'input. Lo stato attivo dell'input viene gestito dal componente gx_system GUIX.

Gli eventi timer vengono sempre inviati alla finestra o al widget proprietario del timer per l'elaborazione.

Gli eventi generati internamente, ad esempio gli eventi clic sui pulsanti o gli eventi di modifica del valore del dispositivo di scorrimento, vengono sempre inviati all'elemento padre del widget che genera l'evento. Se l'elemento padre non elabora l'evento, viene passato verso l'alto nella catena in modo simile agli eventi di input tocco o penna.

## <a name="drawing"></a>Disegno 

Una volta completata l'elaborazione dell'evento, il thread interno GUIX determina se è necessario un aggiornamento dello schermo e, in tal caso, vengono chiamate le funzioni di disegno finestra/widget appropriate. Al termine del disegno, il thread interno GUIX attende semplicemente la coda di eventi per l'elaborazione dell'evento GUIX successivo.

GUIX implementa il concetto di *aree dirty,* ovvero aree che devono essere disegnati nuovamente, per ogni widget e area di disegno. Un widget può disegnare solo in aree precedentemente contrassegnate come dirty. Quando viene chiamata una funzione di disegno del widget, tutte le operazioni di disegno vengono ritagliate internamente in base al rettangolo dirty definito in precedenza.
I tentativi di disegnare all'esterno di quest'area vengono ignorati.

I widget e le finestre si contrassegnano come dirty chiamando la funzione API ***gx_system_dirty_mark***. Questa funzione contrassegna l'intero widget o finestra come necessario per essere ridisegnato. Una seconda funzione, ***gx_system_dirty_partial_add***, può essere richiamata come alternativa per contrassegnare solo una parte di una finestra o un widget come dirty.

Questo modello di contrassegno dei widget come dirty e quindi di ridisegno di tali widget solo quando tutti gli eventi di input sono stati elaborati viene definito disegno *posticipato.* L'algoritmo di disegno posticipato GUIX e la manutenzione degli elenchi dirty sono progettati per migliorare l'efficienza di disegno. Poiché le operazioni di disegno sono in genere dispendiose, GUIX è molto difficile da evitare operazioni di disegno non necessarie.

Il disegno viene eseguito in un canvas *GUIX.* Un'area di disegno è un'area di memoria riservata per contenere i dati grafici. Un'area di disegno può essere o meno collegata direttamente al buffer dei frame hardware, a seconda dell'architettura di sistema e dei vincoli di memoria. Prima di poter eseguire qualsiasi disegno, è necessario aprire un'area di disegno per il disegno chiamando la ***gx_canvas_drawing_initiate*** API. Questa API prepara un'area di disegno per il disegno e ha stabilito il contesto *di disegno corrente.* Quando GUIX esegue un aggiornamento dell'area di disegno di sistema, l'area di disegno viene aperta per il disegno e il contesto di disegno viene stabilito prima che le API di disegno a livello di widget siano richiamate. Non è quindi necessario che i widget avviino il disegno su un'area di disegno all'interno della funzione di disegno del widget.

Tuttavia, se un'applicazione desidera eseguire il disegno immediato in un'area di disegno, al di fuori del flusso dell'algoritmo di disegno posticipato GUIX standard, l'applicazione deve richiamare direttamente il ***gx_canvas_drawing_initiate*** prima di chiamare qualsiasi altra funzione API di disegno e deve chiamare ***gx_canvas_drawing_complete*** dopo il completamento del disegno immediato.

## <a name="user-input"></a>Input utente 

GUIX supporta dispositivi touch screen, mouse e tastiera con tipi di evento predefiniti. È possibile usare dispositivi di input aggiuntivi definendo tipi di evento personalizzati o mappando il dispositivo di input personalizzato ai tipi di evento predefiniti.

Le azioni associate a questi dispositivi vengono convertite in eventi elaborati dal thread GUIX interno. Il software a livello di driver scritto per supportare un touchscreen deve preparare e inviare agli eventi della coda di eventi GUIX gli eventi di pen-down, pen-up e pen-drag. Analogamente, un driver di input del tastierino deve generare eventi per la pressione del tasto e l'input di rilascio del tasto.

## <a name="modal-dialog-execution"></a>Esecuzione di finestre di dialogo modali 

L'esecuzione modale della finestra di dialogo si riferisce alla presentazione di una finestra all'utente che deve essere chiusa in qualche modo prima che qualsiasi altra finestra o widget GUIX possa ricevere l'input dell'utente. Le finestre di dialogo modali acquisiscono tutto l'input dell'utente mentre viene visualizzata la finestra di dialogo, indipendentemente dalla posizione x,y degli eventi di input del mouse o tocco.

Le finestre di dialogo modali vengono attivate dal software dell'applicazione creando prima la finestra nel modo normale chiamando ***gx_window_create*** e quindi chiamando la funzione API GUIX ***gx_window_execute.***

Quando la ***gx_window_execute*** viene chiamata, GUIX entra in un ciclo di elaborazione degli eventi locale. La ***gx_window_execute*** non restituisce al chiamante fino a quando la finestra di dialogo non viene chiusa, tramite input dell'utente ***o chiamando gx_window_close***. Per questo motivo, è molto importante non chiamare mai ***la funzione gx_window_execute*** da un thread diverso dal thread interno GUIX.

## <a name="periodic-processing"></a>Elaborazione periodica 

Per fornire effetti di visualizzazione, animazione sprite e supporto per le richieste periodiche dell'applicazione, GUIX usa un timer ThreadX. Questo singolo timer viene usato per soddisfare tutte le esigenze correlate al tempo GUIX. Per impostazione predefinita, la frequenza per l'elaborazione interna del timer GUIX è impostata su 20 ms tramite la costante **GX_SYSTEM_TIMER_MS**, definita in **_gx_api.h_**, a meno che la costante non sia definita in precedenza nell'intestazione gx_port.h o gx_user.h. La frequenza predefinita può essere modificata dall'applicazione tramite un'opzione di compilazione quando si compila la libreria GUIX o ridefinerla in modo esplicito in ***gx_user.h.***

> [!IMPORTANT]
> Si noti che la frequenza del timer GUIX è espressa in tick del timer RTOS ed è definita dalla **costante GX_SYSTEM_TIMER_TICKS**. Il valore di **GX_SYSTEM_TIMER_TICKS** viene calcolato **usando** GX_SYSTEM_TIMER_MS e **TX_TIMER_TICKS_PER_SECOND**. L'utente può ridefinire uno di questi valori in ***gx_port.h** _ o _ *_gx_user.h_** per regolare la frequenza e la risoluzione del timer GUIX.

## <a name="display-driver"></a>Driver di visualizzazione 

I driver di visualizzazione sono responsabili della fornitura di un set di funzioni di disegno al codice GUIX di base. L'implementazione di ognuna di queste funzioni di disegno è determinata dal driver e, quando possibile, l'implementazione sfrutta il supporto dell'accelerazione hardware. In generale, la funzione di disegno funziona scrivendo dati pixel in un buffer di memoria, che può essere il buffer fisico dei frame o può essere un buffer secondario a seconda dell'architettura del driver. Molti driver implementano il doppio buffer usando due buffer di frame e questi buffer vengono attivati o disattivati richiamando la funzione di attivazione/disattivazione del buffer. GUIX chiama queste funzioni internamente nei momenti appropriati. Per i sistemi con vincoli di memoria, le funzioni di disegno possono scrivere solo in un singolo buffer di frame di memoria.

GUIX fornisce implementazioni software predefinite di ogni funzione di disegno di basso livello a ogni livello di intensità e formato dei colori supportati. Queste funzioni vengono richiamate tramite puntatori a funzione mantenuti **all'interno GX_DISPLAY** struttura . Quando vengono creati driver specifici dell'hardware, in genere sovrascrivono alcuni di questi puntatori a funzione con funzioni specifiche dell'hardware di destinazione.

Un driver di visualizzazione hardware tipico viene implementato creando prima il driver di visualizzazione GUIX predefinito per la profondità e il formato dei colori richiesti.
Il driver hardware sostituirà quindi le funzioni che devono essere ottimizzate o personalizzate per l'implementazione hardware specifica.

GUIX supporta formati di colore in pixel compresi tra il formato monocromatico da 1 bpp e il formato 32-bpp a:r:g:b. GUIX supporta anche molte varianti all'interno di ogni ampia categoria di profondità dei colori, ad esempio r:g:b rispetto all'ordine dei byte b:g:r, formati di pixel con allineamento alle parole e canali alfa. Attualmente sono supportati 25 formati di colore distinti, ma questo elenco aumenta man mano che i fornitori di hardware offrono nuove varianti.

## <a name="display-memory-architectures"></a>Visualizzare le architetture di memoria

Varie destinazioni hardware e schermi utilizzano un'ampia gamma di architetture di memoria di visualizzazione diverse, a seconda dei vincoli di memoria della destinazione e dei requisiti di funzionalità dell'applicazione. Di seguito verranno descritte alcune delle architetture di memoria comuni con una breve descrizione di ognuna.

Modello 1) Nessun buffer di frame, dati grafici mantenuti in GRAM esterno:

![Nessun buffer di frame, dati grafici mantenuti in GRAM esterni](./media/guix/user-guide/no-frame-buffer.png)

Nel modello precedente non esiste memoria per un buffer di frame in memoria locale per la CPU. Tutti i dati grafici vengono archiviati in un GRAM esterno incorporato nella visualizzazione stessa. L'interfaccia per l'GRAM esterno può essere parallela o seriale. Questo tipo di architettura è molto a basso costo. tuttavia può presentare un effetto di rimozione indesiderato quando i dati grafici vengono aggiornati.

Modello 2) Un buffer di frame locale:

![Un buffer di frame locale](./media/guix/user-guide/one-local-frame-buffer.png)

In questo modello, la memoria per i dati grafici viene allocata da una memoria ad accesso casuale accessibile direttamente dalla CPU. L'hardware dedicato deve essere presente per trasmettere ripetutamente i dati grafici (insieme ai segnali di temporizzazione) dalla memoria locale allo schermo. Questo modello è diverso dal modello 1 perché la memoria grafica è un blocco della SRAM o DRAM locale disponibile per la CPU. Può trattarsi della stessa memoria in cui si verificano le variabili dello stack e del programma.

Modello 3) Buffer frame locale + GRAM esterno:

![Buffer di frame locale + GRAM esterno](./media/guix/user-guide/local-frame-buffer-external-gram.png)

Il modello 3 è una combinazione dei primi due. In questo modello esiste memoria locale sufficiente per contenere un buffer di frame. Inoltre, il dispositivo di visualizzazione fornisce un GRAM esterno e si aggiorna automaticamente usando i dati forniti nel GRAM. Questa architettura trae vantaggio da una maggiore efficienza degli aggiornamenti perché è possibile trasferire la parte modificata del buffer dei frame locale al GRAM esterno in un unico trasferimento a blocchi, spesso utilizzando canali DMA di onboarding. Questo modello elimina anche lo sfarfallio e lo sfarfallio che possono essere presenti in uno dei primi due modelli, perché solo il contenuto grafico completato viene copiato nell'GRAM esterno.

Modello 4) Buffer frame Ping-pong:

![Buffer di frame Ping-pong](./media/guix/user-guide/ping-pong-frame-buffers.png)

Nel modello 4 è presente memoria sufficiente per fornire due buffer di frame locali. In questo caso, GUIX considera un buffer di frame come buffer di frame attivo e l'altro come buffer dei frame di lavoro. Quando è in corso un'operazione di disegno o aggiornamento dello schermo, viene eseguita nel buffer di lavoro. Al termine dell'operazione di disegno, i buffer vengono attivati e il buffer di lavoro diventa il buffer attivo e il buffer attivo diventa il buffer di lavoro. Questo modello elimina anche lo sfarfallio dello schermo e lo sfarfallio che può essere osservato in un singolo sistema memorizzato nel buffer.

Modello 5) Buffer Ping-pong con composizione canvas:

![Buffer Ping-pong con composizione canvas](./media/guix/user-guide/ping-pong-buffers-canvas-composting.png)

Nel modello 5 è possibile creare un numero qualsiasi di canvas, fino ai limiti della memoria disponibile. Le aree di disegno possono essere sovrapposte o combinate in base a quanto definito dall'applicazione per creare il composito dell'area di disegno. Quando viene creato un nuovo composito dopo un'operazione di aggiornamento dello schermo, i buffer compositi attivi e funzionanti vengono attivati o disattivati in un'operazione identica all'architettura di buffer ping-pong standard. Il modello 5 aggiunge la possibilità di eseguire operazioni di dissolvenza e fusione dello schermo combinando le aree di disegno nel composito di output finale.

Modello 6) Composizione di canvas con GRAM esterno:

![Composizione di canvas con GRAM esterno](./media/guix/user-guide/canvas-compositing-external-gram.png)

Il modello 6 è una leggera variazione nel modello 5, in cui è necessario un solo buffer composito e il buffer composito viene quindi trasferito a un GRAM esterno. Questo modello supporta anche la fusione a schermo intero e le sovrimpressione.

## <a name="string-encoding"></a>Codifica di stringhe 

GUIX per impostazione predefinita supporta la codifica di stringhe in formato UTF8. Il supporto per la codifica di stringhe UTF8 può essere disabilitato definendo GX_DISABLE_UTF8_SUPPORT **nel** file di ***intestazione gx_user.h.*** Se la codifica UTF8 è disabilitata, GUIX userà internamente solo la codifica standard ASCII a 8 bit più la codifica dei caratteri della tabella codici Latin-1. La disabilitazione della codifica di stringhe UTF8 comporta un footprint della libreria GUIX leggermente più ridotto e un'esecuzione di runtime leggermente più veloce delle funzioni di gestione delle stringhe e di disegno del testo.

La codifica di stringhe UTF8 presenta i tratti seguenti:

  - Le stringhe ASCII non accettano più spazio di archiviazione rispetto alla codifica ASCII standard a 7 bit.

  - La maggior parte delle funzioni stringa ANSI-C funziona con la codifica di stringa UTF8 senza modifiche.

Tutti i set di caratteri attivi in tutto il mondo, inclusi i set di caratteri Kanji, possono essere rappresentati usando la codifica di stringa UTF8.

### <a name="static-and-dynamic-strings"></a>Stringhe statiche e dinamiche 

Le stringhe assegnate ai widget GUIX che supportano la visualizzazione del testo possono essere costanti stringa definite in modo statico, che in genere vengono inserite nell'archiviazione costante come parte della tabella GUIX String descritta di seguito, e stringhe definite dinamicamente, ovvero stringhe generate in fase di esecuzione usando servizi come ***sprintf** _ o _*_gx_utility_ltoa_**.

Esempi di stringhe dinamiche possono includere un valore visualizzato come numero all'interno di un widget di richiesta GUIX o una stringa "ora/data" formattata dinamicamente in base alla posizione e alle preferenze di formato dell'utente. Se si creano stringhe in fase di esecuzione che verranno assegnate ai widget GUIX, ad esempio i widget **GX_PROMPT** o **GX_TEXT_BUTTON,** è necessario scegliere di allocare in modo statico lo spazio di archiviazione per queste stringhe generate dal runtime, ad esempio
matrici di caratteri globali) oppure è possibile definire e installare una funzione allocatore di memoria dinamica e usare lo stile **GX_STYLE_TEXT_COPY,** che indica a tali widget di creare una copia privata delle stringhe di testo assegnate.

È un errore di programmazione usare l'archiviazione temporanea, ad esempio una matrice di caratteri automatica, per contenere una stringa generata dinamicamente e quindi assegnare questa stringa a un widget che non ha lo stile GX_STYLE_TEXT_COPY **personalizzato.** Quando questo stile non è abilitato, il widget copia semplicemente il puntatore di stringa fornito e i dati della stringa devono essere allocati in modo statico. In caso contrario, è probabile che il puntatore della stringa del widget finirà per puntare a dati di garbage che producono risultati imprevedibili.

### <a name="passing-gx_string-arguments"></a>Passaggio GX_STRING argomenti 

Le funzioni API GUIX che accettano un parametro GX_STRING verificano sempre che la lunghezza della stringa a cui punta il campo **GX_STRING.gx_string_ptr** corrisponda al valore del campo **GX_STRING.gx_string_length.** Se i due campi non sono coerenti, viene **GX_INVALID_STRING_LENGTH** restituito un errore e l'API chiamata restituisce senza accettare l'assegnazione di stringa.

Per considerazioni sulla sicurezza, il software GUIX non usa mai internamente le funzioni stringa C standard, ad esempio ***strlen** _ o _*_strcpy_**. Queste funzioni sono soggette ad attacchi dannosi quando i dati di tipo stringa vengono acquisiti dinamicamente, come spesso accade con le applicazioni connesse.

Versioni della libreria GUIX precedenti alla versione 5.6 delle funzioni API definite che accettano ( `GX_CONST GX_CHAR *text` ) come parametro. Queste funzioni, sebbene siano ancora supportate per la compatibilità con le versioni precedenti, sono state sostituite dalle funzioni API preferite che accettano ( `GX_CONST GX_STRING *string` ) come parametro di input.

Per impostazione predefinita, l'API di gestione del testo deprecata è abilitata per consentire a tutte le applicazioni scritte in precedenza di essere compilate in modo pulito con gli aggiornamenti più recenti della libreria GUIX. Per disabilitare l'API di gestione  del testo deprecata, GX_DISABLE_DEPRECATED_STRING_API la definizione deve essere aggiunta al file **_di intestazione gx_user.h_*_. Tutte le nuove applicazioni devono definire _* GX_DISABLE_DEPRECATED_STRING_API** e devono usare solo le funzioni API sostitutive. Tutti i file di output generati da GUIX Studio per la libreria GUIX versione 5.6 o successiva utilizzeranno solo le funzioni API sostitutive.

La tabella seguente elenca i nomi delle funzioni api sostitutive deprecate e appena definite:

| **Nome funzione deprecata**              | **Sostituito con**                              |
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

La tabella di stringhe GUIX e le risorse stringa vengono registrate con un'istanza di visualizzazione GUIX.

Ogni visualizzazione in un sistema a più display ha una propria tabella di stringhe e ogni visualizzazione può essere eseguita nella propria lingua selezionata. Anche gli altri tipi di risorse GUIX (colori, tipi di carattere e mappe pixel) vengono gestiti dal componente GUIX Display, poiché questi tipi di risorse sono specifici per ogni formato di colore di visualizzazione e profondità del colore.

Anche se è possibile creare manualmente la tabella delle stringhe dell'applicazione, nella maggior parte dei casi la tabella delle stringhe di visualizzazione viene definita dall'applicazione GUIX Studio come parte del file di risorse del progetto. Le lingue disponibili sono definite anche nel file di intestazione della risorsa. La tabella delle stringhe di visualizzazione è una tabella a più colonne di puntatori alle stringhe dell'applicazione. Ogni colonna della tabella di stringhe rappresenta una lingua supportata dall'applicazione.
Se l'applicazione supporta una sola lingua, ad esempio l'inglese, la tabella delle stringhe avrà una sola colonna. È comunque possibile aggiungere il supporto per altre lingue in qualsiasi momento senza modificare il software dell'applicazione.

La tabella di stringhe attiva  viene assegnata chiamando la gx_display_string_table_set'API. Questa funzione viene chiamata automaticamente dal codice di avvio generato da GUIX Studio, ma può anche essere chiamata direttamente dall'applicazione per modificare la tabella di stringhe attiva.

Il linguaggio attivo viene  assegnato chiamando la gx_display_active_language_set'API. Questa funzione determina quale colonna della tabella delle stringhe di visualizzazione è attiva.

Quando questa funzione viene richiamata, un evento **GX_EVENT_LANGUAGE_CHANGE** viene inviato a tutti i widget GUIX visibili, consentendo loro di eseguire l'aggiornamento per visualizzare i dati stringa appena attivi.

I widget e il software applicativo risolvono le stringhe definite in modo statico usando i valori ID di stringa ***e*** le funzioni gx_display_string_get_ext o ***gx_widget_string_get_ext'API.*** Queste funzioni restituiscono il **GX_STRING** associato a un ID stringa specificato e alla lingua attualmente attiva.

### <a name="bi-directional-text-display"></a>Visualizzazione testo bidirezionale 

GUIX offre due strategie per il supporto del testo bidirezionale.

Un'opzione è eseguire il riordinamento del testo dell'offerta all'interno dell'applicazione GUIX Studio. L'uso di questa opzione guiX Studio è responsabile della generazione di testo offeri nel file di output nell'ordine di visualizzazione. Questa soluzione non ha alcun impatto sulle prestazioni di runtime e non richiede aggiunte alla libreria di runtime GUIX. Per consentire a GUIX Studio di generare stringhe di testo dell'offerta displayorder, è necessario selezionare la casella di controllo Generate **Offeri Text in Display Order** (Genera testo offeri nell'ordine di visualizzazione) nella finestra di dialogo di configurazione della lingua di GUIX Studio:

![Configurare le lingue](./media/guix/user-guide/configure-languages.png)

Con queste opzioni selezionate, il file di risorse generato conterrà le stringhe Offeri generate in ordine di visualizzazione e non è necessaria alcuna elaborazione aggiuntiva all'interno della libreria di runtime GUIX.

La seconda opzione è eseguire il riordinamento del testo offeri in fase di esecuzione. Questa opzione è supportata per le applicazioni che devono gestire stringhe di testo offeri definite in modo dinamico e non generate dall'applicazione GUIX Studio. In questo caso la libreria di runtime GUIX è responsabile del riordinamento del testo dell'offerta prima di disegnare ogni stringa di testo. Questa soluzione ha un impatto sulle prestazioni di runtime e sulla memoria. Per il processo di riordinamento del testo di Offeri deve essere disponibile memoria dinamica sufficiente. Questa soluzione richiede che il GX_DYNAMIC_BIDI_TEXT_SUPPORT essere definito durante la compilazione della libreria GUIX. Sono disponibili due funzioni ***API gx_system_bidi_text_enable*** ***e gx_system_bidi_text_disable*** per abilitare/disabilitare il supporto del testo offeri in fase di esecuzione.

Non è consigliabile usare sia **GX_DYNAMIC_BIDI_TEXT_SUPPORT** che configurare GUIX Studio per generare testo Offeri in ordine di visualizzazione. È necessario selezionare una strategia o l'altra per la gestione delle stringhe di testo di offeri.

## <a name="memory-usage"></a>Utilizzo memoria 

GUIX risiede insieme al programma dell'applicazione. Di conseguenza, l'utilizzo della memoria statica (o memoria fissa) di GUIX è determinato dagli strumenti di sviluppo; ad esempio il compilatore, il linker e il localizzatore. L'utilizzo della memoria dinamica (o della memoria di run-time) è sotto il controllo diretto dell'applicazione.

### <a name="static-memory-usage"></a>Utilizzo della memoria statica 

La maggior parte degli strumenti di sviluppo divide l'immagine del programma dell'applicazione in cinque aree di *base:* istruzione *,* costante *,* dati inizializzati, dati non inizializzati e stack di thread *GUIX*.  La figura seguente illustra un possibile layout di queste aree di memoria:

![Layout in memoria](./media/guix/user-guide/memory-area-example.png)

È importante comprendere che questo è solo un esempio. Il layout effettivo della memoria statica è specifico del processore, degli strumenti di sviluppo, dell'hardware sottostante e dell'applicazione stessa.

L'area delle istruzioni contiene tutte le istruzioni del processore del programma. Quest'area si trova spesso nella ROM.

L'area costante contiene varie costanti compilate, che in GUIX contengono le impostazioni predefinite e tutte le risorse dell'applicazione (immagini, stringhe, tipi di carattere e colori). Inoltre, quest'area contiene la "copia iniziale" dell'area dati inizializzata. Durante il processo di inizializzazione del compilatore, questa parte dell'area costante viene usata per configurare i dati inizializzati globali nella RAM. L'area costante è in genere la più grande e segue in genere l'area di istruzioni e si trova spesso nella ROM.

Le mappe pixel GUIX e i tipi di carattere richiedono in genere grandi quantità di archiviazione dei dati costante. Queste aree dati statiche di grandi dimensioni vengono in genere mantenute in ROM o FLASH.

Lo stack di thread GUIX viene definito all'interno dell'area dei dati non inizializzati (come variabile globale) nel file ***gx_system.h*** come indicato di seguito:

```C
_gx_system_thread_stack[GX_THREAD_STACK_SIZE];
```

**GX_THREAD_STACK_SIZE** è definito in **_gx_port.h,_** ma può essere sottoposto a override dall'applicazione definendo questo simbolo nel file di intestazione ***gx_user.h*** o tramite opzioni di progetto o parametri della riga di comando. Le dimensioni dello stack devono essere sufficientemente grandi da gestire la gestione degli eventi del caso peggiore e le chiamate di disegno annidate.

### <a name="dynamic-memory-usage"></a>memoria dinamica utilizzo 

Come accennato in precedenza, l'utilizzo della memoria dinamica è sotto controllo diretto dell'applicazione. I blocchi di controllo e la memoria associati alle aree di disegno e così via possono essere posizionati in qualsiasi punto dello spazio di memoria della destinazione. Si tratta di una funzionalità importante perché facilita l'utilizzo di diversi tipi di memoria fisica in fase di esecuzione.

Si supponga, ad esempio, che un ambiente hardware di destinazione abbia memoria veloce e memoria lenta. Se l'applicazione necessita di prestazioni aggiuntive per il disegno, la memoria canvas può essere inserita in modo esplicito nell'area di memoria ad alta velocità per ottenere prestazioni ottimali.

Diversi servizi e funzionalità GUIX facoltativi richiedono un meccanismo di allocazione della memoria dinamica di runtime, comunemente definito heap. Questi servizi e funzionalità sono completamente facoltativi e molte applicazioni GUIX non usano alcun heap e non definiscono un meccanismo di allocazione della memoria di runtime.

Se si usano servizi che richiedono l'allocazione della memoria di runtime, è necessario installare le funzioni che GUIX chiamerà quando la memoria deve essere allocata o liberata dinamicamente. È possibile implementare queste funzioni come si preferisce, in modo che anche in questo caso la posizione del pool di memoria dinamica sia sotto il controllo delle applicazioni. Per installare il supporto per l'allocazione  dinamica della memoria, l'applicazione deve richiamare il gx_system_memory_allocator_set API durante l'avvio del programma per definire l'allocazione di memoria e i servizi senza memoria. Per un esempio completo, vedere la documentazione di questa API.

I servizi GUIX che richiedono un servizio di allocazione e deallocazione della memoria di runtime includono:

  - Caricamento di risorse binarie da una risorsa di archiviazione esterna nell'ambiente di runtime GUIX.

  - Decodificatore di immagini jpeg di runtime del software.

  - Decodificatore di immagine PNG del runtime software.

  - Uso di widget di testo con GX_STYLE_TEXT_COPY.

  - Funzioni di utilità di ridimensionamento e rotazione pixemap di runtime.
  - Allocazione dei blocchi di controllo del widget e della schermata di runtime.

Per le applicazioni più piccole, le risorse GUIX vengono in genere compilate e collegate in modo statico come parte dell'immagine dell'applicazione e l'installazione di risorse binarie non è necessaria. Le risorse binarie consentono a un'applicazione di installare risorse (tipi di carattere, immagini, lingue) in fase di esecuzione caricate da una posizione di archiviazione, ad esempio un'unità flash o un URL.

I decodificatori jpeg e png di runtime sono componenti facoltativi. La maggior parte delle applicazioni GUIX consente lo strumento GUIX Studio di pre-decodificare tutti i file di immagine necessari e di archiviarli come risorse di dati GUIX Pixemap proprietarie. Questi servizi vengono forniti per completezza per le applicazioni che richiedono la conversione in runtime di immagini jpeg e/o PNG in formato pixelmap.

**GX_STYLE_TEXT_COPY** consente all'utente di specificare che uno o più widget specifici manderanno la propria copia privata del testo assegnato dinamicamente. L'uso di questa opzione richiede l'installazione del meccanismo di allocazione della memoria prima dell'uso. Se questo flag di stile non **<span class="underline">viene</span>** specificato quando viene creato un widget di tipo testo, l'applicazione deve allocare aree di archiviazione statiche per tutte le stringhe di testo create e assegnate dinamicamente. Le variabili automatiche non devono essere usate in questo caso per contenere i dati stringa generati dal runtime. Se lo **stile GX_STYLE_TEXT_COPY** è abilitato, le variabili automatiche possono essere usate per contenere i dati stringa assegnati ai widget GUIX, poiché ogni widget creerà una propria copia del testo assegnato.

Le funzioni di utilità di ridimensionamento e rotazione della mappa pixel restituiscono la mappa pixel tradotta risultante come nuova mappa pixel disponibile per l'applicazione.
Se vengono usati questi servizi, deve essere disponibile memoria dinamica sufficiente per contenere questi blocchi di dati pixelmap generati dal runtime.

Infine, i blocchi di controllo per le schermate e i widget GUIX possono essere allocati in modo statico o dinamico. Per le applicazioni più piccole, è comune creare tutte le schermate dell'applicazione durante l'avvio del programma e usare blocchi di controllo allocati staticamente. Per le applicazioni di grandi dimensioni, è comune creare dinamicamente i controlli dello schermo e del widget figlio in base alle esigenze. I blocchi di controllo allocati dinamicamente vengono specificati selezionando la casella di controllo **Runtime Allocate** (Alloca runtime) nella visualizzazione delle proprietà di GUIX Studio o passando il flag di stile **GX_STYLE_DYNAMICALLY_ALLOCATED** durante la creazione di un widget tramite l'API standard. L'uso di blocchi di controllo widget allocati dinamicamente richiede che i servizi di allocazione e deallocazione della memoria siano definiti come descritto in precedenza.

## <a name="guix-components"></a>Componenti GUIX 

Le API GUIX sono divise e organizzate in diversi gruppi di base che corrispondono ai componenti fondamentali del sistema GUIX. I componenti fondamentali includono:

| Componenti  | Descrizione  |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GX_SYSTEM  | Componente di sistema GUIX, responsabile dell'inizializzazione, degli eventi, dei timer, delle tabelle di stringhe e della gestione visibile della gerarchia dei widget.                                                                                                                                                                                                                                                                      |
| GX_CANVAS  | Area di disegno. Un canvas può essere un'astrazione sottile del buffer dei frame hardware oppure può anche essere un canvas di memoria pura. Il tipo di area di disegno è determinato dai parametri passati alla gx_canvas_create'API.                                                                                                                                                                                   |
| GX_CONTEXT | Componente del contesto di disegno. Il contesto di disegno contiene informazioni su schermo, area di disegno, pennello e area di ritaglio per le operazioni di disegno correnti.                                                                                                                                                                                                                                      |
| GX_DISPLAY | Fornisce le API e le implementazioni a livello di driver per consentire all'applicazione e ai widget GUIX di eseguire il disegno su un'area di disegno. GX_DISPLAY viene implementato per eseguire correttamente il rendering della grafica in ogni area di disegno usando il formato colore richiesto dell'area di disegno. Il GX_DISPLAY gestisce anche le risorse (colori, tipi di carattere e mappe pixel) disponibili per i widget che disegnano le aree di disegno collegate a ogni visualizzazione. |
| GX_WIDGET  | Oggetto widget visibile di base e API associate. Tutti i tipi di widget GUIX sono basati o derivati dal tipo di GX_WIDGET base.                                                                                                                                                                                                                                                                      |
| GX_UTILITY | In questo gruppo sono incluse funzioni di utilità per l'utilizzo di rettangoli, funzioni per la conversione di stringhe e funzioni matematiche non ANSI.                                                                                                                                                                                                                                                         |

Oltre a questi componenti di base, GUIX include API univoche per ogni tipo di widget fornito nella libreria. Queste API sono descritte nel capitolo 4 di questo Manuale dell'utente, "Descrizione dei servizi GUIX".

## <a name="guix-system-component"></a>Componente di sistema GUIX

Il componente di sistema GUIX fornisce diversi servizi globali per l'applicazione dell'interfaccia utente. Questi servizi includono: *inizializzazione, gestione degli eventi, gestione dello schermo, gestione delle risorse, gestione timer e* *gestione dei widget.* Ogni servizio è essenziale per l'organizzazione del programma applicativo e questi servizi sono descritti in modo più dettagliato nelle sottose sezioni seguenti.

### <a name="initialization"></a>Inizializzazione 

L'inizializzazione GUIX viene eseguita dall'applicazione che chiama il servizio ***gx_system_initialize***, che può essere chiamato dall'applicazione dalla routine ***tx_application_define*** ThreadX (contesto di inizializzazione) o dai thread dell'applicazione. La ***gx_system_initialize*** inizializza tutte le strutture di dati GUIX globali e crea il mutex di sistema GUIX, la coda di eventi, il timer e il thread. Dopo ***gx_system_initialize,*** l'applicazione può usare GUIX.

### <a name="thread-processing"></a>Elaborazione di thread 

Il thread GUIX interno, creato durante l'inizializzazione, è responsabile della maggior parte dell'elaborazione in GUIX. L'elaborazione in questo thread completa prima qualsiasi inizializzazione aggiuntiva richiesta dal driver di visualizzazione sottostante. Al termine, il thread GUIX entra in un ciclo che prima elabora tutti gli eventi presenti nella coda di eventi GUIX e quindi aggiorna la schermata, se necessario. L'aggiornamento dello schermo esegue le funzioni di disegno GUIX necessarie, in base a ciò che è visibile ed è stato contrassegnato come dirty, ovvero deve essere ridisegnato. Quando non sono presenti eventi e non rimane nulla da aggiornare sullo schermo, il thread GUIX verrà sospeso, in attesa dell'arrivo dell'evento GUIX successivo.

### <a name="rtos-binding"></a>Associazione RTOS 

Per impostazione predefinita, il componente di sistema GUIX è configurato per l'utilizzo del sistema operativo ThreadX in tempo reale per servizi quali servizi thread, servizi di accodamento eventi e servizi timer. È possibile convertire facilmente GUIX in altri sistemi operativi usando la direttiva del preprocessore GX_DISABLE_THREADX_BINDING e ricompilare la libreria GUIX. In questo modo vengono rimosse le dipendenze ThreadX dal codice sorgente GUIX e lo sviluppatore dell'applicazione può implementare i servizi del sistema operativo necessari usando qualsiasi RTOS fornito dal sistema di destinazione. [Appendice F - GUIX RTOS Binding Services](appendix-f.md) descrive i servizi che devono essere implementati per convertire GUIX in un sistema operativo diverso dal sistema operativo ThreadX.

### <a name="multithread-safety"></a>Sicurezza multithread 

L'API GUIX è disponibile dal contesto del thread GUIX e da altri thread dell'applicazione. I thread dell'applicazione possono interagire con il thread GUIX inviando e ricevendo eventi, accedendo alle variabili condivise e usando le funzioni API GUIX. GUIX usa un mutex ThreadX interno per la protezione delle risorse multi-thread. INOLTRE, GUIX impedisce la modifica della struttura interna dei widget visibili dopo l'avvio di un'operazione di aggiornamento dello schermo. Le API che modificano l'albero degli oggetti visibili vengono bloccate mentre sono in corso operazioni di disegno e rilasciate al termine dell'aggiornamento dello schermo.

### <a name="system-timers"></a>Timer di sistema 

GUIX fornisce all'applicazione timer periodici, che vengono spesso usati per l'aggiornamento periodico dei dati visualizzati nelle finestre GUIX. Questa operazione viene eseguita tramite un timer periodico ThreadX, che viene usato anche per eseguire effetti a livello di sistema GUIX come la dissolvenza dello schermo in entrata/uscita e così via.

L'applicazione può creare timer e usare la stessa funzionalità timer usata internamente da GUIX. Naturalmente, l'applicazione può anche creare e usare direttamente i timer ThreadX, se necessario. Il vantaggio dei timer GUIX è che sono molto facili da usare e sono preconfigurato per funzionare all'interno del sistema di elaborazione guiX basato su eventi.

Per creare e avviare un timer GUIX, l'applicazione deve richiamare la funzione ***gx_system_timer_start***. I parametri per questa funzione includono un puntatore al widget chiamante, l'ID timer (che consente a un widget di avviare molti timer) e i valori di timeout iniziale e ripianificazione. Se il valore di timeout della ripianificazione è 0, il timer verrà eseguito una sola volta e verrà eliminato dall'elenco dei timer attivi alla scadenza.

Una volta avviato, il timer GUIX invierà GX_EVENT_TIMEOUT eventi al proprietario del timer, una sola volta o periodicamente a seconda del valore di ripianificazione del timer. Un timer GUIX può essere arrestato chiamando la funzione API ***gx_system_timer_stop***.

### <a name="pen-speed-configuration"></a>Configurazione della velocità della penna 

Il componente di sistema GUIX contiene le informazioni di configurazione correlate al rilevamento della velocità della penna. GuiX generato internamente **GX_EVENT_VERTICAL_FLICK** e **GX_EVENT_HORIZONTAL_FLICK** eventi in base alla velocità e alla distanza degli eventi di PEN_DOWN generati dal driver di input tocco, se presenti. L'applicazione può configurare la distanza minima e la velocità necessarie per attivare questi eventi generati internamente usando la **_gx_system_pen_configure_** API.

### <a name="screen-stack"></a>Stack dello schermo 

Il componente di sistema GUIX fornisce servizi correlati allo stack di schermate GUIX, una funzionalità facoltativa che supporta uno stack di widget virtuali in cui l'applicazione può eseguire il push, il recupero e il recupero delle schermate in fase di esecuzione. Lo stack dello schermo è utile per la gestione di sistemi di menu complessi, in cui il percorso con cui l'utente può arrivare a vari stati nel sistema di menu è vario. Per tornare allo stato precedente nel sistema di menu, è possibile eseguire facilmente il push dello stato precedente della schermata, quindi visualizzare la nuova schermata e consentire alla nuova schermata di visualizzare lo stato precedente dallo stack di schermate quando la schermata corrente viene chiusa.

### <a name="clipboard-maintenance"></a>Manutenzione degli Appunti 

GUIX supporta gli Appunti per copiare e incollare testo durante l'esecuzione del runtime. Questo supporto viene fornito dal componente GUIX System.

### <a name="dirty-list-maintenance"></a>Manutenzione elenco dirty 

GUIX gestisce un elenco di widget dirty, vale a dire widget visibili e che devono essere ridisegnato a causa di modifiche dello stato o appena resi visibili. Questo elenco dirty migliora le prestazioni di disegno consentendo a GUIX di eseguire un'operazione di aggiornamento dell'area di disegno per riflettere tutte le modifiche correnti apportate allo stato dell'interfaccia utente, anziché eseguire un aggiornamento dell'area di disegno man mano che viene apportata ogni modifica dell'interfaccia utente.
Questo elenco dirty viene gestito anche dal componente di sistema GUIX.

### <a name="animation-control-block-pool"></a>Pool di blocchi di controllo dell'animazione 

Le applicazioni spesso desiderano eseguire più sequenze di animazione, spesso in parallelo. GUIX gestisce un pool di blocchi di controllo di animazione da cui l'applicazione può allocare e usare. In questo modo l'applicazione non definisce staticamente questi blocchi di controllo e li riutilizza in momenti diversi, anziché definire un blocco di controllo di animazione univoco per ogni animazione che l'applicazione potrebbe definire. Il pool di blocchi di controllo dell'animazione viene gestito anche dal componente di sistema GUIX.

### <a name="system-error-handling"></a>Gestione degli errori di sistema 

Il gestore degli errori di sistema GUIX è progettato per aiutare l'applicazione a trovare errori di sistema interni in GUIX che potrebbero essere più difficili da determinare dal punto di vista dell'API. Ogni volta che si verifica un errore di sistema all'interno di GUIX, ***_gx_system_error_process*** chiamata della funzione interna. Questa funzione salva il codice di errore fornito e incrementa il numero totale di errori di sistema rilevati. Le variabili di errore di sistema sono definite come segue:

UINT **_gx_system_last_error**;

ULONG **_gx_system_error_count**;

Se l'applicazione GUIX si comporta in modo strano, è utile esaminare la variabile di conteggio degli errori nel debugger. Se è impostata, un modo efficace per risolvere il problema è impostare un punto di interruzione nella funzione ***_gx_system_error_process*** e vedere quando/dove viene chiamato.

## <a name="guix-canvas-component"></a>Componente canvas GUIX

Il componente canvas è responsabile di tutte le elaborazioni correlate all'area di disegno. Un canvas è in effetti un buffer di frame virtuale. L'applicazione deve creare almeno un'area di disegno per produrre output grafico.
In genere, si crea almeno un'area di disegno per ogni visualizzazione fisica supportata dal sistema.

Tutto il disegno GUIX avviene in un'area di disegno. Nei sistemi più semplici o con vincoli di memoria, è probabile che sia presente una sola area di disegno collegata direttamente al buffer dei frame visibile, mentre i sistemi con requisiti di memoria e grafica più avanzati potrebbero richiedere più canvas. La disponibilità di più aree di disegno per un unico schermo abilita funzionalità come la dissolvenza dello schermo e della finestra e gli effetti di dissolvenza in entrata e in uscita.
I canvas possono essere di due tipi principali, semplici o gestiti.

Un'area di disegno semplice è un'area di disegno fuori schermo usata dall'applicazione.
GUIX non esegue alcuna operazione direttamente con un'area di disegno semplice, ma l'applicazione può usare un'area di disegno semplice per eseguire il rendering di un disegno complesso in un buffer fuori schermo e quindi usare questo buffer fuori schermo per aggiornare l'area di disegno visibile quando necessario.

Un'area di disegno gestita viene visualizzata automaticamente all'interno del buffer dei frame hardware da GUIX. Un'area di disegno gestita è inclusa nella creazione di un'area di disegno composita per i sistemi con memoria sufficiente per supportare più canvas gestiti. Le aree di disegno gestite hanno un ordine Z gestito da GUIX e il ritaglio della visualizzazione viene applicato a tutte le aree di disegno gestite.

Un'area di disegno è diversa da un buffer di frame perché è più generica. Nei sistemi con vincoli di memoria può essere presente una sola area di disegno e la memoria per questa area di disegno potrebbe essere la memoria visibile del buffer dei frame. Tuttavia, per sistemi più complessi che supportano sovrimpressione grafica più avanzate e più aree di disegno, alle aree di disegno gestite vengono allocate le proprie aree di memoria distinte dalla memoria buffer dei frame hardware.
Il rendering di queste aree di disegno gestite viene eseguito nel buffer dei frame visibile durante l'operazione di aggiornamento o attivazione/disattivazione del buffer dei frame.

Per l'hardware che supporta più livelli di grafica, ad esempio più buffer di frame sovrapposti, l'applicazione può associare uno o più canvas ai livelli di grafica hardware usando l'API ***gx_canvas_hardware_layer_bind.*** Questo servizio informa l'area di disegno che è collegata a un particolare livello grafico hardware e, una volta collegato, l'area di disegno tenterà di usare il supporto hardware per la visibilità dell'area di disegno, ad esempio gx_canvas_show, gx_canvas_hide), la fusione alfa dell'area di disegno (ad esempio ***gx_canvas_alpha_set***) e l'offset dell'area di disegno all'interno della visualizzazione ***(gx_canvas_offset_set***).

Per architetture diverse dall'organizzazione più semplice di buffer canvas singolo/frame singolo, le dimensioni di un'area di disegno sono determinate dall'applicazione e possono essere diverse da quelle fisse di un buffer di frame.
Può anche essere in corrispondenza di un offset selezionato dall'applicazione. Altre informazioni, ad esempio l'ordine Z, vengono mantenute all'interno dell'area di disegno. Al termine del disegno nell'area di disegno, il contenuto dell'area di disegno viene trasferito alla visualizzazione fisica dal driver di visualizzazione. In alcuni sistemi che non hanno memoria sufficiente per un'area di disegno separata e aree di memoria del buffer dei frame, l'aggiornamento dell'area di disegno viene effettivamente effettuato direttamente sulla visualizzazione fisica tramite il driver di visualizzazione.

### <a name="canvas-creation"></a>Creazione di canvas 

Un oggetto canvas può essere creato durante l'inizializzazione o in qualsiasi momento durante l'esecuzione dei thread dell'applicazione. Non esiste alcun limite al numero di oggetti canvas che possono essere creati da un'applicazione. La maggior parte delle applicazioni, tuttavia, creerà un solo oggetto canvas per tutti i disegni GUIX.

### <a name="canvas-control-block"></a>Blocco di controllo Canvas 

Le caratteristiche di ogni oggetto canvas si trovano nel blocco **di controllo** GX_CANVAS e sono definite in **_gx_api.h._** La memoria necessaria per un oggetto canvas viene fornita dall'applicazione e può essere posizionata in qualsiasi punto della memoria. Tuttavia, è più comune rendere il blocco di controllo dell'oggetto canvas e l'area di disegno una struttura globale definendoli all'esterno dell'ambito di qualsiasi funzione.

### <a name="canvas-alpha-channel"></a>Canale alfa canvas

GUIX supporta la fusione alfa dei colori di primo piano e di sfondo su molti livelli, tra cui il canale alfa della bitmap che specifica un rapporto di fusione per pixel, il valore alfa del pennello che specifica il rapporto di fusione per un pennello a 16 bpp e profondità di colore superiori e il valore alfa dell'area di disegno che specifica il rapporto di fusione per un'area di disegno sovrapposta.

Il valore alfa di un'area di disegno viene usato quando sono presenti più aree di disegno che vengono composte insieme per la visualizzazione all'interno del buffer dei frame. Se l'ordine Z dell'area di disegno è tale che un'area di disegno si trova sopra altre aree di disegno, il valore alfa dell'area di disegno può essere impostato in modo da unire l'area di disegno con quelle che si trovano dietro. La modifica rapida del valore alfa di un'area di disegno viene usata per fornire effetti di transizione dello schermo "dissolvenza in entrata", ma il valore alfa dell'area di disegno può essere usato in molti modi.

Se un'area di disegno è associata a un livello di grafica hardware usando gx_canvas_hardware_layer_bind(), GUIX tenterà di implementare la fusione alfa dell'area di disegno usando il supporto hardware, riducendo al minimo il sovraccarico software associato alla fusione di un'area di disegno sovrapposta.

I valori alfa sono da 0 a 255, dove un valore pari a 0 indica che il pixel è completamente trasparente e i valori maggiori di 0 aumentano meno il valore alfa dell'area di disegno trasparente può essere supportato solo per i driver dello schermo in esecuzione a 16 bpp e superiori, a meno che non venga fornita assistenza hardware per la fusione di canvas.

### <a name="canvas-offset"></a>Offset area di disegno 

Un canvas può essere offset all'interno del buffer dei frame visibile richiamando il ***gx_canvas_offset_set*** API. Gli offset dell'area di disegno vengono in genere usati per implementare animazioni sprite. Se un'area di disegno è associata a un livello di grafica hardware richiamando la funzione API ***gx_canvas_hardware_layer_bind,*** GUIX tenterà di implementare le modifiche di offset dell'area di disegno usando il supporto hardware, riducendo al minimo il sovraccarico software associato allo spostamento della posizione dell'area di disegno.

### <a name="canvas-drawing"></a>Disegno canvas 

Il componente canvas GUIX fornisce un'API di disegno completa all'applicazione. Prima di poter richiamare  le API di disegno, ad esempio gx_canvas_line_draw o ***gx_canvas_pixelmap_draw,*** l'area di  disegno di destinazione deve essere aperta per il disegno richiamando la funzione API gx_canvas_drawing_initiate. Questa funzione prepara un'area di disegno per il disegno e crea un contesto ***di disegno***.

Le API di disegno di cui viene eseguito il rendering nell'area di disegno, ad esempio ***gx_canvas_line_draw** _ _*_o gx_canvas_text_draw_*_, usano i parametri presenti nel pennello del contesto di disegno corrente per definire lo stile, la larghezza e i colori della linea. Questi parametri del pennello vengono modificati chiamando _*_gx_context_brush_define_*_, _* _gx_context_brush_set_**, ***gx_context_brush_style_set**_ e funzioni API simili dopo che è stato stabilito un contesto di disegno chiamando _*_gx_canvas_drawing_initiate_**.

Quando GUIX richiama le funzioni di disegno della finestra e del widget come parte di un'operazione di aggiornamento posticipato dell'area di disegno, l'area di disegno di destinazione viene aperta per il disegno prima di chiamare le funzioni di disegno del widget. Di conseguenza, le funzioni di disegno standard del widget non sono necessarie per aprire l'area di disegno di destinazione. Questa operazione è stata eseguita per tali funzioni.

In alcuni casi l'applicazione potrebbe voler forzare il disegno immediato in un'area di disegno. In questo caso, l'applicazione può eseguire i passaggi seguenti.

1. Chiamare la funzione ***API gx_canvas_drawing_initiate,*** passando l'area di disegno di destinazione e il rettangolo all'interno dell'area di disegno su cui l'applicazione vuole disegnare. 

2. Chiamare un numero qualsiasi di API di disegno canvas per eseguire il disegno desiderato.

3. Chiamare la ***gx_canvas_drawing_complete*** API per segnalare che il disegno è stato completato. In questo modo l'area di disegno viene scaricata nel buffer dei frame visibile e/o viene attivata un'operazione di attivazione/disattivazione del buffer, a seconda dell'architettura della memoria di sistema.

### <a name="drawing-apis"></a>API di disegno 

Esistono diverse primitive di disegno principali richieste da GUIX per disegnare tutti gli elementi visivi sullo schermo. Queste API di disegno possono essere richiamate anche dal software applicativo, in genere come parte di una funzione di disegno personalizzata del widget. Queste API di disegno canvas GUIX eseguono la convalida e il ritaglio dei parametri e quindi passano le coordinate di disegno ritagliate al driver di visualizzazione per le implementazioni di disegno specifiche del formato hardware e del colore. Queste funzioni dell'API di disegno sono definite nel modo seguente.

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

L'API di disegno viene richiamata tramite l'API Canvas GUIX e tutte le attività di disegno vengono eseguite gx_canvas_* funzioni API. Il disegno viene eseguito usando il pennello corrente nel contesto di disegno corrente. Qualsiasi funzione di disegno della forma precedente può essere delineata, colorata a tinta unita o mappa pixel riempita in base a quanto definito dal pennello corrente. Per modificare lo spessore, il colore o il riempimento del contorno della forma, usare le funzioni api gx_context_brush_* per definire il pennello all'interno del contesto di disegno corrente.

Le API di disegno a livello di applicazione precedenti non ese tracciano effettivamente l'area di disegno, ma verificano i parametri del chiamante prima di richiamare la funzione di disegno a livello di driver di visualizzazione. La funzione di disegno a livello di driver scrive effettivamente i dati pixel nella memoria dell'area di disegno.

GUIX offre funzioni di disegno di driver di visualizzazione stock o generiche per diverse profondità di colore, tra cui 1, 2, 4, 8, 16, 24 e 32 bit per pixel (bpp). In alcuni casi, l'implementazione del disegno software predefinita viene sostituita da implementazioni con accelerazione hardware per le destinazioni hardware che forniscono un acceleratore di disegno 2D.

### <a name="color-depth"></a>Profondità colore 

GUIX supporta profondità di colore fino a 32 bpp, nonché monocroma e gradazioni di grigio. Il tipo di profondità del colore è in gran parte determinato dalle funzionalità della visualizzazione fisica sottostante e influisce anche sulla quantità di memoria necessaria per l'area di disegno dell'area di disegno. Di seguito è riportato un elenco del supporto della profondità del colore insieme a una breve descrizione delle variazioni all'interno di tale profondità di colore.

| Formato &nbsp; colore       | Descrizione                                                                                                   |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| Monocromatico a 1 bit   | Formato a 1 bit per pixel.                                                                                                   |
| Scala di grigi a 2 bit    | 4 livelli di grigio, imballati quattro pixel per byte.                                                                                      |
| Scala di grigi a 4 bit    | 16 livelli di grigio, imballati di due pixel per byte.                                                                                      |
| Colore a 4 bit        | Un'organizzazione di memoria planare in formato VGA.                                                                                         |
| Scala di grigi a 8 bit    | 256 livelli di grigio                                                                                                                  |
| Modalità tavolozza a 8 bit | 1 byte per pixel usato come indice della tavolozza                                                                                           |
| Modalità r:g:b a 8 bit   | Formato 2:3:2 r:g:b meno comunemente usato.                                                                                         |
| 16 bit             | Ogni pixel richiede due byte. Può essere r:g:b o b:g:r byte order. In genere struttura 5:6:5, ma può anche essere struttura 5:5:5 o 4:4:4:4 a:r:g:b. |
| 24 bit             | Ogni pixel richiede 3 (formato compresso) o 4 (formato non compresso). Può essere in ordine di byte r:g:b o b:g:r come richiesto dall'hardware. |
| 32 bit             | Ogni pixel richiede 4 byte con un canale alfa. Può essere a:r:g:b o b:g:r:a byte order e determinato dall'hardware.              |

### <a name="mouse-support"></a>Supporto del mouse 

GUIX supporta il disegno di un cursore del mouse su qualsiasi area di disegno desiderata. Il cursore del mouse può essere di disegno nel software o potrebbe essere supportato dalla sovrapposizione del cursore hardware. In entrambi i casi, l'API fornita all'applicazione correlata al supporto del cursore del mouse è la stessa sia che si utilizzi il disegno del cursore del mouse software o hardware.

Il supporto del mouse GUIX è abilitato solo se è definito nel file di intestazione gx_user.h prima di `#define GX_MOUSE_SUPPORT` compilare la libreria GUIX.

L'applicazione deve definire il cursore del mouse e l'area sensibile usando la ***gx_canvas_mouse_define*** API. Questa API accetta un puntatore all'area di disegno su cui disegnare l'immagine del cursore e un puntatore a una struttura **GX_MOUSE_CURSOR_INFO,** che definisce l'immagine del cursore del mouse e l'area sensibile dell'immagine del mouse relativa all'angolo superiore sinistro dell'immagine.

## <a name="guix-display-component"></a>Componente di visualizzazione GUIX 

Il componente di visualizzazione è fondamentale in GUIX, poiché gestisce l'elaborazione di tutti gli oggetti di visualizzazione, che di per sé contengono uno o più canvas, widget e finestre. Il componente di visualizzazione interagisce anche con il driver dello schermo hardware sottostante associato a ogni visualizzazione tramite una serie di puntatori a funzione.

### <a name="display-creation"></a>Creazione della visualizzazione 

Un oggetto di visualizzazione può essere creato durante l'inizializzazione o in qualsiasi momento durante l'esecuzione dei thread dell'applicazione. In genere un'applicazione crea un oggetto di visualizzazione per gestire ogni schermo fisico. Se GUIX Studio è stato usato per definire l'applicazione e gli schermi fisici disponibili, si userà la funzione API gx_studio_display_configure per creare e inizializzare ogni visualizzazione.

### <a name="display-control-block"></a>Visualizzare il blocco di controllo 

Le caratteristiche di ogni oggetto di visualizzazione si trovano nel blocco di controllo *** GX_DISPLAY** _ e sono definite in _*_gx_api.h_**. La memoria necessaria per un oggetto di visualizzazione viene fornita dall'applicazione e può essere posizionata in qualsiasi punto della memoria. Tuttavia, è più comune fare in modo che il controllo di visualizzazione blocchi una struttura globale definendo il controllo all'esterno dell'ambito di qualsiasi funzione.

### <a name="resource-management"></a>Gestione delle risorse 

Le risorse sono componenti dell'interfaccia utente necessari per l'applicazione, ma non sono codice dell'applicazione. Le risorse sono dati dell'applicazione e sono in genere definite in modo statico. I tipi di risorse includono mappe pixel, tipi di carattere, colori e stringhe. Queste risorse possono essere modificate in qualsiasi momento, in genere senza modificare il software dell'applicazione. È importante mantenere l'archiviazione di e i riferimenti alle risorse separati dal software dell'applicazione per consentire la modifica dell'aspetto dell'interfaccia utente senza modificare il codice dell'applicazione poiché le modifiche al software dell'applicazione richiedono in genere il test e la verifica associati di tale software.

Il modulo di ***visualizzazione*** GUIX fornisce funzionalità di gestione delle risorse per tutte le risorse che dipendono dalla profondità del colore e dal formato della visualizzazione. Queste funzionalità includono la gestione della tabella pixelmap attiva, della tabella dei caratteri attiva e della tabella dei colori attiva. La risorsa della tabella di stringhe viene gestita dal modulo di sistema GUIX, poiché le risorse stringa in genere non devono essere modificate in base alla profondità e al formato del colore.

Il software dell'applicazione fa riferimento alle risorse in base al relativo ID risorsa, ovvero un indice nella tabella delle risorse corrispondente. In questo modo è possibile modificare la tabella, ad esempio la tabella dei colori potrebbe essere modificata quando un prodotto cambia da "modalità giorno" a "modalità notte", ma i valori dell'ID colore rimangono invariati.

Le risorse dell'applicazione vengono scritte in un file di risorse (o in un set di file di risorse) dall'applicazione GUIX Studio. I colori predefiniti, le mappe pixel e i tipi di carattere vengono forniti automaticamente quando si crea un nuovo progetto GUIX Studio, ma questi valori predefiniti vengono facilmente sostituiti quando si definisce l'aspetto dell'applicazione.

È importante notare che gli ID risorsa per colori, tipi di carattere e pixelmap non possono essere risolti nei valori effettivi di colore, carattere o mappa pixel fino a quando il componente Display attivo non è noto. Poiché l'architettura GUIX supporta più schermi attivi, gli ID risorsa possono essere risolti in valori di risorsa solo quando un widget e l'ID risorsa associato possono essere risolti in una visualizzazione specifica. Questa proprietà è nota come associazione dinamica. L'ID risorsa per una proprietà, ad esempio un colore di testo, ad esempio l'ID risorsa **GX_COLOR_ID_TEXT,** potrebbe risolversi in un valore R:G:B a 16 bit per il bianco se usato in un unico schermo, ma lo stesso ID colore potrebbe risolversi in un valore di colore nero monocromatico quando usato in un altro display.

In pratica, questa associazione dinamica degli ID risorse ai valori delle risorse implica che il software dell'applicazione e i componenti interni GUIX devono risolvere in genere solo gli ID risorsa in valori di risorsa all'interno di un contesto di disegno attivo. Un contesto di disegno attivo specifica la visualizzazione attualmente attiva, che consente a GUIX di risolvere ogni ID risorsa in un valore di risorsa specifico. Se il software dell'applicazione è necessario per trovare un valore di risorsa specifico all'esterno di un contesto di disegno, questa operazione può essere eseguita anche per i widget visibili. I widget visibili sono collegati a una finestra radice che può essere usata anche per risolvere l'area di disegno attiva e la visualizzazione per tale widget.

Se un widget è stato creato ma non ancora visualizzato (ad esempio, non è stato collegato ad alcuna finestra radice o ad altri elementi padre visibili), gli ID risorsa associati a tale widget non possono essere risolti in un valore di risorsa specifico diverso dall'indicizzazione diretta nella tabella delle risorse assegnata a una visualizzazione specifica. Questo accesso diretto a una tabella di risorse specifica può essere eseguito in modo sicuro dal software dell'applicazione, ma non viene mai eseguito nel software della libreria GUIX interna.

### <a name="widget-defaults"></a>Impostazioni predefinite del widget 

Il componente di visualizzazione GUIX fornisce anche definizioni predefinite per vari attributi del widget. Se non diversamente specificato dall'applicazione, i widget/finestre vengono creati con questi attributi di sistema. Questi attributi di sistema sono costituiti principalmente da tipi di carattere, colori e bitmap gestiti nelle tabelle delle risorse di sistema. Anche gli attributi aggiuntivi per l'aspetto predefinito della barra di scorrimento vengono gestiti dal componente di visualizzazione GUIX.

Le impostazioni dei colori predefinite sono definite dalla tabella dei colori assegnata a ogni visualizzazione e dagli ID colore predefiniti. Questi ID colore predefiniti includono quanto segue.

| ID colore | Descrizione |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| GX_COLOR_ID_CANVAS | Colore predefinito dell'area di disegno ,ad esempio lo sfondo visualizzato |
| GX_COLOR_ID_WIDGET_FILL | Colore di riempimento del widget predefinito |
| GX_COLOR_ID_WINDOW_FILL | Colore di riempimento predefinito della finestra |
| GX_COLOR_ID_DISABLED_FILL | Colore di riempimento del widget disabilitato predefinito |
| GX_COLOR_ID_DEFAULT_BORDER | Colore predefinito del bordo del widget |
| GX_COLOR_ID_WINDOW_BORDER | Colore predefinito del bordo della finestra |
| GX_COLOR_ID_TEXT | Colore del testo predefinito |
| GX_COLOR_ID_SELECTED_TEXT | Colore predefinito del testo selezionato |
| GX_COLOR_ID_DISABLED_TEXT | Colore del testo disabilitato predefinito |
| GX_COLOR_ID_SELECTED_TEXT_FILL | Colore di riempimento del testo selezionato predefinito |
| GX_COLOR_ID_READONLY_TEXT | Colore del testo di sola lettura predefinito |
| GX_COLOR_ID_READONLY_FILL | Colore di riempimento del testo di sola lettura predefinito |
| GX_COLOR_ID_SCROLL_FILL |    Colore di riempimento della barra di scorrimento |
| GX_COLOR_ID_SCROLL_BUTTON | Colore di riempimento del pulsante della barra di scorrimento |
| GX_COLOR_ID_SHADOW | Colore ombreggiatura predefinito |
| GX_COLOR_ID_SHINE | Colore di evidenziazione predefinito |
| GX_COLOR_ID_BUTTON_BORDER | Colore del bordo del widget del pulsante |
| GX_COLOR_ID_BUTTON_UPPER | Colore di riempimento superiore del widget del pulsante |
| GX_COLOR_ID_BUTTON_LOWER | Colore di riempimento inferiore del widget del pulsante |
| GX_COLOR_ID_BUTTON_TEXT | Colore del testo del widget del pulsante |
| GX_COLOR_ID_TEXT_INPUT_TEXT | Colore del testo del widget di input di testo |
| GX_COLOR_ID_TEXT_INPUT_FILL | Colore di riempimento dell'input di testo |
| GX_COLOR_ID_SLIDER_TICK | Colore usato per disegnare i segni di graduazione del dispositivo di scorrimento. |
| GX_COLOR_ID_SLIDER_GROOVE_BOTTOM | Colore usato per disegnare il dispositivo di scorrimento |
| GX_COLOR_ID_SLIDER_NEEDLE_OUTLINE | Colore usato per disegnare il contorno dell'ago |
| GX_COLOR_ID_SLIDER_NEEDLE_FILL | Colore usato per riempire l'ago del dispositivo di scorrimento |
| GX_COLOR_ID_SLIDER_NEEDLE_LINE1 | Colore usato per disegnare l'evidenziazione dell'ago |
| GX_COLOR_ID_SLIDER_NEEDLE_LINE2 | Colore usato per disegnare l'ombreggiatura dell'ago |

Questi valori id colore vengono mappati a un valore di colore specifico, come definito dalla tabella dei colori assegnata a ogni visualizzazione. Queste impostazioni predefinite possono essere modificate come gruppo per una visualizzazione chiamando la gx_display_color_table_set ***api.*** Se si usa GUIX Studio, la tabella dei colori di visualizzazione viene inizializzata automaticamente quando l'applicazione chiama la ***gx_studio_display_configure*** funzione.

Il componente di visualizzazione GUIX mantiene anche una tabella dei tipi di carattere predefinita. La tabella dei tipi di carattere predefinita definisce il tipo di carattere usato da ogni tipo di widget, a meno che non sia specificato in modo specifico dall'applicazione. Gli ID predefiniti della tabella dei tipi di carattere di visualizzazione includono i valori seguenti.

| &nbsp;ID carattere | Descrizione |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------|
| GX_FONT_ID_DEFAULT | Tipo di carattere predefinito usato quando non è definito alcun tipo di carattere specifico |
| GX_FONT_ID_BUTTON | Tipo di carattere predefinito usato per tutto il testo sui pulsanti |
| GX_FONT_ID_TEXT_INPUT | Tipo di carattere predefinito usato per i campi di modifica del testo |

L'ID carattere usato da qualsiasi widget di tipo testo può essere assegnato nuovamente usando l'API **gx_<widget_type>_font_set** fornita per ogni tipo di widget correlato al testo. L'intera tabella dei tipi di carattere può essere riasserta chiamando la **gx_display_font_table_set** api.

### <a name="scrollbar-appearance"></a>Aspetto della barra di scorrimento 

GuiX Display mantiene anche le impostazioni predefinite dell'aspetto della barra di scorrimento per tale visualizzazione. Queste impostazioni sono definite dalla **struttura** GX_SCROLLBAR_APPEARANCE definita di seguito. GuiX Display mantiene una struttura di aspetto della barra di scorrimento per le barre di scorrimento verticali e una seconda struttura per le barre di scorrimento orizzontali. L'applicazione può modificare l'aspetto predefinito della  barra di scorrimento per qualsiasi visualizzazione inizializzando una struttura GX_SCROLLBAR_APPEARANCE e richiamando la funzione API ***gx_display_scroll_appearance_set***.

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
| GX_SCROLLBAR_APPEARANCE membro della struttura | Descrizione |
| --- | --- |
| gx_scroll_width | Larghezza, in pixel, di una barra di scorrimento verticale o dell'altezza di una barra di scorrimento orizzontale. |
| gx_scroll_thumb_width | Larghezza dei pulsanti dell'ascensore e della fine, in pixel. |
| gx_scroll_thumb_travel_max | Offset dalla fine della barra di scorrimento al punto di spostamento massimo del pulsante di scorrimento. |
| gx_scroll_fill_pixelmap | Mappa pixel usata per riempire lo sfondo dello scorrimento. |
| gx_scroll_thumb_pixelmap | Mappa pixel usata per disegnare il pulsante di scorrimento della casella di scorrimento. |
| gx_scroll_up_pixelmap | Mappa pixel usata per disegnare il pulsante di scorrimento verso l'alto. |
| gx_scroll_down_pixelmap | Mappa pixel usata per disegnare il pulsante di scorrimento verso il basso. |
| gx_scroll_fill_color | ID colore del colore usato per riempire lo sfondo della barra di scorrimento. |
| gx_scroll_button_color | ID colore del colore usato per riempire il pulsante della casella di scorrimento della barra di scorrimento. |

Oltre a queste impostazioni predefinite per i tipi di carattere, il colore e gli stili, l'applicazione può specificare uno dei parametri caso per caso in base alle esigenze usando l'API fornita da ogni tipo di widget.

### <a name="skinning-and-themes"></a>Interfaccia e temi

La skinning consente ai widget e alle finestre GUIX di modificare facilmente l'aspetto di base, ad esempio, la modifica dell'"interfaccia" in un'unica posizione modificherà l'aspetto di base di tutti i widget e le finestre associati.

Per ri-eseguire l'interfaccia utente grafica dell'applicazione GUIX è necessario specificare una nuova tabella di colori, tipi di carattere e pixelmap alle tabelle delle risorse GUIX Display. Poiché tutti i widget GUIX fanno riferimento al colore, alla bitmap o al tipo di carattere in base all'ID risorsa, se si specifica una nuova tabella delle risorse, tutti i widget GUIX iniziano automaticamente a usare i nuovi colori e mappe pixel quando si disegnano sulla visualizzazione desiderata.

Un nuovo set di tipi di carattere, colori e pixelmap progettati per funzionare insieme per offrire un aspetto accattivante è denominato *tema*. Un tema definisce un set di tabelle di risorse e le dimensioni di ogni tabella delle risorse. È possibile definire un numero qualsiasi di temi per qualsiasi visualizzazione usando l'applicazione GUIX Studio. È necessario passare l'indice del tema iniziale alla funzione generata da GUIX Studio ***gx_studio_display_configure***, che installa il tema iniziale nella visualizzazione creata. Il tema attivo per qualsiasi visualizzazione può essere modificato in qualsiasi momento chiamando la funzione ***gx_display_theme_install***.

### <a name="root-window"></a>Finestra radice

Per ogni area di disegno visibile creata da un'applicazione, l'applicazione deve anche creare una finestra radice per tale area di disegno. Questa finestra speciale funge fondamentalmente da contenitore per tutte le finestre e i widget dell'applicazione di primo livello. La finestra radice disegna lo sfondo dell'area di  disegno e poiché la finestra radice è derivata dalla classe GX_WINDOW la finestra radice può anche avere lo sfondo. Per modificare il colore di sfondo dello schermo o dell'area di disegno, è sufficiente modificare il colore di riempimento della finestra radice associata a tale area di disegno.

Se si usa la funzione generata da GUIX Studio denominata ***gx_studio_display_configure*** per configurare gli schermi, l'area di disegno e la finestra radice per ogni visualizzazione vengono create automaticamente come parte di questa funzione di inizializzazione.

### <a name="anti-aliasing"></a>Antialiasing 

L'antialiasing è una funzionalità facoltativa di GUIX usata per smussare linee, curve e tipi di carattere. L'antialiasing è supportato solo quando si esegue con un driver di visualizzazione che usa una profondità di colore di 16 bpp o superiore.

Il disegno a linee con antialiasing viene abilitato impostando GX_BRUSH_ALIAS **flash** nel pennello attivo. Questo vale per le linee disegnate direttamente, nonché per le linee disegnate come bordo di un poligono o di un cerchio.

Il disegno di testo con anti-aliasing viene abilitato usando un tipo di carattere con anti-aliasing prodotto dall'applicazione GUIX Studio. Specificare se un tipo di carattere deve essere generato come antialias o binario quando si crea il tipo di carattere.
I tipi di carattere con anti-aliasing in GUIX utilizzano 16 livelli di trasparenza per ogni pixel.

### <a name="clipping"></a>Ritaglio 

Il ritaglio è supportato internamente dal componente di visualizzazione GUIX e nei livelli finestra e widget dall'architettura padre-figlio gestita dai widget GUIX. Non è mai consentito disegnare all'esterno dell'area del widget e un widget non può mai disegnare all'esterno dell'area dell'elemento padre del widget.

In questo modo si impedisce anche ai widget di disegnare in corrispondenza di coordinate di pixel che si trova all'esterno della memoria dell'area di disegno, causando probabilmente un danneggiamento della memoria o un errore di sistema. I widget non possono disegnare all'esterno dell'area del widget, dell'area padre del widget o oltre l'estensione dell'area di disegno.

Inoltre, i widget possono essere disegnati solo in aree precedentemente contrassegnate come dirty. Ciò impedisce che venga disegnata un'intera finestra, ad esempio quando viene visualizzato solo un angolo della finestra. Solo la parte della finestra che deve essere effettivamente aggiornata è contrassegnata come dirty, quindi la funzione di disegno della finestra aggiorna effettivamente solo i pixel nell'area dirty.

Il componente di visualizzazione GUIX applica questi algoritmi di ritaglio prima di richiamare le funzioni di disegno a livello di driver.

### <a name="views"></a>Viste 

GUIX mantiene sempre un set di visualizzazioni per ogni finestra radice e ogni finestra figlio della finestra radice. Le visualizzazioni sono un'area di ritaglio dinamica e determinata in fase di esecuzione che cambia in base alla posizione della finestra e all'ordine Z.
GUIX usa le visualizzazioni per impedire il disegno di una finestra o un widget in background sopra una finestra o un widget in primo piano. Le visualizzazioni applicano la disciplina ordine Z. Inoltre, le visualizzazioni sono importanti per l'efficienza, in quanto impediscono a una finestra in background di disegnare in qualsiasi area dell'area di disegno che non può essere visualizzata. Se una finestra è completamente coperta da un'altra finestra, la finestra coperta non sarà affatto autorizzata a disegnare nell'area di disegno, anche se tenta di eseguire questa operazione.

### <a name="display-driver-interface"></a>Interfaccia del driver di visualizzazione 

I driver di visualizzazione GUIX sono responsabili di tutte le interazioni con lo schermo fisico sottostante. I driver di visualizzazione hanno tre funzioni di base: inizializzazione, disegno e visualizzazione del buffer dei frame.
L'inizializzazione è responsabile della preparazione dell'hardware di visualizzazione fisico, dell'informare GUIX delle proprietà dell'hardware di visualizzazione fisico e di informare GUIX delle funzioni di disegno specifiche da usare. L'inizializzazione del driver di  visualizzazione principale viene chiamata dalla funzione gx_display_create GUIX. Inoltre, il thread GUIX chiamerà anche l'inizializzazione di un driver di visualizzazione secondario dal contesto del thread. Questo driver video secondario è necessario solo se il driver richiede servizi RTOS durante l'inizializzazione, ad esempio interruzioni del dispositivo o richieste ***tx_thread_sleep*** di ritardo tra i passaggi del processo di inizializzazione.

Al termine dell'inizializzazione, il driver di visualizzazione è responsabile di qualsiasi disegno diretto che può essere eseguito nell'hardware dello schermo fisico.
Infine, il driver di visualizzazione è responsabile della visualizzazione del buffer dei frame.

## <a name="guix-widget-component"></a>Componente GUIX Widget

Un widget GUIX è un elemento grafico visibile. Alcuni componenti GUIX non sono visibili, ad esempio timer e funzioni di utilità matematica.
Tuttavia, tutti i componenti visibili derivano dal componente widget GUIX di base. Un widget GUIX è il blocco predefinito principale della visualizzazione GUIX: tutti gli altri elementi grafici derivano dalla funzionalità del widget di base.

I widget GUIX vengono implementati in modo orientato agli oggetti con supporto completo dell'ereditarietà. Questa operazione viene eseguita tramite ANSI C, che comporta i più piccoli requisiti di memoria ed elaborazione possibili. Quando si parla di un particolare widget, ad  esempio **GX_BUTTON ,** derivato da un altro widget, ad esempio il **GX_WIDGET** di base, si intende che la struttura del controllo **GX_BUTTON** contiene tutte le variabili membro e i puntatori a funzione di **GX_WIDGET**, con alcune variabili aggiuntive specifiche di **GX_BUTTON**. GUIX crea livelli di widget in questo modo, in modo che i widget più complessi siano sempre basati su un widget più semplice prima di essi. Questo modello gerarchico di derivazione semplifica l'apprendimento delle API usate per modificare i parametri del widget. Se si vuole modificare il colore di un pulsante, usare la stessa API che si usa per modificare il colore di un widget, vale a gx_widget_fill_color_set ***.***

L'organizzazione dei widget visibili viene gestita in modo padre-figlio usando elenchi strutturati ad albero che collegano i widget figlio ai relativi elementi padre. Gli elementi figlio ereditano caratteristiche dai rispettivi elementi padre, ad esempio le visualizzazioni in cui possono disegnare e l'area di disegno su cui disegnano.
I widget figlio possono avere i propri widget figlio, ereditando di nuovo varie caratteristiche dall'elemento padre. Le caratteristiche di qualsiasi widget possono essere ridefinite in modo esplicito tramite varie chiamate API GUIX.

### <a name="widget-creation"></a>Creazione di widget 

Un oggetto widget può essere creato durante l'inizializzazione o in qualsiasi momento durante l'esecuzione dei thread dell'applicazione. Non esiste alcun limite al numero di oggetti widget che possono essere creati da un'applicazione. Non esiste inoltre alcun limite al numero di elementi figlio che un widget può avere, entro i limiti di memoria dell'hardware di destinazione.

Ogni tipo di widget ha una propria funzione di creazione, ad esempio ***gx_button_create** _ o _*_gx_prompt_create_**. I primi tre parametri di queste funzioni sono sempre gli stessi, vale a esempio un puntatore alla struttura di controllo del widget, un puntatore di stringa al nome del widget e un puntatore all'elemento padre del widget. Ogni funzione di creazione può avere un numero qualsiasi di parametri aggiuntivi a seconda dei requisiti di quel particolare tipo di widget.

### <a name="widget-control-block"></a>Blocco di controllo widget 

Le caratteristiche di ogni oggetto widget si trovano nel blocco **di controllo** GX_WIDGET e sono definite in **_gx_api.h._** La memoria necessaria per un oggetto widget viene fornita dall'applicazione e può essere posizionata in qualsiasi punto della memoria. Tuttavia, è più comune fare in modo che il controllo oggetto widget blocchi una struttura globale definendo l'oggetto all'esterno dell'ambito di qualsiasi funzione. Se si usa GUIX Studio, i blocchi di controllo widget possono essere allocati staticamente all'interno del file delle specifiche generate da Studio oppure possono essere allocati dinamicamente dall'applicazione.

### <a name="dynamic-widget-control-block-allocation-and-de-allocation"></a>Allocazione e deallocazione dei blocchi di controllo widget dinamici 

Se si usa l'allocazione dinamica dei blocchi di controllo, è necessario definire due funzioni che GUIX userà per allocare e liberare la memoria necessaria per i blocchi di controllo del widget. Le funzioni per la gestione della memoria vengono passate al componente di sistema GUIX tramite la ***gx_system_memory_allocator_set*** API. Questa funzione consente di passare due puntatori a funzione in GUIX: il primo è un puntatore a una funzione di allocazione di memoria e il secondo è un puntatore a una funzione senza memoria. Nella maggior parte dei casi, queste funzioni vengono implementate usando pool di byte ThreadX, ma la progettazione di GUIX consente di implementare la gestione dinamica della memoria nel modo preferito.

L'allocazione dinamica dei widget viene spesso utilizzata all'interno del file di specifiche dell'applicazione generato da Studio, quando si seleziona l'opzione "allocata dinamicamente" nel campo Proprietà del widget di Studio. Tuttavia, è anche possibile usare l'allocazione dinamica dei blocchi di controllo all'interno dell'applicazione. Se si usa l'allocazione dinamica dei blocchi di controllo all'interno dell'applicazione, è necessario richiamare la funzione ***gx_widget_allocate** _API per allocare il blocco di controllo widget. Successivamente, quando si crea il widget, assicurarsi di passare il flag di stile _ GX_WIDGET_STYLE_DYNAMICALLY_ALLOCATED * (insieme *a* tutti gli altri flag di stile necessari) alla funzione di creazione del widget. Questo flag viene usato per contrassegnare il widget come allocato dinamicamente nel campo stato del widget. Quando e se il widget viene eliminato in un secondo momento **_usando gx_widget_delete_**, GUIX controlla questo campo di stato e chiama automaticamente la funzione di deallocazione della memoria per assicurare che non si siano verificate perdite di memoria.

> [!IMPORTANT]
> Un widget creato usando un blocco di controllo allocato dinamicamente deve essere creato con il flag **GX_WIDGET_STYLE_DYNAMICALLY_ALLOCATED** per evitare la perdita di memoria.

### <a name="types"></a>Tipi

GUIX offre un set completo e funzionale di widget predefiniti. Come accennato in precedenza, tutti i widget specializzati derivano dal widget di base. Di seguito è riportato un elenco dei widget predefiniti in GUIX:

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

Gli stili dei widget sono costituiti da elementi come le proprietà del bordo (in rilievo, in rilievo, sottile, spessore o nessun lavagna) e le proprietà per tipi di widget specifici, come elencato in precedenza. I flag di stile del widget offrono il metodo più semplice per modificare l'aspetto di qualsiasi widget.
Lo stile del widget iniziale è sempre un parametro passato alla funzione di creazione specifica del tipo di widget.

### <a name="colors"></a>Colori 

I widget si disegnano usando i colori definiti nella tabella dei colori di sistema.
Gli ID colore sono definiti per lo sfondo dell'area di disegno, il colore di riempimento predefinito del widget, il colore di riempimento del pulsante, il colore di riempimento del widget di testo, il colore di riempimento della finestra e diversi altri valori di colore predefiniti. Inoltre, gli **GX_WINDOW** supportano la visualizzazione di una bitmap o di uno sfondo mentre il client della finestra viene riempito.

Il metodo più semplice per modificare la combinazione colori predefinita è usare GUIX Studio e creare o definire una combinazione colori che soddisfi i requisiti.
È anche possibile definire manualmente la combinazione colori creando una matrice di GX_COLOR valori e richiamando la gx_system_color_table_set API.

### <a name="event-notification"></a>Notifica dell'evento 

Gli eventi GUIX sono richieste inviate a uno o più widget per eseguire una determinata azione e notifiche per notificare ai widget l'input dell'utente e le modifiche dello stato interno del sistema. Ad esempio, quando un widget ottiene lo stato attivo, **il GX_EVENT_FOCUS_GAINED** viene inviato al widget tramite il ***gx_system_event_send*** API.

Gli eventi vengono passati attraverso la coda di eventi GUIX e ogni evento è un'istanza della **struttura GX_EVENT** dati. La **GX_EVENT** dei dati è definita in ***gx_api.h***, tuttavia i campi più importanti della struttura sono **gx_event_type**, **gx_event_sender**, **gx_event_target** e **gx_event_payload**.

Il **gx_event_type** viene usato per identificare la classe di evento specifica. Il tipo di evento indica se si tratta, ad esempio, di un evento **GX_EVENT_PEN_DOWN** o di un **GX_EVENT_TIMER** eventi. Il **gx_event_payload** è un'unione di vari campi dati e non sono tutti validi per ogni tipo di evento.
Usare prima il campo del tipo di evento prima di esaminare gli altri campi dati dell'evento.

Il **gx_event_sender** contiene l'ID del widget che ha generato l'evento se l'evento è una notifica del widget figlio.

Il **gx_event_target** campo può essere usato per instradare gli eventi definiti dall'utente a una determinata finestra o widget. Se **si** vuole inviare un evento a una determinata finestra, è necessario assegnare alla finestra un valore ID univoco (in modo che possa essere identificato in modo positivo) e, quando si compila l'evento, inserire il valore id della finestra nel campo gx_event_target. Se non si conosce l'ID di destinazione o si vuole solo che l'evento sia indirizzato al widget con lo stato attivo per l'input, assicurarsi di impostare il campo gx_event_target su 0. 

Infine, il **gx_event_payload** è un'unione di vari tipi di dati. Per **GX_EVENT_PEN_DOWN** e **GX_EVENT_PEN_UP** eventi, il  campo gx_event_pointdata contiene la coordinata x,y pixel della posizione della penna. Per gli eventi timer, **il gx_event_timer_id** contiene l'ID del timer scaduto. Altri campi dati di payload vengono utilizzati per altri tipi di evento. L'elenco completo dei tipi di evento predefiniti e dei relativi campi di payload è definito [nell'Appendice E - Descrizioni degli](appendix-e.md)eventi GUIX .

L'applicazione può anche aggiungere i propri eventi personalizzati, iniziando numericamente dopo la **costante GX_FIRST_APP_EVENT**. Tutti i numeri di evento dopo questa costante sono riservati per l'uso dell'applicazione. Naturalmente, il gestore eventi widget dell'applicazione deve disporre dell'elaborazione per tali eventi dell'applicazione.

### <a name="event-processing"></a>Elaborazione di eventi 

È disponibile una funzione di elaborazione degli eventi del widget predefinita per ogni widget, denominata gx_<***tipo di widget>_event_process***. Nella maggior parte dei casi, l'applicazione non dovrà preoccuparsi della gestione degli eventi di un determinato widget. Tuttavia, nelle situazioni in cui l'applicazione richiede l'elaborazione di eventi personalizzati o supplementari, l'applicazione può eseguire l'override della funzione di elaborazione predefinita con la propria tramite l'API GUIX ***gx_widget_event_process_set***. Questa funzione esegue l'override della funzione di elaborazione degli eventi predefinita con la funzione di elaborazione della funzione di evento specificata nell'API.

> [!IMPORTANT]
> Le funzioni di elaborazione degli eventi dell'applicazione possono sfruttare (ad esempio, non duplicare l'elaborazione) dell'elaborazione predefinita semplicemente chiamando direttamente l'gx_widget_event_process ***predefinita.***

L'elaborazione degli eventi viene chiamata esclusivamente dal contesto del thread di sistema GUIX interno. In questo modo, i requisiti dello stack per elaborare la gestione degli eventi si applicano solo al thread GUIX.

### <a name="implementing-custom-event-processing-example"></a>Implementazione dell'elaborazione di eventi personalizzata (esempio) 

È possibile fornire la propria funzione di elaborazione degli eventi per qualsiasi widget o finestra nel sistema GUIX. Se si sta creando un tipo di widget personalizzato, in genere si installerà il gestore eventi personalizzato nella funzione di creazione del widget. Se si sta semplicemente estendendo o modificando il funzionamento di un widget o di una finestra esistente, è possibile chiamare la funzione API gx_widget_event_process_set dopo la creazione del widget o della finestra. Quasi sempre si fornirà la propria gestione degli eventi per le finestre di primo livello (denominate anche schermate) per elaborare gli eventi generati dai controlli figlio. L'elaborazione dell'evento generato dai controlli figlio di una schermata è il modo principale per aggiungere funzionalità all'applicazione GUIX.

Si supponga, ad esempio, di definire una schermata di primo livello denominata "main_menu".
Questa schermata può essere definita usando GUIX Studio oppure è possibile creare questa schermata nel codice dell'applicazione. Se si definisce la schermata all'interno di GUIX Studio, è sufficiente digitare il nome del gestore eventi nel campo delle proprietà di Studio per tale schermata e il codice delle specifiche generate da Studio installerà automaticamente il gestore eventi. In questo caso, verrà chiamato il gestore eventi personalizzato main_menu_event_handler ***e*** deve essere codificato nel modo seguente:

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

Nell'esempio precedente è importante notare che per gli eventi di sistema come **GX_EVENT_SHOW** (eventi generati internamente per notificare a un widget una modifica dello stato), l'applicazione deve passare tali eventi alla funzione di elaborazione degli eventi del widget di base per assicurare che si verifichi l'elaborazione normale. L'applicazione può quindi aggiungere logica aggiuntiva in base alle esigenze. Tutti gli eventi non gestiti dall'applicazione (caso predefinito precedente) devono essere passati anche alla funzione di elaborazione degli eventi di base. Poiché questo esempio è stato per una schermata di primo livello basata su **GX_WINDOW**, la funzione di elaborazione degli eventi predefinita è gx_window_event_process.

### <a name="drawing-function"></a>Funzione Drawing 

Tutti i disegni dei widget vengono eseguiti separatamente dalla gestione degli eventi. Ciò è più efficiente perché il disegno è in genere dispendioso in termini di cicli della CPU. Implementando un algoritmo di disegno posticipato, tutti gli eventi in sospeso e le modifiche di visualizzazione associate possono essere completati prima di qualsiasi disegno, eliminando così il disegno sprecato. Analogamente all'elaborazione degli eventi, è disponibile una funzione di disegno del widget predefinita per la maggior parte dei widget, denominata ***gx_<widget-type>_draw***, dove xxx è il tipo di widget. Nella maggior parte dei casi, l'applicazione non dovrà preoccuparsi della funzione di disegno di un determinato widget. Tuttavia, nelle situazioni in cui l'applicazione richiede il disegno personalizzato o ***supplementare,*** l'applicazione può eseguire l'override della funzione di disegno predefinita con la propria tramite l'API GUIX gx_widget_draw_set . Questa funzione consente all'applicazione di fornire la propria funzione di disegno personalizzata per qualsiasi widget. In questo modo l'applicazione può definire interi nuovi tipi di widget.

> [!IMPORTANT]
> Le funzioni di disegno dell'applicazione possono sfruttare (ad esempio, non duplicare la codifica) del disegno predefinito semplicemente chiamandolo direttamente dalla funzione di disegno sottoposta a override.

Il disegno di widget viene chiamato esclusivamente dal contesto del thread di sistema GUIX interno. In questo modo, i requisiti di temporizzazione e stack per eseguire il disegno si applicano solo al thread GUIX.

### <a name="implementing-custom-drawing-example"></a>Implementazione del disegno personalizzato (esempio) 

Alla funzione di disegno per qualsiasi widget viene fatto riferimento tramite un puntatore a funzione indiretto che è un membro del blocco GX_WIDGET controllo. Se si usa GUIX Studio per definire il widget, è possibile installare il puntatore a funzione digitando semplicemente il nome della funzione nel parametro "Drawing Function" delle proprietà del widget e Studio installerà automaticamente il puntatore a funzione quando viene creato il widget. Se si crea il widget nel codice dell'applicazione, è necessario usare la funzione API ***gx_widget_draw_set*** per installare la funzione di disegno personalizzata dopo la creazione del widget.

Per questo esempio, si supponga di voler personalizzare l'aspetto di un pulsante. Il pulsante sarà molto simile a un **GX_TEXT_BUTTON**, ma verrà aggiunta una piccola bitmap verde "LED_ON" nella parte centrale destra del pulsante quando viene premuto il pulsante e una piccola bitmap "LED_OFF" quando il pulsante non viene premuto. Si vuole creare un pulsante simile alle illustrazioni seguenti.

![Screenshot del pulsante verde per On.](./media/guix/image4.jpg) pulsante personalizzato "on"

![Screenshot del pulsante rosso per Disattivato.](./media/guix/image5.jpg) pulsante personalizzato "disattivato"

In questo caso, scriveremo una funzione di disegno di pulsanti simile alla seguente.

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

Il contesto di disegno viene creato dinamicamente, in fase di esecuzione, quando GUIX esegue ogni operazione di aggiornamento dell'area di disegno. Il contesto di disegno riunisce l'area di disegno, il driver dello schermo e il pennello usati per eseguire le operazioni di disegno correnti.

Il contesto di disegno è definito dalla **GX_DRAW_CONTEXT** struttura .
Questa struttura contiene variabili che definiscono il ritaglio e la visualizzazione dell'operazione di disegno corrente, definiscono l'area di disegno corrente e definiscono il driver dello schermo corrente in uso. La **GX_DRAW_CONTEXT** contiene anche il pennello usato per il disegno. Il pennello del contesto di disegno è il membro che verrà utilizzato direttamente nelle funzioni di disegno personalizzate. La struttura del pennello è definita come illustrato nel codice seguente.

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

Il **gx_brush_pixelmap** definisce una mappa pixel da usare per i riempimenti di rettangoli e poligoni. Questo membro non viene usato a meno **che il gx_brush_style** non includa lo stile **GX_BRUSH_PIXELMAP** predefinito.

Il **gx_brush_font** definisce il tipo di carattere usato per il disegno del testo.
Il **gx_brush_line_pattern** definisce il modello usato per le linee tratteggiate.
Il **gx_brush_style** è un set di flag di stile che possono essere ord insieme per definire completamente gli attributi del pennello. I flag di stile del pennello disponibili includono i seguenti.

**GX_BRUSH_OUTLINE**  
**GX_BRUSH_SOLID_FILL**  
**GX_BRUSH_PIXELMAP_FILL**  
**GX_BRUSH_ALIAS**  
**GX_BRUSH_UNDERLINE**  
**GX_BRUSH_ROUND**

Il **gx_brush_width** definisce la linea con per il disegno a linee o lo spessore del contorno per il disegno di forme con contorno.

Il **gx_brush_line_color** definisce il colore di primo piano per il disegno di linee e per il disegno di testo.

Il **gx_brush_fill_color** definisce il colore di riempimento a tinta unita usato per il riempimento della forma. Il componente di contesto GUIX fornisce un set di API progettate per semplificare la modifica del pennello corrente all'interno del contesto attivo. Queste API **includono** gx_context_brush_define , **gx_context_line_color_set**, **gx_context_fill_color_set**, **gx_context_font_set** e molti altri.

Il contesto di disegno di un oggetto padre viene ereditato dagli oggetti figlio. In realtà, un clone del contesto di disegno padre viene ereditato dagli oggetti figlio quando vengono richiamate le relative funzioni di disegno. L'elemento figlio può modificare il contesto senza influire sul disegno padre, ma può anche ereditare informazioni dall'elemento padre, ad esempio il colore e lo stile del pennello, se lo si desidera.

## <a name="guix-window-component"></a>Componente della finestra GUIX 

Il componente finestra è responsabile di tutte le elaborazioni di finestre in GUIX. Una finestra GUIX è fondamentalmente un'area di visualizzazione distinta che può contenere uno o più widget figlio. In GUIX la finestra è in realtà solo una forma speciale dell'oggetto widget fondamentale.

Le finestre GUIX vengono implementate in modo orientato agli oggetti con il supporto completo dell'ereditarietà. Questa operazione viene eseguita usando ANSI C, che comporta il minor numero possibile di requisiti di memoria ed elaborazione.

Le finestre GUIX estendono principalmente le funzionalità del widget GUIX aggiungendo il supporto per lo scorrimento orizzontale e verticale. Gli oggetti finestra GUIX possono creare e visualizzare automaticamente barre di scorrimento e rispondere all'input della barra di scorrimento. Le finestre mobili hanno anche la gestione degli eventi incorporata per consentire lo spostamento o il trascinamento della finestra in base agli eventi di input della penna.
Infine, la finestra GUIX risponde alla ricezione dello stato attivo dell'input spostando la finestra nella parte anteriore dell'ordine Z della finestra.

La finestra GUIX mantiene il concetto di *area client*, ovvero la parte interna della finestra quando i bordi della finestra e gli oggetti non client, ad esempio le barre di scorrimento, vengono rimossi dall'area disponibile. I widget figlio dell'area client vengono ritagliati nell'area client della finestra, mentre gli elementi figlio non client, ad esempio le barre di scorrimento, possono disegnare all'esterno dell'area client, ma vengono ancora ritagliati nelle dimensioni esterne della finestra.

Windows vengono mantenute in modo padre-figlio, in cui gli elementi figlio ereditano le caratteristiche dal padre. Le finestre figlio possono avere finestre figlio proprie, ereditando di nuovo varie caratteristiche dal padre. Le caratteristiche di qualsiasi finestra possono essere ridefinite in modo esplicito tramite varie chiamate API GUIX.

### <a name="window-creation"></a>Creazione di finestre 

È possibile creare un oggetto finestra durante l'inizializzazione o in qualsiasi momento durante l'esecuzione dei thread dell'applicazione. Non esiste alcun limite al numero di oggetti finestra che possono essere creati da un'applicazione. Non esiste inoltre alcun limite al numero di elementi figlio che possono essere presenti in una finestra.

### <a name="window-control-block"></a>Blocco di controllo della finestra 

Le caratteristiche di ogni oggetto finestra si trovano nel blocco **di controllo GX_WINDOW** e sono definite in **_gx_api.h_**. La memoria necessaria per un oggetto finestra viene fornita dall'applicazione e può essere posizionata in qualsiasi punto della memoria. Tuttavia, è più comune fare in modo che il controllo oggetto finestra blocchi una struttura globale definendo il controllo all'esterno dell'ambito di qualsiasi funzione.

### <a name="root-window"></a>Finestra radice 

GUIX richiede quella che viene chiamata finestra radice per ogni area di disegno. La finestra radice è senza bordo e ha le stesse dimensioni dell'area di disegno a cui è collegata. Viene usato principalmente come contenitore per tutti i widget e le finestre di primo livello. La finestra radice viene in genere creata dall'applicazione tramite la funzione API ***gx_window_root_create***, subito dopo la creazione dello schermo e dell'area di disegno. Se si usa la funzione generata da Studio gx_studio_display_configure, l'indirizzo della finestra radice può essere restituito nella posizione passata come ultimo parametro a questa funzione.

Per impostazione predefinita, una finestra radice non è spostabile e, nel caso più semplice, la finestra radice è la dimensione dell'area di disegno. La finestra radice disegna lo sfondo dello schermo, quindi per modificare il colore di sfondo dello schermo o per visualizzare lo sfondo dello sfondo si assegna un colore o uno sfondo alla finestra radice.

Se una finestra radice è spostabile, non viene spostata modificandone la posizione nell'area di disegno come farebbe una finestra figlio, ma spostando l'area di disegno stessa.
Questa funzionalità consente alla finestra radice GUIX di sfruttare l'hardware che supporta più buffer frame con registri di offset hardware.

### <a name="background"></a>Sfondo 

Gli sfondi delle finestre sono colori a tinta unita o immagini bitmap. A livello di sistema è presente uno sfondo di finestra predefinito che fornisce l'impostazione predefinita per il set iniziale di finestre. Naturalmente, qualsiasi sfondo della finestra può essere modificato tramite l'API GUIX.

Per modificare lo sfondo a tinta unita di una finestra, usare l'API ***gx_widget_fill_color_set.*** Per assegnare uno sfondo a una finestra, usare l'API ***gx_window_wallpaper_set*** sfondo.

### <a name="scrolling"></a>Scorrimento 

GUIX supporta lo scorrimento della finestra standard quando l'area necessaria per visualizzare gli elementi figlio della finestra supera le dimensioni correnti della finestra, orizzontalmente e/o verticalmente. Per abilitare lo scorrimento, l'applicazione deve creare le barre di scorrimento desiderate e associarle alla finestra.

Il componente finestra GUIX fornisce un'implementazione di scorrimento predefinita in base alle dimensioni dell'area client della finestra e all'estensione di tutti i widget figlio. Le applicazioni possono anche fornire la propria implementazione e interpretazione dello scorrimento eseguendo l'override ***della funzione*** gx_window_scroll_info_get per una determinata finestra.

### <a name="event-notification"></a>Notifica dell'evento 

La funzione di elaborazione degli eventi della finestra predefinita è diversa GX_WIDGET'elaborazione degli eventi principalmente nella gestione degli eventi di scorrimento e ridimensionamento. GX_WINDOW gestori defalt forniti per gli eventi di scorrimento e ridimensionamento.

L'applicazione può anche aggiungere i propri eventi personalizzati, iniziando numericamente dopo la costante **GX_FIRST_APP_EVENT**. Tutti i numeri di evento dopo questa costante sono riservati per l'uso dell'applicazione. Naturalmente, il gestore eventi della finestra dell'applicazione deve disporre dell'elaborazione per tali eventi dell'applicazione.

### <a name="event-processing"></a>Elaborazione di eventi 

Analogamente a tutti gli altri tipi di widget, esiste una funzione di elaborazione degli eventi di finestra predefinita per ogni finestra, denominata ***gx_window_event_process***. In genere si esegue l'override di questa funzione di gestione degli eventi con il proprio gestore eventi nelle finestre create. In questo modo si risponderà agli eventi e si esererà un'azione in base agli eventi generati dai controlli figlio della finestra.

È importante ricordare di richiamare la funzione gx_window_event_process di base per gli eventi di sistema GUIX se si esegue l'override di tale gestore eventi, per consentire la gestione degli eventi predefinita ***oltre a*** qualsiasi azione da aggiungere al gestore eventi. Ad esempio, se si fornisce un gestore personalizzato per l'evento **GX_EVENT_SHOW** e non si passa questo evento a ***gx_window_event_process***, la finestra non diventerà mai visibile.
Per fornire un gestore eventi personalizzato per una finestra, usare la ***funzione gx_widget_event_process_set*** per definire l'indirizzo del gestore eventi. Questa funzione esegue l'override della funzione di elaborazione eventi predefinita con la funzione di elaborazione della funzione di evento specificata nell'API.

> [!IMPORTANT]
> Le funzioni di elaborazione degli eventi dell'applicazione possono sfruttare (ad esempio, non duplicare l'elaborazione) dell'elaborazione predefinita semplicemente chiamando direttamente il gx_window_event_process ***predefinito.***

L'elaborazione degli eventi viene chiamata esclusivamente dal contesto del thread di sistema GUIX interno. In questo modo, i requisiti dello stack per elaborare la gestione degli eventi si applicano solo al thread GUIX.

## <a name="guix-image-reader-component"></a>Componente lettore di immagini GUIX 

Il componente lettore di immagini fornisce utilità e funzioni API per decomprimere le immagini compresse non elaborati in formato pixelmap GUIX. Sono supportati i dati immagine non elaborati in formato JPEG e PNG, con formati aggiuntivi riservati per le versioni future.

Si noti che per la maggior parte delle applicazioni GUIX, il componente GuiX Image Reader non è necessario. La maggior parte delle applicazioni si basa sull'applicazione GUIX Studio per convertire gli asset grafici in formato JPEG e PNG in risorse grafiche compatibili con GUIX GX_PIXELMAP **risorse.** Il componente lettore di immagini GUIX viene utilizzato quando gli asset grafici non elaborati sono noti solo in fase di esecuzione o quando i vincoli di archiviazione di sistema impediscono l'archiviazione delle risorse **GX_PIXELMAP** formato. I dati immagine in formato JPEG e PNG sono in genere più compatti rispetto al formato **GX_PIXELMAP,** ma vi è un notevole sovraccarico di runtime associato all'esecuzione dinamica della decompressione e della conversione dello spazio colore di questi tipi di immagine.

Se le immagini JPEG o PNG in formato non elaborato vengono passate alla funzione API gx_canvas_pixelmap_draw, GUIX decomprime e disegna dinamicamente i dati JPEG o PNG. Si noti che ciò avrà un impatto negativo significativo sulla velocità di disegno di runtime e il passaggio di dati immagine in formato RAW alla funzione gx_canvas_pixelmap_draw non è consigliato a meno che non si utilizzi una destinazione hardware che supporta la decompressione JPEG o PNG assistita dall'hardware.

> [!IMPORTANT]
> Il passaggio di immagini in formato JPEG o PNG non elaborato all'API gx_canvas_pixelmap_draw comporta un sovraccarico di runtime significativo per la maggior parte dell'hardware di destinazione.

In alternativa, i dati JPEG e PNG non elaborati possono essere convertiti in GX_PIXELMAP in fase di esecuzione usando il componente Lettore di immagini.
Le mappe pixel prodotte in questo modo possono essere usate e disegnate esattamente come le mappe pixel prodotte da Studio e contenute nel file di risorse. In questo modo l'applicazione può eseguire una sola volta la decompressione, il dithering e la conversione dello spazio colori dell'immagine (in genere durante l'avvio del programma) anziché eseguire queste operazioni ogni volta che l'immagine viene disegnata.

Le funzioni del componente Lettore di immagini includono:

***gx_image_reader_create***  
***gx_image_reader_palette_set***  
***gx_image_reader_start***

## <a name="guix-animation-component"></a>Componente di animazione GUIX 

Il componente GUIX Animation è un set di funzioni e servizi usati per automatizzare le automazioni delle transizioni di schermo e widget. Il componente GUIX Animation supporta le animazioni di dissolversi, dissolversi e movimento o tipo di diapositiva di qualsiasi tipo di widget.

Le animazioni di tipo dissolvenza possono essere supportate variando il valore alfa interno dei widget in dissolvenza (se **GX_BRUSH_ALPHA_SUPPORT** è abilitato) o disegnando qualsiasi raccolta di widget in un'area di disegno della memoria separata quando viene quindi misto con lo sfondo. Per le destinazioni hardware che supportano più livelli di grafica hardware, è possibile ottenere il supporto per effetti uniformi di dissolvezza usando questo approccio di fusione dell'area di disegno, spesso con una larghezza di banda della CPU di base molto ridotta. Per le destinazioni hardware che non supportano più livelli grafici, la fusione con il valore alfa del pennello GUIX è supportata quando l'esecuzione è a 16 bpp e a profondità di colore superiori.

Se un'animazione deve usare un'area di disegno separata, il componente di animazione GUIX fornisce il servizio API gx_animation_canvas_define a questo scopo. Altri tipi di animazione non richiedono un'area di disegno separata, ma la utilizzeranno se disponibile. In questo modo è possibile usare al meglio qualsiasi supporto hardware sottostante per più superfici hardware.

Le variabili che controllano un'animazione sono definite da due blocchi di controllo. In primo luogo, **GX_ANIMATION** blocco di controllo che definisce il controller di animazione. Il controller di animazione è il motore di guida che esegue la sequenza di animazione definita. Un singolo controller di animazione può essere usato più volte per eseguire molte sequenze di animazione diverse. Se è necessario eseguire più sequenze di animazione contemporaneamente, è possibile creare più controller GX_ANIMATION **di** animazione.

Il componente di sistema GUIX può fornire un blocco riutilizzabile di strutture di controllo **GX_ANIMATION,** che possono essere richieste dall'applicazione quando è necessaria l'animazione e vengono restituite automaticamente al pool di sistema al termine della sequenza di animazione. In questo modo l'applicazione non definisce in modo statico una **GX_ANIMATION** per ogni animazione che potrebbe essere implementata. Le dimensioni di questo pool di **strutture GX_ANIMATION** sono definite dalla costante **GX_ANIMATION_POOL_SIZE**, che per impostazione predefinita è 6, il che significa che per impostazione predefinita è possibile allocare 6 animazioni simultanee dal pool di sistema. È ovviamente possibile ridefinire questa costante nel file di intestazione gx_user.h. Sono necessarie più animazioni simultanee. Se **GX_ANIMATION_POOL_SIZE** è impostato su zero, il componente di sistema GUIX non fornisce un pool di animazioni o i servizi correlati.

Il secondo blocco di controllo o struttura usato per definire un'animazione è la **GX_ANIMATION_INFO** struttura . Questa struttura viene usata per definire una sequenza di animazione specifica. Questa struttura di informazioni viene passata al controller di animazione per avviare una sequenza di animazione usando il gx_animation_start API. La **GX_ANIMATION_INFO** contiene i campi seguenti:

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

Il **gx_animation_target** definisce il widget di destinazione su cui agirà il controller di animazione.

Il **gx_animation_parent** definisce il widget padre, se presente, a cui verrà collegato il widget di destinazione al termine della sequenza di animazione. Il gx_animation_parent è anche il destinatario dell'evento GX_ANIMATION_COMPLETE generato quando viene completata un'animazione.

Il **gx_animation_screen_list** definisce un elenco di widget per le animazioni di scorrimento su schermo guidate da input penna. L'elenco widge deve terminare con un puntatore GX_NULL e ogni widget nell'elenco deve avere le stesse dimensioni x,y del gx_animation_parent.

La **gx_animation_style** è una maschera di bit che definisce il tipo di animazione da eseguire e le opzioni associate. I flag di stile dell'animazione includono quanto segue.

| Flag di &nbsp; stile di &nbsp; animazione | Descrizione |
| --- | --- |
| GX_ANIMATION_TRANSLATE | Richiedere un'animazione di tipo diapositiva o dissolvenza. |
| GX_ANIMATION_SCREEN_DRAG | Richiedere un'animazione di trascinamento dello schermo basata su input penna. |

I flag seguenti possono essere usati in combinazione con **SCREEN_DRAG** di tipo.

| Flag &nbsp; di trascinamento &nbsp; dello schermo | Descrizione |
| --- | --- |
| GX_ANIMATION_WRAP | L'elenco delle schermate dovrebbe andare a capo dall'inizio all'inizio. |
| GX_ANIMATION_HORIZONTAL | Il trascinamento dello schermo è consentito in direzione orizzontale.  |
| GX_ANIMATION_VERTICAL | Il trascinamento dello schermo è consentito in direzione verticale. |

Il flag seguente può essere usato in combinazione con le animazioni di traslazione.

| Convertire i &nbsp; flag delle animazioni &nbsp; | Descrizione |
| --- | --- |
| GX_ANIMATION_DETACH | Scollegare la destinazione dell'animazione dall'elemento padre dell'animazione al termine dell'animazione. Se la destinazione è stata allocata e creata in modo dinamico dalla gestione automatica degli eventi generata da GUIX Studio, la destinazione verrà eliminata dopo lo scollegamento. |
| GX_ANIMATION_TRANSLATE | I tipi di animazione sono animazioni guidate da timer. L'applicazione definisce la posizione iniziale e finale e il valore alfa iniziale e finale per il widget di destinazione e il gestore dell'animazione crea un timer da utilizzare e come forza trainante per eseguire l'animazione.
| GX_ANIMATION_SCREEN_DRAG | Differisce dalle animazioni **TRANSLATE** perché questo tipo di animazione è basato su eventi di input penna. Questo tipo di animazione tiene traccia insieme all'input del touchscreen per scorrere rapidamente il widget di destinazione mentre l'utente trascina una penna o uno stilo sul touchscreen di input. Per usare questo tipo di animazione, l'applicazione deve chiamare l'API **_gx_animation_drag_enable_** per abilitare questa animazione. |

Il **gx_animation_id** viene restituito all'elemento padre dell'animazione nel campo event.gx_event_sender dell'evento **GX_ANIMATION_COMPLETE.** Questo valore viene usato dall'elemento padre dell'animazione per determinare quale delle possibili animazioni figlio segnala il completamento. Questo valore può essere 0 e un'animazione con valore ID 0 non genererà un evento ANIMATION_COMPLETE **eventi.**

Il **gx_animation_start_delay** è un conteggio di tick GUIX che indica il numero di tick del timer da ritardare dopo che gx_animation_start _ viene chiamato prima di eseguire effettivamente ***l'animazione. Il valore può essere 0 per avviare l'animazione immediatamente dopo la chiamata a _*_gx_animation_start_**.

Il **gx_animation_frame_interval** definisce il numero di tick del timer GUIX (un multiplo della frequenza dei tick del sistema operativo sottostante) per ritardare tra ogni fotogramma della sequenza di animazione. Il valore minimo è 1.

Il **gx_animation_start_position** definisce il punto iniziale in alto a sinistra per il widget di destinazione per le animazioni di traslazione.

Il **gx_animation_end_position** definisce la posizione finale in alto a sinistra per il widget di destinazione per le animazioni con tipo di traslazione.

Il **gx_animation_start_alpha** definisce il valore alfa dell'area di disegno iniziale per le animazioni con tipo di traslazione.

Il **gx_animation_end_alpha** definisce il valore alfa dell'area di disegno finale per le animazioni con tipo di traslazione.

Il **gx_animation_steps** definisce il numero di passaggi o fotogrammi che il controller deve eseguire per le animazioni di traslazione. Un numero maggiore di passaggi produce una diapositiva e/o un aspetto di dissolvenza più smussato, ma richiede anche una maggiore larghezza di banda del sistema.

Per implementare gli effetti di animazione nell'applicazione, è innanzitutto necessario chiamare ***gx_animation_create*** per inizializzare il controller di animazione. Se l'animazione usa un canvas secondario, inizializzare l'area di disegno chiamando gx_animation_canvas_define. È quindi necessario inizializzare la **GX_ANIMATION_INFO** per definire il tipo specifico di animazione da eseguire e gli altri parametri di animazione. Infine, chiamare gx_animation_start per attivare la sequenza di animazione.

Quando il controller di animazione completa una sequenza di animazione, invia un evento **GX_ANIMATION_COMPLETE** al widget padre, consentendo la pulizia desiderata dell'area di disegno dell'animazione in quel momento.

## <a name="guix-utility-component"></a>Componente dell'utilità GUIX 

Il componente dell'utilità è responsabile di tutte le funzioni di utilità comuni in GUIX. Si tratta di funzioni comuni che sono utilità utili e possono essere richiamate da qualsiasi punto dell'applicazione o dal codice GUIX interno. Le funzioni del componente dell'utilità includono quanto segue.

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
