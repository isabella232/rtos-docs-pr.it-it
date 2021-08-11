---
title: Esempio semplice Project
description: Questo capitolo descrive come creare un progetto di esempio in GUIX Studio ed eseguire l'esempio in GUIX.
author: jdeere5220
ms.author: kemaxwel
ms.date: 9/30/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 8981bed62d2929703e4233d6a3ee31b692226c26d046875a235bf3aca32a7573
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116786566"
---
# <a name="chapter-10-example-project"></a>Capitolo 10: Esempio Project

Questo capitolo descrive come creare un progetto di esempio in GUIX Studio ed eseguire l'esempio in GUIX.

## <a name="create-new-project"></a>Creare un nuovo progetto

Il primo passaggio consiste nella creazione di un nuovo progetto e nella configurazione delle lingue e delle lingue supportate dal progetto. Quando si avvia GUIX Studio per la prima volta, viene visualizzata la ***schermata Progetti*** recenti:

![Screenshot della finestra di dialogo Progetti recenti di GUIX Studio.](./media/guix-studio/recent_projects.png)

**Figura 10.1**

Fare clic su ***Crea nuovo Project** _... per iniziare un nuovo progetto. Verrà visualizzata la finestra di dialogo _ *_New GUIX Project_** (Nuova GUIX Project *), illustrata di seguito:

![Screenshot della finestra di dialogo Crea nuovo Project GUIX Studio.](./media/guix-studio/create_new_project.png)

**Figura 10.2**

Digitare il nome "***new_example***" come nome del progetto. Project nomi devono usare regole di denominazione delle variabili C standard, ad esempio senza caratteri speciali o riservati. Digitare il percorso in cui salvare il progetto. Il percorso deve essere una directory file system directory, ad esempio GUIX Studio non creerà la directory se non esiste. Fare clic su "OK" per creare il progetto.

La schermata successiva mostrata è la Project configurazione, illustrata di seguito:

![Screenshot della finestra di dialogo Configura Project GUIX Studio.](./media/guix-studio/config_new_project.png)

**Figura 10.3**

Questa finestra di dialogo consente di specificare il numero di schermi che il progetto supporterà e di assegnare un nome a ogni visualizzazione. È necessario specificare il formato colore supportato da ogni visualizzazione e, facoltativamente, digitare un percorso per i file di output generati da Studio per ogni visualizzazione. La directory predefinita per i file di output è "***. \\***", ovvero i file di output C vengono scritti nella stessa directory del progetto stesso.

Per questo esempio, lasciare il valore ***Number of Displays** _ impostato su "1", digitare il nome "_*_main_display_*_" nel campo del nome visualizzato e selezionare " allocate _*_canvas memory_*_". Lasciare i valori predefiniti per i campi risoluzione, formato colore e directory e fare clic su _*_OK_**.

Il progetto dovrebbe ora essere aperto con l'IDE di Studio, come illustrato nella figura 10.4:

![Screenshot di un progetto aperto con l'IDE di Studio.](./media/guix-studio/initial_screen.png)

**Figura 10.4**

Quando si crea un nuovo progetto, GUIX Studio crea automaticamente una finestra predefinita come punto di partenza per il progetto. Questa casella grigia è la finestra predefinita creata automaticamente, centrata all'interno della *visualizzazione di destinazione.*

Se questa finestra non è selezionata, fare clic sulla finestra in modo che la casella di selezione tratteggiata sia disegnata intorno alla finestra. A questo punto, nella visualizzazione * Proprietà modificare il nome del _**_ _*_widget,_*_ l'ID del _*_widget,_*_ il lato sinistro, l'alto, la _*_larghezza,_*_ l'altezza e *_il_* bordo * in modo che corrispondano alle impostazioni indicate di seguito. _**_ _**_ Quando si apportano queste modifiche, le modifiche dovrebbero essere immediatamente effettive all'interno della visualizzazione di destinazione.

![Screenshot della finestra di dialogo Visualizzazione Proprietà.](./media/guix-studio/initial_window_properties.png)

**Figura 10.5**

Successivamente si aggiungerà una risorsa pixelmap da usare all'interno di un widget ***GX_ICON** _. Sono disponibili diverse icone con la distribuzione di GUIX Studio che funzionerà correttamente per questo esempio. Espandere le _*_mappe Visualizzazione risorse_*_ e fare clic sul pulsante _ Add New Pixelmap * (Aggiungi nuova *_mappa pixel*):_*

![Screenshot del pulsante Aggiungi nuova mappa pixel.](./media/guix-studio/image74.jpg)

Passare alla cartella di installazione di GUIX Studio e nella cartella ***./graphics/icons** _ selezionare il file _*_denominatoi_history_lg.png_*_. Fare _*_clic su_*_ Apri per aggiungere la risorsa al progetto. *_L'immagine _ Pixelmaps_** Visualizzazione risorse ora mostra un'anteprima dell'immagine icona appena aggiunta:

![Screenshot del controllo Pixelmaps Visualizzazione risorse.](./media/guix-studio/example_add_pixelmap.png)

**Figura 10.6**

Questa nuova risorsa immagine verrà utilizzata più avanti come parte della progettazione dell'interfaccia utente.

Analogamente all'aggiunta di una risorsa pixelmap, si aggiungerà una nuova risorsa tipo di carattere alla casella degli strumenti in modo da poter usare questo tipo di carattere più avanti nella progettazione. Espandere il nodo ***Tipi** di Visualizzazione risorse e fare clic sul _*_pulsante Aggiungi nuovo tipo di_*_ carattere. Questa azione richiama la finestra _*_di dialogo Aggiungi/Modifica_*_ tipo di carattere. Passare quindi ai tipi di carattere GUIX forniti nella cartella di installazione di GUIX Studio, _*_ . \\ fonts verasans_ _, quindi selezionare il file dei tipi di \\ carattere *TrueType denominato _*_VeraIt.ttf_*_. Digitare il tipo di carattere "_*_MEDIUM_ITALIC_" nel campo del nome del tipo di carattere e *_digitare "_*_30_**" nel campo altezza. Il dialogo dovrebbe ora essere simile al seguente:

![Screenshot della finestra di dialogo Modifica tipo di carattere.](./media/guix-studio/example_add_font.png)

**Figura 10.7**

Fare ***clic su OK*** per aggiungere questo tipo di carattere al progetto. Verrà ora visualizzato il tipo di carattere nel Visualizzazione risorse:

![Screenshot dei tipi di carattere nella Visualizzazione risorse.](./media/guix-studio/example_font_added.png)

**Figura 10.8**

Questo nuovo tipo di carattere verrà utilizzato più avanti nella progettazione dell'interfaccia utente.

Ora che sono disponibili alcune nuove risorse, è necessario aggiungere alcuni widget figlio alla schermata che possono usare queste risorse. Selezionare la finestra creata in precedenza denominata "***hello_world** _" facendo clic con il pulsante destro del mouse sulla finestra nella visualizzazione di destinazione. Nel menu a comparsa visualizzato selezionare il comando di menu _*_Inserisci, Testo,_*_ Richiedi per inserire un nuovo widget _ *_GX_PROMPT_** e collegare il widget alla finestra di sfondo. La finestra dovrebbe ora essere simile alla seguente:

![Screenshot di un menu a comparsa con la selezione di Prompt](./media/guix-studio/image78.jpg)

**Figura 10.9**

Fare clic sul tipo di carattere denominato "***MEDIUM_ITALIC** _" nel Visualizzazione risorse _ *_Caratteri_** e trascinare e rilasciare il tipo di carattere nel widget di richiesta. Modificare quindi le proprietà della richiesta come illustrato nella figura 10.10 per ridimensionare il prompt, impostare la trasparenza della richiesta e modificare il testo e lo stile della richiesta:

![Screenshot della visualizzazione Proprietà per il prompt.](./media/guix-studio/image79.jpg)

**Figura 10.10**

Potrebbe essere necessario scorrere verticalmente nella visualizzazione Proprietà per visualizzare ognuna di queste impostazioni a seconda della risoluzione dello schermo. Dopo aver apportato queste modifiche, la visualizzazione di destinazione dovrebbe essere simile alla seguente:

![Screenshot di un menu a comparsa con la Hello World selezionata.](./media/guix-studio/image80.jpg)

**Figura 10.11**

Successivamente si inserirà un widget di stile Pulsante icona sullo schermo. Selezionare la finestra di sfondo facendo clic su di essa e usare il menu di primo livello o il menu a comparsa con il pulsante destro del mouse per selezionare ***Inserisci, Pulsante,** Pulsante icona _ per aggiungere un nuovo _*_GX_ICON_BUTTON_*_ alla finestra. Fare clic sull'icona denominata _ *_I_HISTORY_LG_** aggiunta in precedenza e trascinarla sul pulsante icona. Usando la visualizzazione delle proprietà, modificare la posizione e le dimensioni dell'icona come illustrato di seguito:

![Screenshot della visualizzazione Proprietà per il widget di stile del pulsante icona.](./media/guix-studio/image81.jpg)

**Figura 10.12**

La schermata avrà un aspetto simile al seguente:

![Screenshot di un menu a comparsa con l'Hello World e gli Appunti.](./media/guix-studio/image82.jpg)

**Figura 10.13**

Questa operazione verrà chiamata completa per la semplice progettazione dello schermo di esempio. Le schermate effettive dell'applicazione saranno probabilmente molto più sofisticate, ma questo è sufficiente per illustrare come usare GUIX Studio per creare schermate dell'applicazione.

## <a name="generate-resource-and-application-code"></a>Generare il codice della risorsa e dell'applicazione

Il passaggio successivo consiste nel generare il file di risorse e il file di specifica che definiscono l'interfaccia utente di run-time GUIX incorporata. Per generare i file di output, è necessario fare clic con il pulsante destro del mouse sul nodo ***main_display** _ nella visualizzazione Project e selezionare il comando _ Genera file *_di_* risorse *. Si osserverà una finestra di informazioni che indica che i file di risorse sono stati generati, come illustrato nella figura 10.14:

![Screenshot di una finestra di dialogo di notifica.](./media/guix-studio/image83.jpg)

**Figura 10.14**

Fare clic su ***OK** _ per ignorare questa notifica e usare la stessa procedura per fare clic con il pulsante destro del mouse sul nodo _*_main_display_*_ e selezionare il comando _ *_Genera_* file di specifica *. Si dovrebbe osservare una finestra di notifica simile. A questo punto sono stati generati i file semplici dell'applicazione dell'interfaccia utente.

## <a name="create-user-supplied-code"></a>Creare il codice fornito dall'utente

Il passaggio successivo consiste nel creare un file di applicazione personalizzato che richiama la progettazione dello schermo generata da GUIX Studio. Usando l'editor preferito, creare un file di origine ***denominato new_example.c*** e immettere il codice sorgente seguente in questo file:

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

Il codice sorgente precedente crea un thread ThreadX tipico `GUIX New Example Thread` denominato con una dimensione dello stack di 4 KB. Il lavoro interessante inizia nella funzione denominata ***new_example_thread_entry***. Questa funzione è il punto in cui inizia l'esecuzione del thread specifico di GUIX.

La prima chiamata è alla funzione denominata ***gx_system_initialize***. Questa chiamata è sempre necessaria prima che qualsiasi altra API GUIX venga richiamata per preparare la libreria GUIX per il primo uso.

Successivamente, l'esempio chiama la ***funzione gx_studio_display_configure***. Questa funzione crea l'istanza di visualizzazione GUIX, installa la lingua richiesta della tabella delle stringhe dell'applicazione, installa il tema richiesto dalle risorse di visualizzazione e restituisce un puntatore alla finestra radice creata per questa visualizzazione. La finestra radice viene usata come elemento padre di tutte le schermate di primo livello che verranno visualizzate dall'applicazione.

L'esempio chiama quindi ***gx_studio_named_widget_create** _ per creare un'istanza della schermata _ *_hello_world_**. Questa funzione usa le strutture dei dati e la risorsa prodotti da GUIX Studio per creare un'istanza della schermata così come è stata definita. Il puntatore della finestra radice viene passato come secondo parametro a questa chiamata di funzione, ovvero si vuole che la schermata sia immediatamente collegata alla finestra radice. L'ultimo parametro è un puntatore restituito facoltativo che può essere usato se si vuole mantenere un puntatore alla schermata creata.

Viene chiamato next *** gx_widget_show** _ , che rende visibili la finestra radice e tutti i relativi elementi figlio, inclusa la schermata _ *_hello_world_**.

Infine, l'esempio ***chiama gx_system_start***. Questa funzione avvia l'esecuzione del ciclo di elaborazione degli eventi di sistema GUIX.

## <a name="build-and-run-the-example"></a>Compilare ed eseguire l'esempio

La compilazione e l'esecuzione dell'esempio sono specifiche per gli strumenti e l'ambiente di compilazione. È tuttavia possibile definire il processo generale:

1. Creare una nuova directory e un nuovo progetto di applicazione
1. Aggiungere questi file al progetto:

    **new_example_resources.c**

    **new_example_specification.c**

    **new_example.c**

1. Aggiungere i file di supporto di run-time Win32 dal percorso di installazione di GUIX Studio ***./win32_runtime***. Sono inclusi l'intestazione Win32 ThreadX e GUIX e i file della libreria di runtime.
1. Aggiungere la libreria GuiX Win32 (***gx.lib***) al progetto
1. Aggiungere la libreria Win32 ThreadX (***tx.lib***) al progetto
1. Compilare, collegare ed eseguire l'applicazione.
