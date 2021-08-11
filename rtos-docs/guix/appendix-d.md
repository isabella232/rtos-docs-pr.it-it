---
title: Appendice D - Pennello GUIX, canvas e attributi sfumatura
description: Informazioni sugli attributi del pennello GUIX, dell'area di disegno e della sfumatura.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 9fbc98f1094cab6be4bc0826fef7c0feb77b50b066b22342cd52404bd85ff98e
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784632"
---
# <a name="appendix-d---guix-brush-canvas-and-gradient-attributes"></a>Appendice D - Pennello GUIX, canvas e attributi sfumatura

__**Stili del pennello:**__

**GX_BRUSH_OUTLINE**
- Valore: 0x0000
- Descrizione: questo stile del pennello si applica alle funzioni di disegno delle forme, ad esempio gx_canvas_rectangle_draw o gx_canvas_polygon_draw. Questo stile indica che la forma deve essere delineata, oltre a essere facoltativamente riempita. Se lo GX_BRUSH_OUTLINE è impostato e la GX_BRSUH_SOLID_FILL è deselezionata, la forma viene solo delineata.

**GX_BRUSH_SOLID_FILL**
- Valore: 0x0001
- Descrizione: questo stile di pennello si applica alle funzioni di disegno delle forme e indica che la forma richiesta deve essere riempita con un colore a tinta unita usando il colore di riempimento del pennello corrente.

**GX_BRUSH_PIXELMAP_FILL**
- Valore: 0x0002
- Descrizione: questo stile del pennello si applica alle funzioni di disegno della forma e indica che la forma richiesta deve essere riempita con la mappa pixel del pennello corrente.

**GX_BRUSH_ALIAS**
- Valore: 0x0004
- Descrizione: questo stile di pennello si applica a tutti i contorni di disegno di linee e forme. Se questo flag è impostato, le linee e i contorni vengono tracciati con gli algoritmi di disegno anti-aliasing più accurati ma anche più lunghi. Questo flag di stile viene usato solo per profondità di colore a 16 bpp e superiori.

**GX_BRUSH_UNDERLINE**
- Valore: 0x0008
- Descrizione: questo flag si applica al disegno di testo e indica che il testo disegnato successivamente deve essere sottolineato.

**GX_BRUSH_ROUND**
- Valore: 0x0010
- Descrizione: questo flag si applica al disegno di linee e indica che le estremità delle linee vengono disegnate con una forma rotonda o circolare, anziché con la forma quadrata predefinita.

__**Flag canvas:**__

**GX_CANVAS_SIMPLE**
- Valore: 0x01
- Descrizione: area di disegno della memoria usata per il disegno fuori schermo.

**GX_CANVAS_MANAGED**
- Valore: 0x02
- Descrizione: area di disegno che viene scaricata automaticamente nella visualizzazione attiva, nell'ambito del processo di compilazione composito o come parte dell'operazione di attivazione/disattivazione del buffer per le architetture a canvas singolo.

**GX_CANVAS_VISIBLE**
- Valore: 0x04
- Descrizione: questo flag può essere usato per attivare e disattivare un'area di disegno, senza perdere il contenuto del disegno dell'area di disegno.

**GX_CANVAS_MODIFIED**
- Valore: 0x08
- Descrizione: riservata per un uso futuro.

**GX_CANVAS_COMPOSITE**
- Valore: 0x20
- Descrizione: questo flag viene usato dall'applicazione quando si configura un sistema con più canvas che compose più canvas gestite nell'area di disegno composita e il composito è guidato dal buffer dei frame hardware.

__**Tipi di sfumatura:**__

**GX_GRADIENT_TYPE_VERTICAL**
- Valore: 0x01
- Descrizione: crea una sfumatura alfamap verticale.

**GX_GRADIENT_TYPE_ALPHA**
- Valore: 0x02
- Descrizione: crea una sfumatura di stile mappa alfa. Questo è attualmente l'unico stile di sfumatura supportato.

**GX_GRADIENT_TYPE_MIRROR**
- Valore: 0x04
- Descrizione: questo flag indica che la sfumatura deve raggiungere il picco al centro dell'intervallo larghezza/altezza e tornare al valore iniziale quando raggiunge il bordo destro/inferiore. Senza questo flag di stile, la sfumatura sarà una sfumatura lineare dall'alto verso il basso o da sinistra a destra, a seconda del flag GX_GRADIENT_TYPE_VERTICAL corrente.