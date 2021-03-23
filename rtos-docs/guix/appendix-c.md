---
title: Appendice C-stili del widget GUIX
description: Informazioni sugli stili dei widget GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 83d5c5167739e91b7af8fce6b04213f610984fc6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823183"
---
# <a name="appendix-c---guix-widget-styles"></a>Appendice C-stili del widget GUIX

__***Stili generali (usati con la maggior parte dei tipi di widget):***__

**GX_STYLE_BORDER_NONE**
  - Valore: 0x00000000
  - Descrizione: usare questo stile per creare un widget senza bordo.

**GX_STYLE_BORDER_RAISED**
  - Valore: 0x00000001
  - Descrizione: creare un widget con un bordo in rilievo.

**GX_STYLE_BORDER_RECESSED**
  - Valore: 0x00000002
  - Descrizione: creare un widget con un bordo incassato.

**GX_STYLE_BORDER_THIN**
  - Valore: 0x00000004
  - Descrizione: creare un bordo della larghezza di un pixel.

**GX_STYLE_BORDER_THICK** 
  - Valore: 0x00000008
  - Descrizione: creare un widget con un bordo spesso.

**GX_STYLE_BORDER_MASK**
  - Valore: 0x0000000F
  - Descrizione: valore della maschera usato per testare solo i campi di stile del membro dello stile del widget.

**GX_STYLE_TRANSPARENT**
  - Valore: 0x10000000
  - Descrizione: creare un widget almeno parzialmente trasparente. Questo stile deve essere usato quando un widget non disegna se stesso completamente opaco, inclusi i widget che disegnano una Pixelmap semi-trasparente come sfondo del widget. Questo flag di stile informa GUIX che è necessario disegnare l'elemento padre del widget per aggiornare l'area di sfondo del widget.

**GX_STYLE_DRAW_SELECTED**
  - Valore: 0x20000000
  - Descrizione: specificare che il widget deve essere disegnato usando i colori e i tipi di carattere selezionati per lo stato. Tipi di widget diversi usano lo stile DRAW_SELECTED in modi diversi per indicare che il widget è attualmente selezionato.

**GX_STYLE_ENABLED**
  - Valore: 0x40000000
  - Descrizione: contrassegnare il widget come abilitato, in modo che il widget accetti gli eventi di input dell'utente e generi i segnali di output.
  
**GX_STYLE_DYNAMICALLY_ALLOCATED**
  - Valore: 0x80000000
  - Descrizione: indica che la memoria del blocco di controllo widget viene allocata in modo dinamico usando il servizio gx_system_memory_allocator quando viene creato il widget e la memoria del blocco di controllo viene liberata se il widget viene eliminato definitivamente.

**GX_STYLE_USE_LOCAL_ALPHA**
  - Valore: 0x01000000
  - Descrizione: indica alle funzioni di disegno GUIX di usare il valore alfa del widget locale durante il disegno del widget. Questo flag viene in genere usato dalla logica GUIX interna per implementare animazioni di dissolvenza dei widget.


__***Stili di allineamento del testo (stili applicati a tutti i widget che consentono di disegnare testo):***__

**GX_STYLE_TEXT_LEFT**
  - Valore: 0x00001000
  - Descrizione: il testo viene disegnato allineato a sinistra all'interno dell'area client del widget.

**GX_STYLE_TEXT_RIGHT** 
  - Valore: 0x00002000
  - Descrizione: il testo viene tracciato allineato a destra nell'area client del widget.

**GX_STYLE_TEXT_CENTER**
  - Valore: 0x00004000
  - Descrizione: il testo viene disegnato allineato al centro all'interno dell'area client del widget.

**GX_STYLE_TEXT_COPY**
  - Valore: 0x00008000
  - Descrizione: per impostazione predefinita, i widget che tracciano testo mantengono solo un puntatore al testo passato dall'applicazione. Per il testo definito in modo statico definito all'interno della tabella di stringhe, non c'è motivo per il widget di creare una copia privata del testo assegnato. Tuttavia, se il testo assegnato a un widget viene creato dinamicamente usando funzioni come Sprint () o gx_utility_ltoa, è spesso utile indicare al widget di mantenerne la copia privata di qualsiasi testo assegnato. Questo consente all'applicazione di usare variabili automatiche o temporanee quando si definisce la stringa di testo, quando l'applicazione sarebbe altrimenti necessaria per definire matrici di caratteri definite in modo statico per ogni widget di testo che usa testo definito in modo dinamico. Quando viene impostato questo flag di stile, il widget utilizzerà la funzione gx_system_memory_allocator per allocare in modo dinamico il blocco di memoria necessario per conservare una copia privata della stringa assegnata. Pertanto, l'utilizzo di questo flag di stile è predicato nell'applicazione che definisce le funzioni memory_allocator e memory_deallocator. GX_STYLE_TEXT_COPY non devono essere cancellate dopo che è stata impostata e questa operazione causerà risultati imprevedibili.

__***Stili del pulsante (si applica solo ai tipi di widget del pulsante GUIX):***__

**GX_STYLE_BUTTON_PUSHED**
  - Valore 0x00000010
  - Descrizione: indica che il pulsante si trova nello stato premuto o selezionato.

**GX_STYLE_BUTTON_TOGGLE**
  - Valore 0x00000020
  - Descrizione: il pulsante commuta lo stato tra push e unpushd a ogni evento click. Questo stile viene comunemente usato con i pulsanti di stile "checkbox".

**GX_STYLE_BUTTON_RADIO**
  - Valore 0x00000040
  - Descrizione: questo stile indica che il pulsante sarà esclusivo e deselezionando gli elementi di pari livello dei pulsanti quando vengono selezionati. Questo stile viene comunemente usato con i pulsanti di stile "pulsante di opzione".

**GX_STYLE_BUTTON_EVENT_ON_PUSH**
  - Valore: 0x00000080
  - Descrizione: indica che il pulsante genera un evento Click quando inizialmente viene eseguito il push. L'operazione predefinita prevede la generazione di un evento Click quando si rilascia il pulsante.

**GX_STYLE_BUTTON_REPEAT**
  - Valore 0x00000100
  - Descrizione: indica che il pulsante deve inviare eventi Click ripetuti al padre del pulsante quando il pulsante è premuto nello stato push.

__***Stili elenco (si applica solo ai tipi di widget Elenco GUIX):***__

**GX_STYLE_CENTER_SELECTED** 
  - Valore: 0x00000010
  - Descrizione: riservata

**GX_STYLE_WRAP**
  - Valore 0x00000020
  - Descrizione: l'elenco di elementi figlio viene eseguito a capo dall'inizio alla fine quando l'elenco viene trascinato o spostato oltre l'indice dell'elenco iniziale o finale.

**GX_STYLE_FLICKABLE**
  - Valore: 0x00000040
  - Descrizione: riservata

__***Stili del pulsante di Pixelmap e dell'icona:***__

**GX_STYLE_HALIGN_CENTER**
  - Valore: 0x00010000
  - Descrizione: il pulsante Pixelmap deve essere allineato al centro all'interno del bordo del pulsante sull'asse orizzontale.

**GX_STYLE_HALIGN_LEFT**
  - Valore: 0x00020000
  - Descrizione: il pulsante Pixelmap deve essere allineato all'interno del bordo del pulsante sull'asse orizzontale.

**GX_STYLE_HALIGN_RIGHT**
  - Valore 0x00040000
  - Descrizione: il pulsante Pixelmap deve essere allineato a destra all'interno del bordo del pulsante sull'asse orizzontale.

**GX_STYLE_VALIGN_CENTER**
  - Valore 0x00080000
  - Descrizione: il pulsante Pixelmap deve essere allineato al centro all'interno del bordo del pulsante sull'asse verticale.

**GX_STYLE_VALIGN_TOP**
  - Valore: 0x00100000
  - Descrizione: il pulsante Pixelmap deve essere allineato in alto all'interno del bordo del pulsante sull'asse verticale.

**GX_STYLE_VALIGN_BOTTOM**
  - Valore: 0x00200000
  - Descrizione: il pulsante Pixelmap deve essere allineato in basso all'interno del bordo del pulsante sull'asse orizzontale verticale.

__***Stili del dispositivo di scorrimento (Appy solo per GX_SLIDER e i tipi di widget derivati):***__

**GX_STYLE_SHOW_NEEDLE**
  - Valore: 0x00000200
  - Descrizione: questo stile deve essere incluso affinché il dispositivo di scorrimento disegni l'indicatore della lancetta. Questo stile può essere disabilitato se l'applicazione vuole disabilitare l'ago del dispositivo di scorrimento o creare un indicatore lancetta personalizzato.

**GX_STYLE_SHOW_TICKMARKS**
  - Valore: 0x00000400
  - Descrizione: il widget del dispositivo di scorrimento eseguirà il disegno del software di linee TickMark tratteggiate quando lo stile è abilitato.

**GX_STYLE_SLIDER_VERTICAL**
  - Valore 0x00000800
  - Descrizione: impostare questo flag di stile per creare un dispositivo di scorrimento verticale e deselezionare questo flag di stile per creare un dispositivo di scorrimento orizzontale.

__***Stili sprite (si applica solo ai tipi di widget GX_SPRITE):***__

**GX_STYLE_SPRITE_AUTO**
  - Valore: 0x00000010
  - Descrizione: indica che l'animazione sprite verrà eseguita automaticamente quando il widget sprite riceve l'evento GX_EVENT_SHOW.

**GX_STYLE_SPRITE_LOOP**
  - Valore: 0x00000020
  - Descrizione: con questo stile, il widget sprite continuerà a scorrere continuamente i frame di animazione sprite fino a quando lo sprite non verrà interrotto dall'applicazione.

__***Stili del dispositivo di scorrimento Pixelmap:***__

**GX_STYLE_TILE_BACKGROUND**
  - Valore 0x00001000
  - Descrizione: per riempire il rettangolo di delimitazione dello sprite, viene affiancata l'immagine di sfondo del dispositivo di scorrimento. In questo modo, è possibile usare una piccola immagine a striscia verticale o orizzontale per riempire lo sfondo del dispositivo di scorrimento.

__***Stili aggiuntivi dell'indicatore di stato:***__

**GX_STYLE_PROGRESS_PERCENT**
  - Valore: 0x00000010
  - Descrizione: quando questo stile è impostato, l'indicatore di stato disegna il valore della barra come percentuale anziché come valore non elaborato. Il testo viene centrato nel rettangolo di delimitazione della barra di avanzamento.

**GX_STYLE_PROGRESS_TEXT_DRAW**
  - Valore: 0x00000020
  - Descrizione: creare il valore indicatore di stato corrente come testo decimale centrato all'interno dell'indicatore di stato.

**GX_STYLE_PROGRESS_VERTICAL**
  - Valore: 0x0000040
  - Descrizione: indicare che lo stato di avanzamento è orientato verticalmente. Il valore predefinito è orientamento orizzontale.

**GX_STYLE_PROGRESS_SEGMENT_FILL**:
  - **Valore**: 0x00000100
  - Descrizione: il valore dell'indicatore di stato è indicato con rettangoli riempiti segmentati, anziché come riempimento a tinta unita.

__***Stili aggiuntivi indicatore di stato radiali:***__

**GX_STYLE_RADIAL_PROGRESS_ALIAS**
  - Valore: 0x00000200
  - Descrizione: disegnare la barra di stato radiale usando gli stili di pennello anti-aliasing. Questa operazione richiede una maggiore larghezza di banda della CPU, ma produce anche un aspetto più gradevole. Per gli obiettivi di CPU con prestazioni inferiori, la cancellazione di questo flag di stile comporterà una maggiore velocità di disegno.

**GX_STYLE_RADIAL_PROGRESS_ROUND**
  - Valore: 0x00000400
  - Descrizione: usare uno stile di pennello finale della linea rotonda quando si disegna l'arco dell'indicatore di stato radiale. Il valore predefinito è una fine della riga quadrata.

__***Stili di input di testo aggiuntivi:***__

**GX_STYLE_ CURSOR_BLINK**
  - Valore: 0x00000040
  - Descrizione: il cursore del widget input di testo lampeggerà e non verrà più stazionario.

**GX_STYLE_ CURSOR_ALWAYS**
  - Valore: 0x00000080
  - Descrizione Il cursore del widget input di testo viene in genere visualizzato solo quando il widget possiede lo stato attivo per l'input. Questo flag di stile renderà il cursore sempre visibile indipendentemente dallo stato attivo per l'input.

**GX_STYLE_TEXT_INPUT_NOTIFY_ALL**
  - Valore: 0x00000100
  - Descrizione: con questo flag di stile impostare l'evento GX_EVENT_TEXT_EDITED ogni volta che viene ricevuto un evento di chiave inattiva dal widget input di testo.

__***Stili di finestra aggiuntivi:***__

**GX_STYLE_TILE_WALLPAPER**
  - Valore: 0x00040000
  - Descrizione: nella finestra viene affiancata un'immagine di sfondo assegnata per riempire il rettangolo client della finestra.

**GX_STYLE_AUTO_HSCROLL**
  - Valore: 0x00100000
  - Descrizione: riservata per un utilizzo futuro.

**GX_STYLE_AUTO_VSCROLL**
  - Valore: 0x00200000
  - Descrizione: riservata per un utilizzo futuro.

__***Stili di menu aggiuntivi:***__

**GX_STYLE_MENU_EXPANDED**
  - Valore: 0x00000010
  - Descrizione: il widget del menu Accordion è inizialmente in stato espanso.

__***Stili di visualizzazione ad albero aggiuntivi:***__

**GX_STYLE_TREE_VIEW_SHOW_ROOT_LINES**
  - Valore: 0x00000010
  - Descrizione: il widget visualizzazione albero deve creare righe dall'icona del nodo al nodo radice della struttura ad albero.

__***Stili aggiuntivi della barra di scorrimento:***__

**GX_SCROLLBAR_BACKGROUND_TILE**
  - Valore: 0x00010000
  - Descrizione: riservata per un utilizzo futuro.

**GX_SCROLLBAR_RELATIVE_THUMB**
  - Valore: 0x00020000
  - Descrizione: la larghezza del cursore della barra di scorrimento (per una barra di scorrimento orizzontale) o l'altezza (per una barra di scorrimento verticale) vengono calcolate in base al rapporto tra l'area visibile della finestra padre e l'intervallo minimo e massimo della barra di scorrimento.

**GX_SCROLLBAR_END_BUTTONS**
  - Valore: 0x00040000
  - Descrizione: la barra di scorrimento Crea e connette automaticamente i pulsanti a ogni estremità dell'area della barra di scorrimento.

**GX_SCROLLBAR_VERTICAL** 
  - Valore: 0x01000000
  - Descrizione: la barra di scorrimento è orientata verticalmente.

**GX_SCROLLBAR_HORIZONTAL**
  - Valore: 0x02000000
  - Descrizione: la barra di scorrimento è orientata orizzontalmente.

__***Stili rotellina di scorrimento testo:***__

**GX_STYLE_TEXT_SCROLL_WHEEL_ROUND**
  - Valore: 0x00000200
  - Descrizione: la rotellina di scorrimento usa un algoritmo sinusoidale per fare in modo che la rotellina di scorrimento appaia con una forma arrotondata. Questo flag di stile può comportare un sovraccarico significativo per le prestazioni del widget della rotellina di scorrimento, ma anche un aspetto realistico 3D.