---
title: Informazioni Azure RTOS FileX
description: Azure RTOS FileX è un file system compatibile con FAT (High Performance, Tabella di allocazione file) completamente integrato con Azure RTOS ThreadX e disponibile per tutti i processori supportati. Come Azure RTOS ThreadX, Azure RTOS FileX è progettato per avere un footprint ridotto e prestazioni elevate, rendendolo ideale per le applicazioni attualmente incorporate che richiedono operazioni di gestione dei file. FileX supporta la maggior parte dei supporti fisici, tra cui RAM, Azure RTOS memoria flash USBX, SD CARD e NAND/NOR tramite Azure RTOS LevelX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: 0a54f160c96fb3e90c2295ae72020c121d367a12
ms.sourcegitcommit: 19d50693d8f5287ba6938ae1d23eef88435ed7b1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2021
ms.locfileid: "108171353"
---
# <a name="overview-of-azure-rtos-filex"></a><span data-ttu-id="d7eb0-105">Panoramica di Azure RTOS FileX</span><span class="sxs-lookup"><span data-stu-id="d7eb0-105">Overview of Azure RTOS FileX</span></span>

<span data-ttu-id="d7eb0-106">Azure RTOS fileX embedded file system è la soluzione avanzata di livello industriale di Azure RTOS per i formati di file FAT Microsoft, progettata specificamente per applicazioni IoT, in tempo reale e con un'incorporazione approfondita.</span><span class="sxs-lookup"><span data-stu-id="d7eb0-106">Azure RTOS FileX embedded file system is Azure RTOS's advanced, industrial grade solution for Microsoft FAT file formats, designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="d7eb0-107">Azure RTOS FileX supporta tutti i formati di file microsoft, inclusi FAT12, FAT16, FAT32 ed exFAT.</span><span class="sxs-lookup"><span data-stu-id="d7eb0-107">Azure RTOS FileX supports all of Microsoft’s file formats, including FAT12, FAT16, FAT32, and exFAT.</span></span> <span data-ttu-id="d7eb0-108">FileX offre anche la tolleranza di errore facoltativa e il livellamento dell'usura FLASH tramite un prodotto aggiuntivo denominato [Azure RTOS LevelX](https://docs.microsoft.com/azure/rtos/levelx/).</span><span class="sxs-lookup"><span data-stu-id="d7eb0-108">FileX also offers optional fault tolerance and FLASH wear leveling via an add-on product called [Azure RTOS LevelX](https://docs.microsoft.com/azure/rtos/levelx/).</span></span> <span data-ttu-id="d7eb0-109">Tutto questo in combinazione con un footprint ridotto, un'esecuzione rapida e una maggiore facilità d'uso, rendono Azure RTOS FileX la scelta ideale per le applicazioni IoT incorporate più complesse.</span><span class="sxs-lookup"><span data-stu-id="d7eb0-109">All of this combined with a small footprint, fast execution, and superior ease-of-use, make Azure RTOS FileX the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="d7eb0-110">Protocolli API</span><span class="sxs-lookup"><span data-stu-id="d7eb0-110">API protocols</span></span>

### <a name="media-services"></a><span data-ttu-id="d7eb0-111">Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="d7eb0-111">Media Services</span></span>

- <span data-ttu-id="d7eb0-112">Supporto di FAT 16/16/32 ed exFAT</span><span class="sxs-lookup"><span data-stu-id="d7eb0-112">FAT 12/16/32 and exFAT support</span></span>
- <span data-ttu-id="d7eb0-113">MINIMO FLASH da 6 KB, 2,5 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="d7eb0-113">Minimal 6KB FLASH, 2.5KB RAM</span></span>
- <span data-ttu-id="d7eb0-114">Completare i servizi di accesso ai supporti</span><span class="sxs-lookup"><span data-stu-id="d7eb0-114">Complete media access services</span></span>
- <span data-ttu-id="d7eb0-115">Numero illimitato di istanze di supporti</span><span class="sxs-lookup"><span data-stu-id="d7eb0-115">Unlimited number of media instance</span></span>
- <span data-ttu-id="d7eb0-116">Interfaccia del driver del settore logico di lettura/scrittura semplice</span><span class="sxs-lookup"><span data-stu-id="d7eb0-116">Simple read/write logical sector driver interface</span></span>
- <span data-ttu-id="d7eb0-117">Supporto di più partizioni</span><span class="sxs-lookup"><span data-stu-id="d7eb0-117">Multiple partition support</span></span>
- <span data-ttu-id="d7eb0-118">Cache del settore logico</span><span class="sxs-lookup"><span data-stu-id="d7eb0-118">Logical sector cache</span></span>
- <span data-ttu-id="d7eb0-119">Cache delle voci FAT</span><span class="sxs-lookup"><span data-stu-id="d7eb0-119">FAT entry cache</span></span>
- <span data-ttu-id="d7eb0-120">Supporto facoltativo per la tolleranza di errore</span><span class="sxs-lookup"><span data-stu-id="d7eb0-120">Optional fault tolerance support</span></span>
- <span data-ttu-id="d7eb0-121">Aggiornamento FAT secondario posticipato</span><span class="sxs-lookup"><span data-stu-id="d7eb0-121">Deferred Secondary FAT update</span></span>
- <span data-ttu-id="d7eb0-122">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="d7eb0-122">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="d7eb0-123">API intuitive per l'accesso ai supporti, tra cui:</span><span class="sxs-lookup"><span data-stu-id="d7eb0-123">Intuitive media access APIs, including:</span></span>
  - <span data-ttu-id="d7eb0-124">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="d7eb0-124">fx_media_open</span></span>
  - <span data-ttu-id="d7eb0-125">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="d7eb0-125">fx_media_close</span></span>
  - <span data-ttu-id="d7eb0-126">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="d7eb0-126">fx_media_format</span></span>
  - <span data-ttu-id="d7eb0-127">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="d7eb0-127">fx_media_space_available</span></span>

### <a name="directory-services"></a><span data-ttu-id="d7eb0-128">Servizi directory</span><span class="sxs-lookup"><span data-stu-id="d7eb0-128">Directory Services</span></span>

- <span data-ttu-id="d7eb0-129">Percorsi fino a 256 byte</span><span class="sxs-lookup"><span data-stu-id="d7eb0-129">Up to 256 byte paths</span></span>
- <span data-ttu-id="d7eb0-130">Nomi di directory lunghi e 8.3 supportati</span><span class="sxs-lookup"><span data-stu-id="d7eb0-130">Long and 8.3 directory names supported</span></span>
- <span data-ttu-id="d7eb0-131">Creazione della directory & eliminazione</span><span class="sxs-lookup"><span data-stu-id="d7eb0-131">Directory create & delete</span></span>
- <span data-ttu-id="d7eb0-132">Navigazione e attraversamento delle directory</span><span class="sxs-lookup"><span data-stu-id="d7eb0-132">Directory navigation and traversal</span></span>
- <span data-ttu-id="d7eb0-133">Gestione degli attributi della directory</span><span class="sxs-lookup"><span data-stu-id="d7eb0-133">Directory attributes management</span></span>
- <span data-ttu-id="d7eb0-134">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="d7eb0-134">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="d7eb0-135">API intuitive per l'accesso alla directory, tra cui:</span><span class="sxs-lookup"><span data-stu-id="d7eb0-135">Intuitive directory access APIs, including:</span></span>
  - <span data-ttu-id="d7eb0-136">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="d7eb0-136">fx_directory_create</span></span>
  - <span data-ttu-id="d7eb0-137">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="d7eb0-137">fx_directory_delete</span></span>
  - <span data-ttu-id="d7eb0-138">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="d7eb0-138">fx_directory_attributes_set</span></span>
  - <span data-ttu-id="d7eb0-139">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="d7eb0-139">fx_directory_attributes_read</span></span>
  - <span data-ttu-id="d7eb0-140">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="d7eb0-140">fx_directory_first_entry_find</span></span>
  - <span data-ttu-id="d7eb0-141">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="d7eb0-141">fx_directory_next_entry_find</span></span>

### <a name="file-services"></a><span data-ttu-id="d7eb0-142">Servizi file</span><span class="sxs-lookup"><span data-stu-id="d7eb0-142">File Services</span></span>

- <span data-ttu-id="d7eb0-143">Flash minimo da 3,3 KB</span><span class="sxs-lookup"><span data-stu-id="d7eb0-143">Minimal 3.3KB FLASH</span></span>
- <span data-ttu-id="d7eb0-144">File aperti illimitati</span><span class="sxs-lookup"><span data-stu-id="d7eb0-144">Unlimited open files</span></span>
- <span data-ttu-id="d7eb0-145">I file di sola lettura possono essere aperti più volte</span><span class="sxs-lookup"><span data-stu-id="d7eb0-145">Read-only files can be opened multiple times</span></span>
- <span data-ttu-id="d7eb0-146">Nomi di directory lunghi e 8.3 supportati</span><span class="sxs-lookup"><span data-stu-id="d7eb0-146">Long and 8.3 directory names supported</span></span>
- <span data-ttu-id="d7eb0-147">Supporto di file contigui</span><span class="sxs-lookup"><span data-stu-id="d7eb0-147">Contiguous file support</span></span>
- <span data-ttu-id="d7eb0-148">Logica di ricerca rapida</span><span class="sxs-lookup"><span data-stu-id="d7eb0-148">Fast seek logic</span></span>
- <span data-ttu-id="d7eb0-149">Preallocazione dei cluster</span><span class="sxs-lookup"><span data-stu-id="d7eb0-149">Pre-allocation of clusters</span></span>
- <span data-ttu-id="d7eb0-150">Creazione, eliminazione e ridenominazione di file</span><span class="sxs-lookup"><span data-stu-id="d7eb0-150">File create, delete, and rename</span></span>
- <span data-ttu-id="d7eb0-151">Lettura, scrittura e lettura di file</span><span class="sxs-lookup"><span data-stu-id="d7eb0-151">File read, write, and see</span></span>
- <span data-ttu-id="d7eb0-152">Gestione degli attributi di file</span><span class="sxs-lookup"><span data-stu-id="d7eb0-152">File attributes management</span></span>
- <span data-ttu-id="d7eb0-153">Traccia a livello di sistema tramite Azure RTOS TraceX</span><span class="sxs-lookup"><span data-stu-id="d7eb0-153">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="d7eb0-154">API di accesso ai file intuitive, tra cui:</span><span class="sxs-lookup"><span data-stu-id="d7eb0-154">Intuitive file access APIs, including:</span></span>
  - <span data-ttu-id="d7eb0-155">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="d7eb0-155">fx_file_create</span></span>
  - <span data-ttu-id="d7eb0-156">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="d7eb0-156">fx_file_delete</span></span>
  - <span data-ttu-id="d7eb0-157">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="d7eb0-157">fx_file_attributes_set</span></span>
  - <span data-ttu-id="d7eb0-158">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="d7eb0-158">fx_file_attributes_read</span></span>
  - <span data-ttu-id="d7eb0-159">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="d7eb0-159">fx_file_read</span></span>
  - <span data-ttu-id="d7eb0-160">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="d7eb0-160">fx_file_seek</span></span>
  - <span data-ttu-id="d7eb0-161">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="d7eb0-161">fx_file_write</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="d7eb0-162">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="d7eb0-162">Advanced technology</span></span>

<span data-ttu-id="d7eb0-163">Azure RTOS FileX è una tecnologia avanzata, tra cui:</span><span class="sxs-lookup"><span data-stu-id="d7eb0-163">Azure RTOS FileX is advanced technology, including the following.</span></span>

- <span data-ttu-id="d7eb0-164">Supporto fat 12/16/32 ed exFAT</span><span class="sxs-lookup"><span data-stu-id="d7eb0-164">FAT 12/16/32 and exFAT support</span></span>
- <span data-ttu-id="d7eb0-165">Supporto di più partizioni</span><span class="sxs-lookup"><span data-stu-id="d7eb0-165">Multiple partition support</span></span>
- <span data-ttu-id="d7eb0-166">Scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="d7eb0-166">Automatic scaling</span></span>
- <span data-ttu-id="d7eb0-167">Neutrale endian</span><span class="sxs-lookup"><span data-stu-id="d7eb0-167">Endian neutral</span></span>
- <span data-ttu-id="d7eb0-168">Nome file lungo e supporto 8.3</span><span class="sxs-lookup"><span data-stu-id="d7eb0-168">Long file name and 8.3 support</span></span>
- <span data-ttu-id="d7eb0-169">Supporto della tolleranza di errore facoltativo</span><span class="sxs-lookup"><span data-stu-id="d7eb0-169">Optional fault tolerance support</span></span>
- <span data-ttu-id="d7eb0-170">Cache dei settori logici</span><span class="sxs-lookup"><span data-stu-id="d7eb0-170">Logical sector cache</span></span>
- <span data-ttu-id="d7eb0-171">Cache delle voci FAT</span><span class="sxs-lookup"><span data-stu-id="d7eb0-171">FAT entry cache</span></span>
- <span data-ttu-id="d7eb0-172">Preallocazione dei cluster</span><span class="sxs-lookup"><span data-stu-id="d7eb0-172">Pre-allocation of clusters</span></span>
- <span data-ttu-id="d7eb0-173">Supporto di file contigui</span><span class="sxs-lookup"><span data-stu-id="d7eb0-173">Contiguous file support</span></span>
- <span data-ttu-id="d7eb0-174">Metriche facoltative delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="d7eb0-174">Optional performance metrics</span></span>
- <span data-ttu-id="d7eb0-175">Azure RTOS di analisi del sistema TraceX</span><span class="sxs-lookup"><span data-stu-id="d7eb0-175">Azure RTOS TraceX system analysis support</span></span>

## <a name="nornand-wear-leveling-azure-rtos-levelx"></a><span data-ttu-id="d7eb0-176">NOR/NAND Wear Leveling (Azure RTOS LevelX)</span><span class="sxs-lookup"><span data-stu-id="d7eb0-176">NOR/NAND Wear Leveling (Azure RTOS LevelX)</span></span>

<span data-ttu-id="d7eb0-177">Azure RTOS LevelX è il prodotto Microsoft di livellamento per usura NOR/NAND FLASH.</span><span class="sxs-lookup"><span data-stu-id="d7eb0-177">Azure RTOS LevelX is Microsoft’s NOR/NAND FLASH wear leveling product.</span></span> <span data-ttu-id="d7eb0-178">Azure RTOS LevelX può essere usato in combinazione con FileX o come libreria di settore FLASH di lettura/scrittura diretta autonoma per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d7eb0-178">Azure RTOS LevelX can be used in conjunction with FileX or as a stand-alone, direct read/write FLASH sector library for the application.</span></span>
