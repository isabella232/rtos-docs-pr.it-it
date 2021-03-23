---
title: Progetto di esempio semplice
description: Questo capitolo descrive come creare un progetto di esempio in GUIX studio ed eseguire l'esempio in GUIX.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 3661396f097e0ed7bd872fae01a7bec9212001b9
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822331"
---
# <a name="chapter-10-example-project"></a>Capitolo 10: progetto di esempio

Questo capitolo descrive come creare un progetto di esempio in GUIX studio ed eseguire l'esempio in GUIX.

## <a name="create-new-project"></a>Creare un nuovo progetto

Il primo passaggio consiste nel creare un nuovo progetto e configurare le visualizzazioni e le lingue supportate dal progetto. Quando si avvia GUIX Studio per la prima volta, viene visualizzata la schermata ***progetti recenti*** :

![Screenshot della finestra di dialogo progetti recenti di GUIX Studio.](./media/guix-studio/recent_projects.png)

**Figura 10,1**

Fare clic sul pulsante ***Crea nuovo progetto** _... pulsante per avviare un nuovo progetto. Verrà visualizzata la finestra di dialogo _ *_nuovo progetto GUIX_**, mostrata di seguito:

![Screenshot della finestra di dialogo Crea nuovo progetto di GUIX Studio.](./media/guix-studio/create_new_project.png)

**Figura 10,2**

Digitare il nome "***new_example***" come nome del progetto. I nomi dei progetti devono usare le regole di denominazione delle variabili C standard, ovvero non caratteri speciali o riservati. Digitare il percorso della posizione in cui salvare il progetto. Il percorso deve essere una directory file system valida, ovvero GUIX Studio non creerà la directory se non esiste. Fare clic su "OK" per creare il progetto.

La schermata successiva mostra la schermata di configurazione del progetto, mostrata di seguito:

![Screenshot della finestra di dialogo Configura progetto di GUIX Studio.](./media/guix-studio/config_new_project.png)

**Figura 10,3**

Questa finestra di dialogo consente di specificare il numero di visualizzazioni che saranno supportate dal progetto e assegnare un nome a ogni visualizzazione. È necessario specificare il formato di colore supportato da ogni visualizzazione e, facoltativamente, digitare un percorso per i file di output generati da studio per ogni visualizzazione. La directory predefinita per i file di output è ***" \\ .***", ovvero i file di output C vengono scritti nella stessa directory del progetto stesso.

Per questo esempio, lasciare il segno ***Number of Displays** _ impostato su "1", digitare il nome "_*_main_display_*_" nel campo Display Name e selezionare "_*_allocate Canvas Memory_*_". Lasciare i valori predefiniti per la risoluzione, il formato di colore e i campi directory, quindi fare clic su _ *_OK_* *.

A questo punto si noterà che il progetto è aperto con l'IDE di studio, come illustrato nella figura 10,4:

![Screenshot di un progetto aperto con l'IDE di studio.](./media/guix-studio/initial_screen.png)

**Figura 10,4**

Quando si crea un nuovo progetto, GUIX Studio crea automaticamente una finestra predefinita come punto di partenza per il progetto. Questa casella grigia è la finestra predefinita creata per l'utente, centrata all'interno della *visualizzazione di destinazione*.

Se questa finestra non è selezionata, fare clic sulla finestra in modo da disegnare la casella di selezione tratteggiata intorno alla finestra. A questo punto, nella **visualizzazione delle proprietà***, modificare il nome del _*_widget_*_, l' _*_ID widget_*_, _*_Left_*_, _*_Top_*_, _*_Width_*_, _*_Height_*_ e _ *_Border_** in modo che corrispondano alle impostazioni indicate di seguito. Quando si apportano queste modifiche, le modifiche verranno applicate immediatamente all'interno della visualizzazione di destinazione.

![Screenshot della finestra di dialogo Visualizzazione proprietà.](./media/guix-studio/initial_window_properties.png)

**Figura 10,5**

Si aggiungerà quindi una risorsa Pixelmap da usare all'interno di un widget ***GX_ICON** _. Con la distribuzione di GUIX studio sono disponibili diverse icone che funzioneranno correttamente per questo esempio. Espandere il Visualizzazione risorse _*_pixelmaps_*_ e fare clic sul pulsante _ *_Aggiungi nuovo Pixelmap_**:

![Screenshot del pulsante Aggiungi nuovo Pixelmap.](./media/guix-studio/image74.jpg)

Passare alla cartella di installazione di GUIX studio e nella cartella ***./graphics/icons** _ selezionare il file denominato _*_i_history_lg.png_*_. Fare clic su _*_Apri_*_ per aggiungere la risorsa al progetto. Il Visualizzazione risorse _ *_pixelmaps_** dovrebbe ora visualizzare un'anteprima dell'immagine dell'icona appena aggiunta:

![Screenshot del Visualizzazione risorse pixelmaps.](./media/guix-studio/example_add_pixelmap.png)

**Figura 10,6**

Questa nuova risorsa immagine verrà usata in un secondo momento nell'ambito della progettazione dell'interfaccia utente.

Analogamente all'aggiunta di una risorsa Pixelmap, verrà aggiunta una nuova risorsa di tipo carattere alla casella degli strumenti in modo che sia possibile utilizzare questo tipo di carattere in un secondo momento nella progettazione. Espandere ***font** _ visualizzazione risorse e fare clic sul pulsante _*_Aggiungi nuovo tipo di carattere_*_ . Questa azione richiama la finestra di dialogo _*_Aggiungi/modifica_*_ carattere. Passare quindi ai tipi di carattere GUIX specificati nella cartella di installazione di GUIX studio, _*_ . \\ \\i tipi di carattere verasans_ *_ e selezionare il file del tipo di carattere TrueType denominato _*_VeraIt. ttf_*_. Digitare il tipo di carattere "_*_MEDIUM_ITALIC_*_" nel campo nome carattere e digitare "_*_30_* *" nel campo altezza. La finestra di dialogo dovrebbe ora essere simile alla seguente:

![Screenshot della finestra di dialogo Modifica carattere.](./media/guix-studio/example_add_font.png)

**Figura 10,7**

Fare clic su ***OK*** per aggiungere questo tipo di carattere al progetto. A questo punto il tipo di carattere dovrebbe essere visualizzato nel Visualizzazione risorse:

![Screenshot dei tipi di carattere nel Visualizzazione risorse.](./media/guix-studio/example_font_added.png)

**Figura 10,8**

Questo nuovo tipo di carattere verrà usato in un secondo momento nella progettazione dell'interfaccia utente.

Ora che sono disponibili alcune nuove risorse, è necessario aggiungere alcuni widget figlio alla schermata che può usare queste risorse. Selezionare la finestra creata in precedenza denominata "***hello_world** _" facendo clic con il pulsante destro del mouse sulla finestra nella visualizzazione di destinazione. Nel menu a comparsa visualizzato, selezionare il comando di menu _*_Inserisci, testo, prompt_*_ per inserire un nuovo widget _ *_GX_PROMPT_** e collegare il widget alla finestra di sfondo. La finestra dovrebbe ora essere simile alla seguente:

![Screenshot di un menu a comparsa con la selezione del prompt](./media/guix-studio/image78.jpg)

**Figura 10,9**

Fare clic sul carattere denominato "***MEDIUM_ITALIC** _" in _ *_fonts_** visualizzazione risorse, quindi trascinare e rilasciare il tipo di carattere nel widget della richiesta. Modificare quindi le proprietà del prompt come illustrato nella figura 10,10 per ridimensionare la richiesta, impostare la trasparenza della richiesta e modificare il testo e lo stile della richiesta:

![Screenshot della visualizzazione delle proprietà per la richiesta.](./media/guix-studio/image79.jpg)

**Figura 10,10**

Potrebbe essere necessario scorrere verticalmente nella visualizzazione proprietà per visualizzare ognuna di queste impostazioni, a seconda della risoluzione dello schermo. Dopo avere apportato queste modifiche, la visualizzazione di destinazione dovrebbe essere simile alla seguente:

![Screenshot di un menu a comparsa con la selezione del Hello World.](./media/guix-studio/image80.jpg)

**Figura 10,11**

A questo punto verrà inserito il widget icona stile pulsante icona sullo schermo. Selezionare la finestra in background facendo clic su di essa e usare il menu di primo livello o il menu a comparsa con il pulsante destro del mouse per selezionare ***Inserisci, pulsante, icona pulsante** _ per aggiungere una nuova _*_GX_ICON_BUTTON_*_ alla finestra. Fare clic sull'icona denominata _ *_I_HISTORY_LG_** aggiunta in precedenza e trascinarla sul pulsante icona. Utilizzando la visualizzazione proprietà, modificare la posizione e le dimensioni dell'icona come mostrato di seguito:

![Screenshot della visualizzazione delle proprietà per il widget stile pulsante icona.](./media/guix-studio/image81.jpg)

**Figura 10,12**

A questo punto la schermata dovrebbe essere simile alla seguente:

![Screenshot di un menu a comparsa con il Hello World e l'icona degli Appunti.](./media/guix-studio/image82.jpg)

**Figura 10,13**

Questa operazione verrà chiamata completa per la semplice progettazione della schermata di esempio. È probabile che le schermate dell'applicazione siano molto più sofisticate, ma ciò è sufficiente per illustrare come usare GUIX Studio per creare schermate delle applicazioni personalizzate.

## <a name="generate-resource-and-application-code"></a>Generare codice di risorse e applicazioni

Il passaggio successivo consiste nel generare il file di risorse e il file di specifica che definiscono l'interfaccia utente di run-time GUIX incorporata. Per generare i file di output, è necessario fare clic con il pulsante destro del mouse sul nodo ***main_display** _ nella visualizzazione del progetto e selezionare il comando _ *_genera file di risorse_**. Si osserverà una finestra informativa che indica che i file di risorse sono stati generati, come illustrato nella figura 10,14:

![Screenshot di una finestra di dialogo di notifica.](./media/guix-studio/image83.jpg)

**Figura 10,14**

Fare clic su ***OK** per chiudere la notifica e utilizzare la stessa procedura per fare clic con il pulsante destro del mouse sul nodo _*_main_display_*_ e selezionare il comando _ *_genera file di specifica_**. È necessario osservare una finestra di notifica simile. A questo punto sono stati generati i file dell'applicazione dell'interfaccia utente semplici.

## <a name="create-user-supplied-code"></a>Crea codice fornito dall'utente

Il passaggio successivo consiste nel creare il file dell'applicazione che richiama la progettazione della schermata generata da GUIX Studio. Usando l'editor preferito, creare un file di origine denominato ***new_example. c*** e immettere il codice sorgente seguente nel file:

```C

/* This is an example of the GUIX graphics framework in Win32. */
/* Include system files. */

#include <stdio.h>
#include "tx_api.h"
#include "gx_api.h"

/* Include GUIX resource and specification files for example. */

#include "new_example_resources.h"
#include "new_example_specifications.h"

/* Define the new example thread control block and stack. */

TX_THREAD new_example_thread;
UCHAR new_example_thread_stack[4096];

/* Define the root window pointer. */

GX_WINDOW_ROOT *root_window;

/* Define function prototypes. */

VOID new_example_thread_entry(ULONG thread_input);
UINT win32_graphics_driver_setup_24bpp(GX_DISPLAY *display);

int main()
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter();
    return(0);
}

VOID tx_application_define(void *first_unused_memory)
{
    /* Create the new example thread. */
    tx_thread_create(&new_example_thread, "GUIX New Example Thread", 
                      new_example_thread_entry, 0, 
                      new_example_thread_stack, sizeof(new_example_thread_stack),
                      1, 1, TX_NO_TIME_SLICE, TX_AUTO_START);
}

VOID new_example_thread_entry(ULONG thread_input)
{

    /* Initialize the GUIX library */
    gx_system_initialize();

    /* Configure the main display. */
    gx_studio_display_configure(MAIN_DISPLAY,                      /* Display to configure*/
                                win32_graphics_driver_setup_24bpp, /* Driver to use */
                                LANGUAGE_ENGLISH,                  /* Language to install */
                                MAIN_DISPLAY_DEFAULT_THEME,        /* Theme to install */
                                &root_window);                     /* Root window pointer */

    /* Create the screen - attached to root window. */

    gx_studio_named_widget_create("hello_world", (GX_WIDGET *) root_window, GX_NULL);

    /* Show the root window to make it visible. */
    gx_widget_show(root_window);

    /* Let GUIX run. */
    gx_system_start();

}
```

Il codice sorgente precedente crea un tipico thread ThreadX denominato `GUIX New Example Thread` con una dimensione dello stack di 4K byte. Il lavoro interessante inizia nella funzione denominata ***new_example_thread_entry***. Questa funzione è la posizione in cui inizia l'esecuzione del thread specifico di GUIX.

La prima chiamata è alla funzione denominata ***gx_system_initialize***. Questa chiamata è sempre obbligatoria prima che vengano richiamate altre API GUIX per preparare la libreria GUIX per il primo utilizzo.

Nell'esempio viene quindi chiamata la funzione ***gx_studio_display_configure***. Questa funzione crea l'istanza di visualizzazione GUIX, installa la lingua richiesta della tabella delle stringhe dell'applicazione, installa il tema richiesto dalle risorse di visualizzazione e restituisce un puntatore alla finestra radice creata per questa visualizzazione. La finestra radice viene usata come elemento padre di tutte le schermate di primo livello che l'applicazione visualizzerà.

Successivamente, l'esempio chiama ***gx_studio_named_widget_create** _ per creare un'istanza della schermata _ *_hello_world_**. Questa funzione usa le strutture di dati e le risorse generate da GUIX Studio per creare un'istanza della schermata come è stata definita. Il puntatore della finestra radice viene passato come secondo parametro a questa chiamata di funzione, ovvero si vuole che la schermata venga collegata immediatamente alla finestra radice. L'ultimo parametro è un puntatore restituito facoltativo che può essere usato se si vuole tenere un puntatore alla schermata creata.

Viene chiamato Next ***gx_widget_show** _, che rende visibile la finestra radice e tutti i relativi elementi figlio, inclusa la schermata _ *_hello_world_**.

Infine, nell'esempio viene chiamato ***gx_system_start***. Questa funzione inizia l'esecuzione del ciclo di elaborazione degli eventi di sistema GUIX.

## <a name="build-and-run-the-example"></a>Compilare ed eseguire l'esempio

Compilare ed eseguire l'esempio è specifico per gli strumenti e l'ambiente di compilazione. Tuttavia è possibile definire il processo generale:

1. Creare una nuova directory e un nuovo progetto di applicazione
1. Aggiungere questi file al progetto:

    **new_example_resources. c**

    **new_example_specification. c**

    **new_example. c**

1. Aggiungere i file di supporto della fase di esecuzione Win32 dal percorso di installazione di GUIX Studio ***./win32_runtime***. Sono inclusi i file di intestazione Win32 ThreadX e GUIX e la libreria di Runtime.
1. Aggiungere la libreria Win32 GUIX (***GX. lib***) al progetto
1. Aggiungere la libreria Win32 ThreadX (***TX. lib***) al progetto
1. Compilare, collegare ed eseguire l'applicazione.
