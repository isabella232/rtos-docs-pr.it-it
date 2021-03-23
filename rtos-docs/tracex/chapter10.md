---
title: Capitolo 10-eventi utente del cliente
description: Questo capitolo contiene una descrizione di come creare eventi definiti dall'utente e campi di informazioni e icone personalizzati per tali eventi.
author: philmea
ms.service: rtos
ms.topic: article
ms.date: 5/19/2020
ms.author: philmea
ms.openlocfilehash: 635c2d79922de9d5649bab841ae946cac862056c
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823510"
---
# <a name="chapter-10---customer-user-events"></a><span data-ttu-id="eb7e7-103">Capitolo 10-eventi utente del cliente</span><span class="sxs-lookup"><span data-stu-id="eb7e7-103">Chapter 10 - Customer user events</span></span>

<span data-ttu-id="eb7e7-104">Questo capitolo contiene una descrizione di come creare eventi definiti dall'utente e campi di informazioni e icone personalizzati per tali eventi.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-104">This chapter contains a description of how to create user-defined events and custom icons and information fields for such events.</span></span> <span data-ttu-id="eb7e7-105">In questo capitolo sono incluse le seguenti sezioni:</span><span class="sxs-lookup"><span data-stu-id="eb7e7-105">This chapter includes the following sections:</span></span> 

## <a name="inserting-user-defined-events"></a><span data-ttu-id="eb7e7-106">Inserimento di eventi User-Defined</span><span class="sxs-lookup"><span data-stu-id="eb7e7-106">Inserting User-Defined Events</span></span>

<span data-ttu-id="eb7e7-107">ThreadX offre agli sviluppatori la possibilità di registrare gli eventi definiti dall'utente, fornendo informazioni ancora più utili che possono essere visualizzate graficamente da TraceX.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-107">ThreadX provides the ability for developers to log their own user-defined events, providing even more useful information that can be viewed graphically by TraceX.</span></span> <span data-ttu-id="eb7e7-108">I numeri di evento definiti dall'utente sono compresi tra</span><span class="sxs-lookup"><span data-stu-id="eb7e7-108">User-defined event numbers range from</span></span>

<span data-ttu-id="eb7e7-109">**TX_TRACE_USER_EVENT_START** (4096) tramite **TX_TRACE_USER_EVENT_END** (65535), inclusi.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-109">**TX_TRACE_USER_EVENT_START** (4096) through **TX_TRACE_USER_EVENT_END** (65535), inclusive.</span></span> <span data-ttu-id="eb7e7-110">La posizione degli eventi nel buffer di traccia viene eseguita tramite la ***tx_trace_user_event_insert***, definita nel capitolo 5.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-110">The placement of the events in the trace buffer is done via the ***tx_trace_user_event_insert***, defined in Chapter 5.</span></span> <span data-ttu-id="eb7e7-111">Nell'esempio seguente viene eseguita una chiamata per inserire due eventi definiti dall'utente nel buffer di traccia corrente nella destinazione, ovvero l'evento definito dall'utente 4096 e l'evento 4098:</span><span class="sxs-lookup"><span data-stu-id="eb7e7-111">The following example calls insert two user-defined events into the current trace buffer on the target, namely user-defined event 4096 and event 4098:</span></span>

```c
tx_trace_user_event_insert(4096, 1, 2, 3, 4);
tx_trace_user_event_insert(4098,0x100,0x200,0x300,0x400);
```

## <a name="default-display-of-user-defined-events"></a><span data-ttu-id="eb7e7-112">Visualizzazione predefinita degli eventi di User-Defined</span><span class="sxs-lookup"><span data-stu-id="eb7e7-112">Default Display of User-Defined Events</span></span>

![Icona evento definito dall'utente](./media/user-guide/tx-events/image0.png)

<span data-ttu-id="eb7e7-114">Per impostazione predefinita, TraceX Visualizza tutti gli eventi utente con l'icona di un evento predefinito definito dall'utente, come descritto nel capitolo 6.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-114">By default, TraceX displays all user events with a default user-defined Event icon as described in Chapter 6.</span></span> <span data-ttu-id="eb7e7-115">La figura 28 Mostra l'icona dell'evento predefinito definito dall'utente per gli eventi 452 e 453, che sono stati inseriti nel buffer degli eventi tramite gli esempi di ***tx_trace_user_event_insert*** precedenti.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-115">Figure 28 shows the default user-defined event icon for events 452 and 453, which were placed in the event buffer via the previous ***tx_trace_user_event_insert*** examples.</span></span>

<span data-ttu-id="eb7e7-116">![Screenshot della visualizzazione predefinita degli eventi definiti dall'utente. ](./media/user-guide/10.1.png)
 **Figura 28**</span><span class="sxs-lookup"><span data-stu-id="eb7e7-116">![Screenshot of the default display of user-defined events.](./media/user-guide/10.1.png)
**FIGURE 28**</span></span>

<span data-ttu-id="eb7e7-117">Sono inoltre disponibili informazioni dettagliate per gli eventi definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-117">Detailed information is also available for user-defined Events.</span></span> <span data-ttu-id="eb7e7-118">La figura 28 Mostra le informazioni dettagliate sugli eventi per l'evento 452, che presenta il numero di evento 4096 e Mostra i quattro campi di informazioni specificati.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-118">Figure 28 shows the detailed event information for event 452, which has event number 4096 and shows the specified four information fields.</span></span>

<span data-ttu-id="eb7e7-119">![Screenshot della visualizzazione dettagliata degli eventi definiti dall'utente. ](./media/user-guide/10.2.png)
 **Figura 29**</span><span class="sxs-lookup"><span data-stu-id="eb7e7-119">![Screenshot of the detailed display of user-defined events.](./media/user-guide/10.2.png)
**FIGURE 29**</span></span>

## <a name="defining-custom-user-defined-event-icons"></a><span data-ttu-id="eb7e7-120">Definizione di icone evento User-Defined personalizzate</span><span class="sxs-lookup"><span data-stu-id="eb7e7-120">Defining Custom User-Defined Event Icons</span></span>

<span data-ttu-id="eb7e7-121">TraceX offre inoltre agli utenti la possibilità di creare icone personalizzate dell'evento definite dall'utente e etichette dei campi di informazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-121">TraceX also provides the user the ability to create custom user-defined event icons and custom information field labels.</span></span> <span data-ttu-id="eb7e7-122">Questa funzionalità viene eseguita aggiungendo le specifiche dell'icona dell'evento al file di configurazione \***tracex_custom. trxc** _.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-122">This capability is achieved by adding event icon specifications to the \***tracex_custom.trxc** _ configuration file.</span></span> <span data-ttu-id="eb7e7-123">Questo file si trova nella sottodirectory _ *_CustomEvents_*\* della directory di installazione TraceX definita dall'utente, che per impostazione predefinita è C:\ Azure_RTOS \tracex.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-123">This file is located in the _ *_CustomEvents_*\* subdirectory of your user-defined TraceX installation directory, which defaults to c:\Azure_RTOS\TraceX.</span></span> <span data-ttu-id="eb7e7-124">Un percorso di directory di esempio è illustrato nella figura 30.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-124">An example directory path is shown in Figure 30.</span></span>

<span data-ttu-id="eb7e7-125">![Screenshot di un percorso di directory di esempio. ](./media/user-guide/custom_events_folder.png)
 **Figura 30**</span><span class="sxs-lookup"><span data-stu-id="eb7e7-125">![Screenshot of an example directory path.](./media/user-guide/custom_events_folder.png)
**FIGURE 30**</span></span>

<span data-ttu-id="eb7e7-126">Il file di configurazione dell'evento personalizzato ***tracex_custom. trxc*** è un semplice file di testo ASCII che contiene zero o più definizioni di evento personalizzate.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-126">The ***tracex_custom.trxc*** custom event configuration file is a simple ASCII text file containing zero or more custom event definitions.</span></span> <span data-ttu-id="eb7e7-127">Di seguito è riportato il formato del file.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-127">The format of the file is as follows:</span></span>

```c
//Comments
**Start **
[custom event definition(s)] **End **
```

<span data-ttu-id="eb7e7-128">Ogni riga tra inizio e fine viene utilizzata per definire un singolo evento personalizzato.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-128">Each line between Start and End is used to define a single custom event.</span></span> <span data-ttu-id="eb7e7-129">TraceX fornisce una versione modello di questo file senza eventi personalizzati definiti (niente tra le etichette "Start" e "end").</span><span class="sxs-lookup"><span data-stu-id="eb7e7-129">TraceX provides a template version of this file with no custom events defined (nothing between the "Start" and "End" labels).</span></span> <span data-ttu-id="eb7e7-130">Il formato di una definizione di evento personalizzata è il seguente:</span><span class="sxs-lookup"><span data-stu-id="eb7e7-130">The format of a custom event definition is as follows:</span></span>

<span data-ttu-id="eb7e7-131">**numero, nome, abbreviazione, top_color, bottom_color, Label1, Label2, Label2, label4**</span><span class="sxs-lookup"><span data-stu-id="eb7e7-131">**number, name, abbreviation, top_color, bottom_color, label1, label2, label2, label4**</span></span>

<span data-ttu-id="eb7e7-132">dove:</span><span class="sxs-lookup"><span data-stu-id="eb7e7-132">where:</span></span>

- <span data-ttu-id="eb7e7-133">Number: definisce il numero di evento definito dall'utente, compreso tra 4096 e 65535, inclusi.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-133">number: Defines the user-defined event number, between 4096 and 65535, inclusive.</span></span></th>
- <span data-ttu-id="eb7e7-134">Nome: definisce il nome logico per l'evento definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-134">name: Defines the logical name for the user-defined event.</span></span></td>
- <span data-ttu-id="eb7e7-135">Abbreviazione: definisce l'abbreviazione di evento definito dall'utente di due lettere.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-135">abbreviation: Defines the two-letter user-defined event abbreviation.</span></span></td>
- <span data-ttu-id="eb7e7-136">top_color: definisce il valore RGB per la metà superiore dell'icona, ovvero un numero di tre cifre tra parentesi.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-136">top_color: Defines the RGB value for the top-half of the icon, which is a three-digit number in parenthesis.</span></span> <span data-ttu-id="eb7e7-137">Alcune definizioni RGB tipiche sono</span><span class="sxs-lookup"><span data-stu-id="eb7e7-137">Some typical RGB definitions are</span></span>
  - <span data-ttu-id="eb7e7-138">NERO = (0, 0, 0)</span><span class="sxs-lookup"><span data-stu-id="eb7e7-138">BLACK = (0,0,0)</span></span>       
  - <span data-ttu-id="eb7e7-139">BIANCO = (255.255.255)</span><span class="sxs-lookup"><span data-stu-id="eb7e7-139">WHITE = (255,255,255)</span></span>
  - <span data-ttu-id="eb7e7-140">ROSSO = (255, 0, 0)</span><span class="sxs-lookup"><span data-stu-id="eb7e7-140">RED = (255,0,0)</span></span>     
  - <span data-ttu-id="eb7e7-141">VERDE = (0255, 0)</span><span class="sxs-lookup"><span data-stu-id="eb7e7-141">GREEN = (0,255,0)</span></span>     
  - <span data-ttu-id="eb7e7-142">BLU = (0255)</span><span class="sxs-lookup"><span data-stu-id="eb7e7-142">BLUE = (0,0,255)</span></span>     
  - <span data-ttu-id="eb7e7-143">GIALLO = (255255, 0)</span><span class="sxs-lookup"><span data-stu-id="eb7e7-143">YELLOW = (255,255,0)</span></span>   
  - <span data-ttu-id="eb7e7-144">CYAN = (0255.255)</span><span class="sxs-lookup"><span data-stu-id="eb7e7-144">CYAN = (0,255,255)</span></span>   
  - <span data-ttu-id="eb7e7-145">MAGENTA = (255, 0255)</span><span class="sxs-lookup"><span data-stu-id="eb7e7-145">MAGENTA = (255,0,255)</span></span>   
  <span data-ttu-id="eb7e7-146">L'uso della specifica RBG offre all'utente un'ampia gamma di colori per ogni icona definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-146">Using the RBG specification gives the user a broad range of colors for each user-defined icon.</span></span> <span data-ttu-id="eb7e7-147">Per ulteriori informazioni sulla definizione di colore RBG, vedere: https://en.wikipedia.org/wiki/RGB#Digital_representations</span><span class="sxs-lookup"><span data-stu-id="eb7e7-147">For more information on RBG color definition, see: https://en.wikipedia.org/wiki/RGB#Digital_representations</span></span>
- <span data-ttu-id="eb7e7-148">botton_color: definisce il valore RGB per la metà inferiore dell'icona, ovvero un numero di tre cifre tra parentesi.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-148">botton_color: Defines the RGB value for the bottom half of the icon, which is a three-digit number in parenthesis.</span></span>
- <span data-ttu-id="eb7e7-149">Label1: etichetta per \***info_field_1** _, come specificato nella chiamata _ \*_tx_trace_user_event_insert_\*\*.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-149">label1: Label for ***info_field_1** _, as specified in the _ *_tx_trace_user_event_insert_** call.</span></span>
- <span data-ttu-id="eb7e7-150">Label2: etichetta per \***info_field_2** _, come specificato nella chiamata _ \*_tx_trace_user_event_insert_\*\*.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-150">label2: Label for ***info_field_2** _, as specified in the _ *_tx_trace_user_event_insert_** call.</span></span>
- <span data-ttu-id="eb7e7-151">Label3: etichetta per \***info_field_3** _, come specificato nella chiamata _ \*_tx_trace_user_event_insert_\*\*.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-151">label3: Label for ***info_field_3** _, as specified in the _ *_tx_trace_user_event_insert_** call.</span></span>
- <span data-ttu-id="eb7e7-152">Label4: etichetta per \***info_field_4** _, come specificato nella chiamata _ \*_tx_trace_user_event_insert_\*\*.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-152">label4: Label for ***info_field_4** _, as specified in the _ *_tx_trace_user_event_insert_** call.</span></span>

<span data-ttu-id="eb7e7-153">Le definizioni di esempio per ognuno dei due eventi definiti dall'utente usati in questo capitolo sono illustrate nella figura 10,4.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-153">Example definitions for each of the two user-defined events used in this chapter are shown in Figure 10.4.</span></span> <span data-ttu-id="eb7e7-154">La prima definizione è relativa all'evento 4096 alla riga 5 del file \***tracex_custom. trxc** _.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-154">The first definition is for event 4096 at line 5 of the \***tracex_custom.trxc** _ file.</span></span> <span data-ttu-id="eb7e7-155">Questa definizione fornisce un evento definito dall'utente 4096 il nome _ \* First_User_Event \* \*, specifica un'abbreviazione di due lettere di **Fe**, rende la parte superiore dell'icona rossa, la parte inferiore dell'icona verde e denomina i campi informativi come **First_Info1**, **First_Info2**, **First_Info3** e **First_Info4**.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-155">This definition gives user-defined event 4096 the name _\*First_User_Event\*\*, specifies a two-letter abbreviation of **FE**, makes the top portion of the icon red, the bottom portion of the icon green, and names the information fields as **First_Info1**, **First_Info2**, **First_Info3**, and **First_Info4**.</span></span> <span data-ttu-id="eb7e7-156">L'evento 4098 definito dall'utente è definito in modo analogo alla riga 6 di **_tracex_custom. trxc_**.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-156">User-defined event 4098 is defined similarly at line 6 of **_tracex_custom.trxc_**.</span></span>

<span data-ttu-id="eb7e7-157">![Screenshot delle definizioni di esempio per gli eventi definiti dall'utente. ](./media/user-guide/10.4.png)
 **Figura 31**</span><span class="sxs-lookup"><span data-stu-id="eb7e7-157">![Screenshot of the example definitions for the user-defined events.](./media/user-guide/10.4.png)
**FIGURE 31**</span></span>

<span data-ttu-id="eb7e7-158">Poiché il file \***tracex_custom. trxc** _ viene letto da TRACEx durante l'inizializzazione, è necessario chiudere e riavviare TRACEx per rendere effettive le definizioni delle icone personalizzate.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-158">Since the \***tracex_custom.trxc** _ file is read by TraceX during initialization, TraceX must be exited and restarted before the custom icon definitions can take effect.</span></span> <span data-ttu-id="eb7e7-159">La figura 32 Mostra la visualizzazione TraceX degli eventi definiti dall'utente 452 e 453 con le icone di evento personalizzate definite in _ *_tracex_custom. trxc_* \*.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-159">Figure 32 shows the TraceX display of user-defined events 452 and 453 with the custom event icons defined in _\*_tracex_custom.trxc_\*\*.</span></span>

<span data-ttu-id="eb7e7-160">![Screenshot della visualizzazione TraceX degli eventi definiti dall'utente con le icone dell'evento personalizzato. ](./media/user-guide/10.5.png)
 **Figura 32**</span><span class="sxs-lookup"><span data-stu-id="eb7e7-160">![Screenshot of the TraceX display of user defined events with the custom event icons.](./media/user-guide/10.5.png)
**FIGURE 32**</span></span>

<span data-ttu-id="eb7e7-161">Le informazioni aggiuntive nella definizione di evento personalizzato vengono visualizzate quando si seleziona l'evento usando un doppio clic, un passaggio del mouse o facendo clic sul pulsante evento corrente.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-161">The additional information in the custom event definition is shown when the event you select using a double-click, mouse-over, or clicking the current event button.</span></span> <span data-ttu-id="eb7e7-162">La figura 33 Mostra la selezione di doppio clic nell'evento 452.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-162">Figure 33 shows the double-click selection on event 452.</span></span> <span data-ttu-id="eb7e7-163">Il nome dell'evento e i campi delle informazioni corrispondono alla definizione di esempio aggiunta a ***tracex_custom. trxc***.</span><span class="sxs-lookup"><span data-stu-id="eb7e7-163">The event name and information fields all match the sample definition that was added to ***tracex_custom.trxc***.</span></span>

<span data-ttu-id="eb7e7-164">![Screenshot della selezione del doppio clic per un evento. ](./media/user-guide/10.6.png)
 **Figura 33**</span><span class="sxs-lookup"><span data-stu-id="eb7e7-164">![Screenshot of the double-click selection on an event.](./media/user-guide/10.6.png)
**FIGURE 33**</span></span>
