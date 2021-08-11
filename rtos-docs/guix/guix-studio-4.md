---
title: Risorse di GUIX Studio
description: GUIX Studio offre la gestione di tutte le risorse dell'interfaccia utente che verranno usate dall'applicazione per colori, tipi di carattere, mappe pixel e stringhe. Le sezioni seguenti descrivono come aggiungere, modificare ed eliminare risorse all'interno della progettazione della schermata dell'interfaccia utente.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: dd694cb7d34df7ecae206c3dcaf7d75a20bd4bd4e26471bb94da4129897ef727
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116786145"
---
# <a name="chapter-4-guix-studio-resources"></a>Capitolo 4: Risorse di GUIX Studio

GUIX Studio offre la gestione di tutte le risorse dell'interfaccia utente che verranno usate dall'applicazione per colori, tipi di carattere, mappe pixel e stringhe. Le sezioni seguenti descrivono come aggiungere, modificare ed eliminare risorse all'interno della progettazione della schermata dell'interfaccia utente. 

Tutta la gestione delle risorse viene eseguita **all'interno Visualizzazione risorse*** dell'interfaccia utente di GUIX Studio, come illustrato di seguito nella figura _8_**.

![Screenshot di GUIX Studio Visualizzazione risorse.](./media/guix-studio/image38.jpg)

**Figura 8**

## <a name="color-resources"></a>Risorse colore

La sezione ***Colors** _ del _*_Visualizzazione risorse_*_ consente di gestire le risorse di colore. È possibile espandere questa visualizzazione facendo clic sul campo _ * nell'intestazione della visualizzazione, risultante nella visualizzazione illustrata di seguito *+* **_nella figura 9:_**

![Screenshot della sezione Colori del Visualizzazione risorse](./media/guix-studio/image_39.png)

**Figura 9**

Le risorse colore sono costituite da uno o più colori, ognuno con un nome logico univoco. Ad esempio, nella **figura 9** il nome logico **CANVAS,** ovvero l'ID colore di sistema per il colore di riempimento dello sfondo dello schermo, è associato al colore fisico nero. Questa risorsa colore viene usata ogni volta che **l'applicazione GX_COLOR_ID_CANVAS** come colore nelle proprietà dell'oggetto.

Il colore "swatch" che indica il valore RGB del colore viene visualizzato a sinistra, seguito dal nome dell'ID colore. È possibile modificare il valore RGB associato a qualsiasi nome ID in qualsiasi momento. Non è possibile modificare i nomi ID dei colori di sistema predefiniti perché vengono usati internamente dalla libreria GUIX. È tuttavia possibile modificare qualsiasi valore di colore. La modifica di un valore del colore di sistema è **una modifica globale.** Ciò significa che qualsiasi widget che non dispone di un'assegnazione di colore specifica avrà il nuovo valore del colore di sistema.

È possibile modificare sia il nome del colore che il valore del colore per i colori personalizzati aggiunti al tema.

Per modificare una risorsa colore, fare doppio clic (o fare clic con il pulsante destro del mouse e scegliere menu) sulla risorsa colore. Questa azione apre la finestra di dialogo di definizione del colore. Da questa finestra di dialogo è possibile modificare la risorsa colore in base alle esigenze dell'interfaccia utente dell'applicazione. ***La figura 10** _ mostra la finestra di dialogo di modifica quando si fa doppio clic su _ *CANVAS**. L'aspetto di questa finestra di dialogo cambierà in base alle impostazioni del formato dei colori della visualizzazione di destinazione.

![Screenshot della finestra di dialogo Modifica colore.](./media/guix-studio/edit_color.png)

**Figura 10**

L'aspetto della finestra di dialogo Modifica colore cambierà a seconda della profondità del colore e della configurazione del formato del colore della visualizzazione corrente.

Per aggiungere una nuova risorsa colore, dalla sezione ***Colors** _ di _ *_Visualizzazione risorse_** selezionare il pulsante seguente:

![Pulsante Aggiungi nuovo colore](./media/guix-studio/image41.jpg)

Usare la finestra di dialogo colore risultante per aggiungere una nuova risorsa colore, come illustrato di seguito nella figura **11**:*

![Screenshot di Nuovo colore nella finestra di dialogo Modifica colore.](./media/guix-studio/new_color.png)

**Figura 11**

Dopo aver completato questi  passaggi, la selezione di Salva una nuova risorsa colore con il **nome NEW_COLOR** con il colore fisico verde sarà disponibile per l'applicazione.

**Considerazioni speciali quando si modificano le impostazioni del formato del colore di visualizzazione:**

Quando si crea un nuovo progetto, viene richiesto automaticamente di configurare le schermi del progetto e il formato del colore di ogni visualizzazione. Nella maggior parte dei casi queste selezioni vengono apportate una sola volta e non è necessario modificare tali impostazioni di configurazione.

È possibile determinare che è necessario modificare le impostazioni del formato del colore di visualizzazione in un secondo momento. In tal caso, GUIX Studio effettua una conversione ottimale dei valori RGB del colore utente e del sistema corrente dal formato di colore precedente al nuovo formato colore. Questa conversione segue alcune regole logiche.

Per i colori definiti dall'utente, GUIX Studio tenta sempre di convertire il colore precedente nel colore corrispondente più vicino nel nuovo formato colore. Se si esegue la conversione da una profondità di colore elevata, ad esempio 16 bpp 5:6:5 in una scala di grigi o in un formato di colore monocromatico, questa modifica potrebbe comportare conversioni di colori indesiderate. Quando si apporta una modifica di grandi dimensioni alle impostazioni di profondità dei colori di visualizzazione, potrebbero essere necessari alcuni aggiornamenti manuali alla nuova tabella dei colori definita dall'utente.

Per i colori di sistema predefiniti, GUIX Studio definisce internamente tre tabelle dei colori predefinite univoche. Una tabella dei colori predefinita viene usata per tutte le profondità di colore maggiori della scala dei grigi a 4 bpp, una seconda tabella dei colori predefinita viene usata per i formati di colore con scala dei grigi (1 bpp < display_color_format <= 4bpp) e infine una terza tabella dei colori di sistema predefinita viene usata per il formato colore monocromatico.

Quando si cambia il formato del colore di visualizzazione Project finestra di dialogo Configurazione, vengono applicate le regole seguenti:

1) Se i formati dei colori di visualizzazione precedenti e nuovi usano tabelle dei colori di sistema predefinite diverse, come definito in precedenza, i colori di sistema vengono ripristinati ai colori predefiniti. In altre parole, se si passa dal colore alla scala dei grigi o dalla scala dei grigi alla profondità del colore monocromatica, i colori di sistema verranno reimpostati sui valori predefiniti definiti internamente per la nuova profondità di colore. Anche se ciò può causare la perdita di alcune informazioni sui colori personalizzate, questa soluzione offre un punto di partenza ragionevole quando si apporta una modifica notevole alle impostazioni del formato del colore di visualizzazione.

2) Se i formati di colore precedente e nuovo usano la stessa tabella dei colori predefinita, vale a dire che si sta apportando una modifica del formato di colore meno notevole, GUIX Studio testerà ogni colore di sistema per determinare se il valore RGB del colore di sistema è stato modificato rispetto al valore predefinito. Se il valore RGB del colore di sistema è stato modificato, GUIX Studio farà una conversione ottimale dal formato di colore precedente al nuovo formato di colore. Se il colore di sistema non è stato modificato, verrà ripristinato il colore predefinito per il nuovo formato colore.

**Considerazioni speciali per il funzionamento della modalità tavolozza:**

Quando un progetto è configurato per il formato a 256 colori in modalità tavolozza dei colori, l'utente può configurare la modalità di installazione e utilizzo della tavolozza. È possibile accedere alla definizione della tavolozza e modificarla tramite il comando Configura| Finestra di dialogo Temi e se il progetto è impostato per 8 bpp, verrà visualizzato il pulsante "Modifica tavolozza". Fare clic su questo pulsante per visualizzare la finestra di dialogo Modifica riquadro:

![Screenshot della finestra di dialogo Modifica riquadro.](./media/guix-studio/edit_palette.png)

GUIX Studio divide la tavolozza in due sezioni: la sezione "definita dall'utente" e la sezione "generata automaticamente". GUIX Studio esegue un sofisticato algoritmo di generazione della tavolozza ottimale per creare la tavolozza migliore per visualizzare le immagini incluse in ogni tema. È possibile definire un numero qualsiasi di voci della tavolozza digitando un numero nel campo "Voci predefinite della tavolozza" e immettere qualsiasi valore RGB per uno di questi slot. Gli slot rimanenti verranno allocati a Studio per creare una tavolozza dei colori ottimale per la visualizzazione delle immagini.

Quando si esegue questa modalità, se si vuole modificare un colore definito nella visualizzazione risorse, l'editor colori consentirà di selezionare solo le voci predefinite della tavolozza definite. Ciò è dovuto al fatto che le voci rimanenti della tavolozza vengono generate automaticamente da GUIX Studio e cambieranno quando vengono modificate le immagini aggiunte al progetto.

Se è necessaria la visualizzazione dei tipi di carattere con anti-aliasing durante l'esecuzione in modalità tavolozza 8bpp, è necessario definire una matrice di voci della tavolozza che creano una sfumatura per ogni colore di primo piano/sfondo utilizzato per visualizzare il testo con anti-aliasing. È possibile usare 8 voci della tavolozza per la sfumatura per ogni combinazione di colori o 16 voci della tavolozza per una sfumatura più smussata. Questo numero di voci della tavolozza usate è determinato dalla casella di controllo "Number of Palette Mode Anti-Aliased Text Colors" (Numero di colori di testo con anti-aliasing modalità tavolozza) nella finestra di dialogo Project configurazione. È possibile usare una sfumatura con solo otto voci per ridurre al minimo le voci della tavolozza usate per ogni combinazione di colori oppure usare 16 sfumature di immissione per ottenere l'aspetto del testo con anti-aliasing più uniforme.

Per semplificare la definizione di una sfumatura di colore per la visualizzazione di testo con anti-aliasing o per generare una sfumatura di colore per un utilizzo personalizzato, nella finestra di dialogo Modifica tavolozza è disponibile il pulsante Genera sfumatura. Per usare questa funzionalità, è prima necessario assegnare i valori r:g:b dei colori sfumatura iniziale e finale.

Ad esempio, se si vuole visualizzare testo rosso anti-aliasing su uno sfondo grigio medio usando otto voci della tavolozza a partire dall'indice 50, assegnare il valore r:g:b di 255:0:0 all'indice della tavolozza 50 e il valore r:g:b 128:128:128 all'indice tavolozza 57. Immettere questi valori di indice della tavolozza nei campi start-index e end-index in questa finestra di dialogo e fare clic sul pulsante Generate Gradient (Genera sfumatura). Le voci della tavolozza da 51 a 56 verranno inizializzate per definire una transizione sfumato uniforme tra i colori di delimitazione.

## <a name="font-resources"></a>Risorse dei tipi di carattere

Per gestire le risorse dei tipi di carattere, è prima necessario espandere la sezione ***Tipi** di carattere _ del _*_Visualizzazione risorse_*_ facendo clic sul campo _ *, visualizzando la finestra di dialogo illustrata di seguito *+* nella figura **_12:_**

![Screenshot della sezione Tipi di carattere nel Visualizzazione risorse.](./media/guix-studio/image44.jpg)

**Figura 12**

Le risorse dei tipi di carattere sono costituite da uno o più tipi di carattere, ognuno con un nome logico univoco. Ad esempio, nella **figura 12 il** nome logico **SYSTEM** è associato a un tipo di carattere specifico. Questa risorsa del tipo di carattere viene usata ogni volta che l'applicazione specifica **SYSTEM** come tipo di carattere nelle proprietà dell'oggetto. Il gruppo di caratteri mostra un'anteprima WYSIWYG dei glifi a sinistra, l'altezza del carattere in pixel, il nome ID carattere e le dimensioni del carattere (in kb).

Nella visualizzazione precedente i primi quattro tipi di carattere sono i tipi di carattere predefiniti richiesti dalla libreria GUIX. È possibile modificare i dati dei tipi di carattere associati a questi tipi di carattere, ma non è possibile modificare questi nomi ID dei tipi di carattere.

L'ultimo tipo di carattere illustrato in precedenza, denominato "Corsivo", è un tipo di carattere personalizzato che è stato aggiunto al progetto dall'utente.

Per modificare una risorsa tipo di carattere, fare doppio clic (o fare clic con il pulsante destro del mouse e scegliere menu) sulla risorsa del tipo di carattere. Da questa finestra di dialogo la risorsa del tipo di carattere può essere modificata in base alle esigenze dell'interfaccia utente dell'applicazione. ***La figura 13** _ mostra la finestra di dialogo di modifica quando si fa doppio clic su _ *SYSTEM**.

! [[Screenshot della finestra di dialogo di modifica quando si fa doppio clic su SYSTEM.](./media/guix-studio/edit_system_font.png)

**Figura 13**

Per aggiungere una nuova risorsa tipo di carattere, nella sezione ***Fonts** _ (Tipi di carattere ) di _ *_Visualizzazione risorse_** selezionare il pulsante seguente:

![Pulsante Aggiungi nuovo tipo di carattere](./media/guix-studio/image46.jpg)

Verrà richiamata la finestra `Font Edit` di dialogo per aggiungere una nuova risorsa tipo di carattere, come illustrato di seguito ***nella figura 14:***

![Screenshot della finestra di dialogo di modifica per aggiungere una nuova risorsa tipo di carattere.](./media/guix-studio/add_new_font.png)

**Figura 14**

I nuovi tipi di carattere GUIX vengono creati da GUIX Studio per il rendering di un tipo di carattere TrueType scelto a una determinata dimensione. Pertanto la finestra di dialogo precedente richiede prima un percorso del tipo di carattere TrueType. È possibile usare il pulsante Sfoglia per passare a una directory contenente i file dei tipi di carattere nel sistema di sviluppo. Diversi tipi di carattere TrueType sono inclusi anche nella sottocartella GUIX/fonts ovunque sia stato installato GUIX Studio.

Se possibile, il percorso del file del tipo di carattere TrueType viene archiviato internamente usando un percorso relativo al progetto. Per questo motivo è importante mantenere tutti i file dei tipi di carattere in un percorso comune e usare una struttura ad albero di directory comune per i progetti e i file dei tipi di carattere per consentire di spostare i progetti di GUIX Studio da una stazione di sviluppo a un'altra.

Il campo Nome carattere consente di specificare il nome ID della risorsa del tipo di carattere. Si tratta dell'ID risorsa che verrà usato nel codice generato da GUIX Studio e usato anche dall'applicazione quando si fa riferimento al tipo di carattere. Questo nome deve rispettare i requisiti della sintassi di denominazione delle variabili C.

Dopo aver scelto un file del tipo di carattere TrueType da usare come input, immettere un nome logico per il tipo di carattere.

La casella di controllo "**Generate Kerning Info**" indica a GUIX Studio di includere informazioni sulla crenatura all'interno del tipo di carattere generato, che viene usato per regolare le posizioni relative dei glifi successivi in una stringa. Se si vuole applicare la crenatura con le stringhe, è necessario usare un tipo di carattere che contiene informazioni sulla crenatura e attivare questa casella di controllo. Sarà anche necessario definire l'opzione di compilazione della libreria GUIX "GX_FONT_KERNING_SUPPORT" per supportare il rendering del testo con informazioni sulla crenatura.

La casella di controllo " Include **character set defined by String Table**" indica a GUIX Studio di includere i glifi a cui fa riferimento la tabella di stringhe statiche all'interno del tipo di carattere generato. È possibile includere altri glifi selezionando e modificando gli intervalli di caratteri elencati di seguito, ma questa opzione può essere selezionata per generare rapidamente il set di caratteri minimo necessario per visualizzare le stringhe definite all'interno della tabella di stringhe. Naturalmente, se la tabella di stringhe usa glifi che non sono presenti nel tipo di carattere di origine TrueType, tali caratteri non saranno disponibili nel tipo di carattere GUIX e non verranno visualizzati nel sistema di destinazione.

Per generare un tipo di carattere più completo o un tipo di carattere che include caratteri che non possono essere usati all'interno della tabella di stringhe definita in modo statico, è anche possibile selezionare intervalli di caratteri dall'elenco seguente. Si noti che è possibile selezionare qualsiasi numero di intervalli di caratteri ed è possibile modificare il codice carattere iniziale e finale effettivo da includere in ogni intervallo selezionato.

Gli intervalli di caratteri predefiniti e i nomi di pagina sono solo suggerimenti che consentono di selezionare facilmente il set di caratteri necessario per le lingue attive attualmente in uso. I nomi delle lingue elencate non hanno alcun effetto sul tipo di carattere GUIX generato ed è possibile digitare qualsiasi intervallo di caratteri esadecimali desiderato per qualsiasi intervallo di caratteri abilitato o selezionato.

Ad esempio, se si vuole generare un tipo di carattere che contiene solo i caratteri numerici, è possibile selezionare la tabella codici "Ascii", ma immettere il valore iniziale 0030 e il valore finale 0039 per generare un tipo di carattere contenente solo i caratteri numerici. Si noti che i valori dell'intervallo di caratteri codificati in formato esadecimale, ovvero la notazione normale per le tabelle di caratteri Unicode.

Per impostazione predefinita, GUIX Studio e la libreria GUIX supportano i codici carattere da 0x0000 a 0xffff, che comprende tutti i linguaggi attivi, le forme matematiche e altri simboli attualmente in uso. Se è necessario usare codici carattere al di sopra del valore 0xffff, incluse alcune aree di utilizzo privato, è necessario attivare la casella di controllo "Support Extended Character Range". Quando questa casella di controllo è selezionata, GUIX Studio consente all'utente di specificare intervalli di caratteri da 0x0000 a 0x10ffff, inclusi gli intervalli di caratteri Unicode Private Use. Se è necessario questo intervallo di caratteri esteso, sarà necessario definire anche l'opzione di compilazione della libreria GUIX "GX_EXTENDED_UNICODE_SUPPORT" in modo che la libreria GUIX supporti internamente i codici di caratteri a 32 bit, anziché la configurazione predefinita che supporta i codici carattere a 16 bit.

Se si seleziona sia la casella di controllo "Includi set di caratteri definito dalla tabella di stringhe" che uno o più intervalli di caratteri nell'elenco seguente, GUIX Studio combina queste selezioni nel superset degli intervalli selezionati e dei caratteri usati nella tabella di stringhe. Naturalmente, il tipo di carattere di origine TrueType selezionato deve contenere anche i caratteri necessari perché GUIX Studio produca glifi significativi per ogni valore di carattere richiesto.

Dopo aver determinato l'intervallo di caratteri, specificare l'altezza del carattere in pixel e il formato del carattere. Sono supportati sia i tipi di carattere con anti-aliasing che i tipi di carattere binari. I tipi di carattere binari richiedono un'area di archiviazione dei dati meno statica, tuttavia i tipi di carattere con anti-aliasing producono l'aspetto migliore nelle destinazioni in esecuzione con gradazioni di grigio a 4 bpp o livelli di colore superiori.

>[!NOTE]  
> *L'"altezza del carattere" si riferisce al quadrato EM del tipo di carattere. Nel tipo di metal tradizionale, em square era uguale all'altezza della linea del corpo del metal da cui ogni lettera aumenta e ogni corpo dimesse era della stessa dimensione. Nel tipo metal, le dimensioni fisiche di una lettera non possono in genere superare il quadrato EM. Nel tipo digitale, EM è una griglia di risoluzione arbitraria usata come spazio di progettazione di un tipo di carattere digitale. Per questi tipi di carattere digitali è comune che alcune caratteristiche del glifo, ad esempio accenti e discese, possano superare i limiti del quadrato EM. Il risultato finale è che l'altezza del widget necessaria per visualizzare completamente un particolare tipo di carattere dovrà spesso essere leggermente maggiore rispetto all'altezza in pixel del carattere richiesta.*

Dopo aver completato tutti i campi di configurazione del tipo di carattere, fare clic sul pulsante OK per creare una nuova risorsa tipo di carattere. GUIX Studio genererà un tipo di carattere compatibile con GUIX con le proprietà scelte, aggiungerà tale tipo di carattere alle risorse del progetto e lo rende disponibile per l'uso da parte dell'applicazione.

## <a name="pixel-map-resources"></a>Risorse mappa pixel

Per gestire le risorse mappa pixel, la sezione ***Mappe** pixel _ del _*_Visualizzazione risorse_*_ deve prima essere espansa facendo clic sul campo _ *, visualizzando la finestra di dialogo illustrata di seguito nella figura *+* **_15:_**

Quando il `Pixelmap` gruppo viene espanso, verrà visualizzata un'anteprima simile alla seguente:

![Screenshot della sezione Mappe pixel nel Visualizzazione risorse.](./media/guix-studio/pixelmap_view.png)

**Figura 15**

Le risorse mappa pixel sono costituite da una o più mappe pixel, ognuna con un'anteprima dell'immagine della mappa pixel a sinistra, le dimensioni della mappa pixel in pixel, un nome logico univoco e le dimensioni di archiviazione della mappa pixel nel file di risorse di output (in kb).

Il primo gruppo di mappe pixel comprende le mappe pixel di sistema predefinite richieste dai widget GUIX, ad esempio pulsanti di opzione e caselle di controllo. È possibile modificare i dati della mappa pixel associati alle mappe pixel di sistema, ma non è possibile modificare questi nomi di ID mappa pixel. Come illustrato in precedenza, sono presenti diverse mappe pixel personalizzate con nomi come "BACKGROUND" e "BUTTON_ACTIVE". Questi sono esempi di mappe pixel aggiunte da un utente al progetto che possono essere usate per eseguire il rendering di GX_PIXELMAP_BUTTON widget.

Poiché molti progetti contengono un numero elevato di mappe pixel, la visualizzazione mappa pixel consente di definire un numero qualsiasi di cartelle mappa pixel per organizzare le immagini mappa pixel. 

Per aggiungere una nuova cartella mappa pixel, fare clic con il pulsante destro del mouse sull'intestazione di sezione `Pixelmaps` ***Visualizzazione risorse*** selezionare "Aggiungi cartella".

Per modificare una risorsa mappa pixel, fare doppio clic (o fare clic con il pulsante destro del mouse e scegliere menu) sulla risorsa mappa pixel. Da questa finestra di dialogo la risorsa mappa pixel può essere modificata in base alle esigenze dell'interfaccia utente dell'applicazione. ***La figura 16** _ mostra la finestra di dialogo di modifica *quando si* fa doppio clic su _ RADIO_ON * .

![Screenshot della finestra di dialogo Modifica mappe pixel.](./media/guix-studio/image49.jpg)

**Figura 16**

La `Edit Pixelmap` finestra di dialogo consente di definire una nuova mappa pixel o di modificare il contenuto di una mappa pixel esistente. In background, GUIX Studio legge l'immagine di input e converte l'immagine nel formato che può essere usato `GUIX GX_PIXELMAP` dalla libreria GUIX. GUIX Studio converte anche lo spazio colore dell'immagine in ingresso nello spazio colore dello schermo in cui verrà usata questa mappa pixel.

Il primo campo di questa finestra di dialogo è il percorso dell'immagine di origine. GUIX Studio supporta l'input di file di immagine in formato PNG (.png) o JPEG (.jpg). È possibile usare il pulsante "Sfoglia" per trovare il file di input desiderato nel file system.

Se possibile, il percorso del file di immagine di input viene archiviato internamente usando un percorso relativo al progetto. Per questo motivo è importante mantenere tutti i file di immagine in un percorso comune e usare una struttura ad albero di directory comune per i progetti e i file di immagine per consentire di spostare i progetti GUIX Studio da una stazione di sviluppo a un'altra senza perdere traccia dei dati di immagine di input.

I `Pixelmap ID` campi consentono di specificare il nome logico della risorsa mappa pixel. Questo nome digitato qui deve essere univoco e deve seguire le regole della sintassi di denominazione delle variabili C.

La casella di controllo Specifica file di output consente di specificare un file di output univoco per ogni mappa pixel. Se questa casella di controllo non è selezionata, i dati della mappa pixel vengono scritti nel file di risorse predefinito per questa visualizzazione. Se la casella di controllo è selezionata, è possibile digitare un nome file specifico in cui verranno scritti i dati per questa mappa pixel. Lo scopo di questa opzione è quello di consentire di dividere i dati della mappa pixel, che possono essere matrici C molto grandi, in più file di output. Alcuni compilatori hanno difficoltà a gestire i file C che sono centinaia di migliaia di righe di codice sorgente.

La casella di controllo "Comprimi output" consente di specificare se l'output della mappa pixel usa un algoritmo di compressione GUIX proprietario. I file di output compressi sono in genere più piccoli, ma richiedono anche il tempo del processore per il rendering nella destinazione. Nella maggior parte dei casi si sceglie la compressione per le mappe pixel di grandi dimensioni e si usa un formato non compresso per le mappe pixel più piccole.

La casella di controllo determina il modo in cui GUIX Studio usa le informazioni sui canali alfa talvolta presenti `Include Alpha Channel` nei .png di input in formato alfa. Se questa casella di controllo è selezionata e la visualizzazione è in esecuzione a una profondità di colore di 16 bpp o superiore, GUIX Studio mantiene i dati alfa in ingresso completi nel file di output. Se questa casella di controllo non è selezionata, GUIX produrrà un file di output leggermente più piccolo. Questo file di output può includere trasparenza, ma non include informazioni complete sulla fusione alfa.

La casella di controllo indica a GUIX Studio di applicare un algoritmo di dithering avanzato durante la conversione dell'immagine di input da usare con una visualizzazione `Dither` con profondità del colore inferiore. Il dithering è in genere abilitato, ma può causare file di output di dimensioni maggiori se viene usata la compressione perché saranno presenti meno pixel ripetuti.

Dopo aver impostato tutte le opzioni nel modo desiderato, fare clic sul pulsante OK per produrre una nuova risorsa mappa pixel. GUIX Studio leggerà il file di immagine di input, lo decomprimerà, eseguirà la conversione dello spazio colore e il dithering, comprimerà facoltativamente i dati e salverà i dati in formato compatibile con `GX_PIXELMAP` GUIX. La nuova mappa pixel viene aggiunta alle risorse del progetto e resa disponibile per l'uso da parte dell'applicazione.

Per aggiungere una nuova risorsa mappa pixel, nella sezione del Visualizzazione risorse `Pixelmaps` selezionare il pulsante seguente: 

![Pulsante Aggiungi nuova mappa pixel.](./media/guix-studio/image50.jpg)

**Batch Pixelmap Edit**

Per modificare le proprietà di una serie di mappe pixel, fare clic con il pulsante destro del mouse sul gruppo o sulla cartella pixelmap e selezionare il **menu** Modifica mappe pixel per richiamare la finestra di dialogo Modifica mappe **pixel.**

![Screenshot della finestra di dialogo Modifica mappe multi pixel.](./media/guix-studio/batch_pixelmap_edit.jpg)

Descrizione dello stato della casella di controllo:

![Pulsante selezionato.](./media/guix-studio/checkbox_checked.jpg)
Questo stato indica che tutte le mappe pixel hanno la proprietà selezionata. È possibile deselezionare il pulsante per modificare la proprietà per tutte le mappe pixel.

![Pulsante Deselezionato.](./media/guix-studio/checkbox_unchecked.jpg)
Questo stato indica che tutte le mappe pixel hanno la proprietà deselezionata. È possibile selezionare il pulsante per modificare la proprietà per tutte le mappe pixel.

![Pulsante Non determinato.](./media/guix-studio/checkbox_undetermined.jpg)
Questo stato indica che le mappe pixel hanno uno stato diverso per la proprietà. È possibile selezionare o deselezionare il pulsante per modificare la proprietà per tutte le mappe pixel. In caso contrario, la proprietà rimane invariata.


## <a name="string-resources"></a>Risorse di tipo stringa

Quando il gruppo Stringhe viene espanso, verrà visualizzata un'anteprima della tabella delle stringhe di progetto, come illustrato di seguito:

![Screenshot del gruppo Stringhe espanso.](./media/guix-studio/string_res_view.png)

**Figura 17**

Le risorse stringa sono costituite da una o più stringhe, ognuna con un nome logico univoco. Ad esempio, nella **figura 17** il nome logico "PATIENT_LIST" è associato alla stringa "Patient List" mostrata a destra. Questa risorsa stringa viene usata ogni volta che l'applicazione PATIENT_LIST come stringa nelle proprietà dell'oggetto.

Tenere sempre presente che i nomi ID per tutti i tipi di risorse devono essere nomi di variabili compatibili con la sintassi C. Questi nomi verranno ampiamente usati quando i file di risorse del progetto e i file di specifiche vengono prodotti da Studio.

Per modificare una risorsa stringa, fare doppio clic (o fare clic con il pulsante destro del mouse e scegliere menu) sulla risorsa stringa per richiamare la finestra di dialogo ***Editor tabella** stringhe _. Nella finestra di _*_dialogo Editor tabella stringhe_*_ la risorsa stringa può essere modificata in base alle esigenze dell'interfaccia utente dell'applicazione. _*_La figura 18_*_ mostra la finestra di dialogo di modifica *quando si* fa doppio clic STRING_13 _ STRING_13 * .

In questo caso, il nome ID della stringa viene visualizzato a sinistra, dove il contenuto della stringa per il primo linguaggio o il linguaggio di riferimento viene visualizzato a destra. Naturalmente, il contenuto esatto della stringa è molto specifico per l'applicazione, ma il layout dell'anteprima del gruppo String è coerente.

GUIX Studio supporta testo statico e applicazioni multilingue definendo e mantenendo una tabella di stringhe. La tabella string definisce un ID stringa per ogni record e una costante stringa per ogni record per ogni lingua supportata.

Le lingue supportate dall'applicazione vengono definite tramite la finestra di dialogo Configurazione lingua, come illustrato di seguito:

![Screenshot della finestra di dialogo Configurazione lingua.](./media/guix-studio/config_languages.png)

**Figura 18**

La finestra di dialogo Configurazione linguaggio viene richiamata tramite l'interfaccia della | Comando Lingue nel menu dell'applicazione. Questa finestra di dialogo consente di definire il numero di lingue supportate dall'applicazione e il nome o l'ID lingua da associare a ogni lingua. Le lingue supportate possono essere modificate dopo la creazione del progetto, tuttavia se viene rimossa una lingua è necessario tenere presente che anche i dati stringa associati a tale lingua vengono rimossi e non possono essere recuperati.

La casella di controllo "**Definito in** modo statico " indica che la lingua selezionata verrà definita in modo statico nel formato del codice sorgente nel file di risorse generato. Se nessun linguaggio è definito in modo statico, il puntatore della tabella della lingua verrà impostato su NULL nella tabella di visualizzazione generata e un linguaggio deve essere caricato e installato dall'applicazione usando le API del caricatore di risorse binarie fornite dalla libreria GUIX.

La casella di controllo "**Support Offeri Text**" indica a GUIX Studio di abilitare il supporto per il rendering del testo bidirezionale. È consigliabile attivare questa casella di controllo se le stringhe che verranno immesse per questa lingua richiedono il rendering del testo bidirezionale.

La casella di controllo "**Generate Offeri Text in Display Order**" indica a GUIX Studio di generare testo bidirezionale nel file di output nell'ordine di visualizzazione. Se questa opzione è selezionata, non è necessaria alcuna elaborazione di runtime all'interno della libreria GUIX per eseguire correttamente il rendering del testo bidirezionale. Quando questa opzione è selezionata, il rendering del testo bidirezionale NON deve essere abilitato all'interno della libreria GUIX. Questa configurazione produce le migliori prestazioni di runtime, ma non supporta il rendering di stringhe di testo bidirezionali definite in modo dinamico.

Il primo linguaggio o linguaggio "Index 1" viene definito "linguaggio di riferimento". Questo è il linguaggio che GUIX Studio userà quando si definisce e si modifica la progettazione dell'interfaccia utente. Tutte le altre lingue nella tabella delle stringhe sono denominate lingue di traduzione. GUIX Studio supporta l'esportazione e l'importazione dei dati della tabella di stringhe nei file di dati in formato XLIFF o CSV standard del settore, utile per lo scambio di informazioni sulle stringhe con i traduttori che potrebbero aiutare lo sviluppatore dell'applicazione ad aggiungere traduzioni per le lingue supportate diverse dalla lingua di riferimento. Quando si esporta la tabella di stringhe GUIX in un file XLIFF o CSV, la lingua di riferimento insieme a una lingua di traduzione viene inclusa nel file di scambio di dati di stringa XLIFF o CSV. Analogamente, quando si importa un file XLIFF o CSV, i dati importati vengono usati per popolare una lingua di traduzione nella tabella GUIX String.

![Screenshot dell'editor della tabella di stringhe.](./media/guix-studio/image53.jpg)

**Figura 19**

La finestra di dialogo Editor tabella stringhe visualizza innanzitutto un elenco di ID stringa a sinistra, seguiti dai dati della stringa del linguaggio di riferimento. Se sono definite più lingue, una terza colonna mostra una delle lingue di traduzione supportate. È possibile aprire e chiudere la terza colonna facendo clic sulla piccola freccia nella parte superiore destra della colonna del linguaggio di riferimento.

Quando la colonna della lingua di traduzione è visibile, è possibile scorrere le lingue di traduzione contenute nel progetto facendo clic sulle piccole frecce in alto a destra nella colonna della lingua di traduzione dell'elenco di stringhe.

È possibile modificare un record di stringa facendo clic sul record nella tabella per selezionarlo. Quando viene selezionato un record, l'ID stringa del record e il contenuto della stringa vengono visualizzati nei campi sotto la visualizzazione tabella. È possibile digitare nuovi valori in questi campi per modificare l'ID stringa e il contenuto della stringa.

La casella sul lato destro della visualizzazione tabella mostra le anteprime dei widget che fanno riferimento alla stringa selezionata. Ciò è utile per determinare se una stringa modificata supererà un'area specifica del widget.

I campi a destra del contenuto della stringa includono:

- "Number of references" (Numero di riferimenti): questo campo indica la frequenza con cui viene usato un ID stringa specifico all'interno del progetto GUIX Studio. Se il conteggio dei riferimenti è 0, questa stringa può essere obsoleta e facoltativamente può essere rimossa dall'utente.
- Larghezza stringa (pixel) indica la larghezza di visualizzazione della stringa usando il tipo di carattere indicato.
- Il campo "Note" è un campo di commento facoltativo che consente di aggiungere informazioni sullo scopo o sull'uso di ogni stringa. Queste note sono incluse in tutti i file di dati stringa XLIFF esportati per aiutare i traduttori a eseguire traduzioni di stringhe accurate e significative.

Ogni volta che viene aperta la ***finestra di*** dialogo Editor tabella stringhe, è possibile aggiungere altre stringhe al progetto facendo clic sul pulsante Aggiungi stringa nella parte superiore della finestra di dialogo. Le stringhe obsolete o inutilizzate possono essere rimosse dal progetto selezionando prima la stringa e quindi facendo clic sul pulsante Elimina stringa nella parte superiore della finestra di dialogo.

Oltre ad aggiungere manualmente nuove stringhe al progetto usando la finestra di dialogo Editor tabella stringhe, è anche possibile aggiungere nuove stringhe indirettamente digitando semplicemente il contenuto della stringa nel campo "Testo" della visualizzazione Proprietà di qualsiasi widget che supporta il testo. In altre parole, quando si aggiungono nuovi widget nella visualizzazione di destinazione o si digitano informazioni di testo nella visualizzazione delle proprietà, queste azioni creano automaticamente nuove voci nella tabella delle stringhe del progetto.

## <a name="adding-language-translations"></a>Aggiunta di traduzioni linguistiche

L'editor della tabella delle stringhe di GUIX Studio supporta un flusso di lavoro di definizione della lingua che consente allo sviluppatore di creare un'applicazione usando la lingua principale, quindi di esportare i dati stringa in un file XML o CSV dello schema standard da inviare a un esperto di traduzione linguistica. Il file di traduzione viene quindi restituito allo sviluppatore, che può importare nuovamente le traduzioni in lingua nel progetto di Studio, aggiungendo così il supporto per una nuova lingua all'applicazione.

Questa funzionalità viene richiamata usando i pulsanti Esporta (per scrivere i dati stringa in un file) e Importa (per leggere le stringhe tradotte) nella parte superiore dell'Editor tabella stringhe. Il pulsante Esporta viene usato per creare un file XML o CSV dello schema XLIFF che contiene le stringhe della lingua di riferimento. Questo file può essere utilizzato da un traduttore usando strumenti ed editor che supportano il formato di file standard XLIFF o CSV.

Quando un esperto di traduzione restituisce il file XLIFF con le nuove traduzioni di stringa, è possibile usare il pulsante Importa per leggere i dati da questo file XLIFF o CSV. Se il file XLIFF o CSV contiene una nuova lingua, la nuova lingua viene aggiunta al progetto. Se il file XLIFF contiene nuovi dati stringa per una lingua esistente, questi nuovi dati vengono importati nel progetto. Le stringhe del linguaggio di riferimento non vengono modificate dall'operazione Import.

Quando si fa clic sul pulsante Esporta, viene visualizzata la finestra di dialogo Controllo esportazione XLIFF/CSV, illustrata di seguito:

![Screenshot della finestra di dialogo Controllo esportazione XLIFF/CSV.](./media/guix-studio/image54.jpg)

**Figura 20**

I campi Lingua di origine e Lingua di destinazione specificano le colonne della tabella di stringhe che verranno scritte nel file XLIFF o CSV come lingua di riferimento e lingua di traduzione. La lingua di origine è la stringa di riferimento e la lingua di destinazione è la lingua per cui il traduttore fornirà i dati della stringa tradotta.

Il campo Versione XLIFF specifica una delle due versioni principali del formato di file XLIFF, ovvero la versione 1.2 o la versione 2.0 (e versioni successive). Questi standard di formato di file XLIFF non sono compatibili ed è necessario conoscere la versione utilizzata per gli strumenti prima di usare i comandi di esportazione/importazione XLIFF. Altre informazioni sullo schema XLIFF e sugli standard XLIFF sono disponibili qui:

- versione 1.2: [https://docs.oasis-open.org/xliff/xliff-core/xliff-core.html](https://docs.oasis-open.org/xliff/xliff-core/xliff-core.html)
- versione 2.0: [https://docs.oasis-open.org/xliff/xliff-core/v2.0/os/xliff-core-v2.0os.pdf](https://docs.oasis-open.org/xliff/xliff-core/v2.0/os/xliff-core-v2.0-os.pdf)

I campi nome file di output e percorso di output consentono di specificare il nome file e il percorso in cui verrà scritto il file di output. Il nome del file dipende interamente dall'utente, tuttavia è consigliabile usare nomi che indicano le lingue di origine e di destinazione contenute nel file esportato.
