---
title: Appendice C-stili del widget GUIX
description: Informazioni sugli stili dei widget GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 83d5c5167739e91b7af8fce6b04213f610984fc6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823183"
---
# <a name="appendix-c---guix-widget-styles"></a><span data-ttu-id="a6883-103">Appendice C-stili del widget GUIX</span><span class="sxs-lookup"><span data-stu-id="a6883-103">Appendix C - GUIX Widget Styles</span></span>

<span data-ttu-id="a6883-104">__***Stili generali (usati con la maggior parte dei tipi di widget):***__</span><span class="sxs-lookup"><span data-stu-id="a6883-104">__***General Styles (Used with most widget types):***__</span></span>

<span data-ttu-id="a6883-105">**GX_STYLE_BORDER_NONE**</span><span class="sxs-lookup"><span data-stu-id="a6883-105">**GX_STYLE_BORDER_NONE**</span></span>
  - <span data-ttu-id="a6883-106">Valore: 0x00000000</span><span class="sxs-lookup"><span data-stu-id="a6883-106">Value: 0x00000000</span></span>
  - <span data-ttu-id="a6883-107">Descrizione: usare questo stile per creare un widget senza bordo.</span><span class="sxs-lookup"><span data-stu-id="a6883-107">Description: Use this style to draw a widget with no border.</span></span>

<span data-ttu-id="a6883-108">**GX_STYLE_BORDER_RAISED**</span><span class="sxs-lookup"><span data-stu-id="a6883-108">**GX_STYLE_BORDER_RAISED**</span></span>
  - <span data-ttu-id="a6883-109">Valore: 0x00000001</span><span class="sxs-lookup"><span data-stu-id="a6883-109">Value: 0x00000001</span></span>
  - <span data-ttu-id="a6883-110">Descrizione: creare un widget con un bordo in rilievo.</span><span class="sxs-lookup"><span data-stu-id="a6883-110">Description: Draw widget with a raised border.</span></span>

<span data-ttu-id="a6883-111">**GX_STYLE_BORDER_RECESSED**</span><span class="sxs-lookup"><span data-stu-id="a6883-111">**GX_STYLE_BORDER_RECESSED**</span></span>
  - <span data-ttu-id="a6883-112">Valore: 0x00000002</span><span class="sxs-lookup"><span data-stu-id="a6883-112">Value: 0x00000002</span></span>
  - <span data-ttu-id="a6883-113">Descrizione: creare un widget con un bordo incassato.</span><span class="sxs-lookup"><span data-stu-id="a6883-113">Description: Draw widget with a recessed border.</span></span>

<span data-ttu-id="a6883-114">**GX_STYLE_BORDER_THIN**</span><span class="sxs-lookup"><span data-stu-id="a6883-114">**GX_STYLE_BORDER_THIN**</span></span>
  - <span data-ttu-id="a6883-115">Valore: 0x00000004</span><span class="sxs-lookup"><span data-stu-id="a6883-115">Value: 0x00000004</span></span>
  - <span data-ttu-id="a6883-116">Descrizione: creare un bordo della larghezza di un pixel.</span><span class="sxs-lookup"><span data-stu-id="a6883-116">Description: Draw a one-pixel width border.</span></span>

<span data-ttu-id="a6883-117">**GX_STYLE_BORDER_THICK**</span><span class="sxs-lookup"><span data-stu-id="a6883-117">**GX_STYLE_BORDER_THICK**</span></span> 
  - <span data-ttu-id="a6883-118">Valore: 0x00000008</span><span class="sxs-lookup"><span data-stu-id="a6883-118">Value: 0x00000008</span></span>
  - <span data-ttu-id="a6883-119">Descrizione: creare un widget con un bordo spesso.</span><span class="sxs-lookup"><span data-stu-id="a6883-119">Description: Draw widget with a thick border.</span></span>

<span data-ttu-id="a6883-120">**GX_STYLE_BORDER_MASK**</span><span class="sxs-lookup"><span data-stu-id="a6883-120">**GX_STYLE_BORDER_MASK**</span></span>
  - <span data-ttu-id="a6883-121">Valore: 0x0000000F</span><span class="sxs-lookup"><span data-stu-id="a6883-121">Value: 0x0000000f</span></span>
  - <span data-ttu-id="a6883-122">Descrizione: valore della maschera usato per testare solo i campi di stile del membro dello stile del widget.</span><span class="sxs-lookup"><span data-stu-id="a6883-122">Description: Mask value used to test only the style fields of the widget style member.</span></span>

<span data-ttu-id="a6883-123">**GX_STYLE_TRANSPARENT**</span><span class="sxs-lookup"><span data-stu-id="a6883-123">**GX_STYLE_TRANSPARENT**</span></span>
  - <span data-ttu-id="a6883-124">Valore: 0x10000000</span><span class="sxs-lookup"><span data-stu-id="a6883-124">Value: 0x10000000</span></span>
  - <span data-ttu-id="a6883-125">Descrizione: creare un widget almeno parzialmente trasparente.</span><span class="sxs-lookup"><span data-stu-id="a6883-125">Description: Create a widget that is at least partially transparent.</span></span> <span data-ttu-id="a6883-126">Questo stile deve essere usato quando un widget non disegna se stesso completamente opaco, inclusi i widget che disegnano una Pixelmap semi-trasparente come sfondo del widget.</span><span class="sxs-lookup"><span data-stu-id="a6883-126">This style should be used when a widget does not draw itself fully opaque, including widgets that draw a semi-transparent pixelmap as the widget background.</span></span> <span data-ttu-id="a6883-127">Questo flag di stile informa GUIX che è necessario disegnare l'elemento padre del widget per aggiornare l'area di sfondo del widget.</span><span class="sxs-lookup"><span data-stu-id="a6883-127">This style flag informs GUIX that the widget parent must be drawn to refresh the widget background area.</span></span>

<span data-ttu-id="a6883-128">**GX_STYLE_DRAW_SELECTED**</span><span class="sxs-lookup"><span data-stu-id="a6883-128">**GX_STYLE_DRAW_SELECTED**</span></span>
  - <span data-ttu-id="a6883-129">Valore: 0x20000000</span><span class="sxs-lookup"><span data-stu-id="a6883-129">Value: 0x20000000</span></span>
  - <span data-ttu-id="a6883-130">Descrizione: specificare che il widget deve essere disegnato usando i colori e i tipi di carattere selezionati per lo stato.</span><span class="sxs-lookup"><span data-stu-id="a6883-130">Description: Specify that the widget should be drawn using selected state colors and fonts.</span></span> <span data-ttu-id="a6883-131">Tipi di widget diversi usano lo stile DRAW_SELECTED in modi diversi per indicare che il widget è attualmente selezionato.</span><span class="sxs-lookup"><span data-stu-id="a6883-131">Different widget types use the DRAW_SELECTED style in different ways to indicate the widget is currently selected.</span></span>

<span data-ttu-id="a6883-132">**GX_STYLE_ENABLED**</span><span class="sxs-lookup"><span data-stu-id="a6883-132">**GX_STYLE_ENABLED**</span></span>
  - <span data-ttu-id="a6883-133">Valore: 0x40000000</span><span class="sxs-lookup"><span data-stu-id="a6883-133">Value: 0x40000000</span></span>
  - <span data-ttu-id="a6883-134">Descrizione: contrassegnare il widget come abilitato, in modo che il widget accetti gli eventi di input dell'utente e generi i segnali di output.</span><span class="sxs-lookup"><span data-stu-id="a6883-134">Description: Mark the widget as enabled, which allows the widget to accept user input events and generate output signals.</span></span>
  
<span data-ttu-id="a6883-135">**GX_STYLE_DYNAMICALLY_ALLOCATED**</span><span class="sxs-lookup"><span data-stu-id="a6883-135">**GX_STYLE_DYNAMICALLY_ALLOCATED**</span></span>
  - <span data-ttu-id="a6883-136">Valore: 0x80000000</span><span class="sxs-lookup"><span data-stu-id="a6883-136">Value: 0x80000000</span></span>
  - <span data-ttu-id="a6883-137">Descrizione: indica che la memoria del blocco di controllo widget viene allocata in modo dinamico usando il servizio gx_system_memory_allocator quando viene creato il widget e la memoria del blocco di controllo viene liberata se il widget viene eliminato definitivamente.</span><span class="sxs-lookup"><span data-stu-id="a6883-137">Description: Indicates the widget control block memory is dynamically allocated using the gx_system_memory_allocator service when the widget is created, and the control block memory is freed if the widget is destroyed.</span></span>

<span data-ttu-id="a6883-138">**GX_STYLE_USE_LOCAL_ALPHA**</span><span class="sxs-lookup"><span data-stu-id="a6883-138">**GX_STYLE_USE_LOCAL_ALPHA**</span></span>
  - <span data-ttu-id="a6883-139">Valore: 0x01000000</span><span class="sxs-lookup"><span data-stu-id="a6883-139">Value: 0x01000000</span></span>
  - <span data-ttu-id="a6883-140">Descrizione: indica alle funzioni di disegno GUIX di usare il valore alfa del widget locale durante il disegno del widget.</span><span class="sxs-lookup"><span data-stu-id="a6883-140">Description: Instructs GUIX drawing functions to use the local widget alpha value when drawing the widget.</span></span> <span data-ttu-id="a6883-141">Questo flag viene in genere usato dalla logica GUIX interna per implementare animazioni di dissolvenza dei widget.</span><span class="sxs-lookup"><span data-stu-id="a6883-141">This flag is normally used by the internal GUIX logic to implement widget fading animations.</span></span>


<span data-ttu-id="a6883-142">__***Stili di allineamento del testo (stili applicati a tutti i widget che consentono di disegnare testo):***__</span><span class="sxs-lookup"><span data-stu-id="a6883-142">__***Text Alignment Styles (styles applied to all widgets that draw text):***__</span></span>

<span data-ttu-id="a6883-143">**GX_STYLE_TEXT_LEFT**</span><span class="sxs-lookup"><span data-stu-id="a6883-143">**GX_STYLE_TEXT_LEFT**</span></span>
  - <span data-ttu-id="a6883-144">Valore: 0x00001000</span><span class="sxs-lookup"><span data-stu-id="a6883-144">Value: 0x00001000</span></span>
  - <span data-ttu-id="a6883-145">Descrizione: il testo viene disegnato allineato a sinistra all'interno dell'area client del widget.</span><span class="sxs-lookup"><span data-stu-id="a6883-145">Description: Text is drawn left-aligned within the widget client area.</span></span>

<span data-ttu-id="a6883-146">**GX_STYLE_TEXT_RIGHT**</span><span class="sxs-lookup"><span data-stu-id="a6883-146">**GX_STYLE_TEXT_RIGHT**</span></span> 
  - <span data-ttu-id="a6883-147">Valore: 0x00002000</span><span class="sxs-lookup"><span data-stu-id="a6883-147">Value: 0x00002000</span></span>
  - <span data-ttu-id="a6883-148">Descrizione: il testo viene tracciato allineato a destra nell'area client del widget.</span><span class="sxs-lookup"><span data-stu-id="a6883-148">Description: Text is drawn right-aligned within the widget client area.</span></span>

<span data-ttu-id="a6883-149">**GX_STYLE_TEXT_CENTER**</span><span class="sxs-lookup"><span data-stu-id="a6883-149">**GX_STYLE_TEXT_CENTER**</span></span>
  - <span data-ttu-id="a6883-150">Valore: 0x00004000</span><span class="sxs-lookup"><span data-stu-id="a6883-150">Value: 0x00004000</span></span>
  - <span data-ttu-id="a6883-151">Descrizione: il testo viene disegnato allineato al centro all'interno dell'area client del widget.</span><span class="sxs-lookup"><span data-stu-id="a6883-151">Description: Text is drawn center-aligned within the widget client area.</span></span>

<span data-ttu-id="a6883-152">**GX_STYLE_TEXT_COPY**</span><span class="sxs-lookup"><span data-stu-id="a6883-152">**GX_STYLE_TEXT_COPY**</span></span>
  - <span data-ttu-id="a6883-153">Valore: 0x00008000</span><span class="sxs-lookup"><span data-stu-id="a6883-153">Value: 0x00008000</span></span>
  - <span data-ttu-id="a6883-154">Descrizione: per impostazione predefinita, i widget che tracciano testo mantengono solo un puntatore al testo passato dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6883-154">Description: By default, widgets that draw text keep only a pointer to the text which is passed in by the application.</span></span> <span data-ttu-id="a6883-155">Per il testo definito in modo statico definito all'interno della tabella di stringhe, non c'è motivo per il widget di creare una copia privata del testo assegnato.</span><span class="sxs-lookup"><span data-stu-id="a6883-155">For statically defined text that is defined within the string table, there is no reason for the widget to make a private copy of the text assigned.</span></span> <span data-ttu-id="a6883-156">Tuttavia, se il testo assegnato a un widget viene creato dinamicamente usando funzioni come Sprint () o gx_utility_ltoa, è spesso utile indicare al widget di mantenerne la copia privata di qualsiasi testo assegnato.</span><span class="sxs-lookup"><span data-stu-id="a6883-156">However, if the text assigned to a widget is created dynamically using functions like sprint() or gx_utility_ltoa, then it is often convenient to tell the widget to keep it’s own private copy of any text assigned.</span></span> <span data-ttu-id="a6883-157">Questo consente all'applicazione di usare variabili automatiche o temporanee quando si definisce la stringa di testo, quando l'applicazione sarebbe altrimenti necessaria per definire matrici di caratteri definite in modo statico per ogni widget di testo che usa testo definito in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="a6883-157">This allows the application to use automatic or temporary variables when defining the text string, when the application would otherwise be required to define statically defined character arrays for each text widget that is using dynamically defined text.</span></span> <span data-ttu-id="a6883-158">Quando viene impostato questo flag di stile, il widget utilizzerà la funzione gx_system_memory_allocator per allocare in modo dinamico il blocco di memoria necessario per conservare una copia privata della stringa assegnata.</span><span class="sxs-lookup"><span data-stu-id="a6883-158">When this style flag is set, the widget will use the gx_system_memory_allocator function to dynamically allocate the memory block needed to hold a private copy of the assigned string.</span></span> <span data-ttu-id="a6883-159">Pertanto, l'utilizzo di questo flag di stile è predicato nell'applicazione che definisce le funzioni memory_allocator e memory_deallocator.</span><span class="sxs-lookup"><span data-stu-id="a6883-159">Therefore using this style flag is predicated on the application defining memory_allocator and memory_deallocator functions.</span></span> <span data-ttu-id="a6883-160">GX_STYLE_TEXT_COPY non devono essere cancellate dopo che è stata impostata e questa operazione causerà risultati imprevedibili.</span><span class="sxs-lookup"><span data-stu-id="a6883-160">GX_STYLE_TEXT_COPY should not be cleared after it has been set, and doing so will cause unpredictable results.</span></span>

<span data-ttu-id="a6883-161">__***Stili del pulsante (si applica solo ai tipi di widget del pulsante GUIX):***__</span><span class="sxs-lookup"><span data-stu-id="a6883-161">__***Button Styles (apply only to GUIX button widget types):***__</span></span>

<span data-ttu-id="a6883-162">**GX_STYLE_BUTTON_PUSHED**</span><span class="sxs-lookup"><span data-stu-id="a6883-162">**GX_STYLE_BUTTON_PUSHED**</span></span>
  - <span data-ttu-id="a6883-163">Valore 0x00000010</span><span class="sxs-lookup"><span data-stu-id="a6883-163">Value 0x00000010</span></span>
  - <span data-ttu-id="a6883-164">Descrizione: indica che il pulsante si trova nello stato premuto o selezionato.</span><span class="sxs-lookup"><span data-stu-id="a6883-164">Description: Indicates the button is in the pushed or selected state.</span></span>

<span data-ttu-id="a6883-165">**GX_STYLE_BUTTON_TOGGLE**</span><span class="sxs-lookup"><span data-stu-id="a6883-165">**GX_STYLE_BUTTON_TOGGLE**</span></span>
  - <span data-ttu-id="a6883-166">Valore 0x00000020</span><span class="sxs-lookup"><span data-stu-id="a6883-166">Value 0x00000020</span></span>
  - <span data-ttu-id="a6883-167">Descrizione: il pulsante commuta lo stato tra push e unpushd a ogni evento click.</span><span class="sxs-lookup"><span data-stu-id="a6883-167">Description: Button will switch status between pushed and unpushed on every click event.</span></span> <span data-ttu-id="a6883-168">Questo stile viene comunemente usato con i pulsanti di stile "checkbox".</span><span class="sxs-lookup"><span data-stu-id="a6883-168">This style is commonly used with “checkbox” style buttons.</span></span>

<span data-ttu-id="a6883-169">**GX_STYLE_BUTTON_RADIO**</span><span class="sxs-lookup"><span data-stu-id="a6883-169">**GX_STYLE_BUTTON_RADIO**</span></span>
  - <span data-ttu-id="a6883-170">Valore 0x00000040</span><span class="sxs-lookup"><span data-stu-id="a6883-170">Value 0x00000040</span></span>
  - <span data-ttu-id="a6883-171">Descrizione: questo stile indica che il pulsante sarà esclusivo e deselezionando gli elementi di pari livello dei pulsanti quando vengono selezionati.</span><span class="sxs-lookup"><span data-stu-id="a6883-171">Description: This style indicates the button will be exclusive, and deselect any button siblings when selected.</span></span> <span data-ttu-id="a6883-172">Questo stile viene comunemente usato con i pulsanti di stile "pulsante di opzione".</span><span class="sxs-lookup"><span data-stu-id="a6883-172">This style is commonly used with “radio button” style buttons.</span></span>

<span data-ttu-id="a6883-173">**GX_STYLE_BUTTON_EVENT_ON_PUSH**</span><span class="sxs-lookup"><span data-stu-id="a6883-173">**GX_STYLE_BUTTON_EVENT_ON_PUSH**</span></span>
  - <span data-ttu-id="a6883-174">Valore: 0x00000080</span><span class="sxs-lookup"><span data-stu-id="a6883-174">Value: 0x00000080</span></span>
  - <span data-ttu-id="a6883-175">Descrizione: indica che il pulsante genera un evento Click quando inizialmente viene eseguito il push.</span><span class="sxs-lookup"><span data-stu-id="a6883-175">Description: Indicates the button generates a click event when initially pushed.</span></span> <span data-ttu-id="a6883-176">L'operazione predefinita prevede la generazione di un evento Click quando si rilascia il pulsante.</span><span class="sxs-lookup"><span data-stu-id="a6883-176">The default operation is to generate a click event when the button is released.</span></span>

<span data-ttu-id="a6883-177">**GX_STYLE_BUTTON_REPEAT**</span><span class="sxs-lookup"><span data-stu-id="a6883-177">**GX_STYLE_BUTTON_REPEAT**</span></span>
  - <span data-ttu-id="a6883-178">Valore 0x00000100</span><span class="sxs-lookup"><span data-stu-id="a6883-178">Value 0x00000100</span></span>
  - <span data-ttu-id="a6883-179">Descrizione: indica che il pulsante deve inviare eventi Click ripetuti al padre del pulsante quando il pulsante è premuto nello stato push.</span><span class="sxs-lookup"><span data-stu-id="a6883-179">Description: Indicates the button should send repeated click events to the button parent when the button is held in the pushed state.</span></span>

<span data-ttu-id="a6883-180">__***Stili elenco (si applica solo ai tipi di widget Elenco GUIX):***__</span><span class="sxs-lookup"><span data-stu-id="a6883-180">__***List Styles (apply only to GUIX list widget types):***__</span></span>

<span data-ttu-id="a6883-181">**GX_STYLE_CENTER_SELECTED**</span><span class="sxs-lookup"><span data-stu-id="a6883-181">**GX_STYLE_CENTER_SELECTED**</span></span> 
  - <span data-ttu-id="a6883-182">Valore: 0x00000010</span><span class="sxs-lookup"><span data-stu-id="a6883-182">Value: 0x00000010</span></span>
  - <span data-ttu-id="a6883-183">Descrizione: riservata</span><span class="sxs-lookup"><span data-stu-id="a6883-183">Description: Reserved</span></span>

<span data-ttu-id="a6883-184">**GX_STYLE_WRAP**</span><span class="sxs-lookup"><span data-stu-id="a6883-184">**GX_STYLE_WRAP**</span></span>
  - <span data-ttu-id="a6883-185">Valore 0x00000020</span><span class="sxs-lookup"><span data-stu-id="a6883-185">Value 0x00000020</span></span>
  - <span data-ttu-id="a6883-186">Descrizione: l'elenco di elementi figlio viene eseguito a capo dall'inizio alla fine quando l'elenco viene trascinato o spostato oltre l'indice dell'elenco iniziale o finale.</span><span class="sxs-lookup"><span data-stu-id="a6883-186">Description: The list children wrap from start to end when the list is dragged or scrolled past the starting or ending list index.</span></span>

<span data-ttu-id="a6883-187">**GX_STYLE_FLICKABLE**</span><span class="sxs-lookup"><span data-stu-id="a6883-187">**GX_STYLE_FLICKABLE**</span></span>
  - <span data-ttu-id="a6883-188">Valore: 0x00000040</span><span class="sxs-lookup"><span data-stu-id="a6883-188">Value: 0x00000040</span></span>
  - <span data-ttu-id="a6883-189">Descrizione: riservata</span><span class="sxs-lookup"><span data-stu-id="a6883-189">Description: Reserved</span></span>

<span data-ttu-id="a6883-190">__***Stili del pulsante di Pixelmap e dell'icona:***__</span><span class="sxs-lookup"><span data-stu-id="a6883-190">__***Pixelmap Button and Icon Button Styles:***__</span></span>

<span data-ttu-id="a6883-191">**GX_STYLE_HALIGN_CENTER**</span><span class="sxs-lookup"><span data-stu-id="a6883-191">**GX_STYLE_HALIGN_CENTER**</span></span>
  - <span data-ttu-id="a6883-192">Valore: 0x00010000</span><span class="sxs-lookup"><span data-stu-id="a6883-192">Value: 0x00010000</span></span>
  - <span data-ttu-id="a6883-193">Descrizione: il pulsante Pixelmap deve essere allineato al centro all'interno del bordo del pulsante sull'asse orizzontale.</span><span class="sxs-lookup"><span data-stu-id="a6883-193">Description: The button pixelmap should be center aligned within the button boundary on the horizontal axis.</span></span>

<span data-ttu-id="a6883-194">**GX_STYLE_HALIGN_LEFT**</span><span class="sxs-lookup"><span data-stu-id="a6883-194">**GX_STYLE_HALIGN_LEFT**</span></span>
  - <span data-ttu-id="a6883-195">Valore: 0x00020000</span><span class="sxs-lookup"><span data-stu-id="a6883-195">Value: 0x00020000</span></span>
  - <span data-ttu-id="a6883-196">Descrizione: il pulsante Pixelmap deve essere allineato all'interno del bordo del pulsante sull'asse orizzontale.</span><span class="sxs-lookup"><span data-stu-id="a6883-196">Description: The button pixelmap should be left aligned within the button boundary on the horizontal axis.</span></span>

<span data-ttu-id="a6883-197">**GX_STYLE_HALIGN_RIGHT**</span><span class="sxs-lookup"><span data-stu-id="a6883-197">**GX_STYLE_HALIGN_RIGHT**</span></span>
  - <span data-ttu-id="a6883-198">Valore 0x00040000</span><span class="sxs-lookup"><span data-stu-id="a6883-198">Value 0x00040000</span></span>
  - <span data-ttu-id="a6883-199">Descrizione: il pulsante Pixelmap deve essere allineato a destra all'interno del bordo del pulsante sull'asse orizzontale.</span><span class="sxs-lookup"><span data-stu-id="a6883-199">Description: The button pixelmap should be right aligned within the button boundary on the horizontal axis.</span></span>

<span data-ttu-id="a6883-200">**GX_STYLE_VALIGN_CENTER**</span><span class="sxs-lookup"><span data-stu-id="a6883-200">**GX_STYLE_VALIGN_CENTER**</span></span>
  - <span data-ttu-id="a6883-201">Valore 0x00080000</span><span class="sxs-lookup"><span data-stu-id="a6883-201">Value 0x00080000</span></span>
  - <span data-ttu-id="a6883-202">Descrizione: il pulsante Pixelmap deve essere allineato al centro all'interno del bordo del pulsante sull'asse verticale.</span><span class="sxs-lookup"><span data-stu-id="a6883-202">Description: The button pixelmap should be center aligned within the button boundary on the vertical axis.</span></span>

<span data-ttu-id="a6883-203">**GX_STYLE_VALIGN_TOP**</span><span class="sxs-lookup"><span data-stu-id="a6883-203">**GX_STYLE_VALIGN_TOP**</span></span>
  - <span data-ttu-id="a6883-204">Valore: 0x00100000</span><span class="sxs-lookup"><span data-stu-id="a6883-204">Value: 0x00100000</span></span>
  - <span data-ttu-id="a6883-205">Descrizione: il pulsante Pixelmap deve essere allineato in alto all'interno del bordo del pulsante sull'asse verticale.</span><span class="sxs-lookup"><span data-stu-id="a6883-205">Description: The button pixelmap should be top aligned within the button boundary on the vertical axis.</span></span>

<span data-ttu-id="a6883-206">**GX_STYLE_VALIGN_BOTTOM**</span><span class="sxs-lookup"><span data-stu-id="a6883-206">**GX_STYLE_VALIGN_BOTTOM**</span></span>
  - <span data-ttu-id="a6883-207">Valore: 0x00200000</span><span class="sxs-lookup"><span data-stu-id="a6883-207">Value: 0x00200000</span></span>
  - <span data-ttu-id="a6883-208">Descrizione: il pulsante Pixelmap deve essere allineato in basso all'interno del bordo del pulsante sull'asse orizzontale verticale.</span><span class="sxs-lookup"><span data-stu-id="a6883-208">Description: The button pixelmap should be bottom aligned within the button boundary on the vertical horizontal axis.</span></span>

<span data-ttu-id="a6883-209">__***Stili del dispositivo di scorrimento (Appy solo per GX_SLIDER e i tipi di widget derivati):***__</span><span class="sxs-lookup"><span data-stu-id="a6883-209">__***Slider Styles (Appy only to GX_SLIDER and derived widget types):***__</span></span>

<span data-ttu-id="a6883-210">**GX_STYLE_SHOW_NEEDLE**</span><span class="sxs-lookup"><span data-stu-id="a6883-210">**GX_STYLE_SHOW_NEEDLE**</span></span>
  - <span data-ttu-id="a6883-211">Valore: 0x00000200</span><span class="sxs-lookup"><span data-stu-id="a6883-211">Value: 0x00000200</span></span>
  - <span data-ttu-id="a6883-212">Descrizione: questo stile deve essere incluso affinché il dispositivo di scorrimento disegni l'indicatore della lancetta.</span><span class="sxs-lookup"><span data-stu-id="a6883-212">Description: This style must be included for the slider to draw the needle indicator.</span></span> <span data-ttu-id="a6883-213">Questo stile può essere disabilitato se l'applicazione vuole disabilitare l'ago del dispositivo di scorrimento o creare un indicatore lancetta personalizzato.</span><span class="sxs-lookup"><span data-stu-id="a6883-213">This style can be disabled if the application wants to disable the slider needle or draw a custom needle indicator.</span></span>

<span data-ttu-id="a6883-214">**GX_STYLE_SHOW_TICKMARKS**</span><span class="sxs-lookup"><span data-stu-id="a6883-214">**GX_STYLE_SHOW_TICKMARKS**</span></span>
  - <span data-ttu-id="a6883-215">Valore: 0x00000400</span><span class="sxs-lookup"><span data-stu-id="a6883-215">Value: 0x00000400</span></span>
  - <span data-ttu-id="a6883-216">Descrizione: il widget del dispositivo di scorrimento eseguirà il disegno del software di linee TickMark tratteggiate quando lo stile è abilitato.</span><span class="sxs-lookup"><span data-stu-id="a6883-216">Description: The slider widget will do software drawing of dashed tickmark lines when this style is enabled.</span></span>

<span data-ttu-id="a6883-217">**GX_STYLE_SLIDER_VERTICAL**</span><span class="sxs-lookup"><span data-stu-id="a6883-217">**GX_STYLE_SLIDER_VERTICAL**</span></span>
  - <span data-ttu-id="a6883-218">Valore 0x00000800</span><span class="sxs-lookup"><span data-stu-id="a6883-218">Value 0x00000800</span></span>
  - <span data-ttu-id="a6883-219">Descrizione: impostare questo flag di stile per creare un dispositivo di scorrimento verticale e deselezionare questo flag di stile per creare un dispositivo di scorrimento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="a6883-219">Description: Set this style flag to create a vertical slider, and clear this style flag to create a horizontal slider.</span></span>

<span data-ttu-id="a6883-220">__***Stili sprite (si applica solo ai tipi di widget GX_SPRITE):***__</span><span class="sxs-lookup"><span data-stu-id="a6883-220">__***Sprite Styles (Applies only to GX_SPRITE widget types):***__</span></span>

<span data-ttu-id="a6883-221">**GX_STYLE_SPRITE_AUTO**</span><span class="sxs-lookup"><span data-stu-id="a6883-221">**GX_STYLE_SPRITE_AUTO**</span></span>
  - <span data-ttu-id="a6883-222">Valore: 0x00000010</span><span class="sxs-lookup"><span data-stu-id="a6883-222">Value: 0x00000010</span></span>
  - <span data-ttu-id="a6883-223">Descrizione: indica che l'animazione sprite verrà eseguita automaticamente quando il widget sprite riceve l'evento GX_EVENT_SHOW.</span><span class="sxs-lookup"><span data-stu-id="a6883-223">Description: Indicates the sprite animation will run automatically when the sprite widget received the GX_EVENT_SHOW event.</span></span>

<span data-ttu-id="a6883-224">**GX_STYLE_SPRITE_LOOP**</span><span class="sxs-lookup"><span data-stu-id="a6883-224">**GX_STYLE_SPRITE_LOOP**</span></span>
  - <span data-ttu-id="a6883-225">Valore: 0x00000020</span><span class="sxs-lookup"><span data-stu-id="a6883-225">Value: 0x00000020</span></span>
  - <span data-ttu-id="a6883-226">Descrizione: con questo stile, il widget sprite continuerà a scorrere continuamente i frame di animazione sprite fino a quando lo sprite non verrà interrotto dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6883-226">Description: With this style, the sprite widget will continuously loop through sprite animation frames until the sprite is stopped by the application.</span></span>

<span data-ttu-id="a6883-227">__***Stili del dispositivo di scorrimento Pixelmap:***__</span><span class="sxs-lookup"><span data-stu-id="a6883-227">__***Pixelmap Slider Styles:***__</span></span>

<span data-ttu-id="a6883-228">**GX_STYLE_TILE_BACKGROUND**</span><span class="sxs-lookup"><span data-stu-id="a6883-228">**GX_STYLE_TILE_BACKGROUND**</span></span>
  - <span data-ttu-id="a6883-229">Valore 0x00001000</span><span class="sxs-lookup"><span data-stu-id="a6883-229">Value 0x00001000</span></span>
  - <span data-ttu-id="a6883-230">Descrizione: per riempire il rettangolo di delimitazione dello sprite, viene affiancata l'immagine di sfondo del dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="a6883-230">Description: The slider background image is tiled to fill the sprite bounding rectangle.</span></span> <span data-ttu-id="a6883-231">In questo modo, è possibile usare una piccola immagine a striscia verticale o orizzontale per riempire lo sfondo del dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="a6883-231">This allows a small vertical or horizontal stripe image to be used to fill the slider background.</span></span>

<span data-ttu-id="a6883-232">__***Stili aggiuntivi dell'indicatore di stato:***__</span><span class="sxs-lookup"><span data-stu-id="a6883-232">__***Additional Progress Bar Styles:***__</span></span>

<span data-ttu-id="a6883-233">**GX_STYLE_PROGRESS_PERCENT**</span><span class="sxs-lookup"><span data-stu-id="a6883-233">**GX_STYLE_PROGRESS_PERCENT**</span></span>
  - <span data-ttu-id="a6883-234">Valore: 0x00000010</span><span class="sxs-lookup"><span data-stu-id="a6883-234">Value: 0x00000010</span></span>
  - <span data-ttu-id="a6883-235">Descrizione: quando questo stile è impostato, l'indicatore di stato disegna il valore della barra come percentuale anziché come valore non elaborato.</span><span class="sxs-lookup"><span data-stu-id="a6883-235">Description: When this style is set, the progress bar will draw  bar value as a percentage rather than a raw value.</span></span> <span data-ttu-id="a6883-236">Il testo viene centrato nel rettangolo di delimitazione della barra di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="a6883-236">The text is centered in the progress bar bounding rectangle.</span></span>

<span data-ttu-id="a6883-237">**GX_STYLE_PROGRESS_TEXT_DRAW**</span><span class="sxs-lookup"><span data-stu-id="a6883-237">**GX_STYLE_PROGRESS_TEXT_DRAW**</span></span>
  - <span data-ttu-id="a6883-238">Valore: 0x00000020</span><span class="sxs-lookup"><span data-stu-id="a6883-238">Value: 0x00000020</span></span>
  - <span data-ttu-id="a6883-239">Descrizione: creare il valore indicatore di stato corrente come testo decimale centrato all'interno dell'indicatore di stato.</span><span class="sxs-lookup"><span data-stu-id="a6883-239">Description: Draw the current progress bar value as decimal text centered within the progress bar.</span></span>

<span data-ttu-id="a6883-240">**GX_STYLE_PROGRESS_VERTICAL**</span><span class="sxs-lookup"><span data-stu-id="a6883-240">**GX_STYLE_PROGRESS_VERTICAL**</span></span>
  - <span data-ttu-id="a6883-241">Valore: 0x0000040</span><span class="sxs-lookup"><span data-stu-id="a6883-241">Value: 0x0000040</span></span>
  - <span data-ttu-id="a6883-242">Descrizione: indicare che lo stato di avanzamento è orientato verticalmente.</span><span class="sxs-lookup"><span data-stu-id="a6883-242">Description: Indicate the progress is vertically oriented.</span></span> <span data-ttu-id="a6883-243">Il valore predefinito è orientamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="a6883-243">The default is horizontal orientation.</span></span>

<span data-ttu-id="a6883-244">**GX_STYLE_PROGRESS_SEGMENT_FILL**:</span><span class="sxs-lookup"><span data-stu-id="a6883-244">**GX_STYLE_PROGRESS_SEGMENT_FILL**:</span></span>
  - <span data-ttu-id="a6883-245">**Valore**: 0x00000100</span><span class="sxs-lookup"><span data-stu-id="a6883-245">**Value**: 0x00000100</span></span>
  - <span data-ttu-id="a6883-246">Descrizione: il valore dell'indicatore di stato è indicato con rettangoli riempiti segmentati, anziché come riempimento a tinta unita.</span><span class="sxs-lookup"><span data-stu-id="a6883-246">Description: The progress bar value is indicated with segmented filled rectangles, rather than a solid fill.</span></span>

<span data-ttu-id="a6883-247">__***Stili aggiuntivi indicatore di stato radiali:***__</span><span class="sxs-lookup"><span data-stu-id="a6883-247">__***Additional Radial Progress Bar Styles:***__</span></span>

<span data-ttu-id="a6883-248">**GX_STYLE_RADIAL_PROGRESS_ALIAS**</span><span class="sxs-lookup"><span data-stu-id="a6883-248">**GX_STYLE_RADIAL_PROGRESS_ALIAS**</span></span>
  - <span data-ttu-id="a6883-249">Valore: 0x00000200</span><span class="sxs-lookup"><span data-stu-id="a6883-249">Value: 0x00000200</span></span>
  - <span data-ttu-id="a6883-250">Descrizione: disegnare la barra di stato radiale usando gli stili di pennello anti-aliasing.</span><span class="sxs-lookup"><span data-stu-id="a6883-250">Description: Draw the radial progress bar using anti-aliased brush styles.</span></span> <span data-ttu-id="a6883-251">Questa operazione richiede una maggiore larghezza di banda della CPU, ma produce anche un aspetto più gradevole.</span><span class="sxs-lookup"><span data-stu-id="a6883-251">This requires more CPU bandwidth but also produces a nicer appearance.</span></span> <span data-ttu-id="a6883-252">Per gli obiettivi di CPU con prestazioni inferiori, la cancellazione di questo flag di stile comporterà una maggiore velocità di disegno.</span><span class="sxs-lookup"><span data-stu-id="a6883-252">For lower performance CPU targets, clearing this style flag will result in faster drawing speed.</span></span>

<span data-ttu-id="a6883-253">**GX_STYLE_RADIAL_PROGRESS_ROUND**</span><span class="sxs-lookup"><span data-stu-id="a6883-253">**GX_STYLE_RADIAL_PROGRESS_ROUND**</span></span>
  - <span data-ttu-id="a6883-254">Valore: 0x00000400</span><span class="sxs-lookup"><span data-stu-id="a6883-254">Value: 0x00000400</span></span>
  - <span data-ttu-id="a6883-255">Descrizione: usare uno stile di pennello finale della linea rotonda quando si disegna l'arco dell'indicatore di stato radiale. Il valore predefinito è una fine della riga quadrata.</span><span class="sxs-lookup"><span data-stu-id="a6883-255">Description: Use a round line end brush style when drawing the radial progress bar arc. The default is a square line end.</span></span>

<span data-ttu-id="a6883-256">__***Stili di input di testo aggiuntivi:***__</span><span class="sxs-lookup"><span data-stu-id="a6883-256">__***Additional Text Input Styles:***__</span></span>

<span data-ttu-id="a6883-257">**GX_STYLE_ CURSOR_BLINK**</span><span class="sxs-lookup"><span data-stu-id="a6883-257">**GX_STYLE_ CURSOR_BLINK**</span></span>
  - <span data-ttu-id="a6883-258">Valore: 0x00000040</span><span class="sxs-lookup"><span data-stu-id="a6883-258">Value: 0x00000040</span></span>
  - <span data-ttu-id="a6883-259">Descrizione: il cursore del widget input di testo lampeggerà e non verrà più stazionario.</span><span class="sxs-lookup"><span data-stu-id="a6883-259">Description: The text input widget cursor will flash on and off rather than being steady.</span></span>

<span data-ttu-id="a6883-260">**GX_STYLE_ CURSOR_ALWAYS**</span><span class="sxs-lookup"><span data-stu-id="a6883-260">**GX_STYLE_ CURSOR_ALWAYS**</span></span>
  - <span data-ttu-id="a6883-261">Valore: 0x00000080</span><span class="sxs-lookup"><span data-stu-id="a6883-261">Value: 0x00000080</span></span>
  - <span data-ttu-id="a6883-262">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a6883-262">Description.</span></span> <span data-ttu-id="a6883-263">Il cursore del widget input di testo viene in genere visualizzato solo quando il widget possiede lo stato attivo per l'input.</span><span class="sxs-lookup"><span data-stu-id="a6883-263">The text input widget cursor is normally only displayed when the widget owns input focus.</span></span> <span data-ttu-id="a6883-264">Questo flag di stile renderà il cursore sempre visibile indipendentemente dallo stato attivo per l'input.</span><span class="sxs-lookup"><span data-stu-id="a6883-264">This style flag will make the cursor always visible regardless of input focus.</span></span>

<span data-ttu-id="a6883-265">**GX_STYLE_TEXT_INPUT_NOTIFY_ALL**</span><span class="sxs-lookup"><span data-stu-id="a6883-265">**GX_STYLE_TEXT_INPUT_NOTIFY_ALL**</span></span>
  - <span data-ttu-id="a6883-266">Valore: 0x00000100</span><span class="sxs-lookup"><span data-stu-id="a6883-266">Value: 0x00000100</span></span>
  - <span data-ttu-id="a6883-267">Descrizione: con questo flag di stile impostare l'evento GX_EVENT_TEXT_EDITED ogni volta che viene ricevuto un evento di chiave inattiva dal widget input di testo.</span><span class="sxs-lookup"><span data-stu-id="a6883-267">Description: With this style flag set the GX_EVENT_TEXT_EDITED event every time key down event is received by the text input widget.</span></span>

<span data-ttu-id="a6883-268">__***Stili di finestra aggiuntivi:***__</span><span class="sxs-lookup"><span data-stu-id="a6883-268">__***Additional Window Styles:***__</span></span>

<span data-ttu-id="a6883-269">**GX_STYLE_TILE_WALLPAPER**</span><span class="sxs-lookup"><span data-stu-id="a6883-269">**GX_STYLE_TILE_WALLPAPER**</span></span>
  - <span data-ttu-id="a6883-270">Valore: 0x00040000</span><span class="sxs-lookup"><span data-stu-id="a6883-270">Value: 0x00040000</span></span>
  - <span data-ttu-id="a6883-271">Descrizione: nella finestra viene affiancata un'immagine di sfondo assegnata per riempire il rettangolo client della finestra.</span><span class="sxs-lookup"><span data-stu-id="a6883-271">Description: The window will tile any assigned wallpaper image to fill the window client rectangle.</span></span>

<span data-ttu-id="a6883-272">**GX_STYLE_AUTO_HSCROLL**</span><span class="sxs-lookup"><span data-stu-id="a6883-272">**GX_STYLE_AUTO_HSCROLL**</span></span>
  - <span data-ttu-id="a6883-273">Valore: 0x00100000</span><span class="sxs-lookup"><span data-stu-id="a6883-273">Value: 0x00100000</span></span>
  - <span data-ttu-id="a6883-274">Descrizione: riservata per un utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="a6883-274">Description: Reserved for future use.</span></span>

<span data-ttu-id="a6883-275">**GX_STYLE_AUTO_VSCROLL**</span><span class="sxs-lookup"><span data-stu-id="a6883-275">**GX_STYLE_AUTO_VSCROLL**</span></span>
  - <span data-ttu-id="a6883-276">Valore: 0x00200000</span><span class="sxs-lookup"><span data-stu-id="a6883-276">Value: 0x00200000</span></span>
  - <span data-ttu-id="a6883-277">Descrizione: riservata per un utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="a6883-277">Description: Reserved for future use.</span></span>

<span data-ttu-id="a6883-278">__***Stili di menu aggiuntivi:***__</span><span class="sxs-lookup"><span data-stu-id="a6883-278">__***Additional Menu Styles:***__</span></span>

<span data-ttu-id="a6883-279">**GX_STYLE_MENU_EXPANDED**</span><span class="sxs-lookup"><span data-stu-id="a6883-279">**GX_STYLE_MENU_EXPANDED**</span></span>
  - <span data-ttu-id="a6883-280">Valore: 0x00000010</span><span class="sxs-lookup"><span data-stu-id="a6883-280">Value: 0x00000010</span></span>
  - <span data-ttu-id="a6883-281">Descrizione: il widget del menu Accordion è inizialmente in stato espanso.</span><span class="sxs-lookup"><span data-stu-id="a6883-281">Description: Accordion menu widget is initially in expanded state.</span></span>

<span data-ttu-id="a6883-282">__***Stili di visualizzazione ad albero aggiuntivi:***__</span><span class="sxs-lookup"><span data-stu-id="a6883-282">__***Additional Tree View Styles:***__</span></span>

<span data-ttu-id="a6883-283">**GX_STYLE_TREE_VIEW_SHOW_ROOT_LINES**</span><span class="sxs-lookup"><span data-stu-id="a6883-283">**GX_STYLE_TREE_VIEW_SHOW_ROOT_LINES**</span></span>
  - <span data-ttu-id="a6883-284">Valore: 0x00000010</span><span class="sxs-lookup"><span data-stu-id="a6883-284">Value: 0x00000010</span></span>
  - <span data-ttu-id="a6883-285">Descrizione: il widget visualizzazione albero deve creare righe dall'icona del nodo al nodo radice della struttura ad albero.</span><span class="sxs-lookup"><span data-stu-id="a6883-285">Description: Tree view widget should draw lines from node icon to root tree node.</span></span>

<span data-ttu-id="a6883-286">__***Stili aggiuntivi della barra di scorrimento:***__</span><span class="sxs-lookup"><span data-stu-id="a6883-286">__***Additional Scrollbar Styles:***__</span></span>

<span data-ttu-id="a6883-287">**GX_SCROLLBAR_BACKGROUND_TILE**</span><span class="sxs-lookup"><span data-stu-id="a6883-287">**GX_SCROLLBAR_BACKGROUND_TILE**</span></span>
  - <span data-ttu-id="a6883-288">Valore: 0x00010000</span><span class="sxs-lookup"><span data-stu-id="a6883-288">Value: 0x00010000</span></span>
  - <span data-ttu-id="a6883-289">Descrizione: riservata per un utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="a6883-289">Description: Reserved for future use.</span></span>

<span data-ttu-id="a6883-290">**GX_SCROLLBAR_RELATIVE_THUMB**</span><span class="sxs-lookup"><span data-stu-id="a6883-290">**GX_SCROLLBAR_RELATIVE_THUMB**</span></span>
  - <span data-ttu-id="a6883-291">Valore: 0x00020000</span><span class="sxs-lookup"><span data-stu-id="a6883-291">Value: 0x00020000</span></span>
  - <span data-ttu-id="a6883-292">Descrizione: la larghezza del cursore della barra di scorrimento (per una barra di scorrimento orizzontale) o l'altezza (per una barra di scorrimento verticale) vengono calcolate in base al rapporto tra l'area visibile della finestra padre e l'intervallo minimo e massimo della barra di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="a6883-292">Description: The scrollbar thumb width (for a horizontal scroll bar) or height (for a vertical scroll bar) are calculated based on the ratio of the visible area of the parent window to the min and max scrollbar range.</span></span>

<span data-ttu-id="a6883-293">**GX_SCROLLBAR_END_BUTTONS**</span><span class="sxs-lookup"><span data-stu-id="a6883-293">**GX_SCROLLBAR_END_BUTTONS**</span></span>
  - <span data-ttu-id="a6883-294">Valore: 0x00040000</span><span class="sxs-lookup"><span data-stu-id="a6883-294">Value: 0x00040000</span></span>
  - <span data-ttu-id="a6883-295">Descrizione: la barra di scorrimento Crea e connette automaticamente i pulsanti a ogni estremità dell'area della barra di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="a6883-295">Description: The scrollbar automatically creates and attaches buttons at each end of the scrollbar region.</span></span>

<span data-ttu-id="a6883-296">**GX_SCROLLBAR_VERTICAL**</span><span class="sxs-lookup"><span data-stu-id="a6883-296">**GX_SCROLLBAR_VERTICAL**</span></span> 
  - <span data-ttu-id="a6883-297">Valore: 0x01000000</span><span class="sxs-lookup"><span data-stu-id="a6883-297">Value: 0x01000000</span></span>
  - <span data-ttu-id="a6883-298">Descrizione: la barra di scorrimento è orientata verticalmente.</span><span class="sxs-lookup"><span data-stu-id="a6883-298">Description: The scrollbar is vertically oriented.</span></span>

<span data-ttu-id="a6883-299">**GX_SCROLLBAR_HORIZONTAL**</span><span class="sxs-lookup"><span data-stu-id="a6883-299">**GX_SCROLLBAR_HORIZONTAL**</span></span>
  - <span data-ttu-id="a6883-300">Valore: 0x02000000</span><span class="sxs-lookup"><span data-stu-id="a6883-300">Value: 0x02000000</span></span>
  - <span data-ttu-id="a6883-301">Descrizione: la barra di scorrimento è orientata orizzontalmente.</span><span class="sxs-lookup"><span data-stu-id="a6883-301">Description: The scrollbar is horizontally oriented.</span></span>

<span data-ttu-id="a6883-302">__***Stili rotellina di scorrimento testo:***__</span><span class="sxs-lookup"><span data-stu-id="a6883-302">__***Text Scroll Wheel Styles:***__</span></span>

<span data-ttu-id="a6883-303">**GX_STYLE_TEXT_SCROLL_WHEEL_ROUND**</span><span class="sxs-lookup"><span data-stu-id="a6883-303">**GX_STYLE_TEXT_SCROLL_WHEEL_ROUND**</span></span>
  - <span data-ttu-id="a6883-304">Valore: 0x00000200</span><span class="sxs-lookup"><span data-stu-id="a6883-304">Value: 0x00000200</span></span>
  - <span data-ttu-id="a6883-305">Descrizione: la rotellina di scorrimento usa un algoritmo sinusoidale per fare in modo che la rotellina di scorrimento appaia con una forma arrotondata.</span><span class="sxs-lookup"><span data-stu-id="a6883-305">Description: The scroll wheel uses a Sinusoidal algorithm to make the scroll wheel appear to have a rounded shape.</span></span> <span data-ttu-id="a6883-306">Questo flag di stile può comportare un sovraccarico significativo per le prestazioni del widget della rotellina di scorrimento, ma anche un aspetto realistico 3D.</span><span class="sxs-lookup"><span data-stu-id="a6883-306">This style flag can add significant overhead to the performance of the scroll wheel widget, but can also give the wheel a 3D realistic appearance.</span></span>