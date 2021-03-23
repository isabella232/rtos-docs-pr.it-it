---
title: Struttura del tipo di carattere Appendice G-GUIX
description: Informazioni sulla struttura del tipo di carattere GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: b5f0232e6c21851014b85cfe7b07795062fd1e8d
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823171"
---
# <a name="appendix-g---guix-font-structure"></a>Struttura del tipo di carattere Appendice G-GUIX

I tipi di carattere GUIX vengono normalmente prodotti dall'applicazione GUIX studio e il rendering dei glifi del tipo di carattere viene eseguito dal driver di visualizzazione GUIX. Il software dell'applicazione deve specificare solo il tipo di carattere e i colori che ciascun widget di visualizzazione del testo deve usare. Le strutture di dati del tipo di carattere GUIX sono documentate qui per completezza e consentono agli sviluppatori di creare metodi personalizzati per la generazione o la conversione di altri tipi di carattere nel formato carattere GUIX.

Ogni tipo di carattere GUIX inizia con una struttura GX_FONT. La struttura GX_FONT definisce i parametri del tipo di carattere globali, ad esempio il carattere incluso all'interno del tipo di carattere e l'altezza della riga del tipo di carattere. La struttura GX_FONT punta a una matrice di strutture di GX_GLYPH. Ogni struttura GX_GLYPH definisce la larghezza, l'altezza e l'offset della linea di base di un glifo di caratteri specifico. La struttura di GX_GLYPH punta anche ai dati di bitmap del glifo effettivi (che possono essere NULL per i caratteri vuoti).

La struttura di GX_FONT, contenuta in gx_api. h, viene dichiarata come segue:

```c
typedef struct GX_FONT_STRUCT
{
    GX_UBYTE                     gx_font_format
    GX_UBYTE                     gx_font_prespace
    GX_UBYTE                     gx_font_postspace
    GX_UBYTE                     gx_font_line_height 
    GX_UBYTE                     gx_font_baseline
    USHORT                       gx_font_first_glyph
    USHORT                       gx_font_last_glyph 
    GX_CONST GX_GLYPH           *gx_font_glyphs
    const struct GX_FONT_STRUCT *gx_font_next_page
} GX_FONT;
```

Il campo gx_font_format definisce il carattere bit per pixel e altri flag, come definito nel file di intestazione gx_api. h.

Il gx_font_prespace definisce lo spazio pixel da ignorare sopra ogni riga di testo in una visualizzazione di testo su più righe.

Il campo gx_font_postspace definisce lo spazio pixel da ignorare sotto ogni riga di testo in una visualizzazione di testo su più righe.

Il campo gx_font_line_height definisce l'altezza del glifo più alto nel tipo di carattere.

Il campo gx_font_baseline definisce la distanza, in pixel, tra la riga superiore dei pixel del glifo e la linea di base del tipo di carattere.

Il campo gx_font_first_glyph definisce la prima codifica dei caratteri Unicode inclusa in questa pagina dei tipi di carattere.

Il campo gx_font_last_glyph definisce l'ultima codifica dei caratteri Unicode inclusa in questa pagina del tipo di carattere.

Il puntatore gx_font_glyphs punta a una matrice di strutture di GX_GLYPH. La dimensione della matrice deve essere uguale al numero di caratteri contenuti in questa pagina dei tipi di carattere, ad esempio (gx_font_last_glyph – gx_font_first_glyph) + 1.

Il membro gx_font_next_page viene usato per i tipi di carattere a più pagine. Per i set di caratteri estesi vengono usati più tipi di carattere della pagina e per ottimizzare le dimensioni delle matrici di struttura GX_GLYPH. Se tutti i caratteri del tipo di carattere sono contenuti all'interno di una pagina del tipo di carattere o se si tratta dell'ultima pagina del tipo di carattere in questione, il gx_font_next_page membro viene impostato su GX_NULL.

Come indicato in precedenza, la GX_FONT struttura precedente contiene un puntatore a una matrice di strutture di GX_GLYPHS. Per ogni carattere della pagina del tipo di carattere deve essere presente una struttura GX_GLYPH. La struttura GX_GLYPH è definita come segue:

```c
typedef struct GX_GLYPH_STRUCT
{
    GX_CONST GX_UBYTE *gx_glyph_map;
    GX_BYTE            gx_glyph_ascent;
    GX_BYTE            gx_glyph_descent;
    GX_BYTE            gx_glyph_advance;
    GX_BYTE            gx_glyph_leading;
    GX_UBYTE           gx_glyph_width;
    GX_UBYTE           gx_glyph_height;
} GX_GLYPH;
```

Il puntatore gx_glyph_map punta alla bitmap dell'icona. Questo puntatore può essere GX_NULL per gli spazi vuoti. I dati bitmap sono codificati come valori alfa 1 BPP, 2 BPP, 4 BPP o 8 BPP. Per i dati a 1 bit, il valore 1 indica che il pixel deve essere scritto nel colore di primo piano e il valore 0 indica che il pixel è trasparente. Per i dati a 8 bit, i valori variano da 0 (completamente trasparente) a 255 (completamente opaca). Tutto il valore intermedio rappresenta un valore di fusione per i tipi di carattere anti-aliasing. I dati bitmap del glifo vengono sempre riempiti con l'allineamento a byte completo per i formati che usano valori di dati inferiori a 8bpp.

I valori gx_glyph_ascent e gx_glyph_descent posizionano verticalmente il glifo rispetto alla linea di base del tipo di carattere.

I valori gx_glyph_width e gx_glyph_height specificano le dimensioni dei dati bitmap del glifo.

Il valore gx_glyph_advance specifica la larghezza in pixel per far avanzare la posizione di disegno dopo aver disegnato il glifo (potrebbe non essere uguale alla larghezza del glifo).

Il valore gx_glyph_leading specifica i pixel da avanzare nella direzione x prima di eseguire il rendering del glifo.