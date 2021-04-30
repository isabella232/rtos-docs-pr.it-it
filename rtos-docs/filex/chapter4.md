---
title: Capitolo 4- Descrizione dei Azure RTOS FileX
description: Questo capitolo contiene una descrizione di tutti i Azure RTOS FileX in ordine alfabetico.
author: philmea
ms.author: philmea
ms.date: 05/19/2020
ms.topic: article
ms.service: rtos
ms.openlocfilehash: f70b8890be6b12f917ac1724a29559afab33b88d
ms.sourcegitcommit: 0520b2afb6b7f8ae1ea48581e160459fc9292ca7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/30/2021
ms.locfileid: "108297497"
---
# <a name="chapter-4--description-of-azure-rtos-filex-services"></a><span data-ttu-id="9969a-103">Capitolo 4- Descrizione dei Azure RTOS FileX</span><span class="sxs-lookup"><span data-stu-id="9969a-103">Chapter 4- Description of Azure RTOS FileX services</span></span>

<span data-ttu-id="9969a-104">Questo capitolo contiene una descrizione di tutti i Azure RTOS FileX in ordine alfabetico.</span><span class="sxs-lookup"><span data-stu-id="9969a-104">This chapter contains a description of all Azure RTOS FileX services in alphabetic order.</span></span> <span data-ttu-id="9969a-105">I nomi dei servizi sono progettati in modo da raggruppare tutti i servizi simili.</span><span class="sxs-lookup"><span data-stu-id="9969a-105">Service names are designed so all similar services are grouped together.</span></span>

## <a name="fx_directory_attributes_read"></a><span data-ttu-id="9969a-106">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-106">fx_directory_attributes_read</span></span>

<span data-ttu-id="9969a-107">Legge gli attributi della directory</span><span class="sxs-lookup"><span data-stu-id="9969a-107">Reads directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-108">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-108">Prototype</span></span>

```c
UINT fx_directory_attributes_read ( 
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes_ptr);
```

### <a name="description"></a><span data-ttu-id="9969a-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-109">Description</span></span>

<span data-ttu-id="9969a-110">Questo servizio legge gli attributi della directory dal supporto specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-110">This service reads the directory's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-111">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-111">Input Parameters</span></span>

- <span data-ttu-id="9969a-112">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-112">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-113">**directory_name**: puntatore al nome della directory richiesta (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="9969a-113">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="9969a-114">**attributes** _ptr: puntatore alla destinazione per gli attributi della directory da inserire.</span><span class="sxs-lookup"><span data-stu-id="9969a-114">**attributes** _ptr: Pointer to the destination for the directory's attributes to be placed.</span></span> <span data-ttu-id="9969a-115">Gli attributi della directory vengono restituiti in un formato mappa di bit con le impostazioni possibili seguenti:</span><span class="sxs-lookup"><span data-stu-id="9969a-115">The directory attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="9969a-116">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="9969a-116">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="9969a-117">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="9969a-117">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="9969a-118">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="9969a-118">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="9969a-119">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="9969a-119">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="9969a-120">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="9969a-120">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="9969a-121">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="9969a-121">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-122">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-122">Return Values</span></span>

- <span data-ttu-id="9969a-123">**FX_SUCCESS** (0x00) Lettura degli attributi di directory riuscita</span><span class="sxs-lookup"><span data-stu-id="9969a-123">**FX_SUCCESS** (0x00) Successful directory attributes read</span></span>
- <span data-ttu-id="9969a-124">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-124">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="9969a-125">**FX _NOT FOUND** (0x04) Directory specificata non trovata nel supporto</span><span class="sxs-lookup"><span data-stu-id="9969a-125">**FX _NOT FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="9969a-126">**FX_NOT_DIRECTORY** (0x0E) La voce non è una directory</span><span class="sxs-lookup"><span data-stu-id="9969a-126">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="9969a-127">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90)</span><span class="sxs-lookup"><span data-stu-id="9969a-127">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="9969a-128">**FX_FILE_CORRUPT** 0x08) Il file è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-128">**FX_FILE_CORRUPT** 0x08) File is corrupted</span></span>
- <span data-ttu-id="9969a-129">**FX_SECTOR_INVALID** (0x89) Settore non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-129">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="9969a-130">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="9969a-130">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="9969a-131">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-131">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-132">**FX_MEDIA_INVALID** (0x02) Supporto non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-132">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="9969a-133">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-133">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="9969a-134">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-134">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-135">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-135">Allowed From</span></span>

<span data-ttu-id="9969a-136">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-136">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-137">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-137">Example</span></span>

```c
FX_MEDIA     my_media;
UINT     status;
/* Retrieve the attributes of "mydir" from the specified media.*/
status = fx_directory_attributes_read(&my_media, "mydir", &attributes);
/* If status equals FX_SUCCESS, "attributes" contains the directory attributes of "mydir". */
```

### <a name="see-also"></a><span data-ttu-id="9969a-138">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-138">See Also</span></span>

- <span data-ttu-id="9969a-139">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-139">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-140">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-140">fx_directory_create</span></span>
- <span data-ttu-id="9969a-141">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-141">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-142">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-142">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-143">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-143">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-144">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-144">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-145">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-145">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-146">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-146">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-147">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-147">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-148">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-148">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-149">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-149">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-150">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-150">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-151">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-151">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-152">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-152">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-153">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-153">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-154">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-154">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-155">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-155">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-156">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-156">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-157">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-157">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-158">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-158">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_attributes_set"></a><span data-ttu-id="9969a-159">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-159">fx_directory_attributes_set</span></span>

<span data-ttu-id="9969a-160">Imposta gli attributi della directory</span><span class="sxs-lookup"><span data-stu-id="9969a-160">Sets directory attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-161">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-161">Prototype</span></span>

```c
UINT fx_directory_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes);
```

### <a name="description"></a><span data-ttu-id="9969a-162">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-162">Description</span></span>

<span data-ttu-id="9969a-163">Questo servizio imposta gli attributi della directory su quelli specificati dal chiamante.</span><span class="sxs-lookup"><span data-stu-id="9969a-163">This service sets the directory's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-164">*Questa applicazione può modificare solo un subset degli attributi della directory con questo servizio. Qualsiasi tentativo di impostare attributi aggiuntivi restituirà un errore.*</span><span class="sxs-lookup"><span data-stu-id="9969a-164">*This application is only allowed to modify a subset of the directory's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-165">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-165">Input Parameters</span></span>

- <span data-ttu-id="9969a-166">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-166">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-167">**directory_name**: puntatore al nome della directory richiesta (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="9969a-167">**directory_name**: Pointer to the name of the requested directory (directory path is optional).</span></span>
- <span data-ttu-id="9969a-168">**attributes:** nuovi attributi per questa directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-168">**attributes**: The new attributes to this directory.</span></span> <span data-ttu-id="9969a-169">Gli attributi di directory validi sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="9969a-169">The valid directory attributes are defined as follows:</span></span>
  - <span data-ttu-id="9969a-170">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="9969a-170">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="9969a-171">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="9969a-171">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="9969a-172">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="9969a-172">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="9969a-173">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="9969a-173">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-174">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-174">Return Values</span></span>

- <span data-ttu-id="9969a-175">**FX_SUCCESS** (0x00) Set di attributi di directory riuscito</span><span class="sxs-lookup"><span data-stu-id="9969a-175">**FX_SUCCESS** (0x00) Successful directory attribute set</span></span>
- <span data-ttu-id="9969a-176">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-176">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="9969a-177">**FX_NOT_FOUND** (0x04) Directory specificata non trovata nel supporto</span><span class="sxs-lookup"><span data-stu-id="9969a-177">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="9969a-178">**FX_NOT_DIRECTORY** (0x0E) La voce non è una directory</span><span class="sxs-lookup"><span data-stu-id="9969a-178">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="9969a-179">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90)</span><span class="sxs-lookup"><span data-stu-id="9969a-179">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="9969a-180">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura</span><span class="sxs-lookup"><span data-stu-id="9969a-180">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="9969a-181">**FX_FILE_CORRUPT** (0x08) Il file è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-181">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="9969a-182">**FX_SECTOR_INVALID** (0x89) Settore non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-182">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="9969a-183">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="9969a-183">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="9969a-184">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-184">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-185">**FX_MEDIA_INVALID** (0x02) Supporto non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-185">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="9969a-186">**FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory</span><span class="sxs-lookup"><span data-stu-id="9969a-186">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="9969a-187">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-187">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="9969a-188">**FX_INVALID_ATTR** (0x19) Attributi non validi selezionati.</span><span class="sxs-lookup"><span data-stu-id="9969a-188">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="9969a-189">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-190">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-190">Allowed From</span></span>

<span data-ttu-id="9969a-191">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-192">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-192">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
status = fx_directory_attributes_set(&my_media, "mydir", FX_READ_ONLY);
/*Set the attributes of "mydir" to read-only. */
/* If status equals FX_SUCCESS, the directory "mydir" is read-only. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-193">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-193">See Also</span></span>

- <span data-ttu-id="9969a-194">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-194">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-195">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-195">fx_directory_create</span></span>
- <span data-ttu-id="9969a-196">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-196">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-197">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-197">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-198">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-198">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-199">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-199">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-200">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-200">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-201">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-201">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-202">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-202">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-203">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-203">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-204">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-204">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-205">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-205">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-206">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-206">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-207">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-207">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-208">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-208">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-209">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-209">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-210">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-210">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-211">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-211">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-212">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-212">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-213">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-213">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_create"></a><span data-ttu-id="9969a-214">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-214">fx_directory_create</span></span>

<span data-ttu-id="9969a-215">Crea una sottodirectory</span><span class="sxs-lookup"><span data-stu-id="9969a-215">Creates subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-216">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-216">Prototype</span></span>

```c
UINT fx_directory_create(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```
### <a name="description"></a><span data-ttu-id="9969a-217">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-217">Description</span></span>

<span data-ttu-id="9969a-218">Questo servizio crea una sottodirectory nella directory predefinita corrente o nel percorso specificato nel nome della directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-218">This service creates a subdirectory in the current default directory or in the path supplied in the directory name.</span></span> <span data-ttu-id="9969a-219">A differenza della directory radice, le sottodirectory non hanno un limite al numero di file che possono contenere.</span><span class="sxs-lookup"><span data-stu-id="9969a-219">Unlike the root directory, subdirectories do not have a limit on the number of files they can hold.</span></span> <span data-ttu-id="9969a-220">La directory radice può contenere solo il numero di voci determinate dal record di avvio.</span><span class="sxs-lookup"><span data-stu-id="9969a-220">The root directory can only hold the number of entries determined by the boot record.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-221">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-221">Input Parameters</span></span>

- <span data-ttu-id="9969a-222">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-222">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-223">**directory_name**: puntatore al nome della directory da creare (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="9969a-223">**directory_name**: Pointer to the name of the directory to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-224">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-224">Return Values</span></span>

- <span data-ttu-id="9969a-225">**FX_SUCCESS** (0x00) Creazione della directory completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-225">**FX_SUCCESS** (0x00) Successful directory create.</span></span>
- <span data-ttu-id="9969a-226">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-226">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="9969a-227">**FX_NOT_FOUND** (0x04) Directory specificata non trovata nel supporto</span><span class="sxs-lookup"><span data-stu-id="9969a-227">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="9969a-228">**FX_NOT_DIRECTORY** (0x0E) La voce non è una directory</span><span class="sxs-lookup"><span data-stu-id="9969a-228">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory</span></span>
- <span data-ttu-id="9969a-229">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90)</span><span class="sxs-lookup"><span data-stu-id="9969a-229">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="9969a-230">**FX_FILE _CORRUPT** (0x08) Il file è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-230">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="9969a-231">**FX_SECTOR_INVALID** (0x89) Settore non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-231">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="9969a-232">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="9969a-232">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="9969a-233">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-233">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-234">**FX_MEDIA_INVALID** (0x02) Supporto non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-234">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="9969a-235">**FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory</span><span class="sxs-lookup"><span data-stu-id="9969a-235">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="9969a-236">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-236">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="9969a-237">**FX_INVALID_ATTR** (0x19) Attributi non validi selezionati.</span><span class="sxs-lookup"><span data-stu-id="9969a-237">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="9969a-238">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-238">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-239">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-239">Allowed From</span></span>

<span data-ttu-id="9969a-240">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-240">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-241">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-241">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Create a subdirectory called "temp" in the current default directory. */

status = fx_directory_create(&my_media, "temp");

/* If status equals FX_SUCCESS, the new subdirectory "temp" has been created. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-242">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-242">See Also</span></span>

- <span data-ttu-id="9969a-243">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-243">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-244">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-244">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-245">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-245">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-246">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-246">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-247">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-247">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-248">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-248">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-249">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-249">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-250">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-250">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-251">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-251">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-252">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-252">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-253">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-253">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-254">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-254">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-255">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-255">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-256">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-256">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-257">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-257">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-258">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-258">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-259">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-259">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-260">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-260">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-261">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-261">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-262">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-262">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_get"></a><span data-ttu-id="9969a-263">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-263">fx_directory_default_get</span></span>

<span data-ttu-id="9969a-264">Ottiene l'ultima directory predefinita</span><span class="sxs-lookup"><span data-stu-id="9969a-264">Gets last default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-265">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-265">Prototype</span></span>

```c
UINT fx_directory_default_get(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="9969a-266">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-266">Description</span></span>

<span data-ttu-id="9969a-267">Questo servizio restituisce il puntatore all'ultimo percorso impostato ***fx_directory_default_set***.</span><span class="sxs-lookup"><span data-stu-id="9969a-267">This service returns the pointer to the path last set by ***fx_directory_default_set***.</span></span> <span data-ttu-id="9969a-268">Se la directory predefinita non è stata impostata o se la directory predefinita corrente è la directory radice, viene restituito FX_NULL valore .</span><span class="sxs-lookup"><span data-stu-id="9969a-268">If the default directory has not been set or if the current default directory is the root directory, a value of FX_NULL is returned.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-269">*La dimensione predefinita della stringa di percorso interna è di 256 caratteri. è possibile modificarlo modificando FX_MAXIMUM_PATH **in** **fx_api.h e** ricompilando l'intera libreria FileX. Il percorso della stringa di caratteri viene mantenuto per l'applicazione e non viene usato internamente da FileX.*</span><span class="sxs-lookup"><span data-stu-id="9969a-269">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-270">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-270">Input Parameters</span></span>

- <span data-ttu-id="9969a-271">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-271">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-272">**return_path_name:** puntatore alla destinazione per l'ultima stringa di directory predefinita.</span><span class="sxs-lookup"><span data-stu-id="9969a-272">**return_path_name**: Pointer to the destination for the last default directory string.</span></span> <span data-ttu-id="9969a-273">Viene restituito FX_NULL valore se l'impostazione corrente della directory predefinita è la radice.</span><span class="sxs-lookup"><span data-stu-id="9969a-273">A value of FX_NULL is returned if the current setting of the default directory is the root.</span></span> <span data-ttu-id="9969a-274">Quando il supporto viene aperto, root è l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9969a-274">When the media is opened, root is the default.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-275">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-275">Return Values</span></span>

- <span data-ttu-id="9969a-276">**FX_SUCCESS** (0x00) Ottenere la directory predefinita corretta</span><span class="sxs-lookup"><span data-stu-id="9969a-276">**FX_SUCCESS** (0x00) Successful default directory get</span></span>
- <span data-ttu-id="9969a-277">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="9969a-278">**FX_PTR_ERROR** (0x18) Supporto o puntatore di destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-278">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="9969a-279">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-279">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-280">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-280">Allowed From</span></span>

<span data-ttu-id="9969a-281">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-281">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-282">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-282">Example</span></span>

```c
FX_MEDIA my_media;
CHAR *current_default_dir;
UINT status;
/* Retrieve the current default directory. */
status = fx_directory_default_get(&my_media, &current_default_dir);
/* If status equals FX_SUCCESS, "current_default_dir" 
    contains a pointer to the current default directory).*/
```

### <a name="see-also"></a><span data-ttu-id="9969a-283">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-283">See Also</span></span>

- <span data-ttu-id="9969a-284">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-284">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-285">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-285">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-286">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-286">fx_directory_create</span></span>
- <span data-ttu-id="9969a-287">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-287">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-288">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-288">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-289">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-289">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-290">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-290">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-291">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-291">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-292">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-292">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-293">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-293">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-294">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-294">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-295">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-295">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-296">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-296">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-297">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-297">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-298">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-298">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-299">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-299">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-300">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-300">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-301">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-301">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-302">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-302">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-303">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-303">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_default_set"></a><span data-ttu-id="9969a-304">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-304">fx_directory_default_set</span></span>

<span data-ttu-id="9969a-305">Imposta la directory predefinita</span><span class="sxs-lookup"><span data-stu-id="9969a-305">Sets default directory</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-306">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-306">Prototype</span></span>

```c

UINT fx_directory_default_set(
    FX_MEDIA *media_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="9969a-307">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-307">Description</span></span>

<span data-ttu-id="9969a-308">Questo servizio imposta la directory predefinita del supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-308">This service sets the default directory of the media.</span></span> <span data-ttu-id="9969a-309">Se viene specificato FX_NULL valore , la directory predefinita viene impostata sulla directory radice del supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-309">If a value of FX_NULL is supplied, the default directory is set to the media's root directory.</span></span> <span data-ttu-id="9969a-310">Tutte le operazioni di file successive che non specificano in modo esplicito un percorso verranno impostate su questa directory per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9969a-310">All subsequent file operations that do not explicitly specify a path will default to this directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-311">*La dimensione predefinita della stringa di percorso interna è di 256 caratteri. è possibile modificarlo modificando FX_MAXIMUM_PATH **in** **fx_api.h e** ricompilando l'intera libreria FileX. Il percorso della stringa di caratteri viene mantenuto per l'applicazione e non viene usato internamente da FileX.*</span><span class="sxs-lookup"><span data-stu-id="9969a-311">*The default size of the internal path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-312">*Per i nomi forniti dall'applicazione, FileX supporta sia la barra rovesciata ( ) che i caratteri barra (/) per separare directory, sottodirectory e nomi \\ di file. Tuttavia, FileX usa solo il carattere barra rovesciata nei percorsi restituiti all'applicazione.*</span><span class="sxs-lookup"><span data-stu-id="9969a-312">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-313">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-313">Input Parameters</span></span>

- <span data-ttu-id="9969a-314">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-314">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-315">**new_path_name:** puntatore al nuovo nome di directory predefinito.</span><span class="sxs-lookup"><span data-stu-id="9969a-315">**new_path_name**: Pointer to new default directory name.</span></span> <span data-ttu-id="9969a-316">Se viene specificato FX_NULL, la directory predefinita del supporto viene impostata sulla directory radice del supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-316">If a value of FX_NULL is supplied, the default directory of the media is set to the media's root directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-317">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-317">Return Values</span></span>

- <span data-ttu-id="9969a-318">**FX_SUCCESS** (0x00) Set di directory predefinito riuscito</span><span class="sxs-lookup"><span data-stu-id="9969a-318">**FX_SUCCESS** (0x00)  Successful default directory set</span></span>
- <span data-ttu-id="9969a-319">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-319">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="9969a-320">**FX_INVALID_PATH** (0x0D) Impossibile trovare la nuova directory</span><span class="sxs-lookup"><span data-stu-id="9969a-320">**FX_INVALID_PATH** (0x0D) New directory could not be found</span></span>
- <span data-ttu-id="9969a-321">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-321">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="9969a-322">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-322">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-323">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-323">Allowed From</span></span>

<span data-ttu-id="9969a-324">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-324">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-325">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-325">Example</span></span>

```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_default_set(&my_media, "\\abc\\def\\ghi");
/* If status equals FX_SUCCESS, the default directory for this media is \abc\def\ghi. All subsequent file operations that do not explicitly specify a path will default to this directory. Note that the character "\" serves as an escape character in a string. To represent the character "\", use the construct "\\". This is done because of the C language- only one "\" is really present in the string. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-326">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-326">See Also</span></span>

- <span data-ttu-id="9969a-327">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-327">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-328">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-328">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-329">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-329">fx_directory_create</span></span>
- <span data-ttu-id="9969a-330">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-330">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-331">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-331">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-332">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-332">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-333">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-333">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-334">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-334">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-335">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-335">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-336">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-336">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-337">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-337">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-338">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-338">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-339">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-339">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-340">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-340">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-341">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-341">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-342">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-342">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-343">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-343">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-344">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-344">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-345">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-345">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-346">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-346">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_delete"></a><span data-ttu-id="9969a-347">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-347">fx_directory_delete</span></span>

<span data-ttu-id="9969a-348">Elimina la sottodirectory</span><span class="sxs-lookup"><span data-stu-id="9969a-348">Deletes subdirectory</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-349">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-349">Prototype</span></span>

```c
UINT fx_directory_delete(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="9969a-350">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-350">Description</span></span>

<span data-ttu-id="9969a-351">Questo servizio elimina la directory specificata.</span><span class="sxs-lookup"><span data-stu-id="9969a-351">This service deletes the specified directory.</span></span> <span data-ttu-id="9969a-352">Si noti che la directory deve essere vuota per eliminarla.</span><span class="sxs-lookup"><span data-stu-id="9969a-352">Note that the directory must be empty to delete it.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-353">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-353">Input Parameters</span></span>

- <span data-ttu-id="9969a-354">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-354">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-355">**directory_name**: puntatore al nome della directory da eliminare (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="9969a-355">**directory_name**: Pointer to name of directory to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-356">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-356">Return Values</span></span>

- <span data-ttu-id="9969a-357">**FX_SUCCESS** (0x00) Eliminazione directory riuscita</span><span class="sxs-lookup"><span data-stu-id="9969a-357">**FX_SUCCESS** (0x00) Successful directory delete</span></span>
- <span data-ttu-id="9969a-358">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-358">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="9969a-359">**FX_NOT_FOUND** (0x04) Directory specificata non trovata</span><span class="sxs-lookup"><span data-stu-id="9969a-359">**FX_NOT_FOUND** (0x04) Specified directory was not found</span></span>
- <span data-ttu-id="9969a-360">**FX_DIR_NOT_EMPTY** (0x10) La directory specificata non è vuota</span><span class="sxs-lookup"><span data-stu-id="9969a-360">**FX_DIR_NOT_EMPTY** (0x10) Specified directory is not empty</span></span>
- <span data-ttu-id="9969a-361">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90)</span><span class="sxs-lookup"><span data-stu-id="9969a-361">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="9969a-362">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura</span><span class="sxs-lookup"><span data-stu-id="9969a-362">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="9969a-363">**FX_FILE_CORRUPT** (0x08) Il file è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-363">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="9969a-364">**FX_SECTOR_INVALID** (0x89) Settore non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-364">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="9969a-365">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="9969a-365">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="9969a-366">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-366">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-367">**FX_MEDIA_INVALID** (0x02) Supporto non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-367">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="9969a-368">**FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory</span><span class="sxs-lookup"><span data-stu-id="9969a-368">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="9969a-369">**FX_NOT_DIRECTORY** (0x0E) Non è una voce di directory</span><span class="sxs-lookup"><span data-stu-id="9969a-369">**FX_NOT_DIRECTORY** (0x0E) Not a directory entry</span></span>
- <span data-ttu-id="9969a-370">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-370">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>
- <span data-ttu-id="9969a-371">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-371">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-372">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-372">Allowed From</span></span>

<span data-ttu-id="9969a-373">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-373">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-374">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-374">Example</span></span>
```c
FX_MEDIA     my_media;
UINT status;
/* Set the default directory to \abc\def\ghi. */
status = fx_directory_delete(&my_media, "abc");
/* Delete the subdirectory "abc." */
/* If status equals FX_SUCCESS, the subdirectory "abc" was deleted. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-375">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-375">See Also</span></span>

- <span data-ttu-id="9969a-376">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-376">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-377">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-377">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-378">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-378">fx_directory_create</span></span>
- <span data-ttu-id="9969a-379">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-379">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-380">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-380">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-381">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-381">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-382">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-382">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-383">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-383">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-384">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-384">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-385">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-385">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-386">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-386">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-387">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-387">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-388">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-388">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-389">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-389">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-390">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-390">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-391">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-391">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-392">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-392">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-393">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-393">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-394">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-394">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-395">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-395">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_entry_find"></a><span data-ttu-id="9969a-396">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-396">fx_directory_first_entry_find</span></span>

<span data-ttu-id="9969a-397">Ottiene la prima voce di directory</span><span class="sxs-lookup"><span data-stu-id="9969a-397">Gets first directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-398">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-398">Prototype</span></span>

```c
UINT fx_directory_first_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="9969a-399">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-399">Description</span></span>

<span data-ttu-id="9969a-400">Questo servizio recupera il nome della prima voce nella directory predefinita e lo copia nella destinazione specificata.</span><span class="sxs-lookup"><span data-stu-id="9969a-400">This service retrieves the first entry name in the default directory and copies it to the specified destination.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-401">*La destinazione specificata deve essere sufficientemente grande da contenere il nome FileX di dimensioni massime, come definito **FX_MAX_LONG_NAME_LEN.***</span><span class="sxs-lookup"><span data-stu-id="9969a-401">*The specified destination must be large enough to hold the maximum sized FileX name, as defined by **FX_MAX_LONG_NAME_LEN.***</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-402">*Se si usa un percorso non locale, è importante impedire agli altri thread dell'applicazione di modificare questa directory (con un semaforo ThreadX, un mutex o una modifica del livello di priorità) mentre è in corso un attraversamento della directory. In caso contrario, è possibile ottenere risultati non validi.*</span><span class="sxs-lookup"><span data-stu-id="9969a-402">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-403">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-403">Input Parameters</span></span>

- <span data-ttu-id="9969a-404">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-404">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-405">**return_entry_name**: puntatore alla destinazione per il nome della prima voce nella directory predefinita.</span><span class="sxs-lookup"><span data-stu-id="9969a-405">**return_entry_name**: Pointer to destination for the first entry name in the default directory.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-406">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-406">Return Values</span></span>

- <span data-ttu-id="9969a-407">**FX_SUCCESS** (0x00) Ricerca della prima voce di directory riuscita</span><span class="sxs-lookup"><span data-stu-id="9969a-407">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="9969a-408">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-408">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="9969a-409">**FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory</span><span class="sxs-lookup"><span data-stu-id="9969a-409">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="9969a-410">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90)</span><span class="sxs-lookup"><span data-stu-id="9969a-410">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="9969a-411">**FX_FILE_CORRUPT** (0x08) Il file è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-411">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="9969a-412">**FX_SECTOR_INVALID** (0x89) Settore non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-412">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="9969a-413">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="9969a-413">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="9969a-414">**FX_PTR_ERROR** (0x18) Supporto non valido o puntatore di destinazione</span><span class="sxs-lookup"><span data-stu-id="9969a-414">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer</span></span>
- <span data-ttu-id="9969a-415">**FX_CALLER_ERROR** (0x20) Il chiamante non è un thread</span><span class="sxs-lookup"><span data-stu-id="9969a-415">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-416">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-416">Allowed From</span></span>

<span data-ttu-id="9969a-417">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-417">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-418">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-418">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;
CHAR             entry[FX_MAX_LONG_NAME_LEN];
/* Retrieve the first directory entry in the current directory. */
status = fx_directory_first_entry_find(&my_media, entry);
/* If status equals FX_SUCCESS, the entry in the directory is the "entry" string. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-419">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-419">See Also</span></span>

- <span data-ttu-id="9969a-420">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-420">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-421">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-421">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-422">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-422">fx_directory_create</span></span>
- <span data-ttu-id="9969a-423">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-423">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-424">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-424">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-425">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-425">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-426">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-426">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-427">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-427">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-428">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-428">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-429">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-429">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-430">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-430">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-431">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-431">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-432">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-432">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-433">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-433">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-434">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-434">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-435">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-435">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-436">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-436">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-437">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-437">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-438">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-438">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-439">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-439">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_first_full_entry_find"></a><span data-ttu-id="9969a-440">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-440">fx_directory_first_full_entry_find</span></span>

<span data-ttu-id="9969a-441">Ottiene la prima voce di directory con informazioni complete</span><span class="sxs-lookup"><span data-stu-id="9969a-441">Gets first directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-442">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-442">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="9969a-443">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-443">Input Parameters</span></span>

- <span data-ttu-id="9969a-444">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-444">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-445">**directory_name**: puntatore alla destinazione per il nome di una voce di directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-445">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="9969a-446">Deve essere grande almeno quanto FX_MAX_LONG_NAME_LEN.</span><span class="sxs-lookup"><span data-stu-id="9969a-446">Must be at least as big as FX_MAX_LONG_NAME_LEN.</span></span>
- <span data-ttu-id="9969a-447">**attributes:** se non Null, puntatore alla destinazione per gli attributi della voce da inserire.</span><span class="sxs-lookup"><span data-stu-id="9969a-447">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.</span></span> <span data-ttu-id="9969a-448">Gli attributi vengono restituiti in un formato mappa di bit con le impostazioni possibili seguenti:</span><span class="sxs-lookup"><span data-stu-id="9969a-448">The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="9969a-449">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="9969a-449">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="9969a-450">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="9969a-450">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="9969a-451">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="9969a-451">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="9969a-452">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="9969a-452">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="9969a-453">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="9969a-453">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="9969a-454">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="9969a-454">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="9969a-455">**size:** se non Null, puntatore alla destinazione per le dimensioni della voce in byte.</span><span class="sxs-lookup"><span data-stu-id="9969a-455">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="9969a-456">**year:** se non Null, puntatore alla destinazione per l'anno di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-456">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="9969a-457">**month:** se non Null, puntatore alla destinazione per il mese di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-457">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="9969a-458">**day:** se non Null, puntatore alla destinazione per il giorno di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-458">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="9969a-459">**hour:** se non Null, puntatore alla destinazione per l'ora di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-459">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="9969a-460">**minute:** se non Null, puntatore alla destinazione per il minuto di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-460">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="9969a-461">**second:** se non Null, puntatore alla destinazione per il secondo elemento di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-461">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-462">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-462">Return Values</span></span>

- <span data-ttu-id="9969a-463">**FX_SUCCESS** (0x00) Ricerca della prima voce di directory riuscita</span><span class="sxs-lookup"><span data-stu-id="9969a-463">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="9969a-464">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-464">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="9969a-465">**FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory</span><span class="sxs-lookup"><span data-stu-id="9969a-465">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory</span></span>
- <span data-ttu-id="9969a-466">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90)</span><span class="sxs-lookup"><span data-stu-id="9969a-466">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="9969a-467">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura</span><span class="sxs-lookup"><span data-stu-id="9969a-467">**FX_WRITE_PROTECT** (0x23) Specified media is write protected</span></span>
- <span data-ttu-id="9969a-468">**FX_FILE _CORRUPT** (0x08) Il file è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-468">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="9969a-469">**FX_SECTOR_INVALID** (0x89) Settore non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-469">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="9969a-470">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="9969a-470">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="9969a-471">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-471">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-472">**FX_MEDIA_INVALID** (0x02) Supporto non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-472">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="9969a-473">**FX_PTR_ERROR** (0x18) Supporto o puntatore di destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-473">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="9969a-474">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-474">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-475">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-475">Allowed From</span></span>

<span data-ttu-id="9969a-476">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-476">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-477">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-477">Example</span></span>

```c
FX_MEDIA     my_media;
UINT         status;
CHAR         entry_name[FX_MAX_LONG_NAME_LEN];
UINT         attributes;
ULONG        size;
UINT         year;
UINT         month;
UINT         day;
UINT         hour;
UINT         minute;
UINT         second;
/* Get the first directory entry in the default directory with full information. */
status = fx_directory_first_full_entry_find(&my_media, entry_name,
    &attributes, &size, &year, &month, &day, &hour, &minute, &second);

/* If status equals FX_SUCCESS, the entry's information is in the local variables. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-478">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-478">See Also</span></span>

- <span data-ttu-id="9969a-479">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-479">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-480">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-480">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-481">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-481">fx_directory_create</span></span>
- <span data-ttu-id="9969a-482">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-482">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-483">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-483">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-484">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-484">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-485">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-485">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-486">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-486">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-487">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-487">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-488">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-488">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-489">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-489">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-490">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-490">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-491">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-491">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-492">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-492">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-493">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-493">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-494">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-494">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-495">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-495">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-496">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-496">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-497">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-497">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-498">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-498">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_information_get"></a><span data-ttu-id="9969a-499">fx_directory_information_get:</span><span class="sxs-lookup"><span data-stu-id="9969a-499">fx_directory_information_get:</span></span>

<span data-ttu-id="9969a-500">Ottiene informazioni sulle voci di directory</span><span class="sxs-lookup"><span data-stu-id="9969a-500">Gets directory entry information</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-501">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-501">Prototype</span></span>

```c
UINT fx_directory_first_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes,
    ULONG *size,
    UINT *year, UINT *month, UINT *day,
    UINT *hour, UINT *minute, UINT *second);
```
### <a name="input-parameters"></a><span data-ttu-id="9969a-502">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-502">Input Parameters</span></span>

- <span data-ttu-id="9969a-503">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-503">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-504">**directory_name:** puntatore al nome della voce di directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-504">**directory_name**: Pointer to name of the directory entry.</span></span>
- <span data-ttu-id="9969a-505">**attributes:** puntatore alla destinazione per gli attributi.</span><span class="sxs-lookup"><span data-stu-id="9969a-505">**attributes**: Pointer to the destination for the attributes.</span></span>
- <span data-ttu-id="9969a-506">**size:** puntatore alla destinazione per le dimensioni.</span><span class="sxs-lookup"><span data-stu-id="9969a-506">**size**: Pointer to the destination for the size.</span></span>
- <span data-ttu-id="9969a-507">**year:** puntatore alla destinazione dell'anno.</span><span class="sxs-lookup"><span data-stu-id="9969a-507">**year**: Pointer to the destination for the year.</span></span>
- <span data-ttu-id="9969a-508">**month:** puntatore alla destinazione del mese.</span><span class="sxs-lookup"><span data-stu-id="9969a-508">**month**: Pointer to the destination for the month.</span></span>
- <span data-ttu-id="9969a-509">**day:** puntatore alla destinazione del giorno.</span><span class="sxs-lookup"><span data-stu-id="9969a-509">**day**: Pointer to the destination for the day.</span></span>
- <span data-ttu-id="9969a-510">**hour:** puntatore alla destinazione per l'ora.</span><span class="sxs-lookup"><span data-stu-id="9969a-510">**hour**: Pointer to the destination for the hour.</span></span>
- <span data-ttu-id="9969a-511">**minute:** puntatore alla destinazione per il minuto.</span><span class="sxs-lookup"><span data-stu-id="9969a-511">**minute**: Pointer to the destination for the minute.</span></span>
- <span data-ttu-id="9969a-512">**second:** puntatore alla destinazione per il secondo.</span><span class="sxs-lookup"><span data-stu-id="9969a-512">**second**: Pointer to the destination for the second.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-513">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-513">Return Values</span></span>

- <span data-ttu-id="9969a-514">**FX_SUCCESS** (0x00) Ricerca della prima voce di directory riuscita</span><span class="sxs-lookup"><span data-stu-id="9969a-514">**FX_SUCCESS** (0x00) Successful first directory entry find</span></span>
- <span data-ttu-id="9969a-515">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-515">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="9969a-516">**FX_NOT_FOUND** (0x04) Directory specificata non trovata nel supporto</span><span class="sxs-lookup"><span data-stu-id="9969a-516">**FX_NOT_FOUND** (0x04) Specified directory was not found in the media</span></span>
- <span data-ttu-id="9969a-517">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90)</span><span class="sxs-lookup"><span data-stu-id="9969a-517">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="9969a-518">**FX_MEDIA_INVALID** (0x02) Supporto non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-518">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="9969a-519">**FX_FILE _CORRUPT** file (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-519">**FX_FILE _CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="9969a-520">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="9969a-520">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="9969a-521">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-521">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-522">**FX_SECTOR_INVALID** (0x89) Settore non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-522">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="9969a-523">**FX_PTR_ERROR** (0x18) Supporto o puntatore di destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-523">**FX_PTR_ERROR** (0x18) Invalid media or destination pointer.</span></span>
- <span data-ttu-id="9969a-524">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-524">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-525">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-525">Allowed From</span></span>

<span data-ttu-id="9969a-526">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-526">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-527">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-527">Example</span></span>

```c
FX_MEDIA     my_media;
UINT         status; attributes; year; month; day;
CHAR         entry_name[FX_MAX_LONG_NAME_LEN];
ULONG        size;
UINT         hour; minute; second;
/* Retrieve information about the directory entry "myfile.txt".*/
status = fx_directory_information_get(&my_media, "myfile.txt", &attributes, &size,
                                      &year, &month, &day,
                                      &hour, &minute, &second);
/* If status equals FX_SUCCESS, the directory entry information is available in the local variables. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-528">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-528">See Also</span></span>

- <span data-ttu-id="9969a-529">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-529">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-530">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-530">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-531">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-531">fx_directory_create</span></span>
- <span data-ttu-id="9969a-532">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-532">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-533">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-533">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-534">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-534">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-535">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-535">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-536">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-536">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-537">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-537">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-538">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-538">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-539">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-539">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-540">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-540">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-541">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-541">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-542">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-542">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-543">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-543">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-544">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-544">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-545">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-545">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-546">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-546">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-547">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-547">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-548">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-548">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_clear"></a><span data-ttu-id="9969a-549">fx_directory_local_path_clear:</span><span class="sxs-lookup"><span data-stu-id="9969a-549">fx_directory_local_path_clear:</span></span>

<span data-ttu-id="9969a-550">Cancella il percorso locale predefinito</span><span class="sxs-lookup"><span data-stu-id="9969a-550">Clears default local path</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-551">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-551">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="9969a-552">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-552">Description</span></span>

<span data-ttu-id="9969a-553">Questo servizio cancella il percorso locale precedente configurato per il thread chiamante.</span><span class="sxs-lookup"><span data-stu-id="9969a-553">This service clears the previous local path set up for the calling thread.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-554">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-554">Input Parameters</span></span>

- <span data-ttu-id="9969a-555">**media_ptr:** puntatore a un supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-555">**media_ptr**: Pointer to a previously opened media.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-556">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-556">Return Values</span></span>

- <span data-ttu-id="9969a-557">**FX_SUCCESS** (0x00) Percorso locale corretto.</span><span class="sxs-lookup"><span data-stu-id="9969a-557">**FX_SUCCESS** (0x00) Successful local path clear.</span></span>
- <span data-ttu-id="9969a-558">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è attualmente aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-558">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="9969a-559">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH definito</span><span class="sxs-lookup"><span data-stu-id="9969a-559">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined</span></span>
- <span data-ttu-id="9969a-560">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-560">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-561">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-561">Allowed From</span></span>

<span data-ttu-id="9969a-562">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-562">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-563">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-563">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
/* Clear the previously setup local path for this media. */
status = fx_directory_local_path_clear(&my_media);
/* If status equals FX_SUCCESS the local path is cleared. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-564">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-564">See Also</span></span>

- <span data-ttu-id="9969a-565">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-565">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-566">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-566">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-567">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-567">fx_directory_create</span></span>
- <span data-ttu-id="9969a-568">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-568">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-569">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-569">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-570">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-570">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-571">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-571">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-572">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-572">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-573">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-573">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-574">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-574">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-575">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-575">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-576">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-576">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-577">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-577">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-578">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-578">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-579">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-579">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-580">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-580">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-581">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-581">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-582">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-582">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-583">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-583">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-584">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-584">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_get"></a><span data-ttu-id="9969a-585">fx_directory_local_path_get:</span><span class="sxs-lookup"><span data-stu-id="9969a-585">fx_directory_local_path_get:</span></span>

<span data-ttu-id="9969a-586">Ottiene la stringa di percorso locale corrente</span><span class="sxs-lookup"><span data-stu-id="9969a-586">Gets the current local path string</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-587">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-587">Prototype</span></span>

```c
UINT fx_directory_local_path_clear(
    FX_MEDIA *media_ptr,
    CHAR **return_path_name);
```

### <a name="description"></a><span data-ttu-id="9969a-588">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-588">Description</span></span>

<span data-ttu-id="9969a-589">Questo servizio restituisce il puntatore del percorso locale del supporto specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-589">This service returns the local path pointer of the specified media.</span></span> <span data-ttu-id="9969a-590">Se non è impostato alcun percorso locale, viene restituito null al chiamante.</span><span class="sxs-lookup"><span data-stu-id="9969a-590">If there is no local path set, a NULL is returned to the caller.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-591">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-591">Input Parameters</span></span>

- <span data-ttu-id="9969a-592">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-592">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-593">**return_path_name:** puntatore al puntatore alla stringa di destinazione per la stringa di percorso locale da archiviare.</span><span class="sxs-lookup"><span data-stu-id="9969a-593">**return_path_name**: Pointer to the destination string pointer for the local path string to be stored.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-594">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-594">Return Values</span></span>

- <span data-ttu-id="9969a-595">**FX_SUCCESS** (0x00) Percorso locale riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-595">**FX_SUCCESS** (0x00) Successful local path get.</span></span>
- <span data-ttu-id="9969a-596">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è attualmente aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-596">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open</span></span>
- <span data-ttu-id="9969a-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="9969a-597">**FX_NOT_IMPLEMENTED** (0x22) NX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="9969a-598">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-598">**FX_PTR_ERROR** (0x18) Invalid media pointer</span></span>


### <a name="allowed-from"></a><span data-ttu-id="9969a-599">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-599">Allowed From</span></span>

<span data-ttu-id="9969a-600">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-600">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-601">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-601">Example</span></span>

```c
FX_MEDIA         my_media;
CHAR             *my_path;
UINT             status;
/* Retrieve the current local path string. */
status = fx_directory_local_path_get(&my_media, &my_path);
/* If status equals FX_SUCCESS, "my_path" points to the local path string. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-602">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-602">See Also</span></span>

- <span data-ttu-id="9969a-603">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-603">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-604">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-604">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-605">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-605">fx_directory_create</span></span>
- <span data-ttu-id="9969a-606">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-606">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-607">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-607">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-608">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-608">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-609">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-609">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-610">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-610">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-611">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-611">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-612">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-612">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-613">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-613">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-614">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-614">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-615">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-615">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-616">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-616">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-617">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-617">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-618">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-618">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-619">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-619">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-620">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-620">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-621">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-621">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-622">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-622">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_restore"></a><span data-ttu-id="9969a-623">fx_directory_local_path_restore:</span><span class="sxs-lookup"><span data-stu-id="9969a-623">fx_directory_local_path_restore:</span></span>

<span data-ttu-id="9969a-624">Ripristina il percorso locale precedente</span><span class="sxs-lookup"><span data-stu-id="9969a-624">Restores previous local path</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-625">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-625">Prototype</span></span>

```c
UINT fx_directory_local_path_restore(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr);
```

### <a name="description"></a><span data-ttu-id="9969a-626">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-626">Description</span></span>

<span data-ttu-id="9969a-627">Questo servizio ripristina un percorso locale impostato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-627">This service restores a previously set local path.</span></span> <span data-ttu-id="9969a-628">Viene ripristinata anche la posizione di ricerca nella directory effettuata in questo percorso locale, che rende questa routine utile negli attraversamenti ricorsivi della directory da parte dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9969a-628">The directory search position made on this local path is also restored, which makes this routine useful in recursive directory traversals by the application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-629">*Ogni percorso locale contiene una stringa di percorso locale **di FX_MAXIMUM_PATH** dimensioni, che per impostazione predefinita è di 256 caratteri. Questa stringa di percorso interna non viene usata da FileX e viene fornita solo per l'uso dell'applicazione. Se **FX_LOCAL_PATH** verrà dichiarata come variabile locale, gli utenti devono fare attenzione all'aumento dello stack in base alle dimensioni di questa struttura. Gli utenti sono invitati a ridurre le dimensioni **del** FX_MAXIMUM_PATH ricompilare l'origine della libreria FileX.*</span><span class="sxs-lookup"><span data-stu-id="9969a-629">*Each local path contains a local path string of **FX_MAXIMUM_PATH** in size, which by default is 256 characters. This internal path string is not used by FileX and is provided only for the application's use. If **FX_LOCAL_PATH** is going to be declared as a local variable, users should beware of the stack growing by the size of this structure. Users are welcome to reduce the size of **FX_MAXIMUM_PATH** and rebuild the FileX library source.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-630">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-630">Input Parameters</span></span>

- <span data-ttu-id="9969a-631">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-631">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-632">**local_path_ptr**: puntatore al percorso locale impostato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-632">**local_path_ptr**: Pointer to the previously set local path.</span></span> <span data-ttu-id="9969a-633">È molto importante assicurarsi che questo puntatore punti effettivamente a un percorso locale usato in precedenza e ancora intatto.</span><span class="sxs-lookup"><span data-stu-id="9969a-633">It's very important to ensure that this pointer does indeed point to a previously used and still intact local path.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-634">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-634">Return Values</span></span>

- <span data-ttu-id="9969a-635">**FX_SUCCESS** (0x00) Ripristino del percorso locale riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-635">**FX_SUCCESS** (0x00) Successful local path restore.</span></span>
- <span data-ttu-id="9969a-636">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-636">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not currently open.</span></span>
- <span data-ttu-id="9969a-637">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH definito.</span><span class="sxs-lookup"><span data-stu-id="9969a-637">**FX_NOT_IMPLEMENTED** (0x22) FX_NO_LCOAL_PATH is defined.</span></span>
- <span data-ttu-id="9969a-638">**FX_PTR_ERROR** (0x18) Supporto o puntatore di percorso locale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-638">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-639">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-639">Allowed From</span></span>

<span data-ttu-id="9969a-640">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-640">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-641">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-641">Example</span></span>

```c
FX_MEDIA                  my_media;
FX_LOCAL_PATH             my_previous_local_path;
UINT                      status;
/* Restore the previous local path. */
status = fx_directory_local_path_restore(&my_media, &my_previous_local_path);
/* If status equals FX_SUCCESS, the previous local path has been restored. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-642">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-642">See Also</span></span>

- <span data-ttu-id="9969a-643">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-643">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-644">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-644">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-645">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-645">fx_directory_create</span></span>
- <span data-ttu-id="9969a-646">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-646">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-647">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-647">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-648">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-648">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-649">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-649">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-650">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-650">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-651">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-651">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-652">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-652">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-653">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-653">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-654">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-654">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-655">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-655">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-656">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-656">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-657">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-657">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-658">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-658">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-659">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-659">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-660">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-660">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-661">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-661">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-662">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-662">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_local_path_set"></a><span data-ttu-id="9969a-663">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-663">fx_directory_local_path_set</span></span>

<span data-ttu-id="9969a-664">Configura un percorso locale specifico del thread</span><span class="sxs-lookup"><span data-stu-id="9969a-664">Sets up a thread-specific local path</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-665">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-665">Prototype</span></span>

```c
UINT fx_directory_local_path_set(
    FX_MEDIA *media_ptr,
    FX_LOCAL_PATH *local_path_ptr,
    CHAR *new_path_name);
```

### <a name="description"></a><span data-ttu-id="9969a-666">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-666">Description</span></span>

<span data-ttu-id="9969a-667">Questo servizio configura un percorso specifico del thread come specificato dal simbolo \***new_path_string** _.</span><span class="sxs-lookup"><span data-stu-id="9969a-667">This service sets up a thread-specific path as specified by the \***new_path_string** _.</span></span> <span data-ttu-id="9969a-668">Al termine di questa routine, le informazioni sul percorso locale archiviate in _ *_local_path_ptr_*\* avranno la precedenza sul percorso multimediale globale per tutte le operazioni su file e directory eseguite da questo thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-668">After successful completion of this routine, the local path information stored in _ *_local_path_ptr_*\* will take precedence over the global media path for all file and directory operations made by this thread.</span></span> <span data-ttu-id="9969a-669">Questa operazione non avrà alcun impatto su altri thread nel sistema</span><span class="sxs-lookup"><span data-stu-id="9969a-669">This will have no impact on any other thread in the system</span></span> 
> [!IMPORTANT]
> <span data-ttu-id="9969a-670">*Le dimensioni predefinite della stringa di percorso locale sono di 256 caratteri. Può essere modificato modificando il FX_MAXIMUM_PATH **in** **fx_api.h** e ricompilando l'intera libreria FileX. Il percorso della stringa di caratteri viene mantenuto per l'applicazione e non viene usato internamente da FileX.*</span><span class="sxs-lookup"><span data-stu-id="9969a-670">*The default size of the local path string is 256 characters; it can be changed by modifying **FX_MAXIMUM_PATH** in **fx_api.h** and rebuilding the entire FileX library. The character string path is maintained for the application and is not used internally by FileX.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-671">*Per i nomi forniti dall'applicazione, FileX supporta sia la barra rovesciata ( ) che la barra (/) per separare directory, sottodirectory e \\ nomi di file. Tuttavia, FileX usa solo il carattere barra rovesciata nei percorsi restituiti all'applicazione.*</span><span class="sxs-lookup"><span data-stu-id="9969a-671">*For names supplied by the application, FileX supports both backslash (\\) and forward slash (/) characters to separate directories, subdirectories, and file names. However, FileX only uses the backslash character in paths returned to the application.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-672">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-672">Input Parameters</span></span>

- <span data-ttu-id="9969a-673">**media_ptr**: puntatore al supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-673">**media_ptr**: Pointer to the previously opened media.</span></span>
- <span data-ttu-id="9969a-674">**local_path_ptr**: destinazione per contenere le informazioni sul percorso locale specifico del thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-674">**local_path_ptr**: Destination for holding the thread-specific local path information.</span></span> <span data-ttu-id="9969a-675">L'indirizzo di questa struttura può essere fornito alla funzione di ripristino del percorso locale in futuro.</span><span class="sxs-lookup"><span data-stu-id="9969a-675">The address of this structure may be supplied to the local path restore function in the future.</span></span>
- <span data-ttu-id="9969a-676">**new_path_name**: specifica il percorso locale da configurare.</span><span class="sxs-lookup"><span data-stu-id="9969a-676">**new_path_name**: Specifies the local path to setup.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-677">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-677">Return Values</span></span>

- <span data-ttu-id="9969a-678">**FX_SUCCESS** (0x00) Set di directory predefinito riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-678">**FX_SUCCESS** (0x00) Successful default directory set.</span></span>
- <span data-ttu-id="9969a-679">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-679">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-680">**FX_NOT_IMPLEMENTED** (0x22) \*\*FX_NO_LCOAL_PATH</span><span class="sxs-lookup"><span data-stu-id="9969a-680">**FX_NOT_IMPLEMENTED** (0x22) \*\*FX_NO_LCOAL_PATH</span></span>
- <span data-ttu-id="9969a-681">**FX_INVALID_PATH** (0x0D) Non è stato possibile trovare la nuova directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-681">**FX_INVALID_PATH** (0x0D) New directory could not be found.</span></span>
- <span data-ttu-id="9969a-682">**FX_NOT_IMPLEMENTED** (0x22) - \*\*FX_NO_LOCAL_PATH definito.</span><span class="sxs-lookup"><span data-stu-id="9969a-682">**FX_NOT_IMPLEMENTED** (0x22)- \*\*FX_NO_LOCAL_PATH is defined.</span></span>
- <span data-ttu-id="9969a-683">**FX_PTR_ERROR** (0x18) Supporto o puntatore di percorso locale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-683">**FX_PTR_ERROR** (0x18) Invalid media or local path pointer.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-684">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-684">Allowed From</span></span>

<span data-ttu-id="9969a-685">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-685">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-686">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-686">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;
FX_LOCAL_PATH     my_previous_local_path;
/* Set the local path to \abc\def\ghi. */
status = fx_directory_local_path_set (&my_media,&local_path,"\\abc\\def\\ghi");

/* If status equals FX_SUCCESS, the default directory for this thread
is \abc\def\ghi. All subsequent file operations that do not explicitly
specify a path will default to this directory. Note that the character
"\" serves as an escape character in a string. To represent the
character "\", use the construct "\\".*/
```

### <a name="see-also"></a><span data-ttu-id="9969a-687">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-687">See Also</span></span>

- <span data-ttu-id="9969a-688">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-688">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-689">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-689">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-690">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-690">fx_directory_create</span></span>
- <span data-ttu-id="9969a-691">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-691">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-692">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-692">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-693">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-693">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-694">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-694">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-695">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-695">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-696">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-696">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-697">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-697">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-698">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-698">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-699">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-699">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-700">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-700">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-701">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-701">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-702">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-702">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-703">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-703">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-704">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-704">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-705">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-705">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-706">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-706">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-707">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-707">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get"></a><span data-ttu-id="9969a-708">fx_directory_long_name_get:</span><span class="sxs-lookup"><span data-stu-id="9969a-708">fx_directory_long_name_get:</span></span>

<span data-ttu-id="9969a-709">Ottiene il nome lungo dal nome breve</span><span class="sxs-lookup"><span data-stu-id="9969a-709">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-710">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-710">Prototype</span></span>

```c
UINT fx_directory_long_name_get(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name);
```

### <a name="description"></a><span data-ttu-id="9969a-711">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-711">Description</span></span>

<span data-ttu-id="9969a-712">Questo servizio recupera il nome lungo (se presente) associato al nome breve (formato 8.3) fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-712">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="9969a-713">Il nome breve può essere un nome di file o un nome di directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-713">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-714">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-714">Input Parameters</span></span>

- <span data-ttu-id="9969a-715">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-715">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-716">**short_name:** puntatore al nome breve di origine (formato 8.3).</span><span class="sxs-lookup"><span data-stu-id="9969a-716">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="9969a-717">**long_name:** puntatore alla destinazione per il nome lungo.</span><span class="sxs-lookup"><span data-stu-id="9969a-717">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="9969a-718">Se non è presente alcun nome lungo, viene restituito il nome breve.</span><span class="sxs-lookup"><span data-stu-id="9969a-718">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="9969a-719">Si noti che la destinazione per il nome lungo deve essere sufficientemente grande da contenere FX_MAX_LONG_NAME_LEN caratteri.</span><span class="sxs-lookup"><span data-stu-id="9969a-719">Note that the destination for the long name must be large enough to hold FX_MAX_LONG_NAME_LEN characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-720">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-720">Return Values</span></span>

- <span data-ttu-id="9969a-721">**FX_SUCCESS** (0x00) Successful long name get</span><span class="sxs-lookup"><span data-stu-id="9969a-721">**FX_SUCCESS** (0x00) Successful long name get</span></span>
- <span data-ttu-id="9969a-722">**FX_NOT_FOUND** (0x04) Nome breve non trovato</span><span class="sxs-lookup"><span data-stu-id="9969a-722">**FX_NOT_FOUND** (0x04) Short name was not found</span></span>
- <span data-ttu-id="9969a-723">**FX_IO_ERROR** di I/O del driver 0x90 (0x90)</span><span class="sxs-lookup"><span data-stu-id="9969a-723">**FX_IO_ERROR** (0x90) Driver I/O error</span></span>
- <span data-ttu-id="9969a-724">**FX_MEDIA_INVALID** (0x02) Supporti non validi</span><span class="sxs-lookup"><span data-stu-id="9969a-724">**FX_MEDIA_INVALID** (0x02) Invalid media</span></span>
- <span data-ttu-id="9969a-725">**FX_FILE_CORRUPT** file (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-725">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="9969a-726">**FX_SECTOR_INVALID** (0x89) Settore non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-726">**FX_SECTOR_INVALID** (0x89) Invalid sector</span></span>
- <span data-ttu-id="9969a-727">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT</span><span class="sxs-lookup"><span data-stu-id="9969a-727">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry</span></span>
- <span data-ttu-id="9969a-728">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-728">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-729">**FX_PTR_ERROR** (0x18) Supporto o puntatore del nome non valido</span><span class="sxs-lookup"><span data-stu-id="9969a-729">**FX_PTR_ERROR** (0x18) Invalid media or name pointer</span></span>
- <span data-ttu-id="9969a-730">**FX_CALLER_ERROR** (0x20) Caller non è un thread</span><span class="sxs-lookup"><span data-stu-id="9969a-730">**FX_CALLER_ERROR** (0x20) Caller is not a thread</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-731">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-731">Allowed From</span></span>

<span data-ttu-id="9969a-732">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-732">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-733">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-733">Example</span></span>

```c
FX_MEDIA            my_media;
UCHAR               my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */
status = fx_directory_long_name_get(&my_media, "TEXT~01.TXT", my_long_name);
/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-734">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-734">See Also</span></span>

- <span data-ttu-id="9969a-735">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-735">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-736">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-736">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-737">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-737">fx_directory_create</span></span>
- <span data-ttu-id="9969a-738">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-738">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-739">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-739">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-740">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-740">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-741">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-741">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-742">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-742">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-743">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-743">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-744">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-744">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-745">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-745">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-746">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-746">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-747">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-747">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-748">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-748">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-749">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-749">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-750">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-750">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-751">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-751">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-752">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-752">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-753">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-753">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-754">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-754">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_long_name_get_extended"></a><span data-ttu-id="9969a-755">fx_directory_long_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="9969a-755">fx_directory_long_name_get_extended</span></span>

<span data-ttu-id="9969a-756">Ottiene il nome lungo dal nome breve</span><span class="sxs-lookup"><span data-stu-id="9969a-756">Gets long name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-757">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-757">Prototype</span></span>

```c
UINT fx_directory_long_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *short_name,
    CHAR *long_name,
    UINT long_file_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="9969a-758">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-758">Description</span></span>

<span data-ttu-id="9969a-759">Questo servizio recupera il nome lungo (se presente) associato al nome breve (formato 8.3) fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-759">This service retrieves the long name (if any) associated with the supplied short (8.3 format) name.</span></span> <span data-ttu-id="9969a-760">Il nome breve può essere un nome di file o un nome di directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-760">The short name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-761">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-761">Input Parameters</span></span>

- <span data-ttu-id="9969a-762">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-762">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-763">**short_name:** puntatore al nome breve di origine (formato 8.3).</span><span class="sxs-lookup"><span data-stu-id="9969a-763">**short_name**: Pointer to source short name (8.3 format).</span></span>
- <span data-ttu-id="9969a-764">**long_name:** puntatore alla destinazione per il nome lungo.</span><span class="sxs-lookup"><span data-stu-id="9969a-764">**long_name**: Pointer to destination for the long name.</span></span> <span data-ttu-id="9969a-765">Se non è presente alcun nome lungo, viene restituito il nome breve.</span><span class="sxs-lookup"><span data-stu-id="9969a-765">If there is no long name, the short name is returned.</span></span> <span data-ttu-id="9969a-766">Nota: la destinazione per il nome lungo deve essere sufficientemente grande da contenere **FX_MAX_LONG_NAME_LEN** caratteri.</span><span class="sxs-lookup"><span data-stu-id="9969a-766">Note: Destination for the long name must be large enough to hold **FX_MAX_LONG_NAME_LEN** characters.</span></span>
- <span data-ttu-id="9969a-767">**long_file_name_buffer_length**: lunghezza del buffer dei nomi lunghi.</span><span class="sxs-lookup"><span data-stu-id="9969a-767">**long_file_name_buffer_length**: Length of the long name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-768">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-768">Return Values</span></span>

- <span data-ttu-id="9969a-769">**FX_SUCCESS** (0x00) Get nome lungo riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-769">**FX_SUCCESS** (0x00) Successful long name get.</span></span>
- <span data-ttu-id="9969a-770">**FX_NOT_FOUND** (0x04) Nome breve non trovato.</span><span class="sxs-lookup"><span data-stu-id="9969a-770">**FX_NOT_FOUND** (0x04) Short name was not found.</span></span>
- <span data-ttu-id="9969a-771">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-771">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-772">**FX_MEDIA_INVALID** (0x02) Supporto non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-772">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="9969a-773">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-773">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-774">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-774">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-775">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-775">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-776">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="9969a-776">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="9969a-777">**FX_PTR_ERROR** (0x18) Supporto o puntatore del nome non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-777">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="9969a-778">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-778">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-779">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-779">Allowed From</span></span>

<span data-ttu-id="9969a-780">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-780">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-781">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-781">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_long_name[FX_MAX_LONG_NAME_LEN];
/* Retrieve the long name associated with "TEXT~01.TXT". */

status = fx_directory_long_name_get_extended(&my_media,
    "TEXT~01.TXT", my_long_name), sizeof(my_long_name));

/* If status is FX_SUCCESS the long name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-782">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-782">See Also</span></span>

- <span data-ttu-id="9969a-783">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-783">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-784">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-784">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-785">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-785">fx_directory_create</span></span>
- <span data-ttu-id="9969a-786">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-786">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-787">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-787">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-788">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-788">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-789">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-789">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-790">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-790">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-791">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-791">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-792">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-792">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-793">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-793">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-794">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-794">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-795">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-795">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-796">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-796">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-797">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-797">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-798">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-798">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-799">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-799">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-800">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-800">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-801">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-801">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-802">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-802">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_name_test"></a><span data-ttu-id="9969a-803">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-803">fx_directory_name_test</span></span>

<span data-ttu-id="9969a-804">Test per la directory</span><span class="sxs-lookup"><span data-stu-id="9969a-804">Tests for directory</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-805">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-805">Prototype</span></span>

```c
UINT fx_directory_name_test(
    FX_MEDIA *media_ptr,
    CHAR *directory_name);
```

### <a name="description"></a><span data-ttu-id="9969a-806">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-806">Description</span></span>

<span data-ttu-id="9969a-807">Questo servizio verifica se il nome fornito è o meno una directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-807">This service tests whether or not the supplied name is a directory.</span></span> <span data-ttu-id="9969a-808">In tal caso, viene restituito FX_SUCCESS valore.</span><span class="sxs-lookup"><span data-stu-id="9969a-808">If so, a FX_SUCCESS is returned.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-809">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-809">Input Parameters</span></span>

- <span data-ttu-id="9969a-810">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-810">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-811">**directory_name**: puntatore al nome della voce di directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-811">**directory_name**: Pointer to name of the directory entry.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-812">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-812">Return Values</span></span>

- <span data-ttu-id="9969a-813">**FX_SUCCESS** (0x00) Nome fornito è una directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-813">**FX_SUCCESS** (0x00) Supplied name is a directory.</span></span>
- <span data-ttu-id="9969a-814">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto</span><span class="sxs-lookup"><span data-stu-id="9969a-814">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open</span></span>
- <span data-ttu-id="9969a-815">**FX_NOT_FOUND** impossibile trovare 0x04 directory (0x04).</span><span class="sxs-lookup"><span data-stu-id="9969a-815">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="9969a-816">**FX_NOT_DIRECTORY** (0x0E) non è una directory</span><span class="sxs-lookup"><span data-stu-id="9969a-816">**FX_NOT_DIRECTORY** (0x0E)  Entry is not a directory</span></span>
- <span data-ttu-id="9969a-817">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-817">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-818">**FX_MEDIA_INVALID** (0x02) Supporto non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-818">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="9969a-819">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-819">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-820">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-820">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-821">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-821">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-822">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="9969a-822">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="9969a-823">**FX_PTR_ERROR** (0x18) Supporto o puntatore del nome non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-823">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="9969a-824">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-824">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-825">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-825">Allowed From</span></span>

<span data-ttu-id="9969a-826">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-826">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-827">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-827">Example</span></span>

```c
FX_MEDIA        my_media;
UNIT             status;
/* Check to see if the name "abc" is directory */

status = fx_directory_name_test(&my_media, "abc");

/* If status equals FX_SUCCESS "abc" is a directory. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-828">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-828">See Also</span></span>

- <span data-ttu-id="9969a-829">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-829">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-830">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-830">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-831">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-831">fx_directory_create</span></span>
- <span data-ttu-id="9969a-832">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-832">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-833">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-833">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-834">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-834">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-835">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-835">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-836">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-836">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-837">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-837">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-838">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-838">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-839">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-839">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-840">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-840">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-841">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-841">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-842">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-842">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-843">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-843">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-844">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-844">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-845">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-845">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-846">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-846">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-847">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-847">fx_unicode_directory_create</span></span>

## <a name="fx_directory_next_entry_find"></a><span data-ttu-id="9969a-848">fx_directory_next_entry_find:</span><span class="sxs-lookup"><span data-stu-id="9969a-848">fx_directory_next_entry_find:</span></span>

<span data-ttu-id="9969a-849">Preleva la voce di directory successiva</span><span class="sxs-lookup"><span data-stu-id="9969a-849">Picks up next directory entry</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-850">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-850">Prototype</span></span>

```c
UINT fx_directory_next_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *return_entry_name);
```

### <a name="description"></a><span data-ttu-id="9969a-851">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-851">Description</span></span>

<span data-ttu-id="9969a-852">Questo servizio restituisce il nome della voce successiva nella directory predefinita corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-852">This service returns the next entry name in the current default directory.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-853">*Se si usa un percorso non locale, è anche importante impedire (con un livello di priorità threadX o semaforo thread) che altri thread dell'applicazione cambino questa directory durante l'attraversamento di una directory. In caso contrario, è possibile ottenere risultati non validi.*</span><span class="sxs-lookup"><span data-stu-id="9969a-853">*If using a non-local path, it is also important to prevent (with a ThreadX semaphore or thread priority level) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-854">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-854">Input Parameters</span></span>

- <span data-ttu-id="9969a-855">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-855">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-856">**return_entry_name**: puntatore alla destinazione per il nome della voce successiva nella directory predefinita.</span><span class="sxs-lookup"><span data-stu-id="9969a-856">**return_entry_name**: Pointer to destination for the next entry name in the default directory.</span></span> <span data-ttu-id="9969a-857">Il buffer a cui punta questo puntatore deve essere sufficientemente grande da contenere la dimensione massima del nome FileX, definita **_da FX_MAX_LONG_NAME_LEN_**.</span><span class="sxs-lookup"><span data-stu-id="9969a-857">The buffer this pointer points to must be large enough to hold the maximum size of FileX name, defined by **_FX_MAX_LONG_NAME_LEN_**.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-858">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-858">Return Values</span></span>

- <span data-ttu-id="9969a-859">**FX_SUCCESS** (0x00) Ricerca voce successiva riuscita</span><span class="sxs-lookup"><span data-stu-id="9969a-859">**FX_SUCCESS** (0x00) Successful next entry find</span></span>
- <span data-ttu-id="9969a-860">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-860">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-861">**FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-861">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="9969a-862">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-862">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-863">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-863">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-864">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-864">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-865">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-865">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-866">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-866">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-867">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-867">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="9969a-868">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-868">**FX_CALLER_ERROR** (0x20)     Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-869">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-869">Allowed From</span></span>

<span data-ttu-id="9969a-870">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-870">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-871">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-871">Example</span></span>

```c
FX_MEDIA        my_media;
CHAR            next_name[FX_MAX_LONG_NAME_LEN];
UINT            status;

/* Retrieve the next entry in the default directory. */

status = fx_directory_next_entry_find(&my_media, next_name);

/* If status equals TX_SUCCESS, the name of the next directory entry is in "next_name". */
```

### <a name="see-also"></a><span data-ttu-id="9969a-872">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-872">See Also</span></span>

- <span data-ttu-id="9969a-873">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-873">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-874">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-874">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-875">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-875">fx_directory_create</span></span>
- <span data-ttu-id="9969a-876">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-876">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-877">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-877">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-878">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-878">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-879">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-879">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-880">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-880">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-881">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-881">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-882">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-882">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-883">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-883">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-884">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-884">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-885">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-885">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-886">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-886">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-887">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-887">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-888">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-888">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-889">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-889">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-890">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-890">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-891">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-891">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-892">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-892">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_next_full_entry_find"></a><span data-ttu-id="9969a-893">fx_directory_next_full_entry_find:</span><span class="sxs-lookup"><span data-stu-id="9969a-893">fx_directory_next_full_entry_find:</span></span>

<span data-ttu-id="9969a-894">Ottiene la voce di directory successiva con informazioni complete</span><span class="sxs-lookup"><span data-stu-id="9969a-894">Gets next directory entry with full information</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-895">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-895">Prototype</span></span>

```c
UINT fx_directory_next_full_entry_find(
    FX_MEDIA *media_ptr,
    CHAR *directory_name,
    UINT *attributes, 
    ULONG *size,
    UINT *year, 
    UINT *month, 
    UINT *day,
    UINT *hour, 
    UINT *minute, 
    UINT *second);
```

### <a name="description"></a><span data-ttu-id="9969a-896">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-896">Description</span></span>

<span data-ttu-id="9969a-897">Questo servizio recupera il nome della voce successiva nella directory predefinita e lo copia nella destinazione specificata.</span><span class="sxs-lookup"><span data-stu-id="9969a-897">This service retrieves the next entry name in the default directory and copies it to the specified destination.</span></span> <span data-ttu-id="9969a-898">Restituisce anche informazioni complete sulla voce come specificato dai parametri di input aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="9969a-898">It also returns full information about the entry as specified by the additional input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-899">\*La destinazione specificata deve essere sufficientemente grande da contenere il nome FileX di dimensioni massime, come definito da \*\*\*FX_MAX_LONG_NAME_LEN\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="9969a-899">\*The specified destination must be large enough to hold the maximum sized FileX name, as defined by \*\*\*FX_MAX_LONG_NAME_LEN\*\*\*\*</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-900">*Se si usa un percorso non locale, è importante impedire agli altri thread dell'applicazione di modificare questa directory (con un semaforo ThreadX, un mutex o una modifica del livello di priorità) mentre è in corso un attraversamento della directory. In caso contrario, è possibile ottenere risultati non validi.*</span><span class="sxs-lookup"><span data-stu-id="9969a-900">*If using a non-local path, it is important to prevent (with a ThreadX semaphore, mutex, or priority level change) other application threads from changing this directory while a directory traversal is taking place. Otherwise, invalid results may be obtained.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-901">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-901">Input Parameters</span></span>

- <span data-ttu-id="9969a-902">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-902">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-903">**directory_name**: puntatore alla destinazione per il nome di una voce di directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-903">**directory_name**: Pointer to the destination for the name of a directory entry.</span></span> <span data-ttu-id="9969a-904">Deve essere grande almeno quanto **FX_MAX_LONG_NAME_LEN**.</span><span class="sxs-lookup"><span data-stu-id="9969a-904">Must be at least as big as **FX_MAX_LONG_NAME_LEN**.</span></span>
- <span data-ttu-id="9969a-905">**attributes:** se non Null, puntatore alla destinazione per gli attributi della voce da inserire. Gli attributi vengono restituiti in un formato mappa di bit con le impostazioni possibili seguenti:</span><span class="sxs-lookup"><span data-stu-id="9969a-905">**attributes**: If non-null, pointer to the destination for the entry's attributes to be placed.The attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="9969a-906">**FX_READ_ONLY** (0x01)</span><span class="sxs-lookup"><span data-stu-id="9969a-906">**FX_READ_ONLY** (0x01)</span></span>
  - <span data-ttu-id="9969a-907">**FX_HIDDEN** (0x02)</span><span class="sxs-lookup"><span data-stu-id="9969a-907">**FX_HIDDEN** (0x02)</span></span>
  - <span data-ttu-id="9969a-908">**FX_SYSTEM** (0x04)</span><span class="sxs-lookup"><span data-stu-id="9969a-908">**FX_SYSTEM** (0x04)</span></span>
  - <span data-ttu-id="9969a-909">**FX_VOLUME** (0x08)</span><span class="sxs-lookup"><span data-stu-id="9969a-909">**FX_VOLUME** (0x08)</span></span>
  - <span data-ttu-id="9969a-910">**FX_DIRECTORY** (0x10)</span><span class="sxs-lookup"><span data-stu-id="9969a-910">**FX_DIRECTORY** (0x10)</span></span>
  - <span data-ttu-id="9969a-911">**FX_ARCHIVE** (0x20)</span><span class="sxs-lookup"><span data-stu-id="9969a-911">**FX_ARCHIVE** (0x20)</span></span>
- <span data-ttu-id="9969a-912">**size:** se non Null, puntatore alla destinazione per le dimensioni della voce in byte.</span><span class="sxs-lookup"><span data-stu-id="9969a-912">**size**: If non-null, pointer to the destination for the entry's size in bytes.</span></span>
- <span data-ttu-id="9969a-913">**month:** se non Null, puntatore alla destinazione per il mese di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-913">**month**: If non-null, pointer to the destination for the entry's month of modification.</span></span>
- <span data-ttu-id="9969a-914">**year:** se non Null, puntatore alla destinazione per l'anno di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-914">**year**: If non-null, pointer to the destination for the entry's year of modification.</span></span>
- <span data-ttu-id="9969a-915">**day:** se non Null, puntatore alla destinazione per il giorno di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-915">**day**: If non-null, pointer to the destination for the entry's day of modification.</span></span>
- <span data-ttu-id="9969a-916">**hour:** se non Null, puntatore alla destinazione per l'ora di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-916">**hour**: If non-null, pointer to the destination for the entry's hour of modification.</span></span>
- <span data-ttu-id="9969a-917">**minute:** se non Null, puntatore alla destinazione per il minuto di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-917">**minute**: If non-null, pointer to the destination for the entry's minute of modification.</span></span>
- <span data-ttu-id="9969a-918">**second:** se non Null, puntatore alla destinazione per il secondo di modifica della voce.</span><span class="sxs-lookup"><span data-stu-id="9969a-918">**second**: If non-null, pointer to the destination for the entry's second of modification.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-919">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-919">Return Values</span></span>

- <span data-ttu-id="9969a-920">**FX_SUCCESS** (0x00) Ricerca della voce successiva nella directory riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-920">**FX_SUCCESS** (0x00) Successful directory next entry find.</span></span>
- <span data-ttu-id="9969a-921">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-921">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-922">**FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-922">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="9969a-923">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-923">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-924">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-924">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-925">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-925">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-926">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-926">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-927">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="9969a-927">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="9969a-928">**FX_MEDIA_INVALID** (0x02) Supporto non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-928">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="9969a-929">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido o tutti i parametri di input sono NULL.</span><span class="sxs-lookup"><span data-stu-id="9969a-929">**FX_PTR_ERROR** (0x18) Invalid media pointer or all input parameters are NULL.</span></span>
- <span data-ttu-id="9969a-930">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-930">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-931">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-931">Allowed From</span></span>

<span data-ttu-id="9969a-932">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-932">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-933">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-933">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
CHAR        entry_name[FX_MAX_LONG_NAME_LEN];
UINT        attributes;
ULONG       size;
UINT        year;
UINT        month;
UINT        day;
UINT        hour;
UINT        minute;
UINT        second;

/* Get the next directory entry in the default directory with full information. */
status = fx_directory_next_full_entry_find(&my_media, entry_name, &attributes, &size,
                                           &year, &month, &day,
                                           &hour, &minute, &second);

/* If status equals FX_SUCCESS, the entry's information is in the local variables. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-934">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-934">See Also</span></span>

- <span data-ttu-id="9969a-935">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-935">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-936">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-936">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-937">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-937">fx_directory_create</span></span>
- <span data-ttu-id="9969a-938">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-938">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-939">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-939">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-940">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-940">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-941">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-941">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-942">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-942">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-943">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-943">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-944">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-944">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-945">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-945">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-946">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-946">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-947">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-947">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-948">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-948">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-949">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-949">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-950">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-950">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-951">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-951">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-952">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-952">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-953">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-953">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-954">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-954">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_rename"></a><span data-ttu-id="9969a-955">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-955">fx_directory_rename</span></span>

<span data-ttu-id="9969a-956">Rinomina la directory</span><span class="sxs-lookup"><span data-stu-id="9969a-956">Renames directory</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-957">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-957">Prototype</span></span>

```c
UINT fx_directory_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_directory_name,
    CHAR *new_directory_name);
```

### <a name="description"></a><span data-ttu-id="9969a-958">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-958">Description</span></span>

<span data-ttu-id="9969a-959">Questo servizio modifica il nome della directory con il nuovo nome di directory specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-959">This service changes the directory name to the specified new directory name.</span></span> <span data-ttu-id="9969a-960">La ridenominazione viene eseguita anche in relazione al percorso specificato o al percorso predefinito.</span><span class="sxs-lookup"><span data-stu-id="9969a-960">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="9969a-961">Se viene specificato un percorso nel nuovo nome di directory, la directory rinominata viene spostata nel percorso specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-961">If a path is specified in the new directory name, the renamed directory is effectively moved to the specified path.</span></span> <span data-ttu-id="9969a-962">Se non viene specificato alcun percorso, la directory rinominata viene inserita nel percorso predefinito corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-962">If no path is specified, the renamed directory is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-963">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-963">Input Parameters</span></span>

- <span data-ttu-id="9969a-964">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-964">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-965">**old_directory_name:** puntatore al nome della directory corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-965">**old_directory_name**: Pointer to current directory name.</span></span>
- <span data-ttu-id="9969a-966">**new_directory_name:** puntatore al nome della nuova directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-966">**new_directory_name**: Pointer to new directory name.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-967">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-967">Return Values</span></span>

- <span data-ttu-id="9969a-968">**FX_SUCCESS** (0x00) Ridenominazione della directory completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-968">**FX_SUCCESS** (0x00) Successful directory rename.</span></span>
- <span data-ttu-id="9969a-969">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-969">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-970">**FX_NOT_FOUND** (0x04) Impossibile trovare la voce della directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-970">**FX_NOT_FOUND** (0x04) Directory entry could not be found.</span></span>
- <span data-ttu-id="9969a-971">**FX_NOT_DIRECTORY** (0x0E) Entry non è una directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-971">**FX_NOT_DIRECTORY** (0x0E) Entry is not a directory.</span></span>
- <span data-ttu-id="9969a-972">**FX_INVALID_NAME** (0x0C) Il nuovo nome di directory non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-972">**FX_INVALID_NAME** (0x0C) New directory name is invalid.</span></span>
- <span data-ttu-id="9969a-973">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-973">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-974">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-974">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-975">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-975">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-976">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-976">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-977">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-977">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-978">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="9969a-978">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="9969a-979">**FX_MEDIA_INVALID** (0x02) Supporto non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-979">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="9969a-980">**FX_NO_MORE_ENTRIES** (0x0F) Non sono presenti altre voci in questa directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-980">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in this directory.</span></span>
- <span data-ttu-id="9969a-981">**FX_INVALID_PATH** (0x0D) Percorso non valido specificato con il nome della directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-981">**FX_INVALID_PATH** (0x0D) Invalid path supplied with directory name.</span></span>
- <span data-ttu-id="9969a-982">**FX_ALREADY_CREATED** (0x0B) Directory specificata già creata.</span><span class="sxs-lookup"><span data-stu-id="9969a-982">**FX_ALREADY_CREATED** (0x0B) Specified directory was already created.</span></span>
- <span data-ttu-id="9969a-983">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-983">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="9969a-984">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-984">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-985">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-985">Allowed From</span></span>

<span data-ttu-id="9969a-986">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-986">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-987">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-987">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Change the directory "abc" to "def". */
status = fx_directory_rename(&my_media, "abc", "def");

/* If status equals FX_SUCCESS, the directory was changed to "def". */
```

### <a name="see-also"></a><span data-ttu-id="9969a-988">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-988">See Also</span></span>

- <span data-ttu-id="9969a-989">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-989">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-990">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-990">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-991">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-991">fx_directory_create</span></span>
- <span data-ttu-id="9969a-992">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-992">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-993">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-993">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-994">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-994">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-995">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-995">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-996">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-996">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-997">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-997">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-998">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-998">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-999">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-999">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-1000">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-1000">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-1001">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1001">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-1002">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1002">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-1003">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-1003">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-1004">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-1004">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-1005">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-1005">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-1006">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1006">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-1007">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1007">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-1008">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1008">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get"></a><span data-ttu-id="9969a-1009">fx_directory_short_name_get:</span><span class="sxs-lookup"><span data-stu-id="9969a-1009">fx_directory_short_name_get:</span></span>

<span data-ttu-id="9969a-1010">Ottiene il nome breve da un nome lungo</span><span class="sxs-lookup"><span data-stu-id="9969a-1010">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1011">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1011">Prototype</span></span>

```c
UINT fx_directory_short_name_get(
    FX_MEDIA *media_ptr,
    CHAR *long_name, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="9969a-1012">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1012">Description</span></span>

<span data-ttu-id="9969a-1013">Questo servizio recupera il nome breve (formato 8.3) associato al nome lungo fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-1013">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="9969a-1014">Il nome lungo può essere un nome file o un nome di directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-1014">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1015">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1015">Input Parameters</span></span>

- <span data-ttu-id="9969a-1016">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-1016">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-1017">**long_name:** puntatore al nome long di origine.</span><span class="sxs-lookup"><span data-stu-id="9969a-1017">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="9969a-1018">**short_name:** puntatore al nome breve di destinazione (formato 8.3).</span><span class="sxs-lookup"><span data-stu-id="9969a-1018">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="9969a-1019">Si noti che la destinazione per il nome breve deve essere sufficientemente grande da contenere 14 caratteri.</span><span class="sxs-lookup"><span data-stu-id="9969a-1019">Note that the destination for the short name must be large enough to hold 14 characters.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1020">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1020">Return Values</span></span>

- <span data-ttu-id="9969a-1021">**FX_SUCCESS** (0x00) Ottiene il nome breve riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-1021">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="9969a-1022">**FX_NOT_FOUND** (0x04) Nome lungo non trovato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1022">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="9969a-1023">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1023">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1024">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1024">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-1025">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1025">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1026">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1026">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1027">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1027">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1028">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-1028">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-1029">**FX_MEDIA_INVALID** (0x02) Supporto non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1029">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="9969a-1030">**FX_PTR_ERROR** (0x18) Supporto non valido o puntatore al nome.</span><span class="sxs-lookup"><span data-stu-id="9969a-1030">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="9969a-1031">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1031">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1032">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1032">Allowed From</span></span>

<span data-ttu-id="9969a-1033">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1033">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1034">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1034">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get(&my_media,
    "my_really_long_name", my_short_name);

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1035">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1035">See Also</span></span>

- <span data-ttu-id="9969a-1036">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1036">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-1037">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1037">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-1038">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1038">fx_directory_create</span></span>
- <span data-ttu-id="9969a-1039">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1039">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-1040">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1040">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-1041">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1041">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-1042">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-1042">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-1043">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-1043">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-1044">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1044">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-1045">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-1045">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-1046">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1046">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-1047">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-1047">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-1048">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1048">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-1049">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1049">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-1050">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-1050">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-1051">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-1051">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-1052">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-1052">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-1053">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1053">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-1054">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1054">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-1055">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1055">fx_unicode_directory_rename</span></span>

## <a name="fx_directory_short_name_get_extended"></a><span data-ttu-id="9969a-1056">fx_directory_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="9969a-1056">fx_directory_short_name_get_extended</span></span>

<span data-ttu-id="9969a-1057">Ottiene il nome breve da un nome lungo</span><span class="sxs-lookup"><span data-stu-id="9969a-1057">Gets short name from a long name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1058">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1058">Prototype</span></span>

```csharp
UINT fx_directory_short_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *long_name,
    CHAR *short_name,
    UINT short_file_name_length);
```

### <a name="description"></a><span data-ttu-id="9969a-1059">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1059">Description</span></span>

<span data-ttu-id="9969a-1060">Questo servizio recupera il nome breve (formato 8.3) associato al nome lungo fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-1060">This service retrieves the short (8.3 format) name associated with the supplied long name.</span></span> <span data-ttu-id="9969a-1061">Il nome lungo può essere un nome file o un nome di directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-1061">The long name can be either a file name or a directory name.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1062">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1062">Input Parameters</span></span>

- <span data-ttu-id="9969a-1063">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-1063">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-1064">**long_name:** puntatore al nome long di origine.</span><span class="sxs-lookup"><span data-stu-id="9969a-1064">**long_name**: Pointer to source long name.</span></span>
- <span data-ttu-id="9969a-1065">**short_name:** puntatore al nome breve di destinazione (formato 8.3).</span><span class="sxs-lookup"><span data-stu-id="9969a-1065">**short_name**: Pointer to destination short name (8.3 format).</span></span> <span data-ttu-id="9969a-1066">Nota: la destinazione per il nome breve deve essere sufficientemente grande da contenere 14 caratteri.</span><span class="sxs-lookup"><span data-stu-id="9969a-1066">Note: Destination for the short name must be large enough to hold 14 characters.</span></span>
- <span data-ttu-id="9969a-1067">**short_file_name_length**: lunghezza del buffer dei nomi brevi.</span><span class="sxs-lookup"><span data-stu-id="9969a-1067">**short_file_name_length**: Length of short name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1068">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1068">Return Values</span></span>

- <span data-ttu-id="9969a-1069">**FX_SUCCESS** (0x00) Ottiene il nome breve riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-1069">**FX_SUCCESS** (0x00) Successful short name get.</span></span>
- <span data-ttu-id="9969a-1070">**FX_NOT_FOUND** (0x04) Nome lungo non trovato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1070">**FX_NOT_FOUND** (0x04) Long name was not found.</span></span>
- <span data-ttu-id="9969a-1071">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1071">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1072">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1072">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-1073">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1074">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1075">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1075">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1076">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-1076">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-1077">**FX_MEDIA_INVALID** (0x02) Supporto non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1077">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="9969a-1078">**FX_PTR_ERROR** (0x18) Supporto non valido o puntatore al nome.</span><span class="sxs-lookup"><span data-stu-id="9969a-1078">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="9969a-1079">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1079">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1080">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1080">Allowed From</span></span>

<span data-ttu-id="9969a-1081">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1081">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1082">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1082">Example</span></span>

```c
FX_MEDIA        my_media;
UCHAR            my_short_name[14];

/* Retrieve the short name associated with "my_really_long_name". */

status = fx_directory_short_name_get_extended(&my_media,
    "my_really_long_name", my_short_name, sizeof(my_short_name));

/* If status is FX_SUCCESS the short name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1083">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1083">See Also</span></span>

- <span data-ttu-id="9969a-1084">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1084">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-1085">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1085">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-1086">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1086">fx_directory_create</span></span>
- <span data-ttu-id="9969a-1087">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1087">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-1088">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1088">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-1089">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1089">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-1090">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-1090">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-1091">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-1091">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-1092">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1092">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-1093">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-1093">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-1094">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1094">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-1095">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-1095">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-1096">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1096">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-1097">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1097">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-1098">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-1098">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-1099">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-1099">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-1100">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-1100">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-1101">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1101">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-1102">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1102">fx_unicode_directory_create</span></span>
- <span data-ttu-id="9969a-1103">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1103">fx_unicode_directory_rename</span></span>

## <a name="fx_fault_tolerant_enable"></a><span data-ttu-id="9969a-1104">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-1104">fx_fault_tolerant_enable</span></span>

<span data-ttu-id="9969a-1105">Abilita il servizio a tolleranza di errore</span><span class="sxs-lookup"><span data-stu-id="9969a-1105">Enables the fault tolerant service</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1106">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1106">Prototype</span></span>

```csharp
UINT fx_fault_tolerant_enable(
    FX_MEDIA *media_ptr,
    VOID *memory_buffer,
    UINT memory_size);
```

### <a name="description"></a><span data-ttu-id="9969a-1107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1107">Description</span></span>

<span data-ttu-id="9969a-1108">Questo servizio abilita il modulo a tolleranza di errore.</span><span class="sxs-lookup"><span data-stu-id="9969a-1108">This service enables the fault tolerant module.</span></span> <span data-ttu-id="9969a-1109">All'avvio, il modulo a tolleranza di errore rileva se il file system è sotto la protezione a tolleranza di errore FileX.</span><span class="sxs-lookup"><span data-stu-id="9969a-1109">Upon starting, the fault tolerant module detects whether or not the file system is under FileX fault tolerant protection.</span></span> <span data-ttu-id="9969a-1110">In caso contrario, il servizio trova i settori disponibili file system per archiviare i log file system transazioni.</span><span class="sxs-lookup"><span data-stu-id="9969a-1110">If it is not, the service finds available sectors on the file system to store logs on file system transactions.</span></span> <span data-ttu-id="9969a-1111">Se il file system è in protezione a tolleranza di errore FileX, applica i log al file system per mantenerne l'integrità.</span><span class="sxs-lookup"><span data-stu-id="9969a-1111">If the file system is under FileX fault tolerant protection, it applies the logs to the file system to maintain its integrity.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1112">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1112">Input Parameters</span></span>

- <span data-ttu-id="9969a-1113">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-1113">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-1114">**memory_ptr:** puntatore a un blocco di memoria usato dal modulo a tolleranza di errore come memoria scratch.</span><span class="sxs-lookup"><span data-stu-id="9969a-1114">**memory_ptr**: Pointer to a block of memory used by the fault tolerant module as scratch memory.</span></span>
- <span data-ttu-id="9969a-1115">**memory_size:** dimensioni della memoria scratch.</span><span class="sxs-lookup"><span data-stu-id="9969a-1115">**memory_size**: The size of the scratch memory.</span></span> <span data-ttu-id="9969a-1116">Per il corretto funzionamento della tolleranza di errore, le dimensioni della memoria scratch devono essere di almeno 3072 byte e devono essere multiple delle dimensioni del settore.</span><span class="sxs-lookup"><span data-stu-id="9969a-1116">In order for fault tolerant to work properly, the scratch memory size shall be at least 3072 bytes,- and must be multiple of sector size.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1117">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1117">Return Values</span></span>

- <span data-ttu-id="9969a-1118">**FX_SUCCESS** (0x00) Abilitato correttamente a tolleranza di errore.</span><span class="sxs-lookup"><span data-stu-id="9969a-1118">**FX_SUCCESS** (0x00) Successfully enabled fault tolerant.</span></span>
- <span data-ttu-id="9969a-1119">**FX_NOT_ENOUGH_MEMORY** (0x91) dimensioni della memoria troppo piccole.</span><span class="sxs-lookup"><span data-stu-id="9969a-1119">**FX_NOT_ENOUGH_MEMORY** (0x91)    memory size too small.</span></span>
- <span data-ttu-id="9969a-1120">**FX_BOOT_ERROR** (0x01) Errore del settore di avvio.</span><span class="sxs-lookup"><span data-stu-id="9969a-1120">**FX_BOOT_ERROR** (0x01) Boot sector error.</span></span>
- <span data-ttu-id="9969a-1121">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1121">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1122">**FX_NO_MORE_ENTRIES** (0x0F) Nessun cluster gratuito disponibile.</span><span class="sxs-lookup"><span data-stu-id="9969a-1122">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="9969a-1123">**FX_NO_MORE_SPACE** (0x0A) I supporti associati a questo file non hanno un numero sufficiente di cluster disponibili.</span><span class="sxs-lookup"><span data-stu-id="9969a-1123">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="9969a-1124">**FX_SECTOR_INVALID** (0x89) Il settore non è valido</span><span class="sxs-lookup"><span data-stu-id="9969a-1124">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="9969a-1125">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1125">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1126">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1126">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="9969a-1127">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1127">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1128">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1128">Allowed From</span></span>

<span data-ttu-id="9969a-1129">inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1129">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1130">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1130">Example</span></span>

```c

/* Declare memory space used for fault tolerant. */

ULONG fault tolerant_memory[3072 / sizeof(ULONG)];

/* Enable fault tolerant. */

fx_fault_tolerant_enable(media_ptr, fault_tolerant_memory, sizeof(fault_tolerant_memory));

```

### <a name="see-also"></a><span data-ttu-id="9969a-1131">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1131">See Also</span></span>

- <span data-ttu-id="9969a-1132">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-1132">fx_system_initialize</span></span>
- <span data-ttu-id="9969a-1133">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-1133">fx_media_abort</span></span>
- <span data-ttu-id="9969a-1134">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-1134">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-1135">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-1135">fx_media_check</span></span>
- <span data-ttu-id="9969a-1136">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1136">fx_media_close</span></span>
- <span data-ttu-id="9969a-1137">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1137">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-1138">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-1138">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-1139">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-1139">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-1140">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-1140">fx_media_flush</span></span>
- <span data-ttu-id="9969a-1141">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-1141">fx_media_format</span></span>
- <span data-ttu-id="9969a-1142">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1142">fx_media_open</span></span>
- <span data-ttu-id="9969a-1143">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1143">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-1144">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1144">fx_media_read</span></span>
- <span data-ttu-id="9969a-1145">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-1145">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-1146">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1146">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-1147">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1147">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-1148">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1148">fx_media_write</span></span>

## <a name="fx_file_allocate"></a><span data-ttu-id="9969a-1149">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1149">fx_file_allocate</span></span>

<span data-ttu-id="9969a-1150">Alloca spazio per un file</span><span class="sxs-lookup"><span data-stu-id="9969a-1150">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1151">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1151">Prototype</span></span>

```csharp
UINT fx_file_allocate(
    FX_FILE *file_ptr, 
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="9969a-1152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1152">Description</span></span>

<span data-ttu-id="9969a-1153">Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1153">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="9969a-1154">FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster.</span><span class="sxs-lookup"><span data-stu-id="9969a-1154">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="9969a-1155">Il risultato viene quindi arrotondato all'intero cluster successivo.</span><span class="sxs-lookup"><span data-stu-id="9969a-1155">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="9969a-1156">Per allocare spazio oltre 4 GB, l'applicazione deve usare il servizio *fx_file_extended_allocate*.</span><span class="sxs-lookup"><span data-stu-id="9969a-1156">To allocate space beyond 4GB, application shall use the service *fx_file_extended_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1157">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1157">Input Parameters</span></span>

- <span data-ttu-id="9969a-1158">**file_ptr:** puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-1158">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="9969a-1159">**size**: numero di byte da allocare per il file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1159">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1160">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1160">Return Values</span></span>

- <span data-ttu-id="9969a-1161">**FX_SUCCESS** (0x00) Corretta allocazione dei file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1161">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="9969a-1162">**FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1162">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="9969a-1163">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1163">**FX_FAT_READ_ERROR** (0x03) Failed to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1164">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1164">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1165">**FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1165">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="9969a-1166">**FX_NO_MORE_ENTRIES** (0x0F) Nessun cluster gratuito disponibile.</span><span class="sxs-lookup"><span data-stu-id="9969a-1166">**FX_NO_MORE_ENTRIES** (0x0F) No more free cluster available.</span></span>
- <span data-ttu-id="9969a-1167">**FX_NO_MORE_SPACE** (0x0A) I supporti associati a questo file non hanno un numero sufficiente di cluster disponibili.</span><span class="sxs-lookup"><span data-stu-id="9969a-1167">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="9969a-1168">**FX_SECTOR_INVALID** (0x89) Il settore non è valido</span><span class="sxs-lookup"><span data-stu-id="9969a-1168">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="9969a-1169">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1169">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1170">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1170">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-1171">**FX_PTR_ERROR** (0x18) Puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1171">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="9969a-1172">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1172">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1173">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1173">Allowed From</span></span>

<span data-ttu-id="9969a-1174">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1174">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1175">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1175">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;

/* Allocate 1024 bytes to the end of my_file. */

status = fx_file_allocate(&my_file, 1024);

/* If status equals FX_SUCCESS the file now has one or more
    contiguous cluster(s) that can accommodate at least 1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1176">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1176">See Also</span></span>

- <span data-ttu-id="9969a-1177">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1177">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1178">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1178">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1179">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1179">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1180">fx_file_close- fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1180">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="9969a-1181">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1181">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1182">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1182">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1183">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1183">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1184">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1184">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1185">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1185">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1186">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1186">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1187">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1187">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1188">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1188">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1189">fx_file_open- fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1189">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="9969a-1190">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1190">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1191">fx_file_rename- fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1191">fx_file_rename- fx_file_seek</span></span>
- <span data-ttu-id="9969a-1192">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1192">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1193">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1193">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1194">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1194">fx_file_write</span></span>
- <span data-ttu-id="9969a-1195">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1195">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1196">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1196">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1197">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1197">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1198">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1198">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1199">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1199">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_read"></a><span data-ttu-id="9969a-1200">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1200">fx_file_attributes_read</span></span>

<span data-ttu-id="9969a-1201">Legge gli attributi del file</span><span class="sxs-lookup"><span data-stu-id="9969a-1201">Reads file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1202">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1202">Prototype</span></span>

```c
    UINT fx_file_attributes_read(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT *attributes_ptr);
```
### <a name="description"></a><span data-ttu-id="9969a-1203">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1203">Description</span></span>

<span data-ttu-id="9969a-1204">Questo servizio legge gli attributi del file dal supporto specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1204">This service reads the file's attributes from the specified media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1205">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1205">Input Parameters</span></span>

- <span data-ttu-id="9969a-1206">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-1206">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-1207">**file_name**: puntatore al nome del file richiesto (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="9969a-1207">**file_name**: Pointer to the name of the requested file (directory path is optional).</span></span>
- <span data-ttu-id="9969a-1208">**attributes_ptr:** puntatore alla destinazione per gli attributi del file da inserire.</span><span class="sxs-lookup"><span data-stu-id="9969a-1208">**attributes_ptr**: Pointer to the destination for the file's attributes to be placed.</span></span> <span data-ttu-id="9969a-1209">Gli attributi del file vengono restituiti in un formato mappa di bit con le impostazioni possibili seguenti:</span><span class="sxs-lookup"><span data-stu-id="9969a-1209">The file attributes are returned in a bit-map format with the following possible settings:</span></span>
  - <span data-ttu-id="9969a-1210">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="9969a-1210">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="9969a-1211">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="9969a-1211">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="9969a-1212">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="9969a-1212">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="9969a-1213">FX_VOLUME (0x08)</span><span class="sxs-lookup"><span data-stu-id="9969a-1213">FX_VOLUME (0x08)</span></span>
  - <span data-ttu-id="9969a-1214">FX_DIRECTORY (0x10)</span><span class="sxs-lookup"><span data-stu-id="9969a-1214">FX_DIRECTORY (0x10)</span></span>
  - <span data-ttu-id="9969a-1215">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="9969a-1215">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1216">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1216">Return Values</span></span>

- <span data-ttu-id="9969a-1217">**FX_SUCCESS** (0x00) Lettura corretta dell'attributo.</span><span class="sxs-lookup"><span data-stu-id="9969a-1217">**FX_SUCCESS** (0x00) Successful attribute read.</span></span>
- <span data-ttu-id="9969a-1218">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1218">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-1219">**FX_NOT_FOUND** (0x04) File specificato non trovato nel supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1219">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="9969a-1220">**FX_NOT_A_FILE** (0x05) Il file specificato è una directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-1220">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="9969a-1221">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1221">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1222">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1222">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1223">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1223">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-1224">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-1224">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-1225">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1225">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1226">**FX_PTR_ERROR** (0x18) Supporto o puntatore di attributi non validi.</span><span class="sxs-lookup"><span data-stu-id="9969a-1226">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="9969a-1227">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1227">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1228">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1228">Allowed From</span></span>

<span data-ttu-id="9969a-1229">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1229">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1230">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1230">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;
UINT             attributes;

/* Retrieve the attributes of "myfile.txt" from the specified media. */

status = fx_file_attributes_read(&my_media, "myfile.txt", &attributes);

/* If status equals FX_SUCCESS, "attributes"
    contains the file attributes for "myfile.txt". */

```

### <a name="see-also"></a><span data-ttu-id="9969a-1231">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1231">See Also</span></span>

- <span data-ttu-id="9969a-1232">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1232">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1233">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1233">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1234">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1234">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1235">fx_file_close- fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1235">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="9969a-1236">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1236">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1237">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1237">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1238">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1238">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1239">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1239">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1240">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1240">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1241">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1241">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1242">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1242">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1243">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1243">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1244">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1244">fx_file_open</span></span>
- <span data-ttu-id="9969a-1245">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1245">fx_file_read</span></span>
- <span data-ttu-id="9969a-1246">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1246">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1247">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1247">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1248">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1248">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1249">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1249">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1250">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1250">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1251">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1251">fx_file_write</span></span>
- <span data-ttu-id="9969a-1252">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1252">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1253">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1253">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1254">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1254">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1255">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1255">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1256">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1256">fx_unicode_short_name_get</span></span>

## <a name="fx_file_attributes_set"></a><span data-ttu-id="9969a-1257">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1257">fx_file_attributes_set</span></span>

<span data-ttu-id="9969a-1258">Imposta gli attributi del file</span><span class="sxs-lookup"><span data-stu-id="9969a-1258">Sets file attributes</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1259">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1259">Prototype</span></span>

```c
UINT fx_file_attributes_set(
    FX_MEDIA *media_ptr,
    CHAR *file_name,
    UINT attributes);
```
### <a name="description"></a><span data-ttu-id="9969a-1260">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1260">Description</span></span>

<span data-ttu-id="9969a-1261">Questo servizio imposta gli attributi del file su quelli specificati dal chiamante.</span><span class="sxs-lookup"><span data-stu-id="9969a-1261">This service sets the file's attributes to those specified by the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-1262">*L'applicazione può modificare solo un subset degli attributi del file con questo servizio. Qualsiasi tentativo di impostare attributi aggiuntivi restituirà un errore.*</span><span class="sxs-lookup"><span data-stu-id="9969a-1262">*The application is only allowed to modify a subset of the file's attributes with this service. Any attempt to set additional attributes will result in an error.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1263">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1263">Input Parameters</span></span>

- <span data-ttu-id="9969a-1264">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-1264">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-1265">**file_name:** puntatore al nome del file richiesto\*\* (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="9969a-1265">**file_name**: Pointer to the name of the requested file\*\* (directory path is optional).</span></span>
- <span data-ttu-id="9969a-1266">**attributes**: i nuovi attributi per il file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1266">**attributes**: The new attributes for the file.</span></span> <span data-ttu-id="9969a-1267">Gli attributi di file validi sono definiti nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="9969a-1267">The valid file attributes are defined as follows:</span></span>
  - <span data-ttu-id="9969a-1268">FX_READ_ONLY (0x01)</span><span class="sxs-lookup"><span data-stu-id="9969a-1268">FX_READ_ONLY (0x01)</span></span>
  - <span data-ttu-id="9969a-1269">FX_HIDDEN (0x02)</span><span class="sxs-lookup"><span data-stu-id="9969a-1269">FX_HIDDEN (0x02)</span></span>
  - <span data-ttu-id="9969a-1270">FX_SYSTEM (0x04)</span><span class="sxs-lookup"><span data-stu-id="9969a-1270">FX_SYSTEM (0x04)</span></span>
  - <span data-ttu-id="9969a-1271">FX_ARCHIVE (0x20)</span><span class="sxs-lookup"><span data-stu-id="9969a-1271">FX_ARCHIVE (0x20)</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1272">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1272">Return Values</span></span>

- <span data-ttu-id="9969a-1273">**FX_SUCCESS** (0x00) Set di attributi riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-1273">**FX_SUCCESS** (0x00) Successful attribute set.</span></span>
- <span data-ttu-id="9969a-1274">**FX_ACCESS_ERROR** file (0x06) è aperto e non è possibile impostarne gli attributi.</span><span class="sxs-lookup"><span data-stu-id="9969a-1274">**FX_ACCESS_ERROR** (0x06) File is open and cannot have its attributes set.</span></span>
- <span data-ttu-id="9969a-1275">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1275">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1276">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1276">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1277">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1277">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-1278">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci nella tabella FAT o nella mappa cluster exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1278">**FX_NO_MORE_ENTRIES** (0x0F) No more entries in the FAT table or exFAT cluster map.</span></span>
- <span data-ttu-id="9969a-1279">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="9969a-1279">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="9969a-1280">**FX_NOT_FOUND** (0x04) Il file specificato non è stato trovato nel supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1280">**FX_NOT_FOUND** (0x04) Specified file was not found in the media.</span></span>
- <span data-ttu-id="9969a-1281">**FX_NOT_A_FILE** (0x05) Il file specificato è una directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-1281">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="9969a-1282">**FX_SECTOR_INVALID** (0x89) Non è valido</span><span class="sxs-lookup"><span data-stu-id="9969a-1282">**FX_SECTOR_INVALID** (0x89) Sector is invalid</span></span>
- <span data-ttu-id="9969a-1283">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1283">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1284">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1284">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-1285">**FX_MEDIA_INVALID** (0x02) Supporto non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1285">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="9969a-1286">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1286">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="9969a-1287">**FX_INVALID_ATTR** (0x19) Attributi non validi selezionati.</span><span class="sxs-lookup"><span data-stu-id="9969a-1287">**FX_INVALID_ATTR** (0x19) Invalid attributes selected.</span></span>
- <span data-ttu-id="9969a-1288">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1288">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1289">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1289">Allowed From</span></span>

<span data-ttu-id="9969a-1290">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1290">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1291">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1291">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Set the attributes of "myfile.txt" to read-only. */

status = fx_file_attributes_set(&my_media, "myfile.txt", FX_READ_ONLY);

/* If status equals FX_SUCCESS, the file is now read-only. */

```

### <a name="see-also"></a><span data-ttu-id="9969a-1292">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1292">See Also</span></span>

- <span data-ttu-id="9969a-1293">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1293">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1294">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1294">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1295">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1295">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1296">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1296">fx_file_close</span></span>
- <span data-ttu-id="9969a-1297">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1297">fx_file_create</span></span>
- <span data-ttu-id="9969a-1298">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1298">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1299">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1299">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1300">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1300">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1301">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1301">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1302">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1302">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1303">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1303">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1304">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1304">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1305">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1305">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1306">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1306">fx_file_open</span></span>
- <span data-ttu-id="9969a-1307">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1307">fx_file_read</span></span>
- <span data-ttu-id="9969a-1308">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1308">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1309">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1309">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1310">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1310">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1311">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1311">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1312">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1312">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1313">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1313">fx_file_write</span></span>
- <span data-ttu-id="9969a-1314">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1314">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1315">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1315">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1316">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1316">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1317">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1317">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1318">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1318">fx_unicode_short_name_get</span></span>

## <a name="fx_file_best_effort_allocate"></a><span data-ttu-id="9969a-1319">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1319">fx_file_best_effort_allocate</span></span>

<span data-ttu-id="9969a-1320">Il massimo sforzo per allocare spazio per un file</span><span class="sxs-lookup"><span data-stu-id="9969a-1320">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1321">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1321">Prototype</span></span>

```c
UINT fx_file_best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG size,
    ULONG *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="9969a-1322">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1322">Description</span></span>

<span data-ttu-id="9969a-1323">Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1323">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="9969a-1324">FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster.</span><span class="sxs-lookup"><span data-stu-id="9969a-1324">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="9969a-1325">Il risultato viene quindi arrotondato per es.</span><span class="sxs-lookup"><span data-stu-id="9969a-1325">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="9969a-1326">Se nel supporto non sono disponibili cluster consecutivi sufficienti, questo servizio collega il blocco più grande disponibile di cluster consecutivi al file .</span><span class="sxs-lookup"><span data-stu-id="9969a-1326">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="9969a-1327">La quantità di spazio effettivamente allocato al file viene restituita al chiamante.</span><span class="sxs-lookup"><span data-stu-id="9969a-1327">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="9969a-1328">Per allocare spazio oltre 4 GB, l'applicazione deve usare il servizio *fx_file_extended_best_effort_allocate*.</span><span class="sxs-lookup"><span data-stu-id="9969a-1328">To allocate space beyond 4GB, application shall use the service *fx_file_extended_best_effort_allocate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1329">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1329">Input Parameters</span></span>

- <span data-ttu-id="9969a-1330">**file_ptr:** puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-1330">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="9969a-1331">**size:** numero di byte da allocare per il file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1331">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1332">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1332">Return Values</span></span>

- <span data-ttu-id="9969a-1333">**FX_SUCCESS** (0x00) Corretta allocazione dei file con il massimo sforzo.</span><span class="sxs-lookup"><span data-stu-id="9969a-1333">**FX_SUCCESS** (0x00) Successful best-effort file allocation.</span></span>
- <span data-ttu-id="9969a-1334">**FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1334">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="9969a-1335">**FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1335">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="9969a-1336">**FX_NO_MORE_SPACE** (0x0A) il supporto associato a questo file non dispone di un numero sufficiente di cluster disponibili.</span><span class="sxs-lookup"><span data-stu-id="9969a-1336">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="9969a-1337">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1337">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1338">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1338">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1339">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1339">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1340">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1340">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-1341">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1341">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1342">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1342">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-1343">**FX_PTR_ERROR** (0x18) Puntatore di file o destinazione non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1343">**FX_PTR_ERROR** (0x18) Invalid file pointer or destination.</span></span>
- <span data-ttu-id="9969a-1344">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1344">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1345">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1345">Allowed From</span></span>

<span data-ttu-id="9969a-1346">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1346">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1347">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1347">Example</span></span>

```c

FX_FILE         my_file;
UINT             status;
ULONG             actual_allocation;

/* Attempt to allocate 1024 bytes to the end of my_file. */

status = fx_file_best_effort_allocate(&my_file, 1024, &actual_allocation);

/* If status equals FX_SUCCESS, the number of bytes
    allocated to the file is found in actual_allocation. */

```

### <a name="see-also"></a><span data-ttu-id="9969a-1348">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1348">See Also</span></span>

- <span data-ttu-id="9969a-1349">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1349">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1350">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1350">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1351">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1351">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1352">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1352">fx_file_close</span></span>
- <span data-ttu-id="9969a-1353">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1353">fx_file_create</span></span>
- <span data-ttu-id="9969a-1354">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1354">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1355">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1355">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1356">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1356">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1357">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1357">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1358">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1358">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1359">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1359">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1360">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1360">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1361">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1361">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1362">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1362">fx_file_open</span></span>
- <span data-ttu-id="9969a-1363">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1363">fx_file_read</span></span>
- <span data-ttu-id="9969a-1364">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1364">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1365">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1365">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1366">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1366">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1367">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1367">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1368">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1368">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1369">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1369">fx_file_write</span></span>
- <span data-ttu-id="9969a-1370">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1370">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1371">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1371">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1372">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1372">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1373">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1373">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1374">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1374">fx_unicode_short_name_get</span></span>

## <a name="fx_file_close"></a><span data-ttu-id="9969a-1375">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1375">fx_file_close</span></span>

<span data-ttu-id="9969a-1376">Chiude il file</span><span class="sxs-lookup"><span data-stu-id="9969a-1376">Closes file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1377">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1377">Prototype</span></span>

```c
UINT fx_file_close(FX_FILE *file_ptr);
```
### <a name="description"></a><span data-ttu-id="9969a-1378">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1378">Description</span></span>

<span data-ttu-id="9969a-1379">Questo servizio chiude il file specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1379">This service closes the specified file.</span></span> <span data-ttu-id="9969a-1380">Se il file è stato aperto per la scrittura e se è stato modificato, questo servizio completa il processo di modifica del file aggiornando la voce di directory con le nuove dimensioni e l'ora e la data correnti del sistema.</span><span class="sxs-lookup"><span data-stu-id="9969a-1380">If the file was open for writing and if it was modified, this service completes the file modification process by updating its directory entry with the new size and the current system time and date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1381">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1381">Input Parameters</span></span>

- <span data-ttu-id="9969a-1382">**file_ptr:** puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-1382">**file_ptr**: Pointer to a previously opened file.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1383">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1383">Return Values</span></span>

- <span data-ttu-id="9969a-1384">**FX_SUCCESS** (0x00) Chiusura del file completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-1384">**FX_SUCCESS** (0x00) Successful file close.</span></span>
- <span data-ttu-id="9969a-1385">**FX_NOT_OPEN** (0x07) Il file specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1385">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="9969a-1386">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1386">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1387">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1387">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1388">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1388">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1389">**FX_PTR_ERROR** (0x18) Supporto o puntatore attributi non validi.</span><span class="sxs-lookup"><span data-stu-id="9969a-1389">**FX_PTR_ERROR** (0x18) Invalid media or attributes pointer.</span></span>
- <span data-ttu-id="9969a-1390">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1390">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1391">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1391">Allowed From</span></span>

<span data-ttu-id="9969a-1392">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1392">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1393">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1393">Example</span></span>

```c

FX_FILE        my_file;
UINT        status;

/* Close the previously opened file "my_file". */
status = fx_file_close(&my_file);

/* If status equals FX_SUCCESS, the file was closed successfully. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1394">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1394">See Also</span></span>

- <span data-ttu-id="9969a-1395">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1395">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1396">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1396">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1397">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1397">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1398">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1398">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1399">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1399">fx_file_create</span></span>
- <span data-ttu-id="9969a-1400">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1400">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1401">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1401">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1402">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1402">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1403">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1403">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1404">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1404">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1405">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1405">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1406">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1406">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1407">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1407">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1408">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1408">fx_file_open</span></span>
- <span data-ttu-id="9969a-1409">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1409">fx_file_read</span></span>
- <span data-ttu-id="9969a-1410">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1410">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1411">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1411">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1412">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1412">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1413">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1413">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1414">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1414">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1415">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1415">fx_file_write</span></span>
- <span data-ttu-id="9969a-1416">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1416">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1417">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1417">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1418">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1418">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1419">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1419">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1420">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1420">fx_unicode_short_name_get</span></span>

## <a name="fx_file_create"></a><span data-ttu-id="9969a-1421">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1421">fx_file_create</span></span>

<span data-ttu-id="9969a-1422">Crea il file</span><span class="sxs-lookup"><span data-stu-id="9969a-1422">Creates file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1423">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1423">Prototype</span></span>

```c
UINT fx_file_create(
    FX_MEDIA *media_ptr,
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="9969a-1424">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1424">Description</span></span>

<span data-ttu-id="9969a-1425">Questo servizio crea il file specificato nella directory predefinita o nel percorso della directory fornito con il nome del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1425">This service creates the specified file in the default directory or in the directory path supplied with the file name.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-1426">*Questo servizio crea un file di lunghezza zero, ad esempio nessun cluster allocato. L'allocazione verrà eseguita automaticamente nelle scritture di file successive o può essere eseguita in anticipo con il servizio fx_file_allocate o il fx_file_extended_allocate per lo spazio superiore a 4 GB).*</span><span class="sxs-lookup"><span data-stu-id="9969a-1426">*This service creates a file of zero length, i.e., no clusters allocated. Allocation will automatically take place on subsequent file writes or can be done in advance with the fx_file_allocate service or fx_file_extended_allocate for space beyond 4GB) service.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1427">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1427">Input Parameters</span></span>

- <span data-ttu-id="9969a-1428">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-1428">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-1429">**file_name**: puntatore al nome del file da creare (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="9969a-1429">**file_name**: Pointer to the name of the file to create (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1430">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1430">Return Values</span></span>

- <span data-ttu-id="9969a-1431">**FX_SUCCESS** (0x00) Creazione del file completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-1431">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="9969a-1432">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1432">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-1433">**FX_ALREADY_CREATED** (0x0B) Il file specificato è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1433">**FX_ALREADY_CREATED** (0x0B) Specified file was already created.</span></span>
- <span data-ttu-id="9969a-1434">**FX_NO_MORE_SPACE** (0x0A) Non sono presenti altre voci nella directory radice o non sono disponibili altri cluster.</span><span class="sxs-lookup"><span data-stu-id="9969a-1434">**FX_NO_MORE_SPACE** (0x0A)    Either there are no more entries in the root directory or there are no more clusters available.</span></span>
- <span data-ttu-id="9969a-1435">**FX_INVALID_PATH** (0x0D) Percorso non valido fornito con il nome file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1435">**FX_INVALID_PATH** (0x0D) Invalid path supplied with file name.</span></span>
- <span data-ttu-id="9969a-1436">**FX_INVALID_NAME** (0x0C) Il nome del file non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1436">**FX_INVALID_NAME** (0x0C) File name is invalid.</span></span>
- <span data-ttu-id="9969a-1437">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1437">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1438">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1438">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1439">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1439">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1440">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1440">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-1441">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-1441">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-1442">**FX_MEDIA_INVALID** (0x02)Supporti non validi.</span><span class="sxs-lookup"><span data-stu-id="9969a-1442">**FX_MEDIA_INVALID** (0x02)Invalid media.</span></span>
- <span data-ttu-id="9969a-1443">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1443">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1444">**FX_WRITE_PROTECT** (0x23) Il supporto sottostante è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1444">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="9969a-1445">**FX_PTR_ERROR** (0x18) Supporto non valido o puntatore al nome file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1445">**FX_PTR_ERROR** (0x18) Invalid media or file name pointer.</span></span>
- <span data-ttu-id="9969a-1446">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1446">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1447">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1447">Allowed From</span></span>

<span data-ttu-id="9969a-1448">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1448">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1449">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1449">Example</span></span>

```c

FX_MEDIA         my_media;
UINT             status;

/* Create a file called "myfile.txt" in the
    root or the default directory of the media. */

status = fx_file_create(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, a zero sized file named "myfile.txt". */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1450">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1450">See Also</span></span>
- <span data-ttu-id="9969a-1451">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1451">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1452">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1452">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1453">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1453">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1454">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1454">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1455">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1455">fx_file_close</span></span>
- <span data-ttu-id="9969a-1456">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1456">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1457">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1457">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1458">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1458">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1459">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1459">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1460">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1460">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1461">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1461">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1462">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1462">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1463">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1463">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1464">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1464">fx_file_open</span></span>
- <span data-ttu-id="9969a-1465">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1465">fx_file_read</span></span>
- <span data-ttu-id="9969a-1466">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1466">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1467">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1467">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1468">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1468">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1469">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1469">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1470">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1470">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1471">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1471">fx_file_write</span></span>
- <span data-ttu-id="9969a-1472">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1472">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1473">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1473">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1474">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1474">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1475">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1475">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1476">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1476">fx_unicode_short_name_get</span></span>

## <a name="fx_file_date_time_set"></a><span data-ttu-id="9969a-1477">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1477">fx_file_date_time_set</span></span>

### <a name="sets-file-date-and-time"></a><span data-ttu-id="9969a-1478">Imposta la data e l'ora del file</span><span class="sxs-lookup"><span data-stu-id="9969a-1478">Sets file date and time</span></span>

<span data-ttu-id="9969a-1479">Impostazione di data e ora del file</span><span class="sxs-lookup"><span data-stu-id="9969a-1479">Setting File Date and Time</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1480">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1480">Prototype</span></span>

```c
UINT fx_file_date_time_set(
    FX_MEDIA *media_ptr, 
    CHAR *file_name,
    UINT year, 
    UINT month, 
    UINT day,
    UINT hour, 
    UINT minute, 
    UINT second);
```
### <a name="description"></a><span data-ttu-id="9969a-1481">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1481">Description</span></span>

<span data-ttu-id="9969a-1482">Questo servizio imposta la data e l'ora del file specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1482">This service sets the date and time of the specified file.</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="input-parameters"></a><span data-ttu-id="9969a-1483">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1483">Input Parameters</span></span>

- <span data-ttu-id="9969a-1484">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-1484">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-1485">**file_name:** puntatore al nome del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1485">**file_name**: Pointer to name of the file.</span></span>
- <span data-ttu-id="9969a-1486">**year:** valore dell'anno (1980-2107 inclusi).</span><span class="sxs-lookup"><span data-stu-id="9969a-1486">**year**: Value of year (1980-2107 inclusive).</span></span>
- <span data-ttu-id="9969a-1487">**month:** valore del mese (da 1 a 12 inclusi).</span><span class="sxs-lookup"><span data-stu-id="9969a-1487">**month**: Value of month (1-12 inclusive).</span></span>
- <span data-ttu-id="9969a-1488">**day:** valore del giorno (da 1 a 31 inclusi).</span><span class="sxs-lookup"><span data-stu-id="9969a-1488">**day**: Value of day (1-31 inclusive).</span></span>
- <span data-ttu-id="9969a-1489">**hour**: valore dell'ora (0-23 inclusi).</span><span class="sxs-lookup"><span data-stu-id="9969a-1489">**hour**: Value of hour (0-23 inclusive).</span></span>
- <span data-ttu-id="9969a-1490">**minute:** valore dei minuti (da 0 a 59 inclusi).</span><span class="sxs-lookup"><span data-stu-id="9969a-1490">**minute**: Value of minute (0-59 inclusive).</span></span>
- <span data-ttu-id="9969a-1491">**second:** valore del secondo (0-59 inclusi).</span><span class="sxs-lookup"><span data-stu-id="9969a-1491">**second**: Value of second (0-59 inclusive).</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1492">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1492">Return Values</span></span>

- <span data-ttu-id="9969a-1493">**FX_SUCCESS** (0x00) Set di data/ora riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-1493">**FX_SUCCESS** (0x00) Successful date/time set.</span></span>
- <span data-ttu-id="9969a-1494">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1494">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-1495">**FX_NOT_FOUND** file (0x04) non trovato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1495">**FX_NOT_FOUND** (0x04)    File was not found.</span></span>
- <span data-ttu-id="9969a-1496">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1496">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="9969a-1497">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1497">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1498">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1498">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1499">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1499">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-1500">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="9969a-1500">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation.</span></span>
- <span data-ttu-id="9969a-1501">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1501">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1502">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1502">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-1503">**FX_PTR_ERROR** (0x18) Supporto o puntatore del nome non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1503">**FX_PTR_ERROR** (0x18) Invalid media or name pointer.</span></span>
- <span data-ttu-id="9969a-1504">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1504">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="9969a-1505">**FX_INVALID_YEAR** (0x12) Year non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1505">**FX_INVALID_YEAR** (0x12) Year is invalid.</span></span>
- <span data-ttu-id="9969a-1506">**FX_INVALID_MONTH** (0x13) Month non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1506">**FX_INVALID_MONTH** (0x13) Month is invalid.</span></span>
- <span data-ttu-id="9969a-1507">**FX_INVALID_DAY** (0x14) Day non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1507">**FX_INVALID_DAY** (0x14) Day is invalid.</span></span>
- <span data-ttu-id="9969a-1508">**FX_INVALID_HOUR** (0x15) Hour non è valida.</span><span class="sxs-lookup"><span data-stu-id="9969a-1508">**FX_INVALID_HOUR** (0x15)    Hour is invalid.</span></span>
- <span data-ttu-id="9969a-1509">**FX_INVALID_MINUTE** (0x16) Minute non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1509">**FX_INVALID_MINUTE** (0x16) Minute is invalid.</span></span>
- <span data-ttu-id="9969a-1510">**FX_INVALID_SECOND** (0x17) Second non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1510">**FX_INVALID_SECOND** (0x17) Second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1511">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1511">Allowed From</span></span>

<span data-ttu-id="9969a-1512">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1512">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1513">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1513">Example</span></span>

```c

FX_MEDIA         my_media;
/* Set the date/time of "my_file". */
status = fx_file_date_time_set(&my_media, "my_file", 1999, 12, 31, 23, 59, 59);

/* If status is FX_SUCCESS the file's date/time was successfully set. /*
```

### <a name="see-also"></a><span data-ttu-id="9969a-1514">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1514">See Also</span></span>

- <span data-ttu-id="9969a-1515">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1515">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1516">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1516">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1517">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1517">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1518">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1518">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1519">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1519">fx_file_close</span></span>
- <span data-ttu-id="9969a-1520">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1520">fx_file_create</span></span>
- <span data-ttu-id="9969a-1521">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1521">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1522">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1522">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1523">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1523">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1524">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1524">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1525">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1525">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1526">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1526">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1527">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1527">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1528">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1528">fx_file_open</span></span>
- <span data-ttu-id="9969a-1529">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1529">fx_file_read</span></span>
- <span data-ttu-id="9969a-1530">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1530">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1531">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1531">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1532">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1532">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1533">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1533">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1534">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1534">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1535">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1535">fx_file_write</span></span>
- <span data-ttu-id="9969a-1536">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1536">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1537">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1537">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1538">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1538">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1539">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1539">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1540">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1540">fx_unicode_short_name_get</span></span>

## <a name="fx_file_delete"></a><span data-ttu-id="9969a-1541">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1541">fx_file_delete</span></span>

### <a name="deletes-file"></a><span data-ttu-id="9969a-1542">Elimina il file</span><span class="sxs-lookup"><span data-stu-id="9969a-1542">Deletes file</span></span>

<span data-ttu-id="9969a-1543">Eliminazione di file</span><span class="sxs-lookup"><span data-stu-id="9969a-1543">File Deletion</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1544">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1544">Prototype</span></span>

```c
UINT fx_file_delete(
    FX_MEDIA *media_ptr, 
    CHAR *file_name);
```
### <a name="description"></a><span data-ttu-id="9969a-1545">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1545">Description</span></span>

<span data-ttu-id="9969a-1546">Questo servizio elimina il file specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1546">This service deletes the specified file.</span></span>


### <a name="input-parameters"></a><span data-ttu-id="9969a-1547">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1547">Input Parameters</span></span>

- <span data-ttu-id="9969a-1548">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-1548">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-1549">**file_name**: puntatore al nome del file da eliminare (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="9969a-1549">**file_name**: Pointer to the name of the file to delete (directory path is optional).</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1550">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1550">Return Values</span></span>

- <span data-ttu-id="9969a-1551">**FX_SUCCESS** (0x00) Eliminazione file riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-1551">**FX_SUCCESS** (0x00) Successful file delete.</span></span>
- <span data-ttu-id="9969a-1552">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1552">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-1553">**FX_NOT_FOUND** (0x04) Il file specificato non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1553">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="9969a-1554">**FX_NOT_A_FILE** (0x05) Il nome file specificato è una directory o un volume.</span><span class="sxs-lookup"><span data-stu-id="9969a-1554">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="9969a-1555">**FX_ACCESS_ERROR** (0x06) Il file specificato è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1555">**FX_ACCESS_ERROR** (0x06) Specified file is currently open.</span></span>
- <span data-ttu-id="9969a-1556">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1556">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1557">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1557">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1558">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1558">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1559">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1559">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-1560">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-1560">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-1561">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1561">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1562">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1562">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-1563">**FX_MEDIA_INVALID** (0x02) Supporto non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1563">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="9969a-1564">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1564">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="9969a-1565">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1565">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1566">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1566">Allowed From</span></span>

<span data-ttu-id="9969a-1567">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1567">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1568">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1568">Example</span></span>

```c

FX_MEDIA            my_media;
UINT                 status;
/* Delete the file "myfile.txt". */

status = fx_file_delete(&my_media, "myfile.txt");

/* If status equals FX_SUCCESS, "myfile.txt" has been deleted. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1569">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1569">See Also</span></span>

- <span data-ttu-id="9969a-1570">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1570">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1571">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1571">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1572">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1572">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1573">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1573">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1574">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1574">fx_file_close</span></span>
- <span data-ttu-id="9969a-1575">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1575">fx_file_create</span></span>
- <span data-ttu-id="9969a-1576">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1576">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1577">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1577">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1578">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1578">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1579">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1579">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1580">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1580">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1581">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1581">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1582">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1582">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1583">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1583">fx_file_open</span></span>
- <span data-ttu-id="9969a-1584">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1584">fx_file_read</span></span>
- <span data-ttu-id="9969a-1585">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1585">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1586">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1586">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1587">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1587">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1588">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1588">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1589">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1589">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1590">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1590">fx_file_write</span></span>
- <span data-ttu-id="9969a-1591">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1591">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1592">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1592">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1593">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1593">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1594">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1594">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1595">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1595">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_allocate"></a><span data-ttu-id="9969a-1596">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1596">fx_file_extended_allocate</span></span>

<span data-ttu-id="9969a-1597">Alloca spazio per un file</span><span class="sxs-lookup"><span data-stu-id="9969a-1597">Allocates space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1598">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1598">Prototype</span></span>

```c
UINT fx_file_extended_allocate(
    FX_FILE *file_ptr, 
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="9969a-1599">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1599">Description</span></span>

<span data-ttu-id="9969a-1600">Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1600">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="9969a-1601">FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster.</span><span class="sxs-lookup"><span data-stu-id="9969a-1601">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="9969a-1602">Il risultato viene quindi arrotondato per es.</span><span class="sxs-lookup"><span data-stu-id="9969a-1602">The result is then rounded up to the next whole cluster.</span></span>

<span data-ttu-id="9969a-1603">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1603">This service is designed for exFAT.</span></span> <span data-ttu-id="9969a-1604">Il *parametro size* accetta un valore intero a 64 bit, che consente al chiamante di preallocare spazio oltre l'intervallo di 4 GB.</span><span class="sxs-lookup"><span data-stu-id="9969a-1604">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1605">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1605">Input Parameters</span></span>

- <span data-ttu-id="9969a-1606">**file_ptr:** puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-1606">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="9969a-1607">**size:** numero di byte da allocare per il file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1607">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1608">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1608">Return Values</span></span>

- <span data-ttu-id="9969a-1609">**FX_SUCCESS** (0x00) Allocazione file riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-1609">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="9969a-1610">**FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1610">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="9969a-1611">**FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1611">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="9969a-1612">**FX_NO_MORE_SPACE** (0x0A) I supporti associati a questo file non hanno un numero sufficiente di cluster disponibili.</span><span class="sxs-lookup"><span data-stu-id="9969a-1612">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="9969a-1613">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1613">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1614">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1614">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1615">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1615">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1616">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1616">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-1617">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1617">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1618">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1618">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-1619">**FX_PTR_ERROR** (0x18) Puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1619">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="9969a-1620">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1620">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1621">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1621">Allowed From</span></span>

<span data-ttu-id="9969a-1622">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1622">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1623">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1623">Example</span></span>

```c

FX_FILE            my_file;
UINT            status;
/* Allocate 0x100000000 bytes to the end of my_file. */

status = fx_file_extended_allocate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS the file now has
    one or more contiguous cluster(s) that can accommodate at least
    1024 bytes of user data. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1624">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1624">See Also</span></span>

- <span data-ttu-id="9969a-1625">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1625">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1626">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1626">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1627">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1627">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1628">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1628">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1629">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1629">fx_file_close</span></span>
- <span data-ttu-id="9969a-1630">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1630">fx_file_create</span></span>
- <span data-ttu-id="9969a-1631">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1631">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1632">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1632">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1633">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1633">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1634">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1634">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1635">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1635">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1636">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1636">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1637">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1637">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1638">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1638">fx_file_open</span></span>
- <span data-ttu-id="9969a-1639">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1639">fx_file_read</span></span>
- <span data-ttu-id="9969a-1640">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1640">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1641">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1641">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1642">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1642">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1643">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1643">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1644">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1644">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1645">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1645">fx_file_write</span></span>
- <span data-ttu-id="9969a-1646">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1646">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1647">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1647">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1648">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1648">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1649">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1649">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1650">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1650">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_best_effort_allocate"></a><span data-ttu-id="9969a-1651">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1651">fx_file_extended_best_effort_allocate</span></span>

<span data-ttu-id="9969a-1652">Il massimo sforzo per allocare spazio per un file</span><span class="sxs-lookup"><span data-stu-id="9969a-1652">Best effort to allocate space for a file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1653">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1653">Prototype</span></span>

```c
UINT fx_file_extended best_effort_allocate(
    FX_FILE *file_ptr,
    ULONG64 size,
    ULONG64 *actual_size_allocated);
```
### <a name="description"></a><span data-ttu-id="9969a-1654">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1654">Description</span></span>

<span data-ttu-id="9969a-1655">Questo servizio alloca e collega uno o più cluster contigui alla fine del file specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1655">This service allocates and links one or more contiguous clusters to the end of the specified file.</span></span> <span data-ttu-id="9969a-1656">FileX determina il numero di cluster necessari dividendo le dimensioni richieste per il numero di byte per cluster.</span><span class="sxs-lookup"><span data-stu-id="9969a-1656">FileX determines the number of clusters required by dividing the requested size by the number of bytes per cluster.</span></span> <span data-ttu-id="9969a-1657">Il risultato viene quindi arrotondato all'intero cluster successivo.</span><span class="sxs-lookup"><span data-stu-id="9969a-1657">The result is then rounded up to the next whole cluster.</span></span> <span data-ttu-id="9969a-1658">Se non sono disponibili cluster consecutivi sufficienti nei supporti, questo servizio collega il blocco più grande disponibile di cluster consecutivi al file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1658">If there are not enough consecutive clusters available in the media, this service links the largest available block of consecutive clusters to the file.</span></span> <span data-ttu-id="9969a-1659">La quantità di spazio effettivamente allocato al file viene restituita al chiamante.</span><span class="sxs-lookup"><span data-stu-id="9969a-1659">The amount of space actually allocated to the file is returned to the caller.</span></span>

<span data-ttu-id="9969a-1660">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1660">This service is designed for exFAT.</span></span> <span data-ttu-id="9969a-1661">Il *parametro size* accetta un valore intero a 64 bit, che consente al chiamante di preallocare spazio oltre l'intervallo di 4 GB.</span><span class="sxs-lookup"><span data-stu-id="9969a-1661">The *size* parameter takes a 64-bit integer value, which allows the caller to pre-allocate space beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1662">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1662">Input Parameters</span></span>

- <span data-ttu-id="9969a-1663">**file_ptr:** puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-1663">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="9969a-1664">**size**: numero di byte da allocare per il file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1664">**size**: Number of bytes to allocate for the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1665">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1665">Return Values</span></span>

- <span data-ttu-id="9969a-1666">**FX_SUCCESS** (0x00) Corretta allocazione dei file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1666">**FX_SUCCESS** (0x00) Successful file allocation.</span></span>
- <span data-ttu-id="9969a-1667">**FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1667">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="9969a-1668">**FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1668">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="9969a-1669">**FX_NO_MORE_SPACE** (0x0A) I supporti associati a questo file non hanno un numero sufficiente di cluster disponibili.</span><span class="sxs-lookup"><span data-stu-id="9969a-1669">**FX_NO_MORE_SPACE** (0x0A) Media associated with this file does not have enough available clusters.</span></span>
- <span data-ttu-id="9969a-1670">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1670">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1671">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1671">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1672">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1672">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1673">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1673">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-1674">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1674">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1675">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1675">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-1676">**FX_PTR_ERROR** (0x18) Puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1676">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="9969a-1677">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1677">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1678">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1678">Allowed From</span></span>

<span data-ttu-id="9969a-1679">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1679">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1680">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1680">Example</span></span>

```c

FX_FILE my_file;
UINT             status;
ULONG64         actual_allocation;

/* Attempt to allocate 0x100000000 bytes to the end of my_file. */

status = fx_file_extended_best_effort_allocate(&my_file,
    0x100000000, &actual_allocation);

/* If status equals FX_SUCCESS, the number of bytes
    allocated to the file is found in actual_allocation. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1681">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1681">See Also</span></span>

- <span data-ttu-id="9969a-1682">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1682">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1683">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1683">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1684">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1684">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1685">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1685">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1686">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1686">fx_file_close</span></span>
- <span data-ttu-id="9969a-1687">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1687">fx_file_create</span></span>
- <span data-ttu-id="9969a-1688">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1688">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1689">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1689">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1690">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1690">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1691">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1691">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1692">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1692">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1693">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1693">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1694">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1694">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1695">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1695">fx_file_open</span></span>
- <span data-ttu-id="9969a-1696">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1696">fx_file_read</span></span>
- <span data-ttu-id="9969a-1697">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1697">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1698">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1698">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1699">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1699">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1700">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1700">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1701">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1701">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1702">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1702">fx_file_write</span></span>
- <span data-ttu-id="9969a-1703">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1703">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1704">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1704">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1705">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1705">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1706">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1706">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1707">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1707">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_relative_seek"></a><span data-ttu-id="9969a-1708">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1708">fx_file_extended_relative_seek</span></span>

<span data-ttu-id="9969a-1709">Posizioni a un offset di byte relativo</span><span class="sxs-lookup"><span data-stu-id="9969a-1709">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1710">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1710">Prototype</span></span>

```c
UINT fx_file_extended_relative_seek(
    FX_FILE *file_ptr,
    ULONG64 byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="9969a-1711">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1711">Description</span></span>

<span data-ttu-id="9969a-1712">Questo servizio posiziona il puntatore di lettura/scrittura del file interno all'offset di byte relativo specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1712">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="9969a-1713">Qualsiasi richiesta di lettura o scrittura di file successiva inizierà in questa posizione nel file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1713">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="9969a-1714">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1714">This service is designed for exFAT.</span></span> <span data-ttu-id="9969a-1715">Il *byte_offset* accetta un valore intero a 64 bit, che consente al chiamante di riposizionare il puntatore di lettura/scrittura oltre l'intervallo di 4 GB.</span><span class="sxs-lookup"><span data-stu-id="9969a-1715">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-1716">*Se l'operazione di ricerca tenta di cercare oltre la fine del file, il puntatore di lettura/scrittura del file viene posizionato alla fine del file. Al contrario, se l'operazione di ricerca tenta di posizionarsi oltre l'inizio del file, il puntatore di lettura/scrittura del file viene posizionato all'inizio del file.*</span><span class="sxs-lookup"><span data-stu-id="9969a-1716">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1717">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1717">Input Parameters</span></span>

- <span data-ttu-id="9969a-1718">**file_ptr:** puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-1718">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="9969a-1719">**byte_offset:** offset di byte relativo desiderato nel file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1719">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="9969a-1720">**seek_from**: direzione e posizione della posizione da cui eseguire la ricerca relativa.</span><span class="sxs-lookup"><span data-stu-id="9969a-1720">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="9969a-1721">Le opzioni di ricerca valide sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="9969a-1721">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="9969a-1722">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="9969a-1722">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="9969a-1723">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="9969a-1723">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="9969a-1724">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="9969a-1724">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="9969a-1725">FX_SEEK_BACK (0x03) Se FX_SEEK_BEGIN specificato, l'operazione di ricerca viene eseguita dall'inizio del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1725">FX_SEEK_BACK (0x03) If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="9969a-1726">Se FX_SEEK_END specificato, l'operazione di ricerca viene eseguita all'indietro a partire dalla fine del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1726">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="9969a-1727">Se FX_SEEK_FORWARD specificato, l'operazione di ricerca viene eseguita in avanti dalla posizione corrente del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1727">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="9969a-1728">Se FX_SEEK_BACK specificato, l'operazione di ricerca viene eseguita all'indietro dalla posizione corrente del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1728">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1729">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1729">Return Values</span></span>

- <span data-ttu-id="9969a-1730">**FX_SUCCESS** (0x00) Ricerca relativa del file completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-1730">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="9969a-1731">**FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1731">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="9969a-1732">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1732">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1733">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1733">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1734">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-1734">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-1735">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1735">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1736">**FX_PTR_ERROR** (0x18) Puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1736">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="9969a-1737">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1737">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1738">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1738">Allowed From</span></span>

<span data-ttu-id="9969a-1739">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1739">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1740">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1740">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to seek forward 0x100000000 bytes in "my_file". */

status = fx_file_extended_relative_seek(&my_file, 0x100000000, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write
    pointers are positioned 0x100000000 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1741">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1741">See Also</span></span>

- <span data-ttu-id="9969a-1742">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1742">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1743">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1743">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1744">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1744">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1745">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1745">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1746">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1746">fx_file_close</span></span>
- <span data-ttu-id="9969a-1747">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1747">fx_file_create</span></span>
- <span data-ttu-id="9969a-1748">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1748">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1749">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1749">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1750">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1750">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1751">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1751">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1752">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1752">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1753">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1753">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1754">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1754">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1755">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1755">fx_file_open</span></span>
- <span data-ttu-id="9969a-1756">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1756">fx_file_read</span></span>
- <span data-ttu-id="9969a-1757">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1757">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1758">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1758">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1759">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1759">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1760">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1760">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1761">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1761">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1762">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1762">fx_file_write</span></span>
- <span data-ttu-id="9969a-1763">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1763">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1764">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1764">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1765">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1765">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1766">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1766">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1767">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1767">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_seek"></a><span data-ttu-id="9969a-1768">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1768">fx_file_extended_seek</span></span>

<span data-ttu-id="9969a-1769">Posizioni per l'offset dei byte</span><span class="sxs-lookup"><span data-stu-id="9969a-1769">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1770">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1770">Prototype</span></span>

```c
UINT fx_file_extended_seek(
    FX_FILE *file_ptr, 
    ULONG64 byte_offset);
```
### <a name="description"></a><span data-ttu-id="9969a-1771">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1771">Description</span></span>

<span data-ttu-id="9969a-1772">Questo servizio posiziona il puntatore interno di lettura/scrittura del file all'offset di byte specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1772">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="9969a-1773">Qualsiasi richiesta di lettura o scrittura di file successiva inizierà in questa posizione nel file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1773">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="9969a-1774">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1774">This service is designed for exFAT.</span></span> <span data-ttu-id="9969a-1775">Il *byte_offset* accetta un valore intero a 64 bit, che consente al chiamante di riposizionare il puntatore di lettura/scrittura oltre l'intervallo di 4 GB.</span><span class="sxs-lookup"><span data-stu-id="9969a-1775">The *byte_offset* parameter takes a 64bit integer value, which allows the caller to reposition the read/write pointer beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1776">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1776">Input Parameters</span></span>

- <span data-ttu-id="9969a-1777">**file_ptr:** puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1777">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="9969a-1778">**byte_offset:** offset di byte desiderato nel file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1778">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="9969a-1779">Il valore zero posiziona il puntatore di lettura/scrittura all'inizio del file, mentre un valore maggiore delle dimensioni del file posiziona il puntatore di lettura/scrittura alla fine del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1779">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1780">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1780">Return Values</span></span>

- <span data-ttu-id="9969a-1781">**FX_SUCCESS** (0x00) Ricerca file riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-1781">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="9969a-1782">**FX_NOT_OPEN** (0x07) Il file specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1782">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="9969a-1783">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1783">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1784">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1784">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1785">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-1785">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-1786">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1786">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1787">**FX_PTR_ERROR** (0x18) Puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1787">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="9969a-1788">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1788">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1789">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1789">Allowed From</span></span>

<span data-ttu-id="9969a-1790">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1790">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1791">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1791">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;
/* Seek to position 0x100000000 of "my_file." */

status = fx_file_extended_seek(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned 0x100000000 bytes from the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1792">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1792">See Also</span></span>

- <span data-ttu-id="9969a-1793">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1793">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1794">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1794">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1795">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1795">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1796">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1796">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1797">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1797">fx_file_close</span></span>
- <span data-ttu-id="9969a-1798">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1798">fx_file_create</span></span>
- <span data-ttu-id="9969a-1799">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1799">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1800">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1800">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1801">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1801">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1802">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1802">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1803">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1803">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1804">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1804">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1805">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1805">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1806">fx_file_open- fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1806">fx_file_open- fx_file_read</span></span>
- <span data-ttu-id="9969a-1807">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1807">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1808">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1808">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1809">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1809">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1810">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1810">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1811">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1811">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1812">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1812">fx_file_write</span></span>
- <span data-ttu-id="9969a-1813">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1813">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1814">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1814">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1815">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1815">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1816">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1816">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1817">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1817">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate"></a><span data-ttu-id="9969a-1818">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1818">fx_file_extended_truncate</span></span>

<span data-ttu-id="9969a-1819">Tronca il file</span><span class="sxs-lookup"><span data-stu-id="9969a-1819">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1820">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1820">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG64 size);
```
### <a name="description"></a><span data-ttu-id="9969a-1821">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1821">Description</span></span>

<span data-ttu-id="9969a-1822">Questo servizio tronca le dimensioni del file alle dimensioni specificate.</span><span class="sxs-lookup"><span data-stu-id="9969a-1822">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="9969a-1823">Se le dimensioni fornite sono maggiori delle dimensioni effettive del file, questo servizio non fa nulla.</span><span class="sxs-lookup"><span data-stu-id="9969a-1823">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="9969a-1824">Nessuno dei cluster di supporti associati al file viene rilasciato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1824">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-1825">*Prestare attenzione al troncamento dei file che possono essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*</span><span class="sxs-lookup"><span data-stu-id="9969a-1825">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="9969a-1826">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1826">This service is designed for exFAT.</span></span> <span data-ttu-id="9969a-1827">Il *parametro size* accetta un valore integer a 64 bit, che consente al chiamante di operare oltre l'intervallo di 4 GB.</span><span class="sxs-lookup"><span data-stu-id="9969a-1827">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1828">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1828">Input Parameters</span></span>

- <span data-ttu-id="9969a-1829">**file_ptr:** puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1829">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="9969a-1830">**size:** nuove dimensioni del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1830">**size**: New file size.</span></span> <span data-ttu-id="9969a-1831">I byte oltre questa nuova dimensione di file vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="9969a-1831">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1832">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1832">Return Values</span></span>

- <span data-ttu-id="9969a-1833">**FX_SUCCESS** (0x00) Troncamento del file riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-1833">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="9969a-1834">**FX_NOT_OPEN** (0x07) Il file specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1834">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="9969a-1835">**FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1835">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="9969a-1836">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1836">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1837">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1837">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1838">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1838">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-1839">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-1839">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-1840">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1840">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1841">**FX_WRITE_PROTECT** (0x23) Il supporto sottostante è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1841">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="9969a-1842">**FX_PTR_ERROR** (0x18) Puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1842">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="9969a-1843">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1843">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1844">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1844">Allowed From</span></span>

<span data-ttu-id="9969a-1845">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1845">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1846">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1846">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Truncate "my_file" to 0x100000000 bytes. */

status = fx_file_extended_truncate(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, "my_file" contains 0x100000000 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1847">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1847">See Also</span></span>

- <span data-ttu-id="9969a-1848">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1848">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1849">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1849">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1850">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1850">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1851">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1851">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1852">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1852">fx_file_close</span></span>
- <span data-ttu-id="9969a-1853">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1853">fx_file_create</span></span>
- <span data-ttu-id="9969a-1854">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1854">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1855">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1855">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1856">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1856">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1857">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1857">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1858">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1858">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1859">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1859">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1860">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1860">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1861">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1861">fx_file_open</span></span>
- <span data-ttu-id="9969a-1862">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1862">fx_file_read</span></span>
- <span data-ttu-id="9969a-1863">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1863">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1864">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1864">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1865">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1865">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1866">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1866">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1867">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1867">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1868">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1868">fx_file_write</span></span>
- <span data-ttu-id="9969a-1869">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1869">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1870">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1870">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1871">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1871">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1872">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1872">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1873">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1873">fx_unicode_short_name_get</span></span>

## <a name="fx_file_extended_truncate_release"></a><span data-ttu-id="9969a-1874">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1874">fx_file_extended_truncate_release</span></span>

<span data-ttu-id="9969a-1875">Tronca i file e rilascia i cluster</span><span class="sxs-lookup"><span data-stu-id="9969a-1875">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1876">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1876">Prototype</span></span>

```c
UINT fx_file_extended_truncate_release(
    FX_FILE *file_ptr, 
    ULONG64 size);
```

### <a name="description"></a><span data-ttu-id="9969a-1877">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1877">Description</span></span>

<span data-ttu-id="9969a-1878">Questo servizio tronca le dimensioni del file alle dimensioni specificate.</span><span class="sxs-lookup"><span data-stu-id="9969a-1878">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="9969a-1879">Se le dimensioni fornite sono maggiori delle dimensioni effettive del file, questo servizio non esegue alcun'operazione.</span><span class="sxs-lookup"><span data-stu-id="9969a-1879">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="9969a-1880">A differenza ***del fx_file_extended_truncate,*** questo servizio rilascia tutti i cluster inutilizzati.</span><span class="sxs-lookup"><span data-stu-id="9969a-1880">Unlike the ***fx_file_extended_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-1881">*Prestare attenzione al troncamento dei file che possono essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*</span><span class="sxs-lookup"><span data-stu-id="9969a-1881">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="9969a-1882">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1882">This service is designed for exFAT.</span></span> <span data-ttu-id="9969a-1883">Il *parametro size* accetta un valore integer a 64 bit, che consente al chiamante di operare oltre l'intervallo di 4 GB.</span><span class="sxs-lookup"><span data-stu-id="9969a-1883">The *size* parameter takes a 64-bit integer value, which allows the caller to operate beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1884">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1884">Input Parameters</span></span>

- <span data-ttu-id="9969a-1885">**file_ptr:** puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-1885">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="9969a-1886">**size:** nuove dimensioni del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1886">**size**: New file size.</span></span> <span data-ttu-id="9969a-1887">I byte oltre le nuove dimensioni del file vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="9969a-1887">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1888">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1888">Return Values</span></span>

- <span data-ttu-id="9969a-1889">**FX_SUCCESS** (0x00) Troncamento del file riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-1889">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="9969a-1890">**FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1890">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="9969a-1891">**FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1891">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="9969a-1892">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1892">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1893">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1893">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-1894">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1894">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1895">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1895">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-1896">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-1896">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-1897">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1897">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1898">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1898">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-1899">**FX_PTR_ERROR** (0x18) Puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1899">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="9969a-1900">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1900">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1901">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1901">Allowed From</span></span>

<span data-ttu-id="9969a-1902">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1902">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1903">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1903">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Attempt to truncate everything after the first 0x100000000 bytes of "my_file". */

status = fx_file_extended_truncate_release(&my_file, 0x100000000);

/* If status equals FX_SUCCESS, the file is now 0x100000000
    bytes or fewer and all unused clusters have been released. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1904">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1904">See Also</span></span>

- <span data-ttu-id="9969a-1905">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1905">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1906">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1906">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1907">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1907">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1908">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1908">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1909">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-1909">fx_file_close</span></span>
- <span data-ttu-id="9969a-1910">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1910">fx_file_create</span></span>
- <span data-ttu-id="9969a-1911">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1911">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1912">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1912">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1913">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1913">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1914">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1914">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1915">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1915">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1916">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1916">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1917">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1917">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1918">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1918">fx_file_open</span></span>
- <span data-ttu-id="9969a-1919">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1919">fx_file_read</span></span>
- <span data-ttu-id="9969a-1920">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1920">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1921">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1921">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1922">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1922">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1923">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1923">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1924">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1924">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1925">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1925">fx_file_write</span></span>
- <span data-ttu-id="9969a-1926">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1926">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1927">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1927">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1928">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1928">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1929">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1929">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1930">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1930">fx_unicode_short_name_get</span></span>

## <a name="fx_file_open"></a><span data-ttu-id="9969a-1931">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-1931">fx_file_open</span></span>

<span data-ttu-id="9969a-1932">Apre il file</span><span class="sxs-lookup"><span data-stu-id="9969a-1932">Opens file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1933">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1933">Prototype</span></span>

```c
UINT fx_file_open(
    FX_MEDIA *media_ptr,
    FX_FILE *file_ptr,
    CHAR *file_name,
    UINT open_type);
```
### <a name="description"></a><span data-ttu-id="9969a-1934">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1934">Description</span></span>

<span data-ttu-id="9969a-1935">Questo servizio apre il file specificato per la lettura o la scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1935">This service opens the specified file for either reading or writing.</span></span> <span data-ttu-id="9969a-1936">Un file può essere aperto per la lettura più volte, mentre un file può essere aperto per la scrittura una sola volta fino a quando il writer non chiude il file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1936">A file may be opened for reading multiple times, while a file can only be opened for writing once until the writer closes the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-1937">*È necessario fare attenzione se un file è aperto contemporaneamente per la lettura e la scrittura. La scrittura di file eseguita quando un file viene aperto contemporaneamente per la lettura potrebbe non essere visibile dal lettore, a meno che il lettore non chiuda e riapre il file per la lettura. Analogamente, il writer di file deve prestare attenzione quando si usano i servizi di troncamento dei file. Se un file viene troncato dal writer, i lettori dello stesso file potrebbero restituire dati non validi.*</span><span class="sxs-lookup"><span data-stu-id="9969a-1937">*Care must be taken if a file is concurrently open for reading and writing. File writing performed when a file is simultaneously opened for reading may not be seen by the reader, unless the reader closes and reopens the file for reading. Similarly, the file writer should be careful when using file truncate services. If a file is truncated by the writer, readers of the same file could return invalid data.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-1938">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-1938">Input Parameters</span></span>

- <span data-ttu-id="9969a-1939">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-1939">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-1940">**file_ptr:** puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1940">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="9969a-1941">**file_name:** puntatore al nome del file da aprire (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="9969a-1941">**file_name**: Pointer to the name of the file to open (directory path is optional).</span></span>
- <span data-ttu-id="9969a-1942">**open_type:** tipo di file aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1942">**open_type**: Type of file open.</span></span> <span data-ttu-id="9969a-1943">Le opzioni valide per i tipi aperti sono:</span><span class="sxs-lookup"><span data-stu-id="9969a-1943">Valid open type options are:</span></span>
  - <span data-ttu-id="9969a-1944">FX_OPEN_FOR_READ (0x00)</span><span class="sxs-lookup"><span data-stu-id="9969a-1944">FX_OPEN_FOR_READ (0x00)</span></span>
  - <span data-ttu-id="9969a-1945">FX_OPEN_FOR_WRITE (0x01)</span><span class="sxs-lookup"><span data-stu-id="9969a-1945">FX_OPEN_FOR_WRITE (0x01)</span></span>
  - <span data-ttu-id="9969a-1946">FX_OPEN_FOR_READ_FAST (0x02)</span><span class="sxs-lookup"><span data-stu-id="9969a-1946">FX_OPEN_FOR_READ_FAST (0x02)</span></span>

<span data-ttu-id="9969a-1947">L'apertura di file FX_OPEN_FOR_READ e FX_OPEN_FOR_READ_FAST è simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="9969a-1947">Opening files with FX_OPEN_FOR_READ and FX_OPEN_FOR_READ_FAST is similar:</span></span>

- <span data-ttu-id="9969a-1948">FX_OPEN_FOR_READ verifica che l'elenco collegato di cluster che costituiscono il file sia intatto e FX_OPEN_FOR_READ_FAST non esegue questa verifica, che lo rende più veloce.</span><span class="sxs-lookup"><span data-stu-id="9969a-1948">FX_OPEN_FOR_READ includes verification that the linked-list of clusters that comprise the file are intact, and FX_OPEN_FOR_READ_FAST does not perform this verification, which makes it faster.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-1949">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-1949">Return Values</span></span>

- <span data-ttu-id="9969a-1950">**FX_SUCCESS** (0x00) Apertura del file completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-1950">**FX_SUCCESS** (0x00) Successful file open.</span></span>
- <span data-ttu-id="9969a-1951">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-1951">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-1952">**FX_NOT_FOUND** (0x04) File specificato non trovato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1952">**FX_NOT_FOUND** (0x04) Specified file was not found.</span></span>
- <span data-ttu-id="9969a-1953">**FX_NOT_A_FILE** (0x05) Il nome file specificato è una directory o un volume.</span><span class="sxs-lookup"><span data-stu-id="9969a-1953">**FX_NOT_A_FILE** (0x05) Specified file name was a directory or volume.</span></span>
- <span data-ttu-id="9969a-1954">**FX_FILE_CORRUPT** (0x08) Il file specificato è danneggiato e l'apertura non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-1954">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the open failed.</span></span>
- <span data-ttu-id="9969a-1955">**FX_ACCESS_ERROR** (0x06) Il file specificato è già aperto o il tipo aperto non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1955">**FX_ACCESS_ERROR** (0x06) Specified file is already open or open type is invalid.</span></span>
- <span data-ttu-id="9969a-1956">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-1956">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-1957">**FX_MEDIA_INVALID** (0x02) Supporto non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1957">**FX_MEDIA_INVALID** (0x02) Invalid media.</span></span>
- <span data-ttu-id="9969a-1958">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-1958">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-1959">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-1959">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-1960">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-1960">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-1961">**FX_WRITE_PROTECT** (0x23) Il supporto sottostante è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-1961">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="9969a-1962">**FX_PTR_ERROR** (0x18) Supporto o puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-1962">**FX_PTR_ERROR** (0x18) Invalid media or file pointer.</span></span>
- <span data-ttu-id="9969a-1963">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-1963">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-1964">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-1964">Allowed From</span></span>

<span data-ttu-id="9969a-1965">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-1965">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-1966">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-1966">Example</span></span>

```c
FX_MEDIA     my_media;
FX_FILE     my_file;
UINT         status;

/* Open the file "myfile.txt" for reading. */

status = fx_file_open(&my_media, &my_file, "myfile.txt", FX_OPEN_FOR_READ);

/* If status equals FX_SUCCESS, file "myfile.txt" is now
    open and may be accessed now with the my_file pointer. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-1967">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-1967">See Also</span></span>

- <span data-ttu-id="9969a-1968">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1968">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-1969">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1969">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-1970">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1970">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-1971">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1971">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1972">fx_file_close- fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1972">fx_file_close- fx_file_create</span></span>
- <span data-ttu-id="9969a-1973">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1973">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-1974">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-1974">fx_file_delete</span></span>
- <span data-ttu-id="9969a-1975">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1975">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-1976">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-1976">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-1977">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1977">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-1978">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1978">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-1979">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1979">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-1980">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1980">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-1981">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1981">fx_file_read</span></span>
- <span data-ttu-id="9969a-1982">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1982">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-1983">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1983">fx_file_rename</span></span>
- <span data-ttu-id="9969a-1984">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-1984">fx_file_seek</span></span>
- <span data-ttu-id="9969a-1985">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-1985">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-1986">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-1986">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-1987">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-1987">fx_file_write</span></span>
- <span data-ttu-id="9969a-1988">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-1988">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-1989">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-1989">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-1990">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-1990">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-1991">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1991">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-1992">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-1992">fx_unicode_short_name_get</span></span>

## <a name="fx_file_read"></a><span data-ttu-id="9969a-1993">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-1993">fx_file_read</span></span>

<span data-ttu-id="9969a-1994">Legge i byte dal file</span><span class="sxs-lookup"><span data-stu-id="9969a-1994">Reads bytes from file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-1995">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-1995">Prototype</span></span>

```c
UINT fx_file_read(
    FX_FILE *file_ptr, 
    VOID *buffer_ptr,
    ULONG request_size, 
    ULONG *actual_size);
```
### <a name="description"></a><span data-ttu-id="9969a-1996">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-1996">Description</span></span>

<span data-ttu-id="9969a-1997">Questo servizio legge i byte dal file e li archivia nel buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-1997">This service reads bytes from the file and stores them in the supplied buffer.</span></span> <span data-ttu-id="9969a-1998">Al termine della lettura, il puntatore di lettura interno del file viene regolato in modo che punti al byte successivo nel file.</span><span class="sxs-lookup"><span data-stu-id="9969a-1998">After the read is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span> <span data-ttu-id="9969a-1999">Se nella richiesta rimane un numero inferiore di byte, solo i byte rimanenti vengono archiviati nel buffer.</span><span class="sxs-lookup"><span data-stu-id="9969a-1999">If there are fewer bytes remaining in the request, only the bytes remaining are stored in the buffer.</span></span> <span data-ttu-id="9969a-2000">In ogni caso, il numero totale di byte inseriti nel buffer viene restituito al chiamante.</span><span class="sxs-lookup"><span data-stu-id="9969a-2000">In any case, the total number of bytes placed in the buffer is returned to the caller.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-2001">*L'applicazione deve garantire che il buffer fornito sia in grado di archiviare il numero specificato di byte richiesti.*</span><span class="sxs-lookup"><span data-stu-id="9969a-2001">*The application must ensure that the buffer supplied is able to store the specified number of requested bytes.*</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-2002">*Si ottiene una maggiore velocità di prestazioni se il buffer di destinazione si trova su un limite di parole lunghe e le dimensioni richieste sono divisibile uniformemente per sizeof(**ULONG**).*</span><span class="sxs-lookup"><span data-stu-id="9969a-2002">*Faster performance is achieved if the destination buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2003">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2003">Input Parameters</span></span>

- <span data-ttu-id="9969a-2004">**file_ptr:** puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2004">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="9969a-2005">**buffer_ptr**: puntatore al buffer di destinazione per la lettura.</span><span class="sxs-lookup"><span data-stu-id="9969a-2005">**buffer_ptr**: Pointer to the destination buffer for the read.</span></span>
- <span data-ttu-id="9969a-2006">**request_size**: numero massimo di byte da leggere.</span><span class="sxs-lookup"><span data-stu-id="9969a-2006">**request_size**: Maximum number of bytes to read.</span></span>
- <span data-ttu-id="9969a-2007">**actual_size**: puntatore alla variabile per contenere il numero effettivo di byte letti nel buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2007">**actual_size**: Pointer to the variable to hold the actual number of bytes read into the supplied buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2008">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2008">Return Values</span></span>

- <span data-ttu-id="9969a-2009">**FX_SUCCESS** (0x00) Lettura file riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-2009">**FX_SUCCESS** (0x00) Successful file read.</span></span>
- <span data-ttu-id="9969a-2010">**FX_NOT_OPEN** (0x07) Il file specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2010">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="9969a-2011">**FX_FILE_CORRUPT** (0x08) Il file specificato è danneggiato e la lettura non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-2011">**FX_FILE_CORRUPT** (0x08) Specified file is corrupt and the read failed.</span></span>
- <span data-ttu-id="9969a-2012">**FX_END_OF_FILE** (0x09) È stata raggiunta la fine del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2012">**FX_END_OF_FILE** (0x09) End of file has been reached.</span></span>
- <span data-ttu-id="9969a-2013">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2013">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-2014">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-2014">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-2015">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2015">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2016">**FX_PTR_ERROR** (0x18) Puntatore a file o buffer non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2016">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="9969a-2017">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2017">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2018">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2018">Allowed From</span></span>

<span data-ttu-id="9969a-2019">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2019">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2020">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2020">Example</span></span>

```c
FX_FILE                 my_file;
unsigned char           my_buffer[1024];
ULONG                   actual_bytes;
UINT                    status;

/* Read up to 1024 bytes into "my_buffer." */
status = fx_file_read(&my_file, my_buffer, 1024, &actual_bytes);

/* If status equals FX_SUCCESS, "my_buffer" contains the bytes
    read from the file. The total number of bytes read is in "actual_bytes." */
```
### <a name="see-also"></a><span data-ttu-id="9969a-2021">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2021">See Also</span></span>

- <span data-ttu-id="9969a-2022">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2022">fx_file_allocate,</span></span>
- <span data-ttu-id="9969a-2023">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="9969a-2023">fx_file_attributes_read,</span></span>
- <span data-ttu-id="9969a-2024">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="9969a-2024">fx_file_attributes_set,</span></span>
- <span data-ttu-id="9969a-2025">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2025">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="9969a-2026">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="9969a-2026">fx_file_close,</span></span>
- <span data-ttu-id="9969a-2027">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="9969a-2027">fx_file_create,</span></span>
- <span data-ttu-id="9969a-2028">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="9969a-2028">fx_file_date_time_set,</span></span>
- <span data-ttu-id="9969a-2029">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="9969a-2029">fx_file_delete,</span></span>
- <span data-ttu-id="9969a-2030">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2030">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="9969a-2031">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2031">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="9969a-2032">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="9969a-2032">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="9969a-2033">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="9969a-2033">fx_file_extended_seek,</span></span>
- <span data-ttu-id="9969a-2034">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2034">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="9969a-2035">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="9969a-2035">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="9969a-2036">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="9969a-2036">fx_file_open,</span></span>
- <span data-ttu-id="9969a-2037">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="9969a-2037">fx_file_relative_seek,</span></span>
- <span data-ttu-id="9969a-2038">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="9969a-2038">fx_file_rename,</span></span>
- <span data-ttu-id="9969a-2039">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="9969a-2039">fx_file_seek,</span></span>
- <span data-ttu-id="9969a-2040">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2040">fx_file_truncate,</span></span>
- <span data-ttu-id="9969a-2041">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="9969a-2041">fx_file_truncate_release,</span></span>
- <span data-ttu-id="9969a-2042">fx_file_write,</span><span class="sxs-lookup"><span data-stu-id="9969a-2042">fx_file_write,</span></span>
- <span data-ttu-id="9969a-2043">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="9969a-2043">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="9969a-2044">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="9969a-2044">fx_unicode_file_create,</span></span>
- <span data-ttu-id="9969a-2045">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="9969a-2045">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="9969a-2046">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="9969a-2046">fx_unicode_name_get,</span></span>
- <span data-ttu-id="9969a-2047">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2047">fx_unicode_short_name_get</span></span>

## <a name="fx_file_relative_seek"></a><span data-ttu-id="9969a-2048">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2048">fx_file_relative_seek</span></span>

<span data-ttu-id="9969a-2049">Posizioni in base a un offset di byte relativo</span><span class="sxs-lookup"><span data-stu-id="9969a-2049">Positions to a relative byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2050">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2050">Prototype</span></span>

```c
UINT fx_file_relative_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset,
    UINT seek_from);
```
### <a name="description"></a><span data-ttu-id="9969a-2051">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2051">Description</span></span>

<span data-ttu-id="9969a-2052">Questo servizio posiziona il puntatore interno di lettura/scrittura del file all'offset di byte relativo specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2052">This service positions the internal file read/write pointer to the specified relative byte offset.</span></span> <span data-ttu-id="9969a-2053">Qualsiasi richiesta di lettura o scrittura di file successiva inizierà in questa posizione nel file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2053">Any subsequent file read or write request will begin at this location in the file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-2054">*Se l'operazione di ricerca tenta di cercare oltre la fine del file, il puntatore di lettura/scrittura del file viene posizionato alla fine del file. Viceversa, se l'operazione di ricerca tenta di posizionarsi oltre l'inizio del file, il puntatore di lettura/scrittura del file viene posizionato all'inizio del file.*</span><span class="sxs-lookup"><span data-stu-id="9969a-2054">*If the seek operation attempts to seek past the end of the file, the file's read/write pointer is positioned to the end of the file. Conversely, if the seek operation attempts to position past the beginning of the file, the file's read/write pointer is positioned to the beginning of the file.*</span></span>

<span data-ttu-id="9969a-2055">Per eseguire la ricerca con un valore di offset superiore a 4 GB, l'applicazione deve usare il *fx_file_extended_relative_seek*.</span><span class="sxs-lookup"><span data-stu-id="9969a-2055">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_relative_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2056">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2056">Input Parameters</span></span>

- <span data-ttu-id="9969a-2057">**file_ptr:** puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-2057">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="9969a-2058">**byte_offset:** offset dei byte relativo desiderato nel file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2058">**byte_offset**: Desired relative byte offset in file.</span></span>
- <span data-ttu-id="9969a-2059">**seek_from**: direzione e posizione della posizione da cui eseguire la ricerca relativa.</span><span class="sxs-lookup"><span data-stu-id="9969a-2059">**seek_from**: The direction and location of where to perform the relative seek from.</span></span> <span data-ttu-id="9969a-2060">Le opzioni di ricerca valide sono definite come segue:</span><span class="sxs-lookup"><span data-stu-id="9969a-2060">Valid seek options are defined as follows:</span></span>
  - <span data-ttu-id="9969a-2061">FX_SEEK_BEGIN (0x00)</span><span class="sxs-lookup"><span data-stu-id="9969a-2061">FX_SEEK_BEGIN (0x00)</span></span>
  - <span data-ttu-id="9969a-2062">FX_SEEK_END (0x01)</span><span class="sxs-lookup"><span data-stu-id="9969a-2062">FX_SEEK_END (0x01)</span></span>
  - <span data-ttu-id="9969a-2063">FX_SEEK_FORWARD (0x02)</span><span class="sxs-lookup"><span data-stu-id="9969a-2063">FX_SEEK_FORWARD (0x02)</span></span>
  - <span data-ttu-id="9969a-2064">FX_SEEK_BACK (0x03)</span><span class="sxs-lookup"><span data-stu-id="9969a-2064">FX_SEEK_BACK (0x03)</span></span>

<span data-ttu-id="9969a-2065">Se FX_SEEK_BEGIN specificato, l'operazione di ricerca viene eseguita dall'inizio del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2065">If FX_SEEK_BEGIN is specified, the seek operation is performed from the beginning of the file.</span></span> <span data-ttu-id="9969a-2066">Se FX_SEEK_END specificato, l'operazione di ricerca viene eseguita all'indietro a partire dalla fine del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2066">If FX_SEEK_END is specified the seek operation is performed backward from the end of the file.</span></span> <span data-ttu-id="9969a-2067">Se FX_SEEK_FORWARD specificato, l'operazione di ricerca viene eseguita in avanti dalla posizione corrente del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2067">If FX_SEEK_FORWARD is specified, the seek operation is performed forward from the current file position.</span></span> <span data-ttu-id="9969a-2068">Se FX_SEEK_BACK specificato, l'operazione di ricerca viene eseguita all'indietro dalla posizione corrente del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2068">If FX_SEEK_BACK is specified, the seek operation is performed backward from the current file position.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2069">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2069">Return Values</span></span>

- <span data-ttu-id="9969a-2070">**FX_SUCCESS** (0x00) Ricerca relativa al file completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-2070">**FX_SUCCESS** (0x00) Successful file relative seek.</span></span>
- <span data-ttu-id="9969a-2071">**FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2071">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="9969a-2072">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2072">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2073">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2073">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-2074">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2074">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-2075">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-2075">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-2076">**FX_PTR_ERROR** (0x18) Puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2076">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="9969a-2077">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2077">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2078">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2078">Allowed From</span></span>

<span data-ttu-id="9969a-2079">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2079">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2080">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2080">Example</span></span>

```c
FX_FILE     my_file;
UINT         status;

/* Attempt to move 10 bytes forward in "my_file". */

status = fx_file_relative_seek(&my_file, 10, FX_SEEK_FORWARD);

/* If status equals FX_SUCCESS, the file read/write pointers
    are positioned 10 bytes forward. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-2081">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2081">See Also</span></span>

- <span data-ttu-id="9969a-2082">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2082">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-2083">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2083">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-2084">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2084">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-2085">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2085">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2086">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2086">fx_file_close</span></span>
- <span data-ttu-id="9969a-2087">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2087">fx_file_create</span></span>
- <span data-ttu-id="9969a-2088">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2088">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-2089">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-2089">fx_file_delete</span></span>
- <span data-ttu-id="9969a-2090">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2090">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-2091">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2091">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2092">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2092">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-2093">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2093">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-2094">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2094">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-2095">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2095">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-2096">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2096">fx_file_open</span></span>
- <span data-ttu-id="9969a-2097">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2097">fx_file_read</span></span>
- <span data-ttu-id="9969a-2098">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2098">fx_file_rename</span></span>
- <span data-ttu-id="9969a-2099">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2099">fx_file_seek</span></span>
- <span data-ttu-id="9969a-2100">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2100">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-2101">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2101">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-2102">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2102">fx_file_write</span></span>
- <span data-ttu-id="9969a-2103">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2103">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-2104">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2104">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-2105">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2105">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-2106">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2106">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-2107">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2107">fx_unicode_short_name_get</span></span>

## <a name="fx_file_rename"></a><span data-ttu-id="9969a-2108">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2108">fx_file_rename</span></span>

<span data-ttu-id="9969a-2109">Rinomina il file</span><span class="sxs-lookup"><span data-stu-id="9969a-2109">Renames  file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2110">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2110">Prototype</span></span>

```c
UINT fx_file_rename(
    FX_MEDIA *media_ptr,
    CHAR *old_file_name,
    CHAR *new_file_name);
```
### <a name="description"></a><span data-ttu-id="9969a-2111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2111">Description</span></span>

<span data-ttu-id="9969a-2112">Questo servizio modifica il nome del file specificato da *old_file_name*.</span><span class="sxs-lookup"><span data-stu-id="9969a-2112">This service changes the name of the file specified by *old_file_name*.</span></span> <span data-ttu-id="9969a-2113">La ridenominazione viene eseguita anche in relazione al percorso specificato o al percorso predefinito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2113">Renaming is also done relative to the specified path or the default path.</span></span> <span data-ttu-id="9969a-2114">Se viene specificato un percorso nel nuovo nome file, il file rinominato viene effettivamente spostato nel percorso specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2114">If a path is specified in the new file name, the renamed file is effectively moved to the specified path.</span></span> <span data-ttu-id="9969a-2115">Se non viene specificato alcun percorso, il file rinominato viene inserito nel percorso predefinito corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-2115">If no path is specified, the renamed file is placed in the current default path.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2116">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2116">Input Parameters</span></span>

- <span data-ttu-id="9969a-2117">**media_ptr:** puntatore a un blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2117">**media_ptr**: Pointer to a media control block.</span></span>
- <span data-ttu-id="9969a-2118">**old_file_name:** puntatore al nome del file da rinominare (il percorso della directory è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="9969a-2118">**old_file_name**: Pointer to the name of the file to rename (directory path is optional).</span></span>
- <span data-ttu-id="9969a-2119">**new_file_name:** puntatore al nuovo nome file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2119">**new_file_name**: Pointer to the new file name.</span></span> <span data-ttu-id="9969a-2120">Il percorso della directory non è consentito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2120">The directory path is not allowed.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2121">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2121">Return Values</span></span>

- <span data-ttu-id="9969a-2122">**FX_SUCCESS** (0x00) Ridenominazione del file completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-2122">**FX_SUCCESS** (0x00) Successful file rename.</span></span>
- <span data-ttu-id="9969a-2123">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2123">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-2124">**FX_NOT_FOUND** (0x04) File specificato non trovato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2124">**FX_NOT_FOUND** (0x04)    Specified file was not found.</span></span>
- <span data-ttu-id="9969a-2125">**FX_NOT_A_FILE** (0x05) Il file specificato è una directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-2125">**FX_NOT_A_FILE** (0x05) Specified file is a directory.</span></span>
- <span data-ttu-id="9969a-2126">**FX_ACCESS_ERROR** (0x06) Il file specificato è già aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2126">**FX_ACCESS_ERROR** (0x06) Specified file is already open.</span></span>
- <span data-ttu-id="9969a-2127">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2127">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2128">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-2128">**FX_WRITE_PROTECT** (0x23)    Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-2129">**FX_INVALID_NAME** (0x0C) Il nuovo nome file specificato non è un nome di file valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2129">**FX_INVALID_NAME** (0x0C) Specified new file name is not a valid file name.</span></span>
- <span data-ttu-id="9969a-2130">**FX_INVALID_PATH** percorso (0x0D) non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2130">**FX_INVALID_PATH** (0x0D)    Path is invalid.</span></span>
- <span data-ttu-id="9969a-2131">**FX_ALREADY_CREATED** (0x0B) Viene usato il nuovo nome file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2131">**FX_ALREADY_CREATED** (0x0B) The new file name is used.</span></span>
- <span data-ttu-id="9969a-2132">**FX_MEDIA_INVALID** (0x02) Il supporto non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2132">**FX_MEDIA_INVALID** (0x02)    Media is invalid.</span></span>
- <span data-ttu-id="9969a-2133">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2133">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-2134">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2134">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-2135">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-2135">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-2136">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-2136">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-2137">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la tabella FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-2137">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="9969a-2138">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2138">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="9969a-2139">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2139">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2140">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2140">Allowed From</span></span>

<span data-ttu-id="9969a-2141">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2141">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2142">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2142">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Rename "myfile1.txt" to "myfile2.txt" in the default directory of the media. */

status = fx_file_rename(&my_media, "myfile1.txt", "myfile2.txt");

/* If status equals FX_SUCCESS, the file was successfully renamed. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-2143">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2143">See Also</span></span>

- <span data-ttu-id="9969a-2144">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2144">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-2145">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2145">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-2146">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2146">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-2147">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2147">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2148">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2148">fx_file_close</span></span>
- <span data-ttu-id="9969a-2149">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2149">fx_file_create</span></span>
- <span data-ttu-id="9969a-2150">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2150">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-2151">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-2151">fx_file_delete</span></span>
- <span data-ttu-id="9969a-2152">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2152">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-2153">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2153">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2154">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2154">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-2155">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2155">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-2156">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2156">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-2157">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2157">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-2158">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2158">fx_file_open</span></span>
- <span data-ttu-id="9969a-2159">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2159">fx_file_read</span></span>
- <span data-ttu-id="9969a-2160">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2160">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-2161">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2161">fx_file_seek</span></span>
- <span data-ttu-id="9969a-2162">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2162">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-2163">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2163">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-2164">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2164">fx_file_write</span></span>
- <span data-ttu-id="9969a-2165">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2165">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-2166">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2166">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-2167">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2167">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-2168">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2168">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-2169">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2169">fx_unicode_short_name_get</span></span>

## <a name="fx_file_seek"></a><span data-ttu-id="9969a-2170">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2170">fx_file_seek</span></span>

<span data-ttu-id="9969a-2171">Posizioni all'offset di byte</span><span class="sxs-lookup"><span data-stu-id="9969a-2171">Positions to byte offset</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2172">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2172">Prototype</span></span>

```c
UINT fx_file_seek(
    FX_FILE *file_ptr,
    ULONG byte_offset);
```
### <a name="description"></a><span data-ttu-id="9969a-2173">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2173">Description</span></span>

<span data-ttu-id="9969a-2174">Questo servizio posiziona il puntatore di lettura/scrittura del file interno all'offset di byte specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2174">This service positions the internal file read/write pointer to the specified byte offset.</span></span> <span data-ttu-id="9969a-2175">Qualsiasi richiesta di lettura o scrittura di file successiva inizierà in questa posizione nel file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2175">Any subsequent file read or write request will begin at this location in the file.</span></span>

<span data-ttu-id="9969a-2176">Per cercare con un valore di offset superiore a 4 GB, l'applicazione deve usare il *servizio* fx_file_extended_seek .</span><span class="sxs-lookup"><span data-stu-id="9969a-2176">To seek with an offset value beyond 4GB, application shall use the service *fx_file_extended_seek*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2177">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2177">Input Parameters</span></span>

- <span data-ttu-id="9969a-2178">**file_ptr:** puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2178">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="9969a-2179">**byte_offset:** offset di byte desiderato nel file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2179">**byte_offset**: Desired byte offset in file.</span></span> <span data-ttu-id="9969a-2180">Un valore pari a zero posizionerà il puntatore in lettura/scrittura all'inizio del file, mentre un valore maggiore delle dimensioni del file posizionerà il puntatore di lettura/scrittura alla fine del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2180">A value of zero will position the read/write pointer at the beginning of the file, while a value greater than the file's size will position the read/write pointer at the end of the file.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2181">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2181">Return Values</span></span>

- <span data-ttu-id="9969a-2182">**FX_SUCCESS** (0x00) Ricerca file riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-2182">**FX_SUCCESS** (0x00) Successful file seek.</span></span>
- <span data-ttu-id="9969a-2183">**FX_NOT_OPEN** (0x07) Il file specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2183">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="9969a-2184">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2184">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2185">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2185">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-2186">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2186">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-2187">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-2187">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-2188">**FX_PTR_ERROR** (0x18) Puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2188">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="9969a-2189">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2189">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2190">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2190">Allowed From</span></span>

<span data-ttu-id="9969a-2191">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2191">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2192">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2192">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Seek to the beginning of "my_file." */
status = fx_file_seek(&my_file, 0);
/* If status equals FX_SUCCESS, the file read/write pointer
    is now positioned to the beginning of the file. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-2193">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2193">See Also</span></span>

- <span data-ttu-id="9969a-2194">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2194">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-2195">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2195">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-2196">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2196">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-2197">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2197">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2198">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2198">fx_file_close</span></span>
- <span data-ttu-id="9969a-2199">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2199">fx_file_create</span></span>
- <span data-ttu-id="9969a-2200">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2200">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-2201">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-2201">fx_file_delete</span></span>
- <span data-ttu-id="9969a-2202">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2202">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-2203">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2203">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2204">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2204">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-2205">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2205">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-2206">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2206">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-2207">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2207">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-2208">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2208">fx_file_open</span></span>
- <span data-ttu-id="9969a-2209">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2209">fx_file_read</span></span>
- <span data-ttu-id="9969a-2210">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2210">fx_file_rename</span></span>
- <span data-ttu-id="9969a-2211">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2211">fx_file_seek</span></span>
- <span data-ttu-id="9969a-2212">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2212">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-2213">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2213">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-2214">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2214">fx_file_write</span></span>
- <span data-ttu-id="9969a-2215">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2215">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-2216">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2216">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-2217">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2217">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-2218">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2218">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-2219">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2219">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate"></a><span data-ttu-id="9969a-2220">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2220">fx_file_truncate</span></span>

<span data-ttu-id="9969a-2221">Tronca il file</span><span class="sxs-lookup"><span data-stu-id="9969a-2221">Truncates file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2222">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2222">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```

### <a name="description"></a><span data-ttu-id="9969a-2223">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2223">Description</span></span>

<span data-ttu-id="9969a-2224">Questo servizio tronca le dimensioni del file alle dimensioni specificate.</span><span class="sxs-lookup"><span data-stu-id="9969a-2224">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="9969a-2225">Se le dimensioni fornite sono maggiori delle dimensioni effettive del file, questo servizio non fa nulla.</span><span class="sxs-lookup"><span data-stu-id="9969a-2225">If the supplied size is greater than the actual file size, this service doesn't do anything.</span></span> <span data-ttu-id="9969a-2226">Nessuno dei cluster multimediali associati al file viene rilasciato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2226">None of the media clusters associated with the file are released.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-2227">*Prestare attenzione al troncamento dei file che possono essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*</span><span class="sxs-lookup"><span data-stu-id="9969a-2227">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="9969a-2228">Per operare oltre 4 GB, l'applicazione userà il servizio *fx_file_extended_truncate*.</span><span class="sxs-lookup"><span data-stu-id="9969a-2228">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2229">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2229">Input Parameters</span></span>

- <span data-ttu-id="9969a-2230">**file_ptr:** puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2230">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="9969a-2231">**size:** nuove dimensioni del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2231">**size**: New file size.</span></span> <span data-ttu-id="9969a-2232">I byte oltre questa nuova dimensione di file vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="9969a-2232">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2233">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2233">Return Values</span></span>

- <span data-ttu-id="9969a-2234">**FX_SUCCESS** (0x00) Troncamento del file riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2234">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="9969a-2235">**FX_NOT_OPEN** (0x07) Il file specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2235">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="9969a-2236">**FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-2236">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="9969a-2237">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2237">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2238">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-2238">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-2239">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2239">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-2240">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2240">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-2241">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-2241">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-2242">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione</span><span class="sxs-lookup"><span data-stu-id="9969a-2242">**FX_NO_MORE_SPACE** (0x0A) No more space to complete the operation</span></span>
- <span data-ttu-id="9969a-2243">**FX_PTR_ERROR** (0x18) Puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2243">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="9969a-2244">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2244">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2245">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2245">Allowed From</span></span>

<span data-ttu-id="9969a-2246">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2246">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2247">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2247">Example</span></span>

```c
FX_FILE                my_file;
UINT                status;
/* Truncate "my_file" to 100 bytes. */

status = fx_file_truncate(&my_file, 100);

/* If status equals FX_SUCCESS, "my_file" contains 100 or fewer bytes. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-2248">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2248">See Also</span></span>

- <span data-ttu-id="9969a-2249">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2249">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-2250">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2250">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-2251">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2251">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-2252">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2252">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2253">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2253">fx_file_close</span></span>
- <span data-ttu-id="9969a-2254">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2254">fx_file_create</span></span>
- <span data-ttu-id="9969a-2255">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2255">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-2256">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-2256">fx_file_delete</span></span>
- <span data-ttu-id="9969a-2257">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2257">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-2258">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2258">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2259">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2259">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-2260">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2260">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-2261">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2261">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-2262">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2262">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-2263">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2263">fx_file_open</span></span>
- <span data-ttu-id="9969a-2264">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2264">fx_file_read</span></span>
- <span data-ttu-id="9969a-2265">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2265">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-2266">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2266">fx_file_rename</span></span>
- <span data-ttu-id="9969a-2267">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2267">fx_file_seek</span></span>
- <span data-ttu-id="9969a-2268">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2268">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-2269">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2269">fx_file_write</span></span>
- <span data-ttu-id="9969a-2270">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2270">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-2271">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2271">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-2272">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2272">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-2273">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2273">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-2274">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2274">fx_unicode_short_name_get</span></span>

## <a name="fx_file_truncate_release"></a><span data-ttu-id="9969a-2275">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2275">fx_file_truncate_release</span></span>

<span data-ttu-id="9969a-2276">Tronca i file e rilascia i cluster</span><span class="sxs-lookup"><span data-stu-id="9969a-2276">Truncates file and releases cluster(s)</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2277">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2277">Prototype</span></span>

```c
UINT fx_file_truncate(
    FX_FILE *file_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="9969a-2278">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2278">Description</span></span>

<span data-ttu-id="9969a-2279">Questo servizio tronca le dimensioni del file alle dimensioni specificate.</span><span class="sxs-lookup"><span data-stu-id="9969a-2279">This service truncates the size of the file to the specified size.</span></span> <span data-ttu-id="9969a-2280">Se le dimensioni fornite sono maggiori delle dimensioni effettive del file, questo servizio non esegue alcun'operazione.</span><span class="sxs-lookup"><span data-stu-id="9969a-2280">If the supplied size is greater than the actual file size, this service does not do anything.</span></span> <span data-ttu-id="9969a-2281">A differenza ***del fx_file_truncate,*** questo servizio rilascia tutti i cluster inutilizzati.</span><span class="sxs-lookup"><span data-stu-id="9969a-2281">Unlike the ***fx_file_truncate*** service, this service does release any unused clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-2282">*Prestare attenzione al troncamento dei file che possono essere aperti contemporaneamente per la lettura. Il troncamento di un file aperto anche per la lettura può comportare la lettura di dati non validi.*</span><span class="sxs-lookup"><span data-stu-id="9969a-2282">*Use caution truncating files that may also be simultaneously open for reading. Truncating a file also opened for reading can result in reading invalid data.*</span></span>

<span data-ttu-id="9969a-2283">Per operare oltre 4 GB, l'applicazione userà il servizio *fx_file_extended_truncate_release*.</span><span class="sxs-lookup"><span data-stu-id="9969a-2283">To operate beyond 4GB, application shall use the service *fx_file_extended_truncate_release*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2284">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2284">Input Parameters</span></span>

- <span data-ttu-id="9969a-2285">**file_ptr:** puntatore a un file aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-2285">**file_ptr**: Pointer to a previously opened file.</span></span>
- <span data-ttu-id="9969a-2286">**size:** nuove dimensioni del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2286">**size**: New file size.</span></span> <span data-ttu-id="9969a-2287">I byte oltre questa nuova dimensione di file vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="9969a-2287">Bytes past this new file size are discarded.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2288">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2288">Return Values</span></span>

- <span data-ttu-id="9969a-2289">**FX_SUCCESS** (0x00) Troncamento del file riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2289">**FX_SUCCESS** (0x00) Successful file truncate.</span></span>
- <span data-ttu-id="9969a-2290">**FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-2290">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="9969a-2291">**FX_NOT_OPEN** (0x07) Il file specificato non è attualmente aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2291">**FX_NOT_OPEN** (0x07) Specified file is not currently open.</span></span>
- <span data-ttu-id="9969a-2292">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2292">**FX_IO_ERROR** (0x90)    Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2293">**FX_WRITE_PROTECT** (0x23) Il supporto sottostante è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-2293">**FX_WRITE_PROTECT** (0x23) Underlying media is write protected.</span></span>
- <span data-ttu-id="9969a-2294">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2294">**FX_FILE_CORRUPT** (0x08)    File is corrupted.</span></span>
- <span data-ttu-id="9969a-2295">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2295">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-2296">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-2296">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-2297">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-2297">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-2298">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="9969a-2298">**FX_NO_MORE_SPACE** (0x0A)    No more space to complete the operation.</span></span>
- <span data-ttu-id="9969a-2299">**FX_PTR_ERROR** (0x18) Puntatore di file non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2299">**FX_PTR_ERROR** (0x18) Invalid file pointer.</span></span>
- <span data-ttu-id="9969a-2300">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2300">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2301">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2301">Allowed From</span></span>

<span data-ttu-id="9969a-2302">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2302">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2303">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2303">Example</span></span>

```c
FX_FILE         my_file;
UINT             status;

/* Attempt to truncate everything after the first 100 bytes of "my_file". */

status = fx_file_truncate_release(&my_file, 100);

/* If status equals FX_SUCCESS, the file is now 100 bytes
    or fewer and all unused clusters have been released. */
```
### <a name="see-also"></a><span data-ttu-id="9969a-2304">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2304">See Also</span></span>

- <span data-ttu-id="9969a-2305">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2305">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-2306">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2306">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-2307">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2307">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-2308">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2308">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2309">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2309">fx_file_close</span></span>
- <span data-ttu-id="9969a-2310">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2310">fx_file_create</span></span>
- <span data-ttu-id="9969a-2311">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2311">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-2312">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-2312">fx_file_delete</span></span>
- <span data-ttu-id="9969a-2313">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2313">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-2314">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2314">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2315">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2315">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-2316">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2316">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-2317">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2317">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-2318">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2318">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-2319">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2319">fx_file_open</span></span>
- <span data-ttu-id="9969a-2320">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2320">fx_file_read</span></span>
- <span data-ttu-id="9969a-2321">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2321">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-2322">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2322">fx_file_rename</span></span>
- <span data-ttu-id="9969a-2323">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2323">fx_file_seek</span></span>
- <span data-ttu-id="9969a-2324">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2324">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-2325">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2325">fx_file_write</span></span>
- <span data-ttu-id="9969a-2326">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2326">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-2327">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2327">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-2328">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2328">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-2329">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2329">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-2330">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2330">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write"></a><span data-ttu-id="9969a-2331">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2331">fx_file_write</span></span>

<span data-ttu-id="9969a-2332">Scrive byte nel file</span><span class="sxs-lookup"><span data-stu-id="9969a-2332">Writes bytes to file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2333">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2333">Prototype</span></span>

```c
UINT fx_file_write(
    FX_FILE *file_ptr,
    VOID *buffer_ptr,
    ULONG size);
```
### <a name="description"></a><span data-ttu-id="9969a-2334">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2334">Description</span></span>

<span data-ttu-id="9969a-2335">Questo servizio scrive byte dal buffer specificato a partire dalla posizione corrente del file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2335">This service writes bytes from the specified buffer starting at the file's current position.</span></span> <span data-ttu-id="9969a-2336">Al termine della scrittura, il puntatore di lettura interno del file viene regolato in modo che punti al byte successivo nel file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2336">After the write is complete, the file's internal read pointer is adjusted to point at the next byte in the file.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-2337">*Si ottiene prestazioni più veloci se il buffer di origine si trova su un limite di parole lunghe e le dimensioni richieste sono divisibile uniformemente per sizeof(**ULONG**).*</span><span class="sxs-lookup"><span data-stu-id="9969a-2337">*Faster performance is achieved if the source buffer is on a long-word boundary and the requested size is evenly divisible by sizeof(**ULONG**).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2338">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2338">Input Parameters</span></span>

- <span data-ttu-id="9969a-2339">**file_ptr:** puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2339">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="9969a-2340">**buffer_ptr**: puntatore al buffer di origine per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-2340">**buffer_ptr**: Pointer to the source buffer for the write.</span></span>
- <span data-ttu-id="9969a-2341">**size:** numero di byte da scrivere.</span><span class="sxs-lookup"><span data-stu-id="9969a-2341">**size**: Number of bytes to write.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2342">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2342">Return Values</span></span>

- <span data-ttu-id="9969a-2343">**FX_SUCCESS** (0x00) Scrittura del file riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-2343">**FX_SUCCESS** (0x00) Successful file write.</span></span>
- <span data-ttu-id="9969a-2344">**FX_NOT_OPEN** (0x07) Il file specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2344">**FX_NOT_OPEN** (0x07) Specified file is not open.</span></span>
- <span data-ttu-id="9969a-2345">**FX_ACCESS_ERROR** (0x06) Il file specificato non è aperto per la scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-2345">**FX_ACCESS_ERROR** (0x06) Specified file is not open for writing.</span></span>
- <span data-ttu-id="9969a-2346">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio nei supporti per eseguire questa scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-2346">**FX_NO_MORE_SPACE** (0x0A) There is no more room available in the media to perform this write.</span></span>
- <span data-ttu-id="9969a-2347">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2347">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2348">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-2348">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-2349">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2349">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-2350">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2350">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-2351">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la voce FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-2351">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT entry.</span></span>
- <span data-ttu-id="9969a-2352">**FX_NO_MORE_ENTRIES** (0x0F) Non sono più presenti voci FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-2352">**FX_NO_MORE_ENTRIES** (0x0F) No more FAT entries.</span></span>
- <span data-ttu-id="9969a-2353">**FX_PTR_ERROR** (0x18) Puntatore al file o al buffer non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2353">**FX_PTR_ERROR** (0x18) Invalid file or buffer pointer.</span></span>
- <span data-ttu-id="9969a-2354">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2354">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2355">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2355">Allowed From</span></span>

<span data-ttu-id="9969a-2356">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2356">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2357">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2357">Example</span></span>

```c
FX_FILE            my_file;
UINT            status;
/* Write a 10 character buffer to "my_file." */

status = fx_file_write(&my_file, "1234567890", 10);

/* If status equals FX_SUCCESS, the small text string was written out to the file. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-2358">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2358">See Also</span></span>

- <span data-ttu-id="9969a-2359">fx_file_allocate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2359">fx_file_allocate,</span></span>
- <span data-ttu-id="9969a-2360">fx_file_attributes_read,</span><span class="sxs-lookup"><span data-stu-id="9969a-2360">fx_file_attributes_read,</span></span>
- <span data-ttu-id="9969a-2361">fx_file_attributes_set,</span><span class="sxs-lookup"><span data-stu-id="9969a-2361">fx_file_attributes_set,</span></span>
- <span data-ttu-id="9969a-2362">fx_file_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2362">fx_file_best_effort_allocate,</span></span>
- <span data-ttu-id="9969a-2363">fx_file_close,</span><span class="sxs-lookup"><span data-stu-id="9969a-2363">fx_file_close,</span></span>
- <span data-ttu-id="9969a-2364">fx_file_create,</span><span class="sxs-lookup"><span data-stu-id="9969a-2364">fx_file_create,</span></span>
- <span data-ttu-id="9969a-2365">fx_file_date_time_set,</span><span class="sxs-lookup"><span data-stu-id="9969a-2365">fx_file_date_time_set,</span></span>
- <span data-ttu-id="9969a-2366">fx_file_delete,</span><span class="sxs-lookup"><span data-stu-id="9969a-2366">fx_file_delete,</span></span>
- <span data-ttu-id="9969a-2367">fx_file_extended_allocate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2367">fx_file_extended_allocate,</span></span>
- <span data-ttu-id="9969a-2368">fx_file_extended_best_effort_allocate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2368">fx_file_extended_best_effort_allocate,</span></span>
- <span data-ttu-id="9969a-2369">fx_file_extended_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="9969a-2369">fx_file_extended_relative_seek,</span></span>
- <span data-ttu-id="9969a-2370">fx_file_extended_seek,</span><span class="sxs-lookup"><span data-stu-id="9969a-2370">fx_file_extended_seek,</span></span>
- <span data-ttu-id="9969a-2371">fx_file_extended_truncate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2371">fx_file_extended_truncate,</span></span>
- <span data-ttu-id="9969a-2372">fx_file_extended_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="9969a-2372">fx_file_extended_truncate_release,</span></span>
- <span data-ttu-id="9969a-2373">fx_file_open,</span><span class="sxs-lookup"><span data-stu-id="9969a-2373">fx_file_open,</span></span>
- <span data-ttu-id="9969a-2374">fx_file_read,</span><span class="sxs-lookup"><span data-stu-id="9969a-2374">fx_file_read,</span></span>
- <span data-ttu-id="9969a-2375">fx_file_relative_seek,</span><span class="sxs-lookup"><span data-stu-id="9969a-2375">fx_file_relative_seek,</span></span>
- <span data-ttu-id="9969a-2376">fx_file_rename,</span><span class="sxs-lookup"><span data-stu-id="9969a-2376">fx_file_rename,</span></span>
- <span data-ttu-id="9969a-2377">fx_file_seek,</span><span class="sxs-lookup"><span data-stu-id="9969a-2377">fx_file_seek,</span></span>
- <span data-ttu-id="9969a-2378">fx_file_truncate,</span><span class="sxs-lookup"><span data-stu-id="9969a-2378">fx_file_truncate,</span></span>
- <span data-ttu-id="9969a-2379">fx_file_truncate_release,</span><span class="sxs-lookup"><span data-stu-id="9969a-2379">fx_file_truncate_release,</span></span>
- <span data-ttu-id="9969a-2380">fx_file_write_notify_set,</span><span class="sxs-lookup"><span data-stu-id="9969a-2380">fx_file_write_notify_set,</span></span>
- <span data-ttu-id="9969a-2381">fx_unicode_file_create,</span><span class="sxs-lookup"><span data-stu-id="9969a-2381">fx_unicode_file_create,</span></span>
- <span data-ttu-id="9969a-2382">fx_unicode_file_rename,</span><span class="sxs-lookup"><span data-stu-id="9969a-2382">fx_unicode_file_rename,</span></span>
- <span data-ttu-id="9969a-2383">fx_unicode_name_get,</span><span class="sxs-lookup"><span data-stu-id="9969a-2383">fx_unicode_name_get,</span></span>
- <span data-ttu-id="9969a-2384">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2384">fx_unicode_short_name_get</span></span>

## <a name="fx_file_write_notify_set"></a><span data-ttu-id="9969a-2385">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2385">fx_file_write_notify_set</span></span>

<span data-ttu-id="9969a-2386">Imposta la funzione di notifica della scrittura di file</span><span class="sxs-lookup"><span data-stu-id="9969a-2386">Sets the file write notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2387">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2387">Prototype</span></span>

```c
UINT fx_file_write_notify_set(
    FX_FILE *file_ptr,
    VOID (*file_write_notify)(FX_FILE*));
```
### <a name="description"></a><span data-ttu-id="9969a-2388">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2388">Description</span></span>

<span data-ttu-id="9969a-2389">Questo servizio installa la funzione di callback richiamata dopo un'operazione di scrittura di file riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-2389">This service installs callback function that is invoked after a successful file write operation.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2390">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2390">Input Parameters</span></span>

- <span data-ttu-id="9969a-2391">**file_ptr:** puntatore al blocco di controllo file.</span><span class="sxs-lookup"><span data-stu-id="9969a-2391">**file_ptr**: Pointer to the file control block.</span></span>
- <span data-ttu-id="9969a-2392">**file_write_notify:** funzione di callback di scrittura file da installare.</span><span class="sxs-lookup"><span data-stu-id="9969a-2392">**file_write_notify**: File write callback function to be installed.</span></span> <span data-ttu-id="9969a-2393">Impostare la funzione di callback su NULL per disabilitare la funzione di callback.</span><span class="sxs-lookup"><span data-stu-id="9969a-2393">Set the callback function to NULL disables the callback function.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2394">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2394">Return Values</span></span>

- <span data-ttu-id="9969a-2395">**FX_SUCCESS** (0x00) La funzione di callback è stata installata correttamente.</span><span class="sxs-lookup"><span data-stu-id="9969a-2395">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="9969a-2396">**FX_PTR_ERROR** (0x18) file_ptr è NULL.</span><span class="sxs-lookup"><span data-stu-id="9969a-2396">**FX_PTR_ERROR** (0x18) file_ptr is NULL.</span></span>
- <span data-ttu-id="9969a-2397">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2397">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2398">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2398">Allowed From</span></span>

<span data-ttu-id="9969a-2399">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2399">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2400">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2400">Example</span></span>

```c
fx_file_write_notify_set(file_ptr, my_file_close_callback);

```

### <a name="see-also"></a><span data-ttu-id="9969a-2401">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2401">See Also</span></span>

- <span data-ttu-id="9969a-2402">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2402">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-2403">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2403">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-2404">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2404">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-2405">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2405">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2406">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2406">fx_file_close</span></span>
- <span data-ttu-id="9969a-2407">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2407">fx_file_create</span></span>
- <span data-ttu-id="9969a-2408">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2408">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-2409">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-2409">fx_file_delete</span></span>
- <span data-ttu-id="9969a-2410">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2410">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-2411">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-2411">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-2412">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2412">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-2413">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2413">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-2414">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2414">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-2415">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2415">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-2416">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2416">fx_file_open</span></span>
- <span data-ttu-id="9969a-2417">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2417">fx_file_read</span></span>
- <span data-ttu-id="9969a-2418">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2418">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-2419">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2419">fx_file_rename</span></span>
- <span data-ttu-id="9969a-2420">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-2420">fx_file_seek</span></span>
- <span data-ttu-id="9969a-2421">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-2421">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-2422">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-2422">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-2423">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2423">fx_file_write</span></span>
- <span data-ttu-id="9969a-2424">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-2424">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-2425">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-2425">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-2426">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2426">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-2427">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2427">fx_unicode_short_name_get</span></span>

## <a name="fx_media_abort"></a><span data-ttu-id="9969a-2428">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2428">fx_media_abort</span></span>

<span data-ttu-id="9969a-2429">Interrompe le attività multimediali</span><span class="sxs-lookup"><span data-stu-id="9969a-2429">Aborts media activities</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2430">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2430">Prototype</span></span>

```c
UINT fx_media_abort(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="9969a-2431">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2431">Description</span></span>

<span data-ttu-id="9969a-2432">Questo servizio interrompe tutte le attività correnti associate al supporto, tra cui la chiusura di tutti i file aperti, l'invio di una richiesta di interruzione al driver associato e l'inserimento dei supporti in uno stato interrotto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2432">This service aborts all current activities associated with the media, including closing all open files, sending an abort request to the associated driver, and placing the media in an aborted state.</span></span> <span data-ttu-id="9969a-2433">Questo servizio viene in genere chiamato quando vengono rilevati errori di I/O.</span><span class="sxs-lookup"><span data-stu-id="9969a-2433">This service is typically called when I/O errors are detected.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-2434">*Il supporto deve essere riaperto per poterlo usare nuovamente dopo l'esecuzione di un'operazione di interruzione.*</span><span class="sxs-lookup"><span data-stu-id="9969a-2434">*The media must be re-opened to use it again after an abort operation is performed.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2435">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2435">Input Parameters</span></span>

- <span data-ttu-id="9969a-2436">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2436">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2437">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2437">Return Values</span></span>

- <span data-ttu-id="9969a-2438">**FX_SUCCESS** (0x00) Interruzione del supporto riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-2438">**FX_SUCCESS** (0x00) Successful media abort.</span></span>
- <span data-ttu-id="9969a-2439">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2439">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-2440">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2440">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="9969a-2441">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2441">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2442">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2442">Allowed From</span></span>

<span data-ttu-id="9969a-2443">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2443">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2444">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2444">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Abort all activity associated with "my_media". */

status = fx_media_abort(&my_media);

/* If status equals FX_SUCCESS, all activity
    associated with the media has been aborted. */

```

### <a name="see-also"></a><span data-ttu-id="9969a-2445">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2445">See Also</span></span>

- <span data-ttu-id="9969a-2446">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2446">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2447">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2447">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2448">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2448">fx_media_check</span></span>
- <span data-ttu-id="9969a-2449">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2449">fx_media_close</span></span>
- <span data-ttu-id="9969a-2450">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2450">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2451">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2451">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2452">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2452">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2453">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2453">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2454">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2454">fx_media_format</span></span>
- <span data-ttu-id="9969a-2455">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2455">fx_media_open</span></span>
- <span data-ttu-id="9969a-2456">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2456">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2457">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2457">fx_media_read</span></span>
- <span data-ttu-id="9969a-2458">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2458">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2459">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2459">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2460">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2460">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2461">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2461">fx_media_write</span></span>
- <span data-ttu-id="9969a-2462">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2462">fx_system_initialize</span></span>

## <a name="fx_media_cache_invalidate"></a><span data-ttu-id="9969a-2463">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2463">fx_media_cache_invalidate</span></span>

<span data-ttu-id="9969a-2464">Invalida la cache dei settori logici</span><span class="sxs-lookup"><span data-stu-id="9969a-2464">Invalidates logical sector cache</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2465">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2465">Prototype</span></span>

```c
UINT fx_media_cache_invalidate(FX_MEDIA *media_ptr);
```

### <a name="description"></a><span data-ttu-id="9969a-2466">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2466">Description</span></span>

<span data-ttu-id="9969a-2467">Questo servizio scarica tutti i settori dirty nella cache e quindi invalida l'intera cache dei settori logici.</span><span class="sxs-lookup"><span data-stu-id="9969a-2467">This service flushes all dirty sectors in the cache and then invalidates the entire logical sector cache.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2468">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2468">Input Parameters</span></span>

- <span data-ttu-id="9969a-2469">**media_ptr:** Puntatore al blocco di controllo multimediale</span><span class="sxs-lookup"><span data-stu-id="9969a-2469">**media_ptr**: Pointer to media control block</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2470">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2470">Return Values</span></span>

- <span data-ttu-id="9969a-2471">**FX_SUCCESS** (0x00) Invalidate la cache dei supporti riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-2471">**FX_SUCCESS** (0x00) Successful media cache invalidate.</span></span>
- <span data-ttu-id="9969a-2472">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2472">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-2473">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2473">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2474">**FX_PTR_ERROR** (0x18) Supporto o puntatore scratch non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2474">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="9969a-2475">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2475">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2476">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2476">Allowed From</span></span>

<span data-ttu-id="9969a-2477">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2477">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2478">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2478">Example</span></span>

```c
FX_MEDIA     my_media;

/* Invalidate the cache of the media. */
status = fx_media_cache_invalidate(&my_media);

/* If status is FX_SUCCESS the cache in the media
    was successfully flushed and invalidated. */

```

### <a name="see-also"></a><span data-ttu-id="9969a-2479">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2479">See Also</span></span>

- <span data-ttu-id="9969a-2480">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2480">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2481">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2481">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2482">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2482">fx_media_check</span></span>
- <span data-ttu-id="9969a-2483">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2483">fx_media_close</span></span>
- <span data-ttu-id="9969a-2484">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2484">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2485">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2485">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2486">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2486">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2487">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2487">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2488">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2488">fx_media_format</span></span>
- <span data-ttu-id="9969a-2489">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2489">fx_media_open</span></span>
- <span data-ttu-id="9969a-2490">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2490">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2491">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2491">fx_media_read</span></span>
- <span data-ttu-id="9969a-2492">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2492">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2493">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2493">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2494">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2494">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2495">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2495">fx_media_write</span></span>
- <span data-ttu-id="9969a-2496">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2496">fx_system_initialize</span></span>

## <a name="fx_media_check"></a><span data-ttu-id="9969a-2497">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2497">fx_media_check</span></span>

<span data-ttu-id="9969a-2498">Controlla la presenza di errori nei supporti</span><span class="sxs-lookup"><span data-stu-id="9969a-2498">Checks media for errors</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2499">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2499">Prototype</span></span>

```c
UINT fx_media_check(
    FX_MEDIA *media_ptr,
    UCHAR *scratch_memory_ptr,
    ULONG scratch_memory_size,
    ULONG error_correction_option,
    ULONG *errors_detected_ptr);
```
### <a name="description"></a><span data-ttu-id="9969a-2500">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2500">Description</span></span>

<span data-ttu-id="9969a-2501">Questo servizio controlla i supporti specificati per verificare la presenza di errori strutturali di base, tra cui collegamento incrociato file/directory, catene FAT non valide e cluster persi.</span><span class="sxs-lookup"><span data-stu-id="9969a-2501">This service checks the specified media for basic structural errors, including file/directory cross-linking, invalid FAT chains, and lost clusters.</span></span> <span data-ttu-id="9969a-2502">Questo servizio offre anche la possibilità di correggere gli errori rilevati.</span><span class="sxs-lookup"><span data-stu-id="9969a-2502">This service also provides the capability to correct detected errors.</span></span>

<span data-ttu-id="9969a-2503">Il fx_media_check richiede memoria scratch per l'analisi approfondita delle directory e dei file nei supporti.</span><span class="sxs-lookup"><span data-stu-id="9969a-2503">The fx_media_check service requires scratch memory for its depth-first analysis of directories and files in the media.</span></span> <span data-ttu-id="9969a-2504">In particolare, la memoria scratch fornita al servizio di controllo dei supporti deve essere sufficientemente grande da contenere diverse voci di directory, una struttura di dati per "impilare" la posizione corrente della voce di directory prima di entrare nelle sottodirectory e infine la mappa di bit FAT logica.</span><span class="sxs-lookup"><span data-stu-id="9969a-2504">Specifically, the scratch memory supplied to the media check service must be large enough to hold several directory entries, a data structure to "stack" the current directory entry position before entering into subdirectories, and finally the logical FAT bit map.</span></span> <span data-ttu-id="9969a-2505">La memoria scratch deve essere di almeno 512-1024 byte più memoria per la mappa di bit FAT logica, che richiede tutti i bit quanti sono i cluster nei supporti.</span><span class="sxs-lookup"><span data-stu-id="9969a-2505">The scratch memory should be at least 512-1024 bytes plus memory for the logical FAT bit map, which requires as many bits as there are clusters in the media.</span></span> <span data-ttu-id="9969a-2506">Ad esempio, un dispositivo con 8000 cluster richiederebbe 1000 byte per rappresentare e quindi richiedere un'area scratch totale nell'ordine di 2048 byte.</span><span class="sxs-lookup"><span data-stu-id="9969a-2506">For example, a device with 8000 clusters would require 1000 bytes to represent and thus require a total scratch area on the order of 2048 bytes.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-2507">*Questo servizio deve essere chiamato solo immediatamente dopo fx_media_open e senza altre file system attività.*</span><span class="sxs-lookup"><span data-stu-id="9969a-2507">*This service should only be called immediately after fx_media_open and without any other file system activity.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2508">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2508">Input Parameters</span></span>

- <span data-ttu-id="9969a-2509">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2509">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-2510">**scratch_memory_ptr:** puntatore all'inizio della memoria scratch.</span><span class="sxs-lookup"><span data-stu-id="9969a-2510">**scratch_memory_ptr**: Pointer to the start of scratch memory.</span></span>
- <span data-ttu-id="9969a-2511">**scratch_memory_size**: dimensioni della memoria scratch in byte.</span><span class="sxs-lookup"><span data-stu-id="9969a-2511">**scratch_memory_size**: Size of scratch memory in bytes.</span></span>
- <span data-ttu-id="9969a-2512">**error_correction_option:** bit dell'opzione di correzione degli errori, quando il bit è impostato, viene eseguita la correzione degli errori.</span><span class="sxs-lookup"><span data-stu-id="9969a-2512">**error_correction_option**: Error correction option bits, when the bit is set, error correction is performed.</span></span> <span data-ttu-id="9969a-2513">I bit dell'opzione di correzione degli errori sono definiti come segue:</span><span class="sxs-lookup"><span data-stu-id="9969a-2513">The error correction option bits are defined as follows:</span></span>
  - <span data-ttu-id="9969a-2514">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="9969a-2514">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="9969a-2515">FX_DIRECTORY_ERROR (0x02)</span><span class="sxs-lookup"><span data-stu-id="9969a-2515">FX_DIRECTORY_ERROR (0x02)</span></span>
  - <span data-ttu-id="9969a-2516">FX_LOST_CLUSTER_ERROR (0x04) È sufficiente o insieme le opzioni di correzione degli errori necessarie.</span><span class="sxs-lookup"><span data-stu-id="9969a-2516">FX_LOST_CLUSTER_ERROR (0x04) Simply OR together the required error correction options.</span></span> <span data-ttu-id="9969a-2517">Se non è necessaria alcuna correzione degli errori, è necessario che sia specificato il valore 0.</span><span class="sxs-lookup"><span data-stu-id="9969a-2517">If no error correction is required, a value of 0 should be supplied.</span></span>
- <span data-ttu-id="9969a-2518">**errors_detected_ptr:** destinazione per i bit di rilevamento degli errori, come definito di seguito:</span><span class="sxs-lookup"><span data-stu-id="9969a-2518">**errors_detected_ptr**: Destination for error detection bits, as defined below:</span></span>
  - <span data-ttu-id="9969a-2519">FX_FAT_CHAIN_ERROR (0x01)</span><span class="sxs-lookup"><span data-stu-id="9969a-2519">FX_FAT_CHAIN_ERROR (0x01)</span></span>
  - <span data-ttu-id="9969a-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span><span class="sxs-lookup"><span data-stu-id="9969a-2520">FX_DIRECTORY_ERROR (0x02) FX_LOST_CLUSTER_ERROR (0x04)</span></span>
  - <span data-ttu-id="9969a-2521">FX_FILE_SIZE_ERROR (0x08)</span><span class="sxs-lookup"><span data-stu-id="9969a-2521">FX_FILE_SIZE_ERROR (0x08)</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2522">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2522">Return Values</span></span>

- <span data-ttu-id="9969a-2523">**FX_SUCCESS** (0x00) Controllo dei supporti riuscito, visualizzare la destinazione degli errori rilevati per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="9969a-2523">**FX_SUCCESS** (0x00) Successful media check, view the errors detected destination for details.</span></span>
- <span data-ttu-id="9969a-2524">**FX_ACCESS_ERROR** (0x06) Impossibile eseguire il controllo con i file aperti.</span><span class="sxs-lookup"><span data-stu-id="9969a-2524">**FX_ACCESS_ERROR** (0x06) Unable to perform check with open files.</span></span>
- <span data-ttu-id="9969a-2525">**FX_FILE_CORRUPT** file (0x08) è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2525">**FX_FILE_CORRUPT** (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-2526">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2526">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-2527">**FX_NO_MORE_SPACE** (0x0A) Non è più disponibile spazio sul supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2527">**FX_NO_MORE_SPACE** (0x0A) No more space on the media.</span></span>
- <span data-ttu-id="9969a-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) La memoria scratch fornita non è sufficientemente grande.</span><span class="sxs-lookup"><span data-stu-id="9969a-2528">**FX_NOT_ENOUGH_MEMORY** (0x91) Supplied scratch memory is not large enough.</span></span>
- <span data-ttu-id="9969a-2529">**FX_ERROR_NOT_FIXED** (0x93) Danneggiamento della directory radice FAT32 che non è stato possibile correzione.</span><span class="sxs-lookup"><span data-stu-id="9969a-2529">**FX_ERROR_NOT_FIXED** (0x93) Corruption of FAT32 root directory that could not be fixed.</span></span>
- <span data-ttu-id="9969a-2530">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2530">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2531">**FX_SECTOR_INVALID** (0x89) Sector non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2531">**FX_SECTOR_INVALID** (0x89) Sector is invalid.</span></span>
- <span data-ttu-id="9969a-2532">**FX_PTR_ERROR** (0x18) Supporto non valido o puntatore scratch.</span><span class="sxs-lookup"><span data-stu-id="9969a-2532">**FX_PTR_ERROR** (0x18) Invalid media or scratch pointer.</span></span>
- <span data-ttu-id="9969a-2533">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2533">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>


### <a name="allowed-from"></a><span data-ttu-id="9969a-2534">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2534">Allowed From</span></span>

<span data-ttu-id="9969a-2535">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2535">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2536">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2536">Example</span></span>

```c
FX_MEDIA         my_media;
ULONG             detected_errors;
UCHAR             sratch_memory[4096];

/* Check the media and correct all errors. */

status = fx_media_check(&my_media, sratch_memory, 4096,
                        FX_FAT_CHAIN_ERROR |
                        FX_DIRECTORY_ERROR |
                        FX_LOST_CLUSTER_ERROR, &detected_errors);

/* If status is FX_SUCCESS and detected_errors is 0,
    the media was successfully checked and found to be error free. */

```

### <a name="see-also"></a><span data-ttu-id="9969a-2537">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2537">See Also</span></span>

- <span data-ttu-id="9969a-2538">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2538">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2539">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2539">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2540">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2540">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2541">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2541">fx_media_close</span></span>
- <span data-ttu-id="9969a-2542">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2542">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2543">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2543">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2544">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2544">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2545">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2545">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2546">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2546">fx_media_format</span></span>
- <span data-ttu-id="9969a-2547">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2547">fx_media_open</span></span>
- <span data-ttu-id="9969a-2548">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2548">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2549">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2549">fx_media_read</span></span>
- <span data-ttu-id="9969a-2550">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2550">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2551">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2551">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2552">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2552">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2553">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2553">fx_media_write</span></span>
- <span data-ttu-id="9969a-2554">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2554">fx_system_initialize</span></span>

## <a name="fx_media_close"></a><span data-ttu-id="9969a-2555">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2555">fx_media_close</span></span>

<span data-ttu-id="9969a-2556">Chiude i supporti</span><span class="sxs-lookup"><span data-stu-id="9969a-2556">Closes media</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2557">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2557">Prototype</span></span>

```c
UINT fx_media_close(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="9969a-2558">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2558">Description</span></span>

<span data-ttu-id="9969a-2559">Questo servizio chiude il supporto specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2559">This service closes the specified media.</span></span> <span data-ttu-id="9969a-2560">Durante il processo di chiusura del supporto, tutti i file aperti vengono chiusi e tutti i buffer rimanenti vengono scaricati nel supporto fisico.</span><span class="sxs-lookup"><span data-stu-id="9969a-2560">In the process of closing the media, all open files are closed and any remaining buffers are flushed to the physical media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2561">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2561">Input Parameters</span></span>

- <span data-ttu-id="9969a-2562">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2562">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2563">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2563">Return Values</span></span>

- <span data-ttu-id="9969a-2564">**FX_SUCCESS** (0x00) Chiusura del supporto completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-2564">**FX_SUCCESS** (0x00) Successful media close.</span></span>
- <span data-ttu-id="9969a-2565">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2565">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-2566">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2566">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2567">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2567">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="9969a-2568">**FX_CALLER_ERROR**    (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2568">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2569">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2569">Allowed From</span></span>

<span data-ttu-id="9969a-2570">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2570">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2571">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2571">Example</span></span>

```c
FX_MEDIA    my_media;
UINT        status;
/* Close "my_media". */

status = fx_media_close(&my_media);

/* If status equals FX_SUCCESS, "my_media" is closed. */

```

### <a name="see-also"></a><span data-ttu-id="9969a-2572">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2572">See Also</span></span>

- <span data-ttu-id="9969a-2573">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2573">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2574">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2574">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2575">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2575">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2576">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2576">fx_media_check</span></span>
- <span data-ttu-id="9969a-2577">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2577">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2578">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2578">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2579">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2579">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2580">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2580">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2581">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2581">fx_media_format</span></span>
- <span data-ttu-id="9969a-2582">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2582">fx_media_open</span></span>
- <span data-ttu-id="9969a-2583">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2583">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2584">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2584">fx_media_read</span></span>
- <span data-ttu-id="9969a-2585">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2585">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2586">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2586">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2587">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2587">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2588">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2588">fx_media_write</span></span>
- <span data-ttu-id="9969a-2589">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2589">fx_system_initialize</span></span>

## <a name="fx_media_close_notify_set"></a><span data-ttu-id="9969a-2590">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2590">fx_media_close_notify_set</span></span>

<span data-ttu-id="9969a-2591">Imposta la funzione di notifica della chiusura dei supporti</span><span class="sxs-lookup"><span data-stu-id="9969a-2591">Sets the media close notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2592">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2592">Prototype</span></span>

```c
UINT fx_media_close_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_close_notify)(FX_MEDIA*));
```

### <a name="description"></a><span data-ttu-id="9969a-2593">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2593">Description</span></span>

<span data-ttu-id="9969a-2594">Questo servizio imposta una funzione di callback di notifica che verrà richiamata dopo la chiusura corretta di un supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2594">This service sets a notify callback function which will be invoked after a media is successfully closed.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2595">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2595">Input Parameters</span></span>

- <span data-ttu-id="9969a-2596">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2596">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-2597">**media_close_notify**: funzione di callback di notifica di chiusura dei supporti da installare.</span><span class="sxs-lookup"><span data-stu-id="9969a-2597">**media_close_notify**: Media close notify callback function to be installed.</span></span> <span data-ttu-id="9969a-2598">Il passaggio di NULL come funzione di callback disabilita il callback di chiusura dei supporti.</span><span class="sxs-lookup"><span data-stu-id="9969a-2598">Passing NULL as the callback function disables the media close callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2599">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2599">Return Values</span></span>

- <span data-ttu-id="9969a-2600">**FX_SUCCESS** (0x00) La funzione di callback è stata installata correttamente.</span><span class="sxs-lookup"><span data-stu-id="9969a-2600">**FX_SUCCESS** (0x00) Successfully installed the callback function.</span></span>
- <span data-ttu-id="9969a-2601">**FX_PTR_ERROR** (0x18) media_ptr è NULL.</span><span class="sxs-lookup"><span data-stu-id="9969a-2601">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="9969a-2602">**FX_CALLER_ERROR**    (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2602">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2603">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2603">Allowed From</span></span>

<span data-ttu-id="9969a-2604">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2604">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2605">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2605">Example</span></span>

```c
fx_media_close_notify_set(media_ptr, my_media_close_callback);

```
### <a name="see-also"></a><span data-ttu-id="9969a-2606">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2606">See Also</span></span>

- <span data-ttu-id="9969a-2607">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2607">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2608">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2608">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2609">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2609">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2610">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2610">fx_media_check</span></span>
- <span data-ttu-id="9969a-2611">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2611">fx_media_close</span></span>
- <span data-ttu-id="9969a-2612">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2612">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2613">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2613">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2614">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2614">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2615">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2615">fx_media_format</span></span>
- <span data-ttu-id="9969a-2616">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2616">fx_media_open</span></span>
- <span data-ttu-id="9969a-2617">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2617">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2618">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2618">fx_media_read</span></span>
- <span data-ttu-id="9969a-2619">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2619">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2620">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2620">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2621">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2621">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2622">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2622">fx_media_write</span></span>
- <span data-ttu-id="9969a-2623">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2623">fx_system_initialize</span></span>

## <a name="fx_media_exfat_format"></a><span data-ttu-id="9969a-2624">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2624">fx_media_exFAT_format</span></span>

<span data-ttu-id="9969a-2625">Formatta i supporti</span><span class="sxs-lookup"><span data-stu-id="9969a-2625">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2626">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2626">Prototype</span></span>

```c
UINT fx_media_exFAT_format(
    FX_MEDIA *media_ptr,
    VOID (*driver)(FX_MEDIA *media),
    VOID *driver_info_ptr, 
    UCHAR *memory_ptr,
    UINT memory_size, 
    CHAR *volume_name,
    UINT number_of_fats,
    ULONG64 hidden_sectors, 
    ULONG64 total_sectors,
    UINT bytes_per_sector, 
    UINT sectors_per_cluster,
    UINT volume_serial_number, 
    UINT boundary_unit);
```
### <a name="description"></a><span data-ttu-id="9969a-2627">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2627">Description</span></span>

<span data-ttu-id="9969a-2628">Questo servizio formatta i supporti forniti in modo compatibile con exFAT in base ai parametri forniti.</span><span class="sxs-lookup"><span data-stu-id="9969a-2628">This service formats the supplied media in an exFAT compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="9969a-2629">Questo servizio deve essere chiamato prima di aprire il supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2629">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-2630">*La formattazione di un supporto già formattato cancella in modo efficace tutti i file e le directory presenti nel supporto.*</span><span class="sxs-lookup"><span data-stu-id="9969a-2630">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-2631">*Le dimensioni del volume exFAT devono corrispondere alle dimensioni della partizione (se è presente un layout MBR o GPT) o alle dimensioni dell'intero dispositivo se non è presente alcun layout di partizione (nessun MBR o GPT). Esiste una limitazione per Windows che exFAT Disk non verrà ricodnato se formattato con alcuni valori dei settori totali inferiori ai settori disponibili*</span><span class="sxs-lookup"><span data-stu-id="9969a-2631">*The exFAT volume size should match the size of the partition (if there is an MBR or GPT layout), or the size of the whole device if there is no partition layout (no MBR or GPT). There is a limitation on Windows that exFAT Disk will not be recoginzed if formatted with some values of total sectors that are less than available sectors*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2632">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2632">Input Parameters</span></span>

- <span data-ttu-id="9969a-2633">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2633">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="9969a-2634">Viene usato solo per fornire alcune informazioni di base necessarie per il funzionamento del driver.</span><span class="sxs-lookup"><span data-stu-id="9969a-2634">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="9969a-2635">**driver:** puntatore al driver di I/O per questo supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2635">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="9969a-2636">Si tratta in genere dello stesso driver fornito alla chiamata fx_media_open successiva.</span><span class="sxs-lookup"><span data-stu-id="9969a-2636">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="9969a-2637">**driver_info_ptr:** puntatore a informazioni facoltative che possono essere utilizzate dal driver di I/O.</span><span class="sxs-lookup"><span data-stu-id="9969a-2637">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="9969a-2638">**memory_ptr:** puntatore alla memoria di lavoro per il supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2638">**memory_ptr**: Pointer to the working memory for the media.</span></span> <span data-ttu-id="9969a-2639">memory_size specifica le dimensioni della memoria dei supporti di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9969a-2639">memory_size Specifies the size of the working media memory.</span></span> <span data-ttu-id="9969a-2640">Le dimensioni devono essere almeno le dimensioni del settore del supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2640">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="9969a-2641">**volume_name:** puntatore alla stringa del nome del volume, che contiene un massimo di 11 caratteri.</span><span class="sxs-lookup"><span data-stu-id="9969a-2641">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="9969a-2642">**number_of_fats**: numero di FTS sul supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2642">**number_of_fats**: Number of FATs on the media.</span></span> <span data-ttu-id="9969a-2643">L'implementazione corrente supporta una fat sul supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2643">Current implementation supports one FAT on the media.</span></span>
- <span data-ttu-id="9969a-2644">**hidden_sectors**: numero di settori nascosti prima del settore di avvio del supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2644">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="9969a-2645">Questo è tipico quando sono presenti più partizioni.</span><span class="sxs-lookup"><span data-stu-id="9969a-2645">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="9969a-2646">**total_sectors**: numero totale di settori nei supporti.</span><span class="sxs-lookup"><span data-stu-id="9969a-2646">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="9969a-2647">**bytes_per_sector**: numero di byte per settore, che in genere è 512.</span><span class="sxs-lookup"><span data-stu-id="9969a-2647">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="9969a-2648">FileX richiede che sia un multiplo di 32.</span><span class="sxs-lookup"><span data-stu-id="9969a-2648">FileX requires this to be a multiple of 32.</span></span>
- <span data-ttu-id="9969a-2649">**sectors_per_cluster**: numero di settori in ogni cluster.</span><span class="sxs-lookup"><span data-stu-id="9969a-2649">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="9969a-2650">Il cluster è l'unità di allocazione minima in un file system.</span><span class="sxs-lookup"><span data-stu-id="9969a-2650">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="9969a-2651">**volumne_serial_number**: numero di serie da usare per questo volume.</span><span class="sxs-lookup"><span data-stu-id="9969a-2651">**volumne_serial_number**: Serial number to be used for this volume.</span></span>
- <span data-ttu-id="9969a-2652">**boundary_unit:** dimensioni di allineamento dell'area dati fisica, in numero di settori.</span><span class="sxs-lookup"><span data-stu-id="9969a-2652">**boundary_unit**: Physical data area alignment size, in number of sectors.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2653">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2653">Return Values</span></span>

- <span data-ttu-id="9969a-2654">**FX_SUCCESS** (0x00) Formato multimediale riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2654">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="9969a-2655">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2655">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2656">**FX_PTR_ERROR** (0x18) Supporto, driver o puntatore di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2656">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="9969a-2657">**FX_CALLER_ERROR**    (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2657">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2658">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2658">Allowed From</span></span>

<span data-ttu-id="9969a-2659">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2659">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2660">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2660">Example</span></span>

```c
FX_MEDIA             sd_card;
UCHAR                 media_memory[512];

/* Format a 64GB SD card with exFAT file system. The media has
    been properly partitioned, with the partition starts from sector 32768.
    For 64GB, there are total of 120913920 sectors, each sector 512 bytes. */

status = fx_media_exFAT_format(&sd_card, _fx_sd_driver,
                                driver_information, media_memory,
                                sizeof(media_memory),
                                "exFAT_DISK" /* Volume Name */,
                                1 /* Number of FATs */,
                                32768 /* Hidden sectors */,
                                120913920 /* Total sectors */,
                                512 /* Sector size */,
                                256 /* Sectors per cluster */,
                                12345 /* Volume ID */,
                                8192 /* Boundary unit */);

/* If status is FX_SUCCESS, the media was successfully formatted. */

```

### <a name="see-also"></a><span data-ttu-id="9969a-2661">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2661">See Also</span></span>

- <span data-ttu-id="9969a-2662">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2662">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2663">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2663">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2664">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2664">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2665">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2665">fx_media_check</span></span>
- <span data-ttu-id="9969a-2666">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2666">fx_media_close</span></span>
- <span data-ttu-id="9969a-2667">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2667">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2668">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2668">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2669">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2669">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2670">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2670">fx_media_format</span></span>
- <span data-ttu-id="9969a-2671">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2671">fx_media_open</span></span>
- <span data-ttu-id="9969a-2672">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2672">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2673">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2673">fx_media_read</span></span>
- <span data-ttu-id="9969a-2674">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2674">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2675">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2675">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2676">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2676">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2677">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2677">fx_media_write</span></span>
- <span data-ttu-id="9969a-2678">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2678">fx_system_initialize</span></span>

## <a name="fx_media_extended_space_available"></a><span data-ttu-id="9969a-2679">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2679">fx_media_extended_space_available</span></span>

<span data-ttu-id="9969a-2680">Restituisce lo spazio multimediale disponibile</span><span class="sxs-lookup"><span data-stu-id="9969a-2680">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2681">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2681">Prototype</span></span>

```c
UINT fx_media_extended_space_available(
    FX_MEDIA *media_ptr,
    ULONG64 *available_bytes_ptr);
```
### <a name="description"></a><span data-ttu-id="9969a-2682">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2682">Description</span></span>

<span data-ttu-id="9969a-2683">Questo servizio restituisce il numero di byte disponibili nel supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2683">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="9969a-2684">Questo servizio è progettato per exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-2684">This service is designed for exFAT.</span></span> <span data-ttu-id="9969a-2685">Il puntatore *available_bytes* parametro accetta un valore integer a 64 bit, che consente al chiamante di usare supporti oltre l'intervallo di 4 GB.</span><span class="sxs-lookup"><span data-stu-id="9969a-2685">The pointer to *available_bytes* parameter takes a 64-bit integer value, which allows the caller to work with media beyond 4GB range.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2686">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2686">Input Parameters</span></span>

- <span data-ttu-id="9969a-2687">**media_ptr:** puntatore a un supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-2687">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="9969a-2688">**available_bytes_ptr:** byte disponibili rimasti nel supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2688">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2689">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2689">Return Values</span></span>

- <span data-ttu-id="9969a-2690">**FX_SUCCESS** (0x00) È stato recuperato lo spazio disponibile nel supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2690">**FX_SUCCESS** (0x00) Successfully retrieved space available on the media.</span></span>
- <span data-ttu-id="9969a-2691">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2691">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-2692">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido o puntatore byte disponibili è NULL.</span><span class="sxs-lookup"><span data-stu-id="9969a-2692">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="9969a-2693">**FX_CALLER_ERROR**    (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2693">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2694">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2694">Allowed From</span></span>

<span data-ttu-id="9969a-2695">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2695">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2696">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2696">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG64            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_extended_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="9969a-2697">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2697">See Also</span></span>

- <span data-ttu-id="9969a-2698">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2698">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2699">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2699">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2700">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2700">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2701">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2701">fx_media_check</span></span>
- <span data-ttu-id="9969a-2702">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2702">fx_media_close</span></span>
- <span data-ttu-id="9969a-2703">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2703">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2704">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2704">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2705">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2705">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2706">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2706">fx_media_format</span></span>
- <span data-ttu-id="9969a-2707">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2707">fx_media_open</span></span>
- <span data-ttu-id="9969a-2708">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2708">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2709">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2709">fx_media_read</span></span>
- <span data-ttu-id="9969a-2710">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2710">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2711">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2711">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2712">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2712">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2713">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2713">fx_media_write</span></span>
- <span data-ttu-id="9969a-2714">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2714">fx_system_initialize</span></span>

## <a name="fx_media_flush"></a><span data-ttu-id="9969a-2715">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2715">fx_media_flush</span></span>

<span data-ttu-id="9969a-2716">Scarica i dati nei supporti fisici</span><span class="sxs-lookup"><span data-stu-id="9969a-2716">Flushes data to physical media</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2717">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2717">Prototype</span></span>

```c
UINT fx_media_flush(FX_MEDIA *media_ptr);
```
### <a name="description"></a><span data-ttu-id="9969a-2718">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2718">Description</span></span>

<span data-ttu-id="9969a-2719">Questo servizio scarica tutti i settori memorizzati nella cache e le voci di directory di tutti i file modificati nel supporto fisico.</span><span class="sxs-lookup"><span data-stu-id="9969a-2719">This service flushes all cached sectors and directory entries of any modified files to the physical media.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-2720">*Questa routine può essere chiamata periodicamente dall'applicazione per ridurre il rischio di danneggiamento dei file e/o perdita di dati in caso di una perdita di alimentazione improvvisa nella destinazione.*</span><span class="sxs-lookup"><span data-stu-id="9969a-2720">*This routine may be called periodically by the application to reduce the risk of file corruption and/or data loss in the event of a sudden loss of power on the target.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2721">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2721">Input Parameters</span></span>

- <span data-ttu-id="9969a-2722">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2722">**media_ptr**: Pointer to media control block.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2723">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2723">Return Values</span></span>

- <span data-ttu-id="9969a-2724">**FX_SUCCESS** (0x00) Scaricamento del supporto riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2724">**FX_SUCCESS** (0x00) Successful media flush.</span></span>
- <span data-ttu-id="9969a-2725">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2725">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-2726">**FX_FILE_CORRUPT**    (0x08) Il file è danneggiato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2726">**FX_FILE_CORRUPT**    (0x08) File is corrupted.</span></span>
- <span data-ttu-id="9969a-2727">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2727">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-2728">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2728">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2729">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-2729">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-2730">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2730">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="9969a-2731">**FX_CALLER_ERROR**    (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2731">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2732">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2732">Allowed From</span></span>

<span data-ttu-id="9969a-2733">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2733">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2734">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2734">Example</span></span>

```c
FX_MEDIA         my_media;
UINT             status;

/* Flush all cached sectors and modified file entries to the physical media. */

status = fx_media_flush(&my_media);

/* If status equals FX_SUCCESS, the physical media is completely up-to-date. */

```

### <a name="see-also"></a><span data-ttu-id="9969a-2735">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2735">See Also</span></span>

- <span data-ttu-id="9969a-2736">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2736">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2737">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2737">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2738">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2738">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2739">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2739">fx_media_check</span></span>
- <span data-ttu-id="9969a-2740">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2740">fx_media_close</span></span>
- <span data-ttu-id="9969a-2741">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2741">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2742">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2742">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2743">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2743">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2744">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2744">fx_media_format</span></span>
- <span data-ttu-id="9969a-2745">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2745">fx_media_open</span></span>
- <span data-ttu-id="9969a-2746">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2746">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2747">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2747">fx_media_read</span></span>
- <span data-ttu-id="9969a-2748">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2748">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2749">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2749">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2750">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2750">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2751">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2751">fx_media_write</span></span>
- <span data-ttu-id="9969a-2752">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2752">fx_system_initialize</span></span>

## <a name="fx_media_format"></a><span data-ttu-id="9969a-2753">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2753">fx_media_format</span></span>

<span data-ttu-id="9969a-2754">Formatta i supporti</span><span class="sxs-lookup"><span data-stu-id="9969a-2754">Formats media</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2755">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2755">Prototype</span></span>

```c
UINT fx_media_format(
    FX_MEDIA *media_ptr,
    VOID (*driver)(FX_MEDIA *media),
    VOID *driver_info_ptr,
    UCHAR *memory_ptr, 
    UINT memory_size,
    CHAR *volume_name, 
    UINT number_of_fats,
    UINT directory_entries, 
    UINT hidden_sectors,
    ULONG total_sectors, 
    UINT bytes_per_sector,
    UINT sectors_per_cluster,
    UINT heads,
    UINT sectors_per_track);
```
### <a name="description"></a><span data-ttu-id="9969a-2756">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2756">Description</span></span>

<span data-ttu-id="9969a-2757">Questo servizio formatta i supporti forniti in modo compatibile con FAT 12/16/32 in base ai parametri forniti.</span><span class="sxs-lookup"><span data-stu-id="9969a-2757">This service formats the supplied media in a FAT 12/16/32 compatible manner based on the supplied parameters.</span></span> <span data-ttu-id="9969a-2758">Questo servizio deve essere chiamato prima di aprire il supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2758">This service must be called prior to opening the media.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-2759">*La formattazione di un supporto già formattato cancella in modo efficace tutti i file e le directory presenti nel supporto.*</span><span class="sxs-lookup"><span data-stu-id="9969a-2759">*Formatting an already formatted media effectively erases all files and directories on the media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2760">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2760">Input Parameters</span></span>

- <span data-ttu-id="9969a-2761">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2761">**media_ptr**: Pointer to media control block.</span></span> <span data-ttu-id="9969a-2762">Viene usato solo per fornire alcune informazioni di base necessarie per il funzionamento del driver.</span><span class="sxs-lookup"><span data-stu-id="9969a-2762">This is used only to provide some basic information necessary for the driver to operate.</span></span>
- <span data-ttu-id="9969a-2763">**driver**: puntatore al driver di I/O per questo supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2763">**driver**: Pointer to the I/O driver for this media.</span></span> <span data-ttu-id="9969a-2764">Si tratta in genere dello stesso driver fornito alla chiamata fx_media_open successiva.</span><span class="sxs-lookup"><span data-stu-id="9969a-2764">This will typically be the same driver supplied to the subsequent fx_media_open call.</span></span>
- <span data-ttu-id="9969a-2765">**driver_info_ptr:** puntatore a informazioni facoltative che possono essere utilizzate dal driver di I/O.</span><span class="sxs-lookup"><span data-stu-id="9969a-2765">**driver_info_ptr**: Pointer to optional information that the I/O driver may utilize.</span></span>
- <span data-ttu-id="9969a-2766">**memory_ptr**: puntatore alla memoria di lavoro per il supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2766">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="9969a-2767">**memory_size**: specifica le dimensioni della memoria dei supporti di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9969a-2767">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="9969a-2768">Le dimensioni devono essere almeno le dimensioni del settore del supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2768">The size must be at least as large as the media's sector size.</span></span>
- <span data-ttu-id="9969a-2769">**volume_name**: puntatore alla stringa del nome del volume, che può avere un massimo di 11 caratteri.</span><span class="sxs-lookup"><span data-stu-id="9969a-2769">**volume_name**: Pointer to the volume name string, which is a maximum of 11 characters.</span></span>
- <span data-ttu-id="9969a-2770">**number_of_fats**: numero di faT nei supporti.</span><span class="sxs-lookup"><span data-stu-id="9969a-2770">**number_of_fats**: Number of FATs in the media.</span></span> <span data-ttu-id="9969a-2771">Il valore minimo è 1 per il fat primario.</span><span class="sxs-lookup"><span data-stu-id="9969a-2771">The minimal value is 1 for the primary FAT.</span></span> <span data-ttu-id="9969a-2772">I valori maggiori di 1 comportano la manutenzione di copie FAT aggiuntive in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9969a-2772">Values greater than 1 result in additional FAT copies being maintained at run-time.</span></span>
- <span data-ttu-id="9969a-2773">**directory_entries**: numero di voci di directory nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="9969a-2773">**directory_entries**: Number of directory entries in the root directory.</span></span>
- <span data-ttu-id="9969a-2774">**hidden_sectors**: numero di settori nascosti prima del settore di avvio del supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2774">**hidden_sectors**: Number of sectors hidden before this media's boot sector.</span></span> <span data-ttu-id="9969a-2775">Questo è tipico quando sono presenti più partizioni.</span><span class="sxs-lookup"><span data-stu-id="9969a-2775">This is typical when multiple partitions are present.</span></span>
- <span data-ttu-id="9969a-2776">**total_sectors**: numero totale di settori nei supporti.</span><span class="sxs-lookup"><span data-stu-id="9969a-2776">**total_sectors**: Total number of sectors in the media.</span></span>
- <span data-ttu-id="9969a-2777">**bytes_per_sector**: numero di byte per settore, che in genere è 512.</span><span class="sxs-lookup"><span data-stu-id="9969a-2777">**bytes_per_sector**: Number of bytes per sector, which is typically 512.</span></span> <span data-ttu-id="9969a-2778">FileX richiede che sia un multiplo di 32.</span><span class="sxs-lookup"><span data-stu-id="9969a-2778">FileX requires this to be a multiple of 32.</span></span>
- <span data-ttu-id="9969a-2779">**sectors_per_cluster**: numero di settori in ogni cluster.</span><span class="sxs-lookup"><span data-stu-id="9969a-2779">**sectors_per_cluster**: Number of sectors in each cluster.</span></span> <span data-ttu-id="9969a-2780">Il cluster è l'unità di allocazione minima in un file system.</span><span class="sxs-lookup"><span data-stu-id="9969a-2780">The cluster is the minimum allocation unit in a FAT file system.</span></span>
- <span data-ttu-id="9969a-2781">**heads**: numero di teste fisiche.</span><span class="sxs-lookup"><span data-stu-id="9969a-2781">**heads**: Number of physical heads.</span></span>
- <span data-ttu-id="9969a-2782">**sectors_per_track**: numero di settori per traccia.</span><span class="sxs-lookup"><span data-stu-id="9969a-2782">**sectors_per_track**: Number of sectors per track.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2783">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2783">Return Values</span></span>

- <span data-ttu-id="9969a-2784">**FX_SUCCESS** (0x00) Formato multimediale riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2784">**FX_SUCCESS** (0x00) Successful media format.</span></span>
- <span data-ttu-id="9969a-2785">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2785">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2786">**FX_PTR_ERROR** (0x18) Supporto, driver o puntatore di memoria non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2786">**FX_PTR_ERROR** (0x18) Invalid media, driver, or memory pointer.</span></span>
- <span data-ttu-id="9969a-2787">**FX_CALLER_ERROR**    (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2787">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2788">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2788">Allowed From</span></span>

<span data-ttu-id="9969a-2789">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2789">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2790">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2790">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             media_memory[512];
UCHAR             ram_disk_memory[32768];

/* Format a RAM disk with 32768 bytes and 512 bytes per sector. */

status = fx_media_format(&ram_disk, _fx_ram_driver,
                         ram_disk_memory, media_memory,
                         sizeof(media_memory),
                         "MY_RAM_DISK" /* Volume Name */,
                         1 /* Number of FATs */,
                         32 /* Directory Entries */,
                         0 /* Hidden sectors */,
                         64 /* Total sectors */,
                         512 /* Sector size */,
                         1 /* Sectors per cluster */,
                         1 /* Heads */,
                         1 /* Sectors per track */);

/* If status is FX_SUCCESS, the media was successfully formatted
    and can now be opened with the following call: */

```

### <a name="see-also"></a><span data-ttu-id="9969a-2791">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2791">See Also</span></span>

- <span data-ttu-id="9969a-2792">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2792">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2793">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2793">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2794">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2794">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2795">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2795">fx_media_check</span></span>
- <span data-ttu-id="9969a-2796">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2796">fx_media_close</span></span>
- <span data-ttu-id="9969a-2797">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2797">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2798">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2798">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2799">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2799">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2800">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2800">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2801">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2801">fx_media_open</span></span>
- <span data-ttu-id="9969a-2802">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2802">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2803">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2803">fx_media_read</span></span>
- <span data-ttu-id="9969a-2804">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2804">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2805">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2805">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2806">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2806">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2807">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2807">fx_media_write</span></span>
- <span data-ttu-id="9969a-2808">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2808">fx_system_initialize</span></span>

## <a name="fx_media_open"></a><span data-ttu-id="9969a-2809">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2809">fx_media_open</span></span>

<span data-ttu-id="9969a-2810">Apre i supporti per l'accesso ai file</span><span class="sxs-lookup"><span data-stu-id="9969a-2810">Opens media for file access</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2811">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2811">Prototype</span></span>

```c
UINT fx_media_open(
    FX_MEDIA *media_ptr, 
    CHAR *media_name,
    VOID(*media_driver)(FX_MEDIA *),
    VOID *driver_info_ptr,
    VOID *memory_ptr, 
    ULONG memory_size);
```
### <a name="description"></a><span data-ttu-id="9969a-2812">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2812">Description</span></span>

<span data-ttu-id="9969a-2813">Questo servizio apre un supporto per l'accesso ai file usando il driver di I/O fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2813">This service opens a media for file access using the supplied I/O driver.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-2814">*La memoria fornita a questo servizio viene usata per implementare una cache di settore logico interna, quindi maggiore è la quantità di memoria fornita, maggiore sarà la quantità di I/O fisico ridotta. FileX richiede una cache di almeno un settore logico (byte per settore del supporto).*</span><span class="sxs-lookup"><span data-stu-id="9969a-2814">*The memory supplied to this service is used to implement an internal logical sector cache, hence, the more memory supplied the more physical I/O is reduced. FileX requires a cache of at least one logical sector (bytes per sector of the media).*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2815">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2815">Input Parameters</span></span>

- <span data-ttu-id="9969a-2816">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2816">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-2817">**media_name:** puntatore al nome del supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2817">**media_name**: Pointer to media's name.</span></span>
- <span data-ttu-id="9969a-2818">**media_driver:** puntatore al driver di I/O per questo supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2818">**media_driver**: Pointer to I/O driver for this media.</span></span> <span data-ttu-id="9969a-2819">Il driver di I/O deve essere conforme ai requisiti del driver FileX definiti nel capitolo 5.</span><span class="sxs-lookup"><span data-stu-id="9969a-2819">The I/O driver must conform to FileX driver requirements defined in Chapter 5.</span></span>
- <span data-ttu-id="9969a-2820">**driver_info_ptr:** puntatore a informazioni facoltative che possono essere utilizzate dal driver di I/O fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2820">**driver_info_ptr**: Pointer to optional information that the supplied I/O driver may utilize.</span></span>
- <span data-ttu-id="9969a-2821">**memory_ptr:** puntatore alla memoria di lavoro per il supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2821">**memory_ptr**: Pointer to the working memory for the media.</span></span>
- <span data-ttu-id="9969a-2822">**memory_size**: specifica le dimensioni della memoria del supporto di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9969a-2822">**memory_size**: Specifies the size of the working media memory.</span></span> <span data-ttu-id="9969a-2823">Le dimensioni devono essere grandi quanto le dimensioni del settore del supporto (in genere 512 byte).</span><span class="sxs-lookup"><span data-stu-id="9969a-2823">The size must be as large as the media's sector size (typically 512 bytes).</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2824">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2824">Return Values</span></span>

- <span data-ttu-id="9969a-2825">**FX_SUCCESS** (0x00) Apertura dei supporti completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-2825">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="9969a-2826">**FX_BOOT_ERROR** (0x01) Errore durante la lettura del settore di avvio del supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2826">**FX_BOOT_ERROR** (0x01) Error reading the media's boot sector.</span></span>
- <span data-ttu-id="9969a-2827">**FX_MEDIA_INVALID** (0x02) Il settore di avvio del supporto specificato è danneggiato o non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2827">**FX_MEDIA_INVALID** (0x02) Specified media's boot sector is corrupt or invalid.</span></span> <span data-ttu-id="9969a-2828">Inoltre, questo codice restituito viene usato per indicare che la dimensione della cache del settore logico o la dimensione della voce FAT non è una potenza di 2.</span><span class="sxs-lookup"><span data-stu-id="9969a-2828">In addition, this return code is used to indicate that either the logical sector cache size or the FAT entry size is not a power of 2.</span></span>
- <span data-ttu-id="9969a-2829">**FX_FAT_READ_ERROR** (0x03) Errore durante la lettura del file FAT multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2829">**FX_FAT_READ_ERROR** (0x03) Error reading the media FAT.</span></span>
- <span data-ttu-id="9969a-2830">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2830">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2831">**FX_PTR_ERROR** (0x18) Uno o più puntatori sono NULL.</span><span class="sxs-lookup"><span data-stu-id="9969a-2831">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="9969a-2832">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2832">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2833">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2833">Allowed From</span></span>

<span data-ttu-id="9969a-2834">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2834">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2835">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2835">Example</span></span>

```c
FX_MEDIA         ram_disk,
UINT             status;
UCHAR             buffer[128];
/* Open a 32KByte RAM disk starting at the fixed address of 0x800000.
    Note that the total 32KByte media size and 128-byte sector size is defined inside of the driver. */

status = fx_media_open(&ram_disk, "RAM DISK", fx_ram_driver, 0, &buffer[0], sizeof(buffer));

/* If status equals FX_SUCCESS, the RAM disk has been successfully setup and is ready for file access! */

```

### <a name="see-also"></a><span data-ttu-id="9969a-2836">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2836">See Also</span></span>

- <span data-ttu-id="9969a-2837">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2837">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2838">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2838">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2839">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2839">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2840">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2840">fx_media_check</span></span>
- <span data-ttu-id="9969a-2841">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2841">fx_media_close</span></span>
- <span data-ttu-id="9969a-2842">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2842">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2843">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2843">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2844">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2844">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2845">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2845">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2846">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2846">fx_media_format</span></span>
- <span data-ttu-id="9969a-2847">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2847">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2848">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2848">fx_media_read</span></span>
- <span data-ttu-id="9969a-2849">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2849">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2850">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2850">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2851">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2851">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2852">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2852">fx_media_write</span></span>
- <span data-ttu-id="9969a-2853">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2853">fx_system_initialize</span></span>

## <a name="fx_media_open_notify_set"></a><span data-ttu-id="9969a-2854">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2854">fx_media_open_notify_set</span></span>

<span data-ttu-id="9969a-2855">Imposta la funzione di notifica dell'apertura dei supporti</span><span class="sxs-lookup"><span data-stu-id="9969a-2855">Sets the media open notify function</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2856">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2856">Prototype</span></span>

```c
UINT fx_media_open_notify_set(
    FX_MEDIA *media_ptr,
    VOID (*media_open_notify)(FX_MEDIA*));
```
### <a name="description"></a><span data-ttu-id="9969a-2857">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2857">Description</span></span>

<span data-ttu-id="9969a-2858">Questo servizio imposta una funzione di callback di notifica che verrà richiamata dopo che un supporto è stato aperto correttamente.</span><span class="sxs-lookup"><span data-stu-id="9969a-2858">This service sets a notify callback function which will be invoked after a media is successfully opened.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2859">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2859">Input Parameters</span></span>

- <span data-ttu-id="9969a-2860">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2860">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-2861">**media_open_notify:** funzione di callback di notifica dell'apertura dei supporti da installare.</span><span class="sxs-lookup"><span data-stu-id="9969a-2861">**media_open_notify**: Media open notify callback function to be installed.</span></span> <span data-ttu-id="9969a-2862">Il passaggio di NULL come funzione di callback disabilita il callback di apertura del supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2862">Passing NULL as the callback function disables the media open callback.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2863">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2863">Return Values</span></span>


- <span data-ttu-id="9969a-2864">**FX_SUCCESS** (0x00) L'installazione della funzione di callback è riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-2864">**FX_SUCCESS** (0x00) Successfuly installed the callback function.</span></span>
- <span data-ttu-id="9969a-2865">**FX_PTR_ERROR** (0x18) media_ptr è NULL.</span><span class="sxs-lookup"><span data-stu-id="9969a-2865">**FX_PTR_ERROR** (0x18) media_ptr is NULL.</span></span>
- <span data-ttu-id="9969a-2866">**FX_CALLER_ERROR**    (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2866">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2867">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2867">Allowed From</span></span>

<span data-ttu-id="9969a-2868">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2868">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2869">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2869">Example</span></span>

```c
fx_media_open_notify_set(media_ptr, my_media_open_callback);

```

### <a name="see-also"></a><span data-ttu-id="9969a-2870">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2870">See Also</span></span>

- <span data-ttu-id="9969a-2871">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2871">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2872">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2872">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2873">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2873">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2874">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2874">fx_media_check</span></span>
- <span data-ttu-id="9969a-2875">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2875">fx_media_close</span></span>
- <span data-ttu-id="9969a-2876">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2876">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2877">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2877">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2878">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2878">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2879">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2879">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2880">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2880">fx_media_format</span></span>
- <span data-ttu-id="9969a-2881">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2881">fx_media_open</span></span>
- <span data-ttu-id="9969a-2882">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2882">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2883">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2883">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2884">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2884">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2885">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2885">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2886">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2886">fx_media_write</span></span>
- <span data-ttu-id="9969a-2887">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2887">fx_system_initialize</span></span>

## <a name="fx_media_read"></a><span data-ttu-id="9969a-2888">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2888">fx_media_read</span></span>

<span data-ttu-id="9969a-2889">Legge il settore logico dai supporti</span><span class="sxs-lookup"><span data-stu-id="9969a-2889">Reads logical sector from media</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2890">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2890">Prototype</span></span>

```c
UINT fx_media_read(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector, 
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="9969a-2891">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2891">Description</span></span>

<span data-ttu-id="9969a-2892">Questo servizio legge un settore logico dal supporto e lo inserisce nel buffer fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2892">This service reads a logical sector from the media and places it into the supplied buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2893">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2893">Input Parameters</span></span>

- <span data-ttu-id="9969a-2894">**media_ptr:** puntatore a un supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-2894">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="9969a-2895">**logical_sector:** settore logico da leggere.</span><span class="sxs-lookup"><span data-stu-id="9969a-2895">**logical_sector**: Logical sector to read.</span></span>
- <span data-ttu-id="9969a-2896">**buffer_ptr**: puntatore alla destinazione per la lettura del settore logico.</span><span class="sxs-lookup"><span data-stu-id="9969a-2896">**buffer_ptr**: Pointer to the destination for the logical sector read.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2897">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2897">Return Values</span></span>

- <span data-ttu-id="9969a-2898">**FX_SUCCESS** (0x00) Lettura supporti riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-2898">**FX_SUCCESS** (0x00) Successful media read.</span></span>
- <span data-ttu-id="9969a-2899">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2899">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-2900">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2900">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2901">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2901">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-2902">**FX_PTR_ERROR** (0x18) Supporto o puntatore del buffer non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-2902">**FX_PTR_ERROR** (0x18) Invalid media or buffer pointer.</span></span>
- <span data-ttu-id="9969a-2903">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2903">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2904">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2904">Allowed From</span></span>

<span data-ttu-id="9969a-2905">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2905">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2906">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2906">Example</span></span>

```c
FX_MEDIA         my_media;
UCHAR             my_buffer[128];
UINT            STATUS;
/* Read logical sector 22 into "my_buffer" assuming the
    physical media has a sector size of 128. */
status = fx_media_read(&my_media, 22, my_buffer);
/* If status equals FX_SUCCESS, the contents of logical sector 22 are in "my_buffer". */
```

### <a name="see-also"></a><span data-ttu-id="9969a-2907">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2907">See Also</span></span>

- <span data-ttu-id="9969a-2908">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2908">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2909">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2909">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2910">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2910">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2911">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2911">fx_media_check</span></span>
- <span data-ttu-id="9969a-2912">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2912">fx_media_close</span></span>
- <span data-ttu-id="9969a-2913">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2913">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2914">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2914">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2915">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2915">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2916">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2916">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2917">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2917">fx_media_format</span></span>
- <span data-ttu-id="9969a-2918">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2918">fx_media_open</span></span>
- <span data-ttu-id="9969a-2919">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2919">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2920">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2920">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2921">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2921">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2922">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2922">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2923">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2923">fx_media_write</span></span>
- <span data-ttu-id="9969a-2924">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2924">fx_system_initialize</span></span>

## <a name="fx_media_space_available"></a><span data-ttu-id="9969a-2925">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2925">fx_media_space_available</span></span>

<span data-ttu-id="9969a-2926">Restituisce lo spazio multimediale disponibile</span><span class="sxs-lookup"><span data-stu-id="9969a-2926">Returns available media space</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2927">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2927">Prototype</span></span>

```c
UINT fx_media_space_available(
    FX_MEDIA *media_ptr,
    ULONG *available_bytes_ptr);
```

### <a name="description"></a><span data-ttu-id="9969a-2928">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2928">Description</span></span>

<span data-ttu-id="9969a-2929">Questo servizio restituisce il numero di byte disponibili nel supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2929">This service returns the number of bytes available in the media.</span></span>

<span data-ttu-id="9969a-2930">Per usare supporti di dimensioni superiori a 4 GB, l'applicazione deve usare il *servizio* fx_media_extended_space_available .</span><span class="sxs-lookup"><span data-stu-id="9969a-2930">To work with the media larger than 4GB, application shall use the service *fx_media_extended_space_available*.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2931">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2931">Input Parameters</span></span>

- <span data-ttu-id="9969a-2932">**media_ptr:** puntatore a un supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-2932">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="9969a-2933">**available_bytes_ptr:** byte disponibili rimasti nel supporto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2933">**available_bytes_ptr**: Available bytes left in the media.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2934">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2934">Return Values</span></span>

- <span data-ttu-id="9969a-2935">**FX_SUCCESS** (0x00) Ha restituito correttamente lo spazio disponibile sui supporti.</span><span class="sxs-lookup"><span data-stu-id="9969a-2935">**FX_SUCCESS** (0x00) Successfully returned available space on media.</span></span>
- <span data-ttu-id="9969a-2936">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2936">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-2937">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido o puntatore byte disponibili è NULL.</span><span class="sxs-lookup"><span data-stu-id="9969a-2937">**FX_PTR_ERROR** (0x18) Invalid media pointer or available bytes pointer is NULL.</span></span>
- <span data-ttu-id="9969a-2938">**FX_CALLER_ERROR**    (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2938">**FX_CALLER_ERROR**    (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2939">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2939">Allowed From</span></span>

<span data-ttu-id="9969a-2940">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2940">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2941">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2941">Example</span></span>

```c
FX_MEDIA        my_media;
ULONG            available_bytes;
UINT            status;
/* Retrieve the available bytes in the media. */

status = fx_media_space_available(&my_media, &available_bytes);

/* If status equals FX_SUCCESS, the number of available bytes is in "available_bytes." */

```

### <a name="see-also"></a><span data-ttu-id="9969a-2942">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2942">See Also</span></span>

- <span data-ttu-id="9969a-2943">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2943">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2944">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2944">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2945">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2945">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2946">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2946">fx_media_check</span></span>
- <span data-ttu-id="9969a-2947">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2947">fx_media_close</span></span>
- <span data-ttu-id="9969a-2948">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2948">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2949">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2949">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2950">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2950">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2951">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2951">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2952">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2952">fx_media_format</span></span>
- <span data-ttu-id="9969a-2953">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2953">fx_media_open</span></span>
- <span data-ttu-id="9969a-2954">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2954">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2955">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2955">fx_media_read</span></span>
- <span data-ttu-id="9969a-2956">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2956">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-2957">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2957">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2958">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2958">fx_media_write</span></span>
- <span data-ttu-id="9969a-2959">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-2959">fx_system_initialize</span></span>

## <a name="fx_media_volume_get"></a><span data-ttu-id="9969a-2960">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-2960">fx_media_volume_get</span></span>

<span data-ttu-id="9969a-2961">Ottiene il nome del volume multimediale</span><span class="sxs-lookup"><span data-stu-id="9969a-2961">Gets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-2962">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-2962">Prototype</span></span>

```c
UINT fx_media_volume_get(
    FX_MEDIA *media_ptr,
    CHAR *volume_name,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="9969a-2963">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-2963">Description</span></span>

<span data-ttu-id="9969a-2964">Questo servizio recupera il nome del volume del supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-2964">This service retrieves the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-2965">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-2965">Input Parameters</span></span>

- <span data-ttu-id="9969a-2966">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-2966">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-2967">**volume_name:** puntatore alla destinazione per il nome del volume.</span><span class="sxs-lookup"><span data-stu-id="9969a-2967">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="9969a-2968">Si noti che la destinazione deve essere sufficientemente grande da contenere 12 caratteri.</span><span class="sxs-lookup"><span data-stu-id="9969a-2968">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="9969a-2969">**volume_source**: indica dove recuperare il nome, dal settore di avvio o dalla directory radice.</span><span class="sxs-lookup"><span data-stu-id="9969a-2969">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="9969a-2970">I valori validi per questo parametro sono:</span><span class="sxs-lookup"><span data-stu-id="9969a-2970">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="9969a-2971">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="9969a-2971">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="9969a-2972">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="9969a-2972">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-2973">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-2973">Return Values</span></span>

- <span data-ttu-id="9969a-2974">**FX_SUCCESS** (0x00) Volume multimediale riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-2974">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="9969a-2975">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-2975">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-2976">**FX_NOT_FOUND** volume (0x04) non trovato.</span><span class="sxs-lookup"><span data-stu-id="9969a-2976">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="9969a-2977">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-2977">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-2978">**FX_PTR_ERROR** (0x18) Supporto non valido o puntatore di destinazione del volume.</span><span class="sxs-lookup"><span data-stu-id="9969a-2978">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="9969a-2979">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-2979">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-2980">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-2980">Allowed From</span></span>

<span data-ttu-id="9969a-2981">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-2981">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-2982">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-2982">Example</span></span>

```c
FX_MEDIA        ram_disk;
UCHAR             volume_name[12];
/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name), FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */

```

### <a name="see-also"></a><span data-ttu-id="9969a-2983">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-2983">See Also</span></span>

- <span data-ttu-id="9969a-2984">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-2984">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-2985">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-2985">fx_media_abort</span></span>
- <span data-ttu-id="9969a-2986">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-2986">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-2987">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-2987">fx_media_check</span></span>
- <span data-ttu-id="9969a-2988">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-2988">fx_media_close</span></span>
- <span data-ttu-id="9969a-2989">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2989">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-2990">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2990">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-2991">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2991">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-2992">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-2992">fx_media_flush</span></span>
- <span data-ttu-id="9969a-2993">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-2993">fx_media_format</span></span>
- <span data-ttu-id="9969a-2994">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-2994">fx_media_open</span></span>
- <span data-ttu-id="9969a-2995">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2995">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-2996">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-2996">fx_media_read</span></span>
- <span data-ttu-id="9969a-2997">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-2997">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-2998">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-2998">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-2999">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-2999">fx_media_write</span></span>
- <span data-ttu-id="9969a-3000">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-3000">fx_system_initialize</span></span>

## <a name="fx_media_volume_get_extended"></a><span data-ttu-id="9969a-3001">fx_media_volume_get_extended</span><span class="sxs-lookup"><span data-stu-id="9969a-3001">fx_media_volume_get_extended</span></span>

<span data-ttu-id="9969a-3002">Ottiene il nome del volume multimediale dei supporti aperti in precedenza</span><span class="sxs-lookup"><span data-stu-id="9969a-3002">Gets media volume name of previously opened media</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3003">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3003">Prototype</span></span>

```c
UINT fx_media_volume_get_extended(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name,
    UINT volume_name_buffer_length,
    UINT volume_source);
```
### <a name="description"></a><span data-ttu-id="9969a-3004">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3004">Description</span></span>

<span data-ttu-id="9969a-3005">Questo servizio recupera il nome del volume del supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-3005">This service retrieves the volume name of the previously opened media.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-3006">Questo servizio è identico a \***fx_media_volume_get()** _ ad eccezione del fatto che il chiamante passa le dimensioni del buffer _ \*volume_name\*\*.</span><span class="sxs-lookup"><span data-stu-id="9969a-3006">This service is identical to ***fx_media_volume_get()** _ except the caller passes in the size of the _ *volume_name** buffer.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3007">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3007">Input Parameters</span></span>


- <span data-ttu-id="9969a-3008">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-3008">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-3009">**volume_name:** puntatore alla destinazione per il nome del volume.</span><span class="sxs-lookup"><span data-stu-id="9969a-3009">**volume_name**: Pointer to destination for volume name.</span></span> <span data-ttu-id="9969a-3010">Si noti che la destinazione deve essere almeno sufficientemente grande da contenere 12 caratteri.</span><span class="sxs-lookup"><span data-stu-id="9969a-3010">Note that the destination must be at least large enough to hold 12 characters.</span></span>
- <span data-ttu-id="9969a-3011">**volume_name_buffer_length**: dimensioni del buffer volume_name.</span><span class="sxs-lookup"><span data-stu-id="9969a-3011">**volume_name_buffer_length**: Size of volume_name buffer.</span></span>
- <span data-ttu-id="9969a-3012">**volume_source**: indica dove recuperare il nome, dal settore di avvio o dalla directory radice.</span><span class="sxs-lookup"><span data-stu-id="9969a-3012">**volume_source**: Designates where to retrieve the name, either from the boot sector or the root directory.</span></span> <span data-ttu-id="9969a-3013">I valori validi per questo parametro sono:</span><span class="sxs-lookup"><span data-stu-id="9969a-3013">Valid values for this parameter are:</span></span>
  - <span data-ttu-id="9969a-3014">FX_BOOT_SECTOR</span><span class="sxs-lookup"><span data-stu-id="9969a-3014">FX_BOOT_SECTOR</span></span>
  - <span data-ttu-id="9969a-3015">FX_DIRECTORY_SECTOR</span><span class="sxs-lookup"><span data-stu-id="9969a-3015">FX_DIRECTORY_SECTOR</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3016">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3016">Return Values</span></span>

- <span data-ttu-id="9969a-3017">**FX_SUCCESS** (0x00) Volume multimediale riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3017">**FX_SUCCESS** (0x00) Successful media volume get.</span></span>
- <span data-ttu-id="9969a-3018">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-3018">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-3019">**FX_NOT_FOUND** volume (0x04) non trovato.</span><span class="sxs-lookup"><span data-stu-id="9969a-3019">**FX_NOT_FOUND** (0x04) Volume not found.</span></span>
- <span data-ttu-id="9969a-3020">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-3020">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-3021">**FX_PTR_ERROR** (0x18) Supporto non valido o puntatore di destinazione del volume.</span><span class="sxs-lookup"><span data-stu-id="9969a-3021">**FX_PTR_ERROR** (0x18) Invalid media or volume destination pointer.</span></span>
- <span data-ttu-id="9969a-3022">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-3022">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3023">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3023">Allowed From</span></span>

<span data-ttu-id="9969a-3024">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3024">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3025">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3025">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             volume_name[12];

/* Retrieve the volume name of the RAM disk, from the boot sector. */

status = fx_media_volume_get_extended(&ram_disk, volume_name,
                                      sizeof(volume_name),
                                      FX_BOOT_SECTOR);

/* If status is FX_SUCCESS, the volume name was successfully retrieved. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3026">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3026">See Also</span></span>

- <span data-ttu-id="9969a-3027">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-3027">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-3028">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-3028">fx_media_abort</span></span>
- <span data-ttu-id="9969a-3029">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-3029">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-3030">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-3030">fx_media_check</span></span>
- <span data-ttu-id="9969a-3031">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-3031">fx_media_close</span></span>
- <span data-ttu-id="9969a-3032">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3032">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-3033">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-3033">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-3034">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-3034">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-3035">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-3035">fx_media_flush</span></span>
- <span data-ttu-id="9969a-3036">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-3036">fx_media_format</span></span>
- <span data-ttu-id="9969a-3037">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-3037">fx_media_open</span></span>
- <span data-ttu-id="9969a-3038">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3038">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-3039">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3039">fx_media_read</span></span>
- <span data-ttu-id="9969a-3040">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-3040">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-3041">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3041">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-3042">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-3042">fx_media_write</span></span>
- <span data-ttu-id="9969a-3043">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-3043">fx_system_initialize</span></span>

## <a name="fx_media_volume_set"></a><span data-ttu-id="9969a-3044">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3044">fx_media_volume_set</span></span>

<span data-ttu-id="9969a-3045">Imposta il nome del volume multimediale</span><span class="sxs-lookup"><span data-stu-id="9969a-3045">Sets media volume name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3046">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3046">Prototype</span></span>

```c
UINT fx_media_volume_set(
    FX_MEDIA *media_ptr, 
    CHAR *volume_name);
```
### <a name="description"></a><span data-ttu-id="9969a-3047">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3047">Description</span></span>

<span data-ttu-id="9969a-3048">Questo servizio imposta il nome del volume del supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-3048">This service sets the volume name of the previously opened media.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3049">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3049">Input Parameters</span></span>

- <span data-ttu-id="9969a-3050">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-3050">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-3051">**volume_name**: puntatore al nome del volume.</span><span class="sxs-lookup"><span data-stu-id="9969a-3051">**volume_name**: Pointer to the volume name.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3052">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3052">Return Values</span></span>

- <span data-ttu-id="9969a-3053">**FX_SUCCESS** (0x00) Set di volumi multimediali riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3053">**FX_SUCCESS** (0x00) Successful media volume set.</span></span>
- <span data-ttu-id="9969a-3054">**FX_INVALID_NAME** (0x0C) Volume_name non è valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-3054">**FX_INVALID_NAME** (0x0C) Volume_name is invalid.</span></span>
- <span data-ttu-id="9969a-3055">**FX_MEDIA_INVALID** (0x02) Impossibile impostare il nome del volume.</span><span class="sxs-lookup"><span data-stu-id="9969a-3055">**FX_MEDIA_INVALID** (0x02) Unable to set volume name.</span></span>
- <span data-ttu-id="9969a-3056">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-3056">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-3057">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-3057">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-3058">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-3058">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-3059">**FX_PTR_ERROR** (0x18) Supporto o puntatore del nome di volume non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-3059">**FX_PTR_ERROR** (0x18) Invalid media or volume name pointer.</span></span>
- <span data-ttu-id="9969a-3060">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-3060">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3061">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3061">Allowed From</span></span>

<span data-ttu-id="9969a-3062">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3062">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3063">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3063">Example</span></span>

```c
FX_MEDIA ram_disk;

/* Set the volume name to "MY_VOLUME". */

status = fx_media_volume_set(&ram_disk, "MY_VOLUME");

/* If status is FX_SUCCESS, the volume name was successfully set. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3064">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3064">See Also</span></span>

- <span data-ttu-id="9969a-3065">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-3065">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-3066">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-3066">fx_media_abort</span></span>
- <span data-ttu-id="9969a-3067">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-3067">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-3068">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-3068">fx_media_check</span></span>
- <span data-ttu-id="9969a-3069">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-3069">fx_media_close</span></span>
- <span data-ttu-id="9969a-3070">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3070">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-3071">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-3071">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-3072">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-3072">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-3073">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-3073">fx_media_flush</span></span>
- <span data-ttu-id="9969a-3074">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-3074">fx_media_format</span></span>
- <span data-ttu-id="9969a-3075">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-3075">fx_media_open</span></span>
- <span data-ttu-id="9969a-3076">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3076">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-3077">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3077">fx_media_read</span></span>
- <span data-ttu-id="9969a-3078">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-3078">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-3079">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3079">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-3080">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-3080">fx_media_write</span></span>
- <span data-ttu-id="9969a-3081">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-3081">fx_system_initialize</span></span>

## <a name="fx_media_write"></a><span data-ttu-id="9969a-3082">fx_media_write</span><span class="sxs-lookup"><span data-stu-id="9969a-3082">fx_media_write</span></span>

<span data-ttu-id="9969a-3083">Scrive un settore logico</span><span class="sxs-lookup"><span data-stu-id="9969a-3083">Writes logical sector</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3084">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3084">Prototype</span></span>

```c
UINT fx_media_write(
    FX_MEDIA *media_ptr, 
    ULONG logical_sector,
    VOID *buffer_ptr);
```
### <a name="description"></a><span data-ttu-id="9969a-3085">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3085">Description</span></span>

<span data-ttu-id="9969a-3086">Questo servizio scrive il buffer fornito nel settore logico specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-3086">This service writes the supplied buffer to the specified logical sector.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3087">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3087">Input Parameters</span></span>

- <span data-ttu-id="9969a-3088">**media_ptr:** puntatore a un supporto aperto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9969a-3088">**media_ptr**: Pointer to a previously opened media.</span></span>
- <span data-ttu-id="9969a-3089">**logical_sector:** settore logico da scrivere.</span><span class="sxs-lookup"><span data-stu-id="9969a-3089">**logical_sector**: Logical sector to write.</span></span>
- <span data-ttu-id="9969a-3090">**buffer_ptr**: puntatore all'origine per la scrittura del settore logico.</span><span class="sxs-lookup"><span data-stu-id="9969a-3090">**buffer_ptr**: Pointer to the source for the logical sector write.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3091">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3091">Return Values</span></span>

- <span data-ttu-id="9969a-3092">**FX_SUCCESS** (0x00) Scrittura su supporti completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-3092">**FX_SUCCESS** (0x00) Successful media write.</span></span>
- <span data-ttu-id="9969a-3093">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-3093">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-3094">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-3094">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-3095">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-3095">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-3096">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-3096">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-3097">**FX_PTR_ERROR** (0x18) Puntatore multimediale non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-3097">**FX_PTR_ERROR** (0x18) Invalid media pointer.</span></span>
- <span data-ttu-id="9969a-3098">**FX_CALLER_ERROR**    (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-3098">**FX_CALLER_ERROR**    (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3099">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3099">Allowed From</span></span>

<span data-ttu-id="9969a-3100">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3100">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3101">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3101">Example</span></span>

```c
FX_MEDIA             my_media;
UCHAR                 my_buffer[128];
UINT                 status;

/* Write logical sector 22 from "my_buffer" assuming
    the physical media has a sector size of 128. */

status = fx_media_write(&my_media, 22, my_buffer);

/* If status equals FX_SUCCESS, the contents of logical
    sector 22 are now the same as "my_buffer." */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3102">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3102">See Also</span></span>

- <span data-ttu-id="9969a-3103">fx_fault_tolerant_enable</span><span class="sxs-lookup"><span data-stu-id="9969a-3103">fx_fault_tolerant_enable</span></span>
- <span data-ttu-id="9969a-3104">fx_media_abort</span><span class="sxs-lookup"><span data-stu-id="9969a-3104">fx_media_abort</span></span>
- <span data-ttu-id="9969a-3105">fx_media_cache_invalidate</span><span class="sxs-lookup"><span data-stu-id="9969a-3105">fx_media_cache_invalidate</span></span>
- <span data-ttu-id="9969a-3106">fx_media_check</span><span class="sxs-lookup"><span data-stu-id="9969a-3106">fx_media_check</span></span>
- <span data-ttu-id="9969a-3107">fx_media_close</span><span class="sxs-lookup"><span data-stu-id="9969a-3107">fx_media_close</span></span>
- <span data-ttu-id="9969a-3108">fx_media_close_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3108">fx_media_close_notify_set</span></span>
- <span data-ttu-id="9969a-3109">fx_media_exFAT_format</span><span class="sxs-lookup"><span data-stu-id="9969a-3109">fx_media_exFAT_format</span></span>
- <span data-ttu-id="9969a-3110">fx_media_extended_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-3110">fx_media_extended_space_available</span></span>
- <span data-ttu-id="9969a-3111">fx_media_flush</span><span class="sxs-lookup"><span data-stu-id="9969a-3111">fx_media_flush</span></span>
- <span data-ttu-id="9969a-3112">fx_media_format</span><span class="sxs-lookup"><span data-stu-id="9969a-3112">fx_media_format</span></span>
- <span data-ttu-id="9969a-3113">fx_media_open</span><span class="sxs-lookup"><span data-stu-id="9969a-3113">fx_media_open</span></span>
- <span data-ttu-id="9969a-3114">fx_media_open_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3114">fx_media_open_notify_set</span></span>
- <span data-ttu-id="9969a-3115">fx_media_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3115">fx_media_read</span></span>
- <span data-ttu-id="9969a-3116">fx_media_space_available</span><span class="sxs-lookup"><span data-stu-id="9969a-3116">fx_media_space_available</span></span>
- <span data-ttu-id="9969a-3117">fx_media_volume_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3117">fx_media_volume_get</span></span>
- <span data-ttu-id="9969a-3118">fx_media_volume_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3118">fx_media_volume_set</span></span>
- <span data-ttu-id="9969a-3119">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-3119">fx_system_initialize</span></span>

## <a name="fx_system_date_get"></a><span data-ttu-id="9969a-3120">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3120">fx_system_date_get</span></span>

<span data-ttu-id="9969a-3121">Ottiene file system data</span><span class="sxs-lookup"><span data-stu-id="9969a-3121">Gets file system date</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3122">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3122">Prototype</span></span>

```c
UINT fx_system_date_get(
    UINT *year, 
    UINT *month, 
    UINT *day);
```
### <a name="description"></a><span data-ttu-id="9969a-3123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3123">Description</span></span>

<span data-ttu-id="9969a-3124">Questo servizio restituisce la data di sistema corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-3124">This service returns the current system date.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3125">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3125">Input Parameters</span></span>

- <span data-ttu-id="9969a-3126">**year:** puntatore alla destinazione per l'anno.</span><span class="sxs-lookup"><span data-stu-id="9969a-3126">**year**: Pointer to destination for year.</span></span>
- <span data-ttu-id="9969a-3127">**month:** puntatore alla destinazione per month.</span><span class="sxs-lookup"><span data-stu-id="9969a-3127">**month**: Pointer to destination for month.</span></span>
- <span data-ttu-id="9969a-3128">**day:** puntatore alla destinazione per il giorno.</span><span class="sxs-lookup"><span data-stu-id="9969a-3128">**day**: Pointer to destination for day.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3129">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3129">Return Values</span></span>

- <span data-ttu-id="9969a-3130">**FX_SUCCESS** (0x00) Recupero della data riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3130">**FX_SUCCESS** (0x00) Successful date retrieval.</span></span>
- <span data-ttu-id="9969a-3131">**FX_PTR_ERROR** (0x18) Uno o più parametri di input sono NULL.</span><span class="sxs-lookup"><span data-stu-id="9969a-3131">**FX_PTR_ERROR** (0x18) One or more of the input parameters are NULL.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3132">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3132">Allowed From</span></span>

<span data-ttu-id="9969a-3133">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3133">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3134">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3134">Example</span></span>

```c
UINT            status;
UINT            year;
UINT            month;
UINT            day;
/* Retrieve the current system date. */

status = fx_system_date_get(&year, &month, &day);

/* If status equals FX_SUCCESS, the year, month,
    and day parameters now have meaningful information. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3135">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3135">See Also</span></span>

- <span data-ttu-id="9969a-3136">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3136">fx_system_date_set</span></span>
- <span data-ttu-id="9969a-3137">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-3137">fx_system_initialize</span></span>
- <span data-ttu-id="9969a-3138">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3138">fx_system_time_get</span></span>
- <span data-ttu-id="9969a-3139">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3139">fx_system_time_set</span></span>

## <a name="fx_system_date_set"></a><span data-ttu-id="9969a-3140">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3140">fx_system_date_set</span></span>

<span data-ttu-id="9969a-3141">Imposta la data di sistema</span><span class="sxs-lookup"><span data-stu-id="9969a-3141">Sets system date</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3142">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3142">Prototype</span></span>

```c
UINT fx_system_date_set(
    UINT year, 
    UINT month, 
    UINT day);
```

### <a name="description"></a><span data-ttu-id="9969a-3143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3143">Description</span></span>

<span data-ttu-id="9969a-3144">Questo servizio imposta la data di sistema come specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-3144">This service sets the system date as specified.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-3145">*Questo servizio deve essere chiamato subito dopo **il** fx_system_initialize impostare la data di sistema iniziale. Per impostazione predefinita, la data di sistema è quella dell'ultima versione generica di FileX.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3145">*This service should be called shortly after **fx_system_initialize** to set the initial system date. By default, the system date is that of the last generic FileX release.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3146">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3146">Input Parameters</span></span>

- <span data-ttu-id="9969a-3147">**year:** nuovo anno.</span><span class="sxs-lookup"><span data-stu-id="9969a-3147">**year**: New year.</span></span> <span data-ttu-id="9969a-3148">L'intervallo valido è compreso tra il 1980 e l'anno 2107.</span><span class="sxs-lookup"><span data-stu-id="9969a-3148">The valid range is from 1980 through the year 2107.</span></span>
- <span data-ttu-id="9969a-3149">**month:** nuovo mese.</span><span class="sxs-lookup"><span data-stu-id="9969a-3149">**month**: New month.</span></span> <span data-ttu-id="9969a-3150">L'intervallo valido è compreso tra 1 e 12.</span><span class="sxs-lookup"><span data-stu-id="9969a-3150">The valid range is from 1 through 12.</span></span>
- <span data-ttu-id="9969a-3151">**day:** nuovo giorno.</span><span class="sxs-lookup"><span data-stu-id="9969a-3151">**day**: New day.</span></span> <span data-ttu-id="9969a-3152">L'intervallo valido è compreso tra 1 e 31, a seconda delle condizioni del mese e dell'anno bisestile.</span><span class="sxs-lookup"><span data-stu-id="9969a-3152">The valid range is from 1 through 31, depending on month and leap year conditions.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3153">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3153">Return Values</span></span>

- <span data-ttu-id="9969a-3154">**FX_SUCCESS** (0x00) Data riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-3154">**FX_SUCCESS** (0x00) Successful date setting.</span></span>
- <span data-ttu-id="9969a-3155">**FX_INVALID_YEAR** (0x12) Anno non valido specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-3155">**FX_INVALID_YEAR** (0x12) Invalid year specified.</span></span>
- <span data-ttu-id="9969a-3156">**FX_INVALID_MONTH** specificato 0x13 mese non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-3156">**FX_INVALID_MONTH** (0x13) Invalid month specified.</span></span>
- <span data-ttu-id="9969a-3157">**FX_INVALID_DAY** (0x14) Giorno non valido specificato.</span><span class="sxs-lookup"><span data-stu-id="9969a-3157">**FX_INVALID_DAY** (0x14) Invalid day specified.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3158">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3158">Allowed From</span></span>

<span data-ttu-id="9969a-3159">Inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3159">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3160">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3160">Example</span></span>

```c
 UINT             status;

/* Set the system date to December 12, 2005. */

status = fx_system_date_set(2005, 12, 12);

/* If status equals FX_SUCCESS, the file system date is now
    12-12-2005. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3161">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3161">See Also</span></span>

- <span data-ttu-id="9969a-3162">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3162">fx_system_date_get</span></span>
- <span data-ttu-id="9969a-3163">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-3163">fx_system_initialize</span></span>
- <span data-ttu-id="9969a-3164">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3164">fx_system_time_get</span></span>
- <span data-ttu-id="9969a-3165">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3165">fx_system_time_set</span></span>

## <a name="fx_system_initialize"></a><span data-ttu-id="9969a-3166">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-3166">fx_system_initialize</span></span>

<span data-ttu-id="9969a-3167">Inizializza l'intero sistema</span><span class="sxs-lookup"><span data-stu-id="9969a-3167">Initializes entire system</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3168">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3168">Prototype</span></span>

```c
VOID fx_system_initialize(void);
```

### <a name="description"></a><span data-ttu-id="9969a-3169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3169">Description</span></span>

<span data-ttu-id="9969a-3170">Questo servizio inizializza tutte le principali strutture di dati FileX.</span><span class="sxs-lookup"><span data-stu-id="9969a-3170">This service initializes all the major FileX data structures.</span></span> <span data-ttu-id="9969a-3171">Deve essere chiamato  in tx_application_define o possibilmente da un thread di inizializzazione e deve essere chiamato prima di usare qualsiasi altro servizio FileX.</span><span class="sxs-lookup"><span data-stu-id="9969a-3171">It should be called either in ***tx_application_define*** or possibly from an initialization thread and must be called prior to using any other FileX service.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-3172">\*Dopo l'inizializzazione da questa chiamata, l'applicazione deve chiamare fx_system_date_set _ e _ fx_system_time_set \* per iniziare con una data e un'ora di sistema *accurate.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3172">*Once initialized by this call, the application should call ***fx_system_date_set** _ and _ *fx_system_time_set** to start with an accurate system date and time.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3173">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3173">Input Parameters</span></span>

<span data-ttu-id="9969a-3174">Nessuno</span><span class="sxs-lookup"><span data-stu-id="9969a-3174">None</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3175">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3175">Return Values</span></span>

<span data-ttu-id="9969a-3176">Nessuno.</span><span class="sxs-lookup"><span data-stu-id="9969a-3176">None.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3177">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3177">Allowed From</span></span>

<span data-ttu-id="9969a-3178">inizializzazione, thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3178">Initialization, threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3179">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3179">Example</span></span>

```c
void tx_application_define(VOID *free_memory)
{
    UINT status;
    /* Initialize the FileX system. */
    fx_system_initialize();
    /* Set the file system date. */
    fx_system_date_set(my_year, my_month, my_day);

    /* Set the file system time. */
    fx_system_time_set(my_hour, my_minute, my_second);

    /* Now perform all other initialization and possibly FileX media
        open calls if the corresponding driver does not block on the boot sector read. */

    ...

}
```

### <a name="see-also"></a><span data-ttu-id="9969a-3180">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3180">See Also</span></span>

- <span data-ttu-id="9969a-3181">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3181">fx_system_date_get</span></span>
- <span data-ttu-id="9969a-3182">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3182">fx_system_date_set</span></span>
- <span data-ttu-id="9969a-3183">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3183">fx_system_time_get</span></span>
- <span data-ttu-id="9969a-3184">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3184">fx_system_time_set</span></span>

## <a name="fx_system_time_get"></a><span data-ttu-id="9969a-3185">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3185">fx_system_time_get</span></span>

<span data-ttu-id="9969a-3186">Ottiene l'ora di sistema corrente</span><span class="sxs-lookup"><span data-stu-id="9969a-3186">Gets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3187">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3187">Prototype</span></span>

```c
UINT fx_system_time_get(
    UINT *hour,
    UINT *minute,
    UINT *second);
```

### <a name="description"></a><span data-ttu-id="9969a-3188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3188">Description</span></span>

<span data-ttu-id="9969a-3189">Questo servizio recupera l'ora di sistema corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-3189">This service retrieves the current system time.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3190">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3190">Input Parameters</span></span>

- <span data-ttu-id="9969a-3191">**hour:** puntatore alla destinazione per l'ora.</span><span class="sxs-lookup"><span data-stu-id="9969a-3191">**hour**: Pointer to destination for hour.</span></span>
- <span data-ttu-id="9969a-3192">**minute:** puntatore alla destinazione per minuti.</span><span class="sxs-lookup"><span data-stu-id="9969a-3192">**minute**: Pointer to destination for minute.</span></span>
- <span data-ttu-id="9969a-3193">**second:** puntatore alla destinazione per il secondo.</span><span class="sxs-lookup"><span data-stu-id="9969a-3193">**second**: Pointer to destination for second.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3194">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3194">Return Values</span></span>

- <span data-ttu-id="9969a-3195">**FX_SUCCESS** (0x00) Recupero dell'ora di sistema riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3195">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="9969a-3196">**FX_PTR_ERROR** (0x18) Uno o più parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3196">**FX_PTR_ERROR** (0x18) One or more of the input parameters</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3197">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3197">Allowed From</span></span>

<span data-ttu-id="9969a-3198">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3198">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3199">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3199">Example</span></span>

```c
UINT             status;
UINT             hour;
UINT             minute;
UINT             second;

/* Retrieve the current system time. */

status = fx_system_time_get(&hour, &minute, &second);

/* If status equals FX_SUCCESS, the current system time
    is in the hour, minute, and second variables. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3200">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3200">See Also</span></span>

- <span data-ttu-id="9969a-3201">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3201">fx_system_date_get</span></span>
- <span data-ttu-id="9969a-3202">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3202">fx_system_date_set</span></span>
- <span data-ttu-id="9969a-3203">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-3203">fx_system_initialize</span></span>
- <span data-ttu-id="9969a-3204">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3204">fx_system_time_set</span></span>

## <a name="fx_system_time_set"></a><span data-ttu-id="9969a-3205">fx_system_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3205">fx_system_time_set</span></span>

<span data-ttu-id="9969a-3206">Imposta l'ora di sistema corrente</span><span class="sxs-lookup"><span data-stu-id="9969a-3206">Sets current system time</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3207">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3207">Prototype</span></span>

```c
UINT fx_system_time_set(UINT hour, UINT minute, UINT second);
```

### <a name="description"></a><span data-ttu-id="9969a-3208">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3208">Description</span></span>

<span data-ttu-id="9969a-3209">Questo servizio imposta l'ora di sistema corrente su quella specificata dai parametri di input.</span><span class="sxs-lookup"><span data-stu-id="9969a-3209">This service sets the current system time to that specified by the input parameters.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-3210">*Questo servizio deve essere  chiamato subito dopo l'fx_system_initialize per impostare l'ora di sistema iniziale. Per impostazione predefinita, l'ora di sistema è 0:0:0.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3210">*This service should be called shortly after **fx_system_initialize** to set the initial system time. By default, the system time is 0:0:0.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3211">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3211">Input Parameters</span></span>

- <span data-ttu-id="9969a-3212">**hour**: nuova ora (0-23).</span><span class="sxs-lookup"><span data-stu-id="9969a-3212">**hour**: New hour (0-23).</span></span>
- <span data-ttu-id="9969a-3213">**minute**: nuovo minuto (0-59).</span><span class="sxs-lookup"><span data-stu-id="9969a-3213">**minute**: New minute (0-59).</span></span>
- <span data-ttu-id="9969a-3214">**second**: nuovo secondo (0-59).</span><span class="sxs-lookup"><span data-stu-id="9969a-3214">**second**: New second (0-59).</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3215">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3215">Return Values</span></span>

- <span data-ttu-id="9969a-3216">**FX_SUCCESS** (0x00) Recupero dell'ora di sistema riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3216">**FX_SUCCESS** (0x00) Successful system time retrieval.</span></span>
- <span data-ttu-id="9969a-3217">**FX_INVALID_HOUR**    (0x15) Nuova ora non è valida.</span><span class="sxs-lookup"><span data-stu-id="9969a-3217">**FX_INVALID_HOUR**    (0x15) New hour is invalid.</span></span>
- <span data-ttu-id="9969a-3218">**FX_INVALID_MINUTE** (0x16) Nuovo minuto non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-3218">**FX_INVALID_MINUTE** (0x16) New minute is invalid.</span></span>
- <span data-ttu-id="9969a-3219">**FX_INVALID_SECOND** (0x17) Nuovo secondo non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-3219">**FX_INVALID_SECOND** (0x17) New second is invalid.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3220">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3220">Allowed From</span></span>

<span data-ttu-id="9969a-3221">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3221">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3222">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3222">Example</span></span>

```c
 UINT status;

/* Set the current system time to hour 23, minute 21, and second 20. */

status = fx_system_time_set(23, 21, 20);

/* If status is FX_SUCCESS, the current system time has been set. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3223">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3223">See Also</span></span>

- <span data-ttu-id="9969a-3224">fx_system_date_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3224">fx_system_date_get</span></span>
- <span data-ttu-id="9969a-3225">fx_system_date_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3225">fx_system_date_set</span></span>
- <span data-ttu-id="9969a-3226">fx_system_initialize</span><span class="sxs-lookup"><span data-stu-id="9969a-3226">fx_system_initialize</span></span>
- <span data-ttu-id="9969a-3227">fx_system_time_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3227">fx_system_time_get</span></span>

## <a name="fx_unicode_directory_create"></a><span data-ttu-id="9969a-3228">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3228">fx_unicode_directory_create</span></span>

<span data-ttu-id="9969a-3229">Crea una directory Unicode</span><span class="sxs-lookup"><span data-stu-id="9969a-3229">Creates a Unicode directory</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3230">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3230">Prototype</span></span>

```c
UINT fx_unicode_directory_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```
### <a name="description"></a><span data-ttu-id="9969a-3231">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3231">Description</span></span>

<span data-ttu-id="9969a-3232">Questo servizio crea una sottodirectory denominata Unicode nella directory predefinita corrente. Non sono consentite informazioni sul percorso nel parametro del nome di origine Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3232">This service creates a Unicode-named subdirectory in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="9969a-3233">In caso di esito positivo, il nome breve (formato 8.3) della sottodirectory Unicode appena creata viene restituito dal servizio.</span><span class="sxs-lookup"><span data-stu-id="9969a-3233">If successful, the short name (8.3 format) of the newly created Unicode subdirectory is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-3234">*Tutte le operazioni nella sottodirectory Unicode (che lo rende il percorso predefinito, l'eliminazione e così via) devono essere eseguite fornendo il nome breve restituito (formato 8.3) ai servizi directory FileX standard.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3234">*All operations on the Unicode subdirectory (making it the default path, deleting, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX directory services.*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-3235">*Questo servizio non è supportato nei supporti exFAT.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3235">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3236">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3236">Input Parameters</span></span>

- <span data-ttu-id="9969a-3237">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-3237">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-3238">**source_unicode_name:** puntatore al nome Unicode per la nuova sottodirectory.</span><span class="sxs-lookup"><span data-stu-id="9969a-3238">**source_unicode_name**: Pointer to the Unicode name for the new subdirectory.</span></span>
- <span data-ttu-id="9969a-3239">**source_unicode_length**: lunghezza del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3239">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="9969a-3240">**short_name:** puntatore alla destinazione per il nome breve (formato 8.3) per la nuova sottodirectory Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3240">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode subdirectory.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3241">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3241">Return Values</span></span>

- <span data-ttu-id="9969a-3242">**FX_SUCCESS** (0x00) Creazione della directory Unicode riuscita.</span><span class="sxs-lookup"><span data-stu-id="9969a-3242">**FX_SUCCESS** (0x00) Successful Unicode directory create.</span></span>
- <span data-ttu-id="9969a-3243">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-3243">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-3244">**FX_ALREADY_CREATED** (0x0B) La directory specificata esiste già.</span><span class="sxs-lookup"><span data-stu-id="9969a-3244">**FX_ALREADY_CREATED** (0x0B) Specified directory already exists.</span></span>
- <span data-ttu-id="9969a-3245">**FX_NO_MORE_SPACE** (0x0A) Nessun altro cluster disponibile nel supporto per la nuova voce di directory.</span><span class="sxs-lookup"><span data-stu-id="9969a-3245">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new directory entry.</span></span>
- <span data-ttu-id="9969a-3246">**FX_NOT_IMPLEMENTED** servizio (0x22) non implementato per l'file system exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-3246">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="9969a-3247">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-3247">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-3248">**FX_PTR_ERROR** (0x18) Supporti o puntatori nome non validi.</span><span class="sxs-lookup"><span data-stu-id="9969a-3248">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="9969a-3249">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-3249">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="9969a-3250">**FX_IO_ERROR (0x90)** Errore di I/O del driver.</span><span class="sxs-lookup"><span data-stu-id="9969a-3250">**FX_IO_ERROR    (0x90)** Driver I/O error.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3251">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3251">Allowed From</span></span>

<span data-ttu-id="9969a-3252">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3252">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3253">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3253">Example</span></span>

```c
FX_MEDIA             ram_disk;
UCHAR                 my_short_name[13];
UCHAR                 my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                         0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                         0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                         0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                         0x63,0x00, 0x00,0x00};

/* Create a Unicode subdirectory with the name contained in "my_unicode_name". */

length = fx_unicode_directory_create(&ram_disk, my_unicode_name, 17, my_short_name);

/* If successful, the Unicode subdirectory is created and "my_short_name"
    contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3254">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3254">See Also</span></span>

- <span data-ttu-id="9969a-3255">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3255">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-3256">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3256">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-3257">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3257">fx_directory_create</span></span>
- <span data-ttu-id="9969a-3258">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3258">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-3259">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3259">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-3260">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-3260">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-3261">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-3261">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-3262">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-3262">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-3263">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3263">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-3264">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-3264">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-3265">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3265">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-3266">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-3266">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-3267">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3267">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-3268">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3268">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-3269">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-3269">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-3270">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-3270">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-3271">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-3271">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-3272">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3272">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-3273">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3273">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-3274">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3274">fx_unicode_directory_rename</span></span>

## <a name="fx_unicode_directory_rename"></a><span data-ttu-id="9969a-3275">fx_unicode_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3275">fx_unicode_directory_rename</span></span>

<span data-ttu-id="9969a-3276">Rinomina la directory usando una stringa Unicode</span><span class="sxs-lookup"><span data-stu-id="9969a-3276">Renames directory using Unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3277">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3277">Prototype</span></span>

```c
UINT fx_unicode_directory_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length,
    CHAR *new_short_name);
```
### <a name="description"></a><span data-ttu-id="9969a-3278">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3278">Description</span></span>

<span data-ttu-id="9969a-3279">Questo servizio modifica una sottodirectory con nome Unicode in un nuovo nome Unicode specificato nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-3279">This service changes a Unicode-named subdirectory to specified new Unicode name in current working directory.</span></span> <span data-ttu-id="9969a-3280">I parametri del nome Unicode non devono avere informazioni sul percorso.</span><span class="sxs-lookup"><span data-stu-id="9969a-3280">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-3281">*Questo servizio non è supportato nei supporti exFAT.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3281">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3282">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3282">Input Parameters</span></span>

- <span data-ttu-id="9969a-3283">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-3283">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-3284">**old_unicode_name:** puntatore al nome Unicode per il file corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-3284">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="9969a-3285">**old_unicode_name_length**: lunghezza del nome Unicode corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-3285">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="9969a-3286">**new_unicode_name:** puntatore al nuovo nome file Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3286">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="9969a-3287">**old_unicode_name_length:** lunghezza del nuovo nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3287">**old_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="9969a-3288">**new_short_name:** puntatore alla destinazione per il nome breve (formato 8.3) per il file Unicode rinominato.</span><span class="sxs-lookup"><span data-stu-id="9969a-3288">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span> <span data-ttu-id="9969a-3289">Rinominare la directory con Unicode</span><span class="sxs-lookup"><span data-stu-id="9969a-3289">Rename Directory with Unicode</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3290">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3290">Return Values</span></span>

- <span data-ttu-id="9969a-3291">**FX_SUCCESS** (0x00) Apertura dei supporti completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-3291">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="9969a-3292">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-3292">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-3293">**FX_ALREADY_CREATED** (0x0B) Il nome di directory specificato esiste già.</span><span class="sxs-lookup"><span data-stu-id="9969a-3293">**FX_ALREADY_CREATED** (0x0B) Specified directory name already exists.</span></span>
- <span data-ttu-id="9969a-3294">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-3294">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-3295">**FX_PTR_ERROR** (0x18) Uno o più puntatori sono NULL.</span><span class="sxs-lookup"><span data-stu-id="9969a-3295">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="9969a-3296">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-3296">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>
- <span data-ttu-id="9969a-3297">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-3297">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3298">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3298">Allowed From</span></span>

<span data-ttu-id="9969a-3299">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3299">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3300">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3300">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
UCHAR                 my_short_name[13];
UCHAR                 my_old_unicode_name[] = {'a', '\0', 'b', '\0', 'c', '\0', '\0', '\0'};
UCHAR                 my_new_unicode_name[] = {'d', '\0', 'e', '\0', 'f', '\0', '\0', '\0'};

/* Change the Unicode-named file "abc" to "def". */

status = fx_unicode_directory_rename(&my_media, my_old_unicode_name,
    3, my_new_unicode_name, 3, my_short_name);

/* If status equals FX_SUCCESS, the directory was changed to "def" and
    "my_short_name" contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3301">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3301">See Also</span></span>

- <span data-ttu-id="9969a-3302">fx_directory_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3302">fx_directory_attributes_read</span></span>
- <span data-ttu-id="9969a-3303">fx_directory_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3303">fx_directory_attributes_set</span></span>
- <span data-ttu-id="9969a-3304">fx_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3304">fx_directory_create</span></span>
- <span data-ttu-id="9969a-3305">fx_directory_default_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3305">fx_directory_default_get</span></span>
- <span data-ttu-id="9969a-3306">fx_directory_default_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3306">fx_directory_default_set</span></span>
- <span data-ttu-id="9969a-3307">fx_directory_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-3307">fx_directory_delete</span></span>
- <span data-ttu-id="9969a-3308">fx_directory_first_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-3308">fx_directory_first_entry_find</span></span>
- <span data-ttu-id="9969a-3309">fx_directory_first_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-3309">fx_directory_first_full_entry_find</span></span>
- <span data-ttu-id="9969a-3310">fx_directory_information_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3310">fx_directory_information_get</span></span>
- <span data-ttu-id="9969a-3311">fx_directory_local_path_clear</span><span class="sxs-lookup"><span data-stu-id="9969a-3311">fx_directory_local_path_clear</span></span>
- <span data-ttu-id="9969a-3312">fx_directory_local_path_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3312">fx_directory_local_path_get</span></span>
- <span data-ttu-id="9969a-3313">fx_directory_local_path_restore</span><span class="sxs-lookup"><span data-stu-id="9969a-3313">fx_directory_local_path_restore</span></span>
- <span data-ttu-id="9969a-3314">fx_directory_local_path_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3314">fx_directory_local_path_set</span></span>
- <span data-ttu-id="9969a-3315">fx_directory_long_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3315">fx_directory_long_name_get</span></span>
- <span data-ttu-id="9969a-3316">fx_directory_name_test</span><span class="sxs-lookup"><span data-stu-id="9969a-3316">fx_directory_name_test</span></span>
- <span data-ttu-id="9969a-3317">fx_directory_next_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-3317">fx_directory_next_entry_find</span></span>
- <span data-ttu-id="9969a-3318">fx_directory_next_full_entry_find</span><span class="sxs-lookup"><span data-stu-id="9969a-3318">fx_directory_next_full_entry_find</span></span>
- <span data-ttu-id="9969a-3319">fx_directory_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3319">fx_directory_rename</span></span>
- <span data-ttu-id="9969a-3320">fx_directory_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3320">fx_directory_short_name_get</span></span>
- <span data-ttu-id="9969a-3321">fx_unicode_directory_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3321">fx_unicode_directory_create</span></span>

## <a name="fx_unicode_file_create"></a><span data-ttu-id="9969a-3322">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3322">fx_unicode_file_create</span></span>

<span data-ttu-id="9969a-3323">Crea un file Unicode</span><span class="sxs-lookup"><span data-stu-id="9969a-3323">Creates a Unicode file</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3324">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3324">Prototype</span></span>

```c
UINT fx_unicode_file_create(
    FX_MEDIA *media_ptr, 
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *short_name);
```

### <a name="description"></a><span data-ttu-id="9969a-3325">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3325">Description</span></span>

<span data-ttu-id="9969a-3326">Questo servizio crea un file con nome Unicode nella directory predefinita corrente. Non sono consentite informazioni sul percorso nel parametro del nome di origine Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3326">This service creates a Unicode-named file in the current default directory—no path information is allowed in the Unicode source name parameter.</span></span> <span data-ttu-id="9969a-3327">In caso di esito positivo, il nome breve (formato 8.3) del file Unicode appena creato viene restituito dal servizio.</span><span class="sxs-lookup"><span data-stu-id="9969a-3327">If successful, the short name (8.3 format) of the newly created Unicode file is returned by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="9969a-3328">*Tutte le operazioni sul file Unicode (apertura, scrittura, lettura, chiusura e così via) devono essere eseguite fornendo il nome breve restituito (formato 8.3) ai servizi file FileX standard.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3328">*All operations on the Unicode file (opening, writing, reading, closing, etc.) should be done by supplying the returned short name (8.3 format) to the standard FileX file services.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3329">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3329">Input Parameters</span></span>


- <span data-ttu-id="9969a-3330">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-3330">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-3331">**source_unicode_name:** puntatore al nome Unicode per il nuovo file.</span><span class="sxs-lookup"><span data-stu-id="9969a-3331">**source_unicode_name**: Pointer to the Unicode name for the new file.</span></span>
- <span data-ttu-id="9969a-3332">**source_unicode_length**: lunghezza del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3332">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="9969a-3333">**short_name:** puntatore alla destinazione per il nome breve (formato 8.3) per il nuovo file Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3333">**short_name**: Pointer to destination for short name (8.3 format) for the new Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3334">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3334">Return Values</span></span>

- <span data-ttu-id="9969a-3335">**FX_SUCCESS** (0x00) Creazione del file completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-3335">**FX_SUCCESS** (0x00) Successful file create.</span></span>
- <span data-ttu-id="9969a-3336">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-3336">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-3337">**FX_ALREADY_CREATED** (0x0B) Il file specificato esiste già.</span><span class="sxs-lookup"><span data-stu-id="9969a-3337">**FX_ALREADY_CREATED** (0x0B) Specified file already exists.</span></span>
- <span data-ttu-id="9969a-3338">**FX_NO_MORE_SPACE** (0x0A) Nessun altro cluster disponibile nel supporto per la nuova voce di file.</span><span class="sxs-lookup"><span data-stu-id="9969a-3338">**FX_NO_MORE_SPACE** (0x0A) No more clusters available in the media for the new file entry.</span></span>
- <span data-ttu-id="9969a-3339">**FX_NOT_IMPLEMENTED** servizio (0x22) non implementato per l'file system exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-3339">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="9969a-3340">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-3340">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-3341">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-3341">**FX_WRITE_PROTECT** (0x23) Specified media is write protected.</span></span>
- <span data-ttu-id="9969a-3342">**FX_PTR_ERROR** (0x18) Supporti o puntatori nome non validi.</span><span class="sxs-lookup"><span data-stu-id="9969a-3342">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="9969a-3343">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-3343">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3344">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3344">Allowed From</span></span>

<span data-ttu-id="9969a-3345">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3345">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3346">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3346">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             my_short_name[13];
UCHAR             my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                     0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                     0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                     0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                     0x63,0x00, 0x00,0x00};

/* Create a Unicode file with the name contained in "my_unicode_name". */

length = fx_unicode_file_create(&ram_disk, my_unicode_name, 17, my_short_name);

/* If successful, the Unicode file is created and "my_short_name"
    contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3347">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3347">See Also</span></span>

- <span data-ttu-id="9969a-3348">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3348">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-3349">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3349">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-3350">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3350">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-3351">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3351">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3352">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-3352">fx_file_close</span></span>
- <span data-ttu-id="9969a-3353">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3353">fx_file_create</span></span>
- <span data-ttu-id="9969a-3354">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3354">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-3355">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-3355">fx_file_delete</span></span>
- <span data-ttu-id="9969a-3356">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3356">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-3357">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3357">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3358">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3358">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-3359">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3359">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-3360">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3360">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-3361">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3361">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-3362">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-3362">fx_file_open</span></span>
- <span data-ttu-id="9969a-3363">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3363">fx_file_read</span></span>
- <span data-ttu-id="9969a-3364">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3364">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-3365">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3365">fx_file_rename</span></span>
- <span data-ttu-id="9969a-3366">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3366">fx_file_seek</span></span>
- <span data-ttu-id="9969a-3367">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3367">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-3368">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3368">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-3369">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-3369">fx_file_write</span></span>
- <span data-ttu-id="9969a-3370">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3370">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-3371">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3371">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-3372">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3372">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-3373">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3373">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_file_rename"></a><span data-ttu-id="9969a-3374">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3374">fx_unicode_file_rename</span></span>

<span data-ttu-id="9969a-3375">Rinomina un file usando una stringa Unicode</span><span class="sxs-lookup"><span data-stu-id="9969a-3375">Renames a file using unicode string</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3376">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3376">Prototype</span></span>

```c
UINT fx_unicode_file_rename(
    FX_MEDIA *media_ptr, 
    UCHAR *old_unicode_name,
    ULONG old_unicode_length, 
    UCHAR *new_unicode_name,
    ULONG new_unicode_length, 
    CHAR *new_short_name);
```

### <a name="description"></a><span data-ttu-id="9969a-3377">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3377">Description</span></span>

<span data-ttu-id="9969a-3378">Questo servizio modifica un nome file denominato Unicode in un nuovo nome Unicode specificato nella directory predefinita corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-3378">This service changes a Unicode-named file name to specified new Unicode name in current default directory.</span></span> <span data-ttu-id="9969a-3379">I parametri del nome Unicode non devono avere informazioni sul percorso.</span><span class="sxs-lookup"><span data-stu-id="9969a-3379">The Unicode name parameters must not have path information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-3380">*Questo servizio non è supportato nei supporti exFAT.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3380">*This service is not supported on exFAT media.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3381">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3381">Input Parameters</span></span>

- <span data-ttu-id="9969a-3382">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-3382">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-3383">**old_unicode_name:** puntatore al nome Unicode per il file corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-3383">**old_unicode_name**: Pointer to the Unicode name for the current file.</span></span>
- <span data-ttu-id="9969a-3384">**old_unicode_name_length**: lunghezza del nome Unicode corrente.</span><span class="sxs-lookup"><span data-stu-id="9969a-3384">**old_unicode_name_length**: Length of current Unicode name.</span></span>
- <span data-ttu-id="9969a-3385">**new_unicode_name:** puntatore al nuovo nome file Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3385">**new_unicode_name**: Pointer to the new Unicode file name.</span></span>
- <span data-ttu-id="9969a-3386">**new_unicode_name_length**: lunghezza del nuovo nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3386">**new_unicode_name_length**: Length of new Unicode name.</span></span>
- <span data-ttu-id="9969a-3387">**new_short_name:** puntatore alla destinazione per il nome breve (formato 8.3) per il file Unicode rinominato.</span><span class="sxs-lookup"><span data-stu-id="9969a-3387">**new_short_name**: Pointer to destination for short name (8.3 format) for the renamed Unicode file.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3388">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3388">Return Values</span></span>


- <span data-ttu-id="9969a-3389">**FX_SUCCESS** (0x00) Apertura dei supporti completata.</span><span class="sxs-lookup"><span data-stu-id="9969a-3389">**FX_SUCCESS** (0x00) Successful media open.</span></span>
- <span data-ttu-id="9969a-3390">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-3390">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-3391">**FX_ALREADY_CREATED** (0x0B) Il nome file specificato esiste già.</span><span class="sxs-lookup"><span data-stu-id="9969a-3391">**FX_ALREADY_CREATED** (0x0B) Specified file name already exists.</span></span>
- <span data-ttu-id="9969a-3392">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-3392">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-3393">**FX_PTR_ERROR** (0x18) Uno o più puntatori sono NULL.</span><span class="sxs-lookup"><span data-stu-id="9969a-3393">**FX_PTR_ERROR** (0x18) One or more pointers are NULL.</span></span>
- <span data-ttu-id="9969a-3394">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-3394">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>
- <span data-ttu-id="9969a-3395">**FX_WRITE_PROTECT** (0x23) Il supporto specificato è protetto da scrittura.</span><span class="sxs-lookup"><span data-stu-id="9969a-3395">**FX_WRITE_PROTECT** (0x23) Specified media is write-protected.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3396">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3396">Allowed From</span></span>

<span data-ttu-id="9969a-3397">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3397">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3398">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3398">Example</span></span>

```c
FX_MEDIA             my_media;
UINT                 status;
UCHAR                 my_short_name[13];
UCHAR                 my_old_unicode_name[] = {'a', '\0', 'b', '\0', 'c', '\0', '\0', '\0'};
UCHAR                 my_new_unicode_name[] = {'d', '\0', 'e', '\0', 'f', '\0', '\0', '\0'};

/* Change the Unicode-named file "abc" to "def". */

status = fx_unicode_file_rename(&my_media, my_old_unicode_name,
    3, my_new_unicode_name, 3, my_short_name);

/* If status equals FX_SUCCESS, the file name was changed to "def" and
    "my_short_name" contains the 8.3 format name that can be used with other FileX services. */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3399">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3399">See Also</span></span>

- <span data-ttu-id="9969a-3400">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3400">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-3401">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3401">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-3402">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3402">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-3403">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3403">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3404">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-3404">fx_file_close</span></span>
- <span data-ttu-id="9969a-3405">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3405">fx_file_create</span></span>
- <span data-ttu-id="9969a-3406">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3406">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-3407">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-3407">fx_file_delete</span></span>
- <span data-ttu-id="9969a-3408">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3408">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-3409">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3409">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3410">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3410">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-3411">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3411">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-3412">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3412">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-3413">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3413">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-3414">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-3414">fx_file_open</span></span>
- <span data-ttu-id="9969a-3415">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3415">fx_file_read</span></span>
- <span data-ttu-id="9969a-3416">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3416">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-3417">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3417">fx_file_rename</span></span>
- <span data-ttu-id="9969a-3418">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3418">fx_file_seek</span></span>
- <span data-ttu-id="9969a-3419">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3419">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-3420">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3420">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-3421">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-3421">fx_file_write</span></span>
- <span data-ttu-id="9969a-3422">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3422">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-3423">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3423">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-3424">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3424">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-3425">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3425">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get"></a><span data-ttu-id="9969a-3426">fx_unicode_length_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3426">fx_unicode_length_get</span></span>

<span data-ttu-id="9969a-3427">Ottiene la lunghezza del nome Unicode</span><span class="sxs-lookup"><span data-stu-id="9969a-3427">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3428">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3428">Prototype</span></span>

```c
ULONG fx_unicode_length_get(UCHAR *unicode_name);
```
### <a name="description"></a><span data-ttu-id="9969a-3429">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3429">Description</span></span>

<span data-ttu-id="9969a-3430">Questo servizio determina la lunghezza del nome Unicode fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3430">This service determines the length of the supplied Unicode name.</span></span> <span data-ttu-id="9969a-3431">Un carattere Unicode è rappresentato da due byte.</span><span class="sxs-lookup"><span data-stu-id="9969a-3431">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="9969a-3432">Un nome Unicode è una serie di caratteri Unicode a due byte terminati da due byte NULL (due byte di valore 0).</span><span class="sxs-lookup"><span data-stu-id="9969a-3432">A Unicode name is a series of two byte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3433">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3433">Input Parameters</span></span>

<span data-ttu-id="9969a-3434">**unicode_name:** puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3434">**unicode_name**: Pointer to Unicode name.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3435">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3435">Return Values</span></span>

<span data-ttu-id="9969a-3436">**length**: lunghezza del nome Unicode (numero di caratteri Unicode nel nome).</span><span class="sxs-lookup"><span data-stu-id="9969a-3436">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3437">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3437">Allowed From</span></span>

<span data-ttu-id="9969a-3438">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3438">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3439">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3439">Example</span></span>

```c
UCHAR     my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                           0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                           0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                           0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                           0x63,0x00, 0x00,0x00};

UINT     length;

/* Get the length of "my_unicode_name". */

length = fx_unicode_length_get(my_unicode_name);

/* A value of 17 will be returned for the length of the "my_unicode_name". */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3440">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3440">See Also</span></span>

- <span data-ttu-id="9969a-3441">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3441">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-3442">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3442">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-3443">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3443">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-3444">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3444">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3445">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-3445">fx_file_close</span></span>
- <span data-ttu-id="9969a-3446">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3446">fx_file_create</span></span>
- <span data-ttu-id="9969a-3447">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3447">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-3448">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-3448">fx_file_delete</span></span>
- <span data-ttu-id="9969a-3449">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3449">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-3450">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3450">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3451">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3451">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-3452">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3452">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-3453">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3453">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-3454">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3454">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-3455">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-3455">fx_file_open</span></span>
- <span data-ttu-id="9969a-3456">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3456">fx_file_read</span></span>
- <span data-ttu-id="9969a-3457">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3457">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-3458">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3458">fx_file_rename</span></span>
- <span data-ttu-id="9969a-3459">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3459">fx_file_seek</span></span>
- <span data-ttu-id="9969a-3460">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3460">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-3461">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3461">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-3462">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-3462">fx_file_write</span></span>
- <span data-ttu-id="9969a-3463">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3463">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-3464">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3464">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-3465">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3465">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-3466">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3466">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-3467">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3467">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_length_get_extended"></a><span data-ttu-id="9969a-3468">fx_unicode_length_get_extended</span><span class="sxs-lookup"><span data-stu-id="9969a-3468">fx_unicode_length_get_extended</span></span>

<span data-ttu-id="9969a-3469">Ottiene la lunghezza del nome Unicode</span><span class="sxs-lookup"><span data-stu-id="9969a-3469">Gets length of Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3470">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3470">Prototype</span></span>

```c
UINT fx_unicode_length_get_extended(
    UCHAR *unicode_name,
    UINT buffer_length);
```
### <a name="description"></a><span data-ttu-id="9969a-3471">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3471">Description</span></span>

<span data-ttu-id="9969a-3472">Questo servizio ottiene la lunghezza del nome Unicode fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3472">This service gets the length of the supplied Unicode name.</span></span> <span data-ttu-id="9969a-3473">Un carattere Unicode è rappresentato da due byte.</span><span class="sxs-lookup"><span data-stu-id="9969a-3473">A Unicode character is represented by two bytes.</span></span> <span data-ttu-id="9969a-3474">Un nome Unicode è una serie di caratteri Unicode di due byte terminati da due byte NULL (due byte di valore 0).</span><span class="sxs-lookup"><span data-stu-id="9969a-3474">A Unicode name is a series of twobyte Unicode characters terminated by two NULL bytes (two bytes of 0 value).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-3475">*Questo servizio è identico **a fx_unicode_length_get(),** ad eccezione del fatto che il chiamante passa le dimensioni del buffer **unicode_name,** inclusi i due caratteri NULL.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3475">*This service is identical to **fx_unicode_length_get()** except the caller passes in the size of the **unicode_name** buffer, including the two NULL characters.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3476">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3476">Input Parameters</span></span>

- <span data-ttu-id="9969a-3477">**unicode_name:** puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3477">**unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="9969a-3478">**buffer_length**: dimensione del buffer dei nomi Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3478">**buffer_length**: Size of Unicode name buffer.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3479">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3479">Return Values</span></span>

<span data-ttu-id="9969a-3480">**length**: lunghezza del nome Unicode (numero di caratteri Unicode nel nome).</span><span class="sxs-lookup"><span data-stu-id="9969a-3480">**length**: Length of Unicode name (number of Unicode characters in the name).</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3481">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3481">Allowed From</span></span>

<span data-ttu-id="9969a-3482">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3482">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3483">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3483">Example</span></span>

```c
UCHAR         my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                 0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                 0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                 0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                 0x63,0x00, 0x00,0x00};

UINT         length;

/* Get the length of "my_unicode_name". */

length = fx_unicode_length_get_extended(my_unicode_name, sizeof(my_unicode_name));

/* A value of 17 will be returned for the length of the "my_unicode_name". */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3484">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3484">See Also</span></span>

- <span data-ttu-id="9969a-3485">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3485">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-3486">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3486">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-3487">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3487">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-3488">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3488">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3489">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-3489">fx_file_close</span></span>
- <span data-ttu-id="9969a-3490">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3490">fx_file_create</span></span>
- <span data-ttu-id="9969a-3491">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3491">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-3492">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-3492">fx_file_delete</span></span>
- <span data-ttu-id="9969a-3493">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3493">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-3494">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3494">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3495">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3495">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-3496">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3496">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-3497">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3497">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-3498">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3498">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-3499">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-3499">fx_file_open</span></span>
- <span data-ttu-id="9969a-3500">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3500">fx_file_read</span></span>
- <span data-ttu-id="9969a-3501">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3501">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-3502">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3502">fx_file_rename</span></span>
- <span data-ttu-id="9969a-3503">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3503">fx_file_seek</span></span>
- <span data-ttu-id="9969a-3504">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3504">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-3505">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3505">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-3506">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-3506">fx_file_write</span></span>
- <span data-ttu-id="9969a-3507">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3507">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-3508">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3508">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-3509">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3509">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-3510">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3510">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-3511">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3511">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get"></a><span data-ttu-id="9969a-3512">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3512">fx_unicode_name_get</span></span>

<span data-ttu-id="9969a-3513">Ottiene il nome Unicode dal nome breve</span><span class="sxs-lookup"><span data-stu-id="9969a-3513">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3514">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3514">Prototype</span></span>

```c
UINT fx_unicode_name_get(
    FX_MEDIA *media_ptr, 
    CHAR *source_short_name,
    UCHAR *destination_unicode_name, 
    ULONG *destination_unicode_length);
```

### <a name="description"></a><span data-ttu-id="9969a-3515">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3515">Description</span></span>

<span data-ttu-id="9969a-3516">Questo servizio recupera il nome Unicode associato al nome breve fornito (formato 8.3) all'interno della directory predefinita corrente. Non sono consentite informazioni sul percorso nel parametro short name.</span><span class="sxs-lookup"><span data-stu-id="9969a-3516">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="9969a-3517">In caso di esito positivo, il nome Unicode associato al nome breve viene restituito dal servizio.</span><span class="sxs-lookup"><span data-stu-id="9969a-3517">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-3518">*Questo servizio può essere usato per ottenere nomi Unicode per file e sottodirectory.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3518">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3519">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3519">Input Parameters</span></span>

- <span data-ttu-id="9969a-3520">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-3520">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-3521">**short_name** Puntatore al nome breve (formato 8.3).</span><span class="sxs-lookup"><span data-stu-id="9969a-3521">**short_name** Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="9969a-3522">**destination_unicode_name:** puntatore alla destinazione per il nome Unicode associato al nome breve fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3522">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="9969a-3523">**destination_unicode_length:** puntatore alla lunghezza del nome Unicode restituita.</span><span class="sxs-lookup"><span data-stu-id="9969a-3523">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3524">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3524">Return Values</span></span>

- <span data-ttu-id="9969a-3525">**FX_SUCCESS** (0x00) Recupero del nome Unicode riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3525">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="9969a-3526">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la tabella FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-3526">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="9969a-3527">**FX_FILE_CORRUPT** (0x08) Il file è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-3527">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="9969a-3528">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-3528">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-3529">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-3529">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-3530">**FX_NOT_FOUND** (0x04) Nome breve non trovato o dimensioni di destinazione Unicode troppo piccole.</span><span class="sxs-lookup"><span data-stu-id="9969a-3530">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="9969a-3531">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-3531">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-3532">**FX_PTR_ERROR** (0x18) Supporti o puntatori nome non validi.</span><span class="sxs-lookup"><span data-stu-id="9969a-3532">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="9969a-3533">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-3533">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3534">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3534">Allowed From</span></span>

<span data-ttu-id="9969a-3535">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3535">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3536">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3536">Example</span></span>

```c
FX_MEDIA             ram_disk;
UCHAR                 my_unicode_name[256*2];
ULONG                 unicode_name_length;

/* Get the Unicode name associated with the short name "ABC0~111.TXT".
    Note that the Unicode destination must have 2 times the
    number of maximum characters in the name. */

length = fx_unicode_name_get(&ram_disk, "ABC0~111.TXT", my_unicode_name, unicode_name_length);

/* If successful, the Unicode name is returned in "my_unicode_name". */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3537">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3537">See Also</span></span>

- <span data-ttu-id="9969a-3538">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3538">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-3539">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3539">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-3540">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3540">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-3541">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3541">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3542">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-3542">fx_file_close</span></span>
- <span data-ttu-id="9969a-3543">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3543">fx_file_create</span></span>
- <span data-ttu-id="9969a-3544">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3544">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-3545">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-3545">fx_file_delete</span></span>
- <span data-ttu-id="9969a-3546">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3546">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-3547">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3547">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3548">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3548">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-3549">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3549">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-3550">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3550">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-3551">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3551">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-3552">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-3552">fx_file_open</span></span>
- <span data-ttu-id="9969a-3553">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3553">fx_file_read</span></span>
- <span data-ttu-id="9969a-3554">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3554">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-3555">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3555">fx_file_rename</span></span>
- <span data-ttu-id="9969a-3556">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3556">fx_file_seek</span></span>
- <span data-ttu-id="9969a-3557">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3557">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-3558">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3558">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-3559">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-3559">fx_file_write</span></span>
- <span data-ttu-id="9969a-3560">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3560">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-3561">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3561">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-3562">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3562">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-3563">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3563">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_name_get_extended"></a><span data-ttu-id="9969a-3564">fx_unicode_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="9969a-3564">fx_unicode_name_get_extended</span></span>

<span data-ttu-id="9969a-3565">Ottiene il nome Unicode dal nome breve</span><span class="sxs-lookup"><span data-stu-id="9969a-3565">Gets Unicode name from short name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3566">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3566">Prototype</span></span>

```c
UINT fx_unicode_name_get_extended(
    FX_MEDIA *media_ptr,
    CHAR *source_short_name,
    UCHAR *destination_unicode_name,
    ULONG *destination_unicode_length,
    ULONG unicode_name_buffer_length);
```
### <a name="description"></a><span data-ttu-id="9969a-3567">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3567">Description</span></span>

<span data-ttu-id="9969a-3568">Questo servizio recupera il nome Unicode associato al nome breve fornito (formato 8.3) all'interno della directory predefinita corrente. Non sono consentite informazioni sul percorso nel parametro short name.</span><span class="sxs-lookup"><span data-stu-id="9969a-3568">This service retrieves the Unicode-name associated with the supplied short name (8.3 format) within the current default directory—no path information is allowed in the short name parameter.</span></span> <span data-ttu-id="9969a-3569">In caso di esito positivo, il nome Unicode associato al nome breve viene restituito dal servizio.</span><span class="sxs-lookup"><span data-stu-id="9969a-3569">If successful, the Unicode name associated with the short name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-3570">\*Questo servizio è identico a \***fx_unicode_name_get**, ad eccezione del chiamante che specifica le dimensioni del buffer Unicode di destinazione _come argomento di input. Ciò consente al servizio di garantire che non sovrascriva il buffer Unicode di destinazione_</span><span class="sxs-lookup"><span data-stu-id="9969a-3570">\*This service is identical to \***fx_unicode_name_get**_, except the caller supplies the size of the destination Unicode buffer as an input argument. This allows the service to guarantee that it will not overwrite the destination Unicode buffer_</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-3571">*Questo servizio può essere usato per ottenere nomi Unicode per file e sottodirectory.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3571">*This service can be used to get Unicode names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3572">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3572">Input Parameters</span></span>

- <span data-ttu-id="9969a-3573">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-3573">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-3574">**short_name:** puntatore al nome breve (formato 8.3).</span><span class="sxs-lookup"><span data-stu-id="9969a-3574">**short_name**: Pointer to short name (8.3 format).</span></span>
- <span data-ttu-id="9969a-3575">**destination_unicode_name:** puntatore alla destinazione per il nome Unicode associato al nome breve fornito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3575">**destination_unicode_name**: Pointer to the destination for the Unicode name associated with the supplied short name.</span></span>
- <span data-ttu-id="9969a-3576">**destination_unicode_length:** puntatore alla lunghezza del nome Unicode restituita.</span><span class="sxs-lookup"><span data-stu-id="9969a-3576">**destination_unicode_length**: Pointer to returned Unicode name length.</span></span>
- <span data-ttu-id="9969a-3577">**unicode_name_buffer_length**: dimensione del buffer dei nomi Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3577">**unicode_name_buffer_length**: Size of the Unicode name buffer.</span></span> <span data-ttu-id="9969a-3578">Nota: è necessario un carattere di terminazione NULL, che crea un byte aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="9969a-3578">Note: A NULL terminator is required, which makes an extra byte.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3579">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3579">Return Values</span></span>

- <span data-ttu-id="9969a-3580">**FX_SUCCESS** (0x00) Recupero del nome Unicode riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3580">**FX_SUCCESS** (0x00) Successful Unicode name retrieval.</span></span>
- <span data-ttu-id="9969a-3581">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la tabella FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-3581">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="9969a-3582">**FX_FILE_CORRUPT** file (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-3582">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="9969a-3583">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-3583">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-3584">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-3584">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-3585">**FX_NOT_FOUND** (0x04) Nome breve non trovato o dimensioni di destinazione Unicode troppo piccole.</span><span class="sxs-lookup"><span data-stu-id="9969a-3585">**FX_NOT_FOUND** (0x04) Short name was not found or the Unicode destination size is too small.</span></span>
- <span data-ttu-id="9969a-3586">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-3586">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-3587">**FX_PTR_ERROR** (0x18) Supporti o puntatori del nome non validi.</span><span class="sxs-lookup"><span data-stu-id="9969a-3587">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="9969a-3588">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-3588">**FX_CALLER_ERROR** (0x20) Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3589">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3589">Allowed From</span></span>

<span data-ttu-id="9969a-3590">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3590">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3591">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3591">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             my_unicode_name[256*2];
ULONG             unicode_name_length;

/* Get the Unicode name associated with the short name "ABC0~111.TXT".
    Note that the Unicode destination must have 2 times the number of maximum characters in the name. */

length = fx_unicode_name_get_extended(&ram_disk, "ABC0~111.TXT",
    my_unicode_name,&unicode_name_length, sizeof(ny_unicode_name));

/* If successful, the Unicode name is returned in "my_unicode_name". */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3592">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3592">See Also</span></span>

- <span data-ttu-id="9969a-3593">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3593">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-3594">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3594">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-3595">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3595">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-3596">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3596">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3597">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-3597">fx_file_close</span></span>
- <span data-ttu-id="9969a-3598">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3598">fx_file_create</span></span>
- <span data-ttu-id="9969a-3599">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3599">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-3600">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-3600">fx_file_delete</span></span>
- <span data-ttu-id="9969a-3601">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3601">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-3602">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3602">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3603">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3603">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-3604">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3604">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-3605">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3605">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-3606">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3606">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-3607">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-3607">fx_file_open</span></span>
- <span data-ttu-id="9969a-3608">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3608">fx_file_read</span></span>
- <span data-ttu-id="9969a-3609">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3609">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-3610">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3610">fx_file_rename</span></span>
- <span data-ttu-id="9969a-3611">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3611">fx_file_seek</span></span>
- <span data-ttu-id="9969a-3612">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3612">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-3613">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3613">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-3614">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-3614">fx_file_write</span></span>
- <span data-ttu-id="9969a-3615">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3615">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-3616">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3616">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-3617">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3617">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-3618">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3618">fx_unicode_short_name_get</span></span>

## <a name="fx_unicode_short_name_get"></a><span data-ttu-id="9969a-3619">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3619">fx_unicode_short_name_get</span></span>

<span data-ttu-id="9969a-3620">Ottiene il nome breve dal nome Unicode</span><span class="sxs-lookup"><span data-stu-id="9969a-3620">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3621">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3621">Prototype</span></span>

```c
UINT fx_unicode_short_name_get(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length,
    CHAR *destination_short_name);
```

<span data-ttu-id="9969a-3622">Questo servizio recupera il nome breve (formato 8.3) associato al nome Unicode all'interno della directory predefinita corrente. Non sono consentite informazioni sul percorso nel parametro del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3622">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="9969a-3623">In caso di esito positivo, il nome breve associato al nome Unicode viene restituito dal servizio.</span><span class="sxs-lookup"><span data-stu-id="9969a-3623">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-3624">*Questo servizio può essere usato per ottenere nomi brevi sia per i file che per le sottodirectory.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3624">*This service can be used to get short names for both files and subdirectories.*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3625">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3625">Input Parameters</span></span>

- <span data-ttu-id="9969a-3626">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-3626">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-3627">**source_unicode_name:** puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3627">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="9969a-3628">**source_unicode_length**: lunghezza del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3628">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="9969a-3629">**destination_short_name**: puntatore alla destinazione per il nome breve (formato 8.3).</span><span class="sxs-lookup"><span data-stu-id="9969a-3629">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="9969a-3630">La dimensione deve essere di almeno 13 byte.</span><span class="sxs-lookup"><span data-stu-id="9969a-3630">This must be at least 13 bytes in size.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3631">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3631">Return Values</span></span>

- <span data-ttu-id="9969a-3632">**FX_SUCCESS** (0x00) Recupero nome breve riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3632">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="9969a-3633">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la tabella FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-3633">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="9969a-3634">**FX_FILE_CORRUPT** file (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-3634">**FX_FILE_CORRUPT** (0x08) File is corrupted</span></span>
- <span data-ttu-id="9969a-3635">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-3635">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-3636">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-3636">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-3637">**FX_NOT_FOUND** non è stato 0x04 il nome Unicode (0x04).</span><span class="sxs-lookup"><span data-stu-id="9969a-3637">**FX_NOT_FOUND** (0x04)    Unicode name was not found.</span></span>
- <span data-ttu-id="9969a-3638">**FX_NOT_IMPLEMENTED** (0x22) non implementato per le file system exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-3638">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="9969a-3639">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-3639">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-3640">**FX_PTR_ERROR** (0x18) Supporti o puntatori del nome non validi.</span><span class="sxs-lookup"><span data-stu-id="9969a-3640">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="9969a-3641">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-3641">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3642">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3642">Allowed From</span></span>

<span data-ttu-id="9969a-3643">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3643">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3644">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3644">Example</span></span>

```c
FX_MEDIA         ram_disk;
UCHAR             my_short_name[13];
UCHAR             my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                     0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                     0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                     0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                     0x63,0x00, 0x00,0x00};

/* Get the short name associated with the Unicode name contained in the array "my_unicode_name". */

length = fx_unicode_short_name_get(&ram_disk, my_unicode_name, 17, my_short_name);

/* If successful, the short name is returned in "my_short_name". */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3645">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3645">See Also</span></span>

- <span data-ttu-id="9969a-3646">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3646">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-3647">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3647">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-3648">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3648">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-3649">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3649">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3650">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-3650">fx_file_close</span></span>
- <span data-ttu-id="9969a-3651">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3651">fx_file_create</span></span>
- <span data-ttu-id="9969a-3652">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3652">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-3653">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-3653">fx_file_delete</span></span>
- <span data-ttu-id="9969a-3654">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3654">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-3655">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3655">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3656">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3656">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-3657">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3657">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-3658">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3658">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-3659">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3659">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-3660">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-3660">fx_file_open</span></span>
- <span data-ttu-id="9969a-3661">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3661">fx_file_read</span></span>
- <span data-ttu-id="9969a-3662">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3662">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-3663">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3663">fx_file_rename</span></span>
- <span data-ttu-id="9969a-3664">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3664">fx_file_seek</span></span>
- <span data-ttu-id="9969a-3665">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3665">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-3666">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3666">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-3667">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-3667">fx_file_write</span></span>
- <span data-ttu-id="9969a-3668">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3668">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-3669">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3669">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-3670">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3670">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-3671">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3671">fx_unicode_name_get</span></span>

## <a name="fx_unicode_short_name_get_extended"></a><span data-ttu-id="9969a-3672">fx_unicode_short_name_get_extended</span><span class="sxs-lookup"><span data-stu-id="9969a-3672">fx_unicode_short_name_get_extended</span></span>

<span data-ttu-id="9969a-3673">Ottiene il nome breve dal nome Unicode</span><span class="sxs-lookup"><span data-stu-id="9969a-3673">Gets short name from Unicode name</span></span>

### <a name="prototype"></a><span data-ttu-id="9969a-3674">Prototipo</span><span class="sxs-lookup"><span data-stu-id="9969a-3674">Prototype</span></span>

```c
UINT fx_unicode_short_name_get_extended(
    FX_MEDIA *media_ptr,
    UCHAR *source_unicode_name,
    ULONG source_unicode_length, 
    CHAR *destination_short_name,
    ULONG short_name_buffer_length);
```

### <a name="description"></a><span data-ttu-id="9969a-3675">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9969a-3675">Description</span></span>

<span data-ttu-id="9969a-3676">Questo servizio recupera il nome breve (formato 8.3) associato al nome Unicode all'interno della directory predefinita corrente. Non sono consentite informazioni sul percorso nel parametro del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3676">This service retrieves the short name (8.3 format) associated with the Unicode-name within the current default directory—no path information is allowed in the Unicode name parameter.</span></span> <span data-ttu-id="9969a-3677">In caso di esito positivo, il nome breve associato al nome Unicode viene restituito dal servizio.</span><span class="sxs-lookup"><span data-stu-id="9969a-3677">If successful, the short name associated with the Unicode name is returned by the service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9969a-3678">*Questo servizio è identico **a fx_unicode_short_name_get()**, ad eccezione del fatto che il chiamante fornisce le dimensioni del buffer di destinazione come argomento di input. Ciò consente al servizio di garantire che il nome breve non superi il buffer di destinazione.*</span><span class="sxs-lookup"><span data-stu-id="9969a-3678">*This service is identical to **fx_unicode_short_name_get()**, except the caller supplies the size of the destination buffer as an input argument. This allows the service to guarantee the short name does not exceed the destination buffer.*</span></span>

<span data-ttu-id="9969a-3679">*Questo servizio può essere usato per ottenere nomi brevi sia per i file che per le sottodirectory*</span><span class="sxs-lookup"><span data-stu-id="9969a-3679">*This service can be used to get short names for both files and subdirectories*</span></span>

### <a name="input-parameters"></a><span data-ttu-id="9969a-3680">Parametri di input</span><span class="sxs-lookup"><span data-stu-id="9969a-3680">Input Parameters</span></span>

- <span data-ttu-id="9969a-3681">**media_ptr:** puntatore al blocco di controllo multimediale.</span><span class="sxs-lookup"><span data-stu-id="9969a-3681">**media_ptr**: Pointer to media control block.</span></span>
- <span data-ttu-id="9969a-3682">**source_unicode_name:** puntatore al nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3682">**source_unicode_name**: Pointer to Unicode name.</span></span>
- <span data-ttu-id="9969a-3683">**source_unicode_length**: lunghezza del nome Unicode.</span><span class="sxs-lookup"><span data-stu-id="9969a-3683">**source_unicode_length**: Length of Unicode name.</span></span>
- <span data-ttu-id="9969a-3684">**destination_short_name**: puntatore alla destinazione per il nome breve (formato 8.3).</span><span class="sxs-lookup"><span data-stu-id="9969a-3684">**destination_short_name**: Pointer to destination for the short name (8.3 format).</span></span> <span data-ttu-id="9969a-3685">La dimensione deve essere di almeno 13 byte.</span><span class="sxs-lookup"><span data-stu-id="9969a-3685">This must be at least 13 bytes in size.</span></span>
- <span data-ttu-id="9969a-3686">**short_name_buffer_length**: dimensioni del buffer di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9969a-3686">**short_name_buffer_length**: Size of the destination buffer.</span></span> <span data-ttu-id="9969a-3687">La dimensione del buffer deve essere di almeno 14 byte.</span><span class="sxs-lookup"><span data-stu-id="9969a-3687">The buffer size must be at least 14 bytes.</span></span>

### <a name="return-values"></a><span data-ttu-id="9969a-3688">Valori restituiti</span><span class="sxs-lookup"><span data-stu-id="9969a-3688">Return Values</span></span>

- <span data-ttu-id="9969a-3689">**FX_SUCCESS** (0x00) Recupero nome breve riuscito.</span><span class="sxs-lookup"><span data-stu-id="9969a-3689">**FX_SUCCESS** (0x00) Successful short name retrieval.</span></span>
- <span data-ttu-id="9969a-3690">**FX_FAT_READ_ERROR** (0x03) Impossibile leggere la tabella FAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-3690">**FX_FAT_READ_ERROR** (0x03) Unable to read FAT table.</span></span>
- <span data-ttu-id="9969a-3691">**FX_FILE_CORRUPT** file (0x08) è danneggiato</span><span class="sxs-lookup"><span data-stu-id="9969a-3691">**FX_FILE_CORRUPT** (0x08)    File is corrupted</span></span>
- <span data-ttu-id="9969a-3692">**FX_IO_ERROR** errore di I/O del driver 0x90 (0x90).</span><span class="sxs-lookup"><span data-stu-id="9969a-3692">**FX_IO_ERROR** (0x90) Driver I/O error.</span></span>
- <span data-ttu-id="9969a-3693">**FX_MEDIA_NOT_OPEN** (0x11) Il supporto specificato non è aperto.</span><span class="sxs-lookup"><span data-stu-id="9969a-3693">**FX_MEDIA_NOT_OPEN** (0x11) Specified media is not open.</span></span>
- <span data-ttu-id="9969a-3694">**FX_NOT_FOUND** non è stato 0x04 il nome Unicode (0x04).</span><span class="sxs-lookup"><span data-stu-id="9969a-3694">**FX_NOT_FOUND** (0x04) Unicode name was not found.</span></span>
- <span data-ttu-id="9969a-3695">**FX_NOT_IMPLEMENTED** servizio (0x22) non implementato per l'file system exFAT.</span><span class="sxs-lookup"><span data-stu-id="9969a-3695">**FX_NOT_IMPLEMENTED** (0x22) Service not implemented for exFAT file system.</span></span>
- <span data-ttu-id="9969a-3696">**FX_SECTOR_INVALID** (0x89) Settore non valido.</span><span class="sxs-lookup"><span data-stu-id="9969a-3696">**FX_SECTOR_INVALID** (0x89) Invalid sector.</span></span>
- <span data-ttu-id="9969a-3697">**FX_PTR_ERROR** (0x18) Supporti o puntatori nome non validi.</span><span class="sxs-lookup"><span data-stu-id="9969a-3697">**FX_PTR_ERROR** (0x18) Invalid media or name pointers.</span></span>
- <span data-ttu-id="9969a-3698">**FX_CALLER_ERROR** (0x20) Caller non è un thread.</span><span class="sxs-lookup"><span data-stu-id="9969a-3698">**FX_CALLER_ERROR** (0x20)    Caller is not a thread.</span></span>

### <a name="allowed-from"></a><span data-ttu-id="9969a-3699">Consentito da</span><span class="sxs-lookup"><span data-stu-id="9969a-3699">Allowed From</span></span>

<span data-ttu-id="9969a-3700">Thread</span><span class="sxs-lookup"><span data-stu-id="9969a-3700">Threads</span></span>

### <a name="example"></a><span data-ttu-id="9969a-3701">Esempio</span><span class="sxs-lookup"><span data-stu-id="9969a-3701">Example</span></span>

```c
#define         SHORT_NAME_BUFFER_SIZE 13
FX_MEDIA         ram_disk;
UCHAR             my_short_name[SHORT_NAME_BUFFER_SIZE];
UCHAR             my_unicode_name[] = {0x38,0xC1, 0x88,0xBC, 0xF8,0xC9, 0x20,0x00,
                                     0x54,0xD6, 0x7C,0xC7, 0x20,0x00, 0x74,0xC7,
                                     0x84,0xB9, 0x20,0x00, 0x85,0xC7, 0xC8,0xB2,
                                     0xE4,0xB2, 0x2E,0x00, 0x64,0x00, 0x6F,0x00,
                                     0x63,0x00, 0x00,0x00};

/* Get the short name associated with the Unicode name contained in the array "my_unicode_name". */

length = fx_unicode_short_name_get_extended(&ram_disk,
    my_unicode_name, 17, my_short_name,SHORT_NAME_BUFFER_SIZE);

/* If successful, the short name is returned in "my_short_name". */
```

### <a name="see-also"></a><span data-ttu-id="9969a-3702">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9969a-3702">See Also</span></span>

- <span data-ttu-id="9969a-3703">fx_file_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3703">fx_file_allocate</span></span>
- <span data-ttu-id="9969a-3704">fx_file_attributes_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3704">fx_file_attributes_read</span></span>
- <span data-ttu-id="9969a-3705">fx_file_attributes_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3705">fx_file_attributes_set</span></span>
- <span data-ttu-id="9969a-3706">fx_file_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3706">fx_file_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3707">fx_file_close</span><span class="sxs-lookup"><span data-stu-id="9969a-3707">fx_file_close</span></span>
- <span data-ttu-id="9969a-3708">fx_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3708">fx_file_create</span></span>
- <span data-ttu-id="9969a-3709">fx_file_date_time_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3709">fx_file_date_time_set</span></span>
- <span data-ttu-id="9969a-3710">fx_file_delete</span><span class="sxs-lookup"><span data-stu-id="9969a-3710">fx_file_delete</span></span>
- <span data-ttu-id="9969a-3711">fx_file_extended_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3711">fx_file_extended_allocate</span></span>
- <span data-ttu-id="9969a-3712">fx_file_extended_best_effort_allocate</span><span class="sxs-lookup"><span data-stu-id="9969a-3712">fx_file_extended_best_effort_allocate</span></span>
- <span data-ttu-id="9969a-3713">fx_file_extended_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3713">fx_file_extended_relative_seek</span></span>
- <span data-ttu-id="9969a-3714">fx_file_extended_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3714">fx_file_extended_seek</span></span>
- <span data-ttu-id="9969a-3715">fx_file_extended_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3715">fx_file_extended_truncate</span></span>
- <span data-ttu-id="9969a-3716">fx_file_extended_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3716">fx_file_extended_truncate_release</span></span>
- <span data-ttu-id="9969a-3717">fx_file_open</span><span class="sxs-lookup"><span data-stu-id="9969a-3717">fx_file_open</span></span>
- <span data-ttu-id="9969a-3718">fx_file_read</span><span class="sxs-lookup"><span data-stu-id="9969a-3718">fx_file_read</span></span>
- <span data-ttu-id="9969a-3719">fx_file_relative_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3719">fx_file_relative_seek</span></span>
- <span data-ttu-id="9969a-3720">fx_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3720">fx_file_rename</span></span>
- <span data-ttu-id="9969a-3721">fx_file_seek</span><span class="sxs-lookup"><span data-stu-id="9969a-3721">fx_file_seek</span></span>
- <span data-ttu-id="9969a-3722">fx_file_truncate</span><span class="sxs-lookup"><span data-stu-id="9969a-3722">fx_file_truncate</span></span>
- <span data-ttu-id="9969a-3723">fx_file_truncate_release</span><span class="sxs-lookup"><span data-stu-id="9969a-3723">fx_file_truncate_release</span></span>
- <span data-ttu-id="9969a-3724">fx_file_write</span><span class="sxs-lookup"><span data-stu-id="9969a-3724">fx_file_write</span></span>
- <span data-ttu-id="9969a-3725">fx_file_write_notify_set</span><span class="sxs-lookup"><span data-stu-id="9969a-3725">fx_file_write_notify_set</span></span>
- <span data-ttu-id="9969a-3726">fx_unicode_file_create</span><span class="sxs-lookup"><span data-stu-id="9969a-3726">fx_unicode_file_create</span></span>
- <span data-ttu-id="9969a-3727">fx_unicode_file_rename</span><span class="sxs-lookup"><span data-stu-id="9969a-3727">fx_unicode_file_rename</span></span>
- <span data-ttu-id="9969a-3728">fx_unicode_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3728">fx_unicode_name_get</span></span>
- <span data-ttu-id="9969a-3729">fx_unicode_short_name_get</span><span class="sxs-lookup"><span data-stu-id="9969a-3729">fx_unicode_short_name_get</span></span>
