---
title: Definizione dell'Flow
description: GUIX Studio supporta la generazione automatica e l'esecuzione della logica di transizione dello schermo.
author: philmea
ms.author: philmea
ms.date: 5/19/2020
ms.service: rtos
ms.topic: article
ms.openlocfilehash: 1df90acd86b4446d96a66ab3ee21545afcd9824e28efb40204c2966cb075c501
ms.sourcegitcommit: 93d716cf7e3d735b18246d659ec9ec7f82c336de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2021
ms.locfileid: "116785570"
---
# <a name="chapter-7-defining-screen-flow"></a>Capitolo 7: Definizione dell'Flow

GUIX Studio supporta la generazione automatica e l'esecuzione della logica di transizione dello schermo. L'utente definisce la logica di transizione dello schermo creando e modificando un diagramma di flusso dello schermo grafico. Quando un diagramma di flusso dello schermo viene aggiunto al progetto, abilita due funzionalità importanti: 1) L'applicazione può essere eseguita dall'ambiente di Studio e 2) Studio genera automaticamente gestori eventi e logica di transizione dello schermo per implementare il flusso dello schermo designato all'interno del file specifications.c generato, rimuovendo questo carico di lavoro dal programma dell'applicazione. 

L'esecuzione dell'applicazione sul desktop dall'ambiente di Studio è una funzionalità utile che consente di risparmiare tempo perché non è necessario eseguire un ciclo di compilazione/collegamento per eseguire l'applicazione. Esistono ovviamente limitazioni a ciò che è possibile eseguire senza compilare l'applicazione. Le funzioni di disegno personalizzate, i gestori eventi personalizzati e la gestione complessa degli eventi non sono disponibili quando si esegue l'applicazione dall'ambiente GUIX Studio. Questa funzionalità consente comunque di generare automaticamente la logica di transizione dello schermo e di programmare le animazioni da eseguire per la transizione da una schermata a un'altra. Questi effetti e animazioni possono essere osservati direttamente dall'ambiente GUIX Studio.

Si noti che quando si definiscono il flusso dello schermo, i trigger e le azioni che verranno descritte nei paragrafi seguenti, non solo si abilita l'esecuzione dell'interfaccia utente dall'ambiente di Studio, ma si abilita anche GUIX Studio per generare logica all'interno del file delle specifiche che gestirà gli eventi ed esegue azioni in base a tali eventi,  ad esempio la transizione da una schermata a un'altra.

## <a name="configuring-screen-flow"></a>Configurazione dell'Flow

Prima di poter eseguire un'applicazione dall'ambiente di Studio, è necessario definire alcuni elementi. In primo luogo, la schermata o le schermate di primo livello che devono essere visualizzate all'avvio del programma devono essere indicate selezionando la proprietà "Visibile all'avvio" nella visualizzazione delle proprietà di Studio. Questo flag indica che questa schermata deve essere visualizzata inizialmente all'avvio del programma. Se lo si desidera, più di una schermata può avere questa designazione.

Dopo aver definito le schermate visibili all'avvio, l'utente può definire il flusso dell'applicazione dell'interfaccia utente da uno schermo all'altro. GUIX Studio fornisce un diagramma di flusso dello schermo grafico per definire la logica di transizione dello schermo. È sufficiente selezionare la selezione di menu ***Configura, Schermata Flow** _ per visualizzare la finestra di dialogo di modifica del flusso dello schermo, vedere lo screenshot in _*_Figura 30_**.

![Screenshot della finestra di dialogo Flow GUIX Studio.](./media/guix-studio/config_screen_flow.png)

**Figura 30**

Ogni schermata di primo livello definita nel progetto verrà visualizzata come una casella che mostra il nome della schermata. Questa casella è un segnaposto che rappresenta ogni schermata di primo livello definita nel progetto. Queste caselle possono essere spostate e ridimensionate in base alle esigenze. Quando è stata definita una transizione da una schermata di primo livello a un'altra, verrà visualizzata una linea di connessione con una punta di freccia tra due schermate per indicare le transizioni da una schermata a un'altra.

La visualizzazione albero sul lato sinistro del diagramma del flusso dello schermo mostra ogni schermata di primo livello ed è possibile selezionare le schermate di primo livello da disegnare nel diagramma di flusso dello schermo.

Il diagramma di flusso dello schermo è scorrevole. È possibile trascinare qualsiasi blocco di schermata verso il basso e all'esterno dell'area visibile per ingrandire la finestra scorrevole. Dopo aver ingrandito la finestra scorrevole, è possibile ingrandire la finestra per adattarla all'area visibile scorrendo la rotellina del mouse verso il basso. Se la finestra scorrevole è ingrandita, è possibile renderla sufficientemente grande da contenere tutti i blocchi scorrendo la rotellina del mouse verso l'alto.

Per definire le transizioni per una schermata, fare clic con il pulsante destro del mouse sul segnaposto per tale schermata per visualizzare una finestra di dialogo Modifica elenco trigger, vedere ***la figura 31.***

![Screenshot della finestra di dialogo MODIFICA elenco trigger di GUIX Studio.](./media/guix-studio/edit_trigger_list.png)

**Figura 31**

Nella finestra di dialogo di modifica trigger sono elencati gli eventi definiti dall'utente che attiveranno una transizione dello schermo, motivo per cui questi eventi vengono definiti trigger. I trigger sono in genere segnali generati da uno o più widget figlio della schermata selezionata.

Per definire un nuovo trigger, selezionare il pulsante * Aggiungi nuovo **trigger** _ nella finestra di dialogo Modifica elenco trigger per visualizzare la finestra di dialogo Aggiungi trigger illustrata nella figura _32_**.

![Screenshot della finestra di dialogo Aggiungi trigger di GUIX Studio.](./media/guix-studio/add_trigger_for.png)

**Figura 32**

È possibile definire il tipo di evento che attiverà un nuovo set di azioni e definire le azioni che verranno eseguite quando l'evento trigger viene ricevuto.

Dopo aver definito il tipo di evento che si vuole usare per attivare una nuova transizione della schermata di animazione, salvare questo nuovo trigger che verrà visualizzato nella finestra di dialogo Modifica elenco trigger.

È possibile modificare questo evento (senza modificare le azioni correlate da eseguire) selezionando l'evento nella finestra di dialogo Modifica elenco trigger e selezionando il ***pulsante Modifica evento trigger.***

Analogamente, è possibile rimuovere qualsiasi evento trigger dall'elenco selezionando l'evento e facendo clic sul ***pulsante Elimina trigger*** selezionato.

Per specificare l'animazione o la transizione dello schermo che deve verificarsi in base a un evento trigger specifico, selezionare l'evento trigger e fare clic sul pulsante Modifica ***azioni.*** Si noti che è possibile attivare più di un'azione in base a ogni trigger definito.

Il **pulsante Modifica azioni** apre la finestra di dialogo Modifica azioni per trigger, illustrata nella figura 33: 

![Screenshot della finestra di dialogo GUIX Studio Edit Actions for Trigger (Azioni di modifica per trigger) di GUIX Studio.](./media/guix-studio/edit_actions_for_trigger.png)

**Figura 33**

Questa finestra di dialogo consente di definire un numero qualsiasi di azioni da implementare in base a questo evento trigger. È possibile assegnare a ogni azione un nome significativo per associare ogni definizione di azione a un'animazione o una transizione visiva. Nell'esempio precedente sono stati definiti due azioni denominate "fade_in_text_screen" e "fade_out_button_screen".

Definire una nuova azione da implementare, fare clic sul pulsante Aggiungi nuova azione, che visualizza la finestra di dialogo Seleziona azione, figura 34:

![Screenshot della finestra di dialogo GuiX Studio Select Action (Azione di selezione di GUIX Studio).](./media/guix-studio/select_action.png)

**Figura 34**

I tipi di azione disponibili includono:

- **Animazione:** avvia un'animazione con le informazioni specificate.
- **Allega:** collega la schermata di destinazione alla schermata padre. Se la schermata padre non è specificata, la schermata di destinazione verrà collegata alla finestra radice.
- **Scollega:** scollegare la schermata di destinazione dal relativo elemento padre.
- **Nascondi:** nasconde la schermata di destinazione.
- **Pop dello stack di** schermate: consente di visualizzare una schermata dallo stack dello schermo interno.
- **Push dello stack dello schermo:** eseguire il push di un puntatore dello schermo nello stack dello schermo interno.
- **Reimpostazione dello stack dello** schermo: rimuovere tutti i puntatori dello schermo dallo stack dello schermo interno.
- **Mostra**: mostra la schermata di destinazione.
- **Attiva/Disattiva:** collega la schermata di destinazione al padre della schermata corrente e scollega la schermata corrente dal relativo elemento padre.
- **Window Execute**:Modally esegue la schermata di destinazione.
- **Arresto dell'esecuzione della** finestra: consente di uscire dall'esecuzione modale della schermata corrente.

Dopo aver definito un'azione da eseguire in base all'evento trigger selezionato, tale azione verrà visualizzata nella finestra di dialogo Modifica azioni per trigger. È possibile selezionare questa azione per modificare i parametri di tale azione, come illustrato nella figura 35.

![Screenshot della finestra di dialogo GUIX Studio Edit Actions for Trigger (Azioni di modifica per trigger) di GUIX Studio.](./media/guix-studio/edit_actions_for_trigger.png)

**Figura 35**

Se il tipo di azione è un'animazione, a destra viene visualizzato un set di parametri di animazione che consentono di definire un'animazione di tipo diapositiva e/o dissolvenza da eseguire. Quando un'azione di animazione viene completata, è anche possibile determinare se l'animazione deve essere scollegata automaticamente dal padre e/o inserita nello stack dello schermo interno, che è spesso utile quando si definiscono sistemi di menu a più livelli.

Per le animazioni con scorrimento e dissolvenza, è anche possibile definire la funzione di andamento da usare selezionando il pulsante Easing Func Select . Le funzioni di easing sono varie curve progettate per simulare più da vicino gli eventi di movimento della vita reale. Selezionando questo pulsante viene visualizzata la finestra di dialogo Seleziona funzione **di easing,** figura 36:

![Screenshot della finestra di dialogo GUIX Studio Select Easing Function (Selezione funzione di easing) di GUIX Studio.](./media/guix-studio/easing_function_select.png)

**Figura 36**

Se si definiscono più azioni da associare a un evento trigger, può essere utile assegnare a ogni azione un nome significativo. I nomi delle azioni devono seguire le regole di denominazione della sintassi C, in quanto questi nomi verranno usati all'interno del file di specifiche generato per definire tabelle di eventi e azioni.

Quando si definiscono eventi di trigger e azioni all'interno di GUIX Studio, i gestori eventi automatizzati vengono generati all'interno del file delle specifiche del progetto per gestire questi eventi ed eseguire le azioni specificate. Ciò significa che NON è necessario gestire questi eventi nel codice dell'applicazione, anche se gli eventi trigger vengono comunque passati a tutti i gestori eventi personalizzati definiti. In altre parole, i gestori eventi generati da Studio aumentano, anziché sostituire, i gestori eventi personalizzati.

## <a name="running-the-application"></a>Esecuzione dell'applicazione

Dopo aver creato le schermate di avvio e un diagramma di flusso dello schermo, è possibile eseguire l'applicazione all'interno di Studio selezionando "Esegui applicazione"

![Screenshot del pulsante Esegui applicazione.](./media/guix-studio/image68.jpg)

sulla barra degli strumenti, selezionando Modifica | Eseguire l'applicazione dal menu del progetto o selezionando il pulsante Esegui nella parte inferiore della finestra di dialogo Modifica Flow schermata.

Quando si esegue l'applicazione, verranno visualizzate le schermate designate come "Visibili all'avvio" all'interno di una nuova finestra. I widget figlio in questa schermata sono completamente operativi. È possibile fare clic sui pulsanti, usare i dispositivi di scorrimento e le rotelle di scorrimento e così via. Se sono state definite funzioni di disegno personalizzate o la gestione degli eventi del cliente per uno di questi widget, ovviamente NON verrà visualizzato quando si esegue l'applicazione in questa modalità. Tuttavia, se è stato definito un diagramma di flusso dello schermo con eventi e azioni di trigger, questi trigger saranno operativi e le schermate verranno eseguite nel modo definito, incluse eventuali animazioni definite.
