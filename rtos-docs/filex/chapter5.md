---
title: Capitolo 5-driver I/O per Azure RTO FileX
description: Questo capitolo contiene una descrizione dei driver I/O per Azure RTO FileX ed è progettato per consentire agli sviluppatori di scrivere driver specifici dell'applicazione.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: 8f2ef697f68a269b24a34147a4bc076b8a2b1660
ms.sourcegitcommit: 60ad844b58639d88830f2660ab0c4ff86b92c10f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2021
ms.locfileid: "106550083"
---
# <a name="chapter-5---io-drivers-for-azure-rtos-filex"></a><span data-ttu-id="0183b-103">Capitolo 5-driver I/O per Azure RTO FileX</span><span class="sxs-lookup"><span data-stu-id="0183b-103">Chapter 5 - I/O Drivers for Azure RTOS FileX</span></span>

<span data-ttu-id="0183b-104">Questo capitolo contiene una descrizione dei driver I/O per Azure RTO FileX ed è progettato per consentire agli sviluppatori di scrivere driver specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0183b-104">This chapter contains a description of I/O drivers for Azure RTOS FileX and is designed to help developers write application-specific drivers.</span></span>

## <a name="io-driver-introduction"></a><span data-ttu-id="0183b-105">Introduzione al driver I/O</span><span class="sxs-lookup"><span data-stu-id="0183b-105">I/O Driver Introduction</span></span>

<span data-ttu-id="0183b-106">FileX supporta più dispositivi multimediali.</span><span class="sxs-lookup"><span data-stu-id="0183b-106">FileX supports multiple media devices.</span></span> <span data-ttu-id="0183b-107">La struttura FX_MEDIA definisce tutti gli elementi necessari per la gestione di un dispositivo multimediale.</span><span class="sxs-lookup"><span data-stu-id="0183b-107">The FX_MEDIA structure defines everything required to manage a media device.</span></span> <span data-ttu-id="0183b-108">Questa struttura contiene tutte le informazioni multimediali, inclusi i driver i/O specifici del supporto e i parametri associati per il passaggio di informazioni e stato tra il driver e FileX.</span><span class="sxs-lookup"><span data-stu-id="0183b-108">This structure contains all media information, including the media-specific I/O driver and associated parameters for passing information and status between the driver and FileX.</span></span> <span data-ttu-id="0183b-109">Nella maggior parte dei sistemi è presente un driver di I/O univoco per ogni istanza del supporto FileX.</span><span class="sxs-lookup"><span data-stu-id="0183b-109">In most systems, there is a unique I/O driver for each FileX media instance.</span></span>

## <a name="io-driver-entry"></a><span data-ttu-id="0183b-110">Voce driver I/O</span><span class="sxs-lookup"><span data-stu-id="0183b-110">I/O Driver Entry</span></span>

<span data-ttu-id="0183b-111">Ogni driver di I/O FileX dispone di una singola funzione entry definita dalla chiamata al servizio ***fx_media_open*** .</span><span class="sxs-lookup"><span data-stu-id="0183b-111">Each FileX I/O driver has a single entry function that is defined by the ***fx_media_open*** service call.</span></span> <span data-ttu-id="0183b-112">La funzione entry driver ha il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="0183b-112">The driver entry function has the following format:</span></span>

```c
void my_driver_entry(FX_MEDIA *media_ptr);
```

<span data-ttu-id="0183b-113">FileX chiama la funzione entry driver I/O per richiedere l'accesso a tutti i supporti fisici, inclusa l'inizializzazione e la lettura del settore di avvio.</span><span class="sxs-lookup"><span data-stu-id="0183b-113">FileX calls the I/O driver entry function to request all physical media access, including initialization and boot sector reading.</span></span> <span data-ttu-id="0183b-114">Le richieste effettuate al driver vengono eseguite in sequenza; ad esempio, FileX attende il completamento della richiesta corrente prima che venga inviata un'altra richiesta.</span><span class="sxs-lookup"><span data-stu-id="0183b-114">Requests made to the driver are done sequentially; i.e., FileX waits for the current request to complete before another request is sent.</span></span>

## <a name="io-driver-requests"></a><span data-ttu-id="0183b-115">Richieste driver I/O</span><span class="sxs-lookup"><span data-stu-id="0183b-115">I/O Driver Requests</span></span>

<span data-ttu-id="0183b-116">Poiché ogni driver di I/O ha una singola funzione entry, FileX esegue richieste specifiche tramite il blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="0183b-116">Because each I/O driver has a single entry function, FileX makes specific requests through the media control block.</span></span> <span data-ttu-id="0183b-117">In particolare, il membro  **fx_media_driver_request** di **FX_MEDIA** viene usato per specificare la richiesta di driver esatta.</span><span class="sxs-lookup"><span data-stu-id="0183b-117">Specifically, the  **fx_media_driver_request** member of **FX_MEDIA** is used to specify the exact driver request.</span></span> <span data-ttu-id="0183b-118">Il driver di I/O comunica l'esito positivo o negativo della richiesta tramite il membro **fx_media_driver_status** di **FX_MEDIA**.</span><span class="sxs-lookup"><span data-stu-id="0183b-118">The I/O driver communicates the success or failure of the request through the **fx_media_driver_status** member of **FX_MEDIA**.</span></span> <span data-ttu-id="0183b-119">Se la richiesta del driver ha avuto esito positivo, **FX_SUCCESS** viene inserita in questo campo prima che il driver venga restituito.</span><span class="sxs-lookup"><span data-stu-id="0183b-119">If the driver request was successful, **FX_SUCCESS** is placed in this field before the driver returns.</span></span> <span data-ttu-id="0183b-120">In caso contrario, se viene rilevato un errore, FX_IO_ERROR viene inserito in questo campo.</span><span class="sxs-lookup"><span data-stu-id="0183b-120">Otherwise, if an error is detected, FX_IO_ERROR is placed in this field.</span></span>

### <a name="driver-initialization"></a><span data-ttu-id="0183b-121">Inizializzazione driver</span><span class="sxs-lookup"><span data-stu-id="0183b-121">Driver Initialization</span></span>

<span data-ttu-id="0183b-122">Sebbene l'effettivo processo di inizializzazione dei driver sia specifico dell'applicazione, in genere è costituito dall'inizializzazione della struttura dei dati e possibilmente da un'inizializzazione preliminare</span><span class="sxs-lookup"><span data-stu-id="0183b-122">Although the actual driver initialization processing is application specific, it usually consists of data structure initialization and possibly some preliminary hardware initialization.</span></span> <span data-ttu-id="0183b-123">Questa richiesta è la prima eseguita da FileX e viene eseguita dall'interno del servizio fx_media_open.</span><span class="sxs-lookup"><span data-stu-id="0183b-123">This request is the first made by FileX and is done from within the fx_media_open service.</span></span>

<span data-ttu-id="0183b-124">Se viene rilevata la protezione da scrittura media, il fx_media_driver_write_protect membro del FX_MEDIA deve essere impostato su FX_TRUE.</span><span class="sxs-lookup"><span data-stu-id="0183b-124">If media write protection is detected, the driver fx_media_driver_write_protect member of FX_MEDIA should be set to FX_TRUE.</span></span>

<span data-ttu-id="0183b-125">Per la richiesta di inizializzazione del driver I/O vengono utilizzati i membri FX_MEDIA seguenti:</span><span class="sxs-lookup"><span data-stu-id="0183b-125">The following FX_MEDIA members are used for the I/O driver initialization request:</span></span>

|<span data-ttu-id="0183b-126">Membro FX_MEDIA</span><span class="sxs-lookup"><span data-stu-id="0183b-126">FX_MEDIA member</span></span>|<span data-ttu-id="0183b-127">Significato</span><span class="sxs-lookup"><span data-stu-id="0183b-127">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="0183b-128">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="0183b-128">fx_media_driver_request</span></span>|<span data-ttu-id="0183b-129">FX_DRIVER_INIT</span><span class="sxs-lookup"><span data-stu-id="0183b-129">FX_DRIVER_INIT</span></span>|

<span data-ttu-id="0183b-130">FileX fornisce un meccanismo per informare il driver dell'applicazione quando i settori non vengono più utilizzati.</span><span class="sxs-lookup"><span data-stu-id="0183b-130">FileX provides a mechanism to inform the application driver when sectors are no longer being used.</span></span> <span data-ttu-id="0183b-131">Questa operazione è particolarmente utile per i gestori di memoria FLASH che devono gestire tutti i settori logici in uso mappati al FLASH.</span><span class="sxs-lookup"><span data-stu-id="0183b-131">This is especially useful for FLASH memory managers that must manage all in-use logical sectors mapped to the FLASH.</span></span>

<span data-ttu-id="0183b-132">Se è necessaria una notifica di settori gratuiti, il driver dell'applicazione imposta semplicemente il campo *fx_media_driver_free_sector_update* nella struttura di **FX_MEDIA** associata a **FX_TRUE**.</span><span class="sxs-lookup"><span data-stu-id="0183b-132">If such notification of free sectors is required, the application driver simply sets the *fx_media_driver_free_sector_update* field in the associated **FX_MEDIA** structure to **FX_TRUE**.</span></span> <span data-ttu-id="0183b-133">Dopo l'impostazione, FileX esegue una chiamata al driver di I/O **_FX_DRIVER_RELEASE_SECTORS_** che indica quando uno o più settori consecutivi diventano disponibili.</span><span class="sxs-lookup"><span data-stu-id="0183b-133">After set, FileX makes a **_FX_DRIVER_RELEASE_SECTORS_** I/O driver call indicating when one or more consecutive sectors becomes free.</span></span>

### <a name="boot-sector-read"></a><span data-ttu-id="0183b-134">Lettura settore di avvio</span><span class="sxs-lookup"><span data-stu-id="0183b-134">Boot Sector Read</span></span>

<span data-ttu-id="0183b-135">Invece di usare una richiesta di lettura standard, FileX esegue una richiesta specifica per leggere il settore di avvio del supporto.</span><span class="sxs-lookup"><span data-stu-id="0183b-135">Instead of using a standard read request, FileX makes a specific request to read the media's boot sector.</span></span> <span data-ttu-id="0183b-136">Per la richiesta di lettura del settore di avvio del driver I/O vengono utilizzati i membri **FX_MEDIA** seguenti:</span><span class="sxs-lookup"><span data-stu-id="0183b-136">The following **FX_MEDIA** members are used for the I/O driver boot sector read request:</span></span>

|<span data-ttu-id="0183b-137">Membro FX_MEDIA</span><span class="sxs-lookup"><span data-stu-id="0183b-137">FX_MEDIA member</span></span>|<span data-ttu-id="0183b-138">Significato</span><span class="sxs-lookup"><span data-stu-id="0183b-138">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="0183b-139">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="0183b-139">fx_media_driver_request</span></span>| <span data-ttu-id="0183b-140">FX_DRIVER_BOOT_READ</span><span class="sxs-lookup"><span data-stu-id="0183b-140">FX_DRIVER_BOOT_READ</span></span>|
|<span data-ttu-id="0183b-141">fx_media_driver_buffer</span><span class="sxs-lookup"><span data-stu-id="0183b-141">fx_media_driver_buffer</span></span>| <span data-ttu-id="0183b-142">Indirizzo della destinazione per il settore di avvio.</span><span class="sxs-lookup"><span data-stu-id="0183b-142">Address of destination for boot sector.</span></span>|

### <a name="boot-sector-write"></a><span data-ttu-id="0183b-143">Scrittura settore di avvio</span><span class="sxs-lookup"><span data-stu-id="0183b-143">Boot Sector Write</span></span>

<span data-ttu-id="0183b-144">Invece di usare una richiesta di scrittura standard, FileX esegue una richiesta specifica per scrivere il settore di avvio del supporto.</span><span class="sxs-lookup"><span data-stu-id="0183b-144">Instead of using a standard write request, FileX makes a specific request to write the media's boot sector.</span></span> <span data-ttu-id="0183b-145">Per la richiesta di scrittura del settore di avvio del driver I/O vengono utilizzati i membri **FX_MEDIA** seguenti:</span><span class="sxs-lookup"><span data-stu-id="0183b-145">The following **FX_MEDIA** members are used for the I/O driver boot sector write request:</span></span>

|<span data-ttu-id="0183b-146">Membro FX_MEDIA</span><span class="sxs-lookup"><span data-stu-id="0183b-146">FX_MEDIA member</span></span>|<span data-ttu-id="0183b-147">Significato</span><span class="sxs-lookup"><span data-stu-id="0183b-147">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="0183b-148">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="0183b-148">fx_media_driver_request</span></span>| <span data-ttu-id="0183b-149">FX_DRIVER_BOOT_WRITE</span><span class="sxs-lookup"><span data-stu-id="0183b-149">FX_DRIVER_BOOT_WRITE</span></span>|
|<span data-ttu-id="0183b-150">fx_media_driver_buffer</span><span class="sxs-lookup"><span data-stu-id="0183b-150">fx_media_driver_buffer</span></span>| <span data-ttu-id="0183b-151">Indirizzo dell'origine per il settore di avvio.</span><span class="sxs-lookup"><span data-stu-id="0183b-151">Address of source for boot sector.</span></span>|

### <a name="sector-read"></a><span data-ttu-id="0183b-152">Lettura settore</span><span class="sxs-lookup"><span data-stu-id="0183b-152">Sector Read</span></span>

<span data-ttu-id="0183b-153">FileX legge uno o più settori nella memoria emettendo una richiesta di lettura al driver di I/O.</span><span class="sxs-lookup"><span data-stu-id="0183b-153">FileX reads one or more sectors into memory by issuing a read request to the I/O driver.</span></span> <span data-ttu-id="0183b-154">Per la richiesta di lettura del driver di I/O vengono usati i membri **FX_MEDIA** seguenti:</span><span class="sxs-lookup"><span data-stu-id="0183b-154">The following **FX_MEDIA** members are used for the I/O driver read request:</span></span>

|<span data-ttu-id="0183b-155">Membro FX_MEDIA</span><span class="sxs-lookup"><span data-stu-id="0183b-155">FX_MEDIA member</span></span>|<span data-ttu-id="0183b-156">Significato</span><span class="sxs-lookup"><span data-stu-id="0183b-156">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="0183b-157">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="0183b-157">fx_media_driver_request</span></span>| <span data-ttu-id="0183b-158">FX_DRIVER_READ</span><span class="sxs-lookup"><span data-stu-id="0183b-158">FX_DRIVER_READ</span></span>|
|<span data-ttu-id="0183b-159">fx_media_driver_logical_sector</span><span class="sxs-lookup"><span data-stu-id="0183b-159">fx_media_driver_logical_sector</span></span>|<span data-ttu-id="0183b-160">Settore logico da leggere</span><span class="sxs-lookup"><span data-stu-id="0183b-160">Logical sector to read</span></span>|
|<span data-ttu-id="0183b-161">fx_media_driver_sectors</span><span class="sxs-lookup"><span data-stu-id="0183b-161">fx_media_driver_sectors</span></span>|<span data-ttu-id="0183b-162">Numero di settori da leggere</span><span class="sxs-lookup"><span data-stu-id="0183b-162">Number of sectors to read</span></span>|
|<span data-ttu-id="0183b-163">fx_media_driver_buffer</span><span class="sxs-lookup"><span data-stu-id="0183b-163">fx_media_driver_buffer</span></span>|<span data-ttu-id="0183b-164">Buffer di destinazione per i settori letti</span><span class="sxs-lookup"><span data-stu-id="0183b-164">Destination buffer for sector(s) read</span></span>|
|<span data-ttu-id="0183b-165">fx_media_driver_data_sector_read</span><span class="sxs-lookup"><span data-stu-id="0183b-165">fx_media_driver_data_sector_read</span></span>|<span data-ttu-id="0183b-166">Impostare su FX_TRUE se viene richiesto un settore di dati di file.</span><span class="sxs-lookup"><span data-stu-id="0183b-166">Set to FX_TRUE if a file data sector is requested.</span></span> <span data-ttu-id="0183b-167">In caso contrario, FX_FALSE se viene richiesto un settore di sistema (FAT o directory).</span><span class="sxs-lookup"><span data-stu-id="0183b-167">Otherwise, FX_FALSE if a system sector (FAT or directory sector) is requested.</span></span>|
|<span data-ttu-id="0183b-168">fx_media_driver_sector_type</span><span class="sxs-lookup"><span data-stu-id="0183b-168">fx_media_driver_sector_type</span></span>|<span data-ttu-id="0183b-169">Definisce il tipo esplicito di settore richiesto, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0183b-169">Defines the explicit type of sector requested, as follows:</span></span><br /><span data-ttu-id="0183b-170">FX_FAT_SECTOR (2)</span><span class="sxs-lookup"><span data-stu-id="0183b-170">FX_FAT_SECTOR (2)</span></span><br /><span data-ttu-id="0183b-171">FX_DIRECTORY_SECTOR (3)</span><span class="sxs-lookup"><span data-stu-id="0183b-171">FX_DIRECTORY_SECTOR (3)</span></span><br /><span data-ttu-id="0183b-172">FX_DATA_SECTOR (4)</span><span class="sxs-lookup"><span data-stu-id="0183b-172">FX_DATA_SECTOR (4)</span></span>|

### <a name="sector-write"></a><span data-ttu-id="0183b-173">Scrittura settore</span><span class="sxs-lookup"><span data-stu-id="0183b-173">Sector Write</span></span>

<span data-ttu-id="0183b-174">FileX scrive uno o più settori nel supporto fisico inviando una richiesta di scrittura al driver di I/O.</span><span class="sxs-lookup"><span data-stu-id="0183b-174">FileX writes one or more sectors to the physical media by issuing a write request to the I/O driver.</span></span> <span data-ttu-id="0183b-175">Per la richiesta di scrittura del driver i/O vengono utilizzati i membri FX_MEDIA seguenti:</span><span class="sxs-lookup"><span data-stu-id="0183b-175">The following FX_MEDIA members are used for the I/O driver write request:</span></span>

|<span data-ttu-id="0183b-176">Membro FX_MEDIA</span><span class="sxs-lookup"><span data-stu-id="0183b-176">FX_MEDIA member</span></span>| <span data-ttu-id="0183b-177">Significato</span><span class="sxs-lookup"><span data-stu-id="0183b-177">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="0183b-178">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="0183b-178">fx_media_driver_request</span></span>|<span data-ttu-id="0183b-179">FX_DRIVER_WRITE</span><span class="sxs-lookup"><span data-stu-id="0183b-179">FX_DRIVER_WRITE</span></span>|
|<span data-ttu-id="0183b-180">fx_media_driver_logical_sector</span><span class="sxs-lookup"><span data-stu-id="0183b-180">fx_media_driver_logical_sector</span></span>|<span data-ttu-id="0183b-181">Settore logico da scrivere</span><span class="sxs-lookup"><span data-stu-id="0183b-181">Logical sector to write</span></span>|
|<span data-ttu-id="0183b-182">fx_media_driver_sectors</span><span class="sxs-lookup"><span data-stu-id="0183b-182">fx_media_driver_sectors</span></span>|<span data-ttu-id="0183b-183">Numero di settori da scrivere</span><span class="sxs-lookup"><span data-stu-id="0183b-183">Number of sectors to write</span></span>|
|<span data-ttu-id="0183b-184">fx_media_driver_buffer</span><span class="sxs-lookup"><span data-stu-id="0183b-184">fx_media_driver_buffer</span></span>|<span data-ttu-id="0183b-185">Buffer di origine per i settori da scrivere</span><span class="sxs-lookup"><span data-stu-id="0183b-185">Source buffer for sector(s) to write</span></span>|
|<span data-ttu-id="0183b-186">fx_media_driver_system_write</span><span class="sxs-lookup"><span data-stu-id="0183b-186">fx_media_driver_system_write</span></span>| <span data-ttu-id="0183b-187">Impostare su FX_TRUE se viene richiesto un settore di sistema (FAT o settore di directory).</span><span class="sxs-lookup"><span data-stu-id="0183b-187">Set to FX_TRUE if a system sector is requested (FAT or directory sector).</span></span> <span data-ttu-id="0183b-188">In caso contrario, FX_FALSE se viene richiesto un settore di dati di file.</span><span class="sxs-lookup"><span data-stu-id="0183b-188">Otherwise, FX_FALSE if a file data sector is requested.</span></span>|
|<span data-ttu-id="0183b-189">fx_media_driver_sector_type</span><span class="sxs-lookup"><span data-stu-id="0183b-189">fx_media_driver_sector_type</span></span>|<span data-ttu-id="0183b-190">Definisce il tipo esplicito di settore richiesto, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0183b-190">Defines the explicit type of sector requested, as follows:</span></span><br> <br><span data-ttu-id="0183b-191">FX_FAT_SECTOR (2)</span><span class="sxs-lookup"><span data-stu-id="0183b-191">FX_FAT_SECTOR (2)</span></span> <br> <span data-ttu-id="0183b-192">FX_DIRECTORY_SECTOR (3)</span><span class="sxs-lookup"><span data-stu-id="0183b-192">FX_DIRECTORY_SECTOR (3)</span></span> <br><span data-ttu-id="0183b-193">FX_DATA_SECTOR (4).</span><span class="sxs-lookup"><span data-stu-id="0183b-193">FX_DATA_SECTOR (4).</span></span>|

### <a name="driver-flush"></a><span data-ttu-id="0183b-194">Scaricamento driver</span><span class="sxs-lookup"><span data-stu-id="0183b-194">Driver Flush</span></span>

<span data-ttu-id="0183b-195">FileX Scarica tutti i settori attualmente presenti nella cache del settore del driver nel supporto fisico inviando una richiesta di scaricamento al driver di I/O.</span><span class="sxs-lookup"><span data-stu-id="0183b-195">FileX flushes all sectors currently in the driver's sector cache to the physical media by issuing a flush request to the I/O driver.</span></span> <span data-ttu-id="0183b-196">Naturalmente, se il driver non è la memorizzazione nella cache dei settori, questa richiesta non richiede l'elaborazione del driver.</span><span class="sxs-lookup"><span data-stu-id="0183b-196">Of course, if the driver is not caching sectors, this request requires no driver processing.</span></span> <span data-ttu-id="0183b-197">Per la richiesta di scaricamento del driver I/O vengono utilizzati i membri FX_MEDIA seguenti:</span><span class="sxs-lookup"><span data-stu-id="0183b-197">The following FX_MEDIA members are used for the I/O driver flush request:</span></span>

|<span data-ttu-id="0183b-198">Membro FX_MEDIA</span><span class="sxs-lookup"><span data-stu-id="0183b-198">FX_MEDIA member</span></span>| <span data-ttu-id="0183b-199">Significato</span><span class="sxs-lookup"><span data-stu-id="0183b-199">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="0183b-200">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="0183b-200">fx_media_driver_request</span></span>|<span data-ttu-id="0183b-201">FX_DRIVER_FLUSH</span><span class="sxs-lookup"><span data-stu-id="0183b-201">FX_DRIVER_FLUSH</span></span>|

### <a name="driver-abort"></a><span data-ttu-id="0183b-202">Interruzione driver</span><span class="sxs-lookup"><span data-stu-id="0183b-202">Driver Abort</span></span>

<span data-ttu-id="0183b-203">FileX indica al driver di interrompere tutte le altre attività di I/O fisiche con i supporti fisici inviando una richiesta di interruzione al driver di I/O.</span><span class="sxs-lookup"><span data-stu-id="0183b-203">FileX informs the driver to abort all further physical I/O activity with the physical media by issuing an abort request to the I/O driver.</span></span> <span data-ttu-id="0183b-204">Il driver non deve eseguire nuovamente le operazioni di I/O fino a quando non viene nuovamente inizializzato.</span><span class="sxs-lookup"><span data-stu-id="0183b-204">The driver should not perform any I/O again until it is re-initialized.</span></span> <span data-ttu-id="0183b-205">Per la richiesta di interruzione del driver I/O vengono utilizzati i membri FX_MEDIA seguenti:</span><span class="sxs-lookup"><span data-stu-id="0183b-205">The following FX_MEDIA members are used for the I/O driver abort request:</span></span>

|<span data-ttu-id="0183b-206">Membro FX_MEDIA</span><span class="sxs-lookup"><span data-stu-id="0183b-206">FX_MEDIA member</span></span>| <span data-ttu-id="0183b-207">Significato</span><span class="sxs-lookup"><span data-stu-id="0183b-207">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="0183b-208">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="0183b-208">fx_media_driver_request</span></span>| <span data-ttu-id="0183b-209">FX_DRIVER_ABORT</span><span class="sxs-lookup"><span data-stu-id="0183b-209">FX_DRIVER_ABORT</span></span>|

### <a name="release-sectors"></a><span data-ttu-id="0183b-210">Settori di rilascio</span><span class="sxs-lookup"><span data-stu-id="0183b-210">Release Sectors</span></span>

<span data-ttu-id="0183b-211">Se selezionato in precedenza dal driver durante l'inizializzazione, FileX informa il driver ogni volta che uno o più settori consecutivi diventano disponibili.</span><span class="sxs-lookup"><span data-stu-id="0183b-211">If previously selected by the driver during initialization, FileX informs the driver whenever one or more consecutive sectors become free.</span></span> <span data-ttu-id="0183b-212">Se il driver è effettivamente una gestione FLASH, queste informazioni possono essere usate per indicare a gestione FLASH che questi settori non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="0183b-212">If the driver is actually a FLASH manager, this information can be used to tell the FLASH manager that these sectors are no longer needed.</span></span> <span data-ttu-id="0183b-213">Per la richiesta dei settori di rilascio i/O vengono usati i membri **FX_MEDIA** seguenti:</span><span class="sxs-lookup"><span data-stu-id="0183b-213">The following **FX_MEDIA** members are used for the I/O release sectors request:</span></span>

|<span data-ttu-id="0183b-214">Membro FX_MEDIA</span><span class="sxs-lookup"><span data-stu-id="0183b-214">FX_MEDIA member</span></span>| <span data-ttu-id="0183b-215">Significato</span><span class="sxs-lookup"><span data-stu-id="0183b-215">Meaning</span></span>|
|-----------|-----------|
|<span data-ttu-id="0183b-216">fx_media_driver_request</span><span class="sxs-lookup"><span data-stu-id="0183b-216">fx_media_driver_request</span></span>|<span data-ttu-id="0183b-217">FX_DRIVER_RELEASE_SECTORS</span><span class="sxs-lookup"><span data-stu-id="0183b-217">FX_DRIVER_RELEASE_SECTORS</span></span>|
|<span data-ttu-id="0183b-218">fx_media_driver_logical_sector</span><span class="sxs-lookup"><span data-stu-id="0183b-218">fx_media_driver_logical_sector</span></span>|<span data-ttu-id="0183b-219">Inizio del settore gratuito</span><span class="sxs-lookup"><span data-stu-id="0183b-219">Start of free sector</span></span>|
|<span data-ttu-id="0183b-220">fx_media_driver_sectors</span><span class="sxs-lookup"><span data-stu-id="0183b-220">fx_media_driver_sectors</span></span>|<span data-ttu-id="0183b-221">Numero di settori disponibili</span><span class="sxs-lookup"><span data-stu-id="0183b-221">Number of free sectors</span></span>|

### <a name="driver-suspension"></a><span data-ttu-id="0183b-222">Sospensione driver</span><span class="sxs-lookup"><span data-stu-id="0183b-222">Driver Suspension</span></span>

<span data-ttu-id="0183b-223">Poiché l'I/O con supporti fisici potrebbe richiedere del tempo, è spesso consigliabile sospendere il thread chiamante.</span><span class="sxs-lookup"><span data-stu-id="0183b-223">Because I/O with physical media may take some time, suspending the calling thread is often desirable.</span></span> <span data-ttu-id="0183b-224">Naturalmente, ciò presuppone che il completamento dell'operazione di I/O sottostante sia basato sull'interrupt.</span><span class="sxs-lookup"><span data-stu-id="0183b-224">Of course, this assumes completion of the underlying I/O operation is interrupt driven.</span></span> <span data-ttu-id="0183b-225">In tal caso, la sospensione dei thread viene facilmente implementata con un semaforo ThreadX.</span><span class="sxs-lookup"><span data-stu-id="0183b-225">If so, thread suspension is easily implemented with a ThreadX semaphore.</span></span> <span data-ttu-id="0183b-226">Dopo l'avvio dell'operazione di input o di output, il driver di I/O viene sospeso sul proprio semaforo di I/O interno, creato con un conteggio iniziale pari a zero durante l'inizializzazione del driver.</span><span class="sxs-lookup"><span data-stu-id="0183b-226">After starting the input or output operation, the I/O driver suspends on its own internal I/O semaphore (created with an initial count of zero during driver initialization).</span></span> <span data-ttu-id="0183b-227">Come parte dell'elaborazione dell'interrupt di completamento i/O del driver, viene impostato lo stesso semaforo di I/O, che a sua volta riattiva il thread sospeso.</span><span class="sxs-lookup"><span data-stu-id="0183b-227">As part of the driver I/O completion interrupt processing, the same I/O semaphore is set, which in turn wakes up the suspended thread.</span></span>

### <a name="sector-translation"></a><span data-ttu-id="0183b-228">Conversione settore</span><span class="sxs-lookup"><span data-stu-id="0183b-228">Sector Translation</span></span>

<span data-ttu-id="0183b-229">Poiché FileX Visualizza i supporti come settori logici lineari, le richieste di I/O effettuate al driver di I/O vengono eseguite con i settori logici.</span><span class="sxs-lookup"><span data-stu-id="0183b-229">Because FileX views the media as linear logical sectors, I/O requests made to the I/O driver are made with logical sectors.</span></span> <span data-ttu-id="0183b-230">Il conducente è responsabile della conversione tra i settori logici e la geometria fisica del supporto, che può includere testine, tracce e settori fisici.</span><span class="sxs-lookup"><span data-stu-id="0183b-230">It is the driver's responsibility to translate between logical sectors and the physical geometry of the media, which may include heads, tracks, and physical sectors.</span></span> <span data-ttu-id="0183b-231">Per i supporti disco FLASH e RAM, i settori logici in genere mappano la directory ai settori fisici.</span><span class="sxs-lookup"><span data-stu-id="0183b-231">For FLASH and RAM disk media, the logical sectors typically map directory to physical sectors.</span></span> <span data-ttu-id="0183b-232">In ogni caso, di seguito sono riportate le formule tipiche per eseguire il mapping logico a settore fisico nel driver I/O:</span><span class="sxs-lookup"><span data-stu-id="0183b-232">In any case, here are the typical formulas to perform the logical to physical sector mapping in the I/O driver:</span></span>

```c
media_ptr -> fx_media_driver_physical_sector =
    (media_ptr -> fx_media_driver_logical_sector % media_ptr -> fx_media_sectors_per_track) + 1;

media_ptr -> fx_media_driver_physical_head =
    (media_ptr -> fx_media_driver_logical_sector/ media_ptr ->
    fx_media_sectors_per_track) % media_ptr -> fx_media_heads;

media_ptr -> fx_media_driver_physical_track =(media_ptr ->
    fx_media_driver_logical_sector/ (media_ptr -> fx_media_sectors_per_track *
    media_ptr -> fx_media_heads)));
```

<span data-ttu-id="0183b-233">Si noti che i settori fisici iniziano da uno, mentre i settori logici iniziano da zero.</span><span class="sxs-lookup"><span data-stu-id="0183b-233">Note that physical sectors start at one, while logical sectors start at zero.</span></span>

### <a name="hidden-sectors"></a><span data-ttu-id="0183b-234">Settori nascosti</span><span class="sxs-lookup"><span data-stu-id="0183b-234">Hidden Sectors</span></span>

<span data-ttu-id="0183b-235">I settori nascosti risiedevano prima del record di avvio sui supporti.</span><span class="sxs-lookup"><span data-stu-id="0183b-235">Hidden sectors resided prior to the boot record on the media.</span></span> <span data-ttu-id="0183b-236">Poiché si trovano realmente al di fuori dell'ambito del layout file system FAT, è necessario che siano contabilizzate in ogni operazione di settore logico eseguita dal driver.</span><span class="sxs-lookup"><span data-stu-id="0183b-236">Because they are really outside the scope of the FAT file system layout, they must be accounted for in each logical sector operation the driver does.</span></span>

### <a name="media-write-protect"></a><span data-ttu-id="0183b-237">Protezione scrittura supporti</span><span class="sxs-lookup"><span data-stu-id="0183b-237">Media Write Protect</span></span>

<span data-ttu-id="0183b-238">Il driver FileX può attivare la protezione da scrittura impostando il campo fx_media_driver_write_protect nel blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="0183b-238">The FileX driver can turn on write protect by setting the fx_media_driver_write_protect field in the media control block.</span></span> <span data-ttu-id="0183b-239">In questo modo verrà restituito un errore se vengono effettuate chiamate FileX durante un tentativo di scrittura nei supporti.</span><span class="sxs-lookup"><span data-stu-id="0183b-239">This will cause an error to be returned if any FileX calls are made in an attempt to write to the media.</span></span>

## <a name="sample-ram-driver"></a><span data-ttu-id="0183b-240">Driver RAM di esempio</span><span class="sxs-lookup"><span data-stu-id="0183b-240">Sample RAM Driver</span></span>

<span data-ttu-id="0183b-241">Il sistema di dimostrazione FileX viene fornito con un piccolo driver di disco RAM, definito nel file fx_ram_driver. c.</span><span class="sxs-lookup"><span data-stu-id="0183b-241">The FileX demonstration system is delivered with a small RAM disk driver, which is defined in the file fx_ram_driver.c.</span></span> <span data-ttu-id="0183b-242">Il driver presuppone uno spazio di memoria 32K e crea un record di avvio per i settori a 256 128 byte.</span><span class="sxs-lookup"><span data-stu-id="0183b-242">The driver assumes a 32K memory space and creates a boot record for 256 128-byte sectors.</span></span> <span data-ttu-id="0183b-243">Questo file fornisce un valido esempio di implementazione di driver di I/O FileX specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0183b-243">This file provides a good example of how to implement application specific FileX I/O drivers.</span></span>

```c
/*FUNCTION: _fx_ram_driver
RELEASE: PORTABLE C 5.7
AUTHOR: William E. Lamie, Microsoft, Inc.
DESCRIPTION: This function is the entry point to the generic
    RAM disk driver that is delivered with all versions of FileX.
    The format of the RAM disk is easily modified by calling fx_media_format prior to opening the media.

    This driver also serves as a template for developing FileX drivers
    for actual devices. Simply replace the read/write sector logic
    with calls to read/write from the appropriate physical device.

FileX RAM/FLASH structures look like the following:
Physical Sector             Contents
    0                         Boot record
    1                         FAT Area Start
    +FAT Sectors             Root Directory Start
    +Directory Sectors         Data Sector Start

INPUT: media_ptr Media control block pointer
OUTPUT: None
CALLS:     _fx_utility_memory_copy Copy sector memory
        _fx_utility_16_unsigned_read Read 16-bit unsigned
CALLED BY: FileX System Functions
RELEASE HISTORY:

    DATE         NAME         DESCRIPTION
    12-12-2005     William E.     Lamie Initial Version 5.0
    07-18-2007     William E.     Lamie Modified comment(s),
                                resulting in version 5.1
    03-01-2009     William E.     Lamie Modified comment(s),
                                resulting in version 5.2
    11-01-2015     William E.     Lamie Modified comment(s),
                                resulting in version 5.3
    04-15-2016     William E.     Lamie Modified comment(s),
                                resulting in version 5.4
    04-03-2017     William E.     Lamie Modified comment(s),
                                fixed compiler warnings,
                                resulting in version 5.5
    12-01-2018     William E.     Lamie Modified comment(s),
                                checked buffer overflow,
                                resulting in version 5.6
    08-15-2019     William E.     Lamie Modified comment(s),
                                resulting in version 5.7
*/

VOID _fx_ram_driver(FX_MEDIA *media_ptr) { UCHAR *source_buffer;
                                           UCHAR *destination_buffer;
                                           UINT bytes_per_sector;

    /* There are several useful/important pieces of information contained
        in the media structure, some of which are supplied by FileX and
        others are for the driver to setup. The following
        is a summary of the necessary FX_MEDIA structure members:
    FX_MEDIA Member                     Meaning

    fx_media_driver_request             FileX request type.
        Valid requests from FileX are as follows:
        FX_DRIVER_READ
        FX_DRIVER_WRITE
        FX_DRIVER_FLUSH
        FX_DRIVER_ABORT
        FX_DRIVER_INIT
        FX_DRIVER_BOOT_READ
        FX_DRIVER_RELEASE_SECTORS
        FX_DRIVER_BOOT_WRITE FX_DRIVER_UNINIT

    fx_media_driver_status              This value is RETURNED by the driver.
        If the operation is successful, this field should be set to FX_SUCCESS
        for before returning. Otherwise, if an error occurred, this field should be set to FX_IO_ERROR.

    fx_media_driver_buffer              Pointer to buffer to read or write sector data. This is supplied by FileX.

    fx_media_driver_logical_sector      Logical sector FileX is requesting.
    fx_media_driver_sectors             Number of sectors FileX is requesting.

    The following is a summary of the optional FX_MEDIA structure members: FX_MEDIA Member Meaning

    fx_media_driver_info                Pointer to any additional information or memory.
        This is optional for the driver use and is setup from the fx_media_open call.
        The RAM disk uses this pointer for the RAM disk memory itself.

    fx_media_driver_write_protect       The DRIVER sets this to FX_TRUE when media is write protected.
        This is typically done in initialization, but can be done anytime.

    fx_media_driver_free_sector_update  The DRIVER sets this to FX_TRUE when it needs
        to know when clusters are released. This is important for FLASH wear-leveling drivers.

    fx_media_driver_system_write        FileX sets this flag to FX_TRUE if the sector
        being written is a system sector, e.g., a boot, FAT, or directory sector.
        The driver may choose to use this to initiate error recovery logic for greater fault
        tolerance. fx_media_driver_data_sector_read FileX sets this flag to FX_TRUE
        if the sector(s) being read are file data sectors, i.e., NOT system sectors.

    fx_media_driver_sector_type         FileX sets this variable to the specific type of
        sector being read or written. The following sector types are identified:
            FX_UNKNOWN_SECTOR
            FX_BOOT_SECTOR
            FX_FAT_SECTOR
            FX_DIRECTORY_SECTOR
            FX_DATA_SECTOR */

    /* Process the driver request specified in the media control block. */

    switch (media_ptr -> fx_media_driver_request){

        case FX_DRIVER_READ: {

            /* Calculate the RAM disk sector offset. Note the RAM disk memory
            is pointed to by the fx_media_driver_info pointer, which is supplied
            by the application in the call to fx_media_open. */

            source_buffer = ((UCHAR *)media_ptr -> fx_media_driver_info) +
                ((media_ptr -> fx_media_driver_logical_sector +
                media_ptr -> fx_media_hidden_sectors) * media_ptr -> fx_media_bytes_per_sector);

            /* Copy the RAM sector into the destination. */

             _fx_utility_memory_copy(source_buffer,
                media_ptr -> fx_media_driver_buffer, media_ptr -> fx_media_driver_sectors *
                media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_WRITE: {

            /* Calculate the RAM disk sector offset. Note the RAM disk memory
                is pointed to by the fx_media_driver_info pointer, which is supplied
                by the application in the call to fx_media_open. */

            destination_buffer = ((UCHAR *)media_ptr -> fx_media_driver_info) +
                ((media_ptr -> fx_media_driver_logical_sector +
                media_ptr -> fx_media_hidden_sectors) * media_ptr -> fx_media_bytes_per_sector);

            /* Copy the source to the RAM sector. */

            _fx_utility_memory_copy(media_ptr -> fx_media_driver_buffer,
                destination_buffer, media_ptr -> fx_media_driver_sectors *
                media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_FLUSH: {
            /* Return driver success. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_ABORT: {
            /* Return driver success. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_INIT: {

            /* FLASH drivers are responsible for setting several fields
                in the media structure, as follows:
                media_ptr -> fx_media_driver_free_sector_update media_ptr ->
                fx_media_driver_write_protect
                The fx_media_driver_free_sector_update flag is used to instruct
                FileX to inform the driver whenever sectors are not being used.
                This is especially useful for FLASH managers so they don't have
                maintain mapping for sectors no longer in use.
                The fx_media_driver_write_protect flag can be set anytime by
                the driver to indicate the media is not writable. Write attempts
                made when this flag is set are returned as errors. */
            /* Perform basic initialization here... since the boot record is going
                to be read subsequently and again for volume name requests. */
            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

         case FX_DRIVER_UNINIT: {

            /* There is nothing to do in this case for the RAM driver.
                For actual devices some shutdown processing may be necessary. */

            /* Successful driver request. */
            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_BOOT_READ: {
            /* Read the boot record and return to the caller. */

            /* Calculate the RAM disk boot sector offset, which is at the
                very beginning of the RAM disk. Note the RAM disk memory is pointed
                to by the fx_media_driver_info pointer, which is supplied by the
                application in the call to fx_media_open. */

            source_buffer = (UCHAR *)media_ptr -> fx_media_driver_info;

            /* For RAM driver, determine if the boot record is valid. */

            if ((source_buffer[0] != (UCHAR)0xEB) ||

            ((source_buffer[1] != (UCHAR)0x34) &&

            (source_buffer[1] != (UCHAR)0x76)) || /* exFAT jump code. */

            (source_buffer[2] != (UCHAR)0x90)) {

            /* Invalid boot record, return an error! */
            media_ptr -> fx_media_driver_status = FX_MEDIA_INVALID; return; }

            /* For RAM disk only, pickup the bytes per sector. */

            bytes_per_sector =
                _fx_utility_16_unsigned_read(&source_buffer[FX_BYTES_SECTOR]); #ifdef FX_ENABLE_EXFAT

            /* if byte per sector is zero, then treat it as exFAT volume. */

            if (bytes_per_sector == 0 && (source_buffer[1] == (UCHAR)0x76)) {

            /* Pickup the byte per sector shift, and calculate byte per sector. */ 
            bytes_per_sector = (UINT)(1 << source_buffer[FX_EF_BYTE_PER_SECTOR_SHIFT]);

            }

            #endif /* FX_ENABLE_EXFAT */

            /* Ensure this is less than the media memory size. */
            if (bytes_per_sector \media_ptr -> fx_media_memory_size) {

            media_ptr -> fx_media_driver_status = FX_BUFFER_ERROR; break; }

            /* Copy the RAM boot sector into the destination. */

            _fx_utility_memory_copy(source_buffer, media_ptr -> fx_media_driver_buffer, bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        case FX_DRIVER_BOOT_WRITE: {

            /* Write the boot record and return to the caller. */

            /* Calculate the RAM disk boot sector offset, which is at the
                very beginning of the RAM disk. Note the RAM disk memory is
                pointed to by the fx_media_driver_info pointer, which is supplied
                by the application in the call to fx_media_open. */ 
            destination_buffer = (UCHAR *)media_ptr -> fx_media_driver_info;

            /* Copy the RAM boot sector into the destination. */

            _fx_utility_memory_copy(media_ptr -> fx_media_driver_buffer,
                destination_buffer, media_ptr -> fx_media_bytes_per_sector);

            /* Successful driver request. */

            media_ptr -> fx_media_driver_status = FX_SUCCESS; break; }

        default: {
            /* Invalid driver request. */
            media_ptr -> fx_media_driver_status = FX_IO_ERROR; break;}
    }
}
```
