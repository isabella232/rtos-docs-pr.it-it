---
title: Appendice I - Strutture di informazioni GUIX
description: Informazioni sulle strutture di informazioni GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8730dbfc49ed51716f32c118a25ebffc907b19a54d98d83ede4155f87fbecb7b
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116784164"
---
# <a name="appendix-i---guix-information-structures"></a>Appendice I - Strutture di informazioni GUIX 

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
| **gx_bidi_text_info_text**               | Testo per il riordinamento |
| **gx_bidi_text_info_font**               | Tipo di carattere usato per visualizzare il testo, impostarlo su GX_NULL se non è necessaria l'interruzione di riga |
| **gx_bidi_text_info_display_width**      | Larghezza disponibile per la visualizzazione, impostarla su -1 se non è necessaria l'interruzione di riga |

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
| **gx_bidi_resolved_text_info_text**             | Puntatore alla matrice di testo dell'offerta riordinata |
| **gx_bidi_resolved_text_info_total_lines**      | Righe totali del testo dell'offerta risolta per un paragrafo |
| **gx_bidi_resolved_text_info_next**             | Risoluzione delle informazioni sul testo dell'offerta per il paragrafo successivo |

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
| **gx_circular_gauge_info_animation_steps**       | Passaggi totali attraversati dalla lance quando si passa dall'angolo corrente della lanceta a un angolo della lanceta appena assegnato |
| **gx_circular_gauge_info_animation_delay**       | Numero di tick di clock GUIX da ritardare tra i passaggi dell'animazione |
| **gx_circular_gauge_info_needle_xpos**           | Distanza tra la parte sinistra del widget del misuratore e il centro di rotazione della lanceta del misuratore |
| **gx_circular_gauge_info_needle_ypos**           | Distanza dalla parte superiore del widget del misuratore al centro di rotazione della lancetta del misuratore |
| **gx_circular_gauge_info_needle_xcor**           | Distanza tra la parte sinistra dell'immagine della lanceta e il centro di rotazione della lanceta del misuratore |
| **gx_circular_gauge_info_needle_ycor**           | Distanza dalla parte superiore dell'immagine della lancetta al centro di rotazione della lancetta del misuratore |
| **gx_circular_gauge_info_needle_pixelmap**       | ID risorsa della mappa pixel che verrà usata per disegnare la lanceta del misuratore. Questa immagine verrà ruotata in base alle esigenze dal widget del misuratore per visualizzare la lanceta del misuratore in qualsiasi posizione |

Il diagramma seguente illustra le coordinate xpos, ypos e xcor, ycor:

![Diagramma delle coordinate Needle Y e X](./media/guix/image8.png)

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
| **gx_line_chart_min_val**          | Valore minimo dei dati, usato per calcolare il ridimensionamento
| **gx_line_chart_max_val**          | Valore massimo dei dati, usato per calcolare il ridimensionamento |
| **gx_line_chart_data**             | Puntatore a una matrice di valori integer. Si tratta dei valori interi tracciati dal widget del grafico a linee |
| **gx_line_ <side> _margin**          | Offset dal limite esterno della finestra del grafico all'area di rendering del grafico effettiva. L'asse del grafico e la linea dati vengono sempre tracciati all'interno di questo limite interno, che consente all'applicazione di disegnare etichette e altre informazioni all'interno della finestra del grafico, ma all'esterno dell'area grafico dei caratteri |
| **gx_line_chart_max_data_count**   | Numero di valori di dati che possono essere presenti. Questo parametro viene usato per calcolare la scala o l'intervallo dell'asse x per il tracciato dei punti dati. |
| **gx_line_active_data_count**      | Numero di valori di dati effettivamente presenti nella matrice di dati. Un grafico a linee può essere ridimensionato per disegnare un massimo di 100 valori (ad esempio), ma in qualsiasi aggiornamento specifico può essere effettivamente presente un numero inferiore di valori di dati. |
| **gx_line_axis_line_width**        | Larghezza della linea utilizzata per disegnare l'asse orizzontale e verticale |
| **gx_line_data_line_width**        | Larghezza della linea dei dati tracciati |
| **gx_line_chart_axis_color**       | ID risorsa del colore usato per disegnare le linee dell'asse |
| **gx_line_chart_line_color**       | ID risorsa del colore usato per disegnare la linea dei dati del grafico |

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
| **gx_mouse_cursor_hotspot_x**      | Offset dalla parte sinistra dell'immagine del mouse all'area sensibile dell'immagine del mouse |
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
| **gx_pen_configuration_min_drag_dist**       | Distanza di trascinamento minima per tick del timer GUIX per attivare un evento FLICK. Chiamare GX_FIXED_VAL_MAKE per impostare un valore del tipo di dati a virgola fissa |
| **gx_pen_configuration_max_pen_speed_ticks** | Velocità massima di trascinamento nei tick del timer GUIX per attivare un evento FLICK | 

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
| **gx_pixelmap_slider_info_lower_background_pixelmap** | ID risorsa della mappa pixel per riempire lo sfondo prima della lanceta. Se la mappa pixel di sfondo superiore non è impostata, viene usata per riempire lo sfondo prima e dopo la lanceta |
| **gx_pixelmap_slider_info_upper_background_pixelmap** | ID risorsa della mappa pixel per riempire lo sfondo dopo la lanceta |
| **gx_pixelmap_slider_info_needle_pixelmap**           | ID risorsa della mappa pixel dell'ago |

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
| **gx_progress_bar_info_font_id**             | ID risorsa del tipo di carattere, usato per disegnare il valore di testo facoltativo all'interno del widget dell'indicatore di stato      |
| **gx_progress_bar_normal_text_color**        | ID risorsa del colore del testo in stato normale, usato per definire il disegno di testo facoltativo all'interno del widget dell'indicatore di stato |
| **gx_progress_bar_selected_text_color**      | ID risorsa del colore del testo quando il widget ottiene lo stato attivo, usato per definire il disegno di testo facoltativo all'interno del widget indicatore di stato |
| **gx_progress_bar_disabled_text_color**      | ID risorsa del colore del testo quando GX_STYLE_ENABLED è attivo, usato per definire il disegno di testo facoltativo all'interno del widget indicatore di stato |
| **gx_progress_bar_fill_pixelmap**            | ID risorsa della mappa pixel per il riempimento dello sfondo|

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
| **gx_radial_progress_bar_info_current_val**       | Il valore corrente, limitato all'intervallo [-360, 360], indica il delta angolare tra la posizione di ancoraggio e il punto finale dell'arco superiore. Il valore negativo fa sì che l'arco sia disegnato in senso orario a partire dalla posizione di ancoraggio. Il valore positivo fa sì che l'arco sia disegnato in senso antiorario a partire dalla posizione di ancoraggio. L'applicazione deve ridimensionare il valore di parola reale indicato per assegnare un valore angolare al widget dell'indicatore di stato |
| **gx_radial_progress_bar_anchor_val**             | Angolo iniziale dell'arco di avanzamento superiore. Il valore è definito in termini di grado intero con 0 gradi che punta a destra e 90 gradi che indica la posizione verso l'alto. |
| **gx_radial_progress_bar_font_id**                | ID risorsa del tipo di carattere usato per disegnare il valore di testo facoltativo all'interno del widget dell'indicatore di stato |
| **gx_radial_progress_bar_normal_text_color**      | ID risorsa del colore del testo in stato normale, usato per definire il disegno di testo facoltativo all'interno del widget dell'indicatore di stato |
| **gx_radial_progress_bar_selected_text_color**    |ID risorsa del colore del testo quando il widget ottiene lo stato attivo, usato per definire il disegno di testo facoltativo all'interno del widget indicatore di stato |
| **gx_radial_progress_bar_disabled_text_color**    | ID risorsa del colore del testo quando GX_STYLE_ENABLED è attivo, usato per definire il disegno di testo facoltativo all'interno del widget indicatore di stato |
| **gx_radial_progress_bar_normal_brush_width**     | Larghezza del cerchio di avanzamento inferiore |
| **gx_radial_progress_bar_selected_brush_width**   | Larghezza dell'arco di avanzamento superiore, l'arco superiore può essere più stretto, uguale o più ampio del cerchio inferiore |
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
**gx_radial_slider_info_xcenter**               | Distanza dal lato sinistro del widget del dispositivo di scorrimento al centro di rotazione dell'ago del dispositivo di scorrimento |
| **gx_radial_slider_info_ycenter**             | Distanza dalla parte superiore del widget del dispositivo di scorrimento al centro di rotazione dell'ago del dispositivo di scorrimento |
| **gx_radial_slider_info_radius**              | Raggio del cerchio del dispositivo di scorrimento radiale |
| **gx_radial_slider_info_track_width**         | Larghezza della traccia del dispositivo di scorrimento radiale |
| **gx_radial_slider_info_current_angle**       | Angolo del dispositivo di scorrimento corrente |
| **gx_radial_slider_info_min_angle**           | Angolo minimo del dispositivo di scorrimento |
| **gx_radial_slider_info_max_angle**           | Angolo massimo del dispositivo di scorrimento |
| **gx_radial_slider_info_angle_list**          | Elenco valori angolo, definisce gli angoli di ancoraggio, se impostato, l'angolo del dispositivo di scorrimento può essere solo uno degli angoli di ancoraggio definiti |
| **gx_radial_slider_info_list_count**          | Numero di angoli di ancoraggio |
| **gx_radial_slider_info_background_pixelmap** | ID risorsa della mappa pixel di sfondo |
| **gx_radial_slider_info_needle_pixelmap**     | ID risorsa della mappa pixel dell'ago |

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
| **gx_rich_text_fonts_normal_id**   | ID risorsa del tipo di carattere normale del testo |
| **gx_rich_text_fonts_bold_id**     | ID risorsa del tipo di carattere di testo in grassetto |
| **gx_rich_text_fonts_italic_id**   | ID risorsa del tipo di carattere del testo in corsivo |
| **gx_rich_text_fonts_bold_italic_id** | ID risorsa del tipo di carattere in grassetto corsivo |

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
| **gx_scroll_increment** | Valore delta minimo della barra di scorrimento |

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
| **gx_scroll_thumb_width**                | Larghezza del pulsante thumb che scorre sulla barra di scorrimento, in pixel. Questo valore è in genere un numero di pixel inferiore alla larghezza totale della barra di scorrimento |
| **gx_scroll_thumb_travel_min**           | Offset dalla fine della barra di scorrimento al punto di spostamento minimo del pulsante thumb. Questo limite può essere usato per impedire al pulsante thumb di passare fino alla fine della barra di scorrimento |
| **gx_scroll_thumb_travel_max**           | Offset dalla fine della barra di scorrimento al punto di spostamento massimo del pulsante thumb. Questo limite può essere usato per impedire al pulsante thumb di passare fino alla fine della barra di scorrimento |
| **gx_scroll_thumb_border_style**         | Stili del bordo del pulsante thumb |
| **gx_scroll_fill_pixelmap**              | ID della mappa pixel facoltativo. Se questo ID mappa pixel è diverso da zero, la barra di scorrimento usa questa mappa pixel per disegnare lo sfondo della barra di scorrimento |
| **gx_scroll_thumb_pixelmap**             | ID della mappa pixel facoltativo. Se l'ID della mappa pixel è diverso da zero, il pulsante thumb della barra di scorrimento usa questa mappa pixel per disegnare se stesso |
| **gx_scroll_up_pixelmap**                | ID della mappa pixel facoltativo. Se l'ID della mappa pixel è diverso da zero, la barra di scorrimento usa questo ID mappa pixel per disegnare la barra di scorrimento verso sinistra o verso l'alto |
| **gx_scroll_down_pixelmap**              | ID della mappa pixel facoltativo. Se questo ID mappa pixel è diverso da zero, la barra di scorrimento usa questo ID mappa pixel per disegnare il pulsante di fine destra/giù della barra di scorrimento |
| **gx_scroll_thumb_color**                | ID risorsa del colore usato per riempire il pulsante thumb |
| **gx_scroll_thumb_border_color**         | ID risorsa di colore usato per disegnare il bordo del pulsante di scorrimento | 
| **gx_scroll_button_color**               | ID risorsa del colore usato per riempire i pulsanti finali della barra di scorrimento |

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
| **gx_slider_info_min_travel**           | Limite di trasferta della lanceta |
| **gx_slider_info_max_travel**           | Limite di trasferta della lanceta |
| **gx_slider_info_needle_width**         | Larghezza della lanceta in pixel |
| **gx_slider_info_needle_height**        | Altezza della lanceta in pixel |
|**gx_slider_info_needle_inset**          | Posizione di disegno della lanceta. Se GX_STYLE_SLIDER_VERTICAL è impostato, usato per specificare l'offset dalla posizione iniziale di disegno della lanceta al dispositivo di scorrimento a sinistra. In caso contrario, usato per specificare l'offset dalla posizione iniziale di disegno della lancetta alla parte superiore del dispositivo di scorrimento. |
| **gx_slider_info_needle_hotspot_offset** | La hotpot_offset, usata per specificare l'offset dalla posizione iniziale di disegno della lanceta all'hotspot del dispositivo di scorrimento. |

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
| **gx_sprite_frame_pixelmap**             | ID risorsa della mappa pixel da visualizzare per questo frame. L'ID può essere 0. |
| **gx_sprite_frame_x_offset**             | Offset dal widget sprite a sinistra per visualizzare la mappa pixel |
| **gx_sprite_frame_y_offset**             | Offset dalla parte superiore del widget sprite per visualizzare la mappa pixel |
| **gx_sprite_frame_delay**                | Valore di ritardo, in tick del timer GUIX, dopo aver visualizzato questo frame prima di passare al frame sprite successivo |
| **gx_sprite_frame_background_operation** | Definire la modalità di cancellazione dello sfondo. I valori possibili per questo campo sono:<br />GX_SPRITE_BACKGROUND_NO_ACTION: Nessun riempimento tra frame<br />GX_SPRITE_BACKGROUND_SOLID_FILL: Ridisegnare lo sfondo dello sprite<br />GX_SPRITE_BACKGROUND_RESTORE: Ripristinare la mappa pixel precedente |
| **gx_sprite_frame_alpha**                | Valore alfa da aggiungere alla mappa pixel visualizzata. Il valore 255 specifica che non deve essere imposto alcun valore alfa aggiuntivo. Se la mappa pixel include un canale alfa, questo canale alfa verrà aggiunto al valore alfa del fotogramma. |
