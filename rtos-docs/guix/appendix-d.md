---
title: Appendice D-GUIX pennello, Canvas e gradiente attributi
description: Informazioni sugli attributi pennello, Canvas e sfumatura GUIX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 19c0687a54be244ae395124664b4b6da0f4e90b6
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823180"
---
# <a name="appendix-d---guix-brush-canvas-and-gradient-attributes"></a><span data-ttu-id="cd2e2-103">Appendice D-GUIX pennello, Canvas e gradiente attributi</span><span class="sxs-lookup"><span data-stu-id="cd2e2-103">Appendix D - GUIX Brush, Canvas and Gradient Attributes</span></span>

<span data-ttu-id="cd2e2-104">__**Stili pennello:**__</span><span class="sxs-lookup"><span data-stu-id="cd2e2-104">__**Brush Styles:**__</span></span>

<span data-ttu-id="cd2e2-105">**GX_BRUSH_OUTLINE**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-105">**GX_BRUSH_OUTLINE**</span></span>
- <span data-ttu-id="cd2e2-106">Valore: 0x0000</span><span class="sxs-lookup"><span data-stu-id="cd2e2-106">Value: 0x0000</span></span>
- <span data-ttu-id="cd2e2-107">Descrizione: questo stile del pennello si applica alle funzioni di disegno delle forme, ad esempio gx_canvas_rectangle_draw o gx_canvas_polygon_draw.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-107">Description: This brush style applies to shape drawing functions such as gx_canvas_rectangle_draw or gx_canvas_polygon_draw.</span></span> <span data-ttu-id="cd2e2-108">Questo stile indica che la forma deve essere delineata, oltre a un riempimento facoltativo.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-108">This style indicateds the shape should be outlined, in addition to optionally being fill.</span></span> <span data-ttu-id="cd2e2-109">Se lo stile del GX_BRUSH_OUTLINE è impostato e la GX_BRSUH_SOLID_FILL è deselezionata, la forma viene configurata solo con la delineatura.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-109">If the GX_BRUSH_OUTLINE style is set and the GX_BRSUH_SOLID_FILL is cleared, the shape is only outlined.</span></span>

<span data-ttu-id="cd2e2-110">**GX_BRUSH_SOLID_FILL**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-110">**GX_BRUSH_SOLID_FILL**</span></span>
- <span data-ttu-id="cd2e2-111">Valore: 0x0001</span><span class="sxs-lookup"><span data-stu-id="cd2e2-111">Value: 0x0001</span></span>
- <span data-ttu-id="cd2e2-112">Descrizione: questo stile del pennello si applica alle funzioni di disegno di forme e indica che la forma richiesta deve essere riempita con un colore a tinta unita utilizzando il colore di riempimento del pennello corrente.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-112">Description: This brush style applies to shape drawing functions, and indicates that the requested shape should be filled with a solid color using the current brush fill color.</span></span>

<span data-ttu-id="cd2e2-113">**GX_BRUSH_PIXELMAP_FILL**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-113">**GX_BRUSH_PIXELMAP_FILL**</span></span>
- <span data-ttu-id="cd2e2-114">Valore: 0x0002</span><span class="sxs-lookup"><span data-stu-id="cd2e2-114">Value: 0x0002</span></span>
- <span data-ttu-id="cd2e2-115">Descrizione: questo stile del pennello si applica alle funzioni di disegno di forme e indica che la forma richiesta deve essere un modello riempito con l'Pixelmap del pennello corrente.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-115">Description: This brush style applies to shape drawing functions, and indicates that the requested shape should be pattern filled with the current brush pixelmap.</span></span>

<span data-ttu-id="cd2e2-116">**GX_BRUSH_ALIAS**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-116">**GX_BRUSH_ALIAS**</span></span>
- <span data-ttu-id="cd2e2-117">Valore: 0x0004</span><span class="sxs-lookup"><span data-stu-id="cd2e2-117">Value: 0x0004</span></span>
- <span data-ttu-id="cd2e2-118">Descrizione: questo stile del pennello si applica a tutti i profili di disegno e di forma delle linee.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-118">Description: This brush style applies to all line drawing and shape outlines.</span></span> <span data-ttu-id="cd2e2-119">Se questo flag è impostato, le linee e le strutture vengono disegnate con il più accurato, ma anche più tempo per l'utilizzo di algoritmi di disegno anti-aliasing.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-119">If this flag is set, lines and outlines are drawing with the more accurate but also more time consuming anti-aliased drawing algorithms.</span></span> <span data-ttu-id="cd2e2-120">Questo flag di stile viene usato solo per le profondità di colore a 16 BPP e superiori.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-120">This style flag is only used for 16-bpp color depths and higher.</span></span>

<span data-ttu-id="cd2e2-121">**GX_BRUSH_UNDERLINE**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-121">**GX_BRUSH_UNDERLINE**</span></span>
- <span data-ttu-id="cd2e2-122">Valore: 0x0008</span><span class="sxs-lookup"><span data-stu-id="cd2e2-122">Value: 0x0008</span></span>
- <span data-ttu-id="cd2e2-123">Descrizione: questo flag si applica al disegno del testo e indica che il testo successivo disegnato deve essere sottolineato.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-123">Description: This flag applies to text drawing, and indicates that subsequent text drawn should be underlined.</span></span>

<span data-ttu-id="cd2e2-124">**GX_BRUSH_ROUND**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-124">**GX_BRUSH_ROUND**</span></span>
- <span data-ttu-id="cd2e2-125">Valore: 0x0010</span><span class="sxs-lookup"><span data-stu-id="cd2e2-125">Value: 0x0010</span></span>
- <span data-ttu-id="cd2e2-126">Descrizione: questo flag si applica al disegno della linea e indica che le estremità della riga vengono disegnate con una forma circolare o circolare, anziché la forma quadrata predefinita.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-126">Description: This flag applies to line drawing, and indicates that line ends are drawn with a round or circular shape, rather than the default square shape.</span></span>

<span data-ttu-id="cd2e2-127">__**Flag Canvas:**__</span><span class="sxs-lookup"><span data-stu-id="cd2e2-127">__**Canvas Flags:**__</span></span>

<span data-ttu-id="cd2e2-128">**GX_CANVAS_SIMPLE**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-128">**GX_CANVAS_SIMPLE**</span></span>
- <span data-ttu-id="cd2e2-129">Valore: 0x01</span><span class="sxs-lookup"><span data-stu-id="cd2e2-129">Value: 0x01</span></span>
- <span data-ttu-id="cd2e2-130">Descrizione: un'area di disegno della memoria usata per il disegno fuori schermo.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-130">Description: A memory canvas which is used to off-screen drawing.</span></span>

<span data-ttu-id="cd2e2-131">**GX_CANVAS_MANAGED**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-131">**GX_CANVAS_MANAGED**</span></span>
- <span data-ttu-id="cd2e2-132">Valore: 0x02</span><span class="sxs-lookup"><span data-stu-id="cd2e2-132">Value: 0x02</span></span>
- <span data-ttu-id="cd2e2-133">Descrizione: un'area di disegno che è stata scaricata automaticamente nella visualizzazione attiva, come parte del processo di compilazione composito o come parte dell'operazione di attivazione/disattivazione del buffer per le architetture con singolo Canvas.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-133">Description: A canvas which automatically flushed to the active display, either as part of the composite building process or as part of the buffer toggle operation for single-canvas architectures.</span></span>

<span data-ttu-id="cd2e2-134">**GX_CANVAS_VISIBLE**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-134">**GX_CANVAS_VISIBLE**</span></span>
- <span data-ttu-id="cd2e2-135">Valore: 0x04</span><span class="sxs-lookup"><span data-stu-id="cd2e2-135">Value: 0x04</span></span>
- <span data-ttu-id="cd2e2-136">Descrizione: questo flag può essere usato per attivare e disattivare un'area di disegno, senza perdere il contenuto del disegno dell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-136">Description: This flag can be used to turn on and off a canvas, without losing the canvas drawing contents.</span></span>

<span data-ttu-id="cd2e2-137">**GX_CANVAS_MODIFIED**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-137">**GX_CANVAS_MODIFIED**</span></span>
- <span data-ttu-id="cd2e2-138">Valore: 0x08</span><span class="sxs-lookup"><span data-stu-id="cd2e2-138">Value: 0x08</span></span>
- <span data-ttu-id="cd2e2-139">Descrizione: riservata per un utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-139">Description: Reserved for future use.</span></span>

<span data-ttu-id="cd2e2-140">**GX_CANVAS_COMPOSITE**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-140">**GX_CANVAS_COMPOSITE**</span></span>
- <span data-ttu-id="cd2e2-141">Valore: 0x20</span><span class="sxs-lookup"><span data-stu-id="cd2e2-141">Value: 0x20</span></span>
- <span data-ttu-id="cd2e2-142">Descrizione: questo flag viene usato dall'applicazione quando si configura un sistema con più Canvas che comporterà più Canvas gestite nell'area di disegno composita e il composito è il driven per il buffer del frame hardware.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-142">Description: This flag is used by the application when configuring a multiple-canvas system which will composite multiple managed canvases into the composite canvas, and the composite is the driven to the hardware frame buffer.</span></span>

<span data-ttu-id="cd2e2-143">__**Tipi di sfumatura:**__</span><span class="sxs-lookup"><span data-stu-id="cd2e2-143">__**Gradient Types:**__</span></span>

<span data-ttu-id="cd2e2-144">**GX_GRADIENT_TYPE_VERTICAL**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-144">**GX_GRADIENT_TYPE_VERTICAL**</span></span>
- <span data-ttu-id="cd2e2-145">Valore: 0x01</span><span class="sxs-lookup"><span data-stu-id="cd2e2-145">Value: 0x01</span></span>
- <span data-ttu-id="cd2e2-146">Descrizione: crea una sfumatura AlphaMap verticale.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-146">Description: Creates a vertical alphamap gradient.</span></span>

<span data-ttu-id="cd2e2-147">**GX_GRADIENT_TYPE_ALPHA**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-147">**GX_GRADIENT_TYPE_ALPHA**</span></span>
- <span data-ttu-id="cd2e2-148">Valore: 0x02</span><span class="sxs-lookup"><span data-stu-id="cd2e2-148">Value: 0x02</span></span>
- <span data-ttu-id="cd2e2-149">Descrizione: crea una sfumatura di stile della mappa alfa.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-149">Description: Creats an alpha-map style gradient.</span></span> <span data-ttu-id="cd2e2-150">Si tratta attualmente dell'unico stile di sfumatura supportato.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-150">This is currently the only gradient style supported.</span></span>

<span data-ttu-id="cd2e2-151">**GX_GRADIENT_TYPE_MIRROR**</span><span class="sxs-lookup"><span data-stu-id="cd2e2-151">**GX_GRADIENT_TYPE_MIRROR**</span></span>
- <span data-ttu-id="cd2e2-152">Valore: 0x04</span><span class="sxs-lookup"><span data-stu-id="cd2e2-152">Value: 0x04</span></span>
- <span data-ttu-id="cd2e2-153">Descrizione: questo flag indica che la sfumatura deve raggiungere il picco al centro dell'intervallo di larghezza/altezza e tornare al valore iniziale mentre raggiunge il bordo destro/inferiore.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-153">Description: This flag indicates that the gradient should peak at the center of the width/height range, and return to the starting value as it reaches the right/bottom edge.</span></span> <span data-ttu-id="cd2e2-154">Senza questo flag di stile, la sfumatura sarà una sfumatura lineare dall'alto verso il basso o da sinistra a destra, a seconda del flag di GX_GRADIENT_TYPE_VERTICAL.</span><span class="sxs-lookup"><span data-stu-id="cd2e2-154">Without this style flag, the gradient will be a linear gradient from top-to-bottom or left-to-right, depending on the GX_GRADIENT_TYPE_VERTICAL flag.</span></span>