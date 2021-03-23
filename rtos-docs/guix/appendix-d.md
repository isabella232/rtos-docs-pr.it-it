---
title: Appendice D-GUIX pennello, Canvas e gradiente attributi
description: Informazioni sugli attributi pennello, Canvas e sfumatura GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 19c0687a54be244ae395124664b4b6da0f4e90b6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823180"
---
# <a name="appendix-d---guix-brush-canvas-and-gradient-attributes"></a>Appendice D-GUIX pennello, Canvas e gradiente attributi

__**Stili pennello:**__

**GX_BRUSH_OUTLINE**
- Valore: 0x0000
- Descrizione: questo stile del pennello si applica alle funzioni di disegno delle forme, ad esempio gx_canvas_rectangle_draw o gx_canvas_polygon_draw. Questo stile indica che la forma deve essere delineata, oltre a un riempimento facoltativo. Se lo stile del GX_BRUSH_OUTLINE è impostato e la GX_BRSUH_SOLID_FILL è deselezionata, la forma viene configurata solo con la delineatura.

**GX_BRUSH_SOLID_FILL**
- Valore: 0x0001
- Descrizione: questo stile del pennello si applica alle funzioni di disegno di forme e indica che la forma richiesta deve essere riempita con un colore a tinta unita utilizzando il colore di riempimento del pennello corrente.

**GX_BRUSH_PIXELMAP_FILL**
- Valore: 0x0002
- Descrizione: questo stile del pennello si applica alle funzioni di disegno di forme e indica che la forma richiesta deve essere un modello riempito con l'Pixelmap del pennello corrente.

**GX_BRUSH_ALIAS**
- Valore: 0x0004
- Descrizione: questo stile del pennello si applica a tutti i profili di disegno e di forma delle linee. Se questo flag è impostato, le linee e le strutture vengono disegnate con il più accurato, ma anche più tempo per l'utilizzo di algoritmi di disegno anti-aliasing. Questo flag di stile viene usato solo per le profondità di colore a 16 BPP e superiori.

**GX_BRUSH_UNDERLINE**
- Valore: 0x0008
- Descrizione: questo flag si applica al disegno del testo e indica che il testo successivo disegnato deve essere sottolineato.

**GX_BRUSH_ROUND**
- Valore: 0x0010
- Descrizione: questo flag si applica al disegno della linea e indica che le estremità della riga vengono disegnate con una forma circolare o circolare, anziché la forma quadrata predefinita.

__**Flag Canvas:**__

**GX_CANVAS_SIMPLE**
- Valore: 0x01
- Descrizione: un'area di disegno della memoria usata per il disegno fuori schermo.

**GX_CANVAS_MANAGED**
- Valore: 0x02
- Descrizione: un'area di disegno che è stata scaricata automaticamente nella visualizzazione attiva, come parte del processo di compilazione composito o come parte dell'operazione di attivazione/disattivazione del buffer per le architetture con singolo Canvas.

**GX_CANVAS_VISIBLE**
- Valore: 0x04
- Descrizione: questo flag può essere usato per attivare e disattivare un'area di disegno, senza perdere il contenuto del disegno dell'area di disegno.

**GX_CANVAS_MODIFIED**
- Valore: 0x08
- Descrizione: riservata per un utilizzo futuro.

**GX_CANVAS_COMPOSITE**
- Valore: 0x20
- Descrizione: questo flag viene usato dall'applicazione quando si configura un sistema con più Canvas che comporterà più Canvas gestite nell'area di disegno composita e il composito è il driven per il buffer del frame hardware.

__**Tipi di sfumatura:**__

**GX_GRADIENT_TYPE_VERTICAL**
- Valore: 0x01
- Descrizione: crea una sfumatura AlphaMap verticale.

**GX_GRADIENT_TYPE_ALPHA**
- Valore: 0x02
- Descrizione: crea una sfumatura di stile della mappa alfa. Si tratta attualmente dell'unico stile di sfumatura supportato.

**GX_GRADIENT_TYPE_MIRROR**
- Valore: 0x04
- Descrizione: questo flag indica che la sfumatura deve raggiungere il picco al centro dell'intervallo di larghezza/altezza e tornare al valore iniziale mentre raggiunge il bordo destro/inferiore. Senza questo flag di stile, la sfumatura sarà una sfumatura lineare dall'alto verso il basso o da sinistra a destra, a seconda del flag di GX_GRADIENT_TYPE_VERTICAL.