---
title: Note sulla modifica di tipi di widget specifici
description: Commenti dettagliati che descrivono i metodi di modifica per determinati tipi di widget complessi.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 3194a1b8c8965bf821631a8c34ac5e9961f8c8ff
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823030"
---
# <a name="chapter-8-notes-on-editing-specific-widget-types"></a>Capitolo 8: Note sulla modifica di tipi di widget specifici

GUIX Studio consente all'utente di creare e modificare facilmente i widget GUIX che compongono le schermate dell'interfaccia utente dell'applicazione. La maggior parte di questi metodi di modifica sono intuitivi e evidenti. Per ridimensionare un widget, ad esempio, è possibile selezionare il widget con il mouse e trascinare i bordi del widget. È anche possibile digitare direttamente nei campi delle proprietà sinistra/superiore/larghezza/altezza del widget selezionato.

Alcuni tipi di widget richiedono un processo di modifica più avanzato, perché questi widget sono a loro volta più sofisticati nel supporto delle funzionalità.

In questo capitolo vengono fornite note sulle funzionalità di modifica più avanzate per questi tipi di widget più complessi. Queste note si espanderanno come le funzionalità di GUIX studio avanzano insieme ai tipi di widget forniti nella libreria GUIX.

## <a name="rich-text-view"></a>Visualizzazione Rich Text

Questo widget viene usato per visualizzare il testo RTF che supporta i codici di formattazione del testo inline. Questi codici di formattazione includono grassetto, corsivo e molti altri. Per iniziare, fare clic con il pulsante destro del mouse sul padre selezionato dalla *vista progetto* o dalla *visualizzazione destinazione* e selezionare menu **Inserisci/testo/visualizzazione testo RTF** per inserire un widget visualizzazione RTF.

Oltre al set standard di proprietà supportato da tutti i tipi di widget, il tipo di widget visualizzazione testo RTF supporta proprietà aggiuntive.

### <a name="additional-properties"></a>Proprietà aggiuntive

| Proprietà | Significato |
|----------|---------|
| Allineamento testo | Allineamento testo predefinito |
| Tipo di carattere normale| Carattere testo predefinito |
| Carattere grassetto  | Carattere testo per il testo contrassegnato come grassetto |
| Carattere corsivo| Carattere testo per testo contrassegnato come corsivo|
| Carattere corsivo grassetto| Carattere testo per il testo contrassegnato come grassetto e corsivo |
| Copia di testo privata | Controllare se il widget deve tenere una copia privata del testo assegnato |
| Spazi vuoti | Larghezza del margine tra il widget e il testo visualizzato, in pixel. |
| Spazio linea | Spazio tra due righe del testo, in pixel. |
|||

### <a name="the-rich-text-formatting-codes"></a>Codici di formattazione del testo RTF

I codici di formato seguenti sono supportati per la formattazione del testo.

|Tag|Significato|
|---|---|
|\<b>\</b> | Carattere di rendering testo con ID carattere grassetto specificato dall'utente|
|\<i>\</i> | Carattere di rendering testo con ID carattere corsivo specificato dall'utente|
|\<u>\</u> | Esegui rendering del testo sottolineato|
|\<f GX_FONT_ID>\</f> | Esegue il rendering del testo utilizzando l'ID del tipo di carattere specificato. |
|\<c GX_COLOR_ID>\</c> | Esegui il rendering del testo con l'ID colore specificato|
|\<hc GX_COLOR_ID>\</hc> | Esegui il rendering del testo usando l'ID del colore di sfondo specificato|
|\<align left/right/center>\</align> | Assegna allineamento testo|
|||

Esistono due modi per modificare la stringa di testo RTF dall'interno di GUIX Studio:

- Utilizzare la finestra di dialogo Modifica testo RTF, che rappresenta il metodo di modifica consigliato e più semplice.
- Utilizzare la finestra di dialogo Editor tabelle di stringhe, che consente di inserire manualmente i tag di formattazione mostrati nella tabella precedente.

Dopo aver selezionato un widget visualizzazione RTF nella *visualizzazione destinazione*, selezionare il pulsante **modifica testo RTF** nella *visualizzazione proprietà* per richiamare la finestra di dialogo Modifica testo rtf, illustrata nella figura 8,1.

![Screenshot della finestra di dialogo Modifica testo RTF di GUIX Studio.](./media/guix-studio/edit_rich_text_dialog.png)

**Figura 8,1**

Il riquadro sinistro è il campo di modifica RTF. È possibile usare le icone della barra degli strumenti per inserire i tag necessari. Selezionare un blocco di testo nel campo modifica, quindi selezionare i pulsanti della barra degli strumenti per applicare gli stili e i colori necessari al blocco di testo selezionato. La finestra di dialogo Modifica testo RTF è un modo semplice per inserire i codici di formattazione nella stringa di test. È anche possibile inserire questi tag manualmente o generarli in fase di esecuzione, se necessario.

Il riquadro destro è l'anteprima del widget per mostrare come viene eseguito il rendering del testo nella visualizzazione di destinazione. Il colore di sfondo dell'anteprima del widget è fisso, che potrebbe non corrispondere al colore di sfondo assegnato del widget nella visualizzazione di destinazione.

I nomi degli ID di risorsa vengono usati in testo RTF per fare riferimento a risorse di tipo carattere o colore specifiche. Se il nome della risorsa di un tipo di carattere o un colore viene modificato dopo che è stato fatto riferimento dalla stringa di testo RTF, GUIX Studio aggiornerà automaticamente la stringa di testo RTF in modo da riflettere le modifiche al nome della risorsa. D'altra parte, se si elimina una risorsa di tipo carattere o colore a cui fa riferimento un widget RTF, è necessario modificare manualmente il testo RTF interessato per rimuovere o modificare i nomi degli ID di risorsa eliminati.

Quando si seleziona il pulsante Salva in questa finestra di dialogo, la stringa di testo RTF definita viene aggiunta alla tabella delle stringhe del progetto.

## <a name="string-scroll-wheel"></a>Rotellina di scorrimento stringa

Un widget della rotellina di scorrimento della stringa supporta la visualizzazione di una matrice di stringhe. Queste stringhe possono essere assegnate in modo dinamico o, nel caso in cui l'applicazione supporti più lingue, le stringhe assegnate possono essere estratte dalla tabella delle stringhe attive.

Il widget della rotellina di scorrimento della stringa supporta una matrice di stringhe. Viene fornita la finestra di dialogo di modifica della rotellina di scorrimento della stringa, illustrata nella figura 8,2, per consentire all'utente di assegnare la matrice di stringhe.

![Screenshot della finestra di dialogo di modifica della rotellina di scorrimento della stringa di GUIX Studio.](./media/guix-studio/string_scroll_wheel_edit.png)

**Figura 8,2**

Per richiamare questa finestra di dialogo, selezionare un widget della rotellina di scorrimento della stringa nella *visualizzazione di destinazione* o nella *visualizzazione del progetto*. Una volta selezionato questo tipo di widget, nella *visualizzazione proprietà* sarà incluso un pulsante **modifica stringhe** . Selezionare questo pulsante per richiamare la finestra di dialogo di modifica della rotellina di scorrimento della stringa.

Per assegnare una stringa per ogni indice di testo, è possibile selezionare un ID stringa dall'elenco a discesa oppure digitare un nuovo valore stringa nel campo di testo a destra. Una volta apportate le modifiche, tutte le stringhe nuove o modificate verranno salvate nella tabella delle stringhe attive.

## <a name="sprite"></a>Sprite

Un widget sprite viene usato per visualizzare una sequenza di immagini per fornire un effetto di animazione. Un widget sprite richiede un elenco di frame, ovvero una matrice di ID immagine e parametri univoci applicati a ogni immagine nel frame. Per compilare questo elenco di frame per il widget sprite, viene fornita la finestra di dialogo modifica frame sprite, illustrata nella figura 8,3:

![Screenshot della finestra di dialogo modifica frame sprite di GUIX Studio.](./media/guix-studio/edit_sprite_frames.png)

**Figura 8,3**

Per richiamare questa finestra di dialogo, selezionare un widget sprite nella *visualizzazione di destinazione* o nella visualizzazione del *progetto*. Una volta selezionato questo tipo di widget, nella *visualizzazione proprietà* sarà incluso un pulsante **modifica frame** . Selezionare questo pulsante per richiamare la finestra di dialogo di modifica della rotellina di scorrimento della stringa.

Il campo *numero totale di frame sprite* è un campo di input che consente di immettere il numero intero di frame che devono essere visualizzati dal widget sprite. Le immagini possono essere riutilizzate all'interno dell'elenco di frame, ovvero non tutte le immagini devono essere univoche.

Il campo sprite ID frame è un valore di selezione dell'indice frame compreso tra 1 e il numero totale di fotogrammi. Incrementare e decrementare questo valore per spostarsi da un frame sprite a quello successivo.

Ogni frame sprite presenta diversi parametri. Il primo è l'operazione in background. Questo campo simula le funzionalità del formato di animazione GIF più diffuso. Di seguito sono riportate le opzioni seguenti:

- Nessuna operazione, ovvero l'immagine del frame corrente viene disegnata sull'immagine del frame precedente.
- Ripristinare la prima mappa pixel, il che significa che la mappa pixel index 1 viene disegnata prima della mappa pixel corrente e
- Riempimento a tinta unita, ovvero lo sfondo dello sprite viene riempito con il colore di sfondo dello sprite prima che venga disegnato il frame corrente.

Il campo ID mappa pixel consente di selezionare qualsiasi mappa pixel aggiunta in precedenza alle risorse del progetto. Lo stesso ID mappa pixel può essere usato per più frame. Ad esempio, l'animazione sprite può utilizzare lo spostamento dell'immagine (usando i campi offset x e y) anziché o oltre a usare immagini sprite diverse.

Il campo del valore alfa viene applicato all'intero disegno della mappa pixel. Questo campo ha un effetto solo quando è in esecuzione a una profondità di colore di 8 BPP e superiore. Il valore alfa 0 è completamente trasparente e il valore alfa 255 è opaco.

È possibile specificare un offset all'interno del frame sprite in corrispondenza del quale verrà disegnata la mappa pixel corrente usando i campi offset x e offset y frame. In altre parole, non è necessario che ogni immagine disegnata sia la dimensione completa del widget sprite.

Il periodo di ritardo specifica il tempo di attesa prima del passaggio al frame sprite successivo. Questo valore è in cicli, che per la configurazione predefinita del timer GUIX/ThreadX ogni segno di selezione rappresenta 50 ms.

Quando si salvano le modifiche nella finestra di dialogo modifica frame sprite, GUIX studio è in grado di generare la matrice di elenco frame completa come parte della generazione di file delle specifiche di output.
