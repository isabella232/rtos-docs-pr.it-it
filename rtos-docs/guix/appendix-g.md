---
title: Appendice G - Struttura dei caratteri GUIX
description: Informazioni sulla struttura dei caratteri GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 4c7cedb49268f97f8e1fc4cd28329b0b61e697d57562865896f0502bdd1d45f1
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784190"
---
# <a name="appendix-g---guix-font-structure"></a>Appendice G - Struttura dei caratteri GUIX

I tipi di carattere GUIX vengono in genere prodotti dall'applicazione GUIX Studio e i glifi dei tipi di carattere vengono sottoposti a rendering dal driver di visualizzazione GUIX. Il software dell'applicazione deve specificare solo il tipo di carattere e i colori che ogni widget di visualizzazione del testo deve usare. Le strutture di dati dei tipi di carattere GUIX sono documentate qui per completezza e per consentire agli sviluppatori di creare metodi personalizzati per la generazione o la conversione di altri tipi di carattere nel formato di carattere GUIX.

Ogni carattere GUIX inizia con una GX_FONT grafica. La GX_FONT definisce parametri di carattere globali, ad esempio il carattere incluso nel tipo di carattere e l'altezza della riga del tipo di carattere. La GX_FONT punta a una matrice di GX_GLYPH struttura. Ogni GX_GLYPH struttura definisce la larghezza, l'altezza e l'offset della linea di base di un glifo di carattere specifico. La GX_GLYPH struttura punta anche ai dati bitmap effettivi del glifo (che possono essere NULL per gli spazi vuoti).

La GX_FONT, contenuta in gx_api.h, viene dichiarata come segue:

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

Il gx_font_format definisce i bit per pixel del tipo di carattere e altri flag, come definito nel file di intestazione gx_api.h.

Il gx_font_prespace definisce lo spazio in pixel da ignorare sopra ogni riga di testo in una visualizzazione di testo su più righe.

Il gx_font_postspace campo definisce lo spazio in pixel da ignorare sotto ogni riga di testo in una visualizzazione di testo su più righe.

Il gx_font_line_height campo definisce l'altezza del glifo più alto nel tipo di carattere.

Il gx_font_baseline campo definisce la distanza, in pixel, dalla riga superiore dei pixel del glifo alla linea di base del tipo di carattere.

Il gx_font_first_glyph definisce la prima codifica dei caratteri Unicode inclusa in questa pagina del tipo di carattere.

Il gx_font_last_glyph definisce l'ultima codifica dei caratteri Unicode inclusa in questa pagina del tipo di carattere.

Il gx_font_glyphs punta a una matrice di GX_GLYPH struttura. Questa matrice deve avere dimensioni uguali al numero di caratteri contenuti in questa pagina del tipo di carattere, ad esempio (gx_font_last_glyph - gx_font_first_glyph) + 1.

Il gx_font_next_page membro viene usato per più tipi di carattere di pagina. Più tipi di carattere di pagina vengono usati per i set di caratteri estesi e per ottimizzare le dimensioni GX_GLYPH matrici di strutture. Se tutti i caratteri del tipo di carattere sono contenuti in una pagina del tipo di carattere o se si tratta dell'ultima pagina del tipo di carattere in questione, il membro gx_font_next_page viene impostato su GX_NULL.

Come indicato in precedenza, la GX_FONT precedente contiene un puntatore a una matrice di GX_GLYPHS strutture. Deve essere presente una GX_GLYPH struttura per ogni carattere nella pagina del tipo di carattere. La GX_GLYPH struttura è definita come:

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

Il gx_glyph_map punta alla bitmap del glifo. Questo puntatore può essere GX_NULL per gli spazi vuoti. I dati bitmap vengono codificati come valori alfa 1 bpp, 2 bpp, 4 bpp o 8 bpp. Per i dati a 1 bit, il valore 1 indica che il pixel deve essere scritto nel colore di primo piano e il valore 0 indica che il pixel è trasparente. Per i dati a 8 bit, i valori vanno da 0 (completamente trasparente) a 255 (completamente opaco). Tutti i valori intermedi rappresentano un valore di fusione per i tipi di carattere con antialiasing. I dati bitmap del glifo vengono sempre riempiti per l'allineamento completo dei byte per i formati che usano valori di dati inferiori a 8bpp.

I gx_glyph_ascent e gx_glyph_descent posizione verticale del glifo rispetto alla linea di base del tipo di carattere.

I gx_glyph_width e gx_glyph_height valori specificano le dimensioni dei dati bitmap del glifo.

Il gx_glyph_advance valore specifica la larghezza in pixel per far avanzare la posizione di disegno dopo il disegno del glifo (potrebbe non essere uguale alla larghezza del glifo).

Il gx_glyph_leading valore specifica i pixel da avanzare nella direzione x prima di eseguire il rendering del glifo.