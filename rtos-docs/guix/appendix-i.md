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
# <a name="appendix-i---guix-information-structures"></a>Appendice I-strutture di informazioni GUIX 

## <a name="gx_bidi_text_info"></a>GX_BIDI_TEXT_INFO 

### <a name="definition"></a>Definizione

```c
typedef struct GX_BIDI_TEXT_INFO_STRUCT
{
    GX_STRING gx_bidi_text_info_text;
    GX_FONT  *gx_bidi_text_info_font;
    GX_VALUE  gx_bidi_text_info_display_width;
} GX_BIDI_TEXT_INFO;
```
| Membri | Descrizione |
| ---------------------------------- | ---------------------------------------------------------- |
| **gx_bidi_text_info_text**               | Testo da riordinare |
| **gx_bidi_text_info_font**               | Tipo di carattere utilizzato per visualizzare il testo, impostarlo su GX_NULL se non è necessaria l'interruzioni di riga |
| **gx_bidi_text_info_display_width**      | Larghezza disponibile per la visualizzazione, impostarla su-1 se non è necessaria l'interruzioni di riga |

## <a name="gx_bidi_resolved_text_info"></a>GX_BIDI_RESOLVED_TEXT_INFO 

### <a name="definition"></a>Definizione

```c
typedef struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT
{
    GX_STRING                                *gx_bidi_resolved_text_info_text;
    UINT                                      gx_bidi_resolved_text_info_total_lines;
    struct GX_BIDI_RESOLVED_TEXT_INFO_STRUCT *gx_bidi_resolved_text_info_next;
} GX_BIDI_RESOLVED_TEXT_INFO;
```

| Membri | Descrizione |
| ---------------------------------- | ---------------------------------------------------------- |
| **gx_bidi_resolved_text_info_text**             | Puntatore alla matrice del testo bidi riordinato |
| **gx_bidi_resolved_text_info_total_lines**      | Righe totali del testo bidi risolto per un paragrafo |
| **gx_bidi_resolved_text_info_next**             | Informazioni sul testo bidi risolto per il paragrafo successivo |

## <a name="gx_circular_gauge_info"></a>GX_CIRCULAR_GAUGE_INFO

### <a name="definition"></a>Definizione

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

| Membri | Descrizione |
| ------------------------------------------------ | -------------------------------------------- |
| **gx_circular_gauge_info_animation_steps**       | Passaggi totali durante i quali viene spostata l'ago quando si passa dall'angolo della lancetta corrente a un angolo della lancetta appena assegnato |
| **gx_circular_gauge_info_animation_delay**       | Il numero di tick dell'orologio GUIX di ritardo tra i passaggi di animazione |
| **gx_circular_gauge_info_needle_xpos**           | Distanza tra la parte sinistra del widget del misuratore e il centro di rotazione della lancetta del misuratore |
| **gx_circular_gauge_info_needle_ypos**           | Distanza tra la parte superiore del widget del misuratore e il centro di rotazione della lancetta del misuratore |
| **gx_circular_gauge_info_needle_xcor**           | Distanza tra il lato sinistro dell'immagine della lancetta e il centro di rotazione della lancetta del misuratore |
| **gx_circular_gauge_info_needle_ycor**           | Distanza tra la parte superiore dell'immagine della lancetta e il centro di rotazione della lancetta del misuratore |
| **gx_circular_gauge_info_needle_pixelmap**       | ID di risorsa di Pixelmap che verrà usato per creare la lancetta del misuratore. Questa immagine verrà ruotata in base alle esigenze del widget misuratore per visualizzare la lancetta del misuratore in qualsiasi posizione |

Il diagramma seguente illustra le coordinate XPos, ypos e XCOR, ycor:

![Diagramma delle coordinate Y e X della lancetta](./media/guix/image8.png)

## <a name="gx_line_chart_info"></a>GX_LINE_CHART_INFO

### <a name="definition"></a>Definizione

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

| Membri | Descrizione |
| ---------------------------------- | ---------------------------------------------------------- |
| **gx_line_chart_min_val**          | Valore minimo dei dati, utilizzato per calcolare il ridimensionamento
| **gx_line_chart_max_val**          | Valore massimo dei dati, utilizzato per calcolare il ridimensionamento |
| **gx_line_chart_data**             | Puntatore a una matrice di valori interi. Questi sono i valori integer tracciati dal widget grafico a linee |
| **gx_line_ <side> _margin**          | Offset dalla finestra del grafico esterna associata all'area di rendering del grafico effettiva. L'asse e la linea dati del grafico vengono sempre tracciati all'interno di questo limite interno, che consente all'applicazione di disegnare etichette e altre informazioni all'interno della finestra del grafico ma all'esterno dell'area del grafico char |
| **gx_line_chart_max_data_count**   | Numero di valori di dati che possono essere presenti. Questo parametro viene utilizzato per calcolare il ridimensionamento o l'intervallo dell'asse x per tracciare i punti dati. |
| **gx_line_active_data_count**      | Numero di valori di dati effettivamente presenti nella matrice di dati. Un grafico a linee può essere ridimensionato in modo da creare un massimo di 100 valori, ad esempio, ma in ogni particolare aggiornamento può essere effettivamente presente un numero minore di valori di dati. |
| **gx_line_axis_line_width**        | Larghezza della linea utilizzata per creare l'asse orizzontale e verticale |
| **gx_line_data_line_width**        | Larghezza della linea dati tracciato |
| **gx_line_chart_axis_color**       | ID risorsa del colore utilizzato per creare le linee dell'asse |
| **gx_line_chart_line_color**       | ID risorsa del colore utilizzato per tracciare la linea dati del grafico |

## <a name="gx_mouse_cursor_info"></a>GX_MOUSE_CURSOR_INFO 

### <a name="definition"></a>Definizione

```c
typedef struct GX_MOUSE_CURSOR_INFO_STRUCT
{
    GX_RESOURCE_ID             gx_mouse_cursor_image_id;
    GX_VALUE                   gx_mouse_cursor_hotspot_x;
    GX_VALUE                   gx_mouse_cursor_hotspot_y;
} GX_MOUSE_CURSOR_INFO;
```

| Membri | Descrizione |
| ---------------------------------- | ---------------------------------------------------------- |
| **gx_mouse_cursor_image_id**       | ID risorsa dell'immagine del mouse |
| **gx_mouse_cursor_hotspot_x**      | Offset dal lato sinistro dell'immagine del mouse all'area sensibile dell'immagine del mouse |
| **gx_mouse_cursor_hotspot_y**      | Offset dalla parte superiore dell'immagine del mouse all'area sensibile dell'immagine del mouse |

## <a name="gx_pen_configuration"></a>GX_PEN_CONFIGURATION 

### <a name="definition"></a>Definizione

```c
typedef struct GX_PEN_CONFIGURATION_STRUCT
{
    GX_FIXED_VAL     gx_pen_configuration_min_drag_dist;
    UINT             gx_pen_configuration_max_pen_speed_ticks;
}GX_PEN_CONFIGURATION;
```

| Membri | Descrizione |
| -------------------------------------------- | ------------------------------------------------ |
| **gx_pen_configuration_min_drag_dist**       | Lunghezza minima del trascinamento per ogni ciclo del timer GUIX per attivare un evento FLICK. Chiamare GX_FIXED_VAL_MAKE per creare un valore del tipo di dati a virgola fissa |
| **gx_pen_configuration_max_pen_speed_ticks** | Velocità massima di trascinamento nei cicli del timer GUIX per attivare un evento FLICK | 

## <a name="gx_pixelmap_slider_info"></a>GX_PIXELMAP_SLIDER_INFO 

### <a name="definition"></a>Definizione

```c
typedef struct GX_PIXELMAP_SLIDER_INFO_STRUCT
{
    GX_RESOURCE_ID gx_pixelmap_slider_info_lower_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_upper_background_pixelmap;
    GX_RESOURCE_ID gx_pixelmap_slider_info_needle_pixelmap;
} GX_PIXELMAP_SLIDER_INFO;
```

| Membri | Descrizione |
| ----------------------------------------------------- | ---------------------------------------- |
| **gx_pixelmap_slider_info_lower_background_pixelmap** | ID di risorsa di Pixelmap per riempire lo sfondo prima della lancetta. Se il Pixelmap in background superiore non è impostato, viene usato per riempire lo sfondo sia prima che dopo la lancetta |
| **gx_pixelmap_slider_info_upper_background_pixelmap** | ID di risorsa di Pixelmap per riempire lo sfondo dopo l'ago |
| **gx_pixelmap_slider_info_needle_pixelmap**           | ID risorsa della lancetta pixelmap |

## <a name="gx_progress_bar_info"></a>GX_PROGRESS_BAR_INFO 

### <a name="definition"></a>**Definition**

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

| Membri | Descrizione |
| -------------------------------------------- | ------------------------------------------------ |
| **gx_progress_bar_info_min_val**             | Valore minimo segnalato |
| **gx_progress_bar_info_max_val**             | Valore massimo segnalato |
| **gx_progress_bar_info_current_val**         | Valore corrente |
| **gx_progress_bar_info_font_id**             | ID risorsa del tipo di carattere, usato per creare il valore di testo facoltativo all'interno del widget indicatore di stato      |
| **gx_progress_bar_normal_text_color**        | ID risorsa del colore del testo nello stato normale, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato |
| **gx_progress_bar_selected_text_color**      | ID risorsa del colore del testo quando il widget ottiene lo stato attivo, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato |
| **gx_progress_bar_disabled_text_color**      | ID risorsa del colore del testo quando GX_STYLE_ENABLED non è attivo, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato |
| **gx_progress_bar_fill_pixelmap**            | ID risorsa di Pixelmap per riempimento in background|

## <a name="gx_radial_progress_bar_info"></a>GX_RADIAL_PROGRESS_BAR_INFO

### <a name="definition"></a>Definizione

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

| Membri | Descrizione |
| ------------------------------------------------- | -------------------------------------------- |
| **gx_radial_progress_bar_info_xcenter**           | Posizione del widget nella coordinata x |
| **gx_radial_progress_bar_info_ycenter**           | Posizione del widget nella coordinata y  |
| **gx_radial_progress_bar_info_radius**            | Raggio del cerchio di avanzamento |
| **gx_radial_progress_bar_info_current_val**       | Il valore corrente, limitato all'intervallo [-360, 360], indica il Delta angolare tra la posizione di ancoraggio e il punto finale dell'arco superiore. Il valore negativo determina il disegno dell'arco in senso orario a partire dalla posizione di ancoraggio. Il valore positivo fa in modo che l'arco venga disegnato in senso antiorario a partire dalla posizione di ancoraggio. L'applicazione deve ridimensionare il valore di parola reale indicato per assegnare un valore angolare al widget indicatore di stato |
| **gx_radial_progress_bar_anchor_val**             | Angolo iniziale dell'arco di avanzamento superiore. Il valore è definito in termini di un numero intero con un grado di 0 che punta a destra e un grado di 90 indica la posizione verticale. |
| **gx_radial_progress_bar_font_id**                | ID risorsa del tipo di carattere utilizzato per creare il valore di testo facoltativo all'interno del widget indicatore di stato |
| **gx_radial_progress_bar_normal_text_color**      | ID risorsa del colore del testo nello stato normale, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato |
| **gx_radial_progress_bar_selected_text_color**    |ID risorsa del colore del testo quando il widget ottiene lo stato attivo, usato per definire il disegno del testo facoltativo nel widget indicatore di stato |
| **gx_radial_progress_bar_disabled_text_color**    | ID risorsa del colore del testo quando GX_STYLE_ENABLED non è attivo, usato per definire il disegno facoltativo del testo all'interno del widget indicatore di stato |
| **gx_radial_progress_bar_normal_brush_width**     | Larghezza del cerchio di avanzamento inferiore |
| **gx_radial_progress_bar_selected_brush_width**   | Larghezza dell'arco di avanzamento superiore, l'arco superiore può essere più piccolo, uguale o più ampio del cerchio inferiore |
| **gx_radial_progress_bar_normal_brush_color**     | ID risorsa del colore per riempire il cerchio di avanzamento inferiore |
| **gx_radial_progress_bar_selected_brush_color**   | ID risorsa del colore per riempire l'arco di avanzamento superiore |

## <a name="gx_radial_slider_info"></a>GX_RADIAL_SLIDER_INFO 

### <a name="definition"></a>Definizione

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

| Membri | Descrizione |
| --------------------------------------------- | ------------------------------------------------ |
**gx_radial_slider_info_xcenter**               | Distanza tra la parte sinistra del widget del dispositivo di scorrimento e il centro di rotazione della lancetta del dispositivo di scorrimento |
| **gx_radial_slider_info_ycenter**             | Distanza dalla parte superiore del widget del dispositivo di scorrimento al centro di rotazione della lancetta del dispositivo di scorrimento |
| **gx_radial_slider_info_radius**              | Raggio del cerchio del dispositivo di scorrimento radiale |
| **gx_radial_slider_info_track_width**         | Larghezza della traccia del dispositivo di scorrimento radiale |
| **gx_radial_slider_info_current_angle**       | Angolo del dispositivo di scorrimento corrente |
| **gx_radial_slider_info_min_angle**           | Angolo minimo del dispositivo di scorrimento |
| **gx_radial_slider_info_max_angle**           | Angolo massimo dispositivo di scorrimento |
| **gx_radial_slider_info_angle_list**          | Elenco di valori angolo, definisce gli angoli di ancoraggio, se impostati, l'angolo del dispositivo di scorrimento può essere solo uno degli angoli di ancoraggio definiti |
| **gx_radial_slider_info_list_count**          | Numero di angoli di ancoraggio |
| **gx_radial_slider_info_background_pixelmap** | ID risorsa dello sfondo pixelmap |
| **gx_radial_slider_info_needle_pixelmap**     | ID risorsa dell'ago pixelmap |

## <a name="gx_rectangle"></a>GX_RECTANGLE

### <a name="definition"></a>Definizione

```c
typedef struct GX_RECTANGLE_STRUCT
{
    GX_VALUE gx_rectangle_left;
    GX_VALUE gx_rectangle_top;
    GX_VALUE gx_rectangle_right;
    GX_VALUE gx_rectangle_bottom;
} GX_RECTANGLE;
```

| Membri | Descrizione |
| -------------------------------- | ------------------------|
| **gx_rectangle_left**            | A sinistra del rettangolo   |  
| **gx_rectangle_top**             | Parte superiore del rettangolo    | 
| **gx_rectangle_right**           | A destra del rettangolo  |
| **gx_rectangle_bottom**          | Parte inferiore del rettangolo |

## <a name="gx_rich_text_fonts"></a>GX_RICH_TEXT_FONTS 

### <a name="definition"></a>Definizione

```c
typedef struct GX_RICH_TEXT_FONTS_STRUCT
{
    GX_RESOURCE_ID             gx_rich_text_fonts_normal_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_italic_id;
    GX_RESOURCE_ID             gx_rich_text_fonts_bold_italic_id;
} GX_RICH_TEXT_FONTS;
```

| Membri | Descrizione |
| ---------------------------------- | ---------------------------------------------------------- |
| **gx_rich_text_fonts_normal_id**   | ID risorsa del tipo di carattere testo normale |
| **gx_rich_text_fonts_bold_id**     | ID risorsa del tipo di carattere testo in grassetto |
| **gx_rich_text_fonts_italic_id**   | ID risorsa del tipo di carattere del testo in corsivo |
| **gx_rich_text_fonts_bold_italic_id** | ID risorsa del tipo di carattere testo in corsivo grassetto |

## <a name="gx_scroll_info"></a>GX_SCROLL_INFO 
### <a name="definition"></a>**Definition**

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

| Membri | Descrizione |
| ----------------------- | ----------------------------- |
| **gx_scroll_value**     | Posizione di scorrimento corrente       |
| **gx_scroll_minimum**   | Posizione minima segnalata     |
| **gx_scroll_maximum**   | Posizione massima segnalata     |
| **gx_scroll_visible**   | Intervallo visibile della finestra padre   |
| **gx_scroll_increment** | Valore delta minimo barra di scorrimento |

## <a name="gx_scrollbar_appearance"></a>GX_SCROLLBAR_APPEARANCE 

### <a name="definition"></a>Definizione

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

| Membri | Descrizione |
| ---------------------------------------- | ----------------------------------------------------- |
| **gx_scroll_width**                      | Larghezza del widget della barra di scorrimento, in pixel |
| **gx_scroll_thumb_width**                | Larghezza del pulsante Thumb che scorre la barra di scorrimento, in pixel. Questo valore è in genere un numero di pixel inferiore alla lunghezza totale della barra di scorrimento |
| **gx_scroll_thumb_travel_min**           | Offset dalla fine della barra di scorrimento al punto di partenza del pulsante Thumb minimo. Questo limite può essere utilizzato per impedire che il pulsante Thumb venga spostata alla fine della barra di scorrimento |
| **gx_scroll_thumb_travel_max**           | Offset dalla fine della barra di scorrimento al punto di partenza del pulsante Thumb massimo. Questo limite può essere utilizzato per impedire che il pulsante Thumb venga spostata alla fine della barra di scorrimento |
| **gx_scroll_thumb_border_style**         | Stili del bordo del pulsante Thumb |
| **gx_scroll_fill_pixelmap**              | ID Pixelmap facoltativo. Se questo ID Pixelmap è diverso da zero, la barra di scorrimento utilizza questo Pixelmap per creare lo sfondo della barra di scorrimento |
| **gx_scroll_thumb_pixelmap**             | ID Pixelmap facoltativo. Se questo ID Pixelmap è diverso da zero, il pulsante Thumb della barra di scorrimento utilizza questo Pixelmap per disegnarsi |
| **gx_scroll_up_pixelmap**                | ID Pixelmap facoltativo. Se questo ID Pixelmap è diverso da zero, la barra di scorrimento utilizza questo ID Pixelmap per creare il pulsante di fine della barra di scorrimento a sinistra |
| **gx_scroll_down_pixelmap**              | ID Pixelmap facoltativo. Se questo ID Pixelmap è diverso da zero, la barra di scorrimento utilizza questo ID Pixelmap per creare il pulsante di fine della barra di scorrimento a destra/giù |
| **gx_scroll_thumb_color**                | ID risorsa del colore usato per riempire il pulsante Thumb |
| **gx_scroll_thumb_border_color**         | ID risorsa del colore utilizzato per creare il bordo del pulsante Thumb | 
| **gx_scroll_button_color**               | ID risorsa del colore usato per riempire i pulsanti di fine della barra di scorrimento |

## <a name="gx_slider_info"></a>GX_SLIDER_INFO

### <a name="definition"></a>Definizione

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

| Membri | Descrizione |
| --------------------------------------- | ------------------------------------------------------ |
| **gx_slider_info_min_val**              | Valore minimo segnalato |
| **gx_slider_info_max_val**              | Valore massimo segnalato |
| **gx_slider_info_current_value**        | Valore corrente |
| **gx_slider_info_min_travel**           | Limite di viaggio della lancetta |
| **gx_slider_info_max_travel**           | Limite di viaggio della lancetta |
| **gx_slider_info_needle_width**         | Spessore lancetta in pixel |
| **gx_slider_info_needle_height**        | Altezza lancetta in pixel |
|**gx_slider_info_needle_inset**          | Posizione di estrazione della lancetta. Se GX_STYLE_SLIDER_VERTICAL è impostato, viene usato per specificare l'offset dalla posizione iniziale di inizio del cursore al dispositivo di scorrimento a sinistra. Else, usato per specificare l'offset dalla posizione iniziale di inizio del cursore al dispositivo di scorrimento superiore. |
| **gx_slider_info_needle_hotspot_offset** | Hotpot_offset lancetta, usato per specificare l'offset dalla posizione iniziale di inizio del cursore all'area sensibile del dispositivo di scorrimento. |

## <a name="gx_sprite_frame"></a>GX_SPRITE_FRAME

### <a name="definition"></a>Definizione

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

| Membri | Descrizione |
| ---------------------------------------- | ----------------------------------------------------- |
| **gx_sprite_frame_pixelmap**             | ID risorsa del Pixelmap da visualizzare per questo frame. L'ID può essere 0. |
| **gx_sprite_frame_x_offset**             | Offset dal widget sprite a sinistra per visualizzare il pixelmap |
| **gx_sprite_frame_y_offset**             | Offset dal primo widget sprite per visualizzare il pixelmap |
| **gx_sprite_frame_delay**                | Valore delay, nei cicli del timer GUIX, dopo aver visualizzato questo frame prima di avanzare al frame sprite successivo |
| **gx_sprite_frame_background_operation** | Definire la modalità di cancellazione dello sfondo. I valori possibili per questo campo sono:<br />GX_SPRITE_BACKGROUND_NO_ACTION: nessun riempimento tra frame<br />GX_SPRITE_BACKGROUND_SOLID_FILL: ricreare lo sfondo dello sprite<br />GX_SPRITE_BACKGROUND_RESTORE: ripristinare Pixelmap precedenti |
| **gx_sprite_frame_alpha**                | Valore alfa da aggiungere al Pixelmap visualizzato. Il valore 255 specifica che non deve essere imposto alcun valore alfa aggiuntivo. Se Pixelmap include un canale alfa, questo canale alfa verrà aggiunto al valore alfa del frame. |
