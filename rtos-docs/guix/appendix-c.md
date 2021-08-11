---
title: Appendice C - Stili dei widget GUIX
description: Informazioni sugli stili del widget GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9519d68af64b777e34deb1bf11e6962e78a96b86bdbfd90f5b379c5b56c92268
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784649"
---
# <a name="appendix-c---guix-widget-styles"></a>Appendice C - Stili dei widget GUIX

__***Stili generali (usati con la maggior parte dei tipi di widget):***__

**GX_STYLE_BORDER_NONE**
  - Valore: 0x00000000
  - Descrizione: usare questo stile per disegnare un widget senza bordo.

**GX_STYLE_BORDER_RAISED**
  - Valore: 0x00000001
  - Descrizione: disegnare un widget con un bordo in rilievo.

**GX_STYLE_BORDER_RECESSED**
  - Valore: 0x00000002
  - Descrizione: disegnare un widget con un bordo incassato.

**GX_STYLE_BORDER_THIN**
  - Valore: 0x00000004
  - Descrizione: disegnare un bordo di larghezza di un pixel.

**GX_STYLE_BORDER_THICK** 
  - Valore: 0x00000008
  - Descrizione: disegnare un widget con un bordo spesso.

**GX_STYLE_BORDER_MASK**
  - Valore: 0x0000000f
  - Descrizione: valore della maschera usato per testare solo i campi di stile del membro di stile del widget.

**GX_STYLE_TRANSPARENT**
  - Valore: 0x10000000
  - Descrizione: creare un widget almeno parzialmente trasparente. Questo stile deve essere usato quando un widget non disegna se stesso completamente opaco, inclusi i widget che disegnano una mappa pixel semitrasparente come sfondo del widget. Questo flag di stile informa GUIX che l'elemento padre del widget deve essere disegnato per aggiornare l'area di sfondo del widget.

**GX_STYLE_DRAW_SELECTED**
  - Valore: 0x20000000
  - Descrizione: specificare che il widget deve essere disegnato usando i colori e i tipi di carattere dello stato selezionati. Diversi tipi di widget usano lo DRAW_SELECTED in modi diversi per indicare che il widget è attualmente selezionato.

**GX_STYLE_ENABLED**
  - Valore: 0x40000000
  - Descrizione: contrassegnare il widget come abilitato, che consente al widget di accettare eventi di input utente e generare segnali di output.
  
**GX_STYLE_DYNAMICALLY_ALLOCATED**
  - Valore: 0x80000000
  - Descrizione: indica che la memoria del blocco di controllo del widget viene allocata dinamicamente usando il servizio gx_system_memory_allocator quando viene creato il widget e la memoria del blocco di controllo viene liberata se il widget viene eliminato.

**GX_STYLE_USE_LOCAL_ALPHA**
  - Valore: 0x01000000
  - Descrizione: indica alle funzioni di disegno GUIX di usare il valore alfa del widget locale durante il disegno del widget. Questo flag viene in genere usato dalla logica GUIX interna per implementare animazioni di dissolvente dei widget.


__***Stili di allineamento del testo (stili applicati a tutti i widget che disegnano testo):***__

**GX_STYLE_TEXT_LEFT**
  - Valore: 0x00001000
  - Descrizione: il testo viene disegnato allineato a sinistra all'interno dell'area client del widget.

**GX_STYLE_TEXT_RIGHT** 
  - Valore: 0x00002000
  - Descrizione: il testo viene disegnato allineato a destra all'interno dell'area client del widget.

**GX_STYLE_TEXT_CENTER**
  - Valore: 0x00004000
  - Descrizione: il testo viene disegnato allineato al centro all'interno dell'area client del widget.

**GX_STYLE_TEXT_COPY**
  - Valore: 0x00008000
  - Descrizione: per impostazione predefinita, i widget che disegnano testo mantengono solo un puntatore al testo passato dall'applicazione. Per il testo definito in modo statico definito all'interno della tabella di stringhe, il widget non deve creare una copia privata del testo assegnato. Tuttavia, se il testo assegnato a un widget viene creato dinamicamente usando funzioni come sprint() o gx_utility_ltoa, è spesso utile indicare al widget di mantenere la propria copia privata di qualsiasi testo assegnato. Ciò consente all'applicazione di usare variabili automatiche o temporanee durante la definizione della stringa di testo, quando in caso contrario sarebbe necessario definire matrici di caratteri definite in modo statico per ogni widget di testo che usa testo definito dinamicamente. Quando questo flag di stile è impostato, il widget userà la funzione gx_system_memory_allocator per allocare dinamicamente il blocco di memoria necessario per contenere una copia privata della stringa assegnata. L'uso di questo flag di stile viene quindi predicato nell'applicazione che definisce memory_allocator e memory_deallocator funzioni. GX_STYLE_TEXT_COPY non deve essere cancellata dopo l'impostazione e questa operazione causerà risultati imprevedibili.

__***Stili dei pulsanti (si applicano solo ai tipi di widget dei pulsanti GUIX):***__

**GX_STYLE_BUTTON_PUSHED**
  - Valore 0x00000010
  - Descrizione: indica che il pulsante è nello stato premuto o selezionato.

**GX_STYLE_BUTTON_TOGGLE**
  - Valore 0x00000020
  - Descrizione: il pulsante cambia stato tra push e annullamento del push in ogni evento click. Questo stile viene comunemente usato con i pulsanti di stile "checkbox".

**GX_STYLE_BUTTON_RADIO**
  - Valore 0x00000040
  - Descrizione: questo stile indica che il pulsante sarà esclusivo e deseleziona eventuali elementi di pari livello del pulsante quando selezionato. Questo stile viene comunemente usato con i pulsanti di stile "pulsante di opzione".

**GX_STYLE_BUTTON_EVENT_ON_PUSH**
  - Valore: 0x00000080
  - Descrizione: indica che il pulsante genera un evento click quando viene inizialmente premuto. L'operazione predefinita è generare un evento click quando viene rilasciato il pulsante.

**GX_STYLE_BUTTON_REPEAT**
  - Valore 0x00000100
  - Descrizione: indica che il pulsante deve inviare eventi click ripetuti all'elemento padre del pulsante quando il pulsante viene mantenuto nello stato di push.

__***Stili elenco (si applicano solo ai tipi di widget elenco GUIX):***__

**GX_STYLE_CENTER_SELECTED** 
  - Valore: 0x00000010
  - Descrizione: Riservato

**GX_STYLE_WRAP**
  - Valore 0x00000020
  - Descrizione: gli elementi figlio dell'elenco vengono a capo dall'inizio alla fine quando l'elenco viene trascinato o scorre oltre l'indice dell'elenco iniziale o finale.

**GX_STYLE_FLICKABLE**
  - Valore: 0x00000040
  - Descrizione: Riservato

__***Stili dei pulsanti Mappa pixel e Pulsante icona:***__

**GX_STYLE_HALIGN_CENTER**
  - Valore: 0x00010000
  - Descrizione: la mappa pixel del pulsante deve essere allineata al centro all'interno del limite del pulsante sull'asse orizzontale.

**GX_STYLE_HALIGN_LEFT**
  - Valore: 0x00020000
  - Descrizione: la mappa pixel del pulsante deve essere allineata a sinistra all'interno del limite del pulsante sull'asse orizzontale.

**GX_STYLE_HALIGN_RIGHT**
  - Valore 0x00040000
  - Descrizione: la mappa pixel del pulsante deve essere allineata a destra all'interno del limite del pulsante sull'asse orizzontale.

**GX_STYLE_VALIGN_CENTER**
  - Valore 0x00080000
  - Descrizione: la mappa pixel del pulsante deve essere allineata al centro all'interno del limite del pulsante sull'asse verticale.

**GX_STYLE_VALIGN_TOP**
  - Valore: 0x00100000
  - Descrizione: la mappa pixel del pulsante deve essere allineata in alto all'interno del limite del pulsante sull'asse verticale.

**GX_STYLE_VALIGN_BOTTOM**
  - Valore: 0x00200000
  - Descrizione: la mappa pixel del pulsante deve essere allineata in basso all'interno del limite del pulsante sull'asse orizzontale verticale.

__***Stili dispositivo di scorrimento (appy solo per GX_SLIDER e i tipi di widget derivati):***__

**GX_STYLE_SHOW_NEEDLE**
  - Valore: 0x00000200
  - Descrizione: questo stile deve essere incluso per il dispositivo di scorrimento per disegnare l'indicatore della lanceta. Questo stile può essere disabilitato se l'applicazione vuole disabilitare la lanceta del dispositivo di scorrimento o disegnare un indicatore della lanceta personalizzato.

**GX_STYLE_SHOW_TICKMARKS**
  - Valore: 0x00000400
  - Descrizione: il widget del dispositivo di scorrimento esegue il disegno software di linee con segni di graduazione tratteggiati quando questo stile è abilitato.

**GX_STYLE_SLIDER_VERTICAL**
  - Valore 0x00000800
  - Descrizione: impostare questo flag di stile per creare un dispositivo di scorrimento verticale e deselezionare questo flag di stile per creare un dispositivo di scorrimento orizzontale.

__***Stili Sprite (si applica solo ai GX_SPRITE di widget):***__

**GX_STYLE_SPRITE_AUTO**
  - Valore: 0x00000010
  - Descrizione: indica che l'animazione sprite verrà eseguita automaticamente quando il widget sprite ha ricevuto l'GX_EVENT_SHOW evento.

**GX_STYLE_SPRITE_LOOP**
  - Valore: 0x00000020
  - Descrizione: con questo stile, il widget sprite scorrerà continuamente i fotogrammi dell'animazione sprite fino a quando lo sprite non viene arrestato dall'applicazione.

__***Stili del dispositivo di scorrimento della mappa pixel:***__

**GX_STYLE_TILE_BACKGROUND**
  - Valore 0x00001000
  - Descrizione: l'immagine di sfondo del dispositivo di scorrimento viene affiancata per riempire il rettangolo di delimitazione dello sprite. In questo modo è possibile usare una piccola immagine a strisce verticali o orizzontali per riempire lo sfondo del dispositivo di scorrimento.

__***Stili aggiuntivi dell'indicatore di stato:***__

**GX_STYLE_PROGRESS_PERCENT**
  - Valore: 0x00000010
  - Descrizione: quando questo stile è impostato, l'indicatore di stato disegna il valore dell'indicatore di stato come percentuale anziché come valore non elaborato. Il testo è centrato nel rettangolo di delimitazione dell'indicatore di stato.

**GX_STYLE_PROGRESS_TEXT_DRAW**
  - Valore: 0x00000020
  - Descrizione: disegnare il valore dell'indicatore di stato corrente come testo decimale centrato all'interno dell'indicatore di stato.

**GX_STYLE_PROGRESS_VERTICAL**
  - Valore: 0x0000040
  - Descrizione: indicare che lo stato di avanzamento è orientato verticalmente. L'impostazione predefinita è l'orientamento orizzontale.

**GX_STYLE_PROGRESS_SEGMENT_FILL**:
  - **Valore**: 0x00000100
  - Descrizione: il valore dell'indicatore di stato è indicato con rettangoli riempiti segmentati, anziché con un riempimento a tinta unita.

__***Stili aggiuntivi dell'indicatore di stato radiale:***__

**GX_STYLE_RADIAL_PROGRESS_ALIAS**
  - Valore: 0x00000200
  - Descrizione: disegnare l'indicatore di stato radiale usando stili del pennello con anti-aliasing. Ciò richiede una maggiore larghezza di banda della CPU, ma produce anche un aspetto più gradevole. Per obiettivi di CPU con prestazioni inferiori, la cancellazione di questo flag di stile comporta una maggiore velocità di disegno.

**GX_STYLE_RADIAL_PROGRESS_ROUND**
  - Valore: 0x00000400
  - Descrizione: usare uno stile di pennello di fine linea rotonda quando si disegna l'arco dell'indicatore di stato radiale. Il valore predefinito è un'estremità quadrata.

__***Stili di input di testo aggiuntivi:***__

**GX_STYLE_ CURSOR_BLINK**
  - Valore: 0x00000040
  - Descrizione: il cursore del widget di input di testo lampeggia e si spegne anziché essere stabile.

**GX_STYLE_ CURSOR_ALWAYS**
  - Valore: 0x00000080
  - Descrizione Il cursore del widget di input di testo viene in genere visualizzato solo quando il widget è proprietario dello stato attivo per l'input. Questo flag di stile rende il cursore sempre visibile indipendentemente dello stato attivo per l'input.

**GX_STYLE_TEXT_INPUT_NOTIFY_ALL**
  - Valore: 0x00000100
  - Descrizione: con questo flag di stile impostare l'evento GX_EVENT_TEXT_EDITED ogni volta che il widget di input di testo riceve l'evento key down.

__***Stili di finestra aggiuntivi:***__

**GX_STYLE_TILE_WALLPAPER**
  - Valore: 0x00040000
  - Descrizione: la finestra affianca qualsiasi immagine di sfondo assegnata per riempire il rettangolo client della finestra.

**GX_STYLE_AUTO_HSCROLL**
  - Valore: 0x00100000
  - Descrizione: riservata per un uso futuro.

**GX_STYLE_AUTO_VSCROLL**
  - Valore: 0x00200000
  - Descrizione: riservata per un uso futuro.

__***Stili di menu aggiuntivi:***__

**GX_STYLE_MENU_EXPANDED**
  - Valore: 0x00000010
  - Descrizione: il widget di menu Accordion è inizialmente in stato espanso.

__***Altri stili di visualizzazione albero:***__

**GX_STYLE_TREE_VIEW_SHOW_ROOT_LINES**
  - Valore: 0x00000010
  - Descrizione: il widget visualizzazione albero deve tracciare linee dall'icona del nodo al nodo dell'albero radice.

__***Stili aggiuntivi della barra di scorrimento:***__

**GX_SCROLLBAR_BACKGROUND_TILE**
  - Valore: 0x00010000
  - Descrizione: riservata per un uso futuro.

**GX_SCROLLBAR_RELATIVE_THUMB**
  - Valore: 0x00020000
  - Descrizione: la larghezza del cursore della barra di scorrimento (per una barra di scorrimento orizzontale) o l'altezza (per una barra di scorrimento verticale) vengono calcolate in base al rapporto tra l'area visibile della finestra padre e l'intervallo minimo e massimo della barra di scorrimento.

**GX_SCROLLBAR_END_BUTTONS**
  - Valore: 0x00040000
  - Descrizione: la barra di scorrimento crea e collega automaticamente i pulsanti a ogni estremità dell'area della barra di scorrimento.

**GX_SCROLLBAR_VERTICAL** 
  - Valore: 0x01000000
  - Descrizione: la barra di scorrimento è orientata verticalmente.

**GX_SCROLLBAR_HORIZONTAL**
  - Valore: 0x02000000
  - Descrizione: la barra di scorrimento è orientata orizzontalmente.

__***Stili della rotellina di scorrimento del testo:***__

**GX_STYLE_TEXT_SCROLL_WHEEL_ROUND**
  - Valore: 0x00000200
  - Descrizione: la rotellina di scorrimento usa un algoritmo sinusoidale per fare in modo che la rotellina di scorrimento abbia una forma arrotondata. Questo flag di stile può aggiungere un sovraccarico significativo alle prestazioni del widget della rotellina di scorrimento, ma può anche dare alla rotellina un aspetto realistico 3D.