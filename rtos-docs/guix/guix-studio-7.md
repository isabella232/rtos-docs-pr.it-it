---
title: Definizione del flusso dello schermo
description: GUIX Studio supporta la generazione automatica e l'esecuzione di logica di transizione dello schermo.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 1c590725281c785181bcb4c5852346bc973c24d1
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104822202"
---
# <a name="chapter-7-defining-screen-flow"></a>Capitolo 7: definizione del flusso dello schermo

GUIX Studio supporta la generazione automatica e l'esecuzione di logica di transizione dello schermo. L'utente definisce la logica di transizione dello schermo mediante la creazione e la modifica di un diagramma di flusso dello schermo grafico. Quando un diagramma di flusso dello schermo viene aggiunto al progetto, Abilita due funzionalità importanti: 1) l'applicazione può essere eseguita dall'ambiente Studio e 2) Studio genera automaticamente i gestori eventi e la logica di transizione dello schermo per implementare il flusso dello schermo designato all'interno del file con estensione c delle specifiche generate, rimuovendo questo onere dal programma dell'applicazione. 

L'esecuzione dell'applicazione sul desktop dall'interno dell'ambiente Studio è una funzionalità utile che consente di risparmiare tempo in quanto non è necessario eseguire un ciclo di compilazione/collegamento per eseguire l'applicazione. Esistono naturalmente limitazioni a ciò che può essere fatto senza compilare l'applicazione. Le funzioni di disegno personalizzate, i gestori eventi personalizzati e la gestione di eventi complessi non sono disponibili quando si esegue l'applicazione dall'ambiente GUIX Studio. Questa funzionalità consente comunque di generare automaticamente la logica di transizione dello schermo e di programmare le animazioni da eseguire per la transizione da una schermata a un'altra. Questi effetti e animazioni possono essere osservati direttamente dall'ambiente GUIX Studio.

Si noti che quando si definiscono il flusso dello schermo, i trigger e le azioni che verranno descritti nei paragrafi seguenti, non solo si Abilita l'esecuzione dell'interfaccia utente dall'ambiente Studio, ma si abilita anche GUIX Studio per generare la logica all'interno del file delle specifiche che gestirà gli eventi e intraprenderà le azioni in base a tali eventi, ad esempio la transizione da una schermata all'altra

## <a name="configuring-screen-flow"></a>Configurazione del flusso dello schermo

Prima che un'applicazione possa essere eseguita dall'interno dell'ambiente di studio, è necessario definire alcuni aspetti. In primo luogo, la schermata o le schermate di livello superiore che devono essere visualizzate all'avvio del programma devono essere indicate selezionando la proprietà "visibile all'avvio" nella visualizzazione delle proprietà di studio. Questo flag indica che questa schermata deve essere visualizzata inizialmente all'avvio del programma. Se lo si desidera, più di una schermata può avere questa designazione.

Dopo aver definito le schermate visibili all'avvio, l'utente può definire il flusso dell'applicazione dell'interfaccia utente da schermo a schermo. GUIX Studio fornisce un diagramma grafico di flusso dello schermo per definire la logica di transizione dello schermo. È sufficiente selezionare la selezione di menu ***Configura, flusso dello schermo** _ per visualizzare la finestra di dialogo di modifica del flusso dello schermo, vedere la schermata in _ *_Figura 30_* *.

![Screenshot della finestra di dialogo flusso schermata di GUIX Studio.](./media/guix-studio/config_screen_flow.png)

**Figura 30**

Ogni schermata di primo livello definita nel progetto verrà visualizzata come una casella che mostra il nome della schermata. Questa casella è un segnaposto che rappresenta ogni schermata di primo livello definita nel progetto. Queste caselle possono essere spostate e ridimensionate a seconda delle esigenze. Quando è stata definita una transizione da una schermata di primo livello a un'altra, viene visualizzata una linea di connessione con una freccia tra due schermate che indica le transizioni da una schermata a un'altra.

La visualizzazione albero nella parte sinistra del diagramma di flusso dello schermo mostra ogni schermata di primo livello e si è in grado di selezionare le schermate di primo livello da disegnare nel diagramma del flusso dello schermo.

Il diagramma di flusso dello schermo è scorrevole. È possibile trascinare un blocco dello schermo verso il basso e verso destra all'esterno dell'area visibile per ingrandire la finestra scorrevole. Quando la finestra scorrevole viene ingrandita, è possibile eseguire lo zoom indietro per adattarla all'area visibile scorrendo la rotellina del mouse verso il basso. Se la finestra scorrevole è ingrandita, è possibile aumentare il numero di blocchi scorrendo la rotellina del mouse verso l'alto.

Per definire le transizioni per una schermata, fare clic con il pulsante destro del mouse sul segnaposto della schermata per visualizzare una finestra di dialogo Modifica elenco trigger, vedere la ***Figura 31***.

![Screenshot della finestra di dialogo di modifica dell'elenco dei trigger di GUIX Studio.](./media/guix-studio/edit_trigger_list.png)

**Figura 31**

Nella finestra di dialogo Modifica trigger sono elencati gli eventi definiti dall'utente che attiverà una transizione dello schermo, motivo per cui questi eventi vengono chiamati trigger. I trigger sono in genere segnali generati da uno o più widget figlio della schermata selezionata.

Per definire un nuovo trigger, selezionare il pulsante ***Aggiungi nuovo trigger** _ nella finestra di dialogo Modifica elenco trigger per visualizzare la finestra di dialogo Aggiungi trigger visualizzata in _ *_Figura 32_* *.

![Screenshot della finestra di dialogo Aggiungi trigger di GUIX Studio.](./media/guix-studio/add_trigger_for.png)

**Figura 32**

È possibile definire il tipo di evento che attiverà un nuovo set di azioni e definire le azioni che verranno eseguite quando viene ricevuto l'evento di attivazione.

Dopo aver definito il tipo di evento che si vuole usare per attivare una nuova transizione della schermata di animazione, salvare il nuovo trigger che verrà visualizzato nella finestra di dialogo Modifica elenco di trigger.

È possibile modificare questo evento (senza modificare le azioni correlate da intraprendere) selezionando l'evento nella finestra di dialogo Modifica elenco di trigger e selezionando il pulsante ***modifica evento trigger*** .

Analogamente, è possibile rimuovere qualsiasi evento trigger dall'elenco selezionando l'evento e facendo clic sul pulsante ***Elimina trigger selezionato*** .

Per specificare l'animazione o la transizione dello schermo che deve essere eseguita in base a un evento trigger specifico, selezionare l'evento di attivazione e fare clic sul pulsante ***Modifica azione*** /i. Si noti che è possibile attivare più di un'azione in base a ogni trigger definito.

Il pulsante **Modifica azione** /i Visualizza la finestra di dialogo Modifica azioni per trigger, illustrata nella figura 33: 

![Screenshot della finestra di dialogo Modifica azioni di GUIX Studio per trigger.](./media/guix-studio/edit_actions_for_trigger.png)

**Figura 33**

Questa finestra di dialogo consente di definire un numero qualsiasi di azioni da implementare in base a questo evento trigger. È possibile assegnare a ogni azione un nome significativo che consenta di associare ogni definizione di azione a un'animazione o a una transizione visiva. Nell'esempio precedente sono state definite due azioni denominate "fade_in_text_screen" e "fade_out_button_screen".

La definizione di una nuova azione da implementare, fare clic sul pulsante Aggiungi nuova azione, che visualizza la finestra di dialogo Seleziona azione, Figura 34:

![Screenshot della finestra di dialogo Seleziona azione di GUIX Studio.](./media/guix-studio/select_action.png)

**Figura 34**

I tipi di azione disponibili includono:

- **Animazione**: avvia un'animazione con le informazioni specificate.
- **Connetti**: collegare la schermata di destinazione alla schermata padre, se la schermata padre non è specificata, la schermata di destinazione verrà collegata alla finestra radice.
- **Scollega**: scollegare la schermata di destinazione dal relativo elemento padre.
- **Nascondi**: nasconde la schermata di destinazione.
- **Pop dello stack dello schermo**: pop una schermata dallo stack interno dello schermo.
- **Push dello stack dello schermo**: effettuare il push di un puntatore dello schermo allo stack interno dello schermo.
- **Reset dello stack dello schermo**: rimuovere tutti i puntatori alla schermata dallo stack interno dello schermo.
- **Mostra**: Mostra la schermata di destinazione.
- **Imposta/Nascondi**: Connetti la schermata di destinazione all'elemento padre della schermata corrente e scollega la schermata corrente dal relativo elemento padre.
- **Finestra Execute**: esegue la schermata di destinazione modale.
- **Window Execute stop**: termina l'esecuzione modale della schermata corrente.

Una volta definita un'azione da eseguire in base all'evento del trigger selezionato, tale azione verrà visualizzata nella finestra di dialogo Modifica azioni per trigger. È possibile selezionare questa azione per modificare i parametri dell'azione, come illustrato nella Figura 35.

![Screenshot della finestra di dialogo Modifica azioni di GUIX Studio per trigger.](./media/guix-studio/edit_actions_for_trigger.png)

**Figura 35**

Se il tipo di azione è un'animazione, viene visualizzato un set di parametri di animazione a destra per consentire di definire una diapositiva e/o un'animazione di tipo dissolvenza da eseguire. Quando un'azione di animazione viene completata, è anche possibile determinare se l'animazione deve essere scollegata automaticamente dall'elemento padre e/o inserita nello stack dello schermo interno, che risulta spesso utile quando si definiscono i sistemi di menu a più livelli.

Per le animazioni di scorrimento e dissolvenza, è anche possibile definire la funzione di interpolazione da usare selezionando il pulsante di selezione funzione di interpolazione. Le funzioni di interpolazione sono diverse curve progettate per simulare più accuratamente gli eventi di spostamento della vita reale. Selezionando questo pulsante viene visualizzata la finestra di dialogo **Seleziona funzione di interpolazione** , Figura 36:

![Screenshot della finestra di dialogo Seleziona funzione di interpolazione di GUIX Studio.](./media/guix-studio/easing_function_select.png)

**Figura 36**

Se si definiscono più azioni da associare a un evento trigger, può essere utile assegnare a ogni azione un nome significativo. I nomi delle azioni devono seguire le regole di denominazione della sintassi C, in quanto questi nomi verranno usati all'interno del file delle specifiche generate per definire le tabelle degli eventi e delle azioni.

Quando si definiscono gli eventi e le azioni del trigger all'interno di GUIX studio, i gestori eventi automatici vengono generati all'interno del file delle specifiche del progetto per gestire questi eventi ed eseguire le azioni specificate. Ciò significa che non è necessario gestire questi eventi nel codice dell'applicazione, anche se gli eventi trigger vengono ancora passati a tutti i gestori eventi personalizzati definiti. In altre parole, i gestori eventi generati da studio aumentano, anziché sostituire, i gestori eventi personalizzati.

## <a name="running-the-application"></a>Esecuzione dell'applicazione

Una volta create le schermate di avvio e un diagramma di flusso dello schermo, è possibile eseguire l'applicazione in Studio selezionando "Esegui applicazione".

![Screenshot del pulsante Esegui applicazione.](./media/guix-studio/image68.jpg)

pulsante sulla barra degli strumenti, selezionando modifica | Eseguire l'applicazione dal menu progetto oppure selezionando il pulsante Esegui nella parte inferiore della finestra di dialogo Modifica flusso schermo.

Quando si esegue l'applicazione, vengono visualizzate le schermate che è stato definito come "visibile all'avvio" in una nuova finestra. I widget figlio in queste schermate sono completamente operativi. È possibile fare clic sui pulsanti, utilizzare i dispositivi di scorrimento e la rotellina e così via. Se sono state definite funzioni di disegno personalizzate o la gestione degli eventi del cliente per uno di questi widget, questo non sarà ovviamente visibile quando si esegue l'applicazione in questa modalità. Tuttavia, se è stato definito un diagramma di flusso dello schermo con eventi di trigger e azioni, questi trigger saranno operativi e le schermate verranno trasformate come definito, incluse le animazioni che potrebbero essere state definite.
