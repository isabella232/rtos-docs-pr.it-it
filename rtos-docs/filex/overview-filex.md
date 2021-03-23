---
title: Informazioni su Azure RTO FileX
description: Azure RTO FileX è un file system compatibile con le prestazioni elevate, che è compatibile con le tabelle di allocazione file (FAT), completamente integrato con Azure RTO ThreadX e disponibile per tutti i processori supportati. Analogamente ad Azure RTO ThreadX, Azure RTO FileX è progettato per avere un footprint ridotto e prestazioni elevate, rendendolo ideale per le applicazioni di oggi profondamente incorporate che richiedono operazioni di gestione file. FileX supporta la maggior parte dei supporti fisici, tra cui RAM, Azure RTO USBX, SD CARD e NAND/NOR Flash Memory tramite Azure RTO LevelX.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.service: rtos
ms.topic: overview
ms.openlocfilehash: a3a20c8ced3426399ceedf6994c872ce7aec93c3
ms.sourcegitcommit: e3d42e1f2920ec9cb002634b542bc20754f9544e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2021
ms.locfileid: "104823225"
---
# <a name="overview-of-azure-rtos-filex"></a><span data-ttu-id="b420b-105">Panoramica di Azure RTO FileX</span><span class="sxs-lookup"><span data-stu-id="b420b-105">Overview of Azure RTOS FileX</span></span>

<span data-ttu-id="b420b-106">Azure RTO FileX Embedded file system è la soluzione avanzata e di livello industriale di Azure RTO per i formati di file FAT Microsoft, progettata in modo specifico per applicazioni incorporate, in tempo reale e Internet.</span><span class="sxs-lookup"><span data-stu-id="b420b-106">Azure RTOS FileX embedded file system is Azure RTOS's advanced, industrial grade solution for Microsoft FAT file formats, designed specifically for deeply embedded, real-time, and IoT applications.</span></span> <span data-ttu-id="b420b-107">Azure RTO FileX supporta tutti i formati di file Microsoft, tra cui FAT12, FAT16, FAT32 e exFAT.</span><span class="sxs-lookup"><span data-stu-id="b420b-107">Azure RTOS FileX supports all of Microsoft’s file formats, including FAT12, FAT16, FAT32, and exFAT.</span></span> <span data-ttu-id="b420b-108">FileX offre anche la tolleranza di errore facoltativa e il livellamento dell'utilizzo FLASH tramite un prodotto aggiuntivo denominato [Azure RTO LevelX](https://docs.microsoft.com/azure/rtos/levelx/).</span><span class="sxs-lookup"><span data-stu-id="b420b-108">FileX also offers optional fault tolerance and FLASH wear leveling via an add-on product called [Azure RTOS LevelX](https://docs.microsoft.com/azure/rtos/levelx/).</span></span> <span data-ttu-id="b420b-109">Tutti questi componenti combinati con un footprint ridotto, un'esecuzione rapida e una maggiore semplicità d'uso, rendono Azure RTO FileX la scelta ideale per le applicazioni per le cose incorporate più complesse.</span><span class="sxs-lookup"><span data-stu-id="b420b-109">All of this combined with a small footprint, fast execution, and superior ease-of-use, make Azure RTOS FileX the ideal choice for the most demanding embedded IoT applications.</span></span>

## <a name="api-protocols"></a><span data-ttu-id="b420b-110">Protocolli API</span><span class="sxs-lookup"><span data-stu-id="b420b-110">API protocols</span></span>

### <a name="azure-rtos-filex-api"></a><span data-ttu-id="b420b-111">API FileX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="b420b-111">Azure RTOS FileX API</span></span>

- <span data-ttu-id="b420b-112">API intuitiva e coerente</span><span class="sxs-lookup"><span data-stu-id="b420b-112">Intuitive and consistent API</span></span>
- <span data-ttu-id="b420b-113">Sostantivo-convenzione di denominazione dei verbi</span><span class="sxs-lookup"><span data-stu-id="b420b-113">Noun-verb naming convention</span></span>
- <span data-ttu-id="b420b-114">Tutte le API hanno *fx_* iniziali per identificare facilmente come FILEX</span><span class="sxs-lookup"><span data-stu-id="b420b-114">All APIs have leading *fx_* to easily identify as FileX</span></span>
- <span data-ttu-id="b420b-115">Le API di blocco hanno un timeout thread facoltativo</span><span class="sxs-lookup"><span data-stu-id="b420b-115">Blocking APIs have optional thread timeout</span></span>
- <span data-ttu-id="b420b-116">Callback facoltativi delle notifiche utente per le operazioni su file e file multimediali</span><span class="sxs-lookup"><span data-stu-id="b420b-116">Optional user-notification callbacks for media and file operations</span></span>
- <span data-ttu-id="b420b-117">Per altri dettagli, vedere la [Guida dell'utente di Azure RTO FILEX](about-this-guide.md)</span><span class="sxs-lookup"><span data-stu-id="b420b-117">Please see [Azure RTOS FileX User Guide](about-this-guide.md) for more details</span></span>

### <a name="media-services"></a><span data-ttu-id="b420b-118">Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="b420b-118">Media Services</span></span>

- <span data-ttu-id="b420b-119">Supporto FAT 12/16/32 e exFAT</span><span class="sxs-lookup"><span data-stu-id="b420b-119">FAT 12/16/32 and exFAT support</span></span>
- <span data-ttu-id="b420b-120">FLASH 6KB minimo, 2,5 KB di RAM</span><span class="sxs-lookup"><span data-stu-id="b420b-120">Minimal 6KB FLASH, 2.5KB RAM</span></span>
- <span data-ttu-id="b420b-121">Servizi di accesso multimediale completi</span><span class="sxs-lookup"><span data-stu-id="b420b-121">Complete media access services</span></span>
- <span data-ttu-id="b420b-122">Numero illimitato di istanze dei supporti</span><span class="sxs-lookup"><span data-stu-id="b420b-122">Unlimited number of media instance</span></span>
- <span data-ttu-id="b420b-123">Interfaccia semplice di driver di settore logico in lettura/scrittura</span><span class="sxs-lookup"><span data-stu-id="b420b-123">Simple read/write logical sector driver interface</span></span>
- <span data-ttu-id="b420b-124">Supporto per più partizioni</span><span class="sxs-lookup"><span data-stu-id="b420b-124">Multiple partition support</span></span>
- <span data-ttu-id="b420b-125">Cache del settore logico</span><span class="sxs-lookup"><span data-stu-id="b420b-125">Logical sector cache</span></span>
- <span data-ttu-id="b420b-126">Cache di immissione FAT</span><span class="sxs-lookup"><span data-stu-id="b420b-126">FAT entry cache</span></span>
- <span data-ttu-id="b420b-127">Supporto della tolleranza di errore facoltativa</span><span class="sxs-lookup"><span data-stu-id="b420b-127">Optional fault tolerance support</span></span>
- <span data-ttu-id="b420b-128">Aggiornamento FAT secondario posticipato</span><span class="sxs-lookup"><span data-stu-id="b420b-128">Deferred Secondary FAT update</span></span>
- <span data-ttu-id="b420b-129">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="b420b-129">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="b420b-130">API di accesso multimediale intuitive, tra cui:</span><span class="sxs-lookup"><span data-stu-id="b420b-130">Intuitive media access APIs, including:</span></span>
  - <span data-ttu-id="b420b-131">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="b420b-131">fx_media_open</span></span>
  - <span data-ttu-id="b420b-132">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="b420b-132">fx_media_close</span></span>
  - <span data-ttu-id="b420b-133">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="b420b-133">fx_media_format</span></span>
  - <span data-ttu-id="b420b-134">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="b420b-134">fx_media_space_available</span></span>

### <a name="directory-services"></a><span data-ttu-id="b420b-135">Servizi directory</span><span class="sxs-lookup"><span data-stu-id="b420b-135">Directory Services</span></span>

- <span data-ttu-id="b420b-136">Fino a 256 di percorsi di byte</span><span class="sxs-lookup"><span data-stu-id="b420b-136">Up to 256 byte paths</span></span>
- <span data-ttu-id="b420b-137">Nomi di directory Long e 8,3 supportati</span><span class="sxs-lookup"><span data-stu-id="b420b-137">Long and 8.3 directory names supported</span></span>
- <span data-ttu-id="b420b-138">Creazione & eliminazione della directory</span><span class="sxs-lookup"><span data-stu-id="b420b-138">Directory create & delete</span></span>
- <span data-ttu-id="b420b-139">Esplorazione e attraversamento della directory</span><span class="sxs-lookup"><span data-stu-id="b420b-139">Directory navigation and traversal</span></span>
- <span data-ttu-id="b420b-140">Gestione degli attributi di directory</span><span class="sxs-lookup"><span data-stu-id="b420b-140">Directory attributes management</span></span>
- <span data-ttu-id="b420b-141">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="b420b-141">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="b420b-142">API di accesso alla directory intuitive, tra cui:</span><span class="sxs-lookup"><span data-stu-id="b420b-142">Intuitive directory access APIs, including:</span></span>
  - <span data-ttu-id="b420b-143">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="b420b-143">fx_directory_create</span></span>
  - <span data-ttu-id="b420b-144">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="b420b-144">fx_directory_delete</span></span>
  - <span data-ttu-id="b420b-145">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="b420b-145">fx_directory_attributes_set</span></span>
  - <span data-ttu-id="b420b-146">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="b420b-146">fx_directory_attributes_read</span></span>
  - <span data-ttu-id="b420b-147">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="b420b-147">fx_directory_first_entry_find</span></span>
  - <span data-ttu-id="b420b-148">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="b420b-148">fx_directory_next_entry_find</span></span>

### <a name="file-services"></a><span data-ttu-id="b420b-149">Servizi file</span><span class="sxs-lookup"><span data-stu-id="b420b-149">File Services</span></span>

- <span data-ttu-id="b420b-150">Minimo 3.3 KB di memoria FLASH</span><span class="sxs-lookup"><span data-stu-id="b420b-150">Minimal 3.3KB FLASH</span></span>
- <span data-ttu-id="b420b-151">File aperti illimitati</span><span class="sxs-lookup"><span data-stu-id="b420b-151">Unlimited open files</span></span>
- <span data-ttu-id="b420b-152">I file di sola lettura possono essere aperti più volte</span><span class="sxs-lookup"><span data-stu-id="b420b-152">Read-only files can be opened multiple times</span></span>
- <span data-ttu-id="b420b-153">Nomi di directory Long e 8,3 supportati</span><span class="sxs-lookup"><span data-stu-id="b420b-153">Long and 8.3 directory names supported</span></span>
- <span data-ttu-id="b420b-154">Supporto file contiguo</span><span class="sxs-lookup"><span data-stu-id="b420b-154">Contiguous file support</span></span>
- <span data-ttu-id="b420b-155">Logica di ricerca veloce</span><span class="sxs-lookup"><span data-stu-id="b420b-155">Fast seek logic</span></span>
- <span data-ttu-id="b420b-156">Pre-allocazione dei cluster</span><span class="sxs-lookup"><span data-stu-id="b420b-156">Pre-allocation of clusters</span></span>
- <span data-ttu-id="b420b-157">Creazione, eliminazione e ridenominazione di file</span><span class="sxs-lookup"><span data-stu-id="b420b-157">File create, delete, and rename</span></span>
- <span data-ttu-id="b420b-158">Lettura, scrittura e visualizzazione del file</span><span class="sxs-lookup"><span data-stu-id="b420b-158">File read, write, and see</span></span>
- <span data-ttu-id="b420b-159">Gestione degli attributi di file</span><span class="sxs-lookup"><span data-stu-id="b420b-159">File attributes management</span></span>
- <span data-ttu-id="b420b-160">Traccia a livello di sistema tramite Azure RTO TraceX</span><span class="sxs-lookup"><span data-stu-id="b420b-160">System-level Trace via Azure RTOS TraceX</span></span>
- <span data-ttu-id="b420b-161">API di accesso ai file intuitive, tra cui:</span><span class="sxs-lookup"><span data-stu-id="b420b-161">Intuitive file access APIs, including:</span></span>
  - <span data-ttu-id="b420b-162">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="b420b-162">fx_file_create</span></span>
  - <span data-ttu-id="b420b-163">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="b420b-163">fx_file_delete</span></span>
  - <span data-ttu-id="b420b-164">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="b420b-164">fx_file_attributes_set</span></span>
  - <span data-ttu-id="b420b-165">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="b420b-165">fx_file_attributes_read</span></span>
  - <span data-ttu-id="b420b-166">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="b420b-166">fx_file_read</span></span>
  - <span data-ttu-id="b420b-167">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="b420b-167">fx_file_seek</span></span>
  - <span data-ttu-id="b420b-168">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="b420b-168">fx_file_write</span></span>

## <a name="small-footprint"></a><span data-ttu-id="b420b-169">Footprint ridotto</span><span class="sxs-lookup"><span data-stu-id="b420b-169">Small-footprint</span></span>

<span data-ttu-id="b420b-170">Azure RTO FileX Embedded file system dispone di un footprint minimo ristretto di 8,6 KB a 12 KB per il supporto di base per i file di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="b420b-170">Azure RTOS FileX embedded file system has a remarkably small minimal footprint of 8.6 KB to 12 KB for basic file read/write support.</span></span> <span data-ttu-id="b420b-171">L'utilizzo minimo della RAM FileX di Azure RTO è nell'ordine di 1,8 KB per un'istanza del supporto e solo con una cache di settore logica a 512 byte.</span><span class="sxs-lookup"><span data-stu-id="b420b-171">Minimal Azure RTOS FileX RAM usage is on the order of 1.8 KB for one media instance and with only a 512-byte logical sector cache.</span></span> <span data-ttu-id="b420b-172">Come Azure RTO ThreadX, le dimensioni di Azure RTO FileX vengono ridimensionate automaticamente in base ai servizi usati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b420b-172">Like Azure RTOS ThreadX, the size of Azure RTOS FileX automatically scales based on the services used by the application.</span></span> <span data-ttu-id="b420b-173">In questo modo si elimina la necessità di una configurazione complicata e dei parametri di compilazione, semplificando le operazioni per lo sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="b420b-173">This virtually eliminates the need for complicated configuration and builds parameters, making things easier for the developer.</span></span>

## <a name="fast-execution"></a><span data-ttu-id="b420b-174">Esecuzione rapida</span><span class="sxs-lookup"><span data-stu-id="b420b-174">Fast execution</span></span>

<span data-ttu-id="b420b-175">Azure RTO FileX offre una cache di settore logica e una cache di immissione FAT.</span><span class="sxs-lookup"><span data-stu-id="b420b-175">Azure RTOS FileX provides a logical sector cache as well as a FAT entry cache.</span></span> <span data-ttu-id="b420b-176">Le dimensioni di entrambi sono sotto il controllo diretto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b420b-176">The sizes of both are under direct control of the application.</span></span> <span data-ttu-id="b420b-177">Azure RTO FileX offre inoltre un'allocazione del cluster contigua e una lettura e scrittura diretta del cluster consecutivi.</span><span class="sxs-lookup"><span data-stu-id="b420b-177">In addition, Azure RTOS FileX provides contiguous cluster allocation and direct consecutive cluster reading and writing.</span></span> <span data-ttu-id="b420b-178">Le richieste di lettura/scrittura di interi settori vengono eseguite direttamente tra il buffer dell'applicazione e il supporto, ovvero non viene eseguito alcun buffer intermedio.</span><span class="sxs-lookup"><span data-stu-id="b420b-178">Read/write requests of whole sectors are done directly between the application buffer and the media – that is, no intermediate buffering is done.</span></span> <span data-ttu-id="b420b-179">Questa e una filosofia di progettazione orientata alle prestazioni generale consentono ad Azure RTO FileX di ottenere le prestazioni più veloci possibile.</span><span class="sxs-lookup"><span data-stu-id="b420b-179">All of this and a general performance-oriented design philosophy helps Azure RTOS FileX achieve the fastest possible performance.</span></span>

## <a name="advanced-technology"></a><span data-ttu-id="b420b-180">Tecnologia avanzata</span><span class="sxs-lookup"><span data-stu-id="b420b-180">Advanced technology</span></span>

<span data-ttu-id="b420b-181">Azure RTO FileX è una tecnologia avanzata, incluse le seguenti.</span><span class="sxs-lookup"><span data-stu-id="b420b-181">Azure RTOS FileX is advanced technology, including the following.</span></span>

- <span data-ttu-id="b420b-182">Supporto FAT 12/16/32 e exFAT</span><span class="sxs-lookup"><span data-stu-id="b420b-182">FAT 12/16/32 and exFAT support</span></span>
- <span data-ttu-id="b420b-183">Supporto per più partizioni</span><span class="sxs-lookup"><span data-stu-id="b420b-183">Multiple partition support</span></span>
- <span data-ttu-id="b420b-184">Scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="b420b-184">Automatic scaling</span></span>
- <span data-ttu-id="b420b-185">Endian neutro</span><span class="sxs-lookup"><span data-stu-id="b420b-185">Endian neutral</span></span>
- <span data-ttu-id="b420b-186">Nome di file lungo e supporto di 8,3</span><span class="sxs-lookup"><span data-stu-id="b420b-186">Long file name and 8.3 support</span></span>
- <span data-ttu-id="b420b-187">Supporto della tolleranza di errore facoltativa</span><span class="sxs-lookup"><span data-stu-id="b420b-187">Optional fault tolerance support</span></span>
- <span data-ttu-id="b420b-188">Cache del settore logico</span><span class="sxs-lookup"><span data-stu-id="b420b-188">Logical sector cache</span></span>
- <span data-ttu-id="b420b-189">Cache di immissione FAT</span><span class="sxs-lookup"><span data-stu-id="b420b-189">FAT entry cache</span></span>
- <span data-ttu-id="b420b-190">Pre-allocazione dei cluster</span><span class="sxs-lookup"><span data-stu-id="b420b-190">Pre-allocation of clusters</span></span>
- <span data-ttu-id="b420b-191">Supporto file contiguo</span><span class="sxs-lookup"><span data-stu-id="b420b-191">Contiguous file support</span></span>
- <span data-ttu-id="b420b-192">Metriche delle prestazioni facoltative</span><span class="sxs-lookup"><span data-stu-id="b420b-192">Optional performance metrics</span></span>
- <span data-ttu-id="b420b-193">Supporto per l'analisi del sistema TraceX di Azure RTO</span><span class="sxs-lookup"><span data-stu-id="b420b-193">Azure RTOS TraceX system analysis support</span></span>

## <a name="nornand-wear-leveling-azure-rtos-levelx"></a><span data-ttu-id="b420b-194">Livelli di utilizzo non/NAND (Azure RTO LevelX)</span><span class="sxs-lookup"><span data-stu-id="b420b-194">NOR/NAND Wear Leveling (Azure RTOS LevelX)</span></span>

<span data-ttu-id="b420b-195">Azure RTO LevelX è il prodotto Microsoft NOR/NAND FLASH Wear Leveling.</span><span class="sxs-lookup"><span data-stu-id="b420b-195">Azure RTOS LevelX is Microsoft’s NOR/NAND FLASH wear leveling product.</span></span> <span data-ttu-id="b420b-196">Azure RTO LevelX può essere usato insieme a FileX o come libreria di settore FLASH autonomo di lettura/scrittura diretta per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b420b-196">Azure RTOS LevelX can be used in conjunction with FileX or as a stand-alone, direct read/write FLASH sector library for the application.</span></span>

## <a name="fastest-time-to-market"></a><span data-ttu-id="b420b-197">Time-to-market più veloce</span><span class="sxs-lookup"><span data-stu-id="b420b-197">Fastest time-to-market</span></span>

<span data-ttu-id="b420b-198">Azure RTO FileX è facile da installare, apprendere, usare, eseguire il debug, verificare, certificare e gestire.</span><span class="sxs-lookup"><span data-stu-id="b420b-198">Azure RTOS FileX is easy to install, learn, use, debug, verify, certify, and maintain.</span></span> <span data-ttu-id="b420b-199">Di conseguenza, Azure RTO FileX è uno dei file system FAT più diffusi per i dispositivi di Internet delle cose embedded.</span><span class="sxs-lookup"><span data-stu-id="b420b-199">As a result, Azure RTOS FileX is one of the most popular FAT file systems for embedded IoT devices.</span></span> <span data-ttu-id="b420b-200">Di seguito sono riportati alcuni motivi per un vantaggio di time-to-Market coerente:</span><span class="sxs-lookup"><span data-stu-id="b420b-200">The following are some reasons for our consistent time-to-market advantage:</span></span>

- <span data-ttu-id="b420b-201">Documentazione sulla qualità: esaminare la [Guida dell'utente di Azure RTO FILEX](about-this-guide.md) e vedere per se stessi.</span><span class="sxs-lookup"><span data-stu-id="b420b-201">Quality Documentation – please review our [Azure RTOS FileX User Guide](about-this-guide.md) and see for yourself!</span></span>
- <span data-ttu-id="b420b-202">Disponibilità del codice sorgente completa</span><span class="sxs-lookup"><span data-stu-id="b420b-202">Complete Source Code Availability</span></span>
- <span data-ttu-id="b420b-203">API di facile utilizzo</span><span class="sxs-lookup"><span data-stu-id="b420b-203">Easy-to-use API</span></span>
- <span data-ttu-id="b420b-204">Set di funzionalità completo e avanzato</span><span class="sxs-lookup"><span data-stu-id="b420b-204">Comprehensive and Advanced Feature Set</span></span>

## <a name="pre-certified--by-tuv-and-ul-to-many-safety-standards"></a><span data-ttu-id="b420b-205">Pre-certificati da TUV e UL a molti standard di sicurezza</span><span class="sxs-lookup"><span data-stu-id="b420b-205">Pre-certified  by TUV and UL to many safety standards</span></span>

![SGS-TUV Saar](./media/overview-filex/partener-logo-sgs-tuv-saar-2.png)

<span data-ttu-id="b420b-207">Azure RTO FileX è stato certificato da SGS-TUV Saar per l'uso nei sistemi critici per la sicurezza, secondo IEC-61508 SIL 4, IEC-62304 SW Safety Class C, ISO 26262 ASIL D e EN 50128.</span><span class="sxs-lookup"><span data-stu-id="b420b-207">Azure RTOS FileX has been certified by SGS-TUV Saar for use in safety-critical systems, according to IEC-61508 SIL 4, IEC-62304  SW Safety Class C, ISO 26262 ASIL D and EN 50128.</span></span> <span data-ttu-id="b420b-208">La certificazione conferma che FileX può essere usato nello sviluppo di software correlato alla sicurezza per i livelli di integrità di sicurezza più elevati di IEC-61508, IEC-62304, ISO 26262 e EN 50128 per la "protezione funzionale dei sistemi elettronici, elettrici e programmabili relativi alla sicurezza elettronica."</span><span class="sxs-lookup"><span data-stu-id="b420b-208">The certification confirms that FileX can be used in the development of safety-related software for the highest safety integrity levels of IEC-61508, IEC-62304, ISO 26262 and EN 50128 for the “Functional Safety of electrical, electronic, and programmable electronic safety-related systems.”</span></span> <span data-ttu-id="b420b-209">SGS-TUV Saar, costituito da una joint venture del SGS-Group e del TUV del Regno Unito, è diventato la società leader accreditata e indipendente per il test, il controllo, la verifica e la certificazione del software incorporato per i sistemi correlati alla sicurezza in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="b420b-209">SGS-TUV Saar, formed through a joint venture of Germany’s SGS-Group and TUV Saarland, has become the leading accredited, independent company for testing, auditing, verifying, and certifying embedded software for safety-related systems worldwide.</span></span> <span data-ttu-id="b420b-210">Lo standard di sicurezza industriale IEC 61508 e tutti gli standard derivati da esso, tra cui IEC-62304, ISO 26262 e EN 50128, vengono usati per garantire la protezione funzionale di dispositivi medicali elettrici, elettronici e programmabili per la sicurezza elettronica, sistemi di controllo dei processi, macchinari industriali, automobili e sistemi di controllo ferroviari.</span><span class="sxs-lookup"><span data-stu-id="b420b-210">The industrial safety standard IEC 61508, and all standards that are derived from it, including IEC-62304, ISO 26262 and EN 50128, are used to assure the functional safety of electrical, electronic, and programmable electronic safety-related medical devices, process control systems, industrial machinery, automobiles, and railway control systems.</span></span>

:::image type="content" source="media/overview-filex/cru-logo-certification.png" alt-text="Certificazione CRU UL":::

<span data-ttu-id="b420b-212">Azure RTO FileX è stato riconosciuto da UL per conformità con UL 60730-1 allegato H, CSA E60730-1 allegato H, IEC 60730-1 allegato H, UL 60335-1 allegato R, IEC 60335-1 allegato R e UL 1998 sicurezza standard per il software in componenti programmabili.</span><span class="sxs-lookup"><span data-stu-id="b420b-212">Azure RTOS FileX has been recognized by UL for compliance with UL 60730-1 Annex H, CSA E60730-1 Annex H, IEC 60730-1 Annex H, UL 60335-1 Annex R, IEC 60335-1 Annex R, and UL 1998 safety standards for software in programmable components.</span></span> <span data-ttu-id="b420b-213">UL è una società globale, indipendente e scientifica per la sicurezza, con più di un secolo di competenze innovative per l'innovazione delle soluzioni di sicurezza, che vanno dall'adozione pubblica di energia elettrica ai progressi della sostenibilità, dell'energia rinnovabile e della nanotecnologia.</span><span class="sxs-lookup"><span data-stu-id="b420b-213">UL is a global, independent, safety-science company with more than a century of expertise innovating safety solutions, ranging from the public adoption of electricity to breakthroughs in sustainability, renewable energy, and nanotechnology.</span></span>

<span data-ttu-id="b420b-214">Gli artefatti (certificato, manuale di sicurezza, report di test e così via) associati alle certificazioni TUV e UL sono disponibili per la vendita.</span><span class="sxs-lookup"><span data-stu-id="b420b-214">Artifacts (Certificate, Safety Manual, Test Report, etc.) associated with the TUV and UL certifications are available for sale.</span></span>

<span data-ttu-id="b420b-215">Nei casi in cui l'applicazione necessita di ulteriore certificazione, un servizio di certificazione è disponibile tramite Microsoft per fornire la certificazione chiavi in volta a diversi standard usando la piattaforma hardware effettiva e persino coprendo il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b420b-215">In cases where the application needs additional certification, a certification service is available through Microsoft for providing turn-key certification to various standards using the actual hardware platform and even covering the application code.</span></span>

## <a name="one-simple-license"></a><span data-ttu-id="b420b-216">Una licenza semplice</span><span class="sxs-lookup"><span data-stu-id="b420b-216">One Simple License</span></span>

<span data-ttu-id="b420b-217">Non è previsto alcun costo per l'uso e il test del codice sorgente e nessun costo per le licenze di produzione quando viene distribuito in dispositivi con licenza preliminare, tutti gli altri dispositivi necessitano di una licenza annuale semplice.</span><span class="sxs-lookup"><span data-stu-id="b420b-217">There is no cost to use and test the source code and no cost for production licenses when deployed to pre-licensed devices, all other devices need a simple annual license.</span></span>

## <a name="full-highest-quality-source-code"></a><span data-ttu-id="b420b-218">Codice sorgente completo di qualità elevata</span><span class="sxs-lookup"><span data-stu-id="b420b-218">Full, highest-quality source code</span></span>

<span data-ttu-id="b420b-219">Nel corso degli anni, il codice sorgente di FileX ha impostato la qualità e la facilità di comprensione.</span><span class="sxs-lookup"><span data-stu-id="b420b-219">Throughout the years, FileX source code has set the bar in quality and ease of understanding.</span></span> <span data-ttu-id="b420b-220">Inoltre, la convenzione relativa alla presenza di una funzione per ogni file fornisce una semplice navigazione all'origine.</span><span class="sxs-lookup"><span data-stu-id="b420b-220">In addition, the convention of having one function per file provides for easy source navigation.</span></span>

## <a name="supports-most-popular-architectures"></a><span data-ttu-id="b420b-221">Supporta le architetture più diffuse</span><span class="sxs-lookup"><span data-stu-id="b420b-221">Supports most popular architectures</span></span>

<span data-ttu-id="b420b-222">Azure RTO FileX viene eseguito sui microprocessori più diffusi a 32/64 bit, predefiniti, completamente testati e completamente supportati, inclusi i seguenti:</span><span class="sxs-lookup"><span data-stu-id="b420b-222">Azure RTOS FileX runs on most popular 32/64-bit microprocessors, out-of-the-box, fully tested and fully supported, including the following:</span></span>

<span data-ttu-id="b420b-223">**Dispositivi analoghi**: SHARC, Blackfin, CM4xx</span><span class="sxs-lookup"><span data-stu-id="b420b-223">**Analog Devices**: SHARC, Blackfin, CM4xx</span></span>

<span data-ttu-id="b420b-224">**Andina Core**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="b420b-224">**Andes Core**: RISC-V</span></span>

<span data-ttu-id="b420b-225">**Ambiqmicro**: Apollo MCU</span><span class="sxs-lookup"><span data-stu-id="b420b-225">**Ambiqmicro**: Apollo MCUs</span></span>

<span data-ttu-id="b420b-226">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/a15/a5/A7/A8/A9/A5x 64-bi/A7X a 64 bit/R4/R5, TrustZone ARMv8-M</span><span class="sxs-lookup"><span data-stu-id="b420b-226">**ARM**: ARM7, ARM9, ARM11, Cortex-M0/M3/M4/M7/A15/A5/A7/A8/A9/A5x 64-bi/A7x 64-bit/R4/R5, TrustZone ARMv8-M</span></span>

<span data-ttu-id="b420b-227">**Cadenza**: Xtensa, diamante</span><span class="sxs-lookup"><span data-stu-id="b420b-227">**Cadence**: Xtensa, Diamond</span></span>

<span data-ttu-id="b420b-228">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0 +, FM3, MF4, WICED WiFi</span><span class="sxs-lookup"><span data-stu-id="b420b-228">**CEVA**: PSoC, PSoC 4, PSoC 5, PSoC 6, FM0+, FM3, MF4, WICED WiFi</span></span>

<span data-ttu-id="b420b-229">**Cypress**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="b420b-229">**Cypress**: RISC-V</span></span>

<span data-ttu-id="b420b-230">**Silice**: ESI-RISC</span><span class="sxs-lookup"><span data-stu-id="b420b-230">**EnSilica**: eSi-RISC</span></span>

<span data-ttu-id="b420b-231">**Infineon**: XMC1000, XMC4000, Tricore</span><span class="sxs-lookup"><span data-stu-id="b420b-231">**Infineon**: XMC1000, XMC4000, TriCore</span></span>

<span data-ttu-id="b420b-232">**Intel**; **Intel FPGA**: x36/Pentium, XScale, Nios II, Cyclone, Arria 10</span><span class="sxs-lookup"><span data-stu-id="b420b-232">**Intel**; **Intel FPGA**: x36/Pentium, XScale, NIOS II, Cyclone, Arria 10</span></span>

<span data-ttu-id="b420b-233">**Microchip**: avr32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span><span class="sxs-lookup"><span data-stu-id="b420b-233">**Microchip**: AVR32, ARM7, ARM9, Cortex-M3/M4/M7, SAM3/4/7/9/A/C/D/E/G/L/SV, PIC24/PIC32</span></span>

<span data-ttu-id="b420b-234">**Microsemi**: RISC-V</span><span class="sxs-lookup"><span data-stu-id="b420b-234">**Microsemi**: RISC-V</span></span>

<span data-ttu-id="b420b-235">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, I.MX, ColdFire, Kinetis Cortex-M3/M4</span><span class="sxs-lookup"><span data-stu-id="b420b-235">**NXP**: LPC, ARM7, ARM9, PowerPC, 68 K, i.MX, ColdFire, Kinetis Cortex-M3/M4</span></span>

<span data-ttu-id="b420b-236">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span><span class="sxs-lookup"><span data-stu-id="b420b-236">**Renesas**: SH, HS, V850, RX, RZ, Synergy</span></span>

<span data-ttu-id="b420b-237">**Silicone** Lab: EFM32</span><span class="sxs-lookup"><span data-stu-id="b420b-237">**Silicon** Labs: EFM32</span></span>

<span data-ttu-id="b420b-238">**Synopsys**: Arc 600, 700, Arc em, Arc HS</span><span class="sxs-lookup"><span data-stu-id="b420b-238">**Synopsys**: ARC 600, 700, ARC EM, ARC HS</span></span>

<span data-ttu-id="b420b-239">**St**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span><span class="sxs-lookup"><span data-stu-id="b420b-239">**ST**: STM32, ARM7, ARM9, Cortex-M3/M4/M7</span></span>

<span data-ttu-id="b420b-240">**TL**: C5xxx, C6xxx, Stellaris, Sitara, tiva-C</span><span class="sxs-lookup"><span data-stu-id="b420b-240">**Tl**: C5xxx, C6xxx, Stellaris, Sitara, Tiva-C</span></span>

<span data-ttu-id="b420b-241">**Elaborazione Wave**: MIPS32 4K, 24 k, 34 k, 1004 k, MIPS64 5K, MicroAptiv, InterAptiv, ProAptiv, M-Class</span><span class="sxs-lookup"><span data-stu-id="b420b-241">**Wave Computing**: MIPS32 4K, 24 K, 34 K, 1004 K, MIPS64 5K, microAptiv, interAptiv, proAptiv, M-Class</span></span>

<span data-ttu-id="b420b-242">**Xilinx**: Microblaze, PowerPC 405, ZYNQ, Zynq UltraSCALE</span><span class="sxs-lookup"><span data-stu-id="b420b-242">**Xilinx**: MicroBlaze, PowerPC 405, ZYNQ, ZYNQ UltraSCALE</span></span>

<span data-ttu-id="b420b-243">*Tutte le cifre relative a tempistiche e dimensioni elencate sono stime e possono essere diverse nella piattaforma di sviluppo.*</span><span class="sxs-lookup"><span data-stu-id="b420b-243">*All timing and size figures listed are estimates and may be different on your development platform.*</span></span>
