---
title: Appendice I-strutture di informazioni GUIX
description: Informazioni sulle strutture di informazioni GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 03a10aeb65017befaf5e7b440046dbff9f9252ef
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823114"
---
# <a name="appendix-i---guix-information-structures"></a><span data-ttu-id="c4bf6-103">Appendice I-strutture di informazioni GUIX</span><span class="sxs-lookup"><span data-stu-id="c4bf6-103">Appendix I - GUIX Information Structures</span></span> 

## <a name="gx_bidi_text_info"></a><span data-ttu-id="c4bf6-104">GX_BIDI_TEXT_INFO</span><span class="sxs-lookup"><span data-stu-id="c4bf6-104">GX_BIDI_TEXT_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="c4bf6-105">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-105">Definition</span></span>

```c
typedef struct GX_BIDI_TEXT_INFO_STRUCT
{
    GX_STRING gx_bidi_text_info_text;
    GX_FONT  *gx_bidi_text_info_font;
    GX_VALUE  gx_bidi_text_info_display_width;
} GX_BIDI_TEXT_INFO;
```

### <a name="members"></a><span data-ttu-id="c4bf6-106">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-106">Members</span></span>

|                                    |                                                            |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="c4bf6-107">**gx_bidi_text_info_text**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-107">**gx_bidi_text_info_text**</span></span>               | <span data-ttu-id="c4bf6-108">Testo da riordinare</span><span class="sxs-lookup"><span data-stu-id="c4bf6-108">Text for reordering</span></span> |
| <span data-ttu-id="c4bf6-109">**gx_bidi_text_info_font**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-109">**gx_bidi_text_info_font**</span></span>               | <span data-ttu-id="c4bf6-110">Tipo di carattere utilizzato per visualizzare il testo, impostarlo su GX_NULL se non è necessaria l'interruzioni di riga</span><span class="sxs-lookup"><span data-stu-id="c4bf6-110">Font used to display text, set it to GX_NULL if line breaking is not needed</span></span> |
| <span data-ttu-id="c4bf6-111">**gx_bidi_text_info_display_width**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-111">**gx_bidi_text_info_display_width**</span></span>      | <span data-ttu-id="c4bf6-112">Larghezza disponibile per la visualizzazione, impostarla su-1 se non è necessaria l'interruzioni di riga</span><span class="sxs-lookup"><span data-stu-id="c4bf6-112">Available width for displaying, set it to -1 if line breaking is not needed</span></span> |

## <a name="gx_bidi_resolved_text_info"></a><span data-ttu-id="c4bf6-113">GX_BIDI_RESOLVED_TEXT_INFO</span><span class="sxs-lookup"><span data-stu-id="c4bf6-113">GX_BIDI_RESOLVED_TEXT_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="c4bf6-114">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-114">Definition</span></span>

```c
typedef struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT
{
    GX_STRING                                *gx_bidi_resolved_text_info_text;
    UINT                                      gx_bidi_resolved_text_info_total_lines;
    struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT *gx_bidi_resolved_text_info_next;
} GX_BIDI_RESOLVED_TEXT_INFO;
```

### <a name="members"></a><span data-ttu-id="c4bf6-115">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-115">Members</span></span>

|                                    |                                                            |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="c4bf6-116">**gx_bidi_resolved_text_info_text**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-116">**gx_bidi_resolved_text_info_text**</span></span>             | <span data-ttu-id="c4bf6-117">Puntatore alla matrice del testo bidi riordinato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-117">Pointer to the array of reordered bidi text</span></span> |
| <span data-ttu-id="c4bf6-118">**gx_bidi_resolved_text_info_total_lines**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-118">**gx_bidi_resolved_text_info_total_lines**</span></span>      | <span data-ttu-id="c4bf6-119">Righe totali del testo bidi risolto per un paragrafo</span><span class="sxs-lookup"><span data-stu-id="c4bf6-119">Total lines of resolved bidi text for one paragraph</span></span> |
| <span data-ttu-id="c4bf6-120">**gx_bidi_resolved_text_info_next**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-120">**gx_bidi_resolved_text_info_next**</span></span>             | <span data-ttu-id="c4bf6-121">Informazioni sul testo bidi risolto per il paragrafo successivo</span><span class="sxs-lookup"><span data-stu-id="c4bf6-121">Resolved bidi text information for the next paragraph</span></span> |

## <a name="gx_circular_gauge_info"></a><span data-ttu-id="c4bf6-122">GX_CIRCULAR_GAUGE_INFO</span><span class="sxs-lookup"><span data-stu-id="c4bf6-122">GX_CIRCULAR_GAUGE_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="c4bf6-123">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-123">Definition</span></span>

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
### <a name="members"></a><span data-ttu-id="c4bf6-124">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-124">Members</span></span>

|                                                  |                                              |
| ------------------------------------------------ | -------------------------------------------- |
| <span data-ttu-id="c4bf6-125">**gx_circular_gauge_info_animation_steps**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-125">**gx_circular_gauge_info_animation_steps**</span></span>       | <span data-ttu-id="c4bf6-126">Passaggi totali durante i quali viene spostata l'ago quando si passa dall'angolo della lancetta corrente a un angolo della lancetta appena assegnato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-126">Total steps the needle will travel through when moving from the current needle angle to a newly assigned needle angle</span></span> |
| <span data-ttu-id="c4bf6-127">**gx_circular_gauge_info_animation_delay**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-127">**gx_circular_gauge_info_animation_delay**</span></span>       | <span data-ttu-id="c4bf6-128">Il numero di tick dell'orologio GUIX di ritardo tra i passaggi di animazione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-128">The number of GUIX clock ticks to delay between animation steps</span></span> |
| <span data-ttu-id="c4bf6-129">**gx_circular_gauge_info_needle_xpos**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-129">**gx_circular_gauge_info_needle_xpos**</span></span>           | <span data-ttu-id="c4bf6-130">Distanza tra la parte sinistra del widget del misuratore e il centro di rotazione della lancetta del misuratore</span><span class="sxs-lookup"><span data-stu-id="c4bf6-130">The distance from the left of the gauge widget to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="c4bf6-131">**gx_circular_gauge_info_needle_ypos**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-131">**gx_circular_gauge_info_needle_ypos**</span></span>           | <span data-ttu-id="c4bf6-132">Distanza tra la parte superiore del widget del misuratore e il centro di rotazione della lancetta del misuratore</span><span class="sxs-lookup"><span data-stu-id="c4bf6-132">The distance from the top of the gauge widget to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="c4bf6-133">**gx_circular_gauge_info_needle_xcor**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-133">**gx_circular_gauge_info_needle_xcor**</span></span>           | <span data-ttu-id="c4bf6-134">Distanza tra il lato sinistro dell'immagine della lancetta e il centro di rotazione della lancetta del misuratore</span><span class="sxs-lookup"><span data-stu-id="c4bf6-134">The distance from the left of the needle image to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="c4bf6-135">**gx_circular_gauge_info_needle_ycor**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-135">**gx_circular_gauge_info_needle_ycor**</span></span>           | <span data-ttu-id="c4bf6-136">Distanza tra la parte superiore dell'immagine della lancetta e il centro di rotazione della lancetta del misuratore</span><span class="sxs-lookup"><span data-stu-id="c4bf6-136">The distance from the top of the needle image to the center-of-rotation of the gauge needle</span></span> |
| <span data-ttu-id="c4bf6-137">**gx_circular_gauge_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-137">**gx_circular_gauge_info_needle_pixelmap**</span></span>       | <span data-ttu-id="c4bf6-138">ID di risorsa di Pixelmap che verrà usato per creare la lancetta del misuratore.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-138">Resource ID of the pixelmap which will be used to draw the gauge needle.</span></span> <span data-ttu-id="c4bf6-139">Questa immagine verrà ruotata in base alle esigenze del widget misuratore per visualizzare la lancetta del misuratore in qualsiasi posizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-139">This image will be rotated as needed by the gauge widget to display the gauge needle in any position</span></span> |

<span data-ttu-id="c4bf6-140">Il diagramma seguente illustra le coordinate XPos, ypos e XCOR, ycor:</span><span class="sxs-lookup"><span data-stu-id="c4bf6-140">The diagram below illustrates the xpos, ypos, and xcor, ycor coordinates:</span></span>

![Diagramma delle coordinate Y e X della lancetta](./media/guix/image8.png)

## <a name="gx_line_chart_info"></a><span data-ttu-id="c4bf6-142">GX_LINE_CHART_INFO</span><span class="sxs-lookup"><span data-stu-id="c4bf6-142">GX_LINE_CHART_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="c4bf6-143">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-143">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="c4bf6-144">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-144">Members</span></span>

|                                    |                                                            |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="c4bf6-145">**gx_line_chart_min_val**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-145">**gx_line_chart_min_val**</span></span>          | <span data-ttu-id="c4bf6-146">Valore minimo dei dati, utilizzato per calcolare il ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-146">The minimum data value, which is used to calculate scaling</span></span>
| <span data-ttu-id="c4bf6-147">**gx_line_chart_max_val**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-147">**gx_line_chart_max_val**</span></span>          | <span data-ttu-id="c4bf6-148">Valore massimo dei dati, utilizzato per calcolare il ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-148">The maximum data value, which is used to calculate scaling</span></span> |
| <span data-ttu-id="c4bf6-149">**gx_line_chart_data**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-149">**gx_line_chart_data**</span></span>             | <span data-ttu-id="c4bf6-150">Puntatore a una matrice di valori interi.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-150">Pointer to an array of integer values.</span></span> <span data-ttu-id="c4bf6-151">Questi sono i valori integer tracciati dal widget grafico a linee</span><span class="sxs-lookup"><span data-stu-id="c4bf6-151">These are the integer values plotted by the line chart widget</span></span> |
| <span data-ttu-id="c4bf6-152">**gx_line_ <side> _margin**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-152">**gx_line_<side>_margin**</span></span>          | <span data-ttu-id="c4bf6-153">Offset dalla finestra del grafico esterna associata all'area di rendering del grafico effettiva.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-153">The offset from the chart window outer bound to the actual chart rendering area.</span></span> <span data-ttu-id="c4bf6-154">L'asse e la linea dati del grafico vengono sempre tracciati all'interno di questo limite interno, che consente all'applicazione di disegnare etichette e altre informazioni all'interno della finestra del grafico ma all'esterno dell'area del grafico char</span><span class="sxs-lookup"><span data-stu-id="c4bf6-154">The chart axis and data line are always plotted within this inner boundary, which allows the application to draw labels and other information inside the chart window but outside the char graphing area</span></span> |
| <span data-ttu-id="c4bf6-155">**gx_line_chart_max_data_count**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-155">**gx_line_chart_max_data_count**</span></span>   | <span data-ttu-id="c4bf6-156">Numero di valori di dati che possono essere presenti.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-156">The number of data values which may be present.</span></span> <span data-ttu-id="c4bf6-157">Questo parametro viene utilizzato per calcolare il ridimensionamento o l'intervallo dell'asse x per tracciare i punti dati.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-157">This parameter is used for calculating the x-axis scaling or interval for plotting data points.</span></span> |
| <span data-ttu-id="c4bf6-158">**gx_line_active_data_count**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-158">**gx_line_active_data_count**</span></span>      | <span data-ttu-id="c4bf6-159">Numero di valori di dati effettivamente presenti nella matrice di dati.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-159">The number of data values that actually present in the data array.</span></span> <span data-ttu-id="c4bf6-160">Un grafico a linee può essere ridimensionato in modo da creare un massimo di 100 valori, ad esempio, ma in ogni particolare aggiornamento può essere effettivamente presente un numero minore di valori di dati.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-160">A line chart may be scaled to draw a maximum of 100 values (for example), but on any particular update a smaller number of data values may actually be present.</span></span> |
| <span data-ttu-id="c4bf6-161">**gx_line_axis_line_width**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-161">**gx_line_axis_line_width**</span></span>        | <span data-ttu-id="c4bf6-162">Larghezza della linea utilizzata per creare l'asse orizzontale e verticale</span><span class="sxs-lookup"><span data-stu-id="c4bf6-162">Width of the line used to draw the horizontal and vertical axis</span></span> |
| <span data-ttu-id="c4bf6-163">**gx_line_data_line_width**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-163">**gx_line_data_line_width**</span></span>        | <span data-ttu-id="c4bf6-164">Larghezza della linea dati tracciato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-164">Width of the plotted data line</span></span> |
| <span data-ttu-id="c4bf6-165">**gx_line_chart_axis_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-165">**gx_line_chart_axis_color**</span></span>       | <span data-ttu-id="c4bf6-166">ID risorsa del colore utilizzato per creare le linee dell'asse</span><span class="sxs-lookup"><span data-stu-id="c4bf6-166">Resource ID of the color used to draw the axis lines</span></span> |
| <span data-ttu-id="c4bf6-167">**gx_line_chart_line_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-167">**gx_line_chart_line_color**</span></span>       | <span data-ttu-id="c4bf6-168">ID risorsa del colore utilizzato per tracciare la linea dati del grafico</span><span class="sxs-lookup"><span data-stu-id="c4bf6-168">Resource ID of the color used to draw the chart data line</span></span> |

## <a name="gx_mouse_cursor_info"></a><span data-ttu-id="c4bf6-169">GX_MOUSE_CURSOR_INFO</span><span class="sxs-lookup"><span data-stu-id="c4bf6-169">GX_MOUSE_CURSOR_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="c4bf6-170">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-170">Definition</span></span>

```c
typedef struct GX_MOUSE_CURSOR_INFO_STRUCT
{
    GX_RESOURCE_ID             gx_mouse_cursor_image_id;
    GX_VALUE                   gx_mouse_cursor_hotspot_x;
    GX_VALUE                   gx_mouse_cursor_hotspot_y;
} GX_MOUSE_CURSOR_INFO;
```

### <a name="members"></a><span data-ttu-id="c4bf6-171">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-171">Members</span></span>

|                                    |                                                            |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="c4bf6-172">**gx_mouse_cursor_image_id**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-172">**gx_mouse_cursor_image_id**</span></span>       | <span data-ttu-id="c4bf6-173">ID risorsa dell'immagine del mouse</span><span class="sxs-lookup"><span data-stu-id="c4bf6-173">Resource ID of the mouse image</span></span> |
| <span data-ttu-id="c4bf6-174">**gx_mouse_cursor_hotspot_x**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-174">**gx_mouse_cursor_hotspot_x**</span></span>      | <span data-ttu-id="c4bf6-175">Offset dal lato sinistro dell'immagine del mouse all'area sensibile dell'immagine del mouse</span><span class="sxs-lookup"><span data-stu-id="c4bf6-175">The offset from the left of the mouse image to the mouse image hotspot</span></span> |
| <span data-ttu-id="c4bf6-176">**gx_mouse_cursor_hotspot_y**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-176">**gx_mouse_cursor_hotspot_y**</span></span>      | <span data-ttu-id="c4bf6-177">Offset dalla parte superiore dell'immagine del mouse all'area sensibile dell'immagine del mouse</span><span class="sxs-lookup"><span data-stu-id="c4bf6-177">The offset from the top of the mouse image to the mouse image hotspot</span></span> |

## <a name="gx_pen_configuration"></a><span data-ttu-id="c4bf6-178">GX_PEN_CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="c4bf6-178">GX_PEN_CONFIGURATION</span></span> 

### <a name="definition"></a><span data-ttu-id="c4bf6-179">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-179">Definition</span></span>

```c
typedef struct GX_PEN_CONFIGURATION_STRUCT
{
    GX_FIXED_VAL     gx_pen_configuration_min_drag_dist;
    UINT             gx_pen_configuration_max_pen_speed_ticks;
}GX_PEN_CONFIGURATION;
```

### <a name="members"></a><span data-ttu-id="c4bf6-180">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-180">Members</span></span>

|                                              |                                                  |
| -------------------------------------------- | ------------------------------------------------ |
| <span data-ttu-id="c4bf6-181">**gx_pen_configuration_min_drag_dist**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-181">**gx_pen_configuration_min_drag_dist**</span></span>       | <span data-ttu-id="c4bf6-182">Lunghezza minima del trascinamento per ogni ciclo del timer GUIX per attivare un evento FLICK.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-182">The minimum drag distance per GUIX timer tick to trigger an FLICK event.</span></span> <span data-ttu-id="c4bf6-183">Chiamare GX_FIXED_VAL_MAKE per creare un valore del tipo di dati a virgola fissa</span><span class="sxs-lookup"><span data-stu-id="c4bf6-183">Call GX_FIXED_VAL_MAKE to make a fixed point data type value</span></span> |
| <span data-ttu-id="c4bf6-184">**gx_pen_configuration_max_pen_speed_ticks**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-184">**gx_pen_configuration_max_pen_speed_ticks**</span></span> | <span data-ttu-id="c4bf6-185">Velocità massima di trascinamento nei cicli del timer GUIX per attivare un evento FLICK</span><span class="sxs-lookup"><span data-stu-id="c4bf6-185">The maximum drag speed in GUIX timer ticks to trigger an FLICK event</span></span> | 

## <a name="gx_pixelmap_slider_info"></a><span data-ttu-id="c4bf6-186">GX_PIXELMAP_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="c4bf6-186">GX_PIXELMAP_SLIDER_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="c4bf6-187">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-187">Definition</span></span>

```c
typedef struct GX_PIXELMAP_SLIDER_INFO_STRUCT
{
    GX_RESOURCE_ID gx_pixelmap_slider_info_lower_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_upper_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_needle_pixelmap;
} GX_PIXELMAP_SLIDER_INFO;
```

### <a name="members"></a><span data-ttu-id="c4bf6-188">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-188">Members</span></span>

|                                                       |                                          |
| ----------------------------------------------------- | ---------------------------------------- |
| <span data-ttu-id="c4bf6-189">**gx_pixelmap_slider_info_lower_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-189">**gx_pixelmap_slider_info_lower_background_pixelmap**</span></span> | <span data-ttu-id="c4bf6-190">ID di risorsa di Pixelmap per riempire lo sfondo prima della lancetta.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-190">Resource ID of the pixelmap for filling the background before the needle.</span></span> <span data-ttu-id="c4bf6-191">Se il Pixelmap in background superiore non è impostato, viene usato per riempire lo sfondo sia prima che dopo la lancetta</span><span class="sxs-lookup"><span data-stu-id="c4bf6-191">If upper background pixelmap is not set, it’s used for filling background both before and after the needle</span></span> |
| <span data-ttu-id="c4bf6-192">**gx_pixelmap_slider_info_upper_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-192">**gx_pixelmap_slider_info_upper_background_pixelmap**</span></span> | <span data-ttu-id="c4bf6-193">ID di risorsa di Pixelmap per riempire lo sfondo dopo l'ago</span><span class="sxs-lookup"><span data-stu-id="c4bf6-193">Resource ID of the pixelmap for filling background after the needle</span></span> |
| <span data-ttu-id="c4bf6-194">**gx_pixelmap_slider_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-194">**gx_pixelmap_slider_info_needle_pixelmap**</span></span>           | <span data-ttu-id="c4bf6-195">ID risorsa della lancetta pixelmap</span><span class="sxs-lookup"><span data-stu-id="c4bf6-195">Resource ID of the needle pixelmap</span></span> |

## <a name="gx_progress_bar_info"></a><span data-ttu-id="c4bf6-196">GX_PROGRESS_BAR_INFO</span><span class="sxs-lookup"><span data-stu-id="c4bf6-196">GX_PROGRESS_BAR_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="c4bf6-197">**Definition**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-197">**Definition**</span></span>

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

### <a name="members"></a><span data-ttu-id="c4bf6-198">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-198">Members</span></span>

|                                              |                                                  |
| -------------------------------------------- | ------------------------------------------------ |
| <span data-ttu-id="c4bf6-199">**gx_progress_bar_info_min_val**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-199">**gx_progress_bar_info_min_val**</span></span>             | <span data-ttu-id="c4bf6-200">Valore minimo segnalato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-200">Minimum reported value</span></span> |
| <span data-ttu-id="c4bf6-201">**gx_progress_bar_info_max_val**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-201">**gx_progress_bar_info_max_val**</span></span>             | <span data-ttu-id="c4bf6-202">Valore massimo segnalato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-202">Maximum reported value</span></span> |
| <span data-ttu-id="c4bf6-203">**gx_progress_bar_info_current_val**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-203">**gx_progress_bar_info_current_val**</span></span>         | <span data-ttu-id="c4bf6-204">Valore corrente</span><span class="sxs-lookup"><span data-stu-id="c4bf6-204">Current value</span></span> |
| <span data-ttu-id="c4bf6-205">**gx_progress_bar_info_font_id**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-205">**gx_progress_bar_info_font_id**</span></span>             | <span data-ttu-id="c4bf6-206">ID risorsa del tipo di carattere, usato per creare il valore di testo facoltativo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-206">Resource ID of the font, used to draw the optional text value within the progress bar widget</span></span>      |
| <span data-ttu-id="c4bf6-207">**gx_progress_bar_normal_text_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-207">**gx_progress_bar_normal_text_color**</span></span>        | <span data-ttu-id="c4bf6-208">ID risorsa del colore del testo nello stato normale, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-208">Resource ID of the text color in normal state, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="c4bf6-209">**gx_progress_bar_selected_text_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-209">**gx_progress_bar_selected_text_color**</span></span>      | <span data-ttu-id="c4bf6-210">ID risorsa del colore del testo quando il widget ottiene lo stato attivo, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-210">Resource ID of the text color when the widget gain focus, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="c4bf6-211">**gx_progress_bar_disabled_text_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-211">**gx_progress_bar_disabled_text_color**</span></span>      | <span data-ttu-id="c4bf6-212">ID risorsa del colore del testo quando GX_STYLE_ENABLED non è attivo, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-212">Resource ID of the text color when GX_STYLE_ENABLED is not active, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="c4bf6-213">**gx_progress_bar_fill_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-213">**gx_progress_bar_fill_pixelmap**</span></span>            | <span data-ttu-id="c4bf6-214">ID risorsa di Pixelmap per riempimento in background</span><span class="sxs-lookup"><span data-stu-id="c4bf6-214">Resource ID of the pixelmap for background filling</span></span>|

## <a name="gx_radial_progress_bar_info"></a><span data-ttu-id="c4bf6-215">GX_RADIAL_PROGRESS_BAR_INFO</span><span class="sxs-lookup"><span data-stu-id="c4bf6-215">GX_RADIAL_PROGRESS_BAR_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="c4bf6-216">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-216">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="c4bf6-217">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-217">Members</span></span>

|                                                   |                                              |
| ------------------------------------------------- | -------------------------------------------- |
| <span data-ttu-id="c4bf6-218">**gx_radial_progress_bar_info_xcenter**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-218">**gx_radial_progress_bar_info_xcenter**</span></span>           | <span data-ttu-id="c4bf6-219">Posizione del widget nella coordinata x</span><span class="sxs-lookup"><span data-stu-id="c4bf6-219">Widget position in x coordinate</span></span> |
| <span data-ttu-id="c4bf6-220">**gx_radial_progress_bar_info_ycenter**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-220">**gx_radial_progress_bar_info_ycenter**</span></span>           | <span data-ttu-id="c4bf6-221">Posizione del widget nella coordinata y</span><span class="sxs-lookup"><span data-stu-id="c4bf6-221">Widget position in y coordinate</span></span>  |
| <span data-ttu-id="c4bf6-222">**gx_radial_progress_bar_info_radius**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-222">**gx_radial_progress_bar_info_radius**</span></span>            | <span data-ttu-id="c4bf6-223">Raggio del cerchio di avanzamento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-223">Radius of the progress circle</span></span> |
| <span data-ttu-id="c4bf6-224">**gx_radial_progress_bar_info_current_val**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-224">**gx_radial_progress_bar_info_current_val**</span></span>       | <span data-ttu-id="c4bf6-225">Il valore corrente, limitato all'intervallo [-360, 360], indica il Delta angolare tra la posizione di ancoraggio e il punto finale dell'arco superiore. Il valore negativo determina il disegno dell'arco in senso orario a partire dalla posizione di ancoraggio.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-225">Current value, limited to the range [-360, 360], indicates the angular delta between the anchor position and the end point of the upper arc. Negative value causes the arc to be drawn in a clockwise direction starting at the anchor position.</span></span> <span data-ttu-id="c4bf6-226">Il valore positivo fa in modo che l'arco venga disegnato in senso antiorario a partire dalla posizione di ancoraggio.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-226">Positive value causes the arc to be drawn in a counter-clockwise direction starting at the anchor position.</span></span> <span data-ttu-id="c4bf6-227">L'applicazione deve ridimensionare il valore di parola reale indicato per assegnare un valore angolare al widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-227">The application must scale the real-word value being indicated to assign an angular value to the progress bar widget</span></span> |
| <span data-ttu-id="c4bf6-228">**gx_radial_progress_bar_anchor_val**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-228">**gx_radial_progress_bar_anchor_val**</span></span>             | <span data-ttu-id="c4bf6-229">Angolo iniziale dell'arco di avanzamento superiore. Il valore è definito in termini di un numero intero con un grado di 0 che punta a destra e un grado di 90 indica la posizione verticale.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-229">Starting angle of the upper progress arc. The value is defined in terms of integer degree with 0 degree pointing to the right and 90 degree indicating straight up position.</span></span> |
| <span data-ttu-id="c4bf6-230">**gx_radial_progress_bar_font_id**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-230">**gx_radial_progress_bar_font_id**</span></span>                | <span data-ttu-id="c4bf6-231">ID risorsa del tipo di carattere utilizzato per creare il valore di testo facoltativo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-231">Resource ID of the font used to draw the optional text value within the progress bar widget</span></span> |
| <span data-ttu-id="c4bf6-232">**gx_radial_progress_bar_normal_text_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-232">**gx_radial_progress_bar_normal_text_color**</span></span>      | <span data-ttu-id="c4bf6-233">ID risorsa del colore del testo nello stato normale, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-233">Resource ID of the text color in normal state, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="c4bf6-234">**gx_radial_progress_bar_selected_text_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-234">**gx_radial_progress_bar_selected_text_color**</span></span>    |<span data-ttu-id="c4bf6-235">ID risorsa del colore del testo quando il widget ottiene lo stato attivo, usato per definire il disegno del testo facoltativo nel widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-235">Resource ID of the text color when widget gain focus, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="c4bf6-236">**gx_radial_progress_bar_disabled_text_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-236">**gx_radial_progress_bar_disabled_text_color**</span></span>    | <span data-ttu-id="c4bf6-237">ID risorsa del colore del testo quando GX_STYLE_ENABLED non è attivo, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-237">Resource ID of the text color when GX_STYLE_ENABLED is not active, used to define the optional text drawing within the progress bar widget</span></span> |
| <span data-ttu-id="c4bf6-238">**gx_radial_progress_bar_normal_brush_width**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-238">**gx_radial_progress_bar_normal_brush_width**</span></span>     | <span data-ttu-id="c4bf6-239">Larghezza del cerchio di avanzamento inferiore</span><span class="sxs-lookup"><span data-stu-id="c4bf6-239">Width of the lower progress circle</span></span> |
| <span data-ttu-id="c4bf6-240">**gx_radial_progress_bar_selected_brush_width**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-240">**gx_radial_progress_bar_selected_brush_width**</span></span>   | <span data-ttu-id="c4bf6-241">Larghezza dell'arco di avanzamento superiore, l'arco superiore può essere più piccolo, uguale o più ampio del cerchio inferiore</span><span class="sxs-lookup"><span data-stu-id="c4bf6-241">Width of the upper progress arc, the upper arc may be narrower, the same as, or wider than the lower circle</span></span> |
| <span data-ttu-id="c4bf6-242">**gx_radial_progress_bar_normal_brush_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-242">**gx_radial_progress_bar_normal_brush_color**</span></span>     | <span data-ttu-id="c4bf6-243">ID risorsa del colore per riempire il cerchio di avanzamento inferiore</span><span class="sxs-lookup"><span data-stu-id="c4bf6-243">Resource ID of the color to fill lower progress circle</span></span> |
| <span data-ttu-id="c4bf6-244">**gx_radial_progress_bar_selected_brush_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-244">**gx_radial_progress_bar_selected_brush_color**</span></span>   | <span data-ttu-id="c4bf6-245">ID risorsa del colore per riempire l'arco di avanzamento superiore</span><span class="sxs-lookup"><span data-stu-id="c4bf6-245">Resource ID of the color to fill upper progress arc</span></span> |

## <a name="gx_radial_slider_info"></a><span data-ttu-id="c4bf6-246">GX_RADIAL_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="c4bf6-246">GX_RADIAL_SLIDER_INFO</span></span> 

### <a name="definition"></a><span data-ttu-id="c4bf6-247">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-247">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="c4bf6-248">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-248">Members</span></span>

|                                               |                                                  |
| --------------------------------------------- | ------------------------------------------------ |
<span data-ttu-id="c4bf6-249">**gx_radial_slider_info_xcenter**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-249">**gx_radial_slider_info_xcenter**</span></span>               | <span data-ttu-id="c4bf6-250">Distanza tra la parte sinistra del widget del dispositivo di scorrimento e il centro di rotazione della lancetta del dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-250">Distance from the left of the slider widget to the center-of-rotation of the slider needle</span></span> |
| <span data-ttu-id="c4bf6-251">**gx_radial_slider_info_ycenter**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-251">**gx_radial_slider_info_ycenter**</span></span>             | <span data-ttu-id="c4bf6-252">Distanza dalla parte superiore del widget del dispositivo di scorrimento al centro di rotazione della lancetta del dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-252">Distance from the top of the slider widget to the center-of-rotation of the slider needle</span></span> |
| <span data-ttu-id="c4bf6-253">**gx_radial_slider_info_radius**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-253">**gx_radial_slider_info_radius**</span></span>              | <span data-ttu-id="c4bf6-254">Raggio del cerchio del dispositivo di scorrimento radiale</span><span class="sxs-lookup"><span data-stu-id="c4bf6-254">Radius of the radial slider circle</span></span> |
| <span data-ttu-id="c4bf6-255">**gx_radial_slider_info_track_width**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-255">**gx_radial_slider_info_track_width**</span></span>         | <span data-ttu-id="c4bf6-256">Larghezza della traccia del dispositivo di scorrimento radiale</span><span class="sxs-lookup"><span data-stu-id="c4bf6-256">Width of radial slider track</span></span> |
| <span data-ttu-id="c4bf6-257">**gx_radial_slider_info_current_angle**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-257">**gx_radial_slider_info_current_angle**</span></span>       | <span data-ttu-id="c4bf6-258">Angolo del dispositivo di scorrimento corrente</span><span class="sxs-lookup"><span data-stu-id="c4bf6-258">Current slider angle</span></span> |
| <span data-ttu-id="c4bf6-259">**gx_radial_slider_info_min_angle**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-259">**gx_radial_slider_info_min_angle**</span></span>           | <span data-ttu-id="c4bf6-260">Angolo minimo del dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-260">Minimum slider angle</span></span> |
| <span data-ttu-id="c4bf6-261">**gx_radial_slider_info_max_angle**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-261">**gx_radial_slider_info_max_angle**</span></span>           | <span data-ttu-id="c4bf6-262">Angolo massimo dispositivo di scorrimento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-262">Maximum slider angle</span></span> |
| <span data-ttu-id="c4bf6-263">**gx_radial_slider_info_angle_list**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-263">**gx_radial_slider_info_angle_list**</span></span>          | <span data-ttu-id="c4bf6-264">Elenco di valori angolo, definisce gli angoli di ancoraggio, se impostati, l'angolo del dispositivo di scorrimento può essere solo uno degli angoli di ancoraggio definiti</span><span class="sxs-lookup"><span data-stu-id="c4bf6-264">Angle value list, defines anchor angles, if set, slider angle can only be one of the defined anchor angles</span></span> |
| <span data-ttu-id="c4bf6-265">**gx_radial_slider_info_list_count**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-265">**gx_radial_slider_info_list_count**</span></span>          | <span data-ttu-id="c4bf6-266">Numero di angoli di ancoraggio</span><span class="sxs-lookup"><span data-stu-id="c4bf6-266">Number of anchor angles</span></span> |
| <span data-ttu-id="c4bf6-267">**gx_radial_slider_info_background_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-267">**gx_radial_slider_info_background_pixelmap**</span></span> | <span data-ttu-id="c4bf6-268">ID risorsa dello sfondo pixelmap</span><span class="sxs-lookup"><span data-stu-id="c4bf6-268">Resource ID of background pixelmap</span></span> |
| <span data-ttu-id="c4bf6-269">**gx_radial_slider_info_needle_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-269">**gx_radial_slider_info_needle_pixelmap**</span></span>     | <span data-ttu-id="c4bf6-270">ID risorsa dell'ago pixelmap</span><span class="sxs-lookup"><span data-stu-id="c4bf6-270">Resource ID of needle pixelmap</span></span> |

## <a name="gx_rectangle"></a><span data-ttu-id="c4bf6-271">GX_RECTANGLE</span><span class="sxs-lookup"><span data-stu-id="c4bf6-271">GX_RECTANGLE</span></span>

### <a name="definition"></a><span data-ttu-id="c4bf6-272">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-272">Definition</span></span>

```c
typedef struct GX_RECTANGLE_STRUCT
{
    GX_VALUE gx_rectangle_left;
    GX_VALUE gx_rectangle_top;
    GX_VALUE gx_rectangle_right;
    GX_VALUE gx_rectangle_bottom;
} GX_RECTANGLE;
```

### <a name="members"></a><span data-ttu-id="c4bf6-273">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-273">Members</span></span>

|                                  |                         |
| -------------------------------- | ------------------------|
| <span data-ttu-id="c4bf6-274">**gx_rectangle_left**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-274">**gx_rectangle_left**</span></span>            | <span data-ttu-id="c4bf6-275">A sinistra del rettangolo</span><span class="sxs-lookup"><span data-stu-id="c4bf6-275">Left of the rectangle</span></span>   |  
| <span data-ttu-id="c4bf6-276">**gx_rectangle_top**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-276">**gx_rectangle_top**</span></span>             | <span data-ttu-id="c4bf6-277">Parte superiore del rettangolo</span><span class="sxs-lookup"><span data-stu-id="c4bf6-277">Top of the rectangle</span></span>    | 
| <span data-ttu-id="c4bf6-278">**gx_rectangle_right**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-278">**gx_rectangle_right**</span></span>           | <span data-ttu-id="c4bf6-279">A destra del rettangolo</span><span class="sxs-lookup"><span data-stu-id="c4bf6-279">Right of the rectangle</span></span>  |
| <span data-ttu-id="c4bf6-280">**gx_rectangle_bottom**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-280">**gx_rectangle_bottom**</span></span>          | <span data-ttu-id="c4bf6-281">Parte inferiore del rettangolo</span><span class="sxs-lookup"><span data-stu-id="c4bf6-281">Bottom of the rectangle</span></span> |

## <a name="gx_rich_text_fonts"></a><span data-ttu-id="c4bf6-282">GX_RICH_TEXT_FONTS</span><span class="sxs-lookup"><span data-stu-id="c4bf6-282">GX_RICH_TEXT_FONTS</span></span> 

### <a name="definition"></a><span data-ttu-id="c4bf6-283">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-283">Definition</span></span>

```c
typedef struct GX_RICH_TEXT_FONTS_STRUCT
{
    GX_RESOURCE_ID             gx_rich_text_fonts_normal_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_italic_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_italic_id;
} GX_RICH_TEXT_FONTS;
```

### <a name="members"></a><span data-ttu-id="c4bf6-284">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-284">Members</span></span>

|                                    |                                                            |
| ---------------------------------- | ---------------------------------------------------------- |
| <span data-ttu-id="c4bf6-285">**gx_rich_text_fonts_normal_id**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-285">**gx_rich_text_fonts_normal_id**</span></span>   | <span data-ttu-id="c4bf6-286">ID risorsa del tipo di carattere testo normale</span><span class="sxs-lookup"><span data-stu-id="c4bf6-286">Resource ID of normal text font</span></span> |
| <span data-ttu-id="c4bf6-287">**gx_rich_text_fonts_bold_id**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-287">**gx_rich_text_fonts_bold_id**</span></span>     | <span data-ttu-id="c4bf6-288">ID risorsa del tipo di carattere testo in grassetto</span><span class="sxs-lookup"><span data-stu-id="c4bf6-288">Resource ID of bold text font</span></span> |
| <span data-ttu-id="c4bf6-289">**gx_rich_text_fonts_italic_id**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-289">**gx_rich_text_fonts_italic_id**</span></span>   | <span data-ttu-id="c4bf6-290">ID risorsa del tipo di carattere del testo in corsivo</span><span class="sxs-lookup"><span data-stu-id="c4bf6-290">Resource ID of italic text font</span></span> |
| <span data-ttu-id="c4bf6-291">**gx_rich_text_fonts_bold_italic_id**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-291">**gx_rich_text_fonts_bold_italic_id**</span></span> | <span data-ttu-id="c4bf6-292">ID risorsa del tipo di carattere testo in corsivo grassetto</span><span class="sxs-lookup"><span data-stu-id="c4bf6-292">Resource ID of bold italic text font</span></span> |

## <a name="gx_scroll_info"></a><span data-ttu-id="c4bf6-293">GX_SCROLL_INFO</span><span class="sxs-lookup"><span data-stu-id="c4bf6-293">GX_SCROLL_INFO</span></span> 
### <a name="definition"></a><span data-ttu-id="c4bf6-294">**Definition**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-294">**Definition**</span></span>

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

### <a name="members"></a><span data-ttu-id="c4bf6-295">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-295">Members</span></span>

|                         |                               |
| ----------------------- | ----------------------------- |
| <span data-ttu-id="c4bf6-296">**gx_scroll_value**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-296">**gx_scroll_value**</span></span>     | <span data-ttu-id="c4bf6-297">Posizione di scorrimento corrente</span><span class="sxs-lookup"><span data-stu-id="c4bf6-297">Current scroll position</span></span>       |
| <span data-ttu-id="c4bf6-298">**gx_scroll_minimum**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-298">**gx_scroll_minimum**</span></span>   | <span data-ttu-id="c4bf6-299">Posizione minima segnalata</span><span class="sxs-lookup"><span data-stu-id="c4bf6-299">Minimum reported position</span></span>     |
| <span data-ttu-id="c4bf6-300">**gx_scroll_maximum**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-300">**gx_scroll_maximum**</span></span>   | <span data-ttu-id="c4bf6-301">Posizione massima segnalata</span><span class="sxs-lookup"><span data-stu-id="c4bf6-301">Maximum reported position</span></span>     |
| <span data-ttu-id="c4bf6-302">**gx_scroll_visible**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-302">**gx_scroll_visible**</span></span>   | <span data-ttu-id="c4bf6-303">Intervallo visibile della finestra padre</span><span class="sxs-lookup"><span data-stu-id="c4bf6-303">Parent window visible range</span></span>   |
| <span data-ttu-id="c4bf6-304">**gx_scroll_increment**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-304">**gx_scroll_increment**</span></span> | <span data-ttu-id="c4bf6-305">Valore delta minimo barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-305">Scrollbar minimum delta value</span></span> |

## <a name="gx_scrollbar_appearance"></a><span data-ttu-id="c4bf6-306">GX_SCROLLBAR_APPEARANCE</span><span class="sxs-lookup"><span data-stu-id="c4bf6-306">GX_SCROLLBAR_APPEARANCE</span></span> 

### <a name="definition"></a><span data-ttu-id="c4bf6-307">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-307">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="c4bf6-308">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-308">Members</span></span>

|                                          |                                                       |
| ---------------------------------------- | ----------------------------------------------------- |
| <span data-ttu-id="c4bf6-309">**gx_scroll_width**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-309">**gx_scroll_width**</span></span>                      | <span data-ttu-id="c4bf6-310">Larghezza del widget della barra di scorrimento, in pixel</span><span class="sxs-lookup"><span data-stu-id="c4bf6-310">Width of the scrollbar widget, in pixels</span></span> |
| <span data-ttu-id="c4bf6-311">**gx_scroll_thumb_width**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-311">**gx_scroll_thumb_width**</span></span>                | <span data-ttu-id="c4bf6-312">Larghezza del pulsante Thumb che scorre la barra di scorrimento, in pixel.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-312">Width of the thumb button which slides on the scrollbar, in pixels.</span></span> <span data-ttu-id="c4bf6-313">Questo valore è in genere un numero di pixel inferiore alla lunghezza totale della barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-313">This value is usually some number of pixels less than the total scrollbar width</span></span> |
| <span data-ttu-id="c4bf6-314">**gx_scroll_thumb_travel_min**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-314">**gx_scroll_thumb_travel_min**</span></span>           | <span data-ttu-id="c4bf6-315">Offset dalla fine della barra di scorrimento al punto di partenza del pulsante Thumb minimo.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-315">Offset from the end of scrollbar to minimum thumb button travel point.</span></span> <span data-ttu-id="c4bf6-316">Questo limite può essere utilizzato per impedire che il pulsante Thumb venga spostata alla fine della barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-316">This limit can be used to prevent the thumb button from traveling to the very end of the scrollbar</span></span> |
| <span data-ttu-id="c4bf6-317">**gx_scroll_thumb_travel_max**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-317">**gx_scroll_thumb_travel_max**</span></span>           | <span data-ttu-id="c4bf6-318">Offset dalla fine della barra di scorrimento al punto di partenza del pulsante Thumb massimo.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-318">Offset from the end of scrollbar to maximum thumb button travel point.</span></span> <span data-ttu-id="c4bf6-319">Questo limite può essere utilizzato per impedire che il pulsante Thumb venga spostata alla fine della barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-319">This limit can be used to prevent the thumb button from traveling to the very end of the scrollbar</span></span> |
| <span data-ttu-id="c4bf6-320">**gx_scroll_thumb_border_style**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-320">**gx_scroll_thumb_border_style**</span></span>         | <span data-ttu-id="c4bf6-321">Stili del bordo del pulsante Thumb</span><span class="sxs-lookup"><span data-stu-id="c4bf6-321">Border styles of thumb button</span></span> |
| <span data-ttu-id="c4bf6-322">**gx_scroll_fill_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-322">**gx_scroll_fill_pixelmap**</span></span>              | <span data-ttu-id="c4bf6-323">ID Pixelmap facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-323">Optional pixelmap ID.</span></span> <span data-ttu-id="c4bf6-324">Se questo ID Pixelmap è diverso da zero, la barra di scorrimento utilizza questo Pixelmap per creare lo sfondo della barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-324">If this pixelmap ID is not zero, the scrollbar uses this pixelmap to draw the scrollbar background</span></span> |
| <span data-ttu-id="c4bf6-325">**gx_scroll_thumb_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-325">**gx_scroll_thumb_pixelmap**</span></span>             | <span data-ttu-id="c4bf6-326">ID Pixelmap facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-326">Optional pixelmap ID.</span></span> <span data-ttu-id="c4bf6-327">Se questo ID Pixelmap è diverso da zero, il pulsante Thumb della barra di scorrimento utilizza questo Pixelmap per disegnarsi</span><span class="sxs-lookup"><span data-stu-id="c4bf6-327">If this pixelmap ID is not zero, the scrollbar thumb button uses this pixelmap to draw itself</span></span> |
| <span data-ttu-id="c4bf6-328">**gx_scroll_up_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-328">**gx_scroll_up_pixelmap**</span></span>                | <span data-ttu-id="c4bf6-329">ID Pixelmap facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-329">Optional pixelmap ID.</span></span> <span data-ttu-id="c4bf6-330">Se questo ID Pixelmap è diverso da zero, la barra di scorrimento utilizza questo ID Pixelmap per creare il pulsante di fine della barra di scorrimento a sinistra</span><span class="sxs-lookup"><span data-stu-id="c4bf6-330">If this pixelmap ID is not zero, the scrollbar uses this pixelmap ID to draw the scrollbar left/up end button</span></span> |
| <span data-ttu-id="c4bf6-331">**gx_scroll_down_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-331">**gx_scroll_down_pixelmap**</span></span>              | <span data-ttu-id="c4bf6-332">ID Pixelmap facoltativo.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-332">Optional pixelmap ID.</span></span> <span data-ttu-id="c4bf6-333">Se questo ID Pixelmap è diverso da zero, la barra di scorrimento utilizza questo ID Pixelmap per creare il pulsante di fine della barra di scorrimento a destra/giù</span><span class="sxs-lookup"><span data-stu-id="c4bf6-333">If this pixelmap ID is not zero, the scrollbar uses this pixelmap ID to draw the scrollbar right/down end button</span></span> |
| <span data-ttu-id="c4bf6-334">**gx_scroll_thumb_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-334">**gx_scroll_thumb_color**</span></span>                | <span data-ttu-id="c4bf6-335">ID risorsa del colore usato per riempire il pulsante Thumb</span><span class="sxs-lookup"><span data-stu-id="c4bf6-335">Resource ID of color used to fill thumb button</span></span> |
| <span data-ttu-id="c4bf6-336">**gx_scroll_thumb_border_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-336">**gx_scroll_thumb_border_color**</span></span>         | <span data-ttu-id="c4bf6-337">ID risorsa del colore utilizzato per creare il bordo del pulsante Thumb</span><span class="sxs-lookup"><span data-stu-id="c4bf6-337">Resource ID of color used to draw the border of thumb button</span></span> | 
| <span data-ttu-id="c4bf6-338">**gx_scroll_button_color**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-338">**gx_scroll_button_color**</span></span>               | <span data-ttu-id="c4bf6-339">ID risorsa del colore usato per riempire i pulsanti di fine della barra di scorrimento</span><span class="sxs-lookup"><span data-stu-id="c4bf6-339">Resource ID of color used to fill scrollbar end buttons</span></span> |

## <a name="gx_slider_info"></a><span data-ttu-id="c4bf6-340">GX_SLIDER_INFO</span><span class="sxs-lookup"><span data-stu-id="c4bf6-340">GX_SLIDER_INFO</span></span>

### <a name="definition"></a><span data-ttu-id="c4bf6-341">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-341">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="c4bf6-342">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-342">Members</span></span>

|                                         |                                                        |
| --------------------------------------- | ------------------------------------------------------ |
| <span data-ttu-id="c4bf6-343">**gx_slider_info_min_val**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-343">**gx_slider_info_min_val**</span></span>              | <span data-ttu-id="c4bf6-344">Valore minimo segnalato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-344">Minimum reported value</span></span> |
| <span data-ttu-id="c4bf6-345">**gx_slider_info_max_val**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-345">**gx_slider_info_max_val**</span></span>              | <span data-ttu-id="c4bf6-346">Valore massimo segnalato</span><span class="sxs-lookup"><span data-stu-id="c4bf6-346">Maximum reported value</span></span> |
| <span data-ttu-id="c4bf6-347">**gx_slider_info_current_value**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-347">**gx_slider_info_current_value**</span></span>        | <span data-ttu-id="c4bf6-348">Valore corrente</span><span class="sxs-lookup"><span data-stu-id="c4bf6-348">Current value</span></span> |
| <span data-ttu-id="c4bf6-349">**gx_slider_info_min_travel**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-349">**gx_slider_info_min_travel**</span></span>           | <span data-ttu-id="c4bf6-350">Limite di viaggio della lancetta</span><span class="sxs-lookup"><span data-stu-id="c4bf6-350">Needle travel limit</span></span> |
| <span data-ttu-id="c4bf6-351">**gx_slider_info_max_travel**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-351">**gx_slider_info_max_travel**</span></span>           | <span data-ttu-id="c4bf6-352">Limite di viaggio della lancetta</span><span class="sxs-lookup"><span data-stu-id="c4bf6-352">Needle travel limit</span></span> |
| <span data-ttu-id="c4bf6-353">**gx_slider_info_needle_width**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-353">**gx_slider_info_needle_width**</span></span>         | <span data-ttu-id="c4bf6-354">Spessore lancetta in pixel</span><span class="sxs-lookup"><span data-stu-id="c4bf6-354">Needle width in pixel</span></span> |
| <span data-ttu-id="c4bf6-355">**gx_slider_info_needle_height**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-355">**gx_slider_info_needle_height**</span></span>        | <span data-ttu-id="c4bf6-356">Altezza lancetta in pixel</span><span class="sxs-lookup"><span data-stu-id="c4bf6-356">Needle height in pixel</span></span> |
|<span data-ttu-id="c4bf6-357">**gx_slider_info_needle_inset**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-357">**gx_slider_info_needle_inset**</span></span>          | <span data-ttu-id="c4bf6-358">Posizione di estrazione della lancetta.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-358">Needle draw position.</span></span> <span data-ttu-id="c4bf6-359">Se GX_STYLE_SLIDER_VERTICAL è impostato, viene usato per specificare l'offset dalla posizione iniziale di inizio del cursore al dispositivo di scorrimento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-359">If GX_STYLE_SLIDER_VERTICAL is set, used to specify the offset from the needle draw start position to the slider left.</span></span> <span data-ttu-id="c4bf6-360">Else, usato per specificare l'offset dalla posizione iniziale di inizio del cursore al dispositivo di scorrimento superiore.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-360">Else, used to specify the offset from the needle draw start position to the slider top.</span></span> |
| <span data-ttu-id="c4bf6-361">**gx_slider_info_needle_hotspot_offset**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-361">**gx_slider_info_needle_hotspot_offset**</span></span> | <span data-ttu-id="c4bf6-362">Hotpot_offset lancetta, usato per specificare l'offset dalla posizione iniziale di inizio del cursore all'area sensibile del dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-362">Needle hotpot_offset, used to specify the offset from the needle draw start position to the slider hotspot.</span></span> |

## <a name="gx_sprite_frame"></a><span data-ttu-id="c4bf6-363">GX_SPRITE_FRAME</span><span class="sxs-lookup"><span data-stu-id="c4bf6-363">GX_SPRITE_FRAME</span></span>

### <a name="definition"></a><span data-ttu-id="c4bf6-364">Definizione</span><span class="sxs-lookup"><span data-stu-id="c4bf6-364">Definition</span></span>

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

### <a name="members"></a><span data-ttu-id="c4bf6-365">Membri</span><span class="sxs-lookup"><span data-stu-id="c4bf6-365">Members</span></span>

|                                          |                                                       |
| ---------------------------------------- | ----------------------------------------------------- |
| <span data-ttu-id="c4bf6-366">**gx_sprite_frame_pixelmap**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-366">**gx_sprite_frame_pixelmap**</span></span>             | <span data-ttu-id="c4bf6-367">ID risorsa del Pixelmap da visualizzare per questo frame.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-367">Resource ID of the pixelmap to be displayed for this frame.</span></span> <span data-ttu-id="c4bf6-368">L'ID può essere 0.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-368">The ID can be 0.</span></span> |
| <span data-ttu-id="c4bf6-369">**gx_sprite_frame_x_offset**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-369">**gx_sprite_frame_x_offset**</span></span>             | <span data-ttu-id="c4bf6-370">Offset dal widget sprite a sinistra per visualizzare il pixelmap</span><span class="sxs-lookup"><span data-stu-id="c4bf6-370">Offset from the sprite widget left to display the pixelmap</span></span> |
| <span data-ttu-id="c4bf6-371">**gx_sprite_frame_y_offset**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-371">**gx_sprite_frame_y_offset**</span></span>             | <span data-ttu-id="c4bf6-372">Offset dal primo widget sprite per visualizzare il pixelmap</span><span class="sxs-lookup"><span data-stu-id="c4bf6-372">Offset from the sprite widget top to display the pixelmap</span></span> |
| <span data-ttu-id="c4bf6-373">**gx_sprite_frame_delay**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-373">**gx_sprite_frame_delay**</span></span>                | <span data-ttu-id="c4bf6-374">Valore delay, nei cicli del timer GUIX, dopo aver visualizzato questo frame prima di avanzare al frame sprite successivo</span><span class="sxs-lookup"><span data-stu-id="c4bf6-374">Delay value, in GUIX timer ticks, after displaying this frame before advancing to the next sprite frame</span></span> |
| <span data-ttu-id="c4bf6-375">**gx_sprite_frame_background_operation**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-375">**gx_sprite_frame_background_operation**</span></span> | <span data-ttu-id="c4bf6-376">Definire la modalità di cancellazione dello sfondo.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-376">Define how the background should be erased.</span></span> <span data-ttu-id="c4bf6-377">I valori possibili per questo campo sono:</span><span class="sxs-lookup"><span data-stu-id="c4bf6-377">Possible values for this field are:</span></span><br /><span data-ttu-id="c4bf6-378">GX_SPRITE_BACKGROUND_NO_ACTION: nessun riempimento tra frame</span><span class="sxs-lookup"><span data-stu-id="c4bf6-378">GX_SPRITE_BACKGROUND_NO_ACTION: No fill between frames</span></span><br /><span data-ttu-id="c4bf6-379">GX_SPRITE_BACKGROUND_SOLID_FILL: ricreare lo sfondo dello sprite</span><span class="sxs-lookup"><span data-stu-id="c4bf6-379">GX_SPRITE_BACKGROUND_SOLID_FILL: Redraw sprite background</span></span><br /><span data-ttu-id="c4bf6-380">GX_SPRITE_BACKGROUND_RESTORE: ripristinare Pixelmap precedenti</span><span class="sxs-lookup"><span data-stu-id="c4bf6-380">GX_SPRITE_BACKGROUND_RESTORE: Restore previous pixelmap</span></span> |
| <span data-ttu-id="c4bf6-381">**gx_sprite_frame_alpha**</span><span class="sxs-lookup"><span data-stu-id="c4bf6-381">**gx_sprite_frame_alpha**</span></span>                | <span data-ttu-id="c4bf6-382">Valore alfa da aggiungere al Pixelmap visualizzato.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-382">Alpha value to be added to the displayed pixelmap.</span></span> <span data-ttu-id="c4bf6-383">Il valore 255 specifica che non deve essere imposto alcun valore alfa aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-383">The value 255 specifies that no extra alpha value should be imposed.</span></span> <span data-ttu-id="c4bf6-384">Se Pixelmap include un canale alfa, questo canale alfa verrà aggiunto al valore alfa del frame.</span><span class="sxs-lookup"><span data-stu-id="c4bf6-384">If the pixelmap includes an alpha channel, this alpha channel will be added to the frame alpha value.</span></span> |
