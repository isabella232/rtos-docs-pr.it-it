---
title: Note sulla modifica di tipi di widget specifici
description: Commenti dettagliati che descrivono i metodi di modifica per determinati tipi di widget complessi.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 374471df85c4cd0fffae5b5cc7ad31d2237877f2
ms.sourcegitcommit: 62cfdf02628530807f4d9c390d6ab623e2973fee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2021
ms.locfileid: "115178281"
---
# <a name="chapter-8-notes-on-editing-specific-widget-types"></a>Capitolo 8: Note sulla modifica di tipi di widget specifici

GUIX Studio consente all'utente di creare e modificare facilmente widget GUIX che compongono le schermate dell'interfaccia utente dell'applicazione. La maggior parte di questi metodi di modifica è intuitiva e ovvia. Ad esempio, per ridimensionare un widget è possibile selezionarlo con il mouse e trascinare i bordi del widget. È anche possibile digitare direttamente nei campi delle proprietà left/top/width/height del widget selezionato.

Alcuni tipi di widget richiedono un processo di modifica più avanzato, perché questi widget sono a loro volta un po' più sofisticati nel supporto delle funzionalità.

Questo capitolo contiene note sulle funzionalità di modifica più avanzate per questi tipi di widget più complessi. Queste note si espanderanno man mano che le funzionalità di GUIX Studio avanzano insieme ai tipi di widget disponibili nella libreria GUIX.

## <a name="rich-text-view"></a>Visualizzazione testo RTF

Questo widget viene usato per visualizzare testo RTF che supporta i codici di formattazione del testo inline. Questi codici di formattazione includono grassetto, corsivo e molti altri. Per iniziare, fare clic con il pulsante destro del  mouse sull'elemento padre selezionato dalla visualizzazione *Project* o dalla visualizzazione di destinazione e scegliere il menu **Inserisci/Testo/Visualizzazione** testo RTF per inserire un widget di visualizzazione rtf.

Oltre al set standard di proprietà supportate da tutti i tipi di widget, il tipo di widget Visualizzazione testo RTF supporta proprietà aggiuntive.

### <a name="additional-properties"></a>Proprietà aggiuntive

| Proprietà | Significato |
|----------|---------|
| Allineamento testo | Allineamento del testo predefinito |
| Tipo di carattere normale| Tipo di carattere del testo predefinito |
| Carattere grassetto  | Tipo di carattere del testo per il testo contrassegnato in grassetto |
| Carattere corsivo| Tipo di carattere del testo per il testo contrassegnato come corsivo|
| Carattere corsivo grassetto| Tipo di carattere del testo per il testo contrassegnato come grassetto e corsivo |
| Copia di testo privata | Deve essere controllato se il widget deve mantenere la propria copia privata di qualsiasi testo assegnato |
| Spazio vuoto | Larghezza del margine tra il widget e il testo visualizzato, in pixel. |
| Spazio riga | Spazio tra due righe del testo, in pixel. |
|||

### <a name="the-rich-text-formatting-codes"></a>Codici di formattazione RTF

I codici di formato seguenti sono supportati per la formattazione del testo.

|Tag|Significato|
|---|---|
|\<b>\</b> | Eseguire il rendering del tipo di carattere del testo con l'ID carattere in grassetto specificato dall'utente|
|\<i>\</i> | Eseguire il rendering del tipo di carattere del testo con l'ID carattere corsivo specificato dall'utente|
|\<u>\</u> | Eseguire il rendering del testo sottolineato|
|\<f GX_FONT_ID>\</f> | Eseguire il rendering del testo usando l'ID del tipo di carattere specificato. |
|\<c GX_COLOR_ID>\</c> | Eseguire il rendering del testo usando l'ID colore specificato|
|\<hc GX_COLOR_ID>\</hc> | Eseguire il rendering del testo usando l'ID colore di sfondo specificato|
|\<align left/right/center>\</align> | Assegnare l'allineamento del testo|
|||

Esistono due modi per modificare la stringa di testo RTF da GUIX Studio:

- Usare la finestra di dialogo Modifica testo RTF, che è il metodo di modifica consigliato e più semplice.
- Usare la finestra di dialogo Editor tabelle stringhe, che consente di inserire manualmente i tag di formattazione mostrati nella tabella precedente.

Dopo aver selezionato un widget Rich Text View (Visualizzazione RTF) in Target *View*(Visualizzazione di destinazione), selezionare il pulsante **Edit Rich Text** (Modifica testo RTF) nella visualizzazione Proprietà per richiamare la finestra di dialogo rich text edit (Modifica testo RTF), illustrata nella figura 8.1. 

![Screenshot della finestra di dialogo Modifica testo RTF di GUIX Studio.](./media/guix-studio/edit_rich_text_dialog.png)

**Figura 8.1**

Il riquadro sinistro è il campo rich text edit. È possibile usare le icone della barra degli strumenti per inserire i tag necessari. Selezionare qualsiasi blocco di testo nel campo di modifica e quindi selezionare i pulsanti della barra degli strumenti per applicare gli stili e i colori necessari al blocco di testo selezionato. La finestra di dialogo Modifica testo RTF è un modo semplice per inserire i codici di formattazione nella stringa di test. È anche possibile inserire questi tag manualmente o anche generarli in fase di esecuzione, se necessario.

Il riquadro destro è l'anteprima del widget che mostra come viene eseguito il rendering del testo nella visualizzazione di destinazione. Il colore di sfondo dell'anteprima del widget è fisso, che potrebbe non corrispondere al colore di sfondo assegnato del widget nella visualizzazione di destinazione.

I nomi degli ID risorsa vengono usati in formato RTF per fare riferimento a risorse specifiche relative a tipi di carattere o colori. Se il nome della risorsa di un tipo di carattere o di un colore viene modificato dopo che è stato fatto riferimento dalla stringa di testo RTF, GUIX Studio aggiornerà automaticamente la stringa di testo RTF in modo da riflettere le modifiche apportate al nome della risorsa. D'altra parte, se si elimina una risorsa di tipo di carattere o colore a cui fa riferimento un widget di testo RTF, è necessario modificare manualmente il testo RTF interessato per rimuovere o modificare i nomi degli ID risorsa che sono stati eliminati.

Quando si seleziona il pulsante Salva in questa finestra di dialogo, la stringa di testo RTF definita viene aggiunta alla tabella delle stringhe del progetto.

## <a name="string-scroll-wheel"></a>String Scroll Wheel

Un widget della rotellina di scorrimento di stringhe supporta la visualizzazione di una matrice di stringhe. Queste stringhe possono essere assegnate in modo dinamico oppure, nel caso in cui l'applicazione supporti più lingue, è possibile eseguire il pulled delle stringhe assegnate dalla tabella delle stringhe attive.

Il widget della rotellina di scorrimento della stringa supporta una matrice di stringhe. Per consentire all'utente di assegnare questa matrice di stringhe, viene visualizzata la finestra di dialogo String Scroll Wheel Edit (Modifica della rotellina di scorrimento della stringa), illustrata nella figura 8.2.

![Screenshot della finestra di dialogo GUIX Studio String Scroll Wheel Edit (Modifica della rotellina di scorrimento della stringa di GUIX Studio).](./media/guix-studio/string_scroll_wheel_edit.png)

**Figura 8.2**

Per richiamare questa finestra di dialogo, selezionare un widget della rotellina di scorrimento della stringa all'interno della visualizzazione *di destinazione* o Project *visualizzazione*. Dopo aver selezionato questo tipo di widget, la *visualizzazione Proprietà* includerà un **pulsante Modifica** stringhe. Selezionare questo pulsante per richiamare la finestra di dialogo String Scroll Wheel Edit (Modifica rotellina di scorrimento stringa).

Per assegnare una stringa per ogni indice di testo, è possibile selezionare un ID stringa dall'elenco a discesa oppure digitare un nuovo valore stringa nel campo Testo a destra. Al termine delle modifiche, tutte le stringhe nuove o modificate vengono salvate nella tabella di stringhe attiva.

## <a name="sprite"></a>Sprite

Un widget sprite viene usato per visualizzare una sequenza di immagini per fornire un effetto di animazione. Un widget sprite richiede un elenco di frame, ovvero una matrice di ID immagine e parametri univoci applicati a ogni immagine nel frame. Per creare questo elenco di frame per il widget sprite, è disponibile la finestra di dialogo Modifica frame Sprite, illustrata nella figura 8.3:

![Screenshot della finestra di dialogo Modifica frame Sprite di GUIX Studio.](./media/guix-studio/edit_sprite_frames.png)

**Figura 8.3**

Per richiamare questa finestra di dialogo, selezionare un widget sprite in *Target View (Visualizzazione di destinazione)* *o Project View (Visualizza).* Dopo aver selezionato questo tipo di widget, la *visualizzazione Proprietà* includerà un pulsante Modifica **elenco frame.** Selezionare questo pulsante per richiamare la finestra di dialogo String Scroll Wheel Edit (Modifica rotellina di scorrimento stringa).

Il campo Total number of Sprite Frames (Numero totale di fotogrammi *sprite)* è un campo di input che consente di immettere il numero intero totale di fotogrammi che devono essere visualizzati dal widget sprite. Le immagini possono essere riutilizzate all'interno dell'elenco di frame, vale a dire che non tutte le immagini devono essere univoche.

Il campo Sprite Frame ID (ID fotogramma sprite) è un valore di selezione dell'indice dei frame compreso tra 1 e Numero totale di frame. Incrementare e decrementare questo valore per passare da un frame sprite a quello successivo.

Ogni frame sprite ha diversi parametri. Il primo è l'operazione in background. Questo campo simula le funzionalità del diffuso formato di animazione GIF. Le opzioni disponibili includono:

- Nessuna operazione, ovvero l'immagine del frame corrente viene disegnata sull'immagine del frame precedente.
- Ripristina prima mappa pixel, ovvero l'indice mappa di 1 pixel viene disegnato prima della mappa pixel corrente e
- Riempimento a tinta unita, ovvero lo sfondo dello sprite viene riempito con il colore di sfondo dello sprite prima che venga disegnata la cornice corrente.

Il campo ID mappa pixel consente di selezionare qualsiasi mappa pixel aggiunta in precedenza alle risorse del progetto. Lo stesso ID mappa pixel può essere usato per più fotogrammi. Ad esempio, l'animazione sprite potrebbe usare il movimento dell'immagine (usando i campi di offset x e y) anziché o oltre a usare immagini sprite diverse.

Il campo Valore alfa viene applicato all'intero disegno mappa pixel. Questo campo ha effetto solo quando l'esecuzione ha una profondità di colore di 8 bpp e superiore. Il valore alfa 0 è completamente trasparente e il valore alfa 255 è opaco.

È possibile specificare un offset all'interno del frame sprite in corrispondenza del quale verrà disegnata la mappa pixel corrente usando i campi Offset x frame e Offset y frame. In altre parole, ogni immagine disegnata non deve avere le dimensioni complete del widget sprite.

Il periodo di ritardo specifica il tempo di ritardo prima di passare al frame dello sprite successivo. Questo valore è in tick, che per la configurazione predefinita del timer GUIX/ThreadX ogni tick rappresenta 50 ms.

Quando si salvano le modifiche nella finestra di dialogo Modifica frame Sprite, GUIX Studio è in grado di generare la matrice dell'elenco di frame completo come parte della generazione del file delle specifiche di output.

### <a name="assign-a-sprite-widget-with-gif-resource"></a>Assegnare un widget sprite con una risorsa GIF
È possibile aggiungere una risorsa GIF al **gruppo di risorse Pixelmap** e assegnare la risorsa GIF direttamente al widget sprite. Dopo aver impostato la risorsa GIF, verrà generato automaticamente un elenco di frame. È possibile modificare ulteriormente ogni frame dell'elenco di frame tramite la finestra di dialogo di modifica dello sprite:

![Screenshot della finestra di dialogo Modifica frame Sprite di GUIX Studio per la risorsa GIF.](./media/guix-studio/edit_sprite_gif_frames.jpg)

**Figura 8.4**