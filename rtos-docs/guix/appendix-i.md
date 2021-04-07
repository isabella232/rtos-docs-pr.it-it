---
title: Appendice I-strutture di informazioni GUIX
description: Informazioni sulle strutture di informazioni GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: dc7775cdde8f1aa89ca650561713f54ac6c069eb
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550219"
---
# <a name="appendix-i---guix-information-structures"></a><span data-ttu-id="6589c-103">Appendice I-strutture di informazioni GUIX</span><span class="sxs-lookup"><span data-stu-id="6589c-103">Appendix I - GUIX Information Structures</span></span> 

## <a name="gx_bidi_text_info"></a><span data-ttu-id="6589c-104">GX_BIDI_TEXT_INFO</span><span class="sxs-lookup"><span data-stu-id="6589c-104">GX_BIDI_TEXT_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="6589c-105">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-105">Definition</span></span>

```c
typedef struct GX_BIDI_TEXT_INFO_STRUCT
{
    GX_STRING gx_bidi_text_info_text;
    GX_FONT  *gx_bidi_text_info_font;
    GX_VALUE  gx_bidi_text_info_display_width;
} GX_BIDI_TEXT_INFO;
```
| <span data-ttu-id="6589c-106">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-106">Members</span></span> | <span data-ttu-id="6589c-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-107">Description</span></span> |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="6589c-108">**gx_bidi_text_info_text**</span><span class="sxs-lookup"><span data-stu-id="6589c-108">**gx_bidi_text_info_text**</span></span>               | <span data-ttu-id="6589c-109">Testo da riordinare</span><span class="sxs-lookup"><span data-stu-id="6589c-109">Text for reordering</span></span> |
| <span data-ttu-id="6589c-110">**gx_bidi_text_info_font**</span><span class="sxs-lookup"><span data-stu-id="6589c-110">**gx_bidi_text_info_font**</span></span>               | <span data-ttu-id="6589c-111">Tipo di carattere utilizzato per visualizzare il testo, impostarlo su GX_NULL se non è necessaria l'interruzioni di riga</span><span class="sxs-lookup"><span data-stu-id="6589c-111">Font used to display text, set it to GX_NULL if line breaking is not needed</span></span> |
| <span data-ttu-id="6589c-112">**gx_bidi_text_info_display_width**</span><span class="sxs-lookup"><span data-stu-id="6589c-112">**gx_bidi_text_info_display_width**</span></span>      | <span data-ttu-id="6589c-113">Larghezza disponibile per la visualizzazione, impostarla su-1 se non è necessaria l'interruzioni di riga</span><span class="sxs-lookup"><span data-stu-id="6589c-113">Available width for displaying, set it to -1 if line breaking is not needed</span></span> |

## <a name="gx_bidi_resolved_text_info"></a><span data-ttu-id="6589c-114">GX_BIDI_RESOLVED_TEXT_INFO</span><span class="sxs-lookup"><span data-stu-id="6589c-114">GX_BIDI_RESOLVED_TEXT_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="6589c-115">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-115">Definition</span></span>

```c
typedef struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT
{
    GX_STRING                                *gx_bidi_resolved_text_info_text;
    UINT                                      gx_bidi_resolved_text_info_total_lines;
    struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT *gx_bidi_resolved_text_info_next;
} GX_BIDI_RESOLVED_TEXT_INFO;
```

| <span data-ttu-id="6589c-116">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-116">Members</span></span> | <span data-ttu-id="6589c-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-117">Description</span></span> |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="6589c-118">**gx_bidi_resolved_text_info_text**</span><span class="sxs-lookup"><span data-stu-id="6589c-118">**gx_bidi_resolved_text_info_text**</span></span>             | <span data-ttu-id="6589c-119">Puntatore alla matrice del testo bidi riordinato</span><span class="sxs-lookup"><span data-stu-id="6589c-119">Pointer to the array of reordered bidi text</span></span> |
| <span data-ttu-id="6589c-120">**gx_bidi_resolved_text_info_total_lines**</span><span class="sxs-lookup"><span data-stu-id="6589c-120">**gx_bidi_resolved_text_info_total_lines**</span></span>      | <span data-ttu-id="6589c-121">Righe totali del testo bidi risolto per un paragrafo</span><span class="sxs-lookup"><span data-stu-id="6589c-121">Total lines of resolved bidi text for one paragraph</span></span> |
| <span data-ttu-id="6589c-122">**gx_bidi_resolved_text_info_next**</span><span class="sxs-lookup"><span data-stu-id="6589c-122">**gx_bidi_resolved_text_info_next**</span></span>             | <span data-ttu-id="6589c-123">Informazioni sul testo bidi risolto per il paragrafo successivo</span><span class="sxs-lookup"><span data-stu-id="6589c-123">Resolved bidi text information for the next paragraph</span></span> |

## <a name="gx_circular_gauge_info"></a><span data-ttu-id="6589c-124">GX_CIRCULAR_GAUGE_INFO</span><span class="sxs-lookup"><span data-stu-id="6589c-124">GX_CIRCULAR_GAUGE_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="6589c-125">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-125">Definition</span></span>

```c
typedef struct GX_CIRCULAR_GAUGE_INFO_STRUCT
{
    INT             gx_circular_gauge_info_animation_steps;
    INT             gx_circular_gauge_info_animation_delay;
    GX_VALUE        gx_circular_gauge_info_needle_xpos;
    GX_VALUE        gx_circular_gauge_info_needle_ypos;
    GX_VALUE        gx_circular_gauge_info_needle_xcor;
    GX_VALUE        gx_circular_gauge_info_needle_ycor;
    GX_RESOURCE_ID  gx_circular_gauge_info_needle_pixelmap;
} GX_CIRCULAR_GAUGE_INFO;
```

| <span data-ttu-id="6589c-126">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-126">Members</span></span> | <span data-ttu-id="6589c-127">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-127">Description</span></span> |
| ------------------------------------------------ | -------------------------------------------- |
| <span data-ttu-id="6589c-128">**gx_circular_gauge_info_animation_steps**</span><span class="sxs-lookup"><span data-stu-id="6589c-128">**gx_circular_gauge_info_animation_steps**</span></span>       | <span data-ttu-id="6589c-129">Passaggi totali durante i quali viene spostata l'ago quando si passa dall'angolo della lancetta corrente a un angolo della lancetta appena assegnato</span><span class="sxs-lookup"><span data-stu-id="6589c-129">Total steps the needle will travel through when moving from the current needle angle to a newly assigned needle angle</span></span> |
| <span data-ttu-id="6589c-130">**gx_circular_gauge_info_animation_delay**</span><span class="sxs-lookup"><span data-stu-id="6589c-130">**gx_circular_gauge_info_animation_delay**</span></span>       | <span data-ttu-id="6589c-131">Il numero di tick dell'orologio GUIX di ritardo tra i passaggi di animazione</span><span class="sxs-lookup"><span data-stu-id="6589c-131">The number of GUIX clock ticks to delay between animation steps</span></span> |
| <span data-ttu-id="6589c-132">**gx_circular_gauge_info_needle_xpos**</span><span class="sxs-lookup"><span data-stu-id="6589c-132">**gx_circular_gauge_info_needle_xpos**</span></span>           | <span data-ttu-id="6589c-133">Distanza tra la parte sinistra del widget del misuratore e il centro di rotazione della lancetta del misuratore</span><span class="sxs-lookup"><span data-stu-id="6589c-133">The distance from the left of the gauge widget to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="6589c-134">**gx_circular_gauge_info_needle_ypos**</span><span class="sxs-lookup"><span data-stu-id="6589c-134">**gx_circular_gauge_info_needle_ypos**</span></span>           | <span data-ttu-id="6589c-135">Distanza tra la parte superiore del widget del misuratore e il centro di rotazione della lancetta del misuratore</span><span class="sxs-lookup"><span data-stu-id="6589c-135">The distance from the top of the gauge widget to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="6589c-136">**gx_circular_gauge_info_needle_xcor**</span><span class="sxs-lookup"><span data-stu-id="6589c-136">**gx_circular_gauge_info_needle_xcor**</span></span>           | <span data-ttu-id="6589c-137">Distanza tra il lato sinistro dell'immagine della lancetta e il centro di rotazione della lancetta del misuratore</span><span class="sxs-lookup"><span data-stu-id="6589c-137">The distance from the left of the needle image to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="6589c-138">**gx_circular_gauge_info_needle_ycor**</span><span class="sxs-lookup"><span data-stu-id="6589c-138">**gx_circular_gauge_info_needle_ycor**</span></span>           | <span data-ttu-id="6589c-139">Distanza tra la parte superiore dell'immagine della lancetta e il centro di rotazione della lancetta del misuratore</span><span class="sxs-lookup"><span data-stu-id="6589c-139">The distance from the top of the needle image to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="6589c-140">**gx_circular_gauge_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-140">**gx_circular_gauge_info_needle_pixelmap**</span></span>       | <span data-ttu-id="6589c-141">ID di risorsa di Pixelmap che verrà usato per creare la lancetta del misuratore.</span><span class="sxs-lookup"><span data-stu-id="6589c-141">Resource ID of the pixelmap which will be used to draw the gauge needle.</span></span> <span data-ttu-id="6589c-142">Questa immagine verrà ruotata in base alle esigenze del widget misuratore per visualizzare la lancetta del misuratore in qualsiasi posizione</span><span class="sxs-lookup"><span data-stu-id="6589c-142">This image will be rotated as needed by the gauge widget to display the gauge needle in any position</span></span> |

<span data-ttu-id="6589c-143">Il diagramma seguente illustra le coordinate XPos, ypos e XCOR, ycor:</span><span class="sxs-lookup"><span data-stu-id="6589c-143">The diagram below illustrates the xpos, ypos, and xcor, ycor coordinates:</span></span>

![Diagramma delle coordinate Y e X della lancetta](./media/guix/image8.png)

## <a name="gx_line_chart_info"></a><span data-ttu-id="6589c-145">GX_LINE_CHART_INFO</span><span class="sxs-lookup"><span data-stu-id="6589c-145">GX_LINE_CHART_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="6589c-146">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-146">Definition</span></span>

```c
typedef struct GX_LINE_CHART_INFO_STRUCT
{
    INT            gx_line_chart_min_val;
    INT            gx_line_chart_max_val;
    INT           *gx_line_chart_data;
    GX_VALUE       gx_line_left_margin;
    GX_VALUE       gx_line_top_margin;
    GX_VALUE       gx_line_right_margin;
    GX_VALUE       gx_line_bottom_margin;
    GX_VALUE       gx_line_chart_max_data_count;
    GX_VALUE       gx_line_chart_active_data_count;
    GX_VALUE       gx_line_chart_axis_line_width;
    GX_VALUE       gx_line_chart_data_line_width;
    GX_RESOURCE_ID gx_line_chart_axis_color;
    GX_RESOURCE_ID gx_line_chart_line_color;
} GX_LINE_CHART_INFO;
```

| <span data-ttu-id="6589c-147">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-147">Members</span></span> | <span data-ttu-id="6589c-148">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-148">Description</span></span> |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="6589c-149">**gx_line_chart_min_val**</span><span class="sxs-lookup"><span data-stu-id="6589c-149">**gx_line_chart_min_val**</span></span>          | <span data-ttu-id="6589c-150">Valore minimo dei dati, utilizzato per calcolare il ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="6589c-150">The minimum data value, which is used to calculate scaling</span></span>
| <span data-ttu-id="6589c-151">**gx_line_chart_max_val**</span><span class="sxs-lookup"><span data-stu-id="6589c-151">**gx_line_chart_max_val**</span></span>          | <span data-ttu-id="6589c-152">Valore massimo dei dati, utilizzato per calcolare il ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="6589c-152">The maximum data value, which is used to calculate scaling</span></span> |
| <span data-ttu-id="6589c-153">**gx_line_chart_data**</span><span class="sxs-lookup"><span data-stu-id="6589c-153">**gx_line_chart_data**</span></span>             | <span data-ttu-id="6589c-154">Puntatore a una matrice di valori interi.</span><span class="sxs-lookup"><span data-stu-id="6589c-154">Pointer to an array of integer values.</span></span> <span data-ttu-id="6589c-155">Questi sono i valori integer tracciati dal widget grafico a linee</span><span class="sxs-lookup"><span data-stu-id="6589c-155">These are the integer values plotted by the line chart widget</span></span> |
| <span data-ttu-id="6589c-156">**gx_line_ <side> _margin**</span><span class="sxs-lookup"><span data-stu-id="6589c-156">**gx_line_<side>_margin**</span></span>          | <span data-ttu-id="6589c-157">Offset dalla finestra del grafico esterna associata all'area di rendering del grafico effettiva.</span><span class="sxs-lookup"><span data-stu-id="6589c-157">The offset from the chart window outer bound to the actual chart rendering area.</span></span> <span data-ttu-id="6589c-158">L'asse e la linea dati del grafico vengono sempre tracciati all'interno di questo limite interno, che consente all'applicazione di disegnare etichette e altre informazioni all'interno della finestra del grafico ma all'esterno dell'area del grafico char</span><span class="sxs-lookup"><span data-stu-id="6589c-158">The chart axis and data line are always plotted within this inner boundary, which allows the application to draw labels and other information inside the chart window but outside the char graphing area</span></span> |
| <span data-ttu-id="6589c-159">**gx_line_chart_max_data_count**</span><span class="sxs-lookup"><span data-stu-id="6589c-159">**gx_line_chart_max_data_count**</span></span>   | <span data-ttu-id="6589c-160">Numero di valori di dati che possono essere presenti.</span><span class="sxs-lookup"><span data-stu-id="6589c-160">The number of data values which may be present.</span></span> <span data-ttu-id="6589c-161">Questo parametro viene utilizzato per calcolare il ridimensionamento o l'intervallo dell'asse x per tracciare i punti dati.</span><span class="sxs-lookup"><span data-stu-id="6589c-161">This parameter is used for calculating the x-axis scaling or interval for plotting data points.</span></span> |
| <span data-ttu-id="6589c-162">**gx_line_active_data_count**</span><span class="sxs-lookup"><span data-stu-id="6589c-162">**gx_line_active_data_count**</span></span>      | <span data-ttu-id="6589c-163">Numero di valori di dati effettivamente presenti nella matrice di dati.</span><span class="sxs-lookup"><span data-stu-id="6589c-163">The number of data values that actually present in the data array.</span></span> <span data-ttu-id="6589c-164">Un grafico a linee può essere ridimensionato in modo da creare un massimo di 100 valori, ad esempio, ma in ogni particolare aggiornamento può essere effettivamente presente un numero minore di valori di dati.</span><span class="sxs-lookup"><span data-stu-id="6589c-164">A line chart may be scaled to draw a maximum of 100 values (for example), but on any particular update a smaller number of data values may actually be present.</span></span> |
| <span data-ttu-id="6589c-165">**gx_line_axis_line_width**</span><span class="sxs-lookup"><span data-stu-id="6589c-165">**gx_line_axis_line_width**</span></span>        | <span data-ttu-id="6589c-166">Larghezza della linea utilizzata per creare l'asse orizzontale e verticale</span><span class="sxs-lookup"><span data-stu-id="6589c-166">Width of the line used to draw the horizontal and vertical axis</span></span> |
| <span data-ttu-id="6589c-167">**gx_line_data_line_width**</span><span class="sxs-lookup"><span data-stu-id="6589c-167">**gx_line_data_line_width**</span></span>        | <span data-ttu-id="6589c-168">Larghezza della linea dati tracciato</span><span class="sxs-lookup"><span data-stu-id="6589c-168">Width of the plotted data line</span></span> |
| <span data-ttu-id="6589c-169">**gx_line_chart_axis_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-169">**gx_line_chart_axis_color**</span></span>       | <span data-ttu-id="6589c-170">ID risorsa del colore utilizzato per creare le linee dell'asse</span><span class="sxs-lookup"><span data-stu-id="6589c-170">Resource ID of the color used to draw the axis lines</span></span> |
| <span data-ttu-id="6589c-171">**gx_line_chart_line_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-171">**gx_line_chart_line_color**</span></span>       | <span data-ttu-id="6589c-172">ID risorsa del colore utilizzato per tracciare la linea dati del grafico</span><span class="sxs-lookup"><span data-stu-id="6589c-172">Resource ID of the color used to draw the chart data line</span></span> |

## <a name="gx_mouse_cursor_info"></a><span data-ttu-id="6589c-173">GX_MOUSE_CURSOR_INFO</span><span class="sxs-lookup"><span data-stu-id="6589c-173">GX_MOUSE_CURSOR_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="6589c-174">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-174">Definition</span></span>

```c
typedef struct GX_MOUSE_CURSOR_INFO_STRUCT
{
    GX_RESOURCE_ID             gx_mouse_cursor_image_id;
    GX_VALUE                   gx_mouse_cursor_hotspot_x;
    GX_VALUE                   gx_mouse_cursor_hotspot_y;
} GX_MOUSE_CURSOR_INFO;
```

| <span data-ttu-id="6589c-175">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-175">Members</span></span> | <span data-ttu-id="6589c-176">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-176">Description</span></span> |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="6589c-177">**gx_mouse_cursor_image_id**</span><span class="sxs-lookup"><span data-stu-id="6589c-177">**gx_mouse_cursor_image_id**</span></span>       | <span data-ttu-id="6589c-178">ID risorsa dell'immagine del mouse</span><span class="sxs-lookup"><span data-stu-id="6589c-178">Resource ID of the mouse image</span></span> |
| <span data-ttu-id="6589c-179">**gx_mouse_cursor_hotspot_x**</span><span class="sxs-lookup"><span data-stu-id="6589c-179">**gx_mouse_cursor_hotspot_x**</span></span>      | <span data-ttu-id="6589c-180">Offset dal lato sinistro dell'immagine del mouse all'area sensibile dell'immagine del mouse</span><span class="sxs-lookup"><span data-stu-id="6589c-180">The offset from the left of the mouse image to the mouse image hotspot</span></span> |
| <span data-ttu-id="6589c-181">**gx_mouse_cursor_hotspot_y**</span><span class="sxs-lookup"><span data-stu-id="6589c-181">**gx_mouse_cursor_hotspot_y**</span></span>      | <span data-ttu-id="6589c-182">Offset dalla parte superiore dell'immagine del mouse all'area sensibile dell'immagine del mouse</span><span class="sxs-lookup"><span data-stu-id="6589c-182">The offset from the top of the mouse image to the mouse image hotspot</span></span> |

## <a name="gx_pen_configuration"></a><span data-ttu-id="6589c-183">GX_PEN_CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="6589c-183">GX_PEN_CONFIGURATION</span></span> 

### <a name="definition"></a><span data-ttu-id="6589c-184">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-184">Definition</span></span>

```c
typedef struct GX_PEN_CONFIGURATION_STRUCT
{
    GX_FIXED_VAL     gx_pen_configuration_min_drag_dist;
    UINT             gx_pen_configuration_max_pen_speed_ticks;
}GX_PEN_CONFIGURATION;
```

| <span data-ttu-id="6589c-185">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-185">Members</span></span> | <span data-ttu-id="6589c-186">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-186">Description</span></span> |
| -------------------------------------------- | ------------------------------------------------ |
| <span data-ttu-id="6589c-187">**gx_pen_configuration_min_drag_dist**</span><span class="sxs-lookup"><span data-stu-id="6589c-187">**gx_pen_configuration_min_drag_dist**</span></span>       | <span data-ttu-id="6589c-188">Lunghezza minima del trascinamento per ogni ciclo del timer GUIX per attivare un evento FLICK.</span><span class="sxs-lookup"><span data-stu-id="6589c-188">The minimum drag distance per GUIX timer tick to trigger an FLICK event.</span></span> <span data-ttu-id="6589c-189">Chiamare GX_FIXED_VAL_MAKE per creare un valore del tipo di dati a virgola fissa</span><span class="sxs-lookup"><span data-stu-id="6589c-189">Call GX_FIXED_VAL_MAKE to make a fixed point data type value</span></span> |
| <span data-ttu-id="6589c-190">**gx_pen_configuration_max_pen_speed_ticks**</span><span class="sxs-lookup"><span data-stu-id="6589c-190">**gx_pen_configuration_max_pen_speed_ticks**</span></span> | <span data-ttu-id="6589c-191">Velocità massima di trascinamento nei cicli del timer GUIX per attivare un evento FLICK</span><span class="sxs-lookup"><span data-stu-id="6589c-191">The maximum drag speed in GUIX timer ticks to trigger an FLICK event</span></span> | 

## <a name="gx_pixelmap_slider_info"></a><span data-ttu-id="6589c-192">GX_PIXELMAP_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="6589c-192">GX_PIXELMAP_SLIDER_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="6589c-193">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-193">Definition</span></span>

```c
typedef struct GX_PIXELMAP_SLIDER_INFO_STRUCT
{
    GX_RESOURCE_ID gx_pixelmap_slider_info_lower_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_upper_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_needle_pixelmap;
} GX_PIXELMAP_SLIDER_INFO;
```

| <span data-ttu-id="6589c-194">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-194">Members</span></span> | <span data-ttu-id="6589c-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-195">Description</span></span> |
| ----------------------------------------------------- | ---------------------------------------- |
| <span data-ttu-id="6589c-196">**gx_pixelmap_slider_info_lower_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-196">**gx_pixelmap_slider_info_lower_background_pixelmap**</span></span> | <span data-ttu-id="6589c-197">ID di risorsa di Pixelmap per riempire lo sfondo prima della lancetta.</span><span class="sxs-lookup"><span data-stu-id="6589c-197">Resource ID of the pixelmap for filling the background before the needle.</span></span> <span data-ttu-id="6589c-198">Se il Pixelmap in background superiore non è impostato, viene usato per riempire lo sfondo sia prima che dopo la lancetta</span><span class="sxs-lookup"><span data-stu-id="6589c-198">If upper background pixelmap is not set, it’s used for filling background both before and after the needle</span></span> |
| <span data-ttu-id="6589c-199">**gx_pixelmap_slider_info_upper_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-199">**gx_pixelmap_slider_info_upper_background_pixelmap**</span></span> | <span data-ttu-id="6589c-200">ID di risorsa di Pixelmap per riempire lo sfondo dopo l'ago</span><span class="sxs-lookup"><span data-stu-id="6589c-200">Resource ID of the pixelmap for filling background after the needle</span></span> |
| <span data-ttu-id="6589c-201">**gx_pixelmap_slider_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-201">**gx_pixelmap_slider_info_needle_pixelmap**</span></span>           | <span data-ttu-id="6589c-202">ID risorsa della lancetta pixelmap</span><span class="sxs-lookup"><span data-stu-id="6589c-202">Resource ID of the needle pixelmap</span></span> |

## <a name="gx_progress_bar_info"></a><span data-ttu-id="6589c-203">GX_PROGRESS_BAR_INFO</span><span class="sxs-lookup"><span data-stu-id="6589c-203">GX_PROGRESS_BAR_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="6589c-204">**Definition**</span><span class="sxs-lookup"><span data-stu-id="6589c-204">**Definition**</span></span>

```c
typedef struct GX_PROGRESS_BAR_INFO_STRUCT
{
    INT gx_progress_bar_info_min_val;
    INT gx_progress_bar_info_max_val;
    INT gx_progress_bar_info_current_val;
    GX_RESOURCE_ID gx_progress_bar_font_id;
    GX_RESOURCE_ID gx_progress_bar_normal_text_color;
    GX_RESOURCE_ID gx_progress_bar_selected_text_color;
    GX_RESOURCE_ID gx_progress_bar_disabled_text_color;
    GX_RESOURCE_ID gx_progress_bar_fill_pixelmap;
} GX_PROGRESS_BAR_INFO;
```

| <span data-ttu-id="6589c-205">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-205">Members</span></span> | <span data-ttu-id="6589c-206">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-206">Description</span></span> |
| -------------------------------------------- | ------------------------------------------------ |
| <span data-ttu-id="6589c-207">**gx_progress_bar_info_min_val**</span><span class="sxs-lookup"><span data-stu-id="6589c-207">**gx_progress_bar_info_min_val**</span></span>             | <span data-ttu-id="6589c-208">Valore minimo segnalato</span><span class="sxs-lookup"><span data-stu-id="6589c-208">Minimum reported value</span></span> |
| <span data-ttu-id="6589c-209">**gx_progress_bar_info_max_val**</span><span class="sxs-lookup"><span data-stu-id="6589c-209">**gx_progress_bar_info_max_val**</span></span>             | <span data-ttu-id="6589c-210">Valore massimo segnalato</span><span class="sxs-lookup"><span data-stu-id="6589c-210">Maximum reported value</span></span> |
| <span data-ttu-id="6589c-211">**gx_progress_bar_info_current_val**</span><span class="sxs-lookup"><span data-stu-id="6589c-211">**gx_progress_bar_info_current_val**</span></span>         | <span data-ttu-id="6589c-212">Valore corrente</span><span class="sxs-lookup"><span data-stu-id="6589c-212">Current value</span></span> |
| <span data-ttu-id="6589c-213">**gx_progress_bar_info_font_id**</span><span class="sxs-lookup"><span data-stu-id="6589c-213">**gx_progress_bar_info_font_id**</span></span>             | <span data-ttu-id="6589c-214">ID risorsa del tipo di carattere, usato per creare il valore di testo facoltativo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="6589c-214">Resource ID of the font, used to draw the optional text value within the progress bar widget</span></span>      |
| <span data-ttu-id="6589c-215">**gx_progress_bar_normal_text_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-215">**gx_progress_bar_normal_text_color**</span></span>        | <span data-ttu-id="6589c-216">ID risorsa del colore del testo nello stato normale, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="6589c-216">Resource ID of the text color in normal state, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="6589c-217">**gx_progress_bar_selected_text_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-217">**gx_progress_bar_selected_text_color**</span></span>      | <span data-ttu-id="6589c-218">ID risorsa del colore del testo quando il widget ottiene lo stato attivo, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="6589c-218">Resource ID of the text color when the widget gain focus, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="6589c-219">**gx_progress_bar_disabled_text_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-219">**gx_progress_bar_disabled_text_color**</span></span>      | <span data-ttu-id="6589c-220">ID risorsa del colore del testo quando GX_STYLE_ENABLED non è attivo, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="6589c-220">Resource ID of the text color when GX_STYLE_ENABLED is not active, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="6589c-221">**gx_progress_bar_fill_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-221">**gx_progress_bar_fill_pixelmap**</span></span>            | <span data-ttu-id="6589c-222">ID risorsa di Pixelmap per riempimento in background</span><span class="sxs-lookup"><span data-stu-id="6589c-222">Resource ID of the pixelmap for background filling</span></span>|

## <a name="gx_radial_progress_bar_info"></a><span data-ttu-id="6589c-223">GX_RADIAL_PROGRESS_BAR_INFO</span><span class="sxs-lookup"><span data-stu-id="6589c-223">GX_RADIAL_PROGRESS_BAR_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="6589c-224">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-224">Definition</span></span>

```c
typedef struct GX_RADIAL_PROGRESS_BAR_INFO_STRUCT
{
    GX_VALUE       gx_radial_progress_bar_info_xcenter;
    GX_VALUE       gx_radial_progress_bar_info_ycenter;
    GX_VALUE       gx_radial_progress_bar_info_radius;
    GX_VALUE       gx_radial_progress_bar_info_current_val;
    GX_VALUE       gx_radial_progress_bar_info_anchor_val;
    GX_RESOURCE_ID gx_radial_progress_bar_info_font_id;
    GX_RESOURCE_ID gx_radial_progress_bar_info_normal_text_color;
    GX_RESOURCE_ID gx_radial_progress_bar_info_selected_text_color;
    GX_RESOURCE_ID gx_radial_progress_bar_info_disabled_text_color;
    GX_VALUE       gx_radial_progress_bar_info_normal_brush_width;
    GX_VALUE       gx_radial_progress_bar_info_selected_brush_width;
    GX_RESOURCE_ID gx_radial_progress_bar_info_normal_brush_color;
    GX_RESOURCE_ID gx_radial_progress_bar_info_selected_brush_color;
} GX_RADIAL_PROGRESS_BAR_INFO;
```

| <span data-ttu-id="6589c-225">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-225">Members</span></span> | <span data-ttu-id="6589c-226">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-226">Description</span></span> |
| ------------------------------------------------- | -------------------------------------------- |
| <span data-ttu-id="6589c-227">**gx_radial_progress_bar_info_xcenter**</span><span class="sxs-lookup"><span data-stu-id="6589c-227">**gx_radial_progress_bar_info_xcenter**</span></span>           | <span data-ttu-id="6589c-228">Posizione del widget nella coordinata x</span><span class="sxs-lookup"><span data-stu-id="6589c-228">Widget position in x coordinate</span></span> |
| <span data-ttu-id="6589c-229">**gx_radial_progress_bar_info_ycenter**</span><span class="sxs-lookup"><span data-stu-id="6589c-229">**gx_radial_progress_bar_info_ycenter**</span></span>           | <span data-ttu-id="6589c-230">Posizione del widget nella coordinata y</span><span class="sxs-lookup"><span data-stu-id="6589c-230">Widget position in y coordinate</span></span>  |
| <span data-ttu-id="6589c-231">**gx_radial_progress_bar_info_radius**</span><span class="sxs-lookup"><span data-stu-id="6589c-231">**gx_radial_progress_bar_info_radius**</span></span>            | <span data-ttu-id="6589c-232">Raggio del cerchio di avanzamento</span><span class="sxs-lookup"><span data-stu-id="6589c-232">Radius of the progress circle</span></span> |
| <span data-ttu-id="6589c-233">**gx_radial_progress_bar_info_current_val**</span><span class="sxs-lookup"><span data-stu-id="6589c-233">**gx_radial_progress_bar_info_current_val**</span></span>       | <span data-ttu-id="6589c-234">Il valore corrente, limitato all'intervallo [-360, 360], indica il Delta angolare tra la posizione di ancoraggio e il punto finale dell'arco superiore. Il valore negativo determina il disegno dell'arco in senso orario a partire dalla posizione di ancoraggio.</span><span class="sxs-lookup"><span data-stu-id="6589c-234">Current value, limited to the range [-360, 360], indicates the angular delta between the anchor position and the end point of the upper arc. Negative value causes the arc to be drawn in a clockwise direction starting at the anchor position.</span></span> <span data-ttu-id="6589c-235">Il valore positivo fa in modo che l'arco venga disegnato in senso antiorario a partire dalla posizione di ancoraggio.</span><span class="sxs-lookup"><span data-stu-id="6589c-235">Positive value causes the arc to be drawn in a counter-clockwise direction starting at the anchor position.</span></span> <span data-ttu-id="6589c-236">L'applicazione deve ridimensionare il valore di parola reale indicato per assegnare un valore angolare al widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="6589c-236">The application must scale the real-word value being indicated to assign an angular value to the progress bar widget</span></span> |
| <span data-ttu-id="6589c-237">**gx_radial_progress_bar_anchor_val**</span><span class="sxs-lookup"><span data-stu-id="6589c-237">**gx_radial_progress_bar_anchor_val**</span></span>             | <span data-ttu-id="6589c-238">Angolo iniziale dell'arco di avanzamento superiore. Il valore è definito in termini di un numero intero con un grado di 0 che punta a destra e un grado di 90 indica la posizione verticale.</span><span class="sxs-lookup"><span data-stu-id="6589c-238">Starting angle of the upper progress arc. The value is defined in terms of integer degree with 0 degree pointing to the right and 90 degree indicating straight up position.</span></span> |
| <span data-ttu-id="6589c-239">**gx_radial_progress_bar_font_id**</span><span class="sxs-lookup"><span data-stu-id="6589c-239">**gx_radial_progress_bar_font_id**</span></span>                | <span data-ttu-id="6589c-240">ID risorsa del tipo di carattere utilizzato per creare il valore di testo facoltativo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="6589c-240">Resource ID of the font used to draw the optional text value within the progress bar widget</span></span> |
| <span data-ttu-id="6589c-241">**gx_radial_progress_bar_normal_text_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-241">**gx_radial_progress_bar_normal_text_color**</span></span>      | <span data-ttu-id="6589c-242">ID risorsa del colore del testo nello stato normale, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="6589c-242">Resource ID of the text color in normal state, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="6589c-243">**gx_radial_progress_bar_selected_text_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-243">**gx_radial_progress_bar_selected_text_color**</span></span>    |<span data-ttu-id="6589c-244">ID risorsa del colore del testo quando il widget ottiene lo stato attivo, usato per definire il disegno del testo facoltativo nel widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="6589c-244">Resource ID of the text color when widget gain focus, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="6589c-245">**gx_radial_progress_bar_disabled_text_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-245">**gx_radial_progress_bar_disabled_text_color**</span></span>    | <span data-ttu-id="6589c-246">ID risorsa del colore del testo quando GX_STYLE_ENABLED non è attivo, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="6589c-246">Resource ID of the text color when GX_STYLE_ENABLED is not active, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="6589c-247">**gx_radial_progress_bar_normal_brush_width**</span><span class="sxs-lookup"><span data-stu-id="6589c-247">**gx_radial_progress_bar_normal_brush_width**</span></span>     | <span data-ttu-id="6589c-248">Larghezza del cerchio di avanzamento inferiore</span><span class="sxs-lookup"><span data-stu-id="6589c-248">Width of the lower progress circle</span></span> |
| <span data-ttu-id="6589c-249">**gx_radial_progress_bar_selected_brush_width**</span><span class="sxs-lookup"><span data-stu-id="6589c-249">**gx_radial_progress_bar_selected_brush_width**</span></span>   | <span data-ttu-id="6589c-250">Larghezza dell'arco di avanzamento superiore, l'arco superiore può essere più piccolo, uguale o più ampio del cerchio inferiore</span><span class="sxs-lookup"><span data-stu-id="6589c-250">Width of the upper progress arc, the upper arc may be narrower, the same as, or wider than the lower circle</span></span> |
| <span data-ttu-id="6589c-251">**gx_radial_progress_bar_normal_brush_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-251">**gx_radial_progress_bar_normal_brush_color**</span></span>     | <span data-ttu-id="6589c-252">ID risorsa del colore per riempire il cerchio di avanzamento inferiore</span><span class="sxs-lookup"><span data-stu-id="6589c-252">Resource ID of the color to fill lower progress circle</span></span> |
| <span data-ttu-id="6589c-253">**gx_radial_progress_bar_selected_brush_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-253">**gx_radial_progress_bar_selected_brush_color**</span></span>   | <span data-ttu-id="6589c-254">ID risorsa del colore per riempire l'arco di avanzamento superiore</span><span class="sxs-lookup"><span data-stu-id="6589c-254">Resource ID of the color to fill upper progress arc</span></span> |

## <a name="gx_radial_slider_info"></a><span data-ttu-id="6589c-255">GX_RADIAL_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="6589c-255">GX_RADIAL_SLIDER_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="6589c-256">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-256">Definition</span></span>

```c
typedef struct GX_RADIAL_SLIDER_INFO_STRUCT
{
    GX_VALUE       gx_radial_slider_info_xcenter;
    GX_VALUE       gx_radial_slider_info_ycenter;
    USHORT         gx_radial_slider_info_radius;
    USHORT         gx_radial_slider_info_track_width;
    GX_VALUE       gx_radial_slider_info_current_angle;
    GX_VALUE       gx_radial_slider_info_min_angle;
    GX_VALUE       gx_radial_slider_info_max_angle;
    GX_VALUE      *gx_radial_slider_info_angle_list;
    USHORT         gx_radial_slider_info_list_cont;
    GX_RESOURCE_ID gx_radial_slider_info_background_pixelmap;
    GX_RESOURCE_ID gx_radial_slider_info_needle_pixelmap;
} GX_RADIAL_SLIDER_INFO;
```

| <span data-ttu-id="6589c-257">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-257">Members</span></span> | <span data-ttu-id="6589c-258">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-258">Description</span></span> |
| --------------------------------------------- | ------------------------------------------------ |
<span data-ttu-id="6589c-259">**gx_radial_slider_info_xcenter**</span><span class="sxs-lookup"><span data-stu-id="6589c-259">**gx_radial_slider_info_xcenter**</span></span>               | <span data-ttu-id="6589c-260">Distanza tra la parte sinistra del widget del dispositivo di scorrimento e il centro di rotazione della lancetta del dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="6589c-260">Distance from the left of the slider widget to the center-of-rotation of the slider needle</span></span> |
| <span data-ttu-id="6589c-261">**gx_radial_slider_info_ycenter**</span><span class="sxs-lookup"><span data-stu-id="6589c-261">**gx_radial_slider_info_ycenter**</span></span>             | <span data-ttu-id="6589c-262">Distanza dalla parte superiore del widget del dispositivo di scorrimento al centro di rotazione della lancetta del dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="6589c-262">Distance from the top of the slider widget to the center-of-rotation of the slider needle</span></span> |
| <span data-ttu-id="6589c-263">**gx_radial_slider_info_radius**</span><span class="sxs-lookup"><span data-stu-id="6589c-263">**gx_radial_slider_info_radius**</span></span>              | <span data-ttu-id="6589c-264">Raggio del cerchio del dispositivo di scorrimento radiale</span><span class="sxs-lookup"><span data-stu-id="6589c-264">Radius of the radial slider circle</span></span> |
| <span data-ttu-id="6589c-265">**gx_radial_slider_info_track_width**</span><span class="sxs-lookup"><span data-stu-id="6589c-265">**gx_radial_slider_info_track_width**</span></span>         | <span data-ttu-id="6589c-266">Larghezza della traccia del dispositivo di scorrimento radiale</span><span class="sxs-lookup"><span data-stu-id="6589c-266">Width of radial slider track</span></span> |
| <span data-ttu-id="6589c-267">**gx_radial_slider_info_current_angle**</span><span class="sxs-lookup"><span data-stu-id="6589c-267">**gx_radial_slider_info_current_angle**</span></span>       | <span data-ttu-id="6589c-268">Angolo del dispositivo di scorrimento corrente</span><span class="sxs-lookup"><span data-stu-id="6589c-268">Current slider angle</span></span> |
| <span data-ttu-id="6589c-269">**gx_radial_slider_info_min_angle**</span><span class="sxs-lookup"><span data-stu-id="6589c-269">**gx_radial_slider_info_min_angle**</span></span>           | <span data-ttu-id="6589c-270">Angolo minimo del dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="6589c-270">Minimum slider angle</span></span> |
| <span data-ttu-id="6589c-271">**gx_radial_slider_info_max_angle**</span><span class="sxs-lookup"><span data-stu-id="6589c-271">**gx_radial_slider_info_max_angle**</span></span>           | <span data-ttu-id="6589c-272">Angolo massimo dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="6589c-272">Maximum slider angle</span></span> |
| <span data-ttu-id="6589c-273">**gx_radial_slider_info_angle_list**</span><span class="sxs-lookup"><span data-stu-id="6589c-273">**gx_radial_slider_info_angle_list**</span></span>          | <span data-ttu-id="6589c-274">Elenco di valori angolo, definisce gli angoli di ancoraggio, se impostati, l'angolo del dispositivo di scorrimento può essere solo uno degli angoli di ancoraggio definiti</span><span class="sxs-lookup"><span data-stu-id="6589c-274">Angle value list, defines anchor angles, if set, slider angle can only be one of the defined anchor angles</span></span> |
| <span data-ttu-id="6589c-275">**gx_radial_slider_info_list_count**</span><span class="sxs-lookup"><span data-stu-id="6589c-275">**gx_radial_slider_info_list_count**</span></span>          | <span data-ttu-id="6589c-276">Numero di angoli di ancoraggio</span><span class="sxs-lookup"><span data-stu-id="6589c-276">Number of anchor angles</span></span> |
| <span data-ttu-id="6589c-277">**gx_radial_slider_info_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-277">**gx_radial_slider_info_background_pixelmap**</span></span> | <span data-ttu-id="6589c-278">ID risorsa dello sfondo pixelmap</span><span class="sxs-lookup"><span data-stu-id="6589c-278">Resource ID of background pixelmap</span></span> |
| <span data-ttu-id="6589c-279">**gx_radial_slider_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-279">**gx_radial_slider_info_needle_pixelmap**</span></span>     | <span data-ttu-id="6589c-280">ID risorsa dell'ago pixelmap</span><span class="sxs-lookup"><span data-stu-id="6589c-280">Resource ID of needle pixelmap</span></span> |

## <a name="gx_rectangle"></a><span data-ttu-id="6589c-281">GX_RECTANGLE</span><span class="sxs-lookup"><span data-stu-id="6589c-281">GX_RECTANGLE</span></span>

### <a name="definition"></a><span data-ttu-id="6589c-282">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-282">Definition</span></span>

```c
typedef struct GX_RECTANGLE_STRUCT
{
    GX_VALUE gx_rectangle_left;
    GX_VALUE gx_rectangle_top;
    GX_VALUE gx_rectangle_right;
    GX_VALUE gx_rectangle_bottom;
} GX_RECTANGLE;
```

| <span data-ttu-id="6589c-283">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-283">Members</span></span> | <span data-ttu-id="6589c-284">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-284">Description</span></span> |
| -------------------------------- | ------------------------|
| <span data-ttu-id="6589c-285">**gx_rectangle_left**</span><span class="sxs-lookup"><span data-stu-id="6589c-285">**gx_rectangle_left**</span></span>            | <span data-ttu-id="6589c-286">A sinistra del rettangolo</span><span class="sxs-lookup"><span data-stu-id="6589c-286">Left of the rectangle</span></span>   |  
| <span data-ttu-id="6589c-287">**gx_rectangle_top**</span><span class="sxs-lookup"><span data-stu-id="6589c-287">**gx_rectangle_top**</span></span>             | <span data-ttu-id="6589c-288">Parte superiore del rettangolo</span><span class="sxs-lookup"><span data-stu-id="6589c-288">Top of the rectangle</span></span>    | 
| <span data-ttu-id="6589c-289">**gx_rectangle_right**</span><span class="sxs-lookup"><span data-stu-id="6589c-289">**gx_rectangle_right**</span></span>           | <span data-ttu-id="6589c-290">A destra del rettangolo</span><span class="sxs-lookup"><span data-stu-id="6589c-290">Right of the rectangle</span></span>  |
| <span data-ttu-id="6589c-291">**gx_rectangle_bottom**</span><span class="sxs-lookup"><span data-stu-id="6589c-291">**gx_rectangle_bottom**</span></span>          | <span data-ttu-id="6589c-292">Parte inferiore del rettangolo</span><span class="sxs-lookup"><span data-stu-id="6589c-292">Bottom of the rectangle</span></span> |

## <a name="gx_rich_text_fonts"></a><span data-ttu-id="6589c-293">GX_RICH_TEXT_FONTS</span><span class="sxs-lookup"><span data-stu-id="6589c-293">GX_RICH_TEXT_FONTS</span></span> 

### <a name="definition"></a><span data-ttu-id="6589c-294">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-294">Definition</span></span>

```c
typedef struct GX_RICH_TEXT_FONTS_STRUCT
{
    GX_RESOURCE_ID             gx_rich_text_fonts_normal_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_italic_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_italic_id;
} GX_RICH_TEXT_FONTS;
```

| <span data-ttu-id="6589c-295">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-295">Members</span></span> | <span data-ttu-id="6589c-296">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-296">Description</span></span> |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="6589c-297">**gx_rich_text_fonts_normal_id**</span><span class="sxs-lookup"><span data-stu-id="6589c-297">**gx_rich_text_fonts_normal_id**</span></span>   | <span data-ttu-id="6589c-298">ID risorsa del tipo di carattere testo normale</span><span class="sxs-lookup"><span data-stu-id="6589c-298">Resource ID of normal text font</span></span> |
| <span data-ttu-id="6589c-299">**gx_rich_text_fonts_bold_id**</span><span class="sxs-lookup"><span data-stu-id="6589c-299">**gx_rich_text_fonts_bold_id**</span></span>     | <span data-ttu-id="6589c-300">ID risorsa del tipo di carattere testo in grassetto</span><span class="sxs-lookup"><span data-stu-id="6589c-300">Resource ID of bold text font</span></span> |
| <span data-ttu-id="6589c-301">**gx_rich_text_fonts_italic_id**</span><span class="sxs-lookup"><span data-stu-id="6589c-301">**gx_rich_text_fonts_italic_id**</span></span>   | <span data-ttu-id="6589c-302">ID risorsa del tipo di carattere del testo in corsivo</span><span class="sxs-lookup"><span data-stu-id="6589c-302">Resource ID of italic text font</span></span> |
| <span data-ttu-id="6589c-303">**gx_rich_text_fonts_bold_italic_id**</span><span class="sxs-lookup"><span data-stu-id="6589c-303">**gx_rich_text_fonts_bold_italic_id**</span></span> | <span data-ttu-id="6589c-304">ID risorsa del tipo di carattere testo in corsivo grassetto</span><span class="sxs-lookup"><span data-stu-id="6589c-304">Resource ID of bold italic text font</span></span> |

## <a name="gx_scroll_info"></a><span data-ttu-id="6589c-305">GX_SCROLL_INFO</span><span class="sxs-lookup"><span data-stu-id="6589c-305">GX_SCROLL_INFO</span></span> 
### <a name="definition"></a><span data-ttu-id="6589c-306">**Definition**</span><span class="sxs-lookup"><span data-stu-id="6589c-306">**Definition**</span></span>

```c
typedef struct GX_SCROLL_INFO_STRUCT
{
    INT      gx_scroll_value;
    INT      gx_scroll_minimum;
    INT      gx_scroll_maximum;
    GX_VALUE gx_scroll_visible;
    GX_VALUE gx_scroll_increment;
} GX_SCROLL_INFO;
```

| <span data-ttu-id="6589c-307">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-307">Members</span></span> | <span data-ttu-id="6589c-308">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-308">Description</span></span> |
| ----------------------- | ----------------------------- |
| <span data-ttu-id="6589c-309">**gx_scroll_value**</span><span class="sxs-lookup"><span data-stu-id="6589c-309">**gx_scroll_value**</span></span>     | <span data-ttu-id="6589c-310">Posizione di scorrimento corrente</span><span class="sxs-lookup"><span data-stu-id="6589c-310">Current scroll position</span></span>       |
| <span data-ttu-id="6589c-311">**gx_scroll_minimum**</span><span class="sxs-lookup"><span data-stu-id="6589c-311">**gx_scroll_minimum**</span></span>   | <span data-ttu-id="6589c-312">Posizione minima segnalata</span><span class="sxs-lookup"><span data-stu-id="6589c-312">Minimum reported position</span></span>     |
| <span data-ttu-id="6589c-313">**gx_scroll_maximum**</span><span class="sxs-lookup"><span data-stu-id="6589c-313">**gx_scroll_maximum**</span></span>   | <span data-ttu-id="6589c-314">Posizione massima segnalata</span><span class="sxs-lookup"><span data-stu-id="6589c-314">Maximum reported position</span></span>     |
| <span data-ttu-id="6589c-315">**gx_scroll_visible**</span><span class="sxs-lookup"><span data-stu-id="6589c-315">**gx_scroll_visible**</span></span>   | <span data-ttu-id="6589c-316">Intervallo visibile della finestra padre</span><span class="sxs-lookup"><span data-stu-id="6589c-316">Parent window visible range</span></span>   |
| <span data-ttu-id="6589c-317">**gx_scroll_increment**</span><span class="sxs-lookup"><span data-stu-id="6589c-317">**gx_scroll_increment**</span></span> | <span data-ttu-id="6589c-318">Valore delta minimo barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="6589c-318">Scrollbar minimum delta value</span></span> |

## <a name="gx_scrollbar_appearance"></a><span data-ttu-id="6589c-319">GX_SCROLLBAR_APPEARANCE</span><span class="sxs-lookup"><span data-stu-id="6589c-319">GX_SCROLLBAR_APPEARANCE</span></span> 

### <a name="definition"></a><span data-ttu-id="6589c-320">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-320">Definition</span></span>

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

| <span data-ttu-id="6589c-321">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-321">Members</span></span> | <span data-ttu-id="6589c-322">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-322">Description</span></span> |
| ---------------------------------------- | ----------------------------------------------------- |
| <span data-ttu-id="6589c-323">**gx_scroll_width**</span><span class="sxs-lookup"><span data-stu-id="6589c-323">**gx_scroll_width**</span></span>                      | <span data-ttu-id="6589c-324">Larghezza del widget della barra di scorrimento, in pixel</span><span class="sxs-lookup"><span data-stu-id="6589c-324">Width of the scrollbar widget, in pixels</span></span> |
| <span data-ttu-id="6589c-325">**gx_scroll_thumb_width**</span><span class="sxs-lookup"><span data-stu-id="6589c-325">**gx_scroll_thumb_width**</span></span>                | <span data-ttu-id="6589c-326">Larghezza del pulsante Thumb che scorre la barra di scorrimento, in pixel.</span><span class="sxs-lookup"><span data-stu-id="6589c-326">Width of the thumb button which slides on the scrollbar, in pixels.</span></span> <span data-ttu-id="6589c-327">Questo valore è in genere un numero di pixel inferiore alla lunghezza totale della barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="6589c-327">This value is usually some number of pixels less than the total scrollbar width</span></span> |
| <span data-ttu-id="6589c-328">**gx_scroll_thumb_travel_min**</span><span class="sxs-lookup"><span data-stu-id="6589c-328">**gx_scroll_thumb_travel_min**</span></span>           | <span data-ttu-id="6589c-329">Offset dalla fine della barra di scorrimento al punto di partenza del pulsante Thumb minimo.</span><span class="sxs-lookup"><span data-stu-id="6589c-329">Offset from the end of scrollbar to minimum thumb button travel point.</span></span> <span data-ttu-id="6589c-330">Questo limite può essere utilizzato per impedire che il pulsante Thumb venga spostata alla fine della barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="6589c-330">This limit can be used to prevent the thumb button from traveling to the very end of the scrollbar</span></span> |
| <span data-ttu-id="6589c-331">**gx_scroll_thumb_travel_max**</span><span class="sxs-lookup"><span data-stu-id="6589c-331">**gx_scroll_thumb_travel_max**</span></span>           | <span data-ttu-id="6589c-332">Offset dalla fine della barra di scorrimento al punto di partenza del pulsante Thumb massimo.</span><span class="sxs-lookup"><span data-stu-id="6589c-332">Offset from the end of scrollbar to maximum thumb button travel point.</span></span> <span data-ttu-id="6589c-333">Questo limite può essere utilizzato per impedire che il pulsante Thumb venga spostata alla fine della barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="6589c-333">This limit can be used to prevent the thumb button from traveling to the very end of the scrollbar</span></span> |
| <span data-ttu-id="6589c-334">**gx_scroll_thumb_border_style**</span><span class="sxs-lookup"><span data-stu-id="6589c-334">**gx_scroll_thumb_border_style**</span></span>         | <span data-ttu-id="6589c-335">Stili del bordo del pulsante Thumb</span><span class="sxs-lookup"><span data-stu-id="6589c-335">Border styles of thumb button</span></span> |
| <span data-ttu-id="6589c-336">**gx_scroll_fill_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-336">**gx_scroll_fill_pixelmap**</span></span>              | <span data-ttu-id="6589c-337">ID Pixelmap facoltativo.</span><span class="sxs-lookup"><span data-stu-id="6589c-337">Optional pixelmap ID.</span></span> <span data-ttu-id="6589c-338">Se questo ID Pixelmap è diverso da zero, la barra di scorrimento utilizza questo Pixelmap per creare lo sfondo della barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="6589c-338">If this pixelmap ID is not zero, the scrollbar uses this pixelmap to draw the scrollbar background</span></span> |
| <span data-ttu-id="6589c-339">**gx_scroll_thumb_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-339">**gx_scroll_thumb_pixelmap**</span></span>             | <span data-ttu-id="6589c-340">ID Pixelmap facoltativo.</span><span class="sxs-lookup"><span data-stu-id="6589c-340">Optional pixelmap ID.</span></span> <span data-ttu-id="6589c-341">Se questo ID Pixelmap è diverso da zero, il pulsante Thumb della barra di scorrimento utilizza questo Pixelmap per disegnarsi</span><span class="sxs-lookup"><span data-stu-id="6589c-341">If this pixelmap ID is not zero, the scrollbar thumb button uses this pixelmap to draw itself</span></span> |
| <span data-ttu-id="6589c-342">**gx_scroll_up_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-342">**gx_scroll_up_pixelmap**</span></span>                | <span data-ttu-id="6589c-343">ID Pixelmap facoltativo.</span><span class="sxs-lookup"><span data-stu-id="6589c-343">Optional pixelmap ID.</span></span> <span data-ttu-id="6589c-344">Se questo ID Pixelmap è diverso da zero, la barra di scorrimento utilizza questo ID Pixelmap per creare il pulsante di fine della barra di scorrimento a sinistra</span><span class="sxs-lookup"><span data-stu-id="6589c-344">If this pixelmap ID is not zero, the scrollbar uses this pixelmap ID to draw the scrollbar left/up end button</span></span> |
| <span data-ttu-id="6589c-345">**gx_scroll_down_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-345">**gx_scroll_down_pixelmap**</span></span>              | <span data-ttu-id="6589c-346">ID Pixelmap facoltativo.</span><span class="sxs-lookup"><span data-stu-id="6589c-346">Optional pixelmap ID.</span></span> <span data-ttu-id="6589c-347">Se questo ID Pixelmap è diverso da zero, la barra di scorrimento utilizza questo ID Pixelmap per creare il pulsante di fine della barra di scorrimento a destra/giù</span><span class="sxs-lookup"><span data-stu-id="6589c-347">If this pixelmap ID is not zero, the scrollbar uses this pixelmap ID to draw the scrollbar right/down end button</span></span> |
| <span data-ttu-id="6589c-348">**gx_scroll_thumb_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-348">**gx_scroll_thumb_color**</span></span>                | <span data-ttu-id="6589c-349">ID risorsa del colore usato per riempire il pulsante Thumb</span><span class="sxs-lookup"><span data-stu-id="6589c-349">Resource ID of color used to fill thumb button</span></span> |
| <span data-ttu-id="6589c-350">**gx_scroll_thumb_border_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-350">**gx_scroll_thumb_border_color**</span></span>         | <span data-ttu-id="6589c-351">ID risorsa del colore utilizzato per creare il bordo del pulsante Thumb</span><span class="sxs-lookup"><span data-stu-id="6589c-351">Resource ID of color used to draw the border of thumb button</span></span> | 
| <span data-ttu-id="6589c-352">**gx_scroll_button_color**</span><span class="sxs-lookup"><span data-stu-id="6589c-352">**gx_scroll_button_color**</span></span>               | <span data-ttu-id="6589c-353">ID risorsa del colore usato per riempire i pulsanti di fine della barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="6589c-353">Resource ID of color used to fill scrollbar end buttons</span></span> |

## <a name="gx_slider_info"></a><span data-ttu-id="6589c-354">GX_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="6589c-354">GX_SLIDER_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="6589c-355">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-355">Definition</span></span>

```c
typedef struct GX_SLIDER_INFO_STRUCT
{
    INT      gx_slider_info_min_val;
    INT      gx_slider_info_max_val;
    INT      gx_slider_info_current_val;
    INT      gx_slider_info_increment;
    GX_VALUE gx_slider_info_min_travel;
    GX_VALUE gx_slider_info_max_travel;
    GX_VALUE gx_slider_info_needle_width;
    GX_VALUE gx_slider_info_needle_height;
    GX_VALUE gx_slider_info_needle_inset;
    GX_VALUE gx_slider_info_needle_hotspot_offset;
} GX_SLIDER_INFO;
```

| <span data-ttu-id="6589c-356">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-356">Members</span></span> | <span data-ttu-id="6589c-357">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-357">Description</span></span> |
| --------------------------------------- | ------------------------------------------------------ |
| <span data-ttu-id="6589c-358">**gx_slider_info_min_val**</span><span class="sxs-lookup"><span data-stu-id="6589c-358">**gx_slider_info_min_val**</span></span>              | <span data-ttu-id="6589c-359">Valore minimo segnalato</span><span class="sxs-lookup"><span data-stu-id="6589c-359">Minimum reported value</span></span> |
| <span data-ttu-id="6589c-360">**gx_slider_info_max_val**</span><span class="sxs-lookup"><span data-stu-id="6589c-360">**gx_slider_info_max_val**</span></span>              | <span data-ttu-id="6589c-361">Valore massimo segnalato</span><span class="sxs-lookup"><span data-stu-id="6589c-361">Maximum reported value</span></span> |
| <span data-ttu-id="6589c-362">**gx_slider_info_current_value**</span><span class="sxs-lookup"><span data-stu-id="6589c-362">**gx_slider_info_current_value**</span></span>        | <span data-ttu-id="6589c-363">Valore corrente</span><span class="sxs-lookup"><span data-stu-id="6589c-363">Current value</span></span> |
| <span data-ttu-id="6589c-364">**gx_slider_info_min_travel**</span><span class="sxs-lookup"><span data-stu-id="6589c-364">**gx_slider_info_min_travel**</span></span>           | <span data-ttu-id="6589c-365">Limite di viaggio della lancetta</span><span class="sxs-lookup"><span data-stu-id="6589c-365">Needle travel limit</span></span> |
| <span data-ttu-id="6589c-366">**gx_slider_info_max_travel**</span><span class="sxs-lookup"><span data-stu-id="6589c-366">**gx_slider_info_max_travel**</span></span>           | <span data-ttu-id="6589c-367">Limite di viaggio della lancetta</span><span class="sxs-lookup"><span data-stu-id="6589c-367">Needle travel limit</span></span> |
| <span data-ttu-id="6589c-368">**gx_slider_info_needle_width**</span><span class="sxs-lookup"><span data-stu-id="6589c-368">**gx_slider_info_needle_width**</span></span>         | <span data-ttu-id="6589c-369">Spessore lancetta in pixel</span><span class="sxs-lookup"><span data-stu-id="6589c-369">Needle width in pixel</span></span> |
| <span data-ttu-id="6589c-370">**gx_slider_info_needle_height**</span><span class="sxs-lookup"><span data-stu-id="6589c-370">**gx_slider_info_needle_height**</span></span>        | <span data-ttu-id="6589c-371">Altezza lancetta in pixel</span><span class="sxs-lookup"><span data-stu-id="6589c-371">Needle height in pixel</span></span> |
|<span data-ttu-id="6589c-372">**gx_slider_info_needle_inset**</span><span class="sxs-lookup"><span data-stu-id="6589c-372">**gx_slider_info_needle_inset**</span></span>          | <span data-ttu-id="6589c-373">Posizione di estrazione della lancetta.</span><span class="sxs-lookup"><span data-stu-id="6589c-373">Needle draw position.</span></span> <span data-ttu-id="6589c-374">Se GX_STYLE_SLIDER_VERTICAL è impostato, viene usato per specificare l'offset dalla posizione iniziale di inizio del cursore al dispositivo di scorrimento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="6589c-374">If GX_STYLE_SLIDER_VERTICAL is set, used to specify the offset from the needle draw start position to the slider left.</span></span> <span data-ttu-id="6589c-375">Else, usato per specificare l'offset dalla posizione iniziale di inizio del cursore al dispositivo di scorrimento superiore.</span><span class="sxs-lookup"><span data-stu-id="6589c-375">Else, used to specify the offset from the needle draw start position to the slider top.</span></span> |
| <span data-ttu-id="6589c-376">**gx_slider_info_needle_hotspot_offset**</span><span class="sxs-lookup"><span data-stu-id="6589c-376">**gx_slider_info_needle_hotspot_offset**</span></span> | <span data-ttu-id="6589c-377">Hotpot_offset lancetta, usato per specificare l'offset dalla posizione iniziale di inizio del cursore all'area sensibile del dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="6589c-377">Needle hotpot_offset, used to specify the offset from the needle draw start position to the slider hotspot.</span></span> |

## <a name="gx_sprite_frame"></a><span data-ttu-id="6589c-378">GX_SPRITE_FRAME</span><span class="sxs-lookup"><span data-stu-id="6589c-378">GX_SPRITE_FRAME</span></span>

### <a name="definition"></a><span data-ttu-id="6589c-379">Definizione</span><span class="sxs-lookup"><span data-stu-id="6589c-379">Definition</span></span>

```c
typedef struct GX_SPRITE_FRAME_STRUCT
{
    GX_RESOURCE_ID gx_sprite_frame_pixelmap;
    GX_VALUE gx_sprite_frame_x_offset;
    GX_VALUE gx_sprite_frame_y_offset;
    UINT gx_sprite_frame_delay;
    UINT gx_sprite_frame_background_operation;
    UCHAR gx_sprite_frame_alpha;
} GX_SPRITE_FRAME;
```

| <span data-ttu-id="6589c-380">Membri</span><span class="sxs-lookup"><span data-stu-id="6589c-380">Members</span></span> | <span data-ttu-id="6589c-381">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6589c-381">Description</span></span> |
| ---------------------------------------- | ----------------------------------------------------- |
| <span data-ttu-id="6589c-382">**gx_sprite_frame_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="6589c-382">**gx_sprite_frame_pixelmap**</span></span>             | <span data-ttu-id="6589c-383">ID risorsa del Pixelmap da visualizzare per questo frame.</span><span class="sxs-lookup"><span data-stu-id="6589c-383">Resource ID of the pixelmap to be displayed for this frame.</span></span> <span data-ttu-id="6589c-384">L'ID può essere 0.</span><span class="sxs-lookup"><span data-stu-id="6589c-384">The ID can be 0.</span></span> |
| <span data-ttu-id="6589c-385">**gx_sprite_frame_x_offset**</span><span class="sxs-lookup"><span data-stu-id="6589c-385">**gx_sprite_frame_x_offset**</span></span>             | <span data-ttu-id="6589c-386">Offset dal widget sprite a sinistra per visualizzare il pixelmap</span><span class="sxs-lookup"><span data-stu-id="6589c-386">Offset from the sprite widget left to display the pixelmap</span></span> |
| <span data-ttu-id="6589c-387">**gx_sprite_frame_y_offset**</span><span class="sxs-lookup"><span data-stu-id="6589c-387">**gx_sprite_frame_y_offset**</span></span>             | <span data-ttu-id="6589c-388">Offset dal primo widget sprite per visualizzare il pixelmap</span><span class="sxs-lookup"><span data-stu-id="6589c-388">Offset from the sprite widget top to display the pixelmap</span></span> |
| <span data-ttu-id="6589c-389">**gx_sprite_frame_delay**</span><span class="sxs-lookup"><span data-stu-id="6589c-389">**gx_sprite_frame_delay**</span></span>                | <span data-ttu-id="6589c-390">Valore delay, nei cicli del timer GUIX, dopo aver visualizzato questo frame prima di avanzare al frame sprite successivo</span><span class="sxs-lookup"><span data-stu-id="6589c-390">Delay value, in GUIX timer ticks, after displaying this frame before advancing to the next sprite frame</span></span> |
| <span data-ttu-id="6589c-391">**gx_sprite_frame_background_operation**</span><span class="sxs-lookup"><span data-stu-id="6589c-391">**gx_sprite_frame_background_operation**</span></span> | <span data-ttu-id="6589c-392">Definire la modalità di cancellazione dello sfondo.</span><span class="sxs-lookup"><span data-stu-id="6589c-392">Define how the background should be erased.</span></span> <span data-ttu-id="6589c-393">I valori possibili per questo campo sono:</span><span class="sxs-lookup"><span data-stu-id="6589c-393">Possible values for this field are:</span></span><br /><span data-ttu-id="6589c-394">GX_SPRITE_BACKGROUND_NO_ACTION: nessun riempimento tra frame</span><span class="sxs-lookup"><span data-stu-id="6589c-394">GX_SPRITE_BACKGROUND_NO_ACTION: No fill between frames</span></span><br /><span data-ttu-id="6589c-395">GX_SPRITE_BACKGROUND_SOLID_FILL: ricreare lo sfondo dello sprite</span><span class="sxs-lookup"><span data-stu-id="6589c-395">GX_SPRITE_BACKGROUND_SOLID_FILL: Redraw sprite background</span></span><br /><span data-ttu-id="6589c-396">GX_SPRITE_BACKGROUND_RESTORE: ripristinare Pixelmap precedenti</span><span class="sxs-lookup"><span data-stu-id="6589c-396">GX_SPRITE_BACKGROUND_RESTORE: Restore previous pixelmap</span></span> |
| <span data-ttu-id="6589c-397">**gx_sprite_frame_alpha**</span><span class="sxs-lookup"><span data-stu-id="6589c-397">**gx_sprite_frame_alpha**</span></span>                | <span data-ttu-id="6589c-398">Valore alfa da aggiungere al Pixelmap visualizzato.</span><span class="sxs-lookup"><span data-stu-id="6589c-398">Alpha value to be added to the displayed pixelmap.</span></span> <span data-ttu-id="6589c-399">Il valore 255 specifica che non deve essere imposto alcun valore alfa aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="6589c-399">The value 255 specifies that no extra alpha value should be imposed.</span></span> <span data-ttu-id="6589c-400">Se Pixelmap include un canale alfa, questo canale alfa verrà aggiunto al valore alfa del frame.</span><span class="sxs-lookup"><span data-stu-id="6589c-400">If the pixelmap includes an alpha channel, this alpha channel will be added to the frame alpha value.</span></span> |
