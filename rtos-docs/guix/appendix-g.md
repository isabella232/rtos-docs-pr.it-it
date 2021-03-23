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
# <a name="appendix-g---guix-font-structure"></a><span data-ttu-id="ba815-103">Struttura del tipo di carattere Appendice G-GUIX</span><span class="sxs-lookup"><span data-stu-id="ba815-103">Appendix G - GUIX Font Structure</span></span>

<span data-ttu-id="ba815-104">I tipi di carattere GUIX vengono normalmente prodotti dall'applicazione GUIX studio e il rendering dei glifi del tipo di carattere viene eseguito dal driver di visualizzazione GUIX.</span><span class="sxs-lookup"><span data-stu-id="ba815-104">GUIX fonts are normally produced by the GUIX Studio application, and font glyphs are rendered by the GUIX display driver.</span></span> <span data-ttu-id="ba815-105">Il software dell'applicazione deve specificare solo il tipo di carattere e i colori che ciascun widget di visualizzazione del testo deve usare.</span><span class="sxs-lookup"><span data-stu-id="ba815-105">The application software need only specify the font and colors that each text display widget should use.</span></span> <span data-ttu-id="ba815-106">Le strutture di dati del tipo di carattere GUIX sono documentate qui per completezza e consentono agli sviluppatori di creare metodi personalizzati per la generazione o la conversione di altri tipi di carattere nel formato carattere GUIX.</span><span class="sxs-lookup"><span data-stu-id="ba815-106">The GUIX font data structures are documented here for completeness, and to enable developers to create their own methods for generating or converting other fonts into the GUIX font format.</span></span>

<span data-ttu-id="ba815-107">Ogni tipo di carattere GUIX inizia con una struttura GX_FONT.</span><span class="sxs-lookup"><span data-stu-id="ba815-107">Each GUIX font starts with a GX_FONT structure.</span></span> <span data-ttu-id="ba815-108">La struttura GX_FONT definisce i parametri del tipo di carattere globali, ad esempio il carattere incluso all'interno del tipo di carattere e l'altezza della riga del tipo di carattere.</span><span class="sxs-lookup"><span data-stu-id="ba815-108">The GX_FONT structure defines global font parameters, such as the character included within the font and the line height of the font.</span></span> <span data-ttu-id="ba815-109">La struttura GX_FONT punta a una matrice di strutture di GX_GLYPH.</span><span class="sxs-lookup"><span data-stu-id="ba815-109">The GX_FONT structure points at an array of GX_GLYPH structures.</span></span> <span data-ttu-id="ba815-110">Ogni struttura GX_GLYPH definisce la larghezza, l'altezza e l'offset della linea di base di un glifo di caratteri specifico.</span><span class="sxs-lookup"><span data-stu-id="ba815-110">Each GX_GLYPH structure defines the width, height, and baseline offset of one specific character glyph.</span></span> <span data-ttu-id="ba815-111">La struttura di GX_GLYPH punta anche ai dati di bitmap del glifo effettivi (che possono essere NULL per i caratteri vuoti).</span><span class="sxs-lookup"><span data-stu-id="ba815-111">The GX_GLYPH structure also points to the actual glyph bitmap data (which may be NULL for whitespace characters).</span></span>

<span data-ttu-id="ba815-112">La struttura di GX_FONT, contenuta in gx_api. h, viene dichiarata come segue:</span><span class="sxs-lookup"><span data-stu-id="ba815-112">The GX_FONT structure, contained in gx_api.h, is declared as follows:</span></span>

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

<span data-ttu-id="ba815-113">Il campo gx_font_format definisce il carattere bit per pixel e altri flag, come definito nel file di intestazione gx_api. h.</span><span class="sxs-lookup"><span data-stu-id="ba815-113">The gx_font_format field defines the font bits-per-pixel and other flags, as defined in the gx_api.h header file.</span></span>

<span data-ttu-id="ba815-114">Il gx_font_prespace definisce lo spazio pixel da ignorare sopra ogni riga di testo in una visualizzazione di testo su più righe.</span><span class="sxs-lookup"><span data-stu-id="ba815-114">The gx_font_prespace defines the pixel space to skip above each line of text in a multi-line text display.</span></span>

<span data-ttu-id="ba815-115">Il campo gx_font_postspace definisce lo spazio pixel da ignorare sotto ogni riga di testo in una visualizzazione di testo su più righe.</span><span class="sxs-lookup"><span data-stu-id="ba815-115">The gx_font_postspace field defines the pixel space to skip below each line of text in a multi-line text display.</span></span>

<span data-ttu-id="ba815-116">Il campo gx_font_line_height definisce l'altezza del glifo più alto nel tipo di carattere.</span><span class="sxs-lookup"><span data-stu-id="ba815-116">The gx_font_line_height field defines the height of the tallest glyph in the font.</span></span>

<span data-ttu-id="ba815-117">Il campo gx_font_baseline definisce la distanza, in pixel, tra la riga superiore dei pixel del glifo e la linea di base del tipo di carattere.</span><span class="sxs-lookup"><span data-stu-id="ba815-117">The gx_font_baseline field defines the distance, in pixels, from the top row of glyph pixels to the font baseline.</span></span>

<span data-ttu-id="ba815-118">Il campo gx_font_first_glyph definisce la prima codifica dei caratteri Unicode inclusa in questa pagina dei tipi di carattere.</span><span class="sxs-lookup"><span data-stu-id="ba815-118">The gx_font_first_glyph field defines the first Unicode character encoding included in this font page.</span></span>

<span data-ttu-id="ba815-119">Il campo gx_font_last_glyph definisce l'ultima codifica dei caratteri Unicode inclusa in questa pagina del tipo di carattere.</span><span class="sxs-lookup"><span data-stu-id="ba815-119">The gx_font_last_glyph field defines the last Unicode character encoding included in this font page.</span></span>

<span data-ttu-id="ba815-120">Il puntatore gx_font_glyphs punta a una matrice di strutture di GX_GLYPH.</span><span class="sxs-lookup"><span data-stu-id="ba815-120">The gx_font_glyphs pointer points to an array of GX_GLYPH structures.</span></span> <span data-ttu-id="ba815-121">La dimensione della matrice deve essere uguale al numero di caratteri contenuti in questa pagina dei tipi di carattere, ad esempio</span><span class="sxs-lookup"><span data-stu-id="ba815-121">This array must be equal in size to the number of characters contained on this font page, i.e</span></span> <span data-ttu-id="ba815-122">(gx_font_last_glyph – gx_font_first_glyph) + 1.</span><span class="sxs-lookup"><span data-stu-id="ba815-122">(gx_font_last_glyph – gx_font_first_glyph) + 1.</span></span>

<span data-ttu-id="ba815-123">Il membro gx_font_next_page viene usato per i tipi di carattere a più pagine.</span><span class="sxs-lookup"><span data-stu-id="ba815-123">The gx_font_next_page member is used for multiple page fonts.</span></span> <span data-ttu-id="ba815-124">Per i set di caratteri estesi vengono usati più tipi di carattere della pagina e per ottimizzare le dimensioni delle matrici di struttura GX_GLYPH.</span><span class="sxs-lookup"><span data-stu-id="ba815-124">Multiple page fonts are used for extended character sets and to optimize the size of the GX_GLYPH structure arrays.</span></span> <span data-ttu-id="ba815-125">Se tutti i caratteri del tipo di carattere sono contenuti all'interno di una pagina del tipo di carattere o se si tratta dell'ultima pagina del tipo di carattere in questione, il gx_font_next_page membro viene impostato su GX_NULL.</span><span class="sxs-lookup"><span data-stu-id="ba815-125">If all of the characters of the font are contained within one font page, or if this is the last page of the font in question, the gx_font_next_page member is set to GX_NULL.</span></span>

<span data-ttu-id="ba815-126">Come indicato in precedenza, la GX_FONT struttura precedente contiene un puntatore a una matrice di strutture di GX_GLYPHS.</span><span class="sxs-lookup"><span data-stu-id="ba815-126">As noted above, the GX_FONT structure above contains a pointer to an array of GX_GLYPHS structures.</span></span> <span data-ttu-id="ba815-127">Per ogni carattere della pagina del tipo di carattere deve essere presente una struttura GX_GLYPH.</span><span class="sxs-lookup"><span data-stu-id="ba815-127">There must be one GX_GLYPH structure for each character on the font page.</span></span> <span data-ttu-id="ba815-128">La struttura GX_GLYPH è definita come segue:</span><span class="sxs-lookup"><span data-stu-id="ba815-128">The GX_GLYPH structure is defined as:</span></span>

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

<span data-ttu-id="ba815-129">Il puntatore gx_glyph_map punta alla bitmap dell'icona.</span><span class="sxs-lookup"><span data-stu-id="ba815-129">The gx_glyph_map pointer points to the glyph bitmap.</span></span> <span data-ttu-id="ba815-130">Questo puntatore può essere GX_NULL per gli spazi vuoti.</span><span class="sxs-lookup"><span data-stu-id="ba815-130">This pointer may be GX_NULL for whitespace characters.</span></span> <span data-ttu-id="ba815-131">I dati bitmap sono codificati come valori alfa 1 BPP, 2 BPP, 4 BPP o 8 BPP.</span><span class="sxs-lookup"><span data-stu-id="ba815-131">The bitmap data is encoded as 1 bpp, 2 bpp, 4 bpp, or 8 bpp alpha values.</span></span> <span data-ttu-id="ba815-132">Per i dati a 1 bit, il valore 1 indica che il pixel deve essere scritto nel colore di primo piano e il valore 0 indica che il pixel è trasparente.</span><span class="sxs-lookup"><span data-stu-id="ba815-132">For 1 bit data, a value of 1 indicates that the pixel should be written in the foreground color, and a value of 0 indicates that the pixel is transparent.</span></span> <span data-ttu-id="ba815-133">Per i dati a 8 bit, i valori variano da 0 (completamente trasparente) a 255 (completamente opaca).</span><span class="sxs-lookup"><span data-stu-id="ba815-133">For 8 bit data, the values range from 0 (fully transparent) to 255 (fully opague).</span></span> <span data-ttu-id="ba815-134">Tutto il valore intermedio rappresenta un valore di fusione per i tipi di carattere anti-aliasing.</span><span class="sxs-lookup"><span data-stu-id="ba815-134">All intermediate value represent a blending value for anti-aliased fonts.</span></span> <span data-ttu-id="ba815-135">I dati bitmap del glifo vengono sempre riempiti con l'allineamento a byte completo per i formati che usano valori di dati inferiori a 8bpp.</span><span class="sxs-lookup"><span data-stu-id="ba815-135">The glyph bitmap data is always padded to full byte alignment for formats using less than 8bpp data values.</span></span>

<span data-ttu-id="ba815-136">I valori gx_glyph_ascent e gx_glyph_descent posizionano verticalmente il glifo rispetto alla linea di base del tipo di carattere.</span><span class="sxs-lookup"><span data-stu-id="ba815-136">The gx_glyph_ascent and gx_glyph_descent values position the glyph vertically with respect to the font baseline.</span></span>

<span data-ttu-id="ba815-137">I valori gx_glyph_width e gx_glyph_height specificano le dimensioni dei dati bitmap del glifo.</span><span class="sxs-lookup"><span data-stu-id="ba815-137">The gx_glyph_width and gx_glyph_height values specify the size of the glyph bitmap data.</span></span>

<span data-ttu-id="ba815-138">Il valore gx_glyph_advance specifica la larghezza in pixel per far avanzare la posizione di disegno dopo aver disegnato il glifo (potrebbe non essere uguale alla larghezza del glifo).</span><span class="sxs-lookup"><span data-stu-id="ba815-138">The gx_glyph_advance value specifies the pixel width to advance the drawing position after drawing the glyph (this may not be equal to the glyph width).</span></span>

<span data-ttu-id="ba815-139">Il valore gx_glyph_leading specifica i pixel da avanzare nella direzione x prima di eseguire il rendering del glifo.</span><span class="sxs-lookup"><span data-stu-id="ba815-139">The gx_glyph_leading value specifies the pixels to advance in the x-direction prior to rendering the glyph.</span></span>