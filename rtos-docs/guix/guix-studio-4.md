---
title: Risorse di GUIX Studio
description: GUIX Studio fornisce la gestione di tutte le risorse dell'interfaccia utente che l'applicazione userà per i colori, i tipi di carattere, le mappe pixel e le stringhe. Le sezioni seguenti descrivono come aggiungere, modificare ed eliminare le risorse all'interno della progettazione della schermata dell'interfaccia utente.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 3c3769c3ddf0eef73546627f1f50fa3d11b16948
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823060"
---
# <a name="chapter-4-guix-studio-resources"></a>Capitolo 4: risorse di GUIX Studio

GUIX Studio fornisce la gestione di tutte le risorse dell'interfaccia utente che l'applicazione userà per i colori, i tipi di carattere, le mappe pixel e le stringhe. Le sezioni seguenti descrivono come aggiungere, modificare ed eliminare le risorse all'interno della progettazione della schermata dell'interfaccia utente. 

Tutte le operazioni di gestione delle risorse vengono eseguite all'interno della ***visualizzazione risorse** _ dell'interfaccia utente di GUIX studio, come illustrato di seguito in _ *_Figura 8_* *.

![Screenshot di GUIX Studio Visualizzazione risorse.](./media/guix-studio/image38.jpg)

**Figura 8**

## <a name="color-resources"></a>Risorse colore

La sezione ***Colors** _ del _*_visualizzazione risorse_*_ consente di gestire le risorse di colore. È possibile espandere questa visualizzazione facendo clic sul campo _ *+* * nell'intestazione della vista, ottenendo la visualizzazione mostrata sotto nella **_Figura 9_**:

![Screenshot della sezione colori della Visualizzazione risorse](./media/guix-studio/image_39.png)

**Figura 9**

Le risorse di colore sono costituite da uno o più colori, ognuno con un nome logico univoco. Nella **Figura 9** , ad esempio, l' **area di disegno** del nome logico, ovvero l'ID del colore di sistema per il colore di riempimento dello sfondo dello schermo, è associata al colore fisico nero. Questa risorsa di colore viene utilizzata ogni volta che l'applicazione specifica **GX_COLOR_ID_CANVAS** come colore nelle proprietà dell'oggetto.

Il colore "swatch" che indica il colore RGB viene visualizzato a sinistra, seguito dal nome ID del colore. È possibile modificare il valore RGB associato a qualsiasi nome ID in qualsiasi momento. Non è possibile modificare i nomi di ID colore di sistema predefiniti perché vengono usati internamente dalla libreria GUIX. È tuttavia possibile modificare i valori dei colori. La modifica di un valore di colore di sistema è una **modifica globale**. Ciò significa che qualsiasi widget che non dispone di un'assegnazione di colore specifica prenderà sul nuovo valore del colore di sistema.

È possibile modificare il nome e il valore del colore per i colori personalizzati aggiunti al tema.

Per modificare una risorsa di colore, fare doppio clic su (oppure fare clic con il pulsante destro del mouse e scegliere il menu) nella risorsa colore. Questa azione Visualizza la finestra di dialogo relativa alla definizione dei colori. Da questa finestra di dialogo è possibile modificare la risorsa colore in modo che corrisponda alle esigenze dell'interfaccia utente dell'applicazione. *La **Figura 10** _ Mostra la finestra di dialogo di modifica quando si fa doppio clic su _ *Canvas**. L'aspetto di questa finestra di dialogo verrà modificato in base alle impostazioni del formato colori della visualizzazione di destinazione.

![Screenshot della finestra di dialogo Modifica colore.](./media/guix-studio/edit_color.png)

**Figura 10**

L'aspetto della finestra di dialogo Modifica colore cambierà in base alla configurazione della profondità di colore e del formato colore della visualizzazione corrente.

Per aggiungere una nuova risorsa di colore, dalla sezione ***Colors** _ di _ *_visualizzazione risorse_** Selezionare il pulsante seguente:

![Pulsante Aggiungi nuovo colore](./media/guix-studio/image41.jpg)

Usare la finestra di dialogo colore risultante per aggiungere una nuova risorsa di colore, come illustrato di seguito nella **Figura 11**:*

![Screenshot del nuovo colore nella finestra di dialogo Modifica colore.](./media/guix-studio/new_color.png)

**Figura 11**

Dopo aver completato questi passaggi, selezionare **Salva** una nuova risorsa di colore con il nome **NEW_COLOR** con il colore verde fisico sarà disponibile per l'applicazione da usare.

**Considerazioni speciali per la modifica delle impostazioni del formato colori visualizzato:**

Quando si crea un nuovo progetto, viene automaticamente richiesto di configurare le visualizzazioni del progetto e il formato colori di ogni visualizzazione. Spesso queste selezioni vengono effettuate una volta e non è necessario modificare le impostazioni di configurazione.

È possibile determinare che è necessario modificare le impostazioni del formato del colore di visualizzazione in un secondo momento. In tal caso, GUIX Studio effettuerà una conversione ottimale del sistema corrente e dei valori RGB del colore utente dal formato di colore precedente al nuovo formato di colore. Questa conversione segue alcune regole logiche.

Per i colori definiti dall'utente, GUIX Studio tenta sempre di convertire il colore precedente nel colore corrispondente più vicino nel nuovo formato di colore. Se si esegue la conversione da una profondità di colore elevata, ad esempio 16 BPP 5:6:5, in un formato di colore grigio o monocromatico, questa modifica può comportare conversioni di colori indesiderate. Quando si apportano modifiche apportate alle impostazioni di profondità del colore di visualizzazione, potrebbero essere necessari alcuni aggiornamenti manuali alla nuova tabella dei colori definita dall'utente.

Per i colori di sistema predefiniti, GUIX Studio definisce internamente tre tabelle dei colori predefinite univoche. Una tabella dei colori predefinita viene usata per tutte le profondità dei colori superiori alla scala di grigia da 4 BPP, viene usata una seconda tabella dei colori predefinita per i formati di colore della scala grigia (1 BPP < display_color_format <= 4BPP) e infine una terza tabella dei colori di sistema predefinita viene usata per il formato di colore monocromatico.

Quando si cambia il formato di colore di visualizzazione utilizzando la finestra di dialogo configurazione progetto, vengono applicate le regole seguenti:

1) Se il vecchio e il nuovo formato dei colori di visualizzazione utilizzano tabelle dei colori di sistema predefinite diverse, come definito in precedenza, i colori di sistema vengono reimpostati sui colori predefiniti predefiniti. In altre parole, se si passa dalla scala da colore a grigio o dalla scala grigia a quella del colore monocromatico, i colori del sistema verranno reimpostati sui valori predefiniti definiti internamente per la nuova profondità di colore. Sebbene ciò possa causare la perdita di alcune informazioni personalizzate sui colori, questa soluzione offre un punto di partenza ragionevole quando si apportano modifiche sostanziali alle impostazioni del formato colori visualizzato.

2) Se il vecchio e il nuovo formato di colore utilizzano la stessa tabella dei colori predefinita, vale a dire che si sta apportando una modifica del formato colori meno drammatico, GUIX Studio testerà ogni colore di sistema per determinare se il valore RGB del colore di sistema è stato modificato rispetto al valore predefinito. Se il valore RGB del colore di sistema è stato modificato, GUIX Studio eseguirà una conversione con la corrispondenza migliore dal formato di colore precedente al nuovo formato colori. Se il colore di sistema non è stato modificato, verrà reimpostato sul colore predefinito per il nuovo formato colori.

**Considerazioni speciali per l'operazione in modalità tavolozza:**

Quando un progetto è configurato per il formato colore della tavolozza colori 256, l'utente può configurare il modo in cui viene definita la tavolozza da installare e utilizzare. È possibile accedere e modificare la definizione della tavolozza usando la configurazione | Finestra di dialogo temi e se il progetto è impostato per 8 BPP verrà visualizzato il pulsante "modifica tavolozza". Fare clic su questo pulsante per visualizzare la finestra di dialogo Modifica tavolozza:

![Screenshot della finestra di dialogo Modifica tavolozza.](./media/guix-studio/edit_palette.png)

GUIX Studio divide la tavolozza in due sezioni: la sezione "definito dall'utente" e la sezione "generata automaticamente". GUIX Studio esegue un sofisticato algoritmo di generazione della tavolozza ottimale per creare la tavolozza migliore per visualizzare le immagini incluse in ogni tema. È possibile suddividere il numero di voci della tavolozza che è necessario definire digitando un numero nel campo "voci predefinite tavolozza" e immettere qualsiasi valore RGB desiderato per uno di questi slot. Gli slot rimanenti verranno allocati a Studio per creare una tavolozza dei colori ottimale per la visualizzazione delle immagini.

Quando si esegue questa modalità, se si desidera modificare un colore definito nella visualizzazione risorse, l'editor dei colori consente di selezionare solo le voci della tavolozza definite. Ciò è dovuto al fatto che le voci della tavolozza rimanenti vengono generate automaticamente da GUIX studio e cambiano quando vengono modificate le immagini aggiunte al progetto.

Se è necessario visualizzare i tipi di carattere con alias durante l'esecuzione in modalità tavolozza 8bpp, è necessario definire una matrice di voci della tavolozza che creino una sfumatura per ogni colore di primo piano o di sfondo usato per visualizzare il testo con anti-aliasing. È possibile utilizzare 8 voci della tavolozza per la sfumatura per ogni combinazione di colori o 16 voci della tavolozza per una sfumatura più liscia. Questo numero di voci della tavolozza utilizzato è determinato dalla casella di controllo "numero di colori di testo con anti-aliasing in modalità tavolozza" nella finestra di dialogo configurazione progetto. È possibile utilizzare una sfumatura con solo otto voci per ridurre al minimo le voci della tavolozza utilizzate per ogni combinazione di colori oppure utilizzare 16 sfumature di voce per fornire l'aspetto del testo con anti-aliasing più semplice.

Per semplificare la definizione di una sfumatura di colore per la visualizzazione di testo con anti-aliasing o per generare una sfumatura di colore per il proprio utilizzo, la finestra di dialogo Modifica tavolozza fornisce un pulsante genera sfumatura. Per utilizzare questa funzionalità, è necessario innanzitutto assegnare i valori r:g: b dei colori sfumatura iniziale e finale.

Ad esempio, se si desidera visualizzare il testo rosso con anti-aliasing su uno sfondo grigio medio con otto voci della tavolozza a partire dall'indice 50, è necessario assegnare il valore r:g: b 255:0:0 all'indice della tavolozza 50 e il valore di r:g: b 128:128:128 all'indice della tavolozza 57. Immettere i valori di indice della tavolozza nei campi Start-index e end-index in questa finestra di dialogo e fare clic sul pulsante genera gradiente. Le voci della tavolozza da 51 a 56 verranno inizializzate per definire una transizione a sfumatura uniforme tra i colori delimitativi.

## <a name="font-resources"></a>Risorse dei tipi di carattere

Per gestire le risorse del tipo di carattere, la sezione ***Fonts** _ del _*_visualizzazione risorse_*_ deve prima essere espansa facendo clic sul *+* campo _ *, dando come risultato la finestra di dialogo riportata di seguito nella **_Figura 12_**:

![Screenshot della sezione dei tipi di carattere nel Visualizzazione risorse.](./media/guix-studio/image44.jpg)

**Figura 12**

Le risorse del tipo di carattere sono costituite da uno o più tipi di carattere, ognuno con un nome logico univoco. Nella **Figura 12** , ad esempio, il **sistema** di nomi logici è associato a un tipo di carattere specifico. Questa risorsa del tipo di carattere viene utilizzata ogni volta che l'applicazione specifica il **sistema** come tipo di carattere nelle proprietà dell'oggetto. Il gruppo di caratteri Mostra un'anteprima WYSIWYG dei glifi del tipo di carattere a sinistra, l'altezza del carattere in pixel, il nome dell'ID del tipo di carattere e la dimensione del carattere (in KB).

Nella vista precedente i primi quattro tipi di carattere sono i tipi di carattere predefiniti predefiniti richiesti dalla libreria GUIX. È possibile modificare i dati del tipo di carattere associati a questi tipi di carattere, ma non è possibile modificare questi nomi di ID.

L'ultimo carattere illustrato in precedenza, denominato "corsivo", è un tipo di carattere personalizzato che è stato aggiunto al progetto dall'utente.

Per modificare una risorsa del tipo di carattere, fare doppio clic su (oppure fare clic con il pulsante destro del mouse e scegliere) nella risorsa del tipo di carattere. Da questa finestra di dialogo la risorsa del tipo di carattere può essere modificata in base alle esigenze dell'interfaccia utente dell'applicazione. *La **Figura 13** _ Mostra la finestra di dialogo di modifica quando si fa doppio clic su _ *System**.

! [[Screenshot della finestra di dialogo di modifica quando si fa doppio clic su sistema.](./media/guix-studio/edit_system_font.png)

**Figura 13**

Per aggiungere una nuova risorsa del tipo di carattere, nella sezione ***Fonts** _ di _ *_visualizzazione risorse_** Selezionare il pulsante seguente:

![Pulsante Aggiungi nuovo carattere](./media/guix-studio/image46.jpg)

Verrà richiamata la `Font Edit` finestra di dialogo per aggiungere una nuova risorsa del tipo di carattere, come illustrato di seguito nella ***Figura 14***:

![Screenshot della finestra di dialogo di modifica per aggiungere una nuova risorsa del tipo di carattere.](./media/guix-studio/add_new_font.png)

**Figura 14**

I nuovi tipi di carattere GUIX vengono creati da GUIX Studio per il rendering di un tipo di carattere TrueType scelto a una determinata dimensione. Per questo motivo, la finestra di dialogo precedente richiede un percorso del tipo di carattere TrueType. È possibile usare il pulsante Sfoglia per passare a una directory contenente i file del tipo di carattere nel sistema di sviluppo. Alcuni tipi di carattere TrueType sono inclusi anche nella sottocartella GUIX/Fonts ogni volta che è stato installato GUIX Studio.

Se possibile, il percorso del file del tipo di carattere TrueType viene archiviato internamente usando un percorso relativo al progetto. Per questo motivo è importante che tutti i file dei tipi di carattere si trovino in una posizione comune e usino una struttura ad albero di directory comune per i progetti e i file del tipo di carattere per consentire lo spostamento di progetti GUIX studio da una stazione di sviluppo a un'altra.

Il campo del nome del tipo di carattere consente di specificare il nome dell'ID della risorsa del tipo di carattere. Si tratta dell'ID risorsa che verrà usato nel codice generato da GUIX studio e usato dall'applicazione anche quando si fa riferimento al tipo di carattere. Questo nome deve seguire i requisiti della sintassi di denominazione delle variabili C.

Dopo aver scelto un file del tipo di carattere TrueType da usare come input, immettere un nome logico del tipo di carattere.

La casella di controllo "**genera informazioni Kerning**" indica a GUIX studio di includere le informazioni sulla crenatura all'interno del tipo di carattere generato, usato per modificare le posizioni relative dei glifi successivi in una stringa. Se si vuole applicare la crenatura con le stringhe, è necessario usare un tipo di carattere che contiene informazioni sulla crenatura e attivare questa casella di controllo. Sarà inoltre necessario definire l'opzione di compilazione della libreria GUIX "GX_FONT_KERNING_SUPPORT" per supportare il rendering del testo con le informazioni sulla crenatura.

La casella di controllo "**Includi set di caratteri definito da tabella stringa**" indica a GUIX studio di includere i glifi a cui fa riferimento la tabella statica delle stringhe all'interno del tipo di carattere generato. È possibile includere glifi aggiuntivi selezionando e modificando gli intervalli di caratteri elencati di seguito, ma è possibile selezionare questa opzione per generare rapidamente il set di caratteri minimo necessario per visualizzare le stringhe definite nella tabella di stringhe. Naturalmente, se la tabella di stringhe USA glifi che non sono presenti nel tipo di carattere di origine TrueType, questi caratteri non saranno disponibili nel tipo di carattere GUIX e non verranno visualizzati nel sistema di destinazione.

Per generare un tipo di carattere più completo o un tipo di carattere che include caratteri che non possono essere usati nella tabella di stringhe definita in modo statico, è anche possibile selezionare gli intervalli di caratteri nell'elenco seguente. Si noti che è possibile selezionare un numero qualsiasi di intervalli di caratteri ed è possibile modificare il codice carattere iniziale e finale effettivo da includere in ogni intervallo selezionato.

Gli intervalli di caratteri e i nomi di pagina predefiniti sono solo suggerimenti che consentono di selezionare facilmente il set di caratteri necessario per le lingue attive attualmente in uso. I nomi di lingua elencati non hanno alcun effetto sul tipo di carattere GUIX generato ed è possibile digitare qualsiasi intervallo di caratteri esadecimali desiderato per qualsiasi intervallo di caratteri abilitato o selezionato.

Se ad esempio si desidera generare un tipo di carattere che contiene solo caratteri numerici, è possibile selezionare la tabella codici "ASCII", ma immettere il valore iniziale 0030 e il valore finale 0039 per generare un tipo di carattere contenente solo i caratteri numerici. Si noti che i valori dell'intervallo di caratteri codificati in esadecimale, ovvero la notazione normale per le tabelle di caratteri Unicode.

Per impostazione predefinita, GUIX studio e la libreria GUIX supportano i codici carattere 0x0000 tramite 0xFFFF, che include tutti i linguaggi attivi, i moduli matematici e altri simboli attualmente in uso. Se è necessario usare i codici carattere sopra il valore 0xFFFF, incluse alcune aree di uso privato, è necessario attivare la casella di controllo "supporto dell'intervallo di caratteri estesi". Quando questa casella di controllo è selezionata, GUIX Studio consente all'utente di specificare gli intervalli di caratteri da 0x0000 a 0x10ffff, che include gli intervalli di caratteri di uso privato Unicode. Se è necessario questo intervallo di caratteri estesi, sarà necessario definire anche l'opzione di compilazione della libreria GUIX "GX_EXTENDED_UNICODE_SUPPORT" in modo che la libreria GUIX supporti internamente i codici carattere a 32 bit, anziché la configurazione predefinita che supporta i codici carattere a 16 bit.

Se si seleziona la casella di controllo "Includi set di caratteri definiti da una tabella di stringhe" e uno o più intervalli di caratteri nell'elenco riportato di seguito, GUIX Studio combinerà queste selezioni nel superset degli intervalli selezionati e dei caratteri usati nella tabella di stringhe. Naturalmente, il tipo di carattere di origine TrueType selezionato deve contenere anche i caratteri necessari per consentire a GUIX studio di produrre glifi significativi per ogni valore di carattere richiesto.

Una volta determinato l'intervallo di caratteri, specificare l'altezza del carattere in pixel e il formato del carattere. Sono supportati sia i tipi di carattere con anti-alias che quelli binari. I tipi di carattere binari richiedono un'area di archiviazione dati statica inferiore, ma i tipi di carattere con alias producono l'aspetto migliore sulle destinazioni eseguite con scala di grigi a 4 BPP o profondità del colore superiore.

>[!NOTE]  
> *"Altezza carattere" si riferisce al quadrato EM del tipo di carattere. Nel tipo metal tradizionale, il quadrato EM era uguale all'altezza della linea del corpo in metallo da cui ogni lettera aumenta e ogni corpo Metal aveva le stesse dimensioni. In un tipo Metal, la dimensione fisica di una lettera non può superare in genere il quadrato EM. In tipo digitale, EM è una griglia di risoluzione arbitraria usata come spazio di progettazione di un tipo di carattere digitale. Per questi tipi di carattere digitali è comune che alcune funzionalità di glifo, ad esempio accenti e deodori, possano estendersi oltre i limiti del quadrato EM. Il risultato finale è che l'altezza del widget necessaria per visualizzare completamente un particolare tipo di carattere deve spesso essere leggermente più grande, quindi l'altezza del pixel del tipo di carattere richiesto.*

Una volta completati tutti i campi di configurazione dei tipi di carattere, fare clic sul pulsante OK per creare una nuova risorsa del tipo di carattere. GUIX Studio genererà un tipo di carattere compatibile con GUIX con le proprietà selezionate, aggiungerà il tipo di carattere alle risorse del progetto e renderà disponibile il tipo di carattere per l'applicazione.

## <a name="pixel-map-resources"></a>Risorse mappa pixel

Per gestire le risorse mappa pixel, la sezione ***pixel-Maps** _ del _*_visualizzazione risorse_*_ deve prima essere espansa facendo clic sul *+* campo _ *, dando come risultato la finestra di dialogo riportata di seguito nella **_Figura 15_**:

Quando il `Pixelmap` gruppo viene espanso, viene visualizzata un'anteprima simile alla seguente:

![Screenshot della sezione pixel-Maps nell'Visualizzazione risorse.](./media/guix-studio/pixelmap_view.png)

**Figura 15**

Le risorse mappa pixel sono costituite da una o più mappe pixel, ciascuna con un'anteprima dell'immagine della mappa pixel a sinistra, le dimensioni in pixel della mappa pixel, un nome logico univoco e le dimensioni di archiviazione con mapping pixel nel file di risorse di output (in KB).

Il primo gruppo di mappe pixel è costituito dalle mappe di pixel di sistema predefinite richieste dai widget GUIX, ad esempio pulsanti di opzione e caselle di controllo. È possibile modificare i dati della mappa pixel associati alle mappe pixel di sistema, tuttavia non è possibile modificare questi nomi di ID mappa pixel. In precedenza sono inoltre disponibili diverse mappe di pixel personalizzate con nomi quali "BACKGROUND" e "BUTTON_ACTIVE". Di seguito sono riportati alcuni esempi di mapping dei pixel che un utente ha aggiunto al progetto che potrebbe essere usato per eseguire il rendering di un widget GX_PIXELMAP_BUTTON.

Poiché molti progetti contengono un numero elevato di mappe pixel, la visualizzazione mappa pixel consente di definire un numero qualsiasi di cartelle mappa pixel per organizzare le immagini della mappa pixel. 

L'aggiunta di una nuova cartella mappa pixel viene eseguita facendo clic con il pulsante destro del mouse sull' `Pixelmaps` intestazione della sezione del ***visualizzazione risorse*** selezionando "Aggiungi cartella".

Per modificare una risorsa mappa pixel, fare doppio clic su (oppure fare clic con il pulsante destro del mouse e scegliere menu) nella risorsa mappa pixel. Da questa finestra di dialogo la risorsa mappa pixel può essere modificata in base alle esigenze dell'interfaccia utente dell'applicazione. ***Nella figura 16** _ viene visualizzata la finestra di dialogo di modifica quando si fa doppio clic su _ *RADIO_ON**.

![Screenshot della finestra di dialogo Edit pixel-maps.](./media/guix-studio/image49.jpg)

**Figura 16**

La `Edit Pixelmap` finestra di dialogo consente di definire una nuova mappa pixel o di modificare il contenuto di una mappa pixel esistente. Dietro le quinte, GUIX studio legge l'immagine di input e converte l'immagine nel `GUIX GX_PIXELMAP` formato che può essere usato dalla libreria GUIX. GUIX Studio converte anche lo spazio dei colori dell'immagine in arrivo nello spazio dei colori dello schermo in cui verrà usata la mappa pixel.

Il primo campo di questa finestra di dialogo è il percorso dell'immagine di origine. GUIX Studio supporta l'input dei file di immagine in formato PNG (PNG) o JPEG (jpg). È possibile usare il pulsante "Sfoglia" per trovare il file di input desiderato nel file system locale.

Se possibile, il percorso del file di immagine di input viene archiviato internamente usando un percorso relativo al progetto. Per questo motivo è importante mantenere tutti i file di immagine in un percorso comune e usare una struttura ad albero di directory comune per i progetti e i file di immagine, in modo da poter spostare i progetti di GUIX studio da una stazione di sviluppo a un'altra e non perdere traccia dei dati dell'immagine di input.

I `Pixelmap ID` campi consentono di specificare il nome logico della risorsa mappa pixel. Questo nome digitato deve essere univoco e deve seguire le regole di sintassi per la denominazione delle variabili C.

La casella di controllo specifica file di output consente di specificare un file di output univoco per ogni mappa pixel. Se questa casella di controllo non è selezionata, i dati della mappa pixel vengono scritti nel file di risorse predefinito per questa visualizzazione. Se la casella di controllo è selezionata, è possibile digitare un nome di file specifico in cui verranno scritti i dati per la mappa pixel. Lo scopo di questa opzione è consentire di dividere i dati della mappa pixel, che possono essere matrici C di dimensioni molto grandi, in più file di output. Alcuni compilatori faticano a gestire i file C che sono centinaia di migliaia di righe di codice sorgente.

La casella di controllo "Comprimi output" consente di specificare se l'output della mappa pixel usa un algoritmo di compressione GUIX proprietario. I file di output compressi sono in genere più piccoli, ma richiedono anche tempo del processore per il rendering sulla destinazione. Spesso si sceglie la compressione per le mappe pixel di grandi dimensioni e si usa un formato non compresso per le mappe pixel più piccole.

La `Include Alpha Channel` casella di controllo determina il modo in cui GUIX studio usa le informazioni sul canale alfa talvolta presenti nei file di input in formato png. Se questa casella di controllo è selezionata e la visualizzazione viene eseguita a una profondità di colore a 16 BPP o superiore, GUIX Studio manterrà i dati alfa in ingresso completi nel file di output. Se questa casella di controllo non è selezionata, GUIX produrrà un file di output leggermente più piccolo. Questo file di output può includere la trasparenza, ma non includerà informazioni complete sulla fusione alfa.

La `Dither` casella di controllo indica a GUIX studio di applicare un algoritmo di retinatura avanzata durante la conversione dell'immagine di input per l'utilizzo con una visualizzazione di profondità del colore inferiore. La dithering è in genere abilitata, ma può causare file di output di dimensioni maggiori se viene utilizzata la compressione perché saranno presenti meno pixel ripetuti.

Quando tutte le opzioni sono impostate nel modo desiderato, fare clic sul pulsante OK per produrre una nuova risorsa mappa pixel. GUIX Studio leggerà il file di immagine di input, lo decomprimerà, eseguirà la conversione dello spazio colore e la dithering, comprimerà facoltativamente i dati e salverà i dati in formato compatibile con GUIX `GX_PIXELMAP` . La nuova mappa pixel verrà aggiunta alle risorse del progetto e resa disponibile per l'uso da parte dell'applicazione.

Per aggiungere una nuova risorsa mappa pixel, nella `Pixelmaps` sezione del ***visualizzazione risorse*** Selezionare il pulsante seguente:

![Pulsante Aggiungi nuova mappa pixel.](./media/guix-studio/image50.jpg)

## <a name="string-resources"></a>Risorse di stringa

Quando il gruppo di stringhe viene espanso, viene visualizzata un'anteprima della tabella delle stringhe del progetto, come illustrato di seguito:

![Screenshot del gruppo di stringhe espanse.](./media/guix-studio/string_res_view.png)

**Figura 17**

Le risorse di stringa sono costituite da una o più stringhe, ognuna con un nome logico univoco. Nella **Figura 17** , ad esempio, il nome logico "PATIENT_LIST" è associato alla stringa "patient list" visualizzata a destra. Questa risorsa di stringa viene utilizzata ogni volta che l'applicazione specifica PATIENT_LIST come stringa nelle proprietà dell'oggetto.

Tenere sempre presente che i nomi di ID per tutti i tipi di risorsa devono essere nomi di variabile compatibili con la sintassi C. Questi nomi verranno usati ampiamente quando i file di risorse del progetto e i file delle specifiche vengono prodotti da studio.

Per modificare una risorsa di stringa, fare doppio clic su (oppure fare clic con il pulsante destro del mouse e scegliere) nella risorsa di stringa per richiamare la finestra di dialogo ***Editor tabella stringhe** _. Dalla finestra di dialogo _*_Editor tabelle di stringhe_*_ la risorsa stringa può essere modificata in base alle esigenze dell'interfaccia utente dell'applicazione. La _*_Figura 18_*_ Mostra la finestra di dialogo di modifica quando si fa doppio clic su _ *STRING_13**.

In questo caso, il nome dell'ID di stringa viene visualizzato a sinistra, che indica il contenuto della stringa per la prima o la lingua di riferimento a destra. Naturalmente, il contenuto esatto della stringa è molto specifico per l'applicazione, tuttavia il layout dell'anteprima del gruppo di stringhe è coerente.

GUIX Studio supporta testo statico e applicazione multilingue mediante la definizione e la gestione di una tabella di stringhe. La tabella delle stringhe definisce un ID di stringa per ogni record e una costante di stringa per ogni record per ogni lingua supportata.

Le lingue che devono essere supportate dall'applicazione vengono definite tramite la finestra di dialogo di configurazione della lingua, Mostra qui:

![Screenshot della finestra di dialogo di configurazione della lingua.](./media/guix-studio/config_languages.png)

**Figura 18**

La finestra di dialogo di configurazione della lingua viene richiamata tramite la configurazione | Lingue dal menu applicazione. Questa finestra di dialogo consente di definire il numero di lingue che devono essere supportate dall'applicazione e il nome o l'ID lingua da associare a ogni lingua. Le lingue supportate possono essere modificate dopo la creazione del progetto. Tuttavia, se viene rimossa una lingua, è necessario tenere presente che anche i dati di stringa associati a tale lingua vengono rimossi e non possono essere recuperati.

La casella di controllo "**staticly defined**" indica che la lingua selezionata verrà definita in modo statico nel formato del codice sorgente nel file di risorse generato. Se nessuna lingua è definita in modo statico, il puntatore della tabella della lingua verrà impostato su NULL nella tabella di visualizzazione generata e una lingua deve essere caricata e installata dall'applicazione usando le API del caricatore di risorse binario fornite dalla libreria GUIX.

La casella di controllo "**supporto del testo bidi**" indica a GUIX studio di abilitare il supporto per il rendering del testo bidirezionale. È necessario attivare questa casella di controllo se le stringhe da immettere per questa lingua richiedono il rendering del testo bidirezionale.

La casella di controllo "**genera testo bidi in ordine di visualizzazione**" indica a GUIX studio di generare testo bidirezionale nel file di output nell'ordine di visualizzazione. Se questa opzione è selezionata, non è necessaria alcuna elaborazione del runtime all'interno della libreria GUIX per eseguire correttamente il rendering del testo bidirezionale. Quando questa opzione è selezionata, il rendering bidirezionale del testo non deve essere abilitato nella libreria GUIX. Questa configurazione consente di ottenere le migliori prestazioni di runtime, ma non supporta il rendering di stringhe di testo bidirezionali definite in modo dinamico.

La lingua del primo o del "indice 1" è detta "lingua di riferimento". Questo è il linguaggio che GUIX Studio userà per la definizione e la modifica della progettazione dell'interfaccia utente. Tutti gli altri linguaggi della tabella di stringhe sono detti linguaggi di traduzione. GUIX Studio supporta l'esportazione e l'importazione dei dati della tabella di stringhe nei file di dati in formato XLIFF o CSV standard di settore, utile per lo scambio di informazioni di stringa con i traduttori che possono assistere lo sviluppatore di applicazioni con l'aggiunta di traduzioni per le lingue da supportare diverse dalla lingua di riferimento. Quando si esporta la tabella delle stringhe GUIX in un file XLIFF o CSV, la lingua di riferimento insieme a un linguaggio di traduzione viene inclusa nel file di scambio dei dati di stringa XLIFF o CSV. Analogamente, quando si importa un file XLIFF o CSV, i dati importati vengono usati per popolare un linguaggio di traduzione nella tabella di stringhe GUIX.

![Screenshot dell'Editor tabella di stringhe.](./media/guix-studio/image53.jpg)

**Figura 19**

Nella finestra di dialogo Editor tabelle di stringhe viene innanzitutto visualizzato un elenco di ID di stringa a sinistra, seguiti dai dati di stringa della lingua di riferimento. Se viene definita più di una lingua, una terza colonna Mostra uno dei linguaggi di traduzione supportati. È possibile aprire e chiudere la terza colonna facendo clic sulla piccola freccia nella parte superiore destra della colonna lingua di riferimento.

Quando la colonna lingua di traduzione è visibile, è possibile scorrere le lingue di traduzione contenute nel progetto facendo clic sulle piccole frecce nella parte superiore destra della colonna lingua di traduzione dell'elenco di stringhe.

È possibile modificare un record di stringa facendo clic sul record nella tabella per selezionarlo. Quando si seleziona un record, l'ID della stringa di record e il contenuto della stringa vengono visualizzati nei campi sotto la visualizzazione tabella. È possibile digitare nuovi valori in questi campi per modificare l'ID di stringa e il contenuto della stringa.

La casella sul lato destro della visualizzazione tabella mostra le anteprime dei widget che fanno riferimento alla stringa selezionata. Questa operazione è utile per stabilire se una stringa modificata supererà un'area specifica del widget.

I campi a destra del contenuto della stringa includono:

- "Numero di riferimenti": questo campo indica la frequenza con cui viene usato un particolare ID di stringa all'interno del progetto GUIX Studio. Se il conteggio dei riferimenti è 0, questa stringa può essere obsoleta e facoltativamente può essere rimossa dall'utente.
- Larghezza stringa (pixel) indica la larghezza di visualizzazione della stringa usando il tipo di carattere indicato.
- Il campo "note" è un campo di commento facoltativo che consente di aggiungere informazioni sullo scopo o sull'uso di ogni stringa. Queste note sono incluse in tutti i file di dati di stringa XLIFF esportati per aiutare i traduttori a eseguire traduzioni di stringhe accurate e significative.

Ogni volta che si apre la finestra di dialogo ***Editor tabelle di stringhe*** , è possibile aggiungere altre stringhe al progetto facendo clic sul pulsante Aggiungi stringa nella parte superiore della finestra di dialogo. È possibile rimuovere le stringhe obsolete o inutilizzate dal progetto selezionando prima la stringa, quindi facendo clic sul pulsante Elimina stringa nella parte superiore della finestra di dialogo.

Oltre a aggiungere manualmente nuove stringhe al progetto tramite la finestra di dialogo Editor tabelle di stringhe, è anche possibile aggiungere indirettamente nuove stringhe semplicemente digitando contenuto stringa nel campo "testo" della visualizzazione proprietà di qualsiasi widget che supporti il testo. In altre parole, quando si aggiungono nuovi widget nella visualizzazione di destinazione o si digitano informazioni di testo nella visualizzazione delle proprietà, queste azioni creano automaticamente nuove voci nella tabella delle stringhe del progetto.

## <a name="adding-language-translations"></a>Aggiunta di traduzioni della lingua

L'Editor tabelle di stringhe di GUIX Studio supporta un flusso di lavoro di definizione della lingua che consente allo sviluppatore di creare un'applicazione usando la lingua principale, quindi esportare i dati stringa in un file XML dello schema standard o CSV da inviare a un esperto di traduzione della lingua. Il file di traduzione viene quindi restituito allo sviluppatore, che può importare di nuovo le traduzioni della lingua nel progetto di studio, aggiungendo in tal modo il supporto per una nuova lingua alla propria applicazione.

Questa funzionalità viene richiamata usando l'esportazione (per scrivere i dati stringa in un file) e i pulsanti Importa (per leggere le stringhe tradotte) nella parte superiore dell'Editor tabella di stringhe. Il pulsante Esporta consente di creare un file XML dello schema XLIFF o un file CSV contenente le stringhe della lingua di riferimento. Questo file può essere utilizzato da un convertitore utilizzando gli strumenti e gli editor che supportano il formato di file XLIFF o CSV standard.

Quando un esperto di traduzione restituisce il file XLIFF con le nuove traduzioni di stringa, è possibile usare il pulsante Importa per leggere i dati da questo file XLIFF o CSV. Se il file XLIFF o CSV contiene una nuova lingua, la nuova lingua verrà aggiunta al progetto. Se il file XLIFF contiene nuovi dati stringa per una lingua esistente, i nuovi dati vengono importati nel progetto. Le stringhe della lingua di riferimento non vengono modificate dall'operazione di importazione.

Quando si fa clic sul pulsante Esporta, viene visualizzata la finestra di dialogo XLIFF/CSV Export Control, mostrata di seguito:

![Screenshot della finestra di dialogo di controllo esportazione XLIFF/CSV.](./media/guix-studio/image54.jpg)

**Figura 20**

I campi lingua di origine e lingua di destinazione specificano quali colonne della tabella di stringhe verranno scritte nel file XLIFF o CSV come lingua di riferimento e linguaggio di traduzione. La lingua di origine è costituita dalle stringhe di riferimento e la lingua di destinazione è la lingua per cui il traduttore fornirà i dati delle stringhe tradotte.

Il campo della versione XLIFF specifica una delle due versioni principali del formato di file XLIFF, ovvero la versione 1,2 o la versione 2,0 e successive. Questi standard del formato di file XLIFF sono incompatibili ed è necessario individuare la versione usata dagli strumenti prima di usare i comandi di esportazione/importazione di XLIFF. Altre informazioni sullo schema XLIFF e sugli standard XLIFF sono disponibili qui:

- versione 1,2: [https://docs.oasis-open.org/xliff/xliff-core/xliff-core.html](https://docs.oasis-open.org/xliff/xliff-core/xliff-core.html)
- versione 2,0: [https://docs.oasis-open.org/xliff/xliff-core/v2.0/os/xliff-core-v2.0os.pdf](https://docs.oasis-open.org/xliff/xliff-core/v2.0/os/xliff-core-v2.0-os.pdf)

I campi output filename e percorso output consentono di specificare il nome file e il percorso in cui verrà scritto il file di output. Il nome file è interamente per l'utente, ma è consigliabile usare nomi che indicano le lingue di origine e di destinazione contenute nel file esportato.
